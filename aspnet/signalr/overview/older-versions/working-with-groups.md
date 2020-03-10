---
uid: signalr/overview/older-versions/working-with-groups
title: Práce se skupinami v nástroji Signal 1. x | Microsoft Docs
author: bradygaster
description: Toto téma popisuje, jak zachovat informace o členství ve skupinách pomocí rozhraní API centra.
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: 22929efd-68c9-4609-b76d-f8ba42fda01e
msc.legacyurl: /signalr/overview/older-versions/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: 5f50dc162d6cdcfbf2261e6a751f5f99078d5c54
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579364"
---
# <a name="working-with-groups-in-signalr-1x"></a>Práce se skupinami v knihovně SignalR 1.x

autorem [Fletcher](https://github.com/pfletcher), který [FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Toto téma popisuje, jak přidat uživatele do skupin a zachovat informace o členství ve skupinách.

## <a name="overview"></a>Přehled

Skupiny v nástroji Signal poskytují metodu pro vysílání zpráv pro zadané podmnožiny připojených klientů. Skupina může mít libovolný počet klientů a klient může být členem libovolného počtu skupin. Nemusíte explicitně vytvářet skupiny. V důsledku toho se skupina automaticky vytvoří při prvním zadání názvu ve volání skupin. Add a odstraní se, když odeberete Poslední připojení z členství v něm. Úvod k používání skupin najdete v tématu [Správa členství ve skupinách z třídy hub](index.md) v průvodci servery rozhraní API centra.

Neexistuje žádné rozhraní API pro získání seznamu členství ve skupině nebo seznamu skupin. Signal odesílá zprávy klientům a skupinám na základě modelu Pub/sub a server neudržuje seznamy skupin nebo členství ve skupinách. To pomáhá maximalizovat škálovatelnost, protože kdykoli přidáte uzel do webové farmy, všechny stavy, které tento signál udržuje, musí být šířeny do nového uzlu.

Když přidáte uživatele do skupiny pomocí metody `Groups.Add`, uživatel obdrží zprávy směrované do této skupiny po dobu trvání aktuálního připojení, ale členství uživatele v této skupině není trvale po aktuálním připojení. Pokud chcete trvale uchovávat informace o skupinách a členství ve skupinách, musíte tato data uložit v úložišti, jako je databáze nebo Azure Table Storage. Pak se pokaždé, když se uživatel připojí k vaší aplikaci, načte z úložiště, do kterého uživatel patří, a ručně do těchto skupin přidá tohoto uživatele.

Po opětovném připojení po dočasném přerušení se uživatel automaticky znovu připojí k dříve přiřazeným skupinám. Automatické opětovné připojení skupiny platí pouze při opětovném připojení, nikoli při vytváření nového připojení. Z klienta, který obsahuje seznam dříve přiřazených skupin, se předává digitálně podepsaný token. Pokud chcete ověřit, jestli uživatel patří do požadovaných skupin, můžete přepsat výchozí chování.

Toto téma obsahuje následující oddíly:

- [Přidávání a odebírání uživatelů](#add)
- [Volání členů skupiny](#call)
- [Ukládání členství ve skupinách v databázi](#storedatabase)
- [Ukládání členství ve skupinách ve službě Azure Table Storage](#storeazuretable)
- [Ověřování členství ve skupině při opětovném připojení](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a>Přidávání a odebírání uživatelů

Chcete-li přidat nebo odebrat uživatele ze skupiny, zavolejte metody [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) nebo [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) a jako parametry předejte ID připojení uživatele a název skupiny. Po ukončení připojení není nutné ručně odebrat uživatele ze skupiny.

Následující příklad ukazuje metody `Groups.Add` a `Groups.Remove` použité v metodách hub.

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

Metody `Groups.Add` a `Groups.Remove` provádějí asynchronně.

Chcete-li přidat klienta do skupiny a okamžitě odeslat zprávu klientovi pomocí skupiny, je nutné zajistit, aby byla metoda groups. Add nejprve dokončena. Následující příklady kódu ukazují, jak to provést, pomocí kódu, který funguje v rozhraní .NET 4,5 a jeden pomocí kódu, který funguje v rozhraní .NET 4.

#### <a name="asynchronous-net-45-example"></a>Příklad asynchronního rozhraní .NET 4,5

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

#### <a name="asynchronous-net-4-example"></a>Příklad asynchronního rozhraní .NET 4

[!code-csharp[Main](working-with-groups/samples/sample3.cs?highlight=3-4)]

Obecně platí, že byste neměli při volání metody `Groups.Remove` zahrnovat `await`, protože ID připojení, které se pokoušíte odebrat, možná nebude k dispozici. V takovém případě je `TaskCanceledException` vyvolána po vypršení časového limitu žádosti. Pokud vaše aplikace musí zajistit, aby byl uživatel ze skupiny odebraný před odesláním zprávy do skupiny, můžete přidat `await` před skupiny. odeberte a pak Zachyťte výjimku `TaskCanceledException`, která může být vyvolána.

<a id="call"></a>

## <a name="calling-members-of-a-group"></a>Volání členů skupiny

Můžete posílat zprávy všem členům skupiny nebo pouze určeným členům skupiny, jak je znázorněno v následujících příkladech.

- **Všichni** připojení klienti v zadané skupině. 

    [!code-css[Main](working-with-groups/samples/sample4.css)]
- Všechny připojené klienty v zadané skupině **s výjimkou určených klientů**identifikovaných podle ID připojení 

    [!code-csharp[Main](working-with-groups/samples/sample5.cs)]
- Všichni připojení klienti v zadané skupině **s výjimkou volajícího klienta**. 

    [!code-css[Main](working-with-groups/samples/sample6.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a>Ukládání členství ve skupinách v databázi

Následující příklady ukazují, jak uchovávat informace o skupinách a uživatelích v databázi. Můžete použít libovolnou technologii pro přístup k datům; Následující příklad však ukazuje, jak definovat modely pomocí Entity Framework. Tyto modely entit odpovídají tabulkám a polím databáze. Vaše datová struktura se může značně lišit v závislosti na požadavcích vaší aplikace. Tento příklad obsahuje třídu s názvem `ConversationRoom`, která by byla jedinečná pro aplikaci, která umožňuje uživatelům připojit se ke konverzaci o různých předmětech, jako je například sportovní nebo zahradnické. Tento příklad také obsahuje třídu pro připojení. Třída Connection není bezpodmínečně nutná pro sledování členství ve skupině, ale je často součástí robustního řešení pro sledování uživatelů.

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

Pak můžete v centru získat informace o skupině a uživateli z databáze a ručně přidat uživatele do příslušných skupin. Příklad nezahrnuje kód pro sledování připojení uživatelů. V tomto příkladu není klíčové slovo `await` použito před `Groups.Add`, protože zpráva není odeslána přímo do členů skupiny. Pokud chcete všem členům skupiny poslat zprávu hned po přidání nového člena, budete chtít použít klíčové slovo `await`, abyste se ujistili, že se asynchronní operace dokončila.

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a>Ukládání členství ve skupinách ve službě Azure Table Storage

Použití úložiště tabulek v Azure k ukládání informací o skupině a uživateli se podobá použití databáze. Následující příklad ukazuje entitu tabulky, která ukládá uživatelské jméno a název skupiny.

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

V centru načtěte přiřazené skupiny při připojení uživatele.

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a>Ověřování členství ve skupině při opětovném připojení

Ve výchozím nastavení Signal automaticky znovu přiřadí uživatele do příslušných skupin při opětovném připojení k dočasnému přerušení, například při přerušení připojení a opětovném navázání před vypršením časového limitu připojení. Informace o skupině uživatele se při opětovném připojení předávají do tokenu a tento token se ověří na serveru. Informace o procesu ověřování pro opětovné připojení uživatelů ke skupinám najdete v tématu opětovné připojení [skupin při opětovném připojení](index.md).

Obecně platí, že při opětovném připojení byste měli použít výchozí chování automaticky znovu připojit skupiny. Skupiny signalizace nejsou určeny jako mechanismus zabezpečení pro omezení přístupu k citlivým datům. Pokud ale vaše aplikace musí při opětovném připojení dvakrát ověřit členství uživatele ve skupině, můžete výchozí chování přepsat. Změna výchozího chování může do databáze přidat zatížení, protože členství uživatele ve skupině musí být načteno pro každé opětovné připojení, nikoli pouze při připojení uživatele.

Pokud je nutné ověřit členství ve skupině při opětovném připojení, vytvořte nový modul kanálu rozbočovače, který vrátí seznam přiřazených skupin, jak je uvedeno níže.

[!code-csharp[Main](working-with-groups/samples/sample11.cs)]

Pak tento modul přidejte do kanálu rozbočovače, jak je zvýrazněno níže.

[!code-csharp[Main](working-with-groups/samples/sample12.cs?highlight=10)]

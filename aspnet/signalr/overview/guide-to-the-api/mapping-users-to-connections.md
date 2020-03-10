---
uid: signalr/overview/guide-to-the-api/mapping-users-to-connections
title: Mapování uživatelů signalizace na připojení | Microsoft Docs
author: bradygaster
description: V tomto tématu se dozvíte, jak uchovávat informace o uživatelích a jejich připojeních. Saminí Fletcher pomáhá psát toto téma. Verze softwaru používané v tomto tématu...
ms.author: bradyg
ms.date: 12/30/2014
ms.assetid: f80c08b1-3f1f-432c-980c-c7b6edeb31b1
msc.legacyurl: /signalr/overview/guide-to-the-api/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: d55d40848e1e9d40570850c3552b225235c5e814
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536776"
---
# <a name="mapping-signalr-users-to-connections"></a>Mapování uživatelů knihovny SignalR na připojení

tím, že [FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> V tomto tématu se dozvíte, jak uchovávat informace o uživatelích a jejich připojeních.
>
> Saminí Fletcher pomáhá psát toto téma.
>
> ## <a name="software-versions-used-in-this-topic"></a>Verze softwaru používané v tomto tématu
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - Signal – verze 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Předchozí verze tohoto tématu
>
> Informace o dřívějších verzích nástroje Signal najdete v části [Signal – starší verze](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Dotazy a komentáře
>
> Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky. Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).

## <a name="introduction"></a>Úvod

Každý klient připojující se k centru projde jedinečným identifikátorem připojení. Tuto hodnotu můžete načíst ve vlastnosti `Context.ConnectionId` v kontextu centra. Pokud vaše aplikace potřebuje mapovat uživatele na ID připojení a zachovat toto mapování, můžete použít jednu z následujících možností:

- [Poskytovatel ID uživatele (Signal 2)](#IUserIdProvider)
- [Úložiště v paměti](#inmemory), jako je například slovník
- [Skupina signálů pro každého uživatele](#groups)
- [Trvalé, externí úložiště](#database), například databázová tabulka nebo Azure Table Storage

Každá z těchto implementací je uvedena v tomto tématu. Pomocí metod `OnConnected`, `OnDisconnected`a `OnReconnected` třídy `Hub` můžete sledovat stav připojení uživatele.

Nejlepší přístup k vaší aplikaci závisí na:

- Počet webových serverů, které hostují vaši aplikaci.
- Bez ohledu na to, zda potřebujete získat seznam aktuálně připojených uživatelů.
- Bez ohledu na to, jestli je potřeba zachovat informace o skupinách a uživatelích při restartování aplikace nebo serveru.
- Zda je latence volání externího serveru problémem.

Následující tabulka ukazuje, jaký přístup k těmto hlediskům funguje.

|  | Více než jeden server | Získat seznam aktuálně připojených uživatelů | Uchovat informace po restartování | Optimální výkon |
| --- | --- | --- | --- | --- |
| Poskytovatel UserID | ![](mapping-users-to-connections/_static/image1.png) |  |  | ![](mapping-users-to-connections/_static/image2.png) |
| V paměti |  | ![](mapping-users-to-connections/_static/image3.png) |  | ![](mapping-users-to-connections/_static/image4.png) |
| Skupiny s jedním uživatelem | ![](mapping-users-to-connections/_static/image5.png) |  |  | ![](mapping-users-to-connections/_static/image6.png) |
| Trvalé, externí | ![](mapping-users-to-connections/_static/image7.png) | ![](mapping-users-to-connections/_static/image8.png) | ![](mapping-users-to-connections/_static/image9.png) |  |

<a id="IUserIdProvider"></a>

## <a name="iuserid-provider"></a>Poskytovatel IUserID

Tato funkce umožňuje uživatelům určit, co je ID uživatele založené na IRequest prostřednictvím nového rozhraní IUserIdProvider.

**IUserIdProvider**

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

Ve výchozím nastavení bude k dispozici implementace, která jako uživatelské jméno používá `IPrincipal.Identity.Name` uživatele. Pokud to chcete změnit, zaregistrujte implementaci `IUserIdProvider` s globálním hostitelem při spuštění aplikace:

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

V rámci centra budete moct posílat zprávy těmto uživatelům pomocí následujícího rozhraní API:

**Odeslání zprávy konkrétnímu uživateli**

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs?highlight=5)]

<a id="inmemory"></a>

## <a name="in-memory-storage"></a>Úložiště v paměti

Následující příklady ukazují, jak uchovávat informace o připojení a uživatelích ve slovníku, který je uložený v paměti. Slovník používá `HashSet` k uložení ID připojení. V každém okamžiku může mít uživatel více než jedno připojení k aplikaci signalizace. Například uživatel, který je připojen prostřednictvím více zařízení nebo více než jedna karta prohlížeče, bude mít více než jedno ID připojení.

Pokud se aplikace ukončí, ztratí se všechny informace, ale budou se znovu naplnit, protože uživatelé znovu naváže připojení. Úložiště v paměti nefunguje, pokud vaše prostředí obsahuje více než jeden webový server, protože každý server by měl samostatnou kolekci připojení.

První příklad ukazuje třídu, která spravuje mapování uživatelů na připojení. Klíčem pro HashSet – budou uživatelské jméno.

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

Další příklad ukazuje, jak použít třídu mapování připojení z rozbočovače. Instance třídy je uložena v názvu proměnné `_connections`.

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a>Skupiny s jedním uživatelem

Můžete vytvořit skupinu pro každého uživatele a poté odeslat zprávu do této skupiny, pokud chcete pouze kontaktovat tohoto uživatele. Název každé skupiny je jméno uživatele. Pokud má uživatel více než jedno připojení, každé ID připojení se přidá do skupiny uživatelů.

Nemusíte ručně odebrat uživatele ze skupiny, když se uživatel odpojí. Tato akce je automaticky prováděna architekturou Signal.

Následující příklad ukazuje, jak implementovat skupiny s jedním uživatelem.

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a>Trvalé, externí úložiště

V tomto tématu se dozvíte, jak použít databázi nebo úložiště tabulek Azure pro ukládání informací o připojení. Tento přístup funguje, když máte více webových serverů, protože každý webový server může komunikovat se stejným úložištěm dat. Pokud vaše webové servery přestanou pracovat nebo se aplikace restartuje, není volána metoda `OnDisconnected`. Proto je možné, že úložiště dat bude obsahovat záznamy pro ID připojení, která již nejsou platná. Chcete-li vyčistit tyto osamocené záznamy, můžete chtít zrušit platnost všech připojení, která byla vytvořena mimo časový rámec, který je pro vaši aplikaci relevantní. Příklady v této části obsahují hodnotu pro sledování při vytvoření připojení, ale neukazují, jak vyčistit staré záznamy, protože je vhodné to udělat jako proces na pozadí.

### <a name="database"></a>databáze

Následující příklady ukazují, jak uchovávat informace o připojení a uživatelích v databázi. Můžete použít libovolnou technologii pro přístup k datům; Následující příklad však ukazuje, jak definovat modely pomocí Entity Framework. Tyto modely entit odpovídají tabulkám a polím databáze. Vaše datová struktura se může značně lišit v závislosti na požadavcích vaší aplikace.

První příklad ukazuje, jak definovat entitu uživatele, která může být přidružena k mnoha entitám připojení.

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

Pak z centra můžete sledovat stav každého připojení s níže uvedeným kódem.

[!code-csharp[Main](mapping-users-to-connections/samples/sample8.cs)]

<a id="azure"></a>
### <a name="azure-table-storage"></a>Azure Table Storage

Následující příklad služby Azure Table Storage je podobný jako příklad databáze. Nezahrnuje všechny informace, které byste museli začít s Azure Table Storage Service. Informace najdete v tématu [použití úložiště Table z rozhraní .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).

Následující příklad ukazuje entitu tabulky pro ukládání informací o připojení. Rozdělí data podle uživatelského jména a identifikují každou entitu podle ID připojení, takže uživatel může mít kdykoli více připojení.

[!code-csharp[Main](mapping-users-to-connections/samples/sample9.cs)]

V centru sledujete stav připojení každého uživatele.

[!code-csharp[Main](mapping-users-to-connections/samples/sample10.cs)]

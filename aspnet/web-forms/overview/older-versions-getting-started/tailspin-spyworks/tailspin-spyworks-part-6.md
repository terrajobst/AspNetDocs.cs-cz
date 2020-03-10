---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
title: '6\. část: ASP.NET členství | Microsoft Docs'
author: JoeStagner
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 6 přidává ASP.NET členství.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: f70a310c-9557-4743-82cb-655265676d39
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-6
msc.type: authoredcontent
ms.openlocfilehash: b0caa89dc9ffb5bb7451fa2d9d346c7db2bf1466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78564181"
---
# <a name="part-6-aspnet-membership"></a>6\. část: Členství v ASP.NET

[Jana Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks ukazuje, jak neobyčejně jednoduché je vytvářet výkonné a škálovatelné aplikace pro platformu .NET. Ukazuje, jak používat Skvělé nové funkce v ASP.NET 4 k vytvoření online obchodu, včetně nákupu, rezervace a správy.
> 
> V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 6 přidává ASP.NET členství.

## <a id="_Toc260221672"></a>Práce s ASP.NET členstvím

![](tailspin-spyworks-part-6/_static/image1.png)

Klikněte na zabezpečení.

![](tailspin-spyworks-part-6/_static/image1.jpg)

Ujistěte se, že používáme ověřování pomocí formulářů.

![](tailspin-spyworks-part-6/_static/image2.jpg)

Pomocí odkazu vytvořit uživatele můžete vytvořit několik uživatelů.

![](tailspin-spyworks-part-6/_static/image3.jpg)

Až budete hotovi, přečtěte si okno Průzkumník řešení a aktualizujte zobrazení.

![](tailspin-spyworks-part-6/_static/image2.png)

Všimněte si, že je k dispaměti ASPNETDB. Byla vytvořena pokuta MDF. Tento soubor obsahuje tabulky pro podporu základních služeb ASP.NET, jako je třeba členství.

Nyní můžeme začít s implementací procesu registrace.

Začněte vytvořením stránky rezervovat. aspx.

Stránka rezervovat. aspx by měla být k dispozici pouze uživatelům, kteří jsou přihlášeni, a proto omezíme přístup k přihlášeným uživatelům a uživatelům, kteří nejsou přihlášení k přihlašovací stránce, budou přesměrováni.

K tomu přidáme následující do konfiguračního oddílu souboru Web. config.

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample1.xml)]

Šablona pro aplikace webových formulářů ASP.NET automaticky přidala oddíl ověřování do našeho souboru Web. config a navázala výchozí přihlašovací stránku.

[!code-xml[Main](tailspin-spyworks-part-6/samples/sample2.xml)]

Pro migraci anonymního nákupního košíku, když se uživatel přihlásí, je nutné upravit soubor přihlašovacího jména. aspx. Následujícím způsobem změňte událost\_načíst stránku.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample3.cs)]

Pak přidejte obslužnou rutinu události "LoggedIn", například tuto hodnotu, chcete-li nastavit název relace na nově přihlášeného uživatele a změnit ID dočasné relace v nákupním košíku na uživatele voláním metody MigrateCart v naší třídě MyShoppingCart. (Implementováno v souboru. cs)

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample4.cs)]

Implementujte metodu MigrateCart (), jako to.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample5.cs)]

V rezervaci. aspx budeme na naší stránce rezervace používat EntityDataSource a GridView, což je mnohem stejně jako na naší stránce nákupního košíku.

[!code-aspx[Main](tailspin-spyworks-part-6/samples/sample6.aspx)]

Všimněte si, že náš ovládací prvek GridView Určuje obslužnou rutinu události "OnDataBound" s názvem MyList\_RowDataBound, takže implementuje tuto obslužnou rutinu události jako.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample7.cs)]

Tato metoda udržuje průběžný součet nákupního košíku, protože je každý řádek svázán a aktualizuje spodní řádek prvku GridView.

V této fázi jsme implementovali "kontrolu" pro objednávku, která se má umístit.

Pořídíme scénář prázdného vozíku přidáním několika řádků kódu na naši stránku\_události načtení:

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample8.cs)]

Když uživatel klikne na tlačítko Odeslat, spustí se v obslužné rutině události Click tlačítka pro odeslání následující kód.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample9.cs)]

"Maso" procesu odeslání objednávky je implementováno v metodě SubmitOrder () naší třídy MyShoppingCart.

SubmitOrder bude:

- Vezměte všechny řádkové položky v nákupním košíku a použijte je k vytvoření nového záznamu objednávky a přidružených záznamů OrderDetails.
- Vypočítat datum expedice.
- Vymažte nákupní košík.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample10.cs)]

Pro účely této ukázkové aplikace vypočítáme datum odeslání pouhým přidáním dvou dnů k aktuálnímu datu.

[!code-csharp[Main](tailspin-spyworks-part-6/samples/sample11.cs)]

Spuštění aplikace teď umožní otestovat nákupní proces od začátku do konce.

> [!div class="step-by-step"]
> [Předchozí](tailspin-spyworks-part-5.md)
> [Další](tailspin-spyworks-part-7.md)

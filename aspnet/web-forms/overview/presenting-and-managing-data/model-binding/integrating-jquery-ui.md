---
uid: web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
title: Integrace DatePicker uživatelského rozhraní JQuery s vazbami modelů a webovými formuláři | Microsoft Docs
author: Rick-Anderson
description: Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET. Vazba modelu umožňuje interakci dat více-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 3cbab37b-fb0f-4751-9ec4-74e068c3f380
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/integrating-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: c8d711dd44950116f3a3e09d5d12c507918c543f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78642476"
---
# <a name="integrating-jquery-ui-datepicker-with-model-binding-and-web-forms"></a>Integrace DatePicker uživatelského rozhraní JQuery s vazbami modelů a webovými formuláři

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET. Vazba modelu umožňuje, aby data byla v interakci s více přímým přesměrováním než při práci s objekty zdroje dat (například ObjectDataSource nebo SqlDataSource). Tato série začíná úvodním materiálem a v pozdějších kurzech přechází na pokročilejší koncepty.
> 
> V tomto kurzu se dozvíte, jak přidat [widget DatePicker](http://jqueryui.com/datepicker/) uživatelského rozhraní jQuery do webového formuláře a použít vazbu modelu k aktualizaci databáze s vybranou hodnotou.
> 
> Tento kurz sestaví na projektu vytvořeném v [první](retrieving-data.md) a [druhé](updating-deleting-and-creating-data.md) části řady.
> 
> Můžete [si stáhnout](https://go.microsoft.com/fwlink/?LinkId=286116) celý projekt v C# nebo VB. Kód ke stažení funguje buď se sadou Visual Studio 2012 nebo Visual Studio 2013. Používá šablonu sady Visual Studio 2012, která se mírně liší od Visual Studio 2013 šablony zobrazené v tomto kurzu.

## <a name="what-youll-build"></a>Co sestavíte

V tomto kurzu:

1. Přidejte do modelu vlastnost pro záznam data registrace studenta.
2. Povolit uživateli vybrat datum registrace pomocí widgetu DatePicker uživatelského rozhraní JQuery
3. Vyhovět ověřovacím pravidlům pro datum zápisu

Pomůcka DatePicker uživatelského rozhraní JQuery umožňuje uživatelům snadno vybrat datum z kalendáře, který se zobrazí, když uživatel pracuje s polem. Použití tohoto widgetu může být vhodnější pro uživatele, než ruční zadání data. Integrace widgetu DatePicker do stránky, která používá vazbu modelu pro datové operace, vyžaduje jenom malé množství další práce.

## <a name="add-a-new-property-to-the-model"></a>Přidat do modelu novou vlastnost

Nejprve do svého modelu studenta přidáte vlastnost **DateTime** a tuto změnu migrujete do databáze. Otevřete **UniversityModels.cs**a přidejte zvýrazněný kód do modelu studenta.

[!code-csharp[Main](integrating-jquery-ui/samples/sample1.cs?highlight=16-18)]

**RangeAttribute** je součástí pro vymáhání ověřovacích pravidel pro vlastnost. Pro účely tohoto kurzu předpokládáme, že je společnost Contoso University založená na 1. lednu 2013 a proto jsou dřívější data registrace neplatná.

V okně Správa balíčků přidejte migraci spuštěním příkazu **Add-Migration AddEnrollmentDate**. Všimněte si, že kód migrace přidá nový sloupec DateTime do tabulky student. Aby se shodovala s hodnotou, kterou jste zadali v RangeAttribute, přidejte výchozí hodnotu pro nový sloupec, jak je znázorněno v následujícím zvýrazněném kódu.

[!code-csharp[Main](integrating-jquery-ui/samples/sample2.cs?highlight=11)]

Uložte změny do souboru migrace.

Data nemusíte znovu naplnit. Proto ve složce migrace otevřete **Configuration.cs** a odeberte nebo Odkomentujte kód v metodě **osazení** . Uložte soubor a zavřete ho.

Nyní spusťte příkaz **Update-Database**. Všimněte si, že sloupec teď v databázi existuje a všechny existující záznamy mají výchozí hodnotu pro EnrollmentDate.

## <a name="add-dynamic-controls-for-enrollment-date"></a>Přidat dynamické ovládací prvky pro datum registrace

Nyní přidáte ovládací prvky pro zobrazení a úpravu data registrace. V tomto okamžiku je hodnota upravována prostřednictvím textového pole. Později v tomto kurzu změníte textové pole na widget JQuery DatePicker.

Nejprve je důležité si uvědomit, že nemusíte dělat žádné změny v souboru **AddStudent. aspx** . Ovládací prvek DynamicEntity automaticky vykreslí novou vlastnost.

Otevřete **studenty. aspx**a přidejte následující zvýrazněný kód.

[!code-aspx[Main](integrating-jquery-ui/samples/sample3.aspx?highlight=13)]

Spusťte aplikaci a Všimněte si, že můžete nastavit hodnotu pro datum zápisu zadáním data. Při přidávání nového studenta:

![nastavit datum](integrating-jquery-ui/_static/image1.png)

Nebo úprava existující hodnoty:

![Upravit datum](integrating-jquery-ui/_static/image2.png)

Zadání data funguje, ale nemusí se jednat o činnost zákazníka, kterou chcete poskytnout. V další části povolíte výběr data prostřednictvím kalendáře.

## <a name="install-nuget-package-to-work-with-jquery-ui"></a>Nainstalovat balíček NuGet pro práci s uživatelským rozhraním JQuery

Balíček NuGet **uživatelského rozhraní sady šťáv** umožňuje snadnou integraci WIDGETŮ uživatelského rozhraní jQuery do vaší webové aplikace. Pokud chcete tento balíček použít, nainstalujte ho přes NuGet.

![Přidat uživatelské rozhraní šťávy](integrating-jquery-ui/_static/image3.png)

Verze rozhraní, kterou nainstalujete, může být v konfliktu s verzí JQuery ve vaší aplikaci. Než budete pokračovat v tomto kurzu, zkuste aplikaci spustit. Pokud dojde k chybě JavaScriptu, je nutné sjednotit verzi JQuery. Můžete buď přidat očekávanou verzi JQuery do složky Scripts (1.8.2 verze v době psaní tohoto kurzu), nebo v souboru site. Master zadat cestu k souboru JQuery.

[!code-aspx[Main](integrating-jquery-ui/samples/sample4.aspx)]

## <a name="customize-datetime-template-to-include-datepicker-widget"></a>Přizpůsobit šablonu DateTime tak, aby zahrnovala widget DatePicker

Přidáte pomůcku DatePicker do šablony dynamických dat pro úpravu hodnoty DateTime. Přidáním widgetu do šablony se automaticky vykreslí ve formuláři pro přidání nového studenta a v zobrazení mřížky pro úpravy studentů. Otevřete **DateTime\_Edit. ascx**a přidejte následující zvýrazněný kód.

[!code-aspx[Main](integrating-jquery-ui/samples/sample5.aspx?highlight=3)]

V souboru kódu na pozadí nastavíte minimální a maximální datum pro DatePicker. Nastavením těchto hodnot zabráníte uživatelům přejít na neplatná data. Pokud je k dispozici, načtete minimální a maximální hodnoty z **RangeAttribute** ve vlastnosti DateTime. Otevřete **datový typ DateTime\_Edit.ascx.cs**a přidejte následující zvýrazněný kód na stránku\_načtení metody.

[!code-csharp[Main](integrating-jquery-ui/samples/sample6.cs?highlight=9-14)]

Spusťte webovou aplikaci a přejděte na stránku AddStudent. Zadejte hodnoty pro pole a Všimněte si, že po kliknutí na textové pole pro datum zápisu se zobrazí kalendář.

![Výběr data](integrating-jquery-ui/_static/image4.png)

Vyberte datum a klikněte na tlačítko **Vložit**. RangeAttribute vynutil ověřování na serveru. Nastavením vlastnosti minDate v DatePicker použijete také ověřování na straně klienta. Kalendář neumožní uživateli přejít na datum před hodnotou minDate.

Při úpravách záznamu v zobrazení mřížky se zobrazí také kalendář.

![DatePicker v prvku GridView](integrating-jquery-ui/_static/image5.png)

## <a name="conclusion"></a>Závěr

V tomto kurzu jste zjistili, jak začlenit widget JQuery do webového formuláře, který používá vazbu modelu.

V dalším [kurzu](using-query-string-values-to-retrieve-data.md)budete při výběru dat používat hodnotu řetězce dotazu.

> [!div class="step-by-step"]
> [Předchozí](sorting-paging-and-filtering-data.md)
> [Další](using-query-string-values-to-retrieve-data.md)

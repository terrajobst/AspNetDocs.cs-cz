---
uid: web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
title: Řazení, stránkování a filtrování dat pomocí vazeb modelů a webových formulářů | Microsoft Docs
author: Rick-Anderson
description: Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET. Vazba modelu umožňuje interakci dat více-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 266e7866-e327-4687-b29d-627a0925e87d
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/sorting-paging-and-filtering-data
msc.type: authoredcontent
ms.openlocfilehash: f8e64392af6110f36c6af98c4e4e9481c94a0d82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78548060"
---
# <a name="sorting-paging-and-filtering-data-with-model-binding-and-web-forms"></a>Řazení, stránkování a filtrování dat pomocí vazeb modelů a webových formulářů

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET. Vazba modelu umožňuje, aby data byla v interakci s více přímým přesměrováním než při práci s objekty zdroje dat (například ObjectDataSource nebo SqlDataSource). Tato série začíná úvodním materiálem a v pozdějších kurzech přechází na pokročilejší koncepty.
> 
> V tomto kurzu se dozvíte, jak přidat řazení, stránkování a filtrování dat prostřednictvím vazby modelu.
> 
> Tento kurz sestaví na projektu vytvořeném v první [části](retrieving-data.md) řady.
> 
> Můžete [si stáhnout](https://go.microsoft.com/fwlink/?LinkId=286116) celý projekt v C# nebo VB. Kód ke stažení funguje buď se sadou Visual Studio 2012 nebo Visual Studio 2013. Používá šablonu sady Visual Studio 2012, která se mírně liší od Visual Studio 2013 šablony zobrazené v tomto kurzu.

## <a name="what-youll-build"></a>Co sestavíte

V tomto kurzu:

1. Povolit řazení a stránkování dat
2. Povolit filtrování dat na základě výběru uživatelem

## <a name="add-sorting"></a>Přidat řazení

Povolení řazení v prvku GridView je velmi snadné. V souboru student. aspx stačí nastavit **AllowSorting** na **hodnotu true** v prvku GridView. Pro každý sloupec není nutné nastavovat hodnotu **SortExpression** , protože pole DataField je automaticky použito. Prvek GridView upraví dotaz tak, aby zahrnoval řazení dat podle vybrané hodnoty. Zvýrazněný kód ukazuje přidání, které je třeba provést, aby bylo možné řazení povolit.

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample1.aspx?highlight=5)]

Spuštění webové aplikace a testování záznamů studentů podle hodnot v různých sloupcích.

![Seřadit studenty](sorting-paging-and-filtering-data/_static/image2.png)

## <a name="add-paging"></a>Přidat stránkování

Povolení stránkování je také velmi snadné. V prvku GridView nastavte vlastnost **li AllowPaging nastavena** na **hodnotu true** a nastavte vlastnost **PageSize** na počet záznamů, které chcete zobrazit na každé stránce. V tomto kurzu ho můžete nastavit na 4.

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample2.aspx?highlight=5)]

Spusťte webovou aplikaci a Všimněte si, že nyní jsou záznamy rozděleny na více stránek s maximálně 4 záznamy zobrazenými na jedné stránce.

![Přidat stránkování](sorting-paging-and-filtering-data/_static/image4.png)

Odložené provádění dotazů vylepšuje efektivitu aplikace. Místo načtení celé datové sady prvek GridView upraví dotaz tak, aby načetl pouze záznamy pro aktuální stránku.

## <a name="filter-records-by-user-selection"></a>Filtrovat záznamy podle výběru uživatele

Vazba modelu přidá několik atributů, které umožňují určit, jak nastavit hodnotu pro parametr v metodě vazby modelu. Tyto atributy jsou v oboru názvů **System. Web. ModelBinding** . Patří mezi ně:

- Řízení
- Soubor cookie
- Formulář
- Profil
- Řetězec dotazu
- RouteData
- Relace
- Profilu
- ViewState

V tomto kurzu použijete hodnotu ovládacího prvku k filtrování, které záznamy se zobrazí v prvku GridView. Přidáte atribut **Control** do metody dotazu, kterou jste vytvořili dříve. V [pozdějším](using-query-string-values-to-retrieve-data.md) kurzu použijete atribut **QueryString** na parametr a určíte tak, že hodnota parametru pochází z hodnoty řetězce dotazu.

Nejdřív nad ovládací souhrnu ověření přidejte rozevírací seznam pro filtrování, které studenty se zobrazí.

[!code-aspx[Main](sorting-paging-and-filtering-data/samples/sample3.aspx?highlight=3-11)]

V souboru kódu na pozadí upravte metodu Select pro příjem hodnoty z ovládacího prvku a nastavte název parametru na název ovládacího prvku, který poskytuje hodnotu.

Pro vyřešení atributu ovládacího prvku je nutné přidat příkaz **using** pro obor názvů **System. Web. ModelBinding** .

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample4.cs)]

Následující kód ukazuje znovu vypracovanou metodu Select pro filtrování vrácených dat na základě hodnoty rozevíracího seznamu. Přidání atributu ovládacího prvku před parametr určuje, že hodnota pro tento parametr pochází z ovládacího prvku se stejným názvem.

[!code-csharp[Main](sorting-paging-and-filtering-data/samples/sample5.cs)]

Pokud chcete filtrovat seznam studentů, spusťte webovou aplikaci a v rozevíracím seznamu vyberte jiné hodnoty.

![filtrovat studenty](sorting-paging-and-filtering-data/_static/image6.png)

## <a name="conclusion"></a>Závěr

V tomto kurzu jste povolili řazení a stránkování dat. Také jste povolili filtrování dat podle hodnoty ovládacího prvku.

V dalším [kurzu](integrating-jquery-ui.md) vylepšíte uživatelské rozhraní integrací WIDGETU uživatelského rozhraní jQuery do šablony dynamických dat.

> [!div class="step-by-step"]
> [Předchozí](updating-deleting-and-creating-data.md)
> [Další](integrating-jquery-ui.md)

---
uid: web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
title: Použití hodnot řetězce dotazu k filtrování dat s vazbami modelů a webovými formuláři | Microsoft Docs
author: Rick-Anderson
description: Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET. Vazba modelu umožňuje interakci dat více-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: b90978bd-795d-4871-9ade-1671caff5730
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/using-query-string-values-to-retrieve-data
msc.type: authoredcontent
ms.openlocfilehash: 143ddcb40b576a3129e659b90bfc8321c061a547
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639095"
---
# <a name="using-query-string-values-to-filter-data-with-model-binding-and-web-forms"></a>Použití hodnot řetězce dotazu k filtrování dat s vazbami modelů a webovými formuláři

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET. Vazba modelu umožňuje, aby data byla v interakci s více přímým přesměrováním než při práci s objekty zdroje dat (například ObjectDataSource nebo SqlDataSource). Tato série začíná úvodním materiálem a v pozdějších kurzech přechází na pokročilejší koncepty.
> 
> V tomto kurzu se dozvíte, jak předat hodnotu v řetězci dotazu a použít tuto hodnotu k načtení dat prostřednictvím vazby modelu.
> 
> Tento kurz sestaví na projektu vytvořeném v [předchozích](retrieving-data.md) částech řady.
> 
> Můžete [si stáhnout](https://go.microsoft.com/fwlink/?LinkId=286116) celý projekt v C# nebo VB. Kód ke stažení funguje buď se sadou Visual Studio 2012 nebo Visual Studio 2013. Používá šablonu sady Visual Studio 2012, která se mírně liší od Visual Studio 2013 šablony zobrazené v tomto kurzu.

## <a name="what-youll-build"></a>Co sestavíte

V tomto kurzu:

1. Přidání nové stránky pro zobrazení zaregistrovaných kurzů pro studenta
2. Načte zaregistrované kurzy pro vybraného studenta na základě hodnoty v řetězci dotazu.
3. Přidání hypertextového odkazu s hodnotou řetězce dotazu ze zobrazení mřížky na novou stránku

Postup v tomto kurzu se podobá tomu, co jste provedli v předchozím [kurzu](sorting-paging-and-filtering-data.md) , chcete-li filtrovat zobrazené studenty na základě výběru uživatele v rozevíracím seznamu. V tomto kurzu jste pomocí atributu **Control** v metodě SELECT určili, že hodnota parametru pochází z ovládacího prvku. V tomto kurzu použijete atribut **QueryString** v metodě SELECT k určení, že hodnota parametru pochází z řetězce dotazu.

## <a name="add-new-page-for-displaying-a-students-courses"></a>Přidání nové stránky pro zobrazení kurzů studenta

Přidejte nový webový formulář, který používá hlavní stránku Web. Master, a pojmenujte si **kurzy**stránky.

V souboru **kurzů. aspx** přidejte zobrazení mřížky pro zobrazení kurzů pro vybraného studenta.

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample1.aspx)]

## <a name="define-the-select-method"></a>Definování metody Select

V **courses.aspx.cs**přidáte metodu Select s názvem, který jste zadali ve vlastnosti **SelectMethod** zobrazení mřížky. V této metodě definujete dotaz pro načtení kurzů studenta a určíte, že parametr pochází z hodnoty řetězce dotazu se stejným názvem, jako má parametr.

Nejprve je třeba přidat následující příkazy **using** .

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample2.cs)]

Pak do Courses.aspx.cs přidejte následující kód:

[!code-csharp[Main](using-query-string-values-to-retrieve-data/samples/sample3.cs)]

Atribut QueryString znamená, že hodnota řetězce dotazu s názvem StudentID je automaticky přiřazena k parametru v této metodě.

## <a name="add-hyperlink-with-query-string-value"></a>Přidat hypertextový odkaz s hodnotou řetězce dotazu

V zobrazení mřížky na studenty. aspx přidáte pole hypertextového odkazu, které odkazuje na stránku nových kurzů. Hypertextový odkaz bude obsahovat hodnotu řetězce dotazu s ID studenta.

V části studenty. aspx přidejte následující pole do sloupců zobrazení mřížky pod polem pro celkové kredity.

[!code-aspx[Main](using-query-string-values-to-retrieve-data/samples/sample4.aspx?highlight=7-8)]

Spusťte aplikaci a Všimněte si, že zobrazení mřížky teď obsahuje odkaz kurzy.

![Přidat hypertextový odkaz](using-query-string-values-to-retrieve-data/_static/image1.png)

Po kliknutí na jeden z odkazů se zobrazí zaregistrované kurzy tohoto studenta.

![Zobrazit kurzy](using-query-string-values-to-retrieve-data/_static/image2.png)

## <a name="conclusion"></a>Závěr

V tomto kurzu jste přidali odkaz s hodnotou řetězce dotazu. Tuto hodnotu řetězce dotazu jste použili pro hodnotu parametru v metodě SELECT.

V dalším [kurzu](adding-business-logic-layer.md)přesunete kód ze souborů kódu na pozadí do vrstvy obchodní logiky a do vrstvy přístupu k datům.

> [!div class="step-by-step"]
> [Předchozí](integrating-jquery-ui.md)
> [Další](adding-business-logic-layer.md)

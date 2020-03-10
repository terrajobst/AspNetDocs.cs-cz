---
uid: web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
title: Aktualizace, odstraňování a vytváření dat s vazbami modelů a webovými formuláři | Microsoft Docs
author: Rick-Anderson
description: Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET. Vazba modelu umožňuje interakci dat více-...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 602baa94-5a4f-46eb-a717-7a9e539c1db4
msc.legacyurl: /web-forms/overview/presenting-and-managing-data/model-binding/updating-deleting-and-creating-data
msc.type: authoredcontent
ms.openlocfilehash: 11dc52ec79ca91119b37ea60e08164eb1b1d0e2b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586644"
---
# <a name="updating-deleting-and-creating-data-with-model-binding-and-web-forms"></a>Aktualizace, odstraňování a vytváření dat pomocí vazeb modelů a webových formulářů

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tato série kurzů ukazuje základní aspekty použití vazby modelu s projektem webových formulářů ASP.NET. Vazba modelu umožňuje, aby data byla v interakci s více přímým přesměrováním než při práci s objekty zdroje dat (například ObjectDataSource nebo SqlDataSource). Tato série začíná úvodním materiálem a v pozdějších kurzech přechází na pokročilejší koncepty.
> 
> V tomto kurzu se dozvíte, jak vytvářet, aktualizovat a odstraňovat data s vazbou modelu. Nastavíte následující vlastnosti:
> 
> - DeleteMethod
> - Určena metoda InsertMethod
> - UpdateMethod
> 
> Tyto vlastnosti obdrží název metody, která zpracovává odpovídající operaci. V rámci této metody poskytnete logiku pro interakci s daty.
> 
> Tento kurz sestaví na projektu vytvořeném v první [části](retrieving-data.md) řady.
> 
> Můžete [si stáhnout](https://go.microsoft.com/fwlink/?LinkId=286116) celý projekt v C# nebo VB. Kód ke stažení funguje buď se sadou Visual Studio 2012 nebo Visual Studio 2013. Používá šablonu sady Visual Studio 2012, která se mírně liší od Visual Studio 2013 šablony zobrazené v tomto kurzu.

## <a name="what-youll-build"></a>Co sestavíte

V tomto kurzu:

1. Přidat šablony dynamických dat
2. Povolení aktualizace a odstraňování dat prostřednictvím metod vazby modelu
3. Použití pravidel ověřování dat – povolení vytvoření nového záznamu v databázi

## <a name="add-dynamic-data-templates"></a>Přidat šablony dynamických dat

Pro zajištění nejlepšího uživatelského prostředí a minimalizaci opakování kódu budete používat šablony dynamických dat. Předem připravené šablony dynamických dat můžete snadno integrovat do stávající lokality instalací balíčku NuGet.

Z okna **Spravovat balíčky NuGet**nainstalujte **DynamicDataTemplatesCS**.

![šablony dynamických dat](updating-deleting-and-creating-data/_static/image1.png)

Všimněte si, že projekt teď obsahuje složku s názvem **DynamicData**. V této složce se nacházejí šablony, které jsou automaticky aplikovány na dynamické ovládací prvky ve webových formulářích.

![Složka s dynamickými daty](updating-deleting-and-creating-data/_static/image2.png)

## <a name="enable-updating-and-deleting"></a>Povolit aktualizace a odstraňování

Umožnění uživatelům aktualizovat a odstraňovat záznamy v databázi se velmi podobá procesu načítání dat. Ve vlastnostech **UpdateMethod** a **DeleteMethod** zadáte názvy metod, které provádějí tyto operace. Pomocí ovládacího prvku GridView můžete také zadat automatické generování tlačítek upravit a odstranit. Následující zvýrazněný kód ukazuje přidání do kódu GridView.

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample1.aspx?highlight=4-5)]

V souboru kódu na pozadí přidejte příkaz using pro **System. data. entity. Infrastructure**.

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample2.cs)]

Pak přidejte následující metody Update a DELETE.

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample3.cs)]

Metoda **TryUpdateModel** aplikuje odpovídající hodnoty vázaných na data z webového formuláře na datovou položku. Datová položka se načte na základě hodnoty parametru ID.

## <a name="enforce-validation-requirements"></a>Vynutilit požadavky na ověření

Atributy ověřování, které jste použili u vlastností FirstName, LastName a year ve třídě student, se automaticky vynutily při aktualizaci dat. Ovládací prvky DynamicField přidávají validátory klientů a serverů na základě ověřovacích atributů. Vlastnosti FirstName a LastName jsou povinné. FirstName nesmí být delší než 20 znaků a příjmení nesmí být delší než 40 znaků. Hodnota Year musí být platná pro výčet AcademicYear.

Pokud uživatel porušuje jeden z požadavků na ověření, aktualizace nepokračuje. Chcete-li zobrazit chybovou zprávu, přidejte ovládací prvek ovládací souhrnu ověření nad prvek GridView. Chcete-li zobrazit chyby ověřování z vazby modelu, nastavte vlastnost **ShowModelStateErrors** na **hodnotu true**. 

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample4.aspx)]

Spusťte webovou aplikaci a aktualizujte a odstraňte všechny záznamy.

![aktualizovat data](updating-deleting-and-creating-data/_static/image3.png)

Všimněte si, že když se v režimu úprav hodnota vlastnosti Year automaticky vykreslí jako rozevírací seznam. Vlastnost year je hodnota výčtu a šablona dynamická data pro hodnotu výčtu Určuje rozevírací seznam pro úpravy. Tuto šablonu můžete najít tak, že otevřete **výčet\_upravit soubor. ascx** ve složce **DynamicData**/**FieldTemplates** .

Pokud zadáte platné hodnoty, aktualizace se úspěšně dokončí. Pokud porušujete jeden z požadavků na ověření, aktualizace nebude pokračovat a zobrazí se chybová zpráva nad mřížkou.

![chybová zpráva](updating-deleting-and-creating-data/_static/image4.png)

## <a name="add-new-records"></a>Přidat nové záznamy

Ovládací prvek GridView nezahrnuje vlastnost **určena metoda InsertMethod** , a proto nemůže být použit pro přidání nového záznamu s vazbou modelu. Vlastnost určena metoda InsertMethod můžete najít v ovládacích prvcích **FormView**, **DetailsView**nebo **ListView** . V tomto kurzu použijete ovládací prvek FormView k přidání nového záznamu.

Nejdřív přidejte odkaz na novou stránku, kterou vytvoříte pro přidání nového záznamu. Nad ovládací souhrnu ověření přidejte:

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample5.aspx)]

Nový odkaz se zobrazí v horní části obsahu pro stránku students.

![nový odkaz](updating-deleting-and-creating-data/_static/image5.png)

Pak přidejte nový webový formulář pomocí stránky předlohy a pojmenujte ho **AddStudent**. Jako hlavní stránku vyberte site. Master.

Pole pro přidání nového studenta vygenerujete pomocí ovládacího prvku **DynamicEntity** . Ovládací prvek DynamicEntity vykreslí tyto upravitelné vlastnosti ve třídě určené vlastností ItemType. Vlastnost StudentID byla označena atributem **[ScaffoldColumn (false)]** , takže není vykreslena. Do zástupného textu MainContent stránky AddStudent přidejte následující kód.

[!code-aspx[Main](updating-deleting-and-creating-data/samples/sample6.aspx)]

V souboru kódu na pozadí (AddStudent.aspx.cs) přidejte příkaz **using** pro obor názvů **ContosoUniversityModelBinding. Models** .

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample7.cs)]

Pak přidejte následující metody pro určení způsobu vložení nového záznamu a obslužné rutiny události pro tlačítko Storno.

[!code-csharp[Main](updating-deleting-and-creating-data/samples/sample8.cs)]

Uložte všechny změny.

Spusťte webovou aplikaci a vytvořte nového studenta.

![Přidat nového studenta](updating-deleting-and-creating-data/_static/image6.png)

Klikněte na **Vložit** a Všimněte si, že se vytvořil nový student.

![Zobrazit nového studenta](updating-deleting-and-creating-data/_static/image7.png)

## <a name="conclusion"></a>Závěr

V tomto kurzu jste povolili aktualizace, odstraňování a vytváření dat. Pravidla ověřování se používají při interakci s daty.

V dalším [kurzu](sorting-paging-and-filtering-data.md) v této sérii budete umožňovat řazení, stránkování a filtrování dat.

> [!div class="step-by-step"]
> [Předchozí](retrieving-data.md)
> [Další](sorting-paging-and-filtering-data.md)

---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
title: Vazba na přiznávání (C#) | Microsoft Docs
author: wenz
description: Řízení přiznávání v ovládacím prvku AJAX Control Toolkit poskytuje více podoken a umožňuje uživateli zobrazit jeden z nich najednou. Panely jsou obvykle deklarovány w...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9c8f0054-e319-46f8-80c0-35b606d2fbd4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-cs
msc.type: authoredcontent
ms.openlocfilehash: 6c28cc958a1de9844627ae16175a5aed153993a8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607275"
---
# <a name="databinding-to-an-accordion-c"></a>Datová vazba ovládacího prvku Accordion (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1CS.pdf)

> Řízení přiznávání v ovládacím prvku AJAX Control Toolkit poskytuje více podoken a umožňuje uživateli zobrazit jeden z nich najednou. Panely jsou obvykle deklarovány v rámci samotné stránky, ale vazba na zdroj dat nabízí větší flexibilitu.

## <a name="overview"></a>Přehled

Řízení přiznávání v ovládacím prvku AJAX Control Toolkit poskytuje více podoken a umožňuje uživateli zobrazit jeden z nich najednou. Panely jsou obvykle deklarovány v rámci samotné stránky, ale vazba na zdroj dat nabízí větší flexibilitu.

## <a name="steps"></a>Uvedené

Nejdříve je vyžadován zdroj dat. V této ukázce se používá databáze AdventureWorks a edice Microsoft SQL Server 2005 Express. Databáze je volitelnou součástí instalace sady Visual Studio (včetně Express Edition) a je k dispozici také jako samostatné stažení v rámci [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064). Databáze AdventureWorks je součástí ukázek SQL Server 2005 a ukázkových databází (Stáhnout v [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Nejjednodušší způsob, jak nastavit databázi, je použít Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) a připojit soubor databáze `AdventureWorks.mdf`.

V této ukázce předpokládáme, že instance SQL Server 2005 Express Edition se nazývá `SQLEXPRESS` a nachází se na stejném počítači jako webový server. Toto je také výchozí nastavení. Pokud se instalace liší, je nutné upravit informace o připojení pro databázi.

Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample1.aspx)]

Pak přidejte zdroj dat na stránku. Aby bylo možné použít omezené množství dat, vyberte pouze prvních pět záznamů v tabulce dodavatelů databáze AdventureWorks. Pokud k vytvoření zdroje dat používáte pomocníka sady Visual Studio, pamatujte, že chyba v aktuální verzi neprefixuje název tabulky (`Vendor`) s `Purchasing`. Následující kód ukazuje správnou syntaxi:

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample2.aspx)]

Zapamatujte si název (ID) zdroje dat. Tato velmi identifikace musí být použita ve vlastnosti `DataSourceID` ovládacího prvku pro přiznávání:

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample3.aspx)]

V rámci řízení přiznávání můžete poskytnout šablony pro různé části ovládacího prvku, včetně hlavičky (`<HeaderTemplate>`) a obsahu (`<ContentTemplate>`). V rámci těchto elementů stačí výstup dat ze zdroje dat pomocí metody `DataBinder.Eval()`:

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample4.aspx)]

Po načtení stránky musí být zdroj dat vázán na toto souhlasu s tímto kódem na straně serveru:

[!code-aspx[Main](databinding-to-an-accordion-cs/samples/sample5.aspx)]

Chcete-li uzavřít tuto ukázku, je nutné definovat dvě třídy šablony stylů CSS, na které se odkazuje v řízení přiznávání (ve vlastnostech `HeaderCssClass` a `ContentCssClass`). Do části `<head>` stránky vložte následující kód:

[!code-css[Main](databinding-to-an-accordion-cs/samples/sample6.css)]

[![se data v přiznávání nacházejí přímo ze zdroje dat.](databinding-to-an-accordion-cs/_static/image2.png)](databinding-to-an-accordion-cs/_static/image1.png)

Data v přiznávání přicházejí přímo ze zdroje dat ([kliknutím zobrazíte obrázek v plné velikosti).](databinding-to-an-accordion-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Next](dynamically-adding-an-accordion-pane-cs.md)

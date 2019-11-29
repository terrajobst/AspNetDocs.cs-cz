---
uid: web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
title: Vazba na přiznávání (VB) | Microsoft Docs
author: wenz
description: Řízení přiznávání v ovládacím prvku AJAX Control Toolkit poskytuje více podoken a umožňuje uživateli zobrazit jeden z nich najednou. Panely jsou obvykle deklarovány w...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: b19f0875-7d3e-4ecf-baa1-a0c693c765b3
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/accordion/databinding-to-an-accordion-vb
msc.type: authoredcontent
ms.openlocfilehash: bfb31940c0395c7ed1d5d471fb8fb686b66c59ad
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599956"
---
# <a name="databinding-to-an-accordion-vb"></a>Datová vazba ovládacího prvku Accordion (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/5/6/d/56d50cef-2011-4c8f-9891-7edc6dc57df9/Accordion1.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/accordion1VB.pdf)

> Řízení přiznávání v ovládacím prvku AJAX Control Toolkit poskytuje více podoken a umožňuje uživateli zobrazit jeden z nich najednou. Panely jsou obvykle deklarovány v rámci samotné stránky, ale vazba na zdroj dat nabízí větší flexibilitu.

## <a name="overview"></a>Přehled

Řízení přiznávání v ovládacím prvku AJAX Control Toolkit poskytuje více podoken a umožňuje uživateli zobrazit jeden z nich najednou. Panely jsou obvykle deklarovány v rámci samotné stránky, ale vazba na zdroj dat nabízí větší flexibilitu.

## <a name="steps"></a>Uvedené

Nejdříve je vyžadován zdroj dat. V této ukázce se používá databáze AdventureWorks a edice Microsoft SQL Server 2005 Express. Databáze je volitelnou součástí instalace sady Visual Studio (včetně Express Edition) a je k dispozici také jako samostatné stažení v rámci [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064). Databáze AdventureWorks je součástí ukázek SQL Server 2005 a ukázkových databází (Stáhnout v [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Nejjednodušší způsob, jak nastavit databázi, je použít Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) a připojit soubor databáze `AdventureWorks.mdf`.

V této ukázce předpokládáme, že instance SQL Server 2005 Express Edition se nazývá `SQLEXPRESS` a nachází se na stejném počítači jako webový server. Toto je také výchozí nastavení. Pokud se instalace liší, je nutné upravit informace o připojení pro databázi.

Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample1.aspx)]

Pak přidejte zdroj dat na stránku. Aby bylo možné použít omezené množství dat, vyberte pouze prvních pět záznamů v tabulce dodavatelů databáze AdventureWorks. Pokud k vytvoření zdroje dat používáte pomocníka sady Visual Studio, pamatujte, že chyba v aktuální verzi neprefixuje název tabulky (`Vendor`) s `Purchasing`. Následující kód ukazuje správnou syntaxi:

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample2.aspx)]

Zapamatujte si název (ID) zdroje dat. Tato velmi identifikace musí být použita ve vlastnosti `DataSourceID` ovládacího prvku pro přiznávání:

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample3.aspx)]

V rámci řízení přiznávání můžete poskytnout šablony pro různé části ovládacího prvku, včetně hlavičky (`<HeaderTemplate>`) a obsahu (`<ContentTemplate>`). V rámci těchto elementů stačí výstup dat ze zdroje dat pomocí metody `DataBinder.Eval()`:

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample4.aspx)]

Po načtení stránky musí být zdroj dat vázán na toto souhlasu s tímto kódem na straně serveru:

[!code-aspx[Main](databinding-to-an-accordion-vb/samples/sample5.aspx)]

Chcete-li uzavřít tuto ukázku, je nutné definovat dvě třídy šablony stylů CSS, na které se odkazuje v řízení přiznávání (ve vlastnostech `HeaderCssClass` a `ContentCssClass`). Do části `<head>` stránky vložte následující kód:

[!code-css[Main](databinding-to-an-accordion-vb/samples/sample6.css)]

[![se data v přiznávání nacházejí přímo ze zdroje dat.](databinding-to-an-accordion-vb/_static/image2.png)](databinding-to-an-accordion-vb/_static/image1.png)

Data v přiznávání přicházejí přímo ze zdroje dat ([kliknutím zobrazíte obrázek v plné velikosti).](databinding-to-an-accordion-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](dynamically-adding-an-accordion-pane-cs.md)
> [Další](dynamically-adding-an-accordion-pane-vb.md)

---
uid: web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
title: Použití ovládacího prvku textboxwatermark ve třídě FormView (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek ovládacího prvku textboxwatermark v sadě nástrojů AJAX Control Toolkit rozšiřuje textové pole tak, aby byl v poli zobrazen text. Když uživatel klikne do pole, i...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 41497361-7fba-4825-b36c-f58d79522a88
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/textboxwatermark/using-textboxwatermark-in-a-formview-vb
msc.type: authoredcontent
ms.openlocfilehash: 1dd17ed57383680122c4ca613ca71f6682dec40e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627104"
---
# <a name="using-textboxwatermark-in-a-formview-vb"></a>Použití ovládacího prvku TextBoxWatermark v ovládacím prvku FormView (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/TextBoxWatermark1.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/textboxwatermark1VB.pdf)

> Ovládací prvek ovládacího prvku textboxwatermark v sadě nástrojů AJAX Control Toolkit rozšiřuje textové pole tak, aby byl v poli zobrazen text. Když uživatel klikne na pole, bude vyprázdněn. Pokud uživatel opustí pole bez zadání textu, předem vyplněný text se zobrazí znovu. To je možné také v rámci ovládacího prvku FormView.

## <a name="overview"></a>Přehled

Ovládací prvek `TextBoxWatermark` v sadě nástrojů AJAX Control Toolkit rozšiřuje textové pole tak, aby byl v poli zobrazen text. Když uživatel klikne na pole, bude vyprázdněn. Pokud uživatel opustí pole bez zadání textu, předem vyplněný text se zobrazí znovu. To je možné také v rámci ovládacího prvku `FormView`.

## <a name="steps"></a>Kroky

Nejdříve je vyžadován zdroj dat. V této ukázce se používá databáze AdventureWorks a edice Microsoft SQL Server 2005 Express. Databáze je volitelnou součástí instalace sady Visual Studio (včetně Express Edition) a je k dispozici také jako samostatné stažení v rámci [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064). Databáze AdventureWorks je součástí ukázek SQL Server 2005 a ukázkových databází (Stáhnout v [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Nejjednodušší způsob, jak nastavit databázi, je použít Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) a připojit soubor databáze `AdventureWorks.mdf`.

V této ukázce předpokládáme, že instance SQL Server 2005 Express Edition se nazývá `SQLEXPRESS` a nachází se na stejném počítači jako webový server. Toto je také výchozí nastavení. Pokud se instalace liší, je nutné upravit informace o připojení pro databázi.

Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample1.aspx)]

Pak přidejte zdroj dat na stránku, která podporuje `DELETE`příkazy SQL `INSERT` a `UPDATE`. Pokud k vytvoření zdroje dat používáte pomocníka sady Visual Studio, pamatujte, že chyba v aktuální verzi neprefixuje název tabulky (`Vendor`) s `Purchasing`. Následující kód ukazuje správnou syntaxi:

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample2.aspx)]

Zapamatujte si název (`ID`) zdroje dat, protože bude použit ve vlastnosti `DataSourceID` ovládacího prvku `FormView`. Oddíl `<InsertItemTemplate>` `FormView` obsahuje textové pole, které je rozšířeno pomocí ovládacího prvku `TextBoxWatermarkExtender`. Ujistěte se, že se zařízení rozšiřuje v rámci šablony a není mimo něj.

[!code-aspx[Main](using-textboxwatermark-in-a-formview-vb/samples/sample3.aspx)]

Když se teď uživatel změní do režimu vkládání ovládacího prvku `FormView`, textové pole pro nového dodavatele se předem naplní s ohledem na ovládací prvek `TextBoxWatermarkExtender`. V textovém poli klikněte do textového pole. zmizí text výplně.

[![meze v poli pocházejících z rozšířeného objektu.](using-textboxwatermark-in-a-formview-vb/_static/image2.png)](using-textboxwatermark-in-a-formview-vb/_static/image1.png)

Meze v poli pochází z pole Extender ([kliknutím zobrazíte obrázek v plné velikosti).](using-textboxwatermark-in-a-formview-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](using-textboxwatermark-with-validation-controls-cs.md)
> [Další](using-textboxwatermark-with-validation-controls-vb.md)

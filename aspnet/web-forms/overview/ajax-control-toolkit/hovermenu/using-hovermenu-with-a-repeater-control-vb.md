---
uid: web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-vb
title: Použití nabídky hovermenu s ovládacím prvkem Repeater (VB) | Microsoft Docs
author: wenz
description: 'Ovládací prvek nabídky hovermenu v sadě nástrojů AJAX Control Toolkit poskytuje jednoduchý překryvný efekt: když ukazatel myši najede na prvek, zobrazí se automaticky otevírané okno...'
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 7f07c112-cd4f-4427-9699-57cfab2791fd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/hovermenu/using-hovermenu-with-a-repeater-control-vb
msc.type: authoredcontent
ms.openlocfilehash: 9386aa2fe3a6174bbed52218337107733cb1fa99
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78621574"
---
# <a name="using-hovermenu-with-a-repeater-control-vb"></a>Použití nabídky HoverMenu s ovládacím prvkem Repeater (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/b/0/6/b06fe835-5b8f-4c00-aef8-062c19d75b95/HoverMenu1.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/hovermenu1VB.pdf)

> Ovládací prvek nabídky hovermenu v sadě nástrojů AJAX Control Toolkit poskytuje jednoduchý překryvný efekt: když ukazatel myši najede myší na prvek, zobrazí se místní nabídka na zadané pozici. Tento ovládací prvek lze také použít v rámci Repeater.

## <a name="overview"></a>Přehled

Ovládací prvek `HoverMenu` v sadě nástrojů AJAX Control Toolkit poskytuje jednoduchý překryvný efekt: když ukazatel myši najede myší na prvek, zobrazí se místní nabídka na zadané pozici. Tento ovládací prvek lze také použít v rámci Repeater.

## <a name="steps"></a>Kroky

Nejdříve je vyžadován zdroj dat. V této ukázce se používá databáze AdventureWorks a edice Microsoft SQL Server 2005 Express. Databáze je volitelnou součástí instalace sady Visual Studio (včetně Express Edition) a je k dispozici také jako samostatné stažení v rámci [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064). Databáze AdventureWorks je součástí ukázek SQL Server 2005 a ukázkových databází (Stáhnout v [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Nejjednodušší způsob, jak nastavit databázi, je použít Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) a připojit soubor databáze `AdventureWorks.mdf`.

V této ukázce předpokládáme, že instance SQL Server 2005 Express Edition se nazývá `SQLEXPRESS` a nachází se na stejném počítači jako webový server. Toto je také výchozí nastavení. Pokud se instalace liší, je nutné upravit informace o připojení pro databázi.

Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample1.aspx)]

Pak přidejte zdroj dat na stránku. Aby bylo možné použít omezené množství dat, vyberte pouze prvních pět záznamů v tabulce dodavatelů databáze AdventureWorks. Pokud k vytvoření zdroje dat používáte pomocníka sady Visual Studio, pamatujte, že chyba v aktuální verzi neprefixuje název tabulky (`Vendor`) s `Purchasing`. Následující kód ukazuje správnou syntaxi:

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample2.aspx)]

Dále přidejte panel, který slouží jako modální automaticky otevíraná okna:

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample3.aspx)]

Nyní `HoverMenuExtender` přichází do hry. Aby každý prvek ve zdroji dat získá svou vlastní místní nabídku, musí být tento ovládací prvek vložen do oddílu `<ItemTemplate>` Repeater. Zde je značka:

[!code-aspx[Main](using-hovermenu-with-a-repeater-control-vb/samples/sample4.aspx)]

Po zpoždění 50 milisekund (`PopDelay` atribut) teď každá položka ve zdroji dat zobrazuje automaticky otevírané okno vpravo (`PopupPosition` atribut).

[![se vedle každé položky v poli Repeater zobrazí nabídka s efektem přechodu](using-hovermenu-with-a-repeater-control-vb/_static/image2.png)](using-hovermenu-with-a-repeater-control-vb/_static/image1.png)

Vedle každé položky v poli Repeater se zobrazí nabídka přechodu ([kliknutím zobrazíte obrázek v plné velikosti).](using-hovermenu-with-a-repeater-control-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](using-hovermenu-with-a-repeater-control-cs.md)

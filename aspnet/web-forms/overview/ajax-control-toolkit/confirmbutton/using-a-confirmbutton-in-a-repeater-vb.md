---
uid: web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
title: Použití extenderu confirmbutton v Repeater (VB) | Microsoft Docs
author: wenz
description: Pokud uživatel klikne na tlačítko (včetně ovládacího prvku LinkButton), vytvoří v ovládacím prvku AJAX Control Toolkit pro extenderu confirmbutton hodnotu Ano/ne. Pouze pokud ano...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 18c31709-3f9d-4d93-8b01-f1356bf610b4
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/confirmbutton/using-a-confirmbutton-in-a-repeater-vb
msc.type: authoredcontent
ms.openlocfilehash: 001233d866d8a731d93d6900f714cd2060f3d08c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613951"
---
# <a name="using-a-confirmbutton-in-a-repeater-vb"></a>Použití ovládacího prvku ConfirmButton v repeateru (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/8/6/d/86dea6c6-bb92-4fa6-aa14-f8c0f82100f5/ConfirmButton1.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/confirmbutton1VB.pdf)

> Pokud uživatel klikne na tlačítko (včetně ovládacího prvku LinkButton), vytvoří v ovládacím prvku AJAX Control Toolkit pro extenderu confirmbutton hodnotu Ano/ne. Pouze pokud kliknete na Ano, akce tlačítka se spustí, jinak se zruší. To je možné také v případě opakovače.

## <a name="overview"></a>Přehled

Pokud uživatel klikne na tlačítko (včetně ovládacího prvku LinkButton), vytvoří v ovládacím prvku AJAX Control Toolkit pro extenderu confirmbutton hodnotu Ano/ne. Pouze pokud kliknete na Ano, akce tlačítka se spustí, jinak se zruší. To je možné také v případě opakovače.

## <a name="steps"></a>Kroky

Nejdříve je vyžadován zdroj dat. V této ukázce se používá databáze AdventureWorks a edice Microsoft SQL Server 2005 Express. Databáze je volitelnou součástí instalace sady Visual Studio (včetně Express Edition) a je k dispozici také jako samostatné stažení v rámci [https://go.microsoft.com/fwlink/?LinkId=64064](https://go.microsoft.com/fwlink/?LinkId=64064). Databáze AdventureWorks je součástí ukázek SQL Server 2005 a ukázkových databází (Stáhnout v [https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;D isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=e719ecf7-9f46-4312-af89-6ad8702e4e6e&amp;DisplayLang=en)). Nejjednodušší způsob, jak nastavit databázi, je použít Microsoft SQL Server Management Studio Express ([https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;D isplaylang = EN](https://www.microsoft.com/downloads/details.aspx?FamilyID=c243a5ae-4bd1-4e3d-94b8-5a0f62bf7796&amp;DisplayLang=en)) a připojit soubor databáze `AdventureWorks.mdf`.

V této ukázce předpokládáme, že instance SQL Server 2005 Express Edition se nazývá `SQLEXPRESS` a nachází se na stejném počítači jako webový server. Toto je také výchozí nastavení. Pokud se instalace liší, je nutné upravit informace o připojení pro databázi.

Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample1.aspx)]

Pak je vyžadován zdroj dat. V zájmu jednoduchosti se načtou jenom prvních pět položek v tabulce dodavatelů AdventureWorks. Všimněte si, že při použití Průvodce sadou Visual Studio k vytvoření zdroje dat je název tabulky (`Vendors`) aktuálně bez správné předpony `Purchasing`. Následující značky jsou správné:

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample2.aspx)]

Tento zdroj dat pak můžete použít v rámci Repeater. V obvyklém případě metoda `DataBinder.Eval()` načítá data ze zdroje dat. Ovládací prvek `ConfirmButtonExtender` musí být umístěn v části `<ItemTemplate>` opakovače tak, aby se zobrazil pro všechny položky ve zdroji dat.

[!code-aspx[Main](using-a-confirmbutton-in-a-repeater-vb/samples/sample3.aspx)]

[![se vedle každé položky ze zdroje dat zobrazuje tlačítko Potvrdit](using-a-confirmbutton-in-a-repeater-vb/_static/image2.png)](using-a-confirmbutton-in-a-repeater-vb/_static/image1.png)

Tlačítko Potvrdit se zobrazí vedle každé položky ze zdroje dat ([kliknutím zobrazíte obrázek v plné velikosti).](using-a-confirmbutton-in-a-repeater-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](using-a-confirmbutton-in-a-repeater-cs.md)

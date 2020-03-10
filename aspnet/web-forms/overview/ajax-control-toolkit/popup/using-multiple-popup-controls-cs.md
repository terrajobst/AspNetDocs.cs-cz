---
uid: web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
title: Použití několika překryvných ovládacíchC#prvků () | Microsoft Docs
author: wenz
description: PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek. Je také možné použít m...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 91511b0b-311d-481f-9e7c-73f07b813b79
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/popup/using-multiple-popup-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 8700fe89af591e8b481e853580b0efa0cddbf1bc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78612649"
---
# <a name="using-multiple-popup-controls-c"></a>Použití několika překryvných ovládacích prvků (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PopupControl1.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/popupcontrol1CS.pdf)

> PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek. Je také možné použít více než jeden ovládací prvek místní nabídky na jedné stránce.

## <a name="overview"></a>Přehled

PopupControl Extender v sadě nástrojů AJAX Control Toolkit nabízí snadný způsob, jak aktivovat automaticky otevírané okno v případě, že je aktivován jakýkoli jiný ovládací prvek. Je také možné použít více než jeden ovládací prvek místní nabídky na jedné stránce.

## <a name="steps"></a>Kroky

Aby bylo možné aktivovat funkce ASP.NET AJAX a Control Toolkit, musí být ovládací prvek `ScriptManager` umístěn kdekoli na stránce (ale v elementu `<form>`):

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample1.aspx)]

Dále přidejte panel, který slouží jako místní nabídka. V aktuálním scénáři panel obsahuje ovládací prvek `Calendar`. Aby se zabránilo aktualizaci stránky způsobené postbacky v kalendáři, je panel umístěn v ovládacím prvku `UpdatePanel`:

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample2.aspx)]

Stránka obsahuje také dvě textová pole. Pro každé textové pole se po aktivaci textového pole zobrazí místní nabídka kalendáře.

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample3.aspx)]

Teď rozšíříte každé ze dvou textových polí `PopupControlExtender`. Atribut `TargetControlID` poskytuje ID ovládacího prvku svázaného s ovládacím prvkem. Atribut `PopupControlID` obsahuje ID překryvného panelu. V takovém případě mají oba ovládací panely stejné panely, ale také je možné použít různé panely.

[!code-aspx[Main](using-multiple-popup-controls-cs/samples/sample4.aspx)]

Když teď kliknete na textové pole, zobrazí se pod polem kalendář, který vám umožní vybrat datum. (Získání vybraného data zpět do textových polí bude pokryto v jiném kurzu.)

[![kalendáři se zobrazí, když uživatel klikne do textového pole.](using-multiple-popup-controls-cs/_static/image2.png)](using-multiple-popup-controls-cs/_static/image1.png)

Kalendář se zobrazí, když uživatel klikne do textového pole ([kliknutím zobrazíte obrázek v plné velikosti).](using-multiple-popup-controls-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Next](handling-postbacks-from-a-popup-control-with-an-updatepanel-cs.md)

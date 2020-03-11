---
uid: web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
title: Používání ovládacích prvků a řídicích prvků AJAX Control ToolkitC#() | Microsoft Docs
author: microsoft
description: Naučte se, jak přidat ovládací prvky AJAX Control Toolkit a rozšířené na stránky ASP.NET.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: c1e6b51c-3bc3-4bf7-9916-9991197af3dd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/using-ajax-control-toolkit-controls-and-control-extenders-cs
msc.type: authoredcontent
ms.openlocfilehash: 1acafaadaf373b488b9e85b7ba31f08cd3b53e85
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78535411"
---
# <a name="using-ajax-control-toolkit-controls-and-control-extenders-c"></a>Použití ovládacích prvků a rozšiřujících ovládacích prvků AJAX Control Toolkit (C#)

od [Microsoftu](https://github.com/microsoft)

> Naučte se, jak přidat ovládací prvky AJAX Control Toolkit a rozšířené na stránky ASP.NET.

Sada nástrojů AJAX Control Toolkit obsahuje sadu ovládacích prvků a řídicích prvků ovládacího prvku. V tomto stručném kurzu se dozvíte, jak přidat ovládací prvky a ovládací prvky do ASP.NET stránky.

> [!NOTE] 
> 
> Pokyny k instalaci sady nástrojů AJAX Control Toolkit a přidání sady nástrojů AJAX Control Toolkit do sady Visual Studio/Visual Web Developer Toolbox naleznete v kurzu [Začínáme s ovládacím prvkem AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs.md).

## <a name="using-ajax-control-toolkit-controls"></a>Používání ovládacích prvků AJAX Control Toolkit

Ovládací prvek AJAX Control Toolkit funguje stejně jako normální ovládací prvek ASP.NET. Ovládací prvek lze přetáhnout z panelu nástrojů na stránku ASP.NET. Ovládací prvek lze přidat na stránku v zobrazení zobrazení Návrh nebo zdroj.

Při použití ovládacích prvků ze sady nástrojů AJAX Control Toolkit je k dispozici jeden zvláštní požadavek. Stránka musí obsahovat ovládací prvek ScriptManager. Ovládací prvek ScriptManager zodpovídá za zahrnutí všech nezbytných JavaScriptu požadovaných ovládacími prvky AJAX Control Toolkit.

Například karta AJAX Control Toolkit obsahuje ovládací prvek s názvem ovládací prvek editor. Tento ovládací prvek zobrazuje bohatý Editor HTML. Chcete-li přidat ovládací prvek editoru na stránku, postupujte podle těchto kroků:

1. Vytvoří novou stránku ASP.NET s názvem ShowEditor. aspx.
2. Vyberte ovládací prvek ScriptManager z karty rozšíření AJAX v sadě nástrojů a přetáhněte ovládací prvek na stránku.
3. Vyberte ovládací prvek editor z karty AJAX Control Toolkit v sadě nástrojů a přetáhněte ovládací prvek na stránku (viz obrázek 1). Návrhář by měl vypadat jako obrázek 2.
4. Spusťte web výběrem možnosti nabídky **ladit, spustit ladění** nebo stiskněte klávesu F5.
5. Stránka by se měla zobrazit na obrázku 3.

[![výběr ovládacího prvku editor HTML](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image1.png)

**Obrázek 01**: výběr ovládacího prvku HTML Editor ([kliknutím zobrazíte obrázek v plné velikosti](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.png))

[![návrháře sady Visual Studio s ovládacím prvkem ScriptManager a Edit](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image2.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.png)

**Obrázek 02**: Návrhář sady Visual Studio s ovládacím prvkem ScriptManager a Edit ([kliknutím zobrazíte obrázek v plné velikosti](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.png))

[![stránce DisplayEditor. aspx](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image3.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.png)

**Obrázek 03**: stránka DisplayEditor. aspx ([kliknutím zobrazíte obrázek v plné velikosti](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.png))

## <a name="using-ajax-control-toolkit-control-extenders"></a>Použití zařízení s rozšířenými ovládacími prvky AJAX Control Toolkit

Sada nástrojů AJAX Control Toolkit také obsahuje ovládací prvky pro rozšiřování. Jak je navrženo, rozšíření ovládacího prvku rozšiřuje funkci existujícího ovládacího prvku. Například rozšíření ovládacího prvku extenderu confirmbutton rozšiřuje standardní ovládací prvek tlačítko ASP.NET. Zařízení Extender změní chování ovládacího prvku tlačítka tak, aby po kliknutí na toto tlačítko zobrazilo potvrzovací dialog.

Rozšiřuje ovládací prvek, stejně jako ovládací prvek AJAX Control Toolkit, vyžaduje ovládací prvek ScriptManager. Než začnete používat rozšířené ovládací prvky ovládacích prvků na stránce, musíte na ni přidat ovládací prvek ScriptManager.

Pomocí tohoto postupu můžete použít extenderu confirmbutton ovládacího prvku pro rozšiřování:

1. Vytvoří novou stránku ASP.NET s názvem ShowConfirmButton. aspx.
2. Přidejte ovládací prvek ScriptManager na stránku přetažením ovládacího prvku na stránku pod kartou rozšíření AJAX.
3. Přidejte na stránku standardní ovládací prvek tlačítko přetažením tlačítka z karty Standardní na panelu nástrojů na plochu návrháře.
4. Klikněte na možnost **přidat rozšířenou** úlohu (viz obrázek 4).
5. V dialogovém okně zvolit rozšířící modul vyberte ConfirmButtonExtender (viz obrázek 5) a klikněte na tlačítko OK.
6. Vyberte ovládací prvek tlačítko v návrháři a rozbalte uzel rozšiřující objekty, Button1\_ConfirmButtonExtender v okno Vlastnosti (viz obrázek 6). Přiřaďte hodnotu *skutečně?* do vlastnosti ConfirmText.
7. Spusťte stránku výběrem možnosti nabídky **ladit, spustit ladění** nebo stiskněte klávesu F5.

[![možnost přidat rozšířenou úlohu](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image4.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.png)

**Obrázek 04**: možnost přidat rozšířenou úlohu ([kliknutím zobrazíte obrázek v plné velikosti](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image8.png))

[![výběr zařízení s rozšířeným ovládáním ovládacího prvku extenderu confirmbutton](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image5.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image9.png)

**Obrázek 05**: výběr zařízení extenderu confirmbutton Control Extender ([kliknutím zobrazíte obrázek v plné velikosti](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image10.png))

[![nastavení vlastnosti extenderu confirmbutton](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image6.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image11.png)

**Obrázek 6**: nastavení vlastnosti extenderu confirmbutton ([kliknutím zobrazíte obrázek v plné velikosti](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image12.png))

Po otevření stránky by se mělo zobrazit tlačítko. Po kliknutí na tlačítko se zobrazí potvrzovací dialogové okno na obrázku 7.

[![zobrazení potvrzovacího dialogu](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image7.jpg)](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image13.png)

**Obrázek 07**: zobrazení dialogového okna pro potvrzení ([kliknutím zobrazíte obrázek v plné velikosti](using-ajax-control-toolkit-controls-and-control-extenders-cs/_static/image14.png))

Všimněte si, že obvykle nepřetáhnete na stránku rozšířený ovládací prvek ovládacího prvku. Místo toho můžete k ovládacímu prvku, který jste již přidali na stránku, přidat do ovládacího prvku přepínač **přidat rozšířenou** úlohu. Všimněte si, že kromě toho můžete nastavit vlastnosti rozšiřujících objektů ovládacího prvku otevřením seznamu vlastností pro rozšiřující ovládací prvek.

Jeden ovládací prvek ASP.NET lze rozšířit o více rozšiřujících ovládacích prvků. Seznam vlastností pro ovládací prvek, který se rozšiřuje, vypíše všechny rozšiřující ovládací prvky přidružené k ovládacímu prvku.

> [!div class="step-by-step"]
> [Předchozí](get-started-with-the-ajax-control-toolkit-cs.md)
> [Další](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)

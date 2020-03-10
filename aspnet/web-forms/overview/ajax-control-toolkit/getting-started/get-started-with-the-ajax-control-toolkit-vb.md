---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
title: Začínáme s AJAX Control Toolkit (VB) | Microsoft Docs
author: microsoft
description: Naučte se všechno, co potřebujete vědět, abyste mohli začít používat AJAX Control Toolkit.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 9f8fa166-49a2-402c-b236-20caef0c658f
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-vb
msc.type: authoredcontent
ms.openlocfilehash: ff614308555b31710b11f408e12e9a6fadbf98d0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613482"
---
# <a name="get-started-with-the-ajax-control-toolkit-vb"></a>Začínáme se sadou nástrojů AJAX Control Toolkit (VB)

od [Microsoftu](https://github.com/microsoft)

> Naučte se všechno, co potřebujete vědět, abyste mohli začít používat AJAX Control Toolkit.

Sada nástrojů AJAX Control Toolkit obsahuje více než 30 bezplatných ovládacích prvků, které lze použít v aplikacích ASP.NET. V tomto kurzu se naučíte, jak stáhnout AJAX Control Toolkit a přidat ovládací prvky Toolkit do sady Visual Studio/Visual Web Developer Express Toolkit.

## <a name="downloading-the-ajax-control-toolkit"></a>Stažení sady nástrojů AJAX Control Toolkit

[AJAX Control Toolkit](http://devexpress.com/act) je open source projekt vyvinutý členy komunity ASP.NET a týmu ASP.NET.

[![stažení sady nástrojů AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image1.png)

**Obrázek 01**: stažení sady nástrojů Ajax Control Toolkit ([kliknutím zobrazíte obrázek v plné velikosti](get-started-with-the-ajax-control-toolkit-vb/_static/image2.png))

Po stažení souboru je nutné soubor odblokovat. Klikněte na soubor pravým tlačítkem, vyberte vlastnosti a klikněte na tlačítko **odblokování** (viz obrázek 2).

[![odblokování souboru ZIP sady nástrojů AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-vb/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image3.png)

**Obrázek 02**: odblokování souboru ZIP sady nástrojů Ajax Control Toolkit ([kliknutím zobrazíte obrázek v plné velikosti](get-started-with-the-ajax-control-toolkit-vb/_static/image4.png))

Po odblokování souboru můžete soubor rozbalit: klikněte pravým tlačítkem myši na soubor a vyberte možnost **Rozbalit vše** v nabídce. Nyní jsme připraveni přidat sadu nástrojů do sady Visual Studio nebo Visual Web Developer Toolkit.

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a>Přidání sady nástrojů AJAX Control Toolkit do sady nástrojů

Nejjednodušší způsob, jak použít sadu nástrojů AJAX Control Toolkit, je přidat sadu nástrojů do sady Visual Studio nebo Visual Web Developer Toolkit (viz obrázek 3). Tímto způsobem můžete jednoduše přetáhnout ovládací prvek Toolkit na stránku, pokud ho chcete použít.

[![sada nástrojů AJAX Control Toolkit se zobrazí v sadě nástrojů](get-started-with-the-ajax-control-toolkit-vb/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image5.png)

**Obrázek 03**: ovládací prvek AJAX Control Toolkit se zobrazuje v sadě nástrojů ([kliknutím zobrazíte obrázek v plné velikosti](get-started-with-the-ajax-control-toolkit-vb/_static/image6.png)).

Nejprve je třeba přidat kartu AJAX Control Toolkit do sady nástrojů. Postupujte následovně.

1. Vytvořte nový web ASP.NET tak, že vyberete soubor možnosti nabídky, nový web. Dvojitým kliknutím na Default. aspx v okně Průzkumník řešení otevřete soubor v editoru.
2. Klikněte pravým tlačítkem myši na panel nástrojů pod kartou obecné a vyberte možnost nabídky **Přidat kartu** (viz obrázek 4).
3. Zadejte novou kartu s názvem AJAX Control Toolkit.

[![přidávání nové karty](get-started-with-the-ajax-control-toolkit-vb/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image7.png)

**Obrázek 04**: Přidání nové karty ([kliknutím zobrazíte obrázek v plné velikosti](get-started-with-the-ajax-control-toolkit-vb/_static/image8.png))

Dále je nutné přidat ovládací prvky AJAX Control Toolkit na novou kartu. postupujte takto:

- Klikněte pravým tlačítkem myši pod kartu AJAX Control Toolkit a vyberte možnost nabídky vybrat **položky (viz obrázek 5)** .
- Přejděte do umístění, kde jste rozAjaxControlToolkiti AJAX Control Toolkit, a vyberte sestavení. dll.

[![zvolit položky, které se mají přidat do sady nástrojů](get-started-with-the-ajax-control-toolkit-vb/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-vb/_static/image9.png)

**Obrázek 05**: vyberte položky, které chcete přidat do sady nástrojů ([kliknutím zobrazíte obrázek v plné velikosti).](get-started-with-the-ajax-control-toolkit-vb/_static/image10.png)

Po dokončení tohoto postupu se všechny ovládací prvky sady Toolkit zobrazí v sadě nástrojů.

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a>Upgrade na novou verzi sady nástrojů

Pokud jste používali starší verzi sady Toolkit a teď potřebujete přejít na novější verzi, doporučujeme postupovat takto:

- Binární soubory – odstraňte starou verzi sestavení AjaxControlToolkit. dll ze složky Bin webu.
- Položky sady nástrojů – odstraňte kartu AJAX Control Toolkit a pomocí výše uvedeného postupu znovu vytvořte kartu s novou verzí sestavení AjaxControlToolkit. dll.

> [!div class="step-by-step"]
> [Předchozí](creating-a-custom-ajax-control-toolkit-control-extender-cs.md)
> [Další](using-ajax-control-toolkit-controls-and-control-extenders-vb.md)

---
uid: web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
title: Použití nástroje pro rozšiřování ovládacího prvku ColorPicker (VB) | Microsoft Docs
author: microsoft
description: ColorPicker je ASP.NET technologie AJAX, která poskytuje funkce pro vybírání barev na straně klienta s uživatelským rozhraním v místním ovládacím prvku. Dá se připojit k jakémukoli ASP.NET...
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 577ae07b-a872-4818-a804-bca489b40ad0
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/colorpicker/using-the-colorpicker-control-extender-vb
msc.type: authoredcontent
ms.openlocfilehash: 77e2e3bc61a5e1498570959ca40acff83dc3fc82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554500"
---
# <a name="using-the-colorpicker-control-extender-vb"></a>Použití nástroje pro rozšiřování ovládacího prvku ColorPicker (VB)

od [Microsoftu](https://github.com/microsoft)

> ColorPicker je ASP.NET technologie AJAX, která poskytuje funkce pro vybírání barev na straně klienta s uživatelským rozhraním v místním ovládacím prvku. Dá se připojit k jakémukoli ovládacímu prvku TextBox ASP.NET. Její.

Cílem tohoto kurzu je vysvětlit, jak můžete použít Extended Control Toolkit ovládacího prvku ColorPicker ovládacího prvku AJAX Control Toolkit. V rozbalovacím seznamu ovládacího prvku ColorPicker se zobrazí automaticky otevírané okno, které umožňuje výběr barvy. Komponenta ColorPicker je užitečná v případě, že chcete uživatelům poskytnout intuitivní uživatelské rozhraní pro výběr barvy.

## <a name="extending-a-textbox-control-with-the-colorpicker-control-extender"></a>Rozšíření ovládacího prvku TextBox pomocí rozšíření ovládacího prvku ColorPicker

Představte si například, že chcete vytvořit web, který umožňuje návštěvníkům vytvářet přizpůsobené obchodní karty. Návštěvníci můžou zadat text pro vizitku a vybrat barvu. Stránka ASP.NET v seznamu 1 obsahuje dva ovládací prvky TextBox s názvem txtCardText a txtCardColor. Při odeslání formuláře se zobrazí vybrané hodnoty (viz obrázek 1).

[![jednoduchý formulář pro vytvoření vizitky](using-the-colorpicker-control-extender-vb/_static/image1.jpg)](using-the-colorpicker-control-extender-vb/_static/image1.png)

**Obrázek 01**: jednoduchý formulář pro vytvoření vizitky ([kliknutím zobrazíte obrázek v plné velikosti](using-the-colorpicker-control-extender-vb/_static/image2.png))

**Výpis 1-CreateCard. aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample1.aspx)]

Formulář v seznamu 1 funguje, ale neposkytuje skvělou činnost koncového uživatele. Uživatel musí zadat barvu do textového pole. Pokud chce uživatel speciální barvu – například pouze pravý barevný stín Pea zeleně, musí uživatel zjistit kód barvy HTML bez jakékoli nápovědu.

Můžete použít rozšířit ovládací prvek ColorPicker pro vytvoření lepšího uživatelského prostředí. Když přesunete fokus na ovládací prvek TextBox (viz obrázek 2), zobrazí se dialogové okno s barvou.

[![zařízení pro rozšiřování ovládacího prvku ColorPicker](using-the-colorpicker-control-extender-vb/_static/image2.jpg)](using-the-colorpicker-control-extender-vb/_static/image3.png)

**Obrázek 02**: zařízení pro rozšiřování ovládacího prvku ColorPicker ([kliknutím zobrazíte obrázek v plné velikosti](using-the-colorpicker-control-extender-vb/_static/image4.png))

Je nutné provést dva kroky, pokud chcete použít rozšířený ovládací prvek ColorPicker s formulářem v seznamu 1:

1. Přidání ovládacího prvku ScriptManager na stránku
2. Přidat do stránky rozšířenou správu ovládacího prvku ColorPicker

Předtím, než budete moci použít ovladač ColorPicker, je nutné přidat do stránky ovládací prvku ScriptManager. Dobrým místem pro přidání ovládacího prvku ScriptManager je přímo pod levou &lt;ovou&gt; značku na straně serveru. Ovládací prvky ScriptManager můžete přetáhnout na stránku ze sady nástrojů (ovládací prvky ScriptManager se nachází na kartě Rozšíření AJAX). Alternativně můžete do zobrazení zdroje pod levou značkou formuláře na straně serveru zadat následující značku:

&lt;ASP: ScriptManager ID = "ScriptManager1" runat = "Server"/&gt;

Nejjednodušší způsob, jak přidat do stránky rozšířený ovládací prvek ovládacího prvku ColorPicker, je v zobrazení Návrh. Pokud najedete myší na textové pole txtCardColor, zobrazí se možnost inteligentního úkolu, která vám umožní přidat zařízení (viz obrázek 3). Pokud vyberete tuto možnost, zobrazí se Průvodce přidáním zařízení (viz obrázek 4).

[![přidání rozšíření](using-the-colorpicker-control-extender-vb/_static/image3.jpg)](using-the-colorpicker-control-extender-vb/_static/image5.png)

**Obrázek 03**: Přidání rozšíření ([kliknutím zobrazíte obrázek v plné velikosti](using-the-colorpicker-control-extender-vb/_static/image6.png))

[![výběru zařízení s rozšířeným ovládáním pomocí průvodce.](using-the-colorpicker-control-extender-vb/_static/image4.jpg)](using-the-colorpicker-control-extender-vb/_static/image7.png)

**Obrázek 04**: výběr zařízení s rozšířeným ovládáním pomocí průvodce[přepínačem (Kliknutím zobrazíte obrázek v plné velikosti](using-the-colorpicker-control-extender-vb/_static/image8.png))

Můžete vybrat zařízení s nástrojem ColorPicker, abyste rozšířili textové pole txtCardColor pomocí zařízení ColorPicker. Kliknutím na tlačítko OK zavřete dialogové okno.

Po provedení těchto změn bude zdroj stránky vypadat jako v seznamu 2.

**Výpis 2-CreateCard. aspx (s komponentou ColorPicker)**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample2.aspx)]

Všimněte si, že stránka nyní obsahuje ovládací prvek ColorPickerExtender, který se zobrazí přímo pod ovládacím prvkem txtCardColor TextBox. Ovládací prvek ColorPickerExtender rozšiřuje ovládací prvek txtCardColor tak, aby zobrazil dialog pro výběr barvy.

## <a name="using-a-button-to-launch-the-color-picker-dialog"></a>Použití tlačítka k otevření dialogového okna pro výběr barvy

Ovládací prvek ColorPicker podporuje následující vlastnosti:

- PopupButtonId – ID tlačítka na stránce, které způsobí zobrazení dialogového okna pro výběr barvy.
- PopupPosition – pozice relativní vzhledem k cílovému ovládacímu prvku dialogového okna pro výběr barvy. Možné hodnoty jsou absolutní, střední, BottomLeft, BottomRight, TopLeft, TopRight, Right a Left (výchozí hodnota je BottomLeft).
- SampleControlId – ID ovládacího prvku, který zobrazuje vybranou barvu.
- SelectedColor – počáteční barva vybraná pomocí komponenty ColorPicker.

Tyto vlastnosti můžete použít k přizpůsobení, jak se zobrazí dialogové okno pro výběr barvy a jak se zobrazuje vybraná barva. Stránka v seznamu 3 ukazuje, jak můžete použít několik těchto vlastností.

**Výpis 3-CreateCardButton. aspx**

[!code-aspx[Main](using-the-colorpicker-control-extender-vb/samples/sample3.aspx)]

Stránka v seznamu 3 obsahuje tlačítko vybrat barvu (viz obrázek 5). Po kliknutí na toto tlačítko se zobrazí dialogové okno pro výběr barvy nad textovým polem. Pokud vyberete barvu z dialogového okna, vybraná barva se zobrazí jako barva pozadí ovládacího prvku popisek lblSample.

Vlastnost ColorPicker PopupButtonID se používá k přidružení tlačítka výběr barvy k zařízení ColorPicker. Když zadáte hodnotu vlastnosti PopupButtonID, dialogové okno pro výběr barvy se již nezobrazuje, když cílový ovládací prvek má fokus. Chcete-li zobrazit dialogové okno, je nutné kliknout na tlačítko.

Vlastnost SampleControlID se používá k přidružení ovládacího prvku, který zobrazuje vybranou barvu pomocí ovládacího prvku ColorPicker. Komponenta ColorPicker změní barvu pozadí tohoto ovládacího prvku na aktuálně vybranou barvu.

[![zobrazení dialogového okna pro výběr barvy tlačítkem](using-the-colorpicker-control-extender-vb/_static/image5.jpg)](using-the-colorpicker-control-extender-vb/_static/image9.png)

**Obrázek 05**: zobrazení dialogového okna pro výběr barvy s tlačítkem ([kliknutím zobrazíte obrázek v plné velikosti](using-the-colorpicker-control-extender-vb/_static/image10.png))

## <a name="summary"></a>Souhrn

V tomto kurzu jste zjistili, jak použít rozšíření ovládacího prvku ColorPicker k zobrazení dialogového okna pro výběr barvy v místním okně. Nejdříve jsme zkoumali, jak můžete zobrazit dialog při přesunutí fokusu na ovládací prvek TextBox. Dále jste zjistili, jak vytvořit tlačítko, které po kliknutí na tlačítko zobrazí dialogové okno pro výběr barvy.

> [!div class="step-by-step"]
> [Předchozí](using-the-colorpicker-control-extender-cs.md)

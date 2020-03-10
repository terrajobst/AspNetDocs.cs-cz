---
uid: web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
title: Návody použít ovládací prvek editor HTML? (C#) | Microsoft Docs
author: microsoft
description: HTMLEditor je ovládací prvek ASP.NET AJAX, který umožňuje snadno vytvářet a upravovat obsah HTML prostřednictvím tlačítek na panelu nástrojů.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: f47e6224-c2e5-4472-b069-b6c7b6115200
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/htmleditor/how-do-i-use-the-html-editor-control-cs
msc.type: authoredcontent
ms.openlocfilehash: cb7d75b59b1361abeb6d3c38ad6e42e34d6e3f7b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78577859"
---
# <a name="how-do-i-use-the-html-editor-control-c"></a>Návody použít ovládací prvek editor HTML? (C#)

od [Microsoftu](https://github.com/microsoft)

> HTMLEditor je ovládací prvek ASP.NET AJAX, který umožňuje snadno vytvářet a upravovat obsah HTML prostřednictvím tlačítek na panelu nástrojů.

Cílem tohoto kurzu je poskytnout vám přehled ovládacího prvku editor HTML, který je součástí sady nástrojů AJAX Control Toolkit. Editor HTML obsahuje možnosti pro změnu velikosti písma, výběr písma, změnu barvy pozadí, úpravu barvy popředí, přidávání odkazů, přidávání obrázků, změnu zarovnání textu a provádění operací vyjmutí, kopírování a vložení (viz obrázek 1).

[![editoru HTML](how-do-i-use-the-html-editor-control-cs/_static/image1.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image1.png)

**Obrázek 01**: Editor HTML ([kliknutím zobrazíte obrázek v plné velikosti](how-do-i-use-the-html-editor-control-cs/_static/image2.png))

Editor HTML umožňuje zadat obsah pomocí režimu návrhu nebo můžete přímo zadat kód HTML. K dispozici je také možnost zobrazit náhled obsahu ve formátu HTML (viz obrázek 2).

[tlačítka pro ![design, HTML a Preview](how-do-i-use-the-html-editor-control-cs/_static/image2.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image3.png)

**Obrázek 02**: tlačítka design, HTML a Preview ([kliknutím zobrazíte obrázek v plné velikosti](how-do-i-use-the-html-editor-control-cs/_static/image4.png))

V tomto kurzu se naučíte, jak zobrazit editor HTML, jak přizpůsobit tlačítka panelu nástrojů, která se zobrazují v editoru HTML, a jak se vyhnout útokům prostřednictvím skriptování mezi weby.

## <a name="displaying-the-html-editor"></a>Zobrazení editoru HTML

Než budete moct použít Editor HTML na stránce ASP.NET, musíte nejdřív na stránku přidat ovládací prvek ScriptManager. Ovládací prvek ScriptManager se nachází pod kartou rozšíření AJAX v sadě nástrojů Visual Studio/Visual Web Developer Express.

Ovládací prvek ScriptManager byste měli umístit v horní části stránky před jakékoli jiné ovládací prvky na stránce. Můžete ji například umístit hned pod úvodní &lt;formuláře na straně serveru&gt; značku.

Ovládací prvek editor HTML je umístěn v sadě nástrojů s ostatními ovládacími prvky AJAX Control Toolkit. Nazývá se ovládací prvek Editor (viz obrázek 3).

[![ovládacího prvku editor HTML](how-do-i-use-the-html-editor-control-cs/_static/image3.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image5.png)

**Obrázek 03**: ovládací prvek editor HTML ([kliknutím zobrazíte obrázek v plné velikosti](how-do-i-use-the-html-editor-control-cs/_static/image6.png))

Po přetažení editoru HTML na stránku můžete nastavit jeho vlastnosti v seznamu vlastností. Například obvykle chcete nastavit vlastnosti Width a Height. Výpis 1 obsahuje zdroj pro stránku ASP.NET, která obsahuje editor HTML.

**Výpis 1-SimpleEditor. aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample1.aspx)]

Stránka v seznamu 1 obsahuje ovládací prvek editoru HTML, ovládací prvek tlačítko a ovládací prvek literálu. Po kliknutí na tlačítko se zobrazí obsah editoru HTML v ovládacím prvku literál (viz obrázek 4).

[![odesílání formuláře pomocí editoru HTML](how-do-i-use-the-html-editor-control-cs/_static/image4.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image7.png)

**Obrázek 04**: odeslání formuláře pomocí editoru HTML ([kliknutím zobrazíte obrázek v plné velikosti](how-do-i-use-the-html-editor-control-cs/_static/image8.png))

Vlastnost obsahu editoru HTML slouží k načtení obsahu HTML zadaného do editoru HTML. Uvědomte si, že tento obsah HTML může obsahovat JavaScript. V další části se podíváme, jak můžete zabránit útokům prostřednictvím injektáže JavaScriptu.

## <a name="customizing-the-html-editor-toolbar"></a>Přizpůsobení panelu nástrojů editoru HTML

Můžete přizpůsobit přesně to, která tlačítka se zobrazí v editoru. Například můžete chtít odebrat kartu HTML a zabránit tak uživatelům v přepínání editoru HTML do režimu HTML. Nebo můžete chtít odebrat rozevírací seznam velikost písma, abyste uživatelům zabránili v vytváření velkého textu v příspěvku zprávy fóra (viz obrázek 5).

[![přizpůsobený Editor HTML](how-do-i-use-the-html-editor-control-cs/_static/image5.jpg)](how-do-i-use-the-html-editor-control-cs/_static/image9.png)

**Obrázek 05**: přizpůsobený Editor HTML ([kliknutím zobrazíte obrázek v plné velikosti](how-do-i-use-the-html-editor-control-cs/_static/image10.png))

Tlačítka panelu nástrojů lze přizpůsobit odvozením nového editoru HTML ze základní třídy editoru. Například vlastní editor v seznamu 2 obsahuje tlačítka panelu nástrojů pro tučné písmo a kurzívu. Všechna ostatní tlačítka panelu nástrojů byla odebrána. Kromě toho se v dolní části editoru odebrala karta HTML (na kartách návrh a náhled stále existují).

**Výpis 2-aplikace\_Code\CustomEditor.cs**

[!code-csharp[Main](how-do-i-use-the-html-editor-control-cs/samples/sample2.cs)]

Je nutné přidat třídu v seznamu 2 do vaší aplikace\_kódové složky tak, aby se třída automaticky kompilována. Pokud ve vašem webu neexistuje složka\_kódu aplikace, můžete jednoduše přidat složku.

Po vytvoření vlastního editoru ho můžete přidat na stránku ASP.NET stejným způsobem jako při přidávání normálního editoru HTML (viz výpis 3).

**Výpis 3-ShowCustomEditor. aspx**

[!code-aspx[Main](how-do-i-use-the-html-editor-control-cs/samples/sample3.aspx)]

## <a name="avoiding-cross-site-scripting-xss-attacks"></a>Zamezení útokům prostřednictvím skriptování mezi weby (XSS)

Pokaždé, když přijmete vstup od uživatele a znovu zobrazíte tento vstup na webu, můžete web otevřít pro útoky skriptování XSS (mezi lokalitami). Teoreticky může útočník odeslat kód JavaScriptu, který se spustí při opětovném zobrazení vstupu. Jazyk JavaScript lze použít ke krádeži uživatelských hesel nebo jiných citlivých informací.

V normálním případě můžete útoky XSS přezkoušet pomocí kódování HTML bez ohledu na to, který vstup načtete od uživatele před jeho zobrazením na webové stránce. Nicméně kódování HTML ve výstupu editoru HTML by nemuselo kódovat pouze &lt;značek&gt; skriptu, ale také zakóduje všechny značky HTML. Jinými slovy, byste ztratili formátování, jako je typ písma, velikost písma a barva pozadí.

Pokud shromažďujete citlivé informace od uživatelů, například hesla, čísla kreditních karet a čísla sociálního pojištění, neměli byste zobrazovat nekódovaný obsah, který načtete od uživatele pomocí editoru HTML. Editor HTML byste měli použít jenom v situacích, kdy nezobrazujete obsah HTML, nebo když je obsah HTML odesílána důvěryhodnou stranou vaší webovému serveru.

Představte si například, že vytváříte aplikaci blogu. V takové situaci má smysl při vytváření příspěvků na blogu použít Editor HTML. Jste jediným z nich, kdo pošle Blogový příspěvek, a PŘEDPOKLÁDANĚ můžete důvěřovat, že nebudete moct odesílat škodlivý JavaScript. Nemá ale smysl používat editor HTML, pokud umožňuje anonymním uživatelům publikovat komentáře. Měli byste být obzvláště opatrní v situacích, kdy uživatelé odesílají citlivé informace, jako jsou hesla. Uživatel se zlými úmysly by potenciálně mohl publikovat komentář, který obsahuje správný JavaScript pro krádeži hesla.

## <a name="summary"></a>Souhrn

V tomto kurzu jste získali stručný přehled ovládacího prvku HTML editor, který je součástí sady AJAX Control Toolkit. Zjistili jste, jak použít Editor HTML k přijetí formátovaného obsahu od uživatele a odeslání obsahu na server. Také jsme zjistili, jak lze přizpůsobit tlačítka panelu nástrojů, která jsou zobrazena editorem HTML. Nakonec jste zjistili, jak se vyhnout útokům prostřednictvím skriptování mezi weby při použití editoru HTML k přijetí potenciálně škodlivého vstupu.

> [!div class="step-by-step"]
> [Next](how-do-i-use-the-html-editor-control-vb.md)

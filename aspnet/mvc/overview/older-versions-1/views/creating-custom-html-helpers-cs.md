---
uid: aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
title: Vytváření vlastních pomocníků HTML (C#) | Microsoft Docs
author: microsoft
description: Cílem tohoto kurzu je Ukázat, jak můžete vytvořit vlastní pomocníky HTML, které můžete použít v zobrazeních MVC. Využívejte si pomocníka HTML...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: e454c67d-a86e-4119-a858-eb04bbec2dff
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: 264ff9850bad397826b45649d52fbfefafc53a01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600238"
---
# <a name="creating-custom-html-helpers-c"></a>Vytvoření vlastních pomocných rutin HTML (C#)

od [Microsoftu](https://github.com/microsoft)

[Stáhnout PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_CS.pdf)

> Cílem tohoto kurzu je Ukázat, jak můžete vytvořit vlastní pomocníky HTML, které můžete použít v zobrazeních MVC. Díky výhodám pomocníků HTML můžete omezit množství zdlouhavého psaní značek HTML, které je nutné provést, aby bylo možné vytvořit standardní stránku HTML.

Cílem tohoto kurzu je Ukázat, jak můžete vytvořit vlastní pomocníky HTML, které můžete použít v zobrazeních MVC. Díky výhodám pomocníků HTML můžete omezit množství zdlouhavého psaní značek HTML, které je nutné provést, aby bylo možné vytvořit standardní stránku HTML.

V první části tohoto kurzu popíšeme některé z existujících pomocníků HTML, které jsou součástí architektury ASP.NET MVC. Dále popíšeme dvě metody vytváření vlastních pomocných pomocníků HTML: Vysvětlete, jak vytvořit vlastní pomocné pomocníky HTML vytvořením statické metody a vytvořením metody rozšíření.

## <a name="understanding-html-helpers"></a>Principy pomocníků HTML

Pomocný objekt HTML je pouze metoda, která vrací řetězec. Řetězec může představovat libovolný typ obsahu, který chcete. Například můžete použít pomocníky HTML k vykreslení standardních značek HTML jako `<input>` HTML a značek `<img>`. Můžete také použít pomocníky HTML k vykreslování složitějšího obsahu, jako je například pruh karet nebo tabulka HTML dat databáze.

Rozhraní ASP.NET MVC obsahuje následující sadu standardních pomocníků HTML (nejedná se o úplný seznam):

- Html.ActionLink()
- Html.BeginForm()
- Html.CheckBox()
- Html.DropDownList()
- Html.EndForm()
- Html.Hidden()
- Html.ListBox()
- Html.Password()
- Html.RadioButton()
- Html.TextArea()
- Html.TextBox()

Zvažte například formulář v seznamu 1. Tento formulář se vykreslí pomocí dvou standardních pomocníků HTML (viz obrázek 1). Tento formulář používá pomocné metody `Html.BeginForm()` a `Html.TextBox()` k vykreslování jednoduchého HTML formuláře.

[Stránka ![vykreslená pomocí pomocníků HTML](creating-custom-html-helpers-cs/_static/image2.png)](creating-custom-html-helpers-cs/_static/image1.png)

**Obrázek 01**: stránka vykreslená pomocí pomocníků HTML ([kliknutím zobrazíte obrázek v plné velikosti](creating-custom-html-helpers-cs/_static/image3.png))

**Výpis 1 – `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample1.aspx)]

Pomocná metoda HTML. BeginForm () se používá k vytvoření počátečních a ukončovacích značek HTML `<form>`. Všimněte si, že metoda `Html.BeginForm()` je volána v rámci příkazu Using. Příkaz using zajišťuje, aby se značka `<form>` na konci bloku using zavřela.

Pokud dáváte přednost místo vytvoření bloku using, můžete zavolat pomocnou metodu HTML. EndForm () pro zavření značky `<form>`. Použijte libovolný přístup k vytvoření úvodní a uzavírací značky `<form>`, která se pro vás jeví jako nejužitečnější.

Pomocné metody `Html.TextBox()` se používají v seznamu 1 k vykreslování značek HTML `<input>`. Pokud v prohlížeči vyberete možnost zdroj zobrazení, zobrazí se v seznamu 2 zdroj HTML. Všimněte si, že zdroj obsahuje standardní značky HTML.

> [!IMPORTANT]
> Všimněte si, že pomocný objekt `Html.TextBox()`-HTML je vykreslen pomocí značek `<%= %>` namísto značek `<% %>`. Pokud nezadáte symbol rovná se, nic se nenačte do prohlížeče.

Rozhraní ASP.NET MVC obsahuje malou sadu pomocníků. Nejpravděpodobnější je, že budete muset architekturu MVC zvětšit s vlastními pomocníky HTML. Ve zbývající části tohoto kurzu se naučíte dvě metody vytváření vlastních pomocníků HTML.

**Výpis 2 – `Index.aspx Source`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-static-methods"></a>Vytváření pomocníků HTML pomocí statických metod

Nejjednodušší způsob, jak vytvořit nový pomocníka v jazyce HTML, je vytvořit statickou metodu, která vrátí řetězec. Představte si například, že se rozhodnete vytvořit nového pomocníka HTML, který vykresluje značku HTML `<label>`. Pomocí třídy v seznamu 2 můžete vykreslit `<label>`.

**Výpis 2 – `Helpers\LabelHelper.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample3.cs)]

V seznamu 2 neexistují žádné zvláštní informace o třídě. Metoda `Label()` jednoduše vrátí řetězec.

Změněné zobrazení indexu v seznamu 3 používá `LabelHelper` k vykreslení značek `<label>` HTML. Všimněte si, že zobrazení obsahuje direktivu `<%@ imports %>`, která importuje obor názvů `Application1.Helpers`.

**Výpis 2 – `Views\Home\Index2.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a>Vytváření pomocných pomocných metod HTML s metodami rozšíření

Chcete-li vytvořit pomocníky HTML, které fungují stejným způsobem jako standardní pomocníky HTML zahrnuté v rozhraní ASP.NET MVC Framework, je nutné vytvořit rozšiřující metody. Metody rozšíření umožňují přidat nové metody do existující třídy. Při vytváření pomocné metody HTML přidáte nové metody do třídy HtmlHelper reprezentované vlastností HTML zobrazení.

Třída v seznamu 3 přidá metodu rozšíření do `HtmlHelper` třídy s názvem `Label()`. Existuje několik věcí, které byste si měli všimnout o této třídě. Nejprve si všimněte, že třída je statická třída. Je nutné definovat metodu rozšíření se statickou třídou.

Za druhé si všimněte, že první parametr metody `Label()` předchází klíčovým slovem `this`. První parametr metody rozšíření označuje třídu, kterou rozšiřující metoda rozšiřuje.

**Výpis 3 – `Helpers\LabelExtensions.cs`**

[!code-csharp[Main](creating-custom-html-helpers-cs/samples/sample5.cs)]

Po vytvoření metody rozšíření a sestavení aplikace úspěšně sestavíte metodu rozšíření v aplikaci Visual Studio IntelliSense jako všechny ostatní metody třídy (viz obrázek 2). Jediným rozdílem je, že metody rozšíření se zobrazí se speciálním symbolem vedle sebe (ikona šipky dolů).

[![pomocí rozšiřující metody HTML. Label ()](creating-custom-html-helpers-cs/_static/image5.png)](creating-custom-html-helpers-cs/_static/image4.png)

**Obrázek 02**: použití rozšiřující metody HTML. Label () ([kliknutím zobrazíte obrázek v plné velikosti](creating-custom-html-helpers-cs/_static/image6.png))

Změněné zobrazení indexu v seznamu 4 používá metodu rozšíření HTML. Label () k vykreslení všech značek `<label>`.

**Výpis 4 – `Views\Home\Index3.aspx`**

[!code-aspx[Main](creating-custom-html-helpers-cs/samples/sample6.aspx)]

## <a name="summary"></a>Souhrn

V tomto kurzu jste se naučili dvě metody vytváření vlastních pomocníků HTML. Nejdříve jste zjistili, jak vytvořit vlastní nápovědu `Label()` HTML vytvořením statické metody, která vrací řetězec. Dále jste zjistili, jak vytvořit vlastní pomocnou metodu `Label()` HTML vytvořením metody rozšíření na `HtmlHelper` třídě.

V tomto kurzu se zaměřujeme na sestavování velmi jednoduchých pomocných metod HTML. Mějte na paměti, že pomocný objekt HTML může být tak složitý, jak chcete. Můžete vytvořit pomocníky HTML, které vykreslují bohatý obsah, jako jsou zobrazení stromové struktury, nabídky nebo tabulky dat databáze.

> [!div class="step-by-step"]
> [Předchozí](asp-net-mvc-views-overview-cs.md)
> [Další](using-the-tagbuilder-class-to-build-html-helpers-cs.md)

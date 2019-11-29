---
uid: mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
title: Vytváření vlastních pomocníků HTML (VB) | Microsoft Docs
author: microsoft
description: Cílem tohoto kurzu je Ukázat, jak můžete vytvořit vlastní pomocníky HTML, které můžete použít v zobrazeních MVC. Využívejte si pomocníka HTML...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: f96f4800-19ef-44c0-b457-55e777eb5de8
msc.legacyurl: /mvc/overview/older-versions-1/views/creating-custom-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: aaeadde258a2855343a5bfb1e5ee76000e04f6bd
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74593827"
---
# <a name="creating-custom-html-helpers-vb"></a><span data-ttu-id="8ee9d-104">Vytvoření vlastních pomocných rutin HTML (VB)</span><span class="sxs-lookup"><span data-stu-id="8ee9d-104">Creating Custom HTML Helpers (VB)</span></span>

<span data-ttu-id="8ee9d-105">od [Microsoftu](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="8ee9d-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="8ee9d-106">Stáhnout PDF</span><span class="sxs-lookup"><span data-stu-id="8ee9d-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_9_VB.pdf)

> <span data-ttu-id="8ee9d-107">Cílem tohoto kurzu je Ukázat, jak můžete vytvořit vlastní pomocníky HTML, které můžete použít v zobrazeních MVC.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-107">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="8ee9d-108">Díky výhodám pomocníků HTML můžete omezit množství zdlouhavého psaní značek HTML, které je nutné provést, aby bylo možné vytvořit standardní stránku HTML.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-108">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="8ee9d-109">Cílem tohoto kurzu je Ukázat, jak můžete vytvořit vlastní pomocníky HTML, které můžete použít v zobrazeních MVC.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-109">The goal of this tutorial is to demonstrate how you can create custom HTML Helpers that you can use within your MVC views.</span></span> <span data-ttu-id="8ee9d-110">Díky výhodám pomocníků HTML můžete omezit množství zdlouhavého psaní značek HTML, které je nutné provést, aby bylo možné vytvořit standardní stránku HTML.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-110">By taking advantage of HTML Helpers, you can reduce the amount of tedious typing of HTML tags that you must perform to create a standard HTML page.</span></span>

<span data-ttu-id="8ee9d-111">V první části tohoto kurzu popíšeme některé z existujících pomocníků HTML, které jsou součástí architektury ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-111">In the first part of this tutorial, I describe some of the existing HTML Helpers included with the ASP.NET MVC framework.</span></span> <span data-ttu-id="8ee9d-112">Dále popíšeme dvě metody vytváření vlastních pomocných pomocníků HTML: Vysvětlete, jak vytvořit vlastní pomocné pomocníky HTML vytvořením sdílené metody a vytvořením metody rozšíření.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-112">Next, I describe two methods of creating custom HTML Helpers: I explain how to create custom HTML Helpers by creating a shared method and by creating an extension method.</span></span>

## <a name="understanding-html-helpers"></a><span data-ttu-id="8ee9d-113">Principy pomocníků HTML</span><span class="sxs-lookup"><span data-stu-id="8ee9d-113">Understanding HTML Helpers</span></span>

<span data-ttu-id="8ee9d-114">Pomocný objekt HTML je pouze metoda, která vrací řetězec.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-114">An HTML Helper is just a method that returns a string.</span></span> <span data-ttu-id="8ee9d-115">Řetězec může představovat libovolný typ obsahu, který chcete.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-115">The string can represent any type of content that you want.</span></span> <span data-ttu-id="8ee9d-116">Například můžete použít pomocníky HTML k vykreslení standardních značek HTML jako `<input>` HTML a značek `<img>`.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-116">For example, you can use HTML Helpers to render standard HTML tags like HTML `<input>` and `<img>` tags.</span></span> <span data-ttu-id="8ee9d-117">Můžete také použít pomocníky HTML k vykreslování složitějšího obsahu, jako je například pruh karet nebo tabulka HTML dat databáze.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-117">You also can use HTML Helpers to render more complex content such as a tab strip or an HTML table of database data.</span></span>

<span data-ttu-id="8ee9d-118">Rozhraní ASP.NET MVC obsahuje následující sadu standardních pomocníků HTML (nejedná se o úplný seznam):</span><span class="sxs-lookup"><span data-stu-id="8ee9d-118">The ASP.NET MVC framework includes the following set of standard HTML Helpers (this is not a complete list):</span></span>

- <span data-ttu-id="8ee9d-119">HTML. ActionLink ()</span><span class="sxs-lookup"><span data-stu-id="8ee9d-119">Html.ActionLink()</span></span>
- <span data-ttu-id="8ee9d-120">HTML. BeginForm ()</span><span class="sxs-lookup"><span data-stu-id="8ee9d-120">Html.BeginForm()</span></span>
- <span data-ttu-id="8ee9d-121">HTML. CheckBox ()</span><span class="sxs-lookup"><span data-stu-id="8ee9d-121">Html.CheckBox()</span></span>
- <span data-ttu-id="8ee9d-122">HTML. DropDownList ()</span><span class="sxs-lookup"><span data-stu-id="8ee9d-122">Html.DropDownList()</span></span>
- <span data-ttu-id="8ee9d-123">HTML. EndForm ()</span><span class="sxs-lookup"><span data-stu-id="8ee9d-123">Html.EndForm()</span></span>
- <span data-ttu-id="8ee9d-124">HTML. Hidden ()</span><span class="sxs-lookup"><span data-stu-id="8ee9d-124">Html.Hidden()</span></span>
- <span data-ttu-id="8ee9d-125">HTML. ListBox ()</span><span class="sxs-lookup"><span data-stu-id="8ee9d-125">Html.ListBox()</span></span>
- <span data-ttu-id="8ee9d-126">HTML. Password ()</span><span class="sxs-lookup"><span data-stu-id="8ee9d-126">Html.Password()</span></span>
- <span data-ttu-id="8ee9d-127">HTML. RadioButton ()</span><span class="sxs-lookup"><span data-stu-id="8ee9d-127">Html.RadioButton()</span></span>
- <span data-ttu-id="8ee9d-128">HTML. TextArea ()</span><span class="sxs-lookup"><span data-stu-id="8ee9d-128">Html.TextArea()</span></span>
- <span data-ttu-id="8ee9d-129">HTML. TextBox ()</span><span class="sxs-lookup"><span data-stu-id="8ee9d-129">Html.TextBox()</span></span>

<span data-ttu-id="8ee9d-130">Zvažte například formulář v seznamu 1.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-130">For example, consider the form in Listing 1.</span></span> <span data-ttu-id="8ee9d-131">Tento formulář se vykreslí pomocí dvou standardních pomocníků HTML (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="8ee9d-131">This form is rendered with the help of two of the standard HTML Helpers (see Figure 1).</span></span> <span data-ttu-id="8ee9d-132">Tento formulář používá pomocné metody `Html.BeginForm()` a `Html.TextBox()`.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-132">This form uses the `Html.BeginForm()` and `Html.TextBox()` Helper methods.</span></span>

<span data-ttu-id="8ee9d-133">[Stránka ![vykreslená pomocí pomocníků HTML](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8ee9d-133">[![Page rendered with HTML Helpers](creating-custom-html-helpers-vb/_static/image2.png)](creating-custom-html-helpers-vb/_static/image1.png)</span></span>

<span data-ttu-id="8ee9d-134">**Obrázek 01**: stránka vykreslená pomocí pomocníků HTML ([kliknutím zobrazíte obrázek v plné velikosti](creating-custom-html-helpers-vb/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="8ee9d-134">**Figure 01**: Page rendered with HTML Helpers ([Click to view full-size image](creating-custom-html-helpers-vb/_static/image3.png))</span></span>

<span data-ttu-id="8ee9d-135">**Výpis 1 – `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="8ee9d-135">**Listing 1 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample1.aspx)]

<span data-ttu-id="8ee9d-136">Pomocná metoda `Html.BeginForm()` slouží k vytvoření počátečních a ukončovacích značek `<form>` HTML.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-136">The `Html.BeginForm()` Helper method is used to create the opening and closing HTML `<form>` tags.</span></span> <span data-ttu-id="8ee9d-137">Všimněte si, že metoda `Html.BeginForm()` je volána v rámci příkazu Using.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-137">Notice that the `Html.BeginForm()` method is called within a using statement.</span></span> <span data-ttu-id="8ee9d-138">Příkaz using zajišťuje, aby se značka `<form>` na konci bloku using zavřela.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-138">The using statement ensures that the `<form>` tag gets closed at the end of the using block.</span></span>

<span data-ttu-id="8ee9d-139">Pokud dáváte přednost místo vytvoření bloku using, můžete zavolat pomocnou metodu HTML. EndForm () pro zavření značky `<form>`.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-139">If you prefer, instead of creating a using block, you can call the Html.EndForm() Helper method to close the `<form>` tag.</span></span> <span data-ttu-id="8ee9d-140">Použijte libovolný přístup k vytvoření úvodní a uzavírací značky `<form>`, která se pro vás jeví jako nejužitečnější.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-140">Use whichever approach to creating an opening and closing `<form>` tag that seems most intuitive to you.</span></span>

<span data-ttu-id="8ee9d-141">Pomocné metody `Html.TextBox()` se používají v seznamu 1 k vykreslování značek HTML `<input>`.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-141">The `Html.TextBox()` Helper methods are used in Listing 1 to render HTML `<input>` tags.</span></span> <span data-ttu-id="8ee9d-142">Pokud v prohlížeči vyberete možnost zdroj zobrazení, zobrazí se v seznamu 2 zdroj HTML.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-142">If you select view source in your browser then you see the HTML source in Listing 2.</span></span> <span data-ttu-id="8ee9d-143">Všimněte si, že zdroj obsahuje standardní značky HTML.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-143">Notice that the source contains standard HTML tags.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8ee9d-144">Všimněte si, že pomocný objekt `Html.TextBox()`-HTML je vykreslen pomocí značek `<%= %>` namísto značek `<% %>`.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-144">notice that the `Html.TextBox()`-HTML Helper is rendered with `<%= %>` tags instead of `<% %>` tags.</span></span> <span data-ttu-id="8ee9d-145">Pokud nezadáte symbol rovná se, nic se nenačte do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-145">If you don't include the equal sign, then nothing gets rendered to the browser.</span></span>

<span data-ttu-id="8ee9d-146">Rozhraní ASP.NET MVC obsahuje malou sadu pomocníků.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-146">The ASP.NET MVC framework contains a small set of helpers.</span></span> <span data-ttu-id="8ee9d-147">Nejpravděpodobnější je, že budete muset architekturu MVC zvětšit s vlastními pomocníky HTML.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-147">Most likely, you will need to extend the MVC framework with custom HTML Helpers.</span></span> <span data-ttu-id="8ee9d-148">Ve zbývající části tohoto kurzu se naučíte dvě metody vytváření vlastních pomocníků HTML.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-148">In the remainder of this tutorial, you learn two methods of creating custom HTML Helpers.</span></span>

<span data-ttu-id="8ee9d-149">**Výpis 2 – `Index.aspx Source`**</span><span class="sxs-lookup"><span data-stu-id="8ee9d-149">**Listing 2 – `Index.aspx Source`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample2.aspx)]

### <a name="creating-html-helpers-with-shared-methods"></a><span data-ttu-id="8ee9d-150">Vytváření pomocníků HTML se sdílenými metodami</span><span class="sxs-lookup"><span data-stu-id="8ee9d-150">Creating HTML Helpers with Shared Methods</span></span>

<span data-ttu-id="8ee9d-151">Nejjednodušší způsob, jak vytvořit nový pomocníka v jazyce HTML, je vytvořit sdílenou metodu, která vrací řetězec.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-151">The easiest way to create a new HTML Helper is to create a shared method that returns a string.</span></span> <span data-ttu-id="8ee9d-152">Představte si například, že se rozhodnete vytvořit nového pomocníka HTML, který vykresluje značku HTML `<label>`.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-152">Imagine, for example, that you decide to create a new HTML Helper that renders an HTML `<label>` tag.</span></span> <span data-ttu-id="8ee9d-153">Pomocí třídy v seznamu 2 můžete vykreslit `<label>`.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-153">You can use the class in Listing 2 to render a `<label>`.</span></span>

<span data-ttu-id="8ee9d-154">**Výpis 2 – `Helpers\LabelHelper.vb`**</span><span class="sxs-lookup"><span data-stu-id="8ee9d-154">**Listing 2 – `Helpers\LabelHelper.vb`**</span></span>

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample3.vb)]

<span data-ttu-id="8ee9d-155">V seznamu 2 neexistují žádné zvláštní informace o třídě.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-155">There is nothing special about the class in Listing 2.</span></span> <span data-ttu-id="8ee9d-156">Metoda `Label()` jednoduše vrátí řetězec.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-156">The `Label()` method simply returns a string.</span></span>

<span data-ttu-id="8ee9d-157">Změněné zobrazení indexu v seznamu 3 používá `LabelHelper` k vykreslení značek `<label>` HTML.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-157">The modified Index view in Listing 3 uses the `LabelHelper` to render HTML `<label>` tags.</span></span> <span data-ttu-id="8ee9d-158">Všimněte si, že zobrazení obsahuje direktivu `<%@ imports %>`, která importuje obor názvů Application1. helps.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-158">Notice that the view includes an `<%@ imports %>` directive that imports the Application1.Helpers namespace.</span></span>

<span data-ttu-id="8ee9d-159">**Výpis 2 – `Views\Home\Index2.aspx`**</span><span class="sxs-lookup"><span data-stu-id="8ee9d-159">**Listing 2 – `Views\Home\Index2.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample4.aspx)]

### <a name="creating-html-helpers-with-extension-methods"></a><span data-ttu-id="8ee9d-160">Vytváření pomocných pomocných metod HTML s metodami rozšíření</span><span class="sxs-lookup"><span data-stu-id="8ee9d-160">Creating HTML Helpers with Extension Methods</span></span>

<span data-ttu-id="8ee9d-161">Chcete-li vytvořit pomocníky HTML, které fungují stejným způsobem jako standardní pomocníky HTML zahrnuté v rozhraní ASP.NET MVC Framework, je nutné vytvořit rozšiřující metody.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-161">If you want to create HTML Helpers that work just like the standard HTML Helpers included in the ASP.NET MVC framework then you need to create extension methods.</span></span> <span data-ttu-id="8ee9d-162">Metody rozšíření umožňují přidat nové metody do existující třídy.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-162">Extension methods enable you to add new methods to an existing class.</span></span> <span data-ttu-id="8ee9d-163">Při vytváření pomocné metody HTML přidáte nové metody do třídy `HtmlHelper` reprezentované vlastností HTML zobrazení.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-163">When creating an HTML Helper method, you add new methods to the `HtmlHelper` class represented by a view's Html property.</span></span>

<span data-ttu-id="8ee9d-164">Modul Visual Basic v seznamu 3 přidá metodu rozšíření s názvem `Label()` do třídy `HtmlHelper`.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-164">The Visual Basic module in Listing 3 adds an extension method named `Label()` to the `HtmlHelper` class.</span></span> <span data-ttu-id="8ee9d-165">Existuje několik věcí, které byste si měli všimnout o tomto modulu.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-165">There are a couple of things that you should notice about this module.</span></span> <span data-ttu-id="8ee9d-166">Nejprve si všimněte, že modul je upraven pomocí atributu `<Extension()>`.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-166">First, notice that the module is decorated with the `<Extension()>` attribute.</span></span> <span data-ttu-id="8ee9d-167">Aby bylo možné použít tento atribut, je nutné importovat `System.Runtime.CompilerServices` obor názvů.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-167">In order to use this attribute, you must import the `System.Runtime.CompilerServices` namespace</span></span>

<span data-ttu-id="8ee9d-168">Za druhé si všimněte, že první parametr metody `Label()` představuje třídu `HtmlHelper`.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-168">Second, notice that the first parameter of the `Label()` method represents the `HtmlHelper` class.</span></span> <span data-ttu-id="8ee9d-169">První parametr metody rozšíření označuje třídu, kterou rozšiřující metoda rozšiřuje.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-169">The first parameter of an extension method indicates the class that the extension method extends.</span></span>

<span data-ttu-id="8ee9d-170">**Výpis 3 – `Helpers\LabelExtensions.vb`**</span><span class="sxs-lookup"><span data-stu-id="8ee9d-170">**Listing 3 – `Helpers\LabelExtensions.vb`**</span></span>

[!code-vb[Main](creating-custom-html-helpers-vb/samples/sample5.vb)]

<span data-ttu-id="8ee9d-171">Po vytvoření metody rozšíření a sestavení aplikace úspěšně sestavíte metodu rozšíření v aplikaci Visual Studio IntelliSense jako všechny ostatní metody třídy (viz obrázek 2).</span><span class="sxs-lookup"><span data-stu-id="8ee9d-171">After you create an extension method, and build your application successfully, the extension method appears in Visual Studio Intellisense like all of the other methods of a class (see Figure 2).</span></span> <span data-ttu-id="8ee9d-172">Jediným rozdílem je, že metody rozšíření se zobrazí se speciálním symbolem vedle sebe (ikona šipky dolů).</span><span class="sxs-lookup"><span data-stu-id="8ee9d-172">The only difference is that extension methods appear with a special symbol next to them (an icon of a downward arrow).</span></span>

<span data-ttu-id="8ee9d-173">[![pomocí rozšiřující metody HTML. Label ()](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="8ee9d-173">[![Using the Html.Label() extension method](creating-custom-html-helpers-vb/_static/image5.png)](creating-custom-html-helpers-vb/_static/image4.png)</span></span>

<span data-ttu-id="8ee9d-174">**Obrázek 02**: použití rozšiřující metody HTML. Label () ([kliknutím zobrazíte obrázek v plné velikosti](creating-custom-html-helpers-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="8ee9d-174">**Figure 02**: Using the Html.Label() extension method  ([Click to view full-size image](creating-custom-html-helpers-vb/_static/image6.png))</span></span>

<span data-ttu-id="8ee9d-175">Změněné zobrazení indexu v seznamu 4 používá metodu rozšíření HTML. Label () k vykreslení všech značek &lt;popisku&gt;.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-175">The modified Index view in Listing 4 uses the Html.Label() extension method to render all of its &lt;label&gt; tags.</span></span>

<span data-ttu-id="8ee9d-176">**Výpis 4 – `Views\Home\Index3.aspx`**</span><span class="sxs-lookup"><span data-stu-id="8ee9d-176">**Listing 4 – `Views\Home\Index3.aspx`**</span></span>

[!code-aspx[Main](creating-custom-html-helpers-vb/samples/sample6.aspx)]

## <a name="summary"></a><span data-ttu-id="8ee9d-177">Přehled</span><span class="sxs-lookup"><span data-stu-id="8ee9d-177">Summary</span></span>

<span data-ttu-id="8ee9d-178">V tomto kurzu jste se naučili dvě metody vytváření vlastních pomocníků HTML.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-178">In this tutorial, you learned two methods of creating custom HTML Helpers.</span></span> <span data-ttu-id="8ee9d-179">Nejdříve jste zjistili, jak vytvořit vlastní nápovědu `Label()` HTML vytvořením sdílené metody, která vrací řetězec.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-179">First, you learned how to create a custom `Label()` HTML Helper by creating a shared method that returns a string.</span></span> <span data-ttu-id="8ee9d-180">Dále jste zjistili, jak vytvořit vlastní pomocnou metodu `Label()` HTML vytvořením metody rozšíření na `HtmlHelper` třídě.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-180">Next, you learned how to create a custom `Label()` HTML Helper method by creating an extension method on the `HtmlHelper` class.</span></span>

<span data-ttu-id="8ee9d-181">V tomto kurzu se zaměřujeme na sestavování velmi jednoduchých pomocných metod HTML.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-181">In this tutorial, I focused on building an extremely simple HTML Helper method.</span></span> <span data-ttu-id="8ee9d-182">Mějte na paměti, že pomocný objekt HTML může být tak složitý, jak chcete.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-182">Realize that an HTML Helper can be as complicated as you want.</span></span> <span data-ttu-id="8ee9d-183">Můžete vytvořit pomocníky HTML, které vykreslují bohatý obsah, jako jsou zobrazení stromové struktury, nabídky nebo tabulky dat databáze.</span><span class="sxs-lookup"><span data-stu-id="8ee9d-183">You can build HTML Helpers that render rich content such as tree views, menus, or tables of database data.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8ee9d-184">[Předchozí](asp-net-mvc-views-overview-vb.md)
> [Další](using-the-tagbuilder-class-to-build-html-helpers-vb.md)</span><span class="sxs-lookup"><span data-stu-id="8ee9d-184">[Previous](asp-net-mvc-views-overview-vb.md)
[Next](using-the-tagbuilder-class-to-build-html-helpers-vb.md)</span></span>

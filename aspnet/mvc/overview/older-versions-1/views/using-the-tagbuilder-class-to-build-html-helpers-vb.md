---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
title: Použití třídy TagBuilder k vytváření pomocníků HTML (VB) | Microsoft Docs
author: StephenWalther
description: Stephen Walther vás seznámí s užitečnou třídou nástrojů v rozhraní ASP.NET MVC s názvem třídy TagBuilder. Můžete snadno použít třídu TagBuilder...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: ec26f264-d0ea-4031-9943-825505a3ac4b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 3b0aa9816209cc326d3dea4b8dfb1b13cf697fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600000"
---
# <a name="using-the-tagbuilder-class-to-build-html-helpers-vb"></a><span data-ttu-id="a4f9d-104">Použití třídy TagBuilder k vytváření pomocníků HTML (VB)</span><span class="sxs-lookup"><span data-stu-id="a4f9d-104">Using the TagBuilder Class to Build HTML Helpers (VB)</span></span>

<span data-ttu-id="a4f9d-105">od [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="a4f9d-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="a4f9d-106">Stephen Walther vás seznámí s užitečnou třídou nástrojů v rozhraní ASP.NET MVC s názvem třídy TagBuilder.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-106">Stephen Walther introduces you to a useful utility class in the ASP.NET MVC framework named the TagBuilder class.</span></span> <span data-ttu-id="a4f9d-107">Třídu TagBuilder lze použít k snadnému sestavení značek jazyka HTML.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-107">You can use the TagBuilder class to easily build HTML tags.</span></span>

<span data-ttu-id="a4f9d-108">Rozhraní ASP.NET MVC obsahuje užitečnou třídu nástrojů nazvanou TagBuilder třídu, kterou lze použít při vytváření pomocníků HTML.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-108">The ASP.NET MVC framework includes a useful utility class named the TagBuilder class that you can use when building HTML helpers.</span></span> <span data-ttu-id="a4f9d-109">Třída TagBuilder, jak naznačuje název třídy, umožňuje snadno vytvářet značky HTML.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-109">The TagBuilder class, as the name of the class suggests, enables you to easily build HTML tags.</span></span> <span data-ttu-id="a4f9d-110">V tomto stručném kurzu se poskytuje přehled třídy TagBuilder a naučíte se, jak tuto třídu použít při vytváření jednoduchého pomocníka HTML, který vykresluje HTML &lt;img&gt; značky.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-110">In this brief tutorial, you are provided with an overview of the TagBuilder class and you learn how to use this class when building a simple HTML helper that renders HTML &lt;img&gt; tags.</span></span>

## <a name="overview-of-the-tagbuilder-class"></a><span data-ttu-id="a4f9d-111">Přehled třídy TagBuilder</span><span class="sxs-lookup"><span data-stu-id="a4f9d-111">Overview of the TagBuilder Class</span></span>

<span data-ttu-id="a4f9d-112">Třída TagBuilder je obsažena v oboru názvů System. Web. Mvc.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-112">The TagBuilder class is contained in the System.Web.Mvc namespace.</span></span> <span data-ttu-id="a4f9d-113">Má pět metod:</span><span class="sxs-lookup"><span data-stu-id="a4f9d-113">It has five methods:</span></span>

- <span data-ttu-id="a4f9d-114">AddCssClass () – umožňuje přidat do značky nový atribut *Class = ""* .</span><span class="sxs-lookup"><span data-stu-id="a4f9d-114">AddCssClass() – Enables you to add a new *class=""* attribute to a tag.</span></span>
- <span data-ttu-id="a4f9d-115">GenerateId () – umožňuje přidat atribut ID k značce.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-115">GenerateId() – Enables you to add an id attribute to a tag.</span></span> <span data-ttu-id="a4f9d-116">Tato metoda automaticky nahrazuje tečky v ID (ve výchozím nastavení jsou tečky nahrazeny podtržítky).</span><span class="sxs-lookup"><span data-stu-id="a4f9d-116">This method automatically replaces periods in the id (by default, periods are replaced by underscores)</span></span>
- <span data-ttu-id="a4f9d-117">MergeAttribute () – umožňuje přidat atributy do značky.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-117">MergeAttribute() – Enables you to add attributes to a tag.</span></span> <span data-ttu-id="a4f9d-118">Existuje více přetížení této metody.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-118">There are multiple overloads of this method.</span></span>
- <span data-ttu-id="a4f9d-119">SetInnerText () – umožňuje nastavit vnitřní text značky.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-119">SetInnerText() – Enables you to set the inner text of the tag.</span></span> <span data-ttu-id="a4f9d-120">Vnitřní text je automaticky kódován HTML.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-120">The inner text is HTML encode automatically.</span></span>
- <span data-ttu-id="a4f9d-121">ToString () – umožňuje vykreslit značku.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-121">ToString() – Enables you to render the tag.</span></span> <span data-ttu-id="a4f9d-122">Můžete určit, zda chcete vytvořit normální značku, počáteční značku, koncovou značku nebo samočinnou uzavírací značku.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-122">You can specify whether you want to create a normal tag, a start tag, an end tag, or a self-closing tag.</span></span>

<span data-ttu-id="a4f9d-123">Třída TagBuilder má čtyři důležité vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="a4f9d-123">The TagBuilder class has four important properties:</span></span>

- <span data-ttu-id="a4f9d-124">Atributy – představuje všechny atributy značky.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-124">Attributes – Represents all of the attributes of the tag.</span></span>
- <span data-ttu-id="a4f9d-125">IdAttributeDotReplacement – představuje znak používaný metodou GenerateId () k nahrazení teček (výchozí je podtržítko).</span><span class="sxs-lookup"><span data-stu-id="a4f9d-125">IdAttributeDotReplacement – Represents the character used by the GenerateId() method to replace periods (the default is an underscore).</span></span>
- <span data-ttu-id="a4f9d-126">InnerHTML – představuje vnitřní obsah značky.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-126">InnerHTML – Represents the inner contents of the tag.</span></span> <span data-ttu-id="a4f9d-127">Přiřazení řetězce k *této vlastnosti* nekóduje řetězec ve formátu HTML.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-127">Assigning a string to this property *does not* HTML encode the string.</span></span>
- <span data-ttu-id="a4f9d-128">TagName – představuje název značky.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-128">TagName – Represents the name of the tag.</span></span>

<span data-ttu-id="a4f9d-129">Tyto metody a vlastnosti poskytují všechny základní metody a vlastnosti, které potřebujete k vytvoření značky jazyka HTML.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-129">These methods and properties give you all of the basic methods and properties that you need to build up an HTML tag.</span></span> <span data-ttu-id="a4f9d-130">Ve skutečnosti nemusíte používat třídu TagBuilder.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-130">You don't really need to use the TagBuilder class.</span></span> <span data-ttu-id="a4f9d-131">Místo toho můžete použít třídu StringBuilder.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-131">You could use a StringBuilder class instead.</span></span> <span data-ttu-id="a4f9d-132">Třída TagBuilder ale ještě víc zjednodušuje život.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-132">However, the TagBuilder class makes your life a little easier.</span></span>

## <a name="creating-an-image-html-helper"></a><span data-ttu-id="a4f9d-133">Vytvoření pomocníka s obrázkem HTML</span><span class="sxs-lookup"><span data-stu-id="a4f9d-133">Creating an Image HTML Helper</span></span>

<span data-ttu-id="a4f9d-134">Při vytváření instance třídy TagBuilder předáte název značky, kterou chcete sestavit do konstruktoru TagBuilder.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-134">When you create an instance of the TagBuilder class, you pass the name of the tag that you want to build to the TagBuilder constructor.</span></span> <span data-ttu-id="a4f9d-135">Dále můžete volat metody jako metody AddCssClass a MergeAttribute () pro úpravu atributů značky.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-135">Next, you can call methods like the AddCssClass and MergeAttribute() methods to modify the attributes of the tag.</span></span> <span data-ttu-id="a4f9d-136">Nakonec zavoláte metodu ToString () pro vykreslení značky.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-136">Finally, you call the ToString() method to render the tag.</span></span>

<span data-ttu-id="a4f9d-137">Například výpis 1 obsahuje pomocníka s obrázkem HTML.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-137">For example, Listing 1 contains an Image HTML helper.</span></span> <span data-ttu-id="a4f9d-138">Pomocná rutina Image je implementována interně pomocí TagBuilder, který představuje značku&gt; HTML &lt;img.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-138">The Image helper is implemented internally with a TagBuilder that represents an HTML &lt;img&gt; tag.</span></span>

<span data-ttu-id="a4f9d-139">**Výpis 1 – Helpers\ImageHelper.vb**</span><span class="sxs-lookup"><span data-stu-id="a4f9d-139">**Listing 1 – Helpers\ImageHelper.vb**</span></span>

[!code-vb[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample1.vb)]

<span data-ttu-id="a4f9d-140">Modul v seznamu 1 obsahuje dvě přetížené metody s názvem Image ().</span><span class="sxs-lookup"><span data-stu-id="a4f9d-140">The module in Listing 1 contains two overloaded methods named Image().</span></span> <span data-ttu-id="a4f9d-141">Při volání metody image () můžete předat objekt, který představuje sadu atributů HTML, nebo ne.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-141">When you call the Image() method, you can pass an object which represents a set of HTML attributes or not.</span></span>

<span data-ttu-id="a4f9d-142">Všimněte si, jak metoda TagBuilder. MergeAttribute () slouží k přidání jednotlivých atributů, jako je například atribut src, do TagBuilder.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-142">Notice how the TagBuilder.MergeAttribute() method is used to add individual attributes such as the src attribute to the TagBuilder.</span></span> <span data-ttu-id="a4f9d-143">Všimněte si navíc, jak metoda TagBuilder. MergeAttributes () slouží k přidání kolekce atributů do TagBuilder.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-143">Notice, furthermore, how the TagBuilder.MergeAttributes() method is used to add a collection of attributes to the TagBuilder.</span></span> <span data-ttu-id="a4f9d-144">Metoda MergeAttributes () přijímá slovník&lt;řetězec&gt; parametr.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-144">The MergeAttributes() method accepts a Dictionary&lt;string,object&gt; parameter.</span></span> <span data-ttu-id="a4f9d-145">Třída RouteValueDictionary slouží k převodu objektu reprezentujícího kolekci atributů do slovníku&lt;řetězec&gt;objektu.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-145">The RouteValueDictionary class is used to convert the Object representing the collection of attributes into a Dictionary&lt;string,object&gt;.</span></span>

<span data-ttu-id="a4f9d-146">Po vytvoření pomocné rutiny image můžete použít pomocníka v zobrazeních ASP.NET MVC stejným způsobem jako kterýkoli jiný standardní pomocník HTML.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-146">After you create the Image helper, you can use the helper in your ASP.NET MVC views just like any of the other standard HTML helpers.</span></span> <span data-ttu-id="a4f9d-147">Zobrazení v seznamu 2 používá pomocníka pro Image k zobrazení stejné image Xbox dvakrát (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="a4f9d-147">The view in Listing 2 uses the Image helper to display the same image of an Xbox twice (see Figure 1).</span></span> <span data-ttu-id="a4f9d-148">Pomocná rutina () se nazývá s kolekcí atributů HTML i bez ní.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-148">The Image() helper is called both with and without an HTML attribute collection.</span></span>

<span data-ttu-id="a4f9d-149">**Výpis 2 – Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="a4f9d-149">**Listing 2 – Home\Index.aspx**</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample2.aspx)]

<span data-ttu-id="a4f9d-150">[![dialogového okna Nový projekt](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a4f9d-150">[![The New Project dialog box](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)</span></span>

<span data-ttu-id="a4f9d-151">**Obrázek 01**: použití pomocné rutiny Image ([kliknutím zobrazíte obrázek v plné velikosti](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="a4f9d-151">**Figure 01**: Using the Image helper([Click to view full-size image](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png))</span></span>

<span data-ttu-id="a4f9d-152">Všimněte si, že musíte importovat obor názvů přidružený k pomocné rutině image v horní části zobrazení index. aspx.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-152">Notice that you must import the namespace associated with the Image helper at the top of the Index.aspx view.</span></span> <span data-ttu-id="a4f9d-153">Pomocná rutina se importuje s následující direktivou:</span><span class="sxs-lookup"><span data-stu-id="a4f9d-153">The helper is imported with the following directive:</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample3.aspx)]

<span data-ttu-id="a4f9d-154">V Visual Basic aplikaci je výchozí obor názvů stejný jako název aplikace.</span><span class="sxs-lookup"><span data-stu-id="a4f9d-154">In a Visual Basic application, the default namespace is the same as the name of the application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a4f9d-155">[Předchozí](creating-custom-html-helpers-vb.md)
> [Další](creating-page-layouts-with-view-master-pages-vb.md)</span><span class="sxs-lookup"><span data-stu-id="a4f9d-155">[Previous](creating-custom-html-helpers-vb.md)
[Next](creating-page-layouts-with-view-master-pages-vb.md)</span></span>

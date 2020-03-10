---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
title: Použití třídy TagBuilder k vytváření pomocníků HTML (C#) | Microsoft Docs
author: StephenWalther
description: Stephen Walther vás seznámí s užitečnou třídou nástrojů v rozhraní ASP.NET MVC s názvem třídy TagBuilder. Můžete snadno použít třídu TagBuilder...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 3975a52f-bd15-4edd-8f3d-1df93672515b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-cs
msc.type: authoredcontent
ms.openlocfilehash: c8eaea9932a30c744b9a69861619ce9458b5a23a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600028"
---
# <a name="using-the-tagbuilder-class-to-build-html-helpers-c"></a><span data-ttu-id="9178e-104">Použití třídy TagBuilder k vytváření pomocníků HTML (C#)</span><span class="sxs-lookup"><span data-stu-id="9178e-104">Using the TagBuilder Class to Build HTML Helpers (C#)</span></span>

<span data-ttu-id="9178e-105">od [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="9178e-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="9178e-106">Stephen Walther vás seznámí s užitečnou třídou nástrojů v rozhraní ASP.NET MVC s názvem třídy TagBuilder.</span><span class="sxs-lookup"><span data-stu-id="9178e-106">Stephen Walther introduces you to a useful utility class in the ASP.NET MVC framework named the TagBuilder class.</span></span> <span data-ttu-id="9178e-107">Třídu TagBuilder lze použít k snadnému sestavení značek jazyka HTML.</span><span class="sxs-lookup"><span data-stu-id="9178e-107">You can use the TagBuilder class to easily build HTML tags.</span></span>

<span data-ttu-id="9178e-108">Rozhraní ASP.NET MVC obsahuje užitečnou třídu nástrojů nazvanou TagBuilder třídu, kterou lze použít při vytváření pomocníků HTML.</span><span class="sxs-lookup"><span data-stu-id="9178e-108">The ASP.NET MVC framework includes a useful utility class named the TagBuilder class that you can use when building HTML helpers.</span></span> <span data-ttu-id="9178e-109">Třída TagBuilder, jak naznačuje název třídy, umožňuje snadno vytvářet značky HTML.</span><span class="sxs-lookup"><span data-stu-id="9178e-109">The TagBuilder class, as the name of the class suggests, enables you to easily build HTML tags.</span></span> <span data-ttu-id="9178e-110">V tomto stručném kurzu se poskytuje přehled třídy TagBuilder a naučíte se, jak tuto třídu použít při vytváření jednoduchého pomocníka HTML, který vykresluje HTML &lt;img&gt; značky.</span><span class="sxs-lookup"><span data-stu-id="9178e-110">In this brief tutorial, you are provided with an overview of the TagBuilder class and you learn how to use this class when building a simple HTML helper that renders HTML &lt;img&gt; tags.</span></span>

## <a name="overview-of-the-tagbuilder-class"></a><span data-ttu-id="9178e-111">Přehled třídy TagBuilder</span><span class="sxs-lookup"><span data-stu-id="9178e-111">Overview of the TagBuilder Class</span></span>

<span data-ttu-id="9178e-112">Třída TagBuilder je obsažena v oboru názvů System. Web. Mvc.</span><span class="sxs-lookup"><span data-stu-id="9178e-112">The TagBuilder class is contained in the System.Web.Mvc namespace.</span></span> <span data-ttu-id="9178e-113">Má pět metod:</span><span class="sxs-lookup"><span data-stu-id="9178e-113">It has five methods:</span></span>

- <span data-ttu-id="9178e-114">AddCssClass () – umožňuje přidat do značky nový atribut *Class = ""* .</span><span class="sxs-lookup"><span data-stu-id="9178e-114">AddCssClass() - Enables you to add a new *class=""* attribute to a tag.</span></span>
- <span data-ttu-id="9178e-115">GenerateId () – umožňuje přidat atribut ID k značce.</span><span class="sxs-lookup"><span data-stu-id="9178e-115">GenerateId() - Enables you to add an id attribute to a tag.</span></span> <span data-ttu-id="9178e-116">Tato metoda automaticky nahrazuje tečky v ID (ve výchozím nastavení jsou tečky nahrazeny podtržítky).</span><span class="sxs-lookup"><span data-stu-id="9178e-116">This method automatically replaces periods in the id (by default, periods are replaced by underscores)</span></span>
- <span data-ttu-id="9178e-117">MergeAttribute () – umožňuje přidat atributy do značky.</span><span class="sxs-lookup"><span data-stu-id="9178e-117">MergeAttribute() - Enables you to add attributes to a tag.</span></span> <span data-ttu-id="9178e-118">Existuje více přetížení této metody.</span><span class="sxs-lookup"><span data-stu-id="9178e-118">There are multiple overloads of this method.</span></span>
- <span data-ttu-id="9178e-119">SetInnerText () – umožňuje nastavit vnitřní text značky.</span><span class="sxs-lookup"><span data-stu-id="9178e-119">SetInnerText() - Enables you to set the inner text of the tag.</span></span> <span data-ttu-id="9178e-120">Vnitřní text je automaticky kódován HTML.</span><span class="sxs-lookup"><span data-stu-id="9178e-120">The inner text is HTML encode automatically.</span></span>
- <span data-ttu-id="9178e-121">ToString () – umožňuje vykreslit značku.</span><span class="sxs-lookup"><span data-stu-id="9178e-121">ToString() - Enables you to render the tag.</span></span> <span data-ttu-id="9178e-122">Můžete určit, zda chcete vytvořit normální značku, počáteční značku, koncovou značku nebo samočinnou uzavírací značku.</span><span class="sxs-lookup"><span data-stu-id="9178e-122">You can specify whether you want to create a normal tag, a start tag, an end tag, or a self-closing tag.</span></span>

<span data-ttu-id="9178e-123">Třída TagBuilder má čtyři důležité vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="9178e-123">The TagBuilder class has four important properties:</span></span>

- <span data-ttu-id="9178e-124">Atributy – představuje všechny atributy značky.</span><span class="sxs-lookup"><span data-stu-id="9178e-124">Attributes - Represents all of the attributes of the tag.</span></span>
- <span data-ttu-id="9178e-125">IdAttributeDotReplacement – představuje znak používaný metodou GenerateId () k nahrazení teček (výchozí je podtržítko).</span><span class="sxs-lookup"><span data-stu-id="9178e-125">IdAttributeDotReplacement - Represents the character used by the GenerateId() method to replace periods (the default is an underscore).</span></span>
- <span data-ttu-id="9178e-126">InnerHTML – představuje vnitřní obsah značky.</span><span class="sxs-lookup"><span data-stu-id="9178e-126">InnerHTML - Represents the inner contents of the tag.</span></span> <span data-ttu-id="9178e-127">Přiřazení řetězce k *této vlastnosti* nekóduje řetězec ve formátu HTML.</span><span class="sxs-lookup"><span data-stu-id="9178e-127">Assigning a string to this property *does not* HTML encode the string.</span></span>
- <span data-ttu-id="9178e-128">TagName – představuje název značky.</span><span class="sxs-lookup"><span data-stu-id="9178e-128">TagName - Represents the name of the tag.</span></span>

<span data-ttu-id="9178e-129">Tyto metody a vlastnosti poskytují všechny základní metody a vlastnosti, které potřebujete k vytvoření značky jazyka HTML.</span><span class="sxs-lookup"><span data-stu-id="9178e-129">These methods and properties give you all of the basic methods and properties that you need to build up an HTML tag.</span></span> <span data-ttu-id="9178e-130">Ve skutečnosti nemusíte používat třídu TagBuilder.</span><span class="sxs-lookup"><span data-stu-id="9178e-130">You don't really need to use the TagBuilder class.</span></span> <span data-ttu-id="9178e-131">Místo toho můžete použít třídu StringBuilder.</span><span class="sxs-lookup"><span data-stu-id="9178e-131">You could use a StringBuilder class instead.</span></span> <span data-ttu-id="9178e-132">Třída TagBuilder ale ještě víc zjednodušuje život.</span><span class="sxs-lookup"><span data-stu-id="9178e-132">However, the TagBuilder class makes your life a little easier.</span></span>

## <a name="creating-an-image-html-helper"></a><span data-ttu-id="9178e-133">Vytvoření pomocníka s obrázkem HTML</span><span class="sxs-lookup"><span data-stu-id="9178e-133">Creating an Image HTML Helper</span></span>

<span data-ttu-id="9178e-134">Při vytváření instance třídy TagBuilder předáte název značky, kterou chcete sestavit do konstruktoru TagBuilder.</span><span class="sxs-lookup"><span data-stu-id="9178e-134">When you create an instance of the TagBuilder class, you pass the name of the tag that you want to build to the TagBuilder constructor.</span></span> <span data-ttu-id="9178e-135">Dále můžete volat metody jako metody AddCssClass a MergeAttribute () pro úpravu atributů značky.</span><span class="sxs-lookup"><span data-stu-id="9178e-135">Next, you can call methods like the AddCssClass and MergeAttribute() methods to modify the attributes of the tag.</span></span> <span data-ttu-id="9178e-136">Nakonec zavoláte metodu ToString () pro vykreslení značky.</span><span class="sxs-lookup"><span data-stu-id="9178e-136">Finally, you call the ToString() method to render the tag.</span></span>

<span data-ttu-id="9178e-137">Například výpis 1 obsahuje pomocníka s obrázkem HTML.</span><span class="sxs-lookup"><span data-stu-id="9178e-137">For example, Listing 1 contains an Image HTML helper.</span></span> <span data-ttu-id="9178e-138">Pomocná rutina Image je implementována interně pomocí TagBuilder, který představuje značku&gt; HTML &lt;img.</span><span class="sxs-lookup"><span data-stu-id="9178e-138">The Image helper is implemented internally with a TagBuilder that represents an HTML &lt;img&gt; tag.</span></span>

<span data-ttu-id="9178e-139">**Výpis 1 – Helpers\ImageHelper.cs**</span><span class="sxs-lookup"><span data-stu-id="9178e-139">**Listing 1 - Helpers\ImageHelper.cs**</span></span>

[!code-csharp[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample1.cs)]

<span data-ttu-id="9178e-140">Třída v seznamu 1 obsahuje dvě statické přetížené metody s názvem Image.</span><span class="sxs-lookup"><span data-stu-id="9178e-140">The class in Listing 1 contains two static overloaded methods named Image.</span></span> <span data-ttu-id="9178e-141">Při volání metody image () můžete předat objekt, který představuje sadu atributů HTML, nebo ne.</span><span class="sxs-lookup"><span data-stu-id="9178e-141">When you call the Image() method, you can pass an object which represents a set of HTML attributes or not.</span></span>

<span data-ttu-id="9178e-142">Všimněte si, jak metoda TagBuilder. MergeAttribute () slouží k přidání jednotlivých atributů, jako je například atribut src, do TagBuilder.</span><span class="sxs-lookup"><span data-stu-id="9178e-142">Notice how the TagBuilder.MergeAttribute() method is used to add individual attributes such as the src attribute to the TagBuilder.</span></span> <span data-ttu-id="9178e-143">Všimněte si navíc, jak metoda TagBuilder. MergeAttributes () slouží k přidání kolekce atributů do TagBuilder.</span><span class="sxs-lookup"><span data-stu-id="9178e-143">Notice, furthermore, how the TagBuilder.MergeAttributes() method is used to add a collection of attributes to the TagBuilder.</span></span> <span data-ttu-id="9178e-144">Metoda MergeAttributes () přijímá slovník&lt;řetězec&gt; parametr.</span><span class="sxs-lookup"><span data-stu-id="9178e-144">The MergeAttributes() method accepts a Dictionary&lt;string,object&gt; parameter.</span></span> <span data-ttu-id="9178e-145">Třída RouteValueDictionary slouží k převodu objektu reprezentujícího kolekci atributů do slovníku&lt;řetězec&gt;objektu.</span><span class="sxs-lookup"><span data-stu-id="9178e-145">The RouteValueDictionary class is used to convert the Object representing the collection of attributes into a Dictionary&lt;string,object&gt;.</span></span>

<span data-ttu-id="9178e-146">Po vytvoření pomocné rutiny image můžete použít pomocníka v zobrazeních ASP.NET MVC stejným způsobem jako kterýkoli jiný standardní pomocník HTML.</span><span class="sxs-lookup"><span data-stu-id="9178e-146">After you create the Image helper, you can use the helper in your ASP.NET MVC views just like any of the other standard HTML helpers.</span></span> <span data-ttu-id="9178e-147">Zobrazení v seznamu 2 používá pomocníka pro Image k zobrazení stejné image Xbox dvakrát (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="9178e-147">The view in Listing 2 uses the Image helper to display the same image of an Xbox twice (see Figure 1).</span></span> <span data-ttu-id="9178e-148">Pomocná rutina () se nazývá s kolekcí atributů HTML i bez ní.</span><span class="sxs-lookup"><span data-stu-id="9178e-148">The Image() helper is called both with and without an HTML attribute collection.</span></span>

<span data-ttu-id="9178e-149">**Výpis 2 – Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="9178e-149">**Listing 2 - Home\Index.aspx**</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample2.aspx)]

<span data-ttu-id="9178e-150">[![dialogového okna Nový projekt](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9178e-150">[![The New Project dialog box](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image1.png)</span></span>

<span data-ttu-id="9178e-151">**Obrázek 01**: použití pomocné rutiny Image ([kliknutím zobrazíte obrázek v plné velikosti](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="9178e-151">**Figure 01**: Using the Image helper([Click to view full-size image](using-the-tagbuilder-class-to-build-html-helpers-cs/_static/image2.png))</span></span>

<span data-ttu-id="9178e-152">Všimněte si, že musíte importovat obor názvů přidružený k pomocné rutině image v horní části zobrazení index. aspx.</span><span class="sxs-lookup"><span data-stu-id="9178e-152">Notice that you must import the namespace associated with the Image helper at the top of the Index.aspx view.</span></span> <span data-ttu-id="9178e-153">Pomocná rutina se importuje s následující direktivou:</span><span class="sxs-lookup"><span data-stu-id="9178e-153">The helper is imported with the following directive:</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-cs/samples/sample3.aspx)]

> [!div class="step-by-step"]
> <span data-ttu-id="9178e-154">[Předchozí](creating-custom-html-helpers-cs.md)
> [Další](creating-page-layouts-with-view-master-pages-cs.md)</span><span class="sxs-lookup"><span data-stu-id="9178e-154">[Previous](creating-custom-html-helpers-cs.md)
[Next](creating-page-layouts-with-view-master-pages-cs.md)</span></span>

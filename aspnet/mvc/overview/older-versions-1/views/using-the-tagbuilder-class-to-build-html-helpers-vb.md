---
uid: mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
title: Pomocí třída TagBuilder pro sestavení pomocných rutin HTML (VB) | Dokumentace Microsoftu
author: StephenWalther
description: Stephen Walther vás seznámí s třídu v rozhraní ASP.NET MVC s názvem třída TagBuilder užitečné nástroje. Třída TagBuilder pro můžete snadno použít...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: ec26f264-d0ea-4031-9943-825505a3ac4b
msc.legacyurl: /mvc/overview/older-versions-1/views/using-the-tagbuilder-class-to-build-html-helpers-vb
msc.type: authoredcontent
ms.openlocfilehash: 3b0aa9816209cc326d3dea4b8dfb1b13cf697fcd
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65130366"
---
# <a name="using-the-tagbuilder-class-to-build-html-helpers-vb"></a><span data-ttu-id="3e9cc-104">Pomocí třída TagBuilder pro sestavení pomocných rutin HTML (VB)</span><span class="sxs-lookup"><span data-stu-id="3e9cc-104">Using the TagBuilder Class to Build HTML Helpers (VB)</span></span>

<span data-ttu-id="3e9cc-105">podle [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="3e9cc-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="3e9cc-106">Stephen Walther vás seznámí s třídu v rozhraní ASP.NET MVC s názvem třída TagBuilder užitečné nástroje.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-106">Stephen Walther introduces you to a useful utility class in the ASP.NET MVC framework named the TagBuilder class.</span></span> <span data-ttu-id="3e9cc-107">Třída TagBuilder můžete použít k snadnému vytváření značky HTML.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-107">You can use the TagBuilder class to easily build HTML tags.</span></span>

<span data-ttu-id="3e9cc-108">Architektura ASP.NET MVC zahrnuje užitečný nástroj pro třídu s názvem třída TagBuilder, který vám pomůže při vytváření pomocných rutin HTML.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-108">The ASP.NET MVC framework includes a useful utility class named the TagBuilder class that you can use when building HTML helpers.</span></span> <span data-ttu-id="3e9cc-109">Třída TagBuilder jako název třídy navrhuje, vám umožní snadno vytvářet značky HTML.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-109">The TagBuilder class, as the name of the class suggests, enables you to easily build HTML tags.</span></span> <span data-ttu-id="3e9cc-110">V tomto kurzu (BRIEF) k dispozici máte přehled o třída TagBuilder a zjistíte, jak použít tuto třídu při vytváření jednoduchých pomocné rutiny HTML, který vykreslí HTML &lt;img&gt; značky.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-110">In this brief tutorial, you are provided with an overview of the TagBuilder class and you learn how to use this class when building a simple HTML helper that renders HTML &lt;img&gt; tags.</span></span>

## <a name="overview-of-the-tagbuilder-class"></a><span data-ttu-id="3e9cc-111">Třída TagBuilder-přehled</span><span class="sxs-lookup"><span data-stu-id="3e9cc-111">Overview of the TagBuilder Class</span></span>

<span data-ttu-id="3e9cc-112">Třída TagBuilder je obsažen v oboru názvů System.Web.Mvc.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-112">The TagBuilder class is contained in the System.Web.Mvc namespace.</span></span> <span data-ttu-id="3e9cc-113">Má pět metod:</span><span class="sxs-lookup"><span data-stu-id="3e9cc-113">It has five methods:</span></span>

- <span data-ttu-id="3e9cc-114">AddCssClass() – umožňuje přidat nový *třídy = ""* atributů pro značku.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-114">AddCssClass() – Enables you to add a new *class=""* attribute to a tag.</span></span>
- <span data-ttu-id="3e9cc-115">GenerateId() – umožňuje přidat atribut id značky.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-115">GenerateId() – Enables you to add an id attribute to a tag.</span></span> <span data-ttu-id="3e9cc-116">Tato metoda automaticky nahrazuje tečky v id (ve výchozím nastavení, tečky jsou nahrazené podtržítka)</span><span class="sxs-lookup"><span data-stu-id="3e9cc-116">This method automatically replaces periods in the id (by default, periods are replaced by underscores)</span></span>
- <span data-ttu-id="3e9cc-117">MergeAttribute() – umožňuje přidat atributů pro značku.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-117">MergeAttribute() – Enables you to add attributes to a tag.</span></span> <span data-ttu-id="3e9cc-118">Existuje více přetížení této metody.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-118">There are multiple overloads of this method.</span></span>
- <span data-ttu-id="3e9cc-119">SetInnerText() – umožňuje nastavit vnitřní text značky.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-119">SetInnerText() – Enables you to set the inner text of the tag.</span></span> <span data-ttu-id="3e9cc-120">Vnitřní text je automaticky použije kódování HTML.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-120">The inner text is HTML encode automatically.</span></span>
- <span data-ttu-id="3e9cc-121">ToString() – Umožňuje vykreslit značky.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-121">ToString() – Enables you to render the tag.</span></span> <span data-ttu-id="3e9cc-122">Můžete určit, zda chcete vytvořit značku normální, počáteční značku, koncovou značku nebo samouzavírací značky.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-122">You can specify whether you want to create a normal tag, a start tag, an end tag, or a self-closing tag.</span></span>

<span data-ttu-id="3e9cc-123">Třída TagBuilder má čtyři důležité vlastnosti:</span><span class="sxs-lookup"><span data-stu-id="3e9cc-123">The TagBuilder class has four important properties:</span></span>

- <span data-ttu-id="3e9cc-124">Atributy – reprezentuje všechny atributy značky.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-124">Attributes – Represents all of the attributes of the tag.</span></span>
- <span data-ttu-id="3e9cc-125">IdAttributeDotReplacement – hodnota představuje znak metodou GenerateId() používá k nahrazení tečky (výchozí hodnota je podtržítko).</span><span class="sxs-lookup"><span data-stu-id="3e9cc-125">IdAttributeDotReplacement – Represents the character used by the GenerateId() method to replace periods (the default is an underscore).</span></span>
- <span data-ttu-id="3e9cc-126">InnerHTML – představuje vnitřní obsah značky.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-126">InnerHTML – Represents the inner contents of the tag.</span></span> <span data-ttu-id="3e9cc-127">Přiřazení k této vlastnosti řetězce *nemá* řetězec s kódováním HTML.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-127">Assigning a string to this property *does not* HTML encode the string.</span></span>
- <span data-ttu-id="3e9cc-128">TagName – představuje název značky.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-128">TagName – Represents the name of the tag.</span></span>

<span data-ttu-id="3e9cc-129">Tyto metody a vlastnosti získáte všechny základní metody a vlastnosti, které potřebujete k vytvoření značky jazyka HTML.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-129">These methods and properties give you all of the basic methods and properties that you need to build up an HTML tag.</span></span> <span data-ttu-id="3e9cc-130">Není nutné opravdu použít třída TagBuilder.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-130">You don't really need to use the TagBuilder class.</span></span> <span data-ttu-id="3e9cc-131">Třída StringBuilder můžete místo toho použít.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-131">You could use a StringBuilder class instead.</span></span> <span data-ttu-id="3e9cc-132">Nicméně třída TagBuilder vám život o něco jednodušší.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-132">However, the TagBuilder class makes your life a little easier.</span></span>

## <a name="creating-an-image-html-helper"></a><span data-ttu-id="3e9cc-133">Vytvoření pomocné rutiny HTML bitové kopie</span><span class="sxs-lookup"><span data-stu-id="3e9cc-133">Creating an Image HTML Helper</span></span>

<span data-ttu-id="3e9cc-134">Při vytváření instance třídy TagBuilder předat název značky, který má být sestaveno TagBuilder konstruktoru.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-134">When you create an instance of the TagBuilder class, you pass the name of the tag that you want to build to the TagBuilder constructor.</span></span> <span data-ttu-id="3e9cc-135">V dalším kroku může volat metody jako metody AddCssClass a MergeAttribute() změnit atributy značky.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-135">Next, you can call methods like the AddCssClass and MergeAttribute() methods to modify the attributes of the tag.</span></span> <span data-ttu-id="3e9cc-136">Nakonec proveďte volání metody ToString() k vykreslení značky.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-136">Finally, you call the ToString() method to render the tag.</span></span>

<span data-ttu-id="3e9cc-137">Výpis 1 obsahuje například pomocné rutiny HTML bitové kopie.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-137">For example, Listing 1 contains an Image HTML helper.</span></span> <span data-ttu-id="3e9cc-138">Pomocná rutina obrázku je implementována interně pomocí TagBuilder, který představuje HTML &lt;img&gt; značky.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-138">The Image helper is implemented internally with a TagBuilder that represents an HTML &lt;img&gt; tag.</span></span>

<span data-ttu-id="3e9cc-139">**Výpis 1 – Helpers\ImageHelper.vb**</span><span class="sxs-lookup"><span data-stu-id="3e9cc-139">**Listing 1 – Helpers\ImageHelper.vb**</span></span>

[!code-vb[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample1.vb)]

<span data-ttu-id="3e9cc-140">Modulu ve výpisu 1 obsahuje dvě přetížené metody s názvem Image().</span><span class="sxs-lookup"><span data-stu-id="3e9cc-140">The module in Listing 1 contains two overloaded methods named Image().</span></span> <span data-ttu-id="3e9cc-141">Při volání metody Image(), můžete předat objekt, který představuje sadu atributů HTML, nebo ne.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-141">When you call the Image() method, you can pass an object which represents a set of HTML attributes or not.</span></span>

<span data-ttu-id="3e9cc-142">Všimněte si, jak metoda TagBuilder.MergeAttribute() umožňuje přidat jednotlivé atributy, jako je například atribut src TagBuilder.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-142">Notice how the TagBuilder.MergeAttribute() method is used to add individual attributes such as the src attribute to the TagBuilder.</span></span> <span data-ttu-id="3e9cc-143">Všimněte si, jak metoda TagBuilder.MergeAttributes() umožňuje přidat kolekci atributů TagBuilder.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-143">Notice, furthermore, how the TagBuilder.MergeAttributes() method is used to add a collection of attributes to the TagBuilder.</span></span> <span data-ttu-id="3e9cc-144">Metoda MergeAttributes() přijímá slovník&lt;řetězec, objekt&gt; parametru.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-144">The MergeAttributes() method accepts a Dictionary&lt;string,object&gt; parameter.</span></span> <span data-ttu-id="3e9cc-145">Třída RouteValueDictionary se používá k převodu objekt představující kolekci atributů do slovníku&lt;řetězec, objekt&gt;.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-145">The RouteValueDictionary class is used to convert the Object representing the collection of attributes into a Dictionary&lt;string,object&gt;.</span></span>

<span data-ttu-id="3e9cc-146">Po vytvoření Image pomocné rutiny, můžete v zobrazení ASP.NET MVC stejně jako u libovolné ostatní standardní pomocných rutin HTML pomocné rutiny.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-146">After you create the Image helper, you can use the helper in your ASP.NET MVC views just like any of the other standard HTML helpers.</span></span> <span data-ttu-id="3e9cc-147">Zobrazení výpisu 2 používá pomocná rutina obrázku pro zobrazení zobrazí stejný obraz Xboxu dvakrát (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="3e9cc-147">The view in Listing 2 uses the Image helper to display the same image of an Xbox twice (see Figure 1).</span></span> <span data-ttu-id="3e9cc-148">Pomocná rutina Image() je volána s i bez kolekce atributů HTML.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-148">The Image() helper is called both with and without an HTML attribute collection.</span></span>

<span data-ttu-id="3e9cc-149">**Výpis 2 – Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="3e9cc-149">**Listing 2 – Home\Index.aspx**</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample2.aspx)]

<span data-ttu-id="3e9cc-150">[![Dialogové okno Nový projekt](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3e9cc-150">[![The New Project dialog box](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.jpg)](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image1.png)</span></span>

<span data-ttu-id="3e9cc-151">**Obrázek 01**: Použití pomocné rutiny bitové kopie ([kliknutím ji zobrazíte obrázek v plné velikosti](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="3e9cc-151">**Figure 01**: Using the Image helper([Click to view full-size image](using-the-tagbuilder-class-to-build-html-helpers-vb/_static/image2.png))</span></span>

<span data-ttu-id="3e9cc-152">Všimněte si, že je nutné naimportovat přidružené pomocná rutina obrázku v horní části zobrazení Index.aspx obor názvů.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-152">Notice that you must import the namespace associated with the Image helper at the top of the Index.aspx view.</span></span> <span data-ttu-id="3e9cc-153">Pomocné rutiny s následující direktivy importu:</span><span class="sxs-lookup"><span data-stu-id="3e9cc-153">The helper is imported with the following directive:</span></span>

[!code-aspx[Main](using-the-tagbuilder-class-to-build-html-helpers-vb/samples/sample3.aspx)]

<span data-ttu-id="3e9cc-154">V aplikaci Visual Basic výchozí obor názvů je stejný jako název aplikace.</span><span class="sxs-lookup"><span data-stu-id="3e9cc-154">In a Visual Basic application, the default namespace is the same as the name of the application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3e9cc-155">[Předchozí](creating-custom-html-helpers-vb.md)
> [další](creating-page-layouts-with-view-master-pages-vb.md)</span><span class="sxs-lookup"><span data-stu-id="3e9cc-155">[Previous](creating-custom-html-helpers-vb.md)
[Next](creating-page-layouts-with-view-master-pages-vb.md)</span></span>

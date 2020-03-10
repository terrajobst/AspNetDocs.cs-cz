---
uid: web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
title: Vytvoření a použití pomocné rutiny na webu ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Tento článek popisuje, jak vytvořit pomocníka na webu ASP.NET Web Pages (Razor). Pomocná komponenta je opakovaně použitelná součást, která zahrnuje kód a označení ke výkonu...
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 46bff772-01e0-40f0-9ae6-9e18c5442ee6
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 380663951094c9fc7d5f0601e30995fa073a204b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563509"
---
# <a name="creating-and-using-a-helper-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="36be3-104">Vytvoření a použití pomocné rutiny na webu ASP.NET Web Pages (Razor)</span><span class="sxs-lookup"><span data-stu-id="36be3-104">Creating and Using a Helper in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="36be3-105">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="36be3-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="36be3-106">Tento článek popisuje, jak vytvořit pomocníka na webu ASP.NET Web Pages (Razor).</span><span class="sxs-lookup"><span data-stu-id="36be3-106">This article describes how to create a helper in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="36be3-107">*Pomocná* komponenta je opakovaně použitelná součást, která obsahuje kód a kód k provedení úlohy, která může být zdlouhavá nebo složitá.</span><span class="sxs-lookup"><span data-stu-id="36be3-107">A *helper* is a reusable component that includes code and markup to perform a task that might be tedious or complex.</span></span>
> 
> <span data-ttu-id="36be3-108">**Co se naučíte:**</span><span class="sxs-lookup"><span data-stu-id="36be3-108">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="36be3-109">Vytvoření a použití jednoduché pomocné rutiny.</span><span class="sxs-lookup"><span data-stu-id="36be3-109">How to create and use a simple helper.</span></span>
> 
> <span data-ttu-id="36be3-110">Jedná se o funkce ASP.NET, které jsou představené v článku:</span><span class="sxs-lookup"><span data-stu-id="36be3-110">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="36be3-111">Syntaxe `@helper`.</span><span class="sxs-lookup"><span data-stu-id="36be3-111">The `@helper` syntax.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="36be3-112">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="36be3-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="36be3-113">Webové stránky ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="36be3-113">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="36be3-114">Tento kurz funguje také s ASP.NET webovými stránkami 2.</span><span class="sxs-lookup"><span data-stu-id="36be3-114">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="overview-of-helpers"></a><span data-ttu-id="36be3-115">Přehled pomocníků</span><span class="sxs-lookup"><span data-stu-id="36be3-115">Overview of Helpers</span></span>

<span data-ttu-id="36be3-116">Pokud potřebujete na různých stránkách na webu provádět stejné úlohy, můžete použít pomocníka.</span><span class="sxs-lookup"><span data-stu-id="36be3-116">If you need to perform the same tasks on different pages in your site, you can use a helper.</span></span> <span data-ttu-id="36be3-117">Webové stránky ASP.NET obsahují celou řadu pomocníků a je možné si je stáhnout a nainstalovat.</span><span class="sxs-lookup"><span data-stu-id="36be3-117">ASP.NET Web Pages includes a number of helpers, and there are many more that you can download and install.</span></span> <span data-ttu-id="36be3-118">(Seznam integrovaných pomocníků v ASP.NET Web Pages najdete v tématu [rychlý přehled rozhraní API pro ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202907).) Pokud žádný z stávajících pomocných rutin nevyhovuje vašim potřebám, můžete si vytvořit vlastní pomoc.</span><span class="sxs-lookup"><span data-stu-id="36be3-118">(A list of the built-in helpers in ASP.NET Web Pages is listed in the [ASP.NET API Quick Reference](https://go.microsoft.com/fwlink/?LinkId=202907).) If none of the existing helpers meet your needs, you can create your own helper.</span></span>

<span data-ttu-id="36be3-119">Pomocná pomůcka umožňuje použít společný blok kódu na více stránkách.</span><span class="sxs-lookup"><span data-stu-id="36be3-119">A helper lets you use a common block of code across multiple pages.</span></span> <span data-ttu-id="36be3-120">Předpokládejme, že na stránce často chcete vytvořit položku poznámky, která je nastavena od normálních odstavců.</span><span class="sxs-lookup"><span data-stu-id="36be3-120">Suppose that in your page you often want to create a note item that's set apart from normal paragraphs.</span></span> <span data-ttu-id="36be3-121">Možná je Poznámka vytvořena jako prvek `<div>`, který je stylem pole s ohraničením.</span><span class="sxs-lookup"><span data-stu-id="36be3-121">Perhaps the note is created as a `<div>` element that's styled as a box with a border.</span></span> <span data-ttu-id="36be3-122">Místo toho, aby se stejný kód přidal na stránku pokaždé, když chcete zobrazit poznámku, můžete kód zabalit jako pomocný objekt.</span><span class="sxs-lookup"><span data-stu-id="36be3-122">Rather than add this same markup to a page every time you want to display a note, you can package the markup as a helper.</span></span> <span data-ttu-id="36be3-123">Pak můžete poznámku vložit s jedním řádkem kódu kdekoliv, kde ji potřebujete.</span><span class="sxs-lookup"><span data-stu-id="36be3-123">You can then insert the note with a single line of code anywhere you need it.</span></span>

<span data-ttu-id="36be3-124">Použití pomocné rutiny umožňuje, aby byl kód v každé stránce jednodušší a čitelnější.</span><span class="sxs-lookup"><span data-stu-id="36be3-124">Using a helper like this makes the code in each of your pages simpler and easier to read.</span></span> <span data-ttu-id="36be3-125">Také usnadňuje údržbu webu, protože pokud potřebujete změnit vzhled poznámek, můžete změnit označení na jednom místě.</span><span class="sxs-lookup"><span data-stu-id="36be3-125">It also makes it easier to maintain your site, because if you need to change how the notes look, you can change the markup in one place.</span></span>

## <a name="creating-a-helper"></a><span data-ttu-id="36be3-126">Vytvoření pomocné rutiny</span><span class="sxs-lookup"><span data-stu-id="36be3-126">Creating a Helper</span></span>

<span data-ttu-id="36be3-127">V tomto postupu se dozvíte, jak vytvořit pomoc, která vytváří poznámku, jak je popsáno výše.</span><span class="sxs-lookup"><span data-stu-id="36be3-127">This procedure shows you how to create the helper that creates the note, as just described.</span></span> <span data-ttu-id="36be3-128">Toto je jednoduchý příklad, ale vlastní pomoc může obsahovat jakýkoli kód kódu a ASP.NET, který potřebujete.</span><span class="sxs-lookup"><span data-stu-id="36be3-128">This is a simple example, but the custom helper can include any markup and ASP.NET code that you need.</span></span>

1. <span data-ttu-id="36be3-129">V kořenové složce webu vytvořte složku s názvem *App\_Code*.</span><span class="sxs-lookup"><span data-stu-id="36be3-129">In the root folder of the website, create a folder named *App\_Code*.</span></span> <span data-ttu-id="36be3-130">Toto je vyhrazený název složky v ASP.NET, kde můžete umístit kód pro součásti, jako jsou například pomocníky.</span><span class="sxs-lookup"><span data-stu-id="36be3-130">This is a reserved folder name in ASP.NET where you can put code for components like helpers.</span></span>
2. <span data-ttu-id="36be3-131">Ve složce *App\_Code* vytvořte nový soubor *. cshtml* a pojmenujte ho *MyHelpers. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="36be3-131">In the *App\_Code* folder create a new *.cshtml* file and name it *MyHelpers.cshtml*.</span></span>
3. <span data-ttu-id="36be3-132">Existující obsah nahraďte následujícím:</span><span class="sxs-lookup"><span data-stu-id="36be3-132">Replace the existing content with the following:</span></span>

    [!code-cshtml[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="36be3-133">Kód používá syntaxi `@helper` k deklaraci nové pomocné rutiny s názvem `MakeNote`.</span><span class="sxs-lookup"><span data-stu-id="36be3-133">The code uses the `@helper` syntax to declare a new helper named `MakeNote`.</span></span> <span data-ttu-id="36be3-134">Tato konkrétní pomocná pomoc vám umožní předat parametr s názvem `content`, který může obsahovat kombinaci textu a značky.</span><span class="sxs-lookup"><span data-stu-id="36be3-134">This particular helper lets you pass a parameter named `content` that can contain a combination of text and markup.</span></span> <span data-ttu-id="36be3-135">Pomocník vloží řetězec do těla poznámky pomocí proměnné `@content`.</span><span class="sxs-lookup"><span data-stu-id="36be3-135">The helper inserts the string into the note body using the `@content` variable.</span></span>

    <span data-ttu-id="36be3-136">Všimněte si, že soubor má název *MyHelpers. cshtml*, ale pomocník má název `MakeNote`.</span><span class="sxs-lookup"><span data-stu-id="36be3-136">Notice that the file is named *MyHelpers.cshtml*, but the helper is named `MakeNote`.</span></span> <span data-ttu-id="36be3-137">Do jednoho souboru můžete vložit několik vlastních pomocníků.</span><span class="sxs-lookup"><span data-stu-id="36be3-137">You can put multiple custom helpers into a single file.</span></span>
4. <span data-ttu-id="36be3-138">Uložte soubor a zavřete ho.</span><span class="sxs-lookup"><span data-stu-id="36be3-138">Save and close the file.</span></span>

## <a name="using-the-helper-in-a-page"></a><span data-ttu-id="36be3-139">Použití pomocné rutiny na stránce</span><span class="sxs-lookup"><span data-stu-id="36be3-139">Using the Helper in a Page</span></span>

1. <span data-ttu-id="36be3-140">V kořenové složce vytvořte nový prázdný soubor s názvem *TestHelper. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="36be3-140">In the root folder, create a new blank file called *TestHelper.cshtml*.</span></span>
2. <span data-ttu-id="36be3-141">Do souboru přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="36be3-141">Add the following code to the file:</span></span>

    [!code-html[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample2.html)]

    <span data-ttu-id="36be3-142">Pokud chcete zavolat pomoc, kterou jste vytvořili, použijte `@` následovaný názvem souboru, kde je pomoc, tečka a pak název pomocné rutiny.</span><span class="sxs-lookup"><span data-stu-id="36be3-142">To call the helper you created, use `@` followed by the file name where the helper is, a dot, and then the helper name.</span></span> <span data-ttu-id="36be3-143">(Pokud jste měli ve složce *App\_Code* více složek, můžete použít syntaxi `@FolderName.FileName.HelperName` k volání pomocné rutiny v rámci libovolné vnořené úrovně složky).</span><span class="sxs-lookup"><span data-stu-id="36be3-143">(If you had multiple folders in the *App\_Code* folder, you could use the syntax `@FolderName.FileName.HelperName` to call your helper within any nested folder level).</span></span> <span data-ttu-id="36be3-144">Text, který přidáte do uvozovek v závorkách, je text, který pomocníka zobrazí jako součást poznámky na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="36be3-144">The text that you add in quotation marks within the parentheses is the text that the helper will display as part of the note in the web page.</span></span>
3. <span data-ttu-id="36be3-145">Uložte stránku a spusťte ji v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="36be3-145">Save the page and run it in a browser.</span></span> <span data-ttu-id="36be3-146">Pomocná položka poznámky vygeneruje přímo tam, kde jste volali pomoc: mezi dvěma odstavci.</span><span class="sxs-lookup"><span data-stu-id="36be3-146">The helper generates the note item right where you called the helper: between the two paragraphs.</span></span>

    ![Snímek obrazovky se stránkou v prohlížeči a způsob, jakým pomocník vygeneroval značku, která umístí kolem zadaného textu rámeček.](creating-and-using-a-helper-in-an-aspnet-web-pages-site/_static/image1.png)

## <a name="additional-resources"></a><span data-ttu-id="36be3-148">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="36be3-148">Additional Resources</span></span>

<span data-ttu-id="36be3-149">[Horizontální nabídka jako pomocníka Razor](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341)</span><span class="sxs-lookup"><span data-stu-id="36be3-149">[Horizontal menu as a Razor helper](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341).</span></span> <span data-ttu-id="36be3-150">Tento záznam blogu pomocí Jan Pope ukazuje, jak vytvořit horizontální nabídku jako pomoc pomocí značek, šablon stylů CSS a kódu.</span><span class="sxs-lookup"><span data-stu-id="36be3-150">This blog entry by Mike Pope shows how to create a horizontal menu as a helper using markup, CSS, and code.</span></span>

<span data-ttu-id="36be3-151">[Využití HTML5 v ASP.NET pomocníkech pro webové stránky pro WebMatrix a ASP.NET MvC3](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx).</span><span class="sxs-lookup"><span data-stu-id="36be3-151">[Leveraging HTML5 in ASP.NET Web Pages Helpers for WebMatrix and ASP.NET MVC3](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx).</span></span> <span data-ttu-id="36be3-152">Tento záznam blogu pomocí Sam Abraham ukazuje pomoc, která vykresluje element HTML5 `Canvas`.</span><span class="sxs-lookup"><span data-stu-id="36be3-152">This blog entry by Sam Abraham shows a helper that renders an HTML5 `Canvas` element.</span></span>

<span data-ttu-id="36be3-153">[Rozdíl mezi @Helpers a @Functions ve WebMatrixu](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix).</span><span class="sxs-lookup"><span data-stu-id="36be3-153">[The Difference Between @Helpers and @Functions in WebMatrix](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix).</span></span> <span data-ttu-id="36be3-154">Tento záznam blogu pomocí Jan slaného popisu popisuje `@helper` syntaxi syntaxe a `@function` a kdy je použít.</span><span class="sxs-lookup"><span data-stu-id="36be3-154">This blog entry by Mike Brind describes `@helper` syntax and `@function` syntax and when to use each.</span></span>

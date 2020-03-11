---
uid: mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
title: Přehled zobrazení ASP.NET MVC (VB) | Microsoft Docs
author: StephenWalther
description: Co je zobrazení ASP.NET MVC a jak se liší od stránky HTML? V tomto kurzu Stephen Walther představuje zobrazení a ukazuje, jak můžete t...
ms.author: riande
ms.date: 02/16/2008
ms.assetid: c28ba88d-3a93-47f5-a306-049bd766714d
msc.legacyurl: /mvc/overview/older-versions-1/views/asp-net-mvc-views-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: f02728ed248f29b09d654e509977ed43889cbb83
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541305"
---
# <a name="aspnet-mvc-views-overview-vb"></a><span data-ttu-id="22411-104">ASP.NET MVC – přehled zobrazení (VB)</span><span class="sxs-lookup"><span data-stu-id="22411-104">ASP.NET MVC Views Overview (VB)</span></span>

<span data-ttu-id="22411-105">od [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="22411-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="22411-106">Co je zobrazení ASP.NET MVC a jak se liší od stránky HTML?</span><span class="sxs-lookup"><span data-stu-id="22411-106">What is an ASP.NET MVC View and how does it differ from a HTML page?</span></span> <span data-ttu-id="22411-107">V tomto kurzu vám Stephen Walther představuje zobrazení a ukazuje, jak můžete využít výhod zobrazení dat a pomocníků HTML v rámci zobrazení.</span><span class="sxs-lookup"><span data-stu-id="22411-107">In this tutorial, Stephen Walther introduces you to Views and demonstrates how you can take advantage of View Data and HTML Helpers within a View.</span></span>

<span data-ttu-id="22411-108">Účelem tohoto kurzu je poskytnout stručný úvod do ASP.NETch zobrazení MVC, zobrazit data a pomocníky HTML.</span><span class="sxs-lookup"><span data-stu-id="22411-108">The purpose of this tutorial is to provide you with a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="22411-109">Na konci tohoto kurzu byste měli pochopit, jak vytvářet nová zobrazení, předávat data z kontroleru do zobrazení a používat pomocníky HTML pro generování obsahu v zobrazení.</span><span class="sxs-lookup"><span data-stu-id="22411-109">By the end of this tutorial, you should understand how to create new views, pass data from a controller to a view, and use HTML Helpers to generate content in a view.</span></span>

## <a name="understanding-views"></a><span data-ttu-id="22411-110">Porozumění zobrazením</span><span class="sxs-lookup"><span data-stu-id="22411-110">Understanding Views</span></span>

<span data-ttu-id="22411-111">Na rozdíl od ASP.NET nebo Active Server stránek nezahrnuje ASP.NET MVC cokoli, co přímo odpovídá stránce.</span><span class="sxs-lookup"><span data-stu-id="22411-111">Unlike ASP.NET or Active Server Pages, ASP.NET MVC does not include anything that directly corresponds to a page.</span></span> <span data-ttu-id="22411-112">V aplikaci ASP.NET MVC není na disku žádná stránka, která by odpovídala cestě v adrese URL, kterou zadáte do panelu Adresa v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="22411-112">In an ASP.NET MVC application, there is not a page on disk that corresponds to the path in the URL that you type into the address bar of your browser.</span></span> <span data-ttu-id="22411-113">Nejbližší věc stránky v aplikaci ASP.NET MVC se říká *zobrazení*.</span><span class="sxs-lookup"><span data-stu-id="22411-113">The closest thing to a page in an ASP.NET MVC application is something called a *view*.</span></span>

<span data-ttu-id="22411-114">V aplikaci ASP.NET MVC jsou příchozí požadavky prohlížeče namapovány na akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="22411-114">In an ASP.NET MVC application, incoming browser requests are mapped to controller actions.</span></span> <span data-ttu-id="22411-115">Akce kontroleru může vrátit zobrazení.</span><span class="sxs-lookup"><span data-stu-id="22411-115">A controller action might return a view.</span></span> <span data-ttu-id="22411-116">Akce kontroleru ale může provést nějaký jiný typ akce, například přesměrování na jinou akci kontroleru.</span><span class="sxs-lookup"><span data-stu-id="22411-116">However, a controller action might perform some other type of action such as redirecting you to another controller action.</span></span>

<span data-ttu-id="22411-117">Výpis 1 obsahuje jednoduchý řadič s názvem HomeController.</span><span class="sxs-lookup"><span data-stu-id="22411-117">Listing 1 contains a simple controller named the HomeController.</span></span> <span data-ttu-id="22411-118">HomeController zpřístupňuje dvě akce kontroleru s názvem index () a podrobnosti ().</span><span class="sxs-lookup"><span data-stu-id="22411-118">The HomeController exposes two controller actions named Index() and Details().</span></span>

<span data-ttu-id="22411-119">**Výpis 1 – HomeController. vb**</span><span class="sxs-lookup"><span data-stu-id="22411-119">**Listing 1 - HomeController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample1.vb)]

<span data-ttu-id="22411-120">Můžete vyvolat první akci, akci index () zadáním následující adresy URL do adresního řádku prohlížeče:</span><span class="sxs-lookup"><span data-stu-id="22411-120">You can invoke the first action, the Index() action, by typing the following URL into your browser address bar:</span></span>

<span data-ttu-id="22411-121">/Home/Index</span><span class="sxs-lookup"><span data-stu-id="22411-121">/Home/Index</span></span>

<span data-ttu-id="22411-122">Druhou akci, akci podrobnosti () můžete vyvolat tak, že do svého prohlížeče zadáte tuto adresu:</span><span class="sxs-lookup"><span data-stu-id="22411-122">You can invoke the second action, the Details() action, by typing this address into your browser:</span></span>

<span data-ttu-id="22411-123">/Home/Details</span><span class="sxs-lookup"><span data-stu-id="22411-123">/Home/Details</span></span>

<span data-ttu-id="22411-124">Akce index () vrátí zobrazení.</span><span class="sxs-lookup"><span data-stu-id="22411-124">The Index() action returns a view.</span></span> <span data-ttu-id="22411-125">Většina akcí, které vytvoříte, budou vracet zobrazení.</span><span class="sxs-lookup"><span data-stu-id="22411-125">Most actions that you create will return views.</span></span> <span data-ttu-id="22411-126">Akce však může vracet jiné typy výsledků akce.</span><span class="sxs-lookup"><span data-stu-id="22411-126">However, an action can return other types of action results.</span></span> <span data-ttu-id="22411-127">Například akce podrobnosti () vrátí RedirectToActionResult, který přesměruje příchozí požadavek do akce index ().</span><span class="sxs-lookup"><span data-stu-id="22411-127">For example, the Details() action returns a RedirectToActionResult that redirects incoming request to the Index() action.</span></span>

<span data-ttu-id="22411-128">Akce index () obsahuje následující jeden řádek kódu:</span><span class="sxs-lookup"><span data-stu-id="22411-128">The Index() action contains the following single line of code:</span></span>

<span data-ttu-id="22411-129">Zobrazit ()</span><span class="sxs-lookup"><span data-stu-id="22411-129">View()</span></span>

<span data-ttu-id="22411-130">Tento řádek kódu vrátí zobrazení, které se musí nacházet na následujícím umístění na webovém serveru:</span><span class="sxs-lookup"><span data-stu-id="22411-130">This line of code returns a view that must be located at the following path on your web server:</span></span>

<span data-ttu-id="22411-131">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="22411-131">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="22411-132">Cesta k zobrazení je odvozena z názvu kontroleru a názvu akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="22411-132">The path to the view is inferred from the name of the controller and the name of the controller action.</span></span>

<span data-ttu-id="22411-133">Pokud budete chtít, můžete být pro zobrazení explicitní.</span><span class="sxs-lookup"><span data-stu-id="22411-133">If you prefer, you can be explicit about the view.</span></span> <span data-ttu-id="22411-134">Následující řádek kódu vrátí zobrazení s názvem Fred:</span><span class="sxs-lookup"><span data-stu-id="22411-134">The following line of code returns a view named Fred :</span></span>

<span data-ttu-id="22411-135">Zobrazení (Fred)</span><span class="sxs-lookup"><span data-stu-id="22411-135">View( Fred )</span></span>

<span data-ttu-id="22411-136">Při spuštění tohoto řádku kódu se vrátí zobrazení z následující cesty:</span><span class="sxs-lookup"><span data-stu-id="22411-136">When this line of code is executed, a view is returned from the following path:</span></span>

<span data-ttu-id="22411-137">\Views\Home\Fred.aspx</span><span class="sxs-lookup"><span data-stu-id="22411-137">\Views\Home\Fred.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="22411-138">Pokud máte v úmyslu vytvořit testy jednotek pro aplikaci ASP.NET MVC, je vhodné, abyste měli explicitní informace o názvech zobrazení.</span><span class="sxs-lookup"><span data-stu-id="22411-138">If you plan to create unit tests for your ASP.NET MVC application then it is a good idea to be explicit about view names.</span></span> <span data-ttu-id="22411-139">Tímto způsobem můžete vytvořit testování částí a ověřit tak, že se očekávané zobrazení vrátilo pomocí akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="22411-139">That way, you can create a unit test to verify that the expected view was returned by a controller action.</span></span>

## <a name="adding-content-to-a-view"></a><span data-ttu-id="22411-140">Přidání obsahu do zobrazení</span><span class="sxs-lookup"><span data-stu-id="22411-140">Adding Content to a View</span></span>

<span data-ttu-id="22411-141">Zobrazení je standardní dokument HTML (X) HTML, který může obsahovat skripty.</span><span class="sxs-lookup"><span data-stu-id="22411-141">A view is a standard (X)HTML document that can contain scripts.</span></span> <span data-ttu-id="22411-142">Pomocí skriptů můžete přidat dynamický obsah do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="22411-142">You use scripts to add dynamic content to a view.</span></span>

<span data-ttu-id="22411-143">Například zobrazení v seznamu 2 zobrazí aktuální datum a čas.</span><span class="sxs-lookup"><span data-stu-id="22411-143">For example, the view in Listing 2 displays the current date and time.</span></span>

<span data-ttu-id="22411-144">**Výpis 2 – \Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="22411-144">**Listing 2 - \Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample2.aspx)]

<span data-ttu-id="22411-145">Všimněte si, že tělo stránky HTML v seznamu 2 obsahuje následující skript:</span><span class="sxs-lookup"><span data-stu-id="22411-145">Notice that the body of the HTML page in Listing 2 contains the following script:</span></span>

<span data-ttu-id="22411-146">&lt;% Response. Write (DateTime. Now)%&gt;</span><span class="sxs-lookup"><span data-stu-id="22411-146">&lt;% Response.Write(DateTime.Now)%&gt;</span></span>

<span data-ttu-id="22411-147">Pomocí oddělovačů skriptů &lt;% a%&gt; označíte začátek a konec skriptu.</span><span class="sxs-lookup"><span data-stu-id="22411-147">You use the script delimiters &lt;% and %&gt; to mark the beginning and end of a script.</span></span> <span data-ttu-id="22411-148">Tento skript je napsán v jazyce Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="22411-148">This script is written in Visual basic.</span></span> <span data-ttu-id="22411-149">Zobrazí aktuální datum a čas voláním metody Response. Write () pro vykreslení obsahu do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="22411-149">It displays the current date and time by calling the Response.Write() method to render content to the browser.</span></span> <span data-ttu-id="22411-150">Oddělovače skriptů &lt;% a%&gt; lze použít ke spuštění jednoho nebo více příkazů.</span><span class="sxs-lookup"><span data-stu-id="22411-150">The script delimiters &lt;% and %&gt; can be used to execute one or more statements.</span></span>

<span data-ttu-id="22411-151">Vzhledem k tomu, že zavoláte Response. Write () tak často, společnost Microsoft poskytuje zástupce pro volání metody Response. Write ().</span><span class="sxs-lookup"><span data-stu-id="22411-151">Since you call Response.Write() so often, Microsoft provides you with a shortcut for calling the Response.Write() method.</span></span> <span data-ttu-id="22411-152">Zobrazení v seznamu 3 používá oddělovače &lt;% = a%&gt; jako zástupce pro volání metody Response. Write ().</span><span class="sxs-lookup"><span data-stu-id="22411-152">The view in Listing 3 uses the delimiters &lt;%= and %&gt; as a shortcut for calling Response.Write().</span></span>

<span data-ttu-id="22411-153">**Výpis 3 – Views\Home\Index2.aspx**</span><span class="sxs-lookup"><span data-stu-id="22411-153">**Listing 3 - Views\Home\Index2.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample3.aspx)]

<span data-ttu-id="22411-154">K vygenerování dynamického obsahu v zobrazení můžete použít libovolný jazyk rozhraní .NET.</span><span class="sxs-lookup"><span data-stu-id="22411-154">You can use any .NET language to generate dynamic content in a view.</span></span> <span data-ttu-id="22411-155">Za normálních okolností můžete použít buď Visual Basic .NET C# , nebo můžete zapisovat řadiče a zobrazení.</span><span class="sxs-lookup"><span data-stu-id="22411-155">Normally, you�ll use either Visual Basic .NET or C# to write your controllers and views.</span></span>

## <a name="using-html-helpers-to-generate-view-content"></a><span data-ttu-id="22411-156">Použití pomocníků HTML ke generování obsahu zobrazení</span><span class="sxs-lookup"><span data-stu-id="22411-156">Using HTML Helpers to Generate View Content</span></span>

<span data-ttu-id="22411-157">Aby bylo snazší přidávat obsah do zobrazení, můžete využít něco jako *pomocníka HTML*.</span><span class="sxs-lookup"><span data-stu-id="22411-157">To make it easier to add content to a view, you can take advantage of something called an *HTML Helper*.</span></span> <span data-ttu-id="22411-158">Pomocný objekt HTML je obvykle metoda, která generuje řetězec.</span><span class="sxs-lookup"><span data-stu-id="22411-158">An HTML Helper, typically, is a method that generates a string.</span></span> <span data-ttu-id="22411-159">Můžete použít pomocníky HTML k vygenerování standardních HTML prvků, jako jsou textová pole, odkazy, rozevírací seznamy a seznam polí.</span><span class="sxs-lookup"><span data-stu-id="22411-159">You can use HTML Helpers to generate standard HTML elements such as textboxes, links, dropdown lists, and list boxes.</span></span>

<span data-ttu-id="22411-160">Například zobrazení v seznamu 4 využívá tři pomocníky HTML – BeginForm (), textové pole () a heslo () – pro vygenerování přihlašovacího formuláře (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="22411-160">For example, the view in Listing 4 takes advantage of three HTML Helpers -- the BeginForm(), the TextBox() and Password() helpers -- to generate a Login form (see Figure 1).</span></span>

<span data-ttu-id="22411-161">**Výpis 4 – \Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="22411-161">**Listing 4 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample4.aspx)]

<span data-ttu-id="22411-162">[![dialogového okna Nový projekt](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="22411-162">[![The New Project dialog box](asp-net-mvc-views-overview-vb/_static/image1.jpg)](asp-net-mvc-views-overview-vb/_static/image1.png)</span></span>

<span data-ttu-id="22411-163">**Obrázek 01**: standardní přihlašovací formulář ([kliknutím zobrazíte obrázek v plné velikosti](asp-net-mvc-views-overview-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="22411-163">**Figure 01**: A standard Login form ([Click to view full-size image](asp-net-mvc-views-overview-vb/_static/image2.png))</span></span>

<span data-ttu-id="22411-164">Všechny metody pomocníka HTML jsou volány ve vlastnosti HTML zobrazení.</span><span class="sxs-lookup"><span data-stu-id="22411-164">All of the HTML Helpers methods are called on the Html property of the view.</span></span> <span data-ttu-id="22411-165">Například můžete vykreslit textové pole voláním metody HTML. TextBox ().</span><span class="sxs-lookup"><span data-stu-id="22411-165">For example, you render a TextBox by calling the Html.TextBox() method.</span></span>

<span data-ttu-id="22411-166">Všimněte si, že používáte oddělovače skriptů &lt;% = a%&gt; při volání pomocníků HTML. TextBox () a HTML. Password ().</span><span class="sxs-lookup"><span data-stu-id="22411-166">Notice that you use the script delimiters &lt;%= and %&gt; when calling both the Html.TextBox() and Html.Password() helpers.</span></span> <span data-ttu-id="22411-167">Tyto pomocníky jednoduše vrátí řetězec.</span><span class="sxs-lookup"><span data-stu-id="22411-167">These helpers simply return a string.</span></span> <span data-ttu-id="22411-168">Pro vykreslení řetězce do prohlížeče je nutné zavolat Response. Write ().</span><span class="sxs-lookup"><span data-stu-id="22411-168">You need to call Response.Write() in order to render the string to the browser.</span></span>

<span data-ttu-id="22411-169">Použití pomocných metod jazyka HTML je volitelné.</span><span class="sxs-lookup"><span data-stu-id="22411-169">Using HTML Helper methods is optional.</span></span> <span data-ttu-id="22411-170">Díky omezení množství HTML a skriptu, který je potřeba napsat, zjednoduší život.</span><span class="sxs-lookup"><span data-stu-id="22411-170">They make your life easier by reducing the amount of HTML and script that you need to write.</span></span> <span data-ttu-id="22411-171">Zobrazení v seznamu 5 vykreslí přesně stejný tvar jako zobrazení v seznamu 4 bez použití pomocníků HTML.</span><span class="sxs-lookup"><span data-stu-id="22411-171">The view in Listing 5 renders the exact same form as the view in Listing 4 without using HTML Helpers.</span></span>

<span data-ttu-id="22411-172">**Výpis 5 – \Views\Home\Login.aspx**</span><span class="sxs-lookup"><span data-stu-id="22411-172">**Listing 5 -- \Views\Home\Login.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample5.aspx)]

<span data-ttu-id="22411-173">Máte také možnost vytvořit si vlastní pomocníky HTML.</span><span class="sxs-lookup"><span data-stu-id="22411-173">You also have the option of creating your own HTML Helpers.</span></span> <span data-ttu-id="22411-174">Můžete například vytvořit pomocnou metodu GridView (), která zobrazí sadu záznamů databáze v tabulce HTML automaticky.</span><span class="sxs-lookup"><span data-stu-id="22411-174">For example, you can create a GridView() helper method that displays a set of database records in an HTML table automatically.</span></span> <span data-ttu-id="22411-175">Prozkoumáme toto téma v kurzu **vytváření vlastních pomocníků HTML**.</span><span class="sxs-lookup"><span data-stu-id="22411-175">We explore this topic in the tutorial **Creating Custom HTML Helpers**.</span></span>

## <a name="using-view-data-to-pass-data-to-a-view"></a><span data-ttu-id="22411-176">Použití zobrazení dat k předání dat do zobrazení</span><span class="sxs-lookup"><span data-stu-id="22411-176">Using View Data to Pass Data to a View</span></span>

<span data-ttu-id="22411-177">Pomocí zobrazení dat můžete předávat data z kontroleru do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="22411-177">You use view data to pass data from a controller to a view.</span></span> <span data-ttu-id="22411-178">Představte si zobrazení dat, jako je balíček, který odešlete prostřednictvím e-mailu.</span><span class="sxs-lookup"><span data-stu-id="22411-178">Think of view data like a package that you send through the mail.</span></span> <span data-ttu-id="22411-179">Všechna data předaná z kontroleru do zobrazení se musí odeslat pomocí tohoto balíčku.</span><span class="sxs-lookup"><span data-stu-id="22411-179">All data passed from a controller to a view must be sent using this package.</span></span> <span data-ttu-id="22411-180">Například kontroler v výpisu 6 přidá zprávu pro zobrazení dat.</span><span class="sxs-lookup"><span data-stu-id="22411-180">For example, the controller in Listing 6 adds a message to view data.</span></span>

<span data-ttu-id="22411-181">**Výpis 6 – ProductController. vb**</span><span class="sxs-lookup"><span data-stu-id="22411-181">**Listing 6 - ProductController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-views-overview-vb/samples/sample6.vb)]

<span data-ttu-id="22411-182">Vlastnost Controller ViewData představuje kolekci párů název-hodnota.</span><span class="sxs-lookup"><span data-stu-id="22411-182">The controller ViewData property represents a collection of name and value pairs.</span></span> <span data-ttu-id="22411-183">V výpisu 6 metoda index () přidá položku do kolekce zobrazení dat s názvem Zpráva s hodnotou Hello World!.</span><span class="sxs-lookup"><span data-stu-id="22411-183">In Listing 6, the Index() method adds an item to the view data collection named message with the value Hello World!.</span></span> <span data-ttu-id="22411-184">Když je zobrazení vráceno metodou index (), zobrazení dat se automaticky předává do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="22411-184">When the view is returned by the Index() method, the view data is passed to the view automatically.</span></span>

<span data-ttu-id="22411-185">Zobrazení v seznamu 7 načte zprávu z dat zobrazení a vykreslí zprávu do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="22411-185">The view in Listing 7 retrieves the message from the view data and renders the message to the browser.</span></span>

<span data-ttu-id="22411-186">**Výpis 7 – \Views\Product\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="22411-186">**Listing 7 -- \Views\Product\Index.aspx**</span></span>

[!code-aspx[Main](asp-net-mvc-views-overview-vb/samples/sample7.aspx)]

<span data-ttu-id="22411-187">Všimněte si, že zobrazení při vykreslování zprávy využívá pomocnou metodu HTML. Encode () HTML.</span><span class="sxs-lookup"><span data-stu-id="22411-187">Notice that the view takes advantage of the Html.Encode() HTML Helper method when rendering the message.</span></span> <span data-ttu-id="22411-188">Pomocný kód HTML. Encode () HTML kóduje speciální znaky, například &lt; a &gt; do znaků, které jsou bezpečné pro zobrazení na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="22411-188">The Html.Encode() HTML Helper encodes special characters such as &lt; and &gt; into characters that are safe to display in a web page.</span></span> <span data-ttu-id="22411-189">Kdykoli vykreslíte obsah, který uživatel odešle na web, měli byste zakódovat obsah a zabránit tak útokům prostřednictvím injektáže JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="22411-189">Whenever you render content that a user submits to a website, you should encode the content to prevent JavaScript injection attacks.</span></span>

<span data-ttu-id="22411-190">(Vzhledem k tomu, že jsme v ProductController vytvořili zprávu dodržovali, nemusíme ji opravdu kódovat.</span><span class="sxs-lookup"><span data-stu-id="22411-190">(Because we created the message ourselves in the ProductController, we don�t really need to encode the message.</span></span> <span data-ttu-id="22411-191">Je však dobrým zvykem při zobrazování obsahu načteného z zobrazení dat načtených v zobrazení, vždy při volání metody HTML. Encode ().)</span><span class="sxs-lookup"><span data-stu-id="22411-191">However, it is a good habit to always call the Html.Encode() method when displaying content retrieved from view data within a view.)</span></span>

<span data-ttu-id="22411-192">V seznamu 7 jsme využili výhod zobrazení dat k předání jednoduché zprávy řetězce z řadiče do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="22411-192">In Listing 7, we took advantage of view data to pass a simple string message from a controller to a view.</span></span> <span data-ttu-id="22411-193">Pomocí zobrazení dat můžete také předat další typy dat, jako je například kolekce záznamů databáze, z kontroleru do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="22411-193">You also can use view data to pass other types of data, such as a collection of database records, from a controller to a view.</span></span> <span data-ttu-id="22411-194">Například pokud chcete zobrazit obsah tabulky databáze produktů v zobrazení, pak byste měli předat kolekci záznamů databáze v zobrazení dat.</span><span class="sxs-lookup"><span data-stu-id="22411-194">For example, if you want to display the contents of the Products database table in a view, then you would pass the collection of database records in view data.</span></span>

<span data-ttu-id="22411-195">Máte také možnost předat data zobrazení silného typu z kontroleru do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="22411-195">You also have the option of passing strongly typed view data from a controller to a view.</span></span> <span data-ttu-id="22411-196">Toto téma se zabývá v kurzu, který popisuje **zobrazení dat a zobrazení silného typu**.</span><span class="sxs-lookup"><span data-stu-id="22411-196">We explore this topic in the tutorial **Understanding Strongly Typed View Data and Views**.</span></span>

## <a name="summary"></a><span data-ttu-id="22411-197">Souhrn</span><span class="sxs-lookup"><span data-stu-id="22411-197">Summary</span></span>

<span data-ttu-id="22411-198">V tomto kurzu najdete stručný úvod k ASP.NET zobrazením MVC, zobrazení dat a pomocníkům HTML.</span><span class="sxs-lookup"><span data-stu-id="22411-198">This tutorial provided a brief introduction to ASP.NET MVC views, view data, and HTML Helpers.</span></span> <span data-ttu-id="22411-199">V první části jste se dozvěděli, jak přidat nová zobrazení do projektu.</span><span class="sxs-lookup"><span data-stu-id="22411-199">In the first section, you learned how to add new views to your project.</span></span> <span data-ttu-id="22411-200">Zjistili jste, že musíte přidat zobrazení do pravé složky, abyste ho mohli zavolat z konkrétního kontroleru.</span><span class="sxs-lookup"><span data-stu-id="22411-200">You learned that you must add a view to the right folder in order to call it from a particular controller.</span></span> <span data-ttu-id="22411-201">Dále jsme probrali téma nápovědy HTML.</span><span class="sxs-lookup"><span data-stu-id="22411-201">Next, we discussed the topic of HTML Helpers.</span></span> <span data-ttu-id="22411-202">Zjistili jste, jak vám pomocník HTML umožňuje snadno vygenerovat standardní obsah HTML.</span><span class="sxs-lookup"><span data-stu-id="22411-202">You learned how HTML Helpers enable you to easily generate standard HTML content.</span></span> <span data-ttu-id="22411-203">Nakonec jste zjistili, jak využít výhod zobrazení dat k předávání dat z kontroleru do zobrazení.</span><span class="sxs-lookup"><span data-stu-id="22411-203">Finally, you learned how to take advantage of view data to pass data from a controller to a view.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="22411-204">[Předchozí](passing-data-to-view-master-pages-cs.md)
> [Další](creating-custom-html-helpers-vb.md)</span><span class="sxs-lookup"><span data-stu-id="22411-204">[Previous](passing-data-to-view-master-pages-cs.md)
[Next](creating-custom-html-helpers-vb.md)</span></span>

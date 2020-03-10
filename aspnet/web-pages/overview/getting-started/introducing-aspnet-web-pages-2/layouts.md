---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
title: Představení webových stránek ASP.NET – vytvoření konzistentního rozložení | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se dozvíte, jak pomocí rozložení vytvořit konzistentní vzhled stránek na webu, který používá webové stránky ASP.NET. Předpokládá se, že jste dokončili...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: c85ec591-f8d7-4882-b763-de6ab9f3df7a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
msc.type: authoredcontent
ms.openlocfilehash: 678eb7089e95e3d221d6b2d82034a62aefa75757
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526689"
---
# <a name="introducing-aspnet-web-pages---creating-a-consistent-layout"></a><span data-ttu-id="a8dbe-104">Představení webových stránek ASP.NET – vytvoření konzistentního rozložení</span><span class="sxs-lookup"><span data-stu-id="a8dbe-104">Introducing ASP.NET Web Pages - Creating a Consistent Layout</span></span>

<span data-ttu-id="a8dbe-105">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="a8dbe-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="a8dbe-106">V tomto kurzu se dozvíte, jak pomocí *rozložení* vytvořit konzistentní vzhled stránek na webu, který používá webové stránky ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-106">This tutorial shows you how to use *layouts* to create a consistent look for the pages on a site that uses ASP.NET Web Pages.</span></span> <span data-ttu-id="a8dbe-107">Předpokládá, že jste dokončili řadu [odstraněním dat databáze na webových stránkách ASP.NET](https://go.microsoft.com/fwlink/?LinkId=251584).</span><span class="sxs-lookup"><span data-stu-id="a8dbe-107">It assumes you have completed the series through [Deleting Database Data in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251584).</span></span>
> 
> <span data-ttu-id="a8dbe-108">Naučíte se:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="a8dbe-109">Stránka rozložení.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-109">What a layout page is.</span></span>
> - <span data-ttu-id="a8dbe-110">Jak kombinovat stránky rozložení s dynamickým obsahem.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-110">How to combine layout pages with dynamic content.</span></span>
> - <span data-ttu-id="a8dbe-111">Jak předat hodnoty na stránku rozložení.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-111">How to pass values to a layout page.</span></span>

## <a name="about-layouts"></a><span data-ttu-id="a8dbe-112">O rozloženích</span><span class="sxs-lookup"><span data-stu-id="a8dbe-112">About Layouts</span></span>

<span data-ttu-id="a8dbe-113">Všechny stránky, které jste doposud vytvořili, mají kompletní, samostatné stránky.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-113">The pages you've created so far have all been complete, standalone pages.</span></span> <span data-ttu-id="a8dbe-114">Všechny patří do stejné lokality, ale nemají žádné společné prvky ani standardní vzhled.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-114">They all belong to the same site, but they don't have any common elements or a standard look.</span></span>

<span data-ttu-id="a8dbe-115">Většina lokalit má konzistentní vzhled a rozložení.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-115">Most sites do have a consistent look and layout.</span></span> <span data-ttu-id="a8dbe-116">Například pokud přejdete na web [Microsoft.com/web](https://www.microsoft.com/web/) a vyhledáte, uvidíte, že stránky všechny odpovídají celkovému rozložení a vizuálnímu motivu:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-116">For example, if you go to the [Microsoft.com/web](https://www.microsoft.com/web/) site and look around, you see that the pages all adhere to an overall layout and to a visual theme:</span></span>

![Stránka Microsoft.com/web webu zobrazující rozložení záhlaví, navigační oblasti, oblasti obsahu a zápatí](layouts/_static/image1.png)

<span data-ttu-id="a8dbe-118">*Neefektivní* způsob, jak vytvořit toto rozložení, by bylo definovat záhlaví, navigační panel a zápatí samostatně na každé stránce.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-118">An *inefficient* way to create this layout would be to define a header, navigation bar, and footer separately on each of your pages.</span></span> <span data-ttu-id="a8dbe-119">Pokaždé, když budete chtít stejný kód duplikovat.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-119">You'd be duplicating the same markup each time.</span></span> <span data-ttu-id="a8dbe-120">Pokud jste chtěli něco změnit (například aktualizovat zápatí), budete muset každou stránku změnit samostatně.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-120">If you wanted to change something (for example, update the footer), you'd have to change each page separately.</span></span>

<span data-ttu-id="a8dbe-121">To je místo, kde jsou *stránky rozložení* součástí.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-121">That's where *layout pages* come in.</span></span> <span data-ttu-id="a8dbe-122">Na webových stránkách ASP.NET můžete definovat stránku rozložení, která poskytuje celkový kontejner pro stránky na webu.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-122">In ASP.NET Web Pages, you can define a layout page that provides an overall container for pages on your site.</span></span> <span data-ttu-id="a8dbe-123">Stránka rozložení může například obsahovat záhlaví, navigační oblast a zápatí.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-123">For example, the layout page can contain the header, navigation area, and footer.</span></span> <span data-ttu-id="a8dbe-124">Stránka rozložení obsahuje zástupný symbol, kde se přechází hlavní obsah.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-124">The layout page includes a placeholder where the main content goes.</span></span>

<span data-ttu-id="a8dbe-125">Pak můžete definovat jednotlivé stránky obsahu, které obsahují značky a kód pouze pro tuto stránku.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-125">You can then define individual content pages that contain the markup and the code for only that page.</span></span> <span data-ttu-id="a8dbe-126">Stránky obsahu nemusí být kompletní stránky HTML. nemusejí mít ani `<body>` element.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-126">Content pages don't have to be complete HTML pages; they don't even have to have a `<body>` element.</span></span> <span data-ttu-id="a8dbe-127">Mají také řádek kódu, který oznamuje ASP.NET, na které stránce rozložení chcete zobrazit obsah.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-127">They also have a line of code that tells ASP.NET what layout page you want to display the content in.</span></span> <span data-ttu-id="a8dbe-128">Tady je obrázek, který ukazuje, jak tento vztah funguje:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-128">Here's a picture that shows roughly how this relationship works:</span></span>

![Koncepční diagram, který zobrazuje dvě stránky obsahu a stránku rozložení, na které se vejdou](layouts/_static/image2.png)

<span data-ttu-id="a8dbe-130">Tato interakce je snadno srozumitelná, když ji vidíte v akci.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-130">This interaction is easy to understand when you see it in action.</span></span> <span data-ttu-id="a8dbe-131">V tomto kurzu změníte stránky filmů na použití rozložení.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-131">In this tutorial, you'll change your movies pages to use a layout.</span></span>

## <a name="adding-a-layout-page"></a><span data-ttu-id="a8dbe-132">Přidání stránky rozložení</span><span class="sxs-lookup"><span data-stu-id="a8dbe-132">Adding a Layout Page</span></span>

<span data-ttu-id="a8dbe-133">Začnete vytvořením stránky rozložení, která definuje typické rozložení stránky pomocí záhlaví, zápatí a oblasti pro hlavní obsah.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-133">You'll start by creating a layout page that defines a typical page layout with a header, footer, and an area for the main content.</span></span> <span data-ttu-id="a8dbe-134">Na webu WebPagesMovies přidejte stránku CSHTML s názvem *\_layout. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-134">In the WebPagesMovies site, add a CSHTML page named *\_Layout.cshtml*.</span></span>

<span data-ttu-id="a8dbe-135">Úvodní znak podtržítka (`_`) je významný.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-135">The leading underscore ( `_` ) character is significant.</span></span> <span data-ttu-id="a8dbe-136">Pokud název stránky začíná podtržítkem, ASP.NET nebude přímo odesílat tuto stránku do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-136">If a page's name starts with an underscore, ASP.NET won't directly send that page to the browser.</span></span> <span data-ttu-id="a8dbe-137">Tato konvence vám umožní definovat stránky, které jsou pro vaši lokalitu nutné, ale uživatelé by nemuseli žádat o přímý přístup.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-137">This convention lets you define pages that are required for your site but that users shouldn't be able to request directly.</span></span>

<span data-ttu-id="a8dbe-138">Obsah stránky nahraďte následujícím:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-138">Replace the content in the page with the following:</span></span>

[!code-html[Main](layouts/samples/sample1.html)]

<span data-ttu-id="a8dbe-139">Jak vidíte, tento kód je pouze HTML, který používá `<div>` prvky pro definování tří částí na stránce a další `<div>` elementu pro uložení tří částí.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-139">As you can see, this markup is just HTML that uses `<div>` elements to define three sections in the page plus one more `<div>` element to hold the three sections.</span></span> <span data-ttu-id="a8dbe-140">Zápatí obsahuje bitovou kopii kódu Razor: `@DateTime.Now.Year`, který vykreslí aktuální rok v tomto umístění stránky.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-140">The footer contains a bit of Razor code: `@DateTime.Now.Year`, which will render the current year at that location in the page.</span></span>

<span data-ttu-id="a8dbe-141">Všimněte si, že existuje odkaz na šablonu stylů s názvem *video. CSS*.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-141">Notice that there's a link to a style sheet named *Movies.css*.</span></span> <span data-ttu-id="a8dbe-142">Šablona stylů je místo, kde budou definovány podrobnosti fyzického rozložení prvků.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-142">The style sheet is where the details of the physical layout of the elements will be defined.</span></span> <span data-ttu-id="a8dbe-143">Vytvoříte to za chvíli.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-143">You'll create that in a moment.</span></span>

<span data-ttu-id="a8dbe-144">Jedinou neobvyklou funkcí na této stránce *\_layout. cshtml* je `@Render.Body()` čára.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-144">The only unusual feature in this *\_Layout.cshtml* page is the `@Render.Body()` line.</span></span> <span data-ttu-id="a8dbe-145">To je zástupný symbol, kde bude obsah přecházet, když je toto rozložení sloučeno s jinou stránkou.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-145">That's the placeholder where the content will go when this layout is merged with another page.</span></span>

## <a name="adding-a-css-file"></a><span data-ttu-id="a8dbe-146">Přidání souboru. CSS</span><span class="sxs-lookup"><span data-stu-id="a8dbe-146">Adding a .css File</span></span>

<span data-ttu-id="a8dbe-147">Upřednostňovaným způsobem, jak definovat skutečné uspořádání (to znamená, vzhled) prvků na stránce, je použití pravidel kaskádových šablon stylů (CSS).</span><span class="sxs-lookup"><span data-stu-id="a8dbe-147">The preferred way to define the actual arrangement (that is, appearance) of elements on the page is to use cascading style sheet (CSS) rules.</span></span> <span data-ttu-id="a8dbe-148">Proto vytvoříte soubor *. CSS* , který obsahuje pravidla pro nové rozložení.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-148">So you'll create a *.css* file that has the rules for your new layout.</span></span>

<span data-ttu-id="a8dbe-149">V části WebMatrix vyberte kořen webu.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-149">In WebMatrix, select the root of your site.</span></span> <span data-ttu-id="a8dbe-150">Pak na kartě **soubory** na pásu karet klikněte na šipku pod tlačítkem **Nový** a pak klikněte na **Nová složka**.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-150">Then in the **Files** tab of the ribbon, click the arrow under the **New** button and then click **New Folder**.</span></span>

![Možnost Nová složka v části nový na pásu karet.](layouts/_static/image3.png)

<span data-ttu-id="a8dbe-152">Pojmenujte nové *styly*složek.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-152">Name the new folder *Styles*.</span></span>

![Pojmenování nové složky ' Styles '](layouts/_static/image4.png)

<span data-ttu-id="a8dbe-154">Uvnitř nové složky *stylů* vytvořte soubor s názvem *filmovés. CSS*.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-154">Inside the new *Styles* folder, create a file named *Movies.css*.</span></span>

![Vytváření nového souboru filmů. CSS](layouts/_static/image5.png)

<span data-ttu-id="a8dbe-156">Nahraďte obsah nového souboru *. CSS* následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-156">Replace the contents of the new *.css* file with the following:</span></span>

[!code-css[Main](layouts/samples/sample2.css)]

<span data-ttu-id="a8dbe-157">V těchto pravidlech šablon stylů CSS nebudeme počítat s výjimkou dvou věcí.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-157">We won't say much about these CSS rules, except to note two things.</span></span> <span data-ttu-id="a8dbe-158">Jedním z nich je, že kromě nastavení písem a velikostí používají pravidla absolutní umístění k určení umístění záhlaví, zápatí a oblasti hlavního obsahu.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-158">One is that in addition to setting fonts and sizes, the rules use absolute positioning to establish the location of the header, footer, and main content area.</span></span> <span data-ttu-id="a8dbe-159">Pokud se chystáte umístění v šablonách stylů CSS, můžete si přečíst kurz pro [umístění šablon stylů CSS](http://www.w3schools.com/css/css_positioning.asp) na webu w3schools.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-159">If you're new to positioning in CSS, you can read the [CSS Positioning](http://www.w3schools.com/css/css_positioning.asp) tutorial at the W3Schools site.</span></span>

<span data-ttu-id="a8dbe-160">Druhá Poznámka je, že v dolní části jsme zkopírovali pravidla stylů, která byla původně definována v souboru *Movies. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="a8dbe-160">The other thing to note is that at the bottom, we've copied the style rules that were originally defined individually in the *Movies.cshtml* file.</span></span> <span data-ttu-id="a8dbe-161">Tato pravidla se použila v [úvodu k zobrazení dat pomocí ASP.NET na webové stránky](https://go.microsoft.com/fwlink/?LinkId=251580) , aby pomocné rutiny `WebGrid` vykreslily značky, které přidaly do tabulky pruhy.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-161">These rules were used in the [Introduction to Displaying Data by Using ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251580) tutorial to make the `WebGrid` helper render markup that added stripes to the table.</span></span> <span data-ttu-id="a8dbe-162">(Pokud budete používat soubor *. CSS* pro definice stylu, můžete také zadat pravidla stylu pro celou lokalitu v tomto umístění.)</span><span class="sxs-lookup"><span data-stu-id="a8dbe-162">(If you're going to use a *.css* file for style definitions, you might as well put the style rules for the whole site in it.)</span></span>

## <a name="updating-the-movies-file-to-use-the-layout"></a><span data-ttu-id="a8dbe-163">Aktualizace souboru filmů pro použití rozložení</span><span class="sxs-lookup"><span data-stu-id="a8dbe-163">Updating the Movies File to Use the Layout</span></span>

<span data-ttu-id="a8dbe-164">Nyní můžete aktualizovat existující soubory na webu, aby používaly nové rozložení.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-164">Now you can update the existing files in your site to use the new layout.</span></span> <span data-ttu-id="a8dbe-165">Otevřete soubor *Movies. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="a8dbe-165">Open the *Movies.cshtml* file.</span></span> <span data-ttu-id="a8dbe-166">V horní části, jako první řádek kódu, přidejte následující:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-166">At the top, as the first line of code, add the following:</span></span>

[!code-csharp[Main](layouts/samples/sample3.cs)]

<span data-ttu-id="a8dbe-167">Stránka teď začíná tímto způsobem:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-167">The page now starts out this way:</span></span>

[!code-cshtml[Main](layouts/samples/sample4.cshtml?highlight=2)]

<span data-ttu-id="a8dbe-168">Tento jeden řádek kódu oznamuje ASP.NET, že když se stránka *videa* spustí, měla by se sloučit se souborem *\_layout. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="a8dbe-168">This one line of code tells ASP.NET that when the *Movies* page runs, it should be merged with the *\_Layout.cshtml* file.</span></span>

<span data-ttu-id="a8dbe-169">Vzhledem k tomu, že soubor *Movies. cshtml* nyní používá stránku rozložení, můžete odebrat značku ze stránky *filmy. cshtml* , která je pořízena souborem *\_layout. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="a8dbe-169">Since the *Movies.cshtml* file now uses a layout page, you can remove the markup from the *Movies.cshtml* page that's taken care of by the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="a8dbe-170">`<!DOCTYPE>`, `<html>`a `<body>` otevírání a zavírání značek.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-170">Take out the `<!DOCTYPE>`, `<html>`, and `<body>` opening and closing tags.</span></span> <span data-ttu-id="a8dbe-171">Odbrat celý `<head>` prvek a jeho obsah, který obsahuje pravidla stylu pro mřížku, protože tato pravidla teď máte v souboru *. CSS* .</span><span class="sxs-lookup"><span data-stu-id="a8dbe-171">Take out the entire `<head>` element and its contents, which includes the style rules for the grid, since you've now got those rules in a *.css* file.</span></span> <span data-ttu-id="a8dbe-172">I když jste na něm, změňte existující `<h1>` element na `<h2>` element; na stránce rozložení již existuje prvek `<h1>`.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-172">While you're at it, change the existing `<h1>` element to an `<h2>` element; you have an `<h1>` element in the layout page already.</span></span> <span data-ttu-id="a8dbe-173">Změňte `<h2>` text na "vypsat filmy".</span><span class="sxs-lookup"><span data-stu-id="a8dbe-173">Change the `<h2>` text to "List Movies".</span></span>

<span data-ttu-id="a8dbe-174">Obvykle byste nemuseli tyto změny na stránce obsahu provádět.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-174">Normally you wouldn't have to make these sorts of changes in a content page.</span></span> <span data-ttu-id="a8dbe-175">Když zahájíte stránku s rozložením, vytvoříte stránky obsahu bez všech těchto prvků, které mají začít.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-175">When you start your site out with a layout page, you create content pages without all these elements to begin with.</span></span> <span data-ttu-id="a8dbe-176">V takovém případě však převádíte samostatnou stránku na jednu, která používá rozložení, takže existuje bit vyčištění.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-176">In this case, though, you're converting a standalone page to one that uses a layout, so there's a bit of cleanup.</span></span>

<span data-ttu-id="a8dbe-177">Až budete hotovi, stránka *filmy. cshtml* bude vypadat následovně:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-177">When you're finished, the *Movies.cshtml* page will look like the following:</span></span>

[!code-cshtml[Main](layouts/samples/sample5.cshtml)]

### <a name="testing-the-layout"></a><span data-ttu-id="a8dbe-178">Testování rozložení</span><span class="sxs-lookup"><span data-stu-id="a8dbe-178">Testing the Layout</span></span>

<span data-ttu-id="a8dbe-179">Nyní vidíte, jak vypadá rozložení.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-179">Now you can see what the layout looks like.</span></span> <span data-ttu-id="a8dbe-180">Ve WebMatrixu klikněte pravým tlačítkem na stránku *filmy. cshtml* a vyberte **Spustit v prohlížeči**.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-180">In WebMatrix, right-click the *Movies.cshtml* page and select **Launch in browser**.</span></span> <span data-ttu-id="a8dbe-181">Když prohlížeč stránku zobrazí, vypadá to jako tato stránka:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-181">When the browser displays the page, it looks like this page:</span></span>

![Stránka filmy vykreslená pomocí rozložení](layouts/_static/image6.png)

<span data-ttu-id="a8dbe-183">ASP.NET sloučil obsah stránky video. cshtml na stránku *\_layout. cshtml* , kde je `RenderBody` metoda.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-183">ASP.NET has merged the content of the Movies.cshtml page into the *\_Layout.cshtml* page right where the `RenderBody` method is.</span></span> <span data-ttu-id="a8dbe-184">A samozřejmě stránku *\_layout. cshtml* odkazuje na soubor *. CSS* , který definuje vzhled stránky.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-184">And of course the *\_Layout.cshtml* page references a *.css* file that defines the look of the page.</span></span>

## <a name="updating-the-addmovie-page-to-use-the-layout"></a><span data-ttu-id="a8dbe-185">Aktualizace stránky AddMovie pro použití rozložení</span><span class="sxs-lookup"><span data-stu-id="a8dbe-185">Updating the AddMovie Page to Use the Layout</span></span>

<span data-ttu-id="a8dbe-186">Výhodou pro výhody rozvržení je, že je můžete použít pro všechny stránky na webu.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-186">The real benefit of layouts is that you can use them for all the pages in your site.</span></span> <span data-ttu-id="a8dbe-187">Otevřete stránku *AddMovie. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="a8dbe-187">Open the *AddMovie.cshtml* page.</span></span>

<span data-ttu-id="a8dbe-188">Můžete si uvědomit, že na stránce *AddMovie. cshtml* byla původně některá pravidla šablon stylů CSS, aby bylo možné definovat vzhled chybových zpráv ověřování.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-188">You might remember that the *AddMovie.cshtml* page originally had some CSS rules in it to define the look of validation error messages.</span></span> <span data-ttu-id="a8dbe-189">Vzhledem k tomu, že máte soubor *. CSS* pro váš web nyní, můžete tato pravidla přesunout do souboru *. CSS* .</span><span class="sxs-lookup"><span data-stu-id="a8dbe-189">Since you have a *.css* file for your site now, you can move those rules to the *.css* file.</span></span> <span data-ttu-id="a8dbe-190">Odeberte je ze souboru *AddMovie. cshtml* a přidejte je do dolní části souboru *Movies. CSS* .</span><span class="sxs-lookup"><span data-stu-id="a8dbe-190">Remove them from the *AddMovie.cshtml* file and add them to the bottom of the *Movies.css* file.</span></span> <span data-ttu-id="a8dbe-191">Přesouváte následující pravidla:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-191">You are moving the following rules:</span></span>

[!code-css[Main](layouts/samples/sample6.css)]

<span data-ttu-id="a8dbe-192">Nyní proveďte stejné řazení změn v *AddMovie. cshtml* , které jste provedli pro *filmy. cshtml* – přidejte `Layout="~/_Layout.cshtml;` a odeberte kód HTML, který je nyní cizí.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-192">Now make the same sorts of changes in *AddMovie.cshtml* that you did for *Movies.cshtml* — add `Layout="~/_Layout.cshtml;` and remove the HTML markup that's now extraneous.</span></span> <span data-ttu-id="a8dbe-193">Změňte `<h1>` element na `<h2>`.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-193">Change the `<h1>` element to `<h2>`.</span></span> <span data-ttu-id="a8dbe-194">Až budete hotovi, stránka bude vypadat jako v tomto příkladu:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-194">When you're done, the page will look like this example:</span></span>

[!code-cshtml[Main](layouts/samples/sample7.cshtml)]

<span data-ttu-id="a8dbe-195">Spusťte stránku.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-195">Run the page.</span></span> <span data-ttu-id="a8dbe-196">Nyní vypadá jako na tomto obrázku:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-196">Now it looks like this illustration:</span></span>

![Stránka Přidat filmy vykreslená pomocí rozložení](layouts/_static/image7.png)

<span data-ttu-id="a8dbe-198">Chcete provést podobné změny na stránkách v lokalitě – *EditMovie. cshtml* a *DeleteMovie. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-198">You want to make similar changes to the pages in the site — *EditMovie.cshtml* and *DeleteMovie.cshtml*.</span></span> <span data-ttu-id="a8dbe-199">Než však provedete, můžete provést další změnu rozložení, které je trochu flexibilnější.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-199">However, before you do, you can make another change to the layout that makes it a little more flexible.</span></span>

## <a name="passing-title-information-to-the-layout-page"></a><span data-ttu-id="a8dbe-200">Předávání informací o názvu na stránku rozložení</span><span class="sxs-lookup"><span data-stu-id="a8dbe-200">Passing Title Information to the Layout Page</span></span>

<span data-ttu-id="a8dbe-201">Stránka *\_layout. cshtml* , kterou jste vytvořili, má `<title>` element, který je nastaven na "moji filmový web".</span><span class="sxs-lookup"><span data-stu-id="a8dbe-201">The *\_Layout.cshtml* page that you created has a `<title>` element that's set to "My Movie Site".</span></span> <span data-ttu-id="a8dbe-202">Většina prohlížečů zobrazuje obsah tohoto prvku jako text na kartě:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-202">Most browsers display the content of this element as the text on a tab:</span></span>

![Element &lt;title&gt; stránky zobrazený na kartě prohlížeče](layouts/_static/image8.png)

<span data-ttu-id="a8dbe-204">Tyto informace o názvu jsou obecné.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-204">This title information is generic.</span></span> <span data-ttu-id="a8dbe-205">Řekněme, že chcete, aby byl text nadpisu pro aktuální stránku konkrétnější.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-205">Suppose that you want the title text to be more specific to the current page.</span></span> <span data-ttu-id="a8dbe-206">(Text nadpisu se používá také vyhledávacími weby k určení toho, co stránka se chystá.) Můžete předat informace ze stránky obsahu, jako je například *filmy. cshtml* nebo *AddMovie. cshtml* , na stránku rozložení a pak tyto informace použít k přizpůsobení toho, co stránka rozložení vykreslí.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-206">(The title text is also used by search engines to determine what your page is about.) You can pass information from a content page like *Movies.cshtml* or *AddMovie.cshtml* to the layout page, and then use that information to customize what the layout page renders.</span></span>

<span data-ttu-id="a8dbe-207">Otevřete znovu stránku *filmy. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="a8dbe-207">Open the *Movies.cshtml* page again.</span></span> <span data-ttu-id="a8dbe-208">V kódu nahoře přidejte následující řádek:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-208">In the code at the top, add the following line:</span></span>

[!code-csharp[Main](layouts/samples/sample8.cs)]

<span data-ttu-id="a8dbe-209">Objekt `Page` je k dispozici na všech stránkách *. cshtml* a je pro tento účel, totiž pro sdílení informací mezi stránkou a jejím rozložením.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-209">The `Page` object is available on all *.cshtml* pages and is for this purpose, namely to share information between a page and its layout.</span></span>

<span data-ttu-id="a8dbe-210">Otevřete stránku *\_layout. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="a8dbe-210">Open the *\_Layout.cshtml* page.</span></span> <span data-ttu-id="a8dbe-211">Změňte element `<title>` tak, aby vypadal jako tento kód:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-211">Change the `<title>` element so that it looks like this markup:</span></span>

[!code-html[Main](layouts/samples/sample9.html)]

<span data-ttu-id="a8dbe-212">Tento kód vykresluje bez ohledu na to, zda je vlastnost `Page.Title` v daném umístění stránky.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-212">This code renders whatever is in the `Page.Title` property right at that location in the page.</span></span>

<span data-ttu-id="a8dbe-213">Spusťte stránku *filmy. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="a8dbe-213">Run the *Movies.cshtml* page.</span></span> <span data-ttu-id="a8dbe-214">Tentokrát karta prohlížeč zobrazuje, co jste předali jako hodnotu `Page.Title`:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-214">This time the browser tab shows what you passed as the value of `Page.Title`:</span></span>

![Karta prohlížeče zobrazující nadpis, který se vytvořil dynamicky](layouts/_static/image9.png)

<span data-ttu-id="a8dbe-216">Pokud chcete, zobrazte zdroj stránky v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-216">If you want, view the page source in the browser.</span></span> <span data-ttu-id="a8dbe-217">Můžete vidět, že `<title>` element je vykreslen jako `<title>List Movies</title>`.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-217">You can see that the `<title>` element is rendered as `<title>List Movies</title>`.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="a8dbe-218">**Objekt Page**</span><span class="sxs-lookup"><span data-stu-id="a8dbe-218">**The Page Object**</span></span>
> 
> <span data-ttu-id="a8dbe-219">Užitečnou funkcí `Page` je, že se jedná o dynamický objekt – vlastnost `Title` není pevným ani rezervovaným názvem.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-219">A useful feature of `Page` is that it's a dynamic object — the `Title` property is not a fixed or reserved name.</span></span> <span data-ttu-id="a8dbe-220">Pro hodnotu objektu `Page` můžete použít *libovolný* název.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-220">You can use *any* name for a value of the `Page` object.</span></span> <span data-ttu-id="a8dbe-221">Například můžete snadno předat název pomocí vlastnosti s názvem `Page.CurrentName` nebo `Page.MyPage`.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-221">For example, you could as easily have passed the title by using a property named `Page.CurrentName` or `Page.MyPage`.</span></span> <span data-ttu-id="a8dbe-222">Jediným omezením je, že název musí dodržovat běžná pravidla pro to, které vlastnosti mohou být pojmenovány.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-222">The only restriction is that the name has to follow the normal rules for what properties can be named.</span></span> <span data-ttu-id="a8dbe-223">(Například název nesmí obsahovat mezeru.)</span><span class="sxs-lookup"><span data-stu-id="a8dbe-223">(For example, the name can't contain a space.)</span></span>
> 
> <span data-ttu-id="a8dbe-224">Můžete předat libovolný počet hodnot pomocí objektu `Page`.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-224">You can pass any number of values by using the `Page` object.</span></span> <span data-ttu-id="a8dbe-225">Pokud jste chtěli předat informace o videu na stránku rozložení, mohli byste předat hodnoty pomocí typu `Page.MovieTitle` a `Page.Genre` a `Page.MovieYear`.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-225">If you wanted to pass movie information to the layout page, you could pass values by using something like `Page.MovieTitle` and `Page.Genre` and `Page.MovieYear`.</span></span> <span data-ttu-id="a8dbe-226">(Nebo jiné názvy, které jste vymysleli k ukládání informací.) Jediným požadavkem, který je pravděpodobně zřejmý – je, že je nutné použít stejné názvy na stránce obsahu a na stránce rozložení.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-226">(Or any other names that you invented to store the information.) The only requirement — which is probably obvious — is that you have to use the same names in the content page and the layout page.</span></span>
> 
> <span data-ttu-id="a8dbe-227">Informace, které předáte pomocí objektu `Page`, nejsou omezeny pouze na text, který se má zobrazit na stránce rozložení.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-227">The information you pass by using the `Page` object isn't limited to just text to display on the layout page.</span></span> <span data-ttu-id="a8dbe-228">Můžete předat hodnotu stránce rozložení a potom kód na stránce rozložení může použít hodnotu k rozhodnutí, zda se má zobrazit sekce stránky, co soubor *. CSS* , který má být použit, a tak dále.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-228">You can pass a value to the layout page, and then code in the layout page can use the value to decide whether to display a section of the page, what *.css* file to use, and so on.</span></span> <span data-ttu-id="a8dbe-229">Hodnoty, které předáte do objektu `Page`, jsou stejně jako jakékoli jiné hodnoty, které používáte v kódu.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-229">The values you pass in the `Page` object are like any other values that you use in code.</span></span> <span data-ttu-id="a8dbe-230">Je pouze to, že hodnoty pocházejí ze stránky obsahu a jsou předány na stránku rozložení.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-230">It's just that the values originate in the content page and are passed to the layout page.</span></span>

<span data-ttu-id="a8dbe-231">Otevřete stránku *AddMovie. cshtml* a přidejte řádek na začátek kódu, který poskytuje název stránky *AddMovie. cshtml* :</span><span class="sxs-lookup"><span data-stu-id="a8dbe-231">Open the *AddMovie.cshtml* page and add a line to the top of the code that provides a title for the *AddMovie.cshtml* page:</span></span>

[!code-csharp[Main](layouts/samples/sample10.cs)]

<span data-ttu-id="a8dbe-232">Spusťte stránku *AddMovie. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="a8dbe-232">Run the *AddMovie.cshtml* page.</span></span> <span data-ttu-id="a8dbe-233">Tady vidíte nový název:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-233">You see the new title there:</span></span>

![Karta prohlížeče zobrazující, že se název přidat filmy vytvořil dynamicky](layouts/_static/image10.png)

## <a name="updating-the-remaining-pages-to-use-the-layout"></a><span data-ttu-id="a8dbe-235">Aktualizace zbývajících stránek na používání rozložení</span><span class="sxs-lookup"><span data-stu-id="a8dbe-235">Updating the Remaining Pages to Use the Layout</span></span>

<span data-ttu-id="a8dbe-236">Nyní můžete zbývající stránky na webu dokončit tak, aby používaly nové rozložení.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-236">Now you can finish the remaining pages in your site so that they use the new layout.</span></span> <span data-ttu-id="a8dbe-237">Otevřete *EditMovie. cshtml* a *DeleteMovie. cshtml* a udělejte v nich stejné změny.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-237">Open *EditMovie.cshtml* and *DeleteMovie.cshtml* in turn and make the same changes in each.</span></span>

<span data-ttu-id="a8dbe-238">Přidejte řádek kódu, který odkazuje na stránku rozložení:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-238">Add the line of code that links to the layout page:</span></span>

[!code-csharp[Main](layouts/samples/sample11.cs)]

<span data-ttu-id="a8dbe-239">Přidejte řádek pro nastavení názvu stránky:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-239">Add a line to set the title of the page:</span></span>

[!code-csharp[Main](layouts/samples/sample12.cs)]

<span data-ttu-id="a8dbe-240">nebo:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-240">or:</span></span>

[!code-csharp[Main](layouts/samples/sample13.cs)]

<span data-ttu-id="a8dbe-241">Odebrat všechny nadbytečné značky HTML – v podstatě ponechte pouze bity, které jsou uvnitř elementu `<body>` (plus blok kódu v horní části).</span><span class="sxs-lookup"><span data-stu-id="a8dbe-241">Remove all the extraneous HTML markup — basically, leave only the bits that are inside the `<body>` element (plus the code block at the top).</span></span>

<span data-ttu-id="a8dbe-242">Změňte `<h1>` element tak, aby byl `<h2>` element.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-242">Change the `<h1>` element to be an `<h2>` element.</span></span>

<span data-ttu-id="a8dbe-243">Jakmile provedete tyto změny, otestujte je a ujistěte se, že se zobrazují správně a že je název správný.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-243">When you've made these changes, test each and make sure that it's displaying properly and that the title is correct.</span></span>

## <a name="parting-thoughts-about-layout-pages"></a><span data-ttu-id="a8dbe-244">Rozmístění nápadů na stránky rozložení</span><span class="sxs-lookup"><span data-stu-id="a8dbe-244">Parting Thoughts About Layout Pages</span></span>

<span data-ttu-id="a8dbe-245">V tomto kurzu jste vytvořili stránku *\_layout. cshtml* a pomocí metody `RenderBody` sloučíte obsah z jiné stránky.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-245">In this tutorial you created a *\_Layout.cshtml* page and used the `RenderBody` method to merge content from another page.</span></span> <span data-ttu-id="a8dbe-246">To je základní model pro použití rozložení na webových stránkách.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-246">That's the basic pattern for using layouts in Web Pages.</span></span>

<span data-ttu-id="a8dbe-247">Stránky rozložení mají další funkce, které tady nepokrýváme.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-247">Layout pages have additional features that we didn't cover here.</span></span> <span data-ttu-id="a8dbe-248">Můžete například vnořovat stránky rozložení – jedna stránka rozložení může odkazovat na další.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-248">For example, you can nest layout pages — one layout page can in turn reference another.</span></span> <span data-ttu-id="a8dbe-249">Vnořená rozložení můžou být užitečná, když pracujete s podčástmi lokality, která vyžaduje různá rozložení.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-249">Nested layouts can be useful if you're working with subsections of a site that require different layouts.</span></span> <span data-ttu-id="a8dbe-250">Můžete také použít další metody (například `RenderSection`), chcete-li nastavit pojmenované oddíly na stránce rozložení.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-250">You can also use additional methods (for example, `RenderSection`) to set up named sections in the layout page.</span></span>

<span data-ttu-id="a8dbe-251">Kombinace stránek rozložení a souborů *. CSS* je výkonné.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-251">The combination of layout pages and *.css* files is powerful.</span></span> <span data-ttu-id="a8dbe-252">Jak vidíte v další sérii kurzů, můžete v WebMatrixu vytvořit web na základě *šablony*, která vám poskytne web s předem sestavenými funkcemi.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-252">As you'll see in the next tutorial series, in WebMatrix you can create a site based on a *template*, which gives you a site that has prebuilt functionality in it.</span></span> <span data-ttu-id="a8dbe-253">Šablony usnadňují použití stránek rozložení a šablon stylů CSS k vytváření webů, které vypadají skvěle a mají funkce jako nabídky.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-253">The templates make good use of layout pages and CSS to create sites that look great and that have features like menus.</span></span> <span data-ttu-id="a8dbe-254">Tady je snímek obrazovky domovské stránky z webu založeného na šabloně, který zobrazuje funkce, které používají stránky rozložení a šablony stylů CSS:</span><span class="sxs-lookup"><span data-stu-id="a8dbe-254">Here's a screenshot of the home page from a site based on a template, showing features that use layout pages and CSS:</span></span>

![Rozložení vytvořené šablonou webu WebMatrix zobrazující záhlaví, navigační oblast, oblast obsahu, volitelný oddíl a přihlašovací odkazy](layouts/_static/image11.png)

## <a name="complete-listing-for-movie-page-updated-to-use-a-layout-page"></a><span data-ttu-id="a8dbe-256">Úplný výpis stránky videa (aktualizovaný pro použití stránky rozložení)</span><span class="sxs-lookup"><span data-stu-id="a8dbe-256">Complete Listing for Movie Page (Updated to Use a Layout Page)</span></span>

[!code-cshtml[Main](layouts/samples/sample14.cshtml)]

## <a name="complete-page-listing-for-add-movie-page-updated-for-layout"></a><span data-ttu-id="a8dbe-257">Dokončení výpisu stránky pro stránku přidat film (Aktualizováno pro rozložení)</span><span class="sxs-lookup"><span data-stu-id="a8dbe-257">Complete Page Listing for Add Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample15.cshtml)]

## <a name="complete-page-listing-for-delete-movie-page-updated-for-layout"></a><span data-ttu-id="a8dbe-258">Dokončení výpisu stránky pro stránku odstranit film (Aktualizováno pro rozložení)</span><span class="sxs-lookup"><span data-stu-id="a8dbe-258">Complete Page Listing for Delete Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample16.cshtml)]

## <a name="complete-page-listing-for-edit-movie-page-updated-for-layout"></a><span data-ttu-id="a8dbe-259">Úplný výpis stránky pro stránku Upravit film (Aktualizováno pro rozložení)</span><span class="sxs-lookup"><span data-stu-id="a8dbe-259">Complete Page Listing for Edit Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample17.cshtml)]

## <a name="coming-up-next"></a><span data-ttu-id="a8dbe-260">Připravujeme další</span><span class="sxs-lookup"><span data-stu-id="a8dbe-260">Coming Up Next</span></span>

<span data-ttu-id="a8dbe-261">V dalším kurzu se dozvíte, jak publikovat web na Internet tak, aby ho všichni mohli vidět.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-261">In the next tutorial, you'll learn how to publish your site to the Internet so everyone can see it.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="a8dbe-262">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="a8dbe-262">Additional Resources</span></span>

- <span data-ttu-id="a8dbe-263">[Vytvoření konzistentního vzhledu](https://go.microsoft.com/fwlink/?LinkID=202891) – článek, který poskytuje další podrobnosti o práci s rozloženími.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-263">[Creating a Consistent Look](https://go.microsoft.com/fwlink/?LinkID=202891) — An article that provides some more detail on working with layouts.</span></span> <span data-ttu-id="a8dbe-264">Popisuje také, jak předat hodnotu stránce rozložení, která zobrazuje nebo skrývá část obsahu.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-264">It also describes how to pass a value to a layout page that shows or hides some of the content.</span></span>
- <span data-ttu-id="a8dbe-265">[Vnořené stránky rozložení se syntaxí Razor](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) – Jan slané Blogy příklad, jak vnořit stránky rozložení.</span><span class="sxs-lookup"><span data-stu-id="a8dbe-265">[Nested Layout Pages with Razor](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) — Mike Brind blogs an example of how to nest layout pages.</span></span> <span data-ttu-id="a8dbe-266">(Zahrnuje stažení stránek.)</span><span class="sxs-lookup"><span data-stu-id="a8dbe-266">(Includes a download of the pages.)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a8dbe-267">[Předchozí](deleting-data.md)
> [Další](publishing.md)</span><span class="sxs-lookup"><span data-stu-id="a8dbe-267">[Previous](deleting-data.md)
[Next](publishing.md)</span></span>

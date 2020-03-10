---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
title: Představení webových stránek ASP.NET-odstraňování dat databáze | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se dozvíte, jak odstranit jednotlivou položku databáze. Předpokládá, že jste dokončili řadu prostřednictvím aktualizace databázových dat v ASP.NET Web PA...
ms.author: riande
ms.date: 01/02/2018
ms.assetid: 75b5c1cf-84bd-434f-8a86-85c568eb5b09
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
msc.type: authoredcontent
ms.openlocfilehash: c8620fc1abc61d514bdc039c66f7a84e67e89abe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78629036"
---
# <a name="introducing-aspnet-web-pages---deleting-database-data"></a><span data-ttu-id="b7b00-104">Představení webových stránek ASP.NET – odstranění databázových dat</span><span class="sxs-lookup"><span data-stu-id="b7b00-104">Introducing ASP.NET Web Pages - Deleting Database Data</span></span>

<span data-ttu-id="b7b00-105">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="b7b00-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="b7b00-106">V tomto kurzu se dozvíte, jak odstranit jednotlivou položku databáze.</span><span class="sxs-lookup"><span data-stu-id="b7b00-106">This tutorial shows you how to delete an individual database entry.</span></span> <span data-ttu-id="b7b00-107">Předpokládá, že jste dokončili řadu prostřednictvím [aktualizace databázových dat ve webových stránkách ASP.NET](updating-data.md).</span><span class="sxs-lookup"><span data-stu-id="b7b00-107">It assumes you have completed the series through [Updating Database Data in ASP.NET Web Pages](updating-data.md).</span></span>
> 
> <span data-ttu-id="b7b00-108">Naučíte se:</span><span class="sxs-lookup"><span data-stu-id="b7b00-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="b7b00-109">Jak vybrat jednotlivý záznam ze seznamu záznamů.</span><span class="sxs-lookup"><span data-stu-id="b7b00-109">How to select an individual record from a listing of records.</span></span>
> - <span data-ttu-id="b7b00-110">Jak odstranit jeden záznam z databáze.</span><span class="sxs-lookup"><span data-stu-id="b7b00-110">How to delete a single record from a database.</span></span>
> - <span data-ttu-id="b7b00-111">Jak kontrolovat, zda bylo na formuláři kliknuto konkrétní tlačítko.</span><span class="sxs-lookup"><span data-stu-id="b7b00-111">How to check that a specific button was clicked in a form.</span></span>
>   
> 
> <span data-ttu-id="b7b00-112">Popsané funkce a technologie:</span><span class="sxs-lookup"><span data-stu-id="b7b00-112">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="b7b00-113">Pomocná rutina `WebGrid`</span><span class="sxs-lookup"><span data-stu-id="b7b00-113">The `WebGrid` helper.</span></span>
> - <span data-ttu-id="b7b00-114">Příkaz SQL `Delete`.</span><span class="sxs-lookup"><span data-stu-id="b7b00-114">The SQL `Delete` command.</span></span>
> - <span data-ttu-id="b7b00-115">Metoda `Database.Execute` pro spuštění příkazu SQL `Delete`</span><span class="sxs-lookup"><span data-stu-id="b7b00-115">The `Database.Execute` method to run a SQL `Delete` command.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="b7b00-116">Co sestavíte</span><span class="sxs-lookup"><span data-stu-id="b7b00-116">What You'll Build</span></span>

<span data-ttu-id="b7b00-117">V předchozím kurzu jste zjistili, jak aktualizovat existující záznam databáze.</span><span class="sxs-lookup"><span data-stu-id="b7b00-117">In the previous tutorial, you learned how to update an existing database record.</span></span> <span data-ttu-id="b7b00-118">Tento kurz je podobný, s tím rozdílem, že místo aktualizace záznamu ho odstraníte.</span><span class="sxs-lookup"><span data-stu-id="b7b00-118">This tutorial is similar, except that instead of updating the record, you'll delete it.</span></span> <span data-ttu-id="b7b00-119">Procesy jsou mnohem stejné, s výjimkou toho, že odstranění je jednodušší, takže tento kurz bude krátký.</span><span class="sxs-lookup"><span data-stu-id="b7b00-119">The processes are much the same, except that deleting is simpler, so this tutorial will be short.</span></span>

<span data-ttu-id="b7b00-120">Na stránce *filmy* aktualizujte pomocníka `WebGrid` tak, aby se zobrazil odkaz pro **odstranění** vedle každého filmu, který se doprovází pomocí odkazu pro **Úpravy** , který jste přidali dříve.</span><span class="sxs-lookup"><span data-stu-id="b7b00-120">In the *Movies* page, you'll update the `WebGrid` helper so that it displays a **Delete** link next to each movie to accompany the **Edit** link you added earlier.</span></span>

![Stránka filmy znázorňující odkaz pro odstranění každého filmu](deleting-data/_static/image1.png)

<span data-ttu-id="b7b00-122">Stejně jako u úprav můžete po kliknutí na odkaz **Odstranit** přejít na jinou stránku, kde jsou informace o filmu již ve formě:</span><span class="sxs-lookup"><span data-stu-id="b7b00-122">As with editing, when you click the **Delete** link, it takes you to a different page, where the movie information is already in a form:</span></span>

![Odstranit stránku videa se zobrazeným filmem](deleting-data/_static/image2.png)

<span data-ttu-id="b7b00-124">Potom můžete kliknutím na toto tlačítko trvale odstranit záznam.</span><span class="sxs-lookup"><span data-stu-id="b7b00-124">You can then click the button to delete the record permanently.</span></span>

## <a name="adding-a-delete-link-to-the-movie-listing"></a><span data-ttu-id="b7b00-125">Přidání odkazu pro odstranění na seznam filmů</span><span class="sxs-lookup"><span data-stu-id="b7b00-125">Adding a Delete Link to the Movie Listing</span></span>

<span data-ttu-id="b7b00-126">Začnete přidáním odkazu pro **odstranění** do pomocné rutiny `WebGrid`.</span><span class="sxs-lookup"><span data-stu-id="b7b00-126">You'll start by adding a **Delete** link to the `WebGrid` helper.</span></span> <span data-ttu-id="b7b00-127">Tento odkaz je podobný odkazu pro **Úpravy** , který jste přidali v předchozím kurzu.</span><span class="sxs-lookup"><span data-stu-id="b7b00-127">This link is similar to the **Edit** link you added in a previous tutorial.</span></span>

<span data-ttu-id="b7b00-128">Otevřete soubor *Movies. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="b7b00-128">Open the *Movies.cshtml* file.</span></span>

<span data-ttu-id="b7b00-129">Změňte `WebGrid` označení v těle stránky přidáním sloupce.</span><span class="sxs-lookup"><span data-stu-id="b7b00-129">Change the `WebGrid` markup in the body of the page by adding a column.</span></span> <span data-ttu-id="b7b00-130">Zde je upravený kód:</span><span class="sxs-lookup"><span data-stu-id="b7b00-130">Here's the modified markup:</span></span>

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

<span data-ttu-id="b7b00-131">Nový sloupec je tento:</span><span class="sxs-lookup"><span data-stu-id="b7b00-131">The new column is this one:</span></span>

[!code-html[Main](deleting-data/samples/sample2.html)]

<span data-ttu-id="b7b00-132">Způsob, jakým je mřížka nakonfigurována, je sloupec pro **Úpravy** v mřížce umístěn nejvíce vlevo a sloupec pro **odstranění** je umístěn nejvíce vpravo.</span><span class="sxs-lookup"><span data-stu-id="b7b00-132">The way the grid is configured, the **Edit** column is leftmost in the grid and the **Delete** column is rightmost.</span></span> <span data-ttu-id="b7b00-133">(Pro případ, že jste si nevšimli, je teď za `Year` sloupce čárka.) Neexistují žádné speciální informace o tom, kde tyto sloupce odkazů přecházejí, a můžete je tak snadno umístit vedle sebe.</span><span class="sxs-lookup"><span data-stu-id="b7b00-133">(There's a comma after the `Year` column now, in case you didn't notice that.) There's nothing special about where these link columns go, and you could as easily put them next to each other.</span></span> <span data-ttu-id="b7b00-134">V takovém případě jsou oddělené, aby byly těžší v kombinaci.</span><span class="sxs-lookup"><span data-stu-id="b7b00-134">In this case, they're separate to make them harder to get mixed up.</span></span>

![Stránka filmy s odkazy upravit a podrobnosti označují, že nejsou vedle sebe navzájem.](deleting-data/_static/image3.png)

<span data-ttu-id="b7b00-136">Nový sloupec zobrazuje odkaz (`<a>` element), jehož text říká "Delete".</span><span class="sxs-lookup"><span data-stu-id="b7b00-136">The new column shows a link (`<a>` element) whose text says "Delete".</span></span> <span data-ttu-id="b7b00-137">Cíl odkazu (jeho `href` atribut) je kód, který se nakonec překládá na něco podobného jako tato adresa URL, přičemž `id` hodnota se u každého filmu liší:</span><span class="sxs-lookup"><span data-stu-id="b7b00-137">The target of the link (its `href` attribute) is code that ultimately resolves to something like this URL, with the `id` value different for each movie:</span></span>

[!code-css[Main](deleting-data/samples/sample3.css)]

<span data-ttu-id="b7b00-138">Tento odkaz vyvolá stránku s názvem *DeleteMovie* a předá jí ID vybraného filmu.</span><span class="sxs-lookup"><span data-stu-id="b7b00-138">This link will invoke a page named *DeleteMovie* and pass it the ID of the movie you've selected.</span></span>

<span data-ttu-id="b7b00-139">Tento kurz nepřejde do podrobností o tom, jak je tento odkaz vytvořený, protože je skoro totožný s odkazem na **Úpravy** z předchozího kurzu ([aktualizace dat databáze na webových stránkách ASP.NET](updating-data.md)).</span><span class="sxs-lookup"><span data-stu-id="b7b00-139">This tutorial won't go into detail about how this link is constructed, because it's almost identical to the **Edit** link from the previous tutorial ([Updating Database Data in ASP.NET Web Pages](updating-data.md)).</span></span>

## <a name="creating-the-delete-page"></a><span data-ttu-id="b7b00-140">Vytvoření stránky pro odstranění</span><span class="sxs-lookup"><span data-stu-id="b7b00-140">Creating the Delete Page</span></span>

<span data-ttu-id="b7b00-141">Nyní můžete vytvořit stránku, která bude cílem pro odkaz **Delete** v mřížce.</span><span class="sxs-lookup"><span data-stu-id="b7b00-141">Now you can create the page that will be the target for the **Delete** link in the grid.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="b7b00-142">**Důležité** informace Technika prvního výběru záznamu, který se má odstranit, a následného použití samostatné stránky a tlačítka k potvrzení, že proces je mimořádně důležitý pro zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="b7b00-142">**Important** The technique of first selecting a record to delete and then using a separate page and button to confirm the process is extremely important for security.</span></span> <span data-ttu-id="b7b00-143">Jak jste si přečetli v předchozích kurzech, je nutné, aby *jakýkoli* druh změny webu byl *vždy* proveden pomocí &mdash; formuláře, který používá operaci http post.</span><span class="sxs-lookup"><span data-stu-id="b7b00-143">As you've read in previous tutorials, making *any* sort of change to your website should *always* be done using a form &mdash; that is, using an HTTP POST operation.</span></span> <span data-ttu-id="b7b00-144">Pokud jste provedli změnu webu pouhým kliknutím na odkaz (tj. pomocí operace GET), můžou lidé na vašem webu provádět jednoduché požadavky a odstraňovat vaše data.</span><span class="sxs-lookup"><span data-stu-id="b7b00-144">If you made it possible to change the site just by clicking a link (that is, using a GET operation), people could make simple requests to your site and delete your data.</span></span> <span data-ttu-id="b7b00-145">I prohledávací modul, který indexuje web, může omylem odstranit data pouze pomocí následujících odkazů.</span><span class="sxs-lookup"><span data-stu-id="b7b00-145">Even a search-engine crawler that's indexing your site could inadvertently delete data just by following links.</span></span>
> 
> <span data-ttu-id="b7b00-146">Když vaše aplikace umožňuje uživatelům změnit záznam, je nutné k tomu připrezentovat záznam uživateli pro úpravy.</span><span class="sxs-lookup"><span data-stu-id="b7b00-146">When your app lets people change a record, you have to present the record to the user for editing anyway.</span></span> <span data-ttu-id="b7b00-147">Ale můžete se rozhodnout, že tento krok vynecháte pro odstranění záznamu.</span><span class="sxs-lookup"><span data-stu-id="b7b00-147">But you might be tempted to skip this step for deleting a record.</span></span> <span data-ttu-id="b7b00-148">Tento krok přeskočte, ale.</span><span class="sxs-lookup"><span data-stu-id="b7b00-148">Don't skip that step, though.</span></span> <span data-ttu-id="b7b00-149">(Je také užitečné, když uživatelé uvidí záznam a potvrdí, že odstraňují záznam, který zamýšlel.)</span><span class="sxs-lookup"><span data-stu-id="b7b00-149">(It's also helpful for users to see the record and confirm that they're deleting the record that they intended.)</span></span>
> 
> <span data-ttu-id="b7b00-150">V další sadě kurzů se dozvíte, jak přidat funkce přihlášení, aby se uživatel musel před odstraněním záznamu přihlásit.</span><span class="sxs-lookup"><span data-stu-id="b7b00-150">In a subsequent tutorial set, you'll see how to add login functionality so a user would have to log in before deleting a record.</span></span>

<span data-ttu-id="b7b00-151">Vytvořte stránku s názvem *DeleteMovie. cshtml* a nahraďte obsah souboru následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="b7b00-151">Create a page named *DeleteMovie.cshtml* and replace what's in the file with the following markup:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

<span data-ttu-id="b7b00-152">Tento kód je podobný jako *EditMovie* stránky s tím rozdílem, že místo použití textových polí (`<input type="text">`) obsahuje značka `<span>` prvky.</span><span class="sxs-lookup"><span data-stu-id="b7b00-152">This markup is like the *EditMovie* pages, except that instead of using text boxes (`<input type="text">`), the markup includes `<span>` elements.</span></span> <span data-ttu-id="b7b00-153">Tady není nic, co byste mohli upravit.</span><span class="sxs-lookup"><span data-stu-id="b7b00-153">There's nothing here to edit.</span></span> <span data-ttu-id="b7b00-154">Vše, co musíte udělat, je zobrazit podrobnosti o videu, aby se uživatelé mohli ujistit, že odstraňují správný film.</span><span class="sxs-lookup"><span data-stu-id="b7b00-154">All you have to do is display the movie details so that users can make sure that they're deleting the right movie.</span></span>

<span data-ttu-id="b7b00-155">Značka již obsahuje odkaz, který uživateli umožňuje vracet se na stránku se seznamem filmů.</span><span class="sxs-lookup"><span data-stu-id="b7b00-155">The markup already contains a link that lets the user return to the movie listing page.</span></span>

<span data-ttu-id="b7b00-156">Stejně jako na stránce *EditMovie* je ID vybraného filmu uloženo ve skrytém poli.</span><span class="sxs-lookup"><span data-stu-id="b7b00-156">As in the *EditMovie* page, the ID of the selected movie is stored in a hidden field.</span></span> <span data-ttu-id="b7b00-157">(Předává se na stránku na prvním místě jako hodnota řetězce dotazu.) `Html.ValidationSummary` volání, které zobrazí chyby ověřování.</span><span class="sxs-lookup"><span data-stu-id="b7b00-157">(It's passed into the page in the first place as a query string value.) There's an `Html.ValidationSummary` call that will display validation errors.</span></span> <span data-ttu-id="b7b00-158">V takovém případě může dojít k chybě, že se na stránku předalo žádné ID filmu nebo že ID filmu není platné.</span><span class="sxs-lookup"><span data-stu-id="b7b00-158">In this case, the error might be that no movie ID was passed to the page or that the movie ID is invalid.</span></span> <span data-ttu-id="b7b00-159">K této situaci může dojít, pokud někdo spustil tuto stránku bez předchozího výběru videa na stránce *filmy* .</span><span class="sxs-lookup"><span data-stu-id="b7b00-159">This situation could occur if someone ran this page without first selecting a movie in the *Movies* page.</span></span>

<span data-ttu-id="b7b00-160">Popisek tlačítka je **Odstranit film**a jeho atribut Name je nastaven na `buttonDelete`.</span><span class="sxs-lookup"><span data-stu-id="b7b00-160">The button caption is **Delete Movie**, and its name attribute is set to `buttonDelete`.</span></span> <span data-ttu-id="b7b00-161">Atribut `name` bude použit v kódu k identifikaci tlačítka, které odeslalo formulář.</span><span class="sxs-lookup"><span data-stu-id="b7b00-161">The `name` attribute will be used in the code to identify the button that submitted the form.</span></span>

<span data-ttu-id="b7b00-162">Budete muset napsat kód na 1) Přečtěte si podrobnosti o videu při prvním zobrazení stránky a 2) opravdu odstranit film, když uživatel klikne na tlačítko.</span><span class="sxs-lookup"><span data-stu-id="b7b00-162">You'll have to write code to 1) read the movie details when the page is first displayed and 2) actually delete the movie when the user clicks the button.</span></span>

## <a name="adding-code-to-read-a-single-movie"></a><span data-ttu-id="b7b00-163">Přidání kódu pro čtení jednoho filmu</span><span class="sxs-lookup"><span data-stu-id="b7b00-163">Adding Code to Read a Single Movie</span></span>

<span data-ttu-id="b7b00-164">V horní části stránky *DeleteMovie. cshtml* přidejte následující blok kódu:</span><span class="sxs-lookup"><span data-stu-id="b7b00-164">At the top of the *DeleteMovie.cshtml* page, add the following code block:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

<span data-ttu-id="b7b00-165">Tento kód je stejný jako odpovídající kód na stránce *EditMovie* .</span><span class="sxs-lookup"><span data-stu-id="b7b00-165">This markup is the same as the corresponding code in the *EditMovie* page.</span></span> <span data-ttu-id="b7b00-166">Získá ID filmu z řetězce dotazu a pomocí ID přečte záznam z databáze.</span><span class="sxs-lookup"><span data-stu-id="b7b00-166">It gets the movie ID out of the query string and uses the ID to read a record from the database.</span></span> <span data-ttu-id="b7b00-167">Kód obsahuje ověřovací test (`IsInt()` a `row != null`), aby bylo zajištěno, že ID filmu, které je předáno na stránku, je platné.</span><span class="sxs-lookup"><span data-stu-id="b7b00-167">The code includes the validation test (`IsInt()` and `row != null`) to make sure that the movie ID being passed to the page is valid.</span></span>

<span data-ttu-id="b7b00-168">Mějte na paměti, že tento kód by měl být spuštěn pouze při prvním spuštění stránky.</span><span class="sxs-lookup"><span data-stu-id="b7b00-168">Remember that this code should only run the first time the page runs.</span></span> <span data-ttu-id="b7b00-169">Pokud uživatel klikne na tlačítko **Odstranit film** , nechcete znovu načíst záznam videa z databáze.</span><span class="sxs-lookup"><span data-stu-id="b7b00-169">You don't want to re-read the movie record from the database when the user clicks the **Delete Movie** button.</span></span> <span data-ttu-id="b7b00-170">Proto kód pro čtení filmu je uvnitř testu, který říká `if(!IsPost)` &mdash;, který je, *Pokud požadavek není operace post (odeslání formuláře)* .</span><span class="sxs-lookup"><span data-stu-id="b7b00-170">Therefore, code to read the movie is inside a test that says `if(!IsPost)` &mdash; that is, *if the request is not a post operation (form submission)*.</span></span>

## <a name="adding-code-to-delete-the-selected-movie"></a><span data-ttu-id="b7b00-171">Přidání kódu pro odstranění vybraného filmu</span><span class="sxs-lookup"><span data-stu-id="b7b00-171">Adding Code to Delete the Selected Movie</span></span>

<span data-ttu-id="b7b00-172">Chcete-li odstranit film, když uživatel klikne na tlačítko, přidejte následující kód těsně do uzavírací závorky bloku `@`:</span><span class="sxs-lookup"><span data-stu-id="b7b00-172">To delete the movie when the user clicks the button, add the following code just inside the closing brace of the `@` block:</span></span>

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

<span data-ttu-id="b7b00-173">Tento kód je podobný kódu pro aktualizaci existujícího záznamu, ale jednodušší.</span><span class="sxs-lookup"><span data-stu-id="b7b00-173">This code is similar to the code for updating an existing record, but simpler.</span></span> <span data-ttu-id="b7b00-174">Kód v podstatě spustí příkaz SQL `Delete`.</span><span class="sxs-lookup"><span data-stu-id="b7b00-174">The code basically runs a SQL `Delete` statement.</span></span>

 <span data-ttu-id="b7b00-175">Stejně jako na stránce *EditMovie* je kód v bloku `if(IsPost)`.</span><span class="sxs-lookup"><span data-stu-id="b7b00-175">As in the *EditMovie* page, the code is in an `if(IsPost)` block.</span></span> <span data-ttu-id="b7b00-176">Tentokrát je stav `if()` trochu složitější:</span><span class="sxs-lookup"><span data-stu-id="b7b00-176">This time, the `if()` condition is a little more complicated:</span></span> 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

<span data-ttu-id="b7b00-177">Existují dvě podmínky.</span><span class="sxs-lookup"><span data-stu-id="b7b00-177">There are two conditions here.</span></span> <span data-ttu-id="b7b00-178">První je, že se stránka posílá, protože jste viděli před &mdash; `if(IsPost)`.</span><span class="sxs-lookup"><span data-stu-id="b7b00-178">The first is that the page is being submitted, as you've seen before &mdash; `if(IsPost)`.</span></span>

<span data-ttu-id="b7b00-179">Druhá podmínka je `!Request["buttonDelete"].IsEmpty()`, což znamená, že žádost obsahuje objekt s názvem `buttonDelete`.</span><span class="sxs-lookup"><span data-stu-id="b7b00-179">The second condition is `!Request["buttonDelete"].IsEmpty()`, meaning that the request has an object named `buttonDelete`.</span></span> <span data-ttu-id="b7b00-180">V případě potřeby se jedná o nepřímý způsob testování, který tlačítko odeslalo formulář.</span><span class="sxs-lookup"><span data-stu-id="b7b00-180">Admittedly, it's an indirect way of testing which button submitted the form.</span></span> <span data-ttu-id="b7b00-181">Pokud formulář obsahuje více tlačítek pro odeslání, zobrazí se v žádosti pouze název tlačítka, které bylo kliknuto.</span><span class="sxs-lookup"><span data-stu-id="b7b00-181">If a form contains multiple submit buttons, only the name of the button that was clicked appears in the request.</span></span> <span data-ttu-id="b7b00-182">Proto logicky, pokud se název určitého tlačítka objeví v žádosti &mdash; nebo jak je uvedeno v kódu, pokud toto tlačítko není prázdné &mdash;, které je tlačítko, které formulář odeslalo.</span><span class="sxs-lookup"><span data-stu-id="b7b00-182">Therefore, logically, if the name of a particular button appears in the request &mdash; or as stated in the code, if that button isn't empty &mdash; that's the button that submitted the form.</span></span>

<span data-ttu-id="b7b00-183">Operátor `&&` znamená "a" (Logical a).</span><span class="sxs-lookup"><span data-stu-id="b7b00-183">The `&&` operator means "and" (logical AND).</span></span> <span data-ttu-id="b7b00-184">Proto je celá podmínka `if`...</span><span class="sxs-lookup"><span data-stu-id="b7b00-184">Therefore the entire `if` condition is ...</span></span>

<span data-ttu-id="b7b00-185">*Tento požadavek je post (nejedná se o první požadavek).*</span><span class="sxs-lookup"><span data-stu-id="b7b00-185">*This request is a post (not a first-time request)*</span></span>  
  
 <span data-ttu-id="b7b00-186">AND</span><span class="sxs-lookup"><span data-stu-id="b7b00-186">AND</span></span>  
  
<span data-ttu-id="b7b00-187">Tlačítko `buttonDelete`*bylo tlačítko, které odeslalo formulář.*</span><span class="sxs-lookup"><span data-stu-id="b7b00-187">*The* `buttonDelete`*button was the button that submitted the form.*</span></span>

<span data-ttu-id="b7b00-188">Tento formulář (ve skutečnosti tuto stránku) obsahuje jenom jedno tlačítko, takže další test pro `buttonDelete` není technicky nutný.</span><span class="sxs-lookup"><span data-stu-id="b7b00-188">This form (in fact, this page) contains only one button, so the additional test for `buttonDelete` is technically not required.</span></span> <span data-ttu-id="b7b00-189">Pořád se chystáte provést operaci, která bude trvale odebírat data.</span><span class="sxs-lookup"><span data-stu-id="b7b00-189">Still, you're about to perform an operation that will permanently remove data.</span></span> <span data-ttu-id="b7b00-190">Proto chcete mít jistotu, že provádíte operaci pouze v případě, že ji uživatel výslovně požadoval.</span><span class="sxs-lookup"><span data-stu-id="b7b00-190">So you want to be as sure as possible that you're performing the operation only when the user has explicitly requested it.</span></span> <span data-ttu-id="b7b00-191">Předpokládejme například, že později jste tuto stránku rozšířili a přidali do ní další tlačítka.</span><span class="sxs-lookup"><span data-stu-id="b7b00-191">For example, suppose that you expanded this page later and added other buttons to it.</span></span> <span data-ttu-id="b7b00-192">Dokonce i kód, který odstraní film, bude spuštěn pouze v případě, že bylo kliknuto na tlačítko `buttonDelete`.</span><span class="sxs-lookup"><span data-stu-id="b7b00-192">Even then, the code that deletes the movie will run only if the `buttonDelete` button was clicked.</span></span>

<span data-ttu-id="b7b00-193">Stejně jako na stránce *EditMovie* získáte ID z skrytého pole a pak spustíte příkaz SQL.</span><span class="sxs-lookup"><span data-stu-id="b7b00-193">As in the *EditMovie* page, you get the ID from the hidden field and then run the SQL command.</span></span> <span data-ttu-id="b7b00-194">Syntaxe příkazu `Delete` je:</span><span class="sxs-lookup"><span data-stu-id="b7b00-194">The syntax for the `Delete` statement is:</span></span>

`DELETE FROM table WHERE ID = value`

<span data-ttu-id="b7b00-195">Je důležité zahrnout klauzuli `WHERE` a ID.</span><span class="sxs-lookup"><span data-stu-id="b7b00-195">It's vital to include the `WHERE` clause and the ID.</span></span> <span data-ttu-id="b7b00-196">Pokud ponecháte klauzuli WHERE, *odstraní se všechny záznamy v tabulce*.</span><span class="sxs-lookup"><span data-stu-id="b7b00-196">If you leave out the WHERE clause, *all the records in the table will be deleted*.</span></span> <span data-ttu-id="b7b00-197">Jak jste viděli, předáte hodnotu ID příkazu SQL pomocí zástupného symbolu.</span><span class="sxs-lookup"><span data-stu-id="b7b00-197">As you have seen, you pass the ID value to the SQL command by using a placeholder.</span></span>

## <a name="testing-the-movie-delete-process"></a><span data-ttu-id="b7b00-198">Testování procesu odstranění filmu</span><span class="sxs-lookup"><span data-stu-id="b7b00-198">Testing the Movie Delete Process</span></span>

<span data-ttu-id="b7b00-199">Nyní můžete provést test.</span><span class="sxs-lookup"><span data-stu-id="b7b00-199">Now you can test.</span></span> <span data-ttu-id="b7b00-200">Spusťte stránku *filmy* a klikněte na tlačítko **Odstranit** vedle videa.</span><span class="sxs-lookup"><span data-stu-id="b7b00-200">Run the *Movies* page, and click **Delete** next to a movie.</span></span> <span data-ttu-id="b7b00-201">Po zobrazení stránky *DeleteMovie* klikněte na **Odstranit film**.</span><span class="sxs-lookup"><span data-stu-id="b7b00-201">When the *DeleteMovie* page appears, click **Delete Movie**.</span></span>

![Stránka odstranit film s zvýrazněným tlačítkem odstranit video](deleting-data/_static/image4.png)

<span data-ttu-id="b7b00-203">Když kliknete na tlačítko, kód odstraní filmy a vrátí se do seznamu filmů.</span><span class="sxs-lookup"><span data-stu-id="b7b00-203">When you click the button, the code deletes the movies and returns to the movie listing.</span></span> <span data-ttu-id="b7b00-204">Můžete vyhledat odstraněný film a potvrdit, že je odstraněný.</span><span class="sxs-lookup"><span data-stu-id="b7b00-204">There you can search for the deleted movie and confirm that it's been deleted.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="b7b00-205">Připravujeme další</span><span class="sxs-lookup"><span data-stu-id="b7b00-205">Coming Up Next</span></span>

<span data-ttu-id="b7b00-206">V dalším kurzu se dozvíte, jak dát všem stránkám na vašem webu běžný vzhled a rozložení.</span><span class="sxs-lookup"><span data-stu-id="b7b00-206">The next tutorial shows you how to give all the pages on your site a common look and layout.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a><span data-ttu-id="b7b00-207">Úplný výpis stránky videa (aktualizovaný s odkazy Delete)</span><span class="sxs-lookup"><span data-stu-id="b7b00-207">Complete Listing for Movie Page (Updated with Delete Links)</span></span>

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a><span data-ttu-id="b7b00-208">Úplný výpis pro stránku DeleteMovie</span><span class="sxs-lookup"><span data-stu-id="b7b00-208">Complete Listing for DeleteMovie Page</span></span>

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="b7b00-209">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="b7b00-209">Additional Resources</span></span>

- [<span data-ttu-id="b7b00-210">Seznámení s ASP.NET webovým programováním pomocí syntaxe Razor</span><span class="sxs-lookup"><span data-stu-id="b7b00-210">Introduction to ASP.NET Web Programming by Using the Razor Syntax</span></span>](../introducing-razor-syntax-c.md)
- <span data-ttu-id="b7b00-211">[Příkaz SQL Delete](http://www.w3schools.com/sql/sql_delete.asp) na webu w3schools</span><span class="sxs-lookup"><span data-stu-id="b7b00-211">[SQL DELETE Statement](http://www.w3schools.com/sql/sql_delete.asp) on the W3Schools site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="b7b00-212">[Předchozí](updating-data.md)
> [Další](layouts.md)</span><span class="sxs-lookup"><span data-stu-id="b7b00-212">[Previous](updating-data.md)
[Next](layouts.md)</span></span>

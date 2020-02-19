---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
title: Zkoumání toho, jak se ASP.NET (generování uživatelského rozhraní MVC) Pomocník pro DropDownList | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 8921d7f2-21f0-427a-8b27-2df7251174b0
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper
msc.type: authoredcontent
ms.openlocfilehash: 275b20ad964b3e8ddc272a7448f0740ed0891eff
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457606"
---
# <a name="examining--how--aspnet-mvc-scaffolds-the-dropdownlist-helper"></a><span data-ttu-id="f46b3-102">Zkoumání, jak ASP.NET MVC vygeneruje uživatelské rozhraní pomocné rutiny DropDownList</span><span class="sxs-lookup"><span data-stu-id="f46b3-102">Examining  how  ASP.NET MVC scaffolds the DropDownList Helper</span></span>

<span data-ttu-id="f46b3-103">od [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="f46b3-103">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

<span data-ttu-id="f46b3-104">V **Průzkumník řešení**klikněte pravým tlačítkem na složku *Controllers* a pak vyberte **Přidat kontroler**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-104">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span> <span data-ttu-id="f46b3-105">Pojmenujte kontroler **StoreManagerController**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-105">Name the controller **StoreManagerController**.</span></span> <span data-ttu-id="f46b3-106">V dialogovém okně **Přidat řadič** nastavte možnosti, jak je znázorněno na obrázku níže.</span><span class="sxs-lookup"><span data-stu-id="f46b3-106">Set the options for the **Add Controller** dialog as shown in the image below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image1.png)

<span data-ttu-id="f46b3-107">Upravte zobrazení *StoreManager\Index.cshtml* a odeberte `AlbumArtUrl`.</span><span class="sxs-lookup"><span data-stu-id="f46b3-107">Edit the *StoreManager\Index.cshtml* view and remove `AlbumArtUrl`.</span></span> <span data-ttu-id="f46b3-108">Po odebrání `AlbumArtUrl` bude prezentace čitelnější.</span><span class="sxs-lookup"><span data-stu-id="f46b3-108">Removing `AlbumArtUrl` will make the presentation more readable.</span></span> <span data-ttu-id="f46b3-109">Dokončený kód je uveden níže.</span><span class="sxs-lookup"><span data-stu-id="f46b3-109">The completed code is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample1.cshtml)]

<span data-ttu-id="f46b3-110">Otevřete soubor *Controllers\StoreManagerController.cs* a vyhledejte metodu `Index`.</span><span class="sxs-lookup"><span data-stu-id="f46b3-110">Open the *Controllers\StoreManagerController.cs* file and find the `Index` method.</span></span> <span data-ttu-id="f46b3-111">Přidejte klauzuli `OrderBy`, aby se alba seřadila podle ceny.</span><span class="sxs-lookup"><span data-stu-id="f46b3-111">Add the `OrderBy` clause so the albums will be sorted by price.</span></span> <span data-ttu-id="f46b3-112">Úplný kód je uveden níže.</span><span class="sxs-lookup"><span data-stu-id="f46b3-112">The complete code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample2.cs)]

<span data-ttu-id="f46b3-113">Třídění podle ceny usnadňuje testování změn v databázi.</span><span class="sxs-lookup"><span data-stu-id="f46b3-113">Sorting by price will make it easier to test changes to the database.</span></span> <span data-ttu-id="f46b3-114">Při testování metod Edit a Create můžete použít nízkou cenu, aby se uložená data zobrazovala jako první.</span><span class="sxs-lookup"><span data-stu-id="f46b3-114">When you are testing the edit and create methods, you can use a low price so the saved data will appear first.</span></span>

<span data-ttu-id="f46b3-115">Otevřete soubor *StoreManager\Edit.cshtml* .</span><span class="sxs-lookup"><span data-stu-id="f46b3-115">Open the *StoreManager\Edit.cshtml* file.</span></span> <span data-ttu-id="f46b3-116">Přidejte následující řádek hned za značku legendy.</span><span class="sxs-lookup"><span data-stu-id="f46b3-116">Add the following line just after the legend tag.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample3.cshtml)]

<span data-ttu-id="f46b3-117">Následující kód ukazuje kontext této změny:</span><span class="sxs-lookup"><span data-stu-id="f46b3-117">The following code shows the context of this change:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample4.cshtml)]

<span data-ttu-id="f46b3-118">`AlbumId` je nutné provést změny v záznamu alba.</span><span class="sxs-lookup"><span data-stu-id="f46b3-118">The `AlbumId` is required to make changes to an album record.</span></span>

<span data-ttu-id="f46b3-119">Stiskněte klávesy CTRL+F5 a spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="f46b3-119">Press CTRL+F5 to run the application.</span></span> <span data-ttu-id="f46b3-120">Vyberte odkaz pro **správce** a pak výběrem odkazu **vytvořit nový** vytvořte nové album.</span><span class="sxs-lookup"><span data-stu-id="f46b3-120">Select to the **Admin** link, then select the **Create New** link to create a new album.</span></span> <span data-ttu-id="f46b3-121">Ověřte, že informace o albu byly uloženy.</span><span class="sxs-lookup"><span data-stu-id="f46b3-121">Verify the album information was saved.</span></span> <span data-ttu-id="f46b3-122">Upravte album a ověřte, že změny, které jste provedli, jsou trvalé.</span><span class="sxs-lookup"><span data-stu-id="f46b3-122">Edit an album and verify the changes you made are persisted.</span></span>

### <a name="the-album-schema"></a><span data-ttu-id="f46b3-123">Schéma alba</span><span class="sxs-lookup"><span data-stu-id="f46b3-123">The Album Schema</span></span>

<span data-ttu-id="f46b3-124">Kontroler `StoreManager` vytvořený mechanismem generování uživatelského rozhraní MVC umožňuje CRUD (vytvořit, číst, aktualizovat, odstranit) přístup k albu v databázi úložiště hudby.</span><span class="sxs-lookup"><span data-stu-id="f46b3-124">The `StoreManager` controller created by the MVC scaffolding mechanism allows CRUD (Create, Read, Update, Delete) access to the albums in the music store database.</span></span> <span data-ttu-id="f46b3-125">Schéma pro informace o albu se zobrazuje níže:</span><span class="sxs-lookup"><span data-stu-id="f46b3-125">The schema for album information is shown below:</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image2.png)

<span data-ttu-id="f46b3-126">Tabulka `Albums` neukládá Žánr a popis alba, ukládá do tabulky `Genres` cizí klíč.</span><span class="sxs-lookup"><span data-stu-id="f46b3-126">The `Albums` table does not store the album genre and description, it stores a foreign key to the `Genres` table.</span></span> <span data-ttu-id="f46b3-127">Tabulka `Genres` obsahuje název a popis žánru.</span><span class="sxs-lookup"><span data-stu-id="f46b3-127">The `Genres` table contains the genre name and description.</span></span> <span data-ttu-id="f46b3-128">Podobně `Albums` tabulka neobsahuje název umělců alba, ale cizí klíč do tabulky `Artists`.</span><span class="sxs-lookup"><span data-stu-id="f46b3-128">Likewise, the `Albums` table doesn't contain the album artists name, but a foreign key to the `Artists` table.</span></span> <span data-ttu-id="f46b3-129">Tabulka `Artists` obsahuje jméno umělce.</span><span class="sxs-lookup"><span data-stu-id="f46b3-129">The `Artists` table contains the artist's name.</span></span> <span data-ttu-id="f46b3-130">Pokud prohlížíte data v tabulce `Albums`, vidíte každý řádek obsahuje cizí klíč do tabulky `Genres` a cizí klíč do tabulky `Artists`.</span><span class="sxs-lookup"><span data-stu-id="f46b3-130">If you examine the data in the `Albums` table, you can see each row contains a foreign key to the `Genres` table and a foreign key to the `Artists` table.</span></span> <span data-ttu-id="f46b3-131">Následující obrázek ukazuje data tabulky z `Albums` tabulky.</span><span class="sxs-lookup"><span data-stu-id="f46b3-131">The image below show some table data from the `Albums` table.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image3.png)

### <a name="the-html-select-tag"></a><span data-ttu-id="f46b3-132">Značka výběru HTML</span><span class="sxs-lookup"><span data-stu-id="f46b3-132">The HTML Select Tag</span></span>

<span data-ttu-id="f46b3-133">Element HTML `<select>` (vytvořený pomocí pomocníka [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) HTML) slouží k zobrazení úplného seznamu hodnot (například seznamu žánrů).</span><span class="sxs-lookup"><span data-stu-id="f46b3-133">The HTML `<select>` element (created by the HTML [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) helper) is used to display a complete list of values (such as the list of genres).</span></span> <span data-ttu-id="f46b3-134">Pro upravit formuláře, pokud je aktuální hodnota známa, může seznam SELECT zobrazit aktuální hodnotu.</span><span class="sxs-lookup"><span data-stu-id="f46b3-134">For edit forms, when the current value is known, the select list can display the current value.</span></span> <span data-ttu-id="f46b3-135">Tuto možnost jsme dřív viděli, když jsme tuto hodnotu nastavili na **komedie**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-135">We saw this previously when we set the selected value to **Comedy**.</span></span> <span data-ttu-id="f46b3-136">Seznam pro výběr je ideální pro zobrazení dat kategorie nebo cizího klíče.</span><span class="sxs-lookup"><span data-stu-id="f46b3-136">The select list is ideal for displaying category or foreign key data.</span></span> <span data-ttu-id="f46b3-137">Element `<select>` pro cizí klíč žánru zobrazuje seznam možných názvů žánrů, ale při uložení formuláře se vlastnost Žánr aktualizuje s hodnotou cizího klíče žánru, nikoli zobrazeným názvem žánru.</span><span class="sxs-lookup"><span data-stu-id="f46b3-137">The `<select>` element for the Genre foreign key displays the list of possible genre names, but when you save the form the Genre property is updated with the Genre foreign key value, not the displayed genre name.</span></span> <span data-ttu-id="f46b3-138">Na následujícím obrázku je vybraný Žánr na **discích** a interpret je **Donnou letního**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-138">In the image below, the genre selected is **Disco** and the artist is **Donna Summer**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image4.png)

### <a name="examining-the-aspnet-mvc-scaffolded-code"></a><span data-ttu-id="f46b3-139">Zkoumání generovaného kódu ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="f46b3-139">Examining the ASP.NET MVC Scaffolded Code</span></span>

<span data-ttu-id="f46b3-140">Otevřete soubor *Controllers\StoreManagerController.cs* a vyhledejte metodu `HTTP GET Create`.</span><span class="sxs-lookup"><span data-stu-id="f46b3-140">Open the *Controllers\StoreManagerController.cs* file and find the `HTTP GET Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample5.cs)]

<span data-ttu-id="f46b3-141">Metoda `Create` přidá do `ViewBag`dva objekty [SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) , jeden, který obsahuje informace o žánru, a druhý, který obsahuje informace o interpretu.</span><span class="sxs-lookup"><span data-stu-id="f46b3-141">The `Create` method adds two [SelectList](https://msdn.microsoft.com/library/system.web.mvc.selectlist.aspx) objects to the `ViewBag`, one to contain the genre information, and one to contain the artist information.</span></span> <span data-ttu-id="f46b3-142">Výše použité přetížení konstruktoru [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) má tři argumenty:</span><span class="sxs-lookup"><span data-stu-id="f46b3-142">The [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) constructor overload used above takes three arguments:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample6.cs)]

1. <span data-ttu-id="f46b3-143">*Items*: rozhraní [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) obsahující položky v seznamu.</span><span class="sxs-lookup"><span data-stu-id="f46b3-143">*items*: An [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) containing the items in the list.</span></span> <span data-ttu-id="f46b3-144">V předchozím příkladu je uveden seznam žánrů vrácených `db.Genres`.</span><span class="sxs-lookup"><span data-stu-id="f46b3-144">In the example above, the list of genres returned by `db.Genres`.</span></span>
2. <span data-ttu-id="f46b3-145">*dataValueField*: název vlastnosti v seznamu **IEnumerable** , který obsahuje hodnotu klíče.</span><span class="sxs-lookup"><span data-stu-id="f46b3-145">*dataValueField*: The name of the property in the **IEnumerable** list that contains the key value.</span></span> <span data-ttu-id="f46b3-146">V předchozím příkladu `GenreId` a `ArtistId`.</span><span class="sxs-lookup"><span data-stu-id="f46b3-146">In the example above, `GenreId` and `ArtistId`.</span></span>
3. <span data-ttu-id="f46b3-147">*dataTextField*: název vlastnosti v seznamu **IEnumerable** obsahující informace, které se mají zobrazit.</span><span class="sxs-lookup"><span data-stu-id="f46b3-147">*dataTextField*: The name of the property in the **IEnumerable** list that contains the information to display.</span></span> <span data-ttu-id="f46b3-148">V tabulce interpreti a žánru se používá pole `name`.</span><span class="sxs-lookup"><span data-stu-id="f46b3-148">In both the artists and genre table, the `name` field is used.</span></span>

<span data-ttu-id="f46b3-149">Otevřete soubor *Views\StoreManager\Create.cshtml* a Projděte si označení pomocné rutiny `Html.DropDownList` pro pole Žánr.</span><span class="sxs-lookup"><span data-stu-id="f46b3-149">Open the *Views\StoreManager\Create.cshtml* file and examine the `Html.DropDownList` helper markup for the genre field.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample7.cshtml)]

<span data-ttu-id="f46b3-150">První řádek ukazuje, že zobrazení vytvořit přebírá model `Album`.</span><span class="sxs-lookup"><span data-stu-id="f46b3-150">The first line shows that the create view takes an `Album` model.</span></span> <span data-ttu-id="f46b3-151">Ve výše uvedené metodě `Create` nebyl předán žádný model, takže zobrazení získá `Album` model s **hodnotou null** .</span><span class="sxs-lookup"><span data-stu-id="f46b3-151">In the `Create` method shown above, no model was passed, so the view gets a **null** `Album` model.</span></span> <span data-ttu-id="f46b3-152">V tuto chvíli vytváříme nové album, takže pro něj neexistují žádná `Album` data.</span><span class="sxs-lookup"><span data-stu-id="f46b3-152">At this point we are creating a new album so we don't have any `Album` data for it.</span></span>

<span data-ttu-id="f46b3-153">Výše zobrazené přetížení [HTML. DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) vezme název pole, které se má vytvořit jako vazby k modelu.</span><span class="sxs-lookup"><span data-stu-id="f46b3-153">The [Html.DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) overload shown above takes the name of the field to bind to the model.</span></span> <span data-ttu-id="f46b3-154">Tento název také používá k vyhledání objektu **ViewBag** obsahujícího objekt [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) .</span><span class="sxs-lookup"><span data-stu-id="f46b3-154">It also uses this name to look for a **ViewBag** object containing a [SelectList](https://msdn.microsoft.com/library/dd505286.aspx) object.</span></span> <span data-ttu-id="f46b3-155">Pomocí tohoto přetížení budete muset pojmenovat objekt **ViewBag SelectList** `GenreId`.</span><span class="sxs-lookup"><span data-stu-id="f46b3-155">Using this overload, you are required to name the **ViewBag SelectList** object `GenreId`.</span></span> <span data-ttu-id="f46b3-156">Druhý parametr (`String.Empty`) je text, který se zobrazí, když není vybrána žádná položka.</span><span class="sxs-lookup"><span data-stu-id="f46b3-156">The second parameter (`String.Empty`) is the text to display when no item is selected.</span></span> <span data-ttu-id="f46b3-157">To je přesně to, co chceme při vytváření nového alba.</span><span class="sxs-lookup"><span data-stu-id="f46b3-157">This is exactly what we want when creating a new album.</span></span> <span data-ttu-id="f46b3-158">Pokud jste odebrali druhý parametr a použili jste následující kód:</span><span class="sxs-lookup"><span data-stu-id="f46b3-158">If you removed the second parameter and used the following code:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample8.cshtml)]

<span data-ttu-id="f46b3-159">Seznam SELECT by byl výchozím nastavením prvního prvku nebo rock v naší ukázce.</span><span class="sxs-lookup"><span data-stu-id="f46b3-159">The select list would default to the first element, or Rock in our sample.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image5.png)

<span data-ttu-id="f46b3-160">Prověřování metody `HTTP POST Create`.</span><span class="sxs-lookup"><span data-stu-id="f46b3-160">Examining the `HTTP POST Create` method.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample9.cs)]

<span data-ttu-id="f46b3-161">Toto přetížení metody `Create` přebírá objekt `album` vytvořený systémem vazeb modelu ASP.NET MVC z publikovaných hodnot formuláře.</span><span class="sxs-lookup"><span data-stu-id="f46b3-161">This overload of the `Create` method takes an `album` object, created by the ASP.NET MVC model binding system from the form values posted.</span></span> <span data-ttu-id="f46b3-162">Pokud odešlete nové album, pokud je stav modelu platný a nejsou k dispozici žádné chyby databáze, přidá se k novému albu databáze.</span><span class="sxs-lookup"><span data-stu-id="f46b3-162">When you submit a new album, if model state is valid and there are no database errors, the new album is added the database.</span></span> <span data-ttu-id="f46b3-163">Následující obrázek ukazuje vytvoření nového alba.</span><span class="sxs-lookup"><span data-stu-id="f46b3-163">The following image shows the creation of a new album.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image6.png)

<span data-ttu-id="f46b3-164">Pomocí [nástroje Fiddler](http://www.fiddler2.com/fiddler2/) můžete prostudovat zaúčtované hodnoty formulářů, které ASP.NET MVC modelů používá k vytvoření objektu alba.</span><span class="sxs-lookup"><span data-stu-id="f46b3-164">You can use the [fiddler tool](http://www.fiddler2.com/fiddler2/) to examine the posted form values that ASP.NET MVC model binding uses to create the album object.</span></span>

<span data-ttu-id="f46b3-165">![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png).</span><span class="sxs-lookup"><span data-stu-id="f46b3-165">![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image7.png).</span></span>

### <a name="refactoring-the-viewbag-selectlist-creation"></a><span data-ttu-id="f46b3-166">Refaktoring SelectList vytváření ViewBag</span><span class="sxs-lookup"><span data-stu-id="f46b3-166">Refactoring the ViewBag SelectList Creation</span></span>

<span data-ttu-id="f46b3-167">Metody `Edit` a metoda `HTTP POST Create` mají stejný kód pro nastavení **SelectList** v **ViewBag**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-167">Both the `Edit` methods and the `HTTP POST Create` method have identical code to set up the **SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="f46b3-168">V duchu [suchého](http://en.wikipedia.org/wiki/Don't_repeat_yourself)kódu budeme tento kód Refaktorovat.</span><span class="sxs-lookup"><span data-stu-id="f46b3-168">In the spirit of [DRY](http://en.wikipedia.org/wiki/Don't_repeat_yourself), we will refactor this code.</span></span> <span data-ttu-id="f46b3-169">Pomocí tohoto refaktoringového kódu ho později využijeme.</span><span class="sxs-lookup"><span data-stu-id="f46b3-169">We'll make use of this refactored code later.</span></span>

<span data-ttu-id="f46b3-170">Vytvořte novou metodu pro přidání žánru a interpreta **SelectList** do **ViewBag**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-170">Create a new method to add a genre and artist **SelectList** to the **ViewBag**.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample10.cs)]

<span data-ttu-id="f46b3-171">Nahraďte dva řádky nastavením `ViewBag` v každé z `Create` a `Edit` metody voláním metody `SetGenreArtistViewBag`.</span><span class="sxs-lookup"><span data-stu-id="f46b3-171">Replace the two lines setting the `ViewBag` in each of the `Create` and `Edit` methods with a call to the `SetGenreArtistViewBag` method.</span></span> <span data-ttu-id="f46b3-172">Dokončený kód je uveden níže.</span><span class="sxs-lookup"><span data-stu-id="f46b3-172">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample11.cs)]

<span data-ttu-id="f46b3-173">Vytvořením nového alba a úpravou alba ověřte, zda změny fungují.</span><span class="sxs-lookup"><span data-stu-id="f46b3-173">Create a new album and edit an album to verify the changes work.</span></span>

### <a name="explicitly-passing-the-selectlist-to-the-dropdownlist"></a><span data-ttu-id="f46b3-174">Explicitní předání SelectList do DropDownList</span><span class="sxs-lookup"><span data-stu-id="f46b3-174">Explicitly Passing the SelectList to the DropDownList</span></span>

<span data-ttu-id="f46b3-175">Zobrazení vytvořit a upravit vytvořená pomocí generování uživatelského rozhraní ASP.NET MVC používají následující přetížení **DropDownList** :</span><span class="sxs-lookup"><span data-stu-id="f46b3-175">The create and edit views created by the ASP.NET MVC scaffolding use the following **DropDownList** overload:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample12.cs)]

<span data-ttu-id="f46b3-176">`DropDownList` značky pro zobrazení pro vytváření jsou uvedeny níže.</span><span class="sxs-lookup"><span data-stu-id="f46b3-176">The `DropDownList` markup for the create view is shown below.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample13.cshtml)]

<span data-ttu-id="f46b3-177">Vzhledem k tomu, že vlastnost `ViewBag` pro `SelectList` má název `GenreId`, pomocník **DropDownList** použije `GenreId`**SelectList** v **ViewBag**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-177">Because the `ViewBag` property for the `SelectList` is named `GenreId`, the **DropDownList** helper will use the `GenreId`**SelectList** in the **ViewBag**.</span></span> <span data-ttu-id="f46b3-178">V následujícím přetížení **DropDownList** je `SelectList` explicitně předán v.</span><span class="sxs-lookup"><span data-stu-id="f46b3-178">In the following **DropDownList** overload, the `SelectList` is explicitly passed in.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample14.cs)]

<span data-ttu-id="f46b3-179">Otevřete soubor *Views\StoreManager\Edit.cshtml* a změňte volání **DropDownList** tak, aby explicitně předávalo v **SelectList**, pomocí výše uvedeného přetížení.</span><span class="sxs-lookup"><span data-stu-id="f46b3-179">Open the *Views\StoreManager\Edit.cshtml* file, and change the **DropDownList** call to explicitly pass in the **SelectList**, using the overload above.</span></span> <span data-ttu-id="f46b3-180">Proveďte tuto kategorii žánru.</span><span class="sxs-lookup"><span data-stu-id="f46b3-180">Do this for the Genre category.</span></span> <span data-ttu-id="f46b3-181">Dokončený kód je zobrazen níže:</span><span class="sxs-lookup"><span data-stu-id="f46b3-181">The completed code is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample15.cshtml)]

<span data-ttu-id="f46b3-182">Spusťte aplikaci a klikněte na odkaz **správce** , přejděte na album jazz a vyberte odkaz **Upravit** .</span><span class="sxs-lookup"><span data-stu-id="f46b3-182">Run the application and click the **Admin** link, then navigate to a Jazz album and select the **Edit** link.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image8.png)

<span data-ttu-id="f46b3-183">Místo zobrazení Jazz jako aktuálně vybraného žánru se zobrazí rock.</span><span class="sxs-lookup"><span data-stu-id="f46b3-183">Instead of showing Jazz as the currently selected genre, Rock is displayed.</span></span> <span data-ttu-id="f46b3-184">Pokud má argument řetězce (vlastnost k vytvoření vazby) a objekt **SelectList** stejný název, vybraná hodnota se nepoužije.</span><span class="sxs-lookup"><span data-stu-id="f46b3-184">When the string argument (the property to bind) and the **SelectList** object have the same name, the selected value is not used.</span></span> <span data-ttu-id="f46b3-185">Pokud není zadána žádná vybraná hodnota, prohlížeče se standardně naplní na první prvek v **SelectList**(což je **Rock** v příkladu výše).</span><span class="sxs-lookup"><span data-stu-id="f46b3-185">When there is no selected value provided, browsers default to the first element in the **SelectList**(which is **Rock** in the example above).</span></span> <span data-ttu-id="f46b3-186">Toto je známé omezení pomocné rutiny **DropDownList** .</span><span class="sxs-lookup"><span data-stu-id="f46b3-186">This is a known limitation of the **DropDownList** helper.</span></span>

<span data-ttu-id="f46b3-187">Otevřete soubor *Controllers\StoreManagerController.cs* a změňte názvy objektů **SelectList** na `Genres` a `Artists`.</span><span class="sxs-lookup"><span data-stu-id="f46b3-187">Open the *Controllers\StoreManagerController.cs* file and change the **SelectList** object names to `Genres` and `Artists`.</span></span> <span data-ttu-id="f46b3-188">Dokončený kód je zobrazen níže:</span><span class="sxs-lookup"><span data-stu-id="f46b3-188">The completed code is shown below:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample16.cs)]

<span data-ttu-id="f46b3-189">Názvy žánrů a umělců mají lepší názvy kategorií, protože obsahují více než pouze ID každé kategorie.</span><span class="sxs-lookup"><span data-stu-id="f46b3-189">The names Genres and Artists are better names for the categories, as they contain more than just the ID of each category.</span></span> <span data-ttu-id="f46b3-190">Refaktoring, kterou jsme dříve vyplatili.</span><span class="sxs-lookup"><span data-stu-id="f46b3-190">The refactoring we did earlier paid off.</span></span> <span data-ttu-id="f46b3-191">Místo změny **ViewBag** ve čtyřech metodách byly tyto změny izolovány na metodu `SetGenreArtistViewBag`.</span><span class="sxs-lookup"><span data-stu-id="f46b3-191">Instead of changing the **ViewBag** in four methods, our changes were isolated to the `SetGenreArtistViewBag` method.</span></span>

<span data-ttu-id="f46b3-192">Chcete-li použít nové názvy **SelectList** , změňte volání **DropDownList** v zobrazeních Create a Edit.</span><span class="sxs-lookup"><span data-stu-id="f46b3-192">Change the **DropDownList** call in the create and edit views to use the new **SelectList** names.</span></span> <span data-ttu-id="f46b3-193">Nové značky pro zobrazení pro úpravy jsou uvedené níže:</span><span class="sxs-lookup"><span data-stu-id="f46b3-193">The new markup for the edit view is shown below:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample17.cshtml)]

<span data-ttu-id="f46b3-194">Zobrazení vytvořit vyžaduje prázdný řetězec, aby se zabránilo zobrazení první položky v SelectList.</span><span class="sxs-lookup"><span data-stu-id="f46b3-194">The Create view requires an empty string to prevent the first item in the SelectList from being displayed.</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample18.cshtml)]

<span data-ttu-id="f46b3-195">Vytvořením nového alba a úpravou alba ověřte, zda změny fungují.</span><span class="sxs-lookup"><span data-stu-id="f46b3-195">Create a new album and edit an album to verify the changes work.</span></span> <span data-ttu-id="f46b3-196">Otestujte kód úprav tak, že vyberete album s jiným žánrem než rock.</span><span class="sxs-lookup"><span data-stu-id="f46b3-196">Test the edit code by selecting an album with a genre other than Rock.</span></span>

### <a name="using-a-view-model-with-the-dropdownlist-helper"></a><span data-ttu-id="f46b3-197">Použití modelu zobrazení s pomocníkem DropDownList</span><span class="sxs-lookup"><span data-stu-id="f46b3-197">Using a View Model with the DropDownList Helper</span></span>

<span data-ttu-id="f46b3-198">Vytvořte novou třídu ve složce ViewModels s názvem `AlbumSelectListViewModel`.</span><span class="sxs-lookup"><span data-stu-id="f46b3-198">Create a new class in the ViewModels folder named `AlbumSelectListViewModel`.</span></span> <span data-ttu-id="f46b3-199">Nahraďte kód ve třídě `AlbumSelectListViewModel` následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="f46b3-199">Replace the code in the `AlbumSelectListViewModel` class with the following:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample19.cs)]

<span data-ttu-id="f46b3-200">Konstruktor `AlbumSelectListViewModel` převezme album, Seznam umělců a žánrů a vytvoří objekt obsahující album a `SelectList` pro žánry a interprety.</span><span class="sxs-lookup"><span data-stu-id="f46b3-200">The `AlbumSelectListViewModel` constructor takes an album, a list of artists and genres and creates an object containing the album and a `SelectList` for genres and artists.</span></span>

<span data-ttu-id="f46b3-201">Sestavte projekt, aby `AlbumSelectListViewModel` k dispozici, když vytvoříme zobrazení v dalším kroku.</span><span class="sxs-lookup"><span data-stu-id="f46b3-201">Build the project so the `AlbumSelectListViewModel` is available when we create a view in the next step.</span></span>

<span data-ttu-id="f46b3-202">Přidejte do `StoreManagerController`metodu `EditVM`.</span><span class="sxs-lookup"><span data-stu-id="f46b3-202">Add an `EditVM` method to the `StoreManagerController`.</span></span> <span data-ttu-id="f46b3-203">Dokončený kód je uveden níže.</span><span class="sxs-lookup"><span data-stu-id="f46b3-203">The completed code is shown below.</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample20.cs)]

<span data-ttu-id="f46b3-204">Klikněte pravým tlačítkem `AlbumSelectListViewModel`, vyberte **vyřešit**a pak **použijte MvcMusicStore. ViewModels;** .</span><span class="sxs-lookup"><span data-stu-id="f46b3-204">Right click `AlbumSelectListViewModel`, select **Resolve**, then **using MvcMusicStore.ViewModels;**.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image9.png)

<span data-ttu-id="f46b3-205">Alternativně můžete přidat následující příkaz using:</span><span class="sxs-lookup"><span data-stu-id="f46b3-205">Alternatively, you can add the following using statement:</span></span>

[!code-csharp[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample21.cs)]

<span data-ttu-id="f46b3-206">Klikněte pravým tlačítkem `EditVM` a vyberte **Přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-206">Right click `EditVM` and select **Add View**.</span></span> <span data-ttu-id="f46b3-207">Použijte níže uvedené možnosti.</span><span class="sxs-lookup"><span data-stu-id="f46b3-207">Use the options shown below.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image10.png)

<span data-ttu-id="f46b3-208">Vyberte **Přidat**a potom nahraďte obsah souboru *Views\StoreManager\EditVM.cshtml* následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="f46b3-208">Select **Add**, then replace the contents of the *Views\StoreManager\EditVM.cshtml* file with the following:</span></span>

[!code-cshtml[Main](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/samples/sample22.cshtml)]

<span data-ttu-id="f46b3-209">Kód `EditVM` se velmi podobá původnímu `Edit` označení pomocí následujících výjimek.</span><span class="sxs-lookup"><span data-stu-id="f46b3-209">The `EditVM` markup is very similar to the original `Edit` markup with the following exceptions.</span></span>

- <span data-ttu-id="f46b3-210">Vlastnosti modelu v zobrazení `Edit` mají `model.property`formuláře (například `model.Title`).</span><span class="sxs-lookup"><span data-stu-id="f46b3-210">Model properties in the `Edit` view are of the form `model.property`(for example, `model.Title` ).</span></span> <span data-ttu-id="f46b3-211">Vlastnosti modelu v zobrazení `EditVm` mají `model.Album.property`formuláře (například `model.Album.Title`).</span><span class="sxs-lookup"><span data-stu-id="f46b3-211">Model properties in the `EditVm` view are of the form `model.Album.property`(for example, `model.Album.Title`).</span></span> <span data-ttu-id="f46b3-212">Důvodem je, že zobrazení `EditVM` předává kontejner pro `Album`, nikoli `Album` jako v `Edit`ém zobrazení.</span><span class="sxs-lookup"><span data-stu-id="f46b3-212">That's because the `EditVM` view is passed a container for an `Album`, not an `Album` as in the `Edit` view.</span></span>
- <span data-ttu-id="f46b3-213">Druhý parametr **DropDownList** pochází z modelu zobrazení, ne z **ViewBag**.</span><span class="sxs-lookup"><span data-stu-id="f46b3-213">The **DropDownList** second parameter comes from the view model, not the **ViewBag**.</span></span>
- <span data-ttu-id="f46b3-214">Pomocná rutina **BeginForm** v zobrazení `EditVM` explicitně odesílá zpět do metody `Edit` akce.</span><span class="sxs-lookup"><span data-stu-id="f46b3-214">The **BeginForm** helper in the `EditVM` view explicitly posts back to the `Edit` action method.</span></span> <span data-ttu-id="f46b3-215">Po odeslání zpět do akce `Edit` nemusíme psát `HTTP POST EditVM` akci a může znovu použít `HTTP POST` `Edit` akci.</span><span class="sxs-lookup"><span data-stu-id="f46b3-215">By posting back to the `Edit` action, we don't have to write an `HTTP POST EditVM` action and can reuse the `HTTP POST` `Edit` action.</span></span>

<span data-ttu-id="f46b3-216">Spusťte aplikaci a upravte album.</span><span class="sxs-lookup"><span data-stu-id="f46b3-216">Run the application and edit an album.</span></span> <span data-ttu-id="f46b3-217">Změňte adresu URL na použití `EditVM`.</span><span class="sxs-lookup"><span data-stu-id="f46b3-217">Change the URL to use `EditVM`.</span></span> <span data-ttu-id="f46b3-218">Změňte pole a stiskněte tlačítko **Uložit** a ověřte, zda kód funguje.</span><span class="sxs-lookup"><span data-stu-id="f46b3-218">Change a field and hit the **Save** button to verify the code is working.</span></span>

![](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper/_static/image11.png)

### <a name="which-approach-should-you-use"></a><span data-ttu-id="f46b3-219">Který přístup byste měli použít?</span><span class="sxs-lookup"><span data-stu-id="f46b3-219">Which Approach Should You Use?</span></span>

<span data-ttu-id="f46b3-220">Všechny uvedené tři přístupy jsou přijatelné.</span><span class="sxs-lookup"><span data-stu-id="f46b3-220">All three approaches shown are acceptable.</span></span> <span data-ttu-id="f46b3-221">Mnoho vývojářů upřednostňuje explicitně předat `SelectList` do `DropDownList` pomocí `ViewBag`.</span><span class="sxs-lookup"><span data-stu-id="f46b3-221">Many developers prefer to explicitly pass the `SelectList` to the `DropDownList` using the `ViewBag`.</span></span> <span data-ttu-id="f46b3-222">Tento přístup má výhodu k tomu, abyste vám poskytli flexibilitu při používání vhodnějšího názvu kolekce.</span><span class="sxs-lookup"><span data-stu-id="f46b3-222">This approach has the added advantage of giving you the flexibility of using a more appropriate name for the collection.</span></span> <span data-ttu-id="f46b3-223">Jediným aspektem je, že objekt `ViewBag SelectList` nemůžete pojmenovat stejným názvem jako vlastnost modelu.</span><span class="sxs-lookup"><span data-stu-id="f46b3-223">The one caveat is you cannot name the `ViewBag SelectList` object the same name as the model property.</span></span>

<span data-ttu-id="f46b3-224">Někteří vývojáři upřednostňují přístup k ViewModel.</span><span class="sxs-lookup"><span data-stu-id="f46b3-224">Some developers prefer the ViewModel approach.</span></span> <span data-ttu-id="f46b3-225">Jiné považují podrobnější značky a vygenerovaný kód HTML ViewModel přístupu k nevýhodám.</span><span class="sxs-lookup"><span data-stu-id="f46b3-225">Others consider the more verbose markup and generated HTML of the ViewModel approach a disadvantage.</span></span>

<span data-ttu-id="f46b3-226">V této části jsme zjistili tři přístupy k použití ovládacího prvkem **DropDownList** s daty kategorií.</span><span class="sxs-lookup"><span data-stu-id="f46b3-226">In this section we have learned three approaches to using the **DropDownList** with category data.</span></span> <span data-ttu-id="f46b3-227">V další části si ukážeme, jak přidat novou kategorii.</span><span class="sxs-lookup"><span data-stu-id="f46b3-227">In the next section, we'll show how to add a new category.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f46b3-228">[Předchozí](using-the-dropdownlist-helper-with-aspnet-mvc.md)
> [Další](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span><span class="sxs-lookup"><span data-stu-id="f46b3-228">[Previous](using-the-dropdownlist-helper-with-aspnet-mvc.md)
[Next](adding-a-new-category-to-the-dropdownlist-using-jquery-ui.md)</span></span>

---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
title: Přidání nové kategorie do DropDownList pomocí uživatelského rozhraní jQuery | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 44aa1ac4-6ea2-48a2-972d-52710c48eae5
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/adding-a-new-category-to-the-dropdownlist-using-jquery-ui
msc.type: authoredcontent
ms.openlocfilehash: cb9053593e2ea788638aec063c845cb91121861b
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075109"
---
# <a name="adding-a-new-category-to-the-dropdownlist-using-jquery-ui"></a><span data-ttu-id="36808-102">Přidání nové kategorie do ovládacího prvku DropDownList v uživatelském rozhraní jQuery</span><span class="sxs-lookup"><span data-stu-id="36808-102">Adding a New Category to the DropDownList using jQuery UI</span></span>

<span data-ttu-id="36808-103">od [Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="36808-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

<span data-ttu-id="36808-104">Značka HTML `Select` je ideální pro prezentaci seznamu dat pevné kategorie, ale často je potřeba přidat novou kategorii.</span><span class="sxs-lookup"><span data-stu-id="36808-104">The HTML `Select` tag is ideal for presenting a list of fixed category data, but often times you need to add a new category.</span></span> <span data-ttu-id="36808-105">Předpokládejme, že chceme přidat Žánr "Operait" do kategorií v naší databázi?</span><span class="sxs-lookup"><span data-stu-id="36808-105">Suppose we want to add the genre "Opera" to the categories in our database?</span></span> <span data-ttu-id="36808-106">V této části použijeme uživatelské rozhraní jQuery k přidání dialogového okna, které můžeme použít k přidání nové kategorie.</span><span class="sxs-lookup"><span data-stu-id="36808-106">In this section, we will use jQuery UI to add a dialog box we can use to add a new category.</span></span> <span data-ttu-id="36808-107">Následující obrázek ukazuje, jak bude uživatelské rozhraní v prohlížeči k dispozici.</span><span class="sxs-lookup"><span data-stu-id="36808-107">The image below shows how the UI will present in the browser.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image1.png)

<span data-ttu-id="36808-108">Když uživatel vybere odkaz **Přidat nový žánr** , automaticky otevírané okno vyzve uživatele k zadání nového názvu žánru (a volitelně i popisu).</span><span class="sxs-lookup"><span data-stu-id="36808-108">When a user selects the **Add New Genre** link, a pop-up dialog box prompts the user for a new genre name (and optionally a description).</span></span> <span data-ttu-id="36808-109">Následující obrázek ukazuje místní dialog **Přidat Žánr** .</span><span class="sxs-lookup"><span data-stu-id="36808-109">The image below show the **Add Genre** pop-up dialog.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image2.png)

<span data-ttu-id="36808-110">Při zadání nového názvu žánru a vložení tlačítka **Uložit** dojde k následujícímu:</span><span class="sxs-lookup"><span data-stu-id="36808-110">When a new genre name is entered and the **Save** button is pushed, the following happens:</span></span>

1. <span data-ttu-id="36808-111">Volání jazyka AJAX odesílá data do metody Create (žánr Controller), která uloží nový žánr do databáze a vrátí nové informace o žánru (název žánru a ID) jako JSON.</span><span class="sxs-lookup"><span data-stu-id="36808-111">An AJAX call posts the data to the Create method of the Genre Controller, which saves the new genre to the database and returns the new genre information (genre name and ID) as JSON.</span></span>
2. <span data-ttu-id="36808-112">JavaScript přidá nová data žánru do seznamu SELECT.</span><span class="sxs-lookup"><span data-stu-id="36808-112">JavaScript adds the new genre data to the select list.</span></span>
3. <span data-ttu-id="36808-113">JavaScript vytvoří nový žánr pro vybranou položku.</span><span class="sxs-lookup"><span data-stu-id="36808-113">JavaScript makes the new genre the selected item.</span></span>

   <span data-ttu-id="36808-114">Na následujícím obrázku byl do databáze přidán **Opera** a v rozevíracím seznamu **žánru** byl vybrán.</span><span class="sxs-lookup"><span data-stu-id="36808-114">In the image below, **Opera** was added to the database and selected in the **Genre** drop down list.</span></span> 

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image3.png)

<span data-ttu-id="36808-115">Otevřete soubor *Views\StoreManager\Create.cshtml* a nahraďte kód žánru následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="36808-115">Open the *Views\StoreManager\Create.cshtml* file and replace the genre markup with the following the following code:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample1.cshtml)]

<span data-ttu-id="36808-116">`_ChooseGenre` částečné zobrazení bude obsahovat veškerou logiku pro připojení JavaScriptu a jQuery, která se používá k implementaci funkce Přidat nový žánr.</span><span class="sxs-lookup"><span data-stu-id="36808-116">The `_ChooseGenre` partial view will contain all the logic to hook up the JavaScript and jQuery used to implement the add new genre feature.</span></span> <span data-ttu-id="36808-117">Až kód dokončíme, bude se jednoduše dělat stejně jako uživatelské rozhraní umělce.</span><span class="sxs-lookup"><span data-stu-id="36808-117">Once we have completed the code it will be simple to do the same with the artist UI.</span></span>

<span data-ttu-id="36808-118">V Průzkumník řešení klikněte pravým tlačítkem na složku *Views\StoreManager* a vyberte **Přidat**a pak **Zobrazit**.</span><span class="sxs-lookup"><span data-stu-id="36808-118">In Solution Explorer, right click the *Views\StoreManager* folder and select **Add**, then **View**.</span></span> <span data-ttu-id="36808-119">Do pole **název zobrazení** zadejte `_ChooseGenre` a pak vyberte **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="36808-119">In the **View name** input, enter `_ChooseGenre` then select **Add**.</span></span> <span data-ttu-id="36808-120">Nahraďte kód v souboru *Views\StoreManager\\_ChooseGenre. cshtml* následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="36808-120">Replace the markup in the *Views\StoreManager\\_ChooseGenre.cshtml* file with the following:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample2.cshtml)]

<span data-ttu-id="36808-121">První řádek deklaruje, že předáváme v `Album` jako náš model, přesně stejný příkaz modelu, který byl nalezen v zobrazení vytvořit.</span><span class="sxs-lookup"><span data-stu-id="36808-121">The first line declares that we are passing in an `Album` as our model, exactly the same model statement found in the Create view.</span></span> <span data-ttu-id="36808-122">Na následujících několika řádcích jsou značky pomocníka **popisku** .</span><span class="sxs-lookup"><span data-stu-id="36808-122">The next few lines are the **Label** helper markup.</span></span> <span data-ttu-id="36808-123">Další řádek je pomocné volání **DropDownList** , stejně jako v původním zobrazení pro vytváření.</span><span class="sxs-lookup"><span data-stu-id="36808-123">The next line is the **DropDownList** helper call, exactly the same as in the original Create view.</span></span> <span data-ttu-id="36808-124">Další řádek přidá odkaz s názvem `Add New Genre`a vytvoří styly jako tlačítko.</span><span class="sxs-lookup"><span data-stu-id="36808-124">The next line adds a link with the name `Add New Genre`, and styles it like a button.</span></span> <span data-ttu-id="36808-125">Řádek obsahující `ValidationMessageFor` se kopíruje přímo ze zobrazení pro vytváření.</span><span class="sxs-lookup"><span data-stu-id="36808-125">The line containing `ValidationMessageFor` is copied directly from the Create view.</span></span> <span data-ttu-id="36808-126">Následující řádky:</span><span class="sxs-lookup"><span data-stu-id="36808-126">The following lines:</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample3.html)]

<span data-ttu-id="36808-127">Vytvoří skrytý div s ID `genreDialog`.</span><span class="sxs-lookup"><span data-stu-id="36808-127">creates a hidden div, with the ID of `genreDialog`.</span></span> <span data-ttu-id="36808-128">Pomocí jQuery se v tomto div připojíme do dialogového okna **Přidat Žánr** s ID `genreDialog`.</span><span class="sxs-lookup"><span data-stu-id="36808-128">We will use jQuery to hook up our **Add Genre** dialog box with the ID `genreDialog` in this div.</span></span> <span data-ttu-id="36808-129">Poslední dva značky skriptu obsahují odkazy na soubory JavaScriptu, které budeme používat k implementaci funkce Přidat nový žánr.</span><span class="sxs-lookup"><span data-stu-id="36808-129">The last two script tags contain links to the JavaScript files we will use to implement the add new genre feature.</span></span> <span data-ttu-id="36808-130">Soubor */Scripts/chooseGenre.js* je k dispozici v projektu a podíváme se na něj později v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="36808-130">The */Scripts/chooseGenre.js* file is provided for you in the project, we will examine it later in the tutorial.</span></span>

<span data-ttu-id="36808-131">Spusťte aplikaci a klikněte na tlačítko **Přidat nový žánr** .</span><span class="sxs-lookup"><span data-stu-id="36808-131">Run the application and click on the **Add New Genre** button.</span></span> <span data-ttu-id="36808-132">V dialogovém okně **Přidat Žánr** zadejte do vstupního pole **název** **Opera** .</span><span class="sxs-lookup"><span data-stu-id="36808-132">In the **Add Genre** dialog box, enter **Opera** in the **Name** input box.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image4.png)

<span data-ttu-id="36808-133">Klikněte na tlačítko **Uložit**.</span><span class="sxs-lookup"><span data-stu-id="36808-133">Click the **Save** button.</span></span> <span data-ttu-id="36808-134">Volání jazyka AJAX vytvoří kategorii Opera a potom naplní rozevírací seznam pomocí nástroje Opera a nastaví Opera jako vybraný Žánr.</span><span class="sxs-lookup"><span data-stu-id="36808-134">An AJAX call creates the Opera category and then populates the dropdown list with Opera, and sets Opera as the selected genre.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image5.png)

<span data-ttu-id="36808-135">Zadejte jméno interpreta, název a cenu a pak vyberte tlačítko **vytvořit** .</span><span class="sxs-lookup"><span data-stu-id="36808-135">Enter an artist, title and price, then select the **Create** button.</span></span> <span data-ttu-id="36808-136">Pokud zadáte cenu menší než $8,99, nové album se zobrazí v horní části zobrazení indexu.</span><span class="sxs-lookup"><span data-stu-id="36808-136">If you enter a price less than $8.99, the new album will appear at the top of the Index view.</span></span> <span data-ttu-id="36808-137">Ověřte, že se nová položka alba uložila do databáze.</span><span class="sxs-lookup"><span data-stu-id="36808-137">Verify the new album entry was saved in the database.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image6.png)

<span data-ttu-id="36808-138">Zkuste vytvořit nový žánr s pouze jedním písmenem.</span><span class="sxs-lookup"><span data-stu-id="36808-138">Try creating a new genre with only one letter.</span></span> <span data-ttu-id="36808-139">Následující kód v souboru *Models\Genre.cs* nastaví minimální a maximální délku názvu žánru.</span><span class="sxs-lookup"><span data-stu-id="36808-139">The following code in the *Models\Genre.cs* file sets the minimum and maximum length of the genre name.</span></span>

[!code-csharp[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample4.cs)]

<span data-ttu-id="36808-140">Sestavy ověřování na straně klienta je nutné zadat řetězec o 2 až 20 znacích.</span><span class="sxs-lookup"><span data-stu-id="36808-140">Client side validation reports you must enter a string between 2 and 20 characters.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image7.png)

### <a name="examining-how-a-new-genre-is-added-to-the-database-and-the-select-list"></a><span data-ttu-id="36808-141">Zkoumání toho, jak se do databáze a seznamu pro výběr přidá nový žánr.</span><span class="sxs-lookup"><span data-stu-id="36808-141">Examining How a New Genre is Added to the Database and the Select List.</span></span>

<span data-ttu-id="36808-142">Otevřete soubor *Scripts\chooseGenre.js* a Projděte si kód.</span><span class="sxs-lookup"><span data-stu-id="36808-142">Open the *Scripts\chooseGenre.js* file and examine the code.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample5.js)]

<span data-ttu-id="36808-143">Druhý řádek používá ID `genreDialog` k vytvoření dialogového okna na značce DIV v souboru *\\_ChooseGenre. cshtml pro Views\StoreManager* .</span><span class="sxs-lookup"><span data-stu-id="36808-143">The second line uses the ID `genreDialog` to create a dialog box on the div tag in the *Views\StoreManager\\_ChooseGenre.cshtml* file.</span></span> <span data-ttu-id="36808-144">Většina pojmenovaných parametrů je vysvětlivekná.</span><span class="sxs-lookup"><span data-stu-id="36808-144">Most of the named parameters are self explanatory.</span></span> <span data-ttu-id="36808-145">Parametr `autoOpen` je nastaven na hodnotu false. Kliknutím na tlačítko **vytvořit Žánr** otevřete dialog explicitně (Tento postup je popsán v tématu).</span><span class="sxs-lookup"><span data-stu-id="36808-145">The `autoOpen` parameter is set to false, selecting the **Create Genre** button will open the dialogue explicitly (this is described latter on).</span></span> <span data-ttu-id="36808-146">Dialogové okno obsahuje dvě tlačítka, **Uložit** a **Zrušit**.</span><span class="sxs-lookup"><span data-stu-id="36808-146">The dialog has two buttons, **Save** and **Cancel**.</span></span> <span data-ttu-id="36808-147">Tlačítko **Storno** zavře dialogové okno.</span><span class="sxs-lookup"><span data-stu-id="36808-147">The **Cancel** button closes the dialog.</span></span> <span data-ttu-id="36808-148">Následující kód ukazuje funkci tlačítko **Uložit** .</span><span class="sxs-lookup"><span data-stu-id="36808-148">The following code shows the **Save** button function.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample6.js)]

<span data-ttu-id="36808-149">`var createGenreForm` se vybere z ID `createGenreForm`.</span><span class="sxs-lookup"><span data-stu-id="36808-149">The `var createGenreForm` is selected from the `createGenreForm` ID.</span></span> <span data-ttu-id="36808-150">ID `createGenreForm` bylo nastaveno v následujícím kódu, který byl nalezen v souboru *Views\Genre\\_CreateGenre. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="36808-150">The `createGenreForm` ID was set in the following code found in the *Views\Genre\\_CreateGenre.cshtml* file.</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample7.cshtml)]

<span data-ttu-id="36808-151">Přetížení pomocné rutiny [HTML. BeginForm](https://msdn.microsoft.com/library/dd492714.aspx) použité v souboru *Views\Genre\\_CreateGenre. cshtml* generuje HTML pomocí atributu Action obsahujícího adresu URL pro odeslání formuláře.</span><span class="sxs-lookup"><span data-stu-id="36808-151">The [Html.BeginForm](https://msdn.microsoft.com/library/dd492714.aspx) helper overload used in the *Views\Genre\\_CreateGenre.cshtml* file generates HTML with an action attribute containing the URL to submit the form.</span></span> <span data-ttu-id="36808-152">Můžete to vidět tak, že v prohlížeči zobrazíte stránku vytvořit album a v prohlížeči vyberete Zobrazit zdroj.</span><span class="sxs-lookup"><span data-stu-id="36808-152">You can see this by displaying the create album page in a browser and selecting show source in the browser.</span></span> <span data-ttu-id="36808-153">Následující kód ukazuje generovaný kód HTML obsahující značku formuláře.</span><span class="sxs-lookup"><span data-stu-id="36808-153">The following markup shows the generated HTML containing the form tag.</span></span>

[!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample8.html)]

<span data-ttu-id="36808-154">Řádek jQuery `$.post` vytvoří volání jazyka AJAX do atributu Action (`/StoreManager/Create`) a předá data z dialogového okna **vytvořit Žánr** .</span><span class="sxs-lookup"><span data-stu-id="36808-154">The jQuery `$.post` line makes an AJAX call to the action attribute (`/StoreManager/Create`) and passes in the data from the **Create Genre** dialog box.</span></span> <span data-ttu-id="36808-155">Data se skládají z názvu nového žánru a volitelného popisu.</span><span class="sxs-lookup"><span data-stu-id="36808-155">The data consists of the name for the new genre and an optional description.</span></span> <span data-ttu-id="36808-156">Pokud je volání jazyka AJAX úspěšné, je nový název a hodnota žánru přidány do značky Select a nový žánr je nastaven na vybranou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="36808-156">If the AJAX call is successful, the new genre name and value are added to the Select markup, and the new genre is set to the selected value.</span></span> <span data-ttu-id="36808-157">Vzhledem k tomu, že se jedná o dynamicky generované značky, nemůžete zobrazit novou možnost vybrat zobrazením zdroje v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="36808-157">Because this is dynamically generated markup, you can't see the new select option by viewing the source in the browser.</span></span> <span data-ttu-id="36808-158">Nový kód HTML můžete zobrazit pomocí vývojářských nástrojů IE 9 F12.</span><span class="sxs-lookup"><span data-stu-id="36808-158">You can see the new HTML with the IE 9 F12 developer tools.</span></span> <span data-ttu-id="36808-159">Chcete-li zobrazit novou možnost výběru v aplikaci Internet Explorer 9, stiskněte klávesu F12 a spusťte nástroje pro vývojáře F12.</span><span class="sxs-lookup"><span data-stu-id="36808-159">To view the new select option, in Internet Explorer 9, hit the F12 key to start the F12 developer tools.</span></span> <span data-ttu-id="36808-160">Přejděte na stránku vytvořit a přidejte nový žánr, aby byl nový žánr vybrán v seznamu Výběr žánru.</span><span class="sxs-lookup"><span data-stu-id="36808-160">Navigate to the Create page and add a new genre so the new genre is selected in the genre select list.</span></span> <span data-ttu-id="36808-161">V vývojářských nástrojích F12:</span><span class="sxs-lookup"><span data-stu-id="36808-161">In the F12 developer tools:</span></span>

1. <span data-ttu-id="36808-162">Vyberte kartu HTML.</span><span class="sxs-lookup"><span data-stu-id="36808-162">Select the HTML tab.</span></span>
2. <span data-ttu-id="36808-163">Stiskněte ikonu aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="36808-163">Hit the refresh icon.</span></span>  
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image8.png)
3. <span data-ttu-id="36808-164">Do vyhledávacího pole zadejte GenreID.</span><span class="sxs-lookup"><span data-stu-id="36808-164">In the search box, enter GenreID.</span></span>
4. <span data-ttu-id="36808-165">Pomocí ikony další</span><span class="sxs-lookup"><span data-stu-id="36808-165">Using the next icon,</span></span>   
    ![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image9.png)  
   <span data-ttu-id="36808-166">přejděte k následující značce SELECT:</span><span class="sxs-lookup"><span data-stu-id="36808-166">navigate to the following select tag:</span></span>

    [!code-html[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample9.html)]
5. <span data-ttu-id="36808-167">Rozbalte hodnotu poslední možnosti.</span><span class="sxs-lookup"><span data-stu-id="36808-167">Expand the last option value.</span></span>

![](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/_static/image10.png)

<span data-ttu-id="36808-168">Následující kód v souboru *Scripts\chooseGenre.js* ukazuje, jak se tlačítko **Přidat nový žánr** připojí k události Click a jak se vytvoří dialogové okno **Přidat nový žánr** .</span><span class="sxs-lookup"><span data-stu-id="36808-168">The following code in the *Scripts\chooseGenre.js* file shows the how the **Add New Genre** button gets connected to the click event, and how the **Add New Genre** dialog box is created.</span></span>

[!code-javascript[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample10.js)]

<span data-ttu-id="36808-169">První řádek vytvoří funkci Click připojenou k tlačítku **Přidat nový žánr** .</span><span class="sxs-lookup"><span data-stu-id="36808-169">The first line creates a click function attached to the **Add New Genre** button.</span></span> <span data-ttu-id="36808-170">Následující kód ze souboru Views\StoreManager\\_ChooseGenre. cshtml ukazuje, jak se vytvoří tlačítko **Přidat nový žánr** :</span><span class="sxs-lookup"><span data-stu-id="36808-170">The following markup from the Views\StoreManager\\_ChooseGenre.cshtml file shows how the **Add New Genre** button is created:</span></span>

[!code-cshtml[Main](adding-a-new-category-to-the-dropdownlist-using-jquery-ui/samples/sample11.cshtml)]

<span data-ttu-id="36808-171">Metoda load vytvoří a otevře dialog Přidat Žánr a zavolá metodu jQuery `parse`, aby k ověřování klienta došlo na datech zadaných v dialogovém okně.</span><span class="sxs-lookup"><span data-stu-id="36808-171">The load method creates and opens the Add Genre dialog and calls the jQuery `parse` method so client validation occurs on data entered in the dialog.</span></span>

<span data-ttu-id="36808-172">V této části jste se naučili, jak vytvořit dialog, který se dá použít k přidání nových dat kategorie do seznamu SELECT.</span><span class="sxs-lookup"><span data-stu-id="36808-172">In this section you have learned how to create a dialog that can be used to add new category data to a select list.</span></span> <span data-ttu-id="36808-173">Stejný postup můžete použít k vytvoření uživatelského rozhraní pro přidání nového interpreta do seznamu pro výběr interpretu.</span><span class="sxs-lookup"><span data-stu-id="36808-173">You can follow the same procedure to create UI to add a new artist to the artist select list.</span></span> <span data-ttu-id="36808-174">V tomto kurzu máte přehled o tom, jak pracovat s ovládacím prvkem pro **NÁPOVĚDU HTML**ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="36808-174">This tutorial has given an overview of working with the ASP.NET MVC HTML helper **DropDownList**.</span></span> <span data-ttu-id="36808-175">Další informace o práci s **DropDownList**najdete v části Přidání odkazů níže.</span><span class="sxs-lookup"><span data-stu-id="36808-175">For additional information on working with the **DropDownList**, see the addition references section below.</span></span> <span data-ttu-id="36808-176">Pokud je tento kurz užitečný, dejte nám prosím jistotu.</span><span class="sxs-lookup"><span data-stu-id="36808-176">Please let us know if this tutorial has been helpful.</span></span>

<span data-ttu-id="36808-177">Rick. Anderson [at] Microsoft. com</span><span class="sxs-lookup"><span data-stu-id="36808-177">Rick.Anderson[at]Microsoft.com</span></span>

### <a name="additional-references"></a><span data-ttu-id="36808-178">Další odkazy</span><span class="sxs-lookup"><span data-stu-id="36808-178">Additional References</span></span>

- <span data-ttu-id="36808-179">[ASP.NET MVC – tento kurz – kaskádové rozevírací seznamy –](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) [radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)</span><span class="sxs-lookup"><span data-stu-id="36808-179">[ASP.NET MVC–Cascading Dropdown Lists Tutorial](https://weblogs.asp.net/raduenuca/archive/2011/03/06/asp-net-mvc-cascading-dropdown-lists-tutorial-part-1-defining-the-problem-and-the-context.aspx) by [Radu Enuca](https://weblogs.asp.net/raduenuca/default.aspx)</span></span>
- <span data-ttu-id="36808-180">[Zvolené](https://harvesthq.github.com/chosen/) Modul plug-in JavaScriptu, který podporuje vícenásobné výběry a filtrování.</span><span class="sxs-lookup"><span data-stu-id="36808-180">[Chosen](https://harvesthq.github.com/chosen/) A JavaScript plugin that support multi-select and filtering.</span></span>

### <a name="contributors"></a><span data-ttu-id="36808-181">Přispěvatelé</span><span class="sxs-lookup"><span data-stu-id="36808-181">Contributors</span></span>

- [<span data-ttu-id="36808-182">Radu Enuca</span><span class="sxs-lookup"><span data-stu-id="36808-182">Radu Enuca</span></span>](https://weblogs.asp.net/raduenuca/default.aspx)
- <span data-ttu-id="36808-183">Jean-Sébastien Goupil</span><span class="sxs-lookup"><span data-stu-id="36808-183">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="36808-184">Brad Wilson</span><span class="sxs-lookup"><span data-stu-id="36808-184">Brad Wilson</span></span>](http://bradwilson.typepad.com/)

### <a name="reviewers"></a><span data-ttu-id="36808-185">Recenzenti</span><span class="sxs-lookup"><span data-stu-id="36808-185">Reviewers</span></span>

- <span data-ttu-id="36808-186">Jean-Sébastien Goupil</span><span class="sxs-lookup"><span data-stu-id="36808-186">Jean-Sébastien Goupil</span></span>
- [<span data-ttu-id="36808-187">Brad Wilson</span><span class="sxs-lookup"><span data-stu-id="36808-187">Brad Wilson</span></span>](http://bradwilson.typepad.com/)
- <span data-ttu-id="36808-188">Mike Pope</span><span class="sxs-lookup"><span data-stu-id="36808-188">Mike Pope</span></span>
- <span data-ttu-id="36808-189">Dykstra</span><span class="sxs-lookup"><span data-stu-id="36808-189">Tom Dykstra</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="36808-190">Předchozí</span><span class="sxs-lookup"><span data-stu-id="36808-190">Previous</span></span>](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)

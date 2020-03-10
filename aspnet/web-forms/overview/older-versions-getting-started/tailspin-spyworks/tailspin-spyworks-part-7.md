---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
title: '7\. část: Přidání funkcí | Microsoft Docs'
author: JoeStagner
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 7 přidává další funkce, jako je například účet revie...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 50223ee9-11b9-4cf3-bca2-e2f10bf471f3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-7
msc.type: authoredcontent
ms.openlocfilehash: ffd2b862c727db9572c272b7b21bcc33c822fffa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641993"
---
# <a name="part-7-adding-features"></a><span data-ttu-id="81ac4-104">7\. část: Přidání funkcí</span><span class="sxs-lookup"><span data-stu-id="81ac4-104">Part 7: Adding Features</span></span>

<span data-ttu-id="81ac4-105">[Jana Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="81ac4-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="81ac4-106">Tailspin Spyworks ukazuje, jak neobyčejně jednoduché je vytvářet výkonné a škálovatelné aplikace pro platformu .NET.</span><span class="sxs-lookup"><span data-stu-id="81ac4-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="81ac4-107">Ukazuje, jak používat Skvělé nové funkce v ASP.NET 4 k vytvoření online obchodu, včetně nákupu, rezervace a správy.</span><span class="sxs-lookup"><span data-stu-id="81ac4-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="81ac4-108">V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="81ac4-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="81ac4-109">Část 7 přidává další funkce, jako je třeba revize účtu, revize produktů a "Oblíbené položky" a také zakoupené uživatelské ovládací prvky.</span><span class="sxs-lookup"><span data-stu-id="81ac4-109">Part 7 adds additional features, such as account review, product reviews, and "popular items" and "also purchased" user controls.</span></span>

## <a id="_Toc260221673"></a><span data-ttu-id="81ac4-110">Přidávání funkcí</span><span class="sxs-lookup"><span data-stu-id="81ac4-110">Adding Features</span></span>

<span data-ttu-id="81ac4-111">I když mohou uživatelé procházet náš katalog, umístit položky do svého nákupního košíku a dokončit proces registrace, bude k dispozici celá řada pomocných funkcí, které budeme použít pro zlepšení našeho webu.</span><span class="sxs-lookup"><span data-stu-id="81ac4-111">Though users can browse our catalog, place items in their shopping cart, and complete the checkout process, there are a number of supporting features that we will include to improve our site.</span></span>

1. <span data-ttu-id="81ac4-112">Recenze účtu (jsou umístěné objednávky seznamu a zobrazí podrobnosti.)</span><span class="sxs-lookup"><span data-stu-id="81ac4-112">Account Review (List orders placed and view details.)</span></span>
2. <span data-ttu-id="81ac4-113">Přidejte nějaký konkrétní kontextový obsah na Front-Page.</span><span class="sxs-lookup"><span data-stu-id="81ac4-113">Add some context specific content to the front page.</span></span>
3. <span data-ttu-id="81ac4-114">Přidejte funkci, která uživatelům umožní zkontrolovat produkty v katalogu.</span><span class="sxs-lookup"><span data-stu-id="81ac4-114">Add a feature to let users Review the products in the catalog.</span></span>
4. <span data-ttu-id="81ac4-115">Vytvoření uživatelského ovládacího prvku pro zobrazení oblíbených položek a umístění tohoto ovládacího prvku na přední stránku.</span><span class="sxs-lookup"><span data-stu-id="81ac4-115">Create a User Control to display Popular Items and Place that control on the front page.</span></span>
5. <span data-ttu-id="81ac4-116">Vytvořte uživatelský ovládací prvek "také koupené" a přidejte jej na stránku s podrobnostmi o produktu.</span><span class="sxs-lookup"><span data-stu-id="81ac4-116">Create an "Also Purchased" user control and add it to the product details page.</span></span>
6. <span data-ttu-id="81ac4-117">Přidejte stránku kontaktu.</span><span class="sxs-lookup"><span data-stu-id="81ac4-117">Add a Contact Page.</span></span>
7. <span data-ttu-id="81ac4-118">Přidejte stránku About.</span><span class="sxs-lookup"><span data-stu-id="81ac4-118">Add an About Page.</span></span>
8. <span data-ttu-id="81ac4-119">Globální chyba</span><span class="sxs-lookup"><span data-stu-id="81ac4-119">Global Error</span></span>

## <a id="_Toc260221674"></a><span data-ttu-id="81ac4-120">Revize účtu</span><span class="sxs-lookup"><span data-stu-id="81ac4-120">Account Review</span></span>

<span data-ttu-id="81ac4-121">Ve složce Account (účet) vytvořte dvě stránky ASPX One s názvem OrderList. aspx a druhou s názvem OrderDetails. aspx.</span><span class="sxs-lookup"><span data-stu-id="81ac4-121">In the "Account" folder create two .aspx pages one named OrderList.aspx and the other named OrderDetails.aspx</span></span>

<span data-ttu-id="81ac4-122">OrderList. aspx bude využívat ovládací prvky GridView a EntityDataSource, podobně jako v minulosti.</span><span class="sxs-lookup"><span data-stu-id="81ac4-122">OrderList.aspx will leverage the GridView and EntityDataSource controls much as we have previously.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample1.aspx)]

<span data-ttu-id="81ac4-123">EntityDataSource vybere záznamy z tabulky Orders filtrované podle uživatelského jména (viz WhereParameter), kterou nastavíme v proměnné relace, když se přihlásí uživatel.</span><span class="sxs-lookup"><span data-stu-id="81ac4-123">The EntityDataSource selects records from the Orders table filtered on the UserName (see the WhereParameter) which we set in a session variable when the user log's in.</span></span>

<span data-ttu-id="81ac4-124">Všimněte si také těchto parametrů v HyperlinkField ovládacího prvku GridView:</span><span class="sxs-lookup"><span data-stu-id="81ac4-124">Note also these parameters in the HyperlinkField of the GridView:</span></span>

[!code-xml[Main](tailspin-spyworks-part-7/samples/sample2.xml)]

<span data-ttu-id="81ac4-125">Tyto údaje určují odkaz na zobrazení podrobností objednávky pro každý produkt, který určuje pole ČísloObjednávky jako parametr QueryString na stránce OrderDetails. aspx.</span><span class="sxs-lookup"><span data-stu-id="81ac4-125">These specify the link to the Order details view for each product specifying the OrderID field as a QueryString parameter to the OrderDetails.aspx page.</span></span>

## <a id="_Toc260221675"></a><span data-ttu-id="81ac4-126">OrderDetails. aspx</span><span class="sxs-lookup"><span data-stu-id="81ac4-126">OrderDetails.aspx</span></span>

<span data-ttu-id="81ac4-127">Použijeme ovládací prvek EntityDataSource pro přístup k objednávkám a FormView k zobrazení dat objednávek a dalšího objektu EntityDataSource s prvkem GridView k zobrazení všech položek řádku objednávky.</span><span class="sxs-lookup"><span data-stu-id="81ac4-127">We will use an EntityDataSource control to access the Orders and a FormView to display the Order data and another EntityDataSource with a GridView to display all the Order's line items.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample3.aspx)]

<span data-ttu-id="81ac4-128">V souboru kódu na pozadí (OrderDetails.aspx.cs) máme dvě trochu bitů údržbu.</span><span class="sxs-lookup"><span data-stu-id="81ac4-128">In the Code Behind file (OrderDetails.aspx.cs) we have two little bits of housekeeping.</span></span>

<span data-ttu-id="81ac4-129">Nejdřív je potřeba zajistit, aby OrderDetails vždy získává ČísloObjednávky.</span><span class="sxs-lookup"><span data-stu-id="81ac4-129">First we need to make sure that OrderDetails always gets an OrderId.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample4.cs)]

<span data-ttu-id="81ac4-130">Také je potřeba vypočítat a zobrazit celkový součet z položek řádků.</span><span class="sxs-lookup"><span data-stu-id="81ac4-130">We also need to calculate and display the order total from the line items.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample5.cs)]

## <a id="_Toc260221676"></a><span data-ttu-id="81ac4-131">Domovská stránka</span><span class="sxs-lookup"><span data-stu-id="81ac4-131">The Home Page</span></span>

<span data-ttu-id="81ac4-132">Pojďme na stránku Default. aspx přidat nějaký statický obsah.</span><span class="sxs-lookup"><span data-stu-id="81ac4-132">Let's add some static content to the Default.aspx page.</span></span>

<span data-ttu-id="81ac4-133">Nejprve vytvořím složku Content (obsah) a v ní složku images (a přidám obrázek, který se má použít na domovské stránce.)</span><span class="sxs-lookup"><span data-stu-id="81ac4-133">First I'll create a "Content" folder and within it an Images folder (and I'll include an image to be used on the home page.)</span></span>

<span data-ttu-id="81ac4-134">Do dolního zástupného znaku stránky default. aspx přidejte následující kód.</span><span class="sxs-lookup"><span data-stu-id="81ac4-134">Into the bottom placeholder of the Default.aspx page, add the following markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample6.aspx)]

## <a id="_Toc260221677"></a><span data-ttu-id="81ac4-135">Recenze produktů</span><span class="sxs-lookup"><span data-stu-id="81ac4-135">Product Reviews</span></span>

<span data-ttu-id="81ac4-136">Nejprve přidáme tlačítko s odkazem na formulář, který můžeme použít k zadání revize produktu.</span><span class="sxs-lookup"><span data-stu-id="81ac4-136">First we'll add a button with a link to a form that we can use to enter a product review.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample7.aspx)]

![](tailspin-spyworks-part-7/_static/image1.jpg)

<span data-ttu-id="81ac4-137">Všimněte si, že do řetězce dotazu předáváme ProductID.</span><span class="sxs-lookup"><span data-stu-id="81ac4-137">Note that we are passing the ProductID in the query string</span></span>

<span data-ttu-id="81ac4-138">Nyní přidáme stránku s názvem ReviewAdd. aspx.</span><span class="sxs-lookup"><span data-stu-id="81ac4-138">Next let's add page named ReviewAdd.aspx</span></span>

<span data-ttu-id="81ac4-139">Tato stránka bude používat ASP.NET AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="81ac4-139">This page will use the ASP.NET AJAX Control Toolkit.</span></span> <span data-ttu-id="81ac4-140">Pokud jste to ještě neudělali, můžete si ho stáhnout z [DevExpress](http://devexpress.com/act) a k instalaci sady Toolkit pro použití se sadou Visual Studio zde [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md)použít pokyny.</span><span class="sxs-lookup"><span data-stu-id="81ac4-140">If you have not already done so you can download it from [DevExpress](http://devexpress.com/act) and there is guidance on setting up the toolkit for use with Visual Studio here [https://www.asp.net/learn/ajax-videos/video-76.aspx](../../../videos/ajax-control-toolkit/how-do-i-get-started-with-the-aspnet-ajax-control-toolkit.md).</span></span>

<span data-ttu-id="81ac4-141">V režimu návrhu přetáhněte ovládací prvky a validátory ze sady nástrojů a sestavte formulář jako ten níže.</span><span class="sxs-lookup"><span data-stu-id="81ac4-141">In design mode, drag controls and validators from the toolbox and build a form like the one below.</span></span>

![](tailspin-spyworks-part-7/_static/image2.jpg)

<span data-ttu-id="81ac4-142">Označení bude vypadat přibližně takto.</span><span class="sxs-lookup"><span data-stu-id="81ac4-142">The markup will look something like this.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample8.aspx)]

<span data-ttu-id="81ac4-143">Teď, když můžeme zadat recenze, umožňuje zobrazit tyto recenze na stránce produktu.</span><span class="sxs-lookup"><span data-stu-id="81ac4-143">Now that we can enter reviews, lets display those reviews on the product page.</span></span>

<span data-ttu-id="81ac4-144">Přidejte tento kód na stránku ProductDetails. aspx.</span><span class="sxs-lookup"><span data-stu-id="81ac4-144">Add this markup to the ProductDetails.aspx page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample9.aspx)]

<span data-ttu-id="81ac4-145">Po spuštění naší aplikace a přechodu na produkt se zobrazí informace o produktu, včetně revizí zákazníků.</span><span class="sxs-lookup"><span data-stu-id="81ac4-145">Running our application now and navigating to a product shows the product information including customer reviews.</span></span>

![](tailspin-spyworks-part-7/_static/image3.jpg)

## <a id="_Toc260221678"></a><span data-ttu-id="81ac4-146">Ovládací prvek oblíbených položek (vytváření uživatelských ovládacích prvků)</span><span class="sxs-lookup"><span data-stu-id="81ac4-146">Popular Items Control (Creating User Controls)</span></span>

<span data-ttu-id="81ac4-147">Aby bylo možné zvýšit prodej na vašem webu, přidáme několik funkcí do oblíbených nebo souvisejících produktů v sugestivní prodeji.</span><span class="sxs-lookup"><span data-stu-id="81ac4-147">In order to increase sales on your web site we will add a couple of features to "suggestive sell" popular or related products.</span></span>

<span data-ttu-id="81ac4-148">První z těchto funkcí bude seznam oblíbených produktů v našem katalogu produktů.</span><span class="sxs-lookup"><span data-stu-id="81ac4-148">The first of these features will be a list of the more popular product in our product catalog.</span></span>

<span data-ttu-id="81ac4-149">Vytvoříme "uživatelský ovládací prvek", na kterém se zobrazí hlavní položky prodeje na domovské stránce naší aplikace.</span><span class="sxs-lookup"><span data-stu-id="81ac4-149">We will create a "User Control" to display the top selling items on the home page of our application.</span></span> <span data-ttu-id="81ac4-150">Vzhledem k tomu, že se jedná o ovládací prvek, můžeme ho použít na libovolné stránce pouhým přetažením ovládacího prvku v návrháři aplikace Visual Studio na libovolnou stránku, kterou se vám líbí.</span><span class="sxs-lookup"><span data-stu-id="81ac4-150">Since this will be a control, we can use it on any page by simply dragging and dropping the control in Visual Studio's designer onto any page that we like.</span></span>

<span data-ttu-id="81ac4-151">V Průzkumníku řešení sady Visual Studio klikněte pravým tlačítkem myši na název řešení a vytvořte nový adresář s názvem Controls.</span><span class="sxs-lookup"><span data-stu-id="81ac4-151">In Visual Studio's solutions explorer, right-click on the solution name and create a new directory named "Controls".</span></span> <span data-ttu-id="81ac4-152">I když to není nutné, pomůžeme uchovávat náš projekt tak, že se vytvoří všechny naše uživatelské ovládací prvky v adresáři Controls.</span><span class="sxs-lookup"><span data-stu-id="81ac4-152">While it is not necessary to do so, we will help keep our project organized by creating all our user controls in the "Controls" directory.</span></span>

<span data-ttu-id="81ac4-153">Klikněte pravým tlačítkem na složku ovládací prvky a vyberte možnost Nová položka:</span><span class="sxs-lookup"><span data-stu-id="81ac4-153">Right-click on the controls folder and choose "New Item" :</span></span>

![](tailspin-spyworks-part-7/_static/image4.jpg)

<span data-ttu-id="81ac4-154">Zadejte název pro náš ovládací prvek "PopularItems".</span><span class="sxs-lookup"><span data-stu-id="81ac4-154">Specify a name for our control of "PopularItems".</span></span> <span data-ttu-id="81ac4-155">Všimněte si, že Přípona souboru pro uživatelské ovládací prvky je. ascx není. aspx.</span><span class="sxs-lookup"><span data-stu-id="81ac4-155">Note that the file extension for user controls is .ascx not .aspx.</span></span>

<span data-ttu-id="81ac4-156">Naše oblíbené položky uživatelský ovládací prvek bude definován následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="81ac4-156">Our Popular Items User control will be defined as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample10.aspx)]

<span data-ttu-id="81ac4-157">Tady používáme metodu, kterou v této aplikaci zatím nepoužíváme.</span><span class="sxs-lookup"><span data-stu-id="81ac4-157">Here we're using a method we have not used yet in this application.</span></span> <span data-ttu-id="81ac4-158">Používáme ovládací prvek Repeater a místo použití ovládacího prvku zdroje dat zavazujeme ovládací prvek Repeater s výsledky LINQ to Entitiesho dotazu.</span><span class="sxs-lookup"><span data-stu-id="81ac4-158">We're using the repeater control and instead of using a data source control we're binding the Repeater Control to the results of a LINQ to Entities query.</span></span>

<span data-ttu-id="81ac4-159">V kódu na pozadí našeho ovládacího prvku máme následující postup.</span><span class="sxs-lookup"><span data-stu-id="81ac4-159">In the code behind of our control we do that as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample11.cs)]

<span data-ttu-id="81ac4-160">Všimněte si také tohoto důležitého řádku v horní části kódu našeho ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="81ac4-160">Note also this important line at the top of our control's markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample12.aspx)]

<span data-ttu-id="81ac4-161">Vzhledem k tomu, že se Nejoblíbenější položky nemění na základě minut na minuty, můžeme přidat direktivu Aching pro zlepšení výkonu naší aplikace.</span><span class="sxs-lookup"><span data-stu-id="81ac4-161">Since the most popular items won't be changing on a minute to minute basis we can add a aching directive to improve the performance of our application.</span></span> <span data-ttu-id="81ac4-162">Tato direktiva způsobí, že bude kód ovládacího prvku proveden pouze v případě, že vyprší výstup v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="81ac4-162">This directive will cause the controls code to only be executed when the cached output of the control expires.</span></span> <span data-ttu-id="81ac4-163">V opačném případě se použije verze výstupu ovládacího prvku v mezipaměti.</span><span class="sxs-lookup"><span data-stu-id="81ac4-163">Otherwise, the cached version of the control's output will be used.</span></span>

<span data-ttu-id="81ac4-164">Vše, co je potřeba udělat, je vše, co je náš nový ovládací prvek na naší stránce Default. aspx.</span><span class="sxs-lookup"><span data-stu-id="81ac4-164">Now all we have to do is include our new control in our Default.aspx page.</span></span>

<span data-ttu-id="81ac4-165">Pomocí přetažení umístěte instanci ovládacího prvku do otevřeného sloupce našeho výchozího formuláře.</span><span class="sxs-lookup"><span data-stu-id="81ac4-165">Use drag and drop to place an instance of the control in the open column of our Default form.</span></span>

![](tailspin-spyworks-part-7/_static/image5.jpg)

<span data-ttu-id="81ac4-166">Když teď spustíme naši aplikaci, zobrazí se na domovské stránce Nejoblíbenější položky.</span><span class="sxs-lookup"><span data-stu-id="81ac4-166">Now when we run our application the home page displays the most popular items.</span></span>

![](tailspin-spyworks-part-7/_static/image6.jpg)

## <a id="_Toc260221679"></a><span data-ttu-id="81ac4-167">"Také koupený" ovládací prvek (uživatelské ovládací prvky s parametry)</span><span class="sxs-lookup"><span data-stu-id="81ac4-167">"Also Purchased" Control (User Controls with Parameters)</span></span>

<span data-ttu-id="81ac4-168">Druhý uživatelský ovládací prvek, který vytvoříme, bude přebírat sugestivní prodej na další úroveň přidáním kontextu kontextu.</span><span class="sxs-lookup"><span data-stu-id="81ac4-168">The second User Control that we'll create will take suggestive selling to the next level by adding context specificity.</span></span>

<span data-ttu-id="81ac4-169">Logika pro výpočet horních "také koupených" položek je netriviální.</span><span class="sxs-lookup"><span data-stu-id="81ac4-169">The logic to calculate the top "Also Purchased" items is non-trivial.</span></span>

<span data-ttu-id="81ac4-170">Náš "zakoupený" ovládací prvek vybírá záznamy OrderDetails (dříve koupené) pro aktuálně vybrané ProductID a přebírá ČísloObjednávky pro každé nalezené jedinečné pořadí.</span><span class="sxs-lookup"><span data-stu-id="81ac4-170">Our "Also Purchased" control will select the OrderDetails records (previously purchased) for the currently selected ProductID and grab the OrderIDs for each unique order that is found.</span></span>

<span data-ttu-id="81ac4-171">Pak z těchto objednávek vybereme možnost Al a nasadíme množství zakoupených produktů.</span><span class="sxs-lookup"><span data-stu-id="81ac4-171">Then we will select al the products from all those Orders and sum the quantities purchased.</span></span> <span data-ttu-id="81ac4-172">Produkty seřadíme podle tohoto množství součtu a zobrazíme prvních pět položek.</span><span class="sxs-lookup"><span data-stu-id="81ac4-172">We'll sort the products by that quantity sum and display the top five items.</span></span>

<span data-ttu-id="81ac4-173">S ohledem na složitost této logiky implementujeme tento algoritmus jako uloženou proceduru.</span><span class="sxs-lookup"><span data-stu-id="81ac4-173">Given the complexity of this logic, we will implement this algorithm as a stored procedure.</span></span>

<span data-ttu-id="81ac4-174">T-SQL pro uloženou proceduru je následující.</span><span class="sxs-lookup"><span data-stu-id="81ac4-174">The T-SQL for the stored procedure is as follows.</span></span>

[!code-sql[Main](tailspin-spyworks-part-7/samples/sample13.sql)]

<span data-ttu-id="81ac4-175">Všimněte si, že tato uložená procedura (SelectPurchasedWithProducts) existovala v databázi, když jsme ji zahrnuli do naší aplikace, a když jsme vygenerovali model EDM (Entity Data Model) jsme určili, že kromě tabulek a zobrazení, které potřebujeme, model EDM (Entity Data Model) by měla obsahovat tuto uloženou proceduru.</span><span class="sxs-lookup"><span data-stu-id="81ac4-175">Note that this stored procedure (SelectPurchasedWithProducts) existed in the database when we included it in our application and when we generated the Entity Data Model we specified that, in addition to the Tables and Views that we needed, the Entity Data Model should include this stored procedure.</span></span>

<span data-ttu-id="81ac4-176">Pro přístup k uložené proceduře z model EDM (Entity Data Model) musíme tuto funkci naimportovat.</span><span class="sxs-lookup"><span data-stu-id="81ac4-176">To access the stored procedure from the Entity Data Model we need to import the function.</span></span>

<span data-ttu-id="81ac4-177">Dvakrát klikněte na model EDM (Entity Data Model) v Průzkumníkovi řešení a otevřete ji v návrháři a otevřete prohlížeč modelů, potom klikněte pravým tlačítkem v návrháři a vyberte Přidat import funkce.</span><span class="sxs-lookup"><span data-stu-id="81ac4-177">Double Click on the Entity Data Model in the Solutions Explorer to open it in the designer and open the Model Browser, then right-click in the designer and select "Add Function Import".</span></span>

![](tailspin-spyworks-part-7/_static/image1.png)

<span data-ttu-id="81ac4-178">Tím se otevře dialogové okno.</span><span class="sxs-lookup"><span data-stu-id="81ac4-178">Doing so will open this dialog.</span></span>

![](tailspin-spyworks-part-7/_static/image2.png)

<span data-ttu-id="81ac4-179">Vyplňte pole, jak vidíte výše, vyberte "SelectPurchasedWithProducts" a použijte název procedury pro název naší importované funkce.</span><span class="sxs-lookup"><span data-stu-id="81ac4-179">Fill out the fields as you see above, selecting the "SelectPurchasedWithProducts" and use the procedure name for the name of our imported function.</span></span>

<span data-ttu-id="81ac4-180">Klikněte na OK.</span><span class="sxs-lookup"><span data-stu-id="81ac4-180">Click "Ok".</span></span>

<span data-ttu-id="81ac4-181">Díky tomu můžeme jednoduše programovat proti uložené proceduře, protože můžeme v modelu provést jinou položku.</span><span class="sxs-lookup"><span data-stu-id="81ac4-181">Having done this we can simply program against the stored procedure as we might any other item in the model.</span></span>

<span data-ttu-id="81ac4-182">Proto v naší "ovládacím prvku" Vytvořte nový uživatelský ovládací prvek s názvem AlsoPurchased. ascx.</span><span class="sxs-lookup"><span data-stu-id="81ac4-182">So, in our "Controls" folder create a new user control named AlsoPurchased.ascx.</span></span>

<span data-ttu-id="81ac4-183">Značky pro tento ovládací prvek budou vypadat velmi dobře s ovládacím prvkem PopularItems.</span><span class="sxs-lookup"><span data-stu-id="81ac4-183">The markup for this control will look very familiar to the PopularItems control.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample14.aspx)]

<span data-ttu-id="81ac4-184">Významný rozdíl je, že výstupy neukládají do mezipaměti, protože položka, která se má vykreslit, se liší podle produktu.</span><span class="sxs-lookup"><span data-stu-id="81ac4-184">The notable difference is that are not caching the output since the item's to be rendered will differ by product.</span></span>

<span data-ttu-id="81ac4-185">ProductId bude ovládacímu prvku "vlastnost".</span><span class="sxs-lookup"><span data-stu-id="81ac4-185">The ProductId will be a "property" to the control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample15.cs)]

<span data-ttu-id="81ac4-186">V obslužné rutině události PreRender ovládacího prvku jsme EED, že máme tři věci.</span><span class="sxs-lookup"><span data-stu-id="81ac4-186">In the control's PreRender event handler we eed to do three things.</span></span>

1. <span data-ttu-id="81ac4-187">Ujistěte se, že je ProductID nastaveno.</span><span class="sxs-lookup"><span data-stu-id="81ac4-187">Make sure the ProductID is set.</span></span>
2. <span data-ttu-id="81ac4-188">Podívejte se, jestli nejsou k dispozici žádné produkty zakoupené s aktuálním.</span><span class="sxs-lookup"><span data-stu-id="81ac4-188">See if there are any products that have been purchased with the current one.</span></span>
3. <span data-ttu-id="81ac4-189">Výstup některých položek určených v #2.</span><span class="sxs-lookup"><span data-stu-id="81ac4-189">Output some items as determined in #2.</span></span>

<span data-ttu-id="81ac4-190">Všimněte si, jak snadné je volat uloženou proceduru prostřednictvím modelu.</span><span class="sxs-lookup"><span data-stu-id="81ac4-190">Note how easy it is to call the stored procedure through the model.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample16.cs)]

<span data-ttu-id="81ac4-191">Až se rozhodnete, že se zakoupí také "zakoupíme", můžeme jednoduše navazovat Repeater na výsledky vrácené dotazem.</span><span class="sxs-lookup"><span data-stu-id="81ac4-191">After determining that there ARE "also purchased" we can simply bind the repeater to the results returned by the query.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample17.cs)]

<span data-ttu-id="81ac4-192">Pokud zde nejsou žádné "zakoupené" položky, jednoduše zobrazíme další oblíbené položky z našeho katalogu.</span><span class="sxs-lookup"><span data-stu-id="81ac4-192">If there were not any "also purchased" items we'll simply display other popular items from our catalog.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-7/samples/sample18.cs)]

<span data-ttu-id="81ac4-193">Chcete-li zobrazit "zakoupené" položky, otevřete stránku ProductDetails. aspx a přetáhněte ovládací prvek AlsoPurchased z Průzkumníku řešení tak, aby se zobrazil v této pozici ve značce.</span><span class="sxs-lookup"><span data-stu-id="81ac4-193">To view the "Also Purchased" items, open the ProductDetails.aspx page and drag the AlsoPurchased control from the Solutions Explorer so that it appears in this position in the markup.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample19.aspx)]

<span data-ttu-id="81ac4-194">Tím se vytvoří odkaz na ovládací prvek v horní části stránky ProductDetails.</span><span class="sxs-lookup"><span data-stu-id="81ac4-194">Doing so will create a reference to the control at the top of the ProductDetails page.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-7/samples/sample20.aspx)]

<span data-ttu-id="81ac4-195">Vzhledem k tomu, že uživatelský ovládací prvek AlsoPurchased vyžaduje číslo ProductId, nastavíme vlastnost ProductID našeho ovládacího prvku pomocí příkazu Eval pro aktuální položku datového modelu stránky.</span><span class="sxs-lookup"><span data-stu-id="81ac4-195">Since the AlsoPurchased user control requires a ProductId number we will set the ProductID property of our control by using an Eval statement against the current data model item of the page.</span></span>

![](tailspin-spyworks-part-7/_static/image3.png)

<span data-ttu-id="81ac4-196">Když teď sestavíme a spustíme a provedeme přechod na produkt, uvidíme také položky koupené.</span><span class="sxs-lookup"><span data-stu-id="81ac4-196">When we build and run now and browse to a product we see the "Also Purchased" items.</span></span>

![](tailspin-spyworks-part-7/_static/image7.jpg)

> [!div class="step-by-step"]
> <span data-ttu-id="81ac4-197">[Předchozí](tailspin-spyworks-part-6.md)
> [Další](tailspin-spyworks-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="81ac4-197">[Previous](tailspin-spyworks-part-6.md)
[Next](tailspin-spyworks-part-8.md)</span></span>

---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: '4\. část: seznam produktů | Microsoft Docs'
author: JoeStagner
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 4 pokrývá výpis produktů pomocí ovládacího prvku GridView...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: 7af1b8afa2ecc8df9846f2edd2091b26b93a811c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78566981"
---
# <a name="part-4-listing-products"></a><span data-ttu-id="97942-104">4\. část: Seznam produktů</span><span class="sxs-lookup"><span data-stu-id="97942-104">Part 4: Listing Products</span></span>

<span data-ttu-id="97942-105">[Jana Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="97942-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="97942-106">Tailspin Spyworks ukazuje, jak neobyčejně jednoduché je vytvářet výkonné a škálovatelné aplikace pro platformu .NET.</span><span class="sxs-lookup"><span data-stu-id="97942-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="97942-107">Ukazuje, jak používat Skvělé nové funkce v ASP.NET 4 k vytvoření online obchodu, včetně nákupu, rezervace a správy.</span><span class="sxs-lookup"><span data-stu-id="97942-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="97942-108">V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="97942-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="97942-109">Část 4 pokrývá výpis produktů pomocí ovládacího prvku GridView.</span><span class="sxs-lookup"><span data-stu-id="97942-109">Part 4 covers listing products with the GridView control.</span></span>

## <a id="_Toc260221670"></a><span data-ttu-id="97942-110">Výpis produktů pomocí ovládacího prvku GridView</span><span class="sxs-lookup"><span data-stu-id="97942-110">Listing Products with the GridView Control</span></span>

<span data-ttu-id="97942-111">Pojďme začít s implementací naší stránky ProductsList. aspx tím, že kliknete pravým tlačítkem na naše řešení a vyberete Přidat a nová položka.</span><span class="sxs-lookup"><span data-stu-id="97942-111">Let's begin implementing our ProductsList.aspx page by "Right Clicking" on our solution and selecting "Add" and "New Item".</span></span>

![](tailspin-spyworks-part-4/_static/image1.jpg)

<span data-ttu-id="97942-112">Vyberte možnost webový formulář pomocí stránky předlohy a zadejte název stránky ProductsList. aspx.</span><span class="sxs-lookup"><span data-stu-id="97942-112">Choose "Web Form Using Master Page" and enter a page name of ProductsList.aspx".</span></span>

<span data-ttu-id="97942-113">Klikněte na tlačítko Přidat.</span><span class="sxs-lookup"><span data-stu-id="97942-113">Click "Add".</span></span>

![](tailspin-spyworks-part-4/_static/image2.jpg)

<span data-ttu-id="97942-114">Dále zvolte složku "Styles" (styly), kde jsme umístili stránku Web. Master a vyberte ji v okně "obsah složky".</span><span class="sxs-lookup"><span data-stu-id="97942-114">Next choose the "Styles" folder where we placed the Site.Master page and select it from the "Contents of folder" window.</span></span>

![](tailspin-spyworks-part-4/_static/image3.jpg)

<span data-ttu-id="97942-115">Stránku vytvoříte kliknutím na OK.</span><span class="sxs-lookup"><span data-stu-id="97942-115">Click "Ok" to create the page.</span></span>

<span data-ttu-id="97942-116">Naše databáze je naplněná daty produktu, jak vidíte níže.</span><span class="sxs-lookup"><span data-stu-id="97942-116">Our database is populated with product data as seen below.</span></span>

![](tailspin-spyworks-part-4/_static/image4.jpg)

<span data-ttu-id="97942-117">Po vytvoření naší stránky znovu použijeme zdroj dat entity pro přístup k datům produktu, ale v této instanci musíme vybrat entity produktů a musíme omezit vrácené položky jenom na ty, které jsou pro vybranou kategorii vracené.</span><span class="sxs-lookup"><span data-stu-id="97942-117">After our page is created we'll again use an Entity Data Source to access that product data, but in this instance we need to select the Product Entities and we need to restrict the items that are returned to only those for the selected Category.</span></span>

<span data-ttu-id="97942-118">Abychom to mohli udělat, řekne EntityDataSource, aby automaticky vygeneroval klauzuli WHERE, a my určíme WhereParameter.</span><span class="sxs-lookup"><span data-stu-id="97942-118">To accomplish this we'll tell the EntityDataSource to Auto Generate the WHERE clause and we'll specify the WhereParameter.</span></span>

<span data-ttu-id="97942-119">Odvoláte to, když jsme vytvořili položky nabídky v naší "nabídce kategorie produktu", dynamicky jsme vytvořili propojení přidáním KódKategorie do řetězce dotazu pro každé propojení.</span><span class="sxs-lookup"><span data-stu-id="97942-119">You'll recall that when we created the Menu Items in our "Product Category Menu" we dynamically built the link by adding the CategoryID to the QueryString for each link.</span></span> <span data-ttu-id="97942-120">Zdroj dat entity sdělíme, aby se odvodil parametr WHERE z tohoto parametru QueryString.</span><span class="sxs-lookup"><span data-stu-id="97942-120">We will tell the Entity Data Source to derive the WHERE parameter from that QueryString parameter.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

<span data-ttu-id="97942-121">Dále nakonfigurujeme ovládací prvek ListView pro zobrazení seznamu produktů.</span><span class="sxs-lookup"><span data-stu-id="97942-121">Next, we'll configure the ListView control to display a list of products.</span></span> <span data-ttu-id="97942-122">Pro vytvoření optimálního prostředí pro nákupy zkomprimujeme několik stručných funkcí do každého jednotlivého produktu zobrazeného v našem ListVew.</span><span class="sxs-lookup"><span data-stu-id="97942-122">To create an optimal shopping experience we'll compact several concise features into each individual product displayed in our ListVew.</span></span>

- <span data-ttu-id="97942-123">Název produktu bude odkaz na detailní zobrazení produktu.</span><span class="sxs-lookup"><span data-stu-id="97942-123">The product name will be a link to the product's detail view.</span></span>
- <span data-ttu-id="97942-124">Zobrazí se cena za produkt.</span><span class="sxs-lookup"><span data-stu-id="97942-124">The product's price will be displayed.</span></span>
- <span data-ttu-id="97942-125">Zobrazí se obrázek produktu a dynamicky se vybere obrázek z adresáře imagí katalogu v naší aplikaci.</span><span class="sxs-lookup"><span data-stu-id="97942-125">An image of the product will be displayed and we'll dynamically select the image from a catalog images directory in our application.</span></span>
- <span data-ttu-id="97942-126">Budeme zahrnovat odkaz na okamžité přidání konkrétního produktu do nákupního košíku.</span><span class="sxs-lookup"><span data-stu-id="97942-126">We will include a link to immediately add the specific product to the shopping cart.</span></span>

<span data-ttu-id="97942-127">Zde je značka pro naši instanci ovládacího prvku ListView.</span><span class="sxs-lookup"><span data-stu-id="97942-127">Here is the markup for our ListView control instance.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

<span data-ttu-id="97942-128">Dynamicky vytváříme několik odkazů na každý zobrazený produkt.</span><span class="sxs-lookup"><span data-stu-id="97942-128">We are dynamically building several links for each displayed product.</span></span>

<span data-ttu-id="97942-129">Před testováním vlastní nové stránky taky musíme vytvořit adresářovou strukturu pro Image katalogu produktů následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="97942-129">Also, before we test own new page we need to create the directory structure for the product catalog images as follows.</span></span>

![](tailspin-spyworks-part-4/_static/image1.png)

<span data-ttu-id="97942-130">Jakmile budou k dispozici naše image produktů, můžeme otestovat stránku seznam produktů.</span><span class="sxs-lookup"><span data-stu-id="97942-130">Once our product images are accessible we can test our product list page.</span></span>

![](tailspin-spyworks-part-4/_static/image5.jpg)

<span data-ttu-id="97942-131">Na domovské stránce webu klikněte na jeden z odkazů seznamu kategorií.</span><span class="sxs-lookup"><span data-stu-id="97942-131">From the site's home page, click on one of the Category List Links.</span></span>

![](tailspin-spyworks-part-4/_static/image6.jpg)

<span data-ttu-id="97942-132">Nyní musíme implementovat stránku ProductDetails. aspx a funkci AddToCart.</span><span class="sxs-lookup"><span data-stu-id="97942-132">Now we need to implement the ProductDetails.aspx page and the AddToCart functionality.</span></span>

<span data-ttu-id="97942-133">Pomocí&gt;souboru New vytvořte stránku s názvem ProductDetails. aspx pomocí stránky předlohy webu, kterou jste předtím používali.</span><span class="sxs-lookup"><span data-stu-id="97942-133">Use File-&gt;New to create a page name ProductDetails.aspx using the site Master Page as we did previously.</span></span>

<span data-ttu-id="97942-134">Znovu použijeme ovládací prvek EntityDataSource pro přístup k určitému záznamu produktu v databázi a my použijeme ovládací prvek ASP.NET FormView k zobrazení dat produktu následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="97942-134">We will again use an EntityDataSource control to access the specific product record in the database and we will use an ASP.NET FormView control to display the product data as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

<span data-ttu-id="97942-135">Nedělejte si starosti, pokud formátování vypadá za bitovou Funny.</span><span class="sxs-lookup"><span data-stu-id="97942-135">Don't worry if the formatting looks a bit funny to you.</span></span> <span data-ttu-id="97942-136">Výše uvedený kód ponechá místo v rozložení zobrazení pro několik funkcí, které budeme implementovat později.</span><span class="sxs-lookup"><span data-stu-id="97942-136">The markup above leaves room in the display layout for a couple of features we'll implement later on.</span></span>

<span data-ttu-id="97942-137">Nákupní košík bude v naší aplikaci představovat složitější logiku.</span><span class="sxs-lookup"><span data-stu-id="97942-137">The Shopping Cart will represent the more complex logic in our application.</span></span> <span data-ttu-id="97942-138">Chcete-li začít, použijte&gt;soubor New k vytvoření stránky s názvem MyShoppingCart. aspx.</span><span class="sxs-lookup"><span data-stu-id="97942-138">To get started, use File-&gt;New to create a page called MyShoppingCart.aspx.</span></span>

<span data-ttu-id="97942-139">Všimněte si, že nepoužíváme název ShoppingCart. aspx.</span><span class="sxs-lookup"><span data-stu-id="97942-139">Note that we are not choosing the name ShoppingCart.aspx.</span></span>

<span data-ttu-id="97942-140">Naše databáze obsahuje tabulku s názvem "ShoppingCart".</span><span class="sxs-lookup"><span data-stu-id="97942-140">Our database contains a table named "ShoppingCart".</span></span> <span data-ttu-id="97942-141">Když jsme vygenerovali model EDM (Entity Data Model) pro každou tabulku v databázi se vytvořila třída.</span><span class="sxs-lookup"><span data-stu-id="97942-141">When we generated an Entity Data Model a class was created for each table in the database.</span></span> <span data-ttu-id="97942-142">Proto model EDM (Entity Data Model) vygeneroval třídu entity s názvem "ShoppingCart".</span><span class="sxs-lookup"><span data-stu-id="97942-142">Therefore, the Entity Data Model generated an Entity Class named "ShoppingCart".</span></span> <span data-ttu-id="97942-143">Mohli jsme model upravit, abychom mohli použít tento název pro implementaci nákupních košíků nebo ho pro naše potřeby využít, ale místo toho je možné jednoduše vybrat název, který se tomuto konfliktu vyhne.</span><span class="sxs-lookup"><span data-stu-id="97942-143">We could edit the model so that we could use that name for our shopping cart implementation or extend it for our needs, but we will opt instead to simply select a name that will avoid the conflict.</span></span>

<span data-ttu-id="97942-144">Také je potřeba poznamenat, že vytvoříme jednoduchý nákupní košík a vložíte logiku nákupního košíku se zobrazením nákupního košíku.</span><span class="sxs-lookup"><span data-stu-id="97942-144">It's also worth noting that we will be creating a simple shopping cart and embedding the shopping cart logic with the shopping cart display.</span></span> <span data-ttu-id="97942-145">Můžeme se také rozhodnout implementovat si nákupní košík v zcela oddělené obchodní vrstvě.</span><span class="sxs-lookup"><span data-stu-id="97942-145">We might also choose to implement our shopping cart in a completely separate Business Layer.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="97942-146">[Předchozí](tailspin-spyworks-part-3.md)
> [Další](tailspin-spyworks-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="97942-146">[Previous](tailspin-spyworks-part-3.md)
[Next](tailspin-spyworks-part-5.md)</span></span>

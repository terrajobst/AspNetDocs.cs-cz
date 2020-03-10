---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: 'Část 3: nabídka rozložení a kategorie | Microsoft Docs'
author: JoeStagner
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 3 pokrývá přidání rozložení a nabídky kategorie.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: a223b97fd362ecf73ecde431e141021c1dcc6a6d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639116"
---
# <a name="part-3-layout-and-category-menu"></a><span data-ttu-id="adb1e-104">3\. část: Nabídka Rozložení a Kategorie</span><span class="sxs-lookup"><span data-stu-id="adb1e-104">Part 3: Layout and Category Menu</span></span>

<span data-ttu-id="adb1e-105">[Jana Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="adb1e-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="adb1e-106">Tailspin Spyworks ukazuje, jak neobyčejně jednoduché je vytvářet výkonné a škálovatelné aplikace pro platformu .NET.</span><span class="sxs-lookup"><span data-stu-id="adb1e-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="adb1e-107">Ukazuje, jak používat Skvělé nové funkce v ASP.NET 4 k vytvoření online obchodu, včetně nákupu, rezervace a správy.</span><span class="sxs-lookup"><span data-stu-id="adb1e-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="adb1e-108">V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="adb1e-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="adb1e-109">Část 3 pokrývá přidání rozložení a nabídky kategorie.</span><span class="sxs-lookup"><span data-stu-id="adb1e-109">Part 3 covers adding layout and a category menu.</span></span>

## <a id="_Toc260221669"></a><span data-ttu-id="adb1e-110">Přidání některých rozložení a nabídky kategorie</span><span class="sxs-lookup"><span data-stu-id="adb1e-110">Adding Some Layout and a Category Menu</span></span>

<span data-ttu-id="adb1e-111">Na naší stránce předlohy webu přidáte div pro sloupec vlevo, který bude obsahovat nabídku kategorie produktu.</span><span class="sxs-lookup"><span data-stu-id="adb1e-111">In our site master page we'll add a div for the left side column that will contain our product category menu.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

<span data-ttu-id="adb1e-112">Všimněte si, že požadované zarovnání a další formátování poskytne Třída CSS, kterou jsme přidali do našeho souboru Style. CSS.</span><span class="sxs-lookup"><span data-stu-id="adb1e-112">Note that the desired aligning and other formatting will be provided by the CSS class that we added to our Style.css file.</span></span>

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

<span data-ttu-id="adb1e-113">Nabídka Produktová kategorie se vytvoří dynamicky za běhu a provede dotazování databáze Commerce na existující kategorie produktů a vytvoření položek nabídky a odpovídajících odkazů.</span><span class="sxs-lookup"><span data-stu-id="adb1e-113">The product category menu will be dynamically created at runtime by querying the Commerce database for existing product categories and creating the menu items and corresponding links.</span></span>

<span data-ttu-id="adb1e-114">K tomuto účelu použijeme dvě stránky ASP. NETTO výkonné ovládací prvky pro data.</span><span class="sxs-lookup"><span data-stu-id="adb1e-114">To accomplish this we will use two of ASP.NET's powerful data controls.</span></span> <span data-ttu-id="adb1e-115">Ovládací prvek zdroje dat entity a ovládací prvek ListView.</span><span class="sxs-lookup"><span data-stu-id="adb1e-115">The "Entity Data Source" control and the "ListView" control.</span></span>

![](tailspin-spyworks-part-3/_static/image1.jpg)

<span data-ttu-id="adb1e-116">Pojďme přepnout na zobrazení Návrh a pomocí pomocníků nakonfigurovat naše ovládací prvky.</span><span class="sxs-lookup"><span data-stu-id="adb1e-116">Let's switch to "Design View" and use the helpers to configure our controls.</span></span>

![](tailspin-spyworks-part-3/_static/image2.jpg)

<span data-ttu-id="adb1e-117">Nastavíme vlastnost ID EntityDataSource na možnost EDS\_kategorii\_a kliknete na Konfigurovat zdroj dat.</span><span class="sxs-lookup"><span data-stu-id="adb1e-117">Let's set the EntityDataSource ID property to EDS\_Category\_Menu and click on "Configure Data Source".</span></span>

![](tailspin-spyworks-part-3/_static/image3.jpg)

<span data-ttu-id="adb1e-118">Vyberte připojení CommerceEntities, které jste vytvořili pro nás, když jsme vytvořili model zdroje dat entity pro naši obchodní databázi a kliknete na další.</span><span class="sxs-lookup"><span data-stu-id="adb1e-118">Select the CommerceEntities Connection that was created for us when we created the Entity Data Source Model for our Commerce Database and click "Next".</span></span>

![](tailspin-spyworks-part-3/_static/image4.jpg)

<span data-ttu-id="adb1e-119">Vyberte název sady entit "kategorie" a ponechte ostatní možnosti jako výchozí.</span><span class="sxs-lookup"><span data-stu-id="adb1e-119">Select the "Categories" Entity set name and leave the rest of the options as default.</span></span> <span data-ttu-id="adb1e-120">Klikněte na tlačítko Dokončit.</span><span class="sxs-lookup"><span data-stu-id="adb1e-120">Click "Finish".</span></span>

<span data-ttu-id="adb1e-121">Nyní nastavíme vlastnost ID instance ovládacího prvku ListView, kterou jsme umístili na naši stránku, na ListView\_ProductsMenu a aktivujete její pomoc.</span><span class="sxs-lookup"><span data-stu-id="adb1e-121">Now let's set the ID property of the ListView control instance that we placed on our page to ListView\_ProductsMenu and activate its helper.</span></span>

![](tailspin-spyworks-part-3/_static/image5.jpg)

<span data-ttu-id="adb1e-122">I když bychom mohli použít možnosti ovládacího prvku k formátování zobrazení a formátování datových položek, vytváření naší nabídky bude vyžadovat pouze jednoduché označení, takže budeme kód zadávat v zobrazení zdroje.</span><span class="sxs-lookup"><span data-stu-id="adb1e-122">Though we could use control options to format the data item display and formatting, our menu creation will only require simple markup so we will enter the code in the source view.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

<span data-ttu-id="adb1e-123">Poznamenejte si prosím příkaz Eval: &lt;% # Eval ("CategoryName")%&gt;</span><span class="sxs-lookup"><span data-stu-id="adb1e-123">Please note the "Eval" statement : &lt;%# Eval("CategoryName") %&gt;</span></span>

<span data-ttu-id="adb1e-124">Syntaxe ASP.NET &lt;% #%&gt; je zjednodušená konvence, která řídí modulu runtime, aby běžela bez ohledu na to, zda je obsažena v rámci výstupu, a výstupem výsledků "na řádku".</span><span class="sxs-lookup"><span data-stu-id="adb1e-124">The ASP.NET syntax &lt;%# %&gt; is a shorthand convention that instructs the runtime to execute whatever is contained within and output the results "in Line".</span></span>

<span data-ttu-id="adb1e-125">Vyhodnocení příkazu ("CategoryName") dává pokyn, aby pro aktuální položku v vázané kolekci datových položek načetla hodnotu názvů položek modelu entity "CategoryName".</span><span class="sxs-lookup"><span data-stu-id="adb1e-125">The statement Eval("CategoryName") instructs that, for the current entry in the bound collection of data items, fetch the value of the Entity Model item names "CategoryName".</span></span> <span data-ttu-id="adb1e-126">Toto je Stručná syntaxe pro velmi výkonnou funkci.</span><span class="sxs-lookup"><span data-stu-id="adb1e-126">This is concise syntax for a very powerful feature.</span></span>

<span data-ttu-id="adb1e-127">Umožňuje aplikaci spustit nyní.</span><span class="sxs-lookup"><span data-stu-id="adb1e-127">Lets run the application now.</span></span>

![](tailspin-spyworks-part-3/_static/image6.jpg)

<span data-ttu-id="adb1e-128">Všimněte si, že se teď zobrazuje naše nabídka kategorie produktů, a když najedete myší na jednu z položek nabídky kategorie, můžeme odkazy na položky nabídky odkazovat na stránku, kterou jsme ještě vytvořili s názvem ProductsList. aspx a že jsme vytvořili argument dynamického řetězce dotazu, který obsahuje  ID kategorie</span><span class="sxs-lookup"><span data-stu-id="adb1e-128">Note that our product category menu is now displayed and when we hover over one of the category menu items we can see the menu item link points to a page we have yet to implement named ProductsList.aspx and that we have built a dynamic query string argument that contains the category id.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="adb1e-129">[Předchozí](tailspin-spyworks-part-2.md)
> [Další](tailspin-spyworks-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="adb1e-129">[Previous](tailspin-spyworks-part-2.md)
[Next](tailspin-spyworks-part-4.md)</span></span>

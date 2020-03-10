---
uid: web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
title: Začínáme s AJAX Control Toolkit (C#) | Microsoft Docs
author: microsoft
description: Naučte se všechno, co potřebujete vědět, abyste mohli začít používat AJAX Control Toolkit.
ms.author: riande
ms.date: 05/12/2009
ms.assetid: 16dc5c11-65be-4eae-a818-9fad7f8259c6
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/getting-started/get-started-with-the-ajax-control-toolkit-cs
msc.type: authoredcontent
ms.openlocfilehash: 7478b090ec52778572d70065983de6be8bdb4e6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78621602"
---
# <a name="get-started-with-the-ajax-control-toolkit-c"></a><span data-ttu-id="866db-103">Začínáme se sadou nástrojů AJAX Control Toolkit (C#)</span><span class="sxs-lookup"><span data-stu-id="866db-103">Get Started with the AJAX Control Toolkit (C#)</span></span>

<span data-ttu-id="866db-104">od [Microsoftu](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="866db-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="866db-105">Naučte se všechno, co potřebujete vědět, abyste mohli začít používat AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="866db-105">Learn all you need to know to get started using the AJAX Control Toolkit.</span></span>

<span data-ttu-id="866db-106">Sada nástrojů AJAX Control Toolkit obsahuje více než 30 bezplatných ovládacích prvků, které lze použít v aplikacích ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="866db-106">The AJAX Control Toolkit contains more than 30 free controls that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="866db-107">V tomto kurzu se naučíte, jak stáhnout AJAX Control Toolkit a přidat ovládací prvky Toolkit do sady Visual Studio/Visual Web Developer Express Toolkit.</span><span class="sxs-lookup"><span data-stu-id="866db-107">In this tutorial, you learn how to download the AJAX Control Toolkit and add the toolkit controls to your Visual Studio/Visual Web Developer Express toolbox.</span></span>

## <a name="downloading-the-ajax-control-toolkit"></a><span data-ttu-id="866db-108">Stažení sady nástrojů AJAX Control Toolkit</span><span class="sxs-lookup"><span data-stu-id="866db-108">Downloading the AJAX Control Toolkit</span></span>

<span data-ttu-id="866db-109">[AJAX Control Toolkit](http://devexpress.com/act) je open source projekt vyvinutý členy komunity ASP.NET a týmu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="866db-109">The [AJAX Control Toolkit](http://devexpress.com/act) is an open source project developed by the members of the ASP.NET community and the ASP.NET team.</span></span> 

<span data-ttu-id="866db-110">[![stažení sady nástrojů AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="866db-110">[![Downloading the AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image1.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image1.png)</span></span>

<span data-ttu-id="866db-111">**Obrázek 01**: stažení sady nástrojů Ajax Control Toolkit ([kliknutím zobrazíte obrázek v plné velikosti](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="866db-111">**Figure 01**: Downloading the AJAX Control Toolkit([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image2.png))</span></span>

<span data-ttu-id="866db-112">Po stažení souboru je nutné soubor odblokovat.</span><span class="sxs-lookup"><span data-stu-id="866db-112">After you download the file, you need to unblock the file.</span></span> <span data-ttu-id="866db-113">Klikněte na soubor pravým tlačítkem, vyberte vlastnosti a klikněte na tlačítko **odblokování** (viz obrázek 2).</span><span class="sxs-lookup"><span data-stu-id="866db-113">Right-click the file, select Properties, and click the **Unblock** button (see Figure 2).</span></span>

<span data-ttu-id="866db-114">[![odblokování souboru ZIP sady nástrojů AJAX Control Toolkit](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="866db-114">[![Unblocking the AJAX Control Toolkit ZIP file](get-started-with-the-ajax-control-toolkit-cs/_static/image2.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image3.png)</span></span>

<span data-ttu-id="866db-115">**Obrázek 02**: odblokování souboru ZIP sady nástrojů Ajax Control Toolkit ([kliknutím zobrazíte obrázek v plné velikosti](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="866db-115">**Figure 02**: Unblocking the AJAX Control Toolkit ZIP file([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image4.png))</span></span>

<span data-ttu-id="866db-116">Po odblokování souboru můžete soubor rozbalit: klikněte pravým tlačítkem myši na soubor a vyberte možnost **Rozbalit vše** v nabídce.</span><span class="sxs-lookup"><span data-stu-id="866db-116">After you unblock the file, you can unzip the file: Right-click the file and select the **Extract All** menu option.</span></span> <span data-ttu-id="866db-117">Nyní jsme připraveni přidat sadu nástrojů do sady Visual Studio nebo Visual Web Developer Toolkit.</span><span class="sxs-lookup"><span data-stu-id="866db-117">Now, we are ready to add the toolkit to the Visual Studio/Visual Web Developer toolbox.</span></span>

## <a name="adding-the-ajax-control-toolkit-to-the-toolbox"></a><span data-ttu-id="866db-118">Přidání sady nástrojů AJAX Control Toolkit do sady nástrojů</span><span class="sxs-lookup"><span data-stu-id="866db-118">Adding the AJAX Control Toolkit to the Toolbox</span></span>

<span data-ttu-id="866db-119">Nejjednodušší způsob, jak použít sadu nástrojů AJAX Control Toolkit, je přidat sadu nástrojů do sady Visual Studio nebo Visual Web Developer Toolkit (viz obrázek 3).</span><span class="sxs-lookup"><span data-stu-id="866db-119">The easiest way to use the AJAX Control Toolkit is to add the toolkit to your Visual Studio/Visual Web Developer toolbox (see Figure 3).</span></span> <span data-ttu-id="866db-120">Tímto způsobem můžete jednoduše přetáhnout ovládací prvek Toolkit na stránku, pokud ho chcete použít.</span><span class="sxs-lookup"><span data-stu-id="866db-120">That way, you can simply drag a toolkit control onto a page when you want to use it.</span></span>

<span data-ttu-id="866db-121">[![sada nástrojů AJAX Control Toolkit se zobrazí v sadě nástrojů](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="866db-121">[![AJAX Control Toolkit appears in toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image3.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image5.png)</span></span>

<span data-ttu-id="866db-122">**Obrázek 03**: ovládací prvek AJAX Control Toolkit se zobrazuje v sadě nástrojů ([kliknutím zobrazíte obrázek v plné velikosti](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png)).</span><span class="sxs-lookup"><span data-stu-id="866db-122">**Figure 03**: AJAX Control Toolkit appears in toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image6.png))</span></span>

<span data-ttu-id="866db-123">Nejprve je třeba přidat kartu AJAX Control Toolkit do sady nástrojů.</span><span class="sxs-lookup"><span data-stu-id="866db-123">First, you need to add an AJAX Control Toolkit tab to the toolbox.</span></span> <span data-ttu-id="866db-124">Postupujte následovně.</span><span class="sxs-lookup"><span data-stu-id="866db-124">Follow these steps.</span></span>

1. <span data-ttu-id="866db-125">Vytvořte nový web ASP.NET tak, že vyberete soubor možnosti nabídky, nový web.</span><span class="sxs-lookup"><span data-stu-id="866db-125">Create a new ASP.NET Website by selecting the menu option File, New Website.</span></span> <span data-ttu-id="866db-126">Dvojitým kliknutím na Default. aspx v okně Průzkumník řešení otevřete soubor v editoru.</span><span class="sxs-lookup"><span data-stu-id="866db-126">Double-click the Default.aspx in the Solution Explorer window to open the file in the editor.</span></span>
2. <span data-ttu-id="866db-127">Klikněte pravým tlačítkem myši na panel nástrojů pod kartou obecné a vyberte možnost nabídky **Přidat kartu** (viz obrázek 4).</span><span class="sxs-lookup"><span data-stu-id="866db-127">Right-click the Toolbox beneath the General Tab and select the menu option **Add Tab** (see Figure 4).</span></span>
3. <span data-ttu-id="866db-128">Zadejte novou kartu s názvem AJAX Control Toolkit.</span><span class="sxs-lookup"><span data-stu-id="866db-128">Enter a new tab named AJAX Control Toolkit.</span></span>

<span data-ttu-id="866db-129">[![přidávání nové karty](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="866db-129">[![Adding a new tab](get-started-with-the-ajax-control-toolkit-cs/_static/image4.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image7.png)</span></span>

<span data-ttu-id="866db-130">**Obrázek 04**: Přidání nové karty ([kliknutím zobrazíte obrázek v plné velikosti](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="866db-130">**Figure 04**: Adding a new tab([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image8.png))</span></span>

<span data-ttu-id="866db-131">Dále je nutné přidat ovládací prvky AJAX Control Toolkit na novou kartu. postupujte takto:</span><span class="sxs-lookup"><span data-stu-id="866db-131">Next, you need to add the AJAX Control Toolkit controls to the new tab. Follow these steps:</span></span>

- <span data-ttu-id="866db-132">Klikněte pravým tlačítkem myši pod kartu AJAX Control Toolkit a vyberte možnost nabídky vybrat **položky (viz obrázek 5)** .</span><span class="sxs-lookup"><span data-stu-id="866db-132">Right-click beneath the AJAX Control Toolkit tab and select the menu option **Choose Items (see Figure 5)**.</span></span>
- <span data-ttu-id="866db-133">Přejděte do umístění, kde jste rozAjaxControlToolkiti AJAX Control Toolkit, a vyberte sestavení. dll.</span><span class="sxs-lookup"><span data-stu-id="866db-133">Browse to the location where you unzipped the AJAX Control Toolkit and select the AjaxControlToolkit.dll assembly.</span></span>

<span data-ttu-id="866db-134">[![zvolit položky, které se mají přidat do sady nástrojů](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="866db-134">[![Choose items to add to the toolbox](get-started-with-the-ajax-control-toolkit-cs/_static/image5.jpg)](get-started-with-the-ajax-control-toolkit-cs/_static/image9.png)</span></span>

<span data-ttu-id="866db-135">**Obrázek 05**: vyberte položky, které chcete přidat do sady nástrojů ([kliknutím zobrazíte obrázek v plné velikosti).](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="866db-135">**Figure 05**: Choose items to add to the toolbox([Click to view full-size image](get-started-with-the-ajax-control-toolkit-cs/_static/image10.png))</span></span>

<span data-ttu-id="866db-136">Po dokončení tohoto postupu se všechny ovládací prvky sady Toolkit zobrazí v sadě nástrojů.</span><span class="sxs-lookup"><span data-stu-id="866db-136">After you complete these steps, all of the toolkit controls will appear in your toolbox.</span></span>

## <a name="upgrading-to-a-new-version-of-the-toolkit"></a><span data-ttu-id="866db-137">Upgrade na novou verzi sady nástrojů</span><span class="sxs-lookup"><span data-stu-id="866db-137">Upgrading to a New Version of the Toolkit</span></span>

<span data-ttu-id="866db-138">Pokud jste používali starší verzi sady Toolkit a teď potřebujete přejít na novější verzi, doporučujeme postupovat takto:</span><span class="sxs-lookup"><span data-stu-id="866db-138">If you were using an older release of the Toolkit and now need to move to a later version here are the recommended steps:</span></span>

- <span data-ttu-id="866db-139">Binární soubory – odstraňte starou verzi sestavení AjaxControlToolkit. dll ze složky Bin webu.</span><span class="sxs-lookup"><span data-stu-id="866db-139">Binaries - Delete the old version of the AjaxControlToolkit.dll assembly from your website Bin folder.</span></span>
- <span data-ttu-id="866db-140">Položky sady nástrojů – odstraňte kartu AJAX Control Toolkit a pomocí výše uvedeného postupu znovu vytvořte kartu s novou verzí sestavení AjaxControlToolkit. dll.</span><span class="sxs-lookup"><span data-stu-id="866db-140">Toolbox Items - Delete the AJAX Control Toolkit tab and follow the steps above to re-create the tab with the new version of the AjaxControlToolkit.dll assembly.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="866db-141">Next</span><span class="sxs-lookup"><span data-stu-id="866db-141">Next</span></span>](using-ajax-control-toolkit-controls-and-control-extenders-cs.md)

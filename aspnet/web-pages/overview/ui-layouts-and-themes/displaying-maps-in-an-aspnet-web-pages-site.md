---
uid: web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
title: Zobrazení map na webu ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Tento článek vysvětluje, jak zobrazit interaktivní mapy na stránkách na webu ASP.NET Web Pages (Razor) na základě mapování služeb poskytovaných bingem, Google, MA...
ms.author: riande
ms.date: 02/20/2014
ms.assetid: b5c268dd-ca6a-4562-b94c-a220fcf01f58
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/displaying-maps-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 36f3b753cf312504892872ff54bef49854588990
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638675"
---
# <a name="displaying-maps-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="56603-103">Zobrazení map na webu ASP.NET Web Pages (Razor)</span><span class="sxs-lookup"><span data-stu-id="56603-103">Displaying Maps in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="56603-104">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="56603-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="56603-105">Tento článek vysvětluje, jak zobrazit interaktivní mapy na stránkách na webu ASP.NET Web Pages (Razor) na základě mapování služeb poskytovaných bingem, Google, MapQuest a Yahoo.</span><span class="sxs-lookup"><span data-stu-id="56603-105">This article explains how to display interactive maps on pages in an ASP.NET Web Pages (Razor) website based on mapping services provided by Bing, Google, MapQuest, and Yahoo.</span></span>
> 
> <span data-ttu-id="56603-106">Naučíte se:</span><span class="sxs-lookup"><span data-stu-id="56603-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="56603-107">Generování mapy založené na adrese.</span><span class="sxs-lookup"><span data-stu-id="56603-107">How to generate a map based on an address.</span></span>
> - <span data-ttu-id="56603-108">Jak vygenerovat mapu na základě souřadnic zeměpisné šířky a délky.</span><span class="sxs-lookup"><span data-stu-id="56603-108">How to generate a map based on latitude and longitude coordinates.</span></span>
> - <span data-ttu-id="56603-109">Jak zaregistrovat vývojářský účet mapy Bing a získat klíč pro použití se službou mapy Bing.</span><span class="sxs-lookup"><span data-stu-id="56603-109">How to register a Bing Maps Developer Account and get a key to use with Bing Maps.</span></span>
> 
> <span data-ttu-id="56603-110">Toto je funkce ASP.NET představená v článku:</span><span class="sxs-lookup"><span data-stu-id="56603-110">This is the ASP.NET feature introduced in the article:</span></span>
> 
> - <span data-ttu-id="56603-111">Pomocná rutina `Maps`</span><span class="sxs-lookup"><span data-stu-id="56603-111">The `Maps` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="56603-112">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="56603-112">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="56603-113">Webové stránky ASP.NET (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="56603-113">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="56603-114">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="56603-114">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="56603-115">V tomto kurzu se používá také WebMatrix 3.</span><span class="sxs-lookup"><span data-stu-id="56603-115">This tutorial also works with WebMatrix 3.</span></span>

<span data-ttu-id="56603-116">Na webových stránkách můžete zobrazit mapy na stránce pomocí pomocné rutiny `Maps`.</span><span class="sxs-lookup"><span data-stu-id="56603-116">In Web Pages, you can display maps on a page by using `Maps` helper.</span></span> <span data-ttu-id="56603-117">Můžete vygenerovat mapy založené na adrese nebo v sadě souřadnic Zeměpisná délka a zeměpisná šířka.</span><span class="sxs-lookup"><span data-stu-id="56603-117">You can generate maps based either on an address or on a set of longitude and latitude coordinates.</span></span> <span data-ttu-id="56603-118">Třída `Maps` umožňuje volat oblíbené mapové moduly, včetně Bingu, Google, MapQuest a Yahoo.</span><span class="sxs-lookup"><span data-stu-id="56603-118">The `Maps` class lets you call into popular map engines including Bing, Google, MapQuest, and Yahoo.</span></span>

<span data-ttu-id="56603-119">Postup pro přidání mapování na stránku je stejný bez ohledu na to, které mapové moduly voláte.</span><span class="sxs-lookup"><span data-stu-id="56603-119">The steps for adding mapping to a page are the same regardless of which of the map engines you call.</span></span> <span data-ttu-id="56603-120">Stačí přidat odkaz na soubor JavaScriptu, který zpřístupňuje dostupné metody pro zobrazení mapy, a potom zavoláte metody pomocné rutiny `Maps`.</span><span class="sxs-lookup"><span data-stu-id="56603-120">You just add a JavaScript file reference that makes available methods to display the map, and then you call methods of the `Maps` helper.</span></span>

<span data-ttu-id="56603-121">Můžete zvolit službu mapování na základě toho, kterou `Maps` pomocnou metodu použijete.</span><span class="sxs-lookup"><span data-stu-id="56603-121">You choose a map service based on which `Maps` helper method you use.</span></span> <span data-ttu-id="56603-122">Můžete použít některý z těchto kroků:</span><span class="sxs-lookup"><span data-stu-id="56603-122">You can use any of these:</span></span>

- `Maps.GetBingHtml`
- `Maps.GetGoogleHtml`
- `Maps.GetYahooHtml`
- `Maps.GetMapQuestHtml`

## <a name="installing-the-pieces-you-need"></a><span data-ttu-id="56603-123">Instalace potřebných částí</span><span class="sxs-lookup"><span data-stu-id="56603-123">Installing the Pieces You Need</span></span>

<span data-ttu-id="56603-124">K zobrazení map budete potřebovat tyto části:</span><span class="sxs-lookup"><span data-stu-id="56603-124">To display maps, you need these pieces:</span></span>

- <span data-ttu-id="56603-125">Pomocná rutina `Maps`</span><span class="sxs-lookup"><span data-stu-id="56603-125">The `Maps` helper.</span></span> <span data-ttu-id="56603-126">Tato pomoc je ve verzi 2 knihovny webových pomoců ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="56603-126">This helper is in version 2 of the ASP.NET Web Helpers Library.</span></span> <span data-ttu-id="56603-127">Pokud jste ještě knihovnu nepřidali, můžete ji nainstalovat na svůj web jako balíček NuGet.</span><span class="sxs-lookup"><span data-stu-id="56603-127">If you haven't already added the library, you can install it in your site as a NuGet package.</span></span> <span data-ttu-id="56603-128">Podrobnosti najdete v tématu [instalace pomocníků na webu webové stránky ASP.NET](https://go.microsoft.com/fwlink/?LinkId=252372).</span><span class="sxs-lookup"><span data-stu-id="56603-128">For details, see [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372).</span></span> <span data-ttu-id="56603-129">(V galerii vyhledejte balíček `microsoft-web-helpers`.)</span><span class="sxs-lookup"><span data-stu-id="56603-129">(In the Gallery, search for the `microsoft-web-helpers` package.)</span></span>
- <span data-ttu-id="56603-130">Knihovna jQuery.</span><span class="sxs-lookup"><span data-stu-id="56603-130">The jQuery library.</span></span> <span data-ttu-id="56603-131">Několik šablon webu WebMatrix již obsahuje knihovny jQuery ve složkách *skriptu* .</span><span class="sxs-lookup"><span data-stu-id="56603-131">Several of the WebMatrix site templates already include jQuery libraries in their *Script* folders.</span></span> <span data-ttu-id="56603-132">Pokud tyto knihovny nemáte, můžete si stáhnout nejnovější knihovnu jQuery přímo z webu [jQuery.org](http://jQuery.org) .</span><span class="sxs-lookup"><span data-stu-id="56603-132">If you do not have these libraries, you can download the latest jQuery library directly from the [jQuery.org](http://jQuery.org) site.</span></span> <span data-ttu-id="56603-133">Můžete také vytvořit novou lokalitu pomocí šablony (například šablony **webu Starter** ) a potom zkopírovat soubory jQuery z dané lokality do aktuální lokality.</span><span class="sxs-lookup"><span data-stu-id="56603-133">Or you can create a new site using a template (for example, the **Starter Site** template) and then copy the jQuery files from that site to your current site.</span></span>

<span data-ttu-id="56603-134">Nakonec, pokud chcete používat mapy Bing, musíte nejdřív vytvořit (bezplatný) účet a získat klíč.</span><span class="sxs-lookup"><span data-stu-id="56603-134">Finally, if you want to use Bing maps, you must first create a (free) account and get a key.</span></span> <span data-ttu-id="56603-135">Klíč získáte pomocí následujících kroků:</span><span class="sxs-lookup"><span data-stu-id="56603-135">To get a key, follow these steps:</span></span>

1. <span data-ttu-id="56603-136">Vytvořte účet na [účtu vývojáře pro mapy Bing](https://www.microsoft.com/maps/developers/web.aspx).</span><span class="sxs-lookup"><span data-stu-id="56603-136">Create an account on the [Bing Maps Developer Account](https://www.microsoft.com/maps/developers/web.aspx).</span></span> <span data-ttu-id="56603-137">Musíte mít také účet Microsoft (Windows Live ID).</span><span class="sxs-lookup"><span data-stu-id="56603-137">You must have a Microsoft account (Windows Live ID) as well.</span></span>

    <span data-ttu-id="56603-138">Můžete určit, že chcete použít klíč pro **vyhodnocení a testování**.</span><span class="sxs-lookup"><span data-stu-id="56603-138">You can specify that you want to use the key for **Evaluation/Test**.</span></span> <span data-ttu-id="56603-139">Pokud testujete funkci mapování na vlastním počítači pomocí WebMatrixu a IIS Express, Projděte si pracovní prostor **webu** a poznamenejte si adresu URL vašeho webu (například `http://localhost:50408`, i když se vaše číslo portu bude pravděpodobně lišit).</span><span class="sxs-lookup"><span data-stu-id="56603-139">If you are testing the mapping function on your own computer using WebMatrix and IIS Express, go the **Site** workspace and note the URL of your site (for example, `http://localhost:50408`, although your port number will probably be different).</span></span> <span data-ttu-id="56603-140">Tuto adresu *localhost* můžete použít jako web při registraci.</span><span class="sxs-lookup"><span data-stu-id="56603-140">You can use this *localhost* address as the site when you register.</span></span>
2. <span data-ttu-id="56603-141">Po registraci účtu přejděte do centra účtů mapy Bing a klikněte na tlačítko **vytvořit nebo zobrazit klíče**:</span><span class="sxs-lookup"><span data-stu-id="56603-141">After you have registered for an account, go to the Bing Maps Account Center and click **Create or view keys**:</span></span>

    ![mapování – 2](displaying-maps-in-an-aspnet-web-pages-site/_static/image1.png)
3. <span data-ttu-id="56603-143">Poznamenejte si klíč, který Bing vytvoří.</span><span class="sxs-lookup"><span data-stu-id="56603-143">Record the key that Bing creates.</span></span>

## <a name="creating-a-map-based-on-an-address-using-google"></a><span data-ttu-id="56603-144">Vytvoření mapy na základě adresy (pomocí Google)</span><span class="sxs-lookup"><span data-stu-id="56603-144">Creating a Map Based on an Address (Using Google)</span></span>

<span data-ttu-id="56603-145">Následující příklad ukazuje, jak vytvořit stránku, která vykresluje mapu na základě adresy.</span><span class="sxs-lookup"><span data-stu-id="56603-145">The following example shows how to create a page that renders a map based on an address.</span></span> <span data-ttu-id="56603-146">Tento příklad ukazuje, jak používat Google Maps.</span><span class="sxs-lookup"><span data-stu-id="56603-146">This example shows how to use Google Maps.</span></span>

1. <span data-ttu-id="56603-147">V kořenovém adresáři webu vytvořte soubor s názvem *MapAddress. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="56603-147">Create a file named *MapAddress.cshtml* in the root of the site.</span></span> <span data-ttu-id="56603-148">Tato stránka vygeneruje mapu založenou na adrese, kterou jí předáte.</span><span class="sxs-lookup"><span data-stu-id="56603-148">This page will generate a map based on an address that you pass to it.</span></span>
2. <span data-ttu-id="56603-149">Zkopírujte do souboru následující kód, který přepíše existující obsah.</span><span class="sxs-lookup"><span data-stu-id="56603-149">Copy the following code into the file, overwriting the existing content.</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    <span data-ttu-id="56603-150">Všimněte si následujících funkcí stránky:</span><span class="sxs-lookup"><span data-stu-id="56603-150">Notice the following features of the page:</span></span>

    - <span data-ttu-id="56603-151">Prvek `<script>` v elementu `<head>`.</span><span class="sxs-lookup"><span data-stu-id="56603-151">The `<script>` element in the `<head>` element.</span></span> <span data-ttu-id="56603-152">V příkladu element `<script>` odkazuje na soubor *jQuery 1.6.4. min. js* , což je minifikovaného (komprimovaná) verze knihovny jQuery, verze 1.6.4.</span><span class="sxs-lookup"><span data-stu-id="56603-152">In the example, the `<script>` element references the *jquery-1.6.4.min.js* file, which is a minified (compressed) version of the jQuery library, version 1.6.4.</span></span> <span data-ttu-id="56603-153">Všimněte si, že odkaz předpokládá, že soubor *. js* je ve složce *Scripts* vaší lokality.</span><span class="sxs-lookup"><span data-stu-id="56603-153">Note that the reference assumes that the *.js* file is in the *Scripts* folder of your site.</span></span> 

        > [!NOTE]
        > <span data-ttu-id="56603-154">Pokud používáte jinou verzi knihovny jQuery, stačí, abyste se ujistili, že budete správně ukazovat na správnou verzi.</span><span class="sxs-lookup"><span data-stu-id="56603-154">If you're using a different version of the jQuery library, just make sure that you're pointing to that version correctly.</span></span>
    - <span data-ttu-id="56603-155">Volání `@Maps.GetGoogleHtml` v těle stránky.</span><span class="sxs-lookup"><span data-stu-id="56603-155">The call to the `@Maps.GetGoogleHtml` in the body of the page.</span></span> <span data-ttu-id="56603-156">Chcete-li namapovat adresu, je nutné předat řetězec adresy.</span><span class="sxs-lookup"><span data-stu-id="56603-156">To map an address, you must pass an address string.</span></span> <span data-ttu-id="56603-157">Metody pro ostatní mapové stroje fungují podobným způsobem (`@Maps.GetYahooHtml``@Maps.GetMapQuestHtml`).</span><span class="sxs-lookup"><span data-stu-id="56603-157">The methods for the other map engines work in a similar way (`@Maps.GetYahooHtml`, `@Maps.GetMapQuestHtml`).</span></span>
3. <span data-ttu-id="56603-158">Spusťte stránku a zadejte adresu.</span><span class="sxs-lookup"><span data-stu-id="56603-158">Run the page and enter an address.</span></span> <span data-ttu-id="56603-159">Stránka zobrazuje mapu založenou na Google Maps, která zobrazuje umístění, které jste zadali.</span><span class="sxs-lookup"><span data-stu-id="56603-159">The page displays a map, based on Google Maps, that shows the location that you specified.</span></span>

     ![mapování – 1](displaying-maps-in-an-aspnet-web-pages-site/_static/image2.png)

## <a name="creating-a-map-based-on-latitude-and-longitude-coordinates-using-bing"></a><span data-ttu-id="56603-161">Vytvoření mapy na základě souřadnic zeměpisné šířky a délky (pomocí Bingu)</span><span class="sxs-lookup"><span data-stu-id="56603-161">Creating a Map Based on Latitude and Longitude Coordinates (Using Bing)</span></span>

<span data-ttu-id="56603-162">Tento příklad ukazuje, jak vytvořit mapu založenou na souřadnicích.</span><span class="sxs-lookup"><span data-stu-id="56603-162">This example shows how to create a map based on coordinates.</span></span> <span data-ttu-id="56603-163">Tento příklad ukazuje, jak používat mapy Bing a jak klíč Bingu zahrnout.</span><span class="sxs-lookup"><span data-stu-id="56603-163">This example shows how to use Bing maps and how to include your Bing key.</span></span> <span data-ttu-id="56603-164">(Můžete také vytvořit mapu založenou na souřadnicích pomocí jiných mapových modulů, a to bez použití klíče Bingu.)</span><span class="sxs-lookup"><span data-stu-id="56603-164">(You can create a map based on coordinates using the other map engines also, without using a Bing key.)</span></span>

1. <span data-ttu-id="56603-165">V kořenovém adresáři lokality vytvořte soubor s názvem *MapCoordinates. cshtml* a nahraďte stávající obsah následujícím kódem a označením:</span><span class="sxs-lookup"><span data-stu-id="56603-165">Create a file named *MapCoordinates.cshtml* in the root of the site and replace the existing content with the following code and markup:</span></span>

    [!code-cshtml[Main](displaying-maps-in-an-aspnet-web-pages-site/samples/sample2.cshtml)]
2. <span data-ttu-id="56603-166">Nahraďte `your-key-here` klíčem mapy Bing, který jste předtím vygenerovali.</span><span class="sxs-lookup"><span data-stu-id="56603-166">Replace `your-key-here` with the Bing Maps key that you generated earlier.</span></span>
3. <span data-ttu-id="56603-167">Spusťte stránku *MapCoordinates. cshtml* , zadejte souřadnice zeměpisné šířky a délky a potom klikněte na **mapu IT!** .</span><span class="sxs-lookup"><span data-stu-id="56603-167">Run the *MapCoordinates.cshtml* page, enter latitude and longitude coordinates, and then click the **Map It!**</span></span> <span data-ttu-id="56603-168">.</span><span class="sxs-lookup"><span data-stu-id="56603-168">button.</span></span> <span data-ttu-id="56603-169">(Pokud neznáte žádné souřadnice, zkuste následující.</span><span class="sxs-lookup"><span data-stu-id="56603-169">(If you don't know any coordinates, try the following.</span></span> <span data-ttu-id="56603-170">Toto je umístění v areálu Microsoft Redmond.)</span><span class="sxs-lookup"><span data-stu-id="56603-170">This is a location on the Microsoft Redmond campus.)</span></span>

   - <span data-ttu-id="56603-171">Zeměpisná šířka: 47.6781005859375</span><span class="sxs-lookup"><span data-stu-id="56603-171">Latitude: 47.6781005859375</span></span>
   - <span data-ttu-id="56603-172">Zeměpisná délka: – 122.158317565918</span><span class="sxs-lookup"><span data-stu-id="56603-172">Longitude: -122.158317565918</span></span>

     <span data-ttu-id="56603-173">Stránka se zobrazí pomocí souřadnic, které jste zadali.</span><span class="sxs-lookup"><span data-stu-id="56603-173">The page is displayed using the coordinates that you specified.</span></span>

     ![mapování – 3](displaying-maps-in-an-aspnet-web-pages-site/_static/image3.png)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="56603-175">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="56603-175">Additional Resources</span></span>

[<span data-ttu-id="56603-176">Reference k rozhraní API Microsoft. Maps</span><span class="sxs-lookup"><span data-stu-id="56603-176">Microsoft.Maps API Reference</span></span>](https://msdn.microsoft.com/library/gg427611.aspx)

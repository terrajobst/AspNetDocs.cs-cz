---
uid: web-pages/overview/ui-layouts-and-themes/10-working-with-video
title: Zobrazení videa na webu ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Tato kapitola vysvětluje, jak zobrazit video na webových stránkách ASP.NET pomocí stránky syntaxe Razor.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 332fb3da-e2a5-460d-bb90-dd911e1e2c95
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/10-working-with-video
msc.type: authoredcontent
ms.openlocfilehash: 516d46f38ce8910209f4207c474b0404bf012950
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628945"
---
# <a name="displaying-video-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="f45d7-103">Zobrazení videa na webu ASP.NET Web Pages (Razor)</span><span class="sxs-lookup"><span data-stu-id="f45d7-103">Displaying Video in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="f45d7-104">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="f45d7-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="f45d7-105">Tento článek vysvětluje, jak pomocí přehrávače videa (Media) na webu ASP.NET Web Pages (Razor) umožnit uživatelům zobrazovat videa, která jsou uložená na webu.</span><span class="sxs-lookup"><span data-stu-id="f45d7-105">This article explains how to use a video (media) player in an ASP.NET Web Pages (Razor) website to let users view videos that are stored on the site.</span></span> <span data-ttu-id="f45d7-106">Webové stránky ASP.NET s syntaxe Razor vám umožní přehrávat videa Flash ( *. swf*), Media Player ( *. wmv*) a Silverlight ( *. xap*).</span><span class="sxs-lookup"><span data-stu-id="f45d7-106">ASP.NET Web Pages with Razor syntax lets you play Flash (*.swf*), Media Player (*.wmv*), and Silverlight (*.xap*) videos.</span></span>
> 
> <span data-ttu-id="f45d7-107">Naučíte se:</span><span class="sxs-lookup"><span data-stu-id="f45d7-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="f45d7-108">Jak zvolit přehrávač videa</span><span class="sxs-lookup"><span data-stu-id="f45d7-108">How to choose a video player.</span></span>
> - <span data-ttu-id="f45d7-109">Přidání videa na webovou stránku.</span><span class="sxs-lookup"><span data-stu-id="f45d7-109">How to add video to a web page.</span></span>
> - <span data-ttu-id="f45d7-110">Jak nastavit atributy přehrávače videa</span><span class="sxs-lookup"><span data-stu-id="f45d7-110">How to set video player attributes.</span></span>
> 
> <span data-ttu-id="f45d7-111">Jedná se o funkce ASP.NET Razor, které jsou představené v článku:</span><span class="sxs-lookup"><span data-stu-id="f45d7-111">These are the ASP.NET Razor pages features introduced in the article:</span></span>
> 
> - <span data-ttu-id="f45d7-112">Pomocná rutina `Video`</span><span class="sxs-lookup"><span data-stu-id="f45d7-112">The `Video` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f45d7-113">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="f45d7-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="f45d7-114">Webové stránky ASP.NET (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="f45d7-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="f45d7-115">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="f45d7-115">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="f45d7-116">V tomto kurzu se používá také WebMatrix 3.</span><span class="sxs-lookup"><span data-stu-id="f45d7-116">This tutorial also works with WebMatrix 3.</span></span>

## <a name="introduction"></a><span data-ttu-id="f45d7-117">Úvod</span><span class="sxs-lookup"><span data-stu-id="f45d7-117">Introduction</span></span>

<span data-ttu-id="f45d7-118">Možná budete chtít zobrazit na svém webu video.</span><span class="sxs-lookup"><span data-stu-id="f45d7-118">You might want to display a video on your site.</span></span> <span data-ttu-id="f45d7-119">To uděláte tak, že se připojíte k webu, který už video obsahuje, jako je YouTube.</span><span class="sxs-lookup"><span data-stu-id="f45d7-119">One way to do that is to link to a site that already has the video, like YouTube.</span></span> <span data-ttu-id="f45d7-120">Pokud chcete vložit video z těchto webů přímo na vlastní stránky, můžete z webu získat značku HTML a pak ho zkopírovat do své stránky.</span><span class="sxs-lookup"><span data-stu-id="f45d7-120">If you want to embed a video from these sites directly in your own pages, you can usually get HTML markup from the site and then copy it into your page.</span></span> <span data-ttu-id="f45d7-121">Například následující příklad ukazuje, jak vložit video na YouTube:</span><span class="sxs-lookup"><span data-stu-id="f45d7-121">For example, the following example shows how to embed a YouTube video:</span></span>

[!code-html[Main](10-working-with-video/samples/sample1.html?highlight=10-14)]

<span data-ttu-id="f45d7-122">Pokud si chcete přehrát video, které je na vašem vlastním webu (ne na veřejném webu pro sdílení videí), nemůžete na něj přímo odkazovat pomocí vloženého kódu, jako je to.</span><span class="sxs-lookup"><span data-stu-id="f45d7-122">If you want to play a video that's on your own website (not on a public video-sharing site), you can't directly link to it using embedded markup like this.</span></span> <span data-ttu-id="f45d7-123">Videa z webu však můžete přehrávat pomocí pomocníka `Video`, který vykresluje přehrávač médií přímo na stránce.</span><span class="sxs-lookup"><span data-stu-id="f45d7-123">However, you can play videos from your site by using the `Video` helper, which renders a media player directly in a page.</span></span>

<a id="Choosing_a_Video_Player"></a>
## <a name="choosing-a-video-player"></a><span data-ttu-id="f45d7-124">Výběr přehrávače videa</span><span class="sxs-lookup"><span data-stu-id="f45d7-124">Choosing a Video Player</span></span>

<span data-ttu-id="f45d7-125">Pro videosoubory existuje spousta formátů a každý formát obvykle vyžaduje jiný přehrávač a jiný způsob konfigurace přehrávače.</span><span class="sxs-lookup"><span data-stu-id="f45d7-125">There are lots of formats for video files, and each format typically requires a different player and a different way to configure the player.</span></span> <span data-ttu-id="f45d7-126">Na stránkách ASP.NET Razor můžete video přehrát na webové stránce pomocí pomocné rutiny `Video`.</span><span class="sxs-lookup"><span data-stu-id="f45d7-126">In ASP.NET Razor pages, you can play a video in a web page using the `Video` helper.</span></span> <span data-ttu-id="f45d7-127">Pomocná rutina `Video` zjednodušuje proces vkládání videí na webové stránce, protože automaticky generuje `object` a `embed` prvky HTML, které se obvykle používají k přidání videa na stránku.</span><span class="sxs-lookup"><span data-stu-id="f45d7-127">The `Video` helper simplifies the process of embedding videos in a web page because it automatically generates the `object` and `embed` HTML elements that are normally used to add video to the page.</span></span>

<span data-ttu-id="f45d7-128">Pomocná rutina `Video` podporuje následující mediální přehrávače:</span><span class="sxs-lookup"><span data-stu-id="f45d7-128">The `Video` helper supports the following media players:</span></span>

- <span data-ttu-id="f45d7-129">Adobe Flash</span><span class="sxs-lookup"><span data-stu-id="f45d7-129">Adobe Flash</span></span>
- <span data-ttu-id="f45d7-130">Windows MediaPlayer</span><span class="sxs-lookup"><span data-stu-id="f45d7-130">Windows MediaPlayer</span></span>
- <span data-ttu-id="f45d7-131">Microsoft Silverlight</span><span class="sxs-lookup"><span data-stu-id="f45d7-131">Microsoft Silverlight</span></span>

### <a name="the-flash-player"></a><span data-ttu-id="f45d7-132">Přehrávač Flash</span><span class="sxs-lookup"><span data-stu-id="f45d7-132">The Flash Player</span></span>

<span data-ttu-id="f45d7-133">`Flash` přehrávači pomocníka `Video` vám umožní přehrávat videa Flash (soubory *. swf* ) na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="f45d7-133">The `Flash` player of the `Video` helper let you play Flash videos (*.swf* files) in a web page.</span></span> <span data-ttu-id="f45d7-134">Je nutné zadat alespoň cestu k souboru videa.</span><span class="sxs-lookup"><span data-stu-id="f45d7-134">At a minimum, you have to provide a path to the video file.</span></span> <span data-ttu-id="f45d7-135">Pokud nezadáte nic, ale cesta, přehrávač použije výchozí hodnoty, které jsou nastavené aktuální verzí Flash.</span><span class="sxs-lookup"><span data-stu-id="f45d7-135">If you specify nothing but the path, the player uses default values that are set by the current version of Flash.</span></span> <span data-ttu-id="f45d7-136">Typická výchozí nastavení:</span><span class="sxs-lookup"><span data-stu-id="f45d7-136">Typical default settings are:</span></span>

- <span data-ttu-id="f45d7-137">Video se zobrazí s výchozí šířkou a výškou a bez barvy pozadí.</span><span class="sxs-lookup"><span data-stu-id="f45d7-137">The video is displayed using its default width and height and without a background color.</span></span>
- <span data-ttu-id="f45d7-138">Video se automaticky přehraje při načtení stránky.</span><span class="sxs-lookup"><span data-stu-id="f45d7-138">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="f45d7-139">Video se nepřetržitě zacykluje, dokud se explicitně nezastaví.</span><span class="sxs-lookup"><span data-stu-id="f45d7-139">The video loops continuously until it's explicitly stopped.</span></span>
- <span data-ttu-id="f45d7-140">Video se škáluje tak, aby se zobrazilo celé video, místo oříznutí videa tak, aby odpovídalo konkrétní velikosti.</span><span class="sxs-lookup"><span data-stu-id="f45d7-140">The video is scaled to show all of the video, rather than cropping the video to fit a specific size.</span></span>
- <span data-ttu-id="f45d7-141">Video se přehrává v okně.</span><span class="sxs-lookup"><span data-stu-id="f45d7-141">The video plays in a window.</span></span>

### <a name="the-mediaplayer-player"></a><span data-ttu-id="f45d7-142">Přehrávač MediaPlayer</span><span class="sxs-lookup"><span data-stu-id="f45d7-142">The MediaPlayer Player</span></span>

<span data-ttu-id="f45d7-143">`MediaPlayer` hráč pomocníka s `Video` vám umožní přehrávat videa Windows Media (soubory *. wmv* ), Windows Media Audio (soubory *. WMA* ) a MP3 (soubory *. mp3* ) na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="f45d7-143">The `MediaPlayer` player of the `Video` helper lets you play Windows Media videos (*.wmv* files), Windows Media audio (*.wma* files), and MP3 (*.mp3* files) in a web page.</span></span> <span data-ttu-id="f45d7-144">Je nutné zadat cestu k mediálnímu souboru, který se má přehrát. všechny ostatní parametry jsou volitelné.</span><span class="sxs-lookup"><span data-stu-id="f45d7-144">You must include path of the media file to play; all other parameters are optional.</span></span> <span data-ttu-id="f45d7-145">Pokud zadáte pouze cestu, přehrávač použije výchozí nastavení nastavené aktuální verzí MediaPlayer, například:</span><span class="sxs-lookup"><span data-stu-id="f45d7-145">If you specify only a path, the player uses default settings set by the current version of MediaPlayer, such as:</span></span>

- <span data-ttu-id="f45d7-146">Video se zobrazuje s výchozí šířkou a výškou.</span><span class="sxs-lookup"><span data-stu-id="f45d7-146">The video is displayed using its default width and height.</span></span>
- <span data-ttu-id="f45d7-147">Video se automaticky přehraje při načtení stránky.</span><span class="sxs-lookup"><span data-stu-id="f45d7-147">The video plays automatically when the page loads.</span></span>
- <span data-ttu-id="f45d7-148">Video se jednou přehrává (nejedná se o smyčku).</span><span class="sxs-lookup"><span data-stu-id="f45d7-148">The video plays once (it doesn't loop).</span></span>
- <span data-ttu-id="f45d7-149">Přehrávač zobrazuje úplnou sadu ovládacích prvků v uživatelském rozhraní.</span><span class="sxs-lookup"><span data-stu-id="f45d7-149">The player displays the full set of controls in the user interface.</span></span>
- <span data-ttu-id="f45d7-150">Video se přehrává v okně.</span><span class="sxs-lookup"><span data-stu-id="f45d7-150">The video plays in a window.</span></span>

### <a name="the-silverlight-player"></a><span data-ttu-id="f45d7-151">Přehrávač Silverlight</span><span class="sxs-lookup"><span data-stu-id="f45d7-151">The Silverlight Player</span></span>

<span data-ttu-id="f45d7-152">`Silverlight` přehrávači pomocníka s `Video` vám umožní přehrát Windows Media Video (soubory *. wmv* ), Windows Media Audio (soubory *. WMA* ) a MP3 (soubory *. mp3* ).</span><span class="sxs-lookup"><span data-stu-id="f45d7-152">The `Silverlight` player of the `Video` helper lets you play Windows Media Video (*.wmv* files), Windows Media Audio (*.wma* files), and MP3 (*.mp3* files).</span></span> <span data-ttu-id="f45d7-153">Je nutné nastavit parametr cesty tak, aby odkazoval na balíček aplikace založený na programu Silverlight (soubor *. xap* ).</span><span class="sxs-lookup"><span data-stu-id="f45d7-153">You must set the path parameter to point to a Silverlight-based application package (*.xap* file).</span></span> <span data-ttu-id="f45d7-154">Musíte také nastavit parametry Width a Height.</span><span class="sxs-lookup"><span data-stu-id="f45d7-154">You also must set the width and height parameters.</span></span> <span data-ttu-id="f45d7-155">Všechny ostatní parametry jsou volitelné.</span><span class="sxs-lookup"><span data-stu-id="f45d7-155">All other parameters are optional.</span></span> <span data-ttu-id="f45d7-156">Pokud použijete přehrávač Silverlight pro video, pokud nastavíte pouze požadované parametry, přehrávač Silverlight zobrazí video bez barvy pozadí.</span><span class="sxs-lookup"><span data-stu-id="f45d7-156">When you use the Silverlight player for video, if you set only the required parameters, the Silverlight player displays the video without a background color.</span></span>

> [!NOTE]
> <span data-ttu-id="f45d7-157">V případě, že Silverlight ještě neznáte: soubor *. xap* je komprimovaný soubor, který obsahuje pokyny k rozložení v souboru *. XAML* , spravovaný kód v sestaveních a volitelné prostředky.</span><span class="sxs-lookup"><span data-stu-id="f45d7-157">In case you don't already know Silverlight: the *.xap* file is a compressed file that contains layout instructions in a *.xaml* file, managed code in assemblies, and optional resources.</span></span> <span data-ttu-id="f45d7-158">V aplikaci Visual Studio můžete vytvořit soubor *. xap* jako projekt aplikace Silverlight.</span><span class="sxs-lookup"><span data-stu-id="f45d7-158">You can create a *.xap* file in Visual Studio as a Silverlight application project.</span></span>

<span data-ttu-id="f45d7-159">`Silverlight` přehrávač videa používá nastavení, která zadáte pro přehrávač, a nastavení, která jsou k dispozici v souboru *. xap* .</span><span class="sxs-lookup"><span data-stu-id="f45d7-159">The `Silverlight` video player uses both the settings that you provide for the player and the settings that are provided in the *.xap* file.</span></span>

> [!TIP] 
> 
> <a id="SB_MimeTypes"></a>
> ### <a name="mime-types"></a><span data-ttu-id="f45d7-160">Typy MIME</span><span class="sxs-lookup"><span data-stu-id="f45d7-160">MIME Types</span></span>
> 
> <span data-ttu-id="f45d7-161">Když prohlížeč stáhne soubor, prohlížeč zajistí, že typ souboru odpovídá typu MIME, který je zadaný pro dokument, který je vykreslený.</span><span class="sxs-lookup"><span data-stu-id="f45d7-161">When a browser downloads a file, the browser makes sure that the file type matches the MIME type that's specified for the document that's being rendered.</span></span> <span data-ttu-id="f45d7-162">Typ MIME je typ obsahu nebo typ média souboru.</span><span class="sxs-lookup"><span data-stu-id="f45d7-162">The MIME type is the content type or media type of a file.</span></span> <span data-ttu-id="f45d7-163">Pomoc `Video` používá následující typy MIME:</span><span class="sxs-lookup"><span data-stu-id="f45d7-163">The `Video` helper uses the following MIME types:</span></span>
> 
> - `application/x-shockwave-flash`
> - `application/x-mplayer2`
> - `application/x-silverlight-2`

<a id="Playing_Flash"></a>
## <a name="playing-flash-swf-videos"></a><span data-ttu-id="f45d7-164">Přehrávání videí pro Flash (. swf)</span><span class="sxs-lookup"><span data-stu-id="f45d7-164">Playing Flash (.swf) Videos</span></span>

<span data-ttu-id="f45d7-165">Tento postup ukazuje, jak přehrát video Flash s názvem *Sample. swf*.</span><span class="sxs-lookup"><span data-stu-id="f45d7-165">This procedure shows you how to play a Flash video named *sample.swf*.</span></span> <span data-ttu-id="f45d7-166">Procedura předpokládá, že máte na svém webu složku s názvem *Media* a že soubor *. swf* je v této složce.</span><span class="sxs-lookup"><span data-stu-id="f45d7-166">The procedure assumes that you've got a folder named *Media* on your site and that the *.swf* file is in that folder.</span></span>

1. <span data-ttu-id="f45d7-167">Přidejte knihovnu webových pomocníků ASP.NET na web, jak je popsáno v [tématu Instalace pomocníků na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste ho ještě nepřidali.</span><span class="sxs-lookup"><span data-stu-id="f45d7-167">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.</span></span>
2. <span data-ttu-id="f45d7-168">Na webu přidejte stránku a pojmenujte ji *FlashVideo. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="f45d7-168">In the website, add a page and name it *FlashVideo.cshtml*.</span></span>
3. <span data-ttu-id="f45d7-169">Přidejte na stránku následující kód:</span><span class="sxs-lookup"><span data-stu-id="f45d7-169">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample2.cshtml)]
4. <span data-ttu-id="f45d7-170">Spusťte stránku v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="f45d7-170">Run the page in a browser.</span></span> <span data-ttu-id="f45d7-171">(Před spuštěním se ujistěte, že je stránka vybraná v pracovním prostoru **soubory** .) Stránka se zobrazí a video se automaticky přehraje.</span><span class="sxs-lookup"><span data-stu-id="f45d7-171">(Make sure the page is selected in the **Files** workspace before you run it.) The page is displayed and the video plays automatically.</span></span> 

    <span data-ttu-id="f45d7-172">![obrazu](10-working-with-video/_static/image1.jpg "ch08_video -1. jpg")</span><span class="sxs-lookup"><span data-stu-id="f45d7-172">![[image]](10-working-with-video/_static/image1.jpg "ch08_video-1.jpg")</span></span>

<span data-ttu-id="f45d7-173">Můžete nastavit parametr `quality` pro video Flash na `low`, `autolow`, `autohigh`, `medium`, `high`a `best`:</span><span class="sxs-lookup"><span data-stu-id="f45d7-173">You can set the `quality` parameter for a Flash video to `low`, `autolow`, `autohigh`, `medium`, `high`, and `best`:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample3.cshtml)]

<span data-ttu-id="f45d7-174">Video Flash můžete změnit tak, aby se v konkrétní velikosti hrálo pomocí parametru `scale`, který můžete nastavit na následující:</span><span class="sxs-lookup"><span data-stu-id="f45d7-174">You can change the Flash video to play at a specific size using the `scale` parameter, which you can set to the following:</span></span>

- <span data-ttu-id="f45d7-175">`showall`.</span><span class="sxs-lookup"><span data-stu-id="f45d7-175">`showall`.</span></span> <span data-ttu-id="f45d7-176">Tím se zajistí, že se celé video zobrazí při zachování původního poměru stran.</span><span class="sxs-lookup"><span data-stu-id="f45d7-176">This makes the entire video visible while maintaining the original aspect ratio.</span></span> <span data-ttu-id="f45d7-177">Můžete ale končit ohraničením na každé straně.</span><span class="sxs-lookup"><span data-stu-id="f45d7-177">However, you might end up with borders on each side.</span></span>
- <span data-ttu-id="f45d7-178">`noorder`.</span><span class="sxs-lookup"><span data-stu-id="f45d7-178">`noorder`.</span></span> <span data-ttu-id="f45d7-179">Tím se zmenší video a zachová se původní poměr stran, ale může se oříznout.</span><span class="sxs-lookup"><span data-stu-id="f45d7-179">This scales the video while maintaining the original aspect ratio, but it might be cropped.</span></span>
- <span data-ttu-id="f45d7-180">`exactfit`.</span><span class="sxs-lookup"><span data-stu-id="f45d7-180">`exactfit`.</span></span> <span data-ttu-id="f45d7-181">Díky tomu se celé video zobrazí bez zachování původního poměru stran, ale může dojít k narušení.</span><span class="sxs-lookup"><span data-stu-id="f45d7-181">This makes the entire video visible without preserving the original aspect ratio, but distortion may occur.</span></span>

<span data-ttu-id="f45d7-182">Pokud nezadáte parametr `scale`, bude viditelné celé video a původní poměr stran bude udržován bez oříznutí.</span><span class="sxs-lookup"><span data-stu-id="f45d7-182">If you don't specify a `scale` parameter, the entire video will be visible and the original aspect ratio will be maintained without any cropping.</span></span> <span data-ttu-id="f45d7-183">Následující příklad ukazuje, jak použít parametr `scale`:</span><span class="sxs-lookup"><span data-stu-id="f45d7-183">The following example shows how to use the `scale` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample4.cshtml)]

<span data-ttu-id="f45d7-184">Přehrávač Flash podporuje nastavení grafického režimu s názvem `windowMode`.</span><span class="sxs-lookup"><span data-stu-id="f45d7-184">The Flash player supports a video mode setting named `windowMode`.</span></span> <span data-ttu-id="f45d7-185">Tuto možnost můžete nastavit na `window`, `opaque`a `transparent`.</span><span class="sxs-lookup"><span data-stu-id="f45d7-185">You can set this to `window`, `opaque`, and `transparent`.</span></span> <span data-ttu-id="f45d7-186">Ve výchozím nastavení je `windowMode` nastaveno na `window`, které zobrazí video v samostatném okně na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="f45d7-186">By default, the `windowMode` is set to `window`, which displays the video in a separate window on the web page.</span></span> <span data-ttu-id="f45d7-187">Nastavení `opaque` skrývá vše za videem na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="f45d7-187">The `opaque` setting hides everything behind the video on the web page.</span></span> <span data-ttu-id="f45d7-188">Nastavení `transparent` umožňuje zobrazit pozadí webové stránky pomocí videa za předpokladu, že část videa je průhledná.</span><span class="sxs-lookup"><span data-stu-id="f45d7-188">The `transparent` setting lets the background of the web page show through the video, assuming any part of the video is transparent.</span></span>

<a id="Playing_MediaPlayer"></a>
## <a name="playing-mediaplayer-wmv-videos"></a><span data-ttu-id="f45d7-189">Přehrávání videí MediaPlayer ( *. wmv*)</span><span class="sxs-lookup"><span data-stu-id="f45d7-189">Playing MediaPlayer (*.wmv*) Videos</span></span>

<span data-ttu-id="f45d7-190">Následující postup ukazuje, jak přehrát mediální video v okně s názvem *Sample. wmv* , které je ve složce *média* .</span><span class="sxs-lookup"><span data-stu-id="f45d7-190">The following procedure shows you how to play a Window Media video named *sample.wmv* that's in the *Media* folder.</span></span>

1. <span data-ttu-id="f45d7-191">Přidejte knihovnu webových pomocníků ASP.NET na web, jak je popsáno v [tématu Instalace pomocníků na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste to ještě neudělali.</span><span class="sxs-lookup"><span data-stu-id="f45d7-191">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="f45d7-192">Vytvořte novou stránku s názvem *MediaPlayerVideo. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="f45d7-192">Create a new page named *MediaPlayerVideo.cshtml*.</span></span>
3. <span data-ttu-id="f45d7-193">Přidejte na stránku následující kód:</span><span class="sxs-lookup"><span data-stu-id="f45d7-193">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample5.cshtml)]
4. <span data-ttu-id="f45d7-194">Spusťte stránku v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="f45d7-194">Run the page in a browser.</span></span> <span data-ttu-id="f45d7-195">Video se načte a automaticky přehraje.</span><span class="sxs-lookup"><span data-stu-id="f45d7-195">The video loads and plays automatically.</span></span> 

    <span data-ttu-id="f45d7-196">![obrazu](10-working-with-video/_static/image2.jpg "ch08_video -2. jpg")</span><span class="sxs-lookup"><span data-stu-id="f45d7-196">![[image]](10-working-with-video/_static/image2.jpg "ch08_video-2.jpg")</span></span>

<span data-ttu-id="f45d7-197">Můžete nastavit `playCount` na celé číslo, které určuje, kolikrát se má video automaticky přehrát:</span><span class="sxs-lookup"><span data-stu-id="f45d7-197">You can set `playCount` to an integer that indicates how many times to play the video automatically:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample6.cshtml)]

<span data-ttu-id="f45d7-198">Parametr `uiMode` umožňuje určit, které ovládací prvky se zobrazí v uživatelském rozhraní.</span><span class="sxs-lookup"><span data-stu-id="f45d7-198">The `uiMode` parameter lets you specify which controls show up in the user interface.</span></span> <span data-ttu-id="f45d7-199">`uiMode` můžete nastavit na `invisible`, `none`, `mini`nebo `full`.</span><span class="sxs-lookup"><span data-stu-id="f45d7-199">You can set `uiMode` to `invisible`, `none`, `mini`, or `full`.</span></span> <span data-ttu-id="f45d7-200">Pokud nezadáte parametr `uiMode`, bude se video zobrazovat spolu s oknem stav, panel hledání, řídicími tlačítky a ovládacími prvky hlasitosti kromě okna videa.</span><span class="sxs-lookup"><span data-stu-id="f45d7-200">If you don't specify a `uiMode` parameter, the video will be displayed with the status window, seek bar, control buttons, and volume controls in addition to the video window.</span></span> <span data-ttu-id="f45d7-201">Tyto ovládací prvky se zobrazí také v případě, že přehrávač použijete k přehrání zvukového souboru.</span><span class="sxs-lookup"><span data-stu-id="f45d7-201">These controls will also be displayed if you use the player to play an audio file.</span></span> <span data-ttu-id="f45d7-202">Tady je příklad, jak použít parametr `uiMode`:</span><span class="sxs-lookup"><span data-stu-id="f45d7-202">Here's an example of how to use the `uiMode` parameter:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample7.cshtml)]

<span data-ttu-id="f45d7-203">Zvuk je ve výchozím nastavení zapnutý, když video přehrává.</span><span class="sxs-lookup"><span data-stu-id="f45d7-203">By default, audio is on when the video plays.</span></span> <span data-ttu-id="f45d7-204">Zvuk můžete ztlumit nastavením parametru `mute` na hodnotu true:</span><span class="sxs-lookup"><span data-stu-id="f45d7-204">You can mute the audio by setting the `mute` parameter to true:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample8.cshtml)]

<span data-ttu-id="f45d7-205">Úroveň zvuku MediaPlayer videa můžete řídit nastavením parametru `volume` na hodnotu mezi 0 a 100.</span><span class="sxs-lookup"><span data-stu-id="f45d7-205">You can control the audio level of the MediaPlayer video by setting the `volume` parameter to a value between 0 and 100.</span></span> <span data-ttu-id="f45d7-206">Výchozí hodnota je 50.</span><span class="sxs-lookup"><span data-stu-id="f45d7-206">The default value is 50.</span></span> <span data-ttu-id="f45d7-207">Tady je příklad:</span><span class="sxs-lookup"><span data-stu-id="f45d7-207">Here's an example:</span></span>

[!code-cshtml[Main](10-working-with-video/samples/sample9.cshtml)]

<a id="Playing_Silverlight"></a>
## <a name="playing-silverlight-videos"></a><span data-ttu-id="f45d7-208">Přehrávání videí Silverlight</span><span class="sxs-lookup"><span data-stu-id="f45d7-208">Playing Silverlight Videos</span></span>

<span data-ttu-id="f45d7-209">Tento postup ukazuje, jak přehrát video obsažené na stránce Silverlight *. xap* nacházející se ve složce s názvem *Media*.</span><span class="sxs-lookup"><span data-stu-id="f45d7-209">This procedure shows you how to play video contained in a Silverlight *.xap* page that's in a folder named *Media*.</span></span>

1. <span data-ttu-id="f45d7-210">Přidejte knihovnu webových pomocníků ASP.NET na web, jak je popsáno v [tématu Instalace pomocníků na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste to ještě neudělali.</span><span class="sxs-lookup"><span data-stu-id="f45d7-210">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already .</span></span>
2. <span data-ttu-id="f45d7-211">Vytvořte novou stránku s názvem *SilverlightVideo. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="f45d7-211">Create a new page named *SilverlightVideo.cshtml*.</span></span>
3. <span data-ttu-id="f45d7-212">Přidejte na stránku následující kód:</span><span class="sxs-lookup"><span data-stu-id="f45d7-212">Add the following markup to the page:</span></span> 

    [!code-cshtml[Main](10-working-with-video/samples/sample10.cshtml)]
4. <span data-ttu-id="f45d7-213">Spusťte stránku v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="f45d7-213">Run the page in a browser.</span></span> 

    <span data-ttu-id="f45d7-214">![obrazu](10-working-with-video/_static/image3.jpg "ch08_video -3. jpg")</span><span class="sxs-lookup"><span data-stu-id="f45d7-214">![[image]](10-working-with-video/_static/image3.jpg "ch08_video-3.jpg")</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="f45d7-215">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="f45d7-215">Additional Resources</span></span>

<span data-ttu-id="f45d7-216">[Přehled programu Silverlight](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span><span class="sxs-lookup"><span data-stu-id="f45d7-216">[Silverlight Overview](https://msdn.microsoft.com/library/bb404700(VS.95).aspx)</span></span>

[<span data-ttu-id="f45d7-217">Atributy značek objektu Flash a vložení</span><span class="sxs-lookup"><span data-stu-id="f45d7-217">Flash OBJECT and EMBED tag attributes</span></span>](http://kb2.adobe.com/cps/127/tn_12701.html)

<span data-ttu-id="f45d7-218">[Windows Media Player 11 – značky parametrů sady SDK](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span><span class="sxs-lookup"><span data-stu-id="f45d7-218">[Windows Media Player 11 SDK PARAM Tags](https://msdn.microsoft.com/library/aa392321(VS.85).aspx)</span></span>

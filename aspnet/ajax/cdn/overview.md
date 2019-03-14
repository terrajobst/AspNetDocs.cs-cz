---
uid: ajax/cdn/overview
title: Síť pro doručování obsahu Microsoft Ajax | Dokumentace Microsoftu
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/14/2017
ms.assetid: 8935bf14-ca6d-4a4e-9dbe-b96ce74cef49
msc.legacyurl: /ajax/cdn
msc.type: content
ms.openlocfilehash: 65eee9bc477fc8adf10e8d819b93375ffbb72d7b
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57071995"
---
<a name="microsoft-ajax-content-delivery-network"></a><span data-ttu-id="d715a-102">Microsoft Ajax Content Delivery Network</span><span class="sxs-lookup"><span data-stu-id="d715a-102">Microsoft Ajax Content Delivery Network</span></span>
====================
> [!WARNING]
> <span data-ttu-id="d715a-103">Aplikace v produkčním prostředí, neměla by mít pevné závislosti prostředků CDN.</span><span class="sxs-lookup"><span data-stu-id="d715a-103">Production applications should not take a hard dependency on CDN assets.</span></span> <span data-ttu-id="d715a-104">Aplikace by měl test pro CDN asset odkazovat a záložní asset používat, pokud síť CDN není k dispozici.</span><span class="sxs-lookup"><span data-stu-id="d715a-104">Applications should test for the CDN asset referenced, and use a fallback asset when the CDN is not available.</span></span> 
>
> <span data-ttu-id="d715a-105">Microsoft Ajax CDN neuzavírá žádná smlouva SLA nenabízející používání Azure CDN.</span><span class="sxs-lookup"><span data-stu-id="d715a-105">The Microsoft Ajax CDN has no SLA above and beyond using an Azure CDN.</span></span>
>
> <span data-ttu-id="d715a-106">Použití [tento problém Githubu](https://github.com/aspnet/Docs/issues/5832) k hlášení problémů s Microsoft Ajax CDN.</span><span class="sxs-lookup"><span data-stu-id="d715a-106">Use [this GitHub issue](https://github.com/aspnet/Docs/issues/5832) to report problems with the Microsoft Ajax CDN.</span></span>

## <a name="table-of-contents"></a><span data-ttu-id="d715a-107">Obsah</span><span class="sxs-lookup"><span data-stu-id="d715a-107">Table of Contents</span></span>

<span data-ttu-id="d715a-108">**[Přejmenovat ajax.aspnetcdn.com adresu AJAX.microsoft.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span><span class="sxs-lookup"><span data-stu-id="d715a-108">**[ajax.microsoft.com renamed to ajax.aspnetcdn.com](#ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18)**</span></span>  
<span data-ttu-id="d715a-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span><span class="sxs-lookup"><span data-stu-id="d715a-109">**[Visual Studio .vsdoc Support](#Visual_Studio_vsdoc_Support_19)**</span></span>  
<span data-ttu-id="d715a-110">**[Pomocí prvku ASP.NET Ajax z CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span><span class="sxs-lookup"><span data-stu-id="d715a-110">**[Using ASP.NET Ajax from the CDN](#Using_ASPNET_Ajax_from_the_CDN_20)**</span></span>  
<span data-ttu-id="d715a-111">**[Pomocí jQuery z CDN](#Using_jQuery_from_the_CDN_21)**</span><span class="sxs-lookup"><span data-stu-id="d715a-111">**[Using jQuery from the CDN](#Using_jQuery_from_the_CDN_21)**</span></span>  
<span data-ttu-id="d715a-112">**[Pomocí jQuery UI z CDN](#Using_jQuery_UI_from_the_CDN_22)**</span><span class="sxs-lookup"><span data-stu-id="d715a-112">**[Using jQuery UI from the CDN](#Using_jQuery_UI_from_the_CDN_22)**</span></span>  
<span data-ttu-id="d715a-113">**[Soubory třetích stran v síti CDN](#Third-Party_Files_on_the_CDN_23)**</span><span class="sxs-lookup"><span data-stu-id="d715a-113">**[Third-Party Files on the CDN](#Third-Party_Files_on_the_CDN_23)**</span></span>  
  
 [<span data-ttu-id="d715a-114">jQuery verze v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-114">jQuery Releases on the CDN</span></span>](#jQuery_Releases_on_the_CDN_0)  
 [<span data-ttu-id="d715a-115">jQuery verze migrace v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-115">jQuery Migrate Releases on the CDN</span></span>](#jQuery_Migrate_Releases_on_the_CDN_1)  
 [<span data-ttu-id="d715a-116">jQuery verze uživatelského rozhraní v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-116">jQuery UI Releases on the CDN</span></span>](#jQuery_UI_Releases_on_the_CDN_2)  
 [<span data-ttu-id="d715a-117">jQuery verze ověření v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-117">jQuery Validation Releases on the CDN</span></span>](#jQuery_Validation_Releases_on_the_CDN_3)  
 [<span data-ttu-id="d715a-118">jQuery Mobile verze v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-118">jQuery Mobile Releases on the CDN</span></span>](#jQuery_Mobile_Releases_on_the_CDN_4)  
 [<span data-ttu-id="d715a-119">jQuery šablony vydané verze v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-119">jQuery Templates Releases on the CDN</span></span>](#jQuery_Templates_Releases_on_the_CDN_5)  
 [<span data-ttu-id="d715a-120">jQuery cyklu vydání v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-120">jQuery Cycle Releases on the CDN</span></span>](#jQuery_Cycle_Releases_on_the_CDN_6)  
 [<span data-ttu-id="d715a-121">jQuery DataTables vydané verze v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-121">jQuery DataTables Releases on the CDN</span></span>](#jQuery_DataTables_Releases_on_the_CDN_7)  
 [<span data-ttu-id="d715a-122">Verze Modernizr v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-122">Modernizr Releases on the CDN</span></span>](#Modernizr_Releases_on_the_CDN_8)  
 [<span data-ttu-id="d715a-123">Verze JSHint v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-123">JSHint Releases on the CDN</span></span>](#JSHint_Releases_on_the_CDN_10)  
 [<span data-ttu-id="d715a-124">Verze knockout v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-124">Knockout Releases on the CDN</span></span>](#Knockout_Releases_on_the_CDN_11)  
 [<span data-ttu-id="d715a-125">Globalizace vydané verze v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-125">Globalize Releases on the CDN</span></span>](#Globalize_Releases_on_the_CDN_12)  
 [<span data-ttu-id="d715a-126">Reakce vydané verze v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-126">Respond Releases on the CDN</span></span>](#Respond_Releases_on_the_CDN_13)  
 [<span data-ttu-id="d715a-127">Spuštění vydané verze v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-127">Bootstrap Releases on the CDN</span></span>](#Bootstrap_Releases_on_the_CDN_14)  
 [<span data-ttu-id="d715a-128">Spuštění TouchCarousel vydané verze v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-128">Bootstrap TouchCarousel Releases on the CDN</span></span>](#BootstrapTouchCarousel_Releases_on_the_CDN_18)  
 [<span data-ttu-id="d715a-129">Verze hammer.js v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-129">Hammer.js Releases on the CDN</span></span>](#Hammerjs_Releases_on_the_CDN_19)  
 [<span data-ttu-id="d715a-130">Webové formuláře ASP.NET a Ajax vydané verze v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-130">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>](#ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15)  
 [<span data-ttu-id="d715a-131">Verze technologie ASP.NET MVC v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-131">ASP.NET MVC Releases on the CDN</span></span>](#ASPNET_MVC_Releases_on_the_CDN_16)  
 [<span data-ttu-id="d715a-132">Verze funkce SignalR technologie ASP.NET ve službě CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-132">ASP.NET SignalR Releases on the CDN</span></span>](#ASPNET_SignalR_Releases_on_the_CDN_17)

<span data-ttu-id="d715a-133">Microsoft Ajax Content Delivery Network (CDN) hostuje knihovny JavaScript oblíbených třetích stran, jako je jQuery a umožňuje snadno přidat je do vašich webových aplikací.</span><span class="sxs-lookup"><span data-stu-id="d715a-133">The Microsoft Ajax Content Delivery Network (CDN) hosts popular third party JavaScript libraries such as jQuery and enables you to easily add them to your Web applications.</span></span> <span data-ttu-id="d715a-134">Například můžete začít používat jQuery, která je hostována na této sítě CDN. jednoduše tak, že přidáte &lt;skript&gt; značky na stránku, která odkazuje na ajax.aspnetcdn.com.</span><span class="sxs-lookup"><span data-stu-id="d715a-134">For example, you can start using jQuery which is hosted on this CDN simply by adding a &lt;script&gt; tag to your page that points to ajax.aspnetcdn.com.</span></span>

<span data-ttu-id="d715a-135">Díky využití CDN může výrazně zlepšit výkon aplikací Ajax.</span><span class="sxs-lookup"><span data-stu-id="d715a-135">By taking advantage of the CDN, you can significantly improve the performance of your Ajax applications.</span></span> <span data-ttu-id="d715a-136">Obsah z CDN jsou ukládány do mezipaměti na serverech umístěných po celém světě.</span><span class="sxs-lookup"><span data-stu-id="d715a-136">The contents of the CDN are cached on servers located around the world.</span></span> <span data-ttu-id="d715a-137">Kromě toho umožňuje CDN prohlížečům soubory jazyka JavaScript v mezipaměti třetích stran pro weby, které se nacházejí v různých doménách.</span><span class="sxs-lookup"><span data-stu-id="d715a-137">In addition, the CDN enables browsers to reuse cached third party JavaScript files for web sites that are located in different domains.</span></span>

<span data-ttu-id="d715a-138">V případě, že budete muset poskytnout webové stránky s použitím Secure Sockets Layer, podporuje CDN SSL (HTTPS).</span><span class="sxs-lookup"><span data-stu-id="d715a-138">The CDN supports SSL (HTTPS) in case you need to serve a web page using the Secure Sockets Layer.</span></span>

<span data-ttu-id="d715a-139">CDN hostitelem následující skript knihovny třetích stran, které byly odeslány a mají licenci, vlastníky těchto knihoven:</span><span class="sxs-lookup"><span data-stu-id="d715a-139">The CDN hosts the following third party script libraries which have been uploaded, and are licensed to you, by the owners of those libraries:</span></span>

- <span data-ttu-id="d715a-140">jQuery (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="d715a-140">jQuery (www.jquery.com)</span></span>
- <span data-ttu-id="d715a-141">jQuery UI (www.jqueryui.com)</span><span class="sxs-lookup"><span data-stu-id="d715a-141">jQuery UI (www.jqueryui.com)</span></span>
- <span data-ttu-id="d715a-142">jQuery Mobile (www.jquerymobile.com)</span><span class="sxs-lookup"><span data-stu-id="d715a-142">jQuery Mobile (www.jquerymobile.com)</span></span>
- <span data-ttu-id="d715a-143">jQuery ověření (www.jquery.com)</span><span class="sxs-lookup"><span data-stu-id="d715a-143">jQuery Validation (www.jquery.com)</span></span>
- <span data-ttu-id="d715a-144">jQuery cyklu (www.malsup.com/jquery/cycle/)</span><span class="sxs-lookup"><span data-stu-id="d715a-144">jQuery Cycle (www.malsup.com/jquery/cycle/)</span></span>
- <span data-ttu-id="d715a-145">jQuery DataTables (http://datatables.net/)</span><span class="sxs-lookup"><span data-stu-id="d715a-145">jQuery DataTables (http://datatables.net/)</span></span>

<span data-ttu-id="d715a-146">Microsoft Ajax CDN také zahrnuje následující knihovny, které byly odeslány společnosti Microsoft:</span><span class="sxs-lookup"><span data-stu-id="d715a-146">The Microsoft Ajax CDN also includes the following libraries which have been uploaded by Microsoft:</span></span>

- <span data-ttu-id="d715a-147">ASP.NET Ajax</span><span class="sxs-lookup"><span data-stu-id="d715a-147">ASP.NET Ajax</span></span>
- <span data-ttu-id="d715a-148">Soubory jazyka JavaScript technologie ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="d715a-148">ASP.NET MVC JavaScript Files</span></span>
- <span data-ttu-id="d715a-149">Soubory ASP.NET SignalR JavaScript</span><span class="sxs-lookup"><span data-stu-id="d715a-149">ASP.NET SignalR JavaScript Files</span></span>

<span data-ttu-id="d715a-150">Společnost Microsoft nečiní nárok na vlastnictví všechny knihovny třetích stran, které jsou hostované na této sítě CDN.</span><span class="sxs-lookup"><span data-stu-id="d715a-150">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="d715a-151">O autorských právech vlastníky knihoven licencují tyto knihovny pro vás.</span><span class="sxs-lookup"><span data-stu-id="d715a-151">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="d715a-152">Veškerá práva, která bude pravděpodobně nutné stáhnout a použít tyto knihovny jsou udělena pouze podle vlastníků o autorských právech.</span><span class="sxs-lookup"><span data-stu-id="d715a-152">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="d715a-153">Protože se nejedná knihoven Microsoftu, společnost Microsoft poskytuje žádné záruky ani licence práv duševního vlastnictví (včetně implicitní patentová práva) pro knihovny třetích stran, který je hostitelem této sítě CDN.</span><span class="sxs-lookup"><span data-stu-id="d715a-153">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<span data-ttu-id="d715a-154">Pokud chcete předložit knihovny jazyka JavaScript a knihovny je součástí hlavní knihovny jazyka JavaScript (jak je uvedeno na http://trends.builtwith.com) nebo rozšíření/modulů plug-in pro tyto knihovny, které mají (a) Oblíbené; nebo (b) užitečné při použití technologie ASP.NET a obraťte se prosím na AjaxCDNSubmission@Microsoft.com.</span><span class="sxs-lookup"><span data-stu-id="d715a-154">If you wish to submit your JavaScript library and your library is one of the top JavaScript libraries (as listed on http://trends.builtwith.com) or extensions/plugins to these libraries that are (a) popular; or (b) helpful for use on ASP.NET then please contact AjaxCDNSubmission@Microsoft.com.</span></span>

<a id="ajaxmicrosoftcom_renamed_to_ajaxaspnetcdncom_18"></a>

## <a name="ajaxmicrosoftcom-renamed-to-ajaxaspnetcdncom"></a><span data-ttu-id="d715a-155">Přejmenovat ajax.aspnetcdn.com adresu AJAX.microsoft.com</span><span class="sxs-lookup"><span data-stu-id="d715a-155">ajax.microsoft.com renamed to ajax.aspnetcdn.com</span></span>

<span data-ttu-id="d715a-156">Síť CDN lze použít název domény webu microsoft.com a byla změněna na název domény aspnetcdn.com použijte.</span><span class="sxs-lookup"><span data-stu-id="d715a-156">The CDN used to use the microsoft.com domain name and has been changed to use the aspnetcdn.com domain name.</span></span> <span data-ttu-id="d715a-157">Tato změna byla provedena ke zvýšení výkonu, protože při odkazování doménu microsoft.com prohlížeči by se odesílat žádné soubory cookie z této domény sítí s každou žádostí.</span><span class="sxs-lookup"><span data-stu-id="d715a-157">This change was made to increase performance because when a browser referenced the microsoft.com domain it would send any cookies from that domain across the wire with each request.</span></span> <span data-ttu-id="d715a-158">Přejmenováním na název domény než microsoft.com je možné zvýšit výkon podle největší 25 %.</span><span class="sxs-lookup"><span data-stu-id="d715a-158">By renaming to a domain name other than microsoft.com performance can be increased by as much to 25%.</span></span> <span data-ttu-id="d715a-159">Poznamenejte si adresu ajax.microsoft.com budou i nadále fungovat, ale doporučuje se ajax.aspnetcdn.com.</span><span class="sxs-lookup"><span data-stu-id="d715a-159">Note ajax.microsoft.com will continue to function but ajax.aspnetcdn.com is recommended.</span></span>

- <span data-ttu-id="d715a-160">Starý formát: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="d715a-160">Old Format: https://ajax.microsoft.com/ajax/jQuery/jquery-1.8.0.js</span></span>
- <span data-ttu-id="d715a-161">Nový formát: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span><span class="sxs-lookup"><span data-stu-id="d715a-161">New Format: https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js</span></span>

<a id="Visual_Studio_vsdoc_Support_19"></a>

## <a name="visual-studio-vsdoc-support"></a><span data-ttu-id="d715a-162">Podpora .vsdoc sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="d715a-162">Visual Studio .vsdoc Support</span></span>

<span data-ttu-id="d715a-163">Použití souborů .vsdoc správně za použití Visual Studia 2008 potřebujete, abyste měli jistotu, že máte aktualizaci VS 2008 SP1 nainstalovány a oprava hotfix pro vsdoc soubory.</span><span class="sxs-lookup"><span data-stu-id="d715a-163">To use the .vsdoc files properly with Visual Studio 2008 you need to make sure that you have VS 2008 SP1 installed and the hotfix for vsdoc files installed.</span></span> <span data-ttu-id="d715a-164">Můžete získat z tohoto umístění:</span><span class="sxs-lookup"><span data-stu-id="d715a-164">You can get these from here:</span></span>

- [<span data-ttu-id="d715a-165">Stáhněte si Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="d715a-165">Download Visual Studio 2008 SP1</span></span>](https://www.microsoft.com/downloads/en/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en "Stáhnout Visual Studio 2008 SP1")
- [<span data-ttu-id="d715a-166">Stažení opravy hotfix .vsdoc pro Visual Studio 2008 SP1</span><span class="sxs-lookup"><span data-stu-id="d715a-166">Download .vsdoc hotfix for Visual Studio 2008 SP1</span></span>](https://code.msdn.microsoft.com/KB958502/Release/ProjectReleases.aspx?ReleaseId=1736 "stažení opravy hotfix .vsdoc pro Visual Studio 2008 SP1")

<span data-ttu-id="d715a-167">Visual Studio 2010 podporuje .vsdoc soubory bez jakékoli další opravy.</span><span class="sxs-lookup"><span data-stu-id="d715a-167">Visual Studio 2010 supports .vsdoc files without any additional patches.</span></span>

<a id="Using_ASPNET_Ajax_from_the_CDN_20"></a>

## <a name="using-aspnet-ajax-from-the-cdn"></a><span data-ttu-id="d715a-168">Pomocí prvku ASP.NET Ajax z CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-168">Using ASP.NET Ajax from the CDN</span></span>

<span data-ttu-id="d715a-169">Při použití technologie ASP.NET 4, můžete přesměrovat všechny požadavky technologie ASP.NET framework skriptů do CDN.</span><span class="sxs-lookup"><span data-stu-id="d715a-169">When using ASP.NET 4, you can redirect all requests for ASP.NET framework scripts to the CDN.</span></span> <span data-ttu-id="d715a-170">Načítání skriptů z CDN místo místní webový server může výrazně zlepšit výkon veřejné weby technologie ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d715a-170">Retrieving scripts from the CDN instead of your local web server can substantially improve the performance of public ASP.NET websites.</span></span>

<span data-ttu-id="d715a-171">Použijte vlastnost ScriptManager EnableCDN přesměrovat požadavky ASP.NET framework skript do Microsoft Ajax CDN:</span><span class="sxs-lookup"><span data-stu-id="d715a-171">Use the ScriptManager EnableCDN property to redirect all ASP.NET framework script requests to the Microsoft Ajax CDN:</span></span>

[!code-aspx[Main](overview/samples/sample1.aspx)]

<a id="Using_jQuery_from_the_CDN_21"></a>

## <a name="using-jquery-from-the-cdn"></a><span data-ttu-id="d715a-172">Pomocí jQuery z CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-172">Using jQuery from the CDN</span></span>

<span data-ttu-id="d715a-173">Můžete použít skripty jQuery hostované ve službě CDN ve vaší webové aplikaci tak, že přidáte následující element script na stránku:</span><span class="sxs-lookup"><span data-stu-id="d715a-173">You can use jQuery scripts hosted on CDN in your Web application by adding the following script element to a page:</span></span>

[!code-html[Main](overview/samples/sample2.html)]

<span data-ttu-id="d715a-174">CDN také obsahuje minifikovaný verzi jQuery skript, který můžete získat pomocí následujícího elementu:</span><span class="sxs-lookup"><span data-stu-id="d715a-174">The CDN also includes the minified version of the jQuery script, which you can get using the following element:</span></span>

[!code-html[Main](overview/samples/sample3.html)]

<span data-ttu-id="d715a-175">Pokud chcete povolit stránku pro použití náhradní lokality pro načítání jQuery z místní cesty na svůj vlastní web, pokud síť CDN se stane nedostupný, přidejte následující prvek ihned po element odkazující na CDN:</span><span class="sxs-lookup"><span data-stu-id="d715a-175">To allow your page to fallback to loading jQuery from a local path on your own website if the CDN happens to be unavailable, add the following element immediately after the element referencing the CDN:</span></span>

[!code-html[Main](overview/samples/sample4.html)]

<span data-ttu-id="d715a-176">Následující stránka s ukázkou používá k zobrazení obsahu elementu div při kliknutí na tlačítko CDN verzi knihovny jQuery (pomocí nouzového řešení ověření pomocí místní kopie).</span><span class="sxs-lookup"><span data-stu-id="d715a-176">The following sample page uses the CDN version of the jQuery library (with fallback to a local copy) to display the contents of a div element when a button is clicked.</span></span>

[!code-html[Main](overview/samples/sample5.html)]

<span data-ttu-id="d715a-177">Můžete získat další informace o jQuery a stáhněte si místní kopii jQuery návštěvou [jQuery](http://jquery.com/) webu.</span><span class="sxs-lookup"><span data-stu-id="d715a-177">You can learn more about jQuery and download a local copy of jQuery by visiting the [jQuery](http://jquery.com/) Web site.</span></span>

<a id="Using_jQuery_UI_from_the_CDN_22"></a>

## <a name="using-jquery-ui-from-the-cdn"></a><span data-ttu-id="d715a-178">Pomocí jQuery UI z CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-178">Using jQuery UI from the CDN</span></span>

<span data-ttu-id="d715a-179">CDN také hostitelem knihovna uživatelského rozhraní jQuery.</span><span class="sxs-lookup"><span data-stu-id="d715a-179">The CDN also hosts the jQuery UI library.</span></span> <span data-ttu-id="d715a-180">Knihovna uživatelského rozhraní jQuery obsahuje bohatou sadu pomůcek a efekty, které můžete použít ve svých aplikacích technologie ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="d715a-180">The jQuery UI library includes a rich set of widgets and effects that you can use in your ASP.NET applications.</span></span> <span data-ttu-id="d715a-181">Například na následující stránce ukazuje, jak je možné používat jQuery UI Datepicker v kontextu aplikace webových formulářů ASP.NET zobrazíte rozevírací kalendář:</span><span class="sxs-lookup"><span data-stu-id="d715a-181">For example, the following page illustrates how you can use the jQuery UI Datepicker in the context of an ASP.NET Web Forms application to display a pop-up calendar:</span></span>

[!code-aspx[Main](overview/samples/sample6.aspx)]

<span data-ttu-id="d715a-182">Když přesunete fokus do textového pole pomocí klávesnice, zobrazí se kalendáře:</span><span class="sxs-lookup"><span data-stu-id="d715a-182">When you move focus to the TextBox using your keyboard, a calendar is displayed:</span></span>

![Překryvný kalendář s prvkem Datepicker vytvořili](overview/_static/image1.png)

<span data-ttu-id="d715a-184">Všimněte si, že musí obsahovat tři soubory z CDN ve výše uvedeném kódu:</span><span class="sxs-lookup"><span data-stu-id="d715a-184">Notice that you must include three files from the CDN in the code above:</span></span>

- <span data-ttu-id="d715a-185">Knihovna jQuery &mdash; knihovna uživatelského rozhraní jQuery závisí na knihovny jQuery.</span><span class="sxs-lookup"><span data-stu-id="d715a-185">The jQuery library &mdash; The jQuery UI library depends on the jQuery library.</span></span> <span data-ttu-id="d715a-186">Knihovna jQuery musíte přidat na stránku předtím, než přidáte knihovna uživatelského rozhraní jQuery.</span><span class="sxs-lookup"><span data-stu-id="d715a-186">You must add the jQuery library to your page before you add the jQuery UI library.</span></span>
- <span data-ttu-id="d715a-187">Knihovna uživatelského rozhraní jQuery &mdash; knihovna uživatelského rozhraní jQuery obsahuje všechny účinky uživatelské rozhraní jQuery a widgetů, například ovládací prvek Datepicker widgetu použity na stránce výše.</span><span class="sxs-lookup"><span data-stu-id="d715a-187">The jQuery UI library &mdash; The jQuery UI library contains all of the jQuery UI effects and widgets such as the Datepicker widget used in the page above.</span></span>
- <span data-ttu-id="d715a-188">Motiv uživatelského rozhraní jQuery &mdash; uživatelské rozhraní jQuery podporuje různé motivy.</span><span class="sxs-lookup"><span data-stu-id="d715a-188">A jQuery UI theme &mdash; The jQuery UI supports different themes.</span></span> <span data-ttu-id="d715a-189">Výše uvedené stránka obsahuje odkaz na soubor šablony stylů CSS pro import motivu Redmondu.</span><span class="sxs-lookup"><span data-stu-id="d715a-189">The page above includes a link to a CSS file to import the Redmond theme.</span></span>

<span data-ttu-id="d715a-190">Všechny motivy uživatelské rozhraní jQuery standardní jsou hostované v síti CDN.</span><span class="sxs-lookup"><span data-stu-id="d715a-190">All of the standard jQuery UI themes are hosted on the CDN.</span></span> <span data-ttu-id="d715a-191">[Tuto stránku](jquery-ui/cdnjqueryui1910.md "uživatelské rozhraní jQuery 1.8.10 ve službě Microsoft Ajax CDN") Chcete-li zobrazit miniatury pro každý motiv.</span><span class="sxs-lookup"><span data-stu-id="d715a-191">[Visit this page](jquery-ui/cdnjqueryui1910.md "jQuery UI 1.8.10 on the Microsoft Ajax CDN") to view thumbnails for each theme.</span></span>

<span data-ttu-id="d715a-192">Další informace o knihovně uživatelské rozhraní jQuery, navštivte oficiální [webu uživatelské rozhraní jQuery](http://jQueryUI.com "webu uživatelské rozhraní jQuery").</span><span class="sxs-lookup"><span data-stu-id="d715a-192">To learn more about the jQuery UI library, visit the official [jQuery UI website](http://jQueryUI.com "jQuery UI website").</span></span>

<a id="Third-Party_Files_on_the_CDN_23"></a>

## <a name="third-party-files-on-the-cdn"></a><span data-ttu-id="d715a-193">Soubory třetích stran v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-193">Third-Party Files on the CDN</span></span>

<span data-ttu-id="d715a-194">CDN je hostitelem některé z Oblíbené knihovny jazyka JavaScript třetích stran.</span><span class="sxs-lookup"><span data-stu-id="d715a-194">The CDN hosts some of the most popular third party JavaScript libraries.</span></span> <span data-ttu-id="d715a-195">Společnost Microsoft nečiní nárok na vlastnictví všechny knihovny třetích stran, které jsou hostované na této sítě CDN.</span><span class="sxs-lookup"><span data-stu-id="d715a-195">Microsoft does not claim ownership of any third-party libraries hosted on this CDN.</span></span> <span data-ttu-id="d715a-196">O autorských právech vlastníky knihoven licencují tyto knihovny pro vás.</span><span class="sxs-lookup"><span data-stu-id="d715a-196">The copyright owners of the libraries are licensing these libraries to you.</span></span> <span data-ttu-id="d715a-197">Veškerá práva, která bude pravděpodobně nutné stáhnout a použít tyto knihovny jsou udělena pouze podle vlastníků o autorských právech.</span><span class="sxs-lookup"><span data-stu-id="d715a-197">Any rights that you may have to download and use such libraries are granted solely by the respective copyright owners.</span></span> <span data-ttu-id="d715a-198">Protože se nejedná knihoven Microsoftu, společnost Microsoft poskytuje žádné záruky ani licence práv duševního vlastnictví (včetně implicitní patentová práva) pro knihovny třetích stran, který je hostitelem této sítě CDN.</span><span class="sxs-lookup"><span data-stu-id="d715a-198">Because these are not Microsoft libraries, Microsoft provides no warranties or intellectual property rights licenses (including no implied patent rights) for the third party libraries hosted on this CDN.</span></span>

<a id="jQuery_Releases_on_the_CDN_0"></a>

### <a name="jquery-releases-on-the-cdn"></a><span data-ttu-id="d715a-199">jQuery verze v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-199">jQuery Releases on the CDN</span></span>

<span data-ttu-id="d715a-200">Tyto verze jQuery jsou hostované v síti CDN:</span><span class="sxs-lookup"><span data-stu-id="d715a-200">The following releases of jQuery are hosted on the CDN:</span></span>

#### <a name="jquery-version-331"></a><span data-ttu-id="d715a-201">jQuery verze 3.3.1</span><span class="sxs-lookup"><span data-stu-id="d715a-201">jQuery version 3.3.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.3.1.slim.min.map

#### <a name="jquery-version-321"></a><span data-ttu-id="d715a-202">jQuery verze 3.2.1</span><span class="sxs-lookup"><span data-stu-id="d715a-202">jQuery version 3.2.1</span></span>
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.1.slim.min.map

#### <a name="jquery-version-320"></a><span data-ttu-id="d715a-203">jQuery verze 3.2.0</span><span class="sxs-lookup"><span data-stu-id="d715a-203">jQuery version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.2.0.slim.min.map

#### <a name="jquery-version-311"></a><span data-ttu-id="d715a-204">jQuery verze 3.1.1</span><span class="sxs-lookup"><span data-stu-id="d715a-204">jQuery version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.1.slim.min.map

#### <a name="jquery-version-310"></a><span data-ttu-id="d715a-205">jQuery verze 3.1.0</span><span class="sxs-lookup"><span data-stu-id="d715a-205">jQuery version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.1.0.slim.min.map

#### <a name="jquery-version-300"></a><span data-ttu-id="d715a-206">jQuery verze 3.0.0</span><span class="sxs-lookup"><span data-stu-id="d715a-206">jQuery version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.min.map
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-3.0.0.slim.min.map

#### <a name="jquery-version-224"></a><span data-ttu-id="d715a-207">jQuery verze 2.2.4</span><span class="sxs-lookup"><span data-stu-id="d715a-207">jQuery version 2.2.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.4.min.map

#### <a name="jquery-version-223"></a><span data-ttu-id="d715a-208">jQuery version 2.2.3</span><span class="sxs-lookup"><span data-stu-id="d715a-208">jQuery version 2.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.3.min.map

#### <a name="jquery-version-222"></a><span data-ttu-id="d715a-209">jQuery verze 2.2.2</span><span class="sxs-lookup"><span data-stu-id="d715a-209">jQuery version 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.2.min.map

#### <a name="jquery-version-221"></a><span data-ttu-id="d715a-210">jQuery verze 2.2.1</span><span class="sxs-lookup"><span data-stu-id="d715a-210">jQuery version 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.1.min.map

#### <a name="jquery-version-220"></a><span data-ttu-id="d715a-211">jQuery verze 2.2.0</span><span class="sxs-lookup"><span data-stu-id="d715a-211">jQuery version 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.2.0.min.map

#### <a name="jquery-version-214"></a><span data-ttu-id="d715a-212">jQuery verzi 2.1.4</span><span class="sxs-lookup"><span data-stu-id="d715a-212">jQuery version 2.1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.4.min.map

#### <a name="jquery-version-213"></a><span data-ttu-id="d715a-213">jQuery verze 2.1.3</span><span class="sxs-lookup"><span data-stu-id="d715a-213">jQuery version 2.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.3.min.map

#### <a name="jquery-version-212"></a><span data-ttu-id="d715a-214">jQuery verze 2.1.2</span><span class="sxs-lookup"><span data-stu-id="d715a-214">jQuery version 2.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.2.min.js

#### <a name="jquery-version-211"></a><span data-ttu-id="d715a-215">jQuery verze 2.1.1</span><span class="sxs-lookup"><span data-stu-id="d715a-215">jQuery version 2.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.1.min.map

#### <a name="jquery-version-210"></a><span data-ttu-id="d715a-216">verze 2.1.0 jQuery</span><span class="sxs-lookup"><span data-stu-id="d715a-216">jQuery version 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.1.0.min.map

#### <a name="jquery-version-203"></a><span data-ttu-id="d715a-217">jQuery version 2.0.3</span><span class="sxs-lookup"><span data-stu-id="d715a-217">jQuery version 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.3.min.map

#### <a name="jquery-version-202"></a><span data-ttu-id="d715a-218">jQuery verze bodu 2.0.2</span><span class="sxs-lookup"><span data-stu-id="d715a-218">jQuery version 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.2.min.map

#### <a name="jquery-version-201"></a><span data-ttu-id="d715a-219">verze jQuery 2.0.1</span><span class="sxs-lookup"><span data-stu-id="d715a-219">jQuery version 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.1.min.map

#### <a name="jquery-version-200"></a><span data-ttu-id="d715a-220">jQuery verze 2.0.0</span><span class="sxs-lookup"><span data-stu-id="d715a-220">jQuery version 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-2.0.0.min.map

#### <a name="jquery-version-1124"></a><span data-ttu-id="d715a-221">jQuery verze 1.12.4</span><span class="sxs-lookup"><span data-stu-id="d715a-221">jQuery version 1.12.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.4.min.map

#### <a name="jquery-version-1123"></a><span data-ttu-id="d715a-222">jQuery verze 1.12.3</span><span class="sxs-lookup"><span data-stu-id="d715a-222">jQuery version 1.12.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.3.min.map

#### <a name="jquery-version-1122"></a><span data-ttu-id="d715a-223">jQuery verze 1.12.2</span><span class="sxs-lookup"><span data-stu-id="d715a-223">jQuery version 1.12.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.2.min.map

#### <a name="jquery-version-1121"></a><span data-ttu-id="d715a-224">verze jQuery 1.12.1</span><span class="sxs-lookup"><span data-stu-id="d715a-224">jQuery version 1.12.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.1.min.map

#### <a name="jquery-version-1120"></a><span data-ttu-id="d715a-225">verze jQuery 1.12.0</span><span class="sxs-lookup"><span data-stu-id="d715a-225">jQuery version 1.12.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.12.0.min.map

#### <a name="jquery-version-1113"></a><span data-ttu-id="d715a-226">verze jQuery 1.11.3</span><span class="sxs-lookup"><span data-stu-id="d715a-226">jQuery version 1.11.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.3.min.map

#### <a name="jquery-version-1112"></a><span data-ttu-id="d715a-227">verze jQuery 1.11.2</span><span class="sxs-lookup"><span data-stu-id="d715a-227">jQuery version 1.11.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.2.min.map

#### <a name="jquery-version-1111"></a><span data-ttu-id="d715a-228">verze jQuery 1.11.1</span><span class="sxs-lookup"><span data-stu-id="d715a-228">jQuery version 1.11.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.1.min.map

#### <a name="jquery-version-1110"></a><span data-ttu-id="d715a-229">verze jQuery 1.11.0</span><span class="sxs-lookup"><span data-stu-id="d715a-229">jQuery version 1.11.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.11.0.min.map

#### <a name="jquery-version-1102"></a><span data-ttu-id="d715a-230">verze jQuery 1.10.2</span><span class="sxs-lookup"><span data-stu-id="d715a-230">jQuery version 1.10.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.2.min.map

#### <a name="jquery-version-1101"></a><span data-ttu-id="d715a-231">verze jQuery 1.10.1</span><span class="sxs-lookup"><span data-stu-id="d715a-231">jQuery version 1.10.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.1.min.map

#### <a name="jquery-version-1100"></a><span data-ttu-id="d715a-232">verze jQuery 1.10.0</span><span class="sxs-lookup"><span data-stu-id="d715a-232">jQuery version 1.10.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.10.0.min.map

#### <a name="jquery-version-191"></a><span data-ttu-id="d715a-233">verze jQuery 1.9.1</span><span class="sxs-lookup"><span data-stu-id="d715a-233">jQuery version 1.9.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.1.min.map

#### <a name="jquery-version-190"></a><span data-ttu-id="d715a-234">verze jQuery 1.9.0</span><span class="sxs-lookup"><span data-stu-id="d715a-234">jQuery version 1.9.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.9.0.min.map

#### <a name="jquery-version-183"></a><span data-ttu-id="d715a-235">jQuery verze 1.8.3</span><span class="sxs-lookup"><span data-stu-id="d715a-235">jQuery version 1.8.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.3-vsdoc.js

#### <a name="jquery-version-182"></a><span data-ttu-id="d715a-236">jQuery verze 1.8.2</span><span class="sxs-lookup"><span data-stu-id="d715a-236">jQuery version 1.8.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.2-vsdoc.js

#### <a name="jquery-version-181"></a><span data-ttu-id="d715a-237">jQuery verze 1.8.1</span><span class="sxs-lookup"><span data-stu-id="d715a-237">jQuery version 1.8.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.1-vsdoc.js

#### <a name="jquery-version-180"></a><span data-ttu-id="d715a-238">jQuery verze 1.8.0</span><span class="sxs-lookup"><span data-stu-id="d715a-238">jQuery version 1.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.8.0-vsdoc.js

#### <a name="jquery-version-172"></a><span data-ttu-id="d715a-239">jQuery verze 1.7.2</span><span class="sxs-lookup"><span data-stu-id="d715a-239">jQuery version 1.7.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.2.min.js

#### <a name="jquery-version-171"></a><span data-ttu-id="d715a-240">jQuery verzi 1.7.1</span><span class="sxs-lookup"><span data-stu-id="d715a-240">jQuery version 1.7.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.1-vsdoc.js

#### <a name="jquery-version-17"></a><span data-ttu-id="d715a-241">jQuery verze 1.7</span><span class="sxs-lookup"><span data-stu-id="d715a-241">jQuery version 1.7</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.7-vsdoc.js

#### <a name="jquery-version-164"></a><span data-ttu-id="d715a-242">jQuery verze 1.6.4</span><span class="sxs-lookup"><span data-stu-id="d715a-242">jQuery version 1.6.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.4-vsdoc.js

#### <a name="jquery-version-163"></a><span data-ttu-id="d715a-243">jQuery verze 1.6.3</span><span class="sxs-lookup"><span data-stu-id="d715a-243">jQuery version 1.6.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.3-vsdoc.js

#### <a name="jquery-version-162"></a><span data-ttu-id="d715a-244">jQuery verze 1.6.2.</span><span class="sxs-lookup"><span data-stu-id="d715a-244">jQuery version 1.6.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.2-vsdoc.js

#### <a name="jquery-version-161"></a><span data-ttu-id="d715a-245">jQuery verze 1.6.1</span><span class="sxs-lookup"><span data-stu-id="d715a-245">jQuery version 1.6.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.1-vsdoc.js

#### <a name="jquery-version-16"></a><span data-ttu-id="d715a-246">jQuery verze 1.6</span><span class="sxs-lookup"><span data-stu-id="d715a-246">jQuery version 1.6</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.6-vsdoc.js

#### <a name="jquery-version-152"></a><span data-ttu-id="d715a-247">jQuery verze 1.5.2</span><span class="sxs-lookup"><span data-stu-id="d715a-247">jQuery version 1.5.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.2-vsdoc.js

#### <a name="jquery-version-151"></a><span data-ttu-id="d715a-248">jQuery verze 1.5.1</span><span class="sxs-lookup"><span data-stu-id="d715a-248">jQuery version 1.5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.1-vsdoc.js

#### <a name="jquery-version-15"></a><span data-ttu-id="d715a-249">verze jQuery 1.5</span><span class="sxs-lookup"><span data-stu-id="d715a-249">jQuery version 1.5</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.5-vsdoc.js

#### <a name="jquery-version-144"></a><span data-ttu-id="d715a-250">jQuery verze 1.4.4</span><span class="sxs-lookup"><span data-stu-id="d715a-250">jQuery version 1.4.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.4-vsdoc.js

#### <a name="jquery-version-143"></a><span data-ttu-id="d715a-251">jQuery verze 1.4.3</span><span class="sxs-lookup"><span data-stu-id="d715a-251">jQuery version 1.4.3</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.3-vsdoc.js

#### <a name="jquery-version-142"></a><span data-ttu-id="d715a-252">verze 1.4.2 jQuery</span><span class="sxs-lookup"><span data-stu-id="d715a-252">jQuery version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.2-vsdoc.js

#### <a name="jquery-version-141"></a><span data-ttu-id="d715a-253">jQuery verze 1.4.1</span><span class="sxs-lookup"><span data-stu-id="d715a-253">jQuery version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.1-vsdoc.js

#### <a name="jquery-version-14"></a><span data-ttu-id="d715a-254">jQuery verze 1.4</span><span class="sxs-lookup"><span data-stu-id="d715a-254">jQuery version 1.4</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.4.min.js

#### <a name="jquery-version-132"></a><span data-ttu-id="d715a-255">jQuery verze 1.3.2</span><span class="sxs-lookup"><span data-stu-id="d715a-255">jQuery version 1.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2-vsdoc.js
- https://ajax.aspnetcdn.com/ajax/jQuery/jquery-1.3.2.min-vsdoc.js

<a id="jQuery_Migrate_Releases_on_the_CDN_1"></a>

### <a name="jquery-migrate-releases-on-the-cdn"></a><span data-ttu-id="d715a-256">jQuery verze migrace v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-256">jQuery Migrate Releases on the CDN</span></span>

<span data-ttu-id="d715a-257">Tyto verze jQuery migrací jsou hostované v síti CDN:</span><span class="sxs-lookup"><span data-stu-id="d715a-257">The following releases of jQuery Migrate are hosted on the CDN:</span></span>

#### <a name="jquery-migrate-version-300"></a><span data-ttu-id="d715a-258">jQuery migrace verze 3.0.0</span><span class="sxs-lookup"><span data-stu-id="d715a-258">jQuery Migrate version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-3.0.0.min.js

#### <a name="jquery-migrate-version-121"></a><span data-ttu-id="d715a-259">Migrace verze 1.2.1 jQuery</span><span class="sxs-lookup"><span data-stu-id="d715a-259">jQuery Migrate version 1.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.1.min.js

<span data-ttu-id="d715a-260">Migrace verzi 1.2.0 jQuery</span><span class="sxs-lookup"><span data-stu-id="d715a-260">jQuery Migrate version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.2.0.min.js

#### <a name="jquery-migrate-version-111"></a><span data-ttu-id="d715a-261">Migrace verze 1.1.1 jQuery</span><span class="sxs-lookup"><span data-stu-id="d715a-261">jQuery Migrate version 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.1.min.js

#### <a name="jquery-migrate-version-110"></a><span data-ttu-id="d715a-262">jQuery migrace verze 1.1.0</span><span class="sxs-lookup"><span data-stu-id="d715a-262">jQuery Migrate version 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.1.0.min.js

#### <a name="jquery-migrate-version-100"></a><span data-ttu-id="d715a-263">jQuery migrace verze 1.0.0</span><span class="sxs-lookup"><span data-stu-id="d715a-263">jQuery Migrate version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.js
- https://ajax.aspnetcdn.com/ajax/jquery.migrate/jquery-migrate-1.0.0.min.js

<a id="jQuery_UI_Releases_on_the_CDN_2"></a>

### <a name="jquery-ui-releases-on-the-cdn"></a><span data-ttu-id="d715a-264">jQuery verze uživatelského rozhraní v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-264">jQuery UI Releases on the CDN</span></span>

<span data-ttu-id="d715a-265">Tyto verze knihovny uživatelského rozhraní jQuery jsou hostované na této sítě CDN.</span><span class="sxs-lookup"><span data-stu-id="d715a-265">The following releases of the jQuery UI library are hosted on this CDN.</span></span> <span data-ttu-id="d715a-266">Klikněte na každý odkaz zobrazíte skutečný seznam souborů.</span><span class="sxs-lookup"><span data-stu-id="d715a-266">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="d715a-267">uživatelské rozhraní jQuery 1.12.1</span><span class="sxs-lookup"><span data-stu-id="d715a-267">jQuery UI 1.12.1</span></span>](jquery-ui/cdnjqueryui1121.md "uživatelské rozhraní jQuery 1.12.1 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-268">uživatelské rozhraní jQuery 1.12.0</span><span class="sxs-lookup"><span data-stu-id="d715a-268">jQuery UI 1.12.0</span></span>](jquery-ui/cdnjqueryui1120.md "uživatelské rozhraní jQuery 1.12.0 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-269">uživatelské rozhraní jQuery 1.11.4</span><span class="sxs-lookup"><span data-stu-id="d715a-269">jQuery UI 1.11.4</span></span>](jquery-ui/cdnjqueryui1114.md "uživatelské rozhraní jQuery 1.11.4 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-270">uživatelské rozhraní jQuery 1.11.3</span><span class="sxs-lookup"><span data-stu-id="d715a-270">jQuery UI 1.11.3</span></span>](jquery-ui/cdnjqueryui1113.md "uživatelské rozhraní jQuery 1.11.3 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-271">uživatelské rozhraní jQuery 1.11.2</span><span class="sxs-lookup"><span data-stu-id="d715a-271">jQuery UI 1.11.2</span></span>](jquery-ui/cdnjqueryui1112.md "uživatelské rozhraní jQuery 1.11.2 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-272">uživatelské rozhraní jQuery 1.11.1</span><span class="sxs-lookup"><span data-stu-id="d715a-272">jQuery UI 1.11.1</span></span>](jquery-ui/cdnjqueryui1111.md "uživatelské rozhraní jQuery 1.11.1 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-273">uživatelské rozhraní jQuery 1.11.0</span><span class="sxs-lookup"><span data-stu-id="d715a-273">jQuery UI 1.11.0</span></span>](jquery-ui/cdnjqueryui1110.md "uživatelské rozhraní jQuery 1.11.0 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-274">uživatelské rozhraní jQuery 1.10.4</span><span class="sxs-lookup"><span data-stu-id="d715a-274">jQuery UI 1.10.4</span></span>](jquery-ui/cdnjqueryui1104.md "uživatelské rozhraní jQuery 1.10.4 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-275">uživatelské rozhraní jQuery 1.10.3</span><span class="sxs-lookup"><span data-stu-id="d715a-275">jQuery UI 1.10.3</span></span>](jquery-ui/cdnjqueryui1103.md "uživatelské rozhraní jQuery 1.10.3 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-276">uživatelské rozhraní jQuery 1.10.2</span><span class="sxs-lookup"><span data-stu-id="d715a-276">jQuery UI 1.10.2</span></span>](jquery-ui/cdnjqueryui1102.md "uživatelské rozhraní jQuery 1.10.2 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-277">uživatelské rozhraní jQuery 1.10.1</span><span class="sxs-lookup"><span data-stu-id="d715a-277">jQuery UI 1.10.1</span></span>](jquery-ui/cdnjqueryui1101.md "uživatelské rozhraní jQuery 1.10.1 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-278">uživatelské rozhraní jQuery 1.10.0</span><span class="sxs-lookup"><span data-stu-id="d715a-278">jQuery UI 1.10.0</span></span>](jquery-ui/cdnjqueryui1100.md "uživatelské rozhraní jQuery 1.10.0 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-279">uživatelské rozhraní jQuery 1.9.2</span><span class="sxs-lookup"><span data-stu-id="d715a-279">jQuery UI 1.9.2</span></span>](jquery-ui/cdnjqueryui192.md "uživatelské rozhraní jQuery 1.9.2 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-280">uživatelské rozhraní jQuery 1.9.1</span><span class="sxs-lookup"><span data-stu-id="d715a-280">jQuery UI 1.9.1</span></span>](jquery-ui/cdnjqueryui191.md "uživatelské rozhraní jQuery 1.9.1 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-281">uživatelské rozhraní jQuery 1.9.0</span><span class="sxs-lookup"><span data-stu-id="d715a-281">jQuery UI 1.9.0</span></span>](jquery-ui/cdnjqueryui190.md "uživatelské rozhraní jQuery 1.9.0 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-282">uživatelské rozhraní jQuery 1.8.24</span><span class="sxs-lookup"><span data-stu-id="d715a-282">jQuery UI 1.8.24</span></span>](jquery-ui/cdnjqueryui1824.md "uživatelské rozhraní jQuery 1.8.24 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-283">uživatelské rozhraní jQuery 1.8.23</span><span class="sxs-lookup"><span data-stu-id="d715a-283">jQuery UI 1.8.23</span></span>](jquery-ui/cdnjqueryui1823.md "uživatelské rozhraní jQuery 1.8.23 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-284">uživatelské rozhraní jQuery 1.8.22</span><span class="sxs-lookup"><span data-stu-id="d715a-284">jQuery UI 1.8.22</span></span>](jquery-ui/cdnjqueryui1822.md "uživatelské rozhraní jQuery 1.8.22 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-285">uživatelské rozhraní jQuery 1.8.21</span><span class="sxs-lookup"><span data-stu-id="d715a-285">jQuery UI 1.8.21</span></span>](jquery-ui/cdnjqueryui1821.md "uživatelské rozhraní jQuery 1.8.21 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-286">uživatelské rozhraní jQuery 1.8.20</span><span class="sxs-lookup"><span data-stu-id="d715a-286">jQuery UI 1.8.20</span></span>](jquery-ui/cdnjqueryui1820.md "uživatelské rozhraní jQuery 1.8.20 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-287">uživatelské rozhraní jQuery 1.8.19</span><span class="sxs-lookup"><span data-stu-id="d715a-287">jQuery UI 1.8.19</span></span>](jquery-ui/cdnjqueryui1819.md "uživatelské rozhraní jQuery 1.8.19 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-288">uživatelské rozhraní jQuery 1.8.18</span><span class="sxs-lookup"><span data-stu-id="d715a-288">jQuery UI 1.8.18</span></span>](jquery-ui/cdnjqueryui1818.md "uživatelské rozhraní jQuery 1.8.18 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-289">uživatelské rozhraní jQuery 1.8.17</span><span class="sxs-lookup"><span data-stu-id="d715a-289">jQuery UI 1.8.17</span></span>](jquery-ui/cdnjqueryui1817.md "uživatelské rozhraní jQuery 1.8.17 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-290">uživatelské rozhraní jQuery 1.8.16</span><span class="sxs-lookup"><span data-stu-id="d715a-290">jQuery UI 1.8.16</span></span>](jquery-ui/cdnjqueryui1816.md "uživatelské rozhraní jQuery 1.8.16 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-291">uživatelské rozhraní jQuery 1.8.15</span><span class="sxs-lookup"><span data-stu-id="d715a-291">jQuery UI 1.8.15</span></span>](jquery-ui/cdnjqueryui1815.md "uživatelské rozhraní jQuery 1.8.15 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-292">uživatelské rozhraní jQuery 1.8.14</span><span class="sxs-lookup"><span data-stu-id="d715a-292">jQuery UI 1.8.14</span></span>](jquery-ui/cdnjqueryui1814.md "uživatelské rozhraní jQuery 1.8.14 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-293">uživatelské rozhraní jQuery 1.8.13</span><span class="sxs-lookup"><span data-stu-id="d715a-293">jQuery UI 1.8.13</span></span>](jquery-ui/cdnjqueryui1813.md "uživatelské rozhraní jQuery 1.8.13 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-294">uživatelské rozhraní jQuery 1.8.12</span><span class="sxs-lookup"><span data-stu-id="d715a-294">jQuery UI 1.8.12</span></span>](jquery-ui/cdnjqueryui1812.md "uživatelské rozhraní jQuery 1.8.12 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-295">jQuery UI 1.8.11</span><span class="sxs-lookup"><span data-stu-id="d715a-295">jQuery UI 1.8.11</span></span>](jquery-ui/cdnjqueryui1811.md "jQuery UI 1.8.11 on the Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-296">uživatelské rozhraní jQuery 1.8.10</span><span class="sxs-lookup"><span data-stu-id="d715a-296">jQuery UI 1.8.10</span></span>](jquery-ui/cdnjqueryui1910.md "uživatelské rozhraní jQuery 1.8.10 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-297">uživatelské rozhraní jQuery 1.8.9</span><span class="sxs-lookup"><span data-stu-id="d715a-297">jQuery UI 1.8.9</span></span>](jquery-ui/cdnjqueryui189.md "uživatelské rozhraní jQuery 1.8.9 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-298">uživatelské rozhraní jQuery 1.8.8</span><span class="sxs-lookup"><span data-stu-id="d715a-298">jQuery UI 1.8.8</span></span>](jquery-ui/cdnjqueryui188.md "uživatelské rozhraní jQuery 1.8.8 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-299">uživatelské rozhraní jQuery 1.8.7</span><span class="sxs-lookup"><span data-stu-id="d715a-299">jQuery UI 1.8.7</span></span>](jquery-ui/cdnjqueryui187.md "uživatelské rozhraní jQuery 1.8.7 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-300">jQuery UI 1.8.6</span><span class="sxs-lookup"><span data-stu-id="d715a-300">jQuery UI 1.8.6</span></span>](jquery-ui/cdnjqueryui186.md "jQuery UI 1.8.6 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-301">jQuery UI 1.8.5</span><span class="sxs-lookup"><span data-stu-id="d715a-301">jQuery UI 1.8.5</span></span>](jquery-ui/cdnjqueryui185.md "jQuery UI 1.8.5")

<a id="jQuery_Validation_Releases_on_the_CDN_3"></a>

### <a name="jquery-validation-releases-on-the-cdn"></a><span data-ttu-id="d715a-302">jQuery verze ověření v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-302">jQuery Validation Releases on the CDN</span></span>

<span data-ttu-id="d715a-303">Tyto verze knihovny jQuery ověření jsou hostované na této sítě CDN.</span><span class="sxs-lookup"><span data-stu-id="d715a-303">The following releases of the jQuery Validation library are hosted on this CDN.</span></span> <span data-ttu-id="d715a-304">Klikněte na každý odkaz zobrazíte skutečný seznam souborů.</span><span class="sxs-lookup"><span data-stu-id="d715a-304">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="d715a-305">jQuery ověřit 1.19.0</span><span class="sxs-lookup"><span data-stu-id="d715a-305">jQuery Validate 1.19.0</span></span>](jquery-validate/cdnjqueryvalidate1190.md "jQuery ověření 1.19.0")
- [<span data-ttu-id="d715a-306">jQuery ověřit 1.17.0</span><span class="sxs-lookup"><span data-stu-id="d715a-306">jQuery Validate 1.17.0</span></span>](jquery-validate/cdnjqueryvalidate1170.md "jQuery ověření 1.17.0")
- [<span data-ttu-id="d715a-307">jQuery ověřit 1.16.0</span><span class="sxs-lookup"><span data-stu-id="d715a-307">jQuery Validate 1.16.0</span></span>](jquery-validate/cdnjqueryvalidate1160.md "jQuery ověření 1.16.0")
- [<span data-ttu-id="d715a-308">jQuery Validate 1.15.1</span><span class="sxs-lookup"><span data-stu-id="d715a-308">jQuery Validate 1.15.1</span></span>](jquery-validate/cdnjqueryvalidate1151.md "jQuery Validation 1.15.1")
- [<span data-ttu-id="d715a-309">jQuery ověřit 1.15.0</span><span class="sxs-lookup"><span data-stu-id="d715a-309">jQuery Validate 1.15.0</span></span>](jquery-validate/cdnjqueryvalidate1150.md "jQuery ověření 1.15.0")
- [<span data-ttu-id="d715a-310">jQuery Validate 1.14.0</span><span class="sxs-lookup"><span data-stu-id="d715a-310">jQuery Validate 1.14.0</span></span>](jquery-validate/cdnjqueryvalidate1140.md "jQuery Validation 1.14.0")
- [<span data-ttu-id="d715a-311">jQuery Validate 1.13.1</span><span class="sxs-lookup"><span data-stu-id="d715a-311">jQuery Validate 1.13.1</span></span>](jquery-validate/cdnjqueryvalidate1131.md "jQuery Validation 1.13.1")
- [<span data-ttu-id="d715a-312">jQuery Validate 1.13.0</span><span class="sxs-lookup"><span data-stu-id="d715a-312">jQuery Validate 1.13.0</span></span>](jquery-validate/cdnjqueryvalidate1130.md "jQuery Validation 1.13.0")
- [<span data-ttu-id="d715a-313">jQuery Validate 1.12.0</span><span class="sxs-lookup"><span data-stu-id="d715a-313">jQuery Validate 1.12.0</span></span>](jquery-validate/cdnjqueryvalidate1120.md "jQuery Validation 1.12.0")
- [<span data-ttu-id="d715a-314">jQuery Validate 1.11.1</span><span class="sxs-lookup"><span data-stu-id="d715a-314">jQuery Validate 1.11.1</span></span>](jquery-validate/cdnjqueryvalidate1111.md "jQuery Validation 1.11.1")
- [<span data-ttu-id="d715a-315">jQuery 1.11.0 ověřit</span><span class="sxs-lookup"><span data-stu-id="d715a-315">jQuery Validate 1.11.0</span></span>](jquery-validate/cdnjqueryvalidate111.md "jQuery 1.11.0 ověření")
- [<span data-ttu-id="d715a-316">jQuery 1.10.0 ověřit</span><span class="sxs-lookup"><span data-stu-id="d715a-316">jQuery Validate 1.10.0</span></span>](jquery-validate/cdnjqueryvalidate110.md "jQuery 1.10.0 ověření")
- [<span data-ttu-id="d715a-317">jQuery Validate 1.9</span><span class="sxs-lookup"><span data-stu-id="d715a-317">jQuery Validate 1.9</span></span>](jquery-validate/cdnjqueryvalidate19.md "jquery.validate version 1.9")
- [<span data-ttu-id="d715a-318">jQuery ověřit 1.8.1</span><span class="sxs-lookup"><span data-stu-id="d715a-318">jQuery Validate 1.8.1</span></span>](jquery-validate/cdnjqueryvalidate181.md "jquery.validate verze 1.8.1")
- [<span data-ttu-id="d715a-319">jQuery Validate 1.8</span><span class="sxs-lookup"><span data-stu-id="d715a-319">jQuery Validate 1.8</span></span>](jquery-validate/cdnjqueryvalidate18.md "jquery.validate version 1.8")
- [<span data-ttu-id="d715a-320">jQuery Validate 1.7</span><span class="sxs-lookup"><span data-stu-id="d715a-320">jQuery Validate 1.7</span></span>](jquery-validate/cdnjqueryvalidate17.md "jquery.validate version 1.7")
- [<span data-ttu-id="d715a-321">jQuery Validate 1.6</span><span class="sxs-lookup"><span data-stu-id="d715a-321">jQuery Validate 1.6</span></span>](jquery-validate/cdnjqueryvalidate16.md "jQuery Validate 1.6")
- [<span data-ttu-id="d715a-322">jQuery Validate 1.5.5</span><span class="sxs-lookup"><span data-stu-id="d715a-322">jQuery Validate 1.5.5</span></span>](jquery-validate/cdnjqueryvalidate155.md "jQuery Validate 1.5.5")

<a id="jQuery_Mobile_Releases_on_the_CDN_4"></a>

### <a name="jquery-mobile-releases-on-the-cdn"></a><span data-ttu-id="d715a-323">jQuery Mobile verze v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-323">jQuery Mobile Releases on the CDN</span></span>

<span data-ttu-id="d715a-324">Tyto verze knihovny jQuery Mobile jsou hostované na této sítě CDN.</span><span class="sxs-lookup"><span data-stu-id="d715a-324">The following releases of the jQuery Mobile library are hosted on this CDN.</span></span> <span data-ttu-id="d715a-325">Klikněte na každý odkaz zobrazíte skutečný seznam souborů.</span><span class="sxs-lookup"><span data-stu-id="d715a-325">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="d715a-326">jQuery Mobile 1.4.5</span><span class="sxs-lookup"><span data-stu-id="d715a-326">jQuery Mobile 1.4.5</span></span>](jquery-mobile/cdnjquerymobile145.md "jQuery Mobile 1.4.5 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-327">jQuery Mobile 1.4.2</span><span class="sxs-lookup"><span data-stu-id="d715a-327">jQuery Mobile 1.4.2</span></span>](jquery-mobile/cdnjquerymobile142.md "jQuery Mobile 1.4.2 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-328">jQuery Mobile 1.4.1</span><span class="sxs-lookup"><span data-stu-id="d715a-328">jQuery Mobile 1.4.1</span></span>](jquery-mobile/cdnjquerymobile141.md "jQuery Mobile 1.4.1 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-329">jQuery Mobile 1.4.0</span><span class="sxs-lookup"><span data-stu-id="d715a-329">jQuery Mobile 1.4.0</span></span>](jquery-mobile/cdnjquerymobile140.md "jQuery Mobile 1.4.0 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-330">jQuery Mobile 1.3.2</span><span class="sxs-lookup"><span data-stu-id="d715a-330">jQuery Mobile 1.3.2</span></span>](jquery-mobile/cdnjquerymobile132.md "jQuery Mobile 1.3.2 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-331">jQuery Mobile 1.3.1</span><span class="sxs-lookup"><span data-stu-id="d715a-331">jQuery Mobile 1.3.1</span></span>](jquery-mobile/cdnjquerymobile131.md "jQuery Mobile 1.3.1 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-332">jQuery Mobile 1.3.0</span><span class="sxs-lookup"><span data-stu-id="d715a-332">jQuery Mobile 1.3.0</span></span>](jquery-mobile/cdnjquerymobile130.md "jQuery Mobile 1.3.0 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-333">jQuery Mobile 1.2.0</span><span class="sxs-lookup"><span data-stu-id="d715a-333">jQuery Mobile 1.2.0</span></span>](jquery-mobile/cdnjquerymobile120.md "jQuery Mobile 1.2.0 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-334">jQuery Mobile 1.1.2</span><span class="sxs-lookup"><span data-stu-id="d715a-334">jQuery Mobile 1.1.2</span></span>](jquery-mobile/cdnjquerymobile112.md "jQuery Mobile 1.1.2 on the Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-335">jQuery Mobile 1.1.1</span><span class="sxs-lookup"><span data-stu-id="d715a-335">jQuery Mobile 1.1.1</span></span>](jquery-mobile/cdnjquerymobile111.md "jQuery Mobile 1.1.1 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-336">jQuery Mobile 1.1.0</span><span class="sxs-lookup"><span data-stu-id="d715a-336">jQuery Mobile 1.1.0</span></span>](jquery-mobile/cdnjquerymobile110.md "jQuery Mobile 1.1.0 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-337">jQuery Mobile 1.1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="d715a-337">jQuery Mobile 1.1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile110rc2.md "jQuery Mobile 1.1.0 RC2 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-338">jQuery Mobile 1.0.1</span><span class="sxs-lookup"><span data-stu-id="d715a-338">jQuery Mobile 1.0.1</span></span>](jquery-mobile/cdnjquerymobile101.md "jQuery Mobile 1.0.1 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-339">jQuery Mobile 1.0</span><span class="sxs-lookup"><span data-stu-id="d715a-339">jQuery Mobile 1.0</span></span>](jquery-mobile/cdnjquerymobile10.md "jQuery Mobile 1.0 ve službě Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-340">jQuery Mobile 1.0 RC 2</span><span class="sxs-lookup"><span data-stu-id="d715a-340">jQuery Mobile 1.0 RC 2</span></span>](jquery-mobile/cdnjquerymobile10rc2.md "jQuery Mobile 1.0 RC2 on the Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-341">jQuery Mobile 1.0 RC 1</span><span class="sxs-lookup"><span data-stu-id="d715a-341">jQuery Mobile 1.0 RC 1</span></span>](jquery-mobile/cdnjquerymobile10rc1.md "jQuery Mobile 1.0 RC1 on the Microsoft Ajax CDN")
- [<span data-ttu-id="d715a-342">jQuery Mobile 1.0 beta 3</span><span class="sxs-lookup"><span data-stu-id="d715a-342">jQuery Mobile 1.0 beta 3</span></span>](jquery-mobile/cdnjquerymobile10b3.md "jQuery Mobile 1.0 Beta 3 ve službě Microsoft Ajax CDN")

<a id="jQuery_Templates_Releases_on_the_CDN_5"></a>

### <a name="jquery-templates-releases-on-the-cdn"></a><span data-ttu-id="d715a-343">jQuery šablony vydané verze v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-343">jQuery Templates Releases on the CDN</span></span>

<span data-ttu-id="d715a-344">Tyto verze modulu plug-in jQuery šablony jsou hostovány na této sítě CDN.</span><span class="sxs-lookup"><span data-stu-id="d715a-344">The following releases of the jQuery Templates plugin are hosted on this CDN.</span></span> <span data-ttu-id="d715a-345">Klikněte na každý odkaz zobrazíte skutečný seznam souborů.</span><span class="sxs-lookup"><span data-stu-id="d715a-345">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="d715a-346">jQuery šablony Beta 1</span><span class="sxs-lookup"><span data-stu-id="d715a-346">jQuery Templates Beta 1</span></span>](jquery-templates/cdnjquerytemplatesbeta1.md "jQuery šablony Beta 1")

<a id="jQuery_Cycle_Releases_on_the_CDN_6"></a>

### <a name="jquery-cycle-releases-on-the-cdn"></a><span data-ttu-id="d715a-347">jQuery cyklu vydání v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-347">jQuery Cycle Releases on the CDN</span></span>

<span data-ttu-id="d715a-348">Tyto verze modulu plug-in jQuery cyklu jsou hostované na této sítě CDN.</span><span class="sxs-lookup"><span data-stu-id="d715a-348">The following releases of the jQuery Cycle plugin are hosted on this CDN.</span></span> <span data-ttu-id="d715a-349">Klikněte na každý odkaz zobrazíte skutečný seznam souborů.</span><span class="sxs-lookup"><span data-stu-id="d715a-349">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="d715a-350">jQuery Cycle 2.99</span><span class="sxs-lookup"><span data-stu-id="d715a-350">jQuery Cycle 2.99</span></span>](jquery-cycle/cdnjquerycycle299.md "jQuery Cycle 2.99")
- [<span data-ttu-id="d715a-351">jQuery Cycle 2.94</span><span class="sxs-lookup"><span data-stu-id="d715a-351">jQuery Cycle 2.94</span></span>](jquery-cycle/cdnjquerycycle294.md "jQuery Cycle 2.94")
- [<span data-ttu-id="d715a-352">jQuery Cycle 2.88</span><span class="sxs-lookup"><span data-stu-id="d715a-352">jQuery Cycle 2.88</span></span>](jquery-cycle/cdnjquerycycle288.md "jQuery Cycle 2.88")

<a id="jQuery_DataTables_Releases_on_the_CDN_7"></a>

### <a name="jquery-datatables-releases-on-the-cdn"></a><span data-ttu-id="d715a-353">jQuery DataTables vydané verze v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-353">jQuery DataTables Releases on the CDN</span></span>

<span data-ttu-id="d715a-354">Tyto verze modulu plug-in jQuery DataTables jsou hostované na této sítě CDN.</span><span class="sxs-lookup"><span data-stu-id="d715a-354">The following releases of the jQuery DataTables plugin are hosted on this CDN.</span></span> <span data-ttu-id="d715a-355">Klikněte na každý odkaz zobrazíte skutečný seznam souborů.</span><span class="sxs-lookup"><span data-stu-id="d715a-355">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="d715a-356">jQuery DataTables 1.10.5</span><span class="sxs-lookup"><span data-stu-id="d715a-356">jQuery DataTables 1.10.5</span></span>](jquery-datatables/cdnjquerydatatables105.md "jQuery DataTables 1.10.5")
- [<span data-ttu-id="d715a-357">jQuery DataTables 1.10.4</span><span class="sxs-lookup"><span data-stu-id="d715a-357">jQuery DataTables 1.10.4</span></span>](jquery-datatables/cdnjquerydatatables104.md "jQuery DataTables 1.10.4")
- [<span data-ttu-id="d715a-358">jQuery DataTables 1.9.4</span><span class="sxs-lookup"><span data-stu-id="d715a-358">jQuery DataTables 1.9.4</span></span>](jquery-datatables/cdnjquerydatatables194.md "jQuery DataTables 1.9.4")
- [<span data-ttu-id="d715a-359">jQuery DataTables 1.9.3</span><span class="sxs-lookup"><span data-stu-id="d715a-359">jQuery DataTables 1.9.3</span></span>](jquery-datatables/cdnjquerydatatables193.md "jQuery DataTables 1.9.3")
- [<span data-ttu-id="d715a-360">jQuery DataTables 1.9.2</span><span class="sxs-lookup"><span data-stu-id="d715a-360">jQuery DataTables 1.9.2</span></span>](jquery-datatables/cdnjquerydatatables192.md "jQuery DataTables 1.9.2")
- [<span data-ttu-id="d715a-361">jQuery DataTables 1.9.1</span><span class="sxs-lookup"><span data-stu-id="d715a-361">jQuery DataTables 1.9.1</span></span>](jquery-datatables/cdnjquerydatatables191.md "jQuery DataTables 1.9.1")
- [<span data-ttu-id="d715a-362">jQuery DataTables 1.9.0</span><span class="sxs-lookup"><span data-stu-id="d715a-362">jQuery DataTables 1.9.0</span></span>](jquery-datatables/cdnjquerydatatables190.md "jQuery DataTables 1.9.0")
- [<span data-ttu-id="d715a-363">jQuery DataTables 1.8.2</span><span class="sxs-lookup"><span data-stu-id="d715a-363">jQuery DataTables 1.8.2</span></span>](jquery-datatables/cdnjquerydatatables182.md "jQuery DataTables 1.8.2")

<a id="Modernizr_Releases_on_the_CDN_8"></a>

### <a name="modernizr-releases-on-the-cdn"></a><span data-ttu-id="d715a-364">Verze Modernizr v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-364">Modernizr Releases on the CDN</span></span>

<span data-ttu-id="d715a-365">Toto vydání [Modernizr](http://www.modernizr.com "Modernizr") jsou hostované v síti CDN:</span><span class="sxs-lookup"><span data-stu-id="d715a-365">The following releases of [Modernizr](http://www.modernizr.com "Modernizr") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-3.5.0.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.8.3.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.7.1.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.6.2.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-1.7-development-only.js
- https://ajax.aspnetcdn.com/ajax/modernizr/modernizr-2.0.6-development-only.js

<a id="JSHint_Releases_on_the_CDN_10"></a>

### <a name="jshint-releases-on-the-cdn"></a><span data-ttu-id="d715a-366">Verze JSHint v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-366">JSHint Releases on the CDN</span></span>

<span data-ttu-id="d715a-367">Toto vydání [JSHint](http://www.jshint.com "JSHint") jsou hostované v síti CDN:</span><span class="sxs-lookup"><span data-stu-id="d715a-367">The following releases of [JSHint](http://www.jshint.com "JSHint") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/jshint/r07/jshint.js

<a id="Knockout_Releases_on_the_CDN_11"></a>

### <a name="knockout-releases-on-the-cdn"></a><span data-ttu-id="d715a-368">Verze knockout v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-368">Knockout Releases on the CDN</span></span>

<span data-ttu-id="d715a-369">Toto vydání [Knockout](http://www.knockoutjs.com "Knockout") jsou hostované v síti CDN:</span><span class="sxs-lookup"><span data-stu-id="d715a-369">The following releases of [Knockout](http://www.knockoutjs.com "Knockout") are hosted on the CDN:</span></span>

- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-2.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.0.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.1.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.2.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.3.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.0.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.1.debug.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.js
- https://ajax.aspnetcdn.com/ajax/knockout/knockout-3.4.2.debug.js

<a id="Globalize_Releases_on_the_CDN_12"></a>

### <a name="globalize-releases-on-the-cdn"></a><span data-ttu-id="d715a-370">Globalizace vydané verze v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-370">Globalize Releases on the CDN</span></span>

<span data-ttu-id="d715a-371">Toto vydání [Globalize](https://github.com/jquery/globalize "Globalize") jsou hostované v síti CDN:</span><span class="sxs-lookup"><span data-stu-id="d715a-371">The following releases of [Globalize](https://github.com/jquery/globalize "Globalize") are hosted on the CDN:</span></span>

#### <a name="globalize-version-100"></a><span data-ttu-id="d715a-372">Globalizace verze 1.0.0</span><span class="sxs-lookup"><span data-stu-id="d715a-372">Globalize version 1.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/node-main.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/currency.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/date.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/message.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/number.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/plural.js
- https://ajax.aspnetcdn.com/ajax/globalize/1.0.0/globalize/relative-time.js

#### <a name="globalize-version-011"></a><span data-ttu-id="d715a-373">Globalizace verze 0.1.1</span><span class="sxs-lookup"><span data-stu-id="d715a-373">Globalize version 0.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.min.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/globalize.js
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.cultures.js

    - <span data-ttu-id="d715a-374">všechny jazykové verze</span><span class="sxs-lookup"><span data-stu-id="d715a-374">all cultures</span></span>
- https://ajax.aspnetcdn.com/ajax/globalize/0.1.1/cultures/globalize.culture.{culture-code}.js

    - <span data-ttu-id="d715a-375">Nahraďte požadovanou jazykovou verzi kódu "{jazyková verze code}", například Microsoft globalize.culture.en GB.js== souborů v síti CDN == tyto knihovny nahraný společností Microsoft.</span><span class="sxs-lookup"><span data-stu-id="d715a-375">Replace "{culture-code}" with the desired culture code, e.g. globalize.culture.en-GB.js== Microsoft Files on the CDN ==These libraries were uploaded by Microsoft.</span></span>

<a id="Respond_Releases_on_the_CDN_13"></a>

### <a name="respond-releases-on-the-cdn"></a><span data-ttu-id="d715a-376">Reakce vydané verze v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-376">Respond Releases on the CDN</span></span>

<span data-ttu-id="d715a-377">Toto vydání [https://github.com/scottjehl/Respond](https://github.com/scottjehl/Respond "https://github.com/scottjehl/Respond") reakce jsou hostované v síti CDN:</span><span class="sxs-lookup"><span data-stu-id="d715a-377">The following releases of [https://github.com/scottjehl/Respond](https://github.com/scottjehl/Respond "https://github.com/scottjehl/Respond") Respond are hosted on the CDN:</span></span>

#### <a name="respond-version-142"></a><span data-ttu-id="d715a-378">Verze 1.4.2 reagovat</span><span class="sxs-lookup"><span data-stu-id="d715a-378">Respond version 1.4.2</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.2/respond.matchmedia.addListener.min.js

#### <a name="respond-version-141"></a><span data-ttu-id="d715a-379">Verze 1.4.1 reagovat</span><span class="sxs-lookup"><span data-stu-id="d715a-379">Respond version 1.4.1</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.1/respond.matchmedia.addListener.min.js

#### <a name="respond-version-140"></a><span data-ttu-id="d715a-380">Verze 1.4.0 reagovat</span><span class="sxs-lookup"><span data-stu-id="d715a-380">Respond version 1.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.min.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.js
- https://ajax.aspnetcdn.com/ajax/respond/1.4.0/respond.matchmedia.addListener.min.js

#### <a name="respond-version-130"></a><span data-ttu-id="d715a-381">Verze 1.3.0 reagovat</span><span class="sxs-lookup"><span data-stu-id="d715a-381">Respond version 1.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.3.0/respond.js

#### <a name="respond-version-120"></a><span data-ttu-id="d715a-382">Verzi 1.2.0 reagovat</span><span class="sxs-lookup"><span data-stu-id="d715a-382">Respond version 1.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/respond/1.2.0/respond.js

<a id="Bootstrap_Releases_on_the_CDN_14"></a>

### <a name="bootstrap-releases-on-the-cdn"></a><span data-ttu-id="d715a-383">Spuštění vydané verze v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-383">Bootstrap Releases on the CDN</span></span>

<span data-ttu-id="d715a-384">Toto vydání [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap jsou hostované v síti CDN:</span><span class="sxs-lookup"><span data-stu-id="d715a-384">The following releases of [getbootstrap.com](http://getbootstrap.com "getbootstrap.com") bootstrap are hosted on the CDN:</span></span>

#### <a name="bootstrap-version-421"></a><span data-ttu-id="d715a-385">Zavedení verze 4.2.1</span><span class="sxs-lookup"><span data-stu-id="d715a-385">Bootstrap version 4.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.2.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-411"></a><span data-ttu-id="d715a-386">Verze 4.1.1 Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d715a-386">Bootstrap version 4.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.1.1/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-400"></a><span data-ttu-id="d715a-387">Zavedení verze 4.0.0</span><span class="sxs-lookup"><span data-stu-id="d715a-387">Bootstrap version 4.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/bootstrap.bundle.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-grid.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/4.0.0/css/bootstrap-reboot.css.map

#### <a name="bootstrap-version-340"></a><span data-ttu-id="d715a-388">Verze 3.4.0 Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d715a-388">Bootstrap version 3.4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.4.0/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-337"></a><span data-ttu-id="d715a-389">Verze 3.3.7 Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d715a-389">Bootstrap version 3.3.7</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.7/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-336"></a><span data-ttu-id="d715a-390">Verze 3.3.6 Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d715a-390">Bootstrap version 3.3.6</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.6/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-335"></a><span data-ttu-id="d715a-391">Verze 3.3.5 Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d715a-391">Bootstrap version 3.3.5</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.5/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-334"></a><span data-ttu-id="d715a-392">Verze 3.3.4 Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d715a-392">Bootstrap version 3.3.4</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.4/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-332"></a><span data-ttu-id="d715a-393">Verze 3.3.2 Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d715a-393">Bootstrap version 3.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.2/fonts/glyphicons-halflings-regular.woff2

#### <a name="bootstrap-version-331"></a><span data-ttu-id="d715a-394">Verze 3.3.1 Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d715a-394">Bootstrap version 3.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-330"></a><span data-ttu-id="d715a-395">Verze 3.3.0 Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d715a-395">Bootstrap version 3.3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.3.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-320"></a><span data-ttu-id="d715a-396">Verze 3.2.0 Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d715a-396">Bootstrap version 3.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.2.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-311"></a><span data-ttu-id="d715a-397">Verze 3.1.1 Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d715a-397">Bootstrap version 3.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-310"></a><span data-ttu-id="d715a-398">Verze 3.1.0 Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d715a-398">Bootstrap version 3.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.css.map
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.1.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-303"></a><span data-ttu-id="d715a-399">Verze 3.0.3 Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d715a-399">Bootstrap version 3.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.3/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-302"></a><span data-ttu-id="d715a-400">Verze 3.0.2 Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d715a-400">Bootstrap version 3.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.2/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-301"></a><span data-ttu-id="d715a-401">Verze 3.0.1 Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d715a-401">Bootstrap version 3.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.1/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-300"></a><span data-ttu-id="d715a-402">Zavedení verze 3.0.0</span><span class="sxs-lookup"><span data-stu-id="d715a-402">Bootstrap version 3.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/css/bootstrap-theme.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.eot
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.svg
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.ttf
- https://ajax.aspnetcdn.com/ajax/bootstrap/3.0.0/fonts/glyphicons-halflings-regular.woff

#### <a name="bootstrap-version-232"></a><span data-ttu-id="d715a-403">Verze 2.3.2 Bootstrap</span><span class="sxs-lookup"><span data-stu-id="d715a-403">Bootstrap version 2.3.2</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.2/img/glyphicons-halflings-white.png

#### <a name="bootstrap-version-231"></a><span data-ttu-id="d715a-404">Zavedení verze 2.3.1</span><span class="sxs-lookup"><span data-stu-id="d715a-404">Bootstrap version 2.3.1</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/bootstrap.min.js
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/css/bootstrap-responsive.min.css
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings.png
- https://ajax.aspnetcdn.com/ajax/bootstrap/2.3.1/img/glyphicons-halflings-white.png

<a id="BootstrapTouchCarousel_Releases_on_the_CDN_18"></a>

### <a name="bootstrap-touchcarousel-releases-on-the-cdn"></a><span data-ttu-id="d715a-405">Spuštění TouchCarousel vydané verze v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-405">Bootstrap TouchCarousel Releases on the CDN</span></span>

<span data-ttu-id="d715a-406">Toto vydání [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel verzích jsou hostované v síti CDN:</span><span class="sxs-lookup"><span data-stu-id="d715a-406">The following releases of [https://github.com/ixisio/bootstrap-touch-carousel](https://github.com/ixisio/bootstrap-touch-carousel "https://github.com/ixisio/bootstrap-touch-carousel") Bootstrap TouchCarousel releases are hosted on the CDN:</span></span>

#### <a name="bootstrap-touchcarousel-version-080"></a><span data-ttu-id="d715a-407">Zavedení TouchCarousel verze 0.8.0</span><span class="sxs-lookup"><span data-stu-id="d715a-407">Bootstrap TouchCarousel version 0.8.0</span></span>

- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/css/bootstrap-touch-carousel.css
- https://ajax.aspnetcdn.com/ajax/bootstrap-touch-carousel/0.8.0/js/bootstrap-touch-carousel.js

<a id="Hammerjs_Releases_on_the_CDN_19"></a>

### <a name="hammerjs-releases-on-the-cdn"></a><span data-ttu-id="d715a-408">Verze hammer.js v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-408">Hammer.js Releases on the CDN</span></span>

<span data-ttu-id="d715a-409">Toto vydání [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js verzích jsou hostované v síti CDN:</span><span class="sxs-lookup"><span data-stu-id="d715a-409">The following releases of [http://hammerjs.github.io/](http://hammerjs.github.io/ "http://hammerjs.github.io/") Hammer.js releases are hosted on the CDN:</span></span>

#### <a name="hammerjs-version-204"></a><span data-ttu-id="d715a-410">Hammer.js version 2.0.4</span><span class="sxs-lookup"><span data-stu-id="d715a-410">Hammer.js version 2.0.4</span></span>

- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.js
- https://ajax.aspnetcdn.com/ajax/hammer.js/2.0.4/hammer.min.map

<a id="ASPNET_Web_Forms_and_Ajax_Releases_on_the_CDN_15"></a>

### <a name="aspnet-web-forms-and-ajax-releases-on-the-cdn"></a><span data-ttu-id="d715a-411">Webové formuláře ASP.NET a Ajax vydané verze v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-411">ASP.NET Web Forms and Ajax Releases on the CDN</span></span>

<span data-ttu-id="d715a-412">Tyto verze knihovny ASP.NET Ajax jsou hostované v síti CDN.</span><span class="sxs-lookup"><span data-stu-id="d715a-412">The following releases of the ASP.NET Ajax Library are hosted on the CDN.</span></span> <span data-ttu-id="d715a-413">Klikněte na každý odkaz zobrazíte skutečný seznam souborů.</span><span class="sxs-lookup"><span data-stu-id="d715a-413">Click each link to see the actual list of files.</span></span>

- [<span data-ttu-id="d715a-414">Verze technologie ASP.NET webové formuláře a Ajax 4.5.2</span><span class="sxs-lookup"><span data-stu-id="d715a-414">ASP.NET Web Forms and Ajax version 4.5.2</span></span>](cdnajax452.md "webových formulářů ASP.NET a Ajax 4.5.2")
- [<span data-ttu-id="d715a-415">Verze technologie ASP.NET webové formuláře a Ajax 4</span><span class="sxs-lookup"><span data-stu-id="d715a-415">ASP.NET Web Forms and Ajax version 4</span></span>](cdnajax4.md "webových formulářů ASP.NET a Ajax 4")
- [<span data-ttu-id="d715a-416">ASP.NET Ajax verze 3.5</span><span class="sxs-lookup"><span data-stu-id="d715a-416">ASP.NET Ajax version 3.5</span></span>](cdnajax35.md "Ajax technologie ASP.NET 3.5")

<a id="ASPNET_MVC_Releases_on_the_CDN_16"></a>

### <a name="aspnet-mvc-releases-on-the-cdn"></a><span data-ttu-id="d715a-417">Verze technologie ASP.NET MVC v síti CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-417">ASP.NET MVC Releases on the CDN</span></span>

<span data-ttu-id="d715a-418">Následující soubory jazyka JavaScript technologie ASP.NET MVC jsou hostované na této sítě CDN:</span><span class="sxs-lookup"><span data-stu-id="d715a-418">The following ASP.NET MVC JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-mvc-523"></a><span data-ttu-id="d715a-419">ASP.NET MVC 5.2.3</span><span class="sxs-lookup"><span data-stu-id="d715a-419">ASP.NET MVC 5.2.3</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.2.3/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-51"></a><span data-ttu-id="d715a-420">ASP.NET MVC 5.1</span><span class="sxs-lookup"><span data-stu-id="d715a-420">ASP.NET MVC 5.1</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.1/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-50"></a><span data-ttu-id="d715a-421">ASP.NET MVC 5.0</span><span class="sxs-lookup"><span data-stu-id="d715a-421">ASP.NET MVC 5.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/5.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-40"></a><span data-ttu-id="d715a-422">ASP.NET MVC 4.0</span><span class="sxs-lookup"><span data-stu-id="d715a-422">ASP.NET MVC 4.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/4.0/jquery.validate.unobtrusive.min.js

#### <a name="aspnet-mvc-30"></a><span data-ttu-id="d715a-423">ASP.NET MVC 3.0</span><span class="sxs-lookup"><span data-stu-id="d715a-423">ASP.NET MVC 3.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.unobtrusive-ajax.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.js
- https://ajax.aspnetcdn.com/ajax/jquery.unobtrusive-ajax/3.2.5/jquery.unobtrusive-ajax.min.js 
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.js 
- https://ajax.aspnetcdn.com/ajax/jquery.validation.unobtrusive/3.2.10/jquery.validate.unobtrusive.min.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/3.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-20"></a><span data-ttu-id="d715a-424">ASP.NET MVC 2.0</span><span class="sxs-lookup"><span data-stu-id="d715a-424">ASP.NET MVC 2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/2.0/MicrosoftMvcAjax.debug.js

#### <a name="aspnet-mvc-10"></a><span data-ttu-id="d715a-425">ASP.NET MVC 1.0</span><span class="sxs-lookup"><span data-stu-id="d715a-425">ASP.NET MVC 1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.js
- https://ajax.aspnetcdn.com/ajax/mvc/1.0/MicrosoftMvcAjax.debug.js

<a id="ASPNET_SignalR_Releases_on_the_CDN_17"></a>

### <a name="aspnet-signalr-releases-on-the-cdn"></a><span data-ttu-id="d715a-426">Verze funkce SignalR technologie ASP.NET ve službě CDN</span><span class="sxs-lookup"><span data-stu-id="d715a-426">ASP.NET SignalR Releases on the CDN</span></span>

<span data-ttu-id="d715a-427">Následující soubory ASP.NET SignalR JavaScript jsou hostované na této sítě CDN:</span><span class="sxs-lookup"><span data-stu-id="d715a-427">The following ASP.NET SignalR JavaScript files are hosted on this CDN:</span></span>

#### <a name="aspnet-signalr-222"></a><span data-ttu-id="d715a-428">Funkce SignalR technologie ASP.NET 2.2.2</span><span class="sxs-lookup"><span data-stu-id="d715a-428">ASP.NET SignalR 2.2.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.2.js

#### <a name="aspnet-signalr-221"></a><span data-ttu-id="d715a-429">Funkce SignalR technologie ASP.NET 2.2.1</span><span class="sxs-lookup"><span data-stu-id="d715a-429">ASP.NET SignalR 2.2.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.1.js

#### <a name="aspnet-signalr-220"></a><span data-ttu-id="d715a-430">Funkce SignalR technologie ASP.NET 2.2.0</span><span class="sxs-lookup"><span data-stu-id="d715a-430">ASP.NET SignalR 2.2.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.2.0.js

#### <a name="aspnet-signalr-210"></a><span data-ttu-id="d715a-431">Funkce SignalR technologie ASP.NET 2.1.0</span><span class="sxs-lookup"><span data-stu-id="d715a-431">ASP.NET SignalR 2.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.1.0.js

#### <a name="aspnet-signalr-203"></a><span data-ttu-id="d715a-432">Funkce SignalR technologie ASP.NET 2.0.3</span><span class="sxs-lookup"><span data-stu-id="d715a-432">ASP.NET SignalR 2.0.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.3.js

#### <a name="aspnet-signalr-202"></a><span data-ttu-id="d715a-433">Funkce SignalR technologie ASP.NET bodu 2.0.2</span><span class="sxs-lookup"><span data-stu-id="d715a-433">ASP.NET SignalR 2.0.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.2.js

#### <a name="aspnet-signalr-201"></a><span data-ttu-id="d715a-434">Funkce SignalR technologie ASP.NET 2.0.1</span><span class="sxs-lookup"><span data-stu-id="d715a-434">ASP.NET SignalR 2.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.1.js

#### <a name="aspnet-signalr-200"></a><span data-ttu-id="d715a-435">Funkce SignalR technologie ASP.NET 2.0.0</span><span class="sxs-lookup"><span data-stu-id="d715a-435">ASP.NET SignalR 2.0.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-2.0.0.js

#### <a name="aspnet-signalr-113"></a><span data-ttu-id="d715a-436">Funkce SignalR technologie ASP.NET 1.1.3</span><span class="sxs-lookup"><span data-stu-id="d715a-436">ASP.NET SignalR 1.1.3</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.3.js

#### <a name="aspnet-signalr-112"></a><span data-ttu-id="d715a-437">Funkce SignalR technologie ASP.NET 1.1.2</span><span class="sxs-lookup"><span data-stu-id="d715a-437">ASP.NET SignalR 1.1.2</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.2.js

#### <a name="aspnet-signalr-111"></a><span data-ttu-id="d715a-438">Funkce SignalR technologie ASP.NET 1.1.1</span><span class="sxs-lookup"><span data-stu-id="d715a-438">ASP.NET SignalR 1.1.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.1.js

#### <a name="aspnet-signalr-110"></a><span data-ttu-id="d715a-439">Funkce SignalR technologie ASP.NET 1.1.0</span><span class="sxs-lookup"><span data-stu-id="d715a-439">ASP.NET SignalR 1.1.0</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.1.0.js

#### <a name="aspnet-signalr-101"></a><span data-ttu-id="d715a-440">Funkce SignalR technologie ASP.NET 1.0.1</span><span class="sxs-lookup"><span data-stu-id="d715a-440">ASP.NET SignalR 1.0.1</span></span>

- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.min.js
- https://ajax.aspnetcdn.com/ajax/signalr/jquery.signalr-1.0.1.js

<span data-ttu-id="d715a-441">Informace o podmínkách použití CDN najdete v tématu [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span><span class="sxs-lookup"><span data-stu-id="d715a-441">For information about the terms of use for the CDN, see [Microsoft Ajax CDN Terms of Use](https://www.asp.net/terms-of-use "Microsoft Ajax CDN Terms of Use").</span></span>
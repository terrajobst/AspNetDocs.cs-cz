---
uid: mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
title: Principy modelů, zobrazení a Kontrolerů (C#) | Dokumentace Microsoftu
author: StephenWalther
description: Ztrácíte přehled o modelů, zobrazení a Kontrolerů? V tomto kurzu Stephen Walther vás seznámí s různé části aplikace ASP.NET MVC.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 87313792-0a96-4caf-89fc-1457d54e5c1e
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-cs
msc.type: authoredcontent
ms.openlocfilehash: 5e9186a6c261266de8f1a1509a49b84b359bd920
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070810"
---
<a name="understanding-models-views-and-controllers-c"></a><span data-ttu-id="a9ffc-104">Principy modelů, zobrazení a kontrolerů (C#)</span><span class="sxs-lookup"><span data-stu-id="a9ffc-104">Understanding Models, Views, and Controllers (C#)</span></span>
====================
<span data-ttu-id="a9ffc-105">podle [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="a9ffc-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="a9ffc-106">Ztrácíte přehled o modelů, zobrazení a Kontrolerů?</span><span class="sxs-lookup"><span data-stu-id="a9ffc-106">Confused about Models, Views, and Controllers?</span></span> <span data-ttu-id="a9ffc-107">V tomto kurzu Stephen Walther vás seznámí s různé části aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-107">In this tutorial, Stephen Walther introduces you to the different parts of an ASP.NET MVC application.</span></span>


<span data-ttu-id="a9ffc-108">Tento kurz obsahuje podrobný přehled ASP.NET MVC modelů, zobrazení a kontrolerů.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-108">This tutorial provides you with a high-level overview of ASP.NET MVC models, views, and controllers.</span></span> <span data-ttu-id="a9ffc-109">Jinými slovy, najdete v něm M ", V" a jazyka C "v architektuře ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-109">In other words, it explains the M', V', and C' in ASP.NET MVC.</span></span>

<span data-ttu-id="a9ffc-110">Po přečtení tohoto kurzu, měli byste porozumět, jak fungují společně různé části aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-110">After reading this tutorial, you should understand how the different parts of an ASP.NET MVC application work together.</span></span> <span data-ttu-id="a9ffc-111">Měli byste porozumět, jak architektury aplikace ASP.NET MVC se liší od aplikace webových formulářů ASP.NET nebo aplikace ASP.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-111">You should also understand how the architecture of an ASP.NET MVC application differs from an ASP.NET Web Forms application or Active Server Pages application.</span></span>

## <a name="the-sample-aspnet-mvc-application"></a><span data-ttu-id="a9ffc-112">Ukázkovou aplikaci ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="a9ffc-112">The Sample ASP.NET MVC Application</span></span>

<span data-ttu-id="a9ffc-113">Výchozí šablony sady Visual Studio pro vytváření webových aplikací ASP.NET MVC zahrnuje jednoduchost ukázkové aplikace, která slouží k pochopení různé části aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-113">The default Visual Studio template for creating ASP.NET MVC Web Applications includes an extremely simple sample application that can be used to understand the different parts of an ASP.NET MVC application.</span></span> <span data-ttu-id="a9ffc-114">Můžeme využít výhod této jednoduché aplikace najdete v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-114">We take advantage of this simple application in this tutorial.</span></span>

<span data-ttu-id="a9ffc-115">Vytvoření nové aplikace ASP.NET MVC pomocí šablony MVC spuštěním sady Visual Studio 2008 a vyberte možnost nabídky soubor, nový projekt (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="a9ffc-115">You create a new ASP.NET MVC application with the MVC template by launching Visual Studio 2008 and selecting the menu option File, New Project (see Figure 1).</span></span> <span data-ttu-id="a9ffc-116">V dialogovém okně Nový projekt, vyberte vašem oblíbeném programovacím jazyce podle typů projektu (Visual Basic nebo C#) a vyberte **webové aplikace ASP.NET MVC** v rámci šablony.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-116">In the New Project dialog, select your favorite programming language under Project Types (Visual Basic or C#) and select **ASP.NET MVC Web Application** under Templates.</span></span> <span data-ttu-id="a9ffc-117">Klikněte na tlačítko OK.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-117">Click the OK button.</span></span>


<span data-ttu-id="a9ffc-118">[![Dialogové okno nového projektu](understanding-models-views-and-controllers-cs/_static/image1.jpg)](understanding-models-views-and-controllers-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="a9ffc-118">[![New Project Dialog](understanding-models-views-and-controllers-cs/_static/image1.jpg)](understanding-models-views-and-controllers-cs/_static/image1.png)</span></span>

<span data-ttu-id="a9ffc-119">**Obrázek 01**: Dialogové okno nového projektu ([kliknutím ji zobrazíte obrázek v plné velikosti](understanding-models-views-and-controllers-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="a9ffc-119">**Figure 01**: New Project Dialog ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image2.png))</span></span>


<span data-ttu-id="a9ffc-120">Při vytváření nové aplikace ASP.NET MVC **vytvořit projekt testování částí** se zobrazí dialogové okno (viz obrázek 2).</span><span class="sxs-lookup"><span data-stu-id="a9ffc-120">When you create a new ASP.NET MVC application, the **Create Unit Test Project** dialog appears (see Figure 2).</span></span> <span data-ttu-id="a9ffc-121">Tento dialog umožňuje vytvořit samostatný projekt v řešení pro testování vašich aplikací ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-121">This dialog enables you to create a separate project in your solution for testing your ASP.NET MVC application.</span></span> <span data-ttu-id="a9ffc-122">Vyberte možnost **Ne, nevytvářejte projekt testování částí** a klikněte na tlačítko **OK** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-122">Select the option **No, do not create a unit test project** and click the **OK** button.</span></span>


<span data-ttu-id="a9ffc-123">[![Vytvořte testovací jednotky dialogové okno](understanding-models-views-and-controllers-cs/_static/image2.jpg)](understanding-models-views-and-controllers-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="a9ffc-123">[![Create Unit Test Dialog](understanding-models-views-and-controllers-cs/_static/image2.jpg)](understanding-models-views-and-controllers-cs/_static/image3.png)</span></span>

<span data-ttu-id="a9ffc-124">**Obrázek 02**: Vytvořte testovací jednotky dialogové okno ([kliknutím ji zobrazíte obrázek v plné velikosti](understanding-models-views-and-controllers-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="a9ffc-124">**Figure 02**: Create Unit Test Dialog ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image4.png))</span></span>


<span data-ttu-id="a9ffc-125">Aplikace se vytvoří po nové technologie ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-125">After the new ASP.NET MVC application is created.</span></span> <span data-ttu-id="a9ffc-126">Zobrazí se několik složek a souborů v okně Průzkumník řešení.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-126">You will see several folders and files in the Solution Explorer window.</span></span> <span data-ttu-id="a9ffc-127">Zejména uvidíte tři složky s názvem modelů, zobrazení a Kontrolerů.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-127">In particular, you'll see three folders named Models, Views, and Controllers.</span></span> <span data-ttu-id="a9ffc-128">Jak může uhodnout z názvy složek, tyto složky obsahují soubory pro implementaci modelů, zobrazení a kontrolerů.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-128">As you might guess from the folder names, these folders contain the files for implementing models, views, and controllers.</span></span>

<span data-ttu-id="a9ffc-129">Pokud rozbalíte složce řadiče, měli byste vidět soubor s názvem AccountController.cs a soubor s názvem HomeController.cs.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-129">If you expand the Controllers folder, you should see a file named AccountController.cs and a file named HomeController.cs.</span></span> <span data-ttu-id="a9ffc-130">Pokud rozbalíte složce zobrazení, měli byste vidět tři podsložky s názvem účtu, Home a sdílené.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-130">If you expand the Views folder, you should see three subfolders named Account, Home and Shared.</span></span> <span data-ttu-id="a9ffc-131">Pokud rozbalíte domovské složky, zobrazí se vám dva další soubory s názvem About.aspx a Index.aspx (viz obrázek 3).</span><span class="sxs-lookup"><span data-stu-id="a9ffc-131">If you expand the Home folder, you'll see two additional files named About.aspx and Index.aspx (see Figure 3).</span></span> <span data-ttu-id="a9ffc-132">Tyto soubory tvoří ukázkové aplikace je součástí výchozí šablony ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-132">These files make up the sample application included with the default ASP.NET MVC template.</span></span>


<span data-ttu-id="a9ffc-133">[![V okně Průzkumník řešení](understanding-models-views-and-controllers-cs/_static/image3.jpg)](understanding-models-views-and-controllers-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="a9ffc-133">[![The Solution Explorer Window](understanding-models-views-and-controllers-cs/_static/image3.jpg)](understanding-models-views-and-controllers-cs/_static/image5.png)</span></span>

<span data-ttu-id="a9ffc-134">**Obrázek 03**: V okně Průzkumník řešení ([kliknutím ji zobrazíte obrázek v plné velikosti](understanding-models-views-and-controllers-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="a9ffc-134">**Figure 03**: The Solution Explorer Window ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image6.png))</span></span>


<span data-ttu-id="a9ffc-135">Ukázkovou aplikaci můžete spustit tak, že vyberete možnost nabídky **ladit, spustit ladění**.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-135">You can run the sample application by selecting the menu option **Debug, Start Debugging**.</span></span> <span data-ttu-id="a9ffc-136">Alternativně můžete stisknutím klávesy F5.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-136">Alternatively, you can press the F5 key.</span></span>

<span data-ttu-id="a9ffc-137">Při prvním spuštění aplikace ASP.NET, zobrazí se dialogové okno na obrázku 4, která se doporučuje, abyste povolili režimu ladění.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-137">When you first run an ASP.NET application, the dialog in Figure 4 appears that recommends that you enable debug mode.</span></span> <span data-ttu-id="a9ffc-138">Klikněte na tlačítko OK a bude aplikace spuštěna.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-138">Click the OK button and the application will run.</span></span>


<span data-ttu-id="a9ffc-139">[![Ladění není povoleno dialogového okna](understanding-models-views-and-controllers-cs/_static/image4.jpg)](understanding-models-views-and-controllers-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="a9ffc-139">[![Debugging Not Enabled dialog](understanding-models-views-and-controllers-cs/_static/image4.jpg)](understanding-models-views-and-controllers-cs/_static/image7.png)</span></span>

<span data-ttu-id="a9ffc-140">**Obrázek 04**: Ladění není povoleno dialogového okna ([kliknutím ji zobrazíte obrázek v plné velikosti](understanding-models-views-and-controllers-cs/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="a9ffc-140">**Figure 04**: Debugging Not Enabled dialog ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image8.png))</span></span>


<span data-ttu-id="a9ffc-141">Při spuštění aplikace ASP.NET MVC, Visual Studio spustí aplikaci ve webovém prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-141">When you run an ASP.NET MVC application, Visual Studio launches the application in your web browser.</span></span> <span data-ttu-id="a9ffc-142">Ukázková aplikace se skládá pouze dvě stránky: indexovou stránku a na stránce o.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-142">The sample application consists of only two pages: the Index page and the About page.</span></span> <span data-ttu-id="a9ffc-143">Při prvním spuštění aplikace, zobrazí se stránka indexu (viz obrázek 5).</span><span class="sxs-lookup"><span data-stu-id="a9ffc-143">When the application first starts, the Index page appears (see Figure 5).</span></span> <span data-ttu-id="a9ffc-144">Můžete přejít na stránku o kliknutím na odkaz nabídce v horní části přímo z aplikace.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-144">You can navigate to the About page by clicking the menu link at the top right of the application.</span></span>


<span data-ttu-id="a9ffc-145">[![Index stránky](understanding-models-views-and-controllers-cs/_static/image10.png)](understanding-models-views-and-controllers-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="a9ffc-145">[![The Index Page](understanding-models-views-and-controllers-cs/_static/image10.png)](understanding-models-views-and-controllers-cs/_static/image9.png)</span></span>

<span data-ttu-id="a9ffc-146">**Obrázek 05**: Index stránky ([kliknutím ji zobrazíte obrázek v plné velikosti](understanding-models-views-and-controllers-cs/_static/image11.png))</span><span class="sxs-lookup"><span data-stu-id="a9ffc-146">**Figure 05**: The Index Page ([Click to view full-size image](understanding-models-views-and-controllers-cs/_static/image11.png))</span></span>


<span data-ttu-id="a9ffc-147">Všimněte si, že adresy URL do adresního řádku prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-147">Notice the URLs in the address bar of your browser.</span></span> <span data-ttu-id="a9ffc-148">Například když kliknete na odkaz o nabídce, adresy URL v adresním řádku prohlížeče se změní na **/Home/About**.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-148">For example, when you click the About menu link, the URL in the browser address bar changes to **/Home/About**.</span></span>

<span data-ttu-id="a9ffc-149">Pokud zavřete okno prohlížeče a vraťte se do sady Visual Studio, nebudete mít k nalezení souboru s domovem cesta/o.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-149">If you close the browser window and return to Visual Studio, you won't be able to find a file with the path Home/About.</span></span> <span data-ttu-id="a9ffc-150">Soubory neexistují.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-150">The files don't exist.</span></span> <span data-ttu-id="a9ffc-151">Jak je to možné?</span><span class="sxs-lookup"><span data-stu-id="a9ffc-151">How is this possible?</span></span>

## <a name="a-url-does-not-equal-a-page"></a><span data-ttu-id="a9ffc-152">Adresa URL se nerovná stránku</span><span class="sxs-lookup"><span data-stu-id="a9ffc-152">A URL Does Not Equal a Page</span></span>

<span data-ttu-id="a9ffc-153">Při sestavování tradiční aplikace webových formulářů ASP.NET nebo Active Server Pages aplikace existuje shoda mezi adresy URL a na stránce.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-153">When you build a traditional ASP.NET Web Forms application or an Active Server Pages application, there is a one-to-one correspondence between a URL and a page.</span></span> <span data-ttu-id="a9ffc-154">Pokud jste požádali o stránku s názvem SomePage.aspx ze serveru, pak měli lépe existovat stránku na disk s názvem SomePage.aspx.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-154">If you request a page named SomePage.aspx from the server, then there had better be a page on disk named SomePage.aspx.</span></span> <span data-ttu-id="a9ffc-155">Pokud se soubor SomePage.aspx neexistuje, dojde bez zbytečných prvků **404 – Stránka nebyla nalezena** chyby.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-155">If the SomePage.aspx file does not exist, you get an ugly **404 - Page Not Found** error.</span></span>

<span data-ttu-id="a9ffc-156">Při sestavování aplikace ASP.NET MVC, naproti tomu neexistuje žádná souvislost mezi adresu URL, kterou zadáte do panelu Adresa v prohlížeči a soubory, které můžete najít ve vaší aplikaci.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-156">When building an ASP.NET MVC application, in contrast, there is no correspondence between the URL that you type into your browser's address bar and the files that you find in your application.</span></span> <span data-ttu-id="a9ffc-157">V aplikaci ASP.NET MVC adresa URL odpovídá místo na disku na stránce akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-157">In an ASP.NET MVC application, a URL corresponds to a controller action instead of a page on disk.</span></span>

<span data-ttu-id="a9ffc-158">V tradiční aplikace ASP.NET nebo ASP prohlížeč požadavek mapovaný na stránky.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-158">In a traditional ASP.NET or ASP application, browser requests are mapped to pages.</span></span> <span data-ttu-id="a9ffc-159">V aplikaci ASP.NET MVC naproti tomu prohlížeč požadavky se mapují na akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-159">In an ASP.NET MVC application, in contrast, browser requests are mapped to controller actions.</span></span> <span data-ttu-id="a9ffc-160">Aplikace webových formulářů technologie ASP.NET je zaměřené na obsah.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-160">An ASP.NET Web Forms application is content-centric.</span></span> <span data-ttu-id="a9ffc-161">Aplikace ASP.NET MVC, je naopak zaměřenou na logiku aplikace.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-161">An ASP.NET MVC application, in contrast, is application logic centric.</span></span>

## <a name="understanding-aspnet-routing"></a><span data-ttu-id="a9ffc-162">Vysvětlení směrování ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a9ffc-162">Understanding ASP.NET Routing</span></span>

<span data-ttu-id="a9ffc-163">Získá mapovat žádost prohlížeče na akce kontroleru prostřednictvím funkce technologie ASP.NET framework, volá se, *směrování ASP.NET*.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-163">A browser request gets mapped to a controller action through a feature of the ASP.NET framework called *ASP.NET Routing*.</span></span> <span data-ttu-id="a9ffc-164">Směrování ASP.NET používá rozhraní ASP.NET MVC do *trasy* příchozí požadavky na akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-164">ASP.NET Routing is used by the ASP.NET MVC framework to *route* incoming requests to controller actions.</span></span>

<span data-ttu-id="a9ffc-165">Směrovací tabulku směrování ASP.NET používá ke zpracování příchozích požadavků.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-165">ASP.NET Routing uses a route table to handle incoming requests.</span></span> <span data-ttu-id="a9ffc-166">Tato tabulka trasy se vytvoří při prvním spuštění vaší webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-166">This route table is created when your web application first starts.</span></span> <span data-ttu-id="a9ffc-167">Směrovací tabulky se nastavení v souboru Global.asax.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-167">The route table is setup in the Global.asax file.</span></span> <span data-ttu-id="a9ffc-168">Výchozí soubor MVC Global.asax je součástí výpis 1.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-168">The default MVC Global.asax file is contained in Listing 1.</span></span>

<span data-ttu-id="a9ffc-169">**Listing 1 - Global.asax**</span><span class="sxs-lookup"><span data-stu-id="a9ffc-169">**Listing 1 - Global.asax**</span></span>

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample1.cs)]

<span data-ttu-id="a9ffc-170">Když poprvé spustí aplikace technologie ASP.NET, aplikace\_volání metody Start().</span><span class="sxs-lookup"><span data-stu-id="a9ffc-170">When an ASP.NET application first starts, the Application\_Start() method is called.</span></span> <span data-ttu-id="a9ffc-171">Ve výpisu 1 Tato metoda volá metodu RegisterRoutes() a metoda RegisterRoutes() vytvoří výchozí směrovací tabulka.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-171">In Listing 1, this method calls the RegisterRoutes() method and the RegisterRoutes() method creates the default route table.</span></span>

<span data-ttu-id="a9ffc-172">Výchozí směrovací tabulka se skládá z jednoho z nich.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-172">The default route table consists of one route.</span></span> <span data-ttu-id="a9ffc-173">Všechny příchozí požadavky této výchozí trase rozdělí do tří segmentů (segment adresy URL se něco mezi lomítka).</span><span class="sxs-lookup"><span data-stu-id="a9ffc-173">This default route breaks all incoming requests into three segments (a URL segment is anything between forward slashes).</span></span> <span data-ttu-id="a9ffc-174">První segment se mapuje na název kontroleru, druhý segment se mapuje na název akce a posledního segmentu je namapována na parametr předaný akce s názvem ID.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-174">The first segment is mapped to a controller name, the second segment is mapped to an action name, and the final segment is mapped to a parameter passed to the action named Id.</span></span>

<span data-ttu-id="a9ffc-175">Představte si třeba následující adresu URL:</span><span class="sxs-lookup"><span data-stu-id="a9ffc-175">For example, consider the following URL:</span></span>

<span data-ttu-id="a9ffc-176">/ Produkt/podrobnosti/3</span><span class="sxs-lookup"><span data-stu-id="a9ffc-176">/Product/Details/3</span></span>

<span data-ttu-id="a9ffc-177">Tato adresa URL je analyzován do tří parametrů takto:</span><span class="sxs-lookup"><span data-stu-id="a9ffc-177">This URL is parsed into three parameters like this:</span></span>

<span data-ttu-id="a9ffc-178">Kontroler = produktu</span><span class="sxs-lookup"><span data-stu-id="a9ffc-178">Controller = Product</span></span>

<span data-ttu-id="a9ffc-179">Akce = podrobnosti</span><span class="sxs-lookup"><span data-stu-id="a9ffc-179">Action = Details</span></span>

<span data-ttu-id="a9ffc-180">Id = 3</span><span class="sxs-lookup"><span data-stu-id="a9ffc-180">Id = 3</span></span>

<span data-ttu-id="a9ffc-181">Výchozí trasy definované v souboru Global.asax obsahuje výchozí hodnoty pro všemi třemi parametry.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-181">The Default route defined in the Global.asax file includes default values for all three parameters.</span></span> <span data-ttu-id="a9ffc-182">Je výchozí kontroler Home, výchozí akce je Index a výchozí hodnota Id je prázdný řetězec.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-182">The default Controller is Home, the default Action is Index, and the default Id is an empty string.</span></span> <span data-ttu-id="a9ffc-183">U tyto výchozí hodnoty na paměti zvažte, jak je analyzován na následující adrese URL:</span><span class="sxs-lookup"><span data-stu-id="a9ffc-183">With these defaults in mind, consider how the following URL is parsed:</span></span>

<span data-ttu-id="a9ffc-184">/ Zaměstnance</span><span class="sxs-lookup"><span data-stu-id="a9ffc-184">/Employee</span></span>

<span data-ttu-id="a9ffc-185">Tato adresa URL je analyzován do tří parametrů takto:</span><span class="sxs-lookup"><span data-stu-id="a9ffc-185">This URL is parsed into three parameters like this:</span></span>

<span data-ttu-id="a9ffc-186">Kontroler = zaměstnance</span><span class="sxs-lookup"><span data-stu-id="a9ffc-186">Controller = Employee</span></span>

<span data-ttu-id="a9ffc-187">Akce = Index</span><span class="sxs-lookup"><span data-stu-id="a9ffc-187">Action = Index</span></span>

<span data-ttu-id="a9ffc-188">Id = ��</span><span class="sxs-lookup"><span data-stu-id="a9ffc-188">Id = ��</span></span>

<span data-ttu-id="a9ffc-189">Nakonec otevřete aplikaci ASP.NET MVC bez poskytnutí libovolnou adresu URL (například `http://localhost`) pak adresa URL se zpracuje tímto způsobem:</span><span class="sxs-lookup"><span data-stu-id="a9ffc-189">Finally, if you open an ASP.NET MVC Application without supplying any URL (for example, `http://localhost`) then the URL is parsed like this:</span></span>

<span data-ttu-id="a9ffc-190">Kontroler = Home</span><span class="sxs-lookup"><span data-stu-id="a9ffc-190">Controller = Home</span></span>

<span data-ttu-id="a9ffc-191">Akce = Index</span><span class="sxs-lookup"><span data-stu-id="a9ffc-191">Action = Index</span></span>

<span data-ttu-id="a9ffc-192">Id = ��</span><span class="sxs-lookup"><span data-stu-id="a9ffc-192">Id = ��</span></span>

<span data-ttu-id="a9ffc-193">Požadavek se přesměruje na akci Index() HomeController třídy.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-193">The request is routed to the Index() action on the HomeController class.</span></span>

## <a name="understanding-controllers"></a><span data-ttu-id="a9ffc-194">Vysvětlení Kontrolerů</span><span class="sxs-lookup"><span data-stu-id="a9ffc-194">Understanding Controllers</span></span>

<span data-ttu-id="a9ffc-195">Kontroler je zodpovědná za řízení tak, jak uživatel komunikuje s aplikaci MVC.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-195">A controller is responsible for controlling the way that a user interacts with an MVC application.</span></span> <span data-ttu-id="a9ffc-196">Kontroler obsahuje logiku řízení toku pro aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-196">A controller contains the flow control logic for an ASP.NET MVC application.</span></span> <span data-ttu-id="a9ffc-197">Kontroler Určuje, jaké odpověď k odeslání zpět na uživatele, když uživatel provede požadavek prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-197">A controller determines what response to send back to a user when a user makes a browser request.</span></span>

<span data-ttu-id="a9ffc-198">Kontroler je právě třídy (například třídy jazyka Visual Basic nebo C#).</span><span class="sxs-lookup"><span data-stu-id="a9ffc-198">A controller is just a class (for example, a Visual Basic or C# class).</span></span> <span data-ttu-id="a9ffc-199">Ukázka aplikace ASP.NET MVC zahrnuje řadič HomeController.cs ve složce řadiče.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-199">The sample ASP.NET MVC application includes a controller named HomeController.cs located in the Controllers folder.</span></span> <span data-ttu-id="a9ffc-200">Obsah souboru HomeController.cs je uveden v informacích 2.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-200">The content of the HomeController.cs file is reproduced in Listing 2.</span></span>

<span data-ttu-id="a9ffc-201">**Výpis 2 - HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="a9ffc-201">**Listing 2 - HomeController.cs**</span></span>

[!code-csharp[Main](understanding-models-views-and-controllers-cs/samples/sample2.cs)]

<span data-ttu-id="a9ffc-202">Všimněte si, HomeController má dvě metody s názvem Index() a About().</span><span class="sxs-lookup"><span data-stu-id="a9ffc-202">Notice that the HomeController has two methods named Index() and About().</span></span> <span data-ttu-id="a9ffc-203">Tyto dvě metody odpovídají dvě akce vystavené kontroleru.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-203">These two methods correspond to the two actions exposed by the controller.</span></span> <span data-ttu-id="a9ffc-204">Adresa URL/Home/Index vyvolá metodu HomeController.Index() a adresy URL/Home/o vyvolá metodu HomeController.About().</span><span class="sxs-lookup"><span data-stu-id="a9ffc-204">The URL /Home/Index invokes the HomeController.Index() method and the URL /Home/About invokes the HomeController.About() method.</span></span>

<span data-ttu-id="a9ffc-205">Všechny veřejné metody v kontroleru je vystavena jako akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-205">Any public method in a controller is exposed as a controller action.</span></span> <span data-ttu-id="a9ffc-206">Musíte být opatrní při to.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-206">You need to be careful about this.</span></span> <span data-ttu-id="a9ffc-207">To znamená, že všechny veřejné metody obsažené v kontroleru, každý, kdo má přístup k Internetu jde vyvolat zadáním správné adresy URL do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-207">This means that any public method contained in a controller can be invoked by anyone with access to the Internet by entering the right URL into a browser.</span></span>

## <a name="understanding-views"></a><span data-ttu-id="a9ffc-208">Principy zobrazení</span><span class="sxs-lookup"><span data-stu-id="a9ffc-208">Understanding Views</span></span>

<span data-ttu-id="a9ffc-209">Akce dvě kontroleru vystavené třídu HomeController Index() a About(), jak vrátit zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-209">The two controller actions exposed by the HomeController class, Index() and About(), both return a view.</span></span> <span data-ttu-id="a9ffc-210">Zobrazení obsahuje kód HTML a obsah, který je odesláno prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-210">A view contains the HTML markup and content that is sent to the browser.</span></span> <span data-ttu-id="a9ffc-211">Zobrazení je ekvivalentem stránky při práci s aplikací ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-211">A view is the equivalent of a page when working with an ASP.NET MVC application.</span></span>

<span data-ttu-id="a9ffc-212">Je třeba vytvořit zobrazení na správném místě.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-212">You must create your views in the right location.</span></span> <span data-ttu-id="a9ffc-213">Akce HomeController.Index() vrátí zobrazení nachází v následujícím umístění:</span><span class="sxs-lookup"><span data-stu-id="a9ffc-213">The HomeController.Index() action returns a view located at the following path:</span></span>

<span data-ttu-id="a9ffc-214">\Views\Home\Index.aspx</span><span class="sxs-lookup"><span data-stu-id="a9ffc-214">\Views\Home\Index.aspx</span></span>

<span data-ttu-id="a9ffc-215">Akce HomeController.About() vrátí zobrazení nachází v následujícím umístění:</span><span class="sxs-lookup"><span data-stu-id="a9ffc-215">The HomeController.About() action returns a view located at the following path:</span></span>

<span data-ttu-id="a9ffc-216">\Views\Home\About.aspx</span><span class="sxs-lookup"><span data-stu-id="a9ffc-216">\Views\Home\About.aspx</span></span>

<span data-ttu-id="a9ffc-217">Obecně platí Pokud budete chtít vrátit zobrazení pro akce kontroleru, musíte vytvořit podsložku ve složce zobrazení se stejným názvem jako řadiče.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-217">In general, if you want to return a view for a controller action, then you need to create a subfolder in the Views folder with the same name as your controller.</span></span> <span data-ttu-id="a9ffc-218">V podsložce musíte vytvořit soubor .aspx se stejným názvem jako akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-218">Within the subfolder, you must create an .aspx file with the same name as the controller action.</span></span>

<span data-ttu-id="a9ffc-219">Soubor výpisu 3 obsahuje About.aspx zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-219">The file in Listing 3 contains the About.aspx view.</span></span>

<span data-ttu-id="a9ffc-220">**Výpis 3 - About.aspx**</span><span class="sxs-lookup"><span data-stu-id="a9ffc-220">**Listing 3 - About.aspx**</span></span>

[!code-aspx[Main](understanding-models-views-and-controllers-cs/samples/sample3.aspx)]

<span data-ttu-id="a9ffc-221">Pokud budete ignorovat prvního řádku v zobrazení 3, většina ostatních zobrazení se skládá z standardní HTML.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-221">If you ignore the first line in Listing 3, most of the rest of the view consists of standard HTML.</span></span> <span data-ttu-id="a9ffc-222">Obsah zobrazení můžete upravit tak, že zadáte veškeré kódování HTML, který chcete, aby zde.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-222">You can modify the contents of the view by entering any HTML that you want here.</span></span>

<span data-ttu-id="a9ffc-223">Zobrazení je velmi podobný stránky ASP nebo ASP.NET webové formuláře.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-223">A view is very similar to a page in Active Server Pages or ASP.NET Web Forms.</span></span> <span data-ttu-id="a9ffc-224">Zobrazení může obsahovat obsah ve formátu HTML a skripty.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-224">A view can contain HTML content and scripts.</span></span> <span data-ttu-id="a9ffc-225">Napíšete skripty v oblíbeném .NET programovací jazyk (například C# nebo Visual Basic .NET).</span><span class="sxs-lookup"><span data-stu-id="a9ffc-225">You can write the scripts in your favorite .NET programming language (for example, C# or Visual Basic .NET).</span></span> <span data-ttu-id="a9ffc-226">Pomocí skriptů zobrazují dynamický obsah, jako je například dat z databáze.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-226">You use scripts to display dynamic content such as database data.</span></span>

## <a name="understanding-models"></a><span data-ttu-id="a9ffc-227">Principy modelů</span><span class="sxs-lookup"><span data-stu-id="a9ffc-227">Understanding Models</span></span>

<span data-ttu-id="a9ffc-228">Mít jsme probírali řadiče a mít jsme probírali zobrazení.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-228">We have discussed controllers and we have discussed views.</span></span> <span data-ttu-id="a9ffc-229">Poslední téma, které potřebujeme fattica je modely.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-229">The last topic that we need to discuss is models.</span></span> <span data-ttu-id="a9ffc-230">Co je MVC model?</span><span class="sxs-lookup"><span data-stu-id="a9ffc-230">What is an MVC model?</span></span>

<span data-ttu-id="a9ffc-231">MVC model obsahuje všechny vaše aplikační logiky, která není součástí zobrazení nebo kontroleru.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-231">An MVC model contains all of your application logic that is not contained in a view or a controller.</span></span> <span data-ttu-id="a9ffc-232">Model by měl obsahovat všechny vaše obchodní logiky aplikace, logiku ověřování a logiky přístupu k databázi.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-232">The model should contain all of your application business logic, validation logic, and database access logic.</span></span> <span data-ttu-id="a9ffc-233">Například pokud Microsoft Entity Framework používají pro přístup k vaší databázi, potom by vytvoříte třídy Entity Framework (soubor .edmx) ve složce modely.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-233">For example, if you are using the Microsoft Entity Framework to access your database, then you would create your Entity Framework classes (your .edmx file) in the Models folder.</span></span>

<span data-ttu-id="a9ffc-234">Zobrazení může obsahovat pouze logiku související generování uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-234">A view should contain only logic related to generating the user interface.</span></span> <span data-ttu-id="a9ffc-235">Kontroler může obsahovat jenom úplné minimální logiku potřebnou k vrácení z druhého zobrazení nebo přesměrovat uživatele na jinou akci (řízení toku).</span><span class="sxs-lookup"><span data-stu-id="a9ffc-235">A controller should only contain the bare minimum of logic required to return the right view or redirect the user to another action (flow control).</span></span> <span data-ttu-id="a9ffc-236">Všechno ostatní, měly by být součástí modelu.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-236">Everything else should be contained in the model.</span></span>

<span data-ttu-id="a9ffc-237">Obecně platí je nutné snažit pro fat modely a tenké kontrolery.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-237">In general, you should strive for fat models and skinny controllers.</span></span> <span data-ttu-id="a9ffc-238">Vaše metody kontroleru by měl obsahovat jenom pár řádků kódu.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-238">Your controller methods should contain only a few lines of code.</span></span> <span data-ttu-id="a9ffc-239">Získá příliš fat-akce kontroleru, pak zvažte přesunutí logiky na novou třídu ve složce modely.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-239">If a controller action gets too fat, then you should consider moving the logic out to a new class in the Models folder.</span></span>

## <a name="summary"></a><span data-ttu-id="a9ffc-240">Souhrn</span><span class="sxs-lookup"><span data-stu-id="a9ffc-240">Summary</span></span>

<span data-ttu-id="a9ffc-241">V tomto kurzu vám poskytuje základní přehled různých součástí ASP.NET MVC webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-241">This tutorial provided you with a high level overview of the different parts of an ASP.NET MVC web application.</span></span> <span data-ttu-id="a9ffc-242">Jste se naučili, jak směrování ASP.NET mapuje příchozí požadavky na prohlížeč pro určitý kontroler akce.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-242">You learned how ASP.NET Routing maps incoming browser requests to particular controller actions.</span></span> <span data-ttu-id="a9ffc-243">Jste se naučili, jak orchestrovat řadiče jak zobrazení se vrátí do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-243">You learned how controllers orchestrate how views are returned to the browser.</span></span> <span data-ttu-id="a9ffc-244">Nakonec jste zjistili, jak modely obsahovat obchodní aplikace, ověření a logiky přístupu k databázi.</span><span class="sxs-lookup"><span data-stu-id="a9ffc-244">Finally, you learned how models contain application business, validation, and database access logic.</span></span>
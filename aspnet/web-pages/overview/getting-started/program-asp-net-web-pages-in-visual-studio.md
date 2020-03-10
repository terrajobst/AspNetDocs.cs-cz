---
uid: aspnet/web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
title: Programování webových stránek ASP.NET (Razor) pomocí sady Visual Studio | Microsoft Docs
author: Rick-Anderson
description: V tomto dodatku se dozvíte, jak můžete pomocí syntaxe Razor použít Visual Studio 2010 nebo Visual Web Developer 2010 Express k programování webových stránek ASP.NET.
ms.author: riande
ms.date: 02/13/2014
ms.assetid: 0acfec5a-48f2-4766-a801-a0f426966f0a
msc.legacyurl: /web-pages/overview/getting-started/program-asp-net-web-pages-in-visual-studio
msc.type: authoredcontent
ms.openlocfilehash: 1a76098779d05912bf7bdf2de5fdce024770752c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78633509"
---
# <a name="programming-aspnet-web-pages-razor-using-visual-studio"></a><span data-ttu-id="427d2-103">Programování webových stránek ASP.NET (Razor) pomocí sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="427d2-103">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>

<span data-ttu-id="427d2-104">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="427d2-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="427d2-105">Tento článek vysvětluje, jak můžete použít aplikaci Visual Studio nebo Visual Web Developer Express k programování webů ASP.NET Web Pages (Razor).</span><span class="sxs-lookup"><span data-stu-id="427d2-105">This article explains how you can use Visual Studio or Visual Web Developer Express to program ASP.NET Web Pages (Razor) websites.</span></span>
>
> <span data-ttu-id="427d2-106">Co se dozvíte</span><span class="sxs-lookup"><span data-stu-id="427d2-106">What you'll learn</span></span>
>
> - <span data-ttu-id="427d2-107">Co je potřeba nainstalovat (Pokud cokoli) pro práci s ASP.NET webovými stránkami ve vaší verzi sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="427d2-107">What you need to install (if anything) to work with ASP.NET Web Pages in your version of Visual Studio.</span></span>
> - <span data-ttu-id="427d2-108">Přidání podpory pro webové stránky ASP.NET do aplikace Visual Web Developer 2010 Express.</span><span class="sxs-lookup"><span data-stu-id="427d2-108">How to add support for ASP.NET Web Pages to Visual Web Developer 2010 Express.</span></span>
> - <span data-ttu-id="427d2-109">Jak používat funkce v aplikaci Visual Studio pro práci se stránkami ASP.NET Razor, včetně IntelliSense a ladicího programu.</span><span class="sxs-lookup"><span data-stu-id="427d2-109">How to use features in Visual Studio to work with ASP.NET Razor pages, including IntelliSense and the debugger.</span></span>
>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="427d2-110">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="427d2-110">Software versions used in the tutorial</span></span>
>
>
> - <span data-ttu-id="427d2-111">Webové stránky ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="427d2-111">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="427d2-112">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="427d2-112">Visual Studio 2013</span></span>
> - <span data-ttu-id="427d2-113">WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="427d2-113">WebMatrix 3</span></span>
>
>
> <span data-ttu-id="427d2-114">Tento kurz funguje také s ASP.NET webovými stránkami 2, Visual Studio 2012, Visual Studio 2010 a WebMatrix 2.</span><span class="sxs-lookup"><span data-stu-id="427d2-114">This tutorial also works with ASP.NET Web Pages 2, Visual Studio 2012, Visual Studio 2010, and WebMatrix 2.</span></span>

<span data-ttu-id="427d2-115">ASP.NET webové syntaxe Razor stránky můžete programovat pomocí WebMatrixu nebo mnoha dalších editorů kódu.</span><span class="sxs-lookup"><span data-stu-id="427d2-115">You can program ASP.NET Web pages with Razor syntax using WebMatrix or many other code editors.</span></span> <span data-ttu-id="427d2-116">Můžete také použít Microsoft Visual Studio, což je integrované vývojové prostředí (IDE), které poskytuje výkonnou sadu nástrojů pro vytváření mnoha typů aplikací (nikoli jenom webů).</span><span class="sxs-lookup"><span data-stu-id="427d2-116">You can also use Microsoft Visual Studio which is a full-featured integrated development environment (IDE) that provides a powerful set of tools for creating many types of applications (not just websites).</span></span> <span data-ttu-id="427d2-117">Chcete-li pracovat se ASP.NET Razor Pages, můžete použít [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span><span class="sxs-lookup"><span data-stu-id="427d2-117">To work with ASP.NET Razor pages, you can use [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span>

<span data-ttu-id="427d2-118">Dvě užitečné funkce, které Visual Studio poskytuje pro programování s webovými stránkami ASP.NET Razor, jsou tyto:</span><span class="sxs-lookup"><span data-stu-id="427d2-118">Two particularly useful features that Visual Studio provides for programming with ASP.NET Razor web pages are:</span></span>

- <span data-ttu-id="427d2-119">*IntelliSense*.</span><span class="sxs-lookup"><span data-stu-id="427d2-119">*IntelliSense*.</span></span> <span data-ttu-id="427d2-120">Funkce IntelliSense integrovaná do sady Visual Studio je komplexnější než IntelliSense ve WebMatrixu.</span><span class="sxs-lookup"><span data-stu-id="427d2-120">The IntelliSense feature built into Visual Studio is more comprehensive than IntelliSense in WebMatrix.</span></span>
- <span data-ttu-id="427d2-121">*Ladicí program*.</span><span class="sxs-lookup"><span data-stu-id="427d2-121">*Debugger*.</span></span> <span data-ttu-id="427d2-122">Ladicí program vám umožní vyřešit potíže s kódem zastavením programu, který je spuštěný, prozkoumáním proměnných a krokování kódem řádek po řádku.</span><span class="sxs-lookup"><span data-stu-id="427d2-122">The debugger lets you troubleshoot your code by stopping a program while it's running, examining variables, and stepping through the code line by line.</span></span>

## <a name="using-visual-studio-with-different-versions-of-aspnet-web-pages"></a><span data-ttu-id="427d2-123">Použití sady Visual Studio s různými verzemi ASP.NET webových stránek</span><span class="sxs-lookup"><span data-stu-id="427d2-123">Using Visual Studio with Different Versions of ASP.NET Web Pages</span></span>

<span data-ttu-id="427d2-124">Chcete-li vyvíjet webové aplikace v ASP.NET v aplikaci Visual Studio 2017, nainstalujte úlohu **vývoje ASP.NET a webu** .</span><span class="sxs-lookup"><span data-stu-id="427d2-124">To develop ASP.NET web apps in Visual Studio 2017, install the **ASP.NET and web development** workload.</span></span>

<span data-ttu-id="427d2-125">Visual Studio 2012 a Visual Studio 2013 zahrnují podporu pro webové stránky ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="427d2-125">Visual Studio 2012 and Visual Studio 2013 include support for ASP.NET Web Pages.</span></span> <span data-ttu-id="427d2-126">(Balíčky, které jsou nutné k podpoře webových stránek ASP.NET, se instalují při instalaci sady Visual Studio.)</span><span class="sxs-lookup"><span data-stu-id="427d2-126">(The packages that are required in order to support ASP.NET Web Pages are installed when you install Visual Studio.)</span></span>

<span data-ttu-id="427d2-127">Visual Studio 2010 ve výchozím nastavení neobsahuje podporu pro webové stránky ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="427d2-127">Visual Studio 2010 does not include support by default for ASP.NET Web Pages.</span></span> <span data-ttu-id="427d2-128">Chcete-li používat webové stránky ASP.NET se sadou Visual Studio 2010, je nutné nainstalovat balíček ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="427d2-128">To use ASP.NET Web Pages with Visual Studio 2010, you must install the ASP.NET MVC package.</span></span> <span data-ttu-id="427d2-129">Pokud chcete získat ASP.NET webové stránky 2, nainstalujte ASP.NET MVC 4.</span><span class="sxs-lookup"><span data-stu-id="427d2-129">To get ASP.NET Web Pages 2, you install ASP.NET MVC 4.</span></span>

<span data-ttu-id="427d2-130">Následující tabulka shrnuje podporu pro webové stránky ASP.NET v různých verzích sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="427d2-130">The following table summarizes the support for ASP.NET Web Pages in different versions of Visual Studio.</span></span>

|  | <span data-ttu-id="427d2-131">Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="427d2-131">Visual Studio 2010</span></span> | <span data-ttu-id="427d2-132">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="427d2-132">Visual Studio 2012</span></span> | <span data-ttu-id="427d2-133">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="427d2-133">Visual Studio 2013</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="427d2-134">**ASP.NET webové stránky 2**</span><span class="sxs-lookup"><span data-stu-id="427d2-134">**ASP.NET Web Pages 2**</span></span> | <span data-ttu-id="427d2-135">Instalace ASP.NET MVC 4</span><span class="sxs-lookup"><span data-stu-id="427d2-135">Install ASP.NET MVC 4</span></span> | <span data-ttu-id="427d2-136">Obsaženy</span><span class="sxs-lookup"><span data-stu-id="427d2-136">(Included)</span></span> | <span data-ttu-id="427d2-137">Obsaženy</span><span class="sxs-lookup"><span data-stu-id="427d2-137">(Included)</span></span> |
| <span data-ttu-id="427d2-138">**Webové stránky ASP.NET 3**</span><span class="sxs-lookup"><span data-stu-id="427d2-138">**ASP.NET Web Pages 3**</span></span> |  | <span data-ttu-id="427d2-139">Aktualizace na ASP.NET webové stránky 3 přes NuGet</span><span class="sxs-lookup"><span data-stu-id="427d2-139">Update to ASP.NET Web Pages 3 through NuGet</span></span> | <span data-ttu-id="427d2-140">Obsaženy</span><span class="sxs-lookup"><span data-stu-id="427d2-140">(Included)</span></span> |

<span data-ttu-id="427d2-141">Chcete-li pracovat se sadou Visual Studio 2010, přečtěte si téma [Instalace podpory pro webové stránky ASP.NET v aplikaci Visual studio 2010](#vs2010support).</span><span class="sxs-lookup"><span data-stu-id="427d2-141">To work with Visual Studio 2010, see [Installing Support for ASP.NET Web Pages in Visual Studio 2010](#vs2010support).</span></span>

## <a name="launching-visual-studio-from-webmatrix"></a><span data-ttu-id="427d2-142">Spouští se Visual Studio z WebMatrixu.</span><span class="sxs-lookup"><span data-stu-id="427d2-142">Launching Visual Studio from WebMatrix</span></span>

<span data-ttu-id="427d2-143">Pokud jste spustili projekt ve WebMatrixu a chcete přepnout na Visual Studio, WebMatrix poskytuje tlačítko pro snadné otevření projektu v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="427d2-143">If you have started a project in WebMatrix and want to switch to Visual Studio, WebMatrix provides a button to easily open the project in Visual Studio.</span></span> <span data-ttu-id="427d2-144">Aby bylo toto tlačítko povoleno, je nutné mít v počítači nainstalovánu aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="427d2-144">You must have Visual Studio installed on your computer for this button to be enabled.</span></span> <span data-ttu-id="427d2-145">Na následujícím obrázku je znázorněno tlačítko v WebMatrixu.</span><span class="sxs-lookup"><span data-stu-id="427d2-145">The following image shows the button in WebMatrix.</span></span>

![Spustit Visual Studio](program-asp-net-web-pages-in-visual-studio/_static/image1.png)

<span data-ttu-id="427d2-147">Po kliknutí na tlačítko se projekt otevře v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="427d2-147">When you click the button, the project is opened in Visual Studio.</span></span> <span data-ttu-id="427d2-148">Můžete přepínat mezi webmaticí a Visual Studio bez problémů.</span><span class="sxs-lookup"><span data-stu-id="427d2-148">You can switch back and forth between WebMatrix and Visual Studio without any problems.</span></span> <span data-ttu-id="427d2-149">Budete upozorněni, pokud se některé soubory změnily v jiném prostředí a potřebujete je znovu načíst, abyste získali nejnovější změny.</span><span class="sxs-lookup"><span data-stu-id="427d2-149">You will be notified if any files have changed in the other environment and need to be reloaded to get the latest changes.</span></span>

## <a name="creating-aspnet-razor-site-in-visual-studio"></a><span data-ttu-id="427d2-150">Vytvoření webu ASP.NET Razor v aplikaci Visual Studio</span><span class="sxs-lookup"><span data-stu-id="427d2-150">Creating ASP.NET Razor Site in Visual Studio</span></span>

<span data-ttu-id="427d2-151">Vytvoření webu ASP.NET Razor v aplikaci Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="427d2-151">To create an ASP.NET Razor website in Visual Studio:</span></span>

1. <span data-ttu-id="427d2-152">Otevřete sadu Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="427d2-152">Open Visual Studio.</span></span>
2. <span data-ttu-id="427d2-153">V nabídce **soubor** klikněte na příkaz **Nový web**.</span><span class="sxs-lookup"><span data-stu-id="427d2-153">In the **File** menu, click **New Web Site**.</span></span>

    ![vytvořit nový web](program-asp-net-web-pages-in-visual-studio/_static/image2.png)
3. <span data-ttu-id="427d2-155">V dialogovém okně **Nový web** vyberte jazyk, který chcete použít (vizuál C# nebo Visual Basic).</span><span class="sxs-lookup"><span data-stu-id="427d2-155">In the **New Web Site** dialog box, select the language to use (Visual C# or Visual Basic).</span></span>
4. <span data-ttu-id="427d2-156">Vyberte šablonu **web web ASP.NET (Razor)** .</span><span class="sxs-lookup"><span data-stu-id="427d2-156">Select the **ASP.NET Web Site (Razor)** template.</span></span>

    ![Web Razor](program-asp-net-web-pages-in-visual-studio/_static/image3.png)
5. <span data-ttu-id="427d2-158">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="427d2-158">Click **OK**.</span></span>

<span data-ttu-id="427d2-159">Nový projekt existuje a je naplněný s některými výchozími webovými stránkami, které vám pomůžou začít.</span><span class="sxs-lookup"><span data-stu-id="427d2-159">Your new project exists and is populated with some default web pages to help you get started.</span></span>

### <a name="using-intellisense"></a><span data-ttu-id="427d2-160">Používání atributu IntelliSense</span><span class="sxs-lookup"><span data-stu-id="427d2-160">Using IntelliSense</span></span>

<span data-ttu-id="427d2-161">Teď, když jste vytvořili lokalitu, uvidíte, jak funguje technologie IntelliSense v sadě Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="427d2-161">Now that you've created a site, you can see how IntelliSense works in Visual Studio.</span></span>

1. <span data-ttu-id="427d2-162">Na webu, který jste právě vytvořili, otevřete stránku *Default. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="427d2-162">In the website you just created, open the *Default.cshtml* page.</span></span>
2. <span data-ttu-id="427d2-163">Po `<h3>` značek na stránce zadejte `@ServerInfo.` (včetně tečky).</span><span class="sxs-lookup"><span data-stu-id="427d2-163">After the `<h3>` tags in the page, type `@ServerInfo.` (including the dot).</span></span> <span data-ttu-id="427d2-164">Všimněte si, jak IntelliSense zobrazuje dostupné metody pro pomoc `ServerInfo` v rozevíracím seznamu.</span><span class="sxs-lookup"><span data-stu-id="427d2-164">Notice how IntelliSense displays the available methods for the `ServerInfo` helper in a drop-down list.</span></span>

    ![IntelliSense](program-asp-net-web-pages-in-visual-studio/_static/image4.png)
3. <span data-ttu-id="427d2-166">V seznamu vyberte metodu `GetHtml` a stiskněte klávesu ENTER.</span><span class="sxs-lookup"><span data-stu-id="427d2-166">Select the `GetHtml` method from the list and then press Enter.</span></span> <span data-ttu-id="427d2-167">Technologie IntelliSense automaticky vyplní metodu.</span><span class="sxs-lookup"><span data-stu-id="427d2-167">IntelliSense automatically fills in the method.</span></span> <span data-ttu-id="427d2-168">(Stejně jako u libovolné metody C#v, je nutné přidat `()` znaků za metodou.) Dokončený kód pro metodu `GetHtml` vypadá jako v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="427d2-168">(As with any method in C#, you must add `()` characters after the method.) The completed code for the `GetHtml` method looks like the following example:</span></span>

    [!code-cshtml[Main](program-asp-net-web-pages-in-visual-studio/samples/sample1.cshtml)]
4. <span data-ttu-id="427d2-169">Stisknutím kombinace kláves CTRL + F5 stránku spusťte.</span><span class="sxs-lookup"><span data-stu-id="427d2-169">Press Ctrl+F5 to run the page.</span></span> <span data-ttu-id="427d2-170">Tato stránka vypadá jako při zobrazení v prohlížeči:</span><span class="sxs-lookup"><span data-stu-id="427d2-170">This is what the page looks like when displayed in a browser:</span></span>

    ![Výchozí stránka v prohlížeči](program-asp-net-web-pages-in-visual-studio/_static/image5.png)
5. <span data-ttu-id="427d2-172">Zavřete prohlížeč.</span><span class="sxs-lookup"><span data-stu-id="427d2-172">Close the browser.</span></span>

### <a name="using-the-debugger"></a><span data-ttu-id="427d2-173">Použití ladicího programu</span><span class="sxs-lookup"><span data-stu-id="427d2-173">Using the Debugger</span></span>

1. <span data-ttu-id="427d2-174">V horní části stránky *Default. cshtml* za řádek, který začíná na `Page.Title`, přidejte následující řádek kódu:</span><span class="sxs-lookup"><span data-stu-id="427d2-174">At the top of the *Default.cshtml* page, after the line that begins with `Page.Title`, add the following line of code:</span></span>

    [!code-csharp[Main](program-asp-net-web-pages-in-visual-studio/samples/sample2.cs)]
2. <span data-ttu-id="427d2-175">V levém okraji editoru nalevo od kódu klikněte na tlačítko Další na tento nový řádek, aby bylo možné přidat *zarážku*.</span><span class="sxs-lookup"><span data-stu-id="427d2-175">In the gray margin of the editor to the left of the code, click next to this new line in order to add a *breakpoint*.</span></span> <span data-ttu-id="427d2-176">Zarážka je značka, která instruuje ladicí program, aby zastavil běh programu v tomto okamžiku, abyste viděli, co se děje.</span><span class="sxs-lookup"><span data-stu-id="427d2-176">A breakpoint is a marker that tells the debugger to stop running the program at that point so you can see what's happening.</span></span>

    ![Nastavit zarážku](program-asp-net-web-pages-in-visual-studio/_static/image6.png)
3. <span data-ttu-id="427d2-178">Odeberte volání metody `ServerInfo.GetHtml` a přidejte volání `@myTime` proměnné na svém místě.</span><span class="sxs-lookup"><span data-stu-id="427d2-178">Remove the call to the `ServerInfo.GetHtml` method, and add a call to the `@myTime` variable in its place.</span></span> <span data-ttu-id="427d2-179">Toto volání zobrazí aktuální časovou hodnotu, která je vrácena novým řádkem kódu.</span><span class="sxs-lookup"><span data-stu-id="427d2-179">This call displays the current time value that's returned by the new line of code.</span></span>
4. <span data-ttu-id="427d2-180">Stiskněte klávesu F5 ke spuštění stránky v ladicím programu.</span><span class="sxs-lookup"><span data-stu-id="427d2-180">Press F5 to run the page in the debugger.</span></span> <span data-ttu-id="427d2-181">Stránka se zastaví na zarážce, kterou jste nastavili.</span><span class="sxs-lookup"><span data-stu-id="427d2-181">The page stops on the breakpoint that you set.</span></span> <span data-ttu-id="427d2-182">Následující obrázek ukazuje, jak stránka vypadá v editoru se zarážkou (žlutě).</span><span class="sxs-lookup"><span data-stu-id="427d2-182">The following image shows what the page looks like in the editor with the breakpoint (in yellow).</span></span>

    ![ladit zarážku](program-asp-net-web-pages-in-visual-studio/_static/image7.png)
5. <span data-ttu-id="427d2-184">Na panelu nástrojů ladění kliknutím na tlačítko **Krok do** (nebo stisknutím klávesy F11) spusťte další řádek kódu.</span><span class="sxs-lookup"><span data-stu-id="427d2-184">In the Debug toolbar, click the **Step Into** button (or press F11) to run the next line of code.</span></span> <span data-ttu-id="427d2-185">Pokaždé, když kliknete na toto tlačítko, budete pokračovat v provádění na další řádek kódu.</span><span class="sxs-lookup"><span data-stu-id="427d2-185">Each time you click this button, you advance the execution to the next line of code.</span></span>

    ![Krok do – tlačítko](program-asp-net-web-pages-in-visual-studio/_static/image8.png)
6. <span data-ttu-id="427d2-187">Prozkoumejte hodnotu proměnné `myTime` tím, že podržíte ukazatel myši nad ní nebo zkontrolujete hodnoty zobrazené v oknech **místní** hodnoty a **zásobník volání** .</span><span class="sxs-lookup"><span data-stu-id="427d2-187">Examine the value of the `myTime` variable by holding your mouse pointer over it or by inspecting the values displayed in the **Locals** and **Call Stack** windows.</span></span> <span data-ttu-id="427d2-188">Visual Studio zobrazí hodnotu proměnné.</span><span class="sxs-lookup"><span data-stu-id="427d2-188">Visual Studio display the value of the variable.</span></span>

    ![Zobrazit časovou hodnotu](program-asp-net-web-pages-in-visual-studio/_static/image9.png)
7. <span data-ttu-id="427d2-190">Po kontrole proměnné a krokování prostřednictvím kódu stiskněte klávesu F5 pro pokračování ve spouštění stránky bez zastavení na každém řádku.</span><span class="sxs-lookup"><span data-stu-id="427d2-190">When you're done examining the variable and stepping through code, press F5 to continue running the page without stopping at each line.</span></span> <span data-ttu-id="427d2-191">Až dokončíte krokování se všemi kódy, prohlížeč zobrazí stránku.</span><span class="sxs-lookup"><span data-stu-id="427d2-191">When you've finished stepping through all the code, the browser displays the page.</span></span>

<span data-ttu-id="427d2-192">Další informace o ladicím programu a o tom, jak ladit kód v aplikaci Visual Studio, naleznete v tématu [Návod: ladění webových stránek ve Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span><span class="sxs-lookup"><span data-stu-id="427d2-192">To learn more about the debugger and about how to debug code in Visual Studio, see [Walkthrough: Debugging Web Pages in Visual Web Developer](https://msdn.microsoft.com/library/z9e7w6cs.aspx).</span></span>

## <a name="using-razor-in-aspnet-mvc-projects-with-visual-studio"></a><span data-ttu-id="427d2-193">Použití Razor v projektech ASP.NET MVC se sadou Visual Studio</span><span class="sxs-lookup"><span data-stu-id="427d2-193">Using Razor in ASP.NET MVC projects with Visual Studio</span></span>

<span data-ttu-id="427d2-194">Syntaxe Razor se také v projektech ASP.NET MVC používá rozsáhle.</span><span class="sxs-lookup"><span data-stu-id="427d2-194">The Razor syntax is also used extensively in ASP.NET MVC projects.</span></span> <span data-ttu-id="427d2-195">MVC je výkonný model založený na vzorcích, který slouží k vytváření dynamických webů.</span><span class="sxs-lookup"><span data-stu-id="427d2-195">MVC is a powerful, patterns-based way to build dynamic websites.</span></span> <span data-ttu-id="427d2-196">Pokud bude web webových stránek ASP.NET obtížné udržovat, můžete zvážit jeho převod na aplikaci ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="427d2-196">If your ASP.NET Web Pages site becomes difficult to maintain, you might want to consider converting it to an ASP.NET MVC application.</span></span> <span data-ttu-id="427d2-197">Příklad vytvoření aplikace MVC najdete v tématu [Začínáme s ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="427d2-197">For an example of creating an MVC application, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<a id="vs2010support"></a>
## <a name="installing-support-for-aspnet-web-pages-in-visual-studio-2010"></a><span data-ttu-id="427d2-198">Instalace podpory pro webové stránky ASP.NET v aplikaci Visual Studio 2010</span><span class="sxs-lookup"><span data-stu-id="427d2-198">Installing Support for ASP.NET Web Pages in Visual Studio 2010</span></span>

<span data-ttu-id="427d2-199">V této části se dozvíte, jak nainstalovat Visual Web Developer Express 2010 a nástroje ASP.NET Web Pages pro Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="427d2-199">This section shows how to install Visual Web Developer Express 2010 and the ASP.NET Web Pages Tools for Visual Studio.</span></span>

1. <span data-ttu-id="427d2-200">Pokud ještě nemáte instalační program webové platformy, Stáhněte si ho z následující adresy URL:</span><span class="sxs-lookup"><span data-stu-id="427d2-200">If you don't already have the Web Platform Installer, download it from the following URL:</span></span>

    [https://www.microsoft.com/web/downloads/platform.aspx](https://www.microsoft.com/web/downloads/platform.aspx)
2. <span data-ttu-id="427d2-201">Spusťte instalační program webové platformy.</span><span class="sxs-lookup"><span data-stu-id="427d2-201">Run the Web Platform Installer.</span></span>
3. <span data-ttu-id="427d2-202">Klikněte na kartu **produkty** .</span><span class="sxs-lookup"><span data-stu-id="427d2-202">Click the **Products** tab.</span></span>

    ![Karta produkty WebPI](program-asp-net-web-pages-in-visual-studio/_static/image10.png)
4. <span data-ttu-id="427d2-204">Vyhledejte **ASP.NET MVC 4** (pro webové stránky ASP.NET 2) a pak klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="427d2-204">Search for **ASP.NET MVC 4** (for ASP.NET Web Pages 2) and then click **Add**.</span></span> <span data-ttu-id="427d2-205">Mezi tyto produkty patří nástroje sady Visual Studio pro vytváření webů ASP.NET Razor.</span><span class="sxs-lookup"><span data-stu-id="427d2-205">These products include Visual Studio tools for building ASP.NET Razor websites.</span></span>

    ![Možnosti instalace WebPi](program-asp-net-web-pages-in-visual-studio/_static/image11.png)
5. <span data-ttu-id="427d2-207">Instalaci dokončíte kliknutím na **instalovat** .</span><span class="sxs-lookup"><span data-stu-id="427d2-207">Click **Install** to complete the installation.</span></span>

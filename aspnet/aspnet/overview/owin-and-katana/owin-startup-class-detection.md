---
uid: aspnet/overview/owin-and-katana/owin-startup-class-detection
title: Detekce spouštěcí třídy OWIN | Microsoft Docs
author: Praburaj
description: V tomto kurzu se dozvíte, jak nakonfigurovat, kterou spouštěcí třídu OWIN je načtená. Další informace o OWIN najdete v tématu Přehled projektu Katana. Tento kurz byl...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 08257f55-36f4-4e39-9c88-2a5602838c79
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-startup-class-detection
msc.type: authoredcontent
ms.openlocfilehash: e1670c32049ec33dd4d1941a091a429d3929c452
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617045"
---
# <a name="owin-startup-class-detection"></a><span data-ttu-id="bb687-105">Rozpoznání spouštěcí třídy OWIN</span><span class="sxs-lookup"><span data-stu-id="bb687-105">OWIN Startup Class Detection</span></span>

> <span data-ttu-id="bb687-106">V tomto kurzu se dozvíte, jak nakonfigurovat, kterou spouštěcí třídu OWIN je načtená.</span><span class="sxs-lookup"><span data-stu-id="bb687-106">This tutorial shows how to configure which OWIN startup class is loaded.</span></span> <span data-ttu-id="bb687-107">Další informace o OWIN najdete v tématu [Přehled projektu Katana](an-overview-of-project-katana.md).</span><span class="sxs-lookup"><span data-stu-id="bb687-107">For more information on OWIN, see [An Overview of Project Katana](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="bb687-108">Tento kurz napsal Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), Praburaj Thiagarajan a Howard Dierking ( [@howard\_Dierking](https://twitter.com/howard_dierking) ).</span><span class="sxs-lookup"><span data-stu-id="bb687-108">This tutorial was written by Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), Praburaj Thiagarajan, and Howard Dierking ( [@howard\_dierking](https://twitter.com/howard_dierking) ).</span></span>
>
> ## <a name="prerequisites"></a><span data-ttu-id="bb687-109">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="bb687-109">Prerequisites</span></span>
>
> [<span data-ttu-id="bb687-110">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="bb687-110">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)

## <a name="owin-startup-class-detection"></a><span data-ttu-id="bb687-111">Rozpoznání spouštěcí třídy OWIN</span><span class="sxs-lookup"><span data-stu-id="bb687-111">OWIN Startup Class Detection</span></span>

 <span data-ttu-id="bb687-112">Každá aplikace OWIN má spouštěcí třídu, kde zadáte komponenty pro kanál aplikace.</span><span class="sxs-lookup"><span data-stu-id="bb687-112">Every OWIN Application has a startup class where you specify components for the application pipeline.</span></span> <span data-ttu-id="bb687-113">Existují různé způsoby, jak můžete připojit třídu spuštění s modulem runtime v závislosti na zvoleném modelu hostování (OwinHost, IIS a IIS-Express).</span><span class="sxs-lookup"><span data-stu-id="bb687-113">There are different ways you can connect your startup class with the runtime, depending on the hosting model you choose (OwinHost, IIS, and IIS-Express).</span></span> <span data-ttu-id="bb687-114">Spouštěcí třída uvedená v tomto kurzu se dá použít v každé hostující aplikaci.</span><span class="sxs-lookup"><span data-stu-id="bb687-114">The startup class shown in this tutorial can be used in every hosting application.</span></span> <span data-ttu-id="bb687-115">Pomocí jednoho z těchto přístupů připojíte spouštěcí třídu k hostujícímu modulu runtime:</span><span class="sxs-lookup"><span data-stu-id="bb687-115">You connect the startup class with the hosting runtime using one of the these approaches:</span></span>

1. <span data-ttu-id="bb687-116">**Konvence pojmenování**: Katana vyhledá třídu s názvem `Startup` v oboru názvů, která odpovídá názvu sestavení nebo globálnímu oboru názvů.</span><span class="sxs-lookup"><span data-stu-id="bb687-116">**Naming Convention**: Katana looks for a class named `Startup` in namespace matching the assembly name or the global namespace.</span></span>
2. <span data-ttu-id="bb687-117">**OwinStartup atribut**: Jedná se o přístup většiny vývojářů, kteří budou muset zadat třídu pro spuštění.</span><span class="sxs-lookup"><span data-stu-id="bb687-117">**OwinStartup Attribute**: This is the approach most developers will take to specify the startup class.</span></span> <span data-ttu-id="bb687-118">Následující atribut nastaví spouštěcí třídu na třídu `TestStartup` v oboru názvů `StartupDemo`.</span><span class="sxs-lookup"><span data-stu-id="bb687-118">The following attribute will set the startup class to the `TestStartup` class in the `StartupDemo` namespace.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample1.cs)]

   <span data-ttu-id="bb687-119">Atribut `OwinStartup` Přepisuje konvence pojmenování.</span><span class="sxs-lookup"><span data-stu-id="bb687-119">The `OwinStartup` attribute overrides the naming convention.</span></span> <span data-ttu-id="bb687-120">Můžete také zadat popisný název s tímto atributem, ale použití popisného názvu vyžaduje, abyste také používali `appSetting` prvek v konfiguračním souboru.</span><span class="sxs-lookup"><span data-stu-id="bb687-120">You can also specify a friendly name with this attribute, however, using a friendly name requires you to also use the `appSetting` element in the configuration file.</span></span>
3. <span data-ttu-id="bb687-121">**Element appSetting v konfiguračním souboru**: element `appSetting` přepisuje atribut `OwinStartup` a konvence pojmenování.</span><span class="sxs-lookup"><span data-stu-id="bb687-121">**The appSetting element in the Configuration file**: The `appSetting` element overrides the `OwinStartup` attribute and naming convention.</span></span> <span data-ttu-id="bb687-122">Můžete mít více spouštěcích tříd (každý pomocí atributu `OwinStartup`) a nakonfigurovat, která spouštěcí třída bude načtena do konfiguračního souboru pomocí kódu, který je podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="bb687-122">You can have multiple startup classes (each using an `OwinStartup` attribute) and configure which startup class will be loaded in a configuration file using markup similar to the following:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample2.xml)]

   <span data-ttu-id="bb687-123">Následující klíč, který explicitně specifikuje spouštěcí třídu a sestavení lze také použít:</span><span class="sxs-lookup"><span data-stu-id="bb687-123">The following key, which explicitly specifies the startup class and assembly can also be used:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample3.xml)]

   <span data-ttu-id="bb687-124">Následující kód XML v konfiguračním souboru Určuje popisný název spouštěcí třídy `ProductionConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="bb687-124">The following XML in the configuration file specifies a friendly startup class name of `ProductionConfiguration`.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample4.xml)]

   <span data-ttu-id="bb687-125">Výše uvedený kód musí být použit s následujícím atributem `OwinStartup`, který určuje popisný název a způsobuje, že se třída `ProductionStartup2` spustí.</span><span class="sxs-lookup"><span data-stu-id="bb687-125">The above markup must be used with the following `OwinStartup` attribute which specifies a friendly name and causes the `ProductionStartup2` class to run.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample5.cs?highlight=1,16)]
4. <span data-ttu-id="bb687-126">Chcete-li zakázat zjišťování spouštění OWIN, přidejte `appSetting owin:AutomaticAppStartup` s hodnotou `"false"` v souboru Web. config.</span><span class="sxs-lookup"><span data-stu-id="bb687-126">To disable OWIN startup discovery add the `appSetting owin:AutomaticAppStartup` with a value of `"false"` in the web.config file.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample6.xml)]

## <a name="create-an-aspnet-web-app-using-owin-startup"></a><span data-ttu-id="bb687-127">Vytvoření webové aplikace v ASP.NET pomocí spuštění OWIN</span><span class="sxs-lookup"><span data-stu-id="bb687-127">Create an ASP.NET Web App using OWIN Startup</span></span>

1. <span data-ttu-id="bb687-128">Vytvořte prázdnou webovou aplikaci v Asp.Net a pojmenujte ji **StartupDemo**.</span><span class="sxs-lookup"><span data-stu-id="bb687-128">Create an empty Asp.Net web application and name it **StartupDemo**.</span></span> <span data-ttu-id="bb687-129">– Nainstalujte `Microsoft.Owin.Host.SystemWeb` pomocí Správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="bb687-129">- Install `Microsoft.Owin.Host.SystemWeb` using the NuGet package manager.</span></span> <span data-ttu-id="bb687-130">V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak klikněte na **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="bb687-130">From the **Tools** menu, select **NuGet Package Manager**, and then **Package Manager Console**.</span></span> <span data-ttu-id="bb687-131">Zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="bb687-131">Enter the following command:</span></span>

    [!code-powershell[Main](owin-startup-class-detection/samples/sample7.ps1)]
2. <span data-ttu-id="bb687-132">Přidejte třídu pro spuštění OWIN.</span><span class="sxs-lookup"><span data-stu-id="bb687-132">Add an OWIN startup class.</span></span> <span data-ttu-id="bb687-133">V aplikaci Visual Studio 2017 klikněte pravým tlačítkem myši na projekt a vyberte možnost **Přidat třídu**.-v dialogovém okně **Přidat novou položku** zadejte do vyhledávacího pole *OWIN* a změňte název na Startup.cs a pak vyberte **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="bb687-133">In Visual Studio 2017 right-click the project and select **Add Class**.- In the **Add New Item** dialog box, enter *OWIN* in the search field, and change the name to Startup.cs, and then select **Add**.</span></span>

     ![](owin-startup-class-detection/_static/image1.png)

   <span data-ttu-id="bb687-134">Až příště budete chtít přidat *třídu pro spuštění Owin*, bude dostupná z nabídky **Přidat** .</span><span class="sxs-lookup"><span data-stu-id="bb687-134">The next time you want to add an *Owin Startup class*, it will be in available from the **Add** menu.</span></span>

     ![](owin-startup-class-detection/_static/image2.png)

   <span data-ttu-id="bb687-135">Případně můžete kliknout pravým tlačítkem myši na projekt a vybrat možnost **Přidat**, vybrat **položku Nová položka**a vybrat třídu pro **spuštění Owin**.</span><span class="sxs-lookup"><span data-stu-id="bb687-135">Alternatively, you can right-click the project and select **Add**, then select **New Item**, and then select the **Owin Startup class**.</span></span>

     ![](owin-startup-class-detection/_static/image3.png)

- <span data-ttu-id="bb687-136">Vygenerovaný kód nahraďte v souboru *Startup.cs* následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="bb687-136">Replace the generated code in the *Startup.cs* file with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample8.cs?highlight=5,7,15-28,31-34)]

  <span data-ttu-id="bb687-137">Výraz lambda `app.Use` slouží k registraci zadané komponenty middlewaru do kanálu OWIN.</span><span class="sxs-lookup"><span data-stu-id="bb687-137">The `app.Use` lambda expression is used to register the specified middleware component to the OWIN pipeline.</span></span> <span data-ttu-id="bb687-138">V tomto případě nastavujeme protokolování příchozích požadavků před reakcí na příchozí požadavek.</span><span class="sxs-lookup"><span data-stu-id="bb687-138">In this case we are setting up logging of incoming requests before responding to the incoming request.</span></span> <span data-ttu-id="bb687-139">Parametr `next` je delegát ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt; [Task](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx) &gt;) k další komponentě v kanálu.</span><span class="sxs-lookup"><span data-stu-id="bb687-139">The `next` parameter is the delegate ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt; [Task](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx) &gt; ) to the next component in the pipeline.</span></span> <span data-ttu-id="bb687-140">Výraz lambda `app.Run` zapojování kanálu na příchozí požadavky a poskytuje mechanismus odezvy.</span><span class="sxs-lookup"><span data-stu-id="bb687-140">The `app.Run` lambda expression hooks up the pipeline to incoming requests and provides the response mechanism.</span></span>
     > [!NOTE]
     > <span data-ttu-id="bb687-141">V kódu výše jsme zavedli komentář k atributu `OwinStartup` a budeme se spoléhat na konvenci spuštění třídy s názvem `Startup`.-Stisknutím klávesy ***F5*** spusťte aplikaci.</span><span class="sxs-lookup"><span data-stu-id="bb687-141">In the code above we have commented out the `OwinStartup` attribute and we're relying on the convention of running the class named `Startup` .- Press ***F5*** to run the application.</span></span> <span data-ttu-id="bb687-142">Stiskněte několikrát aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="bb687-142">Hit refresh a few times.</span></span>

    <span data-ttu-id="bb687-143">![](owin-startup-class-detection/_static/image4.png) Poznámka: číslo zobrazené na obrázcích v tomto kurzu se neshoduje s číslem, které vidíte.</span><span class="sxs-lookup"><span data-stu-id="bb687-143">![](owin-startup-class-detection/_static/image4.png) Note: The number shown in the images in this tutorial will not match the number you see.</span></span> <span data-ttu-id="bb687-144">Řetězec milisekund se používá k zobrazení nové odpovědi při aktualizaci stránky.</span><span class="sxs-lookup"><span data-stu-id="bb687-144">The millisecond string is used to show a new response when you refresh the page.</span></span>
  <span data-ttu-id="bb687-145">Trasovací informace můžete zobrazit v okně **výstup** .</span><span class="sxs-lookup"><span data-stu-id="bb687-145">You can see the trace information in the **Output** window.</span></span>

    ![](owin-startup-class-detection/_static/image5.png)

## <a name="add-more-startup-classes"></a><span data-ttu-id="bb687-146">Přidat další třídy po spuštění</span><span class="sxs-lookup"><span data-stu-id="bb687-146">Add More Startup Classes</span></span>

<span data-ttu-id="bb687-147">V této části přidáme další spouštěcí třídu.</span><span class="sxs-lookup"><span data-stu-id="bb687-147">In this section we'll add another Startup class.</span></span> <span data-ttu-id="bb687-148">Do své aplikace můžete přidat více tříd OWIN Startup.</span><span class="sxs-lookup"><span data-stu-id="bb687-148">You can add multiple OWIN startup class to your application.</span></span> <span data-ttu-id="bb687-149">Můžete například chtít vytvořit třídy po spuštění pro vývoj, testování a produkci.</span><span class="sxs-lookup"><span data-stu-id="bb687-149">For example, you might want to create startup classes for development, testing and production.</span></span>

1. <span data-ttu-id="bb687-150">Vytvořte novou třídu OWIN Startup a pojmenujte ji `ProductionStartup`.</span><span class="sxs-lookup"><span data-stu-id="bb687-150">Create a new OWIN Startup class and name it `ProductionStartup`.</span></span>
2. <span data-ttu-id="bb687-151">Vygenerovaný kód nahraďte následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="bb687-151">Replace the generated code with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample9.cs?highlight=14-18)]
3. <span data-ttu-id="bb687-152">Aplikaci spustíte stisknutím klávesy Control F5.</span><span class="sxs-lookup"><span data-stu-id="bb687-152">Press Control F5 to run the app.</span></span> <span data-ttu-id="bb687-153">Atribut `OwinStartup` určuje, že se spouští spouštěcí třída výroby.</span><span class="sxs-lookup"><span data-stu-id="bb687-153">The `OwinStartup` attribute specifies the production startup class is run.</span></span>

    ![](owin-startup-class-detection/_static/image6.png)
4. <span data-ttu-id="bb687-154">Vytvořte další třídu OWIN Startup a pojmenujte ji `TestStartup`.</span><span class="sxs-lookup"><span data-stu-id="bb687-154">Create another OWIN Startup class and name it `TestStartup`.</span></span>
5. <span data-ttu-id="bb687-155">Vygenerovaný kód nahraďte následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="bb687-155">Replace the generated code with the following:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample10.cs?highlight=6,14-18)]

   <span data-ttu-id="bb687-156">Přetížení atributu `OwinStartup` výše určuje `TestingConfiguration` jako *popisný* název třídy po spuštění.</span><span class="sxs-lookup"><span data-stu-id="bb687-156">The `OwinStartup` attribute overload above specifies `TestingConfiguration` as the *friendly* name of the Startup class.</span></span>
6. <span data-ttu-id="bb687-157">Otevřete soubor *Web. config* a přidejte spouštěcí klíč aplikace Owin, který určuje popisný název třídy po spuštění:</span><span class="sxs-lookup"><span data-stu-id="bb687-157">Open the *web.config* file and add the OWIN App startup key which specifies the friendly name of the Startup class:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample11.xml?highlight=3-5)]
7. <span data-ttu-id="bb687-158">Aplikaci spustíte stisknutím klávesy Control F5.</span><span class="sxs-lookup"><span data-stu-id="bb687-158">Press Control F5 to run the app.</span></span> <span data-ttu-id="bb687-159">Prvek nastavení aplikace má stejný předchůdce a je spuštěna konfigurace testu.</span><span class="sxs-lookup"><span data-stu-id="bb687-159">The app settings element takes precedent, and the test configuration is run.</span></span>

    ![](owin-startup-class-detection/_static/image7.png)
8. <span data-ttu-id="bb687-160">Odeberte *popisný* název z atributu `OwinStartup` ve třídě `TestStartup`.</span><span class="sxs-lookup"><span data-stu-id="bb687-160">Remove the *friendly* name from the `OwinStartup` attribute in the `TestStartup` class.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample12.cs)]
9. <span data-ttu-id="bb687-161">Nahraďte spouštěcí klíč aplikace OWIN v souboru *Web. config* následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="bb687-161">Replace the OWIN App startup key in the *web.config* file with the following:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample13.xml)]
10. <span data-ttu-id="bb687-162">Vrátit atribut `OwinStartup` v každé třídě na kód výchozího atributu generovaný aplikací Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="bb687-162">Revert the `OwinStartup` attribute in each class to the default attribute code generated by Visual Studio:</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample14.cs)]

    <span data-ttu-id="bb687-163">Každý z následujících spouštěcích klíčů aplikace OWIN způsobí spuštění produkční třídy.</span><span class="sxs-lookup"><span data-stu-id="bb687-163">Each of the OWIN App startup keys below will cause the production class to run.</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample15.xml)]

    <span data-ttu-id="bb687-164">Poslední spouštěcí klíč určuje metodu konfigurace spuštění.</span><span class="sxs-lookup"><span data-stu-id="bb687-164">The last startup key specifies the startup configuration method.</span></span> <span data-ttu-id="bb687-165">Následující spouštěcí klíč aplikace OWIN umožňuje změnit název třídy konfigurace na `MyConfiguration`.</span><span class="sxs-lookup"><span data-stu-id="bb687-165">The following OWIN App startup key allows you to change the name of the configuration class to `MyConfiguration` .</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample16.xml)]

## <a name="using-owinhostexe"></a><span data-ttu-id="bb687-166">Použití Owinhost. exe</span><span class="sxs-lookup"><span data-stu-id="bb687-166">Using Owinhost.exe</span></span>

1. <span data-ttu-id="bb687-167">Soubor Web. config nahraďte následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="bb687-167">Replace the Web.config file with the following markup:</span></span>

    [!code-xml[Main](owin-startup-class-detection/samples/sample17.xml?highlight=3-6)]

   <span data-ttu-id="bb687-168">Poslední klíč služby WINS, takže v tomto případě je `TestStartup` zadán.</span><span class="sxs-lookup"><span data-stu-id="bb687-168">The last key wins, so in this case `TestStartup` is specified.</span></span>
2. <span data-ttu-id="bb687-169">Nainstalujte Owinhost z PMC:</span><span class="sxs-lookup"><span data-stu-id="bb687-169">Install Owinhost from the PMC:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample18.cmd)]
3. <span data-ttu-id="bb687-170">Přejděte do složky aplikace (do složky obsahující soubor *Web. config* ) a do příkazového řádku zadejte:</span><span class="sxs-lookup"><span data-stu-id="bb687-170">Navigate to the application folder (the folder containing the *Web.config* file) and in a command prompt and type:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample19.cmd)]

   <span data-ttu-id="bb687-171">Zobrazí se okno příkazového řádku:</span><span class="sxs-lookup"><span data-stu-id="bb687-171">The command window will show:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample20.cmd)]
4. <span data-ttu-id="bb687-172">Spusťte prohlížeč s `http://localhost:5000/`URL.</span><span class="sxs-lookup"><span data-stu-id="bb687-172">Launch a browser with the URL `http://localhost:5000/`.</span></span>

    ![](owin-startup-class-detection/_static/image8.png)

   <span data-ttu-id="bb687-173">OwinHost respektují konvence při spuštění uvedené výše.</span><span class="sxs-lookup"><span data-stu-id="bb687-173">OwinHost honored the startup conventions listed above.</span></span>
5. <span data-ttu-id="bb687-174">V příkazovém okně ukončete OwinHost stisknutím klávesy ENTER.</span><span class="sxs-lookup"><span data-stu-id="bb687-174">In the command window, press Enter to exit OwinHost.</span></span>
6. <span data-ttu-id="bb687-175">Ve třídě `ProductionStartup` přidejte následující atribut OwinStartup, který určuje popisný název *ProductionConfiguration*.</span><span class="sxs-lookup"><span data-stu-id="bb687-175">In the `ProductionStartup` class, add the following OwinStartup attribute which specifies a friendly name of *ProductionConfiguration*.</span></span>

    [!code-csharp[Main](owin-startup-class-detection/samples/sample21.cs)]
7. <span data-ttu-id="bb687-176">Do příkazového řádku zadejte:</span><span class="sxs-lookup"><span data-stu-id="bb687-176">In the command prompt and type:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample22.cmd)]

   <span data-ttu-id="bb687-177">Je načtena produkční spouštěcí třída.</span><span class="sxs-lookup"><span data-stu-id="bb687-177">The Production startup class is loaded.</span></span>
    ![](owin-startup-class-detection/_static/image9.png)

   <span data-ttu-id="bb687-178">Naše aplikace má více tříd po spuštění a v tomto příkladu jsme odvodili, která spouštěcí třída se načte až do doby běhu.</span><span class="sxs-lookup"><span data-stu-id="bb687-178">Our application has multiple startup classes, and in this example we have deferred which startup class to load until runtime.</span></span>
8. <span data-ttu-id="bb687-179">Otestujte následující možnosti spuštění modulu runtime:</span><span class="sxs-lookup"><span data-stu-id="bb687-179">Test the following runtime startup options:</span></span>

    [!code-console[Main](owin-startup-class-detection/samples/sample23.cmd)]

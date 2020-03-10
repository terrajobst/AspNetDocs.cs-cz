---
uid: web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
title: Trasování ve webovém rozhraní API 2 pro ASP.NET | Microsoft Docs
author: MikeWasson
description: Ukazuje, jak povolit trasování v ASP.NET webovém rozhraní API.
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 66a837e9-600b-4b72-97a9-19804231c64a
msc.legacyurl: /web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: a01acb649556d06ab9828ceab0fcbdf363bbc0d1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598551"
---
# <a name="tracing-in-aspnet-web-api-2"></a><span data-ttu-id="6a190-103">Trasování ve webovém rozhraní API 2 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="6a190-103">Tracing in ASP.NET Web API 2</span></span>

<span data-ttu-id="6a190-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6a190-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="6a190-105">Při pokusu o ladění webové aplikace nenahrazujete správnou sadu protokolů trasování.</span><span class="sxs-lookup"><span data-stu-id="6a190-105">When you are trying to debug a web-based application, there is no substitute for a good set of trace logs.</span></span> <span data-ttu-id="6a190-106">V tomto kurzu se dozvíte, jak povolit trasování v ASP.NET webovém rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="6a190-106">This tutorial shows how to enable tracing in ASP.NET Web API.</span></span> <span data-ttu-id="6a190-107">Pomocí této funkce můžete sledovat, co rozhraní Web API funguje před a poté, co vyvolá kontroler.</span><span class="sxs-lookup"><span data-stu-id="6a190-107">You can use this feature to trace what the Web API framework does before and after it invokes your controller.</span></span> <span data-ttu-id="6a190-108">Můžete ho také použít k trasování vlastního kódu.</span><span class="sxs-lookup"><span data-stu-id="6a190-108">You can also use it to trace your own code.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="6a190-109">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="6a190-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="6a190-110">[Visual studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (také funguje se sadou visual Studio 2015)</span><span class="sxs-lookup"><span data-stu-id="6a190-110">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (also works with Visual Studio 2015)</span></span>
> - <span data-ttu-id="6a190-111">Webové rozhraní API 2</span><span class="sxs-lookup"><span data-stu-id="6a190-111">Web API 2</span></span>
> - [<span data-ttu-id="6a190-112">Microsoft. AspNet. WebApi. Tracing</span><span class="sxs-lookup"><span data-stu-id="6a190-112">Microsoft.AspNet.WebApi.Tracing</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)

## <a name="enable-systemdiagnostics-tracing-in-web-api"></a><span data-ttu-id="6a190-113">Povolit trasování System. Diagnostics ve webovém rozhraní API</span><span class="sxs-lookup"><span data-stu-id="6a190-113">Enable System.Diagnostics Tracing in Web API</span></span>

<span data-ttu-id="6a190-114">Nejprve vytvoříme nový projekt webové aplikace ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="6a190-114">First, we'll create a new ASP.NET Web Application project.</span></span> <span data-ttu-id="6a190-115">V aplikaci Visual Studio v nabídce **soubor** vyberte **Nový** > **projekt**.</span><span class="sxs-lookup"><span data-stu-id="6a190-115">In Visual Studio, from the **File** menu, select **New** > **Project**.</span></span> <span data-ttu-id="6a190-116">V části **šablony**, **Web**vyberte **ASP.NET webová aplikace**.</span><span class="sxs-lookup"><span data-stu-id="6a190-116">Under **Templates**, **Web**, select **ASP.NET Web Application**.</span></span>

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="6a190-117">Vyberte šablonu projektu webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="6a190-117">Choose the Web API project template.</span></span>

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

<span data-ttu-id="6a190-118">V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak **balíček spravovat konzolu**.</span><span class="sxs-lookup"><span data-stu-id="6a190-118">From the **Tools** menu, select **NuGet Package Manager**, then **Package Manage Console**.</span></span>

<span data-ttu-id="6a190-119">V okně konzoly Správce balíčků zadejte následující příkazy.</span><span class="sxs-lookup"><span data-stu-id="6a190-119">In the Package Manager Console window, type the following commands.</span></span>

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

<span data-ttu-id="6a190-120">První příkaz nainstaluje nejnovější balíček trasování webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="6a190-120">The first command installs the latest Web API tracing package.</span></span> <span data-ttu-id="6a190-121">Také aktualizuje základní balíčky webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="6a190-121">It also updates the core Web API packages.</span></span> <span data-ttu-id="6a190-122">Druhý příkaz aktualizuje balíček WebApi. webhost na nejnovější verzi.</span><span class="sxs-lookup"><span data-stu-id="6a190-122">The second command updates the WebApi.WebHost package to the latest version.</span></span>

> [!NOTE]
> <span data-ttu-id="6a190-123">Pokud chcete cílit na konkrétní verzi webového rozhraní API, použijte příznak-Version při instalaci balíčku trasování.</span><span class="sxs-lookup"><span data-stu-id="6a190-123">If you want to target a specific version of Web API, use the -Version flag when you install the tracing package.</span></span>

<span data-ttu-id="6a190-124">Otevřete soubor WebApiConfig.cs ve složce App\_Start.</span><span class="sxs-lookup"><span data-stu-id="6a190-124">Open the file WebApiConfig.cs in the App\_Start folder.</span></span> <span data-ttu-id="6a190-125">Do metody **Register** přidejte následující kód.</span><span class="sxs-lookup"><span data-stu-id="6a190-125">Add the following code to the **Register** method.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

<span data-ttu-id="6a190-126">Tento kód přidá do kanálu webového rozhraní API třídu [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) .</span><span class="sxs-lookup"><span data-stu-id="6a190-126">This code adds the [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) class to the Web API pipeline.</span></span> <span data-ttu-id="6a190-127">Třída **SystemDiagnosticsTraceWriter** zapisuje trasování do [System. Diagnostics. Trace](https://msdn.microsoft.com/library/system.diagnostics.trace).</span><span class="sxs-lookup"><span data-stu-id="6a190-127">The **SystemDiagnosticsTraceWriter** class writes traces to [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace).</span></span>

<span data-ttu-id="6a190-128">Chcete-li zobrazit trasování, spusťte aplikaci v ladicím programu.</span><span class="sxs-lookup"><span data-stu-id="6a190-128">To see the traces, run the application in the debugger.</span></span> <span data-ttu-id="6a190-129">V prohlížeči přejděte na adresu `/api/values`.</span><span class="sxs-lookup"><span data-stu-id="6a190-129">In the browser, navigate to `/api/values`.</span></span>

![](tracing-in-aspnet-web-api/_static/image5.png)

<span data-ttu-id="6a190-130">Příkazy trasování jsou zapsány do okna výstup v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6a190-130">The trace statements are written to the Output window in Visual Studio.</span></span> <span data-ttu-id="6a190-131">(V nabídce **zobrazení** vyberte **výstup**).</span><span class="sxs-lookup"><span data-stu-id="6a190-131">(From the **View** menu, select **Output**).</span></span>

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

<span data-ttu-id="6a190-132">Vzhledem k tomu, že **SystemDiagnosticsTraceWriter** zapisuje trasování do **System. Diagnostics. Trace**, můžete registrovat další naslouchací procesy trasování; například pro zápis trasování do souboru protokolu.</span><span class="sxs-lookup"><span data-stu-id="6a190-132">Because **SystemDiagnosticsTraceWriter** writes traces to **System.Diagnostics.Trace**, you can register additional trace listeners; for example, to write traces to a log file.</span></span> <span data-ttu-id="6a190-133">Další informace o zapisovačích trasování naleznete v tématu [naslouchací procesy trasování](https://msdn.microsoft.com/library/4y5y10s7.aspx) na webu MSDN.</span><span class="sxs-lookup"><span data-stu-id="6a190-133">For more information about trace writers, see the [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx) topic on MSDN.</span></span>

### <a name="configuring-systemdiagnosticstracewriter"></a><span data-ttu-id="6a190-134">Konfigurace SystemDiagnosticsTraceWriter</span><span class="sxs-lookup"><span data-stu-id="6a190-134">Configuring SystemDiagnosticsTraceWriter</span></span>

<span data-ttu-id="6a190-135">Následující kód ukazuje, jak nakonfigurovat zapisovač trasování.</span><span class="sxs-lookup"><span data-stu-id="6a190-135">The following code shows how to configure the trace writer.</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="6a190-136">Můžete řídit dvě nastavení:</span><span class="sxs-lookup"><span data-stu-id="6a190-136">There are two settings that you can control:</span></span>

- <span data-ttu-id="6a190-137">Verbose: Pokud má hodnotu false, každé trasování obsahuje minimální informace.</span><span class="sxs-lookup"><span data-stu-id="6a190-137">IsVerbose: If false, each trace contains minimal information.</span></span> <span data-ttu-id="6a190-138">Je-li nastavena hodnota true, trasování obsahují více informací.</span><span class="sxs-lookup"><span data-stu-id="6a190-138">If true, traces include more information.</span></span>
- <span data-ttu-id="6a190-139">MinimumLevel: nastaví minimální úroveň trasování.</span><span class="sxs-lookup"><span data-stu-id="6a190-139">MinimumLevel: Sets the minimum trace level.</span></span> <span data-ttu-id="6a190-140">Úrovně trasování jsou v pořadí ladění, informace, varování, chyba a závažná.</span><span class="sxs-lookup"><span data-stu-id="6a190-140">Trace levels, in order, are Debug, Info, Warn, Error, and Fatal.</span></span>

## <a name="adding-traces-to-your-web-api-application"></a><span data-ttu-id="6a190-141">Přidání trasování do aplikace webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="6a190-141">Adding Traces to Your Web API Application</span></span>

<span data-ttu-id="6a190-142">Přidáním zapisovače trasování získáte okamžitý přístup k trasování vytvořeným kanálem webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="6a190-142">Adding a trace writer gives you immediate access to the traces created by the Web API pipeline.</span></span> <span data-ttu-id="6a190-143">Můžete také použít zapisovač trasování k trasování vlastního kódu:</span><span class="sxs-lookup"><span data-stu-id="6a190-143">You can also use the trace writer to trace your own code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="6a190-144">Chcete-li získat zapisovač trasování, zavolejte **HttpConfiguration. Services. GetTraceWriter**.</span><span class="sxs-lookup"><span data-stu-id="6a190-144">To get the trace writer, call **HttpConfiguration.Services.GetTraceWriter**.</span></span> <span data-ttu-id="6a190-145">Z kontroleru je tato metoda přístupná prostřednictvím vlastnosti **ApiController. Configuration** .</span><span class="sxs-lookup"><span data-stu-id="6a190-145">From a controller, this method is accessible through the **ApiController.Configuration** property.</span></span>

<span data-ttu-id="6a190-146">Chcete-li napsat trasování, můžete zavolat metodu **ITraceWriter. Trace** přímo, ale třída [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) definuje některé rozšiřující metody, které jsou výstižnější.</span><span class="sxs-lookup"><span data-stu-id="6a190-146">To write a trace, you can call the **ITraceWriter.Trace** method directly, but the [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) class defines some extension methods that are more friendly.</span></span> <span data-ttu-id="6a190-147">Například metoda **info** zobrazená výše vytvoří trasování s **informacemi**úrovně trasování.</span><span class="sxs-lookup"><span data-stu-id="6a190-147">For example, the **Info** method shown above creates a trace with trace level **Info**.</span></span>

## <a name="web-api-tracing-infrastructure"></a><span data-ttu-id="6a190-148">Infrastruktura trasování webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="6a190-148">Web API Tracing Infrastructure</span></span>

<span data-ttu-id="6a190-149">Tato část popisuje, jak napsat vlastní zapisovač trasování pro webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="6a190-149">This section describes how to write a custom trace writer for Web API.</span></span>

<span data-ttu-id="6a190-150">Balíček Microsoft. AspNet. WebApi. Tracing je postaven na obecnější trasovací infrastruktuře ve webovém rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="6a190-150">The Microsoft.AspNet.WebApi.Tracing package is built on top of a more general tracing infrastructure in Web API.</span></span> <span data-ttu-id="6a190-151">Místo použití Microsoft. AspNet. WebApi. Tracing můžete také připojit jiné knihovny trasování nebo protokolování, jako je například [nLOG](http://nlog-project.org/) nebo [log4net](http://logging.apache.org/log4net/).</span><span class="sxs-lookup"><span data-stu-id="6a190-151">Instead of using Microsoft.AspNet.WebApi.Tracing, you can also plug in some other tracing/logging library, such as [NLog](http://nlog-project.org/) or [log4net](http://logging.apache.org/log4net/).</span></span>

<span data-ttu-id="6a190-152">Chcete-li shromažďovat trasování, implementujte rozhraní **ITraceWriter** .</span><span class="sxs-lookup"><span data-stu-id="6a190-152">To collect traces, implement the **ITraceWriter** interface.</span></span> <span data-ttu-id="6a190-153">Tady je jednoduchý příklad:</span><span class="sxs-lookup"><span data-stu-id="6a190-153">Here is a simple example:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="6a190-154">Metoda **ITraceWriter. Trace** vytvoří trasování.</span><span class="sxs-lookup"><span data-stu-id="6a190-154">The **ITraceWriter.Trace** method creates a trace.</span></span> <span data-ttu-id="6a190-155">Volající určuje kategorii a úroveň trasování.</span><span class="sxs-lookup"><span data-stu-id="6a190-155">The caller specifies a category and trace level.</span></span> <span data-ttu-id="6a190-156">Kategorie může být libovolný uživatelsky definovaný řetězec.</span><span class="sxs-lookup"><span data-stu-id="6a190-156">The category can be any user-defined string.</span></span> <span data-ttu-id="6a190-157">Vaše implementace **trasování** by měla provádět následující akce:</span><span class="sxs-lookup"><span data-stu-id="6a190-157">Your implementation of **Trace** should do the following:</span></span>

1. <span data-ttu-id="6a190-158">Vytvořte nový **TraceRecord**.</span><span class="sxs-lookup"><span data-stu-id="6a190-158">Create a new **TraceRecord**.</span></span> <span data-ttu-id="6a190-159">Inicializujte ji pomocí úrovně žádosti, kategorie a trasování, jak je znázorněno na obrázku.</span><span class="sxs-lookup"><span data-stu-id="6a190-159">Initialize it with the request, category, and trace level, as shown.</span></span> <span data-ttu-id="6a190-160">Tyto hodnoty poskytuje volající.</span><span class="sxs-lookup"><span data-stu-id="6a190-160">These values are provided by the caller.</span></span>
2. <span data-ttu-id="6a190-161">Vyvolat delegáta *traceAction*</span><span class="sxs-lookup"><span data-stu-id="6a190-161">Invoke the *traceAction* delegate.</span></span> <span data-ttu-id="6a190-162">Uvnitř tohoto delegáta se očekává, že volající vyplní zbytek **TraceRecord**.</span><span class="sxs-lookup"><span data-stu-id="6a190-162">Inside this delegate, the caller is expected to fill in the rest of the **TraceRecord**.</span></span>
3. <span data-ttu-id="6a190-163">Napište **TraceRecord**pomocí jakékoli metody protokolování, kterou chcete.</span><span class="sxs-lookup"><span data-stu-id="6a190-163">Write the **TraceRecord**, using any logging technique that you like.</span></span> <span data-ttu-id="6a190-164">Zde uvedený příklad jednoduše volá do **System. Diagnostics. Trace**.</span><span class="sxs-lookup"><span data-stu-id="6a190-164">The example shown here simply calls into **System.Diagnostics.Trace**.</span></span>

## <a name="setting-the-trace-writer"></a><span data-ttu-id="6a190-165">Nastavení zapisovače trasování</span><span class="sxs-lookup"><span data-stu-id="6a190-165">Setting the Trace Writer</span></span>

<span data-ttu-id="6a190-166">Chcete-li povolit trasování, je nutné nakonfigurovat webové rozhraní API tak, aby používalo implementaci **ITraceWriter** .</span><span class="sxs-lookup"><span data-stu-id="6a190-166">To enable tracing, you must configure Web API to use your **ITraceWriter** implementation.</span></span> <span data-ttu-id="6a190-167">Provedete to pomocí objektu **HttpConfiguration** , jak je znázorněno v následujícím kódu:</span><span class="sxs-lookup"><span data-stu-id="6a190-167">You do this through the **HttpConfiguration** object, as shown in the following code:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="6a190-168">Aktivní může být pouze jeden zapisovač trasování.</span><span class="sxs-lookup"><span data-stu-id="6a190-168">Only one trace writer can be active.</span></span> <span data-ttu-id="6a190-169">Ve výchozím nastavení webové rozhraní API nastaví &quot;trasování no-op&quot;, které nedělá nic.</span><span class="sxs-lookup"><span data-stu-id="6a190-169">By default, Web API sets a &quot;no-op&quot; tracer that does nothing.</span></span> <span data-ttu-id="6a190-170">(&quot;trasování no-op&quot; existuje, aby trasovací kód nemusel před zápisem trasování kontrolovat, zda má zapisovač trasování **hodnotu null** .)</span><span class="sxs-lookup"><span data-stu-id="6a190-170">(The &quot;no-op&quot; tracer exists so that tracing code does not have to check whether the trace writer is **null** before writing a trace.)</span></span>

## <a name="how-web-api-tracing-works"></a><span data-ttu-id="6a190-171">Jak funguje trasování webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="6a190-171">How Web API Tracing Works</span></span>

<span data-ttu-id="6a190-172">Trasování ve webovém rozhraní API používá vzor *fasády* : Pokud je povoleno trasování, webové rozhraní API zalomí různé části kanálu požadavků se třídami, které provádějí volání trasování.</span><span class="sxs-lookup"><span data-stu-id="6a190-172">Tracing in Web API uses a *facade* pattern: When tracing is enabled, Web API wraps various parts of the request pipeline with classes that perform trace calls.</span></span>

<span data-ttu-id="6a190-173">Když například vyberete kontroler, kanál používá rozhraní **IHttpControllerSelector** .</span><span class="sxs-lookup"><span data-stu-id="6a190-173">For example, when selecting a controller, the pipeline uses the **IHttpControllerSelector** interface.</span></span> <span data-ttu-id="6a190-174">Pokud je povoleno trasování, kanál vloží třídu, která implementuje **IHttpControllerSelector** , ale volá do reálné implementace:</span><span class="sxs-lookup"><span data-stu-id="6a190-174">With tracing enabled, the pipeline inserts a class that implements **IHttpControllerSelector** but calls through to the real implementation:</span></span>

![Trasování webového rozhraní API používá vzorek fasády.](tracing-in-aspnet-web-api/_static/image8.png)

<span data-ttu-id="6a190-176">Mezi výhody tohoto návrhu patří:</span><span class="sxs-lookup"><span data-stu-id="6a190-176">The benefits of this design include:</span></span>

- <span data-ttu-id="6a190-177">Pokud nepřidáte zapisovač trasování, nebudou vytvořeny instance trasování a nebude mít žádný vliv na výkon.</span><span class="sxs-lookup"><span data-stu-id="6a190-177">If you do not add a trace writer, the tracing components are not instantiated and have no performance impact.</span></span>
- <span data-ttu-id="6a190-178">Pokud nahradíte výchozí služby, jako je například **IHttpControllerSelector** , vlastní implementací, trasování není ovlivněno, protože trasování je provedeno pomocí objektu obálky.</span><span class="sxs-lookup"><span data-stu-id="6a190-178">If you replace default services such as **IHttpControllerSelector** with your own custom implementation, tracing is not affected, because tracing is done by the wrapper object.</span></span>

<span data-ttu-id="6a190-179">Můžete také nahradit celé rozhraní trasování API pro web pomocí vlastního rozhraní, a to nahrazením výchozí služby **ITraceManager** :</span><span class="sxs-lookup"><span data-stu-id="6a190-179">You can also replace the entire Web API trace framework with your own custom framework, by replacing the default **ITraceManager** service:</span></span>

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="6a190-180">Implementujte **ITraceManager. Initialize** pro inicializaci vašeho sledovacího systému.</span><span class="sxs-lookup"><span data-stu-id="6a190-180">Implement **ITraceManager.Initialize** to initialize your tracing system.</span></span> <span data-ttu-id="6a190-181">Uvědomte si, že to nahrazuje *celé* rozhraní trasování, včetně veškerého trasovacího kódu, který je součástí webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="6a190-181">Be aware that this replaces the *entire* trace framework, including all of the tracing code that is built into Web API.</span></span>

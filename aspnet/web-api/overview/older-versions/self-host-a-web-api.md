---
uid: web-api/overview/older-versions/self-host-a-web-api
title: Samoobslužné hostování ASP.NET webového rozhraní API 1C#()-ASP.NET 4. x
author: MikeWasson
description: Kurz s kódem ukazuje, jak hostovat webové rozhraní API v konzolové aplikaci.
ms.author: riande
ms.date: 01/26/2012
ms.custom: seoapril2019
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: bae1737ba5b16bc67fa0ed0474ff04df0add1b3a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525086"
---
# <a name="self-host-aspnet-web-api-1-c"></a><span data-ttu-id="49565-103">Samoobslužné hostování ASP.NET webového rozhraní API 1C#()</span><span class="sxs-lookup"><span data-stu-id="49565-103">Self-Host ASP.NET Web API 1 (C#)</span></span>

<span data-ttu-id="49565-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="49565-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="49565-105">V tomto kurzu se dozvíte, jak hostovat webové rozhraní API v konzolové aplikaci.</span><span class="sxs-lookup"><span data-stu-id="49565-105">This tutorial shows how to host a web API inside a console application.</span></span> <span data-ttu-id="49565-106">Webové rozhraní API ASP.NET nevyžaduje službu IIS.</span><span class="sxs-lookup"><span data-stu-id="49565-106">ASP.NET Web API does not require IIS.</span></span> <span data-ttu-id="49565-107">Webové rozhraní API můžete sami hostovat ve svém vlastním hostitelském procesu.</span><span class="sxs-lookup"><span data-stu-id="49565-107">You can self-host a web API in your own host process.</span></span> 
> 
> <span data-ttu-id="49565-108">**Nové aplikace by měly používat OWIN k samoobslužnému hostování webového rozhraní API.**</span><span class="sxs-lookup"><span data-stu-id="49565-108">**New applications should use OWIN to self-host Web API.**</span></span> <span data-ttu-id="49565-109">Viz [použití Owin k samoobslužnému hostování ASP.NET webového rozhraní API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="49565-109">See [Use OWIN to Self-Host ASP.NET Web API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="49565-110">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="49565-110">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="49565-111">Webové rozhraní API 1</span><span class="sxs-lookup"><span data-stu-id="49565-111">Web API 1</span></span>
> - <span data-ttu-id="49565-112">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="49565-112">Visual Studio 2012</span></span>

## <a name="create-the-console-application-project"></a><span data-ttu-id="49565-113">Vytvoření projektu konzolové aplikace</span><span class="sxs-lookup"><span data-stu-id="49565-113">Create the Console Application Project</span></span>

<span data-ttu-id="49565-114">Spusťte Visual Studio a na **úvodní** stránce vyberte **Nový projekt** .</span><span class="sxs-lookup"><span data-stu-id="49565-114">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="49565-115">Nebo v nabídce **soubor** vyberte **Nový** a pak **projekt**.</span><span class="sxs-lookup"><span data-stu-id="49565-115">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="49565-116">V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte uzel  **C# vizuál** .</span><span class="sxs-lookup"><span data-stu-id="49565-116">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="49565-117">V **části C#vizuál** vyberte **Windows**.</span><span class="sxs-lookup"><span data-stu-id="49565-117">Under **Visual C#**, select **Windows**.</span></span> <span data-ttu-id="49565-118">V seznamu šablon projektu vyberte možnost **Konzolová aplikace**.</span><span class="sxs-lookup"><span data-stu-id="49565-118">In the list of project templates, select **Console Application**.</span></span> <span data-ttu-id="49565-119">Pojmenujte projekt &quot;SelfHost&quot; a klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="49565-119">Name the project &quot;SelfHost&quot; and click **OK**.</span></span>

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a><span data-ttu-id="49565-120">Nastavení cílové architektury (Visual Studio 2010)</span><span class="sxs-lookup"><span data-stu-id="49565-120">Set the Target Framework (Visual Studio 2010)</span></span>

<span data-ttu-id="49565-121">Pokud používáte Visual Studio 2010, změňte cílovou architekturu na .NET Framework 4,0.</span><span class="sxs-lookup"><span data-stu-id="49565-121">If you are using Visual Studio 2010, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="49565-122">(Ve výchozím nastavení se šablona projektu zaměřuje na [Profil klienta rozhraní .NET Framework](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span><span class="sxs-lookup"><span data-stu-id="49565-122">(By default, the project template targets the [.Net Framework Client Profile](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)</span></span>

<span data-ttu-id="49565-123">V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a vyberte **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="49565-123">In Solution Explorer, right-click the project and select **Properties**.</span></span> <span data-ttu-id="49565-124">V rozevíracím seznamu **cílové rozhraní** Změňte cílovou architekturu na .NET Framework 4,0.</span><span class="sxs-lookup"><span data-stu-id="49565-124">In the **Target framework** dropdown list, change the target framework to .NET Framework 4.0.</span></span> <span data-ttu-id="49565-125">Po zobrazení výzvy k použití změny klikněte na **Ano**.</span><span class="sxs-lookup"><span data-stu-id="49565-125">When prompted to apply the change, click **Yes**.</span></span>

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a><span data-ttu-id="49565-126">Nainstalovat správce balíčků NuGet</span><span class="sxs-lookup"><span data-stu-id="49565-126">Install NuGet Package Manager</span></span>

<span data-ttu-id="49565-127">Správce balíčků NuGet je nejjednodušší způsob, jak přidat sestavení webového rozhraní API do projektu non-ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="49565-127">The NuGet Package Manager is the easiest way to add the Web API assemblies to a non-ASP.NET project.</span></span>

<span data-ttu-id="49565-128">Chcete-li zjistit, zda je nainstalován Správce balíčků NuGet, klikněte na nabídku **nástroje** v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="49565-128">To check if NuGet Package Manager is installed, click the **Tools** menu in Visual Studio.</span></span> <span data-ttu-id="49565-129">Pokud se zobrazí položka nabídky s názvem **Správce balíčků NuGet**, měli byste mít správce balíčků NuGet.</span><span class="sxs-lookup"><span data-stu-id="49565-129">If you see a menu item called **NuGet Package Manager**, then you have NuGet Package Manager.</span></span>

<span data-ttu-id="49565-130">Instalace správce balíčků NuGet:</span><span class="sxs-lookup"><span data-stu-id="49565-130">To install NuGet Package Manager:</span></span>

1. <span data-ttu-id="49565-131">Spusťte Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="49565-131">Start Visual Studio.</span></span>
2. <span data-ttu-id="49565-132">V nabídce **nástroje** vyberte **rozšíření a aktualizace**.</span><span class="sxs-lookup"><span data-stu-id="49565-132">From the **Tools** menu, select **Extensions and Updates**.</span></span>
3. <span data-ttu-id="49565-133">V dialogovém okně **rozšíření a aktualizace** vyberte **online**.</span><span class="sxs-lookup"><span data-stu-id="49565-133">In the **Extensions and Updates** dialog, select **Online**.</span></span>
4. <span data-ttu-id="49565-134">Pokud nevidíte "Správce balíčků NuGet", do vyhledávacího pole zadejte "Správce balíčků NuGet".</span><span class="sxs-lookup"><span data-stu-id="49565-134">If you don't see "NuGet Package Manager", type "nuget package manager" in the search box.</span></span>
5. <span data-ttu-id="49565-135">Vyberte správce balíčků NuGet a klikněte na **Stáhnout**.</span><span class="sxs-lookup"><span data-stu-id="49565-135">Select the NuGet Package Manager and click **Download**.</span></span>
6. <span data-ttu-id="49565-136">Po dokončení stahování se zobrazí výzva k instalaci.</span><span class="sxs-lookup"><span data-stu-id="49565-136">After the download completes, you will be prompted to install.</span></span>
7. <span data-ttu-id="49565-137">Po dokončení instalace se může zobrazit výzva k restartování sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="49565-137">After the installation completes, you might be prompted to restart Visual Studio.</span></span>

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a><span data-ttu-id="49565-138">Přidat balíček NuGet webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="49565-138">Add the Web API NuGet Package</span></span>

<span data-ttu-id="49565-139">Po instalaci správce balíčků NuGet přidejte do svého projektu balíček samoobslužného hostování webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="49565-139">After NuGet Package Manager is installed, add the Web API Self-Host package to your project.</span></span>

1. <span data-ttu-id="49565-140">V nabídce **nástroje** vyberte **Správce balíčků NuGet**.</span><span class="sxs-lookup"><span data-stu-id="49565-140">From the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="49565-141">*Poznámka*: Pokud tuto položku nabídky nevidíte, ujistěte se, že je správce balíčků NuGet nainstalovaný správně.</span><span class="sxs-lookup"><span data-stu-id="49565-141">*Note*: If do you not see this menu item, make sure that NuGet Package Manager installed correctly.</span></span>
2. <span data-ttu-id="49565-142">Vyberte **Spravovat balíčky NuGet pro řešení** .</span><span class="sxs-lookup"><span data-stu-id="49565-142">Select **Manage NuGet Packages for Solution**</span></span>
3. <span data-ttu-id="49565-143">V dialogovém okně **Spravovat balíčky zrnko** vyberte možnost **online**.</span><span class="sxs-lookup"><span data-stu-id="49565-143">In the **Manage NugGet Packages** dialog, select **Online**.</span></span>
4. <span data-ttu-id="49565-144">Do vyhledávacího pole zadejte &quot;Microsoft. AspNet. WebApi. SelfHost&quot;.</span><span class="sxs-lookup"><span data-stu-id="49565-144">In the search box, type &quot;Microsoft.AspNet.WebApi.SelfHost&quot;.</span></span>
5. <span data-ttu-id="49565-145">Vyberte samostatný hostitel webového rozhraní API ASP.NET a klikněte na **nainstalovat**.</span><span class="sxs-lookup"><span data-stu-id="49565-145">Select the ASP.NET Web API Self Host package and click **Install**.</span></span>
6. <span data-ttu-id="49565-146">Po instalaci balíčku zavřete dialog kliknutím na **Zavřít** .</span><span class="sxs-lookup"><span data-stu-id="49565-146">After the package installs, click **Close** to close the dialog.</span></span>

> [!NOTE]
> <span data-ttu-id="49565-147">Nezapomeňte nainstalovat balíček s názvem Microsoft. AspNet. WebApi. SelfHost, nikoli AspNetWebApi. SelfHost.</span><span class="sxs-lookup"><span data-stu-id="49565-147">Make sure to install the package named Microsoft.AspNet.WebApi.SelfHost, not AspNetWebApi.SelfHost.</span></span>

![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="49565-148">Vytvoření modelu a kontroleru</span><span class="sxs-lookup"><span data-stu-id="49565-148">Create the Model and Controller</span></span>

<span data-ttu-id="49565-149">V tomto kurzu se jako [Začínáme](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) kurz používá stejný model a třídy kontroleru.</span><span class="sxs-lookup"><span data-stu-id="49565-149">This tutorial uses the same model and controller classes as the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="49565-150">Přidejte veřejnou třídu s názvem `Product`.</span><span class="sxs-lookup"><span data-stu-id="49565-150">Add a public class named `Product`.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

<span data-ttu-id="49565-151">Přidejte veřejnou třídu s názvem `ProductsController`.</span><span class="sxs-lookup"><span data-stu-id="49565-151">Add a public class named `ProductsController`.</span></span> <span data-ttu-id="49565-152">Tato třída je odvozena od třídy **System. Web. http. ApiController**.</span><span class="sxs-lookup"><span data-stu-id="49565-152">Derive this class from **System.Web.Http.ApiController**.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

<span data-ttu-id="49565-153">Další informace o kódu v tomto kontroleru najdete v kurzu [Začínáme](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) .</span><span class="sxs-lookup"><span data-stu-id="49565-153">For more information about the code in this controller, see the [Getting Started](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) tutorial.</span></span> <span data-ttu-id="49565-154">Tento kontroler definuje tři akce GET:</span><span class="sxs-lookup"><span data-stu-id="49565-154">This controller defines three GET actions:</span></span>

| <span data-ttu-id="49565-155">URI</span><span class="sxs-lookup"><span data-stu-id="49565-155">URI</span></span> | <span data-ttu-id="49565-156">Popis</span><span class="sxs-lookup"><span data-stu-id="49565-156">Description</span></span> |
| --- | --- |
| <span data-ttu-id="49565-157">/api/products</span><span class="sxs-lookup"><span data-stu-id="49565-157">/api/products</span></span> | <span data-ttu-id="49565-158">Získá seznam všech produktů.</span><span class="sxs-lookup"><span data-stu-id="49565-158">Get a list of all products.</span></span> |
| <span data-ttu-id="49565-159">*ID* /API/Products/</span><span class="sxs-lookup"><span data-stu-id="49565-159">/api/products/*id*</span></span> | <span data-ttu-id="49565-160">Získá produkt podle ID.</span><span class="sxs-lookup"><span data-stu-id="49565-160">Get a product by ID.</span></span> |
| <span data-ttu-id="49565-161">/API/Products/? kategorie =*kategorie*</span><span class="sxs-lookup"><span data-stu-id="49565-161">/api/products/?category=*category*</span></span> | <span data-ttu-id="49565-162">Získá seznam produktů podle kategorií.</span><span class="sxs-lookup"><span data-stu-id="49565-162">Get a list of products by category.</span></span> |

## <a name="host-the-web-api"></a><span data-ttu-id="49565-163">Hostování webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="49565-163">Host the Web API</span></span>

<span data-ttu-id="49565-164">Otevřete soubor Program.cs a přidejte následující příkazy using:</span><span class="sxs-lookup"><span data-stu-id="49565-164">Open the file Program.cs and add the following using statements:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

<span data-ttu-id="49565-165">Do třídy **program** přidejte následující kód.</span><span class="sxs-lookup"><span data-stu-id="49565-165">Add the following code to the **Program** class.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a><span data-ttu-id="49565-166">Volitelné Přidání rezervace oboru názvů URL protokolu HTTP</span><span class="sxs-lookup"><span data-stu-id="49565-166">(Optional) Add an HTTP URL Namespace Reservation</span></span>

<span data-ttu-id="49565-167">Tato aplikace naslouchá `http://localhost:8080/`.</span><span class="sxs-lookup"><span data-stu-id="49565-167">This application listens to `http://localhost:8080/`.</span></span> <span data-ttu-id="49565-168">Ve výchozím nastavení vyžaduje naslouchání na konkrétní adrese HTTP oprávnění správce.</span><span class="sxs-lookup"><span data-stu-id="49565-168">By default, listening at a particular HTTP address requires administrator privileges.</span></span> <span data-ttu-id="49565-169">Při spuštění tohoto kurzu se vám proto může zobrazit tato chyba: "protokol HTTP nemohl zaregistrovat adresu URL http://+:8080/" Existují dva způsoby, jak se vyhnout této chybě:</span><span class="sxs-lookup"><span data-stu-id="49565-169">When you run the tutorial, therefore, you may get this error: "HTTP could not register URL http://+:8080/" There are two ways to avoid this error:</span></span>

- <span data-ttu-id="49565-170">Spusťte aplikaci Visual Studio se zvýšenými oprávněními správce nebo</span><span class="sxs-lookup"><span data-stu-id="49565-170">Run Visual Studio with elevated administrator permissions, or</span></span>
- <span data-ttu-id="49565-171">Pomocí nástroje Netsh. exe udělte vašemu účtu oprávnění k rezervaci adresy URL.</span><span class="sxs-lookup"><span data-stu-id="49565-171">Use Netsh.exe to give your account permissions to reserve the URL.</span></span>

<span data-ttu-id="49565-172">Chcete-li použít nástroj Netsh. exe, otevřete příkazový řádek s oprávněními správce a zadejte následující příkaz: následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="49565-172">To use Netsh.exe, open a command prompt with administrator privileges and enter the following command:following command:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

<span data-ttu-id="49565-173">kde *machine\username* je váš uživatelský účet.</span><span class="sxs-lookup"><span data-stu-id="49565-173">where *machine\username* is your user account.</span></span>

<span data-ttu-id="49565-174">Po skončení samoobslužného hostování nezapomeňte rezervaci odstranit:</span><span class="sxs-lookup"><span data-stu-id="49565-174">When you are finished self-hosting, be sure to delete the reservation:</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a><span data-ttu-id="49565-175">Volání webového rozhraní API z klientské aplikace (C#)</span><span class="sxs-lookup"><span data-stu-id="49565-175">Call the Web API from a Client Application (C#)</span></span>

<span data-ttu-id="49565-176">Pojďme napsat jednoduchou konzolovou aplikaci, která volá webové rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="49565-176">Let's write a simple console application that calls the web API.</span></span>

<span data-ttu-id="49565-177">Přidejte do řešení nový projekt konzolové aplikace:</span><span class="sxs-lookup"><span data-stu-id="49565-177">Add a new console application project to the solution:</span></span>

- <span data-ttu-id="49565-178">V Průzkumník řešení klikněte pravým tlačítkem na řešení a vyberte **Přidat nový projekt**.</span><span class="sxs-lookup"><span data-stu-id="49565-178">In Solution Explorer, right-click the solution and select **Add New Project**.</span></span>
- <span data-ttu-id="49565-179">Vytvořte novou konzolovou aplikaci s názvem &quot;ClientApp&quot;.</span><span class="sxs-lookup"><span data-stu-id="49565-179">Create a new console application named &quot;ClientApp&quot;.</span></span>

![](self-host-a-web-api/_static/image5.png)

<span data-ttu-id="49565-180">Pomocí Správce balíčků NuGet přidejte balíček základních knihoven webových rozhraní API ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="49565-180">Use NuGet Package Manager to add the ASP.NET Web API Core Libraries package:</span></span>

- <span data-ttu-id="49565-181">V nabídce Nástroje vyberte **Správce balíčků NuGet**.</span><span class="sxs-lookup"><span data-stu-id="49565-181">From the Tools menu, select **NuGet Package Manager**.</span></span>
- <span data-ttu-id="49565-182">Vyberte **Spravovat balíčky NuGet pro řešení** .</span><span class="sxs-lookup"><span data-stu-id="49565-182">Select **Manage NuGet Packages for Solution**</span></span>
- <span data-ttu-id="49565-183">V dialogovém okně **Spravovat balíčky NuGet** vyberte **online**.</span><span class="sxs-lookup"><span data-stu-id="49565-183">In the **Manage NuGet Packages** dialog, select **Online**.</span></span>
- <span data-ttu-id="49565-184">Do vyhledávacího pole zadejte &quot;Microsoft. AspNet. WebApi. Client&quot;.</span><span class="sxs-lookup"><span data-stu-id="49565-184">In the search box, type &quot;Microsoft.AspNet.WebApi.Client&quot;.</span></span>
- <span data-ttu-id="49565-185">Vyberte balíček klientské knihovny Microsoft ASP.NET webového rozhraní API a klikněte na **nainstalovat**.</span><span class="sxs-lookup"><span data-stu-id="49565-185">Select the Microsoft ASP.NET Web API Client Libraries package and click **Install**.</span></span>

<span data-ttu-id="49565-186">Přidejte odkaz v ClientApp do projektu SelfHost:</span><span class="sxs-lookup"><span data-stu-id="49565-186">Add a reference in ClientApp to the SelfHost project:</span></span>

- <span data-ttu-id="49565-187">V Průzkumník řešení klikněte pravým tlačítkem myši na projekt ClientApp.</span><span class="sxs-lookup"><span data-stu-id="49565-187">In Solution Explorer, right-click the ClientApp project.</span></span>
- <span data-ttu-id="49565-188">Vyberte **Přidat odkaz**.</span><span class="sxs-lookup"><span data-stu-id="49565-188">Select **Add Reference**.</span></span>
- <span data-ttu-id="49565-189">V dialogovém okně **Správce odkazů** v části **řešení**vyberte **projekty**.</span><span class="sxs-lookup"><span data-stu-id="49565-189">In the **Reference Manager** dialog, under **Solution**, select **Projects**.</span></span>
- <span data-ttu-id="49565-190">Vyberte projekt SelfHost.</span><span class="sxs-lookup"><span data-stu-id="49565-190">Select the SelfHost project.</span></span>
- <span data-ttu-id="49565-191">Klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="49565-191">Click **OK**.</span></span>

![](self-host-a-web-api/_static/image6.png)

<span data-ttu-id="49565-192">Otevřete soubor Client/program. cs.</span><span class="sxs-lookup"><span data-stu-id="49565-192">Open the Client/Program.cs file.</span></span> <span data-ttu-id="49565-193">Přidejte následující příkaz **using** :</span><span class="sxs-lookup"><span data-stu-id="49565-193">Add the following **using** statement:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

<span data-ttu-id="49565-194">Přidejte statickou instanci **HttpClient** :</span><span class="sxs-lookup"><span data-stu-id="49565-194">Add a static **HttpClient** instance:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

<span data-ttu-id="49565-195">Přidejte následující metody k vypsání seznamu všechny produkty, vypíše produkt podle ID a vypíše produkty podle kategorie.</span><span class="sxs-lookup"><span data-stu-id="49565-195">Add the following methods to list all products, list a product by ID, and list products by category.</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

<span data-ttu-id="49565-196">Každá z těchto metod se shoduje se stejným vzorem:</span><span class="sxs-lookup"><span data-stu-id="49565-196">Each of these methods follows the same pattern:</span></span>

1. <span data-ttu-id="49565-197">Voláním **HttpClient. GetAsync** odešlete požadavek GET na příslušný identifikátor URI.</span><span class="sxs-lookup"><span data-stu-id="49565-197">Call **HttpClient.GetAsync** to send a GET request to the appropriate URI.</span></span>
2. <span data-ttu-id="49565-198">Zavolejte **HttpResponseMessage. EnsureSuccessStatusCode**.</span><span class="sxs-lookup"><span data-stu-id="49565-198">Call **HttpResponseMessage.EnsureSuccessStatusCode**.</span></span> <span data-ttu-id="49565-199">Tato metoda vyvolá výjimku, pokud je stavem odpovědi HTTP kód chyby.</span><span class="sxs-lookup"><span data-stu-id="49565-199">This method throws an exception if the HTTP response status is an error code.</span></span>
3. <span data-ttu-id="49565-200">Pro rekonstrukci typu CLR z odpovědi HTTP zavolejte **ReadAsAsync&lt;t&gt;** .</span><span class="sxs-lookup"><span data-stu-id="49565-200">Call **ReadAsAsync&lt;T&gt;** to deserialize a CLR type from the HTTP response.</span></span> <span data-ttu-id="49565-201">Tato metoda je rozšiřující metoda definovaná v **System .NET. http. HttpContentExtensions**.</span><span class="sxs-lookup"><span data-stu-id="49565-201">This method is an extension method, defined in **System.Net.Http.HttpContentExtensions**.</span></span>

<span data-ttu-id="49565-202">Metody **GetAsync** a **ReadAsAsync** jsou asynchronní.</span><span class="sxs-lookup"><span data-stu-id="49565-202">The **GetAsync** and **ReadAsAsync** methods are both asynchronous.</span></span> <span data-ttu-id="49565-203">Vrací objekty **úkolu** , které představují asynchronní operaci.</span><span class="sxs-lookup"><span data-stu-id="49565-203">They return **Task** objects that represent the asynchronous operation.</span></span> <span data-ttu-id="49565-204">Získání vlastnosti **výsledku** zablokuje vlákno, dokud se operace nedokončí.</span><span class="sxs-lookup"><span data-stu-id="49565-204">Getting the **Result** property blocks the thread until the operation completes.</span></span>

<span data-ttu-id="49565-205">Další informace o použití HttpClient, včetně toho, jak provést neblokující volání, najdete v tématu [volání webového rozhraní API z klienta .NET](../advanced/calling-a-web-api-from-a-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="49565-205">For more information about using HttpClient, including how to make non-blocking calls, see [Calling a Web API From a .NET Client](../advanced/calling-a-web-api-from-a-net-client.md).</span></span>

<span data-ttu-id="49565-206">Před voláním těchto metod nastavte vlastnost BaseAddress v instanci HttpClient na hodnotu "`http://localhost:8080`".</span><span class="sxs-lookup"><span data-stu-id="49565-206">Before calling these methods, set the BaseAddress property on the HttpClient instance to "`http://localhost:8080`".</span></span> <span data-ttu-id="49565-207">Příklad:</span><span class="sxs-lookup"><span data-stu-id="49565-207">For example:</span></span>

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

<span data-ttu-id="49565-208">To by mělo mít následující výstup.</span><span class="sxs-lookup"><span data-stu-id="49565-208">This should output the following.</span></span> <span data-ttu-id="49565-209">(Nezapomeňte nejdřív spustit aplikaci SelfHost.)</span><span class="sxs-lookup"><span data-stu-id="49565-209">(Remember to run the SelfHost application first.)</span></span>

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)

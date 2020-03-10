---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
title: Vytvoření klientské aplikace OData v4 (C#) | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 47202362-3808-4add-9a69-c9d1f91d5e4e
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
msc.type: authoredcontent
ms.openlocfilehash: a0016cf2cc7bffe6268664395ccb38e140090310
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556292"
---
# <a name="create-an-odata-v4-client-app-c"></a><span data-ttu-id="bdfba-102">Vytvoření klientské aplikace OData v4 (C#)</span><span class="sxs-lookup"><span data-stu-id="bdfba-102">Create an OData v4 Client App (C#)</span></span>

<span data-ttu-id="bdfba-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="bdfba-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="bdfba-104">V předchozím kurzu jste vytvořili základní službu OData, která podporuje operace CRUD.</span><span class="sxs-lookup"><span data-stu-id="bdfba-104">In the previous tutorial, you created a basic OData service that supports CRUD operations.</span></span> <span data-ttu-id="bdfba-105">Nyní vytvoříme klienta pro službu.</span><span class="sxs-lookup"><span data-stu-id="bdfba-105">Now let's create a client for the service.</span></span>

<span data-ttu-id="bdfba-106">Spusťte novou instanci sady Visual Studio a vytvořte nový projekt konzolové aplikace.</span><span class="sxs-lookup"><span data-stu-id="bdfba-106">Start a new instance of Visual Studio and create a new console application project.</span></span> <span data-ttu-id="bdfba-107">V dialogovém okně **Nový projekt** vyberte možnost **nainstalované** &gt; **šablony** &gt; **Visual C#**  &gt; **plocha Windows**a vyberte šablonu **Konzolová aplikace** .</span><span class="sxs-lookup"><span data-stu-id="bdfba-107">In the **New Project** dialog, select **Installed** &gt; **Templates** &gt; **Visual C#** &gt; **Windows Desktop**, and select the **Console Application** template.</span></span> <span data-ttu-id="bdfba-108">Pojmenujte projekt &quot;ProductsApp&quot;.</span><span class="sxs-lookup"><span data-stu-id="bdfba-108">Name the project &quot;ProductsApp&quot;.</span></span>

![](create-an-odata-v4-client-app/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="bdfba-109">Konzolovou aplikaci můžete také přidat do stejného řešení sady Visual Studio, které obsahuje službu OData.</span><span class="sxs-lookup"><span data-stu-id="bdfba-109">You can also add the console app to the same Visual Studio solution that contains the OData service.</span></span>

## <a name="install-the-odata-client-code-generator"></a><span data-ttu-id="bdfba-110">Instalace generátoru kódu klienta OData</span><span class="sxs-lookup"><span data-stu-id="bdfba-110">Install the OData Client Code Generator</span></span>

<span data-ttu-id="bdfba-111">V nabídce **nástroje** vyberte **rozšíření a aktualizace**.</span><span class="sxs-lookup"><span data-stu-id="bdfba-111">From the **Tools** menu, select **Extensions and Updates**.</span></span> <span data-ttu-id="bdfba-112">Vyberte **Online** &gt; **galerii sady Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="bdfba-112">Select **Online** &gt; **Visual Studio Gallery**.</span></span> <span data-ttu-id="bdfba-113">Do vyhledávacího pole vyhledejte &quot;&quot;generátoru kódu klienta OData.</span><span class="sxs-lookup"><span data-stu-id="bdfba-113">In the search box, search for &quot;OData Client Code Generator&quot;.</span></span> <span data-ttu-id="bdfba-114">Kliknutím na **Stáhnout** nainstalujte VSIX.</span><span class="sxs-lookup"><span data-stu-id="bdfba-114">Click **Download** to install the VSIX.</span></span> <span data-ttu-id="bdfba-115">Může se zobrazit výzva k restartování sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bdfba-115">You might be prompted to restart Visual Studio.</span></span>

[![](create-an-odata-v4-client-app/_static/image3.png)](create-an-odata-v4-client-app/_static/image2.png)

## <a name="run-the-odata-service-locally"></a><span data-ttu-id="bdfba-116">Místní spuštění služby OData</span><span class="sxs-lookup"><span data-stu-id="bdfba-116">Run the OData Service Locally</span></span>

<span data-ttu-id="bdfba-117">Spusťte projekt ProductService ze sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bdfba-117">Run the ProductService project from Visual Studio.</span></span> <span data-ttu-id="bdfba-118">Ve výchozím nastavení Visual Studio spustí prohlížeč do kořenového adresáře aplikace.</span><span class="sxs-lookup"><span data-stu-id="bdfba-118">By default, Visual Studio launches a browser to the application root.</span></span> <span data-ttu-id="bdfba-119">Poznamenejte si identifikátor URI; budete ho potřebovat v dalším kroku.</span><span class="sxs-lookup"><span data-stu-id="bdfba-119">Note the URI; you will need this in the next step.</span></span> <span data-ttu-id="bdfba-120">Ponechte aplikaci spuštěnou.</span><span class="sxs-lookup"><span data-stu-id="bdfba-120">Leave the application running.</span></span>

![](create-an-odata-v4-client-app/_static/image4.png)

> [!NOTE]
> <span data-ttu-id="bdfba-121">Pokud oba projekty umístíte do stejného řešení, nezapomeňte spustit projekt ProductService bez ladění.</span><span class="sxs-lookup"><span data-stu-id="bdfba-121">If you put both projects in the same solution, make sure to run the ProductService project without debugging.</span></span> <span data-ttu-id="bdfba-122">V dalším kroku budete muset zajistit, aby služba běžela při úpravě projektu konzolové aplikace.</span><span class="sxs-lookup"><span data-stu-id="bdfba-122">In the next step, you will need to keep the service running while you modify the console application project.</span></span>

## <a name="generate-the-service-proxy"></a><span data-ttu-id="bdfba-123">Vygenerovat proxy služby</span><span class="sxs-lookup"><span data-stu-id="bdfba-123">Generate the Service Proxy</span></span>

<span data-ttu-id="bdfba-124">Proxy služby je třída rozhraní .NET, která definuje metody pro přístup ke službě OData.</span><span class="sxs-lookup"><span data-stu-id="bdfba-124">The service proxy is a .NET class that defines methods for accessing the OData service.</span></span> <span data-ttu-id="bdfba-125">Proxy překládá volání metod na požadavky HTTP.</span><span class="sxs-lookup"><span data-stu-id="bdfba-125">The proxy translates method calls into HTTP requests.</span></span> <span data-ttu-id="bdfba-126">Třídu proxy vytvoříte spuštěním [šablony T4](https://msdn.microsoft.com/library/bb126445.aspx).</span><span class="sxs-lookup"><span data-stu-id="bdfba-126">You will create the proxy class by running a [T4 template](https://msdn.microsoft.com/library/bb126445.aspx).</span></span>

<span data-ttu-id="bdfba-127">Klikněte pravým tlačítkem na projekt.</span><span class="sxs-lookup"><span data-stu-id="bdfba-127">Right-click the project.</span></span> <span data-ttu-id="bdfba-128">Vyberte **přidat** &gt; **novou položku**.</span><span class="sxs-lookup"><span data-stu-id="bdfba-128">Select **Add** &gt; **New Item**.</span></span>

![](create-an-odata-v4-client-app/_static/image5.png)

<span data-ttu-id="bdfba-129">V dialogovém okně **Přidat novou položku** vyberte položku **vizuální C# položky** &gt; **kód** &gt; **OData Client**.</span><span class="sxs-lookup"><span data-stu-id="bdfba-129">In the **Add New Item** dialog, select **Visual C# Items** &gt; **Code** &gt; **OData Client**.</span></span> <span data-ttu-id="bdfba-130">Pojmenujte šablonu &quot;ProductClient.tt&quot;.</span><span class="sxs-lookup"><span data-stu-id="bdfba-130">Name the template &quot;ProductClient.tt&quot;.</span></span> <span data-ttu-id="bdfba-131">Klikněte na **Přidat** a potom na upozornění zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="bdfba-131">Click **Add** and click through the security warning.</span></span>

[![](create-an-odata-v4-client-app/_static/image7.png)](create-an-odata-v4-client-app/_static/image6.png)

<span data-ttu-id="bdfba-132">V tomto okamžiku se zobrazí chyba, kterou můžete ignorovat.</span><span class="sxs-lookup"><span data-stu-id="bdfba-132">At this point, you'll get an error, which you can ignore.</span></span> <span data-ttu-id="bdfba-133">Visual Studio automaticky spustí šablonu, ale šablona potřebuje nejdřív některá nastavení konfigurace.</span><span class="sxs-lookup"><span data-stu-id="bdfba-133">Visual Studio automatically runs the template, but the template needs some configuration settings first.</span></span>

[![](create-an-odata-v4-client-app/_static/image9.png)](create-an-odata-v4-client-app/_static/image8.png)

<span data-ttu-id="bdfba-134">Otevřete soubor ProductClient. OData. config. V elementu `Parameter` vložte identifikátor URI z projektu ProductService (předchozí krok).</span><span class="sxs-lookup"><span data-stu-id="bdfba-134">Open the file ProductClient.odata.config. In the `Parameter` element, paste in the URI from the ProductService project (previous step).</span></span> <span data-ttu-id="bdfba-135">Příklad:</span><span class="sxs-lookup"><span data-stu-id="bdfba-135">For example:</span></span>

[!code-xml[Main](create-an-odata-v4-client-app/samples/sample1.xml)]

[![](create-an-odata-v4-client-app/_static/image11.png)](create-an-odata-v4-client-app/_static/image10.png)

<span data-ttu-id="bdfba-136">Znovu spusťte šablonu.</span><span class="sxs-lookup"><span data-stu-id="bdfba-136">Run the template again.</span></span> <span data-ttu-id="bdfba-137">V Průzkumník řešení klikněte pravým tlačítkem na soubor ProductClient.tt a vyberte **Spustit vlastní nástroj**.</span><span class="sxs-lookup"><span data-stu-id="bdfba-137">In Solution Explorer, right click the ProductClient.tt file and select **Run Custom Tool**.</span></span>

<span data-ttu-id="bdfba-138">Šablona vytvoří soubor kódu s názvem ProductClient.cs, který definuje proxy server.</span><span class="sxs-lookup"><span data-stu-id="bdfba-138">The template creates a code file named ProductClient.cs that defines the proxy.</span></span> <span data-ttu-id="bdfba-139">Při vývoji aplikace můžete při změně koncového bodu OData znovu spustit šablonu a aktualizovat proxy.</span><span class="sxs-lookup"><span data-stu-id="bdfba-139">As you develop your app, if you change the OData endpoint, run the template again to update the proxy.</span></span>

![](create-an-odata-v4-client-app/_static/image12.png)

## <a name="use-the-service-proxy-to-call-the-odata-service"></a><span data-ttu-id="bdfba-140">Použití proxy služby pro volání služby OData</span><span class="sxs-lookup"><span data-stu-id="bdfba-140">Use the Service Proxy to Call the OData Service</span></span>

<span data-ttu-id="bdfba-141">Otevřete soubor Program.cs a nahraďte často používaný kód následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="bdfba-141">Open the file Program.cs and replace the boilerplate code with the following.</span></span>

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample2.cs)]

<span data-ttu-id="bdfba-142">Nahraďte hodnotu *SERVICEURI* identifikátorem URI služby ze starší verze.</span><span class="sxs-lookup"><span data-stu-id="bdfba-142">Replace the value of *serviceUri* with the service URI from earlier.</span></span>

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample3.cs)]

<span data-ttu-id="bdfba-143">Při spuštění aplikace by měla být výstupem následující:</span><span class="sxs-lookup"><span data-stu-id="bdfba-143">When you run the app, it should output the following:</span></span>

[!code-console[Main](create-an-odata-v4-client-app/samples/sample4.cmd)]

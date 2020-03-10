---
uid: mvc/overview/deployment/docker
title: Migrace aplikací ASP.NET MVC do kontejnerů s Windows
description: Naučte se, jak převzít existující aplikaci ASP.NET MVC a spustit ji v kontejneru Docker ve Windows
keywords: Kontejnery Windows, Docker, ASP. NET MVC
author: BillWagner
ms.author: wiwagn
ms.date: 12/14/2018
ms.assetid: c9f1d52c-b4bd-4b5d-b7f9-8f9ceaf778c4
ms.openlocfilehash: ef184f4256c20e2a66de8fd2d4f8e67f07d9a086
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583627"
---
# <a name="migrating-aspnet-mvc-applications-to-windows-containers"></a><span data-ttu-id="8db03-104">Migrace aplikací ASP.NET MVC do kontejnerů s Windows</span><span class="sxs-lookup"><span data-stu-id="8db03-104">Migrating ASP.NET MVC Applications to Windows Containers</span></span>

<span data-ttu-id="8db03-105">Spuštění existující aplikace založené na .NET Framework v kontejneru Windows nevyžaduje žádné změny aplikace.</span><span class="sxs-lookup"><span data-stu-id="8db03-105">Running an existing .NET Framework-based application in a Windows container doesn't require any changes to your app.</span></span> <span data-ttu-id="8db03-106">Pokud chcete aplikaci spustit v kontejneru Windows, vytvořte image Docker obsahující vaši aplikaci a spusťte kontejner.</span><span class="sxs-lookup"><span data-stu-id="8db03-106">To run your app in a Windows container you create a Docker image containing your app and start the container.</span></span> <span data-ttu-id="8db03-107">Toto téma vysvětluje, jak přijmout existující [aplikaci ASP.NET MVC](http://www.asp.net/mvc) a jak ji nasadit do kontejneru Windows.</span><span class="sxs-lookup"><span data-stu-id="8db03-107">This topic explains how to take an existing [ASP.NET MVC application](http://www.asp.net/mvc) and deploy it in a Windows container.</span></span>

<span data-ttu-id="8db03-108">Začnete s existující aplikací ASP.NET MVC a pak sestavíte publikované assety pomocí sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8db03-108">You start with an existing ASP.NET MVC app, then build the published assets using Visual Studio.</span></span> <span data-ttu-id="8db03-109">Pomocí Docker vytvoříte image, která obsahuje a spustí vaši aplikaci.</span><span class="sxs-lookup"><span data-stu-id="8db03-109">You use Docker to create the image that contains and runs your app.</span></span> <span data-ttu-id="8db03-110">Přejdete na web běžící v kontejneru Windows a ověříte, že aplikace funguje.</span><span class="sxs-lookup"><span data-stu-id="8db03-110">You'll browse to the site running in a Windows container and verify the app is working.</span></span>

<span data-ttu-id="8db03-111">Tento článek předpokládá základní znalost Dockeru.</span><span class="sxs-lookup"><span data-stu-id="8db03-111">This article assumes a basic understanding of Docker.</span></span> <span data-ttu-id="8db03-112">Informace o Dockeru najdete v článku [Docker Overview](https://docs.docker.com/engine/understanding-docker/) (Přehled Dockeru).</span><span class="sxs-lookup"><span data-stu-id="8db03-112">You can learn about Docker by reading the [Docker Overview](https://docs.docker.com/engine/understanding-docker/).</span></span>

<span data-ttu-id="8db03-113">Aplikace, kterou spouštíte v kontejneru, je jednoduchý web, který je náhodně zodpovězený na otázky.</span><span class="sxs-lookup"><span data-stu-id="8db03-113">The app you'll run in a container is a simple website that answers questions randomly.</span></span> <span data-ttu-id="8db03-114">Tato aplikace je základní aplikace MVC bez ověřování nebo úložiště databáze. Díky tomu se můžete zaměřit na přesun webové vrstvy do kontejneru.</span><span class="sxs-lookup"><span data-stu-id="8db03-114">This app is a basic MVC application with no authentication or database storage; it lets you focus on moving the web tier to a container.</span></span> <span data-ttu-id="8db03-115">V budoucích tématech se dozvíte, jak přesunout a spravovat trvalé úložiště v kontejnerových aplikacích.</span><span class="sxs-lookup"><span data-stu-id="8db03-115">Future topics will show how to move and manage persistent storage in containerized applications.</span></span>

<span data-ttu-id="8db03-116">Přesunutí aplikace zahrnuje tyto kroky:</span><span class="sxs-lookup"><span data-stu-id="8db03-116">Moving your application involves these steps:</span></span>

1. [<span data-ttu-id="8db03-117">Vytvoření úlohy publikování pro sestavení assetů pro obrázek.</span><span class="sxs-lookup"><span data-stu-id="8db03-117">Creating a publish task to build the assets for an image.</span></span>](#publish-script)
1. [<span data-ttu-id="8db03-118">Sestavení image Docker, která spustí vaši aplikaci.</span><span class="sxs-lookup"><span data-stu-id="8db03-118">Building a Docker image that will run your application.</span></span>](#build-the-image)
1. [<span data-ttu-id="8db03-119">Spouští se kontejner Docker, který spouští vaši image.</span><span class="sxs-lookup"><span data-stu-id="8db03-119">Starting a Docker container that runs your image.</span></span>](#start-a-container)
1. [<span data-ttu-id="8db03-120">Ověřuje se aplikace v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="8db03-120">Verifying the application using your browser.</span></span>](#verify-in-the-browser)

<span data-ttu-id="8db03-121">[Dokončená aplikace](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator) je na GitHubu.</span><span class="sxs-lookup"><span data-stu-id="8db03-121">The [finished application](https://github.com/dotnet/samples/tree/master/framework/docker/MVCRandomAnswerGenerator) is on GitHub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8db03-122">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="8db03-122">Prerequisites</span></span>

<span data-ttu-id="8db03-123">Vývojový počítač musí mít následující software:</span><span class="sxs-lookup"><span data-stu-id="8db03-123">The development machine must have the following software:</span></span>

- <span data-ttu-id="8db03-124">[Windows 10 – aktualizace pro výročí](https://www.microsoft.com/software-download/windows10/) (nebo vyšší) nebo [Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) (nebo vyšší)</span><span class="sxs-lookup"><span data-stu-id="8db03-124">[Windows 10 Anniversary Update](https://www.microsoft.com/software-download/windows10/) (or higher) or [Windows Server 2016](https://www.microsoft.com/cloud-platform/windows-server) (or higher)</span></span>
- <span data-ttu-id="8db03-125">[Docker for Windows](https://docs.docker.com/docker-for-windows/) – stabilní verze 1.13.0 nebo 1,12 beta 26 (nebo novější verze)</span><span class="sxs-lookup"><span data-stu-id="8db03-125">[Docker for Windows](https://docs.docker.com/docker-for-windows/) - version Stable 1.13.0 or 1.12 Beta 26 (or newer versions)</span></span>
- [<span data-ttu-id="8db03-126">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="8db03-126">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

> [!IMPORTANT]
> <span data-ttu-id="8db03-127">Pokud používáte Windows Server 2016, postupujte podle pokynů pro [nasazení hostitele kontejnerů – Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment).</span><span class="sxs-lookup"><span data-stu-id="8db03-127">If you are using Windows Server 2016, follow the instructions for [Container Host Deployment - Windows Server](https://msdn.microsoft.com/virtualization/windowscontainers/deployment/deployment).</span></span>

<span data-ttu-id="8db03-128">Po nainstalování a spuštění Dockeru klikněte pravým tlačítkem myši na ikonu na hlavním panelu a vyberte **Switch to Windows containers** (Přepnout na kontejnery Windows).</span><span class="sxs-lookup"><span data-stu-id="8db03-128">After installing and starting Docker, right-click on the tray icon and select **Switch to Windows containers**.</span></span> <span data-ttu-id="8db03-129">To se vyžaduje pro spuštění imagí Dockeru založených na Windows.</span><span class="sxs-lookup"><span data-stu-id="8db03-129">This is required to run Docker images based on Windows.</span></span> <span data-ttu-id="8db03-130">Spuštění tohoto příkazu trvá několik sekund:</span><span class="sxs-lookup"><span data-stu-id="8db03-130">This command takes a few seconds to execute:</span></span>

<span data-ttu-id="8db03-131">![Kontejner Windows][windows-container]</span><span class="sxs-lookup"><span data-stu-id="8db03-131">![Windows Container][windows-container]</span></span>

## <a name="publish-script"></a><span data-ttu-id="8db03-132">Publikovat skript</span><span class="sxs-lookup"><span data-stu-id="8db03-132">Publish script</span></span>

<span data-ttu-id="8db03-133">Shromážděte na jednom místě všechny prostředky, které potřebujete nahrát do image Dockeru.</span><span class="sxs-lookup"><span data-stu-id="8db03-133">Collect all the assets that you need to load into a Docker image in one place.</span></span> <span data-ttu-id="8db03-134">Pomocí příkazu **publikovat** v aplikaci Visual Studio můžete pro svou aplikaci vytvořit profil publikování.</span><span class="sxs-lookup"><span data-stu-id="8db03-134">You can use the Visual Studio **Publish** command to create a publish profile for your app.</span></span> <span data-ttu-id="8db03-135">Tento profil vloží všechny prostředky do jednoho adresářového stromu, které zkopírujete do cílové image později v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="8db03-135">This profile will put all the assets in one directory tree that you copy to your target image later in this tutorial.</span></span>

<span data-ttu-id="8db03-136">**Kroky publikování**</span><span class="sxs-lookup"><span data-stu-id="8db03-136">**Publish Steps**</span></span>

1. <span data-ttu-id="8db03-137">Klikněte pravým tlačítkem na webový projekt v aplikaci Visual Studio a vyberte **publikovat**.</span><span class="sxs-lookup"><span data-stu-id="8db03-137">Right click on the web project in Visual Studio, and select **Publish**.</span></span>
1. <span data-ttu-id="8db03-138">Klikněte na **tlačítko vlastní profil**a pak jako metodu vyberte **systém souborů** .</span><span class="sxs-lookup"><span data-stu-id="8db03-138">Click the **Custom profile button**, and then select **File System** as the method.</span></span>
1. <span data-ttu-id="8db03-139">Vyberte adresář.</span><span class="sxs-lookup"><span data-stu-id="8db03-139">Choose the directory.</span></span> <span data-ttu-id="8db03-140">Podle konvence stažený vzorek používá `bin\Release\PublishOutput`.</span><span class="sxs-lookup"><span data-stu-id="8db03-140">By convention, the downloaded sample uses `bin\Release\PublishOutput`.</span></span>

<span data-ttu-id="8db03-141">![Publikovat připojení][publish-connection]</span><span class="sxs-lookup"><span data-stu-id="8db03-141">![Publish Connection][publish-connection]</span></span>

<span data-ttu-id="8db03-142">Otevřete část **Možnosti publikování souboru** na kartě **Nastavení** . Vyberte **předkompilovat během publikování**.</span><span class="sxs-lookup"><span data-stu-id="8db03-142">Open the **File Publish Options** section of the **Settings** tab. Select **Precompile during publishing**.</span></span> <span data-ttu-id="8db03-143">Tato optimalizace znamená, že budete kompilovat zobrazení v kontejneru Docker, kopírujete Předkompilovaná zobrazení.</span><span class="sxs-lookup"><span data-stu-id="8db03-143">This optimization means that you'll be compiling views in the Docker container, you are copying the precompiled views.</span></span>

<span data-ttu-id="8db03-144">![Nastavení publikování][publish-settings]</span><span class="sxs-lookup"><span data-stu-id="8db03-144">![Publish Settings][publish-settings]</span></span>

<span data-ttu-id="8db03-145">Klikněte na **publikovat**a Visual Studio zkopíruje všechny potřebné prostředky do cílové složky.</span><span class="sxs-lookup"><span data-stu-id="8db03-145">Click **Publish**, and Visual Studio will copy all the needed assets to the destination folder.</span></span>

## <a name="build-the-image"></a><span data-ttu-id="8db03-146">Sestavení image</span><span class="sxs-lookup"><span data-stu-id="8db03-146">Build the image</span></span>

<span data-ttu-id="8db03-147">Vytvořte nový soubor s názvem *souboru Dockerfile* a definujte image Docker.</span><span class="sxs-lookup"><span data-stu-id="8db03-147">Create a new file named *Dockerfile* to define your Docker image.</span></span> <span data-ttu-id="8db03-148">*Souboru Dockerfile* obsahuje pokyny pro sestavení finální image a zahrnuje všechny základní názvy imagí, požadované komponenty, aplikaci, kterou chcete spustit, a další konfigurační image.</span><span class="sxs-lookup"><span data-stu-id="8db03-148">*Dockerfile* contains instructions to build the final image and includes any base image names, required components, the app you want to run, and other configuration images.</span></span> <span data-ttu-id="8db03-149">*Souboru Dockerfile* je vstup k příkazu `docker build`, který vytváří bitovou kopii.</span><span class="sxs-lookup"><span data-stu-id="8db03-149">*Dockerfile* is the input to the `docker build` command that creates the image.</span></span>

<span data-ttu-id="8db03-150">Pro toto cvičení sestavíte image na základě `microsoft/aspnet` image, která se nachází v [Docker Hub](https://hub.docker.com/r/microsoft/aspnet/).</span><span class="sxs-lookup"><span data-stu-id="8db03-150">For this exercise, you will build an image based on the `microsoft/aspnet` image located on [Docker Hub](https://hub.docker.com/r/microsoft/aspnet/).</span></span>
<span data-ttu-id="8db03-151">Základní bitová kopie, `microsoft/aspnet`, je image Windows serveru.</span><span class="sxs-lookup"><span data-stu-id="8db03-151">The base image, `microsoft/aspnet`, is a Windows Server image.</span></span> <span data-ttu-id="8db03-152">Obsahuje Windows Server Core, IIS a ASP.NET 4.7.2.</span><span class="sxs-lookup"><span data-stu-id="8db03-152">It contains Windows Server Core, IIS, and ASP.NET 4.7.2.</span></span> <span data-ttu-id="8db03-153">Když spustíte tuto image ve vašem kontejneru, automaticky se spustí IIS a nainstalují weby.</span><span class="sxs-lookup"><span data-stu-id="8db03-153">When you run this image in your container, it will automatically start IIS and installed websites.</span></span>

<span data-ttu-id="8db03-154">Souboru Dockerfile, který vytváří obrázek, vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="8db03-154">The Dockerfile that creates your image looks like this:</span></span>

```console
# The `FROM` instruction specifies the base image. You are
# extending the `microsoft/aspnet` image.

FROM microsoft/aspnet

# The final instruction copies the site you published earlier into the container.
COPY ./bin/Release/PublishOutput/ /inetpub/wwwroot
```

<span data-ttu-id="8db03-155">V tomto souboru Dockerfile není žádný příkaz `ENTRYPOINT`.</span><span class="sxs-lookup"><span data-stu-id="8db03-155">There is no `ENTRYPOINT` command in this Dockerfile.</span></span> <span data-ttu-id="8db03-156">Žádný nepotřebujete.</span><span class="sxs-lookup"><span data-stu-id="8db03-156">You don't need one.</span></span> <span data-ttu-id="8db03-157">Při spuštění Windows serveru se službou IIS je proces IIS vstupním parametrem, který je nakonfigurovaný tak, aby se spouštěl v základní imagi ASPNET.</span><span class="sxs-lookup"><span data-stu-id="8db03-157">When running Windows Server with IIS, the IIS process is the entrypoint, which is configured to start in the aspnet base image.</span></span>

<span data-ttu-id="8db03-158">Spuštěním příkazu Docker Build vytvořte image, která spustí vaši aplikaci ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="8db03-158">Run the Docker build command to create the image that runs your ASP.NET app.</span></span> <span data-ttu-id="8db03-159">Provedete to tak, že otevřete okno prostředí PowerShell v adresáři projektu a v adresáři řešení zadáte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="8db03-159">To do this, open a PowerShell window in the directory of your project and type the following command in the solution directory:</span></span>

```console
docker build -t mvcrandomanswers .
```

<span data-ttu-id="8db03-160">Tento příkaz sestaví novou image pomocí instrukcí ve vašem souboru Dockerfile, pojmenovávání (-t označení) obrázku jako mvcrandomanswers.</span><span class="sxs-lookup"><span data-stu-id="8db03-160">This command will build the new image using the instructions in your Dockerfile, naming (-t tagging) the image as mvcrandomanswers.</span></span> <span data-ttu-id="8db03-161">To může zahrnovat přijetí základní image z [Docker Hub](http://hub.docker.com)a přidání vaší aplikace do této image.</span><span class="sxs-lookup"><span data-stu-id="8db03-161">This may include pulling the base image from [Docker Hub](http://hub.docker.com), and then adding your app to that image.</span></span>

<span data-ttu-id="8db03-162">Po dokončení tohoto příkazu můžete spustit příkaz `docker images`, abyste viděli informace na nové imagi:</span><span class="sxs-lookup"><span data-stu-id="8db03-162">Once that command completes, you can run the `docker images` command to see information on the new image:</span></span>

```console
REPOSITORY                    TAG                 IMAGE ID            CREATED             SIZE
mvcrandomanswers              latest              86838648aab6        2 minutes ago       10.1 GB
```

<span data-ttu-id="8db03-163">ID IMAGE se na vašem počítači liší.</span><span class="sxs-lookup"><span data-stu-id="8db03-163">The IMAGE ID will be different on your machine.</span></span> <span data-ttu-id="8db03-164">Teď aplikaci spusťte.</span><span class="sxs-lookup"><span data-stu-id="8db03-164">Now, let's run the app.</span></span>

## <a name="start-a-container"></a><span data-ttu-id="8db03-165">Spuštění kontejneru</span><span class="sxs-lookup"><span data-stu-id="8db03-165">Start a container</span></span>

<span data-ttu-id="8db03-166">Spusťte kontejner spuštěním následujícího příkazu `docker run`:</span><span class="sxs-lookup"><span data-stu-id="8db03-166">Start a container by executing the following `docker run` command:</span></span>

```console
docker run -d --name randomanswers mvcrandomanswers
```

<span data-ttu-id="8db03-167">Argument `-d` instruuje Docker, aby spustil obrázek v odpojeném režimu.</span><span class="sxs-lookup"><span data-stu-id="8db03-167">The `-d` argument tells Docker to start the image in detached mode.</span></span> <span data-ttu-id="8db03-168">To znamená, že se image Docker spustí odpojený od aktuálního prostředí.</span><span class="sxs-lookup"><span data-stu-id="8db03-168">That means the Docker image runs disconnected from the current shell.</span></span>

<span data-ttu-id="8db03-169">V mnoha ukázkách Docker se může zobrazit – p pro mapování kontejneru a hostitelských portů.</span><span class="sxs-lookup"><span data-stu-id="8db03-169">In many docker examples, you may see -p to map the container and host ports.</span></span> <span data-ttu-id="8db03-170">Výchozí image ASPNET již nakonfigurovala kontejner pro naslouchání na portu 80 a zpřístupňuje ho.</span><span class="sxs-lookup"><span data-stu-id="8db03-170">The default aspnet image has already configured the container to listen on port 80 and expose it.</span></span>

<span data-ttu-id="8db03-171">`--name randomanswers` poskytuje název ke spuštěnému kontejneru.</span><span class="sxs-lookup"><span data-stu-id="8db03-171">The `--name randomanswers` gives a name to the running container.</span></span> <span data-ttu-id="8db03-172">Ve většině příkazů můžete použít tento název místo ID kontejneru.</span><span class="sxs-lookup"><span data-stu-id="8db03-172">You can use this name instead of the container ID in most commands.</span></span>

<span data-ttu-id="8db03-173">`mvcrandomanswers` je název obrázku, který se má spustit.</span><span class="sxs-lookup"><span data-stu-id="8db03-173">The `mvcrandomanswers` is the name of the image to start.</span></span>

## <a name="verify-in-the-browser"></a><span data-ttu-id="8db03-174">Ověření v prohlížeči</span><span class="sxs-lookup"><span data-stu-id="8db03-174">Verify in the browser</span></span>

<span data-ttu-id="8db03-175">Po spuštění kontejneru se připojte ke spuštěnému kontejneru pomocí `http://localhost` v zobrazeném příkladu.</span><span class="sxs-lookup"><span data-stu-id="8db03-175">Once the container starts, connect to the running container using `http://localhost` in the example shown.</span></span> <span data-ttu-id="8db03-176">Zadejte tuto adresu URL do prohlížeče a měli byste vidět běžící Web.</span><span class="sxs-lookup"><span data-stu-id="8db03-176">Type that URL into your browser, and you should see the running site.</span></span>

> [!NOTE]
> <span data-ttu-id="8db03-177">Některé software VPN nebo proxy serveru vám může bránit v přechodu na váš web.</span><span class="sxs-lookup"><span data-stu-id="8db03-177">Some VPN or proxy software may prevent you from navigating to your site.</span></span>
> <span data-ttu-id="8db03-178">Můžete ho dočasně zakázat, abyste se ujistili, že váš kontejner funguje.</span><span class="sxs-lookup"><span data-stu-id="8db03-178">You can temporarily disable it to make sure your container is working.</span></span>

<span data-ttu-id="8db03-179">Ukázkový adresář na GitHubu obsahuje [skript PowerShellu](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1) , který tyto příkazy spouští za vás.</span><span class="sxs-lookup"><span data-stu-id="8db03-179">The sample directory on GitHub contains a [PowerShell script](https://github.com/dotnet/samples/blob/master/framework/docker/MVCRandomAnswerGenerator/run.ps1) that executes these commands for you.</span></span> <span data-ttu-id="8db03-180">Otevřete okno PowerShellu, změňte adresář na adresář řešení a zadejte:</span><span class="sxs-lookup"><span data-stu-id="8db03-180">Open a PowerShell window, change directory to your solution directory, and type:</span></span>

```console
./run.ps1
```

<span data-ttu-id="8db03-181">Výše uvedený příkaz sestaví image, zobrazí seznam imagí na vašem počítači a spustí kontejner.</span><span class="sxs-lookup"><span data-stu-id="8db03-181">The command above builds the image, displays the list of images on your machine, and starts a container.</span></span>

<span data-ttu-id="8db03-182">Pokud chcete kontejner zastavit, vydejte `docker stop` příkaz:</span><span class="sxs-lookup"><span data-stu-id="8db03-182">To stop your container, issue a `docker stop` command:</span></span>

```console
docker stop randomanswers
```

<span data-ttu-id="8db03-183">Pokud chcete kontejner odebrat, vydejte příkaz `docker rm`:</span><span class="sxs-lookup"><span data-stu-id="8db03-183">To remove the container, issue a `docker rm` command:</span></span>

```console
docker rm randomanswers
```

[windows-container]: media/aspnetmvc/SwitchContainer.png "Přepnout do kontejneru Windows"
[publish-connection]: media/aspnetmvc/PublishConnection.png "Publikovat do systému souborů"
[publish-settings]: media/aspnetmvc/PublishSettings.png "Nastavení publikování"

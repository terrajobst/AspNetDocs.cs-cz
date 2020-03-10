---
uid: aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
title: Povoluje se ověřování Windows v Katana | Microsoft Docs
author: MikeWasson
description: 'Tento článek popisuje, jak v Katana povolit ověřování systému Windows. Týká se to dvou scénářů: použití služby IIS k hostování Katana a použití HttpListener k samoobslužnému hostování kat...'
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 82324ef0-3b75-4f63-a217-76ef4036ec93
msc.legacyurl: /aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
msc.type: authoredcontent
ms.openlocfilehash: 3d81e7e1bf13ab63417378fba0c5ab80213f404b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617178"
---
# <a name="enabling-windows-authentication-in-katana"></a><span data-ttu-id="78148-104">Povolení ověřování systému Windows v sadě Katana</span><span class="sxs-lookup"><span data-stu-id="78148-104">Enabling Windows Authentication in Katana</span></span>

<span data-ttu-id="78148-105">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="78148-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="78148-106">Tento článek popisuje, jak v Katana povolit ověřování systému Windows.</span><span class="sxs-lookup"><span data-stu-id="78148-106">This article shows how to enable Windows Authentication in Katana.</span></span> <span data-ttu-id="78148-107">Zabývá se dvěma scénáři: používání služby IIS k hostování Katana a použití HttpListener k samoobslužnému hostování Katana ve vlastním procesu.</span><span class="sxs-lookup"><span data-stu-id="78148-107">It covers two scenarios: Using IIS to host Katana, and using HttpListener to self-host Katana in a custom process.</span></span> <span data-ttu-id="78148-108">Děkujeme Barryho Dorrans, David Matson a Novák Rossův pro kontrolu tohoto článku.</span><span class="sxs-lookup"><span data-stu-id="78148-108">Thanks to Barry Dorrans, David Matson, and Chris Ross for reviewing this article.</span></span>

<span data-ttu-id="78148-109">Katana je implementace [Owin](http://owin.org/)od Microsoftu, které představuje otevřené webové rozhraní pro .NET.</span><span class="sxs-lookup"><span data-stu-id="78148-109">Katana is Microsoft's implementation of [OWIN](http://owin.org/), the Open Web Interface for .NET.</span></span> <span data-ttu-id="78148-110">Úvod do OWIN a Katana si můžete přečíst [tady](an-overview-of-project-katana.md).</span><span class="sxs-lookup"><span data-stu-id="78148-110">You can read an introduction to OWIN and Katana [here](an-overview-of-project-katana.md).</span></span> <span data-ttu-id="78148-111">Architektura OWIN má několik vrstev:</span><span class="sxs-lookup"><span data-stu-id="78148-111">The OWIN architecture has several layers:</span></span>

- <span data-ttu-id="78148-112">Hostitel: slouží ke správě procesu, ve kterém je spuštěný kanál OWIN.</span><span class="sxs-lookup"><span data-stu-id="78148-112">Host: Manages the process in which the OWIN pipeline runs.</span></span>
- <span data-ttu-id="78148-113">Server: otevře síťový soket a naslouchat žádostem.</span><span class="sxs-lookup"><span data-stu-id="78148-113">Server: Opens a network socket and listens for requests.</span></span>
- <span data-ttu-id="78148-114">Middleware: zpracovává požadavek HTTP a odpověď.</span><span class="sxs-lookup"><span data-stu-id="78148-114">Middleware: Processes the HTTP request and response.</span></span>

<span data-ttu-id="78148-115">Katana v současné době poskytuje dva servery, které podporují integrované ověřování Windows:</span><span class="sxs-lookup"><span data-stu-id="78148-115">Katana currently provides two servers, both of which support Windows Integrated Authentication:</span></span>

- <span data-ttu-id="78148-116">**Microsoft. Owin. Host. SystemWeb**.</span><span class="sxs-lookup"><span data-stu-id="78148-116">**Microsoft.Owin.Host.SystemWeb**.</span></span> <span data-ttu-id="78148-117">Používá službu IIS s kanálem ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="78148-117">Uses IIS with the ASP.NET pipeline.</span></span>
- <span data-ttu-id="78148-118">**Microsoft. Owin. Host. HttpListener**.</span><span class="sxs-lookup"><span data-stu-id="78148-118">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="78148-119">Používá [System .NET. HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx).</span><span class="sxs-lookup"><span data-stu-id="78148-119">Uses [System.Net.HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx).</span></span> <span data-ttu-id="78148-120">Tento server je momentálně výchozí možností při hostování Katana.</span><span class="sxs-lookup"><span data-stu-id="78148-120">This server is currently the default option when self-hosting Katana.</span></span>

> [!NOTE]
> <span data-ttu-id="78148-121">Katana v současné době neposkytuje OWIN middleware pro ověřování systému Windows, protože tato funkce je již na serverech k dispozici.</span><span class="sxs-lookup"><span data-stu-id="78148-121">Katana does not currently provide OWIN middleware for Windows Authentication, because this functionality is already available in the servers.</span></span>

## <a name="windows-authentication-in-iis"></a><span data-ttu-id="78148-122">Ověřování systému Windows ve službě IIS</span><span class="sxs-lookup"><span data-stu-id="78148-122">Windows Authentication in IIS</span></span>

<span data-ttu-id="78148-123">Pomocí Microsoft. Owin. Host. SystemWeb můžete jednoduše povolit ověřování systému Windows ve službě IIS.</span><span class="sxs-lookup"><span data-stu-id="78148-123">Using Microsoft.Owin.Host.SystemWeb, you can simply enable Windows Authentication in IIS.</span></span>

<span data-ttu-id="78148-124">Pojďme začít vytvořením nové aplikace ASP.NET pomocí šablony projektu "prázdná webová aplikace ASP.NET".</span><span class="sxs-lookup"><span data-stu-id="78148-124">Let's start by creating a new ASP.NET application, using the "ASP.NET Empty Web Application" project template.</span></span>

![](enabling-windows-authentication-in-katana/_static/image1.png)

<span data-ttu-id="78148-125">Dále přidejte balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="78148-125">Next, add NuGet packages.</span></span> <span data-ttu-id="78148-126">V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="78148-126">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="78148-127">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="78148-127">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

<span data-ttu-id="78148-128">Nyní přidejte třídu s názvem `Startup` s následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="78148-128">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

<span data-ttu-id="78148-129">To je vše, co potřebujete k vytvoření aplikace "Hello World" pro OWIN, která běží na službě IIS.</span><span class="sxs-lookup"><span data-stu-id="78148-129">That's all you need to create a "Hello world" application for OWIN, running on IIS.</span></span> <span data-ttu-id="78148-130">Pro ladění aplikace stiskněte klávesu F5.</span><span class="sxs-lookup"><span data-stu-id="78148-130">Press F5 to debug the application.</span></span> <span data-ttu-id="78148-131">Měl by se zobrazit "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="78148-131">You should see "Hello World!"</span></span> <span data-ttu-id="78148-132">v okně prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="78148-132">in the browser window.</span></span>

![](enabling-windows-authentication-in-katana/_static/image2.png)

<span data-ttu-id="78148-133">Dále povolíme ověřování systému Windows v IIS Express.</span><span class="sxs-lookup"><span data-stu-id="78148-133">Next, we'll enable Windows Authentication in IIS Express.</span></span> <span data-ttu-id="78148-134">V nabídce **zobrazení** vyberte možnost **vlastnosti**.</span><span class="sxs-lookup"><span data-stu-id="78148-134">From the **View** menu, select **Properties**.</span></span> <span data-ttu-id="78148-135">Kliknutím na název projektu v Průzkumník řešení zobrazíte vlastnosti projektu.</span><span class="sxs-lookup"><span data-stu-id="78148-135">Click on the project name in Solution Explorer to view the project properties.</span></span>

<span data-ttu-id="78148-136">V okně **vlastnosti** nastavte **anonymní ověřování** na **zakázáno** a nastavte **ověřování systému Windows** na **povoleno**.</span><span class="sxs-lookup"><span data-stu-id="78148-136">In the **Properties** window, set **Anonymous Authentication** to **Disabled** and set **Windows Authentication** to **Enabled**.</span></span>

![](enabling-windows-authentication-in-katana/_static/image3.png)

<span data-ttu-id="78148-137">Při spuštění aplikace ze sady Visual Studio bude IIS Express vyžadovat pověření systému Windows uživatele.</span><span class="sxs-lookup"><span data-stu-id="78148-137">When you run the application from Visual Studio, IIS Express will require the user's Windows credentials.</span></span> <span data-ttu-id="78148-138">To můžete zobrazit pomocí [Fiddler](http://fiddler2.com/home) nebo jiného nástroje pro ladění http.</span><span class="sxs-lookup"><span data-stu-id="78148-138">You can see this by using [Fiddler](http://fiddler2.com/home) or another HTTP debugging tool.</span></span> <span data-ttu-id="78148-139">Tady je příklad odpovědi HTTP:</span><span class="sxs-lookup"><span data-stu-id="78148-139">Here is an example HTTP response:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

<span data-ttu-id="78148-140">Hlavičky WWW-Authenticate v této odpovědi označují, že server podporuje protokol [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) , který používá protokol Kerberos nebo NTLM.</span><span class="sxs-lookup"><span data-stu-id="78148-140">The WWW-Authenticate headers in this response indicate that the server supports the [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) protocol, which uses either Kerberos or NTLM.</span></span>

<span data-ttu-id="78148-141">Když později nasadíte aplikaci na server, postupujte podle [těchto kroků](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) a povolte ověřování systému Windows ve službě IIS na daném serveru.</span><span class="sxs-lookup"><span data-stu-id="78148-141">Later, when you deploy the application to a server, follow [these steps](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) to enable Windows Authentication in IIS on that server.</span></span>

## <a name="windows-authentication-in-httplistener"></a><span data-ttu-id="78148-142">Ověřování systému Windows v HttpListener</span><span class="sxs-lookup"><span data-stu-id="78148-142">Windows Authentication in HttpListener</span></span>

<span data-ttu-id="78148-143">Pokud používáte Microsoft. Owin. Host. HttpListener k samoobslužnému hostování Katana, můžete povolit ověřování systému Windows přímo v instanci **HttpListener** .</span><span class="sxs-lookup"><span data-stu-id="78148-143">If you are using Microsoft.Owin.Host.HttpListener to self-host Katana, you can enable Windows Authentication directly on the **HttpListener** instance.</span></span>

<span data-ttu-id="78148-144">Nejprve vytvořte novou konzolovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="78148-144">First, create a new console application.</span></span> <span data-ttu-id="78148-145">Dále přidejte balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="78148-145">Next, add NuGet packages.</span></span> <span data-ttu-id="78148-146">V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="78148-146">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="78148-147">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="78148-147">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

<span data-ttu-id="78148-148">Nyní přidejte třídu s názvem `Startup` s následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="78148-148">Now add a class named `Startup` with the following code:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

<span data-ttu-id="78148-149">Tato třída implementuje stejný příklad "Hello World" z dřív, ale také nastaví ověřování systému Windows jako schéma ověřování.</span><span class="sxs-lookup"><span data-stu-id="78148-149">This class implements the same "Hello world" example from before, but it also sets Windows Authentication as the authentication scheme.</span></span>

<span data-ttu-id="78148-150">Uvnitř funkce `Main` spusťte kanál OWIN:</span><span class="sxs-lookup"><span data-stu-id="78148-150">Inside the `Main` function, start the OWIN pipeline:</span></span>

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

<span data-ttu-id="78148-151">V Fiddler můžete odeslat žádost o potvrzení, že aplikace používá ověřování systému Windows:</span><span class="sxs-lookup"><span data-stu-id="78148-151">You can send a request in Fiddler to confirm that the application is using Windows Authentication:</span></span>

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a><span data-ttu-id="78148-152">Související témata</span><span class="sxs-lookup"><span data-stu-id="78148-152">Related Topics</span></span>

[<span data-ttu-id="78148-153">Přehled projektu Katana</span><span class="sxs-lookup"><span data-stu-id="78148-153">An Overview of Project Katana</span></span>](an-overview-of-project-katana.md)

[<span data-ttu-id="78148-154">System .NET. HttpListener</span><span class="sxs-lookup"><span data-stu-id="78148-154">System.Net.HttpListener</span></span>](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[<span data-ttu-id="78148-155">Principy ověřování OWIN Forms v MVC 5</span><span class="sxs-lookup"><span data-stu-id="78148-155">Understanding OWIN Forms Authentication in MVC 5</span></span>](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)

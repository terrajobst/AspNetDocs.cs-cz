---
uid: visual-studio/overview/2013/release-notes
title: ASP.NET and Web Tools pro Visual Studio 2013 poznámky k verzi | Microsoft Docs
author: microsoft
description: Tento dokument popisuje vydání ASP.NET and Web Tools pro Visual Studio 2013.
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 08815768-2702-42ae-ae85-0a59934a11d1
msc.legacyurl: /visual-studio/overview/2013/release-notes
msc.type: authoredcontent
ms.openlocfilehash: d8af9c8e7ee1316a5eac90c5959d07c628154e09
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600441"
---
# <a name="aspnet-and-web-tools-for-visual-studio-2013-release-notes"></a><span data-ttu-id="4300c-103">ASP.NET a webové nástroje pro Visual Studio 2013 – poznámky k verzi</span><span class="sxs-lookup"><span data-stu-id="4300c-103">ASP.NET and Web Tools for Visual Studio 2013 Release Notes</span></span>

<span data-ttu-id="4300c-104">od [Microsoftu](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="4300c-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="4300c-105">Tento dokument popisuje vydání ASP.NET and Web Tools pro Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="4300c-105">This document describes the release of ASP.NET and Web Tools for Visual Studio 2013.</span></span>

## <a name="contents"></a><span data-ttu-id="4300c-106">Obsah</span><span class="sxs-lookup"><span data-stu-id="4300c-106">Contents</span></span>

- [<span data-ttu-id="4300c-107">Poznámky k instalaci</span><span class="sxs-lookup"><span data-stu-id="4300c-107">Installation Notes</span></span>](#TOC1)
- [<span data-ttu-id="4300c-108">Dokumentace</span><span class="sxs-lookup"><span data-stu-id="4300c-108">Documentation</span></span>](#TOC2)
- [<span data-ttu-id="4300c-109">Požadavky na software</span><span class="sxs-lookup"><span data-stu-id="4300c-109">Software Requirements</span></span>](#TOC4)

### <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="4300c-110">Nové funkce v ASP.NET and Web Tools pro Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="4300c-110">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

- [<span data-ttu-id="4300c-111">Jeden ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4300c-111">One ASP.NET</span></span>](#TOC6)
- [<span data-ttu-id="4300c-112">Nové prostředí webového projektu</span><span class="sxs-lookup"><span data-stu-id="4300c-112">New Web Project Experience</span></span>](#newproj)
- [<span data-ttu-id="4300c-113">ASP.NET generování uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="4300c-113">ASP.NET Scaffolding</span></span>](#scaffold)
- [<span data-ttu-id="4300c-114">Browser Link</span><span class="sxs-lookup"><span data-stu-id="4300c-114">Browser Link</span></span>](#browser-link)
- [<span data-ttu-id="4300c-115">Vylepšení webového editoru sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4300c-115">Visual Studio Web Editor Enhancements</span></span>](#web-editor)
- [<span data-ttu-id="4300c-116">Podpora Azure App Service Web Apps v aplikaci Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4300c-116">Azure App Service Web Apps Support in Visual Studio</span></span>](#waws)
- [<span data-ttu-id="4300c-117">Vylepšení publikování na webu</span><span class="sxs-lookup"><span data-stu-id="4300c-117">Web Publish Enhancements</span></span>](#publish)
- [<span data-ttu-id="4300c-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="4300c-118">NuGet 2.7</span></span>](#nuget)
- [<span data-ttu-id="4300c-119">Webové formuláře ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4300c-119">ASP.NET Web Forms</span></span>](#TOC9)
- [<span data-ttu-id="4300c-120">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="4300c-120">ASP.NET MVC 5</span></span>](#TOC10)
- [<span data-ttu-id="4300c-121">Webové rozhraní API 2 ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4300c-121">ASP.NET Web API 2</span></span>](#TOC11)
- [<span data-ttu-id="4300c-122">ASP.NET signál</span><span class="sxs-lookup"><span data-stu-id="4300c-122">ASP.NET SignalR</span></span>](#TOC13)
- [<span data-ttu-id="4300c-123">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="4300c-123">ASP.NET Identity</span></span>](#TOC8)
- [<span data-ttu-id="4300c-124">Komponenty Microsoft OWIN</span><span class="sxs-lookup"><span data-stu-id="4300c-124">Microsoft OWIN Components</span></span>](#TOC7)
- [<span data-ttu-id="4300c-125">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="4300c-125">Entity Framework 6</span></span>](#ef6)
- [<span data-ttu-id="4300c-126">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="4300c-126">ASP.NET Razor 3</span></span>](#TOC14)
- [<span data-ttu-id="4300c-127">Pozastavení aplikace ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4300c-127">ASP.NET App Suspend</span></span>](#TOC15)
- [<span data-ttu-id="4300c-128">Známé problémy a zásadní změny</span><span class="sxs-lookup"><span data-stu-id="4300c-128">Known Issues and Breaking Changes</span></span>](#knownissues)

<a id="TOC1"></a>
## <a name="installation-notes"></a><span data-ttu-id="4300c-129">Poznámky k instalaci</span><span class="sxs-lookup"><span data-stu-id="4300c-129">Installation Notes</span></span>

<span data-ttu-id="4300c-130">ASP.NET and Web Tools pro Visual Studio 2013 jsou v hlavním instalačním programu rozčleněné a dají se stáhnout [tady](https://www.asp.net/downloads).</span><span class="sxs-lookup"><span data-stu-id="4300c-130">ASP.NET and Web Tools for Visual Studio 2013 are bundled in the main installer and can be downloaded [here](https://www.asp.net/downloads).</span></span>

<a id="TOC2"></a>
## <a name="documentation"></a><span data-ttu-id="4300c-131">Dokumentace</span><span class="sxs-lookup"><span data-stu-id="4300c-131">Documentation</span></span>

<span data-ttu-id="4300c-132">Kurzy a další informace o ASP.NET and Web Tools pro Visual Studio 2013 jsou k dispozici na webu [ASP.NET](https://www.asp.net/).</span><span class="sxs-lookup"><span data-stu-id="4300c-132">Tutorials and other information about ASP.NET and Web Tools for Visual Studio 2013 are available from the [ASP.NET web site](https://www.asp.net/).</span></span>

<a id="TOC4"></a>
## <a name="software-requirements"></a><span data-ttu-id="4300c-133">Požadavky na software</span><span class="sxs-lookup"><span data-stu-id="4300c-133">Software Requirements</span></span>

<span data-ttu-id="4300c-134">ASP.NET and Web Tools vyžaduje Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="4300c-134">ASP.NET and Web Tools requires Visual Studio 2013.</span></span>

<a id="TOC5"></a>
## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-2013"></a><span data-ttu-id="4300c-135">Nové funkce v ASP.NET and Web Tools pro Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="4300c-135">New Features in ASP.NET and Web Tools for Visual Studio 2013</span></span>

<span data-ttu-id="4300c-136">V následujících částech jsou popsány funkce, které byly představeny v této verzi.</span><span class="sxs-lookup"><span data-stu-id="4300c-136">The following sections describe the features that have been introduced in the release.</span></span>

<a id="TOC6"></a>
## <a name="one-aspnet"></a><span data-ttu-id="4300c-137">Jeden ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4300c-137">One ASP.NET</span></span>

<span data-ttu-id="4300c-138">S vydáním Visual Studio 2013 jsme udělali krok k sjednocení zkušeností s používáním technologií ASP.NET, abyste mohli snadno kombinovat a porovnat ty, které chcete.</span><span class="sxs-lookup"><span data-stu-id="4300c-138">With the release of Visual Studio 2013, we have taken a step towards unifying the experience of using ASP.NET technologies, so that you can easily mix and match the ones you want.</span></span> <span data-ttu-id="4300c-139">Můžete například spustit projekt pomocí MVC a snadno přidat stránky webových formulářů do projektu, nebo webové rozhraní API pro generování uživatelského rozhraní v projektu webových formulářů.</span><span class="sxs-lookup"><span data-stu-id="4300c-139">For example, you can start a project using MVC and easily add Web Forms pages to the project later, or scaffold Web APIs in a Web Forms project.</span></span> <span data-ttu-id="4300c-140">Jeden ASP.NET je vše, co usnadňuje vývojářům práci v ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4300c-140">One ASP.NET is all about making it easier for you as a developer to do the things you love in ASP.NET.</span></span> <span data-ttu-id="4300c-141">Bez ohledu na to, jakou technologii si zvolíte, můžete mít jistotu, že sestavíte na důvěryhodném základním rozhraní jednoho ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4300c-141">No matter what technology you choose, you can have confidence that you are building on the trusted underlying framework of One ASP.NET.</span></span>

<a id="newproj"></a>
## <a name="new-web-project-experience"></a><span data-ttu-id="4300c-142">Nové prostředí webového projektu</span><span class="sxs-lookup"><span data-stu-id="4300c-142">New Web Project Experience</span></span>

<span data-ttu-id="4300c-143">Vylepšili jsme možnosti vytváření nových webových projektů v Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="4300c-143">We have enhanced the experience of creating new web projects in Visual Studio 2013.</span></span> <span data-ttu-id="4300c-144">V dialogovém okně **Nový webový projekt ASP.NET** můžete vybrat požadovaný typ projektu, nakonfigurovat libovolnou kombinaci technologií (webové formuláře, MVC, webové rozhraní API), nakonfigurovat možnosti ověřování a přidat projekt testu jednotek.</span><span class="sxs-lookup"><span data-stu-id="4300c-144">In the **New ASP.NET Web Project** dialog you can select the project type you want, configure any combination of technologies (Web Forms, MVC, Web API), configure authentication options, and add a unit test project.</span></span>

![Nový projekt ASP.NET](release-notes/_static/image1.png)

<span data-ttu-id="4300c-146">Nové dialogové okno umožňuje změnit výchozí možnosti ověřování pro mnoho šablon.</span><span class="sxs-lookup"><span data-stu-id="4300c-146">The new dialog enables you to change the default authentication options for many of the templates.</span></span> <span data-ttu-id="4300c-147">Například při vytváření projektu webových formulářů ASP.NET můžete vybrat některou z následujících možností:</span><span class="sxs-lookup"><span data-stu-id="4300c-147">For example, when you create an ASP.NET Web Forms project you can select any of the following options:</span></span>

- <span data-ttu-id="4300c-148">Bez ověřování</span><span class="sxs-lookup"><span data-stu-id="4300c-148">No Authentication</span></span>
- <span data-ttu-id="4300c-149">Individuální uživatelské účty (členství v ASP.NET nebo přihlašování k poskytovateli sociálních sítí)</span><span class="sxs-lookup"><span data-stu-id="4300c-149">Individual User Accounts (ASP.NET membership or social provider log in)</span></span>
- <span data-ttu-id="4300c-150">Účty organizace (Active Directory v internetové aplikaci)</span><span class="sxs-lookup"><span data-stu-id="4300c-150">Organizational Accounts (Active Directory in an internet application)</span></span>
- <span data-ttu-id="4300c-151">Ověřování systému Windows (služba Active Directory v intranetové aplikaci)</span><span class="sxs-lookup"><span data-stu-id="4300c-151">Windows Authentication (Active Directory in an intranet application)</span></span>

![Možnosti ověřování](release-notes/_static/image2.png)

<span data-ttu-id="4300c-153">Další informace o novém procesu pro vytváření webových projektů naleznete [v tématu creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="4300c-153">For more information about the new process for creating web projects, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span> <span data-ttu-id="4300c-154">Další informace o nových možnostech ověřování najdete v tématu [ASP.NET identity](#TOC8) dále v tomto dokumentu.</span><span class="sxs-lookup"><span data-stu-id="4300c-154">For more information about the new authentication options, see [ASP.NET Identity](#TOC8) later in this document.</span></span>

<a id="scaffold"></a>
## <a name="aspnet-scaffolding"></a><span data-ttu-id="4300c-155">ASP.NET generování uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="4300c-155">ASP.NET Scaffolding</span></span>

<span data-ttu-id="4300c-156">Generování uživatelského rozhraní ASP.NET je rozhraní pro generování kódu pro webové aplikace v ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4300c-156">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="4300c-157">Umožňuje snadno přidat do projektu často používaný kód, který komunikuje s datovým modelem.</span><span class="sxs-lookup"><span data-stu-id="4300c-157">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="4300c-158">V předchozích verzích sady Visual Studio bylo generování uživatelského rozhraní omezeno na ASP.NET projekty MVC.</span><span class="sxs-lookup"><span data-stu-id="4300c-158">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="4300c-159">Pomocí Visual Studio 2013 můžete nyní použít generování uživatelského rozhraní pro libovolný projekt ASP.NET, včetně webových formulářů.</span><span class="sxs-lookup"><span data-stu-id="4300c-159">With Visual Studio 2013, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="4300c-160">Visual Studio 2013 aktuálně nepodporuje generování stránek pro projekt webových formulářů, ale můžete i nadále používat generování uživatelského rozhraní s webovými formuláři přidáním závislostí MVC do projektu.</span><span class="sxs-lookup"><span data-stu-id="4300c-160">Visual Studio 2013 does not currently support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="4300c-161">Do budoucí aktualizace se přidají podpora pro generování stránek webových formulářů.</span><span class="sxs-lookup"><span data-stu-id="4300c-161">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="4300c-162">Při použití generování uživatelského rozhraní zajišťujeme, aby byly v projektu nainstalované všechny požadované závislosti.</span><span class="sxs-lookup"><span data-stu-id="4300c-162">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="4300c-163">Například pokud začnete s projektem ASP.NET Web Forms a potom použijete generování uživatelského rozhraní pro přidání kontroleru webového rozhraní API, požadované balíčky NuGet a odkazy se automaticky přidají do projektu.</span><span class="sxs-lookup"><span data-stu-id="4300c-163">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="4300c-164">Chcete-li přidat generování uživatelského rozhraní MVC do projektu webových formulářů, přidejte **novou vygenerované položky** a v dialogovém okně vyberte **závislosti MVC 5** .</span><span class="sxs-lookup"><span data-stu-id="4300c-164">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="4300c-165">K dispozici jsou dvě možnosti pro generování uživatelského rozhraní MVC; Minimální a plná.</span><span class="sxs-lookup"><span data-stu-id="4300c-165">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="4300c-166">Pokud vyberete minimální, do projektu se přidají jenom balíčky NuGet a odkazy pro ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="4300c-166">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="4300c-167">Pokud vyberete možnost úplná, budou přidány minimální závislosti a také požadované soubory obsahu pro projekt MVC.</span><span class="sxs-lookup"><span data-stu-id="4300c-167">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="4300c-168">Podpora pro generování generovaných asynchronních řadičů používá nové asynchronní funkce z Entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="4300c-168">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="4300c-169">Další informace a kurzy najdete v tématu [Přehled generování uživatelského rozhraní ASP.NET](aspnet-scaffolding-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4300c-169">For more information and tutorials, see [ASP.NET Scaffolding Overview](aspnet-scaffolding-overview.md).</span></span>

<a id="browser-link"></a>
## <a name="browser-link--signalr-channel-between-browser-and-visual-studio"></a><span data-ttu-id="4300c-170">Odkaz na prohlížeč – kanál signálu mezi prohlížečem a Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4300c-170">Browser Link – SignalR channel between browser and Visual Studio</span></span>

<span data-ttu-id="4300c-171">Nová funkce [odkaz v prohlížeči](using-browser-link.md) umožňuje připojit více prohlížečů k sadě Visual Studio a aktualizovat je všechny kliknutím na tlačítko na panelu nástrojů.</span><span class="sxs-lookup"><span data-stu-id="4300c-171">The new [Browser Link](using-browser-link.md) feature lets you connect multiple browsers to Visual Studio and refresh them all by clicking a button in the toolbar.</span></span> <span data-ttu-id="4300c-172">Můžete připojit více prohlížečů k vašemu vývojovému webu, včetně emulátorů pro mobilní zařízení, a kliknutím na aktualizovat aktualizovat všechny prohlížeče současně.</span><span class="sxs-lookup"><span data-stu-id="4300c-172">You can connect multiple browsers to your development site, including mobile emulators, and click refresh to refresh all the browsers all at the same time.</span></span> <span data-ttu-id="4300c-173">Odkaz na prohlížeč také zpřístupňuje rozhraní API, které vývojářům umožňuje psát rozšíření Browser Link Extensions.</span><span class="sxs-lookup"><span data-stu-id="4300c-173">Browser Link also exposes an API to enable developers to write Browser Link extensions.</span></span>

![](release-notes/_static/image3.png)

<span data-ttu-id="4300c-174">Tím, že vývojářům umožní využít rozhraní API pro připojení k prohlížeči, je možné vytvořit velmi pokročilé scénáře, které překračují hranice mezi Visual Studio a jakýmkoli připojeným prohlížečem.</span><span class="sxs-lookup"><span data-stu-id="4300c-174">By enabling developers to take advantage of the Browser Link API, it becomes possible to create very advanced scenarios that crosses boundaries between Visual Studio and any browser that's connected.</span></span> <span data-ttu-id="4300c-175">Web Essentials využívá rozhraní API k vytvoření integrovaného prostředí mezi Visual Studio a vývojářskými nástroji v prohlížeči, vzdáleného řízení emulátorů pro mobilní zařízení a další spoustou.</span><span class="sxs-lookup"><span data-stu-id="4300c-175">Web Essentials takes advantage of the API to create an integrated experience between Visual Studio and the browser's developer tools, remote controlling mobile emulators and a lot more.</span></span>

<a id="web-editor"></a>
## <a name="visual-studio-web-editor-enhancements"></a><span data-ttu-id="4300c-176">Vylepšení webového editoru sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4300c-176">Visual Studio Web Editor Enhancements</span></span>

<span data-ttu-id="4300c-177">Visual Studio 2013 obsahuje nový editor HTML pro soubory Razor a soubory HTML ve webových aplikacích.</span><span class="sxs-lookup"><span data-stu-id="4300c-177">Visual Studio 2013 includes a new HTML editor for Razor files and HTML files in web applications.</span></span> <span data-ttu-id="4300c-178">Nový editor HTML poskytuje jedno sjednocené schéma založené na HTML5.</span><span class="sxs-lookup"><span data-stu-id="4300c-178">The new HTML editor provides a single unified schema based on HTML5.</span></span> <span data-ttu-id="4300c-179">Má automatické dokončování složených závorek, uživatelské rozhraní jQuery a atribut AngularJS pro technologii IntelliSense, atributy seskupování IntelliSense, ID a název třídy IntelliSense a další vylepšení, včetně lepšího výkonu, formátování a inteligentních operací.</span><span class="sxs-lookup"><span data-stu-id="4300c-179">It has automatic brace completion, jQuery UI and AngularJS attribute IntelliSense, attribute IntelliSense Grouping, ID and class name Intellisense, and other improvements including better performance, formatting and SmartTags.</span></span>

<span data-ttu-id="4300c-180">Následující snímek obrazovky ukazuje použití funkce Bootstrap atributu IntelliSense v editoru HTML.</span><span class="sxs-lookup"><span data-stu-id="4300c-180">The following screenshot demonstrates using Bootstrap attribute IntelliSense in the HTML editor.</span></span>

![IntelliSense v editoru HTML](release-notes/_static/image4.png)

<span data-ttu-id="4300c-182">Visual Studio 2013 také přináší CoffeeScript i méně editorů.</span><span class="sxs-lookup"><span data-stu-id="4300c-182">Visual Studio 2013 also comes with both CoffeeScript and LESS editors built in.</span></span> <span data-ttu-id="4300c-183">Editor LESS se dodává se všemi studenými funkcemi z editoru šablon stylů CSS a má konkrétní IntelliSense pro proměnné a objekty Mixin napříč všemi méně dokumenty v řetězci @import.</span><span class="sxs-lookup"><span data-stu-id="4300c-183">The LESS editor comes with all the cool features from the CSS editor and has specific Intellisense for variables and mixins across all the LESS documents in the @import chain.</span></span>

<a id="waws"></a>
## <a name="azure-app-service-web-apps-support-in-visual-studio"></a><span data-ttu-id="4300c-184">Podpora Azure App Service Web Apps v aplikaci Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4300c-184">Azure App Service Web Apps Support in Visual Studio</span></span>

<span data-ttu-id="4300c-185">V Visual Studio 2013 se sadou Azure SDK pro .NET 2,2 můžete pomocí **Průzkumník serveru** komunikovat přímo se vzdálenými webovými aplikacemi.</span><span class="sxs-lookup"><span data-stu-id="4300c-185">In Visual Studio 2013 with the Azure SDK for .NET 2.2, you can use **Server Explorer** to interact directly with your remote web apps.</span></span> <span data-ttu-id="4300c-186">Můžete se přihlásit ke svému účtu Azure, vytvářet nové webové aplikace, konfigurovat aplikace, zobrazovat protokoly v reálném čase a další.</span><span class="sxs-lookup"><span data-stu-id="4300c-186">You can sign in to your Azure account, create new web apps, configure apps, view real-time logs, and more.</span></span> <span data-ttu-id="4300c-187">Po vydání sady SDK 2,2 budete moci spustit v režimu ladění vzdáleně v Azure.</span><span class="sxs-lookup"><span data-stu-id="4300c-187">Coming soon after SDK 2.2 is released, you'll be able to run in debug mode remotely in Azure.</span></span> <span data-ttu-id="4300c-188">Většina nových funkcí pro Azure App Service Web Apps v sadě Visual Studio 2012 funguje i při instalaci aktuální verze sady Azure SDK pro .NET.</span><span class="sxs-lookup"><span data-stu-id="4300c-188">Most of the new features for Azure App Service Web Apps also work in Visual Studio 2012 when you install the current release of the Azure SDK for .NET.</span></span>

<span data-ttu-id="4300c-189">Další informace naleznete v následujících zdrojích:</span><span class="sxs-lookup"><span data-stu-id="4300c-189">For more information, see the following resources:</span></span>

- [<span data-ttu-id="4300c-190">Vytvoření webové aplikace v ASP.NET v Azure App Service</span><span class="sxs-lookup"><span data-stu-id="4300c-190">Create an ASP.NET web app in Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)
- [<span data-ttu-id="4300c-191">Řešení potíží s webovou aplikací v Azure App Service pomocí sady Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4300c-191">Troubleshoot a web app in Azure App Service using Visual Studio</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)

<a id="publish"></a>
## <a name="web-publish-enhancements"></a><span data-ttu-id="4300c-192">Vylepšení publikování na webu</span><span class="sxs-lookup"><span data-stu-id="4300c-192">Web Publish Enhancements</span></span>

<span data-ttu-id="4300c-193">Visual Studio 2013 zahrnují nové a vylepšené funkce publikování na webu.</span><span class="sxs-lookup"><span data-stu-id="4300c-193">Visual Studio 2013 includes new and enhanced Web Publish features.</span></span> <span data-ttu-id="4300c-194">Tady je několik z nich:</span><span class="sxs-lookup"><span data-stu-id="4300c-194">Here are a few of them:</span></span>

- <span data-ttu-id="4300c-195">Snadné [Automatické automatizace šifrování souborů Web. config](https://go.microsoft.com/fwlink/?LinkId=325529).</span><span class="sxs-lookup"><span data-stu-id="4300c-195">Easily [automate Web.config file encryption](https://go.microsoft.com/fwlink/?LinkId=325529).</span></span> <span data-ttu-id="4300c-196">(Tento odkaz a následující dva body dokumentaci na webu MSDN, které nemusí být k dispozici, dokud neuplyne pozdě v den 10/17.)</span><span class="sxs-lookup"><span data-stu-id="4300c-196">(This link and the following two point to documentation on MSDN that might not be available until late in the day on 10/17.)</span></span>
- <span data-ttu-id="4300c-197">Snadná [automatizace při nasazení aplikace v režimu offline](https://go.microsoft.com/fwlink/?LinkId=325530).</span><span class="sxs-lookup"><span data-stu-id="4300c-197">Easily [automate taking an application offline during deployment](https://go.microsoft.com/fwlink/?LinkId=325530).</span></span>
- <span data-ttu-id="4300c-198">Nakonfigurujte Nasazení webu pro [použití kontrolního součtu souborů namísto data poslední změny](https://go.microsoft.com/fwlink/?LinkId=325531) pro určení, které soubory se mají zkopírovat na server.</span><span class="sxs-lookup"><span data-stu-id="4300c-198">Configure Web Deploy to [use file checksum instead of last-changed date](https://go.microsoft.com/fwlink/?LinkId=325531) for determining which files should be copied to the server.</span></span>
- <span data-ttu-id="4300c-199">Jednotlivé vybrané soubory (včetně souboru Web. config) můžete rychle publikovat při použití metod pro publikování FTP nebo systému souborů a také pomocí Nasazení webu.</span><span class="sxs-lookup"><span data-stu-id="4300c-199">Quickly publish individual selected files (including Web.config) when you're using the FTP or file system publish methods as well as with Web Deploy.</span></span>

<span data-ttu-id="4300c-200">Další informace o nasazení webu ASP.NET najdete [na webu ASP.NET](https://go.microsoft.com/fwlink/?LinkId=322027).</span><span class="sxs-lookup"><span data-stu-id="4300c-200">For more information about ASP.NET web deployment, see [the ASP.NET site](https://go.microsoft.com/fwlink/?LinkId=322027).</span></span>

<a id="nuget"></a>
## <a name="nuget-27"></a><span data-ttu-id="4300c-201">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="4300c-201">NuGet 2.7</span></span>

<span data-ttu-id="4300c-202">NuGet 2,7 obsahuje bohatou sadu nových funkcí, které jsou podrobně popsány v [poznámkách k verzi nuget 2,7](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span><span class="sxs-lookup"><span data-stu-id="4300c-202">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="4300c-203">Tato verze NuGet také odstraňuje nutnost poskytnout explicitní souhlas funkce obnovení balíčku NuGet pro stažení balíčků.</span><span class="sxs-lookup"><span data-stu-id="4300c-203">This version of NuGet also removes the need to provide explicit consent for NuGet's package restore feature to download packages.</span></span> <span data-ttu-id="4300c-204">Souhlas (a související zaškrtávací políčko v dialogovém okně Předvolby NuGet) je teď udělené instalací NuGet.</span><span class="sxs-lookup"><span data-stu-id="4300c-204">Consent (and the associated checkbox in NuGet's preferences dialog) is now granted by installing NuGet.</span></span> <span data-ttu-id="4300c-205">Nově funguje i obnovení balíčků ve výchozím nastavení.</span><span class="sxs-lookup"><span data-stu-id="4300c-205">Now package restore simply works by default.</span></span>

<a id="TOC9"></a>
## <a name="aspnet-web-forms"></a><span data-ttu-id="4300c-206">ASP.NET – webové formuláře</span><span class="sxs-lookup"><span data-stu-id="4300c-206">ASP.NET Web Forms</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="4300c-207">Jeden ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4300c-207">One ASP.NET</span></span>

<span data-ttu-id="4300c-208">Šablony projektů webových formulářů se hladce integrují s novým jedním ASP.NETm prostředím.</span><span class="sxs-lookup"><span data-stu-id="4300c-208">The Web Forms project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="4300c-209">Do projektu webových formulářů můžete přidat podporu MVC a webového rozhraní API a ověřování můžete nakonfigurovat pomocí jednoho Průvodce vytvořením projektu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4300c-209">You can add MVC and Web API support to your Web Forms project, and you can configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="4300c-210">Další informace najdete v tématu [vytváření ASP.NET webových projektů v Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="4300c-210">For more information, see [Creating ASP.NET Web Projects in Visual Studio 2013](creating-web-projects-in-visual-studio.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="4300c-211">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="4300c-211">ASP.NET Identity</span></span>

<span data-ttu-id="4300c-212">Šablony projektů webových formulářů podporují novou ASP.NET Identity Framework.</span><span class="sxs-lookup"><span data-stu-id="4300c-212">The Web Forms project templates support the new ASP.NET Identity framework.</span></span> <span data-ttu-id="4300c-213">Šablony teď podporují vytváření projektu v intranetu webových formulářů.</span><span class="sxs-lookup"><span data-stu-id="4300c-213">In addition, the templates now support creation of a Web Forms intranet project.</span></span> <span data-ttu-id="4300c-214">Další informace najdete v tématu [metody ověřování](creating-web-projects-in-visual-studio.md#auth) při **vytváření ASP.NET webových projektů v Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="4300c-214">For more information, see [Authentication Methods](creating-web-projects-in-visual-studio.md#auth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="bootstrap"></a><span data-ttu-id="4300c-215">Spouštěcí rutina</span><span class="sxs-lookup"><span data-stu-id="4300c-215">Bootstrap</span></span>

<span data-ttu-id="4300c-216">Šablony webových formulářů používají [bootstrap](http://twitter.github.io/bootstrap/) k zajištění elegantního a reakce na vzhled a chování, které lze snadno přizpůsobit.</span><span class="sxs-lookup"><span data-stu-id="4300c-216">The Web Forms templates use [Bootstrap](http://twitter.github.io/bootstrap/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="4300c-217">Další informace naleznete v tématu [bootstrap v šablonách webového projektu Visual Studio 2013](creating-web-projects-in-visual-studio.md#bootstrap).</span><span class="sxs-lookup"><span data-stu-id="4300c-217">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

<a id="TOC10"></a>
## <a name="aspnet-mvc-5"></a><span data-ttu-id="4300c-218">ASP.NET MVC 5</span><span class="sxs-lookup"><span data-stu-id="4300c-218">ASP.NET MVC 5</span></span>

### <a name="one-aspnet"></a><span data-ttu-id="4300c-219">Jeden ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4300c-219">One ASP.NET</span></span>

<span data-ttu-id="4300c-220">Šablony projektů webové MVC se hladce integrují s novým ASP.NET prostředím.</span><span class="sxs-lookup"><span data-stu-id="4300c-220">The Web MVC project templates integrate seamlessly with the new One ASP.NET experience.</span></span> <span data-ttu-id="4300c-221">Můžete přizpůsobit projekt MVC a nakonfigurovat ověřování pomocí jednoho Průvodce vytvořením projektu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4300c-221">You can customize your MVC project and configure authentication using the One ASP.NET project creation wizard.</span></span> <span data-ttu-id="4300c-222">Úvodní kurz k ASP.NET MVC 5 najdete na adrese [Začínáme s ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="4300c-222">An introductory tutorial to ASP.NET MVC 5 can be found at [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="4300c-223">Informace o tom, jak upgradovat projekty MVC 4 na MVC 5, najdete v tématu [Postup upgradu ASP.NET MVC 4 a projektu webového rozhraní API na ASP.NET MVC 5 a webové rozhraní API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="4300c-223">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>

### <a name="aspnet-identity"></a><span data-ttu-id="4300c-224">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="4300c-224">ASP.NET Identity</span></span>

<span data-ttu-id="4300c-225">Šablony projektů MVC byly aktualizovány, aby používaly ASP.NET Identity pro ověřování a správu identit.</span><span class="sxs-lookup"><span data-stu-id="4300c-225">The MVC project templates have been updated to use ASP.NET Identity for authentication and identity management.</span></span> <span data-ttu-id="4300c-226">Kurz týkající se webu Facebook a ověřování Google a nového rozhraní API pro členství najdete v části [Vytvoření aplikace ASP.NET MVC 5 s aplikacemi Facebook a Google OAuth2 a OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) a [vytvoření aplikace pro ASP.NET MVC s ověřováním a SQL DB a nasazením do Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="4300c-226">A tutorial featuring Facebook and Google authentication and the new membership API can be found at [Create an ASP.NET MVC 5 App with Facebook and Google OAuth2 and OpenID Sign-on](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md) and [Create an ASP.NET MVC app with auth and SQL DB and deploy to Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/).</span></span>

### <a name="bootstrap"></a><span data-ttu-id="4300c-227">Spouštěcí rutina</span><span class="sxs-lookup"><span data-stu-id="4300c-227">Bootstrap</span></span>

<span data-ttu-id="4300c-228">Šablona projektu MVC byla aktualizována tak, aby používala [bootstrap](http://getbootstrap.com/) , aby poskytovala elegantní a reagující vzhled a dojem, že je možné snadno přizpůsobit.</span><span class="sxs-lookup"><span data-stu-id="4300c-228">The MVC project template has been updated to use [Bootstrap](http://getbootstrap.com/) to provide a sleek and responsive look and feel that you can easily customize.</span></span> <span data-ttu-id="4300c-229">Další informace naleznete v tématu [bootstrap v šablonách webového projektu Visual Studio 2013](creating-web-projects-in-visual-studio.md#bootstrap).</span><span class="sxs-lookup"><span data-stu-id="4300c-229">For more information, see [Bootstrap in the Visual Studio 2013 web project templates](creating-web-projects-in-visual-studio.md#bootstrap).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="4300c-230">Filtry ověřování</span><span class="sxs-lookup"><span data-stu-id="4300c-230">Authentication filters</span></span>

<span data-ttu-id="4300c-231">Filtry ověřování jsou novým druhem filtru v ASP.NET MVC, který se spouští před autorizačními filtry v kanálu služby ASP.NET MVC, a umožňuje pro všechny řadiče zadat logiku ověřování pro jednotlivé akce, řadiče nebo globálně.</span><span class="sxs-lookup"><span data-stu-id="4300c-231">Authentication filters are a new kind of filter in ASP.NET MVC that run prior to authorization filters in the ASP.NET MVC pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="4300c-232">Ověřovací filtry zpracovávají přihlašovací údaje v žádosti a poskytují odpovídající objekt zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="4300c-232">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="4300c-233">Ověřovací filtry mohou také přidat výzvy ověřování v reakci na neautorizované žádosti.</span><span class="sxs-lookup"><span data-stu-id="4300c-233">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="4300c-234">Přepsání filtru</span><span class="sxs-lookup"><span data-stu-id="4300c-234">Filter overrides</span></span>

<span data-ttu-id="4300c-235">Nyní můžete přepsat, které filtry se vztahují na danou metodu akce nebo kontroler zadáním filtru pro přepsání.</span><span class="sxs-lookup"><span data-stu-id="4300c-235">You can now override which filters apply to a given action method or controller by specifying an override filter.</span></span> <span data-ttu-id="4300c-236">Filtry přepsání určují sadu typů filtrů, které by neměly být spuštěny pro daný obor (akce nebo kontroler).</span><span class="sxs-lookup"><span data-stu-id="4300c-236">Override filters specify a set of filter types that should not be run for a given scope (action or controller).</span></span> <span data-ttu-id="4300c-237">To vám umožní nakonfigurovat filtry, které se použijí globálně, ale pak vyloučit určité globální filtry z použití na konkrétní akce nebo řadiče.</span><span class="sxs-lookup"><span data-stu-id="4300c-237">This allows you to configure filters that apply globally but then exclude certain global filters from applying to specific actions or controllers.</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="4300c-238">Směrování atributů</span><span class="sxs-lookup"><span data-stu-id="4300c-238">Attribute routing</span></span>

<span data-ttu-id="4300c-239">ASP.NET MVC teď podporuje směrování atributů. díky příspěvku ve službě Tim McCall je autorem [http://attributerouting.net](http://attributerouting.net).</span><span class="sxs-lookup"><span data-stu-id="4300c-239">ASP.NET MVC now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="4300c-240">Při směrování atributů můžete zadat trasy zadáním poznámek k vašim akcím a řadičům.</span><span class="sxs-lookup"><span data-stu-id="4300c-240">With attribute routing you can specify your routes by annotating your actions and controllers.</span></span>

<a id="TOC11"></a>
## <a name="aspnet-web-api-2"></a><span data-ttu-id="4300c-241">Webové rozhraní API 2 technologie ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4300c-241">ASP.NET Web API 2</span></span>

### <a name="attribute-routing"></a><span data-ttu-id="4300c-242">Směrování atributů</span><span class="sxs-lookup"><span data-stu-id="4300c-242">Attribute routing</span></span>

<span data-ttu-id="4300c-243">Webové rozhraní API ASP.NET teď podporuje směrování atributů. díky příspěvku ve službě Tim McCall je autorem [http://attributerouting.net](http://attributerouting.net).</span><span class="sxs-lookup"><span data-stu-id="4300c-243">ASP.NET Web API now supports attribute routing, thanks to a contribution by Tim McCall, the author of [http://attributerouting.net](http://attributerouting.net).</span></span> <span data-ttu-id="4300c-244">Při směrování atributů můžete zadat své trasy webového rozhraní API zadáním poznámek k vašim akcím a řadičům takto:</span><span class="sxs-lookup"><span data-stu-id="4300c-244">With attribute routing you can specify your Web API routes by annotating your actions and controllers like this:</span></span>

[!code-csharp[Main](release-notes/samples/sample1.cs)]

<span data-ttu-id="4300c-245">Směrování atributů nabízí větší kontrolu nad identifikátory URI ve webovém rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="4300c-245">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="4300c-246">Můžete například snadno definovat hierarchii prostředků pomocí jediného kontroleru rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="4300c-246">For example, you can easily define a resource hierarchy using a single API controller:</span></span>

[!code-csharp[Main](release-notes/samples/sample2.cs)]

<span data-ttu-id="4300c-247">Směrování atributů také poskytuje pohodlný Syntax pro určení volitelných parametrů, výchozích hodnot a omezení trasy:</span><span class="sxs-lookup"><span data-stu-id="4300c-247">Attribute routing also provides a convenient syntax for specifying optional parameters, default values, and route constraints:</span></span>

[!code-csharp[Main](release-notes/samples/sample3.cs)]

<span data-ttu-id="4300c-248">Další informace o směrování atributů najdete v tématu [Směrování atributů ve webovém rozhraní API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="4300c-248">For more information about attribute routing, see [Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2.md).</span></span>

### <a name="oauth-20"></a><span data-ttu-id="4300c-249">OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="4300c-249">OAuth 2.0</span></span>

<span data-ttu-id="4300c-250">Webové rozhraní API a šablony projektů aplikace na jedné stránce teď podporují autorizaci pomocí OAuth 2,0.</span><span class="sxs-lookup"><span data-stu-id="4300c-250">The Web API and Single Page Application project templates now support authorization using OAuth 2.0.</span></span> <span data-ttu-id="4300c-251">OAuth 2,0 je architektura pro autorizaci přístupu klienta k chráněným prostředkům.</span><span class="sxs-lookup"><span data-stu-id="4300c-251">OAuth 2.0 is a framework for authorizing client access to protected resources.</span></span> <span data-ttu-id="4300c-252">Funguje pro celou řadu klientů, včetně prohlížečů a mobilních zařízení.</span><span class="sxs-lookup"><span data-stu-id="4300c-252">It works for a variety of clients including browsers and mobile devices.</span></span>

<span data-ttu-id="4300c-253">Podpora OAuth 2,0 vychází z nového middlewaru zabezpečení poskytnutého komponentami Microsoft OWIN pro ověřování držitele a implementaci role autorizačního serveru.</span><span class="sxs-lookup"><span data-stu-id="4300c-253">Support for OAuth 2.0 is based on new security middleware provided by the Microsoft OWIN Components for bearer authentication and implementing the authorization server role.</span></span> <span data-ttu-id="4300c-254">Klienty je taky možné autorizovat pomocí autorizačního serveru organizace, jako je Azure Active Directory nebo ADFS ve Windows Serveru 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="4300c-254">Alternatively, clients can be authorized using an organizational authorization server, such as Azure Active Directory or ADFS in Windows Server 2012 R2.</span></span>

### <a name="odata-improvements"></a><span data-ttu-id="4300c-255">Vylepšení OData</span><span class="sxs-lookup"><span data-stu-id="4300c-255">OData Improvements</span></span>

<span data-ttu-id="4300c-256">**Podpora pro $select, $expand, $batch a $value**</span><span class="sxs-lookup"><span data-stu-id="4300c-256">**Support for $select, $expand, $batch, and $value**</span></span>

<span data-ttu-id="4300c-257">ASP.NET Web API OData teď má úplnou podporu pro $select, $expand a $value.</span><span class="sxs-lookup"><span data-stu-id="4300c-257">ASP.NET Web API OData now has full support for $select, $expand, and $value.</span></span> <span data-ttu-id="4300c-258">Můžete také použít $batch pro vyžádání dávkování a zpracování sad změn.</span><span class="sxs-lookup"><span data-stu-id="4300c-258">You can also use $batch for request batching and processing of change sets.</span></span>

<span data-ttu-id="4300c-259">Možnosti $select a $expand umožňují změnit tvar dat vrácených z koncového bodu OData.</span><span class="sxs-lookup"><span data-stu-id="4300c-259">The $select and $expand options let you change the shape of the data that is returned from an OData endpoint.</span></span> <span data-ttu-id="4300c-260">Další informace najdete v tématu [představujeme $Select a $expand podporu ve webovém rozhraní API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).</span><span class="sxs-lookup"><span data-stu-id="4300c-260">For more information, see [Introducing $select and $expand support in Web API OData](../../../web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value.md).</span></span>

<span data-ttu-id="4300c-261">**Vylepšené rozšíření**</span><span class="sxs-lookup"><span data-stu-id="4300c-261">**Improved extensibility**</span></span>

<span data-ttu-id="4300c-262">Formátovací moduly OData jsou teď rozšiřitelné.</span><span class="sxs-lookup"><span data-stu-id="4300c-262">The OData formatters are now extensible.</span></span> <span data-ttu-id="4300c-263">Můžete přidat metadata záznamů o atomech, podporu pojmenovaných datových proudů a mediálních odkazů, přidat poznámky k instanci a přizpůsobit způsob generování odkazů.</span><span class="sxs-lookup"><span data-stu-id="4300c-263">You can add Atom entry metadata, support named stream and media link entries, add instance annotations, and customize how links are generated.</span></span>

<span data-ttu-id="4300c-264">**Podpora typu bez typu**</span><span class="sxs-lookup"><span data-stu-id="4300c-264">**Type-less support**</span></span>

<span data-ttu-id="4300c-265">Nyní můžete vytvářet služby OData bez nutnosti definovat typy CLR pro vaše typy entit.</span><span class="sxs-lookup"><span data-stu-id="4300c-265">You can now build OData services without needing to define CLR types for your entity types.</span></span> <span data-ttu-id="4300c-266">Místo toho můžou vaše řadiče OData brát nebo vracet instance **IEdmObject**, což jsou deserializace formátovacích modulů OData.</span><span class="sxs-lookup"><span data-stu-id="4300c-266">Instead, your OData controllers can take or return instances of **IEdmObject**, which are the OData formatters serialize/deserialize.</span></span>

<span data-ttu-id="4300c-267">**Opětovné použití existujícího modelu**</span><span class="sxs-lookup"><span data-stu-id="4300c-267">**Reuse an existing model**</span></span>

<span data-ttu-id="4300c-268">Pokud už máte existující entity data model (EDM), můžete ho teď znovu použít přímo místo toho, abyste museli sestavovat nový.</span><span class="sxs-lookup"><span data-stu-id="4300c-268">If you already have an existing entity data model (EDM), you can now reuse it directly, instead of having to build a new one.</span></span> <span data-ttu-id="4300c-269">Například pokud používáte Entity Framework, můžete použít model EDM, který pro vás sestaví sestavení EF.</span><span class="sxs-lookup"><span data-stu-id="4300c-269">For example, if you are using Entity Framework, you can use the EDM that EF builds for you.</span></span>

### <a name="request-batching"></a><span data-ttu-id="4300c-270">Dávkování požadavků</span><span class="sxs-lookup"><span data-stu-id="4300c-270">Request Batching</span></span>

<span data-ttu-id="4300c-271">Dávkování požadavků kombinuje více operací do jedné žádosti HTTP POST, aby snížilo zatížení sítě a poskytovalo hladší a méně konverzace uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="4300c-271">Request batching combines multiple operations into a single HTTP POST request, to reduce network traffic and provide a smoother, less chatty user interface.</span></span> <span data-ttu-id="4300c-272">Webové rozhraní API ASP.NET teď podporuje několik strategií pro dávkování žádostí:</span><span class="sxs-lookup"><span data-stu-id="4300c-272">ASP.NET Web API now supports several strategies for request batching:</span></span>

- <span data-ttu-id="4300c-273">Použijte koncový bod $batch služby OData.</span><span class="sxs-lookup"><span data-stu-id="4300c-273">Use the $batch endpoint of an OData service.</span></span>
- <span data-ttu-id="4300c-274">Zabalit více požadavků do jedné žádosti MIME na jednu část.</span><span class="sxs-lookup"><span data-stu-id="4300c-274">Package multiple requests into a single MIME multipart request.</span></span>
- <span data-ttu-id="4300c-275">Použijte vlastní formát dávkování.</span><span class="sxs-lookup"><span data-stu-id="4300c-275">Use a custom batching format.</span></span>

<span data-ttu-id="4300c-276">Pokud chcete povolit dávkování žádostí, jednoduše přidejte trasu s obslužnou rutinou dávkování do vaší konfigurace webového rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="4300c-276">To enable request batching, simply add a route with a batching handler to your Web API configuration:</span></span>

[!code-csharp[Main](release-notes/samples/sample4.cs)]

<span data-ttu-id="4300c-277">Můžete také řídit, zda jsou požadavky nebo provedeny postupně, nebo v libovolném pořadí.</span><span class="sxs-lookup"><span data-stu-id="4300c-277">You can also control whether requests or executed sequentially or in any order.</span></span>

### <a name="portable-aspnet-web-api-client"></a><span data-ttu-id="4300c-278">Klient webového rozhraní API pro přenosné ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4300c-278">Portable ASP.NET Web API Client</span></span>

<span data-ttu-id="4300c-279">Nyní můžete používat klienta webového rozhraní API ASP.NET k vytváření přenosných knihoven tříd, které fungují v aplikacích pro Windows Store a Windows Phone 8.</span><span class="sxs-lookup"><span data-stu-id="4300c-279">You can now use the ASP.NET Web API Client to create portable class libraries that work across your Windows Store and Windows Phone 8 applications.</span></span> <span data-ttu-id="4300c-280">Můžete také vytvářet přenosné formátovací moduly, které lze sdílet mezi klientem a serverem.</span><span class="sxs-lookup"><span data-stu-id="4300c-280">You can also create portable formatters that can be shared across client and server.</span></span>

### <a name="improved-testability"></a><span data-ttu-id="4300c-281">Vylepšená testování</span><span class="sxs-lookup"><span data-stu-id="4300c-281">Improved Testability</span></span>

<span data-ttu-id="4300c-282">Webové rozhraní API 2 významně usnadňuje testování řadičů rozhraní API na jednotkách.</span><span class="sxs-lookup"><span data-stu-id="4300c-282">Web API 2 makes it much easier to unit test your API controllers.</span></span> <span data-ttu-id="4300c-283">Stačí vytvořit instanci vašeho kontroleru rozhraní API se zprávou a konfigurací požadavku a pak zavolat metodu akce, kterou chcete otestovat.</span><span class="sxs-lookup"><span data-stu-id="4300c-283">Just instantiate your API controller with your request message and configuration, and then call the action method you wish to test.</span></span> <span data-ttu-id="4300c-284">Pro metody akcí, které provádějí vytváření odkazů, je také snadné vytvořit třídu **UrlHelper** .</span><span class="sxs-lookup"><span data-stu-id="4300c-284">It is also easy to mock the **UrlHelper** class, for action methods that perform link generation.</span></span>

### <a name="ihttpactionresult"></a><span data-ttu-id="4300c-285">IHttpActionResult</span><span class="sxs-lookup"><span data-stu-id="4300c-285">IHttpActionResult</span></span>

<span data-ttu-id="4300c-286">Teď můžete implementovat IHttpActionResult k zapouzdření výsledku vašich metod akce webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="4300c-286">You can now implement IHttpActionResult to encapsulate the result of your Web API action methods.</span></span> <span data-ttu-id="4300c-287">IHttpActionResult vrácená z metody akce webového rozhraní API je prováděna modulem runtime webového rozhraní API ASP.NET a vytvoří výslednou odpověď na zprávu.</span><span class="sxs-lookup"><span data-stu-id="4300c-287">An IHttpActionResult returned from a Web API action method is executed by the ASP.NET Web API runtime to produce the resultant response message.</span></span> <span data-ttu-id="4300c-288">IHttpActionResult může být vrácen z jakékoli akce webového rozhraní API pro zjednodušení testování částí implementace webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="4300c-288">An IHttpActionResult can be returned from any Web API action to simplify unit testing of your Web API implementation.</span></span> <span data-ttu-id="4300c-289">Pro usnadnění práce se vydává řada implementací IHttpActionResult, včetně výsledků pro vracení specifických stavových kódů, formátovaného obsahu nebo odpovědí vydaných obsahem.</span><span class="sxs-lookup"><span data-stu-id="4300c-289">For convenience a number of IHttpActionResult implementations are provided out of the box including results for returning specific status codes, formatted content or content-negotiated responses.</span></span>

### <a name="httprequestcontext"></a><span data-ttu-id="4300c-290">HttpRequestContext</span><span class="sxs-lookup"><span data-stu-id="4300c-290">HttpRequestContext</span></span>

<span data-ttu-id="4300c-291">Nový **HttpRequestContext** sleduje všechny stavy, které jsou svázané s požadavkem, ale není okamžitě k dispozici z požadavku.</span><span class="sxs-lookup"><span data-stu-id="4300c-291">The new **HttpRequestContext** tracks any state that is tied to the request but is not immediately available from the request.</span></span> <span data-ttu-id="4300c-292">Pomocí nástroje **HttpRequestContext** můžete například získat data o trasách, objekt zabezpečení přidružený k žádosti, klientský certifikát, **UrlHelper** a kořen virtuální cesty.</span><span class="sxs-lookup"><span data-stu-id="4300c-292">For example, you can use the **HttpRequestContext** to get route data, the principal associated with the request, the client certificate, the **UrlHelper** and the virtual path root.</span></span> <span data-ttu-id="4300c-293">Můžete snadno vytvořit **HttpRequestContext** pro účely testování částí.</span><span class="sxs-lookup"><span data-stu-id="4300c-293">You can easily create an **HttpRequestContext** for unit testing purposes.</span></span>

<span data-ttu-id="4300c-294">Vzhledem k tomu, že objekt zabezpečení pro požadavek se předá na **vlákno. CurrentPrincipal**, je teď k dispozici objekt zabezpečení po celou dobu životnosti žádosti, když je v kanálu webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="4300c-294">Because the principal for the request is flowed with the request instead of relying on **Thread.CurrentPrincipal**, the principal is now available throughout the lifetime of the request while it is in the Web API pipeline.</span></span>

### <a name="cors"></a><span data-ttu-id="4300c-295">CORS</span><span class="sxs-lookup"><span data-stu-id="4300c-295">CORS</span></span>

<span data-ttu-id="4300c-296">Díky dalšímu skvělému příspěvku z Brock Allen teď ASP.NET nyní plně podporuje sdílení žádostí mezi zdroji (CORS).</span><span class="sxs-lookup"><span data-stu-id="4300c-296">Thanks to another great contribution from Brock Allen, ASP.NET now fully supports Cross Origin Request Sharing (CORS).</span></span>

<span data-ttu-id="4300c-297">Zabezpečení prohlížeče brání webové stránce v provádění požadavků AJAX na jinou doménu.</span><span class="sxs-lookup"><span data-stu-id="4300c-297">Browser security prevents a web page from making AJAX requests to another domain.</span></span> <span data-ttu-id="4300c-298">[CORS](http://www.w3.org/TR/cors/) je standard W3C, který umožňuje serveru zmírnit zásady stejného zdroje.</span><span class="sxs-lookup"><span data-stu-id="4300c-298">[CORS](http://www.w3.org/TR/cors/) is a W3C standard that allows a server to relax the same-origin policy.</span></span> <span data-ttu-id="4300c-299">Při použití CORS může server explicitně umožnit některé žádosti o více zdrojů a současně odmítat jiné.</span><span class="sxs-lookup"><span data-stu-id="4300c-299">Using CORS, a server can explicitly allow some cross-origin requests while rejecting others.</span></span>

<span data-ttu-id="4300c-300">Webové rozhraní API 2 teď podporuje CORS, včetně automatického zpracování požadavků na kontrolu před výstupem.</span><span class="sxs-lookup"><span data-stu-id="4300c-300">Web API 2 now supports CORS, including automatic handling of preflight requests.</span></span> <span data-ttu-id="4300c-301">Další informace najdete v tématu [Povolení žádostí mezi zdroji v ASP.NET webovém rozhraní API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="4300c-301">For more information, see [Enabling Cross-Origin Requests in ASP.NET Web API](../../../web-api/overview/security/enabling-cross-origin-requests-in-web-api.md).</span></span>

### <a name="authentication-filters"></a><span data-ttu-id="4300c-302">Filtry ověřování</span><span class="sxs-lookup"><span data-stu-id="4300c-302">Authentication Filters</span></span>

<span data-ttu-id="4300c-303">Filtry ověřování jsou novým druhem filtru ve webovém rozhraní API ASP.NET, který se spouští před autorizačními filtry v kanálu webového rozhraní API ASP.NET, a umožňuje pro všechny řadiče zadat logiku ověřování pro jednotlivé akce, řadiče nebo globálně.</span><span class="sxs-lookup"><span data-stu-id="4300c-303">Authentication filters are a new kind of filter in ASP.NET Web API that run prior to authorization filters in the ASP.NET Web API pipeline and allow you to specify authentication logic per-action, per-controller, or globally for all controllers.</span></span> <span data-ttu-id="4300c-304">Ověřovací filtry zpracovávají přihlašovací údaje v žádosti a poskytují odpovídající objekt zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="4300c-304">Authentication filters process credentials in the request and provide a corresponding principal.</span></span> <span data-ttu-id="4300c-305">Ověřovací filtry mohou také přidat výzvy ověřování v reakci na neautorizované žádosti.</span><span class="sxs-lookup"><span data-stu-id="4300c-305">Authentication filters can also add authentication challenges in response to unauthorized requests.</span></span>

### <a name="filter-overrides"></a><span data-ttu-id="4300c-306">Přepsání filtru</span><span class="sxs-lookup"><span data-stu-id="4300c-306">Filter Overrides</span></span>

<span data-ttu-id="4300c-307">Nyní můžete přepsat, které filtry se vztahují na danou metodu akce nebo kontroler, zadáním filtru pro přepsání.</span><span class="sxs-lookup"><span data-stu-id="4300c-307">You can now override which filters apply to a given action method or controller, by specifying an override filter.</span></span> <span data-ttu-id="4300c-308">Filtry přepsání určují sadu typů filtrů, které by neměly být spuštěny pro daný obor (Action nebo Controller).</span><span class="sxs-lookup"><span data-stu-id="4300c-308">Override filters specify a set of filter types that should not run for a given scope (action or controller).</span></span> <span data-ttu-id="4300c-309">To umožňuje přidat globální filtry, ale pak některé z určitých akcí nebo řadičů vyloučit.</span><span class="sxs-lookup"><span data-stu-id="4300c-309">This allows you to add global filters, but then exclude some from specific actions or controllers.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="4300c-310">Integrace OWIN</span><span class="sxs-lookup"><span data-stu-id="4300c-310">OWIN Integration</span></span>

<span data-ttu-id="4300c-311">Webové rozhraní API ASP.NET teď plně podporuje OWIN a dají se spustit na jakémkoli hostiteli podporujícím OWIN.</span><span class="sxs-lookup"><span data-stu-id="4300c-311">ASP.NET Web API now fully supports OWIN and can be run on any OWIN capable host.</span></span> <span data-ttu-id="4300c-312">K dispozici je také **HostAuthenticationFilter** , který poskytuje integraci s ověřovacím systémem Owin.</span><span class="sxs-lookup"><span data-stu-id="4300c-312">Also included is a **HostAuthenticationFilter** that provides integration with the OWIN authentication system.</span></span>

<span data-ttu-id="4300c-313">Díky integraci OWIN můžete webové rozhraní API samostatně hostovat ve vlastním procesu společně s dalšími OWIN middleware, jako je například Signaler.</span><span class="sxs-lookup"><span data-stu-id="4300c-313">With OWIN integration, you can self-host Web API in your own process alongside other OWIN middleware, such as SignalR.</span></span> <span data-ttu-id="4300c-314">Další informace najdete v tématu [použití Owin k samoobslužnému hostování ASP.NET webového rozhraní API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span><span class="sxs-lookup"><span data-stu-id="4300c-314">For more information, see [Use OWIN to Self-Host ASP.NET Web API](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="TOC13"></a>
## <a name="aspnet-signalr-20"></a><span data-ttu-id="4300c-315">ASP.NET signál 2,0</span><span class="sxs-lookup"><span data-stu-id="4300c-315">ASP.NET SignalR 2.0</span></span>

<span data-ttu-id="4300c-316">Následující části popisují funkce nástroje Signal 2,0.</span><span class="sxs-lookup"><span data-stu-id="4300c-316">The following sections describe features of SignalR 2.0.</span></span>

- [<span data-ttu-id="4300c-317">Postavené na OWIN</span><span class="sxs-lookup"><span data-stu-id="4300c-317">Built on OWIN</span></span>](#builtonowin)
- [<span data-ttu-id="4300c-318">MapHubs a MapConnection jsou nyní MapSignalR</span><span class="sxs-lookup"><span data-stu-id="4300c-318">MapHubs and MapConnection are now MapSignalR</span></span>](#MapSignalR)
- [<span data-ttu-id="4300c-319">Podpora mezi doménami</span><span class="sxs-lookup"><span data-stu-id="4300c-319">Cross-Domain Support</span></span>](#crossdomain)
- [<span data-ttu-id="4300c-320">Podpora iOS a Androidu prostřednictvím MonoTouch a MonoDroid</span><span class="sxs-lookup"><span data-stu-id="4300c-320">iOS and Android support via MonoTouch and MonoDroid</span></span>](#mobile)
- [<span data-ttu-id="4300c-321">Přenosný klient .NET</span><span class="sxs-lookup"><span data-stu-id="4300c-321">Portable .NET Client</span></span>](#portable)
- [<span data-ttu-id="4300c-322">Nový balíček pro samoobslužné hostování</span><span class="sxs-lookup"><span data-stu-id="4300c-322">New Self-Host Package</span></span>](#selfhost)
- [<span data-ttu-id="4300c-323">Zpětně kompatibilní serverová podpora</span><span class="sxs-lookup"><span data-stu-id="4300c-323">Backward-compatible server support</span></span>](#backwardcompat)
- [<span data-ttu-id="4300c-324">Odebrala se podpora serveru pro .NET 4,0.</span><span class="sxs-lookup"><span data-stu-id="4300c-324">Removed server support for .NET 4.0</span></span>](#remove40)
- [<span data-ttu-id="4300c-325">Odeslání zprávy do seznamu klientů a skupin</span><span class="sxs-lookup"><span data-stu-id="4300c-325">Sending a message to a list of clients and groups</span></span>](#messagelist)
- [<span data-ttu-id="4300c-326">Odeslání zprávy konkrétnímu uživateli</span><span class="sxs-lookup"><span data-stu-id="4300c-326">Sending a message to a specific user</span></span>](#sendtouser)
- [<span data-ttu-id="4300c-327">Lepší podpora zpracování chyb</span><span class="sxs-lookup"><span data-stu-id="4300c-327">Better error handling support</span></span>](#errorhandling)
- [<span data-ttu-id="4300c-328">Snadnější testování částí Center</span><span class="sxs-lookup"><span data-stu-id="4300c-328">Easier unit testing of hubs</span></span>](#unittesting)
- [<span data-ttu-id="4300c-329">Zpracování chyb JavaScriptu</span><span class="sxs-lookup"><span data-stu-id="4300c-329">JavaScript error handling</span></span>](#javascripterror)

<span data-ttu-id="4300c-330">Příklad, jak upgradovat existující projekt 1. x na Signaler 2,0, najdete v tématu [Upgrade aplikace Signal 1. x](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).</span><span class="sxs-lookup"><span data-stu-id="4300c-330">For an example of how to upgrade an existing 1.x project to SignalR 2.0, see [Upgrading a SignalR 1.x Project](../../../signalr/overview/releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<a id="builtonowin"></a>
### <a name="built-on-owin"></a><span data-ttu-id="4300c-331">Postavené na OWIN</span><span class="sxs-lookup"><span data-stu-id="4300c-331">Built on OWIN</span></span>

<span data-ttu-id="4300c-332">Návěstí 2,0 je zcela postavené na [Owin (otevřené webové rozhraní pro .NET)](http://owin.org/).</span><span class="sxs-lookup"><span data-stu-id="4300c-332">SignalR 2.0 is built completely on [OWIN (the Open Web Interface for .NET)](http://owin.org/).</span></span> <span data-ttu-id="4300c-333">Tato změna způsobí, že proces nastavení signalizace je mnohem větší konzistence mezi aplikacemi, které jsou hostovány v rámci hostování webů a v místním prostředí, ale také vyžadovala několik změn rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="4300c-333">This change makes the setup process for SignalR much more consistent between web-hosted and self-hosted SignalR applications, but has also required a number of API changes.</span></span>

<a id="MapSignalR"></a>

### <a name="maphubs-and-mapconnection-are-now-mapsignalr"></a><span data-ttu-id="4300c-334">MapHubs a MapConnection jsou nyní MapSignalR</span><span class="sxs-lookup"><span data-stu-id="4300c-334">MapHubs and MapConnection are now MapSignalR</span></span>

<span data-ttu-id="4300c-335">Z důvodu kompatibility s normami OWIN byly tyto metody přejmenovány na `MapSignalR`.</span><span class="sxs-lookup"><span data-stu-id="4300c-335">For compatibility with OWIN standards, these methods have been renamed to `MapSignalR`.</span></span> <span data-ttu-id="4300c-336">`MapSignalR`, který se volá bez parametrů, namapuje všechna centra (jako `MapHubs` ve verzi 1. x). Chcete-li namapovat jednotlivé objekty **PersistentConnection** , zadejte typ připojení jako parametr typu a příponu adresy URL pro připojení jako první argument.</span><span class="sxs-lookup"><span data-stu-id="4300c-336">`MapSignalR` called without parameters will map all hubs (as `MapHubs` does in version 1.x); to map individual **PersistentConnection** objects, specify the connection type as the type parameter, and the URL extension for the connection as the first argument.</span></span>

<span data-ttu-id="4300c-337">Metoda `MapSignalR` je volána ve třídě spuštění Owin.</span><span class="sxs-lookup"><span data-stu-id="4300c-337">The `MapSignalR` method is called in an Owin startup class.</span></span> <span data-ttu-id="4300c-338">Visual Studio 2013 obsahuje novou šablonu pro třídu pro spuštění Owin; Chcete-li použít tuto šablonu, postupujte následovně:</span><span class="sxs-lookup"><span data-stu-id="4300c-338">Visual Studio 2013 contains a new template for an Owin startup class; to use this template, do the following:</span></span>

1. <span data-ttu-id="4300c-339">Klikněte pravým tlačítkem na projekt.</span><span class="sxs-lookup"><span data-stu-id="4300c-339">Right-click on the project</span></span>
2. <span data-ttu-id="4300c-340">Vyberte **Přidat**, **Nová položka...**</span><span class="sxs-lookup"><span data-stu-id="4300c-340">Select **Add**, **New Item...**</span></span>
3. <span data-ttu-id="4300c-341">Vyberte **spouštěcí třídu Owin**.</span><span class="sxs-lookup"><span data-stu-id="4300c-341">Select **Owin Startup class**.</span></span> <span data-ttu-id="4300c-342">Pojmenujte novou třídu **Startup.cs**.</span><span class="sxs-lookup"><span data-stu-id="4300c-342">Name the new class **Startup.cs**.</span></span>

<span data-ttu-id="4300c-343">Ve **webové aplikaci** se následně do procesu spouštění Owin přidá třída Startup Owin obsahující metodu `MapSignalR` pomocí položky v uzlu nastavení aplikace souboru Web. config, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="4300c-343">In a **Web application,** the Owin startup class containing the `MapSignalR` method is then added to Owin's startup process using an entry in the application settings node of the Web.Config file, as shown below.</span></span>

<span data-ttu-id="4300c-344">V **samoobslužné aplikaci**je spouštěcí třída předána jako parametr typu metody `WebApp.Start`.</span><span class="sxs-lookup"><span data-stu-id="4300c-344">In a **Self-hosted application**, the Startup class is passed as the type parameter of the `WebApp.Start` method.</span></span>

<span data-ttu-id="4300c-345">**Mapování Center a připojení v návěsti 1. x (ze souboru globální aplikace ve webové aplikaci):**</span><span class="sxs-lookup"><span data-stu-id="4300c-345">**Mapping hubs and connections in SignalR 1.x (from the global application file in a web application):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample5.cs)]

<span data-ttu-id="4300c-346">**Mapování Center a připojení v nástroji Signal 2,0 (ze souboru spouštěcí třídy Owin):**</span><span class="sxs-lookup"><span data-stu-id="4300c-346">**Mapping hubs and connections in SignalR 2.0 (from an Owin Startup class file):**</span></span> 

[!code-csharp[Main](release-notes/samples/sample6.cs)]

<span data-ttu-id="4300c-347">V **samoobslužné aplikaci**je spouštěcí třída předána jako parametr typu pro metodu `WebApp.Start`, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="4300c-347">In a **Self-hosted application**, the Startup class is passed as the type parameter for the `WebApp.Start` method, as shown below.</span></span>

[!code-csharp[Main](release-notes/samples/sample7.cs)]

<a id="crossdomain"></a>

### <a name="cross-domain-support"></a><span data-ttu-id="4300c-348">Podpora mezi doménami</span><span class="sxs-lookup"><span data-stu-id="4300c-348">Cross-Domain Support</span></span>

<span data-ttu-id="4300c-349">V návěsti 1. x byly požadavky křížové domény řízené jediným příznakem EnableCrossDomain.</span><span class="sxs-lookup"><span data-stu-id="4300c-349">In SignalR 1.x, cross domain requests were controlled by a single EnableCrossDomain flag.</span></span> <span data-ttu-id="4300c-350">Tento příznak ovládá požadavky JSONP i CORS.</span><span class="sxs-lookup"><span data-stu-id="4300c-350">This flag controlled both JSONP and CORS requests.</span></span> <span data-ttu-id="4300c-351">Pro větší flexibilitu byla ze serverové součásti signalizace odebrána veškerá podpora CORS (klienti JavaScriptu pořád používají CORS normálně, pokud se zjistí, že ji prohlížeč podporuje) a byl k dispozici nový middleware OWIN pro podporu těchto scénářů.</span><span class="sxs-lookup"><span data-stu-id="4300c-351">For greater flexibility, all CORS support has been removed from the server component of SignalR (JavaScript clients still use CORS normally if it is detected that the browser supports it), and new OWIN middleware has been made available to support these scenarios.</span></span>

<span data-ttu-id="4300c-352">Pokud je ve službě Signal-2,0 vyžadováno, aby klient (podporoval požadavky mezi doménami ve starších prohlížečích), bude muset být povolen explicitně nastavením `EnableJSONP` u objektu `HubConfiguration` na `true`, jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="4300c-352">In SignalR 2.0, If JSONP is required on the client (to support cross-domain requests in older browsers), it will need to be enabled explicitly by setting `EnableJSONP` on the `HubConfiguration` object to `true`, as shown below.</span></span> <span data-ttu-id="4300c-353">Služba JSONP je ve výchozím nastavení zakázána, protože je méně bezpečná než CORS.</span><span class="sxs-lookup"><span data-stu-id="4300c-353">JSONP is disabled by default, as it is less secure than CORS.</span></span>

<span data-ttu-id="4300c-354">Chcete-li přidat nový middleware CORS do služby Signal 2,0, přidejte do projektu knihovnu `Microsoft.Owin.Cors` a zavolejte `UseCors` před middlewari signálu, jak je znázorněno v následující části.</span><span class="sxs-lookup"><span data-stu-id="4300c-354">To add the new CORS middleware in SignalR 2.0, add the `Microsoft.Owin.Cors` library to your project, and call `UseCors` before your SignalR middleware, as shown in the section below.</span></span>

<span data-ttu-id="4300c-355">**Do projektu se přidává soubor Microsoft. Owin. Cors**: Pokud chcete tuto knihovnu nainstalovat, spusťte následující příkaz v konzole správce balíčků:</span><span class="sxs-lookup"><span data-stu-id="4300c-355">**Adding Microsoft.Owin.Cors to your project**: To install this library, run the following command in the Package Manager Console:</span></span>

[!code-powershell[Main](release-notes/samples/sample8.ps1)]

<span data-ttu-id="4300c-356">Tento příkaz přidá do projektu verzi 2.0.0 balíčku.</span><span class="sxs-lookup"><span data-stu-id="4300c-356">This command will add the 2.0.0 version of the package to your project.</span></span>

<span data-ttu-id="4300c-357">**Volání UseCors**</span><span class="sxs-lookup"><span data-stu-id="4300c-357">**Calling UseCors**</span></span>

<span data-ttu-id="4300c-358">Následující fragmenty kódu ukazují, jak implementovat připojení mezi doménami v návěsti 1. x a 2,0.</span><span class="sxs-lookup"><span data-stu-id="4300c-358">The following code snippets demonstrate how to implement cross-domain connections in SignalR 1.x and 2.0.</span></span>

<span data-ttu-id="4300c-359">**Implementace požadavků mezi doménami v nástroji Signal 1. x (z globálního souboru aplikace)**</span><span class="sxs-lookup"><span data-stu-id="4300c-359">**Implementing cross-domain requests in SignalR 1.x (from the global application file)**</span></span>

[!code-csharp[Main](release-notes/samples/sample9.cs)]

<span data-ttu-id="4300c-360">**Implementace žádostí mezi doménami v nástroji Signal 2,0 (ze souboru C# kódu)**</span><span class="sxs-lookup"><span data-stu-id="4300c-360">**Implementing cross-domain requests in SignalR 2.0 (from a C# code file)**</span></span>

<span data-ttu-id="4300c-361">Následující kód ukazuje, jak povolit CORS nebo JSONP v projektu Signal 2,0.</span><span class="sxs-lookup"><span data-stu-id="4300c-361">The following code demonstrates how to enable CORS or JSONP in a SignalR 2.0 project.</span></span> <span data-ttu-id="4300c-362">Tato ukázka kódu používá `Map` a `RunSignalR` namísto `MapSignalR`, takže middleware CORS běží pouze pro požadavky na signál, které vyžadují podporu CORS (nikoli pro všechny přenosy v cestě zadané v `MapSignalR`.) `Map` lze také použít pro jakýkoli jiný middlewarový kód, který je třeba spustit pro konkrétní předponu adresy URL, nikoli pro celou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="4300c-362">This code sample uses `Map` and `RunSignalR` instead of `MapSignalR`, so that the CORS middleware runs only for the SignalR requests that require CORS support (rather than for all traffic at the path specified in `MapSignalR`.) `Map` can also be used for any other middleware that needs to run for a specific URL prefix, rather than for the entire application.</span></span>

[!code-csharp[Main](release-notes/samples/sample10.cs)]

<a id="mobile"></a>

### <a name="ios-and-android-support-via-monotouch-and-monodroid"></a><span data-ttu-id="4300c-363">Podpora iOS a Androidu prostřednictvím MonoTouch a MonoDroid</span><span class="sxs-lookup"><span data-stu-id="4300c-363">iOS and Android support via MonoTouch and MonoDroid</span></span>

<span data-ttu-id="4300c-364">Pro klienty se systémy iOS a Android se přidala podpora pomocí komponent MonoTouch a MonoDroid z [knihovny Xamarin](https://xamarin.com/).</span><span class="sxs-lookup"><span data-stu-id="4300c-364">Support has been added for iOS and Android clients using MonoTouch and MonoDroid components from the [Xamarin library](https://xamarin.com/).</span></span> <span data-ttu-id="4300c-365">Další informace o tom, jak je používat, najdete v tématu [použití komponent Xamarin](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln).</span><span class="sxs-lookup"><span data-stu-id="4300c-365">For more information on how to use them, see [Using Xamarin Components](https://github.com/SignalR/SignalR/wiki/Building-Mono.Mobile.sln).</span></span> <span data-ttu-id="4300c-366">Tyto součásti budou k dispozici v [Xamarin Storu](https://store.xamarin.com/) , až bude dostupná verze nástroje Signal RTW.</span><span class="sxs-lookup"><span data-stu-id="4300c-366">These components will be available in the [Xamarin Store](https://store.xamarin.com/) when the SignalR RTW release is available.</span></span>

<a id="portable"></a><span data-ttu-id="4300c-367"># # # Přenosný klient .NET</span><span class="sxs-lookup"><span data-stu-id="4300c-367">### Portable .NET client</span></span>

<span data-ttu-id="4300c-368">Pro lepší vývoj pro různé platformy se klienti Silverlight, WinRT a Windows Phone nahradili jedním přenosným klientem rozhraní .NET, který podporuje tyto platformy:</span><span class="sxs-lookup"><span data-stu-id="4300c-368">To better facilitate cross-platform development, the Silverlight, WinRT and Windows Phone clients have been replaced with a single portable .NET client that supports the following platforms:</span></span>

- <span data-ttu-id="4300c-369">NET 4,5</span><span class="sxs-lookup"><span data-stu-id="4300c-369">NET 4.5</span></span>
- <span data-ttu-id="4300c-370">Silverlight 5</span><span class="sxs-lookup"><span data-stu-id="4300c-370">Silverlight 5</span></span>
- <span data-ttu-id="4300c-371">WinRT (.NET pro aplikace pro Windows Store)</span><span class="sxs-lookup"><span data-stu-id="4300c-371">WinRT (.NET for Windows Store Apps)</span></span>
- <span data-ttu-id="4300c-372">Windows Phone 8</span><span class="sxs-lookup"><span data-stu-id="4300c-372">Windows Phone 8</span></span>

<a id="selfhost"></a>

### <a name="new-self-host-package"></a><span data-ttu-id="4300c-373">Nový balíček pro samoobslužné hostování</span><span class="sxs-lookup"><span data-stu-id="4300c-373">New Self-Host Package</span></span>

<span data-ttu-id="4300c-374">Nyní je k dispozici balíček NuGet, který usnadňuje zahájení práce s nástrojem pro samoobslužné hostování (aplikace na základě signálů, které jsou hostovány v rámci procesu nebo jiné aplikace) místo hostování na webovém serveru.</span><span class="sxs-lookup"><span data-stu-id="4300c-374">There is now a NuGet package to make it easier to get started with SignalR Self-Host (SignalR applications that are hosted in a process or other application, rather than being hosted in a web server).</span></span> <span data-ttu-id="4300c-375">Chcete-li upgradovat projekt pro samoobslužné hostování sestavený pomocí nástroje Signal 1. x, odeberte balíček Microsoft. AspNet. Signaler. Owin a přidejte balíček Microsoft. AspNet. Signaler. SelfHost.</span><span class="sxs-lookup"><span data-stu-id="4300c-375">To upgrade a self-host project built with SignalR 1.x, remove the Microsoft.AspNet.SignalR.Owin package, and add the Microsoft.AspNet.SignalR.SelfHost package.</span></span> <span data-ttu-id="4300c-376">Další informace o tom, jak začít s balíčkem pro samoobslužné hostování, najdete v tématu [kurz: samoobslužný hostitel signálu](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span><span class="sxs-lookup"><span data-stu-id="4300c-376">For more information on getting started with the self-host package, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<a id="backwardcompat"></a>

### <a name="backward-compatible-server-support"></a><span data-ttu-id="4300c-377">Zpětně kompatibilní serverová podpora</span><span class="sxs-lookup"><span data-stu-id="4300c-377">Backward-compatible server support</span></span>

<span data-ttu-id="4300c-378">V předchozích verzích nástroje Signal bylo nutné, aby byly verze balíčku signálu použité v klientovi a na serveru identické.</span><span class="sxs-lookup"><span data-stu-id="4300c-378">In previous versions of SignalR, the versions of the SignalR package used in the client and the server needed to be identical.</span></span> <span data-ttu-id="4300c-379">Aby bylo možné podporovat silné klientské aplikace, které by bylo obtížné aktualizovat, služba Signal 2,0 nyní podporuje použití novější verze serveru se starším klientem.</span><span class="sxs-lookup"><span data-stu-id="4300c-379">In order to support thick-client applications that would be difficult to update, SignalR 2.0 now supports using a newer server version with an older client.</span></span> <span data-ttu-id="4300c-380">**Poznámka: návěstí 2,0 nepodporuje servery sestavené se staršími verzemi s novějšími klienty.**</span><span class="sxs-lookup"><span data-stu-id="4300c-380">**Note: SignalR 2.0 does not support servers built with older versions with newer clients.**</span></span>

<a id="remove40"></a>

### <a name="removed-server-support-for-net-40"></a><span data-ttu-id="4300c-381">Odebrala se podpora serveru pro .NET 4,0.</span><span class="sxs-lookup"><span data-stu-id="4300c-381">Removed server support for .NET 4.0</span></span>

<span data-ttu-id="4300c-382">Návěstí 2,0 vynechalo podporu pro interoperabilitu serveru s .NET 4,0.</span><span class="sxs-lookup"><span data-stu-id="4300c-382">SignalR 2.0 has dropped support for server interoperability with .NET 4.0.</span></span> <span data-ttu-id="4300c-383">.NET 4,5 musí být používáno se servery signálů 2,0.</span><span class="sxs-lookup"><span data-stu-id="4300c-383">.NET 4.5 must be used with SignalR 2.0 servers.</span></span> <span data-ttu-id="4300c-384">Pro Signal 2,0 je stále k dispozici klient .NET 4,0.</span><span class="sxs-lookup"><span data-stu-id="4300c-384">There is still a .NET 4.0 client for SignalR 2.0.</span></span>

<a id="messagelist"></a>

### <a name="sending-a-message-to-a-list-of-clients-and-groups"></a><span data-ttu-id="4300c-385">Odeslání zprávy do seznamu klientů a skupin</span><span class="sxs-lookup"><span data-stu-id="4300c-385">Sending a message to a list of clients and groups</span></span>

<span data-ttu-id="4300c-386">V nástroji Signal 2,0 je možné odeslat zprávu pomocí seznamu ID klientů a skupin.</span><span class="sxs-lookup"><span data-stu-id="4300c-386">In SignalR 2.0, it's possible to send a message using a list of client and group IDs.</span></span> <span data-ttu-id="4300c-387">Následující fragmenty kódu ukazují, jak to provést.</span><span class="sxs-lookup"><span data-stu-id="4300c-387">The following code snippets demonstrate how to do this.</span></span>

<span data-ttu-id="4300c-388">**Odeslání zprávy do seznamu klientů a skupin pomocí PersistentConnection**</span><span class="sxs-lookup"><span data-stu-id="4300c-388">**Sending a message to a list of clients and groups using PersistentConnection**</span></span>

[!code-csharp[Main](release-notes/samples/sample11.cs)]

<span data-ttu-id="4300c-389">**Odeslání zprávy do seznamu klientů a skupin pomocí Center**</span><span class="sxs-lookup"><span data-stu-id="4300c-389">**Sending a message to a list of clients and groups using Hubs**</span></span>

[!code-csharp[Main](release-notes/samples/sample12.cs)]

<a id="sendtouser"></a>

### <a name="sending-a-message-to-a-specific-user"></a><span data-ttu-id="4300c-390">Odeslání zprávy konkrétnímu uživateli</span><span class="sxs-lookup"><span data-stu-id="4300c-390">Sending a message to a specific user</span></span>

<span data-ttu-id="4300c-391">Tato funkce umožňuje uživatelům určit, co je ID uživatele založené na IRequest prostřednictvím nového rozhraní IUserIdProvider:</span><span class="sxs-lookup"><span data-stu-id="4300c-391">This feature allows users to specify what the userId is based on an IRequest via a new interface IUserIdProvider:</span></span>

<span data-ttu-id="4300c-392">**Rozhraní IUserIdProvider**</span><span class="sxs-lookup"><span data-stu-id="4300c-392">**The IUserIdProvider interface**</span></span>

[!code-csharp[Main](release-notes/samples/sample13.cs)]

<span data-ttu-id="4300c-393">Ve výchozím nastavení bude k dispozici implementace, která jako uživatelské jméno používá IPrincipal.Identity.Name uživatele.</span><span class="sxs-lookup"><span data-stu-id="4300c-393">By default there will be an implementation that uses the user's IPrincipal.Identity.Name as the user name.</span></span>

<span data-ttu-id="4300c-394">V centrech budete moct posílat zprávy těmto uživatelům pomocí nového rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="4300c-394">In hubs, you'll be able to send messages to these users via a new API:</span></span>

<span data-ttu-id="4300c-395">**Použití rozhraní API klientů. User**</span><span class="sxs-lookup"><span data-stu-id="4300c-395">**Using the Clients.User API**</span></span>

[!code-csharp[Main](release-notes/samples/sample14.cs)]

<a id="errorhandling"></a>

### <a name="better-error-handling-support"></a><span data-ttu-id="4300c-396">Lepší podpora zpracování chyb</span><span class="sxs-lookup"><span data-stu-id="4300c-396">Better Error Handling Support</span></span>

<span data-ttu-id="4300c-397">Uživatelé teď můžou vyvolávat **HubException** z jakéhokoli vyvolání centra.</span><span class="sxs-lookup"><span data-stu-id="4300c-397">Users can now throw **HubException** from any hub invocation.</span></span> <span data-ttu-id="4300c-398">Konstruktor **HubException** může přebírat zprávu řetězce a objekt extra chybové údaje.</span><span class="sxs-lookup"><span data-stu-id="4300c-398">The constructor of the **HubException** can take a string message and an object extra error data.</span></span> <span data-ttu-id="4300c-399">Nástroj Signal vygeneruje výjimku automaticky a pošle ji klientovi, kde bude použit k zamítnutí nebo selhání volání metody rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="4300c-399">SignalR will auto-serialize the exception and send it to the client where it will be used to reject/fail the hub method invocation.</span></span>

<span data-ttu-id="4300c-400">Nastavení **Zobrazit podrobné výjimky centra** nemá žádné vliv na **HubException** , které se odesílají zpátky do klienta, nebo ne. Vždycky se posílá.</span><span class="sxs-lookup"><span data-stu-id="4300c-400">The **show detailed hub exceptions** setting has no bearing on **HubException** being sent back to the client or not; it is always sent.</span></span>

<span data-ttu-id="4300c-401">**Kód na straně serveru ukazující odeslání HubException klientovi**</span><span class="sxs-lookup"><span data-stu-id="4300c-401">**Server-side code demonstrating sending a HubException to the client**</span></span>

[!code-csharp[Main](release-notes/samples/sample15.cs)]

<span data-ttu-id="4300c-402">**Kód klienta JavaScriptu, který ukazuje reakci na HubException odeslaný ze serveru**</span><span class="sxs-lookup"><span data-stu-id="4300c-402">**JavaScript client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-html[Main](release-notes/samples/sample16.html)]

<span data-ttu-id="4300c-403">**Kód klienta .NET, který ukazuje odpověď na HubException odeslaný ze serveru**</span><span class="sxs-lookup"><span data-stu-id="4300c-403">**.NET client code demonstrating responding to a HubException sent from the server**</span></span>

[!code-csharp[Main](release-notes/samples/sample17.cs)]

<a id="unittesting"></a>

### <a name="easier-unit-testing-of-hubs"></a><span data-ttu-id="4300c-404">Snadnější testování částí Center</span><span class="sxs-lookup"><span data-stu-id="4300c-404">Easier unit testing of hubs</span></span>

<span data-ttu-id="4300c-405">Návěstí 2,0 obsahuje rozhraní s názvem `IHubCallerConnectionContext` v centrech, které usnadňuje vytváření postranních volání na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="4300c-405">SignalR 2.0 includes an interface called `IHubCallerConnectionContext` on Hubs that makes it easier to create mock client side invocations.</span></span> <span data-ttu-id="4300c-406">Následující fragmenty kódu ukazují použití tohoto rozhraní s oblíbenými testovacími [xUnit.NET](https://github.com/xunit/xunit) a [MOQ](https://code.google.com/p/moq/).</span><span class="sxs-lookup"><span data-stu-id="4300c-406">The following code snippets demonstrate using this interface with popular test harnesses [xUnit.net](https://github.com/xunit/xunit) and [moq](https://code.google.com/p/moq/).</span></span>

<span data-ttu-id="4300c-407">**Signál pro testování částí pomocí xUnit.net**</span><span class="sxs-lookup"><span data-stu-id="4300c-407">**Unit testing SignalR with xUnit.net**</span></span>

[!code-csharp[Main](release-notes/samples/sample18.cs)]

<span data-ttu-id="4300c-408">**Signál pro testování částí pomocí MOQ**</span><span class="sxs-lookup"><span data-stu-id="4300c-408">**Unit testing SignalR with moq**</span></span>

[!code-csharp[Main](release-notes/samples/sample19.cs)]

<a id="javascripterror"></a>

### <a name="javascript-error-handling"></a><span data-ttu-id="4300c-409">Zpracování chyb JavaScriptu</span><span class="sxs-lookup"><span data-stu-id="4300c-409">JavaScript error handling</span></span>

<span data-ttu-id="4300c-410">V nástroji Signal 2,0 všechny zpětná volání zpracovávající chyby JavaScriptu vrátí objekty chyb JavaScriptu místo nezpracovaných řetězců.</span><span class="sxs-lookup"><span data-stu-id="4300c-410">In SignalR 2.0, all JavaScript error handling callbacks return JavaScript error objects instead of raw strings.</span></span> <span data-ttu-id="4300c-411">Díky tomu může signál signalizovat bohatší informace obslužné rutiny chyb.</span><span class="sxs-lookup"><span data-stu-id="4300c-411">This allows SignalR to flow richer information to your error handlers.</span></span> <span data-ttu-id="4300c-412">Vnitřní výjimku můžete získat z vlastnosti `source` chyby.</span><span class="sxs-lookup"><span data-stu-id="4300c-412">You can get the inner exception from the `source` property of the error.</span></span>

<span data-ttu-id="4300c-413">**JavaScriptový kód klienta, který zpracovává výjimku spustit. neúspěch**</span><span class="sxs-lookup"><span data-stu-id="4300c-413">**JavaScript client code that handles the Start.Fail exception**</span></span>

[!code-javascript[Main](release-notes/samples/sample20.js)]

<a id="TOC8"></a>
## <a name="aspnet-identity"></a><span data-ttu-id="4300c-414">ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="4300c-414">ASP.NET Identity</span></span>

### <a name="new-aspnet-membership-system"></a><span data-ttu-id="4300c-415">Nový systém členství v ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4300c-415">New ASP.NET Membership System</span></span>

<span data-ttu-id="4300c-416">ASP.NET Identity je nový systém členství pro aplikace ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4300c-416">ASP.NET Identity is the new membership system for ASP.NET applications.</span></span> <span data-ttu-id="4300c-417">ASP.NET Identity usnadňuje integraci dat profilů specifických pro uživatele s daty aplikací.</span><span class="sxs-lookup"><span data-stu-id="4300c-417">ASP.NET Identity makes it easy to integrate user-specific profile data with application data.</span></span> <span data-ttu-id="4300c-418">ASP.NET Identity také umožňuje zvolit model trvalosti pro profily uživatelů v aplikaci.</span><span class="sxs-lookup"><span data-stu-id="4300c-418">ASP.NET Identity also allows you to choose the persistence model for user profiles in your application.</span></span> <span data-ttu-id="4300c-419">Data můžete ukládat do databáze SQL Server nebo do jiného úložiště dat, včetně úložišť dat NoSQL, jako jsou například Azure Storage tabulky.</span><span class="sxs-lookup"><span data-stu-id="4300c-419">You can store the data in a SQL Server database or another data store, including NoSQL data stores such as Azure Storage Tables.</span></span> <span data-ttu-id="4300c-420">Další informace naleznete v tématu [jednotlivé uživatelské účty](creating-web-projects-in-visual-studio.md#indauth) při **vytváření ASP.NET webových projektů v Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="4300c-420">For more information, see [Individual User Accounts](creating-web-projects-in-visual-studio.md#indauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="claims-based-authentication"></a><span data-ttu-id="4300c-421">Ověřování na základě deklarací</span><span class="sxs-lookup"><span data-stu-id="4300c-421">Claims-based authentication</span></span>

<span data-ttu-id="4300c-422">ASP.NET nyní podporuje ověřování založené na deklaracích, kde je identita uživatele reprezentována jako sada deklarací z důvěryhodného vystavitele.</span><span class="sxs-lookup"><span data-stu-id="4300c-422">ASP.NET now supports claims-based authentication, where the user's identity is represented as a set of claims from a trusted issuer.</span></span> <span data-ttu-id="4300c-423">Uživatele je možné ověřit pomocí uživatelského jména a hesla, které jsou zachovány v databázi aplikace, nebo pomocí poskytovatelů sociálních identit (například účty Microsoft, Facebook, Google, Twitter) nebo pomocí účtů organizace prostřednictvím Azure Active Directory nebo Active Directory Federation Services (AD FS) (ADFS).</span><span class="sxs-lookup"><span data-stu-id="4300c-423">Users can be authenticated using a username and password maintained in an application database, or using social identity providers (for example: Microsoft Accounts, Facebook, Google, Twitter), or using organizational accounts through Azure Active Directory or Active Directory Federation Services (ADFS).</span></span>

### <a name="integration-with-azure-active-directory-and-windows-server-active-directory"></a><span data-ttu-id="4300c-424">Integrace s Azure Active Directory a službou Windows Server Active Directory</span><span class="sxs-lookup"><span data-stu-id="4300c-424">Integration with Azure Active Directory and Windows Server Active Directory</span></span>

<span data-ttu-id="4300c-425">Nyní můžete vytvářet ASP.NET projekty, které pro ověřování používají Azure Active Directory nebo Windows Server Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="4300c-425">You can now create ASP.NET projects that use Azure Active Directory or Windows Server Active Directory (AD) for authentication.</span></span> <span data-ttu-id="4300c-426">Další informace najdete v tématu [účty organizace](creating-web-projects-in-visual-studio.md#orgauth) při **vytváření ASP.NET webových projektů v Visual Studio 2013**.</span><span class="sxs-lookup"><span data-stu-id="4300c-426">For more information, see [Organizational Accounts](creating-web-projects-in-visual-studio.md#orgauth) in **Creating ASP.NET Web Projects in Visual Studio 2013**.</span></span>

### <a name="owin-integration"></a><span data-ttu-id="4300c-427">Integrace OWIN</span><span class="sxs-lookup"><span data-stu-id="4300c-427">OWIN Integration</span></span>

<span data-ttu-id="4300c-428">Ověřování ASP.NET je teď založené na middlewaru OWIN, který se dá použít na jakémkoli hostiteli založeném na OWIN.</span><span class="sxs-lookup"><span data-stu-id="4300c-428">ASP.NET authentication is now based on OWIN middleware that can be used on any OWIN-based host.</span></span> <span data-ttu-id="4300c-429">Další informace o OWIN najdete v části následující [součásti Microsoft Owin](#TOC7) .</span><span class="sxs-lookup"><span data-stu-id="4300c-429">For more information about OWIN, see the following [Microsoft OWIN Components](#TOC7) section.</span></span>

<a id="TOC7"></a>
## <a name="microsoft-owin-components"></a><span data-ttu-id="4300c-430">Komponenty Microsoft OWIN</span><span class="sxs-lookup"><span data-stu-id="4300c-430">Microsoft OWIN Components</span></span>

<span data-ttu-id="4300c-431">[Open Web Interface for .NET](http://owin.org/) (Owin) definuje abstrakci mezi webovými servery .NET a webovými aplikacemi.</span><span class="sxs-lookup"><span data-stu-id="4300c-431">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="4300c-432">OWIN odpojí webovou aplikaci od serveru a vytváří tak webové aplikace Host-nezávislá.</span><span class="sxs-lookup"><span data-stu-id="4300c-432">OWIN decouples the web application from the server, making web applications host-agnostic.</span></span> <span data-ttu-id="4300c-433">Můžete například hostovat webovou aplikaci založenou na OWIN ve službě IIS nebo její vlastní hostování ve vlastním procesu.</span><span class="sxs-lookup"><span data-stu-id="4300c-433">For example, you can host an OWIN-based web application in IIS or self-host it in a custom process.</span></span>

<span data-ttu-id="4300c-434">Změny zavedené v součástech Microsoft OWIN (označované také jako projekt Katana) zahrnují nové součásti serveru a hostitele, nové pomocné knihovny a middlewaru a nový middleware ověřování.</span><span class="sxs-lookup"><span data-stu-id="4300c-434">Changes introduced in the Microsoft OWIN components (also known as the Katana project) include new server and host components, new helper libraries and middleware, and new authentication middleware.</span></span>

<span data-ttu-id="4300c-435">Další informace o OWIN a Katana najdete v tématu [co je nového v Owin a Katana](../../../aspnet/overview/owin-and-katana/index.md).</span><span class="sxs-lookup"><span data-stu-id="4300c-435">For more information about OWIN and Katana, see [What's new in OWIN and Katana](../../../aspnet/overview/owin-and-katana/index.md).</span></span>

<span data-ttu-id="4300c-436">**Poznámka: aplikace [Owin](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) nejde spustit v klasickém režimu služby IIS. musí být spuštěny v integrovaném režimu.**</span><span class="sxs-lookup"><span data-stu-id="4300c-436">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications cannot run in IIS classic mode; they must be run in integrated mode.**</span></span>

<span data-ttu-id="4300c-437">**Poznámka: aplikace [Owin](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) musí běžet v úplném vztahu důvěryhodnosti.**</span><span class="sxs-lookup"><span data-stu-id="4300c-437">**Note: [OWIN](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md) applications must be run in full trust.**</span></span>

### <a name="new-servers-and-hosts"></a><span data-ttu-id="4300c-438">Nové servery a hostitelé</span><span class="sxs-lookup"><span data-stu-id="4300c-438">New Servers and Hosts</span></span>

<span data-ttu-id="4300c-439">V této verzi byly přidány nové komponenty, které umožňují scénáře pro samoobslužné hostování.</span><span class="sxs-lookup"><span data-stu-id="4300c-439">With this release, new components were added to enable self-host scenarios.</span></span> <span data-ttu-id="4300c-440">Mezi tyto komponenty patří následující balíčky NuGet:</span><span class="sxs-lookup"><span data-stu-id="4300c-440">These components include the following NuGet packages:</span></span>

- <span data-ttu-id="4300c-441">**Microsoft. Owin. Host. HttpListener**.</span><span class="sxs-lookup"><span data-stu-id="4300c-441">**Microsoft.Owin.Host.HttpListener**.</span></span> <span data-ttu-id="4300c-442">Poskytuje server OWIN, který používá **HttpListener** k naslouchání požadavkům HTTP a jejich směrování do kanálu Owin.</span><span class="sxs-lookup"><span data-stu-id="4300c-442">Provides an OWIN server that uses **HttpListener** to listen for HTTP requests and direct them into the OWIN pipeline.</span></span>
- <span data-ttu-id="4300c-443">**Microsoft. Owin. hosting** poskytuje knihovnu pro vývojáře, kteří chtějí sami HOSTOVAT kanál Owin ve vlastním procesu, jako je například Konzolová aplikace nebo služba systému Windows.</span><span class="sxs-lookup"><span data-stu-id="4300c-443">**Microsoft.Owin.Hosting** Provides a library for developers who wish to self-host an OWIN pipeline in a custom process, such as a console application or Windows service.</span></span>
- <span data-ttu-id="4300c-444">**OwinHost**.</span><span class="sxs-lookup"><span data-stu-id="4300c-444">**OwinHost**.</span></span> <span data-ttu-id="4300c-445">Poskytuje samostatný spustitelný soubor, který zalomí `Microsoft.Owin.Hosting` a umožňuje vlastní hostování kanálu OWIN bez nutnosti psát vlastní hostitelskou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="4300c-445">Provides a stand-alone executable that wraps `Microsoft.Owin.Hosting` and lets you self-host an OWIN pipeline without having to write a custom host application.</span></span>

<span data-ttu-id="4300c-446">Kromě toho balíček `Microsoft.Owin.Host.SystemWeb` nyní umožňuje middlewaru poskytovat pokyn serveru **SystemWeb** , který označuje, že middleware by měly být volány během konkrétní fáze ASP.NET kanálu.</span><span class="sxs-lookup"><span data-stu-id="4300c-446">In addition, the `Microsoft.Owin.Host.SystemWeb` package now enables middleware to provide hints to the **SystemWeb** server, indicating that the middleware should be called during a specific ASP.NET pipeline stage.</span></span> <span data-ttu-id="4300c-447">Tato funkce je zvláště užitečná pro middleware ověřování, který by měl běžet na začátku v kanálu ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="4300c-447">This feature is particularly useful for authentication middleware, which should run early in the ASP.NET pipeline.</span></span>

### <a name="helper-libraries-and-middleware"></a><span data-ttu-id="4300c-448">Pomocné knihovny a middleware</span><span class="sxs-lookup"><span data-stu-id="4300c-448">Helper Libraries and Middleware</span></span>

<span data-ttu-id="4300c-449">I když můžete zapisovat komponenty OWIN jenom pomocí funkcí a definic typů ze specifikace OWIN, nový balíček `Microsoft.Owin` poskytuje uživatelsky přívětivější sadu abstrakcí.</span><span class="sxs-lookup"><span data-stu-id="4300c-449">Although you can write OWIN components using only the function and type definitions from the OWIN specification, the new `Microsoft.Owin` package provides a more user-friendly set of abstractions.</span></span> <span data-ttu-id="4300c-450">Tento balíček kombinuje několik starších balíčků (například `Owin.Extensions`, `Owin.Types`) do jednoho dobře strukturovaného objektového modelu, který lze následně snadno použít v jiných komponentách OWIN.</span><span class="sxs-lookup"><span data-stu-id="4300c-450">This package combines several earlier packages (e.g., `Owin.Extensions`, `Owin.Types`) into a single, well-structured object model that can then be easily used by other OWIN components.</span></span> <span data-ttu-id="4300c-451">Ve skutečnosti většina komponent Microsoft OWIN nyní používá tento balíček.</span><span class="sxs-lookup"><span data-stu-id="4300c-451">In fact, the majority of Microsoft OWIN components now use this package.</span></span>

> [!NOTE]
> <span data-ttu-id="4300c-452">Aplikace [Owin](http://www.owin.org) nemůžou běžet v klasickém režimu služby IIS. musí být spuštěny v integrovaném režimu.</span><span class="sxs-lookup"><span data-stu-id="4300c-452">[OWIN](http://www.owin.org) applications cannot run in IIS classic mode; they must be run in integrated mode.</span></span>

> [!NOTE]
> <span data-ttu-id="4300c-453">[Owin](http://www.owin.org) aplikace musí být spuštěny v úplném vztahu důvěryhodnosti.</span><span class="sxs-lookup"><span data-stu-id="4300c-453">[OWIN](http://www.owin.org) applications must be run in full trust.</span></span>

<span data-ttu-id="4300c-454">Tato verze zahrnuje také balíček Microsoft. Owin. Diagnostics, který zahrnuje middleware k ověření běžící aplikace OWIN a middlewaru chybových stránek, které vám pomůžou prozkoumat selhání.</span><span class="sxs-lookup"><span data-stu-id="4300c-454">This release also includes the Microsoft.Owin.Diagnostics package, which includes middleware to validate a running OWIN application, plus error-page middleware to help investigate failures.</span></span>

### <a name="authentication-components"></a><span data-ttu-id="4300c-455">Komponenty ověřování</span><span class="sxs-lookup"><span data-stu-id="4300c-455">Authentication Components</span></span>

<span data-ttu-id="4300c-456">K dispozici jsou následující komponenty pro ověřování.</span><span class="sxs-lookup"><span data-stu-id="4300c-456">The following authentication components are available.</span></span>

- <span data-ttu-id="4300c-457">**Microsoft. Owin. Security. Active**.</span><span class="sxs-lookup"><span data-stu-id="4300c-457">**Microsoft.Owin.Security.ActiveDirectory**.</span></span> <span data-ttu-id="4300c-458">Umožňuje ověřování pomocí místních nebo cloudových adresářových služeb.</span><span class="sxs-lookup"><span data-stu-id="4300c-458">Enables authentication using on-premise or cloud-based directory services.</span></span>
- <span data-ttu-id="4300c-459">**Microsoft. Owin. Security. cookies** umožňuje ověřování pomocí souborů cookie.</span><span class="sxs-lookup"><span data-stu-id="4300c-459">**Microsoft.Owin.Security.Cookies** Enables authentication using cookies.</span></span> <span data-ttu-id="4300c-460">Tento balíček se dřív jmenoval `Microsoft.Owin.Security.Forms`.</span><span class="sxs-lookup"><span data-stu-id="4300c-460">This package was previously named `Microsoft.Owin.Security.Forms`.</span></span>
- <span data-ttu-id="4300c-461">**Microsoft. Owin. Security. Facebook** umožňuje ověřování pomocí služby Facebook na Facebooku.</span><span class="sxs-lookup"><span data-stu-id="4300c-461">**Microsoft.Owin.Security.Facebook** Enables authentication using Facebook's OAuth-based service.</span></span>
- <span data-ttu-id="4300c-462">**Microsoft. Owin. Security. Google** umožňuje ověřování pomocí služby Google založené na OpenID.</span><span class="sxs-lookup"><span data-stu-id="4300c-462">**Microsoft.Owin.Security.Google** Enables authentication using Google's OpenID-based service.</span></span>
- <span data-ttu-id="4300c-463">**Microsoft. Owin. Security. JWT** umožňuje ověřování pomocí tokenů JWT.</span><span class="sxs-lookup"><span data-stu-id="4300c-463">**Microsoft.Owin.Security.Jwt** Enables authentication using JWT tokens.</span></span>
- <span data-ttu-id="4300c-464">**Microsoft. Owin. Security. MicrosoftAccount** umožňuje ověřování pomocí účtů Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4300c-464">**Microsoft.Owin.Security.MicrosoftAccount** Enables authentication using Microsoft accounts.</span></span>
- <span data-ttu-id="4300c-465">**Microsoft. Owin. Security. OAuth**.</span><span class="sxs-lookup"><span data-stu-id="4300c-465">**Microsoft.Owin.Security.OAuth**.</span></span> <span data-ttu-id="4300c-466">Poskytuje autorizační Server OAuth a také middleware pro ověřování nosných tokenů.</span><span class="sxs-lookup"><span data-stu-id="4300c-466">Provides an OAuth authorization server as well as middleware for authenticating bearer tokens.</span></span>
- <span data-ttu-id="4300c-467">**Microsoft. Owin. Security. Twitter** umožňuje ověřování pomocí služby Twitter na bázi OAuth.</span><span class="sxs-lookup"><span data-stu-id="4300c-467">**Microsoft.Owin.Security.Twitter** Enables authentication using Twitter's OAuth-based service.</span></span>

<span data-ttu-id="4300c-468">Tato verze zahrnuje také balíček `Microsoft.Owin.Cors`, který obsahuje middleware pro zpracování požadavků protokolu HTTP mezi zdroji.</span><span class="sxs-lookup"><span data-stu-id="4300c-468">This release also includes the `Microsoft.Owin.Cors` package, which contains middleware for processing cross-origin HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="4300c-469">V konečné verzi Visual Studio 2013 byla odebrána podpora pro podpis JWT.</span><span class="sxs-lookup"><span data-stu-id="4300c-469">Support for JWT signing has been removed in the final version of Visual Studio 2013.</span></span>

<a id="ef6"></a>
## <a name="entity-framework-6"></a><span data-ttu-id="4300c-470">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="4300c-470">Entity Framework 6</span></span>

<span data-ttu-id="4300c-471">Seznam nových funkcí a dalších změn v Entity Framework 6 najdete v části [Entity Framework Historie verzí](https://msdn.com/data/jj574253).</span><span class="sxs-lookup"><span data-stu-id="4300c-471">For a list of new features and other changes in Entity Framework 6, see [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<a id="TOC14"></a>
## <a name="aspnet-razor-3"></a><span data-ttu-id="4300c-472">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="4300c-472">ASP.NET Razor 3</span></span>

<span data-ttu-id="4300c-473">ASP.NET Razor 3 obsahuje následující nové funkce:</span><span class="sxs-lookup"><span data-stu-id="4300c-473">ASP.NET Razor 3 includes the following new features:</span></span>

- <span data-ttu-id="4300c-474">Podpora pro úpravu karet.</span><span class="sxs-lookup"><span data-stu-id="4300c-474">Support for Tab editing.</span></span> <span data-ttu-id="4300c-475">Dříve při použití možnosti **zachovat záložky** nefungovala v aplikaci Visual Studio příkaz **Formát dokumentu** , automatické odsazení a automatické formátování.</span><span class="sxs-lookup"><span data-stu-id="4300c-475">Previously, the **Format Document** command, auto indenting, and auto formatting in Visual Studio did not work correctly when using the **Keep Tabs** option.</span></span> <span data-ttu-id="4300c-476">Tato změna opravuje formátování sady Visual Studio pro kód Razor pro formátování tabulátoru.</span><span class="sxs-lookup"><span data-stu-id="4300c-476">This change corrects Visual Studio formatting for Razor code for tab formatting.</span></span>
- <span data-ttu-id="4300c-477">Podpora pravidel pro přepis adres URL při generování odkazů</span><span class="sxs-lookup"><span data-stu-id="4300c-477">Support for URL Rewrite rules when generating links.</span></span>
- <span data-ttu-id="4300c-478">Odebrání transparentního atributu zabezpečení</span><span class="sxs-lookup"><span data-stu-id="4300c-478">Removal of security transparent attribute.</span></span>
  > [!NOTE]
  > <span data-ttu-id="4300c-479">Toto je zásadní změna a má Razor 3 kompatibilní s MVC4 a starším, zatímco Razor 2 je nekompatibilní s MVC5 nebo sestaveními kompilovanými proti MVC5.</span><span class="sxs-lookup"><span data-stu-id="4300c-479">This is a breaking change, and makes Razor 3 incompatible with MVC4 and earlier, while Razor 2 is incompatible with MVC5 or assemblies compiled against MVC5.</span></span>

<span data-ttu-id="4300c-480">Problémy Razor 3 opravené ve Visual Studio 2013 z předběžných verzí najdete [tady](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="4300c-480">Razor 3 issues fixed in Visual Studio 2013 from pre-release versions can be found [here](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Resolved%7cClosed&type=All&priority=All&release=All%7cv5.0%2bPreview%7cv5.0%2bRC%7cv5.0%2bRTM&assignedTo=All&component=Web%2bPages%252fRazor&reasonClosed=Fixed&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

<a id="TOC15"></a>
## <a name="aspnet-app-suspend"></a><span data-ttu-id="4300c-481">Pozastavení aplikace ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4300c-481">ASP.NET App Suspend</span></span>

<span data-ttu-id="4300c-482">Pozastavení aplikace ASP.NET je funkce měnící hru v .NET Framework 4.5.1, která odmění uživatelské prostředí a ekonomický model pro hostování velkých počtů ASP.NET webů v jednom počítači.</span><span class="sxs-lookup"><span data-stu-id="4300c-482">ASP.NET App Suspend is a game-changing feature in the .NET Framework 4.5.1 that radically changes the user experience and economic model for hosting large numbers of ASP.NET sites on a single machine.</span></span> <span data-ttu-id="4300c-483">Další informace najdete v tématu [pozastavení aplikace ASP.NET – reagující na sdílené webové hostování .NET](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span><span class="sxs-lookup"><span data-stu-id="4300c-483">For more information, see [ASP.NET App Suspend – responsive shared .NET web hosting](https://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).</span></span>

<a id="knownissues"></a>
## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="4300c-484">Známé problémy a zásadní změny</span><span class="sxs-lookup"><span data-stu-id="4300c-484">Known Issues and Breaking Changes</span></span>

<span data-ttu-id="4300c-485">Tato část popisuje známé problémy a zásadní změny ASP.NET and Web Tools pro Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="4300c-485">This section describes known issues and breaking changes in the ASP.NET and Web Tools for Visual Studio 2013.</span></span>

### <a name="nuget"></a><span data-ttu-id="4300c-486">NuGet</span><span class="sxs-lookup"><span data-stu-id="4300c-486">NuGet</span></span>

- <span data-ttu-id="4300c-487">[Nové obnovení balíčku nefunguje na mono při použití souboru sln](https://nuget.codeplex.com/workitem/3596) – bude opraveno v nadcházejícím stažení NuGet. exe a aktualizace [balíčku NuGet. CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) .</span><span class="sxs-lookup"><span data-stu-id="4300c-487">[New package restore doesn't work on Mono when using SLN file](https://nuget.codeplex.com/workitem/3596) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="4300c-488">[Nové obnovení balíčku nefunguje s WIX projekty](https://nuget.codeplex.com/workitem/3598) – bude opraveno v nadcházejícím stažení NuGet. exe a aktualizace [balíčku NuGet. CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) .</span><span class="sxs-lookup"><span data-stu-id="4300c-488">[New package restore doesn't work with Wix projects](https://nuget.codeplex.com/workitem/3598) – will be fixed in an upcoming nuget.exe download and [NuGet.CommandLine package](http://www.nuget.org/packages/NuGet.CommandLine/) update.</span></span>
- <span data-ttu-id="4300c-489">[Automatické obnovení balíčku nefunguje pro projekty ve složce řešení](https://nuget.codeplex.com/workitem/3625) – bude opraveno v NuGet 2,8.</span><span class="sxs-lookup"><span data-stu-id="4300c-489">[Automatic Package restore doesn't work for projects under a solution folder](https://nuget.codeplex.com/workitem/3625) – will be fixed in NuGet 2.8.</span></span>

### <a name="aspnet-web-api"></a><span data-ttu-id="4300c-490">Rozhraní ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="4300c-490">ASP.NET Web API</span></span>

1. <span data-ttu-id="4300c-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` nevrací `IQueryable<T>` vždy, protože jsme přidali podporu pro `$select` a `$expand`.</span><span class="sxs-lookup"><span data-stu-id="4300c-491">`ODataQueryOptions<T>.ApplyTo(IQueryable)` doesn't return `IQueryable<T>` always, as we added support for `$select` and `$expand`.</span></span>

    <span data-ttu-id="4300c-492">Naše předchozí ukázky pro `ODataQueryOptions<T>` vždycky přetypování návratové hodnoty z `ApplyTo` na `IQueryable<T>`.</span><span class="sxs-lookup"><span data-stu-id="4300c-492">Our earlier samples for `ODataQueryOptions<T>` always casted the return value from `ApplyTo` to `IQueryable<T>`.</span></span> <span data-ttu-id="4300c-493">To dříve fungovalo, protože možnosti dotazu, které jsme dříve podporovali (`$filter`, `$orderby`, `$skip`, `$top`) nemění tvar dotazu.</span><span class="sxs-lookup"><span data-stu-id="4300c-493">This worked earlier because the query options that we supported earlier (`$filter`, `$orderby`, `$skip`, `$top`) do not change the shape of the query.</span></span> <span data-ttu-id="4300c-494">Teď, když podporujeme `$select` a `$expand` návratovou hodnotu z `ApplyTo` nebudou `IQueryable<T>` vždycky.</span><span class="sxs-lookup"><span data-stu-id="4300c-494">Now that we support `$select` and `$expand` the return value from `ApplyTo` will not be `IQueryable<T>` always.</span></span>

    [!code-csharp[Main](release-notes/samples/sample21.cs)]

    <span data-ttu-id="4300c-495">Pokud používáte vzorový kód ze starší verze, bude pokračovat v práci, pokud klient neodešle `$select` a `$expand`.</span><span class="sxs-lookup"><span data-stu-id="4300c-495">If you are using the sample code from earlier, it will continue working if the client does not send `$select` and `$expand`.</span></span> <span data-ttu-id="4300c-496">Pokud však chcete podporovat `$select` a `$expand` je nutné tento kód změnit.</span><span class="sxs-lookup"><span data-stu-id="4300c-496">However, if you wish to support `$select` and `$expand` you have to change that code to this.</span></span>

    [!code-csharp[Main](release-notes/samples/sample22.cs)]
2. <span data-ttu-id="4300c-497">**Request. URL nebo Třída requestContext. URL má během dávkového požadavku hodnotu null.**</span><span class="sxs-lookup"><span data-stu-id="4300c-497">**Request.Url or RequestContext.Url is null during a batch request**</span></span>

    <span data-ttu-id="4300c-498">V případě dávkového zpracování má **UrlHelper** při použití z **Request. URL** nebo **Třída requestContext. URL**hodnotu null.</span><span class="sxs-lookup"><span data-stu-id="4300c-498">In a batching scenario, **UrlHelper** is null when accessed from **Request.Url** or **RequestContext.Url**.</span></span>

    <span data-ttu-id="4300c-499">Tento problém je momentálně sledován: [BatchRequestContext. URL má pro požadavek Batch hodnotu null](http://aspnetwebstack.codeplex.com/workitem/1301).</span><span class="sxs-lookup"><span data-stu-id="4300c-499">This issue is currently tracked here: [BatchRequestContext.Url is null for batching request](http://aspnetwebstack.codeplex.com/workitem/1301).</span></span>

    <span data-ttu-id="4300c-500">Alternativním řešením tohoto problému je vytvoření nové instance **UrlHelper**, jako v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="4300c-500">The workaround for this issue is to create a new instance of **UrlHelper**, as in the following example:</span></span>

    <span data-ttu-id="4300c-501">**Vytváření nové instance třídy UrlHelper**</span><span class="sxs-lookup"><span data-stu-id="4300c-501">**Creating a new instance of UrlHelper**</span></span>

    [!code-csharp[Main](release-notes/samples/sample23.cs)]

### <a name="aspnet-mvc"></a><span data-ttu-id="4300c-502">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="4300c-502">ASP.NET MVC</span></span>

1. <span data-ttu-id="4300c-503">Pokud máte zobrazení, která se AntiForgerToken ověřováním, při použití MVC5 a OrgAuth může při odesílání dat do zobrazení docházet k následující chybě:</span><span class="sxs-lookup"><span data-stu-id="4300c-503">When using MVC5 and OrgAuth, if you have views which do AntiForgerToken validation, you might come across the following error when you post data to the view:</span></span>

    <span data-ttu-id="4300c-504">**Chyba**:</span><span class="sxs-lookup"><span data-stu-id="4300c-504">**Error**:</span></span>

    <span data-ttu-id="4300c-505">*Chyba serveru v aplikaci/*</span><span class="sxs-lookup"><span data-stu-id="4300c-505">*Server Error in '/' Application.*</span></span>

    <span data-ttu-id="4300c-506"><em>Deklarace identity typu<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>nebo<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>nebyla v poskytnutém hodnota ClaimsIdentity nalezena. Pokud chcete povolit podporu tokenů ochrany proti padělání pomocí ověřování založeného na deklaracích, ověřte prosím, jestli nakonfigurovaný zprostředkovatel deklarací poskytuje obě tyto deklarace na hodnota ClaimsIdentity instancích, které generuje. Pokud nakonfigurované zprostředkovatel deklarací místo toho používá jiný typ deklarace identity jako jedinečný identifikátor, dá se nakonfigurovat nastavením static Property AntiForgeryConfig. UniqueClaimTypeIdentifier.</em></span><span class="sxs-lookup"><span data-stu-id="4300c-506"><em>A claim of type '<http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier>' or '<https://schemas.microsoft.com/accesscontrolservice/2010/07/claims/identityprovider>' was not present on the provided ClaimsIdentity. To enable anti-forgery token support with claims-based authentication, please verify that the configured claims provider is providing both of these claims on the ClaimsIdentity instances it generates. If the configured claims provider instead uses a different claim type as a unique identifier, it can be configured by setting the static property AntiForgeryConfig.UniqueClaimTypeIdentifier.</em></span></span>

    <span data-ttu-id="4300c-507">**Alternativní řešení**:</span><span class="sxs-lookup"><span data-stu-id="4300c-507">**Workaround**:</span></span>

    <span data-ttu-id="4300c-508">Přidejte následující řádek do Global. asax k opravě:</span><span class="sxs-lookup"><span data-stu-id="4300c-508">Add the following line in Global.asax to fix it:</span></span>

    `AntiForgeryConfig.UniqueClaimTypeIdentifier = ClaimTypes.Name;`

    <span data-ttu-id="4300c-509">Tato akce bude opravena pro další vydání.</span><span class="sxs-lookup"><span data-stu-id="4300c-509">This will be fixed for the next release.</span></span>
2. <span data-ttu-id="4300c-510">Po upgradu aplikace MVC4 na MVC5 Sestavte řešení a spusťte ho.</span><span class="sxs-lookup"><span data-stu-id="4300c-510">After upgrading an MVC4 app to MVC5, build the solution and launch it.</span></span> <span data-ttu-id="4300c-511">Měla by se zobrazit následující chyba:</span><span class="sxs-lookup"><span data-stu-id="4300c-511">You should see the following error:</span></span>

    <span data-ttu-id="4300c-512">Určitého System. Web. webpages. Razor. Configuration. HostSection nelze přetypovat na [B] System. Web. webpages. Razor. Configuration. HostSection.</span><span class="sxs-lookup"><span data-stu-id="4300c-512">[A]System.Web.WebPages.Razor.Configuration.HostSection cannot be cast to [B]System.Web.WebPages.Razor.Configuration.HostSection.</span></span> <span data-ttu-id="4300c-513">Typ A pochází z ' System. Web. webpages. Razor, Version = 2.0.0.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 ' v kontextu ' default ' na pozici ' C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35 \ System. Web. webpages. Razor. dll '.</span><span class="sxs-lookup"><span data-stu-id="4300c-513">Type A originates from 'System.Web.WebPages.Razor, Version=2.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\windows\Microsoft.Net\assembly\GAC\_MSIL\System.Web.WebPages.Razor\v4.0\_2.0.0.0\_\_31bf3856ad364e35\System.Web.WebPages.Razor.dll'.</span></span> <span data-ttu-id="4300c-514">Typ B pochází z ' System. Web. webpages. Razor, Version = 3.0.0.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 ' v kontextu ' default ' na pozici ' C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01 \ System. Web. webpages. Razor. dll '.</span><span class="sxs-lookup"><span data-stu-id="4300c-514">Type B originates from 'System.Web.WebPages.Razor, Version=3.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' in the context 'Default' at location 'C:\Windows\Microsoft.NET\Framework\v4.0.30319\Temporary ASP.NET Files\root\6d05bbd0\e8b5908e\assembly\dl3\c9cbca63\f8910382\_6273ce01\System.Web.WebPages.Razor.dll'.</span></span>

    <span data-ttu-id="4300c-515">Chcete-li opravit uvedenou chybu, otevřete *všechny* soubory Web. config (včetně těch ve složce views) ve vašem projektu a proveďte následující kroky:</span><span class="sxs-lookup"><span data-stu-id="4300c-515">To fix the above error, open *all* the Web.config files (including the ones in the Views folder) in your project and do the following:</span></span>

   1. <span data-ttu-id="4300c-516">Aktualizuje všechny výskyty verze "4.0.0.0" z "System. Web. Mvc" na "5.0.0.0".</span><span class="sxs-lookup"><span data-stu-id="4300c-516">Update all occurrences of version "4.0.0.0" of "System.Web.Mvc" to "5.0.0.0".</span></span>
   2. <span data-ttu-id="4300c-517">Aktualizuje všechny výskyty verze "2.0.0.0" z "System. Web. helps", &quot;System. Web. webpages&quot; a &quot;System. Web. webpages. Razor&quot; na "3.0.0.0".</span><span class="sxs-lookup"><span data-stu-id="4300c-517">Update all occurrences of version "2.0.0.0" of "System.Web.Helpers", &quot;System.Web.WebPages&quot; and &quot;System.Web.WebPages.Razor&quot; to "3.0.0.0"</span></span>

      <span data-ttu-id="4300c-518">Například po provedení výše uvedených změn by vazby sestavení měly vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="4300c-518">For example, after you make the above changes, the assembly bindings should look like this:</span></span>

      [!code-xml[Main](release-notes/samples/sample24.xml)]

      <span data-ttu-id="4300c-519">Informace o tom, jak upgradovat projekty MVC 4 na MVC 5, najdete v tématu [Postup upgradu ASP.NET MVC 4 a projektu webového rozhraní API na ASP.NET MVC 5 a webové rozhraní API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span><span class="sxs-lookup"><span data-stu-id="4300c-519">For information on upgrading MVC 4 projects to MVC 5, see [How to Upgrade an ASP.NET MVC 4 and Web API Project to ASP.NET MVC 5 and Web API 2](../../../mvc/overview/releases/how-to-upgrade-an-aspnet-mvc-4-and-web-api-project-to-aspnet-mvc-5-and-web-api-2.md).</span></span>
3. <span data-ttu-id="4300c-520">Při ověřování na straně klienta s nenáročným ověřováním jQuery je ověřovací zpráva někdy nesprávná pro element input HTML s typem = ' Number '.</span><span class="sxs-lookup"><span data-stu-id="4300c-520">When using client-side validation with jQuery Unobtrusive Validation, the validation message is sometimes incorrect for an HTML input element with type='number'.</span></span> <span data-ttu-id="4300c-521">Při zadání neplatného čísla namísto správné zprávy, která vyžaduje platné číslo, se zobrazí chyba ověření požadované hodnoty (pole stáří je povinné).</span><span class="sxs-lookup"><span data-stu-id="4300c-521">The validation error for a required value ("The Age field is required") is shown when an invalid number is entered instead of the correct message that a valid number is required.</span></span>

    <span data-ttu-id="4300c-522">Tento problém se běžně objevuje s generovaným kódem pro model s vlastností Integer v zobrazeních vytvořit a upravit.</span><span class="sxs-lookup"><span data-stu-id="4300c-522">This issue is commonly found with scaffolded code for a model with an integer property on the Create and Edit views.</span></span>

    <span data-ttu-id="4300c-523">Pokud chcete tento problém obejít, změňte pomocníka editoru z:</span><span class="sxs-lookup"><span data-stu-id="4300c-523">To work around this issue, change the editor helper from:</span></span>

    `@Html.EditorFor(person => person.Age)`

    <span data-ttu-id="4300c-524">Na:</span><span class="sxs-lookup"><span data-stu-id="4300c-524">To:</span></span>

    `@Html.TextBoxFor(person => person.Age)`
4. <span data-ttu-id="4300c-525">ASP.NET MVC 5 už nepodporuje částečnou důvěryhodnost.</span><span class="sxs-lookup"><span data-stu-id="4300c-525">ASP.NET MVC 5 no longer supports partial trust.</span></span> <span data-ttu-id="4300c-526">Projekty, které propojuje s binárními soubory MVC nebo WebAPI, by měly odebrat atribut [atributy SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) a atribut [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4300c-526">Projects linking to the MVC or WebAPI binaries should remove the [SecurityTransparent](https://msdn.microsoft.com/library/system.security.securitytransparentattribute.aspx) attribute and the [AllowPartiallyTrustedCallers](https://msdn.microsoft.com/library/system.security.allowpartiallytrustedcallersattribute.aspx) attribute.</span></span> <span data-ttu-id="4300c-527">Odebrání těchto atributů odstraní chyby kompilátoru, například následující.</span><span class="sxs-lookup"><span data-stu-id="4300c-527">Removing these attributes will eliminate compiler errors such as the following.</span></span>

    `Attempt by security transparent method ‘MyComponent' to access security critical type 'System.Web.Mvc.MvcHtmlString' failed. Assembly 'PagedList.Mvc, Version=4.3.0.0, Culture=neutral, PublicKeyToken=abbb863e9397c5e1' is marked with the AllowPartiallyTrustedCallersAttribute, and uses the level 2 security transparency model. Level 2 transparency causes all methods in AllowPartiallyTrustedCallers assemblies to become security transparent by default, which may be the cause of this exception.`

    > <span data-ttu-id="4300c-528">Všimněte si, že v důsledku vedlejších účinků nelze ve stejné aplikaci použít sestavení 4,0 a 5,0.</span><span class="sxs-lookup"><span data-stu-id="4300c-528">Note, as a side effect of this you cannot use 4.0 and 5.0 assemblies in the same application.</span></span> <span data-ttu-id="4300c-529">Je potřeba je aktualizovat na 5,0.</span><span class="sxs-lookup"><span data-stu-id="4300c-529">You need to update all of them to 5.0.</span></span>

### <a name="spa-template-with-facebook-authorization-may-cause-instability-in-ie-while-the-web-site-is-hosted-in-intranet-zone"></a><span data-ttu-id="4300c-530">Šablona SPA s autorizací na Facebooku může způsobit nestabilitu v IE, pokud je web hostovaný v zóně intranetu.</span><span class="sxs-lookup"><span data-stu-id="4300c-530">SPA Template with Facebook authorization may cause instability in IE while the web site is hosted in intranet zone</span></span>

<span data-ttu-id="4300c-531">Šablona SPA poskytuje externí přihlášení pomocí Facebooku.</span><span class="sxs-lookup"><span data-stu-id="4300c-531">The SPA template provides external log in with Facebook.</span></span> <span data-ttu-id="4300c-532">Když je projekt vytvořený pomocí šablony místně spuštěný, přihlášení může způsobit chybu aplikace IE.</span><span class="sxs-lookup"><span data-stu-id="4300c-532">When the project created with the template is running locally, signing in may cause IE to crash.</span></span>

<span data-ttu-id="4300c-533">Řešení:</span><span class="sxs-lookup"><span data-stu-id="4300c-533">Solution:</span></span>

1. <span data-ttu-id="4300c-534">Hostování webu v zóně Internet; ani</span><span class="sxs-lookup"><span data-stu-id="4300c-534">Host the web site in internet zone; or</span></span>

2. <span data-ttu-id="4300c-535">Otestujte scénář v jiném prohlížeči než IE.</span><span class="sxs-lookup"><span data-stu-id="4300c-535">Test the scenario in a browser other than IE.</span></span>

### <a name="web-forms-scaffolding"></a><span data-ttu-id="4300c-536">Webové formuláře – generování uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="4300c-536">Web Forms Scaffolding</span></span>

<span data-ttu-id="4300c-537">Generování uživatelského rozhraní webových formulářů z VS2013 bylo odebráno a bude k dispozici v budoucí aktualizaci sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4300c-537">Web Forms Scaffolding has been removed from VS2013 and will be available in a future update to Visual Studio.</span></span> <span data-ttu-id="4300c-538">Můžete však i nadále používat generování uživatelského rozhraní v rámci projektu webových formulářů přidáním závislosti MVC a generováním generování uživatelského rozhraní pro MVC.</span><span class="sxs-lookup"><span data-stu-id="4300c-538">However, you can still use scaffolding within a Web Forms project by adding MVC dependencies and generating scaffolding for MVC.</span></span> <span data-ttu-id="4300c-539">Projekt bude obsahovat kombinaci webových formulářů a MVC.</span><span class="sxs-lookup"><span data-stu-id="4300c-539">Your project will contain a combination of Web Forms and MVC.</span></span>

<span data-ttu-id="4300c-540">Chcete-li přidat MVC do projektu webových formulářů, přidejte novou vygenerované položky a vyberte **závislosti MVC 5**.</span><span class="sxs-lookup"><span data-stu-id="4300c-540">To add MVC to your Web Forms project, add a new scaffolded item and select **MVC 5 Dependencies**.</span></span> <span data-ttu-id="4300c-541">V závislosti na tom, jestli potřebujete všechny soubory obsahu, jako jsou skripty, vyberte buď minimální, nebo úplné.</span><span class="sxs-lookup"><span data-stu-id="4300c-541">Select either Minimal or Full depending on whether you need all of the content files, such as scripts.</span></span> <span data-ttu-id="4300c-542">Pak přidejte vygenerované položky pro MVC, které vytvoří zobrazení a kontroler v projektu.</span><span class="sxs-lookup"><span data-stu-id="4300c-542">Then, add a scaffolded item for MVC, which will create views and a controller in your project.</span></span>

### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="4300c-543">Rozhraní API pro MVC a webové rozhraní API – chyba při nenalezení protokolu HTTP 404</span><span class="sxs-lookup"><span data-stu-id="4300c-543">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="4300c-544">Pokud při přidávání vygenerované položky do projektu dojde k chybě, je možné, že váš projekt zůstane v nekonzistentním stavu.</span><span class="sxs-lookup"><span data-stu-id="4300c-544">If an error is encountered when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="4300c-545">Některé změny generované generováním uživatelského rozhraní se vrátí zpátky, ale jiné změny, třeba nainstalované balíčky NuGet, se nebudou vracet zpátky.</span><span class="sxs-lookup"><span data-stu-id="4300c-545">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="4300c-546">Pokud se změny konfigurace směrování vrátí zpět, uživatelům se při přechodu na vygenerované položky zobrazí chyba HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="4300c-546">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="4300c-547">Alternativní řešení:</span><span class="sxs-lookup"><span data-stu-id="4300c-547">Workaround:</span></span>

- <span data-ttu-id="4300c-548">Pokud chcete tuto chybu pro MVC opravit, přidejte novou vygenerované položky a vyberte závislosti MVC 5 (minimální nebo plné).</span><span class="sxs-lookup"><span data-stu-id="4300c-548">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="4300c-549">Tento proces přidá všechny požadované změny do projektu.</span><span class="sxs-lookup"><span data-stu-id="4300c-549">This process will add all of the required changes to your project.</span></span>
- <span data-ttu-id="4300c-550">Oprava této chyby pro webové rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="4300c-550">To fix this error for Web API:</span></span>

  1. <span data-ttu-id="4300c-551">Přidejte do projektu třídu WebApiConfig.</span><span class="sxs-lookup"><span data-stu-id="4300c-551">Add the WebApiConfig class to your project.</span></span>

      [!code-csharp[Main](release-notes/samples/sample25.cs)]

      [!code-vb[Main](release-notes/samples/sample26.vb)]
  2. <span data-ttu-id="4300c-552">Nakonfigurujte WebApiConfig. Register v aplikaci\_metodu Start v Global. asax následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="4300c-552">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

      [!code-csharp[Main](release-notes/samples/sample27.cs)]

      [!code-vb[Main](release-notes/samples/sample28.vb)]

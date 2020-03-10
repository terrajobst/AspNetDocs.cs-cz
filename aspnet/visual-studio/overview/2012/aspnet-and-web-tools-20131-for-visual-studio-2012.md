---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: Poznámky k verzi pro ASP.NET and Web Tools 2013,1 pro Visual Studio 2012 | Microsoft Docs
author: microsoft
description: Tento dokument popisuje vydání ASP.NET and Web Tools 2013,1 pro sadu Visual Studio 2012.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 260af1018064d60d80cbb1002001f28c4daffffd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578440"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="1c23f-103">Poznámky k verzi pro ASP.NET a webové nástroje 2013.1 pro Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="1c23f-103">Release Notes for ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<span data-ttu-id="1c23f-104">od [Microsoftu](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="1c23f-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="1c23f-105">Tento dokument popisuje vydání ASP.NET and Web Tools 2013,1 pro sadu Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="1c23f-105">This document describes the release of ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

## <a name="contents"></a><span data-ttu-id="1c23f-106">Obsah</span><span class="sxs-lookup"><span data-stu-id="1c23f-106">Contents</span></span>

- [<span data-ttu-id="1c23f-107">Poznámky k instalaci</span><span class="sxs-lookup"><span data-stu-id="1c23f-107">Installation Notes</span></span>](#install)
- [<span data-ttu-id="1c23f-108">Požadavky na software</span><span class="sxs-lookup"><span data-stu-id="1c23f-108">Software Requirements</span></span>](#requirements)
- <span data-ttu-id="1c23f-109">Nové funkce v ASP.NET and Web Tools 2013,1 pro Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="1c23f-109">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

    - [<span data-ttu-id="1c23f-110">Bootstrap</span><span class="sxs-lookup"><span data-stu-id="1c23f-110">Bootstrap</span></span>](#bootstrap)
    - [<span data-ttu-id="1c23f-111">Šablony</span><span class="sxs-lookup"><span data-stu-id="1c23f-111">Templates</span></span>](#templates)

        - [<span data-ttu-id="1c23f-112">Šablona MVC 5 pro ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1c23f-112">ASP.NET MVC 5 template</span></span>](#mvc5template)
        - [<span data-ttu-id="1c23f-113">Šablona webového rozhraní API 2 pro ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1c23f-113">ASP.NET Web API 2 template</span></span>](#apitemplate)
        - [<span data-ttu-id="1c23f-114">Šablony položek</span><span class="sxs-lookup"><span data-stu-id="1c23f-114">Item Templates</span></span>](#itemtemplate)
    - [<span data-ttu-id="1c23f-115">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="1c23f-115">Entity Framework 6</span></span>](#ef6)
    - [<span data-ttu-id="1c23f-116">ASP.NET generování uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="1c23f-116">ASP.NET Scaffolding</span></span>](#scaffold)
    - [<span data-ttu-id="1c23f-117">Editor Razor</span><span class="sxs-lookup"><span data-stu-id="1c23f-117">Razor Editor</span></span>](#razor)
    - [<span data-ttu-id="1c23f-118">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="1c23f-118">NuGet 2.7</span></span>](#nuget)
- <span data-ttu-id="1c23f-119">Známé problémy a zásadní změny</span><span class="sxs-lookup"><span data-stu-id="1c23f-119">Known Issues and Breaking Changes</span></span>

    - [<span data-ttu-id="1c23f-120">ASP.NET generování uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="1c23f-120">ASP.NET Scaffolding</span></span>](#issuescaffolding)

        - [<span data-ttu-id="1c23f-121">Rozhraní API pro MVC a webové rozhraní API – chyba při nenalezení protokolu HTTP 404</span><span class="sxs-lookup"><span data-stu-id="1c23f-121">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>](#404issue)
        - [<span data-ttu-id="1c23f-122">Visual Studio Express 2012 pro web přestane fungovat po přidání vygenerované položky</span><span class="sxs-lookup"><span data-stu-id="1c23f-122">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>](#expressissue)
    - [<span data-ttu-id="1c23f-123">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="1c23f-123">ASP.NET Razor 3</span></span>](#issuerazor)

        - [<span data-ttu-id="1c23f-124">Zobrazení souboru CSHTML s procházením nebo F5 způsobuje chybu serveru</span><span class="sxs-lookup"><span data-stu-id="1c23f-124">Viewing cshtml file with Browse With or F5 causes a server error</span></span>](#browseissue)
        - [<span data-ttu-id="1c23f-125">Přepsání adresy URL a tilda (~)</span><span class="sxs-lookup"><span data-stu-id="1c23f-125">Url Rewrite and Tilde(~)</span></span>](#rewriteissue)
    - [<span data-ttu-id="1c23f-126">Šablony</span><span class="sxs-lookup"><span data-stu-id="1c23f-126">Templates</span></span>](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a><span data-ttu-id="1c23f-127">Poznámky k instalaci</span><span class="sxs-lookup"><span data-stu-id="1c23f-127">Installation Notes</span></span>

<span data-ttu-id="1c23f-128">[Nainstalovat](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013,1 pro Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="1c23f-128">[Install](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="requirements"></a>
## <a name="software-requirements"></a><span data-ttu-id="1c23f-129">Požadavky na software</span><span class="sxs-lookup"><span data-stu-id="1c23f-129">Software Requirements</span></span>

<span data-ttu-id="1c23f-130">Pro web musíte mít buď Visual Studio 2012, nebo Visual Studio Express 2012.</span><span class="sxs-lookup"><span data-stu-id="1c23f-130">You must have either Visual Studio 2012 or Visual Studio Express 2012 for Web.</span></span>

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a><span data-ttu-id="1c23f-131">Nové funkce v ASP.NET and Web Tools 2013,1 pro Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="1c23f-131">New Features in ASP.NET and Web Tools 2013.1 for Visual Studio 2012</span></span>

<a id="bootstrap"></a>
### <a name="bootstrap"></a><span data-ttu-id="1c23f-132">Spouštěcí rutina</span><span class="sxs-lookup"><span data-stu-id="1c23f-132">Bootstrap</span></span>

<span data-ttu-id="1c23f-133">Při generování uživatelského rozhraní a zobrazení řadiče MVC 5 označení pro zobrazení používá [bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="1c23f-133">When you scaffold MVC 5 controllers and views, the markup for the views uses [Bootstrap](http://getbootstrap.com/).</span></span>

<a id="templates"></a>
### <a name="templates"></a><span data-ttu-id="1c23f-134">Šablony</span><span class="sxs-lookup"><span data-stu-id="1c23f-134">Templates</span></span>

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a><span data-ttu-id="1c23f-135">Šablona MVC 5 pro ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1c23f-135">ASP.NET MVC 5 template</span></span>

<span data-ttu-id="1c23f-136">Přidali jsme novou šablonu MVC 5.</span><span class="sxs-lookup"><span data-stu-id="1c23f-136">We added a new MVC 5 template.</span></span> <span data-ttu-id="1c23f-137">Odkazuje na nejnovější balíčky NuGet sady MVC 5 a pomocí generování uživatelského rozhraní můžete přidat řadiče a zobrazení.</span><span class="sxs-lookup"><span data-stu-id="1c23f-137">It references the latest MVC 5 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a><span data-ttu-id="1c23f-138">Šablona webového rozhraní API 2 pro ASP.NET</span><span class="sxs-lookup"><span data-stu-id="1c23f-138">ASP.NET Web API 2 template</span></span>

<span data-ttu-id="1c23f-139">Přidali jsme novou šablonu webového rozhraní API 2.</span><span class="sxs-lookup"><span data-stu-id="1c23f-139">We added a new Web API 2 template.</span></span> <span data-ttu-id="1c23f-140">Odkazuje na nejnovější balíčky rozhraní Web API 2 NuGet a pomocí generování uživatelského rozhraní můžete přidat řadiče a zobrazení.</span><span class="sxs-lookup"><span data-stu-id="1c23f-140">It references the latest Web API 2 NuGet packages, and you can use scaffolding to add controllers and views.</span></span>

<a id="itemtemplate"></a>
#### <a name="item-templates"></a><span data-ttu-id="1c23f-141">Šablony položek</span><span class="sxs-lookup"><span data-stu-id="1c23f-141">Item Templates</span></span>

<span data-ttu-id="1c23f-142">Přidali jsme nové šablony položek pro zobrazení MVC 5, webové stránky (Razor 3) a ovladače webového rozhraní API 2.</span><span class="sxs-lookup"><span data-stu-id="1c23f-142">We added new item templates for MVC 5 views, Web Pages (Razor 3), and Web API 2 controllers.</span></span> <span data-ttu-id="1c23f-143">Při přidávání nových položek nainstalují do projektu související balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="1c23f-143">They install the related NuGet packages to the project while adding new items.</span></span>

<a id="ef6"></a>
### <a name="entity-framework-6"></a><span data-ttu-id="1c23f-144">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="1c23f-144">Entity Framework 6</span></span>

<span data-ttu-id="1c23f-145">Při generování uživatelského rozhraní MVC nebo kontroleru webového rozhraní API pomocí Entity Framework používáme rozhraní .NET Framework 6.</span><span class="sxs-lookup"><span data-stu-id="1c23f-145">When you scaffold an MVC or Web API controller using Entity Framework, we use Framework 6.</span></span> <span data-ttu-id="1c23f-146">Další informace o Entity Framework najdete v tématu [Historie verzí Entity Framework](https://msdn.com/data/jj574253).</span><span class="sxs-lookup"><span data-stu-id="1c23f-146">For more information about Entity Framework, see the [Entity Framework Version History](https://msdn.com/data/jj574253).</span></span>

<span data-ttu-id="1c23f-147">Můžete si také stáhnout a nainstalovat nástroje Entity Framework 6 pro Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="1c23f-147">You can also download and install the Entity Framework 6 Tools for Visual Studio 2012.</span></span> <span data-ttu-id="1c23f-148">Viz část [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span><span class="sxs-lookup"><span data-stu-id="1c23f-148">See the [Get Entity Framework](https://msdn.com/data/ee712906#tooling).</span></span>

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="1c23f-149">ASP.NET generování uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="1c23f-149">ASP.NET Scaffolding</span></span>

<span data-ttu-id="1c23f-150">Generování uživatelského rozhraní ASP.NET je rozhraní pro generování kódu pro webové aplikace v ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1c23f-150">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="1c23f-151">Umožňuje snadno přidat do projektu často používaný kód, který komunikuje s datovým modelem.</span><span class="sxs-lookup"><span data-stu-id="1c23f-151">It makes it easy to add boilerplate code to your project that interacts with a data model.</span></span>

<span data-ttu-id="1c23f-152">V předchozích verzích sady Visual Studio bylo generování uživatelského rozhraní omezeno na ASP.NET projekty MVC.</span><span class="sxs-lookup"><span data-stu-id="1c23f-152">In previous versions of Visual Studio, scaffolding was limited to ASP.NET MVC projects.</span></span> <span data-ttu-id="1c23f-153">V této aktualizaci teď můžete použít generování uživatelského rozhraní pro libovolný projekt ASP.NET, včetně webových formulářů.</span><span class="sxs-lookup"><span data-stu-id="1c23f-153">With this update, you can now use scaffolding for any ASP.NET project, including Web Forms.</span></span> <span data-ttu-id="1c23f-154">Tato aktualizace nepodporuje generování stránek pro projekt webových formulářů, ale můžete stále používat generování uživatelského rozhraní s webovými formuláři přidáním závislostí MVC do projektu.</span><span class="sxs-lookup"><span data-stu-id="1c23f-154">This update does not support generating pages for a Web Forms project, but you can still use scaffolding with Web Forms by adding MVC dependencies to the project.</span></span> <span data-ttu-id="1c23f-155">Do budoucí aktualizace se přidají podpora pro generování stránek webových formulářů.</span><span class="sxs-lookup"><span data-stu-id="1c23f-155">Support for generating pages for Web Forms will be added in a future update.</span></span>

<span data-ttu-id="1c23f-156">Při použití generování uživatelského rozhraní zajišťujeme, aby byly v projektu nainstalované všechny požadované závislosti.</span><span class="sxs-lookup"><span data-stu-id="1c23f-156">When using scaffolding, we ensure that all required dependencies are installed in the project.</span></span> <span data-ttu-id="1c23f-157">Například pokud začnete s projektem ASP.NET Web Forms a potom použijete generování uživatelského rozhraní pro přidání kontroleru webového rozhraní API, požadované balíčky NuGet a odkazy se automaticky přidají do projektu.</span><span class="sxs-lookup"><span data-stu-id="1c23f-157">For example, if you start with an ASP.NET Web Forms project and then use scaffolding to add a Web API Controller, the required NuGet packages and references are added to your project automatically.</span></span>

<span data-ttu-id="1c23f-158">Chcete-li přidat generování uživatelského rozhraní MVC do projektu webových formulářů, přidejte **novou vygenerované položky** a v dialogovém okně vyberte **závislosti MVC 5** .</span><span class="sxs-lookup"><span data-stu-id="1c23f-158">To add MVC scaffolding to a Web Forms project, add a **New Scaffolded Item** and select **MVC 5 Dependencies** in the dialog window.</span></span> <span data-ttu-id="1c23f-159">K dispozici jsou dvě možnosti pro generování uživatelského rozhraní MVC; Minimální a plná.</span><span class="sxs-lookup"><span data-stu-id="1c23f-159">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="1c23f-160">Pokud vyberete minimální, do projektu se přidají jenom balíčky NuGet a odkazy pro ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="1c23f-160">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="1c23f-161">Pokud vyberete možnost úplná, budou přidány minimální závislosti a také požadované soubory obsahu pro projekt MVC.</span><span class="sxs-lookup"><span data-stu-id="1c23f-161">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span>

<span data-ttu-id="1c23f-162">Podpora pro generování generovaných asynchronních řadičů používá nové asynchronní funkce z Entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="1c23f-162">Support for scaffolding async controllers uses the new async features from Entity Framework 6.</span></span>

<span data-ttu-id="1c23f-163">Další informace a kurzy najdete v tématu [Přehled generování uživatelského rozhraní ASP.NET](../2013/aspnet-scaffolding-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1c23f-163">For more information and tutorials, see [ASP.NET Scaffolding Overview](../2013/aspnet-scaffolding-overview.md).</span></span> <span data-ttu-id="1c23f-164">Tyto kurzy ukazují generování uživatelského rozhraní s Visual Studio 2013, ale platí také pro ASP.NET and Web Tools 2013,1 pro Visual Studio 2012.</span><span class="sxs-lookup"><span data-stu-id="1c23f-164">These tutorials show scaffolding with Visual Studio 2013, but they are also applicable to ASP.NET and Web Tools 2013.1 for Visual Studio 2012.</span></span>

<a id="razor"></a>
### <a name="razor-editor"></a><span data-ttu-id="1c23f-165">Editor Razor</span><span class="sxs-lookup"><span data-stu-id="1c23f-165">Razor Editor</span></span>

<span data-ttu-id="1c23f-166">V této aktualizaci Visual Studio 2012 teď podporuje nástroje a úpravy Razor 3.</span><span class="sxs-lookup"><span data-stu-id="1c23f-166">With this update, Visual Studio 2012 now supports Razor 3 tooling/editing.</span></span>

<a id="nuget"></a>
### <a name="nuget-27"></a><span data-ttu-id="1c23f-167">NuGet 2.7</span><span class="sxs-lookup"><span data-stu-id="1c23f-167">NuGet 2.7</span></span>

<span data-ttu-id="1c23f-168">NuGet 2,7 obsahuje bohatou sadu nových funkcí, které jsou podrobně popsány v [poznámkách k verzi nuget 2,7](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span><span class="sxs-lookup"><span data-stu-id="1c23f-168">NuGet 2.7 includes a rich set of new features which are described in detail at [NuGet 2.7 Release Notes](http://docs.nuget.org/docs/release-notes/nuget-2.7).</span></span>

<span data-ttu-id="1c23f-169">Tato verze NuGet neumožňuje uživatelům explicitně dovolit NuGet obnovovat chybějící balíčky.</span><span class="sxs-lookup"><span data-stu-id="1c23f-169">This version of NuGet removes the need for users to explicitly allow NuGet to restore missing packages.</span></span> <span data-ttu-id="1c23f-170">Při instalaci NuGet 2,7 budou uživatelé implicitně souhlasit s automatickým obnovením chybějících balíčků.</span><span class="sxs-lookup"><span data-stu-id="1c23f-170">When installing NuGet 2.7, users implicitly consent to automatically restoring missing packages.</span></span> <span data-ttu-id="1c23f-171">Uživatelé se můžou výslovně odhlásit z obnovení balíčků prostřednictvím nastavení NuGet v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1c23f-171">Users can explicitly opt out of package restoration through the NuGet settings in Visual Studio.</span></span> <span data-ttu-id="1c23f-172">Tato změna zjednodušuje způsob, jakým funguje obnovení balíčku.</span><span class="sxs-lookup"><span data-stu-id="1c23f-172">This change simplifies how package restoration works.</span></span>

## <a name="known-issues-and-breaking-changes"></a><span data-ttu-id="1c23f-173">Známé problémy a zásadní změny</span><span class="sxs-lookup"><span data-stu-id="1c23f-173">Known Issues and Breaking Changes</span></span>

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a><span data-ttu-id="1c23f-174">ASP.NET generování uživatelského rozhraní</span><span class="sxs-lookup"><span data-stu-id="1c23f-174">ASP.NET Scaffolding</span></span>

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a><span data-ttu-id="1c23f-175">Rozhraní API pro MVC a webové rozhraní API – chyba při nenalezení protokolu HTTP 404</span><span class="sxs-lookup"><span data-stu-id="1c23f-175">MVC and Web API Scaffolding - HTTP 404, Not Found error</span></span>

<span data-ttu-id="1c23f-176">Pokud narazíte na chybu při přidávání vygenerované položky do projektu, je možné, že váš projekt zůstane v nekonzistentním stavu.</span><span class="sxs-lookup"><span data-stu-id="1c23f-176">If you encounter an error when adding a scaffolded item to a project, it is possible your project will be left in an inconsistent state.</span></span> <span data-ttu-id="1c23f-177">Některé změny generované generováním uživatelského rozhraní se vrátí zpátky, ale jiné změny, třeba nainstalované balíčky NuGet, se nebudou vracet zpátky.</span><span class="sxs-lookup"><span data-stu-id="1c23f-177">Some of the changes made be scaffolding will be rolled back but other changes, such as the installed NuGet packages, will not be rolled back.</span></span> <span data-ttu-id="1c23f-178">Pokud se změny konfigurace směrování vrátí zpět, uživatelům se při přechodu na vygenerované položky zobrazí chyba HTTP 404.</span><span class="sxs-lookup"><span data-stu-id="1c23f-178">If the routing configuration changes are rolled back, users will receive an HTTP 404 error when navigating to scaffolded items.</span></span>

<span data-ttu-id="1c23f-179">Pokud chcete tuto chybu pro MVC opravit, přidejte novou vygenerované položky a vyberte závislosti MVC 5 (minimální nebo plné).</span><span class="sxs-lookup"><span data-stu-id="1c23f-179">To fix this error for MVC, add a new scaffolded item and select MVC 5 Dependencies (either Minimal or Full).</span></span> <span data-ttu-id="1c23f-180">Tento proces přidá všechny požadované změny do projektu.</span><span class="sxs-lookup"><span data-stu-id="1c23f-180">This process will add all of the required changes to your project.</span></span>

<span data-ttu-id="1c23f-181">Oprava této chyby pro webové rozhraní API:</span><span class="sxs-lookup"><span data-stu-id="1c23f-181">To fix this error for Web API:</span></span>

1. <span data-ttu-id="1c23f-182">Do projektu přidejte následující třídu WebApiConfig.</span><span class="sxs-lookup"><span data-stu-id="1c23f-182">Add the following WebApiConfig class to your project.</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. <span data-ttu-id="1c23f-183">Nakonfigurujte WebApiConfig. Register v aplikaci\_metodu Start v Global. asax následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="1c23f-183">Configure WebApiConfig.Register in the Application\_Start method in Global.asax as follows:</span></span>

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a><span data-ttu-id="1c23f-184">Visual Studio Express 2012 pro web přestane fungovat po přidání vygenerované položky</span><span class="sxs-lookup"><span data-stu-id="1c23f-184">Visual Studio Express 2012 for Web stops working after adding a scaffolded item</span></span>

<span data-ttu-id="1c23f-185">Pokud Visual Studio Express 2012 pro web přestane fungovat po přidání vygenerované položky s Entity Framework (například kontroler webového rozhraní API 2 s akcemi pomocí Entity Framework), je možné, že se Visual Studio Express nepodařilo načíst nativní bitovou kopii sestavení. závisí na System. Web. Extensions.</span><span class="sxs-lookup"><span data-stu-id="1c23f-185">If Visual Studio Express 2012 for Web stops working after adding scaffolded item with Entity Framework (such as Web API 2 Controller with actions, using Entity Framework), it is possible that Visual Studio Express failed to load the native image of an assembly dependent on System.Web.Extensions.</span></span>

<span data-ttu-id="1c23f-186">Chcete-li tento problém vyřešit, nakonfigurujte Visual Studio Express pro práci s imagí jazyka MSIL typu System. Web. Extensions:</span><span class="sxs-lookup"><span data-stu-id="1c23f-186">To correct this problem, configure Visual Studio Express to work with the MSIL image of System.Web.Extensions:</span></span>

1. <span data-ttu-id="1c23f-187">Otevřete příkazový řádek v režimu správce.</span><span class="sxs-lookup"><span data-stu-id="1c23f-187">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="1c23f-188">Přejít na%ProgramFiles%\Microsoft Visual Studio 11.0 \ Common7\IDE nebo% ProgramFiles (x86)% \ Microsoft Visual Studio 11.0 \ Common7\IDE (pro 64 bitových oken).</span><span class="sxs-lookup"><span data-stu-id="1c23f-188">Go to %ProgramFiles%\Microsoft Visual Studio 11.0\Common7\IDE or %ProgramFiles(x86)%\Microsoft Visual Studio 11.0\Common7\IDE (for 64 bit Windows).</span></span>
3. <span data-ttu-id="1c23f-189">V textovém editoru otevřete soubor VWDExpress. exe. config.</span><span class="sxs-lookup"><span data-stu-id="1c23f-189">Open VWDExpress.exe.config in a text editor.</span></span>
4. <span data-ttu-id="1c23f-190">Přidejte následující řádek pod &lt;konfigurační&gt;/&lt;modulu runtime&gt;:</span><span class="sxs-lookup"><span data-stu-id="1c23f-190">Add the following line under the &lt;configuration&gt;/&lt;runtime&gt; element:</span></span>  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. <span data-ttu-id="1c23f-191">Restartujte Visual Studio Express 2012 pro web.</span><span class="sxs-lookup"><span data-stu-id="1c23f-191">Restart Visual Studio Express 2012 for Web.</span></span>

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a><span data-ttu-id="1c23f-192">ASP.NET Razor 3</span><span class="sxs-lookup"><span data-stu-id="1c23f-192">ASP.NET Razor 3</span></span>

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a><span data-ttu-id="1c23f-193">Zobrazení souboru CSHTML s procházením nebo F5 způsobuje chybu serveru</span><span class="sxs-lookup"><span data-stu-id="1c23f-193">Viewing cshtml file with Browse With or F5 causes a server error</span></span>

<span data-ttu-id="1c23f-194">Když vytvoříte projekt MVC 5 v aplikaci Visual Studio 2012 (nebo otevřete v aplikaci Visual Studio 2012 projekt MVC 5, který byl vytvořen v Visual Studio 2013), a pokusíte se zobrazit soubor cshtml pomocí příkazu procházet s nebo F5, zobrazí se chyba oznamující, že **Chyba serveru v aplikaci/** .</span><span class="sxs-lookup"><span data-stu-id="1c23f-194">When you create an MVC 5 project in Visual Studio 2012 (or open in Visual Studio 2012 an MVC 5 project that was created in Visual Studio 2013) and attempt to view a cshtml file by using Browse With or F5, you will receive an error that states - **Server Error in '/' Application**.</span></span> <span data-ttu-id="1c23f-195">Server se pokusí přejít na `http://localhost:XXXX/Views/../XXXX.cshtml`</span><span class="sxs-lookup"><span data-stu-id="1c23f-195">The server attempts to navigate to `http://localhost:XXXX/Views/../XXXX.cshtml`</span></span>

<span data-ttu-id="1c23f-196">Chcete-li tento problém vyřešit, změňte nastavení **Akce spuštění** v projektu na **konkrétní stránku**.</span><span class="sxs-lookup"><span data-stu-id="1c23f-196">To resolve this issue, change the **Start Action** setting in your project to **Specific Page**.</span></span> <span data-ttu-id="1c23f-197">Pro stránku nemusíte zadávat hodnotu.</span><span class="sxs-lookup"><span data-stu-id="1c23f-197">You do not need to provide a value for the page.</span></span>

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

<span data-ttu-id="1c23f-198">Po provedení této změny vyberete F5 přejít na kořen vaší aplikace (`http://localhost:XXXX`).</span><span class="sxs-lookup"><span data-stu-id="1c23f-198">After making this change, selecting F5 navigates to the root of your application (`http://localhost:XXXX`).</span></span> <span data-ttu-id="1c23f-199">Toto chování není stejné jako chování pro projekty MVC 5 v Visual Studio 2013, kde **aktuální nastavení stránky** spouští otevřenou stránku.</span><span class="sxs-lookup"><span data-stu-id="1c23f-199">This behavior is not the same as the behavior for MVC 5 projects in Visual Studio 2013, where the **Current Page** setting launches the open page.</span></span>

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a><span data-ttu-id="1c23f-200">Přepsání adresy URL a tilda (~)</span><span class="sxs-lookup"><span data-stu-id="1c23f-200">Url Rewrite and Tilde(~)</span></span>

<span data-ttu-id="1c23f-201">Po upgradu na ASP.NET Razor 3 nebo ASP.NET MVC 5 již nemusí zápis tildy (~) fungovat správně, pokud používáte přepisy URL.</span><span class="sxs-lookup"><span data-stu-id="1c23f-201">After upgrading to ASP.NET Razor 3 or ASP.NET MVC 5, the tilde(~) notation may no longer work correctly if you are using URL rewrites.</span></span> <span data-ttu-id="1c23f-202">Přepsání adresy URL má vliv na znak tilda (~) v prvcích HTML, jako je například &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, a v důsledku toho není tilda nadále namapována do kořenového adresáře.</span><span class="sxs-lookup"><span data-stu-id="1c23f-202">The URL rewrite affects the tilde(~) notation in HTML elements such as &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, and as a result the tilde no longer maps to the root directory.</span></span>

<span data-ttu-id="1c23f-203">Například pokud přepíšete požadavky pro **ASP.NET/Content** do **ASP.NET**, atribut href v &lt;a href = "~/content/"/&gt; překládá na **/Content/Content/** namísto **/** .</span><span class="sxs-lookup"><span data-stu-id="1c23f-203">For example, if you rewrite requests for **asp.net/content** to **asp.net**, the href attribute in &lt;A href="~/content/"/&gt; resolves to **/content/content/** instead of **/**.</span></span> <span data-ttu-id="1c23f-204">Chcete-li tuto změnu potlačit, můžete nastavit **WasUrlRewritten kontext služby IIS\_** na hodnotu false na každé webové stránce nebo v **aplikaci\_beginRequest** v souboru Global. asax.</span><span class="sxs-lookup"><span data-stu-id="1c23f-204">To suppress this change, you can set the **IIS\_WasUrlRewritten** context to false in each Web Page or in **Application\_BeginRequest** in Global.asax.</span></span>

<a id="templateissue"></a>
### <a name="templates"></a><span data-ttu-id="1c23f-205">Šablony</span><span class="sxs-lookup"><span data-stu-id="1c23f-205">Templates</span></span>

<span data-ttu-id="1c23f-206">Když vytváříte projekty ASP.NET MVC pomocí sady Visual Studio 2012 v systému Windows 8.1 nebo Windows Server 2012 R2, Visual Studio zobrazí chybovou zprávu s informací o tom, že se nezdařila konfigurace webu [URL] pro ASP.NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="1c23f-206">When you create ASP.NET MVC projects with Visual Studio 2012 on Windows 8.1 or Windows Server 2012 R2, Visual Studio displays an error message that states "Configuring Web [url] for ASP.NET 4.5 failed."</span></span>

![Chyba konfigurace](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

<span data-ttu-id="1c23f-208">Tato chyba se zobrazí, protože Visual Studio 2012 nepovoluje funkci ASP.NET 4,5, když je nainstalovaná v těchto verzích Windows.</span><span class="sxs-lookup"><span data-stu-id="1c23f-208">You see this error because Visual Studio 2012 does not enable the ASP.NET 4.5 feature when it is installed on those releases of Windows.</span></span> <span data-ttu-id="1c23f-209">Pokud chcete povolit ASP.NET 4,5, postupujte podle kroků popsaných v tématu [Zapnutí nebo vypnutí funkcí systému Windows](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span><span class="sxs-lookup"><span data-stu-id="1c23f-209">To enable ASP.NET 4.5, perform the steps described in [Turn Windows features on or off](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).</span></span>

![Zapnutí nebo vypnutí funkcí Windows](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

<span data-ttu-id="1c23f-211">Alternativně můžete povolit ASP.NET 4,5 prostřednictvím příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="1c23f-211">Alternatively, you can enable ASP.NET 4.5 through the command line.</span></span>

1. <span data-ttu-id="1c23f-212">Otevřete příkazový řádek v režimu správce.</span><span class="sxs-lookup"><span data-stu-id="1c23f-212">Open Command Prompt in the Administrator mode.</span></span>
2. <span data-ttu-id="1c23f-213">Spusťte následující příkaz, který povolí ASP.NET 4,5.</span><span class="sxs-lookup"><span data-stu-id="1c23f-213">Run the following command to enable ASP.NET 4.5.</span></span>  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`

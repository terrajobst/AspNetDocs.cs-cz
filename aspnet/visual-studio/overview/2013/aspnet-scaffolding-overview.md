---
uid: visual-studio/overview/2013/aspnet-scaffolding-overview
title: ASP.NET generování uživatelského rozhraní v Visual Studio 2013 | Microsoft Docs
author: Rick-Anderson
description: ASP.NET generování uživatelského rozhraní je nová funkce, která je součástí Visual Studio 2013.
ms.author: riande
ms.date: 04/09/2014
ms.assetid: a41ec9d4-8287-4f31-9e2a-460e7b7f04be
msc.legacyurl: /visual-studio/overview/2013/aspnet-scaffolding-overview
msc.type: authoredcontent
ms.openlocfilehash: cf4669b769cee28475e2dd6a6ddf07ea1434d04d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557979"
---
# <a name="aspnet-scaffolding-in-visual-studio-2013"></a><span data-ttu-id="16a7e-103">Vygenerování uživatelského rozhraní ASP.NET v sadě Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="16a7e-103">ASP.NET Scaffolding in Visual Studio 2013</span></span>

<span data-ttu-id="16a7e-104">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="16a7e-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="16a7e-105">ASP.NET generování uživatelského rozhraní je nová funkce, která je součástí Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="16a7e-105">ASP.NET Scaffolding is a new feature that is included in Visual Studio 2013.</span></span>

## <a name="overview"></a><span data-ttu-id="16a7e-106">Přehled</span><span class="sxs-lookup"><span data-stu-id="16a7e-106">Overview</span></span>

<span data-ttu-id="16a7e-107">Generování uživatelského rozhraní ASP.NET je rozhraní pro generování kódu pro webové aplikace v ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="16a7e-107">ASP.NET Scaffolding is a code generation framework for ASP.NET Web applications.</span></span> <span data-ttu-id="16a7e-108">Visual Studio 2013 obsahuje předem instalované generátory kódu pro MVC a projekty webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="16a7e-108">Visual Studio 2013 includes pre-installed code generators for MVC and Web API projects.</span></span> <span data-ttu-id="16a7e-109">Pokud chcete rychle přidat kód, který komunikuje s datovými modely, přidejte do projektu generování uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="16a7e-109">You add scaffolding to your project when you want to quickly add code that interacts with data models.</span></span> <span data-ttu-id="16a7e-110">Použití generování uživatelského rozhraní může zkrátit dobu vývoje standardních datových operací v projektu.</span><span class="sxs-lookup"><span data-stu-id="16a7e-110">Using scaffolding can reduce the amount of time to develop standard data operations in your project.</span></span>

<span data-ttu-id="16a7e-111">Ve výchozím nastavení Visual Studio 2013 nepodporuje generování kódu pro projekt webových formulářů, ale můžete použít generování uživatelského rozhraní s webovými formuláři, a to buď přidáním závislosti MVC do projektu, nebo instalací rozšíření.</span><span class="sxs-lookup"><span data-stu-id="16a7e-111">By default, Visual Studio 2013 does not support generating code for a Web Forms project, but you can use scaffolding with Web Forms by either adding MVC dependencies to the project or installing an extension.</span></span> <span data-ttu-id="16a7e-112">Oba přístupy jsou uvedené níže.</span><span class="sxs-lookup"><span data-stu-id="16a7e-112">Both approaches are shown below.</span></span>

<span data-ttu-id="16a7e-113">Visual Studio 2013 Update 2 (aktuálně RC) poskytuje možnost rozšiřování ASP.NET generování uživatelského rozhraní tak, aby splňovalo požadavky vašeho scénáře.</span><span class="sxs-lookup"><span data-stu-id="16a7e-113">Visual Studio 2013 Update 2 (currently RC) provides the ability to extend ASP.NET Scaffolding to meet the requirements of your scenario.</span></span> <span data-ttu-id="16a7e-114">Pomocí této funkce můžete vytvořit vlastní šablonu generování uživatelského rozhraní a přidat ji do dialogového okna Přidat nové generování uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="16a7e-114">With this functionality, you can create a customized scaffolding template and add it to Add New Scaffold dialog.</span></span> <span data-ttu-id="16a7e-115">V rámci vlastní šablony určíte kód, který se generuje při přidávání vygenerované položky.</span><span class="sxs-lookup"><span data-stu-id="16a7e-115">Within the customized template, you specify the code that is generated when adding a scaffolded item.</span></span> <span data-ttu-id="16a7e-116">Další informace najdete v tématu [Vytvoření vlastního lešení pro Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span><span class="sxs-lookup"><span data-stu-id="16a7e-116">For more information, see [Creating a Custom Scaffolder for Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="16a7e-117">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="16a7e-117">Prerequisites</span></span>

<span data-ttu-id="16a7e-118">Chcete-li použít generování uživatelského rozhraní ASP.NET, musíte mít:</span><span class="sxs-lookup"><span data-stu-id="16a7e-118">To use ASP.NET Scaffolding, you must have:</span></span>

- <span data-ttu-id="16a7e-119">Microsoft Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="16a7e-119">Microsoft Visual Studio 2013</span></span>
- <span data-ttu-id="16a7e-120">Web Vývojářské nástroje (součást výchozí instalace Visual Studio 2013)</span><span class="sxs-lookup"><span data-stu-id="16a7e-120">Web Developer Tools (part of default Visual Studio 2013 installation)</span></span>
- <span data-ttu-id="16a7e-121">ASP.NET webová rozhraní a nástroje 2013 (součást výchozí instalace Visual Studio 2013)</span><span class="sxs-lookup"><span data-stu-id="16a7e-121">ASP.NET Web Frameworks and Tools 2013 (part of default Visual Studio 2013 installation)</span></span>

## <a name="add-a-scaffolded-item-to-mvc-or-web-api"></a><span data-ttu-id="16a7e-122">Přidání vygenerované položky do MVC nebo webového rozhraní API</span><span class="sxs-lookup"><span data-stu-id="16a7e-122">Add a scaffolded item to MVC or Web API</span></span>

<span data-ttu-id="16a7e-123">Chcete-li přidat generování uživatelského rozhraní, klikněte pravým tlačítkem myši buď na projekt, nebo na složku v rámci projektu, a vyberte možnost **Přidat** – **Nová vygenerovaná položka**, jak je znázorněno na následujícím obrázku.</span><span class="sxs-lookup"><span data-stu-id="16a7e-123">To add a scaffold, right-click either the project or a folder within the project, and select **Add** – **New Scaffolded Item**, as shown in the following image.</span></span>

![Přidat položku uživatelského rozhraní](aspnet-scaffolding-overview/_static/image1.png)

<span data-ttu-id="16a7e-125">V okně **Přidat generování uživatelského rozhraní** vyberte typ uživatelského rozhraní, které chcete přidat.</span><span class="sxs-lookup"><span data-stu-id="16a7e-125">From the **Add Scaffold** window, select the type of scaffold to add.</span></span>

![Vybrat typ uživatelského rozhraní](aspnet-scaffolding-overview/_static/image2.png)

<span data-ttu-id="16a7e-127">Okno **Přidat kontrolér** nabízí možnost vybrat možnosti pro vygenerování kontroleru, včetně toho, jestli chcete použít nové asynchronní funkce z Entity Framework 6.</span><span class="sxs-lookup"><span data-stu-id="16a7e-127">The **Add Controller** window gives you the opportunity to select options for generating the controller, including whether you want to use the new async features from Entity Framework 6.</span></span>

![Přidat kontroler](aspnet-scaffolding-overview/_static/image3.png)

<span data-ttu-id="16a7e-129">Pro váš scénář jsou vytvořeny relevantní třídy a stránky.</span><span class="sxs-lookup"><span data-stu-id="16a7e-129">The relevant classes and pages are created for your scenario.</span></span> <span data-ttu-id="16a7e-130">Například následující obrázek ukazuje kontroler MVC a zobrazení, které byly vytvořeny pomocí generování uživatelského rozhraní pro třídu modelu s názvem filmy.</span><span class="sxs-lookup"><span data-stu-id="16a7e-130">For example, the following image shows the MVC controller and views that were created through scaffolding for a model class named Movies.</span></span>

![Vytvořené soubory](aspnet-scaffolding-overview/_static/image4.png)

## <a name="add-a-scaffolded-item-to-web-forms"></a><span data-ttu-id="16a7e-132">Přidání vygenerované položky do webových formulářů</span><span class="sxs-lookup"><span data-stu-id="16a7e-132">Add a scaffolded item to Web Forms</span></span>

<span data-ttu-id="16a7e-133">Chcete-li přidat generování uživatelského rozhraní, které generuje kód webových formulářů, je nutné buď nainstalovat rozšíření do sady Visual Studio, nebo přidat závislosti MVC.</span><span class="sxs-lookup"><span data-stu-id="16a7e-133">To add scaffolding that generates Web Forms code, you must either install an extension to Visual Studio or add MVC dependencies.</span></span> <span data-ttu-id="16a7e-134">Oba přístupy jsou uvedené níže, ale stačí udělat jenom jeden z těchto přístupů.</span><span class="sxs-lookup"><span data-stu-id="16a7e-134">Both approaches are shown below, but you only need to do one of these approaches.</span></span>

### <a name="web-forms-scaffolding-extension"></a><span data-ttu-id="16a7e-135">Rozšíření pro generování uživatelského rozhraní webových formulářů</span><span class="sxs-lookup"><span data-stu-id="16a7e-135">Web Forms Scaffolding Extension</span></span>

<span data-ttu-id="16a7e-136">Můžete nainstalovat rozšíření sady Visual Studio, které vám umožní používat generování uživatelského rozhraní s projektem webových formulářů.</span><span class="sxs-lookup"><span data-stu-id="16a7e-136">You can install a Visual Studio extension that enable you to use scaffolding with a Web Forms project.</span></span> <span data-ttu-id="16a7e-137">V aplikaci Visual Studio vyberte **nástroje** a pak **rozšíření a aktualizace**.</span><span class="sxs-lookup"><span data-stu-id="16a7e-137">In Visual Studio, select **Tools** and then **Extensions and Updates**.</span></span> <span data-ttu-id="16a7e-138">Z tohoto dialogového okna vyhledejte galerii sady Visual Studio pro **vygenerování uživatelského rozhraní webových formulářů**.</span><span class="sxs-lookup"><span data-stu-id="16a7e-138">From this dialog search the Visual Studio Gallery for **Web Forms Scaffolding**.</span></span>

![instalace generování uživatelského rozhraní webových formulářů](aspnet-scaffolding-overview/_static/image5.png)

<span data-ttu-id="16a7e-140">Další informace najdete v tématu [generování uživatelského rozhraní webových formulářů](https://go.microsoft.com/fwlink/p/?LinkId=396478).</span><span class="sxs-lookup"><span data-stu-id="16a7e-140">For more information, see [Web Forms Scaffolding](https://go.microsoft.com/fwlink/p/?LinkId=396478).</span></span>

### <a name="mvc-dependencies"></a><span data-ttu-id="16a7e-141">Závislosti MVC</span><span class="sxs-lookup"><span data-stu-id="16a7e-141">MVC Dependencies</span></span>

<span data-ttu-id="16a7e-142">Chcete-li přidat závislosti MVC, vyberte **přidat** - **Nová vygenerovaná položka**.</span><span class="sxs-lookup"><span data-stu-id="16a7e-142">To add MVC dependencies, select **Add** - **New Scaffolded Item**.</span></span> <span data-ttu-id="16a7e-143">V okně Přidat generování uživatelského rozhraní vyberte **závislosti MVC**, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="16a7e-143">In the Add Scaffold window, select **MVC Dependencies**, as shown below.</span></span>

![přidat závislosti MVC](aspnet-scaffolding-overview/_static/image6.png)

<span data-ttu-id="16a7e-145">K dispozici jsou dvě možnosti pro generování uživatelského rozhraní MVC; Minimální a plná.</span><span class="sxs-lookup"><span data-stu-id="16a7e-145">There are two options for scaffolding MVC; Minimal and Full.</span></span> <span data-ttu-id="16a7e-146">Pokud vyberete minimální, do projektu se přidají jenom balíčky NuGet a odkazy pro ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="16a7e-146">If you select Minimal, only the NuGet packages and references for ASP.NET MVC are added to your project.</span></span> <span data-ttu-id="16a7e-147">Pokud vyberete možnost úplná, budou přidány minimální závislosti a také požadované soubory obsahu pro projekt MVC.</span><span class="sxs-lookup"><span data-stu-id="16a7e-147">If you select the Full option, the Minimal dependencies are added, as well as the required content files for an MVC project.</span></span> <span data-ttu-id="16a7e-148">Chcete-li snadno používat generování uživatelského rozhraní, vyberte možnost úplné závislosti.</span><span class="sxs-lookup"><span data-stu-id="16a7e-148">To easily use scaffolding, select Full dependencies.</span></span>

![Výběr úplných závislostí](aspnet-scaffolding-overview/_static/image7.png)

<span data-ttu-id="16a7e-150">Po přidání závislostí se zobrazí soubor **Readme. txt** .</span><span class="sxs-lookup"><span data-stu-id="16a7e-150">After adding the dependencies, you will see a **readme.txt** file.</span></span> <span data-ttu-id="16a7e-151">Pečlivě postupujte podle pokynů v tomto souboru a ujistěte se, že váš projekt funguje správně.</span><span class="sxs-lookup"><span data-stu-id="16a7e-151">Carefully follow the instructions in this file to ensure that your project works correctly.</span></span>

<span data-ttu-id="16a7e-152">Po dokončení kroků v souboru Readme. txt můžete přidat novou vygenerované položky, jak je znázorněno v předchozí části o MVC a webovém rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="16a7e-152">When you have completed the steps in the readme.txt file, you can add a new scaffolded item as shown in the previous section about MVC and Web API.</span></span> <span data-ttu-id="16a7e-153">Automaticky vygenerovaná zobrazení a kontroler budou správně fungovat v rámci projektu.</span><span class="sxs-lookup"><span data-stu-id="16a7e-153">The automatically-generated views and controller will function correctly within your project.</span></span>

## <a name="tutorials"></a><span data-ttu-id="16a7e-154">Kurzy</span><span class="sxs-lookup"><span data-stu-id="16a7e-154">Tutorials</span></span>

<span data-ttu-id="16a7e-155">Chcete-li vytvořit přizpůsobený generátor, přečtěte si téma [Vytvoření vlastního lešení pro Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span><span class="sxs-lookup"><span data-stu-id="16a7e-155">To create a customized scaffolder, see [Creating a Custom Scaffolder for Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).</span></span>

<span data-ttu-id="16a7e-156">Chcete-li přizpůsobit vygenerované soubory, přečtěte si téma [jak přizpůsobit vygenerované soubory z dialogového okna nové vygenerované položky](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx).</span><span class="sxs-lookup"><span data-stu-id="16a7e-156">To customize the generated files, see [How to customize the generated files from the New Scaffolded Item dialog](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx).</span></span>

<span data-ttu-id="16a7e-157">Příklad použití generování uživatelského rozhraní s **Database Firstm vývojem**naleznete v tématu [EF Database First with ASP.NET MVC](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md).</span><span class="sxs-lookup"><span data-stu-id="16a7e-157">For an example of using scaffolding with **Database First development**, see [EF Database First with ASP.NET MVC](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md).</span></span>

<span data-ttu-id="16a7e-158">Příklad použití generování uživatelského rozhraní v projektu **MVC** najdete v tématu [Začínáme s ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="16a7e-158">For an example of using scaffolding in an **MVC** project, see [Getting Started with ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).</span></span>

<span data-ttu-id="16a7e-159">Příklad použití generování uživatelského rozhraní v projektu **webového rozhraní API** najdete v tématu [Vytvoření REST API s směrováním atributů ve webovém rozhraní API 2](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md).</span><span class="sxs-lookup"><span data-stu-id="16a7e-159">For an example of using scaffolding in a **Web API** project, see [Create a REST API with Attribute Routing in Web API 2](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md).</span></span>

---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
title: Přidání modelu (VB) | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, který je...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b3aa7720-5c78-4ca2-baef-9a52234fb7ce
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: e69d59aed4d74f08f1c653c4965b128c4dbe20ff
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457242"
---
# <a name="adding-a-model-vb"></a><span data-ttu-id="be504-103">Přidání modelu (VB)</span><span class="sxs-lookup"><span data-stu-id="be504-103">Adding a Model (VB)</span></span>

<span data-ttu-id="be504-104">od [Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="be504-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="be504-105">V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, což je bezplatná verze Microsoft Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="be504-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="be504-106">Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže.</span><span class="sxs-lookup"><span data-stu-id="be504-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="be504-107">Všechny z nich můžete nainstalovat kliknutím na následující odkaz: instalace [webové platformy](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="be504-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="be504-108">Případně můžete požadavky jednotlivě nainstalovat pomocí následujících odkazů:</span><span class="sxs-lookup"><span data-stu-id="be504-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="be504-109">Požadavky sady Visual Studio Web Developer Express SP1</span><span class="sxs-lookup"><span data-stu-id="be504-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="be504-110">Aktualizace nástrojů MVC 3 pro ASP.NET</span><span class="sxs-lookup"><span data-stu-id="be504-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="be504-111">[SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(podpora modulu runtime + nástroje)</span><span class="sxs-lookup"><span data-stu-id="be504-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="be504-112">Pokud používáte sadu Visual Studio 2010 místo sady Visual Web Developer 2010, nainstalujte požadavky kliknutím na následující odkaz: sady [Visual studio 2010 požadavky](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span><span class="sxs-lookup"><span data-stu-id="be504-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="be504-113">Projekt Visual Web Developer s VB.NET zdrojovým kódem je k dispozici pro toto téma.</span><span class="sxs-lookup"><span data-stu-id="be504-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="be504-114">[Stáhněte si verzi VB.NET](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span><span class="sxs-lookup"><span data-stu-id="be504-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="be504-115">Pokud dáváte přednost C#, přepněte se na [ C# verzi](../cs/adding-a-model.md) tohoto kurzu.</span><span class="sxs-lookup"><span data-stu-id="be504-115">If you prefer C#, switch to the [C# version](../cs/adding-a-model.md) of this tutorial.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="be504-116">Přidání modelu</span><span class="sxs-lookup"><span data-stu-id="be504-116">Adding a Model</span></span>

<span data-ttu-id="be504-117">V této části přidáte některé třídy pro správu filmů v databázi.</span><span class="sxs-lookup"><span data-stu-id="be504-117">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="be504-118">Tyto třídy budou součástí modelu aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="be504-118">These classes will be the "model" part of the ASP.NET MVC application.</span></span>

<span data-ttu-id="be504-119">K definování a práci s těmito třídami modelů použijete .NET Framework technologie pro přístup k datům, která je známá jako Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="be504-119">You'll use a .NET Framework data-access technology known as the Entity Framework to define and work with these model classes.</span></span> <span data-ttu-id="be504-120">Entity Framework (často označované jako EF) podporují vývojové paradigma nazvané *Code First*.</span><span class="sxs-lookup"><span data-stu-id="be504-120">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="be504-121">Code First umožňuje vytvářet objekty modelu zápisem jednoduchých tříd.</span><span class="sxs-lookup"><span data-stu-id="be504-121">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="be504-122">(Tyto třídy se označují také jako třídy POCO, od "objektů CLR v prostém Old". Databázi pak můžete z vašich tříd vytvořit průběžně, což umožňuje velmi čistý a rychlý vývojový pracovní postup.</span><span class="sxs-lookup"><span data-stu-id="be504-122">(These are also known as POCO classes, from "plain-old CLR objects.") You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="be504-123">Přidávání tříd modelu</span><span class="sxs-lookup"><span data-stu-id="be504-123">Adding Model Classes</span></span>

<span data-ttu-id="be504-124">V **Průzkumník řešení**klikněte pravým tlačítkem na složku *modely* , vyberte **Přidat**a pak vyberte **Třída**.</span><span class="sxs-lookup"><span data-stu-id="be504-124">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="be504-125">Pojmenujte třídu "film".</span><span class="sxs-lookup"><span data-stu-id="be504-125">Name the class "Movie".</span></span>

<span data-ttu-id="be504-126">Do `Movie` třídy přidejte následující pět vlastností:</span><span class="sxs-lookup"><span data-stu-id="be504-126">Add the following five properties to the `Movie` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample1.vb)]

<span data-ttu-id="be504-127">K reprezentaci filmů v databázi použijeme třídu `Movie`.</span><span class="sxs-lookup"><span data-stu-id="be504-127">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="be504-128">Každá instance `Movie` objektu bude odpovídat řádku v tabulce databáze a každá vlastnost `Movie` třídy bude namapována na sloupec v tabulce.</span><span class="sxs-lookup"><span data-stu-id="be504-128">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="be504-129">Do stejného souboru přidejte následující třídu `MovieDBContext`:</span><span class="sxs-lookup"><span data-stu-id="be504-129">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-vb[Main](adding-a-model/samples/sample2.vb)]

<span data-ttu-id="be504-130">Třída `MovieDBContext` představuje kontext Entity Framework filmového databáze, který zpracovává načítání, ukládání a aktualizaci instancí tříd `Movie` v databázi.</span><span class="sxs-lookup"><span data-stu-id="be504-130">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="be504-131">`MovieDBContext` je odvozen ze `DbContext` základní třídy poskytované Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="be504-131">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span> <span data-ttu-id="be504-132">Další informace o `DbContext` a `DbSet`najdete v tématu [vylepšení produktivity pro Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span><span class="sxs-lookup"><span data-stu-id="be504-132">For more information about `DbContext` and `DbSet`, see [Productivity Improvements for the Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).</span></span>

<span data-ttu-id="be504-133">Aby bylo možné odkazovat `DbContext` a `DbSet`, je nutné do horní části souboru přidat následující příkaz `imports`:</span><span class="sxs-lookup"><span data-stu-id="be504-133">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `imports` statement at the top of the file:</span></span>

[!code-vb[Main](adding-a-model/samples/sample3.vb)]

<span data-ttu-id="be504-134">Úplný soubor *Movie. vb* je zobrazený níže.</span><span class="sxs-lookup"><span data-stu-id="be504-134">The complete *Movie.vb* file is shown below.</span></span>

[!code-vb[Main](adding-a-model/samples/sample4.vb)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a><span data-ttu-id="be504-135">Vytvoření připojovacího řetězce a práce s SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="be504-135">Creating a Connection String and Working with SQL Server Compact</span></span>

<span data-ttu-id="be504-136">Třída `MovieDBContext`, kterou jste vytvořili, zpracovává úlohu připojení k databázi a mapování objektů `Movie` na záznamy databáze.</span><span class="sxs-lookup"><span data-stu-id="be504-136">The `MovieDBContext` class you created handles the task of connecting to the database and mapping `Movie` objects to database records.</span></span> <span data-ttu-id="be504-137">Jedna otázka, na kterou se můžete zeptat, ale je, jak určit databázi, ke které se bude připojovat.</span><span class="sxs-lookup"><span data-stu-id="be504-137">One question you might ask, though, is how to specify which database it will connect to.</span></span> <span data-ttu-id="be504-138">Provedete to tak, že přidáte informace o připojení do souboru *Web. config* aplikace.</span><span class="sxs-lookup"><span data-stu-id="be504-138">You'll do that by adding connection information in the *Web.config* file of the application.</span></span>

<span data-ttu-id="be504-139">Otevřete kořenový soubor *Web. config* aplikace.</span><span class="sxs-lookup"><span data-stu-id="be504-139">Open the application root *Web.config* file.</span></span> <span data-ttu-id="be504-140">(Ne soubor *Web. config* ve složce *views* .) Následující obrázek zobrazuje soubory *Web. config* ; Otevřete soubor *Web. config* v podobě červeného kruhu.</span><span class="sxs-lookup"><span data-stu-id="be504-140">(Not the *Web.config* file in the *Views* folder.) The image below show both *Web.config* files; open the *Web.config* file circled in red.</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="be504-141">Přidejte následující připojovací řetězec do prvku `<connectionStrings>` v souboru *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="be504-141">Add the following connection string to the `<connectionStrings>` element in the *Web.config* file.</span></span>

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

<span data-ttu-id="be504-142">Následující příklad ukazuje část souboru *Web. config* s přidaným novým připojovacím řetězcem:</span><span class="sxs-lookup"><span data-stu-id="be504-142">The following example shows a portion of the *Web.config* file with the new connection string added:</span></span>

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

<span data-ttu-id="be504-143">Tento malý objem kódu a XML je vše, co potřebujete k tomu, abyste mohli zastupovat a ukládat data videa v databázi.</span><span class="sxs-lookup"><span data-stu-id="be504-143">This small amount of code and XML is everything you need to write in order to represent and store the movie data in a database.</span></span>

<span data-ttu-id="be504-144">V dalším kroku vytvoříte novou třídu `MoviesController`, kterou můžete použít k zobrazení dat filmu a umožníte uživatelům vytvářet nové seznamy filmů.</span><span class="sxs-lookup"><span data-stu-id="be504-144">Next, you'll build a new `MoviesController` class that you can use to display the movie data and allow users to create new movie listings.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="be504-145">[Předchozí](adding-a-view.md)
> [Další](accessing-your-models-data-from-a-controller.md)</span><span class="sxs-lookup"><span data-stu-id="be504-145">[Previous](adding-a-view.md)
[Next](accessing-your-models-data-from-a-controller.md)</span></span>

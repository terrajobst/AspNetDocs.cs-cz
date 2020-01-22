---
uid: mvc/overview/getting-started/introduction/adding-a-model
title: Přidání modelu | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 276552b5-f349-4fcf-8f40-6d042f7aa88e
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: 0d926c7a8bd99c56820208921c10e609da56d236
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519034"
---
# <a name="adding-a-model"></a><span data-ttu-id="c937d-102">Přidání modelu</span><span class="sxs-lookup"><span data-stu-id="c937d-102">Adding a Model</span></span>

<span data-ttu-id="c937d-103">od [Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="c937d-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [Tutorial Note](index.md)]

<span data-ttu-id="c937d-104">V této části přidáte některé třídy pro správu filmů v databázi.</span><span class="sxs-lookup"><span data-stu-id="c937d-104">In this section you'll add some classes for managing movies in a database.</span></span> <span data-ttu-id="c937d-105">Tyto třídy budou &quot;model&quot; součást aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="c937d-105">These classes will be the &quot;model&quot; part of the ASP.NET MVC app.</span></span>

<span data-ttu-id="c937d-106">K definování a práci s těmito třídami modelů použijete .NET Framework technologie pro přístup k datům, která je známá jako [Entity Framework](https://docs.microsoft.com/ef/) .</span><span class="sxs-lookup"><span data-stu-id="c937d-106">You'll use a .NET Framework data-access technology known as the [Entity Framework](https://docs.microsoft.com/ef/) to define and work with these model classes.</span></span> <span data-ttu-id="c937d-107">Entity Framework (často označované jako EF) podporují vývojové paradigma nazvané *Code First*.</span><span class="sxs-lookup"><span data-stu-id="c937d-107">The Entity Framework (often referred to as EF) supports a development paradigm called *Code First*.</span></span> <span data-ttu-id="c937d-108">Code First umožňuje vytvářet objekty modelu zápisem jednoduchých tříd.</span><span class="sxs-lookup"><span data-stu-id="c937d-108">Code First allows you to create model objects by writing simple classes.</span></span> <span data-ttu-id="c937d-109">(Tyto třídy jsou také známé jako třídy POCO, od &quot;objektů CLR, které jsou prosté staré.&quot;) Databázi pak můžete z vašich tříd vytvořit průběžně, což umožňuje velmi čistý a rychlý vývojový pracovní postup.</span><span class="sxs-lookup"><span data-stu-id="c937d-109">(These are also known as POCO classes, from &quot;plain-old CLR objects.&quot;) You can then have the database created on the fly from your classes, which enables a very clean and rapid development workflow.</span></span> <span data-ttu-id="c937d-110">Pokud je nutné nejprve vytvořit databázi, můžete postupovat podle tohoto kurzu, kde se dozvíte o vývoji aplikací MVC a EF.</span><span class="sxs-lookup"><span data-stu-id="c937d-110">If you are required to create the database first, you can still follow this tutorial to learn about MVC and EF app development.</span></span> <span data-ttu-id="c937d-111">Pak můžete postupovat podle vlastního kurzu Fizmakens [ASP.NET pro generování uživatelského rozhraní](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) , který se zabývá prvním přístupem k databázi.</span><span class="sxs-lookup"><span data-stu-id="c937d-111">You can then follow Tom Fizmakens [ASP.NET Scaffolding](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) tutorial, which covers the database first approach.</span></span>

## <a name="adding-model-classes"></a><span data-ttu-id="c937d-112">Přidávání tříd modelu</span><span class="sxs-lookup"><span data-stu-id="c937d-112">Adding Model Classes</span></span>

<span data-ttu-id="c937d-113">V **Průzkumník řešení**klikněte pravým tlačítkem na složku *modely* , vyberte **Přidat**a pak vyberte **Třída**.</span><span class="sxs-lookup"><span data-stu-id="c937d-113">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-model/_static/image1.png)

<span data-ttu-id="c937d-114">Zadejte název *třídy* &quot;filmový&quot;.</span><span class="sxs-lookup"><span data-stu-id="c937d-114">Enter the *class* name &quot;Movie&quot;.</span></span>

<span data-ttu-id="c937d-115">Do `Movie` třídy přidejte následující pět vlastností:</span><span class="sxs-lookup"><span data-stu-id="c937d-115">Add the following five properties to the `Movie` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

<span data-ttu-id="c937d-116">K reprezentaci filmů v databázi použijeme třídu `Movie`.</span><span class="sxs-lookup"><span data-stu-id="c937d-116">We'll use the `Movie` class to represent movies in a database.</span></span> <span data-ttu-id="c937d-117">Každá instance `Movie` objektu bude odpovídat řádku v tabulce databáze a každá vlastnost `Movie` třídy bude namapována na sloupec v tabulce.</span><span class="sxs-lookup"><span data-stu-id="c937d-117">Each instance of a `Movie` object will correspond to a row within a database table, and each property of the `Movie` class will map to a column in the table.</span></span>

<span data-ttu-id="c937d-118">Poznámka: aby bylo možné použít System. data. entity a související třídu, je nutné nainstalovat [balíček Entity Framework NuGet](https://www.nuget.org/packages/EntityFramework/).</span><span class="sxs-lookup"><span data-stu-id="c937d-118">Note: In order to use System.Data.Entity, and the related class, you need to install the [Entity Framework NuGet Package](https://www.nuget.org/packages/EntityFramework/).</span></span> <span data-ttu-id="c937d-119">Další pokyny získáte pomocí odkazu.</span><span class="sxs-lookup"><span data-stu-id="c937d-119">Follow the link for further instructions.</span></span>

<span data-ttu-id="c937d-120">Do stejného souboru přidejte následující třídu `MovieDBContext`:</span><span class="sxs-lookup"><span data-stu-id="c937d-120">In the same file, add the following `MovieDBContext` class:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

<span data-ttu-id="c937d-121">Třída `MovieDBContext` představuje kontext Entity Framework filmového databáze, který zpracovává načítání, ukládání a aktualizaci instancí tříd `Movie` v databázi.</span><span class="sxs-lookup"><span data-stu-id="c937d-121">The `MovieDBContext` class represents the Entity Framework movie database context, which handles fetching, storing, and updating `Movie` class instances in a database.</span></span> <span data-ttu-id="c937d-122">`MovieDBContext` je odvozen ze `DbContext` základní třídy poskytované Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="c937d-122">The `MovieDBContext` derives from the `DbContext` base class provided by the Entity Framework.</span></span>

<span data-ttu-id="c937d-123">Aby bylo možné odkazovat `DbContext` a `DbSet`, je nutné do horní části souboru přidat následující příkaz `using`:</span><span class="sxs-lookup"><span data-stu-id="c937d-123">In order to be able to reference `DbContext` and `DbSet`, you need to add the following `using` statement at the top of the file:</span></span>

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

<span data-ttu-id="c937d-124">To můžete provést ručním přidáním příkazu Using, nebo můžete ukazatel myši umístit na červené vlnovky, kliknout na `Show potential fixes` a kliknout na `using System.Data.Entity;`</span><span class="sxs-lookup"><span data-stu-id="c937d-124">You can do this by manually adding the using statement, or you can hover over the red squiggly lines, click `Show potential fixes` and click `using System.Data.Entity;`</span></span>

![](adding-a-model/_static/image2.png)

<span data-ttu-id="c937d-125">Poznámka: odebrali jsme několik nepoužitých `using` příkazů.</span><span class="sxs-lookup"><span data-stu-id="c937d-125">Note: Several unused `using` statements have been removed.</span></span> <span data-ttu-id="c937d-126">Visual Studio zobrazí nepoužívané závislosti jako šedé.</span><span class="sxs-lookup"><span data-stu-id="c937d-126">Visual Studio will show unused dependencies as gray.</span></span> <span data-ttu-id="c937d-127">Nepoužívané závislosti můžete odebrat tak, že najedete myší na šedé závislosti, kliknete `Show potential fixes` a kliknete na **Odebrat nepoužité direktivy using.**</span><span class="sxs-lookup"><span data-stu-id="c937d-127">You can remove unused dependencies by hovering over the gray dependencies, click `Show potential fixes` and click **Remove Unused Usings.**</span></span>

![](adding-a-model/_static/image3.png)

<span data-ttu-id="c937d-128">Nakonec jsme přidali model (M v MVC).</span><span class="sxs-lookup"><span data-stu-id="c937d-128">We've finally added a model (the M in MVC).</span></span> <span data-ttu-id="c937d-129">V další části budete pracovat s připojovacím řetězcem databáze.</span><span class="sxs-lookup"><span data-stu-id="c937d-129">In the next section you'll work with the database connection string.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c937d-130">[Předchozí](adding-a-view.md)
> [Další](creating-a-connection-string.md)</span><span class="sxs-lookup"><span data-stu-id="c937d-130">[Previous](adding-a-view.md)
[Next](creating-a-connection-string.md)</span></span>

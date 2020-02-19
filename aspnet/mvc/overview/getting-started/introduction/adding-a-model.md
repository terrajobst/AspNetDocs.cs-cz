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
ms.openlocfilehash: c5525cfe940cadff5113c63eb0508d15697b5606
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456540"
---
# <a name="adding-a-model"></a>Přidání modelu

od [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

V této části přidáte některé třídy pro správu filmů v databázi. Tyto třídy budou &quot;model&quot; součást aplikace ASP.NET MVC.

K definování a práci s těmito třídami modelů použijete .NET Framework technologie pro přístup k datům, která je známá jako [Entity Framework](https://docs.microsoft.com/ef/) . Entity Framework (často označované jako EF) podporují vývojové paradigma nazvané *Code First*. Code First umožňuje vytvářet objekty modelu zápisem jednoduchých tříd. (Tyto třídy jsou také známé jako třídy POCO, od &quot;objektů CLR, které jsou prosté staré.&quot;) Databázi pak můžete z vašich tříd vytvořit průběžně, což umožňuje velmi čistý a rychlý vývojový pracovní postup. Pokud je nutné nejprve vytvořit databázi, můžete postupovat podle tohoto kurzu, kde se dozvíte o vývoji aplikací MVC a EF. Pak můžete postupovat podle vlastního kurzu Fizmakens [ASP.NET pro generování uživatelského rozhraní](xref:visual-studio/overview/2013/aspnet-scaffolding-overview) , který se zabývá prvním přístupem k databázi.

## <a name="adding-model-classes"></a>Přidávání tříd modelu

V **Průzkumník řešení**klikněte pravým tlačítkem na složku *modely* , vyberte **Přidat**a pak vyberte **Třída**.

![](adding-a-model/_static/image1.png)

Zadejte název *třídy* &quot;filmový&quot;.

Do `Movie` třídy přidejte následující pět vlastností:

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

K reprezentaci filmů v databázi použijeme třídu `Movie`. Každá instance `Movie` objektu bude odpovídat řádku v tabulce databáze a každá vlastnost `Movie` třídy bude namapována na sloupec v tabulce.

Poznámka: aby bylo možné použít System. data. entity a související třídu, je nutné nainstalovat [balíček Entity Framework NuGet](https://www.nuget.org/packages/EntityFramework/). Další pokyny získáte pomocí odkazu.

Do stejného souboru přidejte následující třídu `MovieDBContext`:

[!code-csharp[Main](adding-a-model/samples/sample2.cs?highlight=2,15-18)]

Třída `MovieDBContext` představuje kontext Entity Framework filmového databáze, který zpracovává načítání, ukládání a aktualizaci instancí tříd `Movie` v databázi. `MovieDBContext` je odvozen ze `DbContext` základní třídy poskytované Entity Framework.

Aby bylo možné odkazovat `DbContext` a `DbSet`, je nutné do horní části souboru přidat následující příkaz `using`:

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

To můžete provést ručním přidáním příkazu Using, nebo můžete ukazatel myši umístit na červené vlnovky, kliknout na `Show potential fixes` a kliknout na `using System.Data.Entity;`

![](adding-a-model/_static/image2.png)

Poznámka: odebrali jsme několik nepoužitých `using` příkazů. Visual Studio zobrazí nepoužívané závislosti jako šedé. Nepoužívané závislosti můžete odebrat tak, že najedete myší na šedé závislosti, kliknete `Show potential fixes` a kliknete na **Odebrat nepoužité direktivy using.**

![](adding-a-model/_static/image3.png)

Nakonec jsme přidali model (M v MVC). V další části budete pracovat s připojovacím řetězcem databáze.

> [!div class="step-by-step"]
> [Předchozí](adding-a-view.md)
> [Další](creating-a-connection-string.md)

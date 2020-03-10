---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
title: Přidání modelu | Microsoft Docs
author: Rick-Anderson
description: 'Poznámka: v této části je k dispozici aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013. Je to bezpečnější, takže je mnohem jednodušší postupovat a demo...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 53db72da-e0b9-44d9-b60b-6e6988c00b28
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-model
msc.type: authoredcontent
ms.openlocfilehash: a9851d93dde495814f67fa0c807d3534f5f0d8ef
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540304"
---
# <a name="adding-a-model"></a>Přidání modelu

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > K [dispozici je](../../getting-started/introduction/getting-started.md) aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013. Je to bezpečnější, mnohem jednodušší a ukazuje více funkcí.

V této části přidáte některé třídy pro správu filmů v databázi. Tyto třídy budou &quot;model&quot; součást aplikace ASP.NET MVC.

K definování a práci s těmito třídami modelů použijete .NET Framework technologie pro přístup k datům, která je známá jako [Entity Framework](https://msdn.microsoft.com/library/bb399572(VS.110).aspx) . Entity Framework (často označované jako EF) podporují vývojové paradigma nazvané *Code First*. Code First umožňuje vytvářet objekty modelu zápisem jednoduchých tříd. (Tyto třídy jsou také známé jako třídy POCO, od &quot;objektů CLR, které jsou prosté staré.&quot;) Databázi pak můžete z vašich tříd vytvořit průběžně, což umožňuje velmi čistý a rychlý vývojový pracovní postup.

## <a name="adding-model-classes"></a>Přidávání tříd modelu

V **Průzkumník řešení**klikněte pravým tlačítkem na složku *modely* , vyberte **Přidat**a pak vyberte **Třída**.

![](adding-a-model/_static/image1.png)

Zadejte název *třídy* &quot;filmový&quot;.

Do `Movie` třídy přidejte následující pět vlastností:

[!code-csharp[Main](adding-a-model/samples/sample1.cs)]

K reprezentaci filmů v databázi použijeme třídu `Movie`. Každá instance `Movie` objektu bude odpovídat řádku v tabulce databáze a každá vlastnost `Movie` třídy bude namapována na sloupec v tabulce.

Do stejného souboru přidejte následující třídu `MovieDBContext`:

[!code-csharp[Main](adding-a-model/samples/sample2.cs)]

Třída `MovieDBContext` představuje kontext Entity Framework filmového databáze, který zpracovává načítání, ukládání a aktualizaci instancí tříd `Movie` v databázi. `MovieDBContext` je odvozen ze `DbContext` základní třídy poskytované Entity Framework.

Aby bylo možné odkazovat `DbContext` a `DbSet`, je nutné do horní části souboru přidat následující příkaz `using`:

[!code-csharp[Main](adding-a-model/samples/sample3.cs)]

Úplný soubor *Movie.cs* je uveden níže. (Několik příkazů using, které nejsou potřeba, se odebralo.)

[!code-csharp[Main](adding-a-model/samples/sample4.cs)]

## <a name="creating-a-connection-string-and-working-with-sql-server-localdb"></a>Vytvoření připojovacího řetězce a práce s databází SQL Serveru LocalDB

Třída `MovieDBContext`, kterou jste vytvořili, zpracovává úlohu připojení k databázi a mapování objektů `Movie` na záznamy databáze. Jedna otázka, na kterou se můžete zeptat, ale je, jak určit databázi, ke které se bude připojovat. Provedete to tak, že přidáte informace o připojení do souboru *Web. config* aplikace.

Otevřete kořenový soubor *Web. config* aplikace. (Ne soubor *Web. config* ve složce *views* .) Otevřete soubor *Web. config* , který je popsaný červeně.

![](adding-a-model/_static/image2.png)

Přidejte následující připojovací řetězec do prvku `<connectionStrings>` v souboru *Web. config* .

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

Následující příklad ukazuje část souboru *Web. config* s přidaným novým připojovacím řetězcem:

[!code-xml[Main](adding-a-model/samples/sample6.xml?highlight=6-9)]

Tento malý objem kódu a XML je vše, co potřebujete k tomu, abyste mohli zastupovat a ukládat data videa v databázi.

V dalším kroku vytvoříte novou třídu `MoviesController`, kterou můžete použít k zobrazení dat filmu a umožníte uživatelům vytvářet nové seznamy filmů.

> [!div class="step-by-step"]
> [Předchozí](adding-a-view.md)
> [Další](accessing-your-models-data-from-a-controller.md)

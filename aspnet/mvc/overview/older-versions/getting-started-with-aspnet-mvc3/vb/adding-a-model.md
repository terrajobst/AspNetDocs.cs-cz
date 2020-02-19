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
# <a name="adding-a-model-vb"></a>Přidání modelu (VB)

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, což je bezplatná verze Microsoft Visual Studio. Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže. Všechny z nich můžete nainstalovat kliknutím na následující odkaz: instalace [webové platformy](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Případně můžete požadavky jednotlivě nainstalovat pomocí následujících odkazů:
> 
> - [Požadavky sady Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Aktualizace nástrojů MVC 3 pro ASP.NET](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(podpora modulu runtime + nástroje)
> 
> Pokud používáte sadu Visual Studio 2010 místo sady Visual Web Developer 2010, nainstalujte požadavky kliknutím na následující odkaz: sady [Visual studio 2010 požadavky](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Projekt Visual Web Developer s VB.NET zdrojovým kódem je k dispozici pro toto téma. [Stáhněte si verzi VB.NET](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Pokud dáváte přednost C#, přepněte se na [ C# verzi](../cs/adding-a-model.md) tohoto kurzu.

## <a name="adding-a-model"></a>Přidání modelu

V této části přidáte některé třídy pro správu filmů v databázi. Tyto třídy budou součástí modelu aplikace ASP.NET MVC.

K definování a práci s těmito třídami modelů použijete .NET Framework technologie pro přístup k datům, která je známá jako Entity Framework. Entity Framework (často označované jako EF) podporují vývojové paradigma nazvané *Code First*. Code First umožňuje vytvářet objekty modelu zápisem jednoduchých tříd. (Tyto třídy se označují také jako třídy POCO, od "objektů CLR v prostém Old". Databázi pak můžete z vašich tříd vytvořit průběžně, což umožňuje velmi čistý a rychlý vývojový pracovní postup.

## <a name="adding-model-classes"></a>Přidávání tříd modelu

V **Průzkumník řešení**klikněte pravým tlačítkem na složku *modely* , vyberte **Přidat**a pak vyberte **Třída**.

![](adding-a-model/_static/image1.png)

Pojmenujte třídu "film".

Do `Movie` třídy přidejte následující pět vlastností:

[!code-vb[Main](adding-a-model/samples/sample1.vb)]

K reprezentaci filmů v databázi použijeme třídu `Movie`. Každá instance `Movie` objektu bude odpovídat řádku v tabulce databáze a každá vlastnost `Movie` třídy bude namapována na sloupec v tabulce.

Do stejného souboru přidejte následující třídu `MovieDBContext`:

[!code-vb[Main](adding-a-model/samples/sample2.vb)]

Třída `MovieDBContext` představuje kontext Entity Framework filmového databáze, který zpracovává načítání, ukládání a aktualizaci instancí tříd `Movie` v databázi. `MovieDBContext` je odvozen ze `DbContext` základní třídy poskytované Entity Framework. Další informace o `DbContext` a `DbSet`najdete v tématu [vylepšení produktivity pro Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0).

Aby bylo možné odkazovat `DbContext` a `DbSet`, je nutné do horní části souboru přidat následující příkaz `imports`:

[!code-vb[Main](adding-a-model/samples/sample3.vb)]

Úplný soubor *Movie. vb* je zobrazený níže.

[!code-vb[Main](adding-a-model/samples/sample4.vb)]

## <a name="creating-a-connection-string-and-working-with-sql-server-compact"></a>Vytvoření připojovacího řetězce a práce s SQL Server Compact

Třída `MovieDBContext`, kterou jste vytvořili, zpracovává úlohu připojení k databázi a mapování objektů `Movie` na záznamy databáze. Jedna otázka, na kterou se můžete zeptat, ale je, jak určit databázi, ke které se bude připojovat. Provedete to tak, že přidáte informace o připojení do souboru *Web. config* aplikace.

Otevřete kořenový soubor *Web. config* aplikace. (Ne soubor *Web. config* ve složce *views* .) Následující obrázek zobrazuje soubory *Web. config* ; Otevřete soubor *Web. config* v podobě červeného kruhu.

![](adding-a-model/_static/image2.png)

Přidejte následující připojovací řetězec do prvku `<connectionStrings>` v souboru *Web. config* .

[!code-xml[Main](adding-a-model/samples/sample5.xml)]

Následující příklad ukazuje část souboru *Web. config* s přidaným novým připojovacím řetězcem:

[!code-xml[Main](adding-a-model/samples/sample6.xml)]

Tento malý objem kódu a XML je vše, co potřebujete k tomu, abyste mohli zastupovat a ukládat data videa v databázi.

V dalším kroku vytvoříte novou třídu `MoviesController`, kterou můžete použít k zobrazení dat filmu a umožníte uživatelům vytvářet nové seznamy filmů.

> [!div class="step-by-step"]
> [Předchozí](adding-a-view.md)
> [Další](accessing-your-models-data-from-a-controller.md)

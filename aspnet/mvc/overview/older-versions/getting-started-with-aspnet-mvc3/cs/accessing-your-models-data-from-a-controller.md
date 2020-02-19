---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/accessing-your-models-data-from-a-controller
title: Přístup k datům modelu z kontroleru (C#) | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, který je...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 002ada5c-f114-47ab-a441-57dbdb728ea0
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 2e9c7f24d426635760b613f570b85455ce71b3dc
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458075"
---
# <a name="accessing-your-models-data-from-a-controller-c"></a>Přístup k datům modelu z kontroleru (C#)

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > K [dispozici je](../../../getting-started/introduction/getting-started.md) aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013. Je to bezpečnější, mnohem jednodušší a ukazuje více funkcí.
> 
> 
> V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, což je bezplatná verze Microsoft Visual Studio. Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže. Všechny z nich můžete nainstalovat kliknutím na následující odkaz: instalace [webové platformy](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Případně můžete požadavky jednotlivě nainstalovat pomocí následujících odkazů:
> 
> - [Požadavky sady Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Aktualizace nástrojů MVC 3 pro ASP.NET](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(podpora modulu runtime + nástroje)
> 
> Pokud používáte sadu Visual Studio 2010 místo sady Visual Web Developer 2010, nainstalujte požadavky kliknutím na následující odkaz: sady [Visual studio 2010 požadavky](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Projekt Visual Web Developer se C# zdrojovým kódem je k dispozici pro toto téma. [Stáhněte si C# verzi](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Pokud dáváte přednost Visual Basic, přepněte se na [Visual Basic verzi](../vb/intro-to-aspnet-mvc-3.md) tohoto kurzu.

V této části vytvoříte novou třídu `MoviesController` a napíšete kód, který načte data videa a zobrazí se v prohlížeči pomocí šablony zobrazení. Než budete pokračovat, nezapomeňte sestavit aplikaci.

Klikněte pravým tlačítkem na složku *Controllers* a vytvořte nový kontroler `MoviesController`. Vyberte následující možnosti:

- Název kontroleru: **MoviesController**. (Toto je výchozí nastavení. )
- Šablona: **kontroler s akcemi čtení/zápisu a zobrazeními pomocí Entity Framework**.
- Třída modelu: **video (MvcMovie. Models)** .
- Třída kontextu dat: **MovieDBContext (MvcMovie. Models)** .
- Zobrazení: **Razor (cshtml)** . (Výchozí nastavení.)

[![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image2.png "AddScaffoldedMovieController")](accessing-your-models-data-from-a-controller/_static/image1.png)

Klikněte na **Přidat**. Visual Web Developer vytvoří následující soubory a složky:

- Soubor *MoviesController.cs* ve složce *řadičů* projektu.
- Složka *filmy* ve složce *zobrazení* projektu.
- *Vytvořte. cshtml, odstraňte. cshtml, details. cshtml, upravte. cshtml*a *index. cshtml* ve složce New *Views\Movies* .

[![NewMovieControllerScreenShot](accessing-your-models-data-from-a-controller/_static/image4.png "NewMovieControllerScreenShot")](accessing-your-models-data-from-a-controller/_static/image3.png)

Mechanizmus pro generování uživatelského rozhraní ASP.NET MVC 3 automaticky vytvořila metody a zobrazení operací CRUD (vytváření, čtení, aktualizace a odstraňování). Nyní máte plně funkční webovou aplikaci, která umožňuje vytvářet, zobrazovat, upravovat a odstraňovat položky filmů.

Spusťte aplikaci a přejděte k řadiči `Movies` připojením */Movies* k adrese URL v adresním řádku prohlížeče. Vzhledem k tomu, že se aplikace spoléhá na výchozí směrování (definované v souboru *Global. asax* ), je požadavek prohlížeče `http://localhost:xxxxx/Movies` směrován do výchozí metody `Index` action kontroleru `Movies`. Jinými slovy, `http://localhost:xxxxx/Movies` požadavek prohlížeče je ve skutečnosti stejný jako `http://localhost:xxxxx/Movies/Index`žádosti prohlížeče. Výsledkem je prázdný seznam filmů, protože jste to ještě nepřidali.

![](accessing-your-models-data-from-a-controller/_static/image5.png)

### <a name="creating-a-movie"></a>Vytvoření filmu

Vyberte odkaz **vytvořit nový** . Zadejte podrobnosti o videu a potom klikněte na tlačítko **vytvořit** .

![](accessing-your-models-data-from-a-controller/_static/image6.png)

Kliknutím na tlačítko **vytvořit** dojde k odeslání formuláře na server, kde jsou informace o filmu uloženy v databázi. Pak budete přesměrováni na adresu URL */Movies* , kde uvidíte nově vytvořený film v seznamu.

[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png "IndexWhenHarryMet")](accessing-your-models-data-from-a-controller/_static/image7.png)

Vytvořte ještě několik dalších záznamů filmů. Zkuste odkazy **Upravit**, **Podrobnosti**a **Odstranit** , které jsou všechny funkční.

## <a name="examining-the-generated-code"></a>Prověřování generovaného kódu

Otevřete soubor *Controllers\MoviesController.cs* a prověřte vygenerovanou metodu `Index`. Část kontroleru videí s metodou `Index` je uvedena níže.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

Následující řádek z třídy `MoviesController` vytváří instanci kontextu databáze videa, jak je popsáno výše. Můžete použít kontext databáze videa k dotazování, úpravám a odstraňování filmů.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

Požadavek na kontroler `Movies` vrátí všechny položky v tabulce `Movies` v databázi videa a poté předá výsledky do zobrazení `Index`.

## <a name="strongly-typed-models-and-the-model-keyword"></a>Modely silného typu a klíčové slovo @model

Dříve v tomto kurzu jste viděli, jak může řadič předat data nebo objekty do šablony zobrazení pomocí objektu `ViewBag`. `ViewBag` je dynamický objekt, který poskytuje pohodlný způsob, jak předat informace do zobrazení.

ASP.NET MVC také poskytuje možnost předat data silného typu nebo objekty do šablony zobrazení. Tento přístup silného typu umožňuje lepší kontrolu kódu a bohatší IntelliSense v editoru Visual Web Developer. Tento přístup používáme pro třídu `MoviesController` a *index. cshtml* pro zobrazení.

Všimněte si, jak kód vytvoří objekt [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) při volání pomocné metody `View` v metodě akce `Index`. Kód pak předá tento seznam `Movies` z kontroleru k zobrazení:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

Zahrnutím příkazu `@model` v horní části souboru šablony zobrazení můžete určit typ objektu, který zobrazení očekává. Když jste vytvořili kontroler filmů, Visual Web Developer automaticky zahrne do horní části souboru *index. cshtml* následující příkaz `@model`:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

Tato direktiva `@model` umožňuje přístup k seznamu filmů, které kontroler předává do zobrazení, pomocí silně typovaného objektu `Model`. Například v šabloně *index. cshtml* kód projde pomocí příkazu `foreach` přes `Model` objekt silného typu:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml)]

Vzhledem k tomu, že objekt `Model` je silného typu (jako objekt `IEnumerable<Movie>`), je každý objekt `item` ve smyčce zadán jako `Movie`. Kromě dalších výhod to znamená, že získáte kontrolu v době kompilace kódu a úplnou podporu technologie IntelliSense v editoru kódu:

[![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image10.png "ModelIntelliSense")](accessing-your-models-data-from-a-controller/_static/image9.png)

## <a name="working-with-sql-server-compact"></a>Práce s SQL Server Compact

Entity Framework Code First zjistil, že zadaný připojovací řetězec databáze odkazoval na `Movies` databázi, která ještě neexistuje, takže Code First databázi automaticky vytvořil. Můžete ověřit, že se vytvořila, a to tak, že se podíváte na složku *Data\_App* . Pokud nevidíte soubor *Movies. sdf* , klikněte na tlačítko **Zobrazit všechny soubory** na panelu nástrojů **Průzkumník řešení** , klikněte na tlačítko **aktualizovat** a potom rozbalte složku *\_data App* .

[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png "SDF_in_SolnExp")](accessing-your-models-data-from-a-controller/_static/image11.png)

Dvojitým kliknutím na *video. sdf* otevřete **Průzkumník serveru**. Pak rozbalte složku **Tables (tabulky** ) a zobrazte tabulky, které byly vytvořeny v databázi.

> [!NOTE]
> Pokud při poklepání na *filmy. sdf*dojde k chybě, ujistěte se, že jste nainstalovali [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(podpora modulů runtime a nástrojů). (Informace o odkazech na software najdete v seznamu požadavků v části 1 této série kurzů.) Pokud nainstalujete tuto verzi hned, budete muset aplikaci Visual Web Developer zavřít a znovu otevřít.

[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png "DB_explorer")](accessing-your-models-data-from-a-controller/_static/image13.png)

K dispozici jsou dvě tabulky, jednu pro sadu entit `Movie` a potom tabulku `EdmMetadata`. `EdmMetadata` tabulce používá Entity Framework k určení, kdy model a databáze nejsou synchronizované.

Kliknutím pravým tlačítkem na tabulku `Movies` a výběrem **Zobrazit data tabulky** zobrazíte data, která jste vytvořili.

[![Filmy](accessing-your-models-data-from-a-controller/_static/image16.png "Filmy")](accessing-your-models-data-from-a-controller/_static/image15.png)

Klikněte pravým tlačítkem na tabulku `Movies` a vyberte **Upravit schéma tabulky**.

[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png "EditTableSchema")](accessing-your-models-data-from-a-controller/_static/image17.png)

[![TableSchemaSM](accessing-your-models-data-from-a-controller/_static/image20.png "TableSchemaSM")](accessing-your-models-data-from-a-controller/_static/image19.png)

Všimněte si, jak se schéma `Movies` tabulky mapuje na třídu `Movie`, kterou jste vytvořili dříve. Entity Framework Code First automaticky vytvořil toto schéma na základě vaší třídy `Movie`.

Až skončíte, připojení ukončete. (Pokud připojení neukončíte, při příštím spuštění projektu se může zobrazit chyba.

[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image22.png "CloseConnection")](accessing-your-models-data-from-a-controller/_static/image21.png)

Teď máte databázi a jednoduchou stránku se seznamem, ze které můžete zobrazit obsah. V dalším kurzu prověříme zbytek vygenerovaného kódu a přidáte `SearchIndex` metodu a `SearchIndex` zobrazení, které vám umožní vyhledat filmy v této databázi.

> [!div class="step-by-step"]
> [Předchozí](adding-a-model.md)
> [Další](examining-the-edit-methods-and-edit-view.md)

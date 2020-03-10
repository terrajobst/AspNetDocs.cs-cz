---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
title: Přístup k datům modelu z kontroleru | Microsoft Docs
author: Rick-Anderson
description: 'Poznámka: v této části je k dispozici aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013. Je to bezpečnější, takže je mnohem jednodušší postupovat a demo...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 61e0206d-7f32-4018-992d-0a51b48b37dc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 7c4aa34567ac4fb31d1ed874cf65986c4e779e66
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540388"
---
# <a name="accessing-your-models-data-from-a-controller"></a>Přístup k datům modelu z kontroleru

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > K [dispozici je](../../getting-started/introduction/getting-started.md) aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013. Je to bezpečnější, mnohem jednodušší a ukazuje více funkcí.

V této části vytvoříte novou třídu `MoviesController` a napíšete kód, který načte data videa a zobrazí se v prohlížeči pomocí šablony zobrazení.

Než začnete pokračovat k dalšímu kroku, **sestavte aplikaci** .

Klikněte pravým tlačítkem na složku *Controllers* a vytvořte nový kontroler `MoviesController`. Níže uvedené možnosti se nezobrazí, dokud nevytvoříte aplikaci. Vyberte následující možnosti:

- Název kontroleru: **MoviesController**. (Toto je výchozí nastavení. )
- Šablona: **kontroler MVC s akcemi a zobrazeními pro čtení/zápis pomocí Entity Framework**.
- Třída modelu: **video (MvcMovie. Models)** .
- Třída kontextu dat: **MovieDBContext (MvcMovie. Models)** .
- Zobrazení: **Razor (cshtml)** . (Výchozí nastavení.)

![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image1.png)

Klikněte na **Přidat**. Visual Studio Express vytvoří následující soubory a složky:

- Soubor *MoviesController.cs* ve složce *řadičů* projektu.
- Složka *filmy* ve složce *zobrazení* projektu.
- *Vytvořte. cshtml, odstraňte. cshtml, details. cshtml, upravte. cshtml*a *index. cshtml* ve složce New *Views\Movies* .

ASP.NET MVC 4 automaticky vytvořila metody a zobrazení akcí CRUD (vytváření, čtení, aktualizace a odstraňování) (automatické vytváření metod a zobrazení operací CRUD se říká generování uživatelského rozhraní). Nyní máte plně funkční webovou aplikaci, která umožňuje vytvářet, zobrazovat, upravovat a odstraňovat položky filmů.

Spusťte aplikaci a přejděte k řadiči `Movies` připojením */Movies* k adrese URL v adresním řádku prohlížeče. Vzhledem k tomu, že se aplikace spoléhá na výchozí směrování (definované v souboru *Global. asax* ), je požadavek prohlížeče `http://localhost:xxxxx/Movies` směrován do výchozí metody `Index` action kontroleru `Movies`. Jinými slovy, `http://localhost:xxxxx/Movies` požadavek prohlížeče je ve skutečnosti stejný jako `http://localhost:xxxxx/Movies/Index`žádosti prohlížeče. Výsledkem je prázdný seznam filmů, protože jste to ještě nepřidali.

![](accessing-your-models-data-from-a-controller/_static/image2.png)

### <a name="creating-a-movie"></a>Vytvoření filmu

Vyberte odkaz **vytvořit nový** . Zadejte podrobnosti o videu a potom klikněte na tlačítko **vytvořit** .

![](accessing-your-models-data-from-a-controller/_static/image3.png)

Kliknutím na tlačítko **vytvořit** dojde k odeslání formuláře na server, kde jsou informace o filmu uloženy v databázi. Pak budete přesměrováni na adresu URL */Movies* , kde uvidíte nově vytvořený film v seznamu.

![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")

Vytvořte ještě několik dalších záznamů filmů. Zkuste odkazy **Upravit**, **Podrobnosti**a **Odstranit** , které jsou všechny funkční.

## <a name="examining-the-generated-code"></a>Prověřování generovaného kódu

Otevřete soubor *Controllers\MoviesController.cs* a prověřte vygenerovanou metodu `Index`. Část kontroleru videí s metodou `Index` je uvedena níže.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

Následující řádek z třídy `MoviesController` vytváří instanci kontextu databáze videa, jak je popsáno výše. Můžete použít kontext databáze videa k dotazování, úpravám a odstraňování filmů.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

Požadavek na kontroler `Movies` vrátí všechny položky v tabulce `Movies` v databázi videa a poté předá výsledky do zobrazení `Index`.

## <a name="strongly-typed-models-and-the-model-keyword"></a>Modely silného typu a klíčové slovo @model

Dříve v tomto kurzu jste viděli, jak může řadič předat data nebo objekty do šablony zobrazení pomocí objektu `ViewBag`. `ViewBag` je dynamický objekt, který poskytuje pohodlný způsob, jak předat informace do zobrazení.

ASP.NET MVC také poskytuje možnost předat data silného typu nebo objekty do šablony zobrazení. Tento přístup silného typu umožňuje lepší kontrolu kódu a bohatší IntelliSense v editoru sady Visual Studio. Mechanizmus pro generování uživatelského rozhraní v aplikaci Visual Studio používal tento přístup ke třídě `MoviesController` a zobrazení šablon při vytváření metod a zobrazení.

V souboru *Controllers\MoviesController.cs* prověřte vygenerovanou metodu `Details`. Část kontroleru videí s metodou `Details` je uvedena níže.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs?highlight=3,8)]

Pokud je nalezen `Movie`, je do zobrazení podrobností předána instance modelu `Movie`. Prověřte obsah souboru *Views\Movies\Details.cshtml* .

Zahrnutím příkazu `@model` v horní části souboru šablony zobrazení můžete určit typ objektu, který zobrazení očekává. Když jste vytvořili kontroler filmů, Visual Studio automaticky v horní části souboru *Details. cshtml* obsahuje následující příkaz `@model`:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

Tato direktiva `@model` umožňuje přístup k videu, který kontroler předává do zobrazení pomocí objektu `Model` se silným typem. Například v šabloně *Details. cshtml* kód předá do každého pole video `DisplayNameFor` a [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) nápovědu HTML pomocí objektu silného typu `Model`. Metody Create a Edit a zobrazení šablony také předají objekt filmového modelu.

Prohlédněte si šablonu zobrazení *index. cshtml* a metodu `Index` v souboru *MoviesController.cs* . Všimněte si, jak kód vytvoří objekt [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) při volání pomocné metody `View` v metodě akce `Index`. Kód pak předá tento seznam `Movies` z kontroleru k zobrazení:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample5.cs?highlight=3)]

Když jste vytvořili kontroler filmů, Visual Studio Express do horní části souboru *index. cshtml* automaticky zahrnout následující `@model` příkaz:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

Tato direktiva `@model` umožňuje přístup k seznamu filmů, které kontroler předává do zobrazení, pomocí silně typovaného objektu `Model`. Například v šabloně *index. cshtml* kód projde pomocí příkazu `foreach` přes `Model` objekt silného typu:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample7.cshtml?highlight=1,4,7,10,13,16,19-21)]

Vzhledem k tomu, že objekt `Model` je silného typu (jako objekt `IEnumerable<Movie>`), je každý objekt `item` ve smyčce zadán jako `Movie`. Kromě dalších výhod to znamená, že získáte kontrolu v době kompilace kódu a úplnou podporu technologie IntelliSense v editoru kódu:

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="working-with-sql-server-localdb"></a>Práce s SQL Server LocalDB

Entity Framework Code First zjistil, že zadaný připojovací řetězec databáze odkazoval na `Movies` databázi, která ještě neexistuje, takže Code First databázi automaticky vytvořil. Můžete ověřit, že se vytvořila, a to tak, že se podíváte na složku *Data\_App* . Pokud nevidíte soubor *filmy. mdf* , klikněte na tlačítko **Zobrazit všechny soubory** na panelu nástrojů **Průzkumník řešení** , klikněte na tlačítko **aktualizovat** a potom rozbalte složku *\_data App* .

![](accessing-your-models-data-from-a-controller/_static/image6.png)

Dvojím kliknutím na *filmy. mdf* otevřete **Průzkumníka databáze**a potom rozbalte složku **Tables (tabulky** ) a zobrazte tabulku filmů.

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")

> [!NOTE]
> Pokud se Průzkumník databáze nezobrazí, v nabídce **nástroje** vyberte **připojit k databázi**a pak zrušte dialog **Zvolit zdroj dat** . Tím se vynutí otevření Průzkumníka databáze.

> [!NOTE]
> Pokud používáte souboru vwd nebo Visual Studio 2010 a získáte chybu podobnou následující:
> 
> - Databáze ' C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES. MDF nelze otevřít, protože je verze 706. Tento server podporuje verzi 655 a starší. Cesta k downgradu není podporována.
> - &quot;výjimka nebyla ošetřena uživatelským kódem&quot; zadaný SqlConnection neurčuje počáteční katalog.
> 
> Musíte nainstalovat [nástroje SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx) a [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0). Ověřte `MovieDBContext` připojovací řetězec zadaný na předchozí stránce.

Kliknutím pravým tlačítkem na tabulku `Movies` a výběrem **Zobrazit data tabulky** zobrazíte data, která jste vytvořili.

![](accessing-your-models-data-from-a-controller/_static/image8.png)

Klikněte pravým tlačítkem na tabulku `Movies` a vyberte možnost **Otevřít definici tabulky** . zobrazí se struktura tabulky, která Entity Framework Code First vytvořena.

![](accessing-your-models-data-from-a-controller/_static/image9.png "MoviesTable")

![](accessing-your-models-data-from-a-controller/_static/image10.png)

Všimněte si, jak se schéma `Movies` tabulky mapuje na třídu `Movie`, kterou jste vytvořili dříve. Entity Framework Code First automaticky vytvořil toto schéma na základě vaší třídy `Movie`.

Až skončíte, připojení zavřete kliknutím pravým tlačítkem na *MovieDBContext* a výběrem možnosti **Zavřít připojení**. (Pokud připojení neukončíte, při příštím spuštění projektu se může zobrazit chyba.

![](accessing-your-models-data-from-a-controller/_static/image11.png "CloseConnection")

Teď máte databázi a jednoduchou stránku se seznamem, ze které můžete zobrazit obsah. V dalším kurzu prověříme zbytek vygenerovaného kódu a přidáte `SearchIndex` metodu a `SearchIndex` zobrazení, které vám umožní vyhledat filmy v této databázi.

> [!div class="step-by-step"]
> [Předchozí](adding-a-model.md)
> [Další](examining-the-edit-methods-and-edit-view.md)

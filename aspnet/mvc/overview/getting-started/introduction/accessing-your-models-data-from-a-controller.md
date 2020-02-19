---
uid: mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
title: Přístup k datům modelu z kontroleru | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: caa1ba4a-f9f0-4181-ba21-042e3997861d
msc.legacyurl: /mvc/overview/getting-started/introduction/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 5d882d765133d32d3acdba9ffb5d43b69119a273
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457229"
---
# <a name="accessing-your-models-data-from-a-controller"></a>Přístup k datům modelu z kontroleru

od [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

V této části vytvoříte novou třídu `MoviesController` a napíšete kód, který načte data videa a zobrazí se v prohlížeči pomocí šablony zobrazení.

Než začnete pokračovat k dalšímu kroku, **sestavte aplikaci** . Pokud nevytvoříte aplikaci, zobrazí se chyba při přidávání kontroleru.

V Průzkumník řešení klikněte pravým tlačítkem na složku *Controllers* a pak klikněte na **Přidat**a pak na **kontroler**.

![](accessing-your-models-data-from-a-controller/_static/image1.png)

V dialogovém okně **Přidat vygenerované uživatelské rozhraní** klikněte na **kontroler MVC 5 se zobrazeními, pomocí Entity Framework**a pak klikněte na **Přidat**.

![](accessing-your-models-data-from-a-controller/_static/image2.png)

- Vyberte **video (MvcMovie. Models)** pro třídu modelu.
- Jako třídu kontextu dat vyberte **MovieDBContext (MvcMovie. Models)** .
- Jako název kontroleru zadejte **MoviesController**.

  Následující obrázek ukazuje dokončený dialog.  
  
![](accessing-your-models-data-from-a-controller/_static/image3.png)   

Klikněte na **Přidat**. (Pokud se zobrazí chyba, pravděpodobně jste před zahájením přidávání kontroleru aplikaci nesestavili.) Visual Studio vytvoří následující soubory a složky:

- Soubor *MoviesController.cs* ve složce *Controllers* .
- Složka *Views\Movies*
- *Vytvořte. cshtml, odstraňte. cshtml, details. cshtml, upravte. cshtml*a *index. cshtml* ve složce New *Views\Movies* .

Aplikace Visual Studio automaticky vytvořila metody a zobrazení akcí [CRUD](http://en.wikipedia.org/wiki/Create,_read,_update_and_delete) (vytváření, čtení, aktualizace a odstraňování) (automatické vytváření metod a zobrazení operace CRUD se říká generování uživatelského rozhraní). Nyní máte plně funkční webovou aplikaci, která umožňuje vytvářet, zobrazovat, upravovat a odstraňovat položky filmů.

Spusťte aplikaci a klikněte na filmový odkaz **MVC** (nebo přejděte k řadiči `Movies` připojením */Movies* k adrese URL v adresním řádku prohlížeče). Vzhledem k tomu, že se aplikace spoléhá na výchozí směrování (definované v souboru *App\_Start\RouteConfig.cs* ), požadavek `http://localhost:xxxxx/Movies` prohlížeče se směruje na výchozí metodu `Index` akce kontroleru `Movies`. Jinými slovy, `http://localhost:xxxxx/Movies` požadavek prohlížeče je ve skutečnosti stejný jako `http://localhost:xxxxx/Movies/Index`žádosti prohlížeče. Výsledkem je prázdný seznam filmů, protože jste to ještě nepřidali.

![](accessing-your-models-data-from-a-controller/_static/image4.png)

### <a name="creating-a-movie"></a>Vytvoření filmu

Vyberte odkaz **vytvořit nový** . Zadejte podrobnosti o videu a potom klikněte na tlačítko **vytvořit** .

![](accessing-your-models-data-from-a-controller/_static/image5.png)

> [!NOTE]
> V poli Price možná nebudete moct zadat desetinné nebo čárkové tečky. aby bylo možné podporovat ověřování jQuery pro jiné než anglické národní prostředí, které používá čárku (&quot;,&quot;) pro desetinnou čárku a formáty kalendářních dat, které nejsou v češtině, je nutné zahrnout *globalizaci. js* a konkrétní soubory *kultury/globalizace. js* (z [https://github.com/jquery/globalize](https://github.com/jquery/globalize) ) a JavaScript pro použití `Globalize.parseFloat`. Ukážeme si, jak to udělat v dalším kurzu. Prozatím stačí zadat celá čísla, třeba 10.

Kliknutím na tlačítko **vytvořit** dojde k odeslání formuláře na server, kde jsou informace o filmu uloženy v databázi. Pak budete přesměrováni na adresu URL */Movies* , kde uvidíte nově vytvořený film v seznamu.

![](accessing-your-models-data-from-a-controller/_static/image6.png)

Vytvořte ještě několik dalších záznamů filmů. Zkuste odkazy **Upravit**, **Podrobnosti**a **Odstranit** , které jsou všechny funkční.

## <a name="examining-the-generated-code"></a>Prověřování generovaného kódu

Otevřete soubor *Controllers\MoviesController.cs* a prověřte vygenerovanou metodu `Index`. Část kontroleru videí s metodou `Index` je uvedena níže.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

Požadavek na kontroler `Movies` vrátí všechny položky v tabulce `Movies` a poté předá výsledky do zobrazení `Index`. Následující řádek z třídy `MoviesController` vytváří instanci kontextu databáze videa, jak je popsáno výše. Můžete použít kontext databáze videa k dotazování, úpravám a odstraňování filmů.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

## <a name="strongly-typed-models-and-the-model-keyword"></a>Modely silného typu a klíčové slovo @model

Dříve v tomto kurzu jste viděli, jak může řadič předat data nebo objekty do šablony zobrazení pomocí objektu `ViewBag`. `ViewBag` je dynamický objekt, který poskytuje pohodlný způsob, jak předat informace do zobrazení.

MVC také poskytuje možnost předat objekty *silného* typu do šablony zobrazení. Tento přístup silného typu umožňuje lepší kontrolu kódu a bohatší [IntelliSense](https://msdn.microsoft.com/library/hcw1s69b(v=vs.120).aspx) v editoru sady Visual Studio. Mechanismus generování uživatelského rozhraní v aplikaci Visual Studio používal tento přístup (to znamená předání modelu *silného* typu) s třídou `MoviesController` a zobrazení šablon při vytváření metod a zobrazení.

V souboru *Controllers\MoviesController.cs* prověřte vygenerovanou metodu `Details`. Níže je uvedena metoda `Details`.

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs)]

Parametr `id` se obecně předává jako data směrování, například `http://localhost:1234/movies/details/1` nastaví kontroler na filmový kontroler, akci na `details` a `id` na 1. ID můžete předat také řetězci dotazu následujícím způsobem:

`http://localhost:1234/movies/details?id=1`

Pokud je nalezen `Movie`, je do zobrazení `Details` předána instance `Movie` modelu:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample4.cs)]

Projděte si obsah souboru *Views\Movies\Details.cshtml* :

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.cshtml?highlight=1-2)]

Zahrnutím příkazu `@model` v horní části souboru šablony zobrazení můžete určit typ objektu, který zobrazení očekává. Když jste vytvořili kontroler filmů, Visual Studio automaticky v horní části souboru *Details. cshtml* obsahuje následující příkaz `@model`:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

Tato direktiva `@model` umožňuje přístup k videu, který kontroler předává do zobrazení pomocí objektu `Model` se silným typem. Například v šabloně *Details. cshtml* kód předá do každého pole video `DisplayNameFor` a [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) nápovědu HTML pomocí objektu silného typu `Model`. Metody `Create` a `Edit` a šablony zobrazení také předají objekt filmového modelu.

Prohlédněte si šablonu zobrazení *index. cshtml* a metodu `Index` v souboru *MoviesController.cs* . Všimněte si, jak kód vytvoří objekt [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) při volání pomocné metody `View` v metodě akce `Index`. Kód pak předá tento seznam `Movies` z metody `Index` akce do zobrazení:

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample7.cs?highlight=3)]

Když jste vytvořili kontroler filmů, Visual Studio automaticky obsahuje následující příkaz `@model` v horní části souboru *index. cshtml* :

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample8.cshtml)]

Tato direktiva `@model` umožňuje přístup k seznamu filmů, které kontroler předává do zobrazení, pomocí silně typovaného objektu `Model`. Například v šabloně *index. cshtml* kód projde pomocí příkazu `foreach` přes `Model` objekt silného typu:

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample9.cshtml?highlight=1,4,7,10,13,16,19-21)]

Vzhledem k tomu, že objekt `Model` je silného typu (jako objekt `IEnumerable<Movie>`), je každý objekt `item` ve smyčce zadán jako `Movie`. Kromě dalších výhod to znamená, že získáte kontrolu v době kompilace kódu a úplnou podporu technologie IntelliSense v editoru kódu:

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image8.png)

## <a name="working-with-sql-server-localdb"></a>Práce s SQL Server LocalDB

Entity Framework Code First zjistil, že zadaný připojovací řetězec databáze odkazoval na `Movies` databázi, která ještě neexistuje, takže Code First databázi automaticky vytvořil. Můžete ověřit, že se vytvořila, a to tak, že se podíváte na složku *Data\_App* . Pokud nevidíte soubor *filmy. mdf* , klikněte na tlačítko **Zobrazit všechny soubory** na panelu nástrojů **Průzkumník řešení** , klikněte na tlačítko **aktualizovat** a potom rozbalte složku *\_data App* .

![](accessing-your-models-data-from-a-controller/_static/image9.png)

Dvojím kliknutím na *filmy. mdf* otevřete **Průzkumníka serveru**a potom rozbalte složku **Tables (tabulky** ) a zobrazte tabulku filmů. Poznamenejte si klíčovou ikonu vedle pole ID. Ve výchozím nastavení vlastnost EF vytvoří primární klíč s názvem ID. Další informace o EF a MVC najdete v Dykstra skvělého kurzu na [MVC a EF](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

![DB_explorer](accessing-your-models-data-from-a-controller/_static/image10.png "DB_explorer")

Kliknutím pravým tlačítkem na tabulku `Movies` a výběrem **Zobrazit data tabulky** zobrazíte data, která jste vytvořili.

![](accessing-your-models-data-from-a-controller/_static/image11.png) 

![](accessing-your-models-data-from-a-controller/_static/image12.png)

Klikněte pravým tlačítkem na tabulku `Movies` a vyberte možnost **Otevřít definici tabulky** . zobrazí se struktura tabulky, která Entity Framework Code First vytvořena.

![](accessing-your-models-data-from-a-controller/_static/image13.png)

![](accessing-your-models-data-from-a-controller/_static/image14.png)

Všimněte si, jak se schéma `Movies` tabulky mapuje na třídu `Movie`, kterou jste vytvořili dříve. Entity Framework Code First automaticky vytvořil toto schéma na základě vaší třídy `Movie`.

Až skončíte, připojení zavřete kliknutím pravým tlačítkem na *MovieDBContext* a výběrem možnosti **Zavřít připojení**. (Pokud připojení neukončíte, při příštím spuštění projektu se může zobrazit chyba.

![](accessing-your-models-data-from-a-controller/_static/image15.png "CloseConnection")

Teď máte databázi a stránky k zobrazení, úpravám, aktualizaci a odstraňování dat. V dalším kurzu prověříme zbytek vygenerovaného kódu a přidáte `SearchIndex` metodu a `SearchIndex` zobrazení, které vám umožní vyhledat filmy v této databázi. Další informace o použití Entity Framework s MVC najdete v tématu [vytvoření datového modelu Entity Framework pro aplikaci ASP.NET MVC](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

> [!div class="step-by-step"]
> [Předchozí](creating-a-connection-string.md)
> [Další](examining-the-edit-methods-and-edit-view.md)

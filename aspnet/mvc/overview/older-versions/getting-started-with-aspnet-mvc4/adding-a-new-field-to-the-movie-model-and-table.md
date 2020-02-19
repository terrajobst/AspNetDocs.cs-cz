---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
title: Přidání nového pole do modelu a tabulky filmů | Microsoft Docs
author: Rick-Anderson
description: 'Poznámka: v této části je k dispozici aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013. Je to bezpečnější, takže je mnohem jednodušší postupovat a demo...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 9ef2c4f1-a305-4e0a-9fb8-bfbd9ef331d9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
msc.type: authoredcontent
ms.openlocfilehash: d966b95163f64b20a17d2327a12c5d6c44a4a66b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457697"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table"></a>Přidání nového pole do modelu a tabulky Movie

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > K [dispozici je](../../getting-started/introduction/getting-started.md) aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013. Je to bezpečnější, mnohem jednodušší a ukazuje více funkcí.

V této části použijete Migrace Entity Framework Code First k migraci některých změn do tříd modelu, takže se změna aplikuje na databázi.

Ve výchozím nastavení platí, že při použití Entity Framework Code First k automatickému vytvoření databáze, stejně jako v tomto kurzu, Code First přidá do databáze tabulku, která bude sledovat, zda je schéma databáze synchronizované s třídami modelů, ze kterých byla vygenerována. Pokud nejsou synchronizované, Entity Framework vyvolá chybu. Díky tomu je snazší sledovat problémy v době vývoje, které byste jinak mohli najít (překrytím chyb) v době běhu.

## <a name="setting-up-code-first-migrations-for-model-changes"></a>Nastavení Migrace Code First pro změny modelu

Pokud používáte Visual Studio 2012, poklikejte na soubor *filmů. mdf* z Průzkumník řešení a otevřete nástroj Database Tool. Visual Studio Express pro web se zobrazí Průzkumník databáze, v aplikaci Visual Studio 2012 se zobrazí Průzkumník serveru. Pokud používáte Visual Studio 2010, použijte Průzkumník objektů systému SQL Server.

V databázovém nástroji (Průzkumník databáze Průzkumník serveru nebo Průzkumník objektů systému SQL Server) klikněte pravým tlačítkem na `MovieDBContext` a výběrem **Odstranit** vyřaďte databázi filmů.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image1.png)

Přejděte zpět na Průzkumník řešení. Klikněte pravým tlačítkem na soubor *filmů. mdf* a výběrem **Odstranit** odeberte databázi filmů.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image2.png)

Sestavte aplikaci, abyste se ujistili, že nejsou k dispozici žádné chyby.

V nabídce **Nástroje** klikněte na **Správce balíčků NuGet** a pak na **Konzola Správce balíčků**.

![Přidat Man Pack](adding-a-new-field-to-the-movie-model-and-table/_static/image3.png)

V okně **konzoly Správce balíčků** na `PM>`ovém řádku zadejte Enable-migrations-ContextTypeName MvcMovie. Models. MovieDBContext.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image4.png)

Příkaz **Povolit – migrace** (zobrazený výše) vytvoří soubor *Configuration.cs* v nové složce *migrace* .

![](adding-a-new-field-to-the-movie-model-and-table/_static/image5.png)

Visual Studio otevře soubor *Configuration.cs* . Metodu `Seed` v souboru *Configuration.cs* nahraďte následujícím kódem:

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample1.cs)]

Klikněte pravým tlačítkem myši na červenou vlnovku pod `Movie` a vyberte **vyřešit** a pak **použijte** **MvcMovie. Models;**

![](adding-a-new-field-to-the-movie-model-and-table/_static/image6.png)

Tím přidáte následující příkaz using:

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample2.cs)]

> [!NOTE] 
> 
> Migrace Code First volá metodu `Seed` po každé migraci (to znamená volání metody **Update-Database** v konzole správce balíčků) a tato metoda aktualizuje řádky, které již byly vloženy, nebo je vloží, pokud ještě neexistují.

**Stisknutím kombinace kláves CTRL + SHIFT + B Sestavte projekt.** (Pokud v tomto okamžiku nebudete sestavovat, následující kroky selžou.)

Dalším krokem je vytvoření třídy `DbMigration` pro prvotní migraci. Tato migrace vytvoří novou databázi. to je důvod, proč jste odstranili soubor *Movie. mdf* v předchozím kroku.

V okně **konzoly Správce balíčků** zadejte příkaz "Přidání-migrace počátečního" a vytvořte prvotní migraci. Název "Initial" je libovolný a slouží k pojmenování vytvořeného souboru migrace.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image7.png)

Migrace Code First vytvoří další soubor třídy ve složce *migrations* (s názvem *{DateStamp}\_Initial.cs* ) a tato třída obsahuje kód, který vytvoří schéma databáze. Název souboru migrace je předem vyřešen s časovým razítkem, které vám pomůžou s řazením. Projděte si soubor *{dateStamp}\_Initial.cs* , který obsahuje pokyny k vytvoření tabulky filmů pro filmovou databázi. Při aktualizaci databáze v níže uvedených pokynech se tento soubor *{dateStamp}\_Initial.cs* spustí a vytvoří se schéma databáze. Pak se metoda **počáteční** hodnoty spustí k naplnění databáze testovacími daty.

V **konzole správce balíčků**zadejte příkaz "Update-Database" a vytvořte databázi a spusťte metodu **počáteční** hodnoty.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image8.png)

Pokud se zobrazí chyba, která indikuje, že tabulka již existuje a nelze ji vytvořit, je pravděpodobné, že jste aplikaci spustili po odstranění databáze a před provedením `update-database`. V takovém případě odstraňte soubor *Movies. mdf* znovu a opakujte příkaz `update-database`. Pokud se vám stále stala chyba, odstraňte složku a obsah migrace a pak začněte s pokyny v horní části této stránky (to znamená odstranění souboru *filmů. mdf* a následného povolení migrace).

Spusťte aplikaci a přejděte na adresu URL */Movies* . Zobrazí se data počáteční hodnoty.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image9.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a>Přidání vlastnosti hodnocení do modelu videa

Začněte přidáním nové vlastnosti `Rating` do existující třídy `Movie`. Otevřete soubor *Models\Movie.cs* a přidejte vlastnost `Rating`, jako je tato:

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample3.cs)]

Úplná `Movie` třída teď vypadá jako v následujícím kódu:

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample4.cs?highlight=8)]

Sestavte aplikaci pomocí příkazu nabídky **build** &gt;**Build Movie** nebo stisknutím kombinace kláves CTRL + SHIFT + B.

Teď, když jste aktualizovali `Model` třídu, budete také muset aktualizovat šablony zobrazení *\Views\Movies\Index.cshtml* a *\Views\Movies\Create.cshtml* , aby se zobrazila nová vlastnost `Rating` v zobrazení prohlížeče.

Otevřete soubor<em>\Views\Movies\Index.cshtml</em> a přidejte `<th>Rating</th>` záhlaví sloupce hned za sloupec <strong>Price</strong> . Pak přidejte `<td>` sloupec poblíž konce šablony, aby se vygenerovala `@item.Rating` hodnota. Níže vidíte, že aktualizovaná šablona zobrazení <em>index. cshtml</em> vypadá takto:

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample5.cshtml?highlight=26-28,46-48)]

Potom otevřete soubor *\Views\Movies\Create.cshtml* a přidejte následující kód poblíž konce formuláře. Tím vykreslíte textové pole, abyste mohli při vytváření nového filmu zadat hodnocení.

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample6.cshtml)]

Nyní jste aktualizovali kód aplikace, aby podporoval novou vlastnost `Rating`.

Nyní spusťte aplikaci a přejděte na adresu URL */Movies* . Když to uděláte, zobrazí se jedna z následujících chyb:

![](adding-a-new-field-to-the-movie-model-and-table/_static/image10.png)

![](adding-a-new-field-to-the-movie-model-and-table/_static/image11.png)

Tato chyba se zobrazuje, protože aktualizovaná třída modelu `Movie` v aplikaci je nyní odlišná od schématu `Movie` tabulky existující databáze. (V tabulce databáze nejsou žádné `Rating` sloupce.)

K řešení této chyby je potřeba několik přístupů:

1. Entity Framework automaticky vyřadit a znovu vytvořit databázi na základě nového schématu třídy modelu. Tento přístup je velmi výhodný při aktivním vývoji na testovací databázi. umožňuje rychlou vývoj modelu a schématu databáze dohromady. Nevýhodou, ale je to, že ztratíte stávající data v databázi, takže *nechcete tento* přístup použít v provozní databázi. Použití inicializátoru k automatickému osazení databáze s testovacími daty je často produktivním způsobem pro vývoj aplikace. Další informace o Entity Frameworkch inicializátorech databáze najdete v [kurzu ASP.NET MVC/Entity Framework](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)Dykstra.
2. Explicitně upravte schéma existující databáze tak, aby odpovídalo třídám modelu. Výhodou tohoto přístupu je, že zachováte data. Tuto změnu můžete provést buď ručně, nebo vytvořením skriptu změny databáze.
3. K aktualizaci schématu databáze použijte Migrace Code First.

V tomto kurzu použijeme Migrace Code First.

Aktualizujte metodu počáteční hodnoty tak, aby poskytovala hodnotu pro nový sloupec. Otevřete soubor Migrations\Configuration.cs a přidejte pole hodnocení do každého objektu filmu.

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample7.cs?highlight=6)]

Sestavte řešení a otevřete okno **konzoly Správce balíčků** a zadejte následující příkaz:

`add-migration AddRatingMig`

Příkaz `add-migration` oznamuje migračnímu rozhraní, aby kontroloval aktuální model videa s aktuálním schématem video DB a vytvořil potřebný kód pro migraci databáze do nového modelu. AddRatingMig je libovolný a slouží k pojmenování souboru migrace. Je užitečné použít pro krok migrace smysluplný název.

Po dokončení tohoto příkazu aplikace Visual Studio otevře soubor třídy definující novou `DbMigration` odvozenou třídu a v metodě `Up` můžete zobrazit kód, který vytvoří nový sloupec.

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample8.cs)]

Sestavte řešení a potom v okně **konzoly Správce balíčků** zadejte příkaz Update-Database.

Následující obrázek ukazuje výstup v okně **konzoly Správce balíčků** (AddRatingMig data razítko se liší.)

![](adding-a-new-field-to-the-movie-model-and-table/_static/image12.png)

Spusťte aplikaci znovu a přejděte na adresu URL/Movies. Můžete zobrazit nové pole hodnocení.

![](adding-a-new-field-to-the-movie-model-and-table/_static/image13.png)

Kliknutím na odkaz **vytvořit nový** přidejte nový film. Všimněte si, že můžete přidat hodnocení.

![7_CreateRioII](adding-a-new-field-to-the-movie-model-and-table/_static/image14.png)

Klikněte na možnost **Vytvořit**. Nový film, včetně hodnocení, se teď zobrazí v seznamu filmů:

![7_ourNewMovie_SM](adding-a-new-field-to-the-movie-model-and-table/_static/image15.png)

Do šablon zobrazení Edit, Details a SearchIndex byste měli také přidat pole `Rating`.

Znovu můžete zadat příkaz "aktualizovat databázi" v okně **konzoly Správce balíčků** a provést žádné změny, protože schéma odpovídá modelu.

V této části jste viděli, jak můžete upravovat objekty modelu a udržovat databázi synchronizované se změnami. Zjistili jste taky způsob, jak naplnit nově vytvořenou databázi pomocí ukázkových dat, abyste si mohli vyzkoušet scénáře. Teď se podíváme na to, jak můžete přidat bohatou logiku ověřování do tříd modelu a povolit uplatnění některých obchodních pravidel.

> [!div class="step-by-step"]
> [Předchozí](examining-the-edit-methods-and-edit-view.md)
> [Další](adding-validation-to-the-model.md)

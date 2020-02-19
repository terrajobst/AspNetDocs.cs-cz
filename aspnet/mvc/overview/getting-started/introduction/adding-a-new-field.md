---
uid: mvc/overview/getting-started/introduction/adding-a-new-field
title: Přidání nového pole | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 4085de68-d243-4378-8a64-86236ea8d2da
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 5974e53e4610dccc7812df261dc97a9b0327de85
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456683"
---
# <a name="adding-a-new-field"></a>Přidání nového pole

od [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

V této části použijete Migrace Entity Framework Code First k migraci některých změn do tříd modelu, takže se změna aplikuje na databázi.

Ve výchozím nastavení platí, že při použití Entity Framework Code First k automatickému vytvoření databáze, stejně jako v tomto kurzu, Code First přidá do databáze tabulku, která bude sledovat, zda je schéma databáze synchronizované s třídami modelů, ze kterých byla vygenerována. Pokud nejsou synchronizované, Entity Framework vyvolá chybu. Díky tomu je snazší sledovat problémy v době vývoje, které byste jinak mohli najít (překrytím chyb) v době běhu.

## <a name="setting-up-code-first-migrations-for-model-changes"></a>Nastavení Migrace Code First pro změny modelu

Přejděte na Průzkumník řešení. Klikněte pravým tlačítkem na soubor *filmů. mdf* a výběrem **Odstranit** odeberte databázi filmů. Pokud nevidíte soubor *filmy. mdf* , klikněte na ikonu **Zobrazit všechny soubory** zobrazené níže v červeném obrysu.

![](adding-a-new-field/_static/image1.png)

Sestavte aplikaci, abyste se ujistili, že nejsou k dispozici žádné chyby.

V nabídce **Nástroje** klikněte na **Správce balíčků NuGet** a pak na **Konzola Správce balíčků**.

![Přidat Man Pack](adding-a-new-field/_static/image2.png)

V okně **konzoly Správce balíčků** na `PM>` příkazovém řádku zadejte

Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext

![](adding-a-new-field/_static/image3.png)

Příkaz **Povolit – migrace** (zobrazený výše) vytvoří soubor *Configuration.cs* v nové složce *migrace* .

![](adding-a-new-field/_static/image4.png)

Visual Studio otevře soubor *Configuration.cs* . Metodu `Seed` v souboru *Configuration.cs* nahraďte následujícím kódem:

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

Najeďte myší na červenou vlnovku pod `Movie` a klikněte na `Show Potential Fixes` a pak klikněte na **použití** **MvcMovie. Models;**

![](adding-a-new-field/_static/image5.png)

Tím přidáte následující příkaz using:

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

> [!NOTE]
> 
> Migrace Code First volá metodu `Seed` po každé migraci (to znamená volání metody **Update-Database** v konzole správce balíčků) a tato metoda aktualizuje řádky, které již byly vloženy, nebo je vloží, pokud ještě neexistují.
> 
> Metoda [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) v následujícím kódu provádí operaci "Upsert":
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample3.cs)]
> 
> Vzhledem k tomu, že metoda [počáteční](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) hodnoty se spouští při každé migraci, nemůžete pouze vkládat data, protože řádky, které se pokoušíte přidat, budou již po první migraci, která databázi vytvořila, k dispozici. Operace "[Upsert](http://en.wikipedia.org/wiki/Upsert)" zabraňuje chybám, které by byly provedeny při pokusu o vložení řádku, který již existuje, ale přepíše všechny změny dat, které jste mohli provést při testování aplikace. S testovacími daty v některých tabulkách možná nebudete chtít, aby došlo k tomu, že v některých případech změníte data při testování, které chcete po aktualizaci databáze zůstat. V takovém případě chcete provést operaci podmíněného vložení: vložte řádek pouze v případě, že ještě neexistuje.   
> 
> První parametr předaný metodě [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) určuje vlastnost, která má být použita pro kontrolu, zda řádek již existuje. Pro testovací data, která poskytujete, se vlastnost `Title` dá použít k tomuto účelu, protože každý název v seznamu je jedinečný:
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample4.cs)]
> 
> Tento kód předpokládá, že názvy jsou jedinečné. Pokud ručně přidáte duplicitní název, při příštím provedení migrace se zobrazí následující výjimka.   
> 
> *Sekvence obsahuje více než jeden element.*  
> 
> Další informace o metodě [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) naleznete v tématu [postará se o metodu EF 4,3 AddOrUpdate](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)..

**Stisknutím kombinace kláves CTRL + SHIFT + B Sestavte projekt.** (Následující kroky selžou, pokud v tomto okamžiku nebudete sestavovat.)

Dalším krokem je vytvoření třídy `DbMigration` pro prvotní migraci. Tato migrace vytvoří novou databázi. to je důvod, proč jste odstranili soubor *Movie. mdf* v předchozím kroku.

V okně **konzoly Správce balíčků** zadejte příkaz `add-migration Initial` pro vytvoření prvotní migrace. Název "Initial" je libovolný a slouží k pojmenování vytvořeného souboru migrace.

![](adding-a-new-field/_static/image6.png)

Migrace Code First vytvoří další soubor třídy ve složce *migrations* (s názvem *{DateStamp}\_Initial.cs* ) a tato třída obsahuje kód, který vytvoří schéma databáze. Název souboru migrace je předem vyřešen s časovým razítkem, které vám pomůžou s řazením. Projděte si soubor *{dateStamp}\_Initial.cs* , který obsahuje pokyny pro vytvoření tabulky `Movies` pro filmovou databázi. Při aktualizaci databáze v níže uvedených pokynech se tento soubor *{dateStamp}\_Initial.cs* spustí a vytvoří se schéma databáze. Pak se metoda **počáteční** hodnoty spustí k naplnění databáze testovacími daty.

V **konzole správce balíčků**zadejte příkaz `update-database` pro vytvoření databáze a spuštění metody `Seed`.

![](adding-a-new-field/_static/image7.png)

Pokud se zobrazí chyba, která indikuje, že tabulka již existuje a nelze ji vytvořit, je pravděpodobné, že jste aplikaci spustili po odstranění databáze a před provedením `update-database`. V takovém případě odstraňte soubor *Movies. mdf* znovu a opakujte příkaz `update-database`. Pokud se vám stále stala chyba, odstraňte složku a obsah migrace a pak začněte s pokyny v horní části této stránky (to znamená odstranění souboru *filmů. mdf* a následného povolení migrace). Pokud se stále zobrazí chyba, otevřete Průzkumník objektů systému SQL Server a odeberte databázi ze seznamu.

Spusťte aplikaci a přejděte na adresu URL */Movies* . Zobrazí se data počáteční hodnoty.

![](adding-a-new-field/_static/image8.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a>Přidání vlastnosti hodnocení do modelu videa

Začněte přidáním nové vlastnosti `Rating` do existující třídy `Movie`. Otevřete soubor *Models\Movie.cs* a přidejte vlastnost `Rating`, jako je tato:

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

Úplná `Movie` třída teď vypadá jako v následujícím kódu:

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs?highlight=12)]

Sestavte aplikaci (CTRL + SHIFT + B).

Vzhledem k tomu, že jste přidali nové pole do `Movie` třídy, budete také muset aktualizovat *seznam* vazeb, aby byla tato nová vlastnost zahrnutá. Aktualizujte atribut `bind` pro metody `Create` a `Edit` akcí tak, aby zahrnovaly vlastnost `Rating`:

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs?highlight=1)]

Je také nutné aktualizovat šablony zobrazení, aby se zobrazily, vytvořili a upravili novou vlastnost `Rating` v zobrazení prohlížeče.

Otevřete soubor *\Views\Movies\Index.cshtml* a přidejte `<th>Rating</th>` záhlaví sloupce hned za sloupec **Price** . Pak přidejte `<td>` sloupec poblíž konce šablony, aby se vygenerovala `@item.Rating` hodnota. Níže vidíte, že aktualizovaná šablona zobrazení *index. cshtml* vypadá takto:

[!code-cshtml[Main](adding-a-new-field/samples/sample8.cshtml?highlight=31-33,52-54)]

Potom otevřete soubor *\Views\Movies\Create.cshtml* a přidejte pole `Rating` s následujícím zvýrazněným označením. Tím vykreslíte textové pole, abyste mohli při vytváření nového filmu zadat hodnocení.

[!code-cshtml[Main](adding-a-new-field/samples/sample9.cshtml?highlight=9-15)]

Nyní jste aktualizovali kód aplikace, aby podporoval novou vlastnost `Rating`.

Spusťte aplikaci a přejděte na adresu URL */Movies* . Když to uděláte, zobrazí se jedna z následujících chyb:

![](adding-a-new-field/_static/image9.png)  
  
Model, který provedl zálohování kontextu ' MovieDBContext ', se od vytvoření databáze změnil. Zvažte použití Migrace Code First k aktualizaci databáze (https://go.microsoft.com/fwlink/?LinkId=238269).

![](adding-a-new-field/_static/image10.png)

Tato chyba se zobrazuje, protože aktualizovaná třída modelu `Movie` v aplikaci je nyní odlišná od schématu `Movie` tabulky existující databáze. (V tabulce databáze nejsou žádné `Rating` sloupce.)

K řešení této chyby je potřeba několik přístupů:

1. Entity Framework automaticky vyřadit a znovu vytvořit databázi na základě nového schématu třídy modelu. Tento přístup je velmi výhodný v rané fázi vývoje, když provádíte aktivní vývoj na testovací databázi. umožňuje rychlou vývoj modelu a schématu databáze dohromady. Nevýhodou, ale je to, že ztratíte stávající data v databázi, takže *nechcete tento* přístup použít v provozní databázi. Použití inicializátoru k automatickému osazení databáze s testovacími daty je často produktivním způsobem pro vývoj aplikace. Další informace o Entity Framework inicializátorech databáze najdete v [kurzu ASP.NET MVC/Entity Framework](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).
2. Explicitně upravte schéma existující databáze tak, aby odpovídalo třídám modelu. Výhodou tohoto přístupu je, že zachováte data. Tuto změnu můžete provést buď ručně, nebo vytvořením skriptu změny databáze.
3. K aktualizaci schématu databáze použijte Migrace Code First.

V tomto kurzu použijeme Migrace Code First.

Aktualizujte metodu počáteční hodnoty tak, aby poskytovala hodnotu pro nový sloupec. Otevřete soubor Migrations\Configuration.cs a přidejte pole hodnocení do každého objektu filmu.

[!code-csharp[Main](adding-a-new-field/samples/sample10.cs?highlight=6)]

Sestavte řešení a otevřete okno **konzoly Správce balíčků** a zadejte následující příkaz:

`add-migration Rating`

Příkaz `add-migration` oznamuje migračnímu rozhraní, aby kontroloval aktuální model videa s aktuálním schématem video DB a vytvořil potřebný kód pro migraci databáze do nového modelu. *Hodnocení* názvu je libovolné a slouží k pojmenování souboru migrace. Je užitečné použít pro krok migrace smysluplný název.

Po dokončení tohoto příkazu aplikace Visual Studio otevře soubor třídy definující novou `DbMigration` odvozenou třídu a v metodě `Up` můžete zobrazit kód, který vytvoří nový sloupec.

[!code-csharp[Main](adding-a-new-field/samples/sample11.cs)]

Sestavte řešení a potom v okně **konzoly Správce balíčků** zadejte příkaz `update-database`.

Následující obrázek ukazuje výstup v okně **konzoly Správce balíčků** (nedokončené *hodnocení* data razítka se liší.)

![](adding-a-new-field/_static/image11.png)

Spusťte aplikaci znovu a přejděte na adresu URL/Movies. Můžete zobrazit nové pole hodnocení.

![](adding-a-new-field/_static/image12.png)

Kliknutím na odkaz **vytvořit nový** přidejte nový film. Všimněte si, že můžete přidat hodnocení.

![7_CreateRioII](adding-a-new-field/_static/image13.png)

Klikněte na možnost **Vytvořit**. Nový film, včetně hodnocení, se teď zobrazí v seznamu filmů:

![7_ourNewMovie_SM](adding-a-new-field/_static/image14.png)

Teď, když projekt používá migrace, nebudete muset databázi vyřadit, když přidáte nové pole nebo jinak aktualizujete schéma. V další části provedete další změny schématu a použijete migrace k aktualizaci databáze.

Měli byste také přidat pole `Rating` do šablon zobrazení upravit, podrobnosti a odstranit.

Znovu můžete zadat příkaz "aktualizovat databázi" v okně **konzoly Správce balíčků** a spustit žádný kód migrace, protože schéma odpovídá modelu. Spuštěním příkazu "Update-Database" však znovu spustíte metodu `Seed`, a pokud jste změnili jakékoli počáteční údaje, změny se ztratí, protože `Seed` metoda upsertuje data. Další informace o metodě `Seed` najdete v oblíbeném [kurzu ASP.NET MVC/Entity Framework](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)Dykstra.

V této části jste viděli, jak můžete upravovat objekty modelu a udržovat databázi synchronizované se změnami. Zjistili jste taky způsob, jak naplnit nově vytvořenou databázi pomocí ukázkových dat, abyste si mohli vyzkoušet scénáře. Toto bylo jenom rychlý Úvod k Code First. Další informace najdete v tématu [vytvoření datového modelu Entity Framework pro aplikaci ASP.NET MVC](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) pro ucelený kurz na daném předmětu. Teď se podíváme na to, jak můžete přidat bohatou logiku ověřování do tříd modelu a povolit uplatnění některých obchodních pravidel.

> [!div class="step-by-step"]
> [Předchozí](adding-search.md)
> [Další](adding-validation.md)

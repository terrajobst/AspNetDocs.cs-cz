---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
title: Vytváření tříd modelu pomocí LINQ to SQL (VB) | Microsoft Docs
author: microsoft
description: Cílem tohoto kurzu je vysvětlit jednu metodu vytváření tříd modelů pro aplikaci ASP.NET MVC. V tomto kurzu se naučíte sestavit model c...
ms.author: riande
ms.date: 10/07/2008
ms.assetid: a4a25a75-d71f-4509-98b4-df72e748985a
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-linq-to-sql-vb
msc.type: authoredcontent
ms.openlocfilehash: 88a5f1037d93ef3bdc95bf60b6005ebb254ab440
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74588457"
---
# <a name="creating-model-classes-with-linq-to-sql-vb"></a>Vytvoření tříd modelu pomocí LINQ to SQL (VB)

od [Microsoftu](https://github.com/microsoft)

[Stáhnout PDF](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_10_VB.pdf)

> Cílem tohoto kurzu je vysvětlit jednu metodu vytváření tříd modelů pro aplikaci ASP.NET MVC. V tomto kurzu se naučíte, jak sestavovat třídy modelů a provádět přístup k databázím díky využití LINQ to SQL Microsoftu.

Cílem tohoto kurzu je vysvětlit jednu metodu vytváření tříd modelů pro aplikaci ASP.NET MVC. V tomto kurzu se naučíte, jak sestavovat třídy modelů a provádět přístup k databázím díky využití LINQ to SQL Microsoftu.

V tomto kurzu sestavíme základní aplikaci video Database. Začneme vytvořením aplikace filmové databáze nejrychleji a nejjednodušší možností. Veškerý přístup k datům provádíme přímo z našich akcí kontroleru.

V dalším kroku se naučíte používat vzor úložiště. Použití vzoru úložiště vyžaduje trochu více práce. Výhodou toho, jak tento model obdržíte, je však, že umožňuje sestavovat aplikace, které lze upravit a lze je snadno testovat.

## <a name="what-is-a-model-class"></a>Co je třída modelu?

Model MVC obsahuje veškerou aplikační logiku, která není obsažena v zobrazení MVC nebo řadiči MVC. Konkrétně model MVC obsahuje všechny vaše aplikace a logiku přístupu k datům.

K implementaci logiky přístupu k datům můžete použít celou řadu různých technologií. Můžete například sestavit třídy pro přístup k datům pomocí tříd Microsoft Entity Framework, NHibernate, Subsonic nebo ADO.NET.

V tomto kurzu používám LINQ to SQL k dotazování a aktualizaci databáze. LINQ to SQL poskytuje velmi snadnou metodu interakce s databází Microsoft SQL Server. Je ale důležité pochopit, že rozhraní ASP.NET MVC není vázané na LINQ to SQL jakýmkoli způsobem. ASP.NET MVC je kompatibilní se všemi technologiemi pro přístup k datům.

## <a name="create-a-movie-database"></a>Vytvoření filmové databáze

V tomto kurzu – pro ilustraci, jak můžete sestavovat třídy modelu – sestavíme jednoduchou aplikaci filmové databáze. Prvním krokem je vytvoření nové databáze. V okně Průzkumník řešení klikněte pravým tlačítkem na složku data\_aplikace a vyberte možnost nabídky **Přidat, nová položka**. Vyberte šablonu databáze SQL Server, přiřaďte jí název MoviesDB. mdf a klikněte na tlačítko **Přidat** (viz obrázek 1).

[![přidávání nové databáze SQL Server](creating-model-classes-with-linq-to-sql-vb/_static/image2.png)](creating-model-classes-with-linq-to-sql-vb/_static/image1.png)

**Obrázek 01**: Přidání nové databáze SQL Server ([kliknutím zobrazíte obrázek v plné velikosti](creating-model-classes-with-linq-to-sql-vb/_static/image3.png))

Po vytvoření nové databáze můžete databázi otevřít dvojitým kliknutím na soubor MoviesDB. mdf ve složce App\_data. Dvojím kliknutím na soubor MoviesDB. mdf se otevře okno Průzkumník serveru (viz obrázek 2).

|   | Okno Průzkumník serveru se nazývá okno Průzkumník databáze při použití aplikace Visual Web Developer. |
|---|----------------------------------------------------------------------------------------------------|
|   |                                                                                                    |

[![pomocí okna Průzkumník serveru](creating-model-classes-with-linq-to-sql-vb/_static/image5.png)](creating-model-classes-with-linq-to-sql-vb/_static/image4.png)

**Obrázek 02**: použití okna Průzkumník serveru ([obrázek pro celou velikost zobrazíte kliknutím](creating-model-classes-with-linq-to-sql-vb/_static/image6.png))

Musíme do naší databáze přidat jednu tabulku, která představuje naše filmy. Klikněte pravým tlačítkem na složku tabulky a vyberte možnost nabídky **Přidat novou tabulku**. Výběr této možnosti nabídky otevře Návrháře tabulky (viz obrázek 3).

[![pomocí okna Průzkumník serveru](creating-model-classes-with-linq-to-sql-vb/_static/image8.png)](creating-model-classes-with-linq-to-sql-vb/_static/image7.png)

**Obrázek 03**: Návrhář tabulky ([kliknutím zobrazíte obrázek v plné velikosti](creating-model-classes-with-linq-to-sql-vb/_static/image9.png))

Do tabulky databáze musíme přidat následující sloupce:

| **Název sloupce** | **Datový typ** | **Povoluje hodnoty null.** |
| --- | --- | --- |
| Id | Hmot | Nepravda |
| Název | Nvarchar (200) | Nepravda |
| Adresářů | nvarchar (50) | Nepravda |

Ve sloupci ID musíte udělat dvě speciální věci. Nejprve je třeba označit sloupec ID jako sloupec primárního klíče tak, že vyberete sloupec v Návrháři tabulky a kliknete na ikonu klíče. LINQ to SQL vyžaduje, abyste při vkládání nebo aktualizaci databáze určili sloupce primárního klíče.

Dále je nutné označit sloupec ID jako sloupec identity přiřazením hodnoty Ano k vlastnosti **identity identity** (viz obrázek 3). Sloupec identity je sloupec, který je automaticky přiřazen k novému číslu pokaždé, když do tabulky přidáte nový řádek dat.

Po provedení těchto změn tabulku uložte s názvem tblMovie. Tabulku můžete uložit kliknutím na tlačítko Uložit.

## <a name="create-linq-to-sql-classes"></a>Vytváření tříd LINQ to SQL

Náš model MVC bude obsahovat LINQ to SQL třídy, které reprezentují tabulku databáze tblMovie. Nejjednodušší způsob, jak vytvořit tyto LINQ to SQL třídy, je kliknout pravým tlačítkem myši na složku modely, vybrat položku **Přidat, nová položka**, vybrat šablonu LINQ to SQL třídy, přidělit třídy název Movie. dbml a kliknout na tlačítko **Přidat** (viz obrázek 4).

[![vytváření tříd LINQ to SQL](creating-model-classes-with-linq-to-sql-vb/_static/image11.png)](creating-model-classes-with-linq-to-sql-vb/_static/image10.png)

**Obrázek 04**: vytváření tříd LINQ to SQL ([kliknutím zobrazíte obrázek v plné velikosti](creating-model-classes-with-linq-to-sql-vb/_static/image12.png))

Ihned po vytvoření třídy video LINQ to SQL se zobrazí Návrhář relací objektů. Tabulky databáze můžete přetáhnout z okna Průzkumník serveru do Návrhář relací objektů a vytvořit LINQ to SQL třídy, které reprezentují konkrétní databázové tabulky. Na Návrhář relací objektů musíme přidat tabulku databáze tblMovie (viz obrázek 4).

[![používání Návrhář relací objektů](creating-model-classes-with-linq-to-sql-vb/_static/image14.png)](creating-model-classes-with-linq-to-sql-vb/_static/image13.png)

**Obrázek 05**: použití Návrhář relací objektů ([kliknutím zobrazíte obrázek v plné velikosti](creating-model-classes-with-linq-to-sql-vb/_static/image15.png))

Ve výchozím nastavení Návrhář relací objektů vytvoří třídu se stejným názvem, jako má databázová tabulka, kterou jste přetáhli do návrháře. Nechce ale volat naši třídu tblMovie. Proto klikněte v návrháři na název třídy a změňte název třídy na video.

Nakonec nezapomeňte kliknout na tlačítko **Uložit** (Obrázek diskety) a uložit LINQ to SQL třídy. V opačném případě LINQ to SQL třídy nebudou vygenerovány Návrhář relací objektů.

## <a name="using-linq-to-sql-in-a-controller-action"></a>Použití LINQ to SQL v akci kontroleru

Teď, když máme naše LINQ to SQL třídy, můžeme tyto třídy použít k načtení dat z databáze. V této části se dozvíte, jak použít třídy LINQ to SQL přímo v rámci akce kontroleru. Zobrazí se seznam filmů z tabulky tblMovies Database v zobrazení MVC.

Nejdřív je potřeba upravit třídu HomeController. Tuto třídu lze najít ve složce Controllers aplikace. Upravte třídu tak, aby vypadala jako třída v seznamu 1.

**Výpis 1 – `Controllers\HomeController.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample1.vb)]

Akce index () v výpisu 1 používá třídu LINQ to SQL DataContext (MovieDataContext), která představuje databázi MoviesDB. Třída MoveDataContext byla vygenerována Návrhář relací objektů sady Visual Studio.

Dotaz LINQ se provede proti kontextu DataContext, aby se načetly všechny filmy z tabulky databáze tblMovies. Seznam filmů je přiřazen místní proměnné s názvem filmy. Nakonec se seznam filmů předává do zobrazení prostřednictvím zobrazení dat.

Aby se zobrazovaly filmy, dál je potřeba upravit zobrazení indexu. Zobrazení indexu můžete najít ve složce Views\Home\. Aktualizujte zobrazení indexu tak, aby vypadalo jako zobrazení v seznamu 2.

**Výpis 2 – `Views\Home\Index.aspx`**

[!code-aspx[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample2.aspx)]

Všimněte si, že upravené zobrazení indexu obsahuje direktivu &lt;% @ import oboru názvů&gt; v horní části zobrazení. Tato direktiva importuje obor názvů MvcApplication1. Tento obor názvů potřebujeme, aby bylo možné pracovat s třídami modelů – zejména se třídou filmu v zobrazení.

Zobrazení v seznamu 2 obsahuje pro každou smyčku, která prochází všemi položkami reprezentovanými vlastností ViewData. model. Hodnota vlastnosti title se zobrazí pro každý film.

Všimněte si, že hodnota vlastnosti ViewData. model je přetypování na IEnumerable. To je nezbytné, aby bylo možné projít obsah ViewData. model. Další možností je vytvořit zobrazení silného typu. Když vytvoříte zobrazení silného typu, převedete vlastnost ViewData. model na konkrétní typ v rámci třídy zobrazení kódu na pozadí.

Pokud aplikaci spustíte po úpravě třídy HomeController a zobrazení indexu, zobrazí se prázdná stránka. Zobrazí se prázdná stránka, protože v tabulce databáze tblMovies nejsou žádné filmové záznamy.

Chcete-li přidat záznamy do tabulky databáze tblMovies, klikněte pravým tlačítkem myši na tabulku databáze tblMovies v okně Průzkumník serveru (okno Průzkumník databáze v aplikaci Visual Web Developer) a vyberte možnost nabídky **Zobrazit data tabulky**. Záznamy filmů můžete vložit pomocí mřížky, která se zobrazí (viz obrázek 5).

[![vkládání filmů](creating-model-classes-with-linq-to-sql-vb/_static/image17.png)](creating-model-classes-with-linq-to-sql-vb/_static/image16.png)

**Obrázek 6**: vkládání filmů ([kliknutím zobrazíte obrázek v plné velikosti](creating-model-classes-with-linq-to-sql-vb/_static/image18.png))

Po přidání záznamů databáze do tabulky tblMovies a spuštění aplikace uvidíte stránku na obrázku 7. Všechny záznamy z filmové databáze se zobrazí v seznamu s odrážkami.

[![zobrazení filmů pomocí zobrazení indexu](creating-model-classes-with-linq-to-sql-vb/_static/image20.png)](creating-model-classes-with-linq-to-sql-vb/_static/image19.png)

**Obrázek 07**: zobrazení filmů pomocí zobrazení indexu ([kliknutím zobrazíte obrázek v plné velikosti](creating-model-classes-with-linq-to-sql-vb/_static/image21.png))

## <a name="using-the-repository-pattern"></a>Použití vzoru úložiště

V předchozí části jsme použili LINQ to SQL třídy přímo v rámci akce kontroleru. Třídu MovieDataContext jsme použili přímo z akce řadiče indexu (). V případě jednoduché aplikace není v tomto případě nic špatné. Ale práce přímo s LINQ to SQL v třídě Controller vytvoří problémy, když potřebujete vytvořit složitější aplikaci.

Použití LINQ to SQL v rámci třídy Controller ztěžuje přepínání technologií pro přístup k datům v budoucnu. Například se můžete rozhodnout, že budete používat Microsoft LINQ to SQL k používání Microsoft Entity Framework jako technologie pro přístup k datům. V takovém případě byste museli přepsat každý kontroler, který přistupuje k databázi v rámci aplikace.

Použití LINQ to SQL v rámci třídy Controller také ztěžuje vytváření testů jednotek pro vaši aplikaci. V normálním případě nechcete při provádění testů jednotek pracovat s databází. Chcete použít testy jednotek k otestování logiky aplikace a nikoli databázového serveru.

Aby bylo možné vytvořit aplikaci MVC, která je více přizpůsobitelná na budoucí změnu a kterou lze snadněji testovat, měli byste zvážit použití vzoru úložiště. Při použití vzoru úložiště vytvoříte samostatnou třídu úložiště, která bude obsahovat veškerou logiku přístupu k databázi.

Při vytváření třídy úložiště vytvoříte rozhraní, které představuje všechny metody používané třídou úložiště. V rámci řadičů napíšete kód pro rozhraní místo úložiště. Tímto způsobem můžete v budoucnu implementovat úložiště pomocí různých technologií pro přístup k datům.

Rozhraní v seznamu 3 má název IMovieRepository a představuje jednu metodu s názvem ListAll ().

**Výpis 3 – `Models\IMovieRepository.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample3.vb)]

Třída úložiště v výpisu 4 implementuje rozhraní IMovieRepository. Všimněte si, že obsahuje metodu s názvem ListAll (), která odpovídá metodě vyžadované rozhraním IMovieRepository.

**Výpis 4 – `Models\MovieRepository.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample4.vb)]

Nakonec třída MoviesController v seznamu 5 používá vzor úložiště. Již nepoužívá LINQ to SQL třídy přímo.

**Výpis 5 – `Controllers\MoviesController.vb`**

[!code-vb[Main](creating-model-classes-with-linq-to-sql-vb/samples/sample5.vb)]

Všimněte si, že třída MoviesController v seznamu 5 má dva konstruktory. První konstruktor, konstruktor bez parametrů, je volána, když je aplikace spuštěna. Tento konstruktor vytvoří instanci třídy MovieRepository a předá ji druhému konstruktoru.

Druhý konstruktor má jeden parametr: parametr IMovieRepository. Tento konstruktor jednoduše přiřadí hodnotu parametru poli na úrovni třídy s názvem \_úložiště.

Třída MoviesController využívá vzor návrhu softwaru, který se nazývá vzor vkládání závislostí. Konkrétně používá něco s názvem vkládání závislostí konstruktoru. Další informace o tomto vzoru si můžete přečíst v následujícím článku: Martin Fowlera:

[http://martinfowler.com/articles/injection.html](http://martinfowler.com/articles/injection.html)

Všimněte si, že veškerý kód ve třídě MoviesController (s výjimkou prvního konstruktoru) spolupracuje s rozhraním IMovieRepository namísto skutečné třídy MovieRepository. Kód komunikuje s abstraktním rozhraním namísto konkrétní implementace rozhraní.

Chcete-li upravit technologii pro přístup k datům, kterou používá aplikace, můžete jednoduše implementovat rozhraní IMovieRepository se třídou, která používá jinou technologii přístupu k databázi. Můžete například vytvořit třídu EntityFrameworkMovieRepository nebo třídu SubSonicMovieRepository. Vzhledem k tomu, že třída Controller je naprogramována na rozhraní, můžete předat novou implementaci IMovieRepository do třídy kontroleru a třída bude i nadále fungovat.

Kromě toho, pokud chcete otestovat třídu MoviesController, můžete předat falešné třídy úložiště filmu do MoviesController. Můžete implementovat třídu IMovieRepository s třídou, která nemá ve skutečnosti přístup k databázi, ale obsahuje všechny požadované metody rozhraní IMovieRepository. Tímto způsobem můžete jednotkové testování třídy MoviesController bez skutečného přístupu ke skutečné databázi.

## <a name="summary"></a>Přehled

Cílem tohoto kurzu je předvést, jak můžete vytvořit třídy modelu MVC s využitím Microsoft LINQ to SQL. Prozkoumali jsme dvě strategie pro zobrazení databázových dat v aplikaci ASP.NET MVC. Nejprve jsme vytvořili třídy LINQ to SQL a použili třídy přímo v rámci akce kontroleru. Použití tříd LINQ to SQL v rámci kontroleru umožňuje rychle a snadno zobrazit databázová data v aplikaci MVC.

V dalším kroku jsme prozkoumali trochu obtížnější, ale s omezenou další virtuousou cestu k zobrazování databázových dat. Využili jsme výhod vzoru úložiště a umístili jsme veškerou logiku přístupu k databázím do samostatné třídy úložiště. V našem řadiči jsme napsali veškerý náš kód na rozhraní místo konkrétní třídy. Výhodou vzoru úložiště je, že nám umožňuje snadno měnit technologie přístupu k databázím v budoucnu a umožňuje nám snadno testovat naše třídy kontroleru.

> [!div class="step-by-step"]
> [Předchozí](creating-model-classes-with-the-entity-framework-vb.md)
> [Další](displaying-a-table-of-database-data-vb.md)

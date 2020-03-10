---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
title: '4\. část: modely a přístup k datům | Microsoft Docs'
author: jongalloway
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 4 pokrývá modely a přístup k datům.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: ab55ca81-ab9b-44a0-8700-dc6da2599335
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
msc.type: authoredcontent
ms.openlocfilehash: 402be340f1ea3344675e7b859cea8c5130cfc8ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559673"
---
# <a name="part-4-models-and-data-access"></a>4\. část: Modely a přístup k datům

o [Jan Galloway](https://github.com/jongalloway)

> Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio pro vývoj webů.  
>   
> Úložiště hudby MVC je zjednodušená ukázka implementace úložiště, která prodává hudební alba online a implementuje základní funkce pro správu webů, přihlašování uživatelů a nákupních košíků.
> 
> V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 4 pokrývá modely a přístup k datům.

Zatím jsme právě předali "" fiktivní data "z našich řadičů do našich šablon zobrazení. Teď jsme připraveni připojit skutečnou databázi. V tomto kurzu pokryjeme, jak používat edici SQL Server Compact (často označovanou jako SQL CE) jako náš databázový stroj. SQL CE je bezplatná, vložená databáze založená na souborech, která nevyžaduje žádnou instalaci nebo konfiguraci, což usnadňuje místní vývoj.

## <a name="database-access-with-entity-framework-code-first"></a>Přístup k databázi pomocí Entity Frameworkho kódu – první

K dotazování a aktualizaci databáze budeme používat podporu Entity Framework (EF), která je obsažená v projektech ASP.NET MVC 3. EF je flexibilní rozhraní API pro mapování relačních objektů (ORM), které umožňuje vývojářům dotazovat a aktualizovat data uložená v databázi v objektově orientovaném způsobem.

Entity Framework verze 4 podporuje vývojové paradigma s názvem Code-First. Code – First umožňuje vytvořit objekt modelu zápisem jednoduchých tříd (označovaných také jako POCO z objektů CLR "v prostém formátu") a může dokonce vytvořit databázi průběžně z vašich tříd.

### <a name="changes-to-our-model-classes"></a>Změny v našich třídách modelu

Využijeme funkci vytváření databáze v Entity Framework v tomto kurzu. Předtím, než to provedeme, provedeme několik menších změn našich tříd modelů, které se dají přidat do některých věcí, které použijeme později.

#### <a name="adding-the-artist-model-classes"></a>Přidání tříd interpretů

Naše alba budou přidružena k umělcům, takže přidáme jednoduchou třídu modelu pro popis interpreta. Do složky modely s názvem Artist.cs přidejte novou třídu pomocí kódu uvedeného níže.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample1.cs)]

#### <a name="updating-our-model-classes"></a>Aktualizují se třídy modelů

Aktualizujte třídu alba, jak je znázorněno níže.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample2.cs)]

Dále proveďte následující aktualizace třídy žánru.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample3.cs)]

### <a name="adding-the-app_data-folder"></a>Přidání složky s\_dat aplikace

Do našeho projektu přidáme aplikaci\_datový adresář, abychom mohli uchovávat soubory databáze SQL Server Express. Data\_aplikace jsou speciální adresář v ASP.NET, který už má správná oprávnění zabezpečení přístupu pro přístup k databázi. V nabídce projekt vyberte Přidat složku ASP.NET a pak aplikace\_data.

![](mvc-music-store-part-4/_static/image1.png)

### <a name="creating-a-connection-string-in-the-webconfig-file"></a>Vytvoření připojovacího řetězce v souboru Web. config

Do konfiguračního souboru webu přidáme pár řádků, aby Entity Framework vědět, jak se připojit k naší databázi. Dvakrát klikněte na soubor Web. config umístěný v kořenovém adresáři projektu.

![](mvc-music-store-part-4/_static/image2.png)

Posuňte se k dolnímu okraji tohoto souboru a přidejte &lt;connectionStrings&gt; sekci přímo nad poslední řádek, jak je znázorněno níže.

[!code-xml[Main](mvc-music-store-part-4/samples/sample4.xml)]

### <a name="adding-a-context-class"></a>Přidání třídy kontextu

Klikněte pravým tlačítkem na složku modely a přidejte novou třídu s názvem MusicStoreEntities.cs.

![](mvc-music-store-part-4/_static/image3.png)

Tato třída bude představovat kontext databáze Entity Framework a bude zpracovávat naše operace vytvoření, čtení, aktualizace a odstranění pro nás. Kód pro tuto třídu je uveden níže.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample5.cs)]

To je to – neexistuje žádná další konfigurace, speciální rozhraní atd. Rozšířením základní třídy DbContext je naše třída MusicStoreEntities schopna zpracovat naše databázové operace pro nás. Teď, když jsme se připojili, můžeme přidat několik dalších vlastností do našich tříd modelů a využít tak některé z dalších informací v naší databázi.

### <a name="adding-our-store-catalog-data"></a>Přidávají se naše data katalogu Storu.

Budeme využívat funkci Entity Framework, která přidá "počáteční" data do nově vytvořené databáze. Tím se předem naplní náš katalog Storu seznamem žánrů, umělců a alb. Stažení MvcMusicStore-Assets. zip – které zahrnovalo naše soubory návrhu webu použité dříve v tomto kurzu – obsahuje soubor třídy s těmito počátečními daty, který je umístěný ve složce s názvem Code.

Ve složce Code/modely vyhledejte soubor SampleData.cs a umístěte jej do složky modely v našem projektu, jak je znázorněno níže.

![](mvc-music-store-part-4/_static/image4.png)

Nyní musíme přidat jeden řádek kódu, který sděluje Entity Framework o této třídě SampleData. Dvojím kliknutím na soubor Global. asax v kořenovém adresáři projektu jej otevřete a přidejte následující řádek do horní části aplikace\_spustit metodu.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample6.cs)]

V tomto okamžiku dokončili jsme práci nutnou ke konfiguraci Entity Framework pro náš projekt.

## <a name="querying-the-database"></a>Dotazy do databáze

Teď aktualizujeme naše StoreController tak, aby místo použití "fiktivních dat" místo toho volaly do naší databáze dotaz na všechny informace. Zahájíme deklarováním pole v **StoreController** k uložení instance třídy MusicStoreEntities s názvem storeDB:

[!code-csharp[Main](mvc-music-store-part-4/samples/sample7.cs)]

### <a name="updating-the-store-index-to-query-the-database"></a>Aktualizace indexu úložiště pro dotazování databáze

Třída MusicStoreEntities je udržována Entity Framework a zpřístupňuje vlastnost kolekce pro každou tabulku v naší databázi. Pojďme aktualizovat naši akci indexu StoreController a načíst všechny žánry v naší databázi. Dříve jsme to provedli pomocí pevného kódování řetězcových dat. Místo toho můžeme pouze Entity Framework použít Generesou kontextovou kolekci:

[!code-csharp[Main](mvc-music-store-part-4/samples/sample8.cs)]

Od naší šablony zobrazení se nemusí provádět žádné změny, protože pořád vracíme stejné StoreIndexViewModel, jako jsme vrátili data z naší databáze hned teď!

Když znovu spustíte projekt a navštívíte adresu URL "/Store", zobrazí se teď seznam všech žánrů v naší databázi:

![](mvc-music-store-part-4/_static/image1.jpg)

### <a name="updating-store-browse-and-details-to-use-live-data"></a>Aktualizace procházení a podrobností Storu pro použití živých dat

Pomocí metody Action/Store/Browse? Žánr = *[subžánr]* hledáme Žánr podle názvu. Očekáváme jenom jeden výsledek, protože by nikdy neměl mít dvě položky pro stejný název žánru, a proto můžeme použít. Rozšíření Single () v LINQ pro dotaz na příslušný objekt žánru (ještě nepište):

[!code-csharp[Main](mvc-music-store-part-4/samples/sample9.cs)]

Jediná metoda přijímá výraz lambda jako parametr, který určuje, že chceme, aby měl jeden objekt žánru tak, aby jeho název odpovídal hodnotě, kterou jsme definovali. V výše uvedeném případě načítáme jeden objekt žánru s hodnotou názvu, která odpovídá discích.

Využijeme funkci Entity Framework, která nám umožní označit další související entity, které chceme načíst, i když se objekt žánru načte. Tato funkce se nazývá tvarování výsledků dotazů a umožňuje snížit počet pokusů, které potřebujeme pro přístup k databázi, aby se načetly všechny informace, které potřebujeme. Chceme předběžně načíst alba pro žánry, které načteme, abychom aktualizovali náš dotaz tak, aby se zahrnul ze žánrů. zahrňte ("alba"), abyste označili, že máme také související alba. To je efektivnější, protože načte data žánru i alba v jediné žádosti databáze.

Tady je vysvětlení, jak vypadá naše aktualizovaná akce kontroleru procházení:

[!code-csharp[Main](mvc-music-store-part-4/samples/sample10.cs)]

Teď můžeme aktualizovat zobrazení pro procházení Storu, aby se zobrazila alba, která jsou k dispozici v jednotlivých žánrech. Otevřete šablonu zobrazení (najdete v/Views/Store/Browse.cshtml) a přidejte seznam alb s odrážkami, jak je znázorněno níže.

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample11.cshtml)]

Po spuštění naší aplikace a přechodu na/Store/Browse? Žánr = Jazz vidíte, že se výsledky z databáze teď shromažďují a zobrazují se všechna alba v našem vybraném žánru.

![](mvc-music-store-part-4/_static/image2.jpg)

Provedeme stejnou změnu na naši adresu URL/Store/Details/[ID] a nahradíme naše fiktivní data databázovým dotazem, který načte album, jehož ID odpovídá hodnotě parametru.

[!code-csharp[Main](mvc-music-store-part-4/samples/sample12.cs)]

Spuštění naší aplikace a procházení na/Store/Details/1 ukazuje, že se z databáze teď shromažďují výsledky.

![](mvc-music-store-part-4/_static/image5.png)

Teď, když je naše stránka s podrobnostmi o Storu nastavená tak, aby zobrazovala album podle ID alba, pojďme aktualizovat zobrazení pro **procházení** a propojit zobrazení podrobností. Použijeme HTML. ActionLink, přesně tak, jak jsme přešli na odkaz z indexu úložiště k uložení na konci předchozí části. Níže se zobrazí úplný zdroj zobrazení pro procházení.

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample13.cshtml)]

Teď jsme schopni přejít ze stránky pro Store na stránku žánru, která obsahuje seznam dostupných alb a kliknutím na album si můžete zobrazit podrobnosti o tomto albu.

![](mvc-music-store-part-4/_static/image6.png)

> [!div class="step-by-step"]
> [Předchozí](mvc-music-store-part-3.md)
> [Další](mvc-music-store-part-5.md)

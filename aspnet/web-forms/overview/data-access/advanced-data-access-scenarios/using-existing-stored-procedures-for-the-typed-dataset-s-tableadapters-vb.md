---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
title: Použití existujících uložených procedur pro objekty TableAdapter typované datové sady (VB) | Microsoft Docs
author: rick-anderson
description: V předchozím kurzu jsme zjistili, jak pomocí Průvodce TableAdapter vygenerovat nové uložené procedury. V tomto kurzu se naučíme, jak stejné TableAdapter...
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 2da25f6a-757e-4e7b-a812-1575288d8f7a
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
msc.type: authoredcontent
ms.openlocfilehash: e35c3d6a98516a07f6119e6cb9dbeb99bc28fe33
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78531799"
---
# <a name="using-existing-stored-procedures-for-the-typed-datasets-tableadapters-vb"></a>Použití stávajících uložených procedur komponentami TableAdapter typových sad dat (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_68_VB.zip) nebo [stažení PDF](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/datatutorial68vb1.pdf)

> V předchozím kurzu jsme zjistili, jak pomocí Průvodce TableAdapter vygenerovat nové uložené procedury. V tomto kurzu se dozvíte, jak může stejný Průvodce TableAdapter pracovat se stávajícími uloženými procedurami. Také se dozvíte, jak ručně přidat nové uložené procedury do naší databáze.

## <a name="introduction"></a>Úvod

V [předchozím kurzu](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) jsme viděli, jak může být zadaná datová sada s objekty TableAdapter nakonfigurovaná tak, aby používala uložené procedury pro přístup k datům, nikoli k příkazům SQL ad hoc. Zejména jsme prozkoumali, jak má Průvodce TableAdapter automaticky vytvořit tyto uložené procedury. Při přenosu starší verze aplikace do ASP.NET 2,0 nebo při sestavování webu ASP.NET 2,0 kolem existujícího datového modelu je pravděpodobné, že databáze již obsahuje uložené procedury, které potřebujeme. Alternativně můžete chtít vytvořit uložené procedury ručně nebo pomocí jiného nástroje než Průvodce TableAdapter, který automaticky vygeneruje vaše uložené procedury.

V tomto kurzu se podíváme na to, jak nakonfigurovat TableAdapter na použití existujících uložených procedur. Vzhledem k tomu, že databáze Northwind má pouze malou sadu vestavěných uložených procedur, podíváme se také na kroky potřebné k ručnímu přidání nových uložených procedur do databáze prostřednictvím prostředí sady Visual Studio. Pojďme začít!

> [!NOTE]
> V rámci kurzových [úprav v rámci transakce](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) jsme do TableAdapter přidali metody pro podporu transakcí (`BeginTransaction`, `CommitTransaction`a tak dále). Transakce lze případně spravovat zcela v rámci uložené procedury, která nevyžaduje žádné úpravy kódu vrstvy přístupu k datům. V tomto kurzu prozkoumáme příkazy T-SQL, které se použijí ke spuštění příkazů uložené procedury s v rámci rozsahu transakce.

## <a name="step-1-adding-stored-procedures-to-the-northwind-database"></a>Krok 1: Přidání uložených procedur do databáze Northwind

Visual Studio usnadňuje přidání nových uložených procedur do databáze. Přidáme do databáze Northwind novou uloženou proceduru, která vrátí všechny sloupce z `Products` tabulky pro ty, které mají určitou hodnotu `CategoryID`. V okně Průzkumník serveru rozbalte databázi Northwind, aby se zobrazily její složky – diagramy databáze, tabulky, zobrazení a tak dále. Jak jsme viděli v předchozím kurzu, složka uložené procedury obsahuje databázi s existujícími uloženými procedurami. Chcete-li přidat novou uloženou proceduru, jednoduše klikněte pravým tlačítkem myši na složku uložené procedury a v místní nabídce vyberte možnost Přidat novou uloženou proceduru.

[![klikněte pravým tlačítkem na složku uložené procedury a přidejte novou uloženou proceduru.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image2.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image1.png)

**Obrázek 1**: klikněte pravým tlačítkem na složku uložené procedury a přidejte novou uloženou proceduru ([kliknutím zobrazíte obrázek v plné velikosti).](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image3.png)

Jak ukazuje obrázek 1, výběrem možnosti Přidat novou uloženou proceduru se otevře okno skriptu v aplikaci Visual Studio s osnovou SQL skriptu potřebného k vytvoření uložené procedury. Tato úloha se dá využít k uložení tohoto skriptu a jeho provedení. v takovém případě bude uložená procedura přidána do databáze.

Zadejte následující skript:

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample1.sql)]

Když se tento skript spustí, přidá se do databáze Northwind s názvem `Products_SelectByCategoryID`nová uložená procedura. Tato uložená procedura přijímá jeden vstupní parametr (`@CategoryID`typu `int`) a vrací všechna pole pro tyto produkty s hodnotou odpovídajícího `CategoryID`.

Chcete-li spustit tento skript `CREATE PROCEDURE` a přidat uloženou proceduru do databáze, klikněte na panelu nástrojů na ikonu Uložit nebo stiskněte klávesu CTRL + S. Po takovém případě se složka uložených procedur aktualizuje a zobrazí nově vytvořenou uloženou proceduru. Také se skript v okně změní Subtlety z `CREATE PROCEDURE dbo.Products_SelectProductByCategoryID` na `ALTER PROCEDURE` `dbo.Products_SelectProductByCategoryID`. `CREATE PROCEDURE` do databáze přidá novou uloženou proceduru, zatímco `ALTER PROCEDURE` aktualizuje stávající. Vzhledem k tomu, že se začátek skriptu změnil na `ALTER PROCEDURE`, změna vstupních parametrů uložených procedur nebo příkazů SQL a kliknutí na ikonu Uložit aktualizuje uloženou proceduru těmito změnami.

Obrázek 2 ukazuje Visual Studio po uložení uložené procedury `Products_SelectByCategoryID`.

[![se uložená procedura Products_SelectByCategoryID přidala do databáze.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image5.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image4.png)

**Obrázek 2**: uložená procedura `Products_SelectByCategoryID` byla přidána do databáze ([kliknutím zobrazíte obrázek v plné velikosti).](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image6.png)

## <a name="step-2-configuring-the-tableadapter-to-use-an-existing-stored-procedure"></a>Krok 2: Konfigurace TableAdapter pro použití existující uložené procedury

Teď, když se do databáze přidala uložená procedura `Products_SelectByCategoryID`, můžeme nakonfigurovat vrstvu přístupu k datům, aby používala tuto uloženou proceduru, když je vyvolána jedna z jejích metod. Konkrétně přidáme metodu `GetProductsByCategoryID(<_i22_>categoryID)<!--_i22_-->` do `ProductsTableAdapter` v datové sadě `NorthwindWithSprocs` typu, která volá `Products_SelectByCategoryID` uloženou proceduru, kterou jsme právě vytvořili.

Začněte tím, že otevřete `NorthwindWithSprocs` datovou sadu. Klikněte pravým tlačítkem na `ProductsTableAdapter` a výběrem možnosti Přidat dotaz spusťte Průvodce konfigurací dotazu TableAdapter. V [předchozím kurzu](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) jsme se rozhodli, že TableAdapter vytvoří novou uloženou proceduru pro nás. Pro tento kurz ale chceme, aby se nová metoda TableAdapter nacházela na stávající uloženou proceduru `Products_SelectByCategoryID`. Proto v prvním kroku průvodce použijte možnost použít existující uloženou proceduru a potom klikněte na tlačítko Další.

[![zvolit možnost použít existující uloženou proceduru](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image8.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image7.png)

**Obrázek 3**: vyberte možnost použít existující uloženou proceduru ([kliknutím zobrazíte obrázek v plné velikosti).](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image9.png)

Následující obrazovka nabízí rozevírací seznam naplněný uloženými procedurami databáze. Výběr uložené procedury vypíše vstupní parametry na levé straně a datová pole, která se vrátí (pokud existují) na pravé straně. V seznamu vyberte uloženou proceduru `Products_SelectByCategoryID` a klikněte na další.

[![vybrat uloženou proceduru Products_SelectByCategoryID](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image11.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image10.png)

**Obrázek 4**: vyberte uloženou proceduru `Products_SelectByCategoryID` ([kliknutím zobrazíte obrázek v plné velikosti](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image12.png)).

Na další obrazovce se zobrazí informace o tom, jaký druh dat je vrácen uloženou procedurou, a naše odpověď zde určuje typ vrácený metodou TableAdapter s. Například pokud oznamujeme, že se vrátí tabulková data, metoda vrátí instanci `ProductsDataTable` naplněnou záznamy vrácenými uloženou procedurou. Naproti tomu, pokud oznamujeme, že tato uložená procedura vrátí jedinou hodnotu, `Object` TableAdapter vrátí hodnotu, která je přiřazena k hodnotě v prvním sloupci prvního záznamu vráceného uloženou procedurou.

Vzhledem k tomu, že `Products_SelectByCategoryID` uložená procedura vrátí všechny produkty patřící do konkrétní kategorie, vyberte první data v tabulkovém typu odpovědi a klikněte na další.

[![označují, že uložená procedura vrátí tabulková data](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image14.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image13.png)

**Obrázek 5**: označení, že uložená procedura vrátí tabulková data ([kliknutím zobrazíte obrázek v plné velikosti](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image15.png))

To vše zůstává, chcete-li určit, jaké vzory metod použít a které jsou následovány názvy těchto metod. Ponechte naplnit DataTable a vraťte možnosti DataTable, ale přejmenujte metody na `FillByCategoryID` a `GetProductsByCategoryID`. Pak klikněte na další a zkontrolujte souhrnné úkoly, které průvodce provede. Pokud vše vypadá správně, klikněte na Dokončit.

[![pojmenovat metody FillByCategoryID a GetProductsByCategoryID](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image17.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image16.png)

**Obrázek 6**: pojmenování metod `FillByCategoryID` a `GetProductsByCategoryID` ([kliknutím zobrazíte obrázek v plné velikosti](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image18.png))

> [!NOTE]
> Metody TableAdapter, které jsme právě vytvořili, `FillByCategoryID` a `GetProductsByCategoryID`, očekávají vstupní parametr typu `Integer`. Tato hodnota vstupního parametru se předává do uložené procedury prostřednictvím parametru `@CategoryID`. Pokud změníte `Products_SelectByCategory` uložené procedury s parametry, budete muset také aktualizovat parametry těchto metod TableAdapter. Jak je popsáno v [předchozím kurzu](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md), lze to provést jedním ze dvou způsobů: ručním přidáním nebo odebráním parametrů z kolekce Parameters nebo spuštěním Průvodce TableAdapter.

## <a name="step-3-adding-agetproductsbycategoryidcategoryidmethod-to-the-bll"></a>Krok 3: Přidání metody`GetProductsByCategoryID(categoryID)`do knihoven BLL

Po dokončení metody `GetProductsByCategoryID` DAL je dalším krokem poskytnutí přístupu k této metodě ve vrstvě obchodní logiky. Otevřete soubor `ProductsBLLWithSprocs` třídy a přidejte následující metodu:

[!code-vb[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample2.vb)]

Tato metoda knihoven BLL jednoduše vrátí `ProductsDataTable` vrácenou metodou `ProductsTableAdapter` s `GetProductsByCategoryID`. Atribut `DataObjectMethodAttribute` poskytuje metadata používaná průvodcem zdroj dat v prvku ObjectDataSource s konfigurací. Konkrétně se tato metoda zobrazí v rozevíracím seznamu vybrat kartu s.

## <a name="step-4-displaying-products-by-category"></a>Krok 4: zobrazení produktů podle kategorií

Chcete-li otestovat nově přidanou `Products_SelectByCategoryID` uloženou proceduru a odpovídající metody DAL a knihoven BLL, vytvoříme stránku ASP.NET, která obsahuje DropDownList a GridView. DropDownList zobrazí seznam všech kategorií v databázi, zatímco v prvku GridView se zobrazí produkty patřící do vybrané kategorie.

> [!NOTE]
> V předchozích kurzech jsme vytvořili rozhraní hlavní/podrobnosti pomocí ovládacích prvků DropDownList. Podrobnější pohled na implementaci takové sestavy hlavní/podrobnosti najdete v kurzu zobrazení [hlavního/podrobného filtru pomocí DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-vb.md) .

Otevřete stránku `ExistingSprocs.aspx` ve složce `AdvancedDAL` a přetáhněte DropDownList z panelu nástrojů na Návrhář. Nastavte vlastnost `ID` DropDownList s na `Categories` a její vlastnost `AutoPostBack` na `True`. Dále z jeho inteligentní značky vytvořte objekt DropDownList s novým prvkem ObjectDataSource s názvem `CategoriesDataSource`. Nakonfigurujte prvek ObjectDataSource tak, aby načítají jeho data z metody `CategoriesBLL` třídy s `GetCategories`. Nastavte rozevírací seznamy na kartách aktualizace, vložení a odstranění na (žádné).

[![načíst data z metody CategoriesBLL třídy s GetCategories](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image20.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image19.png)

**Obrázek 7**: načtení dat z metody `GetCategories` `CategoriesBLL` třídy s ([kliknutím zobrazíte obrázek v plné velikosti](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image21.png))

[![nastavení rozevíracích seznamů na kartách aktualizace, vložení a odstranění na (žádné)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image23.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image22.png)

**Obrázek 8**: nastavení rozevíracích seznamů na kartách aktualizace, vložení a odstranění na (žádné) ([kliknutím zobrazíte obrázek v plné velikosti](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image24.png))

Po dokončení průvodce ObjectDataSource nakonfigurujte DropDownList tak, aby zobrazilo pole `CategoryName` dat a `CategoryID` pole jako `Value` pro každý `ListItem`.

V tomto okamžiku by deklarativní označení DropDownList a ObjectDataSource s mělo vypadat podobně jako následující:

[!code-aspx[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample3.aspx)]

Dále přetáhněte prvek GridView do návrháře a umístěte jej pod ovládací prvek DropDownList. Nastavte `ID` prvku GridView s `ProductsByCategory` a ze své inteligentní značky jej navažte na nový prvek ObjectDataSource s názvem `ProductsByCategoryDataSource`. Nakonfigurujte `ProductsByCategoryDataSource` prvek ObjectDataSource pro použití `ProductsBLLWithSprocs` třídy, který získá data pomocí metody `GetProductsByCategoryID(categoryID)`. Vzhledem k tomu, že se tento prvek GridView použije jenom k zobrazení dat, nastavte rozevírací seznamy na kartách aktualizace, vložení a odstranění na (žádné) a klikněte na další.

[![nakonfigurovat prvek ObjectDataSource tak, aby používal třídu ProductsBLLWithSprocs](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image26.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image25.png)

**Obrázek 9**: Konfigurace prvku ObjectDataSource, aby používal třídu `ProductsBLLWithSprocs` ([kliknutím zobrazíte obrázek v plné velikosti](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image27.png))

[![načíst data z metody GetProductsByCategoryID (KódKategorie)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image29.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image28.png)

**Obrázek 10**: načtení dat z metody `GetProductsByCategoryID(categoryID)` ([kliknutím zobrazíte obrázek v plné velikosti](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image30.png))

Metoda zvolená na kartě vybrat očekává parametr, takže poslední krok průvodce vás vyzve k zadání zdroje parametru s. V rozevíracím seznamu zdroj parametrů nastavte ovládací prvek a vyberte ovládací prvek `Categories` v rozevíracím seznamu ControlID. Kliknutím na Dokončit dokončete průvodce.

[![použít kategorii DropDownList jako zdroj parametru KódKategorie](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image32.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image31.png)

**Obrázek 11**: jako zdroj parametru `categoryID` použijte `Categories` DropDownList ([kliknutím zobrazíte obrázek v plné velikosti](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image33.png)).

Po dokončení průvodce ObjectDataSource Visual Studio přidá BoundFields a třídě CheckBoxField podporována pro každé pole dat produktu. V takovém případě můžete tato pole přizpůsobit podle potřeby.

Navštivte stránku v prohlížeči. Při návštěvě stránky je vybrána kategorie nápoje a odpovídající produkty uvedené v mřížce. Změna rozevíracího seznamu na alternativní kategorii, jak ukazuje obrázek 12, způsobí postback a znovu načte mřížku s produkty nově vybrané kategorie.

[![se zobrazí produkty v kategorii plodiny.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image35.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image34.png)

**Obrázek 12**: zobrazí se produkty v kategorii plodiny ([kliknutím zobrazíte obrázek v plné velikosti](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image36.png)).

## <a name="step-5-wrapping-a-stored-procedure-s-statements-within-the-scope-of-a-transaction"></a>Krok 5: zabalení uložených procedur s příkazy v rámci oboru transakce

V rámci kurzových [úprav v rámci transakce](../working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb.md) jsme provedli postupy pro provádění řady příkazů pro úpravu databáze v rámci rozsahu transakce. Navrácení změn provedených v rámci zastřešující transakce buď úspěšně, nebo neúspěšných, s jistotou nedělitelnost Mezi techniky použití transakcí patří:

- Pomocí tříd v oboru názvů `System.Transactions`,
- Vrstva přístupu k datům používá třídy ADO.NET jako `SqlTransaction`a
- Přidání příkazů transakce T-SQL přímo do uložené procedury

V *rámci kurzu transakce zalamování změn databáze* byly použity třídy ADO.NET v dal. Zbývající část tohoto kurzu prověřuje způsob správy transakce pomocí příkazů T-SQL z uložené procedury.

Tři klíčové příkazy jazyka SQL pro ruční spuštění, potvrzení a vrácení transakce jsou `BEGIN TRANSACTION`, `COMMIT TRANSACTION`a `ROLLBACK TRANSACTION`v uvedeném pořadí. Podobně jako u přístupu ADO.NET potřebuje při použití transakcí z uložené procedury použít následující vzor:

1. Označuje začátek transakce.
2. Spusťte příkazy SQL, které tvoří transakci.
3. Pokud dojde k chybě v některém z příkazů z kroku 2, vraťte transakci zpět.
4. Pokud všechny příkazy z kroku 2 se dokončí bez chyby, potvrďte transakci.

Tento model může být implementován v syntaxi T-SQL pomocí následující šablony:

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample4.sql)]

Šablona začíná definováním `TRY...CATCH`ho bloku, konstrukce nového do SQL Server 2005. Podobně jako u `Try...Catch`ch bloků v Visual Basic spustí blok SQL `TRY...CATCH` příkazy v bloku `TRY`. Pokud některý příkaz vyvolá chybu, řízení je okamžitě převedeno na blok `CATCH`.

Pokud nedochází k žádným chybám, které provádějí příkazy SQL, které strukturu transakci, příkaz `COMMIT TRANSACTION` potvrdí změny a dokončí transakci. Pokud však jeden z příkazů způsobí chybu, `ROLLBACK TRANSACTION` v bloku `CATCH` vrátí databázi do stavu před zahájením transakce. Uložená procedura také vyvolá chybu pomocí [příkazu RAISERROR](https://msdn.microsoft.com/library/ms178592.aspx), který způsobí, že `SqlException` v aplikaci vyvolána.

> [!NOTE]
> Vzhledem k tomu, že je `TRY...CATCH` blok novinkou SQL Server 2005, nebude tato šablona fungovat, pokud používáte starší verze Microsoft SQL Server. Pokud nepoužíváte SQL Server 2005, prostudujte si část [Správa transakcí v SQL Server uložených procedurách](http://www.4guysfromrolla.com/webtech/080305-1.shtml) pro šablonu, která bude fungovat s jinými verzemi SQL Server.

Pojďme se podívat na konkrétní příklad. Mezi tabulkami `Categories` a `Products` existuje omezení cizího klíče, což znamená, že každé `CategoryID` pole v tabulce `Products` musí být namapováno na `CategoryID` hodnotu v tabulce `Categories`. Výsledkem jakékoli akce, která by porušila toto omezení, například pokus o odstranění kategorie s přidruženými produkty, má za následek porušení omezení cizího klíče. Pokud to chcete ověřit, přečtěte si příklad aktualizace a odstranění stávajících binárních dat v části práce s binárními daty (`~/BinaryData/UpdatingAndDeleting.aspx`). Tato stránka obsahuje všechny kategorie v systému spolu s tlačítky upravit a odstranit (viz obrázek 13), ale pokud se pokusíte odstranit kategorii, která má přidružené produkty, například nápoje – odstranění se nezdaří kvůli porušení omezení cizího klíče (viz obrázek 14).

[![se každá kategorie zobrazuje v prvku GridView s tlačítky upravit a odstranit](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image38.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image37.png)

**Obrázek 13**: Každá kategorie se zobrazuje v prvku GridView s tlačítky upravit a odstranit ([kliknutím zobrazíte obrázek v plné velikosti](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image39.png)).

[![nemůžete odstranit kategorii, která má existující produkty.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image41.png)](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image40.png)

**Obrázek 14**: nelze odstranit kategorii, která obsahuje existující produkty ([kliknutím zobrazíte obrázek v plné velikosti).](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image42.png)

Představte si, že ale chceme, aby se kategorie odstranily bez ohledu na to, jestli mají přidružené produkty. Pokud má být kategorie s produkty smazána, Představte si, že chceme také odstranit stávající produkty (i když další možností je jednoduše nastavit produkty `CategoryID` hodnoty na `NULL`). Tato funkce se dá implementovat pomocí pravidel kaskádového omezení cizího klíče. Alternativně můžeme vytvořit uloženou proceduru, která přijímá vstupní parametr `@CategoryID` a při vyvolání explicitně odstraní všechny přidružené produkty a pak zadanou kategorii.

Náš první pokus na takovou uloženou proceduru by mohl vypadat takto:

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample5.sql)]

I když se tím neodstraní přidružené produkty a kategorie, neudělá to v rámci transakce. Představte si, že je u `Categories` nějaké jiné omezení cizího klíče, které by bránilo odstranění konkrétní `@CategoryID` hodnoty. Problémem je to, že v takovém případě se před pokusem o odstranění kategorie odstraní všechny produkty. Čistý výsledek je takový, že pro takovou kategorii by tato uložená procedura odebrala všechny své produkty, zatímco tato kategorie stále obsahuje související záznamy v některé jiné tabulce.

Pokud byla uložená procedura zabalena v rámci rozsahu transakce, ale odstranění do `Products` tabulky by se vrátilo zpět na tvář neúspěšného odstranění při `Categories`. Následující skript uložených procedur používá transakci k zajištění nedělitelnost mezi dvěma příkazy `DELETE`:

[!code-sql[Main](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample6.sql)]

Chvíli přidejte `Categories_Delete` uloženou proceduru do databáze Northwind. Pokyny k přidání uložených procedur do databáze najdete v části zpět ke kroku 1.

## <a name="step-6-updating-thecategoriestableadapter"></a>Krok 6: aktualizace`CategoriesTableAdapter`

I když jsme do databáze přidali `Categories_Delete` uloženou proceduru, je DAL v současné době nakonfigurovaná k provedení odstranění pomocí ad hoc příkazů SQL. Musíme aktualizovat `CategoriesTableAdapter` a dát mu pokyn použít místo toho `Categories_Delete` uloženou proceduru.

> [!NOTE]
> Dříve v tomto kurzu jsme pracovali s `NorthwindWithSprocs` datovou sadou. Tato datová sada ale má jenom jednu entitu, `ProductsDataTable`a potřebujeme pracovat s kategoriemi. Proto ve zbývající části tohoto kurzu zjistíte, že se ve vrstvě pro přístup k datům I m odkazuje na `Northwind` datovou sadu, kterou jsme vytvořili poprvé v kurzu [Vytvoření vrstvy přístupu k datům](../introduction/creating-a-data-access-layer-vb.md) .

Otevřete datovou sadu Northwind, vyberte `CategoriesTableAdapter`a přejít na okno Vlastnosti. Okno Vlastnosti uvádí `InsertCommand`, `UpdateCommand`, `DeleteCommand`a `SelectCommand` používané v TableAdapter a také název a informace o připojení. Rozbalením vlastnosti `DeleteCommand` zobrazíte její podrobnosti. Jak ukazuje obrázek 15, vlastnost `DeleteCommand` s `CommandType` je nastavena na text, který dává pokyn k odeslání textu ve vlastnosti `CommandText` jako dotaz SQL ad-hoc.

![Vyberte CategoriesTableAdapter v návrháři, aby se zobrazily jeho vlastnosti v okně Vlastnosti.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image43.png)

**Obrázek 15**: vyberte `CategoriesTableAdapter` v návrháři, aby se zobrazily jeho vlastnosti v okně Vlastnosti.

Chcete-li změnit tato nastavení, vyberte v okno Vlastnosti text (DeleteCommand) a v rozevíracím seznamu zvolte možnost (nové). Tím se vymažou nastavení vlastností `CommandText`, `CommandType`a `Parameters`. V dalším kroku nastavte vlastnost `CommandType` na `StoredProcedure` a potom zadejte název uložené procedury pro `CommandText` (`dbo.Categories_Delete`). Pokud zadáte vlastnosti v tomto pořadí – nejdříve `CommandType` a potom `CommandText` – Visual Studio automaticky naplní kolekci Parameters. Pokud tyto vlastnosti v tomto pořadí nezadáte, budete muset ručně přidat parametry pomocí editoru kolekce Parameters. V obou případech je vhodné kliknout na tři tečky ve vlastnosti Parameters a vyvolat tak editor kolekce Parameters, aby bylo možné ověřit, zda byly provedeny správné změny nastavení parametrů (viz obrázek 16). Pokud v dialogovém okně nevidíte žádné parametry, přidejte parametr `@CategoryID` ručně (nemusíte `@RETURN_VALUE` parametr přidat).

![Ujistěte se, že je nastavení parametrů správné.](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image44.png)

**Obrázek 16**: Ujistěte se, že je nastavení parametrů správné.

Po aktualizaci DAL dojde k odstranění kategorie k automatickému odstranění všech přidružených produktů a k tomu v rámci transakce. Pokud to chcete ověřit, vraťte se na stránku aktualizace a odstranění stávajících binárních dat a klikněte na tlačítko Odstranit pro jednu z kategorií. Jedním kliknutím myši se odstraní kategorie a všechny její přidružené produkty.

> [!NOTE]
> Než otestujete `Categories_Delete` uloženou proceduru, která odstraní řadu produktů společně s vybranou kategorií, může být vhodné vytvořit záložní kopii vaší databáze. Pokud používáte databázi `NORTHWND.MDF` v `App_Data`, stačí zavřít aplikaci Visual Studio a zkopírovat soubory MDF a LDF v `App_Data` do jiné složky. Po otestování funkčnosti můžete databázi obnovit ukončením sady Visual Studio a nahrazením aktuálních souborů MDF a LDF v `App_Data` záložními kopiemi.

## <a name="summary"></a>Souhrn

I když Průvodce TableAdapterí automaticky vygeneruje uložené procedury pro nás, nastane čas, kdy je možné tyto uložené procedury už vytvořit nebo je chtít vytvořit ručně nebo pomocí jiných nástrojů. Pro uspokojení takových scénářů může být TableAdapter také nakonfigurován tak, aby odkazoval na stávající uloženou proceduru. V tomto kurzu jsme se vyhlédli do postupu ručního přidání uložených procedur do databáze prostřednictvím prostředí sady Visual Studio a způsobu, jak tyto uložené procedury nakabelovat metody TableAdapter s. Prozkoumali jsme také příkazy T-SQL a vzor skriptu, který se používá pro spouštění, potvrzování a vracení zpětných transakcí z uložené procedury.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Hilton Geisenow, S Ren Jacob Lauritsen a Teresa Murphy. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
> [Další](updating-the-tableadapter-to-use-joins-vb.md)

---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs
title: Implementace optimistického řízení souběžnosti (C#) | Microsoft Docs
author: rick-anderson
description: U webové aplikace, která umožňuje více uživatelům upravovat data, existuje riziko, že dva uživatelé mohou současně upravovat stejná data. V tomto tutori...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 56e15b33-93b8-43ad-8e19-44c6647ea05c
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs
msc.type: authoredcontent
ms.openlocfilehash: 3cddb0efd28249ffc5708ece39c80581d078a5a2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74617486"
---
# <a name="implementing-optimistic-concurrency-c"></a>Implementace optimistického řízení souběžnosti (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_21_CS.exe) nebo [Stáhnout PDF](implementing-optimistic-concurrency-cs/_static/datatutorial21cs1.pdf)

> U webové aplikace, která umožňuje více uživatelům upravovat data, existuje riziko, že dva uživatelé mohou současně upravovat stejná data. V tomto kurzu implementujeme optimistické řízení souběžnosti pro zpracování tohoto rizika.

## <a name="introduction"></a>Úvod

U webových aplikací, které umožňují uživatelům pouze zobrazovat data nebo pro ty, které obsahují pouze jednoho uživatele, který může upravovat data, neexistuje hrozba dvou souběžných uživatelů, kteří by omylem přepsali nějaké další změny. U webových aplikací, které umožňují více uživatelům aktualizovat nebo odstraňovat data, je však možné, že změny jednoho uživatele v konfliktu s jiným souběžným uživatelem. Pokud neexistují žádné zásady souběžnosti, když dva uživatelé současně upravují jeden záznam, uživatel, který poslední změny potvrdí, přepíše změny provedené v prvním z nich.

Představte si například, že dva uživatelé, Jisun a Sam, navštívili stránku v naší aplikaci, která umožnila návštěvníkům aktualizovat a odstranit produkty prostřednictvím ovládacího prvku GridView. Obě klikněte na tlačítko Upravit v prvku GridView kolem stejného času. Jisun změní název produktu na "Chai čaj" a klikne na tlačítko Aktualizovat. Čistým výsledkem je příkaz `UPDATE`, který se pošle do databáze, která nastaví *všechna* pole s aktualizovatelným produktem (i když Jisun aktualizuje jenom jedno pole `ProductName`). V tomto okamžiku má databáze hodnoty "Chai čaj", "kategorie nápoje, exotické kapaliny dodavatele a tak dále pro tento konkrétní produkt. Ale v prvku GridView na obrazovce Sam se stále zobrazuje název produktu v upravitelném řádku GridView jako "Chai". Několik sekund po potvrzení změn Jisun aktualizuje správce Sam kategorii na koření a klikne na aktualizovat. Výsledkem je příkaz `UPDATE` odeslaný do databáze, která nastaví název produktu na "Chai", `CategoryID` na odpovídající ID kategorie nápojů atd. Změny názvu produktu Jisun byly přepsány. Obrázek 1 graficky znázorňuje tuto řadu událostí.

[![, když dva uživatelé současně aktualizují záznam, u kterých se může změnit jeden uživatel a přepsat ostatní s.](implementing-optimistic-concurrency-cs/_static/image2.png)](implementing-optimistic-concurrency-cs/_static/image1.png)

**Obrázek 1**: když dva uživatelé současně aktualizují záznam, který je potenciální pro změny jednoho uživatele, aby přepsal ostatní s ([kliknutím zobrazíte obrázek v plné velikosti).](implementing-optimistic-concurrency-cs/_static/image3.png)

Podobně platí, že když se na stránce zobrazí dva uživatelé, může být jedním uživatelem průběhu aktualizace záznamu, když ho odstraní jiný uživatel. Nebo v případě, že uživatel načte stránku a klikne na tlačítko Odstranit, mohl jiný uživatel změnit obsah tohoto záznamu.

K dispozici jsou tři strategie [řízení souběžnosti](http://en.wikipedia.org/wiki/Concurrency_control) :

- **Nedělat nic** – Pokud se souběžným uživatelům mění stejný záznam, nechte si poslední potvrzování změn (výchozí chování).
- [**Optimistická souběžnost**](http://en.wikipedia.org/wiki/Optimistic_concurrency_control) – předpokládá, že zatímco v současnosti může dojít ke konfliktům souběžnosti, a pak i velká většina času, ke kterému nedochází, ke konfliktům nedojde. Proto pokud dojde ke konfliktu, stačí informovat uživatele, že jejich změny nelze uložit, protože stejná data změnil jiný uživatel.
- **Pesimistická souběžnost** – předpokládá, že konflikty souběžnosti jsou maloobchodech a že uživatelé nemůžou tolerovat své změny v důsledku souběžné aktivity jiného uživatele. Proto když jeden uživatel spustí aktualizaci záznamu, zamkne ho a zabrání tak ostatním uživatelům v úpravách nebo odstraňování tohoto záznamu, dokud uživatel nepotvrdí jejich změny.

Všechny naše kurzy proto používaly výchozí strategii překladu souběžnosti – konkrétně si ponechá poslední soubor k zápisu. V tomto kurzu podíváme se, jak implementovat optimistické řízení souběžnosti.

> [!NOTE]
> V této sérii kurzů se nebudeme pohlížet na pesimistické příklady souběžnosti. Pesimistická souběžnost se používá zřídka, protože takové zámky, pokud nejsou řádně odstraněné, můžou ostatním uživatelům zabránit v aktualizaci dat. Pokud uživatel například zamkne záznam pro úpravy a potom před jeho odemknutím opustí den, nebude moci tento záznam aktualizovat, dokud původní uživatel nevrátí a nedokončí svoji aktualizaci. Proto v situacích, kde je používána pesimistická souběžnost, je obvykle časový limit, který, pokud je dosaženo, zrušení zámku. Websites pro prodej lístků, které zablokují konkrétní umístění pro umístění po krátké době, kdy uživatel dokončí proces objednávky, je příkladem pesimistické řízení souběžnosti.

## <a name="step-1-looking-at-how-optimistic-concurrency-is-implemented"></a>Krok 1: Podívejte se, jak je Optimistická souběžnost implementována

Optimistické řízení souběžnosti funguje tak, že zajistí, že záznam, který má být aktualizován nebo odstraněn, má stejné hodnoty jako při zahájení procesu aktualizace nebo odstranění. Například když kliknete na tlačítko Upravit ve upravitelném prvku GridView, hodnoty záznamu se čtou z databáze a zobrazují se v textových polích a dalších webových ovládacích prvcích. Tyto původní hodnoty jsou uloženy v prvku GridView. Později poté, co uživatel provede změny a klikne na tlačítko Aktualizovat, původní hodnoty a nové hodnoty se odešlou do vrstvy obchodní logiky a pak dolů do vrstvy přístupu k datům. Vrstva přístupu k datům musí vydat příkaz SQL, který bude aktualizovat pouze v případě, že původní hodnoty, které uživatel začal upravovat, jsou shodné s hodnotami stále v databázi. Obrázek 2 znázorňuje tuto posloupnost událostí.

[![aby se aktualizace nebo odstranění zdařily, měly by se původní hodnoty rovnat aktuálním hodnotám databáze.](implementing-optimistic-concurrency-cs/_static/image5.png)](implementing-optimistic-concurrency-cs/_static/image4.png)

**Obrázek 2**: aby byla aktualizace nebo odstranění úspěšná, původní hodnoty se musí shodovat s aktuálními hodnotami databáze ([kliknutím zobrazíte obrázek v plné velikosti).](implementing-optimistic-concurrency-cs/_static/image6.png)

Existují různé přístupy k implementaci optimistického řízení souběžnosti (viz [Petra a. Bromberg](http://peterbromberg.net/) [optimistická logika souběžného zpracování](http://www.eggheadcafe.com/articles/20050719.asp) pro Stručný pohled na řadu možností). Typová datová sada ADO.NET poskytuje jednu implementaci, která může být nakonfigurována pouze pomocí zaškrtnutí políčka. Povolení optimistického řízení souběžnosti pro TableAdapter ve typované datové sadě rozšiřuje příkazy `UPDATE` TableAdapter a `DELETE`, aby zahrnovaly porovnání všech původních hodnot v klauzuli `WHERE`. Následující příkaz `UPDATE` například aktualizuje název a cenu produktu pouze v případě, že aktuální hodnoty databáze jsou rovny hodnotám, které byly původně načteny při aktualizaci záznamu v prvku GridView. Parametry `@ProductName` a `@UnitPrice` obsahují nové hodnoty zadané uživatelem, zatímco `@original_ProductName` a `@original_UnitPrice` obsahují hodnoty, které byly původně načteny do prvku GridView při kliknutí na tlačítko pro úpravy:

[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample1.sql)]

> [!NOTE]
> Tento příkaz `UPDATE` byl pro čtení zjednodušen. V praxi by `UnitPrice` v klauzuli `WHERE` došlo k většímu podílu, protože `UnitPrice` může obsahovat `NULL` s a kontrola, zda `NULL = NULL` Always vrátí hodnotu false (místo toho musíte použít `IS NULL`).

Kromě použití jiného podkladového příkazu `UPDATE` konfigurace TableAdapter na použití optimistické souběžnosti mění také signaturu svých přímých metod databáze. Navrácení z našeho prvního kurzu, [*Vytvoření vrstvy přístupu k datům*](../introduction/creating-a-data-access-layer-cs.md), na kterou přímo metody databáze dostaly ty, které jako vstupní parametry přijaly seznam skalárních hodnot (spíše než silně typované instance DataRow nebo DataTable). Při použití optimistické souběžnosti metoda DB Direct `Update()` a `Delete()` zahrnuje vstupní parametry pro původní hodnoty. Kromě toho je nutné změnit také kód v knihoven BLL pro použití vzorce aktualizace dávky (přetížení metody `Update()`, které přijímají objekty DataRows a DataTables namísto skalárních hodnot).

Místo toho, abyste rozšířili naše stávající objekty TableAdapter DAL k používání optimistické souběžnosti (což by vyžadovalo změnu knihoven BLL na), vytvoříme místo toho novou typovou datovou sadu s názvem `NorthwindOptimisticConcurrency`, do které přidáme `Products` TableAdapter, která používá optimistickou souběžnost. Za tímto účelem vytvoříme třídu vrstvy `ProductsOptimisticConcurrencyBLL` obchodní logiky, která bude mít odpovídající úpravy pro podporu optimistické souběžnosti DAL. Po navýšení tohoto základyu budete připraveni vytvořit stránku ASP.NET.

## <a name="step-2-creating-a-data-access-layer-that-supports-optimistic-concurrency"></a>Krok 2: vytvoření vrstvy přístupu k datům, která podporuje optimistickou souběžnost

Chcete-li vytvořit novou typovou datovou sadu, klikněte pravým tlačítkem myši na složku `DAL` ve složce `App_Code` a přidejte novou datovou sadu s názvem `NorthwindOptimisticConcurrency`. Jak jsme viděli v prvním kurzu, tak se k typované datové sadě přidá nový TableAdapter a automaticky se spustí Průvodce konfigurací TableAdapter. Na první obrazovce se zobrazí výzva k zadání databáze pro připojení k databázi Northwind pomocí nastavení `NORTHWNDConnectionString` z `Web.config`.

[![se připojit ke stejné databázi Northwind](implementing-optimistic-concurrency-cs/_static/image8.png)](implementing-optimistic-concurrency-cs/_static/image7.png)

**Obrázek 3**: Připojte se ke stejné databázi Northwind ([kliknutím zobrazíte obrázek v plné velikosti).](implementing-optimistic-concurrency-cs/_static/image9.png)

V dalším kroku se zobrazí výzva k dotazování na data: prostřednictvím příkazu SQL ad-hoc, nové uložené procedury nebo existující uložené procedury. Vzhledem k tomu, že jsme v naší původní úrovni DAL používali dotazy SQL ad hoc, použijte tuto možnost i tady.

[![zadat data, která se mají načíst pomocí příkazu SQL ad hoc](implementing-optimistic-concurrency-cs/_static/image11.png)](implementing-optimistic-concurrency-cs/_static/image10.png)

**Obrázek 4**: určení dat, která se mají načíst pomocí příkazu SQL ad hoc ([kliknutím zobrazíte obrázek v plné velikosti](implementing-optimistic-concurrency-cs/_static/image12.png))

Na následující obrazovce zadejte dotaz SQL, který se použije k načtení informací o produktu. Pojďme použít přesně stejný dotaz SQL, který se používá pro `Products` TableAdapter z našeho původního DAL, který vrátí všechny `Product` sloupce společně s názvy dodavatele a kategorií produktů:

[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample2.sql)]

[![použít stejný dotaz SQL z produktů, které TableAdapter původní DAL.](implementing-optimistic-concurrency-cs/_static/image14.png)](implementing-optimistic-concurrency-cs/_static/image13.png)

**Obrázek 5**: použijte stejný dotaz SQL z `Products` TableAdapter v původním dal ([kliknutím zobrazíte obrázek v plné velikosti).](implementing-optimistic-concurrency-cs/_static/image15.png)

Než přejdete na další obrazovku, klikněte na tlačítko Upřesnit možnosti. Chcete-li, aby tato TableAdapter využívala optimistické řízení souběžnosti, stačí zaškrtnout políčko použít optimistickou souběžnost.

[![Povolit řízení souběžnosti kontrolou zaškrtnutím políčka &quot;použít optimistickou souběžnost&quot;](implementing-optimistic-concurrency-cs/_static/image17.png)](implementing-optimistic-concurrency-cs/_static/image16.png)

**Obrázek 6**: povolení optimistického řízení souběžnosti zaškrtnutím políčka použít optimistickou souběžnost ([kliknutím zobrazíte obrázek v plné velikosti](implementing-optimistic-concurrency-cs/_static/image18.png))

Nakonec uveďte, že by měl TableAdapter použít vzory přístupu k datům, které naplní DataTable a vrátí DataTable. také naznačovat, že by měly být vytvořeny metody přímé databáze. Změňte název metody pro návrat vzoru DataTable z GetData na GetProducts, aby bylo možné zrcadlit podle konvencí pojmenování, které jsme použili v naší původní DAL.

[![TableAdapter využívat všechny vzory přístupu k datům](implementing-optimistic-concurrency-cs/_static/image20.png)](implementing-optimistic-concurrency-cs/_static/image19.png)

**Obrázek 7**: TableAdapter využije všechny vzory přístupu k datům ([kliknutím zobrazíte obrázek v plné velikosti](implementing-optimistic-concurrency-cs/_static/image21.png)).

Po dokončení průvodce bude Návrhář DataSet obsahovat `Products` DataTable a TableAdapter se silným typem. Přejmenujte DataTable z `Products` na `ProductsOptimisticConcurrency`, což lze provést tak, že kliknete pravým tlačítkem na záhlaví objektu DataTable a zvolíte možnost Přejmenovat z kontextové nabídky.

[![objekt DataTable a TableAdapter byly přidány do typované datové sady.](implementing-optimistic-concurrency-cs/_static/image23.png)](implementing-optimistic-concurrency-cs/_static/image22.png)

**Obrázek 8**: do typované datové sady se přidala tabulka DataTable a TableAdapter ([kliknutím zobrazíte obrázek v plné velikosti](implementing-optimistic-concurrency-cs/_static/image24.png)).

Chcete-li zobrazit rozdíly mezi `UPDATE` a `DELETE` dotazech mezi `ProductsOptimisticConcurrency` TableAdapter (která používá Optimistická souběžnost) a produkty TableAdapter (což ne), klikněte na TableAdapter a přejděte na okno Vlastnosti. Ve vlastnostech `DeleteCommand` a `UpdateCommand` `CommandText` dílčí vlastnosti můžete zobrazit vlastní syntaxi SQL, která se pošle do databáze v případě, že jsou vyvolány metody týkající se aktualizace nebo odstranění DAL. Pro `ProductsOptimisticConcurrency` TableAdapter je použit příkaz `DELETE`:

[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample3.sql)]

Vzhledem k tomu, že příkaz `DELETE` TableAdapter produktu v našem originálu DAL je mnohem jednodušší:

[!code-sql[Main](implementing-optimistic-concurrency-cs/samples/sample4.sql)]

Jak vidíte, klauzule `WHERE` v příkazu `DELETE` pro TableAdapter, který používá optimistickou souběžnost, zahrnuje porovnání mezi každou z existujících hodnot sloupců tabulky `Product` a původními hodnotami v době, kdy byl objekt GridView (nebo DetailsView) naposledy vyplněn. Vzhledem k tomu, že všechna pole kromě `ProductID`, `ProductName`a `Discontinued` mohou mít `NULL` hodnoty, jsou zahrnuty další parametry a kontroly pro správné porovnání `NULL` hodnot v klauzuli `WHERE`.

Pro tento kurz nebudeme přidávat žádné další datové tabulky pro optimistickou datovou sadu s povoleným souběžným zpracováním, protože naše stránka ASP.NET bude poskytovat jenom aktualizaci a odstraňování informací o produktu. Pořád ale potřebujeme přidat metodu `GetProductByProductID(productID)` do `ProductsOptimisticConcurrency` TableAdapter.

Chcete-li to provést, klikněte pravým tlačítkem myši na záhlaví TableAdapter (oblast vpravo nad `Fill` a `GetProducts` názvy metod) a v místní nabídce vyberte možnost Přidat dotaz. Tím se spustí Průvodce konfigurací dotazu TableAdapter. Stejně jako u našich počátečních konfigurací TableAdapter se můžete rozhodnout vytvořit metodu `GetProductByProductID(productID)` pomocí ad-hoc příkazu SQL (viz obrázek 4). Vzhledem k tomu, že metoda `GetProductByProductID(productID)` vrací informace o konkrétním produktu, znamená to, že tento dotaz je `SELECT` typ dotazu, který vrací řádky.

[![označit typ dotazu jako &quot;vyberte, který vrací řádky&quot;](implementing-optimistic-concurrency-cs/_static/image26.png)](implementing-optimistic-concurrency-cs/_static/image25.png)

**Obrázek 9**: označte typ dotazu jako`SELECT`, která vrací řádky ([kliknutím zobrazíte obrázek v plné velikosti).](implementing-optimistic-concurrency-cs/_static/image27.png)

Na další obrazovce se zobrazí výzva k použití dotazu SQL s předem načteným výchozím dotazem TableAdapter. Rozšiřte existující dotaz tak, aby zahrnoval klauzuli `WHERE ProductID = @ProductID`, jak je znázorněno na obrázku 10.

[![do předem načteného dotazu přidat klauzuli WHERE, která vrátí konkrétní záznam produktu](implementing-optimistic-concurrency-cs/_static/image29.png)](implementing-optimistic-concurrency-cs/_static/image28.png)

**Obrázek 10**: přidání klauzule `WHERE` do předem načteného dotazu pro vrácení konkrétního záznamu produktu ([kliknutím zobrazíte obrázek v plné velikosti](implementing-optimistic-concurrency-cs/_static/image30.png))

Nakonec Změňte názvy generovaných metod na `FillByProductID` a `GetProductByProductID`.

[![přejmenovat metody na FillByProductID a GetProductByProductID](implementing-optimistic-concurrency-cs/_static/image32.png)](implementing-optimistic-concurrency-cs/_static/image31.png)

**Obrázek 11**: přejmenování metod `FillByProductID` a `GetProductByProductID` ([kliknutím zobrazíte obrázek v plné velikosti](implementing-optimistic-concurrency-cs/_static/image33.png))

Po dokončení tohoto průvodce TableAdapter nyní obsahuje dvě metody pro načítání dat: `GetProducts()`, které vrátí *všechny* produkty. a `GetProductByProductID(productID)`, které vrátí zadaný produkt.

## <a name="step-3-creating-a-business-logic-layer-for-the-optimistic-concurrency-enabled-dal"></a>Krok 3: vytvoření vrstvy obchodní logiky pro optimistickou souběžnost s povoleným přeměnum DAL

Naše existující třída `ProductsBLL` obsahuje příklady použití vzorových jak dávková aktualizace, tak i databáze Direct. Metoda `AddProduct` a `UpdateProduct` přetížení používají vzor aktualizace Batch, který předává instanci `ProductRow` k metodě aktualizace TableAdapter. `DeleteProduct` metoda na druhé straně používá model přímé DB, který volá metodu `Delete(productID)` TableAdapter.

Pomocí nového `ProductsOptimisticConcurrency` TableAdapter metody DB Direct nyní vyžadují, aby byly původní hodnoty také předány. Například metoda `Delete` nyní očekává deset vstupních parametrů: původní `ProductID`, `ProductName`, `SupplierID`, `CategoryID`, `QuantityPerUnit`, `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`, `ReorderLevel`a `Discontinued`. Používá tyto další hodnoty vstupních parametrů v klauzuli `WHERE` příkazu `DELETE`, který se posílá do databáze. zadaný záznam se odstraní jenom v případě, že jsou aktuální hodnoty databáze namapované na původní.

I když se signatura metody `Update` TableAdapter použitá ve vzorku aktualizace dávky nezměnila, kód potřebný k záznamu původní a nové hodnoty má. Proto se namísto pokusu o použití optimistické souběžnosti s naší existující `ProductsBLL` třídy vytvoří nová třída vrstvy obchodní logiky, která vám umožní pracovat s naším novým DAL.

Přidejte třídu s názvem `ProductsOptimisticConcurrencyBLL` do složky `BLL` ve složce `App_Code`.

![Přidání třídy ProductsOptimisticConcurrencyBLL do složky knihoven BLL](implementing-optimistic-concurrency-cs/_static/image34.png)

**Obrázek 12**: přidání třídy `ProductsOptimisticConcurrencyBLL` do složky knihoven BLL

Dále přidejte následující kód do třídy `ProductsOptimisticConcurrencyBLL`:

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample5.cs)]

Všimněte si, že příkaz using `NorthwindOptimisticConcurrencyTableAdapters` překračuje začátek deklarace třídy. Obor názvů `NorthwindOptimisticConcurrencyTableAdapters` obsahuje třídu `ProductsOptimisticConcurrencyTableAdapter`, která poskytuje metody DAL. Také před deklarací třídy najdete atribut `System.ComponentModel.DataObject`, který instruuje Visual Studio, aby zahrnoval tuto třídu v rozevíracím seznamu Průvodce ObjectDataSource.

Vlastnost `Adapter` `ProductsOptimisticConcurrencyBLL`poskytuje rychlý přístup k instanci třídy `ProductsOptimisticConcurrencyTableAdapter` a řídí se vzorem použitým v našich původních třídách knihoven BLL (`ProductsBLL`, `CategoriesBLL`atd.). Nakonec metoda `GetProducts()` jednoduše zavolá do metody `GetProducts()` DAL a vrátí objekt `ProductsOptimisticConcurrencyDataTable` naplněný instancí `ProductsOptimisticConcurrencyRow` pro každý záznam produktu v databázi.

## <a name="deleting-a-product-using-the-db-direct-pattern-with-optimistic-concurrency"></a>Odstranění produktu pomocí přímého vzoru DB s optimistické souběžnosti

Při použití modelu přímého přenosu databáze proti DAL, který používá optimistickou souběžnost, musí metody předat nové a původní hodnoty. Pro odstranění nejsou k dispozici žádné nové hodnoty, takže je potřeba předávat jenom původní hodnoty. V našem knihoven BLL musíte přijmout všechny původní parametry jako vstupní parametry. Pojďme mít metodu `DeleteProduct` ve třídě `ProductsOptimisticConcurrencyBLL` použijte metodu DB Direct. To znamená, že tato metoda musí převzít všechna deset datových polí produktu jako vstupní parametry a předat je do DAL, jak je znázorněno v následujícím kódu:

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample6.cs)]

Pokud původní hodnoty – tyto hodnoty, které byly naposledy načteny do prvku GridView (nebo DetailsView nebo FormView), se liší od hodnot v databázi, když uživatel klikne na tlačítko Odstranit, klauzule `WHERE` nebude odpovídat žádnému záznamu databáze a nebudou ovlivněny žádné záznamy. Proto bude metoda `Delete` TableAdapter vracet `0` a metoda `DeleteProduct` knihoven BLL vrátí `false`.

## <a name="updating-a-product-using-the-batch-update-pattern-with-optimistic-concurrency"></a>Aktualizace produktu pomocí vzorce aktualizace dávky s optimistické souběžnosti

Jak bylo uvedeno dříve, TableAdapter metoda pro vzor aktualizace dávky má stejnou signaturu metody bez ohledu na to, zda je nebo není k dis`Update` Optimistická souběžnost. Konkrétně metoda `Update` očekává objekt DataRow, pole DataRows, DataTable nebo typovou datovou sadu. Pro zadání původních hodnot nejsou k dispozici žádné další vstupní parametry. To je možné, protože objekt DataTable sleduje původní a změněné hodnoty pro jeho objekty DataRow (y). Když hodnota DAL vydá svůj `UPDATE` příkaz, naplní se parametry `@original_ColumnName` původními hodnotami objektu DataRow, zatímco parametry `@ColumnName` jsou naplněny změněnými hodnotami objektu DataRow.

Ve třídě `ProductsBLL` (která používá naši původní neoptimistickou souběžnost DAL) při použití vzorce aktualizace dávky k aktualizaci informací o produktu náš kód provede následující posloupnost událostí:

1. Přečtěte si informace o produktu Current Database do instance `ProductRow` pomocí `GetProductByProductID(productID)` metody TableAdapter
2. Přiřaďte nové hodnoty k instanci `ProductRow` z kroku 1.
3. Zavolejte metodu `Update` TableAdapter a předejte ji do instance `ProductRow`

Tato sekvence kroků ale nebude správně podporovat optimistickou souběžnost, protože `ProductRow` naplněná v kroku 1 je naplněna přímo z databáze, což znamená, že původní hodnoty použité objektem DataRow jsou ty, které aktuálně existují v databázi, a nikoli ty, které byly vázány na prvek GridView na začátku procesu úprav. Místo toho musíme při použití optimistické souběžnosti s povolenou metodou DAL změnit přetížení metody `UpdateProduct`, aby bylo možné použít následující kroky:

1. Přečtěte si informace o produktu Current Database do instance `ProductsOptimisticConcurrencyRow` pomocí `GetProductByProductID(productID)` metody TableAdapter
2. Přiřaďte *původní* hodnoty k instanci `ProductsOptimisticConcurrencyRow` z kroku 1.
3. Zavolejte metodu `AcceptChanges()` instance `ProductsOptimisticConcurrencyRow`, která instruuje, že aktuální hodnoty jsou "původní".
4. Přiřaďte *nové* hodnoty k instanci `ProductsOptimisticConcurrencyRow`.
5. Zavolejte metodu `Update` TableAdapter a předejte ji do instance `ProductsOptimisticConcurrencyRow`

Krok 1 přečte všechny aktuální hodnoty databáze pro zadaný záznam produktu. Tento krok je nadbytečný v `UpdateProduct` přetížení, které aktualizuje *všechny* sloupce produktu (protože tyto hodnoty jsou v kroku 2 přepsány), ale jsou nezbytné pro ta přetížení, kde jsou jako vstupní parametry předány pouze podmnožina hodnot sloupců. Po přiřazení původních hodnot k instanci `ProductsOptimisticConcurrencyRow` je volána metoda `AcceptChanges()`, která označuje aktuální hodnoty objektu DataRow jako původní hodnoty, které mají být použity v parametrech `@original_ColumnName` v příkazu `UPDATE`. Dále jsou nové hodnoty parametrů přiřazeny `ProductsOptimisticConcurrencyRow` a nakonec je vyvolána metoda `Update`, která předává objekt DataRow.

Následující kód ukazuje `UpdateProduct` přetížení, které přijímá všechna pole dat produktu jako vstupní parametry. I když tady není zobrazená, třída `ProductsOptimisticConcurrencyBLL` obsažená ve stahování pro tento kurz obsahuje taky `UpdateProduct` přetížení, které přijímá jenom název a cenu produktu jako vstupní parametry.

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample7.cs)]

## <a name="step-4-passing-the-original-and-new-values-from-the-aspnet-page-to-the-bll-methods"></a>Krok 4: předání původní a nové hodnoty ze stránky ASP.NET do metod knihoven BLL

V případě, že je DAL a knihoven BLL kompletní, vše zůstává k vytvoření stránky ASP.NET, která může využít logiku optimistického souběžnosti integrovaného systému. Konkrétně musí webový ovládací prvek data (GridView, DetailsView nebo FormView) pamatovat jeho původní hodnoty a prvek ObjectDataSource musí předat obě sady hodnot do vrstvy obchodní logiky. Kromě toho musí být stránka ASP.NET nakonfigurována tak, aby řádně zpracovávala narušení souběžnosti.

Začněte otevřením stránky `OptimisticConcurrency.aspx` ve složce `EditInsertDelete` a přidáním prvku GridView do návrháře, nastavením jeho vlastnosti `ID` na `ProductsGrid`. Z inteligentní značky GridViewu se můžete rozhodnout pro vytvoření nového prvku ObjectDataSource s názvem `ProductsOptimisticConcurrencyDataSource`. Vzhledem k tomu, že chceme, aby tato ObjectDataSource používala, která podporuje optimistickou souběžnost, nakonfigurujte ji tak, aby používala objekt `ProductsOptimisticConcurrencyBLL`.

[![mají prvek ObjectDataSource použít objekt ProductsOptimisticConcurrencyBLL](implementing-optimistic-concurrency-cs/_static/image36.png)](implementing-optimistic-concurrency-cs/_static/image35.png)

**Obrázek 13**: v prvku ObjectDataSource použijte objekt `ProductsOptimisticConcurrencyBLL` ([kliknutím zobrazíte obrázek v plné velikosti](implementing-optimistic-concurrency-cs/_static/image37.png)).

V průvodci vyberte metody `GetProducts`, `UpdateProduct`a `DeleteProduct` z rozevíracích seznamů. Pro metodu UpdateProduct použijte přetížení, které přijímá všechna datová pole produktu.

## <a name="configuring-the-objectdatasource-controls-properties"></a>Konfigurace vlastností ovládacího prvku ObjectDataSource

Po dokončení průvodce by deklarativní označení prvku ObjectDataSource mělo vypadat takto:

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample8.aspx)]

Jak vidíte, kolekce `DeleteParameters` obsahuje instanci `Parameter` pro každý z deseti vstupních parametrů v metodě `DeleteProduct` třídy `ProductsOptimisticConcurrencyBLL`. Podobně kolekce `UpdateParameters` obsahuje `Parameter` instanci pro každý vstupní parametr v `UpdateProduct`.

V předchozích kurzech, které se týkají změny dat, bychom v tomto okamžiku odebrali vlastnost `OldValuesParameterFormatString` ObjectDataSource, protože tato vlastnost označuje, že metoda knihoven BLL očekává, že se původní (nebo původní) hodnoty mají předat, a také nové hodnoty. Kromě toho tato hodnota vlastnosti označuje názvy vstupních parametrů pro původní hodnoty. Vzhledem k tomu, že do knihoven BLL přecházejí původní hodnoty, *neodstraňujte* tuto vlastnost.

> [!NOTE]
> Hodnota vlastnosti `OldValuesParameterFormatString` musí být namapována na názvy vstupních parametrů v knihoven BLL, které očekávají původní hodnoty. Vzhledem k tomu, že jsme tyto parametry jmenovali `original_productName`, `original_supplierID`a tak dále, můžete hodnotu vlastnosti `OldValuesParameterFormatString` ponechat jako `original_{0}`. Pokud však vstupní parametry metod knihoven BLL měly názvy, například `old_productName`, `old_supplierID`a tak dále, je nutné aktualizovat vlastnost `OldValuesParameterFormatString` na `old_{0}`.

Existuje jedno nastavení konečné vlastnosti, které je nutné provést, aby prvek ObjectDataSource správně předával původní hodnoty metodám knihoven BLL. Prvek ObjectDataSource má [vlastnost ConflictDetection](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.conflictdetection.aspx) , kterou lze přiřadit [jedné ze dvou hodnot](https://msdn.microsoft.com/library/system.web.ui.conflictoptions.aspx):

- `OverwriteChanges` – výchozí hodnota; neodesílá původní hodnoty do původních vstupních parametrů metod knihoven BLL.
- `CompareAllValues` – pošle původní hodnoty metodám knihoven BLL; tuto možnost vyberte při použití optimistického řízení souběžnosti.

Chvíli počkejte, než se nastaví vlastnost `ConflictDetection` na `CompareAllValues`.

## <a name="configuring-the-gridviews-properties-and-fields"></a>Konfigurace vlastností a polí prvku GridView

Když jsou vlastnosti prvku ObjectDataSource správně nakonfigurované, pojďme věnovat pozornost nastavení prvku GridView. Vzhledem k tomu, že chceme, aby prvek GridView podporoval úpravy a odstranění, klikněte na zaškrtávací políčka Povolit úpravy a povolit odstranění z inteligentní značky prvku GridView. Tím se přidá CommandField, jehož `ShowEditButton` a `ShowDeleteButton` jsou obě nastaveny na `true`.

Pokud je svázán s `ProductsOptimisticConcurrencyDataSource` ObjectDataSource, prvek GridView obsahuje pole pro každé datové pole produktu. I když takový prvek GridView lze upravovat, uživatelské prostředí je cokoli, ale přijatelné. `CategoryID` a `SupplierID` BoundFields se vykreslí jako textová pole a vyžadují, aby uživatel zadal příslušnou kategorii a dodavatele jako čísla ID. Pro číselná pole nebude žádné formátování a žádné ovládací prvky ověřování, aby se zajistilo, že byl dodán název produktu a že jednotková cena, jednotky v zásobách, jednotky v objednávce a změnit pořadí hodnot úrovně jsou správné číselné hodnoty a jsou větší než nebo rovny. na nulu.

Jak jsme popsali v tématu *přidávání ověřovacích ovládacích prvků do rozhraní pro úpravy a vkládání* a *přizpůsobení kurzů rozhraní pro úpravu dat* , lze uživatelské rozhraní přizpůsobit nahrazením BoundFields pomocí templatefields. Tento prvek GridView a jeho rozhraní pro úpravy jsem změnil (a) následujícími způsoby:

- Odebrání `ProductID`, `SupplierName`a `CategoryName` BoundFields
- Byl převeden `ProductName` vlastnost BoundField na TemplateField a přidán ovládací prvek RequiredFieldValidation.
- Převedli jsme `CategoryID` a `SupplierID` BoundFields na TemplateFields a upravili jsme rozhraní pro úpravy tak, aby místo textových polí používala DropDownList. V těchto TemplateFieldch `ItemTemplates`se zobrazí `CategoryName` a `SupplierName` datová pole.
- Převedly se `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`a `ReorderLevel` BoundFields na TemplateFields a přidali ovládací prvky CompareValidator.

Vzhledem k tomu, že jsme už prozkoumali, jak tyto úlohy provést v předchozích kurzech, stačí jenom vypsat tu konečnou deklarativní syntaxi a ponechání implementace v praxi.

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample9.aspx)]

Máme moc blízko, že máme plně funkční příklad. Existuje však několik odlišnostíů, které se budou podařit a mohou způsobovat problémy s námi. Dál potřebujeme některé rozhraní, které uživatele upozorní na to, kdy došlo k narušení souběžnosti.

> [!NOTE]
> Aby webové ovládací prvek data mohl správně předat původní hodnoty do prvku ObjectDataSource (které jsou poté předány do knihoven BLL), je důležité, aby vlastnost `EnableViewState` prvku GridView byla nastavena na `true` (výchozí). Pokud stav zobrazení zakážete, původní hodnoty se při postbacku ztratí.

## <a name="passing-the-correct-original-values-to-the-objectdatasource"></a>Předání správných původních hodnot prvku ObjectDataSource

Existuje několik problémů se způsobem konfigurace prvku GridView. Pokud je vlastnost `ConflictDetection` prvku ObjectDataSource nastavena na hodnotu `CompareAllValues` (jako je naše), při volání metody `Update()` nebo `Delete()` prvku GridView (nebo DetailsView), se ObjectDataSource pokusí zkopírovat původní hodnoty prvku GridView do příslušných `Parameter` instancí. Pro grafické znázornění tohoto procesu se podívejte zpátky na obrázek 2.

Konkrétně jsou hodnoty z původních hodnot prvku GridView přiřazeny v případě, že jsou data svázána s prvku GridView. Proto je nutné, aby všechny požadované původní hodnoty byly zachyceny prostřednictvím obousměrné vazby dat a aby byly poskytnuty v převoditelné podobě.

Pokud chcete zjistit, proč je to důležité, chvíli počkejte, než navštívíte naši stránku v prohlížeči. Podle očekávání je v prvku GridView uveden každý produkt s tlačítkem upravit a odstranit ve sloupci nejvíce vlevo.

[![jsou produkty uvedeny v prvku GridView.](implementing-optimistic-concurrency-cs/_static/image39.png)](implementing-optimistic-concurrency-cs/_static/image38.png)

**Obrázek 14**: produkty jsou uvedeny v prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](implementing-optimistic-concurrency-cs/_static/image40.png)).

Pokud kliknete na tlačítko Odstranit pro libovolný produkt, je vyvolána `FormatException`.

[![pokusu o odstranění jakéhokoli výsledku produktu v rámci aplikace FormatException](implementing-optimistic-concurrency-cs/_static/image42.png)](implementing-optimistic-concurrency-cs/_static/image41.png)

**Obrázek 15**: pokus o odstranění jakýchkoliv výsledků produktu v `FormatException` ([kliknutím zobrazíte obrázek v plné velikosti](implementing-optimistic-concurrency-cs/_static/image43.png))

`FormatException` je vyvolána, když se prvek ObjectDataSource pokusí přečíst původní hodnotu `UnitPrice`. Vzhledem k tomu, že `ItemTemplate` má `UnitPrice` formátované jako měna (`<%# Bind("UnitPrice", "{0:C}") %>`), zahrnuje symbol měny, například $19,95. K `FormatException` dojde, když se prvek ObjectDataSource pokusí převést tento řetězec na `decimal`. K obcházení tohoto problému máme několik možností:

- Odebere formátování měny z `ItemTemplate`. To znamená, že místo použití `<%# Bind("UnitPrice", "{0:C}") %>`stačí použít `<%# Bind("UnitPrice") %>`. Nevýhodou je, že cena už není naformátovaná.
- Umožňuje zobrazit `UnitPrice` v `ItemTemplate`formátovat jako měnu, ale k tomu použijte klíčové slovo `Eval`. Odvolání tohoto `Eval` provádí jednosměrnou vazbu. Pro původní hodnoty stále potřebujeme zadat `UnitPrice` hodnotu, takže v `ItemTemplate`pořád potřebujeme obousměrný příkaz DataBinding, ale dá se umístit do ovládacího prvku popisek webu, jehož vlastnost `Visible` je nastavená na `false`. V šabloně ItemTemplate můžeme použít následující kód:

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample10.aspx)]

- Odeberte formátování měny z `ItemTemplate`pomocí `<%# Bind("UnitPrice") %>`. V obslužné rutině události `RowDataBound` prvku GridView programově přístup k ovládacímu prvku popisek webu, ve kterém je zobrazena hodnota `UnitPrice` a nastavte její vlastnost `Text` na naformátovanou verzi.
- Ponechte `UnitPrice` formátovanou jako měnu. V obslužné rutině události `RowDeleting` prvku GridView nahraďte existující hodnotu `UnitPrice` ($19,95) skutečnou hodnotou typu Decimal pomocí `Decimal.Parse`. Zjistili jsme, jak v knihoven BLL obslužné rutiny při [*zpracování výjimek na úrovni a dal v kurzu ASP.NET stránky*](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md) udělat něco podobného jako v obslužné rutině události `RowUpdating`.

V tomto příkladu jsem se rozhodl s druhým přístupem, a to přidáním skrytého webového ovládacího prvku popisek, jehož vlastnost `Text` je obousměrná data vázaná na neformátovanou `UnitPrice` hodnotu.

Po vyřešení tohoto problému zkuste znovu kliknout na tlačítko Odstranit pro libovolný produkt. Tentokrát získáte `InvalidOperationException`, když se ObjectDataSource pokusí vyvolat metodu `UpdateProduct` knihoven BLL.

[![prvek ObjectDataSource nemůže najít metodu se vstupními parametry, které chce odeslat.](implementing-optimistic-concurrency-cs/_static/image45.png)](implementing-optimistic-concurrency-cs/_static/image44.png)

**Obrázek 16**: prvek ObjectDataSource nemůže najít metodu se vstupními parametry, které chce odeslat ([kliknutím zobrazíte obrázek v plné velikosti).](implementing-optimistic-concurrency-cs/_static/image46.png)

Při prohlížení zprávy o výjimce je jasné, že prvek ObjectDataSource chce vyvolat metodu knihoven BLL `DeleteProduct`, která zahrnuje `original_CategoryName` a vstupní parametry `original_SupplierName`. Důvodem je, že `ItemTemplate` s pro `CategoryID` a `SupplierID` TemplateFields aktuálně obsahují obousměrné příkazy BIND s datovými poli `CategoryName` a `SupplierName`. Místo toho je potřeba zahrnout `Bind` příkazy do datových polí `CategoryID` a `SupplierID`. Chcete-li to provést, nahraďte existující příkazy BIND příkazy `Eval` a poté přidejte skryté ovládací prvky popisek, jejichž `Text` vlastnosti jsou vázány na `CategoryID` a `SupplierID` datových polí pomocí obousměrné datové sady, jak je znázorněno níže:

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample11.aspx)]

S těmito změnami teď dokážeme úspěšně odstranit a upravit informace o produktu! V kroku 5 se podíváme na to, jak ověřit, že se zjišťují narušení souběžnosti. Prozatím ale počkejte několik minut, než se pokusíte aktualizovat a odstranit pár záznamů, abyste zajistili, že aktualizace a odstraňování pro jednoho uživatele funguje podle očekávání.

## <a name="step-5-testing-the-optimistic-concurrency-support"></a>Krok 5: testování podpory optimistického řízení souběžnosti

Aby bylo možné ověřit, že došlo k narušení souběžnosti (místo toho, aby se data nemusela přepsat), musíme na této stránce otevřít dva okna prohlížeče. V obou instancích prohlížeče klikněte na tlačítko Upravit pro příkaz Chai. Pak v jednom z prohlížečů změňte název na "Chai čaj" a klikněte na aktualizovat. Aktualizace by měla být úspěšná a vracet prvek GridView do stavu před úpravou "Chai čaj" jako nový název produktu.

V ostatních instancích okna prohlížeče se ale v textovém poli název produktu stále zobrazuje "Chai". V tomto druhém okně prohlížeče aktualizujte `UnitPrice` na `25.00`. Bez podpory optimistického řízení souběžnosti po kliknutí na aktualizovat ve druhé instanci prohlížeče se změní název produktu zpět na "Chai". tím se přepíší změny provedené první instancí prohlížeče. S využitím optimistické souběžnosti, ale kliknutím na tlačítko Aktualizovat v druhé instanci prohlížeče dojde k [DBConcurrencyException –](https://msdn.microsoft.com/library/system.data.dbconcurrencyexception.aspx).

[![, když se zjistí porušení souběžnosti, vyvolá se DBConcurrencyException –.](implementing-optimistic-concurrency-cs/_static/image48.png)](implementing-optimistic-concurrency-cs/_static/image47.png)

**Obrázek 17**: když se zjistí porušení souběžnosti, vyvolá se `DBConcurrencyException` ([kliknutím zobrazíte obrázek v plné velikosti).](implementing-optimistic-concurrency-cs/_static/image49.png)

`DBConcurrencyException` se vyvolá pouze v případě, že je využíván vzor hromadné aktualizace dávky DAL. Model přímé databáze nevyvolává výjimku, ale pouze označuje, že nebyly ovlivněny žádné řádky. K tomu je potřeba, aby oba instance prohlížeče vracely stav před úpravou. Potom v první instanci prohlížeče klikněte na tlačítko Upravit a změňte název produktu z "Chai čaj" zpět na "Chai" a klikněte na aktualizovat. V druhém okně prohlížeče klikněte na tlačítko Odstranit pro příkaz Chai.

Po kliknutí na tlačítko Odstranit se stránka publikuje zpět, prvek GridView Vyvolá metodu `Delete()` prvku ObjectDataSource a prvek ObjectDataSource se zavolá do `DeleteProduct` metody `ProductsOptimisticConcurrencyBLL` třídy, přičemž se přesměruje na původní hodnoty. Původní hodnota `ProductName` druhé instance prohlížeče je "Chai čaj", která se neshoduje s aktuální `ProductName` hodnotou v databázi. Proto příkaz `DELETE` vydaný pro databázi má vliv na nulové řádky, protože v databázi není žádný záznam, který splňuje klauzule `WHERE`. Metoda `DeleteProduct` vrací `false` a data prvku ObjectDataSource jsou znovu svázána s ovládacím prvkem GridView.

V perspektivě koncového uživatele kliknutí na tlačítko Odstranit pro Chai čaj v druhém okně prohlížeče způsobilo, že se obrazovka Flash a po návratu zpátky produkt pořád obsahuje, i když je teď uvedený jako "Chai" (Změna názvu produktu vytvořeného prvním prohlížečem). instance). Pokud uživatel klikne na tlačítko Odstranit znovu, odstranění bude úspěšné, protože původní hodnota `ProductName` ovládacího prvku GridView ("Chai") nyní odpovídá hodnotě v databázi.

V obou těchto případech je činnost koncového uživatele mnohem z ideálního. Jasně nechceme uživateli zobrazit Nitty-Gritty podrobnosti o výjimce `DBConcurrencyException` při použití vzorce aktualizace dávky. A chování při použití vzoru DB Direct je trochu matoucí, protože příkaz uživatele se nezdařil, ale nedošlo k přesnému uvedení důvodu.

Abychom tyto dva problémy napravili, můžeme na stránce Vytvořit popisek webové ovládací prvky, které poskytují vysvětlení, proč se aktualizace nebo odstranění nepovedlo. Pro vzor dávkové aktualizace můžeme určit, zda došlo k výjimce `DBConcurrencyException` v obslužné rutině události na post-Level prvku GridView a zobrazit popisek upozornění podle potřeby. Pro metodu DB Direct můžeme zkontrolovat návratovou hodnotu metody knihoven BLL (což je `true`, pokud byl ovlivněn jeden řádek, `false` jinak) a podle potřeby zobrazit informační zprávu.

## <a name="step-6-adding-informational-messages-and-displaying-them-in-the-face-of-a-concurrency-violation"></a>Krok 6: Přidání informačních zpráv a jejich zobrazení na tvář narušení souběžnosti

Když dojde k narušení souběžnosti, chování se projeví v závislosti na tom, jestli se použil vzor pro dávkovou aktualizaci nebo přímý DB. Náš kurz používá oba vzory s vzorem aktualizace dávky, který se používá pro aktualizaci, a vzor databáze Direct použitý k odstranění. Chcete-li začít, přidejte na naši stránku dva webové ovládací prvky Label, které vysvětlují, že při pokusu o odstranění nebo aktualizaci dat došlo k narušení souběžnosti. Nastavte vlastnosti ovládacího prvku popisek `Visible` a `EnableViewState` na `false`; To způsobí, že budou skryté na každé návštěvě stránky s výjimkou toho, že se jedná o konkrétní stránky, u nichž je jejich vlastnost `Visible` programově nastavená na `true`.

[!code-aspx[Main](implementing-optimistic-concurrency-cs/samples/sample12.aspx)]

Kromě nastavení vlastností `Visible`, `EnabledViewState`a `Text` jsem také nastavil (a) vlastnost `CssClass` na `Warning`, což způsobí zobrazení popisku ve velkém, červené, kurzívě a tučném písmu. Tato třída CSS `Warning` byla definována a přidána do stylů. CSS zpátky při *zkoumání událostí souvisejících s kurzem vložení, aktualizace a odstranění* .

Po přidání těchto popisků by měl Návrhář v aplikaci Visual Studio vypadat podobně jako obrázek 18.

[na stránku se přidaly dva ovládací prvky Label ![.](implementing-optimistic-concurrency-cs/_static/image51.png)](implementing-optimistic-concurrency-cs/_static/image50.png)

**Obrázek 18**: na stránku bylo přidáno dva ovládací prvky popisku ([kliknutím zobrazíte obrázek v plné velikosti).](implementing-optimistic-concurrency-cs/_static/image52.png)

S těmito webovými ovládacími prvky popisků jsme připraveni zjistit, jak určit, kdy došlo k narušení souběžnosti. v takovém případě je možné vlastnost `Visible` popisku nastavit na `true`a zobrazit informační zprávu.

## <a name="handling-concurrency-violations-when-updating"></a>Manipulace s porušením souběžnosti při aktualizaci

Nejdřív se podíváme na to, jak zvládnout porušení souběžnosti při použití vzorce aktualizace dávky. Vzhledem k tomu, že taková porušení se vzorkem aktualizace dávky způsobí vyvolání výjimky `DBConcurrencyException`, musíme na naši stránku ASP.NET přidat kód, který určí, jestli během procesu aktualizace došlo k výjimce `DBConcurrencyException`. Pokud ano, měli byste uživateli zobrazit zprávu, že jejich změny nebyly uloženy, protože jiná uživatel změnil stejná data mezi tím, kdy začala upravovat záznam a po kliknutí na tlačítko Aktualizovat.

Jak jsme viděli v kurzu *zpracování knihoven BLL a na úrovni dal v kurzu stránky ASP.NET* , takové výjimky se dají detekovat a potlačit v obslužných rutinách událostí na úrovni ovládacího prvku webové správy dat. Proto musíme vytvořit obslužnou rutinu události pro událost `RowUpdated` prvku GridView, která kontroluje, zda byla vyvolána výjimka `DBConcurrencyException`. Tato obslužná rutina události je předána odkaz na jakoukoliv výjimku, která byla vyvolána během procesu aktualizace, jak je znázorněno v následujícím kódu obslužné rutiny události:

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample13.cs)]

Na straně `DBConcurrencyException` výjimky tato obslužná rutina události zobrazuje ovládací prvek `UpdateConflictMessage` popisek a indikuje, že byla výjimka zpracována. Pokud je tento kód na místě, když při aktualizaci záznamu dojde k narušení souběžnosti, změny uživatele se ztratí, protože by přepsali změny jiného uživatele ve stejnou dobu. Konkrétně je prvek GridView vrácen do svého stavu před úpravou a svázán s aktuálními daty databáze. Tím se aktualizuje řádek prvku GridView o změny provedené jiným uživatelem, které byly dříve neviditelné. Kromě toho ovládací prvek popisek `UpdateConflictMessage` vysvětlí uživateli, co se právě stalo. Tato posloupnost událostí je podrobně popsána na obrázku 19.

[![, že se aktualizace uživatelů ztratí při narušení souběžnosti](implementing-optimistic-concurrency-cs/_static/image54.png)](implementing-optimistic-concurrency-cs/_static/image53.png)

**Obrázek 19**: při narušení souběžnosti dojde ke ztrátě aktualizací uživatelů ([kliknutím zobrazíte obrázek s plnou velikostí](implementing-optimistic-concurrency-cs/_static/image55.png)).

> [!NOTE]
> Alternativně, namísto vrácení prvku GridView do stavu před úpravou, můžeme opustit prvek GridView ve svém stavu úprav nastavením vlastnosti `KeepInEditMode` předaného objektu `GridViewUpdatedEventArgs` na hodnotu true. Pokud tento postup použijete, je však nutné, aby se data znovu navázala na prvek GridView (vyvoláním jeho `DataBind()` metody), aby byly hodnoty ostatních uživatelů načteny do rozhraní pro úpravy. Kód, který je k dispozici ke stažení v tomto kurzu, má tyto dva řádky kódu v obslužné rutině události `RowUpdated` s komentářem. jednoduše Odkomentujte tyto řádky kódu, aby ovládací prvek GridView zůstal v režimu úprav po porušení souběžnosti.

## <a name="responding-to-concurrency-violations-when-deleting"></a>Reakce na porušení souběžnosti při odstraňování

Při přímém vzoru DB není při narušení souběžnosti vyvolána žádná výjimka. Místo toho databázový příkaz jednoduše neovlivní žádné záznamy, protože klauzule WHERE neodpovídá žádnému záznamu. Všechny metody změny dat vytvořené v knihoven BLL byly navrženy tak, aby vracely logickou hodnotu, která určuje, zda ovlivnila přesně jeden záznam. Proto, aby bylo možné zjistit, jestli při odstraňování záznamu došlo k narušení souběžnosti, můžeme prostudovat návratovou hodnotu metody `DeleteProduct` knihoven BLL.

Návratovou hodnotu pro metodu knihoven BLL lze prozkoumat v obslužných rutinách události na úrovni ovládacího prvku ObjectDataSource prostřednictvím vlastnosti `ReturnValue` objektu `ObjectDataSourceStatusEventArgs` předaného do obslužné rutiny události. Vzhledem k tomu, že vás zajímá určení návratové hodnoty z metody `DeleteProduct`, musíme vytvořit obslužnou rutinu události pro událost `Deleted` prvku ObjectDataSource. Vlastnost `ReturnValue` je typu `object` a může být `null`, pokud byla vyvolána výjimka a metoda byla přerušena před tím, než by mohla vracet hodnotu. Proto je třeba nejprve zajistit, aby vlastnost `ReturnValue` nebyla `null` a je logická hodnota. Za předpokladu, že tato kontrola projde, zobrazí se `DeleteConflictMessage` ovládací prvek popisek, pokud je `ReturnValue` `false`. To lze provést pomocí následujícího kódu:

[!code-csharp[Main](implementing-optimistic-concurrency-cs/samples/sample14.cs)]

V případě porušení souběžnosti se žádost o odstranění uživatele zruší. Prvek GridView se aktualizuje a zobrazí změny, ke kterým došlo pro daný záznam mezi časem, kdy uživatel stránku načetl, a když klikl na tlačítko Odstranit. Pokud takové porušení nastane, zobrazí se popisek `DeleteConflictMessage`, který vysvětluje, co se právě stalo (viz obrázek 20).

[![odstranění uživatele se zrušilo na straně porušení souběžnosti.](implementing-optimistic-concurrency-cs/_static/image57.png)](implementing-optimistic-concurrency-cs/_static/image56.png)

**Obrázek 20**: odstranění uživatele se zrušilo na straně porušení souběžnosti ([kliknutím zobrazíte obrázek v plné velikosti).](implementing-optimistic-concurrency-cs/_static/image58.png)

## <a name="summary"></a>Přehled

Příležitosti pro narušení souběžnosti existují v každé aplikaci, která umožňuje více souběžným uživatelům aktualizovat nebo odstraňovat data. Pokud se taková porušení neúčtují pro, když dva uživatelé současně aktualizují stejná data, která jsou v posledním zápisu "WINS", přepíše změny provedené ostatními uživateli. Vývojáři mohou případně implementovat buď optimistické, nebo pesimistické řízení souběžnosti. Optimistické řízení souběžnosti předpokládá, že narušení souběžnosti jsou zřídka a jednoduše nepovoluje příkaz Update nebo DELETE, který by představoval narušení souběžnosti. Pesimistické řízení souběžnosti předpokládá, že narušení souběžnosti často a jednoduše odmítání aktualizace jednoho uživatele nebo příkazu k odstranění není přijatelné. Díky pesimistické kontrole souběžnosti aktualizace záznamů zahrnuje jejich uzamykání, což brání ostatním uživatelům v úpravách nebo odstraňování záznamu v době, kdy je uzamčen.

Typová datová sada v rozhraní .NET poskytuje funkce pro podporu optimistického řízení souběžnosti. Konkrétně příkazy `UPDATE` a `DELETE` vydané do databáze obsahují všechny sloupce tabulky, čímž se zajistí, že aktualizace nebo odstranění budou provedeny pouze v případě, že se aktuální data záznamu shodují s původními daty, která měla uživatel při provádění aktualizace nebo odstranění. Jakmile je DAL nakonfigurovaný tak, aby podporoval optimistickou souběžnost, metody knihoven BLL je potřeba aktualizovat. Kromě toho musí být stránka ASP.NET, která volá do knihoven BLL, nakonfigurována tak, aby prvek ObjectDataSource načítají původní hodnoty z ovládacího prvku data a předává je do knihoven BLL.

Jak jsme viděli v tomto kurzu, implementace optimistického řízení souběžnosti ve webové aplikaci ASP.NET zahrnuje aktualizaci DAL a knihoven BLL a přidání podpory na stránku ASP.NET. Bez ohledu na to, jestli tato přidaná práce představuje moudrou investici vašeho času a úsilí, záleží na vaší aplikaci. Pokud nechcete, aby souběžní uživatelé aktualizovali data, nebo se data, která aktualizují, liší od sebe, pak řízení souběžnosti není klíčový problém. Pokud ale pravidelně máte na svém webu více uživatelů, kteří pracují se stejnými daty, řízení souběžnosti může zabránit tomu, aby se aktualizace jednoho uživatele nebo odstranění z unwittingly přepsaly jiným.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Předchozí](customizing-the-data-modification-interface-cs.md)
> [Další](adding-client-side-confirmation-when-deleting-cs.md)

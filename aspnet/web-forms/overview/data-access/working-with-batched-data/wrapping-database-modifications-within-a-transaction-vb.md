---
uid: web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb
title: Zalamování změn databáze v rámci transakce (VB) | Microsoft Docs
author: rick-anderson
description: Tento kurz je první ze čtyř, které se prohlíží při aktualizaci, odstraňování a vkládání dávek dat. V tomto kurzu se dozvíte, jak povolují transakce databáze...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: 7d821db5-6cbb-4b38-af14-198f9155fc82
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-vb
msc.type: authoredcontent
ms.openlocfilehash: dee95ee2789a69aac5aa79b8358e58e3ee99e1b2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74636616"
---
# <a name="wrapping-database-modifications-within-a-transaction-vb"></a>Zabalení úprav databáze do transakce (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_63_VB.zip) nebo [stažení PDF](wrapping-database-modifications-within-a-transaction-vb/_static/datatutorial63vb1.pdf)

> Tento kurz je první ze čtyř, které se prohlíží při aktualizaci, odstraňování a vkládání dávek dat. V tomto kurzu se dozvíte, jak transakce databáze umožňují provádět úpravy dávek jako atomická operace, která zajišťuje, že se všechny kroky úspěšně nebo selžou.

## <a name="introduction"></a>Úvod

Jak jsme zjistili, že jsme začali s [přehledem vkládání, aktualizace a odstraňování dat](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) , prvek GridView nabízí integrovanou podporu pro úpravy a odstraňování na úrovni řádků. Pomocí několika kliknutí myši je možné vytvořit bohatou rozhraní pro úpravu dat bez psaní řádku kódu, pokud jste obsah s úpravami a odstraňováním na jednotlivých řádcích. V některých scénářích to však není dostačující a musíme uživatelům poskytnout možnost upravit nebo odstranit dávku záznamů.

Například většina webových e-mailových klientů používá mřížku k vypsání každé zprávy, kde každý řádek obsahuje zaškrtávací políčko spolu s informacemi o e-mailu (předmět, odesilatel atd.). Toto rozhraní umožňuje uživateli odstranit více zpráv tím, že je zkontroluje a pak klikne na tlačítko Odstranit vybrané zprávy. Rozhraní pro úpravu dávky je ideální v situacích, kdy uživatelé běžně upravují mnoho různých záznamů. Místo toho, aby uživatel mohl kliknout na upravit, provést změnu a pak kliknout na aktualizovat u každého záznamu, který je potřeba upravit, rozhraní pro úpravu dávky vykresluje jednotlivé řádky s rozhraním pro úpravu. Uživatel může rychle upravit sadu řádků, které je potřeba změnit, a pak tyto změny uložit kliknutím na tlačítko Aktualizovat vše. V této sadě kurzů podíváme se, jak vytvořit rozhraní pro vkládání, úpravu a odstraňování dávek dat.

Při provádění dávkových operací je důležité určit, jestli má být možné, aby některé operace v dávce byly úspěšné, zatímco jiné selžou. Vezměte v úvahu dávkové odstranění rozhraní – co se stane, když se první vybraný záznam úspěšně odstraní, ale druhý z nich se nezdaří, například kvůli porušení omezení cizího klíče? Má se první záznam odstranit zpátky nebo je přijatelný, aby se první záznam stále odstranil?

Pokud chcete, aby se operace dávky zpracovala jako [atomická operace](http://en.wikipedia.org/wiki/Atomic_operation), jedna, kde všechny kroky proběhly úspěšně, nebo všechny kroky selžou, je nutné rozšířit vrstvu přístupu k datům, aby zahrnovala podporu [databázových transakcí](http://en.wikipedia.org/wiki/Database_transaction). Transakce databáze zaručují nedělitelnost pro sadu `INSERT`, `UPDATE`a `DELETE`ch příkazů spouštěných v rámci transakce a jsou funkcí podporovanými většinou všech moderních databázových systémů.

V tomto kurzu se podíváme na to, jak rozšiřujete DAL na použití databázových transakcí. Další kurzy budou kontrolovat implementaci webových stránek pro dávkové vkládání, aktualizaci a odstraňování rozhraní. Pojďme začít!

> [!NOTE]
> Při úpravě dat v transakci dávky není atomie vždy potřeba. V některých scénářích může být přijatelné, aby některé změny dat byly úspěšné a jiné ve stejné dávce selžou, například při odstraňování sady e-mailů z webového e-mailového klienta. Pokud dojde k chybě databáze na základě procesu odstranění, je pravděpodobné, že tyto záznamy byly zpracovány bez chyby, ale zůstanou odstraněny. V takových případech není nutné upravovat DAL pro podporu databázových transakcí. Existují i další scénáře operace Batch, kde je však nevýznamná atomická akce. Když zákazník přesune své prostředky z jednoho bankovního účtu do jiného, musí se provést dvě operace: prostředky se musí od prvního účtu odečíst a pak se přidají k druhému. I když banka nemusí mít k úspěšnému prvnímu kroku úspěch, ale druhý krok selže, jeho zákazníci by pochopili, že by se nemuseli rušit. Doporučujeme, abyste s tímto kurzem pracovali a implementovali vylepšení pro podporu transakcí databáze i v případě, že je neplánujete při jejich použití v dávkách vkládat, aktualizovat a odstraňovat rozhraní Batch, která se budou sestavovat v následujících třech kurzech.

## <a name="an-overview-of-transactions"></a>Přehled transakcí

Většina databází zahrnuje podporu pro *transakce*, které umožňují seskupení více databázových příkazů do jedné logické jednotky práce. Příkazy databáze, které tvoří transakci, jsou zaručené jako atomické, což znamená, že všechny příkazy selžou nebo budou úspěšné.

Obecně platí, že transakce jsou implementovány prostřednictvím příkazů SQL pomocí následujícího vzoru:

1. Označuje začátek transakce.
2. Spusťte příkazy SQL, které tvoří transakci.
3. Pokud dojde k chybě v jednom z příkazů z kroku 2, vraťte transakci zpět.
4. Pokud všechny příkazy z kroku 2 se dokončí bez chyby, potvrďte transakci.

Příkazy jazyka SQL použité k vytvoření, potvrzení a vrácení transakce lze zadat ručně při psaní skriptů SQL nebo při vytváření uložených procedur nebo prostřednictvím programových prostředků s použitím buď ADO.NET nebo třídy v [oboru názvů`System.Transactions`](https://msdn.microsoft.com/library/system.transactions.aspx). V tomto kurzu prověříme jenom správu transakcí pomocí ADO.NET. V budoucím kurzu se podíváme na to, jak používat uložené procedury ve vrstvě přístupu k datům. v této době prozkoumáme příkazy SQL pro vytváření, vracení zpátky a potvrzování transakcí. Mezitím si přečtěte další informace [v části Správa transakcí v uložených procedurách SQL Server](http://www.4guysfromrolla.com/webtech/080305-1.shtml) .

> [!NOTE]
> [Třída`TransactionScope`](https://msdn.microsoft.com/library/system.transactions.transactionscope.aspx) v oboru názvů `System.Transactions` umožňuje vývojářům programově zabalit řadu příkazů v rámci oboru transakce a zahrnuje podporu pro komplexní transakce, které zahrnují více zdrojů, jako jsou dvě různé databáze nebo dokonce heterogenní typy úložišť dat, jako je například databáze Microsoft SQL Server, databáze Oracle a webová služba. Rozhodl (a) použít transakce ADO.NET pro tento kurz místo `TransactionScope` třídy, protože ADO.NET je konkrétnější pro databázové transakce a v mnoha případech je mnohem méně náročná na prostředky. Kromě toho se v některých scénářích `TransactionScope` třída používá Microsoft DTC (Distributed Transaction Coordinator) (MSDTC). Problémy s konfigurací, implementací a výkonem v případě, že koordinátor MSDTC vytvoří místo specializovaného a pokročilého tématu a překračuje rozsah těchto kurzů.

Při práci se zprostředkovatelem SqlClient v ADO.NET jsou transakce iniciovány prostřednictvím volání [metody`BeginTransaction`](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.begintransaction.aspx) [třídy`SqlConnection`](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx) , která vrací [objekt`SqlTransaction`](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.aspx). Příkazy změny dat, které strukturu transakci, jsou umístěny v rámci `try...catch`ho bloku. Pokud dojde k chybě v příkazu v bloku `try`, spuštění se přenese do bloku `catch`, kde lze transakci vrátit zpět prostřednictvím metody `SqlTransaction` objektů s [`Rollback`](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.rollback.aspx). Pokud všechny příkazy byly úspěšně dokončeny, volání metody `SqlTransaction` objektu s [`Commit`](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.commit.aspx) na konci bloku `try` potvrdí transakci. Tento model ilustruje následující fragment kódu. Další syntaxe a příklady použití transakcí s ADO.NET najdete v tématu [Údržba konzistence databáze pomocí transakcí](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx) .

[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample1.vb)]

Ve výchozím nastavení objekty TableAdapter ve typované datové sadě nepoužívá transakce. Pro zajištění podpory pro transakce, které potřebujeme k rozšíření tříd TableAdapter, aby zahrnovaly další metody, které používají výše uvedený vzor k provádění řady příkazů pro úpravu dat v rámci oboru transakce. V kroku 2 se dozvíte, jak použít částečné třídy pro přidání těchto metod.

## <a name="step-1-creating-the-working-with-batched-data-web-pages"></a>Krok 1: vytvoření práce s webovými stránkami dávková data

Předtím, než začneme zkoumat, jak rozšířit DAL na podporu databázových transakcí, si nejdřív chvíli počkejte, než se vytvoří webové stránky ASP.NET, které budeme potřebovat pro tento kurz a tři kroky. Začněte přidáním nové složky s názvem `BatchData` a pak přidejte následující stránky ASP.NET a přiřadíte každou stránku k `Site.master` stránce předlohy.

- `Default.aspx`
- `Transactions.aspx`
- `BatchUpdate.aspx`
- `BatchDelete.aspx`
- `BatchInsert.aspx`

![Přidání stránek ASP.NET pro kurzy týkající se SqlDataSource](wrapping-database-modifications-within-a-transaction-vb/_static/image1.gif)

**Obrázek 1**: přidání stránek ASP.NET pro kurzy týkající se SqlDataSource

Stejně jako u ostatních složek `Default.aspx` použije uživatelský ovládací prvek `SectionLevelTutorialListing.ascx` k vypsání kurzů v rámci své části. Proto tento uživatelský ovládací prvek přidejte do `Default.aspx` tím, že ho přetáhnete z Průzkumník řešení na zobrazení Návrh stránky.

[![přidat uživatelský ovládací prvek SectionLevelTutorialListing. ascx do default. aspx](wrapping-database-modifications-within-a-transaction-vb/_static/image2.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image1.png)

**Obrázek 2**: Přidání uživatelského ovládacího prvku `SectionLevelTutorialListing.ascx` do `Default.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](wrapping-database-modifications-within-a-transaction-vb/_static/image2.png))

Nakonec tyto čtyři stránky přidejte jako položky do souboru `Web.sitemap`. Konkrétně přidejte následující značky po přizpůsobení mapy webu `<siteMapNode>`:

[!code-xml[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample2.xml)]

Po aktualizaci `Web.sitemap`chvíli počkejte, než se zobrazí web kurzy prostřednictvím prohlížeče. Nabídka na levé straně teď obsahuje položky pro práci s kurzy dat v dávce.

![Mapa webu teď obsahuje položky pro práci s kurzy dat v dávce.](wrapping-database-modifications-within-a-transaction-vb/_static/image3.gif)

**Obrázek 3**: Mapa webu teď obsahuje položky pro práci s kurzy dat v dávce.

## <a name="step-2-updating-the-data-access-layer-to-support-database-transactions"></a>Krok 2: aktualizace vrstvy přístupu k datům pro podporu databázových transakcí

Jak jsme probrali zpět v prvním kurzu, [Vytvoření vrstvy přístupu k datům](../introduction/creating-a-data-access-layer-vb.md), zadaná datová sada v naší dál se skládá z datových tabulek a objekty TableAdapter. Datové tabulky uchovávají data, zatímco objekty TableAdapter poskytuje funkce pro čtení dat z databáze do datových tabulek, k aktualizaci databáze se změnami provedenými v datových tabulkách a tak dále. Odvoláte si, že objekty TableAdapter poskytuje dva vzory pro aktualizaci dat, které se označují jako dávkové aktualizace a DB-Direct. Se vzorem aktualizace pro dávku je TableAdapter předán objekt DataSet, DataTable nebo kolekce datových řádků. Tato data jsou vyčíslovaná a pro každý vložený, změněný nebo odstraněný řádek, `InsertCommand`, `UpdateCommand`nebo `DeleteCommand`. Pomocí vzoru DB-Direct je TableAdapter místo toho předán hodnot sloupců potřebných pro vložení, aktualizaci nebo odstranění jednoho záznamu. Metoda přímého vzoru DB pak pomocí těchto předaných hodnot provede příslušný `InsertCommand`, `UpdateCommand`nebo příkaz `DeleteCommand`.

Bez ohledu na použitý vzor aktualizace nepoužívají automaticky generované metody objekty TableAdapter transakce. Ve výchozím nastavení se každé vložení, aktualizace nebo odstranění prováděné TableAdapter považuje za jednu diskrétní operaci. Představte si například, že vzor DB-Direct je použit nějakým kódem v knihoven BLL k vložení deseti záznamů do databáze. Tento kód by volal metodu TableAdapter s `Insert` desetkrát. Pokud je první pět vložení úspěšné, ale šestá z nich způsobila výjimku, prvních pět vložených záznamů by v databázi zůstalo. Podobně platí, že pokud se vzor aktualizace dávky používá k provádění vložení, aktualizace a odstranění řádků vložených, upravených a odstraněných v objektu DataTable, pokud bylo prvních několik změn úspěšné, ale později v nich došlo k chybě, tyto dřívější úpravy dokončeno by zůstalo v databázi.

V některých scénářích chceme zajistit nedělitelnost v rámci řady úprav. Aby bylo možné tento postup provést, je nutné ručně rozšíření TableAdapter přidáním nových metod, které spouštějí `InsertCommand`, `UpdateCommand`a `DeleteCommand` s v rámci transakce. Při [vytváření vrstvy přístupu k datům](../introduction/creating-a-data-access-layer-vb.md) jsme prohlédli pomocí [částečných tříd](http://en.wikipedia.org/wiki/Partial_type) a rozšířili jsme funkce datových tabulek v rámci typové datové sady. Tento postup lze také použít s objekty TableAdapter.

Zadaná datová sada `Northwind.xsd` je umístěná v podsložce `App_Code` složky s `DAL`. Vytvořte podsložku ve složce `DAL` s názvem `TransactionSupport` a přidejte nový soubor třídy s názvem `ProductsTableAdapter.TransactionSupport.vb` (viz obrázek 4). Tento soubor bude obsahovat částečnou implementaci `ProductsTableAdapter`, která obsahuje metody pro provádění úprav dat pomocí transakce.

![Přidejte složku s názvem TransactionSupport a soubor třídy s názvem ProductsTableAdapter. TransactionSupport. vb.](wrapping-database-modifications-within-a-transaction-vb/_static/image4.gif)

**Obrázek 4**: přidejte složku s názvem `TransactionSupport` a soubor třídy s názvem `ProductsTableAdapter.TransactionSupport.vb`

Do souboru `ProductsTableAdapter.TransactionSupport.vb` zadejte následující kód:

[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample3.vb)]

Klíčové slovo `Partial` v deklaraci třídy zde označuje kompilátor, že členy přidané v rámci mají být přidány do `ProductsTableAdapter` třídy v oboru názvů `NorthwindTableAdapters`. Všimněte si příkazu `Imports System.Data.SqlClient` v horní části souboru. Vzhledem k tomu, že služba TableAdapter byla nakonfigurovaná tak, aby používala poskytovatele SqlClient, interně použije objekt [`SqlDataAdapter`](https://msdn.microsoft.com/library/system.data.sqlclient.sqldataadapter.aspx) k vystavení příkazů do databáze. V důsledku toho je potřeba použít třídu `SqlTransaction` k zahájení transakce a pak ji potvrdit nebo vrátit zpět. Pokud používáte jiné úložiště dat než Microsoft SQL Server, bude nutné použít příslušného poskytovatele.

Tyto metody poskytují stavební bloky potřebné ke spuštění, vrácení zpět a potvrzení transakce. Jsou označeny `Public`a umožňují jejich použití v rámci `ProductsTableAdapter`, z jiné třídy v DAL nebo z jiné vrstvy v architektuře, jako je například knihoven BLL. `BeginTransaction` otevře interní `SqlConnection` TableAdapter s (v případě potřeby), zahájí transakci a přiřadí ji k vlastnosti `Transaction` a připojí transakci k interním objektům `SqlCommand` `SqlDataAdapter` s. `CommitTransaction` a `RollbackTransaction` před zavřením interního objektu `Rollback` zavolá `Transaction` Object s `Commit` a `Connection` metody.

## <a name="step-3-adding-methods-to-update-and-delete-data-under-the-umbrella-of-a-transaction"></a>Krok 3: Přidání metod, které aktualizují a odstraňují data v zastřešující transakci

Po dokončení těchto metod jsme znovu připraveni přidat metody do `ProductsDataTable` nebo knihoven BLL, které provádějí řadu příkazů v rámci transakce. Následující metoda používá vzor aktualizace Batch k aktualizaci instance `ProductsDataTable` pomocí transakce. Spustí transakci voláním metody `BeginTransaction` a poté pomocí bloku `Try...Catch` vystaví příkazy pro úpravu dat. Pokud volání metody `Adapter` objektů `Update` má za následek výjimku, provádění se převede na blok `catch`, kde transakce bude vrácena zpět a výjimka se znovu vyvolala. Vyvoláním metody `Update` implementuje vzor aktualizace dávky vytvořením výčtu řádků zadaného `ProductsDataTable` a provedením potřebných `InsertCommand`, `UpdateCommand`a `DeleteCommand` s. Pokud některý z těchto příkazů způsobí chybu, transakce se vrátí zpět a vrátí zpět předchozí změny provedené během doby platnosti transakce. Pokud by byl příkaz `Update` dokončen bez chyby, transakce je zapsána v celém rozsahu.

[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample4.vb)]

Přidejte metodu `UpdateWithTransaction` do `ProductsTableAdapter` třídy prostřednictvím částečné třídy v `ProductsTableAdapter.TransactionSupport.vb`. Alternativně lze tuto metodu přidat do třídy `ProductsBLL` vrstvy obchodní logiky s několika vedlejšími syntaktickými změnami. Klíčové slovo `Me` v `Me.BeginTransaction()`, `Me.CommitTransaction()`a `Me.RollbackTransaction()` by proto muselo být nahrazeno `Adapter` (odvolání `Adapter` je název vlastnosti v `ProductsBLL` typu `ProductsTableAdapter`).

Metoda `UpdateWithTransaction` používá vzor aktualizace služby Batch, ale v rámci rozsahu transakce lze také použít řadu volání DB-Direct, jak ukazuje následující metoda. Metoda `DeleteProductsWithTransaction` přijímá jako vstup `List(Of T)` typu `Integer`, což jsou `ProductID` s pro odstranění. Metoda inicializuje transakci prostřednictvím volání `BeginTransaction` a poté v bloku `Try` prochází dodaným seznamem voláním metody `Delete` vzoru DB-Direct pro každou `ProductID` hodnotu. Pokud některá z volání `Delete` selžou, řízení je převedeno do `Catch` bloku, kde transakce je vrácena zpět a výjimka je znovu vyvolána. Pokud všechna volání `Delete` úspěšná, transakce je potvrzena. Přidejte tuto metodu do třídy `ProductsBLL`.

[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample5.vb)]

## <a name="applying-transactions-across-multiple-tableadapters"></a>Použití transakcí napříč několika objekty TableAdapter

Kód, který je v tomto kurzu přezkoumán, umožňuje, aby bylo více příkazů na `ProductsTableAdapter` považováno za atomickou operaci. Ale co dělat v případě, že je potřeba provést nedělitelnost více změn v různých databázových tabulkách? Například při odstraňování kategorie můžeme nejdřív chtít změnit přiřazení aktuálních produktů k jiné kategorii. Tyto dva kroky mění přiřazení produktů a odstraňování kategorie by se měly provádět jako atomická operace. `ProductsTableAdapter` však obsahují pouze metody pro úpravu tabulky `Products` a `CategoriesTableAdapter` obsahuje pouze metody pro úpravu tabulky `Categories`. Jak může transakce zahrnovat jak objekty TableAdapter?

Jednou z možností je přidat metodu do `CategoriesTableAdapter` s názvem `DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)` a tato metoda volá uloženou proceduru, která znovu přiřadí produkty a odstraní kategorii v rámci oboru transakce definované v rámci uložené procedury. V budoucím kurzu se podíváme na to, jak začít, potvrzovat a vrátit zpátky transakce v uložených procedurách.

Další možností je vytvořit pomocnou třídu v rámci DAL, která obsahuje metodu `DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)`. Tato metoda vytvoří instanci `CategoriesTableAdapter` a `ProductsTableAdapter` a poté nastaví tyto dvě vlastnosti objekty TableAdapter `Connection` na stejnou instanci `SqlConnection`. V tomto okamžiku buď jedna ze dvou objekty TableAdapter zahájí transakci se voláním `BeginTransaction`. Metody objekty TableAdapter pro opětovné přiřazení produktů a odstraňování kategorie by se vyvolaly v `Try...Catch`ovém bloku s transakcí potvrzenou nebo vrácenou zpět podle potřeby.

## <a name="step-4-adding-theupdatewithtransactionmethod-to-the-business-logic-layer"></a>Krok 4: Přidání metody`UpdateWithTransaction`do vrstvy obchodní logiky

V kroku 3 jsme do `ProductsTableAdapter` do DAL přidali metodu `UpdateWithTransaction`. Do knihoven BLL bychom měli přidat odpovídající metodu. Zatímco prezentační vrstva může zavolat přímo dolů na DAL k vyvolání metody `UpdateWithTransaction`, tyto kurzy se snaží definovat vrstvenou architekturu, která z prezentační vrstvy izolaci DAL. Proto behooves nás, abychom mohli pokračovat v tomto přístupu.

Otevřete soubor `ProductsBLL` třídy a přidejte metodu nazvanou `UpdateWithTransaction`, která jednoduše zavolá do odpovídající metody DAL. V `ProductsBLL`by teď měly být dvě nové metody: `UpdateWithTransaction`, které jste právě přidali, a `DeleteProductsWithTransaction`, které jste přidali v kroku 3.

[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample6.vb)]

> [!NOTE]
> Tyto metody neobsahují atribut `DataObjectMethodAttribute` přiřazený většině jiných metod v `ProductsBLL` třídě, protože budeme vydávat tyto metody přímo ze tříd kódu na pozadí ASP.NET stránek. Odvolání tohoto `DataObjectMethodAttribute` slouží k označení toho, jaké metody se mají zobrazit v průvodci ObjectDataSource s konfigurací zdroje dat, a v části jakou kartu (výběr, aktualizace, vložení nebo odstranění). Vzhledem k tomu, že v prvku GridView chybí integrovaná podpora pro dávkové úpravy nebo odstranění, bude nutné tyto metody vyvolat programově namísto použití deklarativního přístupu bez kódu.

## <a name="step-5-atomically-updating-database-data-from-the-presentation-layer"></a>Krok 5: atomická aktualizace databázových dat z prezentační vrstvy

Pro ilustraci účinku, který má transakce při aktualizaci dávky záznamů, vytvoříme uživatelské rozhraní, které obsahuje seznam všech produktů v prvku GridView a obsahuje ovládací prvek web Button, který po kliknutí znovu přiřadí produkty `CategoryID` hodnoty. Konkrétně bude postup opětovného přiřazení kategorie mít za následek, že prvnímu z těchto produktů je přiřazena platná `CategoryID` hodnota, zatímco ostatní jsou záměrně přiřazeny neexistující `CategoryID` hodnotě. Pokud se pokusíme aktualizovat databázi s produktem, jehož `CategoryID` se neshoduje s `CategoryID`existující kategorie, dojde k porušení omezení cizího klíče a vyvolá se výjimka. V tomto příkladu se dozvíte, že při použití transakce výjimka vyvolaná z porušení omezení cizího klíče způsobí, že se předchozí platná `CategoryID` změny vrátí zpátky. Pokud se však transakce nepoužívá, změny původních kategorií zůstanou.

Začněte otevřením stránky `Transactions.aspx` ve složce `BatchData` a přetažením prvku GridView z panelu nástrojů do návrháře. Nastavte jeho `ID` na `Products` a ze své inteligentní značky ho navažte na nový prvek ObjectDataSource s názvem `ProductsDataSource`. Nakonfigurujte prvek ObjectDataSource tak, aby vyčetl data z `ProductsBLL` třídy s `GetProducts` metody. Toto bude prvek GridView, který je jen pro čtení, proto nastavte rozevírací seznamy na kartách aktualizace, vložení a odstranění na hodnotu (žádné) a klikněte na tlačítko Dokončit.

[![nakonfigurovat prvek ObjectDataSource tak, aby používal metodu ProductsBLL třídy s GetProducts](wrapping-database-modifications-within-a-transaction-vb/_static/image5.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image3.png)

**Obrázek 5**: Konfigurace prvku ObjectDataSource pro použití `GetProducts` metody `ProductsBLL` třídy s ([kliknutím zobrazíte obrázek v plné velikosti](wrapping-database-modifications-within-a-transaction-vb/_static/image4.png))

[![nastavení rozevíracích seznamů na kartách aktualizace, vložení a odstranění na (žádné)](wrapping-database-modifications-within-a-transaction-vb/_static/image6.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image5.png)

**Obrázek 6**: nastavení rozevíracích seznamů na kartách aktualizace, vložení a odstranění na (žádné) ([kliknutím zobrazíte obrázek v plné velikosti](wrapping-database-modifications-within-a-transaction-vb/_static/image6.png))

Po dokončení Průvodce konfigurací zdroje dat vytvoří Visual Studio BoundFields a třídě CheckBoxField podporována pro pole dat produktu. Odeberte všechna tato pole s výjimkou `ProductID`, `ProductName`, `CategoryID`a `CategoryName` a přejmenujte `ProductName` `CategoryName` `HeaderText` vlastností na produkt a kategorii v uvedeném pořadí. Z inteligentní značky zaškrtněte možnost Povolit stránkování. Po provedení těchto úprav by deklarativní označení GridView a ObjectDataSource s mělo vypadat takto:

[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample7.aspx)]

Dále přidejte tři webové ovládací prvky tlačítka nad ovládací prvek GridView. Nastavte vlastnost text prvního tlačítka na aktualizovat mřížku, druhé s pro úpravu kategorií (s transakcí) a třetí jednu pro úpravu kategorií (bez transakcí).

[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample8.aspx)]

V tomto okamžiku by zobrazení Návrh v aplikaci Visual Studio mělo vypadat podobně jako snímek obrazovky, který je znázorněn na obrázku 7.

[![stránka obsahuje ovládací prvky GridView a tři tlačítka webu](wrapping-database-modifications-within-a-transaction-vb/_static/image7.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image7.png)

**Obrázek 7**: stránka obsahuje ovládací prvky GridView a tři tlačítka webu ([kliknutím zobrazíte obrázek v plné velikosti](wrapping-database-modifications-within-a-transaction-vb/_static/image8.png)).

Vytvořte obslužné rutiny událostí pro každé tři tlačítko s `Click` událostí a použijte následující kód:

[!code-vb[Main](wrapping-database-modifications-within-a-transaction-vb/samples/sample9.vb)]

Obslužná rutina události `Click` tlačítky aktualizovat jednoduše znovu naváže data na prvek GridView voláním metody `Products` GridView. `DataBind`.

Druhá obslužná rutina události znovu přiřadí produkty `CategoryID` s a používá novou metodu transakce z knihoven BLL k provedení aktualizací databáze za zastřešujícím v rámci transakce. Všimněte si, že každý `CategoryID` produktů je libovolně nastavený na stejnou hodnotu jako jeho `ProductID`. Tato operace bude pro prvních několik produktů fungovat správně, protože tyto produkty mají `ProductID` hodnoty, které se namapují na platné `CategoryID` s. Když ale `ProductID` s začne hodně velká, tento překrytí `ProductID` s a `CategoryID` se už nepoužijí.

Třetí `Click` obslužná rutina události aktualizuje produkty `CategoryID` stejným způsobem, ale odešle aktualizaci do databáze pomocí výchozí `Update` metody `ProductsTableAdapter` s. Tato `Update` metoda nezalomí řadu příkazů v rámci transakce, takže tyto změny jsou provedeny před prvním zjištěným chybou porušení omezení cizího klíče.

Pokud chcete toto chování předvést, navštivte tuto stránku v prohlížeči. Zpočátku byste měli vidět první stránku dat, jak je znázorněno na obrázku 8. Potom klikněte na tlačítko upravit kategorie (s transakcí). Tím dojde k provedení zpětného volání a pokusu o aktualizaci všech produktů `CategoryID` hodnoty, ale výsledkem bude porušení omezení cizího klíče (viz obrázek 9).

[![se produkty zobrazují ve stránkovém prvku GridView](wrapping-database-modifications-within-a-transaction-vb/_static/image8.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image9.png)

**Obrázek 8**: produkty se zobrazují ve stránkovém prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](wrapping-database-modifications-within-a-transaction-vb/_static/image10.png)).

[![Změna přiřazení kategorií má za následek porušení omezení cizího klíče](wrapping-database-modifications-within-a-transaction-vb/_static/image9.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image11.png)

**Obrázek 9**: Změna přiřazení kategorií má za následek porušení omezení cizího klíče ([kliknutím zobrazíte obrázek v plné velikosti).](wrapping-database-modifications-within-a-transaction-vb/_static/image12.png)

Nyní stiskněte tlačítko zpět v prohlížeči a potom klikněte na tlačítko Obnovit mřížku. Po aktualizaci dat byste měli vidět přesný stejný výstup, jak je znázorněno na obrázku 8. To znamená, že i když byly některé z produktů `CategoryID` změněny na platné hodnoty a aktualizovány v databázi, byly vráceny zpět v případě, že došlo k porušení omezení cizího klíče.

Nyní zkuste kliknout na tlačítko upravit kategorie (bez transakce). Výsledkem bude stejná chyba při porušení omezení cizího klíče (viz obrázek 9), ale tentokrát se tyto produkty, jejichž hodnoty `CategoryID` změnily na platnou hodnotu, nevrátí zpět. Stiskněte tlačítko zpět v prohlížeči a pak klikněte na tlačítko Obnovit mřížku. Jak ukazuje obrázek 10, `CategoryID` s prvních osm produkty byly znovu přiřazeny. Například na obrázku 8 má změn `CategoryID` hodnotu 1, ale na obrázku 10 bylo přiřazeno 2.

[![některé produkty v hodnotách KódKategorie byly aktualizovány, zatímco jiné nebyly](wrapping-database-modifications-within-a-transaction-vb/_static/image10.gif)](wrapping-database-modifications-within-a-transaction-vb/_static/image13.png)

**Obrázek 10**: některé produkty `CategoryID` hodnoty byly aktualizovány, i když jiné nebyly ([kliknutím zobrazíte obrázek v plné velikosti).](wrapping-database-modifications-within-a-transaction-vb/_static/image14.png)

## <a name="summary"></a>Přehled

Ve výchozím nastavení metody TableAdapter s nebalí provedené příkazy databáze v rámci oboru transakce, ale s malým množstvím práce můžeme přidat metody, které vytvoří, potvrdí a vrátí zpět transakci. V tomto kurzu jsme vytvořili tři takové metody ve třídě `ProductsTableAdapter`: `BeginTransaction`, `CommitTransaction`a `RollbackTransaction`. Zjistili jsme, jak tyto metody použít spolu s blokem `Try...Catch` a vytvořit tak řadu příkazů pro úpravu dat. Konkrétně jsme vytvořili metodu `UpdateWithTransaction` v `ProductsTableAdapter`, která používá vzor aktualizace Batch k provedení nezbytných úprav řádků zadaného `ProductsDataTable`. Přidali jsme také metodu `DeleteProductsWithTransaction` do `ProductsBLL` třídy v knihoven BLL, která přijímá `List` `ProductID` hodnot jako svůj vstup a volá metodu vzoru DB-Direct `Delete` pro každý `ProductID`. Obě metody se spustí vytvořením transakce a následným spuštěním příkazů pro úpravu dat v rámci `Try...Catch`ho bloku. Pokud dojde k výjimce, transakce je vrácena zpět, jinak je potvrzena.

Krok 5 ilustruje účinek transakčních aktualizací dávek a aktualizací dávek, které opomíjeny použít transakci. V následujících třech kurzech vytvoříme základ uvedený v tomto kurzu a vytvoříme uživatelská rozhraní pro provádění aktualizací dávek, odstraňování a vkládání.

Šťastné programování!

## <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Údržba konzistence databáze s transakcemi](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx)
- [Správa transakcí v uložených procedurách SQL Server](http://www.4guysfromrolla.com/webtech/080305-1.shtml)
- [Jednoduché transakce: `System.Transactions`](https://blogs.msdn.com/florinlazar/archive/2004/07/23/192239.aspx)
- [Objekt TransactionScope a dataadaptéry](http://andyclymer.blogspot.com/2007/01/transactionscope-and-dataadapters.html)
- [Používání transakcí Oracle Database v .NET](http://www.oracle.com/technology/pub/articles/price_dbtrans_dotnet.html)

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Dave Gardner, Hilton Giesenow a Teresa Murphy. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](batch-inserting-cs.md)
> [Další](batch-updating-vb.md)

---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-vb
title: Přidání dalších sloupců DataTable (VB) | Microsoft Docs
author: rick-anderson
description: Když pomocí Průvodce TableAdapter vytvoříte typovou datovou sadu, odpovídající objekt DataTable obsahuje sloupce vracené hlavním databázovým dotazem. Ale existuje...
ms.author: riande
ms.date: 07/18/2007
ms.assetid: 1e8e65f9-fe3e-4250-810b-c90227786bed
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/adding-additional-datatable-columns-vb
msc.type: authoredcontent
ms.openlocfilehash: 3a55f8bc4d3508387927ca81674073a001867de7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78534102"
---
# <a name="adding-additional-datatable-columns-vb"></a>Přidání dalších sloupců do tabulky DataTable (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_70_VB.zip) nebo [stažení PDF](adding-additional-datatable-columns-vb/_static/datatutorial70vb1.pdf)

> Když pomocí Průvodce TableAdapter vytvoříte typovou datovou sadu, odpovídající objekt DataTable obsahuje sloupce vracené hlavním databázovým dotazem. Existují však situace, kdy objekt DataTable musí zahrnovat další sloupce. V tomto kurzu se dozvíte, proč se doporučuje ukládání uložených procedur, když potřebujeme další sloupce DataTable.

## <a name="introduction"></a>Úvod

Při přidávání TableAdapter do typové datové sady je odpovídající schéma DataTable s určeno hlavním dotazem TableAdapter s. Například pokud hlavní dotaz vrátí datová pole *a*, *b*a *c*, bude mít DataTable tři odpovídající sloupce s názvem *a*, *b*a *c*. Kromě hlavního dotazu může TableAdapter zahrnovat další dotazy, které vracejí, případně i podmnožinu dat na základě některého parametru. Například kromě hlavního dotazu `ProductsTableAdapter` s, který vrací informace o všech produktech, obsahuje také metody jako `GetProductsByCategoryID(categoryID)` a `GetProductByProductID(productID)`, které vracejí konkrétní informace o produktu na základě zadaného parametru.

Model, ve kterém je schéma DataTable, odráží hlavní dotaz TableAdapter s, pokud všechny metody TableAdaptery vrátí stejné nebo méně datových polí, než jsou zadaná v hlavním dotazu. Pokud metoda TableAdapter potřebuje vrátit další datová pole, měli bychom odpovídajícím způsobem rozbalovat schéma DataTable s. V [seznamu a podrobnostech pomocí seznamu hlavních záznamů s odrážkami s kurzem podrobností DataList](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md) jsme přidali metodu do `CategoriesTableAdapter`, která vrátila datová pole `CategoryID`, `CategoryName`a `Description` definovaná v hlavním dotazu a `NumberOfProducts`, další datové pole, které oznámilo počet produktů přidružených ke každé kategorii. Ručně jsme do `CategoriesDataTable` přidali nový sloupec, aby se z této nové metody zachytí hodnota datového pole `NumberOfProducts`.

Jak je popsáno v kurzu [nahrávání souborů](../working-with-binary-files/uploading-files-vb.md) , je potřeba věnovat velkou péči s objekty TableAdapter, které používají příkazy SQL ad hoc, a mají metody, jejichž datová pole neodpovídají přesně hlavnímu dotazu. Pokud se Průvodce konfigurací TableAdapter znovu spustí, aktualizuje všechny metody TableAdapter s tak, aby se jejich seznam datových polí shodoval s hlavním dotazem. V důsledku toho se všechny metody s přizpůsobenými seznamy sloupců vrátí do seznamu sloupců hlavní dotaz s a nevrátí očekávaná data. Tento problém se neprojeví při použití uložených procedur.

V tomto kurzu se podíváme na to, jak rozšíříte schéma DataTable s, aby zahrnovalo další sloupce. V tomto kurzu použijeme k tomu, aby se brittlenessy TableAdapter při použití příkazů SQL ad hoc. v tomto kurzu budeme používat uložené procedury. Další informace o konfiguraci TableAdapter pro použití uložených procedur najdete v tématu [vytváření nových uložených procedur pro typovou sadu dat s objekty TableAdapter](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) a [použití existujících uložených procedur pro kurzy typované sady dat s objekty TableAdapter](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) .

## <a name="step-1-adding-apricequartilecolumn-to-theproductsdatatable"></a>Krok 1: Přidání sloupce`PriceQuartile`do`ProductsDataTable`

V kurzu *vytváření nových uložených procedur pro typovou datovou sadu s objekty TableAdapter* jsme vytvořili typovou datovou sadu s názvem `NorthwindWithSprocs`. Tato datová sada aktuálně obsahuje dvě datové tabulky: `ProductsDataTable` a `EmployeesDataTable`. `ProductsTableAdapter` má následující tři metody:

- `GetProducts` – hlavní dotaz, který vrátí všechny záznamy z tabulky `Products`
- `GetProductsByCategoryID(categoryID)` – vrátí všechny produkty se zadaným *KódKategorie*.
- `GetProductByProductID(productID)` – vrátí konkrétní produkt se zadaným *ProductID*.

Hlavní dotaz a dvě další metody vrací stejnou sadu datových polí, konkrétně všechny sloupce z `Products` tabulky. Neexistují žádné korelační poddotazy nebo `JOIN` s přijímáním souvisejících dat z tabulek `Categories` nebo `Suppliers`. Proto má `ProductsDataTable` odpovídající sloupec pro každé pole v tabulce `Products`.

Pro účely tohoto kurzu přidejte do `ProductsTableAdapter` s názvem `GetProductsWithPriceQuartile` metodu, která vrátí všechny produkty. Kromě standardních datových polí produktu bude `GetProductsWithPriceQuartile` také obsahovat `PriceQuartile` datové pole, které indikuje, že funkce QUARTIL ceny produktů spadá do rozsahu. Například u produktů, jejichž ceny jsou v nejdražším 25%, bude mít `PriceQuartile` hodnotu 1, zatímco ceny, jejichž ceny spadají do 25% nejnižší ceny, budou mít hodnotu 4. Než se obáváme, jak vytvořit uloženou proceduru, aby se tyto informace vracely, nejdřív je potřeba aktualizovat `ProductsDataTable` tak, aby obsahovala sloupec, který bude obsahovat výsledky `PriceQuartile` při použití `GetProductsWithPriceQuartile` metody.

Otevřete `NorthwindWithSprocs` datovou sadu a klikněte pravým tlačítkem na `ProductsDataTable`. V kontextové nabídce zvolte Přidat a pak vyberte sloupec.

[![přidat nový sloupec do ProductsDataTable](adding-additional-datatable-columns-vb/_static/image2.png)](adding-additional-datatable-columns-vb/_static/image1.png)

**Obrázek 1**: Přidání nového sloupce do `ProductsDataTable` ([kliknutím zobrazíte obrázek v plné velikosti](adding-additional-datatable-columns-vb/_static/image3.png))

Tím se přidá nový sloupec do objektu DataTable s názvem Sloupe typu `System.String`. Musíme tento název sloupce aktualizovat tak, aby PriceQuartile a jeho typ `System.Int32`, protože se použije k uložení čísla mezi 1 a 4. Vyberte nově přidaný sloupec v `ProductsDataTable` a z okno Vlastnosti nastavte vlastnost `Name` na hodnotu PriceQuartile a vlastnost `DataType` na `System.Int32`.

[![nastavit nové vlastnosti název sloupce a datového typu.](adding-additional-datatable-columns-vb/_static/image5.png)](adding-additional-datatable-columns-vb/_static/image4.png)

**Obrázek 2**: nastavení nových `Name` sloupců a vlastností `DataType` ([kliknutím zobrazíte obrázek v plné velikosti](adding-additional-datatable-columns-vb/_static/image6.png))

Jak ukazuje obrázek 2, existují další vlastnosti, které lze nastavit, například zda musí být hodnoty ve sloupci jedinečné, pokud se jedná o sloupec s automatickým přírůstem, bez ohledu na to, zda jsou povoleny hodnoty `NULL` databáze a tak dále. Ponechte tyto hodnoty nastavené na výchozí hodnoty.

## <a name="step-2-creating-thegetproductswithpricequartilemethod"></a>Krok 2: vytvoření metody`GetProductsWithPriceQuartile`

Teď, když se `ProductsDataTable` aktualizovala tak, aby obsahovala `PriceQuartile` sloupec, jsme připraveni vytvořit metodu `GetProductsWithPriceQuartile`. Začněte tím, že kliknete pravým tlačítkem na TableAdapter a zvolíte přidat dotaz z kontextové nabídky. Tím se zobrazí Průvodce konfigurací dotazu TableAdapter, který vás nejdřív vyzve k tomu, jestli chceme použít příkazy SQL ad hoc nebo novou nebo existující uloženou proceduru. Vzhledem k tomu, že ještě nemáme uloženou proceduru, která vrací data o nákladech, umožňují TableAdapter vytvořit tuto uloženou proceduru pro nás. Vyberte možnost vytvořit novou uloženou proceduru a klikněte na tlačítko Další.

[![instruuje Průvodce TableAdapter, aby vytvořil uloženou proceduru pro nás.](adding-additional-datatable-columns-vb/_static/image8.png)](adding-additional-datatable-columns-vb/_static/image7.png)

**Obrázek 3**: Řekněte průvodci TableAdapter, aby vytvořil uloženou proceduru pro nás ([kliknutím zobrazíte obrázek v plné velikosti).](adding-additional-datatable-columns-vb/_static/image9.png)

Na další obrazovce zobrazené na obrázku 4 Průvodce požádá o typ dotazu, který se má přidat. Vzhledem k tomu, že metoda `GetProductsWithPriceQuartile` vrátí všechny sloupce a záznamy z tabulky `Products`, vyberte možnost vybrat, které vrací řádky, a klikněte na tlačítko Další.

[![náš dotaz bude příkaz SELECT, který vrátí více řádků.](adding-additional-datatable-columns-vb/_static/image11.png)](adding-additional-datatable-columns-vb/_static/image10.png)

**Obrázek 4**: náš dotaz bude příkaz `SELECT`, který vrací více řádků ([kliknutím zobrazíte obrázek v plné velikosti).](adding-additional-datatable-columns-vb/_static/image12.png)

V dalším kroku se zobrazí výzva k zadání dotazu na `SELECT`. Do průvodce zadejte následující dotaz:

[!code-sql[Main](adding-additional-datatable-columns-vb/samples/sample1.sql)]

Výše uvedený dotaz využije SQL Server 2005 s nové [funkce`NTILE`](https://msdn.microsoft.com/library/ms175126.aspx) k rozdělení výsledků do čtyř skupin, kde jsou skupiny určeny hodnotami `UnitPrice` seřazenými v sestupném pořadí.

Tvůrce dotazů bohužel neví, jak analyzovat klíčové slovo `OVER` a zobrazí při analýze výše uvedeného dotazu chybu. Proto zadejte výše uvedený dotaz přímo do textového pole v průvodci bez použití Tvůrce dotazů.

> [!NOTE]
> Další informace o dalších funkcích hodnocení NTILE a SQL Server 2005 s najdete v tématu věnovaném [vrácení seřazených výsledků pomocí Microsoft SQL Server 2005](http://www.4guysfromrolla.com/webtech/010406-1.shtml) a [oddílu funkcí hodnocení](https://msdn.microsoft.com/library/ms189798.aspx) [2005 SQL Server Knihy online](https://msdn.microsoft.com/library/ms189798.aspx).

Po zadání `SELECT` dotazu a kliknutí na tlačítko Další vás průvodce vyzve k zadání názvu pro uloženou proceduru, kterou vytvoří. Pojmenujte novou uloženou proceduru `Products_SelectWithPriceQuartile` a klikněte na tlačítko Další.

[![uloženou proceduru pojmenovat Products_SelectWithPriceQuartile](adding-additional-datatable-columns-vb/_static/image14.png)](adding-additional-datatable-columns-vb/_static/image13.png)

**Obrázek 5**: pojmenujte uloženou proceduru `Products_SelectWithPriceQuartile` ([kliknutím zobrazíte obrázek v plné velikosti).](adding-additional-datatable-columns-vb/_static/image15.png)

Nakonec se zobrazí výzva k pojmenování metod TableAdapter. Ponechte naplnit objekt DataTable a vraťte zaškrtávací políčka DataTable a pojmenujte metody `FillWithPriceQuartile` a `GetProductsWithPriceQuartile`.

[![pojmenovat metody TableAdapter a klikněte na Dokončit.](adding-additional-datatable-columns-vb/_static/image17.png)](adding-additional-datatable-columns-vb/_static/image16.png)

**Obrázek 6**: pojmenujte metody TableAdapter s a klikněte na Dokončit ([kliknutím zobrazíte obrázek v plné velikosti).](adding-additional-datatable-columns-vb/_static/image18.png)

Když je zadaný dotaz `SELECT` a metody uložené procedury a TableAdapter s názvem, kliknutím na Dokončit dokončete průvodce. V tomto okamžiku se vám může zobrazit upozornění nebo dva z nich, že `OVER` konstrukce nebo příkaz jazyka SQL není podporován. Tato upozornění je možné ignorovat.

Po dokončení průvodce by měl TableAdapter zahrnovat metody `FillWithPriceQuartile` a `GetProductsWithPriceQuartile` a databáze by měla obsahovat uloženou proceduru s názvem `Products_SelectWithPriceQuartile`. Chvíli počkejte, než ověříte, že TableAdapter skutečně obsahuje tuto novou metodu a že uložená procedura byla správně přidána do databáze. Pokud nevidíte uloženou proceduru v databázi, klikněte pravým tlačítkem na složku uložené procedury a zvolte možnost aktualizovat.

![Ověřte, že se do TableAdapter přidala nová metoda.](adding-additional-datatable-columns-vb/_static/image19.png)

**Obrázek 7**: ověření, zda byla do TableAdapter přidána nová metoda

[![zajistěte, aby databáze obsahovala uloženou proceduru Products_SelectWithPriceQuartile](adding-additional-datatable-columns-vb/_static/image21.png)](adding-additional-datatable-columns-vb/_static/image20.png)

**Obrázek 8**: Ujistěte se, že databáze obsahuje `Products_SelectWithPriceQuartile` uloženou proceduru ([kliknutím zobrazíte obrázek v plné velikosti).](adding-additional-datatable-columns-vb/_static/image22.png)

> [!NOTE]
> Jednou z výhod použití uložených procedur místo ad-hoc příkazů SQL je, že opětovné spuštění Průvodce konfigurací TableAdapter neupraví seznam sloupců uložených procedur. Ověřte to tak, že kliknete pravým tlačítkem na TableAdapter, zvolíte možnost konfigurace z kontextové nabídky a spustíte průvodce a pak kliknutím na Dokončit dokončete jeho dokončení. V dalším kroku přejdete do databáze a zobrazíte uloženou proceduru `Products_SelectWithPriceQuartile`. Všimněte si, že se seznam sloupců nezměnil. Používali jsme příkazy SQL ad hoc, ale opětovné spuštění Průvodce konfigurací TableAdapter by vrátilo tento seznam sloupců dotazu s dotazem na hlavní seznam sloupců dotazu, čímž se odstraní příkaz NTILE z dotazu, který používá metoda `GetProductsWithPriceQuartile`.

Při vyvolání metody Data Access Layer s `GetProductsWithPriceQuartile` spustí TableAdapter `Products_SelectWithPriceQuartile` uloženou proceduru a přidá řádek do `ProductsDataTable` pro každý vrácený záznam. Datová pole vrácená uloženou procedurou jsou namapována na sloupce `ProductsDataTable` s. Vzhledem k tomu, že v uložené proceduře je vráceno datové pole `PriceQuartile`, je jeho hodnota přiřazena do sloupce `ProductsDataTable` s `PriceQuartile`.

Pro tyto metody TableAdapter, jejichž dotazy nevracejí `PriceQuartile` datové pole, je hodnota `PriceQuartile` sloupci s hodnotou určenou vlastností `DefaultValue`. Jak ukazuje obrázek 2, tato hodnota je nastavená na `DBNull`, výchozí. Pokud dáváte přednost jiné výchozí hodnotě, jednoduše nastavte vlastnost `DefaultValue` odpovídajícím způsobem. Stačí se ujistit, že hodnota `DefaultValue` je platná pro `DataType` sloupce (tj. `System.Int32` pro sloupec `PriceQuartile`).

V tuto chvíli jsme provedli nezbytné kroky pro přidání dalšího sloupce do objektu DataTable. Chcete-li ověřit, zda tento další sloupec funguje podle očekávání, můžete vytvořit stránku ASP.NET, která zobrazuje jednotlivé produkty s názvem, cenou a kvartil ceny. Předtím, než to provedeme, nejdřív je potřeba aktualizovat vrstvu obchodní logiky tak, aby zahrnovala metodu, která volá metodu `GetProductsWithPriceQuartile` DAL s. KNIHOVEN BLL budeme aktualizovat dál, v kroku 3, a pak vytvořte stránku ASP.NET v kroku 4.

## <a name="step-3-augmenting-the-business-logic-layer"></a>Krok 3: rozšíření vrstvy obchodní logiky

Předtím, než použijeme novou `GetProductsWithPriceQuartile` metodu z prezentační vrstvy, doporučujeme nejprve přidat odpovídající metodu do knihoven BLL. Otevřete soubor `ProductsBLLWithSprocs` třídy a přidejte následující kód:

[!code-vb[Main](adding-additional-datatable-columns-vb/samples/sample2.vb)]

Podobně jako jiné metody načítání dat v `ProductsBLLWithSprocs`volá metoda `GetProductsWithPriceQuartile` jednoduše volání metody DAL s odpovídající `GetProductsWithPriceQuartile` a vrátí její výsledky.

## <a name="step-4-displaying-the-price-quartile-information-in-an-aspnet-web-page"></a>Krok 4: zobrazení informací o kvartil ceny na webové stránce ASP.NET

Po dokončení doplňování knihoven BLL jsme připraveni vytvořit stránku ASP.NET, na které se zobrazí kvartil ceny pro každý produkt. Otevřete stránku `AddingColumns.aspx` ve složce `AdvancedDAL` a přetáhněte prvek GridView z panelu nástrojů do návrháře a nastavte jeho vlastnost `ID` na `Products`. Z inteligentní značky GridView s, navažte ji na nový prvek ObjectDataSource s názvem `ProductsDataSource`. Nakonfigurujte prvek ObjectDataSource tak, aby používal metodu `ProductsBLLWithSprocs` třídy s `GetProductsWithPriceQuartile`. Vzhledem k tomu, že se jedná o mřížku jen pro čtení, nastavte rozevírací seznamy na kartách aktualizace, vložení a odstranění na (žádné).

[![nakonfigurovat prvek ObjectDataSource tak, aby používal třídu ProductsBLLWithSprocs](adding-additional-datatable-columns-vb/_static/image24.png)](adding-additional-datatable-columns-vb/_static/image23.png)

**Obrázek 9**: Konfigurace prvku ObjectDataSource, aby používal třídu `ProductsBLLWithSprocs` ([kliknutím zobrazíte obrázek v plné velikosti](adding-additional-datatable-columns-vb/_static/image25.png))

[![načíst informace o produktu z metody GetProductsWithPriceQuartile](adding-additional-datatable-columns-vb/_static/image27.png)](adding-additional-datatable-columns-vb/_static/image26.png)

**Obrázek 10**: načtení informací o produktu z metody `GetProductsWithPriceQuartile` ([kliknutím zobrazíte obrázek v plné velikosti](adding-additional-datatable-columns-vb/_static/image28.png))

Po dokončení Průvodce konfigurací zdroje dat bude Visual Studio automaticky přidávat vlastnost BoundField nebo třídě CheckBoxField podporována do prvku GridView pro každé z datových polí vrácených metodou. Jedno z těchto datových polí je `PriceQuartile`, což je sloupec, který jsme přidali do `ProductsDataTable` v kroku 1.

Upravte pole GridView s tím, že odeberete všechny kromě `ProductName`, `UnitPrice`a `PriceQuartile` BoundFields. Nakonfigurujte `UnitPrice` vlastnost BoundField, abyste nastavili jeho hodnotu jako měnu a `UnitPrice` a `PriceQuartile` BoundFields a zarovnaná na střed. Nakonec aktualizujte zbývající vlastnosti BoundFields `HeaderText` na produkt, cenu a kvartil ceny v uvedeném pořadí. Také zaškrtněte políčko Povolit řazení z inteligentní značky GridView.

Po těchto úpravách by deklarativní označení GridView a ObjectDataSource s mělo vypadat takto:

[!code-aspx[Main](adding-additional-datatable-columns-vb/samples/sample3.aspx)]

Obrázek 11 ukazuje tuto stránku, když se navštíví přes prohlížeč. Všimněte si, že zpočátku jsou produkty seřazené podle ceny v sestupném pořadí s každým produktem přiřazeným příslušné `PriceQuartile`é hodnotě. Tato data je samozřejmě možné seřadit podle jiných kritérií s hodnotou data QUARTIL (cena), která je stále v souladu s hodnocením produktů s ohledem na cenu (viz obrázek 12).

[![produkty jsou seřazené podle jejich cen](adding-additional-datatable-columns-vb/_static/image30.png)](adding-additional-datatable-columns-vb/_static/image29.png)

**Obrázek 11**: produkty jsou seřazené podle jejich cen ([kliknutím zobrazíte obrázek v plné velikosti).](adding-additional-datatable-columns-vb/_static/image31.png)

[![produkty jsou seřazené podle jejich názvů.](adding-additional-datatable-columns-vb/_static/image33.png)](adding-additional-datatable-columns-vb/_static/image32.png)

**Obrázek 12**: produkty jsou seřazené podle jejich názvů ([kliknutím zobrazíte obrázek v plné velikosti](adding-additional-datatable-columns-vb/_static/image34.png)).

> [!NOTE]
> Pomocí několika řádků kódu jsme mohli prvek GridView rozšířit tak, aby na základě jeho `PriceQuartile` vybarvené řádky produktu. Tyto produkty můžeme nabarvit v první kvartil a světle zelenou, ta ve druhé kvartil je světle žlutá a tak dále. Doporučuje se chvíli trvat, než tuto funkci přidáte. Pokud potřebujete aktualizační program pro formátování prvku GridView, přečtěte si kurz [vlastní formátování na základě data](../custom-formatting/custom-formatting-based-upon-data-vb.md) .

## <a name="an-alternative-approach---creating-another-tableadapter"></a>Alternativní přístup – vytváření dalších TableAdapter

Jak jsme to viděli v tomto kurzu, při přidávání metody do TableAdapter, která vrací datová pole, která vrací hlavní dotaz, můžeme do objektu DataTable přidat odpovídající sloupce. Takový přístup ale funguje i v případě, že v TableAdapter existuje malý počet metod, které vracejí různá datová pole a pokud se tato alternativní datová pole neliší od hlavního dotazu.

Místo přidávání sloupců do objektu DataTable můžete místo toho přidat další TableAdapter do datové sady, která obsahuje metody z prvního TableAdapter, která vrací různá datová pole. Pro tento kurz místo přidání sloupce `PriceQuartile` do `ProductsDataTable` (kde ho používá jenom metoda `GetProductsWithPriceQuartile`) jsme mohli přidat další TableAdapter do datové sady s názvem `ProductsWithPriceQuartileTableAdapter`, která jako svůj hlavní dotaz používala uloženou proceduru `Products_SelectWithPriceQuartile`. ASP.NET stránky, které jsou potřeba k získání informací o produktech s využitím funkce Price, by používaly `ProductsWithPriceQuartileTableAdapter`, zatímco ty, které nemohly `ProductsTableAdapter`používat.

Přidáním nového TableAdapter datové tabulky zůstanou untarnished a jejich sloupce přesně zrcadlí datová pole vrácená metodami TableAdapter s. Další objekty TableAdapter ale můžou vést k opakujícím se úlohám a funkcím. Například pokud jsou tyto stránky ASP.NET se zobrazeným sloupcem `PriceQuartile` také nezbytné k zajištění podpory vložení, aktualizace a odstranění, `ProductsWithPriceQuartileTableAdapter` by musel mít správně nakonfigurovanou vlastnost `InsertCommand`, `UpdateCommand`a `DeleteCommand`. I když tyto vlastnosti zrcadlí `ProductsTableAdapter` s, tato konfigurace zavádí další krok. Kromě toho existují dva způsoby, jak aktualizovat, odstranit nebo přidat produkt do databáze-prostřednictvím tříd `ProductsTableAdapter` a `ProductsWithPriceQuartileTableAdapter`.

Stažení pro tento kurz obsahuje třídu `ProductsWithPriceQuartileTableAdapter` v datové sadě `NorthwindWithSprocs`, která ukazuje tento alternativní přístup.

## <a name="summary"></a>Souhrn

Ve většině scénářů vrátí všechny metody v TableAdapter stejnou sadu datových polí, ale v některých případech nastane čas, kdy konkrétní metoda nebo dvě nemusí vracet další pole. Například v [seznamu hlavní/podrobnosti pomocí seznamu hlavních záznamů s odrážkami s kurzem podrobností DataList](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-vb.md) jsme přidali metodu do `CategoriesTableAdapter`, který kromě datových polí Main Query s vrátí `NumberOfProducts` pole, které oznámilo počet produktů přidružených ke každé kategorii. V tomto kurzu jsme se vyhledali přidáním metody do `ProductsTableAdapter`, která kromě datových polí Main Query s vrátila pole `PriceQuartile`. K zachycení dalších datových polí vrácených metodami TableAdapter s musíme do objektu DataTable přidat odpovídající sloupce.

Pokud plánujete ručně přidávat sloupce do objektu DataTable, je doporučeno, aby TableAdapter používal uložené procedury. Pokud TableAdapter používá příkazy SQL ad hoc, pokaždé, když se spustí Průvodce konfigurací TableAdapter, se vrátí do datových polí vrácených hlavním dotazem. Tento problém se nerozšiřuje na uložené procedury, což je důvod, proč jsou doporučené a byly použity v tomto kurzu.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Recenzenti potenciálních zákazníků pro tento kurz byly Randy Schmidt, Jacky Goor, Bernadette Leigh a Hilton Giesenow. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](updating-the-tableadapter-to-use-joins-vb.md)
> [Další](working-with-computed-columns-vb.md)

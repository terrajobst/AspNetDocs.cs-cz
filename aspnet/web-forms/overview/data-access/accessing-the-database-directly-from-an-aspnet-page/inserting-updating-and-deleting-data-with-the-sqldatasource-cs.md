---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-cs
title: Vložení, aktualizace a odstranění dat pomocí SqlDataSource (C#) | Microsoft Docs
author: rick-anderson
description: V předchozích kurzech jsme zjistili, jak je ovládací prvek ObjectDataSource povolen pro vkládání, aktualizaci a odstraňování dat. Ovládací prvek SqlDataSource podporuje t...
ms.author: riande
ms.date: 02/20/2007
ms.assetid: a526f0ec-779e-4a2b-a476-6604090d25ce
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/inserting-updating-and-deleting-data-with-the-sqldatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: 495e0e81a67e6926e1c4fa92e29ebbda747cd418
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74610397"
---
# <a name="inserting-updating-and-deleting-data-with-the-sqldatasource-c"></a>Vkládání, aktualizace a odstraňování dat ovládacím prvkem SqlDataSource (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_49_CS.exe) nebo [Stáhnout PDF](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/datatutorial49cs1.pdf)

> V předchozích kurzech jsme zjistili, jak je ovládací prvek ObjectDataSource povolen pro vkládání, aktualizaci a odstraňování dat. Ovládací prvek SqlDataSource podporuje stejné operace, ale přístup je jiný a v tomto kurzu se dozvíte, jak nakonfigurovat SqlDataSource pro vkládání, aktualizaci a odstraňování dat.

## <a name="introduction"></a>Úvod

Jak je popsáno v tématu [Přehled vložení, aktualizace a odstranění](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md), ovládací prvek GridView poskytuje integrované možnosti aktualizace a odstraňování, zatímco ovládací prvky DetailsView a FormView zahrnují vkládání podpory spolu s funkcemi úprav a odstranění. Tyto možnosti změny dat můžou být zapojeny přímo do ovládacího prvku zdroje dat, aniž by bylo nutné zapsat řádek kódu. [Přehled vložení, aktualizace a odstranění](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) prověřený pomocí prvku ObjectDataSource pro usnadnění vkládání, aktualizaci a odstraňování pomocí ovládacích prvků GridView, DetailsView a FormView. Případně lze SqlDataSource použít místo prvku ObjectDataSource.

Odvolání, že podpora vložení, aktualizace a odstranění s prvkem ObjectDataSource, který potřebujeme k určení metod objektové vrstvy, které se mají vyvolat k provedení akce vložení, aktualizace nebo odstranění. Ve třídě SqlDataSource potřebujeme pro spuštění `INSERT`, `UPDATE`a `DELETE` příkazy SQL (nebo uložené procedury). Jak je uvedeno v tomto kurzu, tyto příkazy lze vytvořit ručně nebo mohou být automaticky generovány Průvodcem vytvořením zdroje dat SqlDataSource s konfigurací.

> [!NOTE]
> Vzhledem k tomu, že jsme již probrali možnosti vložení, úpravy a odstranění ovládacích prvků GridView, DetailsView a FormView, tento kurz se zaměřuje na konfiguraci ovládacího prvku SqlDataSource pro podporu těchto operací. Pokud potřebujete štětce na implementaci těchto funkcí v prvku GridView, DetailsView a FormView, vraťte se do kurzů pro úpravy, vkládání a odstraňování dat a začněte s [přehledem vložení, aktualizace a odstranění](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md).

## <a name="step-1-specifyinginsertupdate-anddeletestatements"></a>Krok 1: určení příkazů`INSERT`,`UPDATE`a`DELETE`

Jak jsme viděli v minulých dvou kurzech, aby bylo možné načíst data z ovládacího prvku SqlDataSource, potřebujeme nastavit dvě vlastnosti:

1. `ConnectionString`, která určuje databázi, do které se má dotaz odeslat, a
2. `SelectCommand`, která určuje příkaz SQL ad hoc nebo uloženou proceduru, která má být provedena pro vrácení výsledků.

U hodnot `SelectCommand` s parametry jsou hodnoty parametrů zadány prostřednictvím kolekce `SelectParameters` SqlDataSource s a mohou obsahovat pevně zakódované hodnoty, společné zdrojové hodnoty parametrů (pole QueryString, proměnné relací, hodnoty webového ovládacího prvku atd.), nebo lze programově přiřadit. Když je metoda ovládacího prvku SqlDataSource `Select()` vyvolána buď programově nebo automaticky z webového ovládacího prvku data, je navázáno připojení k databázi, hodnoty parametrů jsou přiřazeny dotazu a příkaz je od databáze přerušen. Výsledky se pak vrátí jako datová sada nebo objekt DataReader, v závislosti na hodnotě vlastnosti `DataSourceMode` ovládacího prvku.

Spolu s vybranými daty lze ovládací prvek SqlDataSource použít k vkládání, aktualizaci a odstraňování dat tím, že poskytujete `INSERT`, `UPDATE`a `DELETE` příkazy SQL podobným způsobem. Jednoduše přiřaďte `InsertCommand`, `UpdateCommand`a `DeleteCommand` vlastnosti `INSERT`, `UPDATE`a `DELETE` příkazy SQL, které se mají spustit. Pokud mají příkazy parametry (tak, jak jsou vždy nejčastěji), zahrňte je do kolekcí `InsertParameters`, `UpdateParameters`a `DeleteParameters`.

Po zadání `InsertCommand`, `UpdateCommand`nebo `DeleteCommand` hodnoty bude k dispozici možnost Povolit vkládání, povolit úpravy nebo povolit odstraňování v odpovídajících inteligentních značkách webového ovládacího prvku s daty. K ilustraci je možné použít příklad ze stránky `Querying.aspx`, kterou jsme vytvořili v [dotazech na data pomocí ovládacího prvku SqlDataSource](querying-data-with-the-sqldatasource-control-cs.md) a rozšířit ho tak, aby zahrnoval možnosti odstranění.

Začněte tím, že otevřete `InsertUpdateDelete.aspx` a `Querying.aspx` stránky ze složky `SqlDataSource`. Z návrháře na stránce `Querying.aspx` vyberte SqlDataSource a GridView z prvního příkladu (ovládací prvky `ProductsDataSource` a `GridView1`). Po výběru dvou ovládacích prvků přejděte do nabídky upravit a zvolte možnost Kopírovat (nebo jednoduše stiskněte CTRL + C). V dalším kroku přejdete do návrháře `InsertUpdateDelete.aspx` a vložíte ho do ovládacích prvků. Po přesunutí dvou ovládacích prvků na `InsertUpdateDelete.aspx`testujte stránku v prohlížeči. Měli byste vidět hodnoty `ProductID`, `ProductName`a `UnitPrice` sloupců pro všechny záznamy v tabulce databáze `Products`.

[![všechny produkty jsou seřazené podle ProductID.](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image1.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image1.png)

**Obrázek 1**: seznam všech produktů je seřazený podle `ProductID` ([kliknutím zobrazíte obrázek v plné velikosti).](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image2.png)

## <a name="adding-the-sqldatasource-sdeletecommandanddeleteparametersproperties"></a>Přidání vlastností`DeleteCommand`a`DeleteParameters`SqlDataSource

V tomto okamžiku máme prvek SqlDataSource, který jednoduše vrátí všechny záznamy z `Products` tabulky a GridView, který tato data vykresluje. Naším cílem je tento příklad zvětšit, aby mohl uživatel odstraňovat produkty prostřednictvím prvku GridView. Abychom to dosáhli, musíme zadat hodnoty pro ovládací prvek SqlDataSource `DeleteCommand` a vlastnosti `DeleteParameters` a potom nakonfigurovat prvek GridView tak, aby podporoval odstranění.

Vlastnosti `DeleteCommand` a `DeleteParameters` lze zadat několika způsoby:

- Prostřednictvím deklarativní syntaxe
- Z okno Vlastnosti v Návrháři
- Z obrazovky zadat vlastní příkaz SQL nebo uloženou proceduru v Průvodci konfigurací zdroje dat
- Prostřednictvím tlačítka Upřesnit na obrazovce zadat sloupce v tabulce zobrazení v Průvodci konfigurací zdroje dat, která ve skutečnosti automaticky generuje příkaz `DELETE` SQL a kolekce parametrů použité ve vlastnostech `DeleteCommand` a `DeleteParameters`

Podíváme se, jak automaticky vy`DELETE` příkaz vytvořený v kroku 2. Prozatím použijte okno Vlastnosti v návrháři, i když má Průvodce konfigurací zdroje dat nebo možnost deklarativní syntaxe fungovat stejně.

V návrháři v `InsertUpdateDelete.aspx`klikněte na `ProductsDataSource` SqlDataSource a pak zobrazte okno Vlastnosti (v nabídce zobrazení zvolte okno Vlastnosti nebo jednoduše stiskněte F4). Vyberte vlastnost DeleteQuery, která bude přinášet sadu elips.

![V okně Vlastnosti vyberte vlastnost DeleteQuery.](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image2.gif)

**Obrázek 2**: v okně Vlastnosti vyberte vlastnost DeleteQuery.

> [!NOTE]
> Třída SqlDataSource nemá vlastnost DeleteQuery. Místo toho je DeleteQuery kombinací vlastností `DeleteCommand` a `DeleteParameters` a je uvedena pouze v okno Vlastnosti při prohlížení okna prostřednictvím návrháře. Pokud se díváte na okno Vlastnosti v zobrazení zdroje, najdete místo toho vlastnost `DeleteCommand`.

Kliknutím na elipsy ve vlastnosti DeleteQuery otevřete dialogové okno Editor příkazů a parametrů (viz obrázek 3). Z tohoto dialogového okna můžete zadat příkaz `DELETE` SQL a zadat parametry. Do textového pole `DELETE` příkazu zadejte následující dotaz (buď ručně, nebo pomocí Tvůrce dotazů, pokud dáváte přednost):

[!code-sql[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/samples/sample1.sql)]

Potom kliknutím na tlačítko Aktualizovat parametry přidejte parametr `@ProductID` do seznamu níže uvedených parametrů.

[![v okně Vlastnosti vyberte vlastnost DeleteQuery.](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image3.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image3.png)

**Obrázek 3**: v okně Vlastnosti vyberte vlastnost DeleteQuery ([kliknutím zobrazíte obrázek v plné velikosti](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image4.png)).

Nezadávejte *hodnotu* pro tento parametr (nechejte jeho zdroj parametru v žádné). Jakmile přidáme odstranění podpory do prvku GridView, prvek GridView automaticky dodá tuto hodnotu parametru pomocí hodnoty jeho kolekce `DataKeys` pro řádek, na kterém bylo tlačítko Odstranit kliknuto.

> [!NOTE]
> Název parametru použitý v dotazu `DELETE` *musí* být stejný jako název `DataKeyNames` hodnoty v prvku GridView, DetailsView nebo FormView. To znamená, že parametr v příkazu `DELETE` je záměrně pojmenovaný `@ProductID` (namísto, řekněme, `@ID`), protože název sloupce primárního klíče v tabulce Products (a proto hodnota DataKeyNames v prvku GridView) je `ProductID`.

Pokud se název parametru a hodnota `DataKeyNames` neshodují, prvek GridView nemůže automaticky přiřadit parametr hodnotu z kolekce `DataKeys`.

Po zadání informací souvisejících s odstraněním do dialogového okna a editoru parametrů klikněte na OK a přejděte do zobrazení zdroje a Prohlédněte si výsledný deklarativní kód:

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/samples/sample2.aspx)]

Všimněte si přidání vlastnosti `DeleteCommand` a také oddílu `<DeleteParameters>` a objektu Parameter s názvem `productID`.

## <a name="configuring-the-gridview-for-deleting"></a>Konfigurace prvku GridView pro odstranění

Pomocí přidané vlastnosti `DeleteCommand` nyní obsahuje inteligentní značka GridView s možnost Povolit odstranění. Pokračujte a zaškrtněte toto políčko. Jak je popsáno v tématu [Přehled vložení, aktualizace a odstranění](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md), způsobí to, že prvek GridView přidá objekt CommandField s vlastností `ShowDeleteButton` nastavenou na hodnotu `true`. Jak ukazuje obrázek 4, když je stránka navštívená v prohlížeči, je zahrnuto tlačítko pro odstranění. Otestujte tuto stránku odstraněním některých produktů.

[![každý řádek prvku GridView nyní obsahuje tlačítko Odstranit](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image4.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image5.png)

**Obrázek 4**: každý řádek prvku GridView teď obsahuje tlačítko pro odstranění ([kliknutím zobrazíte obrázek v plné velikosti](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image6.png)).

Po kliknutí na tlačítko Odstranit dojde k postbacku, ovládací prvek GridView přiřadí parametr `ProductID` hodnotu hodnoty `DataKeys` kolekce pro řádek, na kterém bylo tlačítko Odstranit, a vyvolá metodu `Delete()` SqlDataSource s. Ovládací prvek SqlDataSource se pak připojí k databázi a spustí příkaz `DELETE`. Prvek GridView se pak znovu připojí ke třídě SqlDataSource, získá zpět a zobrazí aktuální sadu produktů (které již neobsahují záznam pouhým odstraněním).

> [!NOTE]
> Vzhledem k tomu, že prvek GridView používá kolekci `DataKeys` k naplnění parametrů třídy SqlDataSource, je důležité, aby vlastnost GridView. `DataKeyNames` byla nastavena na sloupce, které tvoří primární klíč a které `SelectCommand` třída SqlDataSource s vrátí tyto sloupce. Kromě toho je důležité, aby byl název parametru ve třídě SqlDataSource s `DeleteCommand` nastaven na hodnotu `@ProductID`. Pokud vlastnost `DataKeyNames` není nastavena nebo není pojmenována `@ProductsID`, kliknutí na tlačítko Odstranit způsobí postback, ale ve skutečnosti nedojde k odstranění žádného záznamu.

Obrázek 5 znázorňuje tuto interakci graficky. Prostudujte si informace o [událostech souvisejících s vložením, aktualizací a odstraněním](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs.md) kurzu podrobnější diskuzi o řetězcích událostí spojených s vložením, aktualizací a odstraněním z webového ovládacího prvku dat.

![Kliknutí na tlačítko Odstranit v prvku GridView Vyvolá metodu SqlDataSource s Delete ().](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image5.gif)

**Obrázek 5**: kliknutí na tlačítko Odstranit v prvku GridView vyvolá metodu `Delete()` SqlDataSource s.

## <a name="step-2-automatically-generating-theinsertupdate-anddeletestatements"></a>Krok 2: automatické generování`INSERT`,`UPDATE`a příkazů`DELETE`

Jak je uvedeno v kroku 1, `INSERT`, `UPDATE`a `DELETE` příkazy SQL lze zadat prostřednictvím okno Vlastnosti nebo pomocí deklarativní syntaxe ovládacího prvku. Tento přístup ale vyžaduje ruční zápis SQL příkazů ručně, což může být monotonous a náchylné k chybám. Naštěstí Průvodce konfigurací zdroje dat nabízí možnost mít při použití obrazovky zadat sloupce z tabulky zobrazení automaticky generované příkazy `INSERT`, `UPDATE`a `DELETE`.

Tuto možnost automatické generace si nechte prozkoumat. Přidejte prvek DetailsView do návrháře v `InsertUpdateDelete.aspx` a nastavte jeho vlastnost `ID` na `ManageProducts`. Dále z inteligentní značky DetailsView s vyberte Vytvoření nového zdroje dat a vytvořte SqlDataSource s názvem `ManageProductsDataSource`.

[![vytvořit novou SqlDataSource s názvem ManageProductsDataSource](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image6.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image7.png)

**Obrázek 6**: Vytvořte novou SqlDataSource s názvem `ManageProductsDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image8.png)).

V Průvodci konfigurací zdroje dat se přihlaste k použití `NORTHWINDConnectionString` připojovacího řetězce a klikněte na další. Na obrazovce konfigurace příkazu SELECT ponechte vybraný přepínač zadat sloupce z tabulky nebo zobrazení a v rozevíracím seznamu vyberte tabulku `Products`. V seznamu zaškrtávacích políček vyberte sloupce `ProductID`, `ProductName`, `UnitPrice`a `Discontinued`.

[![použití tabulky Products, vraťte sloupce ProductID, ProductName, UnitPrice a vyřazeno.](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image7.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image9.png)

**Obrázek 7**: pomocí `Products` tabulky vrátíte sloupce `ProductID`, `ProductName`, `UnitPrice`a `Discontinued` ([kliknutím zobrazíte obrázek v plné velikosti).](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image10.png)

Chcete-li automaticky generovat příkazy `INSERT`, `UPDATE`a `DELETE` založené na vybrané tabulce a sloupcích, klikněte na tlačítko Upřesnit a zaškrtněte políčko Generovat `INSERT`, `UPDATE`a `DELETE` příkazy.

![Zaškrtněte políčko Generovat příkazy INSERT, UPDATE a DELETE.](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image8.gif)

**Obrázek 8**: zaškrtněte políčko Generovat `INSERT`, `UPDATE`a `DELETE` příkazy.

Zaškrtávací políčko Generovat `INSERT`, `UPDATE`a `DELETE` se dá kontrolovat jenom v případě, že vybraná tabulka má primární klíč a sloupec primárního klíče (nebo sloupce) obsahuje seznam vrácených sloupců. Zaškrtávací políčko použít optimistickou souběžnost, které je možné vybrat, jakmile je zaškrtnuto políčko Generovat `INSERT`, `UPDATE`a `DELETE`, budou rozšiřovat `WHERE` klauzulí ve výsledných `UPDATE`ch a `DELETE`ch příkazech k zajištění optimistického řízení souběžnosti. Prozatím ponechejte toto políčko nezaškrtnuté. v dalším kurzu prověříme optimistickou souběžnost s ovládacím prvkem SqlDataSource.

Po zaškrtnutí políčka Generovat `INSERT`, `UPDATE`a `DELETE` se kliknutím na OK vraťte na obrazovku konfigurace příkazu pro výběr, potom klikněte na další a potom na Dokončit. tím dokončíte Průvodce konfigurací zdroje dat. Po dokončení Průvodce přidá Visual Studio BoundFields do ovládacího prvku DetailsView pro sloupce `ProductID`, `ProductName`a `UnitPrice` a třídě CheckBoxField podporována pro sloupec `Discontinued`. Z inteligentní značky DetailsView s zaškrtněte možnost Povolit stránkování, aby uživatel, který navštíví tuto stránku, mohl procházet produkty. Také vymažte vlastnosti ovládacího prvku DetailsView s `Width` a `Height`.

Všimněte si, že inteligentní značka má k dispozici možnosti Povolit vkládání, povolit úpravy a povolit odstraňování. Je to proto, že třída SqlDataSource obsahuje hodnoty pro svůj `InsertCommand`, `UpdateCommand`a `DeleteCommand`, jak ukazuje následující deklarativní syntaxe:

[!code-aspx[Main](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/samples/sample3.aspx)]

Všimněte si, jak ovládací prvek SqlDataSource má automaticky nastaveny hodnoty pro jeho `InsertCommand`, `UpdateCommand`a vlastnosti `DeleteCommand`. Sada sloupců, na které odkazuje `InsertCommand` a `UpdateCommand` vlastností, jsou založeny na těch, které jsou uvedeny v příkazu `SELECT`. To znamená, že místo toho, aby *všechny* produkty v `InsertCommand` a `UpdateCommand`, existují pouze sloupce, které jsou zadány ve `SelectCommand` (méně `ProductID`, což je vynecháno, protože se jedná o [`IDENTITY` sloupec](http://www.sqlteam.com/item.asp?ItemID=102), jehož hodnotu nelze změnit, pokud je upravena a která je automaticky přiřazena při vložení). Kromě toho platí, že pro každý parametr v `InsertCommand`, `UpdateCommand`a vlastnosti `DeleteCommand` existují odpovídající parametry v kolekcích `InsertParameters`, `UpdateParameters`a `DeleteParameters`.

Chcete-li zapnout funkce ovládacího prvku DetailsView s, zaškrtněte možnost Povolit vkládání, povolit úpravy a povolit odstraňování možností ve své inteligentní značce. Tím se přidá CommandField s vlastnostmi `ShowInsertButton`, `ShowEditButton`a `ShowDeleteButton` nastavenými na `true`.

Navštivte stránku v prohlížeči a poznamenejte si tlačítka pro úpravy, odstranění a nová okna zahrnutá v ovládacím prvku DetailsView. Kliknutím na tlačítko Upravit dojde k přepínání ovládacího prvku DetailsView do režimu úprav, který zobrazí všechny vlastnost BoundField, jejichž vlastnost `ReadOnly` je nastavena na `false` (výchozí) jako textové pole a jako zaškrtávací políčko třídě CheckBoxField podporována.

[![rozhraní pro úpravy s výchozím ovládacím prvky DetailsView](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image9.gif)](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image11.png)

**Obrázek 9**: výchozí rozhraní pro úpravy DetailsView s ([kliknutím zobrazíte obrázek v plné velikosti](inserting-updating-and-deleting-data-with-the-sqldatasource-cs/_static/image12.png))

Podobně můžete odstranit aktuálně vybraný produkt nebo přidat do systému nový produkt. Vzhledem k tomu, že příkaz `InsertCommand` pracuje pouze se sloupci `ProductName`, `UnitPrice`a `Discontinued`, ostatní sloupce mají buď `NULL`, nebo jejich výchozí hodnotu přiřazenou databází při vložení. Stejně jako u prvku ObjectDataSource, pokud `InsertCommand` chybí žádné sloupce databázové tabulky, které neumožňují `NULL` s a nemají výchozí hodnotu, při pokusu o spuštění příkazu `INSERT` dojde k chybě SQL.

> [!NOTE]
> Rozhraní pro vložení a úpravu ovládacího prvku DetailsView s chybějícím přizpůsobením nebo ověřením. Chcete-li přidat ovládací prvky ověřování nebo přizpůsobit rozhraní, je nutné převést BoundFields na TemplateFields. Další informace najdete v tématu [přidání ověřovacích ovládacích prvků do rozhraní pro úpravy a vkládání](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md) a [přizpůsobení kurzů rozhraní pro úpravu dat](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) .

Pamatujte také na to, že pro aktualizaci a odstranění ovládací prvek DetailsView používá aktuální hodnotu `DataKey` produktů, která je přítomna pouze v případě, že je nakonfigurována vlastnost `DataKeyNames`. Pokud se zdá, že úpravy nebo odstranění nemají žádný účinek, ujistěte se, že je nastavená vlastnost `DataKeyNames`.

## <a name="limitations-of-automatically-generating-sql-statements"></a>Omezení automatického generování příkazů SQL

Vzhledem k tomu, že možnost generovat `INSERT`, `UPDATE`a příkazy `DELETE` je k dispozici pouze při vybírání sloupců z tabulky, pro složitější dotazy budete muset napsat vlastní `INSERT`, `UPDATE`a `DELETE` příkazy, jako jsme to v kroku 1. Příkazy SQL `SELECT` často používají `JOIN` s k vrácení dat z jedné nebo více vyhledávacích tabulek pro účely zobrazení (například při návratu do pole `Categories` tabulky s `CategoryName` při zobrazení informací o produktu). Zároveň můžeme uživatelům dovolit, aby mohli upravovat, aktualizovat nebo vkládat data do základní tabulky (`Products`v tomto případě).

I když příkazy `INSERT`, `UPDATE`a `DELETE` lze zadat ručně, vezměte v úvahu následující Tip pro úsporu času. Zpočátku nastavili SqlDataSource, aby data ze `Products` tabulky vrátila zpět. Pomocí Průvodce konfigurací zdroje dat můžete zadat sloupce z obrazovky tabulky nebo zobrazení, abyste mohli automaticky vygenerovat příkazy `INSERT`, `UPDATE`a `DELETE`. Po dokončení průvodce zvolte, že se má nakonfigurovat SelectQuery z okno Vlastnosti (nebo můžete také přejít zpět do Průvodce konfigurací zdroje dat, ale použijte možnost zadat vlastní příkaz SQL nebo uloženou proceduru). Pak aktualizujte příkaz `SELECT` tak, aby zahrnoval syntaxi `JOIN`. Tato technika nabízí časově náročné výhody automaticky generovaných příkazů SQL a umožňuje přizpůsobený příkaz `SELECT`.

Dalším omezením automatického generování `INSERT`, `UPDATE`a `DELETE`ch příkazů je, že sloupce v `INSERT` a příkazy `UPDATE` jsou založené na sloupcích vrácených příkazem `SELECT`. Můžeme však potřebovat aktualizovat nebo vložit více nebo méně polí. Například v příkladu z kroku 2 Možná chceme mít `UnitPrice` vlastnost BoundField být jen pro čtení. V takovém případě by se neměl zobrazovat v `UpdateCommand`. Nebo můžeme chtít nastavit hodnotu pole tabulky, které se nezobrazí v prvku GridView. Například při přidávání nového záznamu můžeme chtít, aby byla hodnota `QuantityPerUnit` nastavena na TODO.

Pokud jsou takové úpravy požadovány, je nutné je ručně provést buď pomocí okno Vlastnosti, v průvodci zadat vlastní příkaz SQL nebo uloženou proceduru nebo prostřednictvím deklarativní syntaxe.

> [!NOTE]
> Při přidávání parametrů, které nemají odpovídající pole v ovládacím prvku data web, pamatujte na to, že tyto hodnoty parametrů bude nutné přiřadit hodnoty nějakým způsobem. Tyto hodnoty mohou být: pevně zakódovány přímo v `InsertCommand` nebo `UpdateCommand`; může pocházet z nějakého předem definovaného zdroje (QueryString, stav relace, webové ovládací prvky na stránce atd.); nebo se dá přiřadit programově, jak jsme viděli v předchozím kurzu.

## <a name="summary"></a>Přehled

Aby webové ovládací prvky dat využily integrované funkce pro vkládání, úpravy a odstraňování, je nutné, aby ovládací prvek zdroje dat, ke kterému jsou vazby, poskytoval tyto funkce. Pro SqlDataSource to znamená, že `INSERT`, `UPDATE`a `DELETE` příkazy SQL musí být přiřazeny vlastnostem `InsertCommand`, `UpdateCommand`a `DeleteCommand`. Tyto vlastnosti a odpovídající kolekce parametrů lze přidat ručně nebo generovat automaticky prostřednictvím Průvodce konfigurací zdroje dat. V tomto kurzu jsme prozkoumali oba postupy.

Prozkoumali jsme použití optimistického řízení souběžnosti s prvkem ObjectDataSource v kurzu [implementace optimistického řízení souběžnosti](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs.md) . Ovládací prvek SqlDataSource také poskytuje podporu optimistického řízení souběžnosti. Jak je uvedeno v kroku 2, když automaticky generujete příkazy `INSERT`, `UPDATE`a `DELETE`, průvodce nabízí možnost použít optimistickou souběžnost. Jak je vidět v dalším kurzu, použití optimistické souběžnosti se sestavou SqlDataSource upravuje klauzule `WHERE` v příkazech `UPDATE` a `DELETE`, aby se zajistilo, že se hodnoty ostatních sloupců nezměnily od posledního zobrazení dat na stránce.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Předchozí](using-parameterized-queries-with-the-sqldatasource-cs.md)
> [Další](implementing-optimistic-concurrency-with-the-sqldatasource-cs.md)

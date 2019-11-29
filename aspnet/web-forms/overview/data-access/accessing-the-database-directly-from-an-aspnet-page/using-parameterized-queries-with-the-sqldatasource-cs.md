---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/using-parameterized-queries-with-the-sqldatasource-cs
title: Použití parametrizovaných dotazů s třídami SqlDataSourceC#() | Microsoft Docs
author: rick-anderson
description: V tomto kurzu budeme pokračovat v hledání na ovládacím prvku SqlDataSource a naučíte se, jak definovat parametrizované dotazy. Parametry lze zadat současně deklaraci...
ms.author: riande
ms.date: 02/20/2007
ms.assetid: 9128aaac-afe2-449f-84b2-bb1d035083c4
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/using-parameterized-queries-with-the-sqldatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: 241dc8c089d4faa9eb95a63684e8a56756bb302c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74611302"
---
# <a name="using-parameterized-queries-with-the-sqldatasource-c"></a>Použití parametrizovaných dotazů s ovládacím prvkem SqlDataSource (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_48_CS.exe) nebo [Stáhnout PDF](using-parameterized-queries-with-the-sqldatasource-cs/_static/datatutorial48cs1.pdf)

> V tomto kurzu budeme pokračovat v hledání na ovládacím prvku SqlDataSource a naučíte se, jak definovat parametrizované dotazy. Parametry lze zadat deklarativně i programově a lze je načíst z několika umístění, jako je například QueryString, stav relace, další ovládací prvky a další.

## <a name="introduction"></a>Úvod

V předchozím kurzu jsme viděli, jak použít ovládací prvek SqlDataSource k načtení dat přímo z databáze. Pomocí Průvodce konfigurací zdroje dat můžeme zvolit databázi a potom buď: Vyberte sloupce, které se mají vrátit z tabulky nebo zobrazení. Zadejte vlastní příkaz SQL. nebo použijte uloženou proceduru. Bez ohledu na `SELECT` to, jestli se mají vybrat sloupce z tabulky nebo zobrazit nebo zadat vlastní příkaz SQL, se vlastnosti `SelectCommand` ovládacího prvku SqlDataSource přiřadí Výsledný příkaz SQL `SELECT`, který se spustí při vyvolání metody `Select()` SqlDataSource (buď prostřednictvím kódu programu, nebo automaticky z webového ovládacího prvku data).

Příkazy SQL `SELECT` používané v předchozích ukázkách kurzu s chybí `WHERE` klauzulí. V příkazu `SELECT` lze použít klauzuli `WHERE` k omezení vrácených výsledků. Pokud například chcete zobrazit názvy produktů více než $50,00, můžeme použít následující dotaz:

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample1.sql)]

Hodnoty používané v klauzuli `WHERE` se obvykle určují pomocí některého externího zdroje, jako je například hodnota QueryString, proměnná relace nebo vstup uživatele z webového ovládacího prvku na stránce. V ideálním případě jsou tyto vstupy zadány pomocí *parametrů*. U Microsoft SQL Server jsou parametry označeny pomocí `@parameterName`, jako v:

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample2.sql)]

Třída SqlDataSource podporuje parametrizované dotazy, pro `SELECT` příkazy a `INSERT`, `UPDATE`a `DELETE` příkazy. Hodnoty parametrů je navíc možné automaticky načíst z nejrůznějších zdrojů. QueryString, stav relace, ovládací prvky na stránce a tak dále lze přiřadit programově. V tomto kurzu se dozvíte, jak definovat parametrizované dotazy a jak deklarativně i programově zadat hodnoty parametrů.

> [!NOTE]
> V předchozím kurzu jsme porovnali prvek ObjectDataSource, který je nášm nástrojem, který je v prvních 46 kurzech, který se nachází ve třídě SqlDataSource a označuje jejich koncepční podobnosti. Tyto podobnosti se také rozšíří na parametry. Parametry ObjectDataSource s mapované na vstupní parametry pro metody ve vrstvě obchodní logiky. Pomocí SqlDataSource jsou parametry definovány přímo v rámci dotazu SQL. Oba ovládací prvky mají kolekce parametrů pro jejich `Select()`, `Insert()`, `Update()`a metody `Delete()` a obě můžou mít tyto hodnoty parametrů naplněné z předdefinovaných zdrojů (hodnoty QueryString, proměnné relace atd.) nebo přiřazené programově.

## <a name="creating-a-parameterized-query"></a>Vytvoření parametrického dotazu

Průvodce pro ovládací prvek SqlDataSource s konfigurací zdroje dat nabízí tři cesty vedoucíy pro definování příkazu, který se má provést pro načtení záznamů databáze:

- Když vybíráte sloupce z existující tabulky nebo zobrazení,
- Zadáním vlastního příkazu SQL nebo
- Výběrem uložené procedury

Když vybíráte sloupce z existující tabulky nebo zobrazení, parametry klauzule `WHERE` musí být zadány pomocí dialogového okna Přidat `WHERE` klauzuli. Při vytváření vlastního příkazu SQL však můžete zadat parametry přímo do klauzule `WHERE` (pomocí `@parameterName` pro označení každého parametru). [Uložená procedura](http://www.awprofessional.com/articles/article.asp?p=25288&amp;rl=1) se skládá z jednoho nebo více příkazů SQL a tyto příkazy mohou být parametrizované. Parametry použité v příkazech jazyka SQL však musí být předány jako vstupní parametry do uložené procedury.

Vzhledem k tomu, že vytvoření parametrizovaného dotazu závisí na tom, jak je `SelectCommand` SqlDataSource, se můžeme podívat na všechny tři přístupy. Chcete-li začít, otevřete stránku `ParameterizedQueries.aspx` ve složce `SqlDataSource`, přetáhněte ovládací prvek SqlDataSource ze sady nástrojů do návrháře a nastavte jeho `ID` na `Products25BucksAndUnderDataSource`. Potom klikněte na odkaz konfigurace zdroje dat z inteligentní značky Control s. Vyberte databázi, kterou chcete použít (`NORTHWINDConnectionString`) a klikněte na další.

## <a name="step-1-adding-awhereclause-when-picking-the-columns-from-a-table-or-view"></a>Krok 1: Přidání klauzule`WHERE`při výběru sloupců z tabulky nebo zobrazení

Když vyberete data, která se mají vrátit z databáze pomocí ovládacího prvku SqlDataSource, Průvodce konfigurací zdroje dat nám umožní jednoduše vybrat sloupce, které se vrátí z existující tabulky nebo zobrazení (viz obrázek 1). Tím se automaticky vytvoří příkaz SQL `SELECT`, který je odeslán do databáze při vyvolání metody SqlDataSource s `Select()`. Stejně jako v předchozím kurzu vyberte v rozevíracím seznamu tabulku Products a zaškrtněte sloupce `ProductID`, `ProductName`a `UnitPrice`.

[![vybrat sloupce, které se mají vrátit z tabulky nebo zobrazení](using-parameterized-queries-with-the-sqldatasource-cs/_static/image1.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image1.png)

**Obrázek 1**: Vyberte sloupce, které se mají vrátit z tabulky nebo zobrazení ([kliknutím zobrazíte obrázek v plné velikosti](using-parameterized-queries-with-the-sqldatasource-cs/_static/image2.png)).

Chcete-li do příkazu `SELECT` zahrnout klauzuli `WHERE`, klikněte na tlačítko `WHERE`, které vyvolá dialogové okno Přidat `WHERE` klauzuli (viz obrázek 2). Chcete-li přidat parametr pro omezení výsledků vrácených dotazem `SELECT`, nejprve vyberte sloupec, podle kterého chcete data filtrovat. Dále vyberte operátor, který se má použít pro filtrování (=, &lt;, &lt;=, &gt;atd.). Nakonec vyberte zdroj hodnoty parametru s, například ze stavu QueryString nebo relace. Po nakonfigurování parametru klikněte na tlačítko Přidat a zahrňte ho do `SELECT`ového dotazu.

V tomto příkladu vrátíme pouze výsledky, kde `UnitPrice` hodnota je menší nebo rovna $25,00. Proto vyberte `UnitPrice` z rozevíracího seznamu sloupec a &lt;= v rozevíracím seznamu operátor. Při použití pevně zakódované hodnoty parametru (například $25,00) nebo pokud má být hodnota parametru zadána programově, vyberte v rozevíracím seznamu zdroj možnost žádná. Potom do textového pole hodnota 25,00 zadejte pevně zakódovaný parametr a kliknutím na tlačítko Přidat proces dokončete.

[![omezit výsledky vrácené z dialogového okna Přidat klauzuli WHERE](using-parameterized-queries-with-the-sqldatasource-cs/_static/image2.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image3.png)

**Obrázek 2**: omezení výsledků vrácených z dialogového okna přidat klauzuli `WHERE` ([kliknutím zobrazíte obrázek v plné velikosti](using-parameterized-queries-with-the-sqldatasource-cs/_static/image4.png))

Po přidání parametru se kliknutím na tlačítko OK vraťte do Průvodce konfigurací zdroje dat. Příkaz `SELECT` v dolní části Průvodce by teď měl obsahovat klauzuli `WHERE` s parametrem s názvem `@UnitPrice`:

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample3.sql)]

> [!NOTE]
> Pokud v klauzuli `WHERE` zadáte v dialogovém okně Přidat `WHERE` klauzuli více podmínek, průvodce je spojí s operátorem `AND`. Pokud potřebujete zahrnout `OR` do klauzule `WHERE` (například `WHERE UnitPrice <= @UnitPrice OR Discontinued = 1`), musíte vytvořit `SELECT` příkaz pomocí vlastní obrazovky příkazů SQL.

Dokončete konfiguraci značky SqlDataSource (klikněte na tlačítko Další a pak na Dokončit) a pak zkontrolujte deklarativní označení SqlDataSource s. Značka nyní obsahuje kolekci `<SelectParameters>`, která vypíše zdroje pro parametry v `SelectCommand`.

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample4.aspx)]

Při vyvolání metody `Select()` SqlDataSource, je před odesláním do databáze v `SelectCommand` `@UnitPrice` použita hodnota parametru `UnitPrice` (25,00). Výsledkem je, že v `Products` tabulce jsou vráceny pouze ty produkty menší nebo rovny $25,00. Potvrďte to tak, že na stránku přidáte prvek GridView, svážete ho s tímto zdrojem dat a pak tuto stránku zobrazíte v prohlížeči. Měli byste vidět jenom ty produkty, které jsou uvedené v seznamu, který je menší nebo roven $25,00, jak obrázek 3 potvrdí.

[![se zobrazí jenom ty produkty, které jsou menší nebo rovny $25,00.](using-parameterized-queries-with-the-sqldatasource-cs/_static/image3.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image5.png)

**Obrázek 3**: zobrazuje se jenom tento počet produktů, které jsou menší nebo rovny $25,00 ([kliknutím zobrazíte obrázek v plné velikosti).](using-parameterized-queries-with-the-sqldatasource-cs/_static/image6.png)

## <a name="step-2-adding-parameters-to-a-custom-sql-statement"></a>Krok 2: Přidání parametrů do vlastního příkazu SQL

Při přidávání vlastního příkazu SQL můžete zadat klauzuli `WHERE` explicitně nebo zadat hodnotu do buňky filtru Tvůrce dotazů. K tomu je možné Ukázat, že se zobrazí pouze tyto produkty v prvku GridView, jejichž ceny jsou nižší než určitá prahová hodnota. Začněte přidáním textového pole na stránku `ParameterizedQueries.aspx`, aby se tato prahová hodnota z uživatele shromáždila. Nastavte vlastnost TextBox s `ID` na `MaxPrice`. Přidejte webový ovládací prvek tlačítko a nastavte jeho vlastnost `Text`, aby se zobrazily odpovídající produkty.

Dále přetáhněte prvek GridView na stránku a z jeho inteligentní značky vyberte, chcete-li vytvořit novou SqlDataSource s názvem `ProductsFilteredByPriceDataSource`. V Průvodci konfigurací zdroje dat přejděte na obrazovku zadat vlastní příkaz SQL nebo uloženou proceduru (viz obrázek 4) a zadejte následující dotaz:

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample5.sql)]

Po zadání dotazu (buď ručně nebo prostřednictvím Tvůrce dotazů) klikněte na další.

[![vrátit pouze ty produkty, které jsou menší nebo rovny hodnotě parametru](using-parameterized-queries-with-the-sqldatasource-cs/_static/image4.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image7.png)

**Obrázek 4**: vrácení pouze těch produktů, které jsou menší nebo rovny hodnotě parametru ([kliknutím zobrazíte obrázek v plné velikosti](using-parameterized-queries-with-the-sqldatasource-cs/_static/image8.png))

Vzhledem k tomu, že dotaz obsahuje parametry, zobrazí další obrazovka v průvodci nápovědu pro zdroj hodnot parametrů. Z rozevíracího seznamu zdroj parametrů vyberte ovládací prvek a `MaxPrice` (ovládací prvek TextBox s `ID` hodnota) z rozevíracího seznamu ControlID. Můžete také zadat volitelnou výchozí hodnotu, která se použije v případě, že uživatel nezadal žádný text do textového pole `MaxPrice`. V tomto časovém období nezadávejte výchozí hodnotu.

[![vlastnost text TextBox MaxPrice s textem se používá jako zdroj parametru.](using-parameterized-queries-with-the-sqldatasource-cs/_static/image5.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image9.png)

**Obrázek 5**: vlastnost `MaxPrice` TextBox s `Text` se používá jako zdroj parametru ([kliknutím zobrazíte obrázek v plné velikosti).](using-parameterized-queries-with-the-sqldatasource-cs/_static/image10.png)

Dokončete Průvodce konfigurací zdroje dat kliknutím na tlačítko Další a potom na Dokončit. Následuje deklarativní označení pro prvek GridView, TextBox, Button a SqlDataSource:

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample6.aspx)]

Všimněte si, že parametr v sekci `<SelectParameters>` SqlDataSource je `ControlParameter`, která zahrnuje další vlastnosti, jako je `ControlID` a `PropertyName`. Když je vyvolána metoda `Select()` SqlDataSource, `ControlParameter` převede hodnotu ze zadané vlastnosti ovládacího prvku web a přiřadí ji k odpovídajícímu parametru v `SelectCommand`. V tomto příkladu se jako hodnota parametru `@MaxPrice` používá vlastnost text `MaxPrice` s.

Tuto stránku si můžete zobrazit pomocí prohlížeče. Při první návštěvě stránky nebo pokaždé, když `MaxPrice` textového pole chybí hodnota, se v prvku GridView zobrazí žádné záznamy.

[Když je textové pole MaxPrice prázdné, neobjeví se žádné záznamy. ![](using-parameterized-queries-with-the-sqldatasource-cs/_static/image6.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image11.png)

**Obrázek 6**: když je textové pole `MaxPrice` prázdné ([kliknutím zobrazíte obrázek v plné velikosti](using-parameterized-queries-with-the-sqldatasource-cs/_static/image12.png)), nezobrazí se žádné záznamy.

Důvod, proč nejsou zobrazeny žádné produkty, je, že ve výchozím nastavení je prázdný řetězec pro hodnotu parametru převeden na hodnotu `NULL` databáze. Vzhledem k tomu, že se porovnání `[UnitPrice] <= NULL` vždy vyhodnocuje jako false, nejsou vráceny žádné výsledky.

Do textového pole zadejte hodnotu, třeba 5,00, a klikněte na tlačítko Zobrazit porovnání produktů. Při zpětném volání, třída SqlDataSource informuje prvek GridView, že došlo ke změně některého z jeho zdrojů parametrů. V důsledku toho se prvek GridView znovu připojí ke třídě SqlDataSource a zobrazí tyto produkty menší nebo rovny $5,00.

[Zobrazí se ![é produkty menší nebo rovny $5,00.](using-parameterized-queries-with-the-sqldatasource-cs/_static/image7.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image13.png)

**Obrázek 7**: zobrazí se produkty, které jsou menší nebo rovny $5,00 ([kliknutím zobrazíte obrázek v plné velikosti).](using-parameterized-queries-with-the-sqldatasource-cs/_static/image14.png)

## <a name="initially-displaying-all-products"></a>Počáteční zobrazení všech produktů

Místo zobrazování žádného produktu při prvním načtení stránky můžeme zobrazit *všechny* produkty. Jedním ze způsobů, jak zobrazit seznam všech produktů pokaždé, když je textové pole `MaxPrice` prázdné, je nastavit výchozí hodnotu parametru s některými neskutečně vysokou hodnotou, jako je 1000000, protože je pravděpodobné, že v seznamu Northwind Traders bude někdy inventář, jehož jednotková cena překračuje $1 000 000. Tento přístup je ale shortsighted a nemusí fungovat v jiných situacích.

V předchozích kurzech – [deklarativní parametry](../basic-reporting/declarative-parameters-cs.md) a [filtrování hlavního/podrobného filtru s ovládacím prvkem DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) jsme dělali s podobným problémem. Naše řešení mělo tuto logiku vložit do vrstvy obchodní logiky. Konkrétně knihoven BLL zkontroloval příchozí hodnotu, a pokud `NULL` nebo nějaké rezervované hodnoty, bylo volání směrováno na metodu DAL, která vrátila všechny záznamy. Pokud byla vstupní hodnota normální hodnotou filtrování, bylo provedeno volání metody DAL, která provedla příkaz jazyka SQL, který použil parametrizovanou klauzuli `WHERE` se zadanou hodnotou.

Bohužel při použití SqlDataSource tuto architekturu vynecháváme. Místo toho je potřeba přizpůsobit příkaz SQL inteligentnímu převzetí všech záznamů, pokud je parametr `@MaximumPrice` `NULL` nebo některá rezervovaná hodnota. Pro účely tohoto cvičení ji nechte mít, aby v případě, že je parametr `@MaximumPrice` stejný jako `-1.0`, byly vráceny *všechny* záznamy (`-1.0` fungovat jako rezervovaná hodnota, protože žádný produkt nemůže mít záporný `UnitPrice` hodnotu). K tomu můžeme použít následující příkaz SQL:

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample7.sql)]

Tato klauzule `WHERE` vrátí *všechny* záznamy, pokud se parametr `@MaximumPrice` rovná `-1.0`. Pokud hodnota parametru není `-1.0`, vrátí se pouze ty produkty, jejichž `UnitPrice` je menší nebo rovno hodnotě `@MaximumPrice` parametru. Nastavením výchozí hodnoty parametru `@MaximumPrice` na `-1.0`, při prvním načtení stránky (nebo pokaždé, když je pole `MaxPrice` prázdné) `@MaximumPrice` bude mít hodnotu `-1.0` a zobrazí se všechny produkty.

[Když je textové pole MaxPrice prázdné, ![se teď všechny produkty zobrazovat.](using-parameterized-queries-with-the-sqldatasource-cs/_static/image8.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image15.png)

**Obrázek 8**: teď se zobrazí všechny produkty, když je textové pole `MaxPrice` prázdné ([kliknutím zobrazíte obrázek v plné velikosti).](using-parameterized-queries-with-the-sqldatasource-cs/_static/image16.png)

S tímto přístupem je potřeba vzít v paměti několik aspektů. Nejprve si pojistěte, aby datový typ parametru s byl odvozen využitím IT v dotazu SQL. Změníte-li klauzuli `WHERE` z `@MaximumPrice = -1.0` na `@MaximumPrice = -1`, modul runtime zpracuje parametr jako celé číslo. Pokud se pak pokusíte přiřadit `MaxPrice` TextBox k desítkové hodnotě (například 5,00), dojde k chybě, protože nemůže převést 5,00 na celé číslo. Chcete-li tento problém napravit, buď se ujistěte, že používáte `@MaximumPrice = -1.0` v klauzuli `WHERE` nebo ještě lépe nastavte vlastnost `ControlParameter` objektů s `Type` na hodnotu Decimal.

Po přidání `OR @MaximumPrice = -1.0` do klauzule `WHERE` nemůže dotazovací modul použít index v `UnitPrice` (za předpokladu, že existuje), což by vedlo k prohledávání tabulky. To může mít vliv na výkon, pokud je v `Products` tabulce dostatečně velký počet záznamů. Lepším přístupem je přesunutí této logiky do úložné procedury, kde příkaz `IF` buď provede `SELECT` dotaz z tabulky `Products` bez klauzule `WHERE`, pokud se mají vrátit všechny záznamy, nebo jedna z jejích klauzulí `WHERE` obsahuje pouze kritéria `UnitPrice`, aby bylo možné použít index.

## <a name="step-3-creating-and-using-parameterized-stored-procedures"></a>Krok 3: vytvoření a použití parametrizovaných uložených procedur

Uložené procedury mohou zahrnovat sadu vstupních parametrů, které lze použít v příkazech jazyka SQL definovaných v rámci uložené procedury. Při konfiguraci aplikace SqlDataSource tak, aby používala uloženou proceduru, která přijímá vstupní parametry, lze tyto hodnoty parametrů zadat stejným způsobem jako s příkazy SQL ad-hoc.

Chcete-li ilustrovat použití uložených procedur ve třídě SqlDataSource, je nutné vytvořit novou uloženou proceduru v databázi Northwind s názvem `GetProductsByCategory`, která přijímá parametr s názvem `@CategoryID` a vrátí všechny sloupce produktů, jejichž `CategoryID` sloupec odpovídá `@CategoryID`. Chcete-li vytvořit uloženou proceduru, přejděte do Průzkumník serveru a přejděte do databáze `NORTHWND.MDF`. (Pokud nevidíte Průzkumník serveru, přepněte ho do nabídky zobrazení a vyberte možnost Průzkumník serveru.)

Z databáze `NORTHWND.MDF` klikněte pravým tlačítkem na složku uložené procedury, vyberte možnost Přidat novou uloženou proceduru a zadejte následující syntaxi:

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample8.sql)]

Uložte uloženou proceduru kliknutím na ikonu Uložit (nebo CTRL + S). Uloženou proceduru můžete otestovat tak, že na ni kliknete pravým tlačítkem ze složky uložené procedury a kliknete na spustit. Zobrazí se výzva k zadání parametrů uložené procedury (`@CategoryID`v této instanci), po jejichž uplynutí se výsledky zobrazí v okně výstup.

[![uloženou proceduru GetProductsByCategory při spuštění s @CategoryID 1](using-parameterized-queries-with-the-sqldatasource-cs/_static/image9.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image17.png)

**Obrázek 9**: `GetProductsByCategory` uloženou proceduru při spuštění s `@CategoryID` 1 ([kliknutím zobrazíte obrázek v plné velikosti](using-parameterized-queries-with-the-sqldatasource-cs/_static/image18.png))

Tuto uloženou proceduru můžete použít k zobrazení všech produktů v kategorii nápoje v prvku GridView. Přidejte na stránku nový prvek GridView a vytvořte jeho vazby k nové třídě SqlDataSource s názvem `BeverageProductsDataSource`. Přejděte na obrazovku zadat vlastní příkaz SQL nebo uloženou proceduru, vyberte přepínač uložené procedury a z rozevíracího seznamu vyberte `GetProductsByCategory` uloženou proceduru.

[![v rozevíracím seznamu vyberte uloženou proceduru GetProductsByCategory.](using-parameterized-queries-with-the-sqldatasource-cs/_static/image10.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image19.png)

**Obrázek 10**: v rozevíracím seznamu vyberte uloženou proceduru `GetProductsByCategory` ([kliknutím zobrazíte obrázek v plné velikosti).](using-parameterized-queries-with-the-sqldatasource-cs/_static/image20.png)

Vzhledem k tomu, že úložná procedura akceptuje vstupní parametr (`@CategoryID`), zobrazí se kliknutím na další výzva k zadání zdroje pro tuto hodnotu parametru s. `CategoryID` nápoje mají hodnotu 1, takže rozevírací seznam zdroj parametrů ponechte v žádné a zadejte hodnotu 1 do textového pole DefaultValue.

[pro vrácení produktů v kategorii nápoje ![použít pevně kódovanou hodnotu 1.](using-parameterized-queries-with-the-sqldatasource-cs/_static/image11.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image21.png)

**Obrázek 11**: použití pevně zakódované hodnoty 1 pro vrácení produktů v kategorii nápoje ([kliknutím zobrazíte obrázek v plné velikosti](using-parameterized-queries-with-the-sqldatasource-cs/_static/image22.png))

Jak ukazuje následující deklarativní označení, při použití uložené procedury je vlastnost SqlDataSource s `SelectCommand` nastavena na název uložené procedury a [vlastnost`SelectCommandType`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.selectcommandtype.aspx) je nastavena na hodnotu `StoredProcedure`, což značí, že `SelectCommand` je název uložené procedury a nikoli příkaz SQL ad-hoc.

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample9.aspx)]

Otestujte stránku v prohlížeči. Zobrazí se pouze ty produkty, které patří do kategorie nápoje, i když se zobrazí *všechna* pole produktu, protože `GetProductsByCategory` uložená procedura vrátí všechny sloupce z tabulky `Products`. Můžeme samozřejmě omezit nebo přizpůsobit pole zobrazená v prvku GridView v dialogovém okně Upravit sloupce GridView.

[![zobrazí se všechny nápoje.](using-parameterized-queries-with-the-sqldatasource-cs/_static/image12.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image23.png)

**Obrázek 12**: zobrazí se všechny nápoje ([kliknutím zobrazíte obrázek v plné velikosti).](using-parameterized-queries-with-the-sqldatasource-cs/_static/image24.png)

## <a name="step-4-programmatically-invoking-a-sqldatasource-sselectstatement"></a>Krok 4: vyvolání příkazu`Select()`SqlDataSource s pomocí kódu programu

Příklady, které jsme si poznamenali v předchozím kurzu, a v tomto kurzu mají i nadále vázané ovládací prvky SqlDataSource přímo na prvek GridView. Data ovládacího prvku SqlDataSource však lze programově přistupovat a zobrazit v kódu. To může být zvláště užitečné, když potřebujete zadat dotaz na data, abyste je zkontrolovali, ale nemusíte je zobrazit. Místo toho, abyste museli zapisovat všechen často používaný kód ADO.NET pro připojení k databázi, zadejte příkaz a načtěte výsledky. můžete tak nechat, aby tento kód monotonous zpracovala třída SqlDataSource.

Představte si, že se vám při práci s daty ve třídě SqlDataSource s data připravuje váš nadřízený, na který se přibližuje požadavek na vytvoření webové stránky, která zobrazuje název náhodně vybrané kategorie a jejích přidružených produktů. To znamená, že když uživatel navštíví tuto stránku, chceme v tabulce `Categories` náhodně zvolit kategorii, zobrazit název kategorie a pak uvést seznam produktů patřících do této kategorie.

Abychom to dosáhli, potřebujeme dva ovládací prvky SqlDataSource pro vytvoření náhodné kategorie z `Categories` tabulky a další pro získání produktů kategorie s. Vytvoříme SqlDataSource, která v tomto kroku načte náhodný záznam kategorie. Krok 5 se zabývá vytvářením značky SqlDataSource, která načítá produkty kategorie s.

Začněte přidáním SqlDataSource do `ParameterizedQueries.aspx` a nastavte jeho `ID` na `RandomCategoryDataSource`. Nakonfigurujte ji tak, aby používala následující dotaz SQL:

[!code-sql[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample10.sql)]

`ORDER BY NEWID()` vrátí záznamy seřazené v náhodném pořadí (viz [použití `NEWID()` k náhodnému řazení záznamů](http://www.sqlteam.com/item.asp?ItemID=8747)). `SELECT TOP 1` vrátí první záznam ze sady výsledků dotazu. Tento dotaz společně vloží hodnoty sloupce `CategoryID` a `CategoryName` z jedné náhodně vybrané kategorie.

Chcete-li zobrazit kategorii s `CategoryName` hodnotou, přidejte na stránku webový ovládací prvek popisek, nastavte jeho vlastnost `ID` na hodnotu `CategoryNameLabel`a vymažte jeho vlastnost `Text`. Abychom mohli programově načíst data z ovládacího prvku SqlDataSource, musíme vyvolat jeho `Select()` metodu. [Metoda`Select()`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.select.aspx) očekává jeden vstupní parametr typu [`DataSourceSelectArguments`](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.aspx), který určuje, jak se mají data před vrácením vrátit. To může zahrnovat pokyny pro řazení a filtrování dat a používá se při řazení nebo stránkování přes data z ovládacího prvku SqlDataSource k datovým webovým ovládacím prvkům. Pro náš příklad ale potřebujeme, aby data byla před vrácením změněna, a proto budou předána do objektu `DataSourceSelectArguments.Empty`.

Metoda `Select()` vrátí objekt, který implementuje `IEnumerable`. Přesný typ vrácený závisí na hodnotě [vlastnosti`DataSourceMode`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.datasourcemode.aspx)ovládacího prvku SqlDataSource. Jak je popsáno v předchozím kurzu, tato vlastnost může být nastavena na hodnotu buď `DataSet`, nebo `DataReader`. Pokud je nastavena na `DataSet`, metoda `Select()` vrátí objekt [DataView](https://msdn.microsoft.com/library/01s96x0z.aspx) ; Pokud je nastaveno na `DataReader`, vrátí objekt, který implementuje [`IDataReader`](https://msdn.microsoft.com/library/system.data.idatareader.aspx). Vzhledem k tomu, že `RandomCategoryDataSource` SqlDataSource má svou vlastnost `DataSourceMode` nastavenou na `DataSet` (výchozí), budeme pracovat s objektem DataView.

Následující kód ilustruje, jak načíst záznamy z `RandomCategoryDataSource` SqlDataSource jako objekt DataView a jak načíst `CategoryName` hodnotu sloupce z prvního řádku DataView:

[!code-csharp[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample11.cs)]

`randomCategoryView[0]` vrátí první `DataRowView` v objektu DataView. `randomCategoryView[0]["CategoryName"]` vrátí hodnotu sloupce `CategoryName` v tomto prvním řádku. Všimněte si, že DataView je volně typované. Chcete-li odkazovat na konkrétní hodnotu sloupce, musíme předat název sloupce jako řetězec (CategoryName, v tomto případě). Obrázek 13 zobrazuje zprávu zobrazenou v `CategoryNameLabel` při zobrazení stránky. Skutečný název kategorie se samozřejmě náhodně vybere na základě `RandomCategoryDataSource` SqlDataSource na každé návštěvě stránky (včetně postbacků).

[![se zobrazí náhodně vybraný název kategorie s.](using-parameterized-queries-with-the-sqldatasource-cs/_static/image13.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image25.png)

**Obrázek 13**: zobrazí se náhodně vybraný název kategorie s ([kliknutím zobrazíte obrázek v plné velikosti).](using-parameterized-queries-with-the-sqldatasource-cs/_static/image26.png)

> [!NOTE]
> Pokud byla vlastnost `DataSourceMode` ovládacího prvku SqlDataSource nastavena na hodnotu `DataReader`, návratová hodnota z metody `Select()` by musela být převedena na `IDataReader`. Pro načtení `CategoryName` hodnoty sloupce z prvního řádku používáme kód jako:

[!code-csharp[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample12.cs)]

Při náhodném výběru kategorie se znovu připravujeme k přidání prvku GridView, který obsahuje seznam produktů kategorií.

> [!NOTE]
> Namísto použití webového ovládacího prvku popisek k zobrazení kategorie s název jsme mohli na stránku přidat FormView nebo DetailsView a vytvořit vazbu na třídě SqlDataSource. Použití popisku ale nám umožňuje prozkoumat, jak programově vyvolat příkaz SqlDataSource s `Select()` a pracovat s jeho výslednými daty v kódu.

## <a name="step-5-assigning-parameter-values-programmatically"></a>Krok 5: přiřazení hodnot parametrů prostřednictvím kódu programu

Všechny příklady, které jsme doposud viděli v tomto kurzu, použily pevně zakódované hodnoty parametru nebo jeden z předdefinovaných zdrojů parametrů (hodnota QueryString, webový ovládací prvek na stránce atd.). Parametry ovládacího prvku SqlDataSource ale lze nastavit také programově. Abychom dokončili náš aktuální příklad, potřebujeme SqlDataSource, který vrátí všechny produkty patřící do určité kategorie. Tato třída SqlDataSource bude mít parametr `CategoryID`, jehož hodnota musí být nastavena na základě hodnoty `CategoryID` sloupce vráceného `RandomCategoryDataSource`m SqlDataSource v obslužné rutině události `Page_Load`.

Začněte přidáním prvku GridView na stránku a vytvořte jeho vazby na novou třídě SqlDataSource s názvem `ProductsByCategoryDataSource`. Podobně jako v kroku 3, nakonfigurujete SqlDataSource, aby vyvolalo `GetProductsByCategory` uloženou proceduru. Rozevírací seznam pro zdroj parametrů nechejte nastavený na žádná, ale nezadávejte výchozí hodnotu, protože tuto výchozí hodnotu nastavíme programově.

[![nespecifikovat zdroj parametru nebo výchozí hodnotu](using-parameterized-queries-with-the-sqldatasource-cs/_static/image14.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image27.png)

**Obrázek 14**: nezadávejte zdroj parametru ani výchozí hodnotu ([kliknutím zobrazíte obrázek v plné velikosti](using-parameterized-queries-with-the-sqldatasource-cs/_static/image28.png)).

Po dokončení průvodce SqlDataSource by výsledný deklarativní kód měl vypadat podobně jako následující:

[!code-aspx[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample13.aspx)]

`DefaultValue` parametru `CategoryID` můžeme programově přiřadit v obslužné rutině události `Page_Load`:

[!code-csharp[Main](using-parameterized-queries-with-the-sqldatasource-cs/samples/sample14.cs)]

S tímto sčítáním stránka obsahuje prvek GridView, který zobrazuje produkty přidružené k náhodně vybrané kategorii.

[![nespecifikovat zdroj parametru nebo výchozí hodnotu](using-parameterized-queries-with-the-sqldatasource-cs/_static/image15.gif)](using-parameterized-queries-with-the-sqldatasource-cs/_static/image29.png)

**Obrázek 15**: nezadávejte zdroj parametru ani výchozí hodnotu ([kliknutím zobrazíte obrázek v plné velikosti](using-parameterized-queries-with-the-sqldatasource-cs/_static/image30.png)).

## <a name="summary"></a>Přehled

Třída SqlDataSource umožňuje vývojářům stránek definovat parametrizované dotazy, jejichž hodnoty parametrů mohou být pevně kódované, získány z předem definovaných zdrojů parametrů nebo přiřazeny programově. V tomto kurzu jsme zjistili, jak vytvořit parametrizovaný dotaz pomocí Průvodce konfigurací zdroje dat pro dotazy SQL ad hoc i pro uložené procedury. Zjistili jsme také použití pevně zakódovaných zdrojů parametrů, webového ovládacího prvku jako zdroje parametrů a programovému zadání hodnoty parametru.

Podobně jako u prvku ObjectDataSource, třída SqlDataSource také poskytuje možnosti pro úpravu jeho podkladových dat. V dalším kurzu se podíváme na to, jak definovat `INSERT`, `UPDATE`a `DELETE` příkazy ve třídě SqlDataSource. Po přidání těchto příkazů můžeme využít integrované funkce vkládání, úprav a odstraňování, které jsou součástí ovládacích prvků GridView, DetailsView a FormView.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Recenzenti potenciálních zákazníků pro tento kurz byly Scott Clyde, Randell Schmidt a Ken Pespisa. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](querying-data-with-the-sqldatasource-control-cs.md)
> [Další](inserting-updating-and-deleting-data-with-the-sqldatasource-cs.md)

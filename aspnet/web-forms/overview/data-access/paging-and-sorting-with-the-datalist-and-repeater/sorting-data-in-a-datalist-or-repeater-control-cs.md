---
uid: web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-cs
title: Řazení dat v ovládacím prvku DataList nebo Repeater (C#) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu podíváme se, jak zahrnout podporu řazení do prvku DataList a Repeater, a jak vytvořit DataList nebo Repeater, jejichž data mohou...
ms.author: riande
ms.date: 11/13/2006
ms.assetid: f52c302a-1b7c-46fe-8a13-8412c95cbf6d
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting-with-the-datalist-and-repeater/sorting-data-in-a-datalist-or-repeater-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 66a09c637d33c812b39e0ce85a552bd71665a2e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78620279"
---
# <a name="sorting-data-in-a-datalist-or-repeater-control-c"></a>Řazení dat sestavy ovládacími prvky DataList nebo Repeater (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_45_CS.exe) nebo [Stáhnout PDF](sorting-data-in-a-datalist-or-repeater-control-cs/_static/datatutorial45cs1.pdf)

> V tomto kurzu podíváme se, jak zahrnout podporu řazení do prvku DataList a Repeater a jak vytvořit DataList nebo Repeater, jejichž data lze stránkovat a seřadit.

## <a name="introduction"></a>Úvod

V [předchozím kurzu](paging-report-data-in-a-datalist-or-repeater-control-cs.md) jsme prozkoumali, jak přidat podporu stránkování do prvku DataList. Vytvořili jsme novou metodu ve třídě `ProductsBLL` (`GetProductsAsPagedDataSource`), která vrátila objekt `PagedDataSource`. Při vazbě na prvek DataList nebo Repeater by prvek DataList nebo Repeater zobrazil pouze požadovanou stránku dat. Tato technika je podobná tomu, co se používá interně ovládacími prvky GridView, DetailsView a FormView k zajištění předdefinovaných výchozích funkcí stránkování.

Kromě nabídky Podpora stránkování zahrnuje prvek GridView také podporu řazení v krabici. Prvky DataList ani Repeater neposkytují integrovanou funkci řazení; funkce řazení však lze přidat s bitem kódu. V tomto kurzu podíváme se, jak zahrnout podporu řazení do prvku DataList a Repeater a jak vytvořit DataList nebo Repeater, jejichž data lze stránkovat a seřadit.

## <a name="a-review-of-sorting"></a>Kontrola řazení

Jak jsme viděli v kurzu pro [data o stránkování a řazení dat sestavy](../paging-and-sorting/paging-and-sorting-report-data-cs.md) , ovládací prvek GridView poskytuje podporu řazení v krabici. Každé pole GridView může mít přidruženou `SortExpression`, která označuje datové pole, podle kterého se mají data řadit. Pokud je vlastnost GridView s `AllowSorting` nastavena na `true`, každé pole GridView, které má hodnotu vlastnosti `SortExpression`, má jeho hlavičku vykreslenou jako LinkButton. Když uživatel klikne na určité záhlaví pole GridView, dojde k postbacku a data jsou seřazena podle `SortExpression`pole, které jste klikli.

Ovládací prvek GridView má také vlastnost `SortExpression`, která ukládá `SortExpression` pole GridView, podle kterého se data řadí. Kromě toho vlastnost `SortDirection` označuje, zda mají být data řazena ve vzestupném nebo sestupném pořadí (Pokud uživatel klikne na konkrétní pole GridView s hlavičkou dvakrát po úspěchu, je pořadí řazení přepnuto).

Když je ovládací prvek GridView svázán s ovládacím prvkem zdroje dat, vypíná jeho `SortExpression` a `SortDirection` vlastnosti ovládacího prvku zdroje dat. Ovládací prvek zdroje dat načte data a pak je seřadí podle zadaného `SortExpression` a vlastností `SortDirection`. Po řazení dat se ovládací prvek zdroje dat vrátí do prvku GridView.

Pro replikaci této funkce pomocí ovládacích prvků DataList nebo Repeater je nutné:

- Vytvoření rozhraní pro řazení
- Zapamatujte si datové pole, podle kterého se má řadit, a zda se má seřadit ve vzestupném nebo sestupném pořadí
- Instruujte ObjectDataSource, aby data seřadila podle konkrétního datového pole.

Tyto tři úkoly budeme řešit v krocích 3 a 4. V takovém případě se podíváme, jak zahrnout podporu stránkování i řazení do prvku DataList nebo Repeater.

## <a name="step-2-displaying-the-products-in-a-repeater"></a>Krok 2: zobrazení produktů v Repeater

Než se pustíme do implementace jakékoli funkce související s řazením, nechte začít seznamem produktů v ovládacím prvku Repeater. Začněte tím, že otevřete stránku `Sorting.aspx` ve složce `PagingSortingDataListRepeater`. Přidejte ovládací prvek Repeater na webovou stránku a nastavte jeho vlastnost `ID` na hodnotu `SortableProducts`. Z inteligentní značky Repeater vytvořte nový prvek ObjectDataSource s názvem `ProductsDataSource` a nakonfigurujte jej tak, aby načetl data z metody `GetProducts()` `ProductsBLL` třídy s. V rozevíracích seznamech na kartách INSERT, UPDATE a DELETE vyberte možnost (žádná).

[![vytvořit prvek ObjectDataSource a nakonfigurovat jej pro použití metody GetProductsAsPagedDataSource ()](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image2.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image1.png)

**Obrázek 1**: vytvořte prvek ObjectDataSource a nakonfigurujte ho tak, aby používal metodu `GetProductsAsPagedDataSource()` ([kliknutím zobrazíte obrázek v plné velikosti).](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image3.png)

[![nastavení rozevíracích seznamů na kartách aktualizace, vložení a odstranění na (žádné)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image5.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image4.png)

**Obrázek 2**: nastavení rozevíracích seznamů na kartách aktualizace, vložení a odstranění na (žádné) ([kliknutím zobrazíte obrázek v plné velikosti](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image6.png))

Na rozdíl od u prvku DataList, Visual Studio automaticky nevytvoří `ItemTemplate` pro ovládací prvek Repeater po jeho svázání se zdrojem dat. Kromě toho je nutné přidat toto `ItemTemplate` deklarativně, protože inteligentní značka ovládacího prvku Repeater chybí možnost Upravit šablony, která se nachází v prvku DataList s. Umožňuje použít stejný `ItemTemplate` z předchozího kurzu, který zobrazuje název produktu, dodavatele a kategorii.

Po přidání `ItemTemplate`by měl být argument Repeat a ObjectDataSource s deklarativním označením podobný následujícímu:

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample1.aspx)]

Obrázek 3 ukazuje tuto stránku při prohlížení v prohlížeči.

[Zobrazí se ![každý název produktu, dodavatel a kategorie.](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image8.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image7.png)

**Obrázek 3**: zobrazí se každý název produktu, dodavatel a kategorie ([kliknutím zobrazíte obrázek v plné velikosti).](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image9.png)

## <a name="step-3-instructing-the-objectdatasource-to-sort-the-data"></a>Krok 3: pokyny pro prvek ObjectDataSource k řazení dat

Abychom mohli seřadit data zobrazená v OPAKOVAČI, musíme informovat prvek ObjectDataSource výrazu řazení, podle kterého by se měla data seřadit. Před tím, než prvek ObjectDataSource načte svá data, nejprve spustí svou [`Selecting` událost](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.selecting.aspx), která nám poskytne příležitost zadat výraz řazení. Obslužné rutině události `Selecting` je předán objekt typu [`ObjectDataSourceSelectingEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.aspx), který má vlastnost s názvem [`Arguments`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourceselectingeventargs.arguments.aspx) typu [`DataSourceSelectArguments`](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.aspx). Třída `DataSourceSelectArguments` je navržena tak, aby předávala požadavky související s daty od příjemce dat do ovládacího prvku zdroje dat a obsahuje [vlastnost`SortExpression`](https://msdn.microsoft.com/library/system.web.ui.datasourceselectarguments.sortexpression.aspx).

Chcete-li předat informace o řazení ze stránky ASP.NET do prvku ObjectDataSource, vytvořte obslužnou rutinu události pro událost `Selecting` a použijte následující kód:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample2.cs)]

Hodnota *SortExpression* by měla být přiřazena názvu datového pole, podle kterého se data mají seřadit (například NázevVýrobku). Neexistuje žádná vlastnost související s směrem řazení, takže pokud chcete seřadit data v sestupném pořadí, přidejte řetězec DESC k hodnotě *SortExpression* (například NázevVýrobku DESC).

Pokračujte a vyzkoušejte některé jiné pevně zakódované hodnoty pro *SortExpression* a otestujte výsledky v prohlížeči. Jak ukazuje obrázek 4, při použití příkazu ProductName DESC jako *SortExpression*jsou produkty seřazené podle jejich názvu v opačném abecedním pořadí.

[![produktů seřazené podle jejich názvu v obráceném abecedním pořadí](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image11.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image10.png)

**Obrázek 4**: produkty jsou seřazené podle jejich názvu v obráceném abecedním pořadí ([kliknutím zobrazíte obrázek v plné velikosti](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image12.png)).

## <a name="step-4-creating-the-sorting-interface-and-remembering-the-sort-expression-and-direction"></a>Krok 4: vytvoření rozhraní řazení a pamatujce si výraz a směr řazení

Zapnutí podpory řazení v prvku GridView převede každý text záhlaví pole, který lze seřadit, do prvku LinkButton, který po kliknutí vyřadí data odpovídajícím způsobem. Takové rozhraní řazení dává smysl pro prvek GridView, kde jsou data ve sloupcích správně rozložena. Pro ovládací prvky DataList a Repeater je však potřeba jiné rozhraní řazení. Běžné rozhraní pro řazení seznamu dat (na rozdíl od mřížky dat) je rozevírací seznam, který poskytuje pole, podle kterých lze data seřadit. Umožňuje implementovat takové rozhraní pro tento kurz.

Přidejte webový ovládací prvek DropDownList nad `SortableProducts` a nastavte jeho vlastnost `ID` na `SortBy`. V okno Vlastnosti klikněte na elipsy ve vlastnosti `Items` a zobrazte tak editor kolekce ListItem. Přidejte `ListItem` s a seřaďte data podle polí `ProductName`, `CategoryName`a `SupplierName`. Přidejte také `ListItem` k seřazení produktů podle jejich názvu v opačném abecedním pořadí.

Vlastnosti `ListItem` `Text` lze nastavit na libovolnou hodnotu (například název), ale vlastnosti `Value` musí být nastaveny na název datového pole (například NázevVýrobku). Chcete-li výsledky seřadit v sestupném pořadí, přidejte řetězec DESC k názvu datového pole, jako je například NázevVýrobku DESC.

![Přidat ListItem pro každé pole dat, která lze seřadit](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image13.png)

**Obrázek 5**: Přidání `ListItem` pro každé pole s řazením dat

Nakonec přidejte ovládací prvek webové tlačítko napravo od ovládacího prvku DropDownList. Nastavte jeho `ID` na `RefreshRepeater` a jeho vlastnost `Text` na hodnotu aktualizovat.

Po vytvoření `ListItem` s a přidání tlačítka Aktualizovat by měla být deklarativní syntaxe DropDownList a tlačítka s podobným způsobem vypadat takto:

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample3.aspx)]

S kompletním řazením DropDownList je potřeba aktualizovat obslužnou rutinu události ObjectDataSource s `Selecting` tak, aby používala vybranou vlastnost `SortBy``ListItem` s `Value` na rozdíl od pevně zakódovaného výrazu řazení.

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample4.cs)]

V tomto okamžiku se při první návštěvě stránky budou produkty zpočátku seřadit podle pole `ProductName` dat, protože `SortBy` `ListItem` vybraná ve výchozím nastavení (viz obrázek 6). Výběr jiné možnosti řazení, jako je například kategorie a kliknutí na tlačítko Aktualizovat, způsobí postback a znovu seřadí data podle názvu kategorie, jak ukazuje obrázek 7.

[![jsou produkty zpočátku seřazené podle jména](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image15.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image14.png)

**Obrázek 6**: produkty jsou zpočátku seřazené podle jejich názvu ([kliknutím zobrazíte obrázek v plné velikosti](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image16.png)).

[![jsou teď produkty seřazené podle kategorie.](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image18.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image17.png)

**Obrázek 7**: produkty jsou nyní seřazené podle kategorie ([kliknutím zobrazíte obrázek v plné velikosti](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image19.png)).

> [!NOTE]
> Kliknutím na tlačítko Aktualizovat dojde k automatickému seřazení dat, protože stav zobrazení opakování s byl zakázán, což způsobí, že se má opakovat změna vazby na zdroj dat při každém postbacku. Pokud jste opustili stav zobrazení opakovače s povoleným, změna rozevíracího seznamu řazení nebude mít vliv na pořadí řazení. Chcete-li tento problém napravit, vytvořte obslužnou rutinu události pro tlačítko Obnovit `Click` událost a znovu navažte na svůj zdroj dat (voláním metody Repeater s `DataBind()`).

## <a name="remembering-the-sort-expression-and-direction"></a>Pamatuje výraz řazení a směr

Při vytváření třídicího prvku DataList nebo opakovače na stránce, kde může dojít k neřazení souvisejících postbacků, je nutné, aby byl výraz řazení a směr v rámci zpětného volání. Představte si například, že v tomto kurzu jsme aktualizovali Repeater, aby se pro každý produkt zahrnulo tlačítko pro odstranění. Když uživatel klikne na tlačítko Odstranit, spustíme nějaký kód, který odstraní vybraný produkt a pak znovu naváže data na Repeater. Pokud nejsou podrobnosti řazení uchovány v rámci zpětného odeslání, data zobrazená na obrazovce se vrátí k původnímu pořadí řazení.

Pro tento kurz implicitně uloží výraz řazení a směr do svého stavu zobrazení pro nás. Pokud jsme používali jiné rozhraní řazení s jedním z nich, řekněme, že k různým možnostem řazení potřebujeme pamatovat si pořadí řazení napříč zpětnými odesláními. To lze provést uložením parametrů řazení ve stavu zobrazení stránky, zahrnutím parametru řazení do řetězce dotazu nebo prostřednictvím některé jiné techniky trvalosti stavu.

V budoucích příkladech v tomto kurzu se seznámíte s tím, jak zachovat podrobnosti o řazení ve stavu zobrazení stránky s.

## <a name="step-5-adding-sorting-support-to-a-datalist-that-uses-default-paging"></a>Krok 5: Přidání podpory řazení do prvku DataList, který používá výchozí stránkování

V [předchozím kurzu](paging-report-data-in-a-datalist-or-repeater-control-cs.md) jsme prozkoumali, jak implementovat výchozí stránkování pomocí prvku DataList. Tento předchozí příklad můžete využít k tomu, aby se zahrnula možnost řazení stránkovaných dat. Začněte tím, že otevřete `SortingWithDefaultPaging.aspx` a `Paging.aspx` stránky ve složce `PagingSortingDataListRepeater`. Na stránce `Paging.aspx` klikněte na tlačítko zdroj a zobrazte tak deklarativní označení stránky. Zkopíruje vybraný text (viz obrázek 8) a vloží jej do deklarativní značky `SortingWithDefaultPaging.aspx` mezi značkami `<asp:Content>`.

[![replikovat deklarativní označení v &lt;ASP: obsah&gt; značky z stránkování. aspx do SortingWithDefaultPaging. aspx](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image21.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image20.png)

**Obrázek 8**: replikace deklarativní značky v `<asp:Content>` značek z `Paging.aspx` na `SortingWithDefaultPaging.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image22.png))

Po zkopírování deklarativní značky zkopírujte metody a vlastnosti ve třídě `Paging.aspx` stránky s kódem na pozadí do třídy kódu na pozadí pro `SortingWithDefaultPaging.aspx`. Dále si chvíli počkejte, než se zobrazí stránka `SortingWithDefaultPaging.aspx` v prohlížeči. Mělo by se jednat o stejné funkce a vzhled jako `Paging.aspx`.

## <a name="enhancing-productsbll-to-include-a-default-paging-and-sorting-method"></a>Vylepšení ProductsBLL, aby zahrnovalo výchozí metodu stránkování a řazení

V předchozím kurzu jsme vytvořili metodu `GetProductsAsPagedDataSource(pageIndex, pageSize)` ve třídě `ProductsBLL`, která vrátila objekt `PagedDataSource`. Tento objekt `PagedDataSource` byl vyplněn *všemi* produkty (prostřednictvím metody `GetProducts()` knihoven BLL s), ale při vazbě na prvek DataList byly zobrazeny pouze záznamy odpovídající zadaným vstupním parametrům *pageIndex* a *PageSize* .

Dříve v tomto kurzu jsme přidali podporu řazení zadáním výrazu řazení z obslužné rutiny události `Selecting` ObjectDataSource s. To funguje dobře, když je prvek ObjectDataSource vrácen objekt, který lze seřadit, jako `ProductsDataTable` vrácenou metodou `GetProducts()`. Objekt `PagedDataSource` vrácený metodou `GetProductsAsPagedDataSource` však nepodporuje řazení vnitřního zdroje dat. Místo toho je potřeba *před* vložením do `PagedDataSource`seřadit výsledky vrácené z metody `GetProducts()`.

Chcete-li to provést, vytvořte novou metodu ve třídě `ProductsBLL` `GetProductsSortedAsPagedDataSource(sortExpression, pageIndex, pageSize)`. Chcete-li seřadit `ProductsDataTable` vracené metodou `GetProducts()`, zadejte vlastnost `Sort` jejího výchozího `DataTableView`:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample5.cs)]

Metoda `GetProductsSortedAsPagedDataSource` se od `GetProductsAsPagedDataSource` metody vytvořená v předchozím kurzu liší jenom mírně. Konkrétně `GetProductsSortedAsPagedDataSource` akceptuje další vstupní parametr `sortExpression` a přiřadí tuto hodnotu k vlastnosti `Sort` `ProductDataTable` s `DefaultView`. Několik řádků kódu později je `PagedDataSource` objekt s zdrojem dat, přiřazen `ProductDataTable` `DefaultView`.

## <a name="calling-the-getproductssortedaspageddatasource-method-and-specifying-the-value-for-the-sortexpression-input-parameter"></a>Volání metody GetProductsSortedAsPagedDataSource a určení hodnoty pro vstupní parametr SortExpression

Po dokončení metody `GetProductsSortedAsPagedDataSource` je dalším krokem poskytnutí hodnoty pro tento parametr. Prvek ObjectDataSource v `SortingWithDefaultPaging.aspx` je aktuálně nakonfigurován pro volání metody `GetProductsAsPagedDataSource` a předá dva vstupní parametry prostřednictvím jejich dvou `QueryStringParameters`, které jsou zadány v kolekci `SelectParameters`. Tyto dva `QueryStringParameters` označují, že zdroj pro parametry `GetProductsAsPagedDataSource` metoda s *pageIndex* a *PageSize* pocházejí z polí QueryString `pageIndex` a `pageSize`.

Aktualizujte vlastnost ObjectDataSource `SelectMethod` tak, aby vyvolala novou metodu `GetProductsSortedAsPagedDataSource`. Pak přidejte nový `QueryStringParameter` tak, aby byl vstupní parametr *SortExpression* k dispozici z pole QueryString `sortExpression`. Nastavte `QueryStringParameter` s `DefaultValue` na NázevVýrobku.

Po těchto změnách by deklarativní označení ObjectDataSource s mělo vypadat takto:

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample6.aspx)]

V tomto okamžiku bude stránka `SortingWithDefaultPaging.aspx` seřadit výsledky abecedně podle názvu produktu (viz obrázek 9). Důvodem je, že ve výchozím nastavení je hodnota NázevVýrobku předána jako parametr `GetProductsSortedAsPagedDataSource` *SortExpression* metoda s.

[![ve výchozím nastavení jsou výsledky seřazené podle NázevVýrobku.](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image24.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image23.png)

**Obrázek 9**: ve výchozím nastavení jsou výsledky seřazené podle `ProductName` ([kliknutím zobrazíte obrázek v plné velikosti).](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image25.png)

Pokud ručně přidáte `sortExpression` pole QueryString, například `SortingWithDefaultPaging.aspx?sortExpression=CategoryName` výsledky budou seřazeny podle zadaného `sortExpression`. Tento parametr `sortExpression` však není při přesunu na jinou stránku dat zahrnut v dotazu QueryString. Ve skutečnosti se kliknutím na tlačítko Další nebo poslední stránky vrátíte zpátky na `Paging.aspx`! Kromě toho momentálně neexistuje žádné rozhraní řazení. Jediný způsob, jakým uživatel může změnit pořadí řazení stránkovaných dat, je manipulace s řetězcem dotazu přímo.

## <a name="creating-the-sorting-interface"></a>Vytvoření rozhraní řazení

Nejdřív je potřeba aktualizovat metodu `RedirectUser`, aby uživatel mohl `SortingWithDefaultPaging.aspx` (místo `Paging.aspx`) a zahrnout `sortExpression` hodnotu do řetězce dotazu. Měli bychom také přidat vlastnost `SortExpression` s názvem stránky jen pro čtení, na úrovni stránky. Tato vlastnost, podobně jako `PageIndex` a `PageSize` vlastnosti vytvořené v předchozím kurzu, vrátí hodnotu pole `sortExpression` QueryString, pokud existuje, a výchozí hodnotu (ProductName) v opačném případě.

V současné době metoda `RedirectUser` přijímá pouze jeden vstupní parametr index stránky, která se má zobrazit. Nicméně mohou nastat situace, kdy chceme uživatele přesměrovat na konkrétní stránku dat pomocí výrazu řazení, který není zadán v řetězci QueryString. V okamžiku vytvoříme rozhraní řazení pro tuto stránku, které bude obsahovat řadu webových ovládacích prvků tlačítek pro řazení dat podle zadaného sloupce. Když se klikne na jedno z těchto tlačítek, chceme přesměrovat uživatele na příslušnou hodnotu řadicího výrazu. Chcete-li poskytnout tuto funkci, vytvořte dvě verze `RedirectUser` metody. První z nich by měl přijmout jenom index stránky, aby se zobrazila, zatímco druhá druhá přijímá index stránky a výraz řazení.

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample7.cs)]

V prvním příkladu v tomto kurzu jsme vytvořili rozhraní řazení pomocí ovládacího prvkem DropDownList. V tomto příkladu můžete použít tři webové ovládací prvky tlačítka umístěné nad prvek DataList One pro řazení podle `ProductName`, jeden pro `CategoryName`a druhý pro `SupplierName`. Přidejte tři webové ovládací prvky tlačítka a patřičným nastavením vlastností `ID` a `Text`:

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample8.aspx)]

Dále vytvořte obslužnou rutinu události `Click` pro každou. Obslužné rutiny události by měly volat metodu `RedirectUser` a vracet uživatele na první stránku pomocí vhodného výrazu řazení.

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample9.cs)]

Při první návštěvě stránky se data seřadí podle názvu produktu abecedně (odkazují zpátky na obrázek 9). Kliknutím na tlačítko Další přejdete na druhou stránku dat a potom kliknete na tlačítko Seřadit podle kategorie. Tím se vrátíme na první stránku dat, která je seřazená podle názvu kategorie (viz obrázek 10). Podobně kliknutím na tlačítko Seřadit podle dodavatele seřadí data podle dodavatele počínaje první stránkou dat. Výběr řazení se pamatuje, protože data jsou stránkovaná. Obrázek 11 ukazuje stránku po řazení podle kategorie a přechod na třináctou stránku dat.

[![produkty jsou seřazené podle kategorie](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image27.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image26.png)

**Obrázek 10**: produkty jsou seřazené podle kategorie ([kliknutím zobrazíte obrázek v plné velikosti](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image28.png)).

[![výraz řazení se pamatuje při stránkování prostřednictvím dat.](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image30.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image29.png)

**Obrázek 11**: výraz řazení se při stránkování přes data pamatuje ([kliknutím zobrazíte obrázek v plné velikosti](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image31.png)).

## <a name="step-6-custom-paging-through-records-in-a-repeater"></a>Krok 6: vlastní stránkování prostřednictvím záznamů v Repeater

Příklad DataList vyhodnocený v kroku 5 stránky prostřednictvím svých dat pomocí neefektivní výchozí techniky stránkování. Když je stránkování po dostatečně velkých objemech dat, je nezbytné, aby se použilo vlastní stránkování. V rámci [efektivního stránkování až po velké objemy dat](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md) a [seřazení vlastních](../paging-and-sorting/sorting-custom-paged-data-cs.md) výukových kurzů s daty jsme prozkoumali rozdíly mezi výchozími a vlastními metodami STRÁNKOVÁNÍ a vytvoření v knihoven BLL pro použití vlastních stránkování a řazení vlastních stránkovaných dat. Zejména v těchto dvou předchozích kurzech jsme přidali následující tři metody do třídy `ProductsBLL`:

- `GetProductsPaged(startRowIndex, maximumRows)` vrátí konkrétní podmnožinu záznamů začínající na *StartRowIndex* a nepřekračuje *MaximumRows*.
- `GetProductsPagedAndSorted(sortExpression, startRowIndex, maximumRows)` vrátí konkrétní podmnožinu záznamů seřazených podle zadaného vstupního parametru *SortExpression* .
- `TotalNumberOfProducts()` poskytuje celkový počet záznamů v tabulce databáze `Products`.

Tyto metody lze použít k efektivnímu vytvoření stránky a k řazení dat pomocí ovládacího prvku DataList nebo Repeater. K ilustraci je možné začít vytvořením ovládacího prvku Repeater s podporou vlastního stránkování; Pak přidáme možnosti řazení.

Ve složce `PagingSortingDataListRepeater` otevřete stránku `SortingWithCustomPaging.aspx` a přidejte do ní Repeater a nastavte její vlastnost `ID` na `Products`. Z inteligentní značky Repeater vytvořte nový prvek ObjectDataSource s názvem `ProductsDataSource`. Nakonfigurujte ho tak, aby vybral jeho data z `GetProductsPaged` metody `ProductsBLL` třídy s.

[![nakonfigurovat prvek ObjectDataSource tak, aby používal metodu ProductsBLL třídy s GetProductsPaged](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image33.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image32.png)

**Obrázek 12**: Konfigurace prvku ObjectDataSource pro použití `GetProductsPaged` metody `ProductsBLL` třídy s ([kliknutím zobrazíte obrázek v plné velikosti](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image34.png))

V rozevíracích seznamech na kartě aktualizovat, vložit a odstranit klikněte na možnost (žádné) a potom klikněte na tlačítko Další. Průvodce konfigurací zdroje dat teď vyzve k zadání zdrojů `GetProductsPaged` metod s *StartRowIndex* a vstupními parametry *MaximumRows* . Ve skutečnosti jsou tyto vstupní parametry ignorovány. Místo toho budou hodnoty *StartRowIndex* a *MaximumRows* předány prostřednictvím vlastnosti `Arguments` v obslužné rutině prvku ObjectDataSource s `Selecting`, stejně jako způsob, jakým jsme určili *SortExpression* v tomto kurzu s první ukázkou. Proto ponechte rozevírací seznamy zdroje parametrů v nastavení Průvodce na žádné.

[![ponechat zdroje parametrů nastavené na None](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image36.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image35.png)

**Obrázek 13**: ponechte nastavené zdroje parametrů na None ([kliknutím zobrazíte obrázek v plné velikosti).](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image37.png)

> [!NOTE]
> Nenastavujte *vlastnost* `EnablePaging` ObjectDataSource s na `true`. Prvek ObjectDataSource bude mít za následek automatické zahrnutí vlastních parametrů *StartRowIndex* a *MaximumRows* do seznamu existujících parametrů `SelectMethod` s. Vlastnost `EnablePaging` je užitečná při vázání vlastních stránkovaných dat na ovládací prvek GridView, DetailsView nebo FormView, protože tyto ovládací prvky očekávají určité chování prvku ObjectDataSource, který je k dispozici pouze v případě, že je `true`vlastnost `EnablePaging`. Vzhledem k tomu, že je nutné ručně přidat podporu stránkování pro prvek DataList a Repeater, nechte tuto vlastnost nastavenou na `false` (výchozí), jak se v rámci naší ASP.NET stránky zanesli k potřebným funkcím.

Nakonec definujte `ItemTemplate` Repeater, aby se zobrazil název produktu, kategorie a dodavatel. Po těchto změnách by deklarativní syntaxe Repeater a ObjectDataSource s vypadala podobně jako v následujícím příkladu:

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample10.aspx)]

Chvíli počkejte, než navštívíte stránku v prohlížeči, a Všimněte si, že se nevrátí žádné záznamy. Je to proto, že jsme zatím zadali hodnoty parametrů *StartRowIndex* a *MaximumRows* ; Proto jsou hodnoty 0 předávány pro obě. Chcete-li zadat tyto hodnoty, vytvořte obslužnou rutinu události pro událost ObjectDataSource `Selecting` a nastavte tyto hodnoty programově na pevně zakódované hodnoty 0 a 5 v uvedeném pořadí:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample11.cs)]

Při této změně zobrazí stránka při zobrazení v prohlížeči prvních pět produktů.

[![se zobrazí prvních pět záznamů.](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image39.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image38.png)

**Obrázek 14**: zobrazí se prvních pět záznamů ([kliknutím zobrazíte obrázek v plné velikosti](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image40.png)).

> [!NOTE]
> Produkty uvedené na obrázku 14 se seřadí podle názvu produktu, protože `GetProductsPaged` uložený postup, který provádí efektivní vlastní stránkovací dotaz, vyřadí výsledky podle `ProductName`.

Aby bylo možné uživateli procházet stránky, musíme sledovat index počátečního řádku a maximální počet řádků a zapamatovat si tyto hodnoty napříč zpětnými voláními. Ve výchozím příkladu stránkování používali pole QueryString k uchování těchto hodnot; v této ukázce je možné zachovat tyto informace ve stavu zobrazení stránky s. Vytvořte následující dvě vlastnosti:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample12.cs)]

Dále aktualizujte kód v obslužné rutině události výběru tak, aby místo pevně kódovaných hodnot 0 a 5 používala vlastnosti `StartRowIndex` a `MaximumRows`:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample13.cs)]

V tomto okamžiku se na naší stránce pořád zobrazuje prvních pět záznamů. Avšak u těchto vlastností je nově připraveno vytvořit rozhraní stránkování.

## <a name="adding-the-paging-interface"></a>Přidání rozhraní stránkování

Pojďme použít stejné první, předchozí, další, poslední rozhraní pro stránkování, které se používá ve výchozím příkladu stránkování, včetně webového ovládacího prvku popisek, který zobrazuje zobrazovanou stránku dat a celkový počet stránek, které existují. Přidejte čtyři webové ovládací prvky tlačítka a popisek pod Repeater.

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample14.aspx)]

Dále vytvořte obslužné rutiny událostí `Click` pro čtyři tlačítka. Po kliknutí na jedno z těchto tlačítek musíme aktualizovat `StartRowIndex` a znovu navazovat data na Repeater. Kód pro první, předchozí a další tlačítka jsou dostatečně snadné, ale pro poslední tlačítko, jak pro poslední stránku dat určit index počátečního řádku? Aby bylo možné tento index vypočítat i v případě, že chcete určit, zda má být povoleno tlačítko Další a poslední, musíme zjistit, kolik záznamů je celkem na straně sebe. To můžeme určit voláním metody `ProductsBLL` třídy s `TotalNumberOfProducts()`. Umožňuje vytvořit vlastnost na úrovni stránky jen pro čtení s názvem `TotalRowCount`, která vrací výsledky `TotalNumberOfProducts()` metody:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample15.cs)]

Pomocí této vlastnosti teď můžeme určit index počátečního řádku s poslední stránkou. Konkrétně se jedná o celočíselný výsledek `TotalRowCount` minus 1 děleno `MaximumRows`vynásobené `MaximumRows`. Nyní můžeme zapisovat obslužné rutiny událostí `Click` pro čtyři tlačítka rozhraní pro stránkování:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample16.cs)]

Nakonec musíme při zobrazení poslední stránky vypnout první a předchozí tlačítka ve stránkovacím rozhraní při zobrazení první stránky dat a tlačítka Další a poslední. K tomu je potřeba přidat následující kód do obslužné rutiny události `Selecting` ObjectDataSource s:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample17.cs)]

Po přidání těchto obslužných rutin událostí `Click` a kódu pro povolení nebo zakázání prvků stránkovacího rozhraní v závislosti na aktuálním indexu počátečního řádku otestujte stránku v prohlížeči. Jak ukazuje obrázek 15, při první návštěvě stránky se neaktivují první a předchozí tlačítka. Kliknutím na další zobrazíte druhou stránku dat a při kliknutí na poslední se zobrazí poslední stránka (viz obrázek 16 a 17). Při zobrazení poslední stránky dat se vypne tlačítko Další i poslední.

[Při zobrazení první stránky produktů jsou zakázané ![předchozí a poslední tlačítka](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image42.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image41.png)

**Obrázek 15**: při prohlížení první stránky produktů je vypnuto tlačítko předchozí a poslední ([kliknutím zobrazíte obrázek v plné velikosti](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image43.png))

[![se zobrazí druhá stránka produktů](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image45.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image44.png)

**Obrázek 16**: zobrazí se druhá stránka produktů ([kliknutím zobrazíte obrázek v plné velikosti).](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image46.png)

[![kliknutí na poslední zobrazí poslední stránku dat.](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image48.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image47.png)

**Obrázek 17**: po kliknutí na poslední se zobrazí poslední stránka dat (Kliknutím zobrazíte[obrázek v plné velikosti).](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image49.png)

## <a name="step-7-including-sorting-support-with-the-custom-paged-repeater"></a>Krok 7: včetně podpory řazení u vlastního stránkovaného opakovače

Po implementaci vlastního stránkování se teď znovu připravujeme k zahrnutí podpory řazení. Metoda `ProductsBLL` třídy s `GetProductsPagedAndSorted` má stejné vstupní parametry *StartRowIndex* a *MaximumRows* jako `GetProductsPaged`, ale umožňuje další vstupní parametr *SortExpression* . Pokud chcete použít metodu `GetProductsPagedAndSorted` z `SortingWithCustomPaging.aspx`, musíme provést následující kroky:

1. Změňte vlastnost `SelectMethod` ObjectDataSource s z `GetProductsPaged` na `GetProductsPagedAndSorted`.
2. Přidejte objekt *sortExpression* `Parameter` do kolekce `SelectParameters` ObjectDataSource s.
3. Vytvořte soukromou vlastnost `SortExpression` na úrovni stránky, která bude zachována jeho hodnotu napříč zpětnými voláními ve stavu zobrazení stránky.
4. Aktualizujte obslužnou rutinu události ObjectDataSource s `Selecting` pro přiřazení parametru ObjectDataSource s *SortExpression* hodnotu vlastnosti `SortExpression` na úrovni stránky.
5. Vytvořte rozhraní řazení.

Začněte tím, že aktualizujete vlastnost `SelectMethod` ObjectDataSource s a přidáte `Parameter`*SortExpression* . Ujistěte se, že vlastnost *sortExpression* `Parameter` s `Type` je nastavená na `String`. Po dokončení těchto prvních dvou úkolů by deklarativní označení ObjectDataSource s mělo vypadat takto:

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample18.aspx)]

Dále potřebujeme vlastnost `SortExpression` na úrovni stránky, jejíž hodnota je serializovaná na zobrazení stavu. Pokud nebyla nastavena žádná hodnota výrazu řazení, použijte jako výchozí výchozí hodnotu NázevVýrobku:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample19.cs)]

Předtím, než prvek ObjectDataSource vyvolá metodu `GetProductsPagedAndSorted` potřebujeme nastavit `Parameter` *SortExpression* na hodnotu vlastnosti `SortExpression`. V obslužné rutině události `Selecting` přidejte následující řádek kódu:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample20.cs)]

To vše zůstává k implementaci rozhraní řazení. Stejně jako v posledním příkladu se musí mít rozhraní řazení implementované pomocí tří webových ovládacích prvků na tlačítku, které umožní uživateli seřadit výsledky podle názvu produktu, kategorie nebo dodavatele.

[!code-aspx[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample21.aspx)]

Vytvořte obslužné rutiny událostí `Click` pro tyto tři ovládací prvky tlačítka. V obslužné rutině události obnovte `StartRowIndex` na 0, nastavte `SortExpression` na odpovídající hodnotu a znovu Navažte data na Repeater:

[!code-csharp[Main](sorting-data-in-a-datalist-or-repeater-control-cs/samples/sample22.cs)]

To všechno je! I když bylo k dispozici několik kroků pro získání vlastního stránkování a seřazení, byly kroky velmi podobné těm, které jsou potřeba pro výchozí stránkování. Obrázek 18 zobrazuje produkty při prohlížení poslední stránky dat, pokud jsou seřazeny podle kategorie.

[![se zobrazí poslední stránka dat seřazená podle kategorie.](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image51.png)](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image50.png)

**Obrázek 18**: zobrazí se poslední stránka dat seřazená podle kategorie ([kliknutím zobrazíte obrázek v plné velikosti).](sorting-data-in-a-datalist-or-repeater-control-cs/_static/image52.png)

> [!NOTE]
> V předchozích příkladech se při třídění podle dodavatele dodavatele použil jako výraz řazení. Pro implementaci vlastního stránkování ale musíme použít CompanyName. Důvodem je skutečnost, že úložná procedura zodpovědná za implementaci vlastního stránkování `GetProductsPagedAndSorted` předá výraz řazení do klíčového slova `ROW_NUMBER()`, klíčové slovo `ROW_NUMBER()` vyžaduje skutečný název sloupce, nikoli alias. Proto je nutné použít `CompanyName` (název sloupce v tabulce `Suppliers`) místo aliasu používaného v dotazu `SELECT` (`SupplierName`) pro výraz řazení.

## <a name="summary"></a>Souhrn

Prvky DataList ani Repeat nenabízejí integrovanou podporu pro řazení, ale s bitem kódu a vlastním rozhraním řazení. Tyto funkce lze přidat. Při implementaci řazení, ale ne stránkování, lze výraz řazení určit prostřednictvím objektu `DataSourceSelectArguments` předaného do metody ObjectDataSource s `Select`. Tuto vlastnost `DataSourceSelectArguments` objektů `SortExpression` lze přiřadit v obslužné rutině události ObjectDataSource s `Selecting`.

Chcete-li přidat možnosti řazení do prvku DataList nebo Repeater, který již poskytuje podporu stránkování, nejjednodušší způsob je přizpůsobení vrstvy obchodní logiky tak, aby zahrnovala metodu, která přijímá řadicí výraz. Tyto informace lze následně předat prostřednictvím parametru v prvku ObjectDataSource s `SelectParameters`.

V tomto kurzu se dokončí naše zkoumání stránkování a řazení pomocí ovládacího prvku DataList a Repeater. Náš další a finální kurz vám podíváme se, jak přidat webové ovládací prvky tlačítka do šablon DataList a Repeater s, aby bylo možné poskytovat některé vlastní uživatelem iniciované funkce na základě jednotlivých položek.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolorovi realizace tohoto kurzu bylo David Suru. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](paging-report-data-in-a-datalist-or-repeater-control-cs.md)
> [Další](paging-report-data-in-a-datalist-or-repeater-control-vb.md)

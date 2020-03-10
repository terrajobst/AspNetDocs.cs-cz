---
uid: web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb
title: Zobrazení souhrnných informací v zápatí prvku GridView (VB) | Microsoft Docs
author: rick-anderson
description: Souhrnné informace se často zobrazují v dolní části sestavy na souhrnném řádku. Ovládací prvek GridView může obsahovat řádek zápatí, do jehož buněk můžeme použít...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 41c818b7-603a-402b-8847-890a63547b6f
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb
msc.type: authoredcontent
ms.openlocfilehash: c208b4a756f5700be46eec924d8cf8f49b9d2507
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78595912"
---
# <a name="displaying-summary-information-in-the-gridviews-footer-vb"></a>Zobrazení souhrnných informací v zápatí prvku GridView (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_15_VB.exe) nebo [Stáhnout PDF](displaying-summary-information-in-the-gridview-s-footer-vb/_static/datatutorial15vb1.pdf)

> Souhrnné informace se často zobrazují v dolní části sestavy na souhrnném řádku. Ovládací prvek GridView může obsahovat řádek zápatí, do jehož buněk můžeme programově vložit agregovaná data. V tomto kurzu uvidíme, jak zobrazit agregovaná data v tomto řádku zápatí.

## <a name="introduction"></a>Úvod

Kromě toho, že se každý z cen produktů, jednotky na skladě, jednotky na objednávce a změnit pořadí úrovní, může uživatel také zajímat o agregované informace, jako je průměrná cena, celkový počet jednotek na skladě atd. Tyto souhrnné informace se často zobrazují v dolní části sestavy na souhrnném řádku. Ovládací prvek GridView může obsahovat řádek zápatí, do jehož buněk můžeme programově vložit agregovaná data.

Tato úloha představuje tři problémy:

1. Konfigurace prvku GridView pro zobrazení řádku zápatí
2. Určení souhrnných dat; To znamená, Jak vypočítám průměrnou cenu nebo celkový součet jednotek v zásobách?
3. Vložení souhrnných dat do příslušných buněk na řádku zápatí

V tomto kurzu si ukážeme, jak tyto problémy překonat. Konkrétně vytvoříme stránku se seznamem kategorií v rozevíracím seznamu s produkty vybrané kategorie zobrazené v prvku GridView. Prvek GridView bude obsahovat řádek zápatí, který zobrazuje průměrnou cenu a celkový počet jednotek v zásobách a pořadí pro produkty v této kategorii.

[![souhrnné informace se zobrazí v řádku zápatí prvku GridView.](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image2.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image1.png)

**Obrázek 1**: zobrazení souhrnných informací v řádku zápatí prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image3.png))

V tomto kurzu se svým kategoriím na rozhraní hlavní/podrobné prostředí staví na konceptech, které jsou popsané v předchozím [filtrování hlavního/podrobného filtru s](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md) kurzem DropDownList. Pokud jste ještě nepracovali v předchozím kurzu, udělejte to prosím ještě před tím, než budete pokračovat s tímto.

## <a name="step-1-adding-the-categories-dropdownlist-and-products-gridview"></a>Krok 1: Přidání ovládacího prvku kategorie DropDownList a Products

Před tím, než se rozhodnete o dodržovali přidáním souhrnných informací do zápatí prvku GridView, je nejdříve třeba vytvořit sestavu hlavní/podrobnosti. Po dokončení tohoto prvního kroku se podíváme na to, jak zahrnout souhrnná data.

Začněte tím, že otevřete stránku `SummaryDataInFooter.aspx` ve složce `CustomFormatting`. Přidejte ovládací prvek DropDownList a nastavte jeho `ID` na `Categories`. Potom klikněte na odkaz zvolit zdroj dat z inteligentní značky DropDownList a přidejte nový prvek ObjectDataSource s názvem `CategoriesDataSource`, který vyvolá metodu `GetCategories()` `CategoriesBLL` třídy.

[![přidat nový prvek ObjectDataSource s názvem CategoriesDataSource](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image5.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image4.png)

**Obrázek 2**: Přidání nového prvku ObjectDataSource s názvem `CategoriesDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image6.png))

[![mají prvek ObjectDataSource vyvolat metodu GetCategories () třídy CategoriesBLL](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image8.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image7.png)

**Obrázek 3**: Chcete-li, aby prvek ObjectDataSource vyvolal metodu `GetCategories()` `CategoriesBLL` třídy ([kliknutím zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image9.png))

Po nakonfigurování prvku ObjectDataSource se Průvodce vrátí do Průvodce konfigurací zdroje dat DropDownList, ze kterého musíme zadat, jaká hodnota datového pole by měla být zobrazena a který z nich musí odpovídat hodnotě `ListItem` ovládacího prvku DropDownList. Zobrazí se pole `CategoryName` a jako hodnotu použije `CategoryID`.

[![použít pole CategoryName a KódKategorie jako text a hodnotu pro položky ListItems, v uvedeném pořadí](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image11.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image10.png)

**Obrázek 4**: použijte pole `CategoryName` a `CategoryID` jako `Text` a `Value` pro `ListItem` s ([kliknutím zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image12.png)).

V tuto chvíli máme DropDownList (`Categories`), ve kterém jsou uvedené kategorie v systému. Teď je potřeba přidat prvek GridView, který obsahuje seznam produktů, které patří do vybrané kategorie. Než budeme, ale chvíli počkejte, než v inteligentní značce DropDownList zkontrolujete zaškrtávací políčko Povolit automatické odeslání. Jak je popsáno v tématu *filtrování hlavního/podrobného ovládacího prvku DropDownList* , nastavením vlastnosti `AutoPostBack` ovládacího prvku dropdownlist na `True` bude stránka publikována při každém změně hodnoty DropDownList. Tím dojde k aktualizaci prvku GridView a zobrazení těchto produktů pro nově vybranou kategorii. Pokud je vlastnost `AutoPostBack` nastavena na hodnotu `False` (výchozí nastavení), změna kategorie nezpůsobí postback, a proto nebude aktualizovat uvedené produkty.

[![zaškrtněte políčko Povolit AutoPostBack v inteligentní značce DropDownList.](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image14.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image13.png)

**Obrázek 5**: zaškrtněte políčko Povolit automatické odeslání v inteligentní značce DropDownList ([kliknutím zobrazíte obrázek v plné velikosti).](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image15.png)

Přidejte ovládací prvek GridView do stránky, aby se zobrazily produkty vybrané kategorie. Nastavte `ID` ovládacího prvku GridView na `ProductsInCategory` a navažte jej na nový prvek ObjectDataSource s názvem `ProductsInCategoryDataSource`.

[![přidat nový prvek ObjectDataSource s názvem ProductsInCategoryDataSource](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image17.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image16.png)

**Obrázek 6**: Přidání nového prvku ObjectDataSource s názvem `ProductsInCategoryDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image18.png))

Nakonfigurujte prvek ObjectDataSource tak, aby vyvolal metodu `GetProductsByCategoryID(categoryID)` `ProductsBLL` třídy.

[![mají-li prvek ObjectDataSource vyvolat metodu GetProductsByCategoryID (KódKategorie)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image20.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image19.png)

**Obrázek 7**: prvek ObjectDataSource vyvolá metodu `GetProductsByCategoryID(categoryID)` ([kliknutím zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image21.png)).

Vzhledem k tomu, že metoda `GetProductsByCategoryID(categoryID)` přebírá vstupní parametr, můžete v posledním kroku průvodce zadat zdroj hodnoty parametru. Aby bylo možné zobrazit tyto produkty z vybrané kategorie, je nutné, aby byl parametr získán z `Categories` DropDownList.

[![získat hodnotu parametru KódKategorie z vybraných kategorií DropDownList](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image23.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image22.png)

**Obrázek 8**: získání hodnoty parametru *`categoryID`* z vybraných kategorií DropDownList ([kliknutím zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image24.png))

Po dokončení průvodce bude mít prvek GridView vlastnost BoundField pro každou z vlastností produktu. Pojďme tyto BoundFields vyčistit, aby se zobrazily jenom `ProductName`, `UnitPrice`, `UnitsInStock`a `UnitsOnOrder` BoundFields. Můžete přidat všechna nastavení na úrovni pole do zbývajících BoundFields (například formátování `UnitPrice` jako měny). Po provedení těchto změn by deklarativní označení prvku GridView mělo vypadat podobně jako následující:

[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample1.aspx)]

V tuto chvíli máme plně funkční sestavu Master/Detail, která zobrazuje název, jednotkovou cenu, jednotky na skladě a jednotky, které patří do vybrané kategorie.

[![získat hodnotu parametru KódKategorie z vybraných kategorií DropDownList](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image26.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image25.png)

**Obrázek 9**: získání hodnoty parametru *`categoryID`* z vybraných kategorií DropDownList ([kliknutím zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image27.png))

## <a name="step-2-displaying-a-footer-in-the-gridview"></a>Krok 2: zobrazení zápatí v prvku GridView

Ovládací prvek GridView může zobrazit hlavičku a řádek zápatí. Tyto řádky se zobrazí v závislosti na hodnotách `ShowHeader` a `ShowFooter`ch vlastností, v uvedeném pořadí `ShowHeader` výchozím nastavení `True` a `ShowFooter` `False`. Chcete-li do prvku GridView přidat zápatí, stačí nastavit jeho vlastnost `ShowFooter` na hodnotu `True`.

[![nastavte vlastnost ShowFooter prvku GridView na hodnotu true.](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image29.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image28.png)

**Obrázek 10**: nastavte vlastnost `ShowFooter` prvku GridView na hodnotu `True` ([kliknutím zobrazíte obrázek v plné velikosti).](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image30.png)

Řádek zápatí obsahuje buňku pro každé pole definované v prvku GridView; ve výchozím nastavení jsou ale tyto buňky prázdné. Počkejte, než se vám zobrazí náš průběh v prohlížeči. Vlastnost `ShowFooter` je nyní nastavena na hodnotu `True`, prvek GridView obsahuje prázdný řádek zápatí.

[![prvek GridView teď obsahuje řádek zápatí.](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image32.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image31.png)

**Obrázek 11**: prvek GridView teď obsahuje řádek zápatí ([kliknutím zobrazíte obrázek v plné velikosti](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image33.png)).

Řádek zápatí na obrázku 11 není v klidu, protože obsahuje bílé pozadí. Nyní vytvoříme třídu `FooterStyle` CSS v `Styles.css`, která určuje tmavě červené pozadí a pak nakonfigurujete `GridView.skin` soubor skinu v motivu `DataWebControls` k přiřazení této třídy CSS k vlastnosti `FooterStyle``CssClass` prvku GridView. Pokud potřebujete štětce na vzhledech a motivech, přečtěte si téma [zobrazení dat pomocí kurzu ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) .

Začněte přidáním následující třídy CSS do `Styles.css`:

[!code-css[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample2.css)]

Třída `FooterStyle` šablon stylů CSS je podobná `HeaderStyle` třídě, přestože barva pozadí `HeaderStyle`je Subtlety tmavší a její text je zobrazen tučným písmem. Text v zápatí je navíc zarovnán vpravo, zatímco text záhlaví je zarovnán na střed.

Chcete-li tuto třídu CSS přidružit k zápatí každého prvku GridView, otevřete soubor `GridView.skin` v motivu `DataWebControls` a nastavte vlastnost `CssClass` `FooterStyle`. Po přidání značky souboru by se měly vypadat takto:

[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample3.aspx)]

Jak ukazuje snímek obrazovky, tato změna způsobí, že se zápatí ponechá zřetelně.

[![řádek zápatí prvku GridView má nyní načervenou barvu pozadí](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image35.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image34.png)

**Obrázek 12**: řádek zápatí prvku GridView má nyní načervenou barvu pozadí ([kliknutím zobrazíte obrázek v plné velikosti).](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image36.png)

## <a name="step-3-computing-the-summary-data"></a>Krok 3: výpočet souhrnných dat

V zobrazeném zápatí prvku GridView je další výzva, na kterou nás odkazuje, jak vypočítat souhrnná data. K dispozici jsou dva způsoby, jak vypočítat tyto agregované informace:

1. Prostřednictvím dotazu SQL můžeme vystavit další dotaz na databázi, aby se vypočítala souhrnná data určité kategorie. SQL zahrnuje řadu agregačních funkcí spolu s klauzulí `GROUP BY` k určení dat, nad kterými by se měla shrnout data. Následující dotaz SQL by vrátil informace o potřebných informacích:  

    [!code-sql[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample4.sql)]

    Tento dotaz samozřejmě nebudete chtít vydat přímo ze stránky `SummaryDataInFooter.aspx`, ale místo toho, že vytvoříte metodu v `ProductsTableAdapter` a `ProductsBLL`.
2. Tyto informace lze vypočítat při přidávání do prvku GridView, jak je popsáno v tématu [vlastní formátování na základě kurzu dat](custom-formatting-based-upon-data-cs.md) . obslužná rutina události `RowDataBound` prvku GridView je aktivována jednou pro každý řádek, který je přidán do prvku GridView po jeho datové vazbě. Vytvořením obslužné rutiny události pro tuto událost můžeme udržovat průběžný součet hodnot, které chceme agregovat. Po navázání posledního řádku dat na prvek GridView máme součty a informace potřebné k výpočtu průměru.

Obvykle se používá druhý postup, protože ukládá cestu k databázi a úsilí potřebné k implementaci souhrnných funkcí v úrovni vrstvy přístupu k datům a obchodní logiky, ale buď stačí. Pro účely tohoto kurzu použijeme druhou možnost a sledujte průběžný součet pomocí `RowDataBound` obslužná rutina události.

Vytvořte obslužnou rutinu události `RowDataBound` pro prvek GridView výběrem prvku GridView v návrháři, kliknutím na ikonu blesku z okno Vlastnosti a dvojím kliknutím na událost `RowDataBound`. Alternativně můžete vybrat prvek GridView a jeho událost RowDataBound z rozevíracích seznamů v horní části souboru třídy ASP.NET kódu na pozadí. Tím se vytvoří nová obslužná rutina události s názvem `ProductsInCategory_RowDataBound` ve třídě kódu na pozadí `SummaryDataInFooter.aspx` stránky.

[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample5.vb)]

Aby bylo možné udržovat průběžný součet, je nutné definovat proměnné mimo rozsah obslužné rutiny události. Vytvořte následující čtyři proměnné na úrovni stránky:

- `_totalUnitPrice`typu `Decimal`
- `_totalNonNullUnitPriceCount`typu `Integer`
- `_totalUnitsInStock`typu `Integer`
- `_totalUnitsOnOrder`typu `Integer`

Dále napište kód pro zvýšení těchto tří proměnných pro každý řádek dat nalezený v obslužné rutině `RowDataBound` události.

[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample6.vb)]

Obslužná rutina události `RowDataBound` začíná tím, že zaručí, že se používá objekt DataRow. Jakmile je tato instance vytvořena, je `Northwind.ProductsRow` instance, která byla pouze svázána s objektem `GridViewRow` v `e.Row`, uložena v proměnné `product`. V dalším kroku jsou spuštěny celkový počet proměnných, které odpovídají hodnotám aktuálního produktu (za předpokladu, že neobsahují `NULL` hodnotu databáze). Průběžně sledujete celkový počet spuštěných `UnitPrice` a počet ne`NULL`ch záznamů, které jsou `UnitPrice`, protože Průměrná cena je podíl těchto dvou čísel.

## <a name="step-4-displaying-the-summary-data-in-the-footer"></a>Krok 4: zobrazení souhrnných dat v zápatí

Se souhrnnými daty celkem je posledním krokem jeho zobrazení v řádku zápatí prvku GridView. Tuto úlohu lze provést také programově prostřednictvím obslužné rutiny události `RowDataBound`. Odvolání, že se obslužná rutina události `RowDataBound` aktivuje pro *všechny* řádky, které jsou svázané s prvku GridView, včetně řádku zápatí. Proto můžeme naši obslužnou rutinu události rozšířit tak, aby zobrazovala data v řádku zápatí pomocí následujícího kódu:

[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample7.vb)]

Vzhledem k tomu, že se řádek zápatí přidá do prvku GridView po přidání všech řádků dat, můžeme si být jistí, že v době, kdy jsme připraveni zobrazit souhrnná data v zápatí, bude dokončeno spuštění celkových výpočtů. Posledním krokem je nastavení těchto hodnot v buňkách zápatí.

Chcete-li zobrazit text v konkrétní buňce zápatí, použijte `e.Row.Cells(index).Text = value`, kde se index `Cells` začíná na 0. Následující kód vypočítá průměrnou cenu (celkovou cenu vydělenou počtem produktů) a zobrazí ji spolu s celkovým počtem jednotek v zásobách a jednotek v daném pořadí v příslušných buňkách prvku GridView.

[!code-vb[Main](displaying-summary-information-in-the-gridview-s-footer-vb/samples/sample8.vb)]

Obrázek 13 znázorňuje zprávu po přidání tohoto kódu. Všimněte si, jak `ToString("c")` způsobí, že se souhrnné informace o průměrné ceně naformátují jako měna.

[![řádek zápatí prvku GridView má nyní načervenou barvu pozadí](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image38.png)](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image37.png)

**Obrázek 13**: řádek zápatí prvku GridView má nyní načervenou barvu pozadí ([kliknutím zobrazíte obrázek v plné velikosti).](displaying-summary-information-in-the-gridview-s-footer-vb/_static/image39.png)

## <a name="summary"></a>Souhrn

Zobrazení souhrnných dat je běžnou požadavkem sestavy a ovládací prvek GridView usnadňuje zahrnutí takových informací do svého řádku zápatí. Řádek zápatí se zobrazí, pokud je vlastnost `ShowFooter` prvku GridView nastavena na hodnotu `True` a může být text ve svých buňkách nastaven programově prostřednictvím obslužné rutiny události `RowDataBound`. Výpočet souhrnných dat lze provést tak, že znovu provedete dotazování databáze nebo pomocí kódu ve třídě kódu na pozadí stránky ASP.NET programově vypočítáte souhrnná data.

V tomto kurzu se uzavírá naše zkoumání vlastního formátování pomocí ovládacích prvků GridView, DetailsView a FormView. Náš další kurz se dokončí náš průzkum při vkládání, aktualizaci a odstraňování dat pomocí těchto stejných ovládacích prvků.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Předchozí](using-the-formview-s-templates-vb.md)

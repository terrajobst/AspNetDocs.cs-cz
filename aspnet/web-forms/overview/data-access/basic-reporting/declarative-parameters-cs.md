---
uid: web-forms/overview/data-access/basic-reporting/declarative-parameters-cs
title: Deklarativní parametry (C#) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu ukážeme, jak použít parametr nastavený na pevně zakódované hodnoty pro výběr dat, která se mají zobrazit v ovládacím prvku DetailsView.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 603c9bd3-b895-4ec6-853b-0c81ff36d580
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/declarative-parameters-cs
msc.type: authoredcontent
ms.openlocfilehash: 87c8cfe064abc536e6015b0e553618981da9fefe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78597270"
---
# <a name="declarative-parameters-c"></a>Deklarované parametry (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_5_CS.exe) nebo [Stáhnout PDF](declarative-parameters-cs/_static/datatutorial05cs1.pdf)

> V tomto kurzu ukážeme, jak použít parametr nastavený na pevně zakódované hodnoty pro výběr dat, která se mají zobrazit v ovládacím prvku DetailsView.

## <a name="introduction"></a>Úvod

V [posledním kurzu](displaying-data-with-the-objectdatasource-cs.md) jsme se prohlédli při zobrazování dat pomocí ovládacích prvků GridView, DetailsView a FormView vázaných na ovládací prvek ObjectDataSource, který vyvolal metodu `GetProducts()` z `ProductsBLL` třídy. Metoda `GetProducts()` vrátí DataTable se silným typem, který se naplní všemi záznamy z tabulky `Products` databáze Northwind. Třída `ProductsBLL` obsahuje další metody pro vrácení pouze podmnožiny produktů – `GetProductByProductID(productID)`, `GetProductsByCategoryID(categoryID)`a `GetProductsBySupplierID(supplierID)`. Tyto tři metody očekávají vstupní parametr, který určuje, jak filtrovat vrácené informace o produktu.

Prvek ObjectDataSource lze použít k vyvolání metod, které očekávají vstupní parametry, ale v takovém případě je nutné specifikovat, kde hodnoty pro tyto parametry pocházejí. Hodnoty parametrů mohou být pevně zakódované nebo mohou pocházet z nejrůznějších dynamických zdrojů, včetně hodnot QueryString, proměnných relací, hodnoty vlastnosti webového ovládacího prvku na stránce nebo jiné.

V tomto kurzu začneme tím, že ukážeme, jak použít parametr nastavený na pevně zakódované hodnoty. Konkrétně se podíváme na přidání prvku DetailsView na stránku, která zobrazuje informace o konkrétním produktu, jmenovitě Antoni Gumbo, která má `ProductID` 5. Dále se dozvíte, jak nastavit hodnotu parametru na základě webového ovládacího prvku. Konkrétně použijeme textové pole, které umožní uživateli psát v zemi, po které můžou kliknout na tlačítko a zobrazit seznam dodavatelů, kteří se nacházejí v dané zemi.

## <a name="using-a-hard-coded-parameter-value"></a>Použití pevně kódované hodnoty parametru

Pro první příklad Začněte přidáním ovládacího prvku DetailsView na stránku `DeclarativeParams.aspx` ve složce `BasicReporting`. Z inteligentní značky DetailsView vyberte v rozevíracím seznamu &lt;nový zdroj dat&gt; a zvolte možnost Přidat prvek ObjectDataSource.

[![přidat prvek ObjectDataSource na stránku](declarative-parameters-cs/_static/image2.png)](declarative-parameters-cs/_static/image1.png)

**Obrázek 1**: Přidání prvku ObjectDataSource na stránku ([kliknutím zobrazíte obrázek v plné velikosti](declarative-parameters-cs/_static/image3.png))

Tím se automaticky spustí Průvodce vybrat zdroj dat pro ovládací prvek ObjectDataSource. Na první obrazovce průvodce vyberte třídu `ProductsBLL`.

[![výběr třídy ProductsBLL](declarative-parameters-cs/_static/image5.png)](declarative-parameters-cs/_static/image4.png)

**Obrázek 2**: vyberte třídu `ProductsBLL` ([kliknutím zobrazíte obrázek v plné velikosti](declarative-parameters-cs/_static/image6.png)).

Vzhledem k tomu, že chceme zobrazit informace o konkrétním produktu, chceme použít metodu `GetProductByProductID(productID)`.

[![zvolit metodu GetProductByProductID (productID)](declarative-parameters-cs/_static/image8.png)](declarative-parameters-cs/_static/image7.png)

**Obrázek 3**: vyberte metodu `GetProductByProductID(productID)` ([kliknutím zobrazíte obrázek v plné velikosti](declarative-parameters-cs/_static/image9.png)).

Vzhledem k tomu, že metoda, kterou jsme zvolili, obsahuje parametr, pro Průvodce je k dispozici další obrazovka, kde se zobrazí výzva k definování hodnoty, která se má použít pro parametr. Seznam na levé straně zobrazuje všechny parametry pro vybranou metodu. `GetProductByProductID(productID)` jenom jeden `productID`. Na pravé straně můžeme zadat hodnotu pro vybraný parametr. Rozevírací seznam zdroj parametrů vytvoří výčet různých možných zdrojů pro hodnotu parametru. Vzhledem k tomu, že chceme zadat pevně zakódované hodnoty 5 pro parametr `productID`, ponechte zdroj parametru jako None a zadejte 5 do textového pole DefaultValue.

[pro parametr productID se použije ![pevně zakódovaného parametru, který má hodnotu 5.](declarative-parameters-cs/_static/image11.png)](declarative-parameters-cs/_static/image10.png)

**Obrázek 4**: pro parametr `productID` bude použita pevně kódovaná hodnota parametru 5 ([kliknutím zobrazíte obrázek v plné velikosti).](declarative-parameters-cs/_static/image12.png)

Po dokončení Průvodce konfigurací zdroje dat obsahuje deklarativní označení ovládacího prvku ObjectDataSource objekt `Parameter` v kolekci `SelectParameters` pro každý vstupní parametr očekávaný metodou definovanou ve vlastnosti `SelectMethod`. Vzhledem k tomu, že metoda, kterou v tomto příkladu používáme, očekává jenom jeden vstupní parametr, `parameterID`, tady je jenom jedna položka. Kolekce `SelectParameters` může obsahovat libovolnou třídu, která je odvozena od `Parameter` třídy v oboru názvů `System.Web.UI.WebControls`. Pro pevně zakódované hodnoty parametrů je použita základní `Parameter` třída, ale pro ostatní možnosti zdrojového parametru je použita odvozená `Parameter` třída; v případě potřeby můžete také vytvořit vlastní [typy parametrů](http://www.leftslipper.com/ShowFaq.aspx?FaqId=11).

[!code-aspx[Main](declarative-parameters-cs/samples/sample1.aspx)]

> [!NOTE]
> Pokud sledujete na vlastním počítači, deklarativní označení, které vidíte v tomto okamžiku, může zahrnovat hodnoty vlastností `InsertMethod`, `UpdateMethod`a `DeleteMethod` a také `DeleteParameters`. Průvodce zvolit zdroj dat v prvku ObjectDataSource automaticky určuje metody z `ProductBLL` pro vložení, aktualizaci a odstranění, takže pokud je výslovně nevymažete, budou zahrnuty do značky výše.

Při návštěvě této stránky Webová ovládací prvek data vyvolá metodu `Select` ObjectDataSource, která zavolá metodu `GetProductByProductID(productID)` `ProductsBLL` třídy s použitím pevně zakódované hodnoty 5 pro `productID` vstupní parametr. Metoda vrátí objekt se silným typem `ProductDataTable`, který obsahuje jeden řádek s informacemi o Gumbo (produkt s `ProductID` 5) pro Anton.

[Zobrazí se ![informace o Gumbo mix pro Anton](declarative-parameters-cs/_static/image14.png)](declarative-parameters-cs/_static/image13.png)

**Obrázek 5**: zobrazí se informace o Gumbo ([kliknutím zobrazíte obrázek v plné velikosti) pro](declarative-parameters-cs/_static/image15.png)Anton.

## <a name="setting-the-parameter-value-to-the-property-value-of-a-web-control"></a>Nastavení hodnoty parametru na hodnotu vlastnosti webového ovládacího prvku

Hodnoty parametru ObjectDataSource lze také nastavit na základě hodnoty webového ovládacího prvku na stránce. Aby to bylo možné, Podívejme se na prvek GridView, který obsahuje seznam všech dodavatelů nacházejících se v zemi určené uživatelem. Pro dosažení tohoto začátku přidejte textové pole na stránku, do které může uživatel zadat název země. Nastavte vlastnost `ID` ovládacího prvku TextBox na hodnotu `CountryName`. Přidejte také webový ovládací prvek tlačítko.

[![přidat textové pole na stránku s ID země](declarative-parameters-cs/_static/image17.png)](declarative-parameters-cs/_static/image16.png)

**Obrázek 6**: Přidání textového pole na stránku pomocí `ID` `CountryName` ([kliknutím zobrazíte obrázek v plné velikosti](declarative-parameters-cs/_static/image18.png))

Dále přidejte prvek GridView na stránku a z inteligentní značky vyberte možnost Přidat nový prvek ObjectDataSource. Vzhledem k tomu, že chceme zobrazit informace o dodavateli, vyberte na první obrazovce Průvodce třídu `SuppliersBLL`. Na druhé obrazovce vyberte metodu `GetSuppliersByCountry(country)`.

[![zvolit metodu GetSuppliersByCountry (země)](declarative-parameters-cs/_static/image20.png)](declarative-parameters-cs/_static/image19.png)

**Obrázek 7**: vyberte metodu `GetSuppliersByCountry(country)` ([kliknutím zobrazíte obrázek v plné velikosti](declarative-parameters-cs/_static/image21.png)).

Vzhledem k tomu, že metoda `GetSuppliersByCountry(country)` má vstupní parametr, průvodce po opětovném spuštění obsahuje poslední obrazovku pro výběr hodnoty parametru. Tentokrát nastavte zdroj parametru tak, aby byl ovládací prvek. Tím se naplní rozevírací seznam ControlID názvy ovládacích prvků na stránce. v seznamu vyberte ovládací prvek `CountryName`. Při prvním navštívení stránky bude pole `CountryName` prázdné, takže se nevrátí žádné výsledky a nic se nezobrazí. Pokud chcete ve výchozím nastavení zobrazit některé výsledky, nastavte textové pole DefaultValue odpovídajícím způsobem.

[![nastavte hodnotu parametru na hodnotu ovládacího prvku Country.](declarative-parameters-cs/_static/image23.png)](declarative-parameters-cs/_static/image22.png)

**Obrázek 8**: nastavte hodnotu parametru na hodnotu ovládacího prvku `CountryName` ([kliknutím zobrazíte obrázek v plné velikosti).](declarative-parameters-cs/_static/image24.png)

Deklarativní označení ovládacího prvku ObjectDataSource se mírně liší od našeho prvního příkladu pomocí [třídě ControlParameter](https://msdn.microsoft.com/library/system.web.ui.webcontrols.controlparameter.aspx) namísto standardního objektu `Parameter`. `ControlParameter` má další vlastnosti pro určení `ID` webového ovládacího prvku a hodnotu vlastnosti, která se má použít pro parametr (`PropertyName`). Průvodce konfigurací zdroje dat byl dostatečně inteligentní k určení toho, že pro textové pole budeme nejspíš chtít použít vlastnost `Text` pro hodnotu parametru. Pokud však chcete použít jinou hodnotu vlastnosti z webového ovládacího prvku, můžete změnit `PropertyName` hodnotu nebo kliknutím na odkaz Zobrazit pokročilé vlastnosti v průvodci.

[!code-aspx[Main](declarative-parameters-cs/samples/sample2.aspx)]

Při prvním návštěvě `CountryName` textového pole je prázdné. Metoda `Select` ovládacího prvku ObjectDataSource je stále vyvolána prvkem GridView, ale hodnota `null` je předána do metody `GetSuppliersByCountry(country)`. TableAdapter převede `null` na `NULL` hodnotu databáze (`DBNull.Value`), ale dotaz používaný metodou `GetSuppliersByCountry(country)` je napsán tak, aby nevrátil žádné hodnoty, pokud je pro parametr `NULL` zadána hodnota `@CategoryID`. V krátkém případě se nevrátí žádní dodavatelé.

Jakmile návštěvník vstoupí do země a klikne na tlačítko Zobrazit dodavatele, aby způsobil postback, je znovu dotazována metoda `Select` ovládacího prvku TextBox, která předá hodnotu ovládacího prvku TextBox `Text` jako parametr `country`.

[![se zobrazí dodavatelé z Kanady.](declarative-parameters-cs/_static/image26.png)](declarative-parameters-cs/_static/image25.png)

**Obrázek 9**: zobrazí se dodavatelé z Kanady ([kliknutím zobrazíte obrázek v plné velikosti](declarative-parameters-cs/_static/image27.png)).

## <a name="showing-all-suppliers-by-default"></a>Zobrazení všech dodavatelů ve výchozím nastavení

Místo toho, abyste při prvním zobrazení stránky viděli žádné ze dodavatelů, můžeme nejdřív zobrazit *všechny* dodavatele a povolit tak uživateli, aby ho zredukovali v seznamu tak, že do textového pole zadáte název země. Když je textové pole prázdné, metoda `GetSuppliersByCountry(country)` třídy `SuppliersBLL` je předána do `null` hodnoty pro svůj *`country`* vstupní parametr. Tato hodnota `null` se pak předává do metody `GetSupplierByCountry(country)` DAL, kde je přeložena na hodnotu `NULL` databáze pro parametr `@Country` v následujícím dotazu:

[!code-sql[Main](declarative-parameters-cs/samples/sample3.sql)]

Výraz `Country = NULL` vždy vrátí hodnotu false, a to i u záznamů, jejichž `Country` sloupec má `NULL` hodnotu; Proto nejsou vráceny žádné záznamy.

Chcete-li vrátit *všechny* dodavatele, když je textové pole země prázdné, můžeme rozšířit metodu `GetSuppliersByCountry(country)` v knihoven BLL k vyvolání metody `GetSuppliers()`, pokud je její parametr země `null` a chcete-li volat metodu `GetSuppliersByCountry(country)` dal, jinak. To bude mít vliv na vrácení všech dodavatelů, pokud není zadána žádná země a příslušné podmnožiny dodavatelů, pokud je zahrnut parametr země.

Změňte metodu `GetSuppliersByCountry(country)` třídy `SuppliersBLL` na následující:

[!code-csharp[Main](declarative-parameters-cs/samples/sample4.cs)]

Pomocí této změny se na stránce `DeclarativeParams.aspx` zobrazí při prvním navštívení všichni dodavatelé (nebo pokaždé, když je textové pole `CountryName` prázdné).

[![se teď ve výchozím nastavení zobrazují všichni dodavatelé.](declarative-parameters-cs/_static/image29.png)](declarative-parameters-cs/_static/image28.png)

**Obrázek 10**: ve výchozím nastavení se teď zobrazují všichni dodavatelé ([kliknutím zobrazíte obrázek v plné velikosti).](declarative-parameters-cs/_static/image30.png)

## <a name="summary"></a>Souhrn

Aby bylo možné používat metody se vstupními parametry, musíme zadat hodnoty parametrů v kolekci `SelectParameters` ObjectDataSource. Různé typy parametrů umožňují získat hodnotu parametru z různých zdrojů. Výchozí typ parametru používá pevně zakódované hodnoty, ale stejně jako snadno (a bez řádku kódu) lze získat hodnoty parametrů z řetězce dotazu, proměnných relace, souborů cookie a dokonce uživatelem zadaných hodnot z webových ovládacích prvků na stránce.

Příklady, které jsme vyhledali v tomto kurzu, ilustrují použití deklarativních hodnot parametrů. Nicméně může nastat čas, kdy potřebujeme použít zdroj parametru, který není k dispozici, jako je aktuální datum a čas, nebo pokud náš web použil členství, ID uživatele návštěvníka. V takových scénářích můžeme hodnoty parametrů nastavit programově před vyvoláním metody základního objektu ObjectDataSource. V [dalším kurzu](programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)vám ukážeme, jak to provést.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Hilton Giesenow. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](displaying-data-with-the-objectdatasource-cs.md)
> [Další](programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)

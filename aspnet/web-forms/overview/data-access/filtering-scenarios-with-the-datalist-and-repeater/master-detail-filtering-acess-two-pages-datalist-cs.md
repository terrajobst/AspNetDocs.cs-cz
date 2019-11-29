---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-acess-two-pages-datalist-cs
title: Filtrování seznamu a podrobností na dvou stránkách (C#) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se podíváme na to, jak oddělit hlavní a podrobné sestavy mezi dvěma stránkami. Na hlavní stránce používáme ovládací prvek Repeater k vykreslení seznamu CATEG...
ms.author: riande
ms.date: 10/30/2010
ms.assetid: 68b8c023-92fa-4df6-9563-1764e16e4b04
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-acess-two-pages-datalist-cs
msc.type: authoredcontent
ms.openlocfilehash: 545b24a66476c55aff88ac62d3a6528105fea6c0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74631249"
---
# <a name="masterdetail-filtering-across-two-pages-c"></a>Filtrování hlavních záznamů / podrobností na dvou stránkách (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_34_CS.exe) nebo [Stáhnout PDF](master-detail-filtering-acess-two-pages-datalist-cs/_static/datatutorial34cs1.pdf)

> V tomto kurzu se podíváme na to, jak oddělit hlavní a podrobné sestavy mezi dvěma stránkami. Na stránce "hlavní" používáme ovládací prvek Repeater k vykreslení seznamu kategorií, který při kliknutí na něj převezme uživatele na stránku podrobností, kde se ve dvou sloupcích DataList zobrazí tyto produkty patřící do vybrané kategorie.

## <a name="introduction"></a>Úvod

V [předchozím kurzu](master-detail-filtering-with-a-dropdownlist-datalist-cs.md) jsme viděli, jak zobrazit hlavní a podrobné sestavy na jedné webové stránce pomocí DropDownList pro zobrazení "hlavních" záznamů a prvku DataList pro zobrazení podrobností. Dalším běžným vzorem, který se používá pro hlavní a podrobné sestavy, je mít hlavní záznamy na jedné webové stránce a podrobnosti na jiném. V předchozím kurzu zobrazení [hlavního/podrobného filtrování na dvou stránkách](../masterdetail/master-detail-filtering-across-two-pages-cs.md) jsme tento model prozkoumali pomocí prvku GridView, který zobrazí všechny dodavatele v systému. Tento prvek GridView obsahuje objekt HyperLinkField, který je vykreslen jako odkaz na druhou stránku, který se předává podél `SupplierID` v řetězci dotazu. Druhá stránka použila prvek GridView k vypsání produktů poskytovaných vybraným dodavatelem.

Tyto dvě a podrobné sestavy lze také provést pomocí prvků DataList a Repeater. Jediným rozdílem je, že prvek DataList ani Repeater neposkytují podporu pro ovládací prvek HyperLinkField. Místo toho je nutné přidat webový ovládací prvek hypertextového odkazu nebo ukotvení elementu HTML (`<a>`) v rámci `ItemTemplate`ovládacího prvku. Vlastnost `NavigateUrl` hypertextového odkazu nebo atribut `href` kotvy lze následně přizpůsobit pomocí deklarativních nebo programových přístupů.

V tomto kurzu prozkoumáme příklad, který vypíše kategorie v seznamu s odrážkami na jedné stránce pomocí ovládacího prvku Repeater. Každá položka seznamu bude obsahovat název a Popis kategorie s názvem kategorie zobrazeným jako odkaz na druhou stránku. Kliknutím na tento odkaz zobrazíte uživatele na druhou stránku, kde prvek DataList zobrazí tyto produkty, které patří do vybrané kategorie.

## <a name="step-1-displaying-the-categories-in-a-bulleted-list"></a>Krok 1: zobrazení kategorií v seznamu s odrážkami

Prvním krokem při vytváření libovolné hlavní a podrobné sestavy je spuštění zobrazením "hlavních" záznamů. Naším prvním úkolem je proto zobrazení kategorií na hlavní stránce. Otevřete stránku `CategoryListMaster.aspx` ve složce `DataListRepeaterFiltering`, přidejte ovládací prvek Repeater a z inteligentní značky se přihlaste k přidání nového prvku ObjectDataSource. Nakonfigurujte nový prvek ObjectDataSource tak, aby měl přístup k jeho datům z metody `GetCategories` `CategoriesBLL` třídy (viz obrázek 1).

[![nakonfigurovat prvek ObjectDataSource na použití metody GetCategories třídy CategoriesBLL](master-detail-filtering-acess-two-pages-datalist-cs/_static/image2.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image1.png)

**Obrázek 1**: Konfigurace prvku ObjectDataSource pro použití metody `GetCategories` `CategoriesBLL` třídy ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-acess-two-pages-datalist-cs/_static/image3.png))

Dále definujte šablony opakování tak, aby se v seznamu s odrážkami zobrazovaly jednotlivé názvy a popisy kategorií jako položka. Nedělejme si ještě starosti s tím, že každá kategorie má odkaz na stránku podrobností. Následující příklad ukazuje deklarativní označení pro Repeater a ObjectDataSource:

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample1.aspx)]

Po dokončení tohoto kódu si chvíli počkejte, než se vám zobrazí náš pokrok v prohlížeči. Jak ukazuje obrázek 2, opakuje se vykreslení v seznamu s odrážkami, který zobrazuje název a popis každé kategorie.

[![se každá kategorie zobrazuje jako položka seznamu s odrážkami](master-detail-filtering-acess-two-pages-datalist-cs/_static/image5.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image4.png)

**Obrázek 2**: Každá kategorie se zobrazuje jako položka seznamu s odrážkami ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-acess-two-pages-datalist-cs/_static/image6.png)

## <a name="step-2-turning-the-category-name-into-a-link-to-the-details-page"></a>Krok 2: zapnutí názvu kategorie na odkaz na stránku podrobností

Aby uživatel mohl uživateli zobrazit informace o podrobnostech pro danou kategorii, musíme přidat odkaz na každou položku seznamu s odrážkami, kterou při kliknutí na ni převezme uživatele na druhou stránku (`ProductsForCategoryDetails.aspx`). Na druhé stránce se pak zobrazí produkty vybrané kategorie pomocí prvku DataList. Aby bylo možné určit kategorii, jejíž odkaz byl kliknuto, musíme k druhé stránce v rámci určitého mechanismu předat `CategoryID`a kategorie kliknutí. Nejjednodušší, nejjednodušším způsobem přenosu skalárních dat z jedné stránky na druhý je prostřednictvím řetězce dotazu, což je možnost, kterou v tomto kurzu použijeme. Konkrétně `ProductsForCategoryDetails.aspx` stránka očekává, že vybraná hodnota *`categoryID`* bude předána pomocí pole QueryString s názvem `CategoryID`. Pokud například chcete zobrazit produkty pro kategorii nápoje, která má `CategoryID` 1, uživatel navštíví `ProductsForCategoryDetails.aspx?CategoryID=1`.

Pro vytvoření hypertextového odkazu pro každou položku seznamu s odrážkami v OPAKOVAČI musíme přidat webový ovládací prvek hypertextového odkazu nebo prvek ukotvení HTML (`<a>`) do `ItemTemplate`. Ve scénářích, kdy se hypertextový odkaz zobrazí u každého řádku, bude stačit kterýkoli přístup. Pro opakuje raději použití prvku ukotvení. Chcete-li použít prvek ukotvení, aktualizujte hodnoty ItemTemplate opakování na:

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample2.aspx)]

Všimněte si, že `CategoryID` lze vložit přímo do atributu `href` elementu ukotvení; Nicméně k tomu je potřeba určit, aby se hodnota atributu `href`a pomocí apostrofů (a uvozovky), protože metoda `Eval` v atributu `href` omezuje svůj řetězec (`"CategoryID"`) na uvozovky. Alternativně lze místo toho použít webový ovládací prvek hypertextového odkazu:

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample3.aspx)]

Všimněte si, jak se statická část adresy URL – `ProductsForCategoryDetails.aspx?CategoryID` – připojí k výsledku `Eval("CategoryID")` přímo v rámci syntaxe DataBinding pomocí zřetězení řetězců.

Jednou z výhod používání ovládacího prvku hypertextový odkaz je to, že se v případě potřeby dá programově přistupovat z obslužné rutiny události `ItemDataBound` Repeater. Například může být vhodné zobrazit název kategorie jako text, nikoli jako odkaz pro kategorie bez přidružených produktů. Tato kontrolu by mohla být provedena programově v obslužné rutině události `ItemDataBound`; u kategorií bez přidružených produktů může být vlastnost `NavigateUrl` hypertextového odkazu nastavena na prázdný řetězec, což vede k vygenerování konkrétního názvu kategorie jako prostý text (nikoli jako odkaz). Další informace o formátování prvku DataList a zopakování obsahu v závislosti na programové logice prostřednictvím obslužné rutiny události `ItemDataBound` naleznete v tématu o [formátování prvku DataList a Repeater na základě](../displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-cs.md) výukového kurzu.

Pokud potřebujete, můžete na stránce použít buď prvek ukotvení, nebo přístup k ovládacímu prvku hypertextový odkaz. Bez ohledu na přístup by se při prohlížení stránky v prohlížeči měly všechny názvy kategorií vykreslovat jako odkaz na `ProductsForCategoryDetails.aspx`s předáním příslušné `CategoryID` hodnoty (viz obrázek 3).

[![název kategorie teď odkazují na ProductsForCategoryDetails. aspx.](master-detail-filtering-acess-two-pages-datalist-cs/_static/image8.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image7.png)

**Obrázek 3**: názvy kategorií teď odkazují na `ProductsForCategoryDetails.aspx` ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-acess-two-pages-datalist-cs/_static/image9.png)

## <a name="step-3-listing-the-products-that-belong-to-the-selected-category"></a>Krok 3: seznam produktů, které patří do vybrané kategorie

Po dokončení stránky `CategoryListMaster.aspx` jsme připraveni na to, abychom vám pomohli s implementací stránky podrobností, `ProductsForCategoryDetails.aspx`. Otevřete tuto stránku, přetáhněte prvek DataList z panelu nástrojů do návrháře a nastavte jeho vlastnost `ID` na hodnotu `ProductsInCategory`. Dále můžete z inteligentní značky prvku DataList zvolit přidání nového prvku ObjectDataSource na stránku a pojmenování `ProductsInCategoryDataSource`. Nakonfigurujte ji tak, aby zavolala metodu `GetProductsByCategoryID(categoryID)` třídy `ProductsBLL`; v rozevíracích seznamech na kartách vložení, aktualizace a odstranění nastavte (žádné).

[![nakonfigurovat prvek ObjectDataSource pro použití metody GetProductsByCategoryID (KódKategorie) třídy ProductsBLL](master-detail-filtering-acess-two-pages-datalist-cs/_static/image11.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image10.png)

**Obrázek 4**: Konfigurace prvku ObjectDataSource pro použití metody `GetProductsByCategoryID(categoryID)` `ProductsBLL` třídy ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-acess-two-pages-datalist-cs/_static/image12.png))

Vzhledem k tomu, že metoda `GetProductsByCategoryID(categoryID)` přijímá vstupní parametr ( *`categoryID`* ), průvodce zvolit zdroj dat nabízí možnost zadat zdroj parametru. Nastavte zdroj parametru na QueryString pomocí `CategoryID`vlastnost QueryStringField.

[![jako zdroj parametru použít KódKategorie pole QueryString](master-detail-filtering-acess-two-pages-datalist-cs/_static/image14.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image13.png)

**Obrázek 5**: použijte pole QueryString `CategoryID` jako zdroj parametru ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-acess-two-pages-datalist-cs/_static/image15.png)

Jak jsme viděli v předchozích kurzech, po dokončení průvodce vybrat zdroj dat automaticky vytvoří Visual Studio `ItemTemplate` pro prvek DataList, kde jsou uvedeny jednotlivé názvy a hodnoty datových polí. Nahraďte tuto šablonu názvem, který obsahuje jenom název produktu, dodavatele a cenu. Také nastavte vlastnost `RepeatColumns` prvku DataList na hodnotu 2. Po těchto změnách by deklarativní označení DataList a ObjectDataSource mělo vypadat podobně jako následující:

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample4.aspx)]

Chcete-li zobrazit tuto stránku v akci, začněte na stránce `CategoryListMaster.aspx`; potom klikněte na odkaz v seznamu kategorie s odrážkami. Provedete to tak, že přejdete na `ProductsForCategoryDetails.aspx`a projdete `CategoryID` skrze dotaz QueryString. `ProductsInCategoryDataSource` ObjectDataSource v `ProductsForCategoryDetails.aspx` pak získá pouze tyto produkty pro určenou kategorii a zobrazí je v prvku DataList, který vykresluje dva produkty na řádek. Obrázek 6 zobrazuje snímek obrazovky `ProductsForCategoryDetails.aspx` při prohlížení nápojů.

[![zobrazeny nápoje, dvě na každý řádek](master-detail-filtering-acess-two-pages-datalist-cs/_static/image17.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image16.png)

**Obrázek 6**: zobrazeny nápoje, dva řádky ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-acess-two-pages-datalist-cs/_static/image18.png))

## <a name="step-4-displaying-category-information-on-productsforcategorydetailsaspx"></a>Krok 4: zobrazení informací o kategorii v ProductsForCategoryDetails. aspx

Když uživatel klikne na kategorii v `CategoryListMaster.aspx`, předají se `ProductsForCategoryDetails.aspx` a zobrazí se produkty, které patří do vybrané kategorie. V `ProductsForCategoryDetails.aspx` ale neexistují žádné vizuální pomůcky k výběru kategorie. Uživatel, který chtěl kliknout na nápoje, ale omylem klikl na koření, nemá žádný způsob, jak svou chybu realizovat, jakmile dosáhnou `ProductsForCategoryDetails.aspx`. Pro zmírnění tohoto potenciálního problému můžeme zobrazit informace o vybrané kategorii – její název a popis, a to v horní části stránky `ProductsForCategoryDetails.aspx`.

K tomu je nutné přidat FormView nad ovládací prvek Repeater v `ProductsForCategoryDetails.aspx`. Dále přidejte nový prvek ObjectDataSource na stránku z inteligentní značky FormView s názvem `CategoryDataSource` a nakonfigurujte ji tak, aby používala metodu `GetCategoryByCategoryID(categoryID)` `CategoriesBLL` třídy.

[![přístup k informacím o kategorii prostřednictvím metody GetCategoryByCategoryID (KódKategorie) třídy CategoriesBLL](master-detail-filtering-acess-two-pages-datalist-cs/_static/image20.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image19.png)

**Obrázek 7**: přístup k informacím o kategorii prostřednictvím metody `GetCategoryByCategoryID(categoryID)` `CategoriesBLL` třídy ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-acess-two-pages-datalist-cs/_static/image21.png))

Stejně jako u `ProductsInCategoryDataSource` ObjectDataSource přidané v kroku 3 Průvodce konfigurací zdroje dat `CategoryDataSource`vyzve nás ke zdroji pro vstupní parametr metody `GetCategoryByCategoryID(categoryID)`. Použijte přesně stejné nastavení jako předtím a nastavte zdroj parametru na hodnotu QueryString a hodnotu vlastnost QueryStringField na `CategoryID` (odkaz zpět na obrázek 5).

Po dokončení Průvodce vytvoří Visual Studio automaticky `ItemTemplate`, `EditItemTemplate`a `InsertItemTemplate` pro FormView. Vzhledem k tomu, že poskytujeme rozhraní jen pro čtení, můžete `EditItemTemplate` a `InsertItemTemplate`odebrat. Také si můžete bez obav přizpůsobit `ItemTemplate`třídy FormView. Po odebrání nadbytečných šablon a přizpůsobení šablony ItemTemplate by měly deklarativní značky FormView a ObjectDataSource vypadat podobně jako následující:

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample5.aspx)]

Obrázek 8 ukazuje snímek obrazovky při prohlížení této stránky prostřednictvím prohlížeče.

> [!NOTE]
> Kromě třídy FormView jsem také přidali ovládací prvek hypertextový odkaz nad FormView, který převezme uživatele zpět do seznamu kategorií (`CategoryListMaster.aspx`). Tento odkaz můžete umístit jinam nebo ho zcela vynechat.

[Informace o ![kategorie se teď zobrazují v horní části stránky.](master-detail-filtering-acess-two-pages-datalist-cs/_static/image23.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image22.png)

**Obrázek 8**: informace o kategorii se teď zobrazují v horní části stránky ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-acess-two-pages-datalist-cs/_static/image24.png)).

## <a name="step-5-displaying-a-message-if-no-products-belong-to-the-selected-category"></a>Krok 5: zobrazení zprávy, pokud žádné produkty nepatří do vybrané kategorie

Stránka `CategoryListMaster.aspx` obsahuje seznam všech kategorií v systému bez ohledu na to, zda jsou k dispozici nějaké produkty. Pokud uživatel klikne na kategorii bez přidružených produktů, prvek DataList v `ProductsForCategoryDetails.aspx` nebude vykreslen, protože jeho zdroj dat nebude obsahovat žádné položky. Jak jsme viděli v minulých kurzech, prvek GridView poskytuje vlastnost `EmptyDataText`, která se dá použít k určení textové zprávy, která se má zobrazit, pokud ve svém zdroji dat nejsou žádné záznamy. Prvek DataList ani Repeater ale takovou vlastnost bohužel neexistují.

Aby se zobrazila zpráva informující o uživateli, že pro vybranou kategorii neexistují žádné odpovídající produkty, musíme na stránku přidat ovládací prvek popisek, jehož vlastnost `Text` je přiřazena zprávě, která se zobrazí v případě, že neexistují žádné odpovídající produkty. Pak je nutné programově nastavit jeho vlastnost `Visible` na základě toho, zda prvek DataList obsahuje nějaké položky.

Chcete-li to dosáhnout, Začněte přidáním popisku pod prvkem DataList. Vlastnost `ID` nastavte na `NoProductsMessage` a vlastnost `Text` na hodnotu pro vybranou kategorii nejsou k dispozici žádné produkty... Dál je potřeba programově nastavit vlastnost `Visible` tohoto popisku na základě toho, jestli jsou nějaká data vázaná na `ProductsInCategory` DataList. Toto přiřazení je nutné provést poté, co byla data svázána s ovládacím prvky DataList. Pro prvky GridView, DetailsView a FormView jsme mohli vytvořit obslužnou rutinu události pro událost `DataBound` ovládacího prvku, která se aktivuje po dokončení datové vazby. Prvek DataList ani Repeater však nemá k dispozici událost `DataBound`.

Pro tento konkrétní příklad můžeme přiřadit vlastnost `Visible` popisku v obslužné rutině události `Page_Load`, protože data budou přiřazena do prvku DataList před událostí `Load` stránky. Tento přístup však nefunguje v obecném případě, protože data z prvku ObjectDataSource mohou být vázána na DataList později v životním cyklu stránky. Například pokud jsou zobrazená data založena na hodnotě v jiném ovládacím prvku, jako je například při zobrazení sestavy hlavní/podrobnosti pomocí ovládacího prvku DropDownList pro uchovávání "hlavních" záznamů, data se nemusí svázat s webovým ovládacím prvkem data, dokud ne`PreRender` fáze v životním cyklu stránky.

Jedno řešení, které bude fungovat pro všechny případy, je přiřazení vlastnosti `Visible` k `False` v obslužné rutině události `ItemDataBound` (nebo `ItemCreated`) prvku DataList při vytváření vazby typu položky `Item` nebo `AlternatingItem`. V takovém případě víme, že ve zdroji dat existuje alespoň jedna položka dat, a proto může popisek `NoProductsMessage` skrýt. Kromě této obslužné rutiny události potřebujeme také obslužnou rutinu události pro událost `DataBinding` prvku DataList, kde inicializujeme vlastnost `Visible` popisku na `True`. Vzhledem k tomu, že událost `DataBinding` je aktivována před `ItemDataBound` událostí, bude zpočátku vlastnost `Visible` popisku nastavena na `True`; Pokud však existují nějaké datové položky, bude nastaveno na `False`. Následující kód implementuje tuto logiku:

[!code-csharp[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample6.cs)]

Všechny kategorie v databázi Northwind jsou přidruženy k jednomu nebo více produktům. K otestování této funkce jsem ručně upravil (a) databázi Northwind pro tento kurz, a proto znovu přiřadíte všechny produkty přidružené ke kategorii Products (`CategoryID` = 7) do kategorie rybích plodů (`CategoryID` = 8). To lze provést z Průzkumník serveru tím, že vyberete nový dotaz a použijete následující příkaz `UPDATE`:

[!code-sql[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample7.sql)]

Po aktualizaci databáze se odpovídajícím způsobem vraťte na stránku `CategoryListMaster.aspx` a klikněte na odkaz vytvořit. Vzhledem k tomu, že už neexistují žádné produkty patřící do kategorie produktů, měli byste vidět, že pro vybranou kategorii nejsou žádné produkty... zpráva, jak je znázorněno na obrázku 9.

[![se zobrazí zpráva, pokud nejsou k dispozici žádné produkty patřící do vybrané kategorie.](master-detail-filtering-acess-two-pages-datalist-cs/_static/image26.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image25.png)

**Obrázek 9**: Pokud nejsou k dispozici žádné produkty patřící do vybrané kategorie ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-acess-two-pages-datalist-cs/_static/image27.png)), zobrazí se zpráva.

## <a name="summary"></a>Přehled

I když se v sestavách a podrobností můžou zobrazovat hlavní a podrobné záznamy na jedné stránce, na mnoha webech, které jsou oddělené na dvou webových stránkách. V tomto kurzu jsme se podívali na to, jak implementovat takovou sestavu hlavní/podrobnosti s kategoriemi uvedenými v seznamu s odrážkami pomocí opakovače na webové stránce hlavní a s přidruženými produkty uvedenými na stránce Podrobnosti. Každá položka seznamu na hlavní webové stránce obsahovala odkaz na stránku s podrobnostmi, která prošla `CategoryID` hodnotou řádku.

Na stránce podrobností načítající tyto produkty pro zadaného dodavatele byl provedeno prostřednictvím metody `GetProductsByCategoryID(categoryID)` `ProductsBLL` třídy. Hodnota parametru *`categoryID`* byla určena deklarativně pomocí hodnoty `CategoryID` QueryString jako zdroje parametru. Zjistili jsme také, jak zobrazit podrobnosti o kategorii na stránce podrobností pomocí FormView a jak zobrazit zprávu, pokud neexistovaly žádné produkty patřící do vybrané kategorie.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky...

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Zack Novotný a Liz Shulok. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](master-detail-filtering-with-a-dropdownlist-datalist-cs.md)
> [Další](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)

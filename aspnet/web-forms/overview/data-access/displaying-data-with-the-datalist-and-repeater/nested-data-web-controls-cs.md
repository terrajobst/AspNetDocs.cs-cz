---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/nested-data-web-controls-cs
title: Webové ovládací prvky vnořenýchC#dat () | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se naučíme, jak použít opakování vnořené uvnitř jiného opakovače. V příkladech je znázorněno, jak naplnit vnitřní opakovač d...
ms.author: riande
ms.date: 09/13/2006
ms.assetid: ad3cb0ec-26cf-42d7-b81b-184a34ec9f86
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/nested-data-web-controls-cs
msc.type: authoredcontent
ms.openlocfilehash: 8ef15bebb2c29976274b0cca1d6ace434ccc55ce
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640318"
---
# <a name="nested-data-web-controls-c"></a>Webové ovládací prvky vnořených dat (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_32_CS.exe) nebo [Stáhnout PDF](nested-data-web-controls-cs/_static/datatutorial32cs1.pdf)

> V tomto kurzu se naučíme, jak použít opakování vnořené uvnitř jiného opakovače. V příkladech je znázorněno, jak naplnit vnitřní opakovač deklarativně i programově.

## <a name="introduction"></a>Úvod

Kromě statických syntaxí HTML a vázání dat mohou šablony také obsahovat webové ovládací prvky a uživatelské ovládací prvky. Tyto webové ovládací prvky mohou mít své vlastnosti přiřazené prostřednictvím deklarativní, datové vazby nebo mohou být k dispozici programově v rámci příslušných obslužných rutin událostí na straně serveru.

Vložením ovládacích prvků v rámci šablony je možné přizpůsobit a zlepšit vzhled a činnost koncového uživatele na portálu. Například v tématu [použití templatefields v kurzu ovládacího prvku GridView](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) jsme viděli, jak přizpůsobit zobrazení prvku GridView s přidáním ovládacího prvku kalendáře ve třídě TemplateField k zobrazení data nástupu zaměstnance; v [přidávání ovládacích prvků ověřování do rozhraní pro úpravy a vkládání](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md) a [přizpůsobení](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) kurzů pro rozhraní úprav dat jsme viděli, jak přizpůsobit rozhraní pro úpravy a vkládání přidáním ovládacích prvků ověřování, textových polí, DropDownList a dalších webových ovládacích prvků.

Šablony mohou obsahovat také další webové ovládací prvky dat. To znamená, že v rámci svých šablon můžeme mít prvek DataList, který obsahuje další prvky DataList (nebo Repeater, GridView, DetailsView atd.). Výzva s takovým rozhraním je svázána s odpovídajícími daty webového ovládacího prvku pro vnitřní data. K dispozici je několik různých přístupů, od deklarativních možností použití prvku ObjectDataSource až po programové aplikace.

V tomto kurzu se naučíme, jak použít opakování vnořené uvnitř jiného opakovače. Vnější opakovač bude obsahovat položku pro každou kategorii v databázi a zobrazí název kategorie s popisem. U každé položky kategorie s vnitřním opakovačem se zobrazí informace pro každý produkt patřící do této kategorie (viz obrázek 1) v seznamu s odrážkami. Naše příklady ilustrují způsob naplnění vnitřního opakovače deklarativně i programově.

[![jednotlivé kategorie spolu s jejími produkty, jsou uvedeny](nested-data-web-controls-cs/_static/image2.png)](nested-data-web-controls-cs/_static/image1.png)

**Obrázek 1**: v seznamu jsou uvedeny všechny kategorie spolu s jeho produkty ([kliknutím zobrazíte obrázek v plné velikosti](nested-data-web-controls-cs/_static/image3.png)).

## <a name="step-1-creating-the-category-listing"></a>Krok 1: vytvoření seznamu kategorií

Při vytváření stránky, která používá webové ovládací prvky vnořených dat, je vhodné nejprve navrhnout, vytvořit a otestovat webový ovládací prvek nejvzdálenějšího data, aniž by se musely obávat vnitřní vnořené ovládací prvky. Proto začněte Projděte kroky potřebnými k přidání opakovače na stránku, která obsahuje seznam názvů a popisů pro každou kategorii.

Začněte tím, že otevřete stránku `NestedControls.aspx` ve složce `DataListRepeaterBasics` a na stránku přidáte ovládací prvek Repeater a nastavíte jeho vlastnost `ID` na `CategoryList`. Z inteligentní značky Repeater vyberte, chcete-li vytvořit nový prvek ObjectDataSource s názvem `CategoriesDataSource`.

[![název nového prvku ObjectDataSource CategoriesDataSource](nested-data-web-controls-cs/_static/image5.png)](nested-data-web-controls-cs/_static/image4.png)

**Obrázek 2**: pojmenování nové `CategoriesDataSource` ObjectDataSource ([kliknutím zobrazíte obrázek v plné velikosti](nested-data-web-controls-cs/_static/image6.png))

Nastavte prvek ObjectDataSource tak, aby přečetl svá data z `CategoriesBLL` třídy s `GetCategories` metody.

[![nakonfigurovat prvek ObjectDataSource na použití metody CategoriesBLL třídy s GetCategories](nested-data-web-controls-cs/_static/image8.png)](nested-data-web-controls-cs/_static/image7.png)

**Obrázek 3**: Konfigurace prvku ObjectDataSource pro použití `GetCategories` metody `CategoriesBLL` třídy s ([kliknutím zobrazíte obrázek v plné velikosti](nested-data-web-controls-cs/_static/image9.png))

Chcete-li určit obsah šablony opakování s, musíme přejít do zobrazení zdroje a ručně zadat deklarativní syntaxi. Přidejte `ItemTemplate`, který zobrazuje název kategorie v elementu `<h4>` a Popis kategorie s v prvku odstavce (`<p>`). Jednotlivé kategorie se navíc oddělují vodorovným pravidlem (`<hr>`). Po provedení těchto změn by měla stránka obsahovat deklarativní syntaxi pro Repeater a prvek ObjectDataSource, který je podobný následujícímu:

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample1.aspx)]

Obrázek 4 ukazuje náš průběh při prohlížení v prohlížeči.

[![se v seznamu zobrazí všechny kategorie s názvem a popis, oddělené vodorovným pravidlem.](nested-data-web-controls-cs/_static/image11.png)](nested-data-web-controls-cs/_static/image10.png)

**Obrázek 4**: seznam všech kategorií s názvem a popisem jsou uvedeny a odděleny vodorovným pravidlem ([kliknutím zobrazíte obrázek v plné velikosti).](nested-data-web-controls-cs/_static/image12.png)

## <a name="step-2-adding-the-nested-product-repeater"></a>Krok 2: Přidání vnořeného opakovače produktu

Po dokončení seznamu kategorií je dalším úkolem přidání opakovače do `ItemTemplate` `CategoryList` s, které zobrazí informace o těchto produktech patřící do příslušné kategorie. K dispozici je několik způsobů, jak získat data pro tento vnitřní opakovač, z nichž dvakrát prozkoumáme. Prozatím teď stačí vytvořit produkty v rámci `ItemTemplate``CategoryList` Repeater. V případě, že má produkt opakovat, musí mít každý produkt v seznamu s odrážkami všechny položky seznamu, včetně názvu a ceny produktu.

Aby bylo možné vytvořit tohoto opakovače, musíme do `ItemTemplate``CategoryList` s zadat deklarativní syntax a šablony s vnitřním opakováním. Do `ItemTemplate``CategoryList` Repeater přidejte následující kód:

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample2.aspx)]

## <a name="step-3-binding-the-category-specific-products-to-the-productsbycategorylist-repeater"></a>Krok 3: vytvoření vazby produktů specifických pro kategorii k ProductsByCategoryList Repeater

Pokud v tomto okamžiku navštívíte stránku v prohlížeči, vaše obrazovka bude vypadat stejně jako na obrázku 4, protože jsme zatím navázali všechna data na Repeater. K dispozici je několik způsobů, jak můžeme přizpůsobovat příslušné záznamy produktů a navazovat je na Repeater, což je ještě efektivnější než jiné. Hlavní výzva se tady dostává zpátky o příslušné produkty zadané kategorie.

Data, která lze navazovat na vnitřní ovládací prvek Repeater, lze buď přistupovat deklarativně, prostřednictvím prvku ObjectDataSource v `ItemTemplate``CategoryList` Repeater s, nebo programově ze stránky s kódem na pozadí stránky ASP.NET. Podobně tato data mohou být svázána s vnitřním opakovačem buď deklarativně prostřednictvím vlastnosti vnitřní Repeater s `DataSourceID`, nebo prostřednictvím deklarativní syntaxe datových vazeb nebo programově odkazováním na vnitřní opakovač v obslužné rutině události `CategoryList` opakovače s `ItemDataBound`, programově nastavením jeho vlastnosti `DataSource` a voláním metody `DataBind()`. Pojďme si prozkoumat každý z těchto přístupů.

## <a name="accessing-the-data-declaratively-with-an-objectdatasource-control-and-theitemdataboundevent-handler"></a>Deklarativní přístup k datům pomocí ovládacího prvku ObjectDataSource a obslužné rutiny události`ItemDataBound`

Vzhledem k tomu, že jsme v rámci této série kurzů rozsáhle používali ObjectDataSource, je pro přístup k datům v tomto příkladu nejpřirozenější výběr prvku ObjectDataSource. Třída `ProductsBLL` má `GetProductsByCategoryID(categoryID)` metodu, která vrací informace o těchto produktech, které patří do zadaného *`categoryID`* . Proto můžeme přidat prvek ObjectDataSource do `CategoryList` Repeater `ItemTemplate` a nakonfigurovat ho tak, aby měl přístup k datům z této metody třídy s.

Omlouváme se, ale neumožňuje, aby se šablony upravovaly prostřednictvím zobrazení Návrh, takže musíme přidat deklarativní syntaxi pro tento ovládací prvek ObjectDataSource ručně. Následující syntaxe zobrazuje `CategoryList` Repeater `ItemTemplate` po přidání tohoto nového prvku ObjectDataSource (`ProductsByCategoryDataSource`):

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample3.aspx)]

Při použití přístupu ObjectDataSource potřebujeme nastavit vlastnost `ProductsByCategoryList` Repeater s `DataSourceID` na `ID` prvku ObjectDataSource (`ProductsByCategoryDataSource`). Všimněte si také, že náš prvek ObjectDataSource má `<asp:Parameter>` element, který určuje hodnotu *`categoryID`* , která bude předána metodě `GetProductsByCategoryID(categoryID)`. Ale jak tuto hodnotu specifikovat? V ideálním případě je možné pouze nastavit vlastnost `DefaultValue` elementu `<asp:Parameter>` pomocí syntaxe DataBinding, například takto:

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample4.aspx)]

Syntaxe datové vazby bohužel je platná pouze v ovládacích prvcích, které mají událost `DataBinding`. Třída `Parameter` postrádá takovou událost, a proto je výše uvedená syntaxe neplatná a výsledkem bude chyba za běhu.

Pro nastavení této hodnoty musíme vytvořit obslužnou rutinu události pro událost `ItemDataBound` `CategoryList` Repeater. Odvolání, že se událost `ItemDataBound` aktivuje jednou pro každou položku, která je vázaná na Repeater. Proto každé události, která je aktivována pro vnějšího opakovače, můžeme přiřadit aktuální `CategoryID` hodnotu k parametru `ProductsByCategoryDataSource` ObjectDataSource s `CategoryID`.

Vytvořte obslužnou rutinu události pro událost `ItemDataBound` `CategoryList` Repeater s následujícím kódem:

[!code-csharp[Main](nested-data-web-controls-cs/samples/sample5.cs)]

Tato obslužná rutina události se spustí tím, že zajistí, že budeme znovu pracovat s datovou položkou, a ne s hlavičkou, zápatím nebo položkou oddělovače. Dále odkazujeme na skutečnou instanci `CategoriesRow`, která se právě váže na aktuální `RepeaterItem`. Nakonec odkazujeme na prvek ObjectDataSource v `ItemTemplate` a přiřadíte jeho hodnotu parametru `CategoryID` do `CategoryID` aktuální `RepeaterItem`.

V rámci této obslužné rutiny události je `ProductsByCategoryList` opakování v každém `RepeaterItem` vázáno na tyto produkty v kategorii `RepeaterItem` s. Obrázek 5 znázorňuje snímek obrazovky s výsledným výstupem.

[![vnějšího opakovače seznam všech kategorií; Vnitřní seznam obsahuje produkty pro danou kategorii.](nested-data-web-controls-cs/_static/image14.png)](nested-data-web-controls-cs/_static/image13.png)

**Obrázek 5**: vnější opakovač obsahuje všechny kategorie; Vnitřní seznam produktů pro danou kategorii ([kliknutím zobrazíte obrázek v plné velikosti](nested-data-web-controls-cs/_static/image15.png))

## <a name="accessing-the-products-by-category-data-programmatically"></a>Programový přístup k produktům podle dat kategorie

Namísto použití prvku ObjectDataSource k načtení produktů pro aktuální kategorii můžeme vytvořit metodu v naší třídě ASP.NET stránky s kódem na pozadí (nebo ve složce `App_Code` nebo v samostatném projektu knihovny tříd), která vrací příslušnou sadu produktů při předání v `CategoryID`. Představte si, že tato metoda byla v naší třídě ASP.NET stránky s kódem na pozadí a že byla pojmenována `GetProductsInCategory(categoryID)`. V rámci této metody jsme mohli navazovat produkty pro aktuální kategorii na vnitřní opakovač pomocí následující deklarativní syntaxe:

[!code-aspx[Main](nested-data-web-controls-cs/samples/sample6.aspx)]

Vlastnost Repeater s `DataSource` používá syntaxi DataBinding k označení, že data pocházejí z metody `GetProductsInCategory(categoryID)`. Vzhledem k tomu, že `Eval("CategoryID")` vrátí hodnotu typu `Object`, přetypování objektu na `Integer` před předáním do metody `GetProductsInCategory(categoryID)`. Všimněte si, že `CategoryID`, ke kterému se přistupoval prostřednictvím syntaxe datové vazby, je `CategoryID` *vnějšího* opakovače (`CategoryList`), který je svázán s záznamy v tabulce `Categories`. Proto víme, že `CategoryID` nemůže být `NULL` hodnota databáze, což je důvod, proč můžeme metodu `Eval` bez kontroly vrátit, aniž byste museli provádět kontrolu `DBNull`.

V rámci tohoto přístupu potřebujeme vytvořit metodu `GetProductsInCategory(categoryID)` a nechat si načíst příslušnou sadu produktů, které mají poskytnutou *`categoryID`* . Můžeme to provést pouhým vrácením `ProductsDataTable` vráceného metodou `ProductsBLL` třídy s `GetProductsByCategoryID(categoryID)`. Pro naši `NestedControls.aspx` stránku vytvoříme metodu `GetProductsInCategory(categoryID)` v třídě Code-na pozadí. Použijte následující kód:

[!code-csharp[Main](nested-data-web-controls-cs/samples/sample7.cs)]

Tato metoda jednoduše vytvoří instanci metody `ProductsBLL` a vrátí výsledky metody `GetProductsByCategoryID(categoryID)`. Všimněte si, že metoda musí být označena `Public` nebo `Protected`; Pokud je metoda označená jako `Private`, nebude přístupná z deklarativních značek stránky ASP.NET.

Po provedení těchto změn pro použití této nové techniky si chvíli počkejte, než se stránka zobrazí v prohlížeči. Výstup by měl být stejný jako výstup při použití přístupu k obslužné rutině události ObjectDataSource a `ItemDataBound` (Chcete-li zobrazit snímek obrazovky, přejděte zpět na obrázek 5).

> [!NOTE]
> Může se zdát, že busywork vytvořit metodu `GetProductsInCategory(categoryID)` ve třídě ASP.NET stránky s kódem na pozadí. Po tom Tato metoda jednoduše vytvoří instanci třídy `ProductsBLL` a vrátí výsledky její `GetProductsByCategoryID(categoryID)` metody. Proč nestačí volat tuto metodu přímo z syntaxe datové vazby v interním Opakovaču, například: `DataSource='<%# ProductsBLL.GetProductsByCategoryID((int)(Eval("CategoryID"))) %>'`? I když tato syntaxe nebude fungovat s naší aktuální implementací třídy `ProductsBLL` (vzhledem k tomu, že metoda `GetProductsByCategoryID(categoryID)` je metoda instance), můžete upravit `ProductsBLL`, aby zahrnovaly statickou `GetProductsByCategoryID(categoryID)` metodu nebo aby třída zahrnovala statickou `Instance()` metodu pro návrat nové instance třídy `ProductsBLL`.

I když by tyto úpravy vyloučily nutnost `GetProductsInCategory(categoryID)` metoda ve třídě ASP.NET Page s kódem na pozadí, metoda třídy kódu na pozadí poskytuje větší flexibilitu při práci s načtenými daty, jak uvidíme krátce.

## <a name="retrieving-all-of-the-product-information-at-once"></a>Načítání všech informací o produktu najednou

Dva zkontrolují postupy, které jsme prozkoumali, převedli jsme tyto produkty pro aktuální kategorii tím, že provedeme volání metody `ProductsBLL` třídy s `GetProductsByCategoryID(categoryID)` (první přístup byl tak, že by byl druhý prostřednictvím metody `GetProductsInCategory(categoryID)` v třídě Code-na pozadí). Pokaždé, když je tato metoda vyvolána, vrstva obchodní logiky zavolá do vrstvy přístupu k datům, která dotazuje databázi pomocí příkazu jazyka SQL, který vrací řádky z `Products` tabulky, jejichž `CategoryID` pole odpovídá zadanému vstupnímu parametru.

V rámci těchto *N* kategorií v systému tento přístup sítě *n* + 1 volá do databáze databázový dotaz, aby získal všechny kategorie a potom *N* volání pro získání produktů specifických pro jednotlivé kategorie. Můžeme ale načíst všechna potřebná data v jediné dvou databázích voláním jednoho volání, abyste získali všechny kategorie a další pro získání všech produktů. Jakmile máme všechny produkty, můžeme tyto produkty filtrovat, aby byly na tuto kategorii s vnitřním opakovačem vázány jenom produkty odpovídající aktuálnímu `CategoryID`.

Abychom tuto funkci mohli poskytnout, musíme v naší třídě ASP.NET stránky s kódem na pozadí udělat mírněu úpravu metody `GetProductsInCategory(categoryID)`. Místo toho, abyste nemuseli vracet výsledky `ProductsBLL` třídy s `GetProductsByCategoryID(categoryID)`, můžeme místo toho nejdřív přistupovat ke *všem* produktům (Pokud k nim ještě nedošlo) a pak vracet jenom filtrované zobrazení produktů na základě předaných `CategoryID`.

[!code-csharp[Main](nested-data-web-controls-cs/samples/sample8.cs)]

Všimněte si přidání proměnné na úrovni stránky `allProducts`. Tím se uchovávají informace o všech produktech a vyplní se při prvním vyvolání metody `GetProductsInCategory(categoryID)`. Po zajistěte, aby byl objekt `allProducts` vytvořen a naplněn, metoda vyfiltruje výsledky DataTable, aby byly přístupné pouze ty řádky, jejichž `CategoryID` odpovídá zadanému `CategoryID`. Tento přístup snižuje počet přístupů k databázi z *N* + 1 dolů na dvě.

Toto vylepšení nezavádí žádné změny vykresleného kódu stránky ani nevrací méně záznamů než druhý přístup. Jednoduše snižuje počet volání databáze.

> [!NOTE]
> Jedním z nich může být intuitivní důvod, který snižuje počet přístupů k databázím, což zvyšuje výkon. To ale nemusí být případ. Pokud máte velký počet produktů, jejichž `CategoryID` je `NULL`například, pak volání metody `GetProducts` vrátí počet produktů, které nejsou nikdy zobrazeny. Kromě toho může být vrácení všech produktů wasteful, pokud znovu zobrazíte pouze podmnožinu kategorií, což může být případ, pokud jste implementovali stránkování.

Stejně jako vždy, když přichází k analýze výkonu dvou technik, je jedinou surefireou mírou spuštění řízených testů přizpůsobených pro běžné scénáře v případě použití aplikace.

## <a name="summary"></a>Přehled

V tomto kurzu jsme viděli, jak v rámci sebe vnořovat webové ovládací prvky pro data, konkrétně si prozkoumáte, jak má vnější opakovač Zobrazit položku pro každou kategorii s vnitřním opakovačem, který obsahuje seznam produktů pro každou kategorii v seznamu s odrážkami. Hlavní výzva při sestavování vnořeného uživatelského rozhraní je v přístupu a vázání správných dat k webovému ovládacímu prvku pro vnitřní data. K dispozici je celá řada techniků, z nichž dva jsme prozkoumali v tomto kurzu. První metoda zkoumala použití prvku ObjectDataSource v ovládacím prvku webového ovládacího prvku s vnějším daty `ItemTemplate`, který byl svázán s ovládacím prvkem pro vnitřní data prostřednictvím jeho vlastnosti `DataSourceID`. Druhá technika získala data prostřednictvím metody ve třídě ASP.NET stránky s kódem na pozadí. Tato metoda může být svázána s vlastností webového ovládacího prvku s vnitřním daty `DataSource` prostřednictvím syntaxe datové vazby.

Přestože vložené uživatelské rozhraní v tomto kurzu použilo pro opakování vnořený argument, lze tyto techniky rozšířit na jiné webové ovládací prvky dat. Můžete vnořit Repeater do prvku GridView nebo GridView v rámci prvku DataList a tak dále.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Zack Novotný a Liz Shulok. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](showing-multiple-records-per-row-with-the-datalist-control-cs.md)
> [Další](displaying-data-with-the-datalist-and-repeater-controls-vb.md)

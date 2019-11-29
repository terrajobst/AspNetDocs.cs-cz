---
uid: web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-vb
title: Vytvoření vlastního zprostředkovatele mapy webu založeného na databázi (VB) | Microsoft Docs
author: rick-anderson
description: Výchozí poskytovatel mapy webu v ASP.NET 2,0 načte jeho data ze statického souboru XML. I když je zprostředkovatel založený na jazyce XML vhodný pro mnoho malých a středně sizch...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: f904cd2c-a408-4484-9324-8b8d7fe33893
msc.legacyurl: /web-forms/overview/data-access/database-driven-site-maps/building-a-custom-database-driven-site-map-provider-vb
msc.type: authoredcontent
ms.openlocfilehash: 78051696bd75e1d574f55b1c5d5891fe67c3030d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74630064"
---
# <a name="building-a-custom-database-driven-site-map-provider-vb"></a>Vytvoření vlastního databázově řízeného zprostředkovatele mapy webu (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_62_VB.zip) nebo [stažení PDF](building-a-custom-database-driven-site-map-provider-vb/_static/datatutorial62vb1.pdf)

> Výchozí poskytovatel mapy webu v ASP.NET 2,0 načte jeho data ze statického souboru XML. I když je zprostředkovatel založený na jazyce XML vhodný pro velký počet malých a středně velkých webů, vyžadují větší webové aplikace dynamičtější mapy webu. V tomto kurzu vytvoříme vlastního poskytovatele mapy webu, který načte svá data z vrstvy obchodní logiky, která zase načte data z databáze.

## <a name="introduction"></a>Úvod

Funkce mapa webu ASP.NET 2,0 s umožňuje vývojářům stránky definovat mapu webu webové aplikace v některém trvalém médiu, například v souboru XML. Po definování můžete k datům map lokality přistupovat programově prostřednictvím [třídy`SiteMap`](https://msdn.microsoft.com/library/system.web.sitemap.aspx) v [oboru názvů`System.Web`](https://msdn.microsoft.com/library/system.web.aspx) nebo prostřednictvím různých webových ovládacích prvků navigace, jako jsou ovládací prvky SiteMapPath, menu a TreeView. Mapový systém lokality používá [model poskytovatele](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx) , aby bylo možné vytvořit různé implementace serializace mapy webu a připojit je do webové aplikace. Výchozí poskytovatel mapy webu, který je dodáván s ASP.NET 2,0, se zachovává se strukturou mapy webu v souboru XML. Zpět na [stránkách předlohy a](../introduction/master-pages-and-site-navigation-vb.md) v kurzu navigace na webu jsme vytvořili soubor s názvem `Web.sitemap`, který obsahuje tuto strukturu a aktualizovali XML pomocí každého nového kurzu.

Výchozí zprostředkovatel mapy webu založený na jazyce XML funguje dobře, pokud je struktura mapy webu poměrně statická, například pro tyto kurzy. V mnoha scénářích se však vyžaduje více map dynamického webu. Vezměte v úvahu mapu webu znázorněnou na obrázku 1, kde se každá kategorie a produkt zobrazuje jako oddíly ve struktuře webu. Pomocí této mapy webu mohou webové stránky, které odpovídají kořenovému uzlu, obsahovat seznam všech kategorií, zatímco při návštěvě konkrétní kategorie webové stránky by se zobrazily tyto kategorie produktů a zobrazení konkrétní webové stránky s informacemi o produktu.

[![kategorií a produktů strukturu struktury map webu](building-a-custom-database-driven-site-map-provider-vb/_static/image1.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image1.png)

**Obrázek 1**: kategorie a produkty strukturu struktury map webu ([kliknutím zobrazíte obrázek v plné velikosti](building-a-custom-database-driven-site-map-provider-vb/_static/image2.png)).

Zatímco tato struktura na základě kategorie a produktu by mohla být pevně zakódovaná do `Web.sitemap` souboru, je třeba aktualizovat soubor pokaždé, když byla kategorie nebo produkt přidaný, odebraný nebo přejmenovaný. V důsledku toho bude údržba mapy webu výrazně zjednodušená, pokud byla jeho struktura načtena z databáze nebo, v ideálním případě z vrstvy obchodní logiky architektury aplikace. Tímto způsobem byly přidány, přejmenovány nebo smazány produkty a kategorie, mapa webu se automaticky aktualizuje, aby odrážela tyto změny.

Vzhledem k tomu, že serializace mapy lokality ASP.NET 2,0 s je sestavena základem modelem poskytovatele, můžeme vytvořit vlastního poskytovatele mapy webu, který získává data z alternativního úložiště dat, například databáze nebo architektury. V tomto kurzu vytvoříme vlastního poskytovatele, který načte data z knihoven BLL. Pojďme začít!

> [!NOTE]
> Vlastní poskytovatel mapy webu vytvořený v tomto kurzu je pevně spojený s architekturou aplikace a datovým modelem. Jan Prosise s [uložením map webů v SQL Server](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/) a [poskytovatele mapy webu SQL, kterého jste čekali na články,](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx) prozkoumali zobecněný přístup k ukládání dat map webu v SQL Server.

## <a name="step-1-creating-the-custom-site-map-provider-web-pages"></a>Krok 1: vytvoření vlastních webových stránek poskytovatele mapy webu

Než začneme s vytvářením vlastního poskytovatele mapy webu, můžeme nejdřív přidat stránky ASP.NET, které budeme potřebovat pro tento kurz. Začněte přidáním nové složky s názvem `SiteMapProvider`. Dále přidejte následující stránky ASP.NET do této složky a nezapomeňte přidružit jednotlivé stránky k `Site.master` hlavní stránce:

- `Default.aspx`
- `ProductsByCategory.aspx`
- `ProductDetails.aspx`

Přidejte také podsložku `CustomProviders` do složky `App_Code`.

![Přidání stránek ASP.NET pro kurzy související se zprostředkovatelem mapy webu](building-a-custom-database-driven-site-map-provider-vb/_static/image2.gif)

**Obrázek 2**: přidání stránek ASP.NET pro kurzy související se zprostředkovatelem mapy webu

Vzhledem k tomu, že je k dispozici pouze jeden kurz pro tuto část, nepotřebujeme `Default.aspx` k vypsání kurzů oddílu s. Místo toho `Default.aspx` zobrazí kategorie v ovládacím prvku GridView. Budeme to řešit v kroku 2.

Dále aktualizujte `Web.sitemap` tak, aby obsahovaly odkaz na stránku `Default.aspx`. Konkrétně přidejte následující kód po `<siteMapNode>`ukládání do mezipaměti:

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample1.xml)]

Po aktualizaci `Web.sitemap`chvíli počkejte, než se zobrazí web kurzy prostřednictvím prohlížeče. Nabídka na levé straně teď obsahuje položku pro jediný kurz pro poskytovatele mapy webu.

![Mapa webu teď obsahuje položku kurzu pro poskytovatele mapy webu.](building-a-custom-database-driven-site-map-provider-vb/_static/image3.gif)

**Obrázek 3**: Mapa webu teď obsahuje položku kurzu pro poskytovatele mapy webu.

V tomto kurzu s hlavním fokusem je znázornění vytvoření vlastního poskytovatele mapy webu a konfigurace webové aplikace pro použití tohoto poskytovatele. Konkrétně sestavíme poskytovatele, který vrátí mapu webu, která obsahuje kořenový uzel společně s uzlem pro každou kategorii a produkt, jak je znázorněno na obrázku 1. Obecně platí, že každý uzel v mapě webu může určovat adresu URL. Pro naši mapu webu bude `~/SiteMapProvider/Default.aspx`adresa URL kořenového uzlu, která bude obsahovat seznam všech kategorií v databázi. U každého uzlu kategorie v mapě webu bude uvedena adresa URL, která odkazuje na `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID`. zobrazí se seznam všech produktů v zadaném *poli ČísloKategorie*. Nakonec bude každý uzel mapa webu produktu ukazovat na `~/SiteMapProvider/ProductDetails.aspx?ProductID=productID`, ve kterém se zobrazí konkrétní podrobnosti o produktu.

Abychom mohli začít, musíme vytvořit `Default.aspx`, `ProductsByCategory.aspx`a `ProductDetails.aspx` stránky. Tyto stránky jsou dokončeny v krocích 2, 3 a 4 v uvedeném pořadí. Vzhledem k tomu, že je tah tohoto kurzu na poskytovatelích mapy webu a vzhledem k tomu, že minulé kurzy pokryly vytváření těchto seřazení vícestránkových sestav s více stránkami a podrobnostmi, budeme Pospěšte si prostřednictvím kroků 2 až 4. Pokud potřebujete aktualizační program pro vytváření sestav hlavní/podrobnosti, které jsou rozloženy na více stránkách, přečtěte si kurz pro [filtrování hlavní/podrobnosti na dvou stránkách](../masterdetail/master-detail-filtering-across-two-pages-vb.md) .

## <a name="step-2-displaying-a-list-of-categories"></a>Krok 2: zobrazení seznamu kategorií

Otevřete stránku `Default.aspx` ve složce `SiteMapProvider` a přetáhněte prvek GridView z panelu nástrojů do návrháře a nastavte jeho `ID` na `Categories`. Z inteligentní značky GridView s, navažte ji na nový prvek ObjectDataSource s názvem `CategoriesDataSource` a nakonfigurujte ho tak, aby se jeho data navázala pomocí metody `GetCategories` `CategoriesBLL` třídy s. Vzhledem k tomu, že tento prvek GridView pouze zobrazí kategorie a neposkytuje možnosti změny dat, nastavte rozevírací seznamy na kartách aktualizace, vložení a odstranění na hodnotu (žádné).

[![nakonfigurovat prvek ObjectDataSource tak, aby vracel kategorie pomocí metody GetCategories](building-a-custom-database-driven-site-map-provider-vb/_static/image4.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image3.png)

**Obrázek 4**: Konfigurace prvku ObjectDataSource tak, aby vracela kategorie pomocí metody `GetCategories` ([kliknutím zobrazíte obrázek v plné velikosti](building-a-custom-database-driven-site-map-provider-vb/_static/image4.png))

[![nastavení rozevíracích seznamů na kartách aktualizace, vložení a odstranění na (žádné)](building-a-custom-database-driven-site-map-provider-vb/_static/image5.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image5.png)

**Obrázek 5**: nastavení rozevíracích seznamů na kartách aktualizace, vložení a odstranění na (žádné) ([kliknutím zobrazíte obrázek v plné velikosti).](building-a-custom-database-driven-site-map-provider-vb/_static/image6.png)

Po dokončení Průvodce konfigurací zdroje dat přidá Visual Studio vlastnost BoundField pro `CategoryID`, `CategoryName`, `Description`, `NumberOfProducts`a `BrochurePath`. Upravte prvek GridView tak, že obsahuje pouze `CategoryName` a `Description` BoundFields a aktualizujte vlastnost `HeaderText` `CategoryName` vlastnost BoundField s na kategorii.

Dále přidejte HyperLinkField a umístěte ji tak, aby byla v poli nejvíce vlevo. Vlastnost `DataNavigateUrlFields` nastavte na `CategoryID` a vlastnost `DataNavigateUrlFormatString` na `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID={0}`. Pro zobrazení produktů nastavte vlastnost `Text`.

![Přidání HyperLinkField do kategorií GridView](building-a-custom-database-driven-site-map-provider-vb/_static/image6.gif)

**Obrázek 6**: Přidání prvku HyperLinkField do prvku GridView `Categories`

Po vytvoření prvku ObjectDataSource a přizpůsobení polí GridViewu budou tyto dva ovládací prvky deklarativním označením vypadat takto:

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample2.aspx)]

Obrázek 7 zobrazuje `Default.aspx` při prohlížení v prohlížeči. Kliknutím na odkaz Zobrazit produkty ve kategoriích přejdete na `ProductsByCategory.aspx?CategoryID=categoryID`, které budeme sestavit v kroku 3.

[![je každá kategorie uvedená spolu s odkazem Zobrazit produkty.](building-a-custom-database-driven-site-map-provider-vb/_static/image7.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image7.png)

**Obrázek 7**: Každá kategorie je uvedena spolu s odkazem Zobrazit produkty ([kliknutím zobrazíte obrázek v plné velikosti](building-a-custom-database-driven-site-map-provider-vb/_static/image8.png)).

## <a name="step-3-listing-the-selected-category-s-products"></a>Krok 3: výpis vybraných produktů kategorie s

Otevřete stránku `ProductsByCategory.aspx` a přidejte prvek GridView a pojmenujte ho `ProductsByCategory`. Z jeho inteligentní značky svažte prvek GridView s novým prvkem ObjectDataSource s názvem `ProductsByCategoryDataSource`. Nastavte prvek ObjectDataSource na použití `GetProductsByCategoryID(categoryID)` metody `ProductsBLL` třídy s a nastavte rozevírací seznamy na (žádné) na kartách aktualizace, vložení a odstranění.

[![použít metodu ProductsBLL třídy s GetProductsByCategoryID (KódKategorie)](building-a-custom-database-driven-site-map-provider-vb/_static/image8.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image9.png)

**Obrázek 8**: použijte metodu `GetProductsByCategoryID(categoryID)` `ProductsBLL` třídy s ([kliknutím zobrazíte obrázek v plné velikosti](building-a-custom-database-driven-site-map-provider-vb/_static/image10.png)).

Poslední krok v Průvodci konfigurací zdroje dat vyzve k zadání zdroje parametru pro *KódKategorie*. Vzhledem k tomu, že tyto informace jsou předány pomocí pole QueryString `CategoryID`, v rozevíracím seznamu vyberte hodnotu QueryString a do textového pole vlastnost QueryStringField zadejte KódKategorie, jak je znázorněno na obrázku 9. Kliknutím na Dokončit dokončete průvodce.

[![použít pole QueryString dotazu KódKategorie pro parametr KódKategorie](building-a-custom-database-driven-site-map-provider-vb/_static/image9.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image11.png)

**Obrázek 9**: použijte pole `CategoryID` QueryString pro parametr *CategoryID* ([kliknutím zobrazíte obrázek v plné velikosti](building-a-custom-database-driven-site-map-provider-vb/_static/image12.png)).

Po dokončení Průvodce přidá Visual Studio odpovídající BoundFields a třídě CheckBoxField podporována do prvku GridView pro pole dat produktu. Odeberte všechny kromě `ProductName`, `UnitPrice`a `SupplierName` BoundFields. Přizpůsobte tyto tři BoundFields `HeaderText` vlastností, abyste si mohli přečíst produkt, cenu a dodavatele v uvedeném pořadí. Naformátujte `UnitPrice` vlastnost BoundField jako měnu.

Dále přidejte HyperLinkField a přesuňte ji do nejvyšší pozice. Vlastnost `Text` nastavte na hodnotu Zobrazit podrobnosti, její vlastnost `DataNavigateUrlFields` na `ProductID`a její vlastnost `DataNavigateUrlFormatString` na `~/SiteMapProvider/ProductDetails.aspx?ProductID={0}`.

![Přidejte podrobnosti zobrazení HyperLinkField, které odkazuje na ProductDetails. aspx.](building-a-custom-database-driven-site-map-provider-vb/_static/image10.gif)

**Obrázek 10**: Přidání podrobností zobrazení HyperLinkField, které odkazuje na `ProductDetails.aspx`

Po provedení těchto úprav by deklarativní označení GridView a ObjectDataSource s mělo vypadat takto:

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample3.aspx)]

Vraťte se do zobrazení `Default.aspx` přes prohlížeč a klikněte na odkaz Zobrazit produkty pro nápoje. Tím přejdete na `ProductsByCategory.aspx?CategoryID=1`a zobrazí se názvy, ceny a dodavatelé produktů v databázi Northwind, které patří do kategorie nápoje (viz obrázek 11). Tuto stránku můžete dál vylepšit tak, aby obsahovala odkaz pro vracení uživatelů na stránku seznamu kategorií (`Default.aspx`) a ovládací prvek DetailsView nebo FormView, který zobrazuje název a Popis kategorie s názvem.

[![se zobrazí názvy nápojů, ceny a dodavatelé.](building-a-custom-database-driven-site-map-provider-vb/_static/image11.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image13.png)

**Obrázek 11**: zobrazí se názvy nápojů, ceny a dodavatelé ([kliknutím zobrazíte obrázek v plné velikosti).](building-a-custom-database-driven-site-map-provider-vb/_static/image14.png)

## <a name="step-4-showing-a-product-s-details"></a>Krok 4: zobrazení podrobností o produktu

Poslední stránka, `ProductDetails.aspx`, zobrazí vybrané podrobnosti o produktech. Otevřete `ProductDetails.aspx` a přetáhněte prvek DetailsView z panelu nástrojů na Návrhář. Nastavte vlastnost `ID` ovládacího prvku DetailsView na `ProductInfo` a vymažte hodnoty vlastností `Height` a `Width`. Z jeho inteligentní značky navažte prvek DetailsView na nový prvek ObjectDataSource s názvem `ProductDataSource`a nakonfigurujte prvek ObjectDataSource, aby vyčetl data z metody `GetProductByProductID(productID)` `ProductsBLL` třídy s. Stejně jako u předchozích webových stránek vytvořených v krocích 2 a 3 nastavte rozevírací seznamy na kartách aktualizace, vložení a odstranění na (žádné).

[![nakonfigurovat prvek ObjectDataSource na použití metody GetProductByProductID (productID)](building-a-custom-database-driven-site-map-provider-vb/_static/image12.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image15.png)

**Obrázek 12**: Konfigurace prvku ObjectDataSource pro použití metody `GetProductByProductID(productID)` ([kliknutím zobrazíte obrázek v plné velikosti](building-a-custom-database-driven-site-map-provider-vb/_static/image16.png))

Poslední krok průvodce konfigurací zdroje dat vyzve k zadání zdroje parametru *ProductID* . Vzhledem k tomu, že tato data přicházejí pomocí pole QueryString `ProductID`, nastavte rozevírací seznam na QueryString a textové pole vlastnost QueryStringField na ProductID. Nakonec kliknutím na tlačítko Dokončit průvodce dokončete.

[![nakonfigurovat parametr productID, aby vyčetl svou hodnotu z pole ProductID QueryString.](building-a-custom-database-driven-site-map-provider-vb/_static/image13.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image17.png)

**Obrázek 13**: Konfigurace parametru *ProductID* , který načte svou hodnotu z pole `ProductID` QueryString ([kliknutím zobrazíte obrázek v plné velikosti](building-a-custom-database-driven-site-map-provider-vb/_static/image18.png))

Po dokončení Průvodce konfigurací zdroje dat vytvoří Visual Studio odpovídající BoundFields a třídě CheckBoxField podporována v ovládacím prvku pro pole dat produktu. Odeberte `ProductID`, `SupplierID`a `CategoryID` BoundFields a nakonfigurujte zbývající pole podle potřeby. Po několiki estetických konfigurací je můj ovládací prvek DetailsView a ObjectDataSource s podobným kódem jako následující:

[!code-aspx[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample4.aspx)]

Tuto stránku otestujete tak, že se vrátíte do `Default.aspx` a kliknete na Zobrazit produkty pro kategorii nápoje. Ze seznamu nápojových produktů klikněte na odkaz Zobrazit podrobnosti pro Chai čaj. Tím přejdete na `ProductDetails.aspx?ProductID=1`, které zobrazí podrobnosti Chai čaj s (viz obrázek 14).

[Zobrazí se ![Chai čaj s dodavatel, kategorie, cena a další informace.](building-a-custom-database-driven-site-map-provider-vb/_static/image14.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image19.png)

**Obrázek 14**: zobrazí se hodnota Chai čaj s, kategorie, ceny a další informace ([kliknutím zobrazíte obrázek v plné velikosti).](building-a-custom-database-driven-site-map-provider-vb/_static/image20.png)

## <a name="step-5-understanding-the-inner-workings-of-a-site-map-provider"></a>Krok 5: princip interních pracovních kroků poskytovatele mapy webu

Mapa webu je reprezentovaná v paměti webového serveru jako kolekce instancí `SiteMapNode`, které tvoří hierarchii. Musí existovat přesně jeden kořen, všechny nekořenové uzly musí mít přesně jeden nadřazený uzel a všechny uzly mohou mít libovolný počet podřízených objektů. Každý objekt `SiteMapNode` představuje oddíl ve struktuře webu. Tyto oddíly často obsahují odpovídající webovou stránku. V důsledku toho má [třída`SiteMapNode`](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx) vlastnosti jako `Title`, `Url`a `Description`, které poskytují informace pro oddíl, který `SiteMapNode` představuje. K dispozici je také vlastnost `Key`, která jednoznačně identifikuje každý `SiteMapNode` v hierarchii a také vlastnosti používané k vytvoření této hierarchie `ChildNodes`, `ParentNode`, `NextSibling`, `PreviousSibling`a tak dále.

Obrázek 15 ukazuje obecnou strukturu mapy webu z obrázku 1, ale podrobné informace o implementaci jsou vysvětlené podrobněji.

[![každý oddíl SiteMapNode má vlastnosti, jako je název, adresa URL, klíč a tak dále.](building-a-custom-database-driven-site-map-provider-vb/_static/image16.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image15.gif)

**Obrázek 15**: každá `SiteMapNode` má vlastnosti jako `Title`, `Url`, `Key`a tak dále ([kliknutím zobrazíte obrázek v plné velikosti).](building-a-custom-database-driven-site-map-provider-vb/_static/image17.gif)

Mapa webu je přístupná prostřednictvím [třídy`SiteMap`](https://msdn.microsoft.com/library/system.web.sitemap.aspx) v [oboru názvů`System.Web`](https://msdn.microsoft.com/library/system.web.aspx). Tato vlastnost `RootNode` třídy vrací instanci kořenového `SiteMapNode` mapy webu. `CurrentNode` vrátí `SiteMapNode`, jehož vlastnost `Url` odpovídá adrese URL aktuálně požadované stránky. Tato třída se používá interně pro navigační webové ovládací prvky ASP.NET 2,0 s.

Pokud jsou k dispozici vlastnosti `SiteMap` třídy, musí serializovat strukturu mapy webu z nějakého trvalého média do paměti. Logika serializace mapy webu však není pevně zakódována do `SiteMap` třídy. Místo toho je za běhu `SiteMap` třída určit, který *poskytovatel* mapy webu se má použít pro serializaci. Ve výchozím nastavení se používá [třída`XmlSiteMapProvider`](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx) , která čte strukturu map webu ze správně formátovaného souboru XML. Nicméně s trochou práce můžeme vytvořit vlastního poskytovatele mapy webu.

Všichni poskytovatelé map webu musí být odvozeni od [`SiteMapProvider` třídy](https://msdn.microsoft.com/library/system.web.sitemapprovider.aspx), která zahrnuje základní metody a vlastnosti potřebné pro poskytovatele mapy webu, ale vynechává mnoho podrobností implementace. Druhá třída, [`StaticSiteMapProvider`](https://msdn.microsoft.com/library/system.web.staticsitemapprovider.aspx), rozšiřuje třídu `SiteMapProvider` a obsahuje robustnější implementaci potřebných funkcí. Interně `StaticSiteMapProvider` ukládá `SiteMapNode` instance mapy webu do `Hashtable` a poskytuje metody jako `AddNode(child, parent)`, `RemoveNode(siteMapNode),` a `Clear()`, které přidávají a odstraňují `SiteMapNode` s interní `Hashtable`. `XmlSiteMapProvider` je odvozen z `StaticSiteMapProvider`.

Při vytváření vlastního poskytovatele mapy webu, který rozšiřuje `StaticSiteMapProvider`, existují dvě abstraktní metody, které musí být přepsány: [`BuildSiteMap`](https://msdn.microsoft.com/library/system.web.staticsitemapprovider.buildsitemap.aspx) a [`GetRootNodeCore`](https://msdn.microsoft.com/library/system.web.sitemapprovider.getrootnodecore.aspx). `BuildSiteMap`, jak název naznačuje, zodpovídá za načtení struktury mapy webu z trvalého úložiště a jeho sestavení v paměti. `GetRootNodeCore` vrátí kořenový uzel na mapě webu.

Než může webová aplikace použít poskytovatele mapy webu, musí být zaregistrovaná v konfiguraci aplikace. Ve výchozím nastavení je třída `XmlSiteMapProvider` registrována pomocí `AspNetXmlSiteMapProvider`názvu. Chcete-li zaregistrovat další poskytovatele map webu, přidejte následující kód pro `Web.config`:

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample5.xml)]

Hodnota *Name* přiřadí poskytovateli popisný název, zatímco *typ* Určuje plně kvalifikovaný název typu poskytovatele mapy webu. Po vytvoření našeho vlastního poskytovatele mapy webu prozkoumáme konkrétní hodnoty *názvu* a hodnot *typu* v kroku 7.

Je vytvořena instance třídy poskytovatele mapy webu při prvním přístupu z třídy `SiteMap` a zůstane v paměti po dobu životnosti webové aplikace. Vzhledem k tomu, že existuje pouze jedna instance poskytovatele mapy webu, kterou lze vyvolat od více souběžných návštěvníků webu, je nezbytné, aby metody poskytovatele s byly bezpečné pro přístup z více *vláken*.

V zájmu výkonu a škálovatelnosti je důležité, abyste do mezipaměti naukládali strukturu mapy lokality v paměti a místo opakovaného vytváření nevytvořili tuto strukturu uloženou v mezipaměti, a to i při každém vyvolání metody `BuildSiteMap`. v závislosti na tom, jaké navigační ovládací prvky se používají na stránce a hloubku struktury mapy webu, může být `BuildSiteMap` pro požadavek na stránku vyvoláno několikrát. Pokud v žádném případě neukládáme do mezipaměti strukturu mapy webu v `BuildSiteMap` pak pokaždé, když se vyvolá, potřebujeme znovu načíst informace o produktech a kategoriích z architektury (což by způsobilo dotaz na databázi). Jak jsme probrali v předchozích kurzech pro ukládání do mezipaměti, můžou být data v mezipaměti zastaralá. V takovém případě můžeme použít buď vypršení platnosti, nebo vypršení platnosti SQL cache založené na závislostech.

> [!NOTE]
> Poskytovatel mapy webu může volitelně přepsat [metodu`Initialize`](https://msdn.microsoft.com/library/system.web.sitemapprovider.initialize.aspx). `Initialize` se vyvolá při prvním vytvoření instance poskytovatele mapy webu a předává se všem vlastním atributům přiřazeným poskytovateli v `Web.config` v elementu `<add>`, jako je: `<add name="name" type="type" customAttribute="value" />`. To je užitečné, pokud chcete, aby vývojář stránky mohl určit různá nastavení týkající se poskytovatele mapy webu bez nutnosti upravovat kód poskytovatele s. Například pokud jsme načetli data kategorií a produktů přímo z databáze na rozdíl od architektury, je vhodné, aby vývojář stránky místo použití pevně kódované hodnoty v kódu poskytovatele umožnil určit připojovací řetězec databáze prostřednictvím `Web.config`. Vlastní poskytovatel mapy webu, který sestavíme v kroku 6, nepřepisuje tuto metodu `Initialize`. Příklad použití metody `Initialize` najdete v článku [Jan Prosise](http://www.wintellect.com/Weblogs/CategoryView,category,Jeff%20Prosise.aspx) s [uložením map webu v SQL Server](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/) článku.

## <a name="step-6-creating-the-custom-site-map-provider"></a>Krok 6: Vytvoření vlastního poskytovatele mapy webu

Abychom vytvořili vlastního poskytovatele mapy webu, který vytvoří mapu webu z kategorií a produktů v databázi Northwind, musíme vytvořit třídu, která rozšiřuje `StaticSiteMapProvider`. V kroku 1 jste požádali o přidání složky `CustomProviders` do složky `App_Code` – přidejte novou třídu do této složky s názvem `NorthwindSiteMapProvider`. Do `NorthwindSiteMapProvider` třídy přidejte následující kód:

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample6.vb)]

Pojďme začít prozkoumávat tuto metodu `BuildSiteMap` třídy, která začíná [příkazem`lock`](https://msdn.microsoft.com/library/c5kehkcz.aspx). Příkaz `lock` umožňuje zadat pouze jedno vlákno v čase, a tím i serializaci přístupu ke svému kódu a zabránění dvěma souběžným vláknům z krokování na jednom dalším nohou.

`root` `SiteMapNode` proměnné na úrovni třídy slouží k ukládání struktury mapy webu do mezipaměti. Když je mapa webu vytvořena poprvé nebo poprvé po změně podkladových dat, `root` bude `Nothing` a bude vytvořena struktura mapy webu. Kořenový uzel map webu s je přiřazen `root` během procesu vytváření, takže při příštím volání této metody `root` nebude `Nothing`. Proto pokud `root` není `Nothing` struktura mapy webu se vrátí volajícímu, aniž by ji museli znovu vytvořit.

Pokud je kořen `Nothing`, vytvoří se struktura mapy webu z informací o produktu a kategorii. Mapa webu je sestavena vytvořením instancí `SiteMapNode` a následným vytvořením hierarchie prostřednictvím volání metody `AddNode` `StaticSiteMapProvider` třídy s. `AddNode` provádí interní účetnictví a ukládá instance `SiteMapNode` roztříděné do `Hashtable`. Předtím, než začneme sestavovat hierarchii, začneme voláním metody `Clear`, která vymaže prvky z interního `Hashtable`. Dále je metoda `ProductsBLL` třídy s `GetProducts` a výsledná `ProductsDataTable` uložená v místních proměnných.

Konstrukce mapy webu začíná vytvořením kořenového uzlu a jeho přiřazením `root`. Přetížení [konstruktoru`SiteMapNode` s](https://msdn.microsoft.com/library/system.web.sitemapnode.sitemapnode.aspx) , který se tady používá, a v rámci této `BuildSiteMap` se předaly tyto informace:

- Odkaz na zprostředkovatele mapy webu (`Me`).
- `Key``SiteMapNode` s. Požadovaná hodnota musí být pro každý `SiteMapNode`jedinečná.
- `Url``SiteMapNode` s. `Url` je volitelné, ale pokud je k dispozici, musí být každá hodnota `Url` `SiteMapNode` s jedinečná.
- `Title`, který je třeba zadat `SiteMapNode` s.

Volání metody `AddNode(root)` přidá `SiteMapNode` `root` na mapu webu jako kořen. V dalším kroku se zobrazí výčet všech `ProductRow` ve `ProductsDataTable`. Pokud již existuje `SiteMapNode` pro aktuální kategorii produktů, odkaz na ni. V opačném případě je nová `SiteMapNode` pro kategorii vytvořena a přidána jako podřízená `SiteMapNode``root` prostřednictvím volání metody `AddNode(categoryNode, root)`. Po nalezení nebo vytvoření odpovídající kategorie `SiteMapNode` uzel se vytvoří `SiteMapNode` pro aktuální produkt a přidá se jako podřízený prvek kategorie `SiteMapNode` prostřednictvím `AddNode(productNode, categoryNode)`. Všimněte si, že hodnota vlastnosti `SiteMapNode` kategorie `Url` je `~/SiteMapProvider/ProductsByCategory.aspx?CategoryID=categoryID`, zatímco vlastnost `SiteMapNode` s produktem `Url` má přiřazen `~/SiteMapNode/ProductDetails.aspx?ProductID=productID`.

> [!NOTE]
> Tyto produkty, které mají hodnotu `NULL` databáze pro jejich `CategoryID` jsou seskupeny do kategorie `SiteMapNode` jejichž vlastnost `Title` je nastavena na hodnotu None a jejíž vlastnost `Url` je nastavena na prázdný řetězec. Rozhodli jste se nastavit `Url` na prázdný řetězec, protože metoda `ProductBLL` třídy `GetProductsByCategory(categoryID)` v tuto chvíli neobsahuje schopnost vracet jenom tyto produkty s hodnotou `NULL` `CategoryID`. Také jsem chtěl předvést, jak navigační ovládací prvky vykreslují `SiteMapNode`, který postrádá hodnotu pro jeho vlastnost `Url`. Doporučujem, abyste tento kurz rozšířili tak, aby se vlastnost None `SiteMapNode` s `Url` na `ProductsByCategory.aspx`, ale zobrazila se jenom produkty s hodnotami `NULL` `CategoryID`.

Po sestavení mapy webu je do mezipaměti dat přidán libovolný objekt pomocí závislosti mezipaměti SQL na `Categories` a `Products` tabulek prostřednictvím objektu `AggregateCacheDependency`. Prozkoumali jsme pomocí závislostí mezipaměti SQL v předchozím kurzu *pomocí závislostí mezipaměti SQL*. Vlastní poskytovatel mapy webu však používá přetížení metody datové mezipaměti s `Insert`, kterou jsme ještě prozkoumali. Toto přetížení přijímá jako konečný vstupní parametr delegáta, který je volán při odebrání objektu z mezipaměti. Konkrétně Předáte novému [delegátu`CacheItemRemovedCallback`](https://msdn.microsoft.com/library/system.web.caching.cacheitemremovedcallback.aspx) , který odkazuje na metodu `OnSiteMapChanged` definovanou níže ve třídě `NorthwindSiteMapProvider`.

> [!NOTE]
> Reprezentace mapy webu v paměti je uložená v mezipaměti prostřednictvím proměnné na úrovni třídy `root`. Vzhledem k tomu, že existuje pouze jedna instance třídy vlastního zprostředkovatele mapy webu a protože tato instance je sdílena mezi všemi vlákny webové aplikace, tato proměnná třídy slouží jako mezipaměť. Metoda `BuildSiteMap` také používá datovou mezipaměť, ale pouze jako způsob, jak dostávat oznámení, když se změní podkladová data databáze v tabulkách `Categories` nebo `Products`. Všimněte si, že hodnota vložená do mezipaměti dat je pouze aktuální datum a čas. Skutečná data mapy webu *nejsou* vložena do mezipaměti dat.

Metoda `BuildSiteMap` se dokončí vrácením kořenového uzlu mapy webu.

Zbývající metody jsou poměrně jasné. `GetRootNodeCore` zodpovídá za vrácení kořenového uzlu. Vzhledem k tomu, že `BuildSiteMap` vrací kořen, `GetRootNodeCore` jednoduše vrátí návratovou hodnotu `BuildSiteMap` s. Metoda `OnSiteMapChanged` nastaví `root` zpět na `Nothing` při odebrání položky mezipaměti. Když se kořenová sada vrátí zpátky na `Nothing`, při příštím `BuildSiteMap` se znovu vytvoří struktura mapy webu. Nakonec vlastnost `CachedDate` vrátí hodnotu data a času uloženou v mezipaměti dat, pokud taková hodnota existuje. Tuto vlastnost může vývojář stránky použít k určení, kdy byla data mapy webu naposledy uložena do mezipaměti.

## <a name="step-7-registering-thenorthwindsitemapprovider"></a>Krok 7: registrace`NorthwindSiteMapProvider`

Aby naše webová aplikace používala poskytovatele `NorthwindSiteMapProvider` lokality vytvořeného v kroku 6, musíme ho zaregistrovat v `<siteMap>` části `Web.config`. Konkrétně přidejte následující značku do prvku `<system.web>` v `Web.config`:

[!code-xml[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample7.xml)]

Tento kód obsahuje dvě věci: nejdřív indikuje, že je předdefinovaná `AspNetXmlSiteMapProvider` výchozím poskytovatelem mapy webu. za druhé zaregistruje vlastního poskytovatele mapy webu vytvořeného v kroku 6 s popisným názvem Northwind.

> [!NOTE]
> Pro poskytovatele mapy webu nacházející se ve složce `App_Code` aplikací je hodnota atributu `type` jednoduše název třídy. Alternativně může být vlastní poskytovatel mapy webu vytvořen v samostatném projektu knihovny tříd se sestavením, které je umístěno v adresáři `/Bin` webové aplikace. V takovém případě by hodnota atributu `type` mohla být *obor názvů*. *ClassName*, *AssemblyName* .

Po aktualizaci `Web.config`chvíli počkejte, než se zobrazí všechny stránky z kurzů v prohlížeči. Všimněte si, že navigační rozhraní na levé straně stále zobrazuje oddíly a kurzy definované v `Web.sitemap`. Důvodem je to, že `AspNetXmlSiteMapProvider` jako výchozí poskytovatel jsme opustili. Aby bylo možné vytvořit prvek uživatelského rozhraní navigace, který používá `NorthwindSiteMapProvider`, je nutné explicitně určit, že má být použit poskytovatel mapy webu Northwind. V kroku 8 si ukážeme, jak to provést.

## <a name="step-8-displaying-site-map-information-using-the-custom-site-map-provider"></a>Krok 8: zobrazení informací o mapě webu pomocí vlastního poskytovatele mapy webu

Pomocí vlastního poskytovatele mapy webu vytvořeného a registrovaného v `Web.config`jsme připraveni přidat navigační ovládací prvky do `Default.aspx`, `ProductsByCategory.aspx`a `ProductDetails.aspx` stránek do složky `SiteMapProvider`. Začněte otevřením stránky `Default.aspx` a přetažením `SiteMapPath` z panelu nástrojů do návrháře. Ovládací prvek SiteMapPath je umístěn v navigační oblasti sady nástrojů.

[![přidat SiteMapPath do default. aspx](building-a-custom-database-driven-site-map-provider-vb/_static/image19.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image18.gif)

**Obrázek 16**: Přidání akce SiteMapPath do `Default.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](building-a-custom-database-driven-site-map-provider-vb/_static/image20.gif))

Ovládací prvek SiteMapPath zobrazí popis cesty, který označuje aktuální umístění stránky v mapě webu. Do horní části stránky předlohy jsme přidali zpět na *stránkách předlohy a* v kurzu navigace na webu.

Chvíli počkejte, než tuto stránku zobrazíte v prohlížeči. Hodnota SiteMapPath přidaná na obrázku 16 používá výchozího poskytovatele mapy webu, který získává data z `Web.sitemap`. Popis cesty proto zobrazuje domovskou &gt; přizpůsobení mapy webu, stejně jako navigace v pravém horním rohu.

[![popis cesty používá výchozího poskytovatele mapy webu](building-a-custom-database-driven-site-map-provider-vb/_static/image22.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image21.gif)

**Obrázek 17**: navigace s popisem cesty používá výchozího poskytovatele mapy webu ([kliknutím zobrazíte obrázek v plné velikosti).](building-a-custom-database-driven-site-map-provider-vb/_static/image23.gif)

Chcete-li přidat SiteMapPath na obrázku 16 použijte vlastního poskytovatele mapy webu, který jsme vytvořili v kroku 6, nastavte jeho [vlastnost`SiteMapProvider`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemappath.sitemapprovider.aspx) na Northwind, název, který jsme přiřadili `NorthwindSiteMapProvider` v `Web.config`. Návrhář bohužel nadále používá výchozího poskytovatele mapy webu, ale pokud po provedení této změny této vlastnosti navštívíte stránku pomocí prohlížeče, uvidíte, že popis cesty teď používá vlastního poskytovatele mapy webu.

[![popis cesty teď používá vlastního poskytovatele mapy webu NorthwindSiteMapProvider](building-a-custom-database-driven-site-map-provider-vb/_static/image25.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image24.gif)

**Obrázek 18**: navigace s popisem cesty nyní používá vlastního poskytovatele mapy webu `NorthwindSiteMapProvider` ([kliknutím zobrazíte obrázek v plné velikosti](building-a-custom-database-driven-site-map-provider-vb/_static/image26.gif))

Ovládací prvek SiteMapPath zobrazuje více funkčních uživatelských rozhraní na `ProductsByCategory.aspx` a `ProductDetails.aspx` stránkách. Přidejte na tyto stránky SiteMapPath a nastavte vlastnost `SiteMapProvider` v obou na Northwind. Z `Default.aspx` klikněte na odkaz Zobrazit produkty pro nápoje a pak na odkaz Zobrazit podrobnosti pro pole Chai čaj. Jak ukazuje obrázek 19, popis cesty obsahuje oddíl aktuální mapy webu (Chai čaj) a jeho předchůdce: nápoje a všechny kategorie.

[![popis cesty teď používá vlastního poskytovatele mapy webu NorthwindSiteMapProvider](building-a-custom-database-driven-site-map-provider-vb/_static/image27.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image21.png)

**Obrázek 19**: navigace s popisem cesty nyní používá vlastního poskytovatele mapy webu `NorthwindSiteMapProvider` ([kliknutím zobrazíte obrázek v plné velikosti](building-a-custom-database-driven-site-map-provider-vb/_static/image22.png))

Jiné prvky uživatelského rozhraní navigace lze použít kromě prvku SiteMapPath, jako je například nabídka a ovládací prvky TreeView. Stránky `Default.aspx`, `ProductsByCategory.aspx`a `ProductDetails.aspx` ve stažení pro tento kurz, například všechny ovládací prvky nabídky zahrnutí (viz obrázek 20). Podrobnější pohled na navigační ovládací prvky a systém mapy webu v ASP.NET 2,0 najdete v tématu [prozkoumání funkcí navigace na webu ASP.NET 2,0 s](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx) a v části [použití ovládacích prvků navigace na webu](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/navigation/sitenavcontrols.aspx) v [rychlém startu ASP.NET 2,0](https://quickstarts.asp.net/QuickStartv20/aspnet/) .

[![ovládacího prvku nabídky obsahuje všechny kategorie a produkty.](building-a-custom-database-driven-site-map-provider-vb/_static/image29.gif)](building-a-custom-database-driven-site-map-provider-vb/_static/image28.gif)

**Obrázek 20**: ovládací prvek nabídky obsahuje seznam všech kategorií a produktů ([kliknutím zobrazíte obrázek v plné velikosti).](building-a-custom-database-driven-site-map-provider-vb/_static/image30.gif)

Jak bylo zmíněno dříve v tomto kurzu, struktura mapy webu je k dispozici programově prostřednictvím `SiteMap` třídy. Následující kód vrátí kořenové `SiteMapNode` výchozího zprostředkovatele:

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample8.vb)]

Vzhledem k tomu, že `AspNetXmlSiteMapProvider` je výchozím poskytovatelem pro naši aplikaci, výše uvedený kód vrátí kořenový uzel definovaný v `Web.sitemap`. Chcete-li odkazovat na jiného poskytovatele mapy webu než na výchozí, použijte vlastnost `SiteMap` třídy s [`Providers`](https://msdn.microsoft.com/library/system.web.sitemap.providers.aspx) , například takto:

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample9.vb)]

Kde *Name* je název vlastního zprostředkovatele mapy webu (Northwind, pro naši webovou aplikaci).

Chcete-li získat přístup ke členu, který je specifický pro poskytovatele mapy webu, použijte `SiteMap.Providers["name"]` k načtení instance poskytovatele a jejich přetypování na příslušný typ. Chcete-li například zobrazit vlastnost `NorthwindSiteMapProvider` s `CachedDate` na stránce ASP.NET, použijte následující kód:

[!code-vb[Main](building-a-custom-database-driven-site-map-provider-vb/samples/sample10.vb)]

> [!NOTE]
> Ujistěte se, že testujete funkci závislosti mezipaměti SQL. Po návštěvě `Default.aspx`, `ProductsByCategory.aspx`a `ProductDetails.aspx` stránky, jděte do jednoho z kurzů v části úpravy, vložení a odstranění a upravte název kategorie nebo produktu. Pak se vraťte na jednu ze stránek ve složce `SiteMapProvider`. Za předpokladu, že se pro mechanismus cyklického dotazování předává dostatek času na změnu podkladové databáze, měla by být mapa lokality aktualizována, aby se zobrazil nový název produktu nebo kategorie.

## <a name="summary"></a>Přehled

Funkce mapy webu ASP.NET 2,0 s obsahuje třídu `SiteMap`, řadu integrovaných webových ovládacích prvků a výchozího poskytovatele mapy webu, který očekává, že informace o mapě webu jsou trvale uložené v souboru XML. Aby bylo možné používat informace o mapě webu z nějakého jiného zdroje, například z databáze, architektury aplikace nebo vzdálené webové služby, musíme vytvořit vlastního poskytovatele mapy webu. To zahrnuje vytvoření třídy, která je přímo nebo nepřímo odvozena z třídy `SiteMapProvider`.

V tomto kurzu jsme zjistili, jak vytvořit vlastního poskytovatele mapy webu, který bude na základě mapy webu na informace o produktu a kategorii odvrácených z architektury aplikace. Náš poskytovatel rozšířil třídu `StaticSiteMapProvider` a vznikla tak vytvoření metody `BuildSiteMap`, která načetla data, vytvořila hierarchii mapy webu a ukládá do mezipaměti výslednou strukturu v proměnné na úrovni třídy. Použili jsme závislost mezipaměti SQL s funkcí zpětného volání k zrušení platnosti struktury uložené v mezipaměti, když se upraví základní `Categories` nebo data `Products`.

Šťastné programování!

## <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Uložení map webů v SQL Server](https://msdn.microsoft.com/msdnmag/issues/05/06/WickedCode/) a [poskytovatele mapy webu SQL, kterého jste čekali na](https://msdn.microsoft.com/msdnmag/issues/06/02/wickedcode/default.aspx)
- [Podívejte se na model poskytovatele ASP.NET 2,0 s.](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx)
- [Sada nástrojů pro poskytovatele](https://msdn.microsoft.com/asp.net/aa336558.aspx)
- [Zkoumání funkcí navigace na webu ASP.NET 2,0 s](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Recenzenti potenciálních zákazníků pro tento kurz byly Dave Gardner, Zack Novák, Teresa Murphy a Bernadette Leigh. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](building-a-custom-database-driven-site-map-provider-cs.md)

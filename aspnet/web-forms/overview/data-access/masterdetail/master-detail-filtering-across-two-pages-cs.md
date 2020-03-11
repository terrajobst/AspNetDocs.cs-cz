---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-cs
title: Filtrování seznamu a podrobností na dvou stránkách (C#) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu implementujeme tento model pomocí prvku GridView k vypsání dodavatelů v databázi. Každý řádek dodavatele v prvku GridView bude obsahovat...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 552d2d50-fe73-4153-9a7f-2b379bec4625
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-across-two-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: ccb3bfa5f215ba6e65b8a10b40041d5c2896c7e3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78529174"
---
# <a name="masterdetail-filtering-across-two-pages-c"></a>Filtrování hlavních záznamů / podrobností na dvou stránkách (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_9_CS.exe) nebo [Stáhnout PDF](master-detail-filtering-across-two-pages-cs/_static/datatutorial09cs1.pdf)

> V tomto kurzu implementujeme tento model pomocí prvku GridView k vypsání dodavatelů v databázi. Každý řádek dodavatele v prvku GridView bude obsahovat odkaz Zobrazit produkty, který po kliknutí umožní uživateli samostatnou stránku se seznamem těchto produktů pro vybraného dodavatele.

## <a name="introduction"></a>Úvod

V předchozích dvou kurzech jsme viděli, jak [Zobrazit hlavní a podrobné sestavy na jediné webové stránce pomocí DropDownList](master-detail-filtering-with-a-dropdownlist-cs.md) k [zobrazení "hlavních" záznamů a ovládacího prvku GridView nebo DetailsView](master-detail-filtering-with-two-dropdownlists-cs.md) pro zobrazení podrobností. Dalším běžným vzorem, který se používá pro sestavy Master/Details, je mít hlavní záznamy na jedné webové stránce a podrobnosti zobrazené na jiném. Web fóra, jako [jsou fóra ASP.NET](https://forums.asp.net/), je skvělým příkladem tohoto vzoru v praxi. Fóra ASP.NET se skládají z nejrůznějších fór Začínáme, webových formulářů, ovládacích prvků prezentace dat a tak dále. Každé fórum se skládá z mnoha vláken a každé vlákno se skládá z řady příspěvků. Na domovské stránce fóra ASP.NET jsou fóra uvedená v seznamu. Kliknutím na fórum se zobrazí stránka `ShowForum.aspx`, která obsahuje seznam vláken pro toto fórum. Podobně kliknutím na vlákno přejdete na `ShowPost.aspx`, které zobrazí příspěvky pro vlákno, na které jste klikli.

V tomto kurzu implementujeme tento model pomocí prvku GridView k vypsání dodavatelů v databázi. Každý řádek dodavatele v prvku GridView bude obsahovat odkaz Zobrazit produkty, který po kliknutí umožní uživateli samostatnou stránku se seznamem těchto produktů pro vybraného dodavatele.

## <a name="step-1-addingsupplierlistmasteraspxandproductsforsupplierdetailsaspxpages-to-thefilteringfolder"></a>Krok 1: Přidání`SupplierListMaster.aspx`a`ProductsForSupplierDetails.aspx`stránek do složky pro`Filtering`

Při definování rozložení stránky v třetím kurzu jsme do složky `BasicReporting`, `Filtering`a `CustomFormatting` přidali řadu počátečních stránek. V tuto chvíli jsme zatím nepřidali úvodní stránku pro tento kurz, a proto je potřeba přidat dvě nové stránky do složky `Filtering`: `SupplierListMaster.aspx` a `ProductsForSupplierDetails.aspx`. `SupplierListMaster.aspx` zobrazí seznam "hlavních" záznamů (dodavatelé), zatímco `ProductsForSupplierDetails.aspx` zobrazí produkty pro vybraného dodavatele.

Při vytváření těchto dvou nových stránek je jisté, že je přidružíte k `Site.master` hlavní stránku.

![Přidejte stránky SupplierListMaster. aspx a ProductsForSupplierDetails. aspx do složky filtrování.](master-detail-filtering-across-two-pages-cs/_static/image1.png)

**Obrázek 1**: přidejte `SupplierListMaster.aspx` a `ProductsForSupplierDetails.aspx` stránky do složky `Filtering`

Při přidávání nových stránek do projektu Nezapomeňte také aktualizovat soubor mapy webu, `Web.sitemap`odpovídajícím způsobem. Pro účely tohoto kurzu jednoduše přidejte stránku `SupplierListMaster.aspx` k mapě webu pomocí následujícího obsahu XML jako podřízeného prvku pro filtrování sestav `<siteMapNode>` elementu:

[!code-xml[Main](master-detail-filtering-across-two-pages-cs/samples/sample1.xml)]

> [!NOTE]
> Proces aktualizace souboru mapy lokality můžete automatizovat při přidávání nových stránek ASP.NET pomocí [makra K mapě webu](http://odetocode.com/Blogs/scott/archive/2005/11/29/2537.aspx)aplikace Visual Studio [. Scott Allen](http://odetocode.com/Blogs/scott/).

## <a name="step-2-displaying-the-supplier-list-insupplierlistmasteraspx"></a>Krok 2: zobrazení seznamu dodavatelů v`SupplierListMaster.aspx`

Při vytváření stránek `SupplierListMaster.aspx` a `ProductsForSupplierDetails.aspx` je dalším krokem vytvoření prvku GridView pro dodavatele v `SupplierListMaster.aspx`. Přidejte prvek GridView na stránku a vytvořte jeho vazby s novým prvkem ObjectDataSource. Tento prvek ObjectDataSource by měl použít metodu `GetSuppliers()` `SuppliersBLL` třídy k vrácení všech dodavatelů.

[![výběr třídy SuppliersBLL](master-detail-filtering-across-two-pages-cs/_static/image3.png)](master-detail-filtering-across-two-pages-cs/_static/image2.png)

**Obrázek 2**: vyberte třídu `SuppliersBLL` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-cs/_static/image4.png)).

[![nakonfigurovat prvek ObjectDataSource pro použití metody getsuppliers ()](master-detail-filtering-across-two-pages-cs/_static/image6.png)](master-detail-filtering-across-two-pages-cs/_static/image5.png)

**Obrázek 3**: Konfigurace prvku ObjectDataSource pro použití metody `GetSuppliers()` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-cs/_static/image7.png))

Musíme zahrnovat odkaz s názvem zobrazení produktů v každém řádku GridView, který po kliknutí převezme uživatele, aby `ProductsForSupplierDetails.aspx` přesměroval do `SupplierID` hodnoty vybraného řádku pomocí řetězce dotazu QueryString. Pokud uživatel například klikne na odkaz Zobrazit produkty pro dodavatele Tokio Traders (s `SupplierID` hodnotou 4), mělo by se mu `ProductsForSupplierDetails.aspx?SupplierID=4`odeslat.

K tomuto účelu přidejte [HyperLinkField](https://msdn.microsoft.com/library/system.web.ui.webcontrols.hyperlinkfield.aspx) do prvku GridView, který přidá hypertextový odkaz na každý řádek prvku GridView. Začněte kliknutím na odkaz Upravit sloupce z inteligentní značky GridView. Dále vyberte HyperLinkField ze seznamu v levém horním rohu a kliknutím na tlačítko Přidat zahrňte HyperLinkField do seznamu polí prvku GridView.

[![přidat HyperLinkField do prvku GridView.](master-detail-filtering-across-two-pages-cs/_static/image9.png)](master-detail-filtering-across-two-pages-cs/_static/image8.png)

**Obrázek 4**: Přidání prvku HyperLinkField do prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-cs/_static/image10.png))

HyperLinkField je možné nakonfigurovat tak, aby používala stejný text nebo hodnoty URL jako odkaz v jednotlivých řádcích prvku GridView nebo tyto hodnoty mohou být základem datových hodnot vázaných na konkrétní řádek. Chcete-li určit statickou hodnotu ve všech řádcích, použijte vlastnosti `Text` nebo `NavigateUrl` HyperLinkField. Vzhledem k tomu, že chceme, aby byl text odkazu stejný pro všechny řádky, nastavte vlastnost `Text` HyperLinkField na Zobrazit produkty.

[![pro zobrazení produktů nastavit vlastnost text HyperLinkField](master-detail-filtering-across-two-pages-cs/_static/image12.png)](master-detail-filtering-across-two-pages-cs/_static/image11.png)

**Obrázek 5**: nastavte vlastnost `Text` HyperLinkField na zobrazení produktů ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-cs/_static/image13.png)).

Chcete-li nastavit hodnoty textu nebo adresy URL na základě podkladových dat vázaných na řádek prvku GridView, určete datová pole, která mají být z vlastností text nebo URL načítána ve vlastnostech `DataTextField` nebo `DataNavigateUrlFields`. `DataTextField` lze nastavit pouze na jedno datové pole; `DataNavigateUrlFields`však lze nastavit na seznam datových polí oddělených čárkami. Často je potřeba založit text nebo adresu URL na kombinaci hodnoty datového pole aktuálního řádku a některých statických značek. V tomto kurzu například chceme, aby adresa URL odkazů HyperLinkField byla `ProductsForSupplierDetails.aspx?SupplierID=supplierID`a, kde *`supplierID`* je hodnota `SupplierID` row's jednotlivých prvků prvku GridView. Všimněte si, že na tomto místě potřebujeme jak statické, tak datově řízené hodnoty: `ProductsForSupplierDetails.aspx?SupplierID=` část adresy URL odkazu je statická, zatímco *`supplierID`* část je řízená daty jako její hodnota je vlastní `SupplierID` hodnota každého řádku.

Chcete-li označit kombinaci statických a dat řízených hodnot, použijte vlastnosti `DataTextFormatString` a `DataNavigateUrlFormatString`. V těchto vlastnostech zadejte statické značky podle potřeby a pak použijte značku `{0}`, kde chcete zobrazit hodnotu pole zadaného ve vlastnostech `DataTextField` nebo `DataNavigateUrlFields`. Pokud má vlastnost `DataNavigateUrlFields` použít více polí, `{0}` kde má být první hodnota pole vložená, `{1}` pro druhou hodnotu pole atd.

V našem kurzu musíme nastavit vlastnost `DataNavigateUrlFields` na `SupplierID`, protože se jedná o datové pole, jehož hodnota potřebujeme přizpůsobit pro jednotlivé řádky a vlastnost `DataNavigateUrlFormatString` na `ProductsForSupplierDetails.aspx?SupplierID={0}`.

[![nakonfigurovat HyperLinkField tak, aby zahrnoval správnou adresu URL odkazu na základě ČísloDodavatele](master-detail-filtering-across-two-pages-cs/_static/image15.png)](master-detail-filtering-across-two-pages-cs/_static/image14.png)

**Obrázek 6**: Nakonfigurujte HyperLinkField tak, aby zahrnoval správnou adresu URL odkazu na základě `SupplierID` ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-across-two-pages-cs/_static/image16.png)

Po přidání HyperLinkField Nebojte se přizpůsobit a změnit pořadí polí prvku GridView. Následující kód ukazuje prvek GridView po provedení některých menších úprav na úrovni pole.

[!code-aspx[Main](master-detail-filtering-across-two-pages-cs/samples/sample2.aspx)]

Chvíli si prohlédněte stránku `SupplierListMaster.aspx` přes prohlížeč. Jak ukazuje obrázek 7, stránka aktuálně obsahuje seznam všech dodavatelů včetně odkazu zobrazit produkty. Kliknutím na odkaz Zobrazit produkty přejdete na `ProductsForSupplierDetails.aspx`a předáte `SupplierID` dodavatele v řetězci QueryString.

[![každý řádek dodavatele obsahuje odkaz Zobrazit produkty](master-detail-filtering-across-two-pages-cs/_static/image18.png)](master-detail-filtering-across-two-pages-cs/_static/image17.png)

**Obrázek 7**: každý řádek dodavatele obsahuje odkaz na zobrazení produktů ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-cs/_static/image19.png)).

## <a name="step-3-listing-the-suppliers-products-inproductsforsupplierdetailsaspx"></a>Krok 3: výpis produktů dodavatele v`ProductsForSupplierDetails.aspx`

V tomto okamžiku `SupplierListMaster.aspx` stránka posílá uživatele do `ProductsForSupplierDetails.aspx`a předá `SupplierID` vybraného dodavatele do řetězce dotazu. Posledním krokem kurzu je zobrazit produkty v prvku GridView v `ProductsForSupplierDetails.aspx`, jejichž `SupplierID` se rovná `SupplierID` předanému pomocí řetězce dotazu. Chcete-li dosáhnout tohoto začátku přidáním prvku GridView do stránky `ProductsForSupplierDetails.aspx`, pomocí nového ovládacího prvku ObjectDataSource s názvem `ProductsBySupplierDataSource`, který vyvolá metodu `GetProductsBySupplierID(supplierID)` z třídy `ProductsBLL`.

[![přidat nový prvek ObjectDataSource s názvem ProductsBySupplierDataSource](master-detail-filtering-across-two-pages-cs/_static/image21.png)](master-detail-filtering-across-two-pages-cs/_static/image20.png)

**Obrázek 8**: Přidání nového prvku ObjectDataSource s názvem `ProductsBySupplierDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-cs/_static/image22.png))

[![výběr třídy ProductsBLL](master-detail-filtering-across-two-pages-cs/_static/image24.png)](master-detail-filtering-across-two-pages-cs/_static/image23.png)

**Obrázek 9**: vyberte třídu `ProductsBLL` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-cs/_static/image25.png)).

[![má prvek ObjectDataSource vyvolat metodu GetProductsBySupplierID (KódDodavatele)](master-detail-filtering-across-two-pages-cs/_static/image27.png)](master-detail-filtering-across-two-pages-cs/_static/image26.png)

**Obrázek 10**: prvek ObjectDataSource vyvolá metodu `GetProductsBySupplierID(supplierID)` ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-across-two-pages-cs/_static/image28.png)

Poslední krok průvodce konfigurací zdroje dat vás požádá o zadání zdroje *`supplierID`* parametru `GetProductsBySupplierID(supplierID)` metody. Chcete-li použít hodnotu QueryString, nastavte zdroj parametru na hodnotu QueryString a zadejte název hodnoty řetězce dotazu, který chcete použít v textovém poli vlastnost QueryStringField (`SupplierID`).

[![naplnit hodnotu parametru KódDodavatele z hodnoty QueryString řetězce KódDodavatele](master-detail-filtering-across-two-pages-cs/_static/image30.png)](master-detail-filtering-across-two-pages-cs/_static/image29.png)

**Obrázek 11**: naplnění hodnoty parametru *`supplierID`* z hodnoty řetězce dotazu `SupplierID` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-cs/_static/image31.png))

A je to! Obrázek 12: po návštěvě se zobrazí stránka `ProductsForSupplierDetails.aspx` kliknutím na odkaz Tokio Traders z `SupplierListMaster.aspx`.

[Zobrazuje se ![produktů poskytovaných pomocí Brna Traders.](master-detail-filtering-across-two-pages-cs/_static/image33.png)](master-detail-filtering-across-two-pages-cs/_static/image32.png)

**Obrázek 12**: zobrazí se produkty dodávané pomocí Brna Traders ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-across-two-pages-cs/_static/image34.png)

## <a name="displaying-supplier-information-inproductsforsupplierdetailsaspx"></a>Zobrazení informací o dodavateli v`ProductsForSupplierDetails.aspx`

Jak ukazuje obrázek 12, stránka `ProductsForSupplierDetails.aspx` jednoduše zobrazí seznam produktů, které jsou dodány `SupplierID` určeném v řetězci QueryString. Někdo odeslaný přímo na tuto stránku ale neví, že na obrázku 12 se zobrazuje produkty z Brna Traders. Aby bylo možné tento problém vyřešit, můžeme na této stránce zobrazit také informace o dodavateli.

Začněte přidáním třídy FormView nad ovládací prvek prvků pro produkty. Vytvořte nový ovládací prvek ObjectDataSource s názvem `SuppliersDataSource`, který vyvolá metodu `GetSupplierBySupplierID(supplierID)` `SuppliersBLL` třídy.

[![výběr třídy SuppliersBLL](master-detail-filtering-across-two-pages-cs/_static/image36.png)](master-detail-filtering-across-two-pages-cs/_static/image35.png)

**Obrázek 13**: vyberte třídu `SuppliersBLL` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-cs/_static/image37.png)).

[![má prvek ObjectDataSource vyvolat metodu GetSupplierBySupplierID (KódDodavatele)](master-detail-filtering-across-two-pages-cs/_static/image39.png)](master-detail-filtering-across-two-pages-cs/_static/image38.png)

**Obrázek 14**: Chcete-li, aby prvek ObjectDataSource vyvolal metodu `GetSupplierBySupplierID(supplierID)` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-cs/_static/image40.png))

Stejně jako u `ProductsBySupplierDataSource`mají *`supplierID`* parametr přiřazenou hodnotu `SupplierID` hodnota QueryString.

[![naplnit hodnotu parametru KódDodavatele z hodnoty QueryString řetězce KódDodavatele](master-detail-filtering-across-two-pages-cs/_static/image42.png)](master-detail-filtering-across-two-pages-cs/_static/image41.png)

**Obrázek 15**: naplňte hodnotu parametru *`supplierID`* z hodnoty řetězce dotazu `SupplierID` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-cs/_static/image43.png)).

Při vázání třídy FormView na prvek ObjectDataSource v zobrazení Návrh aplikace Visual Studio automaticky vytvoří `ItemTemplate`, `InsertItemTemplate`a `EditItemTemplate` ve třídě FormView ovládací prvky Label a TextBox pro každé z datových polí vrácených prvkem ObjectDataSource. Vzhledem k tomu, že chceme pouze zobrazit informace o dodavateli, odebrat `InsertItemTemplate` a `EditItemTemplate`. V dalším kroku upravte ItemTemplate tak, aby se zobrazil název společnosti dodavatele v prvku `<h3>` a adresa, město, země a telefonní číslo pod názvem společnosti. Alternativně můžete ručně nastavit `DataSourceID` třídy FormView a vytvořit `ItemTemplate` značky, jak jsme byli zpátky v kurzu[zobrazení dat s prvkem ObjectDataSource](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md).

Po úpravách deklarativních značek třídy FormView by měl vypadat nějak takto:

[!code-aspx[Main](master-detail-filtering-across-two-pages-cs/samples/sample3.aspx)]

Obrázek 16 ukazuje snímek obrazovky `ProductsForSupplierDetails.aspx` stránky po zahrnutí informací o dodavateli.

[![seznam produktů obsahuje souhrnné informace o dodavateli.](master-detail-filtering-across-two-pages-cs/_static/image45.png)](master-detail-filtering-across-two-pages-cs/_static/image44.png)

**Obrázek 16**: seznam produktů obsahuje souhrnné informace o dodavateli ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-cs/_static/image46.png)).

## <a name="applying-the-final-touches-for-theproductsforsupplierdetailsaspxui"></a>Použití konečných vylepšení`ProductsForSupplierDetails.aspx`uživatelského rozhraní

Pokud chcete zlepšit uživatelské prostředí pro tuto sestavu, měli byste na `ProductsForSupplierDetails.aspx` stránku udělat několik dodatků. V současné době může uživatel přejít ze stránky `ProductsForSupplierDetails.aspx` zpět na seznam dodavatelů, a to tak, že klikne na tlačítko zpět v prohlížeči. Přidáváme ovládací prvek hypertextový odkaz na stránku `ProductsForSupplierDetails.aspx`, která odkazuje zpět na `SupplierListMaster.aspx`, a poskytuje tak jiný způsob, jak se uživatel vrátí do hlavního seznamu.

[![přidání ovládacího prvku hypertextový odkaz, který uživateli převezme zpátky do SupplierListMaster. aspx](master-detail-filtering-across-two-pages-cs/_static/image48.png)](master-detail-filtering-across-two-pages-cs/_static/image47.png)

**Obrázek 17**: Přidání ovládacího prvku hypertextový odkaz pro převzetí uživatele zpět do `SupplierListMaster.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-across-two-pages-cs/_static/image49.png))

Pokud uživatel klikne na odkaz Zobrazit produkty pro dodavatele, který nemá žádné produkty, `ProductsBySupplierDataSource` prvek ObjectDataSource v `ProductsForSupplierDetails.aspx` nevrátí žádné výsledky. Ovládací prvek GridView vázaný na prvek ObjectDataSource nevytiskne žádný kód, který je v prohlížeči uživatele v prázdné oblasti na stránce. Aby bylo možné uživatele s vybraným dodavatelem lépe informovat, můžeme nastavit vlastnost `EmptyDataText` prvku GridView na zprávu, kterou chcete zobrazit, pokud taková situace nastane. Tato vlastnost jsem nastavila na hodnotu neexistují žádné produkty od tohoto dodavatele.

Ve výchozím nastavení poskytují všichni dodavatelé v databázi Northwind alespoň jeden produkt. V tomto kurzu jsme ale ručně změnili `Products`ovou tabulku tak, že dodavatel Escargots Nouveaux už není přidružený k žádným produktům. Po provedení této změny se na obrázku 18 zobrazí stránka s podrobnostmi pro Escargots Nouveaux.

[![uživatelé jsou informováni o tom, že dodavatel neposkytuje žádné produkty.](master-detail-filtering-across-two-pages-cs/_static/image51.png)](master-detail-filtering-across-two-pages-cs/_static/image50.png)

**Obrázek 18**: uživatelům se dozvíte, že dodavatel neposkytuje žádné produkty ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-across-two-pages-cs/_static/image52.png)

## <a name="summary"></a>Souhrn

I když se v sestavách a podrobností můžou zobrazovat hlavní a podrobné záznamy na jedné stránce, na mnoha webech, které jsou oddělené na dvou webových stránkách. V tomto kurzu jsme se podívali na to, jak implementovat takovou sestavu hlavní/podrobnosti, která má dodavatele uvedené v prvku GridView v hlavní webové stránce a v přidružených produktech uvedených na stránce podrobností. Každý řádek dodavatele na hlavní webové stránce obsahoval odkaz na stránku s podrobnostmi, která byla předána po `SupplierID` hodnotě řádku. Tyto odkazy na konkrétní řádek lze snadno přidat pomocí HyperLinkField prvku GridView.

Na stránce podrobností načítající tyto produkty pro zadaného dodavatele bylo provedeno vyvoláním metody `GetProductsBySupplierID(supplierID)` `ProductsBLL` třídy. Hodnota parametru *`supplierID`* byla určena deklarativně pomocí řetězce dotazu jako zdroje parametru. Zjistili jsme také, jak zobrazit podrobnosti o dodavatelích na stránce podrobností pomocí FormView.

Náš [Další kurz](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) je konečným řešením pro hlavní a podrobné sestavy. Podíváme se na to, jak zobrazit seznam produktů v prvku GridView, kde každý řádek obsahuje tlačítko pro výběr. Po kliknutí na tlačítko vybrat se zobrazí podrobnosti o tomto produktu v ovládacím prvku DetailsView na stejné stránce.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Hilton Giesenow. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](master-detail-filtering-with-two-dropdownlists-cs.md)
> [Další](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)

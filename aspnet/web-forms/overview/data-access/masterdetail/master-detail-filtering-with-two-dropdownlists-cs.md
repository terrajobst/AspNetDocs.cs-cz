---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-cs
title: Filtrování hlavního/podrobného filtru se dvěma DropDownListC#() | Microsoft Docs
author: rick-anderson
description: Tento kurz rozbalí vztah hlavní/podrobnosti a přidá třetí vrstvu pomocí dvou ovládacích prvků DropDownList pro výběr požadované nadřazené položky a Recor...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: ac4b0d77-4816-4ded-afd0-88dab667aedd
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-two-dropdownlists-cs
msc.type: authoredcontent
ms.openlocfilehash: e24b7f91d34fbce1676f7f28ebb7d23903157f7f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78528488"
---
# <a name="masterdetail-filtering-with-two-dropdownlists-c"></a>Filtrování hlavních záznamů / podrobností dvou ovládacích prvků DropDownList (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_8_CS.exe) nebo [Stáhnout PDF](master-detail-filtering-with-two-dropdownlists-cs/_static/datatutorial08cs1.pdf)

> Tento kurz rozšiřuje hlavní a podrobný vztah a přidá třetí vrstvu pomocí dvou ovládacích prvků DropDownList k výběru požadovaných nadřazených záznamů a.

## <a name="introduction"></a>Úvod

V [předchozím kurzu](master-detail-filtering-with-a-dropdownlist-cs.md) jsme prozkoumali, jak zobrazit jednoduchou sestavu hlavní/podrobnosti pomocí jednoho prvku DropDownList naplněný pomocí kategorií a prvku GridView zobrazujícího tyto produkty, které patří do vybrané kategorie. Tento model sestavy funguje dobře při zobrazení záznamů, které mají relaci 1:1, a lze ji snadno rozšířit tak, aby fungovala v případě scénářů, které zahrnují více vztahů 1: n. Například systém záznamu objednávky by měl mít tabulky, které odpovídají zákazníkům, objednávkám a položkám řádků objednávky. Daný zákazník může mít více objednávek s jednotlivými objednávkami, které se skládají z několika položek. Taková data mohou být prezentována uživateli se dvěma DropDownList a GridView. První ovládací prvek DropDownList by měl položku seznamu pro každého zákazníka v databázi s obsahem druhé položky, který se nachází v objednávkách vybraných zákazníkem. Prvek GridView bude vypisovat položky řádku z vybraného pořadí.

I když databáze Northwind obsahuje informace o podrobnostech o zákaznících/objednávkách nebo objednávkách v tabulkách `Customers`, `Orders`a `Order Details`, nejsou tyto tabulky zachyceny v naší architektuře. Přesto můžeme i nadále ilustrovat použití dvou závislých ovládacích prvků DropDownList. První DropDownList zobrazí seznam kategorií a druhých produktů, které patří do vybrané kategorie. Prvek DetailsView pak zobrazí podrobnosti o vybraném produktu.

## <a name="step-1-creating-and-populating-the-categories-dropdownlist"></a>Krok 1: vytvoření a naplnění kategorie DropDownList

Naším prvním cílem je přidat DropDownList, který obsahuje seznam kategorií. Tyto kroky byly podrobně prověřeny v předchozím kurzu, ale jsou zde shrnuty pro úplnost.

Otevřete stránku `MasterDetailsDetails.aspx` ve složce `Filtering`, přidejte na ni objekt DropDownList, nastavte jeho vlastnost `ID` na `Categories`a potom klikněte na odkaz konfigurace zdroje dat v jeho inteligentní značce. V Průvodci konfigurací zdroje dat vyberte možnost Přidat nový zdroj dat.

[![přidat nový zdroj dat pro DropDownList](master-detail-filtering-with-two-dropdownlists-cs/_static/image2.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image1.png)

**Obrázek 1**: Přidání nového zdroje dat pro DropDownList ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-two-dropdownlists-cs/_static/image3.png))

Nový zdroj dat by měl být přirozeně prvkem ObjectDataSource. Pojmenujte tuto novou `CategoriesDataSource` ObjectDataSource a vyvolejte metodu `GetCategories()` `CategoriesBLL` objektu.

[![zvolit použití třídy CategoriesBLL](master-detail-filtering-with-two-dropdownlists-cs/_static/image5.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image4.png)

**Obrázek 2**: vyberte, pokud chcete použít třídu `CategoriesBLL` ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-with-two-dropdownlists-cs/_static/image6.png)

[![nakonfigurovat prvek ObjectDataSource pro použití metody GetCategories ()](master-detail-filtering-with-two-dropdownlists-cs/_static/image8.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image7.png)

**Obrázek 3**: Konfigurace prvku ObjectDataSource pro použití metody `GetCategories()` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-two-dropdownlists-cs/_static/image9.png))

Po nakonfigurování prvku ObjectDataSource je stále potřeba určit, které pole zdroje dat by se mělo zobrazit v `Categories` DropDownList a které z nich má být nakonfigurováno jako hodnota pro položku seznamu. Nastavte pole `CategoryName` jako hodnotu zobrazení a `CategoryID` jako hodnotu pro každou položku seznamu.

[![mají DropDownList zobrazit pole CategoryName a jako hodnotu použít CategoryID.](master-detail-filtering-with-two-dropdownlists-cs/_static/image11.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image10.png)

**Obrázek 4**: zobrazení pole `CategoryName` a použití `CategoryID` jako hodnoty ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-two-dropdownlists-cs/_static/image12.png)).

V tuto chvíli máme ovládací prvek DropDownList (`Categories`), který je naplněný záznamy z tabulky `Categories`. Když uživatel zvolí z DropDownList novou kategorii, chceme, aby se provedl postback, aby se aktualizovala vlastnost DropDownList produktu, kterou vytvoříme v kroku 2. Proto zaškrtněte možnost Povolit AutoPostBack z inteligentní značky `categories` DropDownList.

[![povolit AutoPostBack pro kategorie DropDownList](master-detail-filtering-with-two-dropdownlists-cs/_static/image14.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image13.png)

**Obrázek 5**: povolení automatického zpětného odeslání pro `Categories` DropDownList ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-two-dropdownlists-cs/_static/image15.png))

## <a name="step-2-displaying-the-selected-categorys-products-in-a-second-dropdownlist"></a>Krok 2: zobrazení produktů vybrané kategorie v druhém DropDownList

Po dokončení `Categories` DropDownList je dalším krokem zobrazení DropDownList produktů patřících do vybrané kategorie. Chcete-li to provést, přidejte do stránky s názvem `ProductsByCategory`další DropDownList. Stejně jako u `Categories` DropDownList vytvořte nový prvek ObjectDataSource pro `ProductsByCategory` DropDownList s názvem `ProductsByCategoryDataSource`.

[![přidat nový zdroj dat pro ProductsByCategory DropDownList](master-detail-filtering-with-two-dropdownlists-cs/_static/image17.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image16.png)

**Obrázek 6**: Přidání nového zdroje dat pro `ProductsByCategory` DropDownList ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-two-dropdownlists-cs/_static/image18.png))

[![vytvořit nový prvek ObjectDataSource s názvem ProductsByCategoryDataSource](master-detail-filtering-with-two-dropdownlists-cs/_static/image20.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image19.png)

**Obrázek 7**: vytvoření nového prvku ObjectDataSource s názvem `ProductsByCategoryDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-two-dropdownlists-cs/_static/image21.png))

Vzhledem k tomu, že `ProductsByCategory` DropDownList potřebuje zobrazit pouze takové produkty patřící do vybrané kategorie, musí prvek ObjectDataSource vyvolat metodu `GetProductsByCategoryID(categoryID)` z objektu `ProductsBLL`.

[![zvolit použití třídy ProductsBLL](master-detail-filtering-with-two-dropdownlists-cs/_static/image23.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image22.png)

**Obrázek 8**: Volba použití třídy `ProductsBLL` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-two-dropdownlists-cs/_static/image24.png))

[![nakonfigurovat prvek ObjectDataSource na použití metody GetProductsByCategoryID (KódKategorie)](master-detail-filtering-with-two-dropdownlists-cs/_static/image26.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image25.png)

**Obrázek 9**: Konfigurace prvku ObjectDataSource pro použití metody `GetProductsByCategoryID(categoryID)` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-two-dropdownlists-cs/_static/image27.png))

V posledním kroku průvodce musíme zadat hodnotu parametru *`categoryID`* . Přiřaďte tento parametr vybrané položce z `Categories` DropDownList.

[![načíst hodnotu parametru KódKategorie z kategorií DropDownList](master-detail-filtering-with-two-dropdownlists-cs/_static/image29.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image28.png)

**Obrázek 10**: vyžádání hodnoty parametru *`categoryID`* z `Categories` DropDownList ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-two-dropdownlists-cs/_static/image30.png))

Po nakonfigurovaném prvku ObjectDataSource je vše ponecháno pro určení, která pole zdroje dat jsou použita pro zobrazení a hodnotu položek ovládacího prvku DropDownList. Zobrazte pole `ProductName` a jako hodnotu použijte pole `ProductID`.

[![zadejte pole zdroje dat, která se použijí pro vlastnosti text a hodnota ovládacího prvku ListItems.](master-detail-filtering-with-two-dropdownlists-cs/_static/image32.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image31.png)

**Obrázek 11**: Určete pole zdroje dat, která se používají pro vlastnosti `ListItem` s a `Value` ovládacího prvku pro `Text` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-two-dropdownlists-cs/_static/image33.png)).

Pomocí ovládacího prvku ObjectDataSource a `ProductsByCategory` DropDownList nakonfigurovaného na naší stránce se zobrazí dvě DropDownList: první zobrazí seznam všech kategorií, zatímco druhá bude obsahovat tyto produkty patřící do vybrané kategorie. Když uživatel vybere novou kategorii z prvního DropDownList, postback se následovat a druhý objekt DropDownList se znovu sváže a zobrazí se tyto produkty, které patří do nově vybrané kategorie. Obrázky 12 a 13 ukazují `MasterDetailsDetails.aspx` v akci při prohlížení v prohlížeči.

[![při první návštěvě stránky se vybere kategorie nápoje.](master-detail-filtering-with-two-dropdownlists-cs/_static/image35.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image34.png)

**Obrázek 12**: když poprvé navštívíte stránku, vybere se kategorie nápoje ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-with-two-dropdownlists-cs/_static/image36.png)

[![výběru jiné kategorie zobrazí produkty nové kategorie.](master-detail-filtering-with-two-dropdownlists-cs/_static/image38.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image37.png)

**Obrázek 13**: volba jiné kategorie zobrazuje produkty nové kategorie ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-with-two-dropdownlists-cs/_static/image39.png)

V současné době `productsByCategory` DropDownList při změně *nezpůsobí* postback. Budeme ale chtít, aby po přidání ovládacího prvku DetailsView k zobrazení podrobností vybraného produktu (krok 3) bylo provedeno zpětné odeslání. Proto zaškrtněte políčko Povolit automatické odeslání z inteligentní značky `productsByCategory` DropDownList.

[![povolit funkci automatického odeslání pro productsByCategory DropDownList](master-detail-filtering-with-two-dropdownlists-cs/_static/image41.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image40.png)

**Obrázek 14**: povolení funkce AutoPostBack pro `productsByCategory` DropDownList ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-two-dropdownlists-cs/_static/image42.png))

## <a name="step-3-using-a-detailsview-to-display-details-for-the-selected-product"></a>Krok 3: použití ovládacího prvku DetailsView k zobrazení podrobností pro vybraný produkt

Posledním krokem je zobrazit podrobnosti o vybraném produktu v ovládacím prvku DetailsView. Chcete-li to provést, přidejte prvek DetailsView na stránku, nastavte jeho vlastnost `ID` na `ProductDetails`a vytvořte pro něj nový prvek ObjectDataSource. Nakonfigurujte tento prvek ObjectDataSource tak, aby načetl data z metody `GetProductByProductID(productID)` `ProductsBLL` třídy pomocí vybrané hodnoty `ProductsByCategory` DropDownList pro hodnotu parametru *`productID`* .

[![zvolit použití třídy ProductsBLL](master-detail-filtering-with-two-dropdownlists-cs/_static/image44.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image43.png)

**Obrázek 15**: vyberte, pokud chcete použít třídu `ProductsBLL` ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-with-two-dropdownlists-cs/_static/image45.png)

[![nakonfigurovat prvek ObjectDataSource na použití metody GetProductByProductID (productID)](master-detail-filtering-with-two-dropdownlists-cs/_static/image47.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image46.png)

**Obrázek 16**: Konfigurace prvku ObjectDataSource pro použití metody `GetProductByProductID(productID)` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-two-dropdownlists-cs/_static/image48.png))

[![načíst hodnotu parametru productID z ProductsByCategory DropDownList](master-detail-filtering-with-two-dropdownlists-cs/_static/image50.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image49.png)

**Obrázek 17**: vyžádání hodnoty parametru *`productID`* z `ProductsByCategory` DropDownList ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-two-dropdownlists-cs/_static/image51.png))

Můžete zvolit zobrazení libovolného z dostupných polí v ovládacím prvku DetailsView. Rozhodli jste se odebrat pole `ProductID`, `SupplierID`a `CategoryID` a změnit jejich pořadí a formátování zbývajících polí. Kromě toho jsem vymazal vlastnosti `Height` a `Width` ovládacího prvku DetailsView, což umožňuje, aby se ovládací prvek DetailsView rozšířil na šířku potřebnou k tomu, aby se co nejlépe zobrazovala data, místo omezení na zadanou velikost. Zobrazí se úplné označení níže:

[!code-aspx[Main](master-detail-filtering-with-two-dropdownlists-cs/samples/sample1.aspx)]

Chvíli si vyzkoušíte `MasterDetailsDetails.aspx` stránku v prohlížeči. Na první pohled se může zdát, že vše funguje podle potřeby, ale je to drobný problém. Když zvolíte novou kategorii, `ProductsByCategory` DropDownList se aktualizuje tak, aby obsahovala tyto produkty pro vybranou kategorii, ale v `ProductDetails` DetailsView pokračovala možnost Zobrazit předchozí informace o produktu. Prvek DetailsView je aktualizován při výběru jiného produktu pro vybranou kategorii. Pokud se navíc důkladně otestujete, zjistíte, že pokud průběžně vyberete nové kategorie (například zvolíte nápoje z `Categories` DropDownList, potom se Confections) každý další výběr kategorie způsobí, že se `ProductDetails` prvek DetailsView aktualizuje.

Abychom vám pomohli tento problém konkretizovat, Podívejme se na konkrétní příklad. Při první návštěvě stránky vyberte kategorii nápoje a související produkty se načtou v `ProductsByCategory` DropDownList. Možnost Chai je vybraný produkt a jeho podrobnosti se zobrazí v prvku `ProductDetails` DetailsView, jak je znázorněno na obrázku 18.

[![podrobnosti vybraného produktu se zobrazí v ovládacím prvku DetailsView.](master-detail-filtering-with-two-dropdownlists-cs/_static/image53.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image52.png)

**Obrázek 18**: informace o vybraném produktu se zobrazí v prvku DetailsView ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-two-dropdownlists-cs/_static/image54.png)).

Změníte-li výběr kategorie z nápojů na koření, dojde k postbacku a odpovídajícím způsobem `ProductsByCategory` DropDownList. ovládací prvek DetailsView stále zobrazuje podrobnosti o Chai.

[![se stále zobrazují podrobnosti o dříve vybraném produktu.](master-detail-filtering-with-two-dropdownlists-cs/_static/image56.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image55.png)

**Obrázek 19**: stále se zobrazují podrobnosti o dříve vybraném produktu ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-with-two-dropdownlists-cs/_static/image57.png)

Výběr nového produktu ze seznamu aktualizuje prvek DetailsView podle očekávání. Pokud po změně produktu vyberete novou kategorii, prvek DetailsView se znovu neaktualizuje. Pokud se ale místo výběru nového produktu, který jste vybrali v nové kategorii, aktualizuje prvek DetailsView. Co na světě prochází?

Jedná se o problém s časováním v životním cyklu stránky. Pokaždé, když je vyžádána stránka, pokračuje pomocí několika kroků v průběhu jejího vykreslování. V jednom z těchto kroků ovládací prvky ObjectDataSource kontrolují, aby se zobrazily, zda se změnily některé `SelectParameters` hodnoty. Pokud ano, webové ovládací prvky dat svázané s ovládacím prvkem ObjectDataSource ví, že je potřeba aktualizovat svůj displej. Například když je vybrána nová kategorie, `ProductsByCategoryDataSource` prvek ObjectDataSource zjistí, že došlo ke změně hodnot parametrů, a `ProductsByCategory` DropDownList se znovu sváže a získá produkty pro vybranou kategorii.

Problém, který vzniká v této situaci, je, že bod v životním cyklu stránky, ke kterému se kontroluje změny, nastávají *před změnou* vazby přidružených webových ovládacích prvků dat. Proto při výběru nové kategorie `ProductsByCategoryDataSource` prvek ObjectDataSource zjistí změnu hodnoty jeho parametru. Prvek ObjectDataSource, který je použit ovládacím prvkem `ProductDetails` DetailsView, však tyto změny neprojeví, protože je ještě převázána `ProductsByCategory` DropDownList. Později v životním cyklu se `ProductsByCategory` DropDownList znovu váže ke svému prvku ObjectDataSource a přebírá produkty pro nově vybranou kategorii. I když se změní hodnota `ProductsByCategory` DropDownList, prvek ObjectDataSource prvku `ProductDetails` DetailsView již dokončil kontrolu hodnoty parametru; Proto DetailsView zobrazí předchozí výsledky. Tato interakce je znázorněna na obrázku 20.

[![změny hodnoty DropDownList ovládacího prvku ProductsByCategory poté, co ovládací prvek ObjectDataSource prvku ProductDetails DetailsView vrátí změny](master-detail-filtering-with-two-dropdownlists-cs/_static/image59.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image58.png)

**Obrázek 20**: hodnota `ProductsByCategory` DropDownList se mění po kontrole změn v ovládacím prvku `ProductDetails` DetailsView ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-with-two-dropdownlists-cs/_static/image60.png)

Chcete-li tento problém napravit, je nutné explicitně znovu svázat prvek `ProductDetails` DetailsView poté, co byla vytvořena vazba `ProductsByCategory` DropDownList. To můžeme provést voláním metody `DataBind()` `ProductDetails` DetailsView, když se aktivuje událost `DataBound` `ProductsByCategory` DropDownList. Přidejte následující kód obslužné rutiny události do třídy kódu na pozadí `MasterDetailsDetails.aspx` stránky (viz téma "[programové nastavení hodnot parametru ObjectDataSource](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-cs.md)" pro diskuzi o tom, jak přidat obslužnou rutinu události):

[!code-csharp[Main](master-detail-filtering-with-two-dropdownlists-cs/samples/sample2.cs)]

Po přidání tohoto explicitního volání metody `DataBind()` prvku `ProductDetails` DetailsView se v kurzu pracuje podle očekávání. Obrázek 21 ukazuje, jak tato změna prostala vyřešená předchozí problém.

[![prvku DetailsView ProductDetails se explicitně aktualizuje, když se aktivuje událost DataBound ovládacího prvku ProductsByCategory.](master-detail-filtering-with-two-dropdownlists-cs/_static/image62.png)](master-detail-filtering-with-two-dropdownlists-cs/_static/image61.png)

**Obrázek 21**: `ProductDetails` DetailsView se explicitně aktualizuje, když se aktivuje událost `DataBound` `ProductsByCategory` DropDownList ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-two-dropdownlists-cs/_static/image63.png)).

## <a name="summary"></a>Souhrn

DropDownList slouží jako ideální prvek uživatelského rozhraní pro sestavy hlavních a podrobností, kde existuje vztah 1:1 mezi hlavními a podrobnými záznamy. V předchozím kurzu jsme viděli, jak použít jeden objekt DropDownList k filtrování produktů zobrazených ve vybrané kategorii. V tomto kurzu jsme nahradili prvku GridView v produktech pomocí ovládacího prvku DropDownList a použili prvek DetailsView k zobrazení podrobností o vybraném produktu. Koncepty popsané v tomto kurzu lze snadno rozšířit na datové modely zahrnující více relací 1:1, jako jsou například zákazníci, objednávky a položky objednávek. Obecně platí, že vždy můžete přidat DropDownList pro každou entitu "jedna" v relaci 1: n.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Hilton Giesenow. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](master-detail-filtering-with-a-dropdownlist-cs.md)
> [Další](master-detail-filtering-across-two-pages-cs.md)

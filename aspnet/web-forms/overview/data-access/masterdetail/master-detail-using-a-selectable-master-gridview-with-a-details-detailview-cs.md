---
uid: web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs
title: Hlavní a podrobnosti pomocí selektivního hlavního prvku GridView s podrobnostmi prvku detailview (C#) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu bude mít prvek GridView, jehož řádky obsahují název a cenu každého produktu spolu s tlačítkem vybrat. Klikněte na tlačítko vybrat pro particu...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 0f982827-f8f9-420d-b36b-57b23f5aa519
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs
msc.type: authoredcontent
ms.openlocfilehash: 04c427341f063729bd23b416a96f5acb20702792
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74632490"
---
# <a name="masterdetail-using-a-selectable-master-gridview-with-a-details-detailview-c"></a>Zobrazení hlavních záznamů / podrobností výběrem hlavního záznamu prvkem GridView s podrobnostmi v prvku DetailView (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_10_CS.exe) nebo [Stáhnout PDF](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/datatutorial10cs1.pdf)

> V tomto kurzu bude mít prvek GridView, jehož řádky obsahují název a cenu každého produktu spolu s tlačítkem vybrat. Kliknutí na tlačítko pro výběr konkrétního produktu způsobí, že se jeho úplné podrobnosti zobrazí v ovládacím prvku DetailsView na stejné stránce.

## <a name="introduction"></a>Úvod

V [předchozím kurzu](master-detail-filtering-across-two-pages-cs.md) jsme viděli, jak vytvořit sestavu hlavní a podrobnosti pomocí dvou webových stránek: "hlavní" Webová stránka, ze které jsme zobrazili seznam dodavatelů. a na webové stránce Podrobnosti, která je uvedená v seznamu produktů poskytovaných vybraným dodavatelem. Tento formát sestavy stránky může být zúžený na jednu stránku. V tomto kurzu bude mít prvek GridView, jehož řádky obsahují název a cenu každého produktu spolu s tlačítkem vybrat. Kliknutí na tlačítko pro výběr konkrétního produktu způsobí, že se jeho úplné podrobnosti zobrazí v ovládacím prvku DetailsView na stejné stránce.

[![kliknutí na tlačítko vybrat zobrazí podrobnosti o produktu.](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image2.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image1.png)

**Obrázek 1**: kliknutím na tlačítko vybrat zobrazíte podrobnosti o produktu ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image3.png)

## <a name="step-1-creating-a-selectable-gridview"></a>Krok 1: vytvoření selektivního prvku GridView

Nahlaste se v sestavě Master/Detail na dvou stránkách, kterou každý hlavní záznam obsahuje, a když se na něj klikne, pošle se uživateli na stránku podrobností, která přesměruje na hodnotu `SupplierID` řádku v řetězci dotazu. Takový hypertextový odkaz byl přidán do každého řádku GridView pomocí HyperLinkField. V případě sestavy hlavní stránka/podrobnosti pro jednu stránku budeme potřebovat tlačítko pro každý řádek GridView, který po kliknutí zobrazí podrobnosti. Ovládací prvek GridView lze nakonfigurovat tak, aby zahrnoval tlačítko pro výběr pro každý řádek, který způsobí postback, a označí tento řádek jako [SelectedRow](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedrow.aspx)prvku GridView.

Začněte přidáním ovládacího prvku GridView na stránku `DetailsBySelecting.aspx` ve složce `Filtering` a nastavte jeho vlastnost `ID` na `ProductsGrid`. Dále přidejte nový prvek ObjectDataSource pojmenovaný `AllProductsDataSource`, který vyvolá metodu `GetProducts()` `ProductsBLL` třídy.

[![vytvořit prvek ObjectDataSource s názvem AllProductsDataSource](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image5.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image4.png)

**Obrázek 2**: Vytvoření prvku ObjectDataSource s názvem `AllProductsDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image6.png))

[![použít třídu ProductsBLL](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image8.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image7.png)

**Obrázek 3**: použijte třídu `ProductsBLL` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image9.png)).

[![nakonfigurovat prvek ObjectDataSource pro vyvolání metody GetProducts ()](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image11.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image10.png)

**Obrázek 4**: Konfigurace prvku ObjectDataSource pro vyvolání metody `GetProducts()` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image12.png))

Upravte pole prvku GridView odebráním všech prvků kromě `ProductName` a `UnitPrice` BoundFields. Také si klidně Přizpůsobte tyto BoundFields podle potřeby, jako je například formátování `UnitPrice` vlastnost BoundField jako měny a změna vlastností `HeaderText` BoundFields. Tyto kroky lze provést graficky kliknutím na odkaz Upravit sloupce z inteligentní značky prvku GridView nebo ruční konfigurací deklarativní syntaxe.

[![odebrat všechny kromě BoundFields NázevVýrobku a UnitPrice](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image14.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image13.png)

**Obrázek 5**: Odeberte všechny kromě `ProductName` a `UnitPrice` BoundFields ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image15.png)).

Konečné označení prvku GridView je:

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample1.aspx)]

Dále je nutné označit prvek GridView jako volitelný, čímž přidáte tlačítko pro výběr na každý řádek. K tomuto účelu stačí zaškrtnout políčko Povolit výběr v inteligentní značce prvku GridView.

[![nastavit, že se mají vybrat řádky prvku GridView](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image17.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image16.png)

**Obrázek 6**: umožňuje vybrat řádky prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image18.png)).

Zaškrtnutím možnosti povolit výběr přidáte CommandField do prvku GridView `ProductsGrid` s vlastností `ShowSelectButton` nastavenou na hodnotu true. Výsledkem je tlačítko výběru pro každý řádek prvku GridView, jak ukazuje obrázek 6. Ve výchozím nastavení jsou tlačítka pro výběr vykreslena jako LinkButtons, ale místo toho můžete použít tlačítka nebo ImageButtons prostřednictvím vlastnosti `ButtonType` CommandField.

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample2.aspx)]

Když je kliknutí na tlačítko výběru řádku GridView (odeslání) kliknuto a vlastnost `SelectedRow` prvku GridView je aktualizována. Kromě vlastnosti `SelectedRow` poskytuje prvek GridView vlastnosti [SelectedIndex](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindex%28VS.80%29.aspx), [SelectedValue](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedvalue%28VS.80%29.aspx)a [SelectedDataKey](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selecteddatakey%28VS.80%29.aspx) . Vlastnost `SelectedIndex` vrací index vybraného řádku, zatímco vlastnosti `SelectedValue` a `SelectedDataKey` vrací hodnoty založené na [vlastnosti DataKeyNames](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames%28VS.80%29.aspx)prvku GridView.

Vlastnost `DataKeyNames` slouží k asociaci jedné nebo více hodnot datových polí s každým řádkem a často se používá k atributu jedinečně identifikující informace z podkladových dat s každým řádkem GridView. Vlastnost `SelectedValue` vrací hodnotu prvního `DataKeyNames` datového pole pro vybraný řádek, kde hodnota vlastnosti `SelectedDataKey` vrátí objekt `DataKey` vybraného řádku, který obsahuje všechny hodnoty pro zadaná klíčová pole dat pro daný řádek.

Vlastnost `DataKeyNames` je automaticky nastavena na jednoznačně identifikující datová pole, když svážete zdroj dat s GridView, DetailsView nebo FormView prostřednictvím návrháře. I když se tato vlastnost automaticky nastavila pro nás v předchozích kurzech, vypracovaly příklady bez zadané vlastnosti `DataKeyNames`. Pro sadu GridView v tomto kurzu a také pro budoucí kurzy, ve kterých budeme zkoumat vkládání, aktualizaci a odstraňování, musí být správně nastavena vlastnost `DataKeyNames`. Chvíli zajistěte, aby vlastnost `DataKeyNames` prvku GridView byla nastavena na hodnotu `ProductID`.

Pojďme si projít náš pokrok v prohlížeči. Všimněte si, že v prvku GridView je uveden název a cena všech produktů společně s přepínačem select LinkButton. Kliknutím na tlačítko Vybrat dojde k zpětnému odeslání. V kroku 2 se dozvíte, jak mít prvek DetailsView reagovat na tento postback zobrazením podrobností pro vybraný produkt.

[![každý produktový řádek obsahuje příkaz SELECT LinkButton](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image20.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image19.png)

**Obrázek 7**: každý produktový řádek obsahuje příkaz SELECT LinkButton ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image21.png)

### <a name="highlighting-the-selected-row"></a>Zvýraznění vybraného řádku

`ProductsGrid` GridView má vlastnost `SelectedRowStyle`, která se dá použít k diktování vizuálního stylu pro vybraný řádek. Používá se správně, což může zlepšit uživatelské prostředí pomocí přehlednějšího zobrazení, který řádek prvku GridView je aktuálně vybrán. Pro tento kurz nechte vybraný řádek zvýrazněný žlutým pozadím.

Stejně jako u našich předchozích kurzů se snažíme, aby se nastavení související s estetickým způsobem definovala jako třídy CSS. Proto vytvořte novou třídu CSS v `Styles.css` s názvem `SelectedRowStyle`.

[!code-css[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample3.css)]

Chcete-li tuto třídu šablony stylů CSS použít pro vlastnost `SelectedRowStyle` *všech* prvků GridView v naší sérii kurzů, upravte `GridView.skin` Skin v motivu `DataWebControls` tak, aby zahrnoval `SelectedRowStyle` nastavení, jak je znázorněno níže:

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/samples/sample4.aspx)]

S tímto sčítáním je teď vybraný řádek GridView zvýrazněný žlutou barvou pozadí.

[![přizpůsobit vzhled vybraného řádku pomocí vlastnosti SelectedRowStyle prvku GridView.](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image23.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image22.png)

**Obrázek 8**: přizpůsobení vzhledu vybraného řádku pomocí vlastnosti `SelectedRowStyle` prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image24.png))

## <a name="step-2-displaying-the-selected-products-details-in-a-detailsview"></a>Krok 2: zobrazení podrobností vybraného produktu v ovládacím prvku DetailsView

Když je dokončeno `ProductsGrid` GridView, vše zůstává pro přidání prvku DetailsView, který zobrazuje informace o vybraném produktu. Do prvku GridView přidejte ovládací prvek DetailsView a vytvořte nový prvek ObjectDataSource s názvem `ProductDetailsDataSource`. Vzhledem k tomu, že chceme, aby tento prvek DetailsView zobrazoval konkrétní informace o vybraném produktu, nakonfigurujte `ProductDetailsDataSource` pro použití `GetProductByProductID(productID)` metody `ProductsBLL` třídy.

[![vyvolat metodu GetProductByProductID (productID) třídy ProductsBLL](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image26.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image25.png)

**Obrázek 9**: vyvolání metody `GetProductByProductID(productID)` `ProductsBLL` třídy ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image27.png))

Hodnota parametru *`productID`* získaná z vlastnosti `SelectedValue` ovládacího prvku GridView. Jak bylo popsáno dříve, vlastnost `SelectedValue` prvku GridView vrátí první hodnotu datového klíče pro vybraný řádek. Proto je nutné, aby vlastnost `DataKeyNames` prvku GridView byla nastavena na hodnotu `ProductID`, aby byla hodnota `ProductID` vybraného řádku vrácena `SelectedValue`.

[![nastavte parametr productID na vlastnost SelectedValue prvku GridView.](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image29.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image28.png)

**Obrázek 10**: nastavte parametr *`productID`* na vlastnost prvku GridView `SelectedValue` ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image30.png)

Po správném nakonfigurování ovládacího prvku `productDetailsDataSource` ObjectDataSource a jeho svázání s ovládacím prvkem DetailsView je tento kurz dokončený. Při prvním navštívení stránky není vybrán žádný řádek, takže vlastnost `SelectedValue` prvku GridView vrátí `null`. Vzhledem k tomu, že neexistují žádné produkty s hodnotou `NULL` `ProductID`, nejsou vráceny žádné záznamy pomocí metody `GetProductByProductID(productID)`, což znamená, že prvek DetailsView není zobrazen (viz obrázek 11). Po kliknutí na tlačítko pro výběr řádku prvku GridView dojde k postbacku a ovládací prvek DetailsView se aktualizuje. Tentokrát `SelectedValue` vlastnost prvku GridView vrátí `ProductID` vybraného řádku, vrátí metoda `GetProductByProductID(productID)` `ProductsDataTable` informace o tomto konkrétním produktu a prvek DetailsView zobrazí tyto podrobnosti (viz obrázek 12).

[![při prvním navštívení se zobrazí pouze prvek GridView.](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image32.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image31.png)

**Obrázek 11**: při prvním navštívení se zobrazí pouze prvek GridView ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image33.png)

[![při výběru řádku se zobrazí podrobnosti o produktu.](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image35.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image34.png)

**Obrázek 12**: po výběru řádku se zobrazí podrobnosti o produktu ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs/_static/image36.png)).

## <a name="summary"></a>Přehled

V tomto a předchozích třech kurzech jsme viděli řadu postupů pro zobrazení hlavních a podrobných sestav. V tomto kurzu jsme prozkoumali použití selektivního prvku GridView pro vytvoření hlavních záznamů a prvku DetailsView k zobrazení podrobností o vybraném hlavním záznamu na stejné stránce. V předchozích kurzech jsme se podívali na postup zobrazení sestav hlavních a podrobností pomocí ovládacích prvků DropDownList a zobrazení hlavních záznamů na jedné webové stránce a podrobností záznamů na jiném.

V tomto kurzu se uzavírá naše zkoumání hlavních a podrobných sestav. Počínaje dalším kurzem zahájíme náš průzkum přizpůsobeného formátování pomocí prvku GridView, DetailsView a FormView. Ukážeme, jak přizpůsobit vzhled těchto ovládacích prvků na základě dat, která jsou s nimi svázána, jak shrnout data v zápatí prvku GridView a jak použít šablony k získání větší úrovně kontroly nad rozložením.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Hilton Giesenow. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](master-detail-filtering-across-two-pages-cs.md)
> [Další](master-detail-filtering-with-a-dropdownlist-vb.md)

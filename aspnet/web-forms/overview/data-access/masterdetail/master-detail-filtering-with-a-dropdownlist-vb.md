---
uid: web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-vb
title: Filtrování seznamu a podrobností s ovládacím prvkem DropDownList (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se dozvíte, jak zobrazit hlavní záznamy v ovládacím prvku DropDownList a podrobnosti o vybrané položce seznamu v prvku GridView.
ms.author: riande
ms.date: 03/31/2010
ms.assetid: ea44717e-ab2e-46cd-a692-e4a9c0de194c
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-filtering-with-a-dropdownlist-vb
msc.type: authoredcontent
ms.openlocfilehash: 62cd296a3f36e1779666a6b5db15b0ce2488d0e4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78528719"
---
# <a name="masterdetail-filtering-with-a-dropdownlist-vb"></a>Filtrování hlavních záznamů / podrobností ovládacím prvkem DropDownList (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_7_VB.exe) nebo [Stáhnout PDF](master-detail-filtering-with-a-dropdownlist-vb/_static/datatutorial07vb1.pdf)

> V tomto kurzu se dozvíte, jak zobrazit hlavní záznamy v ovládacím prvku DropDownList a podrobnosti o vybrané položce seznamu v prvku GridView.

## <a name="introduction"></a>Úvod

Běžným typem sestavy je *Sestava hlavní a podrobnosti*, ve které sestava začíná zobrazením některých sad "hlavních" záznamů. Uživatel pak může přejít k podrobnostem jednoho ze vzorových záznamů, takže zobrazí podrobnosti o tomto hlavním záznamu. Hlavní a podrobné sestavy jsou ideální volbou pro vizualizaci vztahů 1: n, jako je sestava, která zobrazuje všechny kategorie a umožňuje uživateli vybrat konkrétní kategorii a zobrazit její přidružené produkty. Sestavy hlavní/podrobnosti jsou navíc užitečné pro zobrazení podrobných informací z zvláště "nejrůznějších" tabulek (ty, které mají mnoho sloupců). Například "hlavní" úroveň sestavy hlavní/podrobnosti může zobrazit pouze název produktu a jednotkovou cenu produktů v databázi a přechodem na určitý produkt by se zobrazila další pole produktu (kategorie, dodavatel, množství na jednotku atd.).

Existuje mnoho způsobů, jak lze implementovat sestavu hlavní/podrobnosti. Přes toto a další tři kurzy se podíváme na nejrůznější sestavy hlavní/podrobnosti. V tomto kurzu se dozvíte, jak zobrazit hlavní záznamy v [ovládacím prvku DropDownList](https://msdn.microsoft.com/library/dtx91y0z.aspx) a podrobnosti o vybrané položce seznamu v prvku GridView. Konkrétně Sestava hlavní a podrobnosti tohoto kurzu zobrazí seznam kategorií a informací o produktu.

## <a name="step-1-displaying-the-categories-in-a-dropdownlist"></a>Krok 1: zobrazení kategorií v DropDownList

V naší sestavě Master/Detail se zobrazí seznam kategorií v DropDownList a na stránce v prvku GridView se zobrazí níže zobrazené produkty vybrané položky seznamu. První úkol je před námi a pak má mít kategorie zobrazené v DropDownList. Otevřete stránku `FilterByDropDownList.aspx` ve složce `Filtering`, přetáhněte objekt DropDownList z panelu nástrojů na Návrhář stránky a nastavte jeho vlastnost `ID` na `Categories`. Potom klikněte na odkaz zvolit zdroj dat z inteligentní značky DropDownList. Tím se zobrazí Průvodce konfigurací zdroje dat.

[![určení zdroje dat ovládacího prvku DropDownList](master-detail-filtering-with-a-dropdownlist-vb/_static/image2.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image1.png)

**Obrázek 1**: určení zdroje dat DropDownList ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-a-dropdownlist-vb/_static/image3.png))

Vyberte, chcete-li přidat nový prvek ObjectDataSource s názvem `CategoriesDataSource`, který vyvolá metodu `GetCategories()` `CategoriesBLL` třídy.

[![přidat nový prvek ObjectDataSource s názvem CategoriesDataSource](master-detail-filtering-with-a-dropdownlist-vb/_static/image5.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image4.png)

**Obrázek 2**: Přidání nového prvku ObjectDataSource s názvem `CategoriesDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-a-dropdownlist-vb/_static/image6.png))

[![zvolit použití třídy CategoriesBLL](master-detail-filtering-with-a-dropdownlist-vb/_static/image8.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image7.png)

**Obrázek 3**: vyberte, pokud chcete použít třídu `CategoriesBLL` ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-with-a-dropdownlist-vb/_static/image9.png)

[![nakonfigurovat prvek ObjectDataSource pro použití metody GetCategories ()](master-detail-filtering-with-a-dropdownlist-vb/_static/image11.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image10.png)

**Obrázek 4**: Konfigurace prvku ObjectDataSource pro použití metody `GetCategories()` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-a-dropdownlist-vb/_static/image12.png))

Po nakonfigurování prvku ObjectDataSource je stále potřeba určit, jaké pole zdroje dat by se mělo zobrazit v DropDownList a který má být přidružen jako hodnota pro položku seznamu. Má pole `CategoryName` jako hodnotu zobrazení a `CategoryID` jako hodnotu pro každou položku seznamu.

[![mají DropDownList zobrazit pole CategoryName a jako hodnotu použít CategoryID.](master-detail-filtering-with-a-dropdownlist-vb/_static/image14.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image13.png)

**Obrázek 5**: DropDownList zobrazí pole `CategoryName` a jako hodnotu použije `CategoryID` ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-with-a-dropdownlist-vb/_static/image15.png)

V tuto chvíli máme ovládací prvek DropDownList, který je naplněný záznamy z `Categories` tabulky (vše bylo dokončeno přibližně po dobu šesti sekund). Obrázek 6 znázorňuje náš průběh, pokud je zobrazený v prohlížeči.

[![rozevíracího seznamu pro aktuální kategorie](master-detail-filtering-with-a-dropdownlist-vb/_static/image17.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image16.png)

**Obrázek 6**: rozevírací seznam pro aktuální kategorie ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-a-dropdownlist-vb/_static/image18.png))

## <a name="step-2-adding-the-products-gridview"></a>Krok 2: Přidání prvku GridView pro produkty

Poslední krok v naší sestavě hlavní/podrobnosti je seznam produktů přidružených k vybrané kategorii. K tomu je nutné přidat prvek GridView na stránku a vytvořit nový prvek ObjectDataSource s názvem `productsDataSource`. Mít ovládací prvek `productsDataSource` Odvrácená data z metody `GetProductsByCategoryID(categoryID)` `ProductsBLL` třídy.

[![vybrat metodu GetProductsByCategoryID (KódKategorie)](master-detail-filtering-with-a-dropdownlist-vb/_static/image20.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image19.png)

**Obrázek 7**: vyberte metodu `GetProductsByCategoryID(categoryID)` ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-a-dropdownlist-vb/_static/image21.png)).

Po zvolení této metody Průvodce ObjectDataSource zobrazí výzvu k zadání hodnoty parametru *`categoryID`* metody. Chcete-li použít hodnotu vybrané `categories` položku DropDownList, nastavte zdroj parametru jako ovládací prvek a vlastnosti ControlID k `Categories`.

[![nastavit parametr categoryID na hodnotu kategorie DropDownList](master-detail-filtering-with-a-dropdownlist-vb/_static/image23.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image22.png)

**Obrázek 8**: nastavte parametr *`categoryID`* na hodnotu `Categories` DropDownList ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-with-a-dropdownlist-vb/_static/image24.png)

Chvíli si Projděte náš pokrok v prohlížeči. Při první návštěvě stránky budou tyto produkty patřit do vybrané kategorie (nápoje) (jak je znázorněno na obrázku 9), ale změna ovládacího prvkem DropDownList neaktualizuje data. Je to proto, že k tomu, aby se prvek GridView mohl aktualizovat, musí dojít k postbacku. K tomu máme dvě možnosti (ani to, co nevyžaduje psaní kódu):

- Nastavte[vlastnost AutoPostBack](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listcontrol.autopostback%28VS.80%29.aspx) **kategorie ovládacího prvku DropDownList** **na hodnotu true.** (Můžete to provést tak, že zkontrolujete možnost Povolit AutoPostBack v inteligentní značce DropDownList.) Tím se aktivuje postback, kdykoli uživatel změní vybranou položku DropDownList. Proto když uživatel vybere novou kategorii z ovládacího prvku DropDownList, vystavení zpětného volání bude následovat a komponenta GridView bude aktualizována s produkty nově vybrané kategorie. (Jedná se o přístup, který jsem v tomto kurzu použili.)
- **Přidejte webové ovládací prvky tlačítka vedle ovládacího prvku DropDownList.** Nastavte jeho vlastnost `Text` na hodnotu aktualizovat nebo podobným způsobem. S tímto přístupem bude uživatel muset vybrat novou kategorii a pak kliknout na tlačítko. Kliknutím na tlačítko dojde k odeslání zpětného volání a aktualizaci prvku GridView, aby vybral seznam produktů vybrané kategorie.

Obrázky 9 a 10 ilustrují sestavu hlavní/podrobnosti v akci.

[![při první návštěvě stránky se zobrazí nápojové produkty.](master-detail-filtering-with-a-dropdownlist-vb/_static/image26.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image25.png)

**Obrázek 9**: když poprvé navštívíte stránku, zobrazí se nápojové produkty ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-a-dropdownlist-vb/_static/image27.png)).

[![výběru nového produktu (vytvořeného) automaticky způsobí PostBack, aktualizaci prvku GridView.](master-detail-filtering-with-a-dropdownlist-vb/_static/image29.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image28.png)

**Obrázek 10**: výběr nového produktu (vytvořeného) automaticky způsobí postback, aktualizaci prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-a-dropdownlist-vb/_static/image30.png)).

## <a name="adding-a----choose-a-category----list-item"></a>Přidání položky seznamu "--zvolit kategorii"

Při první návštěvě `FilterByDropDownList.aspx` stránky je ve výchozím nastavení vybrána položka první položka seznamu (nápoje) kategorie, která zobrazuje nápoje v prvku GridView. Místo toho, aby se zobrazovaly výrobky první kategorie, můžeme místo toho mít vybranou položku DropDownList, která říká něco, jako je například, a zvolit kategorii--.

Chcete-li přidat novou položku seznamu do ovládacího prvků DropDownList, přejděte na okno Vlastnosti a klikněte na tlačítko se třemi tečkami ve vlastnosti `Items`. Přidejte novou položku seznamu s `Text` "--zvolit kategorii--" a `Value` `-1`.

[![přidání a výběr kategorie--vyberte položku seznamu.](master-detail-filtering-with-a-dropdownlist-vb/_static/image32.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image31.png)

**Obrázek 11**: Přidání a výběr kategorie – seznam položek ([kliknutím zobrazíte obrázek v plné velikosti](master-detail-filtering-with-a-dropdownlist-vb/_static/image33.png))

Alternativně můžete přidat položku seznamu přidáním následujícího kódu do ovládacího prvkem DropDownList:

[!code-aspx[Main](master-detail-filtering-with-a-dropdownlist-vb/samples/sample1.aspx)]

Kromě toho je potřeba nastavit `AppendDataBoundItems` ovládacího prvku DropDownList na hodnotu true, protože pokud jsou kategorie svázány s ovládacím prvkem DropDownList z prvku ObjectDataSource, budou přepsány jakékoli ručně přidané položky seznamu, pokud `AppendDataBoundItems` není true.

![Nastavte vlastnost AppendDataBoundItems na hodnotu true.](master-detail-filtering-with-a-dropdownlist-vb/_static/image34.png)

**Obrázek 12**: nastavte vlastnost `AppendDataBoundItems` na hodnotu true.

Po těchto změnách se při první návštěvě stránky vybere možnost--zvolit kategorii – a nezobrazí se žádné produkty.

[![na počátečním načtení stránky nejsou zobrazeny žádné produkty.](master-detail-filtering-with-a-dropdownlist-vb/_static/image36.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image35.png)

**Obrázek 13**: na počátečním načtení stránky nejsou zobrazeny žádné produkty ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-with-a-dropdownlist-vb/_static/image37.png)

Důvod, proč se nezobrazují žádné produkty, pokud je vybrána položka "--zvolit kategorii--" položka seznamu, protože její hodnota je `-1` a v databázi nejsou žádné produkty s `CategoryID` `-1`. Pokud se jedná o požadované chování, jste v tomto okamžiku hotovi! Pokud však chcete zobrazit *všechny* kategorie, když je vybrána položka seznamu "--zvolit kategorii--", vraťte se do třídy `ProductsBLL` a upravte metodu `GetProductsByCategoryID(categoryID)` tak, aby vyvolala metodu `GetProducts()`, pokud předaný parametr *`categoryID`* je menší než nula:

[!code-vb[Main](master-detail-filtering-with-a-dropdownlist-vb/samples/sample2.vb)]

Postup, který se tady používá, je podobný přístupu, který jsme použili k zobrazení všech dodavatelů zpátky v kurzu [deklarativních parametrů](../basic-reporting/declarative-parameters-cs.md) , i když v tomto příkladu používáme hodnotu `-1` k označení toho, že všechny záznamy by se měly načíst na rozdíl od `Nothing`. Důvodem je, že parametr *`categoryID`* metody `GetProductsByCategoryID(categoryID)` očekává, že předaná celočíselná hodnota, která je v kurzu deklarativních parametrů, přešla do vstupního parametru řetězce.

Obrázek 14 ukazuje snímek obrazovky `FilterByDropDownList.aspx`, když je vybrána možnost--zvolit kategorii--. Tady se zobrazí všechny produkty ve výchozím nastavení a uživatel může zúžit zobrazení výběrem konkrétní kategorie.

[![všechny produkty jsou teď uvedené ve výchozím nastavení.](master-detail-filtering-with-a-dropdownlist-vb/_static/image39.png)](master-detail-filtering-with-a-dropdownlist-vb/_static/image38.png)

**Obrázek 14**: všechny produkty jsou teď uvedené ve výchozím nastavení ([kliknutím zobrazíte obrázek v plné velikosti).](master-detail-filtering-with-a-dropdownlist-vb/_static/image40.png)

## <a name="summary"></a>Souhrn

Při zobrazení hierarchicky souvisejících dat často pomáhá prezentovat data pomocí hlavních a podrobných sestav, od kterých může uživatel začít perusing data z horní části hierarchie a přejít k podrobnostem. V tomto kurzu jsme prozkoumali vytvoření jednoduché sestavy hlavní/podrobnosti zobrazující produkty vybrané kategorie. To bylo provedeno pomocí ovládacího prvku DropDownList pro seznam kategorií a GridView pro produkty patřící do vybrané kategorie.

V [dalším kurzu](master-detail-filtering-with-two-dropdownlists-vb.md) budeme postupně přebírat rozhraní DropDownList pomocí dvou ovládacích prvků DropDownList.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Předchozí](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md)
> [Další](master-detail-filtering-with-two-dropdownlists-vb.md)

---
uid: web-forms/overview/data-access/introduction/creating-a-business-logic-layer-vb
title: Vytvoření vrstvy obchodní logiky (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se dozvíte, jak centralizovat vaše obchodní pravidla do vrstvy obchodní logiky (knihoven BLL), která slouží jako prostředník pro výměnu dat mezi t...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 142e5181-29ce-4bb9-907b-2a0becf7928b
msc.legacyurl: /web-forms/overview/data-access/introduction/creating-a-business-logic-layer-vb
msc.type: authoredcontent
ms.openlocfilehash: 2ee4789ea9567b7bcd70eb63695e0b1d73076dc2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74572650"
---
# <a name="creating-a-business-logic-layer-vb"></a>Vytvoření vrstvy obchodní logiky (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_2_VB.exe) nebo [Stáhnout PDF](creating-a-business-logic-layer-vb/_static/datatutorial02vb1.pdf)

> V tomto kurzu se dozvíte, jak centralizovat vaše obchodní pravidla do vrstvy obchodní logiky (knihoven BLL), která slouží jako prostředník pro výměnu dat mezi prezentační vrstvou a DAL.

## <a name="introduction"></a>Úvod

Vrstva přístupu k datům (DAL) vytvořená v [prvním kurzu](creating-a-data-access-layer-vb.md) čistě odděluje logiku přístupu k datům z logiky prezentace. Nicméně zatímco DAL čistě odděluje údaje o přístupu k datům z prezentační vrstvy, nevynutila žádná obchodní pravidla, která by mohla platit. U naší aplikace například můžeme chtít zakázat pole `CategoryID` nebo `SupplierID` tabulky `Products`, která se mají změnit, když je pole `Discontinued` nastaveno na hodnotu 1, nebo můžeme vynutilit pravidla seniority, což zabrání situacím, kdy je zaměstnanec spravován jiným uživatelem, který byl zařazen po nich. Dalším běžným scénářem je autorizace, ale jenom uživatelé v určité roli můžou odstranit produkty nebo můžou změnit `UnitPrice`ou hodnotu.

V tomto kurzu se dozvíte, jak centralizovat tato obchodní pravidla do vrstvy obchodní logiky (knihoven BLL), která slouží jako prostředník pro výměnu dat mezi prezentační vrstvou a DAL. V reálné aplikaci by měla být knihoven BLL implementována jako samostatný projekt knihovny tříd; Nicméně pro tyto kurzy implementujeme knihoven BLL jako řadu tříd v naší složce `App_Code`, aby se zjednodušila struktura projektu. Obrázek 1 znázorňuje vztahy architektury mezi prezentační vrstvou, knihoven BLL a DAL.

![KNIHOVEN BLL odděluje prezentační vrstvu od vrstvy přístupu k datům a ukládá obchodní pravidla.](creating-a-business-logic-layer-vb/_static/image1.png)

**Obrázek 1**: knihoven BLL odděluje prezentační vrstvu od vrstvy přístupu k datům a ukládá obchodní pravidla.

Namísto vytváření samostatných tříd pro implementaci naší [obchodní logiky](http://en.wikipedia.org/wiki/Business_logic)můžeme Alternativně umístit tuto logiku přímo do typové datové sady s částečnými třídami. Příklad vytvoření a rozšíření typované datové sady naleznete v prvním kurzu.

## <a name="step-1-creating-the-bll-classes"></a>Krok 1: vytvoření tříd knihoven BLL

Naše knihoven BLL se skládají ze čtyř tříd, jedna pro každý TableAdapter v rámci DAL; Každá z těchto tříd knihoven BLL bude mít metody pro načítání, vkládání, aktualizaci a odstraňování z odpovídajících TableAdapter v rámci DAL, přičemž se použijí vhodná obchodní pravidla.

Aby bylo možné čistě oddělit třídy související s DAL a knihoven BLL, vytvoříme dvě podsložky ve složce `App_Code` `DAL` a `BLL`. Jednoduše klikněte pravým tlačítkem myši na složku `App_Code` v Průzkumník řešení a vyberte možnost Nová složka. Po vytvoření těchto dvou složek přesuňte typovou datovou sadu vytvořenou v prvním kurzu do podsložky `DAL`.

Dále vytvořte v podsložce `BLL` čtyři soubory třídy knihoven BLL. Chcete-li to provést, klikněte pravým tlačítkem myši na podsložku `BLL`, vyberte možnost Přidat novou položku a vyberte šablonu třídy. Pojmenujte čtyři třídy `ProductsBLL`, `CategoriesBLL`, `SuppliersBLL`a `EmployeesBLL`.

![Přidat čtyři nové třídy do složky App_Code](creating-a-business-logic-layer-vb/_static/image2.png)

**Obrázek 2**: Přidání čtyř nových tříd do složky `App_Code`

Nyní přidáme do každé třídy metody, které jednoduše zabalí metody definované pro objekty TableAdapter z prvního kurzu. V současné době budou tyto metody volat přímo na DAL. později se vrátíme k přidání jakékoli potřebné obchodní logiky.

> [!NOTE]
> Pokud používáte Visual Studio Standard Edition nebo vyšší (to znamená, že *nepoužíváte* Visual Web Developer), můžete volitelně navrhnout třídy vizuálně pomocí [Návrhář tříd](https://msdn.microsoft.com/library/default.asp?url=/library/dv_vstechart/html/clssdsgnr.asp). Další informace o této nové funkci v aplikaci Visual Studio najdete na [blogu Návrhář tříd](https://blogs.msdn.com/classdesigner/default.aspx) .

Pro třídu `ProductsBLL` musíme přidat celkem sedm metod:

- `GetProducts()` vrátí všechny produkty.
- `GetProductByProductID(productID)` vrátí produkt se zadaným ID produktu.
- `GetProductsByCategoryID(categoryID)` vrátí všechny produkty ze zadané kategorie.
- `GetProductsBySupplier(supplierID)` vrátí všechny produkty od určeného dodavatele.
- `AddProduct(productName, supplierID, categoryID, quantityPerUnit, unitPrice, unitsInStock, unitsOnOrder, reorderLevel, discontinued)` vloží do databáze nový produkt pomocí předaných hodnot; Vrátí hodnotu `ProductID` nově vloženého záznamu.
- `UpdateProduct(productName, supplierID, categoryID, quantityPerUnit, unitPrice, unitsInStock, unitsOnOrder, reorderLevel, discontinued, productID)` aktualizuje existující produkt v databázi pomocí předaných hodnot. Vrátí `True`, pokud se přesně jeden řádek aktualizoval, `False` jinak.
- `DeleteProduct(productID)` Odstraní zadaný produkt z databáze.

ProductsBLL. vb

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample1.vb)]

Metody, které jednoduše vracejí data `GetProducts`, `GetProductByProductID`, `GetProductsByCategoryID`a `GetProductBySuppliersID` jsou poměrně jednoduché, protože se jednoduše volají na DAL. V některých scénářích můžou existovat obchodní pravidla, která je potřeba implementovat na této úrovni (například autorizační pravidla na základě aktuálně přihlášeného uživatele nebo role, ke které uživatel patří), ale tyto metody ponecháme tak, jak jsou. Pro tyto metody pak knihoven BLL slouží pouze jako proxy, prostřednictvím kterého prezentační vrstva přistupuje k podkladovým datům z vrstvy přístupu k datům.

Metody `AddProduct` a `UpdateProduct` obě přijímají jako parametry hodnoty pro různá pole produktu a přidávají nový produkt nebo aktualizují existující produkt, v uvedeném pořadí. Vzhledem k tomu, že mnoho sloupců `Product` tabulky může přijmout `NULL` hodnoty (`CategoryID`, `SupplierID`a `UnitPrice`), tyto vstupní parametry pro `AddProduct` a `UpdateProduct`, které mapují na tyto sloupce, používají [typy s možnou hodnotou null](https://msdn.microsoft.com/library/1t3y8s4s(v=vs.80).aspx). Typy s možnou hodnotou null jsou v rozhraní .NET 2,0 nové a poskytují techniku pro určení, zda by měl být typ hodnoty místo `Nothing`. Další informace najdete v blogu [Vick](http://www.panopticoncentral.net/)na stránce o [pravdivosti typů s možnou hodnotou null a VB](http://www.panopticoncentral.net/archive/2004/06/04/1180.aspx) a technickou dokumentaci pro strukturu s [možnou hodnotou null](https://msdn.microsoft.com/library/b3h38hb0%28VS.80%29.aspx) .

Všechny tři metody vrací logickou hodnotu, která označuje, zda byl řádek vložen, aktualizován nebo odstraněn, protože výsledkem operace není ovlivněný řádek. Například pokud vývojář stránky volá `DeleteProduct` předání v `ProductID` pro neexistující produkt, nebude příkaz `DELETE` vydaný pro databázi nijak ovlivněn, takže metoda `DeleteProduct` bude vracet `False`.

Všimněte si, že při přidávání nového produktu nebo aktualizaci existujícího produktu převezmeme nové nebo změněné hodnoty pole produktu jako seznam skalárních hodnot na rozdíl od přijetí instance `ProductsRow`. Tento přístup se vybral, protože třída `ProductsRow` je odvozená od `DataRow` třídy ADO.NET, která nemá výchozí konstruktor bez parametrů. Aby bylo možné vytvořit novou instanci `ProductsRow`, je nutné nejprve vytvořit instanci `ProductsDataTable` a poté vyvolat metodu `NewProductRow()` (kterou provedeme v `AddProduct`). Tím dojde k nedostatku svých hlav při vkládání a aktualizaci produktů pomocí prvku ObjectDataSource. V krátkém případě se prvek ObjectDataSource pokusí vytvořit instanci vstupních parametrů. Pokud metoda knihoven BLL očekává instanci `ProductsRow`, prvek ObjectDataSource se pokusí jeden vytvořit, ale selže z důvodu nedostatku výchozího konstruktoru bez parametrů. Další informace o tomto problému naleznete v následujících dvou příspěvcích na fórech ASP.NET: [aktualizace objectdatasources pomocí datových sad se silnými typy](https://forums.asp.net/1098630/ShowPost.aspx)a [problém s datovou sadou ObjectDataSource a silně typovaného typu](https://forums.asp.net/1048212/ShowPost.aspx).

Dále kód v `AddProduct` i `UpdateProduct`vytvoří instanci `ProductsRow` a naplní ji hodnotami, které jsou právě předány. Při přiřazování hodnot k datacolumnům objektu DataRow může dojít k různým kontrolám ověření na úrovni pole. Proto ručním vložením předaných hodnot do objektu DataRow pomůže zajistit, aby byla data předána do metody knihoven BLL. Třídy DataRow silného typu generované v aplikaci Visual Studio bohužel nepoužívají typy s možnou hodnotou null. Místo toho, abyste označili, že konkrétní DataColumn v objektu DataRow by měl odpovídat hodnotě `NULL` databáze, je nutné použít metodu `SetColumnNameNull()`.

V `UpdateProduct` nejdřív nahrajeme produkt, který se má aktualizovat pomocí `GetProductByProductID(productID)`. I když se to může zdát jako zbytečných cest k databázi, tato dodatečná cesta se v budoucích kurzech ukáže v budoucích kurzech, které se seznámí s optimistické souběžnosti. Optimistická souběžnost je technika, která zajistí, že dva uživatelé, kteří pracují současně se stejnými daty, nechtěně nepřepisují žádné další změny. Při překonávání celého záznamu je také snazší vytvořit metody aktualizace v knihoven BLL, které upraví pouze podmnožinu sloupců objektu DataRow. Při zkoumání `SuppliersBLL` třídy uvidíme takový příklad.

Nakonec si všimněte, že třída `ProductsBLL` má pro ni použit [atribut DataObject](https://msdn.microsoft.com/library/system.componentmodel.dataobjectattribute.aspx) (syntaxe `[System.ComponentModel.DataObject]` těsně před příkazem třídy v horní části souboru) a metody mají [atributy DataObjectMethodAttribute](https://msdn.microsoft.com/library/system.componentmodel.dataobjectmethodattribute.aspx). Atribut `DataObject` označuje třídu jako objekt vhodný pro vazbu k [ovládacímu prvku ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx), zatímco `DataObjectMethodAttribute` označuje účel metody. Jak uvidíme v budoucích kurzech, ASP.NET 2.0 ObjectDataSource usnadňuje deklarativní přístup k datům z třídy. Aby bylo možné filtrovat seznam možných tříd, ke kterým lze navazovat vazby v průvodci ObjectDataSource, ve výchozím nastavení se v rozevíracím seznamu Průvodce zobrazují pouze ty třídy označené jako `DataObjects`. Třída `ProductsBLL` bude fungovat stejně i bez těchto atributů, ale přidáním jim usnadňuje práci v průvodci ObjectDataSource.

## <a name="adding-the-other-classes"></a>Přidání dalších tříd

Po dokončení `ProductsBLL` třídy je stále potřeba přidat třídy pro práci s kategoriemi, dodavateli a zaměstnanci. Vytvořte si chvilku pro vytvoření následujících tříd a metod pomocí konceptů z výše uvedeného příkladu:

- **CategoriesBLL.cs**

    - `GetCategories()`
    - `GetCategoryByCategoryID(categoryID)`
- **SuppliersBLL.cs**

    - `GetSuppliers()`
    - `GetSupplierBySupplierID(supplierID)`
    - `GetSuppliersByCountry(country)`
    - `UpdateSupplierAddress(supplierID, address, city, country)`
- **EmployeesBLL.cs**

    - `GetEmployees()`
    - `GetEmployeeByEmployeeID(employeeID)`
    - `GetEmployeesByManager(managerID)`

Jedna z metod, které se zaznamená, je metoda `UpdateSupplierAddress` `SuppliersBLL` třídy. Tato metoda poskytuje rozhraní pro aktualizaci pouze informací o adrese dodavatele. Interně Tato metoda přečte v objektu `SupplierDataRow` pro zadanou `supplierID` (pomocí `GetSupplierBySupplierID`), nastaví jeho vlastnosti související s adresou a pak zavolá do `Update` metody `SupplierDataTable`. Následující metoda `UpdateSupplierAddress`:

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample2.vb)]

Informace najdete v tomto článku ke stažení pro úplnou implementaci tříd knihoven BLL.

## <a name="step-2-accessing-the-typed-datasets-through-the-bll-classes"></a>Krok 2: přístup k typovým datovým sadám prostřednictvím tříd knihoven BLL

V prvním kurzu jsme viděli příklady práce přímo s typovou datovou sadou, ale s přidáním našich tříd knihoven BLL, musí prezentační vrstva pracovat s knihoven BLL. V příkladu `AllProducts.aspx` v prvním kurzu `ProductsTableAdapter` byl použit k navázání seznamu produktů na prvek GridView, jak je znázorněno v následujícím kódu:

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample3.vb)]

Chcete-li použít nové třídy knihoven BLL, je třeba změnit první řádek kódu pouhým nahrazením objektu `ProductsTableAdapter` objektem `ProductBLL`:

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample4.vb)]

Ke třídám knihoven BLL lze také přistupovat deklarativně (jako lze použít typovou datovou sadu) pomocí prvku ObjectDataSource. V následujících kurzech se podrobněji podíváme na ObjectDataSource.

[![se seznam produktů zobrazuje v prvku GridView.](creating-a-business-logic-layer-vb/_static/image4.png)](creating-a-business-logic-layer-vb/_static/image3.png)

**Obrázek 3**: seznam produktů se zobrazí v prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-business-logic-layer-vb/_static/image5.png)).

## <a name="step-3-adding-field-level-validation-to-the-datarow-classes"></a>Krok 3: Přidání ověřování na úrovni pole do tříd DataRow

Ověřování na úrovni pole jsou kontroly, které se vztahují k hodnotám vlastností obchodních objektů při vkládání nebo aktualizaci. Některá ověřovací pravidla na úrovni polí pro produkty zahrnují:

- Pole `ProductName` musí mít délku 40 znaků nebo méně.
- Pole `QuantityPerUnit` nesmí být delší než 20 znaků.
- Pole `ProductID`, `ProductName`a `Discontinued` jsou povinná, ale všechna ostatní pole jsou volitelná.
- Pole `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`a `ReorderLevel` musí být větší nebo rovna nule.

Tato pravidla mohou a by se měla vyjádřit na úrovni databáze. Omezení počtu znaků u polí `ProductName` a `QuantityPerUnit` jsou zachycena datovými typy těchto sloupců v tabulce `Products` (`nvarchar(40)` a `nvarchar(20)`uvedeném v uvedeném pořadí). Zda jsou pole povinná a volitelná, se vyjádří, pokud sloupec databázových tabulek povoluje `NULL` s. Existují čtyři [kontrolní omezení](https://msdn.microsoft.com/library/ms188258.aspx) , která zajišťují, že se do `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`nebo `ReorderLevel` sloupců dají pouze hodnoty větší než nula nebo se jim rovnat.

Kromě vynucování těchto pravidel v databázi by měly být také vynuceny na úrovni datové sady. Ve skutečnosti je délka pole a údaj, zda je hodnota vyžadována nebo volitelná, již zachycena pro sadu datových sloupců v objektu DataTable. Pokud chcete zobrazit automaticky zadané ověřování na úrovni pole, přejděte do návrháře DataSet, vyberte pole z jedné z datových tabulek a pak přejděte na okno Vlastnosti. Jak ukazuje obrázek 4, `QuantityPerUnit` DataColumn v `ProductsDataTable` má maximální délku 20 znaků a povoluje `NULL` hodnoty. Pokud se pokusíte nastavit vlastnost `QuantityPerUnit` `ProductsDataRow`na hodnotu řetězce delší než 20 znaků, bude vyvolána `ArgumentException`.

[![DataColumn poskytuje základní ověřování na úrovni pole.](creating-a-business-logic-layer-vb/_static/image7.png)](creating-a-business-logic-layer-vb/_static/image6.png)

**Obrázek 4**: sloupec DataColumn poskytuje základní ověřování na úrovni pole ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-business-logic-layer-vb/_static/image8.png)).

Bohužel nemůžeme specifikovat kontroly hranic, například `UnitPrice` hodnota musí být větší nebo rovna nule, a to prostřednictvím okno Vlastnosti. Pro poskytnutí tohoto typu ověřování na úrovni pole musíme vytvořit obslužnou rutinu události pro událost [ColumnChanging](https://msdn.microsoft.com/library/system.data.datatable.columnchanging%28VS.80%29.aspx) objektu DataTable. Jak je uvedeno v [předchozím kurzu](creating-a-data-access-layer-vb.md), datové sady, datové tabulky a objekty DataRow vytvořené typovou datovou sadou lze rozšířit prostřednictvím použití dílčích tříd. Pomocí této techniky můžeme vytvořit obslužnou rutinu události `ColumnChanging` pro třídu `ProductsDataTable`. Začněte vytvořením třídy ve složce `App_Code` s názvem `ProductsDataTable.ColumnChanging.vb`.

[![přidat novou třídu do složky App_Code](creating-a-business-logic-layer-vb/_static/image10.png)](creating-a-business-logic-layer-vb/_static/image9.png)

**Obrázek 5**: Přidání nové třídy do složky `App_Code` ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-business-logic-layer-vb/_static/image11.png))

Dále vytvořte obslužnou rutinu události pro událost `ColumnChanging`, která zajistí, aby hodnoty sloupce `UnitPrice`, `UnitsInStock`, `UnitsOnOrder`a `ReorderLevel` (pokud nejsou `NULL`) byly větší nebo rovny nule. Pokud je některý z těchto sloupců mimo rozsah, vyvolejte `ArgumentException`.

ProductsDataTable. ColumnChanging. vb

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample5.vb)]

## <a name="step-4-adding-custom-business-rules-to-the-blls-classes"></a>Krok 4: Přidání vlastních obchodních pravidel do tříd knihoven BLL

Kromě ověřování na úrovni pole můžou existovat vlastní obchodní pravidla vysoké úrovně, která zahrnují různé entity nebo koncepty, které se vyhodnotit na úrovni jednoho sloupce, například:

- Pokud je produkt vyřazený, jeho `UnitPrice` nejde aktualizovat.
- Země pobytu zaměstnance musí být stejná jako země pobytu svého nadřízeného.
- Produkt nelze ukončit, pokud se jedná o jediný produkt poskytovaný dodavatelem.

Třídy knihoven BLL by měly obsahovat kontroly, aby se zajistilo dodržování obchodních pravidel aplikace. Tyto kontroly lze přidat přímo do metod, na které se vztahují.

Představte si, že naše obchodní pravidla určují, že produkt nejde označit jako vyřazený, pokud byl jediným produktem od daného dodavatele. To znamená, že pokud produkt *X* byl jediným produktem, který jsme koupili *od dodavatele a*, nemůžeme *X* označit jako vyřazené; Pokud se ale dodavatel *Y* doručí se třemi produkty, *a*, *B*a *C*, můžeme označit všechny z nich jako ukončené. Liché obchodní pravidlo, ale obchodní pravidla a běžné zvyklosti nejsou vždycky zarovnaná!

Abyste toto obchodní pravidlo vynutili v `UpdateProducts` metodě, začneme tak, že zkontrolujete, jestli `Discontinued` byla nastavená na `True`, a pokud ano, zavoláme `GetProductsBySupplierID` k určení, kolik produktů jsme si koupili od dodavatele tohoto produktu. Pokud od tohoto dodavatele koupíte jenom jeden produkt, vyvoláme `ApplicationException`.

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample6.vb)]

## <a name="responding-to-validation-errors-in-the-presentation-tier"></a>Reakce na chyby ověřování v prezentační vrstvě

Při volání knihoven BLL z prezentační vrstvy se můžeme rozhodnout, zda se pokusíte zpracovat jakékoli výjimky, které mohou být vyvolány, nebo umožnit jejich bublinu až do ASP.NET (což vyvolá událost `Error` `HttpApplication`). Abychom mohli zpracovat výjimku při práci s knihoven BLL programově, můžeme použít příkaz [Try... Blok catch](https://msdn.microsoft.com/library/fk6t46tz%28VS.80%29.aspx) , jak ukazuje následující příklad:

[!code-vb[Main](creating-a-business-logic-layer-vb/samples/sample7.vb)]

Jak uvidíme v budoucích kurzech, zpracování výjimek, které se doplňují z knihoven BLL při použití webového ovládacího prvku data pro vložení, aktualizaci nebo odstranění dat, je možné zpracovat přímo v obslužné rutině události, a to na rozdíl od nutnosti zalamovat kód v `Try...Catch`ch blocích.

## <a name="summary"></a>Přehled

Dobře navržená aplikace je vytvořená do samostatných vrstev, z nichž každý zapouzdřuje určitou roli. V prvním kurzu této série článků jsme vytvořili vrstvu přístupu k datům pomocí zadaných datových sad; v tomto kurzu jsme sestavili vrstvu obchodní logiky jako řadu tříd v `App_Code` složce aplikace, která volá na naši DAL. KNIHOVEN BLL implementuje logiku na úrovni polí a na úrovni firmy pro naši aplikaci. Kromě vytvoření samostatného knihoven BLL jako v tomto kurzu je další možností rozšířit metody objekty TableAdapter pomocí částečných tříd. Použití této techniky ale neumožňuje přepsat existující metody ani Nedělit naše DAL a naše knihoven BLL jako čistě jako přístup, který jsme udělali v tomto článku.

Po dokončení DAL a knihoven BLL jsme připraveni začít s naší prezentační vrstvou. V [dalším kurzu](master-pages-and-site-navigation-vb.md) podíváme se na stručný přehled z témat pro přístup k datům a definujte konzistentní rozložení stránky pro použití v rámci kurzů.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Recenzenti potenciálních zákazníků pro tento kurz byly Liz Shulok, Dennis Patterson, Carlos Santos a Hilton Giesenow. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](creating-a-data-access-layer-vb.md)
> [Další](master-pages-and-site-navigation-vb.md)

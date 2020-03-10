---
uid: web-forms/overview/data-access/working-with-batched-data/batch-deleting-vb
title: Dávkové odstraňování (VB) | Microsoft Docs
author: rick-anderson
description: Naučte se, jak odstranit více záznamů databáze v rámci jedné operace. Ve vrstvě uživatelského rozhraní sestavíme na rozšířeném prvku GridView vytvořeném ve starším tut...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: 4fb72f75-32ab-4bf7-a764-be20367be726
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-deleting-vb
msc.type: authoredcontent
ms.openlocfilehash: 0974a16764eee2ef03cf36b4b15f9ef41f99982b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78589353"
---
# <a name="batch-deleting-vb"></a>Dávkové odstraňování (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_65_VB.zip) nebo [stažení PDF](batch-deleting-vb/_static/datatutorial65vb1.pdf)

> Naučte se, jak odstranit více záznamů databáze v rámci jedné operace. Ve vrstvě uživatelského rozhraní sestavíme na rozšířeném prvku GridView vytvořeném v předchozím kurzu. Ve vrstvě přístupu k datům rozbalíme více operací odstranění v rámci transakce, abyste zajistili, že všechna odstranění jsou úspěšná nebo že se všechna odstranění vrátí zpět.

## <a name="introduction"></a>Úvod

[Předchozí kurz](batch-updating-vb.md) prozkoumal, jak vytvořit rozhraní pro úpravu dávky pomocí plně upravitelného prvku GridView. V situacích, kdy uživatelé běžně upravují mnoho záznamů najednou, bude rozhraní pro úpravu dávky vyžadovat mnohem méně zpětných volání a přepínačů kontextu klávesnice na myš, což zlepšuje efektivitu koncových uživatelů. Tato technika je obdobně užitečná pro stránky, kde je běžné, že uživatelé mohou odstranit mnoho záznamů v jednom přechodu.

Kdokoli, kdo používal online e-mailový klient, je již obeznámen s jedním z nejběžnějších rozhraní pro odstranění dávky: zaškrtávací políčko v každém řádku mřížky s odpovídajícím tlačítkem odstranit všechny zaškrtnuté položky (viz obrázek 1). Tento kurz je spíše krátký, protože už jsme dokončili veškerou tvrdou práci v předchozích kurzech při vytváření webového rozhraní a metody pro odstranění řady záznamů jako jedné atomické operace. V kurzu [Přidání sloupce gridviewu pro zaškrtávací políčko](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb.md) jsme vytvořili prvek GridView se sloupcem CheckBoxes a v rámci kurzových [úprav v transakci](wrapping-database-modifications-within-a-transaction-vb.md) , vytvořili jsme metodu v knihoven BLL, která by používala transakci k odstranění `List<T>` `ProductID` hodnot. V tomto kurzu sestavíme a sloučíme naše předchozí prostředí a vytvoříme příklad odstranění funkční dávky.

[![každý řádek obsahuje zaškrtávací políčko.](batch-deleting-vb/_static/image1.gif)](batch-deleting-vb/_static/image1.png)

**Obrázek 1**: každý řádek obsahuje zaškrtávací políčko ([kliknutím zobrazíte obrázek v plné velikosti](batch-deleting-vb/_static/image2.png)).

## <a name="step-1-creating-the-batch-deleting-interface"></a>Krok 1: Vytvoření dávkového odstraňování rozhraní

Vzhledem k tomu, že jsme už vytvořili rozhraní Batch při odstraňování v kurzu pro [Přidání sloupce s popisem zaškrtávacích políček](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb.md) , můžeme ho jednoduše zkopírovat do `BatchDelete.aspx` místo toho, abyste ho vytvořili úplně od začátku. Začněte tím, že otevřete stránku `BatchDelete.aspx` ve složce `BatchData` a na stránce pro `CheckBoxField.aspx` ve složce pro `EnhancedGridView`. Na stránce `CheckBoxField.aspx` přejdete do zobrazení zdroje a nakopírujete značku mezi značkami `<asp:Content>`, jak je znázorněno na obrázku 2.

[![zkopírovat deklarativní označení třídě CheckBoxField podporována. aspx do schránky](batch-deleting-vb/_static/image2.gif)](batch-deleting-vb/_static/image3.png)

**Obrázek 2**: zkopírování deklarativní značky `CheckBoxField.aspx` do schránky ([kliknutím zobrazíte obrázek v plné velikosti](batch-deleting-vb/_static/image4.png))

V dalším kroku přejdete do zobrazení zdroj v `BatchDelete.aspx` a vložíte obsah schránky do značek `<asp:Content>`. Také zkopírujte a vložte kód z třídy kódu na pozadí v `CheckBoxField.aspx.vb` do třídy kódu na pozadí v `BatchDelete.aspx.vb` (`DeleteSelectedProducts` tlačítko s `Click` obslužné rutiny události, metoda `ToggleCheckState` a obslužné rutiny událostí `Click` pro `CheckAll` a `UncheckAll` tlačítka). Po zkopírování tohoto obsahu by třída `BatchDelete.aspx` s kódem na pozadí měla obsahovat následující kód:

[!code-vb[Main](batch-deleting-vb/samples/sample1.vb)]

Po zkopírování deklarativních značek a zdrojového kódu si počkejte, než se otestuje `BatchDelete.aspx` zobrazením přes prohlížeč. Měl by se zobrazit prvek GridView s prvním deseti produkty v prvku GridView s každým řádkem obsahujícím název produktu, kategorii a cenu spolu s zaškrtávacím políčkem. Měla by existovat tři tlačítka: zaškrtnout vše, zrušit výběr všech a odstranit vybrané produkty. Kliknutím na tlačítko pro kontrolu všech vyberete všechna zaškrtávací políčka a políčko zrušit zaškrtnutí políčka zruší všechna zaškrtnutí. Po kliknutí na Odstranit vybrané produkty se zobrazí zpráva se seznamem `ProductID` hodnot vybraných produktů, ale ve skutečnosti neodstraňují produkty.

[![rozhraní z třídě CheckBoxField podporována. aspx se přesunulo na BatchDeleting. aspx.](batch-deleting-vb/_static/image3.gif)](batch-deleting-vb/_static/image5.png)

**Obrázek 3**: rozhraní z `CheckBoxField.aspx` bylo přesunuto do `BatchDeleting.aspx` ([kliknutím zobrazíte obrázek v plné velikosti).](batch-deleting-vb/_static/image6.png)

## <a name="step-2-deleting-the-checked-products-using-transactions"></a>Krok 2: odstranění kontrolovaných produktů pomocí transakcí

Po úspěšném dokončení kopírování rozhraní Batch do `BatchDeleting.aspx`je vše beze aktualizace kódu aktualizovat, aby tlačítko Odstranit vybrané produkty odstranilo kontrolované produkty pomocí metody `DeleteProductsWithTransaction` ve třídě `ProductsBLL`. Tato metoda, která byla přidána v [rámci kurzu transakce](wrapping-database-modifications-within-a-transaction-vb.md) , se mění jako vstupní `List(Of T)` hodnot `ProductID` a odstraní všechny odpovídající `ProductID` v rámci oboru transakce.

Obslužná rutina události `Click` `DeleteSelectedProducts` v současnosti používá následující `For Each` smyčku k iterování každého řádku GridView:

[!code-vb[Main](batch-deleting-vb/samples/sample2.vb)]

Pro každý řádek je webový ovládací prvek zaškrtávací políčko `ProductSelector` programově odkazován. Pokud je zaškrtnuto, řádky `ProductID` jsou načteny z kolekce `DataKeys` a vlastnost `DeleteResults` popisku s `Text` je aktualizována tak, aby obsahovala zprávu oznamující, že byl řádek vybrán pro odstranění.

Výše uvedený kód ve skutečnosti neodstraní žádné záznamy, protože volání metody `ProductsBLL` třídy s `Delete` je zakomentováno. Tato logika odstranění se má použít, kód by tyto produkty odstranil, ale ne v atomické operaci. To znamená, že pokud několik prvních odstranění v sekvenci bylo úspěšné, ale později se nezdařila (možná z důvodu porušení omezení cizího klíče), bude vyvolána výjimka, ale tyto produkty již odstraněny by zůstaly odstraněny.

Abychom zajistili nedělitelnost, musíme místo toho použít metodu `DeleteProductsWithTransaction` `ProductsBLL` třídy s. Vzhledem k tomu, že tato metoda přijímá seznam hodnot `ProductID`, musíme nejdřív tento seznam zkompilovat z mřížky a pak ho předat jako parametr. Nejprve vytvoříme instanci `List(Of T)` typu `Integer`. V rámci smyčky `For Each` musíme do této `List(Of T)`přidat vybrané produkty `ProductID` hodnoty. Po smyčce musí být tento `List(Of T)` předán metodě `ProductsBLL` třídy s `DeleteProductsWithTransaction`. Aktualizujte obslužnou rutinu události `Click` `DeleteSelectedProducts` tlačítko s následujícím kódem:

[!code-vb[Main](batch-deleting-vb/samples/sample3.vb)]

Aktualizovaný kód vytvoří `List(Of T)` typu `Integer` (`productIDsToDelete`) a naplní jej hodnotami `ProductID`, které mají být odstraněny. Pokud je v `For Each` smyčce k dispozici alespoň jeden produkt, je volána metoda `ProductsBLL` třídy `DeleteProductsWithTransaction` a předává se tomuto seznamu. Zobrazí se také popisek `DeleteResults` a data jsou znovu svázána s ovládacím prvek GridView (aby se nově odstraněné záznamy již v mřížce nezobrazovaly jako řádky).

Obrázek 4 znázorňuje prvek GridView po výběru počtu řádků k odstranění. Obrázek 5 zobrazuje obrazovku hned po kliknutí na tlačítko Odstranit vybrané produkty. Všimněte si, že na obrázku 5 se `ProductID` hodnoty odstraněných záznamů zobrazují v popisku pod prvkem GridView a tyto řádky již nejsou v prvku GridView.

[![vybrané produkty se odstraní.](batch-deleting-vb/_static/image4.gif)](batch-deleting-vb/_static/image7.png)

**Obrázek 4**: vybrané produkty se odstraní ([kliknutím zobrazíte obrázek v plné velikosti).](batch-deleting-vb/_static/image8.png)

[![hodnoty ProductID pro odstraněné produkty jsou uvedené pod prvkem GridView.](batch-deleting-vb/_static/image5.gif)](batch-deleting-vb/_static/image9.png)

**Obrázek 5**: odstraněné produkty `ProductID` hodnoty jsou uvedeny pod prvkem GridView ([kliknutím zobrazíte obrázek v plné velikosti).](batch-deleting-vb/_static/image10.png)

> [!NOTE]
> Chcete-li otestovat nedělitelnost `DeleteProductsWithTransaction` metody s, ručně přidejte položku pro produkt v tabulce `Order Details` a pak se pokuste tento produkt odstranit (společně s ostatními). Při pokusu o odstranění produktu s přidruženým pořadím obdržíte porušení omezení cizího klíče, ale Všimněte si, jak se ostatní vybrané produkty odstraní zpátky.

## <a name="summary"></a>Souhrn

Vytvoření dávkového odstranění rozhraní zahrnuje přidání prvku GridView se sloupcem zaškrtávacích políček a webového ovládacího prvku tlačítko, který po kliknutí odstraní všechny vybrané řádky jako jedinou atomickou operaci. V tomto kurzu jsme toto rozhraní sestavili tak, aby piecing dohromady pracovali ve dvou předchozích kurzech: [Přidání sloupce GridView checkboxs](../enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb.md) a [balení úprav databáze v rámci transakce](wrapping-database-modifications-within-a-transaction-vb.md). V prvním kurzu jsme vytvořili prvek GridView se sloupcem CheckBoxes a v druhém jsme implementovali metodu v knihoven BLL, která při předání `List(Of T)` hodnot `ProductID` odstranila všechny v rámci rozsahu transakce.

V dalším kurzu vytvoříme rozhraní pro provádění dávkových vkládání.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Hilton Giesenow a Teresa Murphy. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](batch-updating-vb.md)
> [Další](batch-inserting-vb.md)

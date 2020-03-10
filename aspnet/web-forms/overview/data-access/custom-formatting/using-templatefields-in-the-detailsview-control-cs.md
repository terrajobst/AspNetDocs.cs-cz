---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-cs
title: Použití vlastností TemplateField v ovládacím prvku DetailsView (C#) | Microsoft Docs
author: rick-anderson
description: Stejné schopnosti TemplateFields, které jsou k dispozici v prvku GridView, jsou také k dispozici v ovládacím prvku DetailsView. V tomto kurzu zobrazíme jeden produkt...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 83efb21f-b231-446e-9356-f4c6cbcc6713
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 55c667800a9fb19d200bcf4b68e2c59ca4ef5d0e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78595660"
---
# <a name="using-templatefields-in-the-detailsview-control-c"></a>Použití vlastností TemplateField v ovládacím prvku DetailsView (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_13_CS.exe) nebo [Stáhnout PDF](using-templatefields-in-the-detailsview-control-cs/_static/datatutorial13cs1.pdf)

> Stejné schopnosti TemplateFields, které jsou k dispozici v prvku GridView, jsou také k dispozici v ovládacím prvku DetailsView. V tomto kurzu zobrazíme v jednom okamžiku jeden produkt pomocí ovládacího prvku DetailsView obsahujícího TemplateFields.

## <a name="introduction"></a>Úvod

TemplateField nabízí vyšší míru flexibility při vykreslování dat než vlastnost BoundField, třídě CheckBoxField podporována, HyperLinkField a další ovládací prvky datových polí. V [předchozím kurzu](using-templatefields-in-the-gridview-control-cs.md) jsme se vyhledali pomocí pole TemplateField v prvku GridView:

- Zobrazí více hodnot datových polí v jednom sloupci. Konkrétně pole `FirstName` i `LastName` byla sloučena do jednoho sloupce GridView.
- Pomocí alternativního webového ovládacího prvku vyjádřete hodnotu datového pole. Zjistili jsme, jak zobrazit `HiredDate` hodnotu pomocí ovládacího prvku kalendáře.
- Zobrazí informace o stavu na základě podkladových dat. I když tabulka `Employees` neobsahuje sloupec, který vrací počet dní, po který zaměstnanec v úloze pracoval, mohli bychom tyto informace zobrazit v příkladu GridView v předchozím kurzu s použitím metody TemplateField a Formatting.

Stejné schopnosti TemplateFields, které jsou k dispozici v prvku GridView, jsou také k dispozici v ovládacím prvku DetailsView. V tomto kurzu zobrazíme v jednom okamžiku jeden produkt pomocí ovládacího prvku DetailsView, který obsahuje dvě TemplateFields. První TemplateField bude kombinovat datová pole `UnitPrice`, `UnitsInStock`a `UnitsOnOrder` do jednoho řádku DetailsView. Druhý objekt TemplateField zobrazí hodnotu pole `Discontinued`, ale použije metodu formátování k zobrazení hodnoty "Ano", pokud `Discontinued` je `true`a "ne" jinak.

[k přizpůsobení zobrazení slouží ![dvou TemplateField.](using-templatefields-in-the-detailsview-control-cs/_static/image2.png)](using-templatefields-in-the-detailsview-control-cs/_static/image1.png)

**Obrázek 1**: k přizpůsobení zobrazení slouží dvě pole TemplateField ([kliknutím zobrazíte obrázek v plné velikosti](using-templatefields-in-the-detailsview-control-cs/_static/image3.png)).

Pojďme začít!

## <a name="step-1-binding-the-data-to-the-detailsview"></a>Krok 1: svázání dat s ovládacím prvekem DetailsView

Jak je popsáno v předchozím kurzu, když pracujete s TemplateField, je často nejjednodušší začít vytvořením ovládacího prvku DetailsView, který obsahuje pouze BoundFields a pak přidejte nové TemplateFields nebo převeďte existující BoundFields na TemplateFields, jak je potřeba. . Proto spusťte tento kurz přidáním prvku DetailsView na stránku pomocí návrháře a vytvořte vazbu na prvek ObjectDataSource, který vrátí seznam produktů. Tyto kroky vytvoří prvek DetailsView s BoundFields pro každé pole nelogické hodnoty produktu a třídě CheckBoxField podporována pro pole s jedním logickým hodnotou (ukončeno).

Otevřete stránku `DetailsViewTemplateField.aspx` a přetáhněte prvek DetailsView z panelu nástrojů na Návrhář. Z inteligentní značky prvku DetailsView vyberte, chcete-li přidat nový ovládací prvek ObjectDataSource, který vyvolá metodu `GetProducts()` `ProductsBLL` třídy.

[![přidat nový ovládací prvek ObjectDataSource, který vyvolá metodu GetProducts ()](using-templatefields-in-the-detailsview-control-cs/_static/image5.png)](using-templatefields-in-the-detailsview-control-cs/_static/image4.png)

**Obrázek 2**: Přidání nového ovládacího prvku ObjectDataSource, který vyvolá metodu `GetProducts()` ([kliknutím zobrazíte obrázek v plné velikosti](using-templatefields-in-the-detailsview-control-cs/_static/image6.png))

Pro tuto sestavu odeberte `ProductID`, `SupplierID`, `CategoryID`a `ReorderLevel` BoundFields. Dále přeuspořádat BoundFields, aby se `CategoryName` a `SupplierName` BoundFields hned za `ProductName` vlastnost BoundField. Nebojte se upravit vlastnosti `HeaderText` a vlastnosti formátování BoundFields podle svých potřeb. Podobně jako u prvku GridView lze tyto úpravy na úrovni vlastnost BoundField provádět pomocí dialogového okna pole (přístupné kliknutím na odkaz upravit pole v inteligentní značce ovládacího prvku DetailsView) nebo prostřednictvím deklarativní syntaxe. Nakonec vymažte hodnoty vlastností `Height` ovládacího prvku DetailsView a `Width`, aby se ovládací prvek DetailsView mohl rozšířit na základě zobrazených dat, a zaškrtněte políčko Povolit stránkování v inteligentní značce.

Po provedení těchto změn by deklarativní označení ovládacího prvku DetailsView mělo vypadat podobně jako následující:

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample1.aspx)]

Chvíli si zobrazte stránku v prohlížeči. V tomto okamžiku byste měli vidět jeden produkt uvedený (Chai) s řádky, které zobrazují název produktu, kategorii, dodavatele, cenu, jednotky na skladě, jednotky v objednávce a stav zastaveno.

[![se podrobnosti o produktu zobrazují pomocí řady BoundFields](using-templatefields-in-the-detailsview-control-cs/_static/image8.png)](using-templatefields-in-the-detailsview-control-cs/_static/image7.png)

**Obrázek 3**: podrobnosti o produktu se zobrazují s použitím řady BoundFields ([kliknutím zobrazíte obrázek v plné velikosti).](using-templatefields-in-the-detailsview-control-cs/_static/image9.png)

## <a name="step-2-combining-the-price-units-in-stock-and-units-on-order-into-one-row"></a>Krok 2: kombinování ceny, jednotek v zásobách a jednotek v pořadí do jednoho řádku

Prvek DetailsView obsahuje řádek pro pole `UnitPrice`, `UnitsInStock`a `UnitsOnOrder`. Tato datová pole můžeme zkombinovat do jednoho řádku s vlastností TemplateField buď přidáním nové TemplateField nebo převodem jednoho z existujících `UnitPrice`, `UnitsInStock`a `UnitsOnOrder` BoundFields na TemplateField. I když mám přednost při konverzi stávajících BoundFields, řekněme, že přidáte nové TemplateField.

Začněte tím, že kliknete na odkaz upravit pole v inteligentní značce DetailsView a zobrazí se dialogové okno pole. Dále přidejte nové pole TemplateField a nastavte jeho vlastnost `HeaderText` na "Price and Inventory" a přesuňte novou hodnotu TemplateField, aby byla umístěna nad `UnitPrice` vlastnost BoundField.

[![přidat nové pole TemplateField do ovládacího prvku DetailsView](using-templatefields-in-the-detailsview-control-cs/_static/image11.png)](using-templatefields-in-the-detailsview-control-cs/_static/image10.png)

**Obrázek 4**: přidejte nové pole TemplateField k ovládacímu prvku DetailsView ([kliknutím zobrazíte obrázek v plné velikosti](using-templatefields-in-the-detailsview-control-cs/_static/image12.png)).

Vzhledem k tomu, že tato nová TemplateField bude obsahovat hodnoty, které jsou aktuálně zobrazeny v `UnitPrice`, `UnitsInStock`a `UnitsOnOrder` BoundFields, pojďme je odebrat.

Poslední úlohou pro tento krok je definování `ItemTemplate` označení pro pole pro cenu a inventarizaci, které lze provést buď prostřednictvím rozhraní pro úpravu šablony ovládacího prvku DetailsView v Návrháři nebo ručně prostřednictvím deklarativní syntaxe ovládacího prvku. Stejně jako u prvku GridView, rozhraní pro úpravu šablony ovládacího prvku DetailsView lze použít kliknutím na odkaz Upravit šablony v inteligentní značce. Odsud můžete v rozevíracím seznamu vybrat šablonu, kterou chcete upravit, a pak přidat libovolné webové ovládací prvky ze sady nástrojů.

V tomto kurzu Začněte přidáním ovládacího prvku popisek k `ItemTemplate`cen a zásob TemplateField. Potom klikněte na odkaz Upravit datové vazby z inteligentní značky popisek webového ovládacího prvku a navažte vlastnost `Text` na pole `UnitPrice`.

[![navazovat vlastnost text popisku na datové pole UnitPrice.](using-templatefields-in-the-detailsview-control-cs/_static/image14.png)](using-templatefields-in-the-detailsview-control-cs/_static/image13.png)

**Obrázek 5**: vazba vlastnosti `Text` popisku na datové pole `UnitPrice` ([kliknutím zobrazíte obrázek v plné velikosti](using-templatefields-in-the-detailsview-control-cs/_static/image15.png))

## <a name="formatting-the-price-as-a-currency"></a>Formátování ceny jako měny

S tímto sčítáním se teď v popisku a v poli TemplateField Web Control Price a Inventory zobrazí jenom cena za vybraný produkt. Obrázek 6 zobrazuje snímek obrazovky s průběžným průběhem při prohlížení v prohlížeči.

[![poli Price a Inventory se zobrazí cena.](using-templatefields-in-the-detailsview-control-cs/_static/image17.png)](using-templatefields-in-the-detailsview-control-cs/_static/image16.png)

**Obrázek 6: hodnota**TemplateField ceny a inventarizace zobrazuje cenu ([kliknutím zobrazíte obrázek v plné velikosti).](using-templatefields-in-the-detailsview-control-cs/_static/image18.png)

Všimněte si, že cena produktu není naformátovaná jako měna. Vlastnost BoundField je možné formátování nastavením vlastnosti `HtmlEncode` na `false` a vlastností `DataFormatString` na `{0:formatSpecifier}`. U třídy TemplateField však musí být všechny instrukce formátování specifikovány v syntaxi DataBinding nebo pomocí metody formátování definované někde v rámci kódu aplikace (například ve třídě kódu na pozadí stránky ASP.NET).

Chcete-li určit formátování syntaxe datové vazby použité ve webovém ovládacím prvku popisek, vraťte se do dialogového okna datové vazby kliknutím na odkaz Upravit datové vazby z inteligentní značky popisku. Pokyny pro formátování můžete zadat přímo v rozevíracím seznamu formát nebo vyberte jeden z definovaných formátovacích řetězců. Podobně jako u vlastnosti `DataFormatString` vlastnost BoundField je formátování zadáno pomocí `{0:formatSpecifier}`.

V poli `UnitPrice` použijte formátování měny zadané buď výběrem příslušné hodnoty rozevíracího seznamu, nebo zadáním `{0:C}` ruky.

[![formátovat cenu jako měnu](using-templatefields-in-the-detailsview-control-cs/_static/image20.png)](using-templatefields-in-the-detailsview-control-cs/_static/image19.png)

**Obrázek 7**: naformátování ceny jako měny ([kliknutím zobrazíte obrázek v plné velikosti](using-templatefields-in-the-detailsview-control-cs/_static/image21.png))

Deklarativně je specifikace formátování označena jako druhý parametr do `Bind` nebo `Eval`ch metod. Nastavení provedené prostřednictvím návrháře má za následek následující výraz datové vazby v deklarativní značce:

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample2.aspx)]

## <a name="adding-the-remaining-data-fields-to-the-templatefield"></a>Přidání zbývajících datových polí do TemplateField

V tuto chvíli jsme zobrazili a naformátovali `UnitPrice` datové pole v poli TemplateField (Price and Inventory), ale stále je potřeba zobrazit pole `UnitsInStock` a `UnitsOnOrder`. Pojďme je zobrazit na řádku pod cenou a v závorkách. V rozhraní pro úpravy šablony v Návrháři lze takové značky přidat umístěním kurzoru v rámci šablony a pouhým zadáním textu, který se má zobrazit. Alternativně lze tento kód zadat přímo v deklarativní syntaxi.

Přidejte statické značky, webové ovládací prvky popisků a syntaxi datových vazeb tak, aby pole Price a Inventory TemplateField zobrazila informace o cenách a inventáři, například:

*JednotkováCena*  
(**V zásobách/v pořadí:** *JednotkyNaSkladě* / *ObjednánoJednotek*)

Po provedení tohoto úkolu by deklarativní označení ovládacího prvku DetailsView mělo vypadat podobně jako následující:

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample3.aspx)]

Tyto změny konsolidujeme informace o cenách a inventáři do jednoho řádku DetailsView.

[![informace o cenách a inventáři se zobrazí na jednom řádku.](using-templatefields-in-the-detailsview-control-cs/_static/image23.png)](using-templatefields-in-the-detailsview-control-cs/_static/image22.png)

**Obrázek 8**: informace o cenách a inventáři se zobrazí v jednom řádku ([kliknutím zobrazíte obrázek v plné velikosti).](using-templatefields-in-the-detailsview-control-cs/_static/image24.png)

## <a name="step-3-customizing-the-discontinued-field-information"></a>Krok 3: přizpůsobení informací o vyřazeném poli

Sloupec `Discontinued` `Products` tabulky je bitová hodnota, která označuje, jestli byl produkt vyřazený. Při vázání prvku DetailsView (nebo GridView) na ovládací prvek zdroje dat jsou pole logických hodnot, například `Discontinued`, implementována jako CheckBoxFields, zatímco pole nelogické hodnoty, jako je `ProductID`, `ProductName`a tak dále, jsou implementována jako BoundFields. Třídě CheckBoxField podporována vykreslí jako zakázané zaškrtávací políčko, které je zaškrtnuto, pokud je hodnota datového pole true a není zaškrtnuto jinak.

Místo toho, abyste zobrazili třídě CheckBoxField podporována, můžeme místo toho chtít zobrazit text, který indikuje, jestli je produkt vyřazený. K tomuto účelu můžeme odebrat třídě CheckBoxField podporována z prvku DetailsView a pak přidat vlastnost BoundField, jehož vlastnost `DataField` byla nastavena na hodnotu `Discontinued`. Udělejte to chvilku. Po této změně DetailsView zobrazí text "true" pro zastavené produkty a "false" pro produkty, které jsou stále aktivní.

[![se řetězce true a false slouží k zobrazení stavu Zastaveno.](using-templatefields-in-the-detailsview-control-cs/_static/image26.png)](using-templatefields-in-the-detailsview-control-cs/_static/image25.png)

**Obrázek 9**: pomocí řetězců true a false se zobrazuje stav zastaveno ([kliknutím zobrazíte obrázek v plné velikosti](using-templatefields-in-the-detailsview-control-cs/_static/image27.png)).

Představte si, že nechcete použít řetězce "true" nebo "false", ale místo toho "Ano" a "ne". Takové přizpůsobení lze provést s podporou TemplateField a formátovací metodou. Metoda formátování může přebírat libovolný počet vstupních parametrů, ale musí vracet kód HTML (jako řetězec), který se má vložit do šablony.

Přidejte metodu formátování do třídy kódu na pozadí `DetailsViewTemplateField.aspx` stránky s názvem `DisplayDiscontinuedAsYESorNO`, která přijímá jako vstupní parametr logickou hodnotu a vrátí řetězec. Jak je popsáno v předchozím kurzu, tato metoda *musí* být označena jako `protected` nebo `public`, aby mohla být přístupná ze šablony.

[!code-csharp[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample4.cs)]

Tato metoda zkontroluje vstupní parametr (`discontinued`) a vrátí "Ano", pokud je `true`, "ne" jinak.

> [!NOTE]
> V metodě formátování zkoumané v předchozím kurzu se odvolá, že jsme prošli datovým polem, které může obsahovat `NULL` s, a proto je potřeba zkontrolovat, jestli hodnota vlastnosti `HiredDate` zaměstnance měla `NULL` hodnotu databáze před přístupem k `HiredDate` vlastnosti `EmployeesRow`. Tato kontrolu tady není potřeba, protože `Discontinued` sloupec nemůže nikdy mít přiřazené hodnoty `NULL` databáze. Kromě toho je proto možné, že metoda může přijmout logický vstupní parametr namísto nutnosti přijmout instanci `ProductsRow` nebo parametr typu `object`.

Když je tato metoda formátování dokončena, vše zůstává je volat z `ItemTemplate`TemplateField. Chcete-li vytvořit TemplateField, buď odeberte `Discontinued` vlastnost BoundField a přidejte nové TemplateField nebo převeďte `Discontinued` vlastnost BoundField na TemplateField. Pak z deklarativního zobrazení značek upravte pole TemplateField tak, aby obsahovalo pouze hodnotu ItemTemplate, která vyvolá metodu `DisplayDiscontinuedAsYESorNO` a předává hodnotu vlastnosti `Discontinued` aktuální `ProductRow` instance. K tomu je možné přistupovat prostřednictvím metody `Eval`. Konkrétně by značky TemplateField měly vypadat takto:

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-cs/samples/sample5.aspx)]

Tím dojde k vyvolání metody `DisplayDiscontinuedAsYESorNO` při vykreslování ovládacího prvku DetailsView a předání hodnoty `Discontinued` `ProductRow` instance. Vzhledem k tomu, že metoda `Eval` vrací hodnotu typu `object`, ale metoda `DisplayDiscontinuedAsYESorNO` očekává vstupní parametr typu `bool`, přetypování návratové hodnoty metody `Eval` na `bool`. Metoda `DisplayDiscontinuedAsYESorNO` pak vrátí "YES" nebo "NO" v závislosti na hodnotě, kterou přijímá. Vrácená hodnota je zobrazená v tomto řádku DetailsView (viz obrázek 10).

[![Ano nebo žádné hodnoty nejsou nyní zobrazeny v řádku ukončeno.](using-templatefields-in-the-detailsview-control-cs/_static/image29.png)](using-templatefields-in-the-detailsview-control-cs/_static/image28.png)

**Obrázek 10**: Ano nebo žádné hodnoty se nyní zobrazují v neukončeném řádku ([kliknutím zobrazíte obrázek v plné velikosti).](using-templatefields-in-the-detailsview-control-cs/_static/image30.png)

## <a name="summary"></a>Souhrn

Pole TemplateField v ovládacím prvku DetailsView umožňuje vyšší míru flexibility při zobrazování dat, než je k dispozici v jiných ovládacích prvcích pole a jsou ideální pro situace, kde:

- V jednom sloupci GridView se musí zobrazit víc datových polí.
- Data se nejlépe vyjadřují pomocí webového ovládacího prvku místo prostého textu.
- Výstup závisí na podkladových datech, jako je například zobrazení metadat nebo přeformátování dat.

I když TemplateField umožňují větší flexibilitu při vykreslování podkladových dat ovládacího prvku DetailsView, výstup ovládacího prvku DetailsView ještě nemění bitovou boxyi, když je každé pole vykresleno jako řádek ve formátu HTML `<table>`.

Ovládací prvek FormView nabízí větší stupeň flexibility při konfiguraci vykresleného výstupu. Třída FormView neobsahuje pole, ale ne pouze řadu šablon (`ItemTemplate`, `EditItemTemplate`, `HeaderTemplate`a tak dále). Podíváme se, jak použít FormView k dosažení ještě větší kontroly nad vykresleným rozložením v našem dalším kurzu.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor potenciálních zákazníků pro tento kurz byl Dan Jagers. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](using-templatefields-in-the-gridview-control-cs.md)
> [Další](using-the-formview-s-templates-cs.md)

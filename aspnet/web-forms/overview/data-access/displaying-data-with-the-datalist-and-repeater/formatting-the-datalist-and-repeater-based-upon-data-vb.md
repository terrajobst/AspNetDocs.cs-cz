---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-vb
title: Formátování prvku DataList a Repeater na základě dat (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu budeme postupovat podle příkladů formátování vzhledu ovládacích prvků DataList a Repeater, a to buď pomocí funkcí formátování s...
ms.author: riande
ms.date: 09/13/2006
ms.assetid: e2f401ae-37bb-4b19-aa97-d6b385d40f88
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-vb
msc.type: authoredcontent
ms.openlocfilehash: c9b60e4dacd992962942034e84c01cb82e039c81
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78626278"
---
# <a name="formatting-the-datalist-and-repeater-based-upon-data-vb"></a>Formátování ovládacích prvků DataList a Repeater na základě dat (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_30_VB.exe) nebo [Stáhnout PDF](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/datatutorial30vb1.pdf)

> V tomto kurzu si projdeme příklady, jak naformátovat vzhled ovládacích prvků DataList a Repeater, a to buď pomocí funkcí formátování v rámci šablon, nebo pomocí zpracování události DataBound.

## <a name="introduction"></a>Úvod

Jak jsme viděli v předchozím kurzu, DataList nabízí řadu vlastností souvisejících s Style, které mají vliv na jeho vzhled. Konkrétně jsme viděli, jak přiřadit výchozí třídy CSS k vlastnostem DataList s `HeaderStyle`, `ItemStyle`, `AlternatingItemStyle`a `SelectedItemStyle`. Kromě těchto čtyř vlastností prvek DataList zahrnuje řadu dalších vlastností souvisejících s Style, například `Font`, `ForeColor`, `BackColor`a `BorderWidth`pro pojmenování několika. Ovládací prvek Repeater neobsahuje žádné vlastnosti související s Style. Jakékoli takové nastavení stylu musí být provedeno přímo v rámci značky v šablonách Repeater.

Často ale, jak mají být data naformátovaná, závisí na samotných datech. Například při výpisu produktů může být vhodné zobrazit informace o produktech v barvě šedé barvy písma, pokud je přerušit, nebo můžete chtít zvýraznit `UnitsInStock` hodnotu, pokud je nula. Jak jsme viděli v předchozích kurzech, GridView, DetailsView a FormView nabízí dva různé způsoby formátování jejich vzhledu na základě jejich dat:

- **Událost `DataBound`** vytvoří obslužnou rutinu události pro příslušnou událost `DataBound`, která se aktivuje poté, co byla data svázána s každou položkou (pro ovládací prvek GridView, že se jednalo o událost `RowDataBound`; u prvku DataList a v případě opakování je `ItemDataBound` událost). V této obslužné rutině události lze pouze prověřit data a naformátovat provedené rozhodnutí. Tuto techniku jsme zkoumali ve [vlastním formátování na základě kurzu dat](../custom-formatting/custom-formatting-based-upon-data-vb.md) .
- **Formátování funkcí v šablonách** při použití vlastností TemplateField v ovládacím prvku DetailsView nebo GridView nebo šabloně v ovládacím prvku FormView můžeme přidat funkci formátování do třídy ASP.NET stránky s kódem na pozadí, vrstvy obchodní logiky nebo jakékoli jiné knihovny tříd, která je přístupná z webové aplikace. Tato funkce formátování může přijmout libovolný počet vstupních parametrů, ale musí vrátit kód HTML, který se má vykreslit v šabloně. Funkce formátování byly nejprve přezkoumány v kurzu [použití templatefields v ovládacím prvku GridView](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) .

Obě tyto techniky formátování jsou k dispozici společně s ovládacími prvky DataList a Repeater. V tomto kurzu budeme procházet příklady pomocí obou postupů pro oba ovládací prvky.

## <a name="using-theitemdataboundevent-handler"></a>Použití obslužné rutiny události`ItemDataBound`

Když jsou data svázána s ovládacím prvkem DataList, buď z ovládacího prvku zdroje dat, nebo prostřednictvím programově přiřazují data do vlastnosti `DataSource` ovládacího prvku a voláním jeho metody `DataBind()`, aktivuje se událost DataList s `DataBinding`, zdroj dat se zobrazí ve výčtu a každý datový záznam je svázán s prvkem DataList. Pro každý záznam ve zdroji dat vytvoří prvek DataList objekt [`DataListItem`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistitem.aspx) , který je následně svázán s aktuálním záznamem. Během tohoto procesu DataList vyvolá dvě události:

- **`ItemCreated`** aktivovaná po vytvoření `DataListItem`
- **`ItemDataBound`** aktivuje se po vazbě aktuálního záznamu na `DataListItem`

Následující kroky popisují proces vytváření datových vazeb pro ovládací prvek DataList.

1. [Událost`DataBinding`](https://msdn.microsoft.com/library/system.web.ui.control.databinding.aspx) DataList se aktivuje.
2. Data jsou svázána s ovládacím prvky DataList  
  
   Pro každý záznam ve zdroji dat 

    1. Vytvoření objektu `DataListItem`
    2. Vyvolat [událost`ItemCreated`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.itemcreated.aspx)
    3. Navázání záznamu na `DataListItem`
    4. Vyvolat [událost`ItemDataBound`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.itemdatabound.aspx)
    5. Přidání `DataListItem` do kolekce `Items`

Při vázání dat k ovládacímu prvku Repeater postupuje přes přesně stejné pořadí kroků. Jediným rozdílem je, že se místo vytvoření instancí `DataListItem` používá Repeater [`RepeaterItem`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeateritem(VS.80).aspx)s.

> [!NOTE]
> Čtečka bystří mohla zaznamenat mírnou anomálii mezi sekvencí kroků, které se zobrazí, když jsou prvky DataList a Repeater svázány s daty versus při vázání prvku GridView na data. Na konci procesu vytváření datových vazeb prvek GridView Vyvolá událost `DataBound`; Nicméně ovládací prvek DataList ani Repeater takové události neexistují. Důvodem je to, že ovládací prvky DataList a Repeater byly vytvořeny zpátky v časovém limitu ASP.NET 1. x před tím, než se vzorek obslužné rutiny události před a po úrovni stala běžným.

Podobně jako u prvku GridView, jedna možnost pro formátování na základě dat je vytvořit obslužnou rutinu události pro událost `ItemDataBound`. Tato obslužná rutina události by zkontrolovala data, která byla právě svázána s `DataListItem` nebo `RepeaterItem` a mají vliv na formátování ovládacího prvku podle potřeby.

U ovládacího prvku DataList lze formátování změn pro celou položku implementovat pomocí vlastností souvisejících s `DataListItem` s, které zahrnují standardní `Font`, `ForeColor`, `BackColor`, `CssClass`a tak dále. Abychom ovlivnili formátování konkrétního webového ovládacího prvku v rámci šablony DataList s, potřebujeme programově přistupovat k těmto webovým ovládacím prvkům a upravovat jejich styly. Zjistili jsme, jak to udělat zpátky ve *vlastním formátování na základě kurzu dat* . Stejně jako ovládací prvek Repeater, třída `RepeaterItem` nemá žádné vlastnosti související se styly; Proto všechny změny stylu související se stylem `RepeaterItem` v obslužné rutině události `ItemDataBound` musí být provedeny programově při přístupu k webovým ovládacím prvkům a jejich aktualizace v rámci šablony.

Vzhledem k tomu, že je způsob formátování `ItemDataBound` pro prvky DataList a Repeat prakticky identický, náš příklad se soustředí na použití prvku DataList.

## <a name="step-1-displaying-product-information-in-the-datalist"></a>Krok 1: zobrazení informací o produktu v prvku DataList

Než se obáváme formátování, nechte nejdřív vytvořit stránku, která používá DataList k zobrazení informací o produktu. V [předchozím kurzu](displaying-data-with-the-datalist-and-repeater-controls-vb.md) jsme vytvořili prvek DataList, jehož `ItemTemplate` zobrazuje každý název produktu, kategorii, dodavatele, množství na jednotku a cenu. Tuto funkci teď můžete opakovat v tomto kurzu. K tomuto účelu můžete buď znovu vytvořit DataList a jeho prvek ObjectDataSource od začátku, nebo můžete zkopírovat tyto ovládací prvky ze stránky vytvořené v předchozím kurzu (`Basics.aspx`) a vložit je na stránku tohoto kurzu (`Formatting.aspx`).

Po replikaci funkcí DataList a ObjectDataSource z `Basics.aspx` do `Formatting.aspx`chvíli počkejte, aby se změnila vlastnost `ID` prvku DataList s `DataList1` na výstižnější `ItemDataBoundFormattingExample`. Dále Zobrazte prvek DataList v prohlížeči. Jak ukazuje obrázek 1, jediný rozdíl formátování mezi jednotlivými produkty je to, že barvy pozadí se liší.

[![jsou produkty uvedeny v ovládacím prvku DataList](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image2.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image1.png)

**Obrázek 1**: produkty jsou uvedeny v ovládacím prvku DataList ([kliknutím zobrazíte obrázek v plné velikosti](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image3.png)).

Pro tento kurz si naformátujte prvek DataList tak, že všechny produkty s cenou menší než $20,00 budou mít název a bude zvýrazněna žlutá cena.

## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-itemdatabound-event-handler"></a>Krok 2: určení hodnoty dat v obslužné rutině události ItemDataBound prostřednictvím kódu programu

Vzhledem k tomu, že se vlastní formátování používá jenom u produktů s cenou $20,00, musí být schopné určit každou cenu produktu. Při vázání dat k prvku DataList vytvoří prvek DataList záznamy ve zdroji dat a pro každý záznam vytvoří instanci `DataListItem` a naváže záznam zdroje dat k `DataListItem`. Po vazbě konkrétního záznamu s objektem `DataListItem` je vyvolána událost DataList s `ItemDataBound`. Pro tuto událost můžeme vytvořit obslužnou rutinu události pro kontrolu hodnot dat pro aktuální `DataListItem` a na základě těchto hodnot udělat změny formátování, které jsou potřeba.

Vytvořte událost `ItemDataBound` pro prvek DataList a přidejte následující kód:

[!code-vb[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample1.vb)]

I když je koncept a sémantika v rámci obslužné rutiny události `ItemDataBound` DataList, stejná jako ta, kterou používá obslužná rutina události `RowDataBound` GridView s, ve *vlastním formátování na základě kurzu dat* , syntaxe se mírně liší. Při aktivaci události `ItemDataBound` je `DataListItem` pouze vázaný na data předána do odpovídající obslužné rutiny události prostřednictvím `e.Item` (namísto `e.Row`, jako u obslužné rutiny události prvku GridView s `RowDataBound`). Obslužná rutina události `ItemDataBound` DataList se aktivuje pro *každý* řádek přidaný do prvku DataList, včetně řádků záhlaví, řádků zápatí a oddělovacích řádků. Informace o produktu jsou však vázány pouze na řádky dat. Proto při použití události `ItemDataBound` ke kontrole dat vázaných na prvek DataList musíme nejdřív zkontrolovat, že budeme znovu pracovat s datovou položkou. Můžete to provést tak, že zkontrolujete [vlastnost`ItemType`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistitem.itemtype.aspx)`DataListItem` s, která může mít jednu z [následujících osmi hodnot](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listitemtype.aspx):

- `AlternatingItem`
- `EditItem`
- `Footer`
- `Header`
- `Item`
- `Pager`
- `SelectedItem`
- `Separator`

`Item` i `AlternatingItem``DataListItem` s strukturu datové položky DataList s. Za předpokladu, že provedeme `Item` nebo `AlternatingItem`, přistupujeme ke skutečné instanci `ProductsRow`, která byla svázána s aktuálním `DataListItem`. Vlastnost `DataListItem` s [`DataItem`](https://msdn.microsoft.com/system.web.ui.webcontrols.datalistitem.dataitem.aspx) obsahuje odkaz na objekt `DataRowView`, jehož vlastnost `Row` poskytuje odkaz na skutečný objekt `ProductsRow`.

Potom zkontrolujeme vlastnost `ProductsRow` instance s `UnitPrice`. Vzhledem k tomu, že pole `UnitPrice` tabulky produktů umožňuje `NULL` hodnoty, před pokusem o přístup k vlastnosti `UnitPrice` byste nejprve měli zjistit, zda má `NULL` hodnotu pomocí metody `IsUnitPriceNull()`. Pokud hodnota `UnitPrice` není `NULL`, zkontrolujeme, jestli je méně než $20,00. Pokud je to ve skutečnosti $20,00, je nutné použít vlastní formátování.

## <a name="step-3-highlighting-the-product-s-name-and-price"></a>Krok 3: zvýraznění názvu a ceny produktu

Jakmile zjistíte, že cena za produkt je menší než $20,00, vše zůstává pro zdůraznění jejího názvu a ceny. Abychom to mohli udělat, musíte nejdřív programově odkazovat na ovládací prvky popisku v `ItemTemplate`, které zobrazují název a cenu produktu. V dalším kroku je potřeba, aby se zobrazila žlutá pozadí. Tyto informace o formátování lze použít přímou úpravou popisků `BackColor` vlastností (`LabelID.BackColor = Color.Yellow`); v ideálním případě by se měly všechny otázky související s displejem vyjádřit prostřednictvím kaskádových šablon stylů. Ve skutečnosti už máme šablonu stylů, která poskytuje požadované formátování definované v `Styles.css` - `AffordablePriceEmphasis`, která byla vytvořena a diskutována ve *vlastním formátování na základě kurzu data* .

Chcete-li použít formátování, jednoduše nastavte ovládací prvky pro dva popisky `CssClass` vlastnosti na `AffordablePriceEmphasis`, jak je znázorněno v následujícím kódu:

[!code-vb[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample2.vb)]

Po dokončení obslužné rutiny události `ItemDataBound` znovu navštivte stránku `Formatting.aspx` v prohlížeči. Jak ukazuje obrázek 2, tyto produkty s cenou v $20,00 mají své jméno i cenu zvýrazněnou.

[![jsou tyto produkty méně než $20,00 zvýrazněny.](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image5.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image4.png)

**Obrázek 2**: zvýrazní se tyto produkty menší než $20,00 ([kliknutím zobrazíte obrázek v plné velikosti).](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image6.png)

> [!NOTE]
> Vzhledem k tomu, že je prvek DataList vykreslen jako `<table>`HTML, mají jeho `DataListItem` instance vlastnosti související se styly, které lze nastavit tak, aby pro celou položku použili konkrétní styl. Pokud jsme například chtěli zdůraznit *celou* položku žlutou, pokud její cena byla menší než $20,00, mohli bychom nahradit kód, na který odkazuje popisky, a nastavit jejich `CssClass` vlastnosti pomocí následujícího řádku kódu: `e.Item.CssClass = "AffordablePriceEmphasis"` (viz obrázek 3).

`RepeaterItem` s, které tvoří ovládací prvek Repeater, ale nenabízejí takové vlastnosti na úrovni stylu. Proto použití vlastního formátování na Repeater vyžaduje použití vlastností stylu pro webové ovládací prvky v rámci šablon Repeater, stejně jako na obrázku 2.

[![je pro produkty pod položkou $20,00 zvýrazněna celá položka produktu](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image8.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image7.png)

**Obrázek 3**: pro produkty pod $20,00 se zvýrazní celá položka produktu ([kliknutím zobrazíte obrázek v plné velikosti).](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image9.png)

## <a name="using-formatting-functions-from-within-the-template"></a>Použití funkcí formátování v rámci šablony

V kurzu *použití templatefields v kurzu ovládacího prvku GridView* jsme viděli, jak použít funkci formátování v rámci prvku GridView TemplateField k použití vlastního formátování na základě dat svázaných s řádky GridView. Funkce formátování je metoda, kterou lze vyvolat ze šablony a vrátí kód HTML, který má být vygenerován na svém místě. Funkce formátování se mohou nacházet ve třídě ASP.NET stránky s kódem na pozadí nebo může být centralizovaná do souborů třídy ve složce `App_Code` nebo v samostatném projektu knihovny tříd. Přesunutí funkce formátování mimo třídu ASP.NET stránky s kódem na pozadí je ideální, pokud plánujete použití stejné funkce formátování na více stránkách ASP.NET nebo v jiných ASP.NET webových aplikacích.

Aby bylo možné předvést funkce formátování, obsahují informace o produktu text [UKONČENo] vedle názvu produktu, pokud je ukončen. Také je možné nechat zvýrazněnou cenu žlutou, pokud je menší než $20,00 (jako v příkladu obslužné rutiny události `ItemDataBound`). Pokud je cena $20,00 nebo vyšší, nezobrazuje se vám skutečná cena, ale místo toho je třeba zavolat na cenovou nabídku. Obrázek 4 znázorňuje snímek obrazovky se seznamem produktů, u kterých se tato pravidla formátování aplikují.

[![u drahých produktů se cena nahradí textem, zavolá se na cenovou nabídku.](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image11.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image10.png)

**Obrázek 4**: u drahých produktů je cena nahrazena textem, volá se za cenu nabídky ([kliknutím zobrazíte obrázek v plné velikosti).](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image12.png)

## <a name="step-1-create-the-formatting-functions"></a>Krok 1: vytvoření funkcí formátování

V tomto příkladu potřebujeme dvě funkce formátování, jednu, která zobrazuje název produktu spolu s textem [UKONČENo], pokud je to potřeba, a další, který zobrazí zvýrazněnou cenu, pokud je menší než $20,00, nebo text, zavolejte na cenovou nabídku jinak. Umožňuje vytvořit tyto funkce ve třídě ASP.NET stránky s kódem na pozadí a pojmenovat je `DisplayProductNameAndDiscontinuedStatus` a `DisplayPrice`. Obě metody musí vrátit kód HTML, který se má vykreslit jako řetězec, a obě musí být označené jako `Protected` (nebo `Public`), aby je bylo možné vyvolat z části s deklarativní syntaxí stránky ASP.NET Page. Kód těchto dvou metod je následující:

[!code-vb[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample3.vb)]

Všimněte si, že metoda `DisplayProductNameAndDiscontinuedStatus` přijímá hodnoty datových polí `productName` a `discontinued` jako skalární hodnoty, zatímco metoda `DisplayPrice` akceptuje `ProductsRow` instanci (spíše než `unitPrice` skalární hodnota). Bude fungovat buď přístup. Pokud však funkce formátování pracuje se skalárními hodnotami, které mohou obsahovat databázové `NULL` hodnoty (například `UnitPrice`; ani `ProductName` ani `Discontinued` Allow `NULL` Values), musí být při zpracování těchto skalárních vstupů provedena zvláštní péče.

Konkrétně musí být vstupní parametr typu `Object`, protože příchozí hodnota může být `DBNull` instance namísto očekávaného datového typu. Kromě toho je nutné provést kontrolu, aby bylo možné určit, zda je hodnota `NULL` databáze hodnota. To znamená, že pokud jsme chtěli, aby `DisplayPrice` metoda přijmout tuto cenu jako skalární hodnotu, je potřeba použít následující kód:

[!code-vb[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample4.vb)]

Všimněte si, že vstupní parametr `unitPrice` je typu `Object` a že došlo k úpravě podmíněného příkazu, aby bylo možné zjistit, zda `unitPrice` `DBNull` nebo nikoli. Navíc vzhledem k tomu, že vstupní parametr `unitPrice` je předán jako `Object`, musí být přetypování na desítkovou hodnotu.

## <a name="step-2-calling-the-formatting-function-from-the-datalist-s-itemtemplate"></a>Krok 2: volání funkce formátování z prvku DataList s funkcí ItemTemplate

Díky funkcím formátování přidaným do naší třídy ASP.NET stránky s kódem na pozadí vše, co zbývá, je vyvolat tyto funkce formátování z prvku DataList s `ItemTemplate`. Chcete-li volat funkci formátování ze šablony, umístěte volání funkce v rámci syntaxe datové vazby:

[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample5.aspx)]

V ovládacím prvku DataList s `ItemTemplate` webový ovládací prvek `ProductNameLabel` Label aktuálně zobrazuje název produktu přiřazením jeho vlastnosti `Text` výsledku `<%# Eval("ProductName") %>`. Aby se zobrazil název a text [UKONČENo], v případě potřeby aktualizujte deklarativní syntaxi tak, aby místo toho přiřadí vlastnost `Text` hodnotu `DisplayProductNameAndDiscontinuedStatus` metody. V takovém případě je nutné předat název produktu a ukončené hodnoty pomocí syntaxe `Eval("columnName")`. `Eval` vrací hodnotu typu `Object`, ale metoda `DisplayProductNameAndDiscontinuedStatus` očekává vstupní parametry typu `String` a `Boolean`; Proto je nutné přetypovat hodnoty vrácené metodou `Eval` na očekávané typy vstupních parametrů, například takto:

[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample6.aspx)]

Chcete-li zobrazit cenu, můžeme jednoduše nastavit vlastnost `UnitPriceLabel` popisek s `Text` na hodnotu vrácenou metodou `DisplayPrice`, stejně jako jsme provedli pro zobrazení názvu produktu a [ukončen] text. Místo předání v `UnitPrice` jako skalární vstupní parametr je však místo toho předána celá `ProductsRow` instance:

[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-vb/samples/sample7.aspx)]

Díky volání funkcí formátování si chvíli počkejte, než se zobrazí náš průběh v prohlížeči. Vaše obrazovka by měla vypadat podobně jako na obrázku 5, s vyřazenými produkty, včetně textu [VYŘAZENo], a náklady na více než $20,00, jejichž cena se nahradila textem, zavolejte na cenovou nabídku.

[![u drahých produktů se cena nahradí textem, zavolá se na cenovou nabídku.](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image14.png)](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image13.png)

**Obrázek 5**: u drahých produktů je cena nahrazena textem, volá se za cenu nabídky ([kliknutím zobrazíte obrázek v plné velikosti).](formatting-the-datalist-and-repeater-based-upon-data-vb/_static/image15.png)

## <a name="summary"></a>Souhrn

Formátování obsahu ovládacího prvku DataList nebo Repeater v závislosti na datech lze provést pomocí dvou technik. Prvním postupem je vytvořit obslužnou rutinu události pro událost `ItemDataBound`, která se aktivuje, když se každý záznam ve zdroji dat váže k novému `DataListItem` nebo `RepeaterItem`. V obslužné rutině události `ItemDataBound` lze zkontrolovat data aktuální položky, a poté lze použít formátování na obsah šablony nebo pro `DataListItem` na celou položku samotnou.

Případně lze vlastní formátování realizovat prostřednictvím funkcí formátování. Funkce formátování je metoda, kterou lze vyvolat z šablon DataList nebo Repeater s, které vrátí kód HTML pro vygenerování na svém místě. KÓD HTML vrácený funkcí formátování se často určuje podle hodnot svázaných s aktuální položkou. Tyto hodnoty lze předat do funkce formátování, buď jako skalární hodnoty, nebo předáním celého objektu vázaného na položku (například instance `ProductsRow`).

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Yaakov Ellis, Randy Schmidt a Liz Shulok. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](displaying-data-with-the-datalist-and-repeater-controls-vb.md)
> [Další](showing-multiple-records-per-row-with-the-datalist-control-vb.md)

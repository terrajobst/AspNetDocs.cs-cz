---
uid: web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-cs
title: Vlastní formátování založené na datech (C#) | Microsoft Docs
author: rick-anderson
description: Přizpůsobení formátu prvku GridView, DetailsView nebo FormView na základě dat, která jsou k němu vázána, lze provést několika způsoby. V tomto kurzu budeme l...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 871a4574-f89c-4214-b786-79253ed3653b
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-cs
msc.type: authoredcontent
ms.openlocfilehash: d8f3fa337eda0ceed041475ecb52f8b378b9fbba
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600656"
---
# <a name="custom-formatting-based-upon-data-c"></a>Vlastní formátování založené na datech (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_11_CS.exe) nebo [Stáhnout PDF](custom-formatting-based-upon-data-cs/_static/datatutorial11cs1.pdf)

> Přizpůsobení formátu prvku GridView, DetailsView nebo FormView na základě dat, která jsou k němu vázána, lze provést několika způsoby. V tomto kurzu se podíváme na to, jak provádět formátování vázané na data pomocí obslužných rutin událostí RowDataBound a DataBound.

## <a name="introduction"></a>Úvod

Vzhled ovládacích prvků GridView, DetailsView a FormView lze přizpůsobit pomocí nesčetných vlastností souvisejících s Style. Vlastnosti jako `CssClass`, `Font`, `BorderWidth`, `BorderStyle`, `BorderColor`, `Width`a `Height`, mimo jiné určují obecný vzhled vykresleného ovládacího prvku. Vlastnosti, včetně `HeaderStyle`, `RowStyle`, `AlternatingRowStyle`a dalších, umožňují použití stejných nastavení stylu pro konkrétní oddíly. Podobně lze tato nastavení stylu použít na úrovni pole.

V mnoha scénářích však požadavky na formátování závisí na hodnotě zobrazených dat. Pokud například chcete upozornit na neuložené produkty, může sestava se seznamem informací o produktu nastavit žlutou barvu pozadí pro tyto produkty, jejichž `UnitsInStock` a `UnitsOnOrder` pole jsou rovny 0. Pro zdůraznění dražších produktů můžeme podle tučného písma zobrazit ceny těchto produktů, které jsou v ceně větší než $75,00.

Přizpůsobení formátu prvku GridView, DetailsView nebo FormView na základě dat, která jsou k němu vázána, lze provést několika způsoby. V tomto kurzu se podíváme na to, jak provádět formátování vázané na data pomocí `DataBound` a `RowDataBound` obslužných rutin událostí. V dalším kurzu prozkoumáme alternativní přístup.

## <a name="using-the-detailsview-controlsdataboundevent-handler"></a>Používání obslužné rutiny události`DataBound`ovládacího prvku DetailsView

Pokud jsou data svázána s ovládacím prvkem DetailsView, buď z ovládacího prvku zdroje dat, nebo prostřednictvím programové přiřazování dat do vlastnosti `DataSource` ovládacího prvku a voláním jeho `DataBind()` metody, dojde k následujícímu pořadí kroků:

1. Událost `DataBinding` události webového ovládacího prvku data je aktivována.
2. Data jsou svázána s datovým ovládacím prvkem webového ovládacího prvku.
3. Událost `DataBound` události webového ovládacího prvku data je aktivována.

Vlastní logiku lze vložit hned po krocích 1 a 3 prostřednictvím obslužné rutiny události. Vytvořením obslužné rutiny události pro událost `DataBound` můžeme programově určit data vázaná na webový ovládací prvek data a podle potřeby upravit formátování. Pro ilustraci tohoto pojďme vytvořit prvek DetailsView, který bude obsahovat obecné informace o produktu, ale zobrazí hodnotu `UnitPrice` ***tučným písmem,*** pokud překročí $75,00.

## <a name="step-1-displaying-the-product-information-in-a-detailsview"></a>Krok 1: zobrazení informací o produktu v ovládacím prvku DetailsView

Otevřete stránku `CustomColors.aspx` ve složce `CustomFormatting`, přetáhněte ovládací prvek DetailsView z panelu nástrojů do návrháře, nastavte jeho hodnotu vlastnosti `ID` na `ExpensiveProductsPriceInBoldItalic`a navažte ji na nový ovládací prvek ObjectDataSource, který vyvolá `ProductsBLL` metodu `GetProducts()` třídy. Zde jsou uvedené podrobné kroky pro zkrácení, protože jsme je podrobněji prozkoumali v předchozích kurzech.

Po svázání prvku ObjectDataSource s ovládacím prvkem DetailsView chvíli počkejte, než se upraví seznam polí. Rozhodli jste se odebrat `ProductID`, `SupplierID`, `CategoryID`, `UnitsInStock`, `UnitsOnOrder`, `ReorderLevel`a `Discontinued` BoundFields a přeformátovat zbývající BoundFields. Vymazal jsem taky `Width` a nastavení `Height`. Vzhledem k tomu, že prvek DetailsView zobrazuje pouze jeden záznam, musíme Povolit stránkování, aby mohl koncový uživatel zobrazit všechny produkty. Provedete to tak, že zaškrtnete políčko Povolit stránkování v inteligentní značce DetailsView.

[![zaškrtněte políčko Povolit stránkování v inteligentní značce DetailsView.](custom-formatting-based-upon-data-cs/_static/image2.png)](custom-formatting-based-upon-data-cs/_static/image1.png)

**Obrázek 1**: zaškrtněte políčko Povolit stránkování v inteligentní značce ovládacího prvku DetailsView ([kliknutím zobrazíte obrázek v plné velikosti).](custom-formatting-based-upon-data-cs/_static/image3.png)

Po těchto změnách budou značky DetailsView:

[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample1.aspx)]

Vyzkoušení této stránky v prohlížeči chvíli počkejte.

[![ovládací prvek DetailsView zobrazí jeden produkt v čase.](custom-formatting-based-upon-data-cs/_static/image5.png)](custom-formatting-based-upon-data-cs/_static/image4.png)

**Obrázek 2**: ovládací prvek DetailsView zobrazuje jeden produkt v čase ([kliknutím zobrazíte obrázek v plné velikosti).](custom-formatting-based-upon-data-cs/_static/image6.png)

## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>Krok 2: určení hodnoty dat v obslužné rutině události vázaného na data prostřednictvím kódu programu

Aby se zobrazila cena tučně tučným písmem u těchto produktů, jejichž hodnota `UnitPrice` překračuje $75,00, musíme napřed programově určit hodnotu `UnitPrice`. Pro prvek DetailsView to lze provést v obslužné rutině události `DataBound`. Chcete-li vytvořit obslužnou rutinu události, klikněte na ovládací prvek DetailsView v návrháři a potom přejděte na okno Vlastnosti. Stisknutím klávesy F4 ji přeneste nahoru, pokud není zobrazená, nebo přejděte do nabídky zobrazení a vyberte možnost nabídky okna Vlastnosti. V okno Vlastnosti klikněte na ikonu blesku a uveďte události ovládacího prvku DetailsView. Dále buď poklikejte na událost `DataBound`, nebo zadejte název obslužné rutiny události, kterou chcete vytvořit.

![Vytvoření obslužné rutiny události pro událost DataBound](custom-formatting-based-upon-data-cs/_static/image7.png)

**Obrázek 3**: vytvoření obslužné rutiny události pro událost `DataBound`

Tím dojde k automatickému vytvoření obslužné rutiny události a přejdete do části kódu, kde byla přidána. V tomto okamžiku se zobrazí:

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample2.cs)]

K datům vázaným na prvek DetailsView lze přistupovat prostřednictvím vlastnosti `DataItem`. Odvoláme, že tyto ovládací prvky zavazujeme ke silně typovanému objektu DataTable, který se skládá z kolekce instancí DataRow se silným typem. Je-li objekt DataTable svázán s ovládacím prvek DetailsView, je první objekt DataRow v objektu DataTable přiřazen vlastnosti `DataItem` ovládacího prvku DetailsView. Konkrétně je vlastnost `DataItem` přiřazena objektu `DataRowView`. Pomocí vlastnosti `Row` `DataRowView`můžete získat přístup k podkladovému objektu DataRow, který je ve skutečnosti instancí `ProductsRow`. Až tuto instanci `ProductsRow`me, můžeme nám učinit naše rozhodnutí pouhým zkontrolováním hodnot vlastností objektu.

Následující kód ilustruje, jak určit, zda `UnitPrice` hodnota vázaná k ovládacímu prvku DetailsView je větší než $75,00:

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample3.cs)]

> [!NOTE]
> Vzhledem k tomu, že `UnitPrice` může mít v databázi hodnotu `NULL`, nejdřív zkontrolujeme, že před přístupem k `UnitPrice` vlastnosti `ProductsRow`se ujistěte, že neřešíte `NULL`. Tato kontrolu je důležité, protože pokud se pokusíte o přístup k vlastnosti `UnitPrice`, když má `NULL` hodnotu, objekt `ProductsRow` vyvolá [výjimku StrongTypingException](https://msdn.microsoft.com/library/system.data.strongtypingexception.aspx).

## <a name="step-3-formatting-the-unitprice-value-in-the-detailsview"></a>Krok 3: formátování hodnoty JednotkováCena v ovládacím prvku DetailsView

V tuto chvíli můžeme určit, jestli `UnitPrice` hodnota vázaná k prvku DetailsView má hodnotu, která překračuje $75,00, ale ještě jsme zjistili, jak programově upravit formátování ovládacího prvku DetailsView. Chcete-li upravit formátování celého řádku ovládacího prvku DetailsView, programově přístup k řádku pomocí `DetailsViewID.Rows[index]`; Chcete-li upravit konkrétní buňku, použijte přístup `DetailsViewID.Rows[index].Cells[index]`. Jakmile máme odkaz na řádek nebo buňku, můžeme upravit jeho vzhled nastavením vlastností souvisejících s jeho stylem.

Přístup k řádku programově vyžaduje, abyste znali index řádku, který začíná na 0. `UnitPrice` řádek je pátý řádek v ovládacím prvku DetailsView, který mu dává index 4 a je programově přístupný pomocí `ExpensiveProductsPriceInBoldItalic.Rows[4]`. V tuto chvíli jsme mohli zobrazit obsah celého řádku tučným písmem kurzívou, a to pomocí následujícího kódu:

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample4.cs)]

Tato akce však vytvoří popisek (Price *) i hodnotu* tučnou a kurzívou. Pokud chceme udělat jenom tuto hodnotu tučně a kurzívu, je potřeba použít toto formátování na druhou buňku na řádku, kterou můžete dosáhnout pomocí následujících kroků:

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample5.cs)]

Vzhledem k tomu, že naše kurzy doposud používaly šablony stylů k údržbě čistého oddělení mezi vykreslenými značkami a informacemi souvisejícími se styly, místo nastavení specifických vlastností stylu, jak je uvedeno výše, použijte místo toho třídu CSS. Otevřete `Styles.css` StyleSheet a přidejte novou třídu CSS s názvem `ExpensivePriceEmphasis` s následující definicí:

[!code-css[Main](custom-formatting-based-upon-data-cs/samples/sample6.css)]

Poté v obslužné rutině události `DataBound` nastavte vlastnost `CssClass` buňky na `ExpensivePriceEmphasis`. Následující kód ukazuje obslužnou rutinu události `DataBound` v celém rozsahu:

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample7.cs)]

Při zobrazení hodnoty Chai, která je nižší než $75,00, se cena zobrazuje v normálním písmu (viz obrázek 4). Když ale Mishi Kobe niku, která má cenu $97,00, zobrazí se v tučném písmu tučné písmo kurzíva (viz obrázek 5).

[Ceny ![méně než $75,00 se zobrazují v normálním písmu.](custom-formatting-based-upon-data-cs/_static/image9.png)](custom-formatting-based-upon-data-cs/_static/image8.png)

**Obrázek 4**: ceny menší než $75,00 se zobrazují v normálním písmu ([kliknutím zobrazíte obrázek v plné velikosti).](custom-formatting-based-upon-data-cs/_static/image10.png)

[Ceny ![drahých produktů se zobrazí tučným písmem, kurzívou.](custom-formatting-based-upon-data-cs/_static/image12.png)](custom-formatting-based-upon-data-cs/_static/image11.png)

**Obrázek 5**: ceny drahých produktů se zobrazí tučným písmem, kurzívou ([kliknutím zobrazíte obrázek v plné velikosti](custom-formatting-based-upon-data-cs/_static/image13.png)).

## <a name="using-the-formview-controlsdataboundevent-handler"></a>Použití obslužné rutiny události`DataBound`ovládacího prvku FormView

Postup určení podkladových dat vázaných na FormView je stejný jako u prvku DetailsView vytvoření obslužné rutiny události `DataBound`, přetypujte vlastnost `DataItem` na příslušný typ objektu vázaný na ovládací prvek a určete, jak se má pokračovat. Třída FormView a DetailsView se ve způsobu, jakým se aktualizuje jejich vzhled uživatelského rozhraní, liší.

Třída FormView neobsahuje žádné BoundFields, a proto nemá kolekci `Rows`. Místo toho je třída FormView tvořena šablonami, které mohou obsahovat kombinaci statických prvků HTML, webové ovládací prvky a syntaxe datových vazeb. Úprava stylu třídy FormView obvykle zahrnuje úpravu stylu jednoho nebo více webových ovládacích prvků v rámci šablon třídy FormView.

K tomu je možné použít FormView k vypsání produktů jako v předchozím příkladu, ale tentokrát se zobrazí pouze název produktu a jednotky na skladě s jednotkami v zásobách zobrazenými červeným písmem, pokud je menší nebo rovno 10.

## <a name="step-4-displaying-the-product-information-in-a-formview"></a>Krok 4: zobrazení informací o produktu ve třídě FormView

Přidejte FormView na stránku `CustomColors.aspx` pod ovládacím prvkem DetailsView a nastavte jeho vlastnost `ID` na `LowStockedProductsInRed`. Vytvořte vazby třídy FormView k ovládacímu prvku ObjectDataSource vytvořenému z předchozího kroku. Tím se pro FormView vytvoří `ItemTemplate`, `EditItemTemplate`a `InsertItemTemplate`. Odeberte `EditItemTemplate` a `InsertItemTemplate` a zjednodušte `ItemTemplate`, abyste zahrnuli pouze hodnoty `ProductName` a `UnitsInStock`, každý ve vlastním vhodně pojmenovaném ovládacím prvku Label. Stejně jako u prvku DetailsView z předchozího příkladu zaškrtněte políčko Povolit stránkování v inteligentní značce třídy FormView.

Po úpravách značek FormView by měl vypadat nějak takto:

[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample8.aspx)]

Všimněte si, že `ItemTemplate` obsahuje:

- **Statický kód HTML** : text "produkt" a "jednotky" na skladě: "spolu s prvky `<br />` a `<b>`.
- **Webové ovládací prvky** mají dva ovládací prvky popisku `ProductNameLabel` a `UnitsInStockLabel`.
- **Syntaxe datové vazby** : syntaxe `<%# Bind("ProductName") %>` a `<%# Bind("UnitsInStock") %>`, která přiřazuje hodnoty z těchto polí k vlastnostem `Text` prvků ovládacího prvku Label.

## <a name="step-5-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>Krok 5: určení hodnoty dat v obslužné rutině události DataBound prostřednictvím kódu programu

Po dokončení značek třídy FormView je dalším krokem programové určení, zda je hodnota `UnitsInStock` menší nebo rovna 10. To se provádí stejným způsobem jako u třídy FormView jako v prvku DetailsView. Začněte vytvořením obslužné rutiny události pro událost `DataBound` třídy FormView.

![Vytvoření obslužné rutiny události vázaného na událost](custom-formatting-based-upon-data-cs/_static/image14.png)

**Obrázek 6**: vytvoření obslužné rutiny události `DataBound`

V obslužné rutině události přetypování vlastnosti `DataItem` třídy FormView na instanci `ProductsRow` a určení, zda je hodnota `UnitsInPrice`, kterou je třeba zobrazit v červeném písmu.

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample9.cs)]

## <a name="step-6-formatting-the-unitsinstocklabel-label-control-in-the-formviews-itemtemplate"></a>Krok 6: formátování ovládacího prvku popisek UnitsInStockLabel v šabloně ItemTemplate třídy FormView

Posledním krokem je NaFormát zobrazené hodnoty `UnitsInStock` červeným písmem, pokud je hodnota 10 nebo menší. Abychom to mohli udělat, potřebujeme programově přistupovat k ovládacímu prvku `UnitsInStockLabel` v `ItemTemplate` a nastavit jeho vlastnosti stylu tak, aby se jeho text zobrazoval červeně. Pro přístup k webovému ovládacímu prvku v šabloně použijte metodu `FindControl("controlID")` takto:

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample10.cs)]

Pro náš příklad chceme získat přístup k ovládacímu prvku popisku, jehož hodnota `ID` je `UnitsInStockLabel`, takže budeme používat:

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample11.cs)]

Jakmile máme programový odkaz na webový ovládací prvek, můžeme podle potřeby upravit jeho vlastnosti související se styly. Stejně jako v předchozím příkladu jsem vytvořil (a) třídu CSS v `Styles.css` s názvem `LowUnitsInStockEmphasis`. Chcete-li použít tento styl pro webový ovládací prvek popisek, nastavte jeho vlastnost `CssClass` odpovídajícím způsobem.

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample12.cs)]

> [!NOTE]
> Syntaxe pro formátování šablony programově přistupující k webovému ovládacímu prvku pomocí `FindControl("controlID")` a poté nastavení vlastností souvisejících s Style lze použít také při použití elementů [TemplateField](https://msdn.microsoft.com/library/system.web.ui.webcontrols.templatefield(VS.80).aspx) v ovládacím prvku DetailsView nebo GridView. V našem dalším kurzu vyhledáme pole TemplateField.

Obrázky 7 znázorňují FormView při zobrazení produktu, jehož hodnota `UnitsInStock` je větší než 10, zatímco produkt na obrázku 8 má hodnotu menší než 10.

[![pro produkty s dostatečně velkými jednotkami v zásobách, není použito žádné vlastní formátování.](custom-formatting-based-upon-data-cs/_static/image16.png)](custom-formatting-based-upon-data-cs/_static/image15.png)

**Obrázek 7**: u produktů s dostatečně velkými jednotkami na skladě se nepoužije žádné vlastní formátování ([kliknutím zobrazíte obrázek v plné velikosti).](custom-formatting-based-upon-data-cs/_static/image17.png)

[![jednotky na skladovém čísle se zobrazí červeně pro tyto produkty s hodnotami 10 a méně.](custom-formatting-based-upon-data-cs/_static/image19.png)](custom-formatting-based-upon-data-cs/_static/image18.png)

**Obrázek 8**: jednotky na skladovém čísle jsou zobrazeny červeně pro tyto produkty s hodnotami 10 nebo méně ([kliknutím zobrazíte obrázek v plné velikosti).](custom-formatting-based-upon-data-cs/_static/image20.png)

## <a name="formatting-with-the-gridviewsrowdataboundevent"></a>Formátování pomocí`RowDataBound`události prvku GridView

Dříve jsme zkoumali sekvenci kroků, které ovládací prvek DetailsView a FormView během zpracování datové vazby provede. Pojďme tyto kroky znovu nahlížet jako aktualizační program.

1. Událost `DataBinding` události webového ovládacího prvku data je aktivována.
2. Data jsou svázána s datovým ovládacím prvkem webového ovládacího prvku.
3. Událost `DataBound` události webového ovládacího prvku data je aktivována.

Tyto tři jednoduché kroky jsou dostačující pro ovládací prvek DetailsView a FormView, protože zobrazují pouze jeden záznam. Pro prvek GridView, který zobrazuje *všechny* záznamy s ním spojené (ne pouze první), krok 2 je o něco složitější.

V kroku 2 sestaví prvek GridView zdroj dat a pro každý záznam vytvoří instanci `GridViewRow` a naváže na ni aktuální záznam. Pro každý `GridViewRow` přidaný do prvku GridView jsou vyvolány dvě události:

- **`RowCreated`** aktivovaná po vytvoření `GridViewRow`
- **`RowDataBound`** aktivuje se po vazbě aktuálního záznamu na `GridViewRow`.

Pro prvek GridView je vazba dat přesněji popsána v následujícím pořadí kroků:

1. Událost `DataBinding` prvku GridView je aktivována.
2. Data jsou svázána s ovládacím prvek GridView.   
  
   Pro každý záznam ve zdroji dat 

    1. Vytvoření objektu `GridViewRow`
    2. Vyvolat událost `RowCreated`
    3. Navázání záznamu na `GridViewRow`
    4. Vyvolat událost `RowDataBound`
    5. Přidání `GridViewRow` do kolekce `Rows`
3. Událost `DataBound` prvku GridView je aktivována.

Chcete-li přizpůsobit formát jednotlivých záznamů prvku GridView, musíme pro událost `RowDataBound` vytvořit obslužnou rutinu události. K tomu je možné přidat prvek GridView na stránku `CustomColors.aspx`, která obsahuje název, kategorii a cenu za jednotlivé produkty. zvýrazní se tak produkty, jejichž cena je menší než $10,00 se žlutou barvou pozadí.

## <a name="step-7-displaying-product-information-in-a-gridview"></a>Krok 7: zobrazení informací o produktu v prvku GridView

Přidejte prvek GridView pod objekt FormView z předchozího příkladu a nastavte jeho vlastnost `ID` na hodnotu `HighlightCheapProducts`. Vzhledem k tomu, že již máme prvek ObjectDataSource, který vrací všechny produkty na stránce, navažte na něj prvek GridView. Nakonec upravte BoundFields prvku GridView tak, aby zahrnoval pouze názvy, kategorie a ceny produktů. Po těchto úpravách by značky GridView měly vypadat takto:

[!code-aspx[Main](custom-formatting-based-upon-data-cs/samples/sample13.aspx)]

Obrázek 9 ukazuje náš průběh tohoto bodu při prohlížení v prohlížeči.

[![je v prvku GridView uveden název, kategorie a cena pro každý produkt.](custom-formatting-based-upon-data-cs/_static/image22.png)](custom-formatting-based-upon-data-cs/_static/image21.png)

**Obrázek 9**: v prvku GridView je uveden název, kategorie a cena pro každý produkt ([kliknutím zobrazíte obrázek v plné velikosti](custom-formatting-based-upon-data-cs/_static/image23.png)).

## <a name="step-8-programmatically-determining-the-value-of-the-data-in-the-rowdatabound-event-handler"></a>Krok 8: určení hodnoty dat v obslužné rutině události RowDataBound prostřednictvím kódu programu

Pokud je `ProductsDataTable` svázána s ovládacím prvek GridView, jeho `ProductsRow` instance jsou vyhodnoceny a pro každou `ProductsRow` vytvořenou `GridViewRow`. Vlastnost `DataItem` `GridViewRow`je přiřazena konkrétnímu `ProductRow`, po kterém je vyvolána obslužná rutina události `RowDataBound` prvku GridView. Pro určení `UnitPrice` hodnoty pro každý produkt vázaný na prvek GridView, musíme vytvořit obslužnou rutinu události pro událost `RowDataBound` prvku GridView. V této obslužné rutině události můžeme zkontrolovat hodnotu `UnitPrice` pro aktuální `GridViewRow` a udělat pro tento řádek rozhodnutí o formátování.

Tuto obslužnou rutinu události lze vytvořit pomocí stejné řady kroků jako u třídy FormView a DetailsView.

![Vytvoření obslužné rutiny události pro událost RowDataBound prvku GridView](custom-formatting-based-upon-data-cs/_static/image24.png)

**Obrázek 10**: vytvoření obslužné rutiny události pro událost `RowDataBound` prvku GridView

Vytvoření obslužné rutiny události tímto způsobem způsobí, že se následující kód automaticky přidá do části kódu stránky ASP.NET:

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample14.cs)]

Když událost `RowDataBound` aktivuje, obslužná rutina události se předává jako jeho druhý parametr objekt typu `GridViewRowEventArgs`, který má vlastnost s názvem `Row`. Tato vlastnost vrací odkaz na `GridViewRow`, která byla pouze vázaná na data. Pro přístup k instanci `ProductsRow` navázané na `GridViewRow` používáme vlastnost `DataItem`, například:

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample15.cs)]

Při práci s obslužnou rutinou události `RowDataBound` je důležité mít na paměti, že prvek GridView se skládá z různých typů řádků a že tato událost je aktivována pro *všechny* typy řádků. Typ `GridViewRow`lze určit jeho vlastností `RowType` a může mít jednu z možných hodnot:

- `DataRow` řádek, který je vázán na záznam z `DataSource` prvku GridView.
- `EmptyDataRow` řádek, který se zobrazí, pokud je `DataSource` prvku GridView prázdné
- `Footer` řádku zápatí; Zobrazuje se, pokud je vlastnost `ShowFooter` prvku GridView nastavena na hodnotu `true`
- `Header` řádku záhlaví; Zobrazuje se, pokud je vlastnost ShowHeader prvku GridView nastavená na `true` (výchozí).
- `Pager` pro prvek GridView, který implementuje stránkování, řádek, který zobrazuje rozhraní stránkování
- `Separator` nepoužívá se pro prvek GridView, ale používá se `RowType` vlastností pro ovládací prvky DataList a Repeater, v budoucích kurzech probereme dvě webové ovládací prvky, které budeme projednávat.

Vzhledem k tomu, že `EmptyDataRow`, `Header`, `Footer`a řádky `Pager` nejsou přidruženy k záznamu `DataSource`, budou mít vždy `null` hodnotu pro svou `DataItem` vlastnost. Z tohoto důvodu se před tím, než se pokusíte pracovat s aktuální `GridViewRow`vlastností `DataItem`, nejdřív musíte zajistit, aby se jednalo o `DataRow`. To lze provést kontrolou vlastnosti `GridViewRow``RowType`, například takto:

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample16.cs)]

## <a name="step-9-highlighting-the-row-yellow-when-the-unitprice-value-is-less-than-1000"></a>Krok 9: zvýraznění řádku žlutě, pokud je hodnota UnitPrice menší než $10,00

Posledním krokem je programové zvýraznění celého `GridViewRow`, pokud je hodnota `UnitPrice` pro tento řádek menší než $10,00. Syntaxe pro přístup k řádkům nebo buňkám prvku GridView je stejná jako u `GridViewID.Rows[index]` ovládacího prvku DetailsView pro přístup k celému řádku, `GridViewID.Rows[index].Cells[index]` pro přístup ke konkrétní buňce. Nicméně, pokud obslužná rutina události `RowDataBound` aktivuje, je `GridViewRow` vázaný na data stále přidán do kolekce `Rows` prvku GridView. Proto nemůžete získat přístup k aktuální instanci `GridViewRow` z obslužné rutiny události `RowDataBound` pomocí kolekce řádků.

Místo `GridViewID.Rows[index]`můžeme pomocí `e.Row`použít odkaz na aktuální instanci `GridViewRow` v obslužné rutině události `RowDataBound`. To znamená, že k zdůraznění aktuální instance `GridViewRow` z `RowDataBound` obslužné rutiny události, kterou bychom použili:

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample17.cs)]

Místo toho, abyste nastavili vlastnost `BackColor` `GridViewRow`přímo, pojďme použít třídy CSS. Vytvořili jsme třídu CSS s názvem `AffordablePriceEmphasis`, která nastaví barvu pozadí na žlutou. Dokončená obslužná rutina události `RowDataBound` následující:

[!code-csharp[Main](custom-formatting-based-upon-data-cs/samples/sample18.cs)]

[![je zvýrazněný žlutý produkt.](custom-formatting-based-upon-data-cs/_static/image26.png)](custom-formatting-based-upon-data-cs/_static/image25.png)

**Obrázek 11**: nejvíce dostupné produkty jsou zvýrazněny žlutě ([kliknutím zobrazíte obrázek v plné velikosti).](custom-formatting-based-upon-data-cs/_static/image27.png)

## <a name="summary"></a>Přehled

V tomto kurzu jsme viděli, jak naformátovat prvky GridView, DetailsView a FormView na základě dat svázaných s ovládacím prvkem. Pro dosažení této služby jsme vytvořili obslužnou rutinu události pro události `DataBound` nebo `RowDataBound`, kde jsou podkladová data zkontrolována spolu se změnou formátování v případě potřeby. Pro přístup k datům vázaným na DetailsView nebo FormView používáme vlastnost `DataItem` v obslužné rutině události `DataBound`; u prvku GridView obsahuje každá `GridViewRow`ová vlastnost `DataItem` instance data vázaná na daný řádek, který je k dispozici v obslužné rutině události `RowDataBound`.

Syntaxe pro programové úpravy formátování webového ovládacího prvku data závisí na ovládacím prvku web a na způsobu formátování dat, která mají být formátována. Pro ovládací prvky DetailsView a GridView lze řádky a buňky přistupovat pomocí ordinálního indexu. Pro FormView, který používá šablony, se běžně používá metoda `FindControl("controlID")` k nalezení webového ovládacího prvku v rámci šablony.

V dalším kurzu se podíváme na použití šablon pomocí prvku GridView a DetailsView. Navíc uvidíte další postup přizpůsobení formátování na základě podkladových dat.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli E.R. Gilmore, Dennis Patterson a Dan Jagers. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](using-templatefields-in-the-gridview-control-cs.md)

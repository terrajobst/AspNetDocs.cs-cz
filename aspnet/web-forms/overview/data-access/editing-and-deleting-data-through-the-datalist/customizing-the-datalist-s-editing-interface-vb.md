---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-vb
title: Přizpůsobení rozhraní pro úpravy prvku DataList (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu vytvoříme bohatší rozhraní pro úpravy ovládacího prvku DataList, který obsahuje ovládací prvky DropDownList a CheckBox.
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 718628e2-224c-455f-b33a-a41efd48d5a0
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/customizing-the-datalist-s-editing-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: adee419764cff2f39ee16962080c24b52553aa14
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74637598"
---
# <a name="customizing-the-datalists-editing-interface-vb"></a>Přizpůsobení rozhraní pro úpravy prvku DataList (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_40_VB.exe) nebo [Stáhnout PDF](customizing-the-datalist-s-editing-interface-vb/_static/datatutorial40vb1.pdf)

> V tomto kurzu vytvoříme bohatší rozhraní pro úpravy ovládacího prvku DataList, který obsahuje ovládací prvky DropDownList a CheckBox.

## <a name="introduction"></a>Úvod

Značky a webové ovládací prvky v prvku DataList s `EditItemTemplate` definují své upravitelné rozhraní. Ve všech upravitelných příkladech DataList, které jsme doposud prozkoumali, bylo možné upravit rozhraní, které se skládá z webových ovládacích prvků TextBox. V [předchozím kurzu](adding-validation-controls-to-the-datalist-s-editing-interface-vb.md) jsme vylepšili uživatelské prostředí pro úpravu času přidáním ověřovacích ovládacích prvků.

`EditItemTemplate` lze dále rozšířit tak, aby zahrnovala webové ovládací prvky jiné než textové pole, například DropDownList, RadioButtonLists, calendars a tak dále. Stejně jako u textových polí lze při přizpůsobení rozhraní pro úpravy zahrnout další webové ovládací prvky pomocí následujících kroků:

1. Přidejte webový ovládací prvek do `EditItemTemplate`.
2. K přiřazení odpovídající hodnoty datového pole k příslušné vlastnosti použijte syntaxi DataBinding.
3. V obslužné rutině události `UpdateCommand` programově přistupuje k hodnotě webového ovládacího prvku a předají se do příslušné metody knihoven BLL.

V tomto kurzu vytvoříme bohatší rozhraní pro úpravy ovládacího prvku DataList, který obsahuje ovládací prvky DropDownList a CheckBox. Konkrétně vytvoříme prvek DataList, který zobrazí seznam informací o produktech a povoluje aktualizaci názvu produktu, dodavatele, kategorie a zastaveného stavu (viz obrázek 1).

[![rozhraní pro úpravy obsahuje textové pole, dva DropDownList a CheckBox.](customizing-the-datalist-s-editing-interface-vb/_static/image2.png)](customizing-the-datalist-s-editing-interface-vb/_static/image1.png)

**Obrázek 1**: rozhraní pro úpravy obsahuje textové pole, dva DropDownList a CheckBox ([kliknutím zobrazíte obrázek v plné velikosti).](customizing-the-datalist-s-editing-interface-vb/_static/image3.png)

## <a name="step-1-displaying-product-information"></a>Krok 1: zobrazení informací o produktu

Než budeme moct vytvořit upravitelné rozhraní DataList s, musíme nejdřív vytvořit rozhraní jen pro čtení. Začněte tím, že otevřete `CustomizedUI.aspx` stránku ze složky `EditDeleteDataList` a z návrháře přidáte prvek DataList na stránku a nastavíte jeho vlastnost `ID` na `Products`. Z inteligentní značky DataList s vytvořte nový prvek ObjectDataSource. Pojmenujte tuto novou `ProductsDataSource` ObjectDataSource a nakonfigurujte ji tak, aby načetla data z metody `GetProducts` `ProductsBLL` třídy s. Stejně jako u předchozích upravitelných kurzů DataList aktualizujeme upravené informace o produktech přímo do vrstvy obchodní logiky. Proto nastavte rozevírací seznamy na kartách aktualizace, vložení a odstranění na (žádné).

[![nastavení rozevíracích seznamů pro aktualizaci, vložení a odstranění karet (žádné)](customizing-the-datalist-s-editing-interface-vb/_static/image5.png)](customizing-the-datalist-s-editing-interface-vb/_static/image4.png)

**Obrázek 2**: nastavení rozevíracích seznamů pro aktualizaci, vložení a odstranění karet na (žádné) ([kliknutím zobrazíte obrázek v plné velikosti](customizing-the-datalist-s-editing-interface-vb/_static/image6.png))

Po nakonfigurování prvku ObjectDataSource vytvoří Visual Studio výchozí `ItemTemplate` pro prvek DataList, který obsahuje název a hodnotu pro každé vrácené datové pole. Upravte `ItemTemplate` tak, aby šablona vypisuje název produktu v prvku `<h4>` spolu s názvem kategorie, názvem dodavatele, cenou a ukončeným stavem. Kromě toho přidejte tlačítko Upravit a ujistěte se, že je jeho vlastnost `CommandName` nastavena na hodnotu upravit. Následující deklarativní označení pro moji `ItemTemplate`:

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample1.aspx)]

Výše uvedený kód obsahuje informace o produktu pomocí &lt;H4&gt; nadpis pro název produktu a `<table>` se čtyřmi sloupci u zbývajících polí. Třídy `ProductPropertyLabel` a `ProductPropertyValue` CSS definované v `Styles.css`byly popsány v předchozích kurzech. Obrázek 3 ukazuje náš průběh při prohlížení v prohlížeči.

[![název, dodavatel, kategorie, zastavený stav a zobrazí se cena každého produktu.](customizing-the-datalist-s-editing-interface-vb/_static/image8.png)](customizing-the-datalist-s-editing-interface-vb/_static/image7.png)

**Obrázek 3**: zobrazí se název, dodavatel, kategorie, zastavený stav a cena každého produktu ([kliknutím zobrazíte obrázek v plné velikosti).](customizing-the-datalist-s-editing-interface-vb/_static/image9.png)

## <a name="step-2-adding-the-web-controls-to-the-editing-interface"></a>Krok 2: Přidání webových ovládacích prvků do rozhraní pro úpravy

Prvním krokem při sestavování přizpůsobeného rozhraní pro úpravu prvku DataList je přidat do `EditItemTemplate`potřebné webové ovládací prvky. Konkrétně potřebujeme pro kategorii, jinou pro dodavatele a zaškrtávací políčko pro ukončený stav. Protože cena za produkt není v tomto příkladu upravitelná, můžeme ji dál zobrazit pomocí webového ovládacího prvku popisek.

Chcete-li přizpůsobit rozhraní pro úpravy, klikněte na odkaz Upravit šablony z inteligentní značky DataList s a v rozevíracím seznamu vyberte možnost `EditItemTemplate`. Přidejte do `EditItemTemplate` objekt DropDownList a nastavte jeho `ID` na `Categories`.

[![přidat DropDownList pro kategorie](customizing-the-datalist-s-editing-interface-vb/_static/image11.png)](customizing-the-datalist-s-editing-interface-vb/_static/image10.png)

**Obrázek 4**: Přidání ovládacího prvkem DropDownList pro kategorie ([kliknutím zobrazíte obrázek v plné velikosti](customizing-the-datalist-s-editing-interface-vb/_static/image12.png))

Potom z inteligentní značky DropDownList s vyberte možnost zvolit zdroj dat a vytvořte nový prvek ObjectDataSource s názvem `CategoriesDataSource`. Nakonfigurujte tuto ObjectDataSource tak, aby používala metodu `CategoriesBLL` třídy s `GetCategories()` (viz obrázek 5). Dále Průvodce konfigurací zdroje dat DropDownList s vyzve k zadání datových polí, která se mají použít pro každou `Text` `ListItem` s a vlastnosti `Value`. Zobrazit pole `CategoryName` dat a použít `CategoryID` jako hodnotu, jak je znázorněno na obrázku 6.

[![vytvořit nový prvek ObjectDataSource s názvem CategoriesDataSource](customizing-the-datalist-s-editing-interface-vb/_static/image14.png)](customizing-the-datalist-s-editing-interface-vb/_static/image13.png)

**Obrázek 5**: vytvoření nového prvku ObjectDataSource s názvem `CategoriesDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](customizing-the-datalist-s-editing-interface-vb/_static/image15.png))

[![nakonfigurovat pole zobrazení a hodnoty ovládacího prvků DropDownList](customizing-the-datalist-s-editing-interface-vb/_static/image17.png)](customizing-the-datalist-s-editing-interface-vb/_static/image16.png)

**Obrázek 6**: Konfigurace polí zobrazení a hodnoty ovládacího prvků DropDownList ([kliknutím zobrazíte obrázek v plné velikosti](customizing-the-datalist-s-editing-interface-vb/_static/image18.png))

Zopakováním této série kroků vytvořte pro dodavatele DropDownList. Nastavte `ID` pro tento DropDownList pro `Suppliers` a pojmenujte jeho ObjectDataSource `SuppliersDataSource`.

Po přidání dvou ovládacích prvků DropDownList přidejte zaškrtávací políčko pro stav ukončeno a textové pole pro název produktu. Nastavte `ID` pro zaškrtávací políčko a textové pole tak, aby `Discontinued` a `ProductName`, v uvedeném pořadí. Přidejte RequiredFieldValidator a ujistěte se, že uživatel zadá hodnotu pro název produktu.

Nakonec přidejte tlačítka aktualizovat a zrušit. Pamatujte, že u těchto dvou tlačítek je potřeba, aby se jejich `CommandName` vlastnosti nastavily na aktualizovat a zrušit v uvedeném pořadí.

Klidně rozložte rozhraní pro úpravy, které chcete. Beru na to, že se má použít stejné rozložení `<table>` se čtyřmi sloupci z rozhraní jen pro čtení, protože následující deklarativní syntaxe a snímek obrazovky ilustrují:

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample2.aspx)]

[![rozhraní pro úpravy je určeno jako rozhraní jen pro čtení](customizing-the-datalist-s-editing-interface-vb/_static/image20.png)](customizing-the-datalist-s-editing-interface-vb/_static/image19.png)

**Obrázek 7**: rozhraní pro úpravy je určeno jako rozhraní jen pro čtení ([kliknutím zobrazíte obrázek v plné velikosti).](customizing-the-datalist-s-editing-interface-vb/_static/image21.png)

## <a name="step-3-creating-the-editcommand-and-cancelcommand-event-handlers"></a>Krok 3: Vytvoření obslužných rutin událostí EditCommand a CancelCommand

V současné době není k dispozici žádná syntaxe datové vazby v `EditItemTemplate` (s výjimkou `UnitPriceLabel`, která byla zkopírována přes doslovného `ItemTemplate`). V tuto chvíli přidáme syntaxi datové vazby, ale nejdříve si vytvoříme obslužné rutiny událostí pro `EditCommand` a `CancelCommand` události DataList. Odvolání, že zodpovědnost obslužné rutiny události `EditCommand` je vykreslení rozhraní pro úpravy pro položku DataList, jejíž tlačítko Upravit bylo kliknuto, zatímco úloha `CancelCommand` s má vrátit prvek DataList do stavu před úpravou.

Vytvořte tyto dvě obslužné rutiny událostí a použijte následující kód:

[!code-vb[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample3.vb)]

Pomocí těchto dvou obslužných rutin událostí můžete kliknutím na tlačítko Upravit zobrazit rozhraní pro úpravy a kliknutím na tlačítko Storno vrátíte upravenou položku do režimu jen pro čtení. Obrázek 8 ukazuje ovládací prvek DataList po kliknutí na tlačítko pro úpravy pro Antoní Gumbo. Vzhledem k tomu, že jsme ještě do rozhraní pro úpravy přidali jakoukoliv syntaxi datových vazeb, je `ProductName` textové pole prázdné, zaškrtávací políčko `Discontinued` nezaškrtnuto a první položky vybrané z `Categories` a `Suppliers` DropDownList.

[![kliknutí na tlačítko Upravit zobrazí rozhraní pro úpravy.](customizing-the-datalist-s-editing-interface-vb/_static/image23.png)](customizing-the-datalist-s-editing-interface-vb/_static/image22.png)

**Obrázek 8**: kliknutím na tlačítko Upravit zobrazíte rozhraní pro úpravy (Kliknutím zobrazíte[obrázek v plné velikosti).](customizing-the-datalist-s-editing-interface-vb/_static/image24.png)

## <a name="step-4-adding-the-databinding-syntax-to-the-editing-interface"></a>Krok 4: Přidání syntaxe datové vazby do rozhraní pro úpravy

Aby rozhraní pro úpravy zobrazovalo aktuální hodnoty produktů, musíme k přiřazení hodnot datových polí k odpovídajícím hodnotám webového ovládacího prvku použít syntaxi DataBinding. Syntaxi datové vazby lze použít prostřednictvím návrháře tak, že kliknete na obrazovku upravit šablony a vyberete odkaz Upravit datové vazby z inteligentních značek webového ovládacího prvku. Alternativně lze syntaxi datové vazby přidat přímo k deklarativnímu označení.

Přiřaďte hodnotu datového pole `ProductName` pro vlastnost `ProductName` TextBox s `Text`, hodnoty `CategoryID` a `SupplierID` datových polí pro `Categories` a `Suppliers` vlastnosti DropDownList `SelectedValue` a hodnotu pole `Discontinued` dat pro vlastnost `Discontinued` CheckBox s `Checked`. Po provedení těchto změn, buď prostřednictvím návrháře, nebo přímo prostřednictvím deklarativního označení, znovu přejděte na stránku pomocí prohlížeče a klikněte na tlačítko Upravit pro Anton Blend Gumbo. Jak ukazuje obrázek 9, syntaxe datové vazby přidala aktuální hodnoty do textového pole, DropDownList a CheckBox.

[![kliknutí na tlačítko Upravit zobrazí rozhraní pro úpravy.](customizing-the-datalist-s-editing-interface-vb/_static/image26.png)](customizing-the-datalist-s-editing-interface-vb/_static/image25.png)

**Obrázek 9**: kliknutím na tlačítko Upravit zobrazíte rozhraní pro úpravy (Kliknutím zobrazíte[obrázek v plné velikosti).](customizing-the-datalist-s-editing-interface-vb/_static/image27.png)

## <a name="step-5-saving-the-user-s-changes-in-the-updatecommand-event-handler"></a>Krok 5: uložení změn uživatele v obslužné rutině události UpdateCommand

Když uživatel upraví produkt a klikne na tlačítko Aktualizovat, dojde k postbacku a událost DataList `UpdateCommand` je aktivována. V obslužné rutině události musíme načíst hodnoty z webových ovládacích prvků v `EditItemTemplate` a rozhraní s knihoven BLL pro aktualizaci produktu v databázi. Jak jsme viděli v předchozích kurzech, `ProductID` aktualizovaného produktu je přístupný prostřednictvím kolekce `DataKeys`. Uživatelem zadaná pole jsou k dispozici programově odkazující na webové ovládací prvky pomocí `FindControl("controlID")`, jak ukazuje následující kód:

[!code-vb[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample4.vb)]

Kód začíná projednáním vlastnosti `Page.IsValid`, aby bylo zajištěno, že všechny ovládací prvky ověřování na stránce jsou platné. Pokud je `Page.IsValid` `True`, upraví se hodnota `ProductID` upravených produktů z kolekce `DataKeys` a na `EditItemTemplate` jsou odkazovány prostřednictvím ovládacího prvku webové ovládací prvky pro zadávání dat. Dále jsou hodnoty z těchto webových ovládacích prvků čteny do proměnných, které jsou následně předány příslušnému přetížení `UpdateProduct`. Po aktualizaci dat je prvek DataList vrácen do svého stavu před úpravou.

> [!NOTE]
> Jsem vynechal logiku zpracování výjimek přidanou v kurzu [zpracování výjimek knihoven BLL a dal](handling-bll-and-dal-level-exceptions-vb.md) , aby byl kód a tento příklad zaměřen. Jako cvičení přidejte tuto funkci po dokončení tohoto kurzu.

## <a name="step-6-handling-null-categoryid-and-supplierid-values"></a>Krok 6: zpracování hodnot KódKategorie a KódDodavatele s hodnotou NULL

Databáze Northwind umožňuje `NULL` hodnoty pro sloupce `Products` tabulky `CategoryID` a `SupplierID`. Naše rozhraní pro úpravy ale nesplňuje aktuálně `NULL` hodnoty. Pokud se pokusíte upravit produkt, který má `NULL` hodnotu pro `CategoryID` nebo `SupplierID` sloupce, obdržíme `ArgumentOutOfRangeException` s chybovou zprávou podobnou: *Categories má SelectedValue, která je neplatná, protože neexistuje v seznamu položek.* V současné době neexistuje způsob, jak změnit kategorii produktů nebo dodavatelů z ne`NULL`é hodnoty na `NULL` jedna.

Aby bylo možné podporovat `NULL` hodnoty pro DropDownList kategorie a dodavatele, musíme přidat další `ListItem`. Jsem se rozhodl použít (žádný) jako hodnotu `Text` pro tento `ListItem`, ale pokud chcete, můžete ho změnit na něco jiného (například prázdný řetězec). Nakonec nezapomeňte nastavit `AppendDataBoundItems` DropDownList na `True`; Pokud se k tomu zapomenete, kategorie a dodavatelé navázané na DropDownList přepíšou staticky přidávané `ListItem`.

Po provedení těchto změn by značky DropDownList v `EditItemTemplate` DataList měly vypadat podobně jako následující:

[!code-aspx[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample5.aspx)]

> [!NOTE]
> Statické `ListItem` s lze přidat k ovládacím prvkům DropDownList prostřednictvím návrháře nebo přímo prostřednictvím deklarativní syntaxe. Když přidáváte položku DropDownList představující `NULL`ovou hodnotu databáze, nezapomeňte přidat `ListItem` prostřednictvím deklarativní syntaxe. Použijete-li Editor kolekce `ListItem` v návrháři, vygenerovaná deklarativní syntaxe vynechá nastavení `Value` zcela v případě, že je přiřazen prázdný řetězec, čímž se vytvoří deklarativní označení jako: `<asp:ListItem>(None)</asp:ListItem>`. I když to může vypadat neškodně, chybějící `Value` způsobí, že vlastnost DropDownList použije hodnotu vlastnosti `Text` na svém místě. To znamená, že pokud je vybrána tato `NULL` `ListItem`, bude pokus o přiřazení hodnoty (None) k poli data produktu (`CategoryID` nebo `SupplierID`v tomto kurzu), což bude mít za následek výjimku. Když je explicitně nastavená možnost `Value=""`, do pole data produktu se přiřadí hodnota `NULL`, když se vybere `NULL` `ListItem`.

Chvilku si můžete prohlédnout v prohlížeči. Při úpravách produktu si všimněte, že `Categories` a `Suppliers` DropDownList mají obě možnost (žádná) na začátku ovládacího prvkem DropDownList.

[![kategorie a DropDownList pro dodavatele obsahují možnost (žádná).](customizing-the-datalist-s-editing-interface-vb/_static/image29.png)](customizing-the-datalist-s-editing-interface-vb/_static/image28.png)

**Obrázek 10**: ovládací `Categories` a `Suppliers` DropDownList obsahují možnost (žádná) ([kliknutím zobrazíte obrázek v plné velikosti).](customizing-the-datalist-s-editing-interface-vb/_static/image30.png)

Abychom mohli uložit možnost (žádné) jako hodnotu `NULL` databáze, musíme se vrátit k obslužné rutině události `UpdateCommand`. Změňte proměnné `categoryIDValue` a `supplierIDValue` na celá čísla s možnou hodnotou null a přiřaďte je jiné hodnotě než `Nothing` pouze v případě, že `SelectedValue` DropDownList s není prázdný řetězec:

[!code-vb[Main](customizing-the-datalist-s-editing-interface-vb/samples/sample6.vb)]

Tato změna způsobí, že hodnota `Nothing` bude předána metodě `UpdateProduct` knihoven BLL, pokud uživatel v některém z rozevíracích seznamů vybral možnost (žádné), která odpovídá hodnotě `NULL` databáze.

## <a name="summary"></a>Přehled

V tomto kurzu jsme viděli, jak vytvořit komplexnější rozhraní pro úpravy DataList, které zahrnulo tři různé vstupní webové ovládací prvky, jako je textové pole, dva DropDownList a zaškrtávací políčko společně s ovládacími prvky ověřování. Při sestavování rozhraní pro úpravy jsou tyto kroky stejné bez ohledu na používané webové ovládací prvky: Začněte přidáním webových ovládacích prvků do `EditItemTemplate`DataList s. pomocí syntaxe DataBinding přiřaďte odpovídající hodnoty datových polí odpovídajícím vlastnostem webového ovládacího prvku. a v obslužné rutině události `UpdateCommand` programově přistupují k webovým ovládacím prvkům a jejich příslušným vlastnostem, které předají jejich hodnoty do knihoven BLL.

Při vytváření rozhraní pro úpravy, bez ohledu na to, zda se skládají z pouze textových polí nebo kolekce různých webových ovládacích prvků, nezapomeňte správně zpracovat hodnoty `NULL` databáze. Při monitorování účtů pro `NULL`, je nutné, abyste v rozhraní pro úpravy nezobrazili pouze správně hodnotu `NULL`, ale také nabízíme způsob označení hodnoty jako `NULL`. Pro DropDownList v datalistech to obvykle znamená přidání statického `ListItem`, jehož vlastnost `Value` je explicitně nastavena na prázdný řetězec (`Value=""`), a přidání bitového kódu do `UpdateCommand` obslužné rutiny události pro určení, zda byl vybrán `NULL``ListItem` nebo nikoli.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Dennis Patterson, David Suru a Randy Schmidt. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](adding-validation-controls-to-the-datalist-s-editing-interface-vb.md)

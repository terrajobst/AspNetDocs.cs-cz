---
uid: web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-cs
title: Přidání tlačítek do ovládacího prvku GridView (C#) a reakce na ně | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se podíváme na postup, jak přidat vlastní tlačítka jak k šabloně, tak k polím ovládacího prvku GridView nebo DetailsView. Konkrétně pří...
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 128fdb5f-4c5e-42b5-b485-f3aee90a8e38
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-cs
msc.type: authoredcontent
ms.openlocfilehash: 5c87386e4fe2c53b39162071689f2522dcc6c7ac
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74602404"
---
# <a name="adding-and-responding-to-buttons-to-a-gridview-c"></a>Přidání tlačítek do ovládacího prvku GridView a reakce na ně (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_28_CS.exe) nebo [Stáhnout PDF](adding-and-responding-to-buttons-to-a-gridview-cs/_static/datatutorial28cs1.pdf)

> V tomto kurzu se podíváme na postup, jak přidat vlastní tlačítka jak k šabloně, tak k polím ovládacího prvku GridView nebo DetailsView. Konkrétně sestavíme rozhraní, které má FormView, který umožňuje uživateli stránkovat prostřednictvím dodavatelů.

## <a name="introduction"></a>Úvod

I když mnoho scénářů vytváření sestav zahrnuje přístup k datům sestavy jen pro čtení, není neobvyklá sestava, která by zahrnovala možnost provádět akce na základě zobrazených dat. Obvykle se jedná o přidání webového ovládacího prvku tlačítko, LinkButton nebo obrázkové s každým záznamem zobrazeným v sestavě, který po kliknutí způsobí postback a vyvolá nějaký kód na straně serveru. Nejčastějším příkladem je úpravy a odstranění dat na základě záznamu. Vzhledem k tomu, že jsme zjistili, že jsme začali s [přehledem vkládání, aktualizace a odstraňování dat](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) , jsou úpravy a odstraňování tak běžné, že ovládací prvky GridView, DetailsView a FormView můžou tyto funkce podporovat, aniž by bylo potřeba psát jediný řádek kódu.

Kromě tlačítek upravit a odstranit mohou ovládací prvky GridView, DetailsView a FormView obsahovat také tlačítka, LinkButtons nebo ImageButtons, které po kliknutí vyplní vlastní logiku na straně serveru. V tomto kurzu se podíváme na postup, jak přidat vlastní tlačítka jak k šabloně, tak k polím ovládacího prvku GridView nebo DetailsView. Konkrétně sestavíme rozhraní, které má FormView, který umožňuje uživateli stránkovat prostřednictvím dodavatelů. Pro daného dodavatele bude třída FormView zobrazovat informace o dodavateli spolu s webovým ovládacím prvkem tlačítko, který při kliknutí na něj označí všechny přidružené produkty jako ukončené. Kromě toho GridView zobrazí seznam produktů poskytovaných vybraným dodavatelem, přičemž každý řádek obsahuje tlačítka zvýšení ceny a slevy, které po kliknutí vyvolají nebo sníží `UnitPrice` produktu o 10% (viz obrázek 1).

[![FormView i GridView obsahují tlačítka, která provádějí vlastní akce.](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image2.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image1.png)

**Obrázek 1**: třída FormView a GridView obsahují tlačítka, která provádějí vlastní akce ([kliknutím zobrazíte obrázek v plné velikosti).](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image3.png)

## <a name="step-1-adding-the-button-tutorial-web-pages"></a>Krok 1: Přidání webových stránek s výukou k tlačítkům

Předtím, než se podíváme na postup, jak přidat vlastní tlačítka, nejdřív si vybereme chvilku, abychom vytvořili stránky ASP.NET v našem projektu webu, který budeme potřebovat pro tento kurz. Začněte přidáním nové složky s názvem `CustomButtons`. Dále přidejte do této složky následující dvě ASP.NET stránky a nezapomeňte přidružit jednotlivé stránky k hlavní stránce `Site.master`:

- `Default.aspx`
- `CustomButtons.aspx`

![Přidejte stránky ASP.NET pro vlastní kurzy související s tlačítky.](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image4.png)

**Obrázek 2**: přidejte stránky ASP.NET pro vlastní kurzy související s tlačítky.

Podobně jako v ostatních složkách `Default.aspx` ve složce `CustomButtons` vypíše kurzy v části. Zajistěte, aby tato funkce poskytovala `SectionLevelTutorialListing.ascx` uživatelský ovládací prvek. Proto tento uživatelský ovládací prvek přidejte do `Default.aspx` tím, že ho přetáhnete z Průzkumník řešení na zobrazení Návrh stránky.

[![přidat uživatelský ovládací prvek SectionLevelTutorialListing. ascx do default. aspx](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image6.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image5.png)

**Obrázek 3**: Přidání uživatelského ovládacího prvku `SectionLevelTutorialListing.ascx` do `Default.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image7.png))

Nakonec přidejte stránky jako položky do souboru `Web.sitemap`. Konkrétně přidejte následující značku po stránkování a řazení `<siteMapNode>`:

[!code-xml[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample1.xml)]

Po aktualizaci `Web.sitemap`chvíli počkejte, než se zobrazí web kurzy prostřednictvím prohlížeče. Nabídka na levé straně teď obsahuje položky pro kurzy pro úpravy, vkládání a odstraňování.

![Mapa webu teď obsahuje položku pro úvodní kurz pro vlastní tlačítka.](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image8.png)

**Obrázek 4**: Mapa webu teď obsahuje položku kurzu pro vlastní tlačítka.

## <a name="step-2-adding-a-formview-that-lists-the-suppliers"></a>Krok 2: Přidání třídy FormView se seznamem dodavatelů

Pojďme začít s tímto kurzem přidáním třídy FormView, která uvádí seznam dodavatelů. Jak je popsáno v úvodu, tato třída FormView umožní uživateli stránkovat prostřednictvím dodavatelů a zobrazuje produkty poskytované dodavatelem v prvku GridView. Kromě toho bude tato třída FormView obsahovat tlačítko, které při kliknutí označí všechny produkty dodavatele jako vyřazené. Předtím, než se budeme věnovat dodržovali přidáním vlastního tlačítka na FormView, pojďme nejdřív vytvořit FormView, aby se zobrazily informace o dodavateli.

Začněte tím, že otevřete stránku `CustomButtons.aspx` ve složce `CustomButtons`. Přidejte na stránku FormView přetažením z panelu nástrojů do návrháře a nastavte jeho vlastnost `ID` na hodnotu `Suppliers`. Z inteligentní značky FormView se můžete rozhodnout pro vytvoření nového prvku ObjectDataSource s názvem `SuppliersDataSource`.

[![vytvořit nový prvek ObjectDataSource s názvem SuppliersDataSource](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image10.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image9.png)

**Obrázek 5**: vytvoření nového prvku ObjectDataSource s názvem `SuppliersDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image11.png))

Nakonfigurujte tento nový prvek ObjectDataSource tak, aby se dotazoval z metody `GetSuppliers()` `SuppliersBLL` třídy (viz obrázek 6). Vzhledem k tomu, že tato třída FormView neposkytuje rozhraní pro aktualizaci informací o dodavatelích, vyberte v rozevíracím seznamu na kartě aktualizace možnost (žádná).

[![nakonfigurovat zdroj dat tak, aby používal metodu SuppliersBLL třídy s getdodavatelé ()](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image13.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image12.png)

**Obrázek 6**: Konfigurace zdroje dat pro použití metody `GetSuppliers()` `SuppliersBLL` třídy ([kliknutím zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image14.png))

Po nakonfigurování prvku ObjectDataSource bude aplikace Visual Studio generovat `InsertItemTemplate`, `EditItemTemplate`a `ItemTemplate` pro FormView. Odeberte `InsertItemTemplate` a `EditItemTemplate` a upravte `ItemTemplate` tak, aby se zobrazil pouze název společnosti dodavatele a telefonní číslo. Nakonec zapněte podporu stránkování pro FormView zaškrtnutím políčka Povolit stránkování z jeho inteligentní značky (nebo nastavením jeho vlastnosti `AllowPaging` na `True`). Po těchto změnách by deklarativní označení stránky mělo vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample2.aspx)]

Obrázek 7 zobrazuje stránku CustomButtons. aspx při prohlížení v prohlížeči.

[![ve třídě FormView jsou uvedena pole CompanyName a Phone z aktuálně vybraného dodavatele.](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image16.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image15.png)

**Obrázek 7**: třída FormView vypisuje pole `CompanyName` a `Phone` z aktuálně vybraného dodavatele ([kliknutím zobrazíte obrázek v plné velikosti).](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image17.png)

## <a name="step-3-adding-a-gridview-that-lists-the-selected-suppliers-products"></a>Krok 3: Přidání prvku GridView se seznamem produktů vybraných dodavatelů

Předtím, než přidáte do šablony třídy FormView tlačítko ukončit všechny produkty, nejprve přidáme prvek GridView pod objektem FormView, který obsahuje seznam produktů poskytovaných vybraným dodavatelem. Chcete-li toho dosáhnout, přidejte prvek GridView na stránku, nastavte jeho vlastnost `ID` na `SuppliersProducts`a přidejte nový prvek ObjectDataSource s názvem `SuppliersProductsDataSource`.

[![vytvořit nový prvek ObjectDataSource s názvem SuppliersProductsDataSource](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image19.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image18.png)

**Obrázek 8**: vytvoření nového prvku ObjectDataSource s názvem `SuppliersProductsDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image20.png))

Nakonfigurujte tuto ObjectDataSource tak, aby používala metodu `GetProductsBySupplierID(supplierID)` třídy ProductsBLL (viz obrázek 9). I když tento prvek GridView umožní úpravu ceny produktu, nepoužije integrované úpravy nebo odstranění funkcí z prvku GridView. Proto můžeme rozevírací seznam nastavit na (žádný) pro karty aktualizace, vložení a odstranění prvku ObjectDataSource.

[![nakonfigurovat zdroj dat tak, aby používal metodu ProductsBLL třídy s GetProductsBySupplierID (KódDodavatele)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image22.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image21.png)

**Obrázek 9**: Konfigurace zdroje dat pro použití metody `GetProductsBySupplierID(supplierID)` `ProductsBLL` třídy ([kliknutím zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image23.png))

Vzhledem k tomu, že metoda `GetProductsBySupplierID(supplierID)` přijímá vstupní parametr, průvodce ObjectDataSource zobrazí výzvu pro zdroj této hodnoty parametru. Chcete-li předat `SupplierID` hodnotu ze třídy FormView, nastavte rozevírací seznam zdroj parametru na hodnotu Control a rozevírací seznam ControlID na `Suppliers` (ID třídy FormView vytvořené v kroku 2).

[![označuje, že parametr KódDodavatele by měl pocházet z ovládacího prvku dodavatelé FormView.](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image25.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image24.png)

**Obrázek 10**: Určete, že parametr *`supplierID`* by měl pocházet z ovládacího prvku `Suppliers` FormView ([kliknutím zobrazíte obrázek v plné velikosti).](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image26.png)

Po dokončení průvodce ObjectDataSource bude ovládací prvek GridView obsahovat vlastnost BoundField nebo třídě CheckBoxField podporována pro každé z datových polí produktu. Pojďme to zkrátit, aby se zobrazily pouze `ProductName` a `UnitPrice` BoundFields spolu s `Discontinued` třídě CheckBoxField podporována; Navíc naformátujte `UnitPrice` vlastnost BoundField tak, aby byl jeho text formátován jako měna. Vaše GridView a `SuppliersProductsDataSource` deklarativní značky ObjectDataSource by měly vypadat podobně jako v následujícím kódu:

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample3.aspx)]

V tomto okamžiku náš kurz zobrazí sestavu hlavní/podrobnosti, která umožňuje uživateli vybrat ze třídy FormView v horní části a zobrazit produkty poskytované tímto dodavatelem v dolní části prvku GridView. Obrázek 11 znázorňuje snímek obrazovky této stránky při výběru dodavatele Tokio Traders ze třídy FormView.

[![vybrané produkty dodavatele se zobrazí v prvku GridView.](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image28.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image27.png)

**Obrázek 11**: produkty vybraného dodavatele se zobrazí v prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti).](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image29.png)

## <a name="step-4-creating-dal-and-bll-methods-to-discontinue-all-products-for-a-supplier"></a>Krok 4: vytvoření metod DAL a knihoven BLL pro oddálení všech produktů pro dodavatele

Před přidáním tlačítka do třídy FormView, který po kliknutí vypustí všechny produkty dodavatele, musíme nejdřív přidat metodu do DAL i do knihoven BLL, které tuto akci provádí. Konkrétně tato metoda bude pojmenována `DiscontinueAllProductsForSupplier(supplierID)`. Po kliknutí na tlačítko FormView vyvoláme tuto metodu ve vrstvě obchodní logiky, která předává `SupplierID`vybraného dodavatele; KNIHOVEN BLL pak zavolá do odpovídající metody vrstvy přístupu k datům, která vydá příkaz `UPDATE` do databáze, která ukončí produkty zadaného dodavatele.

Jak jsme udělali v předchozích kurzech, použijeme k tomu nejnižší přístup, počínaje vytvořením metody DAL, potom metodou knihoven BLL a nakonec implementací funkcí na stránce ASP.NET. Otevřete `Northwind.xsd` typovou datovou sadu ve složce `App_Code/DAL` a přidejte do `ProductsTableAdapter` novou metodu (klikněte pravým tlačítkem na `ProductsTableAdapter` a vyberte Přidat dotaz). Provedete to tak, že zobrazíte Průvodce konfigurací dotazu TableAdapter, který nás provede procesem přidání nové metody. Začněte tím, že určíte, že metoda DAL použije příkaz SQL ad-hoc.

[![vytvořit metodu DAL pomocí příkazu SQL ad hoc](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image31.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image30.png)

**Obrázek 12**: vytvoření metody dal pomocí ad-hoc příkazu SQL ([kliknutím zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image32.png))

V dalším kroku vás průvodce vyzve k zadání typu dotazu, který se má vytvořit. Vzhledem k tomu, že metoda `DiscontinueAllProductsForSupplier(supplierID)` bude muset aktualizovat `Products` databázovou tabulku, nastaví `Discontinued` pole na hodnotu 1 pro všechny produkty poskytované zadaným *`supplierID`* , musíme vytvořit dotaz, který aktualizuje data.

[![zvolit typ dotazu UPDATE](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image34.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image33.png)

**Obrázek 13**: Vyberte typ dotazu Update ([kliknutím zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image35.png)).

Další obrazovka průvodce poskytuje existující příkaz `UPDATE` TableAdapter, který aktualizuje všechna pole definovaná v `Products` DataTable. Nahraďte tento text dotazu následujícím příkazem:

[!code-sql[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample4.sql)]

Po zadání tohoto dotazu a kliknutí na tlačítko Další se zobrazí poslední obrazovka průvodce s názvem nové metody použít `DiscontinueAllProductsForSupplier`. Průvodce dokončíte kliknutím na tlačítko Dokončit. Po návratu do návrháře DataSet by se měla zobrazit nová metoda v `ProductsTableAdapter` s názvem `DiscontinueAllProductsForSupplier(@SupplierID)`.

[![název nové metody DAL DiscontinueAllProductsForSupplier](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image37.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image36.png)

**Obrázek 14**: pojmenování nové metody dal `DiscontinueAllProductsForSupplier` ([kliknutím zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image38.png))

S metodou `DiscontinueAllProductsForSupplier(supplierID)` vytvořenou ve vrstvě přístupu k datům je náš další úkol vytvoření metody `DiscontinueAllProductsForSupplier(supplierID)` ve vrstvě obchodní logiky. Chcete-li to provést, otevřete soubor třídy `ProductsBLL` a přidejte následující:

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample5.cs)]

Tato metoda jednoduše volá metodu `DiscontinueAllProductsForSupplier(supplierID)` v hodnotě DAL a předává se do poskytnuté *`supplierID`* hodnoty parametru. Pokud existovala nějaká obchodní pravidla, která za určitých okolností mají za následek, že produkty dodavatele mají za následek nedodržení, měla by být tato pravidla implementována v knihoven BLL.

> [!NOTE]
> Na rozdíl od přetížení `UpdateProduct` ve třídě `ProductsBLL` nezahrnuje signatura metody `DiscontinueAllProductsForSupplier(supplierID)` atribut `DataObjectMethodAttribute` (`<System.ComponentModel.DataObjectMethodAttribute(System.ComponentModel.DataObjectMethodType.Update, Boolean)>`). To vylučuje metodu `DiscontinueAllProductsForSupplier(supplierID)` z rozevíracího seznamu Průvodce konfigurací zdroje dat v prvku ObjectDataSource na kartě aktualizace. Jsem tento atribut vynechal, protože budeme volat metodu `DiscontinueAllProductsForSupplier(supplierID)` přímo z obslužné rutiny události na naší stránce ASP.NET.

## <a name="step-5-adding-a-discontinue-all-products-button-to-the-formview"></a>Krok 5: Přidání tlačítka ukončit všechny produkty do třídy FormView

V případě, že je v knihoven BLL a DAL k dis`DiscontinueAllProductsForSupplier(supplierID)` metoda a DAL, je posledním krokem pro přidání možnosti pro ukončení všech produktů pro vybraného dodavatele Přidání webového ovládacího prvku tlačítko do `ItemTemplate`FormView. Přidáme toto tlačítko pod telefonním číslem dodavatele s textem tlačítka, vynechá všechny produkty a `ID` hodnotu vlastnosti `DiscontinueAllProductsForSupplier`. Toto webové ovládací prvky můžete přidat prostřednictvím návrháře kliknutím na odkaz Upravit šablony v inteligentní značce třídy FormView (viz obrázek 15) nebo přímo prostřednictvím deklarativní syntaxe.

[![přidání webového ovládacího prvku tlačítko ukončit všechny produkty do třídy FormView s ItemTemplate](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image40.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image39.png)

**Obrázek 15**: Přidání webového ovládacího prvku tlačítko ukončit všechny produkty do `ItemTemplate` FormView ([kliknutím zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image41.png))

Když na tlačítko klikne uživatel, který navštíví stránku, vystavuje se postback a aktivuje se [`ItemCommand` událost](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.itemcommand.aspx) třídy FormView. Chcete-li spustit vlastní kód jako odpověď na toto tlačítko, můžeme vytvořit obslužnou rutinu události pro tuto událost. Seznamte se i v případě, že událost `ItemCommand` *aktivuje při každém* kliknutí na tlačítko, LinkButton nebo webový ovládací prvek obrázkové ve třídě FormView. To znamená, že když se uživatel přesune z jedné stránky na jinou ve třídě FormView, aktivuje se `ItemCommand` událost; stejné, když uživatel klikne na nové, upravit nebo odstranit ve třídě FormView, která podporuje vložení, aktualizaci nebo odstranění.

Vzhledem k tomu, že se `ItemCommand` aktivuje bez ohledu na to, na jaké tlačítko jste klikli, potřebuje v obslužné rutině události, abyste zjistili, jestli jste klikli na tlačítko ukončit všechny produkty, nebo jestli se jednalo o nějaké jiné tlačítko. K tomu můžeme nastavit vlastnost `CommandName` webového ovládacího prvku tlačítko na určitou identifikační hodnotu. Po kliknutí na tlačítko se tato hodnota `CommandName` předává do obslužné rutiny události `ItemCommand` a umožňuje nám určit, zda bylo tlačítko ukončit všechny produkty kliknuto na tlačítko. Nastavte vlastnost `CommandName` tlačítka pro všechny produkty na hodnotu DiscontinueProducts.

Nakonec použijeme dialogové okno pro potvrzení na straně klienta, které zajistí, že uživatel bude chtít, aby produkt vybraným dodavatelem nepokračoval. Vzhledem k tomu, že jsme [při odstraňování kurzu viděli potvrzení na straně klienta](../editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs.md) , můžete to provést pomocí bitu JavaScriptu. Konkrétně nastavte vlastnost OnClientClick webového ovládacího prvku tlačítko na hodnotu `return confirm('This will mark _all_ of this supplier\'s products as discontinued. Are you certain you want to do this?');`

Po provedení těchto změn by deklarativní syntaxe třídy FormView vypadala takto:

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample6.aspx)]

Dále vytvořte obslužnou rutinu události pro událost `ItemCommand` třídy FormView. V této obslužné rutině je třeba nejprve určit, zda bylo stisknuto tlačítko ukončit všechny produkty. Pokud ano, chceme vytvořit instanci třídy `ProductsBLL` a vyvolat svoji `DiscontinueAllProductsForSupplier(supplierID)` metodu, která předává `SupplierID` vybrané třídy FormView:

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample7.cs)]

Všimněte si, že `SupplierID` aktuálně vybraného dodavatele ve třídě FormView lze použít [vlastnost`SelectedValue`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.selectedvalue.aspx)třídy FormView. Vlastnost `SelectedValue` vrací první hodnotu datového klíče pro záznam, který se zobrazuje ve třídě FormView. [Vlastnost`DataKeyNames`](https://msdn.microsoft.com/system.web.ui.webcontrols.formview.datakeynames.aspx)třídy FormView, která označuje datová pole, ze kterých jsou načteny hodnoty datových klíčů, byla automaticky nastavena na `SupplierID` sadou Visual Studio při svázání prvku ObjectDataSource s nástrojem FormView zpět v kroku 2.

Když je vytvořená obslužná rutina události `ItemCommand`, chvíli otestujte stránku. Přejděte na dodavatele Cooperativa de quesos "Las Cabras (je to pátý dodavatel ve třídě FormView pro mě). Tento dodavatel poskytuje dva produkty, queso Cabrales a Queso Manchego La PAStore, *které nejsou* ukončeny.

Představte si, že Cooperativa de quesos "Las Cabras" zmizela z podnikání, takže jeho produkty mají být ukončeny. Klikněte na tlačítko ukončit všechny produkty. Zobrazí se dialogové okno pro potvrzení na straně klienta (viz obrázek 16).

[![Cooperativa de quesos Las Cabras nabízí dva aktivní produkty](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image43.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image42.png)

**Obrázek 16**: Cooperativa de quesos Las Cabras nabízí dva aktivní produkty ([kliknutím zobrazíte obrázek v plné velikosti).](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image44.png)

Pokud kliknete na tlačítko OK v dialogovém okně potvrzení na straně klienta, bude odesílání formuláře pokračovat, což způsobí postback, ve kterém bude vyvolána událost `ItemCommand` třídy FormView. Obslužná rutina události, kterou jsme vytvořili, se pak spustí, vyvolá metodu `DiscontinueAllProductsForSupplier(supplierID)` a nepokračuje v produktech queso Cabrales a Queso Manchego La PAStore.

Pokud jste zakázali stav zobrazení prvku GridView, je prvek GridView při každém zpětném odeslání svázán s podkladovým úložištěm dat, a proto bude okamžitě aktualizován, aby odrážel, že tyto dva produkty jsou nyní ukončeny (viz obrázek 17). Pokud však v prvku GridView není zakázán stav zobrazení, budete muset po provedení této změny ručně znovu vytvořit vazby dat na prvek GridView. K tomuto účelu jednoduše zavolejte metodu `DataBind()` prvku GridView ihned po vyvolání metody `DiscontinueAllProductsForSupplier(supplierID)`.

[![po kliknutí na tlačítko ukončit všechny produkty se odpovídajícím způsobem aktualizují produkty dodavatele.](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image46.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image45.png)

**Obrázek 17**: po kliknutí na tlačítko ukončit všechny produkty se odpovídajícím způsobem aktualizují produkty dodavatele ([kliknutím zobrazíte obrázek v plné velikosti](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image47.png)).

## <a name="step-6-creating-an-updateproduct-overload-in-the-business-logic-layer-for-adjusting-a-products-price"></a>Krok 6: vytvoření přetížení UpdateProduct ve vrstvě obchodní logiky pro úpravu ceny produktu

Podobně jako u tlačítka ukončit všechny produkty ve třídě FormView, aby bylo možné přidat tlačítka pro zvýšení a snížení ceny pro produkt v prvku GridView, je nutné nejprve přidat příslušnou vrstvu pro přístup k datům a metody vrstvy obchodní logiky. Vzhledem k tomu, že už máme metodu, která aktualizuje jeden řádek produktu na DAL, můžeme tyto funkce poskytnout vytvořením nového přetížení pro metodu `UpdateProduct` v knihoven BLL.

Naše starší `UpdateProduct` přetížení povedla v některé kombinaci polí produktu jako skalárních vstupních hodnot a pak aktualizovala pouze ta pole pro zadaný produkt. Pro toto přetížení se mírně liší od tohoto standardu a místo toho se předává `ProductID` a procento, podle kterého se `UnitPrice` (na rozdíl od předání v novém upravený `UnitPrice` sám). Tento přístup zjednodušuje kód, který potřebujeme pro zápis do třídy ASP.NET stránky s kódem na pozadí, protože nemusíme bother s určením `UnitPrice`aktuálního produktu.

`UpdateProduct` přetížení tohoto kurzu vidíte níže:

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample8.cs)]

Toto přetížení načte informace o zadaném produktu prostřednictvím metody `GetProductByProductID(productID)` DAL. Pak zkontroluje, jestli je `UnitPrice` produktu přiřazená `NULL` hodnota databáze. V takovém případě je cena ponechána beze změny. Pokud však existuje hodnota `UnitPrice`, která není`NULL`, metoda aktualizuje `UnitPrice` produktu pomocí zadaného procenta (`unitPriceAdjustmentPercent`).

## <a name="step-7-adding-the-increase-and-decrease-buttons-to-the-gridview"></a>Krok 7: Přidání tlačítek zvětšit a zmenšit do prvku GridView.

Prvek GridView (a DetailsView) se skládá z kolekce polí. Kromě BoundFields, CheckBoxFields a TemplateFields ASP.NET zahrnuje ButtonField, což znamená, že jako název napovídá, vykreslí jako sloupec s tlačítkem, LinkButton nebo obrázkové pro každý řádek. Podobně jako u třídy FormView, kliknutí na *jakékoli* tlačítko v rámci tlačítek stránkování ovládacího prvku GridView, tlačítka upravit nebo odstranit, tlačítka řazení a tak v důsledku způsobí postback a vyvolá [událost`RowCommand`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowcommand.aspx)prvku GridView.

ButtonField má vlastnost `CommandName`, která přiřadí zadanou hodnotu každému tlačítku `CommandName` vlastností. Podobně jako u třídy FormView je hodnota `CommandName` používána obslužnou rutinou události `RowCommand` k určení, na které tlačítko bylo kliknuto.

Pojďme do prvku GridView přidat dvě nové ButtonFields, jednu s textem tlačítka + 10% a druhou s textovou cenou – 10%. Chcete-li přidat tyto ButtonFields, klikněte na odkaz Upravit sloupce z inteligentní značky GridView, vyberte typ pole ButtonField ze seznamu v levém horním rohu a klikněte na tlačítko Přidat.

![Přidání dvou ButtonFields do prvku GridView.](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image48.png)

**Obrázek 18**: přidání dvou ButtonFields do prvku GridView.

Přesuňte dva ButtonFields tak, aby se zobrazily jako první dvě pole GridView. V dalším kroku nastavte vlastnosti `Text` těchto dvou ButtonFields na Price + 10% a Price 10% a `CommandName` vlastnosti na IncreasePrice a DecreasePrice, v uvedeném pořadí. Ve výchozím nastavení vykreslí ButtonField svůj sloupec tlačítek jako LinkButtons. To však může být změněno prostřednictvím [vlastnosti`ButtonType`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.buttonfieldbase.buttontype.aspx)ButtonField. Pojďme mít tyto dva ButtonFieldsy vykreslené jako běžná nabízená tlačítka; Proto nastavte vlastnost `ButtonType` na hodnotu `Button`. Obrázek 19: po provedení těchto změn se zobrazí dialogové okno pole. Následuje deklarativní označení ovládacího prvku GridView.

![Konfigurace vlastností ButtonFields text, Command a ButtonType](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image49.png)

**Obrázek 19**: Konfigurace vlastností ButtonFields `Text`, `CommandName`a `ButtonType`

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample9.aspx)]

Pomocí těchto ButtonFields vytvořených je posledním krokem vytvoření obslužné rutiny události pro událost `RowCommand` prvku GridView. Tato obslužná rutina události, je-li vyvolána, protože došlo ke kliknutí na tlačítko cena + 10% nebo cena-10%, musí určit `ProductID` řádku, pod kterým bylo tlačítko kliknuto, a poté vyvolat `UpdateProduct` metodu `ProductsBLL` třídy, a přitom předat příslušné `UnitPrice` procentuální úpravu společně s `ProductID`. Následující kód provádí tyto úlohy:

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample10.cs)]

Aby bylo možné určit `ProductID` řádku, jehož cena + 10% nebo tlačítko Price 10% bylo kliknuto, musíme se obrátit na kolekci `DataKeys` prvku GridView. V této kolekci jsou uloženy hodnoty polí určených vlastností `DataKeyNames` pro každý řádek prvku GridView. Vzhledem k tomu, že vlastnost `DataKeyNames` prvku GridView byla nastavena na hodnotu ProductID sadou Visual Studio při vázání prvku ObjectDataSource na prvek GridView, `DataKeys(rowIndex).Value` poskytuje `ProductID` pro zadaný *RowIndex*.

ButtonField automaticky předává do *RowIndex* řádku, na jehož tlačítko jste klikli pomocí parametru `e.CommandArgument`. Proto pro určení `ProductID` řádku, jehož cena + 10% nebo tlačítko Price 10% bylo kliknuto, používáme: `Convert.ToInt32(SuppliersProducts.DataKeys(Convert.ToInt32(e.CommandArgument)).Value)`.

Stejně jako u tlačítka ukončit všechny produkty, pokud jste zakázali stav zobrazení prvku GridView, je prvek GridView při každém zpětném odeslání svázán s podkladovým úložištěm dat, a proto bude okamžitě aktualizován, aby odrážel změnu ceny, ke které dojde kliknutím jedno z tlačítek. Pokud však v prvku GridView není zakázán stav zobrazení, budete muset po provedení této změny ručně znovu vytvořit vazby dat na prvek GridView. K tomuto účelu jednoduše zavolejte metodu `DataBind()` prvku GridView ihned po vyvolání metody `UpdateProduct`.

Obrázek 20 zobrazuje stránku při prohlížení produktů poskytovaných Homesteadem Grandma Kelly. Obrázek 21 zobrazuje výsledky po kliknutí na tlačítko ceny + 10% dvakrát pro Boysenberry rozprostření Grandma a pro Northwoods Cranberry omáčka tlačítko Price-10%.

[![obsahuje tlačítko Price + 10% a cena-10%](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image51.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image50.png)

**Obrázek 20**: tlačítka pro GridView obsahuje cenu + 10% a cenu-10% ([kliknutím zobrazíte obrázek v plné velikosti).](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image52.png)

[![ceny za první a třetí produkt byly aktualizovány prostřednictvím tlačítek ceny + 10% a cena-10%.](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image54.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image53.png)

**Obrázek 21**: ceny za první a třetí produkt byly aktualizovány prostřednictvím tlačítek Price + 10% a Price 10% ([kliknutím zobrazíte obrázek v plné velikosti).](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image55.png)

> [!NOTE]
> Prvky GridView (a DetailsView) mohou mít také tlačítka, LinkButtons nebo ImageButtons přidané do jejich TemplateFields. Stejně jako u vlastnost BoundField, tato tlačítka při kliknutí způsobí vyvolání zpětného volání a vyvolává událost `RowCommand` prvku GridView. Při přidávání tlačítek v poli TemplateField se ale `CommandArgument` tlačítka automaticky nenastaví na index řádku, protože se používá ButtonFields. Pokud potřebujete určit index řádku tlačítka, které bylo kliknuto v rámci obslužné rutiny události `RowCommand`, je nutné ručně nastavit vlastnost `CommandArgument` tlačítka v jeho deklarativní syntaxi v elementu TemplateField pomocí kódu, jako je:  
> `<asp:Button runat="server" ... CommandArgument='<%# ((GridViewRow) Container).RowIndex %>'`.

## <a name="summary"></a>Přehled

Všechny ovládací prvky GridView, DetailsView a FormView mohou zahrnovat tlačítka, LinkButtons nebo ImageButtons. Taková tlačítka, když je kliknuto, způsobují zpětné odeslání a vyvolávají událost `ItemCommand` v ovládacích prvcích FormView a DetailsView `RowCommand` a v prvku GridView. Tato webová ovládací prvky obsahují integrovanou funkci pro zpracování běžných akcí souvisejících s příkazy, jako je například odstraňování nebo úpravy záznamů. Můžete ale také použít tlačítka, která při kliknutí reagují na vlastní vlastní kód.

K tomu musíme vytvořit obslužnou rutinu události pro událost `ItemCommand` nebo `RowCommand`. V této obslužné rutině události nejdřív zkontrolujeme hodnotu příchozího `CommandName` a určíte, na které tlačítko se kliknulo, a pak se provede vhodná vlastní akce. V tomto kurzu jsme viděli, jak používat tlačítka a ButtonFields k tomu, aby všechny produkty pro zadaného dodavatele nepokračovaly, nebo zvýšili nebo snížili cenu určitého produktu o 10%.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Next](adding-and-responding-to-buttons-to-a-gridview-vb.md)

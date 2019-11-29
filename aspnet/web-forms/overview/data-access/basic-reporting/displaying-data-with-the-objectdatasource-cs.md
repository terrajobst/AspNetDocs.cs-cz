---
uid: web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-cs
title: Zobrazení dat s ovládacím prvkem ObjectDataSourceC#() | Microsoft Docs
author: rick-anderson
description: Tento kurz se zabývá ovládacím prvkem ObjectDataSource pomocí tohoto ovládacího prvku můžete navazovat data získaná z knihoven BLL vytvořených v předchozím kurzu bez Havi...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: af882aef-56f5-4e9a-8f95-3977fde20e74
msc.legacyurl: /web-forms/overview/data-access/basic-reporting/displaying-data-with-the-objectdatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: 9419504ace15b39c35a034dda22f2700ee720157
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74608918"
---
# <a name="displaying-data-with-the-objectdatasource-c"></a>Zobrazení dat ovládacím prvkem ObjectDataSource (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_4_CS.exe) nebo [Stáhnout PDF](displaying-data-with-the-objectdatasource-cs/_static/datatutorial04cs1.pdf)

> Tento kurz se zabývá ovládacím prvkem ObjectDataSource pomocí tohoto ovládacího prvku můžete navazovat data získaná z knihoven BLL vytvořených v předchozím kurzu, aniž byste museli psát řádek kódu.

## <a name="introduction"></a>Úvod

Po dokončení naší architektury aplikace a rozložení stránky webu jsme připraveni začít zkoumat, jak provádět různé běžné úlohy související s daty a vytvářením sestav. V předchozích kurzech jsme viděli, jak programově navazovat data z DAL a knihoven BLL na datovou webovou stránku na ASP.NET stránce. Tato syntaxe přiřazuje vlastnost `DataSource` webového ovládacího prvku data k zobrazení dat, která se zobrazí, a poté volání metody `DataBind()` ovládacího prvku byla vzorem použitým v aplikacích v ASP.NET 1. x a lze nadále používat v aplikacích 2,0. Nové ovládací prvky zdroje dat ASP.NET 2.0 však nabízejí deklarativní způsob, jak pracovat s daty. Pomocí těchto ovládacích prvků můžete navazovat data získaná z knihoven BLL vytvořených v [předchozím kurzu](../introduction/creating-a-business-logic-layer-cs.md) , aniž byste museli psát řádek kódu.

ASP.NET 2,0 dodává s pěti vestavěnými ovládacími prvky zdroje dat [SqlDataSource](https://msdn.microsoft.com/library/dz12d98w(vs.80).aspx), [AccessDataSource](https://msdn.microsoft.com/library/8e5545e1.aspx), [ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx), [XmlDataSource](https://msdn.microsoft.com/library/e8d8587a(en-US,VS.80).aspx)a [SiteMapDataSource](https://msdn.microsoft.com/library/5ex9t96x(en-US,VS.80).aspx) , i když v případě potřeby můžete vytvořit vlastní [ovládací prvky zdroje dat](https://msdn.microsoft.com/library/default.asp?url=/library/dnvs05/html/DataSourceCon1.asp). Vzhledem k tomu, že jsme vyvinuli architekturu pro naši aplikaci kurzu, budeme používat prvek ObjectDataSource pro naše třídy knihoven BLL.

![ASP.NET 2,0 zahrnuje pět vestavěných ovládacích prvků zdroje dat.](displaying-data-with-the-objectdatasource-cs/_static/image1.png)

**Obrázek 1**: ASP.NET 2,0 zahrnuje pět vestavěných ovládacích prvků zdroje dat.

Prvek ObjectDataSource slouží jako proxy server pro práci s nějakým jiným objektem. Pro konfiguraci prvku ObjectDataSource určíme tento základní objekt a způsob, jakým jsou metody mapovány na `Select`, `Insert`, `Update`a `Delete` metody ObjectDataSource prvku ObjectDataSource. Po zadání tohoto podkladového objektu a jeho metod, které jsou namapované na prvek ObjectDataSource, můžeme následně vytvořit vazby prvku ObjectDataSource k datovému ovládacímu prvku Web. ASP.NET se dodává s mnoha webovými ovládacími prvky dat, včetně prvku GridView, DetailsView, RadioButtonList a DropDownList, mimo jiné. Během životního cyklu stránky může webový ovládací prvek data potřebovat přístup k datům, ke kterým je svázán, který bude plnit vyvoláním metody `Select` prvku ObjectDataSource. Pokud webový ovládací prvek data podporuje vložení, aktualizaci nebo odstranění, mohou být volání v rámci `Insert`, `Update`nebo `Delete` metod prvku ObjectDataSource. Tato volání jsou poté směrována v prvku ObjectDataSource do příslušných metod podkladového objektu, jak ukazuje následující diagram.

[![prvek ObjectDataSource slouží jako proxy](displaying-data-with-the-objectdatasource-cs/_static/image3.png)](displaying-data-with-the-objectdatasource-cs/_static/image2.png)

**Obrázek 2**: prvek ObjectDataSource slouží jako proxy ([kliknutím zobrazíte obrázek v plné velikosti).](displaying-data-with-the-objectdatasource-cs/_static/image4.png)

I když prvek ObjectDataSource lze použít k vyvolání metod pro vložení, aktualizaci nebo odstranění dat, můžeme se zaměřit jenom na vracení dat; v budoucích kurzech se naučíte používat ovládací prvky ObjectDataSource a data web, které upravují data.

## <a name="step-1-adding-and-configuring-the-objectdatasource-control"></a>Krok 1: Přidání a konfigurace ovládacího prvku ObjectDataSource

Začněte tím, že otevřete stránku `SimpleDisplay.aspx` ve složce `BasicReporting`, přepnete do zobrazení Návrh a pak přetáhnete ovládací prvek ObjectDataSource ze sady nástrojů na návrhovou plochu stránky. Prvek ObjectDataSource se zobrazí jako šedé pole na návrhové ploše, protože nevytváří žádné značky; jednoduše přistupuje k datům vyvoláním metody ze zadaného objektu. Data vrácená prvkem ObjectDataSource lze zobrazit pomocí webového ovládacího prvku dat, například GridView, DetailsView, FormView a tak dále.

> [!NOTE]
> Alternativně můžete přidat webové ovládací prvek data na stránku a poté z jeho inteligentní značky zvolit&gt; možnost &lt;nový zdroj dat v rozevíracím seznamu.

Chcete-li určit podkladový objekt prvku ObjectDataSource a způsob mapování metod tohoto objektu na prvek ObjectDataSource, klikněte na odkaz konfigurace zdroje dat z inteligentní značky ObjectDataSource.

[![klikněte na odkaz konfigurace zdroje dat z inteligentní značky.](displaying-data-with-the-objectdatasource-cs/_static/image6.png)](displaying-data-with-the-objectdatasource-cs/_static/image5.png)

**Obrázek 3**: klikněte na odkaz konfigurace zdroje dat z inteligentní značky ([kliknutím zobrazíte obrázek v plné velikosti).](displaying-data-with-the-objectdatasource-cs/_static/image7.png)

Tím se zobrazí Průvodce konfigurací zdroje dat. Nejdříve je nutné zadat objekt, se kterým má prvek ObjectDataSource pracovat. Pokud je zaškrtnuto políčko Zobrazit pouze datové součásti, rozevírací seznam na této obrazovce obsahuje pouze objekty, které byly upraveny pomocí atributu `DataObject`. V současné době seznam obsahuje objekty TableAdapter do typové datové sady a třídy knihoven BLL, které jsme vytvořili v předchozím kurzu. Pokud jste zapomněli přidat atribut `DataObject` do tříd vrstvy obchodní logiky, neuvidíte je v tomto seznamu. V takovém případě zrušte zaškrtnutí políčka Zobrazit pouze datové součásti, aby se zobrazily všechny objekty, které by měly zahrnovat třídy knihoven BLL (spolu s jinými třídami v typové datové sadě, které tvoří DataTables, DataRows atd.).

Z první obrazovky vyberte v rozevíracím seznamu třídu `ProductsBLL` a klikněte na další.

[![určení objektu, který se má použít s ovládacím prvkem ObjectDataSource](displaying-data-with-the-objectdatasource-cs/_static/image9.png)](displaying-data-with-the-objectdatasource-cs/_static/image8.png)

**Obrázek 4**: určení objektu, který se má použít s ovládacím prvkem ObjectDataSource ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-objectdatasource-cs/_static/image10.png))

Na další obrazovce průvodce se zobrazí výzva, abyste vybrali metodu, kterou má prvek ObjectDataSource vyvolat. Rozevírací seznam obsahuje metody, které vracejí data v objektu vybraném z předchozí obrazovky. Tady vidíte `GetProductByProductID`, `GetProducts`, `GetProductsByCategoryID`a `GetProductsBySupplierID`. V rozevíracím seznamu vyberte metodu `GetProducts` a klikněte na Dokončit (Pokud jste `DataObjectMethodAttribute` přidali do metod `ProductBLL`, jak je znázorněno v předchozím kurzu, tato možnost bude ve výchozím nastavení vybraná.

[![zvolte metodu vrácení dat z karty vybrat.](displaying-data-with-the-objectdatasource-cs/_static/image12.png)](displaying-data-with-the-objectdatasource-cs/_static/image11.png)

**Obrázek 5**: zvolte metodu vrácení dat z karty vybrat ([kliknutím zobrazíte obrázek v plné velikosti).](displaying-data-with-the-objectdatasource-cs/_static/image13.png)

## <a name="configure-the-objectdatasource-manually"></a>Ruční konfigurace prvku ObjectDataSource

Průvodce konfigurací zdroje dat prvku ObjectDataSource nabízí rychlý způsob určení objektu, který používá, a k přidružení toho, jaké metody objektu jsou vyvolány. Prvek ObjectDataSource lze však nakonfigurovat prostřednictvím jeho vlastností, a to buď pomocí okno Vlastnosti, nebo přímo v deklarativní značce. Jednoduše nastavte vlastnost `TypeName` na typ podkladového objektu, který má být použit, a `SelectMethod` na metodu, která má být vyvolána při načítání dat.

[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample1.aspx)]

I v případě, že dáváte přednost průvodci konfigurací zdroje dat, může nastat situace, kdy potřebujete manuálně nakonfigurovat prvek ObjectDataSource, protože Průvodce uvádí pouze třídy vytvořené vývojářem. Pokud chcete prvek ObjectDataSource navážete na třídu v .NET Framework, jako je například [Třída členství](https://msdn.microsoft.com/library/system.web.security.membership.aspx), získat přístup k informacím o uživatelském účtu nebo [třídu adresáře](https://msdn.microsoft.com/library/system.io.directory.aspx) pro práci s informacemi o systému souborů, budete muset ručně nastavit vlastnosti prvku ObjectDataSource.

## <a name="step-2-adding-a-data-web-control-and-binding-it-to-the-objectdatasource"></a>Krok 2: Přidání webového ovládacího prvku data a jeho svázání s prvkem ObjectDataSource

Po přidání prvku ObjectDataSource na stránku a nakonfigurování je připraveno Přidat datovou webovou ovládací prvky na stránku, aby se zobrazila data vrácená metodou `Select` prvku ObjectDataSource. Jakýkoli ovládací prvek data web může být svázán s prvkem ObjectDataSource; Podívejme se, jak zobrazit data ovládacího prvku ObjectDataSource v prvku GridView, DetailsView a FormView.

## <a name="binding-a-gridview-to-the-objectdatasource"></a>Vazba prvku GridView na prvek ObjectDataSource

Přidejte ovládací prvek GridView z panelu nástrojů na návrhovou plochu `SimpleDisplay.aspx`. Z inteligentní značky GridView vyberte ovládací prvek ObjectDataSource, který jsme přidali v kroku 1. Tím se automaticky vytvoří vlastnost BoundField v prvku GridView pro každou vlastnost vrácenou daty z metody `Select` prvku ObjectDataSource (konkrétně do vlastností definovaných v objektu DataTable Products).

[![ovládací prvek GridView byl přidán na stránku a svázán s prvkem ObjectDataSource](displaying-data-with-the-objectdatasource-cs/_static/image15.png)](displaying-data-with-the-objectdatasource-cs/_static/image14.png)

**Obrázek 6**: ovládací prvek GridView byl přidán na stránku a svázán s prvkem ObjectDataSource ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-objectdatasource-cs/_static/image16.png)).

Pak můžete přizpůsobit, změnit uspořádání nebo odebrat BoundFields prvku GridView kliknutím na možnost Upravit sloupce z inteligentní značky.

[![spravovat BoundFields ovládacího prvku GridView přes dialogové okno Upravit sloupce](displaying-data-with-the-objectdatasource-cs/_static/image18.png)](displaying-data-with-the-objectdatasource-cs/_static/image17.png)

**Obrázek 7**: Správa BoundFields prvku GridView pomocí dialogového okna Upravit sloupce ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-objectdatasource-cs/_static/image19.png))

Chvíli počkejte, než se upraví BoundFields prvku GridView, odebrání `ProductID`, `SupplierID`, `CategoryID`, `QuantityPerUnit`, `UnitsInStock`, `UnitsOnOrder`a `ReorderLevel` BoundFields. Jednoduše vyberte vlastnost BoundField ze seznamu vlevo dole a kliknutím na tlačítko Odstranit (červené X) je odeberte. Dále znovu uspořádejte BoundFields, aby `CategoryName` a `SupplierName` BoundFields před `UnitPrice` vlastnost BoundField, a to tak, že je vyberete a kliknete na šipku nahoru. Nastavte vlastnosti `HeaderText` zbývajícího BoundFields na `Products`, `Category`, `Supplier`a `Price`v uvedeném pořadí. V dalším kroku nastavte `Price` vlastnost BoundField naformátované jako měnu nastavením vlastnosti `HtmlEncode` vlastnosti vlastnost BoundField na false a vlastnost `DataFormatString` na `{0:c}`. Nakonec vodorovně zarovnejte `Price` napravo a `Discontinued` zaškrtávací políčko v centru prostřednictvím vlastnosti `ItemStyle`/`HorizontalAlign`.

[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample2.aspx)]

[![přizpůsobení BoundFields prvku GridView.](displaying-data-with-the-objectdatasource-cs/_static/image21.png)](displaying-data-with-the-objectdatasource-cs/_static/image20.png)

**Obrázek 8**: vlastní BoundFields ovládacího prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-objectdatasource-cs/_static/image22.png))

## <a name="using-themes-for-a-consistent-look"></a>Použití motivů pro konzistentní vzhled

Tyto kurzy se snaží odebrat jakákoli nastavení stylu na úrovni ovládacího prvku namísto použití kaskádových šablon stylů definovaných v externím souboru, kdykoli je to možné. `Styles.css` soubor obsahuje třídy `DataWebControlStyle`, `HeaderStyle`, `RowStyle`a `AlternatingRowStyle`, které by měly být použity k diktování vzhledu webových ovládacích prvků dat používaných v těchto kurzech. K tomu můžeme nastavit vlastnost `CssClass` prvku GridView na `DataWebControlStyle`a příslušné vlastnosti `HeaderStyle`, `RowStyle`a `AlternatingRowStyle` `CssClass` odpovídajícím způsobem.

Pokud tyto `CssClass` vlastnosti nastavíme na webovém ovládacím prvku, musíme si pamatovat explicitně tyto hodnoty vlastností pro každý a každý webový ovládací prvek dat přidaný do našich kurzů. Lépe spravovatelnější přístup je definování výchozích vlastností souvisejících s CSS pro ovládací prvky GridView, DetailsView a FormView pomocí motivu. Motiv je kolekce nastavení vlastností na úrovni ovládacího prvku, obrázků a tříd šablon stylů CSS, které lze použít na stránky v rámci lokality, aby se vynutil běžný vzhled a chování.

Náš motiv nebude obsahovat žádné obrázky ani soubory CSS (šablonu stylů ponecháme `Styles.css`, jak je definováno v kořenové složce webové aplikace), ale bude obsahovat dvě vzhledy. Skin je soubor, který definuje výchozí vlastnosti pro webový ovládací prvek. Konkrétně budeme mít soubor skinu pro ovládací prvky GridView a DetailsView, které označují výchozí vlastnosti `CssClass`.

Začněte přidáním nového souboru skinu do projektu s názvem `GridView.skin` tak, že kliknete pravým tlačítkem myši na název projektu v Průzkumník řešení a zvolíte přidat novou položku.

[![přidat soubor skinu s názvem GridView. Skin](displaying-data-with-the-objectdatasource-cs/_static/image24.png)](displaying-data-with-the-objectdatasource-cs/_static/image23.png)

**Obrázek 9**: přidejte soubor skinu s názvem `GridView.skin` ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-objectdatasource-cs/_static/image25.png)).

Soubory skinu je nutné umístit do motivu, který je umístěn ve složce `App_Themes`. Vzhledem k tomu, že tuto složku ještě nemáte, Visual Studio vám při přidávání našeho prvního vzhledu nabídne vytvoření pro nás. Klikněte na Ano, pokud chcete vytvořit složku `App_Theme` a umístit do ní nový soubor `GridView.skin`.

[![nechat aplikaci Visual Studio vytvořit složku App_Theme](displaying-data-with-the-objectdatasource-cs/_static/image27.png)](displaying-data-with-the-objectdatasource-cs/_static/image26.png)

**Obrázek 10**: Umožněte aplikaci Visual Studio vytvořit složku `App_Theme` ([kliknutím zobrazíte obrázek v plné velikosti).](displaying-data-with-the-objectdatasource-cs/_static/image28.png)

Tím se vytvoří nový motiv ve složce `App_Themes` s názvem GridView se souborem Skin `GridView.skin`.

![Motiv GridView byl přidán do složky App_Theme](displaying-data-with-the-objectdatasource-cs/_static/image29.png)

**Obrázek 11**: motiv GridView byl přidán do složky `App_Theme`

Přejmenujte motiv GridView na DataWebControls (klikněte pravým tlačítkem myši na složku GridView ve složce `App_Theme` a vyberte příkaz Přejmenovat). Dále do souboru `GridView.skin` zadejte následující kód:

[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample3.aspx)]

To definuje výchozí vlastnosti pro vlastnosti související s `CssClass`pro libovolný prvek GridView na libovolné stránce, která používá motiv DataWebControls. Pojďme přidat další vzhled ovládacího prvku DetailsView, datově datovou datovou datovou aplikaci, kterou využijeme krátce. Přidejte nový skin do motivu DataWebControls s názvem `DetailsView.skin` a přidejte následující kód:

[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample4.aspx)]

Po definování našeho motivu je posledním krokem použití motivu na naší stránce ASP.NET. Motiv lze použít pro stránku na stránce nebo pro všechny stránky na webu. Pojďme použít tento motiv pro všechny stránky na webu. Chcete-li to provést, přidejte následující kód do `<system.web>` oddílu `Web.config`:

[!code-xml[Main](displaying-data-with-the-objectdatasource-cs/samples/sample5.xml)]

A je to! Nastavení `styleSheetTheme` určuje, že vlastnosti zadané v motivu by *neměly přepsat vlastnosti* zadané na úrovni ovládacího prvku. Chcete-li určit, že nastavení motivu má mít nastavení ovládacího prvku trumf, použijte atribut `theme` místo `styleSheetTheme`; nastavení motivu zadané pomocí atributu `theme` se v zobrazení Návrh Visual studia bohužel nezobrazí. Další informace o motivech a skinech najdete v tématu [Přehled motivů a vzhledů ASP.NET](https://msdn.microsoft.com/library/ykzx33wh.aspx) a [stylů na straně serveru pomocí motivů](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx) . Další informace o konfiguraci stránky pro použití motivu naleznete v tématu [How to: apply ASP.NET Themes](https://msdn.microsoft.com/library/0yy5hxdk(VS.80).aspx) .

[![se v prvku GridView zobrazuje informace o názvu, kategorii, dodavateli, cenách a vyřazených informacích produktu.](displaying-data-with-the-objectdatasource-cs/_static/image31.png)](displaying-data-with-the-objectdatasource-cs/_static/image30.png)

**Obrázek 12**: v prvku GridView se zobrazí informace o názvu, kategorii, dodavateli, cenách a vyřazených informacích produktu ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-objectdatasource-cs/_static/image32.png)).

## <a name="displaying-one-record-at-a-time-in-the-detailsview"></a>Zobrazení jednoho záznamu v daném okamžiku v ovládacím prvku DetailsView

Prvek GridView zobrazí jeden řádek pro každý záznam vrácený ovládacím prvkem zdroje dat, na který je svázán. Existují však situace, kdy můžeme chtít najednou zobrazit jediný záznam nebo pouze jeden záznam. [Ovládací prvek DetailsView](https://msdn.microsoft.com/library/s3w1w7t4.aspx) nabízí tuto funkci, vykreslení jako `<table>` HTML se dvěma sloupci a jeden řádek pro každý sloupec nebo vlastnost, která je svázána s ovládacím prvkem. Prvek DetailsView lze představit jako prvek GridView s jediným záznamem otočeným 90 stupňů.

Začněte přidáním ovládacího prvku DetailsView *nad* prvek GridView v `SimpleDisplay.aspx`. Potom ji navažte ke stejnému ovládacímu prvku ObjectDataSource jako prvku GridView. Podobně jako u prvku GridView, se vlastnost BoundField přidá do ovládacího prvku DetailsView pro každou vlastnost objektu vrácenou metodou `Select` prvku ObjectDataSource. Jediným rozdílem je, že BoundFields ovládacího prvku DetailsView jsou rozloženy vodorovně, nikoli vertikálně.

[![přidat prvek DetailsView na stránku a vytvořit jeho svázání s prvkem ObjectDataSource](displaying-data-with-the-objectdatasource-cs/_static/image34.png)](displaying-data-with-the-objectdatasource-cs/_static/image33.png)

**Obrázek 13**: Přidání prvku DetailsView na stránku a jeho svázání s ovládacím prvkem ObjectDataSource ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-objectdatasource-cs/_static/image35.png))

Podobně jako v prvku GridView, lze BoundFields ovládacího prvku pro přizpůsobení pro poskytnutí lépe přizpůsobeného zobrazení dat vrácených prvkem ObjectDataSource. Obrázek 14 ukazuje prvek DetailsView po jeho BoundFields a `CssClass` vlastnosti byly nakonfigurovány tak, aby jeho vzhled byl podobný příkladu prvku GridView.

[![ovládacího prvku DetailsView zobrazí jeden záznam.](displaying-data-with-the-objectdatasource-cs/_static/image37.png)](displaying-data-with-the-objectdatasource-cs/_static/image36.png)

**Obrázek 14**: prvek DetailsView zobrazuje jeden záznam ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-objectdatasource-cs/_static/image38.png)).

Všimněte si, že ovládací prvek DetailsView zobrazí pouze první záznam vrácený jeho zdrojem dat. Chcete-li umožnit uživateli procházet všechny záznamy po jednom, je nutné povolit stránkování ovládacího prvku DetailsView. Provedete to tak, že se vrátíte do sady Visual Studio a zaškrtněte políčko Povolit stránkování v inteligentní značce ovládacího prvku DetailsView.

[![povolit stránkování v ovládacím prvku DetailsView](displaying-data-with-the-objectdatasource-cs/_static/image40.png)](displaying-data-with-the-objectdatasource-cs/_static/image39.png)

**Obrázek 15**: povolení stránkování v ovládacím prvku DetailsView ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-objectdatasource-cs/_static/image41.png))

[![s povoleným stránkováním umožňuje ovládací prvek DetailsView uživateli zobrazit libovolný z produktů.](displaying-data-with-the-objectdatasource-cs/_static/image43.png)](displaying-data-with-the-objectdatasource-cs/_static/image42.png)

**Obrázek 16**: s povoleným stránkováním umožňuje DetailsView uživateli zobrazit libovolný z produktů ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-objectdatasource-cs/_static/image44.png)).

V budoucích kurzech budeme mluvit o stránkování.

## <a name="a-more-flexible-layout-for-showing-one-record-at-a-time"></a>Flexibilnější rozložení pro zobrazování jednoho záznamu v daném čase

Prvek DetailsView je poměrně tuhý v tom, jak zobrazuje každý záznam vrácený z prvku ObjectDataSource. Můžeme chtít pružně zobrazit data. Například namísto zobrazení názvu produktu, kategorie, dodavatele, ceny a vyřazených informací, které jsou na samostatném řádku, můžeme v nadpisu `<h4>` zobrazit název produktu a cenu, přičemž informace o kategorii a dodavateli zobrazené pod názvem a cenou se zobrazí v menší velikosti písma. A za hodnoty nemůžeme zobrazit názvy vlastností (produkt, kategorie atd.).

[Ovládací prvek FormView](https://msdn.microsoft.com/library/fyf1dk77.aspx) poskytuje tuto úroveň přizpůsobení. Namísto použití polí (jako například GridView a DetailsView), třída FormView používá šablony, které umožňují kombinovat webové ovládací prvky, statické HTML a [syntaxi datové vazby](http://www.15seconds.com/issue/040630.htm). Pokud jste obeznámeni s ovládacím prvkem Repeater z ASP.NET 1. x, můžete si ho představit jako Repeater pro zobrazení jednoho záznamu.

Přidejte ovládací prvek FormView na návrhovou plochu stránky `SimpleDisplay.aspx`. Zpočátku se FormView zobrazí jako šedý blok, který informuje o tom, že je potřeba poskytnout minimálně `ItemTemplate`ovládacího prvku.

[![třída FormView musí zahrnovat ItemTemplate.](displaying-data-with-the-objectdatasource-cs/_static/image46.png)](displaying-data-with-the-objectdatasource-cs/_static/image45.png)

**Obrázek 17**: třída FormView musí zahrnovat `ItemTemplate` ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-objectdatasource-cs/_static/image47.png)).

FormView lze navazovat přímo na ovládací prvek zdroje dat prostřednictvím inteligentní značky FormView, která vytvoří výchozí `ItemTemplate` automaticky (společně s `EditItemTemplate` a `InsertItemTemplate`, pokud jsou nastaveny vlastnosti `InsertMethod` a `UpdateMethod` ovládacího prvku ObjectDataSource). V tomto příkladu je však možné navazovat data na FormView a zadat její `ItemTemplate` ručně. Začněte nastavením vlastnosti `DataSourceID` třídy FormView na `ID` ovládacího prvku ObjectDataSource `ObjectDataSource1`. V dalším kroku vytvořte `ItemTemplate` tak, aby se v prvku `<h4>` zobrazil název a cena produktu, přičemž kategorie a jména přepravců jsou pod tím, že mají menší velikost písma.

[!code-aspx[Main](displaying-data-with-the-objectdatasource-cs/samples/sample6.aspx)]

[![se první produkt (Chai) zobrazuje ve vlastním formátu.](displaying-data-with-the-objectdatasource-cs/_static/image49.png)](displaying-data-with-the-objectdatasource-cs/_static/image48.png)

**Obrázek 18**: první produkt (Chai) se zobrazí ve vlastním formátu ([kliknutím zobrazíte obrázek v plné velikosti).](displaying-data-with-the-objectdatasource-cs/_static/image50.png)

`<%# Eval(propertyName) %>` je syntaxe datové vazby. Metoda `Eval` vrací hodnotu zadané vlastnosti pro aktuální objekt svázaný s ovládacím prvkem FormView. Další informace o objektech a vydaných datových [vazbách najdete v článku zjednodušená syntaxe Alex Homer a Rozšířená syntaxe datových vazeb v ASP.NET 2,0](http://www.15seconds.com/issue/040630.htm) .

Podobně jako prvek DetailsView, třída FormView zobrazuje pouze první záznam vrácený z prvku ObjectDataSource. Můžete povolit stránkování ve třídě FormView a umožnit tak návštěvníkům postupně procházet produkty.

## <a name="summary"></a>Přehled

Přístup a zobrazování dat z vrstvy obchodní logiky lze provést bez nutnosti psát řádek kódu, a to díky ovládacímu prvku ObjectDataSource ASP.NET 2.0. Prvek ObjectDataSource vyvolá specifikovanou metodu třídy a vrátí výsledky. Tyto výsledky lze zobrazit ve webovém ovládacím prvku dat, který je svázán s prvkem ObjectDataSource. V tomto kurzu jsme se vyhledali vazbou ovládacích prvků GridView, DetailsView a FormView na ObjectDataSource.

Zatím jsme viděli jenom, jak použít prvek ObjectDataSource k vyvolání metody bez parametrů, ale co když chceme vyvolat metodu, která očekává vstupní parametry, jako je `GetProductsByCategoryID(categoryID)``ProductBLL` třídy? Chcete-li volat metodu, která očekává jeden nebo více parametrů, je nutné nakonfigurovat prvek ObjectDataSource pro určení hodnot těchto parametrů. V našem [dalším kurzu](declarative-parameters-cs.md)zjistíme, jak to provést.

Šťastné programování!

## <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Vytvořit vlastní ovládací prvky zdroje dat](https://msdn.microsoft.com/library/ms364049.aspx)
- [Příklady GridView pro ASP.NET 2,0](https://msdn.microsoft.com/library/aa479339.aspx)
- [Zjednodušená a Rozšířená syntaxe datových vazeb v ASP.NET 2,0](http://www.15seconds.com/issue/040630.htm)
- [Motivy v ASP.NET 2,0](http://www.odetocode.com/Articles/423.aspx)
- [Styly na straně serveru pomocí motivů](https://quickstarts.asp.net/quickstartv20/aspnet/doc/themes/stylesheettheme.aspx)
- [Postupy: používání motivů ASP.NET programově](https://msdn.microsoft.com/library/tx35bd89.aspx)

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Hilton Giesenow. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](declarative-parameters-cs.md)

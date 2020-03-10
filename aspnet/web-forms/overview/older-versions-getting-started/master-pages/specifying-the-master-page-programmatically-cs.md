---
uid: web-forms/overview/older-versions-getting-started/master-pages/specifying-the-master-page-programmatically-cs
title: Programové zadání stránky předlohy (C#) | Microsoft Docs
author: rick-anderson
description: Vyhledá stránku předlohy stránky obsahu programově prostřednictvím obslužné rutiny události před inicializací.
ms.author: riande
ms.date: 07/28/2008
ms.assetid: 7c4a3445-2440-4aee-b9fd-779c05e6abb2
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/specifying-the-master-page-programmatically-cs
msc.type: authoredcontent
ms.openlocfilehash: 0db23ea05ba001c2bf9fc5330a60a767caa568a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78625487"
---
# <a name="specifying-the-master-page-programmatically-c"></a>Programové určení stránky předlohy (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_09_CS.zip) nebo [stažení PDF](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_09_CS.pdf)

> Vyhledá stránku předlohy stránky obsahu programově prostřednictvím obslužné rutiny události před inicializací.

## <a name="introduction"></a>Úvod

Vzhledem k tomu, že konference příklad [*vytváření rozložení celého webu pomocí stránek předlohy*](creating-a-site-wide-layout-using-master-pages-cs.md), všechny stránky obsahu odkazovaly na svou hlavní stránku deklarativně prostřednictvím atributu `MasterPageFile` v direktivě `@Page`. Například následující direktiva `@Page` propojuje stránku obsahu se stránkou předlohy `Site.master`:

[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample1.aspx)]

[Třída`Page`](https://msdn.microsoft.com/library/system.web.ui.page.aspx) v oboru názvů `System.Web.UI` obsahuje [vlastnost`MasterPageFile`](https://msdn.microsoft.com/library/system.web.ui.page.masterpagefile.aspx) , která vrací cestu k hlavní stránce stránky obsahu. Tato vlastnost je nastavena pomocí direktivy `@Page`. Tato vlastnost se dá také použít k programovému určení stránky předlohy stránky obsahu. Tento přístup je užitečný, pokud chcete dynamicky přiřazovat hlavní stránku na základě externích faktorů, jako je například uživatel, který stránku navštívil.

V tomto kurzu přidáme na náš web druhou stránku předlohy a dynamicky se rozhodnete, kterou hlavní stránku použít za běhu.

## <a name="step-1-a-look-at-the-page-lifecycle"></a>Krok 1: Prohlédněte si životní cyklus stránky

Pokaždé, když žádost dorazí na webový server pro stránku ASP.NET, která je stránkou obsahu, musí modul ASP.NET pořídit ovládací prvky obsahu stránky do odpovídajících ovládacích prvků ContentPlaceHolder stránky předlohy. Tato syntéza vytvoří jednu hierarchii ovládacích prvků, která pak může pokračovat v běžném životním cyklu stránky.

Tato syntéza je znázorněna na obrázku 1. Krok 1 na obrázku 1 ukazuje počáteční obsah a hierarchie ovládacích prvků stránky předlohy. Na konci fáze předinicializace jsou ovládací prvky obsahu na stránce přidány do odpovídajících prvků ContentPlaceHolder na stránce předlohy (krok 2). Po této syntézě stránka předlohy slouží jako kořen v kontrolní hierarchii. Tato kontrolní hierarchie je pak přidána na stránku, aby vytvořila finální hierarchii řízení (krok 3). Výsledkem je, že hierarchie ovládacích prvků stránky obsahuje pojistou hierarchii řízení.

[![při fázi předinicializačního sestavování hierarchií ovládacího prvku stránky předlohy a stránky obsahu.](specifying-the-master-page-programmatically-cs/_static/image2.png)](specifying-the-master-page-programmatically-cs/_static/image1.png)

**Obrázek 01**: hierarchie ovládacích prvků stránky předlohy a stránky obsahu se během fáze předinicializačního sestavují společně ([kliknutím zobrazíte obrázek v plné velikosti).](specifying-the-master-page-programmatically-cs/_static/image3.png)

## <a name="step-2-setting-themasterpagefileproperty-from-code"></a>Krok 2: nastavení vlastnosti`MasterPageFile`z kódu

Jakou stránku předlohy partakes v této fusion závisí na hodnotě vlastnosti `MasterPageFile` objektu `Page`. Nastavení atributu `MasterPageFile` v direktivě `@Page` má netto účinek přiřazení vlastnosti `MasterPageFile` `Page`během inicializační fáze, což je velmi první fáze životního cyklu stránky. Tuto vlastnost můžeme případně nastavit programově. Je však nutné, aby byla tato vlastnost nastavena před tím, než dojde k fúze na obrázku 1.

Na začátku předinicializační fáze `Page` objekt vyvolá [událost`PreInit`](https://msdn.microsoft.com/library/system.web.ui.page.preinit.aspx) a zavolá jeho [metodu`OnPreInit`](https://msdn.microsoft.com/library/system.web.ui.page.onpreinit.aspx). Chcete-li nastavit hlavní stránku programově, můžeme buď vytvořit obslužnou rutinu události pro událost `PreInit`, nebo přepsat metodu `OnPreInit`. Pojďme se podívat na oba přístupy.

Začněte tím, že otevřete `Default.aspx.cs`, soubor třídy na pozadí pro domovskou stránku webu. Přidejte obslužnou rutinu události pro událost `PreInit` stránky zadáním následujícího kódu:

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample2.cs)]

Odtud můžete nastavit vlastnost `MasterPageFile`. Aktualizujte kód tak, aby přiřadí hodnotu "~/site.Master" do vlastnosti `MasterPageFile`.

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample3.cs)]

Pokud nastavíte zarážku a začnete s laděním, uvidíte, že pokaždé, když se stránka `Default.aspx` navštíví nebo když na této stránce provedete postback, spustí se obslužná rutina `Page_PreInit` události a vlastnost `MasterPageFile` je přiřazena k souboru ~/site.Master.

Alternativně můžete přepsat `OnPreInit` metodu `Page` třídy a nastavit vlastnost `MasterPageFile`. V tomto příkladu není nastavena stránka předlohy na konkrétní stránce, ale místo `BasePage`. Odvolání, že jsme vytvořili vlastní třídu základní stránky (`BasePage`) zpátky v kurzu [*zadání nadpisu, meta značek a dalších hlaviček HTML v kurzu hlavní stránky*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) . V současné době `BasePage` přepisuje metodu `OnLoadComplete` `Page` třídy, kde nastaví vlastnost `Title` stránky na základě dat mapy webu. Pojďme aktualizovat `BasePage` pro přepsání `OnPreInit` metody pro programové určení stránky předlohy.

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample4.cs)]

Vzhledem k tomu, že všechny naše stránky obsahu jsou odvozeny od `BasePage`, všechny z nich nyní mají přiřazenou stránku předlohy programově. V tomto okamžiku je `PreInit` obslužná rutina události v `Default.aspx.cs` nadbytečných; Nebojte se ji odebrat.

### <a name="what-about-thepagedirective"></a>Co je direktiva`@Page`?

To může být trochu matoucí, protože `MasterPageFile` vlastnosti stránky obsahu jsou nyní zadány na dvou místech: programově v `OnPreInit` metodě `BasePage` třídy a také prostřednictvím atributu `MasterPageFile` v direktivě `@Page` stránky obsahu.

První fází životního cyklu stránky je fáze inicializace. Během této fáze je vlastnost objektu `Page` `MasterPageFile` přiřazena hodnotě atributu `MasterPageFile` v direktivě `@Page` (Pokud je k dispozici). Fáze předinicializačního nástroje následuje po inicializační fázi a tady je, kde programově nastavili vlastnost `MasterPageFile` objektu `Page`, čímž se přepíše hodnota přiřazená direktivou `@Page`. Vzhledem k tomu, že nastavujeme vlastnost `MasterPageFile` objektu `Page` programově, mohli bychom z direktivy `@Page` odebrat atribut `MasterPageFile`, aniž by to ovlivnilo činnost koncového uživatele. Pokud to chcete přesvědčit, pokračujte a odeberte atribut `MasterPageFile` z direktivy `@Page` v `Default.aspx` a potom navštivte stránku pomocí prohlížeče. Stejně jako byste očekávali, výstup bude stejný jako před odebráním atributu.

Určuje, zda je vlastnost `MasterPageFile` nastavena prostřednictvím direktivy `@Page` nebo programově bezvýznamnými na činnost koncového uživatele. Atribut `MasterPageFile` v direktivě `@Page` však používá Visual Studio během návrhu k vytvoření zobrazení WYSIWYG v návrháři. Pokud se vrátíte k `Default.aspx` v aplikaci Visual Studio a přejdete k návrháři, zobrazí se zpráva "Chyba stránky předlohy: stránka obsahuje ovládací prvky, které vyžadují odkaz na hlavní stránku, ale žádná není zadaná" (viz obrázek 2).

V krátkém případě je nutné ponechat atribut `MasterPageFile` v direktivě `@Page`, aby v nástroji Visual Studio pracovalo s bohatou funkcí pro práci s časem návrhu.

[![Visual Studio používá k vykreslení návrhového zobrazení atribut MasterPageFile direktivy @Page](specifying-the-master-page-programmatically-cs/_static/image5.png)](specifying-the-master-page-programmatically-cs/_static/image4.png)

**Obrázek 02**: Visual Studio používá atribut `MasterPageFile` direktivy `@Page` k vykreslení zobrazení návrhu ([kliknutím zobrazíte obrázek v plné velikosti](specifying-the-master-page-programmatically-cs/_static/image6.png)).

## <a name="step-3-creating-an-alternative-master-page"></a>Krok 3: vytvoření alternativní stránky předlohy

Vzhledem k tomu, že stránku předlohy stránky obsahu lze nastavit programově za běhu, je možné dynamicky načíst konkrétní hlavní stránku na základě některých externích kritérií. Tato funkce může být užitečná v situacích, kdy se rozložení lokality musí měnit v závislosti na uživateli. Například webová aplikace v modulu blogu může uživatelům dovolit zvolit rozložení pro svůj blog, kde je každé rozložení přidruženo k jiné stránce předlohy. Když se v době běhu návštěvník zobrazuje na blogu uživatele, Webová aplikace by musela určit rozložení blogu a dynamicky přidružit odpovídající stránku předlohy k obsahu stránky.

Pojďme se podívat, jak dynamicky načíst hlavní stránku za běhu na základě některých externích kritérií. Náš web aktuálně obsahuje jenom jednu stránku předlohy (`Site.master`). K ilustraci výběru stránky předlohy za běhu potřebujeme další stránku předlohy. Tento krok se zaměřuje na vytvoření a konfiguraci nové stránky předlohy. Krok 4 se zabývá určením, jakou stránku předlohy použít za běhu.

Vytvořte novou stránku předlohy v kořenové složce s názvem `Alternate.master`. Přidejte také novou šablonu stylů na web s názvem `AlternateStyles.css`.

[![přidat další stránku předlohy a soubor CSS na web](specifying-the-master-page-programmatically-cs/_static/image8.png)](specifying-the-master-page-programmatically-cs/_static/image7.png)

**Obrázek 03**: Přidání další stránky předlohy a souboru CSS na web ([kliknutím zobrazíte obrázek v plné velikosti](specifying-the-master-page-programmatically-cs/_static/image9.png))

Navrhl (a) `Alternate.master` stránku předlohy, aby se název zobrazoval v horní části stránky, na střed a na pozadí námořnická modrá. Vyzkoušel (a) jsem z levého sloupce a přesunuli jsme tento obsah pod ovládací prvek `MainContent` ContentPlaceHolder, který teď pokrývá celou šířku stránky. Kromě toho nixed seznam neuspořádaných lekcí a nahradili ho vodorovným seznamem nad `MainContent`. Také jsem aktualizoval písma a barvy používané stránkou předlohy (a podle přípony, jejích stránek obsahu). Obrázek 4 ukazuje `Default.aspx` při použití `Alternate.master` stránky předlohy.

> [!NOTE]
> ASP.NET zahrnuje možnost definovat *motivy*. Motiv je kolekce obrázků, souborů CSS a nastavení vlastností ovládacích prvků webového ovládacího prvku, která lze použít na stránku za běhu. Motivy slouží jako způsob, jak jít, pokud se rozložení vaší lokality liší pouze v zobrazených obrázcích a jejich pravidly CSS. Pokud se rozložení liší v podstatě, jako je například použití různých webových ovládacích prvků nebo oddálení různých rozložení, bude nutné použít samostatné stránky předlohy. Další informace o motivech najdete v části věnované dalšímu čtení na konci tohoto kurzu.

[![naší stránky obsahu teď můžou používat nový vzhled a chování.](specifying-the-master-page-programmatically-cs/_static/image11.png)](specifying-the-master-page-programmatically-cs/_static/image10.png)

**Obrázek 04**: naše stránky obsahu teď můžou používat nový vzhled a chování ([kliknutím zobrazíte obrázek v plné velikosti).](specifying-the-master-page-programmatically-cs/_static/image12.png)

Když jsou značky hlavního prvku a stránky obsahu pokryty, třída `MasterPage` kontroluje, zda všechny ovládací prvky obsahu na stránce obsahu odkazují na prvky ContentPlaceHolder na stránce předlohy. Výjimka je vyvolána, pokud je nalezen ovládací prvek obsahu, který odkazuje na neexistující prvek ContentPlaceHolder. Jinými slovy, je nezbytné, aby hlavní stránka, která je přiřazena stránce obsahu, měla prvek ContentPlaceHolder pro každý ovládací prvek obsahu na stránce obsahu.

`Site.master` hlavní stránka obsahuje čtyři ovládací prvky ContentPlaceHolder:

- `head`
- `MainContent`
- `QuickLoginUI`
- `LeftColumnContent`

Některé stránky obsahu na našem webu obsahují jenom jeden nebo dva ovládací prvky obsahu. Další součástí jsou ovládací prvky obsahu pro každý z dostupných prvků ContentPlaceHolder. Pokud by naše nová stránka předlohy (`Alternate.master`) mohla být někdy přiřazena k těmto stránkám obsahu, které mají ovládací prvky obsahu pro všechny prvky ContentPlaceHolder v `Site.master` pak je nezbytné, aby `Alternate.master` také zahrnovaly stejné ovládací prvky ContentPlaceHolder jako `Site.master`.

Chcete-li, aby stránka předlohy `Alternate.master` vypadala podobně jako v mikroformátu (viz obrázek 4), začněte definováním stylů stránky předlohy v `AlternateStyles.css` šabloně stylů. Do `AlternateStyles.css`přidejte následující pravidla:

[!code-css[Main](specifying-the-master-page-programmatically-cs/samples/sample5.css)]

Dále přidejte následující deklarativní označení do `Alternate.master`. Jak vidíte, `Alternate.master` obsahuje čtyři ovládací prvky ContentPlaceHolder se stejnými `ID` hodnotami jako ovládací prvky ContentPlaceHolder v `Site.master`. Kromě toho obsahuje ovládací prvek ScriptManager, který je nezbytný pro tyto stránky na našem webu, které používají architekturu ASP.NET AJAX.

[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample6.aspx)]

### <a name="testing-the-new-master-page"></a>Testování nové stránky předlohy

Chcete-li otestovat tuto novou stránku předlohy, aktualizujte metodu `OnPreInit` `BasePage` třídy tak, aby vlastnost `MasterPageFile` byla přiřazena k hodnotě "~/Alternate.Master" a poté návštěvě webu. Každá stránka by měla fungovat bez chyby kromě dvou: `~/Admin/AddProduct.aspx` a `~/Admin/Products.aspx`. Přidání produktu do ovládacího prvku DetailsView v `~/Admin/AddProduct.aspx` má za následek `NullReferenceException` z řádku kódu, který se pokusí nastavit vlastnost `GridMessageText` stránky předlohy. Při návštěvě `~/Admin/Products.aspx` se při načítání stránky vyvolala `InvalidCastException` zpráva: "nelze přetypovat objekt typu ' ASP. alternativní\_Master ' na typ ' ASP. Web\_Master '.

K těmto chybám dochází, protože třída `Site.master` kódu na pozadí obsahuje veřejné události, vlastnosti a metody, které nejsou definovány v `Alternate.master`. Část s označením těchto dvou stránek obsahuje direktivu `@MasterType`, která odkazuje na stránku předlohy `Site.master`.

[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample7.aspx)]

Také obslužná rutina události `ItemInserted` ovládacího prvku DetailsView v `~/Admin/AddProduct.aspx` obsahuje kód, který přesměruje vlastnost `Page.Master` volného typu na objekt typu `Site`. Direktiva `@MasterType` (používá se tímto způsobem) a přetypování v obslužné rutině události `ItemInserted` těsně Couples `~/Admin/AddProduct.aspx` a `~/Admin/Products.aspx` stránky na stránku předlohy `Site.master`.

Pro přerušení tohoto těsného propojení můžeme mít `Site.master` a `Alternate.master` odvozovat ze společné základní třídy, která obsahuje definice pro veřejné členy. Za tímto účelem můžeme aktualizovat direktivu `@MasterType`, aby odkazovala na tento běžný základní typ.

### <a name="creating-a-custom-base-master-page-class"></a>Vytvoření vlastní třídy základní stránky předlohy

Přidejte nový soubor třídy do složky `App_Code` s názvem `BaseMasterPage.cs` a odvodit z `System.Web.UI.MasterPage`. Musíme v `BaseMasterPage`definovat metodu `RefreshRecentProductsGrid` a vlastnost `GridMessageText`, ale nemůžeme je jednoduše přesunout ze `Site.master`, protože tito členové pracují s webovými ovládacími prvky, které jsou specifické pro `Site.master` stránku předlohy (`RecentProducts` prvek GridView a `GridMessage` Label).

To, co musíme udělat, je nakonfigurovat `BaseMasterPage` takovým způsobem, že jsou tyto členy definovány, ale jsou skutečně implementovány pomocí odvozených tříd `BaseMasterPage`(`Site.master` a `Alternate.master`). Tento typ dědičnosti je možné tím, že označíte třídu a její členy jako `abstract`. V krátkém případě přidáním klíčového slova `abstract` těmto dvěma členům oznamuje, že `BaseMasterPage` neimplementuje `RefreshRecentProductsGrid` a `GridMessageText`, ale že jeho odvozené třídy budou.

Také je potřeba definovat událost `PricesDoubled` v `BaseMasterPage` a poskytnout odvozené třídy pro vyvolání události. Vzor použitý v .NET Framework k usnadnění tohoto chování je vytvořit veřejnou událost v základní třídě a přidat chráněnou metodu `virtual` nazvanou `OnEventName`. Odvozené třídy mohou následně volat tuto metodu pro vyvolání události nebo mohou přepsat pro spuštění kódu bezprostředně před nebo po vyvolání události.

Aktualizujte třídu `BaseMasterPage` tak, aby obsahovala následující kód:

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample8.cs)]

V dalším kroku přejdete na třídu `Site.master` kódu na pozadí a ponecháte ji odvozovat z `BaseMasterPage`. Vzhledem k tomu, že `BaseMasterPage` je `abstract` musíme tyto `abstract` členy přepsat v `Site.master`. Přidejte klíčové slovo `override` do definice metody a vlastnosti. Aktualizujte také kód, který vyvolává událost `PricesDoubled` v obslužné rutině události `DoublePrice` tlačítka `Click` voláním metody `OnPricesDoubled` základní třídy.

Po těchto změnách by třída `Site.master` kódu na pozadí měla obsahovat následující kód:

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample9.cs)]

Také je potřeba aktualizovat třídu kódu na pozadí `Alternate.master`pro odvození od `BaseMasterPage` a přepsat dva členy `abstract`. Vzhledem k tomu, že `Alternate.master` neobsahuje prvek GridView, který obsahuje seznam nejaktuálnějších produktů, ani popisek, který zobrazí zprávu po přidání nového produktu do databáze, nemusí tyto metody provádět žádné akce.

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample10.cs)]

### <a name="referencing-the-base-master-page-class"></a>Odkazování na základní třídu stránky předlohy

Teď, když jsme dokončili třídu `BaseMasterPage` a máme dvě stránky předlohy, náš poslední krok je aktualizovat `~/Admin/AddProduct.aspx` a `~/Admin/Products.aspx` stránky, aby odkazovaly na tento společný typ. Začněte změnou direktivy `@MasterType` na obou stránkách z:

[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample11.aspx)]

Komu:

[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample12.aspx)]

Namísto odkazování na cestu k souboru teď vlastnost `@MasterType` odkazuje na základní typ (`BaseMasterPage`). V důsledku toho je vlastnost silně typovaného `Master` použitá na obou stránkách třídy kódu na pozadí nyní typu `BaseMasterPage` (namísto typu `Site`). Tato změna se provádí znovu `~/Admin/Products.aspx`. Dřív to vedlo k chybě při přetypování, protože stránka je nakonfigurovaná tak, aby používala `Alternate.master` stránku předlohy, ale direktiva `@MasterType` odkazovala na `Site.master` soubor. Ale teď se stránka vykreslí bez chyby. Je to proto, že `Alternate.master` hlavní stránku lze přetypovat na objekt typu `BaseMasterPage` (od jeho rozšíření).

Existuje jedna malá změna, kterou je třeba udělat v `~/Admin/AddProduct.aspx`. Obslužná rutina události `ItemInserted` ovládacího prvku DetailsView používá vlastnost `Master` silného typu a vlastnost s volným typem `Page.Master`. Po aktualizaci direktivy `@MasterType` jsme opravili odkaz silného typu, ale pořád potřebujeme aktualizovat volně typované odkazy. Nahraďte následující řádek kódu:

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample13.cs)]

Následující příkaz, který přetypování `Page.Master` na základní typ:

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample14.cs)]

## <a name="step-4-determining-what-master-page-to-bind-to-the-content-pages"></a>Krok 4: určení stránky předlohy, která se má navazovat na stránky obsahu

Naše `BasePage` Třída aktuálně nastavuje všechny vlastnosti stránky obsahu `MasterPageFile` na pevně zakódované hodnoty ve fázi předinicializačního životního cyklu stránky. Tento kód můžeme aktualizovat tak, aby hlavní stránka na některém externím faktoru byla základem. Možná se stránka předlohy načte, záleží na preferencích aktuálně přihlášeného uživatele. V takovém případě musíme napsat kód v metodě `OnPreInit` v `BasePage`, který vyhledá předvolby hlavní stránky aktuálně navštíveného uživatele.

Pojďme vytvořit webovou stránku, která umožňuje uživateli zvolit, kterou hlavní stránku použít-`Site.master` nebo `Alternate.master`-a uložit tuto volbu do proměnné relace. Začněte vytvořením nové webové stránky v kořenovém adresáři s názvem `ChooseMasterPage.aspx`. Při vytváření této stránky (nebo jakékoli jiné stránky obsahu) ji nemusíte navazovat na vzorovou stránku, protože stránka předlohy je nastavena programově v `BasePage`. Pokud však novou stránku nesvážete s hlavní stránkou, bude výchozí deklarativní označení nové stránky obsahovat webový formulář a další obsah poskytnutý stránkou předlohy. Tento kód bude nutné ručně nahradit odpovídajícími ovládacími prvky obsahu. Z tohoto důvodu je snazší vytvořit novou stránku ASP.NET s hlavní stránkou.

> [!NOTE]
> Vzhledem k tomu, že `Site.master` a `Alternate.master` mají stejnou sadu ovládacích prvků ContentPlaceHolder, nezáleží na tom, jakou stránku předlohy jste si zvolili při vytváření nové stránky obsahu. V případě konzistence doporučujeme použít `Site.master`.

[![přidání nové stránky obsahu na web](specifying-the-master-page-programmatically-cs/_static/image14.png)](specifying-the-master-page-programmatically-cs/_static/image13.png)

**Obrázek 05**: Přidání nové stránky obsahu na web ([kliknutím zobrazíte obrázek v plné velikosti](specifying-the-master-page-programmatically-cs/_static/image15.png))

Aktualizujte soubor `Web.sitemap` tak, aby obsahoval položku pro tuto lekci. Přidejte následující kód pod `<siteMapNode>` pro stránku předlohy a lekci ASP.NET AJAX:

[!code-xml[Main](specifying-the-master-page-programmatically-cs/samples/sample15.xml)]

Před přidáním jakéhokoli obsahu na stránku `ChooseMasterPage.aspx` chvíli aktualizujte třídu kódu na pozadí stránky tak, aby byla odvozena z `BasePage` (místo `System.Web.UI.Page`). Dále přidejte ovládací prvek DropDownList na stránku, nastavte jeho vlastnost `ID` na `MasterPageChoice`a přidejte dvě položky ListItems s hodnotami `Text` ~/site.Master a ~/Alternate.Master.

Přidejte na stránku webový ovládací prvek tlačítko a nastavte jeho `ID` a vlastnosti `Text` na `SaveLayout` a "Uložit výběr rozložení" v uvedeném pořadí. V tomto okamžiku by deklarativní označení stránky mělo vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](specifying-the-master-page-programmatically-cs/samples/sample16.aspx)]

Při prvním navštívení stránky musíme zobrazit aktuálně vybranou volbu hlavní stránky uživatele. Vytvořte obslužnou rutinu události `Page_Load` a přidejte následující kód:

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample17.cs)]

Výše uvedený kód se spustí pouze na první stránce (a ne při následném postbacku). Nejprve zkontroluje, zda `MyMasterPage` existuje proměnná relace. Pokud k tomu dojde, pokusí se najít shodu ListItem v `MasterPageChoice` DropDownList. Pokud je nalezen odpovídající ListItem, vlastnost `Selected` je nastavena na hodnotu `true`.

Potřebujeme také kód, který uloží volbu uživatele do proměnné `MyMasterPage` relace. Vytvořte obslužnou rutinu události pro událost `Click` `SaveLayout`ho tlačítka a přidejte následující kód:

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample18.cs)]

> [!NOTE]
> V době, kdy se obslužná rutina události `Click` spustí při zpětném volání, již byla vybrána stránka předlohy. Proto výběr rozevíracího seznamu uživatele nebude platit, dokud další stránka nenavštíví. `Response.Redirect` vynutí, aby prohlížeč znovu vyžádal `ChooseMasterPage.aspx`.

Po dokončení stránky `ChooseMasterPage.aspx` má náš konečný úkol, aby se vlastnost `MasterPageFile` přiřadila `BasePage` na základě hodnoty proměnné relace `MyMasterPage`. Pokud není nastavená proměnná relace, `BasePage` výchozí `Site.master`.

[!code-csharp[Main](specifying-the-master-page-programmatically-cs/samples/sample19.cs)]

> [!NOTE]
> Přesunuli jsme kód, který přiřadí vlastnost `MasterPageFile` `Page` objektu z obslužné rutiny události `OnPreInit` a do dvou samostatných metod. Tato první metoda, `SetMasterPageFile`, přiřadí vlastnost `MasterPageFile` hodnotě vrácené druhou metodou `GetMasterPageFileFromSession`. Provedli jsme metodu `SetMasterPageFile` `virtual` tak, aby budoucí třídy, které přesahují `BasePage`, mohly případně přepsat, aby v případě potřeby implementovaly vlastní logiku. V dalším kurzu se zobrazí příklad přepsání `SetMasterPageFile` vlastnosti `BasePage`.

S tímto kódem je místo na stránce `ChooseMasterPage.aspx`. Zpočátku je vybraná stránka předlohy `Site.master` (viz obrázek 6), ale uživatel může z rozevíracího seznamu vybrat jinou stránku předlohy.

[![stránky obsahu se zobrazí pomocí stránky site. master master.](specifying-the-master-page-programmatically-cs/_static/image17.png)](specifying-the-master-page-programmatically-cs/_static/image16.png)

**Obrázek 6**: stránky obsahu se zobrazují pomocí `Site.master` stránky předlohy ([kliknutím zobrazíte obrázek v plné velikosti).](specifying-the-master-page-programmatically-cs/_static/image18.png)

[![stránky obsahu se nyní zobrazují pomocí alternativní stránky. Hlavní stránka předlohy.](specifying-the-master-page-programmatically-cs/_static/image20.png)](specifying-the-master-page-programmatically-cs/_static/image19.png)

**Obrázek 7**: stránky obsahu se nyní zobrazují pomocí `Alternate.master` stránky předlohy ([kliknutím zobrazíte obrázek v plné velikosti).](specifying-the-master-page-programmatically-cs/_static/image21.png)

## <a name="summary"></a>Souhrn

Po navštívení stránky obsahu jsou ovládací prvky tohoto obsahu poopatřeny ovládacími prvky ContentPlaceHolder stránky předlohy. Stránka předlohy stránky obsahu je označena vlastností `MasterPageFile` třídy `Page`, která je přiřazena k atributu `MasterPageFile` direktivy `@Page` během inicializační fáze. Jak je znázorněno v tomto kurzu, můžeme přiřadit hodnotu vlastnosti `MasterPageFile`, pokud to uděláte před koncem fáze předinicializace. Schopnost programově určit stránku předlohy otevře dvířka pro pokročilejší scénáře, jako je například dynamická vazba stránky obsahu na hlavní stránku na základě externích faktorů.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Diagram životního cyklu stránky ASP.NET](http://emanish.googlepages.com/Asp.Net2.0Lifecycle.PNG)
- [ASP.NET – přehled životního cyklu stránky](https://msdn.microsoft.com/library/ms178472.aspx)
- [Přehled motivů a vzhledů ASP.NET](https://msdn.microsoft.com/library/ykzx33wh.aspx)
- [Stránky předlohy: tipy, triky a depeše](http://www.odetocode.com/articles/450.aspx)
- [Motivy v ASP.NET](http://www.odetocode.com/articles/423.aspx)

### <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 3,5 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco). Scott se dá kontaktovat [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Vedoucí recenzent pro tento kurz byl takový Banerjee. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](master-pages-and-asp-net-ajax-cs.md)
> [Další](nested-master-pages-cs.md)

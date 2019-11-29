---
uid: web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-vb
title: Stránkování a řazení dat sestavy (VB) | Microsoft Docs
author: rick-anderson
description: Stránkování a řazení jsou dvě velmi běžné funkce při zobrazování dat v online aplikaci. V tomto kurzu se podíváme na první pohled na přidání řazení a...
ms.author: riande
ms.date: 08/15/2006
ms.assetid: b895e37e-0e69-45cc-a7e4-17ddd2e1b38d
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/paging-and-sorting-report-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 6785b5cd2d4d3a2c2e7f2c2fea93f5cd5e2fdf24
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74619232"
---
# <a name="paging-and-sorting-report-data-vb"></a>Stránkování a řazení dat sestavy (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_24_VB.exe) nebo [Stáhnout PDF](paging-and-sorting-report-data-vb/_static/datatutorial24vb1.pdf)

> Stránkování a řazení jsou dvě velmi běžné funkce při zobrazování dat v online aplikaci. V tomto kurzu se podíváme na první pohled na přidání řazení a stránkování do našich sestav, které pak vytvoříme v budoucích kurzech.

## <a name="introduction"></a>Úvod

Stránkování a řazení jsou dvě velmi běžné funkce při zobrazování dat v online aplikaci. Například při hledání ASP.NET knih v online knihkupectví mohou existovat stovky takových knih, ale v sestavě se seznamem výsledků hledání se zobrazí pouze deset shod na jednu stránku. Kromě toho je možné výsledky seřadit podle názvu, ceny, počtu stránek, jména autora atd. I když se v posledních 23 kurzech zkoumalo, jak sestavit celou řadu sestav, včetně rozhraní, která umožňují přidávání, upravování a odstraňování dat, nezobrazili jsme se na tom, jak řadit data a jenom příklady stránkování, které jsme viděli, s ovládacím prvekem DetailsView a FormView. ovládací prvky.

V tomto kurzu se dozvíte, jak přidat řazení a stránkování do našich sestav, které je možné dosáhnout pouhým zaškrtnutím několika zaškrtávacích políček. Tato implementace zjednodušený bohužel má nevýhodu, takže rozhraní řazení opustí bitovou kopii, která je žádoucí, a rutiny stránkování nejsou navržené pro efektivní stránkování prostřednictvím rozsáhlých sad výsledků. V budoucích kurzech se dozvíte, jak překonat omezení předem připravených řešení pro stránkování a řazení.

## <a name="step-1-adding-the-paging-and-sorting-tutorial-web-pages"></a>Krok 1: Přidání webových stránek kurzu stránkování a seřazení

Před zahájením tohoto kurzu si nejdřív počkejte, než se přidá stránky ASP.NET, které budeme potřebovat pro tento kurz a další tři. Začněte vytvořením nové složky v projektu s názvem `PagingAndSorting`. V dalším kroku přidejte do této složky následující pět ASP.NET stránek a všechny je nakonfigurované tak, aby používaly stránku předlohy `Site.master`:

- `Default.aspx`
- `SimplePagingSorting.aspx`
- `EfficientPaging.aspx`
- `SortParameter.aspx`
- `CustomSortingUI.aspx`

![Vytvořte složku PagingAndSorting a přidejte stránky ASP.NET kurzu.](paging-and-sorting-report-data-vb/_static/image1.png)

**Obrázek 1**: vytvoření složky PagingAndSorting a přidání stránek kurzu ASP.NET

Potom otevřete stránku `Default.aspx` a přetáhněte uživatelský ovládací prvek `SectionLevelTutorialListing.ascx` ze složky `UserControls` na návrhovou plochu. Tento uživatelský ovládací prvek, který jsme vytvořili v kurzu [hlavní stránky a navigace na webu](../introduction/master-pages-and-site-navigation-vb.md) , vytvoří výčet mapy lokality a v aktuálním oddílu zobrazí v seznamu s odrážkami kurzy.

![Přidat uživatelský ovládací prvek SectionLevelTutorialListing. ascx do default. aspx](paging-and-sorting-report-data-vb/_static/image2.png)

**Obrázek 2**: Přidání uživatelského ovládacího prvku SectionLevelTutorialListing. ascx do default. aspx

Aby se v seznamu s odrážkami zobrazovaly kurzy stránkování a řazení, vytvoříme, že je musíme přidat k mapě webu. Otevřete soubor `Web.sitemap` a po úpravách, vkládání a odstraňování značek uzlu mapy webu přidejte následující kód:

[!code-xml[Main](paging-and-sorting-report-data-vb/samples/sample1.xml)]

![Aktualizovat mapu webu tak, aby obsahovala nové stránky ASP.NET](paging-and-sorting-report-data-vb/_static/image3.png)

**Obrázek 3**: aktualizace mapy webu tak, aby obsahovala nové stránky ASP.NET

## <a name="step-2-displaying-product-information-in-a-gridview"></a>Krok 2: zobrazení informací o produktu v prvku GridView

Předtím, než ve skutečnosti implementujeme možnosti stránkování a řazení, je nejdříve možné vytvořit standardní neuživatelsky nevyhovující prvky GridView, které obsahují informace o produktu. Toto je úkol, který jsme v průběhu celé řady kurzů mnohokrát provedli, aby bylo možné tyto kroky dobře znát. Začněte otevřením stránky `SimplePagingSorting.aspx` a přetažením ovládacího prvku GridView z panelu nástrojů do návrháře nastavte jeho vlastnost `ID` na `Products`. Dále vytvořte nový prvek ObjectDataSource, který pomocí ProductsBLL třídy s `GetProducts()` metodu vrátí všechny informace o produktu.

![Načíst informace o všech produktech pomocí metody GetProducts ()](paging-and-sorting-report-data-vb/_static/image4.png)

**Obrázek 4**: načtení informací o všech produktech pomocí metody GetProducts ()

Vzhledem k tomu, že je tato sestava sestavou jen pro čtení, není nutné mapovat prvky ObjectDataSource `Insert()`, `Update()`nebo `Delete()` metody na odpovídající `ProductsBLL` metody; Proto v rozevíracím seznamu pro karty aktualizace, vložení a odstranění vyberte (žádné).

![V rozevíracím seznamu na kartách aktualizace, vložení a odstranění vyberte možnost (žádná).](paging-and-sorting-report-data-vb/_static/image5.png)

**Obrázek 5**: v rozevíracím seznamu na kartách aktualizace, vložení a odstranění vyberte možnost (žádná).

Dále Přizpůsobte pole GridView s tak, aby se zobrazily pouze názvy produktů, dodavatelé, kategorie, ceny a ukončené stavy. Navíc můžete bez obav udělat jakékoli změny formátování na úrovni polí, jako je například úprava vlastností `HeaderText` nebo formátování ceny jako měny. Po těchto změnách by deklarativní označení GridViewu mělo vypadat podobně jako následující:

[!code-aspx[Main](paging-and-sorting-report-data-vb/samples/sample2.aspx)]

Obrázek 6 znázorňuje náš průběh, pokud je zobrazený v prohlížeči. Všimněte si, že stránka obsahuje seznam všech produktů na jedné obrazovce, kde se zobrazují všechny názvy produktů, kategorie, dodavatele, ceny a ukončené stavy.

[![jednotlivé produkty jsou uvedené](paging-and-sorting-report-data-vb/_static/image7.png)](paging-and-sorting-report-data-vb/_static/image6.png)

**Obrázek 6**: seznam všech produktů ([kliknutím zobrazíte obrázek v plné velikosti](paging-and-sorting-report-data-vb/_static/image8.png))

## <a name="step-3-adding-paging-support"></a>Krok 3: Přidání podpory stránkování

Výpis *všech* produktů na jedné obrazovce může vést k přetížení informací, aby uživatel perusing data. Abychom vám pomohli zlepšit správu výsledků, můžeme rozdělit data na menší stránky dat a umožnit tak uživateli procházet data po jednotlivých stránkách. Chcete-li to provést, zaškrtněte políčko Povolit stránkování z inteligentní značky GridView s (tím se nastaví [vlastnost`AllowPaging`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowpaging.aspx) prvku gridview s `true`).

[![zaškrtnutím políčka Povolit stránkování přidejte podporu stránkování.](paging-and-sorting-report-data-vb/_static/image10.png)](paging-and-sorting-report-data-vb/_static/image9.png)

**Obrázek 7**: Zaškrtnutím políčka Povolit stránkování přidejte podporu stránkování ([kliknutím zobrazíte obrázek v plné velikosti).](paging-and-sorting-report-data-vb/_static/image11.png)

Povolení stránkování omezuje počet záznamů zobrazených na stránce a přidá *rozhraní stránkování* do prvku GridView. Výchozí stránkovací rozhraní zobrazené na obrázku 7 je série čísel stránek, která umožňuje uživateli rychle přejít z jedné stránky dat do jiné. Toto rozhraní stránkování by mělo vypadat dobře, jak jsme ho viděli při přidávání podpory stránkování do ovládacích prvků DetailsView a FormView v předchozích kurzech.

Ovládací prvky DetailsView a FormView zobrazují pouze jeden záznam na stránku. Prvek GridView ale pomocí [vlastnosti`PageSize`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.pagesize.aspx) zjistí, kolik záznamů se má zobrazit na stránce (Tato vlastnost je standardně nastavená na hodnotu 10).

Rozhraní pro stránkování prvku GridView, DetailsView a FormView s lze přizpůsobit pomocí následujících vlastností:

- `PagerStyle` označuje informace o stylu pro rozhraní stránkování; lze určit nastavení, například `BackColor`, `ForeColor`, `CssClass`, `HorizontalAlign`a tak dále.
- `PagerSettings` obsahuje řadou reálných vlastností, které mohou přizpůsobit funkčnost rozhraní stránkování; `PageButtonCount` označuje maximální počet čísel stránek zobrazených ve stránkovacím rozhraní (výchozí hodnota je 10); [vlastnost`Mode`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.pagersettings.mode.aspx) označuje, jak funguje stránkování rozhraní a lze jej nastavit na: 

    - `NextPrevious` zobrazí další a předchozí tlačítka umožňující uživateli krok dopředu nebo dozadu po jedné stránce.
    - k dispozici jsou také `NextPreviousFirstLast` kromě tlačítek Další a předchozí, první a poslední tlačítko a umožňuje uživateli rychle přejít na první nebo poslední stránku dat.
    - `Numeric` zobrazuje řadu čísel stránek a umožňuje uživateli okamžitě přejít na libovolnou stránku.
    - `NumericFirstLast` kromě čísel stránek zahrnuje i první a poslední tlačítko a umožňuje uživateli rychle přejít na první nebo poslední stránku dat; První/poslední tlačítko se zobrazí pouze v případě, že se nevejde na všechna čísla čísel stránek

Kromě toho všechny ovládací prvek GridView, DetailsView a FormView nabízí vlastnosti `PageIndex` a `PageCount`, které označují aktuální prohlíženou stránku a celkový počet stránek dat v uvedeném pořadí. Vlastnost `PageIndex` je indexovaná počínaje hodnotou 0, což znamená, že při zobrazení první stránky `PageIndex` dat se rovná 0. `PageCount`na druhé straně začíná počítat hodnotou 1, což znamená, že `PageIndex` jsou omezeny na hodnoty mezi 0 a `PageCount - 1`.

Počkejte prosím chvíli, než se vylepšit výchozí vzhled našeho rozhraní pro stránkování v prvku GridView. Konkrétně je možné, že mají rozhraní stránkování zarovnané vpravo s lehkým šedým pozadím. Místo toho, aby se tyto vlastnosti nacházely přímo prostřednictvím vlastnosti `PagerStyle` prvku GridView, umožňují vytvořit třídu CSS v `Styles.css` s názvem `PagerRowStyle` a následně přiřadit vlastnost `PagerStyle` s `CssClass` prostřednictvím našeho motivu. Začněte otevřením `Styles.css` a přidáním následující definice třídy CSS:

[!code-css[Main](paging-and-sorting-report-data-vb/samples/sample3.css)]

Potom otevřete soubor `GridView.skin` ve složce `DataWebControls` ve složce `App_Themes`. Jak jsme probrali v kurzu *hlavní stránky a navigace na webu* , soubory skinu se dají použít k určení výchozích hodnot vlastností pro webový ovládací prvek. Proto rozšiřte existující nastavení tak, aby zahrnovalo nastavení vlastnosti `PagerStyle` s `CssClass` na `PagerRowStyle`. Také je možné nakonfigurovat stránkovací rozhraní tak, aby zobrazovalo maximálně pět tlačítek numerické stránky pomocí rozhraní pro stránkování `NumericFirstLast`.

[!code-aspx[Main](paging-and-sorting-report-data-vb/samples/sample4.aspx)]

## <a name="the-paging-user-experience"></a>Uživatelské prostředí stránkování

Obrázek 8 ukazuje webovou stránku při návštěvě prohlížeče poté, co je zaškrtnuto zaškrtávací políčko Povolit stránkování prvku GridView a `PagerStyle` a `PagerSettings` byly provedeny pomocí souboru `GridView.skin`. Všimněte si, jak se zobrazují jenom deset záznamů, a rozhraní stránkování označuje, že zobrazujeme první stránku dat.

[![s povoleným stránkováním se zobrazí pouze podmnožina záznamů.](paging-and-sorting-report-data-vb/_static/image13.png)](paging-and-sorting-report-data-vb/_static/image12.png)

**Obrázek 8**: u povoleného stránkování se zobrazí pouze podmnožina záznamů ([kliknutím zobrazíte obrázek v plné velikosti).](paging-and-sorting-report-data-vb/_static/image14.png)

Když uživatel klikne na jedno z čísel stránek ve stránkovacím rozhraní, vystavuje se postback a stránka se znovu načte, aby se zobrazily požadované záznamy stránky. Obrázek 9 ukazuje výsledky poté, co se rozhodnete, že si budete chtít zobrazit poslední stránku dat. Všimněte si, že poslední stránka má pouze jeden záznam; Důvodem je, že jsou celkem 81 záznamů, což vede k osmi stránkám o 10 záznamům na stránce a jedné stránce se záznamem jedinou.

[![kliknutí na číslo stránky způsobí postback a zobrazí příslušnou podmnožinu záznamů.](paging-and-sorting-report-data-vb/_static/image16.png)](paging-and-sorting-report-data-vb/_static/image15.png)

**Obrázek 9**: kliknutí na číslo stránky způsobí postback a zobrazí příslušnou podmnožinu záznamů ([kliknutím zobrazíte obrázek v plné velikosti).](paging-and-sorting-report-data-vb/_static/image17.png)

## <a name="paging-s-server-side-workflow"></a>Pracovní postup stránkování s na straně serveru

Když koncový uživatel klikne na tlačítko ve stránkovacím rozhraní, vystavuje se postback a spustí se následující pracovní postup na straně serveru:

1. Prvek GridView s (nebo DetailsView nebo FormView) `PageIndexChanging` událost je aktivována.
2. Prvek ObjectDataSource znovu vyžádá *všechna* data z knihoven BLL; hodnoty vlastností `PageIndex` a `PageSize` prvku GridView se používají k určení, které záznamy vrácené z knihoven BLL musí být zobrazeny v prvku GridView.
3. `PageIndexChanged` událost prvku GridView s

V kroku 2 prvek ObjectDataSource znovu vyžádá všechna data ze zdroje dat. Tento styl stránkování se obvykle označuje jako *výchozí stránkování*, protože se chování stránkování používá ve výchozím nastavení při nastavování vlastnosti `AllowPaging` na hodnotu `true`. S výchozím stránkováním webová sada data naively načte všechny záznamy pro každou stránku dat, a to i v případě, že se ve formátu HTML, který se posílá do prohlížeče, skutečně vykreslí jenom podmnožina záznamů. Pokud data databáze knihoven BLL nebo ObjectDataSource neukládají do mezipaměti, výchozí stránkování je nefunkční pro dostatečně velké sady výsledků nebo pro webové aplikace s mnoha souběžnými uživateli.

V dalším kurzu podíváme se, jak implementovat *vlastní stránkování*. Pomocí vlastního stránkování můžete konkrétně dát prvku ObjectDataSource pokyn, aby načetl pouze přesně sadu záznamů potřebných pro požadovanou stránku dat. Vzhledem k tomu, že vlastní stránkování výrazně zlepšuje efektivitu stránkování prostřednictvím rozsáhlých sad výsledků.

> [!NOTE]
> I když výchozí stránkování není vhodné při stránkování přes dostatečně velké sady výsledků nebo pro lokality s mnoha současnými uživateli, je třeba si uvědomit, že vlastní stránkování vyžaduje další změny a úsilí k implementaci a není tak jednoduché jako zaškrtnutí políčka (jako výchozí). stránkování). Výchozí stránkování může být proto ideální volbou pro malé, nenáročné weby nebo při stránkování prostřednictvím relativně malých sad výsledků, protože je mnohem jednodušší a rychlejší je implementovat.

Pokud například víte, že v naší databázi nikdy nebudete mít více než 100 produktů, minimální zvýšení výkonu pro vlastní stránkování se pravděpodobně posune podle úsilí potřebného k jeho implementaci. Pokud ale můžeme za jeden *den používat tisíce* nebo desítky tisíců produktů, neimplementace vlastního stránkování by významně bránila škálovatelnosti naší aplikace.

## <a name="step-4-customizing-the-paging-experience"></a>Krok 4: přizpůsobení prostředí stránkování

Webové ovládací prvky dat poskytují řadu vlastností, které lze použít k vylepšení stránkování uživatele. Vlastnost `PageCount` například indikuje, kolik z celkových stránek existuje, zatímco vlastnost `PageIndex` indikuje aktuální navštívenou stránku a dá se nastavit na rychlé přesunutí uživatele na konkrétní stránku. Chcete-li se seznámit s tím, jak tyto vlastnosti použít ke zlepšení uživatelského prostředí s možností stránkování, přidejte ovládací prvek web Label na naši stránku, který informuje uživatele o tom, jakou stránku uživatel právě navštívil, a ovládací prvek DropDownList, který umožňuje rychle přejít na příslušnou stránku. .

Nejprve přidejte ovládací prvek web Label na stránku, nastavte jeho vlastnost `ID` na `PagingInformation`a zrušte jeho vlastnost `Text`. Dále vytvořte obslužnou rutinu události pro událost GridView `DataBound` a přidejte následující kód:

[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample5.vb)]

Tato obslužná rutina události přiřadí vlastnost `PagingInformation` popisek s `Text` ke zprávě informující o uživateli, na které se aktuálně navštěvuje stránka, která je v současné době navštívená, `Products.PageIndex + 1` z celkového počtu `Products.PageCount`ch stránek (do vlastnosti `Products.PageIndex` přidáme 1, protože `PageIndex` index začíná na 0). V obslužné rutině události `DataBound` jsem zvolil (a) vlastnost přiřadit tuto `Text` popisek, a to na rozdíl od obslužné rutiny události `PageIndexChanged`, protože událost `DataBound` se aktivuje při každém vazbě dat na prvek GridView, zatímco obslužná rutina události `PageIndexChanged` se aktivuje jenom v případě, že se změní index stránky. Při počátečním vázání dat na první stránce se událost `PageIndexChanging` neaktivuje (zatímco `DataBound` událost).

V takovém případě se uživateli teď zobrazuje zpráva, že stránka, na kterou se navštěvuje, a kolik z nich celkový počet stránek dat.

[![aktuální číslo stránky a celkový počet stránek.](paging-and-sorting-report-data-vb/_static/image19.png)](paging-and-sorting-report-data-vb/_static/image18.png)

**Obrázek 10**: zobrazí se číslo aktuální stránky a celkový počet stránek ([kliknutím zobrazíte obrázek v plné velikosti).](paging-and-sorting-report-data-vb/_static/image20.png)

Kromě ovládacího prvku popisek přidejte také ovládací prvek DropDownList, který obsahuje čísla stránek v prvku GridView se zvolenou aktuálně zobrazenou stránkou. Nápad je, že uživatel může rychle přejít z aktuální stránky na jiný tak, že jednoduše vybere nový index stránky z ovládacího prvkem DropDownList. Začněte přidáním ovládacího prvkem DropDownList do návrháře, nastavením jeho vlastnosti `ID` na `PageList` a zaškrtnutím políčka Povolit automatický PostBack z jeho inteligentní značky.

Pak se vraťte k obslužné rutině události `DataBound` a přidejte následující kód:

[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample6.vb)]

Tento kód začíná vymazáním položek v `PageList` DropDownList. Může to být nadbytečných, protože jeden z nich očekává změnu počtu stránek, ale ostatní uživatelé můžou používat systém současně a přidávat nebo odebírat záznamy z `Products` tabulky. Taková vložení nebo odstranění by mohla změnit počet stránek dat.

Dále je potřeba znovu vytvořit čísla stránek a mít tu, která je namapována na aktuální prvek GridView `PageIndex` vybraný ve výchozím nastavení. Tímto dosáhneme smyčkou od 0 do `PageCount - 1`a do každé iterace se přidá nový `ListItem` a vlastnost `Selected` se nastaví na true, pokud aktuální index iterace odpovídá vlastnosti GridView s `PageIndex`.

Nakonec musíme vytvořit obslužnou rutinu události pro událost DropDownList `SelectedIndexChanged`, která se aktivuje pokaždé, když uživatel vybere jinou položku ze seznamu. Chcete-li vytvořit tuto obslužnou rutinu události, stačí dvakrát kliknout na DropDownList v návrháři a pak přidat následující kód:

[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample7.vb)]

Jak je znázorněno na obrázku 11, pouze změna vlastnosti `PageIndex` ovládacího prvku GridView způsobí, že data budou znovu svázána s prvku GridView. V obslužné rutině události GridView `DataBound` je vybrána příslušná `ListItem` DropDownList.

[![se uživatel automaticky převezme na šestou stránku při výběru položky rozevíracího seznamu Stránka 6.](paging-and-sorting-report-data-vb/_static/image22.png)](paging-and-sorting-report-data-vb/_static/image21.png)

**Obrázek 11**: uživatel se automaticky převezme na šestou stránku při výběru položky rozevíracího seznamu Stránka 6 ([kliknutím zobrazíte obrázek v plné velikosti).](paging-and-sorting-report-data-vb/_static/image23.png)

## <a name="step-5-adding-bi-directional-sorting-support"></a>Krok 5: Přidání podpory obousměrného řazení

Přidání podpory obousměrného řazení je jednoduché, protože přidání podpory stránkování stačí zaškrtnout možnost Povolit řazení z inteligentní značky GridView s (která nastaví [vlastnost GridView`AllowSorting`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.allowsorting.aspx) na `true`). Tím se vykreslí všechny hlavičky polí GridView s jako LinkButtons, které při kliknutí způsobí postback a vrátí data seřazená kliknutím na sloupec ve vzestupném pořadí. Opětovné řazení dat v sestupném pořadí po kliknutí na stejnou položku záhlaví.

> [!NOTE]
> Pokud používáte vlastní vrstvu přístupu k datům, nikoli typovou datovou sadu, je možné, že v inteligentní značce GridView s nebudete mít možnost Povolit řazení. Toto zaškrtávací políčko je k dispozici pouze pro GridViews svázané se zdroji dat, které nativně podporují řazení. Typová datová sada poskytuje dopředná podpora řazení, protože ADO.NET DataTable poskytuje metodu `Sort`, která při vyvolání seřadí datové řádky DataTable s pomocí zadaných kritérií.

Pokud váš DAL nevrací objekty, které nativně podporují řazení, budete muset prvek ObjectDataSource nakonfigurovat tak, aby předával informace o řazení do vrstvy obchodní logiky, která může data buď seřadit, nebo data seřadit podle DAL. Podíváme se, jak v budoucím kurzu řadit data z obchodní logiky a vrstev přístupu k datům.

Řazení LinkButtons se vykresluje jako hypertextové odkazy HTML, jejichž aktuální barvy (modré pro Nenavštívený odkaz a tmavě červené pro navštívený odkaz) jsou v konfliktu s barvou pozadí řádku záhlaví. Místo toho mají všechny odkazy na řádky záhlaví zobrazeny bíle bez ohledu na to, zda byly navštíveny nebo nikoli. To lze provést přidáním následujícího do třídy `Styles.css`:

[!code-css[Main](paging-and-sorting-report-data-vb/samples/sample8.css)]

Tato syntaxe označuje použití bílého textu při zobrazování těchto hypertextových odkazů v rámci elementu, který používá třídu HeaderStyle.

Po přidání této šablony stylů CSS by se při návštěvě stránky v prohlížeči měla vaše obrazovka podobat obrázku 12. Konkrétně obrázek 12 zobrazuje výsledky po kliknutí na odkaz záhlaví pole s cenami.

[![výsledky byly seřazené podle standardu UnitPrice ve vzestupném pořadí.](paging-and-sorting-report-data-vb/_static/image25.png)](paging-and-sorting-report-data-vb/_static/image24.png)

**Obrázek 12**: výsledky byly seřazené podle standardu UnitPrice ve vzestupném pořadí ([kliknutím zobrazíte obrázek v plné velikosti).](paging-and-sorting-report-data-vb/_static/image26.png)

## <a name="examining-the-sorting-workflow"></a>Prozkoumání pracovního postupu řazení

Všechna pole GridView vlastnost BoundField, třídě CheckBoxField podporována, TemplateField a So mají vlastnost `SortExpression`, která určuje výraz, který se má použít k řazení dat při kliknutí na odkaz záhlaví pole s řazením. Prvek GridView má také vlastnost `SortExpression`. Když kliknete na záhlaví třídy LinkButton, ovládací prvek GridView přiřadí tomuto poli `SortExpression` hodnotu na jeho vlastnost `SortExpression`. Dále jsou data znovu načtena z prvku ObjectDataSource a seřazena podle vlastnosti `SortExpression` prvků GridView. Následující seznam popisuje pořadí kroků, které se zobrazí, když koncový uživatel seřadí data v prvku GridView:

1. [Událost řazení](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorting(VS.80).aspx) prvku GridView s je aktivována
2. Vlastnost GridView s [`SortExpression`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx) je nastavena na `SortExpression` pole, u kterého bylo kliknuto na řazení záhlaví LinkButton.
3. Prvek ObjectDataSource znovu načte všechna data z knihoven BLL a poté seřadí data pomocí `SortExpression` GridView.
4. Vlastnost GridView s `PageIndex` je nastavena na hodnotu 0, což znamená, že při řazení uživatele do první stránky dat (předpokládá se, že byla implementována podpora stránkování).
5. [`Sorted` událost](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sorted(VS.80).aspx) prvku GridView s

Podobně jako u výchozího stránkování výchozí možnost řazení znovu načte *všechny* záznamy z knihoven BLL. Pokud používáte řazení bez stránkování nebo používáte řazení s výchozím stránkováním, neexistuje žádný způsob, jak obejít tento výkon (krátký ukládání databázových dat do mezipaměti). Jak se ale v budoucím kurzu ukážeme, je možné efektivně seřadit data při použití vlastního stránkování.

Při navázání prvku ObjectDataSource na prvek GridView prostřednictvím rozevíracího seznamu v inteligentní značce GridView s má každé pole GridView automaticky svou `SortExpression` vlastnost přiřazenou k názvu datového pole ve třídě `ProductsRow`. Například `ProductName` vlastnost BoundField s `SortExpression` je nastavena na `ProductName`, jak je znázorněno v následujícím deklarativním kódu:

[!code-aspx[Main](paging-and-sorting-report-data-vb/samples/sample9.aspx)]

Pole lze nakonfigurovat tak, aby se nedala seřadit tak, že vymažete jeho vlastnost `SortExpression` (přiřadíte ji do prázdného řetězce). K ilustraci si představte, že nám nechtěli umožnit našim zákazníkům řadit naše produkty podle ceny. Vlastnost `UnitPrice` vlastnost BoundField s `SortExpression` lze odebrat buď z deklarativní značky, nebo pomocí dialogového okna pole (k dispozici kliknutím na odkaz Upravit sloupce v inteligentní značce GridView).

![Výsledky byly seřazené podle standardu UnitPrice ve vzestupném pořadí.](paging-and-sorting-report-data-vb/_static/image27.png)

**Obrázek 13**: výsledky byly seřazené podle standardu UnitPrice ve vzestupném pořadí.

Po odebrání vlastnosti `SortExpression` pro `UnitPrice` vlastnost BoundField se záhlaví vykreslí jako text, nikoli jako odkaz, a tím uživatelům zabránit v řazení dat podle ceny.

[![odebráním vlastnosti SortExpression už uživatelé nemůžou seřadit produkty podle ceny.](paging-and-sorting-report-data-vb/_static/image29.png)](paging-and-sorting-report-data-vb/_static/image28.png)

**Obrázek 14**: odebráním vlastnosti SortExpression již uživatelé nebudou moci řadit produkty podle ceny ([kliknutím zobrazíte obrázek v plné velikosti).](paging-and-sorting-report-data-vb/_static/image30.png)

## <a name="programmatically-sorting-the-gridview"></a>Programové řazení prvku GridView

Obsah prvku GridView lze také seřadit programově pomocí [metody`Sort`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sort.aspx)GridView. Jednoduše předejte `SortExpression` hodnotu pro řazení společně s [`SortDirection`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sortdirection.aspx) (`Ascending` nebo `Descending`) a data GridView s se znovu seřadí.

Představme si, že důvodem, proč jsme vypnuli `UnitPrice`, bylo, že by naši zákazníci mohli jednoduše koupit jenom ty nižší ceny. Chceme jim ale povzbudit, aby si koupili nejlevnější produkt, takže abychom mohli produkty řadit podle ceny, ale jenom z nejdražších cen na nejméně.

K tomuto účelu přidejte webový ovládací prvek tlačítko na stránku, nastavte jeho vlastnost `ID` na `SortPriceDescending`a jeho vlastnost `Text` na hodnotu seřadit podle ceny. Potom v Návrháři dvakrát klikněte na ovládací prvek tlačítko v návrháři a vytvořte obslužnou rutinu události pro tlačítko s `Click` událostí. Do této obslužné rutiny události přidejte následující kód:

[!code-vb[Main](paging-and-sorting-report-data-vb/samples/sample10.vb)]

Kliknutím na toto tlačítko vrátíte uživatele na první stránku s produkty seřazenými podle ceny, od nejdražších po nejlevnější (viz obrázek 15).

[![kliknutí na tlačítko seřadí produkty od nejdražších po nejmenší](paging-and-sorting-report-data-vb/_static/image32.png)](paging-and-sorting-report-data-vb/_static/image31.png)

**Obrázek 15**: kliknutím na tlačítko seřadíte produkty od nejdražších k nejméně ([kliknutím zobrazíte obrázek v plné velikosti).](paging-and-sorting-report-data-vb/_static/image33.png)

## <a name="summary"></a>Přehled

V tomto kurzu jsme zjistili, jak implementovat výchozí možnosti stránkování a řazení, které byly stejně jednoduché jako zaškrtnutí políčka. Když uživatel seřadí nebo stránkují stránky prostřednictvím dat, podobný pracovní postup se odloží:

1. Odeslání je v důsledku
2. Událost předběžné úrovně webového ovládacího prvku s daty je aktivována (`PageIndexChanging` nebo `Sorting`).
3. Všechna data jsou znovu načtena prvkem ObjectDataSource
4. Událost post-Level webového ovládacího prvku s daty je aktivována (`PageIndexChanged` nebo `Sorted`).

Zatímco implementace základního stránkování a řazení je Breeze, je potřeba, abyste využili efektivnější vlastní stránkování nebo dále vylepšili rozhraní stránkování nebo řazení. V budoucích kurzech se seznámíte s těmito tématy.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Předchozí](creating-a-customized-sorting-user-interface-cs.md)
> [Další](efficiently-paging-through-large-amounts-of-data-vb.md)

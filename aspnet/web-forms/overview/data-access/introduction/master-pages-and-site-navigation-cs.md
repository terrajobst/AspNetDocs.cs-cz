---
uid: web-forms/overview/data-access/introduction/master-pages-and-site-navigation-cs
title: Stránky předlohy a navigace na webuC#() | Microsoft Docs
author: rick-anderson
description: Jednou z běžných vlastností webů, které jsou uživatelsky přívětivé, je to, že mají konzistentní rozložení stránky a navigační schéma pro nejrůznější weby. V tomto kurzu se podíváme na to, jak y...
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 5aee8202-a4e3-4aa9-8a95-cd5d156cea4c
msc.legacyurl: /web-forms/overview/data-access/introduction/master-pages-and-site-navigation-cs
msc.type: authoredcontent
ms.openlocfilehash: e1ddd43524a61ff2e012171eba1a8dc8efbf8f1d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78530840"
---
# <a name="master-pages-and-site-navigation-c"></a>Stránky předlohy a navigace na webu (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/6/3/463cf87c-4724-4cbc-b7b5-3f866f43ba50/ASPNET_Data_Tutorial_3_CS.exe) nebo [Stáhnout PDF](master-pages-and-site-navigation-cs/_static/datatutorial03cs1.pdf)

> Jednou z běžných vlastností webů, které jsou uživatelsky přívětivé, je to, že mají konzistentní rozložení stránky a navigační schéma pro nejrůznější weby. V tomto kurzu se naučíte, jak vytvořit konzistentní vzhled a chování napříč všemi stránkami, které se dají snadno aktualizovat.

## <a name="introduction"></a>Úvod

Jednou z běžných vlastností webů, které jsou uživatelsky přívětivé, je to, že mají konzistentní rozložení stránky a navigační schéma pro nejrůznější weby. ASP.NET 2,0 zavádí dvě nové funkce, které výrazně zjednodušují implementaci rozložení stránky a navigačního schématu v rámci webu: stránky předlohy a navigace na webu. Stránky předlohy umožňují vývojářům vytvořit šablonu na úrovni webu s vybranými upravitelnými oblastmi. Tato šablona se pak dá použít na stránky ASP.NET v lokalitě. Takové stránky ASP.NET vyžadují pouze obsah pro zadané upravitelné oblasti stránky předlohy. všechny ostatní značky na stránce předlohy jsou stejné ve všech ASP.NET stránkách, které používají stránku předlohy. Tento model umožňuje vývojářům definovat a centralizovat rozložení stránky pro celou lokalitu, což usnadňuje vytváření konzistentního vzhledu a chování napříč všemi stránkami, které lze snadno aktualizovat.

[Navigační systém lokality](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx) poskytuje mechanismus pro vývojáře stránky, který definuje mapu webu, a rozhraní API pro tuto mapu webu, které se má programově dotazovat. Nové navigační webové ovládací prvky, které jsou v nabídce, ovládacím prvku TreeView a SiteMapPath, usnadňují vykreslení všech nebo částí mapy webu v rámci společného prvku uživatelského rozhraní navigace. Budeme používat výchozího poskytovatele navigace na webu, což znamená, že naše mapa webu bude definovaná v souboru ve formátu XML.

K ilustraci těchto konceptů a k lepšímu využití webu kurzů doporučujeme tuto lekci, která definuje rozložení stránky na úrovni webu, implementaci mapy webu a přidání uživatelského rozhraní pro navigaci. Na konci tohoto kurzu budeme mít k dispozici dokonalý návrh webu pro vytváření našich webových stránek kurzu.

[![konečný výsledek tohoto kurzu](master-pages-and-site-navigation-cs/_static/image2.png)](master-pages-and-site-navigation-cs/_static/image1.png)

**Obrázek 1**: konečný výsledek tohoto kurzu ([kliknutím zobrazíte obrázek v plné velikosti](master-pages-and-site-navigation-cs/_static/image3.png))

## <a name="step-1-creating-the-master-page"></a>Krok 1: vytvoření hlavní stránky

Prvním krokem je vytvoření stránky předlohy pro daný web. Hned teď náš web obsahuje jenom typovou datovou sadu (`Northwind.xsd`ve složce `App_Code`) třídy knihoven BLL (`ProductsBLL.cs`, `CategoriesBLL.cs`a tak dále, všechny ve složce `App_Code`), databázi (`NORTHWND.MDF`, ve složce `App_Data`), konfigurační soubor (`Web.config`) a soubor šablony stylů CSS (`Styles.css`). Tyto stránky a soubory, které demonstrují použití DAL a knihoven BLL z prvních dvou kurzů, se vyčistí, protože tyto příklady budeme v budoucích kurzech podrobněji prošetřit.

![Soubory v našem projektu](master-pages-and-site-navigation-cs/_static/image4.png)

**Obrázek 2**: soubory v našem projektu

Chcete-li vytvořit hlavní stránku, klikněte pravým tlačítkem myši na název projektu v Průzkumník řešení a vyberte možnost Přidat novou položku. Pak v seznamu šablon vyberte typ hlavní stránky a pojmenujte ho `Site.master`.

[![přidání nové stránky předlohy na web](master-pages-and-site-navigation-cs/_static/image6.png)](master-pages-and-site-navigation-cs/_static/image5.png)

**Obrázek 3**: Přidání nové stránky předlohy na web ([kliknutím zobrazíte obrázek v plné velikosti](master-pages-and-site-navigation-cs/_static/image7.png))

Na stránce předlohy definujte rozložení stránky na úrovni webu. Můžete použít zobrazení Návrh a přidat libovolné rozložení nebo webové ovládací prvky, které potřebujete, nebo můžete ručně přidat značky v zobrazení zdroje. Na stránce předlohy používáme [kaskádové šablony stylů](http://www.w3schools.com/css/default.asp) pro umísťování a styly s nastaveními CSS definovanými v externím souboru `Style.css`. I když nemůžete říct od značky níže, jsou definována pravidla šablony stylů CSS tak, aby byl obsah navigace `<div>`zcela umístěný tak, aby se zobrazil vlevo a měla pevnou šířku 200 pixelů.

Site.master

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample1.aspx)]

Stránka předlohy definuje rozložení statické stránky i oblasti, které lze upravit pomocí stránek ASP.NET, které používají stránku předlohy. Tyto upravitelné oblasti obsahu jsou označeny ovládacím prvkem ContentPlaceHolder, který lze zobrazit v rámci `<div>`obsahu. Naše stránka předlohy má jeden prvek ContentPlaceHolder (`MainContent`), ale stránka předlohy může mít více prvků ContentPlaceHolder.

Pomocí značky uvedeného výše se přepíná na zobrazení Návrh zobrazuje rozložení stránky předlohy. Všechny stránky ASP.NET, které používají tuto stránku předlohy, budou mít jednotné rozložení s možností zadat značku `MainContent` oblasti.

[![stránku předlohy při prohlížení v návrhovém zobrazení](master-pages-and-site-navigation-cs/_static/image9.png)](master-pages-and-site-navigation-cs/_static/image8.png)

**Obrázek 4**: stránka předloha při zobrazení v návrhovém zobrazení ([kliknutím zobrazíte obrázek v plné velikosti](master-pages-and-site-navigation-cs/_static/image10.png))

## <a name="step-2-adding-a-homepage-to-the-website"></a>Krok 2: Přidání domovské stránky na web

Po definování stránky předlohy jsme připraveni přidat stránky ASP.NET pro web. Pojďme začít přidáním `Default.aspx`, domovské stránky našeho webu. V Průzkumník řešení klikněte pravým tlačítkem myši na název projektu a vyberte možnost Přidat novou položku. V seznamu šablon vyberte možnost webový formulář a pojmenujte soubor `Default.aspx`. Také zaškrtněte políčko vybrat hlavní stránku.

[![přidání nového webového formuláře zaškrtnutím políčka Vybrat stránku předlohy.](master-pages-and-site-navigation-cs/_static/image12.png)](master-pages-and-site-navigation-cs/_static/image11.png)

**Obrázek 5**: Přidání nového webového formuláře zaškrtnutím políčka vybrat hlavní stránku ([kliknutím zobrazíte obrázek v plné velikosti](master-pages-and-site-navigation-cs/_static/image13.png))

Po kliknutí na tlačítko OK se zobrazí výzva k výběru stránky předlohy, kterou by tato nová stránka ASP.NET měla použít. I když můžete mít v projektu více stránek předlohy, máme jenom jednu.

[![vyberte stránku předlohy, kterou by měla tato stránka ASP.NET použít.](master-pages-and-site-navigation-cs/_static/image15.png)](master-pages-and-site-navigation-cs/_static/image14.png)

**Obrázek 6**: vyberte stránku předlohy, kterou by měla stránka ASP.NET použít ([kliknutím zobrazíte obrázek v plné velikosti).](master-pages-and-site-navigation-cs/_static/image16.png)

Po výběru stránky předlohy budou nové stránky ASP.NET obsahovat následující značky:

Default.aspx

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample2.aspx)]

V direktivě `@Page` existuje odkaz na použitý soubor hlavní stránky (`MasterPageFile="~/Site.master"`) a značka stránky ASP.NET obsahuje ovládací prvek obsahu pro každé ovládací prvky ContentPlaceHolder definované na stránce předlohy s `ContentPlaceHolderID` ovládacího prvku mapování obsahu ovládacího prvku na konkrétní prvek ContentPlaceHolder. Ovládací prvek Content (obsah) je místo, kam umístíte značku, kterou chcete zobrazit v odpovídajícím prvku ContentPlaceHolder. Nastavte atribut `Title` direktivy `@Page` na hodnotu domů a přidejte k ovládacímu prvku obsahu nějaký uvítací obsah:

Default.aspx

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample3.aspx)]

Atribut `Title` v direktivě `@Page` nám umožňuje nastavit nadpis stránky ze stránky ASP.NET, i když je element `<title>` definovaný na stránce předlohy. Název můžeme také programově nastavit pomocí `Page.Title`. Všimněte si také, že odkazy na šablony stylů (například `Style.css`) se automaticky aktualizují, aby fungovaly na libovolné stránce ASP.NET bez ohledu na to, jaký adresář má stránka ASP.NET ve vztahu k hlavní stránce.

Přepínáním na zobrazení Návrh uvidíme, jak bude stránka vypadat v prohlížeči. Všimněte si, že v zobrazení Návrh pro stránku ASP.NET, na kterou lze upravovat pouze upravitelné oblasti obsahu, se značkou, která je definována na stránce předlohy, je zobrazena šedě.

[![zobrazení Návrh stránky ASP.NET zobrazuje jak upravitelné, tak i neupravitelné oblasti](master-pages-and-site-navigation-cs/_static/image18.png)](master-pages-and-site-navigation-cs/_static/image17.png)

**Obrázek 7**: zobrazení návrh stránky ASP.NET zobrazuje jak upravitelné, tak i neupravitelné oblasti ([kliknutím zobrazíte obrázek v plné velikosti).](master-pages-and-site-navigation-cs/_static/image19.png)

Když prohlížeč `Default.aspx` stránku navštíví, modul ASP.NET automaticky sloučí obsah stránky předlohy a ASP. Obsah netto a vykreslí sloučený obsah do finálního HTML, který se pošle do prohlížeče požadujícího. Při aktualizaci obsahu stránky předlohy budou všechny stránky ASP.NET, které používají tuto stránku předlohy, znovu sloučeny s novým obsahem stránky předlohy při dalším vyžádání. V krátkém případě model stránky předlohy umožňuje definovat jednu šablonu rozložení stránky (hlavní stránku), jejíž změny se projeví okamžitě napříč celou lokalitou.

## <a name="adding-additional-aspnet-pages-to-the-website"></a>Přidání dalších stránek ASP.NET na web

Pojďme se na web pokusit přidat další zástupné procedury stránky ASP.NET, která bude nakonec uchovávat různé Ukázky sestav. Bude se jednat o více než 35 ukázek, takže místo vytváření všech stránek se zástupnými procedurami teď stačí vytvořit několik prvních. Vzhledem k tomu, že bude i mnoho kategorií ukázek, pro lepší správu ukázek přidejte složku pro kategorie. Nyní přidejte následující tři složky:

- `BasicReporting`
- `Filtering`
- `CustomFormatting`

Nakonec přidejte nové soubory, jak je znázorněno na obrázku 8 v Průzkumník řešení. Při přidávání jednotlivých souborů nezapomeňte zaškrtnout políčko vybrat hlavní stránku.

![Přidejte následující soubory.](master-pages-and-site-navigation-cs/_static/image20.png)

**Obrázek 8**: přidání následujících souborů

## <a name="step-2-creating-a-site-map"></a>Krok 2: vytvoření mapy webu

Jedním z výzev ke správě webu složeného z více než několik stránek je poskytnutí jednoduchého způsobu, jak návštěvníci procházet lokalitou. Aby bylo možné začít, musí být definována navigační struktura lokality. Dále musí být tato struktura přeložena do prvků uživatelského rozhraní naviguje, jako jsou nabídky nebo popisy cesty. A konečně, tento celý proces musí být udržován a aktualizován, protože nové stránky jsou přidány do lokality a stávající odebrané. Před ASP.NET 2,0 byly vývojáři vlastní pro vytváření navigačních struktur webu, jejich údržbu a jejich překlad na prvky uživatelského rozhraní naviguje. S ASP.NET 2,0 ale vývojáři můžou využít velmi flexibilní integrovaný systém navigace v lokalitě.

Navigační systém lokality ASP.NET 2,0 poskytuje vývojářům způsob, jak definovat mapu lokality a k nim pak přistupovat prostřednictvím programového rozhraní API. ASP.NET je dodáván se zprostředkovatelem mapy webu, který očekává, že data mapy webu budou uložena v souboru XML naformátovaném určitým způsobem. Ale vzhledem k tomu, že je navigační systém lokality založený na [modelu poskytovatele](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx) , může být prodloužen na podporu alternativních způsobů serializace informací o mapě webu. Jan Prosise, [poskytovatel mapy webu SQL, kterého jste čekali](https://msdn.microsoft.com/msdnmag/issues/06/02/WickedCode/default.aspx) , ukazuje, jak vytvořit poskytovatele mapy webu, který ukládá mapu lokality do databáze SQL Server; Další možností je vytvořit [poskytovatele mapy webu na základě struktury systému souborů](http://aspnet.4guysfromrolla.com/articles/020106-1.aspx).

Pro tento kurz ale budeme používat výchozího poskytovatele mapy webu, který je dodáván s ASP.NET 2,0. Chcete-li vytvořit mapu webu, stačí kliknout pravým tlačítkem myši na název projektu v Průzkumník řešení, zvolit Přidat novou položku a zvolit možnost mapa webu. Název ponechte `Web.sitemap` a klikněte na tlačítko Přidat.

[![přidat mapu webu do projektu](master-pages-and-site-navigation-cs/_static/image22.png)](master-pages-and-site-navigation-cs/_static/image21.png)

**Obrázek 9**: Přidání mapy webu do projektu ([kliknutím zobrazíte obrázek v plné velikosti](master-pages-and-site-navigation-cs/_static/image23.png))

Soubor mapy webu je soubor XML. Všimněte si, že Visual Studio poskytuje IntelliSense pro strukturu mapy webu. Soubor mapy webu musí mít uzel `<siteMap>` jako svůj kořenový uzel, který musí obsahovat přesně jeden `<siteMapNode>` podřízený element. Tento první `<siteMapNode>` prvek může obsahovat libovolný počet podřízených `<siteMapNode>` prvků.

Definujte mapu webu pro napodobení struktury systému souborů. To znamená, že přidáte `<siteMapNode>` element pro každou ze tří složek a podřízené `<siteMapNode>` prvky pro každou ASP.NET stránku v těchto složkách, například:

Web.sitemap

[!code-xml[Main](master-pages-and-site-navigation-cs/samples/sample4.xml)]

Mapa webu definuje navigační strukturu webu, což je hierarchie, která popisuje různé části webu. Každý prvek `<siteMapNode>` v `Web.sitemap` představuje oddíl v navigační struktuře webu.

[![mapa webu představuje hierarchickou navigační strukturu.](master-pages-and-site-navigation-cs/_static/image25.png)](master-pages-and-site-navigation-cs/_static/image24.png)

**Obrázek 10**: Mapa webu představuje hierarchickou navigační strukturu ([kliknutím zobrazíte obrázek v plné velikosti).](master-pages-and-site-navigation-cs/_static/image26.png)

ASP.NET zpřístupňuje strukturu mapy webu prostřednictvím [třídy SiteMap](https://msdn.microsoft.com/library/system.web.sitemap.aspx).NET Framework. Tato třída má vlastnost `CurrentNode`, která vrací informace o oddílu, na který uživatel aktuálně navštěvuje; vlastnost `RootNode` vrátí kořen mapy webu (Domovská stránka, v mapě webu). Vlastnosti `CurrentNode` i `RootNode` vrací instance [SiteMapNode](https://msdn.microsoft.com/library/system.web.sitemapnode.aspx) , které mají vlastnosti jako `ParentNode`, `ChildNodes`, `NextSibling`, `PreviousSibling`a tak dále, které umožňují vás provedl hierarchie lokality.

## <a name="step-3-displaying-a-menu-based-on-the-site-map"></a>Krok 3: zobrazení nabídky na základě mapy webu

Přístup k datům v ASP.NET 2,0 lze provést programově, například v ASP.NET 1. x nebo deklarativně prostřednictvím nových [ovládacích prvků zdroje dat](https://msdn.microsoft.com/library/ms227679.aspx). Existuje několik vestavěných ovládacích prvků zdroje dat, jako je například ovládací prvek SqlDataSource, pro přístup k datům relační databáze, ovládací prvek ObjectDataSource, pro přístup k datům z tříd a dalších. Můžete dokonce vytvořit vlastní [ovládací prvky zdroje dat](https://msdn.microsoft.com/asp.net/reference/data/default.aspx?pull=/library/dnvs05/html/DataSourceCon1.asp).

Ovládací prvky zdroje dat slouží jako proxy mezi stránkou ASP.NET a podkladovými daty. Aby bylo možné zobrazit načtená data ovládacího prvku zdroje dat, obvykle přidáme na stránku další webový ovládací prvek a navážeme ho k ovládacímu prvku zdroje dat. Chcete-li vytvořit vazby webového ovládacího prvku k ovládacímu prvku zdroje dat, jednoduše nastavte vlastnost `DataSourceID` webového ovládacího prvku na hodnotu vlastnosti `ID` ovládacího prvku zdroje dat.

Aby bylo možné pomoci při práci s daty mapy webu, zahrnuje ASP.NET ovládací prvek SiteMapDataSource, který nám umožňuje navazovat webové ovládací prvky na mapě webu našeho webu. Dva webové ovládací prvky: strom a nabídka se běžně používají k poskytnutí uživatelského rozhraní navigace. Chcete-li vytvořit datovou mapu webu k jednomu z těchto dvou ovládacích prvků, stačí přidat prvek SiteMapDataSource na stránku spolu s ovládacím prvkem TreeView nebo menu, jehož vlastnost `DataSourceID` je nastavena odpovídajícím způsobem. Například můžeme přidat ovládací prvek nabídky na stránku předlohy pomocí následujícího kódu:

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample5.aspx)]

Pro jemnější úroveň kontroly nad vygenerovaným kódem HTML můžeme ovládací prvek SiteMapDataSource navazovat na ovládací prvek Repeater, například:

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample6.aspx)]

Ovládací prvek SiteMapDataSource vrátí hierarchii mapy webu po jedné úrovni, počínaje uzlem mapy kořenové lokality (Domovská stránka, na naší mapě webu), pak na další úroveň (základní generování sestav, filtrování sestav a přizpůsobení formátování) atd. Při vázání prvku SiteMapDataSource na Repeater vytvoří výčet první vrácené úrovně a vytvoří instanci `ItemTemplate` pro každou instanci `SiteMapNode` v této první úrovni. Aby bylo možné získat přístup k určité vlastnosti `SiteMapNode`, můžeme použít `Eval(propertyName)`, což je způsob, jak `SiteMapNode`získáme vlastnosti `Url` a `Title` pro ovládací prvek hypertextového odkazu.

Výše uvedený příklad opakovače vykreslí následující značky:

[!code-html[Main](master-pages-and-site-navigation-cs/samples/sample7.html)]

Tyto uzly mapy webu (základní sestavy, filtrování sestav a vlastní formátování) obsahují *druhou* úroveň vykreslování mapy webu, nikoli první. Důvodem je, že vlastnost `ShowStartingNode` prvku SiteMapDataSource je nastavena na hodnotu false, což způsobuje, že SiteMapDataSource obchází uzel mapy kořenové lokality a místo toho začíná vrácením druhé úrovně v hierarchii mapy webu.

Pokud chcete zobrazit podřízené objekty pro základní vytváření sestav, filtrovat sestavy a přizpůsobené formátování `SiteMapNode` s, můžeme do `ItemTemplate`počátečního opakovače přidat dalšího opakovače. Toto druhé opakování bude vázáno na vlastnost `ChildNodes` instance `SiteMapNode`, například takto:

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample8.aspx)]

Výsledkem těchto dvou Repeat je následující kód (některé značky byly odebrány pro zkrácení):

[!code-html[Main](master-pages-and-site-navigation-cs/samples/sample9.html)]

Používání stylů CSS, které jste vybrali v knize [Rachel Andrew](http://www.rachelandrew.co.uk/) [css Anthology: 101 základních tipů, triky &amp; hackatony](https://www.amazon.com/gp/product/0957921888/qid=1137565739/sr=8-1/ref=pd_bbs_1/103-0562306-3386214?n=507846&amp;s=books&amp;v=glance), jsou styly `<ul>` a `<li>`, tak aby kód vytvořil následující vizuální výstup:

![Nabídka složená ze dvou Repeat a některých šablon stylů CSS](master-pages-and-site-navigation-cs/_static/image27.png)

**Obrázek 11**: nabídka složená ze dvou Repeat a některých šablon stylů CSS

Tato nabídka je na stránce Předloha a je svázána s mapou webu definovanou v `Web.sitemap`, což znamená, že všechny změny mapy lokality se projeví přímo na všech stránkách, které používají stránku předlohy `Site.master`.

## <a name="disabling-viewstate"></a>Zakázání vlastnosti ViewState

Všechny ovládací prvky ASP.NET mohou volitelně uchovávat jejich stav do [stavu zobrazení](https://msdn.microsoft.com/msdnmag/issues/03/02/CuttingEdge/), který je serializován jako skryté pole formuláře ve vykresleném HTML. Ovládací prvky používají zobrazení stav, aby si zapamatovali jejich programově změněné stavy napříč zpětnými vazbami, jako jsou například data vázaná k datovému ovládacímu prvku webového ovládacího prvku. Přestože stav zobrazení povoluje, aby informace byly zapamatovatelné napříč zpětnými odesláními, zvyšuje velikost značek, které musí být odeslány klientovi a můžou vést k závažným dispozici determinističtějšíům stránek, pokud není úzce monitorováno. Data webové ovládací prvky, zejména ovládací prvek GridView, jsou zejména USTR pro přidání desítek dalších kilobajtů kódu na stránku. I když takový nárůst může být zanedbatelný pro uživatele se širokopásmovým přístupem nebo intranetem, může stav zobrazení prodloužit dobu odezvy pro uživatele telefonického připojení.

Chcete-li zobrazit dopad stavu zobrazení, přejděte na stránku v prohlížeči a potom zobrazte zdroj odeslaný webovou stránkou (v Internet Exploreru přejděte do nabídky Zobrazit a zvolte možnost zdroj). Můžete také zapnout [trasování stránky](https://msdn.microsoft.com/library/sfbfw58f.aspx) a zobrazit tak přidělení stavu zobrazení používaného jednotlivými ovládacími prvky na stránce. Informace o stavu zobrazení jsou serializovány ve skrytém poli formuláře s názvem `__VIEWSTATE`, umístěné v `<div>` elementu hned za otevírací `<form>` značku. Stav zobrazení je trvalý pouze v případě, že je použit webový formulář; Pokud stránka ASP.NET neobsahuje `<form runat="server">` ve své deklarativní syntaxi, nebude ve vykresleném kódu `__VIEWSTATE` skryté pole formuláře.

Pole formuláře `__VIEWSTATE` vygenerované stránkou předlohy přidá zhruba 1 800 bajtů do vygenerovaného kódu stránky. Tato dodatečná dispozici determinističtější je způsobena hlavně ovládacím prvkem Repeater, protože obsah ovládacího prvku SiteMapDataSource je trvalý pro zobrazení stavu. I když se navíc 1 800 bajtů nemusí zdát, že při použití prvku GridView s mnoha poli a záznamy se může stát, že se stav zobrazení snadno Swell faktorem 10 nebo více.

Stav zobrazení lze zakázat na úrovni stránky nebo ovládacího prvku nastavením vlastnosti `EnableViewState` na `false`, čímž se zmenší velikost vykresleného kódu. Vzhledem k tomu, že stav zobrazení webového ovládacího prvku data přechovává data vázaná na webový ovládací prvek dat napříč zpětnými vazbami, při zakázání stavu zobrazení webového ovládacího prvku data musí být data svázána s každým a každým zpětným voláním. V ASP.NET verze 1. x Tato zodpovědnost se snížila na plece vývojáře stránky; pomocí ASP.NET 2,0 však webové ovládací prvky pro data budou v případě potřeby znovu navazovat vazby na jejich ovládací prvek zdroje dat.

Chcete-li snížit stav zobrazení stránky, nastavte vlastnost `EnableViewState` ovládacího prvku Repeater na hodnotu `false`. To lze provést prostřednictvím okno Vlastnosti v Návrháři nebo deklarativně v zobrazení zdroje. Po provedení této změny by deklarativní označení Repeater mělo vypadat takto:

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample10.aspx)]

Po této změně se velikost stavového zobrazení stránky zmenší na pouhých 52 bajtů, což je 97% úspory ve velikosti zobrazení. V kurzech v celé této sérii zakážeme stav zobrazení webových ovládacích prvků dat ve výchozím nastavení, aby se snížila velikost vykresleného kódu. Ve většině příkladů se vlastnost `EnableViewState` nastaví na `false` a hotovo, takže bez zmínky. Jediný časový stav zobrazení bude popsán v tématu scénáře, kde musí být povoleno, aby webové ovládací prvky dat poskytovaly očekávané funkce.

## <a name="step-4-adding-breadcrumb-navigation"></a>Krok 4: Přidání navigace s popisem cesty

Chcete-li dokončit stránku předlohy, přidejte na každou stránku element uživatelského rozhraní navigace s popisem cesty. Navigace s popisem cesty rychle zobrazuje uživatele aktuální pozice v rámci hierarchie lokality. Přidání cesty k navigaci v ASP.NET 2,0 je snadné přidat na stránku ovládací prvek SiteMapPath; není potřeba žádný kód.

Pro náš web přidejte tento ovládací prvek do záhlaví `<div>`:

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample11.aspx)]

Popis cesty znázorňuje aktuální stránku, na kterou se uživatel navštíví v hierarchii mapy webu, a také "předchůdce uzlu mapy lokality", a to až do kořene (domů) v mapě webu.

![Navigace s popisem cesty zobrazuje aktuální stránku a její předchůdce v hierarchii mapy webu.](master-pages-and-site-navigation-cs/_static/image28.png)

**Obrázek 12**: navigace s popisem cesty zobrazuje aktuální stránku a její předchůdce v hierarchii mapy webu.

## <a name="step-5-adding-the-default-page-for-each-section"></a>Krok 5: přidání výchozí stránky pro každý oddíl

Kurzy na naší webu jsou rozdělené do různých kategorií základní vytváření sestav, filtrování, vlastní formátování atd. pomocí složky pro každou kategorii a odpovídajících kurzů jako ASP.NET stránky v této složce. Kromě toho každá složka obsahuje `Default.aspx` stránku. Pro tuto výchozí stránku zobrazíme všechny kurzy pro aktuální oddíl. To znamená, že pro `Default.aspx` ve složce `BasicReporting` máme odkazy na `SimpleDisplay.aspx`, `DeclarativeParams.aspx`a `ProgrammaticParams.aspx`. Zde je opět možné použít třídu `SiteMap` a datově datovou stránku k zobrazení těchto informací na základě mapy webu definované v `Web.sitemap`.

Pojďme znovu zobrazit neuspořádaný seznam s opakováním, ale tentokrát zobrazíme nadpis a popis kurzů. Vzhledem k tomu, že značky a kód, které mají být provedeny, bude nutné opakovat pro každou stránku `Default.aspx`, můžeme tuto logiku uživatelského rozhraní zapouzdřit do [uživatelského ovládacího prvku](https://msdn.microsoft.com/library/y6wb1a0e.aspx). Vytvořte složku na webu s názvem `UserControls` a přidejte do ní novou položku typu Webový uživatelský ovládací prvek s názvem `SectionLevelTutorialListing.ascx`a přidejte následující kód:

[![přidat nový webový uživatelský ovládací prvek do složky UserControls](master-pages-and-site-navigation-cs/_static/image30.png)](master-pages-and-site-navigation-cs/_static/image29.png)

**Obrázek 13**: Přidání nového webového uživatelského ovládacího prvku do složky `UserControls` ([kliknutím zobrazíte obrázek v plné velikosti](master-pages-and-site-navigation-cs/_static/image31.png))

SectionLevelTutorialListing.ascx

[!code-aspx[Main](master-pages-and-site-navigation-cs/samples/sample12.aspx)]

SectionLevelTutorialListing.ascx.cs

[!code-csharp[Main](master-pages-and-site-navigation-cs/samples/sample13.cs)]

V předchozím příkladu opakovače jsme data `SiteMap` do tohoto opakovače deklarativně naváže. Uživatelský ovládací prvek `SectionLevelTutorialListing` ale to provede programově. V obslužné rutině události `Page_Load` je provedena kontrola, která zajistí, že se tato stránka s adresou URL mapuje na uzel v mapě webu. Pokud se tento uživatelský ovládací prvek používá na stránce, která nemá odpovídající položku `<siteMapNode>`, `SiteMap.CurrentNode` vrátí `null` a nebudou vázána žádná data na Repeater. Za předpokladu, že máme `CurrentNode`, navážeme svoji `ChildNodes` kolekci na Repeater. Vzhledem k tomu, že je naše mapa webu nastavená tak, aby byla stránka `Default.aspx` v každé části nadřazeným uzlem všech kurzů v rámci této části, bude tento kód zobrazovat odkazy a popisy všech kurzů v sekcích, jak je znázorněno na následujícím snímku obrazovky.

Po vytvoření tohoto opakovače otevřete `Default.aspx` stránky v každé složce, přejdete do zobrazení Návrh a jednoduše přetáhněte uživatelský ovládací prvek z Průzkumník řešení na návrhovou plochu, kde se má seznam kurzů zobrazit.

[![uživatelský ovládací prvek byl přidán do default. aspx.](master-pages-and-site-navigation-cs/_static/image33.png)](master-pages-and-site-navigation-cs/_static/image32.png)

**Obrázek 14**: uživatelský ovládací prvek byl přidán do `Default.aspx` ([kliknutím zobrazíte obrázek v plné velikosti).](master-pages-and-site-navigation-cs/_static/image34.png)

[![jsou uvedeny základní kurzy vytváření sestav.](master-pages-and-site-navigation-cs/_static/image36.png)](master-pages-and-site-navigation-cs/_static/image35.png)

**Obrázek 15**: uvádíme základní kurzy vytváření sestav ([kliknutím zobrazíte obrázek v plné velikosti).](master-pages-and-site-navigation-cs/_static/image37.png)

## <a name="summary"></a>Souhrn

Po definování mapy webu a dokončení stránky předlohy teď máme konzistentní rozložení stránky a navigační schéma pro naše kurzy související s daty. Bez ohledu na to, kolik stránek do naší lokality přidáváme, aktualizujeme rozložení stránky nebo informace navigace na webu je rychlý a jednoduchý proces, protože tyto informace jsou centralizované. Konkrétně jsou informace o rozložení stránky definovány na stránce předlohy `Site.master` a mapě webu v `Web.sitemap`. Nemuseli jsme psát *žádný* kód pro dosažení tohoto rozložení stránky a navigační mechanismus pro celou lokalitu a zachováváme kompletní podporu návrháře WYSIWYG v aplikaci Visual Studio.

Po dokončení vrstvy přístupu k datům a vrstvy obchodní logiky a vytvoření konzistentního rozložení stránky a definování navigace na webu jsme připraveni začít zkoumat běžné vzory generování sestav. V [následujících](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md) třech kurzech se podíváme na základní úlohy vytváření sestav zobrazující data získaná z knihoven BLL v ovládacích prvcích GridView, DetailsView a FormView.

Šťastné programování!

## <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [ASP.NET hlavní stránky – přehled](https://msdn.microsoft.com/library/wtxbf3hh.aspx)
- [Stránky předlohy v ASP.NET 2,0](http://odetocode.com/Articles/419.aspx)
- [Šablony návrhu ASP.NET 2,0](https://msdn.microsoft.com/asp.net/reference/design/templates/default.aspx)
- [Přehled navigace na webu ASP.NET](https://msdn.microsoft.com/library/e468hxky.aspx)
- [Prověřování navigace na webu ASP.NET 2.0](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [Navigační funkce lokality ASP.NET 2,0](https://weblogs.asp.net/scottgu/archive/2005/11/20/431019.aspx)
- [Principy stavu zobrazení ASP.NET](https://msdn.microsoft.com/library/default.asp?url=/library/dnaspp/html/viewstate.asp)
- [Postupy: povolení trasování pro stránku ASP.NET](https://msdn.microsoft.com/library/94c55d08%28VS.80%29.aspx)
- [Uživatelské ovládací prvky ASP.NET](https://msdn.microsoft.com/library/y6wb1a0e.aspx)

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Liz Shulok, Dennis Patterson a Hilton Giesenow. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](creating-a-business-logic-layer-cs.md)
> [Další](creating-a-data-access-layer-vb.md)

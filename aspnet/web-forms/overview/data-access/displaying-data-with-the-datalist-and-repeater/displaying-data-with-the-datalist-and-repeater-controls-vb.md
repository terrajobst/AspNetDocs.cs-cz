---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb
title: Zobrazení dat s ovládacími prvky DataList a Repeater (VB) | Microsoft Docs
author: rick-anderson
description: V předchozích kurzech jsme použili ovládací prvek GridView k zobrazení dat. Od tohoto kurzu se podíváme na sestavování běžných vzorů vytváření sestav pomocí...
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 58618954-a9ed-4ca0-8c2d-95a5ffd9c03e
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/displaying-data-with-the-datalist-and-repeater-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 4e7aaa1701da67aec61505b64a835ef41031bb13
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78626362"
---
# <a name="displaying-data-with-the-datalist-and-repeater-controls-vb"></a>Zobrazení dat ovládacími prvky DataList a Repeater (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_29_VB.exe) nebo [Stáhnout PDF](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/datatutorial29vb1.pdf)

> V předchozích kurzech jsme použili ovládací prvek GridView k zobrazení dat. Od tohoto kurzu se podíváme na sestavování běžných vzorů vytváření sestav s ovládacími prvky DataList a Repeater, počínaje základy zobrazování dat pomocí těchto ovládacích prvků.

## <a name="introduction"></a>Úvod

V všech příkladech v posledních 28 kurzech, pokud jsme potřebovali Zobrazit více záznamů ze zdroje dat, který jsme aktivovali v ovládacím prvku GridView. Prvek GridView Vykreslí řádek pro každý záznam ve zdroji dat a zobrazí datová pole záznamu s ve sloupcích. I když ovládací prvek GridView vytvoří přichycení k zobrazení, stránkám, řazení, úpravám a odstraňování dat, jeho vzhled je boxy. Kromě toho je kód zodpovědný za strukturu GridView s pevným kódem, který obsahuje `<table>` HTML s řádkem tabulky (`<tr>`) pro každý záznam a buňkou tabulky (`<td>`) pro každé pole.

Chcete-li zajistit větší stupeň přizpůsobení při zobrazení více záznamů, ASP.NET 2,0 nabízí ovládací prvky DataList a Repeater (obě jsou také k dispozici v ASP.NET verze 1. x). Ovládací prvky DataList a Repeater vykreslují jejich obsah pomocí šablon spíše než BoundFields, CheckBoxFields, ButtonFields a tak dále. Podobně jako v prvku GridView, se DataList vykresluje jako HTML `<table>`, ale umožňuje zobrazení více záznamů zdroje dat pro každý řádek tabulky. Potom na druhé straně vykreslí žádné další značky, než je explicitně zadáte, a je ideální kandidát, pokud potřebujete přesnou kontrolu nad vygenerovaným kódem.

V dalších desítkách nebo v nich se podíváme na sestavování běžných vzorů vytváření sestav s ovládacími prvky DataList a Repeater, počínaje základy zobrazování dat pomocí těchto ovládacích prvků. Podíváme se, jak tyto ovládací prvky naformátovat, jak změnit rozložení záznamů zdrojů dat ve scénářích DataList, běžných hlavních a podrobných scénářích, způsobech úprav a odstranění dat, způsobu stránky záznamů a tak dále.

## <a name="step-1-adding-the-datalist-and-repeater-tutorial-web-pages"></a>Krok 1: Přidání webových stránek kurzu DataList a Repeater

Před zahájením tohoto kurzu si nejdřív počkejte, než se přidá stránky ASP.NET, které budeme potřebovat pro tento kurz, a další několik kurzů, které se týkají zobrazení dat pomocí DataList a Repeater. Začněte vytvořením nové složky v projektu s názvem `DataListRepeaterBasics`. V dalším kroku přidejte do této složky následující pět ASP.NET stránek a všechny je nakonfigurované tak, aby používaly stránku předlohy `Site.master`:

- `Default.aspx`
- `Basics.aspx`
- `Formatting.aspx`
- `RepeatColumnAndDirection.aspx`
- `NestedControls.aspx`

![Vytvořte složku DataListRepeaterBasics a přidejte stránky ASP.NET kurzu.](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image1.png)

**Obrázek 1**: vytvoření složky pro `DataListRepeaterBasics` a přidání ASP.NETových stránek kurzu

Otevřete stránku `Default.aspx` a přetáhněte uživatelský ovládací prvek `SectionLevelTutorialListing.ascx` ze složky `UserControls` na návrhovou plochu. Tento uživatelský ovládací prvek, který jsme vytvořili v kurzu [hlavní stránky a navigace na webu](../introduction/master-pages-and-site-navigation-vb.md) , vytvoří výčet mapy lokality a zobrazí kurzy z aktuální části v seznamu s odrážkami.

[![přidat uživatelský ovládací prvek SectionLevelTutorialListing. ascx do default. aspx](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image3.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image2.png)

**Obrázek 2**: Přidání uživatelského ovládacího prvku `SectionLevelTutorialListing.ascx` do `Default.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image4.png))

Aby se seznam s odrážkami zobrazoval v sestavách DataList a Repeater, budeme vytvářet, musíme je přidat na mapu webu. Otevřete soubor `Web.sitemap` a přidejte následující kód po přidání značek uzlu mapy webu pro vlastní tlačítka:

[!code-xml[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample1.xml)]

![Aktualizovat mapu webu tak, aby obsahovala nové stránky ASP.NET](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image5.png)

**Obrázek 3**: aktualizace mapy webu tak, aby obsahovala nové stránky ASP.NET

## <a name="step-2-displaying-product-information-with-the-datalist"></a>Krok 2: zobrazení informací o produktu pomocí prvku DataList

Podobně jako třída FormView, Vykreslený výstup ovládacího prvku DataList závisí na šablonách, nikoli BoundFields, CheckBoxFields a tak dále. Na rozdíl od třídy FormView je prvek DataList navržen tak, aby zobrazoval sadu záznamů, nikoli Solitary jednu. Pojďme začít s tímto kurzem a podívat se na informace o vazbě produktu na DataList. Začněte tím, že otevřete stránku `Basics.aspx` ve složce `DataListRepeaterBasics`. Dále přetáhněte prvek DataList z panelu nástrojů na Návrhář. Jak ukazuje obrázek 4, před zadáním šablon DataList je Návrhář zobrazí jako šedý rámeček.

[![přetáhněte prvek DataList z panelu nástrojů na Návrhář.](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image7.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image6.png)

**Obrázek 4**: přetáhněte prvek DataList z panelu nástrojů do návrháře ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image8.png)).

Z inteligentní značky DataList s přidejte nové prvky ObjectDataSource a nakonfigurujte ji tak, aby používala `GetProducts` metodu `ProductsBLL` třídy s. Vzhledem k tomu, že v tomto kurzu znovu vytvoříme prvek DataList, který je jen pro čtení, v okně Průvodce VLOŽENÍm, aktualizací a ODSTRANĚNÍm nastavte rozevírací seznam na (žádné).

[![se rozhodnout pro vytvoření nového prvku ObjectDataSource](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image10.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image9.png)

**Obrázek 5**: možnost vytvoření nového prvku ObjectDataSource ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image11.png))

[![nakonfigurovat prvek ObjectDataSource tak, aby používal třídu ProductsBLL](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image13.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image12.png)

**Obrázek 6**: Konfigurace prvku ObjectDataSource, aby používal třídu `ProductsBLL` ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image14.png))

[![načíst informace o všech produktech pomocí metody GetProducts](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image16.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image15.png)

**Obrázek 7**: načtení informací o všech produktech pomocí metody `GetProducts` ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image17.png))

Po nakonfigurování prvku ObjectDataSource a jeho přidružení k prvku DataList prostřednictvím inteligentní značky vytvoří Visual Studio automaticky `ItemTemplate` v prvku DataList, který zobrazí název a hodnotu každého datového pole vráceného zdrojem dat (viz následující kód). Výchozí vzhled `ItemTemplate` s je stejný jako u šablon, které se automaticky vytvořily při vytváření vazby zdroje dat ke třídě FormView prostřednictvím návrháře.

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample2.aspx)]

> [!NOTE]
> Při navázání vazby zdroje dat k ovládacímu prvku FormView prostřednictvím inteligentní značky FormView s vytvoří Visual Studio `ItemTemplate`, `InsertItemTemplate`a `EditItemTemplate`. U prvku DataList se však vytvoří pouze `ItemTemplate`. Je to proto, že prvek DataList nemá stejné integrované úpravy a vkládání podpory, které nabízí třída FormView. Prvek DataList obsahuje události související s úpravou a odstraněním a podporu úprav a odstranění lze přidat s bitem kódu, ale neexistuje žádná jednoduchá podpora jako u třídy FormView. V budoucím kurzu uvidíte, jak zahrnout úpravy a odstraňování podpory v rámci DataList.

Počkejte prosím chvíli, než se vylepšit vzhled této šablony. Místo zobrazení všech datových polí se zobrazí pouze název produktu, dodavatel, kategorie, množství na jednotku a cena za jednotku. Kromě toho je možné zobrazit název v nadpisu `<h4>` a rozvrhnout zbývající pole pomocí `<table>` pod záhlavím.

Chcete-li provést tyto změny, můžete buď použít funkce pro úpravu šablony v Návrháři z inteligentní značky DataList s klikněte na odkaz Upravit šablony nebo můžete šablonu upravit ručně prostřednictvím deklarativní syntaxe stránky. Použijete-li v Návrháři možnost Upravit šablony, výsledný kód nemusí přesně odpovídat následující značce, ale při prohlížení prohlížeče by měl vypadat velmi podobně jako snímek obrazovky znázorněný na obrázku 8.

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample3.aspx)]

> [!NOTE]
> Výše uvedený příklad používá webové ovládací prvky Label, jejichž vlastnost `Text` je přiřazena hodnota syntaxe DataBinding. Alternativně jsme mohli vypustit popisky úplně a zadat jenom syntaxi datové vazby. To znamená, že místo použití `<asp:Label ID="CategoryNameLabel" runat="server" Text='<%# Eval("CategoryName") %>' />` můžeme místo toho použít deklarativní syntax `<%# Eval("CategoryName") %>`.

Ponecháním webové ovládací prvky popisek ale nabízí dvě výhody. Za prvé to poskytuje jednodušší způsob formátování dat na základě dat, jak uvidíme v dalším kurzu. Za druhé, možnost Upravit šablony v Návrháři neumožňuje zobrazit deklarativní syntaxi datové vazby, která se zobrazí mimo nějaký webový ovládací prvek. Místo toho je rozhraní úprav šablon navrženo tak, aby usnadnilo práci se statickými a webovými ovládacími prvky a předpokládá, že všechny datové vazby budou provedeny pomocí dialogového okna Upravit datové vazby, které je přístupné z inteligentních značek webové ovládací prvky.

Proto při práci s ovládacím prvek DataList, který poskytuje možnost upravovat šablony prostřednictvím návrháře, raději použít webové ovládací prvky popisku, aby byl obsah přístupný prostřednictvím rozhraní Edit Templates. Jak vidíte krátce, vyžaduje se, aby se obsah šablony upravoval ze zobrazení zdroje. V důsledku toho při sestavování šablon Repeater I často vynecháte webové ovládací prvky popisku, pokud Nevím, že není nutné naformátovat vzhled vázaného textu dat na základě programové logiky.

[![výstupy každého produktu se vykreslují pomocí DataList s ItemTemplate](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image19.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image18.png)

**Obrázek 8**: každý výstup produktu se vykresluje pomocí `ItemTemplate` DataList s ([kliknutím zobrazíte obrázek v plné velikosti).](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image20.png)

## <a name="step-3-improving-the-appearance-of-the-datalist"></a>Krok 3: vylepšení vzhledu prvku DataList

Podobně jako v prvku GridView nabízí prvek DataList mnoho vlastností souvisejících s Style, například `Font`, `ForeColor`, `BackColor`, `CssClass`, `ItemStyle`, `AlternatingItemStyle`, `SelectedItemStyle`a tak dále. Při práci s ovládacími prvky GridView a DetailsView jsme vytvořili soubory skinu v motivu `DataWebControls`, který předem definoval vlastnosti `CssClass` pro tyto dva ovládací prvky a vlastnost `CssClass` pro několik jejich podvlastností (`RowStyle`, `HeaderStyle`a tak dále). Pojďme to udělat pro prvek DataList.

Jak je popsáno v kurzu [zobrazení dat s](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md) využitím ObjectDataSource, soubor skinu určuje výchozí vlastnosti týkající se vzhledu webového ovládacího prvku. Motiv je kolekce souborů skinu, stylů CSS, obrázků a JavaScriptu, které definují konkrétní vzhled a chování webu. V kurzu *zobrazení dat pomocí ObjectDataSource* jsme vytvořili motiv `DataWebControls` (který je implementovaný jako složka ve `App_Themes` složce), která má aktuálně dva soubory skinu – `GridView.skin` a `DetailsView.skin`. Pojďme přidat třetí soubor skinu, abyste určili předdefinované nastavení stylu pro prvek DataList.

Chcete-li přidat soubor skinu, klikněte pravým tlačítkem myši na složku `App_Themes/DataWebControls`, zvolte možnost Přidat novou položku a v seznamu vyberte možnost soubor skinu. Pojmenujte soubor `DataList.skin`.

[![vytvořit nový soubor skinu s názvem DataList. Skin](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image22.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image21.png)

**Obrázek 9**: vytvořte nový soubor skinu s názvem `DataList.skin` ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image23.png)).

Pro soubor `DataList.skin` použijte následující kód:

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample4.aspx)]

Tato nastavení přiřazují stejné třídy CSS odpovídajícím vlastnostem DataList, jako byly použity s ovládacími prvky GridView a DetailsView. Třídy CSS, které jsou zde použity `DataWebControlStyle`, `AlternatingRowStyle`, `RowStyle`a tak dále, jsou definovány v souboru `Styles.css` a přidány v předchozích kurzech.

Při přidání tohoto souboru skinu se vzhled prvku DataList v Návrháři aktualizuje (možná budete muset aktualizovat zobrazení návrháře, aby se zobrazily účinky nového souboru skinu; v nabídce zobrazení vyberte aktualizovat). Jak ukazuje obrázek 10, každý alternující produkt má světle růžovou barvu pozadí.

[![vytvořit nový soubor skinu s názvem DataList. Skin](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image25.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image24.png)

**Obrázek 10**: vytvořte nový soubor skinu s názvem `DataList.skin` ([kliknutím zobrazíte obrázek v plné velikosti).](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image26.png)

## <a name="step-4-exploring-the-datalist-s-other-templates"></a>Krok 4: zkoumání dalších šablon DataList

Kromě `ItemTemplate`podporuje DataList šest dalších volitelných šablon:

- Pokud je tato `HeaderTemplate` k dispozici, přidá do výstupu řádek záhlaví a použije se k vykreslení tohoto řádku.
- `AlternatingItemTemplate` použito pro vykreslení střídajících se položek
- `SelectedItemTemplate` slouží k vykreslení vybrané položky; Vybraná položka je položka, jejíž index odpovídá [vlastnosti`SelectedIndex`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.selectedindex.aspx) prvků DataList.
- `EditItemTemplate` použito k vykreslení upravované položky
- `SeparatorTemplate` je-li k dispozici, přidá oddělovač mezi každou položku a použije se k vykreslení tohoto oddělovače.
- `FooterTemplate` – Pokud je k dispozici, přidá do výstupu řádek zápatí a použije se k vykreslení tohoto řádku.

Při zadání `HeaderTemplate` nebo `FooterTemplate`přidá prvek DataList do vykresleného výstupu další řádek záhlaví nebo zápatí. Podobně jako u řádků záhlaví a zápatí prvku GridView, záhlaví a zápatí v prvku DataList nejsou svázána s daty. Proto jakákoli syntaxe datové vazby v `HeaderTemplate` nebo `FooterTemplate`, která se pokusí o přístup k vázaným datům, vrátí prázdný řetězec.

> [!NOTE]
> Jak jsme viděli v kurzu pro [zobrazení souhrnných informací v zápatí GridView s](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md) , zatímco řádky hlaviček a zápatí nepodporují syntaxi datových vazeb, informace specifické pro data mohou být vloženy přímo do těchto řádků z obslužné rutiny události GridView `RowDataBound`. Tato technika se dá použít k výpočtu průběžných součtů nebo jiných informací z dat svázaných s ovládacím prvkem a k přiřazení těchto informací do zápatí. Stejný koncept lze použít na ovládací prvky DataList a Repeater; Jediným rozdílem je, že pro prvky DataList a Repeater se vytvoří obslužná rutina události pro událost `ItemDataBound` (namísto `RowDataBound` události).

V našem příkladu mají názvy informace o produktu zobrazené v horní části ovládacího prvku DataList s výsledkem `<h3>` záhlaví. Chcete-li to dosáhnout, přidejte `HeaderTemplate` s odpovídajícím označením. V návrháři to lze provést kliknutím na odkaz Upravit šablony v inteligentní značce DataList s, výběrem šablony záhlaví z rozevíracího seznamu a zadáním textu po výběru možnosti Nadpis 3 v rozevíracím seznamu styl (viz obrázek 11).

[![přidat šablona HeaderTemplate s informacemi o textovém produktu](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image28.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image27.png)

**Obrázek 11**: Přidání `HeaderTemplate` s použitím informací o textovém produktu ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image29.png))

Alternativně lze tuto možnost přidat deklarativně zadáním následujícího kódu v rámci značek `<asp:DataList>`:

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample5.html)]

Chcete-li přidat do každého seznamu produktů nějaký úsek, přidejte `SeparatorTemplate`, který obsahuje čáru mezi jednotlivými oddíly. Značka Horizontal Rule (`<hr>`) přidá takovému oddělovači. Vytvořte `SeparatorTemplate` tak, aby byl následující kód:

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample6.html)]

> [!NOTE]
> Podobně jako `HeaderTemplate` a `FooterTemplates`, `SeparatorTemplate` není vázán na žádný záznam ze zdroje dat, a proto nemůže získat přímý přístup k záznamům zdroje dat, které jsou vázány na prvek DataList.

Po přidání tohoto doplňku při prohlížení stránky v prohlížeči by se měl zobrazit podobný obrázek 12. Poznamenejte si řádek záhlaví a řádek mezi každým seznamem produktů.

[![prvek DataList obsahuje řádek záhlaví a horizontální pravidlo mezi každým seznamem produktů.](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image31.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image30.png)

**Obrázek 12**: prvek DataList obsahuje řádek záhlaví a horizontální pravidlo mezi každým seznamem produktů ([kliknutím zobrazíte obrázek v plné velikosti).](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image32.png)

## <a name="step-5-rendering-specific-markup-with-the-repeater-control"></a>Krok 5: vykreslení specifických značek pomocí ovládacího prvku Repeater

Pokud při návštěvě příkladu DataList z obrázku 12 provedete zobrazení nebo zdroj, zjistíte, že prvek DataList vygeneruje HTML `<table>` obsahující řádek tabulky (`<tr>`) s jednou buňkou tabulky (`<td>`) pro každou položku, která je svázána s ovládacím prvky DataList. Tento výstup je ve skutečnosti totožný s tím, co by bylo vygenerováno z prvku GridView s jednou TemplateField. Jak uvidíme v budoucím kurzu, DataList umožní další přizpůsobení výstupu a umožní nám zobrazit několik záznamů zdrojů dat na řádek tabulky.

Co když nechcete, aby vygenerovali `<table>`HTML, ale? Pro celkovou a úplnou kontrolu nad značkou vygenerovanou webovým ovládacím prvkem dat je nutné použít ovládací prvek Repeater. Podobně jako u prvku DataList, je opakovač založen na šablonách. Repeater ale nabízí jenom tyto pět šablon:

- `HeaderTemplate` je-li k dispozici, přidá zadaný kód před položky
- `ItemTemplate` slouží k vykreslování položek
- `AlternatingItemTemplate`, pokud je k dispozici, použité pro vykreslení střídajících se položek
- `SeparatorTemplate` je-li k dispozici, přidá zadaný kód mezi každou položku
- `FooterTemplate` – Pokud je k dispozici, přidá zadaný kód za položky.

V ASP.NET 1. x byl ovládací prvek Repeater běžně použit k zobrazení seznamu s odrážkami, jehož data pocházejí z určitého zdroje dat. V takovém případě by `HeaderTemplate` a `FooterTemplates` obsahovaly značky otevírací a ukončovací `<ul>`, zatímco `ItemTemplate` by obsahovaly `<li>` elementy se syntaxí DataBinding. Tento přístup se pořád používá v ASP.NET 2,0, jak jsme viděli ve dvou příkladech na [stránkách předlohy a v navigaci na webu](../introduction/master-pages-and-site-navigation-vb.md) .

- Na stránce předloha `Site.master` byl pro zobrazení seznamu s odrážkami obsahu mapy webu nejvyšší úrovně použit příkaz Repeat (základní vytváření sestav, filtrování sestav, přizpůsobené formátování atd.). Další vnořený Repeater se použil k zobrazení oddílů podřízených částí na nejvyšší úrovni.
- V `SectionLevelTutorialListing.ascx`se pro zobrazení seznamu s odrážkami v části mapy aktuálního webu použil Repeater.

> [!NOTE]
> ASP.NET 2,0 zavádí nový [ovládací prvek BulletedList](https://msdn.microsoft.com/library/ms228101.aspx), který může být svázán s ovládacím prvkem zdroje dat, aby bylo možné zobrazit jednoduchý seznam s odrážkami. Pomocí ovládacího prvku BulletedList není nutné zadávat žádné položky HTML v seznamu. místo toho jednoduše označíte pole data, které se má zobrazit jako text pro každou položku seznamu.

Repeater slouží jako catch All data Web Control. Pokud není existující ovládací prvek, který generuje potřebný kód, lze použít ovládací prvek Repeater. Pro ilustraci pomocí opakovače má mít seznam kategorií zobrazených nad informacemi o produktu DataList vytvořenými v kroku 2. Konkrétně se mají kategorie zobrazovat v HTML s jedním řádkem `<table>` s každou kategorií zobrazenou jako sloupec v tabulce.

Chcete-li to provést, začněte přetažením ovládacího prvku Repeater z panelu nástrojů do návrháře, nad rámec informací o produktu DataList. Stejně jako u prvku DataList se úvodní okno zpočátku zobrazí jako šedé pole, dokud není definováno jeho šablony.

[![přidání opakovače do návrháře](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image34.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image33.png)

**Obrázek 13**: Přidání opakovače do návrháře ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image35.png))

Existuje pouze jedna možnost v inteligentní značce Repeater: zvolit zdroj dat. Přihlaste se k vytvoření nového prvku ObjectDataSource a nakonfigurujte ho tak, aby používal metodu `CategoriesBLL` třídy s `GetCategories`.

[![vytvořit nový prvek ObjectDataSource](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image37.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image36.png)

**Obrázek 14**: vytvoření nového prvku ObjectDataSource ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image38.png))

[![nakonfigurovat prvek ObjectDataSource tak, aby používal třídu CategoriesBLL](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image40.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image39.png)

**Obrázek 15**: Konfigurace prvku ObjectDataSource, aby používal třídu `CategoriesBLL` ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image41.png))

[![načíst informace o všech kategoriích pomocí metody GetCategories](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image43.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image42.png)

**Obrázek 16**: načtení informací o všech kategoriích pomocí metody `GetCategories` ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image44.png))

Na rozdíl od prvku DataList, Visual Studio po vytvoření vazby na zdroj dat automaticky nevytvoří pro Repeater hodnotu ItemTemplate. Šablony opakování se navíc nedají konfigurovat prostřednictvím návrháře a musí se zadat deklarativně.

Chcete-li zobrazit kategorie jako `<table>` s jedním řádkem se sloupcem pro každou kategorii, potřebujeme, aby Repeater vygenerovalo kód podobný následujícímu:

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample7.html)]

Vzhledem k tomu, že text `<td>Category X</td>` je část, která se opakuje, zobrazí se tato část v argumentu Repeater s možností ItemTemplate. Značky, které se zobrazí před `<table><tr>` –, budou umístěny do `HeaderTemplate`, zatímco koncová značka-`</tr></table>`-bude umístěna do `FooterTemplate`. Chcete-li zadat tato nastavení šablony, přejděte na deklarativní část stránky ASP.NET kliknutím na tlačítko zdroj v levém dolním rohu a zadejte následující syntaxi:

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample8.aspx)]

Repeater vygeneruje přesné označení, jak je určeno jeho šablonami, nic dalšího, nic neméně. Obrázek 17 ukazuje výstup opakování při prohlížení v prohlížeči.

[![tabulce &lt;HTML s jedním řádkem&gt; seznam všech kategorií v samostatném sloupci.](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image46.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image45.png)

**Obrázek 17**: `<table>` HTML s jedním řádkem obsahuje všechny kategorie v samostatném sloupci ([kliknutím zobrazíte obrázek v plné velikosti).](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image47.png)

## <a name="step-6-improving-the-appearance-of-the-repeater"></a>Krok 6: vylepšení vzhledu opakovače

Vzhledem k tomu, že opakovač vygeneruje přesně značky určené jeho šablonami, měl by být neočekávaně neočekávaně neexistují žádné vlastnosti, které se vztahují na styly pro Repeater. Chcete-li změnit vzhled obsahu generovaného tímto argumentem, je nutné ručně přidat potřebný obsah HTML nebo CSS přímo do šablon Repeater.

V našem příkladu mají mít sloupce kategorie alternativní barvy pozadí, jako je například se střídavými řádky v prvku DataList. Aby to bylo možné, potřebujeme přiřadit třídu `RowStyle` šablon stylů CSS k jednotlivým položkám Repeat a `AlternatingRowStyle` třídy CSS pro každou střídající se položku Repeat prostřednictvím šablon `ItemTemplate` a `AlternatingItemTemplate`, například takto:

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample9.aspx)]

Umožňuje také přidat řádek záhlaví do výstupu s kategoriemi textový produkt. Vzhledem k tomu, že jsme nevěděli, kolik sloupců náš výsledný `<table>` bude sestávat z, nejjednodušší způsob, jak vygenerovat řádek záhlaví, který je zaručený pro všechny sloupce, je použití *dvou* `<table>` s. První `<table>` bude obsahovat dva řádky záhlaví a řádek, který bude obsahovat druhý, jednořádkový `<table>` s jedním řádkem, který má sloupec pro každou kategorii v systému. To znamená, že chceme emitovat následující značky:

[!code-html[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample10.html)]

Následující `HeaderTemplate` a `FooterTemplate` vedou k požadovaným značkám:

[!code-aspx[Main](displaying-data-with-the-datalist-and-repeater-controls-vb/samples/sample11.aspx)]

Obrázek 18 znázorňuje opakování po provedení těchto změn.

[![alternativní sloupce kategorie v barvě pozadí a obsahuje řádek záhlaví](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image49.png)](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image48.png)

**Obrázek 18**: alternativní sloupce kategorie v barvě pozadí a obsahuje řádek záhlaví ([kliknutím zobrazíte obrázek v plné velikosti](displaying-data-with-the-datalist-and-repeater-controls-vb/_static/image50.png))

## <a name="summary"></a>Souhrn

I když ovládací prvek GridView usnadňuje zobrazení, úpravy, odstranění, řazení a stránkování dat, je vzhled velmi boxy a podobný mřížce. Pro lepší kontrolu vzhledu musíme zapnout ovládací prvky DataList nebo Repeater. Oba tyto ovládací prvky zobrazují sadu záznamů pomocí šablon místo BoundFields, CheckBoxFields a tak dále.

DataList se vykresluje jako HTML `<table>`, který ve výchozím nastavení zobrazuje každý záznam zdroje dat v jediném řádku tabulky, stejně jako prvek GridView s jednou vlastností TemplateField. Jak uvidíme v budoucím kurzu, DataList ale umožňuje zobrazení více záznamů na řádek tabulky. V opačném případě striktně vygeneruje značku určenou ve svých šablonách; nepřidává žádné další značky, proto se obvykle používá k zobrazení dat v prvcích HTML kromě `<table>` (například v seznamu s odrážkami).

I když DataList a Repeater nabízí větší flexibilitu v vykresleném výstupu, nemá mnoho z vestavěných funkcí, které se nacházejí v prvku GridView. Jak prověříme v nadcházejících kurzech, některé z těchto funkcí se dají připojit zpátky bez příliš velkého úsilí, ale mějte na paměti, že použití prvku DataList nebo Repeater místo prvku GridView omezuje funkce, které můžete použít, aniž by bylo nutné tyto funkce implementovat. uživatelské.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Recenzenti potenciálních zákazníků pro tento kurz byly Yaakov Ellis, Liz Shulok, Randy Schmidt a Stacy Park. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](nested-data-web-controls-cs.md)
> [Další](formatting-the-datalist-and-repeater-based-upon-data-vb.md)

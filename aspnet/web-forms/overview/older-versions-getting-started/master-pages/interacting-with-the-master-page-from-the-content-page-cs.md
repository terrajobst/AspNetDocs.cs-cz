---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-cs
title: Interakce se stránkou předlohy ze stránky obsahu (C#) | Microsoft Docs
author: rick-anderson
description: Prověřuje způsob volání metod, nastavení vlastností atd. hlavní stránky z kódu na stránce obsahu.
ms.author: riande
ms.date: 07/11/2008
ms.assetid: 32d54638-71b2-491d-81f4-f7417a13a62f
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-master-page-from-the-content-page-cs
msc.type: authoredcontent
ms.openlocfilehash: 5ef030d3bed117e98fdd090f7c63643354b47f76
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74583880"
---
# <a name="interacting-with-the-master-page-from-the-content-page-c"></a>Interakce stránky předlohy se stránkou obsahu (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_06_CS.zip) nebo [stažení PDF](https://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_06_CS.pdf)

> Prověřuje způsob volání metod, nastavení vlastností atd. hlavní stránky z kódu na stránce obsahu.

## <a name="introduction"></a>Úvod

V průběhu posledních pěti kurzů jsme si vyhledali, jak vytvořit hlavní stránku, definovat oblasti obsahu, navazovat ASP.NET stránky na hlavní stránku a definovat obsah specifický pro stránku. Když návštěvník požádá o konkrétní stránku obsahu, značky obsahu a stránek předlohy se ponechají za běhu a výsledkem je vykreslování sjednocené hierarchie ovládacích prvků. Proto jsme již viděli jeden ze způsobů, ve kterém může stránka předlohy a jedna z jeho stránek obsahu interagovat: stránka obsahu vypíše kód, který se má převést na ovládací prvky ContentPlaceHolder stránky předlohy.

Ještě jsme prozkoumali, jakým způsobem může stránka předlohy a stránka obsahu interagovat programově. Kromě definování značek pro ovládací prvky ContentPlaceHolder stránky předlohy může stránka obsahu také přiřadit hodnoty k veřejným vlastnostem hlavní stránky a vyvolat její veřejné metody. Podobně může stránka předlohy komunikovat se stránkami obsahu. I když je programová interakce mezi hlavní stránkou a stránkou obsahu méně společná než interakce mezi jejich deklarativními označeními, existuje mnoho scénářů, ve kterých je třeba takovou programovou interakci potřebovat.

V tomto kurzu prověříme, jak může stránka s obsahem programově interagovat s hlavní stránkou. v dalším kurzu se podíváme na to, jak může stránka předlohy podobně pracovat se stránkami obsahu.

## <a name="examples-of-programmatic-interaction-between-a-content-page-and-its-master-page"></a>Příklady programové interakce mezi stránkou obsahu a její stránkou předlohy

V případě, že je nutné nakonfigurovat určitou oblast stránky na základě stránky, používáme ovládací prvek ContentPlaceHolder. Ale v čem se situace, kdy většina stránek potřebuje vygenerovat určitý výstup, ale malý počet stránek je potřeba přizpůsobit, aby se zobrazil něco jiného? Jeden takový příklad, který jsme prozkoumali v kurzu [*vícenásobné prvky ContentPlaceHolder a výchozí obsah*](multiple-contentplaceholders-and-default-content-cs.md) , zahrnuje zobrazení přihlašovacího rozhraní na každé stránce. I když by většina stránek obsahovala přihlašovací rozhraní, měla by se potlačit pro několik stránky, například: hlavní přihlašovací stránka (`Login.aspx`); Stránka vytvořit účet; a další stránky, které jsou přístupné jenom pro ověřené uživatele. Kurz [*vícenásobné prvky ContentPlaceHolder a výchozí obsah*](multiple-contentplaceholders-and-default-content-cs.md) ukázal, jak definovat výchozí obsah pro ovládací prvek ContentPlaceHolder na stránce předlohy a jak ho přepsat na těchto stránkách, kde nebyl výchozí obsah požadovaný.

Další možností je vytvořit veřejnou vlastnost nebo metodu v rámci stránky předlohy, která označuje, jestli se má zobrazit nebo skrýt přihlašovací rozhraní. Například stránka předlohy může obsahovat veřejnou vlastnost s názvem `ShowLoginUI`, jejíž hodnota byla použita k nastavení vlastnosti `Visible` ovládacího prvku pro přihlášení na stránce předlohy. Tyto stránky obsahu, kde by mělo být potlačeno uživatelské rozhraní přihlášení, by mohlo následně programově nastavit vlastnost `ShowLoginUI` na hodnotu `false`.

Nejběžnější příklad interakce obsahu a stránky předlohy se zobrazí, když se data zobrazená na stránce předlohy musí aktualizovat po zobrazení některé akce na stránce obsahu. Zvažte hlavní stránku, která obsahuje prvek GridView, který zobrazuje pět naposledy přidaných záznamů z konkrétní databázové tabulky a že jedna z jejích stránek obsahu obsahuje rozhraní pro přidávání nových záznamů do stejné tabulky.

Když uživatel navštíví stránku, aby přidal nový záznam, uvidí pět naposledy přidaných záznamů zobrazených na stránce předlohy. Po vyplnění hodnot pro sloupce nového záznamu odešle formulář. Za předpokladu, že prvek GridView na stránce předlohy má svou vlastnost `EnableViewState` nastavenou na hodnotu true (výchozí), je jeho obsah znovu načten ze stavu zobrazení a v důsledku toho se zobrazí pět stejných záznamů i v případě, že se do databáze právě přidal novější záznam. To může Zaměňujte uživatele.

> [!NOTE]
> I když je stav zobrazení prvku GridView zakázán tak, aby se po každém postbacku znovu váže na jeho podkladový zdroj dat, stále nezobrazuje právě přidaný záznam, protože data jsou svázána s podřízeným komponentou v životním cyklu stránky, než když je nový záznam přidán do datab ASE.

Chcete-li tento problém napravit, aby byl právě přidaný záznam zobrazen v prvku GridView stránky předlohy při zpětném volání, je nutné pokyn prvku GridView, aby *po* přidání nového záznamu do databáze znovu navázala jeho zdroj dat. To vyžaduje interakci mezi stránkami obsahu a předlohou, protože rozhraní pro přidání nového záznamu (a jeho obslužných rutin událostí) jsou na stránce obsahu, ale ovládací prvek GridView, který je třeba aktualizovat, je na stránce předlohy.

Vzhledem k tomu, že aktualizace zobrazení hlavní stránky z obslužné rutiny události na stránce obsahu je jedním z nejběžnějších potřeb pro interakci obsahu a stránky předlohy, Podívejme se na toto téma podrobněji. Stažení pro tento kurz obsahuje databázi edice Microsoft SQL Server 2005 Express s názvem `NORTHWIND.MDF` ve složce `App_Data` webu. Databáze Northwind uchovává informace o produktech, zaměstnancích a prodejích pro fiktivní firmu, která je Northwind Traders.

Krok 1 projde zobrazením pěti naposledy přidaných produktů v prvku GridView na stránce předlohy. Krok 2 vytvoří stránku obsahu pro přidávání nových produktů. Krok 3 se zabývá vytvořením veřejných vlastností a metod na stránce předlohy a krok 4 ukazuje, jak programově rozhraní s těmito vlastnostmi a metodami ze stránky obsahu.

> [!NOTE]
> Tento kurz se netýká konkrétních údajů o práci s daty v ASP.NET. Postup pro nastavení stránky předlohy pro zobrazení dat a stránku obsahu pro vkládání dat je hotový, ale Breezy. Podrobnější pohled na zobrazování a vkládání dat a použití ovládacích prvků SqlDataSource a GridView najdete v části zdroje informací v části Další informace na konci tohoto kurzu.

## <a name="step-1-displaying-the-five-most-recently-added-products-in-the-master-page"></a>Krok 1: zobrazení pěti naposledy přidaných produktů na stránce předlohy

Otevřete stránku předlohy `Site.master` a přidejte popisek a ovládací prvek GridView do `leftContent` `<div>`. Vymažte vlastnost `Text` popisku, nastavte její vlastnost `EnableViewState` na false a vlastnost `ID` na `GridMessage`; Nastavte vlastnost `ID` prvku GridView na hodnotu `RecentProducts`. Dále v Návrháři rozbalte inteligentní značku GridView a vyberte, aby se naváže k novému zdroji dat. Spustí se Průvodce konfigurací zdroje dat. Vzhledem k tomu, že databáze Northwind ve složce `App_Data` je databáze Microsoft SQL Server, zvolte možnost vytvořit SqlDataSource výběrem (viz obrázek 1); Pojmenujte `RecentProductsDataSource`SqlDataSource.

[![vazby prvku GridView k ovládacímu prvku SqlDataSource s názvem RecentProductsDataSource](interacting-with-the-master-page-from-the-content-page-cs/_static/image2.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image1.png)

**Obrázek 01**: Svázání prvku GridView s ovládacím prvkem SqlDataSource s názvem `RecentProductsDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](interacting-with-the-master-page-from-the-content-page-cs/_static/image3.png))

V dalším kroku se požádáme o určení databáze, ke které se chcete připojit. V rozevíracím seznamu vyberte soubor databáze `NORTHWIND.MDF` a klikněte na další. Vzhledem k tomu, že se jedná o první použití této databáze, průvodce nabídne uložení připojovacího řetězce v `Web.config`. Je potřeba, aby byl připojovací řetězec uložený pomocí názvu `NorthwindConnectionString`.

[![připojení k databázi Northwind](interacting-with-the-master-page-from-the-content-page-cs/_static/image5.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image4.png)

**Obrázek 02**: připojení k databázi Northwind ([kliknutím zobrazíte obrázek v plné velikosti](interacting-with-the-master-page-from-the-content-page-cs/_static/image6.png))

Průvodce konfigurací zdroje dat poskytuje dva způsoby, kterými můžeme zadat dotaz použitý k načtení dat:

- Zadáním vlastního příkazu SQL nebo uložené procedury nebo
- Vyzvednutím tabulky nebo zobrazení a zadáním sloupců, které se mají vrátit

Vzhledem k tomu, že chceme vracet jenom pět naposledy přidaných produktů, musíme zadat vlastní příkaz SQL. Použijte následující dotaz SELECT:

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample1.sql)]

Klíčové slovo `TOP 5` vrátí pouze prvních pět záznamů z dotazu. Primární klíč `Products` tabulky `ProductID`je `IDENTITY` sloupec, který nám zaručuje, že každý nový produkt přidaný do tabulky bude mít větší hodnotu než předchozí položka. Proto řazení výsledků podle `ProductID` v sestupném pořadí vrátí produkty počínaje naposledy vytvořenými.

[![vrátí pět naposledy přidaných produktů.](interacting-with-the-master-page-from-the-content-page-cs/_static/image8.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image7.png)

**Obrázek 03**: vrátí pět naposledy přidaných produktů ([kliknutím zobrazíte obrázek v plné velikosti](interacting-with-the-master-page-from-the-content-page-cs/_static/image9.png)).

Po dokončení Průvodce aplikace Visual Studio vygeneruje dvě BoundFields pro prvek GridView pro zobrazení `ProductName` a `UnitPrice` polí vrácených z databáze. V tuto chvíli by deklarativní označení stránky předlohy mělo zahrnovat označení podobné následujícímu:

[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample2.aspx)]

Jak vidíte, značka obsahuje: ovládací prvek web popisku (`GridMessage`); Prvek GridView `RecentProducts`se dvěma BoundFieldsmi; a ovládací prvek SqlDataSource, který vrátí pět naposledy přidaných produktů.

Pomocí tohoto prvku GridView vytvořeného s nakonfigurovaným ovládacím prvkem SqlDataSource navštivte web prostřednictvím prohlížeče. Jak ukazuje obrázek 4, v levém dolním rohu se zobrazí mřížka se seznamem pěti naposledy přidaných produktů.

[![zobrazí prvek GridView pět naposledy přidaných produktů.](interacting-with-the-master-page-from-the-content-page-cs/_static/image11.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image10.png)

**Obrázek 04**: v prvku GridView se zobrazí pět naposledy přidaných produktů ([kliknutím zobrazíte obrázek v plné velikosti).](interacting-with-the-master-page-from-the-content-page-cs/_static/image12.png)

> [!NOTE]
> Klidně můžete vyčistit vzhled prvku GridView. Mezi návrhy patří formátování zobrazené `UnitPrice` hodnoty jako měny a použití barev a písem pozadí ke zlepšení vzhledu mřížky.

## <a name="step-2-creating-a-content-page-to-add-new-products"></a>Krok 2: Vytvoření stránky obsahu pro přidání nových produktů

Naším dalším úkolem je vytvořit stránku obsahu, ze které může uživatel přidat nový produkt do tabulky `Products`. Přidejte novou stránku obsahu do složky `Admin` s názvem `AddProduct.aspx`a ujistěte se, že ji svážete se stránkou předlohy `Site.master`. Obrázek 5 ukazuje Průzkumník řešení po přidání této stránky na web.

[![přidat novou stránku ASP.NET do složky pro správu](interacting-with-the-master-page-from-the-content-page-cs/_static/image14.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image13.png)

**Obrázek 05**: Přidání nové stránky ASP.NET do složky `Admin` ([kliknutím zobrazíte obrázek v plné velikosti](interacting-with-the-master-page-from-the-content-page-cs/_static/image15.png))

Nahlaste se v kurzu [*zadání nadpisu, meta značek a dalších záhlaví HTML v kurzu hlavní stránky*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) jsme vytvořili vlastní třídu základní stránky s názvem `BasePage`, která vygenerovala název stránky, pokud nebyla explicitně nastavena. Přejít na třídu kódu na pozadí `AddProduct.aspx` stránky a nechat ji odvozovat z `BasePage` (místo z `System.Web.UI.Page`).

Nakonec aktualizujte soubor `Web.sitemap` tak, aby obsahoval položku pro tuto lekci. Přidejte následující kód pod `<siteMapNode>` v lekci pro pojmenování ID ovládacího prvku lekce:

[!code-xml[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample3.xml)]

Jak je znázorněno na obrázku 6, přidání tohoto `<siteMapNode>` elementu se projeví v seznamu lekcí.

Vraťte se na `AddProduct.aspx`. V ovládacím prvku Content for `MainContent` ContentPlaceHolder přidejte ovládací prvek DetailsView a pojmenujte ho `NewProduct`. Připojte prvek DetailsView k novému ovládacímu prvku SqlDataSource s názvem `NewProductDataSource`. Podobně jako u SqlDataSource v kroku 1 nakonfigurujte Průvodce tak, aby používal databázi Northwind a zvolili možnost zadat vlastní příkaz SQL. Vzhledem k tomu, že ovládací prvek DetailsView bude použit k přidání položek do databáze, musíme zadat jak příkaz `SELECT`, tak příkaz `INSERT`. Použijte následující `SELECT` dotaz:

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample4.sql)]

Pak na kartě Vložení přidejte následující příkaz `INSERT`:

[!code-sql[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample5.sql)]

Po dokončení průvodce přejít na inteligentní značku ovládacího prvku DetailsView a zaškrtněte políčko Povolit vkládání. Tím přidáte CommandField do prvku DetailsView s vlastností `ShowInsertButton` nastavenou na hodnotu true. Vzhledem k tomu, že tento prvek DetailsView bude použit výhradně pro vkládání dat, nastavte vlastnost `DefaultMode` ovládacího prvku DetailsView na hodnotu `Insert`.

A je to! Pojďme tuto stránku otestovat. Navštivte `AddProduct.aspx` v prohlížeči, zadejte název a cenu (viz obrázek 6).

[![přidat do databáze nový produkt](interacting-with-the-master-page-from-the-content-page-cs/_static/image17.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image16.png)

**Obrázek 6**: Přidání nového produktu do databáze ([kliknutím zobrazíte obrázek v plné velikosti](interacting-with-the-master-page-from-the-content-page-cs/_static/image18.png))

Po zadání názvu a ceny nového produktu klikněte na tlačítko Vložit. Způsobí to, že formulář bude převolán. Při zpětném volání je proveden příkaz `INSERT` ovládacího prvku SqlDataSource; jeho dva parametry jsou naplněny hodnotami zadanými uživatelem do dvou ovládacích prvků TextBox ovládacího prvku DetailsView. Bohužel není k dispozici žádná vizuální zpětná vazba, na kterou došlo k vložení. Je vhodné, aby se zobrazila zpráva s potvrzením, že byl přidán nový záznam. Tuto funkci mám jako cvičení pro čtenáře. Po přidání nového záznamu z prvku DetailsView se navíc v prvku GridView na stránce předlohy stále zobrazuje stejný počet pěti záznamů jako předtím; nezahrnuje právě přidaný záznam. Podíváme se, jak tento problém vyřešit v nadcházejících krocích.

> [!NOTE]
> Kromě přidání nějaké formy vizuální zpětné vazby, že vložení bylo úspěšné, doporučujeme také aktualizovat rozhraní pro vložení ovládacího prvku DetailsView, aby zahrnovalo ověřování. V současné době neexistuje žádné ověření. Pokud uživatel zadá v poli `UnitPrice` neplatnou hodnotu, například "moc nákladný", bude při zpětném volání vyvolána výjimka, když se systém pokusí tento řetězec převést na desetinné číslo. Další informace o přizpůsobení rozhraní pro vložení najdete v [kurzu *přizpůsobení rozhraní pro úpravu dat* ](../../data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) ze stránky [práce s datovou řadou kurzů](../../data-access/index.md).

## <a name="step-3-creating-public-properties-and-methods-in-the-master-page"></a>Krok 3: vytvoření veřejných vlastností a metod na stránce předlohy

V kroku 1 jsme přidali webové ovládací prvky popisek s názvem `GridMessage` nad prvek GridView na stránce předlohy. Tato jmenovka slouží k volitelnému zobrazení zprávy. Například po přidání nového záznamu do tabulky `Products` můžeme zobrazit zprávu, že se do databáze přidala zpráva "*ProductName* ". Místo pevného kódu textu pro tento popisek na stránce předlohy můžeme chtít, aby byla zpráva přizpůsobitelná na stránce obsahu.

Vzhledem k tomu, že ovládací prvek popisek je implementován jako chráněná členská proměnná v rámci hlavní stránky, nelze k němu získat přímý pøístup ze stránek obsahu. Aby bylo možné pracovat s popiskem na stránce předlohy na stránce obsahu (nebo v takovém případě libovolný webový ovládací prvek na stránce předlohy), musíme vytvořit veřejnou vlastnost na stránce předlohy, která zveřejňuje webový ovládací prvek nebo slouží jako proxy, pomocí kterého může být jedna z jeho vlastností.  souborům. Přidejte následující syntax do třídy kódu na pozadí hlavní stránky a zpřístupněte vlastnost `Text` popisku:

[!code-csharp[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample6.cs)]

Při přidání nového záznamu do tabulky `Products` ze stránky obsahu musí `RecentProducts` GridView na stránce předlohy znovu navazovat vazby na svůj podkladový zdroj dat. Chcete-li znovu navazovat vazby ovládacího prvku GridView, volejte metodu `DataBind`. Vzhledem k tomu, že prvek GridView na stránce předlohy není programově přístupný pro stránky obsahu, musíme na stránce předlohy vytvořit veřejnou metodu, která při volání znovu naváže data na prvek GridView. Přidejte následující metodu do třídy kódu na pozadí hlavní stránky:

[!code-csharp[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample7.cs)]

Pomocí vlastnosti `GridMessageText` a metody `RefreshRecentProductsGrid` na místě může kterákoli stránka obsahu programově nastavit nebo přečíst hodnotu vlastnosti `Text` popisku `GridMessage` nebo převážete data na `RecentProducts` GridView. Krok 4 kontroluje, jak přistupovat k veřejným vlastnostem a metodám hlavní stránky ze stránky obsahu.

> [!NOTE]
> Nezapomeňte označit vlastnosti a metody hlavní stránky jako `public`. Pokud tyto vlastnosti a metody výslovně nepovažujete za `public`, nebudou dostupné ze stránky obsahu.

## <a name="step-4-calling-the-master-pages-public-members-from-a-content-page"></a>Krok 4: volání veřejných členů stránky předlohy ze stránky obsahu

Teď, když má hlavní stránka potřebné veřejné vlastnosti a metody, jsme připraveni tyto vlastnosti a metody vyvolat ze stránky `AddProduct.aspx` obsahu. Konkrétně je potřeba nastavit vlastnost `GridMessageText` hlavní stránky a volat metodu `RefreshRecentProductsGrid` po přidání nového produktu do databáze. Všechny webové ovládací prvky ASP.NET data vybírají události hned před a po dokončení různých úloh, což usnadňuje vývojářům stránky provést některé programové akce před nebo po úkolu. Například když koncový uživatel klikne na tlačítko pro vložení ovládacího prvku DetailsView, vyvolá se při postbacku událost `ItemInserting` před začátkem vkládání pracovního postupu. Pak vloží záznam do databáze. Po tom ovládací prvek DetailsView vyvolá událost `ItemInserted`. Proto aby bylo možné pracovat se stránkou předlohy po přidání nového produktu, vytvořte obslužnou rutinu události pro událost `ItemInserted` ovládacího prvku DetailsView.

Existují dva způsoby, jak může stránka obsahu programově přizpůsobovat pomocí své hlavní stránky:

- Pomocí vlastnosti `Page.Master`, která vrátí odkaz na stránku předlohy, který bude mít volný typ, nebo
- Zadejte typ stránky předlohy nebo cestu k souboru pomocí direktivy `@MasterType`. Tím se automaticky přidá vlastnost silného typu na stránku s názvem `Master`.

Pojďme se podívat na oba přístupy.

### <a name="using-the-loosely-typedpagemasterproperty"></a>Použití vlastnosti`Page.Master`volného typu

Všechny webové stránky ASP.NET musí být odvozeny od třídy `Page`, která je umístěna v oboru názvů `System.Web.UI`. Třída `Page` obsahuje [vlastnost`Master`](https://msdn.microsoft.com/library/system.web.ui.page.master.aspx) , která vrací odkaz na stránku předlohy stránky. Pokud stránka nemá stránku předlohy `Master` vrátí `null`.

Vlastnost `Master` vrací objekt typu [`MasterPage`](https://msdn.microsoft.com/library/system.web.ui.masterpage.aspx) (také umístěný v `System.Web.UI`m oboru názvů), což je základní typ, ze kterého jsou odvozeny všechny stránky předlohy. Proto je nutné použít veřejné vlastnosti nebo metody definované na stránce předlohy našeho webu, je třeba přetypovat objekt `MasterPage` vrácený z vlastnosti `Master` na příslušný typ. Vzhledem k tomu, že jsme jmenovali náš soubor hlavní stránky `Site.master`, třída kódu na pozadí byla pojmenována `Site`. Proto následující kód přetypování vlastnost `Page.Master` do instance třídy site.

[!code-csharp[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample8.cs)]

Teď, když jsme převedli `Page.Master` vlastnost s volným typem na `Site` typ, můžeme odkazovat na vlastnosti a metody specifické pro web. Jak ukazuje obrázek 7, `GridMessageText` veřejné vlastnosti se zobrazí v rozevíracím seznamu technologie IntelliSense.

[![IntelliSense zobrazuje naše veřejné vlastnosti a metody hlavní stránky.](interacting-with-the-master-page-from-the-content-page-cs/_static/image20.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image19.png)

**Obrázek 07**: IntelliSense zobrazuje naše veřejné vlastnosti a metody hlavní stránky ([kliknutím zobrazíte obrázek v plné velikosti).](interacting-with-the-master-page-from-the-content-page-cs/_static/image21.png)

> [!NOTE]
> Pokud jste najmenovali soubor hlavní stránky `MasterPage.master` pak je název třídy kódu na pozadí hlavní stránky `MasterPage`. To může vést k dvojznačnému kódu při přetypování z typu `System.Web.UI.MasterPage` do vaší `MasterPage` třídy. V krátkém případě je nutné plně kvalifikovat typ, na který předáváte, což může být trochu obtížné při použití modelu projektu webu. Můj návrh by buď měl být při vytváření hlavní stránky pojmenován na jinou hodnotu než `MasterPage.master` nebo ještě lepší, a to tak, že se na stránku předlohy vytvoří odkaz silně typovaného typu.

### <a name="creating-a-strongly-typed-reference-with-themastertypedirective"></a>Vytvoření odkazu silného typu pomocí direktivy`@MasterType`

Pokud se vám podíváte na pečlivě, vidíte, že třída kódu na pozadí stránky ASP.NET je částečná třída (Všimněte si klíčového slova `partial` v definici třídy). Částečné třídy byly představeny C# v a Visual Basic with.NET Framework 2,0 a v kostce umožňují definovat členy třídy v rámci více souborů. Soubor třídy kódu na pozadí – `AddProduct.aspx.cs`například obsahuje kód, který my, vývojář stránky vytvoří. Kromě našeho kódu modul ASP.NET automaticky vytvoří samostatný soubor třídy s vlastnostmi a obslužnými rutinami událostí v, který přeloží deklarativní označení do hierarchie tříd stránky.

Automatické generování kódu, ke kterému dochází pokaždé, když je navštívená stránka ASP.NET PAVES způsobem pro některé místo zajímavé a užitečné možnosti. Pokud v případě stránek předlohy říkáme modulu ASP.NET, kterou hlavní stránku používá naše stránka obsahu, vygeneruje pro nás vlastnost silně typovaného `Master`.

Pomocí [direktivy`@MasterType`](https://msdn.microsoft.com/library/ms228274.aspx) informujte modul ASP.NET typu stránky předlohy stránky obsahu. Direktiva `@MasterType` může přijmout buď název typu stránky předlohy, nebo její cestu k souboru. Chcete-li určit, že stránka `AddProduct.aspx` používá `Site.master` jako svou hlavní stránku, přidejte do horní části `AddProduct.aspx`následující direktivu:

[!code-aspx[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample9.aspx)]

Tato direktiva instruuje modul ASP.NET, aby do hlavní stránky přidal odkaz silného typu pomocí vlastnosti s názvem `Master`. Při použití direktivy `@MasterType` můžeme volat veřejné vlastnosti a metody `Site.master` hlavní stránky a přímo prostřednictvím vlastnosti `Master` bez přetypování.

> [!NOTE]
> Vynecháte-li direktivu `@MasterType`, `Page.Master` syntaxe a `Master` vrátí stejnou věc: objekt na stránce předlohy stránky s volným typem. Pokud zadáte direktivu `@MasterType`, `Master` vrátí odkaz silně typované na určenou stránku předlohy. `Page.Master`však stále vrací odkaz na volně typovaného typu. Podrobnější přehled o tom, proč se jedná o tento případ a jak je vlastnost `Master` vytvořená, když je zahrnutá direktiva `@MasterType`, najdete v tématu K`@MasterType` záznamu na blogu [Scott Allen](http://odetocode.com/blogs/scott/default.aspx) [v ASP.NET 2,0](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx).

### <a name="updating-the-master-page-after-adding-a-new-product"></a>Aktualizace stránky předlohy po přidání nového produktu

Teď, když víme, jak volat veřejné vlastnosti a metody hlavní stránky ze stránky obsahu, jsme připraveni aktualizovat stránku `AddProduct.aspx` tak, aby se stránka předlohy aktualizovala po přidání nového produktu. Na začátku kroku 4 jsme vytvořili obslužnou rutinu události pro událost `ItemInserting` ovládacího prvku DetailsView, která se spustí hned po přidání nového produktu do databáze. Do této obslužné rutiny události přidejte následující kód:

[!code-csharp[Main](interacting-with-the-master-page-from-the-content-page-cs/samples/sample10.cs)]

Výše uvedený kód používá jak volně typované `Page.Master` vlastnost, tak vlastnost `Master` silného typu. Všimněte si, že vlastnost `GridMessageText` je nastavena na hodnotu*NázevVýrobku* přidáno do mřížky... Hodnoty právě přidávaného produktu jsou přístupné prostřednictvím kolekce `e.Values`; Jak vidíte, přidaná hodnota `ProductName` je k dispozici prostřednictvím `e.Values["ProductName"]`.

Obrázek 8 ukazuje stránku `AddProduct.aspx` hned po přidání nového produktu – Scott – soda – přidáno do databáze. Všimněte si, že název právě přidávaného produktu je zaznamenán v popisku hlavní stránky a že prvek GridView byl aktualizován tak, aby zahrnoval produkt a jeho cenu.

[![popisku hlavní stránky a prvku GridView zobrazit právě přidaný produkt](interacting-with-the-master-page-from-the-content-page-cs/_static/image23.png)](interacting-with-the-master-page-from-the-content-page-cs/_static/image22.png)

**Obrázek 08**: popisek a GridView stránky předlohy zobrazují právě přidaný produkt ([kliknutím zobrazíte obrázek v plné velikosti](interacting-with-the-master-page-from-the-content-page-cs/_static/image24.png))

## <a name="summary"></a>Přehled

V ideálním případě jsou hlavní stránka a její stránky obsahu zcela oddělené od sebe a nevyžadují žádnou úroveň interakce. Zatímco stránky a stránky předlohy by měly být navržené s tímto cílem, existuje řada běžných scénářů, ve kterých se stránka obsahu musí nacházet se stránkou předlohy. Jedním z nejběžnějších důvodů je aktualizovat určitou část zobrazení stránky předlohy na základě některé akce, která se zobrazila na stránce obsahu.

Dobrá zpráva je, že je relativně jasné, že stránku obsahu programově komunikují s hlavní stránkou. Začněte tím, že na stránce předlohy vytvoříte veřejné vlastnosti nebo metody, které zapouzdřují funkce, které je potřeba vyvolat na stránce obsahu. Pak na stránce obsahu přejděte k vlastnostem a metodám hlavní stránky prostřednictvím `Page.Master`elné vlastnosti s volným typem nebo použijte direktivu `@MasterType` k vytvoření odkazu silného typu na stránku předlohy.

V dalším kurzu zjistíte, jak má stránka předlohy programově pracovat s jednou z jeho stránek obsahu.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Přístup k datům v ASP.NET a jejich aktualizace](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [Stránky předlohy ASP.NET: tipy, triky a depeše](http://www.odetocode.com/articles/450.aspx)
- [`@MasterType` v ASP.NET 2,0](http://odetocode.com/Blogs/scott/archive/2005/07/16/1944.aspx)
- [Předávání informací mezi obsahem a stránkami předlohy](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [Práce s daty v kurzech ASP.NET](../../data-access/index.md)

### <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 3,5 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco). Scott se dá kontaktovat [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor potenciálních zákazníků pro tento kurz byl Zack Novotný. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](control-id-naming-in-content-pages-cs.md)
> [Další](interacting-with-the-content-page-from-the-master-page-cs.md)

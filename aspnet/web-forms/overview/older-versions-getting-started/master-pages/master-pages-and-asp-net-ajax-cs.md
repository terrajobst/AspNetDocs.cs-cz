---
uid: web-forms/overview/older-versions-getting-started/master-pages/master-pages-and-asp-net-ajax-cs
title: Stránky předlohy a ASP.NET AJAX (C#) | Microsoft Docs
author: rick-anderson
description: Popisuje možnosti pro použití ASP.NET AJAX a stránek předlohy. Podívá se na použití třídy ScriptManagerProxy; Popisuje, jak jsou načteny různé soubory JS v závislosti na...
ms.author: riande
ms.date: 07/11/2008
ms.assetid: 0c55eb66-ba44-4d49-98e8-5c87fd9b1111
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/master-pages-and-asp-net-ajax-cs
msc.type: authoredcontent
ms.openlocfilehash: 8cd1d57b4d2aa01654da53ab2b1cc01f71ad8a87
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74639863"
---
# <a name="master-pages-and-aspnet-ajax-c"></a>Stránky předlohy a ASP.NET AJAX (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_08_CS.zip) nebo [stažení PDF](https://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_08_CS.pdf)

> Popisuje možnosti pro použití ASP.NET AJAX a stránek předlohy. Podívá se na použití třídy ScriptManagerProxy; Popisuje, jak jsou načteny různé soubory JS v závislosti na tom, zda je ovládací uzel ScriptManager použit na stránce předlohy nebo na stránce obsahu.

## <a name="introduction"></a>Úvod

V posledních několika letech více a více vývojářů sestavuje webové aplikace s podporou [AJAX](http://en.wikipedia.org/wiki/Ajax_(programming)). Web s podporou jazyka AJAX používá řadu souvisejících webových technologií, které nabízí větší možnosti reakce uživatelů. Vytváření aplikací ASP.NET podporujících technologii AJAX je úžasné díky [architektuře AJAX](../../../../ajax/index.md)společnosti Microsoft pro ASP.NET. ASP.NET AJAX je integrováno do ASP.NET 3,5 a Visual Studio 2008; je k dispozici také jako samostatné stažení pro aplikace ASP.NET 2,0.

Při sestavování webových stránek s podporou jazyka AJAX s rozhraním ASP.NET AJAX je nutné přidat přesně jeden [ovládací prvek ScriptManager](https://msdn.microsoft.com/library/bb398863.aspx) do každé a všechny stránky, které používají rozhraní. Jak název naznačuje, ovládací prvku ScriptManager spravuje skript na straně klienta, který se používá na webových stránkách s podporou AJAX. Přinejmenším ovládací objekt ScriptManager vygeneruje kód HTML, který instruuje prohlížeč, aby stahoval soubory JavaScriptu, které strukturu klientskou knihovnu ASP.NET AJAX. Dá se použít i k registraci vlastních souborů JavaScriptu, webových služeb s povoleným skriptem a vlastních funkcí aplikační služby.

Pokud vaše lokalita používá stránky předlohy (tak, jak by měla), nemusíte nutně přidávat ovládací prvek ScriptManager na všechny stránky s jedním obsahem. místo toho můžete do stránky předlohy přidat ovládací prvek ScriptManager. V tomto kurzu se dozvíte, jak přidat ovládací prvek ScriptManager do hlavní stránky. Také se podíváme na to, jak pomocí ovládacího prvku ScriptManagerProxy zaregistrovat vlastní skripty a skriptovací služby na konkrétní stránku obsahu.

> [!NOTE]
> V tomto kurzu se nezabývá návrhem a vytvářením webových aplikací s podporou jazyka AJAX s rozhraním ASP.NET AJAX. Další informace o používání AJAX najdete v [výukových programech a kurzech](../aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax.md) [ASP.NET AJAX](../../../videos/aspnet-ajax/index.md) a také na těchto prostředcích uvedených v části Další informace na konci tohoto kurzu.

## <a name="examining-the-markup-emitted-by-the-scriptmanager-control"></a>Kontrola značek vygenerovaných ovládacím prvkem ScriptManager

Ovládací prvek ScriptManager vygeneruje kód, který instruuje prohlížeč ke stažení souborů JavaScriptu, které strukturu klientskou knihovnu ASP.NET AJAX. Přidá také bitovou kopii vloženého JavaScriptu na stránku, která inicializuje tuto knihovnu. Následující kód ukazuje obsah, který je přidán do vykresleného výstupu stránky, který obsahuje ovládací prvek ScriptManager:

[!code-html[Main](master-pages-and-asp-net-ajax-cs/samples/sample1.html)]

Značky `<script src="url"></script>` přidávají prohlížeči pokyn ke stažení a spuštění souboru JavaScriptu na *adrese URL*. Ovládací prvku ScriptManager generuje tři takové značky; jeden odkazuje na soubor `WebResource.axd`, zatímco druhý dva odkazují na soubor `ScriptResource.axd`. Tyto soubory ve skutečnosti neexistují jako soubory na webu. Místo toho, když požadavek na jeden z těchto souborů dorazí na webový server, stroj ASP.NET prověřuje dotaz QueryString a vrátí příslušný obsah JavaScriptu. Skript, který poskytuje tyto tři externí soubory JavaScriptu, tvoří klientskou knihovnu ASP.NET AJAX Framework. Ostatní značky `<script>` generované nástrojem ScriptManager zahrnují vložený skript, který inicializuje tuto knihovnu.

Odkazy na externí skripty a vložený skript vysílané ovládacím prvku ScriptManager jsou nezbytné pro stránku, která používá ASP.NET AJAX Framework, ale není potřebná pro stránky, které rozhraní nepoužívají. Proto je možné, že je ideální pro přidání prvku ScriptManager pouze do těch stránek, které používají architekturu ASP.NET AJAX. A to je dostatečné, ale pokud máte mnoho stránek, které používají rozhraní, skončíte tím, že přidáváte ovládací prvek ScriptManager na všechny stránky – opakující se úkol, aby bylo co nejméně. Alternativně můžete přidat ScriptManager na stránku předlohy, která pak vloží tento nezbytný skript do všech stránek obsahu. Pomocí tohoto přístupu není nutné pamatovat na přidání prvku ScriptManager na novou stránku, která používá rozhraní ASP.NET AJAX Framework, protože je již zahrnuta v rámci hlavní stránky. Krok 1 vás provede přidáním ovládacího prvku ScriptManager na stránku předlohy.

> [!NOTE]
> Pokud plánujete zahrnutí funkcí AJAX v uživatelském rozhraní stránky předlohy, pak v takovém případě nemusíte nic volit – musíte do stránky předlohy přidat ScriptManager.

Jedním z Nevýhodou přidávání ovládacího prvku ScriptManager na stránku předlohy je, že výše uvedený skript je vygenerován na *každé* stránce bez ohledu na to, zda je to potřeba. To jasně vede k plýtvání šířky pásma pro tyto stránky, které mají k dispozici ScriptManager (přes hlavní stránku), zatím nepoužívají žádné funkce ASP.NET AJAX Framework. Ale jenom kolik šířky pásma je plýtvání?

- Skutečný obsah vysílaný ovládacím prvku ScriptManager (zobrazený výše) sčítá za pár přes 1 KB.
- Tři externí soubory skriptu, na které odkazuje element `<script>`, se ale skládají přibližně z nekomprimovaných 450KB dat; na webu, který používá kompresi gzip, se tato celková šířka pásma dá snížit v blízkosti 100 kB. Avšak tyto soubory skriptu jsou ukládány do mezipaměti v prohlížeči po dobu jednoho roku, což znamená, že je třeba je stáhnout pouze jednou a pak je lze znovu použít na jiných stránkách na webu.

V případě, že se soubory skriptu ukládají do mezipaměti, je nejlepší cena 1 KB, což je zanedbatelná hodnota. V nejhorším případě však v případě, že se soubory skriptu ještě nestáhly a webový server nepoužívá žádnou formu komprese, je dosaženo šířky pásma 450KB, která se dá přidat kamkoli od druhého nebo dvou přes širokopásmové připojení až po minutu.  Uživatelé přes vytáčené modemy. Dobrá zpráva je, že vzhledem k tomu, že prohlížeč ukládá soubory externích skriptů do mezipaměti, dochází k tomuto nejhoršímu scénáři zřídka.

> [!NOTE]
> Pokud stále Uncomfortable umístit ovládací prvek ScriptManager do hlavní stránky, zvažte webový formulář (`<form runat="server">` značky na stránce Master). Každá stránka ASP.NET, která používá model zpětného volání, musí obsahovat přesně jeden webový formulář. Přidání webového formuláře přidá další obsah: Počet skrytých polí formuláře, značku `<form>` sám sebe a v případě potřeby i JavaScriptová funkce pro inicializaci zpětného volání ze skriptu. Tento kód není potřebný pro stránky, které se neprovádí zpětná volání. Tento nadbytečný kód se může eliminovat odebráním webového formuláře ze stránky předlohy a jeho ručním přidáním na každou stránku obsahu, která ho potřebuje. Nicméně výhody, které mají webový formulář na hlavní stránce, převáží nevýhody od toho, aby se nemusely přidat zbytečně k určitým stránkám obsahu.

## <a name="step-1-adding-a-scriptmanager-control-to-the-master-page"></a>Krok 1: Přidání ovládacího prvku ScriptManager na stránku předlohy

Každá webová stránka, která používá rozhraní ASP.NET AJAX, musí obsahovat přesně jeden ovládací prvek ScriptManager. Z důvodu tohoto požadavku má obvykle smysl umístit jeden ovládací prvek ScriptManager na hlavní stránku, aby všechny stránky obsahu měly automaticky zahrnut ovládací prvek ScriptManager. Kromě toho musí být objekt ScriptManager uveden před jakýmkoli ovládacím prvkem serveru ASP.NET AJAX, jako jsou ovládací prvky UpdatePanel a UpdateProgress. Proto je vhodné umístit ScriptManager před jakékoli ovládací prvky ContentPlaceHolder v rámci webového formuláře.

Otevřete stránku předlohy `Site.master` a přidejte ovládací prvek ScriptManager na stránku webové formuláře, ale před `<div id="topContent">` prvek (viz obrázek 1). Pokud používáte aplikaci Visual Web Developer 2008 nebo Visual Studio 2008, ovládací prvek ScriptManager se nachází v sadě nástrojů na kartě Rozšíření AJAX. Pokud používáte sadu Visual Studio 2005, bude nejprve nutné nainstalovat rozhraní ASP.NET AJAX a přidat ovládací prvky do sady nástrojů. Navštivte web [ASP.NET AJAX wiki](https://github.com/DevExpress/AjaxControlToolkit/wiki) a získejte rozhraní pro ASP.NET 2,0.

Po přidání prvku ScriptManager na stránku změňte jeho `ID` z `ScriptManager1` na `MyManager`.

[![přidat ScriptManager do stránky předlohy](master-pages-and-asp-net-ajax-cs/_static/image2.png)](master-pages-and-asp-net-ajax-cs/_static/image1.png)

**Obrázek 01**: přidejte ScriptManager do stránky předlohy ([kliknutím zobrazíte obrázek v plné velikosti](master-pages-and-asp-net-ajax-cs/_static/image3.png)).

## <a name="step-2-using-the-aspnet-ajax-framework-from-a-content-page"></a>Krok 2: použití architektury ASP.NET AJAX ze stránky obsahu

Pomocí ovládacího prvku ScriptManager přidaného na stránku předlohy teď můžeme do jakékoli stránky obsahu přidat funkci ASP.NET AJAX Framework. Pojďme vytvořit novou stránku ASP.NET, která zobrazí náhodně vybraný produkt z databáze Northwind. K aktualizaci tohoto zobrazení každých 15 sekund použijeme ovládací prvek časovače ASP.NET AJAX, který zobrazuje nový produkt.

Začněte vytvořením nové stránky v kořenovém adresáři s názvem `ShowRandomProduct.aspx`. Nezapomeňte tuto novou stránku navazovat na `Site.master` hlavní stránku.

[![přidání nové stránky ASP.NET na web](master-pages-and-asp-net-ajax-cs/_static/image5.png)](master-pages-and-asp-net-ajax-cs/_static/image4.png)

**Obrázek 02**: Přidání nové stránky ASP.NET na web ([kliknutím zobrazíte obrázek v plné velikosti](master-pages-and-asp-net-ajax-cs/_static/image6.png))

Nahlaste se v kurzu [*zadání nadpisu, meta značek a dalších záhlaví HTML v kurzu hlavní stránky*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) jsme vytvořili vlastní třídu základní stránky s názvem `BasePage`, která vygenerovala název stránky, pokud nebyla explicitně nastavena. Přejít na třídu kódu na pozadí `ShowRandomProduct.aspx` stránky a nechat ji odvozovat z `BasePage` (místo z `System.Web.UI.Page`).

Nakonec aktualizujte soubor `Web.sitemap` tak, aby obsahoval položku pro tuto lekci. Následující kód přidejte pod `<siteMapNode>` v lekci interakce stránky předlohy s obsahem:

[!code-xml[Main](master-pages-and-asp-net-ajax-cs/samples/sample2.xml)]

Přidání tohoto `<siteMapNode>` elementu se projeví v seznamu lekcí (viz obrázek 5).

### <a name="displaying-a-randomly-selected-product"></a>Zobrazuje se náhodně vybraný produkt.

Vraťte se na `ShowRandomProduct.aspx`. Z návrháře přetáhněte ovládací prvek UpdatePanel ze sady nástrojů do ovládacího prvku `MainContent` obsahu a nastavte jeho vlastnost `ID` na `ProductPanel`. Prvek UpdatePanel představuje oblast na obrazovce, která může být asynchronně aktualizována prostřednictvím postbacku částečné stránky.

Naším prvním úkolem je zobrazit informace o náhodně vybraném produktu v rámci prvku UpdatePanel. Začněte přetažením ovládacího prvku DetailsView do prvku UpdatePanel. Nastavte vlastnost `ID` ovládacího prvku DetailsView na `ProductInfo` a vymažte jeho vlastnosti `Height` a `Width`. Rozbalte inteligentní značku ovládacího prvku DetailsView a v rozevíracím seznamu zvolit zdroj dat vyberte možnost svázání prvku DetailsView s novým ovládacím prvkem SqlDataSource s názvem `RandomProductDataSource`.

[![svázání prvku DetailsView s novým ovládacím prvkem SqlDataSource](master-pages-and-asp-net-ajax-cs/_static/image8.png)](master-pages-and-asp-net-ajax-cs/_static/image7.png)

**Obrázek 03**: Svázání ovládacího prvku DetailsView s novým ovládacím prvkem SqlDataSource ([kliknutím zobrazíte obrázek v plné velikosti](master-pages-and-asp-net-ajax-cs/_static/image9.png))

Nakonfigurujte ovládací prvek SqlDataSource pro připojení k databázi Northwind prostřednictvím `NorthwindConnectionString` (kterou jsme vytvořili v [*interakci se stránkou předlohy z kurzu stránky obsahu*](interacting-with-the-content-page-from-the-master-page-cs.md) ). Při konfiguraci příkazu SELECT zvolte možnost zadat vlastní příkaz SQL a poté zadejte následující dotaz:

[!code-sql[Main](master-pages-and-asp-net-ajax-cs/samples/sample3.sql)]

Klíčové slovo `TOP 1` v klauzuli `SELECT` vrátí pouze první záznam vrácený dotazem. [Funkce`NEWID()`](https://msdn.microsoft.com/library/ms190348.aspx) generuje novou [globálně jedinečnou hodnotu identifikátoru (GUID)](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) a lze ji použít v klauzuli `ORDER BY` pro vrácení záznamů tabulky v náhodném pořadí.

[![nakonfigurovat SqlDataSource pro vrácení jednoho náhodně vybraného záznamu](master-pages-and-asp-net-ajax-cs/_static/image11.png)](master-pages-and-asp-net-ajax-cs/_static/image10.png)

**Obrázek 04**: Konfigurace SqlDataSource pro vrácení jednoho náhodně vybraného záznamu ([kliknutím zobrazíte obrázek v plné velikosti](master-pages-and-asp-net-ajax-cs/_static/image12.png))

Po dokončení Průvodce vytvoří Visual Studio vlastnost BoundField pro dva sloupce vrácené výše uvedeným dotazem. V tomto okamžiku by deklarativní označení stránky mělo vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample4.aspx)]

Obrázek 5 zobrazuje stránku `ShowRandomProduct.aspx` při prohlížení v prohlížeči. Kliknutím na tlačítko obnovit v prohlížeči znovu načtěte stránku. měli byste vidět `ProductName` a `UnitPrice` hodnoty pro nový náhodně vybraný záznam.

[Zobrazí se ![název a cena náhodného produktu.](master-pages-and-asp-net-ajax-cs/_static/image14.png)](master-pages-and-asp-net-ajax-cs/_static/image13.png)

**Obrázek 05**: zobrazí se název a cena náhodného produktu ([kliknutím zobrazíte obrázek v plné velikosti](master-pages-and-asp-net-ajax-cs/_static/image15.png)).

### <a name="automatically-displaying-a-new-product-every-15-seconds"></a>Automatické zobrazení nového produktu každých 15 sekund

Rozhraní ASP.NET AJAX obsahuje ovládací prvek časovače, který v zadaném čase provádí zpětné odeslání. Při zpětném volání se vyvolá událost časovače `Tick`. Pokud je ovládací prvek časovače umístěn v rámci ovládacího prvku UpdatePanel, spouští částečné postback stránky, během kterého můžeme data znovu navazovat na prvek DetailsView a zobrazit tak nový náhodně vybraný produkt.

Chcete-li to provést, přetáhněte časovač ze sady nástrojů a umístěte jej do ovládacího prvku UpdatePanel. Změňte `ID` časovače z `Timer1` na `ProductTimer` a jeho vlastnost `Interval` z 60000 na 15000. Vlastnost `Interval` označuje počet milisekund mezi zpětnými odesláními; nastavení na 15000 způsobí, že časovač spustí částečné odeslání stránky každých 15 sekund. V tomto okamžiku by deklarativní označení časovače mělo vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample5.aspx)]

Vytvořte obslužnou rutinu události pro událost `Tick` časovače. V této obslužné rutině události potřebujeme znovu navazovat vazby na prvek DetailsView voláním metody `DataBind` ovládacího prvku DetailsView. Tím se instruuje ovládací prvek DetailsView, aby znovu obnovil data z ovládacího prvku zdroje dat, který vybere a zobrazí nový náhodně vybraný záznam (stejně jako při opětovném načítání stránky kliknutím na tlačítko obnovit v prohlížeči).

[!code-csharp[Main](master-pages-and-asp-net-ajax-cs/samples/sample6.cs)]

A je to! Znovu navštivte stránku v prohlížeči. Zpočátku se zobrazí informace o náhodném produktu. Pokud si tuto obrazovku sami provedete, všimnete si, že po 15 sekundách si informace o novém produktu připraví jenom v případě, že se stávající displej nahradí.

Chcete-li lépe zjistit, co se děje, přidejte do prvku UpdatePanel ovládací prvek popisek, který zobrazuje čas poslední aktualizace zobrazení. Přidejte ovládací prvek web popisku v ovládacím prvku UpdatePanel, nastavte jeho `ID` na `LastUpdateTime`a vymažte jeho vlastnost `Text`. Dále vytvořte obslužnou rutinu události pro událost `Load` ovládacího prvku UpdatePanel a zobrazte aktuální čas v popisku. (Událost `Load` ovládacího prvku UpdatePanel je aktivována při každém úplném nebo částečném postbacku stránky.)

[!code-csharp[Main](master-pages-and-asp-net-ajax-cs/samples/sample7.cs)]

Po dokončení této změny stránka obsahuje čas, kdy byl aktuálně zobrazený produkt načten. Obrázek 6: při prvním navštívení stránky se zobrazí stránka. Obrázek 7 zobrazuje stránku 15 sekund později, po jejichž uplynutí je ovládací prvek Timer "Ticked" a ovládací prvek UpdatePanel byl aktualizován, aby zobrazil informace o novém produktu.

[při načtení stránky se zobrazí náhodně vybraný produkt ![](master-pages-and-asp-net-ajax-cs/_static/image17.png)](master-pages-and-asp-net-ajax-cs/_static/image16.png)

**Obrázek 6**: při načítání stránky se zobrazí náhodně vybraný produkt ([kliknutím zobrazíte obrázek v plné velikosti](master-pages-and-asp-net-ajax-cs/_static/image18.png)).

[![každých 15 sekund se zobrazí nový náhodně vybraný produkt.](master-pages-and-asp-net-ajax-cs/_static/image20.png)](master-pages-and-asp-net-ajax-cs/_static/image19.png)

**Obrázek 7**: každých 15 sekund se zobrazí nový náhodně vybraný produkt ([kliknutím zobrazíte obrázek v plné velikosti](master-pages-and-asp-net-ajax-cs/_static/image21.png)).

## <a name="step-3-using-the-scriptmanagerproxy-control"></a>Krok 3: použití ovládacího prvku ScriptManagerProxy

Společně s tím, jak je nutný skript pro klientskou knihovnu ASP.NET AJAX Framework, může správce ScriptManager registrovat také vlastní soubory JavaScriptu, odkazy na webové služby s povoleným skriptem a vlastní ověřování, autorizaci a profilové služby. Tato přizpůsobení jsou obvykle specifická pro určitou stránku. Pokud se však v ovládacím prvku ScriptManager na stránce předlohy odkazuje na vlastní soubory skriptu, odkazy na webové služby nebo ověřování, autorizaci nebo profilové služby, budou tyto stránky zahrnuty na *všech* stránkách na webu.

Chcete-li přidat přizpůsobení související s prvkem ScriptManager na stránce, použijte ovládací prvek ScriptManagerProxy. Můžete přidat ScriptManagerProxy na stránku obsahu a pak zaregistrovat vlastní soubor JavaScriptu, odkaz na webovou službu nebo ověřování, autorizaci nebo profilovou službu z ScriptManagerProxy. to má vliv na registraci těchto služeb pro konkrétní stránku obsahu.

> [!NOTE]
> ASP.NET stránka může mít pouze jeden ovládací prvek ScriptManager. Proto nemůžete přidat ovládací prvek ScriptManager na stránku obsahu, pokud je ovládací prvek ScriptManager již definován na stránce předlohy. Jediným účelem ScriptManagerProxy je poskytnout vývojářům způsob, jak definovat ScriptManager na stránce předlohy, ale stále mají možnost přidat přizpůsobení prvku ScriptManager na stránce.

Chcete-li zobrazit ovládací prvek ScriptManagerProxy v akci, připraví prvek UpdatePanel v `ShowRandomProduct.aspx` tak, aby obsahovalo tlačítko, které používá skript na straně klienta pro pozastavení nebo obnovení ovládacího prvku časovač. Ovládací prvek Timer má tři metody na straně klienta, které můžeme použít k dosažení těchto požadovaných funkcí:

- `_startTimer()` – spustí řízení časovače.
- `_raiseTick()` – způsobí, že ovládací prvek časovače zaškrtne, a tak se zpátky a zvýší jeho událost `Tick` na serveru.
- `_stopTimer()` – zastaví řízení časovače.

Pojďme vytvořit soubor JavaScriptu s proměnnou s názvem `timerEnabled` a funkcí nazvanou `ToggleTimer`. Proměnná `timerEnabled` označuje, jestli je ovládací prvek časovače aktuálně povolený, nebo zakázaný. Výchozí hodnota je true. Funkce `ToggleTimer` přijímá dva vstupní parametry: odkaz na tlačítko pozastavit/pokračovat a hodnotu `id` na straně klienta ovládacího prvku Timer. Tato funkce přepíná hodnotu `timerEnabled`, získá odkaz na ovládací prvek Timer, spustí nebo zastaví časovač (v závislosti na hodnotě `timerEnabled`) a aktualizuje zobrazený text tlačítka na "pozastavit" nebo "pokračovat". Tato funkce bude volána vždy, když se klikne na tlačítko pozastavit/pokračovat.

Začněte vytvořením nové složky na webu s názvem `Scripts`. Dále přidejte nový soubor do složky Scripts s názvem `TimerScript.js` typu souboru JScript.

[![přidat nový soubor JavaScriptu do složky Scripts](master-pages-and-asp-net-ajax-cs/_static/image23.png)](master-pages-and-asp-net-ajax-cs/_static/image22.png)

**Obrázek 08**: Přidání nového souboru JavaScriptu do složky `Scripts` ([kliknutím zobrazíte obrázek v plné velikosti](master-pages-and-asp-net-ajax-cs/_static/image24.png))

[![se na web přidal nový soubor JavaScriptu.](master-pages-and-asp-net-ajax-cs/_static/image26.png)](master-pages-and-asp-net-ajax-cs/_static/image25.png)

**Obrázek 09**: do webu byl přidán nový soubor JavaScriptu ([kliknutím zobrazíte obrázek v plné velikosti](master-pages-and-asp-net-ajax-cs/_static/image27.png)).

Dále do souboru TimerScript. js přidejte následující skript:

[!code-csharp[Main](master-pages-and-asp-net-ajax-cs/samples/sample8.cs)]

Nyní je potřeba tento vlastní soubor JavaScriptu zaregistrovat v `ShowRandomProduct.aspx`. Vraťte se na `ShowRandomProduct.aspx` a přidejte na ni ovládací prvek ScriptManagerProxy; nastavte jeho `ID` na `MyManagerProxy`. Chcete-li zaregistrovat vlastní soubor JavaScriptu, vyberte v Návrháři ovládací prvek ScriptManagerProxy a pak pokračujte na okno Vlastnosti. Jedna z vlastností je "skripty". Výběrem této vlastnosti se zobrazí Editor kolekce ScriptReference zobrazený na obrázku 10. Kliknutím na tlačítko Přidat zahrňte nový odkaz na skript a potom zadejte cestu k souboru skriptu ve vlastnosti cesta: `~/Scripts/TimerScript.js`.

[![přidat odkaz na skript do ovládacího prvku ScriptManagerProxy](master-pages-and-asp-net-ajax-cs/_static/image29.png)](master-pages-and-asp-net-ajax-cs/_static/image28.png)

**Obrázek 10**: Přidání odkazu na skript do ovládacího prvku ScriptManagerProxy ([kliknutím zobrazíte obrázek v plné velikosti](master-pages-and-asp-net-ajax-cs/_static/image30.png))

Po přidání odkazu na skript se pro deklarativní označení ovládacího prvku ScriptManagerProxy aktualizuje tak, aby zahrnoval kolekci `<Scripts>` s jedinou položkou `ScriptReference`, jak ukazuje následující fragment kódu:

[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample9.aspx)]

Položka `ScriptReference` dává pokyn ScriptManagerProxy, aby zahrnoval odkaz na soubor JavaScriptu ve vykresleném kódu. To znamená, že když si vlastní skript zaregistrujete do ScriptManagerProxy vygenerovaného výstupu `ShowRandomProduct.aspx` stránky, bude teď zahrnovat další značku `<script src="url"></script>`: `<script src="Scripts/TimerScript.js" type="text/javascript"></script>`.

Nyní můžeme volat funkci `ToggleTimer` definovanou v `TimerScript.js` ze skriptu klienta na stránce `ShowRandomProduct.aspx`. Přidejte následující kód HTML v prvku UpdatePanel:

[!code-aspx[Main](master-pages-and-asp-net-ajax-cs/samples/sample10.aspx)]

Tím se zobrazí tlačítko s textem "pozastavit". Pokaždé, když se na něj klikne, volá se `ToggleTimer` funkce JavaScriptu, která předává odkaz na tlačítko a hodnotu ID ovládacího prvku Timer (`ProductTimer`). Poznamenejte si syntaxi pro získání `id` hodnoty ovládacího prvku Timer. `<%=ProductTimer.ClientID%>` emituje hodnotu vlastnosti `ClientID` ovládacího prvku `ProductTimer` Timer. V kurzu [*pojmenování ID ovládacích prvků v stránkách obsahu*](control-id-naming-in-content-pages-cs.md) jsme probrali rozdíly mezi hodnotou `ID` na straně serveru a výslednou `id`ou na straně klienta a způsobem, jak `ClientID` vrátí `id`na straně klienta.

Obrázek 11 ukazuje tuto stránku, když se poprvé navštíví přes prohlížeč. V tuto chvíli běží časovač a aktualizuje zobrazené informace o produktu každých 15 sekund. Obrázek 12 zobrazuje obrazovku po kliknutí na tlačítko pro pozastavení. Kliknutím na tlačítko pozastavit zastavíte časovač a aktualizujete text tlačítka na pokračovat. Jakmile uživatel klikne na tlačítko pokračovat, informace o produktu budou obnoveny (a budou pokračovat v aktualizaci každých 15 sekund).

[![kliknutím na tlačítko pozastavit zastavíte řízení časovače.](master-pages-and-asp-net-ajax-cs/_static/image32.png)](master-pages-and-asp-net-ajax-cs/_static/image31.png)

**Obrázek 11**: kliknutím na tlačítko pozastavit zastavíte řízení časovače ([kliknutím zobrazíte obrázek v plné velikosti).](master-pages-and-asp-net-ajax-cs/_static/image33.png)

[![kliknutím na tlačítko pokračovat restartujte časovač.](master-pages-and-asp-net-ajax-cs/_static/image35.png)](master-pages-and-asp-net-ajax-cs/_static/image34.png)

**Obrázek 12**: kliknutím na tlačítko Obnovit spustíte časovač ([kliknutím zobrazíte obrázek v plné velikosti](master-pages-and-asp-net-ajax-cs/_static/image36.png)).

## <a name="summary"></a>Přehled

Při sestavování webových aplikací s podporou jazyka AJAX pomocí rozhraní ASP.NET AJAX je nezbytné, aby každá webová stránka s povoleným AJAX zahrnovala ovládací prvek ScriptManager. Abychom tento proces usnadnili, můžeme do stránky předlohy přidat ScriptManager místo nutnosti nezapomeňte si přidat ScriptManager na každou stránku obsahu a všechny. Krok 1 ukázal, jak přidat ScriptManager do hlavní stránky, zatímco krok 2 se prohlédl při implementaci funkcionality AJAX na stránce obsahu.

Pokud potřebujete přidat vlastní skripty, odkazy na webové služby s povoleným skriptem nebo přizpůsobené ověřování, autorizaci nebo profilové služby na konkrétní stránku obsahu, přidejte na stránku obsahu ovládací prvek ScriptManagerProxy a pak nakonfigurujte vlastní nastavení. Krok 3 se zabývá tím, jak použít ScriptManagerProxy k registraci vlastního souboru JavaScriptu na konkrétní stránce obsahu.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [ASP.NET AJAX Framework](../../../../ajax/index.md)
- [Výukové kurzy pro ASP.NET AJAX](../aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax.md)
- [Videa ASP.NET AJAX](../../../videos/aspnet-ajax/index.md)
- [Sestavování interaktivního uživatelského rozhraní pomocí Microsoft ASP.NET AJAX](http://aspnet.4guysfromrolla.com/articles/101007-1.aspx)
- [Použití NEWID k náhodnému řazení záznamů](http://www.sqlteam.com/article/using-newid-to-randomly-sort-records)
- [Použití ovládacího prvku Timer](http://aspnet.4guysfromrolla.com/articles/061808-1.aspx)

### <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 3,5 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco). Scott se dá kontaktovat [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](interacting-with-the-content-page-from-the-master-page-cs.md)
> [Další](specifying-the-master-page-programmatically-cs.md)

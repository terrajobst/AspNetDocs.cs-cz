---
uid: web-forms/overview/older-versions-getting-started/master-pages/multiple-contentplaceholders-and-default-content-vb
title: Několik prvků ContentPlaceHolder a výchozí obsah (VB) | Microsoft Docs
author: rick-anderson
description: Kontroluje, jak do hlavní stránky přidat více držitelů obsahu a jak zadat výchozí obsah v držitelích umístění obsahu.
ms.author: riande
ms.date: 05/21/2008
ms.assetid: 866a7177-6884-451e-88f4-c934b1dd1af5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/multiple-contentplaceholders-and-default-content-vb
msc.type: authoredcontent
ms.openlocfilehash: b71cacb143094dcc5cf483c69c2fcc0f10def51c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78571895"
---
# <a name="multiple-contentplaceholders-and-default-content-vb"></a>Několik prvků ContentPlaceHolder a výchozí obsah (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_02_VB.zip) nebo [stažení PDF](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_02_VB.pdf)

> Kontroluje, jak do hlavní stránky přidat více držitelů obsahu a jak zadat výchozí obsah v držitelích umístění obsahu.

## <a name="introduction"></a>Úvod

V předchozím kurzu jsme prozkoumali, jak stránky předloh umožňují vývojářům ASP.NET vytvořit konzistentní rozložení na úrovni webu. Stránky předlohy definují jak kód, který je společný pro všechny stránky obsahu a oblasti, které jsou přizpůsobitelné na základě stránky. V předchozím kurzu jsme vytvořili jednoduchou stránku předlohy (`Site.master`) a dvě stránky obsahu (`Default.aspx` a `About.aspx`). Naše stránka předlohy se skládá ze dvou prvků ContentPlaceHolder s názvem `head` a `MainContent`, které byly umístěny v prvku `<head>` a ve webovém formuláři v uvedeném pořadí. I když mají stránky obsahu dva ovládací prvky obsahu, určili jsme pouze označení pro ten, který odpovídá `MainContent`.

Jak prokáže dva ovládací prvky ContentPlaceHolder v `Site.master`, stránka předlohy může obsahovat více prvků ContentPlaceHolder. A co více, stránka předlohy může určovat výchozí označení pro ovládací prvky ContentPlaceHolder. Stránka obsahu, pak může volitelně určovat vlastní značku nebo použít výchozí označení. V tomto kurzu se podíváme na použití více ovládacích prvků obsahu na stránce předlohy a viz definování výchozích značek v ovládacích prvcích ContentPlaceHolder.

## <a name="step-1-adding-additional-contentplaceholder-controls-to-the-master-page"></a>Krok 1: Přidání dalších ovládacích prvků ContentPlaceHolder do stránky předlohy

Mnoho návrhů webů obsahuje několik oblastí na obrazovce, které jsou přizpůsobené na základě stránky. `Site.master`hlavní stránka, kterou jsme vytvořili v předchozím kurzu, obsahuje jeden prvek ContentPlaceHolder v rámci webového formuláře s názvem `MainContent`. Konkrétně je tento prvek ContentPlaceHolder umístěný v rámci prvku `mainContent` `<div>`.

Obrázek 1 zobrazuje `Default.aspx` při prohlížení v prohlížeči. Oblast KRUHOVÁ v Red je značka specifická pro stránku, která odpovídá `MainContent`.

[![oblasti v kruhu zobrazuje oblast, která je aktuálně přizpůsobitelná pro stránku na základě stránky.](multiple-contentplaceholders-and-default-content-vb/_static/image2.png)](multiple-contentplaceholders-and-default-content-vb/_static/image1.png)

**Obrázek 01**: oblast v kruhu zobrazuje oblast, která je aktuálně přizpůsobitelná na stránce ([kliknutím zobrazíte obrázek v plné velikosti).](multiple-contentplaceholders-and-default-content-vb/_static/image3.png)

Představte si, že kromě oblasti zobrazené na obrázku 1 je také potřeba do levého sloupce v sekcích lekce a novinky přidat položky specifické pro stránku. K tomu přidáváme další ovládací prvek ContentPlaceHolder na stránku předlohy. Chcete-li postup sledovat, otevřete stránku předlohy `Site.master` v aplikaci Visual Web Developer a přetáhněte ovládací prvek ContentPlaceHolder z panelu nástrojů do návrháře za sekcí zprávy. Nastavte `ID` prvku ContentPlaceHolder na `LeftColumnContent`.

[![přidat ovládací prvek ContentPlaceHolder do levého sloupce stránky předlohy](multiple-contentplaceholders-and-default-content-vb/_static/image5.png)](multiple-contentplaceholders-and-default-content-vb/_static/image4.png)

**Obrázek 02**: Přidejte ovládací prvek ContentPlaceHolder do levého sloupce stránky předlohy ([kliknutím zobrazíte obrázek v plné velikosti).](multiple-contentplaceholders-and-default-content-vb/_static/image6.png)

Po přidání prvku `LeftColumnContent` ContentPlaceHolder na stránku předlohy můžeme pro tuto oblast definovat obsah na stránce na základě stránky, a to tak, že na stránce přidáte ovládací prvek obsahu, jehož `ContentPlaceHolderID` je nastavená na `LeftColumnContent`. Tento proces prověříme v kroku 2.

## <a name="step-2-defining-content-for-the-new-contentplaceholder-in-the-content-pages"></a>Krok 2: definování obsahu pro nový prvek ContentPlaceHolder na stránkách obsahu

Při přidávání nové stránky obsahu na web aplikace Visual Web Developer automaticky vytvoří ovládací prvek obsahu na stránce pro každý prvek ContentPlaceHolder ve vybrané stránce předlohy. Po přidání prvku `LeftColumnContent` ContentPlaceHolder na naši stránku předlohy v kroku 1 budou nové stránky ASP.NET nyní mít tři ovládací prvky obsahu.

Chcete-li to ilustrovat, přidejte novou stránku obsahu do kořenového adresáře s názvem `MultipleContentPlaceHolders.aspx`, který je vázán na `Site.master` stránku předlohy. Visual Web Developer vytvoří tuto stránku s následujícím deklarativním označením:

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample1.aspx)]

Do ovládacího prvku obsahu, který odkazuje na `MainContent` ContentPlaceHolders (`Content2`), zadejte nějaký obsah. Dále přidejte následující kód do ovládacího prvku `Content3` obsahu (který odkazuje na `LeftColumnContent` ContentPlaceHolder):

[!code-html[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample2.html)]

Po přidání tohoto kódu navštivte stránku v prohlížeči. Jak ukazuje obrázek 3, značky umístěné v ovládacím prvku obsahu `Content3` se zobrazí v levém sloupci pod částí zprávy (v kruhu červeně). Značky, které jsou umístěny v `Content2`, se zobrazí v pravé části stránky (v kruhu modře).

[![levý sloupec teď obsahuje obsah specifický pro stránku pod oddílem novinky.](multiple-contentplaceholders-and-default-content-vb/_static/image8.png)](multiple-contentplaceholders-and-default-content-vb/_static/image7.png)

**Obrázek 03**: levý sloupec teď obsahuje obsah specifický pro stránku pod částí Novinky ([kliknutím zobrazíte obrázek v plné velikosti).](multiple-contentplaceholders-and-default-content-vb/_static/image9.png)

### <a name="defining-content-in-existing-content-pages"></a>Definování obsahu v existujících stránkách obsahu

Při vytvoření nové stránky obsahu se automaticky vytvoří ovládací prvek ContentPlaceHolder, který jsme přidali v kroku 1. Ale naše dvě existující stránky obsahu – `About.aspx` a `Default.aspx` – nemají ovládací prvek obsahu pro `LeftColumnContent` ContentPlaceHolder. K určení obsahu pro tento prvek ContentPlaceHolder na těchto dvou existujících stránkách musíme přidat ovládací prvek obsahu dodržovali.

Na rozdíl od většiny webových ovládacích prvků ASP.NET neobsahuje sada nástrojů Visual Web Developer položku ovládacího prvku obsahu. Do zobrazení zdroj můžeme ručně zadat deklarativní označení ovládacího prvku obsahu, ale jednodušší a rychlejší přístup je použít zobrazení Návrh. Otevřete stránku `About.aspx` a přepněte na zobrazení Návrh. Jak ukazuje obrázek 4, `LeftColumnContent` prvek ContentPlaceHolder se zobrazí v zobrazení Návrh; Pokud ukazatel myši nakročíte, zobrazí se nadpis zobrazit: "LeftColumnContent (hlavní)". Zahrnutí "Master" v názvu znamená, že na stránce pro tento prvek ContentPlaceHolder není definován žádný ovládací prvek obsahu. Pokud existuje ovládací prvek obsahu pro prvky ContentPlaceHolder, jako v případě `MainContent`, nadpis se přečte: "*ContentPlaceHolderID* (vlastní)".

Chcete-li přidat ovládací prvek obsahu pro `LeftColumnContent` prvky ContentPlaceHolder do `About.aspx`, rozbalte inteligentní značku ContentPlaceHolder a klikněte na odkaz vytvořit vlastní obsah.

[![zobrazení Návrh pro about. aspx zobrazí LeftColumnContent ContentPlaceHolder](multiple-contentplaceholders-and-default-content-vb/_static/image11.png)](multiple-contentplaceholders-and-default-content-vb/_static/image10.png)

**Obrázek 04**: zobrazení návrhu pro `About.aspx` zobrazuje `LeftColumnContent` ContentPlaceHolder ([kliknutím zobrazíte obrázek v plné velikosti](multiple-contentplaceholders-and-default-content-vb/_static/image12.png)).

Kliknutím na odkaz vytvořit vlastní obsah vygenerujete potřebný ovládací prvek obsahu na stránce a nastavíte jeho vlastnost `ContentPlaceHolderID` na `ID`ContentPlaceHolder. Například kliknutím na odkaz vytvořit vlastní obsah pro `LeftColumnContent` oblasti v `About.aspx` na stránku přidá následující deklarativní označení:

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample3.aspx)]

### <a name="omitting-content-controls"></a>Vynechávání ovládacích prvků obsahu

ASP.NET nevyžaduje, aby všechny stránky obsahu zahrnovaly ovládací prvky obsahu pro všechny a všechny prvky ContentPlaceHolder definované na stránce předlohy. Pokud je ovládací prvek obsahu vynechán, používá modul ASP.NET značky definované v prvku ContentPlaceHolder na stránce předlohy. Tento kód se označuje jako *výchozí obsah* ovládacího prvku ContentPlaceHolder a je užitečný ve scénářích, kdy je obsah pro některé oblasti společný mezi většinou stránek, ale musí být přizpůsoben pro malý počet stránek. Krok 3 zkoumá určení výchozího obsahu na stránce předlohy.

V současné době `Default.aspx` obsahuje dva ovládací prvky obsahu pro `head` a `MainContent` prvky ContentPlaceHolder; nemá ovládací prvek obsahu pro `LeftColumnContent`. V důsledku toho se při `Default.aspx` vykreslí výchozí obsah `LeftColumnContent` ContentPlaceHolder. Vzhledem k tomu, že jsme ještě pro tento prvek ContentPlaceHolder definovali libovolný výchozí obsah, čistý efekt není pro tuto oblast vygenerován žádný kód. Pokud chcete toto chování ověřit, navštivte `Default.aspx` v prohlížeči. Na obrázku 5 ukazuje, že v levém sloupci pod sekcí novinky nejsou vygenerovány žádné značky.

[![není vykreslen žádný obsah pro LeftColumnContent ContentPlaceHolder](multiple-contentplaceholders-and-default-content-vb/_static/image14.png)](multiple-contentplaceholders-and-default-content-vb/_static/image13.png)

**Obrázek 05**: pro `LeftColumnContent` ContentPlaceHolder není vykreslen žádný obsah ([kliknutím zobrazíte obrázek v plné velikosti).](multiple-contentplaceholders-and-default-content-vb/_static/image15.png)

## <a name="step-3-specifying-default-content-in-the-master-page"></a>Krok 3: určení výchozího obsahu na stránce předlohy

Některé návrhy webů obsahují oblast, jejíž obsah je stejný pro všechny stránky v lokalitě s výjimkou jedné nebo dvou výjimek. Vezměte v úvahu web, který podporuje uživatelské účty. Tato lokalita vyžaduje přihlašovací stránku, kde můžou Návštěvníci zadat své přihlašovací údaje, aby se přihlásili k webu. Pro urychlení procesu přihlašování můžou Návrháři webu zahrnovat textová pole uživatelských jmen a hesel v levém horním rohu každé stránky, aby se uživatelé mohli přihlašovat, aniž by museli explicitně navštívit přihlašovací stránku. I když jsou tato textová pole uživatelských jmen a hesel užitečná ve většině stránek, jsou redundantní na přihlašovací stránce, která už obsahuje textová pole pro přihlašovací údaje uživatele.

Chcete-li implementovat tento návrh, můžete vytvořit ovládací prvek ContentPlaceHolder v levém horním rohu stránky předlohy. Každá stránka, která je nutná k zobrazení uživatelského jména a hesla v levém horním rohu, by měla vytvořit ovládací prvek obsahu pro tento prvek ContentPlaceHolder a přidat potřebné rozhraní. Přihlašovací stránka na druhé straně buď vynechat přidání ovládacího prvku obsahu pro tento prvek ContentPlaceHolder, nebo by vytvořila ovládací prvek obsahu bez definovaných značek. Nevýhodou tohoto přístupu je, že nezapomeňte přidat textová pole uživatelských jmen a hesel na každou stránku, kterou do webu přidáte (kromě přihlašovací stránky). Tím se žádá o problémy. Je pravděpodobné, že byste zapomněli přidat tato textová pole na stránku nebo dvě nebo horší, ale rozhraní nemůžeme správně implementovat (možná přidáte pouze jedno textové pole namísto dvou).

Lepším řešením je definovat textové pole uživatelského jména a hesla jako výchozí obsah prvku ContentPlaceHolder. Tímto způsobem musíme tento výchozí obsah přepsat jenom na těchto stránkách, které nezobrazují textová jména a hesla (například přihlašovací stránka). Pro ilustraci určení výchozího obsahu pro ovládací prvek ContentPlaceHolder je implementován scénář, který je právě diskutován.

> [!NOTE]
> Zbývající část tohoto kurzu aktualizuje náš web a vloží přihlašovací rozhraní do levého sloupce pro všechny stránky, ale přihlašovací stránku. V tomto kurzu se ale nezabývá konfigurací webu pro podporu uživatelských účtů. Další informace o tomto tématu najdete v kurzech pro [ověřování a autorizaci uživatelských účtů a rolí](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md) .

### <a name="adding-a-contentplaceholder-and-specifying-its-default-content"></a>Přidání prvku ContentPlaceHolder a určení jeho výchozího obsahu

Otevřete stránku předlohy `Site.master` a přidejte následující kód do levého sloupce mezi oddílem `DateDisplay` popisek a lekce:

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample4.aspx)]

Po přidání tohoto kódu by se zobrazení Návrh hlavní stránky měla podobat obrázku 6.

[![hlavní stránka obsahuje ovládací prvek přihlášení.](multiple-contentplaceholders-and-default-content-vb/_static/image17.png)](multiple-contentplaceholders-and-default-content-vb/_static/image16.png)

**Obrázek 6**: Stránka předlohy obsahuje ovládací prvek přihlášení ([kliknutím zobrazíte obrázek v plné velikosti](multiple-contentplaceholders-and-default-content-vb/_static/image18.png)).

Tento prvek ContentPlaceHolder, `QuickLoginUI`, má přihlašovací web jako svůj výchozí obsah. Ovládací prvek Login zobrazí uživatelské rozhraní, které vyzve uživatele k zadání uživatelského jména a hesla spolu s tlačítkem přihlásit se. Po kliknutí na tlačítko Přihlásit se ovládací prvek přihlášení interně ověří přihlašovací údaje uživatele k rozhraní API pro členství. Chcete-li použít tento ovládací prvek přihlášení v praxi, je nutné nakonfigurovat lokalitu tak, aby používala členství. Toto téma překračuje rámec tohoto kurzu; Další informace o vytváření webových aplikací, které podporují uživatelské účty, najdete v výukových kurzech k [ověřování pomocí formulářů, autorizaci, uživatelských účtů a rolí](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md) .

Nebojte se přizpůsobení chování nebo vzhledu přihlašovacího ovládacího prvku. Nastavil jsem dvě z vlastností: `TitleText` a `FailureAction`. Hodnota vlastnosti `TitleText`, která má výchozí hodnotu "přihlásit", se zobrazí v horní části uživatelského rozhraní ovládacího prvku. Nastavil (a) jsem tuto vlastnost, aby zobrazila text "přihlásit" jako prvek `<h3>`. Vlastnost `FailureAction` určuje, co dělat, když jsou přihlašovací údaje uživatele neplatné. Použije se výchozí hodnota `Refresh`, která uživatele opustí na stejné stránce a v ovládacím prvku pro přihlášení zobrazí zprávu o selhání. Změnil jsem ho na `RedirectToLoginPage`, který uživateli pošle přihlašovací stránku v případě neplatných přihlašovacích údajů. Raději poslat uživatele na přihlašovací stránku, když se uživatel pokusí přihlásit z nějaké jiné stránky, ale neproběhne úspěšně, protože přihlašovací stránka může obsahovat další pokyny a možnosti, které se nedají snadno umístit do levého sloupce. Přihlašovací stránka může například obsahovat možnosti pro načtení zapomenutého hesla nebo vytvoření nového účtu.

### <a name="creating-the-login-page-and-overriding-the-default-content"></a>Vytvoření přihlašovací stránky a přepsání výchozího obsahu

Po dokončení hlavní stránky je dalším krokem vytvoření přihlašovací stránky. Přidejte stránku ASP.NET do kořenového adresáře vaší lokality s názvem `Login.aspx`a naváže ji na `Site.master` stránku předlohy. Tím se vytvoří stránka se čtyřmi ovládacími prvky obsahu, jednu pro každý prvek ContentPlaceHolder definovaný v `Site.master`.

Přidejte ovládací prvek pro přihlášení do ovládacího prvku `MainContent` obsahu. Můžete také volně přidávat obsah do oblasti `LeftColumnContent`. Nezapomeňte ale ponechat ovládací prvek obsahu pro `QuickLoginUI` ContentPlaceHolder prázdné. Tím se zajistí, že se ovládací prvek přihlášení nezobrazí v levém sloupci přihlašovací stránky.

Po definování obsahu pro `MainContent` a oblasti `LeftColumnContent` by deklarativní označení přihlašovací stránky mělo vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](multiple-contentplaceholders-and-default-content-vb/samples/sample5.aspx)]

Obrázek 7 ukazuje tuto stránku při prohlížení v prohlížeči. Vzhledem k tomu, že tato stránka určuje ovládací prvek obsahu pro `QuickLoginUI` ContentPlaceHolder, přepíše výchozí obsah zadaný na stránce předlohy. Netto efekt je, že ovládací prvek přihlášení zobrazený v zobrazení Návrh hlavní stránky (viz obrázek 6) není vykreslen na této stránce.

[![přihlašovací stránka přestiskne výchozí obsah QuickLoginUI ContentPlaceHolder.](multiple-contentplaceholders-and-default-content-vb/_static/image20.png)](multiple-contentplaceholders-and-default-content-vb/_static/image19.png)

**Obrázek 7**: přihlašovací stránka znovu stiskne výchozí obsah `QuickLoginUI` ContentPlaceHolder ([kliknutím zobrazíte obrázek v plné velikosti).](multiple-contentplaceholders-and-default-content-vb/_static/image21.png)

### <a name="using-the-default-content-in-new-pages"></a>Použití výchozího obsahu na nových stránkách

Chceme zobrazit přihlašovací ovládací prvek v levém sloupci pro všechny stránky kromě přihlašovací stránky. Chcete-li toho dosáhnout, všechny stránky obsahu s výjimkou přihlašovací stránky by měly vypustit ovládací prvek obsahu pro `QuickLoginUI` ContentPlaceHolder. Vynecháte-li ovládací prvek obsahu, místo toho bude použit výchozí obsah ovládacího prvku ContentPlaceHolder.

Naše existující stránky obsahu – `Default.aspx`, `About.aspx`a `MultipleContentPlaceHolders.aspx` – neobsahují ovládací prvek obsahu pro `QuickLoginUI`, protože byly vytvořeny před tím, než jsme přidali ovládací prvek ContentPlaceHolder na stránku předlohy. Proto tyto existující stránky nemusíte aktualizovat. Nové stránky přidané na web však ve výchozím nastavení zahrnují ovládací prvek obsahu pro `QuickLoginUI` ContentPlaceHolder. Proto si nezapomeňte tyto ovládací prvky obsahu odebrat pokaždé, když přidáváme novou stránku obsahu (Pokud nechcete přepsat výchozí obsah ovládacího prvku ContentPlaceHolder, jako v případě přihlašovací stránky).

Chcete-li odebrat ovládací prvek obsahu, můžete buď ručně odstranit jeho deklarativní označení ze zdrojového zobrazení, nebo z zobrazení Návrh, z jeho inteligentní značky vyberte odkaz výchozí nastavení pro hlavní obsah předlohy. Buď přístup odebere ovládací prvek obsahu ze stránky a vytvoří stejný čistý efekt.

Obrázek 8 zobrazuje `Default.aspx` při prohlížení v prohlížeči. Odvolání tohoto `Default.aspx` má pouze dva ovládací prvky obsahu, které jsou zadány v deklarativní značce-One pro `head` a jeden pro `MainContent`. V důsledku toho se zobrazí výchozí obsah pro `LeftColumnContent` a `QuickLoginUI` prvky ContentPlaceHolder.

[![se zobrazí výchozí obsah pro prvky ContentPlaceHolder LeftColumnContent a QuickLoginUI.](multiple-contentplaceholders-and-default-content-vb/_static/image23.png)](multiple-contentplaceholders-and-default-content-vb/_static/image22.png)

**Obrázek 08**: zobrazí se výchozí obsah pro `LeftColumnContent` a `QuickLoginUI` ContentPlaceHolders ([kliknutím zobrazíte obrázek v plné velikosti](multiple-contentplaceholders-and-default-content-vb/_static/image24.png)).

## <a name="summary"></a>Souhrn

Model hlavní stránky ASP.NET umožňuje na stránce předlohy libovolný počet prvků ContentPlaceHolder. Prvky ContentPlaceHolders obsahují výchozí obsah, který je generován v případě, že na stránce obsahu není žádný odpovídající ovládací prvek obsahu. V tomto kurzu jsme viděli, jak zahrnout další ovládací prvky ContentPlaceHolder na stránce předlohy a jak definovat ovládací prvky obsahu pro tyto nové prvky ContentPlaceHolder na nové i stávající ASP.NET stránky. Zjistili jsme také určení výchozího obsahu v prvku ContentPlaceHolder, který je užitečný ve scénářích, kdy pouze menšina stran musí přizpůsobit jinak standardizovaný obsah v určité oblasti.

V dalším kurzu prověříme `head` ContentPlaceHolder podrobněji, dozvíte se, jak deklarativně a programově definovat nadpis, meta značky a další záhlaví HTML na stránce stránkou.

Šťastné programování!

### <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 3,5 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Scott se dá kontaktovat [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Vedoucí recenzent pro tento kurz byl takový Banerjee. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com).

> [!div class="step-by-step"]
> [Předchozí](creating-a-site-wide-layout-using-master-pages-vb.md)
> [Další](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md)

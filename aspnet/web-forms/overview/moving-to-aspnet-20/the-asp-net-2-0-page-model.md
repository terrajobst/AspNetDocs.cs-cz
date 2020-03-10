---
uid: web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
title: Model stránky ASP.NET 2,0 | Microsoft Docs
author: microsoft
description: V ASP.NET 1. x si vývojáři zvolili mezi vloženým kódovým modelem a modelem kódu na pozadí. Kód na pozadí lze implementovat buď pomocí src ATTR...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: af4575a3-0ae3-4638-ba4d-218fad7a1642
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/the-asp-net-2-0-page-model
msc.type: authoredcontent
ms.openlocfilehash: bcb71b2b5a484e8756406867e08e8aa699a9024d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547647"
---
# <a name="the-aspnet-20-page-model"></a>Model stránky ASP.NET 2,0

od [Microsoftu](https://github.com/microsoft)

> V ASP.NET 1. x si vývojáři zvolili mezi vloženým kódovým modelem a modelem kódu na pozadí. Kód na pozadí lze implementovat buď pomocí atributu src, nebo atributu CodeBehind direktivy @Page. V ASP.NET 2,0 mají vývojáři stále možnost volby mezi vloženým kódem a kódem na pozadí, ale existovala významná vylepšení modelu kódu na pozadí.

V ASP.NET 1. x si vývojáři zvolili mezi vloženým kódovým modelem a modelem kódu na pozadí. Kód na pozadí lze implementovat buď pomocí atributu src, nebo atributu CodeBehind direktivy @Page. V ASP.NET 2,0 mají vývojáři stále možnost volby mezi vloženým kódem a kódem na pozadí, ale existovala významná vylepšení modelu kódu na pozadí.

## <a name="improvements-in-the-code-behind-model"></a>Vylepšení modelu kódu na pozadí

Aby bylo možné plně pochopit změny v modelu kódu na pozadí v ASP.NET 2,0, je nejvhodnější rychle zkontrolovat model, protože existoval v ASP.NET 1. x.

## <a name="the-code-behind-model-in-aspnet-1x"></a>Model kódu na pozadí v ASP.NET 1. x

V ASP.NET 1. x se model kódu na pozadí skládá ze souboru ASPX (WebForm) a souboru kódu na pozadí, který obsahuje kód programování. Tyto dva soubory byly připojeny pomocí direktivy @Page v souboru ASPX. Každý ovládací prvek na stránce ASPX měl v souboru kódu na pozadí odpovídající deklaraci jako proměnnou instance. Soubor kódu na pozadí také obsahoval kód pro vazby události a generovaný kód potřebný pro návrháře sady Visual Studio. Tento model pracoval poměrně dobře, ale vzhledem k tomu, že každý element ASP.NET na ASPX stránce požaduje odpovídající kód v souboru kódu na pozadí, neexistovala žádná nepravdivá separace kódu a obsahu. Například pokud návrhář přidal nový serverový ovládací prvek do souboru ASPX mimo prostředí Visual Studio IDE, aplikace by byla přerušena z důvodu nepřítomnosti deklarace pro daný ovládací prvek v souboru kódu na pozadí.

## <a name="the-code-behind-model-in-aspnet-20"></a>Model kódu na pozadí v ASP.NET 2,0

ASP.NET 2,0 se na tomto modelu významně vylepšuje. V ASP.NET 2,0 je kód na pozadí implementován pomocí nových *dílčích tříd* poskytovaných v ASP.NET 2,0. Třída kódu na pozadí v ASP.NET 2,0 je definována jako částečná třída, což znamená, že obsahuje pouze část definice třídy. Zbývající část definice třídy je dynamicky generována serverem ASP.NET 2,0 pomocí stránky ASPX za běhu nebo při Předkompilování webu. Propojení mezi souborem kódu na pozadí a stránkou ASPX je stále vytvořeno pomocí direktivy @ Page. Namísto atributu CodeBehind nebo src však nyní ASP.NET 2,0 používá atribut CodeFile. Atribut Inherits se používá také k zadání názvu třídy pro stránku.

Typická direktiva @ Page může vypadat takto:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample1.aspx)]

Typická definice třídy v souboru s kódem na pozadí ASP.NET 2,0 může vypadat takto:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample2.cs)]

> [!NOTE]
> C#a Visual Basic jsou jedinými spravovanými jazyky, které aktuálně podporují částečné třídy. Vývojáři používající jazyk J# proto nebudou moci používat model kódu na pozadí v ASP.NET 2,0.

Nový model vylepšuje model kódu na pozadí, protože vývojáři teď budou mít soubory kódu, které obsahují pouze kód, který vytvořil. Poskytuje také skutečné oddělení kódu a obsahu, protože v souboru kódu na pozadí nejsou žádné deklarace proměnných instance.

> [!NOTE]
> Vzhledem k tomu, že částečná třída pro stránku ASPX je provedena vazba události, Visual Basic vývojáři mohou využít mírné zvýšení výkonu pomocí klíčového slova Handles v kódu na pozadí ke svázání událostí. C#nemá žádné ekvivalentní klíčové slovo.

## <a name="new--page-directive-attributes"></a>Nové atributy direktivy @ Page

ASP.NET 2,0 přidává do direktivy @ Page mnoho nových atributů. Následující atributy jsou v ASP.NET 2,0 novinkou.

## <a name="async"></a>Async

Atribut Async umožňuje konfigurovat spouštění stránky asynchronně. V tomto modulu je dobré pokrýt asynchronní stránky později.

## <a name="asynctimeout"></a>AsyncTimeout

Určil časový limit pro asynchronní stránky. Výchozí hodnota je 45 sekund.

## <a name="codefile"></a>CodeFile

Atribut CodeFile je náhradou pro atribut CodeBehind v aplikaci Visual Studio 2002/2003.

### <a name="codefilebaseclass"></a>CodeFileBaseClass

Atribut CodeFileBaseClass se používá v případech, kdy chcete více stránek odvodit z jedné základní třídy. Z důvodu implementace dílčích tříd v ASP.NET bez tohoto atributu základní třída, která používá sdílené společné pole na referenční ovládací prvky deklarované na ASPX stránce, nebude fungovat správně, protože prostředí kompilace ASP vytvoří nové členy automaticky na základě ovládacích prvků na stránce. Proto pokud chcete společnou základní třídu pro dvě nebo více stránek v ASP.NET, budete muset definovat zadat základní třídu v atributu CodeFileBaseClass a poté odvodit každou třídu Pages z této základní třídy. Atribut CodeFile je také vyžadován při použití tohoto atributu.

## <a name="compilationmode"></a>CompilationMode nastavena

Tento atribut umožňuje nastavit vlastnost CompilationMode nastavena stránky ASPX. Vlastnost CompilationMode nastavena je výčet, který obsahuje hodnoty **Always**, **auto**a **Never**. Výchozí hodnota je **vždy**. **Automatické** nastavení zabrání ASP.NET dynamické kompilaci stránky, pokud je to možné. Vyloučení stránek z dynamické kompilace zvyšuje výkon. Pokud však vyloučená stránka obsahuje tento kód, který musí být zkompilován, při procházení stránky dojde k chybě.

## <a name="enableeventvalidation"></a>EnableEventValidation

Tento atribut určuje, zda jsou události zpětného odeslání a zpětného volání ověřovány. Pokud je tato možnost povolena, jsou vráceny argumenty události zpětného odeslání nebo zpětného volání, aby bylo zajištěno, že pocházejí z ovládacího prvku serveru, který je původně vykreslil.

## <a name="enabletheming"></a>EnableTheming

Tento atribut určuje, zda se na stránce používají motivy ASP.NET. Výchozí hodnota je **false**. Motivy ASP.NET jsou pokryté v [modulu 10](profiles-themes-and-web-parts.md).

## <a name="linepragmas"></a>LinePragmas

Tento atribut určuje, zda by měly být během kompilace přidány direktivy řádku. Direktivy pragma řádku jsou možnosti používané ladicími programy k označení konkrétních sekcí kódu.

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostback

Tento atribut určuje, zda je JavaScript vložen do stránky, aby bylo možné zachovat pozici posouvání mezi zpětnými odesláními. Tento atribut ve výchozím nastavení má **hodnotu false** .

Pokud je tento atribut **true**, ASP.NET přidá skript &lt;&gt; blok při postbacku, který vypadá takto:

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample3.html)]

Všimněte si, že src pro tento blok skriptu je WebResource. axd. Tento prostředek není fyzickou cestou. Když se tento skript vyžádá, ASP.NET dynamicky vytvoří skript.

### <a name="masterpagefile"></a>MasterPageFile

Tento atribut určuje soubor hlavní stránky pro aktuální stránku. Cesta může být relativní nebo absolutní. Stránky předlohy jsou pokryté v [modulu 4](master-pages.md).

## <a name="stylesheettheme"></a>StyleSheetTheme

Tento atribut umožňuje přepsat vlastnosti vzhledu uživatelského rozhraní definované motivem ASP.NET 2,0. Motivy jsou pokryté v [modulu 10](profiles-themes-and-web-parts.md).

## <a name="theme"></a>Použit

Určuje motiv stránky. Pokud není zadána hodnota pro atribut StyleSheetTheme, přepíše atribut Theme všechny styly použité u ovládacích prvků na stránce.

## <a name="title"></a>Název

Nastaví název stránky. Hodnota zadaná zde se zobrazí v prvku &lt;název&gt; vykreslené stránky.

### <a name="viewstateencryptionmode"></a>ViewStateEncryptionMode

Nastaví hodnotu výčtu ViewStateEncryptionMode. Dostupné hodnoty jsou **vždycky**, **auto**a **nikdy**. Výchozí hodnota je **auto**. Pokud je tento atribut nastaven na hodnotu **auto**, je vlastnost ViewState zašifrovaná, je ovládací prvek požádá o volání metody **Metoda RegisterRequiresViewStateEncryption** .

## <a name="setting-public-property-values-via-the--page-directive"></a>Nastavení hodnot veřejných vlastností prostřednictvím direktivy @ Page

Další novou funkcí direktivy @ Page v ASP.NET 2,0 je schopnost nastavit počáteční hodnotu veřejných vlastností základní třídy. Předpokládejme například, že máte veřejnou vlastnost s názvem **SomeText** v základní třídě a Vy d chcete, aby byla inicializována jako **Hello** při načtení stránky. To lze provést pouhým nastavením hodnoty v direktivě @ Page, např.:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample4.aspx)]

Atribut **SomeText** direktivy @ Page nastaví počáteční hodnotu vlastnosti SomeText v základní třídě na hodnotu *Hello!* . Následující video je návodem k nastavení počáteční hodnoty veřejné vlastnosti v základní třídě pomocí direktivy @ Page.

![](the-asp-net-2-0-page-model/_static/image1.png)

[Otevření videa na celé obrazovce](the-asp-net-2-0-page-model/_static/setprop1.wmv)

## <a name="new-public-properties-of-the-page-class"></a>Nové veřejné vlastnosti třídy Page

Následující veřejné vlastnosti jsou v ASP.NET 2,0 novinkou.

## <a name="apprelativetemplatesourcedirectory"></a>AppRelativeTemplateSourceDirectory

Vrátí relativní cestu k aplikaci pro stránku nebo ovládací prvek. Například pro stránku nacházející se v http://app/folder/page.aspxvrátí vlastnost ~/Folder/.

## <a name="apprelativevirtualpath"></a>AppRelativeVirtualPath

Vrátí relativní cestu virtuálního adresáře k stránce nebo ovládacímu prvku. Například pro stránku nacházející se v http://app/folder/page.aspxvrátí vlastnost ~/Folder/Page.aspx.

## <a name="asynctimeout"></a>AsyncTimeout

Získá nebo nastaví časový limit, který se používá pro asynchronní zpracování stránky. (Na asynchronní stránky se pojednává později v tomto modulu.)

## <a name="clientquerystring"></a>ClientQueryString

Vlastnost jen pro čtení, která vrací část řetězce dotazu požadované adresy URL. Tato hodnota je zakódovaná v adrese URL. K dekódování můžete použít metodu UrlDecode třídy HttpServerUtility.

## <a name="clientscript"></a>ClientScript

Tato vlastnost vrátí objekt ClientScriptManager, který se dá použít ke správě technologie ASP. sítě vynásobení emisí skriptu na straně klienta. (Třída ClientScriptManager se zabývá dále v tomto modulu.)

## <a name="enableeventvalidation"></a>EnableEventValidation

Tato vlastnost určuje, zda je povoleno ověřování událostí pro události zpětného volání a zpětného volání. Pokud je povoleno, jsou argumenty pro zpětné odeslání nebo události zpětného volání ověřovány, aby bylo zajištěno, že pocházejí z ovládacího prvku serveru, který je původně vykreslil.

## <a name="enabletheming"></a>EnableTheming

Tato vlastnost získá nebo nastaví logickou hodnotu, která určuje, zda se na stránku vztahuje motiv ASP.NET 2,0.

## <a name="form"></a>Formulář

Tato vlastnost vrátí formulář HTML na stránce ASPX jako objekt HtmlForm.

## <a name="header"></a>Hlavička

Tato vlastnost vrací odkaz na objekt HtmlHead, který obsahuje záhlaví stránky. Vrácený objekt HtmlHead lze použít k získání nebo nastavení šablon stylů, meta značek atd.

## <a name="idseparator"></a>IdSeparator

Tato vlastnost jen pro čtení získá znak, který se používá k oddělení identifikátorů ovládacího prvku, když ASP.NET vytváří jedinečné ID pro ovládací prvky na stránce. Tato metoda není zamýšlena pro použití přímo z vašeho kódu.

## <a name="isasync"></a>IsAsync

Tato vlastnost umožňuje asynchronní stránky. Asynchronní stránky jsou popsány dále v tomto modulu.

## <a name="iscallback"></a>Zpětné volání

Tato vlastnost jen pro čtení vrátí **hodnotu true** , pokud je stránka výsledkem zpětného volání. Zpětná volání jsou popsána dále v tomto modulu.

## <a name="iscrosspagepostback"></a>IsCrossPagePostBack

Tato vlastnost jen pro čtení vrátí **hodnotu true** , pokud je stránka součástí postbacku mezi stránkami. Zpětná volání na více stránek se týkají později v tomto modulu.

## <a name="items"></a>Items

Vrátí odkaz na instanci IDictionary, která obsahuje všechny objekty uložené v kontextu stránky. Do tohoto objektu IDictionary můžete přidat položky, které budou k dispozici během celé životnosti kontextu.

## <a name="maintainscrollpositiononpostback"></a>MaintainScrollPositionOnPostBack

Tato vlastnost určuje, zda ASP.NET emituje jazyk JavaScript, který udržuje pozici posunutí stránek v prohlížeči po vykonání zpětného volání. (Podrobnosti této vlastnosti byly popsány dříve v tomto modulu.)

## <a name="master"></a>Master

Tato vlastnost jen pro čtení vrací odkaz na instanci MasterPage pro stránku, na kterou se používá hlavní stránka.

## <a name="masterpagefile"></a>MasterPageFile

Získá nebo nastaví název souboru hlavní stránky pro stránku. Tato vlastnost může být nastavena pouze v metodě předinit.

## <a name="maxpagestatefieldlength"></a>MaxPageStateFieldLength

Tato vlastnost získá nebo nastaví maximální délku stavu stránek v bajtech. Pokud je vlastnost nastavena na kladné číslo, stav zobrazení stránky bude rozdělen do několika skrytých polí tak, aby nepřevyšuje počet zadaných bajtů. Pokud je vlastnost záporné číslo, stav zobrazení nebude rozdělen do bloků.

## <a name="pageadapter"></a>PageAdapter

Vrátí odkaz na objekt PageAdapter, který upravuje stránku pro požadujícího prohlížeče.

## <a name="previouspage"></a>PreviousPage

Vrátí odkaz na předchozí stránku v případech serveru. přenos nebo zpětné odeslání mezi stránkami.

## <a name="skinid"></a>SkinID

Určuje vzhled ASP.NET 2,0, který se má použít pro stránku.

## <a name="stylesheettheme"></a>StyleSheetTheme

Tato vlastnost získá nebo nastaví šablonu stylů, která je použita na stránku.

## <a name="templatecontrol"></a>Třída TemplateControl

Vrátí odkaz na obsahující ovládací prvek stránky.

## <a name="theme"></a>Použit

Získá nebo nastaví název motivu ASP.NET 2,0, který se na stránku aplikuje. Tato hodnota musí být nastavena před metodou předinicializace.

## <a name="title"></a>Název

Tato vlastnost získá nebo nastaví název stránky získaný z hlavičky stránky.

## <a name="viewstateencryptionmode"></a>ViewStateEncryptionMode

Získá nebo nastaví ViewStateEncryptionMode stránky. Přečtěte si podrobnou diskuzi o této vlastnosti dříve v tomto modulu.

## <a name="new-protected-properties-of-the-page-class"></a>Nové chráněné vlastnosti třídy Page

Níže jsou uvedené nové chráněné vlastnosti třídy Page v ASP.NET 2,0.

## <a name="adapter"></a>Adaptér

Vrátí odkaz na ControlAdapter, který vykresluje stránku na zařízení, které si ho vyžádalo.

## <a name="asyncmode"></a>AsyncMode

Tato vlastnost označuje, zda je stránka zpracovávána asynchronně. Je určena pro použití modulem runtime a nikoli přímo v kódu.

## <a name="clientidseparator"></a>ClientIDSeparator

Tato vlastnost vrátí znak používaný jako oddělovač při vytváření jedinečných ID klientů pro ovládací prvky. Je určena pro použití modulem runtime a nikoli přímo v kódu.

## <a name="pagestatepersister"></a>PageStatePersister

Tato vlastnost vrátí objekt Třída PageStatePersister pro stránku. Tato vlastnost je primárně používána vývojáři ovládacího prvku ASP.NET.

## <a name="uniquefilepathsuffix"></a>UniqueFilePathSuffix

Tato vlastnost vrací jedinečnou příponu, která je připojena k cestě k souboru pro ukládání prohlížečů do mezipaměti. Výchozí hodnota je \_\_ufps = a číslo na 6 číslic.

## <a name="new-public-methods-for-the-page-class"></a>Nové veřejné metody pro třídu Page

Následující veřejné metody jsou pro třídu stránky v ASP.NET 2,0 nové.

## <a name="addonprerendercompleteasync"></a>AddOnPreRenderCompleteAsync

Tato metoda registruje delegáty obslužné rutiny události pro provádění asynchronní stránky. Asynchronní stránky jsou popsány dále v tomto modulu.

## <a name="applystylesheetskin"></a>ApplyStyleSheetSkin

Aplikuje vlastnosti v šabloně stylů Pages na stránku.

## <a name="executeregisteredasynctasks"></a>ExecuteRegisteredAsyncTasks

Tato metoda je asynchronní úlohou.

### <a name="getvalidators"></a>Getvalidátory

Vrátí kolekci validátorů pro zadanou skupinu ověřování nebo výchozí skupinu ověření, pokud není zadána žádná.

## <a name="registerasynctask"></a>RegisterAsyncTask

Tato metoda registruje novou asynchronní úlohu. Na asynchronní stránky se pojednává později v tomto modulu.

## <a name="registerrequirescontrolstate"></a>RegisterRequiresControlState

Tato metoda oznamuje ASP.NET, že je nutné zachovat stav ovládacího prvku stránky.

## <a name="registerrequiresviewstateencryption"></a>Metoda RegisterRequiresViewStateEncryption

Tato metoda oznamuje ASP.NET, že vlastnost ViewState pro stránky vyžaduje šifrování.

## <a name="resolveclienturl"></a>ResolveClientUrl

Vrátí relativní adresu URL, která se dá použít pro požadavky klientů na Image atd.

## <a name="setfocus"></a>SetFocus

Tato metoda nastaví fokus na ovládací prvek, který je určen při počátečním načtení stránky.

## <a name="unregisterrequirescontrolstate"></a>UnregisterRequiresControlState

Tato metoda zruší registraci ovládacího prvku, který je předán, protože již nevyžaduje trvalé zachování stavu ovládacího prvku.

## <a name="changes-to-the-page-lifecycle"></a>Změny životního cyklu stránky

Životní cyklus stránky v ASP.NET 2,0 se významně nezměnil, ale existují některé nové metody, o kterých byste měli vědět. Životní cyklus stránky ASP.NET 2,0 je popsaný níže.

## <a name="preinit-new-in-aspnet-20"></a>Předinicializace (novinka v ASP.NET 2,0)

Událost před inicializací je nejstarší fáze životního cyklu, ke které má vývojář přístup. Přidání této události umožňuje programově změnit motivy ASP.NET 2,0, stránky předlohy, vlastnosti přístupu pro profil ASP.NET 2,0 atd. Pokud jste ve stavu zpětného odeslání, je důležité si uvědomit, že se na ovládací prvky v tomto okamžiku v životním cyklu ještě nepoužila vlastnost ViewState. Proto pokud vývojář změní vlastnost ovládacího prvku v této fázi, bude pravděpodobně přepsán později v životním cyklu stránky.

## <a name="init"></a>Init

Událost init se nezměnila z ASP.NET 1. x. Tady byste chtěli číst nebo inicializovat vlastnosti ovládacích prvků na stránce. V této fázi jsou na stránce již aplikovány stránky předlohy, motivy atd.

## <a name="initcomplete-new-in-20"></a>InitComplete (novinka v 2,0)

Událost InitComplete je volána na konci inicializační fáze stránky. V tomto okamžiku životního cyklu můžete přistupovat k ovládacím prvkům na stránce, ale jejich stav ještě není naplněný.

## <a name="preload-new-in-20"></a>Předběžné načtení (novinka v 2,0)

Tato událost se volá po použití všech dat postbacku a těsně před\_načtení stránky.

## <a name="load"></a>Načtení

Událost Load se nezměnila z ASP.NET 1. x.

## <a name="loadcomplete-new-in-20"></a>LoadComplete (novinka v 2,0)

Událost LoadComplete je poslední událost ve fázi načítání stránek. V této fázi se na stránku nastavila všechna data zpětného odeslání a ViewState.

## <a name="prerender"></a>Vykreslení

Chcete-li, aby byl vlastnost ViewState správně udržována pro ovládací prvky, které jsou přidány na stránku dynamicky, je událost PreRender poslední příležitostí k jejich přidání.

## <a name="prerendercomplete-new-in-20"></a>PreRenderComplete (novinka v 2,0)

Ve fázi PreRenderComplete byly na stránku přidány všechny ovládací prvky a stránka je připravena k vykreslení. Událost PreRenderComplete je poslední událost aktivovaná před tím, než se uloží vlastnosti stránky.

## <a name="savestatecomplete-new-in-20"></a>SaveStateComplete (novinka v 2,0)

Událost SaveStateComplete se volá hned po uložení veškerého zobrazení stránky a stavu ovládacího prvku. Toto je poslední událost před tím, než se stránka ve skutečnosti vykreslí do prohlížeče.

## <a name="render"></a>Vykreslování

Metoda Render se od ASP.NET 1. x nezměnila. Zde je místo, kde se inicializuje HtmlTextWriter a stránka se vykreslí do prohlížeče.

## <a name="cross-page-postback-in-aspnet-20"></a>Zpětná vazba mezi stránkami v ASP.NET 2,0

V ASP.NET 1. x byly pro odeslání na stejnou stránku požadovány zpětné odeslání. Postbacky mezi stránkami se nepovolily. ASP.NET 2,0 přidává možnost zpětného odeslání na jinou stránku prostřednictvím rozhraní IButtonControl. Jakýkoli ovládací prvek, který implementuje nové rozhraní IButtonControl (Button, LinkButton a obrázkové), může využít tuto novou funkci prostřednictvím atributu PostBackUrl. Následující kód ukazuje ovládací prvek tlačítko, který odesílá zpět na druhou stránku.

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample5.aspx)]

Po odeslání stránky zpět je stránka, která iniciuje postback, přístupná prostřednictvím vlastnosti PreviousPage na druhé stránce. Tato funkce je implementována prostřednictvím nového WebForm\_DoPostBackWithOptions funkce na straně klienta, kterou ASP.NET 2,0 vykresluje na stránku, když ovládací prvek odešle zpět na jinou stránku. Tuto funkci JavaScriptu poskytuje Nová obslužná rutina WebResource. axd, která pro klienta generuje skript.

Níže uvedené video je návodem k postbacku mezi stránkami.

![](the-asp-net-2-0-page-model/_static/image2.png)

[Otevření videa na celé obrazovce](the-asp-net-2-0-page-model/_static/xpage1.wmv)

## <a name="more-details-on-cross-page-postbacks"></a>Další podrobnosti o Postbackech mezi stránkami

### <a name="viewstate"></a>Vlastnosti

Mohli jste se už dotazovat na to, co se děje, od první stránky ve scénáři zpětného odeslání mezi stránkami. Po všech případech jakýkoli ovládací prvek, který neimplementuje IPostBackDataHandler, uchová svůj stav prostřednictvím vlastnosti ViewState, takže pokud chcete mít přístup k vlastnostem tohoto ovládacího prvku na druhé stránce zpětného vysílání mezi stránkami, musíte mít přístup k vlastnosti ViewState stránky. ASP.NET 2,0 se postará o tento scénář pomocí nového skrytého pole na druhé stránce s názvem \_\_PREVIOUSPAGE. Pole \_\_PREVIOUSPAGE formuláře obsahuje vlastnost ViewState pro první stránku, takže můžete mít přístup k vlastnostem všech ovládacích prvků na druhé stránce.

### <a name="circumventing-findcontrol"></a>Obejití FindControl

V podrobném návodu k postbacku mezi stránkami jsem použil (a) metodu FindControl, která na první stránce získá odkaz na ovládací prvek TextBox. Tato metoda funguje dobře pro tento účel, ale FindControl je nákladná a vyžaduje zápis dalšího kódu. Naštěstí ASP.NET 2,0 poskytuje alternativu k FindControl pro tento účel, která bude fungovat v mnoha scénářích. Direktiva PreviousPageType vám umožňuje mít na předchozí stránce odkaz silného typu pomocí atributu TypeName nebo VirtualPath. Atribut TypeName umožňuje zadat typ předchozí stránky, zatímco atribut VirtualPath umožňuje odkazování na předchozí stránku pomocí virtuální cesty. Po nastavení direktivy PreviousPageType je nutné vystavit ovládací prvky atd., ke kterým chcete přístup udělit pomocí veřejných vlastností.

## <a name="lab-1-cross-page-postback"></a>Testovací zpětné volání mezi stránkami laboratoře 1

V tomto testovacím prostředí vytvoříte aplikaci, která bude používat novou funkci zpětného volání na více stránkách ASP.NET 2,0.

1. Otevřete Visual Studio 2005 a vytvořte nový web ASP.NET.
2. Přidejte nový webformu s názvem Page2. aspx.
3. Otevřete default. aspx v zobrazení Návrh a přidejte ovládací prvek tlačítko a ovládací prvek TextBox. 

    1. Poskytněte ovládacímu prvku tlačítko ID **submitButton** a textové pole určuje ID **uživatelského jména**.
    2. Nastavte vlastnost PostBackUrl tlačítka na Page2. aspx.
4. Otevřete Page2. aspx ve zdrojovém zobrazení.
5. Přidejte direktivu @ PreviousPageType, jak je znázorněno níže:
6. Přidejte následující kód na stránku\_načtení kódu Page2. aspx s kódem na pozadí: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample6.cs)]
7. Sestavte projekt kliknutím na sestavit v nabídce sestavení.
8. Do kódu na pozadí pro default. aspx přidejte následující kód: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample7.cs)]
9. Změňte stránku\_načíst v Page2. aspx následujícím způsobem: 

    [!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample8.cs)]
10. Sestavte projekt.
11. Spusťte projekt.
12. Do textového pole zadejte své jméno a klikněte na tlačítko.
13. Jaký je výsledek?

## <a name="asynchronous-pages-in-aspnet-20"></a>Asynchronní stránky v ASP.NET 2,0

Mnohé problémy s kolize v ASP.NET způsobuje latence vnějších volání (například webové služby nebo volání databáze), latence v/v souboru atd. Když se v rámci aplikace ASP.NET vytvoří požadavek, ASP.NET použije jedno z jeho pracovních vláken ke zpracování tohoto požadavku. Tento požadavek je vlastníkem tohoto vlákna, dokud není požadavek dokončen a odpověď byla odeslána. ASP.NET 2,0 se snaží vyřešit problémy latence s těmito typy problémů přidáním možnosti pro asynchronní spouštění stránek. To znamená, že může pracovní vlákno zahájit požadavek a pak předat další spuštění jinému vláknu, čímž se rychle vrátí do dostupného fondu vláken. Po dokončení souboru v/v se z fondu vláken získá nové vlákno, aby se žádost dokončila.

Prvním krokem při provádění asynchronního zpracování stránky je nastavení atributu **Async** direktivy stránky, například:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample9.aspx)]

Tento atribut dává ASP.NET pokyn k implementaci IHttpAsyncHandler pro stránku.

Dalším krokem je zavolat metodu AddOnPreRenderCompleteAsync v místě v životním cyklu stránky před provedením operace PreRender. (Tato metoda se obvykle volá při načtení stránky\_.) Metoda AddOnPreRenderCompleteAsync přijímá dva parametry; BeginEventHandler a EndEventHandler. BeginEventHandler vrací IAsyncResult, který je poté předán jako parametr do EndEventHandler.

Následující video je názorný na asynchronní požadavek stránky.

![](the-asp-net-2-0-page-model/_static/image3.png)

[Otevření videa na celé obrazovce](the-asp-net-2-0-page-model/_static/async1.wmv)

> [!NOTE]
> Asynchronní stránka se nevykresluje do prohlížeče, dokud se EndEventHandler nedokončí. Žádné pochybnosti, ale vývojáři si budou považovat asynchronní požadavky za podobné asynchronním zpětnému volání. Je důležité si uvědomit, že nejsou. Výhodou pro asynchronní požadavky je, aby první pracovní vlákno bylo vráceno do fondu vláken, aby bylo možné obsluhovat nové požadavky, čímž se snížila kolize z důvodu vstupně-výstupních operací atd.

## <a name="script-callbacks-in-aspnet-20"></a>Zpětná volání skriptů v ASP.NET 2,0

Vývojáři webu vždy hledali způsob, jak zabránit blikání spojené s zpětným voláním. V ASP.NET 1. x byla SmartNavigation Nejběžnější metodou pro zamezení blikání, ale SmartNavigation způsobila problémy pro některé vývojáře z důvodu složitosti implementace na straně klienta. ASP.NET 2,0 řeší tento problém pomocí zpětných volání skriptů. Zpětná volání skriptu využívají XMLHttp k vytváření požadavků na webový server prostřednictvím JavaScriptu. Požadavek XMLHttp vrátí data XML, která lze následně manipulovat prostřednictvím modelu DOM prohlížeče. Kód XMLHttp je od uživatele skrytý pomocí nové obslužné rutiny WebResource. axd.

Pro konfiguraci zpětného volání skriptu v ASP.NET 2,0 je nutné provést několik kroků.

## <a name="step-1--implement-the-icallbackeventhandler-interface"></a>Krok 1: implementace rozhraní rozhraní ICallbackEventHandler

Aby ASP.NET rozpoznal vaši stránku jako účastnící se zpětného volání skriptu, je nutné implementovat rozhraní rozhraní ICallbackEventHandler. To můžete provést v souboru s kódem na pozadí, například takto:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample10.cs)]

Můžete to také provést pomocí direktivy @ implementers, například:

[!code-aspx[Main](the-asp-net-2-0-page-model/samples/sample11.aspx)]

Direktiva @ Implements se obvykle používá při použití vloženého kódu ASP.NET.

## <a name="step-2--call-getcallbackeventreference"></a>Krok 2: volání GetCallbackEventReference

Jak bylo zmíněno dříve, volání XMLHttp je zapouzdřeno v obslužné rutině WebResource. axd. Po vykreslení stránky ASP.NET přidá volání do WebForm\_DoCallback, skript klienta, který je poskytován pomocí WebResource. axd. Funkce WebForm\_DoCallback nahrazuje funkci \_\_doPostBack pro zpětné volání. Nezapomeňte, že \_\_doPostBack programově odešle formulář na stránce. Ve scénáři zpětného volání chcete zabránit zpětnému volání, takže \_\_doPostBack nebude stačit.

> [!NOTE]
> \_\_doPostBack se pořád vykresluje na stránku ve scénáři zpětného volání klientského skriptu. Nepoužívá se však pro zpětné volání.

Argumenty pro WebForm\_DoCallback funkce na straně klienta jsou k dispozici prostřednictvím GetCallbackEventReference funkce na straně serveru, která by se normálně volala v zatížení stránky\_. Typické volání GetCallbackEventReference může vypadat takto:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample12.cs)]

> [!NOTE]
> V tomto případě je cm instancí ClientScriptManager. Na třídu ClientScriptManager se bude vztahovat později v tomto modulu.

Existuje několik přetížených verzí GetCallbackEventReference. V tomto případě jsou argumenty následující:

`this`

Odkaz na ovládací prvek, ve kterém je volána metoda GetCallbackEventReference. V tomto případě se jedná o stránku samotnou.

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample13.js)]

Řetězcový argument, který bude předán z kódu na straně klienta k události na straně serveru. V tomto případě im pošle hodnotu rozevíracího seznamu s názvem ddlCompany.

`ShowCompanyName`

Název funkce na straně klienta, která přijme vrácenou hodnotu (jako řetězec) z události zpětného volání na straně serveru. Tato funkce bude volána pouze v případě, že zpětné volání na straně serveru je úspěšné. Z důvodu odolnosti se obecně doporučuje použít přetíženou verzi GetCallbackEventReference, která přijímá další řetězcový argument, který určuje název funkce na straně klienta, která se má provést v případě chyby.

`null`

Řetězec představující funkci na straně klienta, kterou inicioval před zpětným voláním na server. V takovém případě žádný takový skript neexistuje, takže argument má hodnotu null.

`true`

Logická hodnota určující, zda se má asynchronní volání provádět asynchronně.

Volání WebForm\_DoCallback na klientovi budou tyto argumenty předat. Proto při vykreslování této stránky na klientovi bude tento kód vypadat takto:

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample14.js)]

Všimněte si, že signatura funkce na klientovi je trochu odlišná. Funkce na straně klienta předává 5 řetězců a logickou hodnotu. Další řetězec (který je ve výše uvedeném příkladu null) obsahuje funkci na straně klienta, která bude zpracovávat chyby z zpětného volání na straně serveru.

## <a name="step-3--hook-the-client-side-control-event"></a>Krok 3: zavěšení události ovládacího prvku na straně klienta

Všimněte si, že návratová hodnota GetCallbackEventReference výše byla přiřazena proměnné řetězce. Tento řetězec slouží k zavěšení události na straně klienta pro ovládací prvek, který iniciuje zpětné volání. V tomto příkladu je zpětné volání iniciováno rozevíracím seznamem na stránce, takže chci připojit událost při *změně* .

Chcete-li připojit událost na straně klienta, jednoduše přidejte obslužnou rutinu do značky na straně klienta následujícím způsobem:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample15.cs)]

Odvolání tohoto *cbRef* je návratovou hodnotou z volání GetCallbackEventReference. Obsahuje volání do WebForm\_DoCallback, které bylo zobrazeno výše.

## <a name="step-4--register-the-client-side-script"></a>Krok 4: registrace skriptu na straně klienta

Odvolání volání GetCallbackEventReference určilo, že skript na straně klienta s názvem **ShowCompanyName** by se spustil při úspěšném zpětném volání na straně serveru. Tento skript musí být přidán na stránku pomocí instance ClientScriptManager. (Třída ClientScriptManager bude popsána dále v tomto modulu.) To uděláte takto:

[!code-javascript[Main](the-asp-net-2-0-page-model/samples/sample16.js)]

## <a name="step-5--call-the-methods-of-the-icallbackeventhandler-interface"></a>Krok 5: volání metod rozhraní rozhraní ICallbackEventHandler

Rozhraní ICallbackEventHandler obsahuje dvě metody, které je třeba implementovat ve svém kódu. Jsou **RaiseCallbackEvent** a **GetCallbackEvent**.

**RaiseCallbackEvent** přebírá řetězec jako argument a nevrací žádnou hodnotu. Řetězcový argument se předává z volání WebForm na straně klienta\_DoCallback. V tomto případě je tato hodnota atributem *Value* rozevíracího seznamu s názvem ddlCompany. Váš kód na straně serveru by měl být umístěn do metody RaiseCallbackEvent. Například pokud zpětné volání vytváří WebRequest proti externímu zdroji, měl by být tento kód umístěn v RaiseCallbackEvent.

**GetCallbackEvent** zodpovídá za zpracování vrácení zpětného volání klientovi. Nepřijímá žádné argumenty a vrací řetězec. Řetězec, který vrátí, bude předán jako argument funkce na straně klienta, v tomto případě *ShowCompanyName*.

Po dokončení výše uvedených kroků jste připraveni provést zpětné volání skriptu v ASP.NET 2,0.

![](the-asp-net-2-0-page-model/_static/image4.png)

[Otevření videa na celé obrazovce](the-asp-net-2-0-page-model/_static/callback1.wmv)

Zpětná volání skriptů v ASP.NET jsou podporována v jakémkoli prohlížeči, který podporuje vytváření volání XMLHttp. To zahrnuje všechny moderní prohlížeče používané dnes. Internet Explorer používá objekt ADO ActiveX, zatímco další moderní prohlížeče (včetně nadcházejících IE 7) používají vnitřní objekt XMLHttp. Chcete-li programově zjistit, zda prohlížeč podporuje zpětná volání, můžete použít vlastnost **Request. browser. SupportCallback** . Tato vlastnost vrátí **hodnotu true** , pokud žádající klient podporuje zpětná volání skriptů.

## <a name="working-with-client-script-in-aspnet-20"></a>Práce s klientským skriptem v ASP.NET 2,0

Klientské skripty v ASP.NET 2,0 jsou spravovány prostřednictvím použití třídy ClientScriptManager. Třída ClientScriptManager sleduje klientské skripty pomocí typu a názvu. Tím se zabrání programovému vložení stejného skriptu na stránku více než jednou.

> [!NOTE]
> Po úspěšné registraci skriptu na stránce se při dalším pokusu o registraci stejného skriptu jednoduše zaznamená, že se skript nebude registrovat podruhé. Nepřidaly se žádné duplicitní skripty a nedochází k žádné výjimce. Aby nedocházelo k zbytečnému výpočtu, existují metody, které lze použít k určení, zda je skript již zaregistrován, takže se nepokusíte o jeho registraci více než jednou.

Metody ClientScriptManager by měly být obeznámené se všemi současnými vývojáři ASP.NET:

## <a name="registerclientscriptblock"></a>RegisterClientScriptBlock

Tato metoda přidá skript do horní části vykreslené stránky. To je užitečné, pokud chcete přidat funkce, které budou explicitně volány na straně klienta.

Existují dvě přetížené verze této metody. Existují tři ze čtyř argumentů, které jsou mezi nimi společné. Jsou to tyto:

`type (string)`

Argument ***typu*** identifikuje typ skriptu. Obecně je vhodné použít typ stránky (to. GetType ()) pro typ.

`key (string)`

Argument ***Key*** je uživatelsky definovaný klíč pro skript. To by mělo být pro každý skript jedinečné. Pokud se pokusíte přidat skript se stejným klíčem a typem již přidaného skriptu, nebude přidán.

`script (string)`

Argument ***Script*** je řetězec obsahující vlastní skript, který se má přidat. Doporučuje se použít StringBuilder k vytvoření skriptu a potom použít metodu ToString () na StringBuilder k přiřazení argumentu ***skriptu*** .

Použijete-li přetížené RegisterClientScriptBlock, které přebírají pouze tři argumenty, musíte do skriptu zahrnout prvky skriptu (&lt;skriptu&gt; a &lt;/Script&gt;).

Můžete se rozhodnout použít přetížení RegisterClientScriptBlock, které přijímá čtvrtý argument. Čtvrtý argument je logická hodnota, která určuje, zda má ASP.NET přidat prvky skriptu. Pokud má tento argument **hodnotu true**, skript by neměl explicitně zahrnovat prvky skriptu.

Pomocí metody IsClientScriptBlockRegistered můžete zjistit, jestli už je skript zaregistrovaný. To vám umožní vyhnout se pokusu o opětovné registraci skriptu, který už je zaregistrovaný.

### <a name="registerclientscriptinclude-new-in-20"></a>RegisterClientScriptInclude (novinka v 2,0)

Značka RegisterClientScriptInclude vytvoří blok skriptu, který odkazuje na externí soubor skriptu. Má dvě přetížení. Jedna vezme klíč a adresu URL. Druhý přidá třetí argument určující typ.

Například následující kód vygeneruje blok skriptu, který odkazuje na jsfunctions. js v kořenu složky Scripts v aplikaci:

[!code-csharp[Main](the-asp-net-2-0-page-model/samples/sample17.cs)]

Tento kód na vykreslené stránce vytvoří následující kód:

[!code-html[Main](the-asp-net-2-0-page-model/samples/sample18.html)]

> [!NOTE]
> Blok skriptu se vykreslí v dolní části stránky.

Pomocí metody IsClientScriptIncludeRegistered můžete zjistit, jestli už je skript zaregistrovaný. To vám umožní vyhnout se pokusu o opětovné registraci skriptu.

## <a name="registerstartupscript"></a>RegisterStartupScript

Metoda RegisterStartupScript přebírá stejné argumenty jako metoda RegisterClientScriptBlock. Skript zaregistrovaný v RegisterStartupScript se spustí po načtení stránky, ale před událostí načtení na straně klienta. V 1. X se skripty zaregistrované v RegisterStartupScript umístily těsně před uzavírací &lt;&gt; značka, zatímco se skripty zaregistrované v RegisterClientScriptBlock umístily hned po počáteční značce &lt;formuláře&gt;. V ASP.NET 2,0 se obě umístí hned před uzavírací &lt;&gt;er značka.

> [!NOTE]
> Pokud zaregistrujete funkci s RegisterStartupScript, tato funkce se nespustí, dokud ji explicitně nebudete volat v kódu na straně klienta.

Použijte metodu IsStartupScriptRegistered k určení, zda již byl skript zaregistrován, a vyhněte se pokusu o opětovné registraci skriptu.

## <a name="other-clientscriptmanager-methods"></a>Jiné metody ClientScriptManager

Zde jsou některé z dalších užitečných metod třídy ClientScriptManager.

|  <strong>GetCallbackEventReference</strong>   |                                                 Viz zpětná volání skriptů dříve v tomto modulu.                                                 |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
|  <strong>GetPostBackClientHyperlink</strong>  |                Získá referenci jazyka JavaScript (JavaScript:&lt;volání&gt;), které lze použít k odeslání zpět z události na straně klienta.                 |
|  <strong>GetPostBackEventReference</strong>   |                                   Načte řetězec, který lze použít k zahájení příspěvku zpět od klienta.                                    |
|      <strong>GetWebResourceUrl</strong>       | Vrátí adresu URL prostředku, který je vložen do sestavení. Musí se používat ve spojení s <strong>RegisterClientScriptResource</strong>. |
| <strong>RegisterClientScriptResource</strong> |     Zaregistruje webový prostředek se stránkou. Jedná se o prostředky vložené v sestavení a zpracovávané pomocí nové obslužné rutiny WebResource. axd.      |
|     <strong>RegisterHiddenField</strong>      |                                                 Zaregistruje skryté pole formuláře se stránkou.                                                 |
|  <strong>RegisterOnSubmitStatement</strong>   |                                  Registruje kód na straně klienta, který se spustí při odeslání formuláře HTML.                                   |

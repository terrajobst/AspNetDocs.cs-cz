---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-debugging-capabilities
title: Principy funkcí ladění v ASP.NET AJAX | Microsoft Docs
author: scottcate
description: Možnost ladění kódu je dovedností, že každý vývojář by měl mít v Arsenal bez ohledu na technologii, kterou používají. I když je mnoho vývojářů...
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 7f9380c6-19f7-4c82-a019-916ec6dffc9c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-debugging-capabilities
msc.type: authoredcontent
ms.openlocfilehash: 08ced380f3551407d757524dbc84b5feeeb5482b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74601443"
---
# <a name="understanding-aspnet-ajax-debugging-capabilities"></a>Principy a možnosti ladění pomocí technologie ASP.NET AJAX

[Scott Cate](https://github.com/scottcate)

[Stáhnout PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial06_Debugging_MS_Ajax_Applications_cs.pdf)

> Možnost ladění kódu je dovedností, že každý vývojář by měl mít v Arsenal bez ohledu na technologii, kterou používají. I když je mnoho vývojářů zvyklé použít Visual Studio .NET nebo Web Developer Express k ladění aplikací ASP.NET, které používají C# VB.NET nebo kód, některé nevědí, že je to také extrémně užitečné pro ladění kódu na straně klienta, jako je například JavaScript. Stejný typ technik, který se používá pro ladění aplikací .NET, je možné použít také pro aplikace podporující AJAX a konkrétnější aplikace ASP.NET AJAX.

## <a name="debugging-aspnet-ajax-applications"></a>Ladění aplikací AJAX v ASP.NET

Dan Wahlin

Možnost ladění kódu je dovedností, že každý vývojář by měl mít v Arsenal bez ohledu na technologii, kterou používají. Je to bez toho, že porozumění různým možnostem ladění, které jsou k dispozici, může ušetřit obrovské množství času v projektu a možná i několik souvisejícím problémům správou. I když je mnoho vývojářů zvyklé použít Visual Studio .NET nebo Web Developer Express k ladění aplikací ASP.NET, které používají C# VB.NET nebo kód, některé nevědí, že je to také extrémně užitečné pro ladění kódu na straně klienta, jako je například JavaScript. Stejný typ technik, který se používá pro ladění aplikací .NET, je možné použít také pro aplikace podporující AJAX a konkrétnější aplikace ASP.NET AJAX.

V tomto článku se dozvíte, jak se dá použít Visual Studio 2008 a několik dalších nástrojů k ladění aplikací ASP.NET AJAX pro rychlé vyhledání chyb a dalších problémů. Tato diskuze bude obsahovat informace o tom, jak povolit Internet Explorer 6 nebo vyšší pro ladění, pomocí sady Visual Studio 2008 a Průzkumníka skriptů Procházet kód a používat jiné bezplatné nástroje, jako je například Pomocník pro vývoj webu. Naučíte se také, jak ladit aplikace ASP.NET AJAX v aplikaci Firefox pomocí rozšíření s názvem Firebug, které umožňuje krokovat kód JavaScriptu přímo v prohlížeči bez jakýchkoli dalších nástrojů. Nakonec se zavedete do tříd v knihovně ASP.NET AJAX, která může pomáhat s různými úlohami ladění, jako jsou například trasování a příkazy kontrolního výrazu kódu.

Předtím, než se pokusíte ladit stránky zobrazené v aplikaci Internet Explorer, je třeba provést několik základních kroků, abyste je mohli povolit pro ladění. Pojďme se podívat na některé základní požadavky na instalaci, které je potřeba provést, aby bylo možné začít.

## <a name="configuring-internet-explorer-for-debugging"></a>Konfigurace aplikace Internet Explorer pro ladění

Většina lidí se zajímá o problémech s JavaScriptem na webu zobrazeném v Internet Exploreru. V tomto faktě průměrný uživatel nedokázal ani zjistit, co dělat, když se jim zobrazila chybová zpráva. V důsledku toho jsou možnosti ladění ve výchozím nastavení v prohlížeči vypnuté. Je však velmi jednoduché zapnout ladění a umístit je, aby se používaly při vývoji nových aplikací AJAX.

Chcete-li povolit funkci ladění, přejděte do části nástroje Možnosti Internetu v nabídce Internet Explorer a vyberte kartu Upřesnit. V části procházení se ujistěte, že nejsou zaškrtnuté následující položky:

- Zakázat ladění skriptů (Internet Explorer)
- Zakázat ladění skriptů (jiné)

I když se snažíte ladit aplikaci, i když se to nepožaduje, budete pravděpodobně chtít, aby se chyby JavaScriptu na stránce hned zobrazovaly a zjevně viděli. Zaškrtnutím políčka Zobrazit oznámení o každé chybě skriptu můžete vynutit, aby se všechny chyby zobrazily v okně se zprávou. I když je to skvělý způsob, jak zapnout, když vyvíjíte aplikaci, může se rychle stát obtěžující, pokud jste perusing jenom jiné weby, protože vaše pravděpodobnost výskytu chyb JavaScriptu je poměrně dobrá.

Obrázek 1 ukazuje, co má dialogové okno Upřesnit v aplikaci Internet Explorer zobrazit po správném nakonfigurování pro ladění.

[![konfiguraci aplikace Internet Explorer pro ladění.](understanding-asp-net-ajax-debugging-capabilities/_static/image2.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image1.png)

**Obrázek 1**: Konfigurace aplikace Internet Explorer pro ladění.  ([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-debugging-capabilities/_static/image3.png))

Po zapnutí ladění se v nabídce zobrazení s názvem ladicí program skriptu zobrazí nová položka nabídky. K dispozici jsou dvě možnosti, včetně příkazu otevřít a přerušit u dalšího příkazu. Když je vybrána možnost otevřít, zobrazí se výzva k ladění stránky v aplikaci Visual Studio 2008 (Všimněte si, že Visual Web Developer Express lze také použít pro ladění). Pokud je aktuálně spuštěna aplikace Visual Studio .NET, můžete zvolit použití této instance nebo k vytvoření nové instance. Když je vybrána možnost přerušení u dalšího příkazu, zobrazí se výzva k ladění stránky při spuštění kódu jazyka JavaScript. Pokud se JavaScriptový kód spustí v události načtení stránky, můžete aktualizovat stránku, aby se aktivovala relace ladění. Pokud se po kliknutí na tlačítko spustí kód jazyka JavaScript, ladicí program se spustí hned po kliknutí na tlačítko.

> [!NOTE]
> Pokud používáte systém Windows Vista s povoleným uživatelským Access Control (UAC) a máte sadu Visual Studio 2008 nastavenou na spouštění jako správce, Visual Studio se při zobrazení výzvy k připojení nepřipojí k procesu. Chcete-li tento problém obejít, spusťte nejprve aplikaci Visual Studio a pomocí této instance proveďte ladění.

I když v další části ukážeme, jak ladit stránku ASP.NET AJAX přímo ze sady Visual Studio 2008, je možnost použití ladicího programu skriptů Internet Exploreru užitečná v případě, že je stránka už otevřená a Vy byste ji chtěli úplně zkontrolovat.

## <a name="debugging-with-visual-studio-2008"></a>Ladění pomocí sady Visual Studio 2008

Visual Studio 2008 poskytuje funkce ladění, které vývojáři po celém světě spoléhají na to, že budou ladit aplikace .NET. Integrovaný ladicí program umožňuje procházet kód, zobrazovat data objektů, sledovat konkrétní proměnné, monitorovat zásobník volání a mnohem více. Kromě ladění VB.NET nebo C# kódu je ladicí program také užitečný pro ladění aplikací ASP.NET AJAX a umožní krokovat kód JavaScriptu řádek po řádku. Podrobnosti, které následují jako zaměření na techniky, které lze použít k ladění souborů skriptu na straně klienta namísto poskytování jakéhokoli procesu ladění aplikací pomocí sady Visual Studio 2008.

Proces ladění stránky v aplikaci Visual Studio 2008 lze spustit několika různými způsoby. Nejprve můžete použít možnost ladicí program skriptů Internet Exploreru, jak je uvedeno v předchozí části. Tato funkce funguje dobře, když je stránka již načtena v prohlížeči a chcete spustit ladění. Případně můžete kliknout pravým tlačítkem na stránku ASPX v Průzkumník řešení a v nabídce vybrat nastavit jako úvodní stránku. Pokud jste zvyklí ladit stránky ASP.NET, pravděpodobně jste to udělali dříve. Po stisknutí klávesy F5 se stránka může ladit. Nicméně, zatímco můžete obecně nastavit zarážku kdekoli, kde byste chtěli v VB.NET nebo C# v kódu, to znamená, že se při zobrazení další zobrazí vždy případ s JavaScriptem.

*Vložené versus externí skripty*

Ladicí program sady Visual Studio 2008 zpracovává JavaScript vložený na stránce odlišnou od externích souborů JavaScriptu. U externích souborů skriptu můžete soubor otevřít a nastavit zarážku na jakémkoli řádku, který zvolíte. Zarážky lze nastavit kliknutím v oblasti šedého zásobníku vlevo v okně editoru kódu. Když je JavaScript vložen přímo na stránku pomocí značky `<script>`, nastavení zarážky kliknutím na šedou oblast zásobníku není možnost. Pokusy o nastavení zarážky na řádku vloženého skriptu budou mít za následek upozornění, že "Toto není platné umístění pro zarážku".

Tento problém můžete obejít přesunutím kódu do externího souboru. js a odkazem na něj pomocí atributu src &lt;značku&gt; skriptu:

[!code-html[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample1.html)]

Co dělat, když přesunete kód do externího souboru, není možnost nebo vyžaduje více práce, než kolik stojí? I když nemůžete nastavit zarážku pomocí editoru, můžete přidat příkaz ladicího programu přímo do kódu, kde chcete spustit ladění. Můžete také použít třídu sys. Debug dostupnou v knihovně AJAX ASP.NET k vynucení spuštění ladění. Další informace o třídě sys. Debug najdete dále v tomto článku.

Příklad použití klíčového slova `debugger` je zobrazen v seznamu 1. Tento příklad vynutí, aby se ladicí program před voláním funkce Update nastavil na přerušení.

**Výpis 1. Použití klíčového slova ladicího programu pro vynucení přerušení ladicího programu sady Visual Studio .NET.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample2.js)]

Jakmile se objeví příkaz ladicího programu, budete vyzváni k ladění stránky pomocí sady Visual Studio .NET a můžete začít s procházením kódu. V takovém případě může dojít k potížím s přístupem k souborům skriptů knihovny AJAX ASP.NET, které se používají na stránce, takže se podíváme na používání sady Visual Studio. Průzkumník skriptů sítě.

## <a name="using-visual-studio-net-windows-to-debug"></a>Ladění pomocí Windows v prostředí Visual Studio .NET

Po spuštění relace ladění a zahájení procházení kódu pomocí výchozí klávesy F11 se může zobrazit dialogové okno chyby zobrazené v části Obrázek 2, pokud nejsou všechny soubory skriptu použité na stránce otevřené a dostupné pro ladění.

[Pokud není k dispozici žádný zdrojový kód pro ladění, zobrazí se dialogové okno chyby ![.](understanding-asp-net-ajax-debugging-capabilities/_static/image5.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image4.png)

**Obrázek 2**: dialogové okno chyby zobrazené, pokud není k dispozici žádný zdrojový kód pro ladění.  ([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-debugging-capabilities/_static/image6.png))

Toto dialogové okno se zobrazí, protože Visual Studio .NET nezajišťuje, jak získat ke zdrojovému kódu některých skriptů, na které stránka odkazuje. I když to může být poměrně frustrující, existuje jednoduchá oprava. Jakmile spustíte relaci ladění a zaškrtnete zarážku, přejděte do okna ladit Průzkumník skriptů Windows v nabídce Visual Studio 2008 nebo použijte klávesovou zkratku CTRL + ALT + N.

> [!NOTE]
> Pokud nevidíte nabídku Průzkumník skriptů v seznamu, přejděte na **nástroje** > **přizpůsobení** **příkazů** > v nabídce Visual Studio .NET. Vyhledejte položku **ladit** v části kategorie a kliknutím na ni zobrazíte všechny dostupné položky nabídky. V seznamu příkazy přejděte dolů ke skriptu Průzkumník skriptů a přetáhněte ho do nabídky Ladit Windows v předchozí části. Tím se zpřístupní položka nabídky Průzkumníka skriptů při každém spuštění sady Visual Studio .NET.

Průzkumník skriptů lze použít k zobrazení všech skriptů používaných na stránce a jejich otevření v editoru kódu. Jakmile je Průzkumník skriptů otevřený, dvakrát klikněte na právě laděnou stránku. aspx a otevřete ji v okně Editor kódu. Proveďte stejnou akci pro všechny ostatní skripty zobrazené v Průzkumníkovi skriptů. Po otevření všech skriptů v okně Code (kód) můžete stisknout klávesu F11 (a použít jiné klávesové zkratky pro ladění) a krokovat kód. Obrázek 3 ukazuje příklad Průzkumníka skriptů. Zobrazuje seznam aktuálně laděných souborů (demo. aspx) a také dva vlastní skripty a dva skripty dynamicky vložené do stránky pomocí ovládacího prvku ASP.NET AJAX AJAX.

[![Průzkumník skriptů poskytuje snadný přístup ke skriptům používaným na stránce.](understanding-asp-net-ajax-debugging-capabilities/_static/image8.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image7.png)

**Obrázek 3**. Průzkumník skriptů poskytuje snadný přístup ke skriptům, které se používají na stránce.  ([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-debugging-capabilities/_static/image9.png))

Několik dalších oken lze také použít k poskytnutí užitečných informací při procházení kódu na stránce. Například můžete použít okno místní hodnoty k zobrazení hodnot různých proměnných použitých na stránce, okamžité okno pro vyhodnocení konkrétních proměnných nebo podmínek a zobrazení výstupu. Můžete také použít okno výstup k zobrazení příkazů trasování zapsaných pomocí funkce sys. Debug. Trace (která bude popsána dále v tomto článku) nebo funkce Debug. writeln – aplikace Internet Explorer.

Při procházení kódu pomocí ladicího programu můžete ukazatel myši nad proměnnými v kódu zobrazit tak, aby se zobrazila hodnota, která je přiřazena. Ladicí program skriptu občas ale při pohybu mezi danou proměnnou JavaScriptu nezobrazuje cokoli. Chcete-li zobrazit hodnotu, zvýrazněte příkaz nebo proměnnou, kterou se snažíte zobrazit v okně editoru kódu, a potom na ni myší. I když tato technika v každé situaci nefunguje, mnoho času bude možné zobrazit hodnotu bez nutnosti Hledat v jiném ladicím okně, jako je okno místních hodnot.

Video, které demonstruje některé z funkcí, které jsou zde popsané, můžete zobrazit na [http://www.xmlforasp.net](http://www.xmlforasp.net).

## <a name="debugging-with-web-development-helper"></a>Ladění pomocí Pomocníka pro vývoj webu

I když je Visual Studio 2008 (a Visual Web Developer Express 2008) velmi kompatibilní nástroje pro ladění, existují další možnosti, které je možné použít, i když jsou v něm méně světla. Jedním z nejnovějších nástrojů, které mají být vydány, je Pomocník pro vývoj webu. Nikhil Kothari Microsoftu (jeden z klíčových ASP.NET AJAX architektů v Microsoftu) vytvořil tento vynikající nástroj, který může provádět mnoho různých úloh od jednoduchého ladění pro zobrazení požadavků HTTP a odpovědí na zprávy. Pomocníka pro vývoj webů se dá stáhnout na [http://projects.nikhilk.net/Projects/WebDevHelper.aspx](http://projects.nikhilk.net/Projects/WebDevHelper.aspx).

Pomocník pro vývoj webu lze použít přímo v aplikaci Internet Explorer, což usnadňuje použití. Spustí se tak, že v nabídce Internet Exploreru vyberete nástroje pro webový vývoj a pomůcku. Tím se v dolní části prohlížeče otevře nástroj, který je dobrý, protože nemusíte opustit prohlížeč, aby bylo možné provádět několik úloh, jako je požadavek HTTP a protokolování zpráv odpovědí. Obrázek 4 ukazuje, jaký Pomocník pro vývoj webů vypadá jako v akci.

[![Pomocník pro vývoj webu](understanding-asp-net-ajax-debugging-capabilities/_static/image11.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image10.png)

**Obrázek 4**: Pomocník pro vývoj webu ([kliknutím zobrazíte obrázek v plné velikosti](understanding-asp-net-ajax-debugging-capabilities/_static/image12.png))

Pomocník pro vývoj webu není nástroj, který použijete pro krokování kódu podle řádku jako u sady Visual Studio 2008. Dá se ale použít k zobrazení výstupu trasování, ke snadnému vyhodnocení proměnných ve skriptu nebo k prozkoumávání dat uvnitř objektu JSON. Je také velmi užitečné pro zobrazení dat, která jsou předána a ze stránky ASP.NET AJAX a serveru.

Po otevření Pomocníka pro vývoj na webu v aplikaci Internet Explorer musí být ladění skriptů povoleno výběrem skriptu povolit ladění skriptu v nabídce pomocníka webu pro vývoj, jak je uvedeno výše na obrázku 4. To umožňuje nástroji zachytit chyby, ke kterým dochází při spuštění stránky. Umožňuje také snadný přístup ke trasovacím zprávám, které jsou na stránce výstup. Chcete-li zobrazit informace o trasování nebo provést příkazy skriptu pro testování různých funkcí v rámci stránky, vyberte možnost skript zobrazit konzolu skriptu v nabídce Pomocník pro webový vývoj. To poskytuje přístup k příkazovému oknu a jednoduchému okamžitému oknu.

*Zobrazení zpráv trasování a dat objektu JSON*

Příkazové okno lze použít ke spuštění příkazů skriptu nebo dokonce k načtení nebo uložení skriptů používaných k testování různých funkcí na stránce. V příkazovém okně se zobrazují zprávy o trasování nebo ladění vypsané stránkou, která je zobrazena. Výpis 2 ukazuje, jak napsat zprávu trasování pomocí funkce Debug. writeln – v Internet Exploreru.

**Výpis 2. Zápis zprávy trasování na straně klienta pomocí třídy ladění.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample3.js)]

Pokud vlastnost LastName obsahuje hodnotu Novák, Pomocník pro vývoj webu zobrazí v příkazovém okně konzoly skriptu zprávu "jméno osoby: Novák" (za předpokladu, že ladění je povolené). Pomocník pro vývoj webu také přidá objekt debugService na nejvyšší úrovni do stránek, které lze použít k zápisu trasovacích informací nebo k zobrazení obsahu objektů JSON. Výpis 3 ukazuje příklad použití funkce Trace třídy debugService.

**Výpis 3. Použití třídy debugService pomocníka pro vývoj webu k zápisu zprávy trasování.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample4.js)]

Dobrá funkce třídy debugService je, že bude fungovat i v případě, že ladění není povoleno v aplikaci Internet Explorer, což usnadňuje vždy přístup k datům trasování při spuštění pomocníka pro vývoj webu. Když se nástroj nepoužívá pro ladění stránky, příkazy trasování budou ignorovány, protože volání window. debugService vrátí hodnotu false.

Třída debugService také umožňuje zobrazit data objektu JSON pomocí okna inspektora nástroje pro vývoj webu. Výpis 4 vytvoří jednoduchý objekt JSON obsahující data osob. Po vytvoření objektu je provedeno volání funkce kontroly třídy debugService, která umožňuje vizuální kontrolu objektu JSON.

**Výpis 4. Použití funkce debugService. prověřit k zobrazení dat objektu JSON.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample5.js)]

Volání funkce getperson () na stránce nebo v příkazovém podokně způsobí zobrazení dialogového okna inspektoru objektu, jak je znázorněno na obrázku 5. Vlastnosti v rámci objektu lze dynamicky měnit jejich zvýrazněním, změnou hodnoty zobrazeného v textovém poli hodnota a kliknutím na odkaz aktualizace. Použití inspektoru objektu usnadňuje zobrazení dat objektu JSON a experimentování s použitím různých hodnot k vlastnostem.

*Chyby ladění*

Kromě toho, že se mají zobrazit data trasování a objekty JSON, může pomocník pro vývoj webu také pomoci při ladění chyb na stránce. Pokud dojde k chybě, zobrazí se výzva k pokračování na další řádek kódu nebo ladění skriptu (viz obrázek 6). Dialogové okno chyba skriptu zobrazuje kompletní zásobník volání a čísla řádků, takže můžete snadno identifikovat, kde jsou problémy v rámci skriptu.

[![pomocí okna Inspektoru objektů zobrazit objekt JSON.](understanding-asp-net-ajax-debugging-capabilities/_static/image14.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image13.png)

**Obrázek 5**: použití okna Inspektoru objektů k zobrazení objektu JSON.  ([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-debugging-capabilities/_static/image15.png))

Výběr možnosti ladění umožňuje spustit příkazy skriptu přímo v příkazovém podokně pomocníka pro vývoj webu, který umožňuje zobrazit hodnotu proměnných, zapisovat objekty JSON a navíc další. Pokud je znovu provedena stejná akce, která aktivovala chybu, a v počítači je k dispozici Visual Studio 2008, zobrazí se výzva ke spuštění relace ladění, takže můžete krokovat kód podle řádku, jak je popsáno v předchozí části.

[![dialogového okna chyby skriptu pomocníka pro vývoj webu](understanding-asp-net-ajax-debugging-capabilities/_static/image17.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image16.png)

**Obrázek 6**: dialogové okno chyby skriptu pomocníka pro vývoj webu ([kliknutím zobrazíte obrázek v plné velikosti](understanding-asp-net-ajax-debugging-capabilities/_static/image18.png))

*Kontrola zpráv žádosti a odpovědi*

Při ladění stránek AJAX ASP.NET je často užitečné zobrazovat zprávy žádosti a odpovědi odeslané mezi stránkou a serverem. Zobrazení obsahu v rámci zpráv vám umožní zjistit, jestli se předávají vhodná data, a také velikost zpráv. Pomocník pro vývoj webu nabízí vynikající funkci protokolovacího nástroje zpráv HTTP, která usnadňuje zobrazení dat jako nezpracovaných textu nebo v čitelnějším formátu.

Pokud chcete zobrazit zprávy žádosti a odpovědi AJAX ASP.NET, musí být povolený protokolovací nástroj HTTP tím, že v nabídce Pomocník pro vývoj webu vybere protokol HTTP povolit protokolování HTTP. Po povolení můžete všechny zprávy odeslané z aktuální stránky zobrazit v prohlížeči protokolu HTTP, ke kterému se dostanete tak, že vyberete HTTP zobrazit protokoly HTTP.

I když zobrazení nezpracovaného textu odeslaného v každé zprávě žádosti nebo odpovědi je určitě užitečné (a možnost v nástroji Web Development Helper), je často snazší zobrazit data zpráv v podrobnějším formátu. Po povolení protokolování protokolu HTTP a zaznamenání zpráv do protokolu lze zobrazit data zpráv dvojitým kliknutím na zprávu v prohlížeči protokolu HTTP. Díky tomu můžete zobrazit všechna záhlaví přidružená ke zprávě a také obsah samotné zprávy. Obrázek 7 ukazuje příklad zprávy s požadavkem a zprávy s odpovědí zobrazované v okně prohlížeče protokolu HTTP.

[Pokud chcete zobrazit data žádosti a odpovědi, ![pomocí prohlížeče protokolu HTTP.](understanding-asp-net-ajax-debugging-capabilities/_static/image20.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image19.png)

**Obrázek 7**: použití prohlížeče protokolu HTTP k zobrazení dat žádosti a odpovědi.  ([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-debugging-capabilities/_static/image21.png))

Prohlížeč protokolu HTTP automaticky analyzuje objekty JSON a zobrazí je pomocí stromového zobrazení, které umožňuje rychlý a snadný pohled na data vlastností objektu. Když se na stránce ASP.NET AJAX používá UpdatePanel, prohlížeč rozdělí každou část zprávy na jednotlivé části, jak je znázorněno na obrázku 8. Jedná se o skvělou funkci, která usnadňuje zobrazení a porozumění tomu, co je ve zprávě ve srovnání s prohlížením nezpracovaných dat zpráv.

[![zprávu odpovědi ovládacího prvku UpdatePanel zobrazovanou v prohlížeči protokolu HTTP.](understanding-asp-net-ajax-debugging-capabilities/_static/image23.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image22.png)

**Obrázek 8**: zpráva odpovědi ovládacího prvku UpdatePanel zobrazovaná pomocí prohlížeče protokolu HTTP.  ([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-debugging-capabilities/_static/image24.png))

K dispozici je několik dalších nástrojů, které se dají použít k zobrazení žádostí a odpovědí kromě pomocníka pro vývoj webů. Další dobrá možnost je Fiddler, která je dostupná zdarma na [http://www.fiddlertool.com](http://www.fiddlertool.com). I když zde Fiddler nebude popsána, je to také dobrá možnost, pokud potřebujete důkladně zkontrolovat záhlaví a data zpráv.

## <a name="debugging-with-firefox-and-firebug"></a>Ladění pomocí Firefox a Firebug

I když je Internet Explorer stále nejpoužívanějším prohlížečem, další prohlížeče, jako je Firefox, jsou poměrně oblíbené a jsou používány více a více. V důsledku toho budete chtít zobrazit a ladit stránky ASP.NET AJAX v prohlížeči Firefox a také aplikaci Internet Explorer, abyste zajistili správnou funkčnost vašich aplikací. I když se Firefox nemůže spojit přímo se Visual Studio 2008 pro ladění, má rozšíření s názvem Firebug, které lze použít k ladění stránek. Firebug se dá zdarma stáhnout tak, že na [http://www.getfirebug.com](http://www.getfirebug.com).

Firebug poskytuje plnohodnotné ladicí prostředí, které lze použít ke krokování kódu řádek po řádku, přístupu ke všem skriptům používaným na stránce, zobrazení struktur modelu DOM, zobrazení stylů CSS a dokonce i ke sledování událostí, ke kterým dochází na stránce. Po nainstalování Firebug k němu můžete vybrat nástroje Firebug otevřít Firebug v nabídce Firefox. Podobně jako pomocník pro vývoj webu se Firebug používá přímo v prohlížeči, i když je možné ho použít jako samostatnou aplikaci.

Po spuštění Firebug lze nastavit zarážky na jakémkoli řádku souboru JavaScriptu, zda je skript vložen na stránku nebo ne. Chcete-li nastavit zarážku, napřed načtěte příslušnou stránku, kterou chcete ladit v prohlížeči Firefox. Po načtení stránky vyberte z rozevíracího seznamu skripty v Firebug skript, který chcete ladit. Zobrazí se všechny skripty používané stránkou. Zarážka je nastavená tak, že kliknete na šedou oblast Firebug zásobníku na řádku, kde by měla zarážka jít, třeba v sadě Visual Studio 2008.

Po nastavení zarážky v Firebug můžete provést akci potřebnou ke spuštění skriptu, který je třeba ladit, například kliknutím na tlačítko nebo obnovením prohlížeče aktivovat událost při načtení. Spuštění se automaticky zastaví na řádku obsahujícím zarážku. Obrázek 9 ukazuje příklad zarážky, která se aktivovala v Firebug.

[![zpracování zarážek v Firebug.](understanding-asp-net-ajax-debugging-capabilities/_static/image26.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image25.png)

**Obrázek 9**: zpracování zarážek v Firebug.  ([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-debugging-capabilities/_static/image27.png))

Po dosažení zarážky můžete krokovat krok dovnitř, Krokovat s vnořením kódu pomocí tlačítek se šipkami. Při procházení kódu jsou proměnné skriptu zobrazeny v pravé části ladicího programu, což vám umožní zobrazit hodnoty a přejít k podrobnostem objektů. Firebug také obsahuje rozevírací seznam zásobník volání pro zobrazení kroků spuštění skriptu, které vedly k ladění aktuálního řádku.

Firebug také obsahuje okno konzoly, které lze použít k otestování různých příkazů skriptu, vyhodnocování proměnných a zobrazení výstupu trasování. K němu se dostanete kliknutím na kartu konzola v horní části okna Firebug. Laděná stránka může obsahovat také "prověření", aby se zobrazila její struktura a obsah DOM kliknutím na kartu zkontrolovat. Při přetažení na jiné prvky modelu DOM zobrazené v okně inspektora se zvýrazní příslušná část stránky, která usnadňuje zjištění, kde se element na stránce používá. Hodnoty atributu přidružené k danému elementu lze změnit "Live" a experimentovat s použitím různých šířek, stylů atd. na prvek. Tato funkce je dobrá, která vám ušetří možnost nepřetržitě přepínat mezi editorem zdrojového kódu a prohlížečem Firefox, aby se zobrazilo, jak jednoduché změny ovlivní stránku.

Obrázek 10 ukazuje příklad použití nástroje DOM Inspector k nalezení textového pole s názvem txtCountry na stránce. Firebug Inspector lze také použít k zobrazení stylů CSS použitých na stránce a také k událostem, ke kterým dochází, jako je sledování pohybu myši, kliknutí na tlačítko a další.

[![pomocí inspektoru DOM v Firebug.](understanding-asp-net-ajax-debugging-capabilities/_static/image29.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image28.png)

**Obrázek 10**: použití inspektoru DOM v Firebug.  ([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-debugging-capabilities/_static/image30.png))

Firebug poskytuje lehký způsob, jak rychle ladit stránku přímo v prohlížeči Firefox a také skvělý nástroj pro kontrolu různých prvků v rámci stránky.

## <a name="debugging-support-in-aspnet-ajax"></a>Podpora ladění v ASP.NET AJAX

Knihovna ASP.NET AJAX obsahuje mnoho různých tříd, které lze použít ke zjednodušení procesu přidávání schopností AJAX do webové stránky. Tyto třídy můžete použít k vyhledání prvků v rámci stránky a manipulaci s nimi, přidání nových ovládacích prvků, volání webových služeb a dokonce zpracování událostí. Knihovna ASP.NET AJAX obsahuje také třídy, které lze použít k rozšíření procesu stránek ladění. V této části se zavedete do třídy Sys. Debug a zjistíte, jak se dá použít v aplikacích.

*Použití třídy Sys. Debug*

Třída Sys. Debug (třída JavaScriptu, která se nachází v oboru názvů sys), se dá použít k provedení několika různých funkcí, jako je například zápis výstupu trasování, provádění kontrolních výrazů kódu a vynucené selhání kódu, aby bylo možné ho ladit. Používá se rozsáhle v souborech ladění knihovny ASP.NET AJAX (ve výchozím nastavení nainstalované ve složce C:\Program Files\Microsoft ASP. NET\ASP.NET 2,0 AJAX Extensions\v1.0.61025\MicrosoftAjaxLibrary\System.Web.Extensions\1.0.61025.0) k provádění podmíněných testů ( označované jako kontrolní výrazy), které zajišťují, že parametry jsou správně předány funkcím, že objekty obsahují očekávaná data a zapisují příkazy TRACE.

Třída Sys. Debug zpřístupňuje několik různých funkcí, které lze použít ke zpracování trasování, kontrolních výrazů kódu nebo selhání, jak je uvedeno v tabulce 1.

**Tabulka 1. Funkce třídy Sys. Debug.**

| **Název funkce** | **Popis** |
| --- | --- |
| Assert (podmínka; zpráva; displayCaller) | Vyhodnotí, že parametr Condition má hodnotu true. Pokud je testovaná podmínka nepravdivá, použije se k zobrazení hodnoty parametru zprávy okno se zprávou. Pokud má parametr displayCaller hodnotu true, metoda také zobrazí informace o volajícím. |
| clearTrace() | Vymaže výstup příkazů z operací trasování. |
| Chyba (zpráva) | Způsobí, že program zastaví provádění a přeruší do ladicího programu. Pomocí parametru zprávy lze určit důvod selhání. |
| trasování (zpráva) | Zapíše parametr zprávy do výstupu trasování. |
| traceDump (objekt; název) | Vytvoří výstup dat objektu v čitelném formátu. Parametr Name lze použít k poskytnutí popisku pro výpis trasování. Všechny dílčí objekty v rámci objektu, které jsou předmětem dumpingu, budou ve výchozím nastavení zapsány. |

Trasování na straně klienta lze použít téměř stejným způsobem jako funkce trasování, které jsou k dispozici v ASP.NET. Umožňuje snadno zobrazit různé zprávy bez přerušení toku aplikace. Výpis 5 ukazuje příklad použití funkce sys. Debug. Trace k zápisu do protokolu trasování. Tato funkce jednoduše vezme zprávu, která by se měla zapsat jako parametr.

**Výpis 5. Pomocí funkce sys. Debug. Trace.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample6.js)]

Pokud spustíte kód zobrazený v seznamu 5, na stránce se nezobrazí žádný výstup trasování. Jediným způsobem, jak se podívat, je použít okno konzoly, které je k dispozici v aplikaci Visual Studio .NET, webové vývojové pomůcky nebo Firebug. Pokud chcete zobrazit výstup trasování na stránce, budete muset přidat značku TextArea a dát mu ID TraceConsole, jak je uvedeno dále:

[!code-html[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample7.html)]

Jakékoli příkazy sys. Debug. Trace na stránce se zapíší do TraceConsole TextArea.

V případech, kdy chcete zobrazit data obsažená v objektu JSON, můžete použít funkci traceDump třídy Sys. Debug. Tato funkce přijímá dva parametry, včetně objektu, které by měly být dumpingové do konzoly trasování, a název, který lze použít k identifikaci objektu ve výstupu trasování. Výpis 6 ukazuje příklad použití funkce traceDump.

**Výpis 6. Použití funkce sys. Debug. traceDump**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample8.js)]

Obrázek 11 ukazuje výstup z volání funkce sys. Debug. traceDump. Všimněte si, že kromě vypsání dat objektu osoby také zapisuje data dílčího objektu Address.

Kromě trasování lze třídu sys. debug použít také k provádění kontrolních výrazů kódu. Kontrolní výrazy se používají k otestování, jestli jsou při spuštění aplikace splněné konkrétní podmínky. Ladicí verze skriptů knihovny ASP.NET AJAX obsahuje několik příkazů kontrolního výrazu pro otestování různých podmínek.

Výpis 7 ukazuje příklad použití funkce sys. Debug. Assert k otestování podmínky. Kód testuje, zda je objekt adresy null před aktualizací objektu Person.

[![výstup funkce sys. Debug. traceDump.](understanding-asp-net-ajax-debugging-capabilities/_static/image32.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image31.png)

**Obrázek 11**: výstup funkce sys. Debug. traceDump  ([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-debugging-capabilities/_static/image33.png))

**Výpis 7. Pomocí funkce Debug. Assert.**

[!code-javascript[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample9.js)]

Tři parametry jsou předány, včetně podmínky k vyhodnocení, zprávy, která se zobrazí, pokud kontrolní výraz vrátí hodnotu false a zda se mají zobrazit informace o volajícím. V případech, kdy se kontrolní výraz nezdaří, se zpráva zobrazí také jako informace o volajícím, pokud byl třetí parametr pravdivý. Obrázek 12 ukazuje příklad dialogového okna selhání, které se zobrazí, pokud se kontrolní výraz uvedený v seznamu 7 nezdaří.

Koncová funkce, která se má krýt, je sys. Debug. selžou. Pokud chcete vynutit selhání kódu na konkrétním řádku ve skriptu, můžete přidat sys. Debug. uncalled, nikoli příkaz ladicího programu, který se obvykle používá v aplikacích JavaScriptu. Funkce sys. Debug. Failure přijímá parametr jednoho řetězce, který představuje důvod selhání, jak je uvedeno dále:

[!code-css[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample10.css)]

[![zprávu o chybě sys. Debug. Assert.](understanding-asp-net-ajax-debugging-capabilities/_static/image35.png)](understanding-asp-net-ajax-debugging-capabilities/_static/image34.png)

**Obrázek 12**: zpráva o chybě sys. Debug. Assert  ([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-debugging-capabilities/_static/image36.png))

Pokud při provádění skriptu dojde k chybě sys. Debug. selhání, hodnota parametru zprávy se zobrazí v konzole ladicí aplikace, jako je například Visual Studio 2008, a zobrazí se výzva k ladění aplikace. Jeden případ, kde to může být poměrně užitečné, je, že nemůžete nastavit zarážku se sadou Visual Studio 2008 na vloženém skriptu, ale chcete, aby se kód zastavil na konkrétním řádku, abyste mohli zkontrolovat hodnotu proměnných.

*Princip vlastnosti ScriptMode ovládacího prvku ScriptManager*

Knihovna ASP.NET AJAX obsahuje verze skriptu ladění a verze, které jsou ve výchozím nastavení nainstalovány ve složce C:\Program Files\Microsoft ASP. NET\ASP.NET 2,0 AJAX Extensions\v1.0.61025\MicrosoftAjaxLibrary\System.Web.Extensions\1.0.61025.0. Ladicí skripty jsou v současné době naformátovány, snadno čitelné a mají několik volání sys. Debug. Assert, zatímco skripty vydaných verzí mají odpuštění prázdných znaků, a k minimalizaci celkové velikosti používají třídu sys. Debug.

Ovládací prvek ScriptManager přidaný do stránek ASP.NET AJAX přečte atribut debug elementu compilation v souboru Web. config a určí, které verze skriptů knihovny se mají načíst. Změnou vlastnosti ScriptMode ale můžete řídit, jestli se mají načítat skripty pro ladění nebo vydávání (skripty knihovny nebo vaše vlastní skripty). ScriptMode přijímá výčet ScriptMode, jehož členové obsahují auto, ladit, vydávat a zdědit.

ScriptMode má výchozí hodnotu auto, což znamená, že ovládací objekt ScriptManager zkontroluje atribut debug v souboru Web. config. Když je ladění false, ovládacímu prvku ScriptManager se načte prodejní verze skriptů knihovny ASP.NET AJAX. Je-li hodnota ladění pravdivá, bude načtena ladicí verze skriptů. Změna vlastnosti ScriptMode na Release nebo Debug vynutí ovládacímu prvku ScriptManager načíst příslušné skripty bez ohledu na to, jakou hodnotu má atribut debug v souboru Web. config. Výpis 8 ukazuje příklad použití ovládacího prvku ScriptManager k načtení skriptů ladění z knihovny ASP.NET AJAX.

**Výpis 8. Načítají se skripty ladění pomocí ovládacího prvku ScriptManager**.

[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample11.aspx)]

Můžete také načíst různé verze (ladění nebo vydání) vlastních skriptů pomocí vlastnosti skripty ovládacího prvku ScriptManager společně s komponentou ScriptReference, jak je uvedeno v seznamu 9.

**Výpis 9. Načítají se vlastní skripty pomocí ovládacího prvku ScriptManager.**

[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample12.aspx)]

> [!NOTE]
> Pokud načítáte vlastní skripty pomocí komponenty ScriptReference, je nutné, aby byl ovládací prvek ScriptManager upozorněn po dokončení načítání skriptu přidáním následujícího kódu do dolní části skriptu:

[!code-csharp[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample13.cs)]

Kód zobrazený v seznamu 9 instruuje ovládacímu prvku ScriptManager, aby vyhledal ladicí verzi skriptu person, aby automaticky hledal Person. Debug. js místo Person. js. Pokud soubor Person. Debug. js nebyl nalezen, bude vyvolána chyba.

V případech, kdy chcete načíst ladicí nebo prodejní verzi vlastního skriptu na základě hodnoty vlastnosti ScriptMode nastavené v ovládacím prvku ScriptManager, můžete nastavit vlastnost ScriptMode ovládacího prvku ScriptReference na dědění. Tím dojde k načtení správné verze vlastního skriptu na základě vlastnosti ScriptMode ovládacího prvku ScriptManager, jak je uvedeno v seznamu 10. Vzhledem k tomu, že vlastnost ScriptMode ovládacího prvku ScriptManager je nastavena na hodnotu ladit, bude na stránce načten a použit skript Person. Debug. js.

**Výpis 10. Dědění ScriptMode z ovládacího prvku ScriptManager pro vlastní skripty.**

[!code-aspx[Main](understanding-asp-net-ajax-debugging-capabilities/samples/sample14.aspx)]

Pomocí vlastnosti ScriptMode můžete snadno ladit aplikace a zjednodušit celkový proces. Skripty pro vydaných verzí knihovny ASP.NET AJAX jsou obtížně krokovat a čteny, protože formátování kódu bylo odebráno v době, kdy skripty ladění jsou formátovány speciálně pro účely ladění.

## <a name="conclusion"></a>Závěr

Technologie Microsoft ASP.NET AJAX poskytuje Solid Foundation pro vytváření aplikací s podporou jazyka AJAX, které můžou zlepšit celkové prostředí koncového uživatele. Nicméně stejně jako u jakékoli programovací technologie, chyby a další problémy s aplikacemi budou určitě nastat. Znalost různých dostupných možností ladění může ušetřit spoustu času a způsobit tak stabilnější produkt.

V tomto článku jste se seznámili s několika různými postupy pro ladění stránek ASP.NET AJAX, včetně aplikace Internet Explorer se sadou Visual Studio 2008, pomocníka pro vývoj webů a Firebug. Tyto nástroje mohou zjednodušit celkový proces ladění, protože můžete získat přístup k proměnným datům, procházením kódu řádek a zobrazení příkazů trasování. Kromě různých popsaných ladicích nástrojů jste si také viděli, jak lze v aplikaci použít třídu sys. Debug knihovny ASP.NET AJAX, a jak lze třídu ScriptManager použít k načtení ladění nebo vydání verzí skriptů.

## <a name="bio"></a>Dostupnost

Dan Wahlin (Microsoft nejvíc Professional for ASP.NET and XML Web Services) je instruktor pro vývoj a architekturu pro vývoj rozhraní .NET na úrovni technického školení ([www.interfacett.com)](http://www.interfacett.com). Daň ze sady XML pro vývojáře na webu ASP.NET ([www.XMLforASP.NET](http://www.XMLforASP.NET)) je v kanceláři mluvčího v INETA a mluví na několika konferencích. Specialista na spolupracovníka Windows DNA (Wrox), ASP.NET: tipy, kurzy a Code (Sams), ASP.NET 1,1 řešení Insider, Professional ASP.NET 2,0 AJAX (Wrox), ASP.NET 2,0 MVP Hackatony a vytvořil XML pro vývojáře ASP.NET (Sams). Když není psaní kódu, článků nebo knih, Dan, požívá psaní a zaznamenávání hudby a hraní Golfů a basketbalový s jeho manželkou a dětem.

Scott Cate spolupracuje s webovými technologiemi Microsoftu od 1997 a je prezidentem myKB.com ([www.myKB.com](http://www.myKB.com)), kde se specializuje při psaní aplikací založených na ASP.NET zaměřené na softwarová řešení ve znalostní bázi Knowledge Base. Scott se dá kontaktovat e-mailem na [scott.cate@myKB.com](mailto:scott.cate@myKB.com) nebo jeho blogu na [ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [Předchozí](understanding-asp-net-ajax-web-services.md)

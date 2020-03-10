---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
title: Začínáme | Microsoft Docs
author: Rick-Anderson
description: WebMatrix se už nedoporučuje jako integrované vývojové prostředí pro webové stránky ASP.NET. Použijte Visual Studio nebo Visual Studio Code. Tento návod...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: a36d3bdf-ef1b-47a4-b932-3a0cf4cad716
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/getting-started
msc.type: authoredcontent
ms.openlocfilehash: bb863f8605e6f8faca3b285607b63a3e88e83012
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547101"
---
# <a name="getting-started"></a>začínáme

tím, že [FitzMacken](https://github.com/tfitzmac)

[!INCLUDE[](~/includes/rp.md)]

> > [!NOTE] 
> > 
> > WebMatrix se už nedoporučuje jako integrované vývojové prostředí pro webové stránky ASP.NET. Použijte [Visual Studio](../program-asp-net-web-pages-in-visual-studio.md) nebo [Visual Studio Code](https://code.visualstudio.com/).
> 
> 
> Tyto doprovodné materiály a aplikace poskytují přehled webových stránek ASP.NET (verze 2 nebo novější) a syntaxe Razor, což je odlehčené rozhraní pro vytváření dynamických webů. Také zavádí WebMatrix, nástroj pro vytváření stránek a lokalit.
> 
> **Level**: New to ASP.NET Web Pages.  
> **Předpokládá se dovednost**: HTML, základní šablony stylů CSS.
> 
> Co se naučíte v prvním kurzu sady:
> 
> - Jaké jsou technologie webových stránek ASP.NET a k čemu slouží.
> - Jaká je WebMatrix.
> - Jak nainstalovat vše.
> - Vytvoření webu pomocí WebMatrixu
>   
> 
> Popsané funkce a technologie:
> 
> - Instalace webové platformy Microsoft.
> - WebMatrixu.
> - stránky *. cshtml*
>   
> 
> Jan Pope původně napsal tento kurz. FitzMacken ho aktualizoval pro Microsoft WebMatrix 3.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 2
> - WebMatrix 3

## <a name="what-should-you-know"></a>Co byste měli znát?

Předpokládáme, že jste obeznámeni s:

- **HTML**. Nejsou vyžadovány žádné podrobné znalosti. Nebudeme vysvětlovat kód HTML, ale nepoužíváme to nic složitě. Poskytneme odkazy na kurzy HTML, kde se domníváme, že jsou užitečné.
- Šablony stylů **CSS**. Stejné jako u formátu HTML.
- **Základní nápady databáze**. Pokud jste tabulku použili pro data a seřadili a vyfiltrují data, je to úroveň odbornosti, která je obecně předpokladem pro tuto sadu kurzů.

Také předpokládáme, že vás zajímá základní programování. Webové stránky ASP.NET používají programovací jazyk s názvem C#. V programování nemusíte mít žádné pozadí, stačí to jenom na vás. Pokud jste už dříve napsali JavaScript na webové stránce, měli byste mít spoustu na pozadí.

Všimněte si, že pokud jste obeznámeni s programováním, může se stát, že tento kurz se zpočátku posouvá pomalu, zatímco nově přinášíme nové programátory do rychlosti. Stejně jako v předchozích několika kurzech se ale bude vysvětlovat méně základních programů, které vám pomohou při seznámení s rychlejším klipem.

## <a name="what-do-you-need"></a>Co potřebujete?

Zde je seznam toho, co budete potřebovat:

- Počítač se systémem Windows 8, Windows 7, Windows Server 2008 nebo Windows Server 2012.
- Živé připojení k Internetu.
- Oprávnění správce (požadováno pro proces instalace).

## <a name="what-is-aspnet-web-pages"></a>Co jsou webové stránky ASP.NET?

Webové stránky ASP.NET jsou rozhraní, které můžete použít k vytvoření dynamických webových stránek. Jednoduchá webová stránka HTML je statická; jeho obsah je určen pevným kódem HTML, který je na stránce. Dynamické stránky, jako jsou ty, které vytvoříte pomocí webových stránek ASP.NET, vám umožní vytvořit obsah stránky za běhu pomocí kódu.

Dynamické stránky umožňují provádět nejrůznější akce. Uživatele můžete požádat o zadání pomocí formuláře a pak změnit, co stránka zobrazuje nebo jak vypadá. Můžete získat informace od uživatele, uložit ho do databáze a pak ho zobrazit později. Můžete odesílat e-maily z webu. Můžete komunikovat s jinými službami na webu (například službou mapování) a vytvořit stránky, které integrují informace z těchto zdrojů.

## <a name="what-is-webmatrix"></a>Co je WebMatrix?

WebMatrix je nástroj, který integruje editor webových stránek, databázový nástroj, webový server pro testování stránek a funkce pro publikování vašeho webu na internetu. WebMatrix je zdarma a je snadné ji nainstalovat a snadno používat. (Funguje také pro jednoduché stránky HTML a také pro jiné technologie, jako je PHP.)

Pro práci s ASP.NET webovými stránkami *nemusíte* ve skutečnosti používat WebMatrix. Můžete vytvářet stránky pomocí textového editoru, například a testovat stránky pomocí webového serveru, ke kterému máte přístup. WebMatrix je ale velmi snadné, takže tyto kurzy budou používat WebMatrix v celém rozsahu.

## <a name="about-these-tutorials"></a>O těchto kurzech

V tomto kurzu se naučíte, jak používat webové stránky ASP.NET. V tomto úvodním kurzu je celkem 9 kurzů. Je součástí série kurzů, které vás přesměrují z ASP.NET začátečníků na webové stránky a vytváření reálných webů s profesionálním přehledem.

V tomto prvním kurzu se soustředíme na to, jak se naučíte pracovat s ASP.NET webovými stránkami. Až budete hotovi, můžete pracovat s dalšími kurzy, které se nacházejí v tomto umístění a které podrobněji ilustrují webové stránky.

Podrobnější vysvětlení jsme záměrně snadno našli. A kdykoli zobrazíme něco, v tomto kurzu si vždycky vyberu způsob, jakým je nejjednodušší pochopit. Pozdější kurzy nastaví další hloubku a ukáže vám efektivnější nebo pružnější přístup (ještě více zajímavější). Tyto kurzy ale vyžadují, abyste nejdřív pochopili základy.

Sada kurzů, kterou jste právě zahájili, pokrývá tyto funkce webových stránek ASP.NET:

- Seznámení s nainstalovanou a načítají se všechno. (To je v kurzu, který čtete.)
- Základy programování webových stránek ASP.NET.
- Vytváří se databáze.
- Vytvoření a zpracování formuláře vstupu uživatele.
- Přidávání, aktualizace a odstraňování dat v databázi.

## <a name="what-will-you-create"></a>Co budete vytvářet?

V tomto kurzu se nastavuje a následně vyvíjejí kolem webu, kde můžete vypsat videa, která chcete. Budete moct zadat filmy, upravit je a zobrazit jejich seznam. Tady je pár stránek, které vytvoříte v této sadě kurzů. První z nich zobrazuje stránku se seznamem filmů, kterou vytvoříte:

![Aplikace dokončil Movie ukazující seznam filmů](getting-started/_static/image1.png)

A tady je stránka, která vám umožní přidat nové informace o videu na web:

![Dokončená aplikace filmů ukazující stránku přidat film](getting-started/_static/image2.png)

V dalším kurzu se nastavují buildy na této sadě a přidají se další funkce, jako je nahrávání obrázků, odesílání a posílání e-mailů a integrace se sociálními médii.

## <a name="see-this-app-running-on-azure"></a>Podívejte se na tuto aplikaci spuštěnou v Azure

Chcete zobrazit dokončený web běžící jako živá webová aplikace? Úplnou verzi aplikace můžete nasadit do svého účtu Azure pouhým kliknutím na následující tlačítko.

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebPagesMovies)

K nasazení tohoto řešení do Azure potřebujete účet Azure. Pokud ještě nemáte účet, máte následující možnosti:

- [Otevřete si bezplatný účet Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) – získáte kredity, které můžete použít k vyzkoušení placených služeb Azure a dokonce i po jejich použití, můžete účet ponechat a používat bezplatné služby Azure.
- [Aktivujte výhody pro předplatitele MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) – vaše předplatné MSDN vám každý měsíc dává kredity, které můžete použít pro placené služby Azure.

## <a name="installing-everything"></a>Instalace všeho

Vše můžete nainstalovat pomocí instalačního programu webové platformy od Microsoftu. V důsledku toho nainstalujete instalační program a pak ho použijete k instalaci všech ostatních.

Chcete-li použít webové stránky, je nutné mít nainstalován alespoň systém Windows XP s aktualizací SP3 nebo Windows Server 2008 nebo novější.

Na [stránce webové stránky](../../../index.md) na webu ASP.NET klikněte na **nainstalovat**.

![Web ASP.NET zobrazující tlačítko &quot;nainstalovat&quot; WebMatrixu](getting-started/_static/image3.png)

Před instalací WebMatrixu se zobrazí výzva, abyste přijali Licenční podmínky a prohlášení o zásadách ochrany osobních údajů.

![přijmout termín pro zahájení instalace](getting-started/_static/image4.png)

Kliknutím na **Spustit** spusťte instalaci. (Pokud chcete instalační program uložit, klikněte na **Uložit** a spusťte instalační program ze složky, kam jste ho uložili.)

![](getting-started/_static/image5.png)

Zobrazí se instalace webové platformy, která je připravena k instalaci WebMatrixu. Klikněte na **Nainstalovat**.

![](getting-started/_static/image6.png)

Instalační proces zobrazí informace o tom, co je potřeba nainstalovat do vašeho počítače, a spustí proces. V závislosti na tom, co je potřeba nainstalovat, může proces trvat několik minut. Kliknutím **na Souhlasím** přijměte licenční podmínky.

## <a name="hello-webmatrix"></a>Hello, WebMatrix

Až to bude hotové, proces instalace může automaticky spustit WebMatrix. Pokud tomu tak není, v systému Windows v nabídce **Start** spusťte **Microsoft WebMatrix**.

Při prvním spuštění WebMatrixu budete mít možnost se přihlásit k Microsoft Azure pomocí účet Microsoft. Když se přihlásíte, obdržíte 10 bezplatných webových aplikací prostřednictvím Azure. Tyto bezplatné webové aplikace poskytují pohodlný způsob, jak testovat vaše aplikace. Pokud ještě nemáte účet Azure, ale máte předplatné MSDN, můžete [si aktivovat výhody předplatného MSDN](https://www.windowsazure.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604). V opačném případě můžete během několika minut vytvořit bezplatný zkušební účet. Podrobnosti najdete v tématu [Bezplatná zkušební verze Azure](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).

K pokračování v tomto kurzu se nemusíte přihlašovat hned. Pokud se teď přihlásíte, budete mít i nadále možnost přihlásit se později. Poslední [téma](publishing.md) v této sérii kurzů se zabývá tím, jak nasadit váš web do Azure. Proto byste se museli přihlašovat k dokončení tohoto tématu.

V tomto okamžiku se buď přihlaste pomocí účet Microsoft nebo v pravém dolním rohu vyberte **ne** .

![Přihlásit se](getting-started/_static/image7.png)

Začněte tím, že vytvoříte prázdný web a přidáte stránku. V pozdějším kurzu v této sadě budete hrát s jednou z vestavěných šablon webů.

V okně Start klikněte na **Nový**.

![Úvodní obrazovka WebMatrixu](getting-started/_static/image8.png)

Šablony jsou předem připravené soubory a stránky pro různé typy webů. Chcete-li zobrazit všechny šablony, které jsou ve výchozím nastavení k dispozici, vyberte možnost galerie šablon.

![Vybrat galerii šablon](getting-started/_static/image9.png)

V okně **rychlé zprovoznění** vyberte ze skupiny **ASP.NET** možnost **prázdná lokalita** a pojmenujte novou lokalitu "WebPagesMovies".

![Okno WebMatrix rychlé zprovoznění s vybranou šablonou prázdného webu](getting-started/_static/image10.png)

Klikněte na **Další**.

Pokud jste se přihlásili k vašemu účet Microsoft, budete mít možnost vytvořit si web na Azure. Na základě názvu vašeho webu je doporučený výchozí název **WebPagesMovies.azurewebsites.NET** ; vykřičník však indikuje, že tento název není k dispozici v systému Windows Azure. Pro jednoduchost vyberte **Přeskočit** pro obejít vytváření webu v Azure hned teď. Později v této sérii publikujte web do Azure.

![Vytvoření webu Azure](getting-started/_static/image11.png)

WebMatrix vytvoří a otevře web:

![Nový web WebPagesMovies otevřený ve WebMatrixu](getting-started/_static/image12.png)

V horní části je k dispozici panel nástrojů Rychlý přístup a pás karet. V levém dolním rohu se zobrazí selektor pracovního prostoru, ve kterém můžete přepínat mezi úlohami (**weby**, **soubory**, **databázemi**a **sestavami**). Napravo je podokno obsahu pro Editor a pro sestavy. V dolní části se vám občas zobrazuje oznamovací pruh pro zprávy.

Další informace o WebMatrixu a jejích funkcích najdete v těchto kurzech.

## <a name="creating-a-web-page"></a>Vytvoření webové stránky

Pokud se chcete seznámit s webovými stránkami WebMatrix a ASP.NET, vytvoříte jednoduchou stránku.

V selektoru pracovního prostoru vyberte pracovní prostor **soubory** . Tento pracovní prostor vám umožní pracovat se soubory a složkami. V levém podokně se zobrazuje struktura souborů webu. Pás karet se změní na Zobrazit úlohy týkající se souborů.

![Pracovní prostor souborů v WebMatrixu](getting-started/_static/image13.png)

Na pásu karet klikněte na šipku pod položkou **Nový** a pak klikněte na **nový soubor**.

![Vytvoření nového souboru pomocí příkazu &quot;nový&quot; na pásu karet](getting-started/_static/image14.png)

WebMatrix zobrazí seznam typů souborů. Vyberte **cshtml**a do pole **název** zadejte "HelloWorld". Stránka CSHTML je stránka ASP.NET webové stránky.

![Vytváří se nová stránka s CSHTML s názvem HelloWorld. cshtml.](getting-started/_static/image15.png)

Klikněte na tlačítko **OK**.

WebMatrix vytvoří stránku a otevře ji v editoru.

![Nová stránka HelloWorld v editoru WebMatrixu](getting-started/_static/image16.png)

Jak vidíte, stránka obsahuje hlavně běžný kód HTML, s výjimkou bloku v horní části, který vypadá takto:

[!code-cshtml[Main](getting-started/samples/sample1.cshtml)]

To je pro přidání kódu, jak uvidíte za chvíli.

Všimněte si, že různé části stránky &mdash; názvy prvků, atributy a text spolu s blokem v horní části, jsou všechny v různých barvách. To se nazývá *zvýrazňování syntaxe*a usnadňuje tak zachování všeho, co je jasné. Je to jedna z funkcí, která usnadňuje práci s webovými stránkami ve WebMatrixu.

Přidejte obsah pro prvky `<head>` a `<body>`, jako v následujícím příkladu. (Pokud chcete, můžete pouze zkopírovat následující blok a nahradit celou existující stránku tímto kódem.)

[!code-cshtml[Main](getting-started/samples/sample2.cshtml)]

Na panelu nástrojů Rychlý přístup nebo v nabídce **soubor** klikněte na **Uložit**.

![Tlačítko Uložit na panelu nástrojů Rychlý přístup k WebMatrixu](getting-started/_static/image17.png)

## <a name="testing-the-page"></a>Testování stránky

V pracovním prostoru **soubory** klikněte pravým tlačítkem na stránku *HelloWorld. cshtml* a pak klikněte na **Spustit v prohlížeči**.

![Spuštění stránky pomocí tlačítka spustit na pásu karet WebMatrix](getting-started/_static/image18.png)

WebMatrix spustí integrovaný webový server (IIS Express), který můžete použít k testování stránek v počítači. (Bez IIS Express ve WebMatrixu byste museli stránku publikovat na webovém serveru ještě předtím, než ji budete moct otestovat.) Stránka se zobrazí ve výchozím prohlížeči.

![Stránka &quot;Hello World&quot; spuštěná v prohlížeči](getting-started/_static/image19.png)

Všimněte si, že při testování stránky v WebMatrix je adresa URL v prohlížeči podobná `http://localhost:33651/HelloWorld.cshtml.` název *localhost* odkazuje na místní server, což znamená, že stránka je obsluhována webovým serverem, který je ve vašem počítači. Jak je uvedeno, WebMatrix obsahuje program webového serveru s názvem IIS Express, který se spouští při spuštění stránky.

Číslo za *localhost* (například *localhost: 33651*) odkazuje na *číslo portu* v počítači. Toto je číslo "kanálu", který IIS Express používá pro tento konkrétní web. Číslo portu je vybráno náhodně z rozsahu 1024 až 65536 při vytváření lokality a je odlišné pro každý web, který vytvoříte. (Při testování vlastního webového serveru bude číslo portu skoro určitě jiné číslo než 33561.) Když pro každý web použijete jiný port, IIS Express může mít přímý odkaz na vaše weby, se kterými se mluví.

Později, když publikujete web na veřejný webový server, na adrese URL se už nezobrazuje *localhost* . V tomto okamžiku se zobrazí podrobnější adresa URL, například `http://myhostingsite/mywebsite/HelloWorld.cshtml` nebo cokoli, co stránka je. V této sérii kurzů se dozvíte více o publikování webu později.

## <a name="adding-some-server-side-code"></a>Přidání kódu na straně serveru

Zavřete prohlížeč a vraťte se zpátky na stránku ve WebMatrixu.

Přidejte řádek do bloku kódu tak, aby vypadal jako následující kód:

[!code-cshtml[Main](getting-started/samples/sample3.cshtml)]

Toto je trochu kódu Razor. Je pravděpodobně jasné, že získá aktuální datum a čas a vloží tuto hodnotu do *proměnné* s názvem `currentDateTime`. V dalším kurzu si přečtete Další informace o syntaxe Razor.

V těle stránky po `<p>Hello World!</p>` elementu přidejte následující:

[!code-html[Main](getting-started/samples/sample4.html)]

Tento kód získá hodnotu, kterou vložíte do proměnné `currentDateTime` v horní části a vloží ji do značky stránky. Znak `@` označuje kód webových stránek ASP.NET na stránce.

Spusťte znovu stránku (WebMatrix uloží změny, než se stránka spustí). Tentokrát se na stránce zobrazí datum a čas.

![&quot;Hello World&quot; stránky běžící v prohlížeči pomocí dynamicky generovaného zobrazení času](getting-started/_static/image20.png)

Chvíli počkejte a pak aktualizujte stránku v prohlížeči. Zobrazuje se aktualizace data a času.

V prohlížeči se podívejte na zdroj stránky. Vypadá to, že se jedná o následující značky:

[!code-html[Main](getting-started/samples/sample5.html)]

Všimněte si, že v horní části není k dispozici blok `@{ }`. Všimněte si také, že zobrazení data a času zobrazuje skutečný řetězec znaků (`1/18/2012 2:49:50 PM` nebo cokoli), ne `@currentDateTime` podobně jako na stránce *. cshtml* . Co se stalo, když jste spustili stránku, ASP.NET zpracoval veškerý kód (velmi malý v tomto případě), který byl označený `@`. Kód vytvoří výstup a tento výstup byl vložen do stránky.

## <a name="this-is-what-aspnet-web-pages-are-about"></a>To je to, co ASP.NET webové stránky.

Když si přečtete, že webové stránky ASP.NET vytvářejí dynamický webový obsah, co se vám zobrazuje, je to nápad. Stránka, kterou jste právě vytvořili, obsahuje stejný kód HTML, který jste viděli předtím. Může také obsahovat kód, který může provádět nejrůznější úlohy. V tomto příkladu existovala triviální úloha získání aktuálního data a času. Jak jste viděli, můžete kód ve formátu HTML a na stránce tak vydávat výstup. Když někdo požádá o stránku *. cshtml* v prohlížeči, ASP.NET zpracuje stránku, i když je stále v rukou webového serveru. ASP.NET vloží výstup kódu (pokud existuje) na stránku jako HTML. Po dokončení zpracování kódu odešle ASP.NET výslednou stránku do prohlížeče. Všechny prohlížeče v tuto minulosti jsou HTML. Zde je diagram:

![Koncepční postup, jak ASP.NET vygeneruje kód HTML dynamicky](getting-started/_static/image21.png)

Nápad je jednoduchý, ale existuje mnoho zajímavých úkolů, které může kód provádět, a existuje mnoho zajímavých způsobů, jak můžete na stránku dynamicky přidávat obsah HTML. A ASP.NET *. cshtml* stránky, podobně jako jakékoli stránky HTML, mohou také obsahovat kód, který běží v samotném prohlížeči (kód JavaScript a jQuery). Všechny tyto věci prozkoumáte v této sadě kurzů a v dalších.

## <a name="coming-up-next"></a>Připravujeme další

V dalším kurzu v této sérii prozkoumáte ASP.NET webové stránky s více dalšími.

## <a name="additional-resources"></a>Další prostředky

[Vytvořte si zcela nového webu ASP.NET](https://www.microsoft.com/web/post/create-an-aspnet-website-from-scratch). Toto je kurz, který se konkrétně týká použití WebMatrixu (nikoli ASP.NET webových stránek). Obsahuje ještě trochu více podrobností o některých dalších funkcích WebMatrixu, které se v této sadě kurzů nezabývá.

> [!div class="step-by-step"]
> [Next](intro-to-web-pages-programming.md)

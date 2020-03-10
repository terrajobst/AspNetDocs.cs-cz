---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: Použití řadičů a zobrazení k implementaci uživatelského rozhraní pro výpisy a podrobnosti | Microsoft Docs
author: microsoft
description: V kroku 4 se dozvíte, jak přidat kontroler do aplikace, která využívá náš model a poskytuje uživatelům přehledy dat a možnosti navigace...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 74319fe5ea4c79b50140834349e2fdf86420cfbb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600742"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a>Použití kontrolerů a zobrazení k implementaci uživatelského rozhraní seznamu a podrobností

od [Microsoftu](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 4 bezplatného [kurzu aplikace "NerdDinner"](introducing-the-nerddinner-tutorial.md) , který vás provede procesem vytvoření malé, ale dokončené webové aplikace pomocí ASP.NET MVC 1.
> 
> V kroku 4 se dozvíte, jak přidat kontroler do aplikace, která využívá náš model a poskytuje uživatelům informace o zobrazení dat a podrobností navigace pro večeři na našem webu NerdDinner.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme vám postupovat podle [Začínáme s kurzy pro](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [hudební úložiště](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) MVC 3 nebo MVC.

## <a name="nerddinner-step-4-controllers-and-views"></a>NerdDinner krok 4: řadiče a zobrazení

V případě tradičních webových rozhraní (klasických webových formulářů ASP, PHP, ASP.NET atd.) jsou příchozí adresy URL obvykle mapovány na soubory na disku. Příklad: požadavek na adresu URL, například "/Products.aspx" nebo "/Products.php", může být zpracován souborem "Products. aspx" nebo "Products. php".

Webové architektury MVC mapují adresy URL na kód serveru trochu jiným způsobem. Namísto mapování příchozích adres URL na soubory místo toho namapujte adresy URL na metody třídy. Tyto třídy se nazývají "řadiče" a zodpovídají za zpracování příchozích požadavků HTTP, zpracování vstupu uživatele, načítání a ukládání dat a určení odpovědi, která se pošle zpátky klientovi (zobrazení HTML, stažení souboru, přesměrování na jiný). Adresa URL atd.).

Teď, když jsme sestavili základní model pro naši aplikaci NerdDinner, náš další krok přidá do aplikace kontroler, který ho bude využívat k tomu, aby uživatelům poskytl informace o zobrazení dat a podrobností navigace pro večeři na našem webu.

### <a name="adding-a-dinnerscontroller-controller"></a>Přidání kontroleru DinnersController

Začneme tak, že kliknete pravým tlačítkem na složku Controllers v našem webovém projektu a pak vyberete příkaz nabídky **Add-&gt;Controller** (Tento příkaz můžete spustit také tak, že zadáte CTRL-M, CTRL-C):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

Tím se zobrazí dialogové okno Přidat kontroler:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

Pojmenujte nový kontroler "DinnersController" a klikněte na tlačítko Přidat. Visual Studio potom do našeho adresáře \Controllers přidá soubor DinnersController.cs:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

Otevře se také nová třída DinnersController v editoru kódu.

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a>Přidání metod akce index () a Details () do třídy DinnersController

Chceme umožnit návštěvníkům, kteří používají naši aplikaci, procházet seznam nadcházejících večeře a povolit jim kliknutí na jakoukoli večeři v seznamu, kde se zobrazí konkrétní podrobnosti. Provedeme to publikováním následujících adres URL z naší aplikace:

| **Adresa URL** | **Účel** |
| --- | --- |
| */Dinners/* | Zobrazit seznam nadcházejících večeře v HTML |
| */Dinners/Details/[ID]* | Zobrazí podrobnosti o konkrétní večeři, který je uvedený v parametru ID vloženém v rámci adresy URL, který bude odpovídat DinnerID večeře v databázi. Například:/Dinners/Details/2 by zobrazil stránku HTML s podrobnostmi o večeři, jejichž DinnerID hodnota je 2. |

Počáteční implementace těchto adres URL budeme publikovat přidáním dvou veřejných "metod akcí" do naší třídy DinnersController, například níže:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

Pak spustíme aplikaci NerdDinner a použijeme náš prohlížeč k jejich vyvolání. Zadáním v adrese URL *"/Dinners/"* způsobí spuštění naší metody *index ()* a pošle zpět následující odpověď:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

Zadáním v adrese URL */Dinners/Details/2* se spustí naše metoda *Details ()* a pošle se zpět následující odpověď:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

Možná vás zajímá, jak ASP.NET MVC ví, jak vytvořit naši třídu DinnersController a vyvolat tyto metody? Abychom porozuměli tomu, jak funguje směrování, podíváme se na to.

### <a name="understanding-aspnet-mvc-routing"></a>Principy směrování MVC ASP.NET

ASP.NET MVC zahrnuje výkonný modul pro směrování adres URL, který poskytuje značnou flexibilitu při řízení způsobu mapování adres URL na třídy kontroleru. Umožňuje nám úplně přizpůsobit, jak ASP.NET MVC zvolí třídu kontroleru, která se má vytvořit, kterou metodu vyvolat a taky nakonfigurovat různé způsoby, které lze automaticky analyzovat z adresy URL nebo řetězce dotazu a předat metodě jako argumenty parametru. Přináší flexibilitu pro zcela optimalizaci webu pro SEO (optimalizace vyhledávacích webů) a také publikování jakékoli struktury adres URL, kterou chceme z aplikace.

Ve výchozím nastavení jsou nové projekty ASP.NET MVC dodávány s předem nakonfigurovanou sadou pravidel směrování adres URL, která jsou již zaregistrována. Díky tomu můžeme snadno začít pracovat s aplikacemi, aniž byste museli explicitně konfigurovat cokoli. Výchozí registrace pravidel směrování najdete v rámci třídy "aplikace" našich projektů – které můžeme otevřít dvojitým kliknutím na soubor Global. asax v kořeni našeho projektu:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

Výchozí pravidla směrování ASP.NET MVC jsou registrována v rámci metody "RegisterRoutes" této třídy:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

"Trasy". Volání metody MapRoute () nad registruje výchozí pravidlo směrování, které mapuje příchozí adresy URL na třídy kontroleru pomocí formátu adresy URL:/{Controller}/{Action}/{ID} "– kde" Controller "je název třídy kontroleru pro vytvoření instance," Action "je název veřejné metody, která má být vyvolána a" ID "je volitelný parametr vložený v rámci adresy URL, který lze předat jako argument metody. Třetí parametr předaný volání metody "MapRoute ()" je sada výchozích hodnot, které se mají použít pro hodnoty Controller/Action/ID v případě, že nejsou přítomny v adrese URL (Controller = "Home", Action = "index", ID = "").

Níže je tabulka, která ukazuje, jak se namapují celá řada adres URL pomocí výchozího pravidla trasy "<em>/{Controllers}/{Action}/{ID}"</em>:

| **Adresa URL** | **Controller – třída** | **Action – metoda** | **Předané parametry** |
| --- | --- | --- | --- |
| */Dinners/Details/2* | DinnersController | Podrobnosti (ID) | id=2 |
| */Dinners/Edit/5* | DinnersController | Upravit (ID) | id=5 |
| */Dinners/Create* | DinnersController | Vytvořit () | neuvedeno |
| */Dinners* | DinnersController | Index() | neuvedeno |
| */Home* | HomeController | Index() | neuvedeno |
| */* | HomeController | Index() | neuvedeno |

Poslední tři řádky zobrazují výchozí hodnoty (Controller = Home, Action = index, ID = ""), které se používají. Vzhledem k tomu, že metoda "index" je registrována jako výchozí název akce, pokud není zadána, adresy URL "/Dinners" a "/Home" způsobují metodu akce index (), která má být vyvolána na svých třídách kontroleru. Protože je "domovský" řadič zaregistrován jako výchozí kontroler, pokud není zadán, adresa URL "/" způsobí vytvoření HomeController a metodu akce index (), která má být vyvolána.

Pokud se vám tato výchozí pravidla směrování adresy URL nelíbí, dobrá zpráva je, že se dají snadno měnit – stačí je upravit v rámci výše uvedené metody RegisterRoutes. U naší aplikace NerdDinner ale nebudeme měnit žádné výchozí pravidla směrování adresy URL – místo toho je stačí použít tak, jak jsou.

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a>Použití DinnerRepository z našeho DinnersControlleru

Pojďme teď nahradit naši aktuální implementaci metod DinnersController index () a Details () akce s implementacemi, které používají náš model.

Použijeme třídu DinnerRepository, kterou jsme vytvořili dříve k implementaci chování. Začneme přidáním příkazu Using, který odkazuje na obor názvů "NerdDinner. Models" a potom deklaruje instanci našeho DinnerRepository jako pole na naší třídě DinnerController.

Později v této kapitole zavádíme koncept "injektáže závislosti" a další způsob, jak můžou naše řadiče získat odkaz na DinnerRepository, který umožňuje lepší testování jednotek, ale hned teď vytvoříme instanci našeho DinnerRepositoryu. vložené jako následující.

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

Teď jsme připraveni vygenerovat odpověď HTML zpátky pomocí našich objektů načteného datového modelu.

### <a name="using-views-with-our-controller"></a>Používání zobrazení u našeho kontroleru

I když je možné napsat kód v rámci našich metod akcí pro sestavení kódu HTML a potom použít pomocnou metodu *Response. Write ()* k odeslání zpátky klientovi, bude tento přístup nepraktický rychle. Mnohem lepším řešením je, aby bylo možné provádět pouze logiku aplikace a dat v rámci našich metod DinnersController akcí a následně předat data potřebná k vygenerování odpovědi HTML do samostatné šablony "zobrazení", která je zodpovědná za výstup reprezentace HTML. z nich. Jak uvidíme za chvilku, šablona zobrazení je textový soubor, který obvykle obsahuje kombinaci značek HTML a vloženého kódu vykreslování.

Oddělení naší logiky kontrol od našeho vykreslování zobrazení přináší několik velkých výhod. Konkrétně pomáhá vymáhat jasné "oddělení obav" mezi kódem aplikace a kódem formátování/vykreslování uživatelského rozhraní. To je mnohem snazší pro logiku aplikace testování částí v izolaci z logiky vykreslování uživatelského rozhraní. Usnadňuje to pozdější úpravu šablon pro vykreslování uživatelského rozhraní, aniž by bylo nutné provádět změny kódu aplikace. A vývojáři a návrháři můžou usnadnit spolupráci na projektech.

Můžeme aktualizovat naši třídu DinnersController, aby označovala, že chceme použít šablonu zobrazení k odeslání zpět odpovědi uživatelského rozhraní HTML změnou signatur metod našich dvou metod, ze kterých má návratový typ typu "void", namísto toho, aby měl návratový typ "ActionResult". Pak můžeme zavolat pomocnou metodu *View ()* na základní třídu kontroleru a vrátit zpět objekt "ViewResult", například:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

Signatura pomocné metody *View ()* , kterou používáme výše, vypadá takto:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

První parametr pomocné metody *View ()* je název souboru šablony zobrazení, který chceme použít k vykreslení odpovědi HTML. Druhý parametr je objekt modelu, který obsahuje data, která šablona zobrazení potřebuje k vykreslení odpovědi HTML.

V rámci naší metody akce index () voláme pomocnou metodu *zobrazení ()* a uvedeme, že chceme vykreslit seznam večeře z HTML pomocí šablony zobrazení "index". Pomocí šablony zobrazení projdeme sekvenci objektů večeře, ze kterých se vygeneruje seznam:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

V naší metodě podrobností () se pokusíme načíst objekt večeře pomocí ID poskytnutého v rámci adresy URL. Pokud se najde platná večeře, zavoláme pomocnou metodu *zobrazení ()* , která indikuje, že se má k vykreslení načteného objektu večeře použít šablona zobrazení Details. Pokud se požaduje neplatnou večeři, vykreslíme vám užitečnou chybovou zprávu, která indikuje, že večeře neexistuje, pomocí šablony zobrazení "NotFound" (a v případě přetížené verze metody *View ()* , která pouze Získá název šablony):

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

Pojďme teď implementovat šablony zobrazení "NotFound", "Details" a "index".

### <a name="implementing-the-notfound-view-template"></a>Implementace šablony zobrazení "NotFound"

Začneme implementací šablony zobrazení "NotFound", která zobrazuje přívětivou chybovou zprávu s oznámením, že nelze najít požadovanou večeři.

Novou šablonu zobrazení vytvoříme tak, že umístíte náš textový kurzor do metody akce kontroleru a kliknete pravým tlačítkem a vyberete příkaz nabídky přidat zobrazení (Tento příkaz můžeme také spustit zadáním CTRL-M, CTRL-V):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

Tím se zobrazí dialogové okno Přidat zobrazení podobné tomuto. Ve výchozím nastavení se v dialogovém okně předem naplní název zobrazení, který se má shodovat s názvem metody akce, při které se v dialogovém okně spustilo kurzor (v tomto případě "Podrobnosti"). Vzhledem k tomu, že chceme nejdřív implementovat šablonu "NotFound", přepíšeme název tohoto zobrazení a nastavíme ho na místo "NotFound":

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

Po kliknutí na tlačítko Přidat vytvoří Visual Studio novou šablonu zobrazení "NotFound. aspx" pro nás v adresáři "\Views\Dinners" (kterou vytvoří i v případě, že adresář ještě neexistuje):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

Otevře se také naše nová šablona zobrazení "NotFound. aspx" v editoru kódu:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

Zobrazení šablon ve výchozím nastavení má dvě oblasti obsahu, kde můžeme přidat obsah a kód. První umožňuje přizpůsobit "název" stránky HTML, která se pošle zpátky. Druhý umožňuje přizpůsobit "hlavní obsah" stránky HTML odeslané zpět.

K implementaci naší šablony zobrazení "NotFound" přidáme základní obsah:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

Můžeme to vyzkoušet v prohlížeči. Pokud to chcete udělat, požádejte o adresu URL *"/Dinners/Details/9999"* . Tato akce bude odkazovat na večeři, který v databázi aktuálně neexistuje, a způsobí, že naše metoda DinnersController. Details () vykreslí naši "NotFound" šablonu zobrazení:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

Při snímku obrazovky výše si všimněte, že naše základní šablona zobrazení zdědila spoustu HTML, která obklopuje hlavní obsah na obrazovce. Je to proto, že naše zobrazení šablony používá šablonu "Master Page", která nám umožňuje použít konzistentní rozložení napříč všemi zobrazeními na webu. Podíváme se, jak stránky předlohy v pozdější části tohoto kurzu pracují rychleji.

### <a name="implementing-the-details-view-template"></a>Implementace šablony zobrazení Details

Pojďme teď implementovat šablonu zobrazení Details – která vygeneruje HTML pro jeden model večeře.

To provedeme tak, že umístíte náš textový kurzor do metody akce Details a kliknete pravým tlačítkem myši a vyberete příkaz nabídky přidat zobrazení (nebo stisknete CTRL + M, CTRL-V):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

Tím se zobrazí dialogové okno Přidat zobrazení. Ponecháme výchozí název zobrazení (podrobnosti). V dialogovém okně také vyberete zaškrtávací políčko vytvořit zobrazení silného typu a vybrat (pomocí rozevíracího seznamu ComboBox) název typu modelu, který předáváme z kontroleru do zobrazení. Pro toto zobrazení předáváme objekt večeře (plně kvalifikovaný název tohoto typu je: "NerdDinner. Models. večeře"):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

Na rozdíl od předchozí šablony, kde jsme zvolili vytvoření "prázdného zobrazení", tentokrát se rozhodneme pro toto zobrazení automaticky "vytvořit" pomocí šablony Details (podrobnosti). To můžeme naznačit změnou rozevíracího seznamu "Zobrazit obsah" v dialogovém okně výše.

"Generování uživatelského rozhraní" vygeneruje počáteční implementaci naší šablony zobrazení podrobností, která je založená na objektu večeře, který do něj předáváme. Díky tomu můžete snadno rychle začít s implementací šablony zobrazení.

Po kliknutí na tlačítko Přidat vytvoří Visual Studio nový soubor šablony zobrazení Details. aspx pro nás v rámci našeho adresáře "\Views\Dinners":

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

Otevře se také naše nová šablona zobrazení "Details. aspx" v editoru kódu. Bude obsahovat počáteční implementaci uživatelského rozhraní pro zobrazení podrobností založené na modelu večeře. Modul pro generování uživatelského rozhraní používá reflexi rozhraní .NET k zobrazení veřejných vlastností zveřejněných na dané třídě a přidá odpovídající obsah na základě každého typu, který najde:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

Můžeme požádat o adresu URL *"/Dinners/Details/1"* , aby se zobrazila informace o tom, jak se tato implementace uživatelského rozhraní "Details" v prohlížeči podobá. Pomocí této adresy URL se zobrazí jedna z večeři, kterou jsme ručně přidali do naší databáze při jejím prvním vytvoření:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

Tím se nám rychle spustí a spustí se úvodní implementace našeho zobrazení Details. aspx. Pak to můžeme použít k přizpůsobení uživatelského rozhraní pro naši spokojenost.

Když se podrobněji podíváme na šablonu details. aspx, zjistíme, že obsahuje statický kód HTML i vložený kód pro vykreslování. &lt;%%&gt; kódu Nuggets spustit kód při vykreslení šablony zobrazení a &lt;% =%&gt; Code Nuggets spustí kód obsažený v nich a pak vykreslí výsledek do výstupního datového proudu šablony.

V našem zobrazení můžeme psát kód, který přistupuje k objektu modelu "večeře", který byl předán z našeho kontroleru pomocí vlastnosti "model" silného typu. Visual Studio poskytuje úplný kód – IntelliSense při přístupu k této vlastnosti "model" v editoru:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

Pojďme udělat několik vylepšení, aby zdroj pro poslední šablonu zobrazení podrobností vypadal takto:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

Když přistupujeme znovu k adrese URL *"/Dinners/Details/1"* , teď se teď vykreslí jako v následujícím příkladu:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a>Implementace šablony zobrazení "index"

Pojďme teď implementovat šablonu zobrazení "index" – tím se vygeneruje výpis nadcházejících večeře. Provedete to tak, že umístíte textový kurzor do metody akce indexu a pak kliknete pravým tlačítkem a vyberete příkaz nabídky přidat zobrazení (nebo stisknete CTRL-M, CTRL-V).

V dialogovém okně Přidat zobrazení budeme uchovávat šablonu zobrazení s názvem index a vybrat zaškrtávací políčko vytvořit zobrazení silného typu. Tentokrát se rozhodneme, že automaticky vygenerujeme šablonu zobrazení "list" a jako typ modelu předaný do zobrazení vyberete "NerdDinner. Models. večeře" (to proto, že jsme zjistili, že vytváříme "list", což způsobí, že se zobrazí dialogové okno Přidat zobrazení. předání posloupnosti objektů večeře z našeho řadiče do zobrazení):

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

Když klikneme na tlačítko Přidat, Visual Studio vytvoří nový soubor šablony zobrazení index. aspx pro nás v rámci našeho adresáře "\Views\Dinners". V rámci něj bude "" generátorem "vytvořená počáteční implementace, která obsahuje seznam večeři v tabulce HTML, který předáte do zobrazení.

Když aplikaci spustíme a získáte přístup k adrese URL *"/Dinners/"* , vykreslíme si náš seznam večeře, například:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

Výše uvedené řešení tabulky nabízí rozložení dat o večeři, které je podobné mřížce, což není dost důležité pro náš seznam večeře pro příjemce. Můžeme aktualizovat šablonu zobrazení index. aspx a upravit ji tak, aby obsahovala méně sloupců dat, a použít &lt;prvek ul&gt; k jejich vykreslení místo tabulky pomocí následujícího kódu:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

Používáme klíčové slovo var v rámci výše uvedeného příkazu foreach jako smyčka za každou večeři v našem modelu. Ty, které nejsou C# známé pomocí 3,0, se můžou domnívat, že použití "var" znamená, že objekt večeře je pozdní vazbou. Místo toho znamená, že kompilátor používá odvozování typů proti silně typované vlastnosti "model" (která je typu "IEnumerable&lt;večeře&gt;") a zkompiluje místní proměnnou "večeře" jako typ večeře, což znamená, že získáme úplnou technologii IntelliSense a kontrolu doby kompilace v rámci bloků kódu:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

Po zobrazení aktualizace na adrese URL */Dinners* v našem prohlížeči se naše aktualizované zobrazení teď zdá, jak vidíte níže:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

To se vyhledává lépe, ale ještě ne úplně tam. Náš poslední krok je povolit koncovým uživatelům kliknout na jednotlivé večeře v seznamu a zobrazit podrobnosti o nich. To provedeme tak, že vyvykreslujeme prvky hypertextového odkazu HTML, které odkazují na metodu Action Details na našem DinnersController.

Tyto hypertextové odkazy můžeme v našem zobrazení indexu vygenerovat jedním ze dvou způsobů. První je ručně vytvořit HTML &lt;prvky&gt;, například níže, kam vložíme &lt;%%&gt; bloky v &lt;&gt; elementu HTML:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

Alternativním přístupem, který můžeme použít, je využít integrované metody "HTML. ActionLink ()" v rámci ASP.NET MVC, která podporuje Programové vytvoření HTML &lt;&gt; elementu, který odkazuje na jinou metodu akce na řadiči.

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

První parametr pro kód HTML. The ActionLink () pomocná metoda je text odkazu, který se má zobrazit (v tomto případě název večeře), druhý parametr je název akce kontroleru, na kterou chcete vytvořit odkaz (v tomto případě metoda Details), a třetí parametr je sada parametrů k odeslání do akce (implementující jako anonymní typ s názvem nebo hodnotami vlastnosti). V tomto případě zadáváme parametr ID pro večeři, ke kterému se chcete připojit, a vzhledem k tomu, že výchozí pravidlo směrování adresy URL v ASP.NET MVC je {Controller}/{Action}/{id} "metoda" HTML. ActionLink () "vygeneruje následující výstup:

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

Pro náš pohled index. aspx použijeme přístup k pomocné metodě HTML. ActionLink () a každý z nich v odkazu seznam na příslušnou adresu URL s podrobnostmi:

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

A teď, když máme přístup k adrese URL */Dinners* , náš seznam večeře vypadá takto:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

Po kliknutí na kteroukoli z těchto večeři v seznamu přejdeme k podrobnostem o tom, jak se dozvíte:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a>Vytváření názvů a adresářové struktury na základě konvence

ASP.NET aplikace MVC ve výchozím nastavení při rozpoznávání šablon zobrazení používají strukturu názvů adresářů na základě konvence. To umožňuje vývojářům vyhnout se nutnosti plně kvalifikovat cestu k umístění při odkazování na zobrazení v rámci třídy Controller. Ve výchozím nastavení bude ASP.NET MVC hledat soubor šablony zobrazení v adresáři * \Views\[Controller]\* Directory pod aplikací.

Pracovali jste například na třídě DinnersController – která explicitně odkazuje na tři šablony zobrazení: "index", "Details" a "NotFound". ASP.NET MVC bude standardně Hledat tato zobrazení v adresáři *\Views\Dinners* pod adresářem kořenový adresář aplikace:

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

Všimněte si, že v projektu jsou aktuálně tři třídy kontroleru (DinnersController, HomeController a AccountController – poslední dvě byly přidány ve výchozím nastavení, když jsme vytvořili projekt) a existují tři podadresáře (jeden pro každý Controller) v adresáři \Views

Zobrazení, na která se odkazují z domácích a řadičů účtů, automaticky vyřeší své šablony zobrazení z příslušných adresářů *\Views\Home* a *\Views\Account* . Podadresář *\Views\Shared* poskytuje způsob, jak uložit šablony zobrazení, které se znovu používají napříč více řadiči v rámci aplikace. Když se ASP.NET MVC pokusí vyřešit šablonu zobrazení, nejdřív se ověří v adresáři *\Views\[Controller]* , a pokud nenalezne šablonu zobrazení, bude se v adresáři *\Views\Shared* zobrazovat.

Při pojmenování jednotlivých šablon zobrazení doporučujeme, aby šablona zobrazení sdílela stejný název jako metoda akce, která způsobila vykreslení. Například výše uvedená metoda akce "index" používá zobrazení "index" k vykreslení výsledku zobrazení a metoda akce "Details" používá zobrazení podrobností k vykreslení výsledků. Díky tomu se snadno rychle zjistí, která šablona je k jednotlivým akcím přidružená.

Vývojáři nemusí explicitně zadávat název šablony zobrazení, pokud má šablona zobrazení stejný název jako metoda akce, která je vyvolána na řadiči. Místo toho můžeme jednoduše předat objekt modelu do pomocné metody View () (bez zadání názvu zobrazení) a ASP.NET MVC automaticky odsadí, že chceme pro vykreslení použít na disku šablonu zobrazení *\[\[Controller] název]* .

Díky tomu můžeme trochu vyčistit náš kód kontroleru a vyhnout se tak dvojímu kopírování názvu v našem kódu:

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

Výše uvedený kód je nezbytný k implementaci seznamu a podrobností o skvělé večeři pro web.

#### <a name="next-step"></a>Další krok

Teď jsme vytvořili prostředí s dobrým přístupem na večeři.

Pojďme nyní povolit možnost CRUD (vytvořit, číst, aktualizovat, odstranit) datový formulář, který podporuje úpravy.

> [!div class="step-by-step"]
> [Předchozí](build-a-model-with-business-rule-validations.md)
> [Další](provide-crud-create-read-update-delete-data-form-entry-support.md)

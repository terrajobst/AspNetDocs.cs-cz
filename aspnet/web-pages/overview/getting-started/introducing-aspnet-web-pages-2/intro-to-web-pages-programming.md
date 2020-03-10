---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
title: Představení webových stránek ASP.NET – základy programování | Microsoft Docs
author: Rick-Anderson
description: 'Tento kurz vám poskytne přehled o tom, jak programovat na webových stránkách ASP.NET pomocí syntaxe Razor. Co se naučíte: Základní syntaxí Razor, kterou použijete pro pr...'
ms.author: riande
ms.date: 06/17/2015
ms.assetid: 7526ed45-a97d-4e8a-8301-01324ef0eff9
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/intro-to-web-pages-programming
msc.type: authoredcontent
ms.openlocfilehash: 474de7671ac2931e5ba9ff635d77385403644521
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628476"
---
# <a name="introducing-aspnet-web-pages---programming-basics"></a>Představení webových stránek ASP.NET – základy programování

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento kurz vám poskytne přehled o tom, jak programovat na webových stránkách ASP.NET pomocí syntaxe Razor.
> 
> Naučíte se:
> 
> - Základní syntaxe Razor, která se používá pro programování na webových stránkách ASP.NET
> - Některé základní C#, což je programovací jazyk, který budete používat.
> - Některé základní koncepty programování webových stránek.
> - Jak nainstalovat balíčky (komponenty, které obsahují předem sestavený kód) pro použití s vaší lokalitou.
> - Jak používat *pomocníky* k provádění běžných programovacích úloh.
>   
> 
> Popsané funkce a technologie:
> 
> - NuGet a správce balíčků.
> - Pomocná rutina `Gravatar`

V tomto kurzu je primárně cvičení, které vás seznámí s syntaxí programování, kterou použijete pro webové stránky ASP.NET. Naučíte se *syntaxe Razor* a kódu, který je napsán v C# programovacím jazyce. V předchozím kurzu jste získali nakoukněte této syntaxe; v tomto kurzu vyvysvětlíme syntaxi.

Probereme, že tento kurz zahrnuje nejvíc programování, která se zobrazí v jednom kurzu, a že se jedná o jediný kurz, který je *jenom o programování* . Ve zbývajících kurzech v této sadě budete ve skutečnosti vytvářet stránky, které budou dělat zajímavé věci.

Naučíte se také o *pomocníky*. Pomocná komponenta je komponenta – zabalená část kódu, kterou můžete přidat na stránku. Pomocná osoba za vás provede práci, kterou by jinak mohlo být zdlouhavé nebo složité.

## <a name="creating-a-page-to-play-with-razor"></a>Vytvoření stránky pro přehrávání pomocí Razor

V této části přehrajete bit se syntaxí Razor, abyste mohli získat představu o základní syntaxi.

Spusťte WebMatrix, pokud ještě není spuštěná. Použijete web, který jste vytvořili v předchozím kurzu ([Začínáme s webovými stránkami](https://go.microsoft.com/fwlink/?LinkId=251578)). Pokud ho chcete znovu otevřít, klikněte na **Moje weby** a vyberte **WebPageMovies**:

![Úvodní obrazovka pro WebMatrix znázorňující zvýrazněné možnosti otevření webu a moje weby](intro-to-web-pages-programming/_static/image1.png)

Vyberte pracovní prostor **soubory** .

Na pásu karet klikněte na **Nový** a vytvořte stránku. Vyberte **cshtml** a pojmenujte novou stránku *TestRazor. cshtml*.

Klikněte na tlačítko **OK**.

Zkopírujte do souboru následující příkaz, zcela nahraďte to, co už je.

> [!NOTE]
> Při kopírování kódu nebo označení z příkladů na stránku nemusí být odsazení a zarovnání stejné jako v tomto kurzu. Odsazení a zarovnání neovlivní způsob, jakým se kód spouští, ale.

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample1.cshtml)]

## <a name="examining-the-example-page"></a>Prozkoumání ukázkové stránky

Většina toho, co vidíte, je běžný HTML. V horní části je však tento blok kódu:

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample2.cshtml)]

Všimněte si následujících informací o tomto bloku kódu:

- Znak @ oznamuje ASP.NET, že následuje kód Razor, nikoli HTML. ASP.NET zpracuje vše po znaku @ jako kód, dokud se znovu nespustí do nějakého kódu HTML. (V tomto případě to je &lt;! Element DOCTYPE&gt;.
- Složené závorky ({a}) uzavírají blok kódu Razor, pokud má kód více než jeden řádek. Složené závorky říkají ASP.NET, kde začíná a končí kód pro daný blok.
- Znaky//označují komentář – to znamená část kódu, který se nespustí.
- Každý příkaz musí končit středníkem (;). (Ne komentáře, ale.)
- Hodnoty můžete ukládat do *proměnných*, které vytvoříte (*deklarujete*) pomocí klíčového slova var. Když vytvoříte proměnnou, přiřadíte jí název, který může obsahovat písmena, číslice a podtržítka (\_). Názvy proměnných nemůžou začínat číslicí a nesmí používat název klíčového slova programování (jako var).
- Řetězce znaků (například "ASP.NET" a "webové stránky") uzavřete do uvozovek. (Musí se jednat o dvojité uvozovky.) Čísla nejsou v uvozovkách.
- Prázdné znaky mimo uvozovky nezáleží. Nezáleží na koncích řádků; výjimkou je, že řetězec nelze rozdělit do uvozovek napříč řádky. Odsazení a zarovnání nezáleží.

Něco, co není zřejmé z tohoto příkladu, je, že veškerý kód rozlišuje velká a malá písmena. To znamená, že proměnná TheSum je jinou proměnnou než proměnné, které mohou být pojmenovány theSum nebo TheSum. Podobně je var klíčové slovo, ale var není.

### <a name="objects-and-properties-and-methods"></a>Objekty a vlastnosti a metody

Pak je výraz DateTime. Now. V jednoduchých výrazech je hodnota DateTime *objektem*. Objekt je věcí, kterou můžete programovat s – stránkou, textovým polem, souborem, obrázkem, webovým požadavkem, e-mailovou zprávou, záznamem zákazníka atd. Objekty mají jednu nebo více *vlastností* , které popisují jejich charakteristiky. Objekt textového pole má vlastnost text (mimo jiné), objekt Request má vlastnost URL (a další), e-mailová zpráva má vlastnost from a vlastnost to a tak dále. Objekty mají také *metody* , které mohou provádět příkazy. S objekty budete pracovat s velkým množstvím.

Jak vidíte v příkladu, DateTime je objekt, který umožňuje Programová data a časy. Má vlastnost pojmenovanou nyní, která vrací aktuální datum a čas.

### <a name="using-code-to-render-markup-in-the-page"></a>Použití kódu k vykreslení značek na stránce

V těle stránky si všimněte následujícího:

[!code-html[Main](intro-to-web-pages-programming/samples/sample3.html)]

Znovu znak @ oznamuje ASP.NET, že následující je kód, nikoli HTML. V kódu můžete přidat @ následovaný výrazem kódu a ASP.NET vykreslí hodnotu tohoto výrazu přímo v daném bodě. V příkladu @a vykreslí bez ohledu na hodnotu proměnné s názvem a, @product vykreslí jakékoli proměnné s názvem Product a tak dále.

Nejste omezeni na proměnné, i když. V několika instancích sem znak @ před výrazem:

- @ (a\*b) vykreslí produkt bez ohledu na proměnné a a b. (Operátor \* znamená násobení.)
- @ (technologie + "" + Product) vykreslí hodnoty v technologii proměnných a produktu po jejich zřetězení a přidání prostoru mezi. Operátor (+) pro zřetězení řetězců je stejný jako operátor pro přidávání čísel. ASP.NET může obvykle určit, zda pracujete s čísly nebo s řetězci a zda má správnou věc s operátorem +.
- @Request.Url vykreslí vlastnost URL objektu Request. Objekt Request obsahuje informace o aktuálním požadavku z prohlížeče a vlastnost adresa URL obsahuje adresu URL daného aktuálního požadavku.

Tento příklad je také navržený tak, aby vám ukázal, že můžete pracovat různými způsoby. Můžete provádět výpočty v bloku kódu v horní části, vložit výsledky do proměnné a následně vykreslit proměnnou v kódu. Případně můžete provádět výpočty ve výrazu přímo v kódu. Přístup, který použijete, závisí na tom, co děláte, a v některém rozsahu podle vlastní předvolby.

### <a name="seeing-the-code-in-action"></a>Zobrazení kódu v akci

Klikněte pravým tlačítkem na název souboru a pak zvolte **Spustit v prohlížeči**. V prohlížeči se zobrazí stránka se všemi hodnotami a výrazy vyřešenými na stránce.

![Stránka ' TestRazor ' spuštěná v prohlížeči](intro-to-web-pages-programming/_static/image2.png)

Podívejte se na zdroj v prohlížeči.

![Zdroj stránky "test Razor" v prohlížeči](intro-to-web-pages-programming/_static/image3.png)

Jak očekáváte od vašeho prostředí v předchozím kurzu, žádný z kódů Razor není na stránce. Zobrazí se skutečné hodnoty zobrazení. Když spouštíte stránku, skutečně vydáváte požadavek na webový server, který je integrovaný do WebMatrixu. Po přijetí žádosti ASP.NET vyřeší všechny hodnoty a výrazy a vykreslí jejich hodnoty do stránky. Pak pošle stránku do prohlížeče.

> [!TIP] 
> 
> **Razor aC#**
> 
> Nyní jsme zjistili, že pracujete s syntaxe Razor. To je pravda, ale není to kompletní příběh. Zavolá *C#* se skutečný programovací jazyk, který používáte. C#Společnost Microsoft vytvořila před rokem desetiletí a stala se jedním z primárních programovacích jazyků pro vytváření aplikací pro Windows. Všechna pravidla, která jste viděli o tom, jak pojmenovat proměnnou a jak vytvořit příkazy a podobně, jsou ve skutečnosti všechna pravidla C# jazyka.
> 
> Syntaxe Razor odkazuje přesněji na malou sadu konvencí pro vložení tohoto kódu do stránky. Například konvence použití @ k označení kódu na stránce a použití @ {} pro vložení bloku kódu je aspektem Razor stránky. Pomocníky se také považují za součást sady Razor. Syntaxe Razor se používá na více místech, než jenom na webových stránkách ASP.NET. (Například používá se také v zobrazeních ASP.NET MVC.)
> 
> Uvádíme to proto, že pokud hledáte informace o programování webových stránek ASP.NET, najdete spoustu odkazů na Razor. Mnoho těchto odkazů se ale nevztahuje na to, co děláte, a proto může být matoucí. A ve skutečnosti mnohé z vašich otázek při programování skutečně vznikne buď při práci s C# ASP.NET, nebo s nimi pracovat. Takže pokud se vám podíváte na konkrétní informace o Razor, nemusí se vám najít odpovědi, které potřebujete.

## <a name="adding-some-conditional-logic"></a>Přidání některé podmíněné logiky

Jednou z skvělých funkcí, které se týkají použití kódu na stránce, je, že můžete změnit to, co se stane na základě různých podmínek. V této části kurzu se seznámíte s různými způsoby, jak změnit, co se zobrazuje na stránce.

Tento příklad bude jednoduchý a trochu contrived, abychom se mohli soustředit na podmíněnou logiku. Vytvoří se stránka, kterou vytvoříte:

- Zobrazit na stránce jiný text v závislosti na tom, zda se stránka zobrazuje při prvním zobrazení stránky nebo zda jste klikli na tlačítko pro odeslání stránky. To bude první podmíněný test.
- Zobrazí zprávu pouze v případě, že je do řetězce dotazu adresy URL předána určitá hodnota (http://...? show = true). To bude druhý podmíněný test.

V WebMatrixu vytvořte stránku a pojmenujte ji *TestRazorPart2. cshtml*. (Na pásu karet klikněte na **Nový**, zvolte **cshtml**, pojmenujte soubor a pak klikněte na **OK**.)

Obsah této stránky nahraďte následujícím:

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample4.cshtml)]

Blok kódu v horní části inicializuje proměnnou s názvem Message s nějakým textem. V těle stránky se obsah proměnné zprávy zobrazuje v prvku &lt;p&gt;. Značka obsahuje také prvek &lt;Input&gt; pro vytvoření tlačítka **Odeslat** .

Spusťte stránku a podívejte se, jak funguje nyní. Teď je to v podstatě statická stránka, a to i v případě, že kliknete na tlačítko **Odeslat** .

Vraťte se do WebMatrixu. Uvnitř bloku kódu přidejte *po* řádku, který inicializuje zprávu, následující zvýrazněný kód:

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample5.cshtml?highlight=4-6)]

### <a name="the-if---block"></a>Blok if {}

To, co jste právě přidali, byl podmínka if. V kódu má podmínka if strukturu, například:

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample6.cs)]

Podmínka, která se má testovat, je v závorkách. Musí se jednat o hodnotu nebo výraz, který vrací hodnotu true nebo false. Pokud je podmínka pravdivá, ASP.NET spustí příkaz nebo příkazy, které jsou uvnitř složených závorek. (Ty jsou *potom* součástí logiky *if-then* .) Pokud je podmínka false, blok kódu se přeskočí.

Tady je několik příkladů podmínek, které můžete testovat v příkazu IF:

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample7.cs)]

Můžete testovat proměnné proti hodnotám nebo proti výrazům pomocí *logického operátoru* nebo *operátoru porovnání*: rovná se (= =), větší než (&gt;), menší než (&lt;), větší než nebo rovno (&gt;=) a menší nebo rovno (&lt;=). Operátor! = znamená, že se nerovná – například pokud (a! = 0) znamená, že *se nerovná 0*.

> [!NOTE]
> Nezapomeňte si všimnout, že operátor porovnání pro Equals (= =) není stejný jako =. Operátor = se používá pouze k přiřazení hodnot (var a = 2). Pokud tyto operátory smícháte nahoru, zobrazí se chybová zpráva nebo se vám zobrazí nějaké neobvyklé výsledky.

Chcete-li otestovat, zda je něco true, úplná syntaxe je if (' provedl = = true). Můžete ale také použít zástupce if (dohotovo). Pokud není k dispozici žádný relační operátor, ASP.NET předpokládá, že testujete na hodnotu true.

Okně! operátor sám o sobě znamená logický operátor NOT. Například podmínka if (! Dispost) znamená, že není- *li vlastnost-post pravdivá*.

Podmínky lze kombinovat pomocí logického operátoru AND (&amp;&amp;) nebo logického operátoru OR (| | operator). Například poslední z podmínek IF v předchozích příkladech znamená, *že FileProcessingIsDone není nastaven na hodnotu true a vlastnost displayMessage je nastavena na hodnotu false*.

### <a name="the-else-block"></a>Blok else

Jedna z konečných věcí o if blocích: za blok if může následovat blok else. Blok else je užitečný, pokud je podmínka nepravdivá, musíte spustit jiný kód. Tady je jednoduchý příklad:

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample8.cs)]

V dalších kurzech uvidíte některé příklady, kde je užitečné použít blok else.

### <a name="testing-whether-the-request-is-a-submit-post"></a>Testování, zda je žádost odeslána (post)

Je to více, ale pojďme se vrátit na příklad, který má podmínku if ("zveřejnit") {...}. Vlastnost WebPost je ve skutečnosti vlastností aktuální stránky. Při prvním vyžádání stránky vrátí vlastnost post hodnotu false. Pokud však kliknete na tlačítko nebo jinak odešlete stránku – to znamená, že příspěvek vrátí hodnotu true. Proto umožňuje určit, zda se chystáte odeslat formulář. (V případě příkazů HTTP, pokud je požadavek operace GET, vrátí funkce WebPost hodnotu false. Pokud je požadavek operace POST, vrátí funkce Turn hodnotu true.) V pozdějším kurzu budete pracovat se vstupními formuláři, kde se tento test stane obzvlášť užitečný.

Spusťte stránku. Vzhledem k tomu, že se jedná o první stránku, kterou požadujete, se zobrazí zpráva "Toto je první požadavek na stránku". Tento řetězec je hodnota, na kterou jste inicializovali proměnnou zprávy. Existuje test if (-post), ale který vrátí hodnotu false v okamžiku, takže se kód uvnitř bloku If nespustí.

Klikněte na tlačítko **Odeslat** . Stránka je znovu vyžádána. Stejně jako předtím je proměnná zprávy nastavena na hodnotu "Toto je poprvé...". Tentokrát ale test if ("post") vrátí hodnotu true, takže kód uvnitř bloku If se spustí. Kód změní hodnotu proměnné zprávy na jinou hodnotu, která je vykreslena v označení.

Nyní do značky přidejte podmínku if. Pod prvkem &lt;p&gt;, který obsahuje tlačítko **Odeslat** , přidejte následující kód:

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample9.cshtml)]

Do značky přidáváte kód, takže je nutné začít s @. Pak je k dispozici test, který je podobný jako ten, který jste přidali dříve v bloku kódu. Ve složených závorkách, ale přidáváte obyčejné HTML – alespoň, je běžné, dokud nezíská @DateTime.Now. Toto je další trochu kódu Razor, proto je třeba před ním přidat @.

Zde je uvedeno, že můžete přidat podmínky if v bloku kódu v horní části i ve značce. Použijete-li podmínku IF v těle stránky, mohou být řádky uvnitř bloku značkami nebo kódem. V takovém případě, a když je hodnota true, kdykoli budete kombinovat značky a kód, je nutné použít @, aby bylo jasné, že je kód ASP.NET.

Spusťte stránku a klikněte na **Odeslat**. Tentokrát při odeslání ("teď, co jste odeslali...") k zobrazení jiné zprávy, ale zobrazí se nová zpráva se seznamem data a času.

![Stránka test Razor 2 spuštěná v prohlížeči s časovým razítkem zobrazeným po odeslání](intro-to-web-pages-programming/_static/image4.png)

### <a name="testing-the-value-of-a-query-string"></a>Testování hodnoty řetězce dotazu

Ještě jeden test. Tentokrát přidáte blok if, který testuje hodnotu s názvem show, která se může předat v řetězci dotazu. (Takto: `http://localhost:43097/TestRazorPart2.cshtml?show=true`) Stránku změníte tak, aby se zobrazila zpráva, kterou jste zobrazili ("Toto je poprvé..." atd.), zobrazí se pouze v případě, že je hodnota zobrazit pravdivá.

V dolní části (ale uvnitř) blok kódu v horní části stránky přidejte následující:

[!code-csharp[Main](intro-to-web-pages-programming/samples/sample10.cs)]

Celý blok kódu teď vypadá jako v následujícím příkladu. (Pamatujte na to, že při kopírování kódu na stránku může odsazení vypadat jinak. To ale nemá vliv na to, jak se kód spouští.)

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample11.cshtml)]

Nový kód v bloku inicializuje proměnnou s názvem showMessage na hodnotu false. Pak provede test if pro vyhledání hodnoty v řetězci dotazu. Když poprvé vyžádáte stránku, má adresu URL, jako je tato:

`http://localhost:43097/TestRazorPart2.cshtml`

Kód určuje, zda adresa URL obsahuje proměnnou s názvem show v řetězci dotazu, jako je tato verze adresy URL:

`http://localhost:43097/TestRazorPart2.cshtml`? show = true

Test sám se podívá na vlastnost QueryString objektu Request. Pokud řetězec dotazu obsahuje položku s názvem show a pokud je tato položka nastavena na hodnotu true, spustí se blok if a nastaví proměnnou showMessage na hodnotu true.

Tady je nějaký štych, jak vidíte. Podobně jako název říká, řetězec dotazu je řetězec. Pokud je testovaná hodnota logická hodnota (true/false), můžete otestovat jenom na true a false. Než budete moci otestovat hodnotu proměnné show v řetězci dotazu, je nutné ji převést na logickou hodnotu. To je to, co metoda AsBool dělá – bere řetězec jako vstup a převede ho na logickou hodnotu. Jasně, pokud je řetězec "true", metoda AsBool převede tuto hodnotu na true. Pokud hodnota řetězce je cokoliv jiného, AsBool vrátí false.

> [!TIP] 
> 
> **Datové typy a metody as ()**
> 
> Zjistili jsme, že když vytvoříte proměnnou, použijete klíčové slovo var. To není celý příběh, ale. Aby bylo možné manipulovat s hodnotami – přidat čísla nebo zřetězit řetězce nebo porovnat kalendářní data nebo otestovat hodnotu true/false, C# musí fungovat s odpovídající interní reprezentace hodnoty. C#může *obvykle* zjistit, co by mělo být znázorněno (to znamená, co je třeba *zadat* data) na základě toho, co děláte s hodnotami. Teď to nemůže udělat. V takovém případě je nutné, abyste byli výslovně uvedeni C# , jak by měla představovat data. Metoda AsBool to znamená, C# že hodnota řetězce "true" nebo "false" by měla být považována za logickou hodnotu. Podobné metody existují také pro reprezentace řetězců jako jiné typy, jako je například AsInt (považovat za celé číslo), AsDateTime (považovat za typ datum/čas), AsFloat (považovat za číslo s plovoucí desetinnou čárkou) a tak dále. Při použití těchto metod as (), pokud C# nemůže reprezentovat řetězcovou hodnotu, jak je požadováno, zobrazí se chyba.

V označení stránky odeberte tento prvek nebo ho Odkomentujte (tady je zobrazený komentovaný):

[!code-html[Main](intro-to-web-pages-programming/samples/sample12.html)]

Přímo tam, kde jste tento text odebrali nebo do něj zakomentovatte, přidejte následující:

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample13.cshtml)]

Test if říká, že pokud je proměnná showMessage true, vykreslí&gt; prvek &lt;p s hodnotou proměnné zprávy.

### <a name="summary-of-your-conditional-logic"></a>Souhrn podmíněné logiky

V případě, že si nejste naprosto jisti, co jste právě udělali, tady je souhrn.

- Proměnná zprávy je inicializovaná na výchozí řetězec ("Toto je první čas...").
- Pokud je žádost stránky výsledkem odeslání (post), hodnota zprávy se změní na nyní, co jste odeslali...
- Proměnná showMessage je inicializovaná na hodnotu false.
- Pokud řetězec dotazu obsahuje? show = true, proměnná showMessage je nastavena na hodnotu true.
- V kódu, pokud je showMessage true, je vykreslen&gt; prvek &lt;p, který zobrazuje hodnotu zprávy. (Pokud má showMessage hodnotu false, v tomto okamžiku se v označení nic nevykresluje.)
- Pokud se v označení jedná o příspěvek, je vykreslen&gt; prvek &lt;p, který zobrazuje datum a čas.

Spusťte stránku. K dispozici není žádná zpráva, protože showMessage má hodnotu false, takže v označení if (showMessage) test vrátí false.

Klikněte na **Odeslat**. Zobrazí se datum a čas, ale stále žádná zpráva.

V prohlížeči přejděte do pole Adresa URL a přidejte následující na konec adresy URL:? show = true a potom stiskněte klávesu ENTER.

![Stránka test Razor 2 v prohlížeči ukazující řetězec dotazu](intro-to-web-pages-programming/_static/image5.png)

Stránka se zobrazí znovu. (Protože jste změnili adresu URL, jedná se o novou žádost, ne Odeslat.) Znovu klikněte na **Odeslat** . Zpráva se zobrazí znovu, jako je datum a čas.

![Stránka test Razor 2 po odeslání, když je řetězec dotazu](intro-to-web-pages-programming/_static/image6.png)

V adrese URL změňte? show = true na? show = false a stiskněte klávesu ENTER. Odešlete stránku znovu. Stránka se vrátí k způsobu, jakým jste začali – bez zprávy.

Jak bylo uvedeno dříve, logika tohoto příkladu je trochu contrived. Pokud se ale objeví v řadě vašich stránek, bude pobírat jedna nebo více formulářů, které jste si poznamenali.

## <a name="installing-a-helper-displaying-a-gravatar-image"></a>Instalace pomocné rutiny (zobrazení obrázku Gravatar)

Některé úlohy, které uživatelé často chtějí dělat na webových stránkách, vyžadují velké množství kódu nebo vyžadují další znalosti. Příklady: zobrazení grafu pro data; Vložení tlačítka pro Facebook "jako" na stránku; odesílání e-mailů z webu oříznutí a změna velikosti imagí; používání služby PayPal pro váš web. Aby bylo možné tyto druhy věcí snadno provést, ASP.NET webové stránky vám umožní používat *pomocníka*. Pomocníky jsou komponenty, které nainstalujete pro lokalitu a umožňují provádět typické úlohy pomocí pouze několika řádků kódu Razor.

ASP.NET webové stránky mají několik vestavěných pomocníků. Mnoho pomocníků je však dostupných v balíčcích (Doplňky), které jsou k dispozici pomocí Správce balíčků NuGet. NuGet umožňuje vybrat balíček, který se má nainstalovat, a pak se postará o všechny podrobnosti o instalaci.

V této části kurzu nainstalujete pomocníka, který vám umožní zobrazit obrázek Gravatar ("globálně rozpoznaný Avatar"). Naučíte se dvě věci. Jedním z nich je najít a nainstalovat pomocníka. Naučíte se také, jak pomáhající pomoc usnadňuje něco, co byste jinak potřebovali udělat pomocí velkého množství kódu, který byste si museli napsat sami.

Vlastní Gravatar můžete zaregistrovat na webu Gravatar na [http://www.gravatar.com/](http://www.gravatar.com/), ale pro provedení této části kurzu není nutné vytvořit účet Gravatar.

V části WebMatrix klikněte na tlačítko **NuGet** .

![Dialogové okno galerie NuGet v WebMatrixu](intro-to-web-pages-programming/_static/image7.png)

Spustí se správce balíčků NuGet a zobrazí dostupné balíčky. (Ne všechny balíčky jsou pomocníky. některé funkce přidávají do samotné WebMatrixu, některé jsou další šablony atd.) Může se zobrazit chybová zpráva o nekompatibilitě verzí. Tuto chybovou zprávu můžete ignorovat kliknutím na **OK** a pokračováním v tomto kurzu.

![Dialogové okno galerie NuGet v WebMatrixu](intro-to-web-pages-programming/_static/image8.png)

Do vyhledávacího pole zadejte "asp.net helps". NuGet zobrazuje balíčky, které splňují hledané výrazy.

![Galerie NuGet v WebMatrixu zobrazující balíčky](intro-to-web-pages-programming/_static/image9.png)

Knihovna webových pomocníků ASP.NET obsahuje kód, který zjednodušuje mnoho běžných úloh, včetně použití imagí Gravatar. Vyberte balíček **knihovny webových pomocníků ASP.NET** a pak kliknutím na **instalovat** spusťte instalační program. Po zobrazení výzvy vyberte možnost **Ano** , pokud chcete balíček nainstalovat, a přijměte podmínky pro dokončení instalace.

A to je vše. NuGet stáhne a nainstaluje vše včetně dalších součástí, které mohou být požadovány (*závislosti*).

Pokud z nějakého důvodu potřebujete odinstalovat pomoc, je tento proces velmi podobný. Klikněte na tlačítko **NuGet** , klikněte na kartu **nainstalované** a vyberte balíček, který chcete odinstalovat.

## <a name="using-a-helper-in-a-page"></a>Použití pomocné rutiny na stránce

Teď budete používat pomocníka, kterou jste právě nainstalovali. Proces přidávání pomocníka na stránku je podobný pro většinu pomocníků.

V WebMatrixu vytvořte stránku a pojmenujte ji *GravatarTest. cshml*. (Vytváříte speciální stránku pro otestování pomocníka, ale pomocníky můžete používat na libovolné stránce webu.)

Uvnitř &lt;tělo&gt; elementu přidejte prvek &lt;div&gt; element. Do prvku &lt;div&gt; elementu zadejte tento příkaz:

@Gravatar.

Znak @ je stejný znak, který jste použili k označení kódu Razor. **Gravatar** je objekt pomocníka, se kterým pracujete.

Jakmile zadáte tečku (.), WebMatrix zobrazí seznam *metod* (funkcí), které Gravatar pomoc zpřístupňuje:

![Rozevírací seznam Gravatar Helper IntelliSense](intro-to-web-pages-programming/_static/image10.png)

Tato funkce se označuje jako *IntelliSense*. Pomůže vám s kódem tím, že poskytuje kontextově vhodné volby. Technologie IntelliSense spolupracuje s HTML, CSS, ASP.NET kódem, JavaScriptem a dalšími jazyky, které jsou podporovány v WebMatrixu. Je to jiná funkce, která usnadňuje vývoj webových stránek ve WebMatrixu.

Na klávesnici stiskněte G a uvidíte, že technologie IntelliSense najde metodu gethtml. Stiskněte klávesu TAB. technologie IntelliSense Vloží vybranou metodu (gethtml). Zadejte levou závorku a Všimněte si, že je automaticky přidána uzavírací závorka. Zadejte svou e-mailovou adresu do uvozovek mezi dvě závorky. Pokud máte účet Gravatar, vrátí se Váš profilový obrázek. Pokud nemáte účet Gravatar, vrátí se výchozí obrázek. Až budete hotovi, čára bude vypadat takto:

[!code-css[Main](intro-to-web-pages-programming/samples/sample14.css)]

Nyní zobrazí stránku v prohlížeči. Zobrazí se váš obrázek nebo výchozí obrázek v závislosti na tom, jestli máte účet Gravatar.

![Gravatar](intro-to-web-pages-programming/_static/image11.png) ![výchozí obrázek](intro-to-web-pages-programming/_static/image12.png)

Chcete-li získat představu o tom, co vám pomocník dělá, zobrazte zdroj stránky v prohlížeči. Spolu s kódem HTML, který jste měli na stránce, vidíte prvek obrázku, který obsahuje identifikátor. Toto je kód, který pomocník vykresluje na stránce místo, kde jste měli @Gravatar.GetHtml. Pomocník převzal informace, které jste zadali, a vygeneroval kód, který se domluví přímo do Gravatar, aby se vrátila správná image pro zadaný účet.

Metoda gethtml také umožňuje přizpůsobení obrázku zadáním dalších parametrů. Následující kód ukazuje, jak vyžádat obrázek má šířku a výšku 40 pixelů a používá zadanou výchozí image s názvem **wavatar** , pokud zadaný účet neexistuje.

[!code-javascript[Main](intro-to-web-pages-programming/samples/sample15.js)]

Tento kód vytváří něco podobného jako následující výsledek (výchozí obrázek se náhodně liší).

![](intro-to-web-pages-programming/_static/image13.png)

## <a name="coming-up-next"></a>Připravujeme další

Abychom tento kurz mohli zkrátit, museli jsme se soustředit jenom na několik základních informací. Přirozeně existuje *mnohem více pro* Razor a C#. Další informace najdete v těchto kurzech. Pokud vás zajímá více o programování aspektů Razor a C# hned teď, můžete si přečíst důkladnější Úvod: [Úvod do webového programování ASP.NET pomocí syntaxe Razor](https://go.microsoft.com/fwlink/?LinkID=202890).

V dalším kurzu se seznámíte s prací s databází. V tomto kurzu začnete vytvářet ukázkovou aplikaci, která vám umožní vytvořit seznam oblíbených filmů.

## <a name="complete-listing-for-testrazor-page"></a>Úplný výpis pro stránku TestRazor

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample16.cshtml)]

## <a name="complete-listing-for-testrazorpart2-page"></a>Úplný výpis pro stránku TestRazorPart2

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample17.cshtml)]

## <a name="complete-listing-for-gravatartest-page"></a>Úplný výpis pro stránku GravatarTest

[!code-cshtml[Main](intro-to-web-pages-programming/samples/sample18.cshtml)]

## <a name="additional-resources"></a>Další prostředky

- [Seznámení s ASP.NET webovým programováním pomocí syntaxe Razor](https://go.microsoft.com/fwlink/?LinkID=202890)
- [Pomocník pro Twitter](../../ui-layouts-and-themes/twitter-helper.md)

> [!div class="step-by-step"]
> [Předchozí](getting-started.md)
> [Další](displaying-data.md)

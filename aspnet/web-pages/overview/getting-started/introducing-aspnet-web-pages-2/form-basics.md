---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
title: Představení webových stránek ASP.NET – základy formulářů HTML | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se dozvíte základní informace o tom, jak vytvořit vstupní formulář a jak zpracovat vstup uživatele, když používáte webové stránky ASP.NET (Razor). A teď...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: 81ed82bf-b940-44f1-b94a-555d0cb7cc98
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/form-basics
msc.type: authoredcontent
ms.openlocfilehash: f57661077ec3bb13f3d4ec41b130bda4d2fb9070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574282"
---
# <a name="introducing-aspnet-web-pages---html-form-basics"></a>Představení webových stránek ASP.NET – základy formulářů HTML

tím, že [FitzMacken](https://github.com/tfitzmac)

> V tomto kurzu se dozvíte základní informace o tom, jak vytvořit vstupní formulář a jak zpracovat vstup uživatele, když používáte webové stránky ASP.NET (Razor). A teď, když máte databázi, budete používat své dovednosti v podobě, aby uživatelé mohli v databázi najít konkrétní filmy. Předpokládá se, že jste dokončili řadu prostřednictvím [úvodního zobrazení dat pomocí webových stránek ASP.NET](/aspnet/web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data).
> 
> Naučíte se:
> 
> - Vytvoření formuláře pomocí standardních prvků jazyka HTML.
> - Způsob čtení vstupu uživatele ve formuláři.
> - Postup vytvoření dotazu SQL, který selektivně načte data pomocí hledaného termínu, který uživatel dodá.
> - Jak mít pole na stránce "pamatovat", co uživatel zadal.
>   
> 
> Popsané funkce a technologie:
> 
> - Objekt `Request`
> - Klauzule `Where` SQL.

## <a name="what-youll-build"></a>Co sestavíte

V předchozím kurzu jste vytvořili databázi, přidali do ní data a pak jste pomocí pomocníka `WebGrid` zobrazili data. V tomto kurzu přidáte vyhledávací pole, které vám umožní najít filmy konkrétního žánru nebo jeho titul, který bude obsahovat jakékoli slovo, které zadáte. (Například budete moci najít všechny filmy, jejichž Žánr je "Action" nebo jehož název obsahuje "Harry" nebo "Adventure.")

Po dokončení tohoto kurzu budete mít stránku, jako je tato:

![Stránka filmy s hledáním žánru a nadpisu](form-basics/_static/image1.png)

Část stránky výpisu je stejná jako v posledním kurzu &mdash; mřížce. Rozdílem bude, že v mřížce se zobrazí pouze filmy, které jste hledali.

## <a name="about-html-forms"></a>O formulářích HTML

(Pokud máte zkušenosti s vytvářením formulářů HTML a rozdílem mezi `GET` a `POST`, můžete tuto část přeskočit.)

Formulář obsahuje prvky uživatelského vstupu &mdash; textových polí, tlačítek, přepínačů, zaškrtávacích políček, rozevíracích seznamech atd. Uživatelé tyto ovládací prvky vyplní nebo provedou výběry a pak formulář odešlou kliknutím na tlačítko.

Základní syntaxe HTML formuláře je znázorněna v tomto příkladu:

[!code-html[Main](form-basics/samples/sample1.html)]

Když se tento kód spustí na stránce, vytvoří jednoduchý tvar, který bude vypadat jako na následujícím obrázku:

![Základní HTML formulář jako vykreslený v prohlížeči](form-basics/_static/image2.png)

Element `<form>` obklopuje elementy HTML, které se mají odeslat. (Snadná chyba je, aby bylo možné přidat prvky na stránku, ale pak je zapomenout, aby byly vloženy do prvku `<form>`. V takovém případě není nic odesláno.) Atribut `method` oznamuje prohlížeči, jak odeslat vstup uživatele. Tuto hodnotu nastavíte na `post`, pokud provádíte aktualizaci na serveru nebo `get`, pokud načítáte data ze serveru.

<a id="GET,_POST,_and_HTTP_Verb_Safety"></a>

> [!TIP] 
> 
> **Zabezpečení operací GET, POST a HTTP**
> 
> HTTP, protokol, který prohlížeče a servery používají k výměně informací, je výjimečně jednoduché v základních operacích. Prohlížeče při vytváření požadavků na servery používají jenom několik příkazů. Při psaní kódu pro web je užitečné pochopit tyto příkazy a způsob jejich použití v prohlížeči a na serveru. A daleko nejčastěji používané operace jsou tyto:
> 
> - `GET`. Prohlížeč používá tuto operaci k načtení něčeho ze serveru. Když například zadáte adresu URL do prohlížeče, prohlížeč provede operaci `GET` a vyžádá si požadovanou stránku. Pokud stránka obsahuje grafiku, prohlížeč pro získání imagí provede další operace `GET`. Pokud `GET` operace musí předat informace na server, informace se předávají jako součást adresy URL v řetězci dotazu.
> - `POST`. Prohlížeč pošle žádost o `POST`, aby mohla odesílat data, která se mají přidat nebo změnit na serveru. Například příkaz `POST` slouží k vytváření záznamů v databázi nebo změně existujících. Ve většině případů, když vyplníte formulář a kliknete na tlačítko Odeslat, prohlížeč provede operaci `POST`. V operaci `POST` se data předávaná na server nachází v těle stránky.
> 
> Důležitým rozdílem mezi těmito operacemi je, že operace `GET` není třeba měnit cokoli na serveru, nebo ji vložit do trochu abstraktního způsobu, `GET` operace nevede ke změně stavu na serveru. Operaci `GET` můžete provádět u stejných prostředků tolikrát, kolikrát chcete, a tyto prostředky se nezmění. (Operace `GET` je často označována jako "bezpečná" nebo "použití technického období", je *idempotentní*.) Naproti tomu `POST` požadavek na server mění při každém provedení operace něco na serveru.
> 
> Toto rozlišení vám může ukázat dva příklady. Když provedete vyhledávání pomocí modulu, jako je například Bing nebo Google, vyplníte formulář, který se skládá z jednoho textového pole, a kliknete na tlačítko Hledat. Prohlížeč provede operaci `GET` s hodnotou, kterou jste zadali do pole předaného jako součást adresy URL. Použití operace `GET` pro tento typ formuláře je přesné, protože operace vyhledávání nemění žádné prostředky na serveru, pouze načítá informace.
> 
> Nyní zvažte proces řazení do online režimu. Vyplníte podrobnosti objednávky a potom kliknete na tlačítko Odeslat. Tato operace bude `POST` požadavek, protože výsledkem operace budou změny na serveru, jako je například nový záznam objednávky, změna informací o účtu a pravděpodobně mnoho dalších změn. Na rozdíl od operace `GET` nemůžete žádost o `POST` opakovat – Pokud jste to provedli, vygenerujete novou objednávku na serveru. (V takových případech se na webech často varuje, že nekliknete na tlačítko Odeslat více než jednou, nebo zakážete tlačítko Odeslat, aby nedošlo k nechtěnému opakovanému odeslání formuláře.)
> 
> V průběhu tohoto kurzu budete pracovat s formuláři HTML pomocí operace `GET` a operace `POST`. V každém z těchto případů vybereme vysvětlení, proč je to ten, co používáte.
> 
> (Další informace o příkazech HTTP naleznete v článku [definice metod](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) na webu W3C.)

Většina prvků uživatelského vstupu je `<input>` prvky HTML. Vypadají jako `<input type="type" name="name">,`, kde *typ* určuje druh ovládacího prvku pro zadávání uživatelského vstupu, který chcete. Tyto prvky jsou společné:

- Textové pole: `<input type="text">`
- Zaškrtávací políčko: `<input type="check">`
- Přepínač: `<input type="radio">`
- Tlačítko: `<input type="button">`
- Tlačítko Odeslat: `<input type="submit">`

Pomocí elementu `<textarea>` lze také vytvořit víceřádkové textové pole a prvek `<select>` k vytvoření rozevíracího seznamu nebo rolovacího seznamu. (Další informace o prvcích formuláře HTML najdete v tématu [formuláře HTML a vstup](http://www.w3schools.com/html/html_forms.asp) na webu w3schools.)

Atribut `name` je velmi důležitý, protože název představuje způsob, jakým se získá hodnota elementu později, jak uvidíte za chvíli.

Zajímavá část je to, co jste vy, vývojář stránky dělat se vstupem uživatele. K těmto prvkům není přidruženo žádné integrované chování. Místo toho musíte získat hodnoty, které uživatel zadal nebo vybral, a s nimi pracovat. To je to, co se v tomto kurzu naučíte.

> [!TIP] 
> 
> **HTML5 a vstupní formuláře**
> 
> Jak je to možné, HTML je v přechodu a nejnovější verze (HTML5) obsahuje podporu pro více intuitivních způsobů, jak mohou uživatelé zadávat informace. Například v HTML5 můžete (vývojář stránky) sdělit stránku, na kterou má uživatel zadat datum. Prohlížeč pak může automaticky zobrazit kalendář, aniž by uživatel musel zadat datum ručně. HTML5 je však novinkou a ve všech prohlížečích ještě není podporováno.
> 
> Webové stránky ASP.NET podporují vstup HTML5 do rozsahu, který je v prohlížeči uživatele. Představu o nových atributech `<input>` elementu v HTML5 najdete v tématu [atribut typu input&gt; &lt;HTML](http://www.w3schools.com/html/html_form_input_types.asp) na webu w3schools.

## <a name="creating-the-form"></a>Vytvoření formuláře

Ve WebMatrixu v pracovním prostoru **soubory** otevřete stránku *filmy. cshtml* .

Za uzavírací značku `</h1>` a před otevírací `<div>`ovou značku `grid.GetHtml` volání přidejte následující kód:

[!code-html[Main](form-basics/samples/sample2.html)]

Tento kód vytvoří formulář, který obsahuje textové pole s názvem `searchGenre` a tlačítko Odeslat. Textové pole a tlačítko Odeslat jsou uzavřeny v elementu `<form>`, jehož atribut `method` je nastaven na `get`. (Nezapomeňte, že pokud textové pole nevložíte a kliknete na tlačítko Odeslat uvnitř prvku `<form>`, nebude se po kliknutí na tlačítko odesílat žádná data.) Tady můžete použít `GET` sloveso, protože vytváříte formulář, který na serveru neprovede žádné změny – výsledkem je hledání. (V předchozím kurzu jste použili metodu `post`, což je způsob, jakým odešlete změny na server. Uvidíte, že v dalším kurzu znovu.)

Spusťte stránku. I když jste nedefinovali žádné chování formuláře, vidíte, co vypadá takto:

![Stránka filmy s vyhledávacím polem pro Žánr](form-basics/_static/image3.png)

Do textového pole zadejte hodnotu, například "komedie". Pak klikněte na **Hledat Žánr**.

Poznamenejte si adresu URL stránky. Vzhledem k tomu, že jste nastavili atribut `method` elementu `<form>` na hodnotu `get`, hodnota, kterou jste zadali, je teď součástí řetězce dotazu v adrese URL, třeba takto:

`http://localhost:45661/Movies.cshtml?searchGenre=Comedy`

## <a name="reading-form-values"></a>Čtení hodnot formuláře

Stránka již obsahuje nějaký kód, který získá data databáze a zobrazí výsledky v mřížce. Nyní je nutné přidat kód, který přečte hodnotu textového pole, abyste mohli spustit dotaz SQL, který obsahuje hledaný termín.

Vzhledem k tomu, že jste nastavili metodu formuláře na `get`, můžete si přečíst hodnotu, která byla zadána do textového pole, pomocí kódu podobného následujícímu:

`var searchTerm = Request.QueryString["searchGenre"];`

Objekt `Request.QueryString` (vlastnost `QueryString` objektu `Request`) obsahuje hodnoty prvků, které byly odeslány jako součást operace `GET`. Vlastnost `Request.QueryString` obsahuje *kolekci* (seznam) hodnot, které jsou odeslány ve formuláři. Chcete-li získat konkrétní hodnotu, zadejte název prvku, který chcete. To je důvod, proč musíte mít atribut `name` u elementu `<input>` (`searchTerm`), který vytvoří textové pole. (Další informace o objektu `Request` naleznete v [postranním panelu](#BKMK_TheRequestObject) později.)

Je dostatečně snadné číst hodnotu textového pole. Pokud ale uživatel v textovém poli vůbec nezadal cokoli, ale na tlačítko **Hledat** , můžete ho ignorovat, protože není k dispozici žádné hledání.

Následující kód je příklad, který ukazuje, jak implementovat tyto podmínky. (Tento kód ještě nemusíte přidávat. za chvilku to provedete.)

[!code-csharp[Main](form-basics/samples/sample3.cs)]

Test rozdělí tímto způsobem:

- Získat hodnotu `Request.QueryString["searchGenre"]`, konkrétně hodnotu, která byla zadána do prvku `<input>` s názvem `searchGenre`.
- Zjistěte, jestli je prázdný pomocí metody `IsEmpty`. Tato metoda je standardní způsob, jak určit, zda něco (například element Form) obsahuje hodnotu. Ale opravdu se zajímáte jenom v případě, že *není* prázdné, proto...
- Před testem `IsEmpty` přidejte operátor `!`. (Operátor `!` znamená logický NOT).

V prostém jazyce English je celý `if` podmínka přeložena do následujícího: *Pokud není element searchGenre formuláře prázdný, pak...*

Tento blok nastaví fázi pro vytvoření dotazu, který používá hledaný termín. Provedete to v další části.

<a id="BKMK_TheRequestObject"></a>

> [!TIP] 
> 
> **Objekt žádosti**
> 
> Objekt `Request` obsahuje všechny informace, které prohlížeč posílá do vaší aplikace, když je vyžádána nebo odeslána stránka. Tento objekt obsahuje všechny informace, které uživatel poskytuje, jako jsou například hodnoty textového pole nebo soubor k nahrání. Zahrnuje také všechny druhy dalších informací, jako jsou soubory cookie, hodnoty v řetězci dotazu adresy URL (pokud existují), cestu k souboru na spuštěné stránce, typ prohlížeče, který uživatel používá, seznam jazyků, které jsou nastaveny v prohlížeči. a mnoho dalšího.
> 
> Objekt `Request` je *kolekce* (seznam) hodnot. Z kolekce získáte jednotlivou hodnotu zadáním jejího názvu:
> 
> `var someValue = Request["name"];`
> 
> Objekt `Request` ve skutečnosti zveřejňuje několik dílčích sad. Příklad:
> 
> - `Request.Form` poskytuje hodnoty z prvků v odeslaném `<form>` elementu, pokud je požadavek `POST` požadavek.
> - `Request.QueryString` poskytuje pouze hodnoty v řetězci dotazu adresy URL. (V adrese URL, jako je například `http://mysite/myapp/page?searchGenre=action&page=2`, je oddíl `?searchGenre=action&page=2` v adrese URL řetězec dotazu.)
> - kolekce `Request.Cookies` umožňuje přístup k souborům cookie, které prohlížeč odeslal.
> 
> Pokud chcete získat hodnotu, o kterou víte, že je v odeslaném formuláři, můžete použít `Request["name"]`. Alternativně můžete použít konkrétnější verze `Request.Form["name"]` (pro `POST` požadavků) nebo `Request.QueryString["name"]` (pro `GET` požadavky). Samozřejmě je *název* položky, kterou chcete získat.
> 
> Název položky, kterou chcete získat, musí být jedinečný v rámci kolekce, kterou používáte. To je důvod, proč objekt `Request` poskytuje podmnožiny jako `Request.Form` a `Request.QueryString`. Předpokládejme, že stránka obsahuje element formuláře s názvem `userName` a obsahuje *také* soubor cookie s názvem `userName`. Pokud získáte `Request["userName"]`, je nejednoznačné, zda chcete mít hodnotu formuláře nebo soubor cookie. Pokud však získáte `Request.Form["userName"]` nebo `Request.Cookie["userName"]`, budete přesně o tom, která hodnota má být získána.
> 
> Je dobrým zvykem určit a využít podmnožinu `Request`, na kterou vás zajímáte, jako je `Request.Form` nebo `Request.QueryString`. Pro jednoduché stránky, které v tomto kurzu vytváříte, to pravděpodobně nevede k žádným rozdílům. Při vytváření složitějších stránek ale pomocí explicitní verze `Request.Form` nebo `Request.QueryString` může pomoci vyhnout se problémům, které mohou nastat, když stránka obsahuje formulář (nebo více formulářů), soubory cookie, hodnoty řetězce dotazu a tak dále.

## <a name="creating-a-query-by-using-a-search-term"></a>Vytvoření dotazu pomocí hledaného termínu

Když teď víte, jak získat hledaný termín, který zadal uživatel, můžete vytvořit dotaz, který ho používá. Nezapomeňte, že pokud chcete všechny položky videa získat z databáze, budete používat dotaz SQL, který vypadá jako tento příkaz:

`SELECT * FROM Movies`

Chcete-li získat pouze některé filmy, je nutné použít dotaz, který obsahuje klauzuli `Where`. Tato klauzule vám umožní nastavit podmínku, na které se v dotazu vrátí řádky. Tady je příklad:

`SELECT * FROM Movies WHERE Genre = 'Action'`

Základní formát je `WHERE column = value`. V závislosti na tom, co hledáte, můžete použít různé operátory kromě `=`, jako je `>` (větší než), `<` (menší než), `<>` (nerovná se), `<=` (menší než nebo rovno) atd.

V případě, že se zajímáte, příkazy SQL nerozlišují velká a malá písmena &mdash; `SELECT` jsou stejné jako `Select` (nebo dokonce `select`). Lidé ale často nemají klíčová slova v příkazu SQL, jako je `SELECT` a `WHERE`, aby se usnadnilo jejich čtení.

### <a name="passing-the-search-term-as-a-parameter"></a>Předání hledaného termínu jako parametru

Hledání konkrétního žánru je dostatečně snadné (`WHERE Genre = 'Action'`), ale chcete být schopni vyhledat jakýkoliv Žánr, který uživatel zadal. Provedete to tak, že vytvoříte dotaz SQL, který obsahuje zástupný symbol pro hledanou hodnotu. Bude vypadat podobně jako tento příkaz:

`SELECT * FROM Movies WHERE Genre = @0`

Zástupný symbol je `@` znak následovaný nulou. Jak můžete odhadnout, dotaz může obsahovat několik zástupných symbolů a má název `@0`, `@1`, `@2`atd.

Chcete-li nastavit dotaz a skutečně ho předat jako hodnotu, použijte následující kód:

[!code-sql[Main](form-basics/samples/sample4.sql)]

Tento kód je podobný tomu, co jste už provedli k zobrazení dat v mřížce. Jedinými rozdíly jsou:

- Dotaz obsahuje zástupný symbol (`WHERE Genre = @0"`).
- Dotaz je vložen do proměnné (`selectCommand`); předtím jste předali dotaz přímo metodě `db.Query`.
- Při volání metody `db.Query` předáte dotaz i hodnotu, která se má použít pro zástupný text. (Pokud má dotaz více zástupných symbolů, měli byste je předat jako samostatné hodnoty do metody.)

Pokud všechny tyto prvky vložíte dohromady, získáte následující kód:

[!code-csharp[Main](form-basics/samples/sample5.cs)]

> [!NOTE] 
> 
> **Významná!** Použití zástupných symbolů (například `@0`) k předávání hodnot příkazu SQL je *mimořádně důležité* pro zabezpečení. Způsob, jakým se tady vidíte, představuje zástupné symboly pro data proměnných, je jediným způsobem, jak byste měli vytvořit příkazy SQL.
> 
> Příkaz SQL nikdy neseskupte vložením (zřetězení) literálového textu a hodnot, které obdržíte od uživatele. Zřetězení vstupu uživatele do příkazu SQL otevře váš web s *útokem na injektáže SQL* , kde uživatel se zlými úmysly odešle hodnoty na stránku, která by proznala vaši databázi. (Další informace si můžete přečíst v článku [SQL vložení](https://msdn.microsoft.com/library/ms161953.aspx) webu MSDN.)

## <a name="updating-the-movies-page-with-search-code"></a>Aktualizace stránky filmů pomocí vyhledávacího kódu

Nyní můžete aktualizovat kód v souboru *Movies. cshtml* . Chcete-li začít, nahraďte kód v bloku kódu v horní části stránky tímto kódem:

[!code-csharp[Main](form-basics/samples/sample6.cs)]

Rozdíl je v tom, že jste dotaz umístili do proměnné `selectCommand`, kterou předáte `db.Query` později. Vložení příkazu SQL do proměnné umožňuje změnit příkaz, který provedete k provedení hledání.

Odebrali jste také tyto dva řádky, které později vrátíte:

[!code-csharp[Main](form-basics/samples/sample7.cs)]

Dotaz ještě nechcete spustit (to znamená volání `db.Query`) a nechcete inicializovat pomocnou nápovědu `WebGrid`. Tyto věci provedete po zjištění, který příkaz SQL musí být spuštěn.

Po provedení tohoto přepsaného bloku můžete přidat novou logiku pro zpracování vyhledávání. Dokončený kód bude vypadat jako následující. Aktualizujte kód na stránce tak, aby odpovídal následujícímu příkladu:

[!code-cshtml[Main](form-basics/samples/sample8.cshtml)]

Stránka teď funguje podobně. Při každém spuštění stránky kód otevře databázi a proměnná `selectCommand` je nastavena na příkaz jazyka SQL, který získá všechny záznamy z tabulky `Movies`. Kód také inicializuje proměnnou `searchTerm`.

Nicméně pokud aktuální požadavek obsahuje hodnotu pro `searchGenre` element, kód nastaví `selectCommand` na jiný dotaz – konkrétně na jeden, který obsahuje klauzuli `Where` pro hledání žánru. Také nastavuje `searchTerm` pro pole hledání, které bylo předáno (což může být nic).

Bez ohledu na to, který příkaz SQL je v `selectCommand`, kód pak zavolá `db.Query` a spustí dotaz, který předává, ať už je v `searchTerm`. Pokud neexistuje žádný `searchTerm`, nezáleží na tom, protože v takovém případě neexistuje parametr pro předání hodnoty do `selectCommand` přesto.

Nakonec kód inicializuje pomoc `WebGrid` pomocí výsledků dotazu, stejně jako předtím.

Můžete vidět, že vložením příkazu jazyka SQL a hledaného termínu do proměnných jste přidali flexibilitu kódu. Jak vidíte později v tomto kurzu, můžete použít tuto základní architekturu a nechat přidat logiku pro různé typy hledání.

## <a name="testing-the-search-by-genre-feature"></a>Testování funkce hledání podle žánru

Ve WebMatrixu spusťte stránku *filmy. cshtml* . Zobrazí se stránka s textovým polem pro Žánr.

Zadejte Žánr, který jste zadali pro jeden ze záznamů testu, a pak klikněte na **Hledat**. Tentokrát se zobrazí seznam pouze filmů, které odpovídají danému žánru:

![Seznam filmů po hledání žánru](form-basics/_static/image4.png)

Zadejte jiný Žánr a znovu proveďte hledání. Zkuste zadat Žánr pomocí všech malých a velkých písmen, abyste viděli, že hledání nerozlišuje malá a velká písmena.

## <a name="remembering-what-the-user-entered"></a>"Pamatuje", co uživatel zadal

Možná jste si všimli, že po zadání žánru a kliknutí na **Search žánru**jste viděli seznam pro tento žánr. Textové pole hledání je ale prázdné &mdash; jinými slovy, nepamatuje si, co jste zadali.

Je důležité pochopit, proč k tomuto chování dochází. Když odešlete stránku, prohlížeč odešle požadavek webovému serveru. Když ASP.NET Získá požadavek, vytvoří značku – novou instanci stránky, spustí kód v něm a pak znovu vykreslí stránku do prohlížeče. V důsledku toho stránka sice neví, že jste právě pracovali s předchozí verzí sebe sama. To znamená, že se v něm objevila žádost, která obsahuje nějaká data formuláře.

Pokaždé, když si vyžádáte stránku &mdash;, jestli poprvé nebo když ji odešlete &mdash; získáte novou stránku. Webový server nemá žádnou paměť vaší poslední žádosti. Nedělá ASP.NET ani prohlížeč. Jediným připojením mezi těmito samostatnými instancemi stránky jsou všechna data, která mezi nimi přenášíte. Pokud odešlete stránku, například nová instance stránky může získat data formuláře, která byla odeslána předchozí instancí. (Další způsob, jak předat data mezi stránkami, je použití souborů cookie.)

Formální způsob, jak tuto situaci popsat, je říci, že webové stránky jsou *bezstavové*. Webové servery a stránky a prvky na stránce neudržují žádné informace o předchozím stavu stránky. Web byl navržen tímto způsobem, protože udržováním stavu pro jednotlivé požadavky by bylo možné rychle vyčerpat prostředky webových serverů, které často zpracovávají tisíce, možná i stovky tisíců požadavků za sekundu.

Takže to je důvod, proč je textové pole prázdné. Po odeslání stránky ASP.NET vytvořila novou instanci stránky a běžela prostřednictvím kódu a kódu. V tomto kódu se neobjevila žádná hodnota, která by ASP.NETa vložení hodnoty do textového pole. Takže ASP.NET neudělal cokoli a textové pole bylo vykresleno bez hodnoty.

Tento problém se dá nejlépe snadno vyřešit. Žánr, který jste zadali do textového pole, *je* k dispozici v kódu &mdash; je `Request.QueryString["searchGenre"]`.

Aktualizujte značky pro textové pole tak, aby atribut `value` pře`searchTerm`hodnotu z, jako v tomto příkladu:

[!code-html[Main](form-basics/samples/sample9.html?highlight=1)]

Na této stránce můžete také nastavit atribut `value` na `searchTerm` proměnnou, protože tato proměnná obsahuje také Žánr, který jste zadali. Ale použití objektu `Request` k nastavení atributu `value`, jak je znázorněno zde, je standardní způsob, jak tuto úlohu provést. (Za předpokladu, že to budete chtít udělat &mdash; v některých situacích, možná budete chtít vykreslit stránku *bez* hodnot v polích. Vše závisí na tom, co se ve vaší aplikaci prochází.)

> [!NOTE]
> Nemůžete si pamatovat na hodnotu textového pole, které se používá pro hesla. Může se jednat o bezpečnostní otvor, který umožňuje lidem vyplnit pole hesla pomocí kódu.

Spusťte znovu stránku, zadejte Žánr a klikněte na **Hledat Žánr**. Tato doba nestačí jenom zobrazit výsledky hledání, ale textové pole pamatuje, co jste zadali za poslední čas:

![Stránka ukazující, že textové pole má "rememberd" předchozí položku](form-basics/_static/image5.png)

## <a name="searching-for-any-word-in-the-title"></a>Hledání libovolného slova v nadpisu

Teď můžete vyhledat jakýkoliv Žánr, ale možná budete chtít také vyhledat nadpis. Při hledání je obtížné získat nadpis přesně. místo toho můžete vyhledat slovo, které se zobrazí kdekoli v názvu. Chcete-li to provést v SQL, použijte operátor `LIKE` a syntax podobný následujícímu:

`SELECT * FROM Movies WHERE Title LIKE '%adventure%'`

Tento příkaz načte všechny filmy, jejichž názvy obsahují slovo "Adventure". Při použití operátoru `LIKE` zahrnete zástupný znak `%` jako součást hledaného termínu. Hledání `LIKE 'adventure%'` znamená "začíná slovem" Adventure ". (Technicky to znamená "řetězec" Adventure "následovaný cokoli.") Podobně hledaný termín `LIKE '%adventure'` znamená "cokoli následované řetězcem" Adventure ", což je další způsob, jak vyslovit" "s" Adventure "".

Hledaný termín `LIKE '%adventure%'` proto znamená "" Adventure "kdekoli v názvu." (Technicky, "cokoli v názvu, následované" Adventure "následovaný cokoli.")

Uvnitř elementu `<form>` přidejte následující kód vpravo pod uzavírací značku `</div>` pro hledání žánru (těsně před uzavíracím `</form>` elementem):

[!code-html[Main](form-basics/samples/sample10.html)]

Kód pro zpracování tohoto hledání je podobný kódu pro hledání žánru, s výjimkou, že je nutné sestavit `LIKE` vyhledávání. Uvnitř bloku kódu v horní části stránky přidejte tento blok `if` hned za `if` bloku pro hledání žánru:

[!code-csharp[Main](form-basics/samples/sample11.cs)]

Tento kód používá stejnou logiku, kterou jste viděli dříve, s tím rozdílem, že vyhledávání používá operátor `LIKE` a kód vloží "`%`" před a za hledaný termín.

Všimněte si, jak bylo snadné přidat další vyhledávání na stránku. Měli byste to udělat:

- Vytvořte `if` blok, který byl testován, aby bylo možné zjistit, zda příslušné vyhledávací pole mělo hodnotu.
- Nastavte proměnnou `selectCommand` na nový příkaz SQL.
- Nastavte proměnnou `searchTerm` na hodnotu, která má být předána dotazu.

Zde je kompletní blok kódu, který obsahuje novou logiku pro hledání v nadpisu:

[!code-cshtml[Main](form-basics/samples/sample12.cshtml)]

Tady je přehled toho, co tento kód dělá:

- Proměnné `searchTerm` a `selectCommand` jsou inicializovány v horní části. Chystáte se nastavit tyto proměnné na příslušný hledaný výraz (pokud existuje) a odpovídající příkaz SQL na základě toho, co uživatel na stránce provádí. Výchozím hledáním je jednoduchý případ získávání všech filmů z databáze.
- V testech pro `searchGenre` a `searchTitle`kód nastaví `searchTerm` na hodnotu, kterou chcete vyhledat. Tyto bloky kódu také nastavují `selectCommand` pro příslušné příkazy SQL pro toto hledání.
- Metoda `db.Query` je vyvolána pouze jednou, přičemž použití jakéhokoliv příkazu SQL je v `selectedCommand` a libovolná hodnota je v `searchTerm`. Pokud neexistuje hledaný termín (žádný Žánr a žádné slovo title), hodnota `searchTerm` je prázdný řetězec. Nicméně to nezáleží, protože v takovém případě dotaz nepožaduje parametr.

## <a name="testing-the-title-search-feature"></a>Testování funkce hledání názvu

Nyní můžete otestovat dokončenou stránku vyhledávání. Spusťte *video. cshtml*.

Zadejte Žánr a klikněte na **Hledat Žánr**. Mřížka zobrazuje filmy tohoto žánru, například před.

Zadejte název slovo a klikněte na **Hledat nadpis**. Mřížka zobrazuje filmy, které mají toto slovo v názvu.

![Seznam filmů po vyhledání ' The ' v nadpisu](form-basics/_static/image6.png)

Obě textová pole ponechte prázdné a klikněte na jedno tlačítko. V mřížce se zobrazí všechny filmy.

## <a name="combining-the-queries"></a>Kombinování dotazů

Můžete si všimnout, že hledání, která můžete provádět, jsou exkluzivní. Nemůžete současně prohledávat název a žánr, a to i v případě, že obě vyhledávací pole obsahují v nich hodnoty. Například nemůžete vyhledat všechny filmy akcí, jejichž název obsahuje text "Adventure". (Jak je stránka kódována, pokud zadáte hodnoty pro Žánr a název, bude hledání názvu přednost.) Chcete-li vytvořit vyhledávání, které kombinuje podmínky, je nutné vytvořit dotaz SQL, který má následující syntaxi:

`SELECT * FROM Movies WHERE Genre = @0 AND Title LIKE @1`

A musíte spustit dotaz pomocí příkazu podobného následujícímu (přibližně řečeno):

`var selectedData = db.Query(selectCommand, searchGenre, searchTitle);`

Vytvoření logiky, která povoluje mnoho permutací kritérií vyhledávání, může mít za to, jak můžete vidět. Proto tady zastavíme.

## <a name="coming-up-next"></a>Připravujeme další

V dalším kurzu vytvoříte stránku, která používá formulář, aby uživatelé mohli přidávat do databáze filmy.

## <a name="complete-listing-for-movie-page-updated-with-search"></a>Úplný výpis pro stránku videa (aktualizovaný pomocí hledání)

[!code-cshtml[Main](form-basics/samples/sample13.cshtml)]

## <a name="additional-resources"></a>Další prostředky

- [Seznámení s ASP.NET webovým programováním pomocí syntaxe Razor](https://go.microsoft.com/fwlink/?LinkID=202890)
- [Klauzule WHERE jazyka SQL](http://www.w3schools.com/sql/sql_where.asp) na webu w3schools
- Článek [definice metod](http://www.w3.org/Protocols/rfc2616/rfc2616-sec9.html) na webu W3C

> [!div class="step-by-step"]
> [Předchozí](displaying-data.md)
> [Další](entering-data.md)

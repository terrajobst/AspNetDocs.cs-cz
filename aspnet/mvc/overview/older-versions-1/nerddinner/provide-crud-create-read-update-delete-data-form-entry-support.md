---
uid: mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
title: Poskytnutí operace CRUD (vytvoření, čtení, aktualizace, odstranění) podpory zadávání dat na formuláři | Microsoft Docs
author: microsoft
description: Krok 5 ukazuje, jak dál využít naši třídu DinnersController, povolením podpory pro úpravy, vytváření a odstraňování večeři i s nimi.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: bbb976e5-6150-4283-a374-c22fbafe29f5
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/provide-crud-create-read-update-delete-data-form-entry-support
msc.type: authoredcontent
ms.openlocfilehash: b3123af9a1477bc496a0d229d628510fc202b6d2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580554"
---
# <a name="provide-crud-create-read-update-delete-data-form-entry-support"></a>Zajištění akcí CRUD (Create, Read, Update, Delete) podporujících zápis dat do formuláře

od [Microsoftu](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 5 bezplatného [kurzu aplikace "NerdDinner"](introducing-the-nerddinner-tutorial.md) , který vás provede procesem vytvoření malé, ale dokončené webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 5 ukazuje, jak dál využít naši třídu DinnersController, povolením podpory pro úpravy, vytváření a odstraňování večeři i s nimi.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme vám postupovat podle [Začínáme s kurzy pro](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [hudební úložiště](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) MVC 3 nebo MVC.

## <a name="nerddinner-step-5-create-update-delete-form-scenarios"></a>NerdDinner krok 5: vytvoření, aktualizace, odstranění scénářů formulářů

Představili jsme řadiče a zobrazení a pokryli jsme, jak je používat k implementaci možností výpisu a podrobností pro večeři na webu. Náš další krok bude dál přebírat naši třídu DinnersController a umožní vám podporu pro úpravy, vytváření a odstraňování večeři i s nimi.

### <a name="urls-handled-by-dinnerscontroller"></a>Adresy URL zpracovávané DinnersController

Dříve jsme přidali metody akcí pro DinnersController, které implementují podporu dvou adres URL: */Dinners* a */Dinners/Details/[ID]* .

| **Adresa URL** | **OPERACE** | **Účel** |
| --- | --- | --- |
| */Dinners/* | GET | Zobrazit seznam nadcházejících večeře v HTML |
| */Dinners/Details/[ID]* | GET | Zobrazí podrobnosti o konkrétní večeři. |

Nyní budeme přidávat metody akcí pro implementaci tří dalších adres URL: */Dinners/Edit/[ID]* , */Dinners/Create*a */Dinners/DELETE/[ID]* . Tyto adresy URL umožní podporu úprav stávajících večeře, vytváření nových večeři a odstraňování večeři.

S těmito novými adresami URL budeme podporovat interakce operací HTTP GET a HTTP POST. Požadavky HTTP GET na tyto adresy URL zobrazí úvodní zobrazení HTML dat (formulář naplněný daty o večeři v případě příkazu "Upravit", prázdný tvar v případě příkazu "vytvořit" a obrazovka pro potvrzení odstranění "v případě" odstranění "). Požadavky HTTP POST na tyto adresy URL budou ukládat, aktualizovat nebo odstraňovat data o večeři v našich DinnerRepository (a odtud i do databáze).

| **Adresa URL** | **OPERACE** | **Účel** |
| --- | --- | --- |
| */Dinners/Edit/[ID]* | GET | Zobrazit Upravitelný formulář HTML vyplněný daty o večeři. |
| POST | Uloží změny formuláře pro konkrétní večeři do databáze. |
| */Dinners/Create* | GET | Zobrazí prázdný formulář HTML, který umožňuje uživatelům definovat nové hostiny. |
| POST | Vytvořte novou večeři a uložte ji do databáze. |
| */Dinners/Delete/[ID]* | GET | Obrazovka pro potvrzení odstranění zobrazení |
| POST | Odstraní zadanou večeři z databáze. |

### <a name="edit-support"></a>Upravit podporu

Pojďme začít implementací scénáře "Edit".

#### <a name="the-http-get-edit-action-method"></a>Metoda HTTP-GET Edit Action

Začneme implementací chování HTTP "GET" naší metody Upravit akci. Tato metoda bude vyvolána, když je vyžádána adresa URL */Dinners/Edit/[ID]* . Naše implementace bude vypadat takto:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample1.cs)]

Výše uvedený kód používá DinnerRepository k načtení objektu večeře. Následně vykreslí šablonu zobrazení pomocí objektu večeře. Vzhledem k tomu, že jsme explicitně nepředali název šablony do pomocné metody *zobrazení ()* , použije se výchozí cesta založená na konvenci k vyřešení šablony zobrazení:/views/Dinners/Edit.aspx.

Teď vytvoříme tuto šablonu zobrazení. To provedete tak, že kliknete pravým tlačítkem myši v rámci metody Edit a vyberete příkaz "přidat zobrazení" v místní nabídce:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image1.png)

V dialogovém okně Přidat zobrazení oznamujeme, že jako svůj model předáváme objekt večeře do naší šablony zobrazení, a zvolíte možnost automatického generování uživatelského rozhraní šablony pro úpravy:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image2.png)

Když klikneme na tlačítko Přidat, Visual Studio přidá nový soubor šablony zobrazení Edit. aspx pro nás v adresáři "\Views\Dinners". Otevře se také nová šablona zobrazení "Edit. aspx" v editoru kódu – naplněná počáteční implementací uživatelského rozhraní, jako je následující:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image3.png)

Pojďme udělat několik změn ve výchozím vygenerovaném generátoru "Edit" a aktualizovat šablonu zobrazení pro úpravy tak, aby měla následující obsah (což odebere několik vlastností, které nechcete zveřejnit):

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample2.aspx)]

Když aplikaci spustíme a požádáme o adresu URL *"/Dinners/Edit/1"* , zobrazí se následující stránka:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image4.png)

Kód HTML generovaný naším zobrazením vypadá níže. Je to standardní HTML – pomocí &lt;formuláře&gt; elementu, který provede odeslání HTTP POST na adresu URL */Dinners/Edit/1* při vložení tlačítka Uložit &lt;input type = "Submit"/&gt;. Jako výstup pro každou upravitelnou vlastnost &lt;vstupní typ HTML = "text"/&gt; element:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image5.png)

#### <a name="htmlbeginform-and-htmltextbox-html-helper-methods"></a>Pomocné metody HTML. BeginForm () a HTML. TextBox ()

Naše šablona zobrazení "Edit. aspx" používá několik metod "Pomocník HTML": HTML. ovládací souhrnu ověření (), HTML. BeginForm (), HTML. TextBox () a HTML. ValidationMessage (). Kromě generování značek HTML pro nás poskytují tyto pomocné metody integrovanou manipulaci s chybami a podporu ověřování.

##### <a name="htmlbeginform-helper-method"></a>Pomocná metoda HTML. BeginForm ()

Pomocná metoda HTML. BeginForm () je výstupem&gt; elementu HTML &lt;formuláře v našem kódu. V naší šabloně zobrazení Edit. aspx si všimnete, že C# při použití této metody používáme příkaz using. Otevřená složená závorka indikuje začátek &lt;formuláře&gt; obsahu a pravá složená závorka je to, co označuje konec &lt;formuláře&gt; elementu:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample3.cs)]

Případně, pokud najdete příkaz "using" přístup nepřirozeným způsobem pro nějaký scénář, můžete použít kombinaci HTML. BeginForm () a HTML. EndForm () (která má stejnou věc):

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample4.aspx)]

Volání souboru HTML. BeginForm () bez parametrů způsobí, že by výstupní prvek formuláře, který provede HTTP-POST, na adresu URL aktuálního požadavku. Proto naše zobrazení pro úpravy generuje *akci&lt;formuláře = "/Dinners/Edit/1" Method = "post"&gt;* elementu. Pokud jsme chtěli poslat na jinou adresu URL, můžeme taky předávat explicitní parametry do HTML. BeginForm ().

##### <a name="htmltextbox-helper-method"></a>Pomocná metoda HTML. TextBox ()

Náš pohled Edit. aspx používá pomocnou metodu HTML. TextBox () pro výstup &lt;vstupní typ = "text"/&gt; prvky:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample5.aspx)]

Výše uvedená metoda HTML. TextBox () přebírá jeden parametr, který se používá k určení atributů ID i názvu &lt;vstupní typ = "text"/&gt; element na výstup a také vlastnost modelu, ze které se má vyplnit hodnota TextBox. Například objekt večeře, který jsme předali do zobrazení pro úpravy, měl hodnotu "název" hodnoty ".NET futures", a proto náš kód HTML. TextBox ("title") volá výstup volání metody: *&lt;Input ID = "title" Name = "title" Type = "text" value = ". NET futures"/&gt;* .

Alternativně můžeme použít první parametr HTML. TextBox () k určení ID/názvu elementu a pak explicitně předat hodnotu, která se má použít jako druhý parametr:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample6.aspx)]

Často chceme pro hodnotu, která je výstupem, provádět vlastní formátování. Statická metoda String. Format () integrovaná do rozhraní .NET je užitečná pro tyto scénáře. Naše šablona zobrazení Edit. aspx používá tuto hodnotu k formátování hodnoty EventDate (která je typu DateTime) tak, aby pro dobu nezobrazovala sekundy:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample7.aspx)]

Třetí parametr do HTML. TextBox () lze volitelně použít pro výstup dalších atributů HTML. Následující fragment kódu ukazuje, jak vykreslit dodatečnou velikost = "30" a atribut class = "mycssclass" na &lt;vstupní typ = "text"/&gt; element. Všimněte si, jak uvozovací znaky názvu atributu Class pomocí "@" character because "třídy" je rezervované klíčové slovo v C#:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample8.aspx)]

#### <a name="implementing-the-http-post-edit-action-method"></a>Implementace metody akce pro úpravu HTTP-POST

Teď je k dispozici verze protokolu HTTP-GET pro naši metodu Edit Action implementovaná. Když uživatel požádá o adresu URL */Dinners/Edit/1* , obdrží stránku HTML, například následující:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image6.png)

Stisknutím tlačítka Save (Uložit) dojde k odeslání příspěvku formuláře na adresu URL */Dinners/Edit/1* a odeslání souboru HTML &lt;vstupní&gt; hodnoty formuláře pomocí příkazu HTTP POST. Pojďme teď implementovat chování HTTP POST metody pro úpravy, která bude zpracovávat večeři.

Začneme přidáním přetížené metody Action "Edit" do našich DinnersController s atributem "AcceptVerbs", který indikuje, že zpracovává scénáře HTTP POST:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample9.cs)]

Pokud je atribut [AcceptVerbs] aplikován na metody reloadd Action, ASP.NET MVC automaticky zpracovává odesílání požadavků na příslušnou metodu akce v závislosti na příchozím příkazu HTTP. Požadavky HTTP POST na adresy URL */Dinners/Edit/[ID]* přejdou na výše uvedenou metodu úprav, zatímco všechny ostatní požadavky HTTP na adresy URL */Dinners/Edit/[ID]* budou přejít na první metodu úprav, kterou jsme implementovali (která neobsahovala atribut `[AcceptVerbs]`).

| **Vedlejší téma: Proč odlišit přes příkazy HTTP?** |
| --- |
| Můžete se zeptat – proč používáme jednu adresu URL a rozlišujeme její chování prostřednictvím příkazu HTTP? Proč ne pouze dvě samostatné adresy URL ke zpracování načítání a ukládání změn úprav? Například:/Dinners/Edit/[ID] pro zobrazení počátečního formuláře a/Dinners/Save/[ID] pro zpracování příspěvku formuláře pro uložení? Nevýhodou s publikováním dvou oddělených adres URL je, že v případech, kdy pošleme na/Dinners/Save/2, a pak je potřeba znovu zobrazit formulář HTML z důvodu chyby vstupu, koncový uživatel bude mít v adresním řádku prohlížeče adresu URL/Dinners/Save/2 (protože to bylo adresa URL, na kterou je formulář publikovaný). Pokud koncový uživatel zachová tuto znovu stránku do seznamu oblíbených položek prohlížeče nebo ji zkopíruje nebo vloží do přítele, ukončí tím ukládání adresy URL, která v budoucnu nebude fungovat (protože tato adresa URL závisí na hodnotách post). Vyvoláním jedné adresy URL (například:/Dinners/Edit/[ID]) a rozlišením jejich zpracování pomocí příkazu HTTP je bezpečné, aby koncoví uživatelé mohli zaměnit stránku úprav a/nebo adresu URL poslat ostatním. |

#### <a name="retrieving-form-post-values"></a>Načítání hodnot post formuláře

Existuje mnoho způsobů, jak získat přístup k parametrům publikovaných formulářů v rámci metody "Upravit" HTTP POST. Jedním jednoduchým přístupem je pouze použití vlastnosti Request v základní třídě kontroleru pro přístup ke kolekci formulářů a k načtení vystavených hodnot přímo:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample10.cs)]

Výše uvedený přístup je trochu podrobný, ale zejména v případě, že přidáváme logiku zpracování chyb.

Lepším přístupem k tomuto scénáři je použití integrované pomocné metody *UpdateModel ()* na základní třídě kontroleru. Podporuje aktualizaci vlastností objektu, který předáte pomocí parametrů příchozího formuláře. Používá reflexi k určení názvů vlastností objektu a poté automaticky převede a přiřadí hodnoty na základě vstupních hodnot odeslaných klientem.

Pomocí metody UpdateModel () jsme mohli zjednodušit naši akci HTTP-POST pomocí tohoto kódu:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample11.cs)]

Teď můžeme navštívit adresu URL */Dinners/Edit/1* a změnit název naší hostiny:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image7.png)

Po kliknutí na tlačítko Save (Uložit) provedeme odeslání příspěvku na naši akci úprav a aktualizované hodnoty budou v databázi trvalé. Budeme přesměrováni na adresu URL podrobností pro večeři (zobrazí se nově uložené hodnoty):

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image8.png)

#### <a name="handling-edit-errors"></a>Zpracování chyb úprav

Naše aktuální implementace HTTP-POST funguje správně – s výjimkou případů, kdy dojde k chybám.

Když uživatel vytvoří chybu v úpravách formuláře, musíme se ujistit, že je formulář znovu zobrazen pomocí informativní chybové zprávy, která je provede k jejich opravě. To zahrnuje případy, kdy koncový uživatel zaúčtuje nesprávný vstup (například: poškozený řetězec data) a také případy, kdy je vstupní formát platný, ale dojde k porušení obchodního pravidla. Pokud dojde k chybám, je třeba zachovat vstupní data, která uživatel původně zadal, aby nemuseli změny znovu plnit ručně. Tento postup by se měl opakovat tolikrát, kolikrát je potřeba, dokud se formulář úspěšně nedokončí.

ASP.NET MVC obsahuje některé skvělé integrované funkce, které umožňují zpracování chyb a rychlé zobrazení formulářů. Pokud chcete zobrazit tyto funkce v akci, aktualizujte naši metodu Edit Action pomocí následujícího kódu:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample12.cs)]

Výše uvedený kód je podobný naší předchozí implementaci – s tím rozdílem, že nyní zabalíme blok zpracování chyb typu try/catch kolem naší práce. Pokud dojde k výjimce buď při volání metody UpdateModel (), nebo při pokusu o uložení DinnerRepository (což vyvolá výjimku, pokud se objekt večeře, který se snažíte uložit, neplatný z důvodu porušení pravidla v rámci našeho modelu), náš blok zpracování chyb catch bude spustit. V rámci této smyčky se přeskočí všechna porušení pravidel, která existují v objektu večeře, a přidejte je do objektu ModelState (který budeme projednávat za chvíli). Znovu zobrazíme zobrazení.

Tuto práci si můžete prohlédnout tak, že aplikaci znovu spustíte, upravíte večeři a změníte ji tak, aby měla prázdný název, EventDate "" FALEŠNou "a používala telefonní číslo Spojené království s hodnotou země USA. Po stisknutí tlačítka Uložit v metodě pro úpravu HTTP POST nebude možné uložit večeři (protože jsou k dispozici chyby) a bude formulář znovu zobrazen:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image9.png)

Naše aplikace má dáté chybové prostředí. Textové prvky s neplatným vstupem jsou zvýrazněny červeně a koncovým uživatelům se jim zobrazí chybové zprávy o ověřování. Ve formuláři se taky zachovává vstupní data, která uživatel původně zadal – aby se nemuseli nic dělat.

Jak se můžete zeptat, došlo k tomu? Jak se v textových polích title, EventDate a ContactPhone zvýrazňují červeně a víte, že původně zadané hodnoty uživatele? A jak se v seznamu v horní části zobrazily chybové zprávy? Dobrá zpráva je, že nedošlo k tomu, že je to u sebe Magic, protože jsme použili některé z vestavěných funkcí ASP.NET MVC, které usnadňují scénáře ověřování vstupu a zpracování chyb.

#### <a name="understanding-modelstate-and-the-validation-html-helper-methods"></a>Principy ModelState a pomocných metod ověřování HTML

Třídy kontroleru mají kolekci vlastností "ModelState", která poskytuje způsob, jak určit, že chyby existují s objektem modelu předaným do zobrazení. Položky chyb v rámci kolekce ModelState identifikují název vlastnosti modelu s problémem (například: "title", "EventDate" nebo "ContactPhone") a umožní zadat uživatelsky přívětivou chybovou zprávu (například: "Nadpis je vyžadován").

Pomocná metoda *UpdateModel ()* automaticky naplní kolekci ModelState, pokud při pokusu o přiřazení hodnot formuláře k vlastnostem objektu modelu dojde k chybám. Například vlastnost EventDate objektu večeře je typu DateTime. Pokud se metodě UpdateModel () nepovedlo přiřadit hodnotu řetězce "nefalešně" ve výše uvedeném scénáři, metoda UpdateModel () přidala položku do kolekce ModelState, která indikuje, že u této vlastnosti došlo k chybě přiřazení.

Vývojáři můžou také napsat kód pro explicitní přidání položek chyb do kolekce ModelState, jako jsme to dělali níže v rámci našeho bloku zpracování chyb "catch", který naplňuje kolekci ModelState položkami na základě porušení aktivních pravidel v Objekt večeře:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample13.cs)]

#### <a name="html-helper-integration-with-modelstate"></a>Integrace pomocníka HTML s ModelState

Pomocné metody HTML – jako HTML. TextBox () – při vykreslování výstupu kontrolovat kolekci ModelState. Pokud pro položku existuje chyba, vykreslí uživatelem zadanou hodnotu a třídu chyb CSS.

Například v našem zobrazení "Edit" používáme pomocnou metodu HTML. TextBox () pro vykreslení EventDate našeho objektu večeře:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample14.aspx)]

Když bylo zobrazení vykresleno v případě chyby, metoda HTML. TextBox () kontroluje kolekci ModelState, aby zjistila, zda došlo k chybám přidružených k vlastnosti "EventDate" objektu večeře. Když bylo zjištěno, že došlo k chybě při vykreslování odeslaného vstupu uživatele ("FALEŠNá") jako hodnoty a přidána třída chyb CSS do &lt;input type = "TextBox"/&gt; vygenerovaného kódu:

[!code-html[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample15.html)]

Vzhled třídy Error šablon stylů CSS můžete přizpůsobit tak, aby vypadala tak, jak chcete. Výchozí třída chyb CSS – "vstup-ověření-Chyba" – je definována v šabloně stylů *\content\site.CSS* a vypadá takto:

[!code-css[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample16.css)]

Toto pravidlo CSS má za následek zvýraznění neplatných vstupních elementů, jako například níže:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image10.png)

##### <a name="htmlvalidationmessage-helper-method"></a>Pomocná metoda HTML. ValidationMessage ()

Pomocná metoda HTML. ValidationMessage () se dá použít k vytvoření výstupu chybové zprávy ModelState přidružené ke konkrétní vlastnosti modelu:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample17.aspx)]

Výše uvedené výstupy kódu: *&lt;span class = "Field-Validation-Error"&gt; hodnota ' falešná ' je neplatná&lt;/span&gt;*

Pomocná metoda HTML. ValidationMessage () také podporuje druhý parametr, který vývojářům umožňuje potlačit textovou zprávu o chybě, která se zobrazí:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample18.aspx)]

Výše uvedené výstupy kódu: *&lt;span class = "Field-Validation-Error"&gt;\*&lt;/span&gt;* namísto výchozího textu chyby, pokud je pro vlastnost EventDate k dispozici chyba.

##### <a name="htmlvalidationsummary-helper-method"></a>Html.ValidationSummary() Helper Method

Pomocná metoda HTML. ovládací souhrnu ověření () se dá použít k vykreslení souhrnné chybové zprávy, která doprovází &lt;ul&gt;&lt;li/&gt;&lt;/ul&gt; seznam všech podrobných chybových zpráv v kolekci ModelState:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image11.png)

Pomocná metoda HTML. ovládací souhrnu ověření () přebírá volitelný řetězcový parametr – což definuje souhrnnou chybovou zprávu, která se zobrazí nad seznamem podrobných chyb:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample19.aspx)]

Můžete volitelně použít CSS k přepsání toho, co vypadá seznam chyb.

#### <a name="using-a-addruleviolations-helper-method"></a>Použití pomocné metody AddRuleViolations

Naše úvodní implementace HTTP-POST použila příkaz foreach v rámci svého bloku catch k cyklickému převzetí služeb při narušení pravidla u objektu večeře a jejich přidání do kolekce ModelState kontroleru:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample20.cs)]

Tento kód můžeme trochu čističovat přidáním třídy "ControllerHelpers" do projektu NerdDinner a implementovat metodu rozšíření "AddRuleViolations", která do ní přidá pomocnou metodu pro třídu ModelStateDictionary ASP.NET MVC. Tato metoda rozšíření může zapouzdřit logiku potřebnou k naplnění ModelStateDictionary seznamem chyb RuleViolation:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample21.cs)]

Pak můžeme aktualizovat metodu akce HTTP-POST pro úpravu, aby tuto metodu rozšíření používal k naplnění kolekce ModelState s porušením pravidla večeře.

#### <a name="complete-edit-action-method-implementations"></a>Dokončit implementace metody akce úprav

Následující kód implementuje veškerou logiku řadiče potřebnou pro náš scénář úprav:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample22.cs)]

V případě naší implementace úprav je to, že ani naše třída Controller ani naše šablona zobrazení neznají žádné informace o konkrétním ověřování nebo obchodních pravidlech vynucujech modelem večeře. Do našeho modelu můžeme v budoucnu přidat další pravidla a nemusíte dělat žádné změny kódu pro náš kontroler nebo zobrazení, aby je bylo možné podporovat. Díky tomu je tato flexibilita flexibilní, aby bylo možné v budoucnu snadno vyvíjet požadavky na aplikace s minimálními změnami kódu.

### <a name="create-support"></a>Vytvořit podporu

Dokončili jsme implementaci "Edit" chování naší třídy DinnersController. Pojďme teď přejít k implementaci podpory "vytvoření", která uživatelům umožní přidávat nové hostiny.

#### <a name="the-http-get-create-action-method"></a>Metoda HTTP-GET Create Action

Zahájíme implementaci chování HTTP "GET" naší metody vytvoření akce. Tato metoda bude volána, když někdo navštíví adresu URL */Dinners/Create* . Naše implementace vypadá takto:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample23.cs)]

Výše uvedený kód vytvoří nový objekt večeře a přiřadí jeho vlastnost EventDate v budoucnosti do jednoho týdne. Následně vykreslí zobrazení, které je založeno na novém objektu večeře. Vzhledem k tomu, že jsme explicitně nepředali název do pomocné metody *zobrazení ()* , použije se výchozí cesta založená na konvenci k vyřešení šablony zobrazení:/views/Dinners/Create.aspx.

Teď vytvoříme tuto šablonu zobrazení. To můžeme provést tak, že kliknete pravým tlačítkem myši v rámci metody Create Action a vyberete příkaz "přidat zobrazení" v kontextové nabídce. V dialogovém okně Přidat zobrazení určíme, že do šablony zobrazení předáváme objekt večeře a v případě, že se rozhodnete k automatickému generování uživatelského rozhraní vytvořit šablonu:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image12.png)

Po kliknutí na tlačítko Přidat bude Visual Studio ukládat nové zobrazení "vytvořit. aspx" na základě uživatelského rozhraní do adresáře "\Views\Dinners" a otevře ho v integrovaném vývojovém prostředí (IDE):

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image13.png)

Pojďme udělat několik změn ve výchozím souboru generátoru "Create", který se vygeneroval pro nás, a upravit ho tak, aby vypadal níže:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample24.aspx)]

A teď když spouštíme naši aplikaci a přistupuje k adrese URL *"/Dinners/Create"* v prohlížeči, vykreslí se uživatelské rozhraní podobně jako v naší implementaci akce vytvoření:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image14.png)

#### <a name="implementing-the-http-post-create-action-method"></a>Implementace metody akce vytvoření HTTP-POST

Máme implementovaná verze HTTP-GET metody Create Action. Když uživatel klikne na tlačítko Save (Uložit), provede formulářový příspěvek na adresu URL */Dinners/Create* a odešle &lt;vstupní&gt; hodnoty formuláře pomocí příkazu HTTP POST.

Pojďme teď implementovat chování HTTP POST metody Create Action. Začneme přidáním přetížené metody "vytvořit" do našich DinnersController s atributem "AcceptVerbs", který indikuje, že zpracovává scénáře HTTP POST:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample25.cs)]

Existuje mnoho způsobů, jak získat přístup k parametrům odeslaného formuláře v rámci metody "Create" odeslané pomocí protokolu HTTP-POST.

Jedním z možností je vytvořit nový objekt večeře a potom použít pomocnou metodu *UpdateModel ()* , která se naplní hodnotami publikovaných formulářů. Můžeme ho následně přidat do našich DinnerRepositoryů, uchovávat ho v databázi a přesměrovat uživatele na naši akci s podrobnostmi, jak zobrazit nově vytvořenou večeři pomocí následujícího kódu:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample26.cs)]

Alternativně můžeme použít přístup, kde máme metodu vytvoření () akce převzít objekt večeře jako parametr metody. ASP.NET MVC pak automaticky vytvoří instanci nového objektu večeře pro nás, naplní své vlastnosti pomocí vstupů formuláře a předává je naší metodě akcí:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample27.cs)]

Naše metoda Action výše ověří, že se objekt večeře úspěšně naplnil hodnotami post formuláře, a to tak, že zkontroluje vlastnost ModelState. IsValid. Pokud dojde k problémům s převodem vstupu (například s řetězcem "FALEŠNÉho" pro vlastnost EventDate) a dojde k nějakému problému, vrátí naše metoda akce formulář.

Pokud jsou vstupní hodnoty platné, pak se metoda akce pokusí přidat a uložit novou večeři do DinnerRepository. Zalomí tuto práci do bloku try/catch a znovu zobrazí formulář, pokud dojde k porušení obchodních pravidel (což by způsobilo, že metoda dinnerRepository. Save () vyvolá výjimku).

Pokud se chcete podívat na chování zpracování chyb v akci, můžeme požádat o adresu URL */Dinners/Create* a vyplnit podrobnosti o nové večeři. Nesprávné zadání nebo hodnoty způsobí, že se ve formuláři pro vytvoření znovu zobrazí chyby zvýrazněné následujícím způsobem:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image15.png)

Všimněte si, jak náš formulář pro tvorbu dodržuje přesně stejná pravidla ověřování a obchodních pravidel jako formulář pro úpravy. Důvodem je to, že naše ověřování a obchodní pravidla byly definovány v modelu a nebyly vloženy do uživatelského rozhraní nebo kontroleru aplikace. To znamená, že můžeme později změnit nebo vyvíjet naše ověřovací nebo obchodní pravidla na jednom místě a použít je v naší aplikaci. Nebudeme muset měnit žádný kód v rámci metod úpravy nebo vytváření akcí, aby automaticky dodržovala nová pravidla nebo změny stávajících pravidel.

Když opravíte vstupní hodnoty a znovu kliknete na tlačítko Uložit, naše přidání do DinnerRepository se podaří a do databáze se přidá nový večeři. Budeme přesměrováni na adresu URL */Dinners/Details/[ID]* , kde budeme prezentovat podrobnosti o nově vytvořené večeři:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image16.png)

### <a name="delete-support"></a>Odstranit podporu

Nyní přidáme podporu "odstranit" na naši DinnersController.

#### <a name="the-http-get-delete-action-method"></a>Metoda akce HTTP-GET DELETE

Začneme implementací chování HTTP GET metody akce Odstranit. Tato metoda se volá, když někdo navštíví adresu URL */Dinners/DELETE/[ID]* . Níže je tato implementace:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample28.cs)]

Metoda akce se pokusí načíst večeři pro odstranění. Pokud večeře existuje, vykreslí zobrazení na základě objektu večeře. Pokud objekt neexistuje (nebo už je odstraněný), vrátí zobrazení, které vykreslí šablonu zobrazení "NotFound", kterou jsme vytvořili dříve pro naši metodu akce "Details".

Šablonu zobrazení "odstranit" můžeme vytvořit tak, že kliknete pravým tlačítkem myši na metodu DELETE Action a vyberete příkaz "přidat zobrazení". V dialogovém okně Přidat zobrazení určíme, že jako svůj model předáte do naší šablony zobrazení objekt večeře a zvolíte vytvoření prázdné šablony:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image17.png)

Po kliknutí na tlačítko Přidat bude Visual Studio do našeho adresáře "\Views\Dinners" Přidat nový soubor šablony zobrazení "Delete. aspx" pro nás. Do šablony přidáme kód HTML a Naimplementujte obrazovku pro potvrzení odstranění, jak je znázorněno níže:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample29.aspx)]

Výše uvedený kód zobrazuje název večeře, který se má odstranit, a vytvoří výstup&gt; elementu &lt;formuláře, který provede příspěvek na adresu URL/Dinners/Delete/[ID], pokud koncový uživatel klikne na tlačítko Odstranit v rámci.

Po spuštění naší aplikace a přístup k adrese URL *"/Dinners/DELETE/[ID]"* pro platný objekt večeře VYKRESLÍ uživatelské rozhraní následujícím způsobem:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image18.png)

| **Vedlejší téma: Proč provádím příspěvek?** |
| --- |
| Můžete se zeptat – proč procházíme úsilím o vytvoření formuláře &lt;&gt; v rámci naší obrazovky pro odstranění potvrzení? Proč nestačí použít standardní hypertextový odkaz k propojení s metodou akce, která provede skutečnou operaci odstranění? Důvodem je, že chceme být opatrní před ochranou před webovými prohledávacími moduly a vyhledávacími moduly, které zjišťují naše adresy URL a nechtěně způsobují odstranění dat, když následují odkazy. Adresy URL založené na protokolu HTTP-GET se považují za "bezpečné", aby je bylo možné používat nebo procházet, a neměly by následovat za HTTP-POST. Dobrým pravidlem je, abyste měli jistotu, že se v rámci požadavků HTTP-POST vždycky umísťují ničivé operace nebo změny dat. |

#### <a name="implementing-the-http-post-delete-action-method"></a>Implementace metody akce odstranění HTTP-POST

Teď máme naimplementovaná verze HTTP-GET metody akce odstranění, která zobrazuje obrazovku pro potvrzení odstranění. Když koncový uživatel klikne na tlačítko Odstranit, provede příspěvek formuláře na adresu URL */Dinners/Dinner/[ID]* .

Pojďme teď implementovat chování metody "POST" metody akce DELETE pomocí kódu níže:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample30.cs)]

Verze metody odstranění HTTP-POST se pokusí načíst objekt večeře, který se má odstranit. Pokud ho nemůžete najít (protože už je odstraněný), vykreslí naši šablonu "NotFound". Pokud najde večeři, odstraní ho z DinnerRepository. Potom vykreslí šablonu "Deleted".

Pokud chcete implementovat šablonu "Deleted", klikněte na ni pravým tlačítkem a vyberte kontextovou nabídku přidat zobrazení. Budeme pojmenovat náš pohled "Deleted" a nechat ho prázdnou šablonu (a nemusíte mít objekt modelu silného typu). Pak do něj přidáte nějaký obsah HTML:

[!code-aspx[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample31.aspx)]

A teď když spouštíme naši aplikaci a přistupuje k adrese URL *"/Dinners/DELETE/[ID]"* pro platný objekt večeře, vykreslí se obrazovka s potvrzením o odstranění na večeři, jak je znázorněno níže:

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image19.png)

Když klikneme na tlačítko Odstranit, provede se odeslání HTTP-POST na adresu URL */Dinners/DELETE/[ID]* , která odstraní večeři z naší databáze a zobrazí naši šablonu zobrazení "smazáno":

![](provide-crud-create-read-update-delete-data-form-entry-support/_static/image20.png)

### <a name="model-binding-security"></a>Zabezpečení vazby modelu

Provedli jsme dva různé způsoby použití vestavěných funkcí vázání modelů ASP.NET MVC. První pomocí metody UpdateModel () pro aktualizaci vlastností existujícího objektu modelu a druhého pomocí podpory ASP.NET MVC pro předávání objektů modelu do jako parametrů metody Action. Oba tyto postupy jsou velmi výkonné a velmi užitečné.

Tato mocnina také přináší zodpovědnost za IT oddělení. Při přijímání jakéhokoli vstupu uživatele je důležité vždy paranoidní o zabezpečení, a to platí také při vytváření vazby objektů k vytvoření vstupu. Měli byste pečlivě zakódovat všechny uživatelem zadané hodnoty, aby se zabránilo útokům prostřednictvím injektáže HTML a JavaScriptu, a buďte opatrní při útocích prostřednictvím injektáže SQL. (Poznámka: používáme LINQ to SQL pro naši aplikaci, která automaticky kóduje parametry, které je zabrání. typy útoků). Nikdy byste neměli spoléhat jenom na ověřování na straně klienta a vždycky používat ověřování na straně serveru pro ochranu proti hackerům, kteří se snaží poslat falešně falešně neoprávněné hodnoty.

Jedna další položka zabezpečení pro zajištění, že budete uvažovat o použití funkcí vazby ASP.NET MVC, je obor objektů, které vytváříte. Konkrétně se ujistěte, že rozumíte vlivům na zabezpečení vlastností, které chcete svázat, a ujistěte se, že tyto vlastnosti povolíte, aby je bylo možné aktualizovat koncovým uživatelem.

Ve výchozím nastavení se metoda UpdateModel () pokusí aktualizovat všechny vlastnosti objektu modelu, které odpovídají hodnotám příchozích parametrů formuláře. Podobně objekty, které jsou předány jako parametry metody akce také ve výchozím nastavení, mohou mít všechny vlastnosti nastavené prostřednictvím parametrů formuláře.

#### <a name="locking-down-binding-on-a-per-usage-basis"></a>Uzamčení vazby u jednotlivých použití

Zásadu vazby můžete u jednotlivých použití uzamknout tím, že poskytnete explicitní "seznam zahrnutí" vlastností, které se dají aktualizovat. To se dá udělat tak, že předáte další parametr řetězcového pole metodě UpdateModel (), jak je znázorněno níže:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample32.cs)]

Objekty předané jako parametry metody Action podporují také atribut [BIND], který umožňuje zadat seznam zahrnutí povolených vlastností následujícím způsobem:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample33.cs)]

#### <a name="locking-down-binding-on-a-type-basis"></a>Uzamčení vazby na základě typu

Pravidla vazby můžete také Uzamknout pro jednotlivé typy. To umožňuje zadat pravidla vazby jednou a pak je použít ve všech scénářích (včetně scénářů parametrů UpdateModel a Action) napříč všemi řadiči a metodami akcí.

Můžete přizpůsobit pravidla vazby podle typu přidáním atributu [BIND] na typ nebo jeho registrací do souboru Global. asax aplikace (hodí se pro scénáře, které nevlastníte typ). Pak můžete pomocí vlastností include a Exclude atributu BIND řídit, které vlastnosti jsou pro konkrétní třídu nebo rozhraní vázané.

Tuto techniku použijeme pro třídu večeře v naší aplikaci NerdDinner a přidáte do ní atribut [BIND], který omezí seznam vlastností s možností vazby na následující:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample34.cs)]

Všimněte si, že nepovolujeme, aby byla kolekce RSVP zpracovávána prostřednictvím vazby, ani aby bylo možné nastavit vlastnosti DinnerID nebo HostedBy prostřednictvím vazby. Z bezpečnostních důvodů budeme místo toho manipulovat jenom s těmito konkrétními vlastnostmi pomocí explicitního kódu v rámci našich metod akcí.

### <a name="crud-wrap-up"></a>Zalamování CRUD

ASP.NET MVC zahrnuje řadu integrovaných funkcí, které vám pomůžou s implementací scénářů pro odesílání formulářů. Používali jsme celou řadu těchto funkcí, které vám poskytnou podporu uživatelského rozhraní CRUD nad naše DinnerRepository.

K implementaci naší aplikace používáme přístup zaměřený na model. To znamená, že všechny naše ověřování a logika obchodních pravidel jsou definovány v rámci naší vrstvy modelu – a ne v rámci našich řadičů nebo zobrazení. Ani naše třída Controller ani naše šablony zobrazení neznají žádné informace o konkrétních obchodních pravidlech, která jsou vynucuje naší třídou modelu večeře.

Tím se zajistí, že naše architektura aplikace bude čistá a bude snazší ji otestovat. Do naší vrstvy modelu můžeme v budoucnu přidat další obchodní pravidla a *není nutné provádět změny kódu* pro náš kontroler nebo zobrazení, aby je bylo možné podporovat. Díky tomu budeme mít velkou flexibilitu pro vývoj a změnu naší aplikace v budoucnu.

Naše DinnersController teď umožňuje vytvářet, upravovat a odstraňovat večeře. Úplný kód pro třídu najdete níže:

[!code-csharp[Main](provide-crud-create-read-update-delete-data-form-entry-support/samples/sample35.cs)]

### <a name="next-step"></a>Další krok

Nyní máme základní třídu CRUD (vytváření, čtení, aktualizace a odstranění), která podporuje implementaci v rámci naší třídy DinnersController.

Teď se podíváme na to, jak můžeme použít třídy ViewData a ViewModel k povolení ještě bohatšího uživatelského rozhraní v našich formulářích.

> [!div class="step-by-step"]
> [Předchozí](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
> [Další](use-viewdata-and-implement-viewmodel-classes.md)

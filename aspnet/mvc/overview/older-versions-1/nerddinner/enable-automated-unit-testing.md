---
uid: mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
title: Povolit automatizované testování částí | Microsoft Docs
author: microsoft
description: Krok 12 ukazuje, jak vyvíjet sadu automatizovaných testů jednotek, které ověřují naše funkce NerdDinner a které nám poskytnou jistotu udělat změny...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: a19ff2ce-3f7e-4358-9a51-a1403da9c63e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/enable-automated-unit-testing
msc.type: authoredcontent
ms.openlocfilehash: 09a7aa186605a6cce48ee94028425ded957c00d3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541676"
---
# <a name="enable-automated-unit-testing"></a>Povolení automatického testování jednotek

od [Microsoftu](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 12 bezplatného [kurzu aplikace "NerdDinner"](introducing-the-nerddinner-tutorial.md) , který vás provede procesem vytvoření malé, ale dokončené webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 12 ukazuje, jak vyvíjet sadu automatizovaných testů jednotek, které ověřují naše funkce NerdDinner a které nám poskytnou jistotu, že v budoucnu bude dělat změny a vylepšení aplikace.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme vám postupovat podle [Začínáme s kurzy pro](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [hudební úložiště](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) MVC 3 nebo MVC.

## <a name="nerddinner-step-12-unit-testing"></a>NerdDinner krok 12: testování částí

Pojďme vyvíjet sadu automatizovaných testů jednotek, které ověřují naše funkce NerdDinner a které nám poskytnou jistotu, že v budoucnu bude dělat změny a vylepšení aplikace.

### <a name="why-unit-test"></a>Proč testování částí?

Na jednotce po jednom ráno máte prudký inspiraciý blesk o aplikaci, na které pracujete. Zjistíte, že se vám dá udělat změna, kterou můžete implementovat. tím se aplikace výrazně zlepší. Může se jednat o refaktoring, který vyčistí kód, přidá novou funkci nebo opraví chybu.

Otázka, na kterou vás přijde, když jste dorazíte na váš počítač, je to, jak bezpečné je toto vylepšení? Co dělat v případě, že změna má vedlejší účinky nebo je něco rušena? Tato změna může být jednoduchá a implementace bude trvat jenom pár minut, ale co když trvá několik hodin k ručnímu otestování všech scénářů aplikací? Co když zapomenete pokrýt scénář a převedená aplikace přejde do produkčního prostředí? Je díky tomuto vylepšení skutečně všechno úsilí?

Automatizované testy jednotek můžou poskytovat bezpečnostní síť, která vám umožní průběžně vylepšovat aplikace a vyhnout se nebojte kódu, na kterém pracujete. Díky automatizovaným testům, které rychle ověřují funkčnost, můžete kódovat s jistotou a pomoct vám v tom, abyste mohli dělat vylepšení, která by mohla být neoprávněná. Také vám pomůžou vytvářet řešení, která jsou udržovatelná a delší životnost – což vede k mnohem vyšší návratnosti investic.

Rozhraní ASP.NET MVC umožňuje snadnou a přirozenou funkčnost aplikace testování částí. Také umožňuje pracovní postup vývoje řízený testováním (TDD), který umožňuje vývoj na základě testů.

### <a name="nerddinnertests-project"></a>Projekt NerdDinner. Tests

Když jsme na začátku tohoto kurzu vytvořili naši aplikaci NerdDinner, zobrazila se vám dialogové okno s dotazem, jestli jsme chtěli vytvořit projekt testování částí, abyste mohli přejít k projektu aplikace:

![](enable-automated-unit-testing/_static/image1.png)

Zavedli jsme vybraný přepínač Ano, vytvořit projekt testování částí – což vedlo k tomu, že se přidávají projekt "NerdDinner. Tests" do našeho řešení:

![](enable-automated-unit-testing/_static/image2.png)

Projekt NerdDinner. Tests odkazuje na sestavení projektu aplikace NerdDinner a umožňuje nám do něj snadno přidat automatizované testy, které ověřují funkčnost aplikace.

### <a name="creating-unit-tests-for-our-dinner-model-class"></a>Vytváření testů jednotek pro třídu modelu večeře

Pojďme přidat některé testy do našeho projektu NerdDinner. Tests, který ověří třídu večeře, kterou jsme vytvořili při sestavování naší vrstvy modelu.

Začneme vytvořením nové složky v rámci našeho testovacího projektu s názvem "modely", kde budeme umísťovat naše testy související s modelem. Potom Klikneme pravým tlačítkem na složku a vyberte příkaz **Přidat-&gt;nový test** nabídky. Tím se zobrazí dialogové okno Přidat nový test.

Zvolíme, že se má vytvořit "test jednotky" a pojmenovat ho "DinnerTest.cs":

![](enable-automated-unit-testing/_static/image3.png)

Když klikneme na tlačítko OK, Visual Studio přidá (a otevře) soubor DinnerTest.cs do projektu:

![](enable-automated-unit-testing/_static/image4.png)

Výchozí šablona testu jednotek sady Visual Studio má v ní spoustu kódů kotlového kódu, který se nachází v malém případě. Pojďme ho vyčistit pouze v následujícím kódu:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample1.cs)]

Atribut [TestClass] u třídy DinnerTest výše ho identifikuje jako třídu, která bude obsahovat testy, a také volitelnou inicializaci testu a kód rozboru. V rámci něj můžeme definovat testy přidáním veřejných metod, které mají pro ně atribut [TestMethod].

Níže jsou uvedené první ze dvou testů, které přidáme do naší třídy večeře. První test ověří, že je naším večeři neplatný, pokud se vytvoří nová večeři, aniž by byly správně nastavené vlastnosti. Druhý test ověří, že je naše večeře platná, když má večeře nastavené všechny vlastnosti s platnými hodnotami:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample2.cs)]

Všimněte si, že naše názvy testů jsou velmi explicitní (a jsou trochu podrobné). Provedeme to proto, že můžeme vytvořit stovky nebo tisíce malých testů a chceme zjednodušit rychlé určení záměru a chování každého z nich (zejména při prohlížení seznamu selhání v nástroji Test Runner). Názvy testů by měly být pojmenovány po testovaných funkcích. Nad\_by měl\_operace použít "substantivum".

Provádíme strukturování testů pomocí vzor testování "AAA" – který představuje "uspořádat, ACT, Assert":

- Uspořádat: nastavení testované jednotky
- ACT: vykonání jednotky v rámci testu a výsledků zachycení
- Assert: Ověřte chování.

Při psaní testů chceme zabránit tomu, aby byly jednotlivé testy příliš velké. Místo toho by každý test měl ověřit pouze jeden koncept (což bude mnohem snazší určit příčinu selhání). Dobrým pokynem je vyzkoušet a mít pouze jeden příkaz kontrolního výrazu pro každý test. Pokud máte více než jeden příkaz kontrolního výrazu v testovací metodě, ujistěte se, že jsou všechny použity pro otestování stejného konceptu. V případě pochybností proveďte jiný test.

### <a name="running-tests"></a>Spouštění testů

Visual Studio 2008 Professional (a novější edice) obsahují vestavěný Test Runner, který lze použít ke spuštění projektů testů jednotek sady Visual Studio v rámci rozhraní IDE. Můžeme vybrat příkaz **test-&gt;spustit-&gt;všechny testy v nabídce řešení** (nebo zadat Ctrl R, A) a spustit všechny naše testy jednotek. Případně můžete umístit kurzor do konkrétní třídy testu nebo testovací metodu a použít **test-&gt;spustit-&gt;testy v aktuálním příkazu místní** nabídky (nebo zadat Ctrl R, t) a spustit podmnožinu jednotek testů.

Pojďme umístit kurzor v rámci třídy DinnerTest a zadat "CTRL R, T" pro spuštění dvou testů, které jsme právě definovali. Když to uděláte, zobrazí se v sadě Visual Studio okno "Výsledky testů" a zobrazí se výsledky našich testovacích běhů uvedených v tomto příkladu:

![](enable-automated-unit-testing/_static/image5.png)

*Poznámka: v okně výsledků testů VS se ve výchozím nastavení nezobrazuje sloupec název třídy. To můžete přidat tak, že kliknete pravým tlačítkem myši do okna Výsledky testů a použijete příkaz nabídky Přidat/odebrat sloupce.*

Naše dva testy trvalo pouze zlomek sekundy ke spuštění – a jak vidíte, jak jsou předány. Nyní můžeme přejít a rozšířit tak, že vytvoříte další testy, které ověřují konkrétní pravidla, a pokryjeme dvě pomocné metody – IsUserHost () a IsUserRegistered () – přidané do třídy večeře. Všechny tyto testy, které jsou na místě pro třídu večeře, budou mnohem jednodušší a bezpečnější pro přidání nových obchodních pravidel a jejich platnosti do budoucna. Naši novou logiku pravidla můžeme přidat na večeři a potom během několika sekund ověřit, že se nepřerušila žádná z našich předchozích funkcí logiky.

Všimněte si, jak použít popisný název testu usnadňuje rychlé pochopení toho, co každý test ověřuje. Doporučuje se použít příkaz nabídky **Možnosti nástrojů-&gt;** , otevřít obrazovku konfigurace testovacích nástrojů –&gt;spuštění testu a zkontrolovat, že dvakrát kliknout na neúspěšný nebo neprůkazný výsledek testu jednotek, zobrazí v políčku test bod selhání. To vám umožní dvakrát kliknout na selhání v okně výsledky testu a okamžitě přejít k chybě kontrolního výrazu.

### <a name="creating-dinnerscontroller-unit-tests"></a>Vytváření testů jednotek DinnersController

Teď vytvoříme několik testů jednotek, které ověřují naše funkce DinnersController. Začneme tak, že kliknete pravým tlačítkem na složku Controllers v rámci našeho testovacího projektu a pak zvolíte příkaz **přidat&gt;nový test** nabídky. Vytvoříme "test jednotky" a pojmenujte ho "DinnersControllerTest.cs".

Vytvoříme dvě testovací metody, které ověří metodu akce Details () na DinnersController. Nejdřív se ověří, že se vrátí zobrazení, když se požaduje stávající večeře. Druhá se ověří, že se vrátí zobrazení "NotFound", když se požaduje neexistující večeře:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample3.cs)]

Výše uvedený kód se zkompiluje čistě. Když testy spustíme, dojde k jejich selhání:

![](enable-automated-unit-testing/_static/image6.png)

Pokud se podíváme na chybové zprávy, ukážeme, že důvodem neúspěchu testů bylo, že se naše třída DinnersRepository nemohla připojit k databázi. Naše aplikace NerdDinner používá řetězec připojení k místnímu SQL Server Express souboru, který je umístěn v adresáři \app\_datového adresáře projektu aplikace NerdDinner. Vzhledem k tomu, že náš projekt NerdDinner. Tests kompiluje a běží v jiném adresáři, pak projekt aplikace, umístění relativní cesty našeho řetězce připojení je nesprávné.

To *můžeme vyřešit* zkopírováním souboru databáze SQL Express do našeho testovacího projektu a potom do souboru App. config našeho testovacího projektu přidat příslušný testovací připojovací řetězec. To by vedlo k tomu, že výše uvedené testy nebudou odblokovány a spuštěny.

Testování částí kódu pomocí reálné databáze sice ale přináší množství výzev. Konkrétně:

- Významně zpomaluje dobu provádění testů jednotek. Čím déle trvá spuštění testů, tím méně pravděpodobně budete provádět často. V ideálním případě budete chtít, aby testy jednotek byly schopny běžet v řádu sekund – a mělo by to být něco, co provedete stejně přirozeně jako při kompilování projektu.
- V rámci testů ztěžuje logiku nastavení a vyčištění. Požadujete, aby byl každý test jednotky izolovaný a nezávisle na ostatních (bez vedlejších účinků nebo závislostí). Při práci na reálné databázi je nutné mít na vědomí stav a obnovit je mezi testy.

Pojďme se podívat na vzor návrhu s názvem "vložení závislostí", který nám může přispět k obejít těchto problémů a vyhnout se nutnosti používat skutečnou databázi s našimi testy.

### <a name="dependency-injection"></a>Injektáž závislostí

Teď DinnersController je úzce "spojená" se třídou DinnerRepository. "Spoj" odkazuje na situaci, kdy třída explicitně spoléhá na jinou třídu, aby fungovala:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample4.cs)]

Vzhledem k tomu, že třída DinnerRepository vyžaduje přístup k databázi, tak úzce propojená závislost třídy DinnersController na DinnerRepository končí, aby nám vyžadovala testování metod DinnersController akcí.

To můžeme obejít tak, že využijete vzor návrhu s názvem "injektáže závislosti" – což je přístup, ke kterému se již implicitně nevytváří závislosti (jako jsou třídy úložiště, které poskytují přístup k datům) ve třídách, které je používají. Místo toho je možné závislosti explicitně předat třídě, která je používá pomocí argumentů konstruktoru. Pokud jsou závislosti definovány pomocí rozhraní, můžeme mít flexibilitu při implementaci "falešného" implementace závislosti pro scénáře testování částí. Díky tomu můžeme vytvořit implementace závislostí specifické pro test, které ve skutečnosti nevyžadují přístup k databázi.

Pokud se chcete podívat, jak to funguje, můžeme implementovat vkládání závislostí s našimi DinnersController.

#### <a name="extracting-an-idinnerrepository-interface"></a>Extrakce rozhraní IDinnerRepository

Náš první krok vytvoří nové rozhraní IDinnerRepository, které zapouzdřuje kontrakty úložiště. naše řadiče potřebují načíst a aktualizovat večeři.

Tuto kontrakt rozhraní můžeme definovat ručně tak, že kliknete pravým tlačítkem na složku \Models a pak zvolíte příkaz nabídky **Přidat novou položku&gt;** a vytvoříte nové rozhraní s názvem IDinnerRepository.cs.

K automatickému extrakci a vytvoření rozhraní pro nás z naší existující třídy DinnerRepository můžeme použít nástroje refaktoringu, které jsou integrované Visual Studio Professional (a novější edice). Chcete-li toto rozhraní extrahovat pomocí VS, jednoduše umístěte kurzor do textového editoru ve třídě DinnerRepository a potom klikněte pravým tlačítkem myši a zvolte příkaz **refaktoring-&gt;Extrahování rozhraní** nabídky:

![](enable-automated-unit-testing/_static/image7.png)

Tím se otevře dialogové okno extrakce rozhraní a požádejte nás o název rozhraní, které se má vytvořit. Ve výchozím nastavení bude IDinnerRepository a automaticky vybírat všechny veřejné metody pro existující třídu DinnerRepository pro přidání do rozhraní:

![](enable-automated-unit-testing/_static/image8.png)

Po kliknutí na tlačítko OK bude Visual Studio do naší aplikace přidávat nové rozhraní IDinnerRepository:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample5.cs)]

A naše existující třída DinnerRepository se aktualizuje tak, aby implementovala rozhraní:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample6.cs)]

#### <a name="updating-dinnerscontroller-to-support-constructor-injection"></a>Aktualizace DinnersController na podporu injektáže konstruktoru

Teď aktualizujeme třídu DinnersController, aby používala nové rozhraní.

Aktuálně DinnersController je pevně zakódována tak, že jeho pole "dinnerRepository" je vždy třída DinnerRepository:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample7.cs)]

Změníme ji tak, aby pole dinnerRepository bylo typu IDinnerRepository namísto DinnerRepository. Pak přidáme dva veřejné konstruktory DinnersController. Jeden z konstruktorů umožňuje předávat IDinnerRepository jako argument. Druhý je výchozí konstruktor, který používá naši stávající implementaci DinnerRepository:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample8.cs)]

Vzhledem k tomu, že ASP.NET MVC ve výchozím nastavení vytvoří třídy kontroléru pomocí výchozích konstruktorů, náš DinnersController za běhu bude k provádění přístupu k datům dál používat třídu DinnerRepository.

Nyní můžeme aktualizovat naše testy jednotek, ale k předání "falešné" implementace úložiště večeře pomocí konstruktoru parametru. Toto "falešné" úložiště večeře nebude vyžadovat přístup ke skutečné databázi a místo toho bude používat ukázková data v paměti.

#### <a name="creating-the-fakedinnerrepository-class"></a>Vytvoření třídy FakeDinnerRepository

Pojďme vytvořit třídu FakeDinnerRepository.

Začneme vytvořením "falešného" adresáře v rámci našeho projektu NerdDinner. Tests a následně do něj přidáte novou FakeDinnerRepository třídu (klikněte pravým tlačítkem na složku a vyberte **Přidat-&gt;novou třídu**):

![](enable-automated-unit-testing/_static/image9.png)

Aktualizujeme kód tak, aby třída FakeDinnerRepository implementovala rozhraní IDinnerRepository. Pak na ni můžeme kliknout pravým tlačítkem a zvolit příkaz "implementovat rozhraní IDinnerRepository", který je v místní nabídce:

![](enable-automated-unit-testing/_static/image10.png)

To způsobí, že Visual Studio automaticky přidá všechny členy rozhraní IDinnerRepository do naší třídy FakeDinnerRepository s výchozími implementacemi "stub ven":

[!code-csharp[Main](enable-automated-unit-testing/samples/sample9.cs)]

Pak můžeme aktualizovat implementaci FakeDinnerRepository, aby fungovala v seznamu v paměti&lt;večeři&gt; z kolekce do ní jako argument konstruktoru:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample10.cs)]

Nyní máme falešnou implementaci IDinnerRepository, která nevyžaduje databázi, a může místo toho pracovat v seznamu objektů večeře v paměti.

#### <a name="using-the-fakedinnerrepository-with-unit-tests"></a>Použití FakeDinnerRepository s testováním částí

Pojďme se vrátit k testům DinnersController jednotek, které se dřív nezdařily, protože databáze nebyla k dispozici. Testovací metody můžeme aktualizovat tak, aby používaly FakeDinnerRepository vyplněné pomocí ukázky dat s daty o večeři v paměti pro DinnersController pomocí následujícího kódu:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample11.cs)]

A teď když spustíme tyto testy, oba projdou:

![](enable-automated-unit-testing/_static/image11.png)

To nejlepší z nich trvá pouze zlomek sekundy ke spuštění a nevyžadují žádnou složitou logiku nastavení/vyčištění. Nyní můžeme otestovat všechny naše kódy metod DinnersController akce (včetně výpisu, stránkování, podrobností, vytvoření, aktualizace a odstranění), aniž byste museli se připojit ke skutečné databázi.

| **Vedlejší téma: rozhraní pro vkládání závislostí** |
| --- |
| Provedení ručního vkládání závislostí (podobně jako v předchozím případě) funguje bez problémů, ale je těžší je udržovat, protože se zvyšuje počet závislostí a komponent v aplikaci. Pro rozhraní .NET existuje několik platforem vkládání závislostí, které vám pomůžou zajistit ještě větší flexibilitu pro správu závislostí. Tyto architektury, někdy označované také jako "inverze ovládacích prvků" (IoC), poskytují mechanismy, které umožňují další úroveň konfigurace pro zadání a předání závislostí objektům v době běhu (nejčastěji pomocí injektáže konstruktoru). ). Mezi nejoblíbenější rozhraní injektáže/IOC závislostí OSS v rozhraní .NET patří: AutoFac, Ninject, Spring.NET, StructureMap a Windsor. ASP.NET MVC zpřístupňuje rozhraní API pro rozšiřitelnost, která vývojářům umožňují zapojit se do řešení a vytváření instancí řadičů a která umožňuje čistě integrovat rozhraní injektáže/IoC pro závislosti v rámci tohoto procesu. Použití rozhraní DI/IOC by nám také umožnilo odebrat výchozí konstruktor z našeho DinnersController – což by zcela odebralo spojení mezi ním a DinnerRepository. V naší aplikaci NerdDinner nebudeme používat rozhraní pro vkládání závislostí/IOC. Ale je to něco, co můžeme v budoucnu zvážit, pokud se NerdDinner základ kódu a možnosti. |

### <a name="creating-edit-action-unit-tests"></a>Vytváření testů jednotek akcí úprav

Pojďme teď vytvořit několik testů jednotek, které ověřují funkčnost DinnersController. Začneme otestováním verze HTTP-GET naší akce úprav:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample12.cs)]

Vytvoříme test, který ověří, že zobrazení, které je zajištěné objektem DinnerFormViewModel, se vrátí zpět, když se požaduje platná večeře:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample13.cs)]

Když tento test spustíte, zjistíme, že se to nepovede, protože je vyvolána výjimka odkazu s hodnotou null, pokud metoda Edit přistupuje k vlastnosti User.Identity.Name, která provede kontrolu večeři. IsHostedBy ().

Objekt uživatele v základní třídě kontroleru zapouzdřuje podrobnosti o přihlášeném uživateli a při vytváření kontroleru za běhu ho naplní ASP.NET MVC. Vzhledem k tomu, že testujeme DinnersController mimo prostředí webového serveru, objekt uživatele není nastaven (tedy výjimka odkazu s hodnotou null).

### <a name="mocking-the-useridentityname-property"></a>Napodobení vlastnosti User.Identity.Name

Napodobení rozhraní usnadňuje testování tím, že nám umožní dynamicky vytvářet falešné verze závislých objektů, které podporují naše testy. Například můžeme použít napodobnou architekturu v testu akcí úprav k dynamickému vytvoření objektu uživatele, který může DinnersController použít k vyhledání simulovaného uživatelského jména. Tím se vyhnete vyjímka nulového odkazu, když spustíme náš test.

Existuje mnoho rozhraní .NET, které lze použít s ASP.NET MVC (můžete zobrazit jejich seznam: [http://www.mockframeworks.com/](http://www.mockframeworks.com/)). Pro testování naší aplikace NerdDinner použijeme Open Source modelující rozhraní s názvem "MOQ", které se dá zdarma stáhnout z [http://www.mockframeworks.com/moq](http://www.mockframeworks.com/moq).

Po stažení přidáme odkaz do našeho projektu NerdDinner. Tests do sestavení MOQ. dll:

![](enable-automated-unit-testing/_static/image12.png)

Pak přidáte pomocnou metodu "CreateDinnersControllerAs (uživatelské jméno)" do naší třídy testu, která převezme uživatelské jméno jako parametr a pak "navýšení" vlastnosti User.Identity.Name na instanci DinnersController:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample14.cs)]

Výše používáme MOQ k vytvoření objektu makety, který předstírá objekt ControllerContext (což je to, co ASP.NET MVC projde do tříd kontroleru a zpřístupňuje běhové objekty, jako je uživatel, požadavek, odpověď a relace). Voláme metodu "SetupGet" na tomto typu, aby označovala, že vlastnost HttpContext.User.Identity.Name v ControllerContext by měla vracet uživatelský řetězec, který předal pomocná metoda.

Můžeme navýšit libovolný počet ControllerContext vlastností a metod. Pro ilustraci toho jsem také přidali volání SetupGet () pro vlastnost Request. Authentication (která není ve skutečnosti nutná pro následující testy, ale pomáhá ilustrovat, jak můžete popsáním vlastností žádosti). Až se dokončíme, přiřadíme instanci ControllerContextového objektu k DinnersController, že se naše pomocná metoda vrátí.

Nyní můžeme napsat testy jednotek, které používají tuto pomocnou metodu k testování scénářů úprav týkajících se různých uživatelů:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample15.cs)]

A teď když spustíme testy, které projdou:

![](enable-automated-unit-testing/_static/image13.png)

### <a name="testing-updatemodel-scenarios"></a>Testování scénářů UpdateModel ()

Vytvořili jsme testy, které pokrývají verzi HTTP-GET akce upravit. Teď vytvoříme některé testy, které ověřují verzi HTTP-POST akce upravit:

[!code-csharp[Main](enable-automated-unit-testing/samples/sample16.cs)]

Zajímavý nový scénář testování, který podporuje podporu pomocí této metody Action, je jeho využití pomocné metody UpdateModel () na základní třídě kontroleru. Tuto pomocnou metodu používáme k vytvoření vazby hodnot formuláře-post k naší instanci objektu večeře.

Níže jsou dva testy, které demonstrují, jak můžeme dodat vyslané hodnoty pro pomocnou metodu UpdateModel (), která se má použít. Provedeme to tak, že vytvoříme a naplníme objekt objektucollection a pak ho přiřadíte do vlastnosti "ValueProvider" na řadiči.

První test ověří, zda je v úspěšném uložení prohlížeč přesměrován na akci podrobnosti. Druhý test ověří, zda je při odeslání neplatného vstupu Tato akce znovu znovu zobrazuje zobrazení pro úpravy s chybovou zprávou.

[!code-csharp[Main](enable-automated-unit-testing/samples/sample17.cs)]

### <a name="testing-wrap-up"></a>Testování zabalení

Pokryli jsme základní koncepty týkající se tříd kontroleru testování částí. Tyto techniky můžeme použít k snadnému vytvoření stovek jednoduchých testů, které ověřují chování naší aplikace.

Vzhledem k tomu, že naše testy kontrol řadičů a modelů nevyžadují skutečnou databázi, jsou extrémně rychlé a snadno se spouštějí. V řádu sekund budeme moci spustit stovky automatizovaných testů a okamžitě získat zpětnou vazbu, ať už jsme udělali změnu, kterou jsme podařilo přerušiti. To nám pomůže zajistit nepřetržitou vylepšování naší aplikace, refaktorování a upřesnění naší aplikace.

Pokryli jsme testování jako poslední téma v této kapitole – ale ne, protože testování je něco, co byste měli dělat na konci procesu vývoje! V opačném případě byste měli psát automatizované testy co nejdříve v procesu vývoje. Díky tomu můžete při vývoji získat okamžitou zpětnou vazbu, která vám pomůže představit Thoughtfully o scénářích použití vaší aplikace a provede vás návrhem aplikace pomocí čistého vrstvení a přihlašování.

Pozdější kapitola v knize bude diskutovat o vývoji řízených testováním (TDD) a jeho použití s ASP.NET MVC. TDD je iterativní postup kódování, kde nejprve zapíšete testy, které váš výsledný kód bude vyhovovat. Pomocí TDD zahájíte jednotlivé funkce vytvořením testu, který ověří funkčnost, kterou se chystáte implementovat. Zapsání testu jednotek jako první vám pomůže zajistit, že tato funkce bude jasně srozumitelná a jak má fungovat. Až po zápisu testu (a ověření, že se nezdařil), implementujete vlastní funkce, které test ověří. Vzhledem k tomu, že jste už věnovali čas v tom, jak má funkce fungovat, budete mít lepší znalosti o požadavcích a jejich implementaci. Až budete s implementací hotovi, můžete znovu spustit test – a získat okamžitou zpětnou vazbu k tomu, zda funkce funguje správně. V kapitole 10 se budeme zabývat více TDD.

### <a name="next-step"></a>Další krok

Některé konečné komentáře k zabalení.

> [!div class="step-by-step"]
> [Předchozí](use-ajax-to-implement-mapping-scenarios.md)
> [Další](nerddinner-wrap-up.md)

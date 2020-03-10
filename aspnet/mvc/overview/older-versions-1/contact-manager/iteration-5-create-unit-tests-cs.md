---
uid: mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-cs
title: 'Iterace #5 – vytvoření testů jednotekC#() | Microsoft Docs'
author: microsoft
description: V páté iteraci aplikace usnadňuje údržbu a úpravy přidáním jednotkových testů. Napodobme si naše třídy datového modelu a vytvoříme testy jednotek pro o...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 28ad8f80-b8a5-444e-b478-8b15a846060c
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-5-create-unit-tests-cs
msc.type: authoredcontent
ms.openlocfilehash: 32e81cce34a0e0b1f6b01934334e1b66dce89651
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544301"
---
# <a name="iteration-5--create-unit-tests-c"></a>Iterace #5 – vytvoření testů jednotekC#()

od [Microsoftu](https://github.com/microsoft)

[Stáhnout kód](iteration-5-create-unit-tests-cs/_static/contactmanager_5_cs1.zip)

> V páté iteraci aplikace usnadňuje údržbu a úpravy přidáním jednotkových testů. Pro naše řadiče a logiku ověřování jsme nastavili třídy datového modelu a testy jednotek.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>Sestavování aplikace pro správu kontaktů ASP.NETC#MVC ()

V této sérii kurzů sestavíme celou aplikaci pro správu kontaktů od začátku do konce. Aplikace Správce kontaktů umožňuje ukládat kontaktní údaje – jména, telefonní čísla a e-mailové adresy – seznam lidí.

Aplikaci sestavíme přes několik iterací. U každé iterace doporučujeme aplikaci postupně vylepšit. Cílem tohoto vícenásobného přístupu k iteraci je umožnit pochopení příčiny každé změny.

- Iterace #1 – Vytvoření aplikace V první iteraci vytvoříme nejjednodušším způsobem správce kontaktů. Přidáváme podporu základních databázových operací: vytváření, čtení, aktualizace a odstraňování (CRUD).

- Iterace #2 – nastaví vzhled aplikace jako příjemné. V této iteraci Vylepšete vzhled aplikace úpravou výchozí stránky předlohy zobrazení ASP.NET MVC a šablony kaskádových stylů.

- Iterace #3 – Přidání ověření formuláře. Třetí iterace přidá základní ověřování formuláře. Uživatelům bráníme v odesílání formuláře bez nutnosti vyplnit požadovaná pole formuláře. Ověřujeme taky e-mailové adresy a telefonní čísla.

- Iterace #4 – zajistěte, aby byla aplikace volně spojená. V této čtvrté iteraci využijeme několik vzorů návrhu softwaru, které usnadňují údržbu a úpravy aplikace Správce kontaktů. Například refaktorujte naši aplikaci, aby používala vzor úložiště a vzor vkládání závislostí.

- Iterace #5 – vytvoření testů jednotek. V páté iteraci aplikace usnadňuje údržbu a úpravy přidáním jednotkových testů. Pro naše řadiče a logiku ověřování jsme nastavili třídy datového modelu a testy jednotek.

- Iterace #6 – použití vývoje řízeného testem. V této šesté iteraci přidáme do naší aplikace nové funkce, a to tak, že nejprve zapíšeme testy jednotek a napíšeme kód na testy jednotek. V této iteraci přidáváme skupiny kontaktů.

- Iterace #7 – přidání funkce AJAX V sedmé iteraci vylepšit rychlost reakce a výkon naší aplikace přidáním podpory pro AJAX.

## <a name="this-iteration"></a>Tato iterace

V předchozí iteraci aplikace Správce kontaktů jsme aplikaci znovu rozdělili tak, aby byla uvolněna. Aplikaci jsme oddělili na samostatné vrstvy řadiče, služby a úložiště. Každá vrstva komunikuje s vrstvou pod ní přes rozhraní.

Aplikaci jsme refaktoringem zajistili snazší údržbu a úpravy aplikace. Například pokud potřebujeme používat novou technologii pro přístup k datům, můžeme jednoduše změnit vrstvu úložiště, aniž byste se museli dotýkat řadiče nebo vrstvy služeb. Tím, že se správce kontaktů volně spojí, udělali jsme aplikaci, která je pružná a mění.

Ale co se stane, když musíme do aplikace Správce kontaktů přidat novou funkci? Nebo co se stane, když opravujeme chybu? JSD, ale dobře prověřená, pravdivost psaní kódu je to, že při každém dotykovém kódu vytvoříte riziko pro zavlečení nových chyb.

Například jeden jemný den, váš nadřízený může požádat o přidání nové funkce do Správce kontaktů. Chce přidat podporu pro skupiny kontaktů. Chce uživatelům povolit uspořádání kontaktů do skupin, jako jsou přátele, firmy a tak dále.

Aby bylo možné tuto novou funkci implementovat, je nutné upravit všechny tři vrstvy aplikace Správce kontaktů. Budete muset přidat nové funkce do řadičů, do vrstvy služeb a do úložiště. Jakmile začnete upravovat kód, riskujete, že jste přestali fungovat dříve.

Použití refaktoringu naší aplikace do samostatných vrstev, stejně jako v předchozí iteraci, bylo dobré. To je dobré, protože nám umožňuje provádět změny celých vrstev bez toho, aby se dotkli zbytku aplikace. Nicméně pokud chcete, aby byl kód v rámci vrstvy snazší udržovat a upravovat, je nutné pro kód vytvořit testy jednotek.

Testování částí lze použít k otestování jednotlivé jednotky kódu. Tyto jednotky kódu jsou menší než celé vrstvy aplikace. Obvykle používáte test jednotek k ověření, zda se konkrétní metoda v kódu chová způsobem, jaký očekáváte. Například byste vytvořili test jednotky pro metodu CreateContact () zveřejněnou třídou ContactManagerService.

Testování částí aplikace funguje stejně jako síť pro bezpečnost. Kdykoli upravíte kód v aplikaci, můžete spustit sadu testů jednotek a ověřit, zda změna přeruší existující funkce. Testování částí usnadňuje úpravy kódu. Testování částí usnadňuje změnu celého kódu v aplikaci.

V této iteraci přidáme testování částí do naší aplikace Správce kontaktů. Tímto způsobem můžeme do naší aplikace přidat skupiny kontaktů, aniž byste se museli starat o přerušení stávajících funkcí.

> [!NOTE] 
> 
> Existuje řada platforem testování částí, včetně NUnit, xUnit.net a MbUnit. V tomto kurzu používáme rozhraní testování částí, které je součástí sady Visual Studio. Můžete ale jednoduše použít jednu z těchto alternativních rozhraní.

## <a name="what-gets-tested"></a>Co se testuje

V ideálním světě by veškerý kód byl pokryt testy jednotek. V ideálním světě byste měli dokonalý bezpečnostní síť. V aplikaci byste mohli změnit libovolný řádek kódu a okamžitě se dozvědět, že se spustí testy jednotek, ať už změna podařilo přerušit stávající funkce.

Ale nepůjde živě na dokonalém světě. V praxi se při psaní testů jednotek soustředíte na zápis testů pro obchodní logiku (například logika ověřování). Konkrétně *nepíšete* testy jednotek pro logiku přístupu k datům nebo logiku zobrazení.

Aby bylo možné provádět testy jednotek, je nutné provést velmi rychle. Snadno můžete shromáždit stovky (nebo dokonce tisíce) testů jednotek pro aplikaci. Pokud spuštění testů jednotek trvá dlouhou dobu, pak se vyhnete jejich spouštění. Jinými slovy, dlouhodobě běžící testy jednotek jsou k disměrnému pro každodenní účely kódování.

Z tohoto důvodu obvykle nepíšete testy jednotek pro kód, který komunikuje s databází. Spouštění stovek jednotek testů proti živé databázi by bylo příliš pomalé. Místo toho můžete napodobovat databázi a napsat kód, který komunikuje s databází typu (projednáváme si napodobení databáze níže).

Z podobného důvodu obvykle nepíšete testy jednotek pro zobrazení. Aby bylo možné otestovat zobrazení, je nutné vystavit webový server. Vzhledem k tomu, že při odstřeďování webového serveru je poměrně pomalý proces, vytváření testů jednotek pro zobrazení se nedoporučuje.

Pokud vaše zobrazení obsahuje složitou logiku, měli byste zvážit přesunutí logiky do pomocných metod. Můžete napsat testy jednotek u pomocných metod, které se spouštějí bez otáčející se webového serveru.

> [!NOTE] 
> 
> Zatímco zápis testů logiky přístupu k datům nebo logiky zobrazení není dobrý nápad při psaní testů jednotek, tyto testy mohou být velmi užitečné při sestavování funkčních nebo integračních testů.

> [!NOTE] 
> 
> ASP.NET MVC je modul zobrazení webových formulářů. I když je modul zobrazení webových formulářů závislý na webovém serveru, jiné moduly zobrazení nemusí být.

## <a name="using-a-mock-object-framework"></a>Použití rozhraní makety objektu

Při sestavování testů jednotek, téměř vždy potřebujete využívat výhod rozhraní pro maketu objektů. Rozhraní typu Object Framework umožňuje vytvořit pro třídy v aplikaci modely a zástupné procedury.

Například můžete použít objektové rozhraní objektu pro vytváření vzorové verze vaší třídy úložiště. Tímto způsobem můžete použít třídu úložiště s přípravou namísto reálné třídy úložiště ve vašich testech jednotek. Použití modelového úložiště vám umožní vyhnout se spouštění kódu databáze při provádění testu jednotek.

Sady Visual Studio neobsahují architekturu objektových modelů. Pro rozhraní .NET Framework je však k dispozici několik komerčních a open source modelů objektů:

1. MOQ – tato architektura je k dispozici v rámci licence Open Source BSD. MOQ si můžete stáhnout z [https://code.google.com/p/moq/](https://code.google.com/p/moq/).
2. Rhinoy – tato architektura je k dispozici v rámci licence Open Source BSD. Z [http://ayende.com/projects/rhino-mocks.aspx](http://ayende.com/projects/rhino-mocks.aspx)můžete stáhnout přípravou z Rhino.
3. Typemock izolujte – jedná se o komerční rozhraní. Zkušební verzi si můžete stáhnout z [http://www.typemock.com/](http://www.typemock.com/).

V tomto kurzu jsem se rozhodl používat MOQ. Mohli byste ale jednoduše použít Rhino nebo Typemock, a vytvořit tak pro aplikaci Správce kontaktů objekty.

Než budete moct používat MOQ, musíte provést následující kroky:

1. .
2. Před rozbalením stahování se ujistěte, že kliknete pravým tlačítkem na soubor a kliknete na tlačítko s popiskem **odblokování** (viz obrázek 1).
3. Rozbalte soubor ke stažení.
4. Přidejte odkaz na MOQ sestavení tak, že kliknete pravým tlačítkem na složku odkazy v projektu ContactManager. Tests a vyberete **Přidat odkaz**. Na kartě Procházet přejděte do složky, kde jste MOQ, a vyberte sestavení MOQ. dll. Klikněte na tlačítko **OK**.
5. Po dokončení tohoto postupu by měla složka s odkazy vypadat jako na obrázku 2.

[![odblokování MOQ](iteration-5-create-unit-tests-cs/_static/image1.jpg)](iteration-5-create-unit-tests-cs/_static/image1.png)

**Obrázek 01**: odblokování MOQ ([kliknutím zobrazíte obrázek v plné velikosti](iteration-5-create-unit-tests-cs/_static/image2.png))

[![odkazů po přidání MOQ](iteration-5-create-unit-tests-cs/_static/image2.jpg)](iteration-5-create-unit-tests-cs/_static/image3.png)

**Obrázek 02**: odkazy po přidání MOQ ([kliknutím zobrazíte obrázek v plné velikosti](iteration-5-create-unit-tests-cs/_static/image4.png))

## <a name="creating-unit-tests-for-the-service-layer"></a>Vytváření testů jednotek pro vrstvu služby

Nechte začít vytvořením sady testů jednotek pro naši aplikační vrstvu správce kontaktů. Tyto testy použijeme k ověření naší ověřovací logiky.

Vytvořte novou složku s názvem modely v projektu ContactManager. Tests. Potom klikněte pravým tlačítkem na složku modely a vyberte **Přidat, nový test**. Zobrazí se dialogové okno **Přidat nový test** zobrazené na obrázku 3. Vyberte šablonu **testu jednotek** a pojmenujte nový test ContactManagerServiceTest.cs. Kliknutím na tlačítko **OK** přidejte nový test do projektu testů.

> [!NOTE] 
> 
> Obecně platí, že chcete, aby struktura složky testovacího projektu odpovídala struktuře složek projektu ASP.NET MVC. Například můžete umístit testy řadiče do složky Controllers, modelovat testy ve složce modelů a tak dále.

[![Models\ContactManagerServiceTest.cs](iteration-5-create-unit-tests-cs/_static/image3.jpg)](iteration-5-create-unit-tests-cs/_static/image5.png)

**Obrázek 03**: Models\ContactManagerServiceTest.cs ([kliknutím zobrazíte obrázek v plné velikosti](iteration-5-create-unit-tests-cs/_static/image6.png))

Zpočátku chceme otestovat metodu CreateContact () zveřejněnou třídou ContactManagerService. Vytvoříme následující pět testů:

- CreateContact () – testy, které CreateContact () vrátí hodnotu true, pokud je do metody předán platný kontakt.
- CreateContactRequiredFirstName () – testuje, zda je chybová zpráva přidána do stavu modelu, pokud je předán kontakt s chybějícím křestním jménem do metody CreateContact ().
- CreateContactRequiredLastName () – testuje, zda je chybová zpráva přidána do stavu modelu, pokud je předán kontakt s chybějícím posledním názvem metodě CreateContact ().
- CreateContactInvalidPhone () – testuje, zda je do stavu modelu přidána chybová zpráva, když je do metody CreateContact () předán kontakt s neplatným telefonním číslem.
- CreateContactInvalidEmail () – testuje, zda je do stavu modelu přidána chybová zpráva, když je do metody CreateContact () předán kontakt s neplatnou e-mailovou adresou..

První test ověří, zda platný kontakt negeneruje chybu ověřování. Zbývající testy kontrolují každé z ověřovacích pravidel.

Kód pro tyto testy je obsažen v seznamu 1.

**Výpis 1 – Models\ContactManagerServiceTest.cs**

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample1.cs)]

Protože používáme třídu Contact v seznamu 1, musíme do našeho testovacího projektu přidat odkaz na Microsoft Entity Framework. Přidejte odkaz na sestavení System. data. entity.

Výpis 1 obsahuje metodu s názvem Initialize (), která je upravena pomocí atributu [TestInitialize]. Tato metoda je volána automaticky před každým spuštěním testu jednotek (je označována jako 5 časů přímo před každou jednotkou testů). Metoda Initialize () vytvoří maketu úložiště s následujícím řádkem kódu:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample2.cs)]

Tento řádek kódu používá MOQ Framework pro generování napodobné úložiště z rozhraní IContactManagerRepository. Místo skutečného EntityContactManagerRepository se použije Maketové úložiště, aby se předešlo přístupu k databázi při každém spuštění testu jednotek. Maketa úložiště implementuje metody rozhraní IContactManagerRepository, ale metody nedělají vůbec žádnou hodnotu.

> [!NOTE] 
> 
> Při použití rozhraní MOQ Framework existuje rozdíl mezi \_mockRepository a \_mockRepository. Object. Předchozí odkazuje na&lt;&gt; třídy, která obsahuje metody pro určení způsobu, jakým se bude napodobné úložiště chovat. Druhý odkazuje na vlastní maketu úložiště, které implementuje rozhraní IContactManagerRepository.

V metodě Initialize () se používá Maketové úložiště při vytváření instance třídy ContactManagerService. Všechny testy jednotlivých jednotek používají tuto instanci třídy ContactManagerService.

Výpis 1 obsahuje pět metod, které odpovídají jednotlivým jednotkovým testům. Každá z těchto metod je upravena s použitím atributu [TestMethod]. Při spuštění testů jednotek je volána jakákoli metoda, která má tento atribut. Jinými slovy jakákoli metoda, která je upravena s atributem [TestMethod] je test jednotky.

První test jednotky s názvem CreateContact () ověří, že volání CreateContact () vrátí hodnotu true, pokud je do metody předána platná instance třídy Contact. Test vytvoří instanci třídy Contact, zavolá metodu CreateContact () a ověří, zda CreateContact () vrátí hodnotu true.

Zbývající testy ověří, že když je metoda CreateContact () volána s neplatným kontaktem, vrátí metoda hodnotu false a do stavu modelu se přidá očekávaná chybová zpráva ověřování. Například test CreateContactRequiredFirstName () vytvoří instanci třídy Contact s prázdným řetězcem pro jeho vlastnost FirstName. Dále je volána metoda CreateContact () s neplatným kontaktem. Nakonec test ověří, že CreateContact () vrátí hodnotu false a stav modelu obsahuje očekávanou chybovou zprávu ověření "křestní jméno je povinné."

Můžete spustit testy jednotek v seznamu 1 výběrem možnosti nabídka **test, spustit, všechny testy v řešení (CTRL + R, a)** . Výsledky testů se zobrazí v okně Výsledky testů (viz obrázek 4).

[![Výsledky testů](iteration-5-create-unit-tests-cs/_static/image4.jpg)](iteration-5-create-unit-tests-cs/_static/image7.png)

**Obrázek 04**: výsledky testů ([kliknutím zobrazíte obrázek v plné velikosti](iteration-5-create-unit-tests-cs/_static/image8.png))

## <a name="creating-unit-tests-for-controllers"></a>Vytváření testů jednotek pro řadiče

Aplikace ASP. NETMVC řídí tok interakce s uživatelem. Při testování kontroleru budete chtít otestovat, zda kontroler vrátí výsledek správné akce a zobrazí data. Také může být vhodné otestovat, zda řadič komunikuje s třídami modelů podle očekávání.

Například výpis 2 obsahuje dvě testy jednotek metody Create () Správce kontaktů. První test jednotky ověřuje, že pokud je do metody Create () předán platný kontakt, přesměruje metoda Create () na akci indexu. Jinými slovy, pokud byl předán platný kontakt, metoda Create () by měla vrátit RedirectToRouteResult, který představuje akci indexu.

Při testování vrstvy kontroleru nechceme testovat vrstvu služby ContactManager. Proto se vrstva služby napodobá následujícímu kódu v metodě Initialize:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample3.cs)]

V testu jednotky CreateValidContact () jsme nazkoušeli chování volání metody Service Layer CreateContact () s následujícím řádkem kódu:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample4.cs)]

Tento řádek kódu způsobí, že ContactManagerová služba vrátí hodnotu true při volání metody CreateContact (). Po napodobování vrstvy služby můžeme otestovat chování našeho kontroleru, aniž byste museli spouštět žádný kód ve vrstvě služeb.

Druhý test jednotek ověří, že akce Create () vrátí zobrazení vytvořit, když je metodě předán neplatný kontakt. Způsob, jakým metodu Service Layer CreateContact () vrací hodnotu false, je následující řádek kódu:

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample5.cs)]

Pokud se metoda Create () chová podle očekávání, měla by vrátit zobrazení vytvořit, když vrstva služby vrátí hodnotu false. Tímto způsobem může kontroler zobrazit chybové zprávy ověřování v zobrazení vytvořit a uživatel má možnost opravit neplatné vlastnosti kontaktu.

Pokud plánujete sestavit testy jednotek pro řadiče, budete muset vrátit explicitní názvy zobrazení z akcí kontroleru. Nevracet například zobrazení jako:

vrátit zobrazení ();

Místo toho vraťte zobrazení následujícím způsobem:

návratové zobrazení ("vytvořit");

Pokud nejste explicitní při vracení zobrazení, vlastnost ViewResult. ViewName vrátí prázdný řetězec.

**Výpis 2 – Controllers\ContactControllerTest.cs**

[!code-csharp[Main](iteration-5-create-unit-tests-cs/samples/sample6.cs)]

## <a name="summary"></a>Souhrn

V této iteraci jsme pro naši aplikaci Správce kontaktů vytvořili testy jednotek. Tyto jednotkové testy můžeme kdykoli spustit, abyste ověřili, že se aplikace pořád chová způsobem, který očekáváme. Testování částí působí jako bezpečnostní síť pro naši aplikaci, která nám umožňuje bezpečně upravit naši aplikaci v budoucnu.

Vytvořili jsme dvě sady testů jednotek. Nejdřív jsme otestovali naši logiku ověřování vytvořením testů jednotek pro naši vrstvu služeb. Dále jsme otestovali naši logiku řízení toku vytvořením testů jednotek pro naši řídicí vrstvu. Při testování naší vrstvy služby jsme z naší vrstvy úložiště zavedli naše testy pro naši vrstvu služby, a to tak, že nasadíme naši vrstvu úložiště. Při testování vrstvy kontroleru jsme izolované testy pro vrstvu řadiče, a to vytvořením vrstvy služby.

V další iteraci upravíte aplikaci Správce kontaktů tak, aby podporovala skupiny kontaktů. Tuto novou funkci přidáme do naší aplikace pomocí procesu návrhu softwaru označovaného jako vývoj řízený testováním.

> [!div class="step-by-step"]
> [Předchozí](iteration-4-make-the-application-loosely-coupled-cs.md)
> [Další](iteration-6-use-test-driven-development-cs.md)

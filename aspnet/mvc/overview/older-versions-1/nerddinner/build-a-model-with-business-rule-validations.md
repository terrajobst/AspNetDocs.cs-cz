---
uid: mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
title: Vytvoření modelu s platnými obchodními pravidly | Microsoft Docs
author: microsoft
description: V kroku 3 se dozvíte, jak vytvořit model, který můžeme použít k dotazování a aktualizaci databáze pro naši aplikaci NerdDinner.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 0bc191b2-4311-479a-a83a-7f1b1c32e6fe
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/build-a-model-with-business-rule-validations
msc.type: authoredcontent
ms.openlocfilehash: 6ebf1b71c089229ba9139ff7dc788b8978724046
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541662"
---
# <a name="build-a-model-with-business-rule-validations"></a>Vytvoření modelu s ověřením obchodních pravidel

od [Microsoftu](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 3 bezplatného [kurzu aplikace "NerdDinner"](introducing-the-nerddinner-tutorial.md) , který vás provede procesem vytvoření malé, ale dokončené webové aplikace pomocí ASP.NET MVC 1.
> 
> V kroku 3 se dozvíte, jak vytvořit model, který můžeme použít k dotazování a aktualizaci databáze pro naši aplikaci NerdDinner.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme vám postupovat podle [Začínáme s kurzy pro](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [hudební úložiště](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) MVC 3 nebo MVC.

## <a name="nerddinner-step-3-building-the-model"></a>NerdDinner krok 3: sestavování modelu

V rámci architektury zobrazení modelu pojem "model" odkazuje na objekty, které představují data aplikace, a na odpovídající logiku domény, která s ním integruje ověřování a obchodní pravidla. Model je v mnoha ohledech na "srdce" aplikace založené na MVC a jak uvidíme později v podstatě jejich chování.

Rozhraní ASP.NET MVC podporuje používání jakékoli technologie pro přístup k datům a vývojáři si můžou vybrat z nejrůznějších různých možností dat .NET k implementaci svých modelů, včetně: LINQ to Entities, LINQ to SQL, NHibernate, LLBLGen pro, antisonic, WilsonORM nebo jenom nezpracovaných objektů ADO. NET datačtecís nebo DataSets.

Pro naši aplikaci NerdDinner budeme používat LINQ to SQL k vytvoření jednoduchého modelu, který přesně odpovídá návrhu naší databáze, a přidá několik vlastních ověřovacích logik a obchodních pravidel. Pak budeme implementovat třídu úložiště, která pomůže abstrakci při implementaci trvalosti dat ze zbytku aplikace, a umožňuje nám ji snadno otestovat.

### <a name="linq-to-sql"></a>Technologie LINQ to SQL

LINQ to SQL je ORM (objekt relačního mapovače), který je dodáván jako součást .NET 3,5.

LINQ to SQL poskytuje snadný způsob, jak mapovat tabulky databáze na třídy .NET, ke kterým můžeme zakódovat. Pro naši aplikaci NerdDinner ji použijeme k namapování tabulek večeře a RSVP v naší databázi na třídy večeře a RSVP. Sloupce večeře a tabulek protokolu RSVP budou odpovídat vlastnostem na třídách večeře a RSVP. Každý z nich a objekt protokolu RSVP bude představovat samostatný řádek v rámci v tabulkách večeře nebo RSVP v databázi.

LINQ to SQL nám umožňuje vyhnout se nutnosti ruční konstrukce příkazů SQL pro načtení a aktualizaci dat o večeři a protokolu RSVP s daty databáze. Místo toho definujeme třídy večeře a RSVP, jejich mapování na databázi a jejich vztahy mezi nimi. LINQ to SQL se pak postará o vygenerování vhodné logiky spuštění SQL, která se použije za běhu při interakci a používání.

Podporu jazyka LINQ v jazyce VB můžeme použít v rámci C# jazyka VB a k zápisu dotazů, které načítají z databáze večeři a objekty RSVP. Tím se minimalizuje množství datových kódů, které potřebujeme napsat, a umožníme nám sestavovat skutečně čisté aplikace.

### <a name="adding-linq-to-sql-classes-to-our-project"></a>Přidání tříd LINQ to SQL do našeho projektu

Začneme tak, že kliknete pravým tlačítkem na složku modely v našem projektu a vyberete příkaz nabídky **přidat&gt;novou položku** :

![](build-a-model-with-business-rule-validations/_static/image1.png)

Tím se zobrazí dialogové okno Přidat novou položku. Vyfiltrujeme podle kategorie "data" a v ní vyberete šablonu "LINQ to SQL třídy":

![](build-a-model-with-business-rule-validations/_static/image2.png)

Pojmenujte položku "NerdDinner" a klikněte na tlačítko Přidat. Visual Studio přidá do našeho adresáře \Models soubor NerdDinner. dbml a pak otevře návrháře relačních objektů LINQ to SQL:

![](build-a-model-with-business-rule-validations/_static/image3.png)

### <a name="creating-data-model-classes-with-linq-to-sql"></a>Vytváření tříd datového modelu pomocí LINQ to SQL

LINQ to SQL nám umožňuje rychle vytvořit třídy datového modelu z existujícího schématu databáze. Provedete to tak, že otevřete databázi NerdDinner v Průzkumník serveru a vyberete tabulky, pro které chcete modelovat:

![](build-a-model-with-business-rule-validations/_static/image4.png)

Pak můžeme tabulky přetáhnout na plochu návrháře LINQ to SQL. Když to provedeme, LINQ to SQL automaticky vytvoří třídy večeře a RSVP pomocí schématu tabulek (s vlastnostmi třídy, které se mapují na sloupce databázové tabulky):

![](build-a-model-with-business-rule-validations/_static/image5.png)

Ve výchozím nastavení LINQ to SQL Návrhář při vytváření tříd založených na schématu databáze automaticky názvy tabulek a sloupců "pluralizes". Příklad: tabulka "večeře" v našem příkladu výše má za následek třídu "večeře". Tato třída pojmenovává, že naše modely jsou konzistentní s konvencemi názvů .NET a obvykle zjistíte, že je to vhodné pro návrháře, což je pohodlné (obzvláště při přidávání spousty tabulek). Pokud se vám nelíbí název třídy nebo vlastnosti, kterou Návrhář generuje, ale můžete ho vždycky přepsat a změnit na libovolný název, který chcete. To můžete provést úpravou názvu entity/vlastnosti v rámci návrháře nebo úpravou prostřednictvím mřížky vlastností.

Ve výchozím nastavení Návrhář LINQ to SQL také kontroluje vztahy primárních klíčů a cizích klíčů v tabulkách a na základě nich automaticky vytvoří výchozí přidružení vztahů mezi různými třídami modelů, které vytvoří. Když jsme například přetáhli tabulky večeře a RSVP do návrháře LINQ to SQL a přidružení vztahů 1:1 mezi tyto dvě byla odvozená od faktu, že tabulka s protokolem RSVP obsahovala cizí klíč v tabulce večeře (Toto je označeno šipkou v Návrhář):

![](build-a-model-with-business-rule-validations/_static/image6.png)

Výše uvedené přidružení způsobí, LINQ to SQL přidat do třídy RSVP vlastnost "večeře", kterou můžou vývojáři použít pro přístup k večeři přidruženému k dané službě RSVP. Také způsobí, že třída večeře bude mít vlastnost kolekce "RSVPs", která umožňuje vývojářům načíst a aktualizovat objekty protokolu RSVP spojené s určitou večeři.

Níže můžete vidět příklad technologie IntelliSense v sadě Visual Studio, když vytvoříme nový objekt protokolu RSVP a přidáte ho do kolekce RSVPs pro večeři. Všimněte si, jak LINQ to SQL do objektu večeře automaticky přidat kolekci "RSVPs":

![](build-a-model-with-business-rule-validations/_static/image7.png)

Přidáním objektu RSVP do kolekce RSVP pro večeři oznamujeme LINQ to SQL k přidružení vztahu cizího klíče mezi večeři a řádkem RSVP v naší databázi:

![](build-a-model-with-business-rule-validations/_static/image8.png)

Pokud si nejste spokojeni s tím, jak má Návrhář modelovat nebo pojmenovat přidružení tabulky, můžete ho přepsat. Stačí kliknout na šipku přidružení v návrháři a přistupovat k jejím vlastnostem přes mřížku vlastností a přejmenovat, odstranit nebo upravit. U naší aplikace NerdDinner se ale u tříd datového modelu, které vytváříme, dobře hodí výchozí pravidla přidružení, ale můžeme použít jenom výchozí chování.

### <a name="nerddinnerdatacontext-class"></a>NerdDinnerDataContext Class

Visual Studio automaticky vytvoří třídy .NET, které reprezentují modely a databázové vztahy definované pomocí návrháře LINQ to SQL. Třída LINQ to SQL DataContext je vygenerována také pro každý soubor návrháře LINQ to SQL přidaný do řešení. Vzhledem k tomu, že jsme jmenovali naši LINQ to SQL položku třídy "NerdDinner", vytvoří se třída DataContext s názvem "NerdDinnerDataContext". Tato třída NerdDinnerDataContext je primárním způsobem, jak budeme pracovat s databází.

Naše třída NerdDinnerDataContext zpřístupňuje dvě vlastnosti – "večeře" a "RSVP", které reprezentují dvě tabulky, které v databázi modelují. Můžeme použít C# k zápisu dotazů LINQ na tyto vlastnosti pro dotazování a načtení objektů večeře a RSVP z databáze.

Následující kód ukazuje, jak vytvořit instanci objektu NerdDinnerDataContext a provést dotaz LINQ na něj a získat tak sekvenci večeře, ke kterým dochází v budoucnosti. Visual Studio poskytuje úplnou technologii IntelliSense při psaní dotazu LINQ a objekty, které jsou z něj vráceny, jsou silné a také podporují technologii IntelliSense:

![](build-a-model-with-business-rule-validations/_static/image9.png)

Kromě toho, že nám umožníme dotazovat se na objekty večeře a RSVP, NerdDinnerDataContext také automaticky sleduje veškeré změny, které následně provedeme na večeři a v objektech RSVP, které prostřednictvím něj získáváme. Pomocí této funkce můžeme snadno uložit změny zpět do databáze, aniž byste museli psát explicitní kód aktualizace SQL.

Například kód níže ukazuje, jak použít dotaz LINQ k načtení jednoho objektu večeře z databáze, aktualizaci dvou vlastností večeře a následné změny uložit zpět do databáze:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample1.cs)]

Objekt NerdDinnerDataContext v kódu výše automaticky sleduje změny vlastností provedené u objektu večeře, který z něho načetli. Když se říká metoda "SubmitChanges ()", spustí se odpovídající příkaz SQL "UPDATE" do databáze, aby se aktualizované hodnoty zachovaly zpátky.

### <a name="creating-a-dinnerrepository-class"></a>Vytvoření třídy DinnerRepository

Pro malé aplikace je někdy dobré pracovat s řadiči přímo proti třídě LINQ to SQL DataContext a vkládat dotazy LINQ v rámci řadičů. Jelikož se aplikace dostanou větší, ale tento přístup je nenáročný na údržbu a testování. Může také vést k tomu, že máme duplikovat stejné dotazy LINQ na více místech.

Jedním z přístupů, které umožňují snazší údržbu a testování aplikací, je použití vzoru "úložiště". Třída úložiště pomáhá zapouzdření logiky dotazování a trvalosti dat a abstrakce informace o implementaci trvalosti dat z aplikace. Kromě toho, že použití čističe kódu aplikace, může pomocí vzoru úložiště snadněji měnit implementace úložiště dat v budoucnu a může pomoci při testování částí aplikace bez nutnosti skutečné databáze.

Pro naši aplikaci NerdDinner definujeme třídu DinnerRepository s níže uvedeným podpisem:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample2.cs)]

*Poznámka: později v této kapitole budeme z této třídy extrahovat rozhraní IDinnerRepository a na našem řadiči povolit vkládání závislostí. Začněte tím, že začnete pracovat jednoduchým způsobem a přímo pracujete přímo s třídou DinnerRepository.*

Pokud chcete tuto třídu implementovat, klikněte pravým tlačítkem na naši složku modely a vyberte příkaz nabídky **Přidat novou položku&gt;** . V dialogovém okně Přidat novou položku vyberete šablonu Class (třída) a pojmenujte soubor "DinnerRepository.cs":

![](build-a-model-with-business-rule-validations/_static/image10.png)

Pak můžeme implementovat naši třídu DinnerRepository pomocí následujícího kódu:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample3.cs)]

### <a name="retrieving-updating-inserting-and-deleting-using-the-dinnerrepository-class"></a>Načítání, aktualizace, vkládání a odstraňování pomocí třídy DinnerRepository

Teď, když jsme vytvořili naši třídu DinnerRepository, Podívejme se na několik příkladů kódu, které předvádějí běžné úlohy, které s ní můžeme dělat:

#### <a name="querying-examples"></a>Příklady dotazování

Následující kód načte jednu večeři pomocí hodnoty DinnerID:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample4.cs)]

Následující kód načte všechny nadcházející večeře a cykly přes ně:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample5.cs)]

#### <a name="insert-and-update-examples"></a>Příklady vložení a aktualizace

Následující kód ukazuje přidání dvou nových večeři. Přidání/úpravy do úložiště nejsou potvrzeny do databáze, dokud není pro ni volána metoda Save (). LINQ to SQL automaticky zalomí všechny změny v transakční transakci – takže buď dojde k žádným změnám, nebo žádná z nich, když naše úložiště uloží:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample6.cs)]

Následující kód načte existující objekt večeře a upraví na něm dvě vlastnosti. Změny jsou potvrzeny zpět do databáze při volání metody Save () v našem úložišti:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample7.cs)]

Následující kód načte večeři a pak k němu přidá odpověď. K tomu slouží pomocí kolekce RSVPs na objektu večeře, kterou LINQ to SQL vytvořili pro nás (protože mezi nimi existuje vztah primárního klíče/cizího klíče mezi dvěma v databázi). Tato změna se uloží zpátky do databáze jako nový řádek tabulky protokolu RSVP, když se v úložišti zavolá metoda Save ():

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample8.cs)]

#### <a name="delete-example"></a>Odstranit příklad

Následující kód načte existující objekt večeře a pak ho označí jako odstraněný. Když se v úložišti zavolá metoda Save (), potvrdí se odstranění zpátky do databáze:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample9.cs)]

### <a name="integrating-validation-and-business-rule-logic-with-model-classes"></a>Integrace logiky ověřování a obchodních pravidel s třídami modelu

Integrací logiky ověřování a obchodních pravidel je klíčová součást jakékoli aplikace, která pracuje s daty.

#### <a name="schema-validation"></a>Ověřování schématu

Pokud jsou třídy modelu definovány pomocí návrháře LINQ to SQL, datové typy vlastností v třídách datového modelu odpovídají datovým typům tabulky databáze. Příklad: Pokud sloupec "EventDate" v tabulce večeře je "DateTime", třída datového modelu vytvořená LINQ to SQL bude typu "DateTime" (což je vestavěný datový typ rozhraní .NET). To znamená, že při pokusu o přiřazení celého čísla nebo logické hodnoty z kódu dojde k chybám kompilace a při pokusu o implicitní převod neplatného typu řetězce za běhu se automaticky vyvolá chyba.

LINQ to SQL také automaticky zpracuje uvozovací hodnoty SQL za vás při použití řetězců – což pomáhá chránit před útoky prostřednictvím injektáže SQL při jejich použití.

#### <a name="validation-and-business-rule-logic"></a>Ověřování a logika obchodních pravidel

Ověřování schématu je užitečné v prvním kroku, ale je málo dostatečné. Většina scénářů reálného světa vyžaduje možnost zadat bohatou logiku ověřování, která může zahrnovat více vlastností, spouštět kód a často má na vědomí stav modelu (například: je vytvořen/Updated/Deleted nebo v rámci stavu specifického pro doménu, jako je "archivovaný"). Existuje celá řada různých vzorů a platforem, které lze použít k definování a použití ověřovacích pravidel pro třídy modelů a k dispozici je několik platforem rozhraní .NET, které je možné použít k tomu, aby s ní mohli pomáhat. V aplikacích ASP.NET MVC můžete použít poměrně mnoho z nich.

Pro účely naší aplikace NerdDinner použijeme model poměrně jednoduchého a přímého přesměrování, kde vystavíme vlastnost IsValid a metodu GetRuleViolations () pro náš objekt modelu večeře. Vlastnost IsValid vrátí hodnotu true nebo false v závislosti na tom, zda jsou všechna platná ověřování a obchodní pravidla. Metoda GetRuleViolations () vrátí seznam chyb pravidel.

Pro náš model večeře implementujeme IsValid a GetRuleViolations () přidáním "částečné třídy" do našeho projektu. Částečné třídy lze použít k přidání metod/vlastností/událostí do tříd udržovaných návrhářem VS (jako je například třída večeře vygenerovaná návrhářem LINQ to SQL) a zabránění tomu, aby se nástroj mohl vyhnout v používání našeho kódu. Do našeho projektu můžeme přidat novou částečnou třídu tak, že kliknete pravým tlačítkem na složku \Models a pak vyberete příkaz nabídky Přidat novou položku. Pak můžeme zvolit šablonu Class v dialogovém okně Přidat novou položku a pojmenovat ji Dinner.cs.

![](build-a-model-with-business-rule-validations/_static/image11.png)

Kliknutím na tlačítko Přidat se do projektu přidá soubor Dinner.cs a otevře se v rámci integrovaného vývojového prostředí (IDE). Pak můžeme implementovat základní rozhraní pro vynucování pravidel a ověření pomocí následujícího kódu:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample10.cs)]

Pár poznámek o výše uvedeném kódu:

- Třída večeře je uvozená klíčovým slovem "Partial" – to znamená, že kód obsažený v něm bude kombinován s třídou generovanou/udržovanou návrhářem LINQ to SQL a zkompilován do jedné třídy.
- Třída RuleViolation je pomocná třída, kterou přidáme do projektu, který nám umožní poskytnout další podrobnosti o porušení pravidla.
- Metoda večeře. GetRuleViolations () způsobí vyhodnocení našich ověřovacích a obchodních pravidel (budeme je za chvíli implementovat). Pak vrátí sekvenci RuleViolation objektů, které poskytují další podrobnosti o chybách pravidel.
- Vlastnost večeře. IsValid poskytuje pohodlnou pomocnou vlastnost, která označuje, zda objekt večeře obsahuje všechny aktivní RuleViolations. Může být aktivně kontrolován vývojářem s využitím objektu večeře v čase (a nevyvolá výjimku).
- Částečnou metodou večeře. OnValidate () je připojení, které LINQ to SQL poskytuje, aby bylo možné upozornit na trvalou upozorňování objektu večeře v rámci databáze. Naše implementace OnValidate () výše zajišťuje, že večeře nemá žádné RuleViolations předtím, než se uloží. Pokud je v neplatném stavu, vyvolá výjimku, která způsobí, že LINQ to SQL přeruší transakci.

Tento přístup poskytuje jednoduchou architekturu, kterou můžeme do portálu integrovat ověřování a obchodní pravidla. Nyní přidáme níže uvedená pravidla do naší metody GetRuleViolations ():

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample11.cs)]

C# K vrácení posloupnosti všech RuleViolations používáme funkci yield return. Prvních šest kontrol pravidel výše vynutilo, že vlastnosti řetězce na naší večeři nemůžou být null ani prázdné. Poslední pravidlo je trochu zajímavější a volá pomocnou metodu PhoneValidator. IsValidNumber (), kterou můžeme do projektu přidat a ověřit tak, že formát čísla ContactPhone odpovídá zemi večeře.

Můžeme použít. Podpora regulárních výrazů netto pro implementaci této podpory ověřování pro telefon. Níže je uvedená Jednoduchá implementace PhoneValidator, kterou můžeme přidat do našeho projektu, který nám umožňuje přidat kontroly vzorů regulárního výrazu specifické pro danou zemi:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample12.cs)]

#### <a name="handling-validation-and-business-logic-violations"></a>Zpracování ověřování a porušení obchodní logiky

Teď, když jsme přidali výše uvedený kód pro ověření a obchodní pravidlo, pokaždé, když se pokusíme vytvořit nebo aktualizovat večeři, naše pravidla logiky ověřování se vyhodnotí a vynutila.

Vývojáři mohou napsat kód podobný níže, aby proaktivně určil, zda je objekt večeře platný, a načíst seznam všech porušení v něm, aniž by vyvolali výjimky:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample13.cs)]

Pokud se pokusíme Uložit večeři v neplatném stavu, vyvolá se výjimka při volání metody Save () na DinnerRepository. Důvodem je, že LINQ to SQL automaticky volá částečnou metodu večeře. OnValidate () předtím, než uloží změny v večeři, a přidáme kód do večeři. OnValidate (), který vyvolá výjimku, pokud v večeři existují porušení pravidel. Tuto výjimku můžeme zachytit a znovu aktivně načíst seznam porušení, která se mají opravit:

[!code-csharp[Main](build-a-model-with-business-rule-validations/samples/sample14.cs)]

Vzhledem k tomu, že naše ověřování a obchodní pravidla jsou implementována v rámci naší vrstvy modelu a ne v rámci vrstvy uživatelského rozhraní, budou použita a použita ve všech scénářích v rámci naší aplikace. Později můžeme změnit nebo přidat obchodní pravidla a všechny kódy, které se budou pracovat s našimi objekty večeře, je respektují.

Flexibilita při změně obchodních pravidel na jednom místě, bez toho, aby byly tyto změny probíhají v celé aplikaci a v logice uživatelského rozhraní, je znaménkem dobře zapsané aplikace a výhodou, kterou architektura MVC pomáhá povzbudit.

### <a name="next-step"></a>Další krok

Nyní jsme získali model, který můžeme použít k dotazování i k aktualizaci naší databáze.

Teď přidáme do projektu některé řadiče a zobrazení, které můžeme použít k sestavení prostředí uživatelského rozhraní HTML.

> [!div class="step-by-step"]
> [Předchozí](create-a-database.md)
> [Další](use-controllers-and-views-to-implement-a-listingdetails-ui.md)

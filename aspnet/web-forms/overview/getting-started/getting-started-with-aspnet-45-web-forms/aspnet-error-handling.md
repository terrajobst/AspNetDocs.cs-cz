---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
title: Zpracování chyb ASP.NET | Microsoft Docs
author: Erikre
description: V této sérii kurzů se seznámíte se základy vytváření aplikací webových formulářů ASP.NET pomocí ASP.NET 4,5 a Microsoft Visual Studio Express 2013 pro My...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 423498f7-1a4b-44a1-b342-5f39d0bcf94f
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/aspnet-error-handling
msc.type: authoredcontent
ms.openlocfilehash: f420be369801208fa875d9a60e6e154afbe84aa7
ms.sourcegitcommit: b67ffd5b2c5cff01ec4c8eb12a21f693f2e11887
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/23/2019
ms.locfileid: "69995305"
---
# <a name="aspnet-error-handling"></a>Zpracování chyb v ASP.NET

od [Erik Reitan](https://github.com/Erikre)

[Stáhnout vzorový projekt Wingtip Toys (C#)](http://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) nebo [Stáhnout elektronickou knihu (PDF)](http://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> V této sérii kurzů se naučíte základy vytváření webových formulářů ASP.NET pomocí ASP.NET 4,5 a Microsoft Visual Studio Express 2013 pro web. K dispozici je Visual Studio 2013 [projekt C# se zdrojovým kódem](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) , který se doprovází v této sérii kurzů.

V tomto kurzu upravíte ukázkovou aplikaci Wingtip Toys, která bude zahrnovat zpracování chyb a protokolování chyb. Zpracování chyb umožní aplikaci řádným způsobem zpracovávat chyby a zobrazovat chybové zprávy. Protokolování chyb vám umožní najít a opravit chyby, ke kterým došlo. Tento kurz sestaví na předchozím kurzu "směrování adresy URL" a je součástí série kurzů Wingtip Toys.

## <a name="what-youll-learn"></a>Co se naučíte:

- Jak přidat globální zpracování chyb do konfigurace aplikace.
- Postup přidání zpracování chyb na úrovni aplikace, stránky a kódu.
- Jak protokolovat chyby pro pozdější kontrolu.
- Jak zobrazit chybové zprávy, které neohrožují zabezpečení.
- Jak implementovat protokolování chyb modulů a obslužných rutin chyb (knihovny ELMAH) protokolování chyb

## <a name="overview"></a>Přehled

ASP.NET aplikace musí být schopné zpracovávat chyby, ke kterým dochází během provádění konzistentním způsobem. ASP.NET používá modul CLR (Common Language Runtime), který poskytuje způsob upozorňování aplikací s chybami jednotným způsobem. Dojde-li k chybě, je vyvolána výjimka. Výjimka je jakákoli chyba, podmínka nebo neočekávané chování, ke kterému dojde v aplikaci.

V .NET Framework výjimka je objekt, který dědí z `System.Exception` třídy. Výjimka je vyvolána z oblasti kódu, kde došlo k problému. Výjimka je předána zásobníku volání do místa, kde aplikace poskytuje kód pro zpracování výjimky. Pokud aplikace výjimku nezpracovává, prohlížeč je nucen zobrazit podrobnosti o chybě.

Osvědčeným postupem je zpracovávat chyby v na úrovni kódu v `Try` / `Catch` / `Finally` blocích v rámci vašeho kódu. Zkuste umístit tyto bloky tak, aby mohl uživatel opravit problémy v kontextu, ve kterém k nim došlo. Pokud jsou bloky zpracování chyb příliš daleko od místa, kde došlo k chybě, bude obtížnější poskytnout uživatelům informace, které potřebují k vyřešení problému.

### <a name="exception-class"></a>Exception – třída

Třída Exception je základní třída, ze které dědí výjimky. Většina objektů Exception je instance některé odvozené třídy třídy Exception, jako je `SystemException` třída `IndexOutOfRangeException` , třída nebo `ArgumentNullException` třída. Třída Exception má vlastnosti, jako je `StackTrace` vlastnost `InnerException` , vlastnost a `Message` vlastnost, které poskytují konkrétní informace o chybě, ke které došlo.

### <a name="exception-inheritance-hierarchy"></a>Hierarchie dědičnosti výjimek

Modul runtime má základní sadu výjimek odvozenou od `SystemException` třídy, kterou modul runtime vyvolá při zjištění výjimky. Většina tříd, které dědí z třídy Exception, jako je `IndexOutOfRangeException` třída `ArgumentNullException` a třída, neimplementují další členy. Proto nejdůležitější informace pro výjimku lze nalézt v hierarchii výjimek, název výjimky a informace obsažené v výjimce.

### <a name="exception-handling-hierarchy"></a>Hierarchie zpracování výjimek

V aplikaci webových formulářů ASP.NET lze výjimky zpracovat v závislosti na konkrétní hierarchii zpracování. Výjimku lze zpracovat na následujících úrovních:

- Úroveň aplikace
- Úroveň stránky
- Úroveň kódu

Pokud aplikace zpracovává výjimky, další informace o výjimce, která je zděděna z třídy výjimky, lze často načíst a zobrazit uživateli. Kromě aplikace, stránky a úrovně kódu můžete také zpracovávat výjimky na úrovni modulu HTTP a pomocí vlastní obslužné rutiny služby IIS.

### <a name="application-level-error-handling"></a>Zpracování chyb na úrovni aplikace

Můžete zpracovat výchozí chyby na úrovni aplikace buď úpravou konfigurace aplikace, nebo přidáním `Application_Error` obslužné rutiny do souboru *Global. asax* vaší aplikace.

Můžete zpracovat výchozí chyby a chyby protokolu HTTP přidáním `customErrors` oddílu do souboru *Web. config* . V `customErrors` části můžete zadat výchozí stránku, na kterou budou uživatelé přesměrováni, když dojde k chybě. Umožňuje taky zadat jednotlivé stránky pro konkrétní chyby stavového kódu.

[!code-xml[Main](aspnet-error-handling/samples/sample1.xml?highlight=3-5)]

Když ale použijete konfiguraci k přesměrování uživatele na jinou stránku, nezískáte podrobnosti o chybě, ke které došlo.

Můžete však zachytit chyby, ke kterým dochází kdekoli v aplikaci, přidáním kódu do `Application_Error` obslužné rutiny v souboru *Global. asax* .

[!code-csharp[Main](aspnet-error-handling/samples/sample2.cs)]

### <a name="page-level-error-event-handling"></a>Zpracování událostí chyb na úrovni stránky

Obslužná rutina na úrovni stránky vrátí uživatele na stránku, kde došlo k chybě, ale vzhledem k tomu, že instance ovládacích prvků nejsou zachovány, již nebudou na stránce žádné. Chcete-li poskytnout podrobnosti o chybě uživateli aplikace, je nutné přímo zapsat podrobnosti o chybě na stránku.

Obvykle byste použili obslužnou rutinu chyb na úrovni stránky k protokolování neošetřených chyb nebo k převzetí uživatele na stránku, která může zobrazit užitečné informace.

Tento příklad kódu ukazuje obslužnou rutinu pro událost Error na webové stránce ASP.NET. Tato obslužná rutina zachytí všechny výjimky, které ještě `try` nejsou zpracovávány / `catch` v blocích na stránce.

[!code-csharp[Main](aspnet-error-handling/samples/sample3.cs)]

Po zpracování chyby je nutné ji vymazat voláním `ClearError` metody objektu serveru (`HttpServerUtility` třídy), jinak se zobrazí chyba, která byla dříve nastala.

### <a name="code-level-error-handling"></a>Zpracování chyb na úrovni kódu

Příkaz try-catch se skládá z bloku try následovaného jednou nebo více klauzulemi catch, které určují obslužné rutiny pro různé výjimky. Je-li vyvolána výjimka, modul CLR (Common Language Runtime) vyhledá příkaz catch, který zpracovává tuto výjimku. Pokud aktuálně spuštěná metoda neobsahuje blok catch, modul CLR vyhledá metodu, která volala aktuální metodu, a tak dále, do zásobníku volání. Pokud není nalezen žádný blok catch, modul CLR zobrazí uživateli neošetřenou zprávu o výjimce a zastaví provádění programu.

Následující příklad kódu ukazuje běžný `try` způsob použití / `catch` / prozpracováníchyb`finally` .

[!code-csharp[Main](aspnet-error-handling/samples/sample4.cs)]

Ve výše uvedeném kódu blok try obsahuje kód, který je nutné chránit před možnou výjimkou. Blok je proveden, dokud není vyvolána výjimka nebo je blok úspěšně dokončen. Pokud dojde k `IOException`výjimce nebo výjimce, je spuštění přeneseno na jinou stránku. `FileNotFoundException` Pak se spustí kód obsažený v bloku finally, bez ohledu na to, jestli došlo k chybě nebo ne.

## <a name="adding-error-logging-support"></a>Přidání podpory protokolování chyb

Před přidáním zpracování chyb do ukázkové aplikace Wingtip Toys přidáte podporu protokolování chyb přidáním `ExceptionUtility` třídy do složky *logiky* . Tím dojde k tomu, že se pokaždé, když aplikace zpracovává chybu, do souboru protokolu chyb přidá podrobnosti o chybě.

1. Klikněte pravým tlačítkem na složku *Logic* a pak vyberte **Přidat**  - &gt; **novou položku**.   
   **Přidat novou položku** se zobrazí dialogové okno.
2. Na levé straně vyberte skupinu šablon  - **vizuálního C#**  &gt; **kódu** . Pak vyberte **Třída**v prostředním seznamu a pojmenujte ji **ExceptionUtility.cs**.
3. Zvolte **přidat**. Zobrazí se nový soubor třídy.
4. Existující kód nahraďte následujícím kódem:  

    [!code-csharp[Main](aspnet-error-handling/samples/sample5.cs)]

Pokud dojde k výjimce, lze výjimku zapsat do souboru protokolu výjimky voláním `LogException` metody. Tato metoda přijímá dva parametry, objekt výjimky a řetězec obsahující podrobnosti o zdroji výjimky. Protokol výjimek se zapisuje do souboru *. txt* ve složce *data aplikací\_* .

### <a name="adding-an-error-page"></a>Přidání chybové stránky

V ukázkové aplikaci Wingtip Toys se k zobrazení chyb použije jedna stránka. Chybová stránka je navržena tak, aby zobrazovala zabezpečenou chybovou zprávu uživatelům webu. Pokud je však uživatel vývojářem, který vytváří požadavek HTTP, který je obsluhován místně na počítači, ve kterém je kód umístěn, budou na chybové stránce zobrazeny další podrobnosti o chybě.

1. V **Průzkumník řešení** klikněte pravým tlačítkem myši na název projektu (**Wingtip Toys**) a vyberte možnost **Přidat**  - &gt; **novou položku**.   
   **Přidat novou položku** se zobrazí dialogové okno.
2. Na levé straně vyberte skupinu  - **Visual C#**  &gt; **Web** Templates. V prostředním seznamu vyberte **webový formulář s hlavní stránkou**a pojmenujte ho **ErrorPage. aspx**.
3. Klikněte na **Přidat**.
4. Vyberte soubor *Web. Master* jako stránku předlohy a pak klikněte na **tlačítko OK**.
5. Existující značku nahraďte následujícím kódem:   

    [!code-aspx[Main](aspnet-error-handling/samples/sample6.aspx)]
6. Nahraďte existující kód kódu na pozadí (*ErrorPage.aspx.cs*) tak, aby se zobrazil jako následující:   

    [!code-csharp[Main](aspnet-error-handling/samples/sample7.cs)]

Po zobrazení `Page_Load` chybové stránky se spustí obslužná rutina události. `Page_Load` V obslužné rutině je určeno umístění, kde byla chyba poprvé zpracována. Poslední chyba, ke které došlo, je určena voláním `GetLastError` metody objektu Server. Pokud již výjimka neexistuje, je vytvořena obecná výjimka. Pokud byl požadavek HTTP proveden místně, zobrazí se všechny podrobnosti o chybě. V takovém případě se tyto podrobnosti o chybě zobrazí jenom na místním počítači, na kterém je spuštěná webová aplikace. Po zobrazení informací o chybě se do souboru protokolu přidá chyba a na serveru se vymaže chyba.

### <a name="displaying-unhandled-error-messages-for-the-application"></a>Zobrazení neošetřených chybových zpráv pro aplikaci

Přidáním `customErrors` oddílu do souboru *Web. config* můžete rychle zpracovávat jednoduché chyby, ke kterým dochází v celé aplikaci. Můžete také určit, jak se mají zpracovávat chyby na základě jejich hodnoty stavového kódu, například 404-soubor nebyl nalezen.

#### <a name="update-the-configuration"></a>Aktualizace konfigurace

Aktualizujte konfiguraci přidáním `customErrors` oddílu do souboru *Web. config* .

1. V **Průzkumník řešení**vyhledejte a otevřete soubor *Web. config* v kořenovém adresáři ukázkové aplikace Wingtip Toys.
2. Přidejte oddíl do souboru *Web. config* v rámci `<system.web>` uzlu následujícím způsobem: `customErrors`   

    [!code-xml[Main](aspnet-error-handling/samples/sample8.xml?highlight=3-5)]
3. Uložte soubor *Web. config* .

`customErrors` Oddíl určuje režim, který je nastaven na zapnuto. Určuje `defaultRedirect`také, který instruuje aplikaci, na kterou stránka přejde, když dojde k chybě. Kromě toho jste přidali konkrétní chybový prvek, který určuje, jak se má zpracovat Chyba 404, když se stránka nenajde. Později v tomto kurzu přidáte další zpracování chyb, které bude zachytit podrobnosti o chybě na úrovni aplikace.

#### <a name="running-the-application"></a>Spuštění aplikace

Nyní můžete spustit aplikaci a zobrazit aktualizované trasy.

1. Stisknutím klávesy **F5** spusťte ukázkovou aplikaci Wingtip Toys.  
 Prohlížeč otevře a zobrazí stránku *Default. aspx* .
2. Do prohlížeče zadejte následující adresu URL (nezapomeňte použít číslo portu) :  
    `https://localhost:44300/NoPage.aspx`
3. Zkontrolujte *ErrorPage. aspx* zobrazený v prohlížeči. 

    ![Zpracování chyb ASP.NET – Chyba nenalezené stránky](aspnet-error-handling/_static/image1.png)

Pokud si vyžádáte stránku *. aspx* , která neexistuje, zobrazí se v chybové stránce jednoduchá chybová zpráva a podrobné informace o chybě, pokud jsou k dispozici další podrobnosti. Pokud ale uživatel požadoval neexistující stránku ze vzdáleného umístění, zobrazí se chybová zpráva jenom červeně.

### <a name="including-an-exception-for-testing-purposes"></a>Zahrnutí výjimky pro účely testování

Chcete-li ověřit, jak bude aplikace fungovat, když dojde k chybě, můžete v ASP.NET úmyslně vytvořit chybové stavy. V ukázkové aplikaci Wingtip Toys vyvoláte výjimku testu, když se výchozí stránka načte, aby se zobrazila informace o tom, co se stane.

1. Otevřete kód na pozadí stránky *Default. aspx* v aplikaci Visual Studio.   
   Zobrazí se stránka *Default.aspx.cs* s kódem na pozadí.
2. `Page_Load` V obslužné rutině přidejte kód tak, aby se obslužná rutina zobrazila takto:   

    [!code-csharp[Main](aspnet-error-handling/samples/sample9.cs?highlight=3-4)]

Je možné vytvořit různé různé typy výjimek. Ve výše uvedeném kódu vytváříte `InvalidOperationException` , když je načtena stránka *Default. aspx* .

#### <a name="running-the-application"></a>Spuštění aplikace

Můžete spustit aplikaci, abyste viděli, jak aplikace zpracovává výjimku.

1. Stisknutím **kombinace kláves CTRL + F5** spusťte ukázkovou aplikaci Wingtip Toys.  
 Aplikace vyvolá chybu InvalidOperationException. 

    > [!NOTE] 
    > 
    > Pokud chcete zobrazit zdroj chyby v aplikaci Visual Studio, je nutné stisknout **kombinaci kláves CTRL + F5** a zobrazit stránku bez přerušení kódu.
2. Zkontrolujte *ErrorPage. aspx* zobrazený v prohlížeči. 

    ![Zpracování chyb ASP.NET – chybová stránka](aspnet-error-handling/_static/image2.png)

Jak vidíte v podrobnostech o chybě, výjimka byla zachycena `customError` oddílem v souboru *Web. config* .

### <a name="adding-application-level-error-handling"></a>Přidání zpracování chyb na úrovni aplikace

Místo zachycení výjimky pomocí `customErrors` oddílu v souboru *Web. config* , kde získáte malé informace o výjimce, můžete zachytit chybu na úrovni aplikace a načíst podrobnosti o chybě.

1. V **Průzkumník řešení**vyhledejte a otevřete soubor *Global.asax.cs* .
2. Přidejte obslužnou rutinu **chyb aplikace\_** tak, aby se zobrazila takto:   

    [!code-csharp[Main](aspnet-error-handling/samples/sample10.cs)]

Pokud v aplikaci dojde k chybě, `Application_Error` je volána obslužná rutina. V této obslužné rutině je poslední výjimka načtena a přezkoumána. Pokud výjimka nebyla ošetřena a výjimka obsahuje podrobnosti vnitřní výjimky (tj `InnerException` . není null), aplikace přenese spuštění na chybovou stránku, kde se zobrazují podrobnosti o výjimce.

#### <a name="running-the-application"></a>Spuštění aplikace

Můžete spustit aplikaci, chcete-li zobrazit další podrobnosti o chybě, které jsou k dispozici, pomocí zpracování výjimky na úrovni aplikace.

1. Stisknutím **kombinace kláves CTRL + F5** spusťte ukázkovou aplikaci Wingtip Toys.  
 Aplikace vyvolá `InvalidOperationException` .
2. Zkontrolujte *ErrorPage. aspx* zobrazený v prohlížeči. 

    ![Zpracování chyb ASP.NET – Chyba na úrovni aplikace](aspnet-error-handling/_static/image3.png)

### <a name="adding-page-level-error-handling"></a>Přidání zpracování chyb na úrovni stránky

Zpracování chyb na úrovni stránky můžete přidat na stránku buď pomocí přidání `ErrorPage` atributu `@Page` do direktivy stránky `Page_Error` , nebo přidáním obslužné rutiny události do kódu na pozadí stránky. V této části přidáte `Page_Error` obslužnou rutinu události, která převede provádění na stránku *ErrorPage. aspx* .

1. V **Průzkumník řešení**vyhledejte a otevřete soubor *Default.aspx.cs* .
2. `Page_Error` Přidejte obslužnou rutinu, aby se kód na pozadí zobrazil následovně:   

    [!code-csharp[Main](aspnet-error-handling/samples/sample11.cs?highlight=18-30)]

Pokud na stránce dojde k chybě, `Page_Error` je volána obslužná rutina události. V této obslužné rutině je poslední výjimka načtena a přezkoumána. Dojde-li k chybě `Page_Error` , obslužná rutina události převede provádění na chybovou stránku, kde se zobrazí podrobnosti o výjimce. `InvalidOperationException`

#### <a name="running-the-application"></a>Spuštění aplikace

Nyní můžete spustit aplikaci a zobrazit aktualizované trasy.

1. Stisknutím **kombinace kláves CTRL + F5** spusťte ukázkovou aplikaci Wingtip Toys.  
 Aplikace vyvolá `InvalidOperationException` .
2. Zkontrolujte *ErrorPage. aspx* zobrazený v prohlížeči. 

    ![Zpracování chyb ASP.NET – Chyba na úrovni stránky](aspnet-error-handling/_static/image4.png)
3. Zavřete okno prohlížeče.

### <a name="removing-the-exception-used-for-testing"></a>Odebrání výjimky používané pro testování

Aby mohla ukázková aplikace Wingtip Toys fungovat bez vyvolání výjimky, kterou jste přidali dříve v tomto kurzu, odeberte výjimku.

1. Otevřete kód na pozadí stránky *Default. aspx* .
2. `Page_Load` V obslužné rutině odstraňte kód, který vyvolá výjimku, aby se obslužná rutina zobrazila takto:   

    [!code-csharp[Main](aspnet-error-handling/samples/sample12.cs)]

### <a name="adding-code-level-error-logging"></a>Přidání protokolování chyb na úrovni kódu

Jak bylo zmíněno dříve v tomto kurzu, můžete přidat příkazy try/catch k pokusu o spuštění části kódu a zpracování první chyby, ke které dojde. V tomto příkladu zapíšete podrobnosti o chybě pouze do souboru protokolu chyb, aby bylo možné chybu později zkontrolovat.

1. V **Průzkumník řešení**ve složce *Logic* najděte a otevřete soubor *PayPalFunctions.cs* .
2. Aktualizujte `HttpCall` metodu tak, že se kód zobrazí takto:   

    [!code-csharp[Main](aspnet-error-handling/samples/sample13.cs?highlight=20,22-23)]

Výše uvedený kód volá `LogException` metodu, která je obsažena `ExceptionUtility` ve třídě. Do složky logiky jste přidali soubor třídy *ExceptionUtility.cs* dříve v tomto kurzu. `LogException` Metoda přebírá dva parametry. První parametr je objekt výjimky. Druhý parametr je řetězec, který slouží k rozpoznání zdroje chyby.

### <a name="inspecting-the-error-logging-information"></a>Kontrola informací o protokolování chyb

Jak už bylo zmíněno dříve, můžete pomocí protokolu chyb určit, které chyby ve vaší aplikaci byste měli nejdřív opravit. Samozřejmě se budou zaznamenávat jenom chyby, které byly zachyceny a zapsány do protokolu chyb.

1. V **Průzkumník řešení**vyhledejte a otevřete soubor *. txt* ve složce *\_data aplikací* .   
 V horní části **Průzkumník řešení** možná budete muset vybrat možnost**Zobrazit všechny soubory**nebo**aktualizovat**, aby se zobrazil soubor s chybou *. txt* .
2. Zkontrolujte protokol chyb zobrazený v aplikaci Visual Studio: 

    ![Zpracování chyb ASP.NET – Chyba protokolu chyb. txt](aspnet-error-handling/_static/image5.png)

### <a name="safe-error-messages"></a>Bezpečné chybové zprávy

Je **důležité si uvědomit** , že když vaše aplikace zobrazuje chybové zprávy, neměli byste si dát informace o tom, že uživatel se zlými úmysly může být užitečný při útoku vaší aplikace. Například pokud se vaše aplikace neúspěšně pokusí o zápis do databáze, neměla by se zobrazit chybová zpráva, která obsahuje uživatelské jméno, které používá. Z tohoto důvodu se uživateli zobrazí obecná chybová zpráva červeně. Všechny podrobnosti o všech dalších chybách se zobrazí pouze vývojářům na místním počítači.

## <a name="using-elmah"></a>Použití knihovny ELMAH

KNIHOVNY ELMAH (moduly a obslužné rutiny protokolu chyb) je Protokolovací zařízení, které se připojuje k vaší aplikaci ASP.NET jako balíček NuGet. KNIHOVNY ELMAH poskytuje následující možnosti:

- Protokolování neošetřených výjimek.
- Webová stránka pro zobrazení celého protokolu překódování neošetřených výjimek.
- Webová stránka pro zobrazení úplných podrobností o všech protokolovaných výjimkách.
- E-mailové oznámení o každé chybě v době, kdy k ní dojde.
- Informační kanál RSS posledních 15 chyb z protokolu.

Než budete moct pracovat s knihovny ELMAH, musíte si ho nainstalovat. To je snadné pomocí instalačního programu balíčku *NuGet* . Jak bylo zmíněno dříve v této sérii kurzů, NuGet je rozšíření sady Visual Studio, které usnadňuje instalaci a aktualizaci Open Source knihoven a nástrojů v sadě Visual Studio.

1. V sadě Visual Studio vyberte v nabídce **nástroje** možnost **správce** > balíčků NuGet**Spravovat balíčky NuGet pro řešení**. 

    ![Zpracování chyb ASP.NET – Správa balíčků NuGet pro řešení](aspnet-error-handling/_static/image6.png)
2. V sadě Visual Studio se zobrazí dialogové okno **Spravovat balíčky NuGet** .
3. V dialogovém okně **Spravovat balíčky NuGet** rozbalte na levé straně **online** a pak vyberte **NuGet.org**. Pak najděte a nainstalujte balíček **knihovny elmah** ze seznamu dostupných balíčků online. 

    ![Zpracování chyb ASP.NET – balíček NuGet ELMA](aspnet-error-handling/_static/image7.png)
4. K stažení balíčku budete potřebovat připojení k Internetu.
5. V dialogovém okně **Vybrat projekty** se ujistěte, že je vybraná možnost **WingtipToys** a pak klikněte na **OK**. 

    ![Zpracování chyb ASP.NET – dialogové okno vybrat projekty](aspnet-error-handling/_static/image8.png)
6. V případě potřeby klikněte na **Zavřít** v dialogovém okně **Spravovat balíčky NuGet** .
7. Pokud aplikace Visual Studio požaduje, abyste znovu znovu otevřeli otevřené soubory, vyberte**Ano všem**.
8. Balíček knihovny ELMAH do souboru *Web. config* v kořenovém adresáři vašeho projektu přidá záznamy pro sebe samé. Pokud se v aplikaci Visual Studio zobrazí dotaz, zda chcete znovu načíst změněný soubor *Web. config* , klikněte na tlačítko **Ano**.

KNIHOVNY ELMAH je teď připravený k uložení všech neošetřených chyb, ke kterým došlo.

### <a name="viewing-the-elmah-log"></a>Zobrazení protokolu knihovny ELMAH

Zobrazení protokolu knihovny ELMAH je jednoduché, ale nejprve vytvoříte neošetřenou výjimku, která bude zaznamenána v protokolu knihovny ELMAH.

1. Stisknutím **kombinace kláves CTRL + F5** spusťte ukázkovou aplikaci Wingtip Toys.
2. Pokud chcete do protokolu knihovny ELMAH zapsat neošetřenou výjimku, přejděte v prohlížeči na následující adresu URL (pomocí čísla portu):  
    `https://localhost:44300/NoPage.aspx`Zobrazí se chybová stránka.
3. Pokud chcete zobrazit protokol knihovny ELMAH, přejděte v prohlížeči na následující adresu URL (pomocí čísla portu):  
    `https://localhost:44300/elmah.axd`

    ![Zpracování chyb ASP.NET – protokol chyb knihovny ELMAH](aspnet-error-handling/_static/image9.png)

## <a name="summary"></a>Souhrn

V tomto kurzu jste se dozvěděli o zpracování chyb na úrovni aplikace, na úrovni stránky a na úrovni kódu. Také jste se naučili, jak protokolovat ošetřené a neošetřené chyby pro pozdější kontrolu. Přidali jste nástroj knihovny ELMAH, který poskytuje protokolování výjimek a oznámení do vaší aplikace pomocí NuGet. Dále jste se dozvěděli o významu bezpečných chybových zpráv.

## <a name="tutorial-series-conclusion"></a>Závěr série kurzů

Děkujeme za následující. Doufám, že tato sada kurzů pomáhá lépe seznámit s ASP.NET webovými formuláři. Pokud potřebujete další informace o funkcích webových formulářů dostupných v ASP.NET 4,5 a Visual Studio 2013, přečtěte si téma [ASP.NET and Web Tools pro Visual Studio 2013 poznámky k verzi](../../../../visual-studio/overview/2013/release-notes.md). Nezapomeňte si také prohlédnout kurz uvedený v části **Další kroky** a defintely si vyzkoušet [bezplatnou zkušební verzi Azure](https://azure.microsoft.com/pricing/free-trial/).

![Děkuji – Erik](aspnet-error-handling/_static/image10.png)  

## <a name="next-steps"></a>Další kroky

Další informace o nasazení webové aplikace do Microsoft Azure najdete v tématu [nasazení zabezpečené aplikace webových formulářů ASP.NET pomocí členství, protokolu OAuth a SQL Database na web Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/).

## <a name="free-trial"></a>Bezplatná zkušební verze

[Microsoft Azure – bezplatná zkušební verze](https://azure.microsoft.com/pricing/free-trial/)  
 Publikování webu do Microsoft Azure vám ušetří čas, údržbu a náklady. Je to rychlý proces nasazení webové aplikace do Azure. Pokud potřebujete zachovat a monitorovat svou webovou aplikaci, Azure nabízí celou řadu nástrojů a služeb. Spravujte data, provoz, identitu, zálohování, zasílání zpráv, média a výkon v Azure. A to vše je k dispozici v rámci velmi nákladově efektivního přístupu.

## <a name="additional-resources"></a>Další prostředky

[Protokolování podrobností o chybách pomocí monitorování stavu ASP.NET](../../older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs.md)   
[ELMAH](https://code.google.com/p/elmah/)

## <a name="acknowledgements"></a>Potvrzení

Chci nás zasílat na následující lidi, kteří významně přispěli k obsahu této série kurzů:

- [Alberto Poblacion, MVP &amp; MCT, Španělsko](https://mvp.microsoft.com/mvp/Alberto%20Poblacion%20Bolano-36772)
- [Alex Thissen, Nizozemsko](http://blog.alexthissen.nl/) (Twitter: [@alexthissen](http://twitter.com/alexthissen))
- [Andre Tournier, USA](http://andret503.wordpress.com/)
- Apurva Joshi, Microsoft
- [Bojan Vrhovnik, Slovinsko](http://twitter.com/bvrhovnik)
- [Bruno Sonnino, Brazílie](http://msmvps.com/blogs/bsonnino) (Twitter: [@bsonnino](http://twitter.com/bsonnino))
- [Carlos dos Santos, Brazílie](http://www.carloscds.net/)
- [Dave Campbell, USA](http://www.wynapse.com/) (Twitter: [@windowsdevnews](http://twitter.com/windowsdevnews))
- [Jan Galloway, Microsoft](https://weblogs.asp.net/jgalloway) (Twitter: [@jongalloway](http://twitter.com/jongalloway))
- [Michael otrub, USA](http://www.930solutions.com/) (Twitter: [@mrsharps](http://twitter.com/mrsharps))
- Mike Pope
- [Prodejci Mitchel, USA](http://www.mitchelsellers.com/) (Twitter: [@MitchelSellers](http://twitter.com/MitchelSellers))
- [Paul Cociuba, Microsoft](http://linqto.me/Links/pcociuba)
- [Paulo Morgado, Portugal](http://paulomorgado.net/)
- [Pranav Rastogi, Microsoft](https://blogs.msdn.com/b/pranav_rastogi)
- [Tim Ammann, Microsoft](https://blogs.iis.net/timamm/default.aspx)
- [Dykstra, Microsoft](https://blogs.msdn.com/aspnetue)

## <a name="community-contributions"></a>Komunitní příspěvky

- Graham Mendick ([@grahammendick](http://twitter.com/grahammendick))  
  Ukázka kódu souvisejícího se službou Visual Studio 2012 na webu MSDN: [Navigace – Wingtip Toys](https://code.msdn.microsoft.com/Navigation-Wingtip-Toys-5f0daba2)
- James Chaney ([jchaney@agvance.net](mailto:jchaney@agvance.net))  
  Ukázka kódu souvisejícího se službou Visual Studio 2012 na webu MSDN: [Série kurzů pro webové formuláře v ASP.NET 4,5 v Visual Basic](https://code.msdn.microsoft.com/ASPNET-45-Web-Forms-f37f0f63)
- Andrielle Azevedo – Microsoft Technical publikum Přispěvatel (Twitter: @driazevedo)  
  Překlad sady Visual Studio 2012: [Iniciando com ASP.NET Web Forms 4,5-parte 1-Introdução e Visão Geral](https://andrielleazevedo.wordpress.com/2013/01/24/iniciando-com-asp-net-web-forms-4-5-introducao-e-visao-geral/)

> [!div class="step-by-step"]
> [Předchozí](url-routing.md)

---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
title: ASP.NET MVC 4 – základy | Microsoft Docs
author: rick-anderson
description: Tato praktická cvičení vychází z hudebního úložiště MVC (Model View Controller), aplikace kurz, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MV...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: b7dba543-73c3-4534-a9a0-ba70fa2c6a8a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-fundamentals
msc.type: authoredcontent
ms.openlocfilehash: 95e9b9f55b2080c0ed01dc34e3a32f9f1c905644
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598817"
---
# <a name="aspnet-mvc-4-fundamentals"></a>ASP.NET MVC 4 – základy

podle [týmu webového Campy](https://twitter.com/webcamps)

[Stáhnout web Campy Training Kit](https://aka.ms/webcamps-training-kit)

Tato praktická cvičení vychází z hudebního úložiště MVC (Model View Controller), aplikace kurz, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio. V průběhu tohoto testovacího prostředí se naučíte jednoduchost, ale budete tyto technologie používat dohromady. Začnete s jednoduchou aplikací a budete ji sestavovat, dokud nebudete mít plně funkční webovou aplikaci ASP.NET MVC 4.

Toto testovací prostředí spolupracuje s ASP.NET MVC 4.

Pokud chcete prozkoumat verzi ASP.NET MVC 3 v aplikaci kurz, najdete ji v [MVC – hudba-Store](https://github.com/evilDave/MVC-Music-Store).

Tato praktická cvičení předpokládá, že má vývojář zkušenosti s technologiemi webového vývoje, jako je HTML a JavaScript.

> [!NOTE]
> Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici v [verzích Microsoft-Web/WebCampTrainingKit](https://aka.ms/webcamps-training-kit). Projekt, který je specifický pro toto testovací prostředí, je k dispozici na [ASP.NET MVC 4 – základy](https://github.com/Microsoft-Web/HOL-MVC4Fundamentals).

<a id="The_Music_Store_application"></a>
### <a name="the-music-store-application"></a>Aplikace pro hudební úložiště

Webová aplikace pro hudební úložiště, která bude sestavená v rámci tohoto testovacího prostředí, zahrnuje tři hlavní části: nákupy, rezervace a správa. Návštěvníci budou moci procházet alba podle žánru, přidávat alba do svého košíku, kontrolovat jejich výběr a nakonec pokračovat v rezervaci a dokončit objednávku. Kromě toho Správci úložiště budou moct spravovat dostupná alba i hlavní vlastnosti.

![Obrazovky pro hudební úložiště](aspnet-mvc-4-fundamentals/_static/image1.png "Obrazovky pro hudební úložiště")

*Obrazovky pro hudební úložiště*

<a id="ASPNET_MVC_4_Essentials"></a>
### <a name="aspnet-mvc-4-essentials"></a>ASP.NET MVC 4 Essentials

Aplikace pro hudební úložiště bude sestavena pomocí **kontroleru zobrazení modelu (MVC)** , což je model architektury, který odděluje aplikaci do tří hlavních součástí:

- **Modely**: objekty modelu jsou části aplikace, které implementují logiku domény. Objekty modelu často také načítají a ukládají stav modelu v databázi.
- **Zobrazení:** Zobrazení jsou komponenty, které zobrazují uživatelské rozhraní (UI) aplikace. Toto uživatelské rozhraní je zpravidla vytvořeno na základě dat modelu. Příkladem může být zobrazení pro úpravy alb, která zobrazují textová pole a rozevírací seznam na základě aktuálního stavu objektu alba.
- **Řadiče:** Řadiče jsou komponenty, které zpracovávají interakci uživatele, manipulují s modelem a nakonec vyberou zobrazení pro vykreslení uživatelského rozhraní. V aplikaci MVC zobrazení pouze zobrazuje informace, zatímco kontroler zpracovává vstup uživatele a interakci s uživatelem a reaguje na ně.

Vzor MVC vám pomůže vytvářet aplikace, které oddělují různé aspekty aplikace (vstupní logiku, obchodní logika a logika uživatelského rozhraní), a současně poskytuje volné spojení mezi těmito prvky. Toto oddělení vám pomůže se správou složitosti při sestavování aplikace, protože umožňuje soustředit se na jeden aspekt implementace v jednom okamžiku. Kromě toho vzor MVC usnadňuje testování aplikací a také podporuje používání služby TDD (test-řízeného vývoje) pro vytváření aplikací.

Rozhraní **ASP.NET MVC** nabízí alternativu ke vzorům webových formulářů ASP.NET pro vytváření webových aplikací založených na ASP.NET MVC. Rozhraní **ASP.NET MVC** je odlehčené, vysoce testovatelné prezentační rozhraní, které (stejně jako u webových aplikací) je integrované s existujícími funkcemi ASP.NET, jako jsou stránky předlohy a ověřování založené na členství, takže získáte všechny možnosti základního rozhraní .NET Framework. To je užitečné, pokud jste již obeznámeni s webovými formuláři ASP.NET, protože všechny knihovny, které už používáte, jsou k dispozici také v ASP.NET MVC 4.

Kromě toho volné spojení mezi třemi hlavními komponentami aplikace MVC podporuje také paralelní vývoj. Například jeden vývojář může pracovat na zobrazení, druhý vývojář může pracovat s logikou kontroleru a třetí vývojář se může soustředit na obchodní logiku v modelu.

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>Cíle

V této praktické laboratorní laboratoři se dozvíte, jak:

- Vytvoření aplikace ASP.NET MVC od začátku na základě kurzu aplikace pro hudební úložiště
- Přidání řadičů pro zpracování adres URL na domovské stránce webu a procházení hlavních funkcí
- Přidání zobrazení pro přizpůsobení obsahu zobrazeného spolu s jeho stylem
- Přidání tříd modelu do zahrnutí a správy dat a logiky domény
- Použití vzoru modelu zobrazení k předávání informací z akcí kontroleru do šablon zobrazení
- Prozkoumejte novou šablonu ASP.NET MVC 4 pro internetové aplikace

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Předpoklady

K dokončení tohoto testovacího prostředí musíte mít následující položky:

- [Visual Studio 2012 Express for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) (pokyny k jeho instalaci najdete v [příloze A](#AppendixA) )

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>Nastavení

**Instalace fragmentů kódu**

Pro usnadnění práce je většina kódu, který budete spravovat v tomto testovacím prostředí, k dispozici jako fragmenty kódu sady Visual Studio. Chcete-li nainstalovat fragmenty kódu, spusťte soubor **.\Source\Setup\CodeSnippets.vsi** .

Pokud nejste obeznámeni s fragmentem Visual Studio Code a chcete se dozvědět, jak je používat, můžete odkazovat na přílohu z tohoto dokumentu &quot;[příloze C: použití fragmentů kódu](#AppendixC)&quot;.

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>Cvičení

Tato praktická cvičení se skládají z následujících cvičení:

1. [Cvičení 1: vytvoření projektu webové aplikace MusicStore ASP.NET MVC](#Exercise1)
2. [Cvičení 2: vytvoření kontroleru](#Exercise2)
3. [Cvičení 3: předávání parametrů řadiči](#Exercise3)
4. [Cvičení 4: Vytvoření zobrazení](#Exercise4)
5. [Cvičení 5: vytvoření modelu zobrazení](#Exercise5)
6. [Cvičení 6: použití parametrů v zobrazení](#Exercise6)
7. [Cvičení 7: zaASP.NETm s novou šablonou MVC 4](#Exercise7)

> [!NOTE]
> Každé cvičení doprovází **koncovou** složku obsahující výsledné řešení, které byste měli získat po dokončení cvičení. Pokud potřebujete další nápovědu k práci prostřednictvím cvičení, můžete toto řešení použít jako vodítko.

Odhadovaný čas dokončení tohoto testovacího prostředí: **60 minut**.

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_MusicStore_ASPNET_MVC_Web_Application_Project"></a>
### <a name="exercise-1-creating-musicstore-aspnet-mvc-web-application-project"></a>Cvičení 1: vytvoření projektu webové aplikace MusicStore ASP.NET MVC

V tomto cvičení se naučíte, jak vytvořit aplikaci ASP.NET MVC v aplikaci Visual Studio 2012 Express for Web i v její hlavní organizaci. Kromě toho se dozvíte, jak přidat nový kontroler a nastavit jeho zobrazení na domovské stránce aplikace jednoduchý řetězec.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_ASPNET_MVC_Web_Application_Project"></a>
#### <a name="task-1---creating-the-aspnet-mvc-web-application-project"></a>Úloha 1 – Vytvoření projektu webové aplikace ASP.NET MVC

1. V této úloze vytvoříte prázdný projekt aplikace ASP.NET MVC pomocí šablony MVC sady Visual Studio. Spusťte **vs Express for Web**.
2. V nabídce **soubor** klikněte na příkaz **Nový projekt**.
3. V dialogovém okně **Nový projekt** vyberte typ projektu **webové aplikace ASP.NET MVC 4** , který je umístěn v **části C#vizuál,** seznam **webových** šablon.
4. Změňte **název** na *MvcMusicStore*.
5. Nastavte umístění řešení v rámci nové **počáteční** složky ve zdrojové složce cvičení, například **[vaše-hol-Path] \Source\Ex01-CreatingMusicStoreProject\Begin**. Klikněte na tlačítko **OK**.

    ![Vytvoření nového projektu – dialogové okno](aspnet-mvc-4-fundamentals/_static/image2.png "Vytvoření nového projektu – dialogové okno")

    *Vytvoření nového projektu – dialogové okno*
6. V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte šablonu **Basic** a ujistěte se, že vybraný **zobrazovací modul** je **Razor**. Klikněte na tlačítko **OK**.

    ![Nový projekt ASP.NET MVC 4 – dialogové okno](aspnet-mvc-4-fundamentals/_static/image3.png "Nový projekt ASP.NET MVC 4 – dialogové okno")

    *Nový projekt ASP.NET MVC 4 – dialogové okno*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Exploring_the_Solution_Structure"></a>
#### <a name="task-2---exploring-the-solution-structure"></a>Úloha 2 – zkoumání struktury řešení

Rozhraní ASP.NET MVC obsahuje šablonu projektu sady Visual Studio, která vám pomůže vytvořit webové aplikace podporující vzor MVC. Tato šablona vytvoří novou webovou aplikaci ASP.NET MVC s požadovanými složkami, šablonami položek a položkami konfiguračního souboru.

V této úloze provedete kontrolu struktury řešení, abyste pochopili prvky, které jsou součástí a jejich vztahy. Následující složky jsou zahrnuté ve všech aplikacích ASP.NET MVC, protože rozhraní ASP.NET MVC ve výchozím nastavení používá ke konfiguraci&quot; přístup &quot;konvenci a vytváří některé výchozí předpoklady na základě zásad vytváření názvů složek.

1. Po vytvoření projektu zkontrolujte strukturu složek, která byla vytvořena v Průzkumník řešení na pravé straně:

    ![Struktura složek ASP.NET MVC v Průzkumník řešení](aspnet-mvc-4-fundamentals/_static/image4.png "Struktura složek ASP.NET MVC v Průzkumník řešení")

    *Struktura složek ASP.NET MVC v Průzkumník řešení*

   1. **Řadiče**. Tato složka bude obsahovat třídy kontroleru. V aplikaci založené na MVC jsou řadiče zodpovědné za zpracování interakce koncového uživatele, manipulace s modelem a nakonec výběr zobrazení pro vykreslení uživatelského rozhraní.

       > [!NOTE]
       > Rozhraní MVC vyžaduje, aby názvy všech řadičů byly ukončeny řadičem &quot;&quot;-například HomeController, LoginController nebo ProductController.
   2. **Modely**. Tato složka je poskytována pro třídy, které reprezentují aplikační model pro webovou aplikaci MVC. To obvykle zahrnuje kód, který definuje objekty a logiku pro interakci s úložištěm dat. Skutečné objekty modelu obvykle budou v samostatných knihovnách tříd. Při vytváření nové aplikace ale můžete zahrnout třídy a pak je přesunout do samostatných knihoven tříd později v rámci vývojového cyklu.
   3. **Zobrazení**. Tato složka je doporučené umístění pro zobrazení, součásti zodpovědné za zobrazení uživatelského rozhraní aplikace. Zobrazení používají soubory. aspx,. ascx,. cshtml a. Master, kromě všech dalších souborů, které se vztahují k vykreslování zobrazení. Složka zobrazení obsahuje složku pro každý kontroler; Složka má název s předponou názvu kontroleru. Například pokud máte řadič s názvem **HomeController**, složka zobrazení bude obsahovat složku s názvem Home. Ve výchozím nastavení, když rozhraní ASP.NET MVC načte zobrazení, vyhledá soubor. aspx s požadovaným názvem zobrazení ve složce Views\controllerName (**zobrazení [kontrolér] [Action]. aspx**) nebo (**zobrazení [kontrolér] [Action]. cshtml**) pro zobrazení Razor.

      > [!NOTE]
      > Kromě dříve uvedených složek používá webová aplikace MVC soubor **Global. asax** k nastavení výchozích nastavení směrování adres URL a používá soubor **Web. config** ke konfiguraci aplikace.

<a id="Ex1Task3"></a>

<a id="Task_3_-_Adding_a_HomeController"></a>
#### <a name="task-3---adding-a-homecontroller"></a>Úloha 3 – přidání HomeController

V aplikacích ASP.NET, které nepoužívají architekturu MVC, je interakce uživatele uspořádána kolem stránek a kolem vyvolání a zpracování událostí z těchto stránek. Naproti tomu interakce uživatele s aplikacemi ASP.NET MVC je uspořádaná kolem řadičů a jejich metod jejich akcí.

Na druhé straně rozhraní ASP.NET MVC mapuje adresy URL na třídy, které jsou označovány jako řadiče. Řadiče zpracovávají příchozí požadavky, zpracovávají uživatelský vstup a interakce, spouštějí příslušnou logiku aplikace a určí odpověď pro odeslání zpátky klientovi (zobrazení HTML, stažení souboru, přesměrování na jinou adresu URL atd.). V případě zobrazení HTML třída kontroleru obvykle volá samostatnou součást zobrazení, která generuje kód HTML pro požadavek. V aplikaci MVC zobrazení pouze zobrazuje informace, zatímco kontroler zpracovává vstup uživatele a interakci s uživatelem a reaguje na ně.

V této úloze přidáte třídu kontroléru, která bude zpracovávat adresy URL na domovské stránce webu hudebního úložiště.

1. V Průzkumník řešení klikněte pravým tlačítkem na složku **řadiče** , vyberte **Přidat** a pak příkaz **kontroleru** :

    ![Přidat kontroler – příkaz](aspnet-mvc-4-fundamentals/_static/image5.png "Přidat kontroler – příkaz")

    *Přidat kontroler – příkaz*
2. Zobrazí se dialogové okno **Přidat řadič** . Pojmenujte kontrolér *HomeController* a stiskněte **Přidat**.

    ![Dialogové okno Přidat řadič](aspnet-mvc-4-fundamentals/_static/image6.png "Dialogové okno Přidat řadič")

    *Dialogové okno Přidat řadič*
3. Soubor **HomeController.cs** se vytvoří ve složce **Controllers** . Aby **HomeController** vrátil řetězec na jeho akci index, nahraďte metodu **indexu** následujícím kódem:

    (Fragment kódu – *základy ASP.NET MVC 4 – EX1 HomeController index*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample1.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>Úloha 4 – spuštění aplikace

V této úloze si vyzkoušíte aplikaci ve webovém prohlížeči.

1. Stisknutím klávesy **F5** spusťte aplikaci. Projekt je zkompilován a spustí se místní webový server služby IIS. Místní webový server služby IIS bude automaticky otevřít webový prohlížeč, který odkazuje na adresu URL webového serveru.

    ![Aplikace spuštěná ve webovém prohlížeči](aspnet-mvc-4-fundamentals/_static/image7.png "Aplikace spuštěná ve webovém prohlížeči")

    *Aplikace spuštěná ve webovém prohlížeči*

    > [!NOTE]
    > Místní webový server služby IIS spustí web na náhodném bezplatném čísle portu. Na obrázku výše je web spuštěný v `http://localhost:50103/`, takže se používá port 50103. Vaše číslo portu se může lišit.
2. Zavřete prohlížeč.

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Controller"></a>
### <a name="exercise-2-creating-a-controller"></a>Cvičení 2: vytvoření kontroleru

V tomto cvičení se dozvíte, jak aktualizovat kontroler pro implementaci jednoduchých funkcí aplikace pro hudební úložiště. Tento kontroler definuje metody akcí pro zpracování všech následujících specifických požadavků:

- Stránka se seznamem hudebních žánrů v obchodě s hudbou
- Stránka pro procházení, na které jsou uvedena všechna hudební alba pro určitý Žánr
- Stránka s podrobnostmi, která zobrazuje informace o konkrétním hudebním albu

V rozsahu tohoto cvičení budou tyto akce jednoduše vracet řetězec nyní.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Adding_a_New_StoreController_Class"></a>
#### <a name="task-1---adding-a-new-storecontroller-class"></a>Úloha 1 – Přidání nové třídy StoreController

V této úloze přidáte nový kontroler.

1. Pokud ještě není otevřený, spusťte **VS Express for Web 2012**.
2. V nabídce **soubor** klikněte na příkaz **Otevřít projekt**. V dialogovém okně Otevřít projekt přejděte na **Source\Ex02-CreatingAController\Begin**, vyberte **Begin. sln** a klikněte na **otevřít**. Alternativně můžete pokračovat v řešení, které jste získali po dokončení předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
3. Přidejte nový kontroler. Provedete to tak, že kliknete pravým tlačítkem myši na složku **Controllers** v rámci Průzkumník řešení, vyberete **Přidat** a pak příkaz **Controller** . Změňte **název kontroleru** na *StoreController*a klikněte na **Přidat**.

    ![Dialogové okno Přidat řadič](aspnet-mvc-4-fundamentals/_static/image8.png "Dialogové okno Přidat řadič")

    *Dialogové okno Přidat řadič*

<a id="Ex2Task2"></a>

<a id="Task_2_-_Modifying_the_StoreControllers_Actions"></a>
#### <a name="task-2---modifying-the-storecontrollers-actions"></a>Úloha 2 – Změna akcí StoreController

V této úloze upravíte metody kontroleru, které se nazývají **Akce**. Akce zodpovídá za zpracování požadavků URL a určení obsahu, který se má poslat zpátky do prohlížeče nebo uživatele, který adresu URL vyvolal.

1. Třída **StoreController** již obsahuje metodu **indexu** . Použijete ji později v tomto testovacím prostředí k implementaci stránky, která obsahuje všechny žánry hudebního obchodu. Prozatím jednoduše nahraďte metodu **indexu** následujícím kódem, který vrátí řetězec &quot;Hello z Store. index ()&quot;:

    (Fragment kódu – *základy ASP.NET MVC 4 – EX2 StoreController index*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample2.cs)]
2. Přidejte metody **Browse** a **Details** . Chcete-li to provést, přidejte do **StoreController**následující kód:

    (Fragment kódu – *základy ASP.NET MVC 4 – EX2 StoreController BrowseAndDetails*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample3.cs)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>Úloha 3 – spuštění aplikace

V této úloze si vyzkoušíte aplikaci ve webovém prohlížeči.

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na **domovské** stránce. Změňte adresu URL pro ověření implementace jednotlivých akcí.

    1. **/Store**. V **&quot;Store. index () se zobrazí&quot;Hello** .
    2. **/Store/Browse**. Zobrazí se **&quot;Hello z Storu. Browse ()&quot;** .
    3. **/Store/Details**. V části Store se zobrazí **&quot;Hello. Details ()&quot;** .

        ![Procházení StoreBrowse](aspnet-mvc-4-fundamentals/_static/image9.png "Procházení StoreBrowse")

        *Procházení/Store/Browse*
3. Zavřete prohlížeč.

<a id="Exercise3"></a>

<a id="Exercise_3_Passing_parameters_to_a_Controller"></a>
### <a name="exercise-3-passing-parameters-to-a-controller"></a>Cvičení 3: předávání parametrů řadiči

Až do této chvíle jste vrátili konstantní řetězce z řadičů. V tomto cvičení se dozvíte, jak předat parametry do kontroleru pomocí adresy URL a řetězce dotazu a potom provést akce metody, které reagují na text do prohlížeče.

<a id="Ex3Task1"></a>

<a id="Task_1_-_Adding_Genre_Parameter_to_StoreController"></a>
#### <a name="task-1---adding-genre-parameter-to-storecontroller"></a>Úloha 1 – Přidání parametru žánru do StoreController

V této úloze použijete dotaz **QueryString** k odeslání parametrů metodě akce **procházení** v **StoreController**.

1. Pokud ještě není otevřený, spusťte **vs Express for Web**.
2. V nabídce **soubor** klikněte na příkaz **Otevřít projekt**. V dialogovém okně Otevřít projekt přejděte na **Source\Ex03-PassingParametersToAController\Begin**, vyberte **Begin. sln** a klikněte na **otevřít**. Alternativně můžete pokračovat v řešení, které jste získali po dokončení předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
3. Otevřete třídu **StoreController** . Provedete to tak, že v **Průzkumník řešení**rozbalíte složku **Controllers (řadiče** ) a dvakrát kliknete na **StoreController.cs**.
4. Změňte metodu **procházení** a přidejte parametr řetězce pro požadavek na konkrétní Žánr. ASP.NET MVC při vyvolání automaticky předáte všechny parametry dotazu nebo formuláře odeslání s názvem **Žánr** na tuto metodu Action. Chcete-li to provést, nahraďte metodu **Browse** následujícím kódem:

    (Fragment kódu – *základy ASP.NET MVC 4 – EX3 StoreController BrowseMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample4.cs)]

> [!NOTE]
> Používáte metodu nástroje **HttpUtility. HtmlEncode** , která uživatelům brání v vkládání JavaScriptu do zobrazení s odkazem jako **/Store/Browse? Žánr =&lt;okno skriptu&gt;Window. Location = '[http://hackersite.com](http://hackersite.com)'&lt;/Script&gt;** .
> 
> Další vysvětlení najdete v [tomto článku na webu MSDN](https://msdn.microsoft.com/library/a2a4yykt(v=VS.80).aspx).

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>Úloha 2 – spuštění aplikace

V této úloze si vyzkoušíte aplikaci ve webovém prohlížeči a použijete parametr **žánru** .

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na **domovské** stránce. Změňte adresu URL na */Store/Browse? Žánr = disco* pro ověření, že akce přijímá parametr žánru.

    ![Procházení StoreBrowseGenre = disco](aspnet-mvc-4-fundamentals/_static/image10.png "Procházení StoreBrowseGenre = disco")

    *Prochází se/Store/Browse? Žánr = disco*
3. Zavřete prohlížeč.

<a id="Ex3Task3"></a>

<a id="Task_3_-_Adding_an_Id_Parameter_Embedded_in_the_URL"></a>
#### <a name="task-3---adding-an-id-parameter-embedded-in-the-url"></a>Úloha 3 – Přidání parametru ID vloženého v adrese URL

V této úloze použijete **adresu URL** k předání parametru **ID** metodě akce **Details** **StoreController**. Výchozí konvence směrování ASP.NET MVC je zacházet s segmentem adresy URL za názvem metody akce jako s parametrem s názvem **ID**. Pokud vaše metoda Action má parametr s názvem ID, pak ASP.NET MVC automaticky předává segment adresy URL jako parametr. V části **úložiště URL/podrobnosti/5**se **ID** bude interpretovat jako **5**.

1. Změňte metodu **Details** objektu **StoreController**přidáním parametru **int** s názvem **ID**. Chcete-li to provést, nahraďte metodu **Details** následujícím kódem:

    (Fragment kódu – *základy ASP.NET MVC 4 – EX3 StoreController DetailsMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample5.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>Úloha 4 – spuštění aplikace

V této úloze si vyzkoušíte aplikaci ve webovém prohlížeči a použijete parametr **ID** .

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na **domovské** stránce. Změňte adresu URL na */Store/Details/5* a ověřte tak, že akce přijme parametr ID.

    ![Procházení StoreDetails5](aspnet-mvc-4-fundamentals/_static/image11.png "Procházení StoreDetails5")

    *Procházení/Store/Details/5*

<a id="Exercise4"></a>

<a id="Exercise_4_Creating_a_View"></a>
### <a name="exercise-4-creating-a-view"></a>Cvičení 4: Vytvoření zobrazení

Zatím jste vrátili řetězce z akcí kontroleru. I když je to užitečný způsob, jak porozumět tomu, jak řadiče fungují, nezpůsobuje to, jak vaše skutečné webové aplikace sestavíte. Zobrazení jsou komponenty, které poskytují lepší přístup k vygenerování kódu HTML zpátky do prohlížeče pomocí souborů šablon.

V tomto cvičení se dozvíte, jak přidat stránku předlohy rozložení, abyste mohli nastavit šablonu pro běžný obsah HTML, šablonu stylů pro vylepšení vzhledu a chování webu a nakonec šablony zobrazení, která umožňuje HomeController vrátit kód HTML.

<a id="Ex4Task1"></a>

<a id="Task_1_-_Modifying_the_file__layoutcshtml"></a>
#### <a name="task-1---modifying-the-file-_layoutcshtml"></a>Úloha 1 – Změna souboru \_layout. cshtml

Soubor **~/Views/Shared/\_layout. cshtml** vám umožní nastavit šablonu pro Common HTML pro použití v celém webu. V této úloze přidáte stránku předlohy rozložení se společným záhlavím s odkazy na domovskou stránku a oblast úložiště.

1. Pokud ještě není otevřený, spusťte **vs Express for Web**.
2. V nabídce **soubor** klikněte na příkaz **Otevřít projekt**. V dialogovém okně Otevřít projekt přejděte na **Source\Ex04-CreatingAView\Begin**, vyberte **Begin. sln** a klikněte na **otevřít**. Alternativně můžete pokračovat v řešení, které jste získali po dokončení předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
3. Soubor <strong>\_layout. cshtml</strong> obsahuje rozložení kontejneru HTML pro všechny stránky na webu. Zahrnuje&lt;prvek <strong>&gt;HTML</strong> pro odpověď HTML a také <strong>&lt;&gt;</strong> a <strong>&lt;tělo&gt;</strong> prvků. <strong>@RenderBody()</strong> v těle HTML identifikují oblasti, které zobrazují šablony, budou moci vyplnit dynamickým obsahem.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample6.cshtml)]
4. Přidejte společnou hlavičku s odkazy na domovskou stránku a oblast pro ukládání na všech stránkách v lokalitě. Chcete-li to provést, přidejte následující kód &lt;tělo&gt; příkaz.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample7.cshtml)]
5. Zahrňte div pro vykreslení oddílu tělo každé stránky. Nahraďte <strong>@RenderBody()</strong> následujícím zvýrazněným kódem: (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample8.cshtml)]

    > [!NOTE]
    > Věděli jste, že? Visual Studio 2012 obsahuje fragmenty kódu, které usnadňují přidávání běžně používaného kódu do HTML, souborů kódu a dalších. Vyzkoušejte si to zadáním **&lt;div&gt;** a dvojím stisknutím klávesy **TAB** vložte úplnou značku **div** .

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_CSS_Stylesheet"></a>
#### <a name="task-2---adding-css-stylesheet"></a>Úloha 2 – Přidání šablony stylů CSS

Prázdná šablona projektu obsahuje velmi zjednodušený soubor CSS, který obsahuje pouze styly používané k zobrazení základních formulářů a ověřovacích zpráv. K vylepšení vzhledu a chování webu budete používat další šablony stylů CSS a obrázky (potenciálně poskytované návrhářem).

V této úloze přidáte šablonu stylů CSS, která definuje styly webu.

1. Do složky **Source\Assets\Content** v tomto testovacím prostředí se zahrnou i soubory CSS a obrázky. Pokud je chcete přidat do aplikace, přetáhněte jejich obsah z okna **Průzkumníka Windows** do **Průzkumník řešení** v Visual Studio Express pro web, jak je znázorněno níže:

    ![Přetahování obsahu stylu](aspnet-mvc-4-fundamentals/_static/image12.png "Přetahování obsahu stylu")

    *Přetahování obsahu stylu*
2. Zobrazí se dialogové okno s upozorněním, které požádá o potvrzení o nahrazení souboru **site. CSS** a některých existujících imagí. Zaškrtněte políčko **použít pro všechny položky** a klikněte na **Ano**.

<a id="Ex4Task3"></a>

<a id="Task_3_-_Adding_a_View_Template"></a>
#### <a name="task-3---adding-a-view-template"></a>Úloha 3 – Přidání šablony zobrazení

V této úloze přidáte šablonu zobrazení, která vygeneruje odpověď HTML, která bude používat stránku předlohy rozložení a šablony stylů CSS přidané v tomto cvičení.

1. Chcete-li použít šablonu zobrazení při procházení domovské stránky webu, budete nejprve muset označit, že místo vrácení řetězce bude metoda **HomeController index** vracet **zobrazení**. Otevřete třídu **HomeController** a změňte její metodu **indexu** tak, aby vracela **ActionResult**a vrátila **zobrazení ()** .

    (Fragment kódu – *základy ASP.NET MVC 4 – Ex4 HomeController index*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample9.cs)]
2. Nyní je třeba přidat příslušnou šablonu zobrazení. Provedete to tak, že **kliknete pravým tlačítkem myši** do metody **index** Action a vyberete **Přidat zobrazení**. Tím se zobrazí dialogové okno **Přidat zobrazení** .

    ![Přidání zobrazení v rámci metody index](aspnet-mvc-4-fundamentals/_static/image13.png "Přidání zobrazení v rámci metody index")

    *Přidání zobrazení v rámci metody index*
3. Zobrazí se dialogové okno **Přidat zobrazení** , ve kterém se vygeneruje soubor šablony zobrazení. Ve výchozím nastavení toto dialogové okno předem vyplní název šablony zobrazení tak, aby odpovídala metodě akce, která ji bude používat. Vzhledem k tomu, že jste použili místní nabídku **Přidat zobrazení** v rámci metody akce **indexu** v rámci HomeController, má dialogové okno **Přidat zobrazení** index jako výchozí název zobrazení. Klikněte na **Přidat**.

    ![Přidat dialog zobrazení](aspnet-mvc-4-fundamentals/_static/image14.png "Přidat dialog zobrazení")

    *Přidat dialog zobrazení*
4. Visual Studio vygeneruje šablonu zobrazení **index. cshtml** ve složce **Views\Home** a pak ji otevře.

    ![Vytvořilo se zobrazení domovského indexu.](aspnet-mvc-4-fundamentals/_static/image15.png "Vytvořilo se zobrazení domovského indexu.")

    *Vytvořilo se zobrazení domovského indexu.*

    > [!NOTE]
    > název a umístění souboru **index. cshtml** je relevantní a řídí se výchozími zásadami vytváření názvů pro ASP.NET MVC.
    > 
    > Složka \Views\**Home** odpovídá názvu kontroleru (**Domovský** adaptér). Název šablony zobrazení (**index**) se shoduje s metodou akce kontroleru, která zobrazení zobrazí.
    > 
    > V ASP.NET MVC se tak vyhnete nutnosti explicitně zadat název nebo umístění šablony zobrazení při použití těchto zásad vytváření názvů k vrácení zobrazení.
5. Vygenerovaná šablona zobrazení je založena na dříve definované šabloně **\_layout. cshtml** . Aktualizujte vlastnost ViewBag. title na **domovskou**stránku a změňte hlavní obsah na **Toto je Domovská stránka**, jak je znázorněno v následujícím kódu:

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample10.cshtml)]
6. V Průzkumník řešení vyberte projekt **MvcMusicStore** a spusťte aplikaci stisknutím klávesy **F5** .

<a id="Ex4Task4"></a>

<a id="Task_4_Verification"></a>
#### <a name="task-4-verification"></a>Úloha 4: ověření

Chcete-li ověřit, zda jste správně provedli všechny kroky v předchozím cvičení, postupujte následovně:

S aplikací otevřenými v prohlížeči byste měli mít na paměti následující:

1. Našla se metoda akce indexu HomeController a zobrazila se šablona zobrazení **\Views\Home\Index.cshtml** , i když kód se nazývá **návratové zobrazení ()** , protože šablona zobrazení následovala standardní konvence pojmenování.
2. Na domovské stránce se zobrazí uvítací zpráva definovaná v rámci šablony zobrazení **\Views\Home\Index.cshtml** .
3. Domovská stránka používá šablonu **\_layout. cshtml** , takže úvodní zpráva je obsažena v rozložení HTML webu Standard.

    ![Zobrazení domovského indexu pomocí definovaných LayoutPage a stylů](aspnet-mvc-4-fundamentals/_static/image16.png "Zobrazení domovského indexu pomocí definovaných LayoutPage a stylů")

    *Zobrazení domovského indexu pomocí definovaných LayoutPage a stylů*

<a id="Exercise5"></a>

<a id="Exercise_5_Creating_a_View_Model"></a>
### <a name="exercise-5-creating-a-view-model"></a>Cvičení 5: vytvoření modelu zobrazení

Zatím jste provedli zobrazení pevně zakódované HTML, ale aby bylo možné vytvářet dynamické webové aplikace, měla by šablona zobrazení přijímat informace z kontroleru. Jednou z běžných postupů, které je vhodné použít k tomuto účelu, je **ViewModel** vzor, který umožňuje řadiči sbalit všechny informace potřebné k vygenerování příslušné odpovědi HTML.

V tomto cvičení se naučíte, jak vytvořit třídu ViewModel a přidat požadované vlastnosti: počet žánrů ve Storu a seznam těchto žánrů. Také aktualizujete StoreController na použití vytvořeného ViewModel a nakonec vytvoříte novou šablonu zobrazení, na které se zobrazí zmíněné vlastnosti na stránce.

<a id="Ex5Task1"></a>

<a id="Task_1_-_Creating_a_ViewModel_Class"></a>
#### <a name="task-1---creating-a-viewmodel-class"></a>Úloha 1 – Vytvoření třídy ViewModel

V této úloze vytvoříte třídu ViewModel, která bude implementovat scénář výpisu žánrů ze Storu.

1. Pokud ještě není otevřený, spusťte **vs Express for Web**.
2. V nabídce **soubor** klikněte na příkaz **Otevřít projekt**. V dialogovém okně Otevřít projekt přejděte na **Source\Ex05-CreatingAViewModel\Begin**, vyberte **Begin. sln** a klikněte na **otevřít**. Alternativně můžete pokračovat v řešení, které jste získali po dokončení předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
3. Vytvořte složku **ViewModels** , která bude obsahovat ViewModel. To provedete tak, že kliknete pravým tlačítkem na projekt **MvcMusicStore** nejvyšší úrovně, vyberete **Přidat** a pak **novou složku**.

    ![Přidání nové složky](aspnet-mvc-4-fundamentals/_static/image17.png "Přidání nové složky")

    *Přidání nové složky*
4. Pojmenujte složku *ViewModels*.

    ![ViewModels složka v Průzkumník řešení](aspnet-mvc-4-fundamentals/_static/image18.png "ViewModels složka v Průzkumník řešení")

    *ViewModels složka v Průzkumník řešení*
5. Vytvořte třídu **ViewModel** . Provedete to tak, že kliknete pravým tlačítkem na nedávno vytvořenou složku **ViewModels** , vyberete **Přidat** a pak **novou položku**. V části **kód**zvolte položku **třídy** a pojmenujte soubor *StoreIndexViewModel.cs*a pak klikněte na tlačítko **Přidat**.

    ![Přidání nové třídy](aspnet-mvc-4-fundamentals/_static/image19.png "Přidání nové třídy")

    *Přidání nové třídy*

    ![Vytváření třídy StoreIndexViewModel](aspnet-mvc-4-fundamentals/_static/image20.png "Vytváření třídy StoreIndexViewModel")

    *Vytváření třídy StoreIndexViewModel*

<a id="Ex5Task2"></a>

<a id="Task_2_-_Adding_Properties_to_the_ViewModel_class"></a>
#### <a name="task-2---adding-properties-to-the-viewmodel-class"></a>Úloha 2 – Přidání vlastností do třídy ViewModel

Existují dva parametry, které mají být předány z StoreController do šablony zobrazení, aby bylo možné vygenerovat očekávanou odpověď HTML: počet žánrů ve Storu a seznam těchto žánrů.

V této úloze přidáte tyto 2 vlastnosti do třídy **StoreIndexViewModel** : **NumberOfGenres** (celé číslo) a **žánry** (seznam řetězců).

1. Přidejte vlastnosti **NumberOfGenres** a **žánrs** do třídy **StoreIndexViewModel** . K tomu přidejte následující 2 řádky do definice třídy:

    (Fragment kódu – *základní informace o ASP.NET MVC 4 – Ex5 StoreIndexViewModel vlastnosti*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample11.cs)]

> [!NOTE]
> Zápis **{Get; Set;}** používá C#funkci automaticky implementovaného vlastností. Poskytuje výhody vlastnosti, aniž by bylo nutné deklarovat pole pro zálohování.

<a id="Ex5Task3"></a>

<a id="Task_3_-_Updating_StoreController_to_use_the_StoreIndexViewModel"></a>
#### <a name="task-3---updating-storecontroller-to-use-the-storeindexviewmodel"></a>Úloha 3 – aktualizace StoreController pro použití StoreIndexViewModel

Třída **StoreIndexViewModel** zapouzdřuje informace potřebné k předání metody indexu **StoreController**do šablony zobrazení, aby bylo možné vygenerovat odpověď.

V této úloze aktualizujete **StoreController** tak, aby používal **StoreIndexViewModel**.

1. Otevřete třídu **StoreController** .

    ![Otevírání třídy StoreController](aspnet-mvc-4-fundamentals/_static/image21.png "Otevírání třídy StoreController")

    *Otevírání třídy StoreController*
2. Aby bylo možné použít třídu **StoreIndexViewModel** z **StoreController**, přidejte následující obor názvů na začátek kódu **StoreController** :

    (Fragment kódu – *ASP.NET MVC 4 – Ex5 StoreIndexViewModel s využitím ViewModels*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample12.cs)]
3. Změňte metodu akce **indexu** **StoreController**tak, aby vytvořila a naplnila objekt **StoreIndexViewModel** a pak ho předá do šablony zobrazení, aby se s ním generovala odpověď HTML.

    > [!NOTE]
    > V testovacím prostředí &quot;ASP.NET MVC a přístup k datům&quot; budete psát kód, který načte seznam žánrů ze Storu z databáze. V následujícím kódu vytvoříte **seznam** fiktivních datových žánrů, které naplní **StoreIndexViewModel**.
    > 
    > Po vytvoření a nastavení objektu **StoreIndexViewModel** bude předán jako argument metody **zobrazení** . To znamená, že šablona zobrazení bude používat tento objekt k vygenerování odpovědi HTML.
4. Nahraďte metodu **indexu** následujícím kódem:

    (Fragment kódu – *ASP.NET MVC 4 – metoda Ex5 StoreController index*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample13.cs)]

> [!NOTE]
> Pokud si nejste obeznámeni C#s, můžete předpokládat, že použití **var** znamená, že proměnná **viewModel** je pozdní vazbou. To není správné – C# kompilátor používá odvození typu v závislosti na tom, co přiřadíte proměnné, abyste zjistili, že **ViewModel** je typu **StoreIndexViewModel**. Také sestavením místní proměnné **viewModel** jako typu **StoreIndexViewModel** získáte kontrolu doby kompilace a podporu editoru kódu sady Visual Studio.

<a id="Ex5Task4"></a>

<a id="Task_4_-_Creating_a_View_Template_that_Uses_StoreIndexViewModel"></a>
#### <a name="task-4---creating-a-view-template-that-uses-storeindexviewmodel"></a>Úloha 4 – Vytvoření šablony zobrazení, která používá StoreIndexViewModel

V této úloze vytvoříte šablonu zobrazení, která bude používat objekt StoreIndexViewModel předaný z kontroleru k zobrazení seznamu žánrů.

1. Než vytvoříte novou šablonu zobrazení, sestavte projekt tak, aby **dialog Přidat zobrazení** věděl o třídě **StoreIndexViewModel** . Sestavte projekt výběrem položky nabídky **sestavení** a poté **Sestavte MvcMusicStore**.

    ![Sestavení projektu](aspnet-mvc-4-fundamentals/_static/image22.png "Sestavení projektu")

    *Sestavení projektu*
2. Vytvoří novou šablonu zobrazení. Provedete to tak, že kliknete pravým tlačítkem dovnitř metody **indexu** a vyberete **Přidat zobrazení**.

    ![Přidání zobrazení](aspnet-mvc-4-fundamentals/_static/image23.png "Přidání zobrazení")

    *Přidání zobrazení*
3. Vzhledem k tomu, že se **dialogové okno Přidat zobrazení** vyvolalo z **StoreController**, přidá se ve výchozím nastavení do souboru **\Views\Store\Index.cshtml** šablona zobrazení. Zaškrtněte políčko **vytvořit silně typovou vlastnost zobrazení** a pak jako **třídu modelu**vyberte **StoreIndexViewModel** . Také se ujistěte, že vybraný zobrazovací modul je **Razor**. Klikněte na **Přidat**.

    ![Přidat dialog zobrazení](aspnet-mvc-4-fundamentals/_static/image24.png "Přidat dialog zobrazení")

    *Přidat dialog zobrazení*

    Vytvoří a otevře se soubor šablony zobrazení **\Views\Store\Index.cshtml** . Na základě informací poskytnutých v dialogovém okně **Přidat zobrazení** v posledním kroku bude šablona zobrazení očekávat instanci **StoreIndexViewModel** jako data, která se mají použít k vygenerování odpovědi HTML. Všimněte si, že šablona dědí `ViewPage<musicstore.viewmodels.storeindexviewmodel>` v C#.

<a id="Ex5Task5"></a>

<a id="Task_5_-_Updating_the_View_Template"></a>
#### <a name="task-5---updating-the-view-template"></a>Úloha 5 – aktualizace šablony zobrazení

V této úloze aktualizujete šablonu zobrazení vytvořenou v posledním úkolu, aby se získal počet žánrů a jejich názvy v rámci stránky.

> [!NOTE]
> K provedení kódu v rámci šablony zobrazení použijete syntaxi @ (často se označuje jako &quot;kódu&quot;Nuggets).

1. V souboru **index. cshtml** v rámci složky **úložiště** nahraďte kód následujícím kódem:

[!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample14.cshtml)]

    > [!NOTE]
    > As soon as you finish typing the period after the word **Model**, Visual Studio's Intellisense will show a list of possible properties and methods to choose from.
    > 
    > ![](aspnet-mvc-4-fundamentals/_static/image25.png)
    > 
    > *Getting Model properties and methods with Visual Studio's IntelliSense*
    > 
    > The **Model** property references the **StoreIndexViewModel** object that the Controller passed to the View template. This means that you can access all of the data passed from the Controller to the View template via the **Model** property, and format it into an appropriate HTML response within the View template.
    > 
    > You can just select the **NumberOfGenres** property from the Intellisense list rather than typing it in and then it will auto-complete it by pressing the **tab key**.
2. Přeskočíte seznam žánrů v **StoreIndexViewModel** a vytvořte&gt;seznam HTML **&lt;ul** pomocí smyčky **foreach** .
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample15.cshtml)]
3. Stisknutím klávesy **F5** spusťte aplikaci a přejděte na **/Store**. Zobrazí se seznam žánrů předaných do objektu **StoreIndexViewModel** z **StoreController** do šablony zobrazení.

    ![Zobrazit zobrazení seznamu žánrů](aspnet-mvc-4-fundamentals/_static/image26.png "Zobrazit zobrazení seznamu žánrů")

    *Zobrazit zobrazení seznamu žánrů*
4. Zavřete prohlížeč.

<a id="Exercise6"></a>

<a id="Exercise_6_Using_Parameters_in_View"></a>
### <a name="exercise-6-using-parameters-in-view"></a>Cvičení 6: použití parametrů v zobrazení

V cvičení 3 jste zjistili, jak předat parametry do kontroleru. V tomto cvičení se naučíte používat tyto parametry v šabloně zobrazení. Pro tento účel se nejprve zavedete na model třídy, které vám pomůžou spravovat vaše data a logiku domény. Dále se naučíte, jak vytvořit odkazy na stránky v aplikaci ASP.NET MVC, aniž byste museli mít obavy, jako je kódování cest URL.

<a id="Ex6Task1"></a>

<a id="Task_1_-_Adding_Model_Classes"></a>
#### <a name="task-1---adding-model-classes"></a>Úloha 1 – Přidání tříd modelu

Na rozdíl od ViewModels, které jsou vytvořeny pouze k předání informací z kontroleru do zobrazení, třídy modelu jsou sestaveny tak, aby obsahovaly a spravovaly data a logiku domény. V této úloze přidáte dvě třídy modelu, které budou představovat tyto koncepty: **Žánr** a **album**.

1. Pokud ještě není otevřený, spusťte **vs Express for Web**
2. V nabídce **soubor** klikněte na příkaz **Otevřít projekt**. V dialogovém okně Otevřít projekt přejděte na **Source\Ex06-UsingParametersInView\Begin**, vyberte **Begin. sln** a klikněte na **otevřít**. Alternativně můžete pokračovat v řešení, které jste získali po dokončení předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
3. Přidejte třídu modelu **žánru** . Provedete to tak, že kliknete pravým tlačítkem na složku **modely** v **Průzkumník řešení**, vyberete **Přidat** a pak **novou položku** . V části **kód**zvolte položku **třídy** a pojmenujte soubor *Genre.cs*a pak klikněte na tlačítko **Přidat**.

    ![Přidání třídy](aspnet-mvc-4-fundamentals/_static/image27.png "Přidání třídy")

    *Přidání nové položky*

    ![Přidat třídu modelu žánru](aspnet-mvc-4-fundamentals/_static/image28.png "Přidat třídu modelu žánru")

    *Přidat třídu modelu žánru*
4. Přidejte do třídy žánru vlastnost **název** . Chcete-li to provést, přidejte následující kód:

    (Fragment kódu – *základy ASP.NET MVC 4 – Žánr Ex6*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample16.cs)]
5. Za stejným postupem jako předtím přidejte třídu **alba** . Provedete to tak, že kliknete pravým tlačítkem na složku **modely** v **Průzkumník řešení**, vyberete **Přidat** a pak **novou položku** . V části **kód**zvolte položku **třídy** a pojmenujte soubor *album.cs*a pak klikněte na tlačítko **Přidat**.
6. Přidejte dvě vlastnosti do třídy alba: **Žánr** a **title**. Chcete-li to provést, přidejte následující kód:

    (Fragment kódu – *základy ASP.NET MVC 4 – album Ex6*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample17.cs)]

<a id="Ex6Task2"></a>

<a id="Task_2_-_Adding_a_StoreBrowseViewModel"></a>
#### <a name="task-2---adding-a-storebrowseviewmodel"></a>Úloha 2 – Přidání StoreBrowseViewModel

V této úloze se použije **StoreBrowseViewModel** , aby se zobrazila alba odpovídající vybranému žánru. V této úloze vytvoříte tuto třídu a pak přidáte dvě vlastnosti, které budou zpracovávat **Žánr** a seznam jeho **alb**.

1. Přidejte třídu **StoreBrowseViewModel** . Provedete to tak, že kliknete pravým tlačítkem na složku **ViewModels** v **Průzkumník řešení**, vyberete **Přidat** a pak **novou položku** . V části **kód**zvolte položku **třídy** a pojmenujte soubor *StoreBrowseViewModel.cs*a pak klikněte na tlačítko **Přidat**.
2. Přidejte odkaz na modely ve třídě **StoreBrowseViewModel** . Chcete-li to provést, přidejte následující obor názvů using:

    (Fragment kódu – *základy ASP.NET MVC 4 – Ex6 UsingModel*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample18.cs)]
3. Přidejte dvě vlastnosti do třídy **StoreBrowseViewModel** : **Žánr** a **alba**. Chcete-li to provést, přidejte následující kód:

    (Fragment kódu – *základy ASP.NET MVC 4 – Ex6 ModelProperties*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample19.cs)]

> [!NOTE]
> Co je **seznam&lt;alba&gt;** ?: Tato definice používá typ **&gt;typu seznam&lt;t** , kde **t** omezuje typ, na který prvky tohoto **seznamu** patří, v tomto případě **alba** (nebo některé z jeho potomků).
> 
> Tato schopnost navrhovat třídy a metody, které odloží specifikace jednoho nebo více typů, dokud není deklarována třída nebo metoda a instance kódu klienta je funkcí C# jazyka s názvem **Obecné**.
> 
> **Seznam&lt;t&gt;** je obecný ekvivalent typu **ArrayList** a je k dispozici v oboru názvů **System. Collections. Generic** . Jednou z výhod použití **generických** typů je, že od zadání typu není nutné provádět kontrolu typu operací, jako je například přetypování prvků do **alba** , stejně jako při práci s objektem **ArrayList**.

<a id="Ex6Task3"></a>

<a id="Task_3_-_Using_the_New_ViewModel_in_the_StoreController"></a>
#### <a name="task-3---using-the-new-viewmodel-in-the-storecontroller"></a>Úloha 3 – použití nového ViewModel v StoreController

V této úloze upravíte metody akce **Browse** a **Detail** pro **StoreController**, které budou používat nový **StoreBrowseViewModel**.

1. Přidejte odkaz do složky modely ve třídě **StoreController** . Provedete to tak, že rozbalíte složku **Controllers** v **Průzkumník řešení** a otevřete třídu **StoreController** . Pak přidejte následující kód:

    (Fragment kódu – *základy ASP.NET MVC 4 – Ex6 UsingModelInController*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample20.cs)]
2. Nahraďte metodu akce **procházení** a použijte třídu **StoreViewBrowseController** . Vytvoříte Žánr a dva nové objekty alba s fiktivními daty (v dalším cvičení budete spotřebovávat skutečná data z databáze). Chcete-li to provést, nahraďte metodu **Browse** následujícím kódem:

    (Fragment kódu – *základy ASP.NET MVC 4 – Ex6 BrowseMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample21.cs)]
3. Nahraďte metodu Action **Details** pro použití třídy **StoreViewBrowseController** . Vytvoří se nový objekt **alba** , který se má vrátit do **zobrazení**. Chcete-li to provést, nahraďte metodu **Details** následujícím kódem:

    (Fragment kódu – *základy ASP.NET MVC 4 – Ex6 DetailsMethod*)

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample22.cs)]

<a id="Ex6Task4"></a>

<a id="Task_4_-_Adding_a_Browse_View_Template"></a>
#### <a name="task-4---adding-a-browse-view-template"></a>Úloha 4 – Přidání šablony zobrazení pro procházení

V této úloze přidáte zobrazení pro **procházení** , ve kterém se zobrazí alba pro určitý Žánr.

1. Předtím, než vytvoříte novou šablonu zobrazení, byste měli sestavit projekt tak, aby dialog **Přidat zobrazení** věděl o třídě **ViewModel** , která se má použít. Sestavte projekt výběrem položky nabídky **sestavení** a poté **Sestavte MvcMusicStore**.
2. Přidejte zobrazení pro **procházení** . Provedete to tak, že kliknete pravým tlačítkem na metodu akce **procházení** **StoreController** a kliknete na **Přidat zobrazení**.
3. V dialogovém okně **Přidat zobrazení** ověřte, zda je název zobrazení **procházen**. Zaškrtněte políčko **vytvořit zobrazení silného typu** a v rozevírací nabídce **třída modelu** vyberte **StoreBrowseViewModel** . Ostatní pole ponechte výchozí hodnotou. Pak klikněte na **Přidat**.

    ![Přidání zobrazení procházení](aspnet-mvc-4-fundamentals/_static/image29.png "Přidání zobrazení procházení")

    *Přidání zobrazení procházení*
4. Upravte **procházení. cshtml** pro zobrazení informací o žánru a přístup k objektu **StoreBrowseViewModel** , který je předán šabloně zobrazení. Chcete-li to provést, nahraďte obsah následujícím způsobem:C#()

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample23.cshtml)]

<a id="Ex6Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>Úloha 5 – spuštění aplikace

V této úloze otestujete, že metoda **procházení** načte alba z akce **Procházet** metodu.

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na domovské stránce. Změňte adresu URL na **/Store/Browse? Žánr = disco** pro ověření, že akce vrátí dvě alba.

    ![Procházení – Uložit alba na discích](aspnet-mvc-4-fundamentals/_static/image30.png "Procházení – Uložit alba na discích")

    *Procházení – Uložit alba na discích*

<a id="Ex6Task6"></a>

<a id="Task_6_-_Displaying_information_About_a_Specific_Album"></a>
#### <a name="task-6---displaying-information-about-a-specific-album"></a>Úloha 6 – zobrazení informací o konkrétním albu

V této úloze implementujete zobrazení **úložiště/podrobností** pro zobrazení informací o konkrétním albu. V této praktické laboratorní laboratoři se všechno, co zobrazíte o albu, již nachází v šabloně **zobrazení** . Takže místo vytvoření třídy **StoreDetailsViewModel** použijete aktuální šablonu **StoreBrowseViewModel** , která do ní předává album.

1. V případě potřeby zavřete prohlížeč a vraťte se do okna sady Visual Studio. Přidejte nové zobrazení **podrobností** pro metodu Action **StoreController** **Details** . Provedete to tak, že kliknete pravým tlačítkem na metodu **Details** ve třídě **StoreController** a kliknete na **Přidat zobrazení**.
2. V dialogovém okně **Přidat zobrazení** ověřte, zda je **název zobrazení** **detailed**. Zaškrtněte políčko **vytvořit zobrazení silného typu** a v rozevíracím seznamu **třída modelu** vyberte **album** . Ostatní pole ponechte výchozí hodnotou. Pak klikněte na **Přidat**. Tím se vytvoří a otevře soubor **\Views\Store\Details.cshtml** .

    ![Přidání zobrazení podrobností](aspnet-mvc-4-fundamentals/_static/image31.png "Přidání zobrazení podrobností")

    *Přidání zobrazení podrobností*
3. Upravte soubor **Details. cshtml** pro zobrazení informací o albu a přístup k objektu **alba** , který je předán šabloně zobrazení. Chcete-li to provést, nahraďte obsah následujícím způsobem:C#()

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample24.cshtml)]

<a id="Ex6Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a>Úloha 7 – spuštění aplikace

V této úloze otestujete, že zobrazení **podrobností** načte informace o albu z metody **Action Details** .

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na **domovské** stránce. Změňte adresu URL na **/Store/Details/5** a ověřte informace o albu.

    ![Podrobnosti o albu procházení](aspnet-mvc-4-fundamentals/_static/image32.png "Podrobnosti o albu procházení")

    *Podrobnosti o procházení alba*

<a id="Ex6Task8"></a>

<a id="Task_8_-_Adding_Links_Between_Pages"></a>
#### <a name="task-8---adding-links-between-pages"></a>Úloha 8 – přidávání odkazů mezi stránkami

V tomto úkolu přidáte odkaz v zobrazení úložiště tak, aby měl odkaz v rámci každého názvu žánru na příslušnou adresu URL **/Store/Browse** . Když kliknete na Žánr, například, bude instance **discového**ovládání přejít na **/Store/Browse? Žánr =** adresa URL.

1. V případě potřeby zavřete prohlížeč a vraťte se do okna sady Visual Studio. Aktualizujte stránku **index** a přidejte odkaz na stránku **procházení** . To provedete tak, že v **Průzkumník řešení** rozbalíte složku **zobrazení** , pak na složku **Store** a dvakrát kliknete na stránku **index. cshtml** .
2. Přidejte odkaz na zobrazení procházení, které indikuje vybraný Žánr. Chcete-li to provést, nahraďte následující zvýrazněný kód v rámci **&lt;&gt;** značkyC#: ()

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample25.cshtml)]

   > [!NOTE]
   > Další postup by se propojuje přímo se stránkou s kódem podobným následujícímu:
   > 
   > &lt;a href =&quot;/Store/Browse? Žánr =@genreName&quot;&gt;@genreName&lt;/a&gt;
   > 
   > I když tento přístup funguje, závisí na pevně zakódované řetězci. Pokud později řadič přejmenujete, budete muset tuto instrukci změnit ručně. Lepší alternativou je použití pomocné metody **HTML** . ASP.NET MVC obsahuje pomocnou metodu HTML, která je pro takové úkoly k dispozici. Pomocná metoda **HTML. ActionLink ()** usnadňuje vytváření **&lt;ch odkazů&gt;** , aby se zajistilo správné kódování URL cest.
   > 
   > HTML. ActionLink má několik přetížení. V tomto cvičení použijete jeden, který má tři parametry:
   > 
   > 1. Text odkazu, ve kterém se zobrazí název žánru
   > 2. Název akce kontroleru (**Procházet**)
   > 3. Hodnoty parametrů směrování, zadání názvu (**Žánr**) a hodnoty (**název žánru**)

<a id="Ex6Task9"></a>

<a id="Task_9_-_Running_the_Application"></a>
#### <a name="task-9---running-the-application"></a>Úloha 9 – spuštění aplikace

V této úloze otestujete, že se každý žánr zobrazuje s odkazem na příslušnou adresu URL **/Store/Browse** .

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na domovské stránce. Změňte adresu URL na **/Store** , abyste ověřili, že každý žánr odkazuje na příslušnou adresu URL **/Store/Browse** .

    ![Procházení žánrů s odkazy na stránku procházení](aspnet-mvc-4-fundamentals/_static/image33.png "Procházení žánrů s odkazy na stránku procházení")

    *Procházení žánrů s odkazy na stránku procházení*

<a id="Ex6Task10"></a>

<a id="Task_10_-_Using_Dynamic_ViewModel_Collection_to_Pass_Values"></a>
#### <a name="task-10---using-dynamic-viewmodel-collection-to-pass-values"></a>Úloha 10 – použití dynamické kolekce ViewModel k předání hodnot

V této úloze se naučíte jednoduchou a výkonnou metodu předávání hodnot mezi kontrolkou a zobrazením bez provedení změn v modelu. ASP.NET MVC 4 poskytuje kolekci &quot;ViewModel&quot;, která se dá přiřadit k libovolné dynamické hodnotě a k nim přistupovaly i v řadičích a zobrazeních.

Nyní použijete dynamickou kolekci ViewBag k předání seznamu &quot;ch **žánrů označených hvězdičkou**&quot; z kontroleru do zobrazení. Zobrazení indexu úložiště bude mít přístup k **ViewModel** a zobrazí se informace.

1. V případě potřeby zavřete prohlížeč a vraťte se do okna sady Visual Studio. Otevřete **StoreController.cs** a upravte metodu **index** a vytvořte seznam žánrů označených hvězdičkou do kolekce ViewModel:

    [!code-csharp[Main](aspnet-mvc-4-fundamentals/samples/sample26.cs)]

    > [!NOTE]
    > Pro přístup k vlastnostem můžete také použít syntaxi **ViewBag [&quot;označených hvězdičkou&quot;]** .
2. Ikona hvězdičky **&quot;označených hvězdičkou. png&quot;** obsažená ve složce **Source\Assets\Images** tohoto testovacího prostředí. Chcete-li jej přidat do aplikace, přetáhněte jeho obsah z okna **Průzkumníka Windows** do **Průzkumník řešení** v aplikaci Visual Web Developer Express, jak je znázorněno níže:

    ![Přidání obrázku hvězdičky do řešení](aspnet-mvc-4-fundamentals/_static/image34.png "Přidání obrázku hvězdičky do řešení")

    *Přidání obrázku hvězdičky do řešení*
3. Otevřete zobrazení **Store/index. cshtml** a upravte obsah. V kolekci **ViewBag** si přečtete vlastnost &quot;označených hvězdičkou&quot; a zobrazí se dotaz, jestli je aktuální název žánru v seznamu. V takovém případě se zobrazí ikona hvězdičky přímo na odkaz Žánr.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-fundamentals/samples/sample27.cshtml)]

<a id="Ex6Task11"></a>

<a id="Task_11_-_Running_the_Application"></a>
#### <a name="task-11---running-the-application"></a>Úloha 11 – spuštění aplikace

V této úloze otestujete, že žánry označených hvězdičkou zobrazí ikonu hvězdičky.

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na **domovské** stránce. Změňte adresu URL na **/Store** a ověřte, že každý doporučený Žánr má popisek pro respektování:

    ![Procházení žánrů pomocí označených hvězdičkou elementů](aspnet-mvc-4-fundamentals/_static/image35.png "Procházení žánrů pomocí označených hvězdičkou elementů")

    *Procházení žánrů pomocí označených hvězdičkou elementů*

<a id="Exercise7"></a>

<a id="Exercise_7_A_lap_around_ASPNET_MVC_4_new_template"></a>
### <a name="exercise-7-a-lap-around-aspnet-mvc-4-new-template"></a>Cvičení 7: zaASP.NETm s novou šablonou MVC 4

V tomto cvičení budete zkoumat vylepšení v šablonách projektů ASP.NET MVC 4 a Prohlédněte si nejdůležitější funkce nové šablony.

<a id="Ex7Task1"></a>

<a id="Task_1_Exploring_the_ASPNET_MVC_4_Internet_Application_Template"></a>
#### <a name="task-1-exploring-the-aspnet-mvc-4-internet-application-template"></a>Úloha 1: zkoumání šablony internetové aplikace ASP.NET MVC 4

1. Pokud ještě není otevřený, spusťte **vs Express for Web**
2. Vyberte **soubor | Nové |** Příkaz nabídky projektu V dialogovém okně **Nový projekt** vyberte **vizuál C#| Webová** šablona ve stromu levého podokna a volba **webové aplikace ASP.NET MVC 4**. **Pojmenujte** projekt *MusicStore* a aktualizujte **název řešení** na *začátek*a pak vyberte umístění (nebo ponechte výchozí) a klikněte na **OK**.

    ![Vytváří se nový projekt ASP.NET MVC 4.](aspnet-mvc-4-fundamentals/_static/image36.png "Vytváří se nový projekt ASP.NET MVC 4.")

    *Vytváří se nový projekt ASP.NET MVC 4.*
3. V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte šablonu projektu **Internetová aplikace** a klikněte na tlačítko **OK**. Všimněte si, že jako zobrazovací modul můžete vybrat buď Razor, nebo ASPX.

    ![Vytváří se nová internetová aplikace ASP.NET MVC 4.](aspnet-mvc-4-fundamentals/_static/image37.png "Vytváří se nová internetová aplikace ASP.NET MVC 4.")

    *Vytváří se nová internetová aplikace ASP.NET MVC 4.*

    > [!NOTE]
    > Syntaxe Razor byla představena v ASP.NET MVC 3. Jeho cílem je minimalizovat počet znaků a klávesových úhozů vyžadovaných v souboru a povolit tak rychlé a kapalné pracovní postupy v kódování. Razor využívá stávající C#jazykové dovednosti v/vb (nebo jiné) a poskytuje syntaxi značek šablony, která umožňuje pracovní postup pro vytváření kódu ve formátu Super HTML.
4. Stisknutím klávesy **F5** spusťte řešení a zobrazte obnovenou šablonu. Můžete se podívat na následující funkce:

    1. **Šablony moderního stylu**

        Šablony byly obnoveny, což poskytuje další styly pro moderní vzhled.

        ![Šablony přeformátované na ASP.NET MVC 4](aspnet-mvc-4-fundamentals/_static/image38.png "Šablony přeformátované na ASP.NET MVC 4")

        *Šablony přeformátované na ASP.NET MVC 4*
    2. **Adaptivní vykreslování**

        Podívejte se na změnu velikosti okna prohlížeče a Všimněte si, jak se rozložení stránky dynamicky přizpůsobí nové velikosti okna. Tyto šablony používají techniku adaptivního vykreslování k tomu, aby se správně vykreslily na stolních i mobilních platformách bez jakýchkoli úprav.

        ![Šablona projektu ASP.NET MVC 4 v různých velikostech prohlížečů](aspnet-mvc-4-fundamentals/_static/image39.png "Šablona projektu ASP.NET MVC 4 v různých velikostech prohlížečů")

        *Šablona projektu ASP.NET MVC 4 v různých velikostech prohlížečů*
5. Zavřete prohlížeč a ukončete ladicí program a vraťte se do sady Visual Studio.
6. Nyní se můžete podívat na řešení a vyzkoušet některé nové funkce, které zavedly ASP.NET MVC 4 v šabloně projektu.

    ![ASP.NET MVC4-Internet-Application-Project-Template](aspnet-mvc-4-fundamentals/_static/image40.png "Šablona projektu internetové aplikace ASP.NET MVC 4")

    *Šablona projektu internetové aplikace ASP.NET MVC 4*

   1. **Značky HTML5**

       Procházejte zobrazením šablon a zjistěte nový kód motivu, například otevřete **o zobrazení. cshtml** v rámci **domovské** složky.

       ![Nová šablona s použitím značek Razor a HTML5](aspnet-mvc-4-fundamentals/_static/image41.png "Nová šablona s použitím značek Razor a HTML5")

       *Nová šablona s použitím značek Razor a HTML5*
   2. **Zahrnuté knihovny JavaScriptu**

      1. **jQuery**: jQuery zjednodušuje procházení dokumentů HTML, zpracování událostí, animaci a interakce AJAX.
      2. **uživatelské rozhraní jQuery**: Tato knihovna poskytuje abstrakce pro interakci a animace nízké úrovně, pokročilé efekty a widgety, které jsou postaveny na knihovně JavaScript jQuery.

         > [!NOTE]
         > Informace o uživatelském rozhraní jQuery a jQuery najdete v [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).
      3. **KnockoutJS**: výchozí šablona ASP.NET MVC 4 teď zahrnuje **KnockoutJS**, rozhraní JavaScript MVVM, které umožňuje vytvářet bohatou a vysoce reagující webové aplikace pomocí JavaScriptu a HTML. Podobně jako v ASP.NET MVC 3 jsou knihovny rozhraní jQuery a jQuery také součástí ASP.NET MVC 4.

          > [!NOTE]
          > Další informace o knihovně KnockOutJS můžete získat v tomto odkazu: [http://learn.knockoutjs.com/](http://learn.knockoutjs.com/).
      4. **Modernizr**: Tato knihovna je spouštěna automaticky, takže při použití technologií HTML5 a CSS3 je váš web kompatibilní se staršími prohlížeči.

          > [!NOTE]
          > Další informace o knihovně modernizr můžete získat v tomto odkazu: [http://www.modernizr.com/](http://www.modernizr.com/).
   3. **SimpleMembership zahrnuté v řešení**

       SimpleMembership byl navržen jako náhrada pro předchozí roli ASP.NET a systém poskytovatele členství. Má mnoho nových funkcí, které vývojářům usnadňuje zabezpečení webových stránek pružnější způsobem.

       Pro integraci SimpleMembership si už sada internetových šablon nastavila několik věcí, například AccountController se připraví na použití OAuthWebSecurity (pro registraci, přihlašování, správu atd.) a zabezpečení webu pomocí protokolu OAuth.

       ![SimpleMembership zahrnuté v řešení](aspnet-mvc-4-fundamentals/_static/image42.png "SimpleMembership zahrnuté v řešení")

       *SimpleMembership zahrnuté v řešení*

       > [!NOTE]
       > Další informace o [OAuthWebSecurity](https://msdn.microsoft.com/library/jj158393(v=vs.111).aspx) najdete na webu MSDN.

> [!NOTE]
> Kromě toho můžete tuto aplikaci nasadit na weby Windows Azure podle [dodatku B: publikování aplikace ASP.NET MVC 4 pomocí nasazení webu](#AppendixB).

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>Souhrn

Vyplněním tohoto praktického cvičení se naučíte základy ASP.NET MVC:

- Základní prvky aplikace MVC a jejich interakce
- Vytvoření aplikace ASP.NET MVC
- Postup přidání a konfigurace řadičů pro zpracování parametrů předaných prostřednictvím adresy URL a řetězce dotazu
- Postup přidání stránky předlohy rozložení pro nastavení šablony pro běžný obsah HTML, šablony stylů pro vylepšení vzhledu a chování a šablony zobrazení pro zobrazení obsahu HTML
- Jak používat vzor ViewModel pro předávání vlastností do šablony zobrazení, aby se zobrazily dynamické informace
- Použití parametrů předaných řadičům v šabloně zobrazení
- Postup přidání odkazů na stránky v aplikaci ASP.NET MVC
- Postup přidání a používání dynamických vlastností v zobrazení
- Vylepšení v šablonách projektů ASP.NET MVC 4

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Příloha A: instalace Visual Studio Express 2012 pro web

**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** . Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.

1. Přejít na [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169). Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;<em>Visual Studio Express 2012 pro web pomocí sady Windows Azure SDK</em>&quot;.
2. Klikněte na **nainstalovat hned**. Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.
3. Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.

    ![Nainstalovat Visual Studio Express](aspnet-mvc-4-fundamentals/_static/image43.png "Nainstalovat Visual Studio Express")

    *Nainstalovat Visual Studio Express*
4. Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**

    ![Přijetí licenčních podmínek](aspnet-mvc-4-fundamentals/_static/image44.png)

    *Přijetí licenčních podmínek*
5. Počkejte na dokončení procesu stahování a instalace.

    ![Průběh instalace](aspnet-mvc-4-fundamentals/_static/image45.png)

    *Průběh instalace*
6. Po dokončení instalace klikněte na **Dokončit**.

    ![Instalace dokončena](aspnet-mvc-4-fundamentals/_static/image46.png)

    *Instalace dokončena*
7. Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.
8. Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .

    ![Dlaždice VS Express for Web](aspnet-mvc-4-fundamentals/_static/image47.png)

    *Dlaždice VS Express for Web*

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Příloha B: publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu

V tomto dodatku se dozvíte, jak vytvořit nový web z Windows Azure Portál pro správu a jak publikovat aplikaci, kterou jste získali, pomocí testovacího prostředí s využitím funkce Nasazení webu pro publikování poskytované službou Windows Azure.

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>Úloha 1 – Vytvoření nového webu z portálu Windows Azure

1. Přejít na [portál pro správu Windows Azure](https://manage.windowsazure.com/) a přihlaste se pomocí přihlašovacích údajů Microsoftu přidružených k vašemu předplatnému.

    > [!NOTE]
    > S Windows Azure můžete hostovat 10 ASP.NET webů zdarma a pak škálovat podle nárůstu provozu. [Tady](https://aka.ms/aspnet-hol-azure)se můžete zaregistrovat.

    ![Přihlaste se k Windows Azure Portal](aspnet-mvc-4-fundamentals/_static/image48.png "Přihlaste se k Windows Azure Portal")

    *Přihlášení k Windows Azure Portál pro správu*
2. Na panelu příkazů klikněte na **Nový** .

    ![Vytvoření nového webu](aspnet-mvc-4-fundamentals/_static/image49.png "Vytvoření nového webu")

    *Vytvoření nového webu*
3. Klikněte na **compute** | **Web**. Pak vyberte možnost **rychlé vytvoření** . Zadejte dostupnou adresu URL pro nový web a klikněte na **vytvořit web**.

    > [!NOTE]
    > Web Windows Azure je hostitelem webové aplikace běžící v cloudu, kterou můžete řídit a spravovat. Možnost rychle vytvořit umožňuje nasadit dokončenou webovou aplikaci do webu Windows Azure z oblasti mimo portál. Nezahrnuje kroky pro nastavení databáze.

    ![Vytvoření nového webu pomocí rychlého vytvoření](aspnet-mvc-4-fundamentals/_static/image50.png "Vytvoření nového webu pomocí rychlého vytvoření")

    *Vytvoření nového webu pomocí rychlého vytvoření*
4. Počkejte, než se nový **Web** vytvoří.
5. Po vytvoření webu klikněte na odkaz ve sloupci **Adresa URL** . Ověřte, zda nový web funguje.

    ![Procházení na nový web](aspnet-mvc-4-fundamentals/_static/image51.png "Procházení na nový web")

    *Procházení na nový web*

    ![Běžící Web](aspnet-mvc-4-fundamentals/_static/image52.png "Běžící Web")

    *Běžící Web*
6. Vraťte se na portál a kliknutím na název webu pod sloupcem **název** zobrazíte stránky pro správu.

    ![Otevření stránek správy webu](aspnet-mvc-4-fundamentals/_static/image53.png "Otevření stránek správy webu")

    *Otevření stránek správy webu*
7. Na stránce **řídicí panel** klikněte v části **rychlý přehled** na odkaz **Stáhnout profil publikování** .

    > [!NOTE]
    > *Profil publikování* obsahuje všechny informace potřebné k publikování webové aplikace na webu Windows Azure pro každou povolenou metodu publikace. Profil publikování obsahuje adresy URL, přihlašovací údaje uživatele a databázové řetězce potřebné k připojení a ověření proti jednotlivým koncovým bodům, pro které je povolena metoda publikace. **Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** a **Microsoft Visual Studio 2012** podporují čtení profilů publikování pro automatizaci konfigurace těchto programů pro publikování webových aplikací na webech Windows Azure.

    ![Stahuje se publikační profil webu.](aspnet-mvc-4-fundamentals/_static/image54.png "Stahuje se publikační profil webu.")

    *Stahuje se publikační profil webu.*
8. Stáhněte si soubor profilu publikování do známého umístění. V tomto cvičení se dozvíte, jak tento soubor použít k publikování webové aplikace na webech Windows Azure ze sady Visual Studio.

    ![Ukládání souboru profilu publikování](aspnet-mvc-4-fundamentals/_static/image55.png "Ukládá se publikační profil.")

    *Ukládání souboru profilu publikování*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>Úloha 2 – Konfigurace databázového serveru

Pokud vaše aplikace využívá SQL Server databází, budete muset vytvořit SQL Database Server. Pokud chcete nasadit jednoduchou aplikaci, která nepoužívá SQL Server, můžete tuto úlohu přeskočit.

1. Pro uložení aplikační databáze budete potřebovat server SQL Database. SQL Database servery můžete zobrazit z předplatného na portálu pro správu Windows Azure na stránce **databáze SQL** | **serverech** | **řídicím panelu serveru**. Pokud nemáte vytvořený server, můžete ho vytvořit pomocí tlačítka **Přidat** na panelu příkazů. Poznamenejte si **název serveru a adresu URL, přihlašovací jméno a heslo správce**, jak je budete používat v dalších úlohách. Databázi ještě nevytvářejte, protože bude vytvořená v pozdější fázi.

    ![Řídicí panel serveru SQL Database](aspnet-mvc-4-fundamentals/_static/image56.png "Řídicí panel serveru SQL Database")

    *Řídicí panel serveru SQL Database*
2. V další úloze budete testovat připojení k databázi ze sady Visual Studio, z tohoto důvodu je třeba zahrnout místní IP adresu do seznamu **povolených IP adres**serveru. Chcete-li to provést, klikněte na tlačítko **Konfigurovat**, vyberte IP adresu z **aktuální IP adresy klienta** a vložte ji do textového pole **Počáteční IP adresa** a **koncová IP adresa** a klikněte na tlačítko ![přidat-Client-IP-Address-OK-tlačítko](aspnet-mvc-4-fundamentals/_static/image57.png).

    ![Přidává se IP adresa klienta.](aspnet-mvc-4-fundamentals/_static/image58.png)

    *Přidává se IP adresa klienta.*
3. Jakmile se **IP adresa klienta** přidá do seznamu povolených IP adres, potvrďte změny kliknutím na **Uložit** .

    ![Potvrdit změny](aspnet-mvc-4-fundamentals/_static/image59.png)

    *Potvrdit změny*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Úloha 3 – publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu

1. Vraťte se do řešení ASP.NET MVC 4. V **Průzkumník řešení**klikněte pravým tlačítkem myši na webový projekt a vyberte **publikovat**.

    ![Publikování aplikace](aspnet-mvc-4-fundamentals/_static/image60.png "Publikování aplikace")

    *Publikování webu*
2. Importujte profil publikování, který jste uložili v prvním úkolu.

    ![Import profilu publikování](aspnet-mvc-4-fundamentals/_static/image61.png "Import profilu publikování")

    *Importuje se publikační profil.*
3. Klikněte na **ověřit připojení**. Po dokončení ověřování klikněte na **Další**.

    > [!NOTE]
    > Ověření je dokončeno, jakmile se zobrazí zelená značka zaškrtnutí vedle tlačítka ověřit připojení.

    ![Ověřování připojení](aspnet-mvc-4-fundamentals/_static/image62.png "Ověřování připojení")

    *Ověřování připojení*
4. Na stránce **Nastavení** v části **databáze** klikněte na tlačítko vedle textového pole připojení k databázi (tj. **DefaultConnection**).

    ![Konfigurace nasazení webu](aspnet-mvc-4-fundamentals/_static/image63.png "Konfigurace nasazení webu")

    *Konfigurace nasazení webu*
5. Připojení k databázi nakonfigurujte následujícím způsobem:

   - Do pole **název serveru** zadejte adresu URL serveru SQL Database pomocí předpony *TCP:* .
   - V **uživatelské jméno** zadejte přihlašovací jméno správce serveru.
   - V **heslo** zadejte přihlašovací heslo správce serveru.
   - Zadejte nový název databáze, například: *MVC4SampleDB*.

     ![Konfigurace cílového připojovacího řetězce](aspnet-mvc-4-fundamentals/_static/image64.png "Konfigurace cílového připojovacího řetězce")

     *Konfigurace cílového připojovacího řetězce*
6. Pak klikněte na **OK**. Po zobrazení výzvy k vytvoření databáze klikněte na **Ano**.

    ![Vytvoření databáze](aspnet-mvc-4-fundamentals/_static/image65.png "Vytváří se řetězec databáze.")

    *Vytvoření databáze*
7. Připojovací řetězec, který budete používat pro připojení k SQL Database ve Windows Azure, se zobrazí ve výchozím textovém poli připojení. Pak klikněte na tlačítko **Další**.

    ![Připojovací řetězec ukazující na SQL Database](aspnet-mvc-4-fundamentals/_static/image66.png "Připojovací řetězec ukazující na SQL Database")

    *Připojovací řetězec ukazující na SQL Database*
8. Na stránce **Náhled** klikněte na **publikovat**.

    ![Publikování webové aplikace](aspnet-mvc-4-fundamentals/_static/image67.png "Publikování webové aplikace")

    *Publikování webové aplikace*
9. Jakmile se proces publikování dokončí, otevře se ve výchozím prohlížeči publikovaný web.

    ![Aplikace byla publikována na platformě Windows Azure](aspnet-mvc-4-fundamentals/_static/image68.png "Aplikace byla publikována na platformě Windows Azure")

    *Aplikace byla publikována na platformě Windows Azure*

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>Příloha C: používání fragmentů kódu

S fragmenty kódu máte veškerý kód, který potřebujete, na dosah ruky. Dokument testovacího prostředí vás přesně upozorní, když ho můžete používat, jak je znázorněno na následujícím obrázku.

![Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio](aspnet-mvc-4-fundamentals/_static/image69.png "Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio")

*Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio*

***Přidání fragmentu kódu pomocí klávesnice (C# pouze)***

1. Umístěte kurzor na místo, kam chcete vložit kód.
2. Začněte psát název fragmentu (bez mezer a spojovníků).
3. Sledujte, jak IntelliSense zobrazuje stejné názvy fragmentů kódu.
4. Vyberte správný fragment kódu (nebo pokračujte v psaní, dokud není vybrán celý název tohoto fragmentu kódu).
5. Dvojím stisknutím klávesy TAB vložte fragment kódu do umístění kurzoru.

![Začněte psát název fragmentu.](aspnet-mvc-4-fundamentals/_static/image70.png "Začněte psát název fragmentu.")

*Začněte psát název fragmentu.*

![Stisknutím klávesy TAB vyberte zvýrazněný fragment.](aspnet-mvc-4-fundamentals/_static/image71.png "Stisknutím klávesy TAB vyberte zvýrazněný fragment.")

*Stisknutím klávesy TAB vyberte zvýrazněný fragment.*

![Stiskněte znovu TAB a fragment kódu se rozšíří.](aspnet-mvc-4-fundamentals/_static/image72.png "Stiskněte znovu TAB a fragment kódu se rozšíří.")

*Stiskněte znovu TAB a fragment kódu se rozšíří.*

***Přidání fragmentu kódu pomocí myši (C#, Visual Basic a XML)*** první. Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.

1. Vyberte **Vložit fragment** a potom **Moje fragmenty kódu**.
2. Kliknutím na něj ze seznamu vyberte příslušný fragment kódu.

![Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.](aspnet-mvc-4-fundamentals/_static/image73.png "Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.")

*Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.*

![Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.](aspnet-mvc-4-fundamentals/_static/image74.png "Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.")

*Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.*

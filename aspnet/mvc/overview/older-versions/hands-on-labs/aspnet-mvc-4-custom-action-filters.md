---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
title: Filtry vlastních akcí ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC poskytuje filtry akcí pro zpracování logiky filtrování před nebo po volání metody Action. Filtry akcí jsou vlastní atributy Tha...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 969ab824-1b98-4552-81fe-b60ef5fc6887
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-custom-action-filters
msc.type: authoredcontent
ms.openlocfilehash: eaeb32180f79fabf557cbc38ff067eb26b47fea7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579693"
---
# <a name="aspnet-mvc-4-custom-action-filters"></a>ASP.NET MVC 4 – filtr vlastních akcí

podle [týmu webového Campy](https://twitter.com/webcamps)

[Stáhnout web Campy Training Kit](https://aka.ms/webcamps-training-kit)

ASP.NET MVC poskytuje filtry akcí pro zpracování logiky filtrování před nebo po volání metody Action. Filtry akcí jsou vlastní atributy, které poskytují deklarativní způsob, jak přidat chování před akcemi a následnou akcím do metod akcí kontroleru.

V tomto praktickém testovacím prostředí vytvoříte vlastní atribut action Filter do řešení MvcMusicStore pro zachycení požadavků kontroléru a Zaprotokolujte aktivitu lokality do databázové tabulky. Filtr protokolování budete moct přidat vložením do libovolného kontroleru nebo akce. Nakonec se zobrazí zobrazení protokolu, které zobrazuje seznam návštěvníků.

Tato praktická cvičení předpokládá, že máte základní znalosti o **ASP.NET MVC**. Pokud jste ještě **ASP.NET MVC** nepoužívali, doporučujeme, abyste si převzali v praxi **ASP.NET MVC 4** pro praktické cvičení.

> [!NOTE]
> Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Training Kit, která je dostupná v [verzích Microsoft-Web/WebCampTrainingKit](https://aka.ms/webcamps-training-kit). Projekt, který je specifický pro toto testovací prostředí, je k dispozici ve [vlastních filtrech akcí ASP.NET MVC 4](https://github.com/Microsoft-Web/HOL-MVC4CustomActionFilters).

<a id="Objectives"></a>
### <a name="objectives"></a>Cíle

V této praktické laboratorní laboratoři se dozvíte, jak:

- Vytvoření vlastního atributu filtru akcí pro rozšiřování možností filtrování
- Použití vlastního atributu filtru vložením na určitou úroveň
- Globální registrace filtrů vlastních akcí

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Předpoklady

K dokončení tohoto testovacího prostředí musíte mít následující položky:

- [Microsoft Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) nebo nadřazený seznam (pokyny k instalaci najdete v [příloze a](#AppendixA) ).

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>Nastavení

**Instalace fragmentů kódu**

Pro usnadnění práce je většina kódu, který budete spravovat v tomto testovacím prostředí, k dispozici jako fragmenty kódu sady Visual Studio. Chcete-li nainstalovat fragmenty kódu, spusťte soubor **.\Source\Setup\CodeSnippets.vsi** .

Pokud nejste obeznámeni s fragmentem Visual Studio Code a chcete se dozvědět, jak je používat, můžete odkazovat na přílohu z tohoto dokumentu &quot;[příloze C: použití fragmentů kódu](#AppendixC)&quot;.

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>Cvičení

Tato praktická cvičení se skládají z následujících cvičení:

1. [Cvičení 1: protokolování akcí](#Exercise1)
2. [Cvičení 2: Správa více filtrů akcí](#Exercise2)

Odhadovaný čas dokončení tohoto testovacího prostředí: **30 minut**.

> [!NOTE]
> Každé cvičení doprovází **koncovou** složku obsahující výsledné řešení, které byste měli získat po dokončení cvičení. Pokud potřebujete další nápovědu k práci prostřednictvím cvičení, můžete toto řešení použít jako vodítko.

<a id="Exercise1"></a>

<a id="Exercise_1_Logging_Actions"></a>
### <a name="exercise-1-logging-actions"></a>Cvičení 1: protokolování akcí

V tomto cvičení se naučíte, jak vytvořit vlastní filtr protokolu akcí pomocí zprostředkovatelů filtru ASP.NET MVC 4. Pro tento účel použijete filtr protokolování na web MusicStore, který bude zaznamená všechny aktivity ve vybraných řadičích.

Filtr rozšíří **ActionFilterAttributeClass** a přepíše metodu **OnActionExecuting** pro zachycení jednotlivých požadavků a následné provádění akcí protokolování. Kontextové informace o požadavcích HTTP, spouštění metod, výsledků a parametrech budou poskytnuty třídou ASP.NET MVC **ActionExecutingContext** **.**

> [!NOTE]
> ASP.NET MVC 4 má také výchozí zprostředkovatele filtrů, které můžete použít bez vytvoření vlastního filtru. ASP.NET MVC 4 nabízí následující typy filtrů:
> 
> - Filtr **autorizace** , který umožňuje rozhodování o zabezpečení, zda se má provést metoda akce, například provedení ověření nebo ověření vlastností žádosti.
> - Filtr **akcí** , který zabalí provádění metody Action. Tento filtr může provádět další zpracování, například poskytnutí dalších dat metodě akce, kontrolu návratové hodnoty nebo zrušení provádění metody Action.
> - Filtr **výsledků** , který zabalí provádění objektu ActionResult. Tento filtr může provést další zpracování výsledku, jako je například změna odpovědi HTTP.
> - Filtr **výjimek** , který se spustí, pokud je v metodě Action vyvolána neošetřená výjimka, počínaje filtry autorizace a končí prováděním výsledku. Filtry výjimek lze použít pro úlohy, jako je protokolování nebo zobrazení chybové stránky.
> 
> Další informace o zprostředkovatelích filtrů najdete na tomto odkazu na webu MSDN: ([https://msdn.microsoft.com/library/dd410209.aspx](https://msdn.microsoft.com/library/dd410209.aspx)).

<a id="AboutLoggingFeature"></a>

<a id="About_MVC_Music_Store_Application_logging_feature"></a>
#### <a name="about-mvc-music-store-application-logging-feature"></a>Informace o funkci protokolování hudby pro aplikace MVC pro Store

Toto řešení pro hudební úložiště obsahuje novou tabulku datového modelu pro protokolování lokality **ActionLog**s následujícími poli: název řadiče, který obdržel požadavek, se nazývá akce, IP adresa klienta a časové razítko.

![Datový model. Tabulka ActionLog](aspnet-mvc-4-custom-action-filters/_static/image1.png "Datový model. Tabulka ActionLog")

*Datový model – tabulka ActionLog*

Řešení poskytuje zobrazení ASP.NET MVC pro protokol akcí, který lze najít v **MvcMusicStores/views/ActionLog**:

![Zobrazení protokolu akcí](aspnet-mvc-4-custom-action-filters/_static/image2.png "Zobrazení protokolu akcí")

*Zobrazení protokolu akcí*

U této struktury se bude všechny práce zaměřit na požadavek řadiče s přerušením a provádění protokolování pomocí vlastního filtrování.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_Custom_Filter_to_Catch_a_Controllers_Request"></a>
#### <a name="task-1---creating-a-custom-filter-to-catch-a-controllers-request"></a>Úloha 1 – Vytvoření vlastního filtru pro zachycení žádosti řadiče

V této úloze vytvoříte vlastní třídu atributů filtru, která bude obsahovat logiku protokolování. Pro tento účel budete rozšířeni třídu ASP.NET MVC **ActionFilterAttribute** a implementujete rozhraní **IActionFilter**.

> [!NOTE]
> **ActionFilterAttribute** je základní třídou pro všechny filtry atributů. Poskytuje následující metody pro spuštění konkrétní logiky po a před provedením akce kontroleru:
> 
> - **OnActionExecuting**(ActionExecutingContext filterContext): těsně před voláním metody Action.
> - **OnActionExecuted**(ActionExecutedContext filterContext): po volání metody Action a před provedením výsledku (před zobrazením vykreslování).
> - **OnResultExecuting**(ResultExecutingContext filterContext): těsně před provedením výsledku (před zobrazením vykreslování).
> - **OnResultExecuted**(ResultExecutedContext filterContext): po provedení výsledku (po vykreslení zobrazení).
> 
> Přepsáním kterékoli z těchto metod na odvozenou třídu můžete spustit vlastní kód pro filtrování.

1. Otevřete řešení **začít** umístěné ve složce **\Source\Ex01-LoggingActions\Begin** .

   1. Než budete pokračovat, budete muset stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
      > 
      > Další informace najdete v tomto článku: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).
2. Přidejte novou C# třídu do složky **Filters** a pojmenujte ji *CustomActionFilter.cs*. Tato složka bude ukládat všechny vlastní filtry.
3. Otevřete **CustomActionFilter.cs** a přidejte odkaz na obory názvů **System. Web. Mvc** a **MvcMusicStore. Models** :

    (Fragment kódu – *ASP.NET MVC 4 – filtry vlastních akcí – EX1-CustomActionFilterNamespaces*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample1.cs)]
4. Dědí třídu **CustomActionFilter** z **ActionFilterAttribute** a pak třídu **CustomActionFilter** implementují rozhraní **IActionFilter** .

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample2.cs)]
5. Udělejte třídu **CustomActionFilter** přepsání metody **OnActionExecuting** a přidejte potřebnou logiku pro protokolování provádění filtru. K tomu přidejte následující zvýrazněný kód v rámci třídy **CustomActionFilter** .

    (Fragment kódu – *ASP.NET MVC 4 – filtry vlastních akcí – EX1-LoggingActions*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample3.cs#Highlight)]

    > [!NOTE]
    > Metoda **OnActionExecuting** používá **Entity Framework** k přidání nového registru ActionLog. Vytvoří a vyplní novou instanci entity s informacemi o kontextu z **filterContext**.
    > 
    > Další informace o třídě **ControllerContext** najdete na [webu MSDN](https://msdn.microsoft.com/library/system.web.mvc.controllercontext.aspx).

<a id="Ex1Task2"></a>

<a id="Task_2_-_Injecting_a_Code_Interceptor_into_the_Store_Controller_Class"></a>
#### <a name="task-2---injecting-a-code-interceptor-into-the-store-controller-class"></a>Úloha 2 – vložení Zachytávosti kódu do třídy kontroleru úložiště

V této úloze přidáte vlastní filtr tak, že ho vložíte do všech tříd kontroleru a kontrolují akce kontroleru, které budou protokolovány. Pro účely tohoto cvičení bude mít třída kontroleru úložiště protokol.

Metoda **OnActionExecuting** z vlastního filtru **ActionLogFilterAttribute** se spouští při volání vloženého prvku.

Je také možné zachytit konkrétní metodu kontroleru.

1. Otevřete **StoreController** na **MvcMusicStore\Controllers** a přidejte odkaz na obor názvů **Filters** :

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample4.cs)]
2. Vložení vlastního filtru **CustomActionFilter** do třídy **StoreController** přidáním atributu **[CustomActionFilter]** před deklarací třídy.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample5.cs)]

   > [!NOTE]
   > Pokud je do třídy kontroleru vložen filtr, jsou také vloženy všechny jeho akce. Chcete-li použít filtr pouze pro sadu akcí, budete muset vložit **[CustomActionFilter]** do každého z nich:
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample6.cs)]

<a id="Ex1Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>Úloha 3 – spuštění aplikace

V této úloze otestujete, zda filtr protokolování funguje. Spustíte aplikaci a navštívíte úložiště a pak zkontrolujete protokolované aktivity.

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Přejděte na **/ActionLog** a zobrazte počáteční stav zobrazení protokolu:

    ![Stav sledování protokolu před aktivitou stránky](aspnet-mvc-4-custom-action-filters/_static/image3.png "Stav sledování protokolu před aktivitou stránky")

    *Stav sledování protokolu před aktivitou stránky*

   > [!NOTE]
   > Ve výchozím nastavení se vždy zobrazí jedna položka, která je generována při načítání existujících žánrů pro nabídku.
   > 
   > Pro zjednodušení čistíme tabulku **ActionLog** pokaždé, když se aplikace spustí, takže se zobrazí jenom protokoly jednotlivých ověření daného úkolu.
   > 
   > Aby bylo možné uložit historický protokol pro všechny akce spouštěné v rámci kontroleru úložiště, může být nutné odebrat následující kód z metody **Session\_Start** (ve třídě **Global. asax** ).
   > 
   > [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample7.cs)]
3. V nabídce klikněte na jeden z **žánrů** a proveďte některé akce, jako je procházení dostupného alba.
4. Přejděte na **/ActionLog** a pokud je protokol prázdný, stiskněte klávesu **F5** , aby se stránka aktualizovala. Ověřte, že byly vaše návštěvy sledovány:

    ![Protokol akcí s protokolem aktivit](aspnet-mvc-4-custom-action-filters/_static/image4.png "Protokol akcí s protokolem aktivit")

    *Protokol akcí s protokolem aktivit*

<a id="Exercise2"></a>

<a id="Exercise_2_Managing_Multiple_Action_Filters"></a>
### <a name="exercise-2-managing-multiple-action-filters"></a>Cvičení 2: Správa více filtrů akcí

V tomto cvičení přidáte druhý filtr vlastní akce do třídy StoreController a definujete konkrétní pořadí, ve kterém budou oba filtry provedeny. Pak aktualizujete kód pro globální registraci filtru.

Při definování pořadí spouštění filtrů existují různé možnosti, které je potřeba vzít v úvahu. Například vlastnost Order a rozsah filtrů:

Můžete definovat **Rozsah** pro každý z filtrů, například můžete určit rozsah všech filtrů akcí, které mají být spuštěny v rámci **oboru kontroleru**, a všechny autorizační filtry pro spuštění v **globálním oboru**. Obory mají definované pořadí provádění.

Každý filtr akcí navíc má vlastnost Order, která se používá k určení pořadí spouštění v oboru filtru.

Další informace o pořadí spouštění vlastních filtrů akcí najdete v tomto článku na webu MSDN: ([https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx](https://msdn.microsoft.com/library/dd381609(v=vs.98).aspx)).

<a id="Ex2Task1"></a>

<a id="Task_1_Creating_a_new_Custom_Action_Filter"></a>
#### <a name="task-1-creating-a-new-custom-action-filter"></a>Úloha 1: vytvoření nového filtru vlastních akcí

V této úloze vytvoříte nový filtr vlastní akce, který bude vložen do třídy StoreController, takže se naučíte spravovat pořadí provádění filtrů.

1. Otevřete řešení **začít** umístěné ve složce **\Source\Ex02-ManagingMultipleActionFilters\Begin** . V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.

    1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
    2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
    3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

        > [!NOTE]
        > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
        > 
        > Další informace najdete v tomto článku: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).
2. Přidejte novou C# třídu do složky **Filters** a pojmenujte ji *MyNewCustomActionFilter.cs* .
3. Otevřete **MyNewCustomActionFilter.cs** a přidejte odkaz na **System. Web. Mvc** a obor názvů **MvcMusicStore. Models** :

    (Fragment kódu – *ASP.NET MVC 4 – filtry vlastních akcí – EX2-MyNewCustomActionFilterNamespaces*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample8.cs)]
4. Nahraďte výchozí deklaraci třídy následujícím kódem.

    (Fragment kódu – *ASP.NET MVC 4 – filtry vlastních akcí – EX2-MyNewCustomActionFilterClass*)

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample9.cs)]

    > [!NOTE]
    > Tento filtr vlastní akce je skoro stejný než ten, který jste vytvořili v předchozím cvičení. Hlavním rozdílem je, že má *&quot;protokolovaná&quot;* atributem s tímto novým názvem Class, který identifikuje, který filtr zaregistroval protokol.

<a id="Ex2Task2"></a>

<a id="Task_2_Injecting_a_new_Code_Interceptor_into_the_StoreController_Class"></a>
#### <a name="task-2-injecting-a-new-code-interceptor-into-the-storecontroller-class"></a>Úkol 2: vložení nového Zachytávosti kódu do třídy StoreController

V této úloze přidáte nový vlastní filtr do třídy StoreController a spustíte řešení, abyste ověřili, jak oba filtry vzájemně spolupracují.

1. Otevřete třídu **StoreController** umístěnou na adrese **MvcMusicStore\Controllers** a vložením nového vlastního filtru **MyNewCustomActionFilter** do třídy **StoreController** , jako je znázorněno v následujícím kódu.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample10.cs)]
2. Nyní spusťte aplikaci, abyste viděli, jak tyto dvě filtry vlastní akce fungují. Pokud to chcete provést, stiskněte klávesu **F5** a počkejte, dokud se aplikace nespustí.
3. Přejděte na **/ActionLog** a zobrazte počáteční stav zobrazení protokolu.

    ![Stav sledování protokolu před aktivitou stránky](aspnet-mvc-4-custom-action-filters/_static/image5.png "Stav sledování protokolu před aktivitou stránky")

    *Stav sledování protokolu před aktivitou stránky*
4. V nabídce klikněte na jeden z **žánrů** a proveďte některé akce, jako je procházení dostupného alba.
5. Ověřte, že tento čas; vaše návštěvy byly sledovány dvakrát: jednou pro každý z vlastních filtrů akcí, které jste přidali ve třídě **StorageController** .

    ![Protokol akcí s protokolem aktivit](aspnet-mvc-4-custom-action-filters/_static/image6.png "Protokol akcí s protokolem aktivit")

    *Protokol akcí s protokolem aktivit*
6. Zavřete prohlížeč.

<a id="Ex2Task3"></a>

<a id="Task_3_Managing_Filter_Ordering"></a>
#### <a name="task-3-managing-filter-ordering"></a>Úloha 3: Správa řazení filtru

V této úloze se dozvíte, jak spravovat pořadí spouštění filtrů pomocí vlastnosti Order.

1. Otevřete třídu **StoreController** umístěnou na adrese **MvcMusicStore\Controllers** a určete vlastnost **Order** v obou filtrech, jak je znázorněno níže.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample11.cs)]
2. Nyní ověřte, jak jsou filtry spouštěny v závislosti na hodnotě vlastnosti pořadí. Zjistíte, že filtr s nejmenší hodnotou objednávky (**CustomActionFilter**) je první spuštěný. Stiskněte klávesu **F5** a počkejte, dokud se aplikace nespustí.
3. Přejděte na **/ActionLog** a zobrazte počáteční stav zobrazení protokolu.

    ![Stav sledování protokolu před aktivitou stránky](aspnet-mvc-4-custom-action-filters/_static/image7.png "Stav sledování protokolu před aktivitou stránky")

    *Stav sledování protokolu před aktivitou stránky*
4. V nabídce klikněte na jeden z **žánrů** a proveďte některé akce, jako je procházení dostupného alba.
5. Ověřte, že v tuto chvíli byly vaše návštěvy sledovány seřazené podle hodnoty pořadí filtrů: **CustomActionFilter** Logs.

    ![Protokol akcí s protokolem aktivit](aspnet-mvc-4-custom-action-filters/_static/image8.png "Protokol akcí s protokolem aktivit")

    *Protokol akcí s protokolem aktivit*
6. Nyní aktualizujete hodnotu pořadí filtrů a ověříte způsob, jakým se mění pořadí protokolování. Ve třídě **StoreController** aktualizujte hodnotu objednávky filters, jak je uvedeno níže.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample12.cs)]
7. Spusťte aplikaci znovu stisknutím klávesy **F5**.
8. V nabídce klikněte na jeden z **žánrů** a proveďte některé akce, jako je procházení dostupného alba.
9. Ověřte, že se nejprve zobrazí protokoly vytvořené filtrem **MyNewCustomActionFilter** .

    ![Protokol akcí s protokolem aktivit](aspnet-mvc-4-custom-action-filters/_static/image9.png "Protokol akcí s protokolem aktivit")

    *Protokol akcí s protokolem aktivit*

<a id="Ex2Task4"></a>

<a id="Task_4_Registering_Filters_Globally"></a>
#### <a name="task-4-registering-filters-globally"></a>Úloha 4: globální registrace filtrů

V této úloze aktualizujete řešení a zaregistrujete nový filtr (**MyNewCustomActionFilter**) jako globální filtr. Tím dojde k aktivaci všemi akcemi provedenými v aplikaci a nikoli pouze v StoreController, jako u předchozí úlohy.

1. Ve třídě **StoreController** odeberte atribut **[MyNewCustomActionFilter]** a vlastnost Order z **[CustomActionFilter]** . Měl by vypadat takto:

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample13.cs)]
2. Otevřete soubor **Global. asax** a vyhledejte **aplikaci\_spustit** metodu. Všimněte si, že při každém spuštění aplikace se registruje globální filtry voláním metody **RegisterGlobalFilters** v rámci třídy **FilterConfig** .

    ![Globální filtry se registrují v Global. asax.](aspnet-mvc-4-custom-action-filters/_static/image10.png "Globální filtry se registrují v Global. asax.")

    *Globální filtry se registrují v Global. asax.*
3. Otevřete soubor **FilterConfig.cs** ve složce **App\_Start** .
4. Přidat odkaz na použití System. Web. Mvc; použití MvcMusicStore. filters; hosting.

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample14.cs)]
5. Aktualizujte metodu **RegisterGlobalFilters** přidáním vlastního filtru. Chcete-li to provést, přidejte zvýrazněný kód:

    [!code-csharp[Main](aspnet-mvc-4-custom-action-filters/samples/sample15.cs)]
6. Spusťte aplikaci stisknutím klávesy **F5**.
7. V nabídce klikněte na jeden z **žánrů** a proveďte některé akce, jako je procházení dostupného alba.
8. Ověřte, zda je nyní **[MyNewCustomActionFilter]** vloženo v HomeController a ActionLogController.

    ![Protokol akcí s protokolem aktivit](aspnet-mvc-4-custom-action-filters/_static/image11.png "Protokol akcí s protokolem aktivit")

    *Protokol akcí s protokolem globálních aktivit*

> [!NOTE]
> Kromě toho můžete tuto aplikaci nasadit na weby Windows Azure podle [dodatku B: publikování aplikace ASP.NET MVC 4 pomocí nasazení webu](#AppendixB).

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>Souhrn

Vyplněním tohoto praktického cvičení jste zjistili, jak roztáhnout filtr akcí, aby bylo možné provádět vlastní akce. Také jste se naučili, jak vložit libovolný filtr na vaše řadiče stránky. Použily se následující koncepty:

- Jak vytvořit vlastní filtry akcí pomocí třídy ASP.NET MVC ActionFilterAttribute
- Vložení filtrů do řadičů ASP.NET MVC
- Jak spravovat řazení filtrů pomocí vlastnosti Order
- Globální registraci filtrů

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Příloha A: instalace Visual Studio Express 2012 pro web

**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** . Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.

1. Přejděte do [ (Nastavení)https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169) (Integrace a služby). Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;<em>Visual Studio Express 2012 pro web pomocí sady Windows Azure SDK</em>&quot;.
2. Klikněte na **nainstalovat hned**. Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.
3. Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.

    ![Nainstalovat Visual Studio Express](aspnet-mvc-4-custom-action-filters/_static/image12.png "Nainstalovat Visual Studio Express")

    *Nainstalovat Visual Studio Express*
4. Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**

    ![Přijetí licenčních podmínek](aspnet-mvc-4-custom-action-filters/_static/image13.png)

    *Přijetí licenčních podmínek*
5. Počkejte na dokončení procesu stahování a instalace.

    ![Průběh instalace](aspnet-mvc-4-custom-action-filters/_static/image14.png)

    *Průběh instalace*
6. Po dokončení instalace klikněte na **Dokončit**.

    ![Instalace dokončena](aspnet-mvc-4-custom-action-filters/_static/image15.png)

    *Instalace dokončena*
7. Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.
8. Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .

    ![Dlaždice VS Express for Web](aspnet-mvc-4-custom-action-filters/_static/image16.png)

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

    ![Přihlaste se k Windows Azure Portal](aspnet-mvc-4-custom-action-filters/_static/image17.png "Přihlaste se k Windows Azure Portal")

    *Přihlášení k Windows Azure Portál pro správu*
2. Na panelu příkazů klikněte na **Nový** .

    ![Vytvoření nového webu](aspnet-mvc-4-custom-action-filters/_static/image18.png "Vytvoření nového webu")

    *Vytvoření nového webu*
3. Klikněte na **compute** | **Web**. Pak vyberte možnost **rychlé vytvoření** . Zadejte dostupnou adresu URL pro nový web a klikněte na **vytvořit web**.

    > [!NOTE]
    > Web Windows Azure je hostitelem webové aplikace běžící v cloudu, kterou můžete řídit a spravovat. Možnost rychle vytvořit umožňuje nasadit dokončenou webovou aplikaci do webu Windows Azure z oblasti mimo portál. Nezahrnuje kroky pro nastavení databáze.

    ![Vytvoření nového webu pomocí rychlého vytvoření](aspnet-mvc-4-custom-action-filters/_static/image19.png "Vytvoření nového webu pomocí rychlého vytvoření")

    *Vytvoření nového webu pomocí rychlého vytvoření*
4. Počkejte, než se nový **Web** vytvoří.
5. Po vytvoření webu klikněte na odkaz ve sloupci **Adresa URL** . Ověřte, zda nový web funguje.

    ![Procházení na nový web](aspnet-mvc-4-custom-action-filters/_static/image20.png "Procházení na nový web")

    *Procházení na nový web*

    ![Běžící Web](aspnet-mvc-4-custom-action-filters/_static/image21.png "Běžící Web")

    *Běžící Web*
6. Vraťte se na portál a kliknutím na název webu pod sloupcem **název** zobrazíte stránky pro správu.

    ![Otevření stránek správy webu](aspnet-mvc-4-custom-action-filters/_static/image22.png "Otevření stránek správy webu")

    *Otevření stránek správy webu*
7. Na stránce **řídicí panel** klikněte v části **rychlý přehled** na odkaz **Stáhnout profil publikování** .

    > [!NOTE]
    > *Profil publikování* obsahuje všechny informace potřebné k publikování webové aplikace na webu Windows Azure pro každou povolenou metodu publikace. Profil publikování obsahuje adresy URL, přihlašovací údaje uživatele a databázové řetězce potřebné k připojení a ověření proti jednotlivým koncovým bodům, pro které je povolena metoda publikace. **Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** a **Microsoft Visual Studio 2012** podporují čtení profilů publikování pro automatizaci konfigurace těchto programů pro publikování webových aplikací na webech Windows Azure.

    ![Stahuje se publikační profil webu.](aspnet-mvc-4-custom-action-filters/_static/image23.png "Stahuje se publikační profil webu.")

    *Stahuje se publikační profil webu.*
8. Stáhněte si soubor profilu publikování do známého umístění. V tomto cvičení se dozvíte, jak tento soubor použít k publikování webové aplikace na webech Windows Azure ze sady Visual Studio.

    ![Ukládání souboru profilu publikování](aspnet-mvc-4-custom-action-filters/_static/image24.png "Ukládá se publikační profil.")

    *Ukládání souboru profilu publikování*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>Úloha 2 – Konfigurace databázového serveru

Pokud vaše aplikace využívá SQL Server databází, budete muset vytvořit SQL Database Server. Pokud chcete nasadit jednoduchou aplikaci, která nepoužívá SQL Server, můžete tuto úlohu přeskočit.

1. Pro uložení aplikační databáze budete potřebovat server SQL Database. SQL Database servery můžete zobrazit z předplatného na portálu pro správu Windows Azure na stránce **databáze SQL** | **serverech** | **řídicím panelu serveru**. Pokud nemáte vytvořený server, můžete ho vytvořit pomocí tlačítka **Přidat** na panelu příkazů. Poznamenejte si **název serveru a adresu URL, přihlašovací jméno a heslo správce**, jak je budete používat v dalších úlohách. Databázi ještě nevytvářejte, protože bude vytvořená v pozdější fázi.

    ![Řídicí panel serveru SQL Database](aspnet-mvc-4-custom-action-filters/_static/image25.png "Řídicí panel serveru SQL Database")

    *Řídicí panel serveru SQL Database*
2. V další úloze budete testovat připojení k databázi ze sady Visual Studio, z tohoto důvodu je třeba zahrnout místní IP adresu do seznamu **povolených IP adres**serveru. Chcete-li to provést, klikněte na tlačítko **Konfigurovat**, vyberte IP adresu z **aktuální IP adresy klienta** a vložte ji do textového pole **Počáteční IP adresa** a **koncová IP adresa** a klikněte na tlačítko ![přidat-Client-IP-Address-OK-tlačítko](aspnet-mvc-4-custom-action-filters/_static/image26.png).

    ![Přidává se IP adresa klienta.](aspnet-mvc-4-custom-action-filters/_static/image27.png)

    *Přidává se IP adresa klienta.*
3. Jakmile se **IP adresa klienta** přidá do seznamu povolených IP adres, potvrďte změny kliknutím na **Uložit** .

    ![Potvrdit změny](aspnet-mvc-4-custom-action-filters/_static/image28.png)

    *Potvrdit změny*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Úloha 3 – publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu

1. Vraťte se do řešení ASP.NET MVC 4. V **Průzkumník řešení**klikněte pravým tlačítkem myši na webový projekt a vyberte **publikovat**.

    ![Publikování aplikace](aspnet-mvc-4-custom-action-filters/_static/image29.png "Publikování aplikace")

    *Publikování webu*
2. Importujte profil publikování, který jste uložili v prvním úkolu.

    ![Import profilu publikování](aspnet-mvc-4-custom-action-filters/_static/image30.png "Import profilu publikování")

    *Importuje se publikační profil.*
3. Klikněte na **ověřit připojení**. Po dokončení ověřování klikněte na **Další**.

    > [!NOTE]
    > Ověření je dokončeno, jakmile se zobrazí zelená značka zaškrtnutí vedle tlačítka ověřit připojení.

    ![Ověřování připojení](aspnet-mvc-4-custom-action-filters/_static/image31.png "Ověřování připojení")

    *Ověřování připojení*
4. Na stránce **Nastavení** v části **databáze** klikněte na tlačítko vedle textového pole připojení k databázi (tj. **DefaultConnection**).

    ![Konfigurace nasazení webu](aspnet-mvc-4-custom-action-filters/_static/image32.png "Konfigurace nasazení webu")

    *Konfigurace nasazení webu*
5. Připojení k databázi nakonfigurujte následujícím způsobem:

   - Do pole **název serveru** zadejte adresu URL serveru SQL Database pomocí předpony *TCP:* .
   - V **uživatelské jméno** zadejte přihlašovací jméno správce serveru.
   - V **heslo** zadejte přihlašovací heslo správce serveru.
   - Zadejte nový název databáze.

     ![Konfigurace cílového připojovacího řetězce](aspnet-mvc-4-custom-action-filters/_static/image33.png "Konfigurace cílového připojovacího řetězce")

     *Konfigurace cílového připojovacího řetězce*
6. Pak klikněte na **OK**. Po zobrazení výzvy k vytvoření databáze klikněte na **Ano**.

    ![Vytvoření databáze](aspnet-mvc-4-custom-action-filters/_static/image34.png "Vytváří se řetězec databáze.")

    *Vytvoření databáze*
7. Připojovací řetězec, který budete používat pro připojení k SQL Database ve Windows Azure, se zobrazí ve výchozím textovém poli připojení. Pak klikněte na tlačítko **Další**.

    ![Připojovací řetězec ukazující na SQL Database](aspnet-mvc-4-custom-action-filters/_static/image35.png "Připojovací řetězec ukazující na SQL Database")

    *Připojovací řetězec ukazující na SQL Database*
8. Na stránce **Náhled** klikněte na **publikovat**.

    ![Publikování webové aplikace](aspnet-mvc-4-custom-action-filters/_static/image36.png "Publikování webové aplikace")

    *Publikování webové aplikace*
9. Jakmile se proces publikování dokončí, otevře se ve výchozím prohlížeči publikovaný web.

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>Příloha C: používání fragmentů kódu

S fragmenty kódu máte veškerý kód, který potřebujete, na dosah ruky. Dokument testovacího prostředí vás přesně upozorní, když ho můžete používat, jak je znázorněno na následujícím obrázku.

![Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio](aspnet-mvc-4-custom-action-filters/_static/image37.png "Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio")

*Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio*

***Přidání fragmentu kódu pomocí klávesnice (C# pouze)***

1. Umístěte kurzor na místo, kam chcete vložit kód.
2. Začněte psát název fragmentu (bez mezer a spojovníků).
3. Sledujte, jak IntelliSense zobrazuje stejné názvy fragmentů kódu.
4. Vyberte správný fragment kódu (nebo pokračujte v psaní, dokud není vybrán celý název tohoto fragmentu kódu).
5. Dvojím stisknutím klávesy TAB vložte fragment kódu do umístění kurzoru.

![Začněte psát název fragmentu.](aspnet-mvc-4-custom-action-filters/_static/image38.png "Začněte psát název fragmentu.")

*Začněte psát název fragmentu.*

![Stisknutím klávesy TAB vyberte zvýrazněný fragment.](aspnet-mvc-4-custom-action-filters/_static/image39.png "Stisknutím klávesy TAB vyberte zvýrazněný fragment.")

*Stisknutím klávesy TAB vyberte zvýrazněný fragment.*

![Stiskněte znovu TAB a fragment kódu se rozšíří.](aspnet-mvc-4-custom-action-filters/_static/image40.png "Stiskněte znovu TAB a fragment kódu se rozšíří.")

*Stiskněte znovu TAB a fragment kódu se rozšíří.*

***Přidání fragmentu kódu pomocí myši (C#, Visual Basic a XML)*** první. Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.

1. Vyberte **Vložit fragment** a potom **Moje fragmenty kódu**.
2. Kliknutím na něj ze seznamu vyberte příslušný fragment kódu.

![Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.](aspnet-mvc-4-custom-action-filters/_static/image41.png "Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.")

*Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.*

![Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.](aspnet-mvc-4-custom-action-filters/_static/image42.png "Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.")

*Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.*

---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
title: Vkládání závislostí ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: 'Poznámka: Tato praktická cvičení předpokládá, že máte základní znalosti o ASP.NET MVC a ASP.NETch filtrech MVC 4. Pokud jste předtím nepoužívali ASP.NET filtry MVC 4, připravujeme...'
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 84c7baca-1c54-4c44-8f52-4282122d6acb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: 15c9d4dcb9e2c6b9f6adf54d65d15737b32cca3b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78560611"
---
# <a name="aspnet-mvc-4-dependency-injection"></a>ASP.NET MVC 4 – injektáž závislostí

podle [týmu webového Campy](https://twitter.com/webcamps)

[Stáhnout web Campy Training Kit](https://aka.ms/webcamps-training-kit)

Tato praktická cvičení předpokládá, že máte základní znalosti o filtrech **ASP.NET MVC** a **ASP.NET MVC 4**. Pokud jste předtím nepoužívali **ASP.NET filtry MVC 4** , doporučujeme, abyste si převzali více než v praxi **vlastní filtry akcí ASP.NET MVC** .

> [!NOTE]
> Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Training Kit, která je dostupná v [verzích Microsoft-Web/WebCampTrainingKit](https://aka.ms/webcamps-training-kit). Projekt, který je specifický pro toto testovací prostředí, je k dispozici pro [vkládání závislostí ASP.NET MVC 4](https://github.com/Microsoft-Web/HOL-MVC4DependencyInjection).

V **objektově orientovaném programovacím** paradigmatu objekty spolupracují v modelu spolupráce, kde jsou přispěvatelé a příjemci. Přirozeně tento komunikační model generuje závislosti mezi objekty a komponentami a je obtížné ho spravovat, když se zvyšuje složitost.

![Závislosti tříd a složitost modelu](aspnet-mvc-4-dependency-injection/_static/image1.png "Závislosti tříd a složitost modelu")

*Závislosti tříd a složitost modelu*

Pravděpodobně jste se dozvěděli o **modelu továrny** a oddělení mezi rozhraním a implementací pomocí služeb, kde jsou objekty klienta často zodpovědné za umístění služby.

Vzor injektáže závislosti je konkrétní implementace inverze ovládacího prvku. **Inverze ovládacího prvku (IOC)** znamená, že objekty nevytvářejí další objekty, na kterých spoléhají na jejich práci. Místo toho získají objekty, které potřebují z vnějšího zdroje (například konfigurační soubor XML).

**Vkládání závislostí (di)** znamená, že je provedeno bez zásahu objektu, obvykle komponentou rozhraní, která předá parametry konstruktoru a nastavují vlastnosti.

<a id="The_Dependency_Injection_DI_Design_Pattern"></a>
### <a name="the-dependency-injection-di-design-pattern"></a>Vzor návrhu vkládání závislostí (DI)

V nejvyšší úrovni je cílem injektáže závislostí, že třída klienta (například *Golf*) potřebuje něco, co splňuje rozhraní (např. *IClub*). Nezáleží na tom, jaký konkrétní typ je (např. *WoodClub, IronClub, WedgeClub* nebo *PutterClub*), chce někomu jinému, aby to zpracovával (například dobrý *Caddy*). Překladač závislostí v ASP.NET MVC vám může dovolit zaregistrovat logiku závislosti někde jinde (například kontejner nebo *penalto*).

![Diagram injektáže závislosti](aspnet-mvc-4-dependency-injection/_static/image2.png "Ilustrace injektáže závislosti")

*Vložení závislostí – Analogová a golfová*

Výhody použití vzoru injektáže závislosti a inverze ovládacího prvku jsou následující:

- Zmenší párování tříd.
- Zvyšuje znovu použití kódu.
- Vylepšuje udržovatelnost kódu
- Vylepšuje testování aplikací

> [!NOTE]
> Vkládání závislostí se někdy porovnává s abstraktním vzorem návrhu výroby, ale mezi oběma přístupy je mírně rozdíl. DI má architekturu pro řešení závislostí voláním továrn a registrovaných služeb.

Teď, když rozumíte vzoru vkládání závislostí, se v tomto testovacím prostředí naučíte, jak ho použít v ASP.NET MVC 4. Zahájíte použití injektáže závislosti v **řadičích** pro zahrnutí služby přístupu k databázi. V dalším kroku použijete vložení závislostí na **zobrazení** , která budou využívat službu a zobrazí informace. Nakonec rozšíříte filtry DI na ASP.NET MVC 4 a vložíte do řešení vlastní filtr akcí.

V této praktické laboratorní laboratoři se dozvíte, jak:

- Integrace ASP.NET MVC 4 s Unity pro vkládání závislostí pomocí balíčků NuGet
- Použití injektáže závislosti v rámci kontroleru ASP.NET MVC
- Použití injektáže závislosti v zobrazení ASP.NET MVC
- Použití injektáže závislosti v rámci filtru akcí ASP.NET MVC

> [!NOTE]
> Toto testovací prostředí používá balíček NuGet. Mvc3 pro řešení závislostí, ale je možné přizpůsobit libovolné rozhraní injektáže závislostí pro práci s ASP.NET MVC 4.

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

Pokud nejste obeznámeni s fragmentem Visual Studio Code a chcete se dozvědět, jak je používat, můžete odkazovat na přílohu z tohoto dokumentu &quot;[příloze B: použití fragmentů kódu](#AppendixB)&quot;.

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>Cvičení

Tato praktická cvičení se skládají z následujících cvičení:

1. [Cvičení 1: vložení kontroleru](#Exercise1)
2. [Cvičení 2: Vložení zobrazení](#Exercise2)
3. [Cvičení 3: vložení filtrů](#Exercise3)

> [!NOTE]
> Každé cvičení doprovází **koncovou** složku obsahující výsledné řešení, které byste měli získat po dokončení cvičení. Pokud potřebujete další nápovědu k práci prostřednictvím cvičení, můžete toto řešení použít jako vodítko.

Odhadovaný čas dokončení tohoto testovacího prostředí: **30 minut**.

<a id="Exercise1"></a>

<a id="Exercise_1_Injecting_a_Controller"></a>
### <a name="exercise-1-injecting-a-controller"></a>Cvičení 1: vložení kontroleru

V tomto cvičení se naučíte používat vkládání závislostí v řadičích ASP.NET MVC integrací Unity pomocí balíčku NuGet. Z tohoto důvodu byste do řadičů MvcMusicStore zahrnuli služby, které budou oddělit logiku od přístupu k datům. Služby vytvoří novou závislost v konstruktoru kontroleru, který bude vyřešen pomocí injektáže závislostí s využitím **Unity**.

Tento přístup vám ukáže, jak vygenerovat méně propojených aplikací, které jsou flexibilnější a jednodušší při údržbě a testování. Naučíte se také, jak integrovat ASP.NET MVC s Unity.

<a id="About_StoreManager_Service"></a>
#### <a name="about-storemanager-service"></a>O službě StoreManager

Hudební úložiště MVC poskytované v řešení zahájit teď obsahuje službu, která spravuje data kontroleru úložiště s názvem **StoreService**. Níže najdete implementaci služby Store. Všimněte si, že všechny metody vrací entity modelu.

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample1.cs)]

**StoreController** z řešení Begin teď spotřebovává **StoreService**. Všechny odkazy na data se odebraly z **StoreController**a teď je možné změnit stávajícího poskytovatele přístupu k datům, aniž byste museli měnit žádnou metodu, která využívá **StoreService**.

Zjistíte, že implementace **StoreController** má závislost s **StoreService** uvnitř konstruktoru třídy.

> [!NOTE]
> Závislost představená v tomto cvičení se vztahuje k **inverze řízení** (IOC).
> 
> Konstruktor třídy **StoreController** přijímá parametr typu **IStoreService** , který je nezbytný pro provádění volání služby zevnitř třídy. **StoreController** však neimplementuje výchozí konstruktor (bez parametrů), že musí mít každý kontroler fungovat s ASP.NET MVC.
> 
> Chcete-li vyřešit závislost, musí být kontrolér vytvořen abstraktní továrnou (třída, která vrací libovolný objekt zadaného typu).

[!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample2.cs)]

> [!NOTE]
> Pokud se třída pokusí vytvořit StoreController bez odeslání objektu služby, zobrazí se chyba, protože není deklarován konstruktor bez parametrů.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Running_the_Application"></a>
#### <a name="task-1---running-the-application"></a>Úloha 1 – spuštění aplikace

V této úloze spustíte aplikaci Begin, která bude zahrnovat službu do řadiče úložiště, který odděluje přístup k datům z aplikační logiky.

Při spuštění aplikace se zobrazí výjimka, protože služba kontroleru se ve výchozím nastavení nepředává jako parametr:

1. Otevřete řešení **začít** umístěné v **Source\Ex01-injecting Controller\Begin**.

   1. Než budete pokračovat, budete muset stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
2. Stisknutím **kombinace kláves CTRL + F5** spusťte aplikaci bez ladění. Zobrazí se chybová zpráva &quot;**pro tento objekt není definován konstruktor bez parametrů**&quot;:

    ![Chyba při spouštění aplikace ASP.NET MVC begin](aspnet-mvc-4-dependency-injection/_static/image3.png "Chyba při spouštění aplikace ASP.NET MVC begin")

    *Chyba při spouštění aplikace ASP.NET MVC begin*
3. Zavřete prohlížeč.

V následujících krocích budete v řešení úložiště pro hudbu pracovat s cílem vložit závislost, kterou tento kontroler potřebuje.

<a id="Ex1Task2"></a>

<a id="Task_2_-_Including_Unity_into_MvcMusicStore_Solution"></a>
#### <a name="task-2---including-unity-into-mvcmusicstore-solution"></a>Úkol 2 – zahrnutí Unity do řešení MvcMusicStore

V této úloze budete do řešení zahrnout balíček NuGet **. Mvc3** NuGet.

> [!NOTE]
> Balíček Unity. Mvc3 byl navržen pro ASP.NET MVC 3, ale je plně kompatibilní s ASP.NET MVC 4.
> 
> Unity je jednoduchý a rozšiřitelný kontejner vkládání závislostí s volitelnou podporou pro instance a zachycení typu. Je to kontejner pro obecné účely pro použití v jakémkoli typu aplikace .NET. Poskytuje všechny společné funkce v mechanismech injektáže závislostí, včetně: vytvoření objektu, abstrakce požadavků zadáním závislostí za běhu a flexibilitu, odložením konfigurace komponenty do kontejneru.

1. Nainstalujte balíček NuGet **. Mvc3** NuGet do projektu **MvcMusicStore** . Provedete to tak, že otevřete **konzolu Správce balíčků** ze **zobrazení** | **jiných oknech**.
2. Spusťte následující příkaz.

    PMC

    [!code-powershell[Main](aspnet-mvc-4-dependency-injection/samples/sample3.ps1)]

    ![Instaluje se balíček NuGet. Mvc3 NuGet.](aspnet-mvc-4-dependency-injection/_static/image4.png "Instaluje se balíček NuGet. Mvc3 NuGet.")

    *Instaluje se balíček NuGet. Mvc3 NuGet.*
3. Jakmile je balíček **Unity. Mvc3** nainstalovaný, prozkoumejte soubory a složky, které automaticky přidá, aby se zjednodušila konfigurace Unity.

    ![Balíček Unity. Mvc3 je nainstalovaný.](aspnet-mvc-4-dependency-injection/_static/image5.png "Balíček Unity. Mvc3 je nainstalovaný.")

    *Balíček Unity. Mvc3 je nainstalovaný.*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Registering_Unity_in_Globalasaxcs_Application_Start"></a>
#### <a name="task-3---registering-unity-in-globalasaxcs-application_start"></a>Úloha 3 – registrace Unity v Global.asax.cs aplikaci\_Start

V této úloze aktualizujete metodu **\_aplikace** , která se nachází v **Global.asax.cs** , aby volala inicializátor zaváděcího nástroje Unity a pak aktualizovala soubor zaváděcího nástroje, který registruje službu a řadič, který budete používat pro vkládání závislostí.

1. Teď se připojíte ke zaváděcímu programu, který je souborem, který inicializuje kontejner Unity a překladač závislostí. Provedete to tak, že otevřete **Global.asax.cs** a do **aplikace\_Start** přidáte následující zvýrazněný kód.

    (Fragment kódu – *ASP.NET Dependency vstřiking Lab-Ex01-Initialize Unity*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample4.cs)]
2. Otevřete soubor **Bootstrapper.cs** .
3. Zahrňte následující obory názvů: **MvcMusicStore. Services** a **MusicStore. Controllers**.

    (Fragment kódu – *ASP.NET Dependency vstřiking Lab-Ex01-zaváděcí obory názvů*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample5.cs)]
4. Nahraďte obsah metody **BuildUnityContainer** následujícím kódem, který registruje řadič úložiště a službu úložiště.

    (Fragment kódu – *ASP.NET Dependency vstřiking Lab-Ex01 – registrace kontroleru a služby úložiště*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample6.cs)]

<a id="Ex1Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>Úloha 4 – spuštění aplikace

V této úloze spustíte aplikaci, abyste ověřili, že se teď dá načíst po zahrnutí Unity.

1. Stisknutím klávesy **F5** spusťte aplikaci, aplikace by se nyní měla načíst bez zobrazení jakékoli chybové zprávy.

    ![Běžící aplikace se vkládáním závislostí](aspnet-mvc-4-dependency-injection/_static/image6.png "Běžící aplikace se vkládáním závislostí")

    *Běžící aplikace se vkládáním závislostí*
2. Přejděte na **/Store**. Tím se vyvolá **StoreController**, který se teď vytvoří pomocí **Unity**.

    ![Hudební úložiště MVC](aspnet-mvc-4-dependency-injection/_static/image7.png "Hudební úložiště MVC")

    *Hudební úložiště MVC*
3. Zavřete prohlížeč.

V následujících cvičeních se naučíte, jak rozšířením oboru pro vkládání závislostí použít uvnitř zobrazení ASP.NET MVC a filtry akcí.

<a id="Exercise2"></a>

<a id="Exercise_2_Injecting_a_View"></a>
### <a name="exercise-2-injecting-a-view"></a>Cvičení 2: Vložení zobrazení

V tomto cvičení se naučíte používat vkládání závislostí v zobrazení s novými funkcemi ASP.NET MVC 4 pro integraci Unity. Aby to bylo možné, budete volat vlastní službu v zobrazení pro procházení úložiště, ve kterém se zobrazí zpráva a obrázek níže.

Pak budete projekt integrovat s Unity a vytvoříte vlastní překladač závislostí pro vložení závislostí.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Creating_a_View_that_Consumes_a_Service"></a>
#### <a name="task-1---creating-a-view-that-consumes-a-service"></a>Úkol 1 – Vytvoření zobrazení, které využívá službu

V této úloze vytvoříte zobrazení, které provede volání služby, aby se vygenerovala nová závislost. Služba se skládá z jednoduché služby zasílání zpráv zahrnuté v tomto řešení.

1. Otevřete řešení **začít** umístěné ve složce **Source\Ex02-injecting View\Begin** . V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
      > 
      > Další informace najdete v tomto článku: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).
2. Zahrňte třídy **MessageService.cs** a **IMessageService.cs** umístěné ve složce **source \Assets** v **/Services**. Provedete to tak, že kliknete pravým tlačítkem na složku **služby** a vyberete **Přidat existující položku**. Vyhledejte umístění soubory a zahrňte je.

    ![Přidání služby zpráv a rozhraní služby](aspnet-mvc-4-dependency-injection/_static/image8.png "Přidání služby zpráv a rozhraní služby")

    *Přidání služby zpráv a rozhraní služby*

    > [!NOTE]
    > Rozhraní **IMessageService** definuje dvě vlastnosti implementované třídou **MessageService** . Tyto vlastnosti –**zpráva** a **ImageUrl**– uloží zprávu a adresu URL obrázku, který se má zobrazit.
3. Vytvořte složku **/Pages** v kořenové složce projektu a pak přidejte existující třídu **MyBasePage.cs** z **Source\Assets**. Základní stránka, ze které budete dědit, má následující strukturu.

    ![Složka stránky](aspnet-mvc-4-dependency-injection/_static/image9.png "Složka stránky")

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample7.cs)]
4. Otevřete zobrazení **Procházet. cshtml** ze složky **/views/Store** a nastavte jeho dědění z **MyBasePage.cs**.

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample8.cshtml)]
5. V zobrazení **Procházet** přidejte volání **MessageService** k zobrazení obrázku a zprávy, kterou služba získala.
   (C#)

    [!code-cshtml[Main](aspnet-mvc-4-dependency-injection/samples/sample9.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Including_a_Custom_Dependency_Resolver_and_a_Custom_View_Page_Activator"></a>
#### <a name="task-2---including-a-custom-dependency-resolver-and-a-custom-view-page-activator"></a>Úloha 2 – včetně vlastního překladače závislostí a vlastní aktivační procedury stránky zobrazení

V předchozím úkolu jste do zobrazení vložili novou závislost, která v rámci něj provede volání služby. Nyní tuto závislost vyřeší implementací rozhraní injektáže závislosti ASP.NET MVC **IViewPageActivator** a **IDependencyResolver**. Do řešení zahrnete implementaci **IDependencyResolver** , která se bude zabývat s načítáním služby pomocí Unity. Pak budete zahrnovat další vlastní implementaci rozhraní **IViewPageActivator** , která vyřeší vytváření zobrazení.

> [!NOTE]
> Vzhledem k tomu, že ASP.NET MVC 3, implementace pro vkládání závislostí zjednodušila rozhraní k registraci služeb. **IDependencyResolver** a **IViewPageActivator** jsou součástí funkcí ASP.NET MVC 3 pro vkládání závislostí.
> 
> **– Rozhraní IDependencyResolver** nahrazuje předchozí IMvcServiceLocator. Implementátori třídy IDependencyResolver musí vracet instanci služby nebo kolekce služeb.
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample10.cs)]
> 
> **-IViewPageActivator** rozhraní poskytuje podrobnější kontrolu nad tím, jak jsou stránky zobrazení vytvořeny pomocí injektáže závislostí. Třídy, které implementují rozhraní **IViewPageActivator** , mohou vytvářet instance zobrazení pomocí informací o kontextu.
> 
> 
> [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample11.cs)]

1. Vytvořte složku/**továrny** v kořenové složce projektu.
2. Zahrňte do svého řešení **CustomViewPageActivator.cs** ze složky **/sources/assets/** to **Factory** . Provedete to tak, že kliknete pravým tlačítkem na složku **/Factories** , vyberete **Přidat | Existující položka** a pak vyberte **CustomViewPageActivator.cs**. Tato třída implementuje rozhraní **IViewPageActivator** pro uchování kontejneru Unity.

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample12.cs)]

    > [!NOTE]
    > **CustomViewPageActivator** zodpovídá za správu vytváření zobrazení pomocí kontejneru Unity.
3. Zahrnout soubor **UnityDependencyResolver.cs** z **/sources/assets** do složky **/Factories** Provedete to tak, že kliknete pravým tlačítkem na složku **/Factories** , vyberete **Přidat | Existující položka** a potom vyberte soubor **UnityDependencyResolver.cs** .

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample13.cs)]

    > [!NOTE]
    > Třída **UnityDependencyResolver** je vlastní DependencyResolver pro Unity. Pokud se služba v kontejneru Unity nedá najít, je základní překladač invocated.

V následujících úlohách budou registrovány obě implementace, aby model věděl umístění služeb a zobrazení.

<a id="Ex2Task3"></a>

<a id="Task_3_-_Registering_for_Dependency_Injection_within_Unity_container"></a>
#### <a name="task-3---registering-for-dependency-injection-within-unity-container"></a>Úloha 3 – registrace pro vkládání závislostí v kontejneru Unity

V této úloze vložíte všechny předchozí věci, aby se provedla práce injektáže.

Až teď vaše řešení obsahuje následující prvky:

- Zobrazení **procházení** , které dědí z **MyBaseClass** a spotřebovává **MessageService**.
- Zprostředkující třída –**MyBaseClass**– obsahuje vkládání závislostí deklarované pro rozhraní služby.
- Služba- **MessageService** -a jeho rozhraní **IMessageService**.
- Vlastní překladač závislostí pro Unity- **UnityDependencyResolver** – který se zabývá načítáním služeb.
- Stránka zobrazení Activator – **CustomViewPageActivator** – vytvoří stránku.

Pro vložení zobrazení pro **procházení** teď zaregistrujete vlastní překladač závislostí do kontejneru Unity.

1. Otevřete soubor **Bootstrapper.cs** .
2. Zaregistrujte instanci **MessageService** do kontejneru Unity pro inicializaci služby:

    (Fragment kódu – *ASP.NET Dependency vstřiking Lab-Ex02-Register Message Service*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample14.cs)]
3. Přidejte odkaz na obor názvů **MvcMusicStore. Factory** .

    (Fragment kódu – *ASP.NET pro vkládání závislostí – obor názvů Ex02-Factory*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample15.cs)]
4. Zaregistrujte **CustomViewPageActivator** jako aktivátor stránky zobrazení do kontejneru Unity:

    (Fragment kódu – *ASP.NET Dependency vstřiking Lab-Ex02-Register CustomViewPageActivator*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample16.cs)]
5. Nahraďte výchozí překladač závislostí ASP.NET MVC 4 instancí **UnityDependencyResolver**. Chcete-li to provést, nahraďte obsah metody **Initialize** následujícím kódem:

    (Fragment kódu – *testovací prostředí pro vkládání závislostí ASP.NET – Ex02 – aktualizace překladače závislostí*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample17.cs)]

    > [!NOTE]
    > ASP.NET MVC poskytuje výchozí třídu překladače závislosti. Pokud chcete pracovat s vlastními Překladači závislostí, jako je ta, kterou jsme vytvořili pro Unity, je nutné tento překladač vyměnit.

<a id="Ex2Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>Úloha 4 – spuštění aplikace

V této úloze spustíte aplikaci, abyste ověřili, že prohlížeč Store používá službu, a zobrazí se obrázek a načtená zpráva:

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. V nabídce žánry klikněte na **rock (Rock** ) a podívejte se, jak byl **MessageService** vložen do zobrazení a načtena uvítací zpráva a obrázek. V tomto příkladu se zadáváme &quot;**Rock**&quot;:

    ![Úložiště hudby pro MVC – zobrazení injektáže](aspnet-mvc-4-dependency-injection/_static/image10.png "Úložiště hudby pro MVC – zobrazení injektáže")

    *Úložiště hudby pro MVC – zobrazení injektáže*
3. Zavřete prohlížeč.

<a id="Exercise3"></a>

<a id="Exercise_3_Injecting_Action_Filters"></a>
### <a name="exercise-3-injecting-action-filters"></a>Cvičení 3: vkládání filtrů akcí

V předchozích **filtrech vlastních akcí** testovacího prostředí jste pracovali s přizpůsobením a vkládáním filtrů. V tomto cvičení se naučíte, jak vložit filtry pomocí injektáže závislosti pomocí kontejneru Unity. Chcete-li to provést, přidejte do řešení úložiště hudby vlastní filtr akcí, který bude trasovat aktivitu tohoto webu.

<a id="Ex3Task1"></a>

<a id="Task_1_-_Including_the_Tracking_Filter_in_the_Solution"></a>
#### <a name="task-1---including-the-tracking-filter-in-the-solution"></a>Úkol 1 – včetně sledovacího filtru v řešení

V této úloze zahrnete do úložiště hudby vlastní filtr akcí, ve kterém se budou trasovat události. Vzhledem k tomu, že koncepty filtru vlastních akcí jsou již ošetřeny v předchozí laboratoři &quot;filtry vlastních akcí&quot;, do složky assets tohoto testovacího prostředí zahrnete pouze třídu Filter a pak vytvoříte zprostředkovatele filtru pro Unity:

1. Otevřete řešení **zahájit** ve složce **Filter\Begin akce Source\Ex03-vložení** . V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
      > 
      > Další informace najdete v tomto článku: [http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages](http://docs.nuget.org/docs/workflows/using-nuget-without-committing-packages).
2. Zahrnout soubor **TraceActionFilter.cs** z **/sources/assets** do složky **/Filters**

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample18.cs)]

    > [!NOTE]
    > Tento vlastní filtr akcí provádí trasování ASP.NET. Další informace najdete v &quot;ASP.NET na základě místní a dynamické filtry akcí MVC 4&quot; Lab.
3. Přidejte do projektu prázdnou třídu **FilterProvider.cs** ve složce **/filters.**
4. Přidejte obory názvů **System. Web. Mvc** a **Microsoft. Practices. Unity** v **FilterProvider.cs**.

    (Fragment kódu – *ASP.NET Dependency vstřiking Lab-Ex03-Filter Provider přidává obory názvů*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample19.cs)]
5. Nastavte třídu na dědění z rozhraní **IFilterProvider** .

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample20.cs)]
6. Přidejte vlastnost **IUnityContainer** do třídy **FilterProvider** a pak vytvořte konstruktor třídy pro přiřazení kontejneru.

    (Fragment kódu – *ASP.NET Dependency injektáže Labs – konstruktor zprostředkovatele filtru Ex03*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample21.cs)]

    > [!NOTE]
    > Konstruktor třídy poskytovatele filtru nevytváří **Nový** objekt uvnitř. Kontejner je předán jako parametr a závislost je vyřešena pomocí Unity.
7. Ve třídě **FilterProvider** Implementujte metody **GetFilters** z rozhraní **IFilterProvider** .

    (Fragment kódu – *ASP.NET Dependency vstřiking Lab-Ex03-Filter Provider GetFilters*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample22.cs)]

<a id="Ex3Task2"></a>

<a id="Task_2_-_Registering_and_Enabling_the_Filter"></a>
#### <a name="task-2---registering-and-enabling-the-filter"></a>Úloha 2 – registrace a povolení filtru

V této úloze povolíte sledování lokality. K tomu je třeba pro spuštění trasování zaregistrovat filtr v metodě **Bootstrapper.cs BuildUnityContainer** :

1. Otevřete soubor **Web. config** umístěný v kořenovém adresáři projektu a povolte sledování trasování v System. Web Group.

    [!code-xml[Main](aspnet-mvc-4-dependency-injection/samples/sample23.xml)]
2. Otevřete **Bootstrapper.cs** v kořenovém adresáři projektu.
3. Přidejte odkaz na obor názvů **MvcMusicStore. filters** .

    (Fragment kódu – *ASP.NET Dependency vstřiking Lab-Ex03-zaváděcí obory názvů*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample24.cs)]
4. Vyberte metodu **BuildUnityContainer** a zaregistrujte filtr v kontejneru Unity. Budete muset zaregistrovat poskytovatele filtru i filtr akcí.

    (Fragment kódu – *ASP.NET Dependency vstřiking Lab-Ex03-Register FilterProvider and ActionFilter*)

    [!code-csharp[Main](aspnet-mvc-4-dependency-injection/samples/sample25.cs)]

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>Úloha 3 – spuštění aplikace

V této úloze spustíte aplikaci a otestujete, že filtr vlastní akce trasování aktivity:

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. V nabídce žánry klikněte na **Rock** . Pokud chcete, můžete přejít na další žánry.

    ![Aplikace Music Store](aspnet-mvc-4-dependency-injection/_static/image11.png "Aplikace Music Store")

    *Aplikace Music Store*
3. Přejděte na **/Trace.axd** a zobrazte stránku trasování aplikace a pak klikněte na **Zobrazit podrobnosti**.

    ![Protokol trasování aplikace](aspnet-mvc-4-dependency-injection/_static/image12.png "Protokol trasování aplikace")

    *Protokol trasování aplikace*

    ![Trasování aplikace – Podrobnosti žádosti](aspnet-mvc-4-dependency-injection/_static/image13.png "Trasování aplikace – Podrobnosti žádosti")

    *Trasování aplikace – Podrobnosti žádosti*
4. Zavřete prohlížeč.

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>Souhrn

Vyplněním tohoto praktického cvičení jste zjistili, jak používat vkládání závislostí v ASP.NET MVC 4 integrací Unity pomocí balíčku NuGet. Pro dosažení tohoto účelu jste použili vkládání závislostí v řadičích, zobrazeních a filtrech akcí.

Byly pokryty následující koncepty:

- Funkce injektáže ASP.NET MVC 4 pro vkládání závislostí
- Integrace Unity pomocí balíčku NuGet. Mvc3 NuGet
- Vkládání závislostí v řadičích
- Vkládání závislostí v zobrazeních
- Vložení závislostí filtrů akcí

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Příloha A: instalace Visual Studio Express 2012 pro web

**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** . Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.

1. Přejděte do [ (Nastavení)https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169) (Integrace a služby). Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;<em>Visual Studio Express 2012 pro web pomocí sady Windows Azure SDK</em>&quot;.
2. Klikněte na **nainstalovat hned**. Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.
3. Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.

    ![Nainstalovat Visual Studio Express](aspnet-mvc-4-dependency-injection/_static/image14.png "Nainstalovat Visual Studio Express")

    *Nainstalovat Visual Studio Express*
4. Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**

    ![Přijetí licenčních podmínek](aspnet-mvc-4-dependency-injection/_static/image15.png)

    *Přijetí licenčních podmínek*
5. Počkejte na dokončení procesu stahování a instalace.

    ![Průběh instalace](aspnet-mvc-4-dependency-injection/_static/image16.png)

    *Průběh instalace*
6. Po dokončení instalace klikněte na **Dokončit**.

    ![Instalace dokončena](aspnet-mvc-4-dependency-injection/_static/image17.png)

    *Instalace dokončena*
7. Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.
8. Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .

    ![Dlaždice VS Express for Web](aspnet-mvc-4-dependency-injection/_static/image18.png)

    *Dlaždice VS Express for Web*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>Příloha B: použití fragmentů kódu

S fragmenty kódu máte veškerý kód, který potřebujete, na dosah ruky. Dokument testovacího prostředí vás přesně upozorní, když ho můžete používat, jak je znázorněno na následujícím obrázku.

![Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio](aspnet-mvc-4-dependency-injection/_static/image19.png "Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio")

*Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio*

***Přidání fragmentu kódu pomocí klávesnice (C# pouze)***

1. Umístěte kurzor na místo, kam chcete vložit kód.
2. Začněte psát název fragmentu (bez mezer a spojovníků).
3. Sledujte, jak IntelliSense zobrazuje stejné názvy fragmentů kódu.
4. Vyberte správný fragment kódu (nebo pokračujte v psaní, dokud není vybrán celý název tohoto fragmentu kódu).
5. Dvojím stisknutím klávesy TAB vložte fragment kódu do umístění kurzoru.

![Začněte psát název fragmentu.](aspnet-mvc-4-dependency-injection/_static/image20.png "Začněte psát název fragmentu.")

*Začněte psát název fragmentu.*

![Stisknutím klávesy TAB vyberte zvýrazněný fragment.](aspnet-mvc-4-dependency-injection/_static/image21.png "Stisknutím klávesy TAB vyberte zvýrazněný fragment.")

*Stisknutím klávesy TAB vyberte zvýrazněný fragment.*

![Stiskněte znovu TAB a fragment kódu se rozšíří.](aspnet-mvc-4-dependency-injection/_static/image22.png "Stiskněte znovu TAB a fragment kódu se rozšíří.")

*Stiskněte znovu TAB a fragment kódu se rozšíří.*

***Přidání fragmentu kódu pomocí myši (C#, Visual Basic a XML)*** první. Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.

1. Vyberte **Vložit fragment** a potom **Moje fragmenty kódu**.
2. Kliknutím na něj ze seznamu vyberte příslušný fragment kódu.

![Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.](aspnet-mvc-4-dependency-injection/_static/image23.png "Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.")

*Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.*

![Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.](aspnet-mvc-4-dependency-injection/_static/image24.png "Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.")

*Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.*

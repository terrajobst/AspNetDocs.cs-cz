---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: ASP.NET, formuláře a ověřování pro MVC 4 | Microsoft Docs
author: rick-anderson
description: V ASP.NET MVC 4 modelech a praktických testovacích prostředích pro přístup k datům jste načetli a zobrazili data z databáze. V této praktické laboratorní laboratoři přidáte do...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: 0e2605a4188eaf814f6ab0ebfeaabed4457bcfa3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539576"
---
# <a name="aspnet-mvc-4-helpers-forms-and-validation"></a>ASP.NET MVC 4 – pomocníci, formuláře a ověřování

podle [týmu webového Campy](https://twitter.com/webcamps)

[Stáhnout web Campy Training Kit](https://aka.ms/webcamps-training-kit)

V **ASP.NET MVC 4 modelech a** praktických testovacích prostředích pro přístup k datům jste načetli a zobrazili data z databáze. V tomto praktickém cvičení přidáte do aplikace **hudebního úložiště** možnost upravovat tato data.

Na základě tohoto cíle se nejprve vytvoří kontroler, který bude podporovat akce vytváření, čtení, aktualizace a odstranění (CRUD) alb. Vygenerujete šablonu zobrazení indexů s využitím funkce generování uživatelského rozhraní ASP.NET MVC k zobrazení vlastností alba v tabulce HTML. Chcete-li toto zobrazení vylepšit, přidejte vlastní nápovědu HTML, která bude zkrátit dlouhé popisy.

Následně přidáte zobrazení upravit a vytvořit, která vám umožní změnit alba v databázi pomocí prvků formuláře jako rozevíracích seznamů.

Nakonec umožníte uživatelům odstranit album a zároveň jim zabráníte v zadávání nesprávných dat, a to tak, že se budou ověřovat jejich vstupy.

Tato praktická cvičení předpokládá, že máte základní znalosti o **ASP.NET MVC**. Pokud jste ještě **ASP.NET MVC** nepoužívali, doporučujeme, abyste si převzali základní praktické prostředí pro **ASP.NET MVC** .

Toto testovací prostředí vás provede vylepšeními a novými funkcemi, které jsme dříve popsali pomocí menších změn ve vzorové webové aplikaci, která je součástí zdrojové složky.

> [!NOTE]
> Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici v [verzích Microsoft-Web/WebCampTrainingKit](https://aka.ms/webcamps-training-kit). Projekt, který je specifický pro toto testovací prostředí, je k dispozici na [ASP.NETch pomocníkech MVC 4, formulářích a ověřování](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation).

<a id="Objectives"></a>
### <a name="objectives"></a>Cíle

V této praktické laboratorní laboratoři se dozvíte, jak:

- Vytvoření kontroleru pro podporu operací CRUD
- Generování zobrazení indexu pro zobrazení vlastností entity v tabulce HTML
- Přidat vlastní nápovědu HTML
- Vytvoření a přizpůsobení zobrazení pro úpravy
- Rozlišit mezi metodami akce, které reagují na volání HTTP-GET nebo HTTP-POST
- Přidání a přizpůsobení zobrazení pro vytvoření
- Zpracování odstranění entity
- Ověření vstupu uživatele

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

Následující cvičení tvoří tuto praktickou laboratoř:

1. [Vytvoření kontroleru Správce úložiště a jeho zobrazení indexu](#Exercise1)
2. [Přidání pomocníka jazyka HTML](#Exercise2)
3. [Vytvoření zobrazení pro úpravy](#Exercise3)
4. [Přidání zobrazení pro vytvoření](#Exercise4)
5. [Odstraňování zpracování](#Exercise5)
6. [Přidání ověřování](#Exercise6)
7. [Použití nenápadu jQuery na straně klienta](#Exercise7)

> [!NOTE]
> Každé cvičení doprovází **koncovou** složku obsahující výsledné řešení, které byste měli získat po dokončení cvičení. Pokud potřebujete další nápovědu k práci prostřednictvím cvičení, můžete toto řešení použít jako vodítko.

Odhadovaný čas dokončení tohoto testovacího prostředí: **60 minut**

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a>Cvičení 1: vytvoření kontroleru Správce úložiště a jeho zobrazení indexu

V tomto cvičení se naučíte, jak vytvořit nový kontroler, který podporuje operace CRUD, přizpůsobení metody jeho akce index, která vrátí seznam alb z databáze a nakonec vygeneruje šablonu zobrazení indexu s využitím generování uživatelského rozhraní ASP.NET MVC. funkce pro zobrazení vlastností alba v tabulce HTML

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a>Úloha 1 – Vytvoření StoreManagerController

V této úloze vytvoříte nový kontroler s názvem **StoreManagerController** , který bude podporovat operace CRUD.

1. Otevřete řešení **zahájit** , které se nachází ve složce **source/EX1-CreatingTheStoreManagerController/Begin/** Folder.

   1. Než budete pokračovat, budete muset stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
2. Přidejte nový kontroler. Provedete to tak, že kliknete pravým tlačítkem myši na složku **Controllers** v rámci Průzkumník řešení, vyberete **Přidat** a pak příkaz **Controller** . Změňte název **kontroleru** na **StoreManagerController** a ujistěte se, že je vybraná možnost **kontroler MVC s prázdnými akcemi čtení/zápisu** . Klikněte na **Přidat**.

    ![Dialogové okno Přidat řadič](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "Dialogové okno Přidat řadič")

    *Dialogové okno Přidat řadič*

    Je vygenerována nová třída kontroleru. Vzhledem k tomu, že jste označili, že se mají přidat akce pro čtení a zápis, jsou pro ně běžné akce CRUD vytvořeny pomocí komentářů TODO, které jsou vyplněny, přičemž se zobrazí výzva k zahrnutí logiky specifické pro aplikaci

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a>Úloha 2 – přizpůsobení indexu StoreManager

V této úloze přizpůsobíte metodu akce indexu StoreManager, která vrátí zobrazení se seznamem alb z databáze.

1. Ve třídě StoreManagerController přidejte následující direktivy *using* .

    (Fragment kódu – *ASP.Nety pomocníka MVC 4 a formuláře a ověřování – EX1 s využitím MvcMusicStore*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. Přidejte do **StoreManagerController** pole pro uložení instance **MusicStoreEntities.**

    (Fragment kódu – *ASP.Nety pomocníka MVC 4 a formuláře a ověření – EX1 MusicStoreEntities*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. Implementujte akci indexu StoreManagerController, která vrátí zobrazení se seznamem alb.

    Logika akce kontroleru bude velmi podobná akci indexu StoreController, která byla zapsána dříve. Použijte LINQ k načtení všech alb, včetně informací o žánrech a interpretech k zobrazení.

    (Fragment kódu – *ASP.Nety pomocníka MVC 4 a formuláře a ověřování – EX1 StoreManagerController index*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a>Úloha 3 – Vytvoření zobrazení indexu

V této úloze vytvoříte šablonu zobrazení indexů, ve které se zobrazí seznam alb vrácených řadičem **StoreManager** .

1. Před vytvořením nové šablony zobrazení byste měli sestavit projekt tak, aby **dialog Přidat zobrazení** věděl o třídě **alba** , která se má použít. Vybrat **Build | Sestavte MvcMusicStore** a sestavte projekt.
2. Klikněte pravým tlačítkem myši do metody **index** Action a vyberte **Přidat zobrazení**. Tím se zobrazí dialogové okno **Přidat zobrazení** .

    ![Přidat zobrazení](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "Přidat zobrazení")

    *Přidání zobrazení v rámci metody index*
3. V dialogovém okně Přidat zobrazení ověřte, zda je název zobrazení **index**. Vyberte možnost **vytvořit zobrazení silného typu** a z rozevíracího seznamu **třída modelu** vyberte **album (MvcMusicStore. model)** . V rozevíracím seznamu **Šablona generování uživatelského rozhraní** vyberte možnost **seznam** . Ponechte **modul zobrazení** na **Razor** a ostatní pole s výchozí hodnotou a pak klikněte na **Přidat**.

    ![Přidání zobrazení indexu](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "Přidání zobrazení indexu")

    *Přidání zobrazení indexu*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a>Úloha 4 – přizpůsobení uživatelského rozhraní zobrazení indexu

V této úloze upravíte šablonu jednoduchého zobrazení vytvořenou funkcí generování uživatelského rozhraní ASP.NET MVC, aby se zobrazila pole, která chcete.

> [!NOTE]
> Podpora **generování uživatelského rozhraní** v rámci ASP.NET MVC generuje jednoduchou šablonu zobrazení, která obsahuje seznam všech polí v modelu alba. **Generování uživatelského rozhraní** poskytuje rychlý způsob, jak začít se zobrazením silného typu: místo ručního psaní šablony zobrazení, generování uživatelského rozhraní rychle vygeneruje výchozí šablonu a potom můžete vygenerovaný kód upravit.

1. Zkontrolujte vytvořený kód. Vygenerovaný seznam polí bude součástí následující tabulky HTML, kterou **generování uživatelského rozhraní** používá pro zobrazení tabulkových dat.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. Chcete-li zobrazit pouze pole **Žánr**, **umělec**, **název alba**a **ceny** , nahraďte **&lt;tabulku&gt;** kód následujícím kódem. Tím se odstraní sloupce **adresy URL pro obrázek** **AlbumId** a alba. Také změní sloupce GenreId a ArtistId tak, aby zobrazovaly vlastnosti propojené třídy **Artist.Name** a **Genre.Name**a odebraly odkaz **Podrobnosti** .

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. Změňte následující popisy.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>Úloha 5 – spuštění aplikace

V této úloze otestujete, že šablona zobrazení **indexu** StoreManager zobrazí seznam alb podle návrhu předchozích kroků.

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na domovské stránce. Změňte adresu URL na **/StoreManager** , abyste ověřili, že se zobrazuje seznam alb a zobrazuje jejich **název**, **Interpret** a **Žánr**.

    ![Procházení seznamu alb](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "Procházení seznamu alb")

    *Procházení seznamu alb*

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a>Cvičení 2: Přidání pomocníka HTML

Stránka indexu StoreManager má jeden potenciální problém: Vlastnosti názvu a jména umělce můžou být pro vyvolání formátování tabulky dostatečně dlouhé. V tomto cvičení se dozvíte, jak přidat vlastní pomůcku HTML pro zkracování tohoto textu.

Na následujícím obrázku vidíte, jak se upraví formát z důvodu délky textu při použití malého velikosti prohlížeče.

![Procházení seznamu alb s nezkráceným textem](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "Procházení seznamu alb s nezkráceným textem")

*Procházení seznamu alb s nezkráceným textem*

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a>Úloha 1 – rozšíření pomocné rutiny HTML

V této úloze přidáte novou metodu pro **oříznutí** objektu **HTML** vystaveného v zobrazeních ASP.NET MVC. Chcete-li to provést, implementujte **metodu rozšíření** do předdefinované třídy **System. Web. Mvc. HtmlHelper** , kterou poskytuje ASP.NET MVC.

> [!NOTE]
> Další informace o **metodách rozšíření**najdete v tomto článku na webu MSDN. [https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).

1. Otevřete řešení **zahájit** , které se nachází ve složce **source/EX2-AddingAnHTMLHelper/Begin/** Folder. V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
2. Otevřete zobrazení indexu StoreManager. Chcete-li to provést, v Průzkumník řešení rozbalte složku **zobrazení** , poté **StoreManager** a otevřete soubor **index. cshtml** .
3. Přidejte následující kód pod direktivu <strong>@model</strong> a definujte pomocnou metodu <strong>zkracování</strong> .

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a>Úkol 2 – zkracování textu na stránce

V této úloze použijete metodu **zkracování** ke zkrácení textu v šabloně zobrazení.

1. Otevřete zobrazení indexu StoreManager. Chcete-li to provést, v Průzkumník řešení rozbalte složku **zobrazení** , poté **StoreManager** a otevřete soubor **index. cshtml** .
2. Nahraďte řádky, které zobrazují **název interpreta** **a název alba.** Chcete-li to provést, nahraďte následující řádky.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>Úloha 3 – spuštění aplikace

V této úloze otestujete, že šablona zobrazení **indexu** StoreManager zkrátí název alba a jméno umělce.

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na domovské stránce. Změňte adresu URL na **/StoreManager** a ověřte, že dlouhé texty ve sloupci **název** a **Interpret** jsou zkrácené.

    ![Zkrácený název názvů a umělců](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "Zkrácený název názvů a umělců")

    *Zkrácený název názvů a umělců*

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a>Cvičení 3: Vytvoření zobrazení pro úpravy

V tomto cvičení se naučíte, jak vytvořit formulář, který správcům úložiště umožní upravovat album. Budou procházet adresu URL **/StoreManager/Edit/ID** (**ID** se jedná o jedinečné ID alba, které se má upravit), takže se k serveru vytvoří volání HTTP-GET.

Metoda akce úprav kontroleru načte příslušné album z databáze, vytvoří objekt **StoreManagerViewModel** , který ho zapouzdří (společně se seznamem umělců a žánrů), a pak ho předá do šablony zobrazení, kde se stránka HTML vykreslí zpátky uživateli. Tato stránka bude obsahovat **&gt;element&lt;formuláře** s textovým polem a rozevíracími seznamy pro úpravu vlastností alba.

Jakmile uživatel aktualizuje hodnoty formuláře alba a klikne na tlačítko **Uložit** , změny se odešlou prostřednictvím volání http-post zpět do **/StoreManager/Edit/ID**. I když adresa URL zůstává stejná jako při posledním volání, ASP.NET MVC zjistí, že je to HTTP-POST, a proto provede jinou metodu úprav akce (jedna dekorovaná s **[HTTPPOST]** ).

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a>Úloha 1 – implementace metody HTTP-GET Edit Action

V této úloze implementujete verzi HTTP-GET metody Edit Action pro načtení příslušného alba z databáze a také seznam všech žánrů a umělců. Bude tato data zabalit až do objektu **StoreManagerViewModel** definovaného v posledním kroku, který se pak předá do šablony zobrazení, ve které se odpověď vykreslí.

1. Otevřete řešení **zahájit** , které se nachází ve složce **source/EX3-CreatingTheEditView/Begin/** Folder. V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
2. Otevřete třídu **StoreManagerController** . Provedete to tak, že rozbalíte složku **Controllers** a dvakrát kliknete na **StoreManagerController.cs**.
3. Nahraďte metodu **HTTP-GET Edit** Action následujícím kódem k načtení vhodného **alba** a také seznamů **žánrů** a **umělců** .

    (Fragment kódu – *ASP.NET MVC 4 a formuláře a ověření – EX3 STOREMANAGERCONTROLLER HTTP-GET Action Edit*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > Používáte **System. Web. Mvc** **SelectList** pro interprety a žánry namísto seznamu **System. Collections. Generic** .
    > 
    > **SelectList** je čisticí způsob, jak naplnit rozevírací seznamy HTML a spravovat věci, jako je aktuální výběr. Vytvoření instance a pozdější nastavení těchto ViewModel objektů v akci kontroleru provede čistič scénářů pro úpravu formuláře.

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a>Úkol 2 – Vytvoření zobrazení pro úpravy

V této úloze vytvoříte šablonu zobrazení pro úpravy, která bude později zobrazovat vlastnosti alba.

1. Vytvořte zobrazení pro úpravy. Provedete to tak, že kliknete pravým tlačítkem myši do metody **Upravit** akci a vyberete **Přidat zobrazení**.
2. V dialogovém okně Přidat zobrazení ověřte, zda je název zobrazení **upraven**. Zaškrtněte políčko **vytvořit zobrazení silného typu** a v rozevíracím seznamu **Třída zobrazení dat** vyberte **album (MvcMusicStore. model)** . V rozevíracím seznamu **Šablona generování uživatelského rozhraní** vyberte **Upravit** . Ostatní pole ponechte výchozí hodnotou a pak klikněte na **Přidat**.

    ![Přidání zobrazení pro úpravy](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "Přidání zobrazení pro úpravy")

    *Přidání zobrazení pro úpravy*

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>Úloha 3 – spuštění aplikace

V této úloze otestujete, že na stránce pro **úpravu** zobrazení **StoreManager** se zobrazí hodnoty vlastností předaného alba jako parametr.

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na domovské stránce. Změňte adresu URL na **/StoreManager/Edit/1** a ověřte, že se zobrazí hodnoty vlastnosti pro předané album.

    ![Zobrazení úprav alba pro procházení](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "Zobrazení úprav alba pro procházení")

    *Zobrazení úprav alba pro procházení*

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a>Úloha 4 – implementace rozevíracích seznamu v šabloně editoru alba

V této úloze přidáte rozevírací seznam pro šablonu zobrazení vytvořenou v posledním úkolu, aby uživatel mohl vybírat ze seznamu umělců a žánrů.

1. Nahraďte celý kód sady polí **alba** následujícím kódem:

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > Pro vykreslení rozevíracího seznamu pro výběr umělců a žánrů byl přidán pomocník **HTML. DropDownList** . Parametry předané do **HTML. DropDownList** jsou:
    > 
    > 1. Název pole formuláře ( **&quot;ArtistId&quot;** ).
    > 2. **SelectList** hodnot rozevíracího seznamu.

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>Úloha 5 – spuštění aplikace

V této úloze otestujete, že stránka pro **úpravu** zobrazení StoreManager zobrazuje rozevírací seznam namísto textových polí umělec a Žánr ID.

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na domovské stránce. Změňte adresu URL na **/StoreManager/Edit/1** a ověřte tak, že se budou zobrazovat rozevírací nabídky místo textových polí jméno umělce a žánru.

    ![Procházení zobrazení pro úpravy alba pomocí rozevíracích seznamu](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "Procházení zobrazení pro úpravy alba pomocí rozevíracích seznamu")

    *Prohlížení zobrazení pro úpravy alba, tentokrát s rozevíracími seznamy*

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a>Úloha 6 – implementace metody akce HTTP-POST pro akci úprav

Teď, když se zobrazení pro úpravy zobrazuje podle očekávání, je nutné implementovat metodu akce HTTP-POST pro úpravy, aby se uložily změny provedené v albu.

1. V případě potřeby zavřete prohlížeč a vraťte se do okna sady Visual Studio. Otevřete **StoreManagerController** ze složky **Controllers** .
2. Nahraďte kód metody akce **http-post** pomocí následujícího postupu (Všimněte si, že metoda, která musí být nahrazena, je přetížená verze, která přijímá dva parametry):

    (Fragment kódu – *ASP.NET MVC 4 a formuláře a ověřování – EX3 STOREMANAGERCONTROLLER http-post Action Edit*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > Tato metoda se spustí, když uživatel klikne na tlačítko **Uložit** v zobrazení a provede http-post hodnoty formuláře zpátky na server, aby byly uchovány v databázi. Dekoratér **[HTTPPOST]** označuje, že metoda by měla být použita pro tyto scénáře http-post. Metoda přebírá objekt **alba** . ASP.NET MVC automaticky vytvoří objekt alba z publikovaných &lt;ových formulářů&gt; hodnot.
    > 
    > Metoda provede tyto kroky:
    > 
    > 1. Pokud je model platný:
    > 
    >     1. Aktualizujte záznam alba v kontextu tak, aby byl označen jako upravený objekt.
    >     2. Uloží změny a přesměruje zobrazení indexu.
    > 2. Pokud model není platný, naplní ViewBag pomocí **GenreId** a **ArtistId**, potom vrátí zobrazení s obdrženým objektem alba, aby uživatel mohl provést požadovanou aktualizaci.

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a>Úloha 7 – spuštění aplikace

V této úloze otestujete, že stránka pro **úpravu zobrazení StoreManager** ve skutečnosti ukládá aktualizovaná data alba v databázi.

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na domovské stránce. Změňte adresu URL na **/StoreManager/Edit/1**. Změňte název alba, který se má **načíst** , a klikněte na **Uložit**. Ověřte, že se název alba ve skutečnosti změnil v seznamu alb.

    ![Aktualizace alba](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "Aktualizace alba")

    *Aktualizace alba*

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a>Cvičení 4: Přidání zobrazení pro vytvoření

Teď, když **StoreManagerController** podporuje možnosti **úprav** , v tomto cvičení se dozvíte, jak přidat šablonu pro vytvoření zobrazení a umožnit tak správcům úložiště přidávat do aplikace nová alba.

Stejně jako u funkce úprav budete implementovat scénář vytváření pomocí dvou samostatných metod v rámci třídy **StoreManagerController** :

1. Jedna metoda akce zobrazí prázdný formulář, když Správci úložiště nejdřív navštíví adresu URL **/StoreManager/Create** .
2. Druhá metoda akce zpracuje scénář, ve kterém Správce úložiště klikne na tlačítko **Uložit** v rámci formuláře a pošle hodnoty zpátky do adresy URL **/StoreManager/Create** jako http-post.

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a>Úloha 1 – implementace metody akce HTTP-GET Create

V této úloze implementujete verzi HTTP-GET metody Create Action pro načtení seznamu všech žánrů a umělců, zabalit tato data do objektu **StoreManagerViewModel** , který pak bude předán do šablony zobrazení.

1. Otevřete řešení **zahájit** , které se nachází ve složce **source/Ex4-AddingACreateView/Begin/** Folder. V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
2. Otevřete třídu **StoreManagerController** . Provedete to tak, že rozbalíte složku **Controllers** a dvakrát kliknete na **StoreManagerController.cs**.
3. Kód metody **Create** Action nahraďte následujícím kódem:

    (Fragment kódu – *ASP.NET MVC 4 a formuláře a ověření – Ex4 STOREMANAGERCONTROLLER http – získat akci vytvořit*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a>Úkol 2 – Přidání zobrazení pro vytvoření

V této úloze přidáte šablonu pro vytvoření zobrazení, která zobrazí nové (prázdné) formuláře alba.

1. Klikněte pravým tlačítkem myši do metody **Create** Action a vyberte **Přidat zobrazení**. Tím se zobrazí dialogové okno Přidat zobrazení.
2. V dialogovém okně Přidat zobrazení ověřte, zda je název zobrazení **vytvořen**. Vyberte možnost **vytvořit zobrazení silného typu** a v rozevíracím seznamu **třída modelu** vyberte **album (MvcMusicStore. model)** a **vytvořte** z rozevíracího seznamu pro **šablonu generování uživatelského rozhraní** . Ostatní pole ponechte výchozí hodnotou a pak klikněte na **Přidat**.

    ![Přidání zobrazení pro vytvoření](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "Adding-a-Create-View. png")

    *Přidání zobrazení pro vytvoření*
3. Aktualizujte pole **GenreId** a **ArtistId** tak, aby používala rozevírací seznam, jak je znázorněno níže:

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a>Úloha 3 – spuštění aplikace

V této úloze otestujete, že se na stránce pro **Vytvoření** zobrazení **StoreManager** zobrazí prázdný formulář alba.

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na domovské stránce. Změňte adresu URL na **/StoreManager/Create**. Ověřte, že se zobrazí prázdný formulář pro vyplňování nových vlastností alba.

    ![Vytvořit zobrazení s prázdným formulářem](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "Vytvořit zobrazení s prázdným formulářem")

    *Vytvořit zobrazení s prázdným formulářem*

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a>Úloha 4 – implementace metody akce HTTP-POST

V této úloze implementujete verzi HTTP-POST metody Create Action, která bude vyvolána, když uživatel klikne na tlačítko **Uložit** . Metoda by měla uložit nové album v databázi.

1. V případě potřeby zavřete prohlížeč a vraťte se do okna sady Visual Studio. Otevřete třídu **StoreManagerController** . Provedete to tak, že rozbalíte složku **Controllers** a dvakrát kliknete na **StoreManagerController.cs**.
2. Nahraďte kód metody **http-post akce Create** následujícím způsobem:

    (Fragment kódu – *ASP.NETi a formuláře MVC 4 a ověřování – Ex4 STOREMANAGERCONTROLLER http-post Create Action*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > Akce vytvořit je poměrně podobná předchozí metodě úprav akce, ale místo nastavení objektu jako upraveného je přidána do kontextu.

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>Úloha 5 – spuštění aplikace

V této úloze otestujete, že stránka **StoreManager vytvořit** zobrazení vám umožní vytvořit nové album a pak přesměrovat do zobrazení indexu StoreManager.

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na domovské stránce. Změňte adresu URL na **/StoreManager/Create**. Vyplňte všechna pole formuláře daty nového alba, jako je například na následujícím obrázku:

    ![Vytvoření alba](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "Vytvoření alba")

    *Vytvoření alba*
3. Ověřte, že se přesměrujete na zobrazení indexu StoreManager, které obsahuje právě vytvořené nové album.

    ![Nové album vytvořeno](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "Nové album vytvořeno")

    *Nové album vytvořeno*

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a>Cvičení 5: zpracování odstranění

Možnost Odstranit alba ještě není naimplementovaná. To je to, co se týká tohoto cvičení. Stejně jako dřív budete implementovat scénář odstranění pomocí dvou samostatných metod v rámci třídy **StoreManagerController** :

1. Jedna metoda akce zobrazí potvrzovací formulář.
2. Druhá metoda akce zpracuje odeslání formuláře.

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a>Úloha 1 – implementace metody akce HTTP-GET DELETE

V této úloze implementujete verzi HTTP-GET metody akce DELETE pro načtení informací o albu.

1. Otevřete řešení **zahájit** , které se nachází ve složce **source/Ex5-HandlingDeletion/Begin/** Folder. V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
2. Otevřete třídu **StoreManagerController** . Provedete to tak, že rozbalíte složku **Controllers** a dvakrát kliknete na **StoreManagerController.cs**.
3. Akce Odstranit řadič je přesně stejná jako předchozí akce kontroleru podrobností úložiště: dotazuje objekt **alba** z databáze pomocí **ID** zadaného v adrese URL a vrátí odpovídající **zobrazení**. Uděláte to tak, že nahradíte kód metody akce HTTP-GET **Delete** následujícím způsobem:

    (Fragment kódu – *ASP.Nety pomocníka MVC 4 a formuláře a ověřování – odstranění Ex5 zpracování http-získat akci odstranit*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. Klikněte pravým tlačítkem myši do metody **Delete** Action a vyberte **Přidat zobrazení**. Tím se zobrazí dialogové okno Přidat zobrazení.
5. V dialogovém okně Přidat zobrazení ověřte, zda je název zobrazení **odstraněn**. Vyberte možnost **vytvořit zobrazení silného typu** a v rozevíracím seznamu **třída modelu** vyberte **album (MvcMusicStore. model)** . V rozevíracím seznamu **Šablona generování uživatelského rozhraní** vyberte **Odstranit** . Ostatní pole ponechte výchozí hodnotou a pak klikněte na **Přidat**.

    ![Přidání zobrazení pro odstranění](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "Přidání zobrazení pro odstranění")

    *Přidání zobrazení pro odstranění*
6. Šablona pro odstranění zobrazuje všechna pole z modelu. Zobrazí se pouze název alba. Chcete-li to provést, nahraďte obsah zobrazení následujícím kódem:

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>Úloha 2 – spuštění aplikace

V této úloze otestujete, že na stránce pro **odstranění** zobrazení **StoreManager** se zobrazí formulář pro odstranění potvrzení.

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na domovské stránce. Změňte adresu URL na **/StoreManager**. Vyberte jedno album, které chcete odstranit, kliknutím na **Odstranit** a ověřte, že se nové zobrazení nahraje.

    ![Odstranění alba](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "Odstranění alba")

    *Odstranění alba*

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a>Úloha 3 – implementace metody akce odstranění HTTP-POST

V této úloze budete implementovat verzi HTTP-POST metody akce odstranění, která bude vyvolána, když uživatel klikne na tlačítko **Odstranit** . Metoda by měla odstranit album v databázi.

1. V případě potřeby zavřete prohlížeč a vraťte se do okna sady Visual Studio. Otevřete třídu **StoreManagerController** . Provedete to tak, že rozbalíte složku **Controllers** a dvakrát kliknete na **StoreManagerController.cs**.
2. Nahraďte kód metody akce **odstranění http-post** následujícím způsobem:

    (Fragment kódu – *ASP.Nety pomocníka MVC 4 a formuláře a ověřování-Ex5 akce odstranění http-post*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>Úloha 4 – spuštění aplikace

V této úloze otestujete, že stránka zobrazení **StoreManager Delete** umožňuje odstranit album a pak přesměrovat do zobrazení indexu StoreManager.

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na domovské stránce. Změňte adresu URL na **/StoreManager**. Kliknutím na Odstranit vyberte jedno album, které chcete odstranit **.** Potvrďte odstranění kliknutím na tlačítko **Odstranit** :

    ![Odstranění alba](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "Odstranění alba")

    *Odstranění alba*
3. Ověřte, že se album odstranilo, protože se nezobrazuje na stránce **index** .

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a>Cvičení 6: Přidání ověřování

Formuláře pro vytváření a úpravy v současné době neprovádí žádný druh ověřování. Pokud uživatel ponechá požadované pole prázdné nebo zadá písmena v poli Cena, první chyba, kterou získáte, bude z databáze.

Do aplikace můžete přidat ověřování přidáním datových poznámek ke třídě modelu. Poznámky k datům umožňují popsat pravidla, která chcete použít pro vlastnosti modelu, a ASP.NET MVC se postará o vynucování a zobrazování příslušné zprávy pro uživatele.

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a>Úkol 1 – přidávání datových poznámek

V této úloze přidáte datové poznámky k modelu alba, ve kterém se v případě potřeby zobrazí zpráva pro vytvoření a úpravu stránky pro ověření.

Pro jednoduchou třídu modelu je přidání datové poznámky zpracováváno pouhým přidáním příkazu **using** pro **System. ComponentModel. DataAnnotation**a následným umístěním atributu **[required]** na příslušné vlastnosti. V následujícím příkladu by vlastnost **Name** měla požadované pole v zobrazení.

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

Toto je trochu složitější v případech, jako je tato aplikace, kde je vygenerována model EDM (Entity Data Model). Pokud jste poznámky k datům přidali přímo do tříd modelu, budou přepsány při aktualizaci modelu z databáze. Místo toho můžete použít částečné třídy metadat, které budou existovat pro uchování poznámek a jsou přidruženy ke třídám modelu pomocí atributu **[MetadataType]** .

1. Otevřete řešení **zahájit** , které se nachází ve složce **source/Ex6-AddingValidation/Begin/** Folder. V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
2. Otevřete **album.cs** ze složky **modely** .
3. Nahraďte obsah **album.cs** zvýrazněným kódem, aby vypadal jako následující:

    > [!NOTE]
    > Řádek **[DisplayFormat (ConvertEmptyStringToNull = false)]** označuje, že prázdné řetězce z modelu nebudou převedeny na hodnotu null, pokud je datové pole aktualizováno ve zdroji dat. Toto nastavení vyloučí výjimku, pokud Entity Framework přiřadí hodnoty null k modelu před tím, než datová Poznámka ověří pole.

    (Fragment kódu – *ASP.Nety pomocníka MVC 4 a formuláře a ověření – částečná třída metadat alba Ex6*)

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > Tato částečná třída **alba** má atribut **MetadataType** , který odkazuje na třídu **AlbumMetaData** pro datové poznámky. Jedná se o některé z atributů anotace dat, které používáte k přidání poznámky k modelu alba:
    > 
    > - Required – označuje, že vlastnost je povinné pole.
    > - DisplayName – definuje text, který se má použít u polí formuláře a ověřovacích zpráv.
    > - DisplayFormat – určuje způsob zobrazení a formátování datových polí.
    > - StringLength – definuje maximální délku pole řetězce.
    > - Rozsah – poskytuje maximální a minimální hodnotu pro číselné pole.
    > - ScaffoldColumn – umožňuje skrývání polí z formulářů editoru.

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>Úloha 2 – spuštění aplikace

V této úloze otestujete, že stránky pro vytváření a úpravy ověřují pole pomocí zobrazovaných názvů vybraných v posledním úkolu.

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na domovské stránce. Změňte adresu URL na **/StoreManager/Create**. Ověřte, že zobrazované názvy odpovídají těm v částečné třídě (jako je **Adresa URL obrázku alba** místo **AlbumArtUrl**).
3. Klikněte na **vytvořit**, aniž byste museli vyplnit formulář. Ověřte, že se zobrazí odpovídající ověřovací zprávy.

    ![Ověřená pole na stránce vytvořit](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "Ověřená pole na stránce vytvořit")

    *Ověřená pole na stránce vytvořit*
4. Můžete ověřit, že se na stránce pro **Úpravy** dojde k stejnému. Změňte adresu URL na **/StoreManager/Edit/1** a ověřte, že zobrazované názvy odpovídají těm, které jsou v částečné třídě (jako je **Adresa URL alba alba** místo **AlbumArtUrl**). Vyprázdněte pole **název** a **Ceník** a klikněte na **Uložit**. Ověřte, že se zobrazí odpovídající ověřovací zprávy.

    ![Ověřená pole na stránce pro úpravy](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    *Ověřená pole na stránce pro úpravy*

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a>Cvičení 7: použití nenápadu jQuery na straně klienta

V tomto cvičení se dozvíte, jak povolit MVC 4 s nenáročném ověřování jQuery na straně klienta.

> [!NOTE]
> Nezpůsobuje, že jQuery používá JavaScript s předponou data-AJAX k vyvolání metod akce na serveru místo rušivého vygenerování vložených klientských skriptů.

<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a>Úloha 1 – spuštění aplikace před tím, než se aktivuje nenáročná jQuery

V této úloze spustíte aplikaci před tím, než zadáte jQuery, aby bylo možné porovnat oba modely ověřování.

1. Otevřete řešení **zahájit** , které se nachází ve složce **source/Ex7-UnobtrusivejQueryValidation/Begin/** Folder. V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
2. Stisknutím klávesy **F5** spusťte aplikaci.
3. Projekt se spustí na domovské stránce. Přejděte na **/StoreManager/Create** a klikněte na **vytvořit** bez vyplnění formuláře, abyste ověřili, že se zobrazí ověřovací zprávy:

    ![Ověřování klienta zakázáno](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "Ověřování klienta zakázáno")

    *Ověřování klienta zakázáno*
4. V prohlížeči otevřete zdrojový kód HTML:

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a>Úloha 2 – povolení nenáročného ověřování klienta

V této úloze povolíte v souboru **Web. config** , který je ve výchozím nastavení nastavené na hodnotu false, v každém novém projektu ASP.NET MVC 4 možnost jQuery neztratí **ověření klienta** . Kromě toho přidáte potřebné odkazy na skripty, aby jQuery nenápadně fungovalo ověřování klienta.

1. Otevřete soubor **Web. config** v kořenovém adresáři projektu a ujistěte se, že hodnoty klíčů **ClientValidationEnabled** a **UnobtrusiveJavaScriptEnabled** jsou nastaveny na **hodnotu true**.

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > Můžete také povolit ověřování klientů pomocí kódu na Global.asax.cs a získat tak stejné výsledky:
    > 
    > **HtmlHelper. ClientValidationEnabled = true;**
    > 
    > Kromě toho můžete přiřadit atribut ClientValidationEnabled do libovolného kontroleru a mít tak vlastní chování.
2. Otevřete **vytvořit. cshtml** na adrese **Views\StoreManager**.
3. Zajistěte, aby se v zobrazení odkazovaly na následující soubory skriptu **jQuery. Validate** a **jQuery. Validate.** nepřehledy prostřednictvím &quot; **~/Bundles/jqueryval**&quot; sady.

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > Všechny tyto knihovny jQuery jsou zahrnuté v nových projektech MVC 4. Další knihovny můžete najít ve složce **/Scripts** v projektu.
    > 
    > Aby bylo možné tyto knihovny ověřování fungovat, je třeba přidat odkaz na knihovnu jQuery Framework. Vzhledem k tomu, že tento odkaz již byl přidán do souboru **\_layout. cshtml** , není nutné jej přidávat do tohoto konkrétního zobrazení.

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a>Úloha 3 – spuštění aplikace pomocí nenápadu ověření jQuery

V této úloze otestujete, že šablona zobrazení **StoreManager** Create View provádí ověřování na straně klienta pomocí knihoven jQuery, když uživatel vytvoří nové album.

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na domovské stránce. Přejděte na **/StoreManager/Create** a klikněte na **vytvořit** bez vyplnění formuláře, abyste ověřili, že se zobrazí ověřovací zprávy:

    ![Ověření klienta s povoleným jQuery](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "Ověření klienta s povoleným jQuery")

    *Ověření klienta s povoleným jQuery*
3. V prohlížeči otevřete zdrojový kód pro vytvoření zobrazení:

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

   > [!NOTE]
   > U každého pravidla ověření klienta přidá příkaz jQuery atribut s data-Val-*rule*=&quot;&quot;*zprávy* . Níže je uveden seznam značek, které nenápadí vložení jQuery do pole vstupu HTML k provedení ověření klienta:
   > 
   > - Data – Val
   > - Data-Val-Number
   > - Data-Val-Range
   > - Data-Val-Range-min/data-Val-Range-max
   > - Data-Val – povinné
   > - Data-Val-Length
   > - Data-Val-Length-Max/data-Val-Length-min.
   > 
   > Všechny hodnoty dat jsou vyplněny pomocí **poznámky k datům**modelu. Veškerá logika, která funguje na straně serveru, se pak dá spustit na straně klienta. Například atribut Price má v modelu následující anotaci dat:
   > 
   > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
   > 
   > Po použití nenápadu jQuery je vygenerovaný kód:
   > 
   > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>Souhrn

Díky tomuto praktickému cvičení jste se dozvěděli, jak uživatelům umožnit změnu dat uložených v databázi s použitím následujícího postupu:

- Akce kontroleru, jako je index, vytvořit, upravit, odstranit
- Funkce generování uživatelského rozhraní MVC pro ASP.NET pro zobrazení vlastností v tabulce HTML
- Vlastní pomocníky HTML pro zlepšení uživatelského prostředí
- Metody akcí, které reagují na volání HTTP-GET nebo HTTP-POST
- Šablona sdíleného editoru pro podobné šablony zobrazení, jako je vytváření a úpravy
- Formuláře, jako jsou rozevírací prvky
- Datové poznámky pro ověřování modelu
- Ověřování na straně klienta pomocí knihovny jQuery – nenáročná knihovna

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Příloha A: instalace Visual Studio Express 2012 pro web

**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** . Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.

1. Přejít na [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169). Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;<em>Visual Studio Express 2012 pro web pomocí sady Windows Azure SDK</em>&quot;.
2. Klikněte na **nainstalovat hned**. Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.
3. Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.

    ![Nainstalovat Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Nainstalovat Visual Studio Express")

    *Nainstalovat Visual Studio Express*
4. Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**

    ![Přijetí licenčních podmínek](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    *Přijetí licenčních podmínek*
5. Počkejte na dokončení procesu stahování a instalace.

    ![Průběh instalace](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    *Průběh instalace*
6. Po dokončení instalace klikněte na **Dokončit**.

    ![Instalace dokončena](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    *Instalace dokončena*
7. Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.
8. Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .

    ![Dlaždice VS Express for Web](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    *Dlaždice VS Express for Web*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>Příloha B: použití fragmentů kódu

S fragmenty kódu máte veškerý kód, který potřebujete, na dosah ruky. Dokument testovacího prostředí vás přesně upozorní, když ho můžete používat, jak je znázorněno na následujícím obrázku.

![Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio")

*Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio*

***Přidání fragmentu kódu pomocí klávesnice (C# pouze)***

1. Umístěte kurzor na místo, kam chcete vložit kód.
2. Začněte psát název fragmentu (bez mezer a spojovníků).
3. Sledujte, jak IntelliSense zobrazuje stejné názvy fragmentů kódu.
4. Vyberte správný fragment kódu (nebo pokračujte v psaní, dokud není vybrán celý název tohoto fragmentu kódu).
5. Dvojím stisknutím klávesy TAB vložte fragment kódu do umístění kurzoru.

![Začněte psát název fragmentu.](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "Začněte psát název fragmentu.")

*Začněte psát název fragmentu.*

![Stisknutím klávesy TAB vyberte zvýrazněný fragment.](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Stisknutím klávesy TAB vyberte zvýrazněný fragment.")

*Stisknutím klávesy TAB vyberte zvýrazněný fragment.*

![Stiskněte znovu TAB a fragment kódu se rozšíří.](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "Stiskněte znovu TAB a fragment kódu se rozšíří.")

*Stiskněte znovu TAB a fragment kódu se rozšíří.*

***Přidání fragmentu kódu pomocí myši (C#, Visual Basic a XML)*** první. Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.

1. Vyberte **Vložit fragment** a potom **Moje fragmenty kódu**.
2. Kliknutím na něj ze seznamu vyberte příslušný fragment kódu.

![Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.")

*Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.*

![Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.")

*Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.*

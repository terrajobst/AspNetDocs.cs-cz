---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
title: ASP.NET MVC 4 Entity Framework generování a migrace | Microsoft Docs
author: rick-anderson
description: Pokud jste obeznámeni s metodami kontroleru ASP.NET MVC 4 nebo jste dokončili &quot;pomocníky, formuláře a ověřování&quot; praktické cvičení, měli byste si být vědomi...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 093c1362-f10b-407c-a708-be370f4b62b0
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
msc.type: authoredcontent
ms.openlocfilehash: 2b26224390af70e19ca0593abe93a6867140f8ab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598901"
---
# <a name="aspnet-mvc-4-entity-framework-scaffolding-and-migrations"></a>ASP.NET MVC 4 – generování uživatelského rozhraní a migrace sady Entity Framework

podle [týmu webového Campy](https://twitter.com/webcamps)

[Stáhnout web Campy Training Kit](https://aka.ms/webcamps-training-kit)

Pokud jste obeznámeni s metodami kontroleru ASP.NET MVC 4 nebo jste dokončili &quot;pomocníky, formuláře a ověřování&quot; praktických cvičeních, měli byste si uvědomit, že mnohé z logiky, jak vytvořit, aktualizovat, vypsat a odebrat jakoukoli entitu dat, se v rámci aplikace opakují. Nezmiňujete si, že pokud má váš model několik tříd pro manipulaci, budete pravděpodobně strávit značnou dobu psaní příspěvku a metody GET pro každou entitu a také pro každé zobrazení.

V tomto testovacím prostředí se naučíte, jak pomocí rozhraní ASP.NET MVC 4 automaticky vygenerovat základní hodnoty pro CRUD vaší aplikace (vytvoření, čtení, aktualizace a odstranění). Od jednoduché třídy modelu a, bez psaní jednoho řádku kódu, vytvoříte kontroler, který bude obsahovat všechny operace CRUD, a také všechna potřebná zobrazení. Po sestavení a spuštění jednoduchého řešení budete mít vytvořenou databázi aplikace společně s logikou a zobrazeními MVC pro manipulaci s daty.

Kromě toho se dozvíte, jak snadné je použít Entity Framework migrace k provádění aktualizací modelů v celé aplikaci. Entity Framework migrace vám umožní upravit databázi poté, co se model změnil pomocí jednoduchých kroků. Díky všem těmto výhodám budete moct vytvářet a udržovat webové aplikace efektivněji a využívat nejnovější funkce ASP.NET MVC 4.

> [!NOTE]
> Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Training Kit, která je dostupná v [verzích Microsoft-Web/WebCampTrainingKit](https://aka.ms/webcamps-training-kit). Projekt, který je specifický pro toto testovací prostředí, je k dispozici na [ASP.NET MVC 4 Entity Framework generování a migrace](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations).

<a id="Objectives"></a>
### <a name="objectives"></a>Cíle

V této praktické laboratorní laboratoři se dozvíte, jak:

- Použijte generování ASP.NET pro operace CRUD v řadičích.
- Změňte databázový model pomocí Entity Framework migrace.

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

1. [Použití generování ASP.NET MVC 4 s Entity Framework migracemi](#Exercise1)

> [!NOTE]
> K tomuto cvičení doprovázíme **koncovou** složku obsahující výsledné řešení, které byste měli získat po dokončení cvičení. Pokud potřebujete další nápovědu k práci prostřednictvím tohoto cvičení, můžete toto řešení použít jako vodítko.

Odhadovaný čas dokončení tohoto testovacího prostředí: **30 minut**

<a id="Exercise1"></a>

<a id="Exercise_1_Using_ASPNET_MVC_4_Scaffolding_with_Entity_Framework_Migrations"></a>
### <a name="exercise-1-using-aspnet-mvc-4-scaffolding-with-entity-framework-migrations"></a>Cvičení 1: použití generování ASP.NET MVC 4 s Entity Framework migrací

Generování ASP.NET MVC poskytuje rychlý způsob, jak generovat operace CRUD standardizovaným způsobem, a vytvořit tak potřebnou logiku, která vaší aplikaci umožní pracovat s databázovou vrstvou.

V tomto cvičení se dozvíte, jak používat generování ASP.NET MVC 4 s kódem jako první k vytvoření metod CRUD. Pak se naučíte, jak aktualizovat model pomocí změn v databázi pomocí Entity Framework migrace.

<a id="Ex1Task1"></a>

<a id="Task_1-_Creating_a_new_ASPNET_MVC_4_project_using_Scaffolding"></a>
#### <a name="task-1--creating-a-new-aspnet-mvc-4-project-using-scaffolding"></a>Úloha 1 – Vytvoření nového projektu ASP.NET MVC 4 pomocí generování uživatelského rozhraní

1. Pokud ještě není otevřený, spusťte **Visual Studio 2012**.
2. Vybrat **soubor | Nový projekt**. V dialogovém okně Nový projekt v části **vizuál C# |** V části Web vyberte **webová aplikace ASP.NET MVC 4**. Pojmenujte projekt **MVC4andEFMigrations** a nastavte umístění na složku **Source\Ex1-UsingMVC4ScaffoldingEFMigrations** v tomto testovacím prostředí. Nastavte **název řešení** na **zahájit** a ověřte, že je zaškrtnuté políčko **vytvořit adresář pro řešení** . Klikněte na tlačítko **OK**.

    ![Nový projekt ASP.NET MVC 4 – dialogové okno](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "Nový projekt ASP.NET MVC 4 – dialogové okno")

    *Nový projekt ASP.NET MVC 4 – dialogové okno*
3. V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte šablonu **Internetová aplikace** a ujistěte se, že je v nástroji **Razor** vybraný **modul zobrazení**. Projekt vytvoříte kliknutím na **OK**.

    ![Nová ASP.NET MVC 4 Internet Application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "Nová ASP.NET MVC 4 Internet Application")

    *Nová ASP.NET MVC 4 Internet Application*
4. V Průzkumník řešení klikněte pravým tlačítkem na **modely** a vyberte **Přidat | Třída** pro vytvoření jednoduché třídy Person (POCO). Pojmenujte **ji a** klikněte na tlačítko **OK**.
5. Otevřete třídu Person a vložte následující vlastnosti.

    (Fragment kódu – *ASP.NET MVC 4 a migrace Entity Framework – vlastnosti osoby EX1*)

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample1.cs)]
6. Klikněte na **sestavit | Sestavte řešení** a uložte změny a sestavte projekt.

    ![Sestavování aplikace](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "Sestavování aplikace")

    *Sestavování aplikace*
7. V Průzkumník řešení klikněte pravým tlačítkem na složku řadiče a vyberte **Přidat | Kontroler**.
8. Pojmenujte kontrolér *PersonController* a dokončete **Možnosti generování uživatelského rozhraní** s následujícími hodnotami.

   1. V rozevíracím seznamu **Šablona** vyberte **kontroler MVC s akcemi čtení/zápisu a zobrazeními pomocí Entity Framework** možnost.
   2. V rozevíracím seznamu **třída modelu** vyberte třídu **Person** .
   3. V seznamu **Třída kontextu dat** vyberte **&lt;nový kontext dat...&gt;** . Vyberte libovolný název a klikněte na **OK**.
   4. V rozevíracím seznamu **zobrazení** ověřte, zda je vybrána možnost **Razor** .

      ![Přidání kontroleru osob s generováním uživatelského rozhraní](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "Přidání kontroleru osob s generováním uživatelského rozhraní")

      *Přidání kontroleru osob s generováním uživatelského rozhraní*
9. Kliknutím na **Přidat** vytvořte nový kontroler pro osobu s vytvářením uživatelského rozhraní. Nyní jste vygenerovali akce kontroleru a také zobrazení.

    ![Po vytvoření kontroleru osoba pomocí generování uživatelského rozhraní](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "Po vytvoření kontroleru osoba pomocí generování uživatelského rozhraní")

    *Po vytvoření kontroleru osoba pomocí generování uživatelského rozhraní*
10. Otevřete třídu **PersonController** . Všimněte si, že všechny metody akce CRUD byly vygenerovány automaticky.

   ![Uvnitř kontroleru osob](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "Uvnitř kontroleru osob")

   *Uvnitř kontroleru osob*

<a id="Ex1Task2"></a>

<a id="Task_2-_Running_the_application"></a>
#### <a name="task-2--running-the-application"></a>Úloha 2 – spuštění aplikace

V tomto okamžiku databáze ještě není vytvořená. V této úloze budete aplikaci spouštět poprvé a otestujete operace CRUD. Databáze se vytvoří průběžně s Code First.

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. V prohlížeči přidejte **/Person** k adrese URL pro otevření stránky osoba.

    ![První spuštění aplikace](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "První spuštění aplikace")

    *Aplikace: první spuštění*
3. Teď budete zkoumat stránky osob a testovat operace CRUD.

    1. Kliknutím na **vytvořit novou** přidejte novou osobu. Zadejte jméno a příjmení a klikněte na **vytvořit**.

        ![Přidává se nová osoba.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "Přidává se nová osoba.")

        *Přidává se nová osoba.*
    2. V seznamu osoby můžete odstranit, upravit nebo přidat položky.

        ![Seznam osob](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "Seznam osob")

        *Seznam osob*
    3. Kliknutím na **Podrobnosti** otevřete podrobnosti o osobě.

        ![Podrobnosti o osobě](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "Podrobnosti o osobě")

        *Podrobnosti o osobě*
4. Zavřete prohlížeč a vraťte se do sady Visual Studio. Všimněte si, že jste vytvořili celou CRUD pro entitu Person v rámci vaší aplikace – z modelu do zobrazení – nemusíte psát jediný řádek kódu!

<a id="Ex1Task3"></a>

<a id="Task_3-_Updating_the_database_using_Entity_Framework_Migrations"></a>
#### <a name="task-3--updating-the-database-using-entity-framework-migrations"></a>Úloha 3 – aktualizace databáze pomocí Entity Framework migrace

V této úloze provedete aktualizaci databáze pomocí Entity Framework migrace. Zjistíte, jak snadné je změnit model a odrážet změny v databázích pomocí funkce Entity Framework migrace.

1. Otevřete konzolu Správce balíčků. Vyberte **nástroje** > **správce balíčků NuGet** > **konzole správce balíčků**.
2. V konzole správce balíčků zadejte následující příkaz:

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample2.ps1)]

    ![Povolování migrací](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "Povolování migrací")

    *Povolování migrací*

    Příkaz Enable-Migration vytvoří složku **migraces** , která obsahuje skript pro inicializaci databáze.

    ![Složka migrace](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "Složka migrace")

    *Složka migrace*
3. Otevřete soubor **Configuration.cs** ve složce migraces. Vyhledejte konstruktor třídy a změňte hodnotu **AutomaticMigrationsEnabled** na *true*.

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample3.cs)]
4. Otevřete třídu Person a přidejte atribut pro prostřední jméno osoby. Pomocí tohoto nového atributu měníte model.

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample4.cs)]
5. Vybrat **Build |** Sestavte řešení v nabídce a sestavte aplikaci.

    ![Sestavování aplikace](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "Sestavování aplikace")

    *Sestavování aplikace*
6. V konzole správce balíčků zadejte následující příkaz:

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample5.ps1)]

    Tento příkaz bude hledat změny v datových objektech a následně přidá potřebné příkazy pro úpravu databáze.

    ![Přidání druhého jména](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "Přidání druhého jména")

    *Přidání druhého jména*
7. Volitelné Spuštěním následujícího příkazu můžete vygenerovat skript SQL s rozdílovou aktualizací. To vám umožní ručně aktualizovat databázi (v tomto případě není nutné), nebo použít změny v jiných databázích:

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample6.ps1)]

    ![Generování skriptu SQL](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "Generování skriptu SQL")

    *Generování skriptu SQL*

    ![Aktualizace skriptu SQL](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "Aktualizace skriptu SQL")

    *Aktualizace skriptu SQL*
8. V konzole správce balíčků zadejte následující příkaz pro aktualizaci databáze:

    PMC

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample7.ps1)]

    ![Aktualizace databáze](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "Aktualizace databáze")

    *Aktualizace databáze*

    Tím se do tabulky **lidé** přidá sloupec **MiddleName** , který bude odpovídat aktuální definici třídy **Person** .
9. Po aktualizaci databáze klikněte pravým tlačítkem na složku kontroleru a vyberte **Přidat | Kontroler** pro přidání řadiče pro fyzickou osobu (dokončeno se stejnými hodnotami) Tím se aktualizují existující metody a zobrazení přidáním nového atributu.

    ![Přidání aktualizace kontroleru](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "Přidání aktualizace kontroleru")

    *Aktualizace kontroleru*
10. Klikněte na **Přidat**. Pak vyberte hodnoty **přepsat PersonController.cs** a **přepsat přidružená zobrazení** a klikněte na **OK**.

   ![Přidání ovladače přepsání](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image19.png)

   *Aktualizace kontroleru*

<a id="Ex1Task4"></a>

<a id="Task4-_Running_the_application"></a>
#### <a name="task4--running-the-application"></a>Task4 – spuštění aplikace

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Otevřete **/Person**. Všimněte si, že data byla zachována, zatímco byl přidán sloupec prostřední název.

    ![Druhé jméno přidané](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "Druhé jméno přidané")

    *Druhé jméno přidané*
3. Pokud kliknete na **Upravit**, budete moct k aktuální osobě přidat prostřední jméno.

    ![Střední název edice](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "Střední název edice")

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>Souhrn

V tomto praktickém cvičení jste se dozvěděli o jednoduchých krocích pro vytváření operací CRUD s ASP.NETm generováním uživatelského rozhraní MVC 4 pomocí libovolné třídy modelu. Pak jste se naučili, jak provést kompletní aktualizaci ve vaší aplikaci – z databáze do zobrazení – pomocí Entity Framework migrace.

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Příloha A: instalace Visual Studio Express 2012 pro web

**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** . Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.

1. Přejděte do [ (Nastavení)https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169) (Integrace a služby). Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;<em>Visual Studio Express 2012 pro web pomocí sady Windows Azure SDK</em>&quot;.
2. Klikněte na **nainstalovat hned**. Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.
3. Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.

    ![Nainstalovat Visual Studio Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Nainstalovat Visual Studio Express")

    *Nainstalovat Visual Studio Express*
4. Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**

    ![Přijetí licenčních podmínek](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image23.png)

    *Přijetí licenčních podmínek*
5. Počkejte na dokončení procesu stahování a instalace.

    ![Průběh instalace](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image24.png)

    *Průběh instalace*
6. Po dokončení instalace klikněte na **Dokončit**.

    ![Instalace dokončena](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image25.png)

    *Instalace dokončena*
7. Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.
8. Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .

    ![Dlaždice VS Express for Web](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image26.png)

    *Dlaždice VS Express for Web*

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a>Příloha B: použití fragmentů kódu

S fragmenty kódu máte veškerý kód, který potřebujete, na dosah ruky. Dokument testovacího prostředí vás přesně upozorní, když ho můžete používat, jak je znázorněno na následujícím obrázku.

![Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio")

*Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio*

***Přidání fragmentu kódu pomocí klávesnice (C# pouze)***

1. Umístěte kurzor na místo, kam chcete vložit kód.
2. Začněte psát název fragmentu (bez mezer a spojovníků).
3. Sledujte, jak IntelliSense zobrazuje stejné názvy fragmentů kódu.
4. Vyberte správný fragment kódu (nebo pokračujte v psaní, dokud není vybrán celý název tohoto fragmentu kódu).
5. Dvojím stisknutím klávesy TAB vložte fragment kódu do umístění kurzoru.

![Začněte psát název fragmentu.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "Začněte psát název fragmentu.")

*Začněte psát název fragmentu.*

![Stisknutím klávesy TAB vyberte zvýrazněný fragment.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Stisknutím klávesy TAB vyberte zvýrazněný fragment.")

*Stisknutím klávesy TAB vyberte zvýrazněný fragment.*

![Stiskněte znovu TAB a fragment kódu se rozšíří.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "Stiskněte znovu TAB a fragment kódu se rozšíří.")

*Stiskněte znovu TAB a fragment kódu se rozšíří.*

***Přidání fragmentu kódu pomocí myši (C#, Visual Basic a XML)*** první. Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.

1. Vyberte **Vložit fragment** a potom **Moje fragmenty kódu**.
2. Kliknutím na něj ze seznamu vyberte příslušný fragment kódu.

![Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.")

*Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.*

![Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.")

*Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.*

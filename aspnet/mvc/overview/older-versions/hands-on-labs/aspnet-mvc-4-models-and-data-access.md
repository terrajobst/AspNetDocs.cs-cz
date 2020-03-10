---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: ASP.NET MVC 4 – modely a přístup k datům | Microsoft Docs
author: rick-anderson
description: 'Poznámka: Toto praktické cvičení předpokládá, že máte základní znalosti o ASP.NET MVC. Pokud jste ještě ASP.NET MVC nepoužívali, doporučujeme, abyste přešli na ASP.NET MVC 4...'
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: 90635b617930d0a9c126795f4c8790d542e33dc9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78560198"
---
# <a name="aspnet-mvc-4-models-and-data-access"></a>ASP.NET MVC 4 – modely a přístup k datům

podle [týmu webového Campy](https://twitter.com/webcamps)

[Stáhnout web Campy Training Kit](https://aka.ms/webcamps-training-kit)

Tato praktická cvičení předpokládá, že máte základní znalosti o **ASP.NET MVC**. Pokud jste ještě **ASP.NET MVC** nepoužívali, doporučujeme, abyste si převzali v praxi **ASP.NET MVC 4** pro praktické cvičení.

Toto testovací prostředí vás provede vylepšeními a novými funkcemi, které jsme dříve popsali pomocí menších změn ve vzorové webové aplikaci, která je součástí zdrojové složky.

> [!NOTE]
> Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici v [verzích Microsoft-Web/WebCampTrainingKit](https://aka.ms/webcamps-training-kit). Projekt, který je specifický pro toto testovací prostředí, je k dispozici na [ASP.NET modelech MVC 4 a přístup k datům](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess).

V **ASP.NET MVC** se praktická praktická cvičení předáváte pevně zakódovaným datům z řadičů do šablon zobrazení. Pro vytvoření reálné webové aplikace ale můžete chtít použít skutečnou databázi.

Tato praktická cvičení vám ukáže, jak používat databázový stroj, aby bylo možné ukládat a načítat data potřebná pro aplikaci pro hudební úložiště. K tomu je potřeba začít s existující databází a vytvořit z ní model EDM (Entity Data Model). V rámci tohoto testovacího prostředí budete splňovat **Database First** přístup a také **Code First** přístup.

Můžete ale také použít **model First** přístup, vytvořit stejný model pomocí nástrojů a pak z něj vygenerovat databázi.

![Database First vs. Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. Model First")

*Database First vs. Model First*

Po vygenerování modelu provedete v StoreController správné úpravy, abyste poskytovali zobrazení ze Storu s daty potřebnými z databáze namísto použití pevně zakódovaných dat. Nebudete muset dělat žádné změny v šablonách zobrazení, protože StoreController vrátí stejný ViewModels k šablonám zobrazení, i když to bude čas od databáze pocházet.

**Code First přístup**

Code First přístup nám umožňuje definovat model z kódu bez generování tříd, které jsou obecně spojeny s rozhraním.

V kódu nejprve objekty modelu jsou definovány s POCOs, &quot;é obyčejné staré objekty CLR&quot;. POCOs jsou jednoduché jednoduché třídy, které nemají žádnou dědičnost a neimplementují rozhraní. Z nich můžeme automaticky vygenerovat databázi nebo můžeme použít stávající databázi a vytvořit mapování třídy z kódu.

Výhodami použití tohoto přístupu je, že model zůstává nezávisle na rozhraní Persistence (v tomto případě Entity Framework), protože třídy POCOs nejsou spojeny s rozhraním Mapping Framework.

> [!NOTE]
> Toto testovací prostředí vychází z ASP.NET MVC 4 a verze ukázkové aplikace pro hudební úložiště, která je přizpůsobená a minimalizovaná tak, aby odpovídala pouze funkcím uvedeným v tomto praktickém testovacím prostředí.
> 
> Pokud si chcete projít celou výukovou aplikaci pro **obchod s hudbou** , najdete ji v [MVC – hudba-Store](https://github.com/evilDave/MVC-Music-Store).

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

1. [Cvičení 1: Přidání databáze](#Exercise1)
2. [Cvičení 2: vytvoření databáze pomocí Code First](#Exercise2)
3. [Cvičení 3: dotazování databáze s parametry](#Exercise3)

> [!NOTE]
> Každé cvičení doprovází **koncovou** složku obsahující výsledné řešení, které byste měli získat po dokončení cvičení. Pokud potřebujete další nápovědu k práci prostřednictvím cvičení, můžete toto řešení použít jako vodítko.

Odhadovaný čas dokončení tohoto testovacího prostředí: **35 minut**.

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a>Cvičení 1: Přidání databáze

V tomto cvičení se dozvíte, jak do řešení přidat databázi s tabulkami aplikace MusicStore, aby se mohla využívat jejich data. Jakmile je databáze generována s modelem a přidána do řešení, upravíte třídu StoreController, aby poskytovala šablonu zobrazení s daty z databáze namísto použití pevně zakódovaných hodnot.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a>Úloha 1 – Přidání databáze

V této úloze přidáte již vytvořenou databázi s hlavními tabulkami aplikace MusicStore do řešení.

1. Otevřete řešení **zahájit** , které se nachází ve složce **source/EX1-AddingADatabaseDBFirst/Begin/** Folder.

   1. Než budete pokračovat, budete muset stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
2. Přidat soubor databáze **MvcMusicStore** V tomto praktickém testovacím prostředí budete používat už vytvořenou databázi s názvem **MvcMusicStore. mdf**. Provedete to tak, že kliknete pravým tlačítkem na složku **Data\_aplikace** , přejdete na **Přidat** a potom kliknete na **existující položka**. Přejděte na **\Source\Assets** a vyberte soubor **MvcMusicStore. mdf** .

    ![Přidání existující položky](aspnet-mvc-4-models-and-data-access/_static/image2.png "Přidání existující položky")

    *Přidání existující položky*

    ![Soubor databáze MvcMusicStore. mdf](aspnet-mvc-4-models-and-data-access/_static/image3.png "Soubor databáze MvcMusicStore. mdf")

    *Soubor databáze MvcMusicStore. mdf*

    Databáze byla přidána do projektu. I v případě, že se databáze nachází v řešení, můžete ji dotazovat a aktualizovat, protože byla hostována na jiném databázovém serveru.

    ![Databáze MvcMusicStore v Průzkumník řešení](aspnet-mvc-4-models-and-data-access/_static/image4.png "Databáze MvcMusicStore v Průzkumník řešení")

    *Databáze MvcMusicStore v Průzkumník řešení*
3. Ověřte připojení k databázi. Chcete-li to provést, dvakrát klikněte na **MvcMusicStore. mdf** pro navázání připojení.

    ![Připojování k MvcMusicStore. mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "Připojování k MvcMusicStore. mdf")

    *Připojování k MvcMusicStore. mdf*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a>Úloha 2 – Vytvoření datového modelu

V této úloze vytvoříte datový model, který bude pracovat s databází přidanou v předchozí úloze.

1. Vytvořte datový model, který bude představovat databázi. Chcete-li to provést, klikněte v Průzkumník řešení pravým tlačítkem myši na složku **modely** , přejděte na **Přidat** a klikněte na **Nová položka**. V dialogovém okně **Přidat novou položku** vyberte šablonu **dat** a pak položku **ADO.NET model EDM (Entity Data Model)** . Změňte název datového modelu na **StoreDB. edmx** a klikněte na **Přidat**.

    ![Přidání model EDM (Entity Data Model) StoreDB ADO.NET](aspnet-mvc-4-models-and-data-access/_static/image6.png "Přidání model EDM (Entity Data Model) StoreDB ADO.NET")

    *Přidání model EDM (Entity Data Model) StoreDB ADO.NET*
2. Zobrazí se **průvodce model EDM (Entity Data Model)** . Tento průvodce vás provede vytvořením vrstvy modelu. Vzhledem k tomu, že se model má vytvořit na základě nedávno přidané existující databáze, vyberte **Generovat z databáze** a klikněte na **Další**.

    ![Výběr obsahu modelu](aspnet-mvc-4-models-and-data-access/_static/image7.png "Výběr obsahu modelu")

    *Výběr obsahu modelu*
3. Vzhledem k tomu, že generujete model z databáze, budete muset zadat připojení, které se má použít. Klikněte na **nové připojení**.
4. Vyberte **Microsoft SQL Server soubor databáze** a klikněte na **pokračovat**.

    ![Zvolit zdroj dat](aspnet-mvc-4-models-and-data-access/_static/image8.png "Zvolit zdroj dat")

    *Dialog zvolit zdroj dat*
5. Klikněte na **Procházet** a vyberte databázi **MvcMusicStore. mdf** umístěnou ve složce **App\_data** a klikněte na **OK**.

    ![Vlastnosti připojení](aspnet-mvc-4-models-and-data-access/_static/image9.png "Vlastnosti připojení")

    *Vlastnosti připojení*
6. Vygenerovaná třída by měla mít stejný název jako připojovací řetězec entity, proto změňte její název na **MusicStoreEntities** a klikněte na **Další**.

    ![Výběr datového připojení](aspnet-mvc-4-models-and-data-access/_static/image10.png "Výběr datového připojení")

    *Výběr datového připojení*
7. Vyberte databázové objekty, které chcete použít. Protože model entity bude používat pouze tabulky databáze, vyberte možnost **tabulky** a ujistěte se, že jsou vybrány také **sloupce zahrnout cizí klíče v modelu** a **doplnit jednotné nebo množné číslo vygenerované názvy objektů** . Změňte obor názvů modelu na **MvcMusicStore. model** a klikněte na **Dokončit**.

    ![Výběr databázových objektů](aspnet-mvc-4-models-and-data-access/_static/image11.png "Výběr databázových objektů")

    *Výběr databázových objektů*

    > [!NOTE]
    > Pokud se zobrazí dialogové okno upozornění zabezpečení, kliknutím na tlačítko **OK** spusťte šablonu a vygenerujte třídy pro entity modelu.
8. Bude se zobrazovat diagram entit pro databázi, zatímco bude vytvořena samostatná třída, která mapuje každou tabulku na databázi. Například tabulka **alba** bude reprezentovaná třídou **alba** , kde každý sloupec v tabulce se namapuje na vlastnost třídy. To vám umožní dotazovat se na objekty, které reprezentují řádky v databázi, a pracovat s nimi.

    ![Diagram entit](aspnet-mvc-4-models-and-data-access/_static/image12.png "Diagram entit")

    *Diagram entit*

    > [!NOTE]
    > Šablony T4 (. TT) spouštějí kód pro generování tříd entit a přepíše existující třídy se stejným názvem. V tomto příkladu třídy &quot;alba&quot;, &quot;Žánr&quot; a &quot;umělec&quot; byly přepsány generovaným kódem.

<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a>Úloha 3 – sestavování aplikace

V této úloze zkontrolujete, že i když generování modelu odebralo třídy **alba**, **žánru** a **interpretu** , sestavení projektu bylo úspěšné pomocí nových tříd datového modelu.

1. Sestavte projekt výběrem položky nabídky **sestavení** a poté **Sestavte MvcMusicStore**.

    ![Sestavení projektu](aspnet-mvc-4-models-and-data-access/_static/image13.png "Sestavení projektu")

    *Sestavení projektu*
2. Sestavení projektu bylo úspěšné. Proč to pořád funguje? Tento postup funguje, protože tabulky databáze obsahují pole obsahující vlastnosti, které jste použili v **albu** a **žánru**odebraných tříd.

    ![Sestavení byla úspěšná](aspnet-mvc-4-models-and-data-access/_static/image14.png "Sestavení byla úspěšná")

    *Sestavení byla úspěšná*
3. Zatímco Návrhář zobrazuje entity ve formátu diagramu, jsou ve skutečnosti C# třídy. Rozbalte uzel **StoreDB. edmx** v Průzkumník řešení a potom **StoreDB.TT**se zobrazí nové vygenerované entity.

    ![Generované soubory](aspnet-mvc-4-models-and-data-access/_static/image15.png "Generované soubory")

    *Generované soubory*

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a>Úloha 4 – dotazování databáze

V této úloze aktualizujete třídu StoreController tak, aby namísto použití dat pevně zakódované se dotazoval na databázi, aby se načetly informace.

1. Otevřete **Controllers\StoreController.cs** a přidejte do třídy následující pole pro uložení instance třídy **MusicStoreEntities** s názvem **storeDB**:

    (Fragment kódu – *modely a přístup k datům – EX1 storeDB*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. Třída **MusicStoreEntities** zpřístupňuje vlastnost kolekce pro každou tabulku v databázi. Aktualizujte metodu akce **procházení** a načtěte Žánr se všemi **alba**.

    (Fragment kódu – *modely a přístup k datům – EX1 Store – procházení*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > Používáte funkci rozhraní .NET s názvem **LINQ** (jazykově integrovaný dotaz) k zápisu výrazů dotazů silně typovaného na tyto kolekce – což spustí kód pro databázi a vrátí objekty, pro které lze programovat.
    > 
    > Další informace o LINQ najdete na [webu MSDN](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx).
3. Aktualizujte metodu akce **indexu** , aby se načetly všechny žánry.

    (Fragment kódu – *modely a přístup k datům – index úložiště EX1*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. Aktualizujte metodu akce **indexu** pro načtení všech žánrů a transformaci kolekce na seznam.

    (Fragment kódu – *modely a přístup k datům – EX1 Store GenreMenu*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>Úloha 5 – spuštění aplikace

V této úloze zkontrolujete, že se na stránce index úložiště nyní zobrazí žánry uložené v databázi místo pevně zakódované. Nemusíte měnit šablonu zobrazení, protože **StoreController** vrací stejné entity jako předtím, i když data pocházejí z databáze.

1. Znovu sestavte řešení a stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na domovské stránce. Ověřte, že nabídka **žánrů** již není seznam pevně zakódované a data jsou přímo načtena z databáze.

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    *Procházení žánrů z databáze*
3. Teď přejděte na libovolný Žánr a ověřte, jestli jsou alba naplněná z databáze.

    ![Procházení alb z databáze](aspnet-mvc-4-models-and-data-access/_static/image17.png "Procházení alb z databáze")

    *Procházení alb z databáze*

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a>Cvičení 2: vytvoření databáze pomocí Code First

V tomto cvičení se naučíte, jak pomocí Code Firstho přístupu vytvořit databázi s tabulkami aplikace MusicStore a jak přistupovat k datům.

Po vygenerování modelu upravíte StoreController tak, aby poskytoval šablonu zobrazení s daty vytvořenými z databáze namísto použití hodnot pevně zakódované.

> [!NOTE]
> Pokud jste dokončili cvičení 1 a již jste pracovali s přístupem Database First, nyní se dozvíte, jak získat stejné výsledky s jiným procesem. Úkoly společné s cvičením 1 byly označeny pro usnadnění čtení. Pokud jste nedokončili cvičení 1, ale chtěli byste se naučit Code Firstý přístup, můžete začít z tohoto cvičení a získat úplné pokrytí tématu.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a>Úloha 1 – vyplnění ukázkových dat

V této úloze naplníte databázi ukázkovými daty při jejím prvním vytvoření pomocí kódu.

1. Otevřete řešení **zahájit** , které se nachází ve složce **source/EX2-CreatingADatabaseCodeFirst/Begin/** Folder. V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
2. Přidejte soubor **sampleData.cs** do složky **modely** . Provedete to tak, že kliknete pravým tlačítkem na složku **modely** , najeďte na **Přidat** a potom kliknete na **existující položka**. Přejděte na **\Source\Assets** a vyberte soubor **sampleData.cs** .

    ![Kód pro vyplnění ukázkových dat](aspnet-mvc-4-models-and-data-access/_static/image18.png "Kód pro vyplnění ukázkových dat")

    *Kód pro vyplnění ukázkových dat*
3. Otevřete soubor **Global.asax.cs** a přidejte následující příkazy *using* .

    (Fragment kódu – *modely a přístup k datům – EX2 Global asax používá*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. V metodě **aplikace\_Start ()** přidejte následující řádek pro nastavení inicializátoru databáze.

    (Fragment kódu – *modely a přístup k datům – EX2 Global asax SetInitializer*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a>Úloha 2 – konfigurace připojení k databázi

Teď, když jste již přidali databázi do našeho projektu, budete do souboru **Web. config** napsáni připojovacím řetězcem.

1. Přidat připojovací řetězec do **souboru Web. config**. Provedete to tak, že otevřete soubor **Web. config** v kořenovém adresáři projektu a nahradíte připojovací řetězec s názvem DefaultConnection tímto řádkem v části **&lt;connectionStrings&gt;** oddíl:

    ![Umístění souboru Web. config](aspnet-mvc-4-models-and-data-access/_static/image19.png "Umístění souboru Web. config")

    *Umístění souboru Web. config*

    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a>Úloha 3 – práce s modelem

Teď, když už máte nakonfigurované připojení k databázi, propojíte model s databázovými tabulkami. V této úloze vytvoříte třídu, která bude propojena s databází pomocí Code First. Mějte na paměti, že existuje existující třída modelu POCO, která by se měla upravovat.

> [!NOTE]
> Pokud jste dokončili cvičení 1, poznamenejte si, že tento krok byl proveden průvodcem. Tím, že provádíte Code First, ručně vytvoříte třídy, které budou propojeny s datovými entitami.

1. Otevřete **Žánr** třídy modelu POCO ze složky projektu **modelů** a zahrňte ID. Použijte vlastnost int s názvem **GenreId**.

    (Fragment kódu – *modely a přístup k datům – Ex2 Code First Žánr*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > Chcete-li pracovat s konvencemi Code First, musí mít Žánr třídy vlastnost primárního klíče, která bude automaticky rozpoznána.
    > 
    > Další informace o konvencích pro Code First najdete v tomto [článku na webu MSDN](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx).
2. Nyní otevřete **album** třídy modelu POCO ze složky projekt **modelů** a zahrňte cizí klíče a vytvořte vlastnosti s názvy **GenreId** a **ArtistId**. Tato třída již má **GenreId** pro primární klíč.

    (Fragment kódu – *modely a přístup k datům – Ex2 Code First alba*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. Otevřete **Interpret** třídy modelu POCO a zahrňte vlastnost **ArtistId** .

    (Fragment kódu – *modely a přístup k datům – Ex2 Code First Interpret*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. Klikněte pravým tlačítkem na složku projekt **modelů** a vyberte **Přidat | Třída**. Název souboru **MusicStoreEntities.cs**. Pak klikněte na tlačítko **Přidat.**

    ![Přidání třídy](aspnet-mvc-4-models-and-data-access/_static/image20.png "Přidání třídy")

    *Přidání nové položky*

    ![Přidání Class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "Přidání Class2")

    *Přidání třídy*
5. Otevřete třídu, kterou jste právě vytvořili, **MusicStoreEntities.cs**a vložte obory názvů **System. data. entity** a **System. data. entity. Infrastructure**.

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. Nahraďte deklaraci třídy za účelem rozšiřování třídy **DbContext** : deklarujte veřejnou **negenerickými** a přepište metodu **OnModelCreating** . Po provedení tohoto kroku získáte doménovou třídu, která bude propojit váš model s Entity Framework. Aby to bylo možné, nahraďte kód třídy následujícím kódem:

    (Fragment kódu – *modely a přístup k datům – Ex2 Code First MusicStoreEntities*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

> [!NOTE]
> Pomocí Entity Framework **DbContext** a **negenerickými** budete moci zadat dotaz na Žánr třídy POCO. Rozšířením metody **OnModelCreating** zadáte v **kódu** , jak bude Žánr mapován na databázovou tabulku. Další informace o DBContext a Negenerickými najdete v tomto článku na webu MSDN: [odkaz](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a>Úloha 4 – dotazování databáze

V této úloze aktualizujete třídu StoreController tak, aby namísto použití dat pevně zakódované se načetla z databáze.

> [!NOTE]
> Tato úloha je společná s cvičením 1.
> 
> Pokud jste dokončili cvičení 1, Všimněte si, že tyto kroky jsou stejné v obou případech (první databáze nebo kód Code First). Liší se v tom, jak jsou data propojena s modelem, ale přístup k datovým entitám je z kontroleru transparentní.

1. Otevřete **Controllers\StoreController.cs** a přidejte do třídy následující pole pro uložení instance třídy **MusicStoreEntities** s názvem **storeDB**:

    (Fragment kódu – *modely a přístup k datům – EX1 storeDB*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. Třída **MusicStoreEntities** zpřístupňuje vlastnost kolekce pro každou tabulku v databázi. Aktualizujte metodu akce **procházení** a načtěte Žánr se všemi **alba**.

    (Fragment kódu – *modely a přístup k datům – EX2 Store – procházení*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > Používáte funkci rozhraní .NET s názvem **LINQ** (jazykově integrovaný dotaz) k zápisu výrazů dotazů silně typovaného na tyto kolekce – což spustí kód pro databázi a vrátí objekty, pro které lze programovat.
    > 
    > Další informace o LINQ najdete na [webu MSDN](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx).
3. Aktualizujte metodu akce **indexu** , aby se načetly všechny žánry.

    (Fragment kódu – *modely a přístup k datům – index úložiště EX2*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. Aktualizujte metodu akce **indexu** pro načtení všech žánrů a transformaci kolekce na seznam.

    (Fragment kódu – *modely a přístup k datům – EX2 Store GenreMenu*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a>Úloha 5 – spuštění aplikace

V této úloze zkontrolujete, že se na stránce index úložiště nyní zobrazí žánry uložené v databázi místo pevně zakódované. Nemusíte měnit šablonu zobrazení, protože **StoreController** vrací stejný **StoreIndexViewModel** jako předtím, ale tentokrát se data podávají z databáze.

1. Znovu sestavte řešení a stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na domovské stránce. Ověřte, že nabídka **žánrů** již není seznam pevně zakódované a data jsou přímo načtena z databáze.

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    *Procházení žánrů z databáze*
3. Teď přejděte na libovolný Žánr a ověřte, jestli jsou alba naplněná z databáze.

    ![Procházení alb z databáze](aspnet-mvc-4-models-and-data-access/_static/image23.png "Procházení alb z databáze")

    *Procházení alb z databáze*

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a>Cvičení 3: dotazování databáze s parametry

V tomto cvičení se dozvíte, jak zadat dotaz na databázi pomocí parametrů a jak používat tvarování výsledků dotazů, což je funkce, která snižuje počet přístupů k databázi tím, že efektivněji získává data.

> [!NOTE]
> Další informace o tvarování výsledků dotazů najdete v následujícím [článku na webu MSDN](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx).

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a>Úloha 1 – Změna StoreController, aby se načetly alba z databáze

V této úloze změníte třídu **StoreController** pro přístup k databázi, aby se načetla alba z konkrétního žánru.

1. Otevřete řešení **, které se nachází** ve složce **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin** , pokud chcete použít přístup k prvnímu kódu nebo složku **Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin** , pokud chcete použít přístup k databázi. V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
2. Otevřete třídu **StoreController** a změňte metodu akce **procházení** . Provedete to tak, že v **Průzkumník řešení**rozbalíte složku **Controllers (řadiče** ) a dvakrát kliknete na **StoreController.cs**.
3. Chcete-li načíst alba pro určitý Žánr, změňte metodu akce **procházení** . Chcete-li to provést, nahraďte následující kód:

    (Fragment kódu – *modely a přístup k datům – EX3 StoreController BrowseMethod*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

> [!NOTE]
> Chcete-li naplnit kolekci entity, je nutné použít metodu **include** k určení, že chcete načíst alba. Můžete použít. Rozšíření **Single ()** v jazyce LINQ, protože v tomto případě je pro album očekáván pouze jeden Žánr. Metoda **Single ()** bere výraz lambda jako parametr, což v tomto případě Určuje jeden objekt žánru, který má název shodný s definovanou hodnotou.
> 
> Budete využívat funkci, která vám umožní označit další související entity, které chcete načíst, i když je objekt žánru načten. Tato funkce se nazývá **tvarování výsledků dotazů**a umožňuje snížit počet potřebných přístupů k databázi a získat informace. V tomto scénáři budete chtít předem načíst alba pro žánr, který načtete.
> 
> Dotaz obsahuje **žánry. zahrnout (&quot;alba&quot;)** k indikaci, že chcete také související alba. Výsledkem bude efektivnější aplikace, protože data o žánrech a albech budou načtena v jedné databázi.

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a>Úloha 2 – spuštění aplikace

V této úloze spustíte aplikaci a načtete alba konkrétního žánru z databáze.

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na domovské stránce. Chcete-li ověřit, zda jsou výsledky z databáze načítány, změňte adresu URL na **/Store/Browse? Žánr = pop** .

    ![Procházení podle žánru](aspnet-mvc-4-models-and-data-access/_static/image24.png "Procházení podle žánru")

    *Prochází se/Store/Browse? Žánr = pop*

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a>Úloha 3 – přístup k albu podle ID

V této úloze zopakujete předchozí postup, abyste získali alba podle jejich ID.

1. V případě potřeby zavřete prohlížeč a vraťte se do sady Visual Studio. Otevřete třídu **StoreController** a změňte metodu akce **Details** . Provedete to tak, že v **Průzkumník řešení**rozbalíte složku **Controllers (řadiče** ) a dvakrát kliknete na **StoreController.cs**.
2. Změňte metodu akce **Details** , aby se načetly informace o albu na základě jejich **ID**. Chcete-li to provést, nahraďte následující kód:

    (Fragment kódu – *modely a přístup k datům – EX3 StoreController DetailsMethod*)

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a>Úloha 4 – spuštění aplikace

V této úloze spustíte aplikaci ve webovém prohlížeči a získáte podrobnosti o albu podle jejich ID.

1. Stisknutím klávesy **F5** spusťte aplikaci.
2. Projekt se spustí na domovské stránce. Změňte adresu URL tak, aby **/Store/Details/51** nebo procházela žánry, a vyberte album, abyste ověřili, že se výsledky načítají z databáze.

    ![Podrobnosti o procházení](aspnet-mvc-4-models-and-data-access/_static/image25.png "Podrobnosti o procházení")

    *Procházení/Store/Details/51*

> [!NOTE]
> Kromě toho můžete tuto aplikaci nasadit na weby Windows Azure podle [dodatku B: publikování aplikace ASP.NET MVC 4 pomocí nasazení webu](#AppendixB).

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>Souhrn

Po absolvování tohoto praktického cvičení se naučíte základy modelů ASP.NET MVC a přístup k datům, a to pomocí **Database First** přístupu a **Code First** přístupu:

- Postup přidání databáze do řešení za účelem využití svých dat
- Postup aktualizace řadičů k poskytnutí šablon zobrazení s daty z databáze místo pevně zakódovaného kódu
- Postup dotazování databáze pomocí parametrů
- Jak používat tvarování výsledků dotazu, funkci, která snižuje počet přístupů k databázím a efektivnější načítání dat
- Jak použít Database First a Code First přístupy v Microsoft Entity Framework k propojení databáze s modelem

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Příloha A: instalace Visual Studio Express 2012 pro web

**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** . Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.

1. Přejít na [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169). Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;<em>Visual Studio Express 2012 pro web pomocí sady Windows Azure SDK</em>&quot;.
2. Klikněte na **nainstalovat hned**. Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.
3. Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.

    ![Nainstalovat Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "Nainstalovat Visual Studio Express")

    *Nainstalovat Visual Studio Express*
4. Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**

    ![Přijetí licenčních podmínek](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    *Přijetí licenčních podmínek*
5. Počkejte na dokončení procesu stahování a instalace.

    ![Průběh instalace](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    *Průběh instalace*
6. Po dokončení instalace klikněte na **Dokončit**.

    ![Instalace dokončena](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    *Instalace dokončena*
7. Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.
8. Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .

    ![Dlaždice VS Express for Web](aspnet-mvc-4-models-and-data-access/_static/image30.png)

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

    ![Přihlaste se k Windows Azure Portal](aspnet-mvc-4-models-and-data-access/_static/image31.png "Přihlaste se k Windows Azure Portal")

    *Přihlášení k Windows Azure Portál pro správu*
2. Na panelu příkazů klikněte na **Nový** .

    ![Vytvoření nového webu](aspnet-mvc-4-models-and-data-access/_static/image32.png "Vytvoření nového webu")

    *Vytvoření nového webu*
3. Klikněte na **compute** | **Web**. Pak vyberte možnost **rychlé vytvoření** . Zadejte dostupnou adresu URL pro nový web a klikněte na **vytvořit web**.

    > [!NOTE]
    > Web Windows Azure je hostitelem webové aplikace běžící v cloudu, kterou můžete řídit a spravovat. Možnost rychle vytvořit umožňuje nasadit dokončenou webovou aplikaci do webu Windows Azure z oblasti mimo portál. Nezahrnuje kroky pro nastavení databáze.

    ![Vytvoření nového webu pomocí rychlého vytvoření](aspnet-mvc-4-models-and-data-access/_static/image33.png "Vytvoření nového webu pomocí rychlého vytvoření")

    *Vytvoření nového webu pomocí rychlého vytvoření*
4. Počkejte, než se nový **Web** vytvoří.
5. Po vytvoření webu klikněte na odkaz ve sloupci **Adresa URL** . Ověřte, zda nový web funguje.

    ![Procházení na nový web](aspnet-mvc-4-models-and-data-access/_static/image34.png "Procházení na nový web")

    *Procházení na nový web*

    ![Běžící Web](aspnet-mvc-4-models-and-data-access/_static/image35.png "Běžící Web")

    *Běžící Web*
6. Vraťte se na portál a kliknutím na název webu pod sloupcem **název** zobrazíte stránky pro správu.

    ![Otevření stránek správy webu](aspnet-mvc-4-models-and-data-access/_static/image36.png "Otevření stránek správy webu")

    *Otevření stránek správy webu*
7. Na stránce **řídicí panel** klikněte v části **rychlý přehled** na odkaz **Stáhnout profil publikování** .

    > [!NOTE]
    > *Profil publikování* obsahuje všechny informace potřebné k publikování webové aplikace na webu Windows Azure pro každou povolenou metodu publikace. Profil publikování obsahuje adresy URL, přihlašovací údaje uživatele a databázové řetězce potřebné k připojení a ověření proti jednotlivým koncovým bodům, pro které je povolena metoda publikace. **Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** a **Microsoft Visual Studio 2012** podporují čtení profilů publikování pro automatizaci konfigurace těchto programů pro publikování webových aplikací na webech Windows Azure.

    ![Stahuje se publikační profil webu.](aspnet-mvc-4-models-and-data-access/_static/image37.png "Stahuje se publikační profil webu.")

    *Stahuje se publikační profil webu.*
8. Stáhněte si soubor profilu publikování do známého umístění. V tomto cvičení se dozvíte, jak tento soubor použít k publikování webové aplikace na webech Windows Azure ze sady Visual Studio.

    ![Ukládání souboru profilu publikování](aspnet-mvc-4-models-and-data-access/_static/image38.png "Ukládá se publikační profil.")

    *Ukládání souboru profilu publikování*

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>Úloha 2 – Konfigurace databázového serveru

Pokud vaše aplikace využívá SQL Server databází, budete muset vytvořit SQL Database Server. Pokud chcete nasadit jednoduchou aplikaci, která nepoužívá SQL Server, můžete tuto úlohu přeskočit.

1. Pro uložení aplikační databáze budete potřebovat server SQL Database. SQL Database servery můžete zobrazit z předplatného na portálu pro správu Windows Azure na stránce **databáze SQL** | **serverech** | **řídicím panelu serveru**. Pokud nemáte vytvořený server, můžete ho vytvořit pomocí tlačítka **Přidat** na panelu příkazů. Poznamenejte si **název serveru a adresu URL, přihlašovací jméno a heslo správce**, jak je budete používat v dalších úlohách. Databázi ještě nevytvářejte, protože bude vytvořená v pozdější fázi.

    ![Řídicí panel serveru SQL Database](aspnet-mvc-4-models-and-data-access/_static/image39.png "Řídicí panel serveru SQL Database")

    *Řídicí panel serveru SQL Database*
2. V další úloze budete testovat připojení k databázi ze sady Visual Studio, z tohoto důvodu je třeba zahrnout místní IP adresu do seznamu **povolených IP adres**serveru. Chcete-li to provést, klikněte na tlačítko **Konfigurovat**, vyberte IP adresu z **aktuální IP adresy klienta** a vložte ji do textového pole **Počáteční IP adresa** a **koncová IP adresa** a klikněte na tlačítko ![přidat-Client-IP-Address-OK-tlačítko](aspnet-mvc-4-models-and-data-access/_static/image40.png).

    ![Přidává se IP adresa klienta.](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    *Přidává se IP adresa klienta.*
3. Jakmile se **IP adresa klienta** přidá do seznamu povolených IP adres, potvrďte změny kliknutím na **Uložit** .

    ![Potvrdit změny](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    *Potvrdit změny*

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Úloha 3 – publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu

1. Vraťte se do řešení ASP.NET MVC 4. V **Průzkumník řešení**klikněte pravým tlačítkem myši na webový projekt a vyberte **publikovat**.

    ![Publikování aplikace](aspnet-mvc-4-models-and-data-access/_static/image43.png "Publikování aplikace")

    *Publikování webu*
2. Importujte profil publikování, který jste uložili v prvním úkolu.

    ![Import profilu publikování](aspnet-mvc-4-models-and-data-access/_static/image44.png "Import profilu publikování")

    *Importuje se publikační profil.*
3. Klikněte na **ověřit připojení**. Po dokončení ověřování klikněte na **Další**.

    > [!NOTE]
    > Ověření je dokončeno, jakmile se zobrazí zelená značka zaškrtnutí vedle tlačítka ověřit připojení.

    ![Ověřování připojení](aspnet-mvc-4-models-and-data-access/_static/image45.png "Ověřování připojení")

    *Ověřování připojení*
4. Na stránce **Nastavení** v části **databáze** klikněte na tlačítko vedle textového pole připojení k databázi (tj. **DefaultConnection**).

    ![Konfigurace nasazení webu](aspnet-mvc-4-models-and-data-access/_static/image46.png "Konfigurace nasazení webu")

    *Konfigurace nasazení webu*
5. Připojení k databázi nakonfigurujte následujícím způsobem:

   - Do pole **název serveru** zadejte adresu URL serveru SQL Database pomocí předpony *TCP:* .
   - V **uživatelské jméno** zadejte přihlašovací jméno správce serveru.
   - V **heslo** zadejte přihlašovací heslo správce serveru.
   - Zadejte nový název databáze.

     ![Konfigurace cílového připojovacího řetězce](aspnet-mvc-4-models-and-data-access/_static/image47.png "Konfigurace cílového připojovacího řetězce")

     *Konfigurace cílového připojovacího řetězce*
6. Pak klikněte na **OK**. Po zobrazení výzvy k vytvoření databáze klikněte na **Ano**.

    ![Vytvoření databáze](aspnet-mvc-4-models-and-data-access/_static/image48.png "Vytváří se řetězec databáze.")

    *Vytvoření databáze*
7. Připojovací řetězec, který budete používat pro připojení k SQL Database ve Windows Azure, se zobrazí ve výchozím textovém poli připojení. Pak klikněte na tlačítko **Další**.

    ![Připojovací řetězec ukazující na SQL Database](aspnet-mvc-4-models-and-data-access/_static/image49.png "Připojovací řetězec ukazující na SQL Database")

    *Připojovací řetězec ukazující na SQL Database*
8. Na stránce **Náhled** klikněte na **publikovat**.

    ![Publikování webové aplikace](aspnet-mvc-4-models-and-data-access/_static/image50.png "Publikování webové aplikace")

    *Publikování webové aplikace*
9. Jakmile se proces publikování dokončí, otevře se ve výchozím prohlížeči publikovaný web.

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a>Příloha C: používání fragmentů kódu

S fragmenty kódu máte veškerý kód, který potřebujete, na dosah ruky. Dokument testovacího prostředí vás přesně upozorní, když ho můžete používat, jak je znázorněno na následujícím obrázku.

![Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio](aspnet-mvc-4-models-and-data-access/_static/image51.png "Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio")

*Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio*

***Přidání fragmentu kódu pomocí klávesnice (C# pouze)***

1. Umístěte kurzor na místo, kam chcete vložit kód.
2. Začněte psát název fragmentu (bez mezer a spojovníků).
3. Sledujte, jak IntelliSense zobrazuje stejné názvy fragmentů kódu.
4. Vyberte správný fragment kódu (nebo pokračujte v psaní, dokud není vybrán celý název tohoto fragmentu kódu).
5. Dvojím stisknutím klávesy TAB vložte fragment kódu do umístění kurzoru.

![Začněte psát název fragmentu.](aspnet-mvc-4-models-and-data-access/_static/image52.png "Začněte psát název fragmentu.")

*Začněte psát název fragmentu.*

![Stisknutím klávesy TAB vyberte zvýrazněný fragment.](aspnet-mvc-4-models-and-data-access/_static/image53.png "Stisknutím klávesy TAB vyberte zvýrazněný fragment.")

*Stisknutím klávesy TAB vyberte zvýrazněný fragment.*

![Stiskněte znovu TAB a fragment kódu se rozšíří.](aspnet-mvc-4-models-and-data-access/_static/image54.png "Stiskněte znovu TAB a fragment kódu se rozšíří.")

*Stiskněte znovu TAB a fragment kódu se rozšíří.*

***Přidání fragmentu kódu pomocí myši (C#, Visual Basic a XML)*** první. Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.

1. Vyberte **Vložit fragment** a potom **Moje fragmenty kódu**.
2. Kliknutím na něj ze seznamu vyberte příslušný fragment kódu.

![Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.](aspnet-mvc-4-models-and-data-access/_static/image55.png "Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.")

*Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.*

![Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.](aspnet-mvc-4-models-and-data-access/_static/image56.png "Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.")

*Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.*

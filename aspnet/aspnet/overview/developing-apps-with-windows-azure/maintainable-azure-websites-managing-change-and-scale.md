---
uid: aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
title: 'Praktická cvičení: Údržba Azure websites: Správa změn a škálování | Microsoft Docs'
author: rick-anderson
description: V tomto testovacím prostředí se dozvíte, jak Microsoft Azure usnadňuje sestavování a nasazování webů do produkčního prostředí.
ms.author: riande
ms.date: 07/16/2014
ms.assetid: ecfd0eb4-c4ad-44e6-9db9-a2a66611ff6a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale
msc.type: authoredcontent
ms.openlocfilehash: c88bae40a8aa092037c0b359ee391acaf161cf10
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624269"
---
# <a name="hands-on-lab-maintainable-azure-websites-managing-change-and-scale"></a>Praktické cvičení: Udržitelné weby Azure – správa změn a škálování

podle [týmu webového Campy](https://twitter.com/webcamps)

[Stáhnout web Campy Training Kit](https://aka.ms/webcamps-training-kit)

> Microsoft Azure usnadňuje sestavování a nasazování webů do produkčního prostředí. Ale nejste hotovi, když je vaše aplikace živá, teprve začínáte! Budete muset zpracovat měnící se požadavky, aktualizace databáze, škálování a další. Naštěstí Azure App Service máte na problém s mnoha funkcemi, které vám pomůžou zajistit bezproblémové fungování vašich webů.
>
> Azure nabízí možnosti bezpečného a flexibilního vývoje, nasazení a škálování libovolné webové aplikace velikosti. Využijte své stávající nástroje k vytváření a nasazování aplikací bez starostí se správou infrastruktury.
>
> Pomocí snadného nasazení obsahu vytvořeného pomocí oblíbeného vývojového nástroje můžete zřídit produkční webovou aplikaci sami v řádu minut. Existující web můžete nasadit přímo ze správy zdrojového kódu s podporou pro **Git**, **GitHub**, **Bitbucket**, **TFS**a dokonce i **Dropbox**. Nasaďte přímo z oblíbeného integrovaného vývojového prostředí (IDE) nebo ze skriptů pomocí **prostředí PowerShell** v nástrojích pro Windows nebo rozhraní příkazového **řádku** Po nasazení Udržujte Vaše weby stále aktuální díky podpoře průběžného nasazování.
>
> Azure poskytuje škálovatelné, odolné cloudové úložiště, zálohování a řešení obnovení pro libovolná data, Velká i malá. Když nasazujete aplikace do provozního prostředí, služby úložiště, jako jsou tabulky, objekty BLOB a databáze SQL, vám pomůžou škálovat aplikace v cloudu.
>
> Databáze SQL jsou důležité při nasazování nových verzí aplikace udržovat produktivní databázi v aktuálním stavu. Díky **migrace Entity Framework Code First**je vývoj a nasazení datového modelu zjednodušené, aby se vaše prostředí aktualizovala během několika minut. Tato praktická cvičení vám ukáže různá témata, se kterými se můžete setkat při nasazení webové aplikace do produkčních prostředí v Microsoft Azure.
>
> Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici na adrese [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).
>
> Podrobnější pokrytí tohoto tématu najdete v tématu [sestavování reálných cloudových aplikací pomocí elektronické knihy Azure](building-real-world-cloud-apps-with-windows-azure/introduction.md).

<a id="Overview"></a>
## <a name="overview"></a>Přehled

<a id="Objectives"></a>
### <a name="objectives"></a>Cíle

V této praktické laboratorní laboratoři se dozvíte, jak:

- Povolit Entity Framework migrace s existujícím modelem
- Aktualizujte objektový model a databázi odpovídajícím způsobem pomocí Entity Framework migrace.
- Nasazení do Azure App Service pomocí Gitu
- Vrácení zpět k předchozímu nasazení pomocí portálu pro správu Azure
- Škálování webové aplikace pomocí Azure Storage
- Konfigurace automatického škálování pro webovou aplikaci pomocí Portál pro správu Azure
- Vytvoření a konfigurace projektu zátěžového testu v aplikaci Visual Studio

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Předpoklady

Následující postup je nutný k dokončení tohoto praktického laboratorního prostředí:

- [Visual Studio Express 2013 pro web](https://www.microsoft.com/visualstudio/) nebo více
- [Sada Azure SDK pro .NET 2,2](https://www.microsoft.com/windowsazure/sdk/)
- [Systém správy verzí GITU](http://git-scm.com/download)
- Microsoft Azure předplatné

    - Zaregistrujte si [bezplatnou zkušební verzi](https://aka.ms/watk-freetrial)
    - Pokud máte Visual Studio Professional, Test Professional, Premium nebo Ultimate s MSDN nebo MSDN Platforms předplatitelem, aktivujte si [výhodu MSDN](https://aka.ms/watk-msdn) hned teď, abyste mohli začít vyvíjet a testovat v Azure.
    - [BizSpark](https://aka.ms/watk-bizspark) členové automaticky získají výhody Azure prostřednictvím předplatného Visual Studio Ultimate with MSDN.
    - Členové programu [Microsoft Partner Network](https://aka.ms/watk-mpn) Cloud Essentials obdrží zdarma měsíční kredit Azure.

<a id="Setup"></a>
### <a name="setup"></a>Nastavení

Aby bylo možné spustit cvičení v této praktické laboratorní laboratoři, budete muset nejprve nastavit prostředí.

1. Otevřete Průzkumníka Windows a přejděte do **zdrojové** složky testovacího prostředí.
2. Klikněte pravým tlačítkem na **Setup. cmd** a vyberte **Spustit jako správce** a spusťte proces instalace, který bude konfigurovat vaše prostředí a nainstaluje fragmenty kódu sady Visual Studio pro toto testovací prostředí.
3. Pokud se zobrazí dialogové okno Řízení uživatelských účtů, potvrďte akci, abyste mohli pokračovat.

> [!NOTE]
> Před spuštěním instalačního programu se ujistěte, že jste kontrolovali všechny závislosti pro toto testovací prostředí.

<a id="CodeSnippets"></a>
### <a name="using-the-code-snippets"></a>Používání fragmentů kódu

V celém dokumentu testovacího prostředí budete vyzváni k vložení bloků kódu. Pro usnadnění práce je většina tohoto kódu k dispozici jako fragmenty Visual Studio Code, ke kterým můžete přistupovat z Visual Studio 2013, abyste se vyhnuli nutnosti ho přidat ručně.

> [!NOTE]
> Každé cvičení se doprovází od počátečního řešení ve složce **Begin** cvičení, které vám umožní sledovat jednotlivá cvičení nezávisle na ostatních. Všimněte si, že fragmenty kódu, které jsou přidány během cvičení, v těchto počátečních řešeních chybí a nemusí fungovat, dokud nedokončíte cvičení. Ve zdrojovém kódu cvičení také najdete **koncovou** složku obsahující řešení sady Visual Studio s kódem, který je výsledkem dokončení kroků v příslušném cvičení. Tato řešení můžete použít jako návod, pokud potřebujete další pomoc při práci s tímto praktickým cvičením.

---

<a id="Exercises"></a>
## <a name="exercises"></a>Cvičení

Tato praktická cvičení zahrnují následující cvičení:

1. [Použití migrace Entity Framework](#Exercise1)
2. [Nasazení webové aplikace do přípravy](#Exercise2)
3. [Provádění vrácení nasazení v produkčním prostředí](#Exercise3)
4. [Škálování pomocí Azure Storage](#Exercise4)
5. [Použití automatického škálování pro Web Apps](#Exercise5) (volitelné pro Visual Studio 2013 Ultimate Edition)

Odhadovaný čas dokončení tohoto testovacího prostředí: **75 minut**

> [!NOTE]
> Při prvním spuštění sady Visual Studio je nutné vybrat jednu z předdefinovaných kolekcí nastavení. Každá předdefinovaná kolekce je navržena tak, aby odpovídala konkrétnímu stylu vývoje a určuje rozložení oken, chování editoru, fragmenty kódu technologie IntelliSense a možnosti dialogového okna. Postupy v tomto testovacím prostředí popisují akce, které jsou nezbytné k provedení daného úkolu v sadě Visual Studio při použití kolekce **Obecné vývojové nastavení** . Pokud zvolíte pro vývojové prostředí jinou kolekci nastavení, mohou být v krocích, které byste měli vzít v úvahu, rozdíly.

<a id="Exercise1"></a>
### <a name="exercise-1-using-entity-framework-migrations"></a>Cvičení 1: použití migrace Entity Framework

Když vyvíjíte aplikaci, váš datový model se může v průběhu času měnit. Tyto změny mohou ovlivnit existující model v databázi (Pokud vytváříte novou verzi) a je důležité udržovat databázi v aktuálním stavu, aby nedocházelo k chybám.

Chcete-li zjednodušit sledování těchto změn v modelu, **migrace Entity Framework Code First** automaticky zjišťovat změny, které porovnávají model s databázovým schématem, a vygeneruje konkrétní kód pro aktualizaci databáze a vytváří nové *verze* vaší databáze.

V tomto cvičení se dozvíte, jak povolit **migrace** pro vaši aplikaci a jak snadno zjišťovat a generovat změny pro aktualizaci databází.

<a id="Ex1Task1"></a>
#### <a name="task-1--enabling-migrations"></a>Úloha 1 – povolení migrací

V této úloze provedete kroky povolení **migrace Entity Framework Code First** do databáze **kvízu informatik** , změnu modelu a porozumění způsobu, jakým se tyto změny projeví v databázi.

1. Otevřete Visual Studio a otevřete soubor řešení **GeekQuiz. sln** z **Source\Ex1-UsingEntityFrameworkMigrations\Begin**.
2. Sestavte řešení, aby se daly stáhnout a nainstalovat závislosti balíčku **NuGet** . Provedete to tak, že kliknete pravým tlačítkem na řešení a kliknete na **Sestavit řešení** nebo stisknete **CTRL + SHIFT + B**.
3. V nabídce **nástroje** v aplikaci Visual Studio vyberte **Správce balíčků NuGet**a pak klikněte na **Konzola správce balíčků**.
4. V **konzole správce balíčků**zadejte následující příkaz a stiskněte klávesu **ENTER**. Vytvoří se počáteční migrace založená na stávajícím modelu.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample1.ps1)]

    ![Povolování migrací](maintainable-azure-websites-managing-change-and-scale/_static/image1.png "Povolování migrací")

    *Povolování migrací*

    > [!NOTE]
    > Tento příkaz přidá složku **migrace** do projektu informatik kvízu, který obsahuje soubor s názvem **Configuration.cs**. Třída **Configuration** umožňuje nakonfigurovat, jak se budou migrace chovat pro váš kontext.
5. U povolených migrací je potřeba aktualizovat třídu **Configuration** , aby se databáze naplnila počátečními daty, která **informatik kvíz** vyžaduje. V části **migrace**nahraďte soubor **Configuration.cs** souborem, který se nachází ve složce **Source\Assets** v tomto testovacím prostředí.

    > [!NOTE]
    > Vzhledem k tomu, že **migrace** zavolá metodu **počáteční** hodnoty s každou aktualizací databáze, je nutné zajistit, aby záznamy nebyly v databázi duplikovány. Metoda **AddOrUpdate** vám pomůže zabránit duplicitním datům.
6. Chcete-li přidat počáteční migraci, zadejte následující příkaz a stiskněte klávesu **ENTER**.

    > [!NOTE]
    > Ujistěte se, že v instanci LocalDB není žádná databáze s názvem &quot;GeekQuizProd&quot;.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample2.ps1)]

    ![Přidává se migrace základního schématu.](maintainable-azure-websites-managing-change-and-scale/_static/image2.png "Přidává se migrace základního schématu.")

    *Přidává se migrace základního schématu.*

    > [!NOTE]
    > **Příkaz Add-Migration** vygeneruje další migraci na základě změn, které jste provedli v modelu od vytvoření poslední migrace. V takovém případě se jako první migrace projektu přidá skripty pro vytvoření všech tabulek definovaných ve třídě **TriviaContext** .
7. Spuštěním následujícího příkazu proveďte migraci k aktualizaci databáze. Pro tento příkaz určíte příznak **verbose** , který zobrazí příkazy SQL, které se aplikují na cílovou databázi.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample3.ps1)]

    ![Vytváření počáteční databáze](maintainable-azure-websites-managing-change-and-scale/_static/image3.png "Vytváření počáteční databáze")

    *Vytváření počáteční databáze*

    > [!NOTE]
    > **Aktualizace – databáze** bude platit pro všechny probíhající migrace do databáze. V tomto případě vytvoří databázi pomocí připojovacího řetězce definovaného v souboru Web. config.
8. Přejděte do nabídky **Zobrazit** a otevřete **Průzkumník objektů systému SQL Server**.

    ![Otevřít v Průzkumník objektů systému SQL Server](maintainable-azure-websites-managing-change-and-scale/_static/image4.png "Otevřít v Průzkumník objektů systému SQL Server")

    *Otevřít v Průzkumník objektů systému SQL Server*
9. V okně **Průzkumník objektů systému SQL Server** se připojte k instanci LocalDB kliknutím pravým tlačítkem myši na uzel **SQL Server** a vybráním možnosti **Přidat SQL Server...** .

    ![Přidání instance SQL Server](maintainable-azure-websites-managing-change-and-scale/_static/image5.png "Přidání instance SQL Server")

    *Přidání instance SQL Server do Průzkumník objektů systému SQL Server*
10. Nastavte **název serveru** na *(LocalDB) \v11.0* a v režimu ověřování nechte **ověřování systému Windows** . Pokračujte kliknutím na **Připojit**.

    ![Připojování k LocalDB](maintainable-azure-websites-managing-change-and-scale/_static/image6.png "Připojování k LocalDB")

    *Připojování k LocalDB*
11. Otevřete databázi **GeekQuizProd** a rozbalte uzel **tabulky** . Jak vidíte, příkaz **Update-Database** vygeneroval všechny tabulky definované ve třídě **TriviaContext** . Vyhledejte **dbo. TriviaQuestions** tabulku a otevřete uzel sloupce. V další úloze přidáte do této tabulky nový sloupec a aktualizujete databázi pomocí **migrací**.

    ![Sloupce otázek minihry](maintainable-azure-websites-managing-change-and-scale/_static/image7.png "Sloupce otázek minihry")

    *Sloupce otázek minihry*

<a id="Ex1Task2"></a>
#### <a name="task-2--updating-database-schema-using-migrations"></a>Úloha 2 – aktualizace schématu databáze pomocí migrací

V této úloze použijete **migrace Entity Framework Code First** k detekci změny v modelu a vygenerujete potřebný kód pro aktualizaci databáze. Entitu **TriviaQuestions** aktualizujete tak, že do ní přidáte novou vlastnost. Potom spustíte příkazy pro vytvoření nové migrace, které budou zahrnovat nový sloupec v tabulce.

1. V **Průzkumník řešení**dvakrát klikněte na soubor **TriviaQuestion.cs** , který se nachází uvnitř složky **modely** .
2. Přidejte novou vlastnost s názvem **Hint**, jak je znázorněno v následujícím fragmentu kódu.

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample4.cs)]
3. V **konzole správce balíčků**zadejte následující příkaz a stiskněte klávesu **ENTER**. Vytvoří se nová migrace odrážející změnu v našem modelu.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample5.ps1)]

    ![Přidání – migrace](maintainable-azure-websites-managing-change-and-scale/_static/image8.png "Přidání – migrace")

    *Přidání – migrace*

    > [!NOTE]
    > Soubor migrace se skládá ze dvou metod, **nahoru** a **dolů**.
    >
    > - Metoda **up** se použije k určení, které změny aktuální verze naší aplikace musí platit pro databázi.
    > - **Dolů** se používá k vrácení změn, které jsme přidali do metody **up** .
    >
    > Když migrace databáze aktualizuje databázi, spustí všechny migrace v pořadí časových razítek a jenom ty, které se od poslední aktualizace nepoužily (tabulka \_MigrationHistory udržuje přehled o tom, které migrace se použily). Metoda **up** pro všechny migrace bude volána a provede změny, které jsme určili v databázi. Pokud se rozhodnete vrátit k předchozí migraci, bude volána metoda **dolů** , která provede změny v obráceném pořadí.
4. V **konzole správce balíčků**zadejte následující příkaz a stiskněte klávesu **ENTER**.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample6.ps1)]
5. Výstup příkazu **Update-Database** vygeneroval příkaz **ALTER TABLE** jazyka SQL pro přidání nového sloupce do tabulky **TriviaQuestions** , jak je znázorněno na následujícím obrázku.

    ![Přidat vygenerovaný příkaz SQL sloupce](maintainable-azure-websites-managing-change-and-scale/_static/image9.png "Přidat vygenerovaný příkaz SQL sloupce")

    *Přidat vygenerovaný příkaz SQL sloupce*
6. V **Průzkumník objektů systému SQL Server**aktualizujte **dbo. TriviaQuestions** tabulku a ověřte, že se zobrazuje nový sloupec s **nápovědou** .

    ![Zobrazení nového sloupce s nápovědou](maintainable-azure-websites-managing-change-and-scale/_static/image10.png "Zobrazení nového sloupce s nápovědou")

    *Zobrazení nového sloupce s nápovědou*
7. Zpět v editoru **TriviaQuestion.cs** přidejte do vlastnosti *Hint* omezení **StringLength** , jak je znázorněno v následujícím fragmentu kódu.

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample7.cs)]
8. V **konzole správce balíčků**zadejte následující příkaz a stiskněte klávesu **ENTER**.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample8.ps1)]
9. V **konzole správce balíčků**zadejte následující příkaz a stiskněte klávesu **ENTER**.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample9.ps1)]
10. Výstup příkazu **Update-Database** vygeneroval příkaz **ALTER TABLE** jazyka SQL, který aktualizuje typ sloupce *pomocného parametru* tabulky **TriviaQuestions** , jak je znázorněno na obrázku níže.

    ![Vygenerované příkazy ALTER COLUMN SQL](maintainable-azure-websites-managing-change-and-scale/_static/image11.png "Vygenerované příkazy ALTER COLUMN SQL")

    *Vygenerované příkazy ALTER COLUMN SQL*
11. V **Průzkumník objektů systému SQL Server**aktualizujte **dbo. TriviaQuestions** tabulku a ověřte, zda je typ sloupce **pomocným parametrem** **nvarchar (150)** .

    ![Zobrazuje se nové omezení.](maintainable-azure-websites-managing-change-and-scale/_static/image12.png "Zobrazuje se nové omezení.")

    *Zobrazuje se nové omezení.*

<a id="Exercise2"></a>
### <a name="exercise-2-deploying-a-web-app-to-staging"></a>Cvičení 2: nasazení webové aplikace do přípravy

**Web Apps v Azure App Service** vám umožní provést dvoufázové publikování. Při dvoufázovém publikování se vytvoří pozice pro pracovní místo pro každý výchozí produkční web a umožní vám tyto sloty prohodit bez času. To je opravdu užitečné k ověření změn před vydáním veřejné, přírůstkově integrování obsahu webu a vrácení zpět, pokud změny nefungují podle očekávání.

V tomto cvičení nasadíte aplikaci **informatik kvíz** do přípravného prostředí vaší webové aplikace pomocí správy zdrojového kódu Git. K tomu vytvoříte webovou aplikaci a zřídíte požadované komponenty na portálu pro správu, nakonfigurujete úložiště **Git** a nahrajete zdrojový kód aplikace z místního počítače do přípravného slotu. Provozní databázi budete aktualizovat také pomocí **migrace Code First** , kterou jste vytvořili v předchozím cvičení. Pak spustíte aplikaci v tomto testovacím prostředí, abyste ověřili její činnost. Jakmile budete přesvědčeni, že funguje podle vašich očekávání, budete aplikaci propagovat na produkční.

> [!NOTE]
> Aby bylo možné povolit dvoufázové publikování, musí být webová aplikace ve **standardním režimu**. Všimněte si, že při změně webové aplikace na standardní režim budou účtovány další poplatky. Další informace o cenách najdete v tématu [App Service ceny](https://azure.microsoft.com/pricing/details/app-service/).

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-web-app-in-azure-app-service"></a>Úloha 1 – Vytvoření webové aplikace v Azure App Service

V této úloze vytvoříte webovou aplikaci v **Azure App Service** na portálu pro správu. Také nakonfigurujete **SQL Database** pro zachování dat aplikace a nakonfigurujete místní úložiště Git pro správu zdrojového kódu.

1. Přejít na [portál pro správu Azure](https://manage.windowsazure.com) a přihlaste se pomocí účet Microsoft přidruženého k vašemu předplatnému.

    ![Přihlaste se k portálu pro správu Azure.](maintainable-azure-websites-managing-change-and-scale/_static/image13.png)

    *Přihlaste se k portálu pro správu Azure.*
2. Na panelu příkazů v dolní části stránky klikněte na **Nový** .

    ![Vytváří se nová webová aplikace.](maintainable-azure-websites-managing-change-and-scale/_static/image14.png "Vytváří se nová webová aplikace.")

    *Vytváří se nová webová aplikace.*
3. Klikněte na **COMPUTE**, **Web** a pak na **vlastní vytvořit**.

    ![Vytvoření nové webové aplikace pomocí vlastního vytvoření](maintainable-azure-websites-managing-change-and-scale/_static/image15.png "Vytvoření nové webové aplikace pomocí vlastního vytvoření")

    *Vytvoření nové webové aplikace pomocí vlastního vytvoření*
4. V dialogovém okně **Nový web – vlastní vytvoření** zadejte dostupnou **adresu URL** (např. *informatik-kvíz*), vyberte umístění v rozevíracím seznamu **oblast** a v rozevíracím seznamu **databáze** vyberte **vytvořit novou databázi SQL** . Nakonec zaškrtněte políčko **publikovat ze správy zdrojového kódu** a klikněte na tlačítko **Další**.

    ![Přizpůsobení nové webové aplikace](maintainable-azure-websites-managing-change-and-scale/_static/image16.png)

    *Přizpůsobení nové webové aplikace*
5. Pro nastavení databáze zadejte následující informace:

   - Do textového pole **název** zadejte název databáze (např. *geekquiz\_DB*).
   - V **rozevíracím** seznamu Server vyberte **Nový server databáze SQL**. Případně můžete vybrat existující server.
   - Do polí **uživatelské jméno databáze** a **heslo databáze** zadejte uživatelské jméno a heslo správce pro server služby SQL Database. Pokud vyberete server, který jste už vytvořili, zobrazí se výzva k zadání hesla.

     ![Určení nastavení databáze](maintainable-azure-websites-managing-change-and-scale/_static/image17.png)

     *Určení nastavení databáze*
6. Pokračujte kliknutím na **Další**.
7. Vyberte **místní úložiště Git** pro správu zdrojového kódu, která se má použít, a klikněte na **Další**.

    > [!NOTE]
    > Může se zobrazit výzva k zadání přihlašovacích údajů pro nasazení (uživatelské jméno a heslo).

    ![Vytváření úložiště Git](maintainable-azure-websites-managing-change-and-scale/_static/image18.png)

    *Vytváření úložiště Git*
8. Počkejte, než se vytvoří nová webová aplikace.

    > [!NOTE]
    > Ve výchozím nastavení poskytuje Azure domény na *azurewebsites.NET* , ale také umožňuje nastavit vlastní domény pomocí portálu pro správu Azure. Vlastní domény ale můžete spravovat jenom v případě, že používáte určité Azure App Service režimy.
    >
    > Azure App Service je k dispozici v edicích Free, Shared, Basic, Standard a Premium. V režimu Free a Shared běží všechny webové aplikace v prostředí s více klienty a mají kvóty pro využití procesoru, paměti a sítě. Maximální počet bezplatných aplikací se může u vašeho plánu lišit. Ve standardním režimu zvolíte, které aplikace se spouštějí na vyhrazených virtuálních počítačích, které odpovídají standardním výpočetním prostředkům Azure. V nabídce **škálování** webové aplikace můžete najít konfiguraci režimu webové aplikace.
    >
    > ![Azure App Service režimy](maintainable-azure-websites-managing-change-and-scale/_static/image19.png "Azure App Service režimy")
    >
    > Pokud používáte **sdílený** nebo **standardní** režim, budete moct spravovat vlastní domény pro vaši webovou aplikaci, a to tak, že přejdete do nabídky **Konfigurace** vaší aplikace a kliknete na **Spravovat domény** v části *názvy domén*.
    >
    > ![Správa domén](maintainable-azure-websites-managing-change-and-scale/_static/image20.png "Správa domén")
    >
    > ![Správa vlastních domén](maintainable-azure-websites-managing-change-and-scale/_static/image21.png "Správa vlastních domén")
9. Po vytvoření webové aplikace klikněte na odkaz ve sloupci **Adresa URL** a ověřte, jestli je spuštěná nová webová aplikace.

    ![Procházení nové webové aplikace](maintainable-azure-websites-managing-change-and-scale/_static/image22.png)

    *Procházení nové webové aplikace*

    ![spuštěná webová aplikace](maintainable-azure-websites-managing-change-and-scale/_static/image23.png)

    *spuštěná webová aplikace*

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-the-production-sql-database"></a>Úloha 2 – Vytvoření produkčního SQL Database

V této úloze použijete **migrace Entity Framework Code First** k vytvoření databáze cílící na instanci **Azure SQL Database** , kterou jste vytvořili v předchozím úkolu.

1. V Portál pro správu přejděte do webové aplikace, kterou jste vytvořili v předchozím úkolu, a přejděte na **řídicí panel**.
2. Na stránce **řídicí panel** klikněte v části **rychlý přehled** na odkaz **Zobrazit připojovací řetězce** .

    ![Zobrazit připojovací řetězce](maintainable-azure-websites-managing-change-and-scale/_static/image24.png "Zobrazit připojovací řetězce")

    *Zobrazit připojovací řetězce*
3. Zkopírujte hodnotu **připojovacího řetězce** a zavřete dialogové okno.

    ![Připojovací řetězec v Azure Portál pro správu](maintainable-azure-websites-managing-change-and-scale/_static/image25.png "Připojovací řetězec v Azure Portál pro správu")

    *Připojovací řetězec v Azure Portál pro správu*
4. Kliknutím na **databáze SQL** zobrazíte seznam databází SQL v Azure.

    ![Nabídka SQL Database](maintainable-azure-websites-managing-change-and-scale/_static/image26.png "Nabídka SQL Database")

    *Nabídka SQL Database*
5. Vyhledejte databázi, kterou jste vytvořili v předchozí úloze, a klikněte na server.

    ![Server SQL Database](maintainable-azure-websites-managing-change-and-scale/_static/image27.png "Server služby SQL Database")

    *Server SQL Database*
6. Na stránce **rychlé zprovoznění** serveru klikněte na možnost **Konfigurovat**.

    ![Konfigurace nabídky](maintainable-azure-websites-managing-change-and-scale/_static/image28.png "Konfigurace nabídky")

    *Konfigurace nabídky*
7. V části **povolené IP adresy** klikněte na odkaz **Přidat na adresu povolených IP adres** , aby se vaše IP adresa mohla připojit k serveru SQL Database.

    ![Povolené IP adresy](maintainable-azure-websites-managing-change-and-scale/_static/image29.png "Povolené IP adresy")

    *Povolené IP adresy*
8. Kliknutím na **Save (Uložit** ) v dolní části stránky dokončete krok.
9. Přepněte zpět do sady Visual Studio.
10. V **konzole správce balíčků**spusťte následující příkaz, kterým nahradíte zástupný symbol *[text-Connection-String]* připojovacím řetězcem, který jste zkopírovali z Azure.

    [!code-powershell[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample10.ps1)]

    ![Aktualizace databáze cílící na Windows Azure SQL Database](maintainable-azure-websites-managing-change-and-scale/_static/image30.png "Aktualizace databáze cílící na Windows Azure SQL Database")

    *Aktualizace cílení databáze Azure SQL Database*

<a id="Ex2Task3"></a>
#### <a name="task-3--deploying-geek-quiz-to-staging-using-git"></a>Úloha 3 – nasazení informatik kvízu do přípravy pomocí Gitu

V této úloze povolíte připravené publikování ve vaší webové aplikaci. Pak použijete Git k publikování aplikace informatik kvízu přímo z místního počítače do přípravného prostředí vaší webové aplikace.

1. Vraťte se na portál a kliknutím na název webové aplikace pod sloupcem **název** zobrazíte stránky pro správu.

    ![Otevření stránek správy webové aplikace](maintainable-azure-websites-managing-change-and-scale/_static/image31.png)

    *Otevření stránek správy webové aplikace*
2. Přejděte na stránku **škálování** . V části **Obecné** vyberte pro konfiguraci možnost **Standard** a na panelu příkazů klikněte na **Uložit** .

    > [!NOTE]
    > Chcete-li spustit všechny webové aplikace v aktuální oblasti a předplatném ve **standardním** režimu, ponechte zaškrtnuté políčko **zaškrtnout vše** v části **zvolit konfiguraci webů** . V opačném případě zrušte zaškrtnutí políčka **Vybrat vše** .

    ![Upgrade webové aplikace na standardní režim](maintainable-azure-websites-managing-change-and-scale/_static/image32.png "Upgrade webové aplikace na standardní režim")

    *Upgrade webové aplikace na standardní režim*
3. Kliknutím na tlačítko **Ano** potvrďte změny.

    ![Potvrzení změny do standardního režimu](maintainable-azure-websites-managing-change-and-scale/_static/image33.png "Pokračování ve změně režimu webové aplikace")

    *Potvrzení změny do standardního režimu*
4. Přejděte na stránku **řídicí panel** a klikněte na **povolit dvoufázové publikování** v části **rychlý přehled** .

    ![Povolení dvoufázové publikování](maintainable-azure-websites-managing-change-and-scale/_static/image34.png "Povolení dvoufázové publikování")

    *Povolení dvoufázové publikování*
5. Kliknutím na **Ano** povolíte dvoufázové publikování.

    ![Potvrzení připraveného publikování](maintainable-azure-websites-managing-change-and-scale/_static/image35.png "Kliknutím na Ano povolíte dvoufázové publikování.")

    *Potvrzení připraveného publikování*
6. V seznamu webových aplikací rozbalte značku vlevo od názvu vaší webové aplikace a zobrazte tak pracovní slot pro přípravu na pracovišti. Má název vaší webové aplikace, za nímž následuje ***(příprava)***. Kliknutím na pracovní web přejdete na stránku správy.

    ![Navigace do pracovní webové aplikace](maintainable-azure-websites-managing-change-and-scale/_static/image36.png "Navigace do pracovní webové aplikace")

    *Navigace do pracovní aplikace*
7. Všimněte si, že stránka správy vypadá jako jakákoli jiná stránka správy webové aplikace. Přejděte na stránku **nasazení** a zkopírujte hodnotu **adresy URL Gitu** . Budete ho používat později v tomto cvičení.

    ![Kopíruje se hodnota adresy URL Gitu.](maintainable-azure-websites-managing-change-and-scale/_static/image37.png)

    *Kopíruje se hodnota adresy URL Gitu.*
8. Otevřete novou konzolu **Git bash** a spusťte následující příkazy. Aktualizujte zástupný text *[vaše aplikace-cesta]* s cestou k řešení **GeekQuiz** , které najdete ve složce **Source\Ex1-DeployingWebSiteToStaging\Begin** tohoto testovacího prostředí.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample11.cmd)]

    ![Inicializace Gitu a první potvrzení](maintainable-azure-websites-managing-change-and-scale/_static/image38.png)

    *Inicializace Gitu a první potvrzení*
9. Spuštěním následujícího příkazu nahrajte webovou aplikaci do vzdáleného úložiště **Git** . Zástupný symbol nahraďte adresou URL, kterou jste získali z portálu pro správu. Zobrazí se výzva k zadání hesla pro nasazení.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample12.cmd)]

    ![Doručování do Windows Azure](maintainable-azure-websites-managing-change-and-scale/_static/image39.png)

    *Doručování do Azure*

    > [!NOTE]
    > Když nasadíte obsah do hostitele FTP nebo úložiště GIT webové aplikace, musíte provést ověření pomocí **přihlašovacích údajů pro nasazení** , které jste vytvořili na stránkách pro správu **rychlé zprovoznění** nebo **řídicího panelu** webové aplikace. Pokud vaše přihlašovací údaje pro nasazení neznáte, můžete je snadno obnovit pomocí portálu pro správu. Otevřete stránku **řídicí panel** webové aplikace a klikněte na odkaz **resetovat přihlašovací údaje pro nasazení** . Zadejte nové heslo a klikněte na **OK**. Přihlašovací údaje pro nasazení jsou platné pro použití se všemi webovými aplikacemi, které jsou přidružené k vašemu předplatnému.
10. Aby bylo možné ověřit, zda byla webová aplikace úspěšně vložena do Azure, přejděte zpět na portál pro správu a klikněte na **weby**.
11. Vyhledejte svou webovou aplikaci a rozbalte položku, abyste zobrazili pracovní pozici pracovního serveru. Kliknutím na jeho **název** přejdete na stránku správy.
12. Kliknutím na **nasazení** zobrazte **historii nasazení**. Ověřte, že existuje **aktivní nasazení** s *&quot;úvodní&quot;potvrzení* .

    ![Aktivní nasazení](maintainable-azure-websites-managing-change-and-scale/_static/image40.png)

    *Aktivní nasazení*
13. Nakonec na panelu příkazů klikněte na tlačítko **Procházet** a přejděte do webové aplikace.

    ![Procházet webovou aplikaci](maintainable-azure-websites-managing-change-and-scale/_static/image41.png)

    *Procházet webovou aplikaci*
14. Pokud je aplikace úspěšně nasazená, zobrazí se stránka pro přihlášení kvízu informatik.

    > [!NOTE]
    > Adresa URL adresy nasazené aplikace obsahuje název webové aplikace následovaný po *přípravě*.

    ![Aplikace spuštěná v přípravném prostředí](maintainable-azure-websites-managing-change-and-scale/_static/image42.png)

    *Aplikace spuštěná v přípravném prostředí*
15. Pokud chcete aplikaci prozkoumat, klikněte na **zaregistrovat** a zaregistrujte nového uživatele. Vyplňte podrobnosti účtu zadáním uživatelského jména, e-mailové adresy a hesla. V dalším kroku aplikace zobrazuje první otázku kvízu. Odpovězte na pár otázek a ujistěte se, že funguje podle očekávání.

    ![Aplikace připravená k použití](maintainable-azure-websites-managing-change-and-scale/_static/image43.png)

    *Aplikace připravená k použití*

<a id="Ex2Task4"></a>
#### <a name="task-4--promoting-the-web-app-to-production"></a>Úloha 4 – propagace webové aplikace do produkčního prostředí

Teď, když jste ověřili, že webová aplikace funguje správně v přípravném prostředí, jste připraveni ji propagovat na produkční prostředí. V této úloze provedete záměnu pracovní pozice webu na pozici produkčního pracoviště.

1. Vraťte se na portál pro správu a vyberte pracovní pozici pracovního serveru. Na panelu příkazů klikněte na **prohodit** .

    ![Přeměna do produkčního prostředí](maintainable-azure-websites-managing-change-and-scale/_static/image44.png)

    *Přeměna do produkčního prostředí*
2. Kliknutím na **Ano** v potvrzovacím dialogovém okně pokračujte v operaci swap. Azure okamžitě zamění obsah produkčního webu s obsahem pracovní lokality.

    > [!NOTE]
    > Některá nastavení ze připravené verze se automaticky zkopírují do produkční verze (např. přepsání připojovacích řetězců, mapování obslužných rutin atd.), ostatní nastavení se ale nezmění (například koncové body DNS, vazby SSL atd.).

    ![Potvrzení operace prohození](maintainable-azure-websites-managing-change-and-scale/_static/image45.png)

    *Potvrzení operace prohození*
3. Po dokončení prohození vyberte produkční slot a kliknutím na tlačítko **Procházet** na panelu příkazů otevřete provozní Web. Všimněte si adresy URL v adresním řádku.

    > [!NOTE]
    > Možná budete muset aktualizovat prohlížeč, aby se mezipaměť vymazala. V Internet Exploreru to můžete udělat stisknutím **kombinace kláves CTRL + R**.

    ![Webová aplikace spuštěná v produkčním prostředí](maintainable-azure-websites-managing-change-and-scale/_static/image46.png)
4. V konzole **GitBash** aktualizujte VZDÁLENOU adresu URL pro místní úložiště Git, aby se cílí na produkční slot. Uděláte to tak, že spustíte následující příkaz, kterým nahradíte zástupné symboly vaším uživatelským jménem nasazení a název vaší webové aplikace.

    > [!NOTE]
    > V následujících cvičeních provedete změny v produkčním webu místo přípravy jenom pro jednoduchost testovacího prostředí. Ve scénáři reálného světa se doporučuje před zvýšením úrovně produkčního prostředí ověřit změny v přípravném prostředí.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample13.cmd)]

<a id="Exercise3"></a>
### <a name="exercise-3-performing-deployment-rollback-in-production"></a>Cvičení 3: provádění vrácení nasazení v produkčním prostředí

K dispozici jsou situace, kdy nemáte přípravný slot pro provádění horkého swapu mezi příchodem a výrobou, například pokud pracujete s **bezplatným** nebo **sdíleným** režimem. V těchto scénářích byste měli testovat aplikaci v testovacím prostředí – buď místně, nebo ve vzdálené lokalitě – před nasazením do produkčního prostředí. Je však možné, že v produkčním prostředí může dojít k problému, který nebyl zjištěn během testovací fáze. V takovém případě je důležité mít mechanismus snadného přepnutí na předchozí a více stabilní verze aplikace co nejrychleji.

V **Azure App Service**umožňuje průběžné nasazování ze správy zdrojového kódu to díky akci **opětovného nasazení** , která je k dispozici na portálu pro správu. Azure sleduje nasazení přidružená k potvrzením, která jsou vložená do úložiště, a poskytuje možnost znovu nasadit aplikaci pomocí libovolného z předchozích nasazení.

V tomto cvičení provedete změnu kódu v aplikaci **informatik kvízu** , která záměrně vloží *chybu*. Aplikaci nasadíte do produkčního prostředí, aby se zobrazila chyba. potom můžete využít funkci opětovného nasazení a vrátit se k předchozímu stavu.

<a id="Ex3Task1"></a>
#### <a name="task-1--updating-the-geek-quiz-application"></a>Úloha 1 – aktualizace aplikace informatik kvíz

V tomto úkolu refaktorujte malé části kódu třídy **TriviaController** , abyste mohli extrahovat část logiky, která načte vybranou možnost kvízu z databáze do nové metody.

1. Přepněte do instance sady Visual Studio s řešením **GeekQuiz** z předchozího cvičení.
2. V **Průzkumník řešení**otevřete soubor **TriviaController.cs** ve složce **Controllers** .
3. Vyhledejte metodu **StoreAsync** a vyberte kód zvýrazněný na následujícím obrázku.

    ![Výběr kódu](maintainable-azure-websites-managing-change-and-scale/_static/image47.png)

    *Výběr kódu*
4. Klikněte pravým tlačítkem myši na vybraný kód, rozbalte nabídku **refaktoration** a vyberte **Extrahovat metodu...** .

    ![Extrakce kódu jako nové metody](maintainable-azure-websites-managing-change-and-scale/_static/image48.png)

    *Výběr metody extrakce*
5. V dialogovém okně **Extrahovat metodu** pojmenujte novou metodu *MatchesOption* a klikněte na tlačítko **OK**.

    ![Zadání názvu metody](maintainable-azure-websites-managing-change-and-scale/_static/image49.png)

    *Určení názvu extrahované metody*
6. Vybraný kód je poté extrahován do metody **MatchesOption** . Výsledný kód je zobrazen v následujícím fragmentu kódu.

    [!code-csharp[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample14.cs)]
7. Změny uložte stisknutím **kombinace kláves CTRL + S** .

<a id="Ex3Task2"></a>
#### <a name="task-2--redeploying-the-geek-quiz-application"></a>Úloha 2 – opětovné nasazení aplikace informatik kvíz

Nyní budete předávat změny, které jste provedli v předchozím úkolu, do úložiště, které aktivuje nové nasazení do provozního prostředí. Pak Troubleshot problém pomocí **vývojářských nástrojů F12** , které poskytuje Internet Explorer, a pak proveďte vrácení zpět k předchozímu nasazení z portálu pro správu Azure.

1. Otevřete novou konzolu **Git bash** a nasaďte aktualizovanou aplikaci na Azure App Service.
2. Spuštěním následujících příkazů nahrajte změny do Azure. Aktualizujte zástupný text *[Your-Application-Path]* cestou k řešení **GeekQuiz** . Zobrazí se výzva k zadání hesla pro nasazení.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample15.cmd)]

    ![Vložení refaktoringového kódu do Azure](maintainable-azure-websites-managing-change-and-scale/_static/image50.png)

    *Vložení refaktoringového kódu do Azure*
3. Spusťte Internet Explorer a přejděte do vaší webové aplikace (např. `http://<your-web-site>.azurewebsites.net`). Přihlaste se pomocí dříve vytvořených přihlašovacích údajů.
4. Stisknutím klávesy **F12** spusťte vývojové nástroje, vyberte kartu **síť** a kliknutím na tlačítko **Přehrát** spusťte záznam.

    ![Spouští se záznam v síti.](maintainable-azure-websites-managing-change-and-scale/_static/image51.png "Spouští se záznam v síti.")

    *Spouští se záznam v síti.*
5. Vyberte libovolnou možnost kvízu. Uvidíte, že se nic nestane.
6. V okně **F12** položka odpovídající požadavku POST HTTP zobrazí výsledek http **500** .

    ![Chyba HTTP 500](maintainable-azure-websites-managing-change-and-scale/_static/image52.png)

    *Chyba HTTP 500*
7. Vyberte kartu **Konzola** . S podrobnostmi o příčině se protokoluje chyba.

    ![Chyba protokolu](maintainable-azure-websites-managing-change-and-scale/_static/image53.png)

    *Chyba protokolu*
8. Vyhledejte část s podrobnostmi o chybě. Tato chyba je jasně způsobena refaktoringem kódu, který jste protvrdili v předchozích krocích.

    `Details: LINQ to Entities does not recognize the method 'Boolean MatchesOption ...`.
9. Nezavírejte prohlížeč.
10. V nové instanci prohlížeče přejděte na [portál pro správu Azure](https://manage.windowsazure.com) a přihlaste se pomocí účet Microsoft přidruženého k vašemu předplatnému.
11. Vyberte **websites** a klikněte na webovou aplikaci, kterou jste vytvořili v cvičení 2.
12. Přejděte na stránku **nasazení** . Všimněte si, že všechna potvrzení změn jsou uvedena v historii nasazení.

    ![Seznam existujících nasazení](maintainable-azure-websites-managing-change-and-scale/_static/image54.png)

    *Seznam existujících nasazení*
13. Vyberte předchozí potvrzení a klikněte na panelu příkazů na **znovu nasadit** .

    ![Opětovné nasazení předchozího potvrzení změn](maintainable-azure-websites-managing-change-and-scale/_static/image55.png)

    *Opětovné nasazení předchozího potvrzení změn*
14. Po zobrazení výzvy k potvrzení klikněte na **Ano**.

    ![Potvrzení opětovného nasazení](maintainable-azure-websites-managing-change-and-scale/_static/image56.png)
15. Po dokončení nasazení přepněte zpátky do instance prohlížeče s vaší webovou aplikací a stiskněte klávesy **CTRL + F5**.
16. Klikněte na kteroukoli z možností. Nyní bude provedeno překlápění animace a zobrazí se výsledek (*správný/nesprávný*).
17. Volitelné Přepněte do konzoly **Git bash** a spusťte následující příkazy, které se vrátí k předchozímu potvrzení změn.

    > [!NOTE]
    > Tyto příkazy vytvoří nové potvrzení, které zruší všechny změny v úložišti Git, které byly provedeny v nesprávném potvrzení. Azure pak znovu nasadí aplikaci pomocí nového potvrzení změn.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample16.cmd)]

<a id="Exercise4"></a>
### <a name="exercise-4-scaling-using-azure-storage"></a>Cvičení 4: škálování pomocí Azure Storage

**Bloby** představují nejjednodušší způsob, jak ukládat velké objemy nestrukturovaných textových nebo binárních dat, jako je video, zvuk a obrázky. Když přesunete statický obsah vaší aplikace do úložiště, pomůže vám škálovat aplikaci tím, že obsluhuje obrázky nebo dokumenty přímo v prohlížeči.

V tomto cvičení přesunete statický obsah vaší aplikace do kontejneru objektů BLOB. Potom nakonfigurujete aplikaci tak, aby do kontejneru objektů BLOB přidala **pravidlo pro přepsání adresy URL ASP.NET** v **souboru Web. config** .

<a id="Ex4Task1"></a>
#### <a name="task-1--creating-an-azure-storage-account"></a>Úloha 1 – Vytvoření účtu Azure Storage

V této úloze se dozvíte, jak vytvořit nový účet úložiště pomocí portálu pro správu.

1. Přejděte na [portál pro správu Azure](https://manage.windowsazure.com) a přihlaste se pomocí účet Microsoft přidruženého k vašemu předplatnému.
2. Vybrat **Nový | Data Services | Úložiště | Rychlé vytvoření** a začněte vytvářet nový účet úložiště. Zadejte jedinečný název pro účet a vyberte **oblast** ze seznamu. Pokračujte kliknutím na **vytvořit účet úložiště** .

    ![Vytváří se nový účet úložiště.](maintainable-azure-websites-managing-change-and-scale/_static/image57.png "Vytváří se nový účet úložiště.")

    *Vytváří se nový účet úložiště.*
3. V části **úložiště** počkejte, než se stav nového účtu úložiště změní na *online* , aby bylo možné pokračovat v následujícím kroku.

    ![Účet úložiště se vytvořil.](maintainable-azure-websites-managing-change-and-scale/_static/image58.png "Účet úložiště se vytvořil.")

    *Účet úložiště se vytvořil.*
4. Klikněte na název účtu úložiště a potom klikněte na odkaz **řídicí panel** v horní části stránky. Stránka **řídicí panel** poskytuje informace o stavu účtu a koncových bodech služby, které lze použít v rámci svých aplikací.

    ![Zobrazuje se řídicí panel účtu úložiště.](maintainable-azure-websites-managing-change-and-scale/_static/image59.png "Zobrazuje se řídicí panel účtu úložiště.")

    *Zobrazuje se řídicí panel účtu úložiště.*
5. Na navigačním panelu klikněte na tlačítko **Správa přístupových klíčů** .

    ![Tlačítko pro správu přístupových klíčů](maintainable-azure-websites-managing-change-and-scale/_static/image60.png "Tlačítko pro správu přístupových klíčů")

    *Tlačítko pro správu přístupových klíčů*
6. V dialogovém okně **Správa přístupových klíčů** zkopírujte **název účtu úložiště** a **Primární přístupový klíč** , protože je budete potřebovat v následujícím cvičení. Pak zavřete dialogové okno.

    ![Dialogové okno Správa přístupového klíče](maintainable-azure-websites-managing-change-and-scale/_static/image61.png "Dialogové okno Správa přístupového klíče")

    *Dialogové okno Správa přístupového klíče*

<a id="Ex4Task2"></a>
#### <a name="task-2--uploading-an-asset-to-azure-blob-storage"></a>Úloha 2 – nahrání Assetu do Azure Blob Storage

V této úloze použijete okno Průzkumník serveru ze sady Visual Studio pro připojení k vašemu účtu úložiště. Pak vytvoříte kontejner objektů BLOB a nahrajete do kontejneru soubor s logem informatik kvízu.

1. Přepněte do instance sady Visual Studio s řešením **GeekQuiz** z předchozího cvičení.
2. V řádku nabídek vyberte **Zobrazit** a pak klikněte na **Průzkumník serveru**.
3. V **Průzkumník serveru**klikněte pravým tlačítkem myši na uzel **Azure** a vyberte **připojit k Azure...** . Přihlaste se pomocí účet Microsoft přidruženého k vašemu předplatnému.

    ![Připojení k Windows Azure](maintainable-azure-websites-managing-change-and-scale/_static/image62.png)

    *Připojení k Azure*
4. Rozbalte uzel **Azure** , klikněte pravým tlačítkem na **úložiště** a vyberte **připojit externí úložiště...** .
5. V dialogovém okně **Přidat nový účet úložiště** zadejte **název účtu** a **klíč účtu** , který jste získali v předchozí úloze, a klikněte na tlačítko **OK**.

    ![Dialogové okno Přidat nový účet úložiště](maintainable-azure-websites-managing-change-and-scale/_static/image63.png)

    *Dialogové okno Přidat nový účet úložiště*
6. Váš účet úložiště by se měl zobrazit pod uzlem **úložiště** . Rozbalte svůj účet úložiště, klikněte pravým tlačítkem na **objekty blob** a vyberte **vytvořit kontejner objektů BLOB...** .

    ![Vytvořit kontejner objektů BLOB](maintainable-azure-websites-managing-change-and-scale/_static/image64.png "Vytvořit kontejner objektů blob")

    *Vytvořit kontejner objektů BLOB*
7. V dialogovém okně **vytvořit kontejner objektů BLOB** zadejte název kontejneru objektů BLOB a klikněte na **OK**.

    ![Dialogové okno vytvořit kontejner objektů BLOB](maintainable-azure-websites-managing-change-and-scale/_static/image65.png "Dialogové okno vytvořit kontejner objektů BLOB")

    *Dialogové okno vytvořit kontejner objektů BLOB*
8. Nový kontejner objektů BLOB by měl být přidán do uzlu **objekty blob** . Změňte přístupová oprávnění v kontejneru tak, aby kontejner byl veřejný. Provedete to tak, že kliknete pravým tlačítkem na kontejner **imagí** a vyberete **vlastnosti**.

    ![vlastnosti kontejneru imagí](maintainable-azure-websites-managing-change-and-scale/_static/image66.png "vlastnosti kontejneru imagí")

    *Vlastnosti kontejneru imagí*
9. V okně **vlastnosti** nastavte **veřejný přístup pro čtení** na **kontejner**.

    ![Změna veřejné vlastnosti přístupu pro čtení](maintainable-azure-websites-managing-change-and-scale/_static/image67.png "Změna veřejné vlastnosti přístupu pro čtení")

    *Změna veřejné vlastnosti přístupu pro čtení*
10. Když se zobrazí dotaz, jestli jste si jisti, že chcete změnit vlastnost veřejného přístupu, klikněte na **Ano**.

    ![Upozornění Microsoft Visual Studio](maintainable-azure-websites-managing-change-and-scale/_static/image68.png "Upozornění Microsoft Visual Studio")

    *Upozornění Microsoft Visual Studio*
11. V **Průzkumník serveru**klikněte pravým tlačítkem na kontejner objektů BLOB **imagí** a vyberte **Zobrazit kontejner objektů BLOB**.

    ![Zobrazit kontejner objektů BLOB](maintainable-azure-websites-managing-change-and-scale/_static/image69.png "Zobrazit kontejner objektů BLOB")

    *Zobrazit kontejner objektů BLOB*
12. Kontejner imagí by měl být otevřen v novém okně a legenda bez položek by měla být zobrazena. Kliknutím na ikonu **nahrát** nahrajte soubor do kontejneru objektů BLOB.

    ![Kontejner imagí bez záznamů](maintainable-azure-websites-managing-change-and-scale/_static/image70.png "Kontejner imagí bez záznamů")

    *Kontejner imagí bez záznamů*
13. V dialogovém okně **nahrát objekt BLOB** přejděte do složky **assets (prostředky** ) v testovacím prostředí. Vyberte soubor **logo-Big. png** a klikněte na **otevřít**.
14. Počkejte, než se soubor nahraje. Až se nahrávání dokončí, soubor by měl být uvedený v kontejneru images. Pravým tlačítkem myši klikněte na položku soubor a vyberte možnost **Kopírovat adresu URL**.

    ![Kopírovat adresu URL objektu BLOB](maintainable-azure-websites-managing-change-and-scale/_static/image71.png "Kopírovat adresu URL souboru objektu BLOB")

    *Kopírovat adresu URL objektu BLOB*
15. Otevřete Internet Explorer a vložte adresu URL. V prohlížeči by se měl zobrazit následující obrázek.

    ![Obrázek logo-Big. png z Windows Blob Storage](maintainable-azure-websites-managing-change-and-scale/_static/image72.png "Obrázek logo-Big. png z úložiště")

    *Obrázek logo-Big. png z Azure Blob Storage*

<a id="Ex4Task3"></a>
#### <a name="task-3--updating-the-solution-to-consume-static-content-from-azure-blob-storage"></a>Úloha 3 – aktualizace řešení pro využívání statického obsahu z Azure Blob Storage

V této úloze nakonfigurujete řešení **GeekQuiz** , aby se využila bitová kopie nahraná do Azure Blob Storage (namísto image umístěná ve webové aplikaci) přidáním pravidla pro přepsání adresy URL ASP.NET v souboru **Web. config** .

1. V aplikaci Visual Studio otevřete soubor **Web. config** v rámci projektu **GeekQuiz** a vyhledejte prvek **&gt;&lt;System. webServer** .
2. Přidejte následující kód, který přidá pravidlo pro přepsání adresy URL a aktualizuje zástupný text názvem svého účtu úložiště.

    (Fragment kódu – *WebSitesInProduction-Ex4-UrlRewriteRule*)

    [!code-xml[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample17.xml)]

    > [!NOTE]
    > Přepsání adresy URL je proces zachycení příchozího webového požadavku a přesměrování požadavku na jiný prostředek. Pravidla přepisu adresy URL přidávají modulu přepisu, když je potřeba přesměrovat požadavek a kde by se měla přesměrovat. Pravidlo přepisování se skládá ze dvou řetězců: vzor, který má být hledán v požadované adrese URL (obvykle pomocí regulárních výrazů), a řetězec, který má nahradit vzor, pokud byl nalezen. Další informace najdete v tématu [přepsání adresy URL v ASP.NET](https://msdn.microsoft.com/library/ms972974.aspx).
3. Změny uložte stisknutím **kombinace kláves CTRL + S** .
4. Otevřete novou konzolu **Git bash** a nasaďte aktualizovanou aplikaci na Azure App Service.
5. Spuštěním následujících příkazů nahrajte změny do Azure. Aktualizujte zástupný text *[Your-Application-Path]* cestou k řešení **GeekQuiz** . Zobrazí se výzva k zadání hesla pro nasazení.

    [!code-console[Main](maintainable-azure-websites-managing-change-and-scale/samples/sample18.cmd)]

    ![Nasazení aktualizace do Azure](maintainable-azure-websites-managing-change-and-scale/_static/image73.png)

    *Nasazení aktualizace do Azure*

<a id="Ex4Task4"></a>
#### <a name="task-4--verification"></a>Úloha 4 – ověření

V této úloze použijete **Internet Explorer** k procházení aplikace **informatik kvíz** a zkontrolujete, že pravidlo pro přepsání adresy URL pro Image funguje a že budete přesměrováni na Image hostovanou v **Azure Blob Storage**.

1. Spusťte Internet Explorer a přejděte do vaší webové aplikace (např. `http://<your-web-site>.azurewebsites.net`). Přihlaste se pomocí dříve vytvořených přihlašovacích údajů.

    ![Zobrazení webové aplikace kvízu informatik s obrázkem](maintainable-azure-websites-managing-change-and-scale/_static/image74.png "Zobrazení webové aplikace kvízu informatik s obrázkem")

    *Zobrazení webové aplikace kvízu informatik s obrázkem*
2. Stisknutím klávesy **F12** spusťte vývojové nástroje, vyberte kartu **síť** a spusťte záznam.

    ![Spouští se záznam v síti.](maintainable-azure-websites-managing-change-and-scale/_static/image75.png "Spouští se záznam v síti.")

    *Spouští se záznam v síti.*
3. Stisknutím **kombinace kláves CTRL + F5** aktualizujte webovou stránku.
4. Po načtení stránky by se měla zobrazit žádost HTTP adresy URL **/img/logo-Big.png** s výsledkem http **301** (přesměrování) a jinou žádostí o `http://[YOUR-STORAGE-ACCOUNT].blob.core.windows.net/images/logo-big.png` url s výsledkem http **200** .

    ![Ověření přesměrování adresy URL](maintainable-azure-websites-managing-change-and-scale/_static/image76.png "Zobrazuje se přesměrování v nástrojích pro vývoj")

    *Ověření přesměrování adresy URL*

<a id="Exercise5"></a>
### <a name="exercise-5-using-autoscale-for-web-apps"></a>Cvičení 5: použití automatického škálování pro Web Apps

> [!NOTE]
> Toto cvičení je volitelné, protože vyžaduje podporu webového zatížení &amp; testování výkonu, které je k dispozici pouze pro **Visual Studio 2013 Ultimate Edition**. Další informace o konkrétních funkcích Visual Studio 2013 najdete v [tématu](https://www.microsoft.com/visualstudio/eng/products/compare)porovnání verzí.

**Azure App Service Web Apps** poskytuje funkci automatického škálování pro webové aplikace běžící ve **standardním režimu**. Automatické škálování umožňuje Azure automaticky škálovat počet instancí webové aplikace v závislosti na zatížení. Když je zapnuté automatické škálování, Azure zkontroluje procesor vaší webové aplikace jednou za pět minut a v daném časovém okamžiku přidá instance podle potřeby. Pokud je využití procesoru nízké, Azure odstraní instance jednou za dvě hodiny, aby se zajistilo, že výkon vaší webové aplikace nebude degradován.

V tomto cvičení provedete kroky nutné ke konfiguraci funkce **automatického škálování** pro webovou aplikaci **informatik kvíz** . Tuto funkci ověříte spuštěním zátěžového testu sady Visual Studio pro vygenerování dostatečného zatížení procesoru v aplikaci pro aktivaci upgradu instance.

<a id="Ex5Task1"></a>
#### <a name="task-1--configuring-autoscale-based-on-the-cpu-metric"></a>Úloha 1 – Konfigurace automatického škálování na základě metriky procesoru

V této úloze použijete portál pro správu Azure k povolení funkce automatického škálování pro webovou aplikaci, kterou jste vytvořili v cvičení 2.

1. Na [portálu pro správu Azure](https://manage.windowsazure.com/)vyberte **weby** a klikněte na webovou aplikaci, kterou jste vytvořili v cvičení 2.
2. Přejděte na stránku **škálování** . V části **kapacita** vyberte možnost **CPU** pro **škálování podle konfigurace metriky** .

    > [!NOTE]
    > Při škálování podle CPU Azure dynamicky přizpůsobí počet instancí, které aplikace používá, pokud se změní využití procesoru.

    ![Výběr pro škálování podle procesoru](maintainable-azure-websites-managing-change-and-scale/_static/image77.png "Výběr metriky procesoru pro automatické škálování")

    *Výběr pro škálování podle procesoru*
3. Změňte **cílovou konfiguraci procesoru** na **20**-**40** procent.

    > [!NOTE]
    > Tento rozsah představuje průměrné využití procesoru vaší webové aplikace. Azure bude přidávat nebo odebírat instance, aby se vaše webová aplikace udržovala v tomto rozsahu. Minimální a maximální počet instancí použitých pro škálování je zadaný v konfiguraci **počtu instancí** . Azure nebude nikdy nad rámec tohoto limitu.
    >
    > Výchozí hodnoty **CÍLOVÉHO procesoru** se upravují pouze pro účely tohoto testovacího prostředí. Konfigurací rozsahu procesoru s malými hodnotami zvýšíte pravděpodobnost aktivace automatického škálování, když se na aplikaci umístí střední zatížení.

    ![Změna cílového procesoru na hodnotu mezi 20 a 40%](maintainable-azure-websites-managing-change-and-scale/_static/image78.png "Změna cílového procesoru na hodnotu mezi 20 a 40%")

    *Změna cílového procesoru na hodnotu mezi 20 a 40%*
4. Změny uložte kliknutím na **Uložit** na panelu příkazů.

<a id="Ex5Task2"></a>
#### <a name="task-2--load-testing-with-visual-studio"></a>Úloha 2 – zátěžové testování pomocí sady Visual Studio

Teď, když je nakonfigurované **Automatické škálování** , vytvoříte v aplikaci Visual Studio **projekt webového výkonu a zátěžového testu** , který vygeneruje některé zatížení procesoru ve vaší webové aplikaci.

1. Otevřete **Visual Studio Ultimate 2013** a vyberte **soubor | Nové | Projekt...** pro spuštění nového řešení.

    ![Vytvoření nového projektu](maintainable-azure-websites-managing-change-and-scale/_static/image79.png "Vytvoření nového projektu")

    *Vytvoření nového projektu*
2. V dialogovém okně **Nový projekt** vyberte v vizuálu  **C# projekt testování výkonu webu a zátěžový test | Karta test** . Ujistěte se, že je vybraná možnost **.NET Framework 4,5** , název projektu *WebAndLoadTestProject*, vyberte **umístění** a klikněte na **OK**.

    ![Vytvoření nového projektu webového a zátěžového testu](maintainable-azure-websites-managing-change-and-scale/_static/image80.png "Vytvoření nového projektu webového a zátěžového testu")

    *Vytvoření nového projektu webového a zátěžového testu*
3. V **WebTest1. webtest** klikněte pravým tlačítkem myši na uzel **WebTest1** a klikněte na **Přidat žádost**.

    ![Přidání žádosti do WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image81.png "Přidání žádosti do WebTest1")

    *Přidání žádosti do WebTest1*
4. V okně **vlastnosti** nového uzlu požadavku aktualizujte vlastnost **Adresa URL** tak, aby odkazovala na adresu URL vaší webové aplikace (např. *[http://geek-quiz.azurewebsites.net/](http://geek-quiz.azurewebsites.net/)* ).

    ![Změna vlastnosti adresy URL](maintainable-azure-websites-managing-change-and-scale/_static/image82.png "Změna vlastnosti adresy URL")

    *Změna vlastnosti adresy URL*
5. V okně **WebTest1. webtest** klikněte pravým tlačítkem myši na **WebTest1** a klikněte na **Přidat smyčku...** .

    ![Přidání smyčky do WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image83.png "Přidání smyčky do WebTest1")

    *Přidání smyčky do WebTest1*
6. V dialogovém okně **přidat podmíněné pravidlo a položky do cyklu** vyberte pravidlo **smyčky for** a upravte následující vlastnosti.

   1. **Koncová hodnota:** 1000
   2. **Název kontextového parametru:** Iterátor
   3. **Přírůstková hodnota:** 1

      ![Výběr pravidla smyčky for a aktualizace vlastností](maintainable-azure-websites-managing-change-and-scale/_static/image84.png "Výběr pravidla smyčky for a aktualizace vlastností")

      *Výběr pravidla smyčky for a aktualizace vlastností*
7. V části **smyčka Items (položky v cyklu** ) vyberte požadavek, který jste dříve vytvořili jako první a poslední položku pro smyčku. Pokračujte kliknutím na tlačítko **OK** .

    ![Výběr první a poslední položky pro smyčku](maintainable-azure-websites-managing-change-and-scale/_static/image85.png "Výběr první a poslední položky pro smyčku")

    *Výběr první a poslední položky pro smyčku*
8. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt **WebAndLoadTestProject** , rozbalte nabídku **Přidat** a vyberte **zátěžový test...** .

    ![Přidání zátěžového testu do projektu WebAndLoadTestProject](maintainable-azure-websites-managing-change-and-scale/_static/image86.png "Přidání zátěžového testu do projektu WebAndLoadTestProject")

    *Přidání zátěžového testu do projektu WebAndLoadTestProject*
9. V dialogovém okně **nový Průvodce zátěžovým testem** klikněte na **Další**.

    ![Nový Průvodce zátěžovým testem](maintainable-azure-websites-managing-change-and-scale/_static/image87.png "Nový Průvodce zátěžovým testem")

    *Nový Průvodce zátěžovým testem*
10. Na stránce **scénář** vyberte **Nepoužívat časy přemýšlení** a klikněte na **Další**.

    ![Výběr nepoužití časů promýšlení](maintainable-azure-websites-managing-change-and-scale/_static/image88.png "Výběr nepoužití časů promýšlení")

    *Výběr nepoužití časů promýšlení*
11. Na stránce **vzor zatížení** se ujistěte, že je vybraná možnost **konstantního zatížení** . Změňte nastavení **počet uživatelů** na **250** uživatelů a klikněte na **Další**.

    ![Změna počtu uživatelů na 250](maintainable-azure-websites-managing-change-and-scale/_static/image89.png "Změna počtu uživatelů na 250")

    *Změna počtu uživatelů na 250*
12. Na stránce **model kombinace testů** vyberte na **základě pořadí sekvenčních testů** a klikněte na **Další**.

    ![Výběr modelu kombinace testů](maintainable-azure-websites-managing-change-and-scale/_static/image90.png "Výběr modelu kombinace testů")

    *Výběr modelu kombinace testů*
13. Na stránce **model** poměru testů klikněte na tlačítko **Přidat...** a přidejte do kombinace test.

    ![Přidání testu do kombinace testů](maintainable-azure-websites-managing-change-and-scale/_static/image91.png "Přidání testu do kombinace testů")

    *Přidání testu do kombinace testů*
14. V dialogovém okně **Přidat testy** poklikejte na **WebTest1** a přidejte test do seznamu **vybraných testů** . Pokračujte kliknutím na tlačítko **OK** .

    ![Přidání testu WebTest1](maintainable-azure-websites-managing-change-and-scale/_static/image92.png "Přidání testu WebTest1")

    *Přidání testu WebTest1*
15. Zpátky na stránce **kombinace testů** klikněte na **Další**.

    ![Dokončuje se stránka kombinace testů.](maintainable-azure-websites-managing-change-and-scale/_static/image93.png "Dokončuje se stránka kombinace testů.")

    *Dokončuje se stránka kombinace testů.*
16. Na stránce **kombinace sítě** klikněte na **Další**.

    ![Kliknutí na tlačítko Další na stránce kombinace sítě](maintainable-azure-websites-managing-change-and-scale/_static/image94.png "Kliknutí na tlačítko Další na stránce kombinace sítě")

    *Kliknutí na tlačítko Další na stránce kombinace sítě*
17. Na stránce **kombinace prohlížečů** jako typ prohlížeče vyberte **Internet Explorer 10,0** a klikněte na **Další**.

    ![Výběr typu prohlížeče](maintainable-azure-websites-managing-change-and-scale/_static/image95.png "Výběr typu prohlížeče")

    *Výběr typu prohlížeče*
18. Na stránce **sady čítačů** klikněte na **Další**.

    ![Kliknutí na další na stránce sady čítačů](maintainable-azure-websites-managing-change-and-scale/_static/image96.png "Kliknutí na další na stránce sady čítačů")

    *Kliknutí na další na stránce sady čítačů*
19. Na stránce **nastavení spuštění** nastavte **dobu trvání zátěžového testu** na **5 minut** a klikněte na tlačítko **Dokončit**.

    ![Nastavení doby trvání zátěžového testu na 5 minut](maintainable-azure-websites-managing-change-and-scale/_static/image97.png "Nastavení doby trvání zátěžového testu na 5 minut")

    *Nastavení doby trvání zátěžového testu na 5 minut*
20. V **Průzkumník řešení**dvakrát klikněte na soubor **Local. Settings** a prozkoumejte nastavení testu. Ve výchozím nastavení používá Visual Studio místní počítač ke spuštění testů.

    > [!NOTE]
    > Alternativně můžete nakonfigurovat projekt testů tak, aby spouštěl zátěžové testy v cloudu pomocí **Azure test Plans**. Azure Test Plans poskytuje cloudovou službu zátěžového testování, která simuluje realističtější zatížení, což vyloučí omezení místních prostředí, jako je kapacita procesoru, dostupná paměť a šířka pásma sítě. Další informace o použití Azure Test Plans ke spouštění zátěžových testů naleznete v tématu [scénáře zátěžového testování](/azure/devops/test/load-test/overview?view=vsts).

    ![Nastavení testu](maintainable-azure-websites-managing-change-and-scale/_static/image98.png)

<a id="Ex5Task3"></a>
#### <a name="task-3--autoscale-verification"></a>Úloha 3 – ověření automatického škálování

Nyní spustíte zátěžový test, který jste vytvořili v předchozí úloze, a zjistíte, jak se webová aplikace chová při zatížení.

1. V **Průzkumník řešení**dvakrát klikněte na **LoadTest1. LoadTest** a otevřete zátěžový test.

    ![Otevírání LoadTest1. LoadTest](maintainable-azure-websites-managing-change-and-scale/_static/image99.png "Otevírání LoadTest1. LoadTest")

    *Otevírání LoadTest1. LoadTest*
2. V okně **LoadTest1. LoadTest** kliknutím na první tlačítko v panelu nástrojů Spusťte zátěžový test.

    ![Spuštění zátěžového testu](maintainable-azure-websites-managing-change-and-scale/_static/image100.png "Spuštění zátěžového testu")

    *Spuštění zátěžového testu*
3. Počkejte na dokončení zátěžového testu.

    > [!NOTE]
    > Zátěžový test simuluje více uživatelů, kteří odesílají požadavky do webové aplikace současně. Po spuštění testu můžete monitorovat dostupné čítače a odhalit případné chyby, varování nebo jiné informace, které se týkají vašeho běhu zátěžového testu.

    ![Zátěžový test běží](maintainable-azure-websites-managing-change-and-scale/_static/image101.png "Čeká se na dokončení zátěžového testu.")

    *Zátěžový test běží*
4. Po dokončení testu se vraťte na portál pro správu a přejděte na stránku **škálování** vaší webové aplikace. V části **kapacita** byste měli vidět v grafu, že se automaticky nasadila nová instance.

    ![Automaticky nasazená nová instance](maintainable-azure-websites-managing-change-and-scale/_static/image102.png)

    *Automaticky nasazená nová instance*

    > [!NOTE]
    > Může trvat několik minut, než se změny objeví v grafu (Pokud chcete stránku aktualizovat, stiskněte klávesu **CTRL + F5** pravidelně). Pokud žádné změny nevidíte, můžete vyzkoušet následující:
    >
    > - Prodloužit dobu trvání zátěžového testu (například na **10 minut**)
    > - Snižte maximální a minimální hodnoty **cílového rozsahu procesoru** v konfiguraci automatického škálování vaší webové aplikace.
    > - Spusťte zátěžový test v cloudu pomocí **Azure test Plans**. Další informace [](/azure/devops/test/load-test/index?view=vsts)

---

<a id="Summary"></a>
## <a name="summary"></a>Souhrn

V tomto praktickém cvičení jste zjistili, jak nastavit a nasadit aplikaci do produkčních webových aplikací v Azure. Začali jste zjišťováním a aktualizací databází pomocí **migrace Entity Framework Code First**a pak pokračovali nasazením nových verzí webu pomocí **Gitu** a vrácením se zpět do nejnovější stabilní verze vaší lokality. Kromě toho jste zjistili, jak škálovat aplikaci pomocí úložiště, aby se váš statický obsah přesunul do kontejneru objektů BLOB.

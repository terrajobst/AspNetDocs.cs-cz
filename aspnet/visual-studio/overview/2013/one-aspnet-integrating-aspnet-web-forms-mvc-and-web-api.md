---
uid: visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
title: 'Praktická cvičení: jedna ASP.NET: integrace webových formulářů ASP.NET, MVC a webového rozhraní API | Microsoft Docs'
author: rick-anderson
description: ASP.NET je architektura pro vytváření webů, aplikací a služeb s využitím specializovaných technologií, jako je MVC, webové rozhraní API a další. S rozšířením ASP.NET h...
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 4fe2558d-67cc-4d12-a5c1-6fb9f6f16137
msc.legacyurl: /visual-studio/overview/2013/one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api
msc.type: authoredcontent
ms.openlocfilehash: 165d104b5d3ef3281af449cc8673ad96f531d628
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623198"
---
# <a name="hands-on-lab-one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api"></a>Praktické cvičení: jeden ASP.NET: Integrace webových formulářů ASP.NET, MVC a webového rozhraní API

podle [týmu webového Campy](https://twitter.com/webcamps)

[Stáhnout web Campy Training Kit](https://aka.ms/webcamps-training-kit)

> ASP.NET je architektura pro vytváření webů, aplikací a služeb s využitím specializovaných technologií, jako je MVC, webové rozhraní API a další. S rozšířením ASP.NET se od jeho vytvoření objevila a vyjádřily se, že tyto technologie jsou integrované, ale bylo nedávno vyvíjené úsilí při práci na **jednom ASP.NET**.
> 
> Visual Studio 2013 zavádí nový jednotný projektový systém, který umožňuje sestavit aplikaci a používat všechny technologie ASP.NET v jednom projektu. Tato funkce eliminuje nutnost vybírat jednu technologii na začátku projektu a místo toho je doporučuje použít více ASP.NETch architektur v rámci jednoho projektu.
> 
> Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici na adrese [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).

<a id="Overview"></a>
## <a name="overview"></a>Přehled

<a id="Objectives"></a>
### <a name="objectives"></a>Cíle

V této praktické laboratorní laboratoři se dozvíte, jak:

- Vytvoření webu založeného na jednom typu projektu **ASP.NET**
- Použijte různé **ASP.NET** architektury, jako je **MVC** a **webové rozhraní API** , ve stejném projektu.
- Identifikujte hlavní součásti aplikace **ASP.NET**
- Využijte rozhraní **ASP.NET pro generování uživatelského rozhraní** k automatickému vytvoření řadičů a zobrazení k provádění operací CRUD na základě tříd modelu.
- Vystavte stejnou sadu informací v formátech strojového a uživatelsky čitelném pomocí správného nástroje pro každou úlohu.

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Předpoklady

Následující postup je nutný k dokončení tohoto praktického laboratorního prostředí:

- [Visual Studio Express 2013 pro web](https://www.microsoft.com/visualstudio/) nebo více
- [Visual Studio 2013 Update 1](https://go.microsoft.com/fwlink/?LinkId=301714)

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

1. [Vytvoření nového projektu webových formulářů](#Exercise1)
2. [Vytvoření kontroleru MVC pomocí generování uživatelského rozhraní](#Exercise2)
3. [Vytvoření kontroleru webového rozhraní API pomocí generování uživatelského rozhraní](#Exercise3)

Odhadovaný čas dokončení tohoto testovacího prostředí: **60 minut**

> [!NOTE]
> Při prvním spuštění sady Visual Studio je nutné vybrat jednu z předdefinovaných kolekcí nastavení. Každá předdefinovaná kolekce je navržena tak, aby odpovídala konkrétnímu stylu vývoje a určuje rozložení oken, chování editoru, fragmenty kódu technologie IntelliSense a možnosti dialogového okna. Postupy v tomto testovacím prostředí popisují akce, které jsou nezbytné k provedení daného úkolu v sadě Visual Studio při použití kolekce **Obecné vývojové nastavení** . Pokud zvolíte pro vývojové prostředí jinou kolekci nastavení, mohou být v krocích, které byste měli vzít v úvahu, rozdíly.

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-new-web-forms-project"></a>Cvičení 1: vytvoření nového projektu webových formulářů

V tomto cvičení vytvoříte nový Web Forms v Visual Studio 2013 pomocí jednotného projektového prostředí **ASP.NET** , které vám umožní snadno integrovat webové formuláře, komponenty MVC a webové rozhraní API do stejné aplikace. Pak budete prozkoumat vygenerované řešení a Identifikujte jeho části a nakonec uvidíte web v akci.

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-a-new-site-using-the-one-aspnet-experience"></a>Úloha 1 – Vytvoření nového webu s využitím jednoho ASP.NETového prostředí

V této úloze začnete vytvářet nový web v aplikaci Visual Studio na základě jednoho typu projektu **ASP.NET** . **Jedna ASP.neta** sjednocuje všechny technologie ASP.NET a dává vám možnost je podle potřeby kombinovat a odpovídat. Pak rozpoznáváte různé komponenty webových formulářů, MVC a webového rozhraní API, které se nachází v rámci aplikace vedle sebe.

1. Otevřete **Visual Studio Express 2013 pro web** a vyberte **soubor | Nový projekt...** pro spuštění nového řešení.

    ![Vytvoření nového projektu](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image1.png)

    *Vytvoření nového projektu*
2. V dialogovém okně **Nový projekt** vyberte v části vizuál  **C# možnost Webová aplikace v ASP.NET | Kartu Web** a ujistěte se, že je vybrána možnost **.NET Framework 4,5** . Pojmenujte projekt *MyHybridSite*, vyberte **umístění** a klikněte na **OK**.

    ![Nový projekt webové aplikace v ASP.NET](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image2.png)

    *Vytvoření nového projektu webové aplikace v ASP.NET*
3. V dialogovém okně **Nový projekt ASP.NET** vyberte šablonu **webové formuláře** a vyberte možnosti **MVC** a **webové rozhraní API** . Také se ujistěte, že je možnost **ověřování** nastavena na **jednotlivé uživatelské účty**. Pokračujte kliknutím na tlačítko **OK** .

    ![Vytvoření nového projektu pomocí šablony webových formulářů, včetně komponent webového rozhraní API a MVC](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image3.png)

    *Vytvoření nového projektu pomocí šablony webových formulářů, včetně komponent webového rozhraní API a MVC*
4. Nyní můžete prozkoumat strukturu vygenerovaného řešení.

    ![Zkoumání vygenerovaného řešení](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image4.png)

    *Zkoumání vygenerovaného řešení*

    1. **Účet:** Tato složka obsahuje stránky webového formuláře k registraci, přihlášení a správu uživatelských účtů aplikace. Tato složka se přidá, pokud je při konfiguraci šablony projektu webové formuláře vybrána možnost ověřování **individuálních uživatelských účtů** .
    2. **Modely:** Tato složka bude obsahovat třídy, které reprezentují data vaší aplikace.
    3. **Řadiče** a **zobrazení**: tyto složky jsou vyžadovány pro komponenty **webového rozhraní API** **ASP.NET MVC** a ASP.NET. V následujících cvičeních budete zkoumat technologie MVC a webové rozhraní API.
    4. Soubory **Default. aspx**, **Contact. aspx** a **About. aspx** jsou předem definované stránky webových formulářů, které lze použít jako výchozí body pro sestavení stránek specifických pro vaši aplikaci. Programovací logika těchto souborů se nachází v samostatném souboru, který je označován jako &quot;soubor&quot; s kódem na pozadí, který obsahuje &quot;. aspx. vb&quot; nebo &quot;. aspx.cs&quot; (v závislosti na používaném jazyce). Logika kódu na pozadí běží na serveru a dynamicky vytváří výstup HTML stránky.
    5. Stránky **site. Master** a **site. Mobile. Master** definují vzhled a chování a standardní chování všech stránek v aplikaci.
5. Dvojím kliknutím na soubor **Default. aspx** můžete prozkoumat obsah stránky.

    ![Prozkoumávání stránky default. aspx](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image5.png)

    *Prozkoumávání stránky default. aspx*

    > [!NOTE]
    > Direktiva **stránky** v horní části souboru definuje atributy stránky webových formulářů. Například atribut **MasterPageFile** Určuje cestu k hlavní stránce – v tomto případě se jedná o stránku *site. Master* – a atribut **Inherits** definuje třídu kódu na pozadí pro stránku, která má dědit. Tato třída je umístěna v souboru určeném atributem **CodeBehind** .
    > 
    > Ovládací prvek **ASP: Content** obsahuje skutečný obsah stránky (text, značky a ovládací prvky) a je namapován na ovládací prvek **ASP: ContentPlaceHolder** na stránce předlohy. V tomto případě se obsah stránky vykreslí uvnitř ovládacího prvku *MainContent* , který je definovaný na stránce *site. Master* .
6. Rozbalte **aplikaci\_spustit** složku a Všimněte si souboru **WebApiConfig.cs** . Visual Studio zahrnulo tento soubor do vygenerovaného řešení, protože jste zahrnuli webové rozhraní API při konfiguraci projektu s jednou šablonou ASP.NET.
7. Otevřete soubor **WebApiConfig.cs** . Ve třídě *WebApiConfig* najdete konfiguraci přidruženou k webovému rozhraní API, která MAPUJE trasy HTTP na **řadiče webového rozhraní API**.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample1.cs)]
8. Otevřete soubor **RouteConfig.cs** . V rámci metody *RegisterRoutes* najdete konfiguraci přidruženou ke MVC, která MAPUJE trasy HTTP na **řadiče MVC**.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample2.cs)]

<a id="Ex1Task2"></a>
#### <a name="task-2--running-the-solution"></a>Úloha 2 – spuštění řešení

V této úloze spustíte vygenerované řešení, prozkoumejte aplikaci a některé její funkce, jako je přepis adres URL a integrované ověřování.

1. Pokud chcete řešení spustit, stiskněte klávesu **F5** nebo klikněte na tlačítko **Start** , které se nachází na panelu nástrojů. Na domovské stránce aplikace by se měl otevřít v prohlížeči.

    ![Spuštění řešení](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image6.png)
2. Ověřte, zda jsou vyvolány stránky webových formulářů. Pokud to chcete provést, přidejte **/Contact.aspx** k adrese URL na adresním řádku a stiskněte klávesu **ENTER**.

    ![Popisné adresy URL](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image7.png)

    *Popisné adresy URL*

    > [!NOTE]
    > Jak vidíte, adresa URL se změní na **/Contact**. Počínaje **ASP.NET 4**byly do webových formulářů přidány možnosti směrování adres URL, takže můžete napsat adresy url jako *[http://www.mysite.com/products/software](http://www.mysite.com/products/software)* místo *[http://www.mysite.com/products.aspx?category=software](http://www.mysite.com/products.aspx?category=software)* . Další informace najdete v tématu [směrování adres URL](../../../web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing.md).
3. Teď budete zkoumat tok ověřování integrovaný do aplikace. Uděláte to tak, že kliknete na **Registrovat** v pravém horním rohu stránky.

    ![Registrace nového uživatele](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image8.png)

    *Registrace nového uživatele*
4. Na stránce **zaregistrovat** zadejte **uživatelské jméno** a **heslo**a potom klikněte na **zaregistrovat**.

    ![Registrovat stránku](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image9.png)

    *Registrovat stránku*
5. Aplikace registruje nový účet a uživatel je ověřený.

    ![Ověřeno uživatelem](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image10.png)

    *Ověřeno uživatelem*
6. Vraťte se do sady Visual Studio a stisknutím klávesy **SHIFT + F5** Zastavte ladění.

<a id="Exercise2"></a>
### <a name="exercise-2-creating-an-mvc-controller-using-scaffolding"></a>Cvičení 2: vytvoření kontroleru MVC pomocí generování uživatelského rozhraní

V tomto cvičení využijete rozhraní ASP.NET pro generování uživatelského rozhraní poskytované sadou Visual Studio k vytvoření kontroleru ASP.NET MVC 5 s akcemi a zobrazeními Razor k provádění operací CRUD, aniž byste museli psát jediný řádek kódu. Proces generování uživatelského rozhraní použije Entity Framework Code First k vygenerování kontextu dat a schématu databáze v databázi SQL.

**Informace o Entity Framework Code First**

Entity Framework (EF) je objektově-relační Mapovač (ORM), který umožňuje vytvářet aplikace pro přístup k datům pomocí programování s modelem konceptuální aplikace namísto programování přímo pomocí schématu relačního úložiště.

Pracovní postup modelování Entity Framework Code First umožňuje použít vlastní třídy domény k reprezentaci modelu, který se v EF spoléhá na použití funkcí dotazování, sledování změn a aktualizace. Pomocí pracovního postupu Code Firstho vývoje nemusíte spouštět aplikaci vytvořením databáze nebo zadáním schématu. Místo toho můžete napsat standardní třídy .NET, které definují nejvhodnější objekty doménového modelu pro vaši aplikaci, a Entity Framework vytvoří databázi za vás.

> [!NOTE]
> Další informace o Entity Framework najdete [tady](../../../entity-framework.md).

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-a-new-model"></a>Úloha 1 – Vytvoření nového modelu

Nyní definujete třídu **Person** , která bude modelem použitým procesem generování uživatelského rozhraní k vytvoření kontroleru MVC a zobrazení. Začnete vytvořením třídy typu **osoba** a operace CRUD v kontroleru se automaticky vytvoří pomocí funkcí generování uživatelského rozhraní.

1. Otevřete **Visual Studio Express 2013 pro web** a řešení **MyHybridSite. sln** nacházející se ve složce **source/EX2-MvcScaffolding/Begin** . Případně můžete pokračovat v řešení, které jste získali v předchozím cvičení.
2. V **Průzkumník řešení**klikněte pravým tlačítkem na složku **modely** projektu **MyHybridSite** a vyberte **Přidat | Třída...** .

    ![Přidání třídy modelu osoby](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image11.png)

    *Přidání třídy modelu osoby*
3. V dialogovém okně **Přidat novou položku** zadejte název souboru *Person.cs* a klikněte na **Přidat**.

    ![Vytvoření třídy modelu osoby](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image12.png)

    *Vytvoření třídy modelu osoby*
4. Obsah souboru **Person.cs** nahraďte následujícím kódem. Změny uložte stisknutím **kombinace kláves CTRL + S** .

    (Fragment kódu – *BringingTogetherOneAspNet-EX2-PersonClass*)

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample3.cs)]
5. V **Průzkumník řešení**klikněte pravým tlačítkem na projekt **MyHybridSite** a vyberte **Build (sestavit**), nebo stiskněte **kombinaci kláves CTRL + SHIFT + B** a sestavte projekt.

<a id="Ex2Task2"></a>
#### <a name="task-2--creating-an-mvc-controller"></a>Úloha 2 – Vytvoření kontroleru MVC

Teď, když se vytvoří model **osoby** , použijete ASP.NET MVC s Entity Framework k vytvoření akcí kontroleru CRUD a zobrazení pro **osobu**.

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku **řadiče** projektu **MyHybridSite** a vyberte **Přidat | Nová vygenerovaná položka...**

    ![Vytváření nového vygenerovaného kontroleru](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image13.png)

    *Vytváření nového vygenerovaného kontroleru*
2. V dialogovém okně **Přidat vygenerované uživatelské rozhraní** vyberte **kontroler MVC 5 se zobrazeními, pomocí Entity Framework** a pak klikněte na **Přidat.**

    ![Výběr kontroleru MVC 5 se zobrazeními a Entity Framework](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image14.png)

    *Výběr kontroleru MVC 5 se zobrazeními a Entity Framework*
3. Jako **název kontroleru**nastavte *MvcPersonController* , vyberte možnost **použít asynchronní řadič akce** a jako **třídu modelu**vyberte **Person (MyHybridSite. Models)** .

    ![Přidání kontroleru MVC s generováním uživatelského rozhraní](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image15.png)

    *Přidání kontroleru MVC s generováním uživatelského rozhraní*
4. V části **Třída kontextu dat**klikněte na **nový kontext dat..** ..

    ![Vytvoření nového kontextu dat](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image16.png)

    *Vytvoření nového kontextu dat*
5. V dialogovém okně **nový kontext dat** pojmenujte nový kontext dat *PersonContext* a klikněte na **Přidat**.

    ![Vytváření nového PersonContext](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image17.png)

    *Vytváří se nový typ PersonContext.*
6. Kliknutím na **Přidat** vytvořte nový kontroler pro **osobu** s vytvářením uživatelského rozhraní. Visual Studio potom vygeneruje akce kontroleru, kontext dat osoby a zobrazení Razor.

    ![Po vytvoření kontroleru MVC pomocí generování uživatelského rozhraní](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image18.png)

    *Po vytvoření kontroleru MVC pomocí generování uživatelského rozhraní*
7. Otevřete soubor **MvcPersonController.cs** ve složce **Controllers** . Všimněte si, že metody akce CRUD byly vygenerovány automaticky.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample4.cs)]

    > [!NOTE]
    > Zaškrtnutím políčka **použít asynchronní akce kontroleru** z možností generování uživatelského rozhraní v předchozích krocích aplikace Visual Studio vygeneruje asynchronní metody akcí pro všechny akce, které zahrnují přístup k datovému kontextu osoby. Doporučuje se používat asynchronní metody akcí pro dlouhotrvající, nevázané požadavky na procesor, aby nedošlo k tomu, aby webový server při zpracování žádosti prováděl práci.

<a id="Ex2Task3"></a>
#### <a name="task-3--running-the-solution"></a>Úloha 3 – spuštění řešení

V této úloze znovu spustíte řešení a ověříte, že zobrazení pro **osobu** pracují podle očekávání. Přidáte novou osobu, která ověří, zda je úspěšně uložena do databáze.

1. Stisknutím klávesy **F5** spusťte řešení.
2. Přejděte na **/MvcPerson**. Zobrazí se vygenerované zobrazení, které zobrazuje seznam osob.
3. Kliknutím na **vytvořit novou** přidejte novou osobu.

    ![Navigace do zobrazení s vygenerovanými MVC](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image19.png)

    *Navigace do zobrazení s vygenerovanými MVC*
4. V zobrazení **vytvořit** zadejte pro osobu **jméno** a **stáří** a klikněte na **vytvořit**.

    ![Přidává se nová osoba.](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image20.png)

    *Přidává se nová osoba.*
5. Nová osoba se přidá do seznamu. V seznamu element kliknutím na tlačítko **Podrobnosti** zobrazíte zobrazení podrobností osoby. Pak v zobrazení **podrobností** klikněte na **zpět k seznamu** a vraťte se do zobrazení seznamu.

    ![Zobrazení podrobností osoby](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image21.png)

    *Zobrazení podrobností osoby*
6. Kliknutím na odkaz **Odstranit** odstraňte osobu. V zobrazení **Odstranit** klikněte na **Odstranit** a potvrďte operaci.

    ![Odstranění osoby](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image22.png)

    *Odstranění osoby*
7. Vraťte se do sady Visual Studio a stisknutím klávesy **SHIFT + F5** Zastavte ladění.

<a id="Exercise3"></a>
### <a name="exercise-3-creating-a-web-api-controller-using-scaffolding"></a>Cvičení 3: vytvoření kontroleru webového rozhraní API pomocí generování uživatelského rozhraní

Rozhraní Web API je součástí sady ASP.NET stack a je navržené pro snazší implementaci služby HTTP, obecně posílání a přijímání dat ve formátu JSON nebo XML prostřednictvím rozhraní RESTful API.

V tomto cvičení použijete znovu generování uživatelského rozhraní ASP.NET, abyste vygenerovali webový kontroler API. V předchozím cvičení použijete stejné třídy **Person** a **PersonContext** , aby poskytovaly stejná data osob ve formátu JSON. Uvidíte, jak můžete stejné prostředky vystavovat různými způsoby v rámci stejné ASP.NET aplikace.

<a id="Ex3Task1"></a>
#### <a name="task-1--creating-a-web-api-controller"></a>Úloha 1 – Vytvoření kontroleru webového rozhraní API

V této úloze vytvoříte nový **kontroler webového rozhraní API** , který bude zveřejňovat data osob ve formátu, ve kterém se jedná o počítač, jako je JSON.

1. Pokud ještě není otevřený, otevřete **Visual Studio Express 2013 pro web** a otevřete řešení **MyHybridSite. sln** umístěné ve složce **source/EX3-WebApi/Begin** . Případně můžete pokračovat v řešení, které jste získali v předchozím cvičení.

    > [!NOTE]
    > Pokud začínáte s řešením zahájení z cvičení 3, sestavte řešení stisknutím **kombinace kláves CTRL + SHIFT + B** .
2. V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku **řadiče** projektu **MyHybridSite** a vyberte **Přidat | Nová vygenerovaná položka...**

    ![Vytváření nového vygenerovaného kontroleru](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image23.png)

    *Vytváření nového vygenerovaného kontroleru*
3. V dialogovém okně **Přidat vygenerované uživatelské rozhraní** v levém podokně vyberte **webové rozhraní API** , potom **kontroler webového rozhraní API 2 s akcemi pomocí Entity Framework** v prostředním podokně a pak klikněte na **Přidat.**

    ![Výběr kontroleru webového rozhraní API 2 s akcemi a Entity Framework](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image24.png "Výběr kontroleru webového rozhraní API 2 s akcemi a Entity Framework")

    *Výběr kontroleru webového rozhraní API 2 s akcemi a Entity Framework*
4. Jako **název kontroleru**nastavte *ApiPersonController* , vyberte možnost **použít asynchronní řadič akce** a jako **model** a třídy **kontextu dat** vyberte **Person (MyHybridSite. Models)** a **PersonContext (MyHybridSite. Models)** . Pak klikněte na **Přidat**.

    ![Přidání kontroleru webového rozhraní API s využitím uživatelského rozhraní](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image25.png "Přidání kontroleru webového rozhraní API s využitím uživatelského rozhraní")

    *Přidání kontroleru webového rozhraní API s využitím uživatelského rozhraní*
5. Visual Studio potom vytvoří třídu **ApiPersonController** se čtyřmi akcemi CRUD pro práci s daty.

    ![Po vytvoření kontroleru webového rozhraní API s využitím uživatelského rozhraní](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image26.png "Po vytvoření kontroleru webového rozhraní API s využitím uživatelského rozhraní")

    *Po vytvoření kontroleru webového rozhraní API s využitím uživatelského rozhraní*
6. Otevřete soubor **ApiPersonController.cs** a prozkoumejte metodu akce *getlidé* . Tato metoda se dotazuje pole DB typu **PersonContext** , aby získala data osob.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample5.cs)]
7. Nyní si všimněte komentáře nad definicí metody. Poskytuje identifikátor URI, který zpřístupňuje tuto akci, kterou použijete v dalším úkolu.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample6.cs)]

    > [!NOTE]
    > Ve výchozím nastavení je webové rozhraní API nakonfigurované pro zachycení dotazů na */API* cestu, aby se předešlo kolizím s řadiči MVC. Pokud potřebujete toto nastavení změnit, přečtěte si téma [směrování ve webovém rozhraní API ASP.NET](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md).

<a id="Ex3Task2"></a>
#### <a name="task-2--running-the-solution"></a>Úloha 2 – spuštění řešení

V této úloze budete pomocí **vývojářských nástrojů** pro Internet Explorer F12 kontrolovat úplnou odpověď z kontroleru webového rozhraní API. Zjistíte, jak můžete zachytit síťový provoz a získat tak lepší přehled o datech aplikace.

> [!NOTE]
> Ujistěte se, že je vybrána možnost **Internet Explorer** v nabídce **Start** , která je umístěna na panelu nástrojů sady Visual Studio.
> 
> ![Možnost aplikace Internet Explorer](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image27.png)
> 
> **Vývojářské nástroje F12** mají rozsáhlou sadu funkcí, která není pokrytá v tomto cvičení. Pokud se o něm chcete dozvědět víc, přečtěte si téma [použití vývojářských nástrojů F12](https://msdn.microsoft.com/library/ie/bg182326(v=vs.85)).

1. Stisknutím klávesy **F5** spusťte řešení.

    > [!NOTE]
    > Aby bylo možné tento úkol provést správně, musí mít aplikace data. Pokud je databáze prázdná, můžete se vrátit k úloze 3 v cvičení 2 a postupovat podle pokynů, jak vytvořit novou osobu pomocí zobrazení MVC.
2. Stisknutím klávesy **F12** v prohlížeči otevřete panel **vývojářské nástroje** . Stiskněte klávesu **CTRL** + **4** nebo klikněte na ikonu **sítě** a potom klikněte na zelenou šipku tlačítka a zahajte zachytávání síťového provozu.

    ![Inicializace zachycení sítě webového rozhraní API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image28.png "Inicializace zachycení sítě webového rozhraní API")

    *Inicializace zachycení sítě webového rozhraní API*
3. **Rozhraní API nebo ApiPerson** přidejte k adrese URL v adresním řádku prohlížeče. Nyní budete kontrolovat podrobnosti odpovědi z **ApiPersonController**.

    ![Načítání dat osob prostřednictvím webového rozhraní API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image29.png "Načítání dat osob prostřednictvím webového rozhraní API")

    *Načítání dat osob prostřednictvím webového rozhraní API*

    > [!NOTE]
    > Po dokončení stahování se zobrazí výzva k provedení akce se staženým souborem. Nechejte dialogové okno otevřené, aby bylo možné sledovat obsah odpovědi prostřednictvím okna nástrojů pro vývojáře.
4. Nyní budete kontrolovat text odpovědi. Chcete-li to provést, klikněte na kartu **Podrobnosti** a pak klikněte na **text odpovědi**. Můžete kontrolovat, že stažená data jsou seznam objektů s **ID**vlastností, **názvem** a **stářím** , které odpovídají třídě **Person** .

    ![Zobrazení textu odpovědi webového rozhraní API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image30.png "Zobrazení textu odpovědi webového rozhraní API")

    *Zobrazení textu odpovědi webového rozhraní API*

<a id="Ex3Task3"></a>
#### <a name="task-3--adding-web-api-help-pages"></a>Úloha 3 – přidání stránek s usnadněním webového rozhraní API

Při vytváření webového rozhraní API je užitečné vytvořit stránku s přehledem, aby ostatní vývojáři věděli, jak vaše rozhraní API volat. Stránky dokumentace můžete vytvořit a aktualizovat ručně, ale je lepší je vygenerovat automaticky, aby nedocházelo k nutnosti provádět údržbu. V této úloze použijete balíček NuGet k automatickému generování stránek s webovým rozhraním API na řešení.

1. V nabídce **nástroje** v aplikaci Visual Studio vyberte **Správce balíčků NuGet**a pak klikněte na **Konzola správce balíčků**.
2. V okně **konzoly Správce balíčků** spusťte následující příkaz:

    [!code-powershell[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample7.ps1)]

    > [!NOTE]
    > Balíček **Microsoft. ASPNET. WebApi. HelpPage** nainstaluje nezbytná sestavení a přidá zobrazení MVC pro stránky s nápovědu ve složce **oblasti/HelpPage** .

    ![Oblast HelpPage](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image31.png "Oblast HelpPage")

    *Oblast HelpPage*
3. Ve výchozím nastavení mají stránky pro nápovědu zástupné řetězce pro dokumentaci. Pomocí dokumentačních komentářů XML můžete vytvořit dokumentaci. Pokud chcete tuto funkci povolit, otevřete soubor **HelpPageConfig.cs** umístěný v **oblasti/HelpPage/App\_Start** a odkomentujte následující řádek:

    [!code-javascript[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample8.js)]
4. V **Průzkumník řešení**klikněte pravým tlačítkem na projekt **MyHybridSite**, vyberte **vlastnosti** a klikněte na kartu **sestavení** .

    ![Karta sestavení](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image32.png "Oddíl Build")

    *Karta sestavení*
5. V části **výstup**vyberte **soubor dokumentace XML**. Do pole pro úpravy zadejte **App\_data/XmlDocument. XML**.

    ![Oddíl Output na kartě sestavení](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image33.png "Oddíl Output na kartě sestavení")

    *Oddíl Output na kartě sestavení*
6. Změny uložte stisknutím **kombinace kláves CTRL** + **S** .
7. Otevřete soubor **ApiPersonController.cs** ze složky **Controllers** .
8. Zadejte nový řádek mezi podpisem metody *getlidech* a *//Get API/ApiPerson* a pak zadejte tři lomítka.

    > [!NOTE]
    > Visual Studio automaticky vloží prvky XML, které definují dokumentaci k metodě.
9. Přidejte souhrnný text a návratovou hodnotu metody *getlidé* . Měl by vypadat nějak takto.

    [!code-csharp[Main](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/samples/sample9.cs)]
10. Stisknutím klávesy **F5** spusťte řešení.
11. Připojením **/help** k adrese URL v adresním řádku přejdete na stránku s usnadněním.

    ![Stránka s webovou pomocí rozhraní API pro ASP.NET](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image34.png "Stránka s webovou pomocí rozhraní API pro ASP.NET")

    *Stránka s webovou pomocí rozhraní API pro ASP.NET*

    > [!NOTE]
    > Hlavním obsahem stránky je tabulka rozhraní API seskupených podle kontroleru. Položky tabulky jsou generovány dynamicky pomocí rozhraní **IApiExplorer** . Pokud přidáte nebo aktualizujete kontroler rozhraní API, tabulka se automaticky aktualizuje při příštím sestavení aplikace.
    > 
    > Sloupec **rozhraní API** obsahuje metodu HTTP a relativní identifikátor URI. Sloupec **Description** obsahuje informace, které byly extrahovány z dokumentace metody.
12. Všimněte si, že popis, který jste přidali nad definici metody, se zobrazí ve sloupci Popis.

    ![Popis metody rozhraní API](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image35.png "Popis metody rozhraní API")

    *Popis metody rozhraní API*
13. Klikněte na jednu z metod rozhraní API a přejděte na stránku s podrobnějšími informacemi, včetně ukázkových těl odpovědí.

    ![Stránka podrobností o podrobnostech](one-aspnet-integrating-aspnet-web-forms-mvc-and-web-api/_static/image36.png "Stránka podrobností o podrobnostech")

    *Stránka podrobné informace*

---

<a id="Summary"></a>
## <a name="summary"></a>Souhrn

Vyplněním tohoto praktického cvičení jste se dozvěděli, jak:

- Vytvořte novou webovou aplikaci s využitím jednoho ASP.NET prostředí v Visual Studio 2013
- Integrujte několik ASP.NET technologií do jednoho jediného projektu.
- Generování řadičů a zobrazení MVC z tříd modelu pomocí generování uživatelského rozhraní ASP.NET
- Generování řadičů webového rozhraní API, které využívají funkce jako asynchronní programování a přístup k datům prostřednictvím Entity Framework
- Automatické generování stránek s nápovědu k webovému rozhraní API pro vaše řadiče

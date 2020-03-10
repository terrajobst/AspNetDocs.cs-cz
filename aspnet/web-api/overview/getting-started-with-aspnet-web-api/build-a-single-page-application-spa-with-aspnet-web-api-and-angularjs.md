---
uid: web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
title: 'Praktická cvičení: vytvoření jednostránkové aplikace (SPA) pomocí webového rozhraní API ASP.NET a úhlů. js – ASP.NET 4. x'
author: rick-anderson
description: 'Krok za krokem: sestavení jednostránkové aplikace (SPA) pomocí webového rozhraní API ASP.NET a úhlů. js pro ASP.NET 4. x.'
ms.author: riande
ms.date: 09/30/2015
ms.custom: seoapril2019
ms.assetid: 719727b7-bef3-45ad-bfe9-ba5bcdb2305f
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs
msc.type: authoredcontent
ms.openlocfilehash: 86833a890da759e489dd11dc9afb128a9b7a75e3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557041"
---
# <a name="hands-on-lab-build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs"></a>Praktické cvičení: Sestavení jednostránkové aplikace (SPA) pomocí webového rozhraní API ASP.NET a Angular.js

podle [týmu webového Campy](https://twitter.com/webcamps)

[Stáhnout web Campy Training Kit](https://aka.ms/webcamps-training-kit)

Tato praktická cvičení vám ukáže, jak vytvořit jednostránkové aplikace (SPA) s webovým rozhraním API ASP.NET a úhlů. js pro ASP.NET 4. x.

V tomto předem dostupném testovacím prostředí využijete tyto technologie k implementaci informatik kvízu, minihry webu založeného na principu SPA. Nejdříve implementujete vrstvu služby s webovým rozhraním API ASP.NET k vystavení požadovaných koncových bodů pro získání otázek kvízu a uložení odpovědí. Pak vytvoříte uživatelské rozhraní s bohatou a reagují pomocí transformačních efektů AngularJS a CSS3.

V tradičních webových aplikacích klient (prohlížeč) iniciuje komunikaci se serverem tím, že požaduje stránku. Server potom zpracuje požadavek a pošle kód HTML stránky klientovi. V následných interakcích se stránkou, třeba uživatel přejde na odkaz nebo odešle formulář s daty – nový požadavek se pošle na server a tok se znovu spustí: Server žádost zpracuje a pošle nové stránce do prohlížeče v reakci na novou žádost o akci. Ed klientem.
> 
> V aplikacích s jednou stránkou (jednostránkové) je celá stránka načtena do prohlížeče po počátečním požadavku, ale následné interakce probíhají prostřednictvím požadavků AJAX. To znamená, že prohlížeč musí aktualizovat pouze část stránky, která se změnila. není nutné znovu načítat celou stránku. Přístup přes zabezpečené ověřování pomocí hesla zkracuje dobu, kterou aplikace reaguje na akce uživatelů, což vede k většímu množství zážitku z více kapalin.
> 
> Architektura zabezpečeného hesla zahrnuje některé výzvy, které nejsou přítomné v tradičních webových aplikacích. Ale vznikající technologie, jako jsou webové rozhraní API ASP.NET, rozhraní JavaScript, jako je AngularJS a nové funkce stylů poskytované CSS3, usnadňují návrh a sestavování jednostránkové.
> 
> 
> Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici na adrese [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).

## <a name="overview"></a>Přehled

<a id="Objectives"></a>
### <a name="objectives"></a>Cíle

V této praktické laboratorní laboratoři se dozvíte, jak:

- Vytvoření služby webového rozhraní API ASP.NET pro odesílání a příjem dat JSON
- Vytvoření uživatelského rozhraní s odezvou pomocí AngularJS
- Vylepšení uživatelského prostředí pomocí transformací CSS3

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Předpoklady

Následující postup je nutný k dokončení tohoto praktického laboratorního prostředí:

- [Visual Studio Express 2013 pro web](https://www.microsoft.com/visualstudio/) nebo více

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

1. [Vytvoření webového rozhraní API](#Exercise1)
2. [Vytvoření rozhraní SPA](#Exercise2)

Odhadovaný čas dokončení tohoto testovacího prostředí: **60 minut**

> [!NOTE]
> Při prvním spuštění sady Visual Studio je nutné vybrat jednu z předdefinovaných kolekcí nastavení. Každá předdefinovaná kolekce je navržena tak, aby odpovídala konkrétnímu stylu vývoje a určuje rozložení oken, chování editoru, fragmenty kódu technologie IntelliSense a možnosti dialogového okna. Postupy v tomto testovacím prostředí popisují akce, které jsou nezbytné k provedení daného úkolu v sadě Visual Studio při použití kolekce **Obecné vývojové nastavení** . Pokud zvolíte pro vývojové prostředí jinou kolekci nastavení, mohou být v krocích, které byste měli vzít v úvahu, rozdíly.

<a id="Exercise1"></a>
### <a name="exercise-1-creating-a-web-api"></a>Cvičení 1: Vytvoření webového rozhraní API

Jednou z klíčových částí zabezpečeného hesla je vrstva služby. Zodpovídá za zpracování volání AJAX odeslaných uživatelským rozhraním a vrací data jako odpověď na dané volání. Načtená data by měla být prezentována v strojově čitelném formátu, aby je bylo možné analyzovat a spotřebovat klientem.

Rozhraní Web API je součástí sady ASP.NET stack a je navržena tak, aby usnadnila implementaci služeb HTTP, což obvykle odesílá a přijímá data ve formátu JSON nebo XML prostřednictvím rozhraní RESTful API. V tomto cvičení vytvoříte web pro hostování aplikace informatik kvíz a pak implementujete back-end službu, která bude zveřejňovat a uchovávat data kvízu pomocí webového rozhraní API ASP.NET.

<a id="Ex1Task1"></a>
#### <a name="task-1--creating-the-initial-project-for-geek-quiz"></a>Úloha 1 – vytvoření počátečního projektu pro informatik kvíz

V této úloze začnete vytvářet nový projekt ASP.NET MVC s podporou ASP.NET webového rozhraní API založenou na jednom typu projektu **ASP.NET** , který je součástí sady Visual Studio. **Jedna ASP.neta** sjednocuje všechny technologie ASP.NET a dává vám možnost je podle potřeby kombinovat a odpovídat. Pak přidáte třídy modelů Entity Framework a inicializátor databáze pro vložení otázek kvízu.

1. Otevřete **Visual Studio Express 2013 pro web** a vyberte **soubor | Nový projekt...** pro spuštění nového řešení.

    ![Vytvoření nového projektu](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image1.png "Vytvoření nového projektu")

    *Vytvoření nového projektu*
2. V dialogovém okně **Nový projekt** vyberte v části vizuál  **C# možnost Webová aplikace v ASP.NET | Karta web** . Ujistěte se, že je vybraná možnost **.NET Framework 4,5** , pojmenujte ji *GeekQuiz*, vyberte **umístění** a klikněte na **OK**.

    ![Vytvoření nového projektu webové aplikace v ASP.NET](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image2.png "Vytvoření nového projektu webové aplikace v ASP.NET")

    *Vytvoření nového projektu webové aplikace v ASP.NET*
3. V dialogovém okně **Nový projekt ASP.NET** vyberte šablonu **MVC** a vyberte možnost **webové rozhraní API** . Také se ujistěte, že je možnost **ověřování** nastavena na **jednotlivé uživatelské účty**. Pokračujte kliknutím na tlačítko **OK** .

    ![Vytvoření nového projektu pomocí šablony MVC, včetně komponent webového rozhraní API](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image3.png)

    *Vytvoření nového projektu pomocí šablony MVC, včetně komponent webového rozhraní API*
4. V **Průzkumník řešení**klikněte pravým tlačítkem na složku **modely** projektu **GeekQuiz** a vyberte **Přidat | Existující položka...** .

    ![Přidání existující položky](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image4.png "Přidání existující položky")

    *Přidání existující položky*
5. V dialogovém okně **Přidat existující položku** přejděte do složky **source/assets/modely** a vyberte všechny soubory. Klikněte na **Přidat**.

    ![Přidání prostředků modelu](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image5.png "Přidání prostředků modelu")

    *Přidání prostředků modelu*

    > [!NOTE]
    > Přidáním těchto souborů přidáte datový model, kontext databáze Entity Framework a inicializátor databáze pro aplikaci kvíz pro informatik.
    > 
    > **Entity Framework (EF)** je objektově-relační MAPOVAČ (ORM), který umožňuje vytvářet aplikace pro přístup k datům pomocí programování s modelem konceptuální aplikace namísto programování přímo pomocí schématu relačního úložiště. Další informace o Entity Framework najdete [tady](../../../entity-framework.md).
    > 
    > Následuje popis tříd, které jste právě přidali:
    > 
    > - **TriviaOption:** představuje jednu možnost přidruženou k otázce kvízu.
    > - **TriviaQuestion:** představuje otázku kvízu a zpřístupňuje přidružené možnosti prostřednictvím vlastnosti **Options** .
    > - **TriviaAnswer:** představuje možnost vybranou uživatelem v reakci na dotaz kvízu.
    > - **TriviaContext:** představuje kontext databáze Entity Framework aplikace kvízu informatik. Tato třída je odvozena z **DContext** a zpřístupňuje vlastnosti **negenerickými** , které reprezentují kolekce výše popsaných entit.
    > - **TriviaDatabaseInitializer:** implementace inicializátoru Entity Framework pro třídu **TriviaContext** , která dědí z **metodu createdatabaseifnotexists**. Výchozím chováním této třídy je vytvoření databáze pouze v případě, že neexistuje, vložením entit uvedených v metodě **osazení** .
6. Otevřete soubor **Global.asax.cs** a přidejte následující příkaz using.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample1.cs)]
7. Přidejte následující kód na začátek **aplikace\_metodu Start** , chcete-li nastavit **TriviaDatabaseInitializer** jako inicializátor databáze.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample2.cs)]
8. Upravte **Domovský** kontroler tak, aby omezil přístup k ověřeným uživatelům. Provedete to tak, že otevřete soubor **HomeController.cs** ve složce **Controllers** a přidáte atribut **autorizovat** do definice třídy **HomeController** .

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample3.cs)]

    > [!NOTE]
    > Filtr **autorizace** ověří, jestli je uživatel ověřený. Pokud uživatel není ověřený, vrátí stavový kód HTTP 401 (Neautorizováno) bez vyvolání akce. Filtr můžete použít globálně, na úrovni řadiče nebo na úrovni jednotlivých akcí.
9. Nyní budete přizpůsobovat rozložení webových stránek a značky. Provedete to tak, že otevřete soubor **\_layout. cshtml** v **zobrazeních | Sdílená** složka a aktualizace obsahu **&lt;název&gt;** elementu nahrazením *aplikace ASP.NET* pomocí *kvízu informatik*.

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample4.cshtml)]
10. Ve stejném souboru aktualizujte navigační panel tak, že odeberete odkazy *About* a *Contact* a přejmenujete odkaz *Domů* na *Přehrát*. Dále přejmenujte odkaz *název aplikace* na *informatik kvíz*. HTML pro navigační panel by měl vypadat podobně jako následující kód.

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample5.cshtml)]
11. Aktualizujte zápatí stránky rozložení tak, že nahradíte *moji aplikaci ASP.NET* pomocí *informatik kvízu*. Chcete-li to provést, nahraďte obsah **&gt;elementu&lt;zápatí** následujícím zvýrazněným kódem.

    [!code-html[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample6.html)]

<a id="Ex1Task2"></a>
#### <a name="task-2--creating-the-triviacontroller-web-api"></a>Úloha 2 – Vytvoření webového rozhraní API TriviaController

V předchozí úloze jste vytvořili počáteční strukturu webové aplikace informatik kvíz. Nyní vytvoříte jednoduchou službu webového rozhraní API, která spolupracuje s datovým modelem kvízu a zpřístupňuje tyto akce:

- **Get/API/Trivia**: načte další otázku ze seznamu kvízu, na kterou má ověřený uživatel odpověď.
- **Post/API/Trivia**: ukládá odpověď kvízu určenou ověřeným uživatelem.

K vytvoření směrného plánu pro třídu kontroleru webového rozhraní API použijete nástroje pro generování uživatelského rozhraní ASP.NET, které nabízí Visual Studio.

1. Otevřete soubor **WebApiConfig.cs** ve složce **App\_Start** . Tento soubor definuje konfiguraci služby webového rozhraní API, například jak jsou trasy namapované na akce kontroleru webového rozhraní API.
2. Na začátek souboru přidejte následující příkaz using.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample7.cs)]
3. Přidejte následující zvýrazněný kód do metody **Register** pro globální konfiguraci formátovacího modulu pro data JSON načtené metodami akce webového rozhraní API.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample8.cs)]

    > [!NOTE]
    > **CamelCasePropertyNamesContractResolver** automaticky převede názvy vlastností na velikost písmen *ve stylu CamelCase* , což je obecná konvence pro názvy vlastností v JavaScriptu.
4. V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku **řadiče** projektu **GeekQuiz** a vyberte **Přidat | Nová vygenerovaná položka...**

    ![Vytvoření nové vygenerované položky](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image6.png "Vytvoření nové vygenerované položky")

    *Vytvoření nové vygenerované položky*
5. V dialogovém okně **Přidat generování uživatelského rozhraní** se ujistěte, že je v levém podokně vybrán **běžný** uzel. Pak v prostředním podokně vyberte položku **řadič Web API 2 – prázdná** šablona a klikněte na **Přidat**.

    ![Výběr prázdné šablony ovladače webového rozhraní API 2](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image7.png "Výběr prázdné šablony ovladače webového rozhraní API 2")

    *Výběr prázdné šablony ovladače webového rozhraní API 2*

    > [!NOTE]
    > **Generování uživatelského rozhraní ASP.NET** je rozhraní pro generování kódu pro webové aplikace v ASP.NET. Visual Studio 2013 obsahuje předem instalované generátory kódu pro MVC a projekty webového rozhraní API. V projektu byste měli použít generování uživatelského rozhraní, pokud chcete rychle přidat kód, který komunikuje s datovými modely, aby se snížila doba potřebná k vývoji standardních datových operací.
    > 
    > Proces generování uživatelského rozhraní také zajišťuje, že všechny požadované závislosti jsou nainstalovány v projektu. Například pokud začnete s prázdným projektem ASP.NET a potom použijete generování uživatelského rozhraní pro přidání kontroleru webového rozhraní API, do projektu se automaticky přidají požadované balíčky a odkazy na webové rozhraní API NuGet.
6. V dialogovém **okně Přidat řadič** zadejte do textového pole **název kontroleru** *TriviaController* a klikněte na **Přidat**.

    ![Přidání kontroleru minihry](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image8.png "Přidání kontroleru minihry")

    *Přidání kontroleru minihry*
7. Soubor **TriviaController.cs** se pak přidá do složky **Controllers** projektu **GeekQuiz** , který obsahuje prázdnou třídu **TriviaController** . Na začátek souboru přidejte následující příkazy using.

    (Fragment kódu – *AspNetWebApiSpa-EX1-TriviaControllerUsings*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample9.cs)]
8. Přidejte následující kód na začátek třídy **TriviaController** k definování, inicializaci a uvolnění instance **TriviaContext** v řadiči.

    (Fragment kódu – *AspNetWebApiSpa-EX1-TriviaControllerContext*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample10.cs)]

    > [!NOTE]
    > Metoda **Dispose** **TriviaController** vyvolá metodu **Dispose** instance **TriviaContext** , která zajistí, že všechny prostředky používané kontextovým objektem jsou uvolněny, když je instance **TriviaContext** vyřazena nebo uvolňována paměti. To zahrnuje uzavírání všech databázových připojení, která jsou otevřená Entity Framework.
9. Na konec třídy **TriviaController** přidejte následující pomocnou metodu. Tato metoda načte následující kvíz z databáze, na kterou bude odpovědět zadaný uživatel.

    (Fragment kódu – *AspNetWebApiSpa-EX1-TriviaControllerNextQuestion*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample11.cs)]
10. Do třídy **TriviaController** přidejte následující metodu **Get** Action. Tato metoda akce volá pomocnou metodu **NextQuestionAsync** definovanou v předchozím kroku k načtení další otázky pro ověřeného uživatele.

    (Fragment kódu – *AspNetWebApiSpa-EX1-TriviaControllerGetAction*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample12.cs)]
11. Na konec třídy **TriviaController** přidejte následující pomocnou metodu. Tato metoda uloží zadanou odpověď v databázi a vrátí hodnotu typu Boolean, která označuje, zda je odpověď správná.

    (Fragment kódu – *AspNetWebApiSpa-EX1-TriviaControllerStoreAsync*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample13.cs)]
12. Přidejte následující metodu **post** Action do třídy **TriviaController** . Tato metoda akce přidružuje odpověď k ověřenému uživateli a zavolá pomocnou metodu **StoreAsync** . Pak pošle odpověď s logickou hodnotou vrácenou pomocnou metodou.

    (Fragment kódu – *AspNetWebApiSpa-EX1-TriviaControllerPostAction*)

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample14.cs)]
13. Upravte kontroler webového rozhraní API tak, aby omezil přístup k ověřeným uživatelům přidáním atributu **autorizace** do definice třídy **TriviaController** .

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample15.cs)]

<a id="Ex1Task3"></a>
#### <a name="task-3--running-the-solution"></a>Úloha 3 – spuštění řešení

V této úloze ověříte, že služba webového rozhraní API, kterou jste vytvořili v předchozím úkolu, funguje podle očekávání. K zaznamenání síťového provozu a kontrole úplné odezvy ze služby webového rozhraní API použijete Vývojářské nástroje Internet Explorer **F12** .

> [!NOTE]
> Ujistěte se, že je vybrána možnost **Internet Explorer** v nabídce **Start** , která je umístěna na panelu nástrojů sady Visual Studio.
> 
> ![Možnost aplikace Internet Explorer](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image9.png)

1. Stisknutím klávesy **F5** spusťte řešení. **Přihlašovací** stránka by se měla zobrazit v prohlížeči.

    > [!NOTE]
    > Po spuštění aplikace se aktivuje výchozí trasa MVC, která je ve výchozím nastavení namapována na akci **indexu** třídy **HomeController** . Vzhledem k tomu, že **HomeController** je omezen na ověřené uživatele (Nezapomeňte, že jste tuto třídu upravovali pomocí atributu **autorizovat** v cvičení 1) a zatím není ověřeno žádného uživatele, aplikace přesměruje původní požadavek na přihlašovací stránku.

    ![Spuštění řešení](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image10.png "Spuštění řešení")

    *Spuštění řešení*
2. Kliknutím na **zaregistrovat** vytvořte nového uživatele.

    ![Registrace nového uživatele](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image11.png "Registrace nového uživatele")

    *Registrace nového uživatele*
3. Na stránce **zaregistrovat** zadejte **uživatelské jméno** a **heslo**a potom klikněte na **zaregistrovat**.

    ![Registrovat stránku](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image12.png "Registrovat stránku")

    *Registrovat stránku*
4. Aplikace registruje nový účet a uživatel je ověřený a přesměrován zpět na domovskou stránku.

    ![Uživatel je ověřený.](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image13.png "Ověřeno uživatelem")

    *Uživatel je ověřený.*
5. Stisknutím klávesy **F12** v prohlížeči otevřete panel **vývojářské nástroje** . Stiskněte **kombinaci kláves CTRL + 4** nebo klikněte na ikonu **sítě** a potom kliknutím na zelenou šipku začněte zachytávání síťového provozu.

    ![Inicializace zachycení sítě webového rozhraní API](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image14.png "Inicializace zachycení sítě webového rozhraní API")

    *Inicializace zachycení sítě webového rozhraní API*
6. **Rozhraní API nebo minihry** přidejte k adrese URL v adresním řádku prohlížeče. Nyní si můžete prohlédnout podrobnosti odpovědi z metody **Get** Action v **TriviaController**.

    ![Načítání dat dalších otázek prostřednictvím webového rozhraní API](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image15.png "Načítání dat dalších otázek prostřednictvím webového rozhraní API")

    *Načítání dat dalších otázek prostřednictvím webového rozhraní API*

    > [!NOTE]
    > Po dokončení stahování se zobrazí výzva k provedení akce se staženým souborem. Nechejte dialogové okno otevřené, aby bylo možné sledovat obsah odpovědi prostřednictvím okna nástrojů pro vývojáře.
7. Nyní budete kontrolovat text odpovědi. Chcete-li to provést, klikněte na kartu **Podrobnosti** a pak klikněte na **text odpovědi**. Můžete kontrolovat, zda jsou stažená data objekt s **možnostmi** vlastností (což je seznam objektů **TriviaOption** ), **ID** a **název** odpovídající třídě **TriviaQuestion** .

    ![Zobrazení textu odpovědi webového rozhraní API](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image16.png "Zobrazení textu odpovědi webového rozhraní API")

    *Zobrazení textu odpovědi webového rozhraní API*
8. Vraťte se do sady Visual Studio a stisknutím klávesy **SHIFT + F5** Zastavte ladění.

<a id="Exercise2"></a>
### <a name="exercise-2-creating-the-spa-interface"></a>Cvičení 2: vytvoření rozhraní SPA

V tomto cvičení budete nejdřív sestavovat webovou front-end část informatik kvízu, která se zaměřuje na interakci jednostránkové aplikace pomocí **AngularJS**. Pak budete moct zlepšit uživatelské prostředí pomocí CSS3 a zajistit tak bohatou animaci a nabídnout vizuální efekt přepínání kontextu při přechodu z jedné otázky na další.

<a id="Ex2Task1"></a>
#### <a name="task-1--creating-the-spa-interface-using-angularjs"></a>Úloha 1 – Vytvoření rozhraní zabezpečeného hesla pomocí AngularJS

V této úloze použijete **AngularJS** k implementaci klientské strany aplikace informatik kvízu. **AngularJS** je open source rozhraní JavaScript, které rozšiřuje aplikace založené na prohlížeči pomocí funkce MVC ( *Model-View-Controller* ) a usnadňuje vývoj a testování.

Začnete tím, že nainstalujete AngularJS z konzoly Správce balíčků sady Visual Studio. Pak vytvoříte kontroler, který bude poskytovat chování aplikace informatik kvíz, a zobrazení a vykreslit otázky kvízu a odpovědi pomocí modulu šablony AngularJS.

> [!NOTE]
> Další informace o AngularJS najdete v tématu [[http://angularjs.org/](http://angularjs.org/)](http://angularjs.org/).

1. Otevřete **Visual Studio Express 2013 pro web** a otevřete řešení **GeekQuiz. sln** nacházející se ve složce **source/EX2-CreatingASPAInterface/Begin** . Případně můžete pokračovat v řešení, které jste získali v předchozím cvičení.
2. Otevřete **konzolu Správce balíčků** z **nástrojů** > **Správce balíčků NuGet**. Zadáním následujícího příkazu nainstalujte balíček NuGet **AngularJS. Core** .

    [!code-powershell[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample16.ps1)]
3. V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku **skripty** projektu **GeekQuiz** a vyberte **Přidat | Nová složka**. Pojmenujte **aplikaci** složky a stiskněte klávesu **ENTER**.
4. Klikněte pravým tlačítkem na složku **aplikace** , kterou jste právě vytvořili, a vyberte **Přidat | JavaScriptový soubor**.

    ![Vytvoření nového souboru JavaScriptu](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image17.png)

    *Vytvoření nového souboru JavaScriptu*
5. V dialogovém okně **Zadejte název pro položku** zadejte do textového pole **název položky** *Test Controller* a klikněte na **OK**.

    ![Pojmenování nového souboru JavaScriptu](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image18.png)

    *Pojmenování nového souboru JavaScriptu*
6. V souboru **Quiz-Controller. js** přidejte následující kód, který deklaruje a inicializuje kontroler **QuizCtrl** AngularJS.

    (Fragment kódu – *AspNetWebApiSpa-EX2-AngularQuizController*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample17.js)]

    > [!NOTE]
    > Funkce konstruktoru kontroleru **QuizCtrl** očekává, že je k **dis$Scope**parametr s názvem. Počáteční stav oboru by měl být nastaven ve funkci konstruktoru připojením vlastností k objektu **$Scope** . Vlastnosti obsahují **model zobrazení**a budou k dispozici pro šablonu při registraci kontroleru.
    > 
    > Kontroler **QuizCtrl** je definovaný v modulu s názvem **QuizApp**. Moduly jsou jednotky práce, které umožňují rozdělit aplikaci na samostatné součásti. Hlavní výhodou použití modulů je, že kód je snazší pochopit a usnadňuje testování částí, jejich použitelnost a udržovatelnost.
7. Nyní přidáte chování do oboru, aby bylo možné reagovat na události aktivované v zobrazení. Přidejte následující kód na konec kontroleru **QuizCtrl** k definování funkce **nextQuestion** v objektu **$Scope** .

    (Fragment kódu – *AspNetWebApiSpa-EX2-AngularQuizControllerNextQuestion*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample18.js)]

    > [!NOTE]
    > Tato funkce načte další otázku z webového rozhraní API **minihry** vytvořené v předchozím cvičení a připojí data otázky k objektu **$Scope** .
8. Vložte následující kód na konec kontroleru **QuizCtrl** k definování funkce **sendAnswer** v objektu **$Scope** .

    (Fragment kódu – *AspNetWebApiSpa-EX2-AngularQuizControllerSendAnswer*)

    [!code-javascript[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample19.js)]

    > [!NOTE]
    > Tato funkce pošle odpověď vybranou uživatelem k webovému rozhraní API **minihry** a uloží výsledek – to znamená, že pokud odpověď je správná nebo ne – v objektu **$Scope** .
    > 
    > Funkce **nextQuestion** a **sendAnswer** shora výše používají objekt AngularJS **$http** k abstrakci komunikace s webovým rozhraním API prostřednictvím objektu XMLHttpRequest JavaScript z prohlížeče. AngularJS podporuje další službu, která přináší vyšší úroveň abstrakce k provádění operací CRUD na prostředku prostřednictvím rozhraní RESTful API. Objekt AngularJS **$Resource** obsahuje metody akcí, které poskytují chování vysoké úrovně, aniž by bylo nutné pracovat s objektem **$http** . Zvažte použití objektu **$Resource** ve scénářích, které vyžadují model CRUD (informace o popředí naleznete v [dokumentaci k $Resource](https://docs.angularjs.org/api/ngResource/service/$resource)).
9. Dalším krokem je vytvoření šablony AngularJS definující zobrazení kvízu. Provedete to tak, že otevřete soubor **index. cshtml** v **zobrazeních | Domovskou** složku a nahraďte obsah následujícím kódem.

    (Fragment kódu – *AspNetWebApiSpa-EX2-GeekQuizView*)

    [!code-cshtml[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample20.cshtml)]

    > [!NOTE]
    > Šablona AngularJS je deklarativní specifikace, která používá informace z modelu a řadiče pro transformaci statických značek do dynamického zobrazení, které uživatel vidí v prohlížeči. Níže jsou uvedeny příklady elementů AngularJS a atributů elementů, které lze použít v šabloně:
    > 
    > - Direktiva **NG-App** oznamuje elementu modelu DOM, který představuje kořenový prvek aplikace.
    > - Direktiva **NG-Controller** připojí řadič k modelu DOM v místě, kde je direktiva deklarována.
    > - Notace složené závorky **{{}}** označuje vazby na vlastnosti oboru definované v kontroleru.
    > - Direktiva **kliknutí na NG** se používá k vyvolání funkcí definovaných v oboru v reakci na kliknutí uživatele.
10. Otevřete soubor **Web. CSS** ve složce **obsahu** a přidejte na konec souboru následující zvýrazněné styly, aby se zobrazil vzhled a chování kvízu.

    (Fragment kódu – *AspNetWebApiSpa-EX2-GeekQuizStyles*)

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample21.css)]

<a id="Ex2Task2"></a>
#### <a name="task-2--running-the-solution"></a>Úloha 2 – spuštění řešení

V této úloze spustíte řešení pomocí nového uživatelského rozhraní, které jste vytvořili ve službě AngularJS, abyste odpověděli na některé otázky kvízu.

1. Stisknutím klávesy **F5** spusťte řešení.
2. Zaregistrujte nový uživatelský účet. K tomu použijte postup registrace popsaný v tématu cvičení 1, úloha 3.

    > [!NOTE]
    > Pokud používáte řešení z předchozího cvičení, můžete se přihlásit pomocí uživatelského účtu, který jste vytvořili dříve.
3. Zobrazí se **Domovská** stránka, která zobrazuje první otázku kvízu. Odpovězte na otázku kliknutím na jednu z možností. Tím se aktivuje dříve definovaná funkce **sendAnswer** , která pošle vybranou možnost webovému rozhraní API **minihry** .

    ![Zodpovězení otázky](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image19.png "Zodpovězení otázky")

    *Zodpovězení otázky*
4. Po kliknutí na jedno z tlačítek by se měla zobrazit odpověď. Kliknutím na **Další dotaz** zobrazíte následující otázku. Tím se aktivuje funkce **nextQuestion** definovaná v kontroleru.

    ![Požadavek na další otázku](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image20.png "Požadavek na další otázku")

    *Požadavek na další otázku*
5. Objeví se další otázka. Pokračujte v zodpovězení otázek tolikrát, kolikrát chcete. Po dokončení všech otázek, které byste měli vracet k první otázce.

    ![Další otázka](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image21.png "Další otázka")

    *Další otázka*
6. Vraťte se do sady Visual Studio a stisknutím klávesy **SHIFT + F5** Zastavte ladění.

<a id="Ex2Task3"></a>
#### <a name="task-3--creating-a-flip-animation-using-css3"></a>Úloha 3 – vytvoření překlápění animace pomocí CSS3

V této úloze použijete vlastnosti CSS3 k provádění bohatých animací přidáním efektu překlopení, když je otázka zodpovězená a když se načte další otázka.

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku **obsahu** projektu **GeekQuiz** a vyberte **Přidat | Existující položka...** .

    ![Přidání existující položky do složky obsahu](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image22.png "Přidání existující položky do složky obsahu")

    *Přidání existující položky do složky obsahu*
2. V dialogovém okně **Přidat existující položku** přejděte do složky **source/assets** a vyberte **převrátit. CSS**. Klikněte na **Přidat**.

    ![Přidání souboru překlopení. CSS z assetů](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image23.png "Přidání souboru překlopení. CSS z assetů")

    *Přidání souboru překlopení. CSS z assetů*
3. Otevřete soubor **překlopení. CSS** , který jste právě přidali, a prozkoumejte jeho obsah.
4. Vyhledejte komentář k **převrácení transformace** . Styly pod tímto komentářem používají **perspektivu** stylů CSS a **otočí** transformace k vygenerování &quot;překlopení&quot;ho efektu na kartu.

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample22.css)]
5. **Při překlápění komentáře Najděte podokno skrýt zpátky** . Styl, který je pod tímto komentářem, skryje zadní stranu objektů, pokud se z prohlížeče neodkazují, nastavením vlastnosti CSS pro **viditelnost** pozadí na hodnotu *skrytý*.

    [!code-css[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample23.css)]
6. Otevřete soubor **BundleConfig.cs** ve složce **App\_Start** a přidejte odkaz na soubor **překlopení. CSS** v sadě **&quot;~/Content/CSS&quot;** Style.

    [!code-csharp[Main](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/samples/sample24.cs)]
7. Stisknutím klávesy **F5** spusťte řešení a přihlaste se pomocí svých přihlašovacích údajů.
8. Odpovězte na otázku tak, že kliknete na jednu z možností. Všimněte si, že při přechodu mezi zobrazeními se projeví překlopení.

    ![Zodpovězení otázky pomocí překlápění efektu](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image24.png "Zodpovězení otázky pomocí překlápění efektu")

    *Zodpovězení otázky pomocí překlápění efektu*
9. Kliknutím na **Další dotaz** načtěte následující otázku. Efekt překlápění by se měl objevit znovu.

    ![Načítání následující otázky s efektem překlápění](build-a-single-page-application-spa-with-aspnet-web-api-and-angularjs/_static/image25.png "Načítání následující otázky s efektem překlápění")

    *Načítání následující otázky s efektem překlápění*

---

<a id="Summary"></a>
## <a name="summary"></a>Souhrn

Vyplněním tohoto praktického cvičení jste se dozvěděli, jak:

- Vytvoření kontroleru webového rozhraní API ASP.NET pomocí generování uživatelského rozhraní ASP.NET
- Implementací akce webového rozhraní API načíst další otázku kvízu
- Implementace akce post webového rozhraní API pro uložení odpovědí kvízu
- Instalace AngularJS z konzoly Správce balíčků sady Visual Studio
- Implementace šablon a řadičů AngularJS
- Použití přechodů CSS3 k provádění animačních efektů

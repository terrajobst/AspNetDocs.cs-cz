---
uid: mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
title: Co je nového v ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: ASP.NET MVC 4 je architektura pro vytváření škálovatelných webových aplikací založených na standardech pomocí dobře zavedených vzorů návrhu a síly ASP.NET a...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 48f7feb3-872f-485d-b96f-e30011ff8c4a
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/whats-new-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 4235f4fe666cdeb7d0821127a2b349f2ff30cd6e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539436"
---
# <a name="whats-new-in-aspnet-mvc-4"></a>Novinky v ASP.NET MVC 4

podle [týmu webového Campy](https://twitter.com/webcamps)

[Stáhnout web Campy Training Kit](https://aka.ms/webcamps-training-kit)

ASP.NET MVC 4 je architektura pro vytváření škálovatelných webových aplikací založených na standardech pomocí dobře zavedených vzorů návrhu a síly ASP.NET a rozhraní .NET Framework. Tato nová, čtvrtá verze rozhraní se zaměřuje na snazší vývoj mobilních webových aplikací.

Pokud chcete začít s, při vytváření nového projektu ASP.NET MVC 4 je teď šablona projektu mobilní aplikace, kterou můžete použít k vytvoření samostatné aplikace speciálně pro mobilní zařízení. Kromě toho ASP.NET MVC 4 integruje s jQuery Mobile prostřednictvím balíčku NuGet jQuery. Mobile. MVC. jQuery Mobile je architektura založená na HTML5 pro vývoj webových aplikací, které jsou kompatibilní se všemi oblíbenými platformami mobilních zařízení, včetně Windows Phone, iPhone, Androidu a tak dále. Pokud však budete potřebovat specializaci, ASP.NET MVC 4 také umožňuje obsluhovat různá zobrazení různých zařízení a poskytovat optimalizace pro konkrétní zařízení.

V tomto praktickém cvičení začnete s ASP.NET MVC 4 &quot;Internet Application&quot; šablona projektu pro vytvoření aplikace Fotogalerie. Pomocí nových funkcí jQuery Mobile a ASP.NET MVC 4 budete aplikaci postupně rozšiřovat, aby byla kompatibilní s různými mobilními zařízeními a webovými prohlížeči pro stolní počítače. Naučíte se také nové složení kódu pro generování kódu a to, jak ASP.NET MVC 4 usnadňuje psaní asynchronních metod akcí díky podpoře úloh&lt;ActionResult&gt; návratových typů.

> [!NOTE]
> Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici v [verzích Microsoft-Web/WebCampTrainingKit](https://aka.ms/webcamps-training-kit). Projekt, který je specifický pro toto testovací prostředí, je k dispozici v části [novinky webových formulářů v ASP.NET 4,5](https://github.com/Microsoft-Web/HOL-ASPNETWebForms).

<a id="Objectives"></a>
### <a name="objectives"></a>Cíle

V této praktické laboratorní laboratoři se dozvíte, jak:

- Využijte výhod vylepšení šablon projektů ASP.NET MVC – včetně nové šablony projektu mobilní aplikace
- Použití atributů zobrazení HTML5 a dotazů na média šablon stylů CSS ke zlepšení zobrazení na mobilních zařízeních
- Použití jQuery Mobile pro progresivní vylepšení a vytváření webového uživatelského rozhraní optimalizovaného pro dotykové ovládání
- Vytváření zobrazení specifických pro mobilní zařízení
- Přepínání mezi zobrazeními mobilních a desktopových aplikací v aplikaci pomocí součásti pro přepínání zobrazení
- Vytváření asynchronních řadičů pomocí podpory úloh

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Předpoklady

K dokončení tohoto testovacího prostředí musíte mít následující položky:

- [Microsoft Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) nebo nejvyšší (pokyny k instalaci najdete v [příloze B](#AppendixB) ).
- [ASP.NET MVC 4](../../../mvc4.md) (zahrnuté v instalaci Microsoft Visual Studio 2012)
- Emulátor Windows Phone (zahrnutý v [sadě Windows Phone 7.1.1 SDK](https://www.microsoft.com/download/details.aspx?id=29233))
- Volitelné – [WebMatrix 2](https://www.microsoft.com/web/webmatrix/) s **elektrickým rozšířením simulátoru Plum iPhone** (jenom pro cvičení 3 používá se k procházení webové aplikace pomocí simulátoru iPhone)

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a>Nastavení

V celém dokumentu testovacího prostředí budete vyzváni k vložení bloků kódu. Pro usnadnění práce je většina tohoto kódu poskytována jako fragmenty Visual Studio Code, které můžete použít v rámci sady Visual Studio, abyste se vyhnuli nutnosti je přidat ručně.

Instalace fragmentů kódu:

1. Otevřete okno Průzkumníka Windows a přejděte do složky **Source\Setup** testovacího prostředí.
2. Dvojím kliknutím na soubor **Setup. cmd** v této složce nainstalujete fragmenty kódu sady Visual Studio.

Pokud nejste obeznámeni s fragmentem Visual Studio Code a chcete se dozvědět, jak je používat, můžete odkazovat na přílohu z tohoto dokumentu &quot;[příloze A: používání fragmentů kódu](#AppendixA)&quot;.

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>Cvičení

Tato praktická cvičení zahrnují následující cvičení:

1. [Nové šablony projektů ASP.NET MVC 4](#Exercise1)
2. [Vytvoření webové aplikace Galerie fotografií](#Exercise2)
3. [Přidání podpory pro mobilní zařízení](#Exercise3)
4. [Použití asynchronních řadičů](#Exercise4)

> [!NOTE]
> Každé cvičení doprovází **koncovou** složku obsahující výsledné řešení, které byste měli získat po dokončení cvičení. Pokud potřebujete další nápovědu k práci prostřednictvím cvičení, můžete toto řešení použít jako vodítko.

Odhadovaný čas dokončení tohoto testovacího prostředí: **60 minut**.

<a id="Exercise1"></a>

<a id="Exercise_1_New_ASPNET_MVC_4_Project_Templates"></a>
### <a name="exercise-1-new-aspnet-mvc-4-project-templates"></a>Cvičení 1: nové šablony projektů ASP.NET MVC 4

V tomto cvičení budete zkoumat vylepšení v šablonách projektů ASP.NET MVC 4. Kromě šablony internetové aplikace, která je již přítomna v MVC 3, tato verze nyní obsahuje samostatnou šablonu pro mobilní aplikace. Nejprve se podíváte na některé relevantní funkce každé z těchto šablon. Pak budete pracovat s tím, jak správně vykreslovat stránku na různých platformách, pomocí správného přístupu.

<a id="Task_1_-_Exploring_the_Internet_Application_Template"></a>
#### <a name="task-1---exploring-the-internet-application-template"></a>Úloha 1 – prozkoumání šablony internetové aplikace

1. Otevřete **Visual Studio**.
2. Vyberte **soubor | Nové |** Příkaz nabídky projektu V dialogovém okně **Nový projekt** vyberte **vizuál C# | Webová** šablona ve stromu levého podokna a výběr **webové aplikace ASP.NET MVC 4.** Pojmenujte **fotogalerii**projektů, vyberte umístění (nebo ponechte výchozí) a klikněte na **OK**.

    > [!NOTE]
    > Později budete přizpůsobovat fotogalerii ASP.NET řešení MVC 4, které teď vytváříte.

    ![Vytvoření nového projektu](whats-new-in-aspnet-mvc-4/_static/image1.png "Vytvoření nového projektu")

    *Vytvoření nového projektu*
3. V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte šablonu projektu **Internetová aplikace** a klikněte na tlačítko **OK**. Ujistěte se, že jste vybrali Razor jako zobrazovací modul.

    ![Vytváří se nová internetová aplikace ASP.NET MVC 4.](whats-new-in-aspnet-mvc-4/_static/image2.png "Vytváří se nová internetová aplikace ASP.NET MVC 4.")

    *Vytváří se nová internetová aplikace ASP.NET MVC 4.*

    > [!NOTE]
    > Syntaxe Razor byla představena v ASP.NET MVC 3. Jeho cílem je minimalizovat počet znaků a klávesových úhozů vyžadovaných v souboru a povolit tak rychlé a kapalné pracovní postupy v kódování. Razor využívá stávající C# jazykové dovednosti/vb (nebo jiné) a poskytuje syntaxi značek šablony, která umožňuje pracovní postup pro vytváření kódu ve formátu Super HTML.
4. Stisknutím klávesy **F5** spusťte řešení a zobrazte obnovené šablony. Můžete se podívat na následující funkce:

    **Šablony moderního stylu**

    Šablony byly obnoveny, což poskytuje další styly pro moderní vzhled.

    ![Šablony přeformátované na ASP.NET MVC 4](whats-new-in-aspnet-mvc-4/_static/image3.png "Šablony s přestylem MVC 4")

    *Šablony přeformátované na ASP.NET MVC 4*

    ![Nová stránka kontaktu](whats-new-in-aspnet-mvc-4/_static/image4.png "Nová stránka kontaktu")

    *Nová stránka kontaktu*

    **Adaptivní vykreslování**

    Podívejte se na změnu velikosti okna prohlížeče a Všimněte si, jak se rozložení stránky dynamicky přizpůsobí nové velikosti okna. Tyto šablony používají techniku adaptivního vykreslování k tomu, aby se správně vykreslily na stolních i mobilních platformách bez jakýchkoli úprav.

    ![Šablona projektu ASP.NET MVC 4 v různých velikostech prohlížečů](whats-new-in-aspnet-mvc-4/_static/image5.png "Šablona projektu ASP.NET MVC 4 v různých velikostech prohlížečů")

    *Šablona projektu ASP.NET MVC 4 v různých velikostech prohlížečů*

    **Bohatší uživatelské rozhraní s JavaScriptem**

    Dalším vylepšením výchozích šablon projektů je použití JavaScriptu k poskytnutí interaktivního JavaScriptu. Odkazy na přihlášení a registraci použité v šabloně exemplify, jak použít ověřování jQuery k ověření vstupních polí ze strany klienta.

    ![Ověření jQuery](whats-new-in-aspnet-mvc-4/_static/image6.png)

    *Ověření jQuery*

    > [!NOTE]
    > Všimněte si dvou částí přihlášení. v první části se můžete přihlásit pomocí registrovaného účtu z lokality a v druhé části se můžete přihlásit pomocí jiné ověřovací služby, jako je Google (ve výchozím nastavení vypnuté).
5. Zavřete prohlížeč a ukončete ladicí program a vraťte se do sady Visual Studio.
6. Otevřete soubor **authconfig.cs** umístěný ve složce **App\_Start** .
7. Odebráním komentáře z posledního řádku zaregistrujete klienta Google pro ověřování *OAuth* .

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample1.cs)]

    > [!NOTE]
    > Všimněte si, že můžete snadno povolit ověřování pomocí kterékoli služby OpenID nebo OAuth, jako je Facebook, Twitter, Microsoft atd.
8. Stisknutím klávesy **F5** spusťte řešení a přejděte na přihlašovací stránku.
9. Vyberte službu **Google** , abyste se mohli přihlásit.

    ![Výběr služby přihlášení](whats-new-in-aspnet-mvc-4/_static/image7.png)

    *Výběr služby přihlášení*
10. Přihlaste se pomocí svého účtu Google.
11. Povolí, aby lokalita (localhost) načetla informace z účtu Google.
12. Nakonec se budete muset zaregistrovat na webu a přidružit k účtu Google.

   ![Přidružte svůj účet Google.](whats-new-in-aspnet-mvc-4/_static/image8.png)

   *Přidruží se Váš účet Google.*
13. Zavřete prohlížeč a ukončete ladicí program a vraťte se do sady Visual Studio.
14. Nyní Prozkoumejte řešení a podívejte se na některé další nové funkce, které byly zavedeny ASP.NET MVC 4 v šabloně projektu.

   ![Šablona projektu internetové aplikace ASP.NET MVC 4](whats-new-in-aspnet-mvc-4/_static/image9.png "Šablona projektu internetové aplikace ASP.NET MVC 4")

   *Šablona projektu internetové aplikace ASP.NET MVC 4*

    - **HTML 5 – označení**

       Procházejte zobrazením šablon a zjistěte nový kód motivu.

       ![Nová šablona s použitím značek Razor a HTML5 o. cshtml](whats-new-in-aspnet-mvc-4/_static/image10.png "Nová šablona s použitím značek Razor a HTML5 o. cshtml")

       *Nová šablona s použitím značek Razor a HTML5 (About. cshtml).*
    - **Aktualizované knihovny JavaScriptu**

       Výchozí šablona ASP.NET MVC 4 nyní zahrnuje KnockoutJS, MVVM rozhraní JavaScript, které umožňuje vytvářet bohatě a vysoce reagující webové aplikace pomocí JavaScriptu a HTML. Podobně jako v knihovnách uživatelského rozhraní MVC3, jQuery a jQuery jsou také zahrnuty v ASP.NET MVC 4.

     > [!NOTE]
     > Další informace o knihovně KnockOutJS můžete získat v tomto odkazu: [[http://learn.knockoutjs.com/](http://learn.knockoutjs.com/)](http://learn.knockoutjs.com/). Kromě toho se můžete dozvědět o uživatelském rozhraní jQuery a jQuery v [[http://docs.jquery.com/](http://docs.jquery.com/)](http://docs.jquery.com/).

<a id="Task_2_-_Exploring_the_Mobile_Application_Template"></a>
#### <a name="task-2---exploring-the-mobile-application-template"></a>Úloha 2 – prozkoumání šablony mobilní aplikace

ASP.NET MVC 4 usnadňuje vývoj webů pro mobilní a tabletové prohlížeče. Tato šablona má stejnou strukturu aplikace jako šablona internetové aplikace (Všimněte si, že kód kontroleru je prakticky identický), ale jeho styl byl upravený tak, aby se správně vykreslil v mobilních zařízeních na bázi dotykového ovládání.

1. Vyberte **soubor | Nové |** Příkaz nabídky projektu V dialogovém okně **Nový projekt** vyberte **vizuál C# | Webová** šablona ve stromu levého podokna a volba **webové aplikace ASP.NET MVC 4.** Pojmenujte projekt **Fotogalerie. Mobile**, vyberte umístění (nebo ponechte výchozí), vyberte &quot;přidat do řešení&quot; a klikněte na **OK**.
2. V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte šablonu projektu **mobilní aplikace** a klikněte na tlačítko **OK**. Ujistěte se, že jste vybrali Razor jako zobrazovací modul.

    ![Vytváří se nová mobilní aplikace ASP.NET MVC 4.](whats-new-in-aspnet-mvc-4/_static/image11.png "Vytváří se nová mobilní aplikace ASP.NET MVC 4.")

    *Vytváří se nová mobilní aplikace ASP.NET MVC 4.*
3. Nyní můžete prozkoumat řešení a zjistit některé nové funkce, které zavedla šablona řešení ASP.NET MVC 4 pro mobilní zařízení:

    - **Knihovna jQuery Mobile**

        Šablona projektu mobilní aplikace zahrnuje knihovnu jQuery Mobile Library, což je open source knihovna pro kompatibilitu s mobilním prohlížečem. jQuery Mobile používá progresivní rozšíření pro mobilní prohlížeče, které podporují šablony stylů CSS a JavaScript. Progresivní navýšení umožňuje všem prohlížečům zobrazovat základní obsah webové stránky, ale umožňuje jenom nejvýkonnějším prohlížečům zobrazit bohatou obsah. Soubory jazyka JavaScript a CSS, které jsou součástí stylu jQuery Mobile, umožňují mobilním prohlížečům přizpůsobení obsahu na obrazovce, aniž by bylo nutné provádět změny v kódu stránky.

        ![jQuery-mobile-library-included-in-the-template](whats-new-in-aspnet-mvc-4/_static/image12.png)

        *Knihovna jQuery Mobile obsažená v šabloně*
    - **Kód založený na HTML5**

        ![Mobile-application-template-using-HTML5-markup](whats-new-in-aspnet-mvc-4/_static/image13.png)

        *Šablona mobilní aplikace pomocí značek HTML5 (login. cshtml a index. cshtml)*
4. Stisknutím klávesy **F5** spusťte řešení.
5. Otevřete **emulátor Windows Phone 7**.
6. Na obrazovce Start telefonu otevřete Internet Explorer. Podívejte se na adresu URL, kde byla spuštěna aplikace klasické pracovní plochy, a přejděte na tuto adresu URL z telefonu (např. `http://localhost:[PortNumber]/`).
7. Nyní je možné zadat přihlašovací stránku nebo se podívat na stránku o službě. Všimněte si, že styl webu je založený na nové aplikaci Metro pro mobilní zařízení. Šablona projektu ASP.NET MVC 4 je na mobilních zařízeních správně zobrazena a zajišťuje, aby všechny prvky stránky byly viditelné a povolené. Všimněte si, že odkazy v hlavičce jsou dostatečně velké, aby je bylo možné kliknout nebo klepnout na tlačítko.

    ![Stránky šablon projektů v mobilním zařízení](whats-new-in-aspnet-mvc-4/_static/image14.png "Stránky šablon projektů v mobilním zařízení")

    *Stránky šablon projektů v mobilním zařízení*
8. Nová šablona používá také **zobrazovací značku meta**. Většina mobilních prohlížečů definuje šířku pro okno virtuálního prohlížeče nebo &quot;zobrazení&quot;, což je větší než skutečná šířka mobilního zařízení. To umožňuje mobilním prohlížečům zobrazit celou webovou stránku uvnitř virtuálního zobrazení. **Značka meta zobrazení** umožňuje webovým vývojářům nastavit šířku, výšku a měřítko oblasti prohlížeče na mobilních zařízeních **.** Šablona ASP.NET MVC 4 pro mobilní aplikace nastaví zobrazení na šířku zařízení (&quot;Width =&quot;šířka zařízení) v šabloně rozložení (*Views\Shared\_layout. cshtml*), takže všechny stránky budou mít nastavené zobrazení na šířku obrazovky zařízení. Všimněte si, že značka meta zobrazení nebude měnit výchozí zobrazení prohlížeče.
9. Otevřete **\_layout. cshtml**, umístěný v **zobrazeních | Sdílená** složka a přikomentujte meta značce zobrazení. Spusťte aplikaci, pokud ještě není spuštěná, a podívejte se na rozdíly.

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample2.cshtml)]

![Lokalita po přidání komentáře k meta značce zobrazení](whats-new-in-aspnet-mvc-4/_static/image15.png "Lokalita po přidání komentáře k meta značce zobrazení")

*Lokalita po přidání komentáře k meta značce zobrazení*
10. V aplikaci Visual Studio stisknutím klávesy **SHIFT** + **F5** zastavíte ladění aplikace.
11. Odkomentujte metaznačku zobrazení značek.

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample3.cshtml)]

<a id="Task_3_-_Using_Adaptive_Rendering"></a>
#### <a name="task-3---using-adaptive-rendering"></a>Úloha 3 – použití adaptivního vykreslování

V této úloze se naučíte, jak na mobilních zařízeních a webových prohlížečích správně vykreslit webovou stránku bez jakéhokoli přizpůsobení. Již jste použili značku meta zobrazení s podobným účelem. Nyní budete vyhovovat další výkonné metodě: *adaptivní vykreslování*.

Adaptivní vykreslování je technika, která používá **CSS3 multimediální dotazy** k přizpůsobení stylu použitému pro stránku. Dotazy na multimédia definují podmínky v šabloně stylů a seskupují CSS styly pod určitou podmínkou. Pouze v případě, že je podmínka pravdivá, je styl aplikován na deklarované objekty.

Flexibilita poskytovaná technikou adaptivního vykreslování umožňuje libovolné přizpůsobení zobrazení webu na různých zařízeních. Můžete definovat tolik stylů, kolik chcete pro jednu šablonu stylů, aniž byste museli psát kód logiky pro výběr stylu. Proto je velmi úhledný způsob přizpůsobení stylů stránky, protože snižuje množství duplicitního kódu a logiky pro účely vykreslování. Na druhé straně by se zvýšila spotřeba šířky pásma, protože velikost souborů CSS by mohla růst na okrajích.

Pomocí techniky adaptivního vykreslování se vaše lokalita **zobrazí správně, bez ohledu na prohlížeč.** Měli byste se však vzít v úvahu i v případě, že je větší zatížení šířky pásma velmi důležité.

> [!NOTE]
> Základní formát dotazu na média je: @media \[oboru: vše | Handheld | Tisk | projekce |\] obrazovky ([vlastnost: hodnota] a... [vlastnost: hodnota])

Příklady dotazů na média: &gt; **@media All a (max-width: 1000px) a (min-width: 700px) {}:** pro všechna rozlišení mezi 700px a 1000px.

> **@media obrazovka a (minimální šířka: 400px) a (max-width: 700px) {...}:** Pouze pro obrazovky. Rozlišení musí být mezi 400 a 700px.
> 
> **@media handheld a (minimální šířka: 20em), obrazovka a (minimální šířka: 20em) {...}:** Pro handheldy (mobilní zařízení a zařízení) a obrazovky. Minimální šířka musí být větší než 20em.
> 
> Další informace najdete na [webu W3C](http://www.w3.org/TR/css3-mediaqueries/).

Nyní si prozkoumáte, jak adaptivní vykreslování funguje, a zlepšuje čitelnost šablony výchozích webů ASP.NET MVC 4.

1. Otevřete řešení **fotogallery. sln** , které jste vytvořili v úloze 1, a vyberte projekt **Galerie** . Stisknutím klávesy **F5** spusťte řešení.
2. Změňte velikost šířky prohlížeče a nastavte Windows na polovinu nebo méně, než je čtvrtina původní velikosti. Všimněte si, co se stane s položkami v hlavičce: některé prvky se nezobrazí v oblasti viditelné v hlavičce.
3. V Průzkumníku řešení sady Visual Studio otevřete soubor **Web. CSS** , který se nachází ve složce projektu **obsahu** . Stisknutím **kombinace kláves CTRL + F** otevřete integrované vyhledávání sady Visual Studio a napíšete `@media` a vyhledejte **mediální dotaz CSS**.

    Podmínka pro dotaz na multimédia definovaná v této šabloně funguje tímto způsobem: když velikost okna prohlížeče je pod **850 px**, použijí se pravidla CSS definovaná v tomto bloku médií.

    ![Hledání multimediálního dotazu](whats-new-in-aspnet-mvc-4/_static/image16.png "Hledání multimediálního dotazu")

    *Hledání multimediálního dotazu*
4. Nahraďte hodnotu atributu max-width nastavenou v 850 px hodnotou **10px**, abyste mohli zakázat adaptivní vykreslování, a stisknutím **kláves CTRL + S** uložte změny. Vraťte se do prohlížeče a stisknutím **kláves CTRL + F5** aktualizujte stránku se změnami, které jste provedli. Všimněte si rozdílů na obou stránkách při úpravách šířky okna.

    ![Na levé straně stránka používá styl @media ve správném napravo je styl vynechán.](whats-new-in-aspnet-mvc-4/_static/image17.png "Na levé straně stránka používá styl @media ve správném napravo je styl vynechán.")

    *Na levé straně stránka používá styl @media ve správném napravo je styl vynechán.*

    Teď se podívejme na to, co se stane na mobilních zařízeních:

    ![Na levé straně stránka používá styl @media ve správném napravo je styl vynechán.](whats-new-in-aspnet-mvc-4/_static/image18.png "Na levé straně stránka používá styl @media ve správném napravo je styl vynechán.")

    *Na levé straně stránka používá styl @media ve správném napravo je styl vynechán.*

    I když si všimnete, že změny při vykreslování stránky ve webovém prohlížeči nejsou velmi důležité, při použití mobilního zařízení se rozdíly stanou jasnější. Na levé straně obrázku vidíte, že vlastní styl zlepšil čitelnost.

    Adaptivní vykreslování lze použít v mnoha dalších scénářích, což usnadňuje použití podmíněného stylování na webu a řešení běžných potíží se styly s úhledným přístupem.

    Metadata zobrazení a dotazy na média šablony stylů CSS nejsou specifické pro ASP.NET MVC 4, takže můžete tyto funkce využít v libovolné webové aplikaci.
5. V aplikaci Visual Studio stisknutím klávesy **SHIFT** + **F5** zastavíte ladění aplikace.

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_the_Photo_Gallery_Web_Application"></a>
### <a name="exercise-2-creating-the-photo-gallery-web-application"></a>Cvičení 2: Vytvoření webové aplikace Galerie fotografií

V tomto cvičení budete pracovat s aplikací Fotogalerie pro zobrazování fotek. Začnete s šablonou projektu ASP.NET MVC 4 a pak přidáte funkci pro načtení fotografií ze služby a jejich zobrazení na domovské stránce.

V následujícím cvičení budete toto řešení aktualizovat, aby se vylepšilo, jak se zobrazuje na mobilních zařízeních.

<a id="Task_1_-_Creating_a_Mock_Photo_Service"></a>
#### <a name="task-1---creating-a-mock-photo-service"></a>Úloha 1 – Vytvoření modelu fotografické služby

V této úloze vytvoříte objekt typu Photo Service, který načte obsah, který se zobrazí v galerii. K tomu je potřeba přidat nový kontroler, který jednoduše vrátí soubor JSON s daty každé fotografie.

1. Otevřete **Visual Studio** , pokud ještě není otevřené.
2. Vyberte **soubor | Nové |** Příkaz nabídky projektu V dialogovém okně **Nový projekt** vyberte **vizuál C# | Webová** šablona ve stromu levého podokna a výběr **webové aplikace ASP.NET MVC 4.** Pojmenujte **fotogalerii**projektů, vyberte umístění (nebo ponechte výchozí) a klikněte na **OK**. Alternativně můžete pokračovat v práci ze stávajícího řešení ASP.NET MVC 4 pro **internetovou aplikaci** z **cvičení 1** a přeskočit další krok.
3. V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte šablonu projektu **Internetová aplikace** a klikněte na tlačítko **OK**. Ujistěte se, že jste jako zobrazovací modul vybrali Razor.
4. V **Průzkumník řešení**klikněte pravým tlačítkem na složku **aplikace\_data** projektu a vyberte **Přidat | Existující položka**. Přejděte do složky **Source\Assets\App\_data** tohoto testovacího prostředí a přidejte soubor **photos. JSON** .
5. Vytvořte nový kontroler s názvem s **ovladačem**. Provedete to tak, že kliknete pravým tlačítkem na složku **řadiče** , přejdete na **Přidat** a vyberte **kontroler.** Dokončete název kontroleru, ponechte **prázdnou šablonu KONTROLERU MVC** a klikněte na **Přidat**.

    ![Přidání kontroleru](whats-new-in-aspnet-mvc-4/_static/image19.png "Přidání kontroleru")

    *Přidání kontroleru*
6. Nahraďte metodu **indexu** následující akcí **Galerie** a vraťte obsah ze souboru JSON, který jste nedávno přidali do projektu.

    (Fragment kódu – *ASP.NET MVC 4 Lab-Ex02-Galerie – akce*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample4.cs)]
7. Stisknutím klávesy **F5** spusťte řešení a potom přejděte na následující adresu URL, abyste mohli otestovat napodobnou fotografii: `http://localhost:[port]/photo/gallery` (hodnota [port] závisí na aktuálním portu, ve kterém byla aplikace spuštěna). Požadavek na tuto adresu URL by měl načíst obsah souboru **photos. JSON** .

    ![Testování služby s napodobnou fotografií](whats-new-in-aspnet-mvc-4/_static/image20.png "Testování služby s napodobnou fotografií")

    *Testování služby s napodobnou fotografií*

Ve skutečné implementaci byste mohli použít [webové rozhraní API ASP.NET](../../../../web-api/index.md) k implementaci služby Fotogalerie. Rozhraní ASP.NET Web API usnadňuje sestavování služeb HTTP, které jsou poskytovány širokému spektru klientů, včetně prohlížečů a mobilních zařízení. Rozhraní ASP.NET Web API představuje ideální platformu pro sestavování aplikací RESTful v rozhraní .NET Framework.

<a id="Task_2_-_Displaying_the_Photo_Gallery"></a>
#### <a name="task-2---displaying-the-photo-gallery"></a>Úloha 2 – zobrazení galerie fotografií

V této úloze aktualizujete domovskou stránku, aby se zobrazila galerie fotografií pomocí napodobované služby, kterou jste vytvořili v prvním úkolu tohoto cvičení. Přidáte soubory modelů a aktualizujete zobrazení galerie.

1. V aplikaci Visual Studio stisknutím klávesy **SHIFT** + **F5** zastavíte ladění aplikace.
2. Ve složce **modely** vytvořte třídu **Photo** . Provedete to tak, že kliknete pravým tlačítkem na složku **modely** , vyberete **Přidat** a klikněte na **Třída**. Potom nastavte název na **Photo.cs** a klikněte na **Přidat**.
3. Přidejte následující členy do třídy **Photo** .

    (Fragment kódu – *ASP.NET MVC 4 Lab – model Ex02-Photo*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample5.cs)]
4. Otevřete soubor **HomeController.cs** ze složky **Controllers** .
5. Přidejte následující příkazy using.

    (Fragment kódu – *ASP.NET MVC 4 Lab-Ex02-HomeController using*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample6.cs)]
6. Aktualizujte akci **indexu** tak, aby používala **HttpClient** k načtení dat galerie, a potom pomocí **JavaScriptSerializer** ji deserializovat do modelu zobrazení.

    (Fragment kódu – *ASP.NET MVC 4 Lab-Ex02-index Action*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample7.cs)]
7. Otevřete soubor **index. cshtml** umístěný ve složce **Views\Home** a nahraďte veškerý obsah následujícím kódem.

    Tento kód projde všemi fotografiemi načtenými ze služby a zobrazí je do neuspořádaného seznamu.

    (Fragment kódu – *ASP.NET MVC 4 Lab – Ex02 – seznam fotek*)

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample8.cshtml)]
8. V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku **obsahu** projektu a vyberte **Přidat | Existující položka**. Přejděte do složky **Source\Assets\Content** v tomto testovacím prostředí a přidejte soubor **Web. CSS** . Bude nutné potvrdit jeho náhradu. Pokud máte soubor **Web. CSS** otevřený, budete se muset ujistit, že soubor znovu načtete.
9. Otevřete Průzkumníka souborů a zkopírujte celou složku **fotek** ve složce **Source\Assets** v tomto testovacím prostředí do kořenové složky projektu v Průzkumník řešení.
10. Spusťte aplikaci. Teď byste měli vidět domovskou stránku zobrazující fotky v galerii.

    ![Galerie fotografií](whats-new-in-aspnet-mvc-4/_static/image21.png "Galerie fotografií")

    *Galerie fotografií*
11. V aplikaci Visual Studio stisknutím klávesy **SHIFT** + **F5** zastavíte ladění aplikace.

<a id="Exercise3"></a>

<a id="Exercise_3_Adding_support_for_mobile_devices"></a>
### <a name="exercise-3-adding-support-for-mobile-devices"></a>Cvičení 3: Přidání podpory pro mobilní zařízení

Jedna z klíčových aktualizací v ASP.NET MVC 4 je podpora pro vývoj pro mobilní zařízení. V tomto cvičení budete prozkoumat ASP.NET MVC 4 nové funkce pro mobilní aplikace tím, že rozšíříte řešení Fotogalerie, které jste vytvořili v předchozím cvičení.

<a id="Task_1_-_Installing_jQuery_Mobile_in_an_ASPNET_MVC_4_Application"></a>
#### <a name="task-1---installing-jquery-mobile-in-an-aspnet-mvc-4-application"></a>Úloha 1 – instalace jQuery Mobile v aplikaci ASP.NET MVC 4

1. Otevřete řešení **zahájit** , které se nachází ve složce **source/EX3-MobileSupport/Begin/** Folder. V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
2. Otevřete **konzolu správce** balíčků kliknutím na nástroje **Správce balíčků NuGet** **nástroje** >  > možnosti nabídky **konzoly Správce balíčků** .

    ![Otevření konzoly Správce balíčků NuGet](whats-new-in-aspnet-mvc-4/_static/image22.png "Otevření konzoly Správce balíčků NuGet")

    *Otevření konzoly Správce balíčků NuGet*
3. V konzole správce balíčků spusťte následující příkaz k instalaci balíčku **jQuery. Mobile. Mvc** .

    jQuery Mobile je open source knihovna pro sestavení webového uživatelského rozhraní optimalizovaného pro dotykové ovládání. Balíček NuGet jQuery. Mobile. MVC zahrnuje pomocníky k používání jQuery Mobile s aplikací ASP.NET MVC 4.

    > [!NOTE]
    > Spuštěním následujícího příkazu budete stahovat knihovnu jQuery. Mobile. MVC z NuGet.

    ČÁSTIC

    [!code-powershell[Main](whats-new-in-aspnet-mvc-4/samples/sample9.ps1)]

    Tento příkaz nainstaluje jQuery Mobile a některé pomocné soubory, včetně následujících:

    - **Zobrazení/Shared/\_layout. Mobile. cshtml**: je mobilní rozložení na bázi jQuery optimalizované pro menší obrazovku. Když webová stránka obdrží požadavek z mobilního prohlížeče, nahradí původní rozložení (\_layout. cshtml) tímto.
    - Komponenta s přepínačem zobrazení: skládá se z částečného zobrazení **zobrazení/Shared/\_ViewSwitcher. cshtml** a řadiče **ViewSwitcherController.cs** . Tato součást zobrazí odkaz na mobilní prohlížeče, aby uživatelé mohli přepnout na desktopovou verzi stránky.  
        ![Projekt galerie fotografií s podporou mobilních zařízení](whats-new-in-aspnet-mvc-4/_static/image23.png "Projekt galerie fotografií s podporou mobilních zařízení")

        *Projekt galerie fotografií s podporou mobilních zařízení*
4. Zaregistrujte mobilní sady. Provedete to tak, že otevřete soubor **Global.asax.cs** a přidáte následující řádek.

    (Fragment kódu – *ASP.NET MVC 4 Lab-Ex03 – Registrace mobilních sad*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample10.cs)]
5. Spusťte aplikaci pomocí desktopového webového prohlížeče.
6. Otevřete **emulátor Windows Phone 7** umístěný v **nabídce Start | Všechny programy | Windows Phone SDK 7,1 | Emulátor Windows Phone.**
7. Na obrazovce Start telefonu otevřete Internet Explorer. Podívejte se na adresu URL, kde je aplikace spuštěná, a přejděte na tuto adresu URL v prohlížeči telefonu (např. `http://localhost:[PortNumber]/`).

    Všimněte si, že vaše aplikace bude vypadat jinak v emulátoru Windows Phone, protože jQuery. Mobile. MVC vytvořilo v projektu nové prostředky, které zobrazují zobrazení optimalizovaná pro mobilní zařízení.

    Všimněte si zprávy v horní části telefonu a zobrazuje odkaz, který se přepne do zobrazení plochy. Kromě toho rozložení **\_layout. Mobile. cshtml** vytvořené balíčkem, který jste nainstalovali, zahrnuje jiné rozložení v aplikaci.

    > [!NOTE]
    > Zatím není k dispozici žádný odkaz pro návrat do mobilního zobrazení. Bude zahrnutý v novějších verzích.

    ![Mobilní zobrazení domovské stránky Galerie fotografií](whats-new-in-aspnet-mvc-4/_static/image24.png "Mobilní zobrazení domovské stránky Galerie fotografií")

    *Mobilní zobrazení domovské stránky Galerie fotografií*
8. V aplikaci Visual Studio stisknutím klávesy **SHIFT** + **F5** zastavíte ladění aplikace.

<a id="Task_2_-_Creating_Mobile_Views"></a>
#### <a name="task-2---creating-mobile-views"></a>Úkol 2 – vytváření mobilních zobrazení

V této úloze vytvoříte mobilní verzi zobrazení index s obsahem upraveným pro lepší vzhled v mobilních zařízeních.

1. Zkopírujte zobrazení **Views\Home\Index.cshtml** a vložte ho, aby se vytvořila kopie, přejmenujte nový soubor na **index. Mobile. cshtml**.
2. Otevřete nový vytvořený **index. Mobile. cshtml** zobrazení a nahraďte existující značku &lt;ul&gt; tímto kódem. Tímto způsobem aktualizujete značku &lt;ul&gt; pomocí poznámek k mobilním datům jQuery, aby se použily mobilní motivy z jQuery.

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample11.html)]

    > [!NOTE] 
    > 
    > Všimněte si, že:
    > 
    > - Atribut **role dat** nastavený na **ListView** vykreslí seznam pomocí stylů ListView.
    > 
    > - Atribut **vsazení dat** nastavený na hodnotu true zobrazí seznam s zaobleným ohraničením a okrajem.
    > 
    > - Atribut **filtru dat** nastavený na **hodnotu true** vygeneruje vyhledávací pole.
    > 
    > Další informace o konvencích pro mobilní zařízení jQuery najdete v dokumentaci k projektu: [ [http://jquerymobile.com/demos/1.1.1/](http://jquerymobile.com/demos/1.1.1/)](http://jquerymobile.com/demos/1.1.1/)
3. Změny uložte stisknutím **kombinace kláves CTRL + S** .
4. Přepněte na **emulátor Windows Phone** a aktualizujte lokalitu. Všimněte si nového vzhledu a chování seznamu galerie a také nového vyhledávacího pole v horní části. Potom zadejte slovo do vyhledávacího pole (například **Tulips**), aby se spustilo hledání v galerii fotografií.

    ![Galerie s filtrováním pomocí stylu ListView](whats-new-in-aspnet-mvc-4/_static/image25.png "Galerie s filtrováním pomocí stylu ListView")

    *Galerie s filtrováním pomocí stylu ListView*

    Pro shrnutí jste použili recept pro zobrazení, pomocí kterého jste vytvořili kopii zobrazení index s příponou &quot;Mobile&quot;. Tato přípona indikuje ASP.NET MVC 4, že každý požadavek vygenerovaný z mobilního zařízení bude používat tuto kopii indexu. Kromě toho jste aktualizovali mobilní verzi zobrazení index pro použití jQuery Mobile pro zlepšení vzhledu lokality a chování v mobilních zařízeních.
5. Vraťte se do sady Visual Studio a otevřete **Web. Mobile. CSS** nacházející se ve složce **obsahu** .
6. Opravte umístění názvu fotografie, aby se zobrazila na pravé straně obrázku. Chcete-li to provést, přidejte do souboru **Web. Mobile. CSS** následující kód.

    CSS

    [!code-css[Main](whats-new-in-aspnet-mvc-4/samples/sample12.css)]
7. Změny uložte stisknutím **kombinace kláves CTRL + S** .
8. Přepněte zpátky na **emulátor Windows Phone** a aktualizujte lokalitu. Všimněte si, že název fotografie je teď správně umístěný.

    ![Název umístěný na pravé straně obrázku](whats-new-in-aspnet-mvc-4/_static/image26.png "Název umístěný na pravé straně obrázku")

    *Název umístěný na pravé straně obrázku*

<a id="Task_3_-_jQuery_Mobile_Themes"></a>
#### <a name="task-3---jquery-mobile-themes"></a>Úloha 3 – jQuery – mobilní motivy

Každé rozložení a widget v jQuery Mobile je navrženo kolem nového objektově orientovaného rozhraní CSS, které umožňuje použít kompletní motiv sjednocení vizuálního návrhu pro weby a aplikace.

výchozí motiv jQuery Mobile obsahuje 5 vzorků, kterým jsou uvedena písmena (a, b, c, d, e) pro rychlé reference.

V této úloze aktualizujete rozložení pro mobilní zařízení tak, aby používalo jiný motiv než výchozí.

1. Přepněte zpět do sady Visual Studio.
2. Otevřete soubor **\_layout. Mobile. cshtml** umístěný v **Views\Shared**.
3. Najděte element div s rolí data-role nastavenou na &quot;&quot; stránky a aktualizujte **motiv dat** na &quot;**e**&quot;.

    [!code-html[Main](whats-new-in-aspnet-mvc-4/samples/sample13.html)]
4. Změny uložte stisknutím **kombinace kláves CTRL + S** .
5. Aktualizujte lokalitu v **emulátoru Windows Phone** a Všimněte si nového schématu barev.

    ![Mobilní rozložení s odlišným barevným schématem](whats-new-in-aspnet-mvc-4/_static/image27.png "Mobilní rozložení s odlišným barevným schématem")

    *Mobilní rozložení s odlišným barevným schématem*

<a id="Task_4_-_Using_the_View-Switcher_Component_and_the_Browser_Overriding_Features"></a>
#### <a name="task-4---using-the-view-switcher-component-and-the-browser-overriding-features"></a>Úloha 4 – použití součásti pro přepínání zobrazení a přepisování funkcí v prohlížeči

Konvence pro mobilní optimalizované webové stránky je přidat odkaz, jehož text je například desktopové zobrazení nebo režim celého webu, který umožňuje uživatelům přepnout na desktopovou verzi stránky. Balíček jQuery. Mobile. MVC obsahuje ukázkovou komponentu pro **přepínání zobrazení** pro tento účel, která se používá v zobrazení **\_layout. Mobile. cshtml** .

![Odkaz pro přepnutí na desktopové zobrazení](whats-new-in-aspnet-mvc-4/_static/image28.png "Odkaz pro přepnutí na desktopové zobrazení")

*Odkaz pro přepnutí na desktopové zobrazení*

Přepínač zobrazení používá novou funkci nazvanou **přepisování prohlížeče**. Tato funkce umožňuje, aby vaše aplikace považovala požadavky, jako kdyby byly přicházející z jiného prohlížeče (uživatelského agenta) než ten, ze kterého přicházejí.

V této úloze prozkoumáte ukázkovou implementaci přepínačů zobrazení přidaných jQuery. Mobile. MVC a nový prohlížeč přepsal funkce v ASP.NET MVC 4.

1. Přepněte zpět do sady Visual Studio.
2. Otevřete zobrazení **\_layout. Mobile. cshtml** nacházející se ve složce **Views\Shared** a Všimněte si, že se na komponentu s přepínači zobrazení odkazuje jako na částečné zobrazení.

    ![Mobilní rozložení pomocí součásti pro přepínač zobrazení](whats-new-in-aspnet-mvc-4/_static/image29.png "Mobilní rozložení pomocí součásti pro přepínač zobrazení")

    *Mobilní rozložení pomocí součásti pro přepínač zobrazení*
3. Otevřete částečné zobrazení **\_ViewSwitcher. cshtml** .

    Částečné zobrazení používá novou metodu **ViewContext. HttpContext. GetOverriddenBrowser ()** k určení původu webového požadavku a zobrazí odpovídající odkaz pro přepnutí buď na Desktop nebo mobilní zobrazení.

    Metoda **GetOverriddenBrowser** vrací instanci **HttpBrowserCapabilitiesBase** , která odpovídá uživatelskému agentovi, který je aktuálně nastaven pro požadavek (skutečnost nebo přepsání). Tuto hodnotu můžete použít k získání vlastností, jako je například **IsMobileDevice**.

    ![ViewSwitcher částečné zobrazení](whats-new-in-aspnet-mvc-4/_static/image30.png "ViewSwitcher částečné zobrazení")

    *ViewSwitcher částečné zobrazení*
4. Otevřete třídu **ViewSwitcherController.cs** , která se nachází ve složce **Controllers** . Podívejte se, že akce SwitchView je volána odkazem v komponentě ViewSwitcher a Všimněte si nových metod HttpContext.

    - Metoda **HttpContext. ClearOverriddenBrowser ()** odebere všechny přepsané uživatelské agenta pro aktuální požadavek.
    - Metoda **HttpContext. SetOverriddenBrowser ()** Přepisuje skutečnou hodnotu uživatelského agenta žádosti pomocí zadaného uživatelského agenta.  
        ![Kontroler ViewSwitcher](whats-new-in-aspnet-mvc-4/_static/image31.png "Kontroler ViewSwitcher")  
*Kontroler ViewSwitcher*

        Přepsání prohlížeče je základní funkcí ASP.NET MVC 4, která je k dispozici i v případě, že balíček jQuery. Mobile. MVC nenainstalujete. Tato funkce ale ovlivňuje jenom zobrazení, rozložení a částečné zobrazení a nemá vliv na žádnou z funkcí, které závisí na objektu Request. browser.

<a id="Task_5_-_Adding_the_View-Switcher_in_the_Desktop_View"></a>
#### <a name="task-5---adding-the-view-switcher-in-the-desktop-view"></a>Úkol 5 – přidání přepínačů zobrazení v desktopovém zobrazení

V této úloze aktualizujete rozložení plochy tak, aby zahrnovalo přepínač zobrazení. To umožní mobilním uživatelům přejít zpět do mobilního zobrazení při procházení plochy.

1. Aktualizujte lokalitu v **emulátoru Windows Phone**.
2. V horní části Galerie klikněte na odkaz **zobrazení plochy** . Všimněte si, že v zobrazení plocha není žádný přepínač zobrazení, který vám umožní vrátit se do mobilního zobrazení.
3. Vraťte se do sady Visual Studio a otevřete zobrazení **\_layout. cshtml** .
4. Vyhledejte část přihlášení a vložte volání, které vykreslí **\_** částečné zobrazení pod\_částečném zobrazením **LogOnPartial** . Potom stisknutím **kombinace kláves CTRL + S** změny uložte.

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample14.cshtml)]
5. Změny uložte stisknutím **kombinace kláves CTRL + S** .
6. Aktualizujte stránku v emulátoru Windows Phone a dvakrát klikněte na obrazovku pro přiblížení. Všimněte si, že na domovské stránce se nyní zobrazuje odkaz **mobilní zobrazení** , který přepíná z mobilního zobrazení na Desktop.

    ![Přepínač zobrazení vykreslený v desktopovém zobrazení](whats-new-in-aspnet-mvc-4/_static/image32.png "Přepínač zobrazení vykreslený v desktopovém zobrazení")

    *Přepínač zobrazení vykreslený v desktopovém zobrazení*
7. Přepněte znovu do mobilního zobrazení a přejděte na stránku **About** (http://localhost[port]/Home/about). Všimněte si, že i v případě, že jste ještě nevytvořili zobrazení About. Mobile. cshtml, zobrazí se stránka o aplikaci pomocí rozložení mobilní (\_layout. Mobile. cshtml).

    ![O stránce](whats-new-in-aspnet-mvc-4/_static/image33.png "O stránce")

    *O stránce*
8. Nakonec otevřete web v desktopovém webovém prohlížeči. Všimněte si, že žádný z předchozích aktualizací neovlivnil zobrazení plochy.

    ![Desktopové zobrazení galerie](whats-new-in-aspnet-mvc-4/_static/image34.png "Desktopové zobrazení galerie")

    *Desktopové zobrazení galerie*

<a id="Task_6_-_Creating_New_Display_Modes"></a>
#### <a name="task-6---creating-new-display-modes"></a>Úloha 6 – vytváření nových režimů zobrazení

Funkce nové režimy zobrazení umožňuje aplikaci vybrat zobrazení v závislosti na prohlížeči, který požadavek vygeneroval. Pokud například prohlížeč stolních počítačů požaduje domovskou stránku, aplikace vrátí šablonu **Views\Home\Index.cshtml** . Pokud pak mobilní prohlížeč požaduje domovskou stránku, aplikace vrátí šablonu **Views\Home\Index.Mobile.cshtml** .

V této úloze vytvoříte přizpůsobené rozložení pro zařízení iPhone a budete muset simulovat žádosti od zařízení iPhone. K tomu můžete použít emulátor nebo simulátor pro iPhone (jako je [elektrický mobilní simulátor](http://www.electricplum.com/)) nebo prohlížeč s doplňky, které upravují uživatelského agenta. Pokyny, jak nastavit řetězec uživatelského agenta v prohlížeči Safari pro emulaci iPhonu, najdete v článku [jak umožnit Safari předstírat je IE](http://www.davidalison.com/2008/05/how-to-let-safari-pretend-its-ie.html) v blogu David Alison.

**Všimněte si, že tato úloha je volitelná a vy můžete pokračovat v rámci testovacího prostředí bez jeho provedení.**

1. V aplikaci Visual Studio stisknutím klávesy **SHIFT** + **F5** zastavíte ladění aplikace.
2. Otevřete **Global.asax.cs** a přidejte následující příkaz using.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample15.cs)]
3. Přidejte následující zvýrazněný kód do aplikace\_spustit metodu.

    (Fragment kódu – *ASP.NET MVC 4 Lab-Ex03-iPhone DisplayMode*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample16.cs)]

Zaregistrovali jste nové **DefaultDisplayMode s názvem &quot;iPhone&quot;** v rámci statického seznamu static **DisplayModeProvider. instance. Modes** , který se bude shodovat s každým příchozím požadavkem. Pokud příchozí požadavek obsahuje řetězec &quot;iPhone&quot;, ASP.NET MVC najde zobrazení, jejichž název obsahuje příponu&quot; iPhone &quot;pro iPhone. Parametr 0 označuje, jak konkrétní je nový režim; Toto zobrazení je například konkrétnější než obecné &quot;. mobilní&quot; pravidlo, které odpovídá žádostem z mobilních zařízení.

Po spuštění tohoto kódu bude aplikace při vygenerování žádosti v prohlížeči iPhone používat **Views\Shared\\_Layout. iPhone. cshtml** , které vytvoříte v dalších krocích.

> [!NOTE]
> Tento způsob testování žádosti pro iPhone byl pro demonstrační účely zjednodušený a nemusí fungovat podle očekávání pro každý řetězec agenta uživatele iPhone (například test rozlišuje malá a velká písmena).

4. Vytvořte kopii souboru **\_layout. Mobile. cshtml** ve složce **Views\Shared** a přejmenujte kopii na &quot; **\_layout. cshtml**&quot;.
5. Otevřete **\_layout. iPhone. cshtml** , který jste vytvořili v předchozím kroku.
6. Najděte element div s atributem role dat nastavenou na **stránku** a změňte atribut **data-Theme** tak, **aby &quot;&quot;** .

[!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample17.cshtml)]

V aplikaci ASP.NET MVC 4 teď máte tři rozložení:

1. **\_layout. cshtml**: výchozí rozložení používané pro desktopové prohlížeče.
2. **\_layout. Mobile. cshtml**: výchozí rozložení používané pro mobilní zařízení.
3. **\_layout. iPhone. cshtml**: konkrétní rozložení pro zařízení iPhone pomocí jiného barevného schématu, které rozlišuje \_layout. Mobile. cshtml.
7. Stisknutím klávesy **F5** spusťte aplikaci a procházejte lokalitou v **emulátoru Windows Phone**.
8. Otevřete **simulátor pro iPhone** (pokyny k instalaci a konfiguraci simulátoru pro iPhone najdete v [příloze C](#AppendixC) ) a přejděte na web také. Všimněte si, že každý telefon používá konkrétní šablonu.

    ![Using-different-views-for-each-mobile-device2](whats-new-in-aspnet-mvc-4/_static/image35.png)

    *Používání různých zobrazení pro každé mobilní zařízení*

<a id="Exercise4"></a>

<a id="Exercise_4_Using_Asynchronous_Controllers"></a>
### <a name="exercise-4-using-asynchronous-controllers"></a>Cvičení 4: použití asynchronních řadičů

Microsoft .NET Framework 4,5 zavádí nové jazykové funkce v C# a Visual Basic k poskytování nového základu pro asynchronii v programování .NET. Tato nová základ usnadňuje asynchronní programování podobným a přibližně jako synchronní programování. Nyní je možné zapisovat metody asynchronních akcí v ASP.NET MVC 4 pomocí třídy **AsyncController** . Asynchronní metody akcí můžete použít pro dlouhotrvající požadavky, které nejsou vázané na procesor. Tím předejdete blokování, aby webový server prováděl práci během zpracování žádosti. Třída AsyncController se obvykle používá pro dlouhotrvající volání webové služby.

Toto cvičení vysvětluje základy asynchronních operací v ASP.NET MVC 4. Pokud potřebujete hlubší podrobně, můžete se podívat na následující článek: [ [https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)](https://msdn.microsoft.com/library/ee728598%28v=vs.100%29.aspx)

<a id="Task_1_-_Implementing_an_Asynchronous_Controller"></a>
#### <a name="task-1---implementing-an-asynchronous-controller"></a>Úloha 1 – implementace asynchronního kontroleru

1. Otevřete řešení **zahájit** , které se nachází ve složce **source/Ex4-Async/Begin/** Folder. V opačném případě můžete i nadále používat **koncová** řešení získaná dokončením předchozího cvičení.

   1. Pokud jste otevřeli poskytnuté řešení **zahájení** , budete muset před pokračováním stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
2. Otevřete třídu **HomeController.cs** ze složky **Controllers** .
3. Přidejte následující příkaz using.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample18.cs)]
4. Aktualizujte třídu **HomeController** tak, aby dědila z **AsyncController**. Řadiče, které jsou odvozeny od AsyncController, umožňují ASP.NET zpracování asynchronních požadavků a stále mohou obsluhovat synchronní metody akcí.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample19.cs)]
5. Přidejte klíčové slovo **Async** do metody **indexu** a vraťte typ **Task&lt;ActionResult&gt;** .

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample20.cs)]

    > [!NOTE]
    > Klíčové slovo **Async** je jedno z nových klíčových slov, které poskytuje .NET Framework 4,5. oznamuje kompilátoru, že tato metoda obsahuje asynchronní kód. Objekt **úlohy** představuje asynchronní operaci, která může být dokončena v nějakém okamžiku v budoucnu.
6. Nahraďte **klienta. Volání GetAsync ()** s úplnou asynchronní verzí pomocí klíčového slova await, jak je uvedeno níže.

    (Fragment kódu – *ASP.NET MVC 4 Lab-Ex04-GetAsync*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample21.cs)]

    > [!NOTE]
    > V předchozí verzi jste používali vlastnost **Result** z objektu **Task** k blokování vlákna, dokud není výsledek vrácen (synchronizační verze).
    > 
    > Přidáním klíčového slova **await** říká kompilátoru, že asynchronně čeká na úlohu vrácenou z volání metody. To znamená, že zbytek kódu bude proveden jako zpětné volání až po dokončení očekávané metody. Další věcí k oznámení je, že nemusíte měnit blok try-catch, aby bylo možné provést tuto práci: výjimky, ke kterým dochází na pozadí nebo v popředí, budou stále zachyceny bez jakékoli další práce pomocí obslužné rutiny poskytované rozhraním.
7. Změňte kód tak, aby pokračoval v asynchronní implementaci nahrazením řádků novým kódem, jak je znázorněno níže.

    (Fragment kódu – *ASP.NET MVC 4 Lab-Ex04-ReadAsStringAsync*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample22.cs)]
8. Spusťte aplikaci. Všimnete si, že nebudete mít žádné zásadní změny, ale váš kód nebude blokovat vlákno z fondu vláken, což vylepší využití prostředků serveru a zlepšuje výkon.

    > [!NOTE]
    > Další informace o nových asynchronních programovacích funkcích v testovacím prostředí &quot;**asynchronní programování v rozhraní .net 4,5 C# s a Visual Basic**&quot; zahrnutých v sadě Visual Studio Training Kit.

<a id="Task_2_-_Handling_Time-Outs_with_Cancellation_Tokens"></a>
#### <a name="task-2---handling-time-outs-with-cancellation-tokens"></a>Úloha 2 – zpracování časových limitů s tokeny zrušení

Asynchronní metody akcí, které vracejí instance úloh, mohou také podporovat časové limity. V této úloze aktualizujete kód metody indexu pro zpracování scénáře časového limitu pomocí tokenu zrušení.

1. Vraťte se do sady Visual Studio a stisknutím klávesy **SHIFT + F5** Zastavte ladění.
2. Do souboru **HomeController.cs** přidejte následující příkaz using.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample23.cs)]
3. Aktualizujte akci indexu tak, aby přijímala argument **CancellationToken** .

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample24.cs)]
4. Aktualizujte volání **GetAsync** , aby se předal token zrušení.

    (Fragment kódu – *ASP.NET MVC 4 Lab-Ex04-SendAsync with CancellationToken*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample25.cs)]
5. Naupravte metodu *indexu* s atributem **hodnota vlastnosti AsyncTimeout** nastaveným na 500 milisekund a atribut **HandleError** nakonfigurovaný tak, aby zpracovávala **TaskCanceledException** přesměrováním na zobrazení pro **vypršení časového limitu** .

    (Fragment kódu – *ASP.NET MVC 4 Lab-Ex04-Attributes*)

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample26.cs)]
6. Otevřete třídu **fotocontroller** a aktualizujte metodu **Galerie** tak, aby zpozdila spuštění 1000 milisekund (1 sekunda), aby se simulovala dlouhodobě spuštěná úloha.

    [!code-csharp[Main](whats-new-in-aspnet-mvc-4/samples/sample27.cs)]
7. Otevřete soubor **Web. config** a povolte vlastní chyby přidáním následujícího elementu.

    [!code-xml[Main](whats-new-in-aspnet-mvc-4/samples/sample28.xml)]
8. Vytvořte nové zobrazení v **Views\Shared** s názvem **časované** a použijte výchozí rozložení. V Průzkumník řešení klikněte pravým tlačítkem na složku **Views\Shared** a vyberte **Přidat | Zobrazit**.

    ![Používání různých zobrazení pro každé mobilní zařízení](whats-new-in-aspnet-mvc-4/_static/image36.png "Používání různých zobrazení pro každé mobilní zařízení")

    *Používání různých zobrazení pro každé mobilní zařízení*
9. Aktualizujte obsah zobrazení s **časovým limitem** , jak je znázorněno níže.

    [!code-cshtml[Main](whats-new-in-aspnet-mvc-4/samples/sample29.cshtml)]
10. Spusťte aplikaci a přejděte na kořenovou adresu URL. Když jste přidali **vlákno. režim spánku** je 1000 milisekund, zobrazí se chyba vypršení časového limitu, generovaná atributem **hodnota vlastnosti AsyncTimeout** a zachycení atributem **HandleError** .

    ![Zpracovaná výjimka časového limitu](whats-new-in-aspnet-mvc-4/_static/image37.png "Zpracovaná výjimka časového limitu")

    *Zpracovaná výjimka časového limitu*

> [!NOTE]
> Kromě toho můžete tuto aplikaci nasadit na weby Windows Azure [v následujícím dodatku D: publikování aplikace ASP.NET MVC 4 pomocí nasazení webu](#AppendixD).

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>Souhrn

V tomto praktickém cvičení jste se seznámili s některými novými funkcemi rezidenty v ASP.NET MVC 4. Byly popsány následující koncepty:

- Využijte výhod vylepšení šablon projektů ASP.NET MVC – včetně nové šablony projektu mobilní aplikace
- Použití atributů zobrazení HTML5 a dotazů na média šablon stylů CSS ke zlepšení zobrazení na mobilních zařízeních
- Použití jQuery Mobile pro progresivní vylepšení a vytváření webového uživatelského rozhraní optimalizovaného pro dotykové ovládání
- Vytváření zobrazení specifických pro mobilní zařízení
- Přepínání mezi zobrazeními mobilních a desktopových aplikací v aplikaci pomocí součásti pro přepínání zobrazení
- Vytváření asynchronních řadičů pomocí podpory úloh

<a id="AppendixA"></a>

<a id="Appendix_A_Using_Code_Snippets"></a>
## <a name="appendix-a-using-code-snippets"></a>Příloha A: používání fragmentů kódu

S fragmenty kódu máte veškerý kód, který potřebujete, na dosah ruky. Dokument testovacího prostředí vás přesně upozorní, když ho můžete používat, jak je znázorněno na následujícím obrázku.

![Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio](whats-new-in-aspnet-mvc-4/_static/image38.png "Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio")

*Vložení kódu do projektu pomocí fragmentů kódu sady Visual Studio*

***Přidání fragmentu kódu pomocí klávesnice (C# pouze)***

1. Umístěte kurzor na místo, kam chcete vložit kód.
2. Začněte psát název fragmentu (bez mezer a spojovníků).
3. Sledujte, jak IntelliSense zobrazuje stejné názvy fragmentů kódu.
4. Vyberte správný fragment kódu (nebo pokračujte v psaní, dokud není vybrán celý název tohoto fragmentu kódu).
5. Dvojím stisknutím klávesy TAB vložte fragment kódu do umístění kurzoru.

![Začněte psát název fragmentu.](whats-new-in-aspnet-mvc-4/_static/image39.png "Začněte psát název fragmentu.")

*Začněte psát název fragmentu.*

![Stisknutím klávesy TAB vyberte zvýrazněný fragment.](whats-new-in-aspnet-mvc-4/_static/image40.png "Stisknutím klávesy TAB vyberte zvýrazněný fragment.")

*Stisknutím klávesy TAB vyberte zvýrazněný fragment.*

![Stiskněte znovu TAB a fragment kódu se rozšíří.](whats-new-in-aspnet-mvc-4/_static/image41.png "Stiskněte znovu TAB a fragment kódu se rozšíří.")

*Stiskněte znovu TAB a fragment kódu se rozšíří.*

***Přidání fragmentu kódu pomocí myši (C#, Visual Basic a XML)***

1. Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu.
2. Vyberte **Vložit fragment** a potom **Moje fragmenty kódu**.
3. Kliknutím na něj ze seznamu vyberte příslušný fragment kódu.

![Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.](whats-new-in-aspnet-mvc-4/_static/image42.png "Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.")

*Klikněte pravým tlačítkem na místo, kam chcete vložit fragment kódu a vyberte Vložit fragment.*

![Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.](whats-new-in-aspnet-mvc-4/_static/image43.png "Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.")

*Vyberte příslušný fragment kódu ze seznamu kliknutím na něj.*

<a id="AppendixB"></a>

<a id="Appendix_B_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-b-installing-visual-studio-express-2012-for-web"></a>Příloha B: instalace Visual Studio Express 2012 pro web

**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** . Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.

1. Přejít na [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169). Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;*Visual Studio Express 2012 pro web pomocí sady Windows Azure SDK*&quot;.
2. Klikněte na **nainstalovat hned**. Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.
3. Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.

    ![Nainstalovat Visual Studio Express](whats-new-in-aspnet-mvc-4/_static/image44.png "Nainstalovat Visual Studio Express")

    *Nainstalovat Visual Studio Express*
4. Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**

    ![Přijetí licenčních podmínek](whats-new-in-aspnet-mvc-4/_static/image45.png)

    *Přijetí licenčních podmínek*
5. Počkejte na dokončení procesu stahování a instalace.

    ![Průběh instalace](whats-new-in-aspnet-mvc-4/_static/image46.png)

    *Průběh instalace*
6. Po dokončení instalace klikněte na **Dokončit**.

    ![Instalace dokončena](whats-new-in-aspnet-mvc-4/_static/image47.png)

    *Instalace dokončena*
7. Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.
8. Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .

    ![Dlaždice VS Express for Web](whats-new-in-aspnet-mvc-4/_static/image48.png)

    *Dlaždice VS Express for Web*

<a id="AppendixC"></a>

<a id="Appendix_C_Installing_WebMatrix_2_and_iPhone_Simulator"></a>
## <a name="appendix-c-installing-webmatrix-2-and-iphone-simulator"></a>Příloha C: instalace simulátoru WebMatrix 2 a iPhonu

Pro spuštění webu v simulovaném zařízení iPhone můžete použít rozšíření WebMatrix &quot;elektrického mobilního simulátoru pro iPhone&quot;pro iPhone. Můžete také nakonfigurovat stejné rozšíření pro spuštění simulátoru ze sady Visual Studio 2012.

<a id="ApxCTask1"></a>

<a id="Task_1_-_Installing_WebMatrix_2"></a>
#### <a name="task-1---installing-webmatrix-2"></a>Úloha 1 – instalace WebMatrixu 2

1. Přejít na [[https://go.microsoft.com/?linkid=9809776](https://go.microsoft.com/?linkid=9809776)](https://go.microsoft.com/?linkid=9810169). Případně, pokud již máte nainstalován instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;&quot;*WebMatrix 2* .
2. Klikněte na **nainstalovat hned**. Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.
3. Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.

    ![Nainstalovat WebMatrix 2](whats-new-in-aspnet-mvc-4/_static/image49.png "Nainstalovat WebMatrix 2")

    *Nainstalovat WebMatrix 2*
4. Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**

    ![Přijetí licenčních podmínek](whats-new-in-aspnet-mvc-4/_static/image50.png "Přijetí licenčních podmínek")

    *Přijetí licenčních podmínek*
5. Počkejte na dokončení procesu stahování a instalace.

    ![Průběh instalace](whats-new-in-aspnet-mvc-4/_static/image51.png "Průběh instalace")

    *Průběh instalace*
6. Po dokončení instalace klikněte na **Dokončit**.

    ![Instalace dokončena](whats-new-in-aspnet-mvc-4/_static/image52.png "Instalace dokončena")

    *Instalace dokončena*
7. Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.

<a id="ApxCTask2"></a>

<a id="Task_2_-_Installing_the_iPhone_Simulator_Extension"></a>
#### <a name="task-2---installing-the-iphone-simulator-extension"></a>Úloha 2 – instalace rozšíření simulátoru iPhonu

1. Spusťte **WebMatrix** a otevřete libovolný existující web nebo vytvořte nový.
2. Na pásu karet **Domů** klikněte na tlačítko **Spustit** a vyberte **Přidat nový**.

    ![Přidává se nové rozšíření WebMatrix.](whats-new-in-aspnet-mvc-4/_static/image53.png "Přidává se nové rozšíření WebMatrix.")

    *Přidává se nové rozšíření WebMatrix.*
3. Vyberte **simulátor iPhone** a klikněte na **nainstalovat**.

    ![Procházení rozšíření WebMatrixu](whats-new-in-aspnet-mvc-4/_static/image54.png "Procházení rozšíření WebMatrixu")

    *Procházení rozšíření WebMatrixu*
4. V podrobnostech balíčku kliknutím na **instalovat** pokračujte v instalaci rozšíření.

    ![rozšíření simulátoru iPhonu](whats-new-in-aspnet-mvc-4/_static/image55.png "rozšíření simulátoru iPhonu")

    *rozšíření simulátoru iPhonu*
5. Přečtěte si a přijměte smlouvu EULA pro rozšíření.

    ![Smlouva EULA rozšíření WebMatrix](whats-new-in-aspnet-mvc-4/_static/image56.png "Smlouva EULA rozšíření WebMatrix")

    *Smlouva EULA rozšíření WebMatrix*
6. Nyní můžete web spustit z WebMatrixu pomocí možnosti simulátoru iPhonu.

    ![Spustit pomocí iPhonu](whats-new-in-aspnet-mvc-4/_static/image57.png "Spustit pomocí iPhonu")

    *Spustit pomocí iPhonu*

<a id="ApxCTask3"></a>

<a id="Task_3_-_Configuring_Visual_Studio_2012_to_run_iPhone_Simulator"></a>
#### <a name="task-3---configuring-visual-studio-2012-to-run-iphone-simulator"></a>Úloha 3 – konfigurace sady Visual Studio 2012 pro spuštění simulátoru iPhonu

1. Otevřete **Visual Studio 2012** a otevřete libovolný web nebo vytvořte nový projekt.
2. Klikněte na šipku dolů na tlačítku spustit a vyberte **Procházet pomocí**.

    ![Procházet](whats-new-in-aspnet-mvc-4/_static/image58.png "Procházet")

    *Procházet*
3. V dialogovém okně &quot;procházení&quot; klikněte na tlačítko **Přidat**.
4. V dialogovém okně &quot;přidat program&quot; použijte následující hodnoty:

   - **Program**: C:\Users\*{CurrentUser} * \AppData\Local\Microsoft\WebMatrix\Extensions\20\iPhoneSimulator\ElectricMobileSim\ElectricMobileSim.exe *(aktualizujte cestu odpovídajícím způsobem)*
   - **Argumenty**: &quot;1&quot;
   - **Popisný název**: simulátor pro iPhone

     ![Přidat program](whats-new-in-aspnet-mvc-4/_static/image59.png "Přidat program")

     *Přidat program pro procházení*
5. Klikněte na **OK** a zavřete dialogová okna.
6. Nyní je možné spouštět webové aplikace v simulátoru iPhone ze sady Visual Studio 2012.

    ![Procházet simulátorem iPhone](whats-new-in-aspnet-mvc-4/_static/image60.png "Procházet simulátorem iPhone")

    *Procházet simulátorem iPhone*

<a id="AppendixD"></a>

<a id="Appendix_D_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-d-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Příloha D: publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu

V tomto dodatku se dozvíte, jak vytvořit nový web z Windows Azure Portál pro správu a jak publikovat aplikaci, kterou jste získali, pomocí testovacího prostředí s využitím funkce Nasazení webu pro publikování poskytované službou Windows Azure.

<a id="ApxDTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>Úloha 1 – Vytvoření nového webu z portálu Windows Azure

1. Přejít na [portál pro správu Windows Azure](https://manage.windowsazure.com/) a přihlaste se pomocí přihlašovacích údajů Microsoftu přidružených k vašemu předplatnému.

    > [!NOTE]
    > S Windows Azure můžete hostovat 10 ASP.NET webů zdarma a pak škálovat podle nárůstu provozu. [Tady](https://aka.ms/aspnet-hol-azure)se můžete zaregistrovat.

    ![Přihlaste se k Windows Azure Portal](whats-new-in-aspnet-mvc-4/_static/image61.png "Přihlaste se k Windows Azure Portal")

    *Přihlášení k Windows Azure Portál pro správu*
2. Na panelu příkazů klikněte na **Nový** .

    ![Vytvoření nového webu](whats-new-in-aspnet-mvc-4/_static/image62.png "Vytvoření nového webu")

    *Vytvoření nového webu*
3. Klikněte na **compute** | **Web**. Pak vyberte možnost **rychlé vytvoření** . Zadejte dostupnou adresu URL pro nový web a klikněte na **vytvořit web**.

    > [!NOTE]
    > Web Windows Azure je hostitelem webové aplikace běžící v cloudu, kterou můžete řídit a spravovat. Možnost rychle vytvořit umožňuje nasadit dokončenou webovou aplikaci do webu Windows Azure z oblasti mimo portál. Nezahrnuje kroky pro nastavení databáze.

    ![Vytvoření nového webu pomocí rychlého vytvoření](whats-new-in-aspnet-mvc-4/_static/image63.png "Vytvoření nového webu pomocí rychlého vytvoření")

    *Vytvoření nového webu pomocí rychlého vytvoření*
4. Počkejte, než se nový **Web** vytvoří.
5. Po vytvoření webu klikněte na odkaz ve sloupci **Adresa URL** . Ověřte, zda nový web funguje.

    ![Procházení na nový web](whats-new-in-aspnet-mvc-4/_static/image64.png "Procházení na nový web")

    *Procházení na nový web*

    ![Běžící Web](whats-new-in-aspnet-mvc-4/_static/image65.png "Běžící Web")

    *Běžící Web*
6. Vraťte se na portál a kliknutím na název webu pod sloupcem **název** zobrazíte stránky pro správu.

    ![Otevření stránek správy webu](whats-new-in-aspnet-mvc-4/_static/image66.png "Otevření stránek správy webu")

    *Otevření stránek správy webu*
7. Na stránce **řídicí panel** klikněte v části **rychlý přehled** na odkaz **Stáhnout profil publikování** .

    > [!NOTE]
    > *Profil publikování* obsahuje všechny informace potřebné k publikování webové aplikace na webu Windows Azure pro každou povolenou metodu publikace. Profil publikování obsahuje adresy URL, přihlašovací údaje uživatele a databázové řetězce potřebné k připojení a ověření proti jednotlivým koncovým bodům, pro které je povolena metoda publikace. **Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** a **Microsoft Visual Studio 2012** podporují čtení profilů publikování pro automatizaci konfigurace těchto programů pro publikování webových aplikací na webech Windows Azure.

    ![Stahuje se publikační profil webu.](whats-new-in-aspnet-mvc-4/_static/image67.png "Stahuje se publikační profil webu.")

    *Stahuje se publikační profil webu.*
8. Stáhněte si soubor profilu publikování do známého umístění. V tomto cvičení se dozvíte, jak tento soubor použít k publikování webové aplikace na webech Windows Azure ze sady Visual Studio.

    ![Ukládání souboru profilu publikování](whats-new-in-aspnet-mvc-4/_static/image68.png "Ukládá se publikační profil.")

    *Ukládání souboru profilu publikování*

<a id="ApxDTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>Úloha 2 – Konfigurace databázového serveru

Pokud vaše aplikace využívá SQL Server databází, budete muset vytvořit SQL Database Server. Pokud chcete nasadit jednoduchou aplikaci, která nepoužívá SQL Server, můžete tuto úlohu přeskočit.

1. Pro uložení aplikační databáze budete potřebovat server SQL Database. SQL Database servery můžete zobrazit z předplatného na portálu pro správu Windows Azure na stránce **databáze SQL** | **serverech** | **řídicím panelu serveru**. Pokud nemáte vytvořený server, můžete ho vytvořit pomocí tlačítka **Přidat** na panelu příkazů. Poznamenejte si **název serveru a adresu URL, přihlašovací jméno a heslo správce**, jak je budete používat v dalších úlohách. Databázi ještě nevytvářejte, protože bude vytvořená v pozdější fázi.

    ![Řídicí panel serveru SQL Database](whats-new-in-aspnet-mvc-4/_static/image69.png "Řídicí panel serveru SQL Database")

    *Řídicí panel serveru SQL Database*
2. V další úloze budete testovat připojení k databázi ze sady Visual Studio, z tohoto důvodu je třeba zahrnout místní IP adresu do seznamu **povolených IP adres**serveru. Chcete-li to provést, klikněte na tlačítko **Konfigurovat**, vyberte IP adresu z **aktuální IP adresy klienta** a vložte ji do textového pole **Počáteční IP adresa** a **koncová IP adresa** a klikněte na tlačítko ![přidat-Client-IP-Address-OK-tlačítko](whats-new-in-aspnet-mvc-4/_static/image70.png).

    ![Přidává se IP adresa klienta.](whats-new-in-aspnet-mvc-4/_static/image71.png)

    *Přidává se IP adresa klienta.*
3. Jakmile se **IP adresa klienta** přidá do seznamu povolených IP adres, potvrďte změny kliknutím na **Uložit** .

    ![Potvrdit změny](whats-new-in-aspnet-mvc-4/_static/image72.png)

    *Potvrdit změny*

<a id="ApxDTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Úloha 3 – publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu

1. Vraťte se do řešení ASP.NET MVC 4. V **Průzkumník řešení**klikněte pravým tlačítkem myši na webový projekt a vyberte **publikovat**.

    ![Publikování aplikace](whats-new-in-aspnet-mvc-4/_static/image73.png "Publikování aplikace")

    *Publikování webu*
2. Importujte profil publikování, který jste uložili v prvním úkolu.

    ![Import profilu publikování](whats-new-in-aspnet-mvc-4/_static/image74.png "Import profilu publikování")

    *Importuje se publikační profil.*
3. Klikněte na **ověřit připojení**. Po dokončení ověřování klikněte na **Další**.

    > [!NOTE]
    > Ověření je dokončeno, jakmile se zobrazí zelená značka zaškrtnutí vedle tlačítka ověřit připojení.

    ![Ověřování připojení](whats-new-in-aspnet-mvc-4/_static/image75.png "Ověřování připojení")

    *Ověřování připojení*
4. Na stránce **Nastavení** v části **databáze** klikněte na tlačítko vedle textového pole připojení k databázi (tj. **DefaultConnection**).

    ![Konfigurace nasazení webu](whats-new-in-aspnet-mvc-4/_static/image76.png "Konfigurace nasazení webu")

    *Konfigurace nasazení webu*
5. Připojení k databázi nakonfigurujte následujícím způsobem:

   - Do pole **název serveru** zadejte adresu URL serveru SQL Database pomocí předpony *TCP:* .
   - V **uživatelské jméno** zadejte přihlašovací jméno správce serveru.
   - V **heslo** zadejte přihlašovací heslo správce serveru.
   - Zadejte nový název databáze, například: *MVC4SampleDB*.

     ![Konfigurace cílového připojovacího řetězce](whats-new-in-aspnet-mvc-4/_static/image77.png "Konfigurace cílového připojovacího řetězce")

     *Konfigurace cílového připojovacího řetězce*
6. Pak klikněte na **OK**. Po zobrazení výzvy k vytvoření databáze klikněte na **Ano**.

    ![Vytvoření databáze](whats-new-in-aspnet-mvc-4/_static/image78.png "Vytváří se řetězec databáze.")

    *Vytvoření databáze*
7. Připojovací řetězec, který budete používat pro připojení k SQL Database ve Windows Azure, se zobrazí ve výchozím textovém poli připojení. Pak klikněte na tlačítko **Další**.

    ![Připojovací řetězec ukazující na SQL Database](whats-new-in-aspnet-mvc-4/_static/image79.png "Připojovací řetězec ukazující na SQL Database")

    *Připojovací řetězec ukazující na SQL Database*
8. Na stránce **Náhled** klikněte na **publikovat**.

    ![Publikování webové aplikace](whats-new-in-aspnet-mvc-4/_static/image80.png "Publikování webové aplikace")

    *Publikování webové aplikace*
9. Jakmile se proces publikování dokončí, otevře se ve výchozím prohlížeči publikovaný web.

    ![Aplikace byla publikována na platformě Windows Azure](whats-new-in-aspnet-mvc-4/_static/image81.png "Aplikace byla publikována na platformě Windows Azure")

    *Aplikace byla publikována na platformě Windows Azure*

---
uid: web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
title: Používání funkce Page Inspector v aplikaci Visual Studio 2012 | Microsoft Docs
author: rick-anderson
description: V tomto praktickém cvičení zjistíte nový nástroj pro vyhledání a opravu problémů s webovými stránkami v aplikaci Visual Studio – inspektor stránky. Page Inspector je nový nástroj, který b...
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 73232292-a5fe-4720-82a1-8f6553effd1f
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/using-page-inspector-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: f42b1be2697ba7d1145b3e334fe8f4ebf019cd12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586252"
---
# <a name="using-page-inspector-in-visual-studio-2012"></a>Použití Page Inspectoru v sadě Visual Studio 2012

podle [týmu webového Campy](https://twitter.com/webcamps)

> V tomto praktickém cvičení zjistíte nový nástroj pro vyhledání a opravu problémů s webovými stránkami v aplikaci Visual Studio – inspektor stránky.
> 
> Page Inspector je nový nástroj, který přináší nástroje pro diagnostiku prohlížeče do sady Visual Studio a poskytuje integrované prostředí mezi prohlížečem, ASP.NET a zdrojovým kódem. Vykresluje webovou stránku (HTML, webové formuláře, ASP.NET MVC nebo webové stránky) přímo v rámci integrovaného vývojového prostředí (IDE) sady Visual Studio a umožňuje prozkoumávat zdrojový kód i výsledný výstup. Nástroj Page Inspector umožňuje snadno rozložit web, rychle sestavit stránky od základů a rychle diagnostikovat problémy.
> 
> Současné době máme spoustu webových platforem, které včas vytvoří flexibilní a škálovatelné weby, jako je ASP.NET MVC a WebForms. Na druhé straně je obtížnější najít problémy na stránkách, protože rozhraní IDE nepodporuje zobrazení návrháře na stránkách založených na šablonách a dynamickém obsahu. Proto je nutné tyto weby otevřít v prohlížeči, abyste viděli, jak se zobrazují uživateli.
> 
> Vývojáři webu používají externí nástroje k nalezení potíží, které se pravidelně spouštějí v prohlížeči. Pak se vrátí do prostředí IDE a začnou opravit. Tato činnost zpět a z rozhraní IDE může být neefektivní a někdy vyžaduje nové nasazení a čištění mezipaměti pokaždé, když chcete reprodukování problému.
> 
> Nástroj Page Inspector vydává mezeru ve vývoji pro web mezi klientem (nástroji prohlížeče) a serverem (ASP.NET a zdrojový kód) tím, že spojuje to nejlepší z obou světů s využitím kombinované sady funkcí.
> 
> Pomocí nástroje Page Inspector vidíte, které prvky ve zdrojových souborech (včetně kódu na straně serveru) vytvořily kód HTML, který se má vykreslit v prohlížeči. Inspektor stránky také umožňuje upravit vlastnosti šablony stylů CSS a atributy elementu modelu DOM, aby se projevily změny, které se projeví v prohlížeči.
> 
> Tato praktická cvičení vás provedou funkcemi pro kontrolu stránky a ukáže vám, jak je můžete použít k opravě problémů ve webových aplikacích. **Toto testovací prostředí obsahuje dva cvičení pomocí podobných toků, ale zaměřuje se na různé technologie. Pokud jste vývojář ASP.NET MVC, postupujte podle jednoho cvičení. Pokud jste vývojářem WebForm, postupujte podle dvou cvičení**.
> 
> Toto testovací prostředí vás provede vylepšeními a novými funkcemi, které jsme dříve popsali pomocí menších změn ve vzorové webové aplikaci, která je součástí zdrojové složky.
> 
> Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici na adrese [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>Cíle

V této praktické laboratorní laboratoři se dozvíte, jak:

- Rozložit web pomocí funkce Page Inspector
- Kontrola a náhled změn stylů CSS pomocí funkce Page Inspector
- Zjišťování a opravy problémů na webových stránkách pomocí inspektoru stránky

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Předpoklady

K dokončení tohoto testovacího prostředí musíte mít následující položky:

- [Microsoft Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) nebo nadřazený seznam (pokyny k instalaci najdete v [příloze a](#AppendixA) ).
- Internet Explorer 9 nebo vyšší

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>Cvičení

Tato praktická cvičení zahrnují následující cvičení:

1. [Cvičení 1: použití funkce Page Inspector v projektech ASP.NET MVC](#Exercise1)
2. [Cvičení 2: použití funkce Page Inspector v projektech WebForms](#Exercise2)

> [!NOTE]
> Každé cvičení je součástí počátečního řešení, které se nachází ve složce Begin cvičení, která umožňuje sledovat jednotlivá cvičení nezávisle na ostatních. Ve zdrojovém kódu cvičení také najdete koncovou složku obsahující řešení sady Visual Studio s kódem, který je výsledkem dokončení kroků v příslušném cvičení. Tato řešení můžete použít jako návod, pokud potřebujete další pomoc při práci s tímto praktickým cvičením.

Odhadovaný čas dokončení tohoto testovacího prostředí: **30 minut**.

<a id="Exercise1"></a>

<a id="Exercise_1_Using_Page_Inspector_in_ASPNET_MVC_Projects"></a>
### <a name="exercise-1-using-page-inspector-in-aspnet-mvc-projects"></a>Cvičení 1: použití funkce Page Inspector v projektech ASP.NET MVC

V tomto cvičení se naučíte, jak zobrazit náhled a ladit řešení **ASP.NET MVC 4** pomocí nástroje **Page Inspector**. Nejdřív provedete stručným poznámkou kolem tohoto nástroje, abyste se seznámili s funkcemi, které usnadňují proces ladění na webu. Pak budete pracovat na webové stránce, která obsahuje problémy se stylem. Naučíte se, jak pomocí nástroje Page Inspector najít zdrojový kód, který vygeneruje problém, a opraví ho.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a>Úloha 1 – prozkoumávání inspektoru stránky

V této úloze se naučíte používat inspektor stránky v kontextu projektu ASP.NET MVC 4, který obsahuje galerii fotografií.

1. Otevřete řešení **zahájit** , které se nachází ve složce **source/EX1-MVC4/Begin/** Folder.

   1. Než budete pokračovat, budete muset stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
2. V Průzkumník řešení Najděte zobrazení **index. cshtml** ve složce projektu **/views/Home** , klikněte na něj pravým tlačítkem myši a vyberte **Zobrazit v okně Kontrola stránky**.

    ![Výběr souboru pro náhled v inspektoru stránky](using-page-inspector-in-visual-studio-2012/_static/image1.png "Výběr souboru pro náhled v inspektoru stránky")

    *Výběr souboru pro náhled v inspektoru stránky*
3. V okně Inspektor stránky se zobrazí adresa URL */Home/index* mapovaná na zobrazení zdroje, které jste vybrali.

    ![První kontakt s PageInspector](using-page-inspector-in-visual-studio-2012/_static/image2.png)

    *První kontakt s nástrojem Page Inspector*

    Nástroj Page Inspector je integrovaný do vašeho prostředí sady Visual Studio. Inspektor obsahuje vložený prohlížeč spolu s výkonným profilerem HTML. Všimněte si, že nemusíte spouštět řešení, abyste viděli, jak stránky vypadají.

    > [!NOTE]
    > Je-li šířka okna Prohlížeč kontroly stránky menší než šířka otevřené stránky, stránka se nezobrazí správně. Pokud k tomu dojde, upravte šířku nástroje Page Inspector.
4. V okně Inspektor stránky klikněte na kartu **soubory** .

    Zobrazí se všechny zdrojové soubory, které vytváří stránku indexu. Tato funkce usnadňuje identifikaci všech prvků na první pohled, zejména při práci s částečnými zobrazeními a šablonami. Všimněte si, že pokud kliknete na odkazy, můžete také otevřít jednotlivé soubory.

    ![The-Files-tab](using-page-inspector-in-visual-studio-2012/_static/image3.png)

    *Karta soubory*
5. Klikněte na tlačítko **Přepnout režim kontroly** , které najdete vlevo na kartách.

    Tento nástroj umožňuje vybrat libovolný prvek stránky a zobrazit jeho kód HTML a Razor.

    ![Přepínač-prohlídky-režim – tlačítko](using-page-inspector-in-visual-studio-2012/_static/image4.png)

    *Přepnout tlačítko režimu kontroly*
6. V prohlížeči Inspector stránky přesuňte ukazatel myši nad prvky stránky. Při přesunutí ukazatele myši na jakoukoli část vykreslené stránky se zobrazí typ elementu a v editoru sady Visual Studio je zvýrazněn odpovídající zdrojový kód nebo kód.

    ![Režim kontroly v akci](using-page-inspector-in-visual-studio-2012/_static/image5.png)

    *Režim kontroly v akci*

    > [!NOTE]
    > Nemaximalizujte okno nástroje Page Inspector nebo nebudete moci zobrazit kartu náhledu zobrazující zdrojový kód. Pokud při maximalizaci kliknete na prvek v inspektoru stránky, bude zobrazen zdrojový kód výběru, ale skryje okno Inspektor stránky.

    Pokud platíte pozornost souboru **index. cshtml** , zjistíte, že část zdrojového kódu, který generuje vybraný prvek, je zvýrazněna. Tato funkce usnadňuje úpravy dlouhých zdrojových souborů a poskytuje přímý a rychlý způsob přístupu ke kódu.

    ![Kontrola elementů](using-page-inspector-in-visual-studio-2012/_static/image6.png)

    *Kontrola elementů*
7. Klikněte na tlačítko **Přepnout režim kontroly** (![Vyberte kartu HTML a zobrazte kód HTML vykreslený v prohlížeči Inspector stránky).](using-page-inspector-in-visual-studio-2012/_static/image7.png "Vyberte kartu HTML pro zobrazení kódu HTML vykresleného v prohlížeči Inspector stránky.") ), chcete-li zakázat kurzor.
8. Vyberte kartu **HTML** pro zobrazení kódu HTML vykresleného v prohlížeči Inspector stránky.
9. V kódu HTML vyhledejte položku seznam s odkazem na Koala a vyberte ji.

    Všimněte si, že když vyberete kód, odpovídající výstup je automaticky zvýrazněn v prohlížeči. Tato funkce je užitečná k tomu, abyste viděli, jak se na stránce vykresluje blok HTML.

    ![Výběr prvku HTML na stránce](using-page-inspector-in-visual-studio-2012/_static/image8.png "Výběr prvku HTML na stránce")

    *Výběr prvku HTML na stránce*
10. Kliknutím na tlačítko **Přepnout režim kontroly** povolíte *režim kontroly* a kliknete na navigační panel. Napravo od kódu HTML v podokně styly se zobrazí seznam s styly CSS použitými pro vybraný prvek.

    > [!NOTE]
    > Vzhledem k tomu, že hlavička je součástí rozložení lokality, bude také otevřen vzhled stránky \_layout. cshtml a byl zvýrazněn segment ovlivněného kódu.

    ![Zjišťují se styly](using-page-inspector-in-visual-studio-2012/_static/image9.png)

    *Zjišťují se styly a zdrojové soubory vybraného elementu.*
11. Když je povolen ukazatel pro přepnutí kontroly, přesuňte ukazatel myši pod modrý zvýrazněný pruh a klikněte na jeho poloviční kruh.

    ![Výběr elementu](using-page-inspector-in-visual-studio-2012/_static/image10.png "Výběr elementu")

    *Výběr elementu*
12. V podokně styly vyhledejte položku **obrázek pozadí** pod skupinou **. Main-Content** . **Zrušte kontrolu** **obrázku na pozadí** a podívejte se, co se stane. Všimněte si, že prohlížeč projeví změny okamžitě a kroužek je skrytý.

    > [!NOTE]
    > Změny, které použijete na kartě styly kontroly stránky, neovlivní původní šablonu stylů. Můžete zrušit kontrolu stylů nebo změnit jejich hodnoty tolikrát, kolikrát chcete, ale budou obnoveny po obnovení stránky.

    ![Povolení a zakázání stylů CSS](using-page-inspector-in-visual-studio-2012/_static/image11.png "Povolení a zakázání stylů CSS")

    *Povolení a zakázání stylů CSS*
13. Nyní klikněte na text**loga**v záhlaví pomocí kontrolního režimu.
14. Na kartě **styly** vyhledejte atribut CSS **velikosti písma** v rámci skupiny **. site-title** . Dvakrát klikněte na hodnotu atributu a nahraďte 2,3 em hodnotou **3 em**a pak stiskněte **ENTER**. Všimněte si, že nadpis vypadá větší.

    ![Změna hodnot šablon stylů CSS v inspektoru stránky](using-page-inspector-in-visual-studio-2012/_static/image12.png "Změna hodnot šablon stylů CSS v inspektoru stránky")

    *Změna hodnot šablon stylů CSS v inspektoru stránky*
15. Klikněte na kartu **Styly trasování** , která se nachází v pravém podokně okna Page Inspector. Toto je alternativní způsob, jak zobrazit všechny styly použité pro výběr, seřazené podle názvu atributu.

    ![Styly CSS – trasování](using-page-inspector-in-visual-studio-2012/_static/image13.png)

    *Styly CSS – trasování vybraného elementu*
16. Další funkcí nástroje Page Inspector je podokno rozložení. Pomocí režimu kontroly vyberte navigační panel a pak klikněte na kartu **rozložení** v pravém podokně. Zobrazí se přesná velikost vybraného prvku a také jeho posun, okraj, odsazení a velikost ohraničení. Všimněte si, že můžete také upravit hodnoty z tohoto zobrazení.

    ![Rozložení prvku v inspektoru stránky](using-page-inspector-in-visual-studio-2012/_static/image14.png "Rozložení prvku v inspektoru stránky")

    *Rozložení prvku v inspektoru stránky*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a>Úloha 2 – hledání a oprava problémů s styly v galerii fotografií

Jak byste měli diagnostikovat problémy s webovými stránkami v předchozích verzích sady Visual Studio? Máte pravděpodobně zkušenosti s nástroji pro ladění webu, které běží mimo Visual Studio IDE, jako je Internet Explorer Vývojářské nástroje nebo Firebug. Prohlížeče porozuměly pouze HTML, skriptování a styly, zatímco základní rozhraní generuje kód HTML, který bude vykreslen. Z tohoto důvodu často potřebujete nasadit celou lokalitu, abyste viděli, jak vypadají webové stránky.

Tento postup jste pravděpodobně provedli, když jste chtěli zjistit a opravit problém na webu:

1. Spusťte řešení ze sady Visual Studio nebo nasaďte stránku na webový server.
2. V prohlížeči otevřete vývojářské nástroje, které používáte, nebo jednoduše otevřete zdrojový kód a styly a pokuste se problém splnit. Chcete-li najít příslušné soubory, měli byste použít &quot;Search&quot; nebo &quot;Hledat v souborech&quot; funkce s názvem tříd stylů.
3. Po zjištění chyby zastavte webový prohlížeč a Server.
4. Vymažte mezipaměť prohlížeče.
5. Vraťte se do sady Visual Studio a použijte opravu. Opakujte všechny kroky, které chcete otestovat.

Vzhledem k nepřítomnosti reálného WYSIWYG v ASP.NET MVC 4 se většina problémů se styly detekuje v pozdější fázi po spuštění nebo nasazení webové aplikace. Teď můžete pomocí nástroje Page Inspector zobrazit náhled libovolné stránky bez spuštění řešení.

V této úloze použijete inspektor stránky a opravíte některé problémy aplikace Fotogalerie.

1. Pomocí nástroje Page Inspector Najděte **Rejstřík** a **přihlašovací** odkazy na levé straně záhlaví.

    Všimněte si, že odkazy se nezobrazují na očekávaném místě na pravé straně a zobrazují se jako seznam s odrážkami. Teď budete zarovnávat odkazy na pravé a odpovídajícím způsobem změnit jejich styl.

    ![Vyhledání odkazů registru a přihlášení](using-page-inspector-in-visual-studio-2012/_static/image15.png "Vyhledání odkazů registru a přihlášení")

    *Vyhledání odkazů registru a přihlášení*
2. Když je vybraný přepínač přepnout do režimu kontroly, klikněte na tlačítko Zavřít na, ale ne na, na odkaz registrovat a otevřete jeho kód.

    Všimněte si, že zdrojový kód odkazů je umístěn v souboru **\_LoginPartial. cshtml** , nikoli index. cshtml ani \_layout. cshtml, což jsou místa, která se mohou nacházet na prvním místě. Přímo jste umístili do správného zdrojového souboru.
3. Na kartě **styly** vyhledejte a klikněte na **oddíl\<> #login** položku, což je kontejner HTML pro tyto odkazy.

    Všimněte si, že po kliknutí na tlačítko se styl **#login** automaticky nachází v umístění **Web. CSS** . Kromě toho je nyní zvýrazněn kód.

    ![Výběr stylů CSS](using-page-inspector-in-visual-studio-2012/_static/image16.png "Výběr stylů CSS")

    *Výběr stylů CSS*
4. Odkomentujte atribut **Text-Align** ve zvýrazněném kódu odebráním počátečních a uzavíracích znaků a uložte soubor **Web. CSS** .

    Page Inspector ví o všech různých souborech, které tvoří aktuální stránku, a může rozpoznat, kdy se některé z těchto souborů změní. Upozorní vás vždy, když aktuální stránka v prohlížeči nebude synchronizována se zdrojovými soubory.
5. V prohlížeči Inspector stránky klikněte na pruh umístěný pod adresním řádkem a znovu načtěte stránku.

    ![Opětovné načtení stránky](using-page-inspector-in-visual-studio-2012/_static/image17.png)

    *Opětovné načtení stránky*

    Odkazy jsou nyní na pravé straně, ale stále vypadají jako seznam s odrážkami. Teď odrážky odeberete a zarovnejte je vodorovně.

    ![Aktualizovaná stránka](using-page-inspector-in-visual-studio-2012/_static/image18.png)

    *Aktualizovaná stránka*
6. V režimu kontroly vyberte některou z **&lt;li&gt;** položky, které obsahují &quot;registru&quot; a &quot;přihlášení&quot;. Potom kliknutím na **oddíl&lt;&gt; #login** položku přejděte na **styly. CSS** kód.

    ![Hledání stylu](using-page-inspector-in-visual-studio-2012/_static/image19.png "Hledání stylu")

    *Hledání stylu*
7. V **style. CSS**Odkomentujte kód pro **#login li** položky. Styl, který přidáváte, skryje odrážku a položky se zobrazí vodorovně.

    ![Přestylování přihlašovacích odkazů](using-page-inspector-in-visual-studio-2012/_static/image20.png "Přestylování přihlašovacích odkazů")

    *Přestylování přihlašovacích odkazů*
8. Uložte soubor **style. CSS** a klikněte na panel umístěný pod adresou pro opětovné načtení stránky. Všimněte si, že se odkazy zobrazují správně.

    ![Odkazy zarovnané na pravou stranu](using-page-inspector-in-visual-studio-2012/_static/image21.png "Odkazy zarovnané na pravou stranu")

    *Odkazy zarovnané na pravou stranu*
9. Nakonec budete měnit Nadpis záhlaví. Pomocí režimu kontroly klikněte na **své logo** a získejte zdrojový kód, který ho generuje.
10. Nyní jste v **\_layout. cshtml**, nahraďte text '**logo tady**'**textem ' Fotogalerie '.** Uložte a aktualizujte prohlížeč Inspector stránky.

    ![Přiřazení nového názvu](using-page-inspector-in-visual-studio-2012/_static/image22.png "Přiřazení nového názvu")

    *Přiřazení nového názvu*

    ![Stránka Galerie fotografií](using-page-inspector-in-visual-studio-2012/_static/image23.png)

    *Stránka Galerie fotografií aktualizována*
11. Nakonec vyberte projekt **Galerie** a stisknutím klávesy **F5** spusťte aplikaci. Podívejte se na všechny změny, které fungují podle očekávání.

---

<a id="Exercise2"></a>

<a id="Exercise_2_Using_Page_Inspector_in_WebForms_Projects"></a>
### <a name="exercise-2-using-page-inspector-in-webforms-projects"></a>Cvičení 2: použití funkce Page Inspector v projektech WebForms

V tomto cvičení se naučíte, jak zobrazit náhled a ladit řešení webových formulářů pomocí nástroje Page Inspector. Nejprve provedete stručný ovládací proces kolem nástroje, abyste se seznámili s funkcemi pro inspektor stránek, které usnadňují proces ladění na webu. Pak budete pracovat na webové stránce, která obsahuje problémy se stylem. Naučíte se, jak pomocí nástroje Page Inspector najít zdrojový kód, který vygeneruje problém, a opraví ho.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Exploring_Page_Inspector"></a>
#### <a name="task-1---exploring-page-inspector"></a>Úloha 1 – prozkoumávání inspektoru stránky

V této úloze se naučíte používat funkce nástroje Page Inspector v kontextu projektu webových formulářů, který zobrazuje galerii fotografií.

1. Otevřete řešení **zahájit** ve složce **source/EX2-webformaes/Begin/** Folder.

   1. Než budete pokračovat, budete muset stáhnout některé chybějící balíčky NuGet. Provedete to tak, že kliknete na nabídku **projekt** a vyberete **Spravovat balíčky NuGet**.
   2. V dialogovém okně **Spravovat balíčky NuGet** klikněte na **obnovit** , aby se stáhly chybějící balíčky.
   3. Nakonec sestavte řešení kliknutím na **sestavit** | **Sestavit řešení**.

      > [!NOTE]
      > Jednou z výhod používání NuGet je, že nemusíte dodávat všechny knihovny v projektu, což snižuje velikost projektu. Pomocí nástrojů NuGet Power Tools zadáte verze balíčku v souboru Packages. config a při prvním spuštění projektu budete moct stáhnout všechny požadované knihovny. To je důvod, proč po otevření existujícího řešení z tohoto testovacího prostředí budete muset spustit tyto kroky.
2. V Průzkumník řešení Najděte stránku **Default. aspx** , klikněte na ni pravým tlačítkem myši a v **okně Kontrola stránky vyberte Zobrazit**.

    ![Otevření default. aspx s nástrojem Page Inspector](using-page-inspector-in-visual-studio-2012/_static/image24.png "Otevření default. aspx s nástrojem Page Inspector")

    *Otevření default. aspx s nástrojem Page Inspector*
3. V okně Inspektor stránky se zobrazí stránka default. aspx.

    ![Zobrazení Default. aspx v inspektoru stránky](using-page-inspector-in-visual-studio-2012/_static/image25.png "Zobrazení Default. aspx v inspektoru stránky")

    *Zobrazení Default. aspx v inspektoru stránky*

    Nástroj Page Inspector je integrovaný do vašeho prostředí sady Visual Studio. Inspektor obsahuje vložený prohlížeč spolu s výkonným profilerem HTML, který zobrazí vybraný kód. Všimněte si, že nemusíte spouštět řešení, abyste viděli, jak stránky vypadají.

    > [!NOTE]
    > Je-li šířka okna Prohlížeč kontroly stránky menší než šířka otevřené stránky, stránka se nezobrazí správně. Pokud k tomu dojde, upravte šířku nástroje Page Inspector.
4. V okně Inspektor stránky klikněte na kartu **soubory** .

    Zobrazí se všechny zdrojové soubory, které budou sestavovat vykreslenou výchozí stránku. Tato funkce je užitečná k identifikaci všech prvků na první pohled, zejména při práci s uživatelskými ovládacími prvky a stránkami předlohy. Všimněte si, že můžete také přejít na jednotlivé soubory.

    ![Karta soubory](using-page-inspector-in-visual-studio-2012/_static/image26.png "Karta soubory")

    *Karta soubory*
5. Klikněte na tlačítko **Přepnout režim kontroly** , které najdete vlevo na kartách.

    Tento nástroj umožňuje vybrat libovolný prvek stránky a zobrazit jeho kód HTML a zdroj. aspx.

    ![Přepnout tlačítko režimu kontroly](using-page-inspector-in-visual-studio-2012/_static/image27.png "Přepnout tlačítko režimu kontroly")

    *Přepnout tlačítko režimu kontroly*
6. V prohlížeči Inspector stránky přesuňte ukazatel myši na prvky stránky. Při přesunutí ukazatele myši na jakoukoli část vykreslené stránky se zobrazí typ elementu a v editoru sady Visual Studio je zvýrazněn odpovídající zdrojový kód nebo kód.

    ![Režim kontroly v akci](using-page-inspector-in-visual-studio-2012/_static/image28.png "Režim kontroly v akci")

    *Režim kontroly v akci*

    > [!NOTE]
    > Nemaximalizujte okno nástroje Page Inspector nebo nebudete moci zobrazit kartu náhledu zobrazující zdrojový kód. Pokud při maximalizaci kliknete na prvek v inspektoru stránky, bude zobrazen zdrojový kód výběru, ale skryje okno Inspektor stránky.

    Pokud platíte pozornost **výchozímu souboru. aspx** , Všimněte si, že je zvýrazněna část zdrojového kódu, která generuje vybraný prvek. Tato funkce usnadňuje edici dlouhých zdrojových souborů a poskytuje přímý a rychlý způsob přístupu ke kódu.

    ![Kontrola elementů](using-page-inspector-in-visual-studio-2012/_static/image29.png "Kontrola elementů")

    *Kontrola elementů*
7. Klikněte na tlačítko **Přepnout do režimu kontroly** (![Vyberte-The-HTML-TAB-to-display-the-HTML-code-in-the-Page-Inspector-browser).](using-page-inspector-in-visual-studio-2012/_static/image30.png "Vyberte-The-HTML-TAB-to-display-the-HTML-Code-Ed-in-the-Page-Inspector-Browser.") ) nacházející se na kartách inspektora stránky pro zakázání kurzoru.
8. Vyberte kartu **HTML** pro zobrazení kódu HTML vykresleného v prohlížeči Inspector stránky.
9. V kódu HTML vyhledejte položku seznamu s odkazem na Koala a vyberte ji.

    Všimněte si, že když vyberete kód, odpovídající výstup je automaticky zvýrazněný prohlížeč. Tato funkce je užitečná k tomu, abyste viděli, jak se na stránce vykresluje blok HTML.

    ![Výběr prvku HTML na stránce](using-page-inspector-in-visual-studio-2012/_static/image31.png "Výběr prvku HTML na stránce")

    *Výběr prvku HTML na stránce*
10. Kliknutím na tlačítko **Přepnout režim kontroly** povolíte *režim kontroly* a kliknete na navigační panel. Napravo od kódu HTML v podokně styly se zobrazí seznam s styly CSS použitými pro vybraný prvek.

    > [!NOTE]
    > vzhledem k tomu, že hlavička je součástí rozložení lokality, bude také otevřen soubor site. Master a zvýrazněný segment ovlivněného kódu.

    ![Zjišťují se styly WebForms.](using-page-inspector-in-visual-studio-2012/_static/image32.png "Zjišťují se styly a zdrojové soubory vybraného elementu.")

    *Zjišťují se styly a zdrojové soubory vybraného elementu.*
11. Když je povolen ukazatel pro přepnutí kontroly, přesuňte ukazatel myši pod panelem nabídek a klikněte na prázdný poloviční kroužek.

    ![Výběr elementu](using-page-inspector-in-visual-studio-2012/_static/image33.png "Výběr elementu")

    *Výběr elementu*
12. V podokně styly vyhledejte položku **obrázek pozadí** pod skupinou **. Main-Content** . **Zrušte kontrolu** **obrázku na pozadí** a podívejte se, co se stane. Všimněte si, že prohlížeč projeví změny okamžitě a kroužek je skrytý.

    > [!NOTE]
    > Změny, které použijete na kartě styly kontroly stránky, neovlivní původní šablonu stylů. Můžete zrušit kontrolu stylů nebo změnit jejich hodnoty tolikrát, kolikrát chcete, ale budou obnoveny po obnovení stránky.

    ![Povolení a zakázání šablon stylů CSS styles2](using-page-inspector-in-visual-studio-2012/_static/image34.png "Povolení a zakázání stylů CSS")

    *Povolení a zakázání stylů CSS*
13. Nyní klikněte na text loga**v záhlaví** pomocí kontrolního režimu.
14. Na kartě **styly** vyhledejte atribut CSS **velikosti písma** v rámci skupiny **. site-title** . Dvakrát klikněte na atribut jednou a upravte jeho hodnotu. Nahraďte hodnotu 2.3 em hodnotou **3em**a stiskněte klávesu ENTER. Všimněte si, že nadpis vypadá větší.

    ![Změna hodnot šablon stylů CSS na stránce Inspector2](using-page-inspector-in-visual-studio-2012/_static/image35.png "Změna hodnot šablon stylů CSS v inspektoru stránky")

    *Změna hodnot šablon stylů CSS v inspektoru stránky*
15. Klikněte na kartu **Styly trasování** , která se nachází v pravém podokně okna Page Inspector. Toto je alternativní způsob, jak zobrazit všechny styly použité pro výběr, seřazené podle názvu atributu.

    ![Styly CSS – trasování vybraného elementu](using-page-inspector-in-visual-studio-2012/_static/image36.png "Styly CSS – trasování vybraného elementu")

    *Styly CSS – trasování vybraného elementu*
16. Další funkcí nástroje Page Inspector je podokno rozložení. Pomocí režimu kontroly vyberte navigační panel a pak klikněte na kartu **rozložení** v pravém podokně. Zobrazí se přesná velikost vybraného prvku a také jeho posun, okraj, odsazení a velikost ohraničení. Všimněte si, že můžete také upravit hodnoty z tohoto zobrazení.

    ![Rozložení prvku v inspektoru stránky](using-page-inspector-in-visual-studio-2012/_static/image37.png "Rozložení prvku v inspektoru stránky")

    *Rozložení prvku v inspektoru stránky*

<a id="Ex2Task2"></a>

<a id="Task_2_-_Finding_and_Fixing_Style_Issues_in_the_Photo_Gallery"></a>
#### <a name="task-2---finding-and-fixing-style-issues-in-the-photo-gallery"></a>Úloha 2 – hledání a oprava problémů s styly v galerii fotografií

Jak byste měli diagnostikovat problémy s webovými stránkami v předchozích verzích sady Visual Studio? Máte pravděpodobně zkušenosti s nástroji pro ladění webu, které běží mimo Visual Studio IDE, jako je Internet Explorer Vývojářské nástroje nebo Firebug. Prohlížeče porozuměly pouze HTML, skriptování a styly, zatímco základní rozhraní generuje kód HTML, který bude vykreslen. Z tohoto důvodu často potřebujete nasadit celou lokalitu, abyste viděli, jak vypadají webové stránky.

Tento postup jste pravděpodobně provedli, když jste chtěli zjistit a opravit problém na webu:

1. Spusťte řešení ze sady Visual Studio nebo nasaďte stránku na webový server.
2. V prohlížeči otevřete vývojářské nástroje, které používáte, nebo jednoduše otevřete zdrojový kód a styly a pokuste se problém splnit. Chcete-li najít soubory, jste použili &quot;Search&quot; nebo &quot;Hledat v souborech&quot; funkce s názvem tříd stylů.
3. Po zjištění chyby zastavte webový prohlížeč a Server.
4. Vymažte mezipaměť prohlížeče.
5. Vraťte se do sady Visual Studio a použijte opravu. Opakujte všechny kroky, které chcete otestovat.

Vzhledem k nepřítomnosti reálného WYSIWYG v ASP.NET WebForms se v pozdější fázi zjistí některé problémy se stylem po spuštění nebo nasazení. Teď můžete pomocí nástroje Page Inspector zobrazit náhled libovolné stránky bez spuštění řešení.

V této úloze použijete inspektor stránky k opravě některých problémů aplikace Fotogalerie. V následujících krocích zjistíte a rychle opravíte některé problémy s jednoduchým stylem v hlavičce.

1. Pomocí kontroly stránky vyhledejte **Rejstřík** a **přihlašovací** odkazy na levé straně záhlaví.

    Všimněte si, že odkaz není zobrazen na očekávaném místě na pravé straně. Nyní zarovnáte vazbu k pravému a správnému stylu.

    ![Odkaz na přihlášení umístěný vlevo](using-page-inspector-in-visual-studio-2012/_static/image38.png "Odkaz na přihlášení umístěný vlevo")

    *Odkaz na přihlášení umístěný vlevo*
2. Když je vybraný přepínač přepnout do režimu kontroly, vyberte odkaz pro přihlášení a otevřete jeho kód.

    Všimněte si, že zdrojový kód odkazu je umístěný v souboru **Web. Master** , nikoli na stránce Default. aspx, která je místem, kde se můžete podívat na první místo. přímo jste umístili do správného zdrojového souboru.
3. Na kartě **styly** vyhledejte a klikněte na **oddíl&lt;&gt; #login** položku, což je kontejner HTML pro tyto odkazy.

    Všimněte si, že po kliknutí na tlačítko se styl **#login** automaticky nachází v umístění **Web. CSS** . Kromě toho je nyní zvýrazněn kód.

    ![Výběr stylů CSS](using-page-inspector-in-visual-studio-2012/_static/image39.png "Výběr stylů CSS")

    *Výběr stylů CSS*
4. Odkomentujte atribut **Text-Align** ve zvýrazněném kódu odebráním počátečních a uzavíracích znaků a uložte soubor **Web. CSS** .

    Page Inspector ví o všech různých souborech, které tvoří aktuální stránku, a může rozpoznat, kdy se některé z těchto souborů změní. Upozorní vás vždy, když aktuální stránka v prohlížeči nebude synchronizována se zdrojovými soubory.
5. V prohlížeči Inspector stránky klikněte na pruh nacházející se pod adresním řádkem a uložte změny a znovu načtěte stránku.

    ![Opětovné načtení stránky](using-page-inspector-in-visual-studio-2012/_static/image40.png)

    *Opětovné načtení stránky*

    Odkazy jsou nyní na pravé straně, ale stále vypadají jako seznam s odrážkami. Teď odrážky odeberete a zarovnejte je vodorovně.

    ![Aktualizovaná stránka](using-page-inspector-in-visual-studio-2012/_static/image41.png)

    *Aktualizovaná stránka*
6. V režimu kontroly vyberte některou z **&lt;li&gt;** položky, které obsahují &quot;registru&quot; a &quot;přihlášení&quot;. Potom kliknutím na **oddíl&lt;&gt; #login** položku přejděte na **styly. CSS** kód.

    ![Hledání stylu](using-page-inspector-in-visual-studio-2012/_static/image42.png "Hledání stylu")

    *Hledání stylu*
7. V **style. CSS**Odkomentujte kód pro **#login li** položky. Styl, který přidáváte, skryje odrážku a položky se zobrazí vodorovně.

    ![Přestylování přihlašovacích odkazů](using-page-inspector-in-visual-studio-2012/_static/image43.png "Přestylování přihlašovacích odkazů")

    *Přestylování přihlašovacích odkazů*
8. Uložte soubor **style. CSS** a klikněte na panel umístěný pod adresou pro opětovné načtení stránky. Všimněte si, že se odkazy zobrazují správně.

    ![Odkazy zarovnané na pravou stranu](using-page-inspector-in-visual-studio-2012/_static/image44.png "Odkazy zarovnané na pravou stranu")

    *Odkazy zarovnané na pravou stranu*
9. Nakonec budete měnit Nadpis záhlaví. Místo hledání textu**loga** ve všech souborech použijte režim kontroly, ve kterém můžete kliknout na text a načíst zdrojový kód, který ho generuje.

    ![Hledání názvu webu](using-page-inspector-in-visual-studio-2012/_static/image45.png "Hledání názvu webu")

    *Hledání názvu webu*
10. Teď jste v souboru **Web. Master**a místo toho zadejte text**loga** **pomocí Fotogalerie.** Uložte a aktualizujte prohlížeč Inspector stránky.

    ![Stránka Galerie fotografií aktualizována](using-page-inspector-in-visual-studio-2012/_static/image46.png "Stránka Galerie fotografií aktualizována")

    *Stránka Galerie fotografií aktualizována*
11. Nakonec stisknutím klávesy **F5** spusťte aplikaci. všechny změny fungují podle očekávání.

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a>Souhrn

Po absolvování tohoto praktického cvičení se naučíte, jak pomocí nástroje Page Inspector zobrazit náhled webové aplikace, aniž by bylo nutné znovu sestavit a spustit web v prohlížeči. Navíc se naučíte, jak rychle najít a opravit chyby přístupem přímo z vykresleného výstupu ke zdrojovému kódu.

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Příloha A: instalace Visual Studio Express 2012 pro web

**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** . Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.

1. Přejít na [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169). Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;<em>Visual Studio Express 2012 pro web pomocí sady Windows Azure SDK</em>&quot;.
2. Klikněte na **nainstalovat hned**. Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.
3. Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.

    ![Nainstalovat Visual Studio Express](using-page-inspector-in-visual-studio-2012/_static/image47.png "Nainstalovat Visual Studio Express")

    *Nainstalovat Visual Studio Express*
4. Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**

    ![Přijetí licenčních podmínek](using-page-inspector-in-visual-studio-2012/_static/image48.png)

    *Přijetí licenčních podmínek*
5. Počkejte na dokončení procesu stahování a instalace.

    ![Průběh instalace](using-page-inspector-in-visual-studio-2012/_static/image49.png)

    *Průběh instalace*
6. Po dokončení instalace klikněte na **Dokončit**.

    ![Instalace dokončena](using-page-inspector-in-visual-studio-2012/_static/image50.png)

    *Instalace dokončena*
7. Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.
8. Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .

    ![Dlaždice VS Express for Web](using-page-inspector-in-visual-studio-2012/_static/image51.png)

    *Dlaždice VS Express for Web*

---
uid: visual-studio/overview/2013/visual-studio-2013-web-tools
title: 'Praktická cvičení: Visual Studio 2013 Web Tools | Microsoft Docs'
author: rick-anderson
description: Visual Studio je vynikající vývojové prostředí pro. SÍTĚ Windows a webové projekty. Obsahuje výkonný textový editor, který lze snadno použít k...
ms.author: riande
ms.date: 07/16/2014
ms.assetid: 09e82351-816b-402d-acd1-0f9ac6901d16
msc.legacyurl: /visual-studio/overview/2013/visual-studio-2013-web-tools
msc.type: authoredcontent
ms.openlocfilehash: 2fb987dd9b26ad9f0e8a88fd881bde4505ec4148
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622673"
---
# <a name="hands-on-lab-visual-studio-2013-web-tools"></a>Praktické cvičení: Webové nástroje v sadě Visual Studio 2013

podle [týmu webového Campy](https://twitter.com/webcamps)

[Stáhnout web Campy Training Kit](https://aka.ms/webcamps-training-kit)

> Visual Studio je vynikající vývojové prostředí pro. SÍTĚ Windows a webové projekty. Obsahuje výkonný textový editor, který lze snadno použít pro úpravu samostatných souborů bez projektu.
> 
> Visual Studio při úpravách jednotlivých souborů udržuje plně vybavený strom analýzy. To umožňuje, aby aplikace Visual Studio poskytovala neparalelní automatické dokončování a akce založené na dokumentech a prováděly vývojové prostředí mnohem rychleji a lépe příjemný. Tyto funkce jsou zvláště výkonné v dokumentech HTML a CSS.
> 
> Všechna tato napájení jsou taky dostupná pro rozšíření, což usnadňuje rozšíření editorů o výkonné nové funkce, které vyhovují vašim potřebám. Web Essentials je kolekce (převážně) vylepšení pro web, která se týkají sady Visual Studio. Zahrnuje spoustu nových doplňování technologie IntelliSense (zejména pro CSS), nové funkce pro propojení prohlížeče, automatické JSHint pro soubory JavaScriptu, nová upozornění pro HTML a CSS a řadu dalších funkcí, které jsou nezbytné pro moderní vývoj webů.
> 
> Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici na adrese [https://aka.ms/webcamps-training-kit](https://aka.ms/webcamps-training-kit).

<a id="Overview"></a>
## <a name="overview"></a>Přehled

<a id="Objectives"></a>
### <a name="objectives"></a>Cíle

V této praktické laboratorní laboratoři se dozvíte, jak:

- Používejte nové funkce editoru HTML, které jsou součástí webových základních prvků, jako jsou například bohatý fragmenty kódu HTML5 a kódování Zen.
- Používejte nové funkce editoru šablon stylů CSS, které jsou součástí sady Web Essentials, jako je výběr barvy a popis matice v prohlížeči.
- Použití nových funkcí editoru JavaScriptu, které jsou součástí webu Essentials, jako je extrakce souborů a IntelliSense pro všechny elementy HTML
- Výměna dat mezi prohlížečem a Visual Studio pomocí odkazu v prohlížeči

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Předpoklady

Následující postup je nutný k dokončení tohoto praktického laboratorního prostředí:

- [Microsoft Visual Studio Professional 2013](https://www.microsoft.com/visualstudio/) nebo vyšší
- [Web Essentials 2013](http://vswebessentials.com/)
- [Google Chrome](https://www.google.com/chrome/)

<a id="Setup"></a>
### <a name="setup"></a>Nastavení

Aby bylo možné spustit cvičení v této praktické laboratorní laboratoři, budete muset nejprve nastavit prostředí.

1. Otevřete okno Průzkumníka Windows a přejděte do **zdrojové** složky testovacího prostředí.
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

1. [Práce s odkazem na prohlížeč a Web Essentials](#Exercise1)
2. [Využití fragmentů kódu a IntelliSense](#Exercise2)

> [!NOTE]
> Při prvním spuštění sady Visual Studio je nutné vybrat jednu z předdefinovaných kolekcí nastavení. Každá předdefinovaná kolekce je navržena tak, aby odpovídala konkrétnímu stylu vývoje a určuje rozložení oken, chování editoru, fragmenty kódu technologie IntelliSense a možnosti dialogového okna. Postupy v tomto testovacím prostředí popisují akce, které jsou nezbytné k provedení daného úkolu v sadě Visual Studio při použití kolekce **Obecné vývojové nastavení** . Pokud zvolíte pro vývojové prostředí jinou kolekci nastavení, mohou být v krocích, které byste měli vzít v úvahu, rozdíly.

<a id="Exercise1"></a>
### <a name="exercise-1-working-with-browser-link-and-web-essentials"></a>Cvičení 1: práce s odkazem na prohlížeč a Web Essentials

**Web Essentials** je rozšíření sady Visual Studio, které přináší řadu užitečných funkcí pro moderní vývoj webů, hlavně zaměřené na to, aby bylo prostředí vývoje webu mnohem rychlejší a příjemný. Web Essentials můžete nainstalovat z galerie rozšíření v aplikaci Visual Studio.

**Odkaz na prohlížeč** je nová funkce, která je součástí Visual Studio 2013, která poskytuje kanál mezi rozhraním IDE sady Visual Studio a jakýmkoli otevřeným prohlížečem pro výměnu dat mezi webovou aplikací a Visual Studiem. Web Essentials rozšiřuje prohlížeč s nástroji pro manipulaci s modelem objektu DOM a styly CSS vašich webových stránek přímo z prohlížeče.

V tomto cvičení prozkoumáte některé funkce, které podporuje **Web Essentials** a **Browser Link** , k vylepšení jednoduché stránky kvízu.

<a id="Ex1Task1"></a>
#### <a name="task-1---running-the-project-in-multiple-browsers"></a>Úloha 1 – spuštění projektu v několika prohlížečích

V této úloze nakonfigurujete webovou aplikaci tak, aby běžela v několika prohlížečích najednou, což je užitečné pro testování v různých prohlížečích.

1. Otevřete **Microsoft Visual Studio**.
2. V nabídce **soubor** vyberte **otevřít | Projekt nebo řešení...** a přejděte do složky **EX1-WorkingwithBrowserLinkandWebEssentials\Begin** ve **zdrojové** složce testovacího prostředí (C:\WebCampsTK\HOL\VSWebTooling\Source). Vyberte možnost **Begin. sln** a klikněte na tlačítko **otevřít**.
3. Na panelu nástrojů sady Visual Studio rozbalte nabídku prohlížeč a vyberte **Procházet pomocí...** .

    ![Možnost Procházet s možností nabídky](visual-studio-2013-web-tools/_static/image1.png "Procházet pomocí... v nabídce prohlížeče")

    *Možnost Procházet s možností nabídky*
4. V dialogovém okně **Procházet se systémem** vyberte **Google Chrome** a **Internet Explorer** tak, že podržíte klávesu **CTRL** a kliknete na **nastavit jako výchozí**.

    ![Procházet s – dialogové okno](visual-studio-2013-web-tools/_static/image2.png "Procházet s – dialogové okno")

    *Výběr několika výchozích prohlížečů*
5. Jako výchozí prohlížeč by se teď měly zobrazovat Google Chrome a Internet Explorer. Kliknutím na tlačítko **Storno** zavřete dialogové okno.

    ![Google Chrome a Internet Explorer jako výchozí prohlížeče](visual-studio-2013-web-tools/_static/image3.png "Výchozí prohlížeče Google Chrome a Internet Exploreru")

    *Google Chrome a Internet Explorer jako výchozí prohlížeče*

    > [!NOTE]
    > Po konfiguraci výchozích prohlížečů se v nabídce prohlížeče vybere možnost **více prohlížečů** .
    > 
    > ![Více prohlížečů](visual-studio-2013-web-tools/_static/image4.png "Více prohlížečů")
6. Stisknutím **kombinace kláves CTRL** + **F5** spusťte aplikaci bez ladění.
7. Pokud jsou okna prohlížeče otevřená, umístěte jeden z nich nad druhý, aby se aktualizace zobrazily současně na obou prohlížečích. V prohlížečích by se měla zobrazit webová stránka s světle modrým obdélníkem.

    ![Umístění jednoho prohlížeče nad druhý](visual-studio-2013-web-tools/_static/image5.png "Umístění jednoho prohlížeče nad druhý")

    *Umístění jednoho prohlížeče nad druhý*
8. Nezavírejte prohlížeče. Budete je používat v dalším úkolu.

<a id="Ex1Task2"></a>
#### <a name="task-2---using-zen-coding-to-create-html-elements"></a>Úkol 2 – použití kódování Zen k vytváření elementů jazyka HTML

**Zen** Code je modul plug-in editoru pro vysokorychlostní HTML, XML, XSL (nebo jakýkoli jiný formát strukturovaného kódu), který můžete kódovat a upravovat. Jádrem tohoto modulu plug-in je výkonný modul zkratky, který umožňuje rozšířit výrazy podobné selektorům CSS v kódu HTML. Kódování Zen je rychlý způsob, jak psát kód HTML pomocí syntaxe selektoru stylu CSS.

V tomto cvičení použijete funkci kódování Zen poskytovanou nástrojem Web Essentials k vygenerování tlačítek HTML, která reprezentují možnosti otázky.

1. Přepněte zpět do sady Visual Studio.
2. Otevřete soubor **index. cshtml** umístěný v **zobrazeních** | **domovské** složce.
3. Nahrazení **&lt;!--TODO: sem přidejte možnosti--&gt;** komentář s následujícím kódem a stiskněte klávesu **TAB**.

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample1.css)]
4. Kód by měl být rozšířen na HTML.

    ![Rozšířené HTML](visual-studio-2013-web-tools/_static/image6.png "Rozšířené HTML")

    *Rozšířené HTML*

    > [!NOTE]
    > Další informace o syntaxi kódování Zen najdete v následujícím [článku](http://www.johnpapa.net/zen-coding-in-visual-studio-2012/).
5. Kliknutím na tlačítko **Aktualizovat propojené prohlížeče** aktualizujte oba prohlížeče.

    ![Aktualizovat propojené prohlížeče](visual-studio-2013-web-tools/_static/image7.png "Aktualizovat propojené prohlížeče")

    *Aktualizovat propojené prohlížeče*

    ![Internet Explorer – stránka se aktualizovala pomocí čtyř tlačítek](visual-studio-2013-web-tools/_static/image8.png "Internet Explorer – stránka se aktualizovala pomocí čtyř tlačítek")

    *Internet Explorer – stránka se aktualizovala pomocí čtyř tlačítek*

    ![Google Chrome – stránka se aktualizovala se čtyřmi tlačítky](visual-studio-2013-web-tools/_static/image9.png "Google Chrome – stránka se aktualizovala se čtyřmi tlačítky")

    *Google Chrome – stránka se aktualizovala se čtyřmi tlačítky*
6. Přepněte zpět do sady Visual Studio.
7. Přidali jste tlačítka na stránku, ale stále potřebujete přidat otázku šablony. K tomu budete používat novou funkci ve Web Essentials s názvem **Lorem Ipsum Generator**. Vyhledejte element **div** s atributem **třídy** **front**.
8. Přidejte následující kód jako první podřízený prvek **div**a stiskněte klávesu **TAB**.

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample2.css)]
9. Kód by měl být rozšířen na HTML.

    ![Lorem Ipsum automaticky generovaný](visual-studio-2013-web-tools/_static/image10.png "Lorem Ipsum autogenerated")

    *Lorem Ipsum automaticky generovaný*

    > [!NOTE]
    > Jako součást kódování Zen nyní můžete vytvořit Lore Ipsum kód přímo v editoru HTML. Stačí napsat typ **Lorem** a stiskněte **kartu** a 30 slov Lorem Ipsum text. Například *lorem10* vloží 10 lorech Ipsum slov.
10. Do horní části otázky přidáte logo pomocí jiné nové funkce ve webové části Web Essentials označované jako **generátor lorech pixelů**. Přidejte následující kód jako první podřízený prvek elementu **div** s **kontejnerem** jako hodnotu **třídy** a stiskněte klávesu **TAB**.

    [!code-css[Main](visual-studio-2013-web-tools/samples/sample3.css)]
11. Kód by měl být rozšířen na HTML.

    ![Automaticky vygenerované v lorech pixelech](visual-studio-2013-web-tools/_static/image11.png "Automaticky vygenerované v lorech pixelech")

    *Automaticky vygenerované v lorech pixelech*

    > [!NOTE]
    > Jako součást kódování Zen můžete také vygenerovat kód Lorech pixelů přímo v editoru HTML. Stačí zadat **pix – 200x200-** animales a stiskněte **kartu** a značku **img** s 200x200 obrázkem zvíře se vloží. Další informace najdete v tématu [lorech pixelů](http://www.lorempixel.com).
12. Kliknutím na tlačítko **Aktualizovat propojené prohlížeče** aktualizujte oba prohlížeče.

    ![Internet Explorer – automaticky vygenerovaný obrázek a text](visual-studio-2013-web-tools/_static/image12.png "Internet Explorer – automaticky vygenerovaný obrázek a text")

    *Internet Explorer – automaticky vygenerovaný obrázek a text*

    ![Google Chrome – automaticky vygenerovaný obrázek a text](visual-studio-2013-web-tools/_static/image13.png "Google Chrome – automaticky vygenerovaný obrázek a text")

    *Google Chrome – automaticky vygenerovaný obrázek a text*

    > [!NOTE]
    > Vzhledem k tomu, že obrázek je vybrán náhodně při přidávání fragmentu kódu, obrázek zobrazený v prohlížečích se může lišit.
13. Nezavírejte prohlížeče. Budete je používat v dalším úkolu.

<a id="Ex1Task3"></a>
#### <a name="task-3---updating-a-style-property"></a>Úloha 3 – aktualizace vlastnosti Style

V této úloze použijete funkci **kontrolního režimu** odkazu v prohlížeči ke zjištění přesného umístění, kde je vygenerován konkrétní element modelu DOM, a poté aktualizujete vlastnost Color daného elementu pomocí výběru barvy, který poskytuje sada Web Essentials.

1. V prohlížeči Internet Explorer stiskněte **CTRL** + **ALT** + **I** , aby se povolil režim kontroly.
2. Přesuňte ukazatel myši na světle modrý okraj a klikněte na.

    ![Přesunutí ukazatele na světle modrý okraj](visual-studio-2013-web-tools/_static/image14.png "Přesunutí ukazatele na světle modrý okraj")

    *Přesunutí ukazatele na světle modrý okraj*
3. Přepněte zpět do sady Visual Studio. Všimněte si, jak je prvek jazyka HTML, který jste vybrali v prohlížeči, vybrán také v editoru HTML sady Visual Studio.

    ![HTML element vybraný v editoru HTML sady Visual Studio](visual-studio-2013-web-tools/_static/image15.png "HTML element vybraný v editoru HTML sady Visual Studio")

    *HTML element vybraný v editoru HTML sady Visual Studio*
4. Nyní aktualizujete **přední** třídu CSS, aby bylo možné změnit styl vybraného elementu. Provedete **to tak,** že stisknutím **kombinace kláves CTRL** + otevřete vyhledávací pole **Navigovat** . Zadejte **site. CSS** a stisknutím klávesy **ENTER** soubor otevřete.

    ![Otevírá se soubor Web. CSS.](visual-studio-2013-web-tools/_static/image16.png "Otevírá se soubor Web. CSS.")

    *Otevírá se soubor Web. CSS.*
5. Stisknutím **kombinace kláves CTRL** + **F** a zadáním **. Flip-Container. zepředu** Najděte Selektor šablon stylů CSS.
6. Kliknutím na světle modrý čtverec ve vlastnosti Border třídy otevřete výběr barvy.

    ![Otevření výběru barvy](visual-studio-2013-web-tools/_static/image17.png "Otevření výběru barvy")

    *Otevření výběru barvy*
7. Rozbalte výběr barvy kliknutím na tlačítko s dvojitou šipkou a výběrem nové barvy.

    ![Rozbalení výběru barvy](visual-studio-2013-web-tools/_static/image18.png "Rozbalení výběru barvy")

    *Rozbalení výběru barvy*
8. Stisknutím **kombinace kláves CTRL** + **ALT** + **ENTER** aktualizujte propojené prohlížeče.
9. Přepněte do aplikace Internet Explorer a Všimněte si, jak se změnila barva ohraničení.

    ![Internet Explorer – aktualizace barvy ohraničení](visual-studio-2013-web-tools/_static/image19.png "Internet Explorer – aktualizace barvy ohraničení")

    *Internet Explorer – aktualizace barvy ohraničení*
10. Přepněte na Google Chrome a Všimněte si, jak se změnila barva ohraničení.

    ![Google Chrome – aktualizace barvy ohraničení](visual-studio-2013-web-tools/_static/image20.png "Google Chrome – aktualizace barvy ohraničení")

    *Google Chrome – aktualizace barvy ohraničení*
11. Přepněte zpět do sady Visual Studio.
12. Přejděte na konec souboru **Web. CSS** a stisknutím klávesy **CTRL** + **F** Najděte selektor **. btn** .
13. Všimněte si, že vlastnost **-WebKit-Border-RADIUS** je podtržená zeleně.

    ![-WebKit-Border-vlastnost poloměru pro selektor BTN](visual-studio-2013-web-tools/_static/image21.png "-WebKit-Border-vlastnost poloměru pro selektor BTN")

    *-WebKit-Border-vlastnost poloměru pro selektor BTN*
14. Umístěte blikající kurzor do vlastnosti **-WebKit-Border-RADIUS** . Pod prvním písmenem prvního slova v této vlastnosti by se měla zobrazit modrá čára. Toto je **inteligentní značka**.
15. Stiskněte klávesu **CTRL** +  **.** Chcete-li otevřít nabídku návrhy a klikněte na tlačítko **Přidat chybějící standardní vlastnost (Border-RADIUS)** .

    ![Přidat chybějící návrh standardní vlastnosti](visual-studio-2013-web-tools/_static/image22.png "Přidat chybějící návrh standardní vlastnosti")

    *Přidat chybějící návrh standardní vlastnosti*
16. Vlastnost **border-RADIUS** je automaticky přidána do pravidla šablony stylů CSS.

    ![Nebyla přidána standardní vlastnost.](visual-studio-2013-web-tools/_static/image23.png "Nebyla přidána standardní vlastnost.")

    *Nebyla přidána standardní vlastnost.*
17. Přesuňte ukazatel na vlastnost **border-RADIUS** , abyste zobrazili **Popis matice v prohlížeči**. **Popisek matice prohlížeče** zobrazuje dostupnost vlastnosti v jednotlivých prohlížečích.

    ![Popis matice v prohlížeči](visual-studio-2013-web-tools/_static/image24.png "Popis matice v prohlížeči")

    *Popis matice v prohlížeči*
18. Všimněte si, že hodnota vlastnosti **border-RADIUS** je pořád podtržená. Přesunutím ukazatele nad hodnotu zobrazíte zprávu s upozorněním.

    ![Border – upozornění na hodnotu vlastnosti protokolu RADIUS](visual-studio-2013-web-tools/_static/image25.png "Border – upozornění na hodnotu vlastnosti protokolu RADIUS")

    *Border – upozornění na hodnotu vlastnosti protokolu RADIUS*
19. Odeberte jednotku hodnoty vlastnosti **border-RADIUS** navrhovanou popisem tlačítka.
20. Jako **border – poloměr** je standardní vlastnost pro definování, jak jsou zaoblené rohy ohraničení, a vlastnost **-WebKit-Border-RADIUS** můžete z pravidla CSS odebrat.
21. Umístěte blikající kurzor do vlastnosti **zalamování řádků** a Všimněte si, že inteligentní značka se zobrazí také níže.
22. Otevřete nabídku a klikněte na možnost **Přidat chybějící konkrétní dodavatele**.

    ![Přidat návrh chybějících konkrétních dodavatelů](visual-studio-2013-web-tools/_static/image26.png "Přidat návrh chybějících konkrétních dodavatelů")

    *Přidat návrh chybějících konkrétních dodavatelů*
23. Vlastnost **-MS-Word-Wrap** je automaticky přidána do pravidla šablony stylů CSS.

    ![Přidána vlastnost specifická pro dodavatele](visual-studio-2013-web-tools/_static/image27.png "Přidána vlastnost specifická pro dodavatele")

    *Přidána vlastnost specifická pro dodavatele*

<a id="Ex1Task4"></a>
#### <a name="task-4---updating-the-html-code-from-the-browser"></a>Úloha 4 – aktualizace kódu HTML z prohlížeče

V této úloze použijete funkci **návrhového režimu** odkazu prohlížeče pro úpravu objektu DOM z prohlížeče a přenos změn do zdrojového souboru HTML v aplikaci Visual Studio.

1. V Google Chrome stiskněte **CTRL** + **ALT** + **D** pro povolení režimu návrhu.
2. Přesuňte ukazatel myši na štítek **Lorem Ipsum dolor Sit Amet** a klikněte na.

    ![Úprava otázky](visual-studio-2013-web-tools/_static/image28.png "Úprava otázky")

    *Úprava otázky*
3. Měl by se zobrazit kurzor. Nahraďte původní text tak, jak vypadá, *když napíšem delší otázku?* , a potom stisknutím klávesy **ESC** Ukončete režim návrhu.

    ![Upravený dotaz](visual-studio-2013-web-tools/_static/image29.png "Upravený dotaz")

    *Upravený dotaz*
4. Přepněte zpátky do sady Visual Studio a otevřete **index. cshtml**, pokud ještě není otevřený. Všimněte si, že vnitřní text prvku **&lt;p&gt;** byl aktualizován.

    ![Aktualizace otázky na stránce HTML](visual-studio-2013-web-tools/_static/image30.png "Aktualizace otázky na stránce HTML")

    *Aktualizace otázky na stránce HTML*

<a id="Ex1Task5"></a>
#### <a name="task-5---reviewing-seo-related-warnings"></a>Úloha 5-Kontrola upozornění spojených s SEO

**Optimalizace** vyhledávače (SEO) je proces, který je v seznamu výsledků vyhledávacího webu vyšší. Čím vyšší je pořadí lokality a čím více je v seznamu uvedeno, tím více návštěvníkům získá web z tohoto vyhledávacího stroje. Web Essentials zahrnuje analytický nástroj, který prověřuje kód HTML, oznamuje zjištěné problémy a poskytuje pomoc při jejich opravě.

1. Přejděte do nabídky **zobrazení** a kliknutím na **Seznam chyb** otevřete okno **Seznam chyb** .

    ![Seznam chyb v nabídce zobrazení](visual-studio-2013-web-tools/_static/image31.png "Seznam chyb v nabídce zobrazení")

    *Seznam chyb v nabídce zobrazení*
2. Všimněte si, že došlo k upozornění na stránku SEO upozorňující na to, že chybí **&lt;Značka meta&gt;** pro popis stránky. Dvakrát klikněte na položku upozornění SEO, abyste ji opravili.

    ![Seznam chyb okno](visual-studio-2013-web-tools/_static/image32.png "okno Seznam chyb")

    *Seznam chyb okno*
3. Kliknutím na tlačítko **Ano** v dialogovém okně **Web Essentials** vložíte popis &lt;meta&gt; tag.

    ![Dialogové okno Web Essentials](visual-studio-2013-web-tools/_static/image33.png "Dialogové okno Web Essentials")

    *Dialogové okno Web Essentials*
4. Editor pro **\_layout. cshtml** se otevře a **&lt;Značka meta&gt;** je automaticky přidána do části **head** v souboru HTML.

    ![Meta značka automaticky přidána na _Layout stránce](visual-studio-2013-web-tools/_static/image34.png "Meta značka automaticky přidána na _Layout stránce")

    *Meta značka se automaticky přidala do \_rozložení stránky.*
5. Změňte hodnotu atributu **Content** na *GeekQuiz* a uložte soubor.

<a id="Exercise2"></a>
### <a name="exercise-2-taking-advantage-of-code-snippets-and-intellisense"></a>Cvičení 2: využití fragmentů kódu a IntelliSense

V případě aplikace Web Essentials byl Editor HTML rozšířen o další funkce. V tomto cvičení se zobrazí některé nové funkce, které jsou užitečné při vývoji webových aplikací.

<a id="Ex2Task1"></a>
#### <a name="task-1---using-intellisense-in-html-documents"></a>Úloha 1 – použití IntelliSense v dokumentech HTML

První nová funkce, kterou se zobrazí v této úloze, se nazývá **Dynamická technologie IntelliSense**. Dynamická technologie IntelliSense čte jiné značky a atributy pro odvození možných ID, která budete používat.

V této úloze vytvoříte nový prvek formuláře HTML, který obsahuje popisek a vstupní pole. Pak přidáte atribut **pro** k popisku, který ho sváže se vstupem, a uvidíte návrhy IntelliSense na základě ID vstupů v oboru.

1. Otevřete **Visual Studio Express 2013 pro web** a řešení **Begin. sln** nacházející se ve složce **source/EX2-TakingAdvantageofCodeSnippetsandIntelliSense/Begin** . Případně můžete pokračovat v řešení, které jste získali v předchozím cvičení.
2. V **Průzkumník řešení**otevřete soubor **index. cshtml** umístěný v **zobrazeních** | **domovské** složce.
3. Do **oddílu&lt;&gt;** elementu přidejte následující formulář.

    (Fragment kódu – *VisualStudio2013WebTooling* - *EX2* - *formulář*)

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample4.html)]
4. Vstupní značka by měla předcházet návěští s nějakým popisem pole. Přidejte následující popisek před vstupní značku.

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample5.html)]
5. Atribut **for** **&lt;Label&gt;** určuje, na který prvek formuláře je popisek svázán. Hodnota atributu musí být rovna ID souvisejícího prvku. Přidejte atribut **pro** **&lt;popisku&gt;** elementu. Jak je znázorněno na následujícím obrázku, &quot;název&quot; hodnota se zobrazí v poli IntelliSense na základě ID prvků v rámci stejného oboru (ohraničující **&lt;formuláře&gt;** ).

    ![Zobrazení ID v IntelliSense](visual-studio-2013-web-tools/_static/image35.png "Zobrazení ID v IntelliSense")

    *Zobrazení ID v IntelliSense*
6. Odstraní naposledy přidaný **&lt;&gt;** element a jeho obsah.

<a id="Ex2Task2"></a>
#### <a name="task-2---using-html-code-snippets"></a>Úloha 2 – používání fragmentů kódu HTML

HTML5 zavedlo více než 25 nových sémantických značek. Visual Studio již pro tyto značky podporuje technologii IntelliSense, ale Visual Studio 2013 rychlejší a snadnější psaní značek přidáním nových fragmentů kódu. I když tyto značky nejsou komplikované, jsou dodávány s několika malými odlišností, jako je například přidání správných záložních kodeků pro *zvukovou* značku. V této úloze se zobrazí fragmenty kódu HTML pro značku zvuku.

1. Do souboru **index. cshtml** zadejte **&lt;AUD** dovnitř **&lt;oddílu&gt;** elementu, jak je znázorněno na následujícím obrázku.

    ![Vložení prvku zvuk](visual-studio-2013-web-tools/_static/image36.png "Vložení prvku zvuk")

    *Vložení prvku zvuk*
2. Stiskněte **tabulátor** dvakrát a Všimněte si, jak se na stránce přidá následující kód a kurzor se umístí do atributu **Src** prvního zdroje.

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample6.html)]

    > [!NOTE]
    > Po kliknutí na klávesu **TAB** dvakrát dojde k vložení fragmentu kódu. Fragment zvuku zobrazuje standardní použití *zvukové* značky se dvěma zdrojovými soubory pro lepší podporu.
3. Odstraňte druhý řádek a aktualizujte zdroj prvního řádku následujícím odkazem na WebCampsTV Katana show: [http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3](http://media.ch9.ms/ch9/11d8/604b8163-fad3-4f12-9607-b404201211d8/KatanaProject.mp3). Výsledný kód je uveden níže.

    [!code-html[Main](visual-studio-2013-web-tools/samples/sample7.html)]

    > [!NOTE]
    > Zdrojový soubor *KatanaProject. mp3* se používá jako příklad. Pokud budete chtít, můžete použít jiný zdroj.
4. Soubor uložte stisknutím **kombinace kláves CTRL** + **S** .
5. Stisknutím **kombinace kláves CTRL** + **F5** spusťte aplikaci.
6. Všimněte si, že se do aplikace přidal zvukový přehrávač.

    ![Zvukový přehrávač v aplikaci Internet Explorer](visual-studio-2013-web-tools/_static/image37.png "Zvukový přehrávač v aplikaci Internet Explorer")

    *Zvukový přehrávač v aplikaci Internet Explorer*

    ![Audio Player v Google Chrome](visual-studio-2013-web-tools/_static/image38.png "Audio Player v Google Chrome")

    *Audio Player v Google Chrome*
7. Nezavírejte prohlížeče. Budete je používat v dalším úkolu.

<a id="Ex2Task3"></a>
#### <a name="task-3---using-intellisense-in-javascript-documents"></a>Úloha 3 – použití IntelliSense v dokumentech JavaScript

S Web Essentials 2013, šablony stylů a stránky HTML vytvoří seznam identifikátorů a názvů tříd. V této úloze se dozvíte, jak tyto seznamy zlepšují podporu technologie IntelliSense v jazyce JavaScript v Web Essentials 2013.

1. V souboru **index. cshtml** přidejte následující kód pro definování značky **skriptu** pro kód jazyka JavaScript.

    [!code-cshtml[Main](visual-studio-2013-web-tools/samples/sample8.cshtml)]
2. Přidejte následující kód do značky **Script** pro definování funkce zpětného volání připravenosti.

    (Fragment kódu – *VisualStudio2013WebTooling* - *EX2* - *ReadyFunction*)

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample9.js)]
3. Umístěte blikající kurzor do značky **Script** a stiskněte klávesu **CTRL** +  **.** pro otevření nabídky návrh.
4. Klikněte na **extrahovat do souboru**.

    ![Extrakce JavaScriptu do souboru návrhu](visual-studio-2013-web-tools/_static/image39.png "Extrakce JavaScriptu do souboru návrhu")

    *Extrakce JavaScriptu do souboru návrhu*
5. V okně **Uložit jako** vyberte složku **skripty** , pojmenujte soubor **init. js** a klikněte na **Uložit**.

    ![Uložit jako okno](visual-studio-2013-web-tools/_static/image40.png "Uložit jako okno")

    *Uložit jako okno*

    > [!NOTE]
    > Vytvoří se soubor **init. js** a obsah skriptu se přesune do souboru.
    > 
    > ![Soubor init. js vytvořený pomocí zahrnutého obsahu](visual-studio-2013-web-tools/_static/image41.png "Soubor init. js vytvořený pomocí zahrnutého obsahu")
    > 
    > *Soubor init. js vytvořený pomocí zahrnutého obsahu*
6. Otevřete soubor **index. cshtml** a ověřte, zda byla značka skriptu nahrazena odkazem na soubor **init. js** .

    ![Reference k souboru init. js HTML](visual-studio-2013-web-tools/_static/image42.png "Reference k souboru init. js HTML")

    *Reference k souboru init. js HTML*
7. Přejít na **Průzkumník řešení** a Všimněte si, že soubor **init. js** byl automaticky zahrnut do řešení.

    ![Soubor init. js zahrnutý v řešení](visual-studio-2013-web-tools/_static/image43.png "Soubor init. js zahrnutý v řešení")

    *Soubor init. js zahrnutý v řešení*
8. Přepněte zpět do souboru **init. js** a aktualizujte tak **připravené** zpětné volání funkce.
9. Uvnitř definice zpětného volání funkce, která je předána *připravenému*, přidejte následující kód, který získá všechny prvky pomocí konkrétního atributu Class.

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample10.js)]
10. Stiskněte klávesu **CTRL** + **mezeru** mezi uvozovky uvnitř volání funkce **getElementsByClassName** .

    ![Zobrazení technologie IntelliSense pro funkci getElementsByClassName](visual-studio-2013-web-tools/_static/image44.png "Zobrazení technologie IntelliSense pro funkci getElementsByClassName")

    *Zobrazení technologie IntelliSense pro funkci getElementsByClassName*

    > [!NOTE]
    > Všimněte si, že technologie IntelliSense zobrazuje třídy definované v šablonách stylů projektu.
11. Nahraďte řádek, který jste vytvořili, pomocí následujícího kódu.

    [!code-javascript[Main](visual-studio-2013-web-tools/samples/sample11.js)]
12. Umístěte kurzor po **au** do uvozovek ve funkci **GetElementsByTagName** a stiskněte klávesy **CTRL** + **MEZERNÍK**.

    ![Zobrazení IntelliSense pro metodu getElementByTagName](visual-studio-2013-web-tools/_static/image45.png "Zobrazení IntelliSense pro metodu getElementByTagName")

    *Zobrazení IntelliSense pro metodu getElementsByTagName*
13. Ze seznamu vyberte **&quot;audio&quot;** a stiskněte klávesu **ENTER**. Výsledek je znázorněn na následujícím obrázku.

    ![Načítání elementů zvuku](visual-studio-2013-web-tools/_static/image46.png "Načítání elementů zvuku")

    *Načítání elementů zvuku*
14. V **Průzkumník řešení**klikněte pravým tlačítkem myši na soubor **init. js** ve složce **Scripts** a v nabídce **Web Essentials** vyberte **minimalizuje soubory JavaScriptu** .

    ![Soubory JavaScriptu minimalizuje](visual-studio-2013-web-tools/_static/image47.png "Soubory JavaScriptu minimalizuje")

    *Soubory JavaScriptu minimalizuje*
15. Po zobrazení výzvy k povolení automatického minifikace, když se změní zdrojový soubor, klikněte na **Ano**.

    ![Povolení automatického upozornění minifikace](visual-studio-2013-web-tools/_static/image48.png "Povolení automatického upozornění minifikace")

    *Povolení automatického upozornění minifikace*

    > [!NOTE]
    > Je vytvořen soubor **init. min. js** a je přidán jako závislost souboru **init. js** .
    > 
    > ![Byl vytvořen soubor init. min. js.](visual-studio-2013-web-tools/_static/image49.png "Byl vytvořen soubor init. min. js.")
    > 
    > *Byl vytvořen soubor init. min. js.*
16. Otevřete soubor **init. min. js** a Všimněte si, že soubor je minifikovaného.

    ![Obsah souboru init. min. js](visual-studio-2013-web-tools/_static/image50.png "Obsah souboru init. min. js")

    *Obsah souboru init. min. js*
17. V souboru **init. js** přidejte následující kód pod voláním funkce **GetElementsByTagName** , aby se hrály všechny zvukové prvky.

    (Fragment kódu – *VisualStudio2013WebTooling* - *EX2* - *PlayAudioElements*)

    [!code-csharp[Main](visual-studio-2013-web-tools/samples/sample12.cs)]
18. Uložte soubor kliknutím na tlačítko **CTRL** + **S** . Vzhledem k tomu, že soubor minifikovaného je již otevřen, zobrazí se dialogové okno s informacemi o tom, že soubor byl změněn mimo editor zdrojového kódu. Klikněte na **Ano**.

    ![Upozornění Microsoft Visual Studio](visual-studio-2013-web-tools/_static/image51.png "Upozornění Microsoft Visual Studio")

    *Upozornění Microsoft Visual Studio*
19. Přepněte zpět do souboru **init. min. js** a ověřte, zda byl soubor aktualizován pomocí nového kódu.

    ![Soubor init. min. js se aktualizoval.](visual-studio-2013-web-tools/_static/image52.png "Soubor init. min. js se aktualizoval.")

    *Soubor init. min. js se aktualizoval.*
20. Klikněte na tlačítko **aktualizovat propojení prohlížeče** .
21. Po obnovení obou prohlížečů se zvukové přehrávače, které jste viděli v předchozí úloze, začnou automaticky přehrávat.

    ![Zvukový přehrávač zahrnutý v zobrazení](visual-studio-2013-web-tools/_static/image53.png "Zvukový přehrávač zahrnutý v zobrazení")

    *Zvukový přehrávač zahrnutý v zobrazení*

---

<a id="Summary"></a>
## <a name="summary"></a>Souhrn

Vyplněním tohoto praktického cvičení jste se dozvěděli, jak:

- Používejte nové funkce editoru HTML, které jsou součástí webových základních prvků, jako jsou například bohatý fragmenty kódu HTML5 a kódování Zen.
- Používejte nové funkce editoru šablon stylů CSS, které jsou součástí sady Web Essentials, jako je výběr barvy a popis matice v prohlížeči.
- Použití nových funkcí editoru JavaScriptu, které jsou součástí webu Essentials, jako je extrakce souborů a IntelliSense pro všechny elementy HTML
- Výměna dat mezi prohlížečem a Visual Studio pomocí odkazu v prohlížeči

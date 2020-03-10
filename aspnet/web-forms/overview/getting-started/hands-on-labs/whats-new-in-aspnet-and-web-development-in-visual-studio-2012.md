---
uid: web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
title: Co je nového v ASP.NET a vývoji pro web v aplikaci Visual Studio 2012 | Microsoft Docs
author: rick-anderson
description: Nová verze sady Visual Studio zavádí řadu vylepšení, která se zaměřují na zlepšení prostředí a výkonu při práci s webovými technologiemi....
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 6d40d276-1642-4a77-b6c9-02ac914f6805
msc.legacyurl: /web-forms/overview/getting-started/hands-on-labs/whats-new-in-aspnet-and-web-development-in-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 80c77ec65ed86b06e417d3f6ba608e404c46768b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525933"
---
# <a name="whats-new-in-aspnet-and-web-development-in-visual-studio-2012"></a>Novinky ASP.NET a webového vývoje v sadě Visual Studio 2012

podle [týmu webového Campy](https://twitter.com/webcamps)

> Nová verze sady Visual Studio zavádí řadu vylepšení, která se zaměřují na zlepšení prostředí a výkonu při práci s webovými technologiemi. Editory sady Visual Studio pro šablony stylů CSS, JavaScript a HTML byly zcela přepracované tak, aby obsahovaly mnoho dalších pomůcek v kódu na vyžádání, jako je IntelliSense a automatické odsazení. S ohledem na výkon, sdružování a minifikace jsou teď integrované jako integrované funkce, které zjednodušují dobu načítání stránek.
> 
> Visual Studio vám umožní pracovat s nejnovějšími technologiemi webů. Pomocí CSS3 fragmentů kódu pro různé prohlížeče se můžete ujistit, že váš web funguje bez ohledu na klientskou platformu a zároveň využívá nové prvky a funkce HTML5.
> 
> Psaní a profilace kódu v jazyce JavaScript by měla být snazší s touto verzí sady Visual Studio. Seznamy IntelliSense, integrovaná dokumentace XML a navigační funkce jsou nyní k dispozici pro kód jazyka JavaScript. Teď máte katalog JavaScriptu na dosah ruky. Kromě toho můžete kontrolovat ECMAScript5 dodržování předpisů pomocí skriptů a zjišťovat chyby syntaxe v rané fázi.
> 
> Takže tato verze sady Visual Studio implementuje předdefinované sdružování a minifikace. Soubory skriptu a šablony stylů budou zabaleny a komprimovány, aby lokalita rychleji prováděla.
> 
> Toto testovací prostředí vás provede vylepšeními a novými funkcemi, které jsme dříve popsali pomocí menších změn ve vzorové webové aplikaci, která je součástí zdrojové složky.
> 
> Veškerý ukázkový kód a fragmenty kódu jsou součástí sady web Campy Traination Kit, která je k dispozici na adrese [https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409](https://go.microsoft.com/fwlink/?LinkID=248297&clcid=0x409).

<a id="Objectives"></a>

<a id="Objectives"></a>
### <a name="objectives"></a>Cíle

V tomto cvičení se naučíte:

- Použití nových funkcí a vylepšení v editoru šablon stylů CSS
- Použití nových funkcí a vylepšení v editoru HTML
- Použití nových funkcí a vylepšení v editoru JavaScriptu
- Konfigurace a použití sdružování a minifikace

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a>Předpoklady

- [Microsoft Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) nebo nadřazený seznam (pokyny k instalaci najdete v [příloze a](#AppendixA) ).
- [Windows PowerShell](https://support.microsoft.com/kb/968930/) (pro instalační skripty – už nainstalované v systémech Windows 8 a windows Server 2008 R2)
- [Internet Explorer 10](https://windows.microsoft.com/internet-explorer/products/ie/home) nebo prohlížeč kompatibilní s HTML5

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a>Cvičení

Tato cvičení v testovacím prostředí zahrnuje následující cvičení:

1. [Cvičení 1: co je nového v editoru šablon stylů CSS](#Exercise1)
2. [Cvičení 2: co je nového v editoru HTML](#Exercise2)
3. [Cvičení 3: co je nového v editoru JavaScriptu](#Exercise3)
4. [Cvičení 4: sdružování a minifikace](#Exercise4)

Odhadovaný čas dokončení tohoto testovacího prostředí: **60 minut**.

<a id="Exercise1"></a>

<a id="Exercise_1_Whats_New_in_the_CSS_Editor"></a>
### <a name="exercise-1-whats-new-in-the-css-editor"></a>Cvičení 1: co je nového v editoru šablon stylů CSS

Vývojáři webu by měli znát mnoho potíží souvisejících s úpravou šablon stylů CSS. Jedním z největších problémů stylu CSS je kompatibilita mezi prohlížečem. K tomu často dochází, když po použití stylů na webu zjistíte, že vypadá jinak, když ho otevřete v jiném prohlížeči nebo zařízení. Proto může dojít k výraznému odstranění těchto vizuálních problémů, aby se zajistilo, že když nakonec budete pracovat v jednom prohlížeči, bude se v ostatních prohlížečích porušen.

Visual Studio teď obsahuje funkce, které vývojářům umožňují efektivně přistupovat k šablonám stylů CSS, pracovat a uspořádávat je. V rámci tohoto cvičení budete splňovat nové funkce pro efektivní organizaci a edici a také fragmenty kódu CSS3 pro zajištění kompatibility mezi prohlížečem.

<a id="Ex1Task1"></a>

<a id="Task_1_-_New_Editor_Features"></a>
#### <a name="task-1---new-editor-features"></a>Úloha 1 – nové funkce editoru

V této úloze zjistíte nové funkce editoru šablon stylů CSS. Tento nový Editor vám pomůže zvýšit produktivitu tím, že využívá nové inteligentní odsazení, vylepšené komentáře ke kódu a vylepšený seznam IntelliSense.

1. Spusťte **Visual Studio** a otevřete řešení **WhatsNewASPNET. sln** nacházející se ve složce **Source\WhatsNewASPNET** tohoto testovacího prostředí.
2. V Průzkumník řešení otevřete soubor **Web. CSS** umístěný ve složce **Styles** . Ujistěte se, že jsou nástroje **textový editor** na panelu nástrojů viditelné. Provedete to tak, že vyberete možnost nabídky **zobrazit** | **panely nástrojů** a pak zkontrolujete možnosti **textového editoru** . Všimněte si, že od této nové verze se pro Editor šablon stylů CSS také povoluje tlačítko **Komentář** (![tlačítko pro komentář](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image1.png)) a tlačítko zrušit **Komentář** (![odkomentovat tlačítko](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image2.png)).

    ![Povolování nástrojů editoru a šablon stylů CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image3.png "Povolování nástrojů editoru a šablon stylů CSS")

    *Povolování nástrojů editoru a šablon stylů CSS*
3. Posuňte kód a vyberte libovolnou definici třídy CSS. Kliknutím na tlačítko **Komentář** (![komentář-tlačítko](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image4.png)) přidejte poznámky k vybraným řádkům. Pak klikněte na tlačítko zrušit **Komentář** (![odkomentovat tlačítko](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image5.png)), aby se změny projevily.
4. Klikněte na **sbalit** (![sbalit](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image6.png)) a **rozbalte** (![rozbalit](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image7.png)) tlačítka umístěná na levém okraji textu. Všimněte si, že teď můžete skrýt styly, které nepoužíváte, aby se zobrazila čisticí zobrazení.

    ![Sbalení tříd CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image8.png "Sbalení tříd CSS")

    *Sbalení tříd CSS*
5. Ujistěte se, že je zapnutá funkce chytrého odsazení. Vyberte možnost nabídky **nástroje** | **Možnosti** a pak v levém podokně obrazovky vyberte **textový editor** | stránce **formátování** **šablon stylů CSS** | . Ověřte možnost **hierarchického odsazení** .

    ![Povoluje se hierarchické odsazení.](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image9.png "Povoluje se hierarchické odsazení.")

    *Povoluje se hierarchické odsazení.*
6. Vyhledejte definici hlavní třídy (. Main) a připojíte styl k elementům div. Všimněte si, že kód se zarovnává automaticky a pomůže uživatelům najít nadřazené třídy na první pohled.

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample1.css)]

    ![Hierarchické zarovnání v šablonách stylů CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image10.png "Hierarchické zarovnání v šablonách stylů CSS")

    *Hierarchické zarovnání v šablonách stylů CSS*
7. Uvnitř **. Main** – třída div vyhledejte kurzor na konci **ohraničení: 0px;** a stisknutím klávesy **ENTER** zobrazte seznam IntelliSense. Začněte psát **nahoru** a Všimněte si, jak je seznam filtrovaný při psaní. V seznamu se zobrazí prvky, které obsahují **horní** část slova (v předchozích verzích sady Visual Studio, seznam je filtrován podle položek, které *začínají* termínem).

    ![Vylepšení technologie IntelliSense v šablonách stylů CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image11.png "Vylepšení technologie IntelliSense v šablonách stylů CSS")

    *Vylepšení technologie IntelliSense v šablonách stylů CSS*

<a id="Ex1Task2"></a>

<a id="Task_2_-_The_Color_Picker"></a>
#### <a name="task-2---the-color-picker"></a>Úkol 2 – Výběr barvy

V této úloze se zobrazí nový dialog pro výběr barvy CSS, který je integrovaný do sady Visual Studio IntelliSense.

1. V **lokalitě. CSS** vyhledejte definici třídy hlaviček (. Header) a umístěte kurzor vedle atributu **background-color** atribut mezi &quot;:&quot; a &quot;#&quot; znaků na daném řádku kódu **.**

    ![Vyhledání kurzoru](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image12.png "Vyhledání kurzoru")

    *Vyhledání kurzoru*
2. Odstraňte **dvojtečku** (:) a zapište ho znovu, abyste zobrazili výběr barvy. Všimněte si, že první barvy, které vidíte, jsou nejčastějšími barvami webu. Pokud kliknete na bílou barvu, jeho kód barvy HTML (#fff) nahradí aktuální kód barvy v šabloně stylů.

    ![Výběr barvy](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image13.png "Výběr barvy")

    *Výběr barvy*
3. Stisknutím tlačítka **Rozbalit** (![com](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image14.png)) na výběr barvy Zobrazte barevný přechod a potom přetažením ukazatele přechodu vyberte jinou barvu. Potom klikněte na tlačítko **kapátka** a vyberte libovolnou barvu na obrazovce. Všimněte si, že se hodnota barvy pozadí při přesunu kurzoru dynamicky mění.

    ![Barevný přechod pro výběr barvy](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image15.png "Barevný přechod pro výběr barvy")

    *Barevný přechod pro výběr barvy*
4. V posuvníku **neprůhlednosti** přesuňte selektor do středu pruhu, aby se snížila průhlednost. Všimněte si, že hodnota pozadí-barva teď změní měřítko na RGBA.

    ![Průhlednost výběru barvy](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image16.png "Průhlednost výběru barvy")

    *Průhlednost výběru barvy*

    > [!NOTE]
    > Definice barvy RGBA (červená, zelená, modrá, alfa) v CSS3 umožňuje definovat hodnotu neprůhlednosti barvy pro jednu položku. Na rozdíl od **neprůhlednosti –** podobný atribut CSS **-** RGBA barvy jsou také kompatibilní s nejnovějšími prohlížeči.

<a id="Ex1Task3"></a>

<a id="Task_3_-_CSS_Compatible_Code_Snippets"></a>
#### <a name="task-3---css-compatible-code-snippets"></a>Úloha 3 – fragmenty kódu kompatibilní se šablonou stylů CSS

V této úloze se naučíte používat fragmenty CSS3 kompatibilní s více prohlížeči, abyste mohli implementovat některé funkce na vašem webu.

1. V souboru **Web. CSS** Najděte hlavičku třídy CSS pro **záhlaví** (. Header) a umístěte kurzor pod **/\*poloměru ohraničení\*/** zástupný symbol pro přidání nového fragmentu. Stiskněte klávesu **ENTER** , chcete-li zobrazit seznam IntelliSense a zadat **protokol RADIUS** pro filtrování seznamu. Vyberte možnost **border-RADIUS** ze seznamu dvojitým kliknutím a potom stiskněte klávesu **tabulátor** pro vložení fragmentu. Pak zadejte velikost poloměru v pixelech a stiskněte klávesu **ENTER**. Například zadejte **15px**.

    Atributy CSS3 přidané fragmentem kódu vykreslí zaoblené ohraničení v prohlížeči dodržování předpisů HTML5, včetně prohlížečů Mozilla a WebKit.

    ![Použití výstřižku Border-RADIUS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image17.png "Použití výstřižku Border-RADIUS")

    *Použití výstřižku Border-RADIUS*
2. Použijte stejné fragmenty **ohraničení** ve stylu stránky (. Page).

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample2.css)]
3. Stisknutím klávesy **F5** spusťte řešení. Všimněte si, že každá stránka má nyní zaoblené ohraničení.

    ![Zaoblené rohy](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image18.png "Zaoblené rohy")

    *Zaoblené rohy*
4. Zavřete prohlížeč a vraťte se do sady Visual Studio.
5. Otevřete soubor **Custom. CSS** umístěný ve složce **styly** a umístěte kurzor do **div. images ul li img** definice třídy.
6. Stiskněte klávesu ENTER, chcete-li zobrazit seznam IntelliSense, zadejte **pole-Shadow** a stiskněte klávesu **TAB** dvakrát pro vložení výchozího fragmentu stínového kódu do definice třídy. Nastavte stínové hodnoty na **10px 10px 5px #888**. Pak zadejte **border-RADIUS** a vložte fragment kódu. Zadejte **15px** pro nastavení velikosti poloměru a stiskněte klávesu **ENTER**.

    ![Zaoblené rohy se stínem](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image19.png "Zaoblené rohy se stínem")

    *Zaoblené rohy se stínem*

    > [!NOTE]
    > V tuto chvíli se atribut Shadow vloží s odpovídající předponou (MOZ, WebKit, o), aby se podporovaly prohlížeče Mozilla a WebKit (Chrome, Safari, Konkeror).
7. Vytvořit novou třídu **div. images ul li IMG: najeďte myší** pod **div. images ul li img** definice třídy a umístěte kurzor do závorek **.**

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample3.css)]
8. Pro vložení transformačního výstřižku zadejte **transformaci** a stiskněte klávesu **TAB** dvakrát. Pak zadejte **otočit (-15deg)** , chcete-li změnit hodnotu úhlu otočení při přechodu na obrázky.

    CSS

    [!code-css[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample4.css)]
9. Stisknutím klávesy **F5** spusťte řešení a přejděte na stránku CSS3. Všimněte si, že obrázky mají zaoblené rohy a stínování box. Najeďte myší na obrázky a sledujte jejich otočení.

    ![Transformovat fragment kódu pro otočení obrázku](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image20.png "Transformovat fragment kódu pro otočení obrázku")

    *Transformovat fragment kódu pro otočení obrázku*

    > [!NOTE]
    > Pokud používáte Internet Explorer 10 a nevidíte stíny, ujistěte se, že je režim dokumentu nastavený na IE10 standardy. Stisknutím klávesy **F12** otevřete nástroje pro vývojáře v aplikaci Internet Explorer a kliknutím na **režim dokumentu** přejděte na IE10 Standards.

    ![o-cz](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image21.png)

<a id="Exercise2"></a>

<a id="Exercise_2_Whats_New_in_the_HTML_Editor"></a>
### <a name="exercise-2-whats-new-in-the-html-editor"></a>Cvičení 2: co je nového v editoru HTML

Visual Studio má Vylepšený editor HTML. Některá vylepšení zahrnutá v této verzi jsou inteligentní odsazení v dokumentech HTML, fragmentech HTML5, počátečních a koncových značkách HTML a při ověřování HTML. V průběhu tohoto cvičení uvidíte, jak tyto změny zlepšují Fluency při práci na webu značek.

Podobně jako editor CSS byl také vylepšen Editor HTML. Většina těchto vylepšení je malými těmi, které usnadňují život webové vývojáře. Podobně jako u více fragmentů kódu pro HTML5, inteligentní odsazení, porovnání počátečních a koncových značek, pokud jsou úpravy a ověřování cílené na typ dokumentu HTML, jsou některá z těchto vylepšení.

<a id="Ex2Task1"></a>

<a id="Task_1_-_Improved_DOCTYPE_Validation"></a>
#### <a name="task-1---improved-doctype-validation"></a>Úloha 1 – Vylepšené ověřování typu DOCTYPE

Editor HTML nyní má možnost kontrolovat typ DOCTYPE stránky, i když definice může být na stránce předlohy. V závislosti na typu DOCTYPE stránky se Editor HTML ověří se správnou sadou pravidel a vyfiltruje seznam IntelliSense, který bude zohledňovat prvky DOCTYPE.

V této úloze změníte typ DOCTYPE stránky, abyste viděli, jak se odpovídajícím způsobem změní chování editoru HTML.

1. Pokud ještě není otevřený, spusťte sadu **Visual Studio** a otevřete řešení **WhatsNewASPNET. sln** ve složce **Source\WhatsNewASPNET** tohoto testovacího prostředí.
2. Otevřete stránku **Web. Master** .
3. Všimněte si cílového schématu pro panel nástrojů ověření. Způsob, jakým se Editor HTML chová (ověřování, IntelliSense atd.), se správně změní tak, aby odpovídal vybranému typu doctype.

    ![Použít typ DOCTYPE na panelu nástrojů pro úpravy zdrojového kódu HTML](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image22.png "Použít typ DOCTYPE na panelu nástrojů pro úpravy zdrojového kódu HTML")

    *Použít typ DOCTYPE na panelu nástrojů pro úpravy zdrojového kódu HTML*
4. Změňte cílové schéma na HTML 4,01.

    ![Změna typu doctype na panelu nástrojů pro úpravy zdrojového kódu HTML](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image23.png "Změna typu doctype na panelu nástrojů pro úpravy zdrojového kódu HTML")

    *Změna typu doctype na panelu nástrojů pro úpravy zdrojového kódu HTML*
5. Umístěte kurzor pod prvek **body** a začněte psát název elementu HTML5 (například **video**). Všimněte si, že prvek není k dispozici v seznamu technologie IntelliSense.

    ![Prvky HTML5 nejsou uvedené](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image24.png "Prvky HTML5 nejsou uvedené")

    *Prvky HTML5 nejsou uvedené*
6. Vraťte změny do cílového schématu pro panel nástrojů ověření a z rozevíracího seznamu vyhledá typ DOCTYPE: XHTML5.

    ![Použít typ DOCTYPE na panelu nástrojů pro úpravy zdrojového kódu HTML](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image25.png "Použít typ DOCTYPE na panelu nástrojů pro úpravy zdrojového kódu HTML")

    *Obnovit typ DOCTYPE na panelu nástrojů pro úpravy zdrojového kódu HTML*
7. Umístěte kurzor pod prvek **tělo** a začněte psát prvek HTML5 znovu (například jako **video**). Všimněte si, že prvky HTML5 jsou nyní k dispozici v seznamu technologie IntelliSense.

    ![Jsou uvedeny prvky HTML5](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image26.png "Jsou uvedeny prvky HTML5")

    *Jsou uvedeny prvky HTML5*

<a id="Ex2Task2"></a>

<a id="Task_2_-_StartEnd_Tags_Automatic_Update"></a>
#### <a name="task-2---startend-tags-automatic-update"></a>Úloha 2 – Automatické aktualizace značek start/end

Visual Studio teď aktualizuje značky otevírání nebo zavírání HTML prvku, který upravujete, aby se vzájemně shodovaly. Tato nová funkce zvýší vaši produktivitu při úpravě značek HTML.

1. Na stránce **Default. aspx** přidejte element **H3** s názvem (například Visual Studio 2012 Rocks!).

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample5.aspx)]
2. Změňte značku **H3** a zadejte **H2** nebo **H1.**

    Všimněte si, že se koncová značka automaticky aktualizuje. Můžete také změnit koncovou značku, abyste viděli, že se odpovídajícím způsobem aktualizují počáteční značky.

    ![Automatická aktualizace koncových značek](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image27.png "Automatická aktualizace koncových značek")

    *Automatická aktualizace koncových značek*

<a id="Ex2Task3"></a>

<a id="Task_3_-_New_HTML5_Code_Snippets"></a>
#### <a name="task-3---new-html5-code-snippets"></a>Úloha 3 – nové fragmenty kódu HTML5

Visual Studio teď obsahuje několik fragmentů kódu HTML5. V tomto úkolu použijete některé z těchto fragmentů kódu.

1. Přidejte novou složku s názvem **zvuk** do kořenového adresáře složky webu. Otevřete Průzkumníka Windows a zkopírujte libovolný zvukový soubor do **zvukové** složky řešení **WhatsNewASPNET. sln** .
2. Na stránce **Default. aspx** Najděte kurzor v části Web11 Rocks. Hlaviček. Zadejte **zvuk** a stiskněte klávesu Tabulátor.

    Nový editor HTML obsahuje fragmenty kódu pro obsah HTML5. Nezapomeňte použít správnou definici DOCTYPE a povolit fragmenty HTML5.

    ![Vkládání fragmentů kódu HTML5](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image28.png "Vkládání fragmentů kódu HTML5")

    *Vkládání fragmentů kódu HTML5*
3. Aktualizujte zdroj zvuku tak, aby odkazoval na existující zvukový soubor.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample6.aspx)]

    > [!NOTE]
    > Do řešení budete muset přidat zvukový soubor.
4. Stiskněte klávesu **F5** ke spuštění lokality a přehrání zvuku.

    ![Spuštění ovládacího prvku zvuk](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image29.png "Spuštění ovládacího prvku zvuk")

    *Spuštění ovládacího prvku zvuk*

    > [!NOTE]
    > Můžete také vyzkoušet další fragmenty kódu, které jsou součástí sady Visual Studio, například video, obrázek atd.
5. Nyní se pokuste vložit ovládací prvek do některé části stránky. Například zkuste vložit ovládací prvek **GridView** , ale místo zadání **&lt;mřížky** začněte psát **&lt;GV**. Všimněte si, že seznam IntelliSense zobrazí ovládací prvek **ASP: GridView** .

    Technologie IntelliSense v editoru HTML nyní poskytuje vyhledávání na základě názvu a velikosti písmen a také částečné porovnávání (načítání všech prvků, které obsahují podmínky).

    ![Vložení prvku GridView se seznamy technologie IntelliSense](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image30.png "Vložení prvku GridView se seznamy technologie IntelliSense")

    *Vložení prvku GridView se seznamy technologie IntelliSense*

    Pokud zadáte **&lt;Grid** , zobrazí se všechny položky, které se shodují s termínem, ale Visual Studio navrhne ovládací prvek **GridView** :

    ![Vložení prvku GridView pomocí seznamů IntelliSense a částečného spárování](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image31.png "Vložení prvku GridView pomocí seznamů IntelliSense a částečného spárování")

    *Vložení prvku GridView pomocí seznamů IntelliSense a částečného spárování*

<a id="Ex2Task4"></a>

<a id="Task_4_-_HTML_Editor_Smart_Tags"></a>
#### <a name="task-4---html-editor-smart-tags"></a>Úloha 4 – inteligentní značky editoru HTML

Dalším vylepšením v editoru HTML je funkce inteligentních značek. Inteligentní značky usnadňují provádění běžných nebo opakujících se úloh vývoje na základě jednotlivých ovládacích prvků. Tato funkce byla již k dispozici v Návrháři HTML, ale ne v editoru HTML.

1. Otevřete **Web. Master** a vyhledejte prvek **ASP: menu** . Umístěte kurzor na značku Start a Všimněte si, že malý glyf zobrazený v dolní části elementu – kliknutím na něj otevřete nabídku inteligentní úlohy. Všimněte si, že máte rychlý přístup k některým úlohám souvisejícím s ovládacím prvkem nabídky.

    ![Inteligentní úkoly pro ovládací prvek nabídky](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image32.png "Inteligentní úkoly pro ovládací prvek nabídky")

    *Inteligentní úkoly pro ovládací prvek nabídky*

<a id="Ex2Task5"></a>

<a id="Task_5_-_Smart_Indentation"></a>
#### <a name="task-5---smart-indentation"></a>Úkol 5 – inteligentní odsazení

Jedním z osvědčených postupů ve formátu HTML je odsadit vnořené prvky, aby kód zůstal čitelný. V aplikaci Visual Studio 2012 zjistíte, že editor při psaní kódu automaticky odsadí prvky.

> [!NOTE]
> V předchozí verzi sady Visual Studio bylo inteligentní odsazení k dispozici v editoru XML, ale ne v editoru HTML.

1. Ujistěte se, že je konfigurace odsazení v editoru HTML nastavená na inteligentní odsazení. To provedete tak, že vyberete **nástroje |** Možnost nabídky možnosti a potom vyberte **textový editor | HTML | Stránka karty** v levém podokně obrazovky Vyberte možnost inteligentní odsazení.

    ![Nastavení editoru HTML](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image33.png "Nastavení editoru HTML")

    *Nastavení editoru HTML*
2. Na stránce **Default. aspx** odeberte veškerý obsah v rámci prvku zvuk.
3. Umístěte kurzor na konec otevřeného **zvukového** prvku a stiskněte klávesu **ENTER**.

    Všimněte si, že nová pozice kurzoru má další úroveň odsazení.

    ![Inteligentní odsazení v editoru HTML](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image34.png "Inteligentní odsazení v editoru HTML")

    *Inteligentní odsazení v editoru HTML*
4. Obnovte zvukovou značku pomocí odebraného obsahu nebo zavřete **Default. aspx** bez uložení změn.

<a id="Ex2Task6"></a>

<a id="Task_6_-_Extract_to_User_Control"></a>
#### <a name="task-6---extract-to-user-control"></a>Úloha 6 – extrakce do uživatelského ovládacího prvku

Nástroje refaktoringu, které jsou součástí sady Visual Studio, například extrakce části kódu pro funkci, jsou skvělé funkce, které usnadňují vylepšení a refaktoring existujícího kódu. Protějšek pro stránky ASP.NET by představoval extrakci kódu HTML do uživatelského ovládacího prvku. Ruční provedení by zahrnovalo několik kroků, jako je vytvoření nového uživatelského ovládacího prvku, přesunutí oddílu kódu do uživatelského ovládacího prvku, registrace předpony značky pro uživatelský ovládací prvek a nakonec, vytvoření instance uživatelského ovládacího prvku na stránkách. Nový nástroj pro *extrakci do uživatelského ovládacího prvku* teď provede všechny tyto kroky automaticky.

V této úloze použijete novou kontextovou operaci extrahovat do uživatelského ovládacího prvku pro vygenerování nového uživatelského ovládacího prvku z vybraného kódu.

1. Na stránce **Default. aspx** vyberte prvky **H2** a **audio** .
2. Klikněte pravým tlačítkem a vyberte **extrahovat do uživatelského ovládacího prvku**.

    ![Možnost extrahovat do nabídky uživatelského ovládacího prvku](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image35.png "Možnost extrahovat do nabídky uživatelského ovládacího prvku")

    *Možnost extrahovat do nabídky uživatelského ovládacího prvku*
3. Zadejte název nového uživatelského ovládacího prvku. Například **jukebox. ascx**a pak klikněte na **OK**.

    ![Ukládání extrahovaných uživatelských ovládacích prvků](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image36.png "Ukládání extrahovaných uživatelských ovládacích prvků")

    *Ukládání extrahovaných uživatelských ovládacích prvků*
4. Všimněte si, že vybraný kód byl extrahován do uživatelského ovládacího prvku a původní umístění vybraného kódu bylo nahrazeno instancí nového uživatelského ovládacího prvku.

    ![Stránka se automaticky aktualizovala tak, aby používala nový uživatelský ovládací prvek.](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image37.png "Stránka se automaticky aktualizovala tak, aby používala nový uživatelský ovládací prvek.")

    *Stránka se automaticky aktualizovala tak, aby používala nový uživatelský ovládací prvek.*
5. Stisknutím klávesy **F5** spusťte stránku a ověřte, zda ovládací prvek funguje.

<a id="Exercise3"></a>

<a id="Exercise_3_Whats_New_in_the_JavaScript_Editor"></a>
### <a name="exercise-3-whats-new-in-the-javascript-editor"></a>Cvičení 3: co je nového v editoru JavaScriptu

Psaní nebo úprava kódu JavaScriptu není jednoduchý úkol, zejména v případě, že se vaše aplikace začne zvětšovat a vy zjistíte, že budete pracovat s dlouhými soubory a stovkami funkcí. Vývojáři skriptu obvykle potřebují udělat nějakou další práci, aby bylo možné udržet čitelnost kódu a procházet mezi soubory. Díky zahrnutí knihoven JavaScriptu, jako je jQuery, se navigace v skriptech stala samotným výzvou z důvodu délky kódu.

Visual Studio obnovilo Editor jazyka JavaScript se příslibem tak, aby byl režim kódu přístupný a uspořádaný. Mnoho funkcí sady Visual Studio, které již C# existovaly v nástroji nebo editory VB, jsou nyní implementovány v editoru JavaScriptu: přejít k definici, automatické odsazení, dokumentaci a ověření při psaní. Díky obnovenému seznamu IntelliSense budete mít katalog funkcí JavaScriptu na dosah ruky.

V tomto cvičení se seznámíte s některými novými funkcemi a vylepšeními editoru JavaScriptu. Budete procházet ukázkové soubory a zjišťovat všechny nové charakteristiky, které budou v sadě Visual Studio 2012 efektivnější pro programování v JavaScriptu.

<a id="Ex3Task1"></a>

<a id="Task_1_-_JavaScript_Editor_New_Features"></a>
#### <a name="task-1---javascript-editor-new-features"></a>Úloha 1 – nové funkce editoru JavaScriptu

Tato úloha vás seznámí s některými z nových funkcí editoru JavaScriptu, které se zaměřují na organizování kódu a lepší uživatelské prostředí.

1. Pokud ještě není otevřený, spusťte sadu **Visual Studio** a otevřete řešení **WhatsNewASPNET. sln** ve složce **Source\WhatsNewASPNET** tohoto testovacího prostředí.
2. Stisknutím klávesy **F5** spusťte aplikaci a potom klikněte na odkaz JavaScriptu na navigačním panelu. Aktualizujte stránku několikrát a podívejte se, jak čítače zvýší.

    ![Čítač stránky](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image38.png "Čítač stránky")

    *Čítač stránky*
3. Zavřete prohlížeč a vraťte se do sady Visual Studio.
4. Otevřete stránku **JavaScript. aspx** a vyhledejte&lt;blok **&gt;skriptu** (viz níže).

    Následující kód používá místní úložiště HTML5 k uložení proměnné *pageLoadCount* , která ukládá počet navštívených stránek aktuálním uživatelem. Místní úložiště je databáze klíč-hodnota na straně klienta, kterou přináší Standard HTML5. Data se ukládají v místním počítači do prohlížeče uživatele.

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample7.html)]

    > [!NOTE]
    > Než budete pokračovat v dalších krocích, ujistěte se, že je typ DOCTYPE nastavený na XHTML5.
5. Upravte kód a Všimněte si, že technologie IntelliSense pro JavaScript obsahuje funkce HTML5, jako je místní úložiště, a jejich vnitřní metody.

    ![Funkce jazyka HTML5 JavaScriptu v JavaScriptu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image39.png "Funkce jazyka HTML5 JavaScriptu v JavaScriptu")

    *Funkce jazyka HTML5 JavaScriptu v JavaScriptu*
6. Klikněte na libovolnou levou hranatou závorku ( **{** ) ze skriptovacího kódu a Všimněte si, že se zvýrazní hranaté závorky.

    ![Hranaté závorky jsou zvýrazněné](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image40.png "Hranaté závorky jsou zvýrazněné")

    *Hranaté závorky jsou zvýrazněné*
7. Odkomentujte funkci **testAutoAlign ()** (vyberte tři řádky a můžete použít **klávesovou zkratku CTRL** + **K**; **CTRL** + **U**) a vyhledejte kurzor uvnitř kódu funkce. Stiskněte klávesu ENTER a přidejte tak druhý řádek. Všimněte si, že kód je nyní **zarovnán** a **automaticky odsazen**.

    ![JavaScriptový kód se automaticky zarovnává.](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image41.png "JavaScriptový kód se automaticky zarovnává.")

    *JavaScriptový kód se automaticky zarovnává.*

<a id="Ex3Task2"></a>

<a id="Task_2_-_Validating_JavaScript"></a>
#### <a name="task-2---validating-javascript"></a>Úloha 2 – ověřování JavaScriptu

V této úloze zjistíte nové ověřování JavaScriptu pro ECMAScript5 Standard. Tato funkce vám pomůže s psaním kompatibilního kódu JavaScriptu a zároveň zabraňuje problémům skriptování před nasazením lokality.

> [!NOTE]
> Visual Studio 2010 implementovalo dodržování předpisů ECMAStript3, zatímco Visual Studio 2012 zajišťuje dodržování předpisů ECMAScript5.

1. Otevřete **ECMA5script5. js** umístěný ve složce projektu **Scripts\custom** . Nyní budete testovat ověření pro ECMAScript5 Standard.

    [!code-html[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample8.html)]

    Na prvním řádku souboru můžete &quot; **použít striktní** &quot;, což umožňuje **striktní režim**ECMAScript5. Tento režim se skládá z podmnožiny jazyka, který objasňuje nejednoznačnosti z minulé edice a přidává některé nové funkce, jako jsou metody getter a setter, podpora knihoven pro JSON a další kompletní reflexe vlastností objektu.
2. Otevřete **Seznam chyb** , pokud ještě není otevřený (**Zobrazit** nabídku | **Seznam chyb**). Všimněte si, že je deklarace **funkce** podtržená. Důvodem je, že ve standardních funkcích ECMA5 nelze vnořovat do jazykových struktur. V seznamu chyb se zobrazí podrobnosti upozornění.

    ![Chybová zpráva ověřování JavaScriptu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image42.png "Chybová zpráva ověřování JavaScriptu")

    *Chybová zpráva ověřování JavaScriptu*
3. Odkomentujte **&quot;použijte striktní&quot;** a Všimněte si, že chyby zmizí, ale upozornění zůstanou.
4. Na posledním řádku souboru zapište libovolný řetězec, například **&quot;test&quot;** (včetně uvozovek pro indikaci, že se jedná o řetězec). Napište tečku vedle řetězce pro zobrazení seznamu IntelliSense a vyberte možnost **Trim** .

    V ECMAScript5 standard mají hodnoty a proměnné řetězců také definovány řetězcové metody, jako je například Trim, Velká písmena, hledání a nahrazování.

    ![Seznam IntelliSense v JavaScriptu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image43.png "Seznam IntelliSense v JavaScriptu")

    *Seznam IntelliSense v JavaScriptu*

<a id="Ex3Task3"></a>

<a id="Task_3_-_XML_Documentation_for_JavaScript"></a>
#### <a name="task-3---xml-documentation-for-javascript"></a>Úloha 3 – dokumentace XML pro JavaScript

V této úloze budete zkoumat funkce sady Visual Studio pro dokumentaci XML v JavaScriptu. Zobrazí se seznam JavaScript IntelliSense, který teď zobrazí dokumentaci XML každé funkce. Kromě toho se v JavaScriptu objeví navigační funkce.

1. Otevřete soubor **XMLDoc. js** umístěný ve složce **skripty nebo vlastní** složka projektu. Tento soubor obsahuje dokumentaci XML ke každé z funkcí jazyka JavaScript.

    ![Dokumentace XML JavaScriptu integrovaná do IntelliSense](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image44.png "Dokumentace XML JavaScriptu integrovaná do IntelliSense")

    *Dokumentace XML JavaScriptu integrovaná do IntelliSense*
2. Pod funkcí **Přidat** funkci v souboru **XMLDoc. js** vytvořte novou funkci s názvem **test**.
3. Ve funkci **test** volejte funkci **násobení** , která přijímá dva parametry. Všimněte si, že se v poli s popisem zobrazuje dokumentace k funkci **násobit** .

    [!code-javascript[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample9.js)]

    ![Dokumentace XML pro funkce JavaScriptu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image45.png "Dokumentace XML pro funkce JavaScriptu")

    *Dokumentace XML pro funkce JavaScriptu*
4. Dokončete příkaz volání funkce a zadejte *tečku* pro otevření seznamu IntelliSense na vrácené hodnotě. Všimněte si, že Visual Studio detekuje **vrácenou** hodnotu v dokumentaci a považuje hodnotu za číslo.

    ![Dokumentace XML pro návratové typy](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image46.png "Dokumentace XML pro návratové typy")

    *Dokumentace XML pro návratové typy*
5. Nyní vložte volání funkce Add. Všimněte si, že editor JavaScriptu teď podporuje přetížení funkcí. Když napíšete název funkce, budete moci vybrat kterékoli z dostupných přetížení uvedených v dokumentaci.

    ![Dokumentace XML pro přetížení](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image47.png "Dokumentace XML pro přetížení")

    *Dokumentace XML pro přetížení*
6. Otevřete soubor **GotoDefinition. js** a vyhledejte volání funkce **$ (). html ()** . Vyhledejte kurzor ve **formátu HTML**.
7. Stiskněte klávesu **F12** a přejděte do definice. Všimněte si, že teď máte přístup k kódu JavaScriptu a můžete ho Procházet bez použití nástroje **find** .
8. Vyhledejte kurzor v instrukci jQuery před blokem podpisu ve spodní části souboru kódu. Stiskněte klávesu **F12**. Přejdete na soubor knihovny jQuery. Všimněte si, že můžete také procházet soubory jQuery pomocí **F12**.

    ![Přechod na definice jQuery](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image48.png "Přechod na definice jQuery")

    *Přechod na definice jQuery*

> [!NOTE]
> Ujistěte se, že GotoDefinition. js neobsahuje žádné chyby syntaxe před uložením souboru.

<a id="Exercise4"></a>

<a id="Exercise_4_Bundling_and_Minification"></a>
### <a name="exercise-4-bundling-and-minification"></a>Cvičení 4: sdružování a minifikace

Kolikrát vaše weby obsahují více než jeden soubor JavaScript nebo CSS? Toto je velmi běžný scénář, kdy může sdružování a minifikace snížit velikost souboru a zrychlit jeho provádění. Nová funkce sdružování v sadě ASP.NET 4,5 sbalí sadu souborů JS nebo CSS do jediného prvku a zmenší její velikost tím, že minifikace obsah (tj. odebrání nevyžadují prázdné mezery, odebrání komentářů a omezení identifikátorů).

Sdružování a minifikace v ASP.NET 4,5 se provádí za běhu, aby proces mohl identifikovat uživatelského agenta (například IE, Mozilla atd.), a tak vylepšit komprimaci tím, že se zacílení na prohlížeč uživatelů (například odstranění věcí, které jsou specifické pro Mozilla. Když požadavek pochází z IE).

V tomto cvičení se naučíte, jak povolit a používat různé typy sdružování a minifikace v ASP.NET 4,5.

<a id="Ex4Task1"></a>

<a id="Task_1_-_Installing_the_Bundling_and_Minification_Package_from_NuGet"></a>
#### <a name="task-1---installing-the-bundling-and-minification-package-from-nuget"></a>Úloha 1 – instalace balíčku sdružování a minifikace z NuGetu

1. Pokud ještě není otevřený, spusťte sadu **Visual Studio** a otevřete řešení **WhatsNewASPNET. sln** ve složce **Source\WhatsNewASPNET** tohoto testovacího prostředí.
2. Otevřete konzolu Správce balíčků NuGet. Chcete-li to provést, použijte **zobrazení** nabídky | jiné **konzoly Správce balíčků** | **systému Windows** .

    ![Otevření Správce balíčků file:///C:/Users/User/AppData/Local/Temp/Marker3744//media/44462/Multiple-Stylesheets-and-JavaScript-files-in-the-application.pngconsole](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image49.png "Otevření konzoly Správce balíčků")

    *Otevření konzoly Správce balíčků*
3. V **konzole správce balíčků** zadejte **Install-Package Microsoft. Web. Optimization** a stiskněte klávesu **ENTER**.

<a id="Ex4Task2"></a>

<a id="Task_2_-_Default_Bundles"></a>
#### <a name="task-2---default-bundles"></a>Úloha 2 – výchozí sady svazků

Nejjednodušší způsob, jak použít sdružování a minifikace, je povolit výchozí balíčky. Tato metoda používá konvence k tomu, aby vám umožnil odkazování na sadu a minifikovaného verzi pro soubory JS a CSS ve složce.

V této úloze se dozvíte, jak povolit a odkazovat na soubory minifikovaného JS a šablony stylů CSS a zobrazit výsledný výstup.

1. Pokud ještě není otevřený, spusťte sadu **Visual Studio** a otevřete řešení **WhatsNewASPNET. sln** ve složce **Source\WhatsNewASPNET** tohoto testovacího prostředí.
2. V **Průzkumník řešení**rozbalte složky **Styles**, **Scripts\custom** a **Scripts\bundle** .

    Všimněte si, že aplikace používá více než jeden soubor CSS a JS.

    ![Více šablon stylů a souborů JavaScriptu v aplikaci](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image50.png "Více šablon stylů a souborů JavaScriptu v aplikaci")

    *Více šablon stylů a souborů JavaScriptu v aplikaci*
3. Otevřete soubor **Global.asax.cs** .

    Všimněte si, že nový obor názvů **Microsoft. Web. Optimization je označený** jako komentář na začátku souboru. Odkomentujte direktivu using, aby zahrnovala funkce sdružování a minifikace.

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample10.cs)]
4. Vyhledejte **aplikaci\_metodu Start** .

    V této metodě Odkomentujte volání EnableDefaultBundles, jak je znázorněno v následujícím fragmentu kódu. Díky tomu je možné odkazovat na kolekci souborů šablon stylů CSS ve složce pomocí cesty k této složce, a navíc &quot;šablon stylů CSS&quot; nebo&quot; příponou &quot;JS.

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample11.cs)]
5. Otevřete soubor **Optimization. aspx** a vyhledejte ovládací prvek obsahu pro **HeadContent**.

    Všimněte si, že soubory CSS a soubory JS mají jedinou odkazovanou značku.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample12.aspx)]

    > [!NOTE]
    > Tento kód je určen pro demonstrační účely. V ideálním případě budete odkazovat na sady v souboru site. Master. V tomto ukázkovém kódu zjistíte, že některé z těchto souborů jsou také odkazovány pomocí souboru site. Master, takže tento poslední odkaz bude redundantní.
6. Všimněte si, že odkazy používají konvence sdružování v atributu **href** k získání všech souborů CSS nebo JS ze složky Styles (styly) a Scripts\custom (v uvedeném pořadí).

    Můžete použít cesty **Scripts/Custom/js** , jak je znázorněno níže, chcete-li seskupit a minimalizuje všechny soubory JS v rámci **skriptů nebo vlastní** složky. Toto je výchozí chování u výchozích sad.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample13.aspx)]
7. Otevřete soubor **Styles\Site.CSS** .

    Všimněte si, že původní soubor CSS obsahuje odsazený kód, prázdné mezery a komentáře, které soubor zvětší. (Také soubor JavaScriptu obsahuje prázdné mezery a komentáře).

    ![Jeden z původních souborů CSS ve složce Scripts](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image51.png "Jeden z původních souborů CSS ve složce Scripts")

    *Jeden z původních souborů CSS ve složce Scripts*
8. Stisknutím klávesy **F5** spusťte aplikaci a přejděte na stránku **optimalizace** .
9. Klikněte na odkaz **Sada šablon stylů CSS** a stáhněte a otevřete soubor.

    Prohlédněte si soubor minifikovanéhoed. Všimněte si, že se odebraly všechny prázdné mezery, komentáře a znaky odsazení, což vygeneruje menší soubor.

    ![Rozbalené soubory šablon stylů CSS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image52.png "Rozbalené soubory šablon stylů CSS")

    *Rozbalené soubory šablon stylů CSS*
10. Nyní klikněte na odkaz **sady prostředků js** a otevřete soubor sady JavaScript. Upozornění Průzkumníka můžete bez obav ignorovat. Všimněte si, že soubory JavaScriptu ve **vlastní** složce jsou také seskupené a minifikovaného.

    ![Seskupené soubory JavaScriptu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image53.png "Seskupené soubory JavaScriptu")

    *Seskupené soubory JavaScriptu*

    Povolení komprese souborů CSS nebo JS bylo v předchozí verzi ASP.NET mnohem složitější. Nyní, jak jste viděli, stačí přidat jeden řádek do souboru *Global. asax* , aby se povolilo sdružování, a pak odkazovaly na soubory z vaší lokality.

<a id="Ex4Task3"></a>

<a id="Task_3_-_Static_Bundles"></a>
#### <a name="task-3---static-bundles"></a>Úloha 3 – statické sady

Přístup ke statickým svazkům vám umožní přizpůsobit sadu souborů na sady, odkaz a metodu minifikace, která se použije.

V této úloze nakonfigurujete statickou sadu pro definování konkrétní sady souborů, které se mají seskupit a minimalizuje.

1. Zavřete prohlížeč.
2. Otevřete soubor **Global.asax.cs** a vyhledejte **aplikaci\_spustit** metodu.
3. Odkomentujte kód statické sady, jak je znázorněno v následujícím kódu.

    Definujete statickou sadu, na kterou se bude odkazovat &quot; **~/StaticBundle**&quot; virtuální cesta, a použijte **JsMinify** pro minifikace všech zadaných souborů pomocí metody **AddFile** . Nakonec přidáváte statickou sadu do **Kompletované sady prostředků** a povolíte ji.

    Všimněte si, že soubory nejsou umístěny na stejném místě; Toto je další výhoda oproti výchozímu sdružování.

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample14.cs)]
4. Otevřete soubor **Optimization. aspx** .

    Všimněte si, že odkaz na **svazek statického js** používá cestu, kterou jste deklarovali při konfiguraci statické sady v souboru Global.asax.cs: **/StaticBundle**.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample15.aspx)]
5. Stisknutím klávesy **F5** spusťte aplikaci a potom přejděte na stránku **optimalizace** .
6. Kliknutím na odkaz **sady statických js** otevřete soubor.

    Všimněte si, že soubor JavaScriptu minifikovanéhoed je výstupem všech souborů JavaScriptu nakonfigurovaných v souboru statické sady v cestě &quot;/StaticBundle&quot;.

    ![Sada statických souborů JavaScriptu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image54.png "Sada statických souborů JavaScriptu")

    *Sada statických souborů JavaScriptu*
7. Zavřete prohlížeč a vraťte se do sady Visual Studio.

<a id="Ex4Task4"></a>

<a id="Task_4_-_Dynamic_Folder_Bundles"></a>
#### <a name="task-4---dynamic-folder-bundles"></a>Úloha 4 – sady svazků dynamické složky

V této úloze se naučíte konfigurovat sady prostředků dynamické složky. Výkonem dynamického sdružování je, že můžete zahrnovat statické JavaScripty i jiné soubory v jazycích, které se zkompiluje do JavaScriptu, a proto vyžadují určité zpracování ještě před provedením sdružování.

V tomto příkladu se naučíte, jak pomocí třídy **DynamicFolderBundle** vytvořit dynamickou sadu souborů napsaných v CofeeScript. CofeeScript je programovací jazyk, který se kompiluje do JavaScriptu a poskytuje jednodušší syntaxi pro psaní kódu JavaScriptu, což usnadňuje zkrácení a čitelnost JavaScriptu.

1. Otevřete soubor **Global.asax.cs** a vyhledejte **aplikaci\_spustit** metodu.
2. Odkomentujte kód dynamické sady, jak je znázorněno v následujícím kódu.

    Definujete sadu prostředků dynamické složky, která bude používat vlastní procesor **CoffeeMinify** minifikace, který se bude vztahovat pouze na soubory s příponou&quot; &quot; **. kávy** (soubory CoffeeScript). Všimněte si, že pomocí vzoru hledání můžete vybrat soubory, které se mají seskupit do složky, například '\*. káva '.

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample16.cs)]
3. Otevřete konzolu Správce balíčků NuGet. Chcete-li to provést, použijte **zobrazení** nabídky | jiné **konzoly Správce balíčků** | **systému Windows** .
4. V **konzole správce balíčků** zadejte **Install-Package CoffeeSharp** a stiskněte klávesu **ENTER**.
5. Klikněte na tlačítko **Zobrazit všechny soubory** v okně **Průzkumník řešení**

    ![Zobrazení všech souborů](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image55.png "Zobrazení všech souborů")

    *Zobrazení všech souborů*
6. V **Průzkumník řešení** klikněte pravým tlačítkem na soubor **CoffeeMinify.cs** a vyberte **zahrnout do projektu** .

    ![Zahrnout soubor CoffeeMinify.cs do projektu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image56.png "Zahrnout soubor CoffeeMinify.cs do projektu")

    *Zahrnout soubor CoffeeMinify.cs do projektu*
7. Otevřete soubor **CoffeeMinify.cs** .

    Tato třída dědí z JsMinify, aby minimalizuje výstup JavaScriptu, který je výsledkem kompilace kódu CoffeeScript. Volá kompilátor CoffeeScript pro vygenerování kódu JavaScriptu a pak ho pošle metodě JsMinify. Process, aby minimalizuje výsledný kód.

    [!code-csharp[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample17.cs)]
8. Otevřete soubory **Script1. kávy** a **Script2. kávy** ze složky **skripty/sady prostředků** .

    Tyto soubory budou zahrnovat kód CoffeScript, který se má kompilovat při provádění sdružování s třídou CoffeeMinify.

    V zájmu zjednodušení jsou poskytnuté soubory CoffeeScript, včetně ukázkového kódu CoffeeScript. Komentáře jsou vyloučeny z procesu JsMinify.

    ![Soubory CoffeeScript](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image57.png "Soubory CoffeeScript")

    *Soubory CoffeeScript*

    > [!NOTE]
    > [CofeeScript](https://github.com/jashkenas/coffeescript/) poskytuje jednodušší syntaxi pro psaní kódu JavaScriptu, vylepšení zkrácení a čitelnosti JavaScriptu, jakož i přidávání dalších funkcí, jako je porozumění poli a porovnávání vzorů.
9. Otevřete soubor **Optimization. aspx** a vyhledejte odkazy na skupinu.

    Všimněte si, že odkaz na **svazek dynamické knihovny JS** odkazuje na složku **Scripts/** **re/Coffees** pomocí přípony pro, kterou jste nakonfigurovali pro sadu svazků dynamické složky.

    [!code-aspx[Main](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/samples/sample18.aspx)]
10. Stisknutím klávesy **F5** spusťte aplikaci a potom přejděte na stránku **optimalizace** .
11. Kliknutím na odkaz **sady dynamických js** Otevřete vygenerovaný soubor.

    Všimněte si, že obsah, který byl součástí této sady, obsahuje pouze soubory **. kávy** . Můžete také zjistit, že kód CoffeeScript byl zkompilován do JavaScriptu a řádky s komentářem byly odstraněny.

    ![Sada dynamických souborů JS](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image58.png "Sada dynamických souborů JS")

    *Sada dynamických souborů JS*

> [!NOTE]
> Kromě toho můžete tuto aplikaci nasadit na weby Windows Azure podle [dodatku B: publikování aplikace ASP.NET MVC 4 pomocí nasazení webu](#AppendixB).

<a id="Summary"></a>
## <a name="summary"></a>Souhrn

Toto testovací prostředí vám pomůže pochopit, co je nového v ASP.NET a vývoji pro web v aplikaci Visual Studio 2012 a jak využít výhod různých vylepšení v rámci sady Visual Studio 2012.

Po absolvování tohoto praktického cvičení se naučíte používat nové funkce a vylepšení editorů Visual Studio 2012 pro šablony stylů CSS, JavaScript a HTML. Navíc se naučíte, jak Visual Studio 2012 implementuje předdefinované sdružování a minifikace.

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a>Příloha A: instalace Visual Studio Express 2012 pro web

**Microsoft Visual Studio Express 2012 pro web** nebo jinou verzi &quot;Express&quot; můžete nainstalovat pomocí **[Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)** . Následující pokyny vás provedou kroky potřebnými k instalaci sady *Visual Studio Express 2012 for Web* pomocí *Instalace webové platformy Microsoft*.

1. Přejít na [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169). Případně, pokud jste již nainstalovali instalační program webové platformy, můžete jej otevřít a vyhledat produkt &quot;<em>Visual Studio Express 2012 pro web pomocí sady Windows Azure SDK</em>&quot;.
2. Klikněte na **nainstalovat hned**. Pokud nemáte **instalační program webové platformy** , budete přesměrováni, abyste ho stáhli a nainstalovali jako první.
3. Po otevření **instalačního programu webové platformy** klikněte na **nainstalovat** a spusťte instalaci.

    ![Nainstalovat Visual Studio Express](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image59.png "Nainstalovat Visual Studio Express")

    *Nainstalovat Visual Studio Express*
4. Přečtěte si všechny licence a podmínky produktů a pokračujte **kliknutím na Souhlasím.**

    ![Přijetí licenčních podmínek](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image60.png)

    *Přijetí licenčních podmínek*
5. Počkejte na dokončení procesu stahování a instalace.

    ![Průběh instalace](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image61.png)

    *Průběh instalace*
6. Po dokončení instalace klikněte na **Dokončit**.

    ![Instalace dokončena](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image62.png)

    *Instalace dokončena*
7. Kliknutím na tlačítko **ukončit** zavřete instalační program webové platformy.
8. Pokud chcete otevřít Visual Studio Express pro web, přejděte na **úvodní** obrazovku a začněte psát &quot;**vs Express**&quot;a pak klikněte na dlaždici **vs Express for Web** .

    ![Dlaždice VS Express for Web](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image63.png)

    *Dlaždice VS Express for Web*

---

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Příloha B: publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu

V tomto dodatku se dozvíte, jak vytvořit nový web z Windows Azure Portál pro správu a jak publikovat aplikaci, kterou jste získali, pomocí testovacího prostředí s využitím funkce Nasazení webu pro publikování poskytované službou Windows Azure.

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a>Úloha 1 – Vytvoření nového webu z portálu Windows Azure

1. Přejít na [portál pro správu Windows Azure](https://manage.windowsazure.com/) a přihlaste se pomocí přihlašovacích údajů Microsoftu přidružených k vašemu předplatnému.

    > [!NOTE]
    > S Windows Azure můžete hostovat 10 ASP.NET webů zdarma a pak škálovat podle nárůstu provozu. [Tady](https://aka.ms/aspnet-hol-azure)se můžete zaregistrovat.

    ![Přihlaste se k Windows Azure Portal](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image64.png "Přihlaste se k Windows Azure Portal")

    *Přihlášení k Windows Azure Portál pro správu*
2. Na panelu příkazů klikněte na **Nový** .

    ![Vytvoření nového webu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image65.png "Vytvoření nového webu")

    *Vytvoření nového webu*
3. Klikněte na **compute** | **Web**. Pak vyberte možnost **rychlé vytvoření** . Zadejte dostupnou adresu URL pro nový web a klikněte na **vytvořit web**.

    > [!NOTE]
    > Web Windows Azure je hostitelem webové aplikace běžící v cloudu, kterou můžete řídit a spravovat. Možnost rychle vytvořit umožňuje nasadit dokončenou webovou aplikaci do webu Windows Azure z oblasti mimo portál. Nezahrnuje kroky pro nastavení databáze.

    ![Vytvoření nového webu pomocí rychlého vytvoření](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image66.png "Vytvoření nového webu pomocí rychlého vytvoření")

    *Vytvoření nového webu pomocí rychlého vytvoření*
4. Počkejte, než se nový **Web** vytvoří.
5. Po vytvoření webu klikněte na odkaz ve sloupci **Adresa URL** . Ověřte, zda nový web funguje.

    ![Procházení na nový web](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image67.png "Procházení na nový web")

    *Procházení na nový web*

    ![Běžící Web](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image68.png "Běžící Web")

    *Běžící Web*
6. Vraťte se na portál a kliknutím na název webu pod sloupcem **název** zobrazíte stránky pro správu.

    ![Otevření stránek správy webu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image69.png "Otevření stránek správy webu")

    *Otevření stránek správy webu*
7. Na stránce **řídicí panel** klikněte v části **rychlý přehled** na odkaz **Stáhnout profil publikování** .

    > [!NOTE]
    > *Profil publikování* obsahuje všechny informace potřebné k publikování webové aplikace na webu Windows Azure pro každou povolenou metodu publikace. Profil publikování obsahuje adresy URL, přihlašovací údaje uživatele a databázové řetězce potřebné k připojení a ověření proti jednotlivým koncovým bodům, pro které je povolena metoda publikace. **Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** a **Microsoft Visual Studio 2012** podporují čtení profilů publikování pro automatizaci konfigurace těchto programů pro publikování webových aplikací na webech Windows Azure.

    ![Stahuje se publikační profil webu.](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image70.png "Stahuje se publikační profil webu.")

    *Stahuje se publikační profil webu.*
8. Stáhněte si soubor profilu publikování do známého umístění. V tomto cvičení se dozvíte, jak tento soubor použít k publikování webové aplikace na webech Windows Azure ze sady Visual Studio.

    ![Ukládání souboru profilu publikování](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image71.png "Ukládá se publikační profil.")

    *Ukládání souboru profilu publikování*

<a id="Ex1Task2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a>Úloha 2 – Konfigurace databázového serveru

Pokud vaše aplikace využívá SQL Server databází, budete muset vytvořit SQL Database Server. Pokud chcete nasadit jednoduchou aplikaci, která nepoužívá SQL Server, můžete tuto úlohu přeskočit.

1. Pro uložení aplikační databáze budete potřebovat server SQL Database. SQL Database servery můžete zobrazit z předplatného na portálu pro správu Windows Azure na stránce **databáze SQL** | **serverech** | **řídicím panelu serveru**. Pokud nemáte vytvořený server, můžete ho vytvořit pomocí tlačítka **Přidat** na panelu příkazů. Poznamenejte si **název serveru a adresu URL, přihlašovací jméno a heslo správce**, jak je budete používat v dalších úlohách. Databázi ještě nevytvářejte, protože bude vytvořená v pozdější fázi.

    ![Řídicí panel serveru SQL Database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image72.png "Řídicí panel serveru SQL Database")

    *Řídicí panel serveru SQL Database*
2. V další úloze budete testovat připojení k databázi ze sady Visual Studio, z tohoto důvodu je třeba zahrnout místní IP adresu do seznamu **povolených IP adres**serveru. Provedete to tak, že kliknete na **Konfigurovat**, vyberete IP adresu z **aktuální IP adresy klienta** a vložíte ji do textových polí **Počáteční IP adresa** a **koncová IP** adresa. Zadejte název pravidla a klikněte na tlačítko ![přidat-Client-IP-Address-tlačítko](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image73.png) tlačítko.

    ![Přidává se IP adresa klienta.](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image74.png)

    *Přidává se IP adresa klienta.*
3. Jakmile se **IP adresa klienta** přidá do seznamu povolených IP adres, potvrďte změny kliknutím na **Uložit** .

    ![Potvrdit změny](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image75.png)

    *Potvrdit změny*

<a id="Ex1Task3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a>Úloha 3 – publikování aplikace ASP.NET MVC 4 pomocí Nasazení webu

1. Vraťte se do řešení ASP.NET MVC 4. V **Průzkumník řešení**klikněte pravým tlačítkem myši na webový projekt a vyberte **publikovat**.

    ![Publikování aplikace](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image76.png "Publikování aplikace")

    *Publikování webu*
2. Importujte profil publikování, který jste uložili v prvním úkolu.

    ![Import profilu publikování](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image77.png "Import profilu publikování")

    *Importuje se publikační profil.*
3. Klikněte na **ověřit připojení**. Po dokončení ověřování klikněte na **Další**.

    > [!NOTE]
    > Ověření je dokončeno, jakmile se zobrazí zelená značka zaškrtnutí vedle tlačítka ověřit připojení.

    ![Ověřování připojení](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image78.png "Ověřování připojení")

    *Ověřování připojení*
4. Na stránce **Nastavení** v části **databáze** klikněte na tlačítko vedle textového pole připojení k databázi (tj. **DefaultConnection**).

    ![Konfigurace nasazení webu](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image79.png "Konfigurace nasazení webu")

    *Konfigurace nasazení webu*
5. Připojení k databázi nakonfigurujte následujícím způsobem:

   - Do pole **název serveru** zadejte adresu URL serveru SQL Database pomocí předpony *TCP:* .
   - V **uživatelské jméno** zadejte přihlašovací jméno správce serveru.
   - V **heslo** zadejte přihlašovací heslo správce serveru.
   - Zadejte nový název databáze, například: *MVC4SampleDB*.

     ![Konfigurace cílového připojovacího řetězce](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image80.png "Konfigurace cílového připojovacího řetězce")

     *Konfigurace cílového připojovacího řetězce*
6. Pak klikněte na **OK**. Po zobrazení výzvy k vytvoření databáze klikněte na **Ano**.

    ![Vytvoření databáze](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image81.png "Vytváří se řetězec databáze.")

    *Vytvoření databáze*
7. Připojovací řetězec, který budete používat pro připojení k SQL Database ve Windows Azure, se zobrazí ve výchozím textovém poli připojení. Pak klikněte na tlačítko **Další**.

    ![Připojovací řetězec ukazující na SQL Database](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image82.png "Připojovací řetězec ukazující na SQL Database")

    *Připojovací řetězec ukazující na SQL Database*
8. Na stránce **Náhled** klikněte na **publikovat**.

    ![Publikování webové aplikace](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image83.png "Publikování webové aplikace")

    *Publikování webové aplikace*
9. Jakmile se proces publikování dokončí, otevře se ve výchozím prohlížeči publikovaný web.

    ![Aplikace byla publikována na platformě Windows Azure](whats-new-in-aspnet-and-web-development-in-visual-studio-2012/_static/image84.png "Aplikace byla publikována na platformě Windows Azure")

    *Aplikace byla publikována na platformě Windows Azure*

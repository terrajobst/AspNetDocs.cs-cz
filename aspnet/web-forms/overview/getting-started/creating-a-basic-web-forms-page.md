---
uid: web-forms/overview/getting-started/creating-a-basic-web-forms-page
title: Vytvoření základní stránky webových formulářů ASP.NET 4,5 pomocí Visual Studio 2013
author: Erikre
description: ''
ms.author: riande
ms.date: 03/03/2014
ms.assetid: a2f1c635-0817-4a9a-8c13-d5b5d29727c0
msc.legacyurl: /web-forms/overview/getting-started/creating-a-basic-web-forms-page
msc.type: authoredcontent
ms.openlocfilehash: 5d13a51128eecd92a82cfd06054448582a348e11
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445679"
---
# <a name="using-visual-studio-2013-to-create-a-basic-aspnet-45-web-forms-page"></a>Vytvoření základní stránky webových formulářů ASP.NET 4,5 pomocí Visual Studio 2013

od [Erik Reitan](https://github.com/Erikre)

[!INCLUDE[](~/includes/rp.md)]

Tento názorný postup vám poskytne Úvod do vývojového prostředí webu v [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) a v [Microsoft Visual Studio Express 2013 pro web](https://www.microsoft.com/visualstudio/11/downloads#express-web). Tento návod vás provede vytvořením jednoduché stránky webových formulářů ASP.NET a znázorňuje základní techniky vytváření nové stránky, přidávání ovládacích prvků a psaní kódu.

Úlohy, které jsou znázorněné v tomto návodu, zahrnují:

- Vytvoření projektu aplikace webového formuláře systému souborů.
- Familiarizing se sadou Visual Studio.
- Vytvoření stránky ASP.NET
- Přidávání ovládacích prvků.
- Přidávání obslužných rutin událostí.
- Spouštění a testování stránky ze sady Visual Studio.

## <a name="prerequisites"></a>Požadavky

Aby bylo možné dokončit tento návod, budete potřebovat:

- [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) nebo [Microsoft Visual Studio Express 2013 pro web](https://www.microsoft.com/visualstudio/11/downloads#express-web). .NET Framework se nainstaluje automaticky. 

    > [!NOTE] 
    > 
    > Microsoft Visual Studio 2013 a Microsoft Visual Studio Express 2013 pro web se často v této sérii kurzů označují jako Visual Studio.  
    >   
    > Pokud používáte sadu Visual Studio, tento návod předpokládá, že jste vybrali kolekci pro **Vývoj webu** nastavení při prvním spuštění sady Visual Studio. Další informace najdete v tématu [Postupy: výběr nastavení prostředí pro vývoj webu](https://msdn.microsoft.com/library/ff521558.aspx).

## <a name="creating-a-web-application-project-and-a-page"></a>Vytvoření projektu webové aplikace a stránky

<a id="sectionToggle0"></a>

V této části návodu vytvoříte projekt webové aplikace a přidáte do něj novou stránku. Přidáte také text HTML a spustíte stránku v prohlížeči.

### <a name="to-create-a-web-application-project"></a>Vytvoření projektu webové aplikace

1. Otevřete Microsoft Visual Studio.
2. V nabídce **soubor** vyberte **Nový projekt**.  
    ![nabídky soubor](creating-a-basic-web-forms-page/_static/image1.png)

    Zobrazí se dialogové okno **Nový projekt** .
3. Na levé straně vyberte **šablony** -&gt; skupinu **Web** Templates &gt; **Visual C#**  -.
4. V prostředním sloupci vyberte šablonu **webové aplikace ASP.NET** .
5. Pojmenujte projekt ***BasicWebApp*** a klikněte na tlačítko **OK** .   
Dialogové okno ![nový projekt](creating-a-basic-web-forms-page/_static/image2.png)
6. Potom vyberte šablonu **webové formuláře** a kliknutím na tlačítko **OK** vytvořte projekt.  
Dialogové okno ![nový projekt v ASP.NET](creating-a-basic-web-forms-page/_static/image3.png)  

    Visual Studio vytvoří nový projekt, který obsahuje předem sestavené funkce založené na šabloně webových formulářů. Neposkytuje vám jenom stránku *Home. aspx* , stránku *About. aspx* , stránku *Contact. aspx* , ale taky obsahuje funkce členství, které registrují uživatele a ukládají jejich přihlašovací údaje, aby se mohli přihlásit k webu. Když se vytvoří nová stránka, ve výchozím nastavení Visual Studio zobrazí stránku v zobrazení **zdroje** , kde uvidíte prvky HTML stránky. Následující ilustrace znázorňuje, co byste viděli v zobrazení **zdroje** , pokud jste vytvořili novou webovou stránku s názvem *BasicWebApp. aspx*.  
    Zobrazení zdrojového ![](creating-a-basic-web-forms-page/_static/image4.png)

### <a name="a-tour-of-the-visual-studio-web-development-environment"></a>Prohlídka vývojového prostředí webu sady Visual Studio

Než budete pokračovat úpravou stránky, je vhodné se seznámit s vývojovým prostředím sady Visual Studio. Následující ilustrace znázorňuje okna a nástroje, které jsou k dispozici v aplikaci Visual Studio a Visual Studio Express pro web.

> [!NOTE] 
> 
> Tento diagram zobrazuje výchozí umístění oken a oken. V nabídce **zobrazení** můžete zobrazit další okna a změnit uspořádání a velikost oken tak, aby vyhovovaly vašim potřebám. Pokud již byly provedeny změny v uspořádání oken, co se vám zobrazí, obrázek nebude odpovídat.

 Prostředí sady Visual Studio

![Prostředí sady Visual Studio](creating-a-basic-web-forms-page/_static/image5.png)

### <a name="familiarize-yourself-with-the-web-designer"></a>Seznamte se s Webový návrhář

Projděte si výše uvedený obrázek a porovnejte text s následujícím seznamem, který popisuje nejčastěji používaná okna a nástroje. (Ne všechny zobrazené systémy Windows a nástroje jsou zde uvedeny, pouze ty označené na předchozí ilustraci.)

- Představuje. Poskytněte příkazy pro formátování textu, hledání textu a tak dále. Některé panely nástrojů jsou k dispozici pouze v případě, že pracujete v **návrhovém** zobrazení.
- **Průzkumník řešení** okno Zobrazí soubory a složky ve vaší webové aplikaci.
- Okno dokumentu. Zobrazí dokumenty, na kterých pracujete v oknech s kartami. Můžete přepínat mezi dokumenty kliknutím na karty.
- Okno **vlastnosti** . Umožňuje změnit nastavení pro stránku, prvky HTML, ovládací prvky a další objekty.
- Zobrazí karty. K dispozici jsou různá zobrazení stejného dokumentu. **Návrhové** zobrazení je plocha pro úpravy poblíž WYSIWYG. Zobrazení **zdroje** je editor HTML pro stránku. **Rozdělené** zobrazení zobrazuje **Návrh** i zobrazení **zdroje** dokumentu. Později v tomto návodu budete pracovat se zobrazeními **Návrh** a **zdroj** . Pokud dáváte přednost otevírání webových stránek v zobrazení **Návrh** , v nabídce **nástroje** klikněte na možnost **Možnosti**, vyberte uzel **Návrháře HTML** a změňte možnost **úvodní stránky** .
- **Sada nástrojů**. Poskytuje ovládací prvky a prvky HTML, které lze přetáhnout na stránku. Prvky **sady nástrojů** jsou seskupeny podle běžné funkce.
- S **erver Explorer**. Zobrazí databázová připojení. Pokud Průzkumník serveru není zobrazená, klikněte v nabídce zobrazení na položku Průzkumník serveru.

### <a name="creating-a-new-aspnet-web-forms-page"></a>Vytvoření nové stránky webových formulářů ASP.NET

Když vytvoříte novou aplikaci webového formuláře pomocí šablony projektu **webové aplikace ASP.NET** , Visual Studio přidá stránku ASP.NET (stránku webového formuláře) s názvem *Default. aspx*a také několik dalších souborů a složek. Stránku *Default. aspx* můžete použít jako domovskou stránku webové aplikace. Pro tento návod ale vytvoříte a budete pracovat s novou stránkou.

### <a name="to-add-a-page-to-the-web-application"></a>Přidání stránky do webové aplikace

1. Zavřete stránku *Default. aspx* . Provedete to tak, že kliknete na kartu, která zobrazuje název souboru, a potom kliknete na možnost Zavřít.
2. V **Průzkumník řešení**klikněte pravým tlačítkem myši na název webové aplikace (v tomto kurzu je název aplikace **BasicWebSite**) a pak klikněte na **Přidat** -&gt; **novou položku**.   
Zobrazí se dialogové okno **Přidat novou položku** .
3. Na levé straně vyberte skupinu **Visual C#**  -&gt; **Web** Templates. Pak v prostředním seznamu vyberte **webový formulář** a pojmenujte ho *FirstWebPage. aspx*.   
    Dialogové okno ![přidat novou položku](creating-a-basic-web-forms-page/_static/image6.png)
4. Kliknutím na tlačítko **Přidat** přidejte webovou stránku do projektu.  
Visual Studio vytvoří novou stránku a otevře ji.

### <a name="adding-html-to-the-page"></a>Přidání kódu HTML na stránku

V této části návodu přidáte na stránku nějaký statický text.

### <a name="to-add-text-to-the-page"></a>Přidání textu na stránku

1. V dolní části okna dokumentu klikněte na kartu **Návrh** a přepněte se na zobrazení **návrhu** .

    Zobrazení Návrh zobrazí aktuální stránku v podobě podobným způsobem. V tomto okamžiku nemáte na stránce žádný text ani ovládací prvky, takže je stránka prázdná s výjimkou přerušované čáry, která obchází obdélník. Tento obdélník představuje element **div** na stránce.
2. Klikněte dovnitř obdélníku, který je ohraničen čárkovanou čárou.
3. Zadejte **Vítá vás Visual Web Developer** a dvakrát stiskněte klávesu **ENTER** .

    Následující ilustrace znázorňuje text, který jste zadali v **návrhovém** zobrazení.

    ![Uvítací text v zobrazení Návrh](creating-a-basic-web-forms-page/_static/image7.png "Uvítací text v zobrazení Návrh")
4. Přepněte do zobrazení **zdroje** .

    KÓD HTML můžete zobrazit ve **zdrojovém** zobrazení, které jste vytvořili při psaní v **návrhovém** zobrazení.  
    ![webové stránky se statickým textem](creating-a-basic-web-forms-page/_static/image8.png)

### <a name="running-the-page"></a>Spuštění stránky

Než budete pokračovat přidáním ovládacích prvků na stránku, můžete ji nejprve spustit.

### <a name="to-run-the-page"></a>Spuštění stránky

1. V **Průzkumník řešení**klikněte pravým tlačítkem na *FirstWebPage. aspx* a vyberte **nastavit jako úvodní stránku**.
2. Stisknutím **kombinace kláves CTRL + F5** stránku spusťte.

    Stránka se zobrazí v prohlížeči. I když stránka, kterou jste vytvořili, má příponu názvu souboru *. aspx*, která se aktuálně spouští jako jakákoli stránka HTML.

    Pokud chcete zobrazit stránku v prohlížeči, můžete také kliknout pravým tlačítkem na stránku v **Průzkumník řešení** a vybrat **Zobrazit v prohlížeči**.
3. Zavřete prohlížeč a zastavte webovou aplikaci.

## <a name="adding-and-programming-controls"></a>Přidávání a programování ovládacích prvků

<a id="sectionToggle1"></a>

Nyní na stránku přidáte serverové ovládací prvky. Serverové ovládací prvky, jako jsou tlačítka, popisky, textová pole a další známé ovládací prvky, poskytují typické možnosti zpracování formulářů pro stránky webových formulářů. Můžete však programovat ovládací prvky s kódem, který je spuštěn na serveru, nikoli klientem.

Přidáte ovládací prvek [tlačítko](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) , ovládací prvek [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) a ovládací prvek [popisek](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) na stránku a napíšete kód, který bude zpracovávat událost [kliknutí](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) pro ovládací prvek [tlačítko](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) .

### <a name="to-add-controls-to-the-page"></a>Přidání ovládacích prvků na stránku

1. Klikněte na kartu **Návrh** a přepněte se do zobrazení **Návrh** .
2. Umístěte kurzor na konec **uvítacího textu aplikace Visual Web Developer** a stisknutím klávesy **ENTER** pětkrát nebo vícekrát uvolněte místo v poli elementu **div** .
3. V **sadě nástrojů**rozbalte **standardní** skupinu, pokud ještě není rozbalená.  
Všimněte si, že možná budete muset rozbalit okno **panelu nástrojů** na levé straně a zobrazit ho.
4. Přetáhněte ovládací prvek [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) na stránku a přetáhněte jej uprostřed pole **div** , které má na prvním řádku **Vítejte Visual Web Developer** .
5. Přetáhněte na stránku ovládací prvek [tlačítko](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) a umístěte jej napravo od ovládacího prvku [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) .
6. Přetáhněte ovládací prvek [popisek](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) na stránku a přetáhněte jej na samostatný řádek pod ovládací prvek [tlačítko](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) .
7. Umístěte kurzor nad ovládací prvek [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) a pak zadejte **Zadejte název:** .

    Tento statický text HTML je titulek ovládacího prvku [TextBox](https://msdn.microsoft.com/library/system.web.ui.webcontrols.textbox.aspx) . Můžete kombinovat statické ovládací prvky HTML a serveru na stejné stránce. Následující obrázek ukazuje, jak se tři ovládací prvky zobrazí v zobrazení **Návrh** .

    ![Tři ovládací prvky v zobrazení Návrh](creating-a-basic-web-forms-page/_static/image9.png "Tři ovládací prvky v zobrazení Návrh")

### <a name="setting-control-properties"></a>Nastavení vlastností ovládacího prvku

Sada Visual Studio nabízí různé způsoby, jak nastavit vlastnosti ovládacích prvků na stránce. V této části návodu nastavíte vlastnosti v zobrazení **Návrh** i ve **zdrojovém** zobrazení.

### <a name="to-set-control-properties"></a>Nastavení vlastností ovládacího prvku

1. Nejprve zobrazte okna **vlastností** výběrem z nabídky **zobrazení** –&gt; -**okno vlastností**&gt; **Windows** . Případně můžete vybrat **F4** , chcete-li zobrazit okno **vlastnosti** .
2. Vyberte ovládací prvek [tlačítko](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) a potom v okně **vlastnosti** nastavte hodnotu **text** na **zobrazované jméno**. Text, který jste zadali, se zobrazí na tlačítku v návrháři, jak je znázorněno na následujícím obrázku.

    ![Nastavit text tlačítka](creating-a-basic-web-forms-page/_static/image10.png "Nastavit text tlačítka")
3. Přepněte do zobrazení **zdroje** .

    Zobrazení **zdroje** zobrazuje HTML stránky, včetně prvků, které aplikace Visual Studio vytvořila pro serverové ovládací prvky. Ovládací prvky jsou deklarovány pomocí syntaxe podobné formátu HTML s tím rozdílem, že značky používají předponu **ASP:** a zahrnují atribut **runat =&quot;Server&quot;** .

    Vlastnosti ovládacího prvku jsou deklarovány jako atributy. Například pokud nastavíte vlastnost [text](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.text.aspx) pro ovládací prvek [tlačítko](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) , v kroku 1 jste nastavili **textový** atribut v označení ovládacího prvku.

    > [!NOTE] 
    > 
    > Všechny ovládací prvky jsou uvnitř prvku **formuláře** , který má také atribut **runat =&quot;Server&quot;** . Atribut **runat =&quot;server&quot;** a **ASP:** prefix ovládacího prvku označí ovládací prvky tak, aby byly zpracovány pomocí ASP.NET na serveru při spuštění stránky. Kód mimo **&lt;formuláře runat =&quot;server&quot;&gt;** a **&lt;skriptu runat =&quot;Server&quot;&gt;** prvky se nemění do prohlížeče, což je důvod, proč kód ASP.NET musí být uvnitř elementu. jehož počáteční značka obsahuje atribut **runat =&quot;server&quot;** .
4. V dalším kroku přidáte k ovládacímu prvku [popisek](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) další vlastnost. Umístěte kurzor přímo po **ASP: Label** do značky **&lt;asp: Label&gt;** a stiskněte **MEZERNÍK**.

    Zobrazí se rozevírací seznam, ve kterém se zobrazí seznam dostupných vlastností, které můžete nastavit pro ovládací prvek [popisek](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) . Tato funkce, která se označuje jako **IntelliSense**, pomáhá v zobrazení **zdroje** s syntaxí serverových ovládacích prvků, prvků HTML a dalších položek na stránce. Následující ilustrace znázorňuje rozevírací seznam **technologie IntelliSense** pro ovládací prvek [popisek](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) .

    ![Technologie IntelliSense – atributy](creating-a-basic-web-forms-page/_static/image11.png "Technologie IntelliSense – atributy")
5. Vyberte **ForeColor** a pak zadejte symbol rovná se.

    IntelliSense zobrazí seznam barev.

    > [!NOTE] 
    > 
    > Rozevírací seznam **technologie IntelliSense** lze kdykoli zobrazit stisknutím **kombinace kláves CTRL + J** při zobrazení kódu.
6. Vyberte barvu pro text ovládacího prvku **[popisek](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx)** . Ujistěte se, že jste vybrali barvu, která je dostatečně tmavá pro čtení s bílým pozadím.

    Atribut **ForeColor** se dokončí barvou, kterou jste vybrali, včetně pravé uvozovky.

### <a name="programming-the-button-control"></a>Programování ovládacího prvku tlačítko

Pro tento návod budete psát kód, který přečte název, který uživatel zadá do textového pole, a pak zobrazí název v ovládacím prvku [popisek](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) .

### <a name="add-a-default-button-event-handler"></a>Přidání obslužné rutiny události výchozího tlačítka

1. Přepněte do zobrazení **návrhu** .
2. Dvakrát klikněte na ovládací prvek [tlačítko](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) .

    Ve výchozím nastavení Visual Studio přepne do souboru kódu na pozadí a vytvoří kostru obslužné rutiny události pro výchozí událost ovládacího prvku [tlačítko](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) , událost [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) . Soubor kódu na pozadí odděluje kód vašeho uživatelského rozhraní (například HTML) od vašeho serverového kódu (například C#).   
   Kurzor je umístěn pro přidání kódu pro tuto obslužnou rutinu události.

    > [!NOTE] 
    > 
    > Dvojité kliknutí na ovládací prvek v zobrazení **Návrh** je jedním z několika způsobů, jak můžete vytvořit obslužné rutiny událostí.
3. Uvnitř **\_klikněte na** obslužnou rutinu události, zadejte **Label1** následovaný tečkou ( **.** ).

    Když zadáte období po **identifikátoru** popisku (**Label1**), Visual Studio zobrazí seznam dostupných členů pro ovládací prvek [popisek](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) , jak je znázorněno na následujícím obrázku. Člen běžně vlastnost, metodu nebo událost.

    ![IntelliSense v zobrazení kódu](creating-a-basic-web-forms-page/_static/image12.png "IntelliSense v zobrazení kódu")
4. Dokončete obslužnou rutinu události **Click** pro tlačítko tak, aby vypadala tak, jak je znázorněno v následujícím příkladu kódu.

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample1.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample2.vb?highlight=2)]
5. Přepněte zpět na zobrazení **zdrojového** kódu HTML kliknutím pravým tlačítkem myši na *FirstWebPage. aspx* v **Průzkumník řešení** a výběrem **Zobrazit značky**.
6. Posuňte se na **&lt;ASP: tlačítko&gt;** elementu. Všimněte si, že **&lt;ASP: tlačítko&gt;** elementu teď má atribut **Click =&quot;Button1\_klikněte na&quot;** .

    Tento atribut váže událost [Click](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) tlačítka k metodě obslužné rutiny, kterou jste si pokódujíi v předchozím kroku.

    Metody obslužné rutiny událostí mohou mít libovolný název; název, který se zobrazí, je výchozí název vytvořený v aplikaci Visual Studio. Důležité je, že název použitý pro atribut při **kliknutí** v HTML se musí shodovat s názvem metody definované v kódu na pozadí.

### <a name="running-the-page"></a>Spuštění stránky

Nyní můžete testovat ovládací prvky serveru na stránce.

### <a name="to-run-the-page"></a>Spuštění stránky

1. Stisknutím **kombinace kláves CTRL + F5** spusťte stránku v prohlížeči. Pokud dojde k chybě, proveďte znovu kontrolu výše uvedených kroků.
2. Do textového pole zadejte název a klikněte na tlačítko **Zobrazit název** .

    Název, který jste zadali, se zobrazí v ovládacím prvku [popisek](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) . Všimněte si, že po kliknutí na tlačítko se stránka publikuje na webovém serveru. ASP.NET pak znovu vytvoří stránku, spustí váš kód (v tomto případě se spustí obslužná rutina události [kliknutí na](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.click.aspx) ovládací prvek [tlačítko](https://msdn.microsoft.com/library/system.web.ui.webcontrols.button.aspx) ) a poté pošle novou stránku do prohlížeče. Pokud sledujete stavový řádek v prohlížeči, vidíte, že se stránka při každém kliknutí na tlačítko na webový server dohlásí.
3. V prohlížeči zobrazte zdroj stránky, kterou používáte, kliknutím pravým tlačítkem myši na stránku a výběrem možnosti **Zobrazit zdroj**.

    Ve zdrojovém kódu stránky vidíte kód HTML bez jakéhokoli kódu serveru. Konkrétně se nezobrazuje **&lt;ASP:&gt;** prvky, se kterými jste pracovali ve **zdrojovém** zobrazení. Při spuštění stránky ASP.NET zpracuje ovládací prvky serveru a vykresluje prvky HTML na stránku, která provádí funkce, které reprezentují ovládací prvek. Například **&lt;ASP: tlačítko&gt;** ovládací prvek je vykreslen jako **Typ vstupu&lt;HTML =&quot;odeslat&quot;&gt;** elementu.
4. Zavřete prohlížeč.

## <a name="working-with-additional-controls"></a>Práce s dalšími ovládacími prvky

<a id="sectionToggle2"></a>

V této části návodu budete pracovat s ovládacím prvkem [Kalendář](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) , který zobrazuje data v měsíci v čase. Ovládací prvek [Kalendář](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) je složitější ovládací prvek než tlačítko, textové pole a popisek, se kterými jste pracovali, a znázorňuje některé další možnosti serverových ovládacích prvků.

V této části přidáte do stránky ovládací prvek [System. Web. UI. WebControls. Calendar](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) a naformátujete ho.

### <a name="to-add-a-calendar-control"></a>Přidání ovládacího prvku kalendáře

1. V aplikaci Visual Studio přepněte do zobrazení **Návrh** .
2. V části **standardní** v **sadě nástrojů**přetáhněte ovládací prvek [Kalendář](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) na stránku a přetáhněte jej pod element **div** , který obsahuje další ovládací prvky.

    Zobrazí se panel inteligentních značek kalendáře. Na panelu se zobrazí příkazy, které usnadňují provádění nejběžnějších úloh pro vybraný ovládací prvek. Následující ilustrace znázorňuje ovládací prvek [Kalendář](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) , který je vykreslený v **návrhovém** zobrazení.

    ![Ovládací prvek Calendar v zobrazení Návrh](creating-a-basic-web-forms-page/_static/image13.png "Ovládací prvek Calendar v zobrazení Návrh")
3. Na panelu inteligentních značek vyberte možnost **automaticky formátovat**.

    Zobrazí se dialogové okno **Automatické formátování** , které umožňuje výběr schématu formátování kalendáře. Na následujícím obrázku je znázorněno dialogové okno **Automatické formátování** pro ovládací prvek [Kalendář](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) .

    ![Dialogové okno Automatické formátování (ovládací prvek kalendáře)](creating-a-basic-web-forms-page/_static/image14.png "Dialogové okno Automatické formátování (ovládací prvek kalendáře)")
4. V seznamu **Vyberte schéma** vyberte možnost **jednoduché** a pak klikněte na tlačítko **OK**.
5. Přepněte do zobrazení **zdroje** .

    Můžete vidět&lt;prvku **ASP:&gt;kalendáře** . Tento prvek je mnohem delší než prvky pro jednoduché ovládací prvky, které jste vytvořili dříve. Obsahuje také dílčí prvky, například **&lt;WeekEndDayStyle&gt;** , které reprezentují různá nastavení formátování. Následující ilustrace znázorňuje ovládací prvek [kalendáře](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) v zobrazení **zdroje** . (Přesný kód, který vidíte v zobrazení **zdroje** , se může mírně lišit od obrázku.)

    ![Ovládací prvek Kalendář v zobrazení zdroje](creating-a-basic-web-forms-page/_static/image15.png "Ovládací prvek Kalendář v zobrazení zdroje")

### <a name="programming-the-calendar-control"></a>Programování ovládacího prvku kalendáře

V této části nakonfigurujete ovládací prvek [Kalendář](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) k zobrazení aktuálně vybraného data.

### <a name="to-program-the-calendar-control"></a>Programové řízení kalendáře

1. V zobrazení **Návrh** dvakrát klikněte na ovládací prvek [Kalendář](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) .

    Vytvoří se nová obslužná rutina události, která se zobrazí v souboru kódu na pozadí s názvem *FirstWebPage.aspx.cs*.
2. Dokončete obslužnou rutinu události [SelectionChanged](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.selectionchanged.aspx) s následujícím kódem.

    [!code-csharp[Main](creating-a-basic-web-forms-page/samples/sample3.cs?highlight=3)]

    [!code-vb[Main](creating-a-basic-web-forms-page/samples/sample4.vb?highlight=2)]

    Výše uvedený kód nastaví text ovládacího prvku popisek na vybrané datum ovládacího prvku Kalendář.

### <a name="running-the-page"></a>Spuštění stránky

Nyní můžete kalendář otestovat.

### <a name="to-run-the-page"></a>Spuštění stránky

1. Stisknutím **kombinace kláves CTRL + F5** spusťte stránku v prohlížeči.
2. Klikněte na datum v kalendáři.

    Datum, na které jste klikli, se zobrazí v ovládacím prvku [popisek](https://msdn.microsoft.com/library/system.web.ui.webcontrols.label.aspx) .
3. V prohlížeči zobrazte zdrojový kód stránky.

    Všimněte si, že ovládací prvek [Kalendář](https://msdn.microsoft.com/library/system.web.ui.webcontrols.calendar.aspx) byl vykreslen na stránku jako **tabulka**a každý den jako prvek **td** .
4. Zavřete prohlížeč.

## <a name="next-steps"></a>Další kroky

<a id="nextStepsToggle"></a>

Tento návod znázornil základní funkce návrháře stránky sady Visual Studio. Teď, když jste se seznámili s vytvářením a úpravou stránky webových formulářů v aplikaci Visual Studio, můžete chtít prozkoumat další funkce. Například můžete chtít provést následující akce:

- Další informace o webových formulářích ASP.NET najdete v podrobných kurzech kurzu [Začínáme s webovými formuláři ASP.NET 4,5 a Visual Studio 2013](getting-started-with-aspnet-45-web-forms/introduction-and-overview.md).
- Přečtěte si další informace o kaskádových šablonách stylů (CSS). Podrobnosti najdete v tématu [práce s CSS – přehled](https://msdn.microsoft.com/library/bb398931.aspx).

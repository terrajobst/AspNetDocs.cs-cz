---
uid: web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
title: Použití funkce Page Inspector pro Visual Studio 2012 ve webových formulářích ASP.NET | Microsoft Docs
author: rick-anderson
description: Page Inspector for Visual Studio 2012 je nástroj pro vývoj webu s integrovaným prohlížečem. Vyberte libovolný prvek v integrovaném prohlížeči a klikněte na tlačítko inspektor stránky...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: 2ece0bf4-aae5-4ff4-8f62-28e0819d4f86
msc.legacyurl: /web-forms/overview/getting-started/using-page-inspector-in-a-visual-studio-11-beta-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: c165bbea505b4cb8eae1312cdd587f4ed36541a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78575920"
---
# <a name="using-page-inspector-for-visual-studio-2012-in-aspnet-web-forms"></a>Použití Page Inspectoru pro Visual Studio 2012 ve webových formulářích ASP.NET

pomocí Tim Ammann

> Page Inspector for Visual Studio 2012 je nástroj pro vývoj webu s integrovaným prohlížečem. Vyberte libovolný prvek v integrovaném prohlížeči a kontrolor stránky okamžitě zvýrazní zdroj a šablonu stylů CSS elementu. Můžete procházet libovolnou stránku aplikace, rychle najít zdroje vykresleného kódu a použít nástroje prohlížeče přímo v prostředí sady Visual Studio.
> 
> V tomto kurzu se dozvíte, jak povolit režim kontroly a pak rychle vyhledat a upravit pravidla a text šablon stylů CSS v rámci webového projektu. V tomto kurzu se používá projekt aplikace Web Forms, ale můžete také použít nástroj Page Inspector pro webové projekty a aplikace [MVC](https://go.microsoft.com/?linkid=9802002) .
> 
> V tomto kurzu najdete následující oddíly:
> 
> [Požadavky](#_1_prerequisites)
> 
> [Vytvoření webové aplikace](#_2_creating_a)
> 
> [Použití nástroje Page Inspector k zobrazení aplikace](#_3_using_page)
> 
> [Povolit režim kontroly](#_4_inspection_mode)
> 
> [Použití inspektoru stránky k provádění změn značek](#_5_using_page)
> 
> [Režim kontroly a okno HTML](#_6_inspection_mode)
> 
> [Náhled změn CSS v okně styly](#_7_previewing_css)
> 
> [Automatická synchronizace šablon stylů CSS](#css_auto_sync)
> 
> [Použití ovládacího prvku pro výběr barvy CSS](#css_color_picker)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a>Předpoklady

- [Visual Studio 2012](https://www.microsoft.com/visualstudio/11) nebo [Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/11/downloads#express-web).

> [!NOTE]
> Pokud chcete získat nejnovější verzi nástroje Page Inspector, nainstalujte pomocí [instalačního programu webové platformy](https://go.microsoft.com/fwlink/?LinkId=255386) sadu Azure SDK pro .NET 2,0.

Funkce Page Inspector je zabalené pomocí Microsoft Web Developer Tools. Nejnovější verze je 1,3. Chcete-li zjistit, kterou verzi máte, spusťte aplikaci Visual Studio a v nabídce **help** vyberte **o Microsoft Visual Studio** .

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a>Vytvoření webové aplikace

Nejprve vytvoříte webovou aplikaci, kterou použijete inspektor stránky s nástrojem. V aplikaci Visual Studio vyberte **soubor** &gt; **Nový projekt**. Na levé straně rozbalte **C#vizuál**, vyberte **Web**a pak vyberte **ASP.NET Web Forms aplikace**.

![Nová aplikace webového formuláře](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image1.png)

Klikněte na tlačítko **OK**.

Aplikace se otevře v zobrazení **zdroje** .

![Nová aplikace webových formulářů v zobrazení zdroje](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image2.png)

Teď, když máte aplikaci, se kterou pracujete, můžete ji zkontrolovat a upravit pomocí nástroje Page Inspector.

<a id="_starting_page_inspector"></a><a id="_3_starting_page"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-view-the-application"></a>Použití nástroje Page Inspector k zobrazení aplikace

V dalším kroku zobrazíte aplikaci s nástrojem Page Inspector. V **Průzkumník řešení**klikněte pravým tlačítkem na projekt a pak zvolte **Zobrazit v okně Kontrola stránky**.

![Zobrazit v inspektoru stránky](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image3.png)

Ve výchozím nastavení je při prvním spuštění nástroje pro kontrolu stránky ukotveno jako úzké okno na levé straně prostředí sady Visual Studio. Ponechte ukotvenou na levé straně a nastavte ji na požadovanou šířku, nebo ji ukotvěte do jedné z oblastí nástrojů nahoře, dole nebo vpravo:

![Ukotvené pozice inspektoru stránky](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image4.png)

Pokud zrušíte ukotvení okna inspektoru stránky, můžete ho umístit mimo Visual Studio, nebo i na druhý monitor, pokud ho máte. Pokud však chcete ALT + TAB mezi nástrojem Page Inspector a Visual Studio, když je okno Inspektor stránky neukotveno, přejdete do části **nástroje** &gt; **možnosti** &gt; **prostředí** &gt; **karty a okna**a v části **dobře**zaškrtnete zaškrtnutí políčka s **plovoucími okny nástrojů vždy v horní části hlavního okna**:

![Zrušte zaškrtnutí políčka plovoucího nástroje okna v systému Windows ALT + TAB mezi Visual Studio a oknem neukotvené kontroly stránky.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image5.png)

V horním podokně okna inspektor stránky se zobrazuje aktuální stránka v okně prohlížeče. Dolní podokno zobrazuje stránku v kódu HTML vlevo a některé karty na pravé straně, které umožňují kontrolu různých aspektů stránky. Dolní podokno se podobá [vývojářské nástroje F12](https://msdn.microsoft.com/ie/aa740478) v Internet Exploreru. (Na rozdíl od vývojářských nástrojů můžete použít inspektor stránky přímo v rámci sady Visual Studio.)

![Inspektor stránek](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image6.png)

V tomto kurzu použijete podokno Prohlížeč Inspector stránky a kartu **HTML** a **styly** , které vám pomůžou rychle procházet a dělat změny aplikace.

<a id="_4_inspection_mode"></a>
## <a name="enable-inspection-mode"></a>Povolit režim kontroly

V dalším kroku se zobrazí, jak funguje kontrolní režim nástroje Page Inspector. V okně Inspektor stránky klikněte na tlačítko **prozkoumat** .

![Kontrola elementu](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image7.png)

Chcete-li zobrazit kontrolní režim v akci, přesuňte ukazatel myši na různé části stránky v okně prohlížeče inspektoru stránky. V takovém případě se ukazatel myši změní na velké znaménko plus a element pod je zvýrazněný:

![Najetí myší na div. Content-wrapper](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image8.png)

Při přesunutí ukazatele myši Pamatujte na to, že

- Obsah ve zobrazení **zdroje** se změní, aby se zobrazil kód odpovídající vybranému prvku na stránce. Relevantní označení je zvýrazněno. Pokud je zdroj v jiném souboru, tento soubor je otevřen v zobrazení zdroje s zvýrazněným odpovídajícím kódem.

- Značka zobrazená na kartě **HTML** v inspektoru stránky se také změní, aby odpovídala vybranému prvku na stránce. Na kartě **HTML** jsou relevantní značky poznačené.

- Karta **styly** zobrazuje pravidla šablon stylů CSS vztahující se k aktuálnímu výběru.

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a>Použití inspektoru stránky k provádění změn značek

Nyní uvidíte, jak můžete pomocí inspektora stránky vyhledat a změnit značky nebo text, jehož umístění nemusí být okamžitě zřejmé.

Umístěte inspektor stránky v režimu kontroly a potom přejděte k dolnímu okraji domovské stránky.

Jakmile zadáte oblast s zápatím, zobrazí se v okně zobrazení **zdroje** na dočasnou kartě na pravé straně stránky rozložení *Web. Master* a zvýrazní se část stránky předlohy, kterou jste vybrali. Tím se dozvíte, jak může inspektor stránky najít a zobrazit obsah na stránce, která může být skutečně popsána z jiného souboru, než ze kterého jste původně otevřeli.

![Zvýraznění zápatí v režimu kontroly](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image9.png)

V okně prohlížeče inspektora stránky přesuňte ukazatel myši na řádek s oznámením o autorských <a id="a"> </a>právech.

Na stránce *site. Master* se zvýrazní odpovídající řádek.

![Zvýrazněný řádek copyrightu pro zápatí](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image10.png)

Přidejte nějaký text na konec řádku v souboru *Web. Master* .

&lt;p&gt;&amp;kopie; &lt;%: DateTime. Now. Year%&gt; – moje aplikace ASP.NET Rocks.&lt;/p&gt;

Nyní stiskněte kombinaci kláves CTRL + ALT + ENTER nebo kliknutím na panel aktualizace zobrazte výsledky v okně prohlížeče inspektoru stránky.

![Moje aplikace ASP.NET Rocks!](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image11.png)

Možná jste si mysleli, že se zápatí nacházelo na stránce *Default. aspx* , ale že je na stránce rozložení stránky hlavní, ale jeho vzhled byl za vás.

<a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a>Režim kontroly a okno HTML

V dalším kroku budete mít rychlý přehled o okně HTML a o tom, jak mapuje prvky pro vás.

Umístit inspektor stránky v režimu kontroly.

![Kontrola elementu](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image12.png)

Klikněte na horní část stránky s textem "vaše logo". Podrobněji prozkoumáte konkrétní prvek, takže zobrazení v okně prohlížeče se již nemění při přesunutí ukazatele myši.

Nyní přesuňte ukazatel myši do okna **HTML** . Když přesunete ukazatel myši, inspektor stránky popisuje prvek v okně **HTML** a zvýrazní odpovídající prvek v okně prohlížeče.

![Okno HTML](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image13.png)

Stejně jako dřív se otevře okno *site. Master* na dočasné kartě. klikněte na kartu Web. Master a v záhlaví &lt;&gt; oddílu se zvýrazní odpovídající kód:

![Zvýrazněný kód](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image14.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a>Náhled změn CSS v okně styly

Dále uvidíte, jak můžete pomocí okna **styly** kontroly stránky zobrazit náhled změn v šablonách stylů CSS.

Kliknutím na tlačítko **zkontrolovat** můžete umístit inspektora stránky v režimu kontroly.

V okně prohlížeče inspektora stránky přesuňte ukazatel myši na domovskou stránku, dokud se nezobrazí popisek **div. Content-wrapper** .

![Najetí myší na elementy](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image15.png)

Jednou klikněte v části div. Content-wrapper a pak přesuňte ukazatel myši do okna **styly** . V selektoru třídy. Doporučené. obsah-obálka zrušte zaškrtnutí políčka a zaškrtněte políčko u vlastnosti Barva pozadí.

![Vymazat barvu pozadí](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image16.png)

Všimněte si, jak se zobrazí náhled změny v okně prohlížeče inspektoru stránky.

Zaškrtněte políčko znovu, potom dvakrát klikněte na hodnotu vlastnosti a změňte ji na `red`. Tato změna se zobrazí okamžitě:

![Barva červeného pozadí](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image17.png)

Okno **styly** usnadňuje testování a náhled změn CSS před potvrzením změn v samotné šabloně stylů.

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a>Automatická synchronizace šablon stylů CSS

> [!NOTE]
> Tato funkce vyžaduje verzi 1,3 ovládacího prvku Page Inspector.

Funkce automatické synchronizace šablon stylů CSS umožňuje přímo upravit soubor CSS a okamžitě zobrazit změny v prohlížeči kontroly stránky.

Kliknutím na tlačítko **zkontrolovat** umístěte inspektor stránky do režimu kontroly.

V prohlížeči Inspector stránky přesuňte ukazatel myši nad oddíl "Domovská stránka", dokud se nezobrazí popisek **div. Content-wrapper** . Klikněte jednou pro výběr tohoto prvku.

Okno **styly** zobrazuje všechna pravidla šablony stylů CSS pro tento element. Přejděte dolů a najděte selektor třídy. Doporučené. Content-wrapper. Klikněte na ". Doporučené. obsah-obálka". Page Inspector otevře soubor CSS, který definuje tento styl (Web. CSS) a zvýrazní odpovídající styl CSS.

![Soubor CSS](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image18.png)

Nyní změňte hodnotu `background-color` na "Red". Tato změna se zobrazí okamžitě v prohlížeči Inspector stránky.

![Prohlížeč Inspector stránky](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image19.png)

<a id="css_color_picker"></a>

## <a name="using-the-css-color-picker"></a>Použití ovládacího prvku pro výběr barvy CSS

V dalším kroku se dozvíte, jak pomocí nástroje Page Inspector rychle najít a změnit šablonu stylů CSS zvýrazněného textu ve výchozí aplikaci. V tomto příkladu jste se rozhodli, že se vám nelíbí modrý zvýraznění a chcete ho změnit na jinou barvu.

Klikněte na tlačítko **prozkoumat** .

![Kontrola elementu](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image20.png)

V okně prohlížeče inspektora stránky přesuňte ukazatel myši na zvýrazněné "videa, kurzy a ukázky" tak, aby se zobrazil popisek CSS "značka".

![Najetí myší na element značky](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image21.png)

Klikněte na text, který chcete vybrat. Odpovídající selektor značek CSS se zobrazí v dolní části okna **styly** .

![označit selektor v okně styly](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image22.png)

Klikněte na selektor značek. Tím se otevře soubor *site. CSS* pro webovou aplikaci. Klikněte na kartu Web. CSS a zvýrazní se odpovídající šablona stylů CSS pro selektor:

![Označte selektor v šabloně stylů.](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image23.png)

Vyberte a odeberte čáru s vlastností background-color.

Nyní použijete nový výběr barvy CSS sady Visual Studio 2012 k výběru nové barvy vlastnosti Barva pozadí **značky** .

<a id="_using_the_visual"></a>

### <a name="using-the-visual-studio-2012-css-color-picker"></a>Použití výběru barvy CSS sady Visual Studio 2012

Editor CSS v aplikaci Visual Studio 2012 má výběr barvy, který usnadňuje výběr a vložení barev. Má jednoduchý pruh barev a "rozbalovací" výběr, který nabízí lepší kontrolu.

Výběr barvy obsahuje standardní paletu barev, podporuje standardní názvy barev, kódy hash, RGB, RGBA, HSL a HSLA barvy a udržuje seznam barev, které jste naposledy použili v dokumentu.

Na řádku, kde byla vlastnost background-color, zadejte "BC" a stiskněte šipku dolů.

Když zadáte první znak každého slova ve vlastnosti oddělené spojovníky, například background-color, IntelliSense vyfiltruje seznam, abyste zobrazili pouze vlastnosti, které odpovídají:

![Filtrované hodnoty IntelliSense](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image24.png)

Nyní zadejte dvojtečku. Když to uděláte, bude vložen celý název vlastnosti Barva pozadí. Zadejte **#** nebo **RGB (** a zobrazí se panel pro výběr barvy:

![Panel pro výběr barvy CSS](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image25.png)

Chcete-li zjistit, jak panel pro výběr barvy funguje, klikněte na jeho barvy ukazatelem myši, nebo stiskněte klávesu šipka dolů a pak použijte šipky vlevo a vpravo k procházení barev. Při návštěvě barvy se zobrazí náhled odpovídající hodnoty vlastnosti background-color:

![Náhled hodnoty vlastnosti background-color](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image26.png)

V tomto okamžiku můžete stisknutím klávesy Enter vybrat hodnotu a potom středníku (;) k dokončení položky šablony stylů CSS. Prozatím přejděte k další části, abyste viděli, jak funguje automaticky otevírané okno pro výběr barvy.

#### <a name="using-the-color-picker-pop-down"></a>Použití rozbalovací nabídky pro výběr barvy

Když pruh barev nemá přesnou barvu, kterou hledáte, můžete použít rozevírací nabídka pro výběr barvy.

Chcete-li jej otevřít, klikněte na dvojitou dvojitou šipku na pravém konci pruhu barev nebo na klávesnici stiskněte šipku dolů nebo dvakrát.

![Místní nabídka pro výběr barvy CSS](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image27.png)

Klikněte na barvu ze svislého pruhu na pravé straně. Tím se v hlavním okně zobrazí barevný přechod pro tuto barvu. Vyberte barvu přímo ze svislého pruhu stisknutím klávesy ENTER nebo kliknutím na libovolný bod v hlavním okně vyberte s větší přesností.

Pokud je na obrazovce počítače barva, kterou chcete použít (nemusí být uvnitř uživatelského rozhraní sady Visual Studio), můžete zachytit její hodnotu pomocí nástroje kapátka v pravém dolním rohu.

Můžete také změnit neprůhlednost barvy přesunutím posuvníku v dolní části výběru barvy. Tím se změní hodnoty barev na hodnoty RGBA, protože formát RGBA může představovat neprůhlednost.

Po zvolení barvy stiskněte klávesu ENTER a zadáním středníku dokončete položku pozadí-Color v souboru *site. CSS* .

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a>Panel aktualizace inspektoru stránky

Funkce Page Inspector okamžitě rozpozná změnu v souboru *Web. CSS* (nebo do libovolného souboru v aplikaci) a zobrazí výstrahu na panelu aktualizace.

![Aktualizovat panel](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image28.png)

Chcete-li uložit všechny soubory a aktualizovat prohlížeč kontroly stránky, stiskněte klávesy CTRL + ALT + ENTER nebo klikněte na panel aktualizace. Změna barvy zvýraznění se zobrazí v prohlížeči:

![Barva zvýraznění změněna](using-page-inspector-in-a-visual-studio-11-beta-web-forms-project/_static/image29.png)

<a id="_using_page_inspector_1"></a>Všimněte si, že jste pohodlně aktualizovali prohlížeč inspektoru stránky přímo z prostředí sady Visual Studio. Použití nástroje Page Inspector místo externího prohlížeče vám umožní zůstat v editoru při vývoji webových aplikací.

## <a name="see-also"></a>Viz také

[Úvod do inspektoru stránky](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector) (video pro kanál 9)

[Chybové zprávy v inspektoru stránky](https://go.microsoft.com/?linkid=9813062) (MSDN)

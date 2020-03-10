---
uid: mvc/overview/views/using-page-inspector-in-aspnet-mvc
title: Používání funkce Page Inspector v ASP.NET MVC | Microsoft Docs
author: rick-anderson
description: Nástroj Page Inspector v aplikaci Visual Studio 2012 je webovým nástrojem pro vývoj na webu s integrovaným prohlížečem. Vyberte libovolný prvek v integrovaném prohlížeči a klikněte na tlačítko inspektor stránky i...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: c7e4e1ab-4932-4614-9f53-aaf7c706d498
msc.legacyurl: /mvc/overview/views/using-page-inspector-in-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5da3e142c52a770f59222c21d9f9a53cbbdbf498
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538015"
---
# <a name="using-page-inspector-in-aspnet-mvc"></a>Použití Page Inspectoru v ASP.NET MVC

pomocí Tim Ammann

> Nástroj Page Inspector v aplikaci Visual Studio 2012 je webovým nástrojem pro vývoj na webu s integrovaným prohlížečem. Vyberte libovolný prvek v integrovaném prohlížeči a kontrolor stránky okamžitě zvýrazní zdroj a šablonu stylů CSS elementu. Můžete procházet libovolné zobrazení MVC, rychle najít zdroje vykreslených značek a použít nástroje prohlížeče přímo v prostředí sady Visual Studio.
> 
> [Přehrát video](../../videos/mvc-4/using-page-inspector-in-aspnet-mvc.md)
> 
> V tomto kurzu se dozvíte, jak povolit režim kontroly a pak rychle vyhledat a upravit značky a šablony stylů CSS v rámci webového projektu. V tomto kurzu se používá projekt MVC, ale můžete také použít nástroj Page Inspector pro [webové formuláře](https://go.microsoft.com/?linkid=9802001) a jiné aplikace ASP.NET.
> 
> V tomto kurzu najdete následující oddíly:
> 
> - [Požadavky](#_1_prerequisites)
> - [Vytvoření webové aplikace](#_2_creating_a)
> - [Použití inspektoru stránky k procházení zobrazení](#_3_using_page)
> - [Povolit režim kontroly](#_4_inspection_mode)
> - [Použití inspektoru stránky k provádění změn značek](#_5_using_page)
> - [Režim kontroly a okno HTML](#_6_inspection_mode)
> - [Náhled změn CSS v okně styly](#_7_previewing_css)
> - [Automatická synchronizace šablon stylů CSS](#css_auto_sync)
> - [Použití ovládacího prvku pro výběr barvy CSS](#css_color_picker)
> - [Mapování dynamických prvků stránky na JavaScript](#map_dynamic_elements)

<a id="_prerequisites"></a><a id="_1_prerequisites"></a>

## <a name="prerequisites"></a>Předpoklady

- [Visual Studio 2012](https://www.microsoft.com/visualstudio/11) nebo [Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/11/downloads#express-web).

> [!NOTE]
> Pokud chcete získat nejnovější verzi nástroje Page Inspector, nainstalujte sadu Windows Azure SDK pro .NET 2,0 pomocí [instalačního programu webové platformy](https://go.microsoft.com/fwlink/?LinkId=255386) .

Funkce Page Inspector je zabalené pomocí Microsoft Web Developer Tools. Nejnovější verze je 1,3. Chcete-li zjistit, kterou verzi máte, spusťte aplikaci Visual Studio a v nabídce **help** vyberte **o Microsoft Visual Studio** .

<a id="_creating_a_web"></a><a id="_2_creating_a"></a>

## <a name="create-a-web-application"></a>Vytvoření webové aplikace

Nejprve vytvořte webovou aplikaci, ve které budete používat inspektor stránky. V aplikaci Visual Studio vyberte **soubor** &gt; **Nový projekt**. Na levé straně rozbalte **C#vizuál**, vyberte **Web**a pak vyberte **Webová aplikace ASP.NET MVC4**.

![Nová aplikace ASP.NET MVC](using-page-inspector-in-aspnet-mvc/_static/image2.png)

Klikněte na tlačítko **OK**.

V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte **internetovou aplikaci**. Ponechá **Razor** jako výchozí zobrazovací modul.

![Nový projekt ASP.NET MVC – Internetová aplikace](using-page-inspector-in-aspnet-mvc/_static/image4.png)

Aplikace se otevře v zobrazení **zdroje** .

![Nová aplikace ASP.NET MVC v zobrazení zdroje](using-page-inspector-in-aspnet-mvc/_static/image6.png)

Teď, když máte aplikaci, se kterou pracujete, můžete ji zkontrolovat a upravit pomocí nástroje Page Inspector.

<a id="_starting_page_inspector"></a><a id="_3_using_page"></a>

## <a name="use-page-inspector-to-browse-to-a-view"></a>Použití inspektoru stránky k procházení zobrazení

V aplikaci Visual Studio 2012 můžete kliknout pravým tlačítkem myši na libovolné zobrazení v projektu, vybrat **Zobrazit v okně Kontrola stránky**a obrazovka inspektor stránky poukáže cestu a zobrazí stránku.

V **Průzkumník řešení**rozbalte složku **zobrazení** a pak do **domovské** složky. Klikněte pravým tlačítkem na soubor index. cshtml a **v okně Kontrola stránky vyberte Zobrazit**.

![Zobrazit index. cshtml v inspektoru stránky](using-page-inspector-in-aspnet-mvc/_static/image8.png)

Ve výchozím nastavení je inspektor stránky ukotven jako okno na levé straně prostředí sady Visual Studio. Pokud budete chtít, můžete ho ukotvit jinde nebo zrušit ukotvení okna. Informace naleznete v tématu [How to: uspořádávat and Dock Windows](https://msdn.microsoft.com/library/z4y0hsax.aspx).

V horním podokně okna inspektor stránky se zobrazuje aktuální stránka v okně prohlížeče. Dolní podokno zobrazuje stránku v kódu HTML spolu s některými kartami, které umožňují kontrolovat různé aspekty stránky. Dolní podokno se podobá [vývojářské nástroje F12](https://msdn.microsoft.com/ie/aa740478) v Internet Exploreru.

![Aplikace ASP.NET MVC v inspektoru stránky](using-page-inspector-in-aspnet-mvc/_static/image10.png)

V tomto kurzu použijete kartu **HTML** a **styly** k rychlému procházení a provádění změn v aplikaci.

<a id="_examining_(&quot;decomposing&quot;)_the"></a><a id="_inspection_mode_and"></a><a id="_4_inspection_mode"></a>

## <a name="enableinspection-mode"></a>EnableInspection režim

Chcete-li umístit inspektor stránky do režimu kontroly, klikněte na tlačítko **prozkoumat** . V režimu kontroly, když držíte ukazatel myši v jakékoli části vykreslené stránky, je zvýrazněn odpovídající zdrojový kód nebo kód.

![Přepnout režim kontroly](using-page-inspector-in-aspnet-mvc/_static/image12.png)

Nyní přesuňte ukazatel myši na různé části stránky v rámci nástroje Page Inspector. V takovém případě se ukazatel myši změní na velké znaménko plus a element pod je zvýrazněný:

![Najetí myší na div. Content-wrapper](using-page-inspector-in-aspnet-mvc/_static/image14.png)

Při přesunutí ukazatele myši zvýrazní aplikace Visual Studio odpovídající syntaxe Razor ve zdrojovém souboru. Pokud prvek HTML pochází z jiného zdrojového souboru, Visual Studio automaticky otevře soubor.

V nástroji Page Inspector zobrazuje karta **HTML** kód HTML, který byl vygenerován z syntaxe Razor. Při přesunutí ukazatele myši jsou zvýrazněny prvky HTML. Karta **styly** zobrazuje pravidla šablony stylů CSS pro element.

<a id="_5_using_page"></a>

## <a name="use-page-inspector-to-make-changes-to-markup"></a>Použití inspektoru stránky k provádění změn značek

Page Inspector vám umožní najít značky, jejichž umístění nemusí být zřejmé. Pak můžete značky upravit a zobrazit výsledné změny.

Pokud to chcete vidět, klikněte na **zkontrolovat** a potom se posuňte do dolní části stránky v okně Inspektor stránky.

Při přesunutí ukazatele myši do oblasti zápatí otevře okno Inspektor stránky soubor \_layout. cshtml a zvýrazní část stránky rozložení, kterou jste vybrali. Jak vidíte, zápatí je definováno v souboru rozložení, a ne v samotném zobrazení.

![Dolní](using-page-inspector-in-aspnet-mvc/_static/image16.png)

Nyní přesuňte ukazatel myši na řádek s oznámením o autorských právech <a id="a"> </a>. Na stránce \_layout. cshtml se zvýrazní odpovídající řádek.

![Zvýrazněný řádek copyrightu pro zápatí](using-page-inspector-in-aspnet-mvc/_static/image18.png)

Přidejte nějaký text na konec řádku v souboru \_layout. cshtml.

&lt;p&gt;&amp;kopie; @DateTime.Now.Year – moje aplikace ASP.NET MVC Rocks&lt;/p&gt;

Nyní stiskněte kombinaci kláves CTRL + ALT + ENTER nebo kliknutím na panel aktualizace zobrazte výsledky v okně prohlížeče inspektoru stránky.

![Moje aplikace ASP.NET Rocks!](using-page-inspector-in-aspnet-mvc/_static/image20.png)

Možná jste si mysleli, že se zápatí definované v indexu. cshtml, ale je zavedené v \_layout. cshtml a inspektor stránky ho pro vás našel.

<a id="_inspection_mode_and_1"></a><a id="_6_inspection_mode"></a>

## <a name="inspection-mode-and-the-html-window"></a>Režim kontroly a okno HTML

V dalším kroku budete mít rychlý přehled o okně HTML a o tom, jak mapuje prvky pro vás.

Kliknutím na tlačítko **zkontrolovat** umístěte inspektor stránky do režimu kontroly.

Klikněte na horní část stránky s textem "vaše logo". Podrobněji prozkoumáte konkrétní prvek, takže zobrazení v okně prohlížeče se již nemění při přesunutí ukazatele myši.

Nyní přesuňte ukazatel myši do okna **HTML** . Když přesunete ukazatel myši, inspektor stránky popisuje prvek v okně **HTML** a zvýrazní odpovídající prvek v okně prohlížeče.

![Okno HTML](using-page-inspector-in-aspnet-mvc/_static/image22.png)

Stejně jako předtím otevře okno \_layout. cshtml pro vás na dočasné kartě. klikněte na položku \_layout. cshtml dočasná karta a odpovídající kód se zvýrazní v&gt; části hlavičky &lt;pro vás:

![Zvýrazněný kód](using-page-inspector-in-aspnet-mvc/_static/image24.png)

<a id="_using_page_inspector"></a><a id="_7_previewing_css"></a>

## <a name="preview-css-changes-in-the-styles-window"></a>Náhled změn CSS v okně styly

V dalším kroku použijete okno **styly** kontroly stránky k zobrazení náhledu změn v šablonách stylů CSS.

Kliknutím na tlačítko **zkontrolovat** umístěte inspektor stránky do režimu kontroly.

V okně prohlížeče inspektora stránky přesuňte ukazatel myši na domovskou stránku, dokud se nezobrazí popisek **div. Content-wrapper** .

![Najetí myší na div. Content-wrapper](using-page-inspector-in-aspnet-mvc/_static/image26.png)

Jednou klikněte v části div. Content-wrapper a pak přesuňte ukazatel myši do okna **styly** . Okno **styly** zobrazuje všechna pravidla šablony stylů CSS pro tento element. Přejděte dolů a najděte selektor třídy. Doporučené. Content-wrapper. Nyní zrušte zaškrtnutí políčka u vlastnosti background-color.

![Vymazat barvu pozadí](using-page-inspector-in-aspnet-mvc/_static/image28.png)

Všimněte si, jak se zobrazí náhled změny v okně prohlížeče inspektoru stránky.

Zaškrtněte políčko znovu, potom dvakrát klikněte na hodnotu vlastnosti a změňte ji na červenou. Tato změna se zobrazí okamžitě:

![Barva červeného pozadí](using-page-inspector-in-aspnet-mvc/_static/image30.png)

Okno **styly** usnadňuje testování a náhled změn CSS před potvrzením změn v samotné šabloně stylů.

<a id="css_auto_sync"></a>
## <a name="css-auto-sync"></a>Automatická synchronizace šablon stylů CSS

> [!NOTE]
> Tato funkce vyžaduje verzi 1,3 ovládacího prvku Page Inspector.

Funkce automatické synchronizace šablon stylů CSS umožňuje přímo upravit soubor CSS a okamžitě zobrazit změny v prohlížeči kontroly stránky.

Kliknutím na tlačítko **zkontrolovat** umístěte inspektor stránky do režimu kontroly.

V prohlížeči Inspector stránky přesuňte ukazatel myši nad oddíl "Domovská stránka", dokud se nezobrazí popisek **div. Content-wrapper** . Klikněte jednou pro výběr tohoto prvku.

Okno **styly** zobrazuje všechna pravidla šablony stylů CSS pro tento element. Přejděte dolů a najděte selektor třídy. Doporučené. Content-wrapper. Klikněte na ". Doporučené. obsah-obálka". Page Inspector otevře soubor CSS, který definuje tento styl (Web. CSS) a zvýrazní odpovídající styl CSS.

![](using-page-inspector-in-aspnet-mvc/_static/image32.png)

Nyní změňte hodnotu `background-color` na "Red". Tato změna se zobrazí okamžitě v prohlížeči Inspector stránky.

![](using-page-inspector-in-aspnet-mvc/_static/image34.png)

<a id="css_color_picker"></a>
## <a name="using-the-css-color-picker"></a>Použití ovládacího prvku pro výběr barvy CSS

Editor CSS v aplikaci Visual Studio 2012 má výběr barvy, který usnadňuje výběr a vložení barev. Výběr barvy obsahuje standardní paletu barev, podporuje standardní názvy barev, kódy hash, RGB, RGBA, HSL a HSLA barvy a udržuje seznam barev, které jste naposledy použili v dokumentu.

V předchozí části jste změnili hodnotu vlastnosti `background-color`. Chcete-li vyvolat výběr barvy, umístěte kurzor za název vlastnosti a typ **#** nebo **RGB (** .

![Panel pro výběr barvy CSS](using-page-inspector-in-aspnet-mvc/_static/image36.png)

Klikněte na barvu, kterou chcete vybrat, nebo stiskněte klávesu šipka dolů a pak použijte šipky vlevo a vpravo k procházení barev. Při návštěvě barvy se zobrazí náhled odpovídající hexadecimální hodnoty:

![Náhled hodnoty vlastnosti background-color](using-page-inspector-in-aspnet-mvc/_static/image38.png)

Pokud pruh barev nemá přesnou barvu, kterou chcete použít, můžete použít rozevírací nabídka pro výběr barvy. Chcete-li jej otevřít, klikněte na dvojitou dvojitou šipku na pravém konci pruhu barev nebo na klávesnici stiskněte šipku dolů nebo dvakrát.

![Místní nabídka pro výběr barvy CSS](using-page-inspector-in-aspnet-mvc/_static/image40.png)

Klikněte na barvu ze svislého pruhu na pravé straně. Tím se v hlavním okně zobrazí barevný přechod pro tuto barvu. Vyberte barvu přímo ze svislého pruhu stisknutím klávesy ENTER nebo kliknutím na libovolný bod v hlavním okně vyberte s větší přesností.

Pokud je na obrazovce počítače barva, kterou chcete použít (nemusí být uvnitř uživatelského rozhraní sady Visual Studio), můžete zachytit její hodnotu pomocí nástroje kapátka v pravém dolním rohu.

Můžete také změnit neprůhlednost barvy přesunutím posuvníku v dolní části výběru barvy. Tím se změní hodnoty barev na hodnoty RGBA, protože formát RGBA může představovat neprůhlednost.

Po zvolení barvy stiskněte klávesu ENTER a zadáním středníku dokončete položku pozadí-Color v souboru *site. CSS* .

<a id="_the_update_bar"></a>

### <a name="the-page-inspector-update-bar"></a>Panel aktualizace inspektoru stránky

Inspektor stránky hned detekuje změnu v souboru *Web. CSS* a zobrazí výstrahu na panelu aktualizace.

![Aktualizovat panel](using-page-inspector-in-aspnet-mvc/_static/image42.png)

Chcete-li uložit všechny soubory a aktualizovat prohlížeč kontroly stránky, stiskněte klávesy CTRL + ALT + ENTER nebo klikněte na panel aktualizace. Změna barvy zvýraznění se zobrazí v prohlížeči.

<a id="map_dynamic_elements"></a>
## <a name="mapping-dynamic-page-elements-to-javascript"></a>Mapování dynamických prvků stránky na JavaScript

V moderních webových aplikacích se prvky na stránce často generují dynamicky pomocí JavaScriptu. To znamená, že není k dispozici žádný statický kód (HTML nebo Razor), který by odpovídal těmto prvkům stránky.

S verzí 1,3 teď může inspektor stránky namapovat položky, které se dynamicky přidaly na stránku, zpátky do odpovídajícího kódu JavaScriptu. K předvedení této funkce použijeme [šablonu jednostránkové aplikace (Spa)](../../../single-page-application/overview/introduction/knockoutjs-template.md).

> [!NOTE]
> Šablona zabezpečeného hesla vyžaduje aktualizaci [ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=282650) .

V aplikaci Visual Studio vyberte **soubor** &gt; **Nový projekt**. Na levé straně rozbalte **C#vizuál**, vyberte **Web**a pak vyberte **Webová aplikace ASP.NET MVC4**. Klikněte na tlačítko **OK**.

V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte **aplikace s jednou stránkou**.

V Průzkumník řešení rozbalte složku **zobrazení** a pak do **domovské** složky. Klikněte pravým tlačítkem na soubor index. cshtml a **v okně Kontrola stránky vyberte Zobrazit**.

První věc zobrazená v prohlížeči Inspector stránky je přihlašovací stránka. Klikněte na zaregistrovat se a vytvořte uživatelské jméno a heslo. Po registraci se aplikace přihlásí a vytvoří seznam úkolů s některými ukázkovými položkami.

Kliknutím na tlačítko **zkontrolovat** umístěte inspektor stránky do režimu kontroly. V prohlížeči Inspector stránky klikněte na jednu z položek úkolů. Všimněte si, že místo aby bylo zvýrazněno modře, je prvek zvýrazněný žlutě a "JS" vedle názvu elementu. To znamená, že prvek byl vytvořen dynamicky prostřednictvím skriptu.

![](using-page-inspector-in-aspnet-mvc/_static/image44.png)

Navíc se na kartě **zásobník volání** zobrazí oranžové podtržení. To značí, že podokno **zásobník volání** obsahuje další informace o elementu.

Klikněte na kartu **zásobník volání** . V podokně **zásobník volání** se zobrazuje zásobník volání pro volání JavaScriptu, které vytvořilo element. Volání externích knihoven, jako je jQuery, jsou sbalena, takže můžete snadno zobrazit volání skriptu aplikace.

![](using-page-inspector-in-aspnet-mvc/_static/image46.png)

Chcete-li zobrazit úplný zásobník, včetně volání externích knihoven, můžete rozbalit uzly s označením "externí knihovny":

![](using-page-inspector-in-aspnet-mvc/_static/image48.png)

Pokud kliknete na položku v zásobníku volání, aplikace Visual Studio otevře soubor kódu a zvýrazní odpovídající skript.

![](using-page-inspector-in-aspnet-mvc/_static/image50.png)

## <a name="see-also"></a>Viz také

[Úvod do ASP.NET MVC 4 s Visual Studiem](../older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md) (ASP.NET Web)

[Úvod do inspektoru stránky](https://channel9.msdn.com/posts/visual-studio-vnext-introducing-page-inspector/) (video pro kanál 9)

[Chybové zprávy v inspektoru stránky](https://go.microsoft.com/?linkid=9813062) (MSDN)

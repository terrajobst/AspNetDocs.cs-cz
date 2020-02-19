---
uid: mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
title: Použití pomocné rutiny DropDownList s ASP.NET MVC | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 01/12/2012
ms.assetid: 53767e05-c8ab-42e1-a94b-22d906195200
msc.legacyurl: /mvc/overview/older-versions/working-with-the-dropdownlist-box-and-jquery/using-the-dropdownlist-helper-with-aspnet-mvc
msc.type: authoredcontent
ms.openlocfilehash: 6375bb2be158cea18309ffa71c71ac3e67bc91ed
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457866"
---
# <a name="using-the-dropdownlist-helper-with-aspnet-mvc"></a>Použití pomocné rutiny DropDownList s ASP.NET MVC

od [Rick Anderson](https://twitter.com/RickAndMSFT)

V tomto kurzu se seznámíte se základy práce s pomocníkem [DropDownList](https://msdn.microsoft.com/library/dd492948.aspx) a doplňkem [ListBox](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx) ve webové aplikaci ASP.NET MVC. Pomocí sady Microsoft Visual Web Developer 2010 Express Service Pack 1, což je bezplatná verze Microsoft Visual Studio, můžete postupovat podle tohoto kurzu. Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže. Všechny z nich můžete nainstalovat kliknutím na následující odkaz: instalace [webové platformy](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Případně můžete požadavky jednotlivě nainstalovat pomocí následujících odkazů:

- [Požadavky sady Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)<a id="post"></a>
- [Aktualizace nástrojů MVC 3 pro ASP.NET](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(podpora modulu runtime + nástroje)

Pokud používáte sadu Visual Studio 2010 místo sady Visual Web Developer 2010, nainstalujte požadavky kliknutím na následující odkaz: sady [Visual studio 2010 požadavky](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack). V tomto kurzu se předpokládá, že jste dokončili kurz [Úvod do ASP.NET MVC](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) nebo kurz pro[hudební úložiště ASP.NET MVC](../mvc-music-store/mvc-music-store-part-1.md) nebo jste obeznámeni s vývojem ASP.NET MVC. Tento kurz začíná upraveným projektem z kurzu [ASP.NET MVC pro hudební úložiště](../mvc-music-store/mvc-music-store-part-1.md) . Spouštěcí projekt si můžete stáhnout pomocí následujícího odkazu [Stáhnout C# verzi](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829).

Projekt Visual Web Developer se zdrojovým kódem dokončeného kurzu C# je k dispozici pro toto téma. [Stáhnout](https://code.msdn.microsoft.com/Using-the-DropDownList-67f9367d).

### <a name="what-youll-build"></a>Co sestavíte

Vytvoříte metody akcí a zobrazení, která používají pomocníka [DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx) k výběru kategorie. K přidání dialogového okna Vložit kategorii, který se dá použít, když je potřeba nová kategorie (třeba Žánr nebo umělec), můžete také použít **jQuery** . Níže je snímek obrazovky pro zobrazení pro vytváření, ve kterém se zobrazují odkazy na přidání nového žánru a přidání nového interpreta.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image1.png)

### <a name="skills-youll-learn"></a>Dovednosti, se kterými se naučíte

Tady je seznam toho, co se naučíte:

- Jak použít pomocníka [DropDownList](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.dropdownlist.aspx) k výběru dat kategorie.
- Postup přidání nového kategorie do dialogového okna **jQuery**

### <a name="getting-started"></a>Začínáme

Začněte stažením počátečního projektu pomocí následujícího odkazu [Stáhnout](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15829). V Průzkumníku Windows klikněte pravým tlačítkem na soubor *DDL\_Starter. zip* a vyberte vlastnosti. V dialogovém okně **vlastnosti\_Starter. zip pro DDL** vyberte odblokovat.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image2.png)

Klikněte pravým tlačítkem na soubor DDL\_Starter. zip a vyberte rozbalit **vše pro rozbalení** souboru. Otevřete soubor *StartMusicStore. sln* pomocí aplikace Visual web Developer 2010 Express ("Visual Web Developer" nebo "souboru vwd" pro Short) nebo Visual Studio 2010.

Stisknutím kombinace kláves CTRL + F5 spusťte aplikaci a klikněte na odkaz **test** .

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image3.png)

Vyberte odkaz **Vybrat kategorii videa (jednoduché)** . Zobrazí se seznam typ filmu, který je vybrán, přičemž komedie vybraná hodnota.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image4.png)

Klikněte pravým tlačítkem na prohlížeč a vyberte Zobrazit zdroj. Zobrazí se HTML pro stránku. Následující kód ukazuje HTML pro element SELECT.

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample1.html)]

Vidíte, že každá položka v seznamu Select má hodnotu (0 pro akci, 1 pro drama, 2 pro komedie a 3 pro vědu fiktivní) a zobrazované jméno (akce, drama, komedie a vědecký fiktivní). Výše uvedený kód je standardní HTML pro výběrový seznam.

Změňte seznam Select na drama a stiskněte tlačítko **Odeslat** . Adresa URL v prohlížeči je `http://localhost:2468/Home/CategoryChosen?MovieType=1` a zobrazí se stránka **, kterou jste vybrali: 1**.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image5.png)

Otevřete soubor *souboru controllers\homecontroller.cs* a prověřte metodu `SelectCategory`.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample2.cs)]

Pomocný objekt [DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) použitý k vytvoření seznamu SELECT jazyka HTML vyžaduje rozhraní **IEnumerable&lt;SelectListItem &gt;** , buď explicitně, nebo implicitně. To znamená, že můžete předat rozhraní **ienumerable&lt;SelectListItem &gt;** explicitně do pomocníka [DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) nebo můžete přidat **&gt;IEnumerable&lt;SelectListItem** do [ViewBag](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) pomocí stejného názvu jako vlastnost modelu **SelectListItem** . Implicitně se předává do **SelectListItem** a výslovně se zabývá v další části tohoto kurzu. Výše uvedený kód ukazuje nejjednodušší možný způsob, jak vytvořit rozhraní **IEnumerable&lt;SelectListItem &gt;** a naplnit ho textem a hodnotami. Všimněte si, že `Comedy`[SelectListItem](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.aspx) má [vybranou](https://msdn.microsoft.com/library/system.web.mvc.selectlistitem.selected.aspx) vlastnost nastavenou na **hodnotu true** . tím dojde k tomu, že vykreslený seznam výběru zobrazí **komedie** jako vybranou položku v seznamu.

**&gt;typu IEnumerable&lt;SelectListItem** , který jste vytvořili výše, se přidá do [ViewBag](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) s názvem MovieType. To je způsob, jak předat rozhraní **IEnumerable&lt;SelectListItem &gt;** implicitně na pomocníka [DropDownList](https://msdn.microsoft.com/library/dd492738.aspx) , jak je uvedeno níže.

Otevřete soubor *Views\Home\SelectCategory.cshtml* a Projděte si označení.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample3.cshtml)]

Na třetím řádku nastavíme rozložení na zobrazení/Shared/\_Simple\_layout. cshtml, což je zjednodušená verze standardního souboru rozložení. Provedeme to tak, aby byl kód HTML snadno zobrazený a vykreslený.

V této ukázce neměníme stav aplikace, takže pošleme data pomocí **HTTP GET**, ne **http post**. [Výběr HTTP GET nebo post najdete v části rychlý kontrolní seznam pro](http://www.w3.org/2001/tag/doc/whenToUseGet.html#checklist)konsorcium W3C. Vzhledem k tomu, že aplikaci neměníme a publikujete formulář, používáme přetížení [HTML. BeginForm](https://msdn.microsoft.com/library/dd460344.aspx) , které nám umožňuje zadat metodu akce, řadič a formu (**http post** nebo **HTTP GET**). Typicky zobrazení obsahují přetížení [HTML. BeginForm](https://msdn.microsoft.com/library/dd505244.aspx) , které nepřijímá žádné parametry. Žádná verze parametru nepoužívá výchozí hodnotu pro publikování dat formuláře do verze příspěvku stejné metody akce a kontroleru.

Následující řádek

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample4.cshtml)]

předá do pomocné rutiny **DropDownList** argument řetězce. Tento řetězec "MovieType" v našem příkladu provádí dvě věci:

- Poskytuje klíč pro pomocníka **DropDownList** k vyhledání **IEnumerable&lt;SelectListItem &gt;** v **ViewBag**.
- Je vázán na data s prvkem formuláře MovieType. Pokud je metoda odeslání **HTTP GET**, `MovieType` bude řetězec dotazu. Pokud je metoda odeslání **http post**, `MovieType` se přidá do textu zprávy. Následující obrázek znázorňuje řetězec dotazu s hodnotou 1.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image6.png)

Následující kód ukazuje metodu `CategoryChosen`, do které byl formulář odeslán.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample5.cs)]

Přejděte zpět na stránku test a vyberte odkaz **HTML SelectList** . Stránka HTML vykresluje element SELECT podobný ASP.NET stránce testu jednoduché sady MVC. Klikněte pravým tlačítkem na okno prohlížeče a vyberte **Zobrazit zdroj**. Označení HTML pro seznam Select je v podstatě identické. Testování stránky HTML funguje jako metoda akce ASP.NET MVC a zobrazení, které jsme dříve otestovali.

### <a name="improving-the-movie-select-list-with-enums"></a>Zlepšení seznamu pro výběr videa s výčty

Pokud jsou kategorie ve vaší aplikaci pevně dané a nemění se, můžete využít výčty, aby byl váš kód robustnější a jednodušší ho lépe roztáhnout. Když přidáte novou kategorii, vygeneruje se správná hodnota kategorie. Vyloučí chyby kopírování a vkládání při přidání nové kategorie, ale nezapomeňte aktualizovat hodnotu kategorie.

Otevřete soubor *souboru controllers\homecontroller.cs* a Projděte si následující kód:

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample6.cs)]

[Výčet](https://msdn.microsoft.com/library/sbbt4032(VS.80).aspx) `eMovieCategories` zachycuje čtyři typy filmů. Metoda `SetViewBagMovieType` vytvoří rozhraní **IEnumerable&lt;SelectListItem &gt;** z **výčtu**`eMovieCategories`a nastaví vlastnost `Selected` z parametru `selectedMovie`. Metoda `SelectCategoryEnum` akce používá stejné zobrazení jako metoda `SelectCategory` akce.

Přejděte na stránku test a klikněte na odkaz `Select Movie Category (Enum)`. Tentokrát místo hodnoty (číslo), který představuje výčet, se zobrazí řetězec představující výčet.

### <a name="posting-enum-values"></a>Účtování hodnot výčtu

Formuláře HTML se obvykle používají k odesílání dat na server. Následující kód ukazuje `HTTP GET` a `HTTP POST` verze metody `SelectCategoryEnumPost`.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample7.cs)]

Předáním `eMovieCategories` výčtu do metody `POST` můžeme extrahovat jak hodnotu výčtu, tak i řetězec Enum. Spusťte ukázku a přejděte na stránku test. Klikněte na odkaz `Select Movie Category(Enum Post)`. Vyberte typ filmu a potom stiskněte tlačítko Odeslat. Zobrazení zobrazuje jak hodnotu, tak název typu videa.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image7.png)

### <a name="creating-a-multiple-section-select-element"></a>Vytvoření více oddílů výběr elementu

Pomocník [HTML v seznamu vykresluje](https://msdn.microsoft.com/library/system.web.mvc.html.selectextensions.listbox.aspx) prvek HTML `<select>` s atributem `multiple`, který umožňuje uživatelům provádět více výběrů. Přejděte na odkaz test a pak vyberte odkaz **vybrat zemi** . Vykreslené uživatelské rozhraní umožňuje vybrat více zemí. Na obrázku níže je vybrána možnost Kanada a Čína.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image8.png)

### <a name="examining-the-multiselectcountry-code"></a>Zkoumání kódu MultiSelectCountry

Projděte si následující kód ze souboru *souboru controllers\homecontroller.cs* .

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample8.cs)]

Metoda `GetCountries` vytvoří seznam zemí a pak ji předává konstruktoru `MultiSelectList`. Přetížení konstruktoru `MultiSelectList` použité v metodě `GetCountries` výše přijímá čtyři parametry:

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample9.cs)]

1. *Items*: rozhraní [IEnumerable](https://msdn.microsoft.com/library/system.collections.ienumerable.aspx) obsahující položky v seznamu. V předchozím příkladu se seznam zemí.
2. *dataValueField*: název vlastnosti v seznamu **IEnumerable** , který obsahuje hodnotu. V předchozím příkladu je vlastnost `ID`.
3. *dataTextField*: název vlastnosti v seznamu **IEnumerable** obsahující informace, které se mají zobrazit. V předchozím příkladu je vlastnost `name`.
4. *selectedValues*: seznam vybraných hodnot.

V předchozím příkladu metoda `MultiSelectCountry` předává `null` hodnotu pro vybrané země, takže při zobrazení uživatelského rozhraní nejsou vybrány žádné země. Následující kód ukazuje značku Razor použitou k vykreslení zobrazení `MultiSelectCountry`.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample10.cshtml)]

Výše použitá metoda [seznamu](https://msdn.microsoft.com/library/dd470200.aspx) POMOCNÍKa HTML přebírá dva parametry, název vlastnosti pro svázání modelů a [MultiSelectList](https://msdn.microsoft.com/library/system.web.mvc.multiselectlist.aspx) obsahující možnosti a hodnoty pro výběr. Výše uvedený kód `ViewBag.YouSelected` slouží k zobrazení hodnot zemí, které jste vybrali při odeslání formuláře. Projděte si přetížení HTTP POST metody `MultiSelectCountry`.

[!code-csharp[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample11.cs)]

`ViewBag.YouSelected` dynamická vlastnost obsahuje vybrané země, které byly získány pro položku `Countries` v kolekci Form. V této verzi se metoda getzemích předává do seznamu vybraných zemí, takže když se zobrazí `MultiSelectCountry` zobrazení, vybrané země se vyberou v uživatelském rozhraní.

### <a name="making-a-select-element-friendly-with-the-harvest-chosen-jquery-plugin"></a>Vytvoření prvku výběru, který je popisný pro vybraný modul plug-in jQuery v rámci sklizně

[Vybraný](https://harvesthq.github.com/chosen/) modul plug-in jQuery pro sklizeň se dá přidat do HTML &lt;vyberte&gt; element a vytvořte uživatelsky přívětivé uživatelské rozhraní. Následující obrázky znázorňují [vybraný](https://harvesthq.github.com/chosen/) modul plug-in jQuery pomocí zobrazení `MultiSelectCountry`.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image9.png)

Na dvou obrázcích níže je vybrána možnost **Kanada** .

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image10.png)

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image11.png)

Na obrázku výše je vybrána možnost Kanada a obsahuje znak **x** . Kliknutím můžete výběr odebrat. Následující obrázek ukazuje, že je vybraná možnost Kanada, Čína a Japonsko.

![](using-the-dropdownlist-helper-with-aspnet-mvc/_static/image12.png)

### <a name="hooking-up-the-harvest-chosen-jquery-plugin"></a>Zapojování vybraného modulu plug-in jQuery vybrané sklizně

V následující části je snazší postupovat, pokud máte zkušenosti s jQuery. Pokud jste ještě nikdy nepoužili jQuery, možná budete chtít vyzkoušet některý z následujících kurzů jQuery.

- [Jak funguje jQuery](http://docs.jquery.com/Tutorials:How_jQuery_Works) pomocí [Jan Resig](http://ejohn.org/)
- [Začínáme pomocí jQuery](http://docs.jquery.com/Tutorials:Getting_Started_with_jQuery) pomocí [Jörn Zaefferer](http://bassistance.de/)
- [Živé příklady jQuery](http://codylindley.com/blogstuff/js/jquery/#) podle [Cody Lindley](http://codylindley.com/)

Vybraný modul plug-in je zahrnutý v ukázkových projektech a dokončených vzorových projektech, které doprovázejí tento kurz. Pro tento kurz budete muset použít jQuery jenom k jeho zapojení do uživatelského rozhraní. Pokud chcete použít vybraný modul plug-in jQuery v ASP.NET MVC, musíte:

1. Stáhněte si zvolený modul plug-in z [GitHubu](https://github.com/harvesthq/chosen/). Tento krok se vám udělal za vás.
2. Přidejte zvolenou složku do projektu ASP.NET MVC. Přidejte prostředky z vybraného modulu plug-in, který jste stáhli v předchozím kroku, do zvolené složky. Tento krok se vám udělal za vás.
3. Zapojte zvolený modul plug-in k Pomocníkovi HTML **DropDownList** nebo **ListBox** .

### <a name="hooking-up-the-chosen-plugin-to-the-multiselectcountry-view"></a>Zapojování zvoleného modulu plug-in do zobrazení MultiSelectCountry

Otevřete soubor *Views\Home\MultiSelectCountry.cshtml* a přidejte do `Html.ListBox`parametr `htmlAttributes`. Parametr, který přidáte, bude obsahovat název třídy pro seznam Select (`@class = "chzn-select"`). Dokončený kód je zobrazen níže:

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample12.cshtml)]

Do výše uvedeného kódu přidáváme atribut HTML a hodnotu atributu `class = "chzn-select"`. \@ znak předchozí třídy nemá žádnou akci s modulem zobrazení Razor. `class` je [ C# klíčové slovo](https://msdn.microsoft.com/library/x53a06bb.aspx). C#Klíčová slova nelze použít jako identifikátory, pokud neobsahují \@ jako předponu. V předchozím příkladu je `@class` platný identifikátor, ale **Třída** není, protože **Třída** je klíčové slovo.

Přidejte odkazy na *zvolený/zvolený jQuery. jQuery. js* a *zvolené nebo zvolené soubory. CSS* . *Zvolený/zvolený jQuery. jQuery. js* a implementuje funkci pro zvolený modul plug-in. *Zvolený nebo zvolený soubor. CSS* poskytuje styly. Přidejte tyto odkazy na konec souboru *Views\Home\MultiSelectCountry.cshtml* . Následující kód ukazuje, jak odkazovat na vybraný modul plug-in.

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample13.cshtml)]

Aktivujte zvolený modul plug-in pomocí názvu třídy používaného v kódu **HTML. ListBox** . V předchozím příkladu je název třídy `chzn-select`. Přidejte následující řádek do dolní části souboru zobrazení *Views\Home\MultiSelectCountry.cshtml* . Tento řádek aktivuje vybraný modul plug-in.

[!code-html[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample14.html)]

Následující řádek je syntaxe, která volá funkci jQuery připravenou, která vybere prvek DOM s názvem třídy `chzn-select`.

[!code-powershell[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample15.ps1)]

Zabalená sada vrácená výše uvedeným voláním pak použije zvolenou metodu (`.chosen();`), která zavolá vybraný modul plug-in.

Následující kód ukazuje dokončený soubor zobrazení *Views\Home\MultiSelectCountry.cshtml* .

[!code-cshtml[Main](using-the-dropdownlist-helper-with-aspnet-mvc/samples/sample16.cshtml)]

Spusťte aplikaci a přejděte do zobrazení `MultiSelectCountry`. Zkuste přidat a odstranit země. Ukázkové stažení obsahuje také metodu `MultiCountryVM` a zobrazení, které implementuje funkci MultiSelectCountry pomocí modelu zobrazení místo **ViewBag**.

V další části se dozvíte, jak mechanismus generování uživatelského rozhraní ASP.NET MVC funguje s pomocníkem **DropDownList** .

> [!div class="step-by-step"]
> [Next](examining-how-aspnet-mvc-scaffolds-the-dropdownlist-helper.md)

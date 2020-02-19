---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
title: Použití místního kalendáře DatePicker HTML5 a jQuery UI s ASP.NET MVC – část 4 | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy práce s šablonami editoru, šablonami zobrazení a místním datepickerm ovládacího prvku jQuery uživatelského rozhraní v ASP.NET MV...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 57666c69-2b0f-423a-a61d-be49547fa585
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4
msc.type: authoredcontent
ms.openlocfilehash: 583e782641efea9a9517edb31f7718b28203d756
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457489"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-4"></a>Použití místního kalendáře DatePicker HTML5 a jQuery UI s ASP.NET MVC – část 4

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> V tomto kurzu se seznámíte se základy práce s šablonami editoru, šablonami zobrazení a místním datepickerm ovládacího prvku jQuery uživatelského rozhraní ve webové aplikaci ASP.NET MVC.

### <a name="adding-a-template-for-editing-dates"></a>Přidání šablony pro data úpravy

V této části vytvoříte šablonu pro úpravu dat, která se použijí, když ASP.NET MVC zobrazí uživatelské rozhraní pro úpravy vlastností modelu, které jsou označené výčtem **data** pro atribut [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) . Šablona vygeneruje pouze datum; čas se nezobrazí. V šabloně použijete místní místní kalendář [jQuery DatePicker](http://jqueryui.com/demos/datepicker/) , který poskytuje způsob, jak upravovat data.

Začněte tím, že otevřete soubor *Movie.cs* a do vlastnosti `ReleaseDate` přidáte atribut [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatypeattribute.aspx) s výčtem **data** , jak je znázorněno v následujícím kódu:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample1.cs)]

Tento kód způsobí, že se pole `ReleaseDate` zobrazí bez času v šablonách zobrazení a úpravách šablon. Pokud vaše aplikace obsahuje šablonu *Date. cshtml* ve složce *Views\Shared\EditorTemplates* nebo ve složce *Views\Movies\EditorTemplates* , bude tato šablona použita k vykreslení libovolné vlastnosti `DateTime` při úpravách. V opačném případě bude integrovaný systém ASP.NET šablonování zobrazovat vlastnost jako datum.

Stiskněte klávesy CTRL+F5 a spusťte aplikaci. Vyberte odkaz pro úpravy a ověřte, že vstupní pole pro datum vydání zobrazuje pouze datum.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image1.png)

V **Průzkumník řešení**rozbalte složku *zobrazení* , rozbalte *sdílenou* složku a potom klikněte pravým tlačítkem na složku *Views\Shared\EditorTemplates* .

Klikněte na tlačítko **Přidat**a potom klikněte na tlačítko **Zobrazit**. Zobrazí se dialogové okno **Přidat zobrazení** .

Do pole **název zobrazení** zadejte &quot;datum&quot;.

Vyberte zaškrtávací políčko **vytvořit jako částečné zobrazení** . Ujistěte se, že nejsou vybrána zaškrtávací políčka **použít rozložení nebo hlavní stránku** a **vytvořit zobrazení se silným typem** .

Klikněte na **Přidat**. Vytvoří se šablona *Views\Shared\EditorTemplates\Date.cshtml* .

Do šablony *Views\Shared\EditorTemplates\Date.cshtml* přidejte následující kód.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample2.cshtml)]

První řádek deklaruje model jako typ `DateTime`. I když nemusíte deklarovat typ modelu v šablonách pro úpravy a zobrazení, je osvědčeným postupem, abyste získali kontrolu nad předaným modelem v průběhu kompilace. (Další výhodou je, že potom získáte IntelliSense pro model v zobrazení v aplikaci Visual Studio.) Pokud typ modelu není deklarován, ASP.NET MVC považuje typ za [dynamický](https://msdn.microsoft.com/library/dd264741.aspx) a neexistuje žádná kontrola typu v době kompilace. Pokud deklarujete model, který bude `DateTime` typ, bude silného typu.

Druhý řádek je pouze literální kód HTML, který zobrazuje &quot;pomocí šablony data&quot; před polem data. Tento řádek použijete dočasně k ověření, že se používá tato šablona kalendářního data.

Další řádek je pomocník [HTML. TextBox](https://msdn.microsoft.com/library/system.web.mvc.html.inputextensions.textbox.aspx) , který vykreslí pole `input`, které je textové pole. Třetí parametr pomocné rutiny používá anonymní typ k nastavení třídy pro textové pole, které se má `datefield`, a typ, který se má `date`. (Protože je `class` rezervován v C#, je nutné použít `@` znak k úniku atributu `class` v C# analyzátoru.)

Typ `date` je vstupní typ HTML5, který umožňuje prohlížečům podporujícím HTML5 vykreslování ovládacího prvku kalendáře HTML5. Později přidáte několik JavaScriptu, abyste připojili jQuery DatePicker k elementu `Html.TextBox` pomocí `datefield` třídy.

Stiskněte klávesy CTRL+F5 a spusťte aplikaci. Můžete ověřit, že vlastnost `ReleaseDate` v zobrazení pro úpravy používá šablonu Edit, protože šablona zobrazuje &quot;pomocí šablony data&quot; těsně před vstupním polem `ReleaseDate` text, jak je znázorněno na tomto obrázku:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image2.png)

V prohlížeči zobrazte zdroj stránky. (Například klikněte pravým tlačítkem na stránku a vyberte **Zobrazit zdroj**.) Následující příklad ukazuje některé značky pro stránku, ilustrující `class` a `type` atributy ve vykresleném HTML.

[!code-html[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample3.html)]

Vraťte se do šablony *Views\Shared\EditorTemplates\Date.cshtml* a odeberte &quot;pomocí šablony data&quot; označení. Hotová šablona teď vypadá takto:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample4.cshtml)]

### <a name="adding-a-jquery-ui-datepicker-popup-calendar-using-nuget"></a>Přidání místního kalendáře DatePicker uživatelského rozhraní jQuery pomocí NuGet

V této části přidáte do šablony data a Edit místní nabídku [DatePicker uživatelského rozhraní jQuery](http://jqueryui.com/demos/datepicker/) . Knihovna [uživatelského rozhraní jQuery](http://jqueryui.com/) poskytuje podporu pro animace, pokročilé efekty a přizpůsobitelné pomůcky. Je postaven na knihovně jazyka jQuery JavaScriptu. Místní okno DatePicker usnadňuje a přirozené zadání dat pomocí kalendáře namísto zadávání řetězce. Místní kalendář také omezuje uživatele na právní data – normální textové zadání data vám umožní zadat něco podobného jako `2/33/1999` (únor 33rd, 1999), ale místní nabídka [DatePicker uživatelského rozhraní jQuery](http://jqueryui.com/demos/datepicker/) to neumožní.

Nejdřív je nutné nainstalovat knihovny uživatelského rozhraní jQuery. K tomu budete používat NuGet, což je správce balíčků, který je zahrnutý ve verzích SP1 sady Visual Studio 2010 a Visual Web Developer.

V aplikaci Visual Web Developer v nabídce **nástroje** vyberte **Správce balíčků NuGet** a pak vyberte **Spravovat balíčky NuGet**.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image3.png)

Poznámka: Pokud se v nabídce **nástroje** nezobrazí příkaz **Správce balíčků NuGet** , je nutné nainstalovat NuGet podle pokynů na stránce [instalace NuGet](http://docs.nuget.org/docs/start-here/installing-nuget) na webu NuGet.   
  
Pokud používáte sadu Visual Studio namísto Visual Web Developer, v nabídce **nástroje** vyberte **Správce balíčků NuGet** a pak vyberte **Přidat odkaz na balíček knihovny**.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image4.png)

V dialogovém okně **MVCMovie – spravovat balíčky NuGet** klikněte na kartu **online** na levé straně a do vyhledávacího pole zadejte &quot;jQuery. UI&quot;. Vyberte j **Query UI widgets: DatePicker**a pak vyberte tlačítko **nainstalovat** .

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image5.png)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image6.png)

NuGet přidá tyto verze ladění a minifikovaného verze jádra uživatelského rozhraní jQuery a výběr data uživatelského rozhraní jQuery do vašeho projektu:

- *jQuery. UI. Core. js*
- *jQuery. UI. Core. min. js*
- *jQuery. UI. DatePicker. js*
- *jQuery. UI. DatePicker. min. js*

Poznámka: ladicí verze (soubory bez přípony *. min. js* ) jsou užitečné pro ladění, ale v produkčním webu byste měli použít jenom minifikovaného verze.

Chcete-li použít nástroj pro výběr data jQuery, je nutné vytvořit skript jQuery, který bude zapojovat pomůcku kalendáře do šablony pro úpravy. V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku *skripty* a vyberte **Přidat**, **Nová položka**a potom **soubor JScript**. Pojmenujte soubor *DatePickerReady. js*.

Do souboru *DatePickerReady. js* přidejte následující kód:

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample5.js)]

Pokud nejste obeznámeni se jQuery, tady je stručné vysvětlení toho, co to dělá: první řádek je funkce &quot;jQuery připravená&quot;, která se volá, když se načtou všechny prvky modelu DOM na stránce. Druhý řádek vybere všechny prvky modelu DOM, které mají název třídy `datefield`a poté vyvolá funkci `datepicker` pro každý z nich. (Nezapomeňte přidat třídu `datefield` do šablony *Views\Shared\EditorTemplates\Date.cshtml* dříve v tomto kurzu.)

Potom otevřete soubor *Views\Shared\\_Layout. cshtml* . Je nutné přidat odkazy na následující soubory, které jsou všechny nutné, aby bylo možné použít nástroj pro výběr data:

- *Content/Themes/Base/jQuery. UI. Core. CSS*
- *Content/Themes/Base/jQuery. UI. DatePicker. CSS*
- *Content/Themes/Base/jQuery. UI. theme. CSS*
- *jQuery. UI. Core. min. js*
- *jQuery. UI. DatePicker. min. js*
- *DatePickerReady. js*

Následující příklad ukazuje skutečný kód, který byste měli přidat v dolní části `head` elementu v souboru *\\_Layout. cshtml pro Views\Shared* .

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample6.cshtml)]

Část kompletní `head` se zobrazí zde:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample7.cshtml)]

[Pomocná metoda obsahu URL](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.content.aspx) převádí cestu prostředku na absolutní cestu. Pokud je aplikace spuštěna ve službě IIS, je nutné použít `@URL.Content` pro správné odkazování na tyto prostředky.

Stiskněte klávesy CTRL+F5 a spusťte aplikaci. Vyberte odkaz upravit a pak umístěte kurzor do pole **ReleaseDate** . Zobrazí se automaticky otevírané okno uživatelského rozhraní jQuery.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image7.png)

Podobně jako většina ovládacích prvků jQuery vám DatePicker umožňuje rozsáhlé přizpůsobení. Informace najdete v tématu [přizpůsobení vizuálů: návrh motivu uživatelského rozhraní jQuery](http://learn.jquery.com/jquery-ui/getting-started/#visual-customization-designing-a-jquery-ui-theme) na webu [uživatelského rozhraní jQuery](http://learn.jquery.com/jquery-ui/getting-started/) .

### <a name="supporting-the-html5-date-input-control"></a>Podpora ovládacího prvku zadávání data HTML5

Protože více prohlížečů podporuje HTML5, budete chtít použít nativní vstup HTML5, například `date` vstupní prvek, a nepoužívat kalendář uživatelského rozhraní jQuery. Do své aplikace můžete přidat logiku pro automatické použití ovládacích prvků HTML5, pokud je prohlížeč podporuje. Chcete-li to provést, nahraďte obsah souboru *DatePickerReady. js* následujícím způsobem:

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample8.js)]

První řádek tohoto skriptu používá modernizr k ověření, že zadání data HTML5 je podporováno. Pokud není podporováno, je místo toho připojen nástroj pro výběr data uživatelského rozhraní jQuery. ([Modernizr](http://www.modernizr.com/docs/) je open source knihovna JavaScriptu, která detekuje dostupnost nativních implementací HTML5 a CSS3. Modernizr je součástí všech nových projektů ASP.NET MVC, které vytvoříte.)

Po provedení této změny ji můžete otestovat pomocí prohlížeče, který podporuje HTML5, jako je například Opera 11. Spusťte aplikaci pomocí prohlížeče kompatibilního s HTML5 a upravte záznam filmu. Použije se ovládací prvek data HTML5 místo místního kalendáře uživatelského rozhraní jQuery:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/_static/image8.png)

Vzhledem k tomu, že nové verze prohlížečů implementují HTML5 přírůstkově, dobrým řešením je nyní přidat kód na web, který bude vyhovovat nejrůznější podpoře HTML5. Například robustnější skript *DatePickerReady. js* je zobrazen níže, který umožňuje, aby vaše lokalita podporovala prohlížeče, které pouze částečně podporují ovládací prvek data HTML5.

[!code-javascript[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample9.js)]

Tento skript vybírá prvky HTML5 `input` typu `date`, které plně nepodporují ovládací prvek data HTML5. U těchto elementů se připojovat k místnímu kalendáři uživatelského rozhraní jQuery a poté změní atribut `type` z `date` na `text`. Změnou atributu `type` z `date` na `text`, částečná podpora data HTML5 se eliminuje. Ještě robustnější skript *DatePickerReady. js* najdete na adrese [JSFIDDLE](http://jsfiddle.net/XSTK8/15/).

### <a name="adding-nullable-dates-to-the-templates"></a>Přidání dat s možnou hodnotou null do šablon

Použijete-li jednu z existujících šablon kalendářních dat a předáte datum v hodnotě null, zobrazí se chyba modulu runtime. Aby bylo možné šablony kalendářních dat robustnější, změňte je tak, aby zpracovávala hodnoty null. Chcete-li podporovat data s možnou hodnotou null, změňte kód v *Views\Shared\DisplayTemplates\DateTime.cshtml* na následující:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample10.cshtml)]

Kód vrátí prázdný řetězec, pokud má model **hodnotu null**.

Změňte kód v souboru *Views\Shared\EditorTemplates\Date.cshtml* na následující:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4/samples/sample11.cshtml)]

Pokud je tento kód spuštěn, v případě, že model není null, je použita hodnota `DateTime` modelu. Pokud je model null, použije se místo toho aktuální datum.

### <a name="wrapup"></a>Wrapup

V tomto kurzu se pokryly základy pomocníků s ASP.NET šablonami a dozvíte se, jak používat místní nabídku DatePicker uživatelského rozhraní jQuery v aplikaci ASP.NET MVC. Další informace najdete v těchto zdrojích:

- Informace o lokalizaci najdete v článku Rajeesh blog [JQueryUI DatePicker v ASP.NET MVC](http://www.rajeeshcv.com/2010/02/jqueryui-datepicker-in-asp-net-mvc/).
- Informace o uživatelském rozhraní jQuery najdete v tématu [uživatelské rozhraní jQuery](http://docs.jquery.com/UI).
- Informace o lokalizaci ovládacího prvku DatePicker naleznete v tématu [UI/Datepicker/lokalizace](http://docs.jquery.com/UI/Datepicker/Localization).
- Další informace o šablonách MVC ASP.NET najdete v článku o sérii blogů brada Wilson v [šablonách ASP.NET MVC 2](http://bradwilson.typepad.com/blog/2009/10/aspnet-mvc-2-templates-part-1-introduction.html). I když byla řada napsaná pro ASP.NET MVC 2, materiál se dál vztahuje na aktuální verzi ASP.NET MVC.

> [!div class="step-by-step"]
> [Předchozí](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)

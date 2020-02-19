---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
title: Použití místního kalendáře DatePicker HTML5 a jQuery UI s ASP.NET MVC – část 2 | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy práce s šablonami editoru, šablonami zobrazení a místním datepickerm ovládacího prvku jQuery uživatelského rozhraní v ASP.NET MV...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 21a178de-4c5a-4211-8a9c-74ec576c0f30
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2
msc.type: authoredcontent
ms.openlocfilehash: 325cc90eb6e717c47863eda6253e0d48d796386b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77455890"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-2"></a>Použití místního kalendáře DatePicker HTML5 a jQuery UI s ASP.NET MVC – část 2

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> V tomto kurzu se seznámíte se základy práce s šablonami editoru, šablonami zobrazení a místním datepickerm ovládacího prvku jQuery uživatelského rozhraní ve webové aplikaci ASP.NET MVC.

## <a name="adding-an-automatic-datetime-template"></a>Přidání automatické šablony DateTime

V první části tohoto kurzu jste viděli, jak můžete do modelu přidat atributy pro explicitní určení formátování a způsob, jakým můžete explicitně zadat šablonu, která se používá k vykreslení modelu. Například atribut [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) v následujícím kódu explicitně určuje formátování vlastnosti `ReleaseDate`.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample1.cs)]

V následujícím příkladu atribut [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) pomocí `Date` výčtu Určuje, že šablona data by měla být použita pro vykreslení modelu. Pokud v projektu není žádná šablona kalendářních dat, použije se předdefinovaná šablona kalendářních dat.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample2.cs)]

Nicméně ASP. MVC může provést odpovídající typ pomocí konvence-over-konfigurace, a to tak, že hledá šablonu, která odpovídá názvu typu. To vám umožní vytvořit šablonu, která automaticky formátuje data bez použití jakýchkoli atributů nebo kódu. V této části kurzu vytvoříte šablonu, která se automaticky použije pro vlastnosti modelu typu [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx). K určení, zda má být šablona použita k vykreslení všech vlastností modelu typu [DateTime](https://msdn.microsoft.com/library/system.datetime.aspx), není nutné použít atribut nebo jinou konfiguraci.

Naučíte se také, jak přizpůsobit zobrazení jednotlivých vlastností nebo i jednotlivých polí.

Začněte tím, že odebereme existující informace o formátování a zobrazíme v aplikaci úplná data.

Otevřete soubor *Movie.cs* a odkomentujte atribut `DataType` ve vlastnosti `ReleaseDate`:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample3.cs)]

Stiskněte klávesy CTRL+F5 a spusťte aplikaci.

Všimněte si, že vlastnost `ReleaseDate` nyní zobrazuje datum i čas, protože se jedná o výchozí hodnotu, pokud nejsou k dispozici žádné informace o formátování.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image1.png)

### <a name="adding-css-styles-for-testing-new-templates"></a>Přidávání stylů CSS pro testování nových šablon

Než vytvoříte šablonu pro formátování kalendářních dat, přidáte několik pravidel stylu CSS, která můžete použít na nové šablony. Tyto informace vám pomůžou ověřit, že vykreslená stránka používá novou šablonu.

Otevřete soubor *Content\Site.cs*s a přidejte do dolní části souboru následující pravidla CSS:

[!code-css[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample4.css)]

### <a name="adding-datetime-display-templates"></a>Přidávání šablon zobrazení typu DateTime

Nyní můžete vytvořit novou šablonu. Ve složce *Views\Movies* vytvořte složku *DisplayTemplates* .

Ve složce *Views\Shared* vytvořte složku *DisplayTemplates* a složku *EditorTemplates* .

Šablony zobrazení ve složce *Views\Shared\DisplayTemplates* budou použity všemi řadiči. Šablony zobrazení ve složce *Views\Movie\DisplayTemplates* budou použity pouze řadičem `Movie`. (Pokud se v obou složkách zobrazí šablona se stejným názvem, šablona ve složce *Views\Movie\DisplayTemplates* , která je konkrétnější šablonou, má přednost před zobrazeními vrácenými řadičem `Movie`.)

V **Průzkumník řešení**rozbalte složku *zobrazení* , rozbalte *sdílenou* složku a potom klikněte pravým tlačítkem na složku *Views\Shared\DisplayTemplates* .

Klikněte na **Přidat** a potom na **Zobrazit**. Zobrazí se dialogové okno **Přidat zobrazení** .

Do pole **název zobrazení** zadejte `DateTime`. (Tento název je nutné použít, aby se shodoval s názvem typu.)

Vyberte zaškrtávací políčko **vytvořit jako částečné zobrazení** . Ujistěte se, že nejsou vybrána zaškrtávací políčka **použít rozložení nebo hlavní stránku** a **vytvořit zobrazení se silným typem** .

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image2.png)

Klikněte na **Přidat**. V *Views\Shared\DisplayTemplates*se vytvoří šablona *DateTime. cshtml* .

Na následujícím obrázku je po vytvoření `DateTime` zobrazení a šablon Editor zobrazená složka *zobrazení* v **Průzkumník řešení** .

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image3.png)

Otevřete soubor *Views\Shared\DisplayTemplates\DateTime.cshtml* a přidejte následující kód, který používá metodu [String. Format](https://msdn.microsoft.com/library/system.string.format.aspx) k naformátování vlastnosti jako data bez času. (Formát `{0:d}` určuje formát krátkého data.)

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample5.cs)]

Zopakováním tohoto kroku vytvořte šablonu `DateTime` ve složce *Views\Movie\DisplayTemplates* . V souboru *Views\Movie\DisplayTemplates\DateTime.cshtml* použijte následující kód.

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample6.cs)]

`loud-1` Třída CSS způsobí, že se datum zobrazí v tučném červeném textu. Přidali jsme třídu `loud-1` CSS stejně jako dočasnou míru, abyste mohli snadno zjistit, kdy se tato konkrétní šablona používá.

K tomu, co jste udělali, se vytvoří a přizpůsobené šablony, které ASP.NET použije k zobrazení dat. Obecnější šablona (ve složce *Views\Shared\DisplayTemplates* ) zobrazuje jednoduché krátké datum. Šablona, která je konkrétně pro řadič `Movie` (ve složce *Views\Movies\DisplayTemplates* ), zobrazuje krátké datum, které je také formátováno tučně červený text.

Stiskněte klávesy CTRL+F5 a spusťte aplikaci. Prohlížeč vykreslí zobrazení indexu pro aplikaci.

Vlastnost `ReleaseDate` nyní zobrazí datum tučně červeného písma bez času. To vám pomůže zkontrolovat, jestli je ve složce *Views\Movies\DisplayTemplates* vybraná pomocná šablona `DateTime` šablonou, a to prostřednictvím pomocníka s `DateTime` šablonou ve sdílené složce (*Views\Shared\DisplayTemplates*).

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image4.png)

Nyní přejmenujte soubor *Views\Movies\DisplayTemplates\DateTime.cshtml* na *Views\Movies\DisplayTemplates\LoudDateTime.cshtml*.

Stiskněte klávesy CTRL+F5 a spusťte aplikaci.

Tentokrát vlastnost `ReleaseDate` zobrazuje datum bez času a bez tučného červeného písma. To ukazuje, že šablona, která má název datového typu (v tomto případě `DateTime`), se automaticky používá k zobrazení všech vlastností modelu daného typu. Po přejmenování souboru *DateTime. cshtml* na *LoudDateTime. cshtml*, ASP.NET už ve složce *Views\Movies\DisplayTemplates* nenajde šablonu, takže se použila Šablona *DateTime. cshtml* ze složky * Views\Movies\Shared\*.

(Porovnávání šablon se nerozlišuje bez rozlišení velkých a malých písmen, takže můžete vytvořit název souboru šablony s libovolným písmenem. Například *DateTime. cshtml, DateTime. cshtml*a *DateTime. cshtml* by odpovídaly všem typům `DateTime`.)

Pro kontrolu: v tomto okamžiku se pole `ReleaseDate` zobrazuje pomocí šablony *Views\Movies\DisplayTemplates\DateTime.cshtml* , která zobrazuje data s použitím krátkého formátu data, ale jinak nepřidává žádný speciální formát.

### <a name="using-uihint-to-specify-a-display-template"></a>Určení šablony zobrazení pomocí UIHint

Pokud vaše webová aplikace má mnoho `DateTime` polí a ve výchozím nastavení chcete zobrazit všechna nebo většinu z nich ve formátu pouze data, je šablona *DateTime. cshtml* dobrým přístupem. Ale co když máte několik kalendářních dat, kde chcete zobrazit úplné datum a čas? Žádný problém. Můžete vytvořit další šablonu a pomocí atributu [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) určit formátování pro úplné datum a čas. Tuto šablonu pak můžete selektivně použít. Můžete použít atribut [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) na úrovni modelu nebo můžete zadat šablonu uvnitř zobrazení. V této části se dozvíte, jak použít atribut `UIHint` pro selektivní změnu formátování některých instancí polí datum a čas.

Otevřete soubor *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* a nahraďte existující kód následujícím kódem:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample7.cshtml)]

Tím dojde k zobrazení úplného data a času a přidání třídy šablony stylů CSS, která změní text na zelený a velký.

Otevřete soubor *Movie.cs* a přidejte atribut [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) do vlastnosti `ReleaseDate`, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample8.cs)]

Tato vlastnost dává ASP.NET MVC, že při zobrazení vlastnosti `ReleaseDate` (konkrétně a nikoli pouze žádné objekty `DateTime`) by měla použít šablonu *LoudDateTime. cshtml* .

Stiskněte klávesy CTRL+F5 a spusťte aplikaci.

Všimněte si, že vlastnost `ReleaseDate` nyní zobrazuje datum a čas ve velkém zeleném písmu.

Vraťte se do atributu `UIHint` v souboru *Movie.cs* a zakomentujte ho, aby se šablona *LoudDateTime. cshtml* nepoužila. Spusťte aplikaci znovu. Datum vydání se nezobrazuje jako velké a zelené. Tím se ověří, že se v zobrazení index a podrobnosti používá šablona *Views\Shared\DisplayTemplates\DateTime.cshtml* .

Jak bylo zmíněno dříve, můžete také použít šablonu v zobrazení, které umožňuje použít šablonu na jednotlivou instanci dat. Otevřete zobrazení *Views\Movies\Details.cshtml* . Přidejte `"LoudDateTime"` jako druhý parametr volání [HTML. DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) pro pole `ReleaseDate`. Dokončený kód vypadá takto:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/samples/sample9.cshtml)]

Tato vlastnost určuje, že šablona `LoudDateTime` by měla být použita k zobrazení vlastnosti modelu bez ohledu na to, jaké atributy jsou použity pro model.

Stiskněte klávesy CTRL+F5 a spusťte aplikaci.

Ověřte, že stránka index videa používá šablonu *Views\Shared\DisplayTemplates\DateTime.cshtml* (červená tučně) a stránka *Movie\Details* používá šablonu *Views\Movies\DisplayTemplates\LoudDateTime.cshtml* (velká a zelená).

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2/_static/image5.png)

V další části vytvoříte šablonu pro komplexní typ.

> [!div class="step-by-step"]
> [Předchozí](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1.md)
> [Další](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3.md)

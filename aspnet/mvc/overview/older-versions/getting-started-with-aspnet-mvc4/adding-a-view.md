---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
title: Přidání zobrazení | Microsoft Docs
author: Rick-Anderson
description: 'Poznámka: v této části je k dispozici aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013. Je to bezpečnější, takže je mnohem jednodušší postupovat a demo...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: dde851d7-882e-4d99-9b96-cf96daed81cc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: 81c2e1f46b08cbc9b5aa5d6c1b36d9d8dc2ba581
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78599748"
---
# <a name="adding-a-view"></a>Přidání zobrazení

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > K [dispozici je](../../getting-started/introduction/getting-started.md) aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013. Je to bezpečnější, mnohem jednodušší a ukazuje více funkcí.

V této části se chystáte upravit třídu `HelloWorldController` tak, aby používala soubory šablon zobrazení k čistě zapouzdření procesu generování odpovědí HTML na klienta.

Vytvoříte soubor šablony zobrazení pomocí [zobrazovacího modulu Razor](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) , který jste zavedli s ASP.NET MVC 3. Šablony zobrazení založené na Razor mají příponu *. cshtml* a poskytují elegantní způsob, jak vytvořit výstup HTML pomocí C#. Razor minimalizuje počet znaků a klávesových úhozů, které jsou požadovány při psaní šablony zobrazení, a umožňuje rychlý a rychlejší pracovní postup kódování.

V současné době metoda `Index` vrací řetězec se zprávou, která je pevně zakódována ve třídě Controller. Změňte metodu `Index` pro vrácení objektu `View`, jak je znázorněno v následujícím kódu:

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

Výše uvedená metoda `Index` používá šablonu zobrazení k vygenerování odpovědi HTML do prohlížeče. Metody kontroleru (známé také jako [metody akcí](http://rachelappel.com/asp.net-mvc-actionresults-explained)), jako je například metoda `Index` výše, obecně vracejí [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (nebo třídu odvozenou z [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)), nikoli primitivní typy, jako je řetězec.

V projektu přidejte šablonu zobrazení, kterou můžete použít s metodou `Index`. Provedete to tak, že kliknete pravým tlačítkem myši do metody `Index` a kliknete na **Přidat zobrazení**.

![](adding-a-view/_static/image1.png)

Zobrazí se dialogové okno **Přidat zobrazení** . Ponechte výchozí nastavení tak, jak jsou, a klikněte na tlačítko **Přidat** :

![](adding-a-view/_static/image2.png)

Vytvoří se složka *MvcMovie\Views\HelloWorld* a soubor *MvcMovie\Views\HelloWorld\Index.cshtml* . Můžete je zobrazit v **Průzkumník řešení**:

![](adding-a-view/_static/image3.png)

Následující příklad ukazuje soubor *index. cshtml* , který byl vytvořen:

![HelloWorldIndex](adding-a-view/_static/image4.png)

Do značky `<h2>` přidejte následující kód HTML.

[!code-html[Main](adding-a-view/samples/sample2.html)]

Úplný soubor *MvcMovie\Views\HelloWorld\Index.cshtml* je uveden níže.

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=7-8)]

Pokud používáte aplikaci Visual Studio 2012, klikněte v Průzkumníku řešení pravým tlačítkem myši na soubor *index. cshtml* a v **okně Kontrola stránky vyberte Zobrazit**.

![PI](adding-a-view/_static/image5.png)

Další informace o tomto novém nástroji najdete v [kurzu pro inspektora stránky](../../views/using-page-inspector-in-aspnet-mvc.md) .

Případně spusťte aplikaci a přejděte k řadiči `HelloWorld` (`http://localhost:xxxx/HelloWorld`). Metoda `Index`a v řadiči neudělala spoustu práce. jednoduše spustil příkaz `return View()`, který určuje, že metoda by měla použít soubor šablony zobrazení k vykreslení odpovědi do prohlížeče. Vzhledem k tomu, že jste explicitně neurčili název souboru šablony zobrazení, který se má použít, ASP.NET MVC se nastaví jako výchozí pro použití souboru zobrazení *index. cshtml* ve složce *\Views\HelloWorld* . Následující obrázek ukazuje řetězec &quot;Hello z naší šablony zobrazení! v zobrazení&quot; pevně zakódované.

![](adding-a-view/_static/image6.png)

Vypadá poměrně dobrý. Všimněte si ale, že záhlaví prohlížeče zobrazuje &quot;index My ASP.NET a&quot; a velký odkaz v horní části stránky říká &quot;na vás.&quot; pod &quot;vaše logo. odkaz&quot; se registruje a přihlásí se a pod ním odkazy na stránky domů, o stránkách kontaktů. Pojďme to změnit.

## <a name="changing-views-and-layout-pages"></a>Změna zobrazení a stránek rozložení

Nejdřív chcete změnit &quot;vaše logo. název&quot; v horní části stránky. Tento text je společný pro každou stránku. V projektu se v současnosti implementuje jenom v jednom místě, i když se objeví na každé stránce aplikace. Do složky */views/Shared* v **Průzkumník řešení** a otevřete soubor *\_layout. cshtml* . Tento soubor se nazývá *Stránka rozložení* a jedná se o sdílené prostředí &quot;&quot;, které používají všechny ostatní stránky.

![_LayoutCshtml](adding-a-view/_static/image7.png)

Šablony rozložení umožňují určit rozložení kontejneru HTML webu na jednom místě a pak ho použít na více stránek na webu. Najděte `@RenderBody()` řádek. `RenderBody` je zástupný symbol, ve kterém se zobrazí všechny stránky specifické pro zobrazení, &quot;zabalené&quot; na stránce rozložení. Pokud například vyberete odkaz o, zobrazení *Views\Home\About.cshtml* se vykreslí v rámci metody `RenderBody`.

Změňte nadpis site-title v šabloně rozložení z &quot;vaše logo&quot; na &quot;filmový&quot;MVC.

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

Obsah elementu title nahraďte následujícím kódem:

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

Spusťte aplikaci a Všimněte si, že nyní říká &quot;filmový &quot;MVC. Klikněte na odkaz **informace** a uvidíte, jak se tato stránka zobrazuje &quot;filmový&quot;MVC. Tuto změnu jsme dokázali udělat v šabloně rozložení a všechny stránky na webu odrážejí nový název.

![](adding-a-view/_static/image8.png)

Teď změníme název zobrazení indexu.

Otevřete *MvcMovie\Views\HelloWorld\Index.cshtml*. Existují dvě místa pro provedení změny: nejprve text, který se zobrazí v názvu prohlížeče, a poté v sekundární hlavičce (`<h2>` element). Mírně se mírně liší, abyste viděli, který bit kódu se změní v rámci aplikace.

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml)]

Chcete-li určit, který název HTML se má zobrazit, kód uvedený výše nastaví vlastnost `Title` objektu `ViewBag` (který je v šabloně zobrazení *index. cshtml* ). Pokud se vrátíte zpět na zdrojový kód šablony rozložení, Všimněte si, že šablona používá tuto hodnotu v prvku `<title>` jako součást `<head>` oddílu HTML, kterou jsme předtím změnili. Pomocí tohoto `ViewBag` přístupu můžete snadno předat další parametry mezi šablonou zobrazení a vaším souborem rozložení.

Spusťte aplikaci a vyhledejte `http://localhost:xx/HelloWorld`. Všimněte si, že se změnil název prohlížeče, primární nadpis a sekundární záhlaví. (Pokud nevidíte změny v prohlížeči, můžete zobrazit obsah uložený v mezipaměti. Stisknutím kombinace kláves CTRL + F5 v prohlížeči vynutíte načtení odpovědi ze serveru.) Název prohlížeče se vytvoří s `ViewBag.Title`, kterou jsme nastavili v šabloně zobrazení *index. cshtml* , a další &quot;filmovou aplikaci,&quot; přidali do souboru rozložení.

Všimněte si také, jak byl obsah v šabloně zobrazení *index. cshtml* sloučen se šablonou zobrazení *\_layout. cshtml* a jedna odpověď HTML byla odeslána do prohlížeče. Šablony rozložení umožňují snadno provádět změny, které se vztahují na všechny stránky aplikace.

![](adding-a-view/_static/image9.png)

Náš malý bit &quot;dat&quot; (v tomto případě &quot;Hello z naší šablony zobrazení!&quot; zpráva) je pevně zakódována, i když. Aplikace MVC má &quot;V&quot; (View) a máte &quot;&quot; C (Controller), ale zatím ne &quot;M&quot; (model). Za chvíli vám ukážeme, jak vytvořit databázi a načíst z ní data modelu.

## <a name="passing-data-from-the-controller-to-the-view"></a>Předávání dat z kontroleru do zobrazení

Než se pustíme do databáze a mluvíme o modelech, můžeme nejdřív mluvit o předávání informací z kontroleru do zobrazení. Třídy kontroleru jsou vyvolány v reakci na příchozí požadavek adresy URL. Třída kontroleru je místo, kde píšete kód, který zpracovává příchozí požadavky prohlížeče, načítá data z databáze a nakonec rozhoduje o tom, jaký typ reakce se má poslat zpátky do prohlížeče. Šablony zobrazení se pak dají použít z kontroleru k vygenerování a formátování odpovědi HTML do prohlížeče.

Řadiče jsou zodpovědné za poskytnutí jakýchkoli dat nebo objektů, aby mohla šablona zobrazení vykreslovat odpověď do prohlížeče. Osvědčeným postupem: **Šablona zobrazení by nikdy neměla provádět obchodní logiku ani pracovat s databází přímo**. Místo toho by šablona zobrazení měla fungovat jenom s daty, která mu poskytl kontroler. Udržování tohoto &quot;oddělení potíží&quot; pomáhá udržet vyčištění kódu, testovatelné a více udržovatelnější.

V současné době metoda `Welcome` Action v `HelloWorldController` třídě přebírá `name` a parametr `numTimes` a pak hodnoty výstupuje přímo do prohlížeče. Místo toho, aby kontroler tuto odpověď vygeneroval jako řetězec, změňte místo toho kontroler tak, aby používal šablonu zobrazení. Šablona zobrazení vygeneruje dynamickou odpověď, což znamená, že před vygenerováním odpovědi musíte předat příslušné bity dat z kontroleru do zobrazení. To můžete provést tak, že řadič umístí dynamická data (parametry), která šablona zobrazení potřebuje, do objektu `ViewBag`, ke kterému bude mít šablona zobrazení přístup.

Vraťte se do souboru *HelloWorldController.cs* a změňte metodu `Welcome`, aby se do objektu `ViewBag` přidala hodnota `Message` a `NumTimes`. `ViewBag` je dynamický objekt, což znamená, že můžete do něj umístit cokoli, co chcete. objekt `ViewBag` nemá žádné definované vlastnosti, dokud do něj nevložíte nějaký text. [Systém vazby modelu ASP.NET MVC](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automaticky mapuje pojmenované parametry (`name` a `numTimes`) z řetězce dotazu v adresním řádku na parametry v metodě. Úplný soubor *HelloWorldController.cs* vypadá takto:

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

Nyní objekt `ViewBag` obsahuje data, která se budou automaticky předávat do zobrazení.

Dále potřebujete šablonu zobrazení Vítejte! V nabídce **sestavení** vyberte **sestavit MvcMovie** a ujistěte se, že je projekt kompilován.

Potom klikněte pravým tlačítkem myši do metody `Welcome` a klikněte na tlačítko **Přidat zobrazení**.

![](adding-a-view/_static/image10.png)

Toto dialogové okno **Přidat zobrazení** vypadá takto:

![](adding-a-view/_static/image11.png)

Klikněte na tlačítko **Přidat**a poté přidejte následující kód pod prvek `<h2>` v novém souboru *Welcome. cshtml* . Vytvoříte smyčku, která říká &quot;Hello&quot; tolikrát, kolikrát by uživatel měl. Úplný soubor *Welcome. cshtml* je uveden níže.

[!code-cshtml[Main](adding-a-view/samples/sample8.cshtml)]

Spusťte aplikaci a přejděte na následující adresu URL:

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

Nyní se data z adresy URL předávají do kontroleru pomocí [pořadače modelů](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx). Kontroler zabalí data do objektu `ViewBag` a předá tento objekt zobrazení. Zobrazení pak zobrazí data jako HTML pro uživatele.

![](adding-a-view/_static/image12.png)

V ukázce výše jsme pomocí objektu `ViewBag` předávali data z kontroleru do zobrazení. V tomto kurzu použijeme model zobrazení k předání dat z kontroleru do zobrazení. Přístup k modelu zobrazení pro předávání dat je obecně mnohem upřednostňovaný nad přístupem k balíčku zobrazení. Další informace najdete v [zobrazeních dynamického typu](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) položky blogu.

Dobře, což bylo druh&quot; &quot;M pro model, ale ne druh databáze. Pojďme pořizovat, co jsme se naučili, a vytvořit databázi filmů.

> [!div class="step-by-step"]
> [Předchozí](adding-a-controller.md)
> [Další](adding-a-model.md)

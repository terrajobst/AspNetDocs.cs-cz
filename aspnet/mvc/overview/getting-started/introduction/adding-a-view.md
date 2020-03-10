---
title: Přidání zobrazení do aplikace MVC
author: Rick-Anderson
description: Přidání zobrazení do aplikace MVC
ms.author: riande
ms.date: 01/23/2019
uid: mvc/overview/getting-started/introduction/adding-a-view
ms.openlocfilehash: 0bc6ac06d12aaee4b2a11c1bf246f9f20f0be017
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582717"
---
# <a name="adding-a-view"></a>Přidání zobrazení

od [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [Tutorial Note](index.md)]

V této části se chystáte upravit třídu `HelloWorldController` tak, aby používala soubory šablon zobrazení k čistě zapouzdření procesu generování odpovědí HTML na klienta. 

Vytvoříte soubor šablony zobrazení pomocí [zobrazovacího modulu Razor](../../../../web-pages/overview/getting-started/introducing-razor-syntax-c.md). Šablony zobrazení založené na Razor mají příponu *. cshtml* a poskytují elegantní způsob, jak vytvořit výstup HTML pomocí C#. Razor minimalizuje počet znaků a klávesových úhozů, které jsou požadovány při psaní šablony zobrazení, a umožňuje rychlý a rychlejší pracovní postup kódování.

V současné době metoda `Index` vrací řetězec se zprávou, která je pevně zakódována ve třídě Controller. Změňte metodu `Index` pro volání metody [zobrazení](/dotnet/api/microsoft.aspnetcore.mvc.controller.view#Microsoft_AspNetCore_Mvc_Controller_View) Controllers, jak je znázorněno v následujícím kódu:

[!code-csharp[Main](adding-a-view/samples/sample1.cs?highlight=1,3)]

Výše uvedená metoda `Index` používá šablonu zobrazení k vygenerování odpovědi HTML do prohlížeče. Metody kontroleru (známé také jako [metody akcí](http://rachelappel.com/asp.net-mvc-actionresults-explained)), jako je například metoda `Index` výše, obecně vracejí [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (nebo třídu odvozenou z [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)), nikoli primitivní typy, jako je řetězec.

Klikněte pravým tlačítkem na složku *Views\HelloWorld* a pak klikněte na **Přidat**a potom na **stránku zobrazení MVC 5 s rozložením (Razor)** .
  
![](adding-a-view/_static/image1.png)   
  
V dialogovém okně **Zadejte název pro položku** zadejte *index*a pak klikněte na **OK**.  
  
![](adding-a-view/_static/image2.png)  
  
V dialogu **Vybrat rozložení stránky** přijměte výchozí **\_layout. cshtml** a klikněte na **OK**.  
  
![](adding-a-view/_static/image3.png)  
  
V dialogovém okně výše se v levém podokně vybere složka *Views\Shared* . Pokud máte vlastní soubor rozložení v jiné složce, můžete ho vybrat. Později v tomto kurzu budeme mluvit o souboru rozložení.

Vytvoří se soubor *MvcMovie\Views\HelloWorld\Index.cshtml* .

![](adding-a-view/_static/image4.png)

Přidejte následující zvýrazněný kód.

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml?highlight=4-11)]

Klikněte pravým tlačítkem na soubor *index. cshtml* a vyberte **Zobrazit v prohlížeči**.

![PI](adding-a-view/_static/image5.png)

Můžete také kliknout pravým tlačítkem na soubor *index. cshtml* a vybrat **Zobrazit v okně Kontrola stránky.** Další informace najdete v [kurzu inspektora stránky](../../views/using-page-inspector-in-aspnet-mvc.md) .

Případně spusťte aplikaci a přejděte k řadiči `HelloWorld` (`http://localhost:xxxx/HelloWorld`). Metoda `Index`a v řadiči neudělala spoustu práce. jednoduše spustil příkaz `return View()`, který určuje, že metoda by měla použít soubor šablony zobrazení k vykreslení odpovědi do prohlížeče. Vzhledem k tomu, že jste explicitně neurčili název souboru šablony zobrazení, který se má použít, ASP.NET MVC se nastaví jako výchozí pro použití souboru zobrazení *index. cshtml* ve složce *\Views\HelloWorld* . Následující obrázek ukazuje řetězec &quot;Hello z naší šablony zobrazení! v zobrazení&quot; pevně zakódované.

![](adding-a-view/_static/image6.png)

Vypadá poměrně dobrý. Všimněte si ale, že v záhlaví prohlížeče se zobrazuje "index – moje aplikace ASP.NET" a velký odkaz v horní části stránky říká "název aplikace". V závislosti na tom, jak malé okno prohlížeče nastavíte, možná budete muset kliknout na tři pruhy v pravém horním rohu, abyste viděli odkazy na **domovskou stránku**, **informace o** **kontaktech**, **registraci** a **přihlášení** .

## <a name="changing-views-and-layout-pages"></a>Změna zobrazení a stránek rozložení

Nejprve je třeba změnit odkaz &quot;název aplikace&quot; v horní části stránky. Tento text je společný pro každou stránku. V projektu se v současnosti implementuje jenom v jednom místě, i když se objeví na každé stránce aplikace. Do složky */views/Shared* v **Průzkumník řešení** a otevřete soubor *\_layout. cshtml* . Tento soubor se nazývá *Stránka rozložení* a je ve sdílené složce, kterou používají všechny ostatní stránky.

![_LayoutCshtml](adding-a-view/_static/image7.png)

Šablony rozložení umožňují určit rozložení kontejneru HTML webu na jednom místě a pak ho použít na více stránek na webu. Najděte `@RenderBody()` řádek. `RenderBody` je zástupný symbol, ve kterém se zobrazí všechny stránky specifické pro zobrazení, &quot;zabalené&quot; na stránce rozložení. Pokud například vyberete odkaz **o** , zobrazení *Views\Home\About.cshtml* se vykreslí v rámci metody `RenderBody`.

Změňte obsah elementu title. Změňte [ActionLink](https://msdn.microsoft.com/library/dd504972(v=vs.108).aspx) v šabloně rozložení z &quot;název aplikace&quot; na &quot;Movie MVC&quot; a kontroler z `Home` na `Movies`. Úplný soubor rozložení je zobrazený níže:

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=6,20)]

Spusťte aplikaci a Všimněte si, že nyní říká &quot;filmový &quot;MVC. Klikněte na odkaz **informace** a uvidíte, jak se tato stránka zobrazuje &quot;filmový&quot;MVC. Tuto změnu jsme dokázali udělat v šabloně rozložení a všechny stránky na webu odrážejí nový název.

![](adding-a-view/_static/image8.png)

Při prvním vytvoření souboru *Views\HelloWorld\Index.cshtml* obsahuje následující kód:

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

Výše uvedený kód Razor explicitně nastavuje stránku rozložení. Projděte si *zobrazení\\souboru _ViewStart. cshtml* , obsahuje přesně stejný kód Razor. *[Zobrazení\\_ViewStart soubor. cshtml](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)* definuje společné rozložení, které budou používat všechna zobrazení, takže můžete odkomentovat nebo odebrat tento kód ze souboru *Views\HelloWorld\Index.cshtml* .

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml?highlight=1-3)]

Pomocí vlastnosti `Layout` můžete nastavit jiné zobrazení rozložení, nebo je nastavit na hodnotu `null`, takže nebude použit žádný soubor rozložení.

Teď změníme název zobrazení indexu.

Otevřete *MvcMovie\Views\HelloWorld\Index.cshtml*. Existují dvě místa pro provedení změny: nejprve text, který se zobrazí v názvu prohlížeče, a poté v sekundární hlavičce (`<h2>` element). Mírně se mírně liší, abyste viděli, který bit kódu se změní v rámci aplikace.

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml?highlight=2,5)]

Chcete-li určit, který název HTML se má zobrazit, kód uvedený výše nastaví vlastnost `Title` objektu `ViewBag` (který je v šabloně zobrazení *index. cshtml* ). Všimněte si, že šablona rozložení ( *Views\Shared\\_Layout. cshtml* ) používá tuto hodnotu v prvku `<title>` jako součást oddílu `<head>` HTML, kterou jsme předtím změnili.

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml?highlight=6)]

Pomocí tohoto `ViewBag` přístupu můžete snadno předat další parametry mezi šablonou zobrazení a vaším souborem rozložení.

Spusťte aplikaci. Všimněte si, že se změnil název prohlížeče, primární nadpis a sekundární záhlaví. (Pokud nevidíte změny v prohlížeči, můžete zobrazit obsah uložený v mezipaměti. Stisknutím kombinace kláves CTRL + F5 v prohlížeči vynutíte načtení odpovědi ze serveru.) Název prohlížeče se vytvoří s `ViewBag.Title`, kterou jsme nastavili v šabloně zobrazení *index. cshtml* , a další &quot;filmovou aplikaci,&quot; přidali do souboru rozložení.

Všimněte si také, jak byl obsah v šabloně zobrazení *index. cshtml* sloučen se šablonou zobrazení *\_layout. cshtml* a jedna odpověď HTML byla odeslána do prohlížeče. Šablony rozložení umožňují snadno provádět změny, které se vztahují na všechny stránky aplikace.

![](adding-a-view/_static/image9.png)

Náš malý bit &quot;dat&quot; (v tomto případě &quot;Hello z naší šablony zobrazení!&quot; zpráva) je pevně zakódována, i když. Aplikace MVC má &quot;V&quot; (View) a máte &quot;&quot; C (Controller), ale zatím ne &quot;M&quot; (model). Za chvíli vám ukážeme, jak vytvořit databázi a načíst z ní data modelu.

## <a name="passing-data-from-the-controller-to-the-view"></a>Předávání dat z kontroleru do zobrazení

Než se pustíme do databáze a mluvíme o modelech, můžeme nejdřív mluvit o předávání informací z kontroleru do zobrazení. Třídy kontroleru jsou vyvolány v reakci na příchozí požadavek adresy URL. Třída kontroleru je místo, kde píšete kód, který zpracovává příchozí požadavky prohlížeče, načítá data z databáze a nakonec rozhoduje o tom, jaký typ reakce se má poslat zpátky do prohlížeče. Šablony zobrazení se pak dají použít z kontroleru k vygenerování a formátování odpovědi HTML do prohlížeče.

Řadiče jsou zodpovědné za poskytnutí jakýchkoli dat nebo objektů, aby mohla šablona zobrazení vykreslovat odpověď do prohlížeče. Osvědčeným postupem: **Šablona zobrazení by nikdy neměla provádět obchodní logiku ani pracovat s databází přímo**. Místo toho by šablona zobrazení měla fungovat jenom s daty, která mu poskytl kontroler. Udržování tohoto &quot;oddělení potíží&quot; pomáhá udržet vyčištění kódu, testovatelné a více udržovatelnější.

V současné době metoda `Welcome` Action v `HelloWorldController` třídě přebírá `name` a parametr `numTimes` a pak hodnoty výstupuje přímo do prohlížeče. Místo toho, aby kontroler tuto odpověď vygeneroval jako řetězec, změňte místo toho kontroler tak, aby používal šablonu zobrazení. Šablona zobrazení vygeneruje dynamickou odpověď, což znamená, že před vygenerováním odpovědi musíte předat příslušné bity dat z kontroleru do zobrazení. To můžete provést tak, že řadič umístí dynamická data (parametry), která šablona zobrazení potřebuje, do objektu `ViewBag`, ke kterému bude mít šablona zobrazení přístup.

Vraťte se do souboru *HelloWorldController.cs* a změňte metodu `Welcome`, aby se do objektu `ViewBag` přidala hodnota `Message` a `NumTimes`. `ViewBag` je dynamický objekt, což znamená, že můžete do něj umístit cokoli, co chcete. objekt `ViewBag` nemá žádné definované vlastnosti, dokud do něj nevložíte nějaký text. [Systém vazby modelu ASP.NET MVC](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automaticky mapuje pojmenované parametry (`name` a `numTimes`) z řetězce dotazu v adresním řádku na parametry v metodě. Úplný soubor *HelloWorldController.cs* vypadá takto:

[!code-csharp[Main](adding-a-view/samples/sample8.cs)]

Nyní objekt `ViewBag` obsahuje data, která se budou automaticky předávat do zobrazení. Dále potřebujete šablonu zobrazení Vítejte! V nabídce **sestavení** vyberte **Sestavit řešení** (nebo CTRL + SHIFT + B) a ujistěte se, že je projekt kompilován. Klikněte pravým tlačítkem na složku *Views\HelloWorld* a pak klikněte na **Přidat**a potom na **stránku zobrazení MVC 5 s rozložením (Razor)** .
  
![](adding-a-view/_static/image10.png)   
  
V dialogovém okně **Zadejte název pro položku** zadejte *Welcome*a pak klikněte na **OK**.   
  
V dialogu **Vybrat rozložení stránky** přijměte výchozí **\_layout. cshtml** a klikněte na **OK**.  
  
![](adding-a-view/_static/image11.png)   

Vytvoří se soubor *MvcMovie\Views\HelloWorld\Welcome.cshtml* .

Nahraďte značku v souboru *Welcome. cshtml* . Vytvoříte smyčku, která říká &quot;Hello&quot; tolikrát, kolikrát by uživatel měl. Úplný soubor *Welcome. cshtml* je uveden níže.

[!code-cshtml[Main](adding-a-view/samples/sample9.cshtml)]

Spusťte aplikaci a přejděte na následující adresu URL:

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

Nyní se data z adresy URL předávají do kontroleru pomocí [pořadače modelů](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx). Kontroler zabalí data do objektu `ViewBag` a předá tento objekt zobrazení. Zobrazení pak zobrazí data jako HTML pro uživatele.

![](adding-a-view/_static/image12.png)

V ukázce výše jsme pomocí objektu `ViewBag` předávali data z kontroleru do zobrazení. Později v tomto kurzu použijeme model zobrazení k předání dat z kontroleru do zobrazení. Přístup k modelu zobrazení pro předávání dat je obecně mnohem upřednostňovaný nad přístupem k balíčku zobrazení. Další informace najdete v [zobrazeních dynamického typu](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) položky blogu. 

Dobře, což bylo druh&quot; &quot;M pro model, ale ne druh databáze. Pojďme pořizovat, co jsme se naučili, a vytvořit databázi filmů.

> [!div class="step-by-step"]
> [Předchozí](adding-a-controller.md)
> [Další](adding-a-model.md)

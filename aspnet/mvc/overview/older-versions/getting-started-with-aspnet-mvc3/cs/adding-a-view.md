---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
title: Přidání zobrazení (C#) | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, který je...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: abc7c78d-cb09-4a4c-a887-61bc401d40e3
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: b4a1316feb8d9b7f3ef5ca4755bf1cc5b23e6ef9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78615470"
---
# <a name="adding-a-view-c"></a>Přidání zobrazení (C#)

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > K [dispozici je](../../../getting-started/introduction/getting-started.md) aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013. Je to bezpečnější, mnohem jednodušší a ukazuje více funkcí.
> 
> 
> V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, což je bezplatná verze Microsoft Visual Studio. Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže. Všechny z nich můžete nainstalovat kliknutím na následující odkaz: instalace [webové platformy](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Případně můžete požadavky jednotlivě nainstalovat pomocí následujících odkazů:
> 
> - [Požadavky sady Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Aktualizace nástrojů MVC 3 pro ASP.NET](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(podpora modulu runtime + nástroje)
> 
> Pokud používáte sadu Visual Studio 2010 místo sady Visual Web Developer 2010, nainstalujte požadavky kliknutím na následující odkaz: sady [Visual studio 2010 požadavky](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Projekt Visual Web Developer se C# zdrojovým kódem je k dispozici pro toto téma. [Stáhněte si C# verzi](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Pokud dáváte přednost Visual Basic, přepněte se na [Visual Basic verzi](../vb/intro-to-aspnet-mvc-3.md) tohoto kurzu.

V této části se chystáte upravit třídu `HelloWorldController` tak, aby používala soubory šablon zobrazení k čistě zapouzdření procesu generování odpovědí HTML na klienta.

Vytvoříte soubor šablony zobrazení pomocí nového zobrazovacího [modulu Razor](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) , který jste zavedli s ASP.NET MVC 3. Šablony zobrazení založené na Razor mají příponu *. cshtml* a poskytují elegantní způsob, jak vytvořit výstup HTML pomocí C#. Razor minimalizuje počet znaků a klávesových úhozů, které jsou požadovány při psaní šablony zobrazení, a umožňuje rychlý a rychlejší pracovní postup kódování.

Začněte tím, že použijete šablonu zobrazení s metodou `Index` ve třídě `HelloWorldController`. V současné době metoda `Index` vrací řetězec se zprávou, která je pevně zakódována ve třídě Controller. Změňte metodu `Index` pro vrácení objektu `View`, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

Tento kód používá šablonu zobrazení k vygenerování odpovědi HTML do prohlížeče. V projektu přidejte šablonu zobrazení, kterou můžete použít s metodou `Index`. Provedete to tak, že kliknete pravým tlačítkem myši do metody `Index` a kliknete na **Přidat zobrazení**.

![](adding-a-view/_static/image1.png)

Zobrazí se dialogové okno **Přidat zobrazení** . Ponechte výchozí nastavení tak, jak jsou, a klikněte na tlačítko **Přidat** :

![](adding-a-view/_static/image2.png)

Vytvoří se složka *MvcMovie\Views\HelloWorld* a soubor *MvcMovie\Views\HelloWorld\Index.cshtml* . Můžete je zobrazit v **Průzkumník řešení**:

![](adding-a-view/_static/image3.png)

Následující příklad ukazuje soubor *index. cshtml* , který byl vytvořen:

[![HelloWorldIndex](adding-a-view/_static/image5.png)](adding-a-view/_static/image4.png)

Přidejte kód HTML pod značku `<h2>`. Upravený soubor *MvcMovie\Views\HelloWorld\Index.cshtml* se zobrazuje níže.

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml)]

Spusťte aplikaci a přejděte k řadiči `HelloWorld` (`http://localhost:xxxx/HelloWorld`). Metoda `Index`a v řadiči neudělala spoustu práce. jednoduše spustil příkaz `return View()`, který určuje, že metoda by měla použít soubor šablony zobrazení k vykreslení odpovědi do prohlížeče. Vzhledem k tomu, že jste explicitně neurčili název souboru šablony zobrazení, který se má použít, ASP.NET MVC se nastaví jako výchozí pro použití souboru zobrazení *index. cshtml* ve složce *\Views\HelloWorld* . Následující obrázek znázorňuje řetězec pevně kódovaný v zobrazení.

![](adding-a-view/_static/image6.png)

Vypadá poměrně dobrý. Všimněte si ale, že záhlaví prohlížeče říká "index" a velký nadpis na stránce říká "Moje aplikace MVC". Pojďme je změnit.

## <a name="changing-views-and-layout-pages"></a>Změna zobrazení a stránek rozložení

Nejdřív chcete v horní části stránky změnit název moje aplikace MVC. Tento text je společný pro každou stránku. Ve skutečnosti je implementována pouze v jednom místě v projektu, i když se zobrazuje na všech stránkách aplikace. Do složky */views/Shared* v **Průzkumník řešení** a otevřete soubor *\_layout. cshtml* . Tento soubor se nazývá *Stránka rozložení* a je to sdílené prostředí "shell", které používají všechny ostatní stránky.

[![_LayoutCshtml](adding-a-view/_static/image8.png)](adding-a-view/_static/image7.png)

Šablony rozložení umožňují určit rozložení kontejneru HTML webu na jednom místě a pak ho použít na více stránek na webu. Poznamenejte si `@RenderBody()` řádek poblíž konce souboru. `RenderBody` je zástupný symbol, kde jsou všechny stránky specifické pro zobrazení, které vytvoříte, zobrazeny na stránce rozložení, "zabaleno". Změňte záhlaví nadpisu v šabloně rozložení z "Moje aplikace MVC" na "MVC Movie App".

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml)]

Spusťte aplikaci a Všimněte si, že teď říká "MVC Movie App". Klikněte na odkaz **informace** a uvidíte, jak se na této stránce zobrazuje zpráva "MVC Movie App". Tuto změnu jsme dokázali udělat v šabloně rozložení a všechny stránky na webu odrážejí nový název.

![](adding-a-view/_static/image9.png)

Úplný soubor *\_layout. cshtml* je uveden níže:

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

Teď změňte název stránky indexu (zobrazení).

Otevřete *MvcMovie\Views\HelloWorld\Index.cshtml*. Existují dvě místa pro provedení změny: nejprve text, který se zobrazí v názvu prohlížeče, a poté v sekundární hlavičce (`<h2>` element). Mírně se mírně liší, abyste viděli, který bit kódu se změní v rámci aplikace.

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

Chcete-li určit, který název HTML se má zobrazit, kód uvedený výše nastaví vlastnost `Title` objektu `ViewBag` (který je v šabloně zobrazení *index. cshtml* ). Pokud se vrátíte zpět na zdrojový kód šablony rozložení, Všimněte si, že šablona používá tuto hodnotu v prvku `<title>` jako součást `<head>` oddílu HTML. Pomocí tohoto přístupu můžete snadno předat další parametry mezi šablonou zobrazení a vaším souborem rozložení.

Spusťte aplikaci a vyhledejte `http://localhost:xx/HelloWorld`. Všimněte si, že se změnil název prohlížeče, primární nadpis a sekundární záhlaví. (Pokud nevidíte změny v prohlížeči, můžete zobrazit obsah uložený v mezipaměti. Stisknutím kombinace kláves CTRL + F5 v prohlížeči vynutíte načtení odpovědi ze serveru.)

Všimněte si také, jak byl obsah v šabloně zobrazení *index. cshtml* sloučen se šablonou zobrazení *\_layout. cshtml* a jedna odpověď HTML byla odeslána do prohlížeče. Šablony rozložení umožňují snadno provádět změny, které se vztahují na všechny stránky aplikace.

![](adding-a-view/_static/image10.png)

Náš malý bit "data" (v tomto případě "Hello z naší šablony zobrazení" zpráva) je pevně zakódována, i když. Aplikace MVC má "V" (zobrazení) a Vy máte "C" (Controller), ale zatím ne "M" (model). Za chvíli vám ukážeme, jak vytvořit databázi a načíst z ní data modelu.

## <a name="passing-data-from-the-controller-to-the-view"></a>Předávání dat z kontroleru do zobrazení

Než se pustíme do databáze a mluvíme o modelech, můžeme nejdřív mluvit o předávání informací z kontroleru do zobrazení. Třídy kontroleru jsou vyvolány v reakci na příchozí požadavek adresy URL. Třída kontroleru je místo, kde píšete kód, který zpracovává příchozí parametry, načítá data z databáze a nakonec rozhoduje o tom, jaký typ reakce se má poslat zpátky do prohlížeče. Šablony zobrazení se pak dají použít z kontroleru k vygenerování a formátování odpovědi HTML do prohlížeče.

Řadiče jsou zodpovědné za poskytnutí jakýchkoli dat nebo objektů, aby mohla šablona zobrazení vykreslovat odpověď do prohlížeče. Šablona zobrazení by nikdy neměla provádět obchodní logiku ani pracovat s databází přímo. Místo toho by měla fungovat jenom s daty, která mu poskytl kontroler. Udržování tohoto "oddělení obav" pomáhá udržet vyčištění kódu a více udržovatelnější.

V současné době metoda `Welcome` Action v `HelloWorldController` třídě přebírá `name` a parametr `numTimes` a pak hodnoty výstupuje přímo do prohlížeče. Místo toho, aby kontroler tuto odpověď vygeneroval jako řetězec, změňte místo toho kontroler tak, aby používal šablonu zobrazení. Šablona zobrazení vygeneruje dynamickou odpověď, což znamená, že před vygenerováním odpovědi musíte předat příslušné bity dat z kontroleru do zobrazení. Můžete to udělat tak, že řadič umístí dynamická data, která šablona zobrazení potřebuje, do objektu `ViewBag`, ke kterému bude mít šablona zobrazení přístup.

Vraťte se do souboru *HelloWorldController.cs* a změňte metodu `Welcome`, aby se do objektu `ViewBag` přidala hodnota `Message` a `NumTimes`. `ViewBag` je dynamický objekt, což znamená, že můžete do něj umístit cokoli, co chcete. objekt `ViewBag` nemá žádné definované vlastnosti, dokud do něj nevložíte nějaký text. Úplný soubor *HelloWorldController.cs* vypadá takto:

[!code-csharp[Main](adding-a-view/samples/sample6.cs)]

Nyní objekt `ViewBag` obsahuje data, která se budou automaticky předávat do zobrazení.

Dále potřebujete šablonu zobrazení Vítejte! V nabídce **ladění** vyberte **sestavit MvcMovie** a ujistěte se, že je projekt kompilován.

[![BuildHelloWorld](adding-a-view/_static/image12.png)](adding-a-view/_static/image11.png)

Potom klikněte pravým tlačítkem myši do metody `Welcome` a klikněte na tlačítko **Přidat zobrazení**. Toto dialogové okno **Přidat zobrazení** vypadá takto:

![](adding-a-view/_static/image13.png)

Klikněte na tlačítko **Přidat**a poté přidejte následující kód pod prvek `<h2>` v novém souboru *Welcome. cshtml* . Vytvoříte smyčku, která říká "Hello" tolikrát, kolikrát by uživatel měl. Úplný soubor *Welcome. cshtml* je uveden níže.

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml)]

Spusťte aplikaci a přejděte na následující adresu URL:

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

Nyní se data z adresy URL předávají a automaticky předají do kontroleru. Kontroler zabalí data do objektu `ViewBag` a předá tento objekt zobrazení. Zobrazení pak zobrazí data jako HTML pro uživatele.

![](adding-a-view/_static/image14.png)

Dobře, což bylo druh "M" pro model, ale ne druh databáze. Pojďme pořizovat, co jsme se naučili, a vytvořit databázi filmů.

> [!div class="step-by-step"]
> [Předchozí](adding-a-controller.md)
> [Další](adding-a-model.md)

---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
title: Přidání zobrazení (VB) | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, který je...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: d3633f64-5d3c-45c9-ae4b-cb1563e3739f
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: fa200935d83bb26c07b302449a6eba6fd67b5322
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457309"
---
# <a name="adding-a-view-vb"></a>Přidání zobrazení (VB)

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, což je bezplatná verze Microsoft Visual Studio. Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže. Všechny z nich můžete nainstalovat kliknutím na následující odkaz: instalace [webové platformy](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Případně můžete požadavky jednotlivě nainstalovat pomocí následujících odkazů:
> 
> - [Požadavky sady Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Aktualizace nástrojů MVC 3 pro ASP.NET](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(podpora modulu runtime + nástroje)
> 
> Pokud používáte sadu Visual Studio 2010 místo sady Visual Web Developer 2010, nainstalujte požadavky kliknutím na následující odkaz: sady [Visual studio 2010 požadavky](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Projekt Visual Web Developer s VB.NET zdrojovým kódem je k dispozici pro toto téma. [Stáhněte si verzi VB.NET](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Pokud dáváte přednost C#, přepněte se na [ C# verzi](../cs/adding-a-view.md) tohoto kurzu.

V této části provedeme úpravu třídy `HelloWorldController` tak, aby používala soubor šablony zobrazení k čistě zapouzdření procesu generování odpovědí HTML na klienta.

Pojďme začít pomocí šablony zobrazení s metodou `Index` ve třídě `HelloWorldController`. V současné době metoda `Index` vrací řetězec se zprávou, která je pevně zakódována v rámci třídy Controller. Změňte metodu `Index` pro vrácení objektu `View`, jak je znázorněno v následujícím příkladu:

[!code-vb[Main](adding-a-view/samples/sample1.vb)]

Teď přidáme šablonu zobrazení do našeho projektu, který můžeme vyvolat pomocí metody `Index`. Provedete to tak, že kliknete pravým tlačítkem myši do metody `Index` a kliknete na **Přidat zobrazení**.

[![IndexAddView](adding-a-view/_static/image2.png "IndexAddView")](adding-a-view/_static/image1.png)

Zobrazí se dialogové okno **Přidat zobrazení** . Ponechte výchozí položky a klikněte na tlačítko **Přidat** .

[![3addView](adding-a-view/_static/image4.png "3addView")](adding-a-view/_static/image3.png)

Vytvoří se složka *MvcMovie\Views\HelloWorld* a soubor *MvcMovie\Views\HelloWorld\Index.vbhtml* . Můžete je zobrazit v **Průzkumník řešení**:

[![SolnExpHelloWorldIndx](adding-a-view/_static/image6.png "SolnExpHelloWorldIndx")](adding-a-view/_static/image5.png)

Přidejte kód HTML pod značku `<h2>`. Upravený soubor *MvcMovie\Views\HelloWorld\Index.vbhtml* se zobrazuje níže.

[!code-vbhtml[Main](adding-a-view/samples/sample2.vbhtml)]

Spusťte aplikaci a vyhledejte &quot;Hello World&quot; Controller (`http://localhost:xxxx/HelloWorld`). Metoda `Index`a v řadiči neudělala spoustu práce. jednoduše spustil příkaz `return View()`, který indikuje, že jsme chtěli použít soubor šablony zobrazení k vykreslování odpovědi klientovi. Vzhledem k tomu, že jsme explicitně neurčili název souboru šablony zobrazení, který se má použít, ASP.NET MVC se nastaví jako výchozí pro použití souboru zobrazení *index. vbhtml* ve složce *\Views\HelloWorld* . Následující obrázek znázorňuje řetězec pevně kódovaný v zobrazení.

[![3HelloWorld](adding-a-view/_static/image8.png "3HelloWorld")](adding-a-view/_static/image7.png)

Vypadá poměrně dobrý. Všimněte si ale, že záhlaví prohlížeče říká &quot;&quot; indexu a na stránce se říká &quot;moje aplikace MVC.&quot; je můžeme změnit.

## <a name="changing-views-and-layout-pages"></a>Změna zobrazení a stránek rozložení

Nejprve změňte text &quot;moje aplikace MVC.&quot;, že se text sdílí a zobrazí se na každé stránce. Ve skutečnosti se zobrazí pouze v jednom místě v našem projektu, a to i v případě, že se nachází na každé stránce v naší aplikaci. Do složky */views/Shared* v **Průzkumník řešení** a otevřete soubor *\_layout. vbhtml* . Tento soubor se nazývá stránka rozložení a jedná se o sdílené prostředí &quot;&quot;, které používají všechny ostatní stránky.

Poznamenejte si `@RenderBody()` řádek kódu poblíž konce souboru. `RenderBody` je zástupný symbol, ve kterém se zobrazí všechny stránky, které vytvoříte, &quot;zabalené&quot; na stránce rozložení. Změňte nadpis `<h1>` z **&quot;** moje aplikace MVC&quot; na &quot;filmových aplikací MVC&quot;.

[!code-html[Main](adding-a-view/samples/sample3.html)]

Spusťte aplikaci a poznamenejte si ji nyní &quot;&quot;filmových aplikací MVC. Klikněte na odkaz **o** stránku a tato stránka zobrazuje &quot;&quot;filmových aplikací MVC.

Úplný soubor *\_layout. vbhtml* se zobrazuje níže:

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

Teď změňte název stránky indexu (zobrazení).

[!code-vbhtml[Main](adding-a-view/samples/sample5.vbhtml)]

Otevřete *MvcMovie\Views\HelloWorld\Index.vbhtml*. Existují dvě místa pro provedení změny: nejprve text, který se zobrazí v názvu prohlížeče, a poté v sekundární hlavičce (`<h2>` element). Vytvoříme je trochu jinak, abyste viděli, který bit kódu se změní v rámci aplikace.

Spusťte aplikaci a vyhledejte`http://localhost:xx/HelloWorld`. Všimněte si, že se změnil název prohlížeče, primární nadpis a sekundární záhlaví. V aplikaci je snadné dělat velké změny s malými změnami v zobrazení. (Pokud nevidíte změny v prohlížeči, můžete zobrazit obsah uložený v mezipaměti. Stisknutím kombinace kláves CTRL + F5 v prohlížeči vynutíte načtení odpovědi ze serveru.)

[![3_MyMovieList](adding-a-view/_static/image10.png "3_MyMovieList")](adding-a-view/_static/image9.png)

Náš malý bit &quot;dat&quot; (v tomto případě &quot;zpráva Hello World!&quot;) je pevně zakódována, i když. Naše aplikace MVC má V (zobrazeních) a my máme C (Controllers), ale ještě ne M (model). Za chvíli vám ukážeme, jak vytvořit databázi a načíst z ní data modelu.

## <a name="passing-data-from-the-controller-to-the-view"></a>Předávání dat z kontroleru do zobrazení

Než se pustíme do databáze a mluvíme o modelech, můžeme nejdřív mluvit o předávání informací z kontroleru do zobrazení. Chceme předat, co šablona zobrazení vyžaduje, aby bylo možné vykreslit odpověď HTML klientovi. Tyto objekty jsou obvykle vytvořeny a předávány třídou Controller do šablony zobrazení a měly by obsahovat pouze data, která šablona zobrazení vyžaduje – a žádné další.

Dříve s `HelloWorldController`ovou třídou prováděla metoda `Welcome` akce `name` a parametr `numTimes` a pak nastavila výstup hodnot parametrů do prohlížeče. Místo toho, aby kontroler pokračoval přímo v vykreslování této odpovědi, pojďme místo toho tato data vložit do kontejneru pro zobrazení. Řadiče a zobrazení mohou použít objekt `ViewBag` k uložení těchto dat. Ta se předává do šablony zobrazení automaticky a používá se k vykreslování odpovědi HTML pomocí obsahu kontejneru jako data. Tímto způsobem se na řadič zajímá jedna věc a šablona zobrazení s jiným. díky tomu můžeme udržovat čisté &quot;oddělení potíží, které&quot; v rámci aplikace.

Alternativně můžeme definovat vlastní třídu a pak vytvořit instanci tohoto objektu na vlastní, vyplnit ji daty a předat ji do zobrazení. Často se označuje jako ViewModel, protože se jedná o vlastní model pro zobrazení. Pro malé objemy dat ale ViewBag funguje skvěle.

Vraťte se do souboru *HelloWorldController. vb* a změňte metodu `Welcome` v řadiči k vložení zprávy a NumTimes do ViewBag. ViewBag je dynamický objekt. To znamená, že do něho můžete přidat cokoli, co chcete. ViewBag nemá žádné definované vlastnosti, dokud do něj nevložíte nějaký text.

Kompletní `HelloWorldController.vb` s novou třídou ve stejném souboru.

[!code-vb[Main](adding-a-view/samples/sample6.vb)]

Naše ViewBag nyní obsahuje data, která se budou automaticky předávat do zobrazení. Případně jsme mohli úspěšně předat náš vlastní objekt, například to, pokud se mi líbilo:

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

Teď potřebujeme šablonu `WelcomeView`! Spusťte aplikaci, aby byl nový kód zkompilován. Zavřete prohlížeč, klikněte pravým tlačítkem myši uvnitř metody `Welcome` a pak klikněte na **Přidat zobrazení**.

Vaše dialogové okno **Přidat zobrazení** vypadá takto.

[![3AddWelcomeView](adding-a-view/_static/image12.png "3AddWelcomeView")](adding-a-view/_static/image11.png)

Do prvku `<h2>` v novém <em>uvítacím</em> elementu přidejte následující kód. soubor vbhtml. Provedeme smyčku a řekněme, že &quot;Hello&quot; tolikrát, kolikrát bychom měli.

[!code-vbhtml[Main](adding-a-view/samples/sample8.vbhtml)]

Spusťte aplikaci a přejděte na `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

Nyní se data z adresy URL předávají a automaticky předají do kontroleru. Kontroler zabalí data do objektu `Model` a předá tento objekt zobrazení. Zobrazení, než zobrazuje data jako HTML pro uživatele.

[![3Hello_Scott_4](adding-a-view/_static/image14.png "3Hello_Scott_4")](adding-a-view/_static/image13.png)

Dobře, což bylo druh&quot; &quot;M pro model, ale ne druh databáze. Pojďme pořizovat, co jsme se naučili, a vytvořit databázi filmů.

> [!div class="step-by-step"]
> [Předchozí](adding-a-controller.md)
> [Další](adding-a-model.md)

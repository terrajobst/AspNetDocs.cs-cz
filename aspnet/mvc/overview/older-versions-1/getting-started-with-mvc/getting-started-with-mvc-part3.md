---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
title: Přidání zobrazení | Microsoft Docs
author: shanselman
description: Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvořte jednoduchou webovou aplikaci, která čte a zapisuje z databáze.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: e8f1515c-c277-47ff-a23e-224118f13f02
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
msc.type: authoredcontent
ms.openlocfilehash: 462b1210c45da67058899193afcea973f3daf122
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581555"
---
# <a name="adding-a-view"></a>Přidání zobrazení

[Scott Hanselman](https://github.com/shanselman)

> Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvoříte jednoduchou webovou aplikaci, která čte a zapisuje z databáze. Navštivte [centrum učení služby ASP.NET MVC](../../../index.md) , kde najdete další kurzy a ukázky pro ASP.NET MVC.

V této části se podíváme na to, jak můžeme mít naši třídu HelloWorldController k čistě zapouzdření generování odpovědí HTML zpět do klienta, pomocí souboru šablony zobrazení.

Pojďme začít pomocí šablony zobrazení pomocí našeho způsobu indexování. Naše metoda se nazývá index a je v HelloWorldController. V současné době metoda index () vrací řetězec se zprávou, která je pevně zakódované v rámci třídy Controller.

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample1.cs)]

Pojďme teď změnit metodu indexu na místo toho, aby vypadala takto:

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample2.cs)]

Teď přidáme šablonu zobrazení do našeho projektu, který můžeme použít pro metodu indexu (). Provedete to tak, že kliknete pravým tlačítkem myši někam do středu metody indexu a kliknete na Přidat zobrazení...

![image](getting-started-with-mvc-part3/_static/image1.png)

Tím se zobrazí dialogové okno Přidat zobrazení, ve kterém jsou uvedeny některé možnosti, jak chceme vytvořit šablonu zobrazení, kterou může použít naše metoda indexu. Prozatím nic neměňte a stačí kliknout na tlačítko Přidat.

[Dialog ![přidat zobrazení](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)

Po kliknutí na tlačítko Přidat se ve složce řešení zobrazí nová složka a nový soubor, jak je vidět zde. Nyní mám složku HelloWorld v nabídce zobrazení a soubor index. aspx v této složce.

[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)

Nový indexový soubor je už otevřený a připravený k úpravám. Do prvního &lt;H2&gt;indexu přidejte nějaký text&lt;/H2&gt; například "Hello World".

[!code-html[Main](getting-started-with-mvc-part3/samples/sample3.html)]

Spusťte aplikaci a v prohlížeči se znovu Podívejte [`http://localhost:xx/HelloWorld`](http://localhostxx) . Metoda index na našem řadiči v tomto příkladu neudělala žádnou práci, ale volala "návratové zobrazení ()", což znamenalo, že jsme chtěli použít soubor šablony zobrazení k vykreslení odpovědi zpátky klientovi. Vzhledem k tomu, že jsme explicitně neurčili název souboru šablony zobrazení, který se má použít, ASP.NET MVC se nastaví jako výchozí pro použití souboru zobrazení index. aspx ve složce \Views\HelloWorld. Nyní se zobrazí řetězec, který je pevně kódovaný v našem zobrazení.

[![– index – Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)

Vypadá poměrně dobrý. Všimněte si ale, že název prohlížeče říká "index" a velký nadpis na stránce říká "Moje aplikace MVC". Pojďme je změnit.

### <a name="changing-views-and-master-pages"></a>Změna zobrazení a stránek předlohy

Nejprve změňte text "Moje aplikace MVC". Tento text se sdílí a zobrazí se na každé stránce. Ve skutečnosti se zobrazí pouze v jednom místě v našem kódu, a to i v případě, že je na každé stránce v naší aplikaci. Do složky/Views/Shared v Průzkumník řešení a otevřete soubor Web. Master. Tento soubor se nazývá hlavní stránka a je to sdílené prostředí "shell", které používají všechny ostatní stránky.

V tomto souboru si všimněte textu, který říká ContentPlaceholder "MainContent".

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample4.aspx)]

Tento zástupný symbol je místo, kde se na stránce předlohy zobrazí všechny stránky, které vytvoříte. Zkuste změnit název a potom spustit aplikaci a navštívit více stránek. Všimněte si, že se jedna změna zobrazuje na více stránkách.

[!code-html[Main](getting-started-with-mvc-part3/samples/sample5.html)]

Teď bude mít každá stránka primární nadpis, který je H1 z mé filmové aplikace MVC. , Který zpracovává bílý text na nejvyšší úrovni, který je sdílen na všech stránkách.

Tady je web. Master v celém rozsahu s naším změněným názvem:

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample6.aspx)]

Teď změníme název stránky indexu.

Otevřít/HelloWorld/Index.aspx. Existují dvě místa ke změně. Nejprve se zobrazí název, který se zobrazí v názvu prohlížeče, a pak také v sekundární hlavičce – to je H2. Povedou se o něco trochu jinak, abyste viděli, který bit kódu se změní v rámci aplikace.

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample7.aspx)]

Spusťte aplikaci a navštivte/Movies. Všimněte si, že se změnil název prohlížeče, primární nadpis a sekundární záhlaví. V aplikaci je snadné dělat velké změny s malými změnami v zobrazení.

[![seznam filmů – Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)

Náš malý bit "data" (v tomto případě "Hello World!" zpráva) byla pevně zakódována. Máme V (zobrazeních) a my máme C (Controllers), ale ještě ne M (model). Brzy si projdeme, jak vytvořit databázi a načíst z ní data modelu.

## <a name="passing-a-viewmodel"></a>Předávání ViewModel

Než se pustíme do databáze a mluvíme o modelech, můžeme nejdřív mluvit o "ViewModels". Jedná se o objekty, které představují, co šablona zobrazení vyžaduje k vykreslení odpovědi HTML zpátky na klienta. Obvykle jsou vytvořeny a předávány třídou Controller na šablonu zobrazení a měly by obsahovat pouze data, která šablona zobrazení vyžaduje, a ne další.

V předchozích příkladech HelloWorld mohl naše úvodní () metoda akce název a parametr numTimes a výstup do prohlížeče. Místo toho, aby kontrolér mohl i nadále vykreslovat tuto odpověď, je místo toho třeba vytvořit malou třídu pro uchování těchto dat a pak ji předat do šablony zobrazení, aby bylo možné vrátit odpověď HTML pomocí ní. Tímto způsobem se kontroler má jedna věc a druhá šablona zobrazení. díky tomu můžeme v rámci naší aplikace udržovat čisté "oddělení obav".

Vraťte se do souboru HelloWorldController.cs a přidejte novou třídu "WelcomeViewModel" a změňte metodu Welcome v rámci kontroleru. Tady je kompletní HelloWorldController.cs s novou třídou ve stejném souboru.

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample8.cs)]

I když je na více řádcích, naše metoda Welcome je ve skutečnosti pouze dva příkazy kódu. První příkaz zabalí naše dva parametry do objektu ViewModel a druhý předává výsledný objekt do zobrazení.

Teď potřebujeme šablonu zobrazení Welcome! Klikněte pravým tlačítkem na úvodní metodu a vyberte Přidat zobrazení. Tentokrát zkontrolujeme "vytvořit zobrazení silného typu" a v rozevíracím seznamu vyberte naši třídu WelcomeViewModel. Toto nové zobrazení bude znát pouze o WelcomeViewModels a žádné jiné typy objektů.

> *Poznámka: po přidání WelcomeViewModel pro zobrazení v rozevíracím seznamu budete muset zkompilovat.*

Zobrazí se dialogové okno Přidat zobrazení, které by mělo vypadat takto. Klikněte na tlačítko Přidat. ![Přidat zobrazení v kruhu](getting-started-with-mvc-part3/_static/image10.png)

Přidejte tento kód pod &lt;H2&gt; v novém Welcome. aspx. Provedeme smyčku a řekněte nám to, kolikrát by uživatel měl.

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample9.aspx)]

Všimněte si také, že zadáváte to, protože jsme si dozvěděli toto zobrazení o WelcomeViewModel (jsou to svatby, nezapomeňte?), že při každém odkazování na náš objekt modelu, jak je vidět na následujícím snímku obrazovky, máme užitečnou technologii IntelliSense:

[Zdrojový kód ![NumTime](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)

Spusťte aplikaci a znovu navštivte `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`. Nyní přijímáme data z adresy URL, která se předává do našeho kontroleru. náš kontroler data zabalí do ViewModel a předá tento objekt do našeho zobrazení. Zobrazení, než zobrazuje data jako HTML pro uživatele.

[![Welcome – Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)

Dobře, což bylo druh "M" pro model, ale ne druh databáze. Pojďme pořizovat, co jsme se naučili, a vytvořit databázi filmů.

> [!div class="step-by-step"]
> [Předchozí](getting-started-with-mvc-part2.md)
> [Další](getting-started-with-mvc-part4.md)

---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
title: Úvod do ASP.NET MVC 3 (C#) | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, který je...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 86a80b35-88bd-4b7c-bd58-f6e7997197d4
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: e71275c93558c0b6ca087a145786e8c846b69721
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457523"
---
# <a name="intro-to-aspnet-mvc-3-c"></a>Úvod do ASP.NET MVC 3 (C#)

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

## <a name="what-youll-build"></a>Co sestavíte

Implementujete jednoduchou aplikaci se seznamem videí, která podporuje vytváření, úpravy a výpis filmů z databáze. Níže jsou uvedeny dva snímky obrazovky aplikace, kterou vytvoříte. Obsahuje stránku, která zobrazuje seznam filmů z databáze:

![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image1.png)

Aplikace také umožňuje přidávat, upravovat a odstraňovat filmy a také zobrazit podrobnosti o jednotlivých uživatelích. Všechny scénáře zadávání dat zahrnují ověřování, aby se zajistilo, že jsou data uložená v databázi správná.

![](intro-to-aspnet-mvc-3/_static/image2.png)

## <a name="skills-youll-learn"></a>Dovednosti, se kterými se naučíte

Tady je seznam toho, co se naučíte:

- Jak vytvořit nový projekt ASP.NET MVC
- Vytvoření řadičů a zobrazení ASP.NET MVC
- Vytvoření nové databáze pomocí Entity Framework Code First paradigma
- Jak načíst a zobrazit data
- Jak upravit data a povolit ověřování dat.

## <a name="getting-started"></a>Začínáme

Spusťte aplikaci Visual Web Developer 2010 Express ("Visual Web Developer" pro krátkou verzi) a na **úvodní** stránce vyberte **Nový projekt** .

Visual Web Developer je integrované vývojové prostředí (IDE). Stejně jako při psaní dokumentů v aplikaci Microsoft Word použijete k vytvoření aplikací rozhraní IDE. V aplikaci Visual Web Developer je v horní části zobrazen panel nástrojů s různými možnostmi, které jsou vám k dispozici. K dispozici je také nabídka, která poskytuje další způsob, jak provádět úlohy v integrovaném vývojovém prostředí. (Například namísto výběru **nového projektu** na **úvodní** stránce můžete použít nabídku a vybrat **soubor** &gt; **Nový projekt**.)

[![](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="creating-your-first-application"></a>Vytvoření první aplikace

Můžete vytvářet aplikace pomocí Visual Basic nebo vizuálu C# jako programovací jazyk. Vyberte vizuál C# na levé straně a pak vyberte **webovou aplikaci ASP.NET MVC 3**. Pojmenujte projekt "MvcMovie" a klikněte na tlačítko **OK**. (Pokud dáváte přednost Visual Basic, přepněte se na [Visual Basic verzi](../vb/intro-to-aspnet-mvc-3.md) tohoto kurzu.)

![](intro-to-aspnet-mvc-3/_static/image5.png)

V dialogovém okně **Nový projekt ASP.NET MVC 3** vyberte možnost **Internetová aplikace**. Zkontrolujte **použití značek HTML5** a ponechte **Razor** jako výchozí modul zobrazení.

![](intro-to-aspnet-mvc-3/_static/image6.png)

Klikněte na tlačítko **OK**. Visual Web Developer použil výchozí šablonu pro projekt ASP.NET MVC, který jste právě vytvořili, takže teď máte funkční aplikaci, aniž by bylo potřeba cokoli dělat! Toto je jednoduché "Hello World!" a je to vhodné místo pro spuštění vaší aplikace.

[![](intro-to-aspnet-mvc-3/_static/image8.png)](intro-to-aspnet-mvc-3/_static/image7.png)

V nabídce **ladění** vyberte **Spustit ladění**.

![](intro-to-aspnet-mvc-3/_static/image9.png)

Všimněte si, že klávesová zkratka pro spuštění ladění je F5.

F5 způsobí, že Visual Web Developer spustí vývojový webový server a spustí webovou aplikaci. Visual Web Developer potom spustí prohlížeč a otevře domovskou stránku aplikace. Všimněte si, že adresní řádek prohlížeče uvádí `localhost` a ne něco jako `example.com`. To je proto, že `localhost` vždy odkazuje na vlastní místní počítač, v tomto případě je spuštěná aplikace, kterou jste právě sestavili. Když Visual Web Developer spustí webový projekt, pro webový server se použije náhodný port. Na následujícím obrázku je číslo náhodného portu 43246. Při spuštění aplikace se pravděpodobně zobrazí jiné číslo portu.

![](intro-to-aspnet-mvc-3/_static/image10.png)

Přímo z tohoto pole vám tato výchozí šablona nabídne dvě stránky, které můžete navštívit, a základní přihlašovací stránku. Dalším krokem je změna fungování této aplikace a další informace o ASP.NET MVC v procesu. Zavřete prohlížeč a Pojďme změnit nějaký kód.

> [!div class="step-by-step"]
> [Next](adding-a-controller.md)

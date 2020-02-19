---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
title: Úvod do ASP.NET MVC 3 (VB) | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, který je...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: a1b3d789-93b4-487f-b90d-80c9c9b4f8fa
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/intro-to-aspnet-mvc-3
msc.type: authoredcontent
ms.openlocfilehash: 24f7de303ef7f5a457bd509ecc6bd0e3be7e3d9d
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456310"
---
# <a name="intro-to-aspnet-mvc-3-vb"></a>Úvod do ASP.NET MVC 3 (VB)

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, což je bezplatná verze Microsoft Visual Studio. Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže. Všechny z nich můžete nainstalovat kliknutím na následující odkaz: instalace [webové platformy](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Případně můžete požadavky jednotlivě nainstalovat pomocí následujících odkazů:
> 
> - [Požadavky sady Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Aktualizace nástrojů MVC 3 pro ASP.NET](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(podpora modulu runtime + nástroje)
> 
> Pokud používáte sadu Visual Studio 2010 místo sady Visual Web Developer 2010, nainstalujte požadavky kliknutím na následující odkaz: sady [Visual studio 2010 požadavky](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Projekt Visual Web Developer s VB.NET zdrojovým kódem je k dispozici pro toto téma. [Stáhněte si verzi VB.NET](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Pokud dáváte přednost C#, přepněte se na [ C# verzi](../cs/intro-to-aspnet-mvc-3.md) tohoto kurzu.

V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, což je bezplatná verze Microsoft Visual Studio. Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže. Všechny z nich můžete nainstalovat kliknutím na následující odkaz: instalace [webové platformy](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Případně můžete požadavky jednotlivě nainstalovat pomocí následujících odkazů:

- [Požadavky sady Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [Aktualizace nástrojů MVC 3 pro ASP.NET](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(podpora modulu runtime + nástroje)

Pokud používáte sadu Visual Studio 2010 místo sady Visual Web Developer 2010, nainstalujte požadavky kliknutím na následující odkaz: sady [Visual studio 2010 požadavky](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).

Projekt Visual Web Developer se zdrojovým kódem VB je k dispozici pro toto téma. [Verzi VB si můžete stáhnout tady](https://code.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=14824). Pokud dáváte přednost CSharp, přepněte se na [verzi](../cs/intro-to-aspnet-mvc-3.md) tohoto kurzu CSharp.

## <a name="what-youll-build"></a>Co sestavíte

Implementujete jednoduchou aplikaci se seznamem videí, která podporuje vytváření, úpravy a výpis filmů z databáze. Níže jsou uvedeny dva snímky obrazovky aplikace, kterou vytvoříte. Obsahuje stránku, která zobrazuje seznam filmů z databáze:

[![MoviesWithVariousSm](intro-to-aspnet-mvc-3/_static/image2.png)](intro-to-aspnet-mvc-3/_static/image1.png)

Aplikace také umožňuje přidávat, upravovat a odstraňovat filmy a také zobrazit podrobnosti o jednotlivých uživatelích. Všechny scénáře zadávání dat zahrnují ověřování, aby se zajistilo, že jsou data uložená v databázi správná.

[![CreateFormSo](intro-to-aspnet-mvc-3/_static/image4.png)](intro-to-aspnet-mvc-3/_static/image3.png)

## <a name="skills-youll-learn"></a>Dovednosti, se kterými se naučíte

Tady je seznam toho, co se naučíte:

- Vytvoření nového projektu ASP.NET MVC
- Vytvoření nové databáze pomocí Entity Frameworkho kódu – první
- Vytvoření řadičů a zobrazení ASP.NET MVC
- Jak načíst a zobrazit data
- Jak upravit data a povolit ověřování dat

## <a name="getting-started"></a>Začínáme

Začněte spuštěním aplikace Visual Web Developer 2010 Express ("souboru vwd" pro krátké) a na **úvodní** stránce vyberte **Nový projekt** .

Visual Web Developer je integrované vývojové prostředí (IDE). Stejně jako při psaní dokumentů v aplikaci Microsoft Word použijete k vytvoření aplikací rozhraní IDE. V aplikaci Visual Web Developer je v horní části zobrazen panel nástrojů s různými možnostmi, které jsou vám k dispozici. K dispozici je také nabídka, která poskytuje další způsob, jak provádět úlohy v integrovaném vývojovém prostředí. (Například namísto výběru **nového projektu** na **úvodní** stránce můžete použít nabídku a vybrat **soubor** &gt; **Nový projekt**.)

[![](intro-to-aspnet-mvc-3/_static/image6.png)](intro-to-aspnet-mvc-3/_static/image5.png)

## <a name="creating-your-first-application"></a>Vytvoření první aplikace

Můžete vytvářet aplikace podle vlastního výběru Visual Basic nebo vizuálu C# jako programovací jazyk. Pro tento kurz vyberte Visual Basic vlevo a pak vyberte **Webová aplikace ASP.NET MVC 3**. Pojmenujte projekt "MvcMovie" a klikněte na tlačítko **OK**.

![1NewMVCproj_sm](intro-to-aspnet-mvc-3/_static/image7.png)

V dialogovém okně **Nový projekt ASP.NET MVC 3** vyberte možnost **Internetová aplikace**. Ponechá **Razor** jako výchozí zobrazovací modul.

![1InternetAppRazor_SM](intro-to-aspnet-mvc-3/_static/image8.png)

Klikněte na tlačítko **OK**. Visual Web Developer použil výchozí šablonu pro projekt ASP.NET MVC, který jste právě vytvořili, takže teď máte funkční aplikaci, aniž by bylo potřeba cokoli dělat! Toto je jednoduché "Hello World!" a je to vhodné místo pro spuštění vaší aplikace.

[![](intro-to-aspnet-mvc-3/_static/image10.png)](intro-to-aspnet-mvc-3/_static/image9.png)

V nabídce **ladění** vyberte **Spustit ladění**.

![](intro-to-aspnet-mvc-3/_static/image11.png)

Všimněte si, že klávesová zkratka pro spuštění ladění je F5.

F5 způsobí, že Visual Web Developer spustí vývojový webový server a spustí webovou aplikaci. SOUBORU vwd pak spustí prohlížeč a otevře domovskou stránku aplikace. Všimněte si, že adresní řádek prohlížeče uvádí `localhost` a ne něco jako `example.com`. To je proto, že `localhost` vždy odkazuje na vlastní místní počítač, v tomto případě je spuštěná aplikace, kterou jste právě sestavili. Když souboru vwd spustí webový projekt, pro projekt se použije náhodný port. Na následujícím obrázku je číslo náhodného portu 43246. Projekt bude pravděpodobně používat jiné číslo portu.

![](intro-to-aspnet-mvc-3/_static/image12.png)

Tato výchozí šablona vám umožní přejít na dvě stránky a základní přihlašovací stránku. Pojďme změnit, jak tato aplikace funguje, a v procesu ASP.NET MVC se dozvíte trochu. Zavřete prohlížeč a Pojďme změnit nějaký kód.

> [!div class="step-by-step"]
> [Next](adding-a-controller.md)

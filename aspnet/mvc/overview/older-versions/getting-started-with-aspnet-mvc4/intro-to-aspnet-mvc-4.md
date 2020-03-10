---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
title: Úvod do ASP.NET MVC 4 | Microsoft Docs
author: Rick-Anderson
description: Aktualizovaná verze, pokud je tento kurz k dispozici zde, pomocí Visual Studio 2013. Nový kurz používá ASP.NET MVC 5, který poskytuje mnoho vylepšení oproti t...
ms.author: riande
ms.date: 08/15/2012
ms.assetid: ed66530a-04d5-49eb-b76a-85be1f57c437
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 51709a9c6ddb39b8fcd1cd94cd08d530a595825a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78599643"
---
# <a name="intro-to-aspnet-mvc-4"></a>Úvod do ASP.NET MVC 4

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> Aktualizovaná verze, pokud je tento kurz k dispozici [zde](../../getting-started/introduction/getting-started.md) , pomocí [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013). Nový kurz používá ASP.NET MVC 5, který poskytuje mnoho vylepšení v rámci tohoto kurzu.
>
> V tomto kurzu se naučíte základy vytvoření webové aplikace ASP.NET MVC 4 pomocí nástroje Microsoft [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express) nebo Visual Web Developer 2010 Express Service Pack 1. Doporučuje se Visual Studio 2012, takže nebudete muset instalovat žádné součásti, abyste mohli tento kurz dokončit. Pokud používáte Visual Studio 2010, je nutné nainstalovat komponenty níže. Všechny z nich můžete nainstalovat kliknutím na následující odkazy:
>
> - [Požadavky sady Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Instalační program služby pracovního procesu pro ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)
> - [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)
> - [SSDT](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)
>
> Pokud používáte sadu Visual Studio 2010 namísto Visual Web Developer 2010, nainstalujte [instalační program služby pro ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392) a [požadavky sady Visual Studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack) .
>
> Projekt Visual Web Developer se C# zdrojovým kódem je k dispozici pro toto téma. [Stáhněte si C# verzi](https://code.msdn.microsoft.com/Intro-to-ASPNET-MVC-4-61d0219d/file/114480/1/MvcMovie.zip).
>
> V kurzu spustíte aplikaci v aplikaci Visual Studio. Aplikaci můžete zpřístupnit i přes Internet tím, že ji nasadíte pro poskytovatele hostingu. Microsoft nabízí bezplatné webové hostování až pro 10 webů na [bezplatném zkušebním účtu Windows Azure](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604). Informace o tom, jak nasadit webový projekt aplikace Visual Studio na web Windows Azure, najdete v tématu [Vytvoření a nasazení webu ASP.NET a SQL Database se sadou Visual Studio](https://docs.microsoft.com/dotnet/azure/). Tento kurz také ukazuje, jak použít Migrace Entity Framework Code First k nasazení databáze SQL Server do Windows Azure SQL Database (dříve SQL Azure).
>
> Tento kurz napsal Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ).

## <a name="what-youll-build"></a>Co sestavíte

> [!NOTE]
> Aktualizovaná verze, pokud je tento kurz k dispozici [zde](../../getting-started/introduction/getting-started.md) , pomocí [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013). Nový kurz používá ASP.NET MVC 5, který poskytuje mnoho vylepšení v rámci tohoto kurzu.

Implementujete jednoduchou aplikaci se seznamem videí, která podporuje vytváření, úpravy, vyhledávání a výpis filmů z databáze. Níže jsou uvedeny dva snímky obrazovky aplikace, kterou vytvoříte. Obsahuje stránku, která zobrazuje seznam filmů z databáze:

![](intro-to-aspnet-mvc-4/_static/image1.png)

Aplikace také umožňuje přidávat, upravovat a odstraňovat filmy a také zobrazit podrobnosti o jednotlivých uživatelích. Všechny scénáře zadávání dat zahrnují ověřování, aby se zajistilo, že jsou data uložená v databázi správná.

![](intro-to-aspnet-mvc-4/_static/image2.png)

## <a name="getting-started"></a>začínáme

Začněte spuštěním Visual Studio Express 2012 nebo Visual Web Developer 2010 Express. Většina snímků obrazovky v této sérii používá Visual Studio Express 2012, ale tento kurz můžete dokončit v sadě Visual Studio 2010/SP1, Visual Studio 2012, Visual Studio Express 2012 nebo Visual Web Developer 2010 Express. Na **úvodní** stránce vyberte **Nový projekt** .

Visual Studio je integrované vývojové prostředí (IDE) nebo integrované vývojové prostředí. Stejně jako při psaní dokumentů v aplikaci Microsoft Word použijete k vytvoření aplikací rozhraní IDE. V sadě Visual Studio je na horním panelu panel nástrojů, na kterém jsou k dispozici různé možnosti. K dispozici je také nabídka, která poskytuje další způsob, jak provádět úlohy v integrovaném vývojovém prostředí. (Například namísto výběru **nového projektu** na **úvodní** stránce můžete použít nabídku a vybrat **soubor** &gt; **Nový projekt**.)

![](intro-to-aspnet-mvc-4/_static/image3.png)

## <a name="creating-your-first-application"></a>Vytvoření první aplikace

Můžete vytvářet aplikace pomocí Visual Basic nebo vizuálu C# jako programovací jazyk. Vyberte vizuál C# na levé straně a pak vyberte **webovou aplikaci ASP.NET MVC 4**. Pojmenujte projekt &quot;MvcMovie&quot; a pak klikněte na tlačítko **OK**.

![](intro-to-aspnet-mvc-4/_static/image4.png)

V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte **internetovou aplikaci**. Ponechá **Razor** jako výchozí zobrazovací modul.

![](intro-to-aspnet-mvc-4/_static/image5.png)

Klikněte na tlačítko **OK**. Aplikace Visual Studio použila pro projekt ASP.NET MVC, který jste právě vytvořili, výchozí šablonu, takže teď máte funkční aplikaci, aniž byste museli cokoli dělat! Toto je jednoduchá &quot;Hello World.&quot; projekt a je dobrým místem pro spuštění aplikace.

![](intro-to-aspnet-mvc-4/_static/image6.png)

V nabídce **ladění** vyberte **Spustit ladění**.

![](intro-to-aspnet-mvc-4/_static/image7.png)

Všimněte si, že klávesová zkratka pro spuštění ladění je F5.

F5 způsobí, že Visual Studio spustí IIS Express a spustí vaši webovou aplikaci. Visual Studio potom spustí prohlížeč a otevře domovskou stránku aplikace. Všimněte si, že adresní řádek prohlížeče uvádí `localhost` a ne něco jako `example.com`. To je proto, že `localhost` vždy odkazuje na vlastní místní počítač, v tomto případě je spuštěná aplikace, kterou jste právě sestavili. Když Visual Studio spustí webový projekt, pro webový server se použije náhodný port. Na následujícím obrázku je číslo portu 41788. Při spuštění aplikace se pravděpodobně zobrazí jiné číslo portu.

![](intro-to-aspnet-mvc-4/_static/image8.png)

Přímo z tohoto pole vám tato výchozí šablona umožní domů, kontaktovat a o stránkách. Poskytuje taky podporu pro registraci a přihlášení a odkazy na Facebook a Twitter. Dalším krokem je změna toho, jak tato aplikace funguje, a dozvíte se trochu o ASP.NET MVC. Zavřete prohlížeč a Pojďme změnit nějaký kód.

> [!div class="step-by-step"]
> [Next](adding-a-controller.md)

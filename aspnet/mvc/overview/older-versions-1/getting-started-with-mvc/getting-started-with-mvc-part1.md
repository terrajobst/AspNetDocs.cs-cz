---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
title: Úvod do ASP.NET MVC | Microsoft Docs
author: shanselman
description: Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvořte jednoduchou webovou aplikaci, která čte a zapisuje z databáze.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: bf4a1c19-0a94-4208-b268-a96ddcf26946
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part1
msc.type: authoredcontent
ms.openlocfilehash: f8f0014776ba1313119e8c39c63a216b0fc864e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581583"
---
# <a name="intro-to-aspnet-mvc"></a>Úvod do ASP.NET MVC

[Scott Hanselman](https://github.com/shanselman)

> > [!NOTE]
> > Aktualizovaná verze, pokud je tento kurz k dispozici [zde](../../getting-started/introduction/getting-started.md) , pomocí [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013). Nový kurz používá ASP.NET MVC 5, který poskytuje mnoho vylepšení v rámci tohoto kurzu.
>
>
> Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvoříte jednoduchou webovou aplikaci, která čte a zapisuje z databáze. Navštivte [centrum učení služby ASP.NET MVC](../../../index.md) , kde najdete další kurzy a ukázky pro ASP.NET MVC.

Pojďme udělat naši první webovou aplikaci v ASP.NET MVC s použitím [aplikace Visual Web Developer 2010 Express](https://www.microsoft.com/express/Web/). Vytvoříme trochu aplikaci seznamu filmů, která nám umožní vytvořit a vypsat filmy.

## <a name="what-youll-build"></a>Co sestavíte

Tady jsou dva snímky obrazovky aplikace, kterou vytvoříte. Budete mít jednoduchou tabulku filmů s různými sloupci.

[Seznam filmů ![– Windows Internet Explorer (12)](getting-started-with-mvc-part1/_static/image2.png)](getting-started-with-mvc-part1/_static/image1.png)

A budete mít formulář pro vytvoření, abychom mohli do seznamu přidat filmy.

[![vytvoření videa – Windows Internet Explorer (2)](getting-started-with-mvc-part1/_static/image4.png)](getting-started-with-mvc-part1/_static/image3.png)

## <a name="skills-youll-learn"></a>Dovednosti, se kterými se naučíte

V tomto kurzu se naučíte základy vytvoření webové aplikace ASP.NET MVC pomocí sady Visual Studio. Naučíte se:

- Vytvoření nového projektu ASP.NET MVC
- Vytvoření nové databáze pomocí SQL Server
- Vytvoření řadičů a zobrazení ASP.NET MVC
- Jak načíst a zobrazit data
- Jak upravit data a povolit ověřování dat
- Postup aktualizace schématu databáze

## <a name="get-started"></a>Začínáme

Začněte spuštěním aplikace Visual Web Developer 2010 Express (nahlaste ji "souboru vwd" od této chvíle) a na úvodní obrazovce vyberte nový projekt.

Visual Web Developer je integrované vývojové prostředí (IDE). Stejně jako při psaní dokumentů v aplikaci Microsoft Word použijete k vytvoření aplikací rozhraní IDE. V horní části je panel nástrojů s různými možnostmi, které jsou vám k dispozici, a také v nabídce, kterou byste mohli použít k výběru souboru | Nový projekt.

[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image6.png)](getting-started-with-mvc-part1/_static/image5.png)

## <a name="creating-your-first-application"></a>Vytvoření první aplikace

Můžete vytvářet aplikace pomocí Visual Basic nebo vizuálu C#. Prozatím na levé straně C# vyberte vizuál a pak vyberte webová aplikace ASP.NET MVC 2. Pojmenujte svůj projekt "filmy" a klikněte na OK.

[![nový projekt](getting-started-with-mvc-part1/_static/image8.png)](getting-started-with-mvc-part1/_static/image7.png)

Na pravé straně je Průzkumník řešení, kde se zobrazují všechny soubory a složky v aplikaci. Velké okno uprostřed je místo, kde upravujete kód a strávíte nejvíce času. Aplikace Visual Studio použila pro projekt ASP.NET MVC, který jste právě vytvořili, výchozí šablonu, takže teď máte funkční aplikaci, aniž byste museli cokoli dělat! Toto je jednoduché "Hello World! projekt a je dobrým místem, kde se má aplikace spouštět.

[![Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part1/_static/image10.png)](getting-started-with-mvc-part1/_static/image9.png)

Na panelu nástrojů vyberte tlačítko Přehrát.

![Spustit ladění](getting-started-with-mvc-part1/_static/image11.png)

Jedná se o zelenou šipku ukazující vpravo, která zkompiluje váš program a spustí aplikaci ve webovém prohlížeči.

*Poznámka: místo toho můžete stisknout klávesu F5 na klávesnici nebo vybrat ladění&gt;spustit ladění z nabídky ladění.*

Tím dojde k tomu, že Visual Web Developer spustí vývoj webového serveru a spustí naši webovou aplikaci (k povolení tohoto postupu není nutná žádná konfigurace nebo ruční kroky). Pak spustí prohlížeč a nakonfiguruje ho pro procházení domovské stránky aplikace. Všimněte si, že adresní řádek prohlížeče říká "localhost", a ne něco jako example.com. To je způsobeno tím, že localhost vždy odkazuje na vlastní místní počítač – v tomto případě je spuštěna aplikace, kterou jsme právě vytvořili.

[![domovskou stránku](getting-started-with-mvc-part1/_static/image13.png)](getting-started-with-mvc-part1/_static/image12.png)

Tato výchozí šablona vám umožní přejít na dvě stránky a základní přihlašovací stránku. Pojďme změnit, jak tato aplikace funguje, a v procesu ASP.NET MVC se dozvíte trochu. Zavřete prohlížeč a můžete změnit nějaký kód.

> [!div class="step-by-step"]
> [Next](getting-started-with-mvc-part2.md)

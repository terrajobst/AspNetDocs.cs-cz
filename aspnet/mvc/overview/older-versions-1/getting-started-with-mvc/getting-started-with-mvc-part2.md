---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
title: Přidání kontroleru | Microsoft Docs
author: shanselman
description: Aktualizovaná verze, pokud je tento kurz k dispozici zde, pomocí Visual Studio 2013. Nový kurz používá ASP.NET MVC 5, který poskytuje mnoho vylepšení oproti t...
ms.author: riande
ms.date: 08/14/2010
ms.assetid: ff03dcc0-da97-458d-838f-0823e7482642
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
msc.type: authoredcontent
ms.openlocfilehash: e2a298584473f57c2b14edf507f0f6886d906ea3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543979"
---
# <a name="adding-a-controller"></a>Přidání kontroleru

[Scott Hanselman](https://github.com/shanselman)

> > [!NOTE]
> > Aktualizovaná verze, pokud je tento kurz k dispozici [zde](../../getting-started/introduction/getting-started.md) , pomocí [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013). Nový kurz používá ASP.NET MVC 5, který poskytuje mnoho vylepšení v rámci tohoto kurzu.
>
>
> Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvoříte jednoduchou webovou aplikaci, která čte a zapisuje z databáze. Navštivte [centrum učení služby ASP.NET MVC](../../../index.md) , kde najdete další kurzy a ukázky pro ASP.NET MVC.

MVC představuje model, zobrazení, kontroler. MVC je vzor pro vývoj aplikací tak, aby každá část měla zodpovědnost, která se liší od jiné.

- Model: data vaší aplikace
- Zobrazení: soubory šablon, které aplikace použije k dynamickému generování odpovědí HTML.
- Řadiče: třídy, které zpracovávají příchozí žádosti adresy URL do aplikace, načítají data modelu a pak určují šablony zobrazení, které vykreslí odpověď zpátky klientovi.

V tomto kurzu pokryjeme všechny tyto koncepty a ukážeme vám, jak je používat k sestavení aplikace.

Pojďme vytvořit nový kontroler tak, že kliknete pravým tlačítkem na složku řadiče v Průzkumníku řešení a vyberete Přidat kontroler.

[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)

Pojmenujte nový kontroler "HelloWorldController" a klikněte na Přidat.

[Dialog ![přidat kontrolér](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)

Všimněte si Průzkumník řešení na pravé straně, že pro vás byl vytvořen nový soubor s názvem HelloWorldController.cs a tento soubor je nyní otevřen v **integrovaném vývojovém prostředí (IDE**).

[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)

Vytvořte dvě nové metody, které vypadají jako v rámci vaší nové veřejné třídy HelloWorldController. Jako příklad vrátíme řetězec HTML přímo z našeho kontroleru.

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample1.cs)]

Váš kontroler má název HelloWorldController a vaše nová metoda se nazývá index. Spusťte aplikaci znovu, stejně jako předtím (klikněte na tlačítko Přehrát nebo stiskněte klávesu F5 k tomuto účelu). Jakmile se Váš prohlížeč spustí, změňte cestu na adresním řádku a `http://localhost:xx/HelloWorld`, kde XX je libovolný počet zvolený počítač. Prohlížeč by teď měl vypadat jako snímek obrazovky níže. V naší metodě jsme vrátili řetězec předaný metodě s názvem "content". Zjistili jsme, že systém pouze vrátí kód HTML a byl to!

ASP.NET MVC vyvolá různé třídy kontroleru (a v rámci nich různé metody akcí) v závislosti na příchozí adrese URL. Výchozí logika mapování, kterou používá ASP.NET MVC, používá formát podobný tomuto: k určení toho, jaký kód se spustí:

/[Kontrolér]/[Action]/[parametry]

První část adresy URL určuje třídu kontroleru, která se má spustit. Proto/HelloWorld mapuje na třídu HelloWorldController. Druhá část adresy URL určuje metodu Action pro třídu, která má být provedena. /HelloWorld/Index by proto způsobila, že se spustí metoda index () třídy HelloWorldController. Všimněte si, že jsme rádi navštívili/HelloWorld výše a index metody byl odvozen. Důvodem je, že metoda s názvem index je výchozí metoda, která bude volána na řadiči, pokud není explicitně určena.

[![Toto je moje výchozí akce](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)

Nyní se teď podívejme, `http://localhost:xx/HelloWorld/Welcome.` nyní naše uvítací metoda provedla a vrátila svůj řetězec HTML.

Znovu,/[kontrolér]/[Action]/[Parameters], takže kontroler je HelloWorld a Welcome je metoda v tomto případě. Zatím jsme neudělali parametry.

[![je to metoda akce Welcome.](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)

Pojďme to trochu upravit, abychom mohli předat nějaké informace z adresy URL naší řadiči, například takto:/HelloWorld/Welcome? název = Scott&amp;numtimes = 4. Změňte metodu Vítejte tak, aby zahrnovala dva parametry a aktualizovala ji, jak je znázorněno níže. Všimněte si, že jsme použili C# funkci volitelného parametru k označení toho, že parametr numTimes by měl být nastaven na hodnotu 1, pokud není předaný.

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample2.cs)]

Spusťte aplikaci a podívejte se na `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` změně hodnoty název a numtimes, jak budete chtít. Systém automaticky namapuje pojmenované parametry z řetězce dotazu na adresní řádek do parametrů ve vaší metodě.

V obou těchto příkladech kontroler provedl veškerou práci a vrátil přímo HTML. Obvykle nepotřebujeme, aby naše řadiče vracely HTML přímo – protože to pro kód končí hodně nenáročných. Místo toho obvykle použijete samostatný soubor šablony zobrazení, který vám pomůžeme vygenerovat odpověď HTML. Pojďme se podívat, jak to můžeme udělat. Zavřete prohlížeč a vraťte se do integrovaného vývojového prostředí (IDE).

> [!div class="step-by-step"]
> [Předchozí](getting-started-with-mvc-part1.md)
> [Další](getting-started-with-mvc-part3.md)

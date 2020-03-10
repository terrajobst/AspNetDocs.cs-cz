---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
title: Přidání kontroleru (VB) | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, který je...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 741259e1-54ac-4f71-b4e8-2bd5560bb950
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 2e77f62a9796211b0e59a99c71bc532659b7cb92
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540514"
---
# <a name="adding-a-controller-vb"></a>Přidání kontroleru (VB)

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, což je bezplatná verze Microsoft Visual Studio. Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže. Všechny z nich můžete nainstalovat kliknutím na následující odkaz: instalace [webové platformy](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Případně můžete požadavky jednotlivě nainstalovat pomocí následujících odkazů:
> 
> - [Požadavky sady Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [Aktualizace nástrojů MVC 3 pro ASP.NET](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(podpora modulu runtime + nástroje)
> 
> Pokud používáte sadu Visual Studio 2010 místo sady Visual Web Developer 2010, nainstalujte požadavky kliknutím na následující odkaz: sady [Visual studio 2010 požadavky](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).
> 
> Projekt Visual Web Developer s VB.NET zdrojovým kódem je k dispozici pro toto téma. [Stáhněte si verzi VB.NET](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098). Pokud dáváte přednost C#, přepněte se na [ C# verzi](../cs/adding-a-controller.md) tohoto kurzu.

MVC představuje *kontroler-View-Controller*. MVC je vzor pro vývoj aplikací, takže každá část má samostatnou zodpovědnost:

- Model: data pro vaši aplikaci.
- Zobrazení: soubory šablon, které aplikace použije k dynamickému generování odpovědí HTML.
- Řadiče: třídy, které zpracovávají příchozí žádosti adresy URL do aplikace, načítají data modelu a pak určují šablony zobrazení, které vykreslí odpověď klientovi.

V tomto kurzu pokryjeme všechny tyto koncepty a ukážeme vám, jak je používat k sestavení aplikace.

Vytvořte nový kontroler tak, že kliknete pravým tlačítkem na složku *Controllers* v **Průzkumník řešení** a pak vyberete **Přidat kontroler**.

[![AddController](adding-a-controller/_static/image2.png "AddController")](adding-a-controller/_static/image1.png)

Pojmenujte nový kontroler &quot;HelloWorldController&quot; a klikněte na **Přidat**.

[![2AddEmptyController](adding-a-controller/_static/image4.png "2AddEmptyController")](adding-a-controller/_static/image3.png)

Všimněte si, že v **Průzkumník řešení** napravo, že pro vás byl vytvořen nový soubor s názvem *HelloWorldController.cs* a že je soubor otevřen v integrovaném vývojovém prostředí.

Uvnitř nového bloku `public class HelloWorldController` vytvořte dvě nové metody, které vypadají jako následující kód. Jako příklad vrátíme řetězec HTML přímo z kontroleru.

[!code-vb[Main](adding-a-controller/samples/sample1.vb)]

Váš kontroler má název `HelloWorldController` a vaše nová metoda se jmenuje `Index`. Spusťte aplikaci (stiskněte klávesu F5 nebo CTRL + F5). Po spuštění prohlížeče přidejte &quot;HelloWorld&quot; k cestě na adresním řádku. (V mém počítači je to `http://localhost:43246/HelloWorld`) Váš prohlížeč bude vypadat jako na následujícím snímku obrazovky. V metodě výše kód vrátil řetězec přímo. Zjistili jsme, že systém vrací nějaký kód HTML a byl to!

![](adding-a-controller/_static/image5.png)

ASP.NET MVC vyvolá různé třídy kontroleru (a v rámci nich různé metody akcí) v závislosti na příchozí adrese URL. Výchozí mapování logiky používané službou ASP.NET MVC používá formát podobný tomuto: k určení toho, jaký kód je vyvolán:

`/[Controller]/[ActionName]/[Parameters]`

První část adresy URL určuje třídu kontroleru, která se má spustit. Proto */HelloWorld* mapuje na třídu `HelloWorldController`. Druhá část adresy URL určuje metodu Action pro třídu, která má být provedena. */HelloWorld/index* by proto způsobila spuštění metody `Index` `HelloWorldController` třídy. Všimněte si, že jsme už navštívili */HelloWorld* výše a ve výchozím nastavení se použila metoda `Index`. Důvodem je, že metoda s názvem `Index` je výchozí metoda, která bude volána na řadiči, pokud není explicitně určena.

Přejděte na `http://localhost:xxxx/HelloWorld/Welcome`. Metoda `Welcome` se spustí a vrátí řetězec, &quot;se jedná o metodu akce Welcome...&quot;. Výchozí mapování MVC je `/[Controller]/[ActionName]/[Parameters]`. Pro tuto adresu URL se kontroler `HelloWorld` a `Welcome` je metoda. Zatím jsme nepoužili `[Parameters]` část této adresy URL.

![](adding-a-controller/_static/image6.png)

Pojďme tento příklad mírně upravit, abychom mohli předat nějaké informace o parametrech z adresy URL do kontroleru (například */HelloWorld/Welcome? Name = Scott&amp;numtimes = 4*). Změňte metodu `Welcome` tak, aby zahrnovala dva parametry, jak je uvedeno níže. Všimněte si, že jsme použili funkci volitelného parametru VB k označení toho, že parametr `numTimes` by měl být nastaven na hodnotu 1, pokud není pro tento parametr předána žádná hodnota.

[!code-vb[Main](adding-a-controller/samples/sample2.vb)]

Spusťte aplikaci a přejděte na `http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4` **.** Můžete zkusit jiné hodnoty pro `name` a `numtimes`. Systém automaticky mapuje pojmenované parametry z řetězce dotazu na adresní řádek do parametrů ve vaší metodě.

![](adding-a-controller/_static/image7.png)

V obou těchto příkladech kontroler provedl součást VC v MVC – to je zobrazení a kontroler práce. Kontroler přímo vrací HTML. Obvykle nepotřebujeme, aby řadiče vracely kód HTML přímo, protože to bude pro kód velmi nenáročný. Místo toho obvykle použijete samostatný soubor šablony zobrazení, který vám pomůžeme vygenerovat odpověď HTML. Pojďme se podívat, jak to můžeme udělat.

> [!div class="step-by-step"]
> [Předchozí](intro-to-aspnet-mvc-3.md)
> [Další](adding-a-view.md)

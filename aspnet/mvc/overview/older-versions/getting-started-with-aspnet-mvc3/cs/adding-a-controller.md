---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
title: Přidání kontroleru (C#) | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy vytváření webových aplikací ASP.NET MVC pomocí nástroje Microsoft Visual Web Developer 2010 Express Service Pack 1, který jsem...
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 0b8c56b5-fdf3-42dd-a866-98fbe0ab78a0
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 959116ff773f4ef466cda6b172e8321590b50e5b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457822"
---
# <a name="adding-a-controller-c"></a>Přidání kontroleru (C#)

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

MVC představuje *kontroler-View-Controller*. MVC je vzor pro vývoj aplikací, které jsou dobře architektované a snadno se udržují. Aplikace založené na MVC obsahují:

- Řadiče: třídy, které zpracovávají příchozí požadavky na aplikaci, načítají data modelu a pak určují šablony zobrazení, které vracejí odpověď klientovi.
- Modely: třídy, které reprezentují data aplikace a používají logiku ověřování k vyhodnocování obchodních pravidel pro tato data.
- Zobrazení: soubory šablon, které vaše aplikace používá k dynamickému generování odpovědí HTML.

Pokryjeme všechny tyto koncepty v této sérii kurzů a ukážeme vám, jak je používat k sestavení aplikace.

Pojďme začít vytvořením třídy Controller. V **Průzkumník řešení**klikněte pravým tlačítkem na složku *Controllers* a pak vyberte **Přidat kontroler**.

[![](adding-a-controller/_static/image2.png)](adding-a-controller/_static/image1.png)

Pojmenujte nový kontroler "HelloWorldController". Ponechte výchozí šablonu jako **prázdný kontroler** a klikněte na **Přidat**.

[![AddHelloWorldController](adding-a-controller/_static/image4.png)](adding-a-controller/_static/image3.png)

Všimněte si **Průzkumník řešení** , že byl vytvořen nový soubor s názvem *HelloWorldController.cs*. Soubor je otevřen v integrovaném vývojovém prostředí.

![](adding-a-controller/_static/image5.png)

Uvnitř bloku `public class HelloWorldController` vytvořte dvě metody, které vypadají jako následující kód. Kontroler jako příklad vrátí řetězec HTML.

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

Váš kontroler má název `HelloWorldController` a první výše uvedená metoda je pojmenována `Index`. Pojďme to vyvolat z prohlížeče. Spusťte aplikaci (stiskněte klávesu F5 nebo CTRL + F5). V prohlížeči přidejte "HelloWorld" do cesty na adresním řádku. (Například na obrázku níže je `http://localhost:43246/HelloWorld.`) Stránka v prohlížeči bude vypadat jako na následujícím snímku obrazovky. V metodě výše kód vrátil řetězec přímo. Dozvěděli jste systém, aby vracel jenom určitý kód HTML a byl.

![](adding-a-controller/_static/image6.png)

ASP.NET MVC vyvolá různé třídy kontroleru (a v rámci nich různé metody akcí) v závislosti na příchozí adrese URL. Výchozí logika mapování, kterou používá ASP.NET MVC, používá formát podobný tomuto: k určení kódu, který se má vyvolat:

`/[Controller]/[ActionName]/[Parameters]`

První část adresy URL určuje třídu kontroleru, která se má spustit. Proto */HelloWorld* mapuje na třídu `HelloWorldController`. Druhá část adresy URL určuje metodu Action pro třídu, která má být provedena. */HelloWorld/index* by proto způsobila spuštění metody `Index` `HelloWorldController` třídy. Všimněte si, že jsme museli procházet na */HelloWorld* a ve výchozím nastavení se použila metoda `Index`. Důvodem je, že metoda s názvem `Index` je výchozí metoda, která bude volána na řadiči, pokud není explicitně určena.

Přejděte na `http://localhost:xxxx/HelloWorld/Welcome`. Metoda `Welcome` se spustí a vrátí řetězec "Toto je metoda akce Welcome...". Výchozí mapování MVC je `/[Controller]/[ActionName]/[Parameters]`. Pro tuto adresu URL se kontroler `HelloWorld` a `Welcome` je metoda Action. Zatím jste nepoužili `[Parameters]` část této adresy URL.

![](adding-a-controller/_static/image7.png)

Pojďme tento příklad mírně upravit, abyste mohli předat nějaké informace o parametrech z adresy URL do kontroleru (například */HelloWorld/Welcome? Name = Scott&amp;numtimes = 4*). Změňte metodu `Welcome` tak, aby zahrnovala dva parametry, jak je uvedeno níže. Všimněte si, že kód používá C# funkci volitelného parametru k označení toho, že parametr `numTimes` by měl být nastaven na hodnotu 1, pokud není pro tento parametr předána žádná hodnota.

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

Spusťte aplikaci a přejděte k ukázkové adrese URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`. Můžete zkusit jiné hodnoty pro `name` a `numtimes` v adrese URL. Systém automaticky mapuje pojmenované parametry z řetězce dotazu v adresním řádku na parametry ve vaší metodě.

![](adding-a-controller/_static/image8.png)

V obou těchto příkladech kontroler prováděl "VC" část MVC – to znamená, že zobrazení a kontroler funguje. Kontroler přímo vrací HTML. Obvykle nechcete, aby řadiče vracely kód HTML přímo, protože to může být velmi nenáročné na kód. Místo toho obvykle použijete samostatný soubor šablony zobrazení, který vám pomůžeme vygenerovat odpověď HTML. Pojďme se podívat na to, jak to můžeme udělat.

> [!div class="step-by-step"]
> [Předchozí](intro-to-aspnet-mvc-3.md)
> [Další](adding-a-view.md)

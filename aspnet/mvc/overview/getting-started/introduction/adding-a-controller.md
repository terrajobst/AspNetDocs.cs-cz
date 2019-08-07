---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: Přidání kontroleru | Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 6b38d757d37374b14979f8a079a46158ff64f9c3
ms.sourcegitcommit: f774732a3960fca079438a88a5472c37cf7be08a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/06/2019
ms.locfileid: "68810774"
---
# <a name="adding-a-controller"></a>Přidání kontroleru

od [Rick Anderson]((https://twitter.com/RickAndMSFT))

[!INCLUDE [Tutorial Note](sample/code-location.md)]

MVC představuje *kontroler-View-Controller*. MVC je vzor pro vývoj aplikací, které jsou dobře architektované, testovatelné a snadno udržovatelnější. Aplikace založené na MVC obsahují:

- Odels **M** : Třídy, které reprezentují data aplikace a používají logiku ověřování k vyhodnocování obchodních pravidel pro tato data.
- **V** iews: Soubory šablon, které vaše aplikace používá k dynamickému generování odpovědí HTML.
- Ontrollers **jazyka C** : Třídy, které zpracovávají příchozí požadavky prohlížeče, načítají data modelu a pak určují šablony zobrazení, které vracejí odpověď prohlížeči.

Pokryjeme všechny tyto koncepty v této sérii kurzů a ukážeme vám, jak je používat k sestavení aplikace.

Pojďme začít vytvořením třídy Controller. V **Průzkumník řešení**klikněte pravým tlačítkem na složku Controllers a pak klikněte na **Přidat**a pak na **kontroler**.

![](adding-a-controller/_static/image1.png)

V dialogovém okně **Přidat vygenerované uživatelské rozhraní** klikněte na kontroler **MVC 5 – prázdné**a pak klikněte na **Přidat**.

![](adding-a-controller/_static/image2.png)  

Pojmenujte nový kontroler "HelloWorldController" a klikněte na **Přidat**.

![Přidat kontroler](adding-a-controller/_static/image3.png)

Všimněte si, že **Průzkumník řešení** , že se vytvořil nový soubor s názvem *HelloWorldController.cs* a novou složkou *Views\HelloWorld*. Kontroler je otevřený v integrovaném vývojovém prostředí.

![](adding-a-controller/_static/image4.png)

Obsah souboru nahraďte následujícím kódem.

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

Metody kontroleru vrátí jako příklad řetězec HTML. Kontroler má název `HelloWorldController` a první metoda je pojmenována. `Index` Pojďme to vyvolat z prohlížeče. Spusťte aplikaci (stiskněte klávesu F5 nebo CTRL + F5). V prohlížeči přidejte &quot;HelloWorld&quot; k cestě na adresním řádku. (Například na ilustraci níže je to `http://localhost:1234/HelloWorld.`) stránka v prohlížeči bude vypadat jako na následujícím snímku obrazovky. V metodě výše kód vrátil řetězec přímo. Dozvěděli jste systém, aby vracel jenom určitý kód HTML a byl.

![](adding-a-controller/_static/image5.png)

ASP.NET MVC vyvolá různé třídy kontroleru (a v rámci nich různé metody akcí) v závislosti na příchozí adrese URL. Výchozí logika směrování adres URL, kterou používá ASP.NET MVC, používá formát podobný tomuto: k určení kódu, který se má vyvolat:

`/[Controller]/[ActionName]/[Parameters]`

Formát pro směrování nastavíte v souboru *Start/\_RouteConfig. cs aplikace* .

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

Když aplikaci spustíte a nezadáte žádné segmenty adresy URL, použije se výchozí řídicí řadič a metoda "index" uvedená v části Defaults výše uvedeného kódu.

První část adresy URL určuje třídu kontroleru, která se má spustit. Takže se */HelloWorld* mapuje na `HelloWorldController` třídu. Druhá část adresy URL určuje metodu Action pro třídu, která má být provedena. */HelloWorld/index* by proto způsobila `Index` , že se `HelloWorldController` metoda třídy spustí. Všimněte si, že jsme museli procházet na */HelloWorld* a `Index` metoda se ve výchozím nastavení použila. Důvodem je, že metoda s `Index` názvem je výchozí metoda, která bude volána na řadiči, pokud není explicitně určena. Třetí část segmentu adresy URL ( `Parameters`) je určena pro data trasy. Později se v tomto kurzu zobrazí data o trasách.

Přejděte do `http://localhost:xxxx/HelloWorld/Welcome`. Metoda se spustí a vrátí řetězec &quot;, který je to metoda akce Welcome... `Welcome` &quot;. Výchozí mapování MVC je `/[Controller]/[ActionName]/[Parameters]`. Pro tuto adresu URL kontroler je `HelloWorld` a `Welcome` je metodou Action. Ještě jste nepoužili `[Parameters]` část této adresy URL.

![](adding-a-controller/_static/image6.png)

Pojďme tento příklad mírně upravit, abyste mohli předat nějaké informace o parametrech z adresy URL do kontroleru (například */HelloWorld/Welcome? Name = Scott&amp;numtimes = 4*). `Welcome` Změňte metodu tak, aby zahrnovala dva parametry, jak je uvedeno níže. Všimněte si, že kód používá C# funkci volitelného parametru k označení toho, `numTimes` že parametr by měl být nastaven na hodnotu 1, pokud není pro tento parametr předána žádná hodnota.

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> Poznámka k zabezpečení: Výše uvedený kód používá [HttpUtility. HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) k ochraně aplikace před škodlivým vstupem (konkrétně JavaScript). Další informace najdete v části [jak: Chraňte proti zneužití skriptů ve webové aplikaci použitím kódování HTML v řetězcích](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx).

 Spusťte aplikaci a přejděte k ukázkové adrese URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`). Můžete zkusit použít jiné hodnoty pro `name` a `numtimes` v adrese URL. [Systém vazby modelu ASP.NET MVC](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automaticky mapuje pojmenované parametry z řetězce dotazu v adresním řádku na parametry v metodě.

![](adding-a-controller/_static/image7.png)

V ukázce výše se nepoužívá segment adresy URL `Parameters`() `name` , parametry a `numTimes` jsou předány jako [řetězce dotazu](http://en.wikipedia.org/wiki/Query_string). Okně? (otazník) na výše uvedené adrese URL je oddělovač a následují řetězce dotazů. &amp; Znak odděluje řetězce dotazu.

Metodu Welcome nahraďte následujícím kódem:

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

Spusťte aplikaci a zadejte následující adresu URL:`http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`

![](adding-a-controller/_static/image8.png)

Tentokrát, kdy třetí segment `ID.` adresy URL odpovídá parametru `Welcome` trasy, metoda Action obsahuje parametr (`ID` `RegisterRoutes` ), který se shoduje se specifikací adresy URL v metodě.

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

V aplikacích ASP.NET MVC je obvyklejší předávat parametry jako údaje o trasách (jako je to u ID výše), než je předáte jako řetězce dotazů. Můžete také přidat trasu, která bude `name` předat parametry i `numtimes` v jako směrovat data v adrese URL. Do souboru *App\_Start\RouteConfig.cs* přidejte trasu "Hello":

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

Spusťte aplikaci a přejděte na `/localhost:XXX/HelloWorld/Welcome/Scott/3`adresu.

![](adding-a-controller/_static/image9.png)

Pro mnoho aplikací MVC funguje výchozí trasa správně. Později v tomto kurzu se dozvíte, jak data předávat pomocí pořadače modelů, a nebudete muset měnit výchozí trasu.

V těchto příkladech kontroler provedl &quot;součást VC&quot; v MVC – to znamená, že zobrazení a kontroler funguje. Kontroler přímo vrací HTML. Obvykle nechcete, aby řadiče vracely kód HTML přímo, protože to může být velmi nenáročné na kód. Místo toho obvykle použijete samostatný soubor šablony zobrazení, který vám pomůžeme vygenerovat odpověď HTML. Pojďme se podívat na to, jak to můžeme udělat.

> [!div class="step-by-step"]
> [Předchozí](getting-started.md)Další
> [](adding-a-view.md)

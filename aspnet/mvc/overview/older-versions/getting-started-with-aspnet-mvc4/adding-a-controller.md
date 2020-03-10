---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
title: Přidání kontroleru | Microsoft Docs
author: Rick-Anderson
description: 'Poznámka: v této části je k dispozici aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013. Je to bezpečnější, takže je mnohem jednodušší postupovat a demo...'
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 0267d31c-892f-49a1-9e7a-3ae8cc12b2ca
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: f528c56435976c7f31fce453c834ef9eaebe6244
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78599839"
---
# <a name="adding-a-controller"></a>Přidání kontroleru

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> > [!NOTE]
> > K [dispozici je](../../getting-started/introduction/getting-started.md) aktualizovaná verze tohoto kurzu, která používá ASP.NET MVC 5 a Visual Studio 2013. Je to bezpečnější, mnohem jednodušší a ukazuje více funkcí.

MVC představuje *kontroler-View-Controller*. MVC je vzor pro vývoj aplikací, které jsou dobře architektované, testovatelné a snadno udržovatelnější. Aplikace založené na MVC obsahují:

- **M** Odels: třídy, které reprezentují data aplikace a používají logiku ověřování k vyhodnocování obchodních pravidel pro tato data.
- **V** iews: soubory šablon, které vaše aplikace používá k dynamickému generování odpovědí HTML.
- **C** Ontrollers: třídy, které zpracovávají příchozí požadavky prohlížeče, načítají data modelu a pak určují šablony zobrazení, které vracejí odpověď prohlížeči.

Pokryjeme všechny tyto koncepty v této sérii kurzů a ukážeme vám, jak je používat k sestavení aplikace.

Pojďme začít vytvořením třídy Controller. V **Průzkumník řešení**klikněte pravým tlačítkem na složku *Controllers* a pak vyberte **Přidat kontroler**.

![](adding-a-controller/_static/image1.png)

Pojmenujte nový kontroler &quot;HelloWorldController&quot;. Ponechte výchozí šablonu jako **prázdný kontroler MVC** a klikněte na **Přidat**.

![Přidat kontroler](adding-a-controller/_static/image2.png)

Všimněte si **Průzkumník řešení** , že byl vytvořen nový soubor s názvem *HelloWorldController.cs*. Soubor je otevřen v integrovaném vývojovém prostředí.

![](adding-a-controller/_static/image3.png)

Obsah souboru nahraďte následujícím kódem.

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

Metody kontroleru vrátí jako příklad řetězec HTML. Kontroler má název `HelloWorldController` a první výše uvedená metoda je pojmenována `Index`. Pojďme to vyvolat z prohlížeče. Spusťte aplikaci (stiskněte klávesu F5 nebo CTRL + F5). V prohlížeči přidejte &quot;HelloWorld&quot; do cesty na adresním řádku. (Například na obrázku níže je `http://localhost:1234/HelloWorld.`) Stránka v prohlížeči bude vypadat jako na následujícím snímku obrazovky. V metodě výše kód vrátil řetězec přímo. Dozvěděli jste systém, aby vracel jenom určitý kód HTML a byl.

![](adding-a-controller/_static/image4.png)

ASP.NET MVC vyvolá různé třídy kontroleru (a v rámci nich různé metody akcí) v závislosti na příchozí adrese URL. Výchozí logika směrování adres URL, kterou používá ASP.NET MVC, používá formát podobný tomuto: k určení kódu, který se má vyvolat:

`/[Controller]/[ActionName]/[Parameters]`

První část adresy URL určuje třídu kontroleru, která se má spustit. Proto */HelloWorld* mapuje na třídu `HelloWorldController`. Druhá část adresy URL určuje metodu Action pro třídu, která má být provedena. */HelloWorld/index* by proto způsobila spuštění metody `Index` `HelloWorldController` třídy. Všimněte si, že jsme museli procházet na */HelloWorld* a ve výchozím nastavení se použila metoda `Index`. Důvodem je, že metoda s názvem `Index` je výchozí metoda, která bude volána na řadiči, pokud není explicitně určena.

Přejděte na `http://localhost:xxxx/HelloWorld/Welcome`. Metoda `Welcome` se spustí a vrátí řetězec, &quot;se jedná o metodu akce Welcome...&quot;. Výchozí mapování MVC je `/[Controller]/[ActionName]/[Parameters]`. Pro tuto adresu URL se kontroler `HelloWorld` a `Welcome` je metoda Action. Zatím jste nepoužili `[Parameters]` část této adresy URL.

![](adding-a-controller/_static/image5.png)

Pojďme tento příklad mírně upravit, abyste mohli předat nějaké informace o parametrech z adresy URL do kontroleru (například */HelloWorld/Welcome? Name = Scott&amp;numtimes = 4*). Změňte metodu `Welcome` tak, aby zahrnovala dva parametry, jak je uvedeno níže. Všimněte si, že kód používá C# funkci volitelného parametru k označení toho, že parametr `numTimes` by měl být nastaven na hodnotu 1, pokud není pro tento parametr předána žádná hodnota.

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

Spusťte aplikaci a přejděte k ukázkové adrese URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`. Můžete zkusit jiné hodnoty pro `name` a `numtimes` v adrese URL. [Systém vazby modelu ASP.NET MVC](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automaticky mapuje pojmenované parametry z řetězce dotazu v adresním řádku na parametry v metodě.

![](adding-a-controller/_static/image6.png)

V obou těchto příkladech kontroler provedl &quot;VC&quot; část MVC – to znamená, že zobrazení a kontroler fungují. Kontroler přímo vrací HTML. Obvykle nechcete, aby řadiče vracely kód HTML přímo, protože to může být velmi nenáročné na kód. Místo toho obvykle použijete samostatný soubor šablony zobrazení, který vám pomůžeme vygenerovat odpověď HTML. Pojďme se podívat na to, jak to můžeme udělat.

> [!div class="step-by-step"]
> [Předchozí](intro-to-aspnet-mvc-4.md)
> [Další](adding-a-view.md)

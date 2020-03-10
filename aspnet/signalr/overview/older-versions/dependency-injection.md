---
uid: signalr/overview/older-versions/dependency-injection
title: Vkládání závislostí v návěsti 1. x | Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/15/2013
ms.assetid: eaa206c4-edb3-487e-8fcb-54a3261fed36
msc.legacyurl: /signalr/overview/older-versions/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: de838ab6b3a299eb1e5ebeb9fa3c583478ce3e56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536951"
---
# <a name="dependency-injection-in-signalr-1x"></a>Injektáž závislostí v centrech SignalR 1.x

[Jan Wasson](https://github.com/MikeWasson), [Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

Injektáže závislosti je způsob, jak odebrat pevně kódované závislosti mezi objekty, což usnadňuje nahrazení závislostí objektu buď pro účely testování (pomocí objektů typu), nebo pro změnu chování za běhu. V tomto kurzu se dozvíte, jak provádět vkládání závislostí na rozbočovačích pro Signal. Také ukazuje, jak používat kontejnery IoC s nástrojem Signal. Kontejner IoC je obecná architektura pro vkládání závislostí.

## <a name="what-is-dependency-injection"></a>Co je vkládání závislostí?

Pokud jste již obeznámeni se vkládáním závislostí, přeskočte tuto část.

*Vkládání závislostí* (di) je vzor, ve kterém objekty nejsou zodpovědné za vytváření vlastních závislostí. Tady je jednoduchý příklad pro motivaci DI. Předpokládejme, že máte objekt, který potřebuje Protokolovat zprávy. Můžete definovat protokolovací rozhraní:

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

Ve svém objektu můžete vytvořit `ILogger` pro protokolování zpráv:

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

To funguje, ale nejedná se o nejlepší návrh. Pokud chcete nahradit `FileLogger` jinou implementací `ILogger`, budete muset změnit `SomeComponent`. Supposing, že mnoho dalších objektů používá `FileLogger`, budete je muset změnit. Nebo pokud se rozhodnete nastavit `FileLogger` typu Singleton, budete také muset provést změny v celé aplikaci.

Lepším přístupem je "vložení" `ILogger` do objektu, například pomocí argumentu konstruktoru:

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

Nyní objekt není zodpovědný za výběr, který `ILogger` použít. Můžete přepínat `ILogger` implementace, aniž byste museli měnit objekty, které jsou na ní závislé.

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

Tento model se nazývá [Injektáže konstruktoru](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection). Dalším vzorem je vkládání pomocí metody Setter, kde můžete nastavit závislost prostřednictvím metody setter nebo vlastnosti.

## <a name="simple-dependency-injection-in-signalr"></a>Jednoduché vkládání závislostí v nástroji Signal

Zvažte aplikaci Chat z kurzu [Začínáme se signálem](../getting-started/tutorial-getting-started-with-signalr.md). Tady je třída centra z této aplikace:

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

Předpokládejme, že chcete před odesláním na server uložit zprávy chatu. Můžete definovat rozhraní, které tuto funkci abstrakce, a použít DI pro vložení rozhraní do třídy `ChatHub`.

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

Jediným problémem je, že aplikace signalizace nevytváří přímo rozbočovače; Signál je vytvoří za vás. Ve výchozím nastavení signál očekává, že třída rozbočovače má konstruktor bez parametrů. Můžete ale snadno zaregistrovat funkci pro vytváření instancí centra a pomocí této funkce provádět DI. Zaregistrujte funkci voláním **GlobalHost. DependencyResolver. Register**.

[!code-csharp[Main](dependency-injection/samples/sample7.cs)]

Signál Now tuto anonymní funkci vyvolá vždy, když je potřeba vytvořit instanci `ChatHub`.

## <a name="ioc-containers"></a>Kontejnery IoC

Předchozí kód je v jednoduchých případech jemný. Ale pořád byste to měli napsat:

[!code-css[Main](dependency-injection/samples/sample8.css)]

Ve složitých aplikacích s mnoha závislostmi může být potřeba napsat spoustu tohoto "" kabelážního "kódu. Údržbu tohoto kódu může být obtížné, zejména v případě, že jsou závislosti vnořené. Je také obtížné testování částí.

Jedním z řešení je použít kontejner IoC. Kontejner IoC je softwarová součást, která zodpovídá za správu závislostí. Zaregistrujte typy s kontejnerem a potom pomocí kontejneru vytvořte objekty. Kontejner automaticky vyhodnotí vztahy závislostí. Mnoho kontejnerů IoC vám také umožňuje řídit objekty, jako je život a rozsah objektu.

> [!NOTE]
> "IoC" je zkratka "inverze ovládacího prvku", což je obecný vzor, ve kterém rozhraní volá kód aplikace. Kontejner IoC sestaví vaše objekty za vás, což "Invertuje" běžný tok řízení.

## <a name="using-ioc-containers-in-signalr"></a>Používání kontejnerů IoC v nástroji Signal

Aplikace chatu je pravděpodobně příliš jednoduchá a nemůže těžit z kontejneru IoC. Místo toho se podívejme na ukázku [StockTicker](http://nuget.org/packages/microsoft.aspnet.signalr.sample) .

Ukázka StockTicker definuje dvě hlavní třídy:

- `StockTickerHub`: třída centra, která spravuje připojení klientů.
- `StockTicker`: typ singleton, který má skladové ceny a pravidelně je aktualizuje.

`StockTickerHub` drží odkaz na `StockTicker` singleton, zatímco `StockTicker` obsahuje odkaz na **IHubConnectionContext** pro `StockTickerHub`. Toto rozhraní používá ke komunikaci s `StockTickerHub` instancemi. (Další informace najdete v tématu [všesměrové vysílání serveru pomocí nástroje ASP.NET Signal](index.md).)

Pomocí kontejneru IoC můžete rozplétání tyto závislosti bitu. Nejprve Zjednodušte `StockTickerHub` a `StockTicker` třídy. V následujícím kódu jsem zakomentované části, které nepotřebujeme.

Odeberte konstruktor bez parametrů z `StockTicker`. Místo toho se k vytvoření centra vždycky používá DI.

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

V případě StockTicker odeberte instanci typu singleton. Později použijeme kontejner IoC k řízení životnosti StockTicker. Také vytvořte konstruktor jako veřejný.

[!code-csharp[Main](dependency-injection/samples/sample10.cs?highlight=7)]

V dalším kroku můžeme kód Refaktorovat vytvořením rozhraní pro `StockTicker`. Toto rozhraní použijeme k oddělit `StockTickerHub` od `StockTicker` třídy.

Visual Studio usnadňuje tento druh refaktoringu. Otevřete soubor StockTicker.cs, klikněte pravým tlačítkem na deklaraci třídy `StockTicker` a vyberte **refaktoring** ... **Rozbalte rozhraní**.

![](dependency-injection/_static/image1.png)

V dialogovém okně **rozbalte rozhraní** klikněte na **Vybrat vše**. Zbytek ponechte ve výchozím nastavení. Klikněte na tlačítko **OK**.

![](dependency-injection/_static/image2.png)

Visual Studio vytvoří nové rozhraní s názvem `IStockTicker`a také změní `StockTicker` odvodit z `IStockTicker`.

Otevřete soubor IStockTicker.cs a změňte rozhraní na **veřejné**.

[!code-csharp[Main](dependency-injection/samples/sample11.cs?highlight=1)]

Ve třídě `StockTickerHub` změňte dvě instance `StockTicker` na `IStockTicker`:

[!code-csharp[Main](dependency-injection/samples/sample12.cs?highlight=4,6)]

Vytvoření rozhraní `IStockTicker` není bezpodmínečně nutné, ale chtěl bych ukázat, jak DI může přispět k omezení spojení mezi komponentami v aplikaci.

## <a name="add-the-ninject-library"></a>Přidat knihovnu Ninject

Existuje mnoho Open Source kontejnerů IoC pro .NET. V tomto kurzu použijeme [Ninject](http://www.ninject.org/). (Mezi další oblíbené knihovny patří [Castle Windsor](http://www.castleproject.org/), [Spring.NET](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Unity](https://github.com/unitycontainer/unity)a [StructureMap](http://docs.structuremap.net).)

Pomocí Správce balíčků NuGet nainstalujte [knihovnu Ninject](https://nuget.org/packages/Ninject/3.0.1.10). V aplikaci Visual Studio v nabídce **nástroje** vyberte **správce balíčků NuGet** > **konzolu Správce balíčků**. V okně konzoly Správce balíčků zadejte následující příkaz:

[!code-powershell[Main](dependency-injection/samples/sample13.ps1)]

## <a name="replace-the-signalr-dependency-resolver"></a>Výměna překladače závislosti signálu

Chcete-li v rámci signálu Ninject použít, vytvořte třídu, která je odvozena z **DefaultDependencyResolver**.

[!code-csharp[Main](dependency-injection/samples/sample14.cs)]

Tato třída Přepisuje metody **GetService** a **GetServices** třídy **DefaultDependencyResolver**. Signál volá tyto metody k vytvoření různých objektů za běhu, včetně instancí centra, a také různých služeb používaných interně nástrojem Signal.

- Metoda **GetService** vytvoří jednu instanci typu. Přepsat tuto metodu pro volání metody **TryGet** jádra Ninject Pokud tato metoda vrátí hodnotu null, vraťte se k výchozímu Překladači.
- Metoda **GetServices** vytvoří kolekci objektů zadaného typu. Přepište tuto metodu pro zřetězení výsledků z Ninject s výsledky z výchozího překladače.

## <a name="configure-ninject-bindings"></a>Konfigurace vazeb Ninject

Nyní použijeme Ninject k deklarování vazeb typů.

Otevřete soubor RegisterHubs.cs. V metodě `RegisterHubs.Start` vytvořte kontejner Ninject, který Ninject volá *jádro*.

[!code-csharp[Main](dependency-injection/samples/sample15.cs)]

Vytvořte instanci našeho vlastního překladače závislosti:

[!code-csharp[Main](dependency-injection/samples/sample16.cs)]

Vytvořte vazbu pro `IStockTicker` následujícím způsobem:

[!code-html[Main](dependency-injection/samples/sample17.html)]

Tento kód říká dvě věci. Nejprve, kdykoli aplikace potřebuje `IStockTicker`, by jádro mělo vytvořit instanci `StockTicker`. Druhý, třída `StockTicker` by měla být vytvořená jako objekt typu singleton. Ninject vytvoří jednu instanci objektu a vrátí stejnou instanci pro každý požadavek.

Vytvořte vazbu pro **IHubConnectionContext** následujícím způsobem:

[!code-csharp[Main](dependency-injection/samples/sample18.cs)]

Tento kód vytvoří anonymní funkci, která vrátí **IHubConnection**. Metoda **WhenInjectedInto** přikáže Ninject, aby tuto funkci používala pouze při vytváření instancí `IStockTicker`. Důvodem je, že signál vytváří instance **IHubConnectionContext** interně a nechceme přepsat způsob, jakým ho signál vytvoří. Tato funkce se vztahuje pouze na naši třídu `StockTicker`.

Předejte překladač závislosti do metody **MapHubs** :

[!code-csharp[Main](dependency-injection/samples/sample19.cs)]

Nyní bude signál používat překladač zadaný v **MapHubs**namísto výchozího překladače.

Zde je kompletní výpis kódu pro `RegisterHubs.Start`.

[!code-csharp[Main](dependency-injection/samples/sample20.cs)]

Chcete-li spustit aplikaci StockTicker v aplikaci Visual Studio, stiskněte klávesu F5. V okně prohlížeče přejděte na `http://localhost:*port*/SignalR.Sample/StockTicker.html`.

![](dependency-injection/_static/image3.png)

Aplikace má naprosto stejné funkce jako předtím. (Popis najdete v tématu [vysílání serveru pomocí nástroje ASP.NET Signal](index.md).) Nezměnili jsme chování. Právě jsme usnadnili testování, údržbu a vývoj kódu.

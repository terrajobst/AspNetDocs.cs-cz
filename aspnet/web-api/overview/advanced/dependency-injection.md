---
uid: web-api/overview/advanced/dependency-injection
title: Vkládání závislostí ve webovém rozhraní API ASP.NET 2 – ASP.NET 4. x
author: MikeWasson
description: V tomto kurzu se dozvíte, jak vložit závislosti do kontroleru webového rozhraní API ASP.NET pro ASP.NET 4. x.
ms.author: riande
ms.date: 01/20/2014
ms.custom: seoapril2019
ms.assetid: e3d3e7ba-87f0-4032-bdd3-31f3c1aa9d9c
msc.legacyurl: /web-api/overview/advanced/dependency-injection
msc.type: authoredcontent
ms.openlocfilehash: f9c212af92168ac02644625b9aa8ec1bef329cab
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600413"
---
# <a name="dependency-injection-in-aspnet-web-api-2"></a>Vkládání závislostí ve webovém rozhraní API 2 ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-468ee148)

> V tomto kurzu se dozvíte, jak vložit závislosti do vašeho kontroleru webového rozhraní API ASP.NET.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové rozhraní API 2
> - [Blok aplikace Unity](https://www.nuget.org/packages/Unity/)
> - Entity Framework 6 (verze 5 také funguje)

## <a name="what-is-dependency-injection"></a>Co je vkládání závislostí?

*Závislost* je libovolný objekt, který vyžaduje jiný objekt. Například je běžné definovat [úložiště](http://martinfowler.com/eaaCatalog/repository.html) , které zpracovává přístup k datům. Podívejme se na příklad. Nejdřív definujeme model domény:

[!code-csharp[Main](dependency-injection/samples/sample1.cs)]

Tady je jednoduchá třída úložiště, která ukládá položky v databázi pomocí Entity Framework.

[!code-csharp[Main](dependency-injection/samples/sample2.cs)]

Nyní nadefinujte kontroler webového rozhraní API, který podporuje požadavky GET na `Product` entit. (Jsem opustili POST a další metody pro jednoduchost.) Toto je první pokus:

[!code-csharp[Main](dependency-injection/samples/sample3.cs)]

Všimněte si, že třída Controller závisí na `ProductRepository`a my umožňuje řadiči vytvořit instanci `ProductRepository`. To je však špatný nápad, jak tímto způsobem pevně zakódovat závislost, a to z několika důvodů.

- Pokud chcete nahradit `ProductRepository` jinou implementací, musíte také změnit třídu kontroleru.
- Pokud `ProductRepository` obsahuje závislosti, musíte je nakonfigurovat v rámci kontroleru. V případě velkého projektu s více řadiči je váš kód konfigurace rozptýlen napříč vaším projektem.
- Testování částí je obtížné, protože kontroler má pevně zakódovaný dotaz na databázi. Pro testování částí byste měli použít úložiště vzoru nebo zástupné procedury, které není možné s aktuálním návrhem.

Tyto problémy můžeme vyřešit *vložením* úložiště do kontroleru. Nejprve refaktorujte třídu `ProductRepository` do rozhraní:

[!code-csharp[Main](dependency-injection/samples/sample4.cs)]

Pak zadejte `IProductRepository` jako parametr konstruktoru:

[!code-csharp[Main](dependency-injection/samples/sample5.cs)]

Tento příklad používá [vkládání konstruktoru](http://www.martinfowler.com/articles/injection.html#FormsOfDependencyInjection). Lze také použít *Injektáže setter*, kde můžete nastavit závislost prostřednictvím metody setter nebo vlastnosti.

Nyní ale dojde k problému, protože aplikace nevytváří kontroler přímo. Webové rozhraní API vytvoří kontroler při směrování žádosti a webové rozhraní API neví o `IProductRepository`žádné informace. Zde je místo, kde se překladač závislostí webového rozhraní API nachází v.

## <a name="the-web-api-dependency-resolver"></a>Překladač závislostí webového rozhraní API

Webové rozhraní API definuje rozhraní **IDependencyResolver** pro řešení závislostí. Tady je definice rozhraní:

[!code-csharp[Main](dependency-injection/samples/sample6.cs)]

Rozhraní **IDependencyScope** má dvě metody:

- **GetService** vytvoří jednu instanci typu.
- **GetService** vytvoří kolekci objektů zadaného typu.

Metoda **IDependencyResolver** dědí **IDependencyScope** a přidá metodu **BeginScope** . V tomto kurzu budu mluvit o oborech později.

Když webové rozhraní API vytvoří instanci kontroleru, nejprve vyvolá **IDependencyResolver. GetService**, která předává typ kontroleru. Pomocí tohoto zavěšení rozšíření můžete vytvořit kontroler a vyřešit všechny závislosti. Pokud **GetService** vrátí hodnotu null, webové rozhraní API vyhledá konstruktor bez parametrů ve třídě Controller.

## <a name="dependency-resolution-with-the-unity-container"></a>Řešení závislostí s kontejnerem Unity

I když můžete napsat úplnou implementaci **IDependencyResolver** od začátku, rozhraní je ve skutečnosti navržené tak, aby fungovalo jako most mezi WEBOVÝm rozhraním API a stávajícími kontejnery IOC.

Kontejner IoC je softwarová součást, která zodpovídá za správu závislostí. Zaregistrujte typy s kontejnerem a potom pomocí kontejneru vytvořte objekty. Kontejner automaticky vyhodnotí vztahy závislostí. Mnoho kontejnerů IoC vám také umožňuje řídit objekty, jako je život a rozsah objektu.

> [!NOTE]
> "IoC" je zkratka "inverze ovládacího prvku", což je obecný vzor, ve kterém rozhraní volá kód aplikace. Kontejner IoC sestaví vaše objekty za vás, což "Invertuje" běžný tok řízení.

V tomto kurzu použijeme [Unity](https://msdn.microsoft.com/library/ff647202.aspx) ze vzorů Microsoft patterns &amp; postupů. (Mezi další oblíbené knihovny patří [Castle Windsor](http://www.castleproject.org/), [Spring.NET](http://www.springframework.net/), [Autofac](https://code.google.com/p/autofac/), [Ninject](http://www.ninject.org/)a [StructureMap](http://structuremap.github.io/documentation/).) K instalaci Unity můžete použít Správce balíčků NuGet. V nabídce **nástroje** v aplikaci Visual Studio vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**. V okně konzoly Správce balíčků zadejte následující příkaz:

[!code-console[Main](dependency-injection/samples/sample7.cmd)]

Zde je implementace **IDependencyResolver** , která obaluje kontejner Unity.

[!code-csharp[Main](dependency-injection/samples/sample8.cs)]

> [!NOTE]
> Pokud metoda **GetService** nemůže vyřešit typ, měla by vracet **hodnotu null**. Pokud metoda **GetServices** nemůže vyřešit typ, měl by vrátit prázdný objekt kolekce. Nevyvolává výjimky pro neznámé typy.

## <a name="configuring-the-dependency-resolver"></a>Konfigurace překladače závislostí

Nastavte překladač závislostí na vlastnost **DependencyResolver** globálního objektu **HttpConfiguration** .

Následující kód registruje rozhraní `IProductRepository` s Unity a potom vytvoří `UnityResolver`.

[!code-csharp[Main](dependency-injection/samples/sample9.cs)]

## <a name="dependency-scope-and-controller-lifetime"></a>Obor závislosti a životnost kontroleru

Řadiče se vytvářejí na základě požadavku. Aby bylo možné spravovat životnost objektů, používá **IDependencyResolver** koncept *oboru*.

Překladač závislostí připojený k objektu **HttpConfiguration** má globální rozsah. Když webové rozhraní API vytvoří kontroler, zavolá **BeginScope**. Tato metoda vrací objekt **IDependencyScope** , který představuje podřízený obor.

Webové rozhraní API pak zavolá metodu **GetService** v podřízeném oboru, aby vytvořila kontroler. Po dokončení žádosti webové rozhraní API zavolá **Dispose** v podřízeném oboru. K odstranění závislostí řadiče použijte metodu **Dispose** .

Způsob implementace **BeginScope** závisí na kontejneru IOC. V případě Unity rozsah odpovídá podřízenému kontejneru:

[!code-csharp[Main](dependency-injection/samples/sample10.cs)]

Většina IoCch kontejnerů má podobné ekvivalenty.

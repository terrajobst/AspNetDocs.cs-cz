---
uid: web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
title: Řadiče testování částí v ASP.NET webovém rozhraní API 2 | Microsoft Docs
author: MikeWasson
description: Toto téma popisuje některé konkrétní techniky pro řadiče testování částí ve webovém rozhraní API 2. Než si přečtete toto téma, možná budete chtít přečíst jednotku kurzu...
ms.author: riande
ms.date: 06/11/2014
ms.assetid: 43a6cce7-a3ef-42aa-ad06-90d36d49f098
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-controllers-in-web-api
msc.type: authoredcontent
ms.openlocfilehash: cdb1700537021e276669de1a9e0330a62659746c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554990"
---
# <a name="unit-testing-controllers-in-aspnet-web-api-2"></a>Testování jednotek kontrolerů webového rozhraní API 2 technologie ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

> Toto téma popisuje některé konkrétní techniky pro řadiče testování částí ve webovém rozhraní API 2. Než si přečtete toto téma, možná budete chtít přečíst kurz [testování částí ASP.NET webového rozhraní API 2](unit-testing-with-aspnet-web-api.md), které ukazuje, jak do řešení přidat projekt testování částí.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Webové rozhraní API 2
> - [MOQ](https://github.com/Moq) 4.5.30

> [!NOTE]
> Použil (a) jsem MOQ, ale stejný nápad se vztahuje i na jakékoli makety rozhraní. MOQ 4.5.30 (a novější) podporuje sady Visual Studio 2017, Roslyn a .NET 4,5 a novější verze.

Běžným vzorem při testování částí je &quot;příkaz Uspořádat-Act-Assert&quot;:

- Uspořádat: nastavte všechny požadované součásti pro spuštění testu.
- ACT: proveďte test.
- Assert: Ověřte, že test proběhl úspěšně.

V kroku uspořádat často použijete objekty s přípravou nebo se zástupnými procedurami. Který minimalizuje počet závislostí, takže se test zaměřuje na testování jedné věci.

Tady je několik věcí, které byste měli testovat jednotkou v řadičích webového rozhraní API:

- Akce vrátí správný typ odpovědi.
- Neplatné parametry vracejí správnou chybovou odpověď.
- Akce volá správnou metodu pro úložiště nebo vrstvu služby.
- Pokud odpověď obsahuje doménový model, ověřte typ modelu.

Jedná se o některé obecné věci, které je potřeba otestovat, ale konkrétní závisí na vaší implementaci kontroleru. Konkrétně se jedná o velký rozdíl, zda akce kontroleru vrátí **HttpResponseMessage** nebo **IHttpActionResult**. Další informace o těchto typech výsledků najdete v tématu [výsledky akcí ve webovém rozhraní API 2](../getting-started-with-aspnet-web-api/action-results.md).

## <a name="testing-actions-that-return-httpresponsemessage"></a>Testování akcí, které vracejí HttpResponseMessage

Tady je příklad kontroleru, jehož akce vrací **HttpResponseMessage**.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample1.cs)]

Všimněte si, že kontroler používá vkládání závislostí pro vložení `IProductRepository`. Tím se kontroler testovatelné, protože můžete vložit maketu úložiště. Následující test jednotky ověřuje, že metoda `Get` zapisuje `Product` do těla odpovědi. Předpokládejme, že `repository` je `IProductRepository`typu.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample2.cs)]

Je důležité nastavit na řadiči **požadavek** a **konfiguraci** . V opačném případě se test nezdaří s **ArgumentNullException** nebo **InvalidOperationException**.

## <a name="testing-link-generation"></a>Testování generování odkazů

Metoda `Post` volá **UrlHelper. Link** a vytvoří odkazy v odpovědi. K tomu je potřeba pár dalších nastavení v testu jednotek:

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample3.cs)]

Třída **UrlHelper** potřebuje adresu URL požadavku a data směrování, takže test musí nastavovat hodnoty pro tyto. Další možností je **UrlHelper**nebo zástupné procedury. S tímto přístupem nahradíte výchozí hodnotu [ApiController. URL](https://msdn.microsoft.com/library/system.web.http.apicontroller.url.aspx) s použitím přípravné nebo zástupné verze, která vrací pevnou hodnotu.

Pojďme přepsat test pomocí [MOQ](https://github.com/Moq) Frameworku. Nainstalujte balíček NuGet `Moq` do testovacího projektu.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample4.cs)]

V této verzi nemusíte nastavovat žádná data trasy, protože **UrlHelper** typu vrátí konstantní řetězec.

## <a name="testing-actions-that-return-ihttpactionresult"></a>Testování akcí, které vracejí IHttpActionResult

Ve webovém rozhraní API 2 může akce kontroleru vracet **IHttpActionResult**, což je obdobou **ACTIONRESULT** ve ASP.NET MVC. Rozhraní **IHttpActionResult** definuje vzor příkazu pro vytváření odpovědí HTTP. Místo přímého vytvoření odpovědi kontroler vrátí **IHttpActionResult**. Později kanál vyvolá **IHttpActionResult** , aby vytvořil odpověď. Tento přístup usnadňuje psaní jednotkových testů, protože můžete přeskočit spoustu nastavení, které je potřeba pro **HttpResponseMessage**.

Tady je příklad kontroleru, jehož akce vrací **IHttpActionResult**.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample5.cs)]

Tento příklad ukazuje některé běžné vzory pomocí **IHttpActionResult**. Pojďme se podívat, jak je zkoušet jednotkou.

### <a name="action-returns-200-ok-with-a-response-body"></a>Akce vrátí 200 (OK) s textem odpovědi.

Metoda `Get` volá `Ok(product)`, pokud se produkt najde. V testu jednotek se ujistěte, že je návratový typ **OkNegotiatedContentResult** a vrácený produkt má správné ID.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample6.cs)]

Všimněte si, že test jednotky neprovede výsledek akce. Můžete předpokládat, že výsledek akce vytvoří odpověď HTTP správně. (To je důvod, proč rozhraní Web API má vlastní testy jednotek!)

### <a name="action-returns-404-not-found"></a>Akce vrátí 404 (Nenalezeno).

Metoda `Get` volá `NotFound()`, pokud produkt nenalezne. Pro tento případ test jednotek pouze kontroluje, zda je návratový typ **NotFoundResult**.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample7.cs)]

### <a name="action-returns-200-ok-with-no-response-body"></a>Akce vrátí 200 (OK) bez textu odpovědi.

Metoda `Delete` volá `Ok()`, aby vrátila prázdnou odpověď HTTP 200. Podobně jako v předchozím příkladu test jednotek kontroluje návratový typ, v tomto případě **OkResult**.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample8.cs)]

### <a name="action-returns-201-created-with-a-location-header"></a>Akce vrátí 201 (vytvořeno) s hlavičkou umístění.

Metoda `Post` volá `CreatedAtRoute`, aby vrátila odpověď HTTP 201 s identifikátorem URI v hlavičce umístění. V testu jednotky ověřte, zda akce nastavuje správné hodnoty směrování.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample9.cs)]

### <a name="action-returns-another-2xx-with-a-response-body"></a>Akce vrátí jiný 2xx s textem odpovědi.

Metoda `Put` volá `Content`, aby vrátila odpověď HTTP 202 (přijato) s textem odpovědi. Tento případ je podobný jako vracení 200 (OK), ale test jednotky by také měl zkontrolovat stavový kód.

[!code-csharp[Main](unit-testing-controllers-in-web-api/samples/sample10.cs)]

## <a name="additional-resources"></a>Další prostředky

- [Napodobování Entity Framework při testování jednotek webového rozhraní API 2 ASP.NET](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md)
- [Zápis testů pro službu ASP.NET Web API](https://blogs.msdn.com/b/youssefm/archive/2013/01/28/writing-tests-for-an-asp-net-webapi-service.aspx) (Blogový příspěvek – Youssef Moussaoui).
- [Ladění webového rozhraní API ASP.NET pomocí ladicího programu směrování](https://blogs.msdn.com/b/webdev/archive/2013/04/04/debugging-asp-net-web-api-with-route-debugger.aspx)

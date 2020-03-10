---
uid: web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
title: Ověřování modelu v ASP.NET Web API – ASP.NET 4. x
author: MikeWasson
description: Přehled ověřování modelu ve webovém rozhraní API ASP.NET pro ASP.NET 4. x
ms.author: riande
ms.date: 07/20/2012
ms.custom: seoapril2019
ms.assetid: 7d061207-22b8-4883-bafa-e89b1e7749ca
msc.legacyurl: /web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 531a66b7ab642bd012663517640f2766f1917f25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557237"
---
# <a name="model-validation-in-aspnet-web-api"></a>Ověření modelu ve webovém rozhraní API ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

Tento článek ukazuje, jak přidávat poznámky k vašim modelům, používat poznámky k ověřování dat a zpracovávat chyby ověřování ve webovém rozhraní API. Když klient odešle data do webového rozhraní API, často chcete ověřit data před jakýmkoli zpracováním. 

## <a name="data-annotations"></a>Datové poznámky

Ve webovém rozhraní API ASP.NET můžete použít atributy z oboru názvů [System. ComponentModel. DataAnnotations](/dotnet/api/system.componentmodel.dataannotations) k nastavení ověřovacích pravidel pro vlastnosti v modelu. Vezměte v úvahu následující model:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample1.cs)]

Pokud jste v ASP.NET MVC použili ověřování modelu, mělo by to vypadat dobře. **Požadovaný** atribut říká, že vlastnost `Name` nesmí mít hodnotu null. Atribut **Range** uvádí, že `Weight` musí být mezi nulou a 999.

Předpokládejme, že klient pošle požadavek POST s následující reprezentací JSON:

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample2.json)]

Můžete vidět, že klient neobsahuje vlastnost `Name`, která je označena jako povinná. Když webové rozhraní API převede JSON na instanci `Product`, ověří `Product` na základě ověřovacích atributů. V akci kontroleru si můžete ověřit, jestli je model platný:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample3.cs)]

Ověřování modelu nezaručuje, že jsou data klienta bezpečná. Další ověřování může být potřeba v jiných vrstvách aplikace. (Například datová vrstva může vynutit omezení cizího klíče.) Tento kurz [s použitím webového rozhraní API Entity Framework](../data/using-web-api-with-entity-framework/part-1.md) prozkoumává některé z těchto problémů.

Pokud klient opustí některé vlastnosti, stane se pod položkou " **odesílání"** . Předpokládejme například, že klient odesílá následující:

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample4.json)]

V tomto případě klient neurčil hodnoty pro `Price` ani `Weight`. Formátovací modul JSON přiřadí výchozí hodnotu nula chybějícím vlastnostem.

![](model-validation-in-aspnet-web-api/_static/image1.png)

Stav modelu je platný, protože nula je platná hodnota pro tyto vlastnosti. Bez ohledu na to, jestli se jedná o problém, závisí na vašem scénáři. Například v operaci aktualizace můžete chtít rozlišovat mezi "0" a "nenastavenou". Chcete-li vynutit, aby klienti nastavili hodnotu, nastavte vlastnost na hodnotu null a nastavte **požadovaný** atribut:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample5.cs?highlight=1-2)]

**"** Při přeposílání": klient může také odesílat *více* dat, než jste očekávali. Příklad:

[!code-json[Main](model-validation-in-aspnet-web-api/samples/sample6.json)]

V tomto příkladu obsahuje JSON vlastnost ("Color"), která neexistuje v modelu `Product`. V tomto případě formátovací modul JSON jednoduše tuto hodnotu ignoruje. (Formátovací modul XML je stejný.) Při převzetí služeb při selhání dochází k problémům, pokud má váš model vlastnosti, které máte v úmyslu jen pro čtení. Příklad:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample7.cs)]

Nechcete, aby uživatelé aktualizovali vlastnost `IsAdmin` a mohli se zvýšit oprávnění správcům! Nejbezpečnější strategií je použít třídu modelu, která přesně odpovídá, co může klient odesílat:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample8.cs)]

> [!NOTE]
> Wilson Blogový příspěvek "[ověření vstupu vs. ověřování modelů v ASP.NET MVC](http://bradwilson.typepad.com/blog/2010/01/input-validation-vs-model-validation-in-aspnet-mvc.html)" obsahuje dobrou diskuzi o tom, jak se účtují a proúčtují. I když je příspěvek o ASP.NET MVC 2, problémy jsou stále relevantní pro webové rozhraní API.

## <a name="handling-validation-errors"></a>Zpracování chyb ověřování

Webové rozhraní API nevrátí klientovi automaticky chybu, pokud se ověření nepovede. Je až do akce kontroleru ke kontrole stavu modelu a odpovídajícím způsobem reagovat.

Můžete také vytvořit filtr akcí pro kontrolu stavu modelu před vyvoláním akce kontroleru. Příklad ukazuje následující kód:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample9.cs)]

Pokud ověření modelu neproběhne úspěšně, vrátí tento filtr odpověď HTTP, která obsahuje chyby ověřování. V takovém případě není vyvolána akce kontroleru.

[!code-console[Main](model-validation-in-aspnet-web-api/samples/sample10.cmd)]

Pokud chcete tento filtr použít u všech řadičů webového rozhraní API, přidejte do kolekce **HttpConfiguration. filters** během konfigurace instanci filtru:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample11.cs)]

Další možností je nastavit filtr jako atribut na jednotlivé řadiče nebo akce kontroleru:

[!code-csharp[Main](model-validation-in-aspnet-web-api/samples/sample12.cs)]

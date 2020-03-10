---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: Výsledek akce ve webovém rozhraní API 2 – ASP.NET 4. x
author: MikeWasson
description: Popisuje způsob, jakým webové rozhraní API ASP.NET převádí návratovou hodnotu z akce kontroleru na zprávu odpovědi HTTP v ASP.NET 4. x.
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: f00ac0db453053e53d6d6942dd1557b409f4167b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557055"
---
# <a name="action-results-in-web-api-2"></a>Výsledky akcí ve webovém rozhraní API 2

[!INCLUDE[](~/includes/coreWebAPI.md)]

Toto téma popisuje, jak webové rozhraní API ASP.NET převádí návratovou hodnotu z akce kontroleru na zprávu HTTP Response.

Akce kontroleru webového rozhraní API může vracet následující:

1. void
2. **HttpResponseMessage**
3. **IHttpActionResult**
4. Nějaký jiný typ

V závislosti na tom, které z těchto funkcí se vrátí, webové rozhraní API použije jiný mechanismus k vytvoření odpovědi HTTP.

| Návratový typ | Způsob, jakým webové rozhraní API vytvoří odpověď |
| --- | --- |
| void | Vrátit prázdné číslo 204 (žádný obsah) |
| **HttpResponseMessage** | Převeďte přímo na zprávu odpovědi HTTP. |
| **IHttpActionResult** | Voláním **metody ExecuteAsync** vytvořte **HttpResponseMessage**a pak proveďte převod na zprávu odpovědi HTTP. |
| Jiný typ | Zapsat serializovanou návratovou hodnotu do těla odpovědi; Vrátí 200 (OK). |

Zbývající část tohoto tématu popisuje jednotlivé možnosti podrobněji.

## <a name="void"></a>void

Pokud je návratový typ `void`, webové rozhraní API jednoduše vrátí prázdnou odpověď HTTP se stavovým kódem 204 (žádný obsah).

Příklad kontroleru:

[!code-csharp[Main](action-results/samples/sample1.cs)]

Odpověď HTTP:

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a>HttpResponseMessage

Pokud akce vrátí [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), webové rozhraní API převede návratovou hodnotu přímo do zprávy odpovědi HTTP pomocí vlastností objektu **HttpResponseMessage** k naplnění odpovědi.

Tato možnost vám poskytne velkou kontrolu nad zprávou odpovědi. Například následující akce kontroleru nastaví hlavičku Cache-Control.

[!code-csharp[Main](action-results/samples/sample3.cs)]

Odpověď:

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

Pokud předáte doménový model metodě **CreateResponse** , webové rozhraní API pomocí [formátovacího modulu médií](../formats-and-model-binding/media-formatters.md) zapíše serializovaný model do těla odpovědi.

[!code-csharp[Main](action-results/samples/sample5.cs)]

Webové rozhraní API používá k výběru formátovacího modulu hlavičku Accept v žádosti. Další informace najdete v tématu [vyjednávání obsahu](../formats-and-model-binding/content-negotiation.md).

## <a name="ihttpactionresult"></a>IHttpActionResult

Rozhraní **IHttpActionResult** bylo zavedeno ve webovém rozhraní API 2. V podstatě definuje objekt pro vytváření **HttpResponseMessage** . Zde jsou některé výhody použití rozhraní **IHttpActionResult** :

- Zjednodušuje [testování částí](../testing-and-debugging/unit-testing-controllers-in-web-api.md) vašich řadičů.
- Přesune společnou logiku pro vytváření odpovědí HTTP na samostatné třídy.
- Provede záměr akce kontroleru tím, že skryje podrobnosti nízké úrovně konstrukce odpovědi.

**IHttpActionResult** obsahuje jedinou metodu **metody ExecuteAsync**, která asynchronně vytvoří instanci **HttpResponseMessage** .

[!code-csharp[Main](action-results/samples/sample6.cs)]

Pokud akce kontroleru vrátí **IHttpActionResult**, webové rozhraní API zavolá metodu **metody ExecuteAsync** , která vytvoří **HttpResponseMessage**. Pak převede **HttpResponseMessage** na zprávu odpovědi HTTP.

Tady je jednoduchá implementace **IHttpActionResult** , která vytvoří odpověď v podobě prostého textu:

[!code-csharp[Main](action-results/samples/sample7.cs)]

Příklad akce kontroleru:

[!code-csharp[Main](action-results/samples/sample8.cs)]

Odpověď:

[!code-console[Main](action-results/samples/sample9.cmd)]

Častěji používáte implementace **IHttpActionResult** definované v oboru názvů **[System. Web. http. Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** . Třída **ApiController** definuje pomocné metody, které vracejí tyto předdefinované výsledky akcí.

Pokud se v následujícím příkladu požadavek neshoduje s existujícím ID produktu, kontroler zavolá [ApiController. NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) , aby vytvořil odpověď 404 (Nenalezeno). V opačném případě kontroler zavolá [ApiController. ok](https://msdn.microsoft.com/library/dn314591.aspx), čímž se vytvoří odpověď 200 (ok), která obsahuje daný produkt.

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a>Jiné návratové typy

Pro všechny ostatní návratové typy používá webové rozhraní API [formátovací modul médií](../formats-and-model-binding/media-formatters.md) k serializaci návratové hodnoty. Webové rozhraní API zapisuje serializovanou hodnotu do těla odpovědi. Stavový kód odpovědi je 200 (OK).

[!code-csharp[Main](action-results/samples/sample11.cs)]

Nevýhodou tohoto přístupu je, že nemůžete přímo vracet kód chyby, například 404. Můžete však vyvolat **HttpResponseException** pro kódy chyb. Další informace najdete v tématu [zpracování výjimek ve webovém rozhraní API ASP.NET](../error-handling/exception-handling.md).

Webové rozhraní API používá k výběru formátovacího modulu hlavičku Accept v žádosti. Další informace najdete v tématu [vyjednávání obsahu](../formats-and-model-binding/content-negotiation.md).

Příklad požadavku

[!code-console[Main](action-results/samples/sample12.cmd)]

Příklad odpovědi

[!code-console[Main](action-results/samples/sample13.cmd)]

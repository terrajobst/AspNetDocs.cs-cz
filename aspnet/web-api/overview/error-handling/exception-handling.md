---
uid: web-api/overview/error-handling/exception-handling
title: Zpracování výjimek ve webovém rozhraní API ASP.NET – ASP.NET 4. x
author: MikeWasson
description: ''
ms.author: riande
ms.date: 03/12/2012
ms.custom: seoapril2019
ms.assetid: cbebeb37-2594-41f2-b71a-f4f26520d512
msc.legacyurl: /web-api/overview/error-handling/exception-handling
msc.type: authoredcontent
ms.openlocfilehash: dbdbab6aefec840e2fec9e9cd33f3d124093750e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622316"
---
# <a name="exception-handling-in-aspnet-web-api"></a>Zpracování výjimek ve webovém rozhraní API ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

Tento článek popisuje zpracování chyb a výjimek v ASP.NET webovém rozhraní API.

- [HttpResponseException](#httpresponserexception)
- [Filtry výjimek](#exception_filters)
- [Registrace filtrů výjimek](#registering_exception_filters)
- [HttpError](#httperror)

<a id="httpresponserexception"></a>
## <a name="httpresponseexception"></a>HttpResponseException

Co se stane, když kontroler webového rozhraní API vyvolá nezachycenou výjimku? Ve výchozím nastavení se většina výjimek převede na odpověď HTTP se stavovým kódem 500, interní chyba serveru.

Typ **HttpResponseException** je zvláštní případ. Tato výjimka vrátí jakýkoli stavový kód HTTP, který zadáte v konstruktoru výjimky. Například následující metoda vrátí 404, nebyla nalezena, pokud parametr *ID* není platný.

[!code-csharp[Main](exception-handling/samples/sample1.cs)]

Pro lepší kontrolu nad odpovědí můžete také sestavit celou zprávu odpovědi a zahrnout ji do **HttpResponseException:** 

[!code-csharp[Main](exception-handling/samples/sample2.cs)]

<a id="exception_filters"></a>
## <a name="exception-filters"></a>Filtry výjimek

Můžete přizpůsobit, jak webové rozhraní API zpracovává výjimky pomocí zápisu *filtru výjimek*. Filtr výjimek je proveden, pokud metoda kontroleru vyvolá jakoukoli neošetřenou výjimku, *která není* **HttpResponseException** výjimkou. Typ **HttpResponseException** je zvláštní případ, protože je navržený speciálně pro vracení odpovědi HTTP.

Filtry výjimek implementují rozhraní **System. Web. http. filters. IExceptionFilter** . Nejjednodušší způsob, jak napsat filtr výjimky, je odvozovat z třídy **System. Web. http. filters. ExceptionFilterAttribute** a přepsat metodu **s výjimkou** .

> [!NOTE]
> Filtry výjimek ve webovém rozhraní API ASP.NET jsou podobné těm v ASP.NET MVC. Jsou však deklarovány v samostatném oboru názvů a funkci samostatně. Konkrétně třída **HandleErrorAttribute** používaná v MVC nezpracovává výjimky vyvolané řadiči webového rozhraní API.

Tady je filtr, který převede výjimky **NotImplementedException** na stavový kód http 501, není implementováno:

[!code-csharp[Main](exception-handling/samples/sample3.cs)]

Vlastnost **Response** objektu **HttpActionExecutedContext** obsahuje zprávu odpovědi HTTP, která se pošle klientovi.

<a id="registering_exception_filters"></a>
## <a name="registering-exception-filters"></a>Registrace filtrů výjimek

Existuje několik způsobů, jak zaregistrovat filtr výjimky webového rozhraní API:

- Podle akce
- Podle kontroléru
- univerzál

Chcete-li použít filtr na konkrétní akci, přidejte filtr jako atribut do akce:

[!code-csharp[Main](exception-handling/samples/sample4.cs)]

Chcete-li použít filtr na všechny akce na řadiči, přidejte filtr jako atribut do třídy Controller:

[!code-csharp[Main](exception-handling/samples/sample5.cs)]

Pokud chcete filtr použít globálně na všechny řadiče webového rozhraní API, přidejte instanci filtru do kolekce **GlobalConfiguration. Configuration. filters** . Filtry výjimek v této kolekci platí pro všechny akce kontroleru webového rozhraní API.

[!code-csharp[Main](exception-handling/samples/sample6.cs)]

Pokud k vytvoření projektu použijete šablonu projektu webová aplikace ASP.NET MVC 4, vložte svůj konfigurační kód webového rozhraní API do třídy `WebApiConfig`, která je umístěna ve složce App\_Start:

[!code-csharp[Main](exception-handling/samples/sample7.cs?highlight=5)]

<a id="httperror"></a>
## <a name="httperror"></a>HttpError

Objekt **HttpError** poskytuje konzistentní způsob, jak vracet informace o chybě v těle odpovědi. Následující příklad ukazuje, jak vrátit stavový kód HTTP 404 (Nenalezeno) s **HttpError** v těle odpovědi.

[!code-csharp[Main](exception-handling/samples/sample8.cs)]

**CreateErrorResponse** je metoda rozšíření definovaná v třídě **System .NET. http. HttpRequestMessageExtensions** . Interně **CreateErrorResponse** vytvoří instanci **HttpError** a pak vytvoří **HttpResponseMessage** obsahující **HttpError**.

V tomto příkladu, pokud je metoda úspěšná, vrátí produkt v odpovědi HTTP. Pokud se ale požadovaný produkt nenajde, odpověď HTTP obsahuje **HttpError** v textu žádosti. Odpověď může vypadat takto:

[!code-console[Main](exception-handling/samples/sample9.cmd)]

Všimněte si, že v tomto příkladu byl v tomto příkladu serializován **HttpError** do formátu JSON. Jednou z výhod použití **HttpError** je to, že projde stejným procesem [pro vyjednávání obsahu](../formats-and-model-binding/content-negotiation.md) a serializaci jako jakýkoli jiný model silného typu.

### <a name="httperror-and-model-validation"></a>HttpError a ověření modelu

Pro ověření modelu můžete předat stav modelu do **CreateErrorResponse**, aby se zahrnuly chyby ověřování v odpovědi:

[!code-csharp[Main](exception-handling/samples/sample10.cs)]

Tento příklad může vracet následující odpověď:

[!code-console[Main](exception-handling/samples/sample11.cmd)]

Další informace o ověřování modelu najdete v tématu [ověřování modelu v ASP.NET webovém rozhraní API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).

### <a name="using-httperror-with-httpresponseexception"></a>Použití HttpError s HttpResponseException

Předchozí příklady vrátí zprávu **HttpResponseMessage** z akce kontroleru, ale můžete také použít **HttpResponseException** a vrátit **HttpError**. To vám umožní vracet model silného typu v normálním případě úspěchu a pořád vracet **HttpError** , pokud dojde k chybě:

[!code-csharp[Main](exception-handling/samples/sample12.cs)]

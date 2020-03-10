---
uid: web-api/overview/advanced/httpclient-message-handlers
title: Obslužné rutiny zpráv HttpClient ve ASP.NET Web API – ASP.NET 4. x
author: MikeWasson
description: Vytváření vlastních obslužných rutin zpráv pro webové rozhraní API ASP.NET v ASP.NET 4. x
ms.author: riande
ms.date: 10/01/2012
ms.custom: seoapril2019
ms.assetid: 5a4b6c80-b2e9-4710-8969-d5076f7f82b8
msc.legacyurl: /web-api/overview/advanced/httpclient-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: 265bd9b2f48ed7d1e955f3c4947d10fd589b3e17
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557643"
---
# <a name="httpclient-message-handlers-in-aspnet-web-api"></a>Obslužné rutiny zpráv HttpClient ve webovém rozhraní API ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

*Obslužná rutina zprávy* je třída, která přijme požadavek HTTP a vrátí odpověď HTTP.

Obvykle je řada obslužných rutin zpráv zřetězena dohromady. První obslužná rutina přijme požadavek HTTP, provede nějaké zpracování a udělí požadavek Další obslužné rutině. V určitém okamžiku se odpověď vytvoří a zálohuje řetězec. Tento model se nazývá *delegování* obslužné rutiny.

![](httpclient-message-handlers/_static/image1.png)

Na straně klienta třída **HttpClient** používá ke zpracování požadavků obslužnou rutinu zprávy. Výchozí obslužná rutina je **HttpClientHandler**, která odesílá požadavek přes síť a získá odpověď ze serveru. Do kanálu klienta můžete vložit vlastní obslužné rutiny zpráv:

![](httpclient-message-handlers/_static/image2.png)

> [!NOTE]
> Webové rozhraní API ASP.NET také používá obslužné rutiny zpráv na straně serveru. Další informace najdete v tématu [obslužné rutiny zpráv HTTP](http-message-handlers.md).

## <a name="custom-message-handlers"></a>Vlastní obslužné rutiny zpráv

Chcete-li napsat vlastní obslužnou rutinu zpráv, odvodit ze **System .NET. http. DelegatingHandler** a přepsat metodu **SendAsync** . Tady je podpis této metody:

[!code-csharp[Main](httpclient-message-handlers/samples/sample1.cs)]

Metoda přebírá **zprávy HttpRequestMessage** jako vstup a asynchronně vrátí **HttpResponseMessage**. Typická implementace provede následující:

1. Zpracování zprávy s požadavkem.
2. Zavolejte `base.SendAsync` k odeslání požadavku vnitřní obslužné rutině.
3. Vnitřní obslužná rutina vrátí zprávu odpovědi. (Tento krok je asynchronní.)
4. Zpracujte odpověď a vraťte ji volajícímu.

Následující příklad ukazuje popisovač zprávy, který přidá vlastní hlavičku do odchozího požadavku:

[!code-csharp[Main](httpclient-message-handlers/samples/sample2.cs)]

Volání `base.SendAsync` je asynchronní. Pokud obslužná rutina po tomto volání funguje, použijte klíčové slovo **await** pro pokračování v provádění po dokončení metody. Následující příklad ukazuje obslužnou rutinu, která protokoluje kódy chyb. Samotné protokolování není velice zajímavé, ale tento příklad ukazuje, jak získat odpověď v rámci obslužné rutiny.

[!code-csharp[Main](httpclient-message-handlers/samples/sample3.cs?highlight=10,13)]

## <a name="adding-message-handlers-to-the-client-pipeline"></a>Přidání obslužných rutin zpráv do kanálu klienta

Chcete-li přidat vlastní obslužné rutiny do **HttpClient**, použijte metodu **HttpClientFactory. Create** :

[!code-csharp[Main](httpclient-message-handlers/samples/sample4.cs)]

Obslužné rutiny zpráv jsou volány v pořadí, které je předáváte do metody **Create** . Vzhledem k tomu, že obslužné rutiny jsou vnořené, zpráva odpovědi se přenáší do druhého směru. To znamená, že poslední obslužná rutina je první, aby zobrazila zprávu odpovědi.

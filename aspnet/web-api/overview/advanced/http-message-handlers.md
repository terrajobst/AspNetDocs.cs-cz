---
uid: web-api/overview/advanced/http-message-handlers
title: Obslužné rutiny zpráv HTTP ve webovém rozhraní API ASP.NET – ASP.NET 4. x
author: MikeWasson
description: Přehled obslužných rutin zpráv HTTP ve webovém rozhraní API ASP.NET pro ASP.NET 4. x
ms.author: riande
ms.date: 02/13/2012
ms.custom: seoapril2019
ms.assetid: 9002018b-3aa3-4358-bb1c-fbb5bc751d01
msc.legacyurl: /web-api/overview/advanced/http-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: a8e6f1da8df4802e1acf7779a2fc75bfe8ab876f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622582"
---
# <a name="http-message-handlers-in-aspnet-web-api"></a>Obslužné rutiny zpráv HTTP ve webovém rozhraní API ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

*Obslužná rutina zprávy* je třída, která přijme požadavek HTTP a vrátí odpověď HTTP. Obslužné rutiny zpráv jsou odvozeny od abstraktní třídy **HttpMessageHandler** .

Obvykle je řada obslužných rutin zpráv zřetězena dohromady. První obslužná rutina přijme požadavek HTTP, provede nějaké zpracování a udělí požadavek Další obslužné rutině. V určitém okamžiku se odpověď vytvoří a zálohuje řetězec. Tento model se nazývá *delegování* obslužné rutiny.

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a>Obslužné rutiny zpráv na straně serveru

Kanál webového rozhraní API na straně serveru používá některé integrované obslužné rutiny zpráv:

- **HttpServer** Získá požadavek od hostitele.
- **HttpRoutingDispatcher** odesílá požadavek na základě trasy.
- **HttpControllerDispatcher** odešle požadavek na kontroler webového rozhraní API.

Do kanálu můžete přidat vlastní obslužné rutiny. Obslužné rutiny zpráv jsou vhodné pro průřezové problémy, které fungují na úrovni zpráv HTTP (místo akcí kontroleru). Například obslužná rutina zprávy může:

- Čtení nebo úpravy hlaviček požadavků.
- Přidejte hlavičku odpovědi na odpovědi.
- Ověřte žádosti předtím, než se dostanou k řadiči.

Tento diagram znázorňuje dva vlastní obslužné rutiny vložené do kanálu:

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> Na straně klienta HttpClient také používá obslužné rutiny zpráv. Další informace najdete v tématu [obslužné rutiny zpráv HttpClient](httpclient-message-handlers.md).

## <a name="custom-message-handlers"></a>Vlastní obslužné rutiny zpráv

Chcete-li napsat vlastní obslužnou rutinu zpráv, odvodit ze **System .NET. http. DelegatingHandler** a přepsat metodu **SendAsync** . Tato metoda má následující signaturu:

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

Metoda přebírá **zprávy HttpRequestMessage** jako vstup a asynchronně vrátí **HttpResponseMessage**. Typická implementace provede následující:

1. Zpracování zprávy s požadavkem.
2. Zavolejte `base.SendAsync` k odeslání požadavku vnitřní obslužné rutině.
3. Vnitřní obslužná rutina vrátí zprávu odpovědi. (Tento krok je asynchronní.)
4. Zpracujte odpověď a vraťte ji volajícímu.

Tady je triviální příklad:

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> Volání `base.SendAsync` je asynchronní. Pokud obslužná rutina po tomto volání funguje, použijte klíčové slovo **await** , jak je znázorněno.

Delegování obslužné rutiny může také přeskočit vnitřní obslužnou rutinu a přímo vytvořit odpověď:

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

Pokud obslužná rutina delegování vytvoří odpověď bez volání `base.SendAsync`, požadavek přeskočí zbytek kanálu. To může být užitečné pro obslužnou rutinu, která ověřuje požadavek (vytvoření chybové odpovědi).

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a>Přidání obslužné rutiny do kanálu

Chcete-li přidat obslužnou rutinu zprávy na straně serveru, přidejte obslužnou rutinu do kolekce **HttpConfiguration. MessageHandlers** . Pokud jste k vytvoření projektu použili šablonu webová aplikace ASP.NET MVC 4, můžete to provést uvnitř třídy **WebApiConfig** :

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

Obslužné rutiny zpráv jsou volány ve stejném pořadí, v jakém jsou uvedeny v kolekci **MessageHandlers** . Vzhledem k tomu, že jsou vnořené, bude zpráva odpovědi přenášena v jiném směru. To znamená, že poslední obslužná rutina je první, aby zobrazila zprávu odpovědi.

Všimněte si, že nemusíte nastavovat vnitřní obslužné rutiny; rozhraní Web API Framework automaticky propojuje obslužné rutiny zpráv.

Pokud provádíte [samoobslužné hostování](../older-versions/self-host-a-web-api.md), vytvořte instanci třídy **HttpSelfHostConfiguration** a přidejte obslužné rutiny do kolekce **MessageHandlers** .

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

Teď se podívejme na některé příklady vlastních obslužných rutin zpráv.

## <a name="example-x-http-method-override"></a>Příklad: X-HTTP-Method – přepsat

X-HTTP-Method-override je nestandardní hlavička HTTP. Je určená pro klienty, kteří nemůžou odesílat určité typy požadavků HTTP, jako je třeba PUT nebo DELETE. Místo toho klient odešle požadavek POST a nastaví hlavičku X-HTTP-Method-override na požadovanou metodu. Příklad:

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

Tady je obslužná rutina zprávy, která přidává podporu pro X-HTTP-Method-override:

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

V metodě **SendAsync** obslužná rutina kontroluje, zda je zpráva požadavku POST, a zda obsahuje hlavičku X-http-Method – přepsat. Pokud ano, ověří hodnotu v hlavičce a pak upraví metodu žádosti. Nakonec obslužná rutina volá `base.SendAsync` k předání zprávy do další obslužné rutiny.

Když požadavek dosáhne třídy **HttpControllerDispatcher** , **HttpControllerDispatcher** bude směrovat požadavek na základě aktualizované metody žádosti.

## <a name="example-adding-a-custom-response-header"></a>Příklad: Přidání vlastní hlavičky odpovědi

Tady je obslužná rutina zprávy, která přidá vlastní hlavičku do každé zprávy odpovědi:

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

Za prvé obslužná rutina volá `base.SendAsync`, aby odeslala požadavek do vnitřní obslužné rutiny zpráv. Vnitřní obslužná rutina vrátí zprávu odpovědi, ale provede asynchronní použití objektu **Task&lt;t&gt;** Object. Zpráva s odpovědí není k dispozici, dokud se `base.SendAsync` nedokončí asynchronně.

Tento příklad používá klíčové slovo **await** k asynchronnímu zpracování práce po dokončení `SendAsync`. Pokud cílíte .NET Framework 4,0, použijte&gt;**úlohy**&lt;t **. Metoda ContinueWith** :

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a>Příklad: Kontrola klíče rozhraní API

Některé webové služby vyžadují, aby klienti do své žádosti zahrnuli klíč rozhraní API. Následující příklad ukazuje, jak může obslužná rutina zprávy kontrolovat žádosti o platný klíč rozhraní API:

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

Tato obslužná rutina hledá klíč rozhraní API v řetězci dotazu identifikátoru URI. (V tomto příkladu předpokládáme, že klíč je statický řetězec. Skutečná implementace by pravděpodobně použila složitější ověřování.) Pokud řetězec dotazu obsahuje klíč, obslužná rutina předá požadavek vnitřní obslužné rutině.

Pokud požadavek nemá platný klíč, obslužná rutina vytvoří zprávu odpovědi se stavem 403, zakázáno. V tomto případě obslužná rutina nevolá `base.SendAsync`, takže vnitřní obslužná rutina nikdy neobdrží požadavek ani neprovádí kontroler. Proto může kontroler předpokládat, že všechny příchozí požadavky mají platný klíč rozhraní API.

> [!NOTE]
> Pokud se klíč rozhraní API vztahuje pouze na určité akce kontroleru, zvažte použití filtru akcí namísto obslužné rutiny zprávy. Filtry akcí se spustí po provedení směrování identifikátorů URI.

## <a name="per-route-message-handlers"></a>Obslužné rutiny zpráv pro směrování

Obslužné rutiny v kolekci **HttpConfiguration. MessageHandlers** platí globálně.

Případně můžete při definování trasy přidat do konkrétní trasy obslužnou rutinu zpráv:

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

Pokud v tomto příkladu identifikátor URI žádosti odpovídá "Route2", požadavek se odešle na `MessageHandler2`. Následující diagram znázorňuje kanál těchto dvou tras:

![](http-message-handlers/_static/image4.png)

Všimněte si, že `MessageHandler2` nahradí výchozí **HttpControllerDispatcher**. V tomto příkladu `MessageHandler2` vytvoří odpověď a požadavky, které odpovídají "Route2" nikdy nejdou na kontroler. To vám umožní nahradit celý mechanizmus kontroleru webového rozhraní API vlastním koncovým bodem.

Alternativně může obslužná rutina zprávy pro směrování delegovat na **HttpControllerDispatcher**, která pak odesílá do kontroleru.

![](http-message-handlers/_static/image5.png)

Následující kód ukazuje, jak nakonfigurovat tuto trasu:

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]

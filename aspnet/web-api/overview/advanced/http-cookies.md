---
uid: web-api/overview/advanced/http-cookies
title: Soubory cookie HTTP ve webovém rozhraní API ASP.NET – ASP.NET 4. x
author: MikeWasson
description: Popisuje, jak odesílat a přijímat soubory cookie HTTP ve webovém rozhraní API pro ASP.NET 4. x.
ms.author: riande
ms.date: 09/17/2012
ms.custom: seoapril2019
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 8ca26ff6776daa13bc4f8b06c2eba61afcfefba2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557685"
---
# <a name="http-cookies-in-aspnet-web-api"></a>Soubory cookie HTTP ve webovém rozhraní API technologie ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

Toto téma popisuje, jak odesílat a přijímat soubory cookie HTTP ve webovém rozhraní API.

## <a name="background-on-http-cookies"></a>Pozadí na souborech cookie HTTP

V této části najdete stručný přehled toho, jak se soubory cookie implementují na úrovni HTTP. Další podrobnosti najdete v [dokumentu RFC 6265](http://tools.ietf.org/html/rfc6265).

Soubor cookie je část dat, kterou server odesílá v odpovědi HTTP. Klient (volitelně) uloží soubor cookie a vrátí ho v dalších požadavcích. Tím umožníte, aby klient a server sdíleli stav. Aby bylo možné nastavit soubor cookie, bude server v odpovědi obsahovat hlavičku souborového souboru cookie. Formátem souboru cookie je pár název-hodnota s nepovinnými atributy. Příklad:

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

Tady je příklad s atributy:

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

Pokud chcete vrátit soubor cookie na server, klient zahrne v pozdějších požadavcích hlavičku souboru cookie.

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

Odpověď protokolu HTTP může zahrnovat více hlaviček souborů cookie sady.

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

Klient vrátí více souborů cookie pomocí jednoho záhlaví souboru cookie.

[!code-console[Main](http-cookies/samples/sample5.cmd)]

Rozsah a doba trvání souboru cookie jsou ovládány pomocí atributů v hlavičce Set-cookie:

- **Doména**: oznamuje klientovi, která doména má přijmout soubor cookie. Pokud je doména například "example.com", vrátí klient soubor cookie do každé subdomény example.com. Pokud není zadaný, doména je původním serverem.
- **Cesta**: omezí soubor cookie na zadanou cestu v doméně. Pokud není zadaný, použije se cesta k identifikátoru URI požadavku.
- **Expires**: nastaví datum vypršení platnosti souboru cookie. Klient odstraní soubor cookie, pokud vyprší jeho platnost.
- **Max-Age**: nastaví maximální stáří pro soubor cookie. Klient odstraní soubor cookie, pokud dosáhne maximálního stáří.

Pokud jsou nastaveny `Expires` i `Max-Age`, má `Max-Age` přednost. Pokud není nastavená ani jedna, klient při ukončení aktuální relace odstraní soubor cookie. (Přesný význam "session" určuje uživatel-agent.)

Upozorňujeme však, že klienti mohou ignorovat soubory cookie. Uživatel může například zakázat soubory cookie z důvodů ochrany osobních údajů. Klienti mohou odstranit soubory cookie před vypršením platnosti nebo omezit počet uložených souborů cookie. Z důvodu ochrany osobních údajů klienti často odmítnou soubory cookie třetích stran, kde doména neodpovídají zdrojovému serveru. V krátkém případě by se server neměl spoléhat na vrácení souborů cookie, které nastaví.

## <a name="cookies-in-web-api"></a>Soubory cookie ve webovém rozhraní API

Chcete-li přidat soubor cookie do odpovědi HTTP, vytvořte instanci **CookieHeaderValue** , která představuje soubor cookie. Pak zavolejte metodu rozšíření **AddCookies** , která je definována v **System .NET. http. HttpResponseHeadersExtensions** třída pro přidání souboru cookie.

Například následující kód přidá soubor cookie v rámci akce kontroleru:

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

Všimněte si, že **AddCookies** přebírá pole instancí **CookieHeaderValue** .

Chcete-li extrahovat soubory cookie z požadavku klienta, zavolejte metodu **GetCookies** :

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

**CookieHeaderValue** obsahuje kolekci instancí **CookieState** . Každý **CookieState** představuje jeden soubor cookie. Použijte metodu indexeru k získání **CookieState** podle názvu, jak je znázorněno na obrázku.

## <a name="structured-cookie-data"></a>Strukturovaná data souborů cookie

Mnoho prohlížečů omezuje počet souborů cookie, které budou&#8212;ukládat celkové číslo, a počet v každé doméně. Proto může být užitečné ukládat strukturovaná data do jediného souboru cookie namísto nastavení více souborů cookie.

> [!NOTE]
> Specifikace RFC 6265 nedefinuje strukturu dat souborů cookie.

Pomocí třídy **CookieHeaderValue** můžete předat seznam párů název-hodnota pro data souborů cookie. Tyto páry název-hodnota se kódují jako data formuláře kódovaná v adresách URL v hlavičce Set-cookie:

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

Předchozí kód vytvoří následující hlavičku souboru cookie sady:

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

Třída **CookieState** poskytuje indexerovou metodu pro čtení dílčích hodnot ze souboru cookie ve zprávě požadavku:

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a>Příklad: nastavení a načtení souborů cookie v obslužné rutině zprávy

Předchozí příklady ukázaly, jak používat soubory cookie v rámci kontroleru webového rozhraní API. Další možností je použít [obslužné rutiny zpráv](http-message-handlers.md). Obslužné rutiny zpráv jsou vyvolány dříve v kanálu než řadiče. Obslužná rutina zprávy může číst soubory cookie z požadavku předtím, než požadavek dosáhne kontroleru, nebo přidat soubory cookie do odpovědi poté, co kontroler odpověď vygeneruje.

![](http-cookies/_static/image2.png)

Následující kód ukazuje popisovač zprávy pro vytváření ID relací. ID relace je uloženo v souboru cookie. Obslužná rutina zkontroluje požadavek na soubor cookie relace. Pokud žádost nezahrnuje soubor cookie, obslužná rutina generuje nové ID relace. V obou případech obslužná rutina ukládá ID relace do kontejneru vlastností **zprávy HttpRequestMessage. Properties** . Také přidá soubor cookie relace do odpovědi HTTP.

Tato implementace neověřuje, zda je ID relace z klienta skutečně vydaným serverem. Nepoužívejte ji jako způsob ověřování. Bodem příkladu je zobrazení správy souborů cookie protokolu HTTP.

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

Kontroler může získat ID relace z kontejneru vlastností **zprávy HttpRequestMessage. Properties** .

[!code-csharp[Main](http-cookies/samples/sample12.cs)]

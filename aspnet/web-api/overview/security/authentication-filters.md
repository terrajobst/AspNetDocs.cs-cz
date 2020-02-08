---
uid: web-api/overview/security/authentication-filters
title: Filtry ověřování v ASP.NET webovém rozhraní API 2 | Microsoft Docs
author: MikeWasson
description: Filtr ověřování je komponenta, která ověřuje požadavek HTTP. Webové rozhraní API 2 a MVC 5 podporují ověřovací filtry, ale mírně se liší...
ms.author: riande
ms.date: 09/25/2014
ms.assetid: b9882e53-b3ca-4def-89b0-322846973ccb
msc.legacyurl: /web-api/overview/security/authentication-filters
msc.type: authoredcontent
ms.openlocfilehash: 2ef9e62a6c634237e920b6d7aba2127b835f959d
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075070"
---
# <a name="authentication-filters-in-aspnet-web-api-2"></a>Filtry ověřování v ASP.NET webovém rozhraní API 2

o [Jan Wasson](https://github.com/MikeWasson)

> Filtr ověřování je komponenta, která ověřuje požadavek HTTP. Webové rozhraní API 2 a MVC 5 podporují ověřovací filtry, ale mírně se liší většinou v zásadách vytváření názvů pro rozhraní filtru. Toto téma popisuje filtry ověřování webového rozhraní API.

Filtry ověřování umožňují nastavit schéma ověřování pro jednotlivé řadiče nebo akce. V takovém případě vaše aplikace může podporovat různé mechanismy ověřování pro různé prostředky HTTP.

V tomto článku se zobrazí kód ze vzorového [ověřování Basic](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication) na [https://github.com/aspnet/samples](https://github.com/aspnet/samples). Ukázka zobrazuje filtr ověřování, který implementuje schéma ověření přístupu Basic protokolu HTTP (RFC 2617). Filtr je implementován ve třídě s názvem `IdentityBasicAuthenticationAttribute`. Nezobrazuje se v ukázce celý kód, jenom části, které ukazují, jak napsat filtr ověřování.

## <a name="setting-an-authentication-filter"></a>Nastavení filtru ověřování

Podobně jako jiné filtry lze ověřovací filtry použít pro každý kontroler, pro akci nebo globálně na všechny řadiče webového rozhraní API.

Chcete-li použít filtr ověřování na kontroler, sestavte třídu kontroleru pomocí atributu Filter. Následující kód nastaví filtr `[IdentityBasicAuthentication]` pro třídu Controller, která umožňuje základní ověřování všech akcí kontroleru.

[!code-csharp[Main](authentication-filters/samples/sample1.cs)]

Chcete-li použít filtr na jednu akci, seupravte akci filtrem. Následující kód nastaví filtr `[IdentityBasicAuthentication]` v metodě `Post` kontroleru.

[!code-csharp[Main](authentication-filters/samples/sample2.cs)]

Pokud chcete filtr použít na všechny řadiče webového rozhraní API, přidejte ho do **GlobalConfiguration. filters**.

[!code-csharp[Main](authentication-filters/samples/sample3.cs)]

## <a name="implementing-a-web-api-authentication-filter"></a>Implementace filtru ověřování webového rozhraní API

Ověřovací filtry ve webovém rozhraní API implementují rozhraní [System. Web. http. filters. IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx) . Měly by také dědit z **atributu System. Attribute**, aby je bylo možné použít jako atributy.

Rozhraní **IAuthenticationFilter** má dvě metody:

- **AuthenticateAsync** ověří požadavek pomocí ověření přihlašovacích údajů v žádosti, pokud je k dispozici.
- **ChallengeAsync** v případě potřeby přidá do odpovědi HTTP výzvu ověřování.

Tyto metody odpovídají toku ověřování definovanému v [dokumentu rfc 2612](http://tools.ietf.org/html/rfc2616) a [RFC 2617](http://tools.ietf.org/html/rfc2617):

1. Klient odesílá pověření do autorizační hlavičky. K tomu obvykle dochází poté, co klient obdrží od serveru odpověď 401 (Neautorizovaná). Klient ale může odesílat přihlašovací údaje s libovolným požadavkem, a ne hned po získání 401.
2. Pokud server přihlašovací údaje nepřijme, vrátí odpověď 401 (Neautorizovaná). Odpověď obsahuje hlavičku WWW-Authenticate, která obsahuje jeden nebo více výzev. Každá výzva Určuje schéma ověřování rozpoznané serverem.

Server může také vrátit 401 z anonymního požadavku. Ve skutečnosti to obvykle způsob, jakým je proces ověřování inicializovaný:

1. Klient pošle anonymní požadavek.
2. Server vrátí 401.
3. Klienti znovu odesílají požadavek s přihlašovacími údaji.

Tento tok zahrnuje jak *ověřování* , tak *autorizační* postup.

- Ověřování prokáže identitu klienta.
- Autorizace určuje, jestli klient může získat přístup k určitému prostředku.

Ve webovém rozhraní API ověřovací filtry zpracovávají ověřování, ale ne autorizaci. Autorizace by se měla provádět pomocí autorizačního filtru nebo uvnitř akce kontroleru.

Toto je tok v kanálu webového rozhraní API 2:

1. Před vyvoláním akce vytvoří webové rozhraní API seznam ověřovacích filtrů pro tuto akci. To zahrnuje filtry s rozsahem akcí, oborem kontroléru a globálním rozsahem.
2. Webové rozhraní API volá **AuthenticateAsync** u každého filtru v seznamu. Každý filtr může v žádosti ověřit přihlašovací údaje. Pokud některý filtr úspěšně ověří přihlašovací údaje, vytvoří filtr **IPrincipal** a připojí ho k žádosti. Filtr může také v tomto okamžiku aktivovat chybu. V takovém případě se zbytek kanálu nespustí.
3. V případě, že není k dispozici žádná chyba, požadavek natéká přes zbytek kanálu.
4. Webové rozhraní API potom volá metodu **ChallengeAsync** každého filtru ověřování. Filtry používají tuto metodu k přidání výzvy k odpovědi, pokud je to potřeba. Obvykle (ale ne vždy), k nimž by došlo v reakci na chybu 401.

Následující diagramy znázorňují dva možné případy. V prvním případě filtr ověřování úspěšně ověří požadavek, autorizační filtr autorizací žádosti a akce kontroleru vrátí 200 (OK).

![](authentication-filters/_static/image1.png)

Ve druhém příkladu ověřovací filtr ověří požadavek, ale autorizační Filtr vrátí 401 (Neautorizováno). V takovém případě není vyvolána akce kontroleru. Filtr ověřování přidá hlavičku WWW-Authenticate do odpovědi.

![](authentication-filters/_static/image2.png)

K dispozici jsou další kombinace&mdash;například, pokud akce kontroleru povoluje anonymní požadavky, je možné, že máte filtr ověřování, ale nemáte autorizaci.

## <a name="implementing-the-authenticateasync-method"></a>Implementace metody AuthenticateAsync

Metoda **AuthenticateAsync** se pokusí ověřit požadavek. Tady je podpis této metody:

[!code-csharp[Main](authentication-filters/samples/sample4.cs)]

Metoda **AuthenticateAsync** musí provést jednu z následujících akcí:

1. Nic (No-OP).
2. Vytvořte **IPrincipal** a nastavte ji na žádost.
3. Nastavte výsledek chyby.

Option (1) znamená, že požadavek nemá žádné přihlašovací údaje, které tento filtr zná. Option (2) znamená, že filtr úspěšně ověřil požadavek. Možnost (3) znamená, že žádost obsahovala neplatné přihlašovací údaje (například nesprávné heslo), která aktivuje chybovou odpověď.

Tady je obecná osnova pro implementaci **AuthenticateAsync**.

1. Vyhledejte přihlašovací údaje v žádosti.
2. Pokud nejsou k dispozici žádná pověření, neprovádějte žádnou akci a vraťte (No-OP).
3. Pokud jsou k dispozici přihlašovací údaje, ale filtr nerozpozná schéma ověřování, neprovádějte nic a vraťte se (No-OP). Schéma může pochopit jiný filtr v kanálu.
4. Pokud jsou k dispozici přihlašovací údaje, které filtr zná, zkuste je ověřit.
5. Pokud jsou přihlašovací údaje chybné, vraťte 401 nastavením `context.ErrorResult`.
6. Pokud jsou přihlašovací údaje platné, vytvořte **IPrincipal** a nastavte `context.Principal`.

Následující kód ukazuje metodu **AuthenticateAsync** ze vzorového [ověřování Basic](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication) . Komentáře označují jednotlivé kroky. Kód ukazuje několik typů chyb: autorizační hlavička bez přihlašovacích údajů, poškozené přihlašovací údaje a chybné uživatelské jméno nebo heslo.

[!code-csharp[Main](authentication-filters/samples/sample5.cs)]

## <a name="setting-an-error-result"></a>Nastavení výsledku chyby

Pokud jsou přihlašovací údaje neplatné, musí filtr nastavit `context.ErrorResult` na **IHttpActionResult** , které vytvoří odpověď na chybu. Další informace o **IHttpActionResult**najdete v tématu [výsledek akce ve webovém rozhraní API 2](../getting-started-with-aspnet-web-api/action-results.md).

Ukázka základního ověřování obsahuje třídu `AuthenticationFailureResult`, která je vhodná pro tento účel.

[!code-csharp[Main](authentication-filters/samples/sample6.cs)]

## <a name="implementing-challengeasync"></a>Implementace ChallengeAsync

Účelem metody **ChallengeAsync** je v případě potřeby přidat do odpovědi výzvy ověřování. Tady je podpis této metody:

[!code-csharp[Main](authentication-filters/samples/sample7.cs)]

Metoda je volána u každého filtru ověřování v kanálu požadavků.

Je důležité pochopit, že **ChallengeAsync** se volá *před* vytvořením odpovědi HTTP a případně i před spuštěním akce kontroleru. Když se zavolá **ChallengeAsync** , `context.Result` obsahuje **IHttpActionResult**, který se později použije k vytvoření odpovědi HTTP. Takže když se zavolá **ChallengeAsync** , neznáte ještě nic o odpovědi HTTP. Metoda **ChallengeAsync** by měla nahradit původní hodnotu `context.Result` novým **IHttpActionResult**. Tento **IHttpActionResult** musí zalamovat původní `context.Result`.

![](authentication-filters/_static/image3.png)

Vyvolám původní **IHttpActionResult** *vnitřní výsledek*a nový **IHttpActionResult** *vnějšího výsledku*. Vnější výsledek musí splňovat následující:

1. Vyvolat vnitřní výsledek pro vytvoření odpovědi HTTP.
2. Projděte si odpověď.
3. V případě potřeby přidejte do odpovědi výzvu pro ověřování.

Následující příklad je pořízen ze vzorového ověřování Basic. Definuje **IHttpActionResult** pro vnější výsledek.

[!code-csharp[Main](authentication-filters/samples/sample8.cs)]

Vlastnost `InnerResult` obsahuje vnitřní **IHttpActionResult**. Vlastnost `Challenge` představuje hlavičku WWW-Authentication. Všimněte si, že **metody ExecuteAsync** nejprve volá `InnerResult.ExecuteAsync` k vytvoření odpovědi HTTP a pak v případě potřeby přidá výzvu.

Před přidáním výzvy si přečtěte kód odpovědi. Většina schémat ověřování přidávají výzvu pouze v případě, že odpověď je 401, jak je znázorněno zde. Některá schémata ověřování však přidávají výzvu k odpovědi na úspěch. Příklad najdete v tématu [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559).

Vzhledem k třídě `AddChallengeOnUnauthorizedResult` je skutečný kód v **ChallengeAsync** jednoduchý. Stačí jenom vytvořit výsledek a připojit ho k `context.Result`.

[!code-csharp[Main](authentication-filters/samples/sample9.cs)]

Poznámka: Ukázka základního ověřování abstrakce tuto logiku a tím, že ji umístí do rozšiřující metody.

## <a name="combining-authentication-filters-with-host-level-authentication"></a>Kombinování ověřovacích filtrů s ověřováním na úrovni hostitele

"Ověřování na úrovni hostitele" je ověřování prováděné hostitelem (například IIS), než požadavek dosáhne rozhraní Web API Framework.

Často můžete chtít povolit ověřování na úrovni hostitele pro zbývající část aplikace, ale zakázat ji pro vaše řadiče webového rozhraní API. Typickým scénářem je například povolit ověřování pomocí formulářů na úrovni hostitele, ale použít ověřování na základě tokenu pro webové rozhraní API.

Pokud chcete zakázat ověřování na úrovni hostitele uvnitř kanálu webového rozhraní API, zavolejte `config.SuppressHostPrincipal()` v konfiguraci. To způsobí, že webové rozhraní API odebere **IPrincipal** z jakékoli žádosti, která vstoupí do kanálu webového rozhraní API. Efektivně &quot;neověřuje&quot; žádosti.

[!code-csharp[Main](authentication-filters/samples/sample10.cs)]

## <a name="additional-resources"></a>Další prostředky

[Filtry zabezpečení webového rozhraní API ASP.NET](https://msdn.microsoft.com/magazine/dn781361.aspx) (MSDN Magazine)

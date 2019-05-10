---
uid: web-api/overview/advanced/http-cookies
title: Soubory cookie protokolu HTTP v rozhraní ASP.NET Web API – ASP.NET 4.x
author: MikeWasson
description: Popisuje, jak odesílat a přijímat soubory cookie protokolu HTTP v rozhraní Web API pro ASP.NET 4.x.
ms.author: riande
ms.date: 09/17/2012
ms.custom: seoapril2019
ms.assetid: 243db2ec-8f67-4a5e-a382-4ddcec4b4164
msc.legacyurl: /web-api/overview/advanced/http-cookies
msc.type: authoredcontent
ms.openlocfilehash: 8ca26ff6776daa13bc4f8b06c2eba61afcfefba2
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/06/2019
ms.locfileid: "65126243"
---
# <a name="http-cookies-in-aspnet-web-api"></a><span data-ttu-id="59452-103">Soubory cookie HTTP ve webovém rozhraní API technologie ASP.NET</span><span class="sxs-lookup"><span data-stu-id="59452-103">HTTP Cookies in ASP.NET Web API</span></span>

<span data-ttu-id="59452-104">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="59452-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="59452-105">Toto téma popisuje, jak odesílat a přijímat soubory cookie protokolu HTTP v rozhraní Web API.</span><span class="sxs-lookup"><span data-stu-id="59452-105">This topic describes how to send and receive HTTP cookies in Web API.</span></span>

## <a name="background-on-http-cookies"></a><span data-ttu-id="59452-106">Na pozadí na soubory cookie protokolu HTTP</span><span class="sxs-lookup"><span data-stu-id="59452-106">Background on HTTP Cookies</span></span>

<span data-ttu-id="59452-107">Tato část poskytuje stručný přehled o tom, jak jsou implementované soubory cookie na úrovni protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="59452-107">This section gives a brief overview of how cookies are implemented at the HTTP level.</span></span> <span data-ttu-id="59452-108">Podrobné informace, [RFC 6265](http://tools.ietf.org/html/rfc6265).</span><span class="sxs-lookup"><span data-stu-id="59452-108">For details, consult [RFC 6265](http://tools.ietf.org/html/rfc6265).</span></span>

<span data-ttu-id="59452-109">Soubor cookie je část dat, která odesílá na server v odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="59452-109">A cookie is a piece of data that a server sends in the HTTP response.</span></span> <span data-ttu-id="59452-110">Klient (volitelně) uloží soubor cookie a vrátí na následné žádosti.</span><span class="sxs-lookup"><span data-stu-id="59452-110">The client (optionally) stores the cookie and returns it on subsequent requests.</span></span> <span data-ttu-id="59452-111">Díky tomu klienta a serveru, sdílení stavu.</span><span class="sxs-lookup"><span data-stu-id="59452-111">This allows the client and server to share state.</span></span> <span data-ttu-id="59452-112">Nastavení souboru cookie, server obsahuje hlavičku Set-Cookie v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="59452-112">To set a cookie, the server includes a Set-Cookie header in the response.</span></span> <span data-ttu-id="59452-113">Formát souboru cookie je pár název hodnota pomocí volitelných atributů.</span><span class="sxs-lookup"><span data-stu-id="59452-113">The format of a cookie is a name-value pair, with optional attributes.</span></span> <span data-ttu-id="59452-114">Příklad:</span><span class="sxs-lookup"><span data-stu-id="59452-114">For example:</span></span>

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

<span data-ttu-id="59452-115">Tady je příklad s atributy:</span><span class="sxs-lookup"><span data-stu-id="59452-115">Here is an example with attributes:</span></span>

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

<span data-ttu-id="59452-116">Pokud chcete vrátit do souboru cookie na serveru, klienta obsahuje hlavičku souboru Cookie novějším žádostem.</span><span class="sxs-lookup"><span data-stu-id="59452-116">To return a cookie to the server, the client includes a Cookie header in later requests.</span></span>

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

<span data-ttu-id="59452-117">Odpověď HTTP může obsahovat více záhlaví Set-Cookie.</span><span class="sxs-lookup"><span data-stu-id="59452-117">An HTTP response can include multiple Set-Cookie headers.</span></span>

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

<span data-ttu-id="59452-118">Klient odešle několik souborů cookie pomocí jednoho hlavičky souboru Cookie.</span><span class="sxs-lookup"><span data-stu-id="59452-118">The client returns multiple cookies using a single Cookie header.</span></span>

[!code-console[Main](http-cookies/samples/sample5.cmd)]

<span data-ttu-id="59452-119">Rozsahu a doby trvání soubor cookie se řídí následujícími atributy v hlavičce Set-Cookie:</span><span class="sxs-lookup"><span data-stu-id="59452-119">The scope and duration of a cookie are controlled by following attributes in the Set-Cookie header:</span></span>

- <span data-ttu-id="59452-120">**Domény**: Instruuje klienta, které domény souboru cookie přijímat.</span><span class="sxs-lookup"><span data-stu-id="59452-120">**Domain**: Tells the client which domain should receive the cookie.</span></span> <span data-ttu-id="59452-121">Pokud tato doména "example.com", klient vrátí soubor cookie pro každou poddoménu example.com.</span><span class="sxs-lookup"><span data-stu-id="59452-121">For example, if the domain is "example.com", the client returns the cookie to every subdomain of example.com.</span></span> <span data-ttu-id="59452-122">Pokud není zadán, doména je zdrojový server.</span><span class="sxs-lookup"><span data-stu-id="59452-122">If not specified, the domain is the origin server.</span></span>
- <span data-ttu-id="59452-123">**Cesta**: Omezuje na zadané cestě v rámci domény souboru cookie.</span><span class="sxs-lookup"><span data-stu-id="59452-123">**Path**: Restricts the cookie to the specified path within the domain.</span></span> <span data-ttu-id="59452-124">Pokud není zadán, je použít cesty identifikátoru URI požadavku.</span><span class="sxs-lookup"><span data-stu-id="59452-124">If not specified, the path of the request URI is used.</span></span>
- <span data-ttu-id="59452-125">**Vypršení platnosti**: Nastaví datum vypršení platnosti souboru cookie.</span><span class="sxs-lookup"><span data-stu-id="59452-125">**Expires**: Sets an expiration date for the cookie.</span></span> <span data-ttu-id="59452-126">Klient odstraní soubor cookie, když jeho platnost vyprší.</span><span class="sxs-lookup"><span data-stu-id="59452-126">The client deletes the cookie when it expires.</span></span>
- <span data-ttu-id="59452-127">**Max-Age**: Nastaví maximální stáří souboru cookie.</span><span class="sxs-lookup"><span data-stu-id="59452-127">**Max-Age**: Sets the maximum age for the cookie.</span></span> <span data-ttu-id="59452-128">Klient odstraní soubor cookie, když dosáhl maximální stáří.</span><span class="sxs-lookup"><span data-stu-id="59452-128">The client deletes the cookie when it reaches the maximum age.</span></span>

<span data-ttu-id="59452-129">Pokud mají oba `Expires` a `Max-Age` jsou nastaveny, `Max-Age` přednost.</span><span class="sxs-lookup"><span data-stu-id="59452-129">If both `Expires` and `Max-Age` are set, `Max-Age` takes precedence.</span></span> <span data-ttu-id="59452-130">Pokud je nastavena ani jedno, klient odstraní soubor cookie po skončení aktuální relaci.</span><span class="sxs-lookup"><span data-stu-id="59452-130">If neither is set, the client deletes the cookie when the current session ends.</span></span> <span data-ttu-id="59452-131">(Přesné význam "relace" se určuje podle uživatelského agenta).</span><span class="sxs-lookup"><span data-stu-id="59452-131">(The exact meaning of "session" is determined by the user-agent.)</span></span>

<span data-ttu-id="59452-132">Nezapomínejte, že klienti mohou ignorovat soubory cookie.</span><span class="sxs-lookup"><span data-stu-id="59452-132">However, be aware that clients may ignore cookies.</span></span> <span data-ttu-id="59452-133">Uživatel může například zakažte soubory cookie z důvodů ochrany osobních údajů.</span><span class="sxs-lookup"><span data-stu-id="59452-133">For example, a user might disable cookies for privacy reasons.</span></span> <span data-ttu-id="59452-134">Klienti soubory cookie odstranit předtím, než vyprší jejich platnost, nebo omezit počet uložených souborů cookie.</span><span class="sxs-lookup"><span data-stu-id="59452-134">Clients may delete cookies before they expire, or limit the number of cookies stored.</span></span> <span data-ttu-id="59452-135">Z důvodu ochrany osobních údajů klientů často odmítnout "třetích stran" soubory cookie, kde doména se neshoduje s původním serveru.</span><span class="sxs-lookup"><span data-stu-id="59452-135">For privacy reasons, clients often reject "third party" cookies, where the domain does not match the origin server.</span></span> <span data-ttu-id="59452-136">Stručně řečeno server neměli spoléhat na návrat, které nastaví soubory cookie.</span><span class="sxs-lookup"><span data-stu-id="59452-136">In short, the server should not rely on getting back the cookies that it sets.</span></span>

## <a name="cookies-in-web-api"></a><span data-ttu-id="59452-137">Soubory cookie ve webovém rozhraní API</span><span class="sxs-lookup"><span data-stu-id="59452-137">Cookies in Web API</span></span>

<span data-ttu-id="59452-138">Pokud chcete přidat do souboru cookie do odpovědi HTTP, vytvořte **CookieHeaderValue** instanci, která představuje soubor cookie.</span><span class="sxs-lookup"><span data-stu-id="59452-138">To add a cookie to an HTTP response, create a **CookieHeaderValue** instance that represents the cookie.</span></span> <span data-ttu-id="59452-139">Zavolejte **AddCookies** rozšiřující metoda, která je definována v **System.Net.Http. HttpResponseHeadersExtensions** třídy, chcete-li přidat soubor cookie.</span><span class="sxs-lookup"><span data-stu-id="59452-139">Then call the **AddCookies** extension method, which is defined in the **System.Net.Http. HttpResponseHeadersExtensions** class, to add the cookie.</span></span>

<span data-ttu-id="59452-140">Například následující kód přidá soubor cookie v rámci akce kontroleru:</span><span class="sxs-lookup"><span data-stu-id="59452-140">For example, the following code adds a cookie within a controller action:</span></span>

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

<span data-ttu-id="59452-141">Všimněte si, že **AddCookies** přijímá pole **CookieHeaderValue** instancí.</span><span class="sxs-lookup"><span data-stu-id="59452-141">Notice that **AddCookies** takes an array of **CookieHeaderValue** instances.</span></span>

<span data-ttu-id="59452-142">Chcete-li extrahovat soubory cookie z požadavku klienta, zavolejte **GetCookies** metody:</span><span class="sxs-lookup"><span data-stu-id="59452-142">To extract the cookies from a client request, call the **GetCookies** method:</span></span>

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

<span data-ttu-id="59452-143">A **CookieHeaderValue** obsahuje kolekci **CookieState** instancí.</span><span class="sxs-lookup"><span data-stu-id="59452-143">A **CookieHeaderValue** contains a collection of **CookieState** instances.</span></span> <span data-ttu-id="59452-144">Každý **CookieState** představuje jeden soubor cookie.</span><span class="sxs-lookup"><span data-stu-id="59452-144">Each **CookieState** represents one cookie.</span></span> <span data-ttu-id="59452-145">Získat pomocí metody indexeru **CookieState** podle názvu, jak je znázorněno.</span><span class="sxs-lookup"><span data-stu-id="59452-145">Use the indexer method to get a **CookieState** by name, as shown.</span></span>

## <a name="structured-cookie-data"></a><span data-ttu-id="59452-146">Soubor Cookie strukturovaná Data</span><span class="sxs-lookup"><span data-stu-id="59452-146">Structured Cookie Data</span></span>

<span data-ttu-id="59452-147">Většina prohlížečů omezení počtu souborů cookie, které se budou ukládat&#8212;celkový počet i číslo na doménu.</span><span class="sxs-lookup"><span data-stu-id="59452-147">Many browsers limit how many cookies they will store&#8212;both the total number, and the number per domain.</span></span> <span data-ttu-id="59452-148">Proto může být užitečné zavést strukturovaná data do jednoho souboru cookie, namísto nastavení více souborů cookie.</span><span class="sxs-lookup"><span data-stu-id="59452-148">Therefore, it can be useful to put structured data into a single cookie, instead of setting multiple cookies.</span></span>

> [!NOTE]
> <span data-ttu-id="59452-149">RFC 6265 nedefinuje strukturu dat souboru cookie.</span><span class="sxs-lookup"><span data-stu-id="59452-149">RFC 6265 does not define the structure of cookie data.</span></span>

<span data-ttu-id="59452-150">Použití **CookieHeaderValue** třídy, můžete předat seznam dvojic název hodnota pro data souborů cookie.</span><span class="sxs-lookup"><span data-stu-id="59452-150">Using the **CookieHeaderValue** class, you can pass a list of name-value pairs for the cookie data.</span></span> <span data-ttu-id="59452-151">Tyto páry název hodnota jsou zakódovány jako data kódovaná adresou URL formuláře v hlavičce Set-Cookie:</span><span class="sxs-lookup"><span data-stu-id="59452-151">These name-value pairs are encoded as URL-encoded form data in the Set-Cookie header:</span></span>

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

<span data-ttu-id="59452-152">Předchozí kód vytvoří následující hlavičkou Set-Cookie:</span><span class="sxs-lookup"><span data-stu-id="59452-152">The previous code produces the following Set-Cookie header:</span></span>

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

<span data-ttu-id="59452-153">**CookieState** třída poskytuje metodu indexer načíst dílčí hodnoty ze souboru cookie ve zprávě požadavku:</span><span class="sxs-lookup"><span data-stu-id="59452-153">The **CookieState** class provides an indexer method to read the sub-values from a cookie in the request message:</span></span>

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a><span data-ttu-id="59452-154">Příklad: Nastavení a načtení souborů cookie v obslužné rutiny zpráv</span><span class="sxs-lookup"><span data-stu-id="59452-154">Example: Set and Retrieve Cookies in a Message Handler</span></span>

<span data-ttu-id="59452-155">Předchozí příklady nám ukázaly, jak používat soubory cookie z v rámci kontroleru webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="59452-155">The previous examples showed how to use cookies from within a Web API controller.</span></span> <span data-ttu-id="59452-156">Další možností je použít [obslužné rutiny zpráv](http-message-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="59452-156">Another option is to use [message handlers](http-message-handlers.md).</span></span> <span data-ttu-id="59452-157">Obslužné rutiny zpráv jsou vyvolány dříve v kanálu než řadiče.</span><span class="sxs-lookup"><span data-stu-id="59452-157">Message handlers are invoked earlier in the pipeline than controllers.</span></span> <span data-ttu-id="59452-158">Obslužné rutiny zpráv můžete číst soubory cookie z požadavku, než požadavek dosáhne kontroleru nebo po kontroleru generuje odpovědi přidat soubory cookie v odpovědi.</span><span class="sxs-lookup"><span data-stu-id="59452-158">A message handler can read cookies from the request before the request reaches the controller, or add cookies to the response after the controller generates the response.</span></span>

![](http-cookies/_static/image2.png)

<span data-ttu-id="59452-159">Následující kód ukazuje obslužné rutiny zpráv pro vytvoření ID relace.</span><span class="sxs-lookup"><span data-stu-id="59452-159">The following code shows a message handler for creating session IDs.</span></span> <span data-ttu-id="59452-160">ID relace se ukládají do souboru cookie.</span><span class="sxs-lookup"><span data-stu-id="59452-160">The session ID is stored in a cookie.</span></span> <span data-ttu-id="59452-161">Obslužná rutina ověří požadavek pro soubor cookie relace.</span><span class="sxs-lookup"><span data-stu-id="59452-161">The handler checks the request for the session cookie.</span></span> <span data-ttu-id="59452-162">Pokud žádost neobsahuje soubor cookie, obslužná rutina generuje ID nové relace.</span><span class="sxs-lookup"><span data-stu-id="59452-162">If the request does not include the cookie, the handler generates a new session ID.</span></span> <span data-ttu-id="59452-163">V obou případech se obslužná rutina uloží ID relace v **HttpRequestMessage.Properties** kontejner objektů a dat.</span><span class="sxs-lookup"><span data-stu-id="59452-163">In either case, the handler stores the session ID in the **HttpRequestMessage.Properties** property bag.</span></span> <span data-ttu-id="59452-164">Také přidá soubor cookie relace do odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="59452-164">It also adds the session cookie to the HTTP response.</span></span>

<span data-ttu-id="59452-165">Tato implementace nelze ověřit, že ID relace, od klienta byl ve skutečnosti vydán serverem.</span><span class="sxs-lookup"><span data-stu-id="59452-165">This implementation does not validate that the session ID from the client was actually issued by the server.</span></span> <span data-ttu-id="59452-166">Nepoužívejte ho jako formu ověřování!</span><span class="sxs-lookup"><span data-stu-id="59452-166">Don't use it as a form of authentication!</span></span> <span data-ttu-id="59452-167">Bod v příkladu je zobrazení správy souboru cookie HTTP.</span><span class="sxs-lookup"><span data-stu-id="59452-167">The point of the example is to show HTTP cookie management.</span></span>

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

<span data-ttu-id="59452-168">Kontroler můžete získat ID relace, od **HttpRequestMessage.Properties** kontejner objektů a dat.</span><span class="sxs-lookup"><span data-stu-id="59452-168">A controller can get the session ID from the **HttpRequestMessage.Properties** property bag.</span></span>

[!code-csharp[Main](http-cookies/samples/sample12.cs)]

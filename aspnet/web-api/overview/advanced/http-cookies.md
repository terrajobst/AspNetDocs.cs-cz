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
# <a name="http-cookies-in-aspnet-web-api"></a><span data-ttu-id="2cb5f-103">Soubory cookie HTTP ve webovém rozhraní API technologie ASP.NET</span><span class="sxs-lookup"><span data-stu-id="2cb5f-103">HTTP Cookies in ASP.NET Web API</span></span>

<span data-ttu-id="2cb5f-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2cb5f-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="2cb5f-105">Toto téma popisuje, jak odesílat a přijímat soubory cookie HTTP ve webovém rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-105">This topic describes how to send and receive HTTP cookies in Web API.</span></span>

## <a name="background-on-http-cookies"></a><span data-ttu-id="2cb5f-106">Pozadí na souborech cookie HTTP</span><span class="sxs-lookup"><span data-stu-id="2cb5f-106">Background on HTTP Cookies</span></span>

<span data-ttu-id="2cb5f-107">V této části najdete stručný přehled toho, jak se soubory cookie implementují na úrovni HTTP.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-107">This section gives a brief overview of how cookies are implemented at the HTTP level.</span></span> <span data-ttu-id="2cb5f-108">Další podrobnosti najdete v [dokumentu RFC 6265](http://tools.ietf.org/html/rfc6265).</span><span class="sxs-lookup"><span data-stu-id="2cb5f-108">For details, consult [RFC 6265](http://tools.ietf.org/html/rfc6265).</span></span>

<span data-ttu-id="2cb5f-109">Soubor cookie je část dat, kterou server odesílá v odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-109">A cookie is a piece of data that a server sends in the HTTP response.</span></span> <span data-ttu-id="2cb5f-110">Klient (volitelně) uloží soubor cookie a vrátí ho v dalších požadavcích.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-110">The client (optionally) stores the cookie and returns it on subsequent requests.</span></span> <span data-ttu-id="2cb5f-111">Tím umožníte, aby klient a server sdíleli stav.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-111">This allows the client and server to share state.</span></span> <span data-ttu-id="2cb5f-112">Aby bylo možné nastavit soubor cookie, bude server v odpovědi obsahovat hlavičku souborového souboru cookie.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-112">To set a cookie, the server includes a Set-Cookie header in the response.</span></span> <span data-ttu-id="2cb5f-113">Formátem souboru cookie je pár název-hodnota s nepovinnými atributy.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-113">The format of a cookie is a name-value pair, with optional attributes.</span></span> <span data-ttu-id="2cb5f-114">Příklad:</span><span class="sxs-lookup"><span data-stu-id="2cb5f-114">For example:</span></span>

[!code-powershell[Main](http-cookies/samples/sample1.ps1)]

<span data-ttu-id="2cb5f-115">Tady je příklad s atributy:</span><span class="sxs-lookup"><span data-stu-id="2cb5f-115">Here is an example with attributes:</span></span>

[!code-powershell[Main](http-cookies/samples/sample2.ps1)]

<span data-ttu-id="2cb5f-116">Pokud chcete vrátit soubor cookie na server, klient zahrne v pozdějších požadavcích hlavičku souboru cookie.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-116">To return a cookie to the server, the client includes a Cookie header in later requests.</span></span>

[!code-console[Main](http-cookies/samples/sample3.cmd)]

![](http-cookies/_static/image1.png)

<span data-ttu-id="2cb5f-117">Odpověď protokolu HTTP může zahrnovat více hlaviček souborů cookie sady.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-117">An HTTP response can include multiple Set-Cookie headers.</span></span>

[!code-powershell[Main](http-cookies/samples/sample4.ps1)]

<span data-ttu-id="2cb5f-118">Klient vrátí více souborů cookie pomocí jednoho záhlaví souboru cookie.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-118">The client returns multiple cookies using a single Cookie header.</span></span>

[!code-console[Main](http-cookies/samples/sample5.cmd)]

<span data-ttu-id="2cb5f-119">Rozsah a doba trvání souboru cookie jsou ovládány pomocí atributů v hlavičce Set-cookie:</span><span class="sxs-lookup"><span data-stu-id="2cb5f-119">The scope and duration of a cookie are controlled by following attributes in the Set-Cookie header:</span></span>

- <span data-ttu-id="2cb5f-120">**Doména**: oznamuje klientovi, která doména má přijmout soubor cookie.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-120">**Domain**: Tells the client which domain should receive the cookie.</span></span> <span data-ttu-id="2cb5f-121">Pokud je doména například "example.com", vrátí klient soubor cookie do každé subdomény example.com.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-121">For example, if the domain is "example.com", the client returns the cookie to every subdomain of example.com.</span></span> <span data-ttu-id="2cb5f-122">Pokud není zadaný, doména je původním serverem.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-122">If not specified, the domain is the origin server.</span></span>
- <span data-ttu-id="2cb5f-123">**Cesta**: omezí soubor cookie na zadanou cestu v doméně.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-123">**Path**: Restricts the cookie to the specified path within the domain.</span></span> <span data-ttu-id="2cb5f-124">Pokud není zadaný, použije se cesta k identifikátoru URI požadavku.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-124">If not specified, the path of the request URI is used.</span></span>
- <span data-ttu-id="2cb5f-125">**Expires**: nastaví datum vypršení platnosti souboru cookie.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-125">**Expires**: Sets an expiration date for the cookie.</span></span> <span data-ttu-id="2cb5f-126">Klient odstraní soubor cookie, pokud vyprší jeho platnost.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-126">The client deletes the cookie when it expires.</span></span>
- <span data-ttu-id="2cb5f-127">**Max-Age**: nastaví maximální stáří pro soubor cookie.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-127">**Max-Age**: Sets the maximum age for the cookie.</span></span> <span data-ttu-id="2cb5f-128">Klient odstraní soubor cookie, pokud dosáhne maximálního stáří.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-128">The client deletes the cookie when it reaches the maximum age.</span></span>

<span data-ttu-id="2cb5f-129">Pokud jsou nastaveny `Expires` i `Max-Age`, má `Max-Age` přednost.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-129">If both `Expires` and `Max-Age` are set, `Max-Age` takes precedence.</span></span> <span data-ttu-id="2cb5f-130">Pokud není nastavená ani jedna, klient při ukončení aktuální relace odstraní soubor cookie.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-130">If neither is set, the client deletes the cookie when the current session ends.</span></span> <span data-ttu-id="2cb5f-131">(Přesný význam "session" určuje uživatel-agent.)</span><span class="sxs-lookup"><span data-stu-id="2cb5f-131">(The exact meaning of "session" is determined by the user-agent.)</span></span>

<span data-ttu-id="2cb5f-132">Upozorňujeme však, že klienti mohou ignorovat soubory cookie.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-132">However, be aware that clients may ignore cookies.</span></span> <span data-ttu-id="2cb5f-133">Uživatel může například zakázat soubory cookie z důvodů ochrany osobních údajů.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-133">For example, a user might disable cookies for privacy reasons.</span></span> <span data-ttu-id="2cb5f-134">Klienti mohou odstranit soubory cookie před vypršením platnosti nebo omezit počet uložených souborů cookie.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-134">Clients may delete cookies before they expire, or limit the number of cookies stored.</span></span> <span data-ttu-id="2cb5f-135">Z důvodu ochrany osobních údajů klienti často odmítnou soubory cookie třetích stran, kde doména neodpovídají zdrojovému serveru.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-135">For privacy reasons, clients often reject "third party" cookies, where the domain does not match the origin server.</span></span> <span data-ttu-id="2cb5f-136">V krátkém případě by se server neměl spoléhat na vrácení souborů cookie, které nastaví.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-136">In short, the server should not rely on getting back the cookies that it sets.</span></span>

## <a name="cookies-in-web-api"></a><span data-ttu-id="2cb5f-137">Soubory cookie ve webovém rozhraní API</span><span class="sxs-lookup"><span data-stu-id="2cb5f-137">Cookies in Web API</span></span>

<span data-ttu-id="2cb5f-138">Chcete-li přidat soubor cookie do odpovědi HTTP, vytvořte instanci **CookieHeaderValue** , která představuje soubor cookie.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-138">To add a cookie to an HTTP response, create a **CookieHeaderValue** instance that represents the cookie.</span></span> <span data-ttu-id="2cb5f-139">Pak zavolejte metodu rozšíření **AddCookies** , která je definována v **System .NET. http. HttpResponseHeadersExtensions** třída pro přidání souboru cookie.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-139">Then call the **AddCookies** extension method, which is defined in the **System.Net.Http. HttpResponseHeadersExtensions** class, to add the cookie.</span></span>

<span data-ttu-id="2cb5f-140">Například následující kód přidá soubor cookie v rámci akce kontroleru:</span><span class="sxs-lookup"><span data-stu-id="2cb5f-140">For example, the following code adds a cookie within a controller action:</span></span>

[!code-csharp[Main](http-cookies/samples/sample6.cs)]

<span data-ttu-id="2cb5f-141">Všimněte si, že **AddCookies** přebírá pole instancí **CookieHeaderValue** .</span><span class="sxs-lookup"><span data-stu-id="2cb5f-141">Notice that **AddCookies** takes an array of **CookieHeaderValue** instances.</span></span>

<span data-ttu-id="2cb5f-142">Chcete-li extrahovat soubory cookie z požadavku klienta, zavolejte metodu **GetCookies** :</span><span class="sxs-lookup"><span data-stu-id="2cb5f-142">To extract the cookies from a client request, call the **GetCookies** method:</span></span>

[!code-csharp[Main](http-cookies/samples/sample7.cs)]

<span data-ttu-id="2cb5f-143">**CookieHeaderValue** obsahuje kolekci instancí **CookieState** .</span><span class="sxs-lookup"><span data-stu-id="2cb5f-143">A **CookieHeaderValue** contains a collection of **CookieState** instances.</span></span> <span data-ttu-id="2cb5f-144">Každý **CookieState** představuje jeden soubor cookie.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-144">Each **CookieState** represents one cookie.</span></span> <span data-ttu-id="2cb5f-145">Použijte metodu indexeru k získání **CookieState** podle názvu, jak je znázorněno na obrázku.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-145">Use the indexer method to get a **CookieState** by name, as shown.</span></span>

## <a name="structured-cookie-data"></a><span data-ttu-id="2cb5f-146">Strukturovaná data souborů cookie</span><span class="sxs-lookup"><span data-stu-id="2cb5f-146">Structured Cookie Data</span></span>

<span data-ttu-id="2cb5f-147">Mnoho prohlížečů omezuje počet souborů cookie, které budou&#8212;ukládat celkové číslo, a počet v každé doméně.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-147">Many browsers limit how many cookies they will store&#8212;both the total number, and the number per domain.</span></span> <span data-ttu-id="2cb5f-148">Proto může být užitečné ukládat strukturovaná data do jediného souboru cookie namísto nastavení více souborů cookie.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-148">Therefore, it can be useful to put structured data into a single cookie, instead of setting multiple cookies.</span></span>

> [!NOTE]
> <span data-ttu-id="2cb5f-149">Specifikace RFC 6265 nedefinuje strukturu dat souborů cookie.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-149">RFC 6265 does not define the structure of cookie data.</span></span>

<span data-ttu-id="2cb5f-150">Pomocí třídy **CookieHeaderValue** můžete předat seznam párů název-hodnota pro data souborů cookie.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-150">Using the **CookieHeaderValue** class, you can pass a list of name-value pairs for the cookie data.</span></span> <span data-ttu-id="2cb5f-151">Tyto páry název-hodnota se kódují jako data formuláře kódovaná v adresách URL v hlavičce Set-cookie:</span><span class="sxs-lookup"><span data-stu-id="2cb5f-151">These name-value pairs are encoded as URL-encoded form data in the Set-Cookie header:</span></span>

[!code-csharp[Main](http-cookies/samples/sample8.cs)]

<span data-ttu-id="2cb5f-152">Předchozí kód vytvoří následující hlavičku souboru cookie sady:</span><span class="sxs-lookup"><span data-stu-id="2cb5f-152">The previous code produces the following Set-Cookie header:</span></span>

[!code-powershell[Main](http-cookies/samples/sample9.ps1)]

<span data-ttu-id="2cb5f-153">Třída **CookieState** poskytuje indexerovou metodu pro čtení dílčích hodnot ze souboru cookie ve zprávě požadavku:</span><span class="sxs-lookup"><span data-stu-id="2cb5f-153">The **CookieState** class provides an indexer method to read the sub-values from a cookie in the request message:</span></span>

[!code-csharp[Main](http-cookies/samples/sample10.cs)]

## <a name="example-set-and-retrieve-cookies-in-a-message-handler"></a><span data-ttu-id="2cb5f-154">Příklad: nastavení a načtení souborů cookie v obslužné rutině zprávy</span><span class="sxs-lookup"><span data-stu-id="2cb5f-154">Example: Set and Retrieve Cookies in a Message Handler</span></span>

<span data-ttu-id="2cb5f-155">Předchozí příklady ukázaly, jak používat soubory cookie v rámci kontroleru webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-155">The previous examples showed how to use cookies from within a Web API controller.</span></span> <span data-ttu-id="2cb5f-156">Další možností je použít [obslužné rutiny zpráv](http-message-handlers.md).</span><span class="sxs-lookup"><span data-stu-id="2cb5f-156">Another option is to use [message handlers](http-message-handlers.md).</span></span> <span data-ttu-id="2cb5f-157">Obslužné rutiny zpráv jsou vyvolány dříve v kanálu než řadiče.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-157">Message handlers are invoked earlier in the pipeline than controllers.</span></span> <span data-ttu-id="2cb5f-158">Obslužná rutina zprávy může číst soubory cookie z požadavku předtím, než požadavek dosáhne kontroleru, nebo přidat soubory cookie do odpovědi poté, co kontroler odpověď vygeneruje.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-158">A message handler can read cookies from the request before the request reaches the controller, or add cookies to the response after the controller generates the response.</span></span>

![](http-cookies/_static/image2.png)

<span data-ttu-id="2cb5f-159">Následující kód ukazuje popisovač zprávy pro vytváření ID relací.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-159">The following code shows a message handler for creating session IDs.</span></span> <span data-ttu-id="2cb5f-160">ID relace je uloženo v souboru cookie.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-160">The session ID is stored in a cookie.</span></span> <span data-ttu-id="2cb5f-161">Obslužná rutina zkontroluje požadavek na soubor cookie relace.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-161">The handler checks the request for the session cookie.</span></span> <span data-ttu-id="2cb5f-162">Pokud žádost nezahrnuje soubor cookie, obslužná rutina generuje nové ID relace.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-162">If the request does not include the cookie, the handler generates a new session ID.</span></span> <span data-ttu-id="2cb5f-163">V obou případech obslužná rutina ukládá ID relace do kontejneru vlastností **zprávy HttpRequestMessage. Properties** .</span><span class="sxs-lookup"><span data-stu-id="2cb5f-163">In either case, the handler stores the session ID in the **HttpRequestMessage.Properties** property bag.</span></span> <span data-ttu-id="2cb5f-164">Také přidá soubor cookie relace do odpovědi HTTP.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-164">It also adds the session cookie to the HTTP response.</span></span>

<span data-ttu-id="2cb5f-165">Tato implementace neověřuje, zda je ID relace z klienta skutečně vydaným serverem.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-165">This implementation does not validate that the session ID from the client was actually issued by the server.</span></span> <span data-ttu-id="2cb5f-166">Nepoužívejte ji jako způsob ověřování.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-166">Don't use it as a form of authentication!</span></span> <span data-ttu-id="2cb5f-167">Bodem příkladu je zobrazení správy souborů cookie protokolu HTTP.</span><span class="sxs-lookup"><span data-stu-id="2cb5f-167">The point of the example is to show HTTP cookie management.</span></span>

[!code-csharp[Main](http-cookies/samples/sample11.cs)]

<span data-ttu-id="2cb5f-168">Kontroler může získat ID relace z kontejneru vlastností **zprávy HttpRequestMessage. Properties** .</span><span class="sxs-lookup"><span data-stu-id="2cb5f-168">A controller can get the session ID from the **HttpRequestMessage.Properties** property bag.</span></span>

[!code-csharp[Main](http-cookies/samples/sample12.cs)]

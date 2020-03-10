---
uid: web-api/overview/security/basic-authentication
title: Základní ověřování ve webovém rozhraní API ASP.NET | Microsoft Docs
author: MikeWasson
description: Popisuje použití základního ověřování ve webovém rozhraní API ASP.NET.
ms.author: riande
ms.date: 10/02/2014
ms.assetid: 41423767-0021-47c3-9e53-0021b457c39f
msc.legacyurl: /web-api/overview/security/basic-authentication
msc.type: authoredcontent
ms.openlocfilehash: 1470bd4b5abd5199b9a5105973b053812d643351
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555725"
---
# <a name="basic-authentication-in-aspnet-web-api"></a><span data-ttu-id="ad693-103">Základní ověřování ve webovém rozhraní API ASP.NET</span><span class="sxs-lookup"><span data-stu-id="ad693-103">Basic Authentication in ASP.NET Web API</span></span>

<span data-ttu-id="ad693-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ad693-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="ad693-105">Základní ověřování je definované v [dokumentu RFC 2617, ověřování protokolem http: základní a ověřování přístupu přes algoritmus Digest](http://www.ietf.org/rfc/rfc2617.txt).</span><span class="sxs-lookup"><span data-stu-id="ad693-105">Basic authentication is defined in [RFC 2617, HTTP Authentication: Basic and Digest Access Authentication](http://www.ietf.org/rfc/rfc2617.txt).</span></span>

<span data-ttu-id="ad693-106">Nevýhody</span><span class="sxs-lookup"><span data-stu-id="ad693-106">Disadvantages</span></span>

- <span data-ttu-id="ad693-107">Přihlašovací údaje uživatele se odesílají v žádosti.</span><span class="sxs-lookup"><span data-stu-id="ad693-107">User credentials are sent in the request.</span></span>
- <span data-ttu-id="ad693-108">Přihlašovací údaje se odesílají jako prostý text.</span><span class="sxs-lookup"><span data-stu-id="ad693-108">Credentials are sent as plaintext.</span></span>
- <span data-ttu-id="ad693-109">Přihlašovací údaje se odesílají u všech požadavků.</span><span class="sxs-lookup"><span data-stu-id="ad693-109">Credentials are sent with every request.</span></span>
- <span data-ttu-id="ad693-110">Neexistuje způsob, jak se odhlásit, s výjimkou ukončení relace prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="ad693-110">No way to log out, except by ending the browser session.</span></span>
- <span data-ttu-id="ad693-111">Zranitelné proti padělání žádostí mezi weby (CSRF); vyžaduje míry anti-CSRF.</span><span class="sxs-lookup"><span data-stu-id="ad693-111">Vulnerable to cross-site request forgery (CSRF); requires anti-CSRF measures.</span></span>

<span data-ttu-id="ad693-112">Výhody</span><span class="sxs-lookup"><span data-stu-id="ad693-112">Advantages</span></span>

- <span data-ttu-id="ad693-113">Internet Standard.</span><span class="sxs-lookup"><span data-stu-id="ad693-113">Internet standard.</span></span>
- <span data-ttu-id="ad693-114">Podporováno všemi hlavními prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="ad693-114">Supported by all major browsers.</span></span>
- <span data-ttu-id="ad693-115">Poměrně jednoduchý protokol.</span><span class="sxs-lookup"><span data-stu-id="ad693-115">Relatively simple protocol.</span></span>

<span data-ttu-id="ad693-116">Základní ověřování funguje takto:</span><span class="sxs-lookup"><span data-stu-id="ad693-116">Basic authentication works as follows:</span></span>

1. <span data-ttu-id="ad693-117">Pokud požadavek vyžaduje ověření, server vrátí 401 (Neautorizováno).</span><span class="sxs-lookup"><span data-stu-id="ad693-117">If a request requires authentication, the server returns 401 (Unauthorized).</span></span> <span data-ttu-id="ad693-118">Odpověď obsahuje hlavičku WWW-Authenticate, která značí, že server podporuje základní ověřování.</span><span class="sxs-lookup"><span data-stu-id="ad693-118">The response includes a WWW-Authenticate header, indicating the server supports Basic authentication.</span></span>
2. <span data-ttu-id="ad693-119">Klient pošle další požadavek s přihlašovacími údaji klienta v autorizační hlavičce.</span><span class="sxs-lookup"><span data-stu-id="ad693-119">The client sends another request, with the client credentials in the Authorization header.</span></span> <span data-ttu-id="ad693-120">Přihlašovací údaje jsou formátovány jako řetězec "název: heslo", kódovaný v kódování Base64.</span><span class="sxs-lookup"><span data-stu-id="ad693-120">The credentials are formatted as the string "name:password", base64-encoded.</span></span> <span data-ttu-id="ad693-121">Pověření nejsou šifrována.</span><span class="sxs-lookup"><span data-stu-id="ad693-121">The credentials are not encrypted.</span></span>

<span data-ttu-id="ad693-122">Základní ověřování se provádí v rámci kontextu "sféra".</span><span class="sxs-lookup"><span data-stu-id="ad693-122">Basic authentication is performed within the context of a "realm."</span></span> <span data-ttu-id="ad693-123">Server obsahuje název sféry v hlavičce WWW-Authenticate.</span><span class="sxs-lookup"><span data-stu-id="ad693-123">The server includes the name of the realm in the WWW-Authenticate header.</span></span> <span data-ttu-id="ad693-124">Přihlašovací údaje uživatele jsou platné v rámci této sféry.</span><span class="sxs-lookup"><span data-stu-id="ad693-124">The user's credentials are valid within that realm.</span></span> <span data-ttu-id="ad693-125">Přesný rozsah sféry je definován serverem.</span><span class="sxs-lookup"><span data-stu-id="ad693-125">The exact scope of a realm is defined by the server.</span></span> <span data-ttu-id="ad693-126">Například můžete definovat několik sfér, aby bylo možné rozdělit prostředky na oddíly.</span><span class="sxs-lookup"><span data-stu-id="ad693-126">For example, you might define several realms in order to partition resources.</span></span>

![](basic-authentication/_static/image1.png)

<span data-ttu-id="ad693-127">Protože se přihlašovací údaje odesílají bez šifrování, základní ověřování se zabezpečuje jenom přes HTTPS.</span><span class="sxs-lookup"><span data-stu-id="ad693-127">Because the credentials are sent unencrypted, Basic authentication is only secure over HTTPS.</span></span> <span data-ttu-id="ad693-128">Viz [práce s protokolem SSL ve webovém rozhraní API](working-with-ssl-in-web-api.md).</span><span class="sxs-lookup"><span data-stu-id="ad693-128">See [Working with SSL in Web API](working-with-ssl-in-web-api.md).</span></span>

<span data-ttu-id="ad693-129">Základní ověřování je také zranitelné vůči útokům CSRF.</span><span class="sxs-lookup"><span data-stu-id="ad693-129">Basic authentication is also vulnerable to CSRF attacks.</span></span> <span data-ttu-id="ad693-130">Jakmile uživatel zadá přihlašovací údaje, prohlížeč je po dobu trvání relace automaticky pošle na následující požadavky do stejné domény.</span><span class="sxs-lookup"><span data-stu-id="ad693-130">After the user enters credentials, the browser automatically sends them on subsequent requests to the same domain, for the duration of the session.</span></span> <span data-ttu-id="ad693-131">To zahrnuje požadavky AJAX.</span><span class="sxs-lookup"><span data-stu-id="ad693-131">This includes AJAX requests.</span></span> <span data-ttu-id="ad693-132">Přečtěte si téma [prevence útoků proti falšování (CSRF) žádostí mezi weby](preventing-cross-site-request-forgery-csrf-attacks.md).</span><span class="sxs-lookup"><span data-stu-id="ad693-132">See [Preventing Cross-Site Request Forgery (CSRF) Attacks](preventing-cross-site-request-forgery-csrf-attacks.md).</span></span>

## <a name="basic-authentication-with-iis"></a><span data-ttu-id="ad693-133">Základní ověřování pomocí služby IIS</span><span class="sxs-lookup"><span data-stu-id="ad693-133">Basic Authentication with IIS</span></span>

<span data-ttu-id="ad693-134">Služba IIS podporuje základní ověřování, ale existuje upozornění: uživatel je ověřený proti svým pověřením systému Windows.</span><span class="sxs-lookup"><span data-stu-id="ad693-134">IIS supports Basic authentication, but there is a caveat: The user is authenticated against their Windows credentials.</span></span> <span data-ttu-id="ad693-135">To znamená, že uživatel musí mít účet v doméně serveru.</span><span class="sxs-lookup"><span data-stu-id="ad693-135">That means the user must have an account on the server's domain.</span></span> <span data-ttu-id="ad693-136">Pro veřejný web se obvykle chcete ověřit u poskytovatele členství ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="ad693-136">For a public-facing web site, you typically want to authenticate against an ASP.NET membership provider.</span></span>

<span data-ttu-id="ad693-137">Pokud chcete povolit základní ověřování pomocí služby IIS, nastavte režim ověřování na Windows v souboru Web. config vašeho projektu ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="ad693-137">To enable Basic authentication using IIS, set the authentication mode to "Windows" in the Web.config of your ASP.NET project:</span></span>

[!code-xml[Main](basic-authentication/samples/sample1.xml)]

<span data-ttu-id="ad693-138">V tomto režimu služba IIS používá k ověření přihlašovací údaje systému Windows.</span><span class="sxs-lookup"><span data-stu-id="ad693-138">In this mode, IIS uses Windows credentials to authenticate.</span></span> <span data-ttu-id="ad693-139">Kromě toho musíte ve službě IIS povolit základní ověřování.</span><span class="sxs-lookup"><span data-stu-id="ad693-139">In addition, you must enable Basic authentication in IIS.</span></span> <span data-ttu-id="ad693-140">Ve Správci služby IIS, v zobrazení funkce, vyberte ověřování a povolit základní ověřování.</span><span class="sxs-lookup"><span data-stu-id="ad693-140">In IIS Manager, go to Features View, select Authentication, and enable Basic authentication.</span></span>

![](basic-authentication/_static/image2.png)

<span data-ttu-id="ad693-141">V projektu webového rozhraní API přidejte atribut `[Authorize]` pro všechny akce kontroleru, které vyžadují ověření.</span><span class="sxs-lookup"><span data-stu-id="ad693-141">In your Web API project, add the `[Authorize]` attribute for any controller actions that need authentication.</span></span>

<span data-ttu-id="ad693-142">Klient se sám ověřuje nastavením autorizační hlavičky v žádosti.</span><span class="sxs-lookup"><span data-stu-id="ad693-142">A client authenticates itself by setting the Authorization header in the request.</span></span> <span data-ttu-id="ad693-143">Klienti prohlížeče tento krok provádějí automaticky.</span><span class="sxs-lookup"><span data-stu-id="ad693-143">Browser clients perform this step automatically.</span></span> <span data-ttu-id="ad693-144">Neprohlížečové klienty budou muset nastavit hlavičku.</span><span class="sxs-lookup"><span data-stu-id="ad693-144">Nonbrowser clients will need to set the header.</span></span>

## <a name="basic-authentication-with-custom-membership"></a><span data-ttu-id="ad693-145">Základní ověřování s vlastním členstvím</span><span class="sxs-lookup"><span data-stu-id="ad693-145">Basic Authentication with Custom Membership</span></span>

<span data-ttu-id="ad693-146">Jak bylo zmíněno, základní ověřování integrované do služby IIS používá pověření systému Windows.</span><span class="sxs-lookup"><span data-stu-id="ad693-146">As mentioned, the Basic Authentication built into IIS uses Windows credentials.</span></span> <span data-ttu-id="ad693-147">To znamená, že potřebujete vytvořit účty pro uživatele na hostitelském serveru.</span><span class="sxs-lookup"><span data-stu-id="ad693-147">That means you need to create accounts for your users on the hosting server.</span></span> <span data-ttu-id="ad693-148">Pro internetovou aplikaci se ale uživatelské účty většinou ukládají do externí databáze.</span><span class="sxs-lookup"><span data-stu-id="ad693-148">But for an internet application, user accounts are typically stored in an external database.</span></span>

<span data-ttu-id="ad693-149">Následující kód ukazuje modul HTTP, který provádí základní ověřování.</span><span class="sxs-lookup"><span data-stu-id="ad693-149">The following code how an HTTP module that performs Basic Authentication.</span></span> <span data-ttu-id="ad693-150">Poskytovatele členství v ASP.NET můžete snadno připojit nahrazením metody `CheckPassword`, která je v tomto příkladu fiktivní metodou.</span><span class="sxs-lookup"><span data-stu-id="ad693-150">You can easily plug in an ASP.NET membership provider by replacing the `CheckPassword` method, which is a dummy method in this example.</span></span>

<span data-ttu-id="ad693-151">Ve webovém rozhraní API 2 byste měli zvážit zápis [ověřovacího filtru](authentication-filters.md) nebo [middlewaru OWIN](../../../aspnet/overview/owin-and-katana/index.md)místo modulu HTTP.</span><span class="sxs-lookup"><span data-stu-id="ad693-151">In Web API 2, you should consider writing an [authentication filter](authentication-filters.md) or [OWIN middleware](../../../aspnet/overview/owin-and-katana/index.md), instead of an HTTP module.</span></span>

[!code-csharp[Main](basic-authentication/samples/sample2.cs)]

<span data-ttu-id="ad693-152">Chcete-li povolit modul HTTP, přidejte následující do souboru Web. config v části **System. webServer Server** :</span><span class="sxs-lookup"><span data-stu-id="ad693-152">To enable the HTTP module, add the following to your web.config file in the **system.webServer** section:</span></span>

[!code-xml[Main](basic-authentication/samples/sample3.xml?highlight=4)]

<span data-ttu-id="ad693-153">Nahraďte "YourAssemblyName" názvem sestavení (včetně přípony "dll").</span><span class="sxs-lookup"><span data-stu-id="ad693-153">Replace "YourAssemblyName" with the name of the assembly (not including the "dll" extension).</span></span>

<span data-ttu-id="ad693-154">Měli byste zakázat jiná schémata ověřování, jako jsou formuláře nebo ověřování systému Windows.</span><span class="sxs-lookup"><span data-stu-id="ad693-154">You should disable other authentication schemes, such as Forms or Windows auth.</span></span>

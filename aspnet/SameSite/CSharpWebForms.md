---
title: Ukázka souboru cookie SameSite pro webforma ASP.NET 4.7.2 C#
author: blowdart
description: Ukázka souboru cookie SameSite pro webforma ASP.NET 4.7.2 C#
ms.author: riande
ms.date: 2/15/2019
uid: samesite/CSharpWebForms
ms.openlocfilehash: 50d4745eca5954275abaa59dab726e7cf7ea193f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526115"
---
# <a name="samesite-cookie-sample-for-aspnet-472-c-webforms"></a><span data-ttu-id="a7bad-103">Ukázka souboru cookie SameSite pro webforma ASP.NET 4.7.2 C#</span><span class="sxs-lookup"><span data-stu-id="a7bad-103">SameSite cookie sample for ASP.NET 4.7.2 C# WebForms</span></span>

<span data-ttu-id="a7bad-104">.NET Framework 4,7 obsahuje integrovanou podporu pro atribut [SameSite](https://www.owasp.org/index.php/SameSite) , ale dodržuje původní standard.</span><span class="sxs-lookup"><span data-stu-id="a7bad-104">.NET Framework 4.7 has built-in support for the [SameSite](https://www.owasp.org/index.php/SameSite) attribute, but it adheres to the original standard.</span></span>
<span data-ttu-id="a7bad-105">Oprava chování změnila význam `SameSite.None` pro vygenerování atributu s hodnotou `None`, namísto toho, aby vůbec generoval hodnotu.</span><span class="sxs-lookup"><span data-stu-id="a7bad-105">The patched behavior changed the meaning of `SameSite.None` to emit the attribute with a value of `None`, rather than not emit the value at all.</span></span> <span data-ttu-id="a7bad-106">Pokud nechcete hodnotu vygenerovat, můžete nastavit vlastnost `SameSite` na soubor cookie na hodnotu-1.</span><span class="sxs-lookup"><span data-stu-id="a7bad-106">If you want to not emit the value you can set the `SameSite` property on a cookie to -1.</span></span>

## <a name="sampleCode"></a><span data-ttu-id="a7bad-107">Zápis atributu SameSite</span><span class="sxs-lookup"><span data-stu-id="a7bad-107">Writing the SameSite attribute</span></span>

<span data-ttu-id="a7bad-108">Následuje příklad, jak napsat atribut SameSite v souboru cookie;</span><span class="sxs-lookup"><span data-stu-id="a7bad-108">Following is an example of how to write a SameSite attribute on a cookie;</span></span>

```c#
// Create the cookie
HttpCookie sameSiteCookie = new HttpCookie("SameSiteSample");

// Set a value for the cookie
sameSiteCookie.Value = "sample";

// Set the secure flag, which Chrome's changes will require for SameSite none.
// Note this will also require you to be running on HTTPS
sameSiteCookie.Secure = true;

// Set the cookie to HTTP only which is good practice unless you really do need
// to access it client side in scripts.
sameSiteCookie.HttpOnly = true;

// Add the SameSite attribute, this will emit the attribute with a value of none.
// To not emit the attribute at all set the SameSite property to -1.
sameSiteCookie.SameSite = SameSiteMode.None;

// Add the cookie to the response cookie collection
Response.Cookies.Add(sameSiteCookie);
```

[!INCLUDE[](~/includes/MTcomments.md)]

<span data-ttu-id="a7bad-109">Výchozí atribut sameSite pro soubor cookie pro ověřování pomocí formulářů je nastavený v parametru `cookieSameSite` nastavení ověřování pomocí formulářů v `web.config`</span><span class="sxs-lookup"><span data-stu-id="a7bad-109">The default sameSite attribute for a forms authentication cookie is set in the `cookieSameSite` parameter of the forms authentication settings in `web.config`</span></span> 

```xml
<system.web>
  <authentication mode="Forms">
    <forms name=".ASPXAUTH" loginUrl="~/" cookieSameSite="None" requireSSL="true">
    </forms>
  </authentication>
</system.web>
```

<span data-ttu-id="a7bad-110">Výchozí atribut sameSite pro stav relace je také nastaven v parametru cookieSameSite nastavení relace v `web.config`</span><span class="sxs-lookup"><span data-stu-id="a7bad-110">The default sameSite attribute for session state is also set in the 'cookieSameSite' parameter of the session settings in `web.config`</span></span>

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

<span data-ttu-id="a7bad-111">Aktualizace z listopadu 2019 na rozhraní .NET změnila výchozí nastavení pro ověřování a relaci formulářů, aby bylo možné `lax`, jak je to nejvíce kompatibilní, ale pokud vložíte stránky na prvky IFrame, může být nutné toto nastavení vrátit na hodnotu žádné a potom přidat níže uvedený kód [zachycení](#interception) , abyste upravili chování `none` v závislosti na schopnosti prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="a7bad-111">The November 2019 update to .NET changed the default settings for Forms Authentication and Session to `lax` as is the most compatible setting, however if you embed pages into iframes you may need to revert this setting to None, and then add the [interception](#interception) code shown below to adjust the `none` behavior depending on browser capability.</span></span>

### <a name="running-the-sample"></a><span data-ttu-id="a7bad-112">Spuštění ukázky</span><span class="sxs-lookup"><span data-stu-id="a7bad-112">Running the sample</span></span>

<span data-ttu-id="a7bad-113">Pokud spustíte ukázkový projekt načíst ladicí program prohlížeče na úvodní stránce a použít ho k zobrazení kolekce souborů cookie pro daný web.</span><span class="sxs-lookup"><span data-stu-id="a7bad-113">If you run the sample project  load your browser debugger on the initial page and use it to view the cookie collection for the site.</span></span>
<span data-ttu-id="a7bad-114">Provedete to tak, že kliknete na tlačítko `F12` vyberte kartu `Application` a kliknete na adresu URL webu pod možností `Cookies` v části `Storage`.</span><span class="sxs-lookup"><span data-stu-id="a7bad-114">To do so in Edge and Chrome press `F12` then select the `Application` tab and click the site URL under the `Cookies` option in the `Storage` section.</span></span>

![Seznam souborů cookie ladicího programu prohlížeče](sample/img/BrowserDebugger.png)

<span data-ttu-id="a7bad-116">Můžete vidět z obrázku, který soubor cookie vytvořil v ukázce, když kliknete na tlačítko "vytvořit soubory cookie", která má hodnotu atributu SameSite `Lax`, která odpovídá hodnotě nastavené v [ukázkovém kódu](#sampleCode).</span><span class="sxs-lookup"><span data-stu-id="a7bad-116">You can see from the image above that the cookie created by the sample when you click the "Create Cookies" button has a SameSite attribute value of `Lax`, matching the value set in the [sample code](#sampleCode).</span></span>

## <a name="interception"></a><span data-ttu-id="a7bad-117">Zachycení souborů cookie, které neovládáte</span><span class="sxs-lookup"><span data-stu-id="a7bad-117">Intercepting cookies you do not control</span></span>

<span data-ttu-id="a7bad-118">.NET 4.5.2 představilo novou událost pro zachycení zápisu hlaviček `Response.AddOnSendingHeaders`.</span><span class="sxs-lookup"><span data-stu-id="a7bad-118">.NET 4.5.2 introduced a new event for intercepting the writing of headers, `Response.AddOnSendingHeaders`.</span></span> <span data-ttu-id="a7bad-119">Tato možnost slouží k zachycení souborů cookie před jejich vrácením do klientského počítače.</span><span class="sxs-lookup"><span data-stu-id="a7bad-119">This can be used to intercept cookies before they are returned to the client machine.</span></span> <span data-ttu-id="a7bad-120">V ukázce jsme událost nastavili na statickou metodu, která kontroluje, jestli prohlížeč podporuje nové sameSite změny, a pokud ne, změní soubory cookie, aby negenerovaly atribut, pokud je nastavená nová hodnota `None`.</span><span class="sxs-lookup"><span data-stu-id="a7bad-120">In the sample we wire up the event to a static method which checks whether the browser supports the new sameSite changes, and if not, changes the cookies to not emit the attribute if the new `None` value has been set.</span></span>

<span data-ttu-id="a7bad-121">Příklad zapojování události a [SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/SameSiteCookieRewriter.cs) pro příklad zpracování události a přizpůsobení atributu `sameSite` souborů cookie naleznete v souboru [Global. asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/Global.asax.cs) .</span><span class="sxs-lookup"><span data-stu-id="a7bad-121">See [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/Global.asax.cs) for an example of hooking up the event and [SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/SameSiteCookieRewriter.cs) for an example of handling the event and adjusting the cookie `sameSite` attribute.</span></span>

```c#
public static void FilterSameSiteNoneForIncompatibleUserAgents(object sender)
{
    HttpApplication application = sender as HttpApplication;
    if (application != null)
    {
        var userAgent = application.Context.Request.UserAgent;
        if (SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent))
        {
            HttpContext.Current.Response.AddOnSendingHeaders(context =>
            {
                var cookies = context.Response.Cookies;
                for (var i = 0; i < cookies.Count; i++)
                {
                    var cookie = cookies[i];
                    if (cookie.SameSite == SameSiteMode.None)
                    {
                        cookie.SameSite = (SameSiteMode)(-1); // Unspecified
                    }
                }
            });
        }
    }
}
```

<span data-ttu-id="a7bad-122">Konkrétní pojmenované chování souborů cookie můžete změnit téměř stejným způsobem. Následující ukázka upraví výchozí soubor cookie ověřování z `Lax` na `None` v prohlížečích, které podporují `None` hodnotu, nebo odstraní atribut sameSite v prohlížečích, které nepodporují `None`.</span><span class="sxs-lookup"><span data-stu-id="a7bad-122">You can change specific named cookie behavior in much the same way; the sample below adjust the default authentication cookie from `Lax` to `None` on browsers which support the `None` value, or removes the sameSite attribute on browsers which do not support `None`.</span></span>

```c#
public static void AdjustSpecificCookieSettings()
{
    HttpContext.Current.Response.AddOnSendingHeaders(context =>
    {
        var cookies = context.Response.Cookies;
        for (var i = 0; i < cookies.Count; i++)
        {
            var cookie = cookies[i]; 
            // Forms auth: ".ASPXAUTH"
            // Session: "ASP.NET_SessionId"
            if (string.Equals(".ASPXAUTH", cookie.Name, StringComparison.Ordinal))
            { 
                if (SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent))
                {
                    cookie.SameSite = -1;
                }
                else
                {
                    cookie.SameSite = SameSiteMode.None;
                }
                cookie.Secure = true;
            }
        }
    });
}
```

## <a name="more-information"></a><span data-ttu-id="a7bad-123">Další informace</span><span class="sxs-lookup"><span data-stu-id="a7bad-123">More Information</span></span>

[<span data-ttu-id="a7bad-124">Aktualizace pro Chrome</span><span class="sxs-lookup"><span data-stu-id="a7bad-124">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)

[<span data-ttu-id="a7bad-125">Dokumentace k ASP.NET</span><span class="sxs-lookup"><span data-stu-id="a7bad-125">ASP.NET Documentation</span></span>](/aspnet/samesite/system-web-samesite)

[<span data-ttu-id="a7bad-126">Opravy .NET SameSite</span><span class="sxs-lookup"><span data-stu-id="a7bad-126">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)
---
title: Ukázka souboru cookie SameSite pro ASP.NET 4.7.2 VB MVC
author: blowdart
description: Ukázka souboru cookie SameSite pro ASP.NET 4.7.2 VB MVC
ms.author: riande
ms.date: 2/15/2019
uid: samesite/vbMVC
ms.openlocfilehash: f6effce6075f94fb58ce10ec08bf010fab8b4b56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547808"
---
# <a name="samesite-cookie-sample-for-aspnet-472-vb-mvc"></a><span data-ttu-id="415cb-103">Ukázka souboru cookie SameSite pro ASP.NET 4.7.2 VB MVC</span><span class="sxs-lookup"><span data-stu-id="415cb-103">SameSite cookie sample for ASP.NET 4.7.2 VB MVC</span></span>

<span data-ttu-id="415cb-104">.NET Framework 4,7 obsahuje integrovanou podporu pro atribut [SameSite](https://www.owasp.org/index.php/SameSite) , ale dodržuje původní standard.</span><span class="sxs-lookup"><span data-stu-id="415cb-104">.NET Framework 4.7 has built-in support for the [SameSite](https://www.owasp.org/index.php/SameSite) attribute, but it adheres to the original standard.</span></span>
<span data-ttu-id="415cb-105">Oprava chování změnila význam `SameSite.None` pro vygenerování atributu s hodnotou `None`, namísto toho, aby vůbec generoval hodnotu.</span><span class="sxs-lookup"><span data-stu-id="415cb-105">The patched behavior changed the meaning of `SameSite.None` to emit the attribute with a value of `None`, rather than not emit the value at all.</span></span> <span data-ttu-id="415cb-106">Pokud nechcete hodnotu vygenerovat, můžete nastavit vlastnost `SameSite` na soubor cookie na hodnotu-1.</span><span class="sxs-lookup"><span data-stu-id="415cb-106">If you want to not emit the value you can set the `SameSite` property on a cookie to -1.</span></span>

## <a name="sampleCode"></a><span data-ttu-id="415cb-107">Zápis atributu SameSite</span><span class="sxs-lookup"><span data-stu-id="415cb-107">Writing the SameSite attribute</span></span>

<span data-ttu-id="415cb-108">Následuje příklad, jak napsat atribut SameSite v souboru cookie;</span><span class="sxs-lookup"><span data-stu-id="415cb-108">Following is an example of how to write a SameSite attribute on a cookie;</span></span>

```vb
' Create the cookie
Dim sameSiteCookie As New HttpCookie("sameSiteSample")

' Set a value for the cookie
sameSiteCookie.Value = "sample"

' Set the secure flag, which Chrome's changes will require for SameSite none.
' Note this will also require you to be running on HTTPS
sameSiteCookie.Secure = True

' Set the cookie to HTTP only which is good practice unless you really do need
' to access it client side in scripts.
sameSiteCookie.HttpOnly = True

' Expire the cookie in 1 minute
sameSiteCookie.Expires = Date.Now.AddMinutes(1)

' Add the SameSite attribute, this will emit the attribute with a value of none.
' To Not emit the attribute at all set the SameSite property to -1.
sameSiteCookie.SameSite = SameSiteMode.None

' Add the cookie to the response cookie collection
Response.Cookies.Add(sameSiteCookie)
```

[!INCLUDE[](~/includes/MTcomments.md)]

<span data-ttu-id="415cb-109">Výchozí atribut sameSite pro stav relace je nastaven v parametru cookieSameSite nastavení relace v `web.config`</span><span class="sxs-lookup"><span data-stu-id="415cb-109">The default sameSite attribute for session state is set in the 'cookieSameSite' parameter of the session settings in `web.config`</span></span>

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

## <a name="mvc-authentication"></a><span data-ttu-id="415cb-110">Ověřování MVC</span><span class="sxs-lookup"><span data-stu-id="415cb-110">MVC Authentication</span></span>

<span data-ttu-id="415cb-111">Ověřování na základě souborů cookie OWIN MVC používá správce souborů cookie k povolení změny atributů souborů cookie.</span><span class="sxs-lookup"><span data-stu-id="415cb-111">OWIN MVC cookie based authentication uses a cookie manager to enable the changing of cookie attributes.</span></span> <span data-ttu-id="415cb-112">[SameSiteCookieManager. vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieManager.vb) je implementace takové třídy, kterou můžete kopírovat do vlastních projektů.</span><span class="sxs-lookup"><span data-stu-id="415cb-112">The [SameSiteCookieManager.vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieManager.vb) is an implementation of such a class which you can copy into your own projects.</span></span> 

<span data-ttu-id="415cb-113">Je nutné zajistit, aby byly komponenty Microsoft. Owin upgradovány na verzi 4.1.0 nebo vyšší.</span><span class="sxs-lookup"><span data-stu-id="415cb-113">You must ensure your Microsoft.Owin components are all upgraded to version 4.1.0 or greater.</span></span> <span data-ttu-id="415cb-114">Zkontrolujte soubor `packages.config`, abyste zajistili, že všechna čísla verzí budou shodná. například.</span><span class="sxs-lookup"><span data-stu-id="415cb-114">Check your `packages.config` file to ensure all the version numbers match, for example.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <!-- other packages -->
  <package id="Microsoft.Owin.Host.SystemWeb" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Owin.Security" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Owin.Security.Cookies" version="4.1.0" targetFramework="net472" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net472" />
  <package id="Owin" version="1.0" targetFramework="net472" />
</packages>
```

<span data-ttu-id="415cb-115">Komponenty ověřování musí být nakonfigurovány tak, aby používaly CookieManager ve vaší třídě Startup;</span><span class="sxs-lookup"><span data-stu-id="415cb-115">The authentication components must be configured to use the CookieManager in your startup class;</span></span>

```vb
Public Sub Configuration(app As IAppBuilder)
    app.UseCookieAuthentication(New CookieAuthenticationOptions() With {
        .CookieSameSite = SameSiteMode.None,
        .CookieHttpOnly = True,
        .CookieSecure = CookieSecureOption.Always,
        .CookieManager = New SameSiteCookieManager(New SystemWebCookieManager())
    })
End Sub
```

<span data-ttu-id="415cb-116">Správce souborů cookie musí být nastaven na *každé* součásti, která ho podporuje, včetně CookieAuthentication a OpenIdConnectAuthentication.</span><span class="sxs-lookup"><span data-stu-id="415cb-116">A cookie manager must be set on *each* component that supports it, this includes CookieAuthentication and OpenIdConnectAuthentication.</span></span>

<span data-ttu-id="415cb-117">SystemWebCookieManager se používá k tomu, aby se předešlo [známým problémům](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues) s integrací souborů cookie odpovědí.</span><span class="sxs-lookup"><span data-stu-id="415cb-117">The SystemWebCookieManager is used to avoid [known issues](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues) with response cookie integration.</span></span>

### <a name="running-the-sample"></a><span data-ttu-id="415cb-118">Spuštění ukázky</span><span class="sxs-lookup"><span data-stu-id="415cb-118">Running the sample</span></span>

<span data-ttu-id="415cb-119">Pokud spustíte ukázkový projekt, načtěte prosím na úvodní stránce ladicí program prohlížeče a použijte ho k zobrazení kolekce souborů cookie pro daný web.</span><span class="sxs-lookup"><span data-stu-id="415cb-119">If you run the sample project please load your browser debugger on the initial page and use it to view the cookie collection for the site.</span></span>
<span data-ttu-id="415cb-120">Provedete to tak, že kliknete na tlačítko `F12` vyberte kartu `Application` a kliknete na adresu URL webu pod možností `Cookies` v části `Storage`.</span><span class="sxs-lookup"><span data-stu-id="415cb-120">To do so in Edge and Chrome press `F12` then select the `Application` tab and click the site URL under the `Cookies` option in the `Storage` section.</span></span>

![Seznam souborů cookie ladicího programu prohlížeče](sample/img/BrowserDebugger.png)

<span data-ttu-id="415cb-122">Můžete vidět z obrázku, který je vytvořen souborem cookie vytvořeným v ukázce po kliknutí na tlačítko vytvořit soubor cookie SameSite má hodnotu atributu SameSite `Lax`, která odpovídá hodnotě nastavené v [ukázkovém kódu](#sampleCode).</span><span class="sxs-lookup"><span data-stu-id="415cb-122">You can see from the image above that the cookie created by the sample when you click the "Create SameSite Cookie" button has a SameSite attribute value of `Lax`, matching the value set in the [sample code](#sampleCode).</span></span>

## <a name="interception"></a><span data-ttu-id="415cb-123">Zachycení souborů cookie, které neovládáte</span><span class="sxs-lookup"><span data-stu-id="415cb-123">Intercepting cookies you do not control</span></span>

<span data-ttu-id="415cb-124">.NET 4.5.2 představilo novou událost pro zachycení zápisu hlaviček `Response.AddOnSendingHeaders`.</span><span class="sxs-lookup"><span data-stu-id="415cb-124">.NET 4.5.2 introduced a new event for intercepting the writing of headers, `Response.AddOnSendingHeaders`.</span></span> <span data-ttu-id="415cb-125">Tato možnost slouží k zachycení souborů cookie před jejich vrácením do klientského počítače.</span><span class="sxs-lookup"><span data-stu-id="415cb-125">This can be used to intercept cookies before they are returned to the client machine.</span></span> <span data-ttu-id="415cb-126">V ukázce jsme událost nastavili na statickou metodu, která kontroluje, jestli prohlížeč podporuje nové sameSite změny, a pokud ne, změní soubory cookie, aby negenerovaly atribut, pokud je nastavená nová hodnota `None`.</span><span class="sxs-lookup"><span data-stu-id="415cb-126">In the sample we wire up the event to a static method which checks whether the browser supports the new sameSite changes, and if not, changes the cookies to not emit the attribute if the new `None` value has been set.</span></span>

<span data-ttu-id="415cb-127">Příklad zapojení události a [SameSiteCookieRewriter. vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieRewriter.vb) pro příklad zpracování události a nastavení souboru cookie `sameSite`, který můžete zkopírovat do vlastního kódu, naleznete v souboru [Global. asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/Global.asax.vb) .</span><span class="sxs-lookup"><span data-stu-id="415cb-127">See [global.asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/Global.asax.vb) for an example of hooking up the event and [SameSiteCookieRewriter.vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieRewriter.vb) for an example of handling the event and adjusting the cookie `sameSite` attribute which you can copy into your own code.</span></span>

```vb
Sub FilterSameSiteNoneForIncompatibleUserAgents(ByVal sender As Object)
    Dim application As HttpApplication = TryCast(sender, HttpApplication)

    If application IsNot Nothing Then
        Dim userAgent = application.Context.Request.UserAgent

        If SameSite.DisallowsSameSiteNone(userAgent) Then
            application.Response.AddOnSendingHeaders(
                Function(context)
                    Dim cookies = context.Response.Cookies

                    For i = 0 To cookies.Count - 1
                        Dim cookie = cookies(i)

                        If cookie.SameSite = SameSiteMode.None Then
                            cookie.SameSite = CType((-1), SameSiteMode)
                        End If
                    Next
                End Function)
        End If
    End If
End Sub
```

<span data-ttu-id="415cb-128">Konkrétní pojmenované chování souborů cookie můžete změnit téměř stejným způsobem. Následující ukázka upraví výchozí soubor cookie ověřování z `Lax` na `None` v prohlížečích, které podporují `None` hodnotu, nebo odstraní atribut sameSite v prohlížečích, které nepodporují `None`.</span><span class="sxs-lookup"><span data-stu-id="415cb-128">You can change specific named cookie behavior in much the same way; the sample below adjust the default authentication cookie from `Lax` to `None` on browsers which support the `None` value, or removes the sameSite attribute on browsers which do not support `None`.</span></span>

```vb
Public Shared Sub AdjustSpecificCookieSettings()
    HttpContext.Current.Response.AddOnSendingHeaders(Function(context)
            Dim cookies = context.Response.Cookies

            For i = 0 To cookies.Count - 1
            Dim cookie = cookies(i)

            If String.Equals(".ASPXAUTH", cookie.Name, StringComparison.Ordinal) Then

                If SameSite.BrowserDetection.DisallowsSameSiteNone(userAgent) Then
                    cookie.SameSite = -1
                Else
                    cookie.SameSite = SameSiteMode.None
                End If

                cookie.Secure = True
            End If
            Next
        End Function)
End Sub
```

## <a name="more-information"></a><span data-ttu-id="415cb-129">Další informace</span><span class="sxs-lookup"><span data-stu-id="415cb-129">More Information</span></span>
 
[<span data-ttu-id="415cb-130">Aktualizace pro Chrome</span><span class="sxs-lookup"><span data-stu-id="415cb-130">Chrome Updates</span></span>](https://www.chromium.org/updates/same-site)

[<span data-ttu-id="415cb-131">Dokumentace k SameSite pro OWIN</span><span class="sxs-lookup"><span data-stu-id="415cb-131">OWIN SameSite Documentation</span></span>](/aspnet/samesite/owin-samesite)

[<span data-ttu-id="415cb-132">Dokumentace k ASP.NET</span><span class="sxs-lookup"><span data-stu-id="415cb-132">ASP.NET Documentation</span></span>](/aspnet/samesite/system-web-samesite)

[<span data-ttu-id="415cb-133">Opravy .NET SameSite</span><span class="sxs-lookup"><span data-stu-id="415cb-133">.NET SameSite Patches</span></span>](/aspnet/samesite/kbs-samesite)
---
title: Ukázka souboru cookie SameSite pro ASP.NET 4.7.2 VB MVC
author: blowdart
description: Ukázka souboru cookie SameSite pro ASP.NET 4.7.2 VB MVC
ms.author: riande
ms.date: 2/15/2019
uid: samesite/vbMVC
ms.openlocfilehash: f6effce6075f94fb58ce10ec08bf010fab8b4b56
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458467"
---
# <a name="samesite-cookie-sample-for-aspnet-472-vb-mvc"></a>Ukázka souboru cookie SameSite pro ASP.NET 4.7.2 VB MVC

.NET Framework 4,7 obsahuje integrovanou podporu pro atribut [SameSite](https://www.owasp.org/index.php/SameSite) , ale dodržuje původní standard.
Oprava chování změnila význam `SameSite.None` pro vygenerování atributu s hodnotou `None`, namísto toho, aby vůbec generoval hodnotu. Pokud nechcete hodnotu vygenerovat, můžete nastavit vlastnost `SameSite` na soubor cookie na hodnotu-1.

## <a name="sampleCode"></a>Zápis atributu SameSite

Následuje příklad, jak napsat atribut SameSite v souboru cookie;

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

Výchozí atribut sameSite pro stav relace je nastaven v parametru cookieSameSite nastavení relace v `web.config`

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

## <a name="mvc-authentication"></a>Ověřování MVC

Ověřování na základě souborů cookie OWIN MVC používá správce souborů cookie k povolení změny atributů souborů cookie. [SameSiteCookieManager. vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieManager.vb) je implementace takové třídy, kterou můžete kopírovat do vlastních projektů. 

Je nutné zajistit, aby byly komponenty Microsoft. Owin upgradovány na verzi 4.1.0 nebo vyšší. Zkontrolujte soubor `packages.config`, abyste zajistili, že všechna čísla verzí budou shodná. například.

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

Komponenty ověřování musí být nakonfigurovány tak, aby používaly CookieManager ve vaší třídě Startup;

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

Správce souborů cookie musí být nastaven na *každé* součásti, která ho podporuje, včetně CookieAuthentication a OpenIdConnectAuthentication.

SystemWebCookieManager se používá k tomu, aby se předešlo [známým problémům](https://github.com/aspnet/AspNetKatana/wiki/System.Web-response-cookie-integration-issues) s integrací souborů cookie odpovědí.

### <a name="running-the-sample"></a>Spuštění ukázky

Pokud spustíte ukázkový projekt, načtěte prosím na úvodní stránce ladicí program prohlížeče a použijte ho k zobrazení kolekce souborů cookie pro daný web.
Provedete to tak, že kliknete na tlačítko `F12` vyberte kartu `Application` a kliknete na adresu URL webu pod možností `Cookies` v části `Storage`.

![Seznam souborů cookie ladicího programu prohlížeče](sample/img/BrowserDebugger.png)

Můžete vidět z obrázku, který je vytvořen souborem cookie vytvořeným v ukázce po kliknutí na tlačítko vytvořit soubor cookie SameSite má hodnotu atributu SameSite `Lax`, která odpovídá hodnotě nastavené v [ukázkovém kódu](#sampleCode).

## <a name="interception"></a>Zachycení souborů cookie, které neovládáte

.NET 4.5.2 představilo novou událost pro zachycení zápisu hlaviček `Response.AddOnSendingHeaders`. Tato možnost slouží k zachycení souborů cookie před jejich vrácením do klientského počítače. V ukázce jsme událost nastavili na statickou metodu, která kontroluje, jestli prohlížeč podporuje nové sameSite změny, a pokud ne, změní soubory cookie, aby negenerovaly atribut, pokud je nastavená nová hodnota `None`.

Příklad zapojení události a [SameSiteCookieRewriter. vb](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/SameSiteCookieRewriter.vb) pro příklad zpracování události a nastavení souboru cookie `sameSite`, který můžete zkopírovat do vlastního kódu, naleznete v souboru [Global. asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicMVC5/Global.asax.vb) .

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

Konkrétní pojmenované chování souborů cookie můžete změnit téměř stejným způsobem. Následující ukázka upraví výchozí soubor cookie ověřování z `Lax` na `None` v prohlížečích, které podporují `None` hodnotu, nebo odstraní atribut sameSite v prohlížečích, které nepodporují `None`.

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

## <a name="more-information"></a>Další informace
 
[Aktualizace pro Chrome](https://www.chromium.org/updates/same-site)

[Dokumentace k SameSite pro OWIN](/aspnet/samesite/owin-samesite)

[Dokumentace k ASP.NET](/aspnet/samesite/system-web-samesite)

[Opravy .NET SameSite](/aspnet/samesite/kbs-samesite)
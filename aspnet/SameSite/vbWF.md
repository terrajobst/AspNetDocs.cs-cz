---
title: Ukázka souboru cookie SameSite pro webformes ASP.NET 4.7.2 VB
author: blowdart
description: Ukázka souboru cookie SameSite pro webformes ASP.NET 4.7.2 VB
ms.author: riande
ms.date: 2/15/2019
uid: samesite/vbWF
ms.openlocfilehash: 8979edecc5acf7dac81b9f53d31af00389f4727c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544994"
---
# <a name="samesite-cookie-sample-for-aspnet-472-vb-webforms"></a>Ukázka souboru cookie SameSite pro webformes ASP.NET 4.7.2 VB
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

Výchozí atribut sameSite pro soubor cookie pro ověřování pomocí formulářů je nastavený v parametru `cookieSameSite` nastavení ověřování pomocí formulářů v `web.config` 

```xml
<system.web>
  <authentication mode="Forms">
    <forms name=".ASPXAUTH" loginUrl="~/" cookieSameSite="None" requireSSL="true">
    </forms>
  </authentication>
</system.web>
```

Výchozí atribut sameSite pro stav relace je také nastaven v parametru cookieSameSite nastavení relace v `web.config`

```xml
<system.web>
  <sessionState cookieSameSite="None">     
  </sessionState>
</system.web>
```

Aktualizace z listopadu 2019 na rozhraní .NET změnila výchozí nastavení pro ověřování a relaci formulářů, aby bylo možné `lax`, jak je to nejvíce kompatibilní, ale pokud vložíte stránky na prvky IFrame, může být nutné toto nastavení vrátit na hodnotu žádné a potom přidat níže uvedený kód [zachycení](#interception) , abyste upravili chování `none` v závislosti na schopnosti prohlížeče.

### <a name="running-the-sample"></a>Spuštění ukázky

Pokud spustíte ukázkový projekt načíst ladicí program prohlížeče na úvodní stránce a použít ho k zobrazení kolekce souborů cookie pro daný web.
Provedete to tak, že kliknete na tlačítko `F12` vyberte kartu `Application` a kliknete na adresu URL webu pod možností `Cookies` v části `Storage`.

![Seznam souborů cookie ladicího programu prohlížeče](sample/img/BrowserDebugger.png)

Můžete vidět z obrázku, který soubor cookie vytvořil v ukázce, když kliknete na tlačítko "vytvořit soubory cookie", která má hodnotu atributu SameSite `Lax`, která odpovídá hodnotě nastavené v [ukázkovém kódu](#sampleCode).

## <a name="interception"></a>Zachycení souborů cookie, které neovládáte

.NET 4.5.2 představilo novou událost pro zachycení zápisu hlaviček `Response.AddOnSendingHeaders`. Tato možnost slouží k zachycení souborů cookie před jejich vrácením do klientského počítače. V ukázce jsme událost nastavili na statickou metodu, která kontroluje, jestli prohlížeč podporuje nové sameSite změny, a pokud ne, změní soubory cookie, aby negenerovaly atribut, pokud je nastavená nová hodnota `None`.

Příklad zapojování události a [SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/SameSiteCookieRewriter.vb) pro příklad zpracování události a přizpůsobení atributu `sameSite` souborů cookie naleznete v souboru [Global. asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472VisualBasicWebForms/Global.asax.vb) .


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

[Dokumentace k ASP.NET](/aspnet/samesite/system-web-samesite)

[Opravy .NET SameSite](/aspnet/samesite/kbs-samesite)
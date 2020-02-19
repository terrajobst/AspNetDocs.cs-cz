---
title: Ukázka souboru cookie SameSite pro webforma ASP.NET 4.7.2 C#
author: blowdart
description: Ukázka souboru cookie SameSite pro webforma ASP.NET 4.7.2 C#
ms.author: riande
ms.date: 2/15/2019
uid: samesite/CSharpWebForms
ms.openlocfilehash: 50d4745eca5954275abaa59dab726e7cf7ea193f
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458481"
---
# <a name="samesite-cookie-sample-for-aspnet-472-c-webforms"></a>Ukázka souboru cookie SameSite pro webforma ASP.NET 4.7.2 C#

.NET Framework 4,7 obsahuje integrovanou podporu pro atribut [SameSite](https://www.owasp.org/index.php/SameSite) , ale dodržuje původní standard.
Oprava chování změnila význam `SameSite.None` pro vygenerování atributu s hodnotou `None`, namísto toho, aby vůbec generoval hodnotu. Pokud nechcete hodnotu vygenerovat, můžete nastavit vlastnost `SameSite` na soubor cookie na hodnotu-1.

## <a name="sampleCode"></a>Zápis atributu SameSite

Následuje příklad, jak napsat atribut SameSite v souboru cookie;

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

Příklad zapojování události a [SameSiteCookieRewriter.cs](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/SameSiteCookieRewriter.cs) pro příklad zpracování události a přizpůsobení atributu `sameSite` souborů cookie naleznete v souboru [Global. asax](https://github.com/blowdart/AspNetSameSiteSamples/blob/master/AspNet472CSharpWebForms/Global.asax.cs) .

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

Konkrétní pojmenované chování souborů cookie můžete změnit téměř stejným způsobem. Následující ukázka upraví výchozí soubor cookie ověřování z `Lax` na `None` v prohlížečích, které podporují `None` hodnotu, nebo odstraní atribut sameSite v prohlížečích, které nepodporují `None`.

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

## <a name="more-information"></a>Další informace

[Aktualizace pro Chrome](https://www.chromium.org/updates/same-site)

[Dokumentace k ASP.NET](/aspnet/samesite/system-web-samesite)

[Opravy .NET SameSite](/aspnet/samesite/kbs-samesite)
---
uid: web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
title: Prevence útoků na ASP.NET (CSRF) žádostí mezi weby v MVC
author: MikeWasson
description: Popisuje útok proti padělání požadavků (CSRF) mezi weby a postup implementace antiCSRF měr v ASP.NET Web MVC.
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 81d46f14-8f48-4d8c-830d-cc8d594dc11b
msc.legacyurl: /web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks
msc.type: authoredcontent
ms.openlocfilehash: 5fb0f8bcc9e587ba4fbbf2b857d3bf7adcaafb94
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555116"
---
# <a name="preventing-cross-site-request-forgery-csrf-attacks-in-aspnet-mvc-application"></a>Prevence útoků prostřednictvím CSRF (site-to Request) v aplikaci ASP.NET MVC

o [Jan Wasson](https://github.com/MikeWasson)

Padělání žádostí mezi weby (CSRF) je útok, kdy škodlivý web pošle požadavek na ohrožený web, ve kterém je aktuálně přihlášený uživatel.

Tady je příklad útoku CSRF:

1. Uživatel se do `www.example.com` přihlašuje pomocí ověřování pomocí formulářů.
2. Server ověřuje uživatele. Odpověď ze serveru obsahuje soubor cookie ověřování.
3. Uživatel navštíví škodlivý web, aniž by se odhlásil. Tento škodlivý web obsahuje následující formulář HTML: 

    [!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample1.html)]

    Všimněte si, že akce formuláře provede příspěvky na ohrožený web, nikoli na škodlivý web. Toto je součást CSRF (pro různé lokality).
4. Uživatel klikne na tlačítko Odeslat. Prohlížeč zahrnuje ověřovací soubor cookie s požadavkem.
5. Požadavek běží na serveru s kontextem ověřování uživatele a může provádět cokoli, co může ověřený uživatel dělat.

I když tento příklad vyžaduje, aby uživatel mohl kliknout na tlačítko formulář, škodlivá stránka může stejně snadno spustit skript, který odešle formulář automaticky. Použití protokolu SSL navíc nebrání útoku CSRF, protože škodlivý web může odeslat žádost "https://".

Obvykle jsou útoky CSRF na weby, které používají soubory cookie pro ověřování, protože prohlížeče odesílají všechny relevantní soubory cookie do cílového webu. Nicméně útoky CSRF nejsou omezené na zneužití souborů cookie. Například základní ověřování a ověřování algoritmem Digest je také zranitelné. Když se uživatel přihlásí pomocí základního ověřování nebo ověřování hodnotou hash. prohlížeč automaticky pošle přihlašovací údaje až do ukončení relace.

## <a name="anti-forgery-tokens"></a>Tokeny proti padělání

Aby se zabránilo útokům CSRF, používá ASP.NET MVC tokeny proti padělání, označované také jako *ověřovací tokeny žádostí*.

1. Klient požaduje stránku HTML, která obsahuje formulář.
2. Server obsahuje dvě tokeny v odpovědi. Jeden token se pošle jako soubor cookie. Druhý je umístěn ve skrytém poli formuláře. Tokeny jsou vygenerované náhodně, aby nežádoucí osoba nemohly odhadnout hodnoty.
3. Když klient formulář odešle, musí odeslat oba tokeny zpátky na server. Klient odešle token souborů cookie jako soubor cookie a odešle token formuláře do dat formuláře. (Klient prohlížeče to automaticky provede, když uživatel formulář odešle.)
4. Pokud požadavek nezahrnuje obě tokeny, server žádost nepovoluje.

Tady je příklad formuláře HTML s tokenem skrytého formuláře:

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample2.html)]

Tokeny ochrany proti padělání fungují, protože škodlivá stránka nemůže číst tokeny uživatele z důvodu zásad stejného původu. ([Zásady se stejným zdrojem](http://www.w3.org/Security/wiki/Same_Origin_Policy) brání tomu, aby se dokumenty hostované na dvou různých webech lišily k obsahu. Takže v předchozím příkladu může škodlivá stránka odesílat požadavky do example.com, ale nemůže přečíst odpověď.)

Aby nedocházelo k útokům CSRF, používejte k jakýmkoli ověřovacím protokolům tokeny proti padělání, kde prohlížeč po přihlášení uživatele tiše odesílá přihlašovací údaje. To zahrnuje protokoly ověřování založené na souborech cookie, jako je ověřování pomocí formulářů, a také protokoly, jako je základní ověřování a ověřování algoritmem Digest.

Pro jakékoli nebezpečné metody (POST, PUT, DELETE) byste měli vyžadovat tokeny pro ochranu proti padělání. Také se ujistěte, že bezpečné metody (GET, HEAD) nemají žádné vedlejší účinky. Kromě toho platí, že pokud povolíte podporu mezi doménami, jako je CORS nebo JSONP, pak i bezpečné metody, jako je GET, jsou potenciálně zranitelné vůči útokům CSRF, což útočníkovi umožňuje číst potenciálně citlivá data.

## <a name="anti-forgery-tokens-in-aspnet-mvc"></a>Tokeny pro ochranu proti padělání ve ASP.NET MVC

Chcete-li přidat tokeny pro ochranu proti padělání na stránku Razor, použijte pomocnou metodu **HtmlHelper. AntiForgeryToken** :

[!code-cshtml[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample3.cshtml)]

Tato metoda přidá skryté pole formuláře a také nastaví token souboru cookie.

## <a name="anti-csrf-and-ajax"></a>Anti-CSRF a AJAX

Token formuláře může být problémem pro požadavky AJAX, protože požadavek AJAX může odesílat data JSON, nikoli data formuláře HTML. Jedním z řešení je odeslat tokeny ve vlastní hlavičce protokolu HTTP. Následující kód používá syntaxe Razor k vygenerování tokenů a následně přidá tokeny do požadavku AJAX. Tokeny se generují na serveru voláním metody **Antipadělání. Gettokens**.

[!code-html[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample4.html)]

Při zpracování žádosti extrahujte tokeny z hlavičky žádosti. Pak zavoláním metody **. Validate** ověřte tokeny. Metoda **Validate** vyvolá výjimku, pokud tokeny nejsou platné.

[!code-csharp[Main](preventing-cross-site-request-forgery-csrf-attacks/samples/sample5.cs)]

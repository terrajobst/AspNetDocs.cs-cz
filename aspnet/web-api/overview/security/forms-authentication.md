---
uid: web-api/overview/security/forms-authentication
title: Ověřování formulářů ve webovém rozhraní API ASP.NET | Microsoft Docs
author: MikeWasson
description: Popisuje použití ověřování pomocí formulářů ve webovém rozhraní API ASP.NET.
ms.author: riande
ms.date: 12/12/2012
ms.assetid: 9f06c1f2-ffaa-4831-94a0-2e4a3befdf07
msc.legacyurl: /web-api/overview/security/forms-authentication
msc.type: authoredcontent
ms.openlocfilehash: 147bfab76e48497f35a72b28cd935f40ec4193bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598593"
---
# <a name="forms-authentication-in-aspnet-web-api"></a>Ověřování formulářů ve webovém rozhraní API ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

Ověřování pomocí formulářů k odeslání přihlašovacích údajů uživatele na server používá formulář HTML. Nejedná se o internetový standard. Ověřování pomocí formulářů je vhodné jenom pro webová rozhraní API, která se volají z webové aplikace, aby uživatel mohl pracovat s formulářem HTML.

| Výhody | Nevýhody |
| --- | --- |
| -Snadná implementace: je integrovaná do ASP.NET. – Používá poskytovatele členství ASP.NET, který usnadňuje správu uživatelských účtů. | – Nejedná se o standardní mechanismus ověřování HTTP; místo standardní autorizační hlavičky používá soubory cookie protokolu HTTP. – Vyžaduje prohlížeč klienta. -Přihlašovací údaje se odesílají jako prostý text. – Zranitelná proti padělání žádostí mezi lokalitami (CSRF); vyžaduje míry anti-CSRF. – Nepoužívejte je obtížné z neprohlížečových klientů. Přihlášení vyžaduje prohlížeč. – V žádosti se odešlou přihlašovací údaje uživatele. – Někteří uživatelé zakazují soubory cookie. |

Stručně funguje ověřování formulářů v ASP.NET takto:

1. Klient požaduje prostředek, který vyžaduje ověření.
2. Pokud uživatel není ověřený, server vrátí HTTP 302 (nalezeno) a přesměruje na přihlašovací stránku.
3. Uživatel zadá přihlašovací údaje a odešle formulář.
4. Server vrátí jiný HTTP 302, který přesměrovává zpátky na původní identifikátor URI. Tato odpověď zahrnuje ověřovací soubor cookie.
5. Klient požaduje prostředek znovu. Požadavek zahrnuje ověřovací soubor cookie, takže server udělí požadavek.

![](forms-authentication/_static/image1.png)

Další informace najdete v tématu [Přehled ověřování typu Forms.](../../../web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs.md)

## <a name="using-forms-authentication-with-web-api"></a>Použití ověřování pomocí formulářů s webovým rozhraním API

Chcete-li vytvořit aplikaci, která používá ověřování pomocí formulářů, vyberte šablonu "Internetová aplikace" v Průvodci projektu MVC 4. Tato šablona vytvoří řadiče MVC pro správu účtů. Můžete také použít šablonu "samostatná aplikace", která je k dispozici ve ASP.NET Update na 2012.

V řadičích webového rozhraní API můžete omezit přístup pomocí atributu `[Authorize]`, jak je popsáno v tématu [použití atributu [autorizovat]](authentication-and-authorization-in-aspnet-web-api.md#auth3).

Formuláře – ověřování používá k ověření požadavků soubor cookie relace. Prohlížeče automaticky odesílají všechny relevantní soubory cookie do cílového webu. Tato funkce usnadňuje ověřování prostřednictvím formulářů (CSRF) proti útokům přes více lokalit, které se [zabraňují útokům prostřednictvím CSRF (pro falšování požadavků mezi lokalitami)](preventing-cross-site-request-forgery-csrf-attacks.md).

Ověřování prostřednictvím formulářů nešifruje přihlašovací údaje uživatele. Proto ověřování pomocí formulářů není zabezpečené, pokud se nepoužívá s protokolem SSL. Viz [práce s protokolem SSL ve webovém rozhraní API](working-with-ssl-in-web-api.md).

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
# <a name="basic-authentication-in-aspnet-web-api"></a>Základní ověřování ve webovém rozhraní API ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

Základní ověřování je definované v [dokumentu RFC 2617, ověřování protokolem http: základní a ověřování přístupu přes algoritmus Digest](http://www.ietf.org/rfc/rfc2617.txt).

Nevýhody

- Přihlašovací údaje uživatele se odesílají v žádosti.
- Přihlašovací údaje se odesílají jako prostý text.
- Přihlašovací údaje se odesílají u všech požadavků.
- Neexistuje způsob, jak se odhlásit, s výjimkou ukončení relace prohlížeče.
- Zranitelné proti padělání žádostí mezi weby (CSRF); vyžaduje míry anti-CSRF.

Výhody

- Internet Standard.
- Podporováno všemi hlavními prohlížeči.
- Poměrně jednoduchý protokol.

Základní ověřování funguje takto:

1. Pokud požadavek vyžaduje ověření, server vrátí 401 (Neautorizováno). Odpověď obsahuje hlavičku WWW-Authenticate, která značí, že server podporuje základní ověřování.
2. Klient pošle další požadavek s přihlašovacími údaji klienta v autorizační hlavičce. Přihlašovací údaje jsou formátovány jako řetězec "název: heslo", kódovaný v kódování Base64. Pověření nejsou šifrována.

Základní ověřování se provádí v rámci kontextu "sféra". Server obsahuje název sféry v hlavičce WWW-Authenticate. Přihlašovací údaje uživatele jsou platné v rámci této sféry. Přesný rozsah sféry je definován serverem. Například můžete definovat několik sfér, aby bylo možné rozdělit prostředky na oddíly.

![](basic-authentication/_static/image1.png)

Protože se přihlašovací údaje odesílají bez šifrování, základní ověřování se zabezpečuje jenom přes HTTPS. Viz [práce s protokolem SSL ve webovém rozhraní API](working-with-ssl-in-web-api.md).

Základní ověřování je také zranitelné vůči útokům CSRF. Jakmile uživatel zadá přihlašovací údaje, prohlížeč je po dobu trvání relace automaticky pošle na následující požadavky do stejné domény. To zahrnuje požadavky AJAX. Přečtěte si téma [prevence útoků proti falšování (CSRF) žádostí mezi weby](preventing-cross-site-request-forgery-csrf-attacks.md).

## <a name="basic-authentication-with-iis"></a>Základní ověřování pomocí služby IIS

Služba IIS podporuje základní ověřování, ale existuje upozornění: uživatel je ověřený proti svým pověřením systému Windows. To znamená, že uživatel musí mít účet v doméně serveru. Pro veřejný web se obvykle chcete ověřit u poskytovatele členství ASP.NET.

Pokud chcete povolit základní ověřování pomocí služby IIS, nastavte režim ověřování na Windows v souboru Web. config vašeho projektu ASP.NET:

[!code-xml[Main](basic-authentication/samples/sample1.xml)]

V tomto režimu služba IIS používá k ověření přihlašovací údaje systému Windows. Kromě toho musíte ve službě IIS povolit základní ověřování. Ve Správci služby IIS, v zobrazení funkce, vyberte ověřování a povolit základní ověřování.

![](basic-authentication/_static/image2.png)

V projektu webového rozhraní API přidejte atribut `[Authorize]` pro všechny akce kontroleru, které vyžadují ověření.

Klient se sám ověřuje nastavením autorizační hlavičky v žádosti. Klienti prohlížeče tento krok provádějí automaticky. Neprohlížečové klienty budou muset nastavit hlavičku.

## <a name="basic-authentication-with-custom-membership"></a>Základní ověřování s vlastním členstvím

Jak bylo zmíněno, základní ověřování integrované do služby IIS používá pověření systému Windows. To znamená, že potřebujete vytvořit účty pro uživatele na hostitelském serveru. Pro internetovou aplikaci se ale uživatelské účty většinou ukládají do externí databáze.

Následující kód ukazuje modul HTTP, který provádí základní ověřování. Poskytovatele členství v ASP.NET můžete snadno připojit nahrazením metody `CheckPassword`, která je v tomto příkladu fiktivní metodou.

Ve webovém rozhraní API 2 byste měli zvážit zápis [ověřovacího filtru](authentication-filters.md) nebo [middlewaru OWIN](../../../aspnet/overview/owin-and-katana/index.md)místo modulu HTTP.

[!code-csharp[Main](basic-authentication/samples/sample2.cs)]

Chcete-li povolit modul HTTP, přidejte následující do souboru Web. config v části **System. webServer Server** :

[!code-xml[Main](basic-authentication/samples/sample3.xml?highlight=4)]

Nahraďte "YourAssemblyName" názvem sestavení (včetně přípony "dll").

Měli byste zakázat jiná schémata ověřování, jako jsou formuláře nebo ověřování systému Windows.

---
uid: web-api/overview/security/integrated-windows-authentication
title: Integrované ověřování systému Windows | Microsoft Docs
author: MikeWasson
description: Popisuje použití integrovaného ověřování systému Windows ve webovém rozhraní API ASP.NET.
ms.author: riande
ms.date: 12/18/2012
ms.assetid: 71ee4c78-c500-4d1c-b761-b4e161a291b5
msc.legacyurl: /web-api/overview/security/integrated-windows-authentication
msc.type: authoredcontent
ms.openlocfilehash: e4f31f191f3c0fabff308ea5dadb0f1d9ce7d448
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78621742"
---
# <a name="integrated-windows-authentication"></a>Integrované ověřování systému Windows

o [Jan Wasson](https://github.com/MikeWasson)

Integrované ověřování systému Windows umožňuje uživatelům přihlašovat se pomocí přihlašovacích údajů k Windows pomocí protokolu Kerberos nebo NTLM. Klient odesílá pověření do autorizační hlavičky. Ověřování systému Windows je nejvhodnější pro intranetové prostředí. Další informace najdete v tématu [ověřování systému Windows](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication).

| Výhody | Nevýhody |
| --- | --- |
| – Integrováno do služby IIS. – Neposílá přihlašovací údaje uživatele v žádosti. – Pokud klientský počítač patří do domény (například intranetové aplikace), uživatel nemusí zadávat přihlašovací údaje. | – Nedoporučuje se pro internetové aplikace. – Vyžaduje podporu protokolu Kerberos nebo NTLM v klientovi. -Klient musí být v doméně služby Active Directory. |

> [!NOTE]
> Pokud je vaše aplikace hostována v Azure a máte místní doménu služby Active Directory, zvažte federování vaší místní služby AD pomocí Azure Active Directory. Tímto způsobem se uživatelé můžou přihlašovat pomocí místních přihlašovacích údajů, ale ověřování provádí služba Azure AD. Další informace najdete v tématu [ověřování Azure](../../../visual-studio/overview/2012/windows-azure-authentication.md).

Pokud chcete vytvořit aplikaci, která používá integrované ověřování systému Windows, vyberte šablonu intranetová aplikace v Průvodci projektem MVC 4. Tato šablona projektu vloží následující nastavení do souboru Web. config:

[!code-xml[Main](integrated-windows-authentication/samples/sample1.xml)]

Na straně klienta funguje integrované ověřování systému Windows s jakýmkoli prohlížečem, který podporuje schéma ověřování [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) , které zahrnuje většinu hlavních prohlížečů. Pro klientské aplikace .NET třída **HttpClient** podporuje ověřování systému Windows:

[!code-csharp[Main](integrated-windows-authentication/samples/sample2.cs)]

Ověřování systému Windows je zranitelné vůči útokům prostřednictvím CSRF (mezi lokalitami). Přečtěte si téma [prevence útoků proti falšování (CSRF) žádostí mezi weby](preventing-cross-site-request-forgery-csrf-attacks.md).

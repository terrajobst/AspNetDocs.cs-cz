---
uid: aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
title: Povoluje se ověřování Windows v Katana | Microsoft Docs
author: MikeWasson
description: 'Tento článek popisuje, jak v Katana povolit ověřování systému Windows. Týká se to dvou scénářů: použití služby IIS k hostování Katana a použití HttpListener k samoobslužnému hostování kat...'
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 82324ef0-3b75-4f63-a217-76ef4036ec93
msc.legacyurl: /aspnet/overview/owin-and-katana/enabling-windows-authentication-in-katana
msc.type: authoredcontent
ms.openlocfilehash: 3d81e7e1bf13ab63417378fba0c5ab80213f404b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617178"
---
# <a name="enabling-windows-authentication-in-katana"></a>Povolení ověřování systému Windows v sadě Katana

o [Jan Wasson](https://github.com/MikeWasson)

> Tento článek popisuje, jak v Katana povolit ověřování systému Windows. Zabývá se dvěma scénáři: používání služby IIS k hostování Katana a použití HttpListener k samoobslužnému hostování Katana ve vlastním procesu. Děkujeme Barryho Dorrans, David Matson a Novák Rossův pro kontrolu tohoto článku.

Katana je implementace [Owin](http://owin.org/)od Microsoftu, které představuje otevřené webové rozhraní pro .NET. Úvod do OWIN a Katana si můžete přečíst [tady](an-overview-of-project-katana.md). Architektura OWIN má několik vrstev:

- Hostitel: slouží ke správě procesu, ve kterém je spuštěný kanál OWIN.
- Server: otevře síťový soket a naslouchat žádostem.
- Middleware: zpracovává požadavek HTTP a odpověď.

Katana v současné době poskytuje dva servery, které podporují integrované ověřování Windows:

- **Microsoft. Owin. Host. SystemWeb**. Používá službu IIS s kanálem ASP.NET.
- **Microsoft. Owin. Host. HttpListener**. Používá [System .NET. HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx). Tento server je momentálně výchozí možností při hostování Katana.

> [!NOTE]
> Katana v současné době neposkytuje OWIN middleware pro ověřování systému Windows, protože tato funkce je již na serverech k dispozici.

## <a name="windows-authentication-in-iis"></a>Ověřování systému Windows ve službě IIS

Pomocí Microsoft. Owin. Host. SystemWeb můžete jednoduše povolit ověřování systému Windows ve službě IIS.

Pojďme začít vytvořením nové aplikace ASP.NET pomocí šablony projektu "prázdná webová aplikace ASP.NET".

![](enabling-windows-authentication-in-katana/_static/image1.png)

Dále přidejte balíčky NuGet. V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**. V okně konzoly Správce balíčků zadejte následující příkaz:

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample1.cmd)]

Nyní přidejte třídu s názvem `Startup` s následujícím kódem:

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample2.cs)]

To je vše, co potřebujete k vytvoření aplikace "Hello World" pro OWIN, která běží na službě IIS. Pro ladění aplikace stiskněte klávesu F5. Měl by se zobrazit "Hello World!" v okně prohlížeče.

![](enabling-windows-authentication-in-katana/_static/image2.png)

Dále povolíme ověřování systému Windows v IIS Express. V nabídce **zobrazení** vyberte možnost **vlastnosti**. Kliknutím na název projektu v Průzkumník řešení zobrazíte vlastnosti projektu.

V okně **vlastnosti** nastavte **anonymní ověřování** na **zakázáno** a nastavte **ověřování systému Windows** na **povoleno**.

![](enabling-windows-authentication-in-katana/_static/image3.png)

Při spuštění aplikace ze sady Visual Studio bude IIS Express vyžadovat pověření systému Windows uživatele. To můžete zobrazit pomocí [Fiddler](http://fiddler2.com/home) nebo jiného nástroje pro ladění http. Tady je příklad odpovědi HTTP:

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample3.cmd?highlight=1,5-6)]

Hlavičky WWW-Authenticate v této odpovědi označují, že server podporuje protokol [Negotiate](http://www.ietf.org/rfc/rfc4559.txt) , který používá protokol Kerberos nebo NTLM.

Když později nasadíte aplikaci na server, postupujte podle [těchto kroků](https://www.iis.net/configreference/system.webserver/security/authentication/windowsauthentication) a povolte ověřování systému Windows ve službě IIS na daném serveru.

## <a name="windows-authentication-in-httplistener"></a>Ověřování systému Windows v HttpListener

Pokud používáte Microsoft. Owin. Host. HttpListener k samoobslužnému hostování Katana, můžete povolit ověřování systému Windows přímo v instanci **HttpListener** .

Nejprve vytvořte novou konzolovou aplikaci. Dále přidejte balíčky NuGet. V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**. V okně konzoly Správce balíčků zadejte následující příkaz:

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample4.cmd)]

Nyní přidejte třídu s názvem `Startup` s následujícím kódem:

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample5.cs)]

Tato třída implementuje stejný příklad "Hello World" z dřív, ale také nastaví ověřování systému Windows jako schéma ověřování.

Uvnitř funkce `Main` spusťte kanál OWIN:

[!code-csharp[Main](enabling-windows-authentication-in-katana/samples/sample6.cs)]

V Fiddler můžete odeslat žádost o potvrzení, že aplikace používá ověřování systému Windows:

[!code-console[Main](enabling-windows-authentication-in-katana/samples/sample7.cmd?highlight=1,4-5)]

## <a name="related-topics"></a>Související témata

[Přehled projektu Katana](an-overview-of-project-katana.md)

[System .NET. HttpListener](https://msdn.microsoft.com/library/system.net.httplistener.aspx)

[Principy ověřování OWIN Forms v MVC 5](https://blogs.msdn.com/b/webdev/archive/2013/07/03/understanding-owin-forms-authentication-in-mvc-5.aspx)

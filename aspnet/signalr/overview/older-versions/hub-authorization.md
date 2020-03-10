---
uid: signalr/overview/older-versions/hub-authorization
title: Ověřování a autorizace pro centra signálů (Signal 1. x) | Microsoft Docs
author: bradygaster
description: Toto téma popisuje, jak omezit, kteří uživatelé nebo role mají přístup k metodám rozbočovače.
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: 3d2dfc0e-eac2-4076-a468-325d3d01cc7b
msc.legacyurl: /signalr/overview/older-versions/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8182677c8931f060d98d17008b16ad545bee4e69
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558532"
---
# <a name="authentication-and-authorization-for-signalr-hubs-signalr-1x"></a>Ověřování a autorizace center SignalR (SignalR 1.x)

autorem [Fletcher](https://github.com/pfletcher), který [FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Toto téma popisuje, jak omezit, kteří uživatelé nebo role mají přístup k metodám rozbočovače.

## <a name="overview"></a>Přehled

Toto téma obsahuje následující oddíly:

- [Autorizovat atribut](#authorizeattribute)
- [Vyžadovat ověření pro všechna centra](#requireauth)
- [Přizpůsobená autorizace](#custom)
- [Předání ověřovacích informací klientům](#passauth)
- [Možnosti ověřování pro klienty rozhraní .NET](#authoptions)

    - [Soubor cookie s ověřováním pomocí formulářů](#cookie)
    - [Ověřování systému Windows](#windows)
    - [Záhlaví připojení](#header)
    - [Certifikát](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a>Autorizovat atribut

Signál poskytuje [autorizačnímu atributu oprávnění](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) určit, kteří uživatelé nebo role mají přístup k rozbočovači nebo metodě. Tento atribut je umístěn v oboru názvů `Microsoft.AspNet.SignalR`. Atribut `Authorize` aplikujete buď na centrum, nebo na konkrétní metody v centru. Při použití atributu `Authorize` pro třídu centra se zadaný požadavek na autorizaci použije na všechny metody v centru. Níže jsou uvedené různé typy autorizačních požadavků, které můžete použít. Bez atributu `Authorize` jsou všechny veřejné metody v centru k dispozici klientovi, který je připojen k centru.

Pokud jste ve webové aplikaci definovali roli admin (správce), můžete určit, že k centru budou mít přístup jenom uživatelé v této roli s následujícím kódem.

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

Nebo můžete určit, že rozbočovač obsahuje jednu metodu, která je k dispozici všem uživatelům, a druhou metodu, která je k dispozici pouze pro ověřené uživatele, jak je znázorněno níže.

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

Následující příklady řeší různé scénáře autorizace:

- `[Authorize]` – pouze ověření uživatelé
- `[Authorize(Roles = "Admin,Manager")]` – pouze ověření uživatelé v zadaných rolích
- `[Authorize(Users = "user1,user2")]` – pouze ověření uživatelé s určenými uživatelskými jmény
- `[Authorize(RequireOutgoing=false)]` – k vyvolání centra můžou použít jenom ověření uživatelé, ale volání ze serveru zpátky na klienty nejsou omezená autorizací, jako je třeba, když můžou poslat zprávu jenom někteří uživatelé, ale zpráva se může dostat do všech ostatních. Vlastnost RequireOutgoing lze použít pouze pro celé centrum, nikoli pro jednotlivce v rámci centra. Pokud RequireOutgoing není nastavené na hodnotu false, budou se ze serveru volat jenom uživatelé, kteří splňují požadavek na autorizaci.

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a>Vyžadovat ověření pro všechna centra

Ověřování pro všechny metody centra a centra v aplikaci můžete vyžadovat voláním metody [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) při spuštění aplikace. Tuto metodu můžete použít, pokud máte více rozbočovačů a chcete vymáhat požadavek na ověření pro všechny z nich. Pomocí této metody nelze zadat roli, uživatele ani odchozí autorizaci. Můžete zadat jenom přístup k metodám rozbočovače, který je omezený na ověřené uživatele. Přesto však můžete použít atribut autorizovat na centra nebo metody k určení dalších požadavků. Kromě základního požadavku ověřování se použije jakýkoli požadavek, který zadáte v atributech.

Následující příklad ukazuje soubor Global. asax, který omezuje všechny metody centra na ověřené uživatele.

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

Pokud zavoláte metodu `RequireAuthentication()` po zpracování žádosti o signál, Signaler vyvolá výjimku `InvalidOperationException`. Tato výjimka je vyvolána, protože po vyvolání kanálu nelze přidat modul do HubPipeline. Předchozí příklad ukazuje volání metody `RequireAuthentication` v metodě `Application_Start`, která je spuštěna jednou před zpracováním prvního požadavku.

<a id="custom"></a>

## <a name="customized-authorization"></a>Přizpůsobená autorizace

Pokud potřebujete přizpůsobit způsob určování autorizace, můžete vytvořit třídu, která je odvozena z `AuthorizeAttribute` a přepsat metodu [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) . Tato metoda je volána pro každý požadavek k určení, zda je uživatel autorizován k dokončení žádosti. V přepsané metodě zadáte potřebnou logiku pro váš autorizační scénář. Následující příklad ukazuje, jak vymáhat autorizaci pomocí identity založené na deklaracích identity.

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a>Předání ověřovacích informací klientům

V kódu, který běží na klientovi, možná budete muset použít ověřovací údaje. Požadované informace předáte při volání metod na klientovi. Například metoda aplikace Chat může předat jako parametr uživatelské jméno osoby, která odesílá zprávu, jak je znázorněno níže.

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

Nebo můžete vytvořit objekt, který představuje ověřovací informace a předat tento objekt jako parametr, jak je znázorněno níže.

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

Nikdy byste neměli předat ID připojení jednoho klienta jiným klientům, protože ho uživatel se zlými úmysly mohl použít k napodobení žádosti od tohoto klienta.

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a>Možnosti ověřování pro klienty rozhraní .NET

Pokud máte klienta .NET, například konzolovou aplikaci, která komunikuje s centrem, které je omezené na ověřené uživatele, můžete přihlašovací údaje pro ověřování předat v souboru cookie, v záhlaví připojení nebo v certifikátu. Příklady v této části ukazují, jak používat tyto různé metody ověřování uživatele. Nejedná se o plně funkční signalizaci aplikací. Další informace o klientech rozhraní .NET s nástrojem Signal najdete v tématu [Průvodce rozhraním API pro centra – klient .NET](../guide-to-the-api/hubs-api-guide-net-client.md).

<a id="cookie"></a>

### <a name="cookie"></a>Soubor cookie

Když klient .NET komunikuje s centrem, které používá ověřování pomocí formulářů ASP.NET, budete muset ručně nastavit ověřovací soubor cookie pro připojení. Soubor cookie přidáte do vlastnosti `CookieContainer` v objektu [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) . Následující příklad ukazuje konzolovou aplikaci, která načte ověřovací soubor cookie z webové stránky a přidá tento soubor cookie k připojení. Adresa URL `https://www.contoso.com/RemoteLogin` v příkladu odkazuje na webovou stránku, kterou byste mohli vytvořit. Stránka načte publikované uživatelské jméno a heslo a pokusí se přihlásit uživatele s přihlašovacími údaji.

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

Aplikace konzoly odesílá pověření do www.contoso.com/RemoteLogin, která by mohla odkazovat na prázdnou stránku, která obsahuje následující soubor kódu na pozadí.

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a>Ověřování systému Windows

Při použití ověřování systému Windows můžete přihlašovací údaje aktuálního uživatele předat pomocí vlastnosti [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) . Přihlašovací údaje pro připojení nastavíte na hodnotu DefaultCredentials.

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a>Záhlaví připojení

Pokud vaše aplikace nepoužívá soubory cookie, můžete informace o uživateli předat v hlavičce připojení. Například můžete předat token v hlavičce připojení.

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

Potom můžete v centru ověřit token uživatele.

<a id="certificate"></a>

### <a name="certificate"></a>Certifikát

Můžete předat klientský certifikát a ověřit uživatele. Certifikát se přidává při vytváření připojení. Následující příklad ukazuje pouze postup přidání klientského certifikátu k připojení; nezobrazuje úplnou konzolovou aplikaci. Používá třídu [certifikátu x509](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) , která poskytuje několik různých způsobů, jak vytvořit certifikát.

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]

---
uid: signalr/overview/security/hub-authorization
title: Ověřování a autorizace pro centra signalizace | Microsoft Docs
author: bradygaster
description: Toto téma popisuje, jak omezit, kteří uživatelé nebo role mají přístup k metodám rozbočovače. Verze softwaru používané v tomto tématu Visual Studio 2013 signalizace rozhraní .NET 4,5...
ms.author: bradyg
ms.date: 01/05/2015
ms.assetid: a610c796-c131-473c-baef-2e6c568cb2a2
msc.legacyurl: /signalr/overview/security/hub-authorization
msc.type: authoredcontent
ms.openlocfilehash: 5006af5e623da6958a6d59949c6f2cf776c77fc3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578916"
---
# <a name="authentication-and-authorization-for-signalr-hubs"></a>Ověřování a autorizace center SignalR

autorem [Fletcher](https://github.com/pfletcher), který [FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Toto téma popisuje, jak omezit, kteří uživatelé nebo role mají přístup k metodám rozbočovače.
>
> ## <a name="software-versions-used-in-this-topic"></a>Verze softwaru používané v tomto tématu
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - Signal – verze 2
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>Předchozí verze tohoto tématu
>
> Informace o dřívějších verzích nástroje Signal najdete v části [Signal – starší verze](../older-versions/index.md).
>
> ## <a name="questions-and-comments"></a>Dotazy a komentáře
>
> Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky. Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).

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

Signál poskytuje [autorizačnímu atributu oprávnění](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) určit, kteří uživatelé nebo role mají přístup k rozbočovači nebo metodě. Tento atribut je umístěn v oboru názvů `Microsoft.AspNet.SignalR`. Atribut `Authorize` aplikujete buď na centrum, nebo na konkrétní metody v centru. Při použití atributu `Authorize` pro třídu centra se zadaný požadavek na autorizaci použije na všechny metody v centru. V tomto tématu najdete příklady různých typů autorizačních požadavků, které můžete použít. Bez atributu `Authorize` má připojený klient přístup k libovolné veřejné metodě v centru.

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

Ověřování pro všechny metody centra a centra v aplikaci můžete vyžadovat voláním metody [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) při spuštění aplikace. Tuto metodu můžete použít, pokud máte více rozbočovačů a chcete vymáhat požadavek na ověření pro všechny z nich. V této metodě nemůžete zadat požadavky na role, uživatele nebo odchozí autorizaci. Můžete zadat jenom přístup k metodám rozbočovače, který je omezený na ověřené uživatele. Přesto však můžete použít atribut autorizovat na centra nebo metody k určení dalších požadavků. Všechny požadavky, které zadáte v atributu, se přidají do základního požadavku ověřování.

Následující příklad ukazuje spouštěcí soubor, který omezuje všechny metody centra na ověřené uživatele.

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

Pokud zavoláte metodu `RequireAuthentication()` po zpracování žádosti o signál, Signaler vyvolá výjimku `InvalidOperationException`. Signál vyvolá tuto výjimku, protože po vyvolání kanálu nelze přidat modul do HubPipeline. Předchozí příklad ukazuje volání metody `RequireAuthentication` v metodě `Configuration`, která je spuštěna jednou před zpracováním prvního požadavku.

<a id="custom"></a>

## <a name="customized-authorization"></a>Přizpůsobená autorizace

Pokud potřebujete přizpůsobit způsob určování autorizace, můžete vytvořit třídu, která je odvozena z `AuthorizeAttribute` a přepsat metodu [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) . Pro každý požadavek vyvolá signál tuto metodu k určení, zda je uživatel autorizován k dokončení žádosti. V přepsané metodě zadáte potřebnou logiku pro váš autorizační scénář. Následující příklad ukazuje, jak vymáhat autorizaci pomocí identity založené na deklaracích identity.

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

Když klient .NET komunikuje s centrem, které používá ověřování pomocí formulářů ASP.NET, budete muset ručně nastavit ověřovací soubor cookie pro připojení. Soubor cookie přidáte do vlastnosti `CookieContainer` v objektu [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) . Následující příklad ukazuje konzolovou aplikaci, která načte ověřovací soubor cookie z webové stránky a přidá tento soubor cookie k připojení.

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

Aplikace konzoly odesílá pověření do <strong>www.contoso.com/RemoteLogin</strong> , která by mohla odkazovat na prázdnou stránku, která obsahuje následující soubor kódu na pozadí.

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

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
# <a name="authentication-and-authorization-for-signalr-hubs-signalr-1x"></a><span data-ttu-id="4cac6-103">Ověřování a autorizace center SignalR (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="4cac6-103">Authentication and Authorization for SignalR Hubs (SignalR 1.x)</span></span>

<span data-ttu-id="4cac6-104">autorem [Fletcher](https://github.com/pfletcher), který [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="4cac6-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="4cac6-105">Toto téma popisuje, jak omezit, kteří uživatelé nebo role mají přístup k metodám rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="4cac6-105">This topic describes how to restrict which users or roles can access hub methods.</span></span>

## <a name="overview"></a><span data-ttu-id="4cac6-106">Přehled</span><span class="sxs-lookup"><span data-stu-id="4cac6-106">Overview</span></span>

<span data-ttu-id="4cac6-107">Toto téma obsahuje následující oddíly:</span><span class="sxs-lookup"><span data-stu-id="4cac6-107">This topic contains the following sections:</span></span>

- [<span data-ttu-id="4cac6-108">Autorizovat atribut</span><span class="sxs-lookup"><span data-stu-id="4cac6-108">Authorize attribute</span></span>](#authorizeattribute)
- [<span data-ttu-id="4cac6-109">Vyžadovat ověření pro všechna centra</span><span class="sxs-lookup"><span data-stu-id="4cac6-109">Require authentication for all hubs</span></span>](#requireauth)
- [<span data-ttu-id="4cac6-110">Přizpůsobená autorizace</span><span class="sxs-lookup"><span data-stu-id="4cac6-110">Customized authorization</span></span>](#custom)
- [<span data-ttu-id="4cac6-111">Předání ověřovacích informací klientům</span><span class="sxs-lookup"><span data-stu-id="4cac6-111">Pass authentication information to clients</span></span>](#passauth)
- [<span data-ttu-id="4cac6-112">Možnosti ověřování pro klienty rozhraní .NET</span><span class="sxs-lookup"><span data-stu-id="4cac6-112">Authentication options for .NET clients</span></span>](#authoptions)

    - [<span data-ttu-id="4cac6-113">Soubor cookie s ověřováním pomocí formulářů</span><span class="sxs-lookup"><span data-stu-id="4cac6-113">Cookie with Forms Authentication</span></span>](#cookie)
    - [<span data-ttu-id="4cac6-114">Ověřování systému Windows</span><span class="sxs-lookup"><span data-stu-id="4cac6-114">Windows Authentication</span></span>](#windows)
    - [<span data-ttu-id="4cac6-115">Záhlaví připojení</span><span class="sxs-lookup"><span data-stu-id="4cac6-115">Connection header</span></span>](#header)
    - [<span data-ttu-id="4cac6-116">Certifikát</span><span class="sxs-lookup"><span data-stu-id="4cac6-116">Certificate</span></span>](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a><span data-ttu-id="4cac6-117">Autorizovat atribut</span><span class="sxs-lookup"><span data-stu-id="4cac6-117">Authorize attribute</span></span>

<span data-ttu-id="4cac6-118">Signál poskytuje [autorizačnímu atributu oprávnění](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) určit, kteří uživatelé nebo role mají přístup k rozbočovači nebo metodě.</span><span class="sxs-lookup"><span data-stu-id="4cac6-118">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users or roles have access to a hub or method.</span></span> <span data-ttu-id="4cac6-119">Tento atribut je umístěn v oboru názvů `Microsoft.AspNet.SignalR`.</span><span class="sxs-lookup"><span data-stu-id="4cac6-119">This attribute is located in the `Microsoft.AspNet.SignalR` namespace.</span></span> <span data-ttu-id="4cac6-120">Atribut `Authorize` aplikujete buď na centrum, nebo na konkrétní metody v centru.</span><span class="sxs-lookup"><span data-stu-id="4cac6-120">You apply the `Authorize` attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="4cac6-121">Při použití atributu `Authorize` pro třídu centra se zadaný požadavek na autorizaci použije na všechny metody v centru.</span><span class="sxs-lookup"><span data-stu-id="4cac6-121">When you apply the `Authorize` attribute to a hub class, the specified authorization requirement is applied to all of the methods in the hub.</span></span> <span data-ttu-id="4cac6-122">Níže jsou uvedené různé typy autorizačních požadavků, které můžete použít.</span><span class="sxs-lookup"><span data-stu-id="4cac6-122">The different types of authorization requirements that you can apply are shown below.</span></span> <span data-ttu-id="4cac6-123">Bez atributu `Authorize` jsou všechny veřejné metody v centru k dispozici klientovi, který je připojen k centru.</span><span class="sxs-lookup"><span data-stu-id="4cac6-123">Without the `Authorize` attribute, all public methods on the hub are available to a client that is connected to the hub.</span></span>

<span data-ttu-id="4cac6-124">Pokud jste ve webové aplikaci definovali roli admin (správce), můžete určit, že k centru budou mít přístup jenom uživatelé v této roli s následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="4cac6-124">If you have defined a role named "Admin" in your web application, you could specify that only users in that role can access a hub with the following code.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

<span data-ttu-id="4cac6-125">Nebo můžete určit, že rozbočovač obsahuje jednu metodu, která je k dispozici všem uživatelům, a druhou metodu, která je k dispozici pouze pro ověřené uživatele, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="4cac6-125">Or, you can specify that a hub contains one method that is available to all users, and a second method that is only available to authenticated users, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

<span data-ttu-id="4cac6-126">Následující příklady řeší různé scénáře autorizace:</span><span class="sxs-lookup"><span data-stu-id="4cac6-126">The following examples address different authorization scenarios:</span></span>

- <span data-ttu-id="4cac6-127">`[Authorize]` – pouze ověření uživatelé</span><span class="sxs-lookup"><span data-stu-id="4cac6-127">`[Authorize]` – only authenticated users</span></span>
- <span data-ttu-id="4cac6-128">`[Authorize(Roles = "Admin,Manager")]` – pouze ověření uživatelé v zadaných rolích</span><span class="sxs-lookup"><span data-stu-id="4cac6-128">`[Authorize(Roles = "Admin,Manager")]` – only authenticated users in the specified roles</span></span>
- <span data-ttu-id="4cac6-129">`[Authorize(Users = "user1,user2")]` – pouze ověření uživatelé s určenými uživatelskými jmény</span><span class="sxs-lookup"><span data-stu-id="4cac6-129">`[Authorize(Users = "user1,user2")]` – only authenticated users with the specified user names</span></span>
- <span data-ttu-id="4cac6-130">`[Authorize(RequireOutgoing=false)]` – k vyvolání centra můžou použít jenom ověření uživatelé, ale volání ze serveru zpátky na klienty nejsou omezená autorizací, jako je třeba, když můžou poslat zprávu jenom někteří uživatelé, ale zpráva se může dostat do všech ostatních.</span><span class="sxs-lookup"><span data-stu-id="4cac6-130">`[Authorize(RequireOutgoing=false)]` – only authenticated users can invoke the hub, but calls from the server back to clients are not limited by authorization, such as, when only certain users can send a message but all others can receive the message.</span></span> <span data-ttu-id="4cac6-131">Vlastnost RequireOutgoing lze použít pouze pro celé centrum, nikoli pro jednotlivce v rámci centra.</span><span class="sxs-lookup"><span data-stu-id="4cac6-131">The RequireOutgoing property can only be applied to the entire hub, not on individuals methods within the hub.</span></span> <span data-ttu-id="4cac6-132">Pokud RequireOutgoing není nastavené na hodnotu false, budou se ze serveru volat jenom uživatelé, kteří splňují požadavek na autorizaci.</span><span class="sxs-lookup"><span data-stu-id="4cac6-132">When RequireOutgoing is not set to false, only users that meet the authorization requirement are called from the server.</span></span>

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a><span data-ttu-id="4cac6-133">Vyžadovat ověření pro všechna centra</span><span class="sxs-lookup"><span data-stu-id="4cac6-133">Require authentication for all hubs</span></span>

<span data-ttu-id="4cac6-134">Ověřování pro všechny metody centra a centra v aplikaci můžete vyžadovat voláním metody [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) při spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="4cac6-134">You can require authentication for all hubs and hub methods in your application by calling the [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="4cac6-135">Tuto metodu můžete použít, pokud máte více rozbočovačů a chcete vymáhat požadavek na ověření pro všechny z nich.</span><span class="sxs-lookup"><span data-stu-id="4cac6-135">You might use this method when you have multiple hubs and want to enforce an authentication requirement for all of them.</span></span> <span data-ttu-id="4cac6-136">Pomocí této metody nelze zadat roli, uživatele ani odchozí autorizaci.</span><span class="sxs-lookup"><span data-stu-id="4cac6-136">With this method, you cannot specify role, user, or outgoing authorization.</span></span> <span data-ttu-id="4cac6-137">Můžete zadat jenom přístup k metodám rozbočovače, který je omezený na ověřené uživatele.</span><span class="sxs-lookup"><span data-stu-id="4cac6-137">You can only specify that access to the hub methods is restricted to authenticated users.</span></span> <span data-ttu-id="4cac6-138">Přesto však můžete použít atribut autorizovat na centra nebo metody k určení dalších požadavků.</span><span class="sxs-lookup"><span data-stu-id="4cac6-138">However, you can still apply the Authorize attribute to hubs or methods to specify additional requirements.</span></span> <span data-ttu-id="4cac6-139">Kromě základního požadavku ověřování se použije jakýkoli požadavek, který zadáte v atributech.</span><span class="sxs-lookup"><span data-stu-id="4cac6-139">Any requirement you specify in attributes is applied in addition to the basic requirement of authentication.</span></span>

<span data-ttu-id="4cac6-140">Následující příklad ukazuje soubor Global. asax, který omezuje všechny metody centra na ověřené uživatele.</span><span class="sxs-lookup"><span data-stu-id="4cac6-140">The following example shows a Global.asax file which restricts all hub methods to authenticated users.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

<span data-ttu-id="4cac6-141">Pokud zavoláte metodu `RequireAuthentication()` po zpracování žádosti o signál, Signaler vyvolá výjimku `InvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="4cac6-141">If you call the `RequireAuthentication()` method after a SignalR request has been processed, SignalR will throw a `InvalidOperationException` exception.</span></span> <span data-ttu-id="4cac6-142">Tato výjimka je vyvolána, protože po vyvolání kanálu nelze přidat modul do HubPipeline.</span><span class="sxs-lookup"><span data-stu-id="4cac6-142">This exception is thrown because you cannot add a module to the HubPipeline after the pipeline has been invoked.</span></span> <span data-ttu-id="4cac6-143">Předchozí příklad ukazuje volání metody `RequireAuthentication` v metodě `Application_Start`, která je spuštěna jednou před zpracováním prvního požadavku.</span><span class="sxs-lookup"><span data-stu-id="4cac6-143">The previous example shows calling the `RequireAuthentication` method in the `Application_Start` method which is executed one time prior to handling the first request.</span></span>

<a id="custom"></a>

## <a name="customized-authorization"></a><span data-ttu-id="4cac6-144">Přizpůsobená autorizace</span><span class="sxs-lookup"><span data-stu-id="4cac6-144">Customized authorization</span></span>

<span data-ttu-id="4cac6-145">Pokud potřebujete přizpůsobit způsob určování autorizace, můžete vytvořit třídu, která je odvozena z `AuthorizeAttribute` a přepsat metodu [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) .</span><span class="sxs-lookup"><span data-stu-id="4cac6-145">If you need to customize how authorization is determined, you can create a class that derives from `AuthorizeAttribute` and override the [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) method.</span></span> <span data-ttu-id="4cac6-146">Tato metoda je volána pro každý požadavek k určení, zda je uživatel autorizován k dokončení žádosti.</span><span class="sxs-lookup"><span data-stu-id="4cac6-146">This method is called for each request to determine whether the user is authorized to complete the request.</span></span> <span data-ttu-id="4cac6-147">V přepsané metodě zadáte potřebnou logiku pro váš autorizační scénář.</span><span class="sxs-lookup"><span data-stu-id="4cac6-147">In the overridden method, you provide the necessary logic for your authorization scenario.</span></span> <span data-ttu-id="4cac6-148">Následující příklad ukazuje, jak vymáhat autorizaci pomocí identity založené na deklaracích identity.</span><span class="sxs-lookup"><span data-stu-id="4cac6-148">The following example shows how to enforce authorization through claims-based identity.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a><span data-ttu-id="4cac6-149">Předání ověřovacích informací klientům</span><span class="sxs-lookup"><span data-stu-id="4cac6-149">Pass authentication information to clients</span></span>

<span data-ttu-id="4cac6-150">V kódu, který běží na klientovi, možná budete muset použít ověřovací údaje.</span><span class="sxs-lookup"><span data-stu-id="4cac6-150">You may need to use authentication information in the code that runs on the client.</span></span> <span data-ttu-id="4cac6-151">Požadované informace předáte při volání metod na klientovi.</span><span class="sxs-lookup"><span data-stu-id="4cac6-151">You pass the required information when calling the methods on the client.</span></span> <span data-ttu-id="4cac6-152">Například metoda aplikace Chat může předat jako parametr uživatelské jméno osoby, která odesílá zprávu, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="4cac6-152">For example, a chat application method could pass as a parameter the user name of the person posting a message, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

<span data-ttu-id="4cac6-153">Nebo můžete vytvořit objekt, který představuje ověřovací informace a předat tento objekt jako parametr, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="4cac6-153">Or, you can create an object to represent the authentication information and pass that object as a parameter, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

<span data-ttu-id="4cac6-154">Nikdy byste neměli předat ID připojení jednoho klienta jiným klientům, protože ho uživatel se zlými úmysly mohl použít k napodobení žádosti od tohoto klienta.</span><span class="sxs-lookup"><span data-stu-id="4cac6-154">You should never pass one client's connection id to other clients, as a malicious user could use it to mimic a request from that client.</span></span>

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a><span data-ttu-id="4cac6-155">Možnosti ověřování pro klienty rozhraní .NET</span><span class="sxs-lookup"><span data-stu-id="4cac6-155">Authentication options for .NET clients</span></span>

<span data-ttu-id="4cac6-156">Pokud máte klienta .NET, například konzolovou aplikaci, která komunikuje s centrem, které je omezené na ověřené uživatele, můžete přihlašovací údaje pro ověřování předat v souboru cookie, v záhlaví připojení nebo v certifikátu.</span><span class="sxs-lookup"><span data-stu-id="4cac6-156">When you have a .NET client, such as a console app, which interacts with a hub that is limited to authenticated users, you can pass the authentication credentials in a cookie, the connection header, or a certificate.</span></span> <span data-ttu-id="4cac6-157">Příklady v této části ukazují, jak používat tyto různé metody ověřování uživatele.</span><span class="sxs-lookup"><span data-stu-id="4cac6-157">The examples in this section show how to use those different methods for authenticating a user.</span></span> <span data-ttu-id="4cac6-158">Nejedná se o plně funkční signalizaci aplikací.</span><span class="sxs-lookup"><span data-stu-id="4cac6-158">They are not fully-functional SignalR apps.</span></span> <span data-ttu-id="4cac6-159">Další informace o klientech rozhraní .NET s nástrojem Signal najdete v tématu [Průvodce rozhraním API pro centra – klient .NET](../guide-to-the-api/hubs-api-guide-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="4cac6-159">For more information about .NET clients with SignalR, see [Hubs API Guide - .NET Client](../guide-to-the-api/hubs-api-guide-net-client.md).</span></span>

<a id="cookie"></a>

### <a name="cookie"></a><span data-ttu-id="4cac6-160">Soubor cookie</span><span class="sxs-lookup"><span data-stu-id="4cac6-160">Cookie</span></span>

<span data-ttu-id="4cac6-161">Když klient .NET komunikuje s centrem, které používá ověřování pomocí formulářů ASP.NET, budete muset ručně nastavit ověřovací soubor cookie pro připojení.</span><span class="sxs-lookup"><span data-stu-id="4cac6-161">When your .NET client interacts with a hub that uses ASP.NET Forms Authentication, you will need to manually set the authentication cookie on the connection.</span></span> <span data-ttu-id="4cac6-162">Soubor cookie přidáte do vlastnosti `CookieContainer` v objektu [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) .</span><span class="sxs-lookup"><span data-stu-id="4cac6-162">You add the cookie to the `CookieContainer` property on the [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) object.</span></span> <span data-ttu-id="4cac6-163">Následující příklad ukazuje konzolovou aplikaci, která načte ověřovací soubor cookie z webové stránky a přidá tento soubor cookie k připojení.</span><span class="sxs-lookup"><span data-stu-id="4cac6-163">The following example shows a console app that retrieves an authentication cookie from a web page and adds that cookie to the connection.</span></span> <span data-ttu-id="4cac6-164">Adresa URL `https://www.contoso.com/RemoteLogin` v příkladu odkazuje na webovou stránku, kterou byste mohli vytvořit.</span><span class="sxs-lookup"><span data-stu-id="4cac6-164">The URL `https://www.contoso.com/RemoteLogin` in the example points to a web page that you would need to create.</span></span> <span data-ttu-id="4cac6-165">Stránka načte publikované uživatelské jméno a heslo a pokusí se přihlásit uživatele s přihlašovacími údaji.</span><span class="sxs-lookup"><span data-stu-id="4cac6-165">The page would retrieve the posted user name and password, and attempt to log in the user with the credentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

<span data-ttu-id="4cac6-166">Aplikace konzoly odesílá pověření do www.contoso.com/RemoteLogin, která by mohla odkazovat na prázdnou stránku, která obsahuje následující soubor kódu na pozadí.</span><span class="sxs-lookup"><span data-stu-id="4cac6-166">The console app posts the credentials to www.contoso.com/RemoteLogin which could refer to an empty page that contains the following code-behind file.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a><span data-ttu-id="4cac6-167">Ověřování systému Windows</span><span class="sxs-lookup"><span data-stu-id="4cac6-167">Windows authentication</span></span>

<span data-ttu-id="4cac6-168">Při použití ověřování systému Windows můžete přihlašovací údaje aktuálního uživatele předat pomocí vlastnosti [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) .</span><span class="sxs-lookup"><span data-stu-id="4cac6-168">When using Windows authentication, you can pass the current user's credentials by using the [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) property.</span></span> <span data-ttu-id="4cac6-169">Přihlašovací údaje pro připojení nastavíte na hodnotu DefaultCredentials.</span><span class="sxs-lookup"><span data-stu-id="4cac6-169">You set the credentials for the connection to the value of the DefaultCredentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a><span data-ttu-id="4cac6-170">Záhlaví připojení</span><span class="sxs-lookup"><span data-stu-id="4cac6-170">Connection header</span></span>

<span data-ttu-id="4cac6-171">Pokud vaše aplikace nepoužívá soubory cookie, můžete informace o uživateli předat v hlavičce připojení.</span><span class="sxs-lookup"><span data-stu-id="4cac6-171">If your application is not using cookies, you can pass user information in the connection header.</span></span> <span data-ttu-id="4cac6-172">Například můžete předat token v hlavičce připojení.</span><span class="sxs-lookup"><span data-stu-id="4cac6-172">For example, you can pass a token in the connection header.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

<span data-ttu-id="4cac6-173">Potom můžete v centru ověřit token uživatele.</span><span class="sxs-lookup"><span data-stu-id="4cac6-173">Then, in the hub, you would verify the user's token.</span></span>

<a id="certificate"></a>

### <a name="certificate"></a><span data-ttu-id="4cac6-174">Certifikát</span><span class="sxs-lookup"><span data-stu-id="4cac6-174">Certificate</span></span>

<span data-ttu-id="4cac6-175">Můžete předat klientský certifikát a ověřit uživatele.</span><span class="sxs-lookup"><span data-stu-id="4cac6-175">You can pass a client certificate to verify the user.</span></span> <span data-ttu-id="4cac6-176">Certifikát se přidává při vytváření připojení.</span><span class="sxs-lookup"><span data-stu-id="4cac6-176">You add the certificate when creating the connection.</span></span> <span data-ttu-id="4cac6-177">Následující příklad ukazuje pouze postup přidání klientského certifikátu k připojení; nezobrazuje úplnou konzolovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="4cac6-177">The following example shows only how to add a client certificate to the connection; it does not show the full console app.</span></span> <span data-ttu-id="4cac6-178">Používá třídu [certifikátu x509](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) , která poskytuje několik různých způsobů, jak vytvořit certifikát.</span><span class="sxs-lookup"><span data-stu-id="4cac6-178">It uses the [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) class which provides several different ways to create the certificate.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]

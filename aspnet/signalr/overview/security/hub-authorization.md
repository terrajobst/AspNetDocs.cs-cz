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
# <a name="authentication-and-authorization-for-signalr-hubs"></a><span data-ttu-id="17850-104">Ověřování a autorizace center SignalR</span><span class="sxs-lookup"><span data-stu-id="17850-104">Authentication and Authorization for SignalR Hubs</span></span>

<span data-ttu-id="17850-105">autorem [Fletcher](https://github.com/pfletcher), který [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="17850-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="17850-106">Toto téma popisuje, jak omezit, kteří uživatelé nebo role mají přístup k metodám rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="17850-106">This topic describes how to restrict which users or roles can access hub methods.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="17850-107">Verze softwaru používané v tomto tématu</span><span class="sxs-lookup"><span data-stu-id="17850-107">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="17850-108">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="17850-108">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="17850-109">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="17850-109">.NET 4.5</span></span>
> - <span data-ttu-id="17850-110">Signal – verze 2</span><span class="sxs-lookup"><span data-stu-id="17850-110">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="17850-111">Předchozí verze tohoto tématu</span><span class="sxs-lookup"><span data-stu-id="17850-111">Previous versions of this topic</span></span>
>
> <span data-ttu-id="17850-112">Informace o dřívějších verzích nástroje Signal najdete v části [Signal – starší verze](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="17850-112">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="17850-113">Dotazy a komentáře</span><span class="sxs-lookup"><span data-stu-id="17850-113">Questions and comments</span></span>
>
> <span data-ttu-id="17850-114">Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="17850-114">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="17850-115">Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="17850-115">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="17850-116">Přehled</span><span class="sxs-lookup"><span data-stu-id="17850-116">Overview</span></span>

<span data-ttu-id="17850-117">Toto téma obsahuje následující oddíly:</span><span class="sxs-lookup"><span data-stu-id="17850-117">This topic contains the following sections:</span></span>

- [<span data-ttu-id="17850-118">Autorizovat atribut</span><span class="sxs-lookup"><span data-stu-id="17850-118">Authorize attribute</span></span>](#authorizeattribute)
- [<span data-ttu-id="17850-119">Vyžadovat ověření pro všechna centra</span><span class="sxs-lookup"><span data-stu-id="17850-119">Require authentication for all hubs</span></span>](#requireauth)
- [<span data-ttu-id="17850-120">Přizpůsobená autorizace</span><span class="sxs-lookup"><span data-stu-id="17850-120">Customized authorization</span></span>](#custom)
- [<span data-ttu-id="17850-121">Předání ověřovacích informací klientům</span><span class="sxs-lookup"><span data-stu-id="17850-121">Pass authentication information to clients</span></span>](#passauth)
- [<span data-ttu-id="17850-122">Možnosti ověřování pro klienty rozhraní .NET</span><span class="sxs-lookup"><span data-stu-id="17850-122">Authentication options for .NET clients</span></span>](#authoptions)

    - [<span data-ttu-id="17850-123">Soubor cookie s ověřováním pomocí formulářů</span><span class="sxs-lookup"><span data-stu-id="17850-123">Cookie with Forms Authentication</span></span>](#cookie)
    - [<span data-ttu-id="17850-124">Ověřování systému Windows</span><span class="sxs-lookup"><span data-stu-id="17850-124">Windows Authentication</span></span>](#windows)
    - [<span data-ttu-id="17850-125">Záhlaví připojení</span><span class="sxs-lookup"><span data-stu-id="17850-125">Connection header</span></span>](#header)
    - [<span data-ttu-id="17850-126">Certifikát</span><span class="sxs-lookup"><span data-stu-id="17850-126">Certificate</span></span>](#certificate)

<a id="authorizeattribute"></a>

## <a name="authorize-attribute"></a><span data-ttu-id="17850-127">Autorizovat atribut</span><span class="sxs-lookup"><span data-stu-id="17850-127">Authorize attribute</span></span>

<span data-ttu-id="17850-128">Signál poskytuje [autorizačnímu atributu oprávnění](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) určit, kteří uživatelé nebo role mají přístup k rozbočovači nebo metodě.</span><span class="sxs-lookup"><span data-stu-id="17850-128">SignalR provides the [Authorize](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute(v=vs.111).aspx) attribute to specify which users or roles have access to a hub or method.</span></span> <span data-ttu-id="17850-129">Tento atribut je umístěn v oboru názvů `Microsoft.AspNet.SignalR`.</span><span class="sxs-lookup"><span data-stu-id="17850-129">This attribute is located in the `Microsoft.AspNet.SignalR` namespace.</span></span> <span data-ttu-id="17850-130">Atribut `Authorize` aplikujete buď na centrum, nebo na konkrétní metody v centru.</span><span class="sxs-lookup"><span data-stu-id="17850-130">You apply the `Authorize` attribute to either a hub or particular methods in a hub.</span></span> <span data-ttu-id="17850-131">Při použití atributu `Authorize` pro třídu centra se zadaný požadavek na autorizaci použije na všechny metody v centru.</span><span class="sxs-lookup"><span data-stu-id="17850-131">When you apply the `Authorize` attribute to a hub class, the specified authorization requirement is applied to all of the methods in the hub.</span></span> <span data-ttu-id="17850-132">V tomto tématu najdete příklady různých typů autorizačních požadavků, které můžete použít.</span><span class="sxs-lookup"><span data-stu-id="17850-132">This topic provides examples of the different types of authorization requirements that you can apply.</span></span> <span data-ttu-id="17850-133">Bez atributu `Authorize` má připojený klient přístup k libovolné veřejné metodě v centru.</span><span class="sxs-lookup"><span data-stu-id="17850-133">Without the `Authorize` attribute, a connected client can access any public method on the hub.</span></span>

<span data-ttu-id="17850-134">Pokud jste ve webové aplikaci definovali roli admin (správce), můžete určit, že k centru budou mít přístup jenom uživatelé v této roli s následujícím kódem.</span><span class="sxs-lookup"><span data-stu-id="17850-134">If you have defined a role named "Admin" in your web application, you could specify that only users in that role can access a hub with the following code.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample1.cs)]

<span data-ttu-id="17850-135">Nebo můžete určit, že rozbočovač obsahuje jednu metodu, která je k dispozici všem uživatelům, a druhou metodu, která je k dispozici pouze pro ověřené uživatele, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="17850-135">Or, you can specify that a hub contains one method that is available to all users, and a second method that is only available to authenticated users, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample2.cs)]

<span data-ttu-id="17850-136">Následující příklady řeší různé scénáře autorizace:</span><span class="sxs-lookup"><span data-stu-id="17850-136">The following examples address different authorization scenarios:</span></span>

- <span data-ttu-id="17850-137">`[Authorize]` – pouze ověření uživatelé</span><span class="sxs-lookup"><span data-stu-id="17850-137">`[Authorize]` – only authenticated users</span></span>
- <span data-ttu-id="17850-138">`[Authorize(Roles = "Admin,Manager")]` – pouze ověření uživatelé v zadaných rolích</span><span class="sxs-lookup"><span data-stu-id="17850-138">`[Authorize(Roles = "Admin,Manager")]` – only authenticated users in the specified roles</span></span>
- <span data-ttu-id="17850-139">`[Authorize(Users = "user1,user2")]` – pouze ověření uživatelé s určenými uživatelskými jmény</span><span class="sxs-lookup"><span data-stu-id="17850-139">`[Authorize(Users = "user1,user2")]` – only authenticated users with the specified user names</span></span>
- <span data-ttu-id="17850-140">`[Authorize(RequireOutgoing=false)]` – k vyvolání centra můžou použít jenom ověření uživatelé, ale volání ze serveru zpátky na klienty nejsou omezená autorizací, jako je třeba, když můžou poslat zprávu jenom někteří uživatelé, ale zpráva se může dostat do všech ostatních.</span><span class="sxs-lookup"><span data-stu-id="17850-140">`[Authorize(RequireOutgoing=false)]` – only authenticated users can invoke the hub, but calls from the server back to clients are not limited by authorization, such as, when only certain users can send a message but all others can receive the message.</span></span> <span data-ttu-id="17850-141">Vlastnost RequireOutgoing lze použít pouze pro celé centrum, nikoli pro jednotlivce v rámci centra.</span><span class="sxs-lookup"><span data-stu-id="17850-141">The RequireOutgoing property can only be applied to the entire hub, not on individuals methods within the hub.</span></span> <span data-ttu-id="17850-142">Pokud RequireOutgoing není nastavené na hodnotu false, budou se ze serveru volat jenom uživatelé, kteří splňují požadavek na autorizaci.</span><span class="sxs-lookup"><span data-stu-id="17850-142">When RequireOutgoing is not set to false, only users that meet the authorization requirement are called from the server.</span></span>

<a id="requireauth"></a>

## <a name="require-authentication-for-all-hubs"></a><span data-ttu-id="17850-143">Vyžadovat ověření pro všechna centra</span><span class="sxs-lookup"><span data-stu-id="17850-143">Require authentication for all hubs</span></span>

<span data-ttu-id="17850-144">Ověřování pro všechny metody centra a centra v aplikaci můžete vyžadovat voláním metody [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) při spuštění aplikace.</span><span class="sxs-lookup"><span data-stu-id="17850-144">You can require authentication for all hubs and hub methods in your application by calling the [RequireAuthentication](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubpipelineextensions.requireauthentication(v=vs.111).aspx) method when the application starts.</span></span> <span data-ttu-id="17850-145">Tuto metodu můžete použít, pokud máte více rozbočovačů a chcete vymáhat požadavek na ověření pro všechny z nich.</span><span class="sxs-lookup"><span data-stu-id="17850-145">You might use this method when you have multiple hubs and want to enforce an authentication requirement for all of them.</span></span> <span data-ttu-id="17850-146">V této metodě nemůžete zadat požadavky na role, uživatele nebo odchozí autorizaci.</span><span class="sxs-lookup"><span data-stu-id="17850-146">With this method, you cannot specify requirements for role, user, or outgoing authorization.</span></span> <span data-ttu-id="17850-147">Můžete zadat jenom přístup k metodám rozbočovače, který je omezený na ověřené uživatele.</span><span class="sxs-lookup"><span data-stu-id="17850-147">You can only specify that access to the hub methods is restricted to authenticated users.</span></span> <span data-ttu-id="17850-148">Přesto však můžete použít atribut autorizovat na centra nebo metody k určení dalších požadavků.</span><span class="sxs-lookup"><span data-stu-id="17850-148">However, you can still apply the Authorize attribute to hubs or methods to specify additional requirements.</span></span> <span data-ttu-id="17850-149">Všechny požadavky, které zadáte v atributu, se přidají do základního požadavku ověřování.</span><span class="sxs-lookup"><span data-stu-id="17850-149">Any requirement you specify in an attribute is added to the basic requirement of authentication.</span></span>

<span data-ttu-id="17850-150">Následující příklad ukazuje spouštěcí soubor, který omezuje všechny metody centra na ověřené uživatele.</span><span class="sxs-lookup"><span data-stu-id="17850-150">The following example shows a Startup file which restricts all hub methods to authenticated users.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample3.cs)]

<span data-ttu-id="17850-151">Pokud zavoláte metodu `RequireAuthentication()` po zpracování žádosti o signál, Signaler vyvolá výjimku `InvalidOperationException`.</span><span class="sxs-lookup"><span data-stu-id="17850-151">If you call the `RequireAuthentication()` method after a SignalR request has been processed, SignalR will throw a `InvalidOperationException` exception.</span></span> <span data-ttu-id="17850-152">Signál vyvolá tuto výjimku, protože po vyvolání kanálu nelze přidat modul do HubPipeline.</span><span class="sxs-lookup"><span data-stu-id="17850-152">SignalR throws this exception because you cannot add a module to the HubPipeline after the pipeline has been invoked.</span></span> <span data-ttu-id="17850-153">Předchozí příklad ukazuje volání metody `RequireAuthentication` v metodě `Configuration`, která je spuštěna jednou před zpracováním prvního požadavku.</span><span class="sxs-lookup"><span data-stu-id="17850-153">The previous example shows calling the `RequireAuthentication` method in the `Configuration` method which is executed one time prior to handling the first request.</span></span>

<a id="custom"></a>

## <a name="customized-authorization"></a><span data-ttu-id="17850-154">Přizpůsobená autorizace</span><span class="sxs-lookup"><span data-stu-id="17850-154">Customized authorization</span></span>

<span data-ttu-id="17850-155">Pokud potřebujete přizpůsobit způsob určování autorizace, můžete vytvořit třídu, která je odvozena z `AuthorizeAttribute` a přepsat metodu [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) .</span><span class="sxs-lookup"><span data-stu-id="17850-155">If you need to customize how authorization is determined, you can create a class that derives from `AuthorizeAttribute` and override the [UserAuthorized](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.authorizeattribute.userauthorized(v=vs.111).aspx) method.</span></span> <span data-ttu-id="17850-156">Pro každý požadavek vyvolá signál tuto metodu k určení, zda je uživatel autorizován k dokončení žádosti.</span><span class="sxs-lookup"><span data-stu-id="17850-156">For each request, SignalR invokes this method to determine whether the user is authorized to complete the request.</span></span> <span data-ttu-id="17850-157">V přepsané metodě zadáte potřebnou logiku pro váš autorizační scénář.</span><span class="sxs-lookup"><span data-stu-id="17850-157">In the overridden method, you provide the necessary logic for your authorization scenario.</span></span> <span data-ttu-id="17850-158">Následující příklad ukazuje, jak vymáhat autorizaci pomocí identity založené na deklaracích identity.</span><span class="sxs-lookup"><span data-stu-id="17850-158">The following example shows how to enforce authorization through claims-based identity.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample4.cs)]

<a id="passauth"></a>

## <a name="pass-authentication-information-to-clients"></a><span data-ttu-id="17850-159">Předání ověřovacích informací klientům</span><span class="sxs-lookup"><span data-stu-id="17850-159">Pass authentication information to clients</span></span>

<span data-ttu-id="17850-160">V kódu, který běží na klientovi, možná budete muset použít ověřovací údaje.</span><span class="sxs-lookup"><span data-stu-id="17850-160">You may need to use authentication information in the code that runs on the client.</span></span> <span data-ttu-id="17850-161">Požadované informace předáte při volání metod na klientovi.</span><span class="sxs-lookup"><span data-stu-id="17850-161">You pass the required information when calling the methods on the client.</span></span> <span data-ttu-id="17850-162">Například metoda aplikace Chat může předat jako parametr uživatelské jméno osoby, která odesílá zprávu, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="17850-162">For example, a chat application method could pass as a parameter the user name of the person posting a message, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample5.cs)]

<span data-ttu-id="17850-163">Nebo můžete vytvořit objekt, který představuje ověřovací informace a předat tento objekt jako parametr, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="17850-163">Or, you can create an object to represent the authentication information and pass that object as a parameter, as shown below.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample6.cs)]

<span data-ttu-id="17850-164">Nikdy byste neměli předat ID připojení jednoho klienta jiným klientům, protože ho uživatel se zlými úmysly mohl použít k napodobení žádosti od tohoto klienta.</span><span class="sxs-lookup"><span data-stu-id="17850-164">You should never pass one client's connection id to other clients, as a malicious user could use it to mimic a request from that client.</span></span>

<a id="authoptions"></a>

## <a name="authentication-options-for-net-clients"></a><span data-ttu-id="17850-165">Možnosti ověřování pro klienty rozhraní .NET</span><span class="sxs-lookup"><span data-stu-id="17850-165">Authentication options for .NET clients</span></span>

<span data-ttu-id="17850-166">Pokud máte klienta .NET, například konzolovou aplikaci, která komunikuje s centrem, které je omezené na ověřené uživatele, můžete přihlašovací údaje pro ověřování předat v souboru cookie, v záhlaví připojení nebo v certifikátu.</span><span class="sxs-lookup"><span data-stu-id="17850-166">When you have a .NET client, such as a console app, which interacts with a hub that is limited to authenticated users, you can pass the authentication credentials in a cookie, the connection header, or a certificate.</span></span> <span data-ttu-id="17850-167">Příklady v této části ukazují, jak používat tyto různé metody ověřování uživatele.</span><span class="sxs-lookup"><span data-stu-id="17850-167">The examples in this section show how to use those different methods for authenticating a user.</span></span> <span data-ttu-id="17850-168">Nejedná se o plně funkční signalizaci aplikací.</span><span class="sxs-lookup"><span data-stu-id="17850-168">They are not fully-functional SignalR apps.</span></span> <span data-ttu-id="17850-169">Další informace o klientech rozhraní .NET s nástrojem Signal najdete v tématu [Průvodce rozhraním API pro centra – klient .NET](../guide-to-the-api/hubs-api-guide-net-client.md).</span><span class="sxs-lookup"><span data-stu-id="17850-169">For more information about .NET clients with SignalR, see [Hubs API Guide - .NET Client](../guide-to-the-api/hubs-api-guide-net-client.md).</span></span>

<a id="cookie"></a>

### <a name="cookie"></a><span data-ttu-id="17850-170">Soubor cookie</span><span class="sxs-lookup"><span data-stu-id="17850-170">Cookie</span></span>

<span data-ttu-id="17850-171">Když klient .NET komunikuje s centrem, které používá ověřování pomocí formulářů ASP.NET, budete muset ručně nastavit ověřovací soubor cookie pro připojení.</span><span class="sxs-lookup"><span data-stu-id="17850-171">When your .NET client interacts with a hub that uses ASP.NET Forms Authentication, you will need to manually set the authentication cookie on the connection.</span></span> <span data-ttu-id="17850-172">Soubor cookie přidáte do vlastnosti `CookieContainer` v objektu [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) .</span><span class="sxs-lookup"><span data-stu-id="17850-172">You add the cookie to the `CookieContainer` property on the [HubConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.hubs.hubconnection(v=vs.111).aspx) object.</span></span> <span data-ttu-id="17850-173">Následující příklad ukazuje konzolovou aplikaci, která načte ověřovací soubor cookie z webové stránky a přidá tento soubor cookie k připojení.</span><span class="sxs-lookup"><span data-stu-id="17850-173">The following example shows a console app that retrieves an authentication cookie from a web page and adds that cookie to the connection.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample7.cs)]

<span data-ttu-id="17850-174">Aplikace konzoly odesílá pověření do <strong>www.contoso.com/RemoteLogin</strong> , která by mohla odkazovat na prázdnou stránku, která obsahuje následující soubor kódu na pozadí.</span><span class="sxs-lookup"><span data-stu-id="17850-174">The console app posts the credentials to <strong>www.contoso.com/RemoteLogin</strong> which could refer to an empty page that contains the following code-behind file.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample8.cs)]

<a id="windows"></a>

### <a name="windows-authentication"></a><span data-ttu-id="17850-175">Ověřování systému Windows</span><span class="sxs-lookup"><span data-stu-id="17850-175">Windows authentication</span></span>

<span data-ttu-id="17850-176">Při použití ověřování systému Windows můžete přihlašovací údaje aktuálního uživatele předat pomocí vlastnosti [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) .</span><span class="sxs-lookup"><span data-stu-id="17850-176">When using Windows authentication, you can pass the current user's credentials by using the [DefaultCredentials](https://msdn.microsoft.com/library/system.net.credentialcache.defaultcredentials.aspx) property.</span></span> <span data-ttu-id="17850-177">Přihlašovací údaje pro připojení nastavíte na hodnotu DefaultCredentials.</span><span class="sxs-lookup"><span data-stu-id="17850-177">You set the credentials for the connection to the value of the DefaultCredentials.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample9.cs?highlight=6)]

<a id="header"></a>

### <a name="connection-header"></a><span data-ttu-id="17850-178">Záhlaví připojení</span><span class="sxs-lookup"><span data-stu-id="17850-178">Connection header</span></span>

<span data-ttu-id="17850-179">Pokud vaše aplikace nepoužívá soubory cookie, můžete informace o uživateli předat v hlavičce připojení.</span><span class="sxs-lookup"><span data-stu-id="17850-179">If your application is not using cookies, you can pass user information in the connection header.</span></span> <span data-ttu-id="17850-180">Například můžete předat token v hlavičce připojení.</span><span class="sxs-lookup"><span data-stu-id="17850-180">For example, you can pass a token in the connection header.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample10.cs?highlight=6)]

<span data-ttu-id="17850-181">Potom můžete v centru ověřit token uživatele.</span><span class="sxs-lookup"><span data-stu-id="17850-181">Then, in the hub, you would verify the user's token.</span></span>

<a id="certificate"></a>

### <a name="certificate"></a><span data-ttu-id="17850-182">Certifikát</span><span class="sxs-lookup"><span data-stu-id="17850-182">Certificate</span></span>

<span data-ttu-id="17850-183">Můžete předat klientský certifikát a ověřit uživatele.</span><span class="sxs-lookup"><span data-stu-id="17850-183">You can pass a client certificate to verify the user.</span></span> <span data-ttu-id="17850-184">Certifikát se přidává při vytváření připojení.</span><span class="sxs-lookup"><span data-stu-id="17850-184">You add the certificate when creating the connection.</span></span> <span data-ttu-id="17850-185">Následující příklad ukazuje pouze postup přidání klientského certifikátu k připojení; nezobrazuje úplnou konzolovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="17850-185">The following example shows only how to add a client certificate to the connection; it does not show the full console app.</span></span> <span data-ttu-id="17850-186">Používá třídu [certifikátu x509](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) , která poskytuje několik různých způsobů, jak vytvořit certifikát.</span><span class="sxs-lookup"><span data-stu-id="17850-186">It uses the [X509Certificate](https://msdn.microsoft.com/library/system.security.cryptography.x509certificates.x509certificate.aspx) class which provides several different ways to create the certificate.</span></span>

[!code-csharp[Main](hub-authorization/samples/sample11.cs?highlight=6)]

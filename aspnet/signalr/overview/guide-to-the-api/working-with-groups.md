---
uid: signalr/overview/guide-to-the-api/working-with-groups
title: Práce se skupinami v nástroji Signaler | Microsoft Docs
author: bradygaster
description: Toto téma popisuje, jak zachovat informace o členství ve skupinách pomocí rozhraní API centra.
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: cd378ecd-3e9e-4236-b902-65916d85a048
msc.legacyurl: /signalr/overview/guide-to-the-api/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: 46dd952fc4902b37c981a111dfa344dad79bb668
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558581"
---
# <a name="working-with-groups-in-signalr"></a><span data-ttu-id="83d4d-103">Práce se skupinami v knihovně SignalR</span><span class="sxs-lookup"><span data-stu-id="83d4d-103">Working with Groups in SignalR</span></span>

<span data-ttu-id="83d4d-104">autorem [Fletcher](https://github.com/pfletcher), který [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="83d4d-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="83d4d-105">Toto téma popisuje, jak přidat uživatele do skupin a zachovat informace o členství ve skupinách.</span><span class="sxs-lookup"><span data-stu-id="83d4d-105">This topic describes how to add users to groups and persist group membership information.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="83d4d-106">Verze softwaru používané v tomto tématu</span><span class="sxs-lookup"><span data-stu-id="83d4d-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="83d4d-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="83d4d-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="83d4d-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="83d4d-108">.NET 4.5</span></span>
> - <span data-ttu-id="83d4d-109">Signal – verze 2</span><span class="sxs-lookup"><span data-stu-id="83d4d-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="83d4d-110">Předchozí verze tohoto tématu</span><span class="sxs-lookup"><span data-stu-id="83d4d-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="83d4d-111">Informace o dřívějších verzích nástroje Signal najdete v části [Signal – starší verze](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="83d4d-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="83d4d-112">Dotazy a komentáře</span><span class="sxs-lookup"><span data-stu-id="83d4d-112">Questions and comments</span></span>
>
> <span data-ttu-id="83d4d-113">Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="83d4d-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="83d4d-114">Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="83d4d-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="83d4d-115">Přehled</span><span class="sxs-lookup"><span data-stu-id="83d4d-115">Overview</span></span>

<span data-ttu-id="83d4d-116">Skupiny v nástroji Signal poskytují metodu pro vysílání zpráv pro zadané podmnožiny připojených klientů.</span><span class="sxs-lookup"><span data-stu-id="83d4d-116">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="83d4d-117">Skupina může mít libovolný počet klientů a klient může být členem libovolného počtu skupin.</span><span class="sxs-lookup"><span data-stu-id="83d4d-117">A group can have any number of clients, and a client can be a member of any number of groups.</span></span> <span data-ttu-id="83d4d-118">Nemusíte explicitně vytvářet skupiny.</span><span class="sxs-lookup"><span data-stu-id="83d4d-118">You don't have to explicitly create groups.</span></span> <span data-ttu-id="83d4d-119">V důsledku toho se skupina automaticky vytvoří při prvním zadání názvu ve volání skupin. Add a odstraní se, když odeberete Poslední připojení z členství v něm.</span><span class="sxs-lookup"><span data-stu-id="83d4d-119">In effect, a group is automatically created the first time you specify its name in a call to Groups.Add, and it is deleted when you remove the last connection from membership in it.</span></span> <span data-ttu-id="83d4d-120">Úvod k používání skupin najdete v tématu [Správa členství ve skupinách z třídy hub](hubs-api-guide-server.md#groupsfromhub) v průvodci servery rozhraní API centra.</span><span class="sxs-lookup"><span data-stu-id="83d4d-120">For an introduction to using groups, see [How to manage group membership from the Hub class](hubs-api-guide-server.md#groupsfromhub) in the Hubs API - Server Guide.</span></span>

<span data-ttu-id="83d4d-121">Neexistuje žádné rozhraní API pro získání seznamu členství ve skupině nebo seznamu skupin.</span><span class="sxs-lookup"><span data-stu-id="83d4d-121">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="83d4d-122">Signal odesílá zprávy klientům a skupinám na základě modelu Pub/sub a server neudržuje seznamy skupin nebo členství ve skupinách.</span><span class="sxs-lookup"><span data-stu-id="83d4d-122">SignalR sends messages to clients and groups based on a pub/sub model, and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="83d4d-123">To pomáhá maximalizovat škálovatelnost, protože kdykoli přidáte uzel do webové farmy, všechny stavy, které tento signál udržuje, musí být šířeny do nového uzlu.</span><span class="sxs-lookup"><span data-stu-id="83d4d-123">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<span data-ttu-id="83d4d-124">Když přidáte uživatele do skupiny pomocí metody `Groups.Add`, uživatel obdrží zprávy směrované do této skupiny po dobu trvání aktuálního připojení, ale členství uživatele v této skupině není trvale po aktuálním připojení.</span><span class="sxs-lookup"><span data-stu-id="83d4d-124">When you add a user to a group using the `Groups.Add` method, the user receives messages directed to that group for the duration of the current connection, but the user's membership in that group is not persisted beyond the current connection.</span></span> <span data-ttu-id="83d4d-125">Pokud chcete trvale uchovávat informace o skupinách a členství ve skupinách, musíte tato data uložit v úložišti, jako je databáze nebo Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="83d4d-125">If you want to permanently retain information about groups and group membership, you must store that data in a repository such as a database or Azure table storage.</span></span> <span data-ttu-id="83d4d-126">Pak se pokaždé, když se uživatel připojí k vaší aplikaci, načte z úložiště, do kterého uživatel patří, a ručně do těchto skupin přidá tohoto uživatele.</span><span class="sxs-lookup"><span data-stu-id="83d4d-126">Then, each time a user connects to your application, you retrieve from the repository which groups the user belongs to, and manually add that user to those groups.</span></span>

<span data-ttu-id="83d4d-127">Po opětovném připojení po dočasném přerušení se uživatel automaticky znovu připojí k dříve přiřazeným skupinám.</span><span class="sxs-lookup"><span data-stu-id="83d4d-127">When reconnecting after a temporary disruption, the user automatically re-joins the previously-assigned groups.</span></span> <span data-ttu-id="83d4d-128">Automatické opětovné připojení skupiny platí pouze při opětovném připojení, nikoli při vytváření nového připojení.</span><span class="sxs-lookup"><span data-stu-id="83d4d-128">Automatically rejoining a group only applies when reconnecting, not when establishing a new connection.</span></span> <span data-ttu-id="83d4d-129">Z klienta, který obsahuje seznam dříve přiřazených skupin, se předává digitálně podepsaný token.</span><span class="sxs-lookup"><span data-stu-id="83d4d-129">A digitally-signed token is passed from the client that contains the list of previously-assigned groups.</span></span> <span data-ttu-id="83d4d-130">Pokud chcete ověřit, jestli uživatel patří do požadovaných skupin, můžete přepsat výchozí chování.</span><span class="sxs-lookup"><span data-stu-id="83d4d-130">If you want to verify whether the user belongs to the requested groups, you can override the default behavior.</span></span>

<span data-ttu-id="83d4d-131">Toto téma obsahuje následující oddíly:</span><span class="sxs-lookup"><span data-stu-id="83d4d-131">This topic includes the following sections:</span></span>

- [<span data-ttu-id="83d4d-132">Přidávání a odebírání uživatelů</span><span class="sxs-lookup"><span data-stu-id="83d4d-132">Adding and removing users</span></span>](#add)
- [<span data-ttu-id="83d4d-133">Volání členů skupiny</span><span class="sxs-lookup"><span data-stu-id="83d4d-133">Calling members of a group</span></span>](#call)
- [<span data-ttu-id="83d4d-134">Ukládání členství ve skupinách v databázi</span><span class="sxs-lookup"><span data-stu-id="83d4d-134">Storing group membership in a database</span></span>](#storedatabase)
- [<span data-ttu-id="83d4d-135">Ukládání členství ve skupinách ve službě Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="83d4d-135">Storing group membership in Azure table storage</span></span>](#storeazuretable)
- [<span data-ttu-id="83d4d-136">Ověřování členství ve skupině při opětovném připojení</span><span class="sxs-lookup"><span data-stu-id="83d4d-136">Verifying group membership when reconnecting</span></span>](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a><span data-ttu-id="83d4d-137">Přidávání a odebírání uživatelů</span><span class="sxs-lookup"><span data-stu-id="83d4d-137">Adding and removing users</span></span>

<span data-ttu-id="83d4d-138">Chcete-li přidat nebo odebrat uživatele ze skupiny, zavolejte metody [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) nebo [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) a jako parametry předejte ID připojení uživatele a název skupiny.</span><span class="sxs-lookup"><span data-stu-id="83d4d-138">To add or remove users from a group, you call the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) or [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods, and pass in the user's connection id and group's name as parameters.</span></span> <span data-ttu-id="83d4d-139">Po ukončení připojení není nutné ručně odebrat uživatele ze skupiny.</span><span class="sxs-lookup"><span data-stu-id="83d4d-139">You do not need to manually remove a user from a group when the connection ends.</span></span>

<span data-ttu-id="83d4d-140">Následující příklad ukazuje metody `Groups.Add` a `Groups.Remove` použité v metodách hub.</span><span class="sxs-lookup"><span data-stu-id="83d4d-140">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

<span data-ttu-id="83d4d-141">Metody `Groups.Add` a `Groups.Remove` provádějí asynchronně.</span><span class="sxs-lookup"><span data-stu-id="83d4d-141">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span>

<span data-ttu-id="83d4d-142">Chcete-li přidat klienta do skupiny a okamžitě odeslat zprávu klientovi pomocí skupiny, je nutné zajistit, aby byla metoda groups. Add nejprve dokončena.</span><span class="sxs-lookup"><span data-stu-id="83d4d-142">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the Groups.Add method finishes first.</span></span> <span data-ttu-id="83d4d-143">Následující příklady kódu ukazují, jak to provést.</span><span class="sxs-lookup"><span data-stu-id="83d4d-143">The following code examples show how to do that.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

<span data-ttu-id="83d4d-144">Obecně platí, že byste neměli při volání metody `Groups.Remove` zahrnovat `await`, protože ID připojení, které se pokoušíte odebrat, možná nebude k dispozici.</span><span class="sxs-lookup"><span data-stu-id="83d4d-144">In general, you should not include `await` when calling the `Groups.Remove` method because the connection id that you are trying to remove might no longer be available.</span></span> <span data-ttu-id="83d4d-145">V takovém případě je `TaskCanceledException` vyvolána po vypršení časového limitu žádosti. Pokud vaše aplikace musí zajistit, aby byl uživatel odebrán ze skupiny před odesláním zprávy do skupiny, můžete přidat `await` před `Groups.Remove`a pak zachytit výjimku `TaskCanceledException`, která může být vyvolána.</span><span class="sxs-lookup"><span data-stu-id="83d4d-145">In that case, `TaskCanceledException` is thrown after the request times out. If your application must ensure that the user has been removed from the group before sending a message to the group, you can add `await` before `Groups.Remove`, and then catch the `TaskCanceledException` exception that might be thrown.</span></span>

<a id="call"></a>

## <a name="calling-members-of-a-group"></a><span data-ttu-id="83d4d-146">Volání členů skupiny</span><span class="sxs-lookup"><span data-stu-id="83d4d-146">Calling members of a group</span></span>

<span data-ttu-id="83d4d-147">Můžete posílat zprávy všem členům skupiny nebo pouze určeným členům skupiny, jak je znázorněno v následujících příkladech.</span><span class="sxs-lookup"><span data-stu-id="83d4d-147">You can send messages to all of the members of a group or only specified members of the group, as shown in the following examples.</span></span>

- <span data-ttu-id="83d4d-148">**Všichni** připojení klienti v zadané skupině.</span><span class="sxs-lookup"><span data-stu-id="83d4d-148">**All** connected clients in a specified group.</span></span>

    [!code-css[Main](working-with-groups/samples/sample3.css)]
- <span data-ttu-id="83d4d-149">Všechny připojené klienty v zadané skupině **s výjimkou určených klientů**identifikovaných podle ID připojení</span><span class="sxs-lookup"><span data-stu-id="83d4d-149">All connected clients in a specified group **except the specified clients**, identified by connection ID.</span></span>

    [!code-csharp[Main](working-with-groups/samples/sample4.cs)]
- <span data-ttu-id="83d4d-150">Všichni připojení klienti v zadané skupině **s výjimkou volajícího klienta**.</span><span class="sxs-lookup"><span data-stu-id="83d4d-150">All connected clients in a specified group **except the calling client**.</span></span>

    [!code-css[Main](working-with-groups/samples/sample5.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a><span data-ttu-id="83d4d-151">Ukládání členství ve skupinách v databázi</span><span class="sxs-lookup"><span data-stu-id="83d4d-151">Storing group membership in a database</span></span>

<span data-ttu-id="83d4d-152">Následující příklady ukazují, jak uchovávat informace o skupinách a uživatelích v databázi.</span><span class="sxs-lookup"><span data-stu-id="83d4d-152">The following examples show how to retain group and user information in a database.</span></span> <span data-ttu-id="83d4d-153">Můžete použít libovolnou technologii pro přístup k datům; Následující příklad však ukazuje, jak definovat modely pomocí Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="83d4d-153">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="83d4d-154">Tyto modely entit odpovídají tabulkám a polím databáze.</span><span class="sxs-lookup"><span data-stu-id="83d4d-154">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="83d4d-155">Vaše datová struktura se může značně lišit v závislosti na požadavcích vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="83d4d-155">Your data structure could vary considerably depending on the requirements of your application.</span></span> <span data-ttu-id="83d4d-156">Tento příklad obsahuje třídu s názvem `ConversationRoom`, která by byla jedinečná pro aplikaci, která umožňuje uživatelům připojit se ke konverzaci o různých předmětech, jako je například sportovní nebo zahradnické.</span><span class="sxs-lookup"><span data-stu-id="83d4d-156">This example includes a class named `ConversationRoom` which would be unique to an application that enables users to join conversations about different subjects, such as sports or gardening.</span></span> <span data-ttu-id="83d4d-157">Tento příklad také obsahuje třídu pro připojení.</span><span class="sxs-lookup"><span data-stu-id="83d4d-157">This example also includes a class for the connections.</span></span> <span data-ttu-id="83d4d-158">Třída Connection není bezpodmínečně nutná pro sledování členství ve skupině, ale je často součástí robustního řešení pro sledování uživatelů.</span><span class="sxs-lookup"><span data-stu-id="83d4d-158">The connection class is not absolutely required for tracking group membership but is frequently part of robust solution to tracking users.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample6.cs)]

<span data-ttu-id="83d4d-159">Pak můžete v centru získat informace o skupině a uživateli z databáze a ručně přidat uživatele do příslušných skupin.</span><span class="sxs-lookup"><span data-stu-id="83d4d-159">Then, in the hub, you can retrieve the group and user information from the database and manually add the user to the appropriate groups.</span></span> <span data-ttu-id="83d4d-160">Příklad nezahrnuje kód pro sledování připojení uživatelů.</span><span class="sxs-lookup"><span data-stu-id="83d4d-160">The example does not include code for tracking the user connections.</span></span> <span data-ttu-id="83d4d-161">V tomto příkladu není klíčové slovo `await` použito před `Groups.Add`, protože zpráva není odeslána přímo do členů skupiny.</span><span class="sxs-lookup"><span data-stu-id="83d4d-161">In this example, the `await` keyword is not applied before `Groups.Add` because a message is not immediately sent to members of the group.</span></span> <span data-ttu-id="83d4d-162">Pokud chcete všem členům skupiny poslat zprávu hned po přidání nového člena, budete chtít použít klíčové slovo `await`, abyste se ujistili, že se asynchronní operace dokončila.</span><span class="sxs-lookup"><span data-stu-id="83d4d-162">If you want to send a message to all members of the group immediately after adding the new member, you would want to apply the `await` keyword to make sure the asynchronous operation has completed.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a><span data-ttu-id="83d4d-163">Ukládání členství ve skupinách ve službě Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="83d4d-163">Storing group membership in Azure table storage</span></span>

<span data-ttu-id="83d4d-164">Použití úložiště tabulek v Azure k ukládání informací o skupině a uživateli se podobá použití databáze.</span><span class="sxs-lookup"><span data-stu-id="83d4d-164">Using Azure table storage to store group and user information is similar to using a database.</span></span> <span data-ttu-id="83d4d-165">Následující příklad ukazuje entitu tabulky, která ukládá uživatelské jméno a název skupiny.</span><span class="sxs-lookup"><span data-stu-id="83d4d-165">The following example shows a table entity that stores the user name and group name.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<span data-ttu-id="83d4d-166">V centru načtěte přiřazené skupiny při připojení uživatele.</span><span class="sxs-lookup"><span data-stu-id="83d4d-166">In the hub, you retrieve the assigned groups when the user connects.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a><span data-ttu-id="83d4d-167">Ověřování členství ve skupině při opětovném připojení</span><span class="sxs-lookup"><span data-stu-id="83d4d-167">Verifying group membership when reconnecting</span></span>

<span data-ttu-id="83d4d-168">Ve výchozím nastavení Signal automaticky znovu přiřadí uživatele do příslušných skupin při opětovném připojení k dočasnému přerušení, například při přerušení připojení a opětovném navázání před vypršením časového limitu připojení. Informace o skupině uživatele se při opětovném připojení předávají do tokenu a tento token se ověří na serveru.</span><span class="sxs-lookup"><span data-stu-id="83d4d-168">By default, SignalR automatically re-assigns a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. The user's group information is passed in a token when reconnecting, and that token is verified on the server.</span></span> <span data-ttu-id="83d4d-169">Informace o procesu ověřování pro opětovné připojení uživatelů ke skupinám najdete v tématu opětovné připojení [skupin při opětovném připojení](../security/introduction-to-security.md#rejoingroup).</span><span class="sxs-lookup"><span data-stu-id="83d4d-169">For information about the verification process for rejoining users to groups, see [Rejoining groups when reconnecting](../security/introduction-to-security.md#rejoingroup).</span></span>

<span data-ttu-id="83d4d-170">Obecně platí, že při opětovném připojení byste měli použít výchozí chování automaticky znovu připojit skupiny.</span><span class="sxs-lookup"><span data-stu-id="83d4d-170">In general, you should use the default behavior of automatically rejoining groups on reconnect.</span></span> <span data-ttu-id="83d4d-171">Skupiny signalizace nejsou určeny jako mechanismus zabezpečení pro omezení přístupu k citlivým datům.</span><span class="sxs-lookup"><span data-stu-id="83d4d-171">SignalR groups are not intended as a security mechanism for restricting access to sensitive data.</span></span> <span data-ttu-id="83d4d-172">Pokud ale vaše aplikace musí při opětovném připojení dvakrát ověřit členství uživatele ve skupině, můžete výchozí chování přepsat.</span><span class="sxs-lookup"><span data-stu-id="83d4d-172">However, if your application must double-check a user's group membership when reconnecting, you can override the default behavior.</span></span> <span data-ttu-id="83d4d-173">Změna výchozího chování může do databáze přidat zatížení, protože členství uživatele ve skupině musí být načteno pro každé opětovné připojení, nikoli pouze při připojení uživatele.</span><span class="sxs-lookup"><span data-stu-id="83d4d-173">Changing the default behavior can add a burden to your database because a user's group membership must be retrieved for each reconnection rather than just when the user connects.</span></span>

<span data-ttu-id="83d4d-174">Pokud je nutné ověřit členství ve skupině při opětovném připojení, vytvořte nový modul kanálu rozbočovače, který vrátí seznam přiřazených skupin, jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="83d4d-174">If you must verify group membership on reconnect, create a new hub pipeline module that returns a list of assigned groups, as shown below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<span data-ttu-id="83d4d-175">Pak tento modul přidejte do kanálu rozbočovače, jak je zvýrazněno níže.</span><span class="sxs-lookup"><span data-stu-id="83d4d-175">Then, add that module to the hub pipeline, as highlighted below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample11.cs?highlight=4)]

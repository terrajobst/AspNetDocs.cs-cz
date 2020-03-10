---
uid: signalr/overview/older-versions/working-with-groups
title: Práce se skupinami v nástroji Signal 1. x | Microsoft Docs
author: bradygaster
description: Toto téma popisuje, jak zachovat informace o členství ve skupinách pomocí rozhraní API centra.
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: 22929efd-68c9-4609-b76d-f8ba42fda01e
msc.legacyurl: /signalr/overview/older-versions/working-with-groups
msc.type: authoredcontent
ms.openlocfilehash: 5f50dc162d6cdcfbf2261e6a751f5f99078d5c54
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579364"
---
# <a name="working-with-groups-in-signalr-1x"></a><span data-ttu-id="35ade-103">Práce se skupinami v knihovně SignalR 1.x</span><span class="sxs-lookup"><span data-stu-id="35ade-103">Working with Groups in SignalR 1.x</span></span>

<span data-ttu-id="35ade-104">autorem [Fletcher](https://github.com/pfletcher), který [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="35ade-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="35ade-105">Toto téma popisuje, jak přidat uživatele do skupin a zachovat informace o členství ve skupinách.</span><span class="sxs-lookup"><span data-stu-id="35ade-105">This topic describes how to add users to groups and persist group membership information.</span></span>

## <a name="overview"></a><span data-ttu-id="35ade-106">Přehled</span><span class="sxs-lookup"><span data-stu-id="35ade-106">Overview</span></span>

<span data-ttu-id="35ade-107">Skupiny v nástroji Signal poskytují metodu pro vysílání zpráv pro zadané podmnožiny připojených klientů.</span><span class="sxs-lookup"><span data-stu-id="35ade-107">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="35ade-108">Skupina může mít libovolný počet klientů a klient může být členem libovolného počtu skupin.</span><span class="sxs-lookup"><span data-stu-id="35ade-108">A group can have any number of clients, and a client can be a member of any number of groups.</span></span> <span data-ttu-id="35ade-109">Nemusíte explicitně vytvářet skupiny.</span><span class="sxs-lookup"><span data-stu-id="35ade-109">You don't have to explicitly create groups.</span></span> <span data-ttu-id="35ade-110">V důsledku toho se skupina automaticky vytvoří při prvním zadání názvu ve volání skupin. Add a odstraní se, když odeberete Poslední připojení z členství v něm.</span><span class="sxs-lookup"><span data-stu-id="35ade-110">In effect, a group is automatically created the first time you specify its name in a call to Groups.Add, and it is deleted when you remove the last connection from membership in it.</span></span> <span data-ttu-id="35ade-111">Úvod k používání skupin najdete v tématu [Správa členství ve skupinách z třídy hub](index.md) v průvodci servery rozhraní API centra.</span><span class="sxs-lookup"><span data-stu-id="35ade-111">For an introduction to using groups, see [How to manage group membership from the Hub class](index.md) in the Hubs API - Server Guide.</span></span>

<span data-ttu-id="35ade-112">Neexistuje žádné rozhraní API pro získání seznamu členství ve skupině nebo seznamu skupin.</span><span class="sxs-lookup"><span data-stu-id="35ade-112">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="35ade-113">Signal odesílá zprávy klientům a skupinám na základě modelu Pub/sub a server neudržuje seznamy skupin nebo členství ve skupinách.</span><span class="sxs-lookup"><span data-stu-id="35ade-113">SignalR sends messages to clients and groups based on a pub/sub model, and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="35ade-114">To pomáhá maximalizovat škálovatelnost, protože kdykoli přidáte uzel do webové farmy, všechny stavy, které tento signál udržuje, musí být šířeny do nového uzlu.</span><span class="sxs-lookup"><span data-stu-id="35ade-114">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<span data-ttu-id="35ade-115">Když přidáte uživatele do skupiny pomocí metody `Groups.Add`, uživatel obdrží zprávy směrované do této skupiny po dobu trvání aktuálního připojení, ale členství uživatele v této skupině není trvale po aktuálním připojení.</span><span class="sxs-lookup"><span data-stu-id="35ade-115">When you add a user to a group using the `Groups.Add` method, the user receives messages directed to that group for the duration of the current connection, but the user's membership in that group is not persisted beyond the current connection.</span></span> <span data-ttu-id="35ade-116">Pokud chcete trvale uchovávat informace o skupinách a členství ve skupinách, musíte tato data uložit v úložišti, jako je databáze nebo Azure Table Storage.</span><span class="sxs-lookup"><span data-stu-id="35ade-116">If you want to permanently retain information about groups and group membership, you must store that data in a repository such as a database or Azure table storage.</span></span> <span data-ttu-id="35ade-117">Pak se pokaždé, když se uživatel připojí k vaší aplikaci, načte z úložiště, do kterého uživatel patří, a ručně do těchto skupin přidá tohoto uživatele.</span><span class="sxs-lookup"><span data-stu-id="35ade-117">Then, each time a user connects to your application, you retrieve from the repository which groups the user belongs to, and manually add that user to those groups.</span></span>

<span data-ttu-id="35ade-118">Po opětovném připojení po dočasném přerušení se uživatel automaticky znovu připojí k dříve přiřazeným skupinám.</span><span class="sxs-lookup"><span data-stu-id="35ade-118">When reconnecting after a temporary disruption, the user automatically re-joins the previously-assigned groups.</span></span> <span data-ttu-id="35ade-119">Automatické opětovné připojení skupiny platí pouze při opětovném připojení, nikoli při vytváření nového připojení.</span><span class="sxs-lookup"><span data-stu-id="35ade-119">Automatically rejoining a group only applies when reconnecting, not when establishing a new connection.</span></span> <span data-ttu-id="35ade-120">Z klienta, který obsahuje seznam dříve přiřazených skupin, se předává digitálně podepsaný token.</span><span class="sxs-lookup"><span data-stu-id="35ade-120">A digitally-signed token is passed from the client that contains the list of previously-assigned groups.</span></span> <span data-ttu-id="35ade-121">Pokud chcete ověřit, jestli uživatel patří do požadovaných skupin, můžete přepsat výchozí chování.</span><span class="sxs-lookup"><span data-stu-id="35ade-121">If you want to verify whether the user belongs to the requested groups, you can override the default behavior.</span></span>

<span data-ttu-id="35ade-122">Toto téma obsahuje následující oddíly:</span><span class="sxs-lookup"><span data-stu-id="35ade-122">This topic includes the following sections:</span></span>

- [<span data-ttu-id="35ade-123">Přidávání a odebírání uživatelů</span><span class="sxs-lookup"><span data-stu-id="35ade-123">Adding and removing users</span></span>](#add)
- [<span data-ttu-id="35ade-124">Volání členů skupiny</span><span class="sxs-lookup"><span data-stu-id="35ade-124">Calling members of a group</span></span>](#call)
- [<span data-ttu-id="35ade-125">Ukládání členství ve skupinách v databázi</span><span class="sxs-lookup"><span data-stu-id="35ade-125">Storing group membership in a database</span></span>](#storedatabase)
- [<span data-ttu-id="35ade-126">Ukládání členství ve skupinách ve službě Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="35ade-126">Storing group membership in Azure table storage</span></span>](#storeazuretable)
- [<span data-ttu-id="35ade-127">Ověřování členství ve skupině při opětovném připojení</span><span class="sxs-lookup"><span data-stu-id="35ade-127">Verifying group membership when reconnecting</span></span>](#verify)

<a id="add"></a>

## <a name="adding-and-removing-users"></a><span data-ttu-id="35ade-128">Přidávání a odebírání uživatelů</span><span class="sxs-lookup"><span data-stu-id="35ade-128">Adding and removing users</span></span>

<span data-ttu-id="35ade-129">Chcete-li přidat nebo odebrat uživatele ze skupiny, zavolejte metody [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) nebo [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) a jako parametry předejte ID připojení uživatele a název skupiny.</span><span class="sxs-lookup"><span data-stu-id="35ade-129">To add or remove users from a group, you call the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) or [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods, and pass in the user's connection id and group's name as parameters.</span></span> <span data-ttu-id="35ade-130">Po ukončení připojení není nutné ručně odebrat uživatele ze skupiny.</span><span class="sxs-lookup"><span data-stu-id="35ade-130">You do not need to manually remove a user from a group when the connection ends.</span></span>

<span data-ttu-id="35ade-131">Následující příklad ukazuje metody `Groups.Add` a `Groups.Remove` použité v metodách hub.</span><span class="sxs-lookup"><span data-stu-id="35ade-131">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample1.cs?highlight=5,10)]

<span data-ttu-id="35ade-132">Metody `Groups.Add` a `Groups.Remove` provádějí asynchronně.</span><span class="sxs-lookup"><span data-stu-id="35ade-132">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span>

<span data-ttu-id="35ade-133">Chcete-li přidat klienta do skupiny a okamžitě odeslat zprávu klientovi pomocí skupiny, je nutné zajistit, aby byla metoda groups. Add nejprve dokončena.</span><span class="sxs-lookup"><span data-stu-id="35ade-133">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the Groups.Add method finishes first.</span></span> <span data-ttu-id="35ade-134">Následující příklady kódu ukazují, jak to provést, pomocí kódu, který funguje v rozhraní .NET 4,5 a jeden pomocí kódu, který funguje v rozhraní .NET 4.</span><span class="sxs-lookup"><span data-stu-id="35ade-134">The following code examples show how to do that, one by using code that works in .NET 4.5, and one by using code that works in .NET 4.</span></span>

#### <a name="asynchronous-net-45-example"></a><span data-ttu-id="35ade-135">Příklad asynchronního rozhraní .NET 4,5</span><span class="sxs-lookup"><span data-stu-id="35ade-135">Asynchronous .NET 4.5 Example</span></span>

[!code-csharp[Main](working-with-groups/samples/sample2.cs?highlight=1,3)]

#### <a name="asynchronous-net-4-example"></a><span data-ttu-id="35ade-136">Příklad asynchronního rozhraní .NET 4</span><span class="sxs-lookup"><span data-stu-id="35ade-136">Asynchronous .NET 4 Example</span></span>

[!code-csharp[Main](working-with-groups/samples/sample3.cs?highlight=3-4)]

<span data-ttu-id="35ade-137">Obecně platí, že byste neměli při volání metody `Groups.Remove` zahrnovat `await`, protože ID připojení, které se pokoušíte odebrat, možná nebude k dispozici.</span><span class="sxs-lookup"><span data-stu-id="35ade-137">In general, you should not include `await` when calling the `Groups.Remove` method because the connection id that you are trying to remove might no longer be available.</span></span> <span data-ttu-id="35ade-138">V takovém případě je `TaskCanceledException` vyvolána po vypršení časového limitu žádosti. Pokud vaše aplikace musí zajistit, aby byl uživatel ze skupiny odebraný před odesláním zprávy do skupiny, můžete přidat `await` před skupiny. odeberte a pak Zachyťte výjimku `TaskCanceledException`, která může být vyvolána.</span><span class="sxs-lookup"><span data-stu-id="35ade-138">In that case, `TaskCanceledException` is thrown after the request times out. If your application must ensure that the user has been removed from the group before sending a message to the group, you can add `await` before Groups.Remove, and then catch the `TaskCanceledException` exception that might be thrown.</span></span>

<a id="call"></a>

## <a name="calling-members-of-a-group"></a><span data-ttu-id="35ade-139">Volání členů skupiny</span><span class="sxs-lookup"><span data-stu-id="35ade-139">Calling members of a group</span></span>

<span data-ttu-id="35ade-140">Můžete posílat zprávy všem členům skupiny nebo pouze určeným členům skupiny, jak je znázorněno v následujících příkladech.</span><span class="sxs-lookup"><span data-stu-id="35ade-140">You can send messages to all of the members of a group or only specified members of the group, as shown in the following examples.</span></span>

- <span data-ttu-id="35ade-141">**Všichni** připojení klienti v zadané skupině.</span><span class="sxs-lookup"><span data-stu-id="35ade-141">**All** connected clients in a specified group.</span></span> 

    [!code-css[Main](working-with-groups/samples/sample4.css)]
- <span data-ttu-id="35ade-142">Všechny připojené klienty v zadané skupině **s výjimkou určených klientů**identifikovaných podle ID připojení</span><span class="sxs-lookup"><span data-stu-id="35ade-142">All connected clients in a specified group **except the specified clients**, identified by connection ID.</span></span> 

    [!code-csharp[Main](working-with-groups/samples/sample5.cs)]
- <span data-ttu-id="35ade-143">Všichni připojení klienti v zadané skupině **s výjimkou volajícího klienta**.</span><span class="sxs-lookup"><span data-stu-id="35ade-143">All connected clients in a specified group **except the calling client**.</span></span> 

    [!code-css[Main](working-with-groups/samples/sample6.css)]

<a id="storedatabase"></a>

## <a name="storing-group-membership-in-a-database"></a><span data-ttu-id="35ade-144">Ukládání členství ve skupinách v databázi</span><span class="sxs-lookup"><span data-stu-id="35ade-144">Storing group membership in a database</span></span>

<span data-ttu-id="35ade-145">Následující příklady ukazují, jak uchovávat informace o skupinách a uživatelích v databázi.</span><span class="sxs-lookup"><span data-stu-id="35ade-145">The following examples show how to retain group and user information in a database.</span></span> <span data-ttu-id="35ade-146">Můžete použít libovolnou technologii pro přístup k datům; Následující příklad však ukazuje, jak definovat modely pomocí Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="35ade-146">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="35ade-147">Tyto modely entit odpovídají tabulkám a polím databáze.</span><span class="sxs-lookup"><span data-stu-id="35ade-147">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="35ade-148">Vaše datová struktura se může značně lišit v závislosti na požadavcích vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="35ade-148">Your data structure could vary considerably depending on the requirements of your application.</span></span> <span data-ttu-id="35ade-149">Tento příklad obsahuje třídu s názvem `ConversationRoom`, která by byla jedinečná pro aplikaci, která umožňuje uživatelům připojit se ke konverzaci o různých předmětech, jako je například sportovní nebo zahradnické.</span><span class="sxs-lookup"><span data-stu-id="35ade-149">This example includes a class named `ConversationRoom` which would be unique to an application that enables users to join conversations about different subjects, such as sports or gardening.</span></span> <span data-ttu-id="35ade-150">Tento příklad také obsahuje třídu pro připojení.</span><span class="sxs-lookup"><span data-stu-id="35ade-150">This example also includes a class for the connections.</span></span> <span data-ttu-id="35ade-151">Třída Connection není bezpodmínečně nutná pro sledování členství ve skupině, ale je často součástí robustního řešení pro sledování uživatelů.</span><span class="sxs-lookup"><span data-stu-id="35ade-151">The connection class is not absolutely required for tracking group membership but is frequently part of robust solution to tracking users.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample7.cs)]

<span data-ttu-id="35ade-152">Pak můžete v centru získat informace o skupině a uživateli z databáze a ručně přidat uživatele do příslušných skupin.</span><span class="sxs-lookup"><span data-stu-id="35ade-152">Then, in the hub, you can retrieve the group and user information from the database and manually add the user to the appropriate groups.</span></span> <span data-ttu-id="35ade-153">Příklad nezahrnuje kód pro sledování připojení uživatelů.</span><span class="sxs-lookup"><span data-stu-id="35ade-153">The example does not include code for tracking the user connections.</span></span> <span data-ttu-id="35ade-154">V tomto příkladu není klíčové slovo `await` použito před `Groups.Add`, protože zpráva není odeslána přímo do členů skupiny.</span><span class="sxs-lookup"><span data-stu-id="35ade-154">In this example, the `await` keyword is not applied before `Groups.Add` because a message is not immediately sent to members of the group.</span></span> <span data-ttu-id="35ade-155">Pokud chcete všem členům skupiny poslat zprávu hned po přidání nového člena, budete chtít použít klíčové slovo `await`, abyste se ujistili, že se asynchronní operace dokončila.</span><span class="sxs-lookup"><span data-stu-id="35ade-155">If you want to send a message to all members of the group immediately after adding the new member, you would want to apply the `await` keyword to make sure the asynchronous operation has completed.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample8.cs)]

<a id="storeazuretable"></a>

## <a name="storing-group-membership-in-azure-table-storage"></a><span data-ttu-id="35ade-156">Ukládání členství ve skupinách ve službě Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="35ade-156">Storing group membership in Azure table storage</span></span>

<span data-ttu-id="35ade-157">Použití úložiště tabulek v Azure k ukládání informací o skupině a uživateli se podobá použití databáze.</span><span class="sxs-lookup"><span data-stu-id="35ade-157">Using Azure table storage to store group and user information is similar to using a database.</span></span> <span data-ttu-id="35ade-158">Následující příklad ukazuje entitu tabulky, která ukládá uživatelské jméno a název skupiny.</span><span class="sxs-lookup"><span data-stu-id="35ade-158">The following example shows a table entity that stores the user name and group name.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample9.cs)]

<span data-ttu-id="35ade-159">V centru načtěte přiřazené skupiny při připojení uživatele.</span><span class="sxs-lookup"><span data-stu-id="35ade-159">In the hub, you retrieve the assigned groups when the user connects.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample10.cs)]

<a id="verify"></a>

## <a name="verifying-group-membership-when-reconnecting"></a><span data-ttu-id="35ade-160">Ověřování členství ve skupině při opětovném připojení</span><span class="sxs-lookup"><span data-stu-id="35ade-160">Verifying group membership when reconnecting</span></span>

<span data-ttu-id="35ade-161">Ve výchozím nastavení Signal automaticky znovu přiřadí uživatele do příslušných skupin při opětovném připojení k dočasnému přerušení, například při přerušení připojení a opětovném navázání před vypršením časového limitu připojení. Informace o skupině uživatele se při opětovném připojení předávají do tokenu a tento token se ověří na serveru.</span><span class="sxs-lookup"><span data-stu-id="35ade-161">By default, SignalR automatically re-assigns a user to the appropriate groups when reconnecting from a temporary disruption, such as when a connection is dropped and re-established before the connection times out. The user's group information is passed in a token when reconnecting, and that token is verified on the server.</span></span> <span data-ttu-id="35ade-162">Informace o procesu ověřování pro opětovné připojení uživatelů ke skupinám najdete v tématu opětovné připojení [skupin při opětovném připojení](index.md).</span><span class="sxs-lookup"><span data-stu-id="35ade-162">For information about the verification process for rejoining users to groups, see [Rejoining groups when reconnecting](index.md).</span></span>

<span data-ttu-id="35ade-163">Obecně platí, že při opětovném připojení byste měli použít výchozí chování automaticky znovu připojit skupiny.</span><span class="sxs-lookup"><span data-stu-id="35ade-163">In general, you should use the default behavior of automatically rejoining groups on reconnect.</span></span> <span data-ttu-id="35ade-164">Skupiny signalizace nejsou určeny jako mechanismus zabezpečení pro omezení přístupu k citlivým datům.</span><span class="sxs-lookup"><span data-stu-id="35ade-164">SignalR groups are not intended as a security mechanism for restricting access to sensitive data.</span></span> <span data-ttu-id="35ade-165">Pokud ale vaše aplikace musí při opětovném připojení dvakrát ověřit členství uživatele ve skupině, můžete výchozí chování přepsat.</span><span class="sxs-lookup"><span data-stu-id="35ade-165">However, if your application must double-check a user's group membership when reconnecting, you can override the default behavior.</span></span> <span data-ttu-id="35ade-166">Změna výchozího chování může do databáze přidat zatížení, protože členství uživatele ve skupině musí být načteno pro každé opětovné připojení, nikoli pouze při připojení uživatele.</span><span class="sxs-lookup"><span data-stu-id="35ade-166">Changing the default behavior can add a burden to your database because a user's group membership must be retrieved for each reconnection rather than just when the user connects.</span></span>

<span data-ttu-id="35ade-167">Pokud je nutné ověřit členství ve skupině při opětovném připojení, vytvořte nový modul kanálu rozbočovače, který vrátí seznam přiřazených skupin, jak je uvedeno níže.</span><span class="sxs-lookup"><span data-stu-id="35ade-167">If you must verify group membership on reconnect, create a new hub pipeline module that returns a list of assigned groups, as shown below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample11.cs)]

<span data-ttu-id="35ade-168">Pak tento modul přidejte do kanálu rozbočovače, jak je zvýrazněno níže.</span><span class="sxs-lookup"><span data-stu-id="35ade-168">Then, add that module to the hub pipeline, as highlighted below.</span></span>

[!code-csharp[Main](working-with-groups/samples/sample12.cs?highlight=10)]

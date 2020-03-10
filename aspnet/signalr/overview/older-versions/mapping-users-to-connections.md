---
uid: signalr/overview/older-versions/mapping-users-to-connections
title: Mapování uživatelů signalizace na připojení v nástroji Signal 1. x | Microsoft Docs
author: bradygaster
description: V tomto tématu se dozvíte, jak uchovávat informace o uživatelích a jejich připojeních.
ms.author: bradyg
ms.date: 10/17/2013
ms.assetid: ebbc93a8-e6c4-4122-8e0d-3aa42293c747
msc.legacyurl: /signalr/overview/older-versions/mapping-users-to-connections
msc.type: authoredcontent
ms.openlocfilehash: 9d948495e9b8821fcb465611b6926603c3756a19
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558483"
---
# <a name="mapping-signalr-users-to-connections-in-signalr-1x"></a><span data-ttu-id="c175d-103">Mapování uživatelů knihovny SignalR na připojení v SignalR 1.x</span><span class="sxs-lookup"><span data-stu-id="c175d-103">Mapping SignalR Users to Connections in SignalR 1.x</span></span>

<span data-ttu-id="c175d-104">autorem [Fletcher](https://github.com/pfletcher), který [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="c175d-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="c175d-105">V tomto tématu se dozvíte, jak uchovávat informace o uživatelích a jejich připojeních.</span><span class="sxs-lookup"><span data-stu-id="c175d-105">This topic shows how to retain information about users and their connections.</span></span>

## <a name="introduction"></a><span data-ttu-id="c175d-106">Úvod</span><span class="sxs-lookup"><span data-stu-id="c175d-106">Introduction</span></span>

<span data-ttu-id="c175d-107">Každý klient připojující se k centru projde jedinečným identifikátorem připojení. Tuto hodnotu můžete načíst ve vlastnosti `Context.ConnectionId` v kontextu centra.</span><span class="sxs-lookup"><span data-stu-id="c175d-107">Each client connecting to a hub passes a unique connection id. You can retrieve this value in the `Context.ConnectionId` property of the hub context.</span></span> <span data-ttu-id="c175d-108">Pokud vaše aplikace potřebuje mapovat uživatele na ID připojení a zachovat toto mapování, můžete použít jednu z následujících možností:</span><span class="sxs-lookup"><span data-stu-id="c175d-108">If your application needs to map a user to the connection id and persist that mapping, you can use one of the following:</span></span>

- <span data-ttu-id="c175d-109">[Úložiště v paměti](#inmemory), jako je například slovník</span><span class="sxs-lookup"><span data-stu-id="c175d-109">[In-memory storage](#inmemory), such as a dictionary</span></span>
- [<span data-ttu-id="c175d-110">Skupina signálů pro každého uživatele</span><span class="sxs-lookup"><span data-stu-id="c175d-110">SignalR group for each user</span></span>](#groups)
- <span data-ttu-id="c175d-111">[Trvalé, externí úložiště](#database), například databázová tabulka nebo Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="c175d-111">[Permanent, external storage](#database), such as a database table or Azure table storage</span></span>

<span data-ttu-id="c175d-112">Každá z těchto implementací je uvedena v tomto tématu.</span><span class="sxs-lookup"><span data-stu-id="c175d-112">Each of these implementations is shown in this topic.</span></span> <span data-ttu-id="c175d-113">Pomocí metod `OnConnected`, `OnDisconnected`a `OnReconnected` třídy `Hub` můžete sledovat stav připojení uživatele.</span><span class="sxs-lookup"><span data-stu-id="c175d-113">You use the `OnConnected`, `OnDisconnected`, and `OnReconnected` methods of the `Hub` class to track the user connection status.</span></span>

<span data-ttu-id="c175d-114">Nejlepší přístup k vaší aplikaci závisí na:</span><span class="sxs-lookup"><span data-stu-id="c175d-114">The best approach for your application depends on:</span></span>

- <span data-ttu-id="c175d-115">Počet webových serverů, které hostují vaši aplikaci.</span><span class="sxs-lookup"><span data-stu-id="c175d-115">The number of web servers hosting your application.</span></span>
- <span data-ttu-id="c175d-116">Bez ohledu na to, zda potřebujete získat seznam aktuálně připojených uživatelů.</span><span class="sxs-lookup"><span data-stu-id="c175d-116">Whether you need to get a list of the currently connected users.</span></span>
- <span data-ttu-id="c175d-117">Bez ohledu na to, jestli je potřeba zachovat informace o skupinách a uživatelích při restartování aplikace nebo serveru.</span><span class="sxs-lookup"><span data-stu-id="c175d-117">Whether you need to persist group and user information when the application or server restarts.</span></span>
- <span data-ttu-id="c175d-118">Zda je latence volání externího serveru problémem.</span><span class="sxs-lookup"><span data-stu-id="c175d-118">Whether the latency of calling an external server is an issue.</span></span>

<span data-ttu-id="c175d-119">Následující tabulka ukazuje, jaký přístup k těmto hlediskům funguje.</span><span class="sxs-lookup"><span data-stu-id="c175d-119">The following table shows which approach works for these considerations.</span></span>

|  | <span data-ttu-id="c175d-120">Více než jeden server</span><span class="sxs-lookup"><span data-stu-id="c175d-120">More than one server</span></span> | <span data-ttu-id="c175d-121">Získat seznam aktuálně připojených uživatelů</span><span class="sxs-lookup"><span data-stu-id="c175d-121">Get list of currently connected users</span></span> | <span data-ttu-id="c175d-122">Uchovat informace po restartování</span><span class="sxs-lookup"><span data-stu-id="c175d-122">Persist information after restarts</span></span> | <span data-ttu-id="c175d-123">Optimální výkon</span><span class="sxs-lookup"><span data-stu-id="c175d-123">Optimal performance</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="c175d-124">V paměti</span><span class="sxs-lookup"><span data-stu-id="c175d-124">In-memory</span></span> |  | ![](mapping-users-to-connections/_static/image1.png) |  | ![](mapping-users-to-connections/_static/image2.png) |
| <span data-ttu-id="c175d-125">Skupiny s jedním uživatelem</span><span class="sxs-lookup"><span data-stu-id="c175d-125">Single-user groups</span></span> | ![](mapping-users-to-connections/_static/image3.png) |  |  | ![](mapping-users-to-connections/_static/image4.png) |
| <span data-ttu-id="c175d-126">Trvalé, externí</span><span class="sxs-lookup"><span data-stu-id="c175d-126">Permanent, external</span></span> | ![](mapping-users-to-connections/_static/image5.png) | ![](mapping-users-to-connections/_static/image6.png) | ![](mapping-users-to-connections/_static/image7.png) |  |

<a id="inmemory"></a>

## <a name="in-memory-storage"></a><span data-ttu-id="c175d-127">Úložiště v paměti</span><span class="sxs-lookup"><span data-stu-id="c175d-127">In-memory storage</span></span>

<span data-ttu-id="c175d-128">Následující příklady ukazují, jak uchovávat informace o připojení a uživatelích ve slovníku, který je uložený v paměti.</span><span class="sxs-lookup"><span data-stu-id="c175d-128">The following examples show how to retain connection and user information in a dictionary that is stored in memory.</span></span> <span data-ttu-id="c175d-129">Slovník používá `HashSet` k uložení ID připojení. V každém okamžiku může mít uživatel více než jedno připojení k aplikaci signalizace.</span><span class="sxs-lookup"><span data-stu-id="c175d-129">The dictionary uses a `HashSet` to store the connection id. At any time a user could have more than one connection to the SignalR application.</span></span> <span data-ttu-id="c175d-130">Například uživatel, který je připojen prostřednictvím více zařízení nebo více než jedna karta prohlížeče, bude mít více než jedno ID připojení.</span><span class="sxs-lookup"><span data-stu-id="c175d-130">For example, a user who is connected through multiple devices or more than one browser tab would have more than one connection id.</span></span>

<span data-ttu-id="c175d-131">Pokud se aplikace ukončí, ztratí se všechny informace, ale budou se znovu naplnit, protože uživatelé znovu naváže připojení.</span><span class="sxs-lookup"><span data-stu-id="c175d-131">If the application shuts down, all of the information is lost, but it will be re-populated as the users re-establish their connections.</span></span> <span data-ttu-id="c175d-132">Úložiště v paměti nefunguje, pokud vaše prostředí obsahuje více než jeden webový server, protože každý server by měl samostatnou kolekci připojení.</span><span class="sxs-lookup"><span data-stu-id="c175d-132">In-memory storage does not work if your environment includes more than one web server because each server would have a separate collection of connections.</span></span>

<span data-ttu-id="c175d-133">První příklad ukazuje třídu, která spravuje mapování uživatelů na připojení.</span><span class="sxs-lookup"><span data-stu-id="c175d-133">The first example shows a class that manages the mapping of users to connections.</span></span> <span data-ttu-id="c175d-134">Klíčem pro HashSet – budou uživatelské jméno.</span><span class="sxs-lookup"><span data-stu-id="c175d-134">The key for the HashSet will be the user's name.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample1.cs)]

<span data-ttu-id="c175d-135">Další příklad ukazuje, jak použít třídu mapování připojení z rozbočovače.</span><span class="sxs-lookup"><span data-stu-id="c175d-135">The next example shows how to use the connection mapping class from a hub.</span></span> <span data-ttu-id="c175d-136">Instance třídy je uložena v názvu proměnné `_connections`.</span><span class="sxs-lookup"><span data-stu-id="c175d-136">The instance of the class is stored in a variable name `_connections`.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample2.cs)]

<a id="groups"></a>

## <a name="single-user-groups"></a><span data-ttu-id="c175d-137">Skupiny s jedním uživatelem</span><span class="sxs-lookup"><span data-stu-id="c175d-137">Single-user groups</span></span>

<span data-ttu-id="c175d-138">Můžete vytvořit skupinu pro každého uživatele a poté odeslat zprávu do této skupiny, pokud chcete pouze kontaktovat tohoto uživatele.</span><span class="sxs-lookup"><span data-stu-id="c175d-138">You can create a group for each user, and then send a message to that group when you want to reach only that user.</span></span> <span data-ttu-id="c175d-139">Název každé skupiny je jméno uživatele.</span><span class="sxs-lookup"><span data-stu-id="c175d-139">The name of each group is the name of the user.</span></span> <span data-ttu-id="c175d-140">Pokud má uživatel více než jedno připojení, každé ID připojení se přidá do skupiny uživatelů.</span><span class="sxs-lookup"><span data-stu-id="c175d-140">If a user has more than one connection, each connection id is added to the user's group.</span></span>

<span data-ttu-id="c175d-141">Nemusíte ručně odebrat uživatele ze skupiny, když se uživatel odpojí.</span><span class="sxs-lookup"><span data-stu-id="c175d-141">You should not manually remove the user from the group when the user disconnects.</span></span> <span data-ttu-id="c175d-142">Tato akce je automaticky prováděna architekturou Signal.</span><span class="sxs-lookup"><span data-stu-id="c175d-142">This action is automatically performed by the SignalR framework.</span></span>

<span data-ttu-id="c175d-143">Následující příklad ukazuje, jak implementovat skupiny s jedním uživatelem.</span><span class="sxs-lookup"><span data-stu-id="c175d-143">The following example shows how to implement single-user groups.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample3.cs)]

<a id="database"></a>

## <a name="permanent-external-storage"></a><span data-ttu-id="c175d-144">Trvalé, externí úložiště</span><span class="sxs-lookup"><span data-stu-id="c175d-144">Permanent, external storage</span></span>

<span data-ttu-id="c175d-145">V tomto tématu se dozvíte, jak použít databázi nebo úložiště tabulek Azure pro ukládání informací o připojení.</span><span class="sxs-lookup"><span data-stu-id="c175d-145">This topic shows how to use either a database or Azure table storage for storing connection information.</span></span> <span data-ttu-id="c175d-146">Tento přístup funguje, když máte více webových serverů, protože každý webový server může komunikovat se stejným úložištěm dat.</span><span class="sxs-lookup"><span data-stu-id="c175d-146">This approach works when you have multiple web servers because each web server can interact with the same data repository.</span></span> <span data-ttu-id="c175d-147">Pokud vaše webové servery přestanou pracovat nebo se aplikace restartuje, není volána metoda `OnDisconnected`.</span><span class="sxs-lookup"><span data-stu-id="c175d-147">If your web servers stop working or the application restarts, the `OnDisconnected` method is not called.</span></span> <span data-ttu-id="c175d-148">Proto je možné, že úložiště dat bude obsahovat záznamy pro ID připojení, která již nejsou platná.</span><span class="sxs-lookup"><span data-stu-id="c175d-148">Therefore, it is possible that your data repository will have records for connection ids that are no longer valid.</span></span> <span data-ttu-id="c175d-149">Chcete-li vyčistit tyto osamocené záznamy, můžete chtít zrušit platnost všech připojení, která byla vytvořena mimo časový rámec, který je pro vaši aplikaci relevantní.</span><span class="sxs-lookup"><span data-stu-id="c175d-149">To clean up these orphaned records, you may wish to invalidate any connection that was created outside of a timeframe that is relevant to your application.</span></span> <span data-ttu-id="c175d-150">Příklady v této části obsahují hodnotu pro sledování při vytvoření připojení, ale neukazují, jak vyčistit staré záznamy, protože je vhodné to udělat jako proces na pozadí.</span><span class="sxs-lookup"><span data-stu-id="c175d-150">The examples in this section include a value for tracking when the connection was created, but do not show how to clean up old records because you may want to do that as background process.</span></span>

### <a name="database"></a><span data-ttu-id="c175d-151">databáze</span><span class="sxs-lookup"><span data-stu-id="c175d-151">Database</span></span>

<span data-ttu-id="c175d-152">Následující příklady ukazují, jak uchovávat informace o připojení a uživatelích v databázi.</span><span class="sxs-lookup"><span data-stu-id="c175d-152">The following examples show how to retain connection and user information in a database.</span></span> <span data-ttu-id="c175d-153">Můžete použít libovolnou technologii pro přístup k datům; Následující příklad však ukazuje, jak definovat modely pomocí Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="c175d-153">You can use any data access technology; however, the example below shows how to define models using Entity Framework.</span></span> <span data-ttu-id="c175d-154">Tyto modely entit odpovídají tabulkám a polím databáze.</span><span class="sxs-lookup"><span data-stu-id="c175d-154">These entity models correspond to database tables and fields.</span></span> <span data-ttu-id="c175d-155">Vaše datová struktura se může značně lišit v závislosti na požadavcích vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="c175d-155">Your data structure could vary considerably depending on the requirements of your application.</span></span>

<span data-ttu-id="c175d-156">První příklad ukazuje, jak definovat entitu uživatele, která může být přidružena k mnoha entitám připojení.</span><span class="sxs-lookup"><span data-stu-id="c175d-156">The first example shows how to define a user entity that can be associated with many connection entities.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample4.cs)]

<span data-ttu-id="c175d-157">Pak z centra můžete sledovat stav každého připojení s níže uvedeným kódem.</span><span class="sxs-lookup"><span data-stu-id="c175d-157">Then, from the hub, you can track the state of each connection with the code shown below.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample5.cs)]

### <a name="azure-table-storage"></a><span data-ttu-id="c175d-158">Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="c175d-158">Azure table storage</span></span>

<span data-ttu-id="c175d-159">Následující příklad služby Azure Table Storage je podobný jako příklad databáze.</span><span class="sxs-lookup"><span data-stu-id="c175d-159">The following Azure table storage example is similar to the database example.</span></span> <span data-ttu-id="c175d-160">Nezahrnuje všechny informace, které byste museli začít s Azure Table Storage Service.</span><span class="sxs-lookup"><span data-stu-id="c175d-160">It does not include all of the information that you would need to get started with Azure Table Storage Service.</span></span> <span data-ttu-id="c175d-161">Informace najdete v tématu [použití úložiště Table z rozhraní .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span><span class="sxs-lookup"><span data-stu-id="c175d-161">For information, see [How to use Table storage from .NET](https://azure.microsoft.com/documentation/articles/storage-dotnet-how-to-use-tables/).</span></span>

<span data-ttu-id="c175d-162">Následující příklad ukazuje entitu tabulky pro ukládání informací o připojení.</span><span class="sxs-lookup"><span data-stu-id="c175d-162">The following example shows a table entity for storing connection information.</span></span> <span data-ttu-id="c175d-163">Rozdělí data podle uživatelského jména a identifikují každou entitu podle ID připojení, takže uživatel může mít kdykoli více připojení.</span><span class="sxs-lookup"><span data-stu-id="c175d-163">It partitions the data by user name, and identifies each entity by the connection id, so a user can have multiple connections at any time.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample6.cs)]

<span data-ttu-id="c175d-164">V centru sledujete stav připojení každého uživatele.</span><span class="sxs-lookup"><span data-stu-id="c175d-164">In the hub, you track the status of each user's connection.</span></span>

[!code-csharp[Main](mapping-users-to-connections/samples/sample7.cs)]

---
uid: signalr/overview/older-versions/persistent-connection-authorization
title: Ověřování a autorizace trvalých připojení k signalizaci (signál 1. x) | Microsoft Docs
author: bradygaster
description: Toto téma popisuje, jak vynutili autorizaci na trvalém připojení. Obecné informace o integraci zabezpečení do aplikace Signal,...
ms.author: bradyg
ms.date: 10/21/2013
ms.assetid: c34bc627-41af-4c21-a817-e97a19a7f252
msc.legacyurl: /signalr/overview/older-versions/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 9ccc59e3ea502daf12ce82382ab30ca73ca0f9b5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536538"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a><span data-ttu-id="863e3-104">Ověřování a autorizace trvalých připojení SignalR (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="863e3-104">Authentication and Authorization for SignalR Persistent Connections (SignalR 1.x)</span></span>

<span data-ttu-id="863e3-105">autorem [Fletcher](https://github.com/pfletcher), který [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="863e3-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="863e3-106">Toto téma popisuje, jak vynutili autorizaci na trvalém připojení.</span><span class="sxs-lookup"><span data-stu-id="863e3-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="863e3-107">Obecné informace o integraci zabezpečení do aplikace signalizace najdete v tématu [Úvod do zabezpečení](index.md).</span><span class="sxs-lookup"><span data-stu-id="863e3-107">For general information about integrating security into a SignalR application, see [Introduction to Security](index.md).</span></span>

## <a name="enforce-authorization"></a><span data-ttu-id="863e3-108">Vymáhat autorizaci</span><span class="sxs-lookup"><span data-stu-id="863e3-108">Enforce authorization</span></span>

<span data-ttu-id="863e3-109">Pokud chcete vynutilit autorizační pravidla při použití [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) , musíte přepsat metodu `AuthorizeRequest`.</span><span class="sxs-lookup"><span data-stu-id="863e3-109">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="863e3-110">Atribut `Authorize` nelze použít u trvalých připojení.</span><span class="sxs-lookup"><span data-stu-id="863e3-110">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="863e3-111">Metoda `AuthorizeRequest` je volána rozhraním signalizace před každou žádostí o ověření, zda je uživatel autorizován k provedení požadované akce.</span><span class="sxs-lookup"><span data-stu-id="863e3-111">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="863e3-112">Metoda `AuthorizeRequest` není volána od klienta; místo toho uživatele ověřujete pomocí mechanismu standardního ověřování vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="863e3-112">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="863e3-113">Následující příklad ukazuje, jak omezit požadavky na ověřené uživatele.</span><span class="sxs-lookup"><span data-stu-id="863e3-113">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="863e3-114">Do metody AuthorizeRequest můžete přidat libovolnou přizpůsobenou logiku autorizace. například kontrola, zda uživatel patří do konkrétní role.</span><span class="sxs-lookup"><span data-stu-id="863e3-114">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>

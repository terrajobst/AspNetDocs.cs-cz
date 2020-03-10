---
uid: signalr/overview/security/persistent-connection-authorization
title: Ověřování a autorizace trvalých připojení k signalizaci | Microsoft Docs
author: bradygaster
description: Toto téma popisuje, jak vynutili autorizaci na trvalém připojení. Obecné informace o integraci zabezpečení do aplikace Signal,...
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: e264677b-9c01-47ec-94f9-3cd8f08f94af
msc.legacyurl: /signalr/overview/security/persistent-connection-authorization
msc.type: authoredcontent
ms.openlocfilehash: 7e69d3c1a18f1239142891734ba58cd2b0078f84
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578874"
---
# <a name="authentication-and-authorization-for-signalr-persistent-connections"></a><span data-ttu-id="312fc-104">Ověřování a autorizace trvalých připojení SignalR</span><span class="sxs-lookup"><span data-stu-id="312fc-104">Authentication and Authorization for SignalR Persistent Connections</span></span>

<span data-ttu-id="312fc-105">autorem [Fletcher](https://github.com/pfletcher), který [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="312fc-105">by [Patrick Fletcher](https://github.com/pfletcher), [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="312fc-106">Toto téma popisuje, jak vynutili autorizaci na trvalém připojení.</span><span class="sxs-lookup"><span data-stu-id="312fc-106">This topic describes how to enforce authorization on a persistent connection.</span></span> <span data-ttu-id="312fc-107">Obecné informace o integraci zabezpečení do aplikace signalizace najdete v tématu [Úvod do zabezpečení](introduction-to-security.md).</span><span class="sxs-lookup"><span data-stu-id="312fc-107">For general information about integrating security into a SignalR application, see [Introduction to Security](introduction-to-security.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="312fc-108">Verze softwaru používané v tomto tématu</span><span class="sxs-lookup"><span data-stu-id="312fc-108">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="312fc-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="312fc-109">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="312fc-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="312fc-110">.NET 4.5</span></span>
> - <span data-ttu-id="312fc-111">Signal – verze 2</span><span class="sxs-lookup"><span data-stu-id="312fc-111">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="312fc-112">Předchozí verze tohoto tématu</span><span class="sxs-lookup"><span data-stu-id="312fc-112">Previous versions of this topic</span></span>
>
> <span data-ttu-id="312fc-113">Informace o dřívějších verzích nástroje Signal najdete v části [Signal – starší verze](../older-versions/index.md).</span><span class="sxs-lookup"><span data-stu-id="312fc-113">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="312fc-114">Dotazy a komentáře</span><span class="sxs-lookup"><span data-stu-id="312fc-114">Questions and comments</span></span>
>
> <span data-ttu-id="312fc-115">Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="312fc-115">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="312fc-116">Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra signálu ASP.NET](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) nebo [StackOverflow.com](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="312fc-116">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="enforce-authorization"></a><span data-ttu-id="312fc-117">Vymáhat autorizaci</span><span class="sxs-lookup"><span data-stu-id="312fc-117">Enforce authorization</span></span>

<span data-ttu-id="312fc-118">Pokud chcete vynutilit autorizační pravidla při použití [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) , musíte přepsat metodu `AuthorizeRequest`.</span><span class="sxs-lookup"><span data-stu-id="312fc-118">To enforce authorization rules when using a [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) you must override the `AuthorizeRequest` method.</span></span> <span data-ttu-id="312fc-119">Atribut `Authorize` nelze použít u trvalých připojení.</span><span class="sxs-lookup"><span data-stu-id="312fc-119">You cannot use the `Authorize` attribute with persistent connections.</span></span> <span data-ttu-id="312fc-120">Metoda `AuthorizeRequest` je volána rozhraním signalizace před každou žádostí o ověření, zda je uživatel autorizován k provedení požadované akce.</span><span class="sxs-lookup"><span data-stu-id="312fc-120">The `AuthorizeRequest` method is called by the SignalR Framework before every request to verify that the user is authorized to perform the requested action.</span></span> <span data-ttu-id="312fc-121">Metoda `AuthorizeRequest` není volána od klienta; místo toho uživatele ověřujete pomocí mechanismu standardního ověřování vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="312fc-121">The `AuthorizeRequest` method is not called from the client; instead, you authenticate the user through your application's standard authentication mechanism.</span></span>

<span data-ttu-id="312fc-122">Následující příklad ukazuje, jak omezit požadavky na ověřené uživatele.</span><span class="sxs-lookup"><span data-stu-id="312fc-122">The example below shows how to limit requests to authenticated users.</span></span>

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

<span data-ttu-id="312fc-123">Do metody AuthorizeRequest můžete přidat libovolnou přizpůsobenou logiku autorizace. například kontrola, zda uživatel patří do konkrétní role.</span><span class="sxs-lookup"><span data-stu-id="312fc-123">You can add any customized authorization logic in the AuthorizeRequest method; such as, checking whether a user belongs to a particular role.</span></span>

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
# <a name="authentication-and-authorization-for-signalr-persistent-connections-signalr-1x"></a>Ověřování a autorizace trvalých připojení SignalR (SignalR 1.x)

autorem [Fletcher](https://github.com/pfletcher), který [FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Toto téma popisuje, jak vynutili autorizaci na trvalém připojení. Obecné informace o integraci zabezpečení do aplikace signalizace najdete v tématu [Úvod do zabezpečení](index.md).

## <a name="enforce-authorization"></a>Vymáhat autorizaci

Pokud chcete vynutilit autorizační pravidla při použití [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) , musíte přepsat metodu `AuthorizeRequest`. Atribut `Authorize` nelze použít u trvalých připojení. Metoda `AuthorizeRequest` je volána rozhraním signalizace před každou žádostí o ověření, zda je uživatel autorizován k provedení požadované akce. Metoda `AuthorizeRequest` není volána od klienta; místo toho uživatele ověřujete pomocí mechanismu standardního ověřování vaší aplikace.

Následující příklad ukazuje, jak omezit požadavky na ověřené uživatele.

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

Do metody AuthorizeRequest můžete přidat libovolnou přizpůsobenou logiku autorizace. například kontrola, zda uživatel patří do konkrétní role.

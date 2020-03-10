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
# <a name="authentication-and-authorization-for-signalr-persistent-connections"></a>Ověřování a autorizace trvalých připojení SignalR

autorem [Fletcher](https://github.com/pfletcher), který [FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Toto téma popisuje, jak vynutili autorizaci na trvalém připojení. Obecné informace o integraci zabezpečení do aplikace signalizace najdete v tématu [Úvod do zabezpečení](introduction-to-security.md).
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

## <a name="enforce-authorization"></a>Vymáhat autorizaci

Pokud chcete vynutilit autorizační pravidla při použití [PersistentConnection](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.persistentconnection(v=vs.111).aspx) , musíte přepsat metodu `AuthorizeRequest`. Atribut `Authorize` nelze použít u trvalých připojení. Metoda `AuthorizeRequest` je volána rozhraním signalizace před každou žádostí o ověření, zda je uživatel autorizován k provedení požadované akce. Metoda `AuthorizeRequest` není volána od klienta; místo toho uživatele ověřujete pomocí mechanismu standardního ověřování vaší aplikace.

Následující příklad ukazuje, jak omezit požadavky na ověřené uživatele.

[!code-csharp[Main](persistent-connection-authorization/samples/sample1.cs)]

Do metody AuthorizeRequest můžete přidat libovolnou přizpůsobenou logiku autorizace. například kontrola, zda uživatel patří do konkrétní role.

---
uid: webhooks/source
title: Zdrojový kód Webhooku ASP.NET a balíčky NuGet | Microsoft Docs
author: rick-anderson
description: Odkazy na zdrojový kód webhooků ASP.NET a balíčky NuGet
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: 8d07848754d9efda9c893b8ba54ac6d0c0214a53
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000705"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a>Zdrojový kód Webhooku ASP.NET a balíčky NuGet

Microsoft ASP.NET webhooků je součástí řady Microsoft ASP.NET modulů a hostuje se jako [Open source projekt na GitHubu](https://github.com/aspnet/WebHooks). To znamená, že budeme přijímat příspěvky, ale před odesláním žádosti o přijetí změn se prosím podívejte na [pokyny pro příspěvky](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) .

Tato online dokumentace, kterou právě čtete, je také hostována jako [Open source na GitHubu](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) a přijímá i příspěvky.

## <a name="nuget-packages"></a>Balíčky NuGet

[Balíčky NuGet](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) jsou rozdělené na tři části:

* [Běžné](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): Společný balíček, který je sdílen mezi odesílateli a přijímači.

* [Odesílatel](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): Sada balíčků, které podporují odesílání vlastních webhooků jiným uživatelům. Funkce pro odesílání webhooků je podrobněji popsána v tématu [odesílání](sending/senders.md)webhooků.

* [Přijímače](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): Sada balíčků podporující příjem webhooků od ostatních. Funkce pro příjem webhooků je podrobněji popsána v tématu [příjem](receiving/index.md)webhooků.

---
uid: webhooks/source
title: Zdrojový kód Webhooku ASP.NET a balíčky NuGet | Microsoft Docs
author: rick-anderson
description: Odkazy na zdrojový kód webhooků ASP.NET a balíčky NuGet
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 91a62bfa-ea3a-41f9-a2e1-e90d2c8fc8ca
ms.openlocfilehash: 8d07848754d9efda9c893b8ba54ac6d0c0214a53
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78633061"
---
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a>Zdrojový kód Webhooku ASP.NET a balíčky NuGet

Microsoft ASP.NET webhooků je součástí řady Microsoft ASP.NET modulů a hostuje se jako [Open source projekt na GitHubu](https://github.com/aspnet/WebHooks). To znamená, že budeme přijímat příspěvky, ale před odesláním žádosti o přijetí změn se prosím podívejte na [pokyny pro příspěvky](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) .

Tato online dokumentace, kterou právě čtete, je také hostována jako [Open source na GitHubu](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) a přijímá i příspěvky.

## <a name="nuget-packages"></a>Balíčky NuGet

[Balíčky NuGet](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) jsou rozdělené na tři části:

* [Běžný](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): společný balíček, který je sdílen mezi odesílateli a přijímači.

* [Odesilatel](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): sada balíčků, které podporují odesílání vlastních webhooků jiným uživatelům. Funkce pro odesílání webhooků je podrobněji popsána v tématu [odesílání webhooků](sending/senders.md).

* [Přijímače](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): sada balíčků podporující příjem webhooků od ostatních. Funkce pro příjem webhooků je podrobněji popsána v tématu [příjem webhooků](receiving/index.md).

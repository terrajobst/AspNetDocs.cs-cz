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
# <a name="aspnet-webhooks-source-code-and-nuget-packages"></a><span data-ttu-id="86b20-103">Zdrojový kód Webhooku ASP.NET a balíčky NuGet</span><span class="sxs-lookup"><span data-stu-id="86b20-103">ASP.NET WebHooks source code and NuGet packages</span></span>

<span data-ttu-id="86b20-104">Microsoft ASP.NET webhooků je součástí řady Microsoft ASP.NET modulů a hostuje se jako [Open source projekt na GitHubu](https://github.com/aspnet/WebHooks).</span><span class="sxs-lookup"><span data-stu-id="86b20-104">Microsoft ASP.NET WebHooks is part of the Microsoft ASP.NET family of modules and is hosted as an [Open Source Project on GitHub](https://github.com/aspnet/WebHooks).</span></span> <span data-ttu-id="86b20-105">To znamená, že budeme přijímat příspěvky, ale před odesláním žádosti o přijetí změn se prosím podívejte na [pokyny pro příspěvky](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) .</span><span class="sxs-lookup"><span data-stu-id="86b20-105">This means that we accept contributions, but please look at the [Contribution Guidelines](https://github.com/aspnet/Home/blob/master/CONTRIBUTING.md) before submitting a pull request.</span></span>

<span data-ttu-id="86b20-106">Tato online dokumentace, kterou právě čtete, je také hostována jako [Open source na GitHubu](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) a přijímá i příspěvky.</span><span class="sxs-lookup"><span data-stu-id="86b20-106">This online documentation which you are reading now is also hosted as [Open Source on GitHub](http://docs.asp.net/en/latest/contribute/style-guide.html#style-guide) and also accepts contributions.</span></span>

## <a name="nuget-packages"></a><span data-ttu-id="86b20-107">Balíčky NuGet</span><span class="sxs-lookup"><span data-stu-id="86b20-107">NuGet packages</span></span>

<span data-ttu-id="86b20-108">[Balíčky NuGet](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) jsou rozdělené na tři části:</span><span class="sxs-lookup"><span data-stu-id="86b20-108">The [NuGet packages](https://nuget.org/packages?q=Microsoft.AspNet.WebHooks) are divided into three parts:</span></span>

* <span data-ttu-id="86b20-109">[Běžné](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): Společný balíček, který je sdílen mezi odesílateli a přijímači.</span><span class="sxs-lookup"><span data-stu-id="86b20-109">[Common](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Common): A common package that is shared between senders and receivers.</span></span>

* <span data-ttu-id="86b20-110">[Odesílatel](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): Sada balíčků, které podporují odesílání vlastních webhooků jiným uživatelům.</span><span class="sxs-lookup"><span data-stu-id="86b20-110">[Sender](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Custom): A set of packages supporting sending your own WebHooks to others.</span></span> <span data-ttu-id="86b20-111">Funkce pro odesílání webhooků je podrobněji popsána v tématu [odesílání](sending/senders.md)webhooků.</span><span class="sxs-lookup"><span data-stu-id="86b20-111">The functionality for sending WebHooks is described in more detail in [Sending WebHooks](sending/senders.md).</span></span>

* <span data-ttu-id="86b20-112">[Přijímače](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): Sada balíčků podporující příjem webhooků od ostatních.</span><span class="sxs-lookup"><span data-stu-id="86b20-112">[Receivers](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers): A set of packages supporting receiving WebHooks from others.</span></span> <span data-ttu-id="86b20-113">Funkce pro příjem webhooků je podrobněji popsána v tématu [příjem](receiving/index.md)webhooků.</span><span class="sxs-lookup"><span data-stu-id="86b20-113">The functionality for receiving WebHooks is described in more detail in [Receiving WebHooks](receiving/index.md).</span></span>

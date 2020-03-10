---
uid: webhooks/receiving/receivers
title: Přijímače webhooků ASP.NET | Microsoft Docs
author: rick-anderson
description: Přijímače webhooků ASP.NET
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 6cdea089-15b2-4732-8c68-921ca561a8f1
ms.openlocfilehash: d771a588b23abcd7b1b33e694af17b219683fc48
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574191"
---
# <a name="aspnet-webhooks-receivers"></a><span data-ttu-id="9c4f5-103">Přijímače webhooků ASP.NET</span><span class="sxs-lookup"><span data-stu-id="9c4f5-103">ASP.NET WebHooks receivers</span></span>

<span data-ttu-id="9c4f5-104">Přijímání webhooků závisí na odesílateli.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-104">Receiving WebHooks depends on who the sender is.</span></span> <span data-ttu-id="9c4f5-105">Někdy jsou k dispozici další kroky pro registraci Webhooku, který ověřuje, že předplatitel skutečně naslouchá.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-105">Sometimes there are additional steps registering a WebHook verifying that the subscriber is really listening.</span></span> <span data-ttu-id="9c4f5-106">Některé Webhooky poskytují model nabízených oznámení, kde požadavek HTTP POST obsahuje jenom odkaz na informace o události, které se pak mají načíst nezávisle.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-106">Some WebHooks provide a push-to-pull model where the HTTP POST request only contains a reference to the event information which is then to be retrieved independently.</span></span> <span data-ttu-id="9c4f5-107">Model zabezpečení se často mění poměrně jako bit.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-107">Often the security model varies quite a bit.</span></span>

<span data-ttu-id="9c4f5-108">Účelem Microsoft ASP.NET webhooků je zjednodušit a lépe odpovídat rozhraní API, aniž byste strávili spoustu času a zjistili si, jak zpracovat konkrétní variantu webhooků.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-108">The purpose of Microsoft ASP.NET WebHooks is to make it both simpler and more consistent to wire up your API without spending a lot of time figuring out how to handle any particular variant of WebHooks.</span></span>

<span data-ttu-id="9c4f5-109">Přijímač Webhooku zodpovídá za příjem a ověření webhooků od konkrétního odesílatele.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-109">A WebHook receiver is responsible for accepting and verifying WebHooks from a particular sender.</span></span> <span data-ttu-id="9c4f5-110">Přijímač Webhooku může podporovat libovolný počet webhooků, z nichž každá má svou vlastní konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-110">A WebHook receiver can support any number of WebHooks, each with their own configuration.</span></span> <span data-ttu-id="9c4f5-111">Přijímač Webhooku GitHubu může například přijímat Webhooky z libovolného počtu úložišť GitHub.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-111">For example, the GitHub WebHook receiver can accept WebHooks from any number of GitHub repositories.</span></span>

## <a name="webhook-receiver-uris"></a><span data-ttu-id="9c4f5-112">Identifikátory URI přijímače Webhooku</span><span class="sxs-lookup"><span data-stu-id="9c4f5-112">WebHook Receiver URIs</span></span>

<span data-ttu-id="9c4f5-113">Instalací Microsoft ASP.NET webhooků získáte obecný řadič Webhooku, který přijímá žádosti Webhooku z otevřeného počtu nedokončených služeb.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-113">By installing Microsoft ASP.NET WebHooks you get a general WebHook controller which accepts WebHook requests from an open-ended number of services.</span></span> <span data-ttu-id="9c4f5-114">Při přijetí žádosti se vybere příslušný přijímač, který jste nainstalovali pro zpracování konkrétního odesílatele Webhooku.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-114">When a request arrives, it picks the appropriate receiver that you have installed for handling a particular WebHook sender.</span></span>

<span data-ttu-id="9c4f5-115">Identifikátor URI tohoto kontroleru je identifikátor URI Webhooku, který zaregistrujete ve službě a má formát:</span><span class="sxs-lookup"><span data-stu-id="9c4f5-115">The URI of this controller is the WebHook URI that you register with the service and is of the form:</span></span>

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

<span data-ttu-id="9c4f5-116">Z bezpečnostních důvodů vyžaduje mnoho přijímačů webhooků, že identifikátor URI je identifikátor URI *https* a v některých případech musí obsahovat taky další parametr dotazu, který se používá k vynucení, aby Webhooky mohli poslat jenom zamýšlenou stranu k identifikátoru URI výše.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-116">For security reasons, many WebHook receivers require that the URI is an *https* URI and in some cases it must also contain an additional query parameter which is used to enforce that only the intended party can send WebHooks to the URI above.</span></span>

<span data-ttu-id="9c4f5-117">Komponenta `<receiver>` je název přijímače, například `github` nebo `slack`.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-117">The `<receiver>` component is the name of the receiver, for example `github` or `slack`.</span></span>

<span data-ttu-id="9c4f5-118">*{ID}* je volitelný identifikátor, který se dá použít k identifikaci konkrétní konfigurace přijímače Webhooku.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-118">The *{id}* is an optional identifier which can be used to identify a particular WebHook receiver configuration.</span></span> <span data-ttu-id="9c4f5-119">To se dá použít k registraci N webhooků s konkrétním přijímačem.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-119">This can be used to register N WebHooks with a particular receiver.</span></span> <span data-ttu-id="9c4f5-120">Například následující tři identifikátory URI lze použít k registraci pro tři nezávislé Webhooky:</span><span class="sxs-lookup"><span data-stu-id="9c4f5-120">For example, the following three URIs can be used to register for three independent WebHooks:</span></span>

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a><span data-ttu-id="9c4f5-121">Instalace přijímače Webhooku</span><span class="sxs-lookup"><span data-stu-id="9c4f5-121">Installing a WebHook Receiver</span></span>

<span data-ttu-id="9c4f5-122">Pokud chcete přijímat Webhooky pomocí Microsoft ASP.NET webhooků, nejdřív nainstalujte balíček NuGet pro poskytovatele Webhooku nebo poskytovatele, ze kterých chcete přijímat Webhooky.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-122">To receive WebHooks using Microsoft ASP.NET WebHooks, you first install the Nuget package for the WebHook provider or providers you want to receive WebHooks from.</span></span> <span data-ttu-id="9c4f5-123">Balíčky NuGet se nazývají [Microsoft. ASPNET. webhooks. přijímačs. \*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) , kde poslední část označuje, že je služba podporovaná.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-123">The Nuget packages are named [Microsoft.AspNet.WebHooks.Receivers.\*](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) where the last part indicates the service supported.</span></span> <span data-ttu-id="9c4f5-124">Například</span><span class="sxs-lookup"><span data-stu-id="9c4f5-124">For example</span></span>

<span data-ttu-id="9c4f5-125">[Microsoft. ASPNET. webhooks. pøijímaèe. GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) poskytuje podporu pro příjem webhooků z GitHubu a [Microsoft. ASPNET. webhooks. pøijímaèe. Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) poskytuje podporu pro příjem webhooků generovaných Webhooky ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-125">[Microsoft.AspNet.WebHooks.Receivers.GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) provides support for receiving WebHooks from GitHub and [Microsoft.AspNet.WebHooks.Receivers.Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) provides support for receiving WebHooks generated by ASP.NET WebHooks.</span></span>

<span data-ttu-id="9c4f5-126">V poli můžete najít podporu pro Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, časovou rezervu, proužek, Trello a WordPress, ale je možné podporovat libovolný počet jiných poskytovatelů.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-126">Out of the box you can find support for Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, Slack, Stripe, Trello, and WordPress but it is possible to support any number of other providers.</span></span>

## <a name="configuring-a-webhook-receiver"></a><span data-ttu-id="9c4f5-127">Konfigurace přijímače Webhooku</span><span class="sxs-lookup"><span data-stu-id="9c4f5-127">Configuring a WebHook Receiver</span></span>

<span data-ttu-id="9c4f5-128">Přijímače Webhooku se konfigurují prostřednictvím [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) rozhraní a konkrétní implementace tohoto rozhraní se dají zaregistrovat pomocí modelu injektáže pro vkládání závislostí.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-128">WebHook Receivers are configured through the [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) inteface and particular implementations of that interface can be registered using any dependency injection model.</span></span> <span data-ttu-id="9c4f5-129">Výchozí implementace používá nastavení aplikace, které může být buď nastaveno v souboru Web. config, nebo pokud používáte Azure Web Apps, lze nastavit prostřednictvím webu [Azure Portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9c4f5-129">The default implementation uses Application Settings which can either be set in the Web.config file, or, if using Azure Web Apps, can be set through the [Azure Portal](https://portal.azure.com/).</span></span>

![Nastavení aplikace Azure](_static/AzureAppSettings.png)

<span data-ttu-id="9c4f5-131">Formát pro klíče nastavení aplikace je následující:</span><span class="sxs-lookup"><span data-stu-id="9c4f5-131">The format for Application Setting keys is as follows:</span></span>

```
MS_WebHookReceiverSecret_<receiver>
```

<span data-ttu-id="9c4f5-132">Hodnota je seznam hodnot oddělených čárkami, které odpovídají hodnotám *{ID}* , pro které Webhooky byly registrovány, například:</span><span class="sxs-lookup"><span data-stu-id="9c4f5-132">The value is a comma-separated list of values matching the *{id}* values for which WebHooks have been registered, for example:</span></span>

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a><span data-ttu-id="9c4f5-133">Inicializuje se přijímač Webhooku.</span><span class="sxs-lookup"><span data-stu-id="9c4f5-133">Initializing a WebHook Receiver</span></span>

<span data-ttu-id="9c4f5-134">Přijímače Webhooku jsou inicializovány jejich registrací, obvykle ve statické třídě *WebApiConfig* , například:</span><span class="sxs-lookup"><span data-stu-id="9c4f5-134">WebHook Receivers are initialized by registering them, typically in the *WebApiConfig* static class, for example:</span></span>

```csharp
namespace WebHookReceivers
{
    public static class WebApiConfig
    {
        public static void Register(HttpConfiguration config)
        {
            // Web API configuration and services

            // Web API routes
            config.MapHttpAttributeRoutes();

            config.Routes.MapHttpRoute(
                name: "DefaultApi",
                routeTemplate: "api/{controller}/{id}",
                defaults: new { id = RouteParameter.Optional }
            );

            // Load receivers
            config.InitializeReceiveGitHubWebHooks();
        }
    }
}
```

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
# <a name="aspnet-webhooks-receivers"></a>Přijímače webhooků ASP.NET

Přijímání webhooků závisí na odesílateli. Někdy jsou k dispozici další kroky pro registraci Webhooku, který ověřuje, že předplatitel skutečně naslouchá. Některé Webhooky poskytují model nabízených oznámení, kde požadavek HTTP POST obsahuje jenom odkaz na informace o události, které se pak mají načíst nezávisle. Model zabezpečení se často mění poměrně jako bit.

Účelem Microsoft ASP.NET webhooků je zjednodušit a lépe odpovídat rozhraní API, aniž byste strávili spoustu času a zjistili si, jak zpracovat konkrétní variantu webhooků.

Přijímač Webhooku zodpovídá za příjem a ověření webhooků od konkrétního odesílatele. Přijímač Webhooku může podporovat libovolný počet webhooků, z nichž každá má svou vlastní konfiguraci. Přijímač Webhooku GitHubu může například přijímat Webhooky z libovolného počtu úložišť GitHub.

## <a name="webhook-receiver-uris"></a>Identifikátory URI přijímače Webhooku

Instalací Microsoft ASP.NET webhooků získáte obecný řadič Webhooku, který přijímá žádosti Webhooku z otevřeného počtu nedokončených služeb. Při přijetí žádosti se vybere příslušný přijímač, který jste nainstalovali pro zpracování konkrétního odesílatele Webhooku.

Identifikátor URI tohoto kontroleru je identifikátor URI Webhooku, který zaregistrujete ve službě a má formát:

```
https://<host>/api/webhooks/incoming/<receiver>/{id}
```

Z bezpečnostních důvodů vyžaduje mnoho přijímačů webhooků, že identifikátor URI je identifikátor URI *https* a v některých případech musí obsahovat taky další parametr dotazu, který se používá k vynucení, aby Webhooky mohli poslat jenom zamýšlenou stranu k identifikátoru URI výše.

Komponenta `<receiver>` je název přijímače, například `github` nebo `slack`.

*{ID}* je volitelný identifikátor, který se dá použít k identifikaci konkrétní konfigurace přijímače Webhooku. To se dá použít k registraci N webhooků s konkrétním přijímačem. Například následující tři identifikátory URI lze použít k registraci pro tři nezávislé Webhooky:

```
https://<host>/api/webhooks/incoming/github
https://<host>/api/webhooks/incoming/github/12345
https://<host>/api/webhooks/incoming/github/54321
```

## <a name="installing-a-webhook-receiver"></a>Instalace přijímače Webhooku

Pokud chcete přijímat Webhooky pomocí Microsoft ASP.NET webhooků, nejdřív nainstalujte balíček NuGet pro poskytovatele Webhooku nebo poskytovatele, ze kterých chcete přijímat Webhooky. Balíčky NuGet se nazývají [Microsoft. ASPNET. webhooks. přijímačs. *](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers) , kde poslední část označuje, že je služba podporovaná. Například

[Microsoft. ASPNET. webhooks. pøijímaèe. GitHub](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.GitHub) poskytuje podporu pro příjem webhooků z GitHubu a [Microsoft. ASPNET. webhooks. pøijímaèe. Custom](https://www.nuget.org/packages?q=Microsoft.AspNet.WebHooks.Receivers.Custom) poskytuje podporu pro příjem webhooků generovaných Webhooky ASP.NET.

V poli můžete najít podporu pro Dropbox, GitHub, MailChimp, PayPal, Pusher, Salesforce, časovou rezervu, proužek, Trello a WordPress, ale je možné podporovat libovolný počet jiných poskytovatelů.

## <a name="configuring-a-webhook-receiver"></a>Konfigurace přijímače Webhooku

Přijímače Webhooku se konfigurují prostřednictvím [IWebHookReceiverConfig](https://github.com/aspnet/WebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/WebHooks/IWebHookReceiverConfig.cs) rozhraní a konkrétní implementace tohoto rozhraní se dají zaregistrovat pomocí modelu injektáže pro vkládání závislostí. Výchozí implementace používá nastavení aplikace, které může být buď nastaveno v souboru Web. config, nebo pokud používáte Azure Web Apps, lze nastavit prostřednictvím webu [Azure Portal](https://portal.azure.com/).

![Nastavení aplikace Azure](_static/AzureAppSettings.png)

Formát pro klíče nastavení aplikace je následující:

```
MS_WebHookReceiverSecret_<receiver>
```

Hodnota je seznam hodnot oddělených čárkami, které odpovídají hodnotám *{ID}* , pro které Webhooky byly registrovány, například:

```
MS_WebHookReceiverSecret_GitHub = <secret1>, 12345=<secret2>, 54321=<secret3>
```

## <a name="initializing-a-webhook-receiver"></a>Inicializuje se přijímač Webhooku.

Přijímače Webhooku jsou inicializovány jejich registrací, obvykle ve statické třídě *WebApiConfig* , například:

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

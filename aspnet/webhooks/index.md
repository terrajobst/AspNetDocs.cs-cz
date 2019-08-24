---
uid: webhooks/index
title: Přehled webhooků ASP.NET | Microsoft Docs
author: rick-anderson
description: Úvod do webhooků ASP.NET
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: aa65a20e1af16d58533e37fafc77ac246e0fe327
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000734"
---
# <a name="aspnet-webhooks-overview"></a><span data-ttu-id="06b87-103">Přehled webhooků ASP.NET</span><span class="sxs-lookup"><span data-stu-id="06b87-103">ASP.NET WebHooks overview</span></span>

<span data-ttu-id="06b87-104">Webhooky je zjednodušený vzor HTTP, který poskytuje jednoduchý model Pub/sub pro zapojení do společné webové rozhraní API a služeb SaaS.</span><span class="sxs-lookup"><span data-stu-id="06b87-104">WebHooks is a lightweight HTTP pattern providing a simple pub/sub model for wiring together Web APIs and SaaS services.</span></span> <span data-ttu-id="06b87-105">Když dojde k události ve službě, pošle se oznámení ve formě požadavku HTTP POST registrovaným předplatitelům.</span><span class="sxs-lookup"><span data-stu-id="06b87-105">When an event happens in a service, a notification is sent in the form of an HTTP POST request to registered subscribers.</span></span> <span data-ttu-id="06b87-106">Požadavek POST obsahuje informace o události, která umožňuje příjemci reagovat odpovídajícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="06b87-106">The POST request contains information about the event which makes it possible for the receiver to act accordingly.</span></span>

<span data-ttu-id="06b87-107">Z důvodu jejich jednoduchosti jsou Webhooky již zveřejněny velkým počtem služeb, včetně Dropboxu [](http://dropbox.com/), [GitHubu](http://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [časové rezervy](http://www.slack.com), prokládaných, [Trello](http://www.trello.com/)a mnoha. [](http://www.stripe.com) aktuálnější.</span><span class="sxs-lookup"><span data-stu-id="06b87-107">Because of their simplicity, WebHooks are already exposed by a large number of services including [Dropbox](http://dropbox.com/), [GitHub](http://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/), and many more.</span></span> <span data-ttu-id="06b87-108">Webhook může například značit, že se soubor změnil v Dropboxu nebo [](http://dropbox.com/)že se změnila Změna kódu na GitHubu, nebo když se v rámci služby [PayPal](http://www.paypal.com/)iniciovala platba nebo byla vytvořena karta v [Trello](http://www.trello.com/).</span><span class="sxs-lookup"><span data-stu-id="06b87-108">For example, a WebHook can indicate that a file has changed in [Dropbox](http://dropbox.com/), or a code change has been committed in GitHub, or a payment has been initiated in [PayPal](http://www.paypal.com/), or a card has been created in [Trello](http://www.trello.com/).</span></span> <span data-ttu-id="06b87-109">Možnosti jsou nekonečné.</span><span class="sxs-lookup"><span data-stu-id="06b87-109">The possibilities are endless!</span></span>

<span data-ttu-id="06b87-110">Microsoft ASP.NET webhookům usnadňuje posílání i příjem webhooků jako součást vaší aplikace ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="06b87-110">Microsoft ASP.NET WebHooks makes it easier to both send and receive WebHooks as part of your ASP.NET application:</span></span>

* <span data-ttu-id="06b87-111">Na straně příjmu poskytuje společný model pro příjem a zpracování webhooků z libovolného počtu zprostředkovatelů webhooků.</span><span class="sxs-lookup"><span data-stu-id="06b87-111">On the receiving side, it provides a common model for receiving and processing WebHooks from any number of WebHook providers.</span></span> <span data-ttu-id="06b87-112">Vychází ze seznamu s podporou Dropboxu, [](http://dropbox.com/)GitHubu [](http://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [časové rezervy](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) a [Zendesk](https://www.zendesk.com/) , ale můžete snadno přidat podporu.</span><span class="sxs-lookup"><span data-stu-id="06b87-112">It comes out of the box with support for [Dropbox](http://dropbox.com/), [GitHub](http://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Slack](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) and [Zendesk](https://www.zendesk.com/) but it is easy to add support for more.</span></span>

* <span data-ttu-id="06b87-113">Na straně odeslání poskytuje podporu pro správu a ukládání předplatných a také pro odesílání oznámení o událostech do správné sady předplatitelů.</span><span class="sxs-lookup"><span data-stu-id="06b87-113">On the sending side it provides support for managing and storing subscriptions as well as for sending event notifications to the right set of subscribers.</span></span> <span data-ttu-id="06b87-114">To vám umožní definovat vlastní sadu událostí, které se předplatitelům můžou přihlásit k odběru a upozorňovat na ně, když k nim dojde.</span><span class="sxs-lookup"><span data-stu-id="06b87-114">This allows you to define your own set of events that subscribers can subscribe to and notify them when things happens.</span></span>

<span data-ttu-id="06b87-115">Tyto dvě části můžete v závislosti na vašem scénáři použít společně nebo odděleně.</span><span class="sxs-lookup"><span data-stu-id="06b87-115">The two parts can be used together or apart depending on your scenario.</span></span> <span data-ttu-id="06b87-116">Pokud potřebujete pouze příjem webhooků z jiných služeb, můžete použít pouze část přijímače. Pokud chcete, aby Webhooky využívaly jenom pro jiné, stačí, když to uděláte.</span><span class="sxs-lookup"><span data-stu-id="06b87-116">If you only need to receive WebHooks from other services then you can use just the receiver part; if you only want to expose WebHooks for others to consume, then you can do just that.</span></span>

<span data-ttu-id="06b87-117">Cílení kódu ASP.NET webové rozhraní API 2 a ASP.NET MVC 5 a je k dispozici jako [OSS na GitHubu](https://github.com/aspnet/WebHooks).</span><span class="sxs-lookup"><span data-stu-id="06b87-117">The code targets ASP.NET Web API 2 and ASP.NET MVC 5 and is available as [OSS on GitHub](https://github.com/aspnet/WebHooks).</span></span>

## <a name="webhooks-overview"></a><span data-ttu-id="06b87-118">Přehled webhooků</span><span class="sxs-lookup"><span data-stu-id="06b87-118">WebHooks Overview</span></span>

<span data-ttu-id="06b87-119">Webhooky je vzor, který znamená, že se liší v tom, jak se používá ze služby k provozu, ale základní nápad je stejný.</span><span class="sxs-lookup"><span data-stu-id="06b87-119">WebHooks is a pattern which means that it varies how it is used from service to service but the basic idea is the same.</span></span> <span data-ttu-id="06b87-120">Webhooky si můžete představit jako jednoduchý model Pub/sub, kde se uživatel může přihlásit k odběru událostí jinde.</span><span class="sxs-lookup"><span data-stu-id="06b87-120">You can think of WebHooks as a simple pub/sub model where a user can subscribe to events happening elsewhere.</span></span> <span data-ttu-id="06b87-121">Oznámení událostí se šíří jako požadavky HTTP POST obsahující informace o samotné události.</span><span class="sxs-lookup"><span data-stu-id="06b87-121">The event notifications are propagated as HTTP POST requests containing information about the event itself.</span></span>

<span data-ttu-id="06b87-122">Požadavek HTTP POST obvykle obsahuje objekt JSON nebo data formuláře HTML určená odesílatelem Webhooku, včetně informací o události, která způsobuje, že se Webhook spustí.</span><span class="sxs-lookup"><span data-stu-id="06b87-122">Typically the HTTP POST request contains a JSON object or HTML form data determined by the WebHook sender including information about the event causing the WebHook to trigger.</span></span> <span data-ttu-id="06b87-123">Například text požadavku POST Webhooku z GitHubu [](http://www.github.com/) vypadá jako v důsledku otevření nového problému v konkrétním úložišti:</span><span class="sxs-lookup"><span data-stu-id="06b87-123">For example, a WebHook POST request body from [GitHub](http://www.github.com/) looks like this as a result of a new issue being opened in a particular repository:</span></span>

```json
{
  "action": "opened",
  "issue": {
      "url": "https://api.github.com/repos/octocat/Hello-World/issues/1347",
      "number": 1347,
      ...
  },
  "repository": {
      "id": 1296269,
      "full_name": "octocat/Hello-World",
      "owner": {
          "login": "octocat",
          "id": 1
          ...
      },
      ...
  },
  "sender": {
      "login": "octocat",
      "id": 1,
      ...
  }
}
```

<span data-ttu-id="06b87-124">Chcete-li zajistit, aby Webhook byl skutečně od zamýšleného odesílatele, je žádost POST zabezpečena způsobem a poté ověřena příjemcem.</span><span class="sxs-lookup"><span data-stu-id="06b87-124">To ensure that the WebHook is indeed from the intended sender, the POST request is secured in some way and then verified by the receiver.</span></span> <span data-ttu-id="06b87-125">Například Webhooky [GitHubu](https://developer.github.com/webhooks/) zahrnují hlavičku HTTP *X-hub-Signature* s hodnotou hash textu žádosti, která je kontrolována implementací příjemce, takže se o ně nemusíte starat.</span><span class="sxs-lookup"><span data-stu-id="06b87-125">For example, [GitHub WebHooks](https://developer.github.com/webhooks/) includes an *X-Hub-Signature* HTTP header with a hash of the request body which is checked by the receiver implementation so you don't have to worry about it.</span></span>

<span data-ttu-id="06b87-126">Tok Webhooku se obecně podobá tomuto:</span><span class="sxs-lookup"><span data-stu-id="06b87-126">The WebHook flow generally goes something like this:</span></span>

* <span data-ttu-id="06b87-127">Odesílatel Webhooku zpřístupňuje události, ke kterým se může klient přihlásit.</span><span class="sxs-lookup"><span data-stu-id="06b87-127">The WebHook sender exposes events that a client can subscribe to.</span></span> <span data-ttu-id="06b87-128">Události popisují pozorovatelné změny v systému, například zda byla vložena nová datová položka, byl dokončen proces nebo něco jiného.</span><span class="sxs-lookup"><span data-stu-id="06b87-128">The events describe observable changes to the system, for example that a new data item has been inserted, that a process has completed, or something else.</span></span>

* <span data-ttu-id="06b87-129">Přihlášení k odběru přijímače Webhooku pomocí registrace Webhooku sestávající ze čtyř věcí:</span><span class="sxs-lookup"><span data-stu-id="06b87-129">The WebHook receiver subscribes by registering a WebHook consisting of four things:</span></span>

     1. <span data-ttu-id="06b87-130">Identifikátor URI, kde má být oznámení o události odesíláno ve formě požadavku HTTP POST;</span><span class="sxs-lookup"><span data-stu-id="06b87-130">A URI for where the event notification should be posted in the form of an HTTP POST request;</span></span>

     2. <span data-ttu-id="06b87-131">Sada filtrů popisujících konkrétní události, pro které by se Webhook měl aktivovat;</span><span class="sxs-lookup"><span data-stu-id="06b87-131">A set of filters describing the particular events for which the WebHook should be fired;</span></span>

     3. <span data-ttu-id="06b87-132">Tajný klíč, který se používá k podepsání požadavku HTTP POST;</span><span class="sxs-lookup"><span data-stu-id="06b87-132">A secret key which is used to sign the HTTP POST request;</span></span>

     4. <span data-ttu-id="06b87-133">Další data, která mají být součástí požadavku HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="06b87-133">Additional data which is to be included in the HTTP POST request.</span></span> <span data-ttu-id="06b87-134">To může být například další pole záhlaví protokolu HTTP nebo vlastnosti, které jsou součástí textu žádosti HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="06b87-134">This can for example be additional HTTP header fields or properties included in the HTTP POST request body.</span></span>

* <span data-ttu-id="06b87-135">Jakmile dojde k události, budou nalezeny vyhovující registrace Webhooku a odešlou se požadavky HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="06b87-135">Once an event happens, the matching WebHook registrations are found and HTTP POST requests are submitted.</span></span> <span data-ttu-id="06b87-136">Obvykle se generování požadavků HTTP POST opakuje několikrát, pokud z nějakého důvodu příjemce neodpovídá nebo požadavek HTTP POST způsobí chybovou odpověď.</span><span class="sxs-lookup"><span data-stu-id="06b87-136">Typically, the generation of the HTTP POST requests are retried several times if for some reason the recipient is not responding or the HTTP POST request results in an error response.</span></span>

## <a name="webhooks-processing-pipeline"></a><span data-ttu-id="06b87-137">Kanál pro zpracování webhooků</span><span class="sxs-lookup"><span data-stu-id="06b87-137">WebHooks Processing Pipeline</span></span>

<span data-ttu-id="06b87-138">Kanál pro zpracování Microsoft ASP.NET webhooků pro příchozí Webhooky vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="06b87-138">The Microsoft ASP.NET WebHooks processing pipeline for incoming WebHooks looks like this:</span></span>

![Kanál pro zpracování webhooků ASP.NET](_static/WebHookReceivers.png)

<span data-ttu-id="06b87-140">Tady jsou tyto dvě klíčové koncepty *přijímače* a *obslužné rutiny*:</span><span class="sxs-lookup"><span data-stu-id="06b87-140">The two key concepts here are *Receivers* and *Handlers*:</span></span>

* <span data-ttu-id="06b87-141">*Přijímače* zodpovídají za zpracování konkrétního charakteru Webhooku od daného odesílatele a pro vynucování kontrol zabezpečení, aby bylo zajištěno, že požadavek Webhooku skutečně pochází od zamýšleného odesílatele.</span><span class="sxs-lookup"><span data-stu-id="06b87-141">*Receivers* are responsible for handling the particular flavor of WebHook from a given sender and for enforcing security checks to ensure that the WebHook request indeed is from the intended sender.</span></span>

* <span data-ttu-id="06b87-142">*Obslužné rutiny* jsou obvykle v případě, kdy uživatelský kód spouští zpracování konkrétního Webhooku.</span><span class="sxs-lookup"><span data-stu-id="06b87-142">*Handlers* are typically where user code runs processing the particular WebHook.</span></span>

<span data-ttu-id="06b87-143">V následujících uzlech jsou tyto koncepty popsány v části Další podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="06b87-143">In the following nodes these concepts are described in more details.</span></span>

---
uid: webhooks/index
title: Přehled webhooků ASP.NET | Microsoft Docs
author: rick-anderson
description: Úvod do webhooků ASP.NET
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5e2843f0-f499-448f-a712-33d4e9858321
ms.openlocfilehash: 1e21c92e950893c0ff87c63f03f4710a158441fd
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075083"
---
# <a name="aspnet-webhooks-overview"></a>Přehled webhooků ASP.NET

Webhooky je zjednodušený vzor HTTP, který poskytuje jednoduchý model Pub/sub pro zapojení do společné webové rozhraní API a služeb SaaS. Když dojde k události ve službě, pošle se oznámení ve formě požadavku HTTP POST registrovaným předplatitelům. Požadavek POST obsahuje informace o události, která umožňuje příjemci reagovat odpovídajícím způsobem.

Z důvodu jejich jednoduchosti jsou Webhooky již zveřejněny velkým počtem služeb, včetně [Dropboxu](http://dropbox.com/), [GitHubu](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [časové rezervy](http://www.slack.com), [prokládaných](http://www.stripe.com), [Trello](http://www.trello.com/)a mnoha dalších. Webhook může například značit, že se soubor změnil v [Dropboxu](http://dropbox.com/)nebo že se změnila Změna kódu na GitHubu, nebo když se v rámci služby [PayPal](http://www.paypal.com/)iniciovala platba nebo byla vytvořena karta v [Trello](http://www.trello.com/). Možnosti jsou nekonečné.

Microsoft ASP.NET webhookům usnadňuje posílání i příjem webhooků jako součást vaší aplikace ASP.NET:

* Na straně příjmu poskytuje společný model pro příjem a zpracování webhooků z libovolného počtu zprostředkovatelů webhooků. Je součástí boxu podpora [Dropboxu](http://dropbox.com/), [GitHubu](https://www.github.com/), [Bitbucket](https://bitbucket.org/), [MailChimp](http://www.mailchimp.com/), [PayPal](http://www.paypal.com/), [Pusher](http://www.pusher.com), [Salesforce](http://www.salesforce.com), [Časová rezerva](http://www.slack.com), [Stripe](http://www.stripe.com), [Trello](http://www.trello.com/),[WordPress](http://www.wordpress.com) a [Zendesk](https://www.zendesk.com/) , ale můžete snadno přidat podporu pro další.

* Na straně odeslání poskytuje podporu pro správu a ukládání předplatných a také pro odesílání oznámení o událostech do správné sady předplatitelů. To vám umožní definovat vlastní sadu událostí, které se předplatitelům můžou přihlásit k odběru a upozorňovat na ně, když k nim dojde.

Tyto dvě části můžete v závislosti na vašem scénáři použít společně nebo odděleně. Pokud potřebujete pouze příjem webhooků z jiných služeb, můžete použít pouze část přijímače. Pokud chcete, aby Webhooky využívaly jenom pro jiné, stačí, když to uděláte.

Cílení kódu ASP.NET webové rozhraní API 2 a ASP.NET MVC 5 a je k dispozici jako [OSS na GitHubu](https://github.com/aspnet/WebHooks).

## <a name="webhooks-overview"></a>Přehled webhooků

Webhooky je vzor, který znamená, že se liší v tom, jak se používá ze služby k provozu, ale základní nápad je stejný. Webhooky si můžete představit jako jednoduchý model Pub/sub, kde se uživatel může přihlásit k odběru událostí jinde. Oznámení událostí se šíří jako požadavky HTTP POST obsahující informace o samotné události.

Požadavek HTTP POST obvykle obsahuje objekt JSON nebo data formuláře HTML určená odesílatelem Webhooku, včetně informací o události, která způsobuje, že se Webhook spustí. Například text požadavku POST Webhooku z [GitHubu](https://www.github.com/) vypadá jako v důsledku otevření nového problému v konkrétním úložišti:

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

Chcete-li zajistit, aby Webhook byl skutečně od zamýšleného odesílatele, je žádost POST zabezpečena způsobem a poté ověřena příjemcem. Například [Webhooky GitHubu](https://developer.github.com/webhooks/) zahrnují hlavičku HTTP *X-hub-Signature* s hodnotou hash textu žádosti, která je kontrolována implementací příjemce, takže se o ně nemusíte starat.

Tok Webhooku se obecně podobá tomuto:

* Odesílatel Webhooku zpřístupňuje události, ke kterým se může klient přihlásit. Události popisují pozorovatelné změny v systému, například zda byla vložena nová datová položka, byl dokončen proces nebo něco jiného.

* Přihlášení k odběru přijímače Webhooku pomocí registrace Webhooku sestávající ze čtyř věcí:

     1. Identifikátor URI, kde má být oznámení o události odesíláno ve formě požadavku HTTP POST;

     2. Sada filtrů popisujících konkrétní události, pro které by se Webhook měl aktivovat;

     3. Tajný klíč, který se používá k podepsání požadavku HTTP POST;

     4. Další data, která mají být součástí požadavku HTTP POST. To může být například další pole záhlaví protokolu HTTP nebo vlastnosti, které jsou součástí textu žádosti HTTP POST.

* Jakmile dojde k události, budou nalezeny vyhovující registrace Webhooku a odešlou se požadavky HTTP POST. Obvykle se generování požadavků HTTP POST opakuje několikrát, pokud z nějakého důvodu příjemce neodpovídá nebo požadavek HTTP POST způsobí chybovou odpověď.

## <a name="webhooks-processing-pipeline"></a>Kanál pro zpracování webhooků

Kanál pro zpracování Microsoft ASP.NET webhooků pro příchozí Webhooky vypadá takto:

![Kanál pro zpracování webhooků ASP.NET](_static/WebHookReceivers.png)

Tady jsou tyto dvě klíčové koncepty *přijímače* a *obslužné rutiny*:

* *Přijímače* zodpovídají za zpracování konkrétního charakteru Webhooku od daného odesílatele a pro vynucování kontrol zabezpečení, aby bylo zajištěno, že požadavek Webhooku skutečně pochází od zamýšleného odesílatele.

* *Obslužné rutiny* jsou obvykle v případě, kdy uživatelský kód spouští zpracování konkrétního Webhooku.

V následujících uzlech jsou tyto koncepty popsány v části Další podrobnosti.

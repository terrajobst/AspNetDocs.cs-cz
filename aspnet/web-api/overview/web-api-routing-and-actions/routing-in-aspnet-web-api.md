---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: Směrování ve webovém rozhraní API ASP.NET | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557608"
---
# <a name="routing-in-aspnet-web-api"></a>Směrování v rozhraní ASP.NET Web API

o [Jan Wasson](https://github.com/MikeWasson)

Tento článek popisuje, jak webové rozhraní API ASP.NET směruje požadavky HTTP na řadiče.

> [!NOTE]
> Pokud jste obeznámeni s ASP.NET MVC, směrování webového rozhraní API se velmi podobá směrování MVC. Hlavní rozdíl spočívá v tom, že webové rozhraní API používá příkaz HTTP, nikoli cestu identifikátoru URI, k výběru akce. Ve webovém rozhraní API můžete také použít směrování ve stylu MVC. Tento článek nepředpokládá žádné znalosti ASP.NET MVC.

## <a name="routing-tables"></a>Směrovací tabulky

Ve webovém rozhraní API ASP.NET je *kontroler* třída, která zpracovává požadavky HTTP. Veřejné metody kontroleru se nazývají *metody akcí* nebo pouhými *akcemi*. Když rozhraní Web API Framework obdrží požadavek, směruje požadavek na akci.

K určení, která akce se má vyvolat, používá rozhraní *směrovací tabulku*. Šablona projektu sady Visual Studio pro webové rozhraní API vytvoří výchozí trasu:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

Tato trasa je definována v souboru *WebApiConfig.cs* , který je umístěn v *aplikaci\_spouštěcí* adresář:

![](routing-in-aspnet-web-api/_static/image1.png)

Další informace o třídě `WebApiConfig` najdete v tématu [Konfigurace webového rozhraní API ASP.NET](../advanced/configuring-aspnet-web-api.md).

Pokud webové rozhraní API sami hostte, musíte nastavit směrovací tabulku přímo na objekt `HttpSelfHostConfiguration`. Další informace najdete v tématu věnovaném [samoobslužnému hostování webového rozhraní API](../older-versions/self-host-a-web-api.md).

Každá položka v tabulce směrování obsahuje *šablonu směrování*. Výchozí šablona trasy pro webové rozhraní API je &quot;API/{Controller}/{ID}&quot;. V této šabloně &quot;rozhraní API&quot; je segment cesty literálu a {Controller} a {ID} jsou zástupné proměnné.

Když rozhraní Web API přijme požadavek HTTP, pokusí se porovnat identifikátor URI s jednou ze šablon směrování ve směrovací tabulce. Pokud neodpovídá žádná trasa, klient obdrží chybu 404. Například následující identifikátory URI odpovídají výchozí trase:

- /api/contacts
- /api/contacts/1
- /api/products/gizmo1

Následující identifikátor URI se však neshoduje, protože nemá&quot; segment &quot;rozhraní API:

- /contacts/1

> [!NOTE]
> Důvodem použití rozhraní API v trase je zamezení kolizí s směrováním ASP.NET MVC. Tímto způsobem můžete mít &quot;/Contacts&quot; přejít na kontroler MVC a &quot;/API/Contacts&quot; přejít na kontroler webového rozhraní API. Samozřejmě, pokud se vám tato konvence nelíbí, můžete změnit výchozí směrovací tabulku.

Po nalezení vyhovující trasy webové rozhraní API vybere kontroler a akci:

- Pokud chcete najít kontroler, webové rozhraní API přidá&quot; kontroleru &quot;k hodnotě proměnné *{Controller}* .
- Pokud chcete najít akci, webové rozhraní API prohlíží příkaz HTTP a pak vyhledá akci, jejíž název začíná tímto názvem příkazu HTTP. Například s požadavkem GET webové rozhraní API vyhledá akci s předponou &quot;získat&quot;, například &quot;GetContact&quot; nebo &quot;GetAllContacts&quot;. Tato konvence se vztahuje pouze na příkazy GET, POST, PUT, DELETE, HEAD, OPTIONS a PATCH. Můžete povolit jiné příkazy HTTP pomocí atributů na řadiči. Později se zobrazí příklad.
- Jiné zástupné proměnné v šabloně směrování, jako je například *{ID},* jsou namapovány na parametry akce.

Pojďme se podívat na příklad. Předpokládejme, že definujete následující kontroler:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

Tady jsou některé možné požadavky HTTP spolu s akcí, která se vyvolá pro každou z těchto možností:

| Příkaz HTTP | Cesta URI | Akce | Parametr |
| --- | --- | --- | --- |
| GET | rozhraní API/produkty | GetAllProducts | *nTato* |
| GET | API/Products/4 | GetProductById | 4 |
| DELETE | API/Products/4 | DeleteProduct | 4 |
| POST | rozhraní API/produkty | *(žádná shoda)* |  |

Všimněte si, že segment *{ID}* identifikátoru URI, pokud je k dispozici, je namapován na parametr *ID* akce. V tomto příkladu kontroler definuje dvě metody GET, jednu s parametrem *ID* a jednu bez parametrů.

Také si všimněte, že požadavek POST selže, protože kontroler nedefinuje metodu &quot;post...&quot;.

## <a name="routing-variations"></a>Variace směrování

Předchozí část popisuje základní mechanismus směrování pro webové rozhraní API ASP.NET. Tato část popisuje některé variace.

### <a name="http-verbs"></a>Příkazy protokolu HTTP

Namísto použití zásad vytváření názvů pro příkazy HTTP můžete explicitně zadat příkaz HTTP pro akci tím, že upravení metodu Action s jedním z následujících atributů:

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

V následujícím příkladu je metoda `FindProduct` namapována na požadavky GET:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

Pro povolení více příkazů HTTP pro akci nebo pro jiné operace HTTP než GET, PUT, POST, DELETE, HEAD, OPTIONS a PATCH použijte atribut `[AcceptVerbs]`, který přebírá seznam příkazů HTTP.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a>Směrování podle názvu akce

S výchozí šablonou směrování používá webové rozhraní API k výběru akce příkaz HTTP. Můžete ale také vytvořit trasu, kde je název akce zahrnutý v identifikátoru URI:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

V této šabloně trasy parametr *{Action}* pojmenuje metodu Action na kontroleru. Pomocí tohoto stylu směrování určete povolené příkazy HTTP pomocí atributů. Předpokládejme například, že řadič má následující metodu:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

V takovém případě se požadavek GET pro "API/Products/Details/1" namapuje na metodu `Details`. Tento styl směrování se podobá ASP.NET MVC a může být vhodný pro rozhraní API ve stylu RPC.

Název akce můžete přepsat pomocí atributu `[ActionName]`. V následujícím příkladu jsou k dispozici dvě akce, které se mapují na &quot;rozhraní API/Products/Miniatura/*ID*. Jedna podporuje GET a druhá podporuje POST:

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a>Bez akcí

Chcete-li zabránit metodě v tom, aby se vyvolala jako akce, použijte atribut `[NonAction]`. Tato signály signalizují rozhraní, že metoda není akcí, i když by jinak odpovídala pravidlům směrování.

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a>Další čtení

Toto téma nabízí podrobný pohled na směrování. Další podrobnosti najdete v tématu [Směrování a výběr akcí](routing-and-action-selection.md), který přesně popisuje, jak architektura odpovídá identifikátoru URI ke směrování, vybere kontroler a pak vybere akci, která se má vyvolat.

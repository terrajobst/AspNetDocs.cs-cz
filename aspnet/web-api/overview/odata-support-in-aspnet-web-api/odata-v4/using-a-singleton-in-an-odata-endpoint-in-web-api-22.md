---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
title: Vytvoření typu Singleton v OData v4 pomocí webového rozhraní API 2,2 | Microsoft Docs
author: rick-anderson
description: V tomto tématu se dozvíte, jak definovat typ singleton v koncovém bodu OData ve webovém rozhraní API 2,2.
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 4064ab14-26ee-4d5c-ae58-1bdda525ad06
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/using-a-singleton-in-an-odata-endpoint-in-web-api-22
msc.type: authoredcontent
ms.openlocfilehash: 218449c18759b306e425c55f8e7b573d837b4658
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622085"
---
# <a name="create-a-singleton-in-odata-v4-using-web-api-22"></a>Vytvoření typu Singleton v OData v4 pomocí webového rozhraní API 2,2

od Zoe Luo

> Obvykle by entita mohla být k dispozici pouze v případě, že byla zapouzdřena v sadě entit. OData v4 ale nabízí dvě další možnosti, singleton a omezení, z nichž WebAPI 2,2 podporuje.

Tento článek ukazuje, jak definovat singleton v koncovém bodu OData ve webovém rozhraní API 2,2. Informace o tom, co je typu Singleton a jakým způsobem vám jeho používání může přinést, najdete v tématu [použití typu Singleton k definování vaší speciální entity](https://blogs.msdn.com/b/odatateam/archive/2014/03/05/use-singleton-to-define-your-special-entity.aspx). Informace o vytvoření koncového bodu OData v4 ve webovém rozhraní API najdete v tématu [Vytvoření koncového bodu OData v4 pomocí webového rozhraní api ASP.NET 2,2](create-an-odata-v4-endpoint.md). 

V projektu webového rozhraní API vytvoříme typ singleton pomocí následujícího datového modelu:

![Datový model](using-a-singleton-in-an-odata-endpoint-in-web-api-22/_static/image1.png)

Typ singleton s názvem `Umbrella` bude definován v závislosti na typu `Company`a v závislosti na typu `Employee`bude definována sada entit s názvem `Employees`.

Řešení použité v tomto kurzu si můžete stáhnout z [webu CodePlex](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/).

## <a name="define-the-data-model"></a>Definování datového modelu

1. Definujte typy CLR.

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample1.cs)]
2. Vygenerujte model EDM na základě typů CLR.

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample2.cs)]

    Zde `builder.Singleton<Company>("Umbrella")` instruuje tvůrce modelů, aby vytvořil typ singleton s názvem `Umbrella` v modelu EDM.

    Vygenerovaná metadata budou vypadat takto:

    [!code-xml[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample3.xml)]

    Z metadat vidíte, že navigační vlastnost `Company` v sadě entit `Employees` je vázána na `Umbrella`typu singleton. Vazba je provedena automaticky `ODataConventionModelBuilder`, protože typ `Company` pouze `Umbrella`. Pokud v modelu dojde k nejednoznačnosti, můžete použít `HasSingletonBinding` k explicitnímu navázání navigační vlastnosti na typ singleton; `HasSingletonBinding` má stejný účinek jako použití atributu `Singleton` v definici typu CLR:

    [!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample4.cs)]

## <a name="define-the-singleton-controller"></a>Definování typu Singleton Controller

Podobně jako u řadiče EntitySet zdědí řadič singleton z `ODataController`a název řadiče singleton by měl být `[singletonName]Controller`.

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample5.cs)]

Aby bylo možné zpracovávat různé druhy požadavků, je nutné v kontroleru předem definovat akce. **Směrování atributů** je ve výchozím nastavení povolené v WebApi 2,2. Chcete-li například definovat akci pro zpracování dotazů `Revenue` z `Company` pomocí směrování atributů, použijte následující:

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample6.cs)]

Pokud nejste ochotni definovat atributy pro každou akci, stačí definovat akce, které následují po [konvencích směrování OData](../odata-routing-conventions.md). Vzhledem k tomu, že klíč není vyžadován pro dotazování typu Singleton, akce definované v řadiči s jedním odkazem se mírně liší od akcí definovaných v řadiči EntitySet.

Pro referenci se v seznamu zobrazí signatury metod pro každou definici akce v řadiči s jedním odkazem.

[!code-csharp[Main](using-a-singleton-in-an-odata-endpoint-in-web-api-22/samples/sample7.cs)]

V podstatě je to vše, co musíte udělat na straně služby. [Ukázkový projekt](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataSingletonSample/) obsahuje veškerý kód pro řešení a klienta OData, který ukazuje, jak použít typ singleton. Klient je sestaven podle kroků v části [vytvoření klientské aplikace OData v4](create-an-odata-v4-client-app.md).

. 

*Díky Leo hu pro původní obsah tohoto článku.*

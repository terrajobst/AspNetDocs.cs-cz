---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
title: Bezpečnostní pokyny pro ASP.NET Web API 2 OData-ASP.NET 4. x
author: MikeWasson
description: Popisuje bezpečnostní problémy, které je potřeba vzít v úvahu při vystavení datové sady prostřednictvím OData pro webové rozhraní API 2 pro ASP.NET ve ASP.NET 4. x.
ms.author: riande
ms.date: 02/06/2013
ms.custom: seoapril2019
ms.assetid: b91e6424-1544-4747-bd0b-d1f8418c9653
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-security-guidance
msc.type: authoredcontent
ms.openlocfilehash: 8194a368cb0629c30e32ec05bf4bed150d442ad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556495"
---
# <a name="security-guidance-for-aspnet-web-api-2-odata"></a>Pokyny k zabezpečení ASP.NET webového rozhraní API 2 OData

o [Jan Wasson](https://github.com/MikeWasson)

Toto téma popisuje některé problémy se zabezpečením, které byste měli zvážit při vystavení datové sady prostřednictvím OData pro webové rozhraní API 2 pro ASP.NET ve ASP.NET 4. x.

## <a name="edm-security"></a>Zabezpečení EDM

Sémantika dotazu je založena na modelu Entity Data Model (EDM), nikoli na podkladových typech modelů. Z datového modelu EDM můžete vyloučit vlastnost, která nebude viditelná pro dotaz. Předpokládejme například, že váš model zahrnuje typ zaměstnance s vlastností mzdy. Tuto vlastnost můžete chtít vyloučit z modelu EDM, aby bylo možné ji skrýt od klientů.

Existují dva způsoby, jak vyloučit vlastnost z modelu EDM. Můžete nastavit atribut **[IgnoreDataMember]** u vlastnosti v třídě modelu:

[!code-csharp[Main](odata-security-guidance/samples/sample1.cs)]

Můžete také odebrat vlastnost z modelu EDM programově:

[!code-csharp[Main](odata-security-guidance/samples/sample2.cs)]

## <a name="query-security"></a>Zabezpečení dotazů

Zlomyslný nebo Naive klient může vytvořit dotaz, který trvá příliš dlouho, než se spustí. V nejhorším případě to může mít za následek nerušený přístup k vaší službě.

Atribut **[Queryable]** je filtr akcí, který analyzuje, ověřuje a aplikuje dotaz. Filtr převede možnosti dotazu na výraz LINQ. Když řadič OData vrátí typ **IQueryable** , poskytovatel **IQueryable** LINQ Převede výraz LINQ na dotaz. Proto výkon závisí na poskytovateli LINQ, který se používá, a také na konkrétní vlastnosti datové sady nebo schématu databáze.

Další informace o použití možností dotazů OData ve webovém rozhraní API ASP.NET najdete v tématu [Podpora možností dotazů OData](supporting-odata-query-options.md).

Pokud víte, že všichni klienti jsou důvěryhodní (například v podnikovém prostředí), nebo pokud je vaše datová sada malá, nemusí se jednat o problém s výkonem dotazů. V opačném případě byste měli zvážit následující doporučení.

- Otestujte službu pomocí různých dotazů a profilujte databázi.
- Povolte stránkování řízené serverem, aby nedošlo k vrácení velkých datových sad v jednom dotazu. Další informace najdete v tématu [stránkování řízené serverem](supporting-odata-query-options.md#server-paging). 

    [!code-csharp[Main](odata-security-guidance/samples/sample3.cs)]
- Potřebujete $filter a $orderby? Některé aplikace mohou umožňovat stránkování klienta pomocí $top a $skip, ale zakazují další možnosti dotazu. 

    [!code-csharp[Main](odata-security-guidance/samples/sample4.cs)]
- Zvažte omezení $orderby na vlastnosti v clusterovaných indexech. Řazení velkých objemů dat bez clusterovaných indexů je pomalé. 

    [!code-csharp[Main](odata-security-guidance/samples/sample5.cs)]
- Maximální počet uzlů: vlastnost **MaxNodeCount** v **[Queryable]** nastaví maximální počet uzlů povolených ve stromu syntaxe $Filter. Výchozí hodnota je 100, ale možná budete chtít nastavit nižší hodnotu, protože velký počet uzlů může být pro zkompilování pomalé. To platí zejména v případě, že používáte LINQ to Objects (tj. dotazy LINQ na kolekci v paměti, bez použití zprostředkujícího poskytovatele LINQ). 

    [!code-csharp[Main](odata-security-guidance/samples/sample6.cs)]
- Zvažte zakázání funkcí any () a All (), protože tyto funkce mohou být pomalé. 

    [!code-csharp[Main](odata-security-guidance/samples/sample7.cs)]
- Pokud některé vlastnosti řetězce obsahují velké řetězce&#8212;, například popis produktu nebo záznam&#8212;blogu, zvažte zakázání funkcí řetězce. 

    [!code-csharp[Main](odata-security-guidance/samples/sample8.cs)]
- Zvažte možnost zakázat filtrování u vlastností navigace. Filtrování vlastností navigace může mít za následek spojení, což může být pomalé v závislosti na schématu databáze. Následující kód ukazuje validátor dotazů, který brání filtrování vlastností navigace. Další informace o validátorech dotazů naleznete v tématu [ověření dotazu](supporting-odata-query-options.md#query-validation). 

    [!code-csharp[Main](odata-security-guidance/samples/sample9.cs)]
- Zvažte omezení $filterch dotazů zápisem ověřovacího modulu, který je přizpůsoben pro vaši databázi. Zvažte například tyto dva dotazy: 

  - Všechny filmy s objekty actor, jejichž příjmení začíná znakem A.
  - Všechny filmy vydané v 1994.

    V případě, že filmy nejsou indexovány aktéry, může první dotaz vyžadovat, aby databázový stroj prohledal celý seznam filmů. Vzhledem k tomu, že druhý dotaz může být přijatelný, předpokládá se, že filmy jsou indexovány v roce vydání.

    Následující kód ukazuje validátor, který umožňuje filtrování vlastností "ReleaseYear" a "title", ale žádné další vlastnosti.

    [!code-csharp[Main](odata-security-guidance/samples/sample10.cs)]
- Obecně zvažte, které $filter funkce potřebujete. Pokud klienti nepotřebují úplné expresivity $filter, můžete povolené funkce omezit.

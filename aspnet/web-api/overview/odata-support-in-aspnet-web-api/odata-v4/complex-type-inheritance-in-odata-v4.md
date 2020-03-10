---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
title: Dědičnost komplexního typu v OData V4 s webovým rozhraním API ASP.NET | Microsoft Docs
author: microsoft
description: Podle specifikace OData v4 může komplexní typ dědit z jiného komplexního typu. (Komplexní typ je strukturovaný typ bez klíče.) Webové rozhraní API...
ms.author: riande
ms.date: 09/16/2014
ms.assetid: a00d3600-9c2a-41bc-9460-06cc527904e2
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/complex-type-inheritance-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 3d90216c8e594055f77577eb6d8b1d978ae4c24d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556306"
---
# <a name="complex-type-inheritance-in-odata-v4-with-aspnet-web-api"></a>Dědičnost komplexního typu v OData V4 s webovým rozhraním API ASP.NET

od [Microsoftu](https://github.com/microsoft)

> Podle [specifikace](http://www.odata.org/documentation/odata-version-4-0/)OData v4 může komplexní typ dědit z jiného komplexního typu. ( *Komplexní* typ je strukturovaný typ bez klíče.) Webové rozhraní API OData 5,3 podporuje dědičnost komplexního typu.
> 
> V tomto tématu se dozvíte, jak vytvořit entity data model (EDM) se složitými typy dědičnosti. Úplný zdrojový kód naleznete v tématu [Ukázka dědičnosti komplexního typu OData](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataComplexTypeInheritanceSample/ReadMe.txt).
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové rozhraní API OData 5,3
> - OData v4

## <a name="model-hierarchy"></a>Hierarchie modelů

K ilustraci dědičnosti komplexního typu používáme následující hierarchii tříd.

![](complex-type-inheritance-in-odata-v4/_static/image1.png)

`Shape` je abstraktní komplexní typ. `Rectangle`, `Triangle`a `Circle` jsou komplexní typy odvozené od `Shape`a `RoundRectangle` jsou odvozeny z `Rectangle`. `Window` je typ entity a obsahuje instanci `Shape`.

Zde jsou třídy CLR, které definují tyto typy.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample1.cs)]

## <a name="build-the-edm-model"></a>Sestavení modelu EDM

Chcete-li vytvořit EDM, můžete použít **ODataConventionModelBuilder**, který odvodí vztahy dědičnosti z typů CLR.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample2.cs)]

Můžete také vytvořit EDM explicitně pomocí **ODataModelBuilder**. Tím se získá více kódu, ale získáte větší kontrolu nad modelem EDM.

[!code-csharp[Main](complex-type-inheritance-in-odata-v4/samples/sample3.cs)]

Tyto dva příklady vytvoří stejné schéma EDM.

## <a name="metadata-document"></a>Dokument metadat

Tady je dokument metadat OData, který ukazuje dědičnost komplexního typu.

[!code-xml[Main](complex-type-inheritance-in-odata-v4/samples/sample4.xml?highlight=13,17,25,30)]

V dokumentu metadat vidíte, že:

- `Shape` komplexní typ je abstraktní.
- Komplexní typ `Rectangle`, `Triangle`a `Circle` mají základní typ `Shape`.
- Typ `RoundRectangle` má `Rectangle`základního typu.

## <a name="casting-complex-types"></a>Přetypování složitých typů

Přetypování na komplexní typy se teď podporuje. Například následující dotaz přetypování `Shape` na `Rectangle`.

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample5.cmd)]

Zde je datová část odpovědi:

[!code-console[Main](complex-type-inheritance-in-odata-v4/samples/sample6.cmd)]

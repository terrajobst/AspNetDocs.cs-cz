---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
title: Otevřené typy v OData V4 s webovým rozhraním API ASP.NET | Microsoft Docs
author: microsoft
description: V OData v4 je otevřený typ strukturovaný typ, který obsahuje dynamické vlastnosti, kromě jakýchkoli vlastností, které jsou deklarovány v definici typu. Otevřít...
ms.author: riande
ms.date: 09/15/2014
ms.assetid: f25f5ac5-4800-4950-abe5-c97750a27fc6
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/use-open-types-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: 950442c071bf50d2c8c1588971f13f85c4891436
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622176"
---
# <a name="open-types-in-odata-v4-with-aspnet-web-api"></a>Otevřené typy v OData V4 s webovým rozhraním API ASP.NET

od [Microsoftu](https://github.com/microsoft)

> V OData v4 je *otevřený typ* strukturovaný typ, který obsahuje dynamické vlastnosti, kromě jakýchkoli vlastností, které jsou deklarovány v definici typu. Otevřené typy umožňují přidat flexibilitu pro vaše datové modely. V tomto kurzu se dozvíte, jak používat otevřené typy v ASP.NET webového rozhraní API OData.
> 
> V tomto kurzu se předpokládá, že už víte, jak ve webovém rozhraní API ASP.NET vytvořit koncový bod OData. Pokud ne, začněte načtením a nejprve [vytvořte koncový bod OData v4](create-an-odata-v4-endpoint.md) .
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové rozhraní API OData 5,3
> - OData v4

Nejdřív některé terminologie OData:

- Typ entity: strukturovaný typ s klíčem.
- Komplexní typ: strukturovaný typ bez klíče.
- Typ otevřeného typu: typ s dynamickými vlastnostmi. Je možné otevřít oba typy entit a komplexní typy.

Hodnotou dynamické vlastnosti může být primitivní typ, komplexní typ nebo Výčtový typ. nebo kolekci některého z těchto typů. Další informace o otevřených typech najdete v tématu [specifikace OData v4](http://www.odata.org/documentation/odata-version-4-0/).

## <a name="install-the-web-odata-libraries"></a>Instalace webových knihoven OData

Pomocí Správce balíčků NuGet nainstalujte nejnovější knihovny Web API OData. V okně konzoly Správce balíčků:

[!code-console[Main](use-open-types-in-odata-v4/samples/sample1.cmd)]

## <a name="define-the-clr-types"></a>Definování typů CLR

Začněte tím, že definujete modely EDM jako typy CLR.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample2.cs)]

Při vytvoření model EDM (Entity Data Model) (EDM),

- `Category` je typ výčtu.
- `Address` je komplexní typ. (Nemá klíč, takže se nejedná o typ entity.)
- `Customer` je typ entity. (Obsahuje klíč.)
- `Press` je otevřený komplexní typ.
- `Book` je otevřený typ entity.

Chcete-li vytvořit otevřený typ, musí mít typ CLR vlastnost typu `IDictionary<string, object>`, která obsahuje dynamické vlastnosti.

## <a name="build-the-edm-model"></a>Sestavení modelu EDM

Použijete-li **ODataConventionModelBuilder** k vytvoření EDM, `Press` a `Book` jsou automaticky přidány jako otevřené typy, a to na základě přítomnosti vlastnosti `IDictionary<string, object>`.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample3.cs)]

Můžete také vytvořit EDM explicitně pomocí **ODataModelBuilder**.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample4.cs)]

## <a name="add-an-odata-controller"></a>Přidat kontroler OData

Dále přidejte kontroler OData. Pro účely tohoto kurzu budeme používat zjednodušený kontroler, který podporuje jenom požadavky GET a POST a používá seznam v paměti k ukládání entit.

[!code-csharp[Main](use-open-types-in-odata-v4/samples/sample5.cs)]

Všimněte si, že první instance `Book` nemá žádné dynamické vlastnosti. Druhá instance `Book` má následující dynamické vlastnosti:

- "Publikováno": primitivní typ
- "Autoři": kolekce primitivních typů
- "OtherCategories": kolekce typů výčtu.

Vlastnost `Press` této instance `Book` má také následující dynamické vlastnosti:

- "Blog": primitivní typ
- "Adresa": komplexní typ

## <a name="query-the-metadata"></a>Dotazování na metadata

K získání dokumentu metadat OData odešlete požadavek GET na `~/$metadata`. Text odpovědi by měl vypadat nějak takto:

[!code-xml[Main](use-open-types-in-odata-v4/samples/sample6.xml?highlight=5,21)]

V dokumentu metadat vidíte, že:

- U typů `Book` a `Press` je hodnota atributu `OpenType` true. Typy `Customer` a `Address` nemají tento atribut.
- Typ entity `Book` obsahuje tři deklarované vlastnosti: ISBN, title a Press. Metadata OData neobsahují vlastnost `Book.Properties` z třídy CLR.
- Podobně `Press` komplexní typ obsahuje pouze dvě deklarované vlastnosti: název a kategorie. Metadata neobsahují vlastnost `Press.DynamicProperties` z třídy CLR.

## <a name="query-an-entity"></a>Dotazování entity

Pokud chcete získat knihu se symbolem ISBN rovnající se "978-0-7356-7942-9", odešlete požadavek GET na `~/Books('978-0-7356-7942-9')`. Tělo odpovědi by mělo vypadat podobně jako následující. (Odsazené tak, aby se čitelnější.)

[!code-console[Main](use-open-types-in-odata-v4/samples/sample7.cmd?highlight=8-13,15-23)]

Všimněte si, že dynamické vlastnosti jsou zahrnuty jako vložené s deklarovanými vlastnostmi.

## <a name="post-an-entity"></a>PUBLIKOVÁNÍ entity

Chcete-li přidat entitu knihy, odešlete požadavek POST na `~/Books`. Klient může v datové části požadavku nastavit dynamické vlastnosti.

Tady je příklad žádosti. Poznamenejte si vlastnosti Price a Publikováno.

[!code-console[Main](use-open-types-in-odata-v4/samples/sample8.cmd?highlight=10)]

Pokud nastavíte zarážku v metodě kontroleru, vidíte, že webové rozhraní API přidalo tyto vlastnosti do slovníku `Properties`.

![](use-open-types-in-odata-v4/_static/image1.png)

## <a name="additional-resources"></a>Další prostředky

[Ukázka otevřeného typu OData](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v4/ODataOpenTypeSample/ReadMe.txt)

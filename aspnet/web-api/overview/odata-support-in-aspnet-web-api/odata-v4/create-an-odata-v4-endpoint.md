---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
title: Vytvoření koncového bodu OData v4 pomocí webového rozhraní API ASP.NET 2,2 | Microsoft Docs
author: MikeWasson
description: Protokol OData (Open Data Protocol) je protokol pro přístup k datům pro web. OData poskytuje jednotný způsob dotazování a manipulace s datovými sadami prostřednictvím operací CRUD...
ms.author: riande
ms.date: 01/23/2019
ms.assetid: 1e1927c0-ded1-4752-80fd-a146628d2f09
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-endpoint
msc.type: authoredcontent
ms.openlocfilehash: 81d134cbd3231b9a0d5537ccbd1bbfe6419254af
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598733"
---
# <a name="create-an-odata-v4-endpoint-using-aspnet-web-api"></a>Vytvoření koncového bodu OData v4 pomocí webového rozhraní API ASP.NET 

> Protokol OData (Open Data Protocol) je protokol pro přístup k datům pro web. OData poskytuje jednotný způsob dotazování a manipulace s datovými sadami prostřednictvím operací CRUD (vytvoření, čtení, aktualizace a odstranění).
>
> Webové rozhraní API ASP.NET podporuje V3 i v4 protokolu. Můžete dokonce i koncový bod v4, který běží souběžně s koncovým bodem v3.
>
> V tomto kurzu se dozvíte, jak vytvořit koncový bod OData v4, který podporuje operace CRUD.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
>
> - Webové rozhraní API 5,2
> - OData v4
> - Visual Studio 2017 ( [tady si můžete](https://visualstudio.microsoft.com/downloads/)stáhnout visual Studio 2017)
> - Entity Framework 6
> - .NET 4.7.2
>
> ## <a name="tutorial-versions"></a>Verze kurzů
>
> Informace o OData verze 3 najdete v tématu [Vytvoření koncového bodu OData V3](../odata-v3/creating-an-odata-endpoint.md).

## <a name="create-the-visual-studio-project"></a>Vytvoření projektu sady Visual Studio

V aplikaci Visual Studio v nabídce **soubor** vyberte **Nový** &gt; **projekt**.

Rozbalte položku **nainstalované** &gt;  **C# Visual** &gt; **Web**a vyberte šablonu **Webová aplikace ASP.NET (.NET Framework)** . Pojmenujte projekt &quot;ProductService&quot;.

[![](create-an-odata-v4-endpoint/_static/image7.png)](create-an-odata-v4-endpoint/_static/image7.png)

Vyberte **OK**.

[![](create-an-odata-v4-endpoint/_static/image8.png)](create-an-odata-v4-endpoint/_static/image8.png)

Vyberte **prázdnou** šablonu. V části **Přidat složky a základní reference pro:** vyberte **webové rozhraní API**. Vyberte **OK**.

## <a name="install-the-odata-packages"></a>Instalace balíčků OData

V nabídce **nástroje** vyberte **správce balíčků NuGet** &gt; **konzolu Správce balíčků**. V okně konzoly Správce balíčků zadejte:

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample1.cmd)]

Tento příkaz nainstaluje nejnovější balíčky NuGet pro OData.

## <a name="add-a-model-class"></a>Přidejte třídu modelu

*Model* je objekt, který představuje datovou entitu v aplikaci.

V Průzkumník řešení klikněte pravým tlačítkem na složku modely. V místní nabídce vyberte **přidat** &gt; **třídy**.

[![](create-an-odata-v4-endpoint/_static/image6.png)](create-an-odata-v4-endpoint/_static/image5.png)

> [!NOTE]
> Podle konvence jsou třídy modelu umístěny do složky modelů, ale nemusíte postupovat podle této konvence ve svých vlastních projektech.

Pojmenujte `Product`třídy. V souboru Product.cs nahraďte často používaný kód následujícím kódem:

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample2.cs)]

Vlastnost `Id` je klíč entity. Klienti můžou zadávat dotazy na entity podle klíče. Chcete-li například získat produkt s ID 5, je identifikátor URI `/Products(5)`. Vlastnost `Id` bude také primárním klíčem v back-endové databázi.

## <a name="enable-entity-framework"></a>Povolit Entity Framework

V tomto kurzu použijeme Entity Framework (EF) Code First k vytvoření back-endové databáze.

> [!NOTE]
> Rozhraní Web API OData nevyžaduje EF. Použijte jakoukoli vrstvu přístupu k datům, která dokáže překládat databázové entity do modelů.

Nejdřív nainstalujte balíček NuGet pro EF. V nabídce **nástroje** vyberte **správce balíčků NuGet** &gt; **konzolu Správce balíčků**. V okně konzoly Správce balíčků zadejte:

[!code-console[Main](create-an-odata-v4-endpoint/samples/sample3.cmd)]

Otevřete soubor Web. config a přidejte následující oddíl do **konfiguračního** elementu za prvek **configSections** .

[!code-xml[Main](create-an-odata-v4-endpoint/samples/sample4.xml?highlight=6)]

Toto nastavení přidá připojovací řetězec pro databázi LocalDB. Tato databáze se použije, když aplikaci spouštíte místně.

Dále do složky modely přidejte třídu s názvem `ProductsContext`:

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample5.cs)]

V konstruktoru `"name=ProductsContext"` poskytuje název připojovacího řetězce.

## <a name="configure-the-odata-endpoint"></a>Konfigurace koncového bodu OData

Otevřete soubor App\_Start/WebApiConfig. cs. Přidejte následující příkazy **using** :

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample6.cs)]

Pak do metody **registru** přidejte následující kód:

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample7.cs)]

Tento kód provede dvě věci:

- Vytvoří model EDM (Entity Data Model) (EDM).
- Přidá trasu.

EDM je abstraktní model dat. Model EDM slouží k vytvoření dokumentu metadat služby. Třída **ODataConventionModelBuilder** vytvoří EDM pomocí výchozích konvencí pojmenování. Tento přístup vyžaduje nejméně kód. Pokud chcete mít větší kontrolu nad modelem EDM, můžete pomocí třídy **ODataModelBuilder** vytvořit EDM přidáním vlastností, klíčů a vlastností navigace explicitně.

*Trasa* oznamuje webovému rozhraní API, jak SMĚROVAT požadavky HTTP na koncový bod. Chcete-li vytvořit trasu OData v4, zavolejte metodu rozšíření **MapODataServiceRoute** .

Pokud má vaše aplikace více koncových bodů OData, vytvořte pro každou z nich samostatnou trasu. Udělte každé trase jedinečný název a předponu trasy.

## <a name="add-the-odata-controller"></a>Přidat kontroler OData

*Kontroler* je třída, která zpracovává požadavky HTTP. Pro každou sadu entit ve službě OData vytvoříte samostatný kontroler. V tomto kurzu vytvoříte pro entitu `Product` jeden kontroler.

V Průzkumník řešení klikněte pravým tlačítkem myši na složku Controllers a vyberte **přidat** &gt; **třídu**. Pojmenujte `ProductsController`třídy.

> [!NOTE]
> Verze tohoto kurzu pro OData V3 používá rozhraní **Add controllering** . V současné době neexistuje pro OData v4 žádné generování uživatelského rozhraní.

Pomocí následujícího kódu nahraďte často používaný kód v ProductsController.cs.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample8.cs)]

Řadič používá třídu `ProductsContext` pro přístup k databázi pomocí EF. Všimněte si, že kontroler přepisuje metodu **Dispose** pro uvolnění **ProductsContext**.

Toto je výchozí bod pro kontroler. Dále přidáme metody pro všechny operace CRUD.

## <a name="query-the-entity-set"></a>Dotazování sady entit

Přidejte následující metody pro `ProductsController`.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample9.cs)]

Verze `Get` metody bez parametrů vrací celou kolekci Products. Metoda `Get` s parametrem *Key* vyhledává produkt podle jeho klíče (v tomto případě vlastnost `Id`).

Atribut **[EnableQuery]** umožňuje klientům upravit dotaz pomocí možností dotazu, jako je $filter, $sort a $Page. Další informace najdete v tématu [Podpora možností dotazů OData](../supporting-odata-query-options.md).

## <a name="add-an-entity-to-the-entity-set"></a>Přidat entitu do sady entit

Chcete-li povolit klientům přidat do databáze nový produkt, přidejte následující metodu pro `ProductsController`.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample10.cs)]

## <a name="update-an-entity"></a>Aktualizace entity

OData podporuje dvě odlišná sémantika pro aktualizaci entity, opravy a vložení.

- Oprava provede částečnou aktualizaci. Klient Určuje pouze vlastnosti, které se mají aktualizovat.
- PUT nahradí celou entitu.

Nevýhodou PUT je, že klient musí odesílat hodnoty všech vlastností v entitě, včetně hodnot, které se nemění. [Specifikace OData](http://docs.oasis-open.org/odata/odata/v4.0/os/part1-protocol/odata-v4.0-os-part1-protocol.html#_Toc372793719) uvádí, že oprava je upřednostňovaná.

V každém případě je zde uveden kód pro metodu PATCH i PUT:

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample11.cs)]

V případě opravy používá kontroler **&gt;typu rozdíl&lt;t** ke sledování změn.

## <a name="delete-an-entity"></a>Odstranění entity

Chcete-li povolit klientům odstranit produkt z databáze nástroje, přidejte následující metodu pro `ProductsController`.

[!code-csharp[Main](create-an-odata-v4-endpoint/samples/sample12.cs)]

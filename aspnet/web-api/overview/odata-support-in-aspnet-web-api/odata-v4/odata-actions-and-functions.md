---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: Akce a funkce v OData v4 pomocí webového rozhraní API ASP.NET 2,2 | Microsoft Docs
author: MikeWasson
description: V rámci OData představují akce a funkce způsob, jak přidat chování na straně serveru, která nejsou snadno definovaná jako operace CRUD u entit. V tomto kurzu se dozvíte, jak...
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: f5af94e93e5b7f2351d40febbf1a468d635c9db1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556222"
---
# <a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a>Akce a funkce v OData v4 pomocí webového rozhraní API ASP.NET 2,2

o [Jan Wasson](https://github.com/MikeWasson)

> V rámci OData představují akce a funkce způsob, jak přidat chování na straně serveru, která nejsou snadno definovaná jako operace CRUD u entit. V tomto kurzu se dozvíte, jak přidat akce a funkce do koncového bodu OData v4 pomocí webového rozhraní API 2,2. Kurz sestaví na kurzu [Vytvoření koncového bodu OData v4 pomocí webového rozhraní API 2 ASP.NET](create-an-odata-v4-endpoint.md) .
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
>
> - Webové rozhraní API 2,2
> - OData v4
> - Visual Studio 2013 (Stáhněte si Visual Studio 2017 [tady](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))
> - .NET 4.5
>
> ## <a name="tutorial-versions"></a>Verze kurzů
>
> Pro OData verze 3 se podívejte [na téma akce OData ve webovém rozhraní API 2 pro ASP.NET](../odata-v3/odata-actions.md).

Rozdíl mezi *akcemi* a *funkcemi* je, že akce mohou mít vedlejší účinky a funkce ne. Akce a funkce mohou vracet data. Mezi tato použití pro akce patří:

- Komplexní transakce.
- Manipulace s několika entitami najednou.
- Povoluje se aktualizace pouze některých vlastností entity.
- Odesílají se data, která nejsou entitou.

Funkce jsou užitečné pro vracení informací, které neodpovídají přímo entitě nebo kolekci.

Akce (nebo funkce) může cílit na jednu entitu nebo kolekci. V terminologii OData je to *vazba*. Můžete mít také &quot;nevázané&quot; akce nebo funkce, které se nazývají jako statické operace ve službě.

## <a name="example-adding-an-action"></a>Příklad: Přidání akce

Pojďme definovat akci pro hodnocení produktu.

> [!NOTE]
> Tento kurz sestaví v kurzu [Vytvoření koncového bodu OData v4 pomocí webového rozhraní API 2 ASP.NET](create-an-odata-v4-endpoint.md) .

Nejdřív přidejte `ProductRating` model, který bude reprezentovat hodnocení.

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

Přidejte také **negenerickými** do třídy `ProductsContext`, aby EF vytvořil v databázi tabulku hodnocení.

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a>Přidat akci do modelu EDM

Do WebApiConfig.cs přidejte následující kód:

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

Metoda **EntityTypeConfiguration. Action** přidá akci do modelu Entity Data Model (EDM). Metoda **parametru** určuje typový parametr pro akci.

Tento kód také nastaví obor názvů pro EDM. Obor názvů záleží na tom, že identifikátor URI pro akci obsahuje plně kvalifikovaný název akce:

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> V typické konfiguraci služby IIS bude tečka v této adrese URL způsobit, že služba IIS vrátí chybu 404. Můžete to vyřešit přidáním následujícího oddílu do souboru Web. config:

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a>Přidat metodu kontroleru pro akci

Pokud chcete povolit akci&quot; &quot;míry, přidejte do `ProductsController`následující metodu:

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

Všimněte si, že název metody se shoduje s názvem akce. Atribut **[HTTPPOST]** určuje způsob, jakým je metoda HTTP POST.

K vyvolání akce klient odešle požadavek HTTP POST podobný následujícímu:

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

Akce &quot;míra&quot; je vázána na instance produktu, takže identifikátor URI pro akci je plně kvalifikovaný název akce připojený k identifikátoru URI entity. (Odvoláme, že obor názvů EDM nastavíme na &quot;ProductService&quot;, takže plně kvalifikovaný název akce je &quot;ProductService. Rate&quot;.)

Tělo požadavku obsahuje parametry akce jako datovou část JSON. Webové rozhraní API automaticky převede datovou část JSON na objekt **ODataActionParameters** , což je pouze slovník hodnot parametrů. Tento slovník použijte pro přístup k parametrům v metodě kontroleru.

Pokud klient odešle parametry akce v nesprávném formátu, hodnota **ModelState. IsValid** je false. Ověřte tento příznak v metodě kontroleru a vraťte chybu, pokud je vlastnost **IsValid** false.

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a>Příklad: Přidání funkce

Nyní přidáme funkci OData, která vrátí nejlevnější produkt. Stejně jako dřív je prvním krokem přidání funkce do modelu EDM. Do WebApiConfig.cs přidejte následující kód.

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

V tomto případě je funkce vázána na kolekci Products, nikoli na jednotlivé instance produktu. Klienti vyvolávají funkci odesláním žádosti o získání:

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

Toto je metoda kontroleru pro tuto funkci:

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

Všimněte si, že název metody se shoduje s názvem funkce. Atribut **[HttpGet]** určuje metodu metodou GET protokolu HTTP.

Toto je odpověď HTTP:

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a>Příklad: Přidání nevázané funkce

Předchozí příklad byl funkce vázaný na kolekci. V tomto dalším příkladu vytvoříme *nevázanou* funkci. Nevázané funkce se volají jako statické operace ve službě. Funkce v tomto příkladu vrátí daň z prodeje pro daný poštovní směrovací číslo.

Do souboru WebApiConfig Přidejte funkci do modelu EDM:

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

Všimněte si, že voláme **Functions** přímo na **ODataModelBuilder**místo typu entity nebo kolekce. Tvůrce modelu tak informuje, že funkce není vázaná.

Zde je metoda kontroleru, která implementuje funkci:

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

Nezáleží na tom, který řídicí řadič webového rozhraní API tuto metodu umístí. Můžete ji umístit do `ProductsController`nebo definovat samostatný kontroler. Atribut **[ODataRoute]** definuje šablonu identifikátoru URI pro funkci.

Tady je příklad žádosti klienta:

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

Odpověď HTTP:

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]

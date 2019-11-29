---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
title: 'Část 2: vytvoření doménových modelů | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: fe3ef85f-bdc6-4e10-9768-25aa565c01d0
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
msc.type: authoredcontent
ms.openlocfilehash: 7c5ed1bdb4b390c94907b14e208231f16ad42d96
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600357"
---
# <a name="part-2-creating-the-domain-models"></a><span data-ttu-id="52f9d-102">Část 2: vytvoření doménových modelů</span><span class="sxs-lookup"><span data-stu-id="52f9d-102">Part 2: Creating the Domain Models</span></span>

<span data-ttu-id="52f9d-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="52f9d-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="52f9d-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="52f9d-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-models"></a><span data-ttu-id="52f9d-105">Přidat modely</span><span class="sxs-lookup"><span data-stu-id="52f9d-105">Add Models</span></span>

<span data-ttu-id="52f9d-106">Existují tři způsoby přístupu k Entity Framework:</span><span class="sxs-lookup"><span data-stu-id="52f9d-106">There are three ways to approach Entity Framework:</span></span>

- <span data-ttu-id="52f9d-107">Databáze – první: začnete s databází a Entity Framework generuje kód.</span><span class="sxs-lookup"><span data-stu-id="52f9d-107">Database-first: You start with a database, and Entity Framework generates the code.</span></span>
- <span data-ttu-id="52f9d-108">Model – první: začnete s vizuálním modelem a Entity Framework generuje databázi i kód.</span><span class="sxs-lookup"><span data-stu-id="52f9d-108">Model-first: You start with a visual model, and Entity Framework generates both the database and code.</span></span>
- <span data-ttu-id="52f9d-109">First Code: Začněte s kódem a Entity Framework vygeneruje databázi.</span><span class="sxs-lookup"><span data-stu-id="52f9d-109">Code-first: You start with code, and Entity Framework generates the database.</span></span>

<span data-ttu-id="52f9d-110">Používáme přístup k prvnímu kódu, takže začneme definováním našich objektů domény jako POCOs (objekty CLR ve starém Old).</span><span class="sxs-lookup"><span data-stu-id="52f9d-110">We are using the code-first approach, so we start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="52f9d-111">V případě přístupu k prvnímu kódu objekty domény nepotřebují žádný další kód pro podporu databázové vrstvy, jako jsou transakce nebo trvalost.</span><span class="sxs-lookup"><span data-stu-id="52f9d-111">With the code-first approach, domain objects don't need any extra code to support the database layer, such as transactions or persistence.</span></span> <span data-ttu-id="52f9d-112">(Konkrétně není nutné dědit od třídy [objektů EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) .) K řízení způsobu, jakým Entity Framework vytváří schéma databáze, můžete i nadále používat datové poznámky.</span><span class="sxs-lookup"><span data-stu-id="52f9d-112">(Specifically, they do not need to inherit from the [EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) class.) You can still use data annotations to control how Entity Framework creates the database schema.</span></span>

<span data-ttu-id="52f9d-113">Vzhledem k tomu, že POCOs neobsahují žádné další vlastnosti, které popisují [stav databáze](https://msdn.microsoft.com/library/system.data.entitystate.aspx), mohou být snadno serializovány do formátu JSON nebo XML.</span><span class="sxs-lookup"><span data-stu-id="52f9d-113">Because POCOs do not carry any extra properties that describe [database state](https://msdn.microsoft.com/library/system.data.entitystate.aspx), they can easily be serialized to JSON or XML.</span></span> <span data-ttu-id="52f9d-114">To ale znamená, že byste měli vždy zveřejnit vaše Entity Framework modely přímo na klienty, jak uvidíme později v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="52f9d-114">However, that does not mean you should always expose your Entity Framework models directly to clients, as we'll see later in the tutorial.</span></span>

<span data-ttu-id="52f9d-115">Vytvoříme následující POCOs:</span><span class="sxs-lookup"><span data-stu-id="52f9d-115">We will create the following POCOs:</span></span>

- <span data-ttu-id="52f9d-116">Produkt</span><span class="sxs-lookup"><span data-stu-id="52f9d-116">Product</span></span>
- <span data-ttu-id="52f9d-117">Za</span><span class="sxs-lookup"><span data-stu-id="52f9d-117">Order</span></span>
- <span data-ttu-id="52f9d-118">OrderDetail</span><span class="sxs-lookup"><span data-stu-id="52f9d-118">OrderDetail</span></span>

<span data-ttu-id="52f9d-119">Chcete-li vytvořit každou třídu, klikněte pravým tlačítkem myši na složku modely v Průzkumník řešení.</span><span class="sxs-lookup"><span data-stu-id="52f9d-119">To create each class, right-click the Models folder in Solution Explorer.</span></span> <span data-ttu-id="52f9d-120">V místní nabídce vyberte **Přidat** a pak vyberte **Třída.**</span><span class="sxs-lookup"><span data-stu-id="52f9d-120">From the context menu, select **Add** and then select **Class.**</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image1.png)

<span data-ttu-id="52f9d-121">Přidejte třídu `Product` s následující implementací:</span><span class="sxs-lookup"><span data-stu-id="52f9d-121">Add a `Product` class with the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample1.cs)]

<span data-ttu-id="52f9d-122">Podle konvence Entity Framework používá vlastnost `Id` jako primární klíč a mapuje ji na sloupec identity v tabulce databáze.</span><span class="sxs-lookup"><span data-stu-id="52f9d-122">By convention, Entity Framework uses the `Id` property as the primary key and maps it to an identity column in the database table.</span></span> <span data-ttu-id="52f9d-123">Když vytvoříte novou instanci `Product`, nenastavíte hodnotu pro `Id`, protože databáze generuje hodnotu.</span><span class="sxs-lookup"><span data-stu-id="52f9d-123">When you create a new `Product` instance, you won't set a value for `Id`, because the database generates the value.</span></span>

<span data-ttu-id="52f9d-124">Atribut **ScaffoldColumn** určuje, že ASP.NET MVC přeskočí vlastnost `Id` při generování formuláře editoru.</span><span class="sxs-lookup"><span data-stu-id="52f9d-124">The **ScaffoldColumn** attribute tells ASP.NET MVC to skip the `Id` property when generating an editor form.</span></span> <span data-ttu-id="52f9d-125">**Požadovaný** atribut se používá k ověření modelu.</span><span class="sxs-lookup"><span data-stu-id="52f9d-125">The **Required** attribute is used to validate the model.</span></span> <span data-ttu-id="52f9d-126">Určuje, že vlastnost `Name` musí být neprázdný řetězec.</span><span class="sxs-lookup"><span data-stu-id="52f9d-126">It specifies that the `Name` property must be a non-empty string.</span></span>

<span data-ttu-id="52f9d-127">Přidejte třídu `Order`:</span><span class="sxs-lookup"><span data-stu-id="52f9d-127">Add the `Order` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample2.cs)]

<span data-ttu-id="52f9d-128">Přidejte třídu `OrderDetail`:</span><span class="sxs-lookup"><span data-stu-id="52f9d-128">Add the `OrderDetail` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample3.cs)]

## <a name="foreign-key-relations"></a><span data-ttu-id="52f9d-129">Vztahy cizího klíče</span><span class="sxs-lookup"><span data-stu-id="52f9d-129">Foreign Key Relations</span></span>

<span data-ttu-id="52f9d-130">Jedna objednávka obsahuje mnoho podrobností objednávky a jednotlivé podrobnosti objednávky se vztahují na jeden produkt.</span><span class="sxs-lookup"><span data-stu-id="52f9d-130">An order contains many order details, and each order detail refers to a single product.</span></span> <span data-ttu-id="52f9d-131">Pro reprezentaci těchto vztahů třída `OrderDetail` definuje vlastnosti pojmenované `OrderId` a `ProductId`.</span><span class="sxs-lookup"><span data-stu-id="52f9d-131">To represent these relations, the `OrderDetail` class defines properties named `OrderId` and `ProductId`.</span></span> <span data-ttu-id="52f9d-132">Entity Framework odvodí, že tyto vlastnosti reprezentují cizí klíče, a přidá do databáze omezení pro cizí klíč.</span><span class="sxs-lookup"><span data-stu-id="52f9d-132">Entity Framework will infer that these properties represent foreign keys, and will add foreign-key constraints to the database.</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image2.png)

<span data-ttu-id="52f9d-133">Třídy `Order` a `OrderDetail` také zahrnují "navigační" vlastnosti, které obsahují odkazy na související objekty.</span><span class="sxs-lookup"><span data-stu-id="52f9d-133">The `Order` and `OrderDetail` classes also include "navigation" properties, which contain references to the related objects.</span></span> <span data-ttu-id="52f9d-134">V pořadí podle vlastností navigace můžete přejít na produkty v pořadí.</span><span class="sxs-lookup"><span data-stu-id="52f9d-134">Given an order, you can navigate to the products in the order by following the navigation properties.</span></span>

<span data-ttu-id="52f9d-135">Zkompilujte projekt nyní.</span><span class="sxs-lookup"><span data-stu-id="52f9d-135">Compile the project now.</span></span> <span data-ttu-id="52f9d-136">Entity Framework používá reflexi ke zjištění vlastností modelů, takže vyžaduje zkompilované sestavení pro vytvoření schématu databáze.</span><span class="sxs-lookup"><span data-stu-id="52f9d-136">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

## <a name="configure-the-media-type-formatters"></a><span data-ttu-id="52f9d-137">Konfigurace formátovacích modulů typu média</span><span class="sxs-lookup"><span data-stu-id="52f9d-137">Configure the Media-Type Formatters</span></span>

<span data-ttu-id="52f9d-138">[Formátovací modul typu Media](../../formats-and-model-binding/media-formatters.md) je objekt, který serializace data při zápisu textu odpovědi HTTP do webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="52f9d-138">A [media-type formatter](../../formats-and-model-binding/media-formatters.md) is an object that serializes your data when Web API writes the HTTP response body.</span></span> <span data-ttu-id="52f9d-139">Vestavěné formátovací moduly podporují výstup JSON a XML.</span><span class="sxs-lookup"><span data-stu-id="52f9d-139">The built-in formatters support JSON and XML output.</span></span> <span data-ttu-id="52f9d-140">Ve výchozím nastavení oba tyto formátovací moduly serializovat všechny objekty podle hodnoty.</span><span class="sxs-lookup"><span data-stu-id="52f9d-140">By default, both of these formatters serialize all objects by value.</span></span>

<span data-ttu-id="52f9d-141">Při serializaci hodnotou se vytvoří problém, pokud graf objektu obsahuje cyklické odkazy.</span><span class="sxs-lookup"><span data-stu-id="52f9d-141">Serialization by value creates a problem if an object graph contains circular references.</span></span> <span data-ttu-id="52f9d-142">To je přesně případ u tříd `Order` a `OrderDetail`, protože každá z nich obsahuje odkaz na druhou.</span><span class="sxs-lookup"><span data-stu-id="52f9d-142">That's exactly the case with the `Order` and `OrderDetail` classes, because each holds a reference to the other.</span></span> <span data-ttu-id="52f9d-143">Formátování bude následovat po odkazech, psaní každého objektu podle hodnoty a jít v kruzích.</span><span class="sxs-lookup"><span data-stu-id="52f9d-143">The formatter will follow the references, writing each object by value, and go in circles.</span></span> <span data-ttu-id="52f9d-144">Proto musíme změnit výchozí chování.</span><span class="sxs-lookup"><span data-stu-id="52f9d-144">Therefore, we need to change the default behavior.</span></span>

<span data-ttu-id="52f9d-145">V Průzkumník řešení rozbalte složku App\_Start Folder a otevřete soubor s názvem WebApiConfig.cs.</span><span class="sxs-lookup"><span data-stu-id="52f9d-145">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="52f9d-146">Do `WebApiConfig` třídy přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="52f9d-146">Add the following code to the `WebApiConfig` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample4.cs?highlight=11)]

<span data-ttu-id="52f9d-147">Tento kód nastaví formátovací modul JSON tak, aby zachoval odkazy na objekty, a odstraní formátovací modul XML z kanálu zcela.</span><span class="sxs-lookup"><span data-stu-id="52f9d-147">This code sets the JSON formatter to preserve object references, and removes the XML formatter from the pipeline entirely.</span></span> <span data-ttu-id="52f9d-148">(Formátovací modul XML můžete nastavit tak, aby zachoval odkazy na objekty, ale je to trochu víc práce a pro tuto aplikaci potřebujeme JSON.</span><span class="sxs-lookup"><span data-stu-id="52f9d-148">(You can configure the XML formatter to preserve object references, but it's a little more work, and we only need JSON for this application.</span></span> <span data-ttu-id="52f9d-149">Další informace naleznete v tématu [zpracování cyklických odkazů na objekty](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).)</span><span class="sxs-lookup"><span data-stu-id="52f9d-149">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="52f9d-150">[Předchozí](using-web-api-with-entity-framework-part-1.md)
> [Další](using-web-api-with-entity-framework-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="52f9d-150">[Previous](using-web-api-with-entity-framework-part-1.md)
[Next](using-web-api-with-entity-framework-part-3.md)</span></span>

---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-5
title: Vytvořit objekty Přenos dat (DTO) | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 0fd07176-b74b-48f0-9fac-0f02e3ffa213
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-5
msc.type: authoredcontent
ms.openlocfilehash: fc0463420207eba764014b8ec7123c5150e38247
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557349"
---
# <a name="create-data-transfer-objects-dtos"></a><span data-ttu-id="61f40-102">Vytvoření objektů pro přenos dat (DTO)</span><span class="sxs-lookup"><span data-stu-id="61f40-102">Create Data Transfer Objects (DTOs)</span></span>

<span data-ttu-id="61f40-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="61f40-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="61f40-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="61f40-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="61f40-105">Teď naše webové rozhraní API zpřístupňuje entity databáze klientovi.</span><span class="sxs-lookup"><span data-stu-id="61f40-105">Right now, our web API exposes the database entities to the client.</span></span> <span data-ttu-id="61f40-106">Klient obdrží data, která se mapují přímo k tabulkám databáze.</span><span class="sxs-lookup"><span data-stu-id="61f40-106">The client receives data that maps directly to your database tables.</span></span> <span data-ttu-id="61f40-107">To však není vždy dobrý nápad.</span><span class="sxs-lookup"><span data-stu-id="61f40-107">However, that's not always a good idea.</span></span> <span data-ttu-id="61f40-108">Někdy budete chtít změnit tvar dat odesílaných klientovi.</span><span class="sxs-lookup"><span data-stu-id="61f40-108">Sometimes you want to change the shape of the data that you send to client.</span></span> <span data-ttu-id="61f40-109">Můžete například potřebovat:</span><span class="sxs-lookup"><span data-stu-id="61f40-109">For example, you might want to:</span></span>

- <span data-ttu-id="61f40-110">Odebrat cyklické odkazy (viz předchozí část).</span><span class="sxs-lookup"><span data-stu-id="61f40-110">Remove circular references (see previous section).</span></span>
- <span data-ttu-id="61f40-111">Skryjte konkrétní vlastnosti, které klienti nemají zobrazovat.</span><span class="sxs-lookup"><span data-stu-id="61f40-111">Hide particular properties that clients are not supposed to view.</span></span>
- <span data-ttu-id="61f40-112">Vynechejte některé vlastnosti, aby se snížila velikost datové části.</span><span class="sxs-lookup"><span data-stu-id="61f40-112">Omit some properties in order to reduce payload size.</span></span>
- <span data-ttu-id="61f40-113">Ploché grafy objektů obsahující vnořené objekty, aby byly lépe praktické pro klienty.</span><span class="sxs-lookup"><span data-stu-id="61f40-113">Flatten object graphs that contain nested objects, to make them more convenient for clients.</span></span>
- <span data-ttu-id="61f40-114">Vyhněte se chybám při "přeúčtování".</span><span class="sxs-lookup"><span data-stu-id="61f40-114">Avoid "over-posting" vulnerabilities.</span></span> <span data-ttu-id="61f40-115">(Viz [ověření modelu](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) pro diskuzi o převzetí služeb při selhání.)</span><span class="sxs-lookup"><span data-stu-id="61f40-115">(See [Model Validation](../../formats-and-model-binding/model-validation-in-aspnet-web-api.md) for a discussion of over-posting.)</span></span>
- <span data-ttu-id="61f40-116">Oddělit vrstvu služby od vaší databázové vrstvy.</span><span class="sxs-lookup"><span data-stu-id="61f40-116">Decouple your service layer from your database layer.</span></span>

<span data-ttu-id="61f40-117">K tomu můžete definovat *objekt pro přenos dat* (DTO).</span><span class="sxs-lookup"><span data-stu-id="61f40-117">To accomplish this, you can define a *data transfer object* (DTO).</span></span> <span data-ttu-id="61f40-118">DTO je objekt, který definuje, jak budou data odesílána přes síť.</span><span class="sxs-lookup"><span data-stu-id="61f40-118">A DTO is an object that defines how the data will be sent over the network.</span></span> <span data-ttu-id="61f40-119">Pojďme se podívat, jak to funguje s entitou Book.</span><span class="sxs-lookup"><span data-stu-id="61f40-119">Let's see how that works with the Book entity.</span></span> <span data-ttu-id="61f40-120">Ve složce modely přidejte dvě třídy DTO:</span><span class="sxs-lookup"><span data-stu-id="61f40-120">In the Models folder, add two DTO classes:</span></span>

[!code-csharp[Main](part-5/samples/sample1.cs)]

<span data-ttu-id="61f40-121">Třída `BookDetailDto` zahrnuje všechny vlastnosti z modelu knihy, s výjimkou toho, že `AuthorName` je řetězec, který bude obsahovat jméno autora.</span><span class="sxs-lookup"><span data-stu-id="61f40-121">The `BookDetailDto` class includes all of the properties from the Book model, except that `AuthorName` is a string that will hold the author name.</span></span> <span data-ttu-id="61f40-122">Třída `BookDto` obsahuje podmnožinu vlastností z `BookDetailDto`.</span><span class="sxs-lookup"><span data-stu-id="61f40-122">The `BookDto` class contains a subset of properties from `BookDetailDto`.</span></span>

<span data-ttu-id="61f40-123">Dále nahraďte dvě metody GET ve třídě `BooksController`, s verzemi, které vracejí DTO.</span><span class="sxs-lookup"><span data-stu-id="61f40-123">Next, replace the two GET methods in the `BooksController` class, with versions that return DTOs.</span></span> <span data-ttu-id="61f40-124">Použijeme příkaz LINQ **Select** pro převod z entit z knihy na DTO.</span><span class="sxs-lookup"><span data-stu-id="61f40-124">We'll use the LINQ **Select** statement to convert from Book entities into DTOs.</span></span>

[!code-csharp[Main](part-5/samples/sample2.cs)]

<span data-ttu-id="61f40-125">Zde je příkaz SQL generovaný novou `GetBooks` metodou.</span><span class="sxs-lookup"><span data-stu-id="61f40-125">Here is the SQL generated by the new `GetBooks` method.</span></span> <span data-ttu-id="61f40-126">Vidíte, že EF překládá výraz LINQ **Select** do příkazu SQL SELECT.</span><span class="sxs-lookup"><span data-stu-id="61f40-126">You can see that EF translates the LINQ **Select** into a SQL SELECT statement.</span></span>

[!code-sql[Main](part-5/samples/sample3.sql)]

<span data-ttu-id="61f40-127">Nakonec upravte metodu `PostBook` tak, aby vracela hodnotu DTO.</span><span class="sxs-lookup"><span data-stu-id="61f40-127">Finally, modify the `PostBook` method to return a DTO.</span></span>

[!code-csharp[Main](part-5/samples/sample4.cs)]

> [!NOTE]
> <span data-ttu-id="61f40-128">V tomto kurzu převádíme ručně na DTO v kódu.</span><span class="sxs-lookup"><span data-stu-id="61f40-128">In this tutorial, we're converting to DTOs manually in code.</span></span> <span data-ttu-id="61f40-129">Další možností je použít knihovnu, jako je automatické [mapovače](http://automapper.org/) , která automaticky zpracovává převod.</span><span class="sxs-lookup"><span data-stu-id="61f40-129">Another option is to use a library like [AutoMapper](http://automapper.org/) that handles the conversion automatically.</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="61f40-130">[Předchozí](part-4.md)
> [Další](part-6.md)</span><span class="sxs-lookup"><span data-stu-id="61f40-130">[Previous](part-4.md)
[Next](part-6.md)</span></span>

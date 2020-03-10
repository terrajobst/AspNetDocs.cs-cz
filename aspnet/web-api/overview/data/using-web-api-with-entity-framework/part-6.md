---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: Vytvoření klienta JavaScriptu | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: 74f2cc4e5e401d690042b05b028dfc0c46ae282a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622344"
---
# <a name="create-the-javascript-client"></a><span data-ttu-id="03bdd-102">Vytvoření javascriptového klienta</span><span class="sxs-lookup"><span data-stu-id="03bdd-102">Create the JavaScript Client</span></span>

<span data-ttu-id="03bdd-103">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="03bdd-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="03bdd-104">Stáhnout dokončený projekt</span><span class="sxs-lookup"><span data-stu-id="03bdd-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="03bdd-105">V této části vytvoříte klienta pro aplikaci pomocí HTML, JavaScriptu a knihovny [vykrojení. js](http://knockoutjs.com/) .</span><span class="sxs-lookup"><span data-stu-id="03bdd-105">In this section, you will create the client for the application, using HTML, JavaScript, and the [Knockout.js](http://knockoutjs.com/) library.</span></span> <span data-ttu-id="03bdd-106">Vytvoříme klientskou aplikaci ve fázích:</span><span class="sxs-lookup"><span data-stu-id="03bdd-106">We'll build the client app in stages:</span></span>

- <span data-ttu-id="03bdd-107">Zobrazuje se seznam knih.</span><span class="sxs-lookup"><span data-stu-id="03bdd-107">Showing a list of books.</span></span>
- <span data-ttu-id="03bdd-108">Zobrazení podrobností knihy.</span><span class="sxs-lookup"><span data-stu-id="03bdd-108">Showing a book detail.</span></span>
- <span data-ttu-id="03bdd-109">Přidává se nová kniha.</span><span class="sxs-lookup"><span data-stu-id="03bdd-109">Adding a new book.</span></span>

<span data-ttu-id="03bdd-110">Knihovna vykrojení používá vzor Model-View-ViewModel (MVVM):</span><span class="sxs-lookup"><span data-stu-id="03bdd-110">The Knockout library uses the Model-View-ViewModel (MVVM) pattern:</span></span>

- <span data-ttu-id="03bdd-111">**Model** je reprezentace dat v obchodní doméně (v našem případě v knihách a autorech) na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="03bdd-111">The **model** is the server-side representation of the data in the business domain (in our case, books and authors).</span></span>
- <span data-ttu-id="03bdd-112">**Zobrazení** je prezentační vrstva (HTML).</span><span class="sxs-lookup"><span data-stu-id="03bdd-112">The **view** is the presentation layer (HTML).</span></span>
- <span data-ttu-id="03bdd-113">**Model zobrazení** je objekt JavaScriptu, který obsahuje modely.</span><span class="sxs-lookup"><span data-stu-id="03bdd-113">The **view model** is a JavaScript object that holds the models.</span></span> <span data-ttu-id="03bdd-114">Model zobrazení je abstrakcí kódu uživatelského rozhraní.</span><span class="sxs-lookup"><span data-stu-id="03bdd-114">The view model is a code abstraction of the UI.</span></span> <span data-ttu-id="03bdd-115">Neobsahuje žádné znalosti reprezentace HTML.</span><span class="sxs-lookup"><span data-stu-id="03bdd-115">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="03bdd-116">Místo toho představuje abstraktní funkce zobrazení, například &quot;seznam knih&quot;.</span><span class="sxs-lookup"><span data-stu-id="03bdd-116">Instead, it represents abstract features of the view, such as &quot;a list of books&quot;.</span></span>

<span data-ttu-id="03bdd-117">Zobrazení je vázáno na data pro model zobrazení.</span><span class="sxs-lookup"><span data-stu-id="03bdd-117">The view is data-bound to the view model.</span></span> <span data-ttu-id="03bdd-118">Aktualizace modelu zobrazení se automaticky projeví v zobrazení.</span><span class="sxs-lookup"><span data-stu-id="03bdd-118">Updates to the view model are automatically reflected in the view.</span></span> <span data-ttu-id="03bdd-119">Model zobrazení také načítá události ze zobrazení, například kliknutí na tlačítko.</span><span class="sxs-lookup"><span data-stu-id="03bdd-119">The view model also gets events from the view, such as button clicks.</span></span>

![](part-6/_static/image1.png)

<span data-ttu-id="03bdd-120">Tento přístup usnadňuje změnu rozložení a uživatelského rozhraní vaší aplikace, protože můžete změnit vazby bez nutnosti přepisovat kód.</span><span class="sxs-lookup"><span data-stu-id="03bdd-120">This approach makes it easy to change the layout and UI of your app, because you can change the bindings, without rewriting any code.</span></span> <span data-ttu-id="03bdd-121">Můžete například zobrazit seznam položek jako `<ul>`a pak ho později změnit na tabulku.</span><span class="sxs-lookup"><span data-stu-id="03bdd-121">For example, you might show a list of items as a `<ul>`, then change it later to a table.</span></span>

## <a name="add-the-knockout-library"></a><span data-ttu-id="03bdd-122">Přidat vyseknutí knihovny</span><span class="sxs-lookup"><span data-stu-id="03bdd-122">Add the Knockout Library</span></span>

<span data-ttu-id="03bdd-123">V aplikaci Visual Studio v nabídce **nástroje** vyberte **Správce balíčků NuGet**.</span><span class="sxs-lookup"><span data-stu-id="03bdd-123">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**.</span></span> <span data-ttu-id="03bdd-124">Pak vyberte **Konzola správce balíčků**.</span><span class="sxs-lookup"><span data-stu-id="03bdd-124">Then select **Package Manager Console**.</span></span> <span data-ttu-id="03bdd-125">V okně konzoly Správce balíčků zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="03bdd-125">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-6/samples/sample1.cmd)]

<span data-ttu-id="03bdd-126">Tento příkaz přidá soubory vykrojení do složky Scripts.</span><span class="sxs-lookup"><span data-stu-id="03bdd-126">This command adds the Knockout files to the Scripts folder.</span></span>

## <a name="create-the-view-model"></a><span data-ttu-id="03bdd-127">Vytvoření modelu zobrazení</span><span class="sxs-lookup"><span data-stu-id="03bdd-127">Create the View Model</span></span>

<span data-ttu-id="03bdd-128">Do složky Scripts přidejte soubor JavaScriptu s názvem App. js.</span><span class="sxs-lookup"><span data-stu-id="03bdd-128">Add a JavaScript file named app.js to the Scripts folder.</span></span> <span data-ttu-id="03bdd-129">(V Průzkumník řešení klikněte pravým tlačítkem myši na složku skripty, vyberte **Přidat**a pak vyberte **soubor JavaScriptu**.) Vložte následující kód:</span><span class="sxs-lookup"><span data-stu-id="03bdd-129">(In Solution Explorer, right-click the Scripts folder, select **Add**, then select **JavaScript File**.) Paste in the following code:</span></span>

[!code-javascript[Main](part-6/samples/sample2.js)]

<span data-ttu-id="03bdd-130">V vykrojení třída `observable` povoluje datovou vazbu.</span><span class="sxs-lookup"><span data-stu-id="03bdd-130">In Knockout, the `observable` class enables data-binding.</span></span> <span data-ttu-id="03bdd-131">Když obsah pozorovatelované změny, pozorovatelně upozorní všechny ovládací prvky vázané na data, aby se mohly aktualizovat sami.</span><span class="sxs-lookup"><span data-stu-id="03bdd-131">When the contents of an observable change, the observable notifies all of the data-bound controls, so they can update themselves.</span></span> <span data-ttu-id="03bdd-132">(Třída `observableArray` je verze pole, která se má *propozorovatelit*.) Aby bylo možné začít s, náš model zobrazení má dva observables:</span><span class="sxs-lookup"><span data-stu-id="03bdd-132">(The `observableArray` class is the array version of *observable*.) To start with, our view model has two observables:</span></span>

- <span data-ttu-id="03bdd-133">`books` obsahuje seznam knih.</span><span class="sxs-lookup"><span data-stu-id="03bdd-133">`books` holds the list of books.</span></span>
- <span data-ttu-id="03bdd-134">`error` obsahuje chybovou zprávu, pokud se volání jazyka AJAX nezdařilo.</span><span class="sxs-lookup"><span data-stu-id="03bdd-134">`error` contains an error message if an AJAX call fails.</span></span>

<span data-ttu-id="03bdd-135">Metoda `getAllBooks` provede volání AJAX pro získání seznamu knih.</span><span class="sxs-lookup"><span data-stu-id="03bdd-135">The `getAllBooks` method makes an AJAX call to get the list of books.</span></span> <span data-ttu-id="03bdd-136">Poté výsledek vloží do pole `books`.</span><span class="sxs-lookup"><span data-stu-id="03bdd-136">Then it pushes the result onto the `books` array.</span></span>

<span data-ttu-id="03bdd-137">Metoda `ko.applyBindings` je součástí knihovny vyseknutí.</span><span class="sxs-lookup"><span data-stu-id="03bdd-137">The `ko.applyBindings` method is part of the Knockout library.</span></span> <span data-ttu-id="03bdd-138">Převezme model zobrazení jako parametr a nastaví datovou vazbu.</span><span class="sxs-lookup"><span data-stu-id="03bdd-138">It takes the view model as a parameter and sets up the data binding.</span></span>

## <a name="add-a-script-bundle"></a><span data-ttu-id="03bdd-139">Přidání sady skriptů</span><span class="sxs-lookup"><span data-stu-id="03bdd-139">Add a Script Bundle</span></span>

<span data-ttu-id="03bdd-140">Sdružování je funkce v ASP.NET 4,5, která usnadňuje kombinování nebo rozčlenění více souborů do jednoho souboru.</span><span class="sxs-lookup"><span data-stu-id="03bdd-140">Bundling is a feature in ASP.NET 4.5 that makes it easy to combine or bundle multiple files into a single file.</span></span> <span data-ttu-id="03bdd-141">Sdružování snižuje počet požadavků na server, což může zlepšit dobu načítání stránky.</span><span class="sxs-lookup"><span data-stu-id="03bdd-141">Bundling reduces the number of requests to the server, which can improve page load time.</span></span>

<span data-ttu-id="03bdd-142">Otevřete soubor App\_Start/BundleConfig. cs.</span><span class="sxs-lookup"><span data-stu-id="03bdd-142">Open the file App\_Start/BundleConfig.cs.</span></span> <span data-ttu-id="03bdd-143">Do metody RegisterBundles přidejte následující kód.</span><span class="sxs-lookup"><span data-stu-id="03bdd-143">Add the following code to the RegisterBundles method.</span></span>

[!code-csharp[Main](part-6/samples/sample3.cs)]

> [!div class="step-by-step"]
> <span data-ttu-id="03bdd-144">[Předchozí](part-5.md)
> [Další](part-7.md)</span><span class="sxs-lookup"><span data-stu-id="03bdd-144">[Previous](part-5.md)
[Next](part-7.md)</span></span>

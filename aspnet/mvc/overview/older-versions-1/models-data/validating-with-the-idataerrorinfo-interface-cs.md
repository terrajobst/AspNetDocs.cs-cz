---
uid: mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
title: Ověřování pomocí rozhraní IDataErrorInfo (C#) | Microsoft Docs
author: StephenWalther
description: Stephen Walther ukazuje, jak zobrazit chybové zprávy vlastního ověřování implementací rozhraní IDataErrorInfo v třídě modelu.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 4733b9f1-9999-48fb-8b73-6038fbcc5ecb
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-the-idataerrorinfo-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: 938b180da02b1963acffd021d18621d75d1d0447
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542558"
---
# <a name="validating-with-the-idataerrorinfo-interface-c"></a><span data-ttu-id="d5181-103">Ověřování v rozhraní IDataErrorInfo (C#)</span><span class="sxs-lookup"><span data-stu-id="d5181-103">Validating with the IDataErrorInfo Interface (C#)</span></span>

<span data-ttu-id="d5181-104">od [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="d5181-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="d5181-105">Stephen Walther ukazuje, jak zobrazit chybové zprávy vlastního ověřování implementací rozhraní IDataErrorInfo v třídě modelu.</span><span class="sxs-lookup"><span data-stu-id="d5181-105">Stephen Walther shows you how to display custom validation error messages by implementing the IDataErrorInfo interface in a model class.</span></span>

<span data-ttu-id="d5181-106">Cílem tohoto kurzu je vysvětlit jeden přístup k provádění ověřování v aplikaci ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="d5181-106">The goal of this tutorial is to explain one approach to performing validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="d5181-107">Naučíte se, jak zabránit odeslání formuláře HTML bez zadání hodnot pro požadovaná pole formuláře.</span><span class="sxs-lookup"><span data-stu-id="d5181-107">You learn how to prevent someone from submitting an HTML form without providing values for required form fields.</span></span> <span data-ttu-id="d5181-108">V tomto kurzu se naučíte provádět ověřování pomocí rozhraní IErrorDataInfo.</span><span class="sxs-lookup"><span data-stu-id="d5181-108">In this tutorial, you learn how to perform validation by using the IErrorDataInfo interface.</span></span>

## <a name="assumptions"></a><span data-ttu-id="d5181-109">Předpoklady</span><span class="sxs-lookup"><span data-stu-id="d5181-109">Assumptions</span></span>

<span data-ttu-id="d5181-110">V tomto kurzu použijeme databázi MoviesDB a databázovou tabulku filmů.</span><span class="sxs-lookup"><span data-stu-id="d5181-110">In this tutorial, I'll use the MoviesDB database and the Movies database table.</span></span> <span data-ttu-id="d5181-111">Tato tabulka obsahuje následující sloupce:</span><span class="sxs-lookup"><span data-stu-id="d5181-111">This table has the following columns:</span></span>

<a id="0.5_table01"></a>

| <span data-ttu-id="d5181-112">**Název sloupce**</span><span class="sxs-lookup"><span data-stu-id="d5181-112">**Column Name**</span></span> | <span data-ttu-id="d5181-113">**Datový typ**</span><span class="sxs-lookup"><span data-stu-id="d5181-113">**Data Type**</span></span> | <span data-ttu-id="d5181-114">**Povoluje hodnoty null.**</span><span class="sxs-lookup"><span data-stu-id="d5181-114">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="d5181-115">ID</span><span class="sxs-lookup"><span data-stu-id="d5181-115">Id</span></span> | <span data-ttu-id="d5181-116">Int</span><span class="sxs-lookup"><span data-stu-id="d5181-116">Int</span></span> | <span data-ttu-id="d5181-117">False</span><span class="sxs-lookup"><span data-stu-id="d5181-117">False</span></span> |
| <span data-ttu-id="d5181-118">Název</span><span class="sxs-lookup"><span data-stu-id="d5181-118">Title</span></span> | <span data-ttu-id="d5181-119">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="d5181-119">Nvarchar(100)</span></span> | <span data-ttu-id="d5181-120">False</span><span class="sxs-lookup"><span data-stu-id="d5181-120">False</span></span> |
| <span data-ttu-id="d5181-121">Ředitel</span><span class="sxs-lookup"><span data-stu-id="d5181-121">Director</span></span> | <span data-ttu-id="d5181-122">Nvarchar(100)</span><span class="sxs-lookup"><span data-stu-id="d5181-122">Nvarchar(100)</span></span> | <span data-ttu-id="d5181-123">False</span><span class="sxs-lookup"><span data-stu-id="d5181-123">False</span></span> |
| <span data-ttu-id="d5181-124">DateReleased</span><span class="sxs-lookup"><span data-stu-id="d5181-124">DateReleased</span></span> | <span data-ttu-id="d5181-125">DateTime</span><span class="sxs-lookup"><span data-stu-id="d5181-125">DateTime</span></span> | <span data-ttu-id="d5181-126">False</span><span class="sxs-lookup"><span data-stu-id="d5181-126">False</span></span> |

<span data-ttu-id="d5181-127">V tomto kurzu použijeme Microsoft Entity Framework k vygenerování tříd databázového modelu.</span><span class="sxs-lookup"><span data-stu-id="d5181-127">In this tutorial, I use the Microsoft Entity Framework to generate my database model classes.</span></span> <span data-ttu-id="d5181-128">Třída Movie vygenerovaná Entity Framework je zobrazena na obrázku 1.</span><span class="sxs-lookup"><span data-stu-id="d5181-128">The Movie class generated by the Entity Framework is displayed in Figure 1.</span></span>

<span data-ttu-id="d5181-129">[![entitě video](validating-with-the-idataerrorinfo-interface-cs/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="d5181-129">[![The Movie entity](validating-with-the-idataerrorinfo-interface-cs/_static/image1.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image1.png)</span></span>

<span data-ttu-id="d5181-130">**Obrázek 01**: entita video ([kliknutím zobrazíte obrázek v plné velikosti](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="d5181-130">**Figure 01**: The Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image2.png))</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="d5181-131">Další informace o použití Entity Framework k vygenerování tříd databázového modelu naleznete v tématu můj kurz s názvem vytváření tříd modelu pomocí Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="d5181-131">To learn more about using the Entity Framework to generate your database model classes, see my tutorial entitled Creating Model Classes with the Entity Framework.</span></span>

## <a name="the-controller-class"></a><span data-ttu-id="d5181-132">Třída Controller</span><span class="sxs-lookup"><span data-stu-id="d5181-132">The Controller Class</span></span>

<span data-ttu-id="d5181-133">K vypsání filmů a vytváření nových filmů používáme domovský kontroler.</span><span class="sxs-lookup"><span data-stu-id="d5181-133">We use the Home controller to list movies and create new movies.</span></span> <span data-ttu-id="d5181-134">Kód pro tuto třídu je obsažen v seznamu 1.</span><span class="sxs-lookup"><span data-stu-id="d5181-134">The code for this class is contained in Listing 1.</span></span>

<span data-ttu-id="d5181-135">**Výpis 1 – souboru controllers\homecontroller.cs**</span><span class="sxs-lookup"><span data-stu-id="d5181-135">**Listing 1 - Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample1.cs)]

<span data-ttu-id="d5181-136">Třída domovského kontroleru v seznamu 1 obsahuje dvě akce Create ().</span><span class="sxs-lookup"><span data-stu-id="d5181-136">The Home controller class in Listing 1 contains two Create() actions.</span></span> <span data-ttu-id="d5181-137">První akce zobrazí formulář HTML pro vytvoření nového filmu.</span><span class="sxs-lookup"><span data-stu-id="d5181-137">The first action displays the HTML form for creating a new movie.</span></span> <span data-ttu-id="d5181-138">Druhá akce Create () provede vlastní vložení nového videa do databáze.</span><span class="sxs-lookup"><span data-stu-id="d5181-138">The second Create() action performs the actual insert of the new movie into the database.</span></span> <span data-ttu-id="d5181-139">Druhá akce Create () je vyvolána, když je formulář zobrazený první akcí Create () na server.</span><span class="sxs-lookup"><span data-stu-id="d5181-139">The second Create() action is invoked when the form displayed by the first Create() action is submitted to the server.</span></span>

<span data-ttu-id="d5181-140">Všimněte si, že druhá akce Create () obsahuje následující řádky kódu:</span><span class="sxs-lookup"><span data-stu-id="d5181-140">Notice that the second Create() action contains the following lines of code:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample2.cs)]

<span data-ttu-id="d5181-141">Vlastnost IsValid vrátí hodnotu false, pokud dojde k chybě ověřování.</span><span class="sxs-lookup"><span data-stu-id="d5181-141">The IsValid property returns false when there is a validation error.</span></span> <span data-ttu-id="d5181-142">V takovém případě se zobrazí znovu zobrazení vytvořit, které obsahuje formulář HTML pro vytvoření filmu.</span><span class="sxs-lookup"><span data-stu-id="d5181-142">In that case, the Create view that contains the HTML form for creating a movie is redisplayed.</span></span>

## <a name="creating-a-partial-class"></a><span data-ttu-id="d5181-143">Vytvoření částečné třídy</span><span class="sxs-lookup"><span data-stu-id="d5181-143">Creating a Partial Class</span></span>

<span data-ttu-id="d5181-144">Třída Movie je vygenerována Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="d5181-144">The Movie class is generated by the Entity Framework.</span></span> <span data-ttu-id="d5181-145">Pokud rozbalíte soubor MoviesDBModel. edmx v okně Průzkumník řešení a otevřete soubor MoviesDBModel.Designer.cs v editoru kódu (viz obrázek 2), můžete zobrazit kód pro třídu filmu.</span><span class="sxs-lookup"><span data-stu-id="d5181-145">You can see the code for the Movie class if you expand the MoviesDBModel.edmx file in the Solution Explorer window and open the MoviesDBModel.Designer.cs file in the Code Editor (see Figure 2).</span></span>

<span data-ttu-id="d5181-146">[![kódu pro entitu video](validating-with-the-idataerrorinfo-interface-cs/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="d5181-146">[![The code for the Movie entity](validating-with-the-idataerrorinfo-interface-cs/_static/image2.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image3.png)</span></span>

<span data-ttu-id="d5181-147">**Obrázek 02**: kód pro entitu video ([kliknutím zobrazíte obrázek v plné velikosti](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="d5181-147">**Figure 02**: The code for the Movie entity([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image4.png))</span></span>

<span data-ttu-id="d5181-148">Třída Movie je částečnou třídou.</span><span class="sxs-lookup"><span data-stu-id="d5181-148">The Movie class is a partial class.</span></span> <span data-ttu-id="d5181-149">To znamená, že můžeme přidat další částečnou třídu se stejným názvem, aby bylo možné roztáhnout funkce třídy video.</span><span class="sxs-lookup"><span data-stu-id="d5181-149">That means that we can add another partial class with the same name to extend the functionality of the Movie class.</span></span> <span data-ttu-id="d5181-150">Do nové dílčí třídy přidáme naši logiku ověřování.</span><span class="sxs-lookup"><span data-stu-id="d5181-150">We'll add our validation logic to the new partial class.</span></span>

<span data-ttu-id="d5181-151">Přidejte třídu v seznamu 2 do složky modely.</span><span class="sxs-lookup"><span data-stu-id="d5181-151">Add the class in Listing 2 to the Models folder.</span></span>

<span data-ttu-id="d5181-152">**Výpis 2 – Models\Movie.cs**</span><span class="sxs-lookup"><span data-stu-id="d5181-152">**Listing 2 - Models\Movie.cs**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample3.cs)]

<span data-ttu-id="d5181-153">Všimněte si, že třída v seznamu 2 obsahuje *částečný* modifikátor.</span><span class="sxs-lookup"><span data-stu-id="d5181-153">Notice that the class in Listing 2 includes the *partial* modifier.</span></span> <span data-ttu-id="d5181-154">Jakékoli metody nebo vlastnosti, které přidáte do této třídy, se stanou součástí třídy filmu vygenerované Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="d5181-154">Any methods or properties that you add to this class become part of the Movie class generated by the Entity Framework.</span></span>

## <a name="adding-onchanging-and-onchanged-partial-methods"></a><span data-ttu-id="d5181-155">Přidávají se částečné metody s jednou změnou a při změně.</span><span class="sxs-lookup"><span data-stu-id="d5181-155">Adding OnChanging and OnChanged Partial Methods</span></span>

<span data-ttu-id="d5181-156">Když Entity Framework generuje třídu entity, Entity Framework automaticky přidá částečné metody do třídy.</span><span class="sxs-lookup"><span data-stu-id="d5181-156">When the Entity Framework generates an entity class, the Entity Framework adds partial methods to the class automatically.</span></span> <span data-ttu-id="d5181-157">Entity Framework generuje proměnlivé a přiměnitelné částečné metody, které odpovídají jednotlivým vlastnostem třídy.</span><span class="sxs-lookup"><span data-stu-id="d5181-157">The Entity Framework generates OnChanging and OnChanged partial methods that correspond to each property of the class.</span></span>

<span data-ttu-id="d5181-158">V případě třídy video vytvoří Entity Framework následující metody:</span><span class="sxs-lookup"><span data-stu-id="d5181-158">In the case of the Movie class, the Entity Framework creates the following methods:</span></span>

- <span data-ttu-id="d5181-159">OnIdChanging</span><span class="sxs-lookup"><span data-stu-id="d5181-159">OnIdChanging</span></span>
- <span data-ttu-id="d5181-160">OnIdChanged</span><span class="sxs-lookup"><span data-stu-id="d5181-160">OnIdChanged</span></span>
- <span data-ttu-id="d5181-161">OnTitleChanging</span><span class="sxs-lookup"><span data-stu-id="d5181-161">OnTitleChanging</span></span>
- <span data-ttu-id="d5181-162">OnTitleChanged</span><span class="sxs-lookup"><span data-stu-id="d5181-162">OnTitleChanged</span></span>
- <span data-ttu-id="d5181-163">OnDirectorChanging</span><span class="sxs-lookup"><span data-stu-id="d5181-163">OnDirectorChanging</span></span>
- <span data-ttu-id="d5181-164">OnDirectorChanged</span><span class="sxs-lookup"><span data-stu-id="d5181-164">OnDirectorChanged</span></span>
- <span data-ttu-id="d5181-165">OnDateReleasedChanging</span><span class="sxs-lookup"><span data-stu-id="d5181-165">OnDateReleasedChanging</span></span>
- <span data-ttu-id="d5181-166">OnDateReleasedChanged</span><span class="sxs-lookup"><span data-stu-id="d5181-166">OnDateReleasedChanged</span></span>

<span data-ttu-id="d5181-167">Metoda při změně je volána přímo před změnou odpovídající vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="d5181-167">The OnChanging method is called right before the corresponding property is changed.</span></span> <span data-ttu-id="d5181-168">Metoda prochange je volána hned po změně vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="d5181-168">The OnChanged method is called right after the property is changed.</span></span>

<span data-ttu-id="d5181-169">Tyto částečné metody můžete využít k přidání logiky ověřování do třídy filmu.</span><span class="sxs-lookup"><span data-stu-id="d5181-169">You can take advantage of these partial methods to add validation logic to the Movie class.</span></span> <span data-ttu-id="d5181-170">Třída aktualizační filmy v seznamu 3 ověřuje, že vlastnosti title a Director jsou přiřazeny neprázdné hodnoty.</span><span class="sxs-lookup"><span data-stu-id="d5181-170">The update Movie class in Listing 3 verifies that the Title and Director properties are assigned nonempty values.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="d5181-171">Částečná metoda je metoda definovaná ve třídě, kterou není nutné implementovat.</span><span class="sxs-lookup"><span data-stu-id="d5181-171">A partial method is a method defined in a class that you are not required to implement.</span></span> <span data-ttu-id="d5181-172">Pokud neimplementujete částečnou metodu, kompilátor odstraní signaturu metody a veškerá volání metody, takže neexistují žádné náklady za běhu spojené s částečnou metodou.</span><span class="sxs-lookup"><span data-stu-id="d5181-172">If you don't implement a partial method then the compiler removes the method signature and all calls to the method so there are no run-time costs associated with the partial method.</span></span> <span data-ttu-id="d5181-173">V editoru Visual Studio Code můžete přidat částečnou metodu zadáním klíčového slova *Partial* následovaného mezerou pro zobrazení seznamu částečných implementací.</span><span class="sxs-lookup"><span data-stu-id="d5181-173">In the Visual Studio Code Editor, you can add a partial method by typing the keyword *partial* followed by a space to view a list of partials to implement.</span></span>

<span data-ttu-id="d5181-174">**Výpis 3 – Models\Movie.cs**</span><span class="sxs-lookup"><span data-stu-id="d5181-174">**Listing 3 - Models\Movie.cs**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample4.cs)]

<span data-ttu-id="d5181-175">Například pokud se pokusíte k vlastnosti title přiřadit prázdný řetězec, chybová zpráva je přiřazena ke slovníku s názvem \_chyby.</span><span class="sxs-lookup"><span data-stu-id="d5181-175">For example, if you attempt to assign an empty string to the Title property, then an error message is assigned to a Dictionary named \_errors.</span></span>

<span data-ttu-id="d5181-176">V tuto chvíli se nic nestane, když přiřadíte prázdný řetězec k vlastnosti title a do pole chyby Private \_se přidá chyba.</span><span class="sxs-lookup"><span data-stu-id="d5181-176">At this point, nothing actually happens when you assign an empty string to the Title property and an error is added to the private \_errors field.</span></span> <span data-ttu-id="d5181-177">Abychom vystavili tyto chyby ověřování v architektuře ASP.NET MVC, musíme implementovat rozhraní IDataErrorInfo.</span><span class="sxs-lookup"><span data-stu-id="d5181-177">We need to implement the IDataErrorInfo interface to expose these validation errors to the ASP.NET MVC framework.</span></span>

## <a name="implementing-the-idataerrorinfo-interface"></a><span data-ttu-id="d5181-178">Implementace rozhraní IDataErrorInfo</span><span class="sxs-lookup"><span data-stu-id="d5181-178">Implementing the IDataErrorInfo Interface</span></span>

<span data-ttu-id="d5181-179">Rozhraní IDataErrorInfo bylo součástí rozhraní .NET Framework od první verze.</span><span class="sxs-lookup"><span data-stu-id="d5181-179">The IDataErrorInfo interface has been part of the .NET framework since the first version.</span></span> <span data-ttu-id="d5181-180">Toto rozhraní je velmi jednoduché rozhraní:</span><span class="sxs-lookup"><span data-stu-id="d5181-180">This interface is a very simple interface:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample5.cs)]

<span data-ttu-id="d5181-181">Pokud třída implementuje rozhraní IDataErrorInfo, rozhraní ASP.NET MVC bude toto rozhraní používat při vytváření instance třídy.</span><span class="sxs-lookup"><span data-stu-id="d5181-181">If a class implements the IDataErrorInfo interface, the ASP.NET MVC framework will use this interface when creating an instance of the class.</span></span> <span data-ttu-id="d5181-182">Například akce domů kontroleru Create () přijímá instanci třídy video:</span><span class="sxs-lookup"><span data-stu-id="d5181-182">For example, the Home controller Create() action accepts an instance of the Movie class:</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample6.cs)]

<span data-ttu-id="d5181-183">Rozhraní ASP.NET MVC vytvoří instanci filmu předanou akci Create () pomocí pořadače modelu (DefaultModelBinder).</span><span class="sxs-lookup"><span data-stu-id="d5181-183">The ASP.NET MVC framework creates the instance of the Movie passed to the Create() action by using a model binder (the DefaultModelBinder).</span></span> <span data-ttu-id="d5181-184">Pořadač modelů zodpovídá za vytvoření instance objektu filmu navázáním polí formuláře HTML na instanci objektu video.</span><span class="sxs-lookup"><span data-stu-id="d5181-184">The model binder is responsible for creating an instance of the Movie object by binding the HTML form fields to an instance of the Movie object.</span></span>

<span data-ttu-id="d5181-185">DefaultModelBinder zjistí, zda třída implementuje rozhraní IDataErrorInfo.</span><span class="sxs-lookup"><span data-stu-id="d5181-185">The DefaultModelBinder detects whether or not a class implements the IDataErrorInfo interface.</span></span> <span data-ttu-id="d5181-186">Pokud třída implementuje toto rozhraní, pořadač modelu vyvolá IDataErrorInfo. Tento indexer pro každou vlastnost třídy.</span><span class="sxs-lookup"><span data-stu-id="d5181-186">If a class implements this interface then the model binder invokes the IDataErrorInfo.this indexer for each property of the class.</span></span> <span data-ttu-id="d5181-187">Pokud indexer vrátí chybovou zprávu, přidá pořadač modelů tuto chybovou zprávu do stavu modelu automaticky.</span><span class="sxs-lookup"><span data-stu-id="d5181-187">If the indexer returns an error message then the model binder adds this error message to model state automatically.</span></span>

<span data-ttu-id="d5181-188">DefaultModelBinder také kontroluje vlastnost IDataErrorInfo. Error.</span><span class="sxs-lookup"><span data-stu-id="d5181-188">The DefaultModelBinder also checks the IDataErrorInfo.Error property.</span></span> <span data-ttu-id="d5181-189">Tato vlastnost slouží k reprezentaci chyb ověřování specifických pro jiné než vlastnosti, které jsou přidruženy ke třídě.</span><span class="sxs-lookup"><span data-stu-id="d5181-189">This property is intended to represent non-property specific validation errors associated with the class.</span></span> <span data-ttu-id="d5181-190">Můžete například vynutili ověřovací pravidlo, které závisí na hodnotách více vlastností třídy video.</span><span class="sxs-lookup"><span data-stu-id="d5181-190">For example, you might want to enforce a validation rule that depends on the values of multiple properties of the Movie class.</span></span> <span data-ttu-id="d5181-191">V takovém případě byste vrátili chybu ověřování z vlastnosti Error.</span><span class="sxs-lookup"><span data-stu-id="d5181-191">In that case, you would return a validation error from the Error property.</span></span>

<span data-ttu-id="d5181-192">Aktualizovaná třída filmu v seznamu 4 implementuje rozhraní IDataErrorInfo.</span><span class="sxs-lookup"><span data-stu-id="d5181-192">The updated Movie class in Listing 4 implements the IDataErrorInfo interface.</span></span>

<span data-ttu-id="d5181-193">**Výpis 4 – Models\Movie.cs (implementuje IDataErrorInfo)**</span><span class="sxs-lookup"><span data-stu-id="d5181-193">**Listing 4 - Models\Movie.cs (implements IDataErrorInfo)**</span></span>

[!code-csharp[Main](validating-with-the-idataerrorinfo-interface-cs/samples/sample7.cs)]

<span data-ttu-id="d5181-194">V seznamu 4 vlastnost indexeru kontroluje kolekci chyb \_, aby bylo možné zjistit, zda obsahuje klíč, který odpovídá názvu vlastnosti předané indexeru.</span><span class="sxs-lookup"><span data-stu-id="d5181-194">In Listing 4, the indexer property checks the \_errors collection to see if it contains a key that corresponds to the property name passed to the indexer.</span></span> <span data-ttu-id="d5181-195">Není-li k této vlastnosti přidružena žádná chyba ověřování, je vrácen prázdný řetězec.</span><span class="sxs-lookup"><span data-stu-id="d5181-195">If there is no validation error associated with the property then an empty string is returned.</span></span>

<span data-ttu-id="d5181-196">Nemusíte upravovat domovský kontroler tak, aby bylo možné použít upravenou třídu filmu.</span><span class="sxs-lookup"><span data-stu-id="d5181-196">You don't need to modify the Home controller in any way to use the modified Movie class.</span></span> <span data-ttu-id="d5181-197">Stránka zobrazená na obrázku 3 ukazuje, co se stane, když pro pole názvu nebo formuláře režiséra není zadána žádná hodnota.</span><span class="sxs-lookup"><span data-stu-id="d5181-197">The page displayed in Figure 3 illustrates what happens when no value is entered for the Title or Director form fields.</span></span>

<span data-ttu-id="d5181-198">[Automatické vytváření metod akcí ![](validating-with-the-idataerrorinfo-interface-cs/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="d5181-198">[![Creating action methods automatically](validating-with-the-idataerrorinfo-interface-cs/_static/image3.jpg)](validating-with-the-idataerrorinfo-interface-cs/_static/image5.png)</span></span>

<span data-ttu-id="d5181-199">**Obrázek 03**: formulář s chybějícími hodnotami ([kliknutím zobrazíte obrázek v plné velikosti](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="d5181-199">**Figure 03**: A form with missing values ([Click to view full-size image](validating-with-the-idataerrorinfo-interface-cs/_static/image6.png))</span></span>

<span data-ttu-id="d5181-200">Všimněte si, že hodnota DateReleased je automaticky ověřena.</span><span class="sxs-lookup"><span data-stu-id="d5181-200">Notice that the DateReleased value is validated automatically.</span></span> <span data-ttu-id="d5181-201">Vzhledem k tomu, že vlastnost DateReleased nepřijímá hodnoty NULL, vygeneruje DefaultModelBinder chybu ověřování pro tuto vlastnost automaticky, pokud nemá hodnotu.</span><span class="sxs-lookup"><span data-stu-id="d5181-201">Because the DateReleased property does not accept NULL values, the DefaultModelBinder generates a validation error for this property automatically when it does not have a value.</span></span> <span data-ttu-id="d5181-202">Pokud chcete změnit chybovou zprávu pro vlastnost DateReleased, musíte vytvořit vlastní pořadač modelů.</span><span class="sxs-lookup"><span data-stu-id="d5181-202">If you want to modify the error message for the DateReleased property then you need to create a custom model binder.</span></span>

## <a name="summary"></a><span data-ttu-id="d5181-203">Souhrn</span><span class="sxs-lookup"><span data-stu-id="d5181-203">Summary</span></span>

<span data-ttu-id="d5181-204">V tomto kurzu jste zjistili, jak používat rozhraní IDataErrorInfo k vytváření chybových zpráv ověřování.</span><span class="sxs-lookup"><span data-stu-id="d5181-204">In this tutorial, you learned how to use the IDataErrorInfo interface to generate validation error messages.</span></span> <span data-ttu-id="d5181-205">Nejprve jsme vytvořili částečnou třídu filmu, která rozšiřuje funkčnost třídy částečného filmu vygenerované Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="d5181-205">First, we created a partial Movie class that extends the functionality of the partial Movie class generated by the Entity Framework.</span></span> <span data-ttu-id="d5181-206">Dále jsme přidali logiku ověřování pro částečné metody třídy film OnTitleChanging () a OnDirectorChanging ().</span><span class="sxs-lookup"><span data-stu-id="d5181-206">Next, we added validation logic to the Movie class OnTitleChanging() and OnDirectorChanging() partial methods.</span></span> <span data-ttu-id="d5181-207">Nakonec jsme implementovali rozhraní IDataErrorInfo, aby se tyto ověřovací zprávy daly vystavit do architektury ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="d5181-207">Finally, we implemented the IDataErrorInfo interface in order to expose these validation messages to the ASP.NET MVC framework.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d5181-208">[Předchozí](performing-simple-validation-cs.md)
> [Další](validating-with-a-service-layer-cs.md)</span><span class="sxs-lookup"><span data-stu-id="d5181-208">[Previous](performing-simple-validation-cs.md)
[Next](validating-with-a-service-layer-cs.md)</span></span>

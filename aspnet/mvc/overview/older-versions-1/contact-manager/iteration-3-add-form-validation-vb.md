---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
title: 'Iterace #3 – Přidání ověřovacího formuláře (VB) | Dokumentace Microsoftu'
author: microsoft
description: Ve třetí iterace přidáme ověření základní formulář. Můžeme zabránit neoprávněným osobám v odeslání formuláře bez dokončení vyžadovaná pole formuláře. Můžeme také ověřit emai...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 4805e75a-7911-46e3-b11b-229a6eed245e
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: b44aaab45f04f736e4171a43a8b24b71aaedca2f
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070534"
---
<a name="iteration-3--add-form-validation-vb"></a><span data-ttu-id="27c25-105">Iterace #3 – Přidání ověřovacího formuláře (VB)</span><span class="sxs-lookup"><span data-stu-id="27c25-105">Iteration #3 – Add form validation (VB)</span></span>
====================
<span data-ttu-id="27c25-106">by [Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="27c25-106">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="27c25-107">Stáhnout kód</span><span class="sxs-lookup"><span data-stu-id="27c25-107">Download Code</span></span>](iteration-3-add-form-validation-vb/_static/contactmanager_3_vb1.zip)

> <span data-ttu-id="27c25-108">Ve třetí iterace přidáme ověření základní formulář.</span><span class="sxs-lookup"><span data-stu-id="27c25-108">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="27c25-109">Můžeme zabránit neoprávněným osobám v odeslání formuláře bez dokončení vyžadovaná pole formuláře.</span><span class="sxs-lookup"><span data-stu-id="27c25-109">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="27c25-110">Také ověření e-mailových adres a telefonních čísel.</span><span class="sxs-lookup"><span data-stu-id="27c25-110">We also validate email addresses and phone numbers.</span></span>


## <a name="building-a-contact-management-aspnet-mvc-application-vb"></a><span data-ttu-id="27c25-111">Vytvoření aplikace pro správu kontaktů ASP.NET MVC (VB)</span><span class="sxs-lookup"><span data-stu-id="27c25-111">Building a Contact Management ASP.NET MVC Application (VB)</span></span>
  

<span data-ttu-id="27c25-112">V této sérii kurzů jsme integrovali celou aplikaci kontakt správy od začátku na dokončení.</span><span class="sxs-lookup"><span data-stu-id="27c25-112">In this series of tutorials, we build an entire Contact Management application from start to finish.</span></span> <span data-ttu-id="27c25-113">Obraťte se na správce aplikace umožňuje ukládat kontaktní údaje - jména, telefonní čísla a e-mailové adresy – seznam lidí.</span><span class="sxs-lookup"><span data-stu-id="27c25-113">The Contact Manager application enables you to store contact information - names, phone numbers and email addresses - for a list of people.</span></span>

<span data-ttu-id="27c25-114">Vytváříme aplikaci přes více iterací.</span><span class="sxs-lookup"><span data-stu-id="27c25-114">We build the application over multiple iterations.</span></span> <span data-ttu-id="27c25-115">S každou iterací zvyšujeme postupně aplikace.</span><span class="sxs-lookup"><span data-stu-id="27c25-115">With each iteration, we gradually improve the application.</span></span> <span data-ttu-id="27c25-116">Cílem tohoto přístupu s více iterace je vám pomohl pochopit důvod pro každou změnu.</span><span class="sxs-lookup"><span data-stu-id="27c25-116">The goal of this multiple iteration approach is to enable you to understand the reason for each change.</span></span>

- <span data-ttu-id="27c25-117">Iterace #1 – Vytvoření aplikace.</span><span class="sxs-lookup"><span data-stu-id="27c25-117">Iteration #1 - Create the application.</span></span> <span data-ttu-id="27c25-118">V první iteraci vytvoříme Správce kontaktů v Nejjednodušším způsobem, jak je to možné.</span><span class="sxs-lookup"><span data-stu-id="27c25-118">In the first iteration, we create the Contact Manager in the simplest way possible.</span></span> <span data-ttu-id="27c25-119">Přidáváme podporu pro základní databázových operací: Vytvoření, čtení, aktualizace a odstranění (CRUD).</span><span class="sxs-lookup"><span data-stu-id="27c25-119">We add support for basic database operations: Create, Read, Update, and Delete (CRUD).</span></span>

- <span data-ttu-id="27c25-120">Ujistěte se, iterace #2 – vylepšení vzhledu aplikace.</span><span class="sxs-lookup"><span data-stu-id="27c25-120">Iteration #2 - Make the application look nice.</span></span> <span data-ttu-id="27c25-121">V této iterace můžeme zlepšit vzhled aplikace tak, že změna výchozích hlavní stránka zobrazení ASP.NET MVC a stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="27c25-121">In this iteration, we improve the appearance of the application by modifying the default ASP.NET MVC view master page and cascading style sheet.</span></span>

- <span data-ttu-id="27c25-122">Iterace #3 – Přidání ověřovacího formuláře.</span><span class="sxs-lookup"><span data-stu-id="27c25-122">Iteration #3 - Add form validation.</span></span> <span data-ttu-id="27c25-123">Ve třetí iterace přidáme ověření základní formulář.</span><span class="sxs-lookup"><span data-stu-id="27c25-123">In the third iteration, we add basic form validation.</span></span> <span data-ttu-id="27c25-124">Můžeme zabránit neoprávněným osobám v odeslání formuláře bez dokončení vyžadovaná pole formuláře.</span><span class="sxs-lookup"><span data-stu-id="27c25-124">We prevent people from submitting a form without completing required form fields.</span></span> <span data-ttu-id="27c25-125">Také ověření e-mailových adres a telefonních čísel.</span><span class="sxs-lookup"><span data-stu-id="27c25-125">We also validate email addresses and phone numbers.</span></span>

- <span data-ttu-id="27c25-126">Iterace #4 – vytvoření volně spárované aplikace.</span><span class="sxs-lookup"><span data-stu-id="27c25-126">Iteration #4 - Make the application loosely coupled.</span></span> <span data-ttu-id="27c25-127">V této iterace čtvrtý můžeme využít několik způsobů návrhu v softwaru k bylo snazší spravovat a upravovat aplikace Správce kontaktů.</span><span class="sxs-lookup"><span data-stu-id="27c25-127">In this fourth iteration, we take advantage of several software design patterns to make it easier to maintain and modify the Contact Manager application.</span></span> <span data-ttu-id="27c25-128">Například Refaktorovat jsme naši aplikaci pomocí vzoru úložiště a vzor vkládání závislostí.</span><span class="sxs-lookup"><span data-stu-id="27c25-128">For example, we refactor our application to use the Repository pattern and the Dependency Injection pattern.</span></span>

- <span data-ttu-id="27c25-129">Iterace #5 – vytvoření testů jednotek.</span><span class="sxs-lookup"><span data-stu-id="27c25-129">Iteration #5 - Create unit tests.</span></span> <span data-ttu-id="27c25-130">V páté iteraci jsme snadněji naší aplikace spravovat a upravovat tak, že přidáte testy jednotek.</span><span class="sxs-lookup"><span data-stu-id="27c25-130">In the fifth iteration, we make our application easier to maintain and modify by adding unit tests.</span></span> <span data-ttu-id="27c25-131">Jsme napodobení našich tříd datových modelů a vytváření testů jednotek pro naše řadiče a logiku ověřování.</span><span class="sxs-lookup"><span data-stu-id="27c25-131">We mock our data model classes and build unit tests for our controllers and validation logic.</span></span>

- <span data-ttu-id="27c25-132">Iterace #6 – použití vývoje řízeného testováním.</span><span class="sxs-lookup"><span data-stu-id="27c25-132">Iteration #6 - Use test-driven development.</span></span> <span data-ttu-id="27c25-133">V této iterace šestého přidáme nové funkce do naší aplikace tak, že nejprve zápis testů jednotek a psaní kódu pro testování částí.</span><span class="sxs-lookup"><span data-stu-id="27c25-133">In this sixth iteration, we add new functionality to our application by writing unit tests first and writing code against the unit tests.</span></span> <span data-ttu-id="27c25-134">V této iterace můžeme přidat skupiny kontaktů.</span><span class="sxs-lookup"><span data-stu-id="27c25-134">In this iteration, we add contact groups.</span></span>

- <span data-ttu-id="27c25-135">Iterace #7 – přidání funkcí Ajax.</span><span class="sxs-lookup"><span data-stu-id="27c25-135">Iteration #7 - Add Ajax functionality.</span></span> <span data-ttu-id="27c25-136">V sedmé iteraci můžeme zlepšit rychlost reakce a výkon naší aplikace tak, že přidáte podporu pro Ajax.</span><span class="sxs-lookup"><span data-stu-id="27c25-136">In the seventh iteration, we improve the responsiveness and performance of our application by adding support for Ajax.</span></span>


## <a name="this-iteration"></a><span data-ttu-id="27c25-137">Tuto iteraci</span><span class="sxs-lookup"><span data-stu-id="27c25-137">This Iteration</span></span>

<span data-ttu-id="27c25-138">V této druhé iterace kontaktujte správce aplikace přidáme ověření základní formulář.</span><span class="sxs-lookup"><span data-stu-id="27c25-138">In this second iteration of the Contact Manager application, we add basic form validation.</span></span> <span data-ttu-id="27c25-139">Můžeme zabránit neoprávněným osobám v odesílání kontaktu bez zadání hodnoty povinných polí formuláře.</span><span class="sxs-lookup"><span data-stu-id="27c25-139">We prevent people from submitting a contact without entering values for required form fields.</span></span> <span data-ttu-id="27c25-140">Také ověření telefonní čísla a e-mailové adresy (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="27c25-140">We also validate phone numbers and email addresses (see Figure 1).</span></span>


<span data-ttu-id="27c25-141">[![Dialogové okno Nový projekt](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="27c25-141">[![The New Project dialog box](iteration-3-add-form-validation-vb/_static/image1.jpg)](iteration-3-add-form-validation-vb/_static/image1.png)</span></span>

<span data-ttu-id="27c25-142">**Obrázek 01**: Formulář s ověřováním ([kliknutím ji zobrazíte obrázek v plné velikosti](iteration-3-add-form-validation-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="27c25-142">**Figure 01**: A form with validation ([Click to view full-size image](iteration-3-add-form-validation-vb/_static/image2.png))</span></span>


<span data-ttu-id="27c25-143">V této iterace přidáme ověřovací logiku přímo na akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="27c25-143">In this iteration, we add the validation logic directly to the controller actions.</span></span> <span data-ttu-id="27c25-144">Obecně toto není doporučený postup pro přidání ověřování do aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="27c25-144">In general, this is not the recommended way to add validation to an ASP.NET MVC application.</span></span> <span data-ttu-id="27c25-145">Lepším řešením je umístit logiku ověřování s aplikací v samostatném [vrstva služby](http://martinfowler.com/eaaCatalog/serviceLayer.html).</span><span class="sxs-lookup"><span data-stu-id="27c25-145">A better approach is to place an application s validation logic in a separate [service layer](http://martinfowler.com/eaaCatalog/serviceLayer.html).</span></span> <span data-ttu-id="27c25-146">V další iteraci jsme Refaktorovat kontaktujte správce aplikace provádět jednodušší údržbu aplikace.</span><span class="sxs-lookup"><span data-stu-id="27c25-146">In the next iteration, we refactor the Contact Manager application to make the application more maintainable.</span></span>

<span data-ttu-id="27c25-147">V této iterace abychom si to nekomplikovali, jsme psát veškerý kód pro ověření ručně.</span><span class="sxs-lookup"><span data-stu-id="27c25-147">In this iteration, to keep things simple, we write all of the validation code by hand.</span></span> <span data-ttu-id="27c25-148">Místo psaní kódu ověření sami, může využíváme rozhraní ověřování.</span><span class="sxs-lookup"><span data-stu-id="27c25-148">Instead of writing the validation code ourselves, we could take advantage of a validation framework.</span></span> <span data-ttu-id="27c25-149">Například můžete použít Microsoft Enterprise Library ověření aplikace blok (VAB) pro implementace logiky ověření pro vaši aplikaci ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="27c25-149">For example, you can use the Microsoft Enterprise Library Validation Application Block (VAB) to implement the validation logic for your ASP.NET MVC application.</span></span> <span data-ttu-id="27c25-150">Další informace o ověření Application Block, naleznete v tématu:</span><span class="sxs-lookup"><span data-stu-id="27c25-150">To learn more about the Validation Application Block, see:</span></span>

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a><span data-ttu-id="27c25-151">Přidání ověření do zobrazení pro vytváření</span><span class="sxs-lookup"><span data-stu-id="27c25-151">Adding Validation to the Create View</span></span>

<span data-ttu-id="27c25-152">Umožní s Začněte přidáním logiku ověřování k zobrazení pro vytváření.</span><span class="sxs-lookup"><span data-stu-id="27c25-152">Let s start by adding validation logic to the Create view.</span></span> <span data-ttu-id="27c25-153">Naštěstí protože jsme vygenerován pomocí sady Visual Studio zobrazení pro vytváření, zobrazení pro vytváření již obsahuje veškerou logiku potřebné uživatelské rozhraní pro zobrazení ověřovacích zpráv.</span><span class="sxs-lookup"><span data-stu-id="27c25-153">Fortunately, because we generated the Create view with Visual Studio, the Create view already contains all of the necessary user interface logic to display validation messages.</span></span> <span data-ttu-id="27c25-154">Zobrazení pro vytváření je součástí výpis 1.</span><span class="sxs-lookup"><span data-stu-id="27c25-154">The Create view is contained in Listing 1.</span></span>

<span data-ttu-id="27c25-155">**Listing 1 - \Views\Contact\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="27c25-155">**Listing 1 - \Views\Contact\Create.aspx**</span></span>

[!code-aspx[Main](iteration-3-add-form-validation-vb/samples/sample1.aspx)]

<span data-ttu-id="27c25-156">Chyba ověření pole Třída se používá k úpravě stylu výstupu vykreslen metodou Html.ValidationMessage() helper.</span><span class="sxs-lookup"><span data-stu-id="27c25-156">The field-validation-error class is used to style the output rendered by the Html.ValidationMessage() helper.</span></span> <span data-ttu-id="27c25-157">Chyba ověření vstupu třída se používá k formátování textového pole (vstup) vykreslen metodou Html.TextBox() helper.</span><span class="sxs-lookup"><span data-stu-id="27c25-157">The input-validation-error class is used to style the textbox (input) rendered by the Html.TextBox() helper.</span></span> <span data-ttu-id="27c25-158">Chyby ověření souhrn třída se používá k úpravě stylu neuspořádaný seznam vykreslen metodou Html.ValidationSummary() helper.</span><span class="sxs-lookup"><span data-stu-id="27c25-158">The validation-summary-errors class is used to style the unordered list rendered by the Html.ValidationSummary() helper.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="27c25-159">Můžete upravit třídy List stylu popsané v této části pro přizpůsobení vzhledu chybových zpráv ověření.</span><span class="sxs-lookup"><span data-stu-id="27c25-159">You can modify the style sheet classes described in this section to customize the appearance of validation error messages.</span></span>


## <a name="adding-validation-logic-to-the-create-action"></a><span data-ttu-id="27c25-160">Přidat logiku ověřování k vytvoření akce</span><span class="sxs-lookup"><span data-stu-id="27c25-160">Adding Validation Logic to the Create Action</span></span>

<span data-ttu-id="27c25-161">V tuto chvíli, zobrazení pro vytváření nikdy nezobrazí chybových zpráv ověření, protože jsme nenapsali logiku pro generování všechny zprávy.</span><span class="sxs-lookup"><span data-stu-id="27c25-161">Right now, the Create view never displays validation error messages because we have not written the logic to generate any messages.</span></span> <span data-ttu-id="27c25-162">Aby bylo možné zobrazit chybových zpráv ověření, budete muset přidat chybové zprávy ModelState.</span><span class="sxs-lookup"><span data-stu-id="27c25-162">In order to display validation error messages, you need to add the error messages to ModelState.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="27c25-163">Metoda UpdateModel() přidá chybové zprávy do ModelState automaticky při dojde k chybám přiřazení hodnoty pole formuláře na vlastnost.</span><span class="sxs-lookup"><span data-stu-id="27c25-163">The UpdateModel() method adds error messages to ModelState automatically when there is an error assigning the value of a form field to a property.</span></span> <span data-ttu-id="27c25-164">Například pokud se pokusíte přiřadit řetězec "apple" datum narození vlastnost, která přijímá hodnoty data a času, pak metoda UpdateModel() přidá chybu do ModelState.</span><span class="sxs-lookup"><span data-stu-id="27c25-164">For example, if you attempt to assign the string "apple" to a BirthDate property that accepts DateTime values, then the UpdateModel() method adds an error to ModelState.</span></span>


<span data-ttu-id="27c25-165">Upravená Metoda Create() výpis 2 obsahuje nový oddíl, který ověřuje vlastnosti třídy kontakt před nový kontakt se vloží do databáze.</span><span class="sxs-lookup"><span data-stu-id="27c25-165">The modified Create() method in Listing 2 contains a new section that validates the properties of the Contact class before the new contact is inserted into the database.</span></span>

<span data-ttu-id="27c25-166">**Výpis 2 - Controllers\ContactController.vb (vytvoření s ověřováním)**</span><span class="sxs-lookup"><span data-stu-id="27c25-166">**Listing 2 - Controllers\ContactController.vb (Create with validation)**</span></span>

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample2.vb)]

<span data-ttu-id="27c25-167">V části ověření vynucuje čtyř různých ověřovacích pravidel:</span><span class="sxs-lookup"><span data-stu-id="27c25-167">The validate section enforces four distinct validation rules:</span></span>

- <span data-ttu-id="27c25-168">Vlastnost FirstName musí mít délku větší než nula (a nemůže skládat pouze z mezer)</span><span class="sxs-lookup"><span data-stu-id="27c25-168">The FirstName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="27c25-169">Větší než nula. délka musí být vlastnost LastName (a nemůže skládat pouze z mezer)</span><span class="sxs-lookup"><span data-stu-id="27c25-169">The LastName property must have a length greater than zero (and it cannot consist solely of spaces)</span></span>
- <span data-ttu-id="27c25-170">Pokud má hodnotu vlastnosti telefonu (má délku větší než 0) a vlastnost telefon musí odpovídat regulárnímu výrazu.</span><span class="sxs-lookup"><span data-stu-id="27c25-170">If the Phone property has a value (has a length greater than 0) then the Phone property must match a regular expression.</span></span>
- <span data-ttu-id="27c25-171">Pokud vlastnost e-mailu obsahuje hodnotu (má délku větší než 0) a vlastnost e-mailu musí odpovídat regulárnímu výrazu.</span><span class="sxs-lookup"><span data-stu-id="27c25-171">If the Email property has a value (has a length greater than 0) then the Email property must match a regular expression.</span></span>

<span data-ttu-id="27c25-172">Po porušení pravidla ověřování je přidána chybová zpráva na ModelState pomocí metody AddModelError().</span><span class="sxs-lookup"><span data-stu-id="27c25-172">When there is a validation rule violation, an error message is added to ModelState with the help of the AddModelError() method.</span></span> <span data-ttu-id="27c25-173">Při přidání zprávy do ModelState zadáte název vlastnosti a text chybovou zprávu ověření.</span><span class="sxs-lookup"><span data-stu-id="27c25-173">When you add a message to ModelState, you provide the name of a property and the text of a validation error message.</span></span> <span data-ttu-id="27c25-174">Tato chybová zpráva se zobrazí v zobrazení Html.ValidationSummary() a Html.ValidationMessage() pomocné metody.</span><span class="sxs-lookup"><span data-stu-id="27c25-174">This error message is displayed in the view by the Html.ValidationSummary() and Html.ValidationMessage() helper methods.</span></span>

<span data-ttu-id="27c25-175">Po provedení ověřovacích pravidel, je vlastnost IsValid ModelState zaškrtnuto.</span><span class="sxs-lookup"><span data-stu-id="27c25-175">After the validation rules are executed, the IsValid property of ModelState is checked.</span></span> <span data-ttu-id="27c25-176">Vlastnost IsValid vrátí hodnotu false, pokud byly přidány do ModelState všech chybových zpráv ověření.</span><span class="sxs-lookup"><span data-stu-id="27c25-176">The IsValid property returns false when any validation error messages have been added to ModelState.</span></span> <span data-ttu-id="27c25-177">Pokud se ověření nezdaří, se zobrazí formulář vytvořit znovu s chybovými zprávami.</span><span class="sxs-lookup"><span data-stu-id="27c25-177">If validation fails, the Create form is redisplayed with the error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="27c25-178">Zobrazilo se mi regulárních výrazů pro ověření telefonní číslo a e-mailová adresa z úložiště regulárních výrazů v [*http://regexlib.com*](http://regexlib.com)</span><span class="sxs-lookup"><span data-stu-id="27c25-178">I got the regular expressions for validating the phone number and email address from the regular expression repository at [*http://regexlib.com*](http://regexlib.com)</span></span>


## <a name="adding-validation-logic-to-the-edit-action"></a><span data-ttu-id="27c25-179">Přidat logiku ověřování k akci Upravit</span><span class="sxs-lookup"><span data-stu-id="27c25-179">Adding Validation Logic to the Edit Action</span></span>

<span data-ttu-id="27c25-180">Akce Edit() aktualizuje kontakt.</span><span class="sxs-lookup"><span data-stu-id="27c25-180">The Edit() action updates a Contact.</span></span> <span data-ttu-id="27c25-181">Akce Edit() musí provádět stejné ověřování jako Create() akce.</span><span class="sxs-lookup"><span data-stu-id="27c25-181">The Edit() action needs to perform exactly the same validation as the Create() action.</span></span> <span data-ttu-id="27c25-182">Namísto duplikování stejný kód pro ověření, jsme měli Refaktorovat kontaktujte řadič tak, aby akce Create() i Edit() volání stejné metody ověřování.</span><span class="sxs-lookup"><span data-stu-id="27c25-182">Instead of duplicating the same validation code, we should refactor the Contact controller so that both the Create() and Edit() actions call the same validation method.</span></span>

<span data-ttu-id="27c25-183">Upravené třídy kontroleru kontakt je obsažen v informacích 3.</span><span class="sxs-lookup"><span data-stu-id="27c25-183">The modified Contact controller class is contained in Listing 3.</span></span> <span data-ttu-id="27c25-184">Tato třída obsahuje novou ValidateContact() metodu, která je volána v rámci Create() i Edit() akcí.</span><span class="sxs-lookup"><span data-stu-id="27c25-184">This class has a new ValidateContact() method that is called within both the Create() and Edit() actions.</span></span>

<span data-ttu-id="27c25-185">**Výpis 3 - Controllers\ContactController.vb**</span><span class="sxs-lookup"><span data-stu-id="27c25-185">**Listing 3 - Controllers\ContactController.vb**</span></span>

[!code-vb[Main](iteration-3-add-form-validation-vb/samples/sample3.vb)]

## <a name="summary"></a><span data-ttu-id="27c25-186">Souhrn</span><span class="sxs-lookup"><span data-stu-id="27c25-186">Summary</span></span>

<span data-ttu-id="27c25-187">V této iterace jsme přidali základní formulář ověření naší aplikace Správce kontaktů.</span><span class="sxs-lookup"><span data-stu-id="27c25-187">In this iteration, we added basic form validation to our Contact Manager application.</span></span> <span data-ttu-id="27c25-188">Naše logiku ověřování zabraňuje uživatelům odeslání nového kontaktu nebo úpravy stávajících kontaktu bez zadání hodnoty pro vlastnosti FirstName a LastName.</span><span class="sxs-lookup"><span data-stu-id="27c25-188">Our validation logic prevents users from submitting a new contact or editing an existing contact without supplying values for the FirstName and LastName properties.</span></span> <span data-ttu-id="27c25-189">Dále uživatelé musí zadat platné telefonní čísla a e-mailové adresy.</span><span class="sxs-lookup"><span data-stu-id="27c25-189">Furthermore, users must supply valid phone numbers and email addresses.</span></span>

<span data-ttu-id="27c25-190">V této iterace jsme přidali logiku ověřování k naší aplikace Správce kontaktů v nejjednodušší způsob, jak je to možné.</span><span class="sxs-lookup"><span data-stu-id="27c25-190">In this iteration, we added the validation logic to our Contact Manager application in the easiest way possible.</span></span> <span data-ttu-id="27c25-191">Ale kombinování naše logiku ověřování do našich logice kontroleru vytvoří problémy nám v dlouhodobém horizontu.</span><span class="sxs-lookup"><span data-stu-id="27c25-191">However, mixing our validation logic into our controller logic will create problems for us in the long term.</span></span> <span data-ttu-id="27c25-192">Naše aplikace bude obtížnější spravovat a upravovat v čase.</span><span class="sxs-lookup"><span data-stu-id="27c25-192">Our application will be more difficult to maintain and modify over time.</span></span>

<span data-ttu-id="27c25-193">V další iteraci jsme se naše řadiče pro Refaktorovat náš logiku ověřování a logiky přístupu k databázi.</span><span class="sxs-lookup"><span data-stu-id="27c25-193">In the next iteration, we will refactor our validation logic and database access logic out of our controllers.</span></span> <span data-ttu-id="27c25-194">Provedeme výhod několika Principy návrhu softwaru umožňují vytvořit více volně a snadněji spravovatelné aplikace.</span><span class="sxs-lookup"><span data-stu-id="27c25-194">We'll take advantage of several software design principles to enable us to create a more loosely coupled, and more maintainable, application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="27c25-195">[Předchozí](iteration-2-make-the-application-look-nice-vb.md)
> [další](iteration-4-make-the-application-loosely-coupled-vb.md)</span><span class="sxs-lookup"><span data-stu-id="27c25-195">[Previous](iteration-2-make-the-application-look-nice-vb.md)
[Next](iteration-4-make-the-application-loosely-coupled-vb.md)</span></span>
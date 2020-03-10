---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
title: 'Část 9: registrace a rezervace | Microsoft Docs'
author: jongalloway
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 9 pokrývá registraci a rezervaci.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: d65c5c2b-a039-463f-ad29-25cf9fb7a1ba
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
msc.type: authoredcontent
ms.openlocfilehash: 040bc0ccef889fb9a7c3d9b5ce88c75b7b754248
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559533"
---
# <a name="part-9-registration-and-checkout"></a><span data-ttu-id="8018c-104">9\. část: Registrace a pokladna</span><span class="sxs-lookup"><span data-stu-id="8018c-104">Part 9: Registration and Checkout</span></span>

<span data-ttu-id="8018c-105">o [Jan Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="8018c-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="8018c-106">Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio pro vývoj webů.</span><span class="sxs-lookup"><span data-stu-id="8018c-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="8018c-107">Úložiště hudby MVC je zjednodušená ukázka implementace úložiště, která prodává hudební alba online a implementuje základní funkce pro správu webů, přihlašování uživatelů a nákupních košíků.</span><span class="sxs-lookup"><span data-stu-id="8018c-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="8018c-108">V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště.</span><span class="sxs-lookup"><span data-stu-id="8018c-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="8018c-109">Část 9 pokrývá registraci a rezervaci.</span><span class="sxs-lookup"><span data-stu-id="8018c-109">Part 9 covers Registration and Checkout.</span></span>

<span data-ttu-id="8018c-110">V této části vytvoříme CheckoutController, ve kterém se budou shromažďovat informace o adrese a platbách nakupujících.</span><span class="sxs-lookup"><span data-stu-id="8018c-110">In this section, we will be creating a CheckoutController which will collect the shopper's address and payment information.</span></span> <span data-ttu-id="8018c-111">Před rezervací budeme vyžadovat, aby se uživatelé zaregistrovali na našem webu, takže tento kontroler bude vyžadovat autorizaci.</span><span class="sxs-lookup"><span data-stu-id="8018c-111">We will require users to register with our site prior to checking out, so this controller will require authorization.</span></span>

<span data-ttu-id="8018c-112">Uživatelé přejdou k procesu rezervace z jeho nákupního košíku kliknutím na tlačítko "rezervovat".</span><span class="sxs-lookup"><span data-stu-id="8018c-112">Users will navigate to the checkout process from their shopping cart by clicking the "Checkout" button.</span></span>

![](mvc-music-store-part-9/_static/image1.jpg)

<span data-ttu-id="8018c-113">Pokud uživatel není přihlášený, zobrazí se jim výzva k zadání.</span><span class="sxs-lookup"><span data-stu-id="8018c-113">If the user is not logged in, they will be prompted to.</span></span>

![](mvc-music-store-part-9/_static/image1.png)

<span data-ttu-id="8018c-114">Po úspěšném přihlášení se zobrazí uživatel zobrazení adresa a platby.</span><span class="sxs-lookup"><span data-stu-id="8018c-114">Upon successful login, the user is then shown the Address and Payment view.</span></span>

![](mvc-music-store-part-9/_static/image2.png)

<span data-ttu-id="8018c-115">Po vyplnění formuláře a odeslání objednávky se zobrazí obrazovka potvrzení objednávky.</span><span class="sxs-lookup"><span data-stu-id="8018c-115">Once they have filled the form and submitted the order, they will be shown the order confirmation screen.</span></span>

![](mvc-music-store-part-9/_static/image3.png)

<span data-ttu-id="8018c-116">Při pokusu o zobrazení neexistující objednávky nebo objednávky, která nepatří do, se zobrazí zobrazení chyb.</span><span class="sxs-lookup"><span data-stu-id="8018c-116">Attempting to view either a non-existent order or an order that doesn't belong to you will show the Error view.</span></span>

![](mvc-music-store-part-9/_static/image4.png)

## <a name="migrating-the-shopping-cart"></a><span data-ttu-id="8018c-117">Migruje se nákupní košík.</span><span class="sxs-lookup"><span data-stu-id="8018c-117">Migrating the Shopping Cart</span></span>

<span data-ttu-id="8018c-118">I když je nákupní proces anonymní, když uživatel klikne na tlačítko rezervovat, bude se muset zaregistrovat a přihlásit.</span><span class="sxs-lookup"><span data-stu-id="8018c-118">While the shopping process is anonymous, when the user clicks on the Checkout button, they will be required to register and login.</span></span> <span data-ttu-id="8018c-119">Uživatelé budou očekávat, že si zachováme informace o nákupních košíkech mezi návštěvami, takže při dokončení registrace nebo přihlášení bude potřeba přidružit informace nákupního košíku k uživateli.</span><span class="sxs-lookup"><span data-stu-id="8018c-119">Users will expect that we will maintain their shopping cart information between visits, so we will need to associate the shopping cart information with a user when they complete registration or login.</span></span>

<span data-ttu-id="8018c-120">To je vlastně velmi jednoduché, protože naše třída ShoppingCart již má metodu, která bude přidružit všechny položky v aktuálním vozíku k uživatelskému jménu.</span><span class="sxs-lookup"><span data-stu-id="8018c-120">This is actually very simple to do, as our ShoppingCart class already has a method which will associate all the items in the current cart with a username.</span></span> <span data-ttu-id="8018c-121">Tuto metodu budeme muset volat, až uživatel dokončí registraci nebo přihlášení.</span><span class="sxs-lookup"><span data-stu-id="8018c-121">We will just need to call this method when a user completes registration or login.</span></span>

<span data-ttu-id="8018c-122">Otevřete třídu **AccountController** , kterou jsme přidali, když jsme nastavili členství a autorizaci.</span><span class="sxs-lookup"><span data-stu-id="8018c-122">Open the **AccountController** class that we added when we were setting up Membership and Authorization.</span></span> <span data-ttu-id="8018c-123">Přidejte příkaz using odkazující na MvcMusicStore. Models a pak přidejte následující metodu MigrateShoppingCart:</span><span class="sxs-lookup"><span data-stu-id="8018c-123">Add a using statement referencing MvcMusicStore.Models, then add the following MigrateShoppingCart method:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample1.cs)]

<span data-ttu-id="8018c-124">V dalším kroku změňte akci po ověření přihlašovacího příspěvku tak, aby se MigrateShoppingCart volala po ověření uživatele, jak je znázorněno níže:</span><span class="sxs-lookup"><span data-stu-id="8018c-124">Next, modify the LogOn post action to call MigrateShoppingCart after the user has been validated, as shown below:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample2.cs)]

<span data-ttu-id="8018c-125">Proveďte stejnou změnu akce registrovat po, ihned po úspěšném vytvoření uživatelského účtu:</span><span class="sxs-lookup"><span data-stu-id="8018c-125">Make the same change to the Register post action, immediately after the user account is successfully created:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample3.cs)]

<span data-ttu-id="8018c-126">To je teď – anonymní nákupní košík se po úspěšné registraci nebo přihlášení automaticky přenese na uživatelský účet.</span><span class="sxs-lookup"><span data-stu-id="8018c-126">That's it - now an anonymous shopping cart will be automatically transferred to a user account upon successful registration or login.</span></span>

## <a name="creating-the-checkoutcontroller"></a><span data-ttu-id="8018c-127">Vytváření CheckoutController</span><span class="sxs-lookup"><span data-stu-id="8018c-127">Creating the CheckoutController</span></span>

<span data-ttu-id="8018c-128">Klikněte pravým tlačítkem na složku Controllers a přidejte do projektu s názvem CheckoutController nový kontroler pomocí prázdné šablony kontroleru.</span><span class="sxs-lookup"><span data-stu-id="8018c-128">Right-click on the Controllers folder and add a new Controller to the project named CheckoutController using the Empty controller template.</span></span>

![](mvc-music-store-part-9/_static/image5.png)

<span data-ttu-id="8018c-129">Nejdřív přidejte atribut autorizovat nad deklaraci třídy kontroleru, aby se před rezervací vyžadovaly, aby se uživatelé zaregistrovali:</span><span class="sxs-lookup"><span data-stu-id="8018c-129">First, add the Authorize attribute above the Controller class declaration to require users to register before checkout:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample4.cs)]

<span data-ttu-id="8018c-130">*Poznámka: Tato změna se podobá StoreManagerController, ale v takovém případě atribut autorizovat vyžaduje, aby uživatel byl v roli správce. V kontroleru rezervací vyžadujeme, aby byl uživatel přihlášený, ale nevyžadoval, aby byli správci.*</span><span class="sxs-lookup"><span data-stu-id="8018c-130">*Note: This is similar to the change we previously made to the StoreManagerController, but in that case the Authorize attribute required that the user be in an Administrator role. In the Checkout Controller, we're requiring the user be logged in but aren't requiring that they be administrators.*</span></span>

<span data-ttu-id="8018c-131">V zájmu jednoduchosti se v tomto kurzu nebudeme zabývat informacemi o platbách.</span><span class="sxs-lookup"><span data-stu-id="8018c-131">For the sake of simplicity, we won't be dealing with payment information in this tutorial.</span></span> <span data-ttu-id="8018c-132">Místo toho umožňujíme uživatelům rezervovat kód propagačního kódu.</span><span class="sxs-lookup"><span data-stu-id="8018c-132">Instead, we are allowing users to check out using a promotional code.</span></span> <span data-ttu-id="8018c-133">Tento kód propagačního kódu budeme uchovávat pomocí konstanty s názvem PromoCode.</span><span class="sxs-lookup"><span data-stu-id="8018c-133">We will store this promotional code using a constant named PromoCode.</span></span>

<span data-ttu-id="8018c-134">Jak je uvedeno v StoreController, deklarujeme pole pro uložení instance třídy MusicStoreEntities s názvem storeDB.</span><span class="sxs-lookup"><span data-stu-id="8018c-134">As in the StoreController, we'll declare a field to hold an instance of the MusicStoreEntities class, named storeDB.</span></span> <span data-ttu-id="8018c-135">Aby bylo možné používat třídu MusicStoreEntities, je nutné přidat příkaz using pro obor názvů MvcMusicStore. Models.</span><span class="sxs-lookup"><span data-stu-id="8018c-135">In order to make use of the MusicStoreEntities class, we will need to add a using statement for the MvcMusicStore.Models namespace.</span></span> <span data-ttu-id="8018c-136">V horní části našeho kontroleru registrace se zobrazí níže.</span><span class="sxs-lookup"><span data-stu-id="8018c-136">The top of our Checkout controller appears below.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample5.cs)]

<span data-ttu-id="8018c-137">CheckoutController bude mít následující akce kontroleru:</span><span class="sxs-lookup"><span data-stu-id="8018c-137">The CheckoutController will have the following controller actions:</span></span>

<span data-ttu-id="8018c-138">**AddressAndPayment (Get Method)** zobrazí formulář, který uživateli umožní zadat jejich informace.</span><span class="sxs-lookup"><span data-stu-id="8018c-138">**AddressAndPayment (GET method)** will display a form to allow the user to enter their information.</span></span>

<span data-ttu-id="8018c-139">**AddressAndPayment (post metoda)** ověří zadání a zpracuje objednávku.</span><span class="sxs-lookup"><span data-stu-id="8018c-139">**AddressAndPayment (POST method)** will validate the input and process the order.</span></span>

<span data-ttu-id="8018c-140">Po úspěšném dokončení procesu registrace se zobrazí **dokončeno** .</span><span class="sxs-lookup"><span data-stu-id="8018c-140">**Complete** will be shown after a user has successfully finished the checkout process.</span></span> <span data-ttu-id="8018c-141">Toto zobrazení bude obsahovat číslo objednávky uživatele jako potvrzení.</span><span class="sxs-lookup"><span data-stu-id="8018c-141">This view will include the user's order number, as confirmation.</span></span>

<span data-ttu-id="8018c-142">Nejprve přejmenujte akci řadiče indexu (která byla generována při vytvoření kontroleru) do AddressAndPayment.</span><span class="sxs-lookup"><span data-stu-id="8018c-142">First, let's rename the Index controller action (which was generated when we created the controller) to AddressAndPayment.</span></span> <span data-ttu-id="8018c-143">Tato akce kontroleru jenom zobrazí formulář pro registraci, takže nevyžaduje žádné informace o modelu.</span><span class="sxs-lookup"><span data-stu-id="8018c-143">This controller action just displays the checkout form, so it doesn't require any model information.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample6.cs)]

<span data-ttu-id="8018c-144">Metoda AddressAndPayment POST se bude řídit stejným vzorem, který jsme použili v StoreManagerController: bude se pokusit přijmout odeslání formuláře a dokončit objednávku a formulář bude znovu zobrazen, pokud selže.</span><span class="sxs-lookup"><span data-stu-id="8018c-144">Our AddressAndPayment POST method will follow the same pattern we used in the StoreManagerController: it will try to accept the form submission and complete the order, and will re-display the form if it fails.</span></span>

<span data-ttu-id="8018c-145">Po ověření, že vstup na formuláři splňuje naše požadavky na ověření pro objednávku, zkontrolujeme přímo hodnotu formuláře PromoCode.</span><span class="sxs-lookup"><span data-stu-id="8018c-145">After validating the form input meets our validation requirements for an Order, we will check the PromoCode form value directly.</span></span> <span data-ttu-id="8018c-146">Za předpokladu, že všechno je správné, uložíme aktualizované informace s objednávkou, poznáte objekt ShoppingCart, aby se dokončil proces pořadí, a přesměruje na akci dokončení.</span><span class="sxs-lookup"><span data-stu-id="8018c-146">Assuming everything is correct, we will save the updated information with the order, tell the ShoppingCart object to complete the order process, and redirect to the Complete action.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample7.cs)]

<span data-ttu-id="8018c-147">Po úspěšném dokončení procesu registrace budou uživatelé přesměrováni na dokončení akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="8018c-147">Upon successful completion of the checkout process, users will be redirected to the Complete controller action.</span></span> <span data-ttu-id="8018c-148">Tato akce provede jednoduchou kontrolu za účelem ověření, že objednávka skutečně patří přihlášenému uživateli před zobrazením čísla objednávky jako potvrzení.</span><span class="sxs-lookup"><span data-stu-id="8018c-148">This action will perform a simple check to validate that the order does indeed belong to the logged-in user before showing the order number as a confirmation.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample8.cs)]

<span data-ttu-id="8018c-149">*Poznámka: ve složce/Views/Shared se při zahájení projektu automaticky vytvořilo zobrazení chyby pro nás.*</span><span class="sxs-lookup"><span data-stu-id="8018c-149">*Note: The Error view was automatically created for us in the /Views/Shared folder when we began the project.*</span></span>

<span data-ttu-id="8018c-150">Úplný kód CheckoutController je následující:</span><span class="sxs-lookup"><span data-stu-id="8018c-150">The complete CheckoutController code is as follows:</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample9.cs)]

## <a name="adding-the-addressandpayment-view"></a><span data-ttu-id="8018c-151">Přidání zobrazení AddressAndPayment</span><span class="sxs-lookup"><span data-stu-id="8018c-151">Adding the AddressAndPayment view</span></span>

<span data-ttu-id="8018c-152">Nyní vytvoříme zobrazení AddressAndPayment.</span><span class="sxs-lookup"><span data-stu-id="8018c-152">Now, let's create the AddressAndPayment view.</span></span> <span data-ttu-id="8018c-153">Klikněte pravým tlačítkem myši na jednu z akcí AddressAndPayment Controller a přidejte zobrazení s názvem AddressAndPayment, které je silně typované jako objednávka a používá úpravu šablony, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="8018c-153">Right-click on one of the AddressAndPayment controller actions and add a view named AddressAndPayment which is strongly typed as an Order and uses the Edit template, as shown below.</span></span>

![](mvc-music-store-part-9/_static/image6.png)

<span data-ttu-id="8018c-154">Toto zobrazení využívá dva techniky, které jsme prohlédli při sestavování zobrazení StoreManagerEdit:</span><span class="sxs-lookup"><span data-stu-id="8018c-154">This view will make use of two of the techniques we looked at while building the StoreManagerEdit view:</span></span>

- <span data-ttu-id="8018c-155">K zobrazení polí formuláře pro model objednávky použijeme HTML. EditorForModel ().</span><span class="sxs-lookup"><span data-stu-id="8018c-155">We will use Html.EditorForModel() to display form fields for the Order model</span></span>
- <span data-ttu-id="8018c-156">Použijeme pravidla ověřování s použitím třídy Order s atributy ověřování.</span><span class="sxs-lookup"><span data-stu-id="8018c-156">We will leverage validation rules using an Order class with validation attributes</span></span>

<span data-ttu-id="8018c-157">Začneme aktualizací kódu formuláře tak, aby používal HTML. EditorForModel () následovaný dalším textovým polem pro propagační kód.</span><span class="sxs-lookup"><span data-stu-id="8018c-157">We'll start by updating the form code to use Html.EditorForModel(), followed by an additional textbox for the Promo Code.</span></span> <span data-ttu-id="8018c-158">Úplný kód pro zobrazení AddressAndPayment je uveden níže.</span><span class="sxs-lookup"><span data-stu-id="8018c-158">The complete code for the AddressAndPayment view is shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample10.cshtml)]

## <a name="defining-validation-rules-for-the-order"></a><span data-ttu-id="8018c-159">Definování ověřovacích pravidel pro objednávku</span><span class="sxs-lookup"><span data-stu-id="8018c-159">Defining validation rules for the Order</span></span>

<span data-ttu-id="8018c-160">Teď, když je naše zobrazení nastavené, nastavíme pro model objednávky pravidla ověřování, která jsme předtím používali pro model alba.</span><span class="sxs-lookup"><span data-stu-id="8018c-160">Now that our view is set up, we will set up the validation rules for our Order model as we did previously for the Album model.</span></span> <span data-ttu-id="8018c-161">Klikněte pravým tlačítkem na složku modely a přidejte třídu s názvem Order.</span><span class="sxs-lookup"><span data-stu-id="8018c-161">Right-click on the Models folder and add a class named Order.</span></span> <span data-ttu-id="8018c-162">Kromě ověřovacích atributů, které jsme pro album používali dřív, použijeme k ověření e-mailové adresy uživatele regulární výraz.</span><span class="sxs-lookup"><span data-stu-id="8018c-162">In addition to the validation attributes we used previously for the Album, we will also be using a Regular Expression to validate the user's email address.</span></span>

[!code-csharp[Main](mvc-music-store-part-9/samples/sample11.cs)]

<span data-ttu-id="8018c-163">Při pokusu o odeslání formuláře s chybějícími nebo neplatnými informacemi se nyní zobrazí chybová zpráva s použitím ověřování na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="8018c-163">Attempting to submit the form with missing or invalid information will now show error message using client-side validation.</span></span>

![](mvc-music-store-part-9/_static/image7.png)

<span data-ttu-id="8018c-164">V pořádku jsme dokončili většinu pevné práce pro proces registrace; jenom pár lichá a končí na dokončení.</span><span class="sxs-lookup"><span data-stu-id="8018c-164">Okay, we've done most of the hard work for the checkout process; we just have a few odds and ends to finish.</span></span> <span data-ttu-id="8018c-165">Musíme přidat dvě jednoduchá zobrazení a musíme se postarat o předání informací o košíku během procesu přihlášení.</span><span class="sxs-lookup"><span data-stu-id="8018c-165">We need to add two simple views, and we need to take care of the handoff of the cart information during the login process.</span></span>

## <a name="adding-the-checkout-complete-view"></a><span data-ttu-id="8018c-166">Přidání zobrazení dokončené rezervace</span><span class="sxs-lookup"><span data-stu-id="8018c-166">Adding the Checkout Complete view</span></span>

<span data-ttu-id="8018c-167">Zobrazení dokončené rezervace je poměrně jednoduché, protože stačí zobrazit ID objednávky.</span><span class="sxs-lookup"><span data-stu-id="8018c-167">The Checkout Complete view is pretty simple, as it just needs to display the Order ID.</span></span> <span data-ttu-id="8018c-168">Klikněte pravým tlačítkem na akci dokončit kontroler a přidejte zobrazení s názvem dokončeno, které je silně typované jako celé číslo.</span><span class="sxs-lookup"><span data-stu-id="8018c-168">Right-click on the Complete controller action and add a view named Complete which is strongly typed as an int.</span></span>

![](mvc-music-store-part-9/_static/image8.png)

<span data-ttu-id="8018c-169">Nyní aktualizujeme kód zobrazení, aby se zobrazilo ID objednávky, jak je znázorněno níže.</span><span class="sxs-lookup"><span data-stu-id="8018c-169">Now we will update the view code to display the Order ID, as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample12.cshtml)]

## <a name="updating-the-error-view"></a><span data-ttu-id="8018c-170">Aktualizace zobrazení chyb</span><span class="sxs-lookup"><span data-stu-id="8018c-170">Updating The Error view</span></span>

<span data-ttu-id="8018c-171">Výchozí šablona obsahuje zobrazení chyb ve složce sdílené zobrazení, aby ji bylo možné znovu použít jinde v lokalitě.</span><span class="sxs-lookup"><span data-stu-id="8018c-171">The default template includes an Error view in the Shared views folder so that it can be re-used elsewhere in the site.</span></span> <span data-ttu-id="8018c-172">Toto zobrazení chyb obsahuje velmi jednoduchou chybu a nepoužívá rozložení webu, takže ji aktualizujeme.</span><span class="sxs-lookup"><span data-stu-id="8018c-172">This Error view contains a very simple error and doesn't use our site Layout, so we'll update it.</span></span>

<span data-ttu-id="8018c-173">Vzhledem k tomu, že se jedná o obecnou chybovou stránku, je obsah velmi jednoduchý.</span><span class="sxs-lookup"><span data-stu-id="8018c-173">Since this is a generic error page, the content is very simple.</span></span> <span data-ttu-id="8018c-174">Pokud chce uživatel opakovat akci, bude obsahovat zprávu a odkaz pro přechod na předchozí stránku v historii.</span><span class="sxs-lookup"><span data-stu-id="8018c-174">We'll include a message and a link to navigate to the previous page in history if the user wants to re-try their action.</span></span>

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample13.cshtml)]

> [!div class="step-by-step"]
> <span data-ttu-id="8018c-175">[Předchozí](mvc-music-store-part-8.md)
> [Další](mvc-music-store-part-10.md)</span><span class="sxs-lookup"><span data-stu-id="8018c-175">[Previous](mvc-music-store-part-8.md)
[Next](mvc-music-store-part-10.md)</span></span>

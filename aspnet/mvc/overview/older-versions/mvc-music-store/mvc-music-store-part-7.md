---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: 'Část 7: Členství a ověřování | Dokumentace Microsoftu'
author: jongalloway
description: V této sérii kurzů podrobně popisuje všechny kroky k vytvoření ukázkové aplikace ASP.NET MVC Music Store. 7. část se věnuje členství a autorizace.
ms.author: riande
ms.date: 10/13/2010
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: f5431d60506f5b0a0f4bbcd8e86b316c728a1191
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59415918"
---
# <a name="part-7-membership-and-authorization"></a><span data-ttu-id="97df9-104">Část 7: Členství a ověřování</span><span class="sxs-lookup"><span data-stu-id="97df9-104">Part 7: Membership and Authorization</span></span>

<span data-ttu-id="97df9-105">podle [Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="97df9-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="97df9-106">MVC Music Store jde o kurz, který se seznámíte, podrobné postupy pro vývoj pro web pomocí ASP.NET MVC a sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="97df9-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="97df9-107">Music Store MVC je jednoduché ukázku implementace úložiště prodává hudebních alb online, který implementuje správu základního webu, přihlášení uživatele a nákupního košíku funkce.</span><span class="sxs-lookup"><span data-stu-id="97df9-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="97df9-108">V této sérii kurzů podrobně popisuje všechny kroky k vytvoření ukázkové aplikace ASP.NET MVC Music Store.</span><span class="sxs-lookup"><span data-stu-id="97df9-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="97df9-109">7. část se věnuje členství a autorizace.</span><span class="sxs-lookup"><span data-stu-id="97df9-109">Part 7 covers Membership and Authorization.</span></span>


<span data-ttu-id="97df9-110">Správce Store kontroleru je nyní k dispozici všem uživatelům na našem webu.</span><span class="sxs-lookup"><span data-stu-id="97df9-110">Our Store Manager controller is currently accessible to anyone visiting our site.</span></span> <span data-ttu-id="97df9-111">Změňme ji omezit oprávnění na správce webu.</span><span class="sxs-lookup"><span data-stu-id="97df9-111">Let's change this to restrict permission to site administrators.</span></span>

## <a name="adding-the-accountcontroller-and-views"></a><span data-ttu-id="97df9-112">Přidání zobrazení a AccountController</span><span class="sxs-lookup"><span data-stu-id="97df9-112">Adding the AccountController and Views</span></span>

<span data-ttu-id="97df9-113">Jedním z rozdílů mezi kompletní šablonu webové aplikace ASP.NET MVC 3 a šablony ASP.NET MVC 3 prázdná webová aplikace je, že prázdnou šablonu neobsahuje řadič účet.</span><span class="sxs-lookup"><span data-stu-id="97df9-113">One difference between the full ASP.NET MVC 3 Web Application template and the ASP.NET MVC 3 Empty Web Application template is that the empty template doesn't include an Account Controller.</span></span> <span data-ttu-id="97df9-114">Přidáme řadič účet tak, že zkopírujete několik souborů z nové aplikace ASP.NET MVC vytvořené z úplné šablony webové aplikace ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="97df9-114">We'll add an Account Controller by copying a few files from a new ASP.NET MVC application created from the full ASP.NET MVC 3 Web Application template.</span></span>

<span data-ttu-id="97df9-115">Vytvoření nové aplikace ASP.NET MVC pomocí úplné šablony webové aplikace ASP.NET MVC 3 a zkopírujte následující soubory do stejného adresáře v našem projektu:</span><span class="sxs-lookup"><span data-stu-id="97df9-115">Create a new ASP.NET MVC application using the full ASP.NET MVC 3 Web Application template and copy the following files into the same directories in our project:</span></span>

1. <span data-ttu-id="97df9-116">Zkopírujte AccountController.cs v adresáři řadiče</span><span class="sxs-lookup"><span data-stu-id="97df9-116">Copy AccountController.cs in the Controllers directory</span></span>
2. <span data-ttu-id="97df9-117">Zkopírujte AccountModels v adresáři modelů</span><span class="sxs-lookup"><span data-stu-id="97df9-117">Copy AccountModels in the Models directory</span></span>
3. <span data-ttu-id="97df9-118">Vytvořte účet adresář do adresáře zobrazení a zkopírujte všechny čtyři zobrazení v</span><span class="sxs-lookup"><span data-stu-id="97df9-118">Create an Account directory inside the Views directory and copy all four views in</span></span>

<span data-ttu-id="97df9-119">Změna oboru názvů pro třídy Kontroleru a Model, začnou se MvcMusicStore.</span><span class="sxs-lookup"><span data-stu-id="97df9-119">Change the namespace for the Controller and Model classes so they begin with MvcMusicStore.</span></span> <span data-ttu-id="97df9-120">Třída AccountController by měl používat obor názvů MvcMusicStore.Controllers a třída AccountModels by měl používat obor názvů MvcMusicStore.Models.</span><span class="sxs-lookup"><span data-stu-id="97df9-120">The AccountController class should use the MvcMusicStore.Controllers namespace, and the AccountModels class should use the MvcMusicStore.Models namespace.</span></span>

*<span data-ttu-id="97df9-121">Poznámka: Tyto soubory jsou také k dispozici MvcMusicStore Assets.zip soubor ke stažení, ze kterého jsme naše lokality návrhu soubory zkopírovány na začátku tohoto kurzu.</span><span class="sxs-lookup"><span data-stu-id="97df9-121">Note: These files are also available in the MvcMusicStore-Assets.zip download from which we copied our site design files at the beginning of the tutorial.</span></span> <span data-ttu-id="97df9-122">Členství soubory jsou umístěny v adresáři kódu.</span><span class="sxs-lookup"><span data-stu-id="97df9-122">The Membership files are located in the Code directory.</span></span>*

<span data-ttu-id="97df9-123">Aktualizované řešení by měl vypadat nějak takto:</span><span class="sxs-lookup"><span data-stu-id="97df9-123">The updated solution should look like the following:</span></span>

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a><span data-ttu-id="97df9-124">Přidání správce s webem konfigurace ASP.NET</span><span class="sxs-lookup"><span data-stu-id="97df9-124">Adding an Administrative User with the ASP.NET Configuration site</span></span>

<span data-ttu-id="97df9-125">Předtím, než jsme v našem webu vyžadují autorizace, potřebujeme vytvořit uživatele s přístupem.</span><span class="sxs-lookup"><span data-stu-id="97df9-125">Before we require Authorization in our website, we'll need to create a user with access.</span></span> <span data-ttu-id="97df9-126">Nejjednodušší způsob, jak vytvořit uživatele je použití webu integrované konfigurace technologie ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="97df9-126">The easiest way to create a user is to use the built-in ASP.NET Configuration website.</span></span>

<span data-ttu-id="97df9-127">Kliknutím na ikonu v okně Průzkumník řešení po spuštění webu konfigurace technologie ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="97df9-127">Launch the ASP.NET Configuration website by clicking following the icon in the Solution Explorer.</span></span>

![](mvc-music-store-part-7/_static/image2.png)

<span data-ttu-id="97df9-128">Tím se spustí konfigurace webu.</span><span class="sxs-lookup"><span data-stu-id="97df9-128">This launches a configuration website.</span></span> <span data-ttu-id="97df9-129">Klikněte na kartu zabezpečení na domovské obrazovce a pak klikněte na odkaz "Povolit role" na střed obrazovky.</span><span class="sxs-lookup"><span data-stu-id="97df9-129">Click on the Security tab on the home screen, then click the "Enable roles" link in the center of the screen.</span></span>

![](mvc-music-store-part-7/_static/image3.png)

<span data-ttu-id="97df9-130">Klikněte na odkaz "Vytvořit nebo spravovat role".</span><span class="sxs-lookup"><span data-stu-id="97df9-130">Click the "Create or Manage roles" link.</span></span>

![](mvc-music-store-part-7/_static/image4.png)

<span data-ttu-id="97df9-131">Zadejte "Administrator" jako název role a klikněte na tlačítko Přidat roli.</span><span class="sxs-lookup"><span data-stu-id="97df9-131">Enter "Administrator" as the role name and press the Add Role button.</span></span>

![](mvc-music-store-part-7/_static/image5.png)

<span data-ttu-id="97df9-132">Klikněte na tlačítko Zpět a potom klikněte na odkaz vytvořit uživatele na levé straně.</span><span class="sxs-lookup"><span data-stu-id="97df9-132">Click the Back button, then click on the Create user link on the left side.</span></span>

![](mvc-music-store-part-7/_static/image6.png)

<span data-ttu-id="97df9-133">Vyplňte pole informace uživatele na levé straně pomocí následujících informací:</span><span class="sxs-lookup"><span data-stu-id="97df9-133">Fill in the user information fields on the left using the following information:</span></span>

| **<span data-ttu-id="97df9-134">Pole</span><span class="sxs-lookup"><span data-stu-id="97df9-134">Field</span></span>** | **<span data-ttu-id="97df9-135">Value</span><span class="sxs-lookup"><span data-stu-id="97df9-135">Value</span></span>** |
| --- | --- |
| **<span data-ttu-id="97df9-136">Uživatelské jméno</span><span class="sxs-lookup"><span data-stu-id="97df9-136">User Name</span></span>** | <span data-ttu-id="97df9-137">Správce</span><span class="sxs-lookup"><span data-stu-id="97df9-137">Administrator</span></span> |
| **<span data-ttu-id="97df9-138">Heslo</span><span class="sxs-lookup"><span data-stu-id="97df9-138">Password</span></span>** | <span data-ttu-id="97df9-139">/ password123!</span><span class="sxs-lookup"><span data-stu-id="97df9-139">password123!</span></span> |
| **<span data-ttu-id="97df9-140">Potvrzení hesla</span><span class="sxs-lookup"><span data-stu-id="97df9-140">Confirm Password</span></span>** | <span data-ttu-id="97df9-141">/ password123!</span><span class="sxs-lookup"><span data-stu-id="97df9-141">password123!</span></span> |
| **<span data-ttu-id="97df9-142">E-mail</span><span class="sxs-lookup"><span data-stu-id="97df9-142">E-mail</span></span>** | <span data-ttu-id="97df9-143">(žádné e-mailová adresa bude fungovat)</span><span class="sxs-lookup"><span data-stu-id="97df9-143">(any email address will work)</span></span> |
| **<span data-ttu-id="97df9-144">Bezpečnostní otázku</span><span class="sxs-lookup"><span data-stu-id="97df9-144">Security Question</span></span>** | <span data-ttu-id="97df9-145">(cokoli, co chcete)</span><span class="sxs-lookup"><span data-stu-id="97df9-145">(whatever you like)</span></span> |
| **<span data-ttu-id="97df9-146">Zabezpečovací odpověď</span><span class="sxs-lookup"><span data-stu-id="97df9-146">Security Answer</span></span>** | <span data-ttu-id="97df9-147">(cokoli, co chcete)</span><span class="sxs-lookup"><span data-stu-id="97df9-147">(whatever you like)</span></span> |

*<span data-ttu-id="97df9-148">Poznámka: Samozřejmě můžete použít jakékoli heslo, které chcete.</span><span class="sxs-lookup"><span data-stu-id="97df9-148">Note: You can of course use any password you'd like.</span></span> <span data-ttu-id="97df9-149">Výchozí nastavení zabezpečení hesel vyžadují heslo, které má 7 znaků a obsahuje jeden jiný než alfanumerický znak.</span><span class="sxs-lookup"><span data-stu-id="97df9-149">The default password security settings require a password that is 7 characters long and contains one non-alphanumeric character.</span></span>*

<span data-ttu-id="97df9-150">Vyberte roli správce u tohoto uživatele a klikněte na tlačítko Vytvořit uživatele.</span><span class="sxs-lookup"><span data-stu-id="97df9-150">Select the Administrator role for this user, and click the Create User button.</span></span>

![](mvc-music-store-part-7/_static/image7.png)

<span data-ttu-id="97df9-151">V tomto okamžiku byste měli vidět zprávu s oznámením, že uživatel byl úspěšně vytvořen.</span><span class="sxs-lookup"><span data-stu-id="97df9-151">At this point, you should see a message indicating that the user was created successfully.</span></span>

![](mvc-music-store-part-7/_static/image8.png)

<span data-ttu-id="97df9-152">Teď můžete zavřít okno prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="97df9-152">You can now close the browser window.</span></span>

## <a name="role-based-authorization"></a><span data-ttu-id="97df9-153">Autorizace na základě rolí</span><span class="sxs-lookup"><span data-stu-id="97df9-153">Role-based Authorization</span></span>

<span data-ttu-id="97df9-154">Nyní jsme můžete omezit přístup k určení, že uživatel musí být v roli správce pro přístup k žádné akci kontroleru ve třídě StoreManagerController pomocí atributu [Authorize].</span><span class="sxs-lookup"><span data-stu-id="97df9-154">Now we can restrict access to the StoreManagerController using the [Authorize] attribute, specifying that the user must be in the Administrator role to access any controller action in the class.</span></span>

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

*<span data-ttu-id="97df9-155">Poznámka: Atribut [Authorize] se můžou umístit na konkrétní akci metody i na úrovni třídy Kontroleru.</span><span class="sxs-lookup"><span data-stu-id="97df9-155">Note: The [Authorize] attribute can be placed on specific action methods as well as at the Controller class level.</span></span>*

<span data-ttu-id="97df9-156">Teď přejdete do /StoreManager otevře dialogové okno přihlášení:</span><span class="sxs-lookup"><span data-stu-id="97df9-156">Now browsing to /StoreManager brings up a Log On dialog:</span></span>

![](mvc-music-store-part-7/_static/image9.png)

<span data-ttu-id="97df9-157">Po přihlášení se náš nový účet správce, jsme byli schopni přejděte na obrazovku alba upravit jako před.</span><span class="sxs-lookup"><span data-stu-id="97df9-157">After logging on with our new Administrator account, we're able to go to the Album Edit screen as before.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="97df9-158">[Předchozí](mvc-music-store-part-6.md)
> [další](mvc-music-store-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="97df9-158">[Previous](mvc-music-store-part-6.md)
[Next](mvc-music-store-part-8.md)</span></span>

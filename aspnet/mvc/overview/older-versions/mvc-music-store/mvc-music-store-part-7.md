---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
title: '7\. část: členství a autorizace | Microsoft Docs'
author: jongalloway
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 7 pokrývá členství a autorizaci.
ms.author: riande
ms.date: 10/13/2010
ms.assetid: c8511ebe-68bc-4240-87c3-d5ced84a3f37
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-7
msc.type: authoredcontent
ms.openlocfilehash: a6a1a936e0ea29ea36721ba78f35845401f74c01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539198"
---
# <a name="part-7-membership-and-authorization"></a><span data-ttu-id="09762-104">7\. část: Členství a ověřování</span><span class="sxs-lookup"><span data-stu-id="09762-104">Part 7: Membership and Authorization</span></span>

<span data-ttu-id="09762-105">o [Jan Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="09762-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="09762-106">Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio pro vývoj webů.</span><span class="sxs-lookup"><span data-stu-id="09762-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="09762-107">Úložiště hudby MVC je zjednodušená ukázka implementace úložiště, která prodává hudební alba online a implementuje základní funkce pro správu webů, přihlašování uživatelů a nákupních košíků.</span><span class="sxs-lookup"><span data-stu-id="09762-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="09762-108">V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště.</span><span class="sxs-lookup"><span data-stu-id="09762-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="09762-109">Část 7 pokrývá členství a autorizaci.</span><span class="sxs-lookup"><span data-stu-id="09762-109">Part 7 covers Membership and Authorization.</span></span>

<span data-ttu-id="09762-110">Náš kontroler Správce úložiště je momentálně přístupný pro každého navštívení našeho webu.</span><span class="sxs-lookup"><span data-stu-id="09762-110">Our Store Manager controller is currently accessible to anyone visiting our site.</span></span> <span data-ttu-id="09762-111">Pojďme to změnit, aby se omezilo oprávnění správců webu.</span><span class="sxs-lookup"><span data-stu-id="09762-111">Let's change this to restrict permission to site administrators.</span></span>

## <a name="adding-the-accountcontroller-and-views"></a><span data-ttu-id="09762-112">Přidání AccountController a zobrazení</span><span class="sxs-lookup"><span data-stu-id="09762-112">Adding the AccountController and Views</span></span>

<span data-ttu-id="09762-113">Jeden rozdíl mezi celou šablonou webové aplikace ASP.NET MVC 3 a šablonou prázdné webové aplikace ASP.NET MVC 3 je, že prázdná šablona neobsahuje kontroler účtu.</span><span class="sxs-lookup"><span data-stu-id="09762-113">One difference between the full ASP.NET MVC 3 Web Application template and the ASP.NET MVC 3 Empty Web Application template is that the empty template doesn't include an Account Controller.</span></span> <span data-ttu-id="09762-114">Přidáme řadič účtu zkopírováním několika souborů z nové aplikace ASP.NET MVC vytvořené z úplné šablony webové aplikace ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="09762-114">We'll add an Account Controller by copying a few files from a new ASP.NET MVC application created from the full ASP.NET MVC 3 Web Application template.</span></span>

<span data-ttu-id="09762-115">Vytvořte novou aplikaci ASP.NET MVC pomocí úplné šablony webové aplikace ASP.NET MVC 3 a zkopírujte následující soubory do stejných adresářů v našem projektu:</span><span class="sxs-lookup"><span data-stu-id="09762-115">Create a new ASP.NET MVC application using the full ASP.NET MVC 3 Web Application template and copy the following files into the same directories in our project:</span></span>

1. <span data-ttu-id="09762-116">Kopírování AccountController.cs do adresáře Controllers</span><span class="sxs-lookup"><span data-stu-id="09762-116">Copy AccountController.cs in the Controllers directory</span></span>
2. <span data-ttu-id="09762-117">Kopírování AccountModels do adresáře modelů</span><span class="sxs-lookup"><span data-stu-id="09762-117">Copy AccountModels in the Models directory</span></span>
3. <span data-ttu-id="09762-118">Vytvořte adresář účtu v adresáři zobrazení a zkopírujte všechna čtyři zobrazení v</span><span class="sxs-lookup"><span data-stu-id="09762-118">Create an Account directory inside the Views directory and copy all four views in</span></span>

<span data-ttu-id="09762-119">Změňte obor názvů pro třídy Controller a model tak, aby začínaly na MvcMusicStore.</span><span class="sxs-lookup"><span data-stu-id="09762-119">Change the namespace for the Controller and Model classes so they begin with MvcMusicStore.</span></span> <span data-ttu-id="09762-120">Třída AccountController by měla používat obor názvů MvcMusicStore. Controllers a třída AccountModels by měla používat obor názvů MvcMusicStore. Models.</span><span class="sxs-lookup"><span data-stu-id="09762-120">The AccountController class should use the MvcMusicStore.Controllers namespace, and the AccountModels class should use the MvcMusicStore.Models namespace.</span></span>

<span data-ttu-id="09762-121">*Poznámka: tyto soubory jsou také k dispozici ve stažení MvcMusicStore-Assets. zip, ze kterého jsme zkopírovali soubory návrhu webu na začátku tohoto kurzu. Soubory členství jsou umístěny v adresáři kódu.*</span><span class="sxs-lookup"><span data-stu-id="09762-121">*Note: These files are also available in the MvcMusicStore-Assets.zip download from which we copied our site design files at the beginning of the tutorial. The Membership files are located in the Code directory.*</span></span>

<span data-ttu-id="09762-122">Aktualizované řešení by mělo vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="09762-122">The updated solution should look like the following:</span></span>

![](mvc-music-store-part-7/_static/image1.png)

## <a name="adding-an-administrative-user-with-the-aspnet-configuration-site"></a><span data-ttu-id="09762-123">Přidání administrativního uživatele s lokalitou konfigurace ASP.NET</span><span class="sxs-lookup"><span data-stu-id="09762-123">Adding an Administrative User with the ASP.NET Configuration site</span></span>

<span data-ttu-id="09762-124">Než budeme vyžadovat autorizaci na našem webu, bude nutné vytvořit uživatele s přístupem.</span><span class="sxs-lookup"><span data-stu-id="09762-124">Before we require Authorization in our website, we'll need to create a user with access.</span></span> <span data-ttu-id="09762-125">Nejjednodušší způsob, jak vytvořit uživatele, je použít vestavěný web ASP.NET Configuration.</span><span class="sxs-lookup"><span data-stu-id="09762-125">The easiest way to create a user is to use the built-in ASP.NET Configuration website.</span></span>

<span data-ttu-id="09762-126">Spusťte web ASP.NET Configuration kliknutím na ikonu v Průzkumník řešení.</span><span class="sxs-lookup"><span data-stu-id="09762-126">Launch the ASP.NET Configuration website by clicking following the icon in the Solution Explorer.</span></span>

![](mvc-music-store-part-7/_static/image2.png)

<span data-ttu-id="09762-127">Tím se spustí konfigurační Web.</span><span class="sxs-lookup"><span data-stu-id="09762-127">This launches a configuration website.</span></span> <span data-ttu-id="09762-128">Klikněte na kartu zabezpečení na domovské obrazovce a potom klikněte na odkaz Povolit role v centru obrazovky.</span><span class="sxs-lookup"><span data-stu-id="09762-128">Click on the Security tab on the home screen, then click the "Enable roles" link in the center of the screen.</span></span>

![](mvc-music-store-part-7/_static/image3.png)

<span data-ttu-id="09762-129">Klikněte na odkaz vytvořit nebo spravovat role.</span><span class="sxs-lookup"><span data-stu-id="09762-129">Click the "Create or Manage roles" link.</span></span>

![](mvc-music-store-part-7/_static/image4.png)

<span data-ttu-id="09762-130">Jako název role zadejte "Administrator" a stiskněte tlačítko Přidat roli.</span><span class="sxs-lookup"><span data-stu-id="09762-130">Enter "Administrator" as the role name and press the Add Role button.</span></span>

![](mvc-music-store-part-7/_static/image5.png)

<span data-ttu-id="09762-131">Klikněte na tlačítko zpět a potom klikněte na odkaz vytvořit uživatele na levé straně.</span><span class="sxs-lookup"><span data-stu-id="09762-131">Click the Back button, then click on the Create user link on the left side.</span></span>

![](mvc-music-store-part-7/_static/image6.png)

<span data-ttu-id="09762-132">Vyplňte pole informace o uživateli vlevo pomocí následujících informací:</span><span class="sxs-lookup"><span data-stu-id="09762-132">Fill in the user information fields on the left using the following information:</span></span>

| <span data-ttu-id="09762-133">**Pole**</span><span class="sxs-lookup"><span data-stu-id="09762-133">**Field**</span></span> | <span data-ttu-id="09762-134">**Hodnota**</span><span class="sxs-lookup"><span data-stu-id="09762-134">**Value**</span></span> |
| --- | --- |
| <span data-ttu-id="09762-135">**Uživatelské jméno**</span><span class="sxs-lookup"><span data-stu-id="09762-135">**User Name**</span></span> | <span data-ttu-id="09762-136">Správce</span><span class="sxs-lookup"><span data-stu-id="09762-136">Administrator</span></span> |
| <span data-ttu-id="09762-137">**Heslo**</span><span class="sxs-lookup"><span data-stu-id="09762-137">**Password**</span></span> | <span data-ttu-id="09762-138">password123!</span><span class="sxs-lookup"><span data-stu-id="09762-138">password123!</span></span> |
| <span data-ttu-id="09762-139">**Potvrzení hesla**</span><span class="sxs-lookup"><span data-stu-id="09762-139">**Confirm Password**</span></span> | <span data-ttu-id="09762-140">password123!</span><span class="sxs-lookup"><span data-stu-id="09762-140">password123!</span></span> |
| <span data-ttu-id="09762-141">**E-mail**</span><span class="sxs-lookup"><span data-stu-id="09762-141">**E-mail**</span></span> | <span data-ttu-id="09762-142">(bude fungovat libovolná e-mailová adresa)</span><span class="sxs-lookup"><span data-stu-id="09762-142">(any email address will work)</span></span> |
| <span data-ttu-id="09762-143">**Bezpečnostní otázka**</span><span class="sxs-lookup"><span data-stu-id="09762-143">**Security Question**</span></span> | <span data-ttu-id="09762-144">(bez ohledu na to, co chcete)</span><span class="sxs-lookup"><span data-stu-id="09762-144">(whatever you like)</span></span> |
| <span data-ttu-id="09762-145">**Bezpečnostní odpověď**</span><span class="sxs-lookup"><span data-stu-id="09762-145">**Security Answer**</span></span> | <span data-ttu-id="09762-146">(bez ohledu na to, co chcete)</span><span class="sxs-lookup"><span data-stu-id="09762-146">(whatever you like)</span></span> |

<span data-ttu-id="09762-147">*Poznámka: můžete samozřejmě použít jakékoli heslo, které chcete. Výchozí nastavení zabezpečení hesla vyžaduje heslo, které je delší než 7 znaků a obsahuje jeden nealfanumerický znak.*</span><span class="sxs-lookup"><span data-stu-id="09762-147">*Note: You can of course use any password you'd like. The default password security settings require a password that is 7 characters long and contains one non-alphanumeric character.*</span></span>

<span data-ttu-id="09762-148">Vyberte roli správce pro tohoto uživatele a klikněte na tlačítko vytvořit uživatele.</span><span class="sxs-lookup"><span data-stu-id="09762-148">Select the Administrator role for this user, and click the Create User button.</span></span>

![](mvc-music-store-part-7/_static/image7.png)

<span data-ttu-id="09762-149">V tomto okamžiku by se měla zobrazit zpráva oznamující, že uživatel byl úspěšně vytvořen.</span><span class="sxs-lookup"><span data-stu-id="09762-149">At this point, you should see a message indicating that the user was created successfully.</span></span>

![](mvc-music-store-part-7/_static/image8.png)

<span data-ttu-id="09762-150">Nyní můžete zavřít okno prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="09762-150">You can now close the browser window.</span></span>

## <a name="role-based-authorization"></a><span data-ttu-id="09762-151">Autorizace na základě rolí</span><span class="sxs-lookup"><span data-stu-id="09762-151">Role-based Authorization</span></span>

<span data-ttu-id="09762-152">Nyní můžeme omezit přístup k StoreManagerController pomocí atributu [autorizovat], který určuje, že uživatel musí být v roli správce pro přístup k jakékoli akci kontroleru ve třídě.</span><span class="sxs-lookup"><span data-stu-id="09762-152">Now we can restrict access to the StoreManagerController using the [Authorize] attribute, specifying that the user must be in the Administrator role to access any controller action in the class.</span></span>

[!code-csharp[Main](mvc-music-store-part-7/samples/sample1.cs)]

<span data-ttu-id="09762-153">*Poznámka: atribut [autorizační] lze umístit na konkrétní metody akce i na úrovni třídy řadiče.*</span><span class="sxs-lookup"><span data-stu-id="09762-153">*Note: The [Authorize] attribute can be placed on specific action methods as well as at the Controller class level.*</span></span>

<span data-ttu-id="09762-154">Když teď přejdete na/StoreManager, zobrazí se dialogové okno pro přihlášení:</span><span class="sxs-lookup"><span data-stu-id="09762-154">Now browsing to /StoreManager brings up a Log On dialog:</span></span>

![](mvc-music-store-part-7/_static/image9.png)

<span data-ttu-id="09762-155">Až se přihlásíte pomocí našeho nového účtu správce, můžeme přejít na obrazovku pro úpravy alba stejně jako dřív.</span><span class="sxs-lookup"><span data-stu-id="09762-155">After logging on with our new Administrator account, we're able to go to the Album Edit screen as before.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="09762-156">[Předchozí](mvc-music-store-part-6.md)
> [Další](mvc-music-store-part-8.md)</span><span class="sxs-lookup"><span data-stu-id="09762-156">[Previous](mvc-music-store-part-6.md)
[Next](mvc-music-store-part-8.md)</span></span>

---
uid: identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
title: Změna primárního klíče pro uživatele v ASP.NET Identity-ASP.NET 4. x
author: Rick-Anderson
description: V Visual Studio 2013 výchozí webová aplikace používá pro klíč pro uživatelské účty řetězcovou hodnotu. ASP.NET Identity umožňuje změnit typ...
ms.author: riande
ms.date: 09/30/2014
ms.assetid: 44925849-5762-4504-a8cd-8f0cd06f6dc3
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/change-primary-key-for-users-in-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 0afea8eacfc646f1489b87629fdb2d437815d88c
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519138"
---
# <a name="change-primary-key-for-users-in-aspnet-identity"></a><span data-ttu-id="5e982-104">Změna primárního klíče uživatelů v ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="5e982-104">Change Primary Key for Users in ASP.NET Identity</span></span>

<span data-ttu-id="5e982-105">podle [Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="5e982-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="5e982-106">V Visual Studio 2013 výchozí webová aplikace používá pro klíč pro uživatelské účty řetězcovou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="5e982-106">In Visual Studio 2013, the default web application uses a string value for the key for user accounts.</span></span> <span data-ttu-id="5e982-107">ASP.NET Identity umožňuje změnit typ klíče tak, aby splňoval požadavky na data.</span><span class="sxs-lookup"><span data-stu-id="5e982-107">ASP.NET Identity enables you to change the type of the key to meet your data requirements.</span></span> <span data-ttu-id="5e982-108">Například můžete změnit typ klíče z řetězce na celé číslo.</span><span class="sxs-lookup"><span data-stu-id="5e982-108">For example, you can change the type of the key from a string to an integer.</span></span>
> 
> <span data-ttu-id="5e982-109">V tomto tématu se dozvíte, jak začít s výchozí webovou aplikací a jak změnit klíč uživatelského účtu na celé číslo.</span><span class="sxs-lookup"><span data-stu-id="5e982-109">This topic shows how to start with the default web application and change the user account key to an integer.</span></span> <span data-ttu-id="5e982-110">Stejné úpravy můžete použít k implementaci libovolného typu klíče v projektu.</span><span class="sxs-lookup"><span data-stu-id="5e982-110">You can use the same modifications to implement any type of key in your project.</span></span> <span data-ttu-id="5e982-111">Ukazuje, jak provést tyto změny ve výchozí webové aplikaci, ale můžete použít podobné změny v přizpůsobené aplikaci.</span><span class="sxs-lookup"><span data-stu-id="5e982-111">It shows how to make these changes in the default web application, but you could apply similar modifications to a customized application.</span></span> <span data-ttu-id="5e982-112">Zobrazuje změny potřebné při práci s MVC nebo webovými formuláři.</span><span class="sxs-lookup"><span data-stu-id="5e982-112">It shows the changes needed when working with MVC or Web Forms.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="5e982-113">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="5e982-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="5e982-114">Visual Studio 2013 s aktualizací Update 2 (nebo novější)</span><span class="sxs-lookup"><span data-stu-id="5e982-114">Visual Studio 2013 with Update 2 (or later)</span></span>
> - <span data-ttu-id="5e982-115">ASP.NET Identity 2,1 nebo novější</span><span class="sxs-lookup"><span data-stu-id="5e982-115">ASP.NET Identity 2.1 or later</span></span>

<span data-ttu-id="5e982-116">K provedení kroků v tomto kurzu musíte mít Visual Studio 2013 Update 2 (nebo novější) a webovou aplikaci vytvořenou v šabloně webové aplikace ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="5e982-116">To perform the steps in this tutorial, you must have Visual Studio 2013 Update 2 (or later), and a web application created from the ASP.NET Web Application template.</span></span> <span data-ttu-id="5e982-117">Šablona se změnila ve Update 3.</span><span class="sxs-lookup"><span data-stu-id="5e982-117">The template changed in Update 3.</span></span> <span data-ttu-id="5e982-118">V tomto tématu se dozvíte, jak změnit šablonu v Update 2 a Update 3.</span><span class="sxs-lookup"><span data-stu-id="5e982-118">This topic shows how to change the template in Update 2 and Update 3.</span></span>

<span data-ttu-id="5e982-119">Toto téma obsahuje následující oddíly:</span><span class="sxs-lookup"><span data-stu-id="5e982-119">This topic contains the following sections:</span></span>

- [<span data-ttu-id="5e982-120">Změna typu klíče ve třídě uživatele identity</span><span class="sxs-lookup"><span data-stu-id="5e982-120">Change the type of the key in the Identity user class</span></span>](#userclass)
- [<span data-ttu-id="5e982-121">Přidat přizpůsobené třídy identity, které používají typ klíče</span><span class="sxs-lookup"><span data-stu-id="5e982-121">Add customized Identity classes that use the key type</span></span>](#customclass)
- [<span data-ttu-id="5e982-122">Změna třídy kontextu a Správce uživatelů na použití typu klíče</span><span class="sxs-lookup"><span data-stu-id="5e982-122">Change the context class and user manager to use the key type</span></span>](#context)
- [<span data-ttu-id="5e982-123">Změna spouštěcí konfigurace tak, aby používala typ klíče</span><span class="sxs-lookup"><span data-stu-id="5e982-123">Change start-up configuration to use the key type</span></span>](#startup)
- [<span data-ttu-id="5e982-124">V případě MVC s aktualizací Update 2 změňte AccountController tak, aby předával typ klíče.</span><span class="sxs-lookup"><span data-stu-id="5e982-124">For MVC with Update 2, change the AccountController to pass the key type</span></span>](#mvcupdate2)
- [<span data-ttu-id="5e982-125">Pro MVC s aktualizací Update 3 změňte AccountController a ManageController, aby se předal typ klíče.</span><span class="sxs-lookup"><span data-stu-id="5e982-125">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>](#mvcupdate3)
- [<span data-ttu-id="5e982-126">U webových formulářů s aktualizací Update 2 změňte stránky účtu, aby předávaly typ klíče.</span><span class="sxs-lookup"><span data-stu-id="5e982-126">For Web Forms with Update 2, change Account pages to pass the key type</span></span>](#webformsupdate2)
- [<span data-ttu-id="5e982-127">U webových formulářů s aktualizací Update 3 změňte stránky účtu, aby předávaly typ klíče.</span><span class="sxs-lookup"><span data-stu-id="5e982-127">For Web Forms with Update 3, change Account pages to pass the key type</span></span>](#webformsupdate3)
- [<span data-ttu-id="5e982-128">Spustit aplikaci</span><span class="sxs-lookup"><span data-stu-id="5e982-128">Run application</span></span>](#run)
- [<span data-ttu-id="5e982-129">Další materiály</span><span class="sxs-lookup"><span data-stu-id="5e982-129">Other resources</span></span>](#other)

<a id="userclass"></a>
## <a name="change-the-type-of-the-key-in-the-identity-user-class"></a><span data-ttu-id="5e982-130">Změna typu klíče ve třídě uživatele identity</span><span class="sxs-lookup"><span data-stu-id="5e982-130">Change the type of the key in the Identity user class</span></span>

<span data-ttu-id="5e982-131">V projektu vytvořeném pomocí šablony webové aplikace ASP.NET určete, že třída ApplicationUser používá pro klíč uživatelských účtů celé číslo.</span><span class="sxs-lookup"><span data-stu-id="5e982-131">In your project created from the ASP.NET Web Application template, specify that the ApplicationUser class uses an integer for the key for user accounts.</span></span> <span data-ttu-id="5e982-132">V IdentityModels.cs změňte třídu ApplicationUser na dědění z IdentityUser, která má typ **int** pro obecný parametr TKey.</span><span class="sxs-lookup"><span data-stu-id="5e982-132">In IdentityModels.cs, change the ApplicationUser class to inherit from IdentityUser that has a type of **int** for the TKey generic parameter.</span></span> <span data-ttu-id="5e982-133">Také předáte názvy tří přizpůsobených tříd, které ještě nebyly implementovány.</span><span class="sxs-lookup"><span data-stu-id="5e982-133">You also pass the names of three customized class which you have not implemented yet.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample1.cs?highlight=1-2)]

<span data-ttu-id="5e982-134">Změnili jste typ klíče, ale ve výchozím nastavení zbývající část aplikace stále předpokládá, že klíč je řetězec.</span><span class="sxs-lookup"><span data-stu-id="5e982-134">You have changed the type of the key, but, by default, the rest of the application still assumes the key is a string.</span></span> <span data-ttu-id="5e982-135">Je nutné explicitně určit typ klíče v kódu, který předpokládá řetězec.</span><span class="sxs-lookup"><span data-stu-id="5e982-135">You must explicitly indicate the type of the key in code that assumes a string.</span></span>

<span data-ttu-id="5e982-136">Ve třídě **ApplicationUser** změňte metodu **GenerateUserIdentityAsync** tak, aby zahrnovala int, jak je znázorněno ve zvýrazněném kódu níže.</span><span class="sxs-lookup"><span data-stu-id="5e982-136">In the **ApplicationUser** class, change the **GenerateUserIdentityAsync** method to include int, as shown in the highlighted code below.</span></span> <span data-ttu-id="5e982-137">Tato změna není nutná pro projekty webových formulářů se šablonou Update 3.</span><span class="sxs-lookup"><span data-stu-id="5e982-137">This change is not necessary for Web Forms projects with the Update 3 template.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample2.cs?highlight=2)]

<a id="customclass"></a>
## <a name="add-customized-identity-classes-that-use-the-key-type"></a><span data-ttu-id="5e982-138">Přidat přizpůsobené třídy identity, které používají typ klíče</span><span class="sxs-lookup"><span data-stu-id="5e982-138">Add customized Identity classes that use the key type</span></span>

<span data-ttu-id="5e982-139">Ostatní třídy identity, například IdentityUserRole, IdentityUserClaim, IdentityUserLogin, IdentityRole, UserStore, RoleStore, jsou stále nastaveny tak, aby používaly řetězcový klíč.</span><span class="sxs-lookup"><span data-stu-id="5e982-139">The other Identity classes, such as IdentityUserRole, IdentityUserClaim, IdentityUserLogin, IdentityRole, UserStore, RoleStore, are still set up to use a string key.</span></span> <span data-ttu-id="5e982-140">Vytvořte nové verze těchto tříd, které určují celé číslo pro klíč.</span><span class="sxs-lookup"><span data-stu-id="5e982-140">Create new versions of these classes that specify an integer for the key.</span></span> <span data-ttu-id="5e982-141">V těchto třídách nemusíte poskytovat mnohem implementační kód, primárně je pouze nastavení int jako klíč.</span><span class="sxs-lookup"><span data-stu-id="5e982-141">You do not need to provide much implementation code in these classes, you are primarily just setting int as the key.</span></span>

<span data-ttu-id="5e982-142">Do souboru IdentityModels.cs přidejte následující třídy.</span><span class="sxs-lookup"><span data-stu-id="5e982-142">Add the following classes to your IdentityModels.cs file.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample3.cs)]

<a id="context"></a>
## <a name="change-the-context-class-and-user-manager-to-use-the-key-type"></a><span data-ttu-id="5e982-143">Změna třídy kontextu a Správce uživatelů na použití typu klíče</span><span class="sxs-lookup"><span data-stu-id="5e982-143">Change the context class and user manager to use the key type</span></span>

<span data-ttu-id="5e982-144">V IdentityModels.cs změňte definici třídy **ApplicationDbContext** tak, aby používala vaše nové přizpůsobené třídy a **int** pro klíč, jak je znázorněno ve zvýrazněném kódu.</span><span class="sxs-lookup"><span data-stu-id="5e982-144">In IdentityModels.cs, change the definition of the **ApplicationDbContext** class to use your new customized classes and an **int** for the key, as shown in the highlighted code.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample4.cs?highlight=1-2)]

<span data-ttu-id="5e982-145">Parametr ThrowIfV1Schema již v konstruktoru není platný.</span><span class="sxs-lookup"><span data-stu-id="5e982-145">The ThrowIfV1Schema parameter is no longer valid in the constructor.</span></span> <span data-ttu-id="5e982-146">Změňte konstruktor tak, aby nepředával hodnotu ThrowIfV1Schema.</span><span class="sxs-lookup"><span data-stu-id="5e982-146">Change the constructor so it does not pass a ThrowIfV1Schema value.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample5.cs)]

<span data-ttu-id="5e982-147">Otevřete IdentityConfig.cs a změňte třídu **ApplicationUserManger** tak, aby používala novou třídu úložiště uživatele pro trvalá data a **int** pro klíč.</span><span class="sxs-lookup"><span data-stu-id="5e982-147">Open IdentityConfig.cs, and change the **ApplicationUserManger** class to use your new user store class for persisting data and an **int** for the key.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample6.cs?highlight=1,3,12,14,32,37,48)]

<span data-ttu-id="5e982-148">V šabloně Update 3 je třeba změnit třídu ApplicationSignInManager.</span><span class="sxs-lookup"><span data-stu-id="5e982-148">In the Update 3 template, you must change the ApplicationSignInManager class.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample7.cs?highlight=1)]

<a id="startup"></a>
## <a name="change-start-up-configuration-to-use-the-key-type"></a><span data-ttu-id="5e982-149">Změna spouštěcí konfigurace tak, aby používala typ klíče</span><span class="sxs-lookup"><span data-stu-id="5e982-149">Change start-up configuration to use the key type</span></span>

<span data-ttu-id="5e982-150">V Startup.Auth.cs nahraďte kód OnValidateIdentity, jak je zvýrazněno níže.</span><span class="sxs-lookup"><span data-stu-id="5e982-150">In Startup.Auth.cs, replace the OnValidateIdentity code, as highlighted below.</span></span> <span data-ttu-id="5e982-151">Všimněte si, že definice getUserIdCallback analyzuje řetězcovou hodnotu na celé číslo.</span><span class="sxs-lookup"><span data-stu-id="5e982-151">Notice that the getUserIdCallback definition, parses the string value into an integer.</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample8.cs?highlight=7-12)]

<span data-ttu-id="5e982-152">Pokud váš projekt nerozpozná obecnou implementaci metody **GetUserID** , budete možná muset aktualizovat balíček NuGet ASP.NET identity na verzi 2,1.</span><span class="sxs-lookup"><span data-stu-id="5e982-152">If your project does not recognize the generic implementation of the **GetUserId** method, you may need to update the ASP.NET Identity NuGet package to version 2.1</span></span>

<span data-ttu-id="5e982-153">Vytvořili jste spoustu změn tříd infrastruktury, které používá ASP.NET Identity.</span><span class="sxs-lookup"><span data-stu-id="5e982-153">You have made a lot of changes to the infrastructure classes used by ASP.NET Identity.</span></span> <span data-ttu-id="5e982-154">Pokud se pokusíte zkompilovat projekt, všimnete si velkého množství chyb.</span><span class="sxs-lookup"><span data-stu-id="5e982-154">If you try compiling the project, you will notice a lot of errors.</span></span> <span data-ttu-id="5e982-155">Naštěstí jsou všechny zbývající chyby podobné.</span><span class="sxs-lookup"><span data-stu-id="5e982-155">Fortunately, the remaining errors are all similar.</span></span> <span data-ttu-id="5e982-156">Třída identity očekává pro klíč celé číslo, ale kontroler (nebo webový formulář) předává řetězcovou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="5e982-156">The Identity class expects an integer for the key, but the controller (or Web Form) is passing a string value.</span></span> <span data-ttu-id="5e982-157">V každém případě je nutné převést řetězec na celé číslo a voláním metody **GetUserID&lt;int&gt;** .</span><span class="sxs-lookup"><span data-stu-id="5e982-157">In each case, you need to convert from a string to and integer by calling **GetUserId&lt;int&gt;**.</span></span> <span data-ttu-id="5e982-158">Můžete buď pracovat se seznamem chyb z kompilace, nebo provést následující změny.</span><span class="sxs-lookup"><span data-stu-id="5e982-158">You can either work through the error list from compilation or follow the changes below.</span></span>

<span data-ttu-id="5e982-159">Zbývající změny závisí na typu vytvářeného projektu a na aktualizaci, kterou jste nainstalovali v aplikaci Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5e982-159">The remaining changes depend on the type of project you are creating and which update you have installed in Visual Studio.</span></span> <span data-ttu-id="5e982-160">Pomocí následujících odkazů můžete přejít přímo k příslušné části</span><span class="sxs-lookup"><span data-stu-id="5e982-160">You can go directly to the relevant section through the following links</span></span>

- [<span data-ttu-id="5e982-161">V případě MVC s aktualizací Update 2 změňte AccountController tak, aby předával typ klíče.</span><span class="sxs-lookup"><span data-stu-id="5e982-161">For MVC with Update 2, change the AccountController to pass the key type</span></span>](#mvcupdate2)
- [<span data-ttu-id="5e982-162">Pro MVC s aktualizací Update 3 změňte AccountController a ManageController, aby se předal typ klíče.</span><span class="sxs-lookup"><span data-stu-id="5e982-162">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>](#mvcupdate3)
- [<span data-ttu-id="5e982-163">U webových formulářů s aktualizací Update 2 změňte stránky účtu, aby předávaly typ klíče.</span><span class="sxs-lookup"><span data-stu-id="5e982-163">For Web Forms with Update 2, change Account pages to pass the key type</span></span>](#webformsupdate2)
- [<span data-ttu-id="5e982-164">U webových formulářů s aktualizací Update 3 změňte stránky účtu, aby předávaly typ klíče.</span><span class="sxs-lookup"><span data-stu-id="5e982-164">For Web Forms with Update 3, change Account pages to pass the key type</span></span>](#webformsupdate3)

<a id="mvcupdate2"></a>
## <a name="for-mvc-with-update-2-change-the-accountcontroller-to-pass-the-key-type"></a><span data-ttu-id="5e982-165">V případě MVC s aktualizací Update 2 změňte AccountController tak, aby předával typ klíče.</span><span class="sxs-lookup"><span data-stu-id="5e982-165">For MVC with Update 2, change the AccountController to pass the key type</span></span>

<span data-ttu-id="5e982-166">Otevřete soubor AccountController.cs.</span><span class="sxs-lookup"><span data-stu-id="5e982-166">Open the AccountController.cs file.</span></span> <span data-ttu-id="5e982-167">Je potřeba změnit následující metody.</span><span class="sxs-lookup"><span data-stu-id="5e982-167">You need to change the following methods.</span></span>

<span data-ttu-id="5e982-168">Metoda **ConfirmEmail**</span><span class="sxs-lookup"><span data-stu-id="5e982-168">**ConfirmEmail** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample9.cs?highlight=1,3)]

<span data-ttu-id="5e982-169">**Zrušit přidružení** metody</span><span class="sxs-lookup"><span data-stu-id="5e982-169">**Disassociate** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample10.cs?highlight=5,9)]

<span data-ttu-id="5e982-170">**Manage (ManageUserViewModel)** – metoda</span><span class="sxs-lookup"><span data-stu-id="5e982-170">**Manage(ManageUserViewModel)** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample11.cs?highlight=11,17,41)]

<span data-ttu-id="5e982-171">Metoda **LinkLoginCallback**</span><span class="sxs-lookup"><span data-stu-id="5e982-171">**LinkLoginCallback** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample12.cs?highlight=10)]

<span data-ttu-id="5e982-172">Metoda **RemoveAccountList**</span><span class="sxs-lookup"><span data-stu-id="5e982-172">**RemoveAccountList** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample13.cs?highlight=3)]

<span data-ttu-id="5e982-173">Metoda **HasPassword**</span><span class="sxs-lookup"><span data-stu-id="5e982-173">**HasPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample14.cs?highlight=3)]

<span data-ttu-id="5e982-174">Nyní můžete [Spustit aplikaci](#run) a zaregistrovat nového uživatele.</span><span class="sxs-lookup"><span data-stu-id="5e982-174">You can now [run the application](#run) and register a new user.</span></span>

<a id="mvcupdate3"></a>
## <a name="for-mvc-with-update-3-change-the-accountcontroller-and-managecontroller-to-pass-the-key-type"></a><span data-ttu-id="5e982-175">Pro MVC s aktualizací Update 3 změňte AccountController a ManageController, aby se předal typ klíče.</span><span class="sxs-lookup"><span data-stu-id="5e982-175">For MVC with Update 3, change the AccountController and ManageController to pass the key type</span></span>

<span data-ttu-id="5e982-176">Otevřete soubor AccountController.cs.</span><span class="sxs-lookup"><span data-stu-id="5e982-176">Open the AccountController.cs file.</span></span> <span data-ttu-id="5e982-177">Je třeba změnit následující metodu.</span><span class="sxs-lookup"><span data-stu-id="5e982-177">You need to change the following method.</span></span>

<span data-ttu-id="5e982-178">Metoda **ConfirmEmail**</span><span class="sxs-lookup"><span data-stu-id="5e982-178">**ConfirmEmail** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample15.cs?highlight=1,3)]

<span data-ttu-id="5e982-179">Metoda **SendCode**</span><span class="sxs-lookup"><span data-stu-id="5e982-179">**SendCode** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample16.cs?highlight=4)]

<span data-ttu-id="5e982-180">Otevřete soubor ManageController.cs.</span><span class="sxs-lookup"><span data-stu-id="5e982-180">Open the ManageController.cs file.</span></span> <span data-ttu-id="5e982-181">Je potřeba změnit následující metody.</span><span class="sxs-lookup"><span data-stu-id="5e982-181">You need to change the following methods.</span></span>

<span data-ttu-id="5e982-182">**Index** – metoda</span><span class="sxs-lookup"><span data-stu-id="5e982-182">**Index** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample17.cs?highlight=15-17)]

<span data-ttu-id="5e982-183">Metody **RemoveLogin**</span><span class="sxs-lookup"><span data-stu-id="5e982-183">**RemoveLogin** methods</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample18.cs?highlight=3,13,17)]

<span data-ttu-id="5e982-184">Metoda **AddPhoneNumber**</span><span class="sxs-lookup"><span data-stu-id="5e982-184">**AddPhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample19.cs?highlight=9)]

<span data-ttu-id="5e982-185">Metoda **EnableTwoFactorAuthentication**</span><span class="sxs-lookup"><span data-stu-id="5e982-185">**EnableTwoFactorAuthentication** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample20.cs?highlight=3-4)]

<span data-ttu-id="5e982-186">Metoda **DisableTwoFactorAuthentication**</span><span class="sxs-lookup"><span data-stu-id="5e982-186">**DisableTwoFactorAuthentication** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample21.cs?highlight=3-4)]

<span data-ttu-id="5e982-187">Metody **VerifyPhoneNumber**</span><span class="sxs-lookup"><span data-stu-id="5e982-187">**VerifyPhoneNumber** methods</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample22.cs?highlight=4,18,21)]

<span data-ttu-id="5e982-188">Metoda **RemovePhoneNumber**</span><span class="sxs-lookup"><span data-stu-id="5e982-188">**RemovePhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample23.cs?highlight=3,8)]

<span data-ttu-id="5e982-189">**ChangePassword** – metoda</span><span class="sxs-lookup"><span data-stu-id="5e982-189">**ChangePassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample24.cs?highlight=10,13)]

<span data-ttu-id="5e982-190">Metoda **SetPassword**</span><span class="sxs-lookup"><span data-stu-id="5e982-190">**SetPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample25.cs?highlight=5,8)]

<span data-ttu-id="5e982-191">Metoda **ManageLogins**</span><span class="sxs-lookup"><span data-stu-id="5e982-191">**ManageLogins** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample26.cs?highlight=7,12)]

<span data-ttu-id="5e982-192">Metoda **LinkLoginCallback**</span><span class="sxs-lookup"><span data-stu-id="5e982-192">**LinkLoginCallback** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample27.cs?highlight=8)]

<span data-ttu-id="5e982-193">Metoda **HasPassword**</span><span class="sxs-lookup"><span data-stu-id="5e982-193">**HasPassword** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample28.cs?highlight=3)]

<span data-ttu-id="5e982-194">Metoda **HasPhoneNumber**</span><span class="sxs-lookup"><span data-stu-id="5e982-194">**HasPhoneNumber** method</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample29.cs?highlight=3)]

<span data-ttu-id="5e982-195">Nyní můžete [Spustit aplikaci](#run) a zaregistrovat nového uživatele.</span><span class="sxs-lookup"><span data-stu-id="5e982-195">You can now [run the application](#run) and register a new user.</span></span>

<a id="webformsupdate2"></a>
## <a name="for-web-forms-with-update-2-change-account-pages-to-pass-the-key-type"></a><span data-ttu-id="5e982-196">U webových formulářů s aktualizací Update 2 změňte stránky účtu, aby předávaly typ klíče.</span><span class="sxs-lookup"><span data-stu-id="5e982-196">For Web Forms with Update 2, change Account pages to pass the key type</span></span>

<span data-ttu-id="5e982-197">U webových formulářů s aktualizací Update 2 je třeba změnit následující stránky.</span><span class="sxs-lookup"><span data-stu-id="5e982-197">For Web Forms with Update 2, you need to change the following pages.</span></span>

<span data-ttu-id="5e982-198">**Confirm.aspx.cx**</span><span class="sxs-lookup"><span data-stu-id="5e982-198">**Confirm.aspx.cx**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample30.cs?highlight=8)]

<span data-ttu-id="5e982-199">**RegisterExternalLogin.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="5e982-199">**RegisterExternalLogin.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample31.cs?highlight=36)]

<span data-ttu-id="5e982-200">**Manage.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="5e982-200">**Manage.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample32.cs?highlight=3,22,47,52,69,85,93,98)]

<span data-ttu-id="5e982-201">Nyní můžete [Spustit aplikaci](#run) a zaregistrovat nového uživatele.</span><span class="sxs-lookup"><span data-stu-id="5e982-201">You can now [run the application](#run) and register a new user.</span></span>

<a id="webformsupdate3"></a>
## <a name="for-web-forms-with-update-3-change-account-pages-to-pass-the-key-type"></a><span data-ttu-id="5e982-202">U webových formulářů s aktualizací Update 3 změňte stránky účtu, aby předávaly typ klíče.</span><span class="sxs-lookup"><span data-stu-id="5e982-202">For Web Forms with Update 3, change Account pages to pass the key type</span></span>

<span data-ttu-id="5e982-203">U webových formulářů s aktualizací Update 3 je třeba změnit následující stránky.</span><span class="sxs-lookup"><span data-stu-id="5e982-203">For Web Forms with Update 3, you need to change the following pages.</span></span>

<span data-ttu-id="5e982-204">**Confirm.aspx.cx**</span><span class="sxs-lookup"><span data-stu-id="5e982-204">**Confirm.aspx.cx**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample33.cs?highlight=8)]

<span data-ttu-id="5e982-205">**RegisterExternalLogin.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="5e982-205">**RegisterExternalLogin.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample34.cs?highlight=36)]

<span data-ttu-id="5e982-206">**Manage.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="5e982-206">**Manage.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample35.cs?highlight=11,27,32,34,82,87,99,108)]

<span data-ttu-id="5e982-207">**VerifyPhoneNumber.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="5e982-207">**VerifyPhoneNumber.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample36.cs?highlight=8,23,27)]

<span data-ttu-id="5e982-208">**AddPhoneNumber.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="5e982-208">**AddPhoneNumber.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample37.cs?highlight=7)]

<span data-ttu-id="5e982-209">**ManagePassword.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="5e982-209">**ManagePassword.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample38.cs?highlight=11,47,50,68)]

<span data-ttu-id="5e982-210">**ManageLogins.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="5e982-210">**ManageLogins.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample39.cs?highlight=16,23,32,41,45)]

<span data-ttu-id="5e982-211">**TwoFactorAuthenticationSignIn.aspx.cs**</span><span class="sxs-lookup"><span data-stu-id="5e982-211">**TwoFactorAuthenticationSignIn.aspx.cs**</span></span>

[!code-csharp[Main](change-primary-key-for-users-in-aspnet-identity/samples/sample40.cs?highlight=14-15,29,53)]

<a id="run"></a>
## <a name="run-application"></a><span data-ttu-id="5e982-212">Spustit aplikaci</span><span class="sxs-lookup"><span data-stu-id="5e982-212">Run application</span></span>

<span data-ttu-id="5e982-213">Dokončili jste všechny požadované změny v šabloně výchozí webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="5e982-213">You have finished all of the required changes to the default Web Application template.</span></span> <span data-ttu-id="5e982-214">Spusťte aplikaci a zaregistrujte nového uživatele.</span><span class="sxs-lookup"><span data-stu-id="5e982-214">Run the application and register a new user.</span></span> <span data-ttu-id="5e982-215">Po registraci uživatele si všimněte, že tabulka AspNetUsers má sloupec ID, který je celé číslo.</span><span class="sxs-lookup"><span data-stu-id="5e982-215">After registering the user, you will notice that the AspNetUsers table has an Id column that is an integer.</span></span>

![nový primární klíč](change-primary-key-for-users-in-aspnet-identity/_static/image1.png)

<span data-ttu-id="5e982-217">Pokud jste již dříve vytvořili ASP.NET Identity tabulky s jiným primárním klíčem, je nutné provést další změny.</span><span class="sxs-lookup"><span data-stu-id="5e982-217">If you have previously created the ASP.NET Identity tables with a different primary key, you need to make some additional changes.</span></span> <span data-ttu-id="5e982-218">Pokud je to možné, stačí odstranit stávající databázi.</span><span class="sxs-lookup"><span data-stu-id="5e982-218">If possible, just delete the existing database.</span></span> <span data-ttu-id="5e982-219">Databáze bude znovu vytvořena se správným návrhem při spuštění webové aplikace a přidání nového uživatele.</span><span class="sxs-lookup"><span data-stu-id="5e982-219">The database will be re-created with the correct design when you run the web application and add a new user.</span></span> <span data-ttu-id="5e982-220">Pokud není možné odstranit, spusťte migraci Code First pro změnu tabulek.</span><span class="sxs-lookup"><span data-stu-id="5e982-220">If deletion is not possible, run code first migrations to change the tables.</span></span> <span data-ttu-id="5e982-221">Nový celočíselný primární klíč ale nebude nastaven jako vlastnost IDENTITY SQL v databázi.</span><span class="sxs-lookup"><span data-stu-id="5e982-221">However, the new integer primary key will not be set up as a SQL IDENTITY property in the database.</span></span> <span data-ttu-id="5e982-222">Sloupec ID je nutné ručně nastavit jako IDENTITU.</span><span class="sxs-lookup"><span data-stu-id="5e982-222">You must manually set the Id column as an IDENTITY.</span></span>

<a id="other"></a>
## <a name="other-resources"></a><span data-ttu-id="5e982-223">Další zdroje</span><span class="sxs-lookup"><span data-stu-id="5e982-223">Other resources</span></span>

- [<span data-ttu-id="5e982-224">Přehled poskytovatelů vlastního úložiště pro ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="5e982-224">Overview of Custom Storage Providers for ASP.NET Identity</span></span>](overview-of-custom-storage-providers-for-aspnet-identity.md)
- [<span data-ttu-id="5e982-225">Migrace stávajícího webu z členství SQL na ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="5e982-225">Migrating an Existing Website from SQL Membership to ASP.NET Identity</span></span>](../migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md)
- [<span data-ttu-id="5e982-226">Migrace dat Universal Provider pro členství a profily uživatelů do ASP.NET Identity</span><span class="sxs-lookup"><span data-stu-id="5e982-226">Migrating Universal Provider Data for Membership and User Profiles to ASP.NET Identity</span></span>](../migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity.md)
- <span data-ttu-id="5e982-227">[Ukázková aplikace](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK) se změněným primárním klíčem</span><span class="sxs-lookup"><span data-stu-id="5e982-227">[Sample application](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/ChangePK) with changed primary key</span></span>

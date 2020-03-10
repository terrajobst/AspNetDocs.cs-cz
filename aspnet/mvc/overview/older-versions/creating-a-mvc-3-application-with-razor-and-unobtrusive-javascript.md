---
uid: mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
title: Vytvoření aplikace MVC 3 se syntaxí Razor a nenápadem JavaScriptu | Microsoft Docs
author: microsoft
description: Ukázková webová aplikace v seznamu uživatelů ukazuje, jak jednoduché je vytvořit ASP.NET aplikace MVC 3 pomocí zobrazovacího modulu Razor. Ukázková aplikace s...
ms.author: riande
ms.date: 11/01/2010
ms.assetid: 658b149b-d770-46bf-8b4b-4e47cca242f3
msc.legacyurl: /mvc/overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript
msc.type: authoredcontent
ms.openlocfilehash: fb63493ff22c9261fc5746a998a32f2511141f87
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540983"
---
# <a name="creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript"></a><span data-ttu-id="7e15d-104">Vytvoření aplikace MVC 3 se syntaxí Razor a nerušivým JavaScriptem</span><span class="sxs-lookup"><span data-stu-id="7e15d-104">Creating a MVC 3 Application with Razor and Unobtrusive JavaScript</span></span>

<span data-ttu-id="7e15d-105">od [Microsoftu](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="7e15d-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="7e15d-106">Ukázková webová aplikace v seznamu uživatelů ukazuje, jak jednoduché je vytvořit ASP.NET aplikace MVC 3 pomocí zobrazovacího modulu Razor.</span><span class="sxs-lookup"><span data-stu-id="7e15d-106">The User List sample web application demonstrates how simple it is to create ASP.NET MVC 3 applications using the Razor view engine.</span></span> <span data-ttu-id="7e15d-107">Ukázková aplikace ukazuje, jak používat nový modul zobrazení Razor s ASP.NET MVC verze 3 a Visual Studio 2010 k vytvoření webu seznam fiktivního uživatele, který obsahuje funkce, jako je vytváření, zobrazování, úpravy a odstraňování uživatelů.</span><span class="sxs-lookup"><span data-stu-id="7e15d-107">The sample application shows how to use the new Razor view engine with ASP.NET MVC version 3 and Visual Studio 2010 to create a fictional User List website that includes functionality such as creating, displaying, editing, and deleting users.</span></span>
> 
> <span data-ttu-id="7e15d-108">Tento kurz popisuje kroky, které byly provedeny při sestavování ukázkového seznamu uživatelů aplikace ASP.NET MVC 3.</span><span class="sxs-lookup"><span data-stu-id="7e15d-108">This tutorial describes the steps that were taken in order to build the User List sample ASP.NET MVC 3 application.</span></span> <span data-ttu-id="7e15d-109">Projekt sady Visual Studio s C# a zdrojový kód VB je k dispozici pro toto téma: [stažení](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span><span class="sxs-lookup"><span data-stu-id="7e15d-109">A Visual Studio project with C# and VB source code is available to accompany this topic: [Download](https://code.msdn.microsoft.com/aspnetmvcsamples/Release/ProjectReleases.aspx?ReleaseId=5114).</span></span> <span data-ttu-id="7e15d-110">Pokud máte dotazy k tomuto kurzu, publikujte je prosím na [fóru MVC](https://forums.asp.net/1146.aspx).</span><span class="sxs-lookup"><span data-stu-id="7e15d-110">If you have questions about this tutorial, please post them to the [MVC forum](https://forums.asp.net/1146.aspx).</span></span>

## <a name="overview"></a><span data-ttu-id="7e15d-111">Přehled</span><span class="sxs-lookup"><span data-stu-id="7e15d-111">Overview</span></span>

<span data-ttu-id="7e15d-112">Aplikace, kterou budete sestavovat, je jednoduchý Web seznam uživatelů.</span><span class="sxs-lookup"><span data-stu-id="7e15d-112">The application you'll be building is a simple user list website.</span></span> <span data-ttu-id="7e15d-113">Uživatelé mohou zadat, zobrazit a aktualizovat informace o uživateli.</span><span class="sxs-lookup"><span data-stu-id="7e15d-113">Users can enter, view, and update user information.</span></span>

![Ukázkový web](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image1.png)

<span data-ttu-id="7e15d-115">Zde si můžete stáhnout VB a C# dokončený [](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f)projekt.</span><span class="sxs-lookup"><span data-stu-id="7e15d-115">You can download the VB and C# completed project [here](https://code.msdn.microsoft.com/Creating-a-MVC-3-28883c0f).</span></span>

## <a name="creating-the-web-application"></a><span data-ttu-id="7e15d-116">Vytvoření webové aplikace</span><span class="sxs-lookup"><span data-stu-id="7e15d-116">Creating the Web Application</span></span>

<span data-ttu-id="7e15d-117">Chcete-li spustit kurz, otevřete Visual Studio 2010 a vytvořte nový projekt pomocí šablony *webové aplikace ASP.NET MVC 3* .</span><span class="sxs-lookup"><span data-stu-id="7e15d-117">To start the tutorial, open Visual Studio 2010 and create a new project using the *ASP.NET MVC 3 Web Application* template.</span></span> <span data-ttu-id="7e15d-118">Pojmenujte aplikaci &quot;Mvc3Razor&quot;.</span><span class="sxs-lookup"><span data-stu-id="7e15d-118">Name the application &quot;Mvc3Razor&quot;.</span></span>

<span data-ttu-id="7e15d-119">[![nový projekt MVC 3](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="7e15d-119">[![New MVC 3 project](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image3.png)](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image2.png)</span></span>

<span data-ttu-id="7e15d-120">V dialogovém okně **Nový projekt ASP.NET MVC 3** vyberte možnost **Internet aplikace**, vyberte modul zobrazení Razor a pak klikněte na tlačítko **OK**.</span><span class="sxs-lookup"><span data-stu-id="7e15d-120">In the **New ASP.NET MVC 3 Project** dialog, select **Internet Application**, select the Razor view engine, and then click **OK**.</span></span>

![Nový projekt ASP.NET MVC 3 – dialog](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image4.png)

<span data-ttu-id="7e15d-122">V tomto kurzu nebudete používat poskytovatele členství ASP.NET, takže můžete odstranit všechny soubory spojené s přihlášením a členstvím.</span><span class="sxs-lookup"><span data-stu-id="7e15d-122">In this tutorial you will not be using the ASP.NET membership provider, so you can delete all the files associated with logon and membership.</span></span> <span data-ttu-id="7e15d-123">V **Průzkumník řešení**odeberte následující soubory a adresáře:</span><span class="sxs-lookup"><span data-stu-id="7e15d-123">In **Solution Explorer**, remove the following files and directories:</span></span>

- <span data-ttu-id="7e15d-124">*Controllers\AccountController*</span><span class="sxs-lookup"><span data-stu-id="7e15d-124">*Controllers\AccountController*</span></span>
- <span data-ttu-id="7e15d-125">*Models\AccountModels*</span><span class="sxs-lookup"><span data-stu-id="7e15d-125">*Models\AccountModels*</span></span>
- <span data-ttu-id="7e15d-126">*Views\Shared\\_LogOnPartial*</span><span class="sxs-lookup"><span data-stu-id="7e15d-126">*Views\Shared\\_LogOnPartial*</span></span>
- <span data-ttu-id="7e15d-127">*Views\Account* (a všechny soubory v tomto adresáři)</span><span class="sxs-lookup"><span data-stu-id="7e15d-127">*Views\Account* (and all the files in this directory)</span></span>

![Soln exp](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image5.png)

<span data-ttu-id="7e15d-129">Upravte soubor <em>\_layout. cshtml</em> a nahraďte kód uvnitř elementu `<div>` s názvem `logindisplay` zprávou <em>&quot;</em>přihlášení je zakázané&quot;.</span><span class="sxs-lookup"><span data-stu-id="7e15d-129">Edit the <em>\_Layout.cshtml</em> file and replace the markup inside the `<div>` element named `logindisplay` with the message <em>&quot;</em>Login Disabled&quot;.</span></span> <span data-ttu-id="7e15d-130">Následující příklad ukazuje nový kód:</span><span class="sxs-lookup"><span data-stu-id="7e15d-130">The following example shows the new markup:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample1.cshtml)]

## <a name="adding-the-model"></a><span data-ttu-id="7e15d-131">Přidání modelu</span><span class="sxs-lookup"><span data-stu-id="7e15d-131">Adding the Model</span></span>

<span data-ttu-id="7e15d-132">V **Průzkumník řešení**klikněte pravým tlačítkem na složku *modely* , vyberte **Přidat**a potom klikněte na **Třída**.</span><span class="sxs-lookup"><span data-stu-id="7e15d-132">In **Solution Explorer**, right-click the *Models* folder, select **Add**, and then click **Class**.</span></span>

![Nová třída uživatelského MDL](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image6.png)

<span data-ttu-id="7e15d-134">Pojmenujte `UserModel`třídy.</span><span class="sxs-lookup"><span data-stu-id="7e15d-134">Name the class `UserModel`.</span></span> <span data-ttu-id="7e15d-135">Obsah souboru *UserModel* nahraďte následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="7e15d-135">Replace the contents of the *UserModel* file with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample2.cs)]

<span data-ttu-id="7e15d-136">Třída `UserModel` představuje uživatele.</span><span class="sxs-lookup"><span data-stu-id="7e15d-136">The `UserModel` class represents users.</span></span> <span data-ttu-id="7e15d-137">Každý člen třídy je opatřen poznámkou s [požadovaným](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) atributem z oboru názvů [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) .</span><span class="sxs-lookup"><span data-stu-id="7e15d-137">Each member of the class is annotated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute from the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace.</span></span> <span data-ttu-id="7e15d-138">Atributy v oboru názvů [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) poskytují automatické ověřování na straně klienta a serveru pro webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="7e15d-138">The attributes in the [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) namespace provide automatic client- and server-side validation for web applications.</span></span>

<span data-ttu-id="7e15d-139">Otevřete třídu `HomeController` a přidejte direktivu `using`, abyste mohli přistupovat ke třídám `UserModel` a `Users`:</span><span class="sxs-lookup"><span data-stu-id="7e15d-139">Open the `HomeController` class and add a `using` directive so that you can access the `UserModel` and `Users` classes:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample3.cs)]

<span data-ttu-id="7e15d-140">Hned za `HomeController` deklarací přidejte následující komentář a odkaz na `Users` třídu:</span><span class="sxs-lookup"><span data-stu-id="7e15d-140">Just after the `HomeController` declaration, add the following comment and the reference to a `Users` class:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample4.cs)]

<span data-ttu-id="7e15d-141">Třída `Users` je zjednodušené úložiště dat v paměti, které použijete v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="7e15d-141">The `Users` class is a simplified, in-memory data store that you'll use in this tutorial.</span></span> <span data-ttu-id="7e15d-142">V reálné aplikaci byste použili databázi k ukládání informací o uživateli.</span><span class="sxs-lookup"><span data-stu-id="7e15d-142">In a real application you would use a database to store user information.</span></span> <span data-ttu-id="7e15d-143">V následujícím příkladu se zobrazuje několik prvních řádků `HomeController` souboru:</span><span class="sxs-lookup"><span data-stu-id="7e15d-143">The first few lines of the `HomeController` file are shown in the following example:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample5.cs)]

<span data-ttu-id="7e15d-144">Sestavte aplikaci tak, aby byl uživatelský model k dispozici průvodci generováním uživatelského rozhraní v dalším kroku.</span><span class="sxs-lookup"><span data-stu-id="7e15d-144">Build the application so that the user model will be available to the scaffolding wizard in the next step.</span></span>

## <a name="creating-the-default-view"></a><span data-ttu-id="7e15d-145">Vytváření výchozího zobrazení</span><span class="sxs-lookup"><span data-stu-id="7e15d-145">Creating the Default View</span></span>

<span data-ttu-id="7e15d-146">Dalším krokem je přidání metody akce a zobrazení pro zobrazení uživatelů.</span><span class="sxs-lookup"><span data-stu-id="7e15d-146">The next step is to add an action method and view to display the users.</span></span>

<span data-ttu-id="7e15d-147">Odstraňte existující soubor *Views\Home\Index* .</span><span class="sxs-lookup"><span data-stu-id="7e15d-147">Delete the existing *Views\Home\Index* file.</span></span> <span data-ttu-id="7e15d-148">Vytvoří se nový soubor *indexu* pro zobrazení uživatelů.</span><span class="sxs-lookup"><span data-stu-id="7e15d-148">You will create a new *Index* file to display the users.</span></span>

<span data-ttu-id="7e15d-149">Ve třídě `HomeController` nahraďte obsah metody `Index` následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="7e15d-149">In the `HomeController` class, replace the contents of the `Index` method with the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample6.cs)]

<span data-ttu-id="7e15d-150">Klikněte pravým tlačítkem myši do metody `Index` a potom klikněte na tlačítko **Přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="7e15d-150">Right-click inside the `Index` method and then click **Add View**.</span></span>

![Přidat zobrazení](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image7.png)

<span data-ttu-id="7e15d-152">Vyberte možnost **vytvořit zobrazení silného typu** .</span><span class="sxs-lookup"><span data-stu-id="7e15d-152">Select the **Create a strongly-typed view** option.</span></span> <span data-ttu-id="7e15d-153">V **zobrazení třída dat**vyberte **Mvc3Razor. Models. UserModel**.</span><span class="sxs-lookup"><span data-stu-id="7e15d-153">For **View data class**, select **Mvc3Razor.Models.UserModel**.</span></span> <span data-ttu-id="7e15d-154">(Pokud nevidíte **Mvc3Razor. Models. UserModel** v poli **Zobrazit data třídy** , je nutné sestavit projekt.) Ujistěte se, že je modul zobrazení nastavený na **Razor**.</span><span class="sxs-lookup"><span data-stu-id="7e15d-154">(If you don't see **Mvc3Razor.Models.UserModel** in the **View data class** box, you need to build the project.) Make sure that the view engine is set to **Razor**.</span></span> <span data-ttu-id="7e15d-155">Nastavte **Zobrazit obsah** na **seznam** a pak klikněte na **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="7e15d-155">Set **View content** to **List** and then click **Add**.</span></span>

![Přidat zobrazení indexu](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image8.png)

<span data-ttu-id="7e15d-157">Nové zobrazení automaticky generuje uživatelská data, která jsou předána do zobrazení `Index`.</span><span class="sxs-lookup"><span data-stu-id="7e15d-157">The new view automatically scaffolds the user data that's passed to the `Index` view.</span></span> <span data-ttu-id="7e15d-158">Prověřte nově vygenerovaný soubor *Views\Home\Index* .</span><span class="sxs-lookup"><span data-stu-id="7e15d-158">Examine the newly generated *Views\Home\Index* file.</span></span> <span data-ttu-id="7e15d-159">Odkazy **vytvořit nové**, **Upravit**, **Podrobnosti**a **Odstranit** nefungují, ale zbytek stránky je funkční.</span><span class="sxs-lookup"><span data-stu-id="7e15d-159">The **Create New**, **Edit**, **Details**, and **Delete** links don't work, but the rest of the page is functional.</span></span> <span data-ttu-id="7e15d-160">Spusťte stránku.</span><span class="sxs-lookup"><span data-stu-id="7e15d-160">Run the page.</span></span> <span data-ttu-id="7e15d-161">Zobrazí se seznam uživatelů.</span><span class="sxs-lookup"><span data-stu-id="7e15d-161">You see a list of users.</span></span>

![Stránka indexu](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image9.png)

<span data-ttu-id="7e15d-163">Otevřete soubor *index. cshtml* a nahraďte `ActionLink` kód pro **Úpravy**, **Podrobnosti**a **odstranění** pomocí následujícího kódu:</span><span class="sxs-lookup"><span data-stu-id="7e15d-163">Open the *Index.cshtml* file and replace the `ActionLink` markup for **Edit**, **Details**, and **Delete** with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample7.cshtml)]

<span data-ttu-id="7e15d-164">Uživatelské jméno se používá jako ID k vyhledání vybraného záznamu v odkazech **Upravit**, **Podrobnosti**a **Odstranit** .</span><span class="sxs-lookup"><span data-stu-id="7e15d-164">The user name is used as the ID to find the selected record in the **Edit**, **Details**, and **Delete** links.</span></span>

## <a name="creating-the-details-view"></a><span data-ttu-id="7e15d-165">Vytváření zobrazení podrobností</span><span class="sxs-lookup"><span data-stu-id="7e15d-165">Creating the Details View</span></span>

<span data-ttu-id="7e15d-166">Dalším krokem je přidání metody a zobrazení akce `Details`, aby se zobrazily podrobnosti o uživateli.</span><span class="sxs-lookup"><span data-stu-id="7e15d-166">The next step is to add a `Details` action method and view in order to display user details.</span></span>

![Podrobnosti](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image10.png)

<span data-ttu-id="7e15d-168">Do domovského kontroleru přidejte následující metodu `Details`:</span><span class="sxs-lookup"><span data-stu-id="7e15d-168">Add the following `Details` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample8.cs)]

<span data-ttu-id="7e15d-169">Klikněte pravým tlačítkem myši do metody `Details` a pak vyberte <strong>Přidat zobrazení</strong>.</span><span class="sxs-lookup"><span data-stu-id="7e15d-169">Right-click inside the `Details` method and then select <strong>Add View</strong>.</span></span> <span data-ttu-id="7e15d-170">Ověřte, že pole <strong>Třída zobrazení dat</strong> obsahuje <strong>Mvc3Razor. Models. UserModel</strong><em>.</em></span><span class="sxs-lookup"><span data-stu-id="7e15d-170">Verify that the <strong>View data class</strong> box contains <strong>Mvc3Razor.Models.UserModel</strong><em>.</em></span></span> <span data-ttu-id="7e15d-171">Nastavte <strong>zobrazení obsahu</strong> na <strong>Podrobnosti</strong> a potom klikněte na tlačítko <strong>Přidat</strong>.</span><span class="sxs-lookup"><span data-stu-id="7e15d-171">Set <strong>View content</strong> to <strong>Details</strong> and then click <strong>Add</strong>.</span></span>

![Přidat zobrazení podrobností](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image11.png)

<span data-ttu-id="7e15d-173">Spusťte aplikaci a vyberte odkaz Podrobnosti.</span><span class="sxs-lookup"><span data-stu-id="7e15d-173">Run the application and select a details link.</span></span> <span data-ttu-id="7e15d-174">Automatické generování uživatelského rozhraní zobrazuje každou vlastnost v modelu.</span><span class="sxs-lookup"><span data-stu-id="7e15d-174">The automatic scaffolding shows each property in the model.</span></span>

![Podrobnosti](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image12.png)

## <a name="creating-the-edit-view"></a><span data-ttu-id="7e15d-176">Vytvoření zobrazení pro úpravy</span><span class="sxs-lookup"><span data-stu-id="7e15d-176">Creating the Edit View</span></span>

<span data-ttu-id="7e15d-177">Do domovského kontroleru přidejte následující metodu `Edit`.</span><span class="sxs-lookup"><span data-stu-id="7e15d-177">Add the following `Edit` method to the home controller.</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample9.cs)]

<span data-ttu-id="7e15d-178">Přidejte zobrazení jako v předchozích krocích, ale nastavte **Zobrazit obsah** , který chcete **Upravit**.</span><span class="sxs-lookup"><span data-stu-id="7e15d-178">Add a view as in the previous steps, but set **View content** to **Edit**.</span></span>

![Přidat zobrazení pro úpravy](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image13.png)

<span data-ttu-id="7e15d-180">Spusťte aplikaci a upravte křestní jméno a příjmení jednoho z uživatelů.</span><span class="sxs-lookup"><span data-stu-id="7e15d-180">Run the application and edit the first and last name of one of the users.</span></span> <span data-ttu-id="7e15d-181">Pokud jste porušili jakákoli omezení `DataAnnotation`, která byla použita na třídu `UserModel`, při odeslání formuláře se zobrazí chyby ověřování, které jsou vytvářeny kódem serveru.</span><span class="sxs-lookup"><span data-stu-id="7e15d-181">If you violate any `DataAnnotation` constraints that have been applied to the `UserModel` class, when you submit the form, you will see validation errors that are produced by server code.</span></span> <span data-ttu-id="7e15d-182">Pokud například změníte křestní jméno &quot;Ann&quot; na &quot;&quot;, ve formuláři se zobrazí následující chyba:</span><span class="sxs-lookup"><span data-stu-id="7e15d-182">For example, if you change the first name &quot;Ann&quot; to &quot;A&quot;, when you submit the form, the following error is displayed on the form:</span></span>

`The field First Name must be a string with a minimum length of 3 and a maximum length of 8.`

<span data-ttu-id="7e15d-183">V tomto kurzu považujete uživatelské jméno za primární klíč.</span><span class="sxs-lookup"><span data-stu-id="7e15d-183">In this tutorial, you're treating the user name as the primary key.</span></span> <span data-ttu-id="7e15d-184">Proto nelze změnit vlastnost uživatelského jména.</span><span class="sxs-lookup"><span data-stu-id="7e15d-184">Therefore, the user name property cannot be changed.</span></span> <span data-ttu-id="7e15d-185">V souboru *Edit. cshtml* hned za příkazem `Html.BeginForm` nastavte uživatelské jméno na skryté pole.</span><span class="sxs-lookup"><span data-stu-id="7e15d-185">In the *Edit.cshtml* file, just after the `Html.BeginForm` statement, set the user name to be a hidden field.</span></span> <span data-ttu-id="7e15d-186">Způsobí to, že se vlastnost předává do modelu.</span><span class="sxs-lookup"><span data-stu-id="7e15d-186">This causes the property to be passed in the model.</span></span> <span data-ttu-id="7e15d-187">Následující fragment kódu ukazuje umístění příkazu `Hidden`:</span><span class="sxs-lookup"><span data-stu-id="7e15d-187">The following code fragment shows the placement of the `Hidden` statement:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample10.cshtml)]

<span data-ttu-id="7e15d-188">Nahraďte `TextBoxFor` a `ValidationMessageFor` označení uživatelského jména pomocí volání `DisplayFor`.</span><span class="sxs-lookup"><span data-stu-id="7e15d-188">Replace the `TextBoxFor` and `ValidationMessageFor` markup for the user name with a `DisplayFor` call.</span></span> <span data-ttu-id="7e15d-189">Metoda `DisplayFor` zobrazí vlastnost jako element jen pro čtení.</span><span class="sxs-lookup"><span data-stu-id="7e15d-189">The `DisplayFor` method displays the property as a read-only element.</span></span> <span data-ttu-id="7e15d-190">Následující příklad ukazuje dokončený kód.</span><span class="sxs-lookup"><span data-stu-id="7e15d-190">The following example shows the completed markup.</span></span> <span data-ttu-id="7e15d-191">Původní volání `TextBoxFor` a `ValidationMessageFor` jsou zakomentovány pomocí znaků Begin-Comment a koncových komentářů Razor (`@* *@`).</span><span class="sxs-lookup"><span data-stu-id="7e15d-191">The original `TextBoxFor` and `ValidationMessageFor` calls are commented out with the Razor begin-comment and end-comment characters (`@* *@`)</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample11.cshtml)]

## <a name="enabling-client-side-validation"></a><span data-ttu-id="7e15d-192">Povolení ověřování na straně klienta</span><span class="sxs-lookup"><span data-stu-id="7e15d-192">Enabling Client-Side Validation</span></span>

<span data-ttu-id="7e15d-193">Chcete-li povolit ověřování na straně klienta v ASP.NET MVC 3, musíte nastavit dva příznaky a musíte zahrnout tři soubory JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="7e15d-193">To enable client-side validation in ASP.NET MVC 3, you must set two flags and you must include three JavaScript files.</span></span>

<span data-ttu-id="7e15d-194">Otevřete soubor *Web. config* aplikace.</span><span class="sxs-lookup"><span data-stu-id="7e15d-194">Open the application's *Web.config* file.</span></span> <span data-ttu-id="7e15d-195">Ověřte `that ClientValidationEnabled` a `UnobtrusiveJavaScriptEnabled` v nastavení aplikace nastaveny na hodnotu true.</span><span class="sxs-lookup"><span data-stu-id="7e15d-195">Verify `that ClientValidationEnabled` and `UnobtrusiveJavaScriptEnabled` are set to true in the application settings.</span></span> <span data-ttu-id="7e15d-196">Následující fragment v kořenovém souboru *Web. config* zobrazuje správná nastavení:</span><span class="sxs-lookup"><span data-stu-id="7e15d-196">The following fragment from the root *Web.config* file shows the correct settings:</span></span>

[!code-xml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample12.xml)]

<span data-ttu-id="7e15d-197">Nastavením `UnobtrusiveJavaScriptEnabled` na true povolíte nenápad AJAX a nebudete moct ověřit klienta.</span><span class="sxs-lookup"><span data-stu-id="7e15d-197">Setting `UnobtrusiveJavaScriptEnabled` to true enables unobtrusive Ajax and unobtrusive client validation.</span></span> <span data-ttu-id="7e15d-198">Při použití nenáročného ověřování jsou ověřovací pravidla převedena na atributy HTML5.</span><span class="sxs-lookup"><span data-stu-id="7e15d-198">When you use unobtrusive validation, the validation rules are turned into HTML5 attributes.</span></span> <span data-ttu-id="7e15d-199">Názvy atributů HTML5 můžou obsahovat jenom malá písmena, číslice a pomlčky.</span><span class="sxs-lookup"><span data-stu-id="7e15d-199">HTML5 attribute names can consist of only lowercase letters, numbers, and dashes.</span></span>

<span data-ttu-id="7e15d-200">Nastavení `ClientValidationEnabled` na true povolí ověřování na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="7e15d-200">Setting `ClientValidationEnabled` to true enables client-side validation.</span></span> <span data-ttu-id="7e15d-201">Nastavením těchto klíčů v souboru *Web. config* aplikace povolíte ověřování klienta a nenápadný jazyk JavaScript pro celou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="7e15d-201">By setting these keys in the application *Web.config* file, you enable client validation and unobtrusive JavaScript for the entire application.</span></span> <span data-ttu-id="7e15d-202">Tato nastavení můžete povolit nebo zakázat v individuálních zobrazeních nebo v metodách kontroleru pomocí následujícího kódu:</span><span class="sxs-lookup"><span data-stu-id="7e15d-202">You can also enable or disable these settings in individual views or in controller methods using the following code:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample13.cs)]

<span data-ttu-id="7e15d-203">Také je nutné do vykresleného zobrazení zahrnout několik souborů JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="7e15d-203">You also need to include several JavaScript files in the rendered view.</span></span> <span data-ttu-id="7e15d-204">Snadný způsob, jak zahrnout JavaScript do všech zobrazení, je přidat je do souboru *Views\Shared\\_Layout. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="7e15d-204">An easy way to include the JavaScript in all views is to add them to the *Views\Shared\\_Layout.cshtml* file.</span></span> <span data-ttu-id="7e15d-205">Nahraďte `<head>` element souboru *\_layout. cshtml* následujícím kódem:</span><span class="sxs-lookup"><span data-stu-id="7e15d-205">Replace the `<head>` element of the *\_Layout.cshtml* file with the following code:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample14.cshtml)]

<span data-ttu-id="7e15d-206">První dva skripty jQuery jsou hostovány rozhraním Microsoft Ajax Content Delivery Network (CDN).</span><span class="sxs-lookup"><span data-stu-id="7e15d-206">The first two jQuery scripts are hosted by the Microsoft Ajax Content Delivery Network (CDN).</span></span> <span data-ttu-id="7e15d-207">Když využijete Microsoft Ajax CDN, můžete významně vylepšit výkon vašich aplikací při prvním zásahu.</span><span class="sxs-lookup"><span data-stu-id="7e15d-207">By taking advantage of the Microsoft Ajax CDN, you can significantly improve the first-hit performance of your applications.</span></span>

<span data-ttu-id="7e15d-208">Spusťte aplikaci a klikněte na odkaz Upravit.</span><span class="sxs-lookup"><span data-stu-id="7e15d-208">Run the application and click an edit link.</span></span> <span data-ttu-id="7e15d-209">Zobrazení zdroje stránky v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="7e15d-209">View the page's source in the browser.</span></span> <span data-ttu-id="7e15d-210">Zdroj prohlížeče zobrazuje mnoho atributů `data-val` formuláře (pro ověření dat).</span><span class="sxs-lookup"><span data-stu-id="7e15d-210">The browser source shows many attributes of the form `data-val` (for data validation).</span></span> <span data-ttu-id="7e15d-211">Když je povolená kontrola klienta a nenáročná technologie JavaScript, vstupní pole s pravidlem ověření klienta obsahují atribut `data-val="true"`, který aktivuje nenáročné ověřování klienta.</span><span class="sxs-lookup"><span data-stu-id="7e15d-211">When client validation and unobtrusive JavaScript is enabled, input fields with a client-validation rule contain the `data-val="true"` attribute to trigger unobtrusive client validation.</span></span> <span data-ttu-id="7e15d-212">Například pole `City` v modelu bylo upraveno pomocí [povinného](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) atributu, což vede k zobrazení kódu HTML v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="7e15d-212">For example, the `City` field in the model was decorated with the [Required](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.requiredattribute.aspx) attribute, which results in the HTML shown in the following example:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample15.cshtml)]

<span data-ttu-id="7e15d-213">Pro každé pravidlo ověřování klienta se přidá atribut, který má `data-val-rulename="message"`formuláře.</span><span class="sxs-lookup"><span data-stu-id="7e15d-213">For each client-validation rule, an attribute is added that has the form `data-val-rulename="message"`.</span></span> <span data-ttu-id="7e15d-214">Pomocí příkladu pole `City` uvedeného výše vygeneruje požadované pravidlo ověřování klienta `data-val-required` atribut a zprávu &quot;pole City (město) se vyžaduje&quot;.</span><span class="sxs-lookup"><span data-stu-id="7e15d-214">Using the `City` field example shown earlier, the required client-validation rule generates the `data-val-required` attribute and the message &quot;The City field is required&quot;.</span></span> <span data-ttu-id="7e15d-215">Spusťte aplikaci, upravte jednoho z nich a zrušte zaškrtnutí pole `City`.</span><span class="sxs-lookup"><span data-stu-id="7e15d-215">Run the application, edit one of the users, and clear the `City` field.</span></span> <span data-ttu-id="7e15d-216">Když zaškrtnete pole na kartě, zobrazí se chybová zpráva ověřování na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="7e15d-216">When you tab out of the field, you see a client-side validation error message.</span></span>

![Požadováno měst](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image14.png)

<span data-ttu-id="7e15d-218">Podobně platí, že pro každý parametr v pravidle ověřování klienta je přidán atribut, který má `data-val-rulename-paramname=paramvalue`formuláře.</span><span class="sxs-lookup"><span data-stu-id="7e15d-218">Similarly, for each parameter in the client-validation rule, an attribute is added that has the form `data-val-rulename-paramname=paramvalue`.</span></span> <span data-ttu-id="7e15d-219">Například vlastnost `FirstName` je označena atributem [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) a určuje minimální délku 3 a maximální délku 8.</span><span class="sxs-lookup"><span data-stu-id="7e15d-219">For example, the `FirstName` property is annotated with the [StringLength](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.stringlengthattribute.aspx) attribute and specifies a minimum length of 3 and a maximum length of 8.</span></span> <span data-ttu-id="7e15d-220">Pravidlo ověření dat s názvem `length` má `max` název parametru a hodnotu parametru 8.</span><span class="sxs-lookup"><span data-stu-id="7e15d-220">The data validation rule named `length` has the parameter name `max` and the parameter value 8.</span></span> <span data-ttu-id="7e15d-221">Následující text zobrazuje kód HTML, který je generován pro pole `FirstName` při úpravě jednoho z uživatelů:</span><span class="sxs-lookup"><span data-stu-id="7e15d-221">The following shows the HTML that is generated for the `FirstName` field when you edit one of the users:</span></span>

[!code-cshtml[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample16.cshtml)]

<span data-ttu-id="7e15d-222">Další informace o tom, jak neupozornit na ověření klienta, najdete v článku o [nenápadu ověřování klienta v ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) v blogu bradu Wilson.</span><span class="sxs-lookup"><span data-stu-id="7e15d-222">For more information about unobtrusive client validation, see the entry [Unobtrusive Client Validation in ASP.NET MVC 3](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html) in Brad Wilson's blog.</span></span>

> [!NOTE]
> <span data-ttu-id="7e15d-223">V ASP.NET MVC 3 beta je někdy nutné formulář odeslat, aby bylo možné spustit ověřování na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="7e15d-223">In ASP.NET MVC 3 Beta, you sometimes need to submit the form in order to start client-side validation.</span></span> <span data-ttu-id="7e15d-224">To může být pro finální verzi změněno.</span><span class="sxs-lookup"><span data-stu-id="7e15d-224">This might be changed for the final release.</span></span>

## <a name="creating-the-create-view"></a><span data-ttu-id="7e15d-225">Vytvoření zobrazení pro vytvoření</span><span class="sxs-lookup"><span data-stu-id="7e15d-225">Creating the Create View</span></span>

<span data-ttu-id="7e15d-226">Dalším krokem je přidání metody a zobrazení akce `Create`, aby uživatel mohl vytvořit nového uživatele.</span><span class="sxs-lookup"><span data-stu-id="7e15d-226">The next step is to add a `Create` action method and view in order to enable the user to create a new user.</span></span> <span data-ttu-id="7e15d-227">Do domovského kontroleru přidejte následující metodu `Create`:</span><span class="sxs-lookup"><span data-stu-id="7e15d-227">Add the following `Create` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample17.cs)]

<span data-ttu-id="7e15d-228">Přidejte zobrazení jako v předchozích krocích, ale nastavte **zobrazení obsahu** na **vytvořit**.</span><span class="sxs-lookup"><span data-stu-id="7e15d-228">Add a view as in the previous steps, but set **View content** to **Create**.</span></span>

![Create View](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image15.png)

<span data-ttu-id="7e15d-230">Spusťte aplikaci, vyberte odkaz **vytvořit** a přidejte nového uživatele.</span><span class="sxs-lookup"><span data-stu-id="7e15d-230">Run the application, select the **Create** link, and add a new user.</span></span> <span data-ttu-id="7e15d-231">Metoda `Create` automaticky využívá ověřování na straně klienta a serveru.</span><span class="sxs-lookup"><span data-stu-id="7e15d-231">The `Create` method automatically takes advantage of client-side and server-side validation.</span></span> <span data-ttu-id="7e15d-232">Zkuste zadat uživatelské jméno, které obsahuje prázdné znaky, například &quot;Ben X&quot;.</span><span class="sxs-lookup"><span data-stu-id="7e15d-232">Try to enter a user name that contains white space, such as &quot;Ben X&quot;.</span></span> <span data-ttu-id="7e15d-233">Když zadáte kartu z pole uživatelské jméno, zobrazí se chyba ověřování na straně klienta (`White space is not allowed`).</span><span class="sxs-lookup"><span data-stu-id="7e15d-233">When you tab out of the user name field, a client-side validation error (`White space is not allowed`) is displayed.</span></span>

## <a name="add-the-delete-method"></a><span data-ttu-id="7e15d-234">Přidat metodu DELETE</span><span class="sxs-lookup"><span data-stu-id="7e15d-234">Add the Delete method</span></span>

<span data-ttu-id="7e15d-235">K dokončení tohoto kurzu přidejte do domovského kontroleru následující metodu `Delete`:</span><span class="sxs-lookup"><span data-stu-id="7e15d-235">To complete the tutorial, add the following `Delete` method to the home controller:</span></span>

[!code-csharp[Main](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/samples/sample18.cs)]

<span data-ttu-id="7e15d-236">Přidejte zobrazení `Delete` jako v předchozích krocích, nastavením **zobrazení obsahu** pro **odstranění**.</span><span class="sxs-lookup"><span data-stu-id="7e15d-236">Add a `Delete` view as in the previous steps, setting **View content** to **Delete**.</span></span>

![Odstranit zobrazení](creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript/_static/image16.png)

<span data-ttu-id="7e15d-238">Teď máte jednoduchou, ale plně funkční ASP.NET aplikaci MVC 3 s ověřením.</span><span class="sxs-lookup"><span data-stu-id="7e15d-238">You now have a simple but fully functional ASP.NET MVC 3 application with validation.</span></span>

---
uid: web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
title: Ověřování vstupu uživatele v lokalitách ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Tento článek popisuje, jak ověřit informace, které získáte od uživatelů &mdash;, abyste se ujistili, že uživatelé zadávají platné informace ve formulářích HTML v...
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 4eb060cc-cf14-41ae-bab1-14a2c15332d0
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/validating-user-input-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: e6f8e1051d09d11f1756bfada44a73ba7c2a1db2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563502"
---
# <a name="validating-user-input-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="e5e16-103">Ověřování vstupu uživatele na webech ASP.NET Web Pages (Razor)</span><span class="sxs-lookup"><span data-stu-id="e5e16-103">Validating User Input in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="e5e16-104">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="e5e16-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="e5e16-105">Tento článek popisuje, jak ověřit informace, které dostanete od uživatelů &mdash;, aby se zajistilo, že uživatelé zadávají platné informace ve formulářích HTML na webu ASP.NET Web Pages (Razor).</span><span class="sxs-lookup"><span data-stu-id="e5e16-105">This article discusses how to validate information you get from users &mdash; that is, to make sure that users enter valid information in HTML forms in an ASP.NET Web Pages (Razor) site.</span></span>
> 
> <span data-ttu-id="e5e16-106">Naučíte se:</span><span class="sxs-lookup"><span data-stu-id="e5e16-106">What you'll learn:</span></span>
> 
> - <span data-ttu-id="e5e16-107">Jak ověřit, jestli vstup uživatele odpovídá ověřovacím kritériím, která definujete.</span><span class="sxs-lookup"><span data-stu-id="e5e16-107">How to check that a user's input matches validation criteria that you define.</span></span>
> - <span data-ttu-id="e5e16-108">Jak určit, zda všechny ověřovací testy prošly.</span><span class="sxs-lookup"><span data-stu-id="e5e16-108">How to determine whether all validation tests have passed.</span></span>
> - <span data-ttu-id="e5e16-109">Jak zobrazit chyby ověřování (a jak je naformátovat).</span><span class="sxs-lookup"><span data-stu-id="e5e16-109">How to display validation errors (and how to format them).</span></span>
> - <span data-ttu-id="e5e16-110">Ověření dat, která nepřicházejí přímo od uživatelů</span><span class="sxs-lookup"><span data-stu-id="e5e16-110">How to validate data that doesn't come directly from users.</span></span>
> 
> <span data-ttu-id="e5e16-111">Toto jsou koncepty programování ASP.NET představené v článku:</span><span class="sxs-lookup"><span data-stu-id="e5e16-111">These are the ASP.NET programming concepts introduced in the article:</span></span>
> 
> - <span data-ttu-id="e5e16-112">Pomocná rutina `Validation`</span><span class="sxs-lookup"><span data-stu-id="e5e16-112">The `Validation` helper.</span></span>
> - <span data-ttu-id="e5e16-113">Metody `Html.ValidationSummary` a `Html.ValidationMessage`.</span><span class="sxs-lookup"><span data-stu-id="e5e16-113">The `Html.ValidationSummary` and `Html.ValidationMessage` methods.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e5e16-114">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="e5e16-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="e5e16-115">Webové stránky ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="e5e16-115">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="e5e16-116">Tento kurz funguje také s ASP.NET webovými stránkami 2.</span><span class="sxs-lookup"><span data-stu-id="e5e16-116">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="e5e16-117">Tento článek obsahuje následující oddíly:</span><span class="sxs-lookup"><span data-stu-id="e5e16-117">This article contains the following sections:</span></span>

- [<span data-ttu-id="e5e16-118">Přehled ověřování vstupu uživatele</span><span class="sxs-lookup"><span data-stu-id="e5e16-118">Overview of User Input Validation</span></span>](#Overview_of_User_Input_Validation)
- [<span data-ttu-id="e5e16-119">Ověřování vstupu uživatele</span><span class="sxs-lookup"><span data-stu-id="e5e16-119">Validating User Input</span></span>](#Validating_User_Input)
- [<span data-ttu-id="e5e16-120">Přidání ověřování na straně klienta</span><span class="sxs-lookup"><span data-stu-id="e5e16-120">Adding Client-Side Validation</span></span>](#Adding_Client-Side_Validation)
- [<span data-ttu-id="e5e16-121">Chyby ověřování formátování</span><span class="sxs-lookup"><span data-stu-id="e5e16-121">Formatting Validation Errors</span></span>](#Formatting_Validation_Errors)
- [<span data-ttu-id="e5e16-122">Ověřování dat, která nepřicházejí přímo od uživatelů</span><span class="sxs-lookup"><span data-stu-id="e5e16-122">Validating Data That Doesn't Come Directly from Users</span></span>](#Validating_Data_That_Doesnt_Come_Directly_from_Users)

<a id="Overview_of_User_Input_Validation"></a>
## <a name="overview-of-user-input-validation"></a><span data-ttu-id="e5e16-123">Přehled ověřování vstupu uživatele</span><span class="sxs-lookup"><span data-stu-id="e5e16-123">Overview of User Input Validation</span></span>

<span data-ttu-id="e5e16-124">Pokud požádáte uživatele, aby zadali informace na stránce, například do formuláře, je důležité se ujistit, že hodnoty, které vstoupí, jsou platné.</span><span class="sxs-lookup"><span data-stu-id="e5e16-124">If you ask users to enter information in a page — for example, into a form — it's important to make sure that the values that they enter are valid.</span></span> <span data-ttu-id="e5e16-125">Nechcete například zpracovat formulář, který neobsahuje důležité informace.</span><span class="sxs-lookup"><span data-stu-id="e5e16-125">For example, you don't want to process a form that's missing critical information.</span></span>

<span data-ttu-id="e5e16-126">Když uživatelé zadávají hodnoty do formuláře HTML, hodnoty, které vstupují, jsou řetězce.</span><span class="sxs-lookup"><span data-stu-id="e5e16-126">When users enter values into an HTML form, the values that they enter are strings.</span></span> <span data-ttu-id="e5e16-127">V mnoha případech jsou hodnoty, které potřebujete, některými jinými datovými typy, jako jsou celá čísla nebo kalendářní data.</span><span class="sxs-lookup"><span data-stu-id="e5e16-127">In many cases, the values you need are some other data types, like integers or dates.</span></span> <span data-ttu-id="e5e16-128">Proto musíte také zajistit, aby hodnoty, které uživatel zadal, mohly být správně převedeny na příslušné datové typy.</span><span class="sxs-lookup"><span data-stu-id="e5e16-128">Therefore, you also have to make sure that the values that users enter can be correctly converted to the appropriate data types.</span></span>

<span data-ttu-id="e5e16-129">U těchto hodnot můžete mít také určitá omezení.</span><span class="sxs-lookup"><span data-stu-id="e5e16-129">You might also have certain restrictions on the values.</span></span> <span data-ttu-id="e5e16-130">I když uživatelé správně zadají celé číslo, může být třeba se ujistit, že hodnota spadá do určitého rozsahu.</span><span class="sxs-lookup"><span data-stu-id="e5e16-130">Even if users correctly enter an integer, for example, you might need to make sure that the value falls within a certain range.</span></span>

![Chyby ověřování, které používají třídy stylů CSS](validating-user-input-in-aspnet-web-pages-sites/_static/image1.png)

> [!NOTE] 
> 
> <span data-ttu-id="e5e16-132">**Důležité** informace Ověřování vstupu uživatele je také důležité pro zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="e5e16-132">**Important** Validating user input is also important for security.</span></span> <span data-ttu-id="e5e16-133">Pokud omezíte hodnoty, které mohou uživatelé zadat do formulářů, snížíte pravděpodobnost, že může někdo zadat hodnotu, která může ohrozit zabezpečení vašeho webu.</span><span class="sxs-lookup"><span data-stu-id="e5e16-133">When you restrict the values that users can enter in forms, you reduce the chance that someone can enter a value that can compromise the security of your site.</span></span>

<a id="Validating_User_Input"></a>
## <a name="validating-user-input"></a><span data-ttu-id="e5e16-134">Ověřování vstupu uživatele</span><span class="sxs-lookup"><span data-stu-id="e5e16-134">Validating User Input</span></span>

<span data-ttu-id="e5e16-135">V ASP.NET webové stránky 2 můžete použít pomocníka `Validator` pro testování vstupu uživatele.</span><span class="sxs-lookup"><span data-stu-id="e5e16-135">In ASP.NET Web Pages 2, you can use the `Validator` helper to test user input.</span></span> <span data-ttu-id="e5e16-136">Základní postup je následující:</span><span class="sxs-lookup"><span data-stu-id="e5e16-136">The basic approach is to do the following:</span></span>

1. <span data-ttu-id="e5e16-137">Určete, které vstupní prvky (pole) chcete ověřit.</span><span class="sxs-lookup"><span data-stu-id="e5e16-137">Determine which input elements (fields) you want to validate.</span></span>

    <span data-ttu-id="e5e16-138">Hodnoty jsou obvykle ověřeny ve `<input>` prvky ve formuláři.</span><span class="sxs-lookup"><span data-stu-id="e5e16-138">You typically validate values in `<input>` elements in a form.</span></span> <span data-ttu-id="e5e16-139">Je však dobrým zvykem ověřit všechny vstupy, dokonce i vstupy, které pocházejí z omezeného prvku, jako je například seznam `<select>`.</span><span class="sxs-lookup"><span data-stu-id="e5e16-139">However, it's a good practice to validate all input, even input that comes from a constrained element like a `<select>` list.</span></span> <span data-ttu-id="e5e16-140">To pomáhá zajistit, že uživatelé neobejde ovládací prvky na stránce a odešlou formulář.</span><span class="sxs-lookup"><span data-stu-id="e5e16-140">This helps to make sure that users don't bypass the controls on a page and submit a form.</span></span>
2. <span data-ttu-id="e5e16-141">V kódu stránky přidejte jednotlivé kontroly ověřování pro každý element input pomocí metod pomocné rutiny `Validation`.</span><span class="sxs-lookup"><span data-stu-id="e5e16-141">In the page code, add individual validation checks for each input element by using methods of the `Validation` helper.</span></span>

    <span data-ttu-id="e5e16-142">Chcete-li vyhledat požadovaná pole, použijte `Validation.RequireField(field, [error message])` (pro jednotlivá pole) nebo `Validation.RequireFields(field1, field2, ...))` (pro seznam polí).</span><span class="sxs-lookup"><span data-stu-id="e5e16-142">To check for required fields, use `Validation.RequireField(field, [error message])` (for an individual field) or `Validation.RequireFields(field1, field2, ...))` (for a list of fields).</span></span> <span data-ttu-id="e5e16-143">Pro jiné typy ověřování použijte `Validation.Add(field, ValidationType)`.</span><span class="sxs-lookup"><span data-stu-id="e5e16-143">For other types of validation, use `Validation.Add(field, ValidationType)`.</span></span> <span data-ttu-id="e5e16-144">Pro `ValidationType`můžete použít tyto možnosti:</span><span class="sxs-lookup"><span data-stu-id="e5e16-144">For `ValidationType`, you can use these options:</span></span>

    `Validator.DateTime ([error message])`  
   `Validator.Decimal([error message])`  
   `Validator.EqualsTo(otherField [, error message])`  
   `Validator.Float([error message])`  
   `Validator.Integer([error message])`  
   `Validator.Range(min, max [, error message])`  
   `Validator.RegEx(pattern [, error message])`  
   `Validator.Required([error message])`  
   `Validator.StringLength(length)`  
   `Validator.Url([error message])`
3. <span data-ttu-id="e5e16-145">Po odeslání stránky ověřte, zda ověření proběhlo zaškrtnutím `Validation.IsValid`:</span><span class="sxs-lookup"><span data-stu-id="e5e16-145">When the page is submitted, check whether validation has passed by checking `Validation.IsValid`:</span></span>

    [!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample1.cs)]

    <span data-ttu-id="e5e16-146">Pokud dojde k chybám ověřování, přeskočíte normální zpracování stránky.</span><span class="sxs-lookup"><span data-stu-id="e5e16-146">If there are any validation errors, you skip normal page processing.</span></span> <span data-ttu-id="e5e16-147">Například pokud účelem stránky je aktualizovat databázi, neuděláte to, dokud nebudou opraveny všechny chyby ověřování.</span><span class="sxs-lookup"><span data-stu-id="e5e16-147">For example, if the purpose of the page is to update a database, you don't do that until all validation errors have been fixed.</span></span>
4. <span data-ttu-id="e5e16-148">Pokud dojde k chybám ověření, zobrazí se chybové zprávy v kódu stránky pomocí `Html.ValidationSummary` nebo `Html.ValidationMessage`nebo obojího.</span><span class="sxs-lookup"><span data-stu-id="e5e16-148">If there are validation errors, display error messages in the page's markup by using `Html.ValidationSummary` or `Html.ValidationMessage`, or both.</span></span>

<span data-ttu-id="e5e16-149">Následující příklad ukazuje stránku, která znázorňuje tyto kroky.</span><span class="sxs-lookup"><span data-stu-id="e5e16-149">The following example shows a page that illustrates these steps.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample2.cshtml)]

<span data-ttu-id="e5e16-150">Pokud chcete zjistit, jak ověřování funguje, spusťte tuto stránku a záměrně udělejte chyby.</span><span class="sxs-lookup"><span data-stu-id="e5e16-150">To see how validation works, run this page and deliberately make mistakes.</span></span> <span data-ttu-id="e5e16-151">Tady je příklad, jak stránka vypadá, když zapomenete zadat název kurzu, pokud zadáte a zadáte neplatné datum:</span><span class="sxs-lookup"><span data-stu-id="e5e16-151">For example, here's what the page looks like if you forget to enter a course name, if you enter an, and if you enter an invalid date:</span></span>

![Chyby ověřování na vykreslené stránce](validating-user-input-in-aspnet-web-pages-sites/_static/image2.png)

<a id="Adding_Client-Side_Validation"></a>
## <a name="adding-client-side-validation"></a><span data-ttu-id="e5e16-153">Přidání ověřování na straně klienta</span><span class="sxs-lookup"><span data-stu-id="e5e16-153">Adding Client-Side Validation</span></span>

<span data-ttu-id="e5e16-154">Ve výchozím nastavení se uživatelský vstup ověří poté, co uživatel stránku odešle – to znamená, že ověření proběhne v kódu serveru.</span><span class="sxs-lookup"><span data-stu-id="e5e16-154">By default, user input is validated after users submit the page — that is, the validation is performed in server code.</span></span> <span data-ttu-id="e5e16-155">Nevýhodou tohoto přístupu je, že uživatelé nevědí, že udělali chybu až po odeslání stránky.</span><span class="sxs-lookup"><span data-stu-id="e5e16-155">A disadvantage of this approach is that users don't know that they've made an error until after they submit the page.</span></span> <span data-ttu-id="e5e16-156">V případě, že je formulář dlouhý nebo složitý, mohou být chyby zasílání zpráv pouze po odeslání stránky pro uživatele nepohodlné.</span><span class="sxs-lookup"><span data-stu-id="e5e16-156">If a form is long or complex, reporting errors only after the page is submitted can be inconvenient to the user.</span></span>

<span data-ttu-id="e5e16-157">Můžete přidat podporu, která provádí ověřování v klientském skriptu.</span><span class="sxs-lookup"><span data-stu-id="e5e16-157">You can add support to perform validation in client script.</span></span> <span data-ttu-id="e5e16-158">V takovém případě se ověřování provádí, protože uživatelé pracují v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="e5e16-158">In that case, the validation is performed as users work in the browser.</span></span> <span data-ttu-id="e5e16-159">Předpokládejme například, že zadáte, že hodnota by měla být celé číslo.</span><span class="sxs-lookup"><span data-stu-id="e5e16-159">For example, suppose you specify that a value should be an integer.</span></span> <span data-ttu-id="e5e16-160">Pokud uživatel zadá hodnotu, která není celočíselná, zobrazí se chyba, jakmile uživatel opustí pole pro zadání.</span><span class="sxs-lookup"><span data-stu-id="e5e16-160">If a user enters a non-integer value, the error is reported as soon as the user leaves the entry field.</span></span> <span data-ttu-id="e5e16-161">Uživatelé získají okamžitou zpětnou vazbu, která je pro ně vhodná.</span><span class="sxs-lookup"><span data-stu-id="e5e16-161">Users get immediate feedback, which is convenient for them.</span></span> <span data-ttu-id="e5e16-162">Ověřování na základě klienta může také snížit počet pokusů, které uživatel musí odeslat formuláři, aby opravil více chyb.</span><span class="sxs-lookup"><span data-stu-id="e5e16-162">Client-based validation can also reduce the number of times that the user has to submit the form to correct multiple errors.</span></span>

> [!NOTE]
> <span data-ttu-id="e5e16-163">I když používáte ověřování na straně klienta, ověřování se vždy provádí také v kódu serveru.</span><span class="sxs-lookup"><span data-stu-id="e5e16-163">Even if you use client-side validation, validation is always also performed in server code.</span></span> <span data-ttu-id="e5e16-164">Ověřování v kódu serveru je bezpečnostní opatření pro případ, že uživatelé obcházejí ověřování na základě klienta.</span><span class="sxs-lookup"><span data-stu-id="e5e16-164">Performing validation in server code is a security measure, in case users bypass client-based validation.</span></span>

1. <span data-ttu-id="e5e16-165">Zaregistrujte následující knihovny JavaScriptu na stránce:</span><span class="sxs-lookup"><span data-stu-id="e5e16-165">Register the following JavaScript libraries in the page:</span></span>  

    [!code-html[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample3.html)]

   <span data-ttu-id="e5e16-166">Dvě knihovny jsou spustitelný ze služby Content Delivery Network (CDN), takže je nemusíte nutně mít na počítači nebo na serveru.</span><span class="sxs-lookup"><span data-stu-id="e5e16-166">Two of the libraries are loadable from a content delivery network (CDN), so you don't necessarily have to have them on your computer or server.</span></span> <span data-ttu-id="e5e16-167">Je však nutné mít místní kopii *jQuery. Validate. nenáročná. js*.</span><span class="sxs-lookup"><span data-stu-id="e5e16-167">However, you must have a local copy of *jquery.validate.unobtrusive.js*.</span></span> <span data-ttu-id="e5e16-168">Pokud ještě nepracujete se šablonou WebMatrix (jako je **startovní web** ), která obsahuje knihovnu, vytvořte web webové stránky, který je založen na **počátečním webu**.</span><span class="sxs-lookup"><span data-stu-id="e5e16-168">If you are not already working with a WebMatrix template (like **Starter Site** ) that includes the library, create a Web Pages site that's based on **Starter Site**.</span></span> <span data-ttu-id="e5e16-169">Pak zkopírujte soubor *. js* na aktuální web.</span><span class="sxs-lookup"><span data-stu-id="e5e16-169">Then copy the *.js* file to your current site.</span></span>
2. <span data-ttu-id="e5e16-170">V označení pro každý prvek, který budete ověřovat, přidejte volání `Validation.For(field)`.</span><span class="sxs-lookup"><span data-stu-id="e5e16-170">In markup, for each element that you're validating, add a call to `Validation.For(field)`.</span></span> <span data-ttu-id="e5e16-171">Tato metoda generuje atributy, které se používají při ověřování na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="e5e16-171">This method emits attributes that are used by client-side validation.</span></span> <span data-ttu-id="e5e16-172">(Místo toho, aby vygeneroval skutečný kód JavaScriptu, metoda vygeneruje atributy jako `data-val-...`.</span><span class="sxs-lookup"><span data-stu-id="e5e16-172">(Rather than emitting actual JavaScript code, the method emits attributes like `data-val-...`.</span></span> <span data-ttu-id="e5e16-173">Tyto atributy podporují nenápadné ověření klienta, které používá jQuery k provedení práce.)</span><span class="sxs-lookup"><span data-stu-id="e5e16-173">These attributes support unobtrusive client validation that uses jQuery to do the work.)</span></span>

<span data-ttu-id="e5e16-174">Následující stránka ukazuje, jak přidat funkce ověřování klientů do výše uvedeného příkladu.</span><span class="sxs-lookup"><span data-stu-id="e5e16-174">The following page shows how to add client validation features to the example shown earlier.</span></span>

[!code-cshtml[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample4.cshtml?highlight=35-39,51,61,71)]

<span data-ttu-id="e5e16-175">Ne všechny ověřovací kontroly jsou spuštěny na klientovi.</span><span class="sxs-lookup"><span data-stu-id="e5e16-175">Not all validation checks run on the client.</span></span> <span data-ttu-id="e5e16-176">Konkrétně ověřování typu dat (celé číslo, datum atd.) neběží na klientovi.</span><span class="sxs-lookup"><span data-stu-id="e5e16-176">In particular, data-type validation (integer, date, and so on) don't run on the client.</span></span> <span data-ttu-id="e5e16-177">Následující kontroly fungují na straně klienta i serveru:</span><span class="sxs-lookup"><span data-stu-id="e5e16-177">The following checks work on both the client and server:</span></span>

- `Required`
- `Range(minValue, maxValue)`
- `StringLength(maxLength[, minLength])`
- `Regex(pattern)`
- `EqualsTo(otherField)`

<span data-ttu-id="e5e16-178">V tomto příkladu test pro platné datum nebude fungovat v klientském kódu.</span><span class="sxs-lookup"><span data-stu-id="e5e16-178">In this example, the test for a valid date won't work in client code.</span></span> <span data-ttu-id="e5e16-179">Test se ale provede v kódu serveru.</span><span class="sxs-lookup"><span data-stu-id="e5e16-179">However, the test will be performed in server code.</span></span>

<a id="Formatting_Validation_Errors"></a>
## <a name="formatting-validation-errors"></a><span data-ttu-id="e5e16-180">Chyby ověřování formátování</span><span class="sxs-lookup"><span data-stu-id="e5e16-180">Formatting Validation Errors</span></span>

<span data-ttu-id="e5e16-181">Můžete řídit, jak se zobrazují chyby ověřování tím, že definujete třídy CSS, které mají následující rezervované názvy:</span><span class="sxs-lookup"><span data-stu-id="e5e16-181">You can control how validation errors are displayed by defining CSS classes that have the following reserved names:</span></span>

- <span data-ttu-id="e5e16-182">`field-validation-error`.</span><span class="sxs-lookup"><span data-stu-id="e5e16-182">`field-validation-error`.</span></span> <span data-ttu-id="e5e16-183">Definuje výstup metody `Html.ValidationMessage`, když se zobrazuje chyba.</span><span class="sxs-lookup"><span data-stu-id="e5e16-183">Defines the output of the `Html.ValidationMessage` method when it's displaying an error.</span></span>
- <span data-ttu-id="e5e16-184">`field-validation-valid`.</span><span class="sxs-lookup"><span data-stu-id="e5e16-184">`field-validation-valid`.</span></span> <span data-ttu-id="e5e16-185">Definuje výstup metody `Html.ValidationMessage`, pokud není k dispozici žádná chyba.</span><span class="sxs-lookup"><span data-stu-id="e5e16-185">Defines the output of the `Html.ValidationMessage` method when there is no error.</span></span>
- <span data-ttu-id="e5e16-186">`input-validation-error`.</span><span class="sxs-lookup"><span data-stu-id="e5e16-186">`input-validation-error`.</span></span> <span data-ttu-id="e5e16-187">Definuje, jak se vykreslují prvky `<input>`, když dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="e5e16-187">Defines how `<input>` elements are rendered when there's an error.</span></span> <span data-ttu-id="e5e16-188">(Například můžete použít tuto třídu k nastavení barvy pozadí &lt;vstupní&gt; elementu na jinou barvu, je-li její hodnota neplatná.) Tato třída CSS se používá pouze během ověřování klienta (na webových stránkách ASP.NET 2).</span><span class="sxs-lookup"><span data-stu-id="e5e16-188">(For example, you can use this class to set the background color of an &lt;input&gt; element to a different color if its value is invalid.) This CSS class is used only during client validation (in ASP.NET Web Pages 2).</span></span>
- <span data-ttu-id="e5e16-189">`input-validation-valid`.</span><span class="sxs-lookup"><span data-stu-id="e5e16-189">`input-validation-valid`.</span></span> <span data-ttu-id="e5e16-190">Definuje vzhled `<input>` prvků v případě, že není k dispozici žádná chyba.</span><span class="sxs-lookup"><span data-stu-id="e5e16-190">Defines the appearance of `<input>` elements when there is no error.</span></span>
- <span data-ttu-id="e5e16-191">`validation-summary-errors`.</span><span class="sxs-lookup"><span data-stu-id="e5e16-191">`validation-summary-errors`.</span></span> <span data-ttu-id="e5e16-192">Definuje výstup metody `Html.ValidationSummary` zobrazuje seznam chyb.</span><span class="sxs-lookup"><span data-stu-id="e5e16-192">Defines the output of the `Html.ValidationSummary` method it's displaying a list of errors.</span></span>
- <span data-ttu-id="e5e16-193">`validation-summary-valid`.</span><span class="sxs-lookup"><span data-stu-id="e5e16-193">`validation-summary-valid`.</span></span> <span data-ttu-id="e5e16-194">Definuje výstup metody `Html.ValidationSummary`, pokud není k dispozici žádná chyba.</span><span class="sxs-lookup"><span data-stu-id="e5e16-194">Defines the output of the `Html.ValidationSummary` method when there is no error.</span></span>

<span data-ttu-id="e5e16-195">Následující blok `<style>` obsahuje pravidla pro chybové podmínky.</span><span class="sxs-lookup"><span data-stu-id="e5e16-195">The following `<style>` block shows rules for error conditions.</span></span>

[!code-css[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample5.css)]

<span data-ttu-id="e5e16-196">Pokud tento blok stylu zadáte na vzorových stránkách výše v článku, zobrazí se chyba, která bude vypadat jako na následujícím obrázku:</span><span class="sxs-lookup"><span data-stu-id="e5e16-196">If you include this style block in the example pages from earlier in the article, the error display will look like the following illustration:</span></span>

![Chyby ověřování, které používají třídy stylů CSS](validating-user-input-in-aspnet-web-pages-sites/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="e5e16-198">Pokud nepoužíváte ověřování klienta v ASP.NET webové stránky 2, třídy CSS pro prvky `<input>` (`input-validation-error` a `input-validation-valid` nemají žádný vliv.</span><span class="sxs-lookup"><span data-stu-id="e5e16-198">If you're not using client validation in ASP.NET Web Pages 2, the CSS classes for the `<input>` elements (`input-validation-error` and `input-validation-valid` don't have any effect.</span></span>

### <a name="static-and-dynamic-error-display"></a><span data-ttu-id="e5e16-199">Zobrazení statické a dynamické chyby</span><span class="sxs-lookup"><span data-stu-id="e5e16-199">Static and Dynamic Error Display</span></span>

<span data-ttu-id="e5e16-200">Pravidla šablony stylů CSS jsou uvedena ve dvojicích, například `validation-summary-errors` a `validation-summary-valid`.</span><span class="sxs-lookup"><span data-stu-id="e5e16-200">The CSS rules come in pairs, such as `validation-summary-errors` and `validation-summary-valid`.</span></span> <span data-ttu-id="e5e16-201">Tyto páry umožňují definovat pravidla pro obě podmínky: chybový stav a podmínku "normální" (nejedná se o chyba).</span><span class="sxs-lookup"><span data-stu-id="e5e16-201">These pairs let you define rules for both conditions: an error condition and a "normal" (non-error) condition.</span></span> <span data-ttu-id="e5e16-202">Je důležité pochopit, že značky pro zobrazení chyb jsou vždy vykresleny, i když nejsou k dispozici žádné chyby.</span><span class="sxs-lookup"><span data-stu-id="e5e16-202">It's important to understand that the markup for the error display is always rendered, even if there are no errors.</span></span> <span data-ttu-id="e5e16-203">Například pokud má stránka jako metodu `Html.ValidationSummary` v kódu, bude zdroj stránky obsahovat následující kód, i když je stránka vyžadovaná poprvé:</span><span class="sxs-lookup"><span data-stu-id="e5e16-203">For example, if a page has an `Html.ValidationSummary` method in the markup, the page source will contain the following markup even when the page is requested for the first time:</span></span>

`<div class="validation-summary-valid" data-valmsg-summary="true"><ul></ul></div>`

<span data-ttu-id="e5e16-204">Jinými slovy, metoda `Html.ValidationSummary` vždy vykresluje `<div>` prvek a seznam, a to i v případě, že seznam chyb je prázdný.</span><span class="sxs-lookup"><span data-stu-id="e5e16-204">In other words, the `Html.ValidationSummary` method always renders a `<div>` element and a list, even if the error list is empty.</span></span> <span data-ttu-id="e5e16-205">Podobně metoda `Html.ValidationMessage` vždy vykresluje `<span>` prvek jako zástupný symbol pro chybu jednotlivých polí, a to i v případě, že nedošlo k chybě.</span><span class="sxs-lookup"><span data-stu-id="e5e16-205">Similarly, the `Html.ValidationMessage` method always renders a `<span>` element as a placeholder for an individual field error, even if there is no error.</span></span>

<span data-ttu-id="e5e16-206">V některých situacích může zobrazování chybové zprávy způsobit přetečení stránky a může způsobit, že se prvky na stránce pohybují.</span><span class="sxs-lookup"><span data-stu-id="e5e16-206">In some situations, displaying an error message can cause the page to reflow and can cause elements on the page to move around.</span></span> <span data-ttu-id="e5e16-207">Pravidla šablony stylů CSS, která končí `-valid` umožňují definovat rozložení, které vám může zabránit tomuto problému.</span><span class="sxs-lookup"><span data-stu-id="e5e16-207">The CSS rules that end in `-valid` let you define a layout that can help prevent this problem.</span></span> <span data-ttu-id="e5e16-208">Můžete například definovat `field-validation-error` a `field-validation-valid` mají stejnou pevnou velikost.</span><span class="sxs-lookup"><span data-stu-id="e5e16-208">For example, you can define `field-validation-error` and `field-validation-valid` to both have the same fixed size.</span></span> <span data-ttu-id="e5e16-209">Tímto způsobem je oblast zobrazení pro pole statická a při zobrazení chybové zprávy se tok stránky nezmění.</span><span class="sxs-lookup"><span data-stu-id="e5e16-209">That way, the display area for the field is static and won't change the page flow if an error message is displayed.</span></span>

<a id="Validating_Data_That_Doesnt_Come_Directly_from_Users"></a>
## <a name="validating-data-that-doesnt-come-directly-from-users"></a><span data-ttu-id="e5e16-210">Ověřování dat, která nepřicházejí přímo od uživatelů</span><span class="sxs-lookup"><span data-stu-id="e5e16-210">Validating Data That Doesn't Come Directly from Users</span></span>

<span data-ttu-id="e5e16-211">Někdy je nutné ověřit informace, které nepocházejí přímo z formuláře HTML.</span><span class="sxs-lookup"><span data-stu-id="e5e16-211">Sometimes you have to validate information that doesn't come directly from an HTML form.</span></span> <span data-ttu-id="e5e16-212">Typickým příkladem je stránka, kde je hodnota předána v řetězci dotazu, jako v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="e5e16-212">A typical example is a page where a value is passed in a query string, as in the following example:</span></span>

`http://server/myapp/EditClassInformation?classid=1022`

<span data-ttu-id="e5e16-213">V takovém případě se chcete ujistit, že hodnota, která je předána stránce (zde 1022 pro hodnotu `classid`), je platná.</span><span class="sxs-lookup"><span data-stu-id="e5e16-213">In this case, you want to make sure that the value that's passed to the page (here, 1022 for the value of `classid`) is valid.</span></span> <span data-ttu-id="e5e16-214">K provedení tohoto ověřování nemůžete přímo použít pomocníka `Validation`.</span><span class="sxs-lookup"><span data-stu-id="e5e16-214">You can't directly use the `Validation` helper to perform this validation.</span></span> <span data-ttu-id="e5e16-215">Můžete však použít jiné funkce systému ověřování, například možnost zobrazit chybové zprávy ověřování.</span><span class="sxs-lookup"><span data-stu-id="e5e16-215">However, you can use other features of the validation system, like the ability to display validation error messages.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="e5e16-216">**Důležité** informace Vždy ověří hodnoty, které získáte z *libovolného* zdroje, včetně hodnot polí formuláře, hodnot řetězce dotazu a hodnot souborů cookie.</span><span class="sxs-lookup"><span data-stu-id="e5e16-216">**Important** Always validate values that you get from *any* source, including form-field values, query-string values, and cookie values.</span></span> <span data-ttu-id="e5e16-217">Lidé můžou tyto hodnoty změnit (třeba pro škodlivé účely).</span><span class="sxs-lookup"><span data-stu-id="e5e16-217">It's easy for people to change these values (perhaps for malicious purposes).</span></span> <span data-ttu-id="e5e16-218">Aby bylo možné aplikaci chránit, je nutné tyto hodnoty ověřit.</span><span class="sxs-lookup"><span data-stu-id="e5e16-218">So you must check these values in order to protect your application.</span></span>

<span data-ttu-id="e5e16-219">Následující příklad ukazuje, jak můžete ověřit hodnotu, která je předána do řetězce dotazu.</span><span class="sxs-lookup"><span data-stu-id="e5e16-219">The following example shows how you might validate a value that's passed in a query string.</span></span> <span data-ttu-id="e5e16-220">Kód testuje, že hodnota není prázdná a že se jedná o celé číslo.</span><span class="sxs-lookup"><span data-stu-id="e5e16-220">The code tests that the value is not empty and that it's an integer.</span></span>

[!code-csharp[Main](validating-user-input-in-aspnet-web-pages-sites/samples/sample6.cs)]

<span data-ttu-id="e5e16-221">Všimněte si, že test je proveden, pokud žádost není odesláním formuláře (`if(!IsPost)`).</span><span class="sxs-lookup"><span data-stu-id="e5e16-221">Notice that the test is performed when the request is not a form submission (`if(!IsPost)`).</span></span> <span data-ttu-id="e5e16-222">Tento test by byl splněn při prvním vyžádání stránky, ale ne v případě, kdy je žádost odeslána formuláři.</span><span class="sxs-lookup"><span data-stu-id="e5e16-222">This test would pass the first time that the page is requested, but not when the request is a form submission.</span></span>

<span data-ttu-id="e5e16-223">Chcete-li zobrazit tuto chybu, můžete přidat chybu do seznamu chyb ověřování voláním `Validation.AddFormError("message")`.</span><span class="sxs-lookup"><span data-stu-id="e5e16-223">To display this error, you can add the error to the list of validation errors by calling `Validation.AddFormError("message")`.</span></span> <span data-ttu-id="e5e16-224">Pokud stránka obsahuje volání metody `Html.ValidationSummary`, zobrazí se chyba podobně jako při ověřování vstupu uživatele.</span><span class="sxs-lookup"><span data-stu-id="e5e16-224">If the page contains a call to the `Html.ValidationSummary` method, the error is displayed there, just like a user-input validation error.</span></span>

<a id="AdditionalResources"></a>
## <a name="additional-resources"></a><span data-ttu-id="e5e16-225">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="e5e16-225">Additional Resources</span></span>

[<span data-ttu-id="e5e16-226">Práce s formuláři HTML na webech webových stránek ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e5e16-226">Working with HTML Forms in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkID=202892)

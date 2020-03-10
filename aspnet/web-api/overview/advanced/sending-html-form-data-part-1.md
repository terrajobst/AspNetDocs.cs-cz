---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: 'Posílání dat formuláře HTML ve webovém rozhraní API ASP.NET: form-urlencoded data – ASP.NET 4. x'
author: MikeWasson
description: Tento článek popisuje, jak publikovat data urlencoded formuláře do kontroleru webového rozhraní API s ASP.NET 4. x.
ms.author: riande
ms.date: 06/15/2012
ms.custom: seoapril2019
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: 7243069dbd8051b1374ed6e0112c273b8fe26f61
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557601"
---
# <a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a><span data-ttu-id="78195-103">Posílání dat formuláře HTML ve webovém rozhraní API ASP.NET: form-urlencoded data</span><span class="sxs-lookup"><span data-stu-id="78195-103">Sending HTML Form Data in ASP.NET Web API: Form-urlencoded Data</span></span>

<span data-ttu-id="78195-104">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="78195-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-1-form-urlencoded-data"></a><span data-ttu-id="78195-105">1\. část: forma-urlencoded data</span><span class="sxs-lookup"><span data-stu-id="78195-105">Part 1: Form-urlencoded Data</span></span>

<span data-ttu-id="78195-106">Tento článek ukazuje, jak odesílat data urlencoded formuláře do kontroleru webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="78195-106">This article shows how to post form-urlencoded data to a Web API controller.</span></span>

- [<span data-ttu-id="78195-107">Přehled formulářů HTML</span><span class="sxs-lookup"><span data-stu-id="78195-107">Overview of HTML Forms</span></span>](#overview_of_html_forms)
- [<span data-ttu-id="78195-108">Posílání složitých typů</span><span class="sxs-lookup"><span data-stu-id="78195-108">Sending Complex Types</span></span>](#sending_complex_types)
- [<span data-ttu-id="78195-109">Posílání dat formuláře prostřednictvím AJAX</span><span class="sxs-lookup"><span data-stu-id="78195-109">Sending Form Data via AJAX</span></span>](#sending_form_data_via_ajax)
- [<span data-ttu-id="78195-110">Posílání jednoduchých typů</span><span class="sxs-lookup"><span data-stu-id="78195-110">Sending Simple Types</span></span>](#sending_simple_types)

> [!NOTE]
> <span data-ttu-id="78195-111">[Stáhněte dokončený projekt](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span><span class="sxs-lookup"><span data-stu-id="78195-111">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span></span>

<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a><span data-ttu-id="78195-112">Přehled formulářů HTML</span><span class="sxs-lookup"><span data-stu-id="78195-112">Overview of HTML Forms</span></span>

<span data-ttu-id="78195-113">Formuláře HTML používají k odesílání dat na server buď GET, nebo POST.</span><span class="sxs-lookup"><span data-stu-id="78195-113">HTML forms use either GET or POST to send data to the server.</span></span> <span data-ttu-id="78195-114">Atribut **Method** prvku **Form** poskytuje metodu http:</span><span class="sxs-lookup"><span data-stu-id="78195-114">The **method** attribute of the **form** element gives the HTTP method:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

<span data-ttu-id="78195-115">Výchozí metoda je GET.</span><span class="sxs-lookup"><span data-stu-id="78195-115">The default method is GET.</span></span> <span data-ttu-id="78195-116">Pokud formulář používá GET, data formuláře jsou v identifikátoru URI kódována jako řetězec dotazu.</span><span class="sxs-lookup"><span data-stu-id="78195-116">If the form uses GET, the form data is encoded in the URI as a query string.</span></span> <span data-ttu-id="78195-117">Pokud formulář používá POST, data formuláře se umístí do textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="78195-117">If the form uses POST, the form data is placed in the request body.</span></span> <span data-ttu-id="78195-118">V případě publikovaných dat určuje atribut **Enctype** formát textu žádosti:</span><span class="sxs-lookup"><span data-stu-id="78195-118">For POSTed data, the **enctype** attribute specifies the format of the request body:</span></span>

| <span data-ttu-id="78195-119">enctype</span><span class="sxs-lookup"><span data-stu-id="78195-119">enctype</span></span> | <span data-ttu-id="78195-120">Popis</span><span class="sxs-lookup"><span data-stu-id="78195-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="78195-121">Application/x-www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="78195-121">application/x-www-form-urlencoded</span></span> | <span data-ttu-id="78195-122">Data formuláře jsou kódována jako páry název-hodnota, podobně jako řetězec dotazu identifikátoru URI.</span><span class="sxs-lookup"><span data-stu-id="78195-122">Form data is encoded as name/value pairs, similar to a URI query string.</span></span> <span data-ttu-id="78195-123">Toto je výchozí formát pro POST.</span><span class="sxs-lookup"><span data-stu-id="78195-123">This is the default format for POST.</span></span> |
| <span data-ttu-id="78195-124">multipart/form-data</span><span class="sxs-lookup"><span data-stu-id="78195-124">multipart/form-data</span></span> | <span data-ttu-id="78195-125">Data formuláře se kódují jako zpráva MIME s více částmi.</span><span class="sxs-lookup"><span data-stu-id="78195-125">Form data is encoded as a multipart MIME message.</span></span> <span data-ttu-id="78195-126">Tento formát použijte při nahrávání souboru na server.</span><span class="sxs-lookup"><span data-stu-id="78195-126">Use this format if you are uploading a file to the server.</span></span> |

<span data-ttu-id="78195-127">Část 1 tohoto článku se zabývá formátem x-www-form-urlencoded.</span><span class="sxs-lookup"><span data-stu-id="78195-127">Part 1 of this article looks at x-www-form-urlencoded format.</span></span> <span data-ttu-id="78195-128">[Část 2](sending-html-form-data-part-2.md) popisuje MIME s více částmi.</span><span class="sxs-lookup"><span data-stu-id="78195-128">[Part 2](sending-html-form-data-part-2.md) describes multipart MIME.</span></span>

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a><span data-ttu-id="78195-129">Posílání složitých typů</span><span class="sxs-lookup"><span data-stu-id="78195-129">Sending Complex Types</span></span>

<span data-ttu-id="78195-130">Obvykle odešlete složitý typ složený z hodnot pořízených z několika ovládacích prvků Form.</span><span class="sxs-lookup"><span data-stu-id="78195-130">Typically, you will send a complex type, composed of values taken from several form controls.</span></span> <span data-ttu-id="78195-131">Vezměte v úvahu následující model, který představuje aktualizaci stavu:</span><span class="sxs-lookup"><span data-stu-id="78195-131">Consider the following model that represents a status update:</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

<span data-ttu-id="78195-132">Tady je kontroler webového rozhraní API, který přijímá objekt `Update` prostřednictvím POST.</span><span class="sxs-lookup"><span data-stu-id="78195-132">Here is a Web API controller that accepts an `Update` object via POST.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="78195-133">Tento kontroler používá [směrování na základě akcí](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), takže šablona trasy je &quot;API/{Controller}/{Action}/{id}&quot;.</span><span class="sxs-lookup"><span data-stu-id="78195-133">This controller uses [action-based routing](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), so the route template is &quot;api/{controller}/{action}/{id}&quot;.</span></span> <span data-ttu-id="78195-134">Klient odešle data do &quot;/API/Updates/Complex&quot;.</span><span class="sxs-lookup"><span data-stu-id="78195-134">The client will post the data to &quot;/api/updates/complex&quot;.</span></span>

<span data-ttu-id="78195-135">Nyní napíšeme formulář HTML pro uživatele, kteří odešlou aktualizaci stavu.</span><span class="sxs-lookup"><span data-stu-id="78195-135">Now let's write an HTML form for users to submit a status update.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

<span data-ttu-id="78195-136">Všimněte si, že atribut **Action** formuláře je identifikátor URI naší akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="78195-136">Notice that the **action** attribute on the form is the URI of our controller action.</span></span> <span data-ttu-id="78195-137">Zde je formulář s některými hodnotami zadanými v:</span><span class="sxs-lookup"><span data-stu-id="78195-137">Here is the form with some values entered in:</span></span>

![](sending-html-form-data-part-1/_static/image1.png)

<span data-ttu-id="78195-138">Když uživatel klikne na Odeslat, prohlížeč odešle požadavek HTTP podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="78195-138">When the user clicks Submit, the browser sends an HTTP request similar to the following:</span></span>

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

<span data-ttu-id="78195-139">Všimněte si, že tělo žádosti obsahuje data formuláře formátovaná jako páry název-hodnota.</span><span class="sxs-lookup"><span data-stu-id="78195-139">Notice that the request body contains the form data, formatted as name/value pairs.</span></span> <span data-ttu-id="78195-140">Webové rozhraní API automaticky převede páry název/hodnota na instanci třídy `Update`.</span><span class="sxs-lookup"><span data-stu-id="78195-140">Web API automatically converts the name/value pairs into an instance of the `Update` class.</span></span>

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a><span data-ttu-id="78195-141">Posílání dat formuláře prostřednictvím AJAX</span><span class="sxs-lookup"><span data-stu-id="78195-141">Sending Form Data via AJAX</span></span>

<span data-ttu-id="78195-142">Když uživatel formulář odešle, prohlížeč přejde pryč z aktuální stránky a vykreslí text zprávy s odpovědí.</span><span class="sxs-lookup"><span data-stu-id="78195-142">When a user submits a form, the browser navigates away from the current page and renders the body of the response message.</span></span> <span data-ttu-id="78195-143">To je v pořádku, když je odpověď stránka HTML.</span><span class="sxs-lookup"><span data-stu-id="78195-143">That's OK when the response is an HTML page.</span></span> <span data-ttu-id="78195-144">V případě webového rozhraní API je však tělo odpovědi obvykle prázdné nebo obsahuje strukturovaná data, jako je například JSON.</span><span class="sxs-lookup"><span data-stu-id="78195-144">With a web API, however, the response body is usually either empty or contains structured data, such as JSON.</span></span> <span data-ttu-id="78195-145">V takovém případě je vhodnější odesílat data formuláře pomocí požadavku AJAX, aby stránka mohla zpracovat odpověď.</span><span class="sxs-lookup"><span data-stu-id="78195-145">In that case, it makes more sense to send the form data using an AJAX request, so that the page can process the response.</span></span>

<span data-ttu-id="78195-146">Následující kód ukazuje, jak publikovat data formuláře pomocí jQuery.</span><span class="sxs-lookup"><span data-stu-id="78195-146">The following code shows how to post form data using jQuery.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

<span data-ttu-id="78195-147">Funkce jQuery pro **odeslání** nahrazuje akci formuláře novou funkcí.</span><span class="sxs-lookup"><span data-stu-id="78195-147">The jQuery **submit** function replaces the form action with a new function.</span></span> <span data-ttu-id="78195-148">Tím se přepíše výchozí chování tlačítka Odeslat.</span><span class="sxs-lookup"><span data-stu-id="78195-148">This overrides the default behavior of the Submit button.</span></span> <span data-ttu-id="78195-149">Funkce **serializace** serializace data formuláře na páry název-hodnota.</span><span class="sxs-lookup"><span data-stu-id="78195-149">The **serialize** function serializes the form data into name/value pairs.</span></span> <span data-ttu-id="78195-150">Chcete-li odeslat data formuláře na server, zavolejte `$.post()`.</span><span class="sxs-lookup"><span data-stu-id="78195-150">To send the form data to the server, call `$.post()`.</span></span>

<span data-ttu-id="78195-151">Po dokončení žádosti zobrazí obslužná rutina `.success()` nebo `.error()` příslušnou zprávu uživateli.</span><span class="sxs-lookup"><span data-stu-id="78195-151">When the request completes, the `.success()` or `.error()` handler displays an appropriate message to the user.</span></span>

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a><span data-ttu-id="78195-152">Posílání jednoduchých typů</span><span class="sxs-lookup"><span data-stu-id="78195-152">Sending Simple Types</span></span>

<span data-ttu-id="78195-153">V předchozích částech jsme poslali komplexní typ, který webové rozhraní API deserializovat na instanci třídy modelu.</span><span class="sxs-lookup"><span data-stu-id="78195-153">In the previous sections, we sent a complex type, which Web API deserialized to an instance of a model class.</span></span> <span data-ttu-id="78195-154">Můžete také odesílat jednoduché typy, jako je například řetězec.</span><span class="sxs-lookup"><span data-stu-id="78195-154">You can also send simple types, such as a string.</span></span>

> [!NOTE]
> <span data-ttu-id="78195-155">Před odesláním jednoduchého typu zvažte místo toho zabalení hodnoty do komplexního typu.</span><span class="sxs-lookup"><span data-stu-id="78195-155">Before sending a simple type, consider wrapping the value in a complex type instead.</span></span> <span data-ttu-id="78195-156">To vám dává výhody ověřování modelu na straně serveru a usnadňuje tak rozšiřování modelu v případě potřeby.</span><span class="sxs-lookup"><span data-stu-id="78195-156">This gives you the benefits of model validation on the server side, and makes it easier to extend your model if needed.</span></span>

<span data-ttu-id="78195-157">Základní kroky pro odeslání jednoduchého typu jsou stejné, ale existují dva malé rozdíly.</span><span class="sxs-lookup"><span data-stu-id="78195-157">The basic steps to send a simple type are the same, but there are two subtle differences.</span></span> <span data-ttu-id="78195-158">Nejprve je třeba v kontroleru vyplnit název parametru atributem **FromBody** .</span><span class="sxs-lookup"><span data-stu-id="78195-158">First, in the controller, you must decorate the parameter name with the **FromBody** attribute.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

<span data-ttu-id="78195-159">Ve výchozím nastavení se webové rozhraní API pokusí získat jednoduché typy z identifikátoru URI požadavku.</span><span class="sxs-lookup"><span data-stu-id="78195-159">By default, Web API tries to get simple types from the request URI.</span></span> <span data-ttu-id="78195-160">Atribut **FromBody** oznamuje webovému rozhraní API načtení hodnoty z textu žádosti.</span><span class="sxs-lookup"><span data-stu-id="78195-160">The **FromBody** attribute tells Web API to read the value from the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="78195-161">Webové rozhraní API čte text odpovědi nejvíce jednou, takže z textu žádosti může pocházet pouze jeden parametr akce.</span><span class="sxs-lookup"><span data-stu-id="78195-161">Web API reads the response body at most once, so only one parameter of an action can come from the request body.</span></span> <span data-ttu-id="78195-162">Pokud potřebujete získat více hodnot z textu žádosti, definujte komplexní typ.</span><span class="sxs-lookup"><span data-stu-id="78195-162">If you need to get multiple values from the request body, define a complex type.</span></span>

<span data-ttu-id="78195-163">Druhý klient potřebuje odeslat hodnotu v následujícím formátu:</span><span class="sxs-lookup"><span data-stu-id="78195-163">Second, the client needs to send the value with the following format:</span></span>

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

<span data-ttu-id="78195-164">Konkrétně část názvu dvojice název/hodnota musí být pro jednoduchý typ prázdná.</span><span class="sxs-lookup"><span data-stu-id="78195-164">Specifically, the name portion of the name/value pair must be empty for a simple type.</span></span> <span data-ttu-id="78195-165">Ne všechny prohlížeče tuto podporu podporují pro formuláře HTML, ale tento formát vytvoříte ve skriptu následujícím způsobem:</span><span class="sxs-lookup"><span data-stu-id="78195-165">Not all browsers support this for HTML forms, but you create this format in script as follows:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

<span data-ttu-id="78195-166">Tady je příklad formuláře:</span><span class="sxs-lookup"><span data-stu-id="78195-166">Here is an example form:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

<span data-ttu-id="78195-167">A zde je skript pro odeslání hodnoty formuláře.</span><span class="sxs-lookup"><span data-stu-id="78195-167">And here is the script to submit the form value.</span></span> <span data-ttu-id="78195-168">Jediným rozdílem z předchozího skriptu je argument předaný do funkce **post** .</span><span class="sxs-lookup"><span data-stu-id="78195-168">The only difference from the previous script is the argument passed into the **post** function.</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

<span data-ttu-id="78195-169">Stejný přístup můžete použít k odeslání pole jednoduchých typů:</span><span class="sxs-lookup"><span data-stu-id="78195-169">You can use the same approach to send an array of simple types:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a><span data-ttu-id="78195-170">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="78195-170">Additional Resources</span></span>

[<span data-ttu-id="78195-171">Část 2: nahrání souboru a MIME s více částmi</span><span class="sxs-lookup"><span data-stu-id="78195-171">Part 2: File Upload and Multipart MIME</span></span>](sending-html-form-data-part-2.md)

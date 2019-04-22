---
uid: web-api/overview/advanced/sending-html-form-data-part-1
title: 'Posílání dat formulářů HTML ve webovém rozhraní API technologie ASP.NET: Data formuláře kódovaná – ASP.NET 4.x'
author: MikeWasson
description: Tento článek ukazuje, jak publikovat data formuláře kódovaná do kontroleru webového rozhraní API v ASP.NET 4.x
ms.author: riande
ms.date: 06/15/2012
ms.custom: seoapril2019
ms.assetid: 585351c4-809a-4bf5-bcbe-35d624f565fe
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-1
msc.type: authoredcontent
ms.openlocfilehash: fb0309af11910125943737ebb721b356b7bd08bc
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/17/2019
ms.locfileid: "59418297"
---
# <a name="sending-html-form-data-in-aspnet-web-api-form-urlencoded-data"></a><span data-ttu-id="6c1cd-103">Posílání dat formulářů HTML ve webovém rozhraní API technologie ASP.NET: Data formuláře kódovaná pomocí adresy URL</span><span class="sxs-lookup"><span data-stu-id="6c1cd-103">Sending HTML Form Data in ASP.NET Web API: Form-urlencoded Data</span></span>

<span data-ttu-id="6c1cd-104">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6c1cd-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-1-form-urlencoded-data"></a><span data-ttu-id="6c1cd-105">Část 1: Data formuláře kódovaná pomocí adresy URL</span><span class="sxs-lookup"><span data-stu-id="6c1cd-105">Part 1: Form-urlencoded Data</span></span>

<span data-ttu-id="6c1cd-106">Tento článek ukazuje, jak publikovat data formuláře kódovaná do kontroleru webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-106">This article shows how to post form-urlencoded data to a Web API controller.</span></span>

- [<span data-ttu-id="6c1cd-107">Přehled formulářů HTML</span><span class="sxs-lookup"><span data-stu-id="6c1cd-107">Overview of HTML Forms</span></span>](#overview_of_html_forms)
- [<span data-ttu-id="6c1cd-108">Odesílání komplexních typů</span><span class="sxs-lookup"><span data-stu-id="6c1cd-108">Sending Complex Types</span></span>](#sending_complex_types)
- [<span data-ttu-id="6c1cd-109">Posílání dat formulářů prostřednictvím AJAX</span><span class="sxs-lookup"><span data-stu-id="6c1cd-109">Sending Form Data via AJAX</span></span>](#sending_form_data_via_ajax)
- [<span data-ttu-id="6c1cd-110">Odesílání jednoduché typy</span><span class="sxs-lookup"><span data-stu-id="6c1cd-110">Sending Simple Types</span></span>](#sending_simple_types)

> [!NOTE]
> <span data-ttu-id="6c1cd-111">[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span><span class="sxs-lookup"><span data-stu-id="6c1cd-111">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-Sending-a6f9d007).</span></span>


<a id="overview_of_html_forms"></a>
## <a name="overview-of-html-forms"></a><span data-ttu-id="6c1cd-112">Přehled formulářů HTML</span><span class="sxs-lookup"><span data-stu-id="6c1cd-112">Overview of HTML Forms</span></span>

<span data-ttu-id="6c1cd-113">Používání formulářů HTML GET nebo POST k odesílání dat na server.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-113">HTML forms use either GET or POST to send data to the server.</span></span> <span data-ttu-id="6c1cd-114">**Metoda** atribut **formuláře** element poskytuje metoda HTTP:</span><span class="sxs-lookup"><span data-stu-id="6c1cd-114">The **method** attribute of the **form** element gives the HTTP method:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample1.html)]

<span data-ttu-id="6c1cd-115">Výchozí metodou je GET.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-115">The default method is GET.</span></span> <span data-ttu-id="6c1cd-116">Pokud formulář používá získáte, formuláře, který dat je zakódovaný v identifikátoru URI jako řetězec dotazu.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-116">If the form uses GET, the form data is encoded in the URI as a query string.</span></span> <span data-ttu-id="6c1cd-117">Pokud formulář používá metodu POST, data formuláře je umístěn v textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-117">If the form uses POST, the form data is placed in the request body.</span></span> <span data-ttu-id="6c1cd-118">Pro zaúčtované data **enctype** atribut určuje formát těla požadavku:</span><span class="sxs-lookup"><span data-stu-id="6c1cd-118">For POSTed data, the **enctype** attribute specifies the format of the request body:</span></span>

| <span data-ttu-id="6c1cd-119">enctype</span><span class="sxs-lookup"><span data-stu-id="6c1cd-119">enctype</span></span> | <span data-ttu-id="6c1cd-120">Popis</span><span class="sxs-lookup"><span data-stu-id="6c1cd-120">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6c1cd-121">Application/x--www-form-urlencoded</span><span class="sxs-lookup"><span data-stu-id="6c1cd-121">application/x-www-form-urlencoded</span></span> | <span data-ttu-id="6c1cd-122">Data formuláře kódovaná jako dvojice název/hodnota, podobně jako řetězce dotazu URI.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-122">Form data is encoded as name/value pairs, similar to a URI query string.</span></span> <span data-ttu-id="6c1cd-123">Toto je výchozí formát pro metodu POST.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-123">This is the default format for POST.</span></span> |
| <span data-ttu-id="6c1cd-124">multipart/formuláře data</span><span class="sxs-lookup"><span data-stu-id="6c1cd-124">multipart/form-data</span></span> | <span data-ttu-id="6c1cd-125">Data formuláře kódovaná jako vícedílné zprávě standardu MIME.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-125">Form data is encoded as a multipart MIME message.</span></span> <span data-ttu-id="6c1cd-126">Pokud nahráváte soubor na server, použijte tento formát.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-126">Use this format if you are uploading a file to the server.</span></span> |

<span data-ttu-id="6c1cd-127">Část 1 tohoto článku bude vypadat ve formátu x--www-form-urlencoded.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-127">Part 1 of this article looks at x-www-form-urlencoded format.</span></span> <span data-ttu-id="6c1cd-128">[Část 2](sending-html-form-data-part-2.md) popisuje vícedílné zprávy standardu MIME.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-128">[Part 2](sending-html-form-data-part-2.md) describes multipart MIME.</span></span>

<a id="sending_complex_types"></a>
## <a name="sending-complex-types"></a><span data-ttu-id="6c1cd-129">Odesílání komplexních typů</span><span class="sxs-lookup"><span data-stu-id="6c1cd-129">Sending Complex Types</span></span>

<span data-ttu-id="6c1cd-130">Obvykle se odesílají komplexní typ, skládající se z hodnot z několika ovládacích prvků formuláře.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-130">Typically, you will send a complex type, composed of values taken from several form controls.</span></span> <span data-ttu-id="6c1cd-131">Vezměte v úvahu následující model, který představuje stav aktualizace:</span><span class="sxs-lookup"><span data-stu-id="6c1cd-131">Consider the following model that represents a status update:</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample2.cs)]

<span data-ttu-id="6c1cd-132">Tady je kontroler Web API, která přijímá `Update` objekt přes POST.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-132">Here is a Web API controller that accepts an `Update` object via POST.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="6c1cd-133">Tento kontroler používá [směrování na základě akce](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), takže je šablona trasy &quot;rozhraní api / {controller} / {action} / {id}&quot;.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-133">This controller uses [action-based routing](../web-api-routing-and-actions/routing-in-aspnet-web-api.md#routing_by_action_name), so the route template is &quot;api/{controller}/{action}/{id}&quot;.</span></span> <span data-ttu-id="6c1cd-134">Klient bude publikovat data, která mají &quot;/api/updates/complex&quot;.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-134">The client will post the data to &quot;/api/updates/complex&quot;.</span></span>


<span data-ttu-id="6c1cd-135">Nyní napíšeme formuláře HTML pro uživatele k odeslání aktualizace stavu.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-135">Now let's write an HTML form for users to submit a status update.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample4.html)]

<span data-ttu-id="6c1cd-136">Všimněte si, **akce** atributu ve formuláři je identifikátor URI naší akce kontroleru.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-136">Notice that the **action** attribute on the form is the URI of our controller action.</span></span> <span data-ttu-id="6c1cd-137">Tady je formulář s některé hodnoty zadané v:</span><span class="sxs-lookup"><span data-stu-id="6c1cd-137">Here is the form with some values entered in:</span></span>

![](sending-html-form-data-part-1/_static/image1.png)

<span data-ttu-id="6c1cd-138">Když uživatel klepne na tlačítko Odeslat, prohlížeč odešle požadavek HTTP podobný následujícímu:</span><span class="sxs-lookup"><span data-stu-id="6c1cd-138">When the user clicks Submit, the browser sends an HTTP request similar to the following:</span></span>

[!code-console[Main](sending-html-form-data-part-1/samples/sample5.cmd)]

<span data-ttu-id="6c1cd-139">Všimněte si, že text požadavku obsahuje data formuláře, formátovaný jako dvojice název/hodnota.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-139">Notice that the request body contains the form data, formatted as name/value pairs.</span></span> <span data-ttu-id="6c1cd-140">Webové rozhraní API automaticky převede dvojice název/hodnota do instance `Update` třídy.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-140">Web API automatically converts the name/value pairs into an instance of the `Update` class.</span></span>

<a id="sending_form_data_via_ajax"></a>
## <a name="sending-form-data-via-ajax"></a><span data-ttu-id="6c1cd-141">Posílání dat formulářů prostřednictvím AJAX</span><span class="sxs-lookup"><span data-stu-id="6c1cd-141">Sending Form Data via AJAX</span></span>

<span data-ttu-id="6c1cd-142">Když uživatel odešle formulář, prohlížeči přejde mimo aktuální stránku a vykreslí tělo zprávy s odpovědí.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-142">When a user submits a form, the browser navigates away from the current page and renders the body of the response message.</span></span> <span data-ttu-id="6c1cd-143">Který je v pořádku. Pokud je odpověď na stránku HTML.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-143">That's OK when the response is an HTML page.</span></span> <span data-ttu-id="6c1cd-144">S webovým rozhraním API, ale text odpovědi je obvykle buď prázdná, nebo obsahuje strukturovaná data, jako je například JSON.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-144">With a web API, however, the response body is usually either empty or contains structured data, such as JSON.</span></span> <span data-ttu-id="6c1cd-145">V takovém případě je vhodnější k odesílání dat formuláře pomocí AJAX vyžádání, tak, aby stránky mohou zpracovat odpověď.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-145">In that case, it makes more sense to send the form data using an AJAX request, so that the page can process the response.</span></span>

<span data-ttu-id="6c1cd-146">Následující kód ukazuje, jak publikovat data formuláře pomocí jQuery.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-146">The following code shows how to post form data using jQuery.</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample6.html)]

<span data-ttu-id="6c1cd-147">JQuery **odeslat** funkce nahradí akce formuláře s novou funkci.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-147">The jQuery **submit** function replaces the form action with a new function.</span></span> <span data-ttu-id="6c1cd-148">Tím se přepíše výchozí chování tlačítka pro odeslání.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-148">This overrides the default behavior of the Submit button.</span></span> <span data-ttu-id="6c1cd-149">**Serializovat** funkce serializuje data formuláře na páry název/hodnota.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-149">The **serialize** function serializes the form data into name/value pairs.</span></span> <span data-ttu-id="6c1cd-150">Chcete-li data formuláře odeslat k serveru, zavolejte `$.post()`.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-150">To send the form data to the server, call `$.post()`.</span></span>

<span data-ttu-id="6c1cd-151">Po dokončení žádosti `.success()` nebo `.error()` obslužné rutiny zobrazí odpovídající zprávu pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-151">When the request completes, the `.success()` or `.error()` handler displays an appropriate message to the user.</span></span>

![](sending-html-form-data-part-1/_static/image2.png)

<a id="sending_simple_types"></a>
## <a name="sending-simple-types"></a><span data-ttu-id="6c1cd-152">Odesílání jednoduché typy</span><span class="sxs-lookup"><span data-stu-id="6c1cd-152">Sending Simple Types</span></span>

<span data-ttu-id="6c1cd-153">V předchozích částech jsme vám poslali komplexní typ, který webového rozhraní API se deserializovala na instanci třídy modelu.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-153">In the previous sections, we sent a complex type, which Web API deserialized to an instance of a model class.</span></span> <span data-ttu-id="6c1cd-154">Můžete také odeslat jednoduché typy, jako je například řetězec.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-154">You can also send simple types, such as a string.</span></span>

> [!NOTE]
> <span data-ttu-id="6c1cd-155">Před odesláním jednoduchého typu, zvažte možnost uzavřít hodnotu v komplexního typu. místo toho.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-155">Before sending a simple type, consider wrapping the value in a complex type instead.</span></span> <span data-ttu-id="6c1cd-156">To poskytuje výhody model ověření na straně serveru a usnadňuje rozšíření modelu, v případě potřeby.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-156">This gives you the benefits of model validation on the server side, and makes it easier to extend your model if needed.</span></span>


<span data-ttu-id="6c1cd-157">Toto jsou základní kroky k odeslání jednoduchý typ stejný, ale existují dva drobné rozdíly.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-157">The basic steps to send a simple type are the same, but there are two subtle differences.</span></span> <span data-ttu-id="6c1cd-158">V kontroleru, musíte nejprve uspořádání název parametru se **FromBody** atribut.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-158">First, in the controller, you must decorate the parameter name with the **FromBody** attribute.</span></span>

[!code-csharp[Main](sending-html-form-data-part-1/samples/sample7.cs?highlight=3)]

<span data-ttu-id="6c1cd-159">Ve výchozím nastavení se webové rozhraní API pokusí získat jednoduché typy z identifikátoru URI požadavku.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-159">By default, Web API tries to get simple types from the request URI.</span></span> <span data-ttu-id="6c1cd-160">**FromBody** atribut oznamuje webového rozhraní API načíst hodnotu z textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-160">The **FromBody** attribute tells Web API to read the value from the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="6c1cd-161">Webové rozhraní API přečte text odpovědi nejvýše jednou, takže pouze jeden parametr akce můžou pocházet z textu požadavku.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-161">Web API reads the response body at most once, so only one parameter of an action can come from the request body.</span></span> <span data-ttu-id="6c1cd-162">Pokud je potřeba získat několik hodnot z textu požadavku, definice komplexního typu.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-162">If you need to get multiple values from the request body, define a complex type.</span></span>


<span data-ttu-id="6c1cd-163">Za druhé klient musí k odeslání hodnoty v následujícím formátu:</span><span class="sxs-lookup"><span data-stu-id="6c1cd-163">Second, the client needs to send the value with the following format:</span></span>

[!code-xml[Main](sending-html-form-data-part-1/samples/sample8.xml)]

<span data-ttu-id="6c1cd-164">Konkrétně část název z dvojice název/hodnota musí být prázdná pro jednoduchý typ.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-164">Specifically, the name portion of the name/value pair must be empty for a simple type.</span></span> <span data-ttu-id="6c1cd-165">Některé prohlížeče nepodporují to pro formuláře HTML, ale následujícím způsobem vytvořte tento formát ve skriptu:</span><span class="sxs-lookup"><span data-stu-id="6c1cd-165">Not all browsers support this for HTML forms, but you create this format in script as follows:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample9.js)]

<span data-ttu-id="6c1cd-166">Tady je ukázkový formulář:</span><span class="sxs-lookup"><span data-stu-id="6c1cd-166">Here is an example form:</span></span>

[!code-html[Main](sending-html-form-data-part-1/samples/sample10.html)]

<span data-ttu-id="6c1cd-167">A tady je skript, který chcete odeslat hodnota formuláře.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-167">And here is the script to submit the form value.</span></span> <span data-ttu-id="6c1cd-168">Jediný rozdíl oproti předchozí skript je argument předaný do **příspěvku** funkce.</span><span class="sxs-lookup"><span data-stu-id="6c1cd-168">The only difference from the previous script is the argument passed into the **post** function.</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample11.js?highlight=2)]

<span data-ttu-id="6c1cd-169">Stejný přístup můžete použít k odesílání pole jednoduchých typů:</span><span class="sxs-lookup"><span data-stu-id="6c1cd-169">You can use the same approach to send an array of simple types:</span></span>

[!code-javascript[Main](sending-html-form-data-part-1/samples/sample12.js)]

## <a name="additional-resources"></a><span data-ttu-id="6c1cd-170">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="6c1cd-170">Additional Resources</span></span>

[<span data-ttu-id="6c1cd-171">Část 2: Nahrání souboru a vícedílné zprávy standardu MIME</span><span class="sxs-lookup"><span data-stu-id="6c1cd-171">Part 2: File Upload and Multipart MIME</span></span>](sending-html-form-data-part-2.md)

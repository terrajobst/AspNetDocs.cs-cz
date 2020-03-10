---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: 'Posílání dat formuláře HTML ve webovém rozhraní API ASP.NET: nahrání souboru a MIME-ASP.NET 4. x'
author: MikeWasson
description: V tomto kurzu se dozvíte, jak nahrát soubory do webového rozhraní API. Popisuje také postup zpracování dat MIME v částech.
ms.author: riande
ms.date: 06/21/2012
ms.custom: seoapril2019
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: f5aaebb96f631dfb6b0da1fbca96cd93a6a7fe2d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557566"
---
# <a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a><span data-ttu-id="35d05-104">Posílání dat formuláře HTML ve webovém rozhraní API ASP.NET: nahrání souboru a MIME s více částmi</span><span class="sxs-lookup"><span data-stu-id="35d05-104">Sending HTML Form Data in ASP.NET Web API: File Upload and Multipart MIME</span></span>

<span data-ttu-id="35d05-105">o [Jan Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="35d05-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-2-file-upload-and-multipart-mime"></a><span data-ttu-id="35d05-106">Část 2: nahrání souboru a MIME s více částmi</span><span class="sxs-lookup"><span data-stu-id="35d05-106">Part 2: File Upload and Multipart MIME</span></span>

<span data-ttu-id="35d05-107">V tomto kurzu se dozvíte, jak nahrát soubory do webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="35d05-107">This tutorial shows how to upload files to a web API.</span></span> <span data-ttu-id="35d05-108">Popisuje také postup zpracování dat MIME v částech.</span><span class="sxs-lookup"><span data-stu-id="35d05-108">It also describes how to process multipart MIME data.</span></span>

> [!NOTE]
> <span data-ttu-id="35d05-109">[Stáhněte dokončený projekt](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span><span class="sxs-lookup"><span data-stu-id="35d05-109">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span></span>

<span data-ttu-id="35d05-110">Tady je příklad formuláře HTML pro nahrání souboru:</span><span class="sxs-lookup"><span data-stu-id="35d05-110">Here is an example of an HTML form for uploading a file:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

<span data-ttu-id="35d05-111">Tento formulář obsahuje ovládací prvek textové zadání a ovládací prvek vstupu do souboru.</span><span class="sxs-lookup"><span data-stu-id="35d05-111">This form contains a text input control and a file input control.</span></span> <span data-ttu-id="35d05-112">Pokud formulář obsahuje ovládací prvek vstupního souboru, atribut **Enctype** by měl vždy &quot;multipart/form-data&quot;, který určuje, že formulář bude odeslán jako zpráva MIME s více částmi.</span><span class="sxs-lookup"><span data-stu-id="35d05-112">When a form contains a file input control, the **enctype** attribute should always be &quot;multipart/form-data&quot;, which specifies that the form will be sent as a multipart MIME message.</span></span>

<span data-ttu-id="35d05-113">Formát zprávy MIME s více částmi je nejjednodušší pochopit tím, že se podíváte na příklad požadavku:</span><span class="sxs-lookup"><span data-stu-id="35d05-113">The format of a multipart MIME message is easiest to understand by looking at an example request:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

<span data-ttu-id="35d05-114">Tato zpráva je rozdělena na dvě *části*, jednu pro každý ovládací prvek formuláře.</span><span class="sxs-lookup"><span data-stu-id="35d05-114">This message is divided into two *parts*, one for each form control.</span></span> <span data-ttu-id="35d05-115">Hranice součásti jsou označeny řádky, které začínají pomlčkami.</span><span class="sxs-lookup"><span data-stu-id="35d05-115">Part boundaries are indicated by the lines that start with dashes.</span></span>

> [!NOTE]
> <span data-ttu-id="35d05-116">Hranice součásti zahrnuje náhodnou součást (&quot;41184676334&quot;), aby se zajistilo, že se řetězec hranice omylem neobjeví uvnitř části zprávy.</span><span class="sxs-lookup"><span data-stu-id="35d05-116">The part boundary includes a random component (&quot;41184676334&quot;) to ensure that the boundary string does not accidentally appear inside a message part.</span></span>

<span data-ttu-id="35d05-117">Každá část zprávy obsahuje jednu nebo více hlaviček následovaných obsahem části.</span><span class="sxs-lookup"><span data-stu-id="35d05-117">Each message part contains one or more headers, followed by the part contents.</span></span>

- <span data-ttu-id="35d05-118">Hlavička Content-Disposition obsahuje název ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="35d05-118">The Content-Disposition header includes the name of the control.</span></span> <span data-ttu-id="35d05-119">V případě souborů obsahuje také název souboru.</span><span class="sxs-lookup"><span data-stu-id="35d05-119">For files, it also contains the file name.</span></span>
- <span data-ttu-id="35d05-120">Hlavička Content-Type popisuje data v části.</span><span class="sxs-lookup"><span data-stu-id="35d05-120">The Content-Type header describes the data in the part.</span></span> <span data-ttu-id="35d05-121">Pokud je tato hlavička vynechána, výchozí hodnota je text/prostý.</span><span class="sxs-lookup"><span data-stu-id="35d05-121">If this header is omitted, the default is text/plain.</span></span>

<span data-ttu-id="35d05-122">V předchozím příkladu uživatel nahrál soubor s názvem GrandCanyon. jpg s typem obsahu image/jpeg; a hodnota textového vstupu byla &quot;letní dovolené&quot;.</span><span class="sxs-lookup"><span data-stu-id="35d05-122">In the previous example, the user uploaded a file named GrandCanyon.jpg, with content type image/jpeg; and the value of the text input was &quot;Summer Vacation&quot;.</span></span>

## <a name="file-upload"></a><span data-ttu-id="35d05-123">Nahrání souboru</span><span class="sxs-lookup"><span data-stu-id="35d05-123">File Upload</span></span>

<span data-ttu-id="35d05-124">Nyní se podívejme na kontroler webového rozhraní API, který čte soubory ze zprávy MIME s více částmi.</span><span class="sxs-lookup"><span data-stu-id="35d05-124">Now let's look at a Web API controller that reads files from a multipart MIME message.</span></span> <span data-ttu-id="35d05-125">Řadič bude soubory číst asynchronně.</span><span class="sxs-lookup"><span data-stu-id="35d05-125">The controller will read the files asynchronously.</span></span> <span data-ttu-id="35d05-126">Webové rozhraní API podporuje asynchronní akce pomocí [programovacího modelu založeného na úlohách](https://msdn.microsoft.com/library/dd460693.aspx).</span><span class="sxs-lookup"><span data-stu-id="35d05-126">Web API supports asynchronous actions using the [task-based programming model](https://msdn.microsoft.com/library/dd460693.aspx).</span></span> <span data-ttu-id="35d05-127">Nejdřív je zde kód, pokud cílíte .NET Framework 4,5, které podporují klíčová slova **Async** a **await** .</span><span class="sxs-lookup"><span data-stu-id="35d05-127">First, here is the code if you are targeting .NET Framework 4.5, which supports the **async** and **await** keywords.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

<span data-ttu-id="35d05-128">Všimněte si, že akce kontroleru nepřijímá žádné parametry.</span><span class="sxs-lookup"><span data-stu-id="35d05-128">Notice that the controller action does not take any parameters.</span></span> <span data-ttu-id="35d05-129">To je proto, že zpracováváme tělo žádosti v rámci akce bez vyvolání formátovacího modulu typu média.</span><span class="sxs-lookup"><span data-stu-id="35d05-129">That's because we process the request body inside the action, without invoking a media-type formatter.</span></span>

<span data-ttu-id="35d05-130">Metoda **IsMultipartContent** ověří, zda požadavek obsahuje zprávu MIME s více částmi.</span><span class="sxs-lookup"><span data-stu-id="35d05-130">The **IsMultipartContent** method checks whether the request contains a multipart MIME message.</span></span> <span data-ttu-id="35d05-131">V takovém případě kontroler vrátí stavový kód HTTP 415 (nepodporovaný typ média).</span><span class="sxs-lookup"><span data-stu-id="35d05-131">If not, the controller returns HTTP status code 415 (Unsupported Media Type).</span></span>

<span data-ttu-id="35d05-132">Třída **MultipartFormDataStreamProvider** je pomocný objekt, který přiděluje datové proudy souborů pro nahrané soubory.</span><span class="sxs-lookup"><span data-stu-id="35d05-132">The **MultipartFormDataStreamProvider** class is a helper object that allocates file streams for uploaded files.</span></span> <span data-ttu-id="35d05-133">Chcete-li si přečíst zprávu MIME s více částmi, zavolejte metodu **ReadAsMultipartAsync** .</span><span class="sxs-lookup"><span data-stu-id="35d05-133">To read the multipart MIME message, call the **ReadAsMultipartAsync** method.</span></span> <span data-ttu-id="35d05-134">Tato metoda extrahuje všechny části zprávy a zapisuje je do datových proudů poskytovaných **MultipartFormDataStreamProvider**.</span><span class="sxs-lookup"><span data-stu-id="35d05-134">This method extracts all of the message parts and writes them into the streams provided by the **MultipartFormDataStreamProvider**.</span></span>

<span data-ttu-id="35d05-135">Po dokončení metody můžete získat informace o souborech z vlastnosti **dat** , což je kolekce objektů **MultipartFileData** .</span><span class="sxs-lookup"><span data-stu-id="35d05-135">When the method completes, you can get information about the files from the **FileData** property, which is a collection of **MultipartFileData** objects.</span></span>

- <span data-ttu-id="35d05-136">**MultipartFileData. FileName** je název místního souboru na serveru, kde byl soubor uložen.</span><span class="sxs-lookup"><span data-stu-id="35d05-136">**MultipartFileData.FileName** is the local file name on the server, where the file was saved.</span></span>
- <span data-ttu-id="35d05-137">**MultipartFileData. Headers** obsahuje hlavičku části (*ne* hlavičku požadavku).</span><span class="sxs-lookup"><span data-stu-id="35d05-137">**MultipartFileData.Headers** contains the part header (*not* the request header).</span></span> <span data-ttu-id="35d05-138">Tuto možnost můžete použít pro přístup k obsahu\_k dispozici a k hlavičkám typu Content-Type.</span><span class="sxs-lookup"><span data-stu-id="35d05-138">You can use this to access the Content\_Disposition and Content-Type headers.</span></span>

<span data-ttu-id="35d05-139">Jak název naznačuje, **ReadAsMultipartAsync** je asynchronní metoda.</span><span class="sxs-lookup"><span data-stu-id="35d05-139">As the name suggests, **ReadAsMultipartAsync** is an asynchronous method.</span></span> <span data-ttu-id="35d05-140">K provedení práce po dokončení metody použijte [úlohu pokračování](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4,0) nebo klíčové slovo **await** (.NET 4,5).</span><span class="sxs-lookup"><span data-stu-id="35d05-140">To perform work after the method completes, use a [continuation task](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) or the **await** keyword (.NET 4.5).</span></span>

<span data-ttu-id="35d05-141">Tady je verze .NET Framework 4,0 předchozího kódu:</span><span class="sxs-lookup"><span data-stu-id="35d05-141">Here is the .NET Framework 4.0 version of the previous code:</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a><span data-ttu-id="35d05-142">Čtení dat ovládacího prvku formulář</span><span class="sxs-lookup"><span data-stu-id="35d05-142">Reading Form Control Data</span></span>

<span data-ttu-id="35d05-143">Formulář HTML, který jsem ukázal dříve, měl ovládací prvek textové zadání.</span><span class="sxs-lookup"><span data-stu-id="35d05-143">The HTML form that I showed earlier had a text input control.</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

<span data-ttu-id="35d05-144">Hodnotu ovládacího prvku lze získat z vlastnosti **FormData** třídy **MultipartFormDataStreamProvider**.</span><span class="sxs-lookup"><span data-stu-id="35d05-144">You can get the value of the control from the **FormData** property of the **MultipartFormDataStreamProvider**.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

<span data-ttu-id="35d05-145">**FormData** je **kolekce NameValueCollection** , který obsahuje páry název/hodnota pro ovládací prvky formuláře.</span><span class="sxs-lookup"><span data-stu-id="35d05-145">**FormData** is a **NameValueCollection** that contains name/value pairs for the form controls.</span></span> <span data-ttu-id="35d05-146">Kolekce může obsahovat duplicitní klíče.</span><span class="sxs-lookup"><span data-stu-id="35d05-146">The collection can contain duplicate keys.</span></span> <span data-ttu-id="35d05-147">Vezměte v úvahu tento formulář:</span><span class="sxs-lookup"><span data-stu-id="35d05-147">Consider this form:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

<span data-ttu-id="35d05-148">Text žádosti může vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="35d05-148">The request body might look like this:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

<span data-ttu-id="35d05-149">V takovém případě by kolekce **FormData** obsahovala následující páry klíč/hodnota:</span><span class="sxs-lookup"><span data-stu-id="35d05-149">In that case, the **FormData** collection would contain the following key/value pairs:</span></span>

- <span data-ttu-id="35d05-150">cesta: zpáteční cesta</span><span class="sxs-lookup"><span data-stu-id="35d05-150">trip: round-trip</span></span>
- <span data-ttu-id="35d05-151">možnosti: neukončeno</span><span class="sxs-lookup"><span data-stu-id="35d05-151">options: nonstop</span></span>
- <span data-ttu-id="35d05-152">možnosti: kalendářní data</span><span class="sxs-lookup"><span data-stu-id="35d05-152">options: dates</span></span>
- <span data-ttu-id="35d05-153">sedadlo: okno</span><span class="sxs-lookup"><span data-stu-id="35d05-153">seat: window</span></span>

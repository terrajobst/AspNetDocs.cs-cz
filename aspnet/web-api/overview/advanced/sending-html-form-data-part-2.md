---
uid: web-api/overview/advanced/sending-html-form-data-part-2
title: 'Posílání dat formulářů HTML ve webovém rozhraní API technologie ASP.NET: Nahrání souboru a vícedílné zprávy standardu MIME – ASP.NET 4.x'
author: MikeWasson
description: Tento kurz ukazuje postupy při nahrání souborů do webového rozhraní API. Také popisuje, jak můžete zpracovávat data vícedílné zprávy standardu MIME.
ms.author: riande
ms.date: 06/21/2012
ms.custom: seoapril2019
ms.assetid: a7f3c1b5-69d9-4261-b082-19ffafa5f16a
msc.legacyurl: /web-api/overview/advanced/sending-html-form-data-part-2
msc.type: authoredcontent
ms.openlocfilehash: 70e150a32f208cf75086f959d484d86e8501c6bd
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59419922"
---
# <a name="sending-html-form-data-in-aspnet-web-api-file-upload-and-multipart-mime"></a><span data-ttu-id="1cfc2-104">Posílání dat formulářů HTML ve webovém rozhraní API technologie ASP.NET: Nahrání souboru a vícedílné zprávy standardu MIME</span><span class="sxs-lookup"><span data-stu-id="1cfc2-104">Sending HTML Form Data in ASP.NET Web API: File Upload and Multipart MIME</span></span>

<span data-ttu-id="1cfc2-105">podle [Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="1cfc2-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

## <a name="part-2-file-upload-and-multipart-mime"></a><span data-ttu-id="1cfc2-106">Část 2: Nahrání souboru a vícedílné zprávy standardu MIME</span><span class="sxs-lookup"><span data-stu-id="1cfc2-106">Part 2: File Upload and Multipart MIME</span></span>

<span data-ttu-id="1cfc2-107">Tento kurz ukazuje postupy při nahrání souborů do webového rozhraní API.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-107">This tutorial shows how to upload files to a web API.</span></span> <span data-ttu-id="1cfc2-108">Také popisuje, jak můžete zpracovávat data vícedílné zprávy standardu MIME.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-108">It also describes how to process multipart MIME data.</span></span>

> [!NOTE]
> <span data-ttu-id="1cfc2-109">[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span><span class="sxs-lookup"><span data-stu-id="1cfc2-109">[Download the completed project](https://code.msdn.microsoft.com/ASPNET-Web-API-File-Upload-a8c0fb0d).</span></span>


<span data-ttu-id="1cfc2-110">Tady je příklad z formuláře HTML pro nahrání souboru:</span><span class="sxs-lookup"><span data-stu-id="1cfc2-110">Here is an example of an HTML form for uploading a file:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample1.html)]

![](sending-html-form-data-part-2/_static/image1.png)

<span data-ttu-id="1cfc2-111">Tento formulář obsahuje ovládací prvek textového vstupu a soubor vstupního ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-111">This form contains a text input control and a file input control.</span></span> <span data-ttu-id="1cfc2-112">Pokud formulář obsahuje ovládací prvek vstupu souboru **enctype** atribut by měl vždy být &quot;multipart/formulář data&quot;, která určuje, že bude odeslán formulář jako vícedílné zprávě standardu MIME.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-112">When a form contains a file input control, the **enctype** attribute should always be &quot;multipart/form-data&quot;, which specifies that the form will be sent as a multipart MIME message.</span></span>

<span data-ttu-id="1cfc2-113">Formát vícedílné zprávě standardu MIME je nejjednodušší pochopit zobrazením příklad žádosti:</span><span class="sxs-lookup"><span data-stu-id="1cfc2-113">The format of a multipart MIME message is easiest to understand by looking at an example request:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample2.cmd)]

<span data-ttu-id="1cfc2-114">Tato zpráva je rozdělen do dvou *částí*, jeden pro každý ovládací prvek formuláře.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-114">This message is divided into two *parts*, one for each form control.</span></span> <span data-ttu-id="1cfc2-115">Část hranice jsou označeny řádky, které začínají znakem pomlčky.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-115">Part boundaries are indicated by the lines that start with dashes.</span></span>

> [!NOTE]
> <span data-ttu-id="1cfc2-116">Hranice část obsahuje náhodné komponentu (&quot;41184676334&quot;) k zajištění, že hranici řetězec pravděpodobně neobsahuje omylem uvnitř část zprávy.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-116">The part boundary includes a random component (&quot;41184676334&quot;) to ensure that the boundary string does not accidentally appear inside a message part.</span></span>


<span data-ttu-id="1cfc2-117">Každá část zprávy obsahuje jednu nebo víc hlaviček, za nímž následuje část obsahu.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-117">Each message part contains one or more headers, followed by the part contents.</span></span>

- <span data-ttu-id="1cfc2-118">Hlavička Content-Disposition zahrnuje název ovládacího prvku.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-118">The Content-Disposition header includes the name of the control.</span></span> <span data-ttu-id="1cfc2-119">Pro soubory neobsahuje také název souboru.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-119">For files, it also contains the file name.</span></span>
- <span data-ttu-id="1cfc2-120">Hlavička Content-Type popisuje data v části.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-120">The Content-Type header describes the data in the part.</span></span> <span data-ttu-id="1cfc2-121">Pokud je vynechán této hlavičky, výchozí hodnota je text/plain.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-121">If this header is omitted, the default is text/plain.</span></span>

<span data-ttu-id="1cfc2-122">V předchozím příkladu se uživatel nahrál soubor s názvem GrandCanyon.jpg, s typem obsahu image/jpeg; a byla zadána hodnota textový vstup &quot;léto dovolené&quot;.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-122">In the previous example, the user uploaded a file named GrandCanyon.jpg, with content type image/jpeg; and the value of the text input was &quot;Summer Vacation&quot;.</span></span>

## <a name="file-upload"></a><span data-ttu-id="1cfc2-123">Nahrání souboru</span><span class="sxs-lookup"><span data-stu-id="1cfc2-123">File Upload</span></span>

<span data-ttu-id="1cfc2-124">Nyní Pojďme se podívat na kontroler Web API, která čte soubory z vícedílné zprávě standardu MIME.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-124">Now let's look at a Web API controller that reads files from a multipart MIME message.</span></span> <span data-ttu-id="1cfc2-125">Kontroler se asynchronně číst soubory.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-125">The controller will read the files asynchronously.</span></span> <span data-ttu-id="1cfc2-126">Webové rozhraní API podporuje asynchronní akce [programovací model založený na úlohách](https://msdn.microsoft.com/library/dd460693.aspx).</span><span class="sxs-lookup"><span data-stu-id="1cfc2-126">Web API supports asynchronous actions using the [task-based programming model](https://msdn.microsoft.com/library/dd460693.aspx).</span></span> <span data-ttu-id="1cfc2-127">Nejprve, zde je kód rozhraní .NET Framework 4.5, který podporuje při cílení **asynchronní** a **await** klíčová slova.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-127">First, here is the code if you are targeting .NET Framework 4.5, which supports the **async** and **await** keywords.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample3.cs)]

<span data-ttu-id="1cfc2-128">Všimněte si, že akce kontroleru nepřijímá žádné parametry.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-128">Notice that the controller action does not take any parameters.</span></span> <span data-ttu-id="1cfc2-129">Důvodem je, jsme zpracovat text požadavku v akci, bez vyvolání formátovací modul typu média.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-129">That's because we process the request body inside the action, without invoking a media-type formatter.</span></span>

<span data-ttu-id="1cfc2-130">**IsMultipartContent** metoda zkontroluje, jestli žádost obsahuje vícedílné zprávě standardu MIME.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-130">The **IsMultipartContent** method checks whether the request contains a multipart MIME message.</span></span> <span data-ttu-id="1cfc2-131">V opačném případě kontroleru vrátí stavový kód HTTP 415 (nepodporovaný typ média).</span><span class="sxs-lookup"><span data-stu-id="1cfc2-131">If not, the controller returns HTTP status code 415 (Unsupported Media Type).</span></span>

<span data-ttu-id="1cfc2-132">**MultipartFormDataStreamProvider** třída je pomocný objekt, který přiděluje datové proudy souborů o nahraných souborech.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-132">The **MultipartFormDataStreamProvider** class is a helper object that allocates file streams for uploaded files.</span></span> <span data-ttu-id="1cfc2-133">Čtení zprávy vícedílné zprávy standardu MIME, zavolejte **ReadAsMultipartAsync** metody.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-133">To read the multipart MIME message, call the **ReadAsMultipartAsync** method.</span></span> <span data-ttu-id="1cfc2-134">Tato metoda extrahuje všechny části zprávy a zapisuje je do datových proudů poskytované **MultipartFormDataStreamProvider**.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-134">This method extracts all of the message parts and writes them into the streams provided by the **MultipartFormDataStreamProvider**.</span></span>

<span data-ttu-id="1cfc2-135">Po dokončení metody můžete získat informace o souborech z **FileData** vlastnost, která je kolekce z **MultipartFileData** objekty.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-135">When the method completes, you can get information about the files from the **FileData** property, which is a collection of **MultipartFileData** objects.</span></span>

- <span data-ttu-id="1cfc2-136">**MultipartFileData.FileName** je název místního souboru na serveru, kam byl uložen soubor.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-136">**MultipartFileData.FileName** is the local file name on the server, where the file was saved.</span></span>
- <span data-ttu-id="1cfc2-137">**MultipartFileData.Headers** obsahuje část hlavičky (*není* záhlaví požadavku).</span><span class="sxs-lookup"><span data-stu-id="1cfc2-137">**MultipartFileData.Headers** contains the part header (*not* the request header).</span></span> <span data-ttu-id="1cfc2-138">To můžete použít pro přístup k obsahu\_záhlaví dispozice a Content-Type.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-138">You can use this to access the Content\_Disposition and Content-Type headers.</span></span>

<span data-ttu-id="1cfc2-139">Jak název napovídá, **ReadAsMultipartAsync** je asynchronní metodu.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-139">As the name suggests, **ReadAsMultipartAsync** is an asynchronous method.</span></span> <span data-ttu-id="1cfc2-140">K provedení práce po dokončení metody, použijte [úkol pokračování](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) nebo **await** – klíčové slovo (.NET 4.5).</span><span class="sxs-lookup"><span data-stu-id="1cfc2-140">To perform work after the method completes, use a [continuation task](https://msdn.microsoft.com/library/ee372288.aspx) (.NET 4.0) or the **await** keyword (.NET 4.5).</span></span>

<span data-ttu-id="1cfc2-141">Tady je verze rozhraní .NET Framework 4.0 předchozího kódu:</span><span class="sxs-lookup"><span data-stu-id="1cfc2-141">Here is the .NET Framework 4.0 version of the previous code:</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample4.cs)]

## <a name="reading-form-control-data"></a><span data-ttu-id="1cfc2-142">Čtení dat ovládacího prvku formuláře</span><span class="sxs-lookup"><span data-stu-id="1cfc2-142">Reading Form Control Data</span></span>

<span data-ttu-id="1cfc2-143">Formulář HTML, který jsem ukazoval dříve měli ovládací prvek textového vstupu.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-143">The HTML form that I showed earlier had a text input control.</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample5.html)]

<span data-ttu-id="1cfc2-144">Můžete získat hodnotu z ovládacího prvku **FormData** vlastnost **MultipartFormDataStreamProvider**.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-144">You can get the value of the control from the **FormData** property of the **MultipartFormDataStreamProvider**.</span></span>

[!code-csharp[Main](sending-html-form-data-part-2/samples/sample6.cs?highlight=15)]

<span data-ttu-id="1cfc2-145">**FormData** je **NameValueCollection** obsahující dvojice název/hodnota pro ovládací prvky formuláře.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-145">**FormData** is a **NameValueCollection** that contains name/value pairs for the form controls.</span></span> <span data-ttu-id="1cfc2-146">Kolekce může obsahovat duplicitní klíče.</span><span class="sxs-lookup"><span data-stu-id="1cfc2-146">The collection can contain duplicate keys.</span></span> <span data-ttu-id="1cfc2-147">Vezměte v úvahu tento formulář:</span><span class="sxs-lookup"><span data-stu-id="1cfc2-147">Consider this form:</span></span>

[!code-html[Main](sending-html-form-data-part-2/samples/sample7.html)]

![](sending-html-form-data-part-2/_static/image2.png)

<span data-ttu-id="1cfc2-148">Text žádosti může vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="1cfc2-148">The request body might look like this:</span></span>

[!code-console[Main](sending-html-form-data-part-2/samples/sample8.cmd)]

<span data-ttu-id="1cfc2-149">V takovém případě **FormData** kolekce by obsahovala následující dvojice klíč/hodnota:</span><span class="sxs-lookup"><span data-stu-id="1cfc2-149">In that case, the **FormData** collection would contain the following key/value pairs:</span></span>

- <span data-ttu-id="1cfc2-150">o jízdách: zpátečního převodu</span><span class="sxs-lookup"><span data-stu-id="1cfc2-150">trip: round-trip</span></span>
- <span data-ttu-id="1cfc2-151">možnosti: nonstop</span><span class="sxs-lookup"><span data-stu-id="1cfc2-151">options: nonstop</span></span>
- <span data-ttu-id="1cfc2-152">možnosti: kalendářních dat</span><span class="sxs-lookup"><span data-stu-id="1cfc2-152">options: dates</span></span>
- <span data-ttu-id="1cfc2-153">licence: okno</span><span class="sxs-lookup"><span data-stu-id="1cfc2-153">seat: window</span></span>

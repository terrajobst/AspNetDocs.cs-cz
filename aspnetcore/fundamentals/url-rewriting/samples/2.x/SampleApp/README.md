---
ms.openlocfilehash: 4a4ad30846d1993b3e561c96c00fbf9a0c7f3929
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57070879"
---
# <a name="aspnet-core-url-rewriting-sample-aspnet-core-2x"></a><span data-ttu-id="ea93f-101">Přepisování adres ukázka URL ASP.NET Core (ASP.NET Core 2.x)</span><span class="sxs-lookup"><span data-stu-id="ea93f-101">ASP.NET Core URL Rewriting Sample (ASP.NET Core 2.x)</span></span>

<span data-ttu-id="ea93f-102">Tato ukázka ilustruje použití ASP.NET Core 2.x Middleware pro přepis adres URL.</span><span class="sxs-lookup"><span data-stu-id="ea93f-102">This sample illustrates usage of ASP.NET Core 2.x URL Rewriting Middleware.</span></span> <span data-ttu-id="ea93f-103">Aplikace ukazuje adresu URL pro přesměrování a možnosti přepisování adres URL.</span><span class="sxs-lookup"><span data-stu-id="ea93f-103">The app demonstrates URL redirect and URL rewriting options.</span></span>

<span data-ttu-id="ea93f-104">Při spuštění ukázky, které nejsou soubory odpovědí návratová adresa URL přepsaný nebo přesměrované, při použití některé z pravidel na adrese URL žádosti.</span><span class="sxs-lookup"><span data-stu-id="ea93f-104">When running the sample, non-file responses return the rewritten or redirected URL when one of the rules is applied to a request URL.</span></span> <span data-ttu-id="ea93f-105">Pro příklady souborů XML a text Middleware statické soubory slouží soubor po požadavku na adresu URL je přepsán middlewarem.</span><span class="sxs-lookup"><span data-stu-id="ea93f-105">For the XML and text file examples, Static File Middleware serves the file after the request URL is rewritten by the middleware.</span></span>

## <a name="examples-in-this-sample"></a><span data-ttu-id="ea93f-106">Příklady v této ukázce</span><span class="sxs-lookup"><span data-stu-id="ea93f-106">Examples in this sample</span></span>

* `AddRedirect("redirect-rule/(.*)", "redirected/$1")`
  - <span data-ttu-id="ea93f-107">Stavový kód úspěchu: 302 (Found)</span><span class="sxs-lookup"><span data-stu-id="ea93f-107">Success status code: 302 (Found)</span></span>
  - <span data-ttu-id="ea93f-108">Příklad (přesměrování): **/redirect-rule / {capture_group}** k **/redirected/ {capture_group}**</span><span class="sxs-lookup"><span data-stu-id="ea93f-108">Example (redirect): **/redirect-rule/{capture_group}** to **/redirected/{capture_group}**</span></span>
* `AddRewrite(@"^rewrite-rule/(\d+)/(\d+)", "rewritten?var1=$1&var2=$2", skipRemainingRules: true)`
  - <span data-ttu-id="ea93f-109">Stavový kód úspěchu: 200 (OK)</span><span class="sxs-lookup"><span data-stu-id="ea93f-109">Success status code: 200 (OK)</span></span>
  - <span data-ttu-id="ea93f-110">Příklad (revize): **/rewrite-rule / {capture_group_1} / {capture_group_2}** k **/ přepsán? var1 = {capture_group_1} & var2 = {capture_group_2}**</span><span class="sxs-lookup"><span data-stu-id="ea93f-110">Example (rewrite): **/rewrite-rule/{capture_group_1}/{capture_group_2}** to **/rewritten?var1={capture_group_1}&var2={capture_group_2}**</span></span>
* `AddApacheModRewrite(env.ContentRootFileProvider, "ApacheModRewrite.txt")`
  - <span data-ttu-id="ea93f-111">Stavový kód úspěchu: 302 (Found)</span><span class="sxs-lookup"><span data-stu-id="ea93f-111">Success status code: 302 (Found)</span></span>
  - <span data-ttu-id="ea93f-112">Příklad (přesměrování): **/apache-mod-rules-redirect / {capture_group}** k **/ přesměrováno? id = {capture_group}**</span><span class="sxs-lookup"><span data-stu-id="ea93f-112">Example (redirect): **/apache-mod-rules-redirect/{capture_group}** to **/redirected?id={capture_group}**</span></span>
* `AddIISUrlRewrite(env.ContentRootFileProvider, "IISUrlRewrite.xml")`
  - <span data-ttu-id="ea93f-113">Stavový kód úspěchu: 200 (OK)</span><span class="sxs-lookup"><span data-stu-id="ea93f-113">Success status code: 200 (OK)</span></span>
  - <span data-ttu-id="ea93f-114">Příklad (revize): **/iis-rules-rewrite / {capture_group}** k **/ přepsán? id = {capture_group}**</span><span class="sxs-lookup"><span data-stu-id="ea93f-114">Example (rewrite): **/iis-rules-rewrite/{capture_group}** to **/rewritten?id={capture_group}**</span></span>
* `Add(RedirectXmlFileRequests)`
  - <span data-ttu-id="ea93f-115">Stavový kód úspěchu: 301 (trvale přesunut)</span><span class="sxs-lookup"><span data-stu-id="ea93f-115">Success status code: 301 (Moved Permanently)</span></span>
  - <span data-ttu-id="ea93f-116">Příklad (přesměrování): **/file.xml** k **/xmlfiles/file.xml**</span><span class="sxs-lookup"><span data-stu-id="ea93f-116">Example (redirect): **/file.xml** to **/xmlfiles/file.xml**</span></span>
* `Add(RewriteTextFileRequests)`
  - <span data-ttu-id="ea93f-117">Stavový kód úspěchu: 200 (OK)</span><span class="sxs-lookup"><span data-stu-id="ea93f-117">Success status code: 200 (OK)</span></span>
  - <span data-ttu-id="ea93f-118">Příklad (revize): **/some_file.txt** k **/file.txt**</span><span class="sxs-lookup"><span data-stu-id="ea93f-118">Example (rewrite): **/some_file.txt** to **/file.txt**</span></span>
* `Add(new RedirectImageRequests(".png", "/png-images")))`<br>`Add(new RedirectImageRequests(".jpg", "/jpg-images")))`
  - <span data-ttu-id="ea93f-119">Stavový kód úspěchu: 301 (trvale přesunut)</span><span class="sxs-lookup"><span data-stu-id="ea93f-119">Success status code: 301 (Moved Permanently)</span></span>
  - <span data-ttu-id="ea93f-120">Příklad (přesměrování): **/image.png** k **/png-images/image.png**</span><span class="sxs-lookup"><span data-stu-id="ea93f-120">Example (redirect): **/image.png** to **/png-images/image.png**</span></span>
  - <span data-ttu-id="ea93f-121">Příklad (přesměrování): **/image.jpg** k **/jpg-images/image.jpg**</span><span class="sxs-lookup"><span data-stu-id="ea93f-121">Example (redirect): **/image.jpg** to **/jpg-images/image.jpg**</span></span>

## <a name="use-a-physicalfileprovider"></a><span data-ttu-id="ea93f-122">Použít PhysicalFileProvider</span><span class="sxs-lookup"><span data-stu-id="ea93f-122">Use a PhysicalFileProvider</span></span>

<span data-ttu-id="ea93f-123">Můžete také získat `IFileProvider` tak, že vytvoříte `PhysicalFileProvider` má být předán `AddApacheModRewrite()` a `AddIISUrlRewrite()` metody:</span><span class="sxs-lookup"><span data-stu-id="ea93f-123">You can also obtain an `IFileProvider` by creating a `PhysicalFileProvider` to pass into the `AddApacheModRewrite()` and `AddIISUrlRewrite()` methods:</span></span>

```csharp
using Microsoft.Extensions.FileProviders;
PhysicalFileProvider fileProvider = new PhysicalFileProvider(Directory.GetCurrentDirectory());
```

## <a name="secure-redirection-extensions"></a><span data-ttu-id="ea93f-124">Zabezpečené rozšíření přesměrování</span><span class="sxs-lookup"><span data-stu-id="ea93f-124">Secure redirection extensions</span></span>

<span data-ttu-id="ea93f-125">Tato ukázka obsahuje `WebHostBuilder` konfigurace pro aplikace pro použití adresy URL (`https://localhost:5001`, `https://localhost`) a testovací certifikát (*testCert.pfx*) pomáhat při zkoumání metod zabezpečeného přesměrování.</span><span class="sxs-lookup"><span data-stu-id="ea93f-125">This sample includes `WebHostBuilder` configuration for the app to use URLs (`https://localhost:5001`, `https://localhost`) and a test certificate (*testCert.pfx*) to assist in exploring the secure redirect methods.</span></span> <span data-ttu-id="ea93f-126">Pokud už server má port 443 přiřazené nebo používá, `https://localhost` příklad nefunguje&mdash;odebrat `ListenOptions` pro port 443 v `CreateWebHostBuilder` metodu *Program.cs* souborů nebo zrušení vazby portu 443 na Server, aby Kestrel mohl použít port.</span><span class="sxs-lookup"><span data-stu-id="ea93f-126">If the server already has port 443 assigned or in use, the `https://localhost` example doesn't work&mdash;remove the `ListenOptions` for port 443 in the `CreateWebHostBuilder` method of the *Program.cs* file or unbind port 443 on the server so that Kestrel can use the port.</span></span>

| <span data-ttu-id="ea93f-127">Metoda</span><span class="sxs-lookup"><span data-stu-id="ea93f-127">Method</span></span>                           | <span data-ttu-id="ea93f-128">Stavový kód</span><span class="sxs-lookup"><span data-stu-id="ea93f-128">Status Code</span></span> |    <span data-ttu-id="ea93f-129">Port</span><span class="sxs-lookup"><span data-stu-id="ea93f-129">Port</span></span>    |
| -------------------------------- | :---------: | :--------: |
| `.AddRedirectToHttpsPermanent()` |     <span data-ttu-id="ea93f-130">301</span><span class="sxs-lookup"><span data-stu-id="ea93f-130">301</span></span>     | <span data-ttu-id="ea93f-131">Null (465)</span><span class="sxs-lookup"><span data-stu-id="ea93f-131">null (465)</span></span> |
| `.AddRedirectToHttps()`          |     <span data-ttu-id="ea93f-132">302</span><span class="sxs-lookup"><span data-stu-id="ea93f-132">302</span></span>     | <span data-ttu-id="ea93f-133">Null (465)</span><span class="sxs-lookup"><span data-stu-id="ea93f-133">null (465)</span></span> |
| `.AddRedirectToHttps(301)`       |     <span data-ttu-id="ea93f-134">301</span><span class="sxs-lookup"><span data-stu-id="ea93f-134">301</span></span>     | <span data-ttu-id="ea93f-135">Null (465)</span><span class="sxs-lookup"><span data-stu-id="ea93f-135">null (465)</span></span> |
| `.AddRedirectToHttps(301, 5001)` |     <span data-ttu-id="ea93f-136">301</span><span class="sxs-lookup"><span data-stu-id="ea93f-136">301</span></span>     |    <span data-ttu-id="ea93f-137">5001</span><span class="sxs-lookup"><span data-stu-id="ea93f-137">5001</span></span>    |

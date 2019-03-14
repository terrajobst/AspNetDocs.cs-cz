---
uid: webhooks/diagnostics/debugging
title: ASP.NET – Webhooky ladění | Dokumentace Microsoftu
author: rick-anderson
description: Postup ladění ASP.NET – Webhooky.
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 517d282fc22703b5861b748aea51023fa0a12a26
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57077410"
---
# <a name="aspnet-webhooks-debugging"></a><span data-ttu-id="bd9ee-103">ASP.NET – Webhooky ladění</span><span class="sxs-lookup"><span data-stu-id="bd9ee-103">ASP.NET WebHooks debugging</span></span>  

## <a name="debugging-in-azure"></a><span data-ttu-id="bd9ee-104">Ladění v Azure</span><span class="sxs-lookup"><span data-stu-id="bd9ee-104">Debugging in Azure</span></span>

<span data-ttu-id="bd9ee-105">Ladění webové aplikace při spuštění v Azure, najdete v tématu výukového programu [řešení problémů s webovou aplikací ve službě Azure App Service pomocí sady Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span><span class="sxs-lookup"><span data-stu-id="bd9ee-105">To debug your Web Application while running in Azure, please see the tutorial [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="debugging-with-source-and-symbols"></a><span data-ttu-id="bd9ee-106">Ladění se zdrojem a symboly</span><span class="sxs-lookup"><span data-stu-id="bd9ee-106">Debugging with Source and Symbols</span></span>

<span data-ttu-id="bd9ee-107">Kromě ladění vlastního kódu, je možné ladit přímo do WebHooks Microsoft ASP.NET a ve skutečnosti všechny technologie .NET.</span><span class="sxs-lookup"><span data-stu-id="bd9ee-107">In addition to debugging your own code, it is possible to debug directly into Microsoft ASP.NET WebHooks, and in fact all of .NET.</span></span> <span data-ttu-id="bd9ee-108">Tento postup funguje, bez ohledu na to, zda ladit místně nebo vzdáleně.</span><span class="sxs-lookup"><span data-stu-id="bd9ee-108">This works regardless of whether you debug locally or remotely.</span></span> <span data-ttu-id="bd9ee-109">Nejprve nakonfigurujte Visual Studio a najít tak, že přejdete do zdroje a symbolů **ladění** a potom **možnosti a nastavení**.</span><span class="sxs-lookup"><span data-stu-id="bd9ee-109">First, configure Visual Studio to find the source and symbols by going to **Debug** and then **Options and Settings**.</span></span> <span data-ttu-id="bd9ee-110">Nastavení možností takto:</span><span class="sxs-lookup"><span data-stu-id="bd9ee-110">Set the options like this:</span></span>

![Možnosti a nastavení](_static/SourceSymbols.png)

<span data-ttu-id="bd9ee-112">Pak přidejte odkaz na [symbolsource.org](http://symbolsource.org) pro stahování zdroje a symbolů.</span><span class="sxs-lookup"><span data-stu-id="bd9ee-112">Then add a link to [symbolsource.org](http://symbolsource.org) for downloading the source and symbols.</span></span> <span data-ttu-id="bd9ee-113">Přejděte **symboly** kartu nabídky výše a přidejte následující položky jako umístění symbolů:</span><span class="sxs-lookup"><span data-stu-id="bd9ee-113">Go to the **Symbols** tab of the menu above and add the following as a symbol location:</span></span>

```
http://srv.symbolsource.org/pdb/Public
```

<span data-ttu-id="bd9ee-114">Kromě toho se ujistěte, že adresář mezipaměti obsahuje krátký název; názvy souborů v opačném případě můžete získat příliš dlouho která způsobí, že symboly nelze načíst.</span><span class="sxs-lookup"><span data-stu-id="bd9ee-114">In addition, make sure that the cache directory has a short name; otherwise the file names can get too long which will cause the symbols to not load.</span></span> <span data-ttu-id="bd9ee-115">Je ukázková cesta:</span><span class="sxs-lookup"><span data-stu-id="bd9ee-115">A sample path is:</span></span>

```
C:\SymCache
```

<span data-ttu-id="bd9ee-116">Nastavení by měl vypadat nějak takto:</span><span class="sxs-lookup"><span data-stu-id="bd9ee-116">The settings should look similar to this:</span></span>

![Ukázka umístění souboru možnosti symbolu](_static/SymSource.png)

---
uid: webhooks/diagnostics/debugging
title: Ladění webhooků ASP.NET | Microsoft Docs
author: rick-anderson
description: Jak ladit Webhooky ASP.NET
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 467da78b-3c35-4c51-8b08-77a32379e4a8
ms.openlocfilehash: 517d282fc22703b5861b748aea51023fa0a12a26
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640866"
---
# <a name="aspnet-webhooks-debugging"></a><span data-ttu-id="040f9-103">Ladění webhooků ASP.NET</span><span class="sxs-lookup"><span data-stu-id="040f9-103">ASP.NET WebHooks debugging</span></span>  

## <a name="debugging-in-azure"></a><span data-ttu-id="040f9-104">Ladění v Azure</span><span class="sxs-lookup"><span data-stu-id="040f9-104">Debugging in Azure</span></span>

<span data-ttu-id="040f9-105">Chcete-li ladit webovou aplikaci při spuštění v Azure, přečtěte si kurz [řešení potíží s webovou aplikací v Azure App Service pomocí sady Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span><span class="sxs-lookup"><span data-stu-id="040f9-105">To debug your Web Application while running in Azure, please see the tutorial [Troubleshoot a web app in Azure App Service using Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/#webserverlogs).</span></span>

## <a name="debugging-with-source-and-symbols"></a><span data-ttu-id="040f9-106">Ladění pomocí zdrojů a symbolů</span><span class="sxs-lookup"><span data-stu-id="040f9-106">Debugging with Source and Symbols</span></span>

<span data-ttu-id="040f9-107">Kromě ladění vlastního kódu je možné provést ladění přímo do Microsoft ASP.NET webhooků a ve skutečnosti na rozhraní .NET.</span><span class="sxs-lookup"><span data-stu-id="040f9-107">In addition to debugging your own code, it is possible to debug directly into Microsoft ASP.NET WebHooks, and in fact all of .NET.</span></span> <span data-ttu-id="040f9-108">To funguje bez ohledu na to, zda je místní nebo vzdálené ladění.</span><span class="sxs-lookup"><span data-stu-id="040f9-108">This works regardless of whether you debug locally or remotely.</span></span> <span data-ttu-id="040f9-109">Nejdřív nakonfigurujte Visual Studio tak, aby bylo možné najít zdroj a symboly, a to tak, že kliknete na **ladění** a pak na **Možnosti a nastavení**.</span><span class="sxs-lookup"><span data-stu-id="040f9-109">First, configure Visual Studio to find the source and symbols by going to **Debug** and then **Options and Settings**.</span></span> <span data-ttu-id="040f9-110">Nastavte následující možnosti:</span><span class="sxs-lookup"><span data-stu-id="040f9-110">Set the options like this:</span></span>

![Možnosti a nastavení](_static/SourceSymbols.png)

<span data-ttu-id="040f9-112">Pak přidejte odkaz na [symbolsource.org](http://symbolsource.org) pro stažení zdroje a symbolů.</span><span class="sxs-lookup"><span data-stu-id="040f9-112">Then add a link to [symbolsource.org](http://symbolsource.org) for downloading the source and symbols.</span></span> <span data-ttu-id="040f9-113">Přejděte na kartu **symboly** v nabídce výše a přidejte následující jako umístění symbolu:</span><span class="sxs-lookup"><span data-stu-id="040f9-113">Go to the **Symbols** tab of the menu above and add the following as a symbol location:</span></span>

```
http://srv.symbolsource.org/pdb/Public
```

<span data-ttu-id="040f9-114">Kromě toho se ujistěte, že adresář mezipaměti má krátký název; jinak názvy souborů mohou být příliš dlouhé, což způsobí, že symboly nebudou načteny.</span><span class="sxs-lookup"><span data-stu-id="040f9-114">In addition, make sure that the cache directory has a short name; otherwise the file names can get too long which will cause the symbols to not load.</span></span> <span data-ttu-id="040f9-115">Vzorová cesta:</span><span class="sxs-lookup"><span data-stu-id="040f9-115">A sample path is:</span></span>

```
C:\SymCache
```

<span data-ttu-id="040f9-116">Nastavení by mělo vypadat podobně jako toto:</span><span class="sxs-lookup"><span data-stu-id="040f9-116">The settings should look similar to this:</span></span>

![Možnosti příklad umístění souboru se symboly](_static/SymSource.png)

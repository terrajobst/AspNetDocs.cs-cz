---
uid: web-forms/videos/aspnet-ajax/how-do-i-choose-between-methods-of-ajax-page-updates
title: '[Postupy:] Vyberte si mezi metodami aktualizace stránky AJAX? | Dokumenty Microsoft'
author: JoeStagner
description: V tomto videu Jana Stagner porovná dvě primární metody provádění aktualizací stránky ve stylu AJAX v aplikaci ASP.NET. První metodou je použití UPD...
ms.author: riande
ms.date: 07/09/2007
ms.assetid: a5e33a7d-ccb2-483f-a955-3d39f72ba4ec
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-choose-between-methods-of-ajax-page-updates
msc.type: video
ms.openlocfilehash: 56e3ebfbe0b5af4234791136725de79e38171cc1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78523665"
---
# <a name="how-do-i-choose-between-methods-of-ajax-page-updates"></a><span data-ttu-id="f0269-105">[Postupy:] Vyberte si mezi metodami aktualizace stránky AJAX?</span><span class="sxs-lookup"><span data-stu-id="f0269-105">[How Do I:] Choose Between Methods of AJAX Page Updates?</span></span>

<span data-ttu-id="f0269-106">[Jana Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="f0269-106">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="f0269-107">V tomto videu Jana Stagner porovná dvě primární metody provádění aktualizací stránky ve stylu AJAX v aplikaci ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="f0269-107">In this video Joe Stagner compares the two primary methods of performing AJAX-style page updates in an ASP.NET application.</span></span> <span data-ttu-id="f0269-108">První metodou je použití prvku UpdatePanel, kde není třeba psát žádný další kód na straně klienta nebo na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="f0269-108">The first method is to use an UpdatePanel, where no additional code needs to be written on either the client side or the server side.</span></span> <span data-ttu-id="f0269-109">Výhodou použití prvku UpdatePanel je, že vše funguje automaticky.</span><span class="sxs-lookup"><span data-stu-id="f0269-109">The benefit of using the UpdatePanel is that everything works automatically.</span></span> <span data-ttu-id="f0269-110">Pokutou je to, že u klienta vyžaduje, aby se do žádosti a odpovědi AJAX zavedla spousta dat, a na serveru, který vyžaduje, aby se spustil celý životní cyklus stránky.</span><span class="sxs-lookup"><span data-stu-id="f0269-110">The penalty is that at the client it requires a lot of data to be included in the AJAX request and response, and at the server it requires a full page lifecycle to be executed.</span></span> <span data-ttu-id="f0269-111">Druhou metodou je použití zpětných volání sítě, kde je nutné zapsat další kód na straně klienta i na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="f0269-111">The second method is to use network callbacks, where additional code needs to be written on both the client side and the server side.</span></span> <span data-ttu-id="f0269-112">Výhodou použití zpětných volání sítě je to, že v klientovi, který vyžaduje, aby byly do žádosti a odpovědi AJAX zahrnuty velmi málo dat, a na serveru, který vyžaduje, aby se spustila pouze metoda s názvem služby.</span><span class="sxs-lookup"><span data-stu-id="f0269-112">The benefit of using network callbacks is that at the client it requires very little data to be included in the AJAX request and response, and at the server it requires only the called service method to be executed.</span></span> <span data-ttu-id="f0269-113">Trest je čas a úsilí, které potřebuje k zápisu potřebného kódu.</span><span class="sxs-lookup"><span data-stu-id="f0269-113">The penality is the time and effort it takes to write the necessary code.</span></span> <span data-ttu-id="f0269-114">Jana uzavře video projednáním, co byste měli zvážit při výběru mezi dvěma primárními metodami aktualizace stránky ve stylu AJAX.</span><span class="sxs-lookup"><span data-stu-id="f0269-114">Joe concludes the video by discussing what you should consider when choosing between the two primary methods of AJAX-style page updates.</span></span> <span data-ttu-id="f0269-115">(Toto video používá kód z [postupu jak začít s ASP.NET AJAX](how-do-i-get-started-with-aspnet-ajax.md) a [Jak udělat zpětná volání sítě na straně klienta pomocí videa ASP.NET AJAX](how-do-i-make-client-side-network-callbacks-with-aspnet-ajax.md) .)</span><span class="sxs-lookup"><span data-stu-id="f0269-115">(This video uses the code from the [How Do I Get Started with ASP.NET AJAX](how-do-i-get-started-with-aspnet-ajax.md) video and the [How Do I Make Client-Side Network Callbacks with ASP.NET AJAX](how-do-i-make-client-side-network-callbacks-with-aspnet-ajax.md) video.)</span></span>

[<span data-ttu-id="f0269-116">&#9654;Přehrát video (11 minut)</span><span class="sxs-lookup"><span data-stu-id="f0269-116">&#9654; Watch video (11 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-choose-between-methods-of-ajax-page-updates)

> [!div class="step-by-step"]
> <span data-ttu-id="f0269-117">[Předchozí](how-do-i-update-multiple-regions-of-a-page-with-aspnet-ajax.md)
> [Další](how-do-i-use-other-javascript-user-interface-libraries-with-aspnet-ajax.md)</span><span class="sxs-lookup"><span data-stu-id="f0269-117">[Previous](how-do-i-update-multiple-regions-of-a-page-with-aspnet-ajax.md)
[Next](how-do-i-use-other-javascript-user-interface-libraries-with-aspnet-ajax.md)</span></span>

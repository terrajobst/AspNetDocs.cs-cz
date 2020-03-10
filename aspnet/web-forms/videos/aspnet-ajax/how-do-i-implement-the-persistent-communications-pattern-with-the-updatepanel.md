---
uid: web-forms/videos/aspnet-ajax/how-do-i-implement-the-persistent-communications-pattern-with-the-updatepanel
title: '[Postupy:] Implementujte model trvalé komunikace pomocí ovládacího prvku UpdatePanel? | Dokumenty Microsoft'
author: JoeStagner
description: V tradičním webovém serveru prohlížeč a server neudržují průběžnou komunikaci, ale komunikují pouze v reakci na uživatele, který provádí jednání...
ms.author: riande
ms.date: 08/01/2007
ms.assetid: 49c7a74d-dce7-4d5c-8282-c7846f478e11
msc.legacyurl: /web-forms/videos/aspnet-ajax/how-do-i-implement-the-persistent-communications-pattern-with-the-updatepanel
msc.type: video
ms.openlocfilehash: 2a0a286ad731751460cb9d924a4de4dfe63f45b8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628735"
---
# <a name="how-do-i-implement-the-persistent-communications-pattern-with-the-updatepanel"></a><span data-ttu-id="69e5c-104">[Postupy:] Implementujte model trvalé komunikace pomocí ovládacího prvku UpdatePanel?</span><span class="sxs-lookup"><span data-stu-id="69e5c-104">[How Do I:] Implement the Persistent Communications Pattern with the UpdatePanel?</span></span>

<span data-ttu-id="69e5c-105">[Jana Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="69e5c-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

<span data-ttu-id="69e5c-106">V tradičním webovém serveru prohlížeč a server neudržují průběžnou komunikaci, ale komunikují pouze jako odpověď na uživatele, který provádí akci.</span><span class="sxs-lookup"><span data-stu-id="69e5c-106">In a traditional Web site the browser and the server do not maintain an ongoing communication, but communicate only in response to the user performing an action.</span></span> <span data-ttu-id="69e5c-107">Na moderním webu, kde se stránka stává kontejnerem aplikace, může být výhodné pro prohlížeč a server, aby udržoval průběžnou komunikaci, aby bylo možné provádět aktualizace stránky bez toho, aby uživatel prováděl akci.</span><span class="sxs-lookup"><span data-stu-id="69e5c-107">In a modern Web site where the page becomes an application container, it can be advantageous for the browser and the server to maintain an ongoing communication so that page updates can occur without the user performing an action.</span></span> <span data-ttu-id="69e5c-108">To se označuje jako model trvalé komunikace pro AJAX.</span><span class="sxs-lookup"><span data-stu-id="69e5c-108">This is known as the Persistent Communications Pattern for AJAX.</span></span> <span data-ttu-id="69e5c-109">ASP.NET AJAX nabízí dva hlavní způsoby, jak implementovat model trvalé komunikace pro webové vývojáře.</span><span class="sxs-lookup"><span data-stu-id="69e5c-109">ASP.NET AJAX provides two main ways for Web developers to implement the Persistent Communications Pattern.</span></span> <span data-ttu-id="69e5c-110">Toto video ukazuje jednoduchý způsob, který slouží jako základ implementace ASP.NET AJAX UpdatePanel.</span><span class="sxs-lookup"><span data-stu-id="69e5c-110">This video demonstrates the simple way, which is to use the ASP.NET AJAX UpdatePanel as the basis of the implementation.</span></span> <span data-ttu-id="69e5c-111">V pozdějším videu se naučíte implementovat stejný vzor bez použití prvku ASP.NET AJAX UpdatePanel.</span><span class="sxs-lookup"><span data-stu-id="69e5c-111">In a later video we will learn how to implement the same pattern without the use of the ASP.NET AJAX UpdatePanel.</span></span>

[<span data-ttu-id="69e5c-112">&#9654;Přehrát video (12 minut)</span><span class="sxs-lookup"><span data-stu-id="69e5c-112">&#9654; Watch video (12 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-implement-the-persistent-communications-pattern-with-the-updatepanel)

> [!div class="step-by-step"]
> <span data-ttu-id="69e5c-113">[Předchozí](how-do-i-use-the-conditional-updatemode-of-the-updatepanel.md)
> [Další](how-do-i-localize-an-aspnet-ajax-application.md)</span><span class="sxs-lookup"><span data-stu-id="69e5c-113">[Previous](how-do-i-use-the-conditional-updatemode-of-the-updatepanel.md)
[Next](how-do-i-localize-an-aspnet-ajax-application.md)</span></span>

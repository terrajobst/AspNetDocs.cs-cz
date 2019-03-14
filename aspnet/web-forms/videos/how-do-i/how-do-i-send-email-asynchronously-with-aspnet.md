---
uid: web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
title: '[Postup:] Odeslání e-mailu asynchronně s technologií ASP.NET | Dokumentace Microsoftu'
author: rick-anderson
description: V tomto videu pixelů na Chris ukazuje způsob použití třídy System.Net.Mail v technologii ASP.NET odesílat asynchronní e-mailovou zprávu. Nejdříve si projděte postup konfigurace web si...
ms.author: riande
ms.date: 09/24/2008
ms.assetid: 77a5c8fa-ebb2-426d-b56b-a5a98a46b516
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-send-email-asynchronously-with-aspnet
msc.type: video
ms.openlocfilehash: fc6d1d9b36eec042d1aec22e0e125e8807460a90
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57073702"
---
<a name="how-do-i-send-email-asynchronously-with-aspnet"></a><span data-ttu-id="f83a6-104">[Postup:] Odeslání e-mailu asynchronně pomocí technologie ASP.NET</span><span class="sxs-lookup"><span data-stu-id="f83a6-104">[How Do I:] Send Email Asynchronously with ASP.NET</span></span>
====================
<span data-ttu-id="f83a6-105">podle [Chris pixelů na](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="f83a6-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="f83a6-106">V tomto videu pixelů na Chris ukazuje způsob použití třídy System.Net.Mail v technologii ASP.NET odesílat asynchronní e-mailovou zprávu.</span><span class="sxs-lookup"><span data-stu-id="f83a6-106">In this video, Chris Pels shows how to use the System.Net.Mail classes in ASP.NET to send an asynchronous email message.</span></span> <span data-ttu-id="f83a6-107">Nejdříve si projděte postup konfigurace webové stránky k odesílání e-mailům prostřednictvím &lt;mailSettings&gt; element v souboru web.config.</span><span class="sxs-lookup"><span data-stu-id="f83a6-107">First, see how to configure a web site to send email using the &lt;mailSettings&gt; element in the web.config file.</span></span> <span data-ttu-id="f83a6-108">Dále vytvořte jednoduché uživatelské rozhraní pro zadávání informací o e-mailu.</span><span class="sxs-lookup"><span data-stu-id="f83a6-108">Next, create a simple user interface for entering email information.</span></span> <span data-ttu-id="f83a6-109">Naučíte se vytvářet pomocí třídy MailMessage vytvořit e-mailovou zprávu v kódu stránky.</span><span class="sxs-lookup"><span data-stu-id="f83a6-109">Then learn how to create use the MailMessage class to create an email message in the code behind for the page.</span></span> <span data-ttu-id="f83a6-110">Jako součást tohoto procesu vytvořte obslužnou rutinu události pro asynchronní zpětné volání po odeslání e-mailu.</span><span class="sxs-lookup"><span data-stu-id="f83a6-110">As part of that process create an event handler for the asynchronous callback following the sending of the email.</span></span> <span data-ttu-id="f83a6-111">Obslužná rutina události zjistit, jak použít instanci třídy AsynchCompletedEventArgs, který poskytuje informace o procesu odeslání e-mailu.</span><span class="sxs-lookup"><span data-stu-id="f83a6-111">In the event handler see how to use the instance of the AsynchCompletedEventArgs class which provides information about the email sending process.</span></span> <span data-ttu-id="f83a6-112">Nakonec odeslat testovací e-mail asynchronně, proveďte kroky v režimu ladění a zobrazení skutečné e-maily přijaté z procesu.</span><span class="sxs-lookup"><span data-stu-id="f83a6-112">Finally, send a test email asynchronously, following the steps in the debug mode, and view the actual email received from the process.</span></span>

[<span data-ttu-id="f83a6-113">&#9654;Podívejte se na video (18 minut)</span><span class="sxs-lookup"><span data-stu-id="f83a6-113">&#9654; Watch video (18 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-send-email-asynchronously-with-aspnet)

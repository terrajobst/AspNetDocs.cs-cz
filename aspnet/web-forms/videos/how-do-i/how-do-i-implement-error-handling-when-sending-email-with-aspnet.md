---
uid: web-forms/videos/how-do-i/how-do-i-implement-error-handling-when-sending-email-with-aspnet
title: '[Postupy:] Implementace zpracování chyb při odesílání e-mailů pomocí ASP.NET | Microsoft Docs'
author: rick-anderson
description: Chris pixelů na ukazuje, jak implementovat zpracování chyb při odesílání e-mailů pomocí ASP.NET. Vytvoří webovou stránku ASP.NET k odeslání e-mailu, který ukazuje, jak nakonfigurovat & lt...
ms.author: riande
ms.date: 11/06/2008
ms.assetid: c02ffd50-aa19-4cdc-b1bf-760989979a61
msc.legacyurl: /web-forms/videos/how-do-i/how-do-i-implement-error-handling-when-sending-email-with-aspnet
msc.type: video
ms.openlocfilehash: faa0daa2ffe71e58cd18bb8bed4e476ffcb1852e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78567744"
---
# <a name="how-do-i-implement-error-handling-when-sending-email-with-aspnet"></a><span data-ttu-id="922a6-104">[Postupy:] Implementace zpracování chyb při odesílání e-mailů pomocí ASP.NET</span><span class="sxs-lookup"><span data-stu-id="922a6-104">[How Do I:] Implement Error Handling when Sending Email with ASP.NET</span></span>

<span data-ttu-id="922a6-105">autor – [Chris pixelů na](https://twitter.com/chrispels)</span><span class="sxs-lookup"><span data-stu-id="922a6-105">by [Chris Pels](https://twitter.com/chrispels)</span></span>

<span data-ttu-id="922a6-106">Chris pixelů na ukazuje, jak implementovat zpracování chyb při odesílání e-mailů pomocí ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="922a6-106">Chris Pels shows how to implement error handling when sending an email with ASP.NET.</span></span> <span data-ttu-id="922a6-107">Vytvoří webovou stránku ASP.NET k odeslání e-mailu, ukazuje, jak nakonfigurovat &lt;mailSettings&gt; v souboru Web. config, popisuje třídu System .NET. mail a způsob, jakým se používá k vytváření a odesílání e-mailových zpráv.</span><span class="sxs-lookup"><span data-stu-id="922a6-107">He creates an ASP.NET web page to send email, shows how to configure &lt;mailSettings&gt; in the web.config file, describes the System.Net.Mail class and how it's used to create and send email messages.</span></span> <span data-ttu-id="922a6-108">Následně přidá zpracování chyb pomocí tříd System .NET. mail Exception, které poskytují informace o chybách, které mohou nastat při posílání e-mailů, a kontroluje výčet SmtpStatusCode, který poskytuje seznam možných výsledků při odesílání e-mailů s SmtpClient.</span><span class="sxs-lookup"><span data-stu-id="922a6-108">He then adds error handling using System.Net.Mail exception classes, which provide information about errors that can occur when sending email, and reviews the SmtpStatusCode enumeration, which provides a list of possible outcomes when sending an email with the SmtpClient.</span></span> <span data-ttu-id="922a6-109">Nakonec pošle zkušební e-mail, který vyvolá výjimku, a zkontroluje informace o zpracování chyb v ladicím programu sady Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="922a6-109">Finally, he sends a test email that raises an exception and reviews the error handling information in the Visual Studio debugger.</span></span>

[<span data-ttu-id="922a6-110">&#9654;Sledovat video (24 minut)</span><span class="sxs-lookup"><span data-stu-id="922a6-110">&#9654; Watch video (24 minutes)</span></span>](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/how-do-i-implement-error-handling-when-sending-email-with-aspnet)

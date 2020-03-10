---
uid: web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
title: Sdružování a minifikace prostředků na webu ASP.NET Web Pages (Razor) | Microsoft Docs
author: microsoft
description: Sdružování a minifikace jsou způsoby rychlejšího zprovoznění webu. Sdružování umožňuje kombinovat více souborů JavaScriptu (. js) nebo více kaskádových šablon stylů (...
ms.author: riande
ms.date: 06/21/2012
ms.assetid: 8906f1e9-4b66-4a03-8e8a-9e9debf8ed91
msc.legacyurl: /web-pages/overview/performance-and-traffic/bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site
msc.type: authoredcontent
ms.openlocfilehash: 5e42111ad71ec65581e56c73822e23ecd5fcbd58
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78635707"
---
# <a name="bundling-and-minifying-assets-in-an-aspnet-web-pages-razor-site"></a><span data-ttu-id="d2e45-104">Sdružování a minifikace prostředků na webu s webovými stránkami ASP.NET (Razor)</span><span class="sxs-lookup"><span data-stu-id="d2e45-104">Bundling and Minifying Assets in an ASP.NET Web Pages (Razor) Site</span></span>

<span data-ttu-id="d2e45-105">od [Microsoftu](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d2e45-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="d2e45-106">Sdružování a minifikace jsou způsoby rychlejšího zprovoznění webu.</span><span class="sxs-lookup"><span data-stu-id="d2e45-106">Bundling and minification are ways to make your site faster.</span></span> <span data-ttu-id="d2e45-107">Sdružování umožňuje kombinovat více souborů JavaScriptu ( *. js*) nebo více souborů kaskádových stylů ( *. CSS*), aby je bylo možné stáhnout jako jednotku, nikoli v jednom okamžiku.</span><span class="sxs-lookup"><span data-stu-id="d2e45-107">Bundling lets you combine multiple JavaScript (*.js*) files or multiple cascading style sheet (*.css*) files so that they can be downloaded as a unit, rather than one at a time.</span></span> <span data-ttu-id="d2e45-108">Minifikace roztáhne prázdné znaky a provede další typy komprese, aby stažené soubory byly co nejmenší.</span><span class="sxs-lookup"><span data-stu-id="d2e45-108">Minification squeezes out whitespace and performs other types of compression to make the downloaded files as small a possible.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="d2e45-109">Verze RC ASP.NET Web Pages 2 nepodporuje sdružování a minifikace, protože balíček obsahující požadované prvky ještě není dostupný v Microsoft WebMatrixu.</span><span class="sxs-lookup"><span data-stu-id="d2e45-109">The RC release of ASP.NET Web Pages 2 does not support bundling and minification because the package that contains the required elements is not yet available in Microsoft WebMatrix.</span></span> <span data-ttu-id="d2e45-110">Omlouváme se za tyto nepříjemnosti.</span><span class="sxs-lookup"><span data-stu-id="d2e45-110">We apologize for this inconvenience.</span></span> <span data-ttu-id="d2e45-111">V konečném vydání webových stránek ASP.NET 2 a WebMatrix 2 by měl být balíček k dispozici.</span><span class="sxs-lookup"><span data-stu-id="d2e45-111">The package is expected to be available in the final release of ASP.NET Web Pages 2 and WebMatrix 2.</span></span>

---
uid: aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
title: OWIN OAuth 2,0 – autorizační Server | Microsoft Docs
author: hongyes
description: Tento kurz vás provede postupem implementace autorizačního serveru OAuth 2,0 pomocí middlewaru OWIN OAuth. Toto je pokročilý kurz, který pouze outlin...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 20acee16-c70c-41e9-b38f-92bfcf9a4c1c
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-oauth-20-authorization-server
msc.type: authoredcontent
ms.openlocfilehash: 39c78ee57f791a94af7a5fb66c3ac42d7239760f
ms.sourcegitcommit: b95316530fa51087d6c400ff91814fe37e73f7e8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/23/2019
ms.locfileid: "70000688"
---
# <a name="owin-oauth-20-authorization-server"></a><span data-ttu-id="41a2a-104">Autorizační server OWIN OAuth 2.0</span><span class="sxs-lookup"><span data-stu-id="41a2a-104">OWIN OAuth 2.0 Authorization Server</span></span>

<span data-ttu-id="41a2a-105">[Rozhraní OAuth 2,0 Framework](http://tools.ietf.org/html/rfc6749) umožňuje aplikaci třetí strany získat omezený přístup ke službě HTTP.</span><span class="sxs-lookup"><span data-stu-id="41a2a-105">The [OAuth 2.0 framework](http://tools.ietf.org/html/rfc6749) enables a third-party app to obtain limited access to an HTTP service.</span></span> <span data-ttu-id="41a2a-106">Namísto použití přihlašovacích údajů vlastníka prostředku pro přístup k chráněnému prostředku získá klient přístupový token (což je řetězec, který označuje konkrétní obor, životnost a další atributy přístupu).</span><span class="sxs-lookup"><span data-stu-id="41a2a-106">Instead of using the resource owner's credentials to access a protected resource, the client obtains an access token (which is a string denoting a specific scope, lifetime, and other access attributes).</span></span> <span data-ttu-id="41a2a-107">Přístupové tokeny jsou vydávány klientům třetích stran pomocí autorizačního serveru se schválením vlastníka prostředku.</span><span class="sxs-lookup"><span data-stu-id="41a2a-107">Access tokens are issued to third-party clients by an authorization server with the approval of the resource owner.</span></span>

<span data-ttu-id="41a2a-108">OWIN definuje standardní rozhraní mezi webovými servery .NET a webovými aplikacemi.</span><span class="sxs-lookup"><span data-stu-id="41a2a-108">OWIN defines a standard interface between .NET web servers and web applications.</span></span> <span data-ttu-id="41a2a-109">Cílem rozhraní OWIN je oddělit Server a aplikaci, povzbuzovat vývoj jednoduchých modulů pro vývoj webů .NET a, Díky otevřenému standardu, stimuluje Open Source ekosystém nástrojů pro vývoj webových aplikací .NET.</span><span class="sxs-lookup"><span data-stu-id="41a2a-109">The goal of the OWIN interface is to decouple server and application, encourage the development of simple modules for .NET web development, and, by being an open standard, stimulate the open source ecosystem of .NET web development tools.</span></span>

<span data-ttu-id="41a2a-110">Další informace najdete v tématu [Owin](http://owin.org/) .</span><span class="sxs-lookup"><span data-stu-id="41a2a-110">For more information, see [OWIN](http://owin.org/)</span></span>

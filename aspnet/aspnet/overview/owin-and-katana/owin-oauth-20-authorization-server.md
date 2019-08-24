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
# <a name="owin-oauth-20-authorization-server"></a>Autorizační server OWIN OAuth 2.0

[Rozhraní OAuth 2,0 Framework](http://tools.ietf.org/html/rfc6749) umožňuje aplikaci třetí strany získat omezený přístup ke službě HTTP. Namísto použití přihlašovacích údajů vlastníka prostředku pro přístup k chráněnému prostředku získá klient přístupový token (což je řetězec, který označuje konkrétní obor, životnost a další atributy přístupu). Přístupové tokeny jsou vydávány klientům třetích stran pomocí autorizačního serveru se schválením vlastníka prostředku.

OWIN definuje standardní rozhraní mezi webovými servery .NET a webovými aplikacemi. Cílem rozhraní OWIN je oddělit Server a aplikaci, povzbuzovat vývoj jednoduchých modulů pro vývoj webů .NET a, Díky otevřenému standardu, stimuluje Open Source ekosystém nástrojů pro vývoj webových aplikací .NET.

Další informace najdete v tématu [Owin](http://owin.org/) .

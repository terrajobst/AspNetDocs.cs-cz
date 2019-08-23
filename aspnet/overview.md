---
uid: overview
title: Přehled ASP.NET | Microsoft Docs
author: rick-anderson
description: Seznámení s ASP.NET, bezplatnou architekturou pro vytváření webů, webových aplikací a webových rozhraní API.
ms.assetid: 3a309468-f1ca-4e51-b9c3-536af79d7a8b
ms.author: riande
ms.date: 08/10/2019
msc.legacyurl: ''
msc.type: content
ms.openlocfilehash: 9a6d08849f09c9d7a779df64f70e8770d2af3c87
ms.sourcegitcommit: b67ffd5b2c5cff01ec4c8eb12a21f693f2e11887
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/23/2019
ms.locfileid: "69995290"
---
# <a name="aspnet-overview"></a>Přehled ASP.NET

ASP.NET je bezplatná webová platforma pro vytváření skvělých webů a webových aplikací s využitím HTML, CSS a JavaScriptu. Můžete také vytvářet webová rozhraní API a používat technologie v reálném čase, jako jsou webové sokety.

[ASP.NET Core](https://docs.microsoft.com/aspnet/core/) je alternativou k ASP.NET.  Přečtěte si [pokyny k výběru mezi ASP.NET a ASP.NET Core](https://docs.microsoft.com/aspnet/core/choose-aspnet-framework).

## <a name="get-started"></a>Začínáme

Nainstalujte si [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community Edition, bezplatné integrované vývojové prostředí (IDE) pro ASP.NET ve Windows.

## <a name="websites-and-web-applications"></a>Weby a webové aplikace

 ASP.NET nabízí tři architektury pro vytváření webových aplikací: Webové formuláře, ASP.NET MVC a webové stránky ASP.NET. Všechny tři architektury jsou stabilní a vyspělé a můžete vytvořit skvělé webové aplikace pomocí kterékoli z nich. Bez ohledu na to, jakou architekturu zvolíte, získáte všechny výhody a funkce ASP.NET všude.

Každé rozhraní cílí na jiný styl vývoje. Ten, který zvolíte, závisí na kombinaci vašich programovacích prostředků (znalosti, dovednosti a vývojové prostředí), typu aplikace, kterou vytváříte, a přístupu pro vývoj, se kterým jste spokojeni.

Níže je uveden přehled každé z architektur a několik nápadů, jak mezi nimi vybírat. Pokud dáváte přednost předvedení videa, přečtěte si téma [vytváření webů pomocí ASP.NET](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/Making-Websites-with-ASPNET) a [co jsou webové nástroje?](https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/what-is-web-tools)

|   | Pokud máte zkušenosti s | Styl vývoje | Posudk |
|-----------|----------------------|-----------------------------------------------------|----------------|
| webové formuláře | Formuláře Win, WPF, .NET | Rychlý vývoj s využitím bohatých knihoven ovládacích prvků, které zapouzdřují značky HTML | Střední úroveň, pokročilá RAD |
| MVC       | Ruby na železnici, .NET  | Úplná kontrola značek HTML, kódu a značek oddělených a snadné zápisu testů. Nejlepší volba pro mobilní a jednostránkové aplikace (SPA). | Střední úroveň, rozšířené |
| Webové stránky  | Klasický ASP, PHP     | HTML značky a váš kód společně ve stejném souboru | Novinka, střední úroveň |

### <a name="web-forms"></a>webové formuláře

Pomocí webových formulářů ASP.NET můžete vytvářet dynamické weby pomocí známého modelu založeného na událostech a přetahování. Návrhová plocha a stovky ovládacích prvků a komponent vám umožní rychle vytvořit sofistikované a výkonné weby na základě uživatelského rozhraní s přístupem k datům.

[Další informace o webových formulářích](web-forms/index.md)

### <a name="mvc"></a>MVC

ASP.NET MVC poskytuje výkonný a vzorový způsob vytváření dynamických webů, který umožňuje čistě rozdělit se o obavy a poskytuje plnou kontrolu nad značkou pro užívejte a agilní vývoj. ASP.NET MVC zahrnuje řadu funkcí, které umožňují rychlý vývoj s použitím TDD pro vytváření sofistikovaných aplikací využívajících nejnovější webové standardy.

[Další informace o MVC](mvc/index.md)

### <a name="aspnet-web-pages"></a>ASP.NET – webové stránky

ASP.NET webové stránky a syntaxe Razor poskytují rychlý a snadný způsob, jak kombinovat serverový kód s HTML a vytvořit tak dynamický webový obsah. Připojte se k databázím, přidejte video, připojte se k webům sociální sítě a zahrňte spoustu dalších funkcí, které vám pomůžou vytvořit krásné weby, které odpovídají nejnovějším webovým standardům.

[Další informace o webových stránkách](web-pages/index.md)

### <a name="notes-about-web-forms-mvc-and-web-pages"></a>Poznámky k webovým formulářům, MVC a webovým stránkám

Všechny tři ASP.NET architektury jsou založené na .NET Framework a sdílejí základní funkce rozhraní .NET a ASP.NET. Například všechny tři architektury nabízejí model zabezpečení přihlášení podle členství a všechny tři sdílejí stejné možnosti pro správu požadavků, zpracování relací atd., které jsou součástí základní funkce ASP.NET.

Kromě toho tři architektury nejsou zcela nezávislé a výběr jedné z nich nevylučuje použití jiného. Vzhledem k tomu, že rozhraní můžou existovat ve stejné webové aplikaci, není běžné zobrazovat jednotlivé komponenty aplikací napsané pomocí různých rozhraní. Například zákaznické části aplikace mohou být vyvíjeny v MVC, aby bylo možné optimalizovat označení, zatímco části pro přístup k datům a správu jsou vyvíjeny ve webových formulářích pro využití výhod ovládacích prvků dat a jednoduchého přístupu k datům.

## <a name="web-apis"></a>Webová rozhraní API

Webové rozhraní API ASP.NET je rozhraní, které usnadňuje sestavování služeb HTTP, které dosáhnou široké škály klientů, včetně prohlížečů a mobilních zařízení. Webové rozhraní API ASP.NET je ideální platformou pro sestavování aplikací RESTful na .NET Framework.

[Další informace o webovém rozhraní API](web-api/index.md)

<!-- Put first under Web API TOC:  Watch video (9 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/services-and-aspnet -->

## <a name="real-time-technologies"></a>Technologie v reálném čase

ASP.NET Signal je nová knihovna pro vývojáře v ASP.NET, která usnadňuje vývoj webových funkcí v reálném čase. Signál umožňuje obousměrnou komunikaci mezi serverem a klientem. Servery můžou okamžitě nabízet obsah do připojených klientů, jakmile budou k dispozici. Signál podporuje webové sokety a vrací se k jiným kompatibilním technikům pro starší prohlížeče. Signal obsahuje rozhraní API pro správu připojení (například události připojení a odpojení), seskupování připojení a autorizaci.

[Další informace o signalizaci](signalr/index.md)

<!-- Put first under SignalR TOC:  Watch video (6 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/signalr-and-the-real-time-web -->

## <a name="mobile-apps-and-sites"></a>Mobilní aplikace a weby

ASP.NET může využívat nativní mobilní aplikace s back-end webovým rozhraním API a mobilními weby s odezvou na vývojové architektury, jako je třeba spuštění Twitteru. Pokud vytváříte nativní mobilní aplikaci, je snadné vytvořit webové rozhraní API na bázi JSON pro zpracování přístupu k datům, ověřování a nabízených oznámení pro vaši aplikaci. Pokud vytváříte reagující mobilní web, můžete použít libovolný nebo otevřený systém mřížky, který dáváte přednost, nebo můžete vybrat výkonný mobilní systém jako jQuery Mobile nebo Sencha a skvělé mobilní aplikace s PhoneGap.

[Další informace o mobilní aplikaci a vývoji webu](mobile/index.md)

<!-- Put first under mobile TOC:  Watch video (11 minutes) https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/aspnet-and-mobile -->

## <a name="single-page-applications"></a>Jednostránkové aplikace

ASP.NET aplikace (SPA) pomáhá sestavovat aplikace, které zahrnují významné interakce na straně klienta, pomocí HTML 5, šablon stylů CSS 3 a JavaScriptu. Visual Studio obsahuje šablonu pro vytváření aplikací s jedním stránkou pomocí rozhraní vyseknutí. js a ASP.NET webového rozhraní API. Kromě předdefinovaných šablon zabezpečeného ověřování hesla (Spa) jsou k dispozici také šablony zabezpečené pro vytvoření komunity, které lze stáhnout.

[Další informace o vývoji jednostránkové aplikace](single-page-application/index.md)

## <a name="webhooks"></a>WebHooky

Webhooky je zjednodušený vzor HTTP, který poskytuje jednoduchý model Pub/sub pro zapojení do společné webové rozhraní API a služeb SaaS. Když dojde k události ve službě, pošle se oznámení ve formě požadavku HTTP POST registrovaným předplatitelům. Požadavek POST obsahuje informace o události, která umožňuje příjemci reagovat odpovídajícím způsobem.

Webhooky jsou vystavené velkým počtem služeb, včetně Dropboxu, GitHubu, Instagramu, MailChimp, PayPal, časové rezervy, Trello a spousty dalších. Webhook může například značit, že se soubor změnil v Dropboxu nebo že se změnila Změna kódu na GitHubu, nebo když se v rámci služby PayPal iniciovala platba nebo byla vytvořena karta v Trello.

[Další informace o webhookech](webhooks/index.md)

<!--
Create Deployment TOC based on https://www.asp.net/aspnet/overview/deployment
Copy deployment content map to MVC, WebForms, Web Pages, Web API sections.
Copy Web Deployment in Enterprise from WebForms to MVC
Move under ASP.NET Best practices
    What not to do in ASP.NET, and what to do instead https://review.docs.microsoft.cus/aspnet/aspnet/overview/web-development-best-practices/what-not-to-do-in-aspnet-and-what-to-do-instead
    Async and await https://channel9.msdn.com/Blogs/ASP-NET-Site-Videos/async-and-await
    Building Real World Cloud Apps with Azure https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
    Hands on Lab: Maintainable Azure Websites: Managing Change and Scale https://review.docs.microsoft.com/aspnet/aspnet/overview/developing-apps-with-windows-azure/maintainable-azure-websites-managing-change-and-scale

-->

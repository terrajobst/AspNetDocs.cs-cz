---
uid: web-pages/overview/ui-layouts-and-themes/twitter-helper
title: Pomocník pro Twitter s webovými stránkami ASP.NET | Microsoft Docs
author: Rick-Anderson
description: Toto téma a aplikace ukazují, jak přidat pomocníka pro Twitter do projektu WebMatrix 3. Obsahuje pomocný kód pro Twitter a ukazuje, jak zavolat pomoc...
ms.author: riande
ms.date: 11/26/2018
ms.assetid: c1a1244e-b9c8-42e6-a00b-8456a4ec027c
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/twitter-helper
msc.type: authoredcontent
ms.openlocfilehash: 76e32b7c808467a9a87c70017dac02bdb895e1df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638556"
---
# <a name="twitter-helper-with-aspnet-web-pages"></a>Pomocná rutina Twitteru na webových stránkách ASP.NET

tím, že [FitzMacken](https://github.com/tfitzmac)

> [!IMPORTANT]
> Pomocníky pro Twitter jsou zastaralé. Nejnovější nástroje pro zapojení do Twitteru pro weby najdete v tématu [Přehled Twitteru pro websites](https://developer.twitter.com/en/docs/twitter-for-websites/overview).

> Toto téma a aplikace ukazují, jak přidat pomocníka pro Twitter do projektu WebMatrix 3. Obsahuje pomocný kód pro Twitter a ukazuje, jak volat pomocné metody.
> 
> Tento kód pro soubor Twitter. cshtml vyvinula aplikace **Tian pan** od Microsoftu.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 3
>   
> 
> Tento kurz funguje také s ASP.NET webovými stránkami 2.

## <a name="introduction"></a>Úvod

Toto téma ukazuje, jak přidat pomocníka pro Twitter do vaší aplikace a použít syntaxe Razor pro volání pomocných metod. Pomocník pro Twitter usnadňuje začleňování tlačítek a widgetů Twitteru do vaší aplikace. Pokud chcete použít pomůcku Twitteru, například časovou osu uživatele nebo výsledky hledání pro hashtag, musíte nejdřív vytvořit [widget na Twitteru](https://twitter.com/settings/widgets). Po vytvoření widgetu se zobrazí ID widgetu. Toto ID widgetu předáte jako parametr při volání pomocných metod, které znázorňují widget.

Toto téma bylo napsáno pro verzi 1,1 rozhraní API pro Twitter. Přímým přidáním pomocníka pro Twitter do projektu můžete kód pomocné rutiny aktualizovat, pokud se změní rozhraní API pro Twitter.

Informace o instalaci WebMatrixu najdete v tématu [představení ASP.NET webových stránek 2-Začínáme](../getting-started/introducing-aspnet-web-pages-2/getting-started.md).

## <a name="add-twitter-helper-to-your-project"></a>Přidat pomocníka pro Twitter do projektu

Pokud chcete přidat pomocníka pro Twitter, nejdřív přidejte do projektu složku s názvem **App\_Code** . Pak vytvořte soubor s názvem **Twitter. cshtml**.

![App_Code složka](twitter-helper/_static/image1.png)

Nahraďte výchozí kód v Twitter. cshtml následujícím kódem.

[!code-cshtml[Main](twitter-helper/samples/sample1.cshtml)]

## <a name="call-twitter-methods-from-your-web-pages"></a>Volání metod Twitteru z webových stránek

Následující příklad ukazuje způsob použití pomocných metod Twitteru ze stránky v projektu. V projektu budete chtít nahradit hodnoty parametrů hodnotami, které jsou relevantní pro vaše potřeby. Pomocí poskytnutých ID widgetů můžete prozkoumat, jak metody fungují, ale budete chtít vygenerovat vlastní widgety pro váš projekt.

Ne všechny parametry uvedené níže jsou povinné. Volitelné parametry slouží k přizpůsobení způsobu zobrazení tlačítka nebo pomůcky. Například tlačítko sledovat vyžaduje pouze zadání uživatelského jména, ale tento příklad ukazuje, jak zahrnout Počet sledujících a jak určit velikost tlačítka a jazyk.

[!code-html[Main](twitter-helper/samples/sample2.html)]

## <a name="see-the-results"></a>Zobrazení výsledků

Výše uvedený kód vytváří následující tlačítka a widgety. Tato tlačítka a widgety jsou plně funkční, nikoli snímky obrazovky. Tlačítko sledovat se zobrazí v španělštině, protože parametr Language byl nastaven na **ES**.

### <a name="follow-button"></a>Tlačítko sledovat

[Sledovat @aspnet)](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>`

### <a name="tweet-button"></a>Tlačítko pro možnost pro.

[`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + '://platform.twitter.com/widgets.js'; fjs.parentNode.insertBefore(js, fjs); } }(document, 'script', 'twitter-wjs');</script>` ve](https://twitter.com/share) stejném

### <a name="user-timeline-profile"></a>Časová osa uživatele (profil)

[Tweety podle @aspnet](https://twitter.com/aspnet)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="favorites"></a>Oblíbené položky

[Oblíbené tweety podle @Microsoft](https://twitter.com/Microsoft/favorites)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="list"></a>Seznam

[Tweety z @Microsoft/MS\_\_pásma příjemce](https://twitter.com/microsoft/ms-consumer-brands/)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

### <a name="search"></a>Hledání

[Tweety o &quot;#asp .net&quot;](https://twitter.com/search?q=%23asp.net)`<script>!function (d, s, id) { var js, fjs = d.getElementsByTagName(s)[0], p = /^http:/.test(d.location) ? 'http' : 'https'; if (!d.getElementById(id)) { js = d.createElement(s); js.id = id; js.src = p + "://platform.twitter.com/widgets.js"; fjs.parentNode.insertBefore(js, fjs); } }(document, "script", "twitter-wjs");</script>`

---
uid: web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
title: Boj proti robotyC#() | Microsoft Docs
author: wenz
description: Automatizované roboty sádry Weblogs a další weby s nevyžádanými zprávami, odesílání formulářů komentářů bez zásahu uživatele. Ovládací prvek NoBot v ASP.NET AJAX con...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 0a1917e0-884a-4576-8e93-9ed660faae51
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/nobot/fighting-bots-cs
msc.type: authoredcontent
ms.openlocfilehash: fef55edf12a024e4dd66e2a18ea371ab4dac861f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627412"
---
# <a name="fighting-bots-c"></a>Boj s roboty (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/NoBot0.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/nobot0CS.pdf)

> Automatizované roboty sádry Weblogs a další weby s nevyžádanými zprávami, odesílání formulářů komentářů bez zásahu uživatele. Ovládací prvek NoBot v ASP.NET AJAX Control Toolkit může přispět k boji s těmito robotyy.

## <a name="overview"></a>Přehled

Automatizované roboty sádry Weblogs a další weby s nevyžádanými zprávami, odesílání formulářů komentářů bez zásahu uživatele. Ovládací prvek NoBot v ASP.NET AJAX Control Toolkit může přispět k boji s těmito robotyy.

## <a name="steps"></a>Kroky

Jedním z běžných způsobů, jak předpovědět roboty, je použití CAPTCHAs plně automatizovaného testu veřejné Turing testování, které sděluje počítačům a Člověkům. Test Turing byl původně testem, který někdo potřebuje k rozhodnutí, jestli je komunikační partner člověk nebo počítač. Na webu se CAPTCHA obvykle skládá z obrázku s některými dedeformovanými písmeny. Nápad je, že písmena na obrázku může přečíst jenom člověk, zatímco algoritmy optického rozpoznávání se nezdaří.

Tento přístup má několik výhod a nevýhody, ale diskuze nad rámec tohoto kurzu. V ovládacím prvku ASP.NET AJAX Control Toolkit je však ovládací prvek, který poskytuje podobný přístup: `NoBot`. Je snazší je překonat než CAPTCHA, ale je velmi snadné použít a tarify na webech, jako jsou Blogy, kde se považují za úspěch, pokud dojde k překonání většiny nevyžádaných zpráv, které může ovládací prvek `NoBot` provádět.

`NoBot` zachycuje postback aktuálního webového formuláře ASP.NET, pokud je splněna alespoň jedna z těchto podmínek:

- Prohlížeč nedokáže vyřešit skládanku JavaScriptu (například při deaktivaci JavaScriptu).
- Uživatel odeslal formulář do funkce Fast.
- IP adresa klienta odeslala formulář příliš často v určitém časovém období.

Aby bylo možné kontrolovat tyto podmínky, ovládací prvek `NoBot` vyžaduje tyto atributy (všechny nepovinné):

- `ResponseMinimumDelaySeconds` minimální doba v sekundách mezi zpětnými odesláními
- `CutoffWindowSeconds` Délka časového intervalu, ve kterém se zpětná volání z jedné IP adresy měří
- `CutoffMaximumInstances` maximální dobu v sekundách za časový interval

Následující značka vyžaduje, aby mezi zpětnými odesláními a v intervalu 30 sekund uplynula alespoň dvě sekundy:

[!code-aspx[Main](fighting-bots-cs/samples/sample1.aspx)]

Pak jako obvykle nezapomeňte zahrnout `ScriptManager` do stránky, aby se načetla knihovna AJAX ASP.NET a mohla by se používat ovládací sada Toolkit:

[!code-aspx[Main](fighting-bots-cs/samples/sample2.aspx)]

Vzhledem k tomu, že většina kontrol `NoBot` probíhá na straně serveru, je nutné zkontrolovat výsledek těchto ověření. To lze provést voláním metody `IsValid()` `NoBot`. Má jeden argument (jako `out` parametr/`ByRef` parametr), který je typu `NoBotState`. Jeho řetězcová reprezentace obsahuje důvod, kdy se ověření nepovede, a `Valid` jinak. Následující kód vytvoří výstup zprávy podle výsledku `NoBot`:

[!code-aspx[Main](fighting-bots-cs/samples/sample3.aspx)]

Nakonec potřebujete formulář pro odeslání a označení prvku pro výstup zprávy a Vy jste hotovi.

[!code-aspx[Main](fighting-bots-cs/samples/sample4.aspx)]

Když spustíte tento skript a deaktivujete JavaScript nebo odešlete formulář během prvních dvou sekund nebo formulář odešlete do třiceti sekund, zobrazí se chybová zpráva. Tento ovládací prvek se však dá použít i v takovém případě, protože k aktivaci JavaScriptu má jenom asi 90-95% uživatelů, takže 5-10% uživatelů selže `NoBot`testu.

[![tato chybová zpráva mohla být způsobená robotem.](fighting-bots-cs/_static/image2.png)](fighting-bots-cs/_static/image1.png)

Tato chybová zpráva mohla být způsobena robotem ([kliknutím zobrazíte obrázek v plné velikosti).](fighting-bots-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Next](fighting-bots-vb.md)

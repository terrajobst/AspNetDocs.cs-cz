---
uid: web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
title: Vytvoření číselného ovládacího prvku nahoru/dolů pomocí back-endu webovéC#služby () | Microsoft Docs
author: wenz
description: Místo toho, aby uživatel zadalo zadat hodnotu do zaškrtávacího políčka, by se měl v systému Windows a jiných operačních systémech jednat o další ovládací prvek c...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: c99bbc72-d4de-41ed-92a4-9a4632368363
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/numericupdown/creating-a-numeric-up-down-control-with-a-web-service-backend-cs
msc.type: authoredcontent
ms.openlocfilehash: 816a840b9e93b95a049c3a4cb792e9deeab28983
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598884"
---
# <a name="creating-a-numeric-updown-control-with-a-web-service-backend-c"></a>Vytvoření ovládacího prvku Numeric Up/Down webovou službou typu back-end (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/numericupdown1.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/numericupdown1CS.pdf)

> Místo toho, aby uživatel zadalo zadat hodnotu do zaškrtávacího políčka, může být číselná hodnota ovládacího prvku (která existuje v systému Windows a dalších operačních systémech), a to pohodlnější. Ve výchozím nastavení ovládací prvek NumericUpDown vždycky zvyšuje nebo snižuje hodnotu o 1, ale webová služba prokáže větší flexibilitu.

## <a name="overview"></a>Přehled

Místo toho, aby uživatel zadalo zadat hodnotu do zaškrtávacího políčka, může být číselná hodnota ovládacího prvku (která existuje v systému Windows a dalších operačních systémech), a to pohodlnější. Ve výchozím nastavení `NumericUpDown` ovládací prvek vždy zvyšuje nebo snižuje hodnotu o 1, ale webová služba prokáže větší flexibilitu.

## <a name="steps"></a>Uvedené

ASP.NET AJAX Control Toolkit obsahuje rozšíření `NumericUpDown`, které do textového pole automaticky přidá dvě tlačítka: jednu pro zvýšení své hodnoty, jednu pro snížení její hodnoty. Nicméně ovládací prvek podporuje také volání webové služby (nebo volání metody stránky). Při každém kliknutí na tlačítko nahoru nebo dolů se kód JavaScriptu připojí k webovému serveru a spustí metodu. Signatura metody je následující:

[!code-csharp[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample1.cs)]

Argument `current` je aktuální hodnota v textovém poli; atribut `tag` jsou další kontextová data, která lze nastavit jako vlastnost zařízení `NumericUpDown` (ale není vyžadováno).

V této ukázce má číselný ovládací prvek číselníku jenom hodnoty, které mají dvě mocniny: 1, 2, 4, 8, 16, 32, 64 a tak dále. Proto metoda, která se spustí, když chce uživatel zvýšit hodnotu, musí mít dvojnásobek staré hodnoty; Druhá metoda musí rozdělit hodnotu dvěma. Takže tady je kompletní webová služba:

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample2.aspx)]

Nakonec vytvořte novou stránku ASP.NET. V obvyklých případech potřebujete `ScriptManager` ovládací prvek, ovládací prvek `TextBox` a ovládací prvek `NumericUpDownExtender`. V takovém případě je nutné zadat informace o webové službě:

- `ServiceDownMethod` název metody webové metody nebo stránky
- `ServiceDownPath` cesta k webové službě s metodou služby Down; vynechat, pokud používáte metodu stránky
- `ServiceUpMethod` název metody webové metody nebo metody stránky
- cesta `ServiceUpPath` k webové službě s metodou up Service; vynechat, pokud používáte metodu stránky

Zde je kompletní kód pro stránku:

[!code-aspx[Main](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/samples/sample3.aspx)]

Pokud spouštíte stránku, Všimněte si, jak se hodnota v textovém poli vždy zdvojnásobí po kliknutí na horní tlačítko a po kliknutí na tlačítko dolů se zmenší.

[![pouze čísla, která jsou mocninou 2.](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image2.png)](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image1.png)

Zobrazí se pouze čísla, která jsou mocninou 2 ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-numeric-up-down-control-with-a-web-service-backend-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Next](creating-a-numeric-up-down-control-with-a-web-service-backend-vb.md)

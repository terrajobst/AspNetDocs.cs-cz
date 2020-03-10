---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
title: Testování síly hesla (C#) | Microsoft Docs
author: wenz
description: Hesla jsou vyžadována téměř kdekoli, takže opožděným uživatelům je, aby si vyžádali jednoduchá hesla, která se snadno přeruší. Ovládací prvek PasswordStrength v ASP. N...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: cb4afbae-9b8f-483d-9729-476d4b9f85fc
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-cs
msc.type: authoredcontent
ms.openlocfilehash: e55eab9feebc18f39dd40c59cfb423208296b6c5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627293"
---
# <a name="testing-the-strength-of-a-password-c"></a>Testování síly hesla (C#)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.cs.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0CS.pdf)

> Hesla jsou vyžadována téměř kdekoli, takže opožděným uživatelům je, aby si vyžádali jednoduchá hesla, která se snadno přeruší. Ovládací prvek PasswordStrength v ASP.NET AJAX Control Toolkit může zjistit, jak dobrá je heslo.

## <a name="overview"></a>Přehled

Hesla jsou vyžadována téměř kdekoli, takže opožděným uživatelům je, aby si vyžádali jednoduchá hesla, která se snadno přeruší. Ovládací prvek `PasswordStrength` v sadě nástrojů AJAX pro ASP.NET umožňuje zjistit, jak dobrá je heslo.

## <a name="steps"></a>Kroky

Ovládací prvek `PasswordStrength` rozšiřuje textové pole a kontroluje, zda je v něm dostatečné heslo. Nabízí širokou část možností prostřednictvím atributů; Tady jsou jenom některé z nich:

- `MinimumNumericCharacters` minimální počet číselných znaků vyžadovaných v hesle
- `MinimumSymbolCharacters` minimální počet znaků symbolu (ne písmena a číslice) vyžadovaný v hesle
- `PreferredPasswordLength` minimální délka hesla
- `RequiresUpperAndLowerCaseCharacters`, zda heslo musí používat velká i malá písmena

`StrengthIndicatorType` poskytuje informace o tom, jak prezentovat sílu hesla, jako text (hodnota `"Text"`) nebo jako typ indikátoru průběhu (hodnota `"BarIndicator"`). V atributu `DisplayPosition` nakonfigurujete, kde se informace zobrazí. Tady je kompletní příklad, včetně ovládacího prvku ASP.NET AJAX `ScriptManager`, `PasswordStrength` ovládacího prvku a kurzu textového pole, ve kterém může uživatel zadat heslo. V zájmu ukázky je druhé pole formuláře běžným textovým polem a nikoli polem hesla, abyste viděli během vývoje, co píšete.

[!code-aspx[Main](testing-the-strength-of-a-password-cs/samples/sample1.aspx)]

Spustit stránku a zadat typ: pouze po zadání malých písmen, velkých písmen, číslic a symbolů se heslo považuje za nerušitelné.

[![je teď heslo (poměrně) dobré.](testing-the-strength-of-a-password-cs/_static/image2.png)](testing-the-strength-of-a-password-cs/_static/image1.png)

Nyní je heslo (poměrně) dobré ([kliknutím zobrazíte obrázek v plné velikosti).](testing-the-strength-of-a-password-cs/_static/image3.png)

> [!div class="step-by-step"]
> [Next](testing-the-strength-of-a-password-vb.md)

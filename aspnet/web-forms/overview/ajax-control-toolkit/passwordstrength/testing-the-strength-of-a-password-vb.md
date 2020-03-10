---
uid: web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
title: Testování síly hesla (VB) | Microsoft Docs
author: wenz
description: Hesla jsou vyžadována téměř kdekoli, takže opožděným uživatelům je, aby si vyžádali jednoduchá hesla, která se snadno přeruší. Ovládací prvek PasswordStrength v ASP. N...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 9215a37f-3133-4887-8ed2-3689f3a53551
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/passwordstrength/testing-the-strength-of-a-password-vb
msc.type: authoredcontent
ms.openlocfilehash: b614e1788eeafc175dd792ec6d3e4619f9ea2b7a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627300"
---
# <a name="testing-the-strength-of-a-password-vb"></a><span data-ttu-id="866fe-104">Testování síly hesla (VB)</span><span class="sxs-lookup"><span data-stu-id="866fe-104">Testing the Strength of a Password (VB)</span></span>

<span data-ttu-id="866fe-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="866fe-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="866fe-106">[Stažení kódu](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="866fe-106">[Download Code](https://download.microsoft.com/download/9/3/f/93f8daea-bebd-4821-833b-95205389c7d0/PasswordStrength0.vb.zip) or [Download PDF](https://download.microsoft.com/download/2/d/c/2dc10e34-6983-41d4-9c08-f78f5387d32b/passwordstrength0VB.pdf)</span></span>

> <span data-ttu-id="866fe-107">Hesla jsou vyžadována téměř kdekoli, takže opožděným uživatelům je, aby si vyžádali jednoduchá hesla, která se snadno přeruší.</span><span class="sxs-lookup"><span data-stu-id="866fe-107">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="866fe-108">Ovládací prvek PasswordStrength v ASP.NET AJAX Control Toolkit může zjistit, jak dobrá je heslo.</span><span class="sxs-lookup"><span data-stu-id="866fe-108">The PasswordStrength control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="overview"></a><span data-ttu-id="866fe-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="866fe-109">Overview</span></span>

<span data-ttu-id="866fe-110">Hesla jsou vyžadována téměř kdekoli, takže opožděným uživatelům je, aby si vyžádali jednoduchá hesla, která se snadno přeruší.</span><span class="sxs-lookup"><span data-stu-id="866fe-110">Passwords are required almost anywhere, so that lazy users tend to choose simple passwords which are easy to break.</span></span> <span data-ttu-id="866fe-111">Ovládací prvek `PasswordStrength` v sadě nástrojů AJAX pro ASP.NET umožňuje zjistit, jak dobrá je heslo.</span><span class="sxs-lookup"><span data-stu-id="866fe-111">The `PasswordStrength` control in the ASP.NET AJAX Control Toolkit can check how good a password is.</span></span>

## <a name="steps"></a><span data-ttu-id="866fe-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="866fe-112">Steps</span></span>

<span data-ttu-id="866fe-113">Ovládací prvek `PasswordStrength` rozšiřuje textové pole a kontroluje, zda je v něm dostatečné heslo.</span><span class="sxs-lookup"><span data-stu-id="866fe-113">The `PasswordStrength` control extends a text box and checks whether the password in it is good enough.</span></span> <span data-ttu-id="866fe-114">Nabízí širokou část možností prostřednictvím atributů; Tady jsou jenom některé z nich:</span><span class="sxs-lookup"><span data-stu-id="866fe-114">It offers a wealth of options via attributes; here are just some of them:</span></span>

- <span data-ttu-id="866fe-115">`MinimumNumericCharacters` minimální počet číselných znaků vyžadovaných v hesle</span><span class="sxs-lookup"><span data-stu-id="866fe-115">`MinimumNumericCharacters` minimum number of numeric characters required in the password</span></span>
- <span data-ttu-id="866fe-116">`MinimumSymbolCharacters` minimální počet znaků symbolu (ne písmena a číslice) vyžadovaný v hesle</span><span class="sxs-lookup"><span data-stu-id="866fe-116">`MinimumSymbolCharacters` minimum number of symbol characters (not letters and digits) required in the password</span></span>
- <span data-ttu-id="866fe-117">`PreferredPasswordLength` minimální délka hesla</span><span class="sxs-lookup"><span data-stu-id="866fe-117">`PreferredPasswordLength` minimum length of the password</span></span>
- <span data-ttu-id="866fe-118">`RequiresUpperAndLowerCaseCharacters`, zda heslo musí používat velká i malá písmena</span><span class="sxs-lookup"><span data-stu-id="866fe-118">`RequiresUpperAndLowerCaseCharacters` whether the password needs to use both uppercase and lowercase characters</span></span>

<span data-ttu-id="866fe-119">`StrengthIndicatorType` poskytuje informace o tom, jak prezentovat sílu hesla, jako text (hodnota `"Text"`) nebo jako typ indikátoru průběhu (hodnota `"BarIndicator"`).</span><span class="sxs-lookup"><span data-stu-id="866fe-119">The `StrengthIndicatorType` provides the information how to present the strength of the password, as text (value `"Text"`) or as a kind of progress bar (value `"BarIndicator"`).</span></span> <span data-ttu-id="866fe-120">V atributu `DisplayPosition` nakonfigurujete, kde se informace zobrazí.</span><span class="sxs-lookup"><span data-stu-id="866fe-120">In the `DisplayPosition` attribute, you configure where the information appears.</span></span> <span data-ttu-id="866fe-121">Tady je kompletní příklad, včetně ovládacího prvku ASP.NET AJAX `ScriptManager`, `PasswordStrength` ovládacího prvku a kurzu textového pole, ve kterém může uživatel zadat heslo.</span><span class="sxs-lookup"><span data-stu-id="866fe-121">Here is a complete example, including the ASP.NET AJAX `ScriptManager` control, the `PasswordStrength` control and of course a text box where the user may enter a password.</span></span> <span data-ttu-id="866fe-122">V zájmu ukázky je druhé pole formuláře běžným textovým polem a nikoli polem hesla, abyste viděli během vývoje, co píšete.</span><span class="sxs-lookup"><span data-stu-id="866fe-122">For the sake of demonstration, the latter form field is a regular text field and not a password field so that you can see during development what you are typing.</span></span>

[!code-aspx[Main](testing-the-strength-of-a-password-vb/samples/sample1.aspx)]

<span data-ttu-id="866fe-123">Spustit stránku a zadat typ: pouze po zadání malých písmen, velkých písmen, číslic a symbolů se heslo považuje za nerušitelné.</span><span class="sxs-lookup"><span data-stu-id="866fe-123">Run the page and type away: Only after you have entered lowercase letters, uppercase letters, digits and symbols, the password is deemed as unbreakable .</span></span>

<span data-ttu-id="866fe-124">[![je teď heslo (poměrně) dobré.](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="866fe-124">[![Now the password is (quite) good](testing-the-strength-of-a-password-vb/_static/image2.png)](testing-the-strength-of-a-password-vb/_static/image1.png)</span></span>

<span data-ttu-id="866fe-125">Nyní je heslo (poměrně) dobré ([kliknutím zobrazíte obrázek v plné velikosti).](testing-the-strength-of-a-password-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="866fe-125">Now the password is (quite) good ([Click to view full-size image](testing-the-strength-of-a-password-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="866fe-126">Předchozí</span><span class="sxs-lookup"><span data-stu-id="866fe-126">Previous</span></span>](testing-the-strength-of-a-password-cs.md)

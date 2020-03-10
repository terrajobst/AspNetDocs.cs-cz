---
uid: web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
title: Povolení pouze určitých znaků v textovém poli (VB) | Microsoft Docs
author: wenz
description: Ovládací prvky ověřování ASP.NET můžou zajistit, že ve vstupu uživatele budou povolené jenom určité znaky. To ale pořád nezabrání uživatelům v zadávání neplatných...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: 33af23f1-4016-4740-8fb2-37d1773452cd
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/filteredtextbox/allowing-only-certain-characters-in-a-text-box-vb
msc.type: authoredcontent
ms.openlocfilehash: 895708ebecc30c5f35e6ecd0349604bb777cbd93
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78613510"
---
# <a name="allowing-only-certain-characters-in-a-text-box-vb"></a><span data-ttu-id="79552-104">Povolení určitých znaků v textovém poli (VB)</span><span class="sxs-lookup"><span data-stu-id="79552-104">Allowing Only Certain Characters in a Text Box (VB)</span></span>

<span data-ttu-id="79552-105">od [Christian Wenz](https://github.com/wenz)</span><span class="sxs-lookup"><span data-stu-id="79552-105">by [Christian Wenz](https://github.com/wenz)</span></span>

<span data-ttu-id="79552-106">[Stažení kódu](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)</span><span class="sxs-lookup"><span data-stu-id="79552-106">[Download Code](https://download.microsoft.com/download/4/c/2/4c2def7a-0d23-4055-91f9-1f18504167d7/FilteredTextBox0.vb.zip) or [Download PDF](https://download.microsoft.com/download/b/6/a/b6ae89ee-df69-4c87-9bfb-ad1eb2b23373/filteredtextbox0VB.pdf)</span></span>

> <span data-ttu-id="79552-107">Ovládací prvky ověřování ASP.NET můžou zajistit, že ve vstupu uživatele budou povolené jenom určité znaky.</span><span class="sxs-lookup"><span data-stu-id="79552-107">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="79552-108">Přesto však nebrání uživatelům v zadávání neplatných znaků a pokusu o odeslání formuláře.</span><span class="sxs-lookup"><span data-stu-id="79552-108">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="overview"></a><span data-ttu-id="79552-109">Přehled</span><span class="sxs-lookup"><span data-stu-id="79552-109">Overview</span></span>

<span data-ttu-id="79552-110">Ovládací prvky ověřování ASP.NET můžou zajistit, že ve vstupu uživatele budou povolené jenom určité znaky.</span><span class="sxs-lookup"><span data-stu-id="79552-110">ASP.NET validation controls can ensure that only certain characters are allowed in user input.</span></span> <span data-ttu-id="79552-111">Přesto však nebrání uživatelům v zadávání neplatných znaků a pokusu o odeslání formuláře.</span><span class="sxs-lookup"><span data-stu-id="79552-111">However this still does not prevent users from typing invalid characters and trying to submit the form.</span></span>

## <a name="steps"></a><span data-ttu-id="79552-112">Kroky</span><span class="sxs-lookup"><span data-stu-id="79552-112">Steps</span></span>

<span data-ttu-id="79552-113">ASP.NET AJAX Control Toolkit obsahuje ovládací prvek `FilteredTextBox`, který rozšiřuje textové pole.</span><span class="sxs-lookup"><span data-stu-id="79552-113">The ASP.NET AJAX Control Toolkit contains the `FilteredTextBox` control which extends a text box.</span></span> <span data-ttu-id="79552-114">Po aktivaci lze do pole zadat pouze určitou sadu znaků.</span><span class="sxs-lookup"><span data-stu-id="79552-114">Once activated, only a certain set of characters may be entered into the field.</span></span>

<span data-ttu-id="79552-115">Aby to fungovalo, musíme nejdřív potřebovat běžný ASP.NET AJAX `ScriptManager`, který načte knihovny JavaScriptu, které jsou také používány ASP.NET AJAX Control Toolkit:</span><span class="sxs-lookup"><span data-stu-id="79552-115">For this to work, we first need as usual the ASP.NET AJAX `ScriptManager` which loads the JavaScript libraries which are also used by the ASP.NET AJAX Control Toolkit:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample1.aspx)]

<span data-ttu-id="79552-116">Pak budeme potřebovat textové pole:</span><span class="sxs-lookup"><span data-stu-id="79552-116">Then, we need a text box:</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample2.aspx)]

<span data-ttu-id="79552-117">Nakonec se `FilteredTextBoxExtender` ovládací prvek postará o omezení znaků, které může uživatel zadat.</span><span class="sxs-lookup"><span data-stu-id="79552-117">Finally, the `FilteredTextBoxExtender` control takes care of restricting the characters the user is allowed to type.</span></span> <span data-ttu-id="79552-118">Nejprve nastavte atribut `TargetControlID` na `ID` ovládacího prvku `TextBox`.</span><span class="sxs-lookup"><span data-stu-id="79552-118">First, set the `TargetControlID` attribute to the `ID` of the `TextBox` control.</span></span> <span data-ttu-id="79552-119">Pak zvolte jednu z dostupných hodnot `FilterType`:</span><span class="sxs-lookup"><span data-stu-id="79552-119">Then, choose one of the available `FilterType` values:</span></span>

- <span data-ttu-id="79552-120">`Custom` výchozí nastavení; je nutné zadat seznam platných znaků.</span><span class="sxs-lookup"><span data-stu-id="79552-120">`Custom` default; you have to provide a list of valid chars</span></span>
- <span data-ttu-id="79552-121">jenom `LowercaseLetters` jenom malá písmena</span><span class="sxs-lookup"><span data-stu-id="79552-121">`LowercaseLetters` lowercase letters only</span></span>
- <span data-ttu-id="79552-122">jenom `Numbers` číslice</span><span class="sxs-lookup"><span data-stu-id="79552-122">`Numbers` digits only</span></span>
- <span data-ttu-id="79552-123">`UppercaseLetters` pouze velká písmena</span><span class="sxs-lookup"><span data-stu-id="79552-123">`UppercaseLetters` uppercase letters only</span></span>

<span data-ttu-id="79552-124">Pokud se používá `Custom FilterType`, musí být nastavena vlastnost `ValidChars` a obsahovat seznam znaků, které mohou být zadány.</span><span class="sxs-lookup"><span data-stu-id="79552-124">If the `Custom FilterType` is used, the `ValidChars` property must be set and provide a list of characters that may be typed.</span></span> <span data-ttu-id="79552-125">Způsobem: Pokud se pokusíte vložit text do textového pole, odeberou se všechny neplatné znaky.</span><span class="sxs-lookup"><span data-stu-id="79552-125">By the way: if you try to paste text into the text box, all invalid chars are removed.</span></span>

<span data-ttu-id="79552-126">Zde je značka pro ovládací prvek `FilteredTextBoxExtender`, který povoluje pouze číslice (něco, co by bylo také možné s `FilterType="Numbers"`):</span><span class="sxs-lookup"><span data-stu-id="79552-126">Here is the markup for the `FilteredTextBoxExtender` control that only allows digits (something that would also have been possible with `FilterType="Numbers"`):</span></span>

[!code-aspx[Main](allowing-only-certain-characters-in-a-text-box-vb/samples/sample3.aspx)]

<span data-ttu-id="79552-127">Spusťte stránku a pokuste se zadat písmeno, pokud je jazyk JavaScript povolený, nebude fungovat. číslice se ale zobrazí na stránce.</span><span class="sxs-lookup"><span data-stu-id="79552-127">Run the page and try to enter a letter if JavaScript is enabled, it will not work; digits however appear on the page.</span></span> <span data-ttu-id="79552-128">Upozorňujeme však, že `FilteredTextBox` ochrany nejsou v odrážce. Pokud je JavaScript povolený, můžou být do textového pole vložená nějaká data, takže musíte použít další ověřování, tj. ASP. Ovládací prvky ověřování netto.</span><span class="sxs-lookup"><span data-stu-id="79552-128">However note that the protection `FilteredTextBox` provides is not bullet-proof: If JavaScript is enabled, any data may be entered in the text box, so you have to use additional validation means, i.e. ASP.NET's validation controls.</span></span>

<span data-ttu-id="79552-129">[![zadat lze pouze číslice.](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="79552-129">[![Only digits may be entered](allowing-only-certain-characters-in-a-text-box-vb/_static/image2.png)](allowing-only-certain-characters-in-a-text-box-vb/_static/image1.png)</span></span>

<span data-ttu-id="79552-130">Zadat lze pouze číslice ([kliknutím zobrazíte obrázek v plné velikosti).](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="79552-130">Only digits may be entered ([Click to view full-size image](allowing-only-certain-characters-in-a-text-box-vb/_static/image3.png))</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="79552-131">Předchozí</span><span class="sxs-lookup"><span data-stu-id="79552-131">Previous</span></span>](allowing-only-certain-characters-in-a-text-box-cs.md)

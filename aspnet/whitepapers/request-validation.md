---
uid: whitepapers/request-validation
title: Ověření žádosti – zabránění útokům na skripty | Microsoft Docs
author: rick-anderson
description: Tento dokument popisuje funkci ověření žádosti ASP.NET, kde ve výchozím nastavení aplikace brání v zpracování nekódovaného HTML obsahu Odeslat...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: fa429113-5f8f-4ef4-97c5-5c04900a19fa
msc.legacyurl: /whitepapers/request-validation
msc.type: content
ms.openlocfilehash: 807cccd6fe1acdd6359b014387abd3878840d4cd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640845"
---
# <a name="request-validation---preventing-script-attacks"></a><span data-ttu-id="44e8a-103">Ověření požadavku – obrana před skriptovými útoky</span><span class="sxs-lookup"><span data-stu-id="44e8a-103">Request Validation - Preventing Script Attacks</span></span>

> <span data-ttu-id="44e8a-104">Tento dokument popisuje funkci ověření žádosti ASP.NET, kde ve výchozím nastavení aplikace brání zpracování nekódovaného obsahu HTML odeslaného na server.</span><span class="sxs-lookup"><span data-stu-id="44e8a-104">This paper describes the request validation feature of ASP.NET where, by default, the application is prevented from processing unencoded HTML content submitted to the server.</span></span> <span data-ttu-id="44e8a-105">Tuto funkci ověření žádosti lze zakázat, pokud je aplikace navržena tak, aby bezpečně zpracovala data ve formátu HTML.</span><span class="sxs-lookup"><span data-stu-id="44e8a-105">This request validation feature can be disabled when the application has been designed to safely process HTML data.</span></span>
> 
> <span data-ttu-id="44e8a-106">Platí pro ASP.NET 1,1 a ASP.NET 2,0.</span><span class="sxs-lookup"><span data-stu-id="44e8a-106">Applies to ASP.NET 1.1 and ASP.NET 2.0.</span></span>

<span data-ttu-id="44e8a-107">Žádost o ověření, funkce ASP.NET od verze 1,1, brání serveru v přijetí obsahu obsahujícího nešifrovaný kód HTML.</span><span class="sxs-lookup"><span data-stu-id="44e8a-107">Request validation, a feature of ASP.NET since version 1.1, prevents the server from accepting content containing un-encoded HTML.</span></span> <span data-ttu-id="44e8a-108">Tato funkce je navržená tak, aby zabránila útokům prostřednictvím injektáže skriptu, přičemž kód skriptu nebo HTML může být nevědomě odeslán na server, uložený a následně prezentovan jiným uživatelům.</span><span class="sxs-lookup"><span data-stu-id="44e8a-108">This feature is designed to help prevent some script-injection attacks whereby client script code or HTML can be unknowingly submitted to a server, stored, and then presented to other users.</span></span> <span data-ttu-id="44e8a-109">I když je to vhodné, důrazně doporučujeme ověřit všechna vstupní data a kódování HTML.</span><span class="sxs-lookup"><span data-stu-id="44e8a-109">We still strongly recommend that you validate all input data and HTML encode it when appropriate.</span></span>

<span data-ttu-id="44e8a-110">Například vytvoříte webovou stránku, která žádá o e-mailovou adresu uživatele a uloží tuto e-mailovou adresu do databáze.</span><span class="sxs-lookup"><span data-stu-id="44e8a-110">For example, you create a Web page that requests a user's email address and then stores that email address in a database.</span></span> <span data-ttu-id="44e8a-111">Pokud uživatel zadá &lt;upozornění&gt;skriptu ("Hello ze skriptu")&lt;/SCRIPT&gt; namísto platné e-mailové adresy, když se tato data zobrazí, tento skript se dá spustit, pokud obsah není správně kódovaný.</span><span class="sxs-lookup"><span data-stu-id="44e8a-111">If the user enters &lt;SCRIPT&gt;alert("hello from script")&lt;/SCRIPT&gt; instead of a valid email address, when that data is presented, this script can be executed if the content was not properly encoded.</span></span> <span data-ttu-id="44e8a-112">Funkce ověření žádosti ASP.NET brání tomu, aby se stalo.</span><span class="sxs-lookup"><span data-stu-id="44e8a-112">The request validation feature of ASP.NET prevents this from happening.</span></span>

## <a name="why-this-feature-is-useful"></a><span data-ttu-id="44e8a-113">Proč je tato funkce užitečná</span><span class="sxs-lookup"><span data-stu-id="44e8a-113">Why this feature is useful</span></span>

<span data-ttu-id="44e8a-114">Mnoho webů neví, že jsou otevřené pro jednoduché útoky prostřednictvím injektáže skriptu.</span><span class="sxs-lookup"><span data-stu-id="44e8a-114">Many sites are not aware that they are open to simple script injection attacks.</span></span> <span data-ttu-id="44e8a-115">Bez ohledu na to, jestli je účel těchto útoků v lokalitě, zobrazením HTML, nebo na potenciálně spouštěný klientský skript pro přesměrování uživatele na web hackerů, útoky prostřednictvím injektáže skriptu jsou problémy, ke kterým musí soupeří webové vývojáře.</span><span class="sxs-lookup"><span data-stu-id="44e8a-115">Whether the purpose of these attacks is to deface the site by displaying HTML, or to potentially execute client script to redirect the user to a hacker's site, script injection attacks are a problem that Web developers must contend with.</span></span>

<span data-ttu-id="44e8a-116">Útoky prostřednictvím injektáže skriptu jsou obavy ze všech webových vývojářů, ať už používají ASP.NET, ASP nebo jiné technologie pro vývoj na webu.</span><span class="sxs-lookup"><span data-stu-id="44e8a-116">Script injection attacks are a concern of all web developers, whether they are using ASP.NET, ASP, or other web development technologies.</span></span>

<span data-ttu-id="44e8a-117">Funkce ověření žádosti ASP.NET proaktivně zabraňuje těmto útokům tím, že nepovolí zpracování nekódovaného obsahu HTML serverem, pokud se nerozhodne vývojář povolit tento obsah.</span><span class="sxs-lookup"><span data-stu-id="44e8a-117">The ASP.NET request validation feature proactively prevents these attacks by not allowing unencoded HTML content to be processed by the server unless the developer decides to allow that content.</span></span>

## <a name="what-to-expect-error-page"></a><span data-ttu-id="44e8a-118">Co očekávat: chybová stránka</span><span class="sxs-lookup"><span data-stu-id="44e8a-118">What to expect: Error Page</span></span>

<span data-ttu-id="44e8a-119">Níže uvedený snímek obrazovky ukazuje ukázkový kód ASP.NET:</span><span class="sxs-lookup"><span data-stu-id="44e8a-119">The screen shot below shows some sample ASP.NET code:</span></span>

![](request-validation/_static/image1.png)

<span data-ttu-id="44e8a-120">Výsledkem spuštění tohoto kódu je jednoduchá stránka, která umožňuje zadat nějaký text do textového pole, kliknout na tlačítko a zobrazit text v ovládacím prvku popisek:</span><span class="sxs-lookup"><span data-stu-id="44e8a-120">Running this code results in a simple page that allows you to enter some text in the textbox, click the button, and display the text in the label control:</span></span>

![](request-validation/_static/image2.png)

<span data-ttu-id="44e8a-121">Nicméně byly JavaScripty, například `<script>alert("hello!")</script>` k zadání a odeslání, by se vám zobrazila výjimka:</span><span class="sxs-lookup"><span data-stu-id="44e8a-121">However, were JavaScript, such as `<script>alert("hello!")</script>` to be entered and submitted we would get an exception:</span></span>

![](request-validation/_static/image3.png)

<span data-ttu-id="44e8a-122">Chybová zpráva uvádí, že byla zjištěna hodnota potenciálně nebezpečného nebezpečného požadavku. Form a v popisu je uveden seznam s podrobnostmi o tom, co se stalo a jak změnit chování.</span><span class="sxs-lookup"><span data-stu-id="44e8a-122">The error message states that a 'potentially dangerous Request.Form value was detected' and provides more details in the description as to exactly what occurred and how to change the behavior.</span></span> <span data-ttu-id="44e8a-123">Příklad:</span><span class="sxs-lookup"><span data-stu-id="44e8a-123">For example:</span></span>

<span data-ttu-id="44e8a-124">Ověření žádosti zjistilo potenciálně nebezpečnou vstupní hodnotu klienta a zpracování žádosti bylo přerušeno.</span><span class="sxs-lookup"><span data-stu-id="44e8a-124">Request validation has detected a potentially dangerous client input value, and processing of the request has been aborted.</span></span> <span data-ttu-id="44e8a-125">Tato hodnota může znamenat pokus o ohrožení zabezpečení aplikace, jako je například útok na skriptování mezi weby.</span><span class="sxs-lookup"><span data-stu-id="44e8a-125">This value may indicate an attempt to compromise the security of your application, such as a cross-site scripting attack.</span></span> <span data-ttu-id="44e8a-126">Ověření žádosti můžete zakázat nastavením `validateRequest=false` v direktivě stránky nebo v konfiguračním oddílu.</span><span class="sxs-lookup"><span data-stu-id="44e8a-126">You can disable request validation by setting `validateRequest=false` in the Page directive or in the configuration section.</span></span> <span data-ttu-id="44e8a-127">Důrazně však doporučujeme, aby aplikace v tomto případě explicitně kontrolovala všechny vstupy.</span><span class="sxs-lookup"><span data-stu-id="44e8a-127">However, it is strongly recommended that your application explicitly check all inputs in this case.</span></span>

## <a name="disabling-request-validation-on-a-page"></a><span data-ttu-id="44e8a-128">Zakázání ověření žádosti na stránce</span><span class="sxs-lookup"><span data-stu-id="44e8a-128">Disabling request validation on a page</span></span>

<span data-ttu-id="44e8a-129">Chcete-li zakázat ověření žádosti na stránce, je nutné nastavit atribut `validateRequest` direktivy stránky na `false`:</span><span class="sxs-lookup"><span data-stu-id="44e8a-129">To disable request validation on a page you must set the `validateRequest` attribute of the Page directive to `false`:</span></span>

[!code-aspx[Main](request-validation/samples/sample1.aspx)]

> [!CAUTION]
> <span data-ttu-id="44e8a-130">Je-li požadavek na ověření zakázán, lze obsah odeslat na stránku. je zodpovědný vývojář stránky, aby zajistil, že je obsah správně kódován nebo zpracován.</span><span class="sxs-lookup"><span data-stu-id="44e8a-130">When request validation is disabled, content can be submitted to a page; it is the responsibility of the page developer to ensure that content is properly encoded or processed.</span></span>

## <a name="disabling-request-validation-for-your-application"></a><span data-ttu-id="44e8a-131">Zakázání ověření žádosti pro vaši aplikaci</span><span class="sxs-lookup"><span data-stu-id="44e8a-131">Disabling request validation for your application</span></span>

<span data-ttu-id="44e8a-132">Chcete-li zakázat ověření žádosti pro vaši aplikaci, je nutné upravit nebo vytvořit soubor Web. config pro aplikaci a nastavit atribut validateRequest oddílu `<pages />` na `false`:</span><span class="sxs-lookup"><span data-stu-id="44e8a-132">To disable request validation for your application, you must modify or create a Web.config file for your application and set the validateRequest attribute of the `<pages />` section to `false`:</span></span>

[!code-xml[Main](request-validation/samples/sample2.xml)]

<span data-ttu-id="44e8a-133">Pokud chcete zakázat ověření žádosti pro všechny aplikace na serveru, můžete tuto úpravu provést v souboru Machine. config.</span><span class="sxs-lookup"><span data-stu-id="44e8a-133">If you wish to disable request validation for all applications on your server, you can make this modification to your Machine.config file.</span></span>

> [!CAUTION]
> <span data-ttu-id="44e8a-134">Pokud je žádost o ověření zakázána, může být obsah odeslán do aplikace. je zodpovědný za to, že vývojář aplikace zajišťuje správné kódování nebo zpracování obsahu.</span><span class="sxs-lookup"><span data-stu-id="44e8a-134">When request validation is disabled, content can be submitted to your application; it is the responsibility of the application developer to ensure that content is properly encoded or processed.</span></span>

<span data-ttu-id="44e8a-135">Následující kód je upraven pro vypnutí ověřování žádosti:</span><span class="sxs-lookup"><span data-stu-id="44e8a-135">The code below is modified to turn off request validation:</span></span>

![](request-validation/_static/image4.png)

<span data-ttu-id="44e8a-136">Nyní, pokud byl do textového pole zadán následující kód jazyka JavaScript `<script>alert("hello!")</script>` výsledek by byl:</span><span class="sxs-lookup"><span data-stu-id="44e8a-136">Now if the following JavaScript was entered into the textbox `<script>alert("hello!")</script>` the result would be:</span></span>

![](request-validation/_static/image5.png)

<span data-ttu-id="44e8a-137">Aby nedocházelo k tomu, že se ověření žádosti vypnulo, musíme obsah zakódovat ve formátu HTML.</span><span class="sxs-lookup"><span data-stu-id="44e8a-137">To prevent this from happening, with request validation turned off, we need to HTML encode the content.</span></span>

## <a name="how-to-html-encode-content"></a><span data-ttu-id="44e8a-138">Jak kódovat obsah HTML</span><span class="sxs-lookup"><span data-stu-id="44e8a-138">How to HTML encode content</span></span>

<span data-ttu-id="44e8a-139">Pokud jste zakázali ověřování žádostí, je vhodné zakódovat obsah HTML, který bude uložen pro budoucí použití.</span><span class="sxs-lookup"><span data-stu-id="44e8a-139">If you have disabled request validation, it is good practice to HTML-encode content that will be stored for future use.</span></span> <span data-ttu-id="44e8a-140">Kódování HTML automaticky nahradí všechny "&lt;" nebo "&gt;" (společně s několika dalšími symboly) odpovídající reprezentaci kódované v HTML.</span><span class="sxs-lookup"><span data-stu-id="44e8a-140">HTML encoding will automatically replace any ‘&lt;' or ‘&gt;' (together with several other symbols) with their corresponding HTML encoded representation.</span></span> <span data-ttu-id="44e8a-141">Například '&lt;' nahrazuje '&amp;lt; ' a '&gt;' je nahrazen '&amp;gt; '.</span><span class="sxs-lookup"><span data-stu-id="44e8a-141">For example, ‘&lt;' is replaced by ‘&amp;lt;' and ‘&gt;' is replaced by ‘&amp;gt;'.</span></span> <span data-ttu-id="44e8a-142">Prohlížeče používají tyto speciální kódy k zobrazení&lt;nebo&gt;v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="44e8a-142">Browsers use these special codes to display the ‘&lt;' or ‘&gt;' in the browser.</span></span>

<span data-ttu-id="44e8a-143">Obsah může být na serveru snadno kódovaný HTML pomocí rozhraní `Server.HtmlEncode(string)` API.</span><span class="sxs-lookup"><span data-stu-id="44e8a-143">Content can be easily HTML-encoded on the server using the `Server.HtmlEncode(string)` API.</span></span> <span data-ttu-id="44e8a-144">Obsah může být také snadno dekódovat HTML, to znamená vrácení zpět na standardní HTML pomocí metody `Server.HtmlDecode(string)`.</span><span class="sxs-lookup"><span data-stu-id="44e8a-144">Content can also be easily HTML-decoded, that is, reverted back to standard HTML using the `Server.HtmlDecode(string)` method.</span></span>

![](request-validation/_static/image6.png)

<span data-ttu-id="44e8a-145">Výsledek:</span><span class="sxs-lookup"><span data-stu-id="44e8a-145">Resulting in:</span></span>

![](request-validation/_static/image7.png)

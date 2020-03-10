---
uid: web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
title: Použití CAPTCHA k tomu, aby roboty z webu ASP.NET Web Razor) | Microsoft Docs
author: microsoft
description: Tento článek vysvětluje, jak používat ReCaptcha (bezpečnostní opatření) k tomu, aby nedocházelo k provádění úloh na webových stránkách ASP.NET (Razor) na...
ms.author: riande
ms.date: 05/21/2012
ms.assetid: 2b381a41-2cb3-40c0-8545-1d393e22877f
msc.legacyurl: /web-pages/overview/security/using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site
msc.type: authoredcontent
ms.openlocfilehash: 2647a3155893a3dfb3214795a5f9cf1e8931fa91
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547045"
---
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a><span data-ttu-id="e3cbb-103">Použití CAPTCHA k tomu, aby roboty z webu ASP.NET Web Razor)</span><span class="sxs-lookup"><span data-stu-id="e3cbb-103">Using a CAPTCHA to Prevent Bots from Using Your ASP.NET Web Razor) Site</span></span>

<span data-ttu-id="e3cbb-104">od [Microsoftu](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e3cbb-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="e3cbb-105">V tomto článku se dozvíte, jak používat ReCaptcha (bezpečnostní opatření) k tomu, aby se zabránilo provádění úloh na webu ASP.NET Web Pages (Razor) pomocí automatizovaných programů (roboty).</span><span class="sxs-lookup"><span data-stu-id="e3cbb-105">This article explains how to use ReCaptcha (a security measure) to prevent automated programs (bots) from performing tasks in an ASP.NET Web Pages (Razor) website.</span></span>
> 
> <span data-ttu-id="e3cbb-106">**Co se naučíte:**</span><span class="sxs-lookup"><span data-stu-id="e3cbb-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="e3cbb-107">Jak přidat CAPTCHA test na svůj web</span><span class="sxs-lookup"><span data-stu-id="e3cbb-107">How to add a CAPTCHA test to your site.</span></span>
> 
> <span data-ttu-id="e3cbb-108">Jedná se o funkce ASP.NET, které jsou představené v článku:</span><span class="sxs-lookup"><span data-stu-id="e3cbb-108">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="e3cbb-109">Pomocná rutina `ReCaptcha`</span><span class="sxs-lookup"><span data-stu-id="e3cbb-109">The `ReCaptcha` helper.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="e3cbb-110">Informace v tomto článku se vztahují na ASP.NET webové stránky 1,0 a webové stránky 2.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-110">The information in this article applies to ASP.NET Web Pages 1.0 and Web Pages 2.</span></span>

## <a name="about-captchas"></a><span data-ttu-id="e3cbb-111">O CAPTCHAs</span><span class="sxs-lookup"><span data-stu-id="e3cbb-111">About CAPTCHAs</span></span>

<span data-ttu-id="e3cbb-112">Pokaždé, když uživatelům umožníte zaregistrovat se na vašem webu, nebo dokonce jenom zadat jméno a adresu URL (například pro komentář k blogu), může dojít k zahlcení falešných názvů.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-112">Any time you let people register in your site, or even just enter a name and URL (like for a blog comment), you might get a flood of fake names.</span></span> <span data-ttu-id="e3cbb-113">Často se jedná o automatizované programy (roboty), které se snaží opustit adresy URL na každém webu, který můžou najít.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-113">These are often left by automated programs (bots) that try to leave URLs in every website they can find.</span></span> <span data-ttu-id="e3cbb-114">(Běžnou motivací je zveřejnění adres URL produktů k prodeji.)</span><span class="sxs-lookup"><span data-stu-id="e3cbb-114">(A common motivation is to post the URLs of products for sale.)</span></span>

<span data-ttu-id="e3cbb-115">Můžete se ujistit, že uživatel je skutečnými osobami a nikoli počítačový program pomocí *CAPTCHA* k ověření uživatelů při registraci nebo jiné zadání jména a webu.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-115">You can help make sure that a user is real person and not a computer program by using a *CAPTCHA* to validate users when they register or otherwise enter their name and site.</span></span> <span data-ttu-id="e3cbb-116">CAPTCHA představuje kompletní automatizovaný Turing test, který informuje počítače a lidi od sebe.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-116">CAPTCHA stands for Completely Automated Public Turing test to tell Computers and Humans Apart.</span></span> <span data-ttu-id="e3cbb-117">CAPTCHA je test *reakce na výzvu* , ve kterém se uživatel zeptá, že má něco, co může udělat, ale může to mít za následek, že je to pro automatizované programy snadné.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-117">A CAPTCHA is a *challenge-response* test in which the user is asked to do something that is easy for a person to do but hard for an automated program to do.</span></span> <span data-ttu-id="e3cbb-118">Nejběžnějším typem CAPTCHA je jedna, kde vidíte některá zkreslená písmena a jsou vyzvána k jejich zadání.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-118">The most common type of CAPTCHA is one where you see some distorted letters and are asked to type them.</span></span> <span data-ttu-id="e3cbb-119">(Deformace by měla být schopná roboty dešifrovat písmena.)</span><span class="sxs-lookup"><span data-stu-id="e3cbb-119">(The distortion is supposed to make it hard for bots to decipher the letters.)</span></span>

## <a name="adding-a-recaptcha-test"></a><span data-ttu-id="e3cbb-120">Přidání testu ReCaptcha</span><span class="sxs-lookup"><span data-stu-id="e3cbb-120">Adding a ReCaptcha Test</span></span>

<span data-ttu-id="e3cbb-121">Na stránkách ASP.NET můžete použít pomocníka `ReCaptcha` k vykreslení testu CAPTCHA, který je založen na službě ReCaptcha ([http://recaptcha.net](http://recaptcha.net)).</span><span class="sxs-lookup"><span data-stu-id="e3cbb-121">In ASP.NET pages, you can use the `ReCaptcha` helper to render a CAPTCHA test that is based on the ReCaptcha service ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="e3cbb-122">Pomocník pro `ReCaptcha` zobrazuje obrázek dvou deformovaných slov, která musí uživatelé zadat správně před ověřením stránky.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-122">The `ReCaptcha` helper displays an image of two distorted words that users have to enter correctly before the page is validated.</span></span> <span data-ttu-id="e3cbb-123">Odpověď uživatele je ověřena službou ReCaptcha.Net.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-123">The user response is validated by the ReCaptcha.Net service.</span></span>

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. <span data-ttu-id="e3cbb-124">Zaregistrujte si web na adrese ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span><span class="sxs-lookup"><span data-stu-id="e3cbb-124">Register your website at ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)).</span></span> <span data-ttu-id="e3cbb-125">Po dokončení registrace získáte veřejný klíč a soukromý klíč.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-125">When you've completed registration, you'll get a public key and a private key.</span></span>
2. <span data-ttu-id="e3cbb-126">Přidejte knihovnu webových pomocníků ASP.NET na web, jak je popsáno v [tématu Instalace pomocníků na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste to ještě neudělali.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-126">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
3. <span data-ttu-id="e3cbb-127">Pokud ještě nemáte soubor *\_AppStart. cshtml* , v kořenové složce webu vytvořte soubor s názvem *\_AppStart. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-127">If you don't already have a *\_AppStart.cshtml* file, in the root folder of a website create a file named *\_AppStart.cshtml*.</span></span>
4. <span data-ttu-id="e3cbb-128">Do souboru *\_AppStart. cshtml* přidejte následující nastavení pomocných `Recaptcha`:</span><span class="sxs-lookup"><span data-stu-id="e3cbb-128">Add the following `Recaptcha` helper settings in the *\_AppStart.cshtml* file:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. <span data-ttu-id="e3cbb-129">Nastavte `PublicKey` a vlastnosti `PrivateKey` pomocí vlastních veřejných a privátních klíčů.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-129">Set the `PublicKey` and `PrivateKey` properties using your own public and private keys.</span></span>
6. <span data-ttu-id="e3cbb-130">Uložte soubor *\_AppStart. cshtml* a zavřete ho.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-130">Save the *\_AppStart.cshtml* file and close it.</span></span>
7. <span data-ttu-id="e3cbb-131">V kořenové složce webu vytvořte novou stránku s názvem *reCAPTCHA. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-131">In the root folder of a website, create new page named *Recaptcha.cshtml*.</span></span>
8. <span data-ttu-id="e3cbb-132">Existující obsah nahraďte následujícím:</span><span class="sxs-lookup"><span data-stu-id="e3cbb-132">Replace the existing content with the following:</span></span> 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. <span data-ttu-id="e3cbb-133">Spusťte stránku *reCAPTCHA. cshtml* v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-133">Run the *Recaptcha.cshtml* page in a browser.</span></span> <span data-ttu-id="e3cbb-134">Pokud je hodnota `PrivateKey` platná, stránka zobrazí ovládací prvek ReCaptcha a tlačítko.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-134">If the `PrivateKey` value is valid, the page displays the ReCaptcha control and a button.</span></span> <span data-ttu-id="e3cbb-135">Pokud jste klíče nenastavili globálně v *\_AppStart. html*, zobrazí se na stránce chyba.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-135">If you had not set the keys globally in *\_AppStart.html*, the page would display an error.</span></span> 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. <span data-ttu-id="e3cbb-136">Zadejte slova pro test.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-136">Enter the words for the test.</span></span> <span data-ttu-id="e3cbb-137">Při předání testu ReCaptcha se zobrazí zpráva s tímto efektem.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-137">If you pass the ReCaptcha test, you see a message to that effect.</span></span> <span data-ttu-id="e3cbb-138">V opačném případě se zobrazí chybová zpráva a ovládací prvek ReCaptcha se zobrazí znovu.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-138">Otherwise you see an error message and the ReCaptcha control is redisplayed.</span></span>

> [!NOTE]
> <span data-ttu-id="e3cbb-139">Pokud je počítač v doméně, která používá proxy server, může být nutné nakonfigurovat `defaultproxy` element souboru *Web. config* .</span><span class="sxs-lookup"><span data-stu-id="e3cbb-139">If your computer is on a domain that uses proxy server, you might need to configure the `defaultproxy` element of the *Web.config* file.</span></span> <span data-ttu-id="e3cbb-140">Následující příklad ukazuje soubor *Web. config* s elementem `defaultproxy` nakonfigurovaný, aby služba reCAPTCHA mohla fungovat.</span><span class="sxs-lookup"><span data-stu-id="e3cbb-140">The following example shows a *Web.config* file with the `defaultproxy` element configured to enable the ReCaptcha service to work.</span></span>
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="e3cbb-141">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="e3cbb-141">Additional Resources</span></span>

- [<span data-ttu-id="e3cbb-142">Přizpůsobení chování na úrovni webu pro weby webových stránek ASP.NET</span><span class="sxs-lookup"><span data-stu-id="e3cbb-142">Customizing Site-Wide Behavior for ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
- [<span data-ttu-id="e3cbb-143">ReCaptcha lokalita</span><span class="sxs-lookup"><span data-stu-id="e3cbb-143">ReCaptcha site</span></span>](https://www.google.com/recaptcha)

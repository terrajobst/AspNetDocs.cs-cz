---
uid: web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
title: Přidávání sociálních sítí do webů ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Tato kapitola vysvětluje, jak integrovat svůj web se službami sociální sítě. V této kapitole se dozvíte, jak uživatelům umožnit záložku nebo propojit váš web...
ms.author: riande
ms.date: 02/21/2014
ms.assetid: 03c342f9-b35c-4d7c-b9ed-cd9aaaffedb6
msc.legacyurl: /web-pages/overview/getting-started/13-adding-social-networking-to-your-web-site
msc.type: authoredcontent
ms.openlocfilehash: 1637464b0473bba8133acbbf8918d92b4f552701
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526934"
---
# <a name="adding-social-networking-to-aspnet-web-pages-razor-sites"></a><span data-ttu-id="08f1d-104">Přidávání sociálních sítí do webů ASP.NET Web Pages (Razor)</span><span class="sxs-lookup"><span data-stu-id="08f1d-104">Adding Social Networking to ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="08f1d-105">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="08f1d-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="08f1d-106">Tento článek vysvětluje, jak přidat odkazy na sociální sítě pro Facebook, Twitter, Reddit a Digg na stránky na webu ASP.NET Web Pages (Razor) a jak zahrnout kanály Twitteru, karty Xbox hráčských a image Gravatar.</span><span class="sxs-lookup"><span data-stu-id="08f1d-106">This article explains how to add social networking links for Facebook, Twitter, Reddit, and Digg to pages in an ASP.NET Web Pages (Razor) website, and how to include Twitter feeds, Xbox gamer cards, and Gravatar images.</span></span>
> 
> <span data-ttu-id="08f1d-107">Naučíte se:</span><span class="sxs-lookup"><span data-stu-id="08f1d-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="08f1d-108">Jak umožnit lidem záložku/propojit Web</span><span class="sxs-lookup"><span data-stu-id="08f1d-108">How to let people bookmark/link your site.</span></span>
> - <span data-ttu-id="08f1d-109">Postup přidání kanálu Twitteru</span><span class="sxs-lookup"><span data-stu-id="08f1d-109">How to add a Twitter feed.</span></span>
> - <span data-ttu-id="08f1d-110">Postup přidání tlačítka Facebooku **jako** na stránky</span><span class="sxs-lookup"><span data-stu-id="08f1d-110">How to add a Facebook **Like** button to pages.</span></span>
> - <span data-ttu-id="08f1d-111">Postup vykreslování imagí Gravatar.com</span><span class="sxs-lookup"><span data-stu-id="08f1d-111">How to render Gravatar.com images.</span></span>
> - <span data-ttu-id="08f1d-112">Jak na webu zobrazit kartu Xbox hráčských</span><span class="sxs-lookup"><span data-stu-id="08f1d-112">How to display an Xbox gamer card on your site.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="08f1d-113">Verze softwaru použité v tomto kurzu</span><span class="sxs-lookup"><span data-stu-id="08f1d-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="08f1d-114">Webové stránky ASP.NET (Razor) 2</span><span class="sxs-lookup"><span data-stu-id="08f1d-114">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="08f1d-115">ASP.NET webová pomocná knihovna (balíček NuGet)</span><span class="sxs-lookup"><span data-stu-id="08f1d-115">ASP.NET Web Helper Library (NuGet package)</span></span>
>   
> 
> <span data-ttu-id="08f1d-116">Tento kurz funguje také s ASP.NET webovými stránkami 3, s výjimkou částí, které používají knihovnu webu ASP.NET Web Helper.</span><span class="sxs-lookup"><span data-stu-id="08f1d-116">This tutorial also works with ASP.NET Web Pages 3, except for parts that use the ASP.NET Web Helper Library.</span></span>

<a id="Linking_Your_Website"></a>
## <a name="linking-your-website-on-social-networking-sites"></a><span data-ttu-id="08f1d-117">Propojení webu na sítích sociální sítě</span><span class="sxs-lookup"><span data-stu-id="08f1d-117">Linking Your Website on Social Networking Sites</span></span>

<span data-ttu-id="08f1d-118">Pokud lidé jako na webu něco potřebují, často chtějí ho sdílet s přáteli.</span><span class="sxs-lookup"><span data-stu-id="08f1d-118">If people like something on your site, they often want to share it with friends.</span></span> <span data-ttu-id="08f1d-119">Díky tomu můžete snadno zobrazit glyfy (ikony), na které můžou lidé kliknout a sdílet stránku na Digg, Reddit, Facebooku, Twitteru nebo podobných lokalitách.</span><span class="sxs-lookup"><span data-stu-id="08f1d-119">You can make this easy by displaying glyphs (icons) that people can click to share a page on Digg, Reddit, Facebook, Twitter, or similar sites.</span></span>

<span data-ttu-id="08f1d-120">Chcete-li zobrazit tyto glyfy, přidejte na stránku pomocníka `LinkSharecode`.</span><span class="sxs-lookup"><span data-stu-id="08f1d-120">To display these glyphs, add the `LinkSharecode` helper to a page.</span></span> <span data-ttu-id="08f1d-121">Lidé, kteří navštíví vaši stránku, můžou kliknout na jednotlivé glyfy.</span><span class="sxs-lookup"><span data-stu-id="08f1d-121">People who visit your page can click an individual glyph.</span></span> <span data-ttu-id="08f1d-122">Pokud mají účet s tímto webem sociální sítě, může potom na tomto webu zveřejnit odkaz na vaši stránku.</span><span class="sxs-lookup"><span data-stu-id="08f1d-122">If they have an account with that social networking site, they can then post a link to your page on that site.</span></span>

![Obrázek 1](13-adding-social-networking-to-your-web-site/_static/image1.jpg)

1. <span data-ttu-id="08f1d-124">Přidejte do webu knihovnu webových pomocníků ASP.NET, jak je popsáno v [tématu Instalace pomocníků na webu webové stránky ASP.NET](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste ho ještě nepřidali.-Vytvořte stránku s názvem *ListLinkShare. cshtml* a přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="08f1d-124">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already added it.- Create a page named *ListLinkShare.cshtml* and add the following markup:</span></span>

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample1.cshtml)]

    <span data-ttu-id="08f1d-125">Pokud se v tomto příkladu spustí pomoc `LinkShare`, název stránky se předává jako parametr, který zase předává nadpis stránky sociální síti.</span><span class="sxs-lookup"><span data-stu-id="08f1d-125">In this example, when the `LinkShare` helper runs, the page title is passed as a parameter, which in turn passes the page title to the social networking site.</span></span> <span data-ttu-id="08f1d-126">Můžete však předat libovolný řetězec, který chcete.</span><span class="sxs-lookup"><span data-stu-id="08f1d-126">However, you could pass in any string you want.</span></span> <span data-ttu-id="08f1d-127">Tento příklad také určuje, které lokality sociálních sítí se mají zahrnout do seznamu.</span><span class="sxs-lookup"><span data-stu-id="08f1d-127">This example also specifies which social networking sites to include in the list.</span></span> <span data-ttu-id="08f1d-128">Můžete určit lokality sociální sítě, které jsou relevantní pro vaši lokalitu.</span><span class="sxs-lookup"><span data-stu-id="08f1d-128">You can specify the social networking sites that are relevant to your site.</span></span>
2. <span data-ttu-id="08f1d-129">Spusťte stránku *ListLinkShare. cshtml* v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="08f1d-129">Run the *ListLinkShare.cshtml* page in a browser.</span></span> <span data-ttu-id="08f1d-130">(Před spuštěním se ujistěte, že je stránka vybraná v pracovním prostoru **soubory** .)</span><span class="sxs-lookup"><span data-stu-id="08f1d-130">(Make sure the page is selected in the **Files** workspace before you run it.)</span></span>
3. <span data-ttu-id="08f1d-131">Klikněte na glyf pro jeden z webů, ke kterým jste se zaregistrovali.</span><span class="sxs-lookup"><span data-stu-id="08f1d-131">Click a glyph for one of the sites that you're signed up for.</span></span> <span data-ttu-id="08f1d-132">Odkaz vás přesměruje na stránku na vybrané sociální síti, kde můžete sdílet odkaz.</span><span class="sxs-lookup"><span data-stu-id="08f1d-132">The link takes you to the page on the selected social network site where you can share a link.</span></span> <span data-ttu-id="08f1d-133">Pokud například kliknete na odkaz Reddit, přejdete na stránku `submit to reddit` na webu Reddit.</span><span class="sxs-lookup"><span data-stu-id="08f1d-133">For example, if you click the Reddit link, you're taken to the `submit to reddit` page on the Reddit website.</span></span>

     ![Obrázek 2](13-adding-social-networking-to-your-web-site/_static/image2.jpg)

<a id="Adding_a_Twitter_Feed"></a>
## <a name="adding-a-twitter-feed"></a><span data-ttu-id="08f1d-135">Přidání kanálu Twitteru</span><span class="sxs-lookup"><span data-stu-id="08f1d-135">Adding a Twitter Feed</span></span>

<span data-ttu-id="08f1d-136">Informace o použití Pomocníka pro Twitter, který je kompatibilní s aktuální verzí rozhraní Twitter API, najdete v tématu [Pomocník pro Twitter](../ui-layouts-and-themes/twitter-helper.md).</span><span class="sxs-lookup"><span data-stu-id="08f1d-136">For information about using a Twitter helper that is compatible with the current version of the Twitter API, see [Twitter helper](../ui-layouts-and-themes/twitter-helper.md).</span></span> <span data-ttu-id="08f1d-137">Tento příklad ukazuje, jak napsat vlastní pomocný objekt, abyste mohli snadno znovu použít kód z mnoha stránek.</span><span class="sxs-lookup"><span data-stu-id="08f1d-137">This example shows how to write your own helper so you can easily reuse the code from many pages.</span></span>

<a id="Displaying_a_Facebook_Button"></a>
## <a name="displaying-a-facebook-quotlikequot-button"></a><span data-ttu-id="08f1d-138">Zobrazení &quot;na Facebooku, jako je&quot; tlačítko</span><span class="sxs-lookup"><span data-stu-id="08f1d-138">Displaying a Facebook &quot;Like&quot; Button</span></span>

<span data-ttu-id="08f1d-139">V některých případech je nejlepší možností získat kód přímo od poskytovatele sociálních sítí, ale nespoléhat se na pomocnou pomoc.</span><span class="sxs-lookup"><span data-stu-id="08f1d-139">In some cases, your best option is to get the code directly from the social networking provider rather than relying on a helper.</span></span> <span data-ttu-id="08f1d-140">To platí hlavně v případě, že poskytovatel sociálních sítí aktualizuje své možnosti rychleji, než je pomocná pomocná rutina.</span><span class="sxs-lookup"><span data-stu-id="08f1d-140">This is especially true if the social network provider updates its options more quickly than the helper is updated.</span></span>

<span data-ttu-id="08f1d-141">Chcete-li přidat funkce Facebooku (například tlačítko jako) do webu, můžete načíst fragmenty kódu z webu [Developers.Facebook.com](https://developers.facebook.com/) .</span><span class="sxs-lookup"><span data-stu-id="08f1d-141">To add Facebook features (such as the Like button) to your site, you can retrieve code snippets from the [developers.facebook.com](https://developers.facebook.com/) site.</span></span> <span data-ttu-id="08f1d-142">Na webu Facebook můžete použít jejich nástroje k vygenerování fragmentu kódu, který je relevantní pro vaši lokalitu.</span><span class="sxs-lookup"><span data-stu-id="08f1d-142">On the Facebook site, you use their tools to generate a code snippet that is relevant to your site.</span></span>

<span data-ttu-id="08f1d-143">Následující zvýrazněný kód je kód, který byl načten z nástroje tlačítko like na webu developers.facebook.com.</span><span class="sxs-lookup"><span data-stu-id="08f1d-143">The following highlighted code is the code that was retrieved from the Like Button tool on the developers.facebook.com site.</span></span> <span data-ttu-id="08f1d-144">Musíte zadat vlastní ID aplikace.</span><span class="sxs-lookup"><span data-stu-id="08f1d-144">You must provide your own app ID.</span></span>

[!code-html[Main](13-adding-social-networking-to-your-web-site/samples/sample2.html?highlight=7-14,16-17)]

<a id="Rendering_a_Gravatar_Image"></a>
## <a name="rendering-a-gravatar-image"></a><span data-ttu-id="08f1d-145">Vykreslování obrázku Gravatar</span><span class="sxs-lookup"><span data-stu-id="08f1d-145">Rendering a Gravatar Image</span></span>

<span data-ttu-id="08f1d-146">*Gravatar* (&quot;globálně rozpoznaný avatar&quot;) je obrázek, který se dá použít na více webech jako miniatura &#8212; , což je obrázek, který představuje.</span><span class="sxs-lookup"><span data-stu-id="08f1d-146">A *Gravatar* (a &quot;globally recognized avatar&quot;) is an image that can be used on multiple websites as your avatar &#8212; that is, an image that represents you.</span></span> <span data-ttu-id="08f1d-147">Gravatar může například identifikovat osobu v příspěvku fóra, v komentáři blogu atd.</span><span class="sxs-lookup"><span data-stu-id="08f1d-147">For example, a Gravatar can identify a person in a forum post, in a blog comment, and so on.</span></span> <span data-ttu-id="08f1d-148">(Vlastní Gravatar můžete zaregistrovat na webu Gravatar na adrese [http://www.gravatar.com/](http://www.gravatar.com/).) Pokud chcete zobrazit obrázky vedle jména nebo e-mailových adres uživatelů na vašem webu, můžete použít pomocníka Gravatar.</span><span class="sxs-lookup"><span data-stu-id="08f1d-148">(You can register your own Gravatar at the Gravatar website at [http://www.gravatar.com/](http://www.gravatar.com/).) If you want to display images next to people's names or email addresses on your website, you can use the Gravatar helper.</span></span>

<span data-ttu-id="08f1d-149">V tomto příkladu používáte jeden Gravatar, který představuje sebe sama.</span><span class="sxs-lookup"><span data-stu-id="08f1d-149">In this example, you're using a single Gravatar that represents yourself.</span></span> <span data-ttu-id="08f1d-150">Jiným způsobem, jak Gravatar použít, je umožnit lidem určit svou Gravatar adresu při registraci na vašem webu.</span><span class="sxs-lookup"><span data-stu-id="08f1d-150">Another way to use a Gravatar is to let people specify their Gravatar address when they register on your site.</span></span> <span data-ttu-id="08f1d-151">(Můžete se dozvědět, jak umožnit lidem registraci v [přidávání zabezpečení a členství na web webových stránek ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202904).) Až se pak zobrazí informace pro daného uživatele, stačí přidat Gravatar do místa, kde se zobrazí jméno uživatele.</span><span class="sxs-lookup"><span data-stu-id="08f1d-151">(You can learn how to let people register in [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).) Then whenever you display information for that user, you can just add the Gravatar to where you display the user's name.</span></span>

1. <span data-ttu-id="08f1d-152">Přidejte knihovnu webových pomocníků ASP.NET na web, jak je popsáno v [tématu Instalace pomocníků na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste to ještě neudělali.</span><span class="sxs-lookup"><span data-stu-id="08f1d-152">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="08f1d-153">Vytvořte novou webovou stránku s názvem *Gravatar. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="08f1d-153">Create a new web page named *Gravatar.cshtml*.</span></span>
3. <span data-ttu-id="08f1d-154">Do souboru přidejte následující kód:</span><span class="sxs-lookup"><span data-stu-id="08f1d-154">Add the following markup to the file:</span></span> 

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample3.cshtml)]

    <span data-ttu-id="08f1d-155">Metoda `Gravatar.GetHtml` zobrazí na stránce obrázek Gravatar.</span><span class="sxs-lookup"><span data-stu-id="08f1d-155">The `Gravatar.GetHtml` method displays the Gravatar image on the page.</span></span> <span data-ttu-id="08f1d-156">Chcete-li změnit velikost obrázku, můžete zahrnout číslo jako druhý parametr.</span><span class="sxs-lookup"><span data-stu-id="08f1d-156">To change the size of the image, you can include a number as a second parameter.</span></span> <span data-ttu-id="08f1d-157">Výchozí velikost je 80.</span><span class="sxs-lookup"><span data-stu-id="08f1d-157">The default size is 80.</span></span> <span data-ttu-id="08f1d-158">Čísla menší než 80 zmenší obrázek.</span><span class="sxs-lookup"><span data-stu-id="08f1d-158">Numbers less than 80 make the image smaller.</span></span> <span data-ttu-id="08f1d-159">Čísla větší než 80 nastaví obrázek větší.</span><span class="sxs-lookup"><span data-stu-id="08f1d-159">Numbers greater than 80 make the image larger.</span></span>
4. <span data-ttu-id="08f1d-160">V metodách `Gravatar.GetHtml` nahraďte `<Your Gravatar account here>` e-mailovou adresou, kterou používáte pro svůj účet Gravatar.</span><span class="sxs-lookup"><span data-stu-id="08f1d-160">In the `Gravatar.GetHtml` methods, replace `<Your Gravatar account here>` with the email address that you use for your Gravatar account.</span></span> <span data-ttu-id="08f1d-161">(Pokud nemáte účet Gravatar, můžete použít e-mailovou adresu osoby, která má.)</span><span class="sxs-lookup"><span data-stu-id="08f1d-161">(If you don't have a Gravatar account, you can use the email address of someone who does.)</span></span>
5. <span data-ttu-id="08f1d-162">Spusťte stránku v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="08f1d-162">Run the page in your browser.</span></span> <span data-ttu-id="08f1d-163">Na stránce se zobrazí dvě Gravatar image pro zadanou e-mailovou adresu.</span><span class="sxs-lookup"><span data-stu-id="08f1d-163">The page displays two Gravatar images for the email address you specified.</span></span> <span data-ttu-id="08f1d-164">Druhý obrázek je menší než první.</span><span class="sxs-lookup"><span data-stu-id="08f1d-164">The second image is smaller than the first.</span></span> 

    ![Obrázek 4](13-adding-social-networking-to-your-web-site/_static/image3.jpg)

<a id="Displaying_an_Xbox_Gamer_Card"></a>
## <a name="displaying-an-xbox-gamer-card"></a><span data-ttu-id="08f1d-166">Zobrazení karty Xbox hráčských</span><span class="sxs-lookup"><span data-stu-id="08f1d-166">Displaying an Xbox Gamer Card</span></span>

<span data-ttu-id="08f1d-167">Když lidé hrají online hry Microsoft Xbox, má každý uživatel jedinečné ID.</span><span class="sxs-lookup"><span data-stu-id="08f1d-167">When people play Microsoft Xbox games online, each user has a unique ID.</span></span> <span data-ttu-id="08f1d-168">Statistiky se uchovávají pro každý přehrávač ve formě karty hráčských, která zobrazuje jejich reputaci, skóre hráčských a nedávno přehrávané hry.</span><span class="sxs-lookup"><span data-stu-id="08f1d-168">Statistics are kept for each player in the form of a gamer card, which shows their reputation, gamer score, and recently played games.</span></span> <span data-ttu-id="08f1d-169">Pokud jste hráčských Xbox, můžete na stránkách na webu zobrazit kartu hráčských pomocí pomocné rutiny `GamerCard`.</span><span class="sxs-lookup"><span data-stu-id="08f1d-169">If you're an Xbox gamer, you can show your gamer card on pages in your site by using the `GamerCard` helper.</span></span>

1. <span data-ttu-id="08f1d-170">Přidejte knihovnu webových pomocníků ASP.NET na web, jak je popsáno v [tématu Instalace pomocníků na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste to ještě neudělali.</span><span class="sxs-lookup"><span data-stu-id="08f1d-170">Add the ASP.NET Web Helpers Library to your website as described in [Installing Helpers in an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=252372), if you haven't already.</span></span>
2. <span data-ttu-id="08f1d-171">Vytvořte novou stránku s názvem *XboxGamer. cshtml* a přidejte následující kód.</span><span class="sxs-lookup"><span data-stu-id="08f1d-171">Create a new page named *XboxGamer.cshtml* and add the following markup.</span></span>

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample4.cshtml)]

    <span data-ttu-id="08f1d-172">Vlastnost `GamerCard.GetHtml` slouží k určení aliasu pro zobrazení karty hráčských.</span><span class="sxs-lookup"><span data-stu-id="08f1d-172">You use the `GamerCard.GetHtml` property to specify the alias for the gamer card to be displayed.</span></span>
3. <span data-ttu-id="08f1d-173">Spusťte stránku v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="08f1d-173">Run the page in your browser.</span></span> <span data-ttu-id="08f1d-174">Stránka zobrazuje kartu Xbox hráčských, kterou jste zadali.</span><span class="sxs-lookup"><span data-stu-id="08f1d-174">The page displays the Xbox gamer card that you specified.</span></span>

    ![Obrázek 5](13-adding-social-networking-to-your-web-site/_static/image4.jpg)

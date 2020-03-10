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
# <a name="adding-social-networking-to-aspnet-web-pages-razor-sites"></a>Přidávání sociálních sítí do webů ASP.NET Web Pages (Razor)

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek vysvětluje, jak přidat odkazy na sociální sítě pro Facebook, Twitter, Reddit a Digg na stránky na webu ASP.NET Web Pages (Razor) a jak zahrnout kanály Twitteru, karty Xbox hráčských a image Gravatar.
> 
> Naučíte se:
> 
> - Jak umožnit lidem záložku/propojit Web
> - Postup přidání kanálu Twitteru
> - Postup přidání tlačítka Facebooku **jako** na stránky
> - Postup vykreslování imagí Gravatar.com
> - Jak na webu zobrazit kartu Xbox hráčských
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 2
> - ASP.NET webová pomocná knihovna (balíček NuGet)
>   
> 
> Tento kurz funguje také s ASP.NET webovými stránkami 3, s výjimkou částí, které používají knihovnu webu ASP.NET Web Helper.

<a id="Linking_Your_Website"></a>
## <a name="linking-your-website-on-social-networking-sites"></a>Propojení webu na sítích sociální sítě

Pokud lidé jako na webu něco potřebují, často chtějí ho sdílet s přáteli. Díky tomu můžete snadno zobrazit glyfy (ikony), na které můžou lidé kliknout a sdílet stránku na Digg, Reddit, Facebooku, Twitteru nebo podobných lokalitách.

Chcete-li zobrazit tyto glyfy, přidejte na stránku pomocníka `LinkSharecode`. Lidé, kteří navštíví vaši stránku, můžou kliknout na jednotlivé glyfy. Pokud mají účet s tímto webem sociální sítě, může potom na tomto webu zveřejnit odkaz na vaši stránku.

![Obrázek 1](13-adding-social-networking-to-your-web-site/_static/image1.jpg)

1. Přidejte do webu knihovnu webových pomocníků ASP.NET, jak je popsáno v [tématu Instalace pomocníků na webu webové stránky ASP.NET](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste ho ještě nepřidali.-Vytvořte stránku s názvem *ListLinkShare. cshtml* a přidejte následující kód:

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample1.cshtml)]

    Pokud se v tomto příkladu spustí pomoc `LinkShare`, název stránky se předává jako parametr, který zase předává nadpis stránky sociální síti. Můžete však předat libovolný řetězec, který chcete. Tento příklad také určuje, které lokality sociálních sítí se mají zahrnout do seznamu. Můžete určit lokality sociální sítě, které jsou relevantní pro vaši lokalitu.
2. Spusťte stránku *ListLinkShare. cshtml* v prohlížeči. (Před spuštěním se ujistěte, že je stránka vybraná v pracovním prostoru **soubory** .)
3. Klikněte na glyf pro jeden z webů, ke kterým jste se zaregistrovali. Odkaz vás přesměruje na stránku na vybrané sociální síti, kde můžete sdílet odkaz. Pokud například kliknete na odkaz Reddit, přejdete na stránku `submit to reddit` na webu Reddit.

     ![Obrázek 2](13-adding-social-networking-to-your-web-site/_static/image2.jpg)

<a id="Adding_a_Twitter_Feed"></a>
## <a name="adding-a-twitter-feed"></a>Přidání kanálu Twitteru

Informace o použití Pomocníka pro Twitter, který je kompatibilní s aktuální verzí rozhraní Twitter API, najdete v tématu [Pomocník pro Twitter](../ui-layouts-and-themes/twitter-helper.md). Tento příklad ukazuje, jak napsat vlastní pomocný objekt, abyste mohli snadno znovu použít kód z mnoha stránek.

<a id="Displaying_a_Facebook_Button"></a>
## <a name="displaying-a-facebook-quotlikequot-button"></a>Zobrazení &quot;na Facebooku, jako je&quot; tlačítko

V některých případech je nejlepší možností získat kód přímo od poskytovatele sociálních sítí, ale nespoléhat se na pomocnou pomoc. To platí hlavně v případě, že poskytovatel sociálních sítí aktualizuje své možnosti rychleji, než je pomocná pomocná rutina.

Chcete-li přidat funkce Facebooku (například tlačítko jako) do webu, můžete načíst fragmenty kódu z webu [Developers.Facebook.com](https://developers.facebook.com/) . Na webu Facebook můžete použít jejich nástroje k vygenerování fragmentu kódu, který je relevantní pro vaši lokalitu.

Následující zvýrazněný kód je kód, který byl načten z nástroje tlačítko like na webu developers.facebook.com. Musíte zadat vlastní ID aplikace.

[!code-html[Main](13-adding-social-networking-to-your-web-site/samples/sample2.html?highlight=7-14,16-17)]

<a id="Rendering_a_Gravatar_Image"></a>
## <a name="rendering-a-gravatar-image"></a>Vykreslování obrázku Gravatar

*Gravatar* (&quot;globálně rozpoznaný avatar&quot;) je obrázek, který se dá použít na více webech jako miniatura &#8212; , což je obrázek, který představuje. Gravatar může například identifikovat osobu v příspěvku fóra, v komentáři blogu atd. (Vlastní Gravatar můžete zaregistrovat na webu Gravatar na adrese [http://www.gravatar.com/](http://www.gravatar.com/).) Pokud chcete zobrazit obrázky vedle jména nebo e-mailových adres uživatelů na vašem webu, můžete použít pomocníka Gravatar.

V tomto příkladu používáte jeden Gravatar, který představuje sebe sama. Jiným způsobem, jak Gravatar použít, je umožnit lidem určit svou Gravatar adresu při registraci na vašem webu. (Můžete se dozvědět, jak umožnit lidem registraci v [přidávání zabezpečení a členství na web webových stránek ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202904).) Až se pak zobrazí informace pro daného uživatele, stačí přidat Gravatar do místa, kde se zobrazí jméno uživatele.

1. Přidejte knihovnu webových pomocníků ASP.NET na web, jak je popsáno v [tématu Instalace pomocníků na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste to ještě neudělali.
2. Vytvořte novou webovou stránku s názvem *Gravatar. cshtml*.
3. Do souboru přidejte následující kód: 

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample3.cshtml)]

    Metoda `Gravatar.GetHtml` zobrazí na stránce obrázek Gravatar. Chcete-li změnit velikost obrázku, můžete zahrnout číslo jako druhý parametr. Výchozí velikost je 80. Čísla menší než 80 zmenší obrázek. Čísla větší než 80 nastaví obrázek větší.
4. V metodách `Gravatar.GetHtml` nahraďte `<Your Gravatar account here>` e-mailovou adresou, kterou používáte pro svůj účet Gravatar. (Pokud nemáte účet Gravatar, můžete použít e-mailovou adresu osoby, která má.)
5. Spusťte stránku v prohlížeči. Na stránce se zobrazí dvě Gravatar image pro zadanou e-mailovou adresu. Druhý obrázek je menší než první. 

    ![Obrázek 4](13-adding-social-networking-to-your-web-site/_static/image3.jpg)

<a id="Displaying_an_Xbox_Gamer_Card"></a>
## <a name="displaying-an-xbox-gamer-card"></a>Zobrazení karty Xbox hráčských

Když lidé hrají online hry Microsoft Xbox, má každý uživatel jedinečné ID. Statistiky se uchovávají pro každý přehrávač ve formě karty hráčských, která zobrazuje jejich reputaci, skóre hráčských a nedávno přehrávané hry. Pokud jste hráčských Xbox, můžete na stránkách na webu zobrazit kartu hráčských pomocí pomocné rutiny `GamerCard`.

1. Přidejte knihovnu webových pomocníků ASP.NET na web, jak je popsáno v [tématu Instalace pomocníků na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste to ještě neudělali.
2. Vytvořte novou stránku s názvem *XboxGamer. cshtml* a přidejte následující kód.

    [!code-cshtml[Main](13-adding-social-networking-to-your-web-site/samples/sample4.cshtml)]

    Vlastnost `GamerCard.GetHtml` slouží k určení aliasu pro zobrazení karty hráčských.
3. Spusťte stránku v prohlížeči. Stránka zobrazuje kartu Xbox hráčských, kterou jste zadali.

    ![Obrázek 5](13-adding-social-networking-to-your-web-site/_static/image4.jpg)

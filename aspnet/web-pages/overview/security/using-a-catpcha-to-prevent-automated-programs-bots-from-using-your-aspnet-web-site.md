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
# <a name="using-a-captcha-to-prevent-bots-from-using-your-aspnet-web-razor-site"></a>Použití CAPTCHA k tomu, aby roboty z webu ASP.NET Web Razor)

od [Microsoftu](https://github.com/microsoft)

> V tomto článku se dozvíte, jak používat ReCaptcha (bezpečnostní opatření) k tomu, aby se zabránilo provádění úloh na webu ASP.NET Web Pages (Razor) pomocí automatizovaných programů (roboty).
> 
> **Co se naučíte:** 
> 
> - Jak přidat CAPTCHA test na svůj web
> 
> Jedná se o funkce ASP.NET, které jsou představené v článku:
> 
> - Pomocná rutina `ReCaptcha`
> 
> > [!NOTE]
> > Informace v tomto článku se vztahují na ASP.NET webové stránky 1,0 a webové stránky 2.

## <a name="about-captchas"></a>O CAPTCHAs

Pokaždé, když uživatelům umožníte zaregistrovat se na vašem webu, nebo dokonce jenom zadat jméno a adresu URL (například pro komentář k blogu), může dojít k zahlcení falešných názvů. Často se jedná o automatizované programy (roboty), které se snaží opustit adresy URL na každém webu, který můžou najít. (Běžnou motivací je zveřejnění adres URL produktů k prodeji.)

Můžete se ujistit, že uživatel je skutečnými osobami a nikoli počítačový program pomocí *CAPTCHA* k ověření uživatelů při registraci nebo jiné zadání jména a webu. CAPTCHA představuje kompletní automatizovaný Turing test, který informuje počítače a lidi od sebe. CAPTCHA je test *reakce na výzvu* , ve kterém se uživatel zeptá, že má něco, co může udělat, ale může to mít za následek, že je to pro automatizované programy snadné. Nejběžnějším typem CAPTCHA je jedna, kde vidíte některá zkreslená písmena a jsou vyzvána k jejich zadání. (Deformace by měla být schopná roboty dešifrovat písmena.)

## <a name="adding-a-recaptcha-test"></a>Přidání testu ReCaptcha

Na stránkách ASP.NET můžete použít pomocníka `ReCaptcha` k vykreslení testu CAPTCHA, který je založen na službě ReCaptcha ([http://recaptcha.net](http://recaptcha.net)). Pomocník pro `ReCaptcha` zobrazuje obrázek dvou deformovaných slov, která musí uživatelé zadat správně před ověřením stránky. Odpověď uživatele je ověřena službou ReCaptcha.Net.

![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.jpg)

1. Zaregistrujte si web na adrese ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)). Po dokončení registrace získáte veřejný klíč a soukromý klíč.
2. Přidejte knihovnu webových pomocníků ASP.NET na web, jak je popsáno v [tématu Instalace pomocníků na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste to ještě neudělali.
3. Pokud ještě nemáte soubor *\_AppStart. cshtml* , v kořenové složce webu vytvořte soubor s názvem *\_AppStart. cshtml*.
4. Do souboru *\_AppStart. cshtml* přidejte následující nastavení pomocných `Recaptcha`: 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample1.cshtml?highlight=6-7)]
5. Nastavte `PublicKey` a vlastnosti `PrivateKey` pomocí vlastních veřejných a privátních klíčů.
6. Uložte soubor *\_AppStart. cshtml* a zavřete ho.
7. V kořenové složce webu vytvořte novou stránku s názvem *reCAPTCHA. cshtml*.
8. Existující obsah nahraďte následujícím: 

    [!code-cshtml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample2.cshtml)]
9. Spusťte stránku *reCAPTCHA. cshtml* v prohlížeči. Pokud je hodnota `PrivateKey` platná, stránka zobrazí ovládací prvek ReCaptcha a tlačítko. Pokud jste klíče nenastavili globálně v *\_AppStart. html*, zobrazí se na stránce chyba. 

    ![](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/_static/image1.png)
10. Zadejte slova pro test. Při předání testu ReCaptcha se zobrazí zpráva s tímto efektem. V opačném případě se zobrazí chybová zpráva a ovládací prvek ReCaptcha se zobrazí znovu.

> [!NOTE]
> Pokud je počítač v doméně, která používá proxy server, může být nutné nakonfigurovat `defaultproxy` element souboru *Web. config* . Následující příklad ukazuje soubor *Web. config* s elementem `defaultproxy` nakonfigurovaný, aby služba reCAPTCHA mohla fungovat.
> 
> [!code-xml[Main](using-a-catpcha-to-prevent-automated-programs-bots-from-using-your-aspnet-web-site/samples/sample3.xml)]

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Další prostředky

- [Přizpůsobení chování na úrovni webu pro weby webových stránek ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202906)
- [ReCaptcha lokalita](https://www.google.com/recaptcha)

---
uid: web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
title: Přihlášení pomocí externích webů na webu ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Tento článek vysvětluje, jak se přihlásit k webu ASP.NET Web Pages (Razor) pomocí Facebooku, Google, Twitteru, Yahoo a dalších webů – to znamená, jak podporovat...
ms.author: riande
ms.date: 02/21/2014
ms.assetid: ef852096-a5bf-47b3-9945-125cde065093
msc.legacyurl: /web-pages/overview/security/enabling-login-from-external-sites-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 860b75422c3df1d191ed861344963bfc19270e8f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638752"
---
# <a name="logging-in-using-external-sites-in-an-aspnet-web-pages-razor-site"></a>Přihlášení pomocí externích webů na webu ASP.NET Web Pages (Razor)

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek vysvětluje, jak se přihlásit k webu ASP.NET Web Pages (Razor) pomocí Facebooku, Google, Twitteru, Yahoo a dalších webů – to znamená, jak podporovat OAuth a OpenID ve vaší lokalitě.
> 
> Naučíte se:
> 
> - Jak povolit přihlášení z jiných webů při použití šablony webu WebMatrix Starter
> 
> Toto je funkce ASP.NET představená v článku:
> 
> - Pomocná rutina `OAuthWebSecurity`
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 2
> - WebMatrix 3

Webové stránky ASP.NET zahrnují podporu pro poskytovatele [OAuth](http://oauth.net/) a [OpenID](http://openid.net/) . Pomocí těchto poskytovatelů můžete uživatelům umožnit, aby se k webu přihlásili pomocí svých stávajících přihlašovacích údajů z Facebooku, Twitteru, Microsoftu a Google. Například pro přihlášení pomocí účtu Facebook mohou uživatelé vybrat ikonu Facebook, která je přesměruje na přihlašovací stránku Facebooku, kde zadá informace o uživateli. Pak můžou přidružit přihlášení ke službě Facebook ke svému účtu na vašem webu. Související vylepšení funkcí členství na webových stránkách je, že uživatelé můžou přidružit k jednomu účtu na svém webu několik přihlášení (včetně přihlášení ze sítí sociální sítě).

Tento obrázek ukazuje přihlašovací stránku ze šablony **úvodní lokality** , kde si uživatel může vybrat ikonu Facebook, Twitter, Google nebo Microsoft a povolit přihlášení pomocí externího účtu:

![externí zprostředkovatelé](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image1.png)

Můžete povolit členství OAuth a OpenID tím, že Odkomentujete pár řádků kódu v šabloně **webu Starter** . Metody a vlastnosti, které používáte pro práci s poskytovateli OAuth a OpenID, jsou v třídě `WebMatrix.Security.OAuthWebSecurity`. Šablona **úvodní lokality** obsahuje úplnou infrastrukturu členství, úplnou na přihlašovací stránce, databázi členství a veškerý kód, který potřebujete, aby se uživatelé mohli přihlásit k webu pomocí místních přihlašovacích údajů nebo z jiné lokality.

V této části najdete příklad toho, jak umožnit uživatelům přihlašovat se z externích lokalit na lokalitu, která je založená na šabloně **webu Starter** . Po vytvoření webu počáteční web to uděláte (podrobnosti následují):

- Pro lokality, které používají poskytovatele OAuth (Facebook, Twitter a Microsoft), vytvoříte aplikaci na externím webu. Tím získáte klíče aplikací, které budete potřebovat k vyvolání funkce přihlášení pro tyto lokality.
- Pro lokality, které používají poskytovatele OpenID (Google), není nutné vytvářet aplikace. Pro všechny tyto weby musíte mít účet, abyste se mohli přihlásit a vytvářet vývojářské aplikace.

    > [!NOTE]
    > Aplikace Microsoftu přijímají pro pracovní web pouze živou adresu URL, takže pro testování přihlášení nemůžete použít adresu URL místního webu.
- Upravte několik souborů na webu za účelem určení vhodného poskytovatele ověřování a odeslání přihlašovacích údajů na lokalitu, kterou chcete použít.

Tento článek poskytuje samostatné pokyny pro následující úlohy:

- [Povolení přihlášení Google](#To_enable_Google_logins)
- [Povolení přihlášení na Facebooku](#To_enable_Facebook_logins)
- [Povolení přihlášení k Twitteru](#To_enable_Twitter_logins)

<a id="To_enable_Google_logins"></a>
## <a name="enabling-google-logins"></a>Povolení přihlášení Google

1. Vytvořte nebo otevřete web ASP.NET Web Pages založený na šabloně webu WebMatrix Starter.
2. Otevřete stránku *\_AppStart. cshtml* a odkomentujte následující řádek kódu. 

    [!code-css[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample1.css)]

### <a name="testing-google-login"></a>Testování přihlášení Google

1. Spusťte stránku *Default. cshtml* vaší lokality a klikněte na tlačítko **Přihlásit** se.
2. Na *přihlašovací* stránce v části **použít jinou službu pro přihlášení** vyberte tlačítko Odeslat **Google** nebo **Yahoo** . V tomto příkladu se používá přihlášení Google. 

    Webová stránka přesměruje požadavek na přihlašovací stránku Google.

    ![Přihlášení Google](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image2.png)
3. Zadejte přihlašovací údaje pro existující účet Google.
4. Pokud se Google zeptá, jestli chcete, aby *localhost* mohl používat informace z účtu, klikněte na tlačítko **povoleno**.

    Kód používá k ověření uživatele token Google a pak se na tuto stránku vrátí na vašem webu. Tato stránka umožňuje uživatelům přidružit ke stávajícímu účtu na vašem webu svoje přihlašovací údaje Google, nebo můžou zaregistrovat nový účet a přidružit k externímu přihlášení.

    ![OAuth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image3.png)
5. Klikněte na tlačítko **přidružit** . Prohlížeč se vrátí na domovskou stránku vaší aplikace.

<a id="To_enable_Facebook_logins"></a>
## <a name="enabling-facebook-logins"></a>Povolení přihlášení na Facebooku

1. Přejít na [web pro vývojáře na Facebooku](https://developers.facebook.com/apps) (Přihlaste se, pokud ještě nejste přihlášení).
2. Klikněte na tlačítko **vytvořit novou aplikaci** a potom podle pokynů pojmenujte a vytvořte novou aplikaci.
3. V části **Vyberte, jak bude vaše aplikace integrována s Facebooku**, a zvolte část **Web** .
4. Do pole **Adresa URL webu** zadejte adresu URL vašeho webu (například `http://www.example.com`). Pole **doména** je volitelné. tuto možnost můžete použít k zajištění ověřování pro celou doménu (například *example.com*). 

    > [!NOTE]
    > Pokud používáte web na místním počítači s adresou URL, jako je například `http://localhost:12345` (kde číslo je číslo místního portu), můžete tuto hodnotu přidat do pole **Adresa URL webu** pro testování webu. Při každé změně čísla portu v místní lokalitě budete ale muset aktualizovat pole **Adresa URL webu** vaší aplikace.
5. Klikněte na tlačítko **Uložit změny** .
6. Zvolte znovu kartu **aplikace** a pak zobrazte úvodní stránku aplikace.
7. Zkopírujte **ID aplikace** a **tajné** hodnoty pro aplikaci a vložte je do dočasného textového souboru. Tyto hodnoty předáte poskytovateli Facebooku ve vašem kódu webu.
8. Zavřete web pro vývojáře Facebooku.

Teď provedete změny dvou stránek na webu tak, aby se uživatelé mohli přihlásit k webu pomocí svých účtů Facebook.

1. Vytvořte nebo otevřete web ASP.NET Web Pages založený na šabloně webu WebMatrix Starter.
2. Otevřete stránku *\_AppStart. cshtml* a Odkomentujte kód pro poskytovatele OAuth pro Facebook. Blok kódu, který není v komentáři, vypadá takto: 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample2.cs)]
3. Zkopírujte hodnotu **ID aplikace** z aplikace Facebook jako hodnotu parametru `appId` (uvnitř uvozovek).
4. Zkopírujte hodnotu **tajného klíče aplikace** z aplikace Facebook jako hodnotu parametru `appSecret`.
5. Uložte soubor a zavřete ho.

### <a name="testing-facebook-login"></a>Testování přihlašovacích údajů Facebooku

1. Spusťte stránku *Default. cshtml* webu a klikněte na tlačítko **Přihlásit** .
2. Na *přihlašovací* stránce v části **použít jinou službu pro přihlášení** vyberte ikonu **Facebook** . 

    Webová stránka přesměruje požadavek na přihlašovací stránku Facebooku.

    ![OAuth – 2](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image4.png)
3. Přihlaste se k účtu Facebook. 

    Kód používá token Facebooku k ověření a pak se vrátí na stránku, kde můžete přidružit své přihlášení ke službě Facebook k přihlašovacím údajům vašeho webu. Vaše uživatelské jméno nebo e-mailová adresa se vyplní do pole **e-mail** ve formuláři.

    ![OAuth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image5.png)
4. Klikněte na tlačítko **přidružit** . 

    Prohlížeč se vrátí na domovskou stránku a Vy jste přihlášení.

<a id="To_enable_Twitter_logins"></a>
## <a name="enabling-twitter-logins"></a>Povolení přihlášení k Twitteru

1. Přejděte na [web pro vývojáře na Twitteru](https://dev.twitter.com/).
2. Zvolte odkaz **vytvořit aplikaci** a pak se přihlaste k webu.
3. Ve formuláři **vytvořit aplikaci** vyplňte pole **název** a **Popis** .
4. Do pole **Web** zadejte adresu URL vašeho webu (například `http://www.example.com`). 

    > [!NOTE]
    > Pokud testujete lokalitu místně (pomocí adresy URL, jako je `http://localhost:12345`), Twitter nemusí přijmout adresu URL. Může ale být možné použít IP adresu místní zpětné smyčky (například `http://127.0.0.1:12345`). Tím se zjednoduší proces testování aplikace místně. Pokaždé, když se změní číslo portu místní lokality, budete muset aktualizovat pole **Web** vaší aplikace.
5. V poli **Adresa URL zpětného volání** zadejte adresu URL stránky na webu, na kterou se mají uživatelé vracet po přihlášení do Twitteru. Chcete-li například odeslat uživatele na domovskou stránku úvodní lokality (která rozpozná jejich stav přihlášení), zadejte stejnou adresu URL, kterou jste zadali do pole **Web** .
6. Přijměte podmínky a klikněte na tlačítko **vytvořit aplikaci Twitter** .
7. Na úvodní stránce **Moje aplikace** vyberte aplikaci, kterou jste vytvořili.
8. Na kartě **Podrobnosti** se posuňte do dolní části a klikněte na tlačítko **vytvořit vlastní přístupový token** .
9. Na kartě **Podrobnosti** zkopírujte **klíč příjemce** a **tajné hodnoty příjemce** pro vaši aplikaci a vložte je do dočasného textového souboru. Tyto hodnoty předáte poskytovateli Twitteru v kódu vašeho webu.
10. Ukončete Web Twitter.

Teď provedete změny dvou stránek na webu tak, aby se uživatelé mohli přihlásit k webu pomocí svých účtů Twitteru.

1. Vytvořte nebo otevřete web ASP.NET Web Pages založený na šabloně webu WebMatrix Starter.
2. Otevřete stránku *\_AppStart. cshtml* a Odkomentujte kód pro poskytovatele služby Twitter OAuth. Blok kódu, který není v komentáři, vypadá takto: 

    [!code-csharp[Main](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/samples/sample3.cs)]
3. Zkopírujte hodnotu **klíč příjemce** z aplikace Twitter jako hodnotu parametru `consumerKey` (uvnitř uvozovek).
4. Zkopírujte hodnotu **tajného klíče příjemce** z aplikace Twitter jako hodnotu parametru `consumerSecret`.
5. Uložte soubor a zavřete ho.

### <a name="testing-twitter-login"></a>Testování přihlášení k Twitteru

1. Spusťte stránku *Default. cshtml* vaší lokality a klikněte na tlačítko pro **přihlášení** .
2. Na *přihlašovací* stránce v části **použít jinou službu pro přihlášení** vyberte ikonu **Twitteru** . 

    Webová stránka přesměruje požadavek na přihlašovací stránku na Twitteru pro vytvořenou aplikaci.

    ![OAuth-4](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image6.png)
3. Přihlaste se k účtu na Twitteru.
4. Tento kód k ověření uživatele používá token Twitteru a potom se vrátí na stránku, kde můžete přidružit vaše přihlášení k vašemu účtu webu. Vaše jméno nebo e-mailová adresa se vyplní do pole **e-mail** ve formuláři.

    ![OAuth-5](enabling-login-from-external-sites-in-an-aspnet-web-pages-site/_static/image7.png)
5. Klikněte na tlačítko **přidružit** . 

    Prohlížeč se vrátí na domovskou stránku a Vy jste přihlášení.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Další prostředky

- [Přizpůsobení chování v celém webu](https://go.microsoft.com/fwlink/?LinkId=202906)
- [Přidání zabezpečení a členství do webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkID=202904)

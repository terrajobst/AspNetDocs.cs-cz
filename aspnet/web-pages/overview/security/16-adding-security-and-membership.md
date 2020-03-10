---
uid: web-pages/overview/security/16-adding-security-and-membership
title: Přidání zabezpečení a členství do webu ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: V této kapitole se dozvíte, jak web zabezpečit, aby byly některé stránky k dispozici pouze uživatelům, kteří se přihlašují. (Uvidíte také, jak vytvářet stránky...
ms.author: riande
ms.date: 02/24/2014
ms.assetid: 7a77c2c0-deea-4290-a9c3-97958891758e
msc.legacyurl: /web-pages/overview/security/16-adding-security-and-membership
msc.type: authoredcontent
ms.openlocfilehash: 0be3e767a42939a3c343f6d4a730eb1d9a6b367c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628385"
---
# <a name="adding-security-and-membership-to-an-aspnet-web-pages-razor-site"></a>Přidání zabezpečení a členství do webu ASP.NET Web Pages (Razor)

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek vysvětluje, jak zabezpečit webovou stránku ASP.NET Web Pages (Razor), aby byly některé stránky k dispozici pouze uživatelům, kteří se přihlašují. (Zobrazí se také informace o tom, jak vytvořit stránky, ke kterým má kdokoli přístup.)
> 
> **Co se naučíte:** 
> 
> - Postup vytvoření webu, který má registrační stránku a přihlašovací stránku, aby bylo možné pro některé stránky omezit přístup pouze na členy.
> - Jak vytvořit veřejné a jenom členské stránky.
> - Jak definovat role, které jsou skupiny, které mají odlišná oprávnění zabezpečení na webu a jak přiřadit uživatele k roli.
> - Jak používat CAPTCHA k zabránění automatizovaným programům (roboty) z vytváření členských účtů.
>   
> 
> Jedná se o funkce ASP.NET, které jsou představené v článku:
> 
> - Šablona webu WebMatrix **Starter**
> - Pomocná třída `WebSecurity` a `Roles`.
> - Pomocná rutina `ReCaptcha`
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 2
> - WebMatrix 3
> - Knihovna webových pomocníků ASP.NET

Můžete nastavit svůj web tak, aby se k němu &#8212; uživatelé mohli přihlásit, aby lokalita podporovala *členství*. To může být užitečné z mnoha důvodů. Například váš web může mít stránky, které by měly být k dispozici pouze pro členy. V některých případech můžete vyžadovat, aby se uživatelé přihlásili, aby vám poslali zpětnou vazbu nebo nechali komentář.

I když váš web podporuje členství, uživatelé nemusí nutně vyžadovat, abyste se přihlásili předtím, než použijí některé stránky na webu. Uživatelé, kteří nejsou přihlášení, se nazývají *anonymní uživatelé*.

Uživatel se může zaregistrovat na vašem webu a pak se může přihlásit k webu. Web vyžaduje uživatelské jméno (e-mailovou adresu) a heslo pro potvrzení, že uživatelé mají nárok. Tento proces přihlášení a potvrzení identity uživatele se označuje jako *ověřování*.

Zabezpečení a členství můžete nastavit různými způsoby:

- Pokud používáte WebMatrix, snadný způsob, jak vytvořit novou lokalitu na základě šablony **webu Starter** . Tato šablona je již nakonfigurována pro zabezpečení a členství a má již registrační stránku, přihlašovací stránku a tak dále.

    Lokalita vytvořená šablonou má taky možnost Povolit uživatelům přihlášení pomocí externího webu, jako je Facebook, Google nebo Twitter.
- Pokud chcete přidat zabezpečení do existující lokality nebo pokud nechcete používat šablonu **webu Starter** , můžete vytvořit vlastní registrační stránku, přihlašovací stránku a tak dále.

Tento článek se zaměřuje na první možnost &mdash;, jak přidat zabezpečení pomocí šablony **webu Starter** . Obsahuje taky některé základní informace o tom, jak implementovat vlastní zabezpečení a pak poskytuje odkazy na Další informace o tom, jak to udělat. K dispozici jsou také informace o tom, jak povolit externí přihlášení, která jsou podrobněji popsána v samostatném článku.

## <a name="creating-website-security-using-the-starter-site-template"></a>Vytvoření zabezpečení webu pomocí šablony webu Starter

Ve WebMatrixu můžete pomocí šablony **webu Starter** vytvořit web, který obsahuje následující:

- Databáze, která slouží k ukládání uživatelských jmen a hesel pro členy.
- Registrační stránka, kde se mohou registrovat anonymní (noví) uživatelé.
- Stránka pro přihlášení a odhlášení
- Stránka obnovení a obnovení hesla

Následující postup popisuje, jak vytvořit lokalitu a nakonfigurovat ji.

1. Spusťte WebMatrix a na stránce **rychlé zprovoznění** vyberte možnost **lokalita ze šablony**.
2. Vyberte šablonu **spouštěcího webu** a klikněte na tlačítko **OK**. WebMatrix vytvoří nový web.
3. V levém podokně klikněte na selektor pracovního prostoru **soubory** .
4. V kořenové složce vašeho webu otevřete soubor *\_AppStart. cshtml* , což je speciální soubor, který se používá k tomu, aby obsahoval globální nastavení. Obsahuje některé příkazy, které jsou zakomentovány pomocí `//`ch znaků:

    [!code-csharp[Main](16-adding-security-and-membership/samples/sample1.cs)]

    Tyto příkazy konfigurují pomocný parametr `WebMail`, který se dá použít k odeslání e-mailu. Systém členství může pomocí e-mailu odesílat potvrzovací zprávy, když se uživatelé registrují nebo kdy chtějí měnit hesla. (Například po registraci uživatele obdrží e-mail s odkazem, na který mohou kliknout, aby mohl proces registrace dokončit.)

    Odesílání e-mailů vyžaduje přístup k serveru SMTP, jak je popsáno v tématu [Přidání e-mailu na web webových stránek ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202899). Nastavení e-mailu uložíte v tomto souboru centrální *\_AppStart. cshtml* , abyste je nemuseli zadávat opakovaně na každou stránku, která může odesílat e-maily. (Nemusíte konfigurovat nastavení SMTP pro nastavení registrační databáze. Pokud chcete ověřovat uživatele z e-mailového aliasu a nechat si uživatele resetovat zapomenuté heslo, budete potřebovat jenom nastavení SMTP.)
5. Odkomentujte příkazy odebráním `//` před každou z nich.

    Pokud nechcete nastavit e-mailové potvrzení, můžete tento krok přeskočit a další krok. Pokud nejsou nastavené hodnoty SMTP, je nový účet hned dostupný bez potvrzovacího e-mailu.
6. Upravte následující nastavení související s e-maily v kódu:

   - Nastavte `WebMail.SmtpServer` na název serveru SMTP, ke kterému máte přístup.
   - Ponechte `WebMail.EnableSsl` nastavenou na `true`. Toto nastavení zabezpečuje přihlašovací údaje, které se odesílají na server SMTP, pomocí jejich šifrování.
   - Nastavte `WebMail.UserName` na uživatelské jméno pro svůj účet serveru SMTP.
   - Nastavte `WebMail.Password` na heslo pro svůj účet serveru SMTP.
   - Nastavte `WebMail.From` na vlastní e-mailovou adresu. Toto je e-mailová adresa, ze které se zpráva odesílá.

     > [!NOTE] 
     > 
     > **Tip** Další informace o hodnotách těchto vlastností najdete v tématu [Konfigurace nastavení e-mailu](https://go.microsoft.com/fwlink/?LinkID=202906#configuring_email_settings) v tématu [přizpůsobení chování pro webové stránky ASP.NET napříč lokalitami](https://go.microsoft.com/fwlink/?LinkID=202906).
7. Uložte a zavřete *\_AppStart. cshtml*.
8. Spusťte stránku *Default. cshtml* v prohlížeči.

    ![zabezpečení-členství – 2](16-adding-security-and-membership/_static/image1.png)

   > [!NOTE]
   > Pokud se zobrazí chyba s oznámením, že vlastnost musí být instancí `ExtendedMembershipProvider`, lokalita nemusí být nakonfigurovaná tak, aby používala systém členství na webových stránkách ASP.NET (SimpleMembership). Tato situace může někdy nastat, pokud je server poskytovatele hostingu nakonfigurován jinak než místní server. Chcete-li tento problém vyřešit, přidejte následující prvek do souboru *Web. config* webu:
   > 
   > [!code-xml[Main](16-adding-security-and-membership/samples/sample2.xml)]
   > 
   > Přidejte tento prvek jako podřízený prvek `<configuration>` a jako partnerský uzel `<system.web>` elementu.
9. V pravém horním rohu stránky klikněte na odkaz **zaregistrovat** . Zobrazí se stránka *Register. cshtml* .
10. Zadejte uživatelské jméno a heslo a potom klikněte na **zaregistrovat**.

    ![zabezpečení-členství – 3](16-adding-security-and-membership/_static/image2.png)

    Když jste vytvořili web ze šablony **úvodní web** , vytvořila se databáze s názvem *úvodníweb. sdf* ve složce *data App\_e* webu. Během registrace se do databáze přidají informace o uživateli. Pokud nastavíte hodnoty SMTP, zpráva se pošle na e-mailovou adresu, kterou jste použili, abyste mohli dokončit registraci.

    ![zabezpečení-členství – 4](16-adding-security-and-membership/_static/image3.png)
11. Přečtěte si e-mailový program a vyhledejte zprávu, která bude mít váš potvrzovací kód a hypertextový odkaz na web.
12. Kliknutím na hypertextový odkaz aktivujete svůj účet. Potvrzovací hypertextový odkaz otevře stránku potvrzení registrace.

    ![zabezpečení-členství – 5](16-adding-security-and-membership/_static/image4.png)
13. Klikněte na odkaz pro **přihlášení** a pak se přihlaste pomocí účtu, který jste zaregistrovali.

      Po přihlášení se odkazy na **přihlášení** a **registraci** nahrazují odkazem na **odhlášení** . Vaše přihlašovací jméno se zobrazí jako odkaz. (Odkaz vám umožní přejít na stránku, kde můžete změnit heslo.)

      ![zabezpečení-členství – 6](16-adding-security-and-membership/_static/image5.png)

      > [!NOTE]
      > Ve výchozím nastavení odesílají webové stránky ASP.NET přihlašovací údaje na server v podobě prostého textu (jako text čitelný lidmi). Provozní web by měl používat zabezpečený protokol HTTP (https://, označovaný také jako *Secure Sockets* Layer nebo SSL) k šifrování citlivých informací, které se vyměňují se serverem. Můžete požadovat odeslání e-mailových zpráv pomocí protokolu SSL nastavením `WebMail.EnableSsl=true` jako v předchozím příkladu. Další informace o protokolu SSL najdete v tématu [zabezpečení webové komunikace: certifikáty, SSL a https://](https://go.microsoft.com/fwlink/?LinkId=208660).

## <a name="additional-membership-functionality-in-the-site"></a>Další funkce členství v lokalitě

Vaše lokalita obsahuje další funkce, které uživatelům umožňují spravovat své účty. Uživatelé můžou provádět tyto akce:

- Změnit jejich hesla. Po přihlášení můžou kliknout na uživatelské jméno (což je odkaz). Tím přejdete na stránku, kde mohou vytvořit nové heslo (*účet/ChangePassword. cshtml*).
- Obnovení zapomenutého hesla. Na přihlašovací stránce se nachází odkaz (**Zapomněli jste heslo?** ), které uživatele přebírají na stránku (*účet/forgotPassword. cshtml*), kde můžou zadat e-mailovou adresu. Lokalita jim pošle e-mailovou zprávu s odkazem, na který můžou kliknout, aby si nastavili nové heslo (*account/PasswordReset. cshtml*).

Můžete také umožnit uživatelům přihlášení pomocí externí lokality, jak je vysvětleno později.

<a id="Creating_a_Members-Only_Page"></a>
## <a name="creating-a-members-only-page"></a>Vytvoření stránky jenom pro členy

V době, kdy může kdokoli přejít na libovolnou stránku na webu. Ale možná budete chtít mít stránky, které jsou k dispozici pouze uživatelům, kteří se přihlásili (tj. členům). ASP.NET umožňuje vytvářet stránky, ke kterým mohou být přihlášeni pouze přihlášení členové. Pokud se anonymní uživatelé pokusí získat přístup na stránku jenom pro členy, přesměrují je na přihlašovací stránku.

V tomto postupu vytvoříte složku, která bude obsahovat stránky, které jsou k dispozici pouze pro přihlášené uživatele.

1. V kořenovém adresáři lokality vytvořte novou složku. (Na pásu karet klikněte na šipku pod položkou **nové** a pak zvolte **Nová složka**.)
2. Pojmenujte nové *členy*složky.
3. Uvnitř složky *Členové* vytvořte novou stránku a pojmenujte ji *MembersInformation. cshtml*.
4. Existující obsah nahraďte následujícím kódem a označením:

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample3.cshtml)]

    Tento kód testuje vlastnost `IsAuthenticated` objektu `WebSecurity`, která vrátí `true`, pokud se uživatel přihlásil. Pokud uživatel není přihlášen, kód volá `Response.Redirect` k odeslání uživatele do stránky *Login. cshtml* ve složce *account* .

    Adresa URL přesměrování zahrnuje `returnUrl` hodnotu řetězce dotazu, která používá `Request.Url.LocalPath` k nastavení cesty aktuální stránky. Pokud nastavíte `returnUrl` hodnotu v řetězci dotazu (a pokud je návratová adresa URL místní cesta), přihlašovací stránka po přihlášení vrátí uživatele na tuto stránku.

    Kód také nastaví *\_stránku SiteLayout. cshtml* jako stránku rozložení. (Další informace o stránkách rozložení najdete v tématu [vytvoření konzistentního rozložení v ASP.NET webech webových stránek](https://go.microsoft.com/fwlink/?LinkId=202891).)
5. Spusťte Web. Pokud jste ještě přihlášení, klikněte na tlačítko **Odhlásit** v horní části stránky.
6. V prohlížeči požádejte o stránku */members/MembersInformation*. Adresa URL může vypadat například takto:

    `http://localhost:38366/Members/MembersInformation`

    (Číslo portu (38366) se pravděpodobně v adrese URL liší.)

    Budete přesměrováni na stránku *Login. cshtml* , protože nejste přihlášeni.
7. Přihlaste se pomocí účtu, který jste vytvořili dříve. Budete přesměrováni zpět na stránku *MembersInformation* . Vzhledem k tomu, že jste přihlášení, zobrazí se vám tentokrát obsah stránky.

K zabezpečení přístupu k několika stránkám můžete použít tento postup:

- Přidejte kontrolu zabezpečení na každou stránku.
- Vytvořte stránku *\_PageStart. cshtml* ve složce, kam zachováte chráněné stránky, a přidejte kontrolu zabezpečení. Stránka *\_PageStart. cshtml* funguje jako typ globální stránky pro všechny stránky ve složce. Tato technika je podrobněji vysvětlena v tématu [přizpůsobení chování pro webové stránky ASP.NET v nejrůznějších lokalitách](https://go.microsoft.com/fwlink/?LinkId=202906#Using__PageStart.cshtml_to_Restrict_Folder_Access).

## <a name="creating-security-for-groups-of-users-roles"></a>Vytváření zabezpečení pro skupiny uživatelů (role)

Pokud má vaše lokalita mnoho členů, není efektivní zkontrolovat oprávnění pro každého uživatele předtím, než se jim zobrazí stránka. Místo toho můžete vytvořit skupiny nebo *role*, do kterých patří jednotliví členové. Pak můžete zaškrtnout oprávnění na základě role. V této části vytvoříte roli správce &quot;&quot; a pak vytvoříte stránku, která je přístupná pro uživatele, kteří patří do této role (kteří patří do).

Systém členství v ASP.NET je nastavený tak, aby podporoval role. Na rozdíl od registrace členství a přihlášení ale šablona **úvodní lokality** neobsahuje stránky, které vám pomůžou se správou rolí. (Správa rolí je administrativní úloha, nikoli úkol uživatele.) Skupiny však můžete přidat přímo do databáze členství ve WebMatrixu.

1. V části WebMatrix klikněte na selektor pracovního prostoru **databáze** .
2. V levém podokně otevřete uzel *úvodníweb. sdf* , otevřete uzel **Tables (tabulky** ) a dvakrát klikněte na tabulku *webpages\_role* .

    ![zabezpečení-členství – 7](16-adding-security-and-membership/_static/image6.png)
3. Přidejte roli s názvem &quot;&quot;správce. Pole *RoleId* se vyplní automaticky. (Jedná se o primární klíč a byl nastaven jako pole pro identifikaci, jak je vysvětleno v [úvodu k práci s databází na webech webových stránek ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202893).)
4. Poznamenejte si, jaká je hodnota pro pole *RoleId* . (Pokud se jedná o první roli, kterou definujete, bude se jednat o 1.)

    ![zabezpečení-členství-8](16-adding-security-and-membership/_static/image7.png)
5. Zavřete tabulku *rolí\_webové stránky* .
6. Otevřete tabulku *USERPROFILE* .
7. Poznamenejte si hodnotu *ID* uživatele jednoho nebo více uživatelů v tabulce a pak tabulku zavřete.
8. Otevřete tabulku *webpages\_UserInRoles* a do tabulky zadejte *UserID* a *RoleID* hodnotu. Pokud například chcete uživatele přidat do role &quot;správce&quot;, zadejte tyto hodnoty:

    ![zabezpečení – členství – 9](16-adding-security-and-membership/_static/image8.png)
9. Zavřete *webové stránky\_tabulce UsersInRoles* .

    Teď, když máte definované role, můžete nakonfigurovat stránku, která je přístupná pro uživatele, kteří jsou v této roli.
10. V kořenové složce webu vytvořte novou stránku s názvem *AdminError. cshtml* a stávající obsah nahraďte následujícím kódem. To bude stránka, na kterou budou uživatelé přesměrováni, pokud nemají povolený přístup na stránku.

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample4.cshtml)]
11. V kořenové složce webu vytvořte novou stránku s názvem *AdminOnly. cshtml* a nahraďte existující kód následujícím kódem:

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample5.cshtml)]

    Metoda `Roles.IsUserInRole` vrátí `true`, pokud je aktuální uživatel členem zadané role (v tomto případě role "správce").
12. Spusťte *Default. cshtml* v prohlížeči, ale Přihlaste se. (Pokud jste už přihlášení, odhlaste se.)
13. V adresním řádku prohlížeče přidejte *AdminOnly* do adresy URL. (Jinými slovy, požádejte o soubor *AdminOnly. cshtml* .) Budete přesměrováni na stránku *AdminError. cshtml* , protože v tuto chvíli nejste přihlášeni jako uživatel v roli&quot; správce &quot;.
14. Vraťte se do *Default. cshtml* a přihlaste se jako uživatel, kterého jste přidali do role&quot; správce &quot;.
15. Přejděte na stránku *AdminOnly. cshtml* . Tentokrát se zobrazí stránka.

## <a name="preventing-automated-programs-from-joining-your-website"></a>Zabránění automatizovaným programům v připojení k webu

Přihlašovací stránka neukončí automatizované programy (někdy označované jako *Web robots* nebo *roboty*) z registrace k vašemu webu. Tento postup popisuje, jak povolit ReCaptcha test na registrační stránce.

![/media/38777/ch16securitymembership-18.jpg](16-adding-security-and-membership/_static/image1.jpg)

1. Zaregistrujte si web na adrese ReCaptcha.Net ([http://recaptcha.net](http://recaptcha.net)). Po dokončení registrace získáte veřejný klíč a soukromý klíč.
2. Přidejte knihovnu webových pomocníků ASP.NET na web, jak je popsáno v [tématu Instalace pomocníků na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste to ještě neudělali.
3. Ve složce *account (účet* ) otevřete soubor s názvem *Register. cshtml*.
4. V kódu v horní části stránky Najděte následující řádky a odkomentujte je odebráním znaků `//` komentáře:

    [!code-csharp[Main](16-adding-security-and-membership/samples/sample6.cs)]
5. Nahraďte `PRIVATE_KEY` vlastním privátním klíčem ReCaptcha.
6. V značky stránky odeberte `@*` a `*@` znaky komentářů od následujících řádků v kódu stránky:

    [!code-cshtml[Main](16-adding-security-and-membership/samples/sample7.cshtml)]
7. Nahraďte `PUBLIC_KEY` klíčem.
8. Pokud jste ho ještě neodebrali, odeberte `<div>` element obsahující text, který začíná na "Pokud chcete povolit ověřování CAPTCHA...". (Odebrat celý prvek `<div>` a jeho obsah.)

9. V prohlížeči spusťte *Default. cshtml* . Pokud jste se k webu přihlásili, klikněte na odkaz **Odhlásit** se.
10. Klikněte na odkaz **zaregistrovat** a otestujte registraci pomocí testu captcha.

     ![zabezpečení-členství – 10](16-adding-security-and-membership/_static/image9.png)

Další informace o nástroji `ReCaptcha` Helper najdete v tématu [použití CATPCHA k tomu, aby se zabránilo automatickým programům (roboty) v používání webu ASP.NET](https://go.microsoft.com/fwlink/?LinkId=251967).

<a id="Additional_Resources"></a>
## <a name="letting-users-log-in-using-an-external-site"></a>Umožnění uživatelům přihlásit se pomocí externího webu

Šablona **úvodní lokality** obsahuje kód a značky, které umožní uživatelům přihlásit se pomocí Facebooku, Windows Live, Twitter, Google nebo Yahoo. Tato funkce není ve výchozím nastavení povolená. Obecný postup, jak použít přihlášení uživatelů pomocí těchto externích zprostředkovatelů:

- Rozhodněte, které externí weby chcete podporovat.
- V případě potřeby přejít na tuto lokalitu a nastavit přihlašovací aplikaci. (Můžete to třeba udělat, pokud chcete povolit přihlášení na Facebooku.)
- V lokalitě nakonfigurujte poskytovatele. Ve většině případů stačí pouze zrušit komentář k některému kódu v souboru *\_AppStart. cshtml* .
- Přidejte značky na registrační stránku, která uživatelům umožňuje odkaz na externí web pro přihlášení. Obvykle můžete zkopírovat kód, který potřebujete, a mírně změnit text.

Podrobné pokyny najdete v tématu [Povolení přihlášení z externích webů na webu webové stránky ASP.NET](https://go.microsoft.com/fwlink/?LinkId=251969).

Jakmile se uživatel přihlásí z jiné lokality, uživatel se vrátí k vaší lokalitě a *přidruží* k vašemu webu přihlašovací údaje. V důsledku toho vytvoří položka členství na webu pro externí přihlášení uživatele. To vám umožní používat k externímu přihlášení normální zařízení členství (například role).

## <a name="adding-security-to-an-existing-website"></a>Přidání zabezpečení na existující web

Postup výše v tomto článku se spoléhá na použití šablony **webu Starter** jako základu pro zabezpečení webu. Pokud není vhodné začít od šablony **webu Starter** nebo zkopírovat relevantní stránky z webu na základě této šablony, můžete implementovat stejný typ zabezpečení na vlastní web, a to tak, že ho zakódujete sami. Vytvoříte stejné typy stránek – registrace, přihlašování a tak dále, a pak použijete pomocníky a třídy k nastavení členství.

Základní postup je popsaný v blogovém příspěvku [nejzákladnější způsob implementace zabezpečení ASP.NET Razor](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2240). Většina práce se provádí pomocí následujících metod a vlastností pomocné rutiny `WebSecurity`:

- [WebSecurty. UserExists](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.userexists(v=vs.99).aspx), [WebSecurity. CreateUserAndAccount](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.createuserandaccount(v=vs.99).aspx). Tyto metody umožňují určit, jestli je někdo už zaregistrovaný, a zaregistrovat ho.
- [WebSecurty. Neověřeno](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.isauthenticated(v=vs.99).aspx). Tato vlastnost umožňuje určit, zda je aktuální uživatel přihlášen. To je užitečné pro přesměrování uživatelů na přihlašovací stránku, pokud ještě nejsou přihlášeni.
- [WebSecurity. Login](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.login(v=vs.99).aspx), [WebSecurity. logout](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.logout(v=vs.99).aspx). Tyto metody zaprotokolují uživatele do nebo ven.
- [WebSecurity. CurrentUserName](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity.currentusername(v=vs.99).aspx). Tato vlastnost je užitečná pro zobrazení přihlašovacího jména aktuálního uživatele (Pokud je uživatel přihlášený).
- [WebSecurity. ConfirmAccount](https://msdn.microsoft.com/library/gg569286(v=vs.99).aspx). Tato metoda je užitečná, pokud nastavíte e-mailové potvrzení k registraci. (Podrobnosti najdete v blogovém příspěvku [pomocí funkce potvrzení pro zabezpečení webových stránek ASP.NET](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2267).)

Chcete-li spravovat role, můžete použít [role](https://msdn.microsoft.com/library/gg538398(v=vs.99).aspx) a třídy [členství](https://msdn.microsoft.com/library/gg569035(v=vs.99).aspx) , jak je popsáno v položce blogu.

## <a name="additional-resources"></a>Další prostředky

- [Přizpůsobení chování v celém webu](https://go.microsoft.com/fwlink/?LinkId=202906)
- [Zabezpečení webové komunikace: certifikáty, SSL a https://](https://go.microsoft.com/fwlink/?LinkId=208660)
- Nejzákladnější [způsob implementace zabezpečení ASP.NET Razor](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2240) a [používání funkce potvrzení pro zabezpečení webových stránek ASP.NET](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2267). Jedná se o blogové příspěvky, které popisují implementaci funkcí ASP.NET členství bez použití šablony **webu Starter** .
- [Povolení přihlášení z externích webů na webu s webovými stránkami ASP.NET](https://go.microsoft.com/fwlink/?LinkId=251969)
- [Referenční dokumentace rozhraní API třídy WebSecurity](https://msdn.microsoft.com/library/webmatrix.webdata.websecurity(v=vs.99)) (MSDN)
- [Reference k rozhraní API třídy SimpleRoleProvider](https://msdn.microsoft.com/library/webmatrix.webdata.simpleroleprovider(v=vs.99)) (MSDN)
- [Reference k rozhraní API třídy SimpleMembershipProvider](https://msdn.microsoft.com/library/webmatrix.webdata.simplemembershipprovider(v=vs.99)) (MSDN)

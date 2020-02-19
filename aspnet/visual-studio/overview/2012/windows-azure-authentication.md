---
uid: visual-studio/overview/2012/windows-azure-authentication
title: Ověřování systému Windows Azure | Microsoft Docs
author: Rick-Anderson
description: Microsoft ASP.NET Tools for Windows Azure Active Directory usnadňuje ověřování webových aplikací hostovaných na webech Windows Azure...
ms.author: riande
ms.date: 02/20/2013
ms.assetid: a3cef801-a54b-4ebd-93c3-55764e2e14b1
msc.legacyurl: /visual-studio/overview/2012/windows-azure-authentication
msc.type: authoredcontent
ms.openlocfilehash: ce98effe18dd739504fb0d5453bae8a46c3ba102
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457476"
---
# <a name="windows-azure-authentication"></a>Ověřování Windows Azure

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> Microsoft ASP.NET Tools for Windows Azure Active Directory usnadňuje ověřování webových aplikací hostovaných na [webech Windows Azure](https://www.windowsazure.com/home/features/web-sites/). Ověřování Windows Azure můžete použít k ověření uživatelů Office 365 z vaší organizace a firemních účtů synchronizovaných z místní služby Active Directory nebo uživatelů vytvořených ve vlastní doméně Windows Azure Active Directory. Povolení ověřování Windows Azure nakonfiguruje vaši aplikaci tak, aby ověřovala uživatele s použitím jednoho tenanta [Windows Azure Active Directory](https://docs.microsoft.com/azure/active-directory/) .
>
> Nástroj ASP.NET Windows Azure pro ověřování není pro webové role v cloudové službě podporovaný, ale plánujeme to udělat v budoucí verzi. [Windows Identity Foundation](https://msdn.microsoft.com/library/hh291066(v=VS.110).aspx) (WIF) se podporuje v rolích webu Windows Azure.
>
> Podrobnosti o tom, jak nastavit synchronizaci mezi vaší místní službou Active Directory a vaším klientem Windows Azure Active Directory, najdete v článku [použití AD FS 2,0 k implementaci a správě jednotného přihlašování](https://technet.microsoft.com/library/jj205462.aspx).
>
> Windows Azure Active Directory je aktuálně k dispozici jako [bezplatná služba ve verzi Preview](https://azure.microsoft.com/free/?WT.mc_id=A443DD604).

## <a name="requirements"></a>Požadavky:

- Visual Studio 2012 nebo [Visual Studio Express 2012](https://www.microsoft.com/visualstudio/11/products/express)
- [Rozšíření webových nástrojů pro Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282228&amp;clcid=0x409) nebo [rozšíření webových nástrojů pro Visual Studio Express 2012](https://go.microsoft.com/fwlink/?LinkID=282231&amp;clcid=0x409)
- [Microsoft ASP.NET Tools for windows Azure Active Directory – Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkID=282306) nebo [Microsoft ASP.NET tools for windows Azure Active Directory – Visual Studio Express 2012 for Web](https://go.microsoft.com/fwlink/?LinkId=282652)

## <a name="create-an-aspnet-web-application-with-visual-studio-2012"></a>Vytvoření webové aplikace v ASP.NET pomocí sady Visual Studio 2012

V rámci sady Visual Studio 2012 můžete vytvořit libovolnou webovou aplikaci, v tomto kurzu se používá šablona intranetu ASP.NET MVC.

1. Vytvořte novou intranetovou aplikaci ASP.NET MVC 4 a přijměte všechny výchozí hodnoty. (Musí se jednat o v **tra** NET, nikoli v projektu pro rozkládání na síť **ter** ).
     ![](windows-azure-authentication/_static/image1.png)

## <a name="enable-window-azure-authentication-when-you-are-a-global-administrator-of-the-tenet"></a>Povolit ověřování Azure v systému Windows (Pokud jste globální správce principem)

Pokud nemáte existujícího tenanta Windows Azure Active Directory (například prostřednictvím existujícího účtu Office 365), můžete vytvořit nového tenanta tak, že si zaregistrujete [nový účet Windows Azure Active Directory](https://g.microsoftonline.com/0AX00en/5).

1. V nabídce projekt vyberte **Povolit ověřování Windows Azure**:

   ![](windows-azure-authentication/_static/image2.png)

2. Zadejte doménu pro vašeho tenanta Windows Azure Active Directory (například contoso.onmicrosoft.com) a klikněte na **Povolit**:

![](windows-azure-authentication/_static/image3.png)

3. V dialogovém okně Webové ověřování se přihlaste jako správce pro klienta Azure Active Directory Windows:

   ![](windows-azure-authentication/_static/image4.png)

![](windows-azure-authentication/_static/image5.png)

## <a name="enable-window-azure-by-a-non-administrator-of-the-tenet"></a>Povolit Azure Window principem bez správce

Pokud nemáte oprávnění globálního správce pro klienta Azure Active Directory Windows, můžete zrušit zaškrtnutí políčka pro zřízení aplikace.

![](windows-azure-authentication/_static/image6.png)

V dialogovém okně se zobrazí **doména**, **ID objektu zabezpečení aplikace** a **Adresa URL odpovědi** , které jsou požadovány pro zřízení aplikace s Azure Active Directory principem. Tyto informace je nutné poskytnout někomu, kdo má dostatečná oprávnění ke zřízení aplikace. Podrobnosti o tom, jak použít rutinu k vytvoření instančního objektu, najdete v tématu[implementace jednotného přihlašování pomocí aplikace Windows Azure Active Directory-ASP.NET](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect) .
Po úspěšném zřízení aplikace můžete kliknutím na **pokračovat aktualizovat web. config pomocí vybraného nastavení**. Pokud chcete pokračovat v vývoji aplikace při čekání na zřízení, můžete kliknout na tlačítko **Zavřít a zapamatovat si nastavení v souboru projektu**. Až příště vyvoláte možnost povolit ověřování systému Windows Azure a zrušit zaškrtnutí políčka zřizování, zobrazí se stejná nastavení a můžete kliknout na **pokračovat**a pak na, **použít tato nastavení v souboru Web. config**.

1. Počkejte, než bude vaše aplikace nakonfigurovaná pro ověřování Windows Azure a zřízená pomocí Windows Azure Active Directory.
2. Po povolení ověřování Windows Azure pro vaši aplikaci klikněte na **Zavřít:**

    ![](windows-azure-authentication/_static/image7.png)
3. Stiskněte klávesu F5 ke spuštění aplikace. Automaticky se přesměruje na přihlašovací stránku. K přihlášení do aplikace použijte přihlašovací údaje uživatele adresáře principem.

    ![](windows-azure-authentication/_static/image1.jpg)
4. Vzhledem k tomu, že vaše aplikace aktuálně používá testovací certifikát podepsaný svým držitelem, obdržíte upozornění z prohlížeče, že certifikát nebyl vydán důvěryhodnou certifikační autoritou.

    Toto upozornění se dá bezpečně ignorovat při místním vývoji kliknutím na **pokračovat na tento web:**

    ![](windows-azure-authentication/_static/image8.png)
5. K aplikaci jste se teď úspěšně přihlásili pomocí ověřování Windows Azure.

    ![](windows-azure-authentication/_static/image2.jpg)

Povolení ověřování systému Windows Azure provede následující změny vaší aplikace:

- Do projektu se přidá třída[CSRF](https://www.owasp.org/index.php/Cross-Site_Request_Forgery_(CSRF))(anti-siteing Request) ( *App\_Start\AntiXsrfConfig.cs* ).
- Do projektu se přidají `System.IdentityModel.Tokens.ValidatingIssuerNameRegistry` balíčky NuGet.
- Nastavení Windows Identity Foundation v aplikaci se nakonfigurují tak, aby přijímala tokeny zabezpečení z tenanta Windows Azure Active Directory. Kliknutím na následující obrázek zobrazíte rozšířené zobrazení změn provedených v souboru *Web. config* .

     ![](windows-azure-authentication/_static/image9.png)
- V tenantovi Windows Azure Active Directory se zřídí instanční objekt pro vaši aplikaci.
- Protokol HTTPS je povolený.

## <a name="deploy-the-application-to-windows-azure"></a>Nasazení aplikace do platformy Windows Azure

Podrobné pokyny najdete v tématu [nasazení webové aplikace v ASP.NET do webu Windows Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).

Publikování aplikace pomocí ověřování Windows Azure na webu Azure:

1. Klikněte pravým tlačítkem na aplikaci a vyberte **publikovat:**

    ![](windows-azure-authentication/_static/image3.jpg)
2. V dialogovém okně Publikovat web Stáhněte a importujte profil publikování webu Azure.

    ![](windows-azure-authentication/_static/image4.jpg)
3. Karta **připojení** zobrazuje **cílovou adresu URL** (veřejnou adresu URL vaší aplikace). Otestujte připojení kliknutím na **ověřit připojení** :

    ![](windows-azure-authentication/_static/image5.jpg)
4. Pokud jste už publikovali na tento web Azure, zvažte nastavení možnosti **odebrat další soubory v cílovém umístění** , abyste zajistili, že se aplikace publikuje čistě. Všimněte si, že je zaškrtnuté políčko **Povolit ověřování systému Windows Azure** .

    ![](windows-azure-authentication/_static/image10.png)
5. Volitelné: na kartě **Náhled** klikněte na **Start Preview** , abyste viděli soubory nasazené.

    ![](windows-azure-authentication/_static/image6.jpg)
6. Klikněte na **publikovat.**

    Zobrazí se výzva k povolení ověřování Windows Azure pro cílového hostitele. Pokračujte kliknutím na **Povolit** :

    ![](windows-azure-authentication/_static/image11.png)
7. Zadejte přihlašovací údaje správce pro Azure Active Directory tenanta pro Windows:

    ![](windows-azure-authentication/_static/image7.jpg)
8. Po úspěšném publikování aplikace se otevře prohlížeč publikovaného webu.

    > [!NOTE]
    > Po povolení ověřování Windows Azure pro cílového hostitele může trvat až pět minut (obvykle se musí snížit), aby se vaše aplikace plně zřídila s Windows Azure Active Directory. Při prvním spuštění aplikace, pokud se zobrazí chyba ACS50001: předávající strana s názvem [Realm] nebyla nalezena, počkejte několik minut a zkuste aplikaci znovu spustit.
9. Po zobrazení výzvy se přihlaste jako uživatel ve vašem adresáři:

    ![](windows-azure-authentication/_static/image8.jpg)
10. Úspěšně jste se k hostované aplikaci Azure přihlásili pomocí ověřování Windows Azure.

     ![](windows-azure-authentication/_static/image9.jpg)

## <a name="known-issues"></a>Známé problémy

#### <a name="role-based-authorization-fails-when-using-windows-azure-authentication"></a>Autorizace na základě rolí se při použití ověřování systému Windows Azure nezdařila.

Ověřování systému Windows Azure aktuálně neposkytuje potřebnou deklaraci identity, aby bylo možné provést autorizaci založenou na rolích. Roli ověřeného uživatele je třeba ručně načíst z Windows Azure Active Directory.

#### <a name="browsing-to-an-application-with-windows-azure-authentication-results-in-the-error-acs20016-the-domain-of-the-logged-in-user-livecom-does-not-match-any-allowed-domain-of-this-sts"></a>Když přejdete na aplikaci s ověřováním Windows Azure, dojde k chybě "ACS20016 se doména přihlášeného uživatele (live.com) neshoduje s žádnou povolenou doménou této služby STS".

Pokud jste už přihlášení k účtu Microsoft (například hotmail.com, live.com, outlook.com) a pokusíte se o přístup k aplikaci s povoleným ověřováním Windows Azure, může se vám zobrazit chybová odpověď 400, protože doména vašeho účtu Microsoft. není rozpoznáno Azure Active Directory Windows. Pokud se chcete přihlásit k aplikaci, odhlaste se nejdřív od svého účtu Microsoft.

#### <a name="logging-into-an-application-with-windows-azure-authentication-enabled-and-a-x509certificatevalidationmode-other-than-none-results-in-certificate-validation-errors-for-the-accountsaccesscontrolwindowsnet-certificate"></a>Přihlášení k aplikaci s povoleným ověřováním Windows Azure a X509CertificateValidationMode jiným než None má za následek chyby ověření certifikátu pro certifikát accounts.accesscontrol.windows.net.

Ověření certifikátu není povinné a mělo by být ponecháno zakázáno. Kryptografický otisk certifikátu vystavitele je ověřen pomocí modulu WSFederationAuthenticationModule.

#### <a name="when-attempting-to-enable-windows-azure-authentication-the-web-authentication-dialog-shows-the-error-acs20016-the-domain-of-the-logged-in-user-contosoonmicrosoftcom-does-not-match-any-allowed-domain-of-this-sts"></a>Při pokusu o povolení ověřování Windows Azure se v dialogovém okně Webové ověřování zobrazí chyba "ACS20016: doména přihlášeného uživatele (contoso.onmicrosoft.com) neodpovídá žádné povolené doméně této služby STS."

Tato chyba se může zobrazit v případě, že jste se dříve úspěšně přihlásili pomocí jiného účtu Windows Azure Active Directory v rámci stejného procesu sady Visual Studio. Odhlaste se ze zadaného účtu nebo restartujte aplikaci Visual Studio. Pokud jste už dříve přihlášení a vybrali možnost zůstat přihlášeni, možná budete muset vymazat soubory cookie v prohlížeči.

## <a name="acs20012-the-request-is-not-a-valid-ws-federation-protocol-message"></a>ACS20012: požadavek není platná zpráva protokolu WS-Federation.

K tomu může dojít, pokud jste už přihlášení pomocí nějakého jiného ID Microsoftu k jedné ze služeb Azure. Použijte soukromé okno prohlížeče, jako je například InPrivate v IE nebo anonymním, nebo zrušte zaškrtnutí všech souborů cookie.

## <a name="additional-resources"></a>Další materiály a zdroje informací

- [Microsoft ASP.NET Tools for Windows Azure Active Directory – Visual Studio 2012](https://blogs.msdn.com/b/vbertocci/archive/2013/02/18/microsoft-asp-net-tools-for-windows-azure-active-directory-visual-studio-2012.aspx) – Vittorio Bertocci
- [Funkce Windows Azure: identita](https://docs.microsoft.com/azure/active-directory/)
- [TechNet: Windows Azure Active Directory](https://technet.microsoft.com/library/hh967619.aspx)
- [Windows Azure Active Directory: vývoj aplikací pro vaši organizaci](https://activedirectory.windowsazure.com/Develop/Single-Tenant.aspx)
- [Windows Azure Active Directory: vývoj aplikací pro více organizací](https://activedirectory.windowsazure.com/Develop/Multi-Tenant.aspx)
- [Implementace jednotného přihlašování s Windows Azure Active Directory](https://github.com/Azure-Samples/active-directory-dotnet-webapp-openidconnect)
- [Jednotné přihlašování s Windows Azure Active Directory: hluboká podrobně](https://blogs.msdn.com/b/vbertocci/archive/2012/07/05/single-sign-on-with-windows-azure-active-directory-a-deep-dive.aspx) – Vittorio Bertocci
- [Použití AD FS 2,0 k implementaci a správě jednotného přihlašování](https://technet.microsoft.com/library/jj205462.aspx)

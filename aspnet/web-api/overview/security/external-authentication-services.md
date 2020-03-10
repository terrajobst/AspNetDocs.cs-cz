---
uid: web-api/overview/security/external-authentication-services
title: Externí ověřovací služby s webovým rozhranímC#API ASP.NET () | Microsoft Docs
author: rmcmurray
description: Popisuje použití externích ověřovacích služeb ve webovém rozhraní API ASP.NET.
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 3bb8eb15-b518-44f5-a67d-a27e051aedc6
msc.legacyurl: /web-api/overview/security/external-authentication-services
msc.type: authoredcontent
ms.openlocfilehash: b2571552a3f8040ff42bfa0a9fa48981f71a1e4b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555473"
---
# <a name="external-authentication-services-with-aspnet-web-api-c"></a>Služby externích ověřování s webovým rozhranímC#API ASP.NET ()

Visual Studio 2017 a ASP.NET 4.7.2 rozšiřují možnosti zabezpečení pro [jednostránkové aplikace](../../../single-page-application/index.md) (Spa) a [webové rozhraní API](../../index.md) pro integraci s externími ověřovacími službami, mezi které patří několik OAuth/OpenID a služby sociální média ověřování: účty Microsoft, Twitter, Facebook a Google.  

### <a name="in-this-walkthrough"></a>V tomto návodu

- [Používání služeb externích ověřování](#USING)
- [Vytvoření ukázkové webové aplikace](#SAMPLE)
- [Povoluje se ověřování na Facebooku.](#FACEBOOK)
- [Povoluje se ověřování Google.](#GOOGLE)
- [Povolení ověřování společnosti Microsoft](#MICROSOFT)
- [Povolení ověřování na Twitteru](#TWITTER)
- [Další informace](#MOREINFO)

    - [Kombinování externích ověřovacích služeb](#COMBINE)
    - [Konfigurace IIS Express pro použití plně kvalifikovaného názvu domény](#FQDN)
    - [Jak získat nastavení aplikace pro ověřování Microsoftu](#OBTAIN)
    - [Volitelné: zakázat místní registraci](#DISABLE)

### <a name="prerequisites"></a>Předpoklady

Chcete-li postupovat podle příkladů v tomto návodu, musíte mít následující:

- Visual Studio 2017
- Vývojářský účet s identifikátorem aplikace a tajným klíčem pro jednu z následujících služeb ověřování na sociálních médiích:

  - Účty Microsoft ([https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070))
  - Twitter ([https://dev.twitter.com/](https://dev.twitter.com/))
  - Facebook ([https://developers.facebook.com/](https://developers.facebook.com/))
  - Google ([https://developers.google.com/](https://developers.google.com))

<a id="USING"></a>
## <a name="using-external-authentication-services"></a>Používání služeb externích ověřování

Díky četnosti externích ověřovacích služeb, které jsou aktuálně dostupné vývojářům webu, můžete zkrátit dobu vývoje při vytváření nových webových aplikací. Webové uživatele obvykle mají několik stávajících účtů pro oblíbené webové služby a weby sociálních médií, proto když webová aplikace implementuje ověřovací služby z externí webové služby nebo webu sociálních médií, uloží dobu vývoje, která bylo stráveno vytvořením implementace ověřování. Použití externí služby ověřování ukládá koncovým uživatelům, aby si pro vaši webovou aplikaci vytvářel jiný účet, a také si musí zapamatovat jiné uživatelské jméno a heslo.

V minulosti měli vývojáři dvě možnosti: vytvořit vlastní implementaci ověřování nebo se naučíte integrovat externí službu ověřování do svých aplikací. Na nejvyšší úrovni představuje následující diagram jednoduchý tok požadavků pro uživatelského agenta (webový prohlížeč), který požaduje informace z webové aplikace, která je nakonfigurovaná na používání externí služby ověřování:

[![](external-authentication-services/_static/image2.png "Click to Expand the Image")](external-authentication-services/_static/image1.png)

V předchozím diagramu agent uživatele (nebo webový prohlížeč v tomto příkladu) vytvoří požadavek na webovou aplikaci, která přesměruje webový prohlížeč na externí službu ověřování. Uživatelský agent pošle své přihlašovací údaje do služby externího ověřování a pokud byl agent uživatele úspěšně ověřen, služba externí ověřování přesměruje uživatelského agenta do původní webové aplikace s určitou formou tokenu, kterou uživatelský agent se pošle webové aplikaci. Webová aplikace použije token k ověření, zda byl uživatelský agent úspěšně ověřen pomocí externí služby ověřování, a webová aplikace může token použít k získání dalších informací o uživatelském agentovi. Jakmile se aplikace dokončí zpracováním informací o uživatelském agentovi, Webová aplikace vrátí příslušnou odpověď agentovi uživatele na základě jeho autorizačního nastavení.

V tomto druhém příkladu Agent pro uživatele vychází z webové aplikace a externího autorizačního serveru a webová aplikace provádí další komunikaci s externím autorizačním serverem, aby načetla Další informace o uživateli. agenta

[![](external-authentication-services/_static/image4.png "Click to Expand the Image")](external-authentication-services/_static/image3.png)

Sady Visual Studio 2017 a ASP.NET 4.7.2 umožňují vývojářům zajistit integraci s externími službami ověřování pro vývojáře díky integrované integraci pro následující služby ověřování:

- Facebook
- Google
- Účty Microsoft (účty Windows Live ID)
- Twitter

Příklady v tomto návodu ukazují, jak nakonfigurovat každou z podporovaných externích ověřovacích služeb pomocí nové šablony webové aplikace ASP.NET, která se dodává se sadou Visual Studio 2017.

> [!NOTE]
> V případě potřeby možná budete muset přidat svůj plně kvalifikovaný název domény do nastavení pro službu externího ověřování. Tento požadavek vychází z omezení zabezpečení pro některé externí služby ověřování, které vyžadují, aby plně kvalifikovaný název domény v nastavení vaší aplikace odpovídal plně kvalifikovanému názvu domény, který používají vaši klienti. (Kroky pro tento postup se u každé externí služby ověřování značně liší. budete se muset obrátit na dokumentaci pro každou službu externího ověřování a zjistit, jestli je to potřeba, a jak tato nastavení nakonfigurovat.) Pokud potřebujete nakonfigurovat IIS Express pro použití plně kvalifikovaného názvu domény pro testování tohoto prostředí, přečtěte si část [konfigurace IIS Express použití plně kvalifikovaného názvu domény](#FQDN) v tomto návodu.

<a id="SAMPLE"></a>
## <a name="create-a-sample-web-application"></a>Vytvoření ukázkové webové aplikace

Následující kroky vás provedou vytvořením ukázkové aplikace pomocí šablony webové aplikace ASP.NET a tuto ukázkovou aplikaci použijete pro každou službu externího ověřování dále v tomto návodu.

Spusťte Visual Studio 2017 a na úvodní stránce vyberte **Nový projekt** . Nebo v nabídce **soubor** vyberte **Nový** a pak **projekt**.

<!-- [![](external-authentication-services/_static/image6.png "Click to Expand the Image")](external-authentication-services/_static/image5.png) -->

Po zobrazení dialogového okna **Nový projekt** vyberte možnost **nainstalováno** a rozbalte položku **vizuál C#** . V **části C#vizuál** vyberte **Web**. V seznamu šablon projektu vyberte **ASP.NET webová aplikace (.NET Framework)** . Zadejte název projektu a klikněte na tlačítko **OK**.

[![](external-authentication-services/_static/image71.png "Click to Expand the Image")](external-authentication-services/_static/image71.png)

Po zobrazení **nového projektu ASP.NET** vyberte šablonu **aplikace s jednou stránkou** a klikněte na **vytvořit projekt**.

[![](external-authentication-services/_static/image72.png "Click to Expand the Image")](external-authentication-services/_static/image72.png)

Počkejte, až Visual Studio 2017 vytvoří projekt.

<!-- [![](external-authentication-services/_static/image12.png "Click to Expand the Image")](external-authentication-services/_static/image11.png) -->

Po dokončení vytváření projektu v aplikaci Visual Studio 2017 otevřete soubor *Startup.auth.cs* , který je umístěn ve složce **App\_Start** .

Při prvním vytvoření projektu nejsou v souboru *Startup.auth.cs* povoleny žádné externí ověřovací služby. Následující příklad ilustruje, jak se váš kód může podobat, kde jsou zvýrazněné oddíly, kde byste povolili externí službu ověřování a veškerá relevantní nastavení, aby bylo možné používat účty Microsoft, Twitter, Facebook nebo Google ověřování s vaší aplikací ASP.NET:

[!code-csharp[Main](external-authentication-services/samples/sample1.cs)]

Když stisknete klávesu F5 k sestavení a ladění webové aplikace, zobrazí se přihlašovací obrazovka, na které se zobrazí, že nebyly definovány žádné externí ověřovací služby.

[![](external-authentication-services/_static/image73.png "Click to Expand the Image")](external-authentication-services/_static/image73.png)

V následujících částech se dozvíte, jak povolit každou z externích ověřovacích služeb, které jsou k dispozici v ASP.NET ve Visual Studiu 2017.

<a id="FACEBOOK"></a>
## <a name="enabling-facebook-authentication"></a>Povoluje se ověřování na Facebooku.

Použití ověřování na Facebooku vyžaduje, abyste vytvořili vývojářský účet pro Facebook a váš projekt bude vyžadovat ID aplikace a tajný klíč z Facebooku, aby fungoval. Informace o tom, jak vytvořit vývojářský účet pro Facebook a získat ID aplikace a tajný klíč, najdete v tématu [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).

Jakmile získáte ID aplikace a tajný klíč, použijte následující postup k povolení ověřování na Facebooku pro vaši webovou aplikaci:

1. Když je projekt otevřen v aplikaci Visual Studio 2017, otevřete soubor *Startup.auth.cs* .

2. Vyhledejte část s ověřovacím kódem Facebooku:

    [!code-csharp[Main](external-authentication-services/samples/sample2.cs)]
3. Odebráním &quot;//&quot; znaků Odkomentujte zvýrazněné řádky kódu a pak přidejte ID aplikace a tajný klíč. Po přidání těchto parametrů můžete projekt znovu zkompilovat:

    [!code-csharp[Main](external-authentication-services/samples/sample3.cs)]
4. Po stisknutí klávesy F5 k otevření webové aplikace ve webovém prohlížeči se zobrazí, že Facebook byl definován jako externí Služba ověřování:

    [![](external-authentication-services/_static/image74.png "Click to Expand the Image")](external-authentication-services/_static/image74.png)
5. Když kliknete na tlačítko **Facebook** , váš prohlížeč se přesměruje na přihlašovací stránku Facebooku:

    [![](external-authentication-services/_static/image22.png "Click to Expand the Image")](external-authentication-services/_static/image21.png)
6. Po zadání přihlašovacích údajů k Facebooku a kliknutí na **Přihlásit**se webový prohlížeč přesměruje zpátky do vaší webové aplikace. zobrazí se výzva k zadání **uživatelského jména** , které chcete přidružit k účtu Facebook:

    [![](external-authentication-services/_static/image24.png "Click to Expand the Image")](external-authentication-services/_static/image23.png)
7. Po zadání uživatelského jména a kliknutí na tlačítko **zaregistrovat** vaše webová aplikace zobrazí výchozí **domovskou stránku** pro váš účet Facebook:

    [![](external-authentication-services/_static/image26.png "Click to Expand the Image")](external-authentication-services/_static/image25.png)

<a id="GOOGLE"></a>
## <a name="enabling-google-authentication"></a>Povoluje se ověřování Google.

Použití ověřování Google vyžaduje, abyste vytvořili účet pro vývojáře Google a váš projekt bude vyžadovat ID aplikace a tajný klíč od společnosti Google, aby mohl fungovat. Informace o vytvoření účtu vývojáře Google a získání ID aplikace a tajného klíče najdete v tématu [https://developers.google.com](https://developers.google.com).

Pokud chcete povolit ověřování Google pro vaši webovou aplikaci, použijte následující postup:

1. Když je projekt otevřen v aplikaci Visual Studio 2017, otevřete soubor *Startup.auth.cs* .

2. Vyhledejte oddíl ověřování Google Code:

    [!code-csharp[Main](external-authentication-services/samples/sample4.cs)]
3. Odebráním &quot;//&quot; znaků Odkomentujte zvýrazněné řádky kódu a pak přidejte ID aplikace a tajný klíč. Po přidání těchto parametrů můžete projekt znovu zkompilovat:

    [!code-csharp[Main](external-authentication-services/samples/sample5.cs)]
4. Když stisknete klávesu F5 k otevření webové aplikace ve webovém prohlížeči, uvidíte, že Google byl definován jako externí Služba ověřování:

    [![](external-authentication-services/_static/image75.png "Click to Expand the Image")](external-authentication-services/_static/image75.png)
5. Když kliknete na tlačítko **Google** , váš prohlížeč se přesměruje na přihlašovací stránku Google:

    [![](external-authentication-services/_static/image32.png "Click to Expand the Image")](external-authentication-services/_static/image31.png)
6. Až zadáte svoje přihlašovací údaje Google a kliknete na **Přihlásit**, Google vás vyzve, abyste ověřili, že vaše webová aplikace má oprávnění k přístupu k vašemu účtu Google:

    [![](external-authentication-services/_static/image34.png "Click to Expand the Image")](external-authentication-services/_static/image33.png)
7. Když kliknete na **přijmout**, váš webový prohlížeč se přesměruje zpátky do vaší webové aplikace, kde se zobrazí výzva k zadání **uživatelského jména** , které chcete přidružit k vašemu účtu Google:

    [![](external-authentication-services/_static/image36.png "Click to Expand the Image")](external-authentication-services/_static/image35.png)
8. Po zadání uživatelského jména a kliknutí na tlačítko **zaregistrovat** vaše webová aplikace zobrazí výchozí **domovskou stránku** účtu Google:

    [![](external-authentication-services/_static/image38.png "Click to Expand the Image")](external-authentication-services/_static/image37.png)

<a id="MICROSOFT"></a>
## <a name="enabling-microsoft-authentication"></a>Povolení ověřování společnosti Microsoft

Ověřování společnosti Microsoft vyžaduje, abyste vytvořili vývojářský účet a aby fungovalo, vyžaduje ID klienta a tajný klíč klienta. Informace o vytvoření účtu Microsoft Developer a získání ID klienta a tajného kódu klienta najdete v tématu [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070).

Jakmile získáte klíč příjemce a tajný klíč příjemce, pomocí následujícího postupu povolte ověřování společnosti Microsoft pro vaši webovou aplikaci:

1. Když je projekt otevřen v aplikaci Visual Studio 2017, otevřete soubor *Startup.auth.cs* .

2. Vyhledejte část kódu ověřování společnosti Microsoft:

    [!code-csharp[Main](external-authentication-services/samples/sample6.cs)]
3. Odebráním &quot;//&quot; znaků Odkomentujte zvýrazněné řádky kódu a pak přidejte ID klienta a tajný klíč klienta. Po přidání těchto parametrů můžete projekt znovu zkompilovat:

    [!code-csharp[Main](external-authentication-services/samples/sample7.cs)]
4. Po stisknutí klávesy F5 k otevření webové aplikace ve webovém prohlížeči se zobrazí informace o tom, že společnost Microsoft byla definována jako externí Služba ověřování:

    [![](external-authentication-services/_static/image42.png "Click to Expand the Image")](external-authentication-services/_static/image41.png)
5. Když kliknete na tlačítko **Microsoft** , váš prohlížeč se přesměruje na přihlašovací stránku Microsoftu:

    [![](external-authentication-services/_static/image44.png "Click to Expand the Image")](external-authentication-services/_static/image43.png)
6. Po zadání přihlašovacích údajů Microsoftu a kliknutí na **Přihlásit**se zobrazí výzva, abyste ověřili, že vaše webová aplikace má oprávnění pro přístup k vašemu účet Microsoft:

    [![](external-authentication-services/_static/image46.png "Click to Expand the Image")](external-authentication-services/_static/image45.png)
7. Kliknete-li na tlačítko **Ano**, bude webový prohlížeč přesměrován zpět do vaší webové aplikace. zobrazí se výzva k zadání **uživatelského jména** , které chcete přidružit k vašemu účet Microsoft:

    [![](external-authentication-services/_static/image48.png "Click to Expand the Image")](external-authentication-services/_static/image47.png)
8. Po zadání uživatelského jména a kliknutí na tlačítko **zaregistrovat** se ve vaší webové aplikaci zobrazí výchozí **Domovská stránka** pro váš účet Microsoft:

    [![](external-authentication-services/_static/image50.png "Click to Expand the Image")](external-authentication-services/_static/image49.png)

<a id="TWITTER"></a>
## <a name="enabling-twitter-authentication"></a>Povolení ověřování na Twitteru

Ověřování pomocí Twitteru vyžaduje, abyste vytvořili vývojářský účet a aby mohli fungovat, vyžaduje klíč příjemce a klíč příjemce. Informace o vytvoření účtu vývojáře pro Twitter a získání klíče příjemce a tajného kódu příjemce najdete v tématu [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166).

Jakmile získáte klíč příjemce a tajný klíč příjemce, pomocí následujícího postupu povolte pro webovou aplikaci ověřování pomocí Twitteru:

1. Když je projekt otevřen v aplikaci Visual Studio 2017, otevřete soubor *Startup.auth.cs* .

2. Vyhledejte část s ověřováním na Twitteru v kódu:

    [!code-csharp[Main](external-authentication-services/samples/sample8.cs)]
3. Odebráním &quot;//&quot; znaků Odkomentujte zvýrazněné řádky kódu a pak přidejte svůj klíč příjemce a tajný klíč příjemce. Po přidání těchto parametrů můžete projekt znovu zkompilovat:

    [!code-csharp[Main](external-authentication-services/samples/sample9.cs)]
4. Po stisknutí klávesy F5 k otevření webové aplikace ve webovém prohlížeči se zobrazí, že Twitter byl definován jako externí Služba ověřování:

    [![](external-authentication-services/_static/image54.png "Click to Expand the Image")](external-authentication-services/_static/image53.png)
5. Když kliknete na tlačítko **Twitter** , váš prohlížeč se přesměruje na přihlašovací stránku Twitteru:

    [![](external-authentication-services/_static/image56.png "Click to Expand the Image")](external-authentication-services/_static/image55.png)
6. Po zadání přihlašovacích údajů pro Twitter a kliknutí na **autorizovat**se webový prohlížeč přesměruje zpátky do vaší webové aplikace. zobrazí se výzva k zadání **uživatelského jména** , které chcete přidružit k vašemu účtu Twitteru:

    [![](external-authentication-services/_static/image58.png "Click to Expand the Image")](external-authentication-services/_static/image57.png)
7. Po zadání uživatelského jména a kliknutí na tlačítko **zaregistrovat** se ve vaší webové aplikaci zobrazí výchozí **Domovská stránka** pro váš účet na Twitteru:

    [![](external-authentication-services/_static/image60.png "Click to Expand the Image")](external-authentication-services/_static/image59.png)

<a id="MOREINFO"></a>
## <a name="additional-information"></a>Další informace

Další informace o vytváření aplikací, které používají OAuth a OpenID, najdete v následujících adresách URL:

- [https://go.microsoft.com/fwlink/?LinkID=252166](https://go.microsoft.com/fwlink/?LinkID=252166)
- [https://go.microsoft.com/fwlink/?LinkID=243995](https://go.microsoft.com/fwlink/?LinkID=243995)

<a id="COMBINE"></a>
### <a name="combining-external-authentication-services"></a>Kombinování externích ověřovacích služeb

Pro větší flexibilitu můžete současně definovat více externích služeb ověřování – to umožní uživatelům vaší webové aplikace používat účet z kterékoli z povolených externích ověřovacích služeb:

[![](external-authentication-services/_static/image62.png "Click to Expand the Image")](external-authentication-services/_static/image61.png)

<a id="FQDN"></a>
### <a name="configure-iis-express-to-use-a-fully-qualified-domain-name"></a>Konfigurace IIS Express pro použití plně kvalifikovaného názvu domény

Někteří zprostředkovatelé externího ověřování nepodporují testování aplikace pomocí adresy HTTP, jako je `http://localhost:port/`. Chcete-li tento problém obejít, můžete přidat statické mapování plně kvalifikovaného názvu domény (FQDN) do souboru hostitelů a nakonfigurovat možnosti projektu v aplikaci Visual Studio 2017 pro použití plně kvalifikovaného názvu domény pro testování/ladění. Chcete-li tak učinit, proveďte následující kroky:

- Přidejte statický plně kvalifikovaný název domény pro mapování souboru hostitelů:

  1. Otevřete příkazový řádek se zvýšenými oprávněními v systému Windows.
  2. Zadejte následující příkaz:

      <kbd>Poznámkový blok%WinDir%\system32\drivers\etc\hosts</kbd>
  3. Do souboru hostitelů přidejte položku podobný následujícímu:

      <kbd>127.0.0.1 www.wingtiptoys.com</kbd>
  4. Uložte a zavřete soubor hostitelů.

- Nakonfigurujte projekt sady Visual Studio tak, aby používal plně kvalifikovaný název domény:

  1. Když je projekt otevřen v aplikaci Visual Studio 2017, klikněte na nabídku **projekt** a potom vyberte vlastnosti projektu. Například můžete vybrat **vlastnosti WebApplication1**.
  2. Vyberte kartu **Web** .
  3. Zadejte plně kvalifikovaný název domény pro <strong>adresu URL projektu</strong>. Zadejte například <kbd><http://www.wingtiptoys.com></kbd> , pokud se jednalo o mapování plně kvalifikovaného názvu domény, které jste přidali do souboru hostitelů.

- Nakonfigurujte IIS Express pro použití plně kvalifikovaného názvu domény pro vaši aplikaci:

    1. Otevřete příkazový řádek se zvýšenými oprávněními v systému Windows.
    2. Zadáním následujícího příkazu přejděte do složky IIS Express:

        <kbd>CD/d &quot;%ProgramFiles%\IIS Express&quot;</kbd>
    3. Zadáním následujícího příkazu přidejte do aplikace plně kvalifikovaný název domény:

        <kbd>Appcmd. exe nastavení konfigurace-oddíl: System. applicationHost/sites/+&quot;[name = ' WebApplication1 ']. Bindings. [Protocol = ' http ', bindingInformation = ' *: 80: www. wingtiptoys. com ']&quot;/Commit: apphost</kbd>

  Kde **WebApplication1** je název vašeho projektu a **bindingInformation** obsahuje číslo portu a plně kvalifikovaný název domény, které chcete použít pro testování.

<a id="OBTAIN"></a>
### <a name="how-to-obtain-your-application-settings-for-microsoft-authentication"></a>Jak získat nastavení aplikace pro ověřování Microsoftu

Propojení aplikace s Windows Live pro ověřování Microsoft je jednoduchý proces. Pokud jste ještě nepřipojili aplikaci k Windows Live, můžete použít následující postup:

1. Po zobrazení výzvy vyhledejte [https://go.microsoft.com/fwlink/?LinkID=144070](https://go.microsoft.com/fwlink/?LinkID=144070) a zadejte své účet Microsoft jméno a heslo a pak klikněte na **Přihlásit**se:

   <!--  [![](external-authentication-services/_static/image64.png "Click to Expand the Image")](external-authentication-services/_static/image63.png) -->
2. Vyberte **Přidat aplikaci** a po zobrazení výzvy zadejte název aplikace a potom klikněte na **vytvořit**:

    [![](external-authentication-services/_static/image79.png "Click to Expand the Image")](external-authentication-services/_static/image79.png)
3. V části **název** a jeho vlastnosti aplikace vyberte svou aplikaci.

4. Zadejte doménu přesměrování vaší aplikace. Zkopírujte **ID aplikace** a v části **tajné klíče aplikace**vyberte **generovat heslo**. Zkopírujte heslo, které se zobrazí. ID a heslo aplikace jsou ID klienta a tajný klíč klienta. Vyberte **OK** a pak ho **uložte**.

    [![](external-authentication-services/_static/image77.png "Click to Expand the Image")](external-authentication-services/_static/image77.png)

<a id="DISABLE"></a>
### <a name="optional-disable-local-registration"></a>Volitelné: zakázat místní registraci

Aktuální funkce místní registrace ASP.NET nezabrání v vytváření členských účtů automatizovaným programům (roboty). například pomocí technologie prevence a ověřování robota, jako je [CAPTCHA](../../../web-pages/overview/security/16-adding-security-and-membership.md). Z tohoto důvodu byste měli na přihlašovací stránce odebrat místní přihlašovací formulář a odkaz na registraci. Provedete to tak, že otevřete stránku *\_Login. cshtml* v projektu a pak na řádek zadáte komentář k místnímu přihlašovacímu panelu a odkazu na registraci. Výsledná stránka by měla vypadat jako následující ukázka kódu:

[!code-html[Main](external-authentication-services/samples/sample10.html)]

Po zakázání místního přihlašovacího panelu a registračního odkazu se na přihlašovací stránce zobrazí jenom externí poskytovatelé ověřování, které jste povolili:

[![](external-authentication-services/_static/image70.png "Click to Expand the Image")](external-authentication-services/_static/image69.png)

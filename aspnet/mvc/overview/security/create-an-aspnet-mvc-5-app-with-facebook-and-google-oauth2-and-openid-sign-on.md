---
uid: mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
title: Vytvoření aplikace MVC 5 pomocí služby Facebook, Twitter, LinkedIn a Google OAuth2 Signing (C#) | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci ASP.NET MVC 5, která uživatelům umožňuje přihlásit se pomocí OAuth 2,0 s přihlašovacími údaji z externího předběžné...
ms.author: riande
ms.date: 04/03/2015
ms.assetid: 81ee500f-fc37-40d6-8722-f1b64720fbb6
msc.legacyurl: /mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on
msc.type: authoredcontent
ms.openlocfilehash: dd2e55d68ceb5a90134e394c00f3a3a231cb27d6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78566078"
---
# <a name="create-an-aspnet-mvc-5-app-with-facebook-twitter-linkedin-and-google-oauth2-sign-on-c"></a>Vytvoření aplikace ASP.NET MVC 5 s přihlášením přes Facebook, Twitter, LinkedIn a Google OAuth2 (C#)

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci ASP.NET MVC 5, která uživatelům umožňuje přihlásit se pomocí [OAuth 2,0](http://oauth.net/2/) s přihlašovacími údaji od externího poskytovatele ověřování, jako je Facebook, Twitter, LinkedIn, Microsoft nebo Google. V zájmu zjednodušení se tento kurz zaměřuje na práci s přihlašovacími údaji z Facebooku a Google.
> 
> Povolení těchto přihlašovacích údajů na webech přináší významnou výhodu, protože miliony uživatelů již mají účty s těmito externími poskytovateli. Tito uživatelé můžou být přihlášeni k vašemu webu, pokud je nepotřebují vytvořit a zapamatovat si novou sadu přihlašovacích údajů.
> 
> Viz také [aplikace ASP.NET MVC 5 se serverem SMS a e-mailovým ověřováním pomocí e-mailu](aspnet-mvc-5-app-with-sms-and-email-two-factor-authentication.md).
> 
> Tento kurz také ukazuje, jak přidat data profilu pro uživatele a jak používat rozhraní API pro členství k přidávání rolí. Tento kurz napsal [Rick Anderson](https://blogs.msdn.com/rickAndy) (pořiďte prosím na Twitteru: [@RickAndMSFT](https://twitter.com/RickAndMSFT) ).

<a id="start"></a>
## <a name="getting-started"></a>začínáme

Začněte instalací a spuštěním [Visual Studio Express 2013 pro web](https://go.microsoft.com/fwlink/?LinkId=299058) nebo [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566). Nainstalujte Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) nebo vyšší. Nápovědu k Dropboxu, GitHubu, LinkedInu, Instagramu, vyrovnávací paměti, Salesforce, pára, výměně zásobníku, TripIt, Twitch, Twitteru, Yahoo! a dalším službám najdete v tomto [ukázkovém projektu](https://github.com/matthewdunsdon/oauthforaspnet).

> [!NOTE]
> Pokud chcete používat Google OAuth 2 a ladit místně bez upozornění SSL, musíte nainstalovat Visual Studio [2013 Update 3](https://go.microsoft.com/fwlink/?LinkId=390521) nebo vyšší.

Na **úvodní** stránce klikněte na **Nový projekt** , nebo můžete použít nabídku a vybrat **soubor**a pak **Nový projekt**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image1.png)  

<a id="1st"></a>
## <a name="creating-your-first-application"></a>Vytvoření první aplikace

Klikněte **na nový projekt** **, pak na** levé straně vyberte **vizuál C#**  a potom vyberte **Webová aplikace ASP.NET**. Pojmenujte projekt "MvcAuth" a klikněte na tlačítko **OK**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image2.png)

V dialogovém okně **Nový projekt ASP.NET** klikněte na **MVC**. Pokud ověřování neplatí pro **jednotlivé uživatelské účty**, klikněte na tlačítko **změnit ověřování** a vyberte **jednotlivé uživatelské účty**. Když zkontrolujete **hostitele v cloudu**, aplikace bude velmi snadná pro hostování v Azure.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image3.png)

Pokud jste vybrali možnost **hostitel v cloudu**, dokončete dialog konfigurace.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image4.png)

### <a name="use-nuget-to-update-to-the-latest-owin-middleware"></a>Použití NuGet k aktualizaci na nejnovější middleware OWIN

Pomocí Správce balíčků NuGet aktualizujte [middleware Owin](../../../aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana.md). V nabídce vlevo vyberte **aktualizace** . Můžete kliknout na tlačítko **Aktualizovat vše** nebo můžete vyhledat jenom Owin balíčky (zobrazené na následujícím obrázku):

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image5.png)

Na následujícím obrázku jsou zobrazeny pouze balíčky OWIN:

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image6.png)

V konzole správce balíčků (PMC) můžete zadat příkaz `Update-Package`, který bude aktualizovat všechny balíčky.

Spusťte aplikaci stisknutím klávesy **F5** nebo **kombinací kláves CTRL + F5** . Na následujícím obrázku je číslo portu 1234. Při spuštění aplikace se zobrazí jiné číslo portu.

V závislosti na velikosti okna prohlížeče možná budete muset kliknout na navigační ikonu, aby se zobrazily odkazy **Domů**, **informace**, **kontakt**, **registrace** a **přihlášení** .

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image7.png)  
![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image8.png) 

<a id="ssl"></a>
## <a name="setting-up-ssl-in-the-project"></a>Nastavení SSL v projektu

Pokud se chcete připojit k poskytovatelům ověřování, jako je Google a Facebook, budete muset nastavit službu IIS Express, aby používala protokol SSL. Je důležité, abyste po přihlášení používali protokol SSL a nevrátili se zpátky na HTTP. váš přihlašovací soubor cookie je stejně tajný jako uživatelské jméno a heslo a bez použití protokolu SSL, který odesíláte do prostého textu po celém drátě. Kromě toho už jste popsali čas k provedení metody handshake a zabezpečení kanálu (což je hromadný protokol HTTPS, než HTTP) předtím, než se spustí kanál MVC, takže se po přihlášení znovu přesměruje na protokol HTTP, a to tak, že se aktuální žádost nebo budoucnost neuplatní. požadavky jsou mnohem rychlejší.

1. V **Průzkumník řešení**klikněte na projekt **MvcAuth** .
2. Stiskněte klávesu F4 pro zobrazení vlastností projektu. Případně můžete v nabídce **zobrazení** vybrat **okno Vlastnosti**.
3. Změňte možnost **SSL povoleno** na hodnotu true.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image9.png)
4. Zkopírujte adresu URL SSL (která bude `https://localhost:44300/`, pokud jste nevytvořili jiné projekty SSL).
5. V **Průzkumník řešení**klikněte pravým tlačítkem na projekt **MvcAuth** a vyberte **vlastnosti**.
6. Vyberte kartu **Web** a pak vložte adresu URL SSL do pole **Adresa URL projektu** . Uložte soubor (CTL + S). Tuto adresu URL budete potřebovat ke konfiguraci aplikací pro Facebook a Google Authentication.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image10.png)
7. Přidejte atribut [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) do kontroleru `Home`, aby se vyžadovalo, aby všechny požadavky měly používat protokol HTTPS. Bezpečnějším přístupem je přidání filtru [RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute.aspx) do aplikace. Přečtěte si část &quot;Ochrana aplikace pomocí protokolu SSL a&quot; autorizace atributu v tomto kurzu [vytvořte aplikaci ASP.NET MVC s ověřováním a SQL DB a nasaďte ji do Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Část domovského kontroleru je uvedená níže.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample1.cs?highlight=1)]
8. Stiskněte klávesy CTRL+F5 a spusťte aplikaci. Pokud jste certifikát nainstalovali v minulosti, můžete přeskočit zbytek této části a přejít na [Vytvoření aplikace Google pro OAuth 2 a připojení aplikace k projektu](#goog), jinak postupujte podle pokynů pro důvěřování certifikátu podepsanému svým držitelem, který IIS Express vygeneroval.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image11.png)
9. Přečtěte si dialogové okno **Upozornění zabezpečení** a pak klikněte na tlačítko **Ano** , pokud chcete nainstalovat certifikát reprezentující localhost.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image12.png)
10. Aplikace IE zobrazuje *domovskou* stránku a neexistují žádná upozornění SSL.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image13.png)
11. Google Chrome také akceptuje certifikát a zobrazí obsah HTTPS bez upozornění. Firefox používá vlastní úložiště certifikátů, takže zobrazí upozornění. V případě naší aplikace můžete bezpečně kliknout na možnost **rozumím rizikům**.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image14.png)

<a id="goog"></a>
## <a name="creating-a-google-app-for-oauth-2-and-connecting-the-app-to-the-project"></a>Vytvoření aplikace Google pro OAuth 2 a připojení aplikace k projektu

> [!WARNING]
> Informace o aktuálních pokynech k Google OAuth najdete [v tématu Konfigurace ověřování Google v ASP.NET Core](/aspnet/core/security/authentication/social/google-logins).

1. Přejděte do [konzoly pro vývojáře Google](https://console.developers.google.com/).
2. Pokud jste projekt ještě nevytvořili, vyberte na levé kartě možnost **přihlašovací údaje** a pak vyberte **vytvořit**.
3. Na levé kartě klikněte na **přihlašovací údaje**.
4. Klikněte na **vytvořit přihlašovací údaje** a pak na **ID klienta OAuth**. 

    1. V dialogovém okně **vytvořit ID klienta** ponechte výchozí **webovou aplikaci** pro typ aplikace.
    2. Nastavte **ověřené zdroje JavaScriptu** na adresu URL SSL, kterou jste použili výše (`https://localhost:44300/`, pokud jste nevytvořili jiné projekty SSL).
    3. Nastavte **autorizovaný identifikátor URI pro přesměrování** na:  
         `https://localhost:44300/signin-google`
5. Klikněte na položku nabídky obrazovka pro vyjádření souhlasu OAuth a pak nastavte svou e-mailovou adresu a název produktu. Po vyplnění formuláře klikněte na **Uložit**.
6. Klikněte na položku nabídky knihovna, vyhledejte **Google + API**, klikněte na ni a potom stiskněte povolit.
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image15.png)  
  
   Následující obrázek ukazuje povolená rozhraní API.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image16.png)
7. Ve Správci rozhraní API Google API navštivte kartu **přihlašovací údaje** a získejte **ID klienta**. Stáhněte si a uložte soubor JSON s použitím tajných klíčů. Zkopírujte a vložte **ClientID** a **ClientSecret** do metody `UseGoogleAuthentication` nalezené v souboru *Startup.auth.cs* ve složce *app_start* . Níže uvedené hodnoty **ClientID** a **ClientSecret** jsou ukázky a nefungují.

    [!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample2.cs?highlight=37-39)]

    > [!WARNING]
    > Zabezpečení – nikdy neukládejte citlivá data ve zdrojovém kódu. Účet a přihlašovací údaje se přidají do výše uvedeného kódu, aby se ukázka snadno zachovala. Další informace najdete v tématu [osvědčené postupy pro nasazení hesel a dalších citlivých dat do ASP.NET a Azure App Service](../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).
8. Stisknutím **kombinace kláves CTRL + F5** Sestavte a spusťte aplikaci. Klikněte na odkaz **Přihlásit** se.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image17.png)
9. V části **použít jinou službu pro přihlášení**klikněte na **Google**.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image18.png)

    > [!NOTE]
    > Pokud jste si nedostali některý z výše uvedených kroků, dojde k chybě HTTP 401. Překontrolujte výše uvedené kroky. Pokud nejste požádáni o nastavení (například **název produktu**), přidejte chybějící položku a uložte ji. aby ověřování fungovalo, může trvat několik minut.
10. Budete přesměrováni na web Google, kam budete zadávat své přihlašovací údaje.   
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image19.png)
11. Po zadání přihlašovacích údajů se zobrazí výzva k udělení oprávnění k této webové aplikaci, kterou jste právě vytvořili:
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image20.png)
12. Klikněte na **přijmout**. Nyní budete přesměrováni zpět na stránku **registrace** aplikace MvcAuth, kde můžete zaregistrovat svůj účet Google. Máte možnost změnit název místní registrace e-mailu, který se používá pro váš účet Gmail, ale obecně chcete zachovat výchozí alias e-mailu (tj. ten, který jste použili pro ověřování). Klikněte na **zaregistrovat**.  
  
    ![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image21.png)

<a id="fb"></a>
## <a name="creating-the-app-in-facebook-and-connecting-the-app-to-the-project"></a>Vytvoření aplikace na Facebooku a připojení aplikace k projektu

> [!WARNING]
> Pokyny k aktuálním OAuth2 ověřování na Facebooku najdete v tématu [Konfigurace ověřování na Facebooku](/aspnet/core/security/authentication/social/facebook-logins) .

<a id="mdb"></a>
## <a name="examine-the-membership-data"></a>Prověřte data členství

V nabídce **zobrazení** klikněte na příkaz **Průzkumník serveru**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image32.png)

Rozbalte položku **DefaultConnection (MvcAuth)** , rozbalte položku **tabulky**, klikněte pravým tlačítkem myši na položku **AspNetUsers** a klikněte na možnost **Zobrazit data tabulky**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image33.png)

![data tabulky aspnetusers](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image34.png)

<a id="ap"></a>
## <a name="adding-profile-data-to-the-user-class"></a>Přidání dat profilu do třídy uživatele

V této části přidáte k uživatelským datům během registrace datum narození a domovské město, jak je znázorněno na následujícím obrázku.

![REG s domovským městem a bday](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image35.png)

Otevřete soubor *Models\IdentityModels.cs* a přidejte vlastnosti rodného data a domovské města:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample4.cs?highlight=3-4)]

Otevřete soubor *Models\AccountViewModels.cs* a nastavte vlastnosti rodného data a domovské města v `ExternalLoginConfirmationViewModel`.

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample5.cs?highlight=8-9)]

Otevřete soubor *Controllers\AccountController.cs* a přidejte kód pro datum narození a domovské město v metodě `ExternalLoginConfirmation` akce, jak je znázorněno níže:

[!code-csharp[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample6.cs?highlight=21-23)]

Přidejte datum narození a domovské město do souboru *Views\Account\ExternalLoginConfirmation.cshtml* :

[!code-cshtml[Main](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/samples/sample7.cshtml?highlight=27-40)]

Odstraňte databázi členství, abyste mohli znovu zaregistrovat svůj účet Facebook s vaší aplikací a ověřit, že můžete přidat nové informace o profilu narození a domovské města.

Z **Průzkumník řešení**klikněte na ikonu **Zobrazit všechny soubory** , klikněte pravým tlačítkem na *přidat\_Data\aspnet-MvcAuth-&lt;dateStamp&gt;. mdf* a klikněte na **Odstranit**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image36.png)

V nabídce **nástroje** klikněte na **Správce balíčků NuGet**a pak klikněte na **Konzola správce balíčků** (PMC). Do PMC zadejte následující příkazy.

1. Povolit – migrace
2. Inicializace přidání – migrace
3. Aktualizace – databáze

Spusťte aplikaci a pomocí Facebooku a Google se přihlaste a zaregistrujte některé uživatele.

## <a name="examine-the-membership-data"></a>Prověřte data členství

V nabídce **zobrazení** klikněte na příkaz **Průzkumník serveru**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image37.png)

Klikněte pravým tlačítkem na **AspNetUsers** a pak klikněte na **Zobrazit data tabulky**.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image38.png)

Pole `HomeTown` a `BirthDate` jsou uvedena níže.

![](create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on/_static/image39.png)

<a id="off"></a>
## <a name="logging-off-your-app-and-logging-in-with-another-account"></a>Odhlášení aplikace a přihlášení pomocí jiného účtu

Pokud se přihlásíte k aplikaci přes Facebook, a pak se odhlásíte a zkusíte se přihlásit pomocí jiného účtu Facebook (pomocí stejného prohlížeče), budete k němu přihlášeni hned přes předchozí účet Facebook, který jste použili. Aby bylo možné použít jiný účet, musíte přejít na Facebook a odhlásit se v Facebooku. Stejné pravidlo platí pro všechny ostatní poskytovatele ověřování třetí strany. Případně se můžete přihlásit pomocí jiného účtu pomocí jiného prohlížeče.

## <a name="next-steps"></a>Další kroky

Pokyny pro Yahoo a LinkedIn najdete v tématu [představení zprostředkovatelů zabezpečení Yahoo a LinkedIn OAuth pro Owin](http://www.jerriepelser.com/blog/introducing-the-yahoo-linkedin-oauth-security-providers-for-owin/) pomocí Jerrie Pelser. Pokud chcete získat tlačítka pro přihlášení přes sociální sítě, přečtěte si část Jerrie – tlačítka pro přihlášení k ASP.NET MVC 5.

Postupujte podle kurzu [Vytvoření aplikace ASP.NET MVC s ověřováním a SQL DB a nasaďte ji do Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data), která pokračuje v tomto kurzu a zobrazí se následující:

1. Jak nasadit aplikaci do Azure
2. Jak zabezpečit aplikaci pomocí rolí.
3. Jak zabezpečit aplikaci pomocí [atribut RequireHttps](https://msdn.microsoft.com/library/system.web.mvc.requirehttpsattribute(v=vs.108).aspx) a [autorizovat](https://msdn.microsoft.com/library/system.web.mvc.authorizeattribute(v=vs.100).aspx) filtry.
4. Jak používat rozhraní API pro členství k přidávání uživatelů a rolí.

Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit. Můžete také požádat o nová témata při [zobrazení kódu](http://aspnet.uservoice.com/forums/228522-show-me-how-with-code). Můžete dokonce požádat o nové funkce, které se mají přidat do ASP.NET, a hlasovat o nich. Můžete například hlasovat pro nástroj k [vytváření a správě uživatelů a rolí.](http://aspnet.uservoice.com/forums/41199-general-asp-net/suggestions/5646857-asp-net-identity-membership-db-tool-to-mangage-use)

Dobré vysvětlení, jak služba ASP.NET External Authentication Services funguje, najdete v tématu věnovaném [externím ověřovacím službám](https://asp.net/web-api/overview/security/external-authentication-services)Robert blog. Článek Robert také podrobně popisuje, jak povolit ověřování Microsoft a Twitter. Skvělého kurzu pro Dykstra [EF/MVC](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) ukazuje, jak pracovat s Entity Framework.

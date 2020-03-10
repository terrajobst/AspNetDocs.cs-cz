---
uid: mvc/overview/older-versions/using-oauth-providers-with-mvc
title: Použití zprostředkovatelů OAuth s MVC 4 | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci ASP.NET MVC 4, která umožňuje uživatelům přihlásit se pomocí přihlašovacích údajů od externího poskytovatele, jako je například Facebo...
ms.author: riande
ms.date: 06/19/2013
ms.assetid: 7a87f16f-0e19-4f15-a88a-094ae866c4a2
msc.legacyurl: /mvc/overview/older-versions/using-oauth-providers-with-mvc
msc.type: authoredcontent
ms.openlocfilehash: 5dfd1305376a62f4987caea242ca0f6aac1018e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539079"
---
# <a name="using-oauth-providers-with-mvc-4"></a>Použití poskytovatelů OAuth v MVC 4

tím, že [FitzMacken](https://github.com/tfitzmac)

> V tomto kurzu se dozvíte, jak vytvořit webovou aplikaci ASP.NET MVC 4, která uživatelům umožňuje přihlásit se pomocí přihlašovacích údajů od externího poskytovatele, jako je Facebook, Twitter, Microsoft nebo Google, a potom integrovat některé funkce od těchto poskytovatelů do vaší Webová aplikace V zájmu jednoduchosti se tento kurz zaměřuje na práci s přihlašovacími údaji z Facebooku.
> 
> Pokud chcete použít externí přihlašovací údaje ve webové aplikaci ASP.NET MVC 5, přečtěte si téma [Vytvoření aplikace ASP.NET MVC 5 s Facebookem a Google OAuth2 a OpenID Signing](../security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).
> 
> Povolení těchto přihlašovacích údajů na webech přináší významnou výhodu, protože miliony uživatelů již mají účty s těmito externími poskytovateli. Tito uživatelé můžou být přihlášeni k vašemu webu, pokud je nepotřebují vytvořit a zapamatovat si novou sadu přihlašovacích údajů. Až se uživatel přihlásí pomocí jednoho z těchto poskytovatelů, můžete do poskytovatele začlenit sociální operace.

## <a name="what-youll-build"></a>Co sestavíte

V tomto kurzu existují dva hlavní cíle:

1. Povolí uživateli přihlášení pomocí přihlašovacích údajů z poskytovatele OAuth.
2. Načtěte informace o účtu ze zprostředkovatele a integrujte tyto informace s registrací účtu pro váš web.

I když se příklady v tomto kurzu zaměřují na použití Facebooku jako poskytovatele ověřování, můžete kód upravit tak, aby používal libovolného poskytovatele. Postup implementace libovolného poskytovatele se velmi podobá postupům, které se zobrazí v tomto kurzu. Při přímém volání sady rozhraní API poskytovatele se zobrazí jenom významné rozdíly.

## <a name="prerequisites"></a>Předpoklady

- [Microsoft Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads#vs) nebo [Microsoft Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/eng/downloads#d-2012-express)

Nebo

- Microsoft Visual Studio 2010 SP1 nebo [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/visualstudio/eng/downloads#d-2010-express)
- [ASP.NET MVC 4](https://go.microsoft.com/fwlink/?LinkId=243392)

Kromě toho toto téma předpokládá, že máte základní znalosti o ASP.NET MVC a Visual Studiu. Pokud potřebujete Úvod do ASP.NET MVC 4, přečtěte si [Úvod do ASP.NET MVC 4](getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md).

## <a name="create-the-project"></a>Vytvoření projektu

V aplikaci Visual Studio vytvořte novou webovou aplikaci ASP.NET MVC 4 a pojmenujte ji &quot;OAuthMVC&quot;. Můžete cílit buď na .NET Framework 4,5 nebo 4.

![vytvořit projekt](using-oauth-providers-with-mvc/_static/image1.png)

V novém okně projektu ASP.NET MVC 4 vyberte možnost **Internet aplikace** a ponechte **Razor** jako zobrazovací modul.

![vybrat internetovou aplikaci](using-oauth-providers-with-mvc/_static/image2.png)

## <a name="enable-a-provider"></a>Povolení poskytovatele

Když vytvoříte webovou aplikaci MVC 4 se šablonou internetové aplikace, projekt se vytvoří se souborem s názvem AuthConfig.cs ve složce App\_Start.

![Soubor AuthConfig](using-oauth-providers-with-mvc/_static/image3.png)

Soubor AuthConfig obsahuje kód pro registraci klientů pro externí poskytovatele ověřování. Ve výchozím nastavení je tento kód zakomentován, takže žádný z externích zprostředkovatelů není povolen.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample1.cs)]

Chcete-li použít externího klienta ověřování, je nutné tento kód odkomentovat. Odkomentujete pouze poskytovatele, které chcete zahrnout do webu. V tomto kurzu povolíte jenom přihlašovací údaje pro Facebook.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample2.cs)]

Všimněte si, že metoda v předchozím příkladu obsahuje prázdné řetězce pro parametry registrace. Pokud se pokusíte spustit aplikaci nyní, aplikace vyvolá výjimku argumentu, protože pro parametry nejsou povoleny prázdné řetězce. Chcete-li zadat platné hodnoty, je nutné zaregistrovat svůj web u externích zprostředkovatelů, jak je znázorněno v následující části.

## <a name="registering-with-an-external-provider"></a>Registrace u externího poskytovatele

Chcete-li ověřit uživatele s přihlašovacími údaji od externího poskytovatele, je nutné zaregistrovat svůj web u poskytovatele. Při registraci lokality se zobrazí parametry (například klíč, ID a tajný kód), které se mají zahrnout při registraci klienta. Musíte mít účet s poskytovateli, které chcete použít.

V tomto kurzu se nezobrazují všechny kroky, které musíte provést při registraci u těchto poskytovatelů. Postup obvykle není obtížné. Chcete-li úspěšně zaregistrovat web, postupujte podle pokynů uvedených na těchto webech. Chcete-li začít s registrací lokality, přečtěte si web pro vývojáře:

- [Facebook](https://developers.facebook.com/)
- [Google](https://developers.google.com/)
- [Microsoft](http://manage.dev.live.com/)
- [Twitter](https://dev.twitter.com/)

Při registraci webu na Facebooku můžete zadat &quot;localhost&quot; pro doménu lokality a `&quot; http://localhost/&quot;` pro adresu URL, jak je znázorněno na následujícím obrázku. Použití místního hostitele funguje s většinou zprostředkovatelů, ale v současné době nepracuje u poskytovatele Microsoftu. Pro poskytovatele Microsoftu musíte zahrnout platnou adresu URL webu.

![Registrovat web](using-oauth-providers-with-mvc/_static/image4.png)

V předchozím obrázku se odebraly hodnoty ID aplikace, tajného klíče aplikace a kontaktní e-mailové adresy. Když ve skutečnosti zaregistrujete lokalitu, budou tyto hodnoty k dispozici. Hodnoty pro ID aplikace a tajný klíč aplikace si poznamenejte, protože je přidáte do své aplikace.

## <a name="creating-test-users"></a>Vytváření testovacích uživatelů

Pokud si nejste při testování svého webového serveru použili existující účet Facebook, můžete tuto část přeskočit.

Můžete snadno vytvořit testovací uživatele pro aplikaci na stránce správy aplikace Facebook. Pomocí těchto testovacích účtů se můžete přihlásit k webu. Testovací uživatele vytvoříte kliknutím na odkaz **role** v levém navigačním podokně a kliknutím na odkaz **vytvořit** .

![Vytvoření testovacích uživatelů](using-oauth-providers-with-mvc/_static/image5.png)

Web Facebook automaticky vytvoří počet zkušebních účtů, které požadujete.

## <a name="adding-application-id-and-secret-from-the-provider"></a>Přidání ID aplikace a tajného klíče ze zprostředkovatele

Teď, když jste dostali ID a tajný kód z Facebooku, vraťte se do souboru AuthConfig a přidejte je jako hodnoty parametru. Níže uvedené hodnoty nejsou reálné hodnoty.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample3.cs)]

## <a name="log-in-with-external-credentials"></a>Přihlášení pomocí externích přihlašovacích údajů

To je všechno, co musíte udělat, abyste na svém webu mohli povolit externí přihlašovací údaje. Spusťte aplikaci a klikněte na odkaz pro přihlášení v pravém horním rohu. Šablona automaticky rozpozná, že jste zaregistrováni Facebook jako poskytovatele a obsahuje tlačítko pro poskytovatele. Pokud zaregistrujete více zprostředkovatelů, bude automaticky zahrnuto tlačítko pro každé z nich.

![externí přihlášení](using-oauth-providers-with-mvc/_static/image6.png)

Tento kurz nepopisuje, jak přizpůsobit tlačítka pro přihlášení externích poskytovatelů. Informace najdete v tématu [přizpůsobení uživatelského rozhraní přihlášení při použití OAuth/OpenID](https://blogs.msdn.com/b/pranav_rastogi/archive/2012/08/24/customizing-the-login-ui-when-using-oauth-openid.aspx).

Kliknutím na tlačítko Facebook se přihlaste s přihlašovacími údaji pro Facebook. Když vyberete jednoho z externích zprostředkovatelů, budete přesměrováni na tuto lokalitu a vyzve se k přihlášení této služby.

Na následujícím obrázku vidíte přihlašovací obrazovku pro Facebook. V takovém případě se k přihlášení k webu s názvem oauthmvcexample používá účet Facebook.

![ověřování Facebooku](using-oauth-providers-with-mvc/_static/image7.png)

Po přihlášení pomocí přihlašovacích údajů k Facebooku stránka informuje uživatele o tom, že tento web bude mít přístup k základním informacím.

![požádat o oprávnění](using-oauth-providers-with-mvc/_static/image8.png)

Po výběru možnosti **Přejít do aplikace**musí uživatel zaregistrovat lokalitu. Následující obrázek ukazuje registrační stránku poté, co se uživatel přihlásí pomocí přihlašovacích údajů k Facebooku. Uživatelské jméno je obvykle předem vyplněno názvem od poskytovatele.

![register](using-oauth-providers-with-mvc/_static/image9.png)

Registraci dokončíte kliknutím na **Registrovat** . Zavřete prohlížeč.

Můžete vidět, že se nový účet přidal do vaší databáze. V Průzkumník serveru otevřete databázi **DefaultConnection** a otevřete složku Tables ( **tabulky** ).

![tabulky databáze](using-oauth-providers-with-mvc/_static/image10.png)

Klikněte pravým tlačítkem myši na tabulku **USERPROFILE** a vyberte možnost **Zobrazit data tabulky**.

![Zobrazit data](using-oauth-providers-with-mvc/_static/image11.png)

Zobrazí se nový účet, který jste přidali. Podívejte se na data na **webové stránce\_tabulce OAuthMembership** . Pro účet, který jste právě přidali, se zobrazí další data týkající se externího poskytovatele.

Pokud chcete povolit jenom externí ověřování, budete hotovi. Informace ze zprostředkovatele ale můžete dál integrovat do nového procesu registrace uživatele, jak je znázorněno v následujících oddílech.

## <a name="create-models-for-additional-user-information"></a>Vytvořit modely pro další informace o uživateli

Jak jste si všimli v předchozích částech, nemusíte načítat žádné další informace, aby byla integrovaná registrace účtu fungovat. Většina externích zprostředkovatelů ale přechází k dalším informacím o uživateli. V následujících částech se dozvíte, jak tyto informace uchovat a jak je Uložit do databáze. Konkrétně si zachováte hodnoty pro úplné jméno uživatele, identifikátor URI osobní webové stránky uživatele a hodnotu, která indikuje, jestli je účet ověřený na Facebooku.

Pomocí [migrace Code First](https://msdn.microsoft.com/data/jj591621) přidáte tabulku pro ukládání dalších informací o uživateli. Přidáte tabulku do existující databáze, takže nejprve budete muset vytvořit snímek aktuální databáze. Vytvořením snímku aktuální databáze můžete později vytvořit migraci, která obsahuje pouze novou tabulku. Vytvoření snímku aktuální databáze:

1. Otevřete **konzolu Správce balíčků** .
2. Spuštění příkazu **Povolit – migrace**
3. Spuštění příkazu **Přidat-migraci – počáteční – IgnoreChanges**
4. Spuštění příkazu **Update-Database**

Teď budete přidávat nové vlastnosti. Ve složce modely otevřete soubor AccountModels.cs a najděte třídu RegisterExternalLoginModel. Třída RegisterExternalLoginModel obsahuje hodnoty, které se vrátí od poskytovatele ověřování. Přidejte vlastnosti pojmenované FullName a Link, jak je zvýrazněno níže.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample4.cs?highlight=9-13)]

Také v AccountModels.cs přidejte novou třídu s názvem ExtraUserInformation. Tato třída představuje novou tabulku, která bude vytvořena v databázi.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample5.cs)]

Ve třídě UsersContext přidejte zvýrazněný kód pro vytvoření vlastnosti Negenerickými pro novou třídu.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample6.cs?highlight=9)]

Nyní jste připraveni vytvořit novou tabulku. Znovu otevřete konzolu Správce balíčků a tentokrát:

1. Spusťte příkaz **Add-Migration AddExtraUserInformation**
2. Spuštění příkazu **Update-Database**

Nová tabulka teď v databázi existuje.

## <a name="retrieve-the-additional-data"></a>Načtení dalších dat

Existují dva způsoby, jak načíst další uživatelská data. Prvním způsobem je uchovávat uživatelská data, která se ve výchozím nastavení předávají, během žádosti o ověření. Druhý způsob je konkrétně zavolat rozhraní API poskytovatele a požádat o další informace. Hodnoty pro FullName a Link jsou automaticky předávány Facebookem. Hodnota, která označuje, zda je na Facebooku ověřeno, že je účet načten prostřednictvím volání rozhraní API Facebooku. Nejdřív naplníte hodnoty pro FullName a Link a později se zobrazí ověřená hodnota.

Pokud chcete načíst další uživatelská data, otevřete soubor **AccountController.cs** ve složce **Controllers** .

Tento soubor obsahuje logiku pro protokolování, registraci a správu účtů. Zejména si všimněte, že metody s názvem **ExternalLoginCallback** a **ExternalLoginConfirmation**. V rámci těchto metod můžete přidat kód pro přizpůsobení vnějších operací přihlášení pro aplikaci. První řádek metody **ExternalLoginCallback** obsahuje:

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample7.cs)]

Další uživatelská data jsou předána zpět ve vlastnosti **ExtraData** objektu **AuthenticationResult** , který je vrácen z metody **VerifyAuthentication** . Klient Facebooku obsahuje ve vlastnosti **ExtraData** následující hodnoty:

- id
- jméno
- odkaz
- gender (pohlaví)
- accesstoken

Jiní poskytovatelé budou mít podobná, ale mírně odlišná data ve vlastnosti ExtraData.

Pokud je uživatel ve vašem webu nový, načtou se další data a předají se tato data do zobrazení potvrzení. Poslední blok kódu v metodě je spuštěn pouze v případě, že je uživatel ve vašem webu nový. Nahraďte následující řádek:

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample8.cs)]

s tímto řádkem:

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample9.cs)]

Tato změna zahrnuje pouze hodnoty vlastností FullName a Link.

V metodě **ExternalLoginConfirmation** upravte kód tak, jak je zvýrazněný níže, aby se uložily Další informace o uživateli.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample10.cs?highlight=4,7-13)]

## <a name="adjusting-the-view"></a>Úprava zobrazení

Další uživatelská data, která načtete od poskytovatele, se zobrazí na stránce registrace.

Ve složce **zobrazení**/**účtu** otevřete **ExternalLoginConfirmation. cshtml**. Pod existujícím polem pro uživatelské jméno přidejte pole pro FullName, Link a PictureLink.

[!code-cshtml[Main](using-oauth-providers-with-mvc/samples/sample11.cshtml)]

Teď jste skoro připraveni spustit aplikaci a zaregistrovat nového uživatele s dalšími uloženými informacemi. Musíte mít účet, který ještě není zaregistrovaný v lokalitě. Můžete buď použít jiný testovací účet, nebo odstranit řádky v účtu **USERPROFILE** a **webpages\_OAuthMembership** tabulky pro účet, který chcete znovu použít. Odstraněním těchto řádků se ujistíte, že je účet zaregistrovaný znovu.

Spusťte aplikaci a zaregistrujte nového uživatele. Všimněte si, že tato stránka potvrzení obsahuje více hodnot.

![register](using-oauth-providers-with-mvc/_static/image12.png)

Po dokončení registrace zavřete prohlížeč. Vyhledejte v databázi, abyste si všimli nových hodnot v tabulce **ExtraUserInformation** .

## <a name="install-nuget-package-for-facebook-api"></a>Nainstalovat balíček NuGet pro Facebook API

Facebook poskytuje [rozhraní API](https://developers.facebook.com/docs/reference/apis/) , které můžete volat k provádění operací. Rozhraní API Facebooku můžete volat buď přímým odesláním požadavků HTTP, nebo pomocí instalace balíčku NuGet, který usnadňuje odesílání těchto požadavků. V tomto kurzu se zobrazí použití balíčku NuGet, ale instalace balíčku NuGet není nezbytná. V tomto kurzu se dozvíte, jak C# používat balíček sady Facebook SDK. K dispozici jsou další balíčky NuGet, které pomáhají s voláním rozhraní API Facebooku.

V oknech **Spravovat balíčky NuGet** vyberte balíček sady Facebook C# SDK.

![instalovat balíček](using-oauth-providers-with-mvc/_static/image13.png)

K volání operace, která C# pro uživatele vyžaduje přístupový token, použijete Facebook SDK. V další části se dozvíte, jak získat přístupový token.

## <a name="retrieve-access-token"></a>Načíst přístupový token

Většina externích zprostředkovatelů po ověření přihlašovacích údajů uživatele předává zpět přístupový token. Tento přístupový token je velmi důležitý, protože umožňuje volat operace, které jsou k dispozici jenom pro ověřené uživatele. Proto pokud chcete poskytnout více funkcí, je nutné načíst a uložit přístupový token.

V závislosti na externím poskytovateli může být přístupový token platný jenom po omezené množství času. Abyste měli jistotu, že máte platný přístupový token, načtěte ho pokaždé, když se uživatel přihlásí, a místo uložení do databáze ho uložte jako hodnotu relace.

V metodě **ExternalLoginCallback** je přístupový token také předán zpátky ve vlastnosti **ExtraData** objektu **AuthenticationResult** . Přidejte zvýrazněný kód do **ExternalLoginCallback** k uložení přístupového tokenu do objektu **Session** . Tento kód se spustí pokaždé, když se uživatel přihlásí pomocí účtu Facebook.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample12.cs?highlight=11-14)]

I když tento příklad načte přístupový token z Facebooku, můžete získat přístupový token z libovolného externího poskytovatele pomocí stejného klíče s názvem &quot;AccessToken&quot;.

## <a name="logging-off"></a>Odhlášení

Výchozí metoda **odhlášení** zaznamená uživatele z vaší aplikace, ale neprotokoluje uživatele z externího poskytovatele. Pokud chcete odhlásit uživatele z Facebooku a zabránit tomu, aby se token zachoval po odhlášení uživatele, můžete do metody **odhlášení** v AccountController přidat následující zvýrazněný kód.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample13.cs?highlight=6-14)]

Hodnota, kterou zadáte v parametru `next`, je adresa URL, která se má použít po odhlášení uživatele z Facebooku. Při testování na místním počítači byste zadali správné číslo portu pro místní web. V produkčním prostředí byste zadali výchozí stránku, například contoso.com.

## <a name="retrieve-user-information-that-requires-the-access-token"></a>Načíst informace o uživateli, které vyžadují přístupový token

Po uložení přístupového tokenu a instalaci balíčku Facebook C# SDK můžete použít společně k vyžádání dalších informací o uživateli z Facebooku. V metodě **ExternalLoginConfirmation** vytvořte instanci třídy **FacebookClient** předáním hodnoty přístupového tokenu. Pro aktuálního ověřeného uživatele požádejte o hodnotu **ověřené** vlastnosti. Vlastnost **ověřený** označuje, zda Facebook ověřil účet jiným způsobem, například odeslání zprávy na mobilní telefon. Uloží tuto hodnotu do databáze.

[!code-csharp[Main](using-oauth-providers-with-mvc/samples/sample14.cs?highlight=7-18,25)]

Znovu budete muset buď odstranit záznamy v databázi pro uživatele, nebo použít jiný účet Facebook.

Spusťte aplikaci a zaregistrujte nového uživatele. Podívejte se na tabulku **ExtraUserInformation** , kde se zobrazí hodnota vlastnosti ověřený.

## <a name="conclusion"></a>Závěr

V tomto kurzu jste vytvořili lokalitu, která je integrovaná s Facebookem pro ověřování uživatelů a registrační data. Seznámili jste se s výchozím chováním nastaveným pro webovou aplikaci MVC 4 a postupem přizpůsobení tohoto výchozího chování.

## <a name="related-topics"></a>Související témata

- [Vytvořte aplikaci ASP.NET MVC s ověřováním a SQL DB a nasaďte ji do Azure App Service](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)

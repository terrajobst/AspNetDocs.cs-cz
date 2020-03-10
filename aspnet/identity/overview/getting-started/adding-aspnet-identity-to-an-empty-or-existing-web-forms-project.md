---
uid: identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
title: Přidání ASP.NET Identity do prázdného nebo existujícího projektu webových formulářů – ASP.NET 4. x
author: raquelsa
description: V tomto kurzu se dozvíte, jak přidat ASP.NET Identity (systém členství pro ASP.NET) do aplikace ASP.NET. Při vytváření nových webových formulářů nebo MVC...
ms.author: riande
ms.date: 01/22/2019
ms.assetid: 1cbc0ed2-5bd6-4b62-8d34-4c193dcd8b25
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project
msc.type: authoredcontent
ms.openlocfilehash: 8e82951d57f0b8052ee3f6530a7470be7d030206
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584124"
---
# <a name="adding-aspnet-identity-to-an-empty-or-existing-web-forms-project"></a>Přidání ASP.NET Identity do prázdného nebo stávajícího projektu webových formulářů

> V tomto kurzu se dozvíte, jak přidat [ASP.NET identity](introduction-to-aspnet-identity.md) (nový systém členství pro ASP.NET) do aplikace ASP.NET.
> 
> Když vytvoříte nové webové formuláře nebo projekt MVC v aplikaci Visual Studio 2017 RTM s jednotlivými účty, bude Visual Studio instalovat všechny požadované balíčky a přidat všechny potřebné třídy za vás. V tomto kurzu se zobrazí postup přidání podpory ASP.NET Identity do vašeho existujícího projektu webových formulářů nebo nového prázdného projektu. Vytvořím osnovu všechny balíčky NuGet, které potřebujete nainstalovat, a třídy, které potřebujete přidat. Přecházím vzorovým webovým formulářem při registraci nových uživatelů a při vypínání všech hlavních rozhraní API vstupních bodů pro správu uživatelů a ověřování. Tato ukázka bude používat výchozí implementaci ASP.NET Identity SQL Data Storage, která je založená na Entity Framework. V tomto kurzu použijeme LocalDB pro SQL Database.
> 

## <a name="get-started-with-aspnet-identity"></a>Začínáme s ASP.NET Identity

1. Začněte instalací a spuštěním sady [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/).
2. Na úvodní stránce vyberte **Nový projekt** , nebo můžete použít nabídku a vybrat **soubor**a pak **Nový projekt**.
3. V levém podokně rozbalte **vizuál C#** , pak vyberte **Web**a pak **ASP.NET webová aplikace (.NET Framework)** . Pojmenujte projekt "WebFormsIdentity" a vyberte **OK**.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image17.png)
4. V dialogovém okně **Nový projekt ASP.NET** vyberte **prázdnou** šablonu.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image2.png)  
  
   Všimněte si, že tlačítko **změnit ověřování** je zakázané a v této šabloně není dostupná žádná podpora ověřování. Webové formuláře, šablony MVC a webové rozhraní API umožňují vybrat přístup pro ověřování.

## <a name="add-identity-packages-to-your-app"></a>Přidání balíčků identit do aplikace

V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a vyberte možnost **Spravovat balíčky NuGet**. Vyhledejte a nainstalujte balíček **Microsoft. ASPNET. identity. EntityFramework** . 
  
![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image15.png)
  
Všimněte si, že tento balíček nainstaluje balíčky závislostí: **EntityFramework** a **Microsoft ASP.NET identity Core**.

## <a name="add-a-web-form-to-register-users"></a>Přidání webového formuláře pro registraci uživatelů

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat**a pak **webový formulář**.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image4.png)
2. V dialogovém okně **Zadejte název pro položku** pojmenujte nový **registr**webového formuláře a pak vyberte **OK** .
3. Nahraďte značku v generovaném souboru *Register. aspx* následujícím kódem. Změny kódu jsou zvýrazněny. 

    [!code-html[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample1.aspx?highlight=9,12-40)]

    > [!NOTE]
    > Toto je pouze zjednodušená verze souboru *Register. aspx* , která je vytvořena při vytváření nového projektu webových formulářů ASP.NET. Výše uvedený kód přidá pole formuláře a tlačítko pro registraci nového uživatele.
4. Otevřete soubor *Register.aspx.cs* a nahraďte obsah souboru následujícím kódem:

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample2.cs)]

    > [!NOTE] 
    > 
    > 1. Výše uvedený kód je zjednodušená verze souboru *Register.aspx.cs* , která je vytvořena při vytváření nového projektu webových formulářů ASP.NET.
    > 2. Třída *IdentityUser* je výchozí EntityFramework implementací rozhraní *IUser* . Rozhraní *IUser* je minimální rozhraní pro uživatele v ASP.NET identity Core.
    > 3. Třída *UserStore* je výchozí implementací EntityFramework úložiště uživatele. Tato třída implementuje minimální rozhraní ASP.NET Identity Core: *IUserStore*, *IUserLoginStore*, *IUserClaimStore* a *IUserRoleStore*.
    > 4. Třída *UserManager* zpřístupňuje rozhraní API související s uživatelem, které automaticky uloží změny do *UserStore*.
    > 5. Třída *IdentityResult* představuje výsledek operace identity.
5. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat**, **přidejte složku ASP.NET** a pak **\_data aplikace**.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image5.png)
6. Otevřete soubor *Web. config* a přidejte položku připojovacího řetězce pro databázi, kterou použijeme k uložení informací o uživateli. Databáze bude vytvořena za běhu EntityFramework pro entity identity. Připojovací řetězec je podobný jako ten, který jste vytvořili při vytváření nového projektu webových formulářů. Zvýrazněný kód ukazuje značky, které byste měli přidat:

    [!code-xml[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample3.xml?highlight=11-14)]
    
    > [!NOTE] 
    > V případě sady Visual Studio 2015 nebo vyšší nahraďte `(localdb)\v11.0` `(localdb)\MSSQLLocalDB` ve svém připojovacím řetězci.
    
7. V projektu klikněte pravým tlačítkem na soubor *Register. aspx* a vyberte **nastavit jako úvodní stránku**. Stisknutím kombinace kláves CTRL + F5 Sestavte a spusťte webovou aplikaci. Zadejte nové uživatelské jméno a heslo a pak vyberte **zaregistrovat**.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image6.png)  

    > [!NOTE]
    > ASP.NET Identity podporuje ověřování a v této ukázce můžete ověřit výchozí chování pro validátory uživatelů a hesel, které pocházejí z balíčku identity Core. Výchozí validátor pro uživatele (`UserValidator`) má vlastnost `AllowOnlyAlphanumericUserNames`, která má výchozí hodnotu nastavenou na `true`. Výchozí ověřovací modul pro heslo (`MinimumLengthValidator`) zajišťuje, že heslo má alespoň 6 znaků. Tyto validátory jsou vlastnosti na `UserManager`, které mohou být přepsány, pokud chcete mít vlastní ověření,

## <a name="verify-the-localdb-identity-database-and-tables-generated-by-entity-framework"></a>Ověření databáze identity LocalDb a tabulek generovaných Entity Framework

1. V nabídce **zobrazení** vyberte **Průzkumník serveru**.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image7.png)
2. Rozbalte položku **DefaultConnection (WebFormsIdentity)** , rozbalte položku **tabulky**, klikněte pravým tlačítkem myši na položku **AspNetUsers** a vyberte možnost **Zobrazit data tabulky**.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image8.png)  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image9.png)

## <a name="configure-the-application-for-owin-authentication"></a>Konfigurace aplikace pro ověřování OWIN

V tuto chvíli jsme přidali jenom podporu pro vytváření uživatelů. Teď vám ukážeme, jak můžeme přidat ověřování pro přihlášení uživatele. ASP.NET Identity používá middleware ověřování Microsoft OWIN pro ověřování pomocí formulářů. Ověřování souborem cookie OWIN je soubor cookie a mechanismus ověřování založený na deklaracích, který může být použit jakýmkoli rozhraním hostovaným v [Owin](https://msdn.microsoft.com/magazine/dn451439.aspx) nebo IIS. V tomto modelu je možné použít stejné ověřovací balíčky v rámci několika platforem, včetně ASP.NET MVC a webových formulářů. Další informace o Katana projektu a o tom, jak spustit middleware v hostiteli nezávislá, najdete v tématu [Začínáme s projektem Katana](https://msdn.microsoft.com/magazine/dn451439.aspx).

## <a name="install-authentication-packages-to-your-application"></a>Instalace ověřovacích balíčků do vaší aplikace

1. V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a vyberte možnost **Spravovat balíčky NuGet**. Vyhledejte a nainstalujte balíček ***Microsoft. ASPNET. identity. Owin*** . 
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image16.png)

2. Vyhledejte a nainstalujte balíček ***Microsoft. Owin. Host. SystemWeb*** .

    > [!NOTE]
    > Balíček **Microsoft. ASPNET. identity. Owin** obsahuje sadu rozšiřujících tříd OWIN pro správu a konfiguraci middlewaru pro ověřování Owin, které budou využívat ASP.NET identity základní balíčky.
    > Balíček **Microsoft. Owin. Host. SystemWeb** obsahuje server Owin, který umožňuje, aby se aplikace založené na Owin spouštěly ve službě IIS pomocí kanálu žádosti ASP.NET. Další informace najdete [v tématu Owin middleware v integrovaném kanálu služby IIS](../../../aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline.md).

## <a name="add-owin-startup-and-authentication-configuration-classes"></a>Přidat třídy konfigurace pro spuštění OWIN a ověřování

1. V **Průzkumník řešení**klikněte pravým tlačítkem na projekt, vyberte **Přidat**a pak **přidejte novou položku**. Do textového pole Hledat zadejte "*Owin*". Pojmenujte třídu "*Startup*" a vyberte **Přidat**. 
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image11.png)
2. V souboru Startup.cs přidejte zvýrazněný kód, který je zobrazen níže, a nakonfigurujte ověřování souborů cookie OWIN.

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample4.cs?highlight=1,3,15-19)]

    > [!NOTE]
    > Tato třída obsahuje atribut `OwinStartup` pro zadání spouštěcí třídy OWIN. Každá aplikace OWIN má spouštěcí třídu, kde zadáte komponenty pro kanál aplikace. Další informace o tomto modelu naleznete v tématu [Owin Startup Class Detection](../../../aspnet/overview/owin-and-katana/owin-startup-class-detection.md) .

## <a name="add-web-forms-for-registering-and-signing-in-users"></a>Přidat webové formuláře pro registraci a přihlašování uživatelů

1. Otevřete soubor *Register.aspx.cs* a přidejte následující kód, který se přihlásí uživateli, když se registrace podaří.

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample5.cs)]

    > [!NOTE] 
    > 
    > - Vzhledem k tomu, že ASP.NET Identity a ověřování souborů cookie OWIN jsou systémy založené na deklaracích, rozhraní vyžaduje, aby vývojář aplikace vygeneroval pro uživatele [hodnota ClaimsIdentity](https://msdn.microsoft.com/library/microsoft.identitymodel.claims.claimsidentity.aspx) . Hodnota ClaimsIdentity obsahuje informace o všech deklaracích pro uživatele, například o tom, k jakým rolím uživatel patří. V této fázi můžete také přidat další deklarace identity pro uživatele.
    > - Uživatele se můžete přihlásit pomocí Správce AuthenticationManager z OWIN a voláním `SignIn` a předáním v hodnota ClaimsIdentity, jak je uvedeno výše. Tento kód se přihlásí uživateli a vygeneruje také soubor cookie. Toto volání je analogické jako [FormAuthentication. SetAuthCookie](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) , které používá modul [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) .
2. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt, vyberte možnost **Přidat**a potom **webový formulář**. Pojmenujte **přihlašovací**jméno webového formuláře.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image12.png)
3. Obsah souboru *Login. aspx* nahraďte následujícím kódem:

    [!code-aspx[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample6.aspx)]
4. Obsah souboru *Login.aspx.cs* nahraďte následujícím:

    [!code-csharp[Main](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/samples/sample7.cs)]

    > [!NOTE] 
    > 
    > - `Page_Load` nyní kontroluje stav aktuálního uživatele a provede akci na základě jeho stavu `Context.User.Identity.IsAuthenticated`.
    >   **Zobrazit přihlášené uživatelské jméno** : rozhraní Microsoft ASP.NET identity Framework přidalo rozšiřující metody do [System. Security. Principal. IIdentity](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx) , které vám umožní získat `UserName` a `UserId` pro přihlášeného uživatele. Tyto metody rozšíření jsou definovány v sestavení `Microsoft.AspNet.Identity.Core`. Tyto metody rozšíření jsou náhradou pro [HttpContext.User.identity.Name](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx) .
    > - Metoda přihlašování: metoda `This` nahrazuje předchozí metodu `CreateUser_Click` v této ukázce a uživatel se po úspěšném vytvoření uživatele přihlásí.   
    >   Rozhraní Microsoft OWIN Framework přidalo do `System.Web.HttpContext` rozšiřující metody, které vám umožní získat odkaz na `IOwinContext`. Tyto metody rozšíření jsou definovány v `Microsoft.Owin.Host.SystemWeb` sestavení. Třída `OwinContext` zpřístupňuje vlastnost `IAuthenticationManager`, která představuje funkce middlewaru ověřování, která je k dispozici v aktuální žádosti. Uživatele se můžete přihlásit pomocí `AuthenticationManager` z OWIN a voláním `SignIn` a předáním do `ClaimsIdentity`, jak je uvedeno výše. Vzhledem k tomu, že ověřování souborů cookie ASP.NET Identity a OWIN jsou systémy založené na deklaracích, rozhraní vyžaduje, aby aplikace vygenerovala `ClaimsIdentity` pro uživatele. `ClaimsIdentity` obsahuje informace o všech deklaracích pro uživatele, například o tom, k jakým rolím uživatel patří. V této fázi můžete také přidat další deklarace identity pro uživatele, tento kód se přihlásí uživateli a vygeneruje také soubor cookie. Toto volání je analogické jako [FormAuthentication. SetAuthCookie](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) , které používá modul [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) .
    > - `SignOut` metoda: Získá odkaz na `AuthenticationManager` z OWIN a zavolá `SignOut`. To je obdobou metodě [FormsAuthentication. Signing](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx) , kterou používá modul [FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx) .
5. Stisknutím **kombinace kláves CTRL + F5** Sestavte a spusťte webovou aplikaci. Zadejte nové uživatelské jméno a heslo a pak vyberte **zaregistrovat**.
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image13.png)  
   Poznámka: v tomto okamžiku se vytvoří a přihlásí nový uživatel.
6. Vyberte tlačítko **Odhlásit** se. Budete přesměrováni do formuláře přihlášení.
7. Zadejte neplatné uživatelské jméno nebo heslo a klikněte na tlačítko **Přihlásit** se. 
   Metoda `UserManager.Find` vrátí hodnotu null a zobrazí se chybová zpráva: " *neplatné uživatelské jméno nebo heslo* ".
  
    ![](adding-aspnet-identity-to-an-empty-or-existing-web-forms-project/_static/image14.png)

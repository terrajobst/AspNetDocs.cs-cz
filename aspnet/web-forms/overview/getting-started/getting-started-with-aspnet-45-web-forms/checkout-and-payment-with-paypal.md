---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
title: Rezervace a platby pomocí služby PayPal | Microsoft Docs
author: Erikre
description: V této sérii kurzů se seznámíte se základy vytváření aplikací webových formulářů ASP.NET pomocí ASP.NET 4,5 a Microsoft Visual Studio Express 2013 pro My...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 664ec95e-b0c9-4f43-a39f-798d0f2a7e08
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/checkout-and-payment-with-paypal
msc.type: authoredcontent
ms.openlocfilehash: 62d00a86c6c5845fb894896df65002c7086d039f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78565406"
---
# <a name="checkout-and-payment-with-paypal"></a>Pokladna a platba přes PayPal

od [Erik Reitan](https://github.com/Erikre)

[Stáhnout vzorový projekt Wingtip Toys (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) nebo [Stáhnout elektronickou knihu (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> V této sérii kurzů se naučíte základy vytváření webových formulářů ASP.NET pomocí ASP.NET 4,5 a Microsoft Visual Studio Express 2013 pro web. K dispozici je Visual Studio 2013 [projekt se C# zdrojovým kódem](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) , který se doprovází v této sérii kurzů.

V tomto kurzu se dozvíte, jak upravit ukázkovou aplikaci Wingtip Toys, která zahrnuje autorizaci, registraci a platbu uživatelů pomocí služby PayPal. K nákupu produktů budou mít autorizaci jenom uživatelé, kteří jsou přihlášení. Integrovaná funkce registrace uživatele šablony projektu ASP.NET 4,5 již obsahuje mnoho toho, co potřebujete. Přidáte funkci pro rezervaci služby PayPal Express. V tomto kurzu používáte testovací prostředí pro vývojáře PayPal, takže se nepřesunou žádné skutečné prostředky. Na konci kurzu aplikaci otestujete tak, že vyberete produkty, které chcete přidat do nákupního košíku, kliknete na tlačítko rezervovat a přesunete data na web služby PayPal testování. Na webu služby PayPal testování si potvrdíte informace o expedici a platbách a pak se vrátíte do místní ukázkové aplikace Wingtip Toys, abyste mohli potvrdit a dokončit nákup.

Existuje několik zkušených platebních procesorů třetích stran, které se specializují na Online nákupy, které řeší škálovatelnost a zabezpečení. Vývojáři ASP.NET by měli zvážit výhody využívání řešení pro platby třetí strany před implementací řešení nákupu a nákupu.

> [!NOTE] 
> 
> Ukázková aplikace Wingtip Toys byla navržena tak, aby zobrazovala konkrétní koncepty a funkce ASP.NET, které jsou k dispozici pro webové vývojáře ASP.NET. Tato ukázková aplikace nebyla optimalizována pro všechny možné situace v souvislosti s škálovatelností a zabezpečením.

## <a name="what-youll-learn"></a>Naučíte se:

- Omezení přístupu ke konkrétním stránkám ve složce.
- Jak vytvořit známý nákupní košík z anonymního nákupního košíku
- Jak povolit protokol SSL pro projekt.
- Postup přidání poskytovatele OAuth do projektu.
- Jak používat PayPal k nákupu produktů pomocí testovacího prostředí služby PayPal.
- Jak zobrazit podrobnosti z PayPal v ovládacím prvku **DetailsView** .
- Postup aktualizace databáze aplikace Wingtip Toys s podrobnostmi získanými z PayPal.

## <a name="adding-order-tracking"></a>Přidání sledování objednávky

V tomto kurzu vytvoříte dvě nové třídy, abyste mohli sledovat data z objednávky, kterou uživatel vytvořil. Třídy budou sledovat data o dodávkách, celkovém nákupu a potvrzení platby.

### <a name="add-the-order-and-orderdetail-model-classes"></a>Přidání tříd modelu Order a OrderDetail

Dříve v této sérii kurzů jste definovali schéma pro kategorie, produkty a položky nákupních košíků tím, že ve složce *modely* vytvoříte `Category`, `Product`a třídy `CartItem`. Nyní přidáte dvě nové třídy pro definování schématu pro pořadí produktů a podrobnosti objednávky.

1. Ve složce **modely** přidejte novou třídu s názvem *Order.cs*.   
   V editoru se zobrazí nový soubor třídy.
2. Výchozí kód nahraďte následujícím kódem:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample1.cs)]
3. Do složky *modely* přidejte třídu *OrderDetail.cs* .
4. Nahraďte výchozí kód následujícím kódem:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample2.cs)]

Třídy `Order` a `OrderDetail` obsahují schéma pro definování informací o objednávce používané k nákupu a expedici.

Kromě toho budete muset aktualizovat třídu kontextu databáze, která spravuje třídy entit a který poskytuje přístup k datům databáze. K tomu přidáte nově vytvořenou objednávku a `OrderDetail` třídy modelu do `ProductContext` třídy.

1. V **Průzkumník řešení**vyhledejte a otevřete soubor *ProductContext.cs* .
2. Přidejte zvýrazněný kód do souboru *ProductContext.cs* , jak je znázorněno níže:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample3.cs?highlight=14-15)]

Jak bylo zmíněno dříve v této sérii kurzů, kód v souboru *ProductContext.cs* přidá obor názvů `System.Data.Entity`, abyste měli přístup ke všem základním funkcím Entity Framework. Tato funkce zahrnuje možnost dotazování, vkládání, aktualizaci a odstraňování dat pomocí objektů se silnými typy. Výše uvedený kód ve třídě `ProductContext` přidává Entity Framework přístup k nově přidaným třídám `Order` a `OrderDetail`.

## <a name="adding-checkout-access"></a>Přidávání přístupu k registraci

Ukázková aplikace Wingtip Toys umožňuje anonymním uživatelům kontrolovat a přidávat produkty do nákupního košíku. Pokud se však anonymní uživatelé rozhodnou koupit produkty přidané do nákupního košíku, musí se přihlásit k webu. Jakmile se přihlásí, budou mít přístup ke stránkám s omezeným přístupem webové aplikace, která bude zpracovávat proces registrace a nákupu. Tyto stránky s omezeným přístupem jsou obsaženy ve složce pro *rezervaci* aplikace.

### <a name="add-a-checkout-folder-and-pages"></a>Přidat složku a stránky rezervace

Nyní vytvoříte složku pro *rezervaci* a stránky, které bude zákazník uvidí během procesu registrace. Tyto stránky budete aktualizovat později v tomto kurzu.

1. V **Průzkumník řešení** klikněte pravým tlačítkem myši na název projektu (**Wingtip Toys**) a vyberte **Přidat novou složku**. 

    ![Rezervace a platba pomocí služby PayPal – nová složka](checkout-and-payment-with-paypal/_static/image1.png)
2. Pojmenujte novou *složku.*
3. Klikněte pravým tlačítkem na složku *rezervace* a pak vyberte **Přidat**-&gt;**Nová položka**. 

    ![Rezervace a platby pomocí služby PayPal – nová položka](checkout-and-payment-with-paypal/_static/image2.png)
4. Zobrazí se dialogové okno **Přidat novou položku** .
5. Na levé straně vyberte skupinu **Visual C#**  -&gt; **Web** Templates. Pak v prostředním podokně vyberte **webový formulář se stránkou předloha**a pojmenujte ho *CheckoutStart. aspx*. 

    ![Registrace a platby pomocí PayPal – dialogové okno Přidat novou položku](checkout-and-payment-with-paypal/_static/image3.png)
6. Stejně jako dřív vyberte soubor *Web. Master* jako stránku předlohy.
7. Přidejte následující další stránky do složky *rezervací* pomocí výše uvedených kroků:   

    - CheckoutReview.aspx
    - CheckoutComplete.aspx
    - CheckoutCancel.aspx
    - CheckoutError.aspx

### <a name="add-a-webconfig-file"></a>Přidat soubor Web. config

Přidáním nového souboru *Web. config* do složky pro *rezervaci* budete moci omezit přístup ke všem stránkám obsaženým ve složce.

1. Klikněte pravým tlačítkem na složku *rezervace* a vyberte **Přidat** -&gt; **Nová položka**.  
   Zobrazí se dialogové okno **Přidat novou položku** .
2. Na levé straně vyberte skupinu **Visual C#**  -&gt; **Web** Templates. Pak v prostředním podokně vyberte **soubor webové konfigurace**, přijměte výchozí název souboru *Web. config*a pak vyberte **Přidat**.
3. Nahraďte existující obsah XML v souboru *Web. config* následujícím způsobem:  

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample4.xml)]
4. Uložte soubor *Web. config* .

Soubor *Web. config* určuje, že všem neznámým uživatelům webové aplikace musí být odepřen přístup ke stránkám obsaženým ve složce pro *rezervaci* . Pokud ale uživatel zaregistroval účet a je přihlášený, bude se jednat o známého uživatele a bude mít přístup ke stránkám ve složce pro *rezervaci* .

Je důležité si uvědomit, že konfigurace ASP.NET se řídí hierarchií, kde každý soubor *Web. config* aplikuje konfigurační nastavení do složky, ve které se nachází, a do všech podřízených adresářů pod ním.

<a id="SSLWebForms"></a>
## <a name="enable-ssl-for-the-project"></a>Povolit SSL pro projekt

 SSL (Secure Sockets Layer) (SSL) je protokol určený k tomu, aby webové servery a webové klienty komunikovaly bezpečněji pomocí šifrování. Pokud se SSL nepoužívá, data odesílaná mezi klientem a serverem se otevřou pro monitorování paketů kýmkoli, kdo s fyzickým přístupem k síti. Kromě toho několik běžných schémat ověřování není v případě obyčejného protokolu HTTP zabezpečené. Konkrétně základní ověřování a ověřování formulářů odesílají nezašifrované přihlašovací údaje. Aby bylo zajištěno zabezpečení, musí tato schémata ověřování používat protokol SSL. 

1. V **Průzkumník řešení**klikněte na projekt **WingtipToys** a stisknutím klávesy **F4** zobrazte okno **vlastnosti** .
2. Změňte **povolený protokol SSL** na `true`.
3. Zkopírujte **adresu URL SSL** , abyste ji mohli později použít.   
 Adresa URL protokolu SSL bude `https://localhost:44300/`, pokud jste dříve nevytvořili weby SSL (jak je vidět níže).   
    ![Vlastnosti projektu](checkout-and-payment-with-paypal/_static/image4.png)
4. V **Průzkumník řešení**klikněte pravým tlačítkem na projekt **WingtipToys** a klikněte na **vlastnosti**.
5. Na levé kartě klikněte na **Web**.
6. Změňte **adresu URL projektu** tak, aby používala **adresu URL SSL** , kterou jste předtím uložili.   
    ](checkout-and-payment-with-paypal/_static/image5.png) ![Project Web Properties
7. Uložte stránku stisknutím **kombinace kláves CTRL + S**.
8. Aplikaci spustíte stisknutím kombinace kláves **Ctrl+F5**. Visual Studio zobrazí možnost, která vám umožní vyhnout se upozornění SSL.
9. Kliknutím na **Ano** důvěřujete IIS Express certifikátu SSL a pokračujte.   
    podrobnosti certifikátu ![IIS Express SSL](checkout-and-payment-with-paypal/_static/image6.png)  
 Zobrazí se upozornění zabezpečení.
10. Kliknutím na **Ano** nainstalujte certifikát pro místního hostitele.   
    Dialogové okno upozornění zabezpečení ![](checkout-and-payment-with-paypal/_static/image7.png)  
 Zobrazí se okno prohlížeče.

Webovou aplikaci teď můžete snadno testovat v místním prostředí pomocí protokolu SSL.

<a id="OAuthWebForms"></a>
## <a name="add-an-oauth-20-provider"></a>Přidat poskytovatele OAuth 2,0

Webové formuláře ASP.NET poskytují rozšířené možnosti pro členství a ověřování. Mezi tato vylepšení patří OAuth. OAuth je otevřený protokol, který umožňuje zabezpečenou autorizaci v jednoduché a standardní metodě z webových, mobilních a desktopových aplikací. Šablona webových formulářů ASP.NET používá OAuth k vystavování služeb Facebook, Twitter, Google a Microsoft jako poskytovatele ověřování. I když tento kurz používá pouze Google jako poskytovatele ověřování, můžete kód snadno upravit, aby používal kteréhokoli poskytovatele. Postup implementace jiných zprostředkovatelů se podobá postupům, které se v tomto kurzu zobrazí.

Kromě ověřování bude kurz používat taky role k implementaci autorizace. Pouze uživatelé, které přidáte do role `canEdit`, budou moci měnit data (kontakty vytvořit, upravit nebo odstranit).

> [!NOTE] 
> 
> Aplikace pro Windows Live přijímají pro pracovní web pouze živou adresu URL, takže pro testování přihlašovacích údajů nemůžete použít adresu URL místního webu.

Následující postup vám umožní přidat poskytovatele ověřování Google.

1. Otevřete soubor *App\_Start\Startup.auth.cs* .
2. Odeberte znaky komentáře z metody `app.UseGoogleAuthentication()` tak, aby se metoda zobrazila takto: 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample5.cs)]
3. Přejděte do [konzoly pro vývojáře Google](https://console.developers.google.com/). Budete také muset přihlásit se pomocí e-mailového účtu pro vývojáře Google (gmail.com). Pokud nemáte účet Google, vyberte odkaz **vytvořit účet** .   
   V dalším kroku uvidíte **konzolu pro vývojáře Google**.   
    ![konzole pro vývojáře Google](checkout-and-payment-with-paypal/_static/image8.png)
4. Klikněte na tlačítko **vytvořit projekt** a zadejte název projektu a ID (můžete použít výchozí hodnoty). Pak klikněte na **zaškrtávací políčko smlouva** a tlačítko **vytvořit** .  

    ![Google – nový projekt](checkout-and-payment-with-paypal/_static/image9.png)

   Během několika sekund se vytvoří nový projekt a v prohlížeči se zobrazí stránka nové projekty.
5. Na levé kartě klikněte na **rozhraní api &amp; auth**a pak klikněte na **přihlašovací údaje**.
6. V části **OAuth**klikněte na **vytvořit nové ID klienta** .   
   Zobrazí se dialogové okno **vytvořit ID klienta** .   
    ![ID klienta pro Google-Create](checkout-and-payment-with-paypal/_static/image10.png)
7. V dialogovém okně **vytvořit ID klienta** ponechte výchozí **webovou aplikaci** pro typ aplikace.
8. Nastavte **autorizované zdroje JavaScriptu** na adresu URL SSL, kterou jste použili dříve v tomto kurzu (`https://localhost:44300/`, pokud jste nevytvořili jiné projekty SSL).   
   Tato adresa URL je zdrojem vaší aplikace. V této ukázce budete zadávat jenom adresu URL testu localhost. Můžete ale zadat více adres URL pro místní localhost a produkční prostředí.
9. Nastavte **autorizovaný identifikátor URI přesměrování** na následující: 

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample6.html)]

   Tato hodnota je identifikátor URI, který ASP.NET uživatele OAuth ke komunikaci se serverem Google OAuth. Zapamatujte si adresu URL SSL, kterou jste použili výše (`https://localhost:44300/`, pokud jste nevytvořili jiné projekty SSL).
10. Klikněte na tlačítko **vytvořit ID klienta** .
11. V nabídce vlevo v konzole pro vývojáře Google klikněte na položku nabídky **obrazovka pro vyjádření souhlasu** a pak nastavte svou e-mailovou adresu a název produktu. Po vyplnění formuláře klikněte na **Uložit**.
12. Klikněte na položku nabídky **rozhraní API** , přejděte dolů a klikněte na tlačítko **vypnout** vedle položky **Google + rozhraní API**.   
    Přijetím této možnosti povolíte rozhraní Google + API.
13. Také je nutné aktualizovat balíček NuGet **Microsoft. Owin** na verzi 3.0.0.   
    V nabídce **nástroje** vyberte **Správce balíčků NuGet** a pak vyberte **Spravovat balíčky NuGet pro řešení**.  
    V okně **Spravovat balíčky NuGet** vyhledejte a aktualizujte balíček **Microsoft. Owin** na verzi 3.0.0.
14. V aplikaci Visual Studio aktualizujte metodu `UseGoogleAuthentication` stránky *Startup.auth.cs* zkopírováním a vložením **ID klienta** a **tajného klíče klienta** do metody. Níže uvedené hodnoty **ID klienta** a **tajného klíče klienta** jsou ukázky a nebudou fungovat. 

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample7.cs?highlight=64-65)]
15. Stisknutím **kombinace kláves CTRL + F5** Sestavte a spusťte aplikaci. Klikněte na odkaz **Přihlásit** se.
16. V části **použít jinou službu pro přihlášení**klikněte na **Google**.  
    ![Přihlásit se](checkout-and-payment-with-paypal/_static/image11.png)
17. Pokud potřebujete zadat svoje přihlašovací údaje, budete přesměrováni na web Google, kam budete zadávat svoje přihlašovací údaje.  
    ![Google – přihlášení](checkout-and-payment-with-paypal/_static/image12.png)
18. Po zadání přihlašovacích údajů se zobrazí výzva k udělení oprávnění k této webové aplikaci, kterou jste právě vytvořili.  
    ![Výchozí účet služby projektu](checkout-and-payment-with-paypal/_static/image13.png)
19. Klikněte na **přijmout**. Nyní budete přesměrováni zpět na stránku **registrace** aplikace **WingtipToys** , kde můžete zaregistrovat svůj účet Google.  
    Registrace ![s vaším účtem Google](checkout-and-payment-with-paypal/_static/image14.png)
20. Máte možnost změnit název místní registrace e-mailu, který se používá pro váš účet Gmail, ale obecně chcete zachovat výchozí alias e-mailu (tj. ten, který jste použili pro ověřování). Klikněte na **Přihlásit** se, jak je uvedeno výše.

### <a name="modifying-login-functionality"></a>Úprava funkce přihlášení

Jak už jsme uvedli v této sérii kurzů, ve výchozím nastavení je většina funkcí registrace uživatelů zahrnutá v šabloně webových formulářů ASP.NET. Nyní upravíte výchozí *přihlašovací stránky. aspx* a *Register. aspx* , které budou volat metodu `MigrateCart`. Metoda `MigrateCart` přidruží nově přihlášeného uživatele k anonymnímu nákupnímu košíku. Když přidružíte uživatele a nákupní košík, ukázková aplikace Wingtip Toys bude moct zachovat nákupní košík uživatele mezi návštěvami.

1. V **Průzkumník řešení**vyhledejte a otevřete složku *account* .
2. Upravte stránku s kódem na pozadí s názvem *Login.aspx.cs* tak, aby zahrnovala kód zvýrazněný žlutě, aby se zobrazila takto:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample8.cs?highlight=41-43)]
3. Uložte soubor *Login.aspx.cs* .

Prozatím můžete ignorovat upozornění, že není k dispozici žádná definice pro metodu `MigrateCart`. Později v tomto kurzu ho budete moct přidat.

Soubor kódu na pozadí *Login.aspx.cs* podporuje metodu Login. Kontrolou stránky login. aspx uvidíte, že tato stránka obsahuje "přihlášení", které po kliknutí spustí obslužnou rutinu `LogIn` pro kód na pozadí.

Při volání metody `Login` v *Login.aspx.cs* se vytvoří nová instance nákupního košíku s názvem `usersShoppingCart`. ID nákupního košíku (GUID) je načteno a nastaveno na `cartId` proměnnou. Pak je volána metoda `MigrateCart`, která předá do této metody předání `cartId` a jména přihlášeného uživatele. Při migraci nákupního košíku se identifikátor GUID, který se používá k identifikaci anonymního nákupního košíku, nahradí uživatelským jménem.

Kromě změny *Login.aspx.cs* souboru s kódem na pozadí pro migraci nákupního košíku, když se uživatel přihlásí, musíte také upravit *soubor s kódem na pozadí Register.aspx.cs* , aby se migruje nákupní košík, když uživatel vytvoří nový účet a přihlásí se.

1. Ve složce *account (účet* ) otevřete soubor kódu na pozadí s názvem *Register.aspx.cs*.
2. Upravte soubor kódu na pozadí tak, že kód zahrnete žlutě, takže se zobrazí takto:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample9.cs?highlight=28-32)]
3. Uložte soubor *Register.aspx.cs* . Znovu ignorujte upozornění na metodu `MigrateCart`.

Všimněte si, že kód, který jste použili v obslužné rutině události `CreateUser_Click`, je velmi podobný kódu, který jste použili v metodě `LogIn`. Když uživatel zaregistruje nebo přihlásí k lokalitě, bude provedeno volání metody `MigrateCart`.

## <a name="migrating-the-shopping-cart"></a>Migruje se nákupní košík.

Teď, když máte aktualizovaný proces přihlášení a registrace, můžete přidat kód pro migraci nákupního košíku pomocí metody `MigrateCart`.

1. V **Průzkumník řešení**Najděte složku *Logic* a otevřete soubor třídy *ShoppingCartActions.cs* .
2. Přidejte kód zvýrazněný žlutě ke stávajícímu kódu v souboru *ShoppingCartActions.cs* , aby se kód v souboru *ShoppingCartActions.cs* zobrazil takto:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample10.cs?highlight=215-224)]

Metoda `MigrateCart` používá existující cartId k nalezení nákupního košíku uživatele. Dále kód projde všemi položkami nákupní košíku a nahradí vlastnost `CartId` (jak je určeno schématem `CartItem`) s přihlášeným uživatelským jménem.

### <a name="updating-the-database-connection"></a>Aktualizuje se připojení k databázi.

Pokud s tímto kurzem používáte **předem vytvořenou** ukázkovou aplikaci Wingtip Toys, musíte znovu vytvořit výchozí databázi členství. Změnou výchozího připojovacího řetězce se databáze členství vytvoří při příštím spuštění aplikace.

1. Otevřete soubor *Web. config* v kořenovém adresáři projektu.
2. Aktualizujte výchozí připojovací řetězec tak, aby se zobrazil následujícím způsobem:   

    [!code-xml[Main](checkout-and-payment-with-paypal/samples/sample11.xml)]

<a id="PayPalWebForms"></a>
## <a name="integrating-paypal"></a>Integrace služby PayPal

PayPal je webová platforma pro fakturaci, která přijímá platby na základě online obchodních obchodníků. V tomto kurzu se dozvíte, jak integrovat funkci expresního rezervace služby PayPal do vaší aplikace. Expresní registrace umožňuje zákazníkům používat PayPal pro platby za položky, které přidal do svého nákupního košíku.

### <a name="create-paypal-test-accounts"></a>Vytváření zkušebních účtů PayPal

Chcete-li použít testovací prostředí služby PayPal, je nutné vytvořit a ověřit testovací účet vývojář. K vytvoření účtu testu nákupčího a účtu testu prodávajícího budete používat účet test vývojáře. Pověření k testovacímu účtu pro vývojáře také umožní ukázkové aplikaci Wingtip Toys přístup k testovacímu prostředí služby PayPal.

1. V prohlížeči přejděte na web PayPal Developer Testing:   
    [https://developer.paypal.com](https://developer.paypal.com/)
2. Pokud nemáte účet vývojáře služby PayPal, vytvořte nový účet kliknutím na **zaregistrovat**a podle pokynů pro registraci. Pokud máte existující účet vývojáře služby PayPal, přihlaste se kliknutím na **Přihlásit se**. Později v tomto kurzu budete potřebovat vývojářský účet služby PayPal pro testování ukázkové aplikace Wingtip Toys.
3. Pokud jste se právě zaregistrovali do svého účtu vývojáře služby PayPal, možná budete muset účet pro vývojáře PayPal ověřit pomocí služby PayPal. Svůj účet můžete ověřit podle kroků, které služba PayPal poslala na váš e-mailový účet. Po ověření účtu vývojáře pro vývojáře služby PayPal se znovu přihlaste k webu PayPal Developer Testing.
4. Po přihlášení k webu pro vývojáře služby PayPal pomocí svého účtu vývojáře služby PayPal potřebujete vytvořit zkušební účet nákupčího pro účet PayPal, pokud ho ještě nemáte. Chcete-li vytvořit testovací účet nákupčího, klikněte na webu PayPal na kartu **aplikace** a pak klikněte na **účty izolovaného prostoru**.   
 Zobrazí se stránka **testovací účty izolovaného prostoru** .   

    > [!NOTE] 
    > 
    > Web pro vývojáře služby PayPal už poskytuje obchodní testovací účet.

    ![Rezervace a platby pomocí účtů služby PayPal – izolovaného prostoru (sandbox)](checkout-and-payment-with-paypal/_static/image15.png)
5. Na stránce testovací účty izolovaného prostoru klikněte na **vytvořit účet**.
6. Na stránce **vytvořit testovací účet** zvolte e-mailový účet nákupčího a heslo podle vašeho výběru.   

    > [!NOTE] 
    > 
    > Na konci tohoto kurzu budete potřebovat e-mailové adresy a heslo nákupčího k otestování ukázkové aplikace Wingtip Toys.

    ![Rezervace a platby pomocí účtů služby PayPal – izolovaného prostoru (sandbox)](checkout-and-payment-with-paypal/_static/image16.png)
7. Kliknutím na tlačítko **vytvořit účet** vytvořte testovací účet nákupčího.  
 Zobrazí se stránka **testovací účty izolovaného prostoru** . 

    ![Rezervace a platby pomocí účtů PayPal a PayPal](checkout-and-payment-with-paypal/_static/image17.png)
8. Na stránce **testovací účty izolovaného prostoru** klikněte na e-mailový účet pro **usnadnění** .  
    Zobrazí se možnosti **profilu** a **oznámení** .
9. Vyberte možnost **profil** a potom kliknutím na **přihlašovací údaje rozhraní API** Zobrazte přihlašovací údaje k rozhraní API pro testovací účet obchodníka.
10. Zkopírujte přihlašovací údaje rozhraní API testu do poznámkového bloku.

Abyste mohli volat rozhraní API z ukázkové aplikace Wingtip Toys do testovacího prostředí služby PayPal, budete potřebovat vaše zobrazená pověření rozhraní API pro klasický TEST (uživatelské jméno, heslo a podpis). Přihlašovací údaje budete přidávat v dalším kroku.

### <a name="add-paypal-class-and-api-credentials"></a>Přidání přihlašovacích údajů pro třídu PayPal a rozhraní API

Většinu kódu PayPal umístíte do jediné třídy. Tato třída obsahuje metody, které slouží ke komunikaci s PayPal. Do této třídy taky přidáte svoje přihlašovací údaje PayPal.

1. V ukázkové aplikaci Wingtip Toys v sadě Visual Studio klikněte pravým tlačítkem na složku **Logic** a pak vyberte **Přidat** -&gt; **Nová položka**.   
   Zobrazí se dialogové okno **Přidat novou položku** .
2. V **části C# vizuál** z **nainstalovaného** podokna na levé straně vyberte **kód**.
3. V prostředním podokně vyberte **Třída**. Pojmenujte tuto novou třídu **PayPalFunctions.cs**.
4. Klikněte na **Přidat**.  
   V editoru se zobrazí nový soubor třídy.
5. Nahraďte výchozí kód následujícím kódem:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample12.cs)]
6. Přidejte přihlašovací údaje k obchodnímu rozhraní API (uživatelské jméno, heslo a podpis), které jste si zobrazili v tomto kurzu, abyste mohli provádět volání funkcí do testovacího prostředí služby PayPal.  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample13.cs)]

> [!NOTE] 
> 
> V této ukázkové aplikaci jednoduše přidáte přihlašovací údaje do C# souboru (. cs). V implementovaném řešení byste však měli zvážit šifrování přihlašovacích údajů v konfiguračním souboru.

Třída NVPAPICaller obsahuje většinu funkcí služby PayPal. Kód ve třídě poskytuje metody potřebné k provedení testovacího nákupu z testovacího prostředí služby PayPal. K nákupu se používají následující tři funkce PayPal:

- `SetExpressCheckout` funkce
- `GetExpressCheckoutDetails` funkce
- `DoExpressCheckoutPayment` funkce

Metoda `ShortcutExpressCheckout` shromažďuje informace o nákupu testů a údaje o produktech z nákupního košíku a volá funkci služby PayPal `SetExpressCheckout`. Metoda `GetCheckoutDetails` potvrdí podrobnosti nákupu a před provedením nákupu testu zavolá funkci služby PayPal `GetExpressCheckoutDetails`. Metoda `DoCheckoutPayment` dokončí nákup testu z testovacího prostředí zavoláním funkce `DoExpressCheckoutPayment` PayPal. Zbývající kód podporuje metody a procesy PayPal, jako je například kódování řetězců, dekódování řetězců, zpracování polí a určení přihlašovacích údajů.

> [!NOTE] 
> 
> PayPal vám umožní zahrnout volitelné údaje o nákupu na základě [specifikace rozhraní API služby PayPal](https://cms.paypal.com/us/cgi-bin/?cmd=_render-content&amp;content_ID=developer/e_howto_api_nvp_r_SetExpressCheckout). Rozšířením kódu v ukázkové aplikaci Wingtip Toys můžete zahrnout podrobnosti lokalizace, popisy produktů, daň, číslo zákaznické služby a také mnoho dalších volitelných polí.

Všimněte si, že návratové a zrušené adresy URL, které jsou zadány v metodě **ShortcutExpressCheckout** , používají číslo portu.

[!code-html[Main](checkout-and-payment-with-paypal/samples/sample14.html)]

Když Visual Web Developer spustí webový projekt pomocí protokolu SSL, pro webový server se běžně používá port 44300. Jak je uvedeno výše, číslo portu je 44300. Při spuštění aplikace se zobrazí jiné číslo portu. Číslo portu musí být správně nastaveno v kódu, aby bylo možné na konci tohoto kurzu úspěšně spustit ukázkovou aplikaci Wingtip Toys. V další části tohoto kurzu se dozvíte, jak načíst číslo portu místního hostitele a aktualizovat třídu PayPal.

### <a name="update-the-localhost-port-number-in-the-paypal-class"></a>Aktualizace čísla portu LocalHost ve třídě PayPal

Ukázková aplikace Wingtip Toys si koupí produkty tak, že přejde na testovací web PayPal a vrátí se do místní instance ukázkové aplikace Wingtip Toys. Aby se službě PayPal vrátila správná adresa URL, musíte v kódu PayPal uvedeného výše zadat číslo portu pro místně běžící ukázkovou aplikaci.

1. V **Průzkumník řešení** klikněte pravým tlačítkem na název projektu (**WingtipToys**) a vyberte **vlastnosti**.
2. V levém sloupci vyberte kartu **Web** .
3. Načte číslo portu z pole **Adresa URL projektu** .
4. V případě potřeby aktualizujte `returnURL` a `cancelURL` ve třídě PayPal (`NVPAPICaller`) v souboru *PayPalFunctions.cs* , aby používala číslo portu vaší webové aplikace:   

    [!code-html[Main](checkout-and-payment-with-paypal/samples/sample15.html?highlight=1-2)]

Nově přidaný kód bude odpovídat očekávanému portu vaší místní webové aplikace. PayPal se bude moct vrátit na správnou adresu URL na vašem místním počítači.

### <a name="add-the-paypal-checkout-button"></a>Přidat tlačítko pro rezervaci služby PayPal

Teď, když se do ukázkové aplikace přidaly primární funkce PayPal, můžete začít přidávat značky a kód potřebný k volání těchto funkcí. Nejdřív je nutné přidat tlačítko pro rezervaci, které uživatel uvidí na stránce nákupní košík.

1. Otevřete soubor *ShoppingCart. aspx* .
2. Posuňte se do dolní části souboru a najděte `<!--Checkout Placeholder -->` komentář.
3. Nahraďte komentář ovládacím prvkem `ImageButton`, aby se značka nahradila následujícím způsobem:  

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample16.aspx)]
4. V souboru *ShoppingCart.aspx.cs* přidejte po `UpdateBtn_Click` obslužné rutiny události poblíž konce souboru obslužnou rutinu `CheckOutBtn_Click` události:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample17.cs)]
5. V souboru *ShoppingCart.aspx.cs* přidejte odkaz na `CheckoutBtn`, aby bylo na tlačítko Nový obrázek odkazováno následujícím způsobem:  

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample18.cs?highlight=18)]
6. Uložte změny do souboru *ShoppingCart. aspx* i do souboru *ShoppingCart.aspx.cs* .
7. V nabídce vyberte možnost **ladění**-&gt;**WingtipToys sestavení**.  
   Projekt bude znovu vytvořen s nově přidaným ovládacím prvkem **obrázkové** .

### <a name="send-purchase-details-to-paypal"></a>Odeslat podrobnosti o nákupu do služby PayPal

Když uživatel klikne na tlačítko **Rezervovat** na stránce nákupního košíku (*ShoppingCart. aspx*), zahájí proces nákupu. Následující kód volá první funkci PayPal potřebnou k nákupu produktů.

1. Ve složce pro *rezervaci* otevřete soubor kódu na pozadí s názvem *CheckoutStart.aspx.cs*.   
   Nezapomeňte otevřít soubor kódu na pozadí.
2. Existující kód nahraďte následujícím kódem:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample19.cs)]

Když uživatel aplikace klikne na tlačítko **Rezervovat** na stránce nákupní košík, prohlížeč přejde na stránku *CheckoutStart. aspx* . Při načtení stránky *CheckoutStart. aspx* se zavolá metoda `ShortcutExpressCheckout`. V tomto okamžiku se uživatel přenese na web PayPal testování. Na webu PayPal uživatel zadá svoje přihlašovací údaje k účtu PayPal, zkontroluje podrobnosti o nákupu, přijme smlouvu PayPal a vrátí se do ukázkové aplikace Wingtip Toys, kde se `ShortcutExpressCheckout` metoda dokončí. Po dokončení metody `ShortcutExpressCheckout` se uživatel přesměruje na stránku *CheckoutReview. aspx* zadanou v metodě `ShortcutExpressCheckout`. Uživatel tak může zkontrolovat podrobnosti objednávky v rámci ukázkové aplikace Wingtip Toys.

### <a name="review-order-details"></a>Podrobnosti o revizi objednávky

Po návratu ze služby PayPal se na stránce *CheckoutReview. aspx* ukázkové aplikace Wingtip Toys zobrazí podrobnosti objednávky. Tato stránka umožňuje uživateli před nákupem produktů zkontrolovat podrobnosti o objednávce. Stránka *CheckoutReview. aspx* se musí vytvořit takto:

1. Ve složce pro *rezervaci* otevřete stránku s názvem *CheckoutReview. aspx*.
2. Existující značku nahraďte následujícím kódem:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample20.aspx)]
3. Otevřete stránku s kódem na pozadí s názvem *CheckoutReview.aspx.cs* a nahraďte existující kód následujícím kódem:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample21.cs)]

Ovládací prvek **DetailsView** slouží k zobrazení podrobností objednávky, které byly vráceny ze služby PayPal. Výše uvedený kód také uloží podrobnosti objednávky do databáze Wingtip Toys jako objekt `OrderDetail`. Když uživatel klikne na tlačítko pro **dokončení objednávky** , budou přesměrováni na stránku *CheckoutComplete. aspx* .

> [!NOTE] 
> 
> **Tip**
> 
> V kódu stránky *CheckoutReview. aspx* si všimněte, že značka `<ItemStyle>` slouží ke změně stylu položek v ovládacím prvku **DetailsView** v dolní části stránky. Zobrazením stránky v **návrhovém zobrazení** (výběrem možnosti **Návrh** v levém dolním rohu sady Visual Studio) a následným výběrem ovládacího prvku **DetailsView** a vybráním **inteligentní značky** (ikona šipky v pravé horní části ovládacího prvku) uvidíte **úkoly DetailsView**.
> 
> ![Rezervace a platby pomocí polí pro úpravy PayPal](checkout-and-payment-with-paypal/_static/image18.png)
> 
> Když vyberete možnost **Upravit pole**, zobrazí se dialogové okno **pole** . V tomto dialogovém okně lze snadno ovládat vlastnosti vizuálu, například **ItemStyle**, ovládacího prvku **DetailsView** .
> 
> ![Dialogové okno rezervace a platby s poli PayPal – pole](checkout-and-payment-with-paypal/_static/image19.png)

### <a name="complete-purchase"></a>Dokončit nákup

Stránka *CheckoutComplete. aspx* slouží k nákupu z PayPal. Jak je uvedeno výše, uživatel musí kliknout na tlačítko **Dokončit objednávku** , aby se aplikace mohla přejít na stránku *CheckoutComplete. aspx* .

1. Ve složce pro *rezervaci* otevřete stránku s názvem *CheckoutComplete. aspx*.
2. Existující značku nahraďte následujícím kódem:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample22.aspx)]
3. Otevřete stránku s kódem na pozadí s názvem *CheckoutComplete.aspx.cs* a nahraďte existující kód následujícím kódem:   

    [!code-csharp[Main](checkout-and-payment-with-paypal/samples/sample23.cs)]

Když je načtena stránka *CheckoutComplete. aspx* , je volána metoda `DoCheckoutPayment`. Jak bylo zmíněno dříve, metoda `DoCheckoutPayment` dokončuje nákup z testovacího prostředí služby PayPal. Jakmile si PayPal dokončí nákup objednávky, na stránce *CheckoutComplete. aspx* se zobrazí platební transakce `ID` k nákupu.

### <a name="handle-cancel-purchase"></a>Zrušit nákup s popisovačem

Pokud se uživatel rozhodne zrušit nákup, budou přesměrováni na stránku *CheckoutCancel. aspx* , kde uvidí, že jejich objednávka byla zrušena.

1. Ve složce pro *rezervaci* otevřete stránku s názvem *CheckoutCancel. aspx* .
2. Existující značku nahraďte následujícím kódem:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample24.aspx)]

### <a name="handle-purchase-errors"></a>Zpracovat chyby nákupu

Chyby během procesu nákupu budou zpracovány stránkou *CheckoutError. aspx* . Kód na pozadí stránky *CheckoutStart. aspx* , stránka *CheckoutReview. aspx* a stránka *CheckoutComplete. aspx* budou přesměrovány na stránku *CheckoutError. aspx* , pokud dojde k chybě.

1. Ve složce pro *rezervaci* otevřete stránku s názvem *CheckoutError. aspx* .
2. Existující značku nahraďte následujícím kódem:   

    [!code-aspx[Main](checkout-and-payment-with-paypal/samples/sample25.aspx)]

Pokud během procesu registrace dojde k chybě, zobrazí se stránka *CheckoutError. aspx* s podrobnostmi o chybě.

## <a name="running-the-application"></a>Spuštění aplikace

Spusťte aplikaci a podívejte se, jak zakoupit produkty. Všimněte si, že budete používat prostředí pro testování služby PayPal. Neprobíhá výměna skutečných peněz.

1. Zajistěte, aby byly všechny vaše soubory uloženy v aplikaci Visual Studio.
2. Otevřete webový prohlížeč a přejděte na [https://developer.paypal.com](https://developer.paypal.com/).
3. Přihlaste se pomocí svého účtu vývojáře služby PayPal, který jste vytvořili dříve v tomto kurzu.  
   Pro izolovaný prostor (sandbox) pro vývojáře služby PayPal musíte být přihlášeni [https://developer.paypal.com](https://developer.paypal.com/) k otestování expresní rezervace. To platí jenom pro testování izolovaného prostoru (sandbox) služby PayPal, nikoli na živé prostředí PayPal.
4. V aplikaci Visual Studio stiskněte klávesu **F5** a spusťte ukázkovou aplikaci Wingtip Toys.  
   Po opětovném sestavení databáze se v prohlížeči otevře a zobrazí stránka *Default. aspx* .
5. Přidejte do nákupního košíku tři různé produkty, a to tak, že vyberete kategorii produktů, například "auta", a potom kliknete na **Přidat do košíku** vedle každého produktu.  
   V nákupním košíku se zobrazí vybraný produkt.
6. Klikněte na tlačítko **PayPal** a proveďte rezervaci. 

    ![Registrace a platba pomocí služby PayPal-košík](checkout-and-payment-with-paypal/_static/image20.png)

   Rezervace bude vyžadovat, abyste měli uživatelský účet pro ukázkovou aplikaci Wingtip Toys.
7. Kliknutím na odkaz **Google** na pravé straně stránky se přihlaste pomocí stávajícího e-mailového účtu Gmail.com.  
   Pokud nemáte účet gmail.com, můžete ho vytvořit pro účely testování na [www.gmail.com](https://www.gmail.com/). Můžete také použít standardní místní účet kliknutím na registrovat. 

    ![Rezervace a platby pomocí služby PayPal – přihlášení](checkout-and-payment-with-paypal/_static/image21.png)
8. Přihlaste se pomocí účtu a hesla gmail. 

    ![Rezervace a platby pomocí služby PayPal – přihlášení ke službě Gmail](checkout-and-payment-with-paypal/_static/image22.png)
9. Kliknutím na tlačítko **Přihlásit** zaregistrujete účet Gmail pomocí uživatelského jména ukázkové aplikace Wingtip Toys. 

    ![Rezervace a platby pomocí služby PayPal – registrace účtu](checkout-and-payment-with-paypal/_static/image23.png)
10. Na testovacím webu PayPal přidejte e-mailovou adresu a heslo **nákupčího** , které jste vytvořili dříve v tomto kurzu, a pak klikněte na tlačítko **Přihlásit** se. 

    ![Registrace a platba pomocí PayPal – přihlášení k PayPal](checkout-and-payment-with-paypal/_static/image24.png)
11. Přijměte zásady PayPal a klikněte na tlačítko **Souhlasím a pokračovat** .  
    Všimněte si, že se tato stránka zobrazuje jenom při prvním použití tohoto účtu PayPal. Znovu si všimněte, že se jedná o testovací účet, nevyměňují se skutečné peníze. 

    ![Rezervace a platby pomocí zásad PayPal pro PayPal](checkout-and-payment-with-paypal/_static/image25.png)
12. Zkontrolujte informace o objednávce na stránce Kontrola testovacího prostředí služby PayPal a klikněte na **pokračovat**. 

    ![Rezervace a platby pomocí služby PayPal – informace o kontrole](checkout-and-payment-with-paypal/_static/image26.png)
13. Na stránce *CheckoutReview. aspx* Ověřte množství objednávky a zobrazte vygenerovanou dodací adresu. Pak klikněte na tlačítko **Dokončit objednávku** . 

    ![Rezervace a platba pomocí služby PayPal – přezkoumání objednávek](checkout-and-payment-with-paypal/_static/image27.png)
14. Zobrazí se stránka **CheckoutComplete. aspx** s ID platební transakce. 

    ![Rezervace a platba pomocí služby PayPal – dokončení rezervace](checkout-and-payment-with-paypal/_static/image28.png)

<a id="ReviewDBWebForms"></a>
## <a name="reviewing-the-database"></a>Kontrola databáze

Kontrolou aktualizovaných dat v databázi ukázkové aplikace Wingtip Toys po spuštění aplikace uvidíte, že aplikace úspěšně zaznamenala nákup produktů.

Data obsažená v souboru databáze *wingtiptoys. mdf* můžete zkontrolovat pomocí okna **průzkumník databáze** (**Průzkumník serveru** okno v sadě Visual Studio) stejně jako dříve v této sérii kurzů.

1. Zavřete okno prohlížeče, pokud je stále otevřené.
2. V aplikaci Visual Studio vyberte ikonu **Zobrazit všechny soubory** v horní části **Průzkumník řešení** , abyste mohli rozšířit složku **\_dat aplikace** .
3. Rozbalte složku **Data\_aplikace** .  
 Možná budete muset pro složku vybrat ikonu **Zobrazit všechny soubory** .
4. Klikněte pravým tlačítkem myši na soubor databáze *wingtiptoys. mdf* a vyberte **otevřít**.  
    Zobrazí se **Průzkumník serveru** .
5. Rozbalte složku **tabulky** .
6. Klikněte pravým tlačítkem myši na tabulku **Orders**a vyberte možnost **Zobrazit data tabulky**.  
 Zobrazí se tabulka **objednávky** .
7. Zkontrolujte sloupec **PaymentTransactionID** a potvrďte úspěšné transakce. 

    ![Rezervace a platba pomocí databáze služby PayPal-Revize](checkout-and-payment-with-paypal/_static/image29.png)
8. Zavřete okno tabulky **Orders** .
9. V Průzkumník serveru klikněte pravým tlačítkem myši na tabulku **OrderDetails** a vyberte možnost **Zobrazit data tabulky**.
10. Zkontrolujte hodnoty `OrderId` a `Username` v tabulce **OrderDetails** . Všimněte si, že tyto hodnoty odpovídají `OrderId` a `Username` hodnoty zahrnuté v tabulce **Orders** .
11. Zavřete okno tabulky **OrderDetails** .
12. Pravým tlačítkem myši klikněte na soubor databáze Wingtip Toys (*wingtiptoys. mdf*) a vyberte **Zavřít připojení**.
13. Pokud se okno **Průzkumník řešení** nezobrazí, klikněte v dolní části okna **Průzkumník serveru** na **Průzkumník řešení** a znovu zobrazte **Průzkumník řešení** .

## <a name="summary"></a>Souhrn

V tomto kurzu jste přidali schémata podrobností o objednávkách a objednávkách pro sledování nákupu produktů. Do ukázkové aplikace Wingtip Toys jste také integrovaných funkcí služby PayPal.

## <a name="additional-resources"></a>Další prostředky

[Přehled konfigurace ASP.NET](https://msdn.microsoft.com/library/ms178683(v=vs.100).aspx)  
[Nasazení zabezpečené aplikace webových formulářů ASP.NET pomocí členství, protokolu OAuth a SQL Database pro Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure – bezplatná zkušební verze](https://azure.microsoft.com/pricing/free-trial/)

## <a name="disclaimer"></a>Právní omezení

Tento kurz obsahuje vzorový kód. Vzorový kód je poskytován tak, jak je, bez záruky jakéhokoli druhu. Proto společnost Microsoft nezaručuje přesnost, integritu ani kvalitu ukázkového kódu. Souhlasíte s tím, že použijete vzorový kód na vlastní riziko. Za žádných okolností vám společnost Microsoft nenese žádný vzorový kód, obsah, včetně, ale nikoli omezení, případné chyby nebo opomenutí v jakémkoli vzorovém kódu, obsahu nebo jakékoli ztrátě nebo poškození jakéhokoli druhu, které vznikly v důsledku použití libovolného ukázkového kódu. Souhlasíte s tím, že neškodí škodu proti všem ztrátám, jejich škodám a škodám, škodám nebo škodám jakéhokoli druhu, včetně bez omezení, u kterých vzniklých nebo plynoucích z materiálu, který zveřejníte. přenášet, používat nebo spoléhat na zahrnutí, ale ne omezení na, zobrazení vyjádřená v nich.

> [!div class="step-by-step"]
> [Předchozí](shopping-cart.md)
> [Další](membership-and-administration.md)

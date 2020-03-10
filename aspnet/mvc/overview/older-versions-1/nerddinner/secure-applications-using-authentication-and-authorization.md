---
uid: mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
title: Zabezpečení aplikací pomocí ověřování a autorizace | Microsoft Docs
author: microsoft
description: Krok 9 ukazuje, jak přidat ověřování a autorizaci k zabezpečení naší aplikace NerdDinner, aby se uživatelé museli zaregistrovat a přihlásit k lokalitě, která se má vytvořit...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 9e4d5cac-b071-440c-b044-20b6d0c964fb
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/secure-applications-using-authentication-and-authorization
msc.type: authoredcontent
ms.openlocfilehash: 8d509c5f15bb4d5014e53b8dc2a736454238e72c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600980"
---
# <a name="secure-applications-using-authentication-and-authorization"></a>Zabezpečení aplikací ověřováním a autorizací

od [Microsoftu](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 9 bezplatného [kurzu aplikace "NerdDinner"](introducing-the-nerddinner-tutorial.md) , který vás provede procesem vytvoření malé, ale dokončené webové aplikace pomocí ASP.NET MVC 1.
> 
> V kroku 9 se dozvíte, jak přidat ověřování a autorizaci k zabezpečení naší aplikace NerdDinner, aby se uživatelé museli zaregistrovat a přihlašovat k webu a vytvořit novou večeři a aby ho později mohl upravovat jenom uživatel, který hostuje večeři.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme vám postupovat podle [Začínáme s kurzy pro](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [hudební úložiště](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) MVC 3 nebo MVC.

## <a name="nerddinner-step-9-authentication-and-authorization"></a>NerdDinner krok 9: ověřování a autorizace

Teď naše aplikace NerdDinner uděluje komukoli návštěvě webu možnost vytvářet a upravovat podrobnosti o večeři. Pojďme to změnit, aby se uživatelé museli zaregistrovat a přihlásit k webu a vytvořit novou večeři a přidat omezení tak, aby ho mohli později upravovat jenom uživatel, který hostuje večeři.

Pokud to chcete povolit, použijeme k zabezpečení naší aplikace ověřování a autorizaci.

### <a name="understanding-authentication-and-authorization"></a>Principy ověřování a autorizace

*Ověřování* je proces identifikace a ověření identity klienta, který přistupuje k aplikaci. Přesněji řečeno, jedná se o identifikaci "kdo", který je koncovým uživatelem při návštěvě webu. ASP.NET podporuje více způsobů ověřování uživatelů prohlížeče. Pro internetové webové aplikace se nejčastěji používaný přístup pro ověřování nazývá "ověřování pomocí formulářů". Ověřování pomocí formulářů umožňuje vývojářům vytvořit formulář pro přihlášení ve formátu HTML v rámci své aplikace a ověřit uživatelské jméno a heslo, které koncoví uživatelé odesílají do databáze nebo jiného úložiště přihlašovacích údajů k heslu. Pokud je kombinace uživatelského jména a hesla správná, může vývojář požádat ASP.NET o vydání šifrovaného souboru cookie protokolu HTTP, aby identifikoval uživatele v rámci budoucích požadavků. Pomocí ověřování pomocí formulářů v naší aplikaci NerdDinner.

*Autorizace* je proces určení, jestli ověřený uživatel má oprávnění pro přístup k určité adrese URL nebo prostředku nebo k provedení nějaké akce. V rámci naší aplikace NerdDinner si například přejete, aby k adrese URL */Dinners/Create* mohli získat přístup pouze uživatelé, kteří jsou přihlášeni, a vytvořit novou večeři. Také budete chtít přidat logiku autorizace tak, aby ji mohl upravovat jenom uživatel, který je hostitelem večeře – a odepřít přístup pro úpravy všem ostatním uživatelům.

### <a name="forms-authentication-and-the-accountcontroller"></a>Ověřování formulářů a AccountController

Výchozí šablona projektu sady Visual Studio pro ASP.NET MVC automaticky povoluje ověřování prostřednictvím formulářů při vytváření nových aplikací ASP.NET MVC. Také automaticky přidá předem vestavěnou implementaci přihlašovací stránky účtu do projektu – což usnadňuje integraci zabezpečení v rámci lokality.

Výchozí lokalita. Hlavní stránka předlohy zobrazí odkaz Přihlásit se v pravém horním rohu webu, když uživatel přistupující k němu není ověřený:

![](secure-applications-using-authentication-and-authorization/_static/image1.png)

Kliknutím na odkaz přihlásit převezme uživatel adresu URL */account/LogOn* :

![](secure-applications-using-authentication-and-authorization/_static/image2.png)

Návštěvníkům, kteří se nezaregistrovali, můžete tak učinit kliknutím na odkaz zaregistrovat, který převezme adresu URL */account/Register* a umožní jim zadat podrobnosti účtu:

![](secure-applications-using-authentication-and-authorization/_static/image3.png)

Kliknutím na tlačítko zaregistrovat vytvoříte nového uživatele v rámci systému členství v ASP.NET a ověříte uživatele na webu pomocí ověřování pomocí formulářů.

Když je uživatel přihlášený, lokalita. Master změní pravou stranu stránky na výstup "Vítejte [UserName]!". zpráva a vykreslí odkaz odhlásit se místo jednoho přihlášení. Kliknutím na odkaz odhlásit se odhlásí uživatel:

![](secure-applications-using-authentication-and-authorization/_static/image4.png)

Výše uvedené funkce přihlášení, odhlášení a registrace jsou implementovány v rámci třídy AccountController, která byla přidána do našeho projektu při vytváření projektu v sadě Visual Studio. Uživatelské rozhraní pro AccountController je implementováno pomocí šablon zobrazení v adresáři \Views\Account:

![](secure-applications-using-authentication-and-authorization/_static/image5.png)

Třída AccountController používá systém ověřování pomocí formulářů ASP.NET k vydávání šifrovaných souborů cookie ověřování a rozhraní API pro členství v ASP.NET pro ukládání a ověřování uživatelských jmen a hesel. Rozhraní API pro členství v ASP.NET je rozšiřitelné a povoluje použití úložiště přihlašovacích údajů k heslům. ASP.NET se dodává s integrovanými implementacemi zprostředkovatele členství, které ukládají uživatelské jméno a hesla v rámci databáze SQL nebo v rámci služby Active Directory.

Můžeme nakonfigurovat, který poskytovatel členství má naše aplikace NerdDinner použít, otevřením souboru Web. config v kořenovém adresáři projektu a vyhledáním oddílu &lt;&gt; členství v něm. Výchozí soubor Web. config, který byl přidán při vytvoření projektu, zaregistruje poskytovatele členství SQL a nakonfiguruje ho pro použití připojovacího řetězce s názvem ApplicationServices k určení umístění databáze.

Výchozí připojovací řetězec "ApplicationServices" (který je uveden v části &lt;connectionStrings&gt; souboru Web. config) je nakonfigurován tak, aby používal SQL Express. Odkazuje na databázi SQL Express s názvem ASPNETDB. MDF v adresáři App\_data aplikace Pokud tato databáze neexistuje při prvním použití rozhraní API členství v rámci aplikace, ASP.NET automaticky vytvoří databázi a zřídí příslušné schéma databáze členství v této aplikaci:

![](secure-applications-using-authentication-and-authorization/_static/image6.png)

Pokud místo používání SQL Express chceme použít úplnou instanci SQL Server (nebo se připojit ke vzdálené databázi), stačí, když je potřeba aktualizovat připojovací řetězec "ApplicationServices" v souboru Web. config a ujistit se, že příslušné schéma členství bylo přidáno do databáze, na které odkazuje. Můžete spustit nástroj "ASPNET\_regsql. exe" v adresáři \Windows\Microsoft.NET\Framework\v2.0.50727\ a přidat tak příslušné schéma pro členství a další ASP.NET aplikační služby do databáze.

### <a name="authorizing-the-dinnerscreate-url-using-the-authorize-filter"></a>Autorizace adresy URL/Dinners/Create pomocí filtru [autorizovat]

Nemuseli jsme psát žádný kód, který umožní implementaci zabezpečeného ověřování a správy účtů pro aplikaci NerdDinner. Uživatelé mohou registrovat nové účty pomocí naší aplikace a přihlašovat nebo odhlásit Web.

Nyní můžeme do aplikace přidat logiku autorizace a použít stav ověřování a uživatelské jméno návštěvníků k řízení toho, co můžou a v rámci lokality dělat. Pojďme začít přidáním logiky autorizace do metod akce "vytvořit" naší třídy DinnersController. Konkrétně budeme vyžadovat, aby uživatelé, kteří přistupují k adrese URL */Dinners/Create* , museli být přihlášeni. Pokud nejsou přihlášeni, přesměrujte je na přihlašovací stránku, aby se mohli přihlásit.

Implementace této logiky je poměrně jednoduchá. Vše, co je potřeba udělat, je přidat atribut filtru [autorizovat] k našim způsobům akce vytvoření, jako je například:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample1.cs)]

ASP.NET MVC podporuje možnost vytvořit "filtry akcí", které lze použít k implementaci opakované použitelné logiky, která se dá deklarativně použít na metody akcí. Filtr [autorizovat] je jedním z vestavěných filtrů akcí, které poskytuje ASP.NET MVC, a umožňuje vývojářům deklarativní použití autorizačních pravidel na metody akcí a tříd kontroleru.

Při použití bez parametrů (například výše) filtr [autorizační] vynutil, aby uživatel provádějící požadavek na akci metody byl přihlášen – a automaticky přesměruje prohlížeč na adresu URL pro přihlášení, pokud nejsou. Při tomto přesměrování je původní požadovaná adresa URL předána jako argument typu QueryString (například:/Account/LogOn? ReturnUrl =% 2fDinners% 2fCreate). AccountController pak přesměruje uživatele zpět na původně požadovanou adresu URL po přihlášení.

Filtr [autorizovat] volitelně podporuje možnost zadat vlastnost "uživatelé" nebo "role", která se dá použít k vyžadování, aby byl uživatel přihlášený, a v rámci seznamu povolených uživatelů nebo členem povolené role zabezpečení. Například kód níže umožňuje přístup k adrese URL/Dinners/Create pouze dvěma konkrétním uživatelům "scottgu" a "billg":

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample2.cs)]

Vkládání specifických uživatelských jmen do kódu je v podstatě neudržovatelnější i když. Lepším řešením je definovat "role vyšší úrovně", které kód kontroluje, a pak mapovat uživatele do role pomocí databáze nebo systému služby Active Directory (Povolit externí uložení vlastního seznamu mapování uživatelů z kódu). ASP.NET zahrnuje integrované rozhraní API pro správu rolí i integrovanou sadu poskytovatelů rolí (včetně těch, které jsou pro SQL a Active Directory), které můžou pomáhat s tímto mapováním uživatelů nebo rolí. Kód můžeme potom aktualizovat tak, aby uživatelům v rámci určité role správce povolil přístup k adrese URL/Dinners/Create:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample3.cs)]

### <a name="using-the-useridentityname-property-when-creating-dinners"></a>Použití vlastnosti User.Identity.Name při vytváření večeři

Uživatelské jméno aktuálně přihlášeného uživatele žádosti můžeme načíst pomocí vlastnosti User.Identity.Name vystavené u základní třídy Controller.

Dříve, když jsme implementovali verzi HTTP-POST metody akce Create (), měli jsme pevně zakódované vlastnost HostedBy pro večeři na statický řetězec. Tento kód teď můžeme aktualizovat, aby místo toho používal vlastnost User.Identity.Name, a také automaticky přidat protokol RSVP pro hostitele, který vytváří večeři:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample4.cs)]

Vzhledem k tomu, že jsme přidali atribut [autorizovat] do metody Create (), ASP.NET MVC zajistí, že se metoda Action spustí jenom v případě, že se uživateli, který navštíví adresu URL/Dinners/Create, přihlásí na webu. V takovém případě hodnota vlastnosti User.Identity.Name bude vždy obsahovat platné uživatelské jméno.

### <a name="using-the-useridentityname-property-when-editing-dinners"></a>Použití vlastnosti User.Identity.Name při úpravě večeři

Teď přidáme část autorizační logiky, která omezí uživatele tak, aby mohli upravovat jenom vlastnosti večeře, které sami sami hostují.

Abychom vám to usnadnili, Přidali jsme do objektu večeře (v rámci předchozí třídy Dinner.cs, kterou jsme vytvořili dříve) pomocnou metodu "IsHostedBy (uživatelské jméno)". Tato pomocná metoda vrátí hodnotu true nebo false v závislosti na tom, zda zadané uživatelské jméno odpovídá vlastnosti večeře HostedBy, a zapouzdřuje logiku nutnou k provedení porovnávání řetězců nerozlišujících velká a malá písmena:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample5.cs)]

Pak přidáte atribut [autorizovat] do metod akce Edit () v rámci naší třídy DinnersController. Tím se zajistí, že se uživatelé musí přihlásili, aby si vyžádali adresu URL */Dinners/Edit/[ID]* .

Pak můžeme do našich metod úprav, které používají pomocnou metodu večeře. IsHostedBy (Username), přidat kód, který ověří, jestli přihlášený uživatel odpovídá hostiteli večeře. Pokud uživatel není hostitel, zobrazí se zobrazení "InvalidOwner" a žádost se ukončí. Kód, který se má udělat, vypadá takto:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample6.cs)]

Potom můžete kliknout pravým tlačítkem na adresář \Views\Dinners a pomocí příkazu nabídky pro zobrazení pro přidání&gt;vytvořit nové zobrazení "InvalidOwner". Naplníme ji následující chybovou zprávou:

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample7.aspx)]

A teď když se uživatel pokusí upravit večeři, že nevlastní, zobrazí se chybová zpráva:

![](secure-applications-using-authentication-and-authorization/_static/image7.png)

Stejný postup můžete opakovat pro metody akce DELETE () v rámci našeho kontroleru, abyste mohli uzamknout oprávnění k odstranění večeři i k tomu, že ho může odstranit jenom hostitel večeře.

### <a name="showinghiding-edit-and-delete-links"></a>Zobrazení nebo skrytí odkazů pro úpravy a odstranění

Odkazujeme na metodu akce upravit a odstranit naší třídy DinnersController z naší adresy URL s podrobnostmi:

![](secure-applications-using-authentication-and-authorization/_static/image8.png)

V současné době zobrazujeme odkazy na akce upravit a odstranit bez ohledu na to, jestli je návštěvníkem této hostiny adresa URL s podrobnostmi. Pojďme to změnit, aby se odkazy zobrazovaly jenom v případě, že je uživatel, který je návštěvníkem, vlastníkem večeře.

Metoda Action () v rámci našeho DinnersController načte objekt večeře a pak ho předává jako objekt modelu do naší šablony zobrazení:

[!code-csharp[Main](secure-applications-using-authentication-and-authorization/samples/sample8.cs)]

Naši šablonu zobrazení můžeme aktualizovat tak, aby podmíněně zobrazovala nebo skryla odkazy pro úpravy a odstranění pomocí pomocné metody večeře. IsHostedBy (), jak je uvedeno níže:

[!code-aspx[Main](secure-applications-using-authentication-and-authorization/samples/sample9.aspx)]

#### <a name="next-steps"></a>Další kroky

Teď se podíváme na to, jak můžeme ověřeným uživatelům povolit protokol RSVP pro večeři pomocí AJAX.

> [!div class="step-by-step"]
> [Předchozí](implement-efficient-data-paging.md)
> [Další](use-ajax-to-deliver-dynamic-updates.md)

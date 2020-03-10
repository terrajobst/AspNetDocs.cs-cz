---
uid: web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-vb
title: Ověřování uživatelských přihlašovacích údajů proti uživatelskému úložišti členství (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu podíváme se, jak ověřit přihlašovací údaje uživatele proti úložišti uživatelů členství pomocí programových prostředků a přihlašovacího ovládacího prvku....
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 17772912-b47b-4557-9ce9-80f22df642f7
msc.legacyurl: /web-forms/overview/older-versions-security/membership/validating-user-credentials-against-the-membership-user-store-vb
msc.type: authoredcontent
ms.openlocfilehash: 37574e4cdc86f518d01d12da58cc2862bc77d463
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78527928"
---
# <a name="validating-user-credentials-against-the-membership-user-store-vb"></a>Ověření přihlašovacích údajů uživatele v úložišti uživatelů, kteří jsou členy (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_06_VB.zip) nebo [stažení PDF](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial06_LoggingIn_vb.pdf)

> V tomto kurzu podíváme se, jak ověřit přihlašovací údaje uživatele pro uživatelské úložiště členství pomocí programových prostředků a přihlašovacího ovládacího prvku. Také se podíváme na to, jak přizpůsobit vzhled a chování ovládacího prvku pro přihlášení.

## <a name="introduction"></a>Úvod

<a id="Tutorial05"> </a>V [předchozím kurzu](creating-user-accounts-vb.md) jsme se podívali na postup vytvoření nového uživatelského účtu v rámci sady členství. Nejdříve jsme prohlédli programově vytváření uživatelských účtů prostřednictvím metody `CreateUser` `Membership` třídy a pak prozkoumali pomocí webového ovládacího prvku ovládacím CreateUserWizard. Přihlašovací stránka teď ale ověřuje zadané přihlašovací údaje proti pevně zakódovanému seznamu párů uživatelských jmen a hesel. Musíme aktualizovat logiku přihlašovací stránky tak, aby ověřovala přihlašovací údaje pro uživatelské úložiště v rozhraní .NET Framework.

Podobně jako při vytváření uživatelských účtů lze přihlašovací údaje ověřit programově nebo deklarativně. Rozhraní API pro členství zahrnuje metodu pro programové ověření přihlašovacích údajů uživatele proti uživatelskému úložišti. A ASP.NET se dodává s přihlašovacím webovým ovládacím prvkem, který vykreslí uživatelské rozhraní s textovým polem pro uživatelské jméno a heslo a tlačítko pro přihlášení.

V tomto kurzu podíváme se, jak ověřit přihlašovací údaje uživatele pro uživatelské úložiště členství pomocí programových prostředků a přihlašovacího ovládacího prvku. Také se podíváme na to, jak přizpůsobit vzhled a chování ovládacího prvku pro přihlášení. Pojďme začít!

## <a name="step-1-validating-credentials-against-the-membership-user-store"></a>Krok 1: ověření přihlašovacích údajů proti uživatelskému úložišti členství

Pro weby, které používají ověřování pomocí formulářů, se uživatel přihlašuje k webu návštěvou přihlašovací stránky a zadáním jejich přihlašovacích údajů. Tyto přihlašovací údaje se pak porovnají s uživatelským úložištěm. Pokud jsou platné, pak se uživateli udělí lístek ověřování pomocí formulářů, což je token zabezpečení, který označuje identitu a pravost návštěvníka.

Chcete-li ověřit uživatele v rámci rozhraní členství, použijte [metodu`ValidateUser`](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx)třídy `Membership`. Metoda `ValidateUser` přebírá dva vstupní parametry – `username` a `password` a vrací logickou hodnotu označující, zda byla pověření platná. Podobně jako u `CreateUser` metoda, kterou jsme prozkoumali v předchozím kurzu, metoda `ValidateUser` deleguje skutečné ověření nakonfigurovanému zprostředkovateli členství.

`SqlMembershipProvider` ověří zadané přihlašovací údaje tím, že získá heslo zadaného uživatele prostřednictvím uložené procedury `aspnet_Membership_GetPasswordWithFormat`. Odvolat, že `SqlMembershipProvider` ukládá hesla uživatelů pomocí jednoho ze tří formátů: Clear, Encrypted nebo Hashed. Uložená procedura `aspnet_Membership_GetPasswordWithFormat` vrátí heslo v nezpracovaném formátu. Pro šifrovaná hesla nebo hesla s algoritmem hash `SqlMembershipProvider` transformuje hodnotu `password` předanou do `ValidateUser` metody do jejího ekvivalentního zašifrovaného nebo hashového stavu a pak ji porovná s tím, co bylo vráceno z databáze. Pokud heslo uložené v databázi odpovídá formátovanému heslu zadanému uživatelem, přihlašovací údaje jsou platné.

Pojďme aktualizovat přihlašovací stránku (~/`Login.aspx`) tak, aby ověřovala zadané přihlašovací údaje s uživatelským úložištěm pro členství v rozhraní. Tuto přihlašovací stránku jsme vytvořili zpátky v <a id="Tutorial02"> </a> [*přehledu kurzu ověřování pomocí formulářů*](../introduction/an-overview-of-forms-authentication-vb.md) , vytváření rozhraní se dvěma textboxy pro uživatelské jméno a heslo, zaškrtávací políčko pro zapamatování identity a přihlašovací tlačítko (viz obrázek 1). Kód ověří zadané přihlašovací údaje proti pevně zakódovanému seznamu párů uživatelského jména a hesla (Scott/Password, Jisun/Password a Sam/Password). <a id="Tutorial03"> </a>V kurzu [*Konfigurace ověřování formulářů a Pokročilá témata*](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md) jsme aktualizovali kód přihlašovací stránky pro ukládání dalších informací do vlastnosti `UserData` lístku pro ověřování formulářů.

[![rozhraní přihlašovací stránky obsahuje dvě textová pole, CheckBoxList a tlačítko.](validating-user-credentials-against-the-membership-user-store-vb/_static/image2.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image1.png)

**Obrázek 1**: rozhraní přihlašovací stránky obsahuje dvě textová pole, CheckBoxList a tlačítko ([kliknutím zobrazíte obrázek v plné velikosti).](validating-user-credentials-against-the-membership-user-store-vb/_static/image3.png)

Uživatelské rozhraní přihlašovací stránky může zůstat beze změny, ale je potřeba nahradit obslužnou rutinu události `Click`ho tlačítka přihlášení kódem, který ověřuje uživatele v úložišti uživatelů rozhraní .NET Framework. Aktualizujte obslužnou rutinu události tak, aby se její kód zobrazoval takto:

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample1.vb)]

Tento kód je výjimečně jednoduchý. Začneme voláním metody `Membership.ValidateUser` s předáním zadaného uživatelského jména a hesla. Pokud tato metoda vrátí hodnotu true, pak je uživatel přihlášen k webu prostřednictvím metody RedirectFromLoginPage třídy `FormsAuthentication`. (Jak jsme probrali <a id="Tutorial02"> </a>v kurzu [*Přehled ověřování formulářů*](../introduction/an-overview-of-forms-authentication-vb.md) , `FormsAuthentication.RedirectFromLoginPage` vytvoří lístek ověřování formuláře a pak přesměruje uživatele na příslušnou stránku.) Pokud jsou přihlašovací údaje neplatné, zobrazí se ale popisek `InvalidCredentialsMessage`, který informuje uživatele o tom, že jeho uživatelské jméno nebo heslo nebylo správné.

A je to!

Pokud chcete otestovat, jestli přihlašovací stránka funguje podle očekávání, zkuste se přihlásit pomocí jednoho z uživatelských účtů, které jste vytvořili v předchozím kurzu. Nebo, pokud jste ještě nevytvořili účet, pokračujte a vytvořte si ho ze stránky `~/Membership/CreatingUserAccounts.aspx`.

> [!NOTE]
> Když uživatel zadá své přihlašovací údaje a odešle formulář přihlašovací stránky, přihlašovací údaje, včetně jejího hesla, se přenáší přes Internet na webový server v *prostém textu*. To znamená, že uživatelské jméno a heslo může sledovat jakýkoli počítačový podvodník, který bude sledovat síťový provoz. Aby k tomu nedocházelo, je nezbytné šifrovat síťový provoz pomocí [protokolu SSL (Secure Socket Layer)](http://en.wikipedia.org/wiki/Secure_Sockets_Layer). Tím se zajistí, že přihlašovací údaje (stejně jako kód HTML celé stránky) budou šifrovány od okamžiku, kdy prohlížeč opustí, dokud je webový server neobdrží.

### <a name="how-the-membership-framework-handles-invalid-login-attempts"></a>Způsob, jakým rozhraní členství zpracovává neplatné pokusy o přihlášení

Když návštěvník dostane přihlašovací stránku a odešle své přihlašovací údaje, prohlížeč vytvoří požadavek HTTP na přihlašovací stránku. Pokud jsou přihlašovací údaje platné, odpověď protokolu HTTP zahrnuje ověřovací lístek do souboru cookie. Proto by počítačový podvodník pokoušející se o přemístění do vaší lokality mohl vytvořit program, který vyčerpá požadavky HTTP na přihlašovací stránku s platným uživatelským jménem a odhadem v hesle. Pokud je odhad hesla správný, přihlašovací stránka vrátí soubor cookie ověřovacího lístku, u kterého bude program vědět, že má stumbled na platný pár uživatelského jména a hesla. Díky útokům hrubou silou může být takový program Stumble na heslo uživatele, zejména v případě, že je heslo slabé.

Aby nedocházelo k takovým útokům hrubou silou, rozhraní pro členství zamkne uživatele, pokud v určitém časovém období dojde k určitému počtu neúspěšných pokusů o přihlášení. Přesné parametry lze konfigurovat prostřednictvím následujících dvou nastavení konfigurace zprostředkovatele členství:

- `maxInvalidPasswordAttempts` – určuje, kolik neplatných pokusů o zadání hesla pro uživatele v časovém období, než je účet uzamčen. Výchozí hodnota je 5.
- `passwordAttemptWindow` – určuje časové období v minutách, během kterého se zadaný počet neplatných pokusů o přihlášení může stát, že dojde k uzamknutí účtu. Výchozí hodnota je 10.

Pokud uživatel byl uzamčen, nemůže se přihlásit, dokud správce neodemkne svůj účet. Když je uživatel uzamčený, bude metoda `ValidateUser` *vždycky* vracet `False`, i když jsou dodány platné přihlašovací údaje. I když toto chování snižuje pravděpodobnost, že se hacker do vaší lokality přeruší prostřednictvím metod hrubou silou, může ukončit uzamykání platného uživatele, který jednoduše zapomene heslo, nebo neúmyslně má na začátku neplatný den zápisu.

Bohužel není k dispozici žádný integrovaný nástroj pro odemknutí uživatelského účtu. Chcete-li odemknout účet, můžete databázi změnit přímo, změnit pole `IsLockedOut` v tabulce `aspnet_Membership` pro příslušný uživatelský účet – nebo vytvořit webové rozhraní se seznamem uzamčených účtů s možnostmi jejich odemknutí. Podíváme se na vytváření rozhraní pro správu pro provádění běžných úloh souvisejících s uživatelským účtem a rolemi v budoucím kurzu.

> [!NOTE]
> Jedním z Nevýhodou metody `ValidateUser` je, že pokud jsou zadané přihlašovací údaje neplatné, neposkytuje žádné vysvětlení k tomu, proč. Přihlašovací údaje mohou být neplatné, protože v úložišti uživatele není žádné párování uživatelského jména a hesla, nebo protože uživatel nebyl dosud schválen, nebo protože byl uživatel uzamčen. V kroku 4 se dozvíte, jak zobrazit uživateli podrobnější zprávu, když se jejich pokus o přihlášení nezdaří.

## <a name="step-2-collecting-credentials-through-the-login-web-control"></a>Krok 2: shromažďování přihlašovacích údajů prostřednictvím přihlašovacího webového ovládacího prvku

[Přihlašovací webový ovládací prvek](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx) vykresluje výchozí uživatelské rozhraní velmi podobné jako ten, který jsme vytvořili zpátky v <a id="Tutorial02"> </a> [*přehledu kurzu ověřování pomocí formulářů*](../introduction/an-overview-of-forms-authentication-vb.md) . Použití přihlašovacího ovládacího prvku uloží nám práci s vytvořením rozhraní ke shromáždění přihlašovacích údajů návštěvníka. Kromě toho přihlašovací ovládací prvek automaticky přihlašuje uživatele (za předpokladu, že odeslaná pověření jsou platná), a tím šetříme, že je potřeba psát jakýkoliv kód.

Pojďme aktualizovat `Login.aspx`a nahradit ručně vytvořené rozhraní a kód ovládacím prvkem pro přihlášení. Začněte odebráním existujícího kódu a kódu v `Login.aspx`. Můžete ho odstranit hned nebo jednoduše komentovat. Chcete-li komentovat deklarativní označení, uzavřete ho pomocí `<%--` a oddělovače `--%>`. Tyto oddělovače můžete zadat ručně, nebo jak vidíte na obrázku 2, můžete vybrat text, který chcete komentovat, a pak na panelu nástrojů kliknout na ikonu odkomentovat vybrané řádky. Podobně můžete použít ikonu odkomentovat vybrané řádky a komentovat vybraný kód v třídě Code-na pozadí.

[![komentovat existující deklarativní značky a zdrojový kód v Login. aspx](validating-user-credentials-against-the-membership-user-store-vb/_static/image5.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image4.png)

**Obrázek 2**: Odkomentujte existující deklarativní značky a zdrojový kód v Login. aspx ([kliknutím zobrazíte obrázek v plné velikosti](validating-user-credentials-against-the-membership-user-store-vb/_static/image6.png)).

> [!NOTE]
> Při zobrazení deklarativních značek v aplikaci Visual Studio 2005 není k dispozici ikona komentovat vybrané řádky. Pokud nepoužíváte aplikaci Visual Studio 2008, bude nutné ručně přidat `<%--` a oddělovače `--%>`.

Dále přetáhněte ovládací prvek Login ze sady nástrojů na stránku a nastavte jeho vlastnost `ID` na hodnotu `myLogin`. V tuto chvíli by vaše obrazovka měla vypadat podobně jako na obrázku 3. Všimněte si, že výchozí rozhraní ovládacího prvku pro přihlášení obsahuje ovládací prvky TextBox pro uživatelské jméno a heslo, zaškrtávací políčko Zapamatovat mě v dalším čase a tlačítko přihlásit. K dispozici jsou také `RequiredFieldValidator` ovládací prvky pro dvě textová pole.

[![přidání ovládacího prvku pro přihlášení na stránku](validating-user-credentials-against-the-membership-user-store-vb/_static/image8.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image7.png)

**Obrázek 3**: Přidání ovládacího prvku pro přihlášení na stránku ([kliknutím zobrazíte obrázek v plné velikosti](validating-user-credentials-against-the-membership-user-store-vb/_static/image9.png))

A hotovi! Po kliknutí na tlačítko Přihlásit se k ovládacímu prvku přihlašování dojde k postbacku a ovládací prvek pro přihlášení zavolá metodu `Membership.ValidateUser`, která předá zadané uživatelské jméno a heslo. Pokud jsou přihlašovací údaje neplatné, ovládací prvek přihlášení zobrazí zprávu s oznámením, že. Pokud jsou však přihlašovací údaje platné, ovládací prvek přihlášení vytvoří lístek ověřování formuláře a přesměruje uživatele na příslušnou stránku.

Řízení přihlášení používá ke zjištění vhodné stránky pro přesměrování uživatele na základě úspěšného přihlášení čtyři faktory:

- Určuje, zda je ovládací prvek přihlášení na přihlašovací stránce definovaný `loginUrl` nastavení v konfiguraci ověřování pomocí formulářů. Výchozí hodnota tohoto nastavení je `Login.aspx`
- Přítomnost parametru `ReturnUrl` QueryString
- Hodnota [vlastnosti`DestinationUrl`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.destinationpageurl.aspx) ovládacího prvku pro přihlášení
- Hodnota `defaultUrl` zadaná v nastavení konfigurace ověřování formulářů; Výchozí hodnota tohoto nastavení je Default. aspx.

Obrázek 4 znázorňuje, jak ovládací prvek Login používá tyto čtyři parametry k přijetí na příslušné stránce rozhodnutí.

[![přidání ovládacího prvku pro přihlášení na stránku](validating-user-credentials-against-the-membership-user-store-vb/_static/image11.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image10.png)

**Obrázek 4**: Přidání ovládacího prvku pro přihlášení na stránku ([kliknutím zobrazíte obrázek v plné velikosti](validating-user-credentials-against-the-membership-user-store-vb/_static/image12.png))

Chvíli počkejte, než se otestuje přihlašovací řízení, a to tak, že navštívíte web prostřednictvím prohlížeče a přihlásíte se jako stávající uživatel v rámci systému členství.

Vykreslené rozhraní ovládacího prvku přihlášení je vysoce konfigurovatelné. Existuje mnoho vlastností, které ovlivňují jeho vzhled. a co víc, ovládací prvek pro přihlášení se dá převést na šablonu, aby se přes rozložení prvky uživatelského rozhraní poskytovala přesnou kontrolu. Zbývající část tohoto kroku zjistí, jak přizpůsobit vzhled a rozložení.

### <a name="customizing-the-login-controls-appearance"></a>Přizpůsobení vzhledu přihlašovacího ovládacího prvku

Nastavení výchozí vlastnosti ovládacího prvku pro přihlášení vykreslí uživatelské rozhraní s nadpisem (přihlásit se), textovým polem a popiskem pro zadání uživatelského jména a hesla, zaškrtávací políčko Zapamatovat mě Next Time a přihlašovací tlačítko. Vzhled těchto prvků je možné konfigurovat prostřednictvím mnoha vlastností ovládacího prvku přihlašovacího jména. Kromě toho je možné přidat další prvky uživatelského rozhraní, například odkaz na stránku pro vytvoření nového uživatelského účtu, a to nastavením vlastnosti nebo dvou.

Pojďme si za chvíli Gussy vzhled našeho přihlašovacího řízení. Vzhledem k tomu, že stránka `Login.aspx` již obsahuje text v horní části stránky, která říká přihlášení, je název ovládacího prvku přihlašovacího jména nadbytečný. Proto vymažte hodnotu [vlastnosti`TitleText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.titletext.aspx) , abyste mohli odebrat název ovládacího prvku přihlašovacího jména.

Uživatelské jméno: a heslo: popisky vlevo od dvou ovládacích prvků TextBox lze přizpůsobit pomocí [`UserNameLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.usernamelabeltext.aspx) a [`PasswordLabelText` vlastností](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordlabeltext.aspx), v uvedeném pořadí. Pojďme změnit uživatelské jméno: popisek pro čtení uživatelského jména:. Styly popisku a textového pole lze konfigurovat prostřednictvím [`LabelStyle`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.labelstyle.aspx) a [`TextBoxStyle` vlastností](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textboxstyle.aspx), v uvedeném pořadí.

Vlastnost text v poli zapamatovat mě v následujícím čase se dá nastavit prostřednictvím [vlastnosti`RememberMeText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermetext.aspx)ovládacího prvku pro přihlášení a její výchozí stav zaškrtnutí se dá nakonfigurovat prostřednictvím [vlastnosti`RememberMeSet`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.remembermeset.aspx) (která má výchozí hodnotu false). Pokračujte a nastavte vlastnost `RememberMeSet` na hodnotu true, aby se ve výchozím nastavení kontrolovalo zaškrtávací políčko Zapamatovat mě Next Time.

Ovládací prvek Login nabízí dvě vlastnosti pro úpravu rozložení ovládacích prvků uživatelského rozhraní. [Vlastnost`TextLayout`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.textlayout.aspx) označuje, zda jsou popisky zobrazeny nalevo od jejich odpovídajících textových polí (výchozí nastavení), nebo nad nimi. [Vlastnost`Orientation`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.orientation.aspx) označuje, zda jsou vstupy uživatelského jména a hesla umístěny svisle (jedna nad druhou) nebo horizontálně. Nechám tyto dvě vlastnosti nastavené na výchozí hodnoty, ale doporučujeme, abyste si vyzkoušeli nastavení těchto dvou vlastností na jiné než výchozí hodnoty, aby se zobrazil výsledný efekt.

> [!NOTE]
> V další části Konfigurace rozložení přihlašovacího ovládacího prvku se podíváme na použití šablon k definování přesného rozložení prvků uživatelského rozhraní ovládacího prvku rozložení.

Zabalte nastavení vlastností ovládacího prvku pro přihlášení nastavením [`CreateUserText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createusertext.aspx) a [vlastností`CreateUserUrl`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.createuserurl.aspx) na Neregistrováno? Vytvořte si účet! a `~/Membership/CreatingUserAccounts.aspx`v uvedeném pořadí. Tím se přidá hypertextový odkaz na rozhraní ovládacího prvku pro přihlášení ukazující na stránku, kterou jsme <a id="Tutorial05"> </a>vytvořili v [předchozím kurzu](creating-user-accounts-vb.md). Vlastnosti [`HelpPageText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppagetext.aspx) a [`HelpPageUrl`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.helppageurl.aspx) ovládacího prvku přihlášení a vlastnosti [`PasswordRecoveryText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoverytext.aspx) a [`PasswordRecoveryUrl`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.passwordrecoveryurl.aspx) fungují stejným způsobem, vykreslovat odkazy na stránku s usnadněním a stránku pro obnovení hesla.

Po provedení změn těchto vlastností by deklarativní značení a vzhled ovládacího prvku přihlašovacího jména měly vypadat podobně jako na obrázku 5.

[![hodnoty vlastností ovládacího prvku pro přihlašovací údaje určují jeho vzhled.](validating-user-credentials-against-the-membership-user-store-vb/_static/image14.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image13.png)

**Obrázek 5**: hodnoty vlastností ovládacího prvku pro přihlašovací údaje určují jeho vzhled ([kliknutím zobrazíte obrázek v plné velikosti](validating-user-credentials-against-the-membership-user-store-vb/_static/image15.png)).

### <a name="configuring-the-login-controls-layout"></a>Konfigurace rozložení ovládacího prvku přihlašovacího jména

Výchozí uživatelské rozhraní ovládacího prvku přihlašovací web určuje rozhraní v jazyce HTML `<table>`. Ale co když potřebujeme lepší kontrolu nad vykresleným výstupem? Je možné, že chceme nahradit `<table>` řadou značek `<div>`. Nebo co když naše aplikace vyžaduje pro ověřování další přihlašovací údaje? Mnoho finančních webů vyžaduje, aby uživatelé zadali nejen uživatelské jméno a heslo, ale také osobní identifikační číslo (PIN) nebo jiné identifikační údaje. Bez ohledu na to, jak je možné, lze ovládací prvek přihlášení převést na šablonu, ze které můžeme explicitně definovat deklarativní označení rozhraní.

Abychom mohli aktualizovat přihlašovací ovládací prvek pro shromažďování dalších přihlašovacích údajů, musíme udělat dvě věci:

1. Aktualizujte rozhraní ovládacího prvku přihlášení tak, aby zahrnovalo webové ovládací prvky, aby se shromáždily další přihlašovací údaje.
2. Přepište logiku interního ověřování ovládacího prvku přihlášení tak, aby byl uživatel ověřen pouze v případě, že jsou jeho uživatelské jméno a heslo platné a že jsou také platné jejich další přihlašovací údaje.

Abychom mohli dosáhnout prvního úkolu, musíme převést ovládací prvek Login na šablonu a přidat potřebné webové ovládací prvky. Jako u druhé úlohy lze logiku ověřování ovládacího prvku přihlášení nahradit vytvořením obslužné rutiny události pro [událost`Authenticate`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx)ovládacího prvku.

Pojďme aktualizovat přihlašovací ovládací prvek tak, aby vyzvat uživatele k zadání uživatelského jména, hesla a e-mailové adresy a ověří uživatele jenom v případě, že zadaná e-mailová adresa odpovídá své e-mailové adrese v souboru. Nejdřív je potřeba převést rozhraní ovládacího prvku Login na šablonu. V inteligentní značce ovládacího prvku přihlašovací jméno vyberte možnost převést na šablonu.

[![převedení přihlašovacího ovládacího prvku na šablonu](validating-user-credentials-against-the-membership-user-store-vb/_static/image17.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image16.png)

**Obrázek 6**: převod ovládacího prvku pro přihlášení na šablonu ([kliknutím zobrazíte obrázek v plné velikosti](validating-user-credentials-against-the-membership-user-store-vb/_static/image18.png))

> [!NOTE]
> Chcete-li vrátit ovládací prvek přihlášení ke své předběžné verzi šablony, klikněte na odkaz Obnovit z inteligentní značky ovládacího prvku.

Převedení přihlašovacího ovládacího prvku na šablonu přidá `LayoutTemplate` k deklarativní značce ovládacího prvku s prvky HTML a webovými ovládacími prvky definujícími uživatelské rozhraní. Jak ukazuje obrázek 7, převod ovládacího prvku na šablonu odebere z okno Vlastnosti počet vlastností, například `TitleText`, `CreateUserUrl`a tak dále, protože tyto hodnoty vlastností jsou při použití šablony ignorovány.

[![méně vlastností, které jsou k dispozici, když je ovládací prvek přihlášení převeden na šablonu](validating-user-credentials-against-the-membership-user-store-vb/_static/image20.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image19.png)

**Obrázek 7**: k dispozici je méně vlastností, pokud je ovládací prvek přihlášení převeden na šablonu ([kliknutím zobrazíte obrázek v plné velikosti).](validating-user-credentials-against-the-membership-user-store-vb/_static/image21.png)

Značky HTML v `LayoutTemplate` lze podle potřeby upravit. Stejně tak můžete do šablony přidat jakékoli nové webové ovládací prvky. Je ale důležité, aby hlavní webové ovládací prvky ovládacího prvku přihlášení zůstaly v šabloně a zůstaly přiřazené `ID` hodnoty. Konkrétně neodstraňujte ani neměňte `UserName` nebo `Password` textová pole, zaškrtávací políčko `RememberMe`, tlačítko `LoginButton`, popisek `FailureText` nebo ovládací prvky `RequiredFieldValidator`.

Abychom mohli shromažďovat e-mailovou adresu návštěvníka, musíme do šablony přidat textové pole. Přidejte následující deklarativní značku mezi řádek tabulky (`<tr>`), který obsahuje textové pole `Password` a řádek tabulky, který obsahuje následující zaškrtávací políčko pro zapamatování času:

[!code-aspx[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample2.aspx)]

Po přidání textového pole `Email` přejděte na stránku pomocí prohlížeče. Jak ukazuje obrázek 8, uživatelské rozhraní ovládacího prvku Login nyní obsahuje třetí textové pole.

[![přihlašovací řízení teď obsahuje textové pole pro e-mailovou adresu uživatele.](validating-user-credentials-against-the-membership-user-store-vb/_static/image23.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image22.png)

**Obrázek 8**: přihlašovací ovládací prvek teď obsahuje textové pole pro e-mailovou adresu uživatele ([kliknutím zobrazíte obrázek v plné velikosti).](validating-user-credentials-against-the-membership-user-store-vb/_static/image24.png)

V tomto okamžiku přihlašovací ovládací prvek stále používá metodu `Membership.ValidateUser` k ověření zadaných přihlašovacích údajů. Odpovídající hodnota, která se zadává do textového pole `Email`, nemá žádný vliv na to, jestli se uživatel může přihlásit. V kroku 3 se podíváme na to, jak přepsat logiku ověřování ovládacího prvku přihlášení, aby se přihlašovací údaje považovaly jenom za platné, pokud jsou uživatelské jméno a heslo platné a zadaná e-mailová adresa se shoduje s e-mailovou adresou v souboru.

## <a name="step-3-modifying-the-login-controls-authentication-logic"></a>Krok 3: změna logiky ověřování ovládacího prvku přihlášení

Když návštěvník poskytne své přihlašovací údaje a klikne na tlačítko Přihlásit se, vystavení se provede a přihlašovací řízení pokračuje prostřednictvím pracovního postupu ověřování. Pracovní postup se spustí tím, že se vyvyvolává [událost`LoggingIn`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggingin.aspx). Jakékoli obslužné rutiny události přidružené k této události mohou zrušit operaci přihlášení nastavením vlastnosti `e.Cancel` na hodnotu `True`.

Pokud není operace přihlášení zrušena, pracovní postup pokračuje vyvoláním [události`Authenticate`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.authenticate.aspx). Pokud je pro událost `Authenticate` obslužná rutina události, zodpovídá za určení, zda jsou zadaná pověření platná nebo nikoli. Pokud není zadána žádná obslužná rutina události, ovládací prvek Login používá metodu `Membership.ValidateUser` k určení platnosti přihlašovacích údajů.

Pokud jsou zadané přihlašovací údaje platné, vytvoří se lístek ověřování formulářů, vyvolá se [`LoggedIn` událost](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loggedin.aspx) a uživatel se přesměruje na příslušnou stránku. Pokud se však přihlašovací údaje považují za neplatné, vyvolá se [událost`LoginError`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.loginerror.aspx) a zobrazí se zpráva informující o tom, že jejich přihlašovací údaje byly neplatné. Ve výchozím nastavení při selhání ovládací prvek přihlášení jednoduše nastaví jeho vlastnost text ovládacího prvku popisek `FailureText` na zprávu o selhání (váš pokus o přihlášení nebyl úspěšný. Zkuste to prosím znovu. Pokud je však [vlastnost`FailureAction`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failureaction.aspx) ovládacího prvku pro přihlášení nastavena na hodnotu `RedirectToLoginPage`, pak přihlašovací řízení vydá `Response.Redirect` na přihlašovací stránku, která připojuje parametr QueryString `loginfailure=1` (což způsobí, že ovládací prvek Login zobrazí zprávu o selhání).

Obrázek 9 nabízí vývojový diagram pracovního postupu ověřování.

[![pracovního postupu ověřování ovládacího prvku přihlášení](validating-user-credentials-against-the-membership-user-store-vb/_static/image26.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image25.png)

**Obrázek 9**: pracovní postup ověření přihlašovacího ovládacího prvku ([kliknutím zobrazíte obrázek v plné velikosti](validating-user-credentials-against-the-membership-user-store-vb/_static/image27.png))

> [!NOTE]
> Pokud vás zajímá, že byste použili možnost `RedirectToLogin` stránky `FailureAction`, zvažte následující scénář. Nyní naše hlavní stránka `Site.master` v současné době zobrazuje v levém sloupci text, Hello, cizí, pokud je navštíven anonymní uživatel, ale Představme si, že jsme tento text nahradili přihlašovacím ovládacím prvkem. To umožňuje anonymnímu uživateli přihlásit se ze všech stránek na webu, aniž by musel navštěvovat přihlašovací stránku přímo. Pokud se ale uživatel nemůže přihlásit prostřednictvím ovládacího prvku pro přihlášení, který vygenerovala stránka předlohy, může to mít smysl ho přesměrovat na přihlašovací stránku (`Login.aspx`), protože tato stránka pravděpodobně obsahuje další pokyny, odkazy a další informace, jako jsou například odkazy na vytvoření nového účtu nebo načtení ztraceného hesla – které nebyly přidány do hlavní stránky.

### <a name="creating-theauthenticateevent-handler"></a>Vytvoření obslužné rutiny události`Authenticate`

Aby bylo možné připojit vlastní logiku ověřování, musíme vytvořit obslužnou rutinu události pro událost `Authenticate` ovládacího prvku pro přihlášení. Vytvořením obslužné rutiny události pro událost `Authenticate` se vygeneruje následující definice obslužné rutiny události:

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample3.vb)]

Jak vidíte, obslužná rutina události `Authenticate` je předána objektu typu [`AuthenticateEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.authenticateeventargs.aspx) jako jeho druhý vstupní parametr. Třída `AuthenticateEventArgs` obsahuje logickou vlastnost nazvanou `Authenticated`, která se používá k určení, zda jsou zadaná pověření platná. Do naší úlohy pak napíšete kód, který určuje, zda jsou zadané přihlašovací údaje platné, nebo ne, a nastavte vlastnost `e.Authenticate` odpovídajícím způsobem.

### <a name="determining-and-validating-the-supplied-credentials"></a>Určení a ověření zadaných přihlašovacích údajů

Pomocí vlastností [`UserName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.username.aspx) a [`Password`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.password.aspx) ovládacího prvku pro přihlášení Určete přihlašovací údaje uživatele a hesla zadané uživatelem. Chcete-li určit hodnoty zadané do jakýchkoli dalších webových ovládacích prvků (například `Email` textového pole, které jsme přidali v předchozím kroku), použijte `LoginControlID.FindControl`(" *`controlID`* ") k získání programového odkazu na webový ovládací prvek v šabloně, jejíž vlastnost `ID` je rovna *`controlID`* . Chcete-li například získat odkaz na textové pole `Email`, použijte následující kód:

`Dim EmailTextBox As TextBox = CType(myLogin.FindControl("Email"), TextBox)`

Aby bylo možné ověřit přihlašovací údaje uživatele, musíme udělat dvě věci:

1. Ujistěte se, že zadané uživatelské jméno a heslo jsou platné.
2. Zajistěte, aby zadaná e-mailová adresa odpovídala e-mailové adrese v souboru, aby se uživatel pokusil přihlásit.

Pro provedení první kontroly můžeme jednoduše použít metodu `Membership.ValidateUser`, jako bychom viděli v kroku 1. Pro druhou kontrolu musíme určit e-mailovou adresu uživatele, abychom ji mohli porovnat s e-mailovou adresou, kterou zadal do ovládacího prvku TextBox. Chcete-li získat informace o konkrétním uživateli, použijte [metodu`GetUser`](https://msdn.microsoft.com/library/system.web.security.membership.getuser.aspx)třídy `Membership`.

Metoda `GetUser` má několik přetížení. Pokud se tato funkce použije bez předání jakýchkoli parametrů, vrátí informace o aktuálně přihlášeném uživateli. Chcete-li získat informace o konkrétním uživateli, zavolejte `GetUser` předání přihlašovacího jména. V obou případech `GetUser` vrátí [objekt`MembershipUser`](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx), který má vlastnosti jako `UserName`, `Email`, `IsApproved`, `IsOnline`a tak dále.

Následující kód implementuje tyto dvě kontroly. Je-li nastaveno obě metody Pass, je `e.Authenticate` nastavena na `True`, jinak je přiřazen `False`.

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample4.vb)]

V případě tohoto kódu se pokuste přihlásit jako platný uživatel a zadat správné uživatelské jméno, heslo a e-mailovou adresu. Zkuste to znovu, ale tentokrát záměrně použít nesprávnou e-mailovou adresu (viz obrázek 10). Nakonec se pomocí neexistujícího uživatelského jména pokuste použít jiný čas. V prvním případě byste měli být úspěšně přihlášení k lokalitě, ale v posledních dvou případech byste měli vidět zprávu neplatných přihlašovacích údajů ovládacího prvku přihlašovací jméno.

[![tito se nemůže přihlásit při zadání nesprávné e-mailové adresy.](validating-user-credentials-against-the-membership-user-store-vb/_static/image29.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image28.png)

**Obrázek 10**: Tito se nemůže přihlásit při zadání nesprávné e-mailové adresy ([kliknutím zobrazíte obrázek v plné velikosti).](validating-user-credentials-against-the-membership-user-store-vb/_static/image30.png)

> [!NOTE]
> Jak je popsáno v části jak rozhraní členství zpracovává neúspěšné pokusy o přihlášení v kroku 1, když je volána metoda `Membership.ValidateUser` a předala neplatné přihlašovací údaje, sleduje Neplatný pokus o přihlášení a zamkne uživatele, pokud překročí určitou prahovou hodnotu neplatných pokusů v zadaném časovém intervalu. Vzhledem k tomu, že naše vlastní logika ověřování volá metodu `ValidateUser`, nesprávnému heslu pro platné uživatelské jméno dojde k zvýšení neplatného počítadla počtu pokusů o přihlášení, ale v případě, že je uživatelské jméno a heslo platné, není tento čítač zvýšený, ale e-mailová adresa není správná. Důvodem je to, že toto chování je vhodné, protože je pravděpodobné, že hacker bude znát uživatelské jméno a heslo, ale musí použít techniky hrubou silou k určení e-mailové adresy uživatele.

## <a name="step-4-improving-the-login-controls-invalid-credentials-message"></a>Krok 4: vylepšení zprávy s neplatnými přihlašovacími údaji ovládacího prvku pro přihlášení

Když se uživatel pokusí přihlásit pomocí neplatných přihlašovacích údajů, zobrazí ovládací prvek přihlášení zprávu s vysvětlením, že se pokus o přihlášení nezdařil. Konkrétně ovládací prvek zobrazuje zprávu určenou [vlastností`FailureText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.failuretext.aspx), která má výchozí hodnotu pokusu o přihlášení nebylo úspěšné. Zkuste to prosím znovu.

Odvolat, že existuje mnoho důvodů, proč přihlašovací údaje uživatele mohou být neplatné:

- Uživatelské jméno možná neexistuje.
- Uživatelské jméno existuje, ale heslo je neplatné.
- Uživatelské jméno a heslo jsou platné, ale uživatel se ještě neschválil.
- Uživatelské jméno a heslo jsou platné, ale uživatel je uzamčený (pravděpodobně proto, že překročil počet neplatných pokusů o přihlášení v rámci zadaného časového rámce).

A při použití vlastní logiky ověřování mohou nastat jiné důvody. Například s kódem, který jsme napsali v kroku 3, může být uživatelské jméno a heslo platné, ale e-mailová adresa může být nesprávná.

Bez ohledu na to, proč jsou přihlašovací údaje neplatné, zobrazí ovládací prvek přihlášení stejnou chybovou zprávu. Tato nedostatečná zpětná vazba může být matoucí pro uživatele, jehož účet ještě nebyl schválen nebo byl uzamčen. I když máme trochu práci, můžeme ovládacímu prvku přihlášení zobrazit vhodnější zprávu.

Pokaždé, když se uživatel pokusí přihlásit s neplatnými přihlašovacími údaji, vyvolá ovládací prvek pro přihlášení událost `LoginError`. Pokračujte a vytvořte obslužnou rutinu události pro tuto událost a přidejte následující kód:

[!code-vb[Main](validating-user-credentials-against-the-membership-user-store-vb/samples/sample5.vb)]

Výše uvedený kód začíná nastavením vlastnosti `FailureText` ovládacího prvku pro přihlášení na výchozí hodnotu (váš pokus o přihlášení nebyl úspěšný. Zkuste to prosím znovu. Pak zkontroluje, jestli je zadané uživatelské jméno namapováno na existující uživatelský účet. V takovém případě se na základě vlastností `IsLockedOut` a `IsApproved` `MembershipUser` objektu zobrazí informace o tom, jestli byl účet uzamčený nebo ještě není schválený. V obou případech je vlastnost `FailureText` aktualizována na odpovídající hodnotu.

K otestování tohoto kódu se záměrně pokus o přihlášení jako stávající uživatel, ale použijte nesprávné heslo. Udělejte to pětkrát za řádek během 10 minut a účet se zablokuje. Jak ukazuje obrázek 11, následné pokusy o přihlášení vždy selžou (i se správným heslem), ale teď se zobrazí podrobnější popis, který váš účet byl uzamčen z důvodu příliš velkého počtu neplatných pokusů o přihlášení. Kontaktujte prosím správce, aby se Váš účet odemkl.

[![tito provedlo příliš mnoho neplatných pokusů o přihlášení a byl uzamčen.](validating-user-credentials-against-the-membership-user-store-vb/_static/image32.png)](validating-user-credentials-against-the-membership-user-store-vb/_static/image31.png)

**Obrázek 11**: tito provedl příliš mnoho neplatných pokusů o přihlášení a byl uzamčen ([kliknutím zobrazíte obrázek v plné velikosti).](validating-user-credentials-against-the-membership-user-store-vb/_static/image33.png)

## <a name="summary"></a>Souhrn

Před tímto kurzem přihlašovací stránka ověřila zadané přihlašovací údaje proti pevně zakódovanému seznamu párů uživatelských jmen a hesel. V tomto kurzu jsme aktualizovali stránku, aby ověřila přihlašovací údaje proti členskému rozhraní. V kroku 1 jsme si vyhledali použití metody `Membership.ValidateUser` programově. V kroku 2 jsme nahradili naše ručně vytvořené uživatelské rozhraní a kód pomocí přihlašovacího ovládacího prvku.

Přihlašovací ovládací prvek vykreslí standardní přihlašovací uživatelské rozhraní a automaticky ověří přihlašovací údaje uživatele v rámci architektury členství. V případě platných přihlašovacích údajů navíc přihlašovací ovládací prvek podepisuje uživatele prostřednictvím ověřování pomocí formulářů. V krátkém případě je k dispozici plně funkční uživatelské prostředí přihlášení pouhým přetažením ovládacího prvku pro přihlášení na stránku bez nutnosti dalšího deklarativního kódu. A co více, ovládací prvek přihlašování je vysoce přizpůsobitelný, což umožňuje jemný stupeň kontroly nad vykresleným uživatelským rozhraním a logikou ověřování.

V tomto okamžiku můžou Návštěvníci na našem webu vytvořit nový uživatelský účet a přihlásit se k webu, ale ještě jsme si vyhledali omezení přístupu k stránkám na základě ověřeného uživatele. V současné době může libovolný uživatel, ověřený nebo anonymní zobrazit jakoukoli stránku na našem webu. Společně s řízením přístupu na stránky našeho webu na základě uživatele můžeme mít určité stránky, jejichž funkce závisí na uživateli. V dalším kurzu se podíváme na to, jak omezit přístup a funkce na stránce na základě přihlášeného uživatele.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Zobrazení vlastních zpráv pro zamčené a neschválené uživatele](http://aspnet.4guysfromrolla.com/articles/050306-1.aspx)
- [Zkoumání členství, rolí a profilů v ASP.NET 2.0](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [Postupy: vytvoření přihlašovací stránky ASP.NET](https://msdn.microsoft.com/library/ms178331.aspx)
- [Technická dokumentace k řízení přihlašování](https://msdn.microsoft.com/library/system.web.ui.webcontrols.login.aspx)
- [Používání ovládacích prvků přihlášení](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/login.aspx)

### <a name="about-the-author"></a>O autorovi

Scott Mitchell, autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je *[Sams naučit se ASP.NET 2,0 za 24 hodin](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* . Scott se dá kontaktovat [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Teresa Murphy a Michael Olivero. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com).

> [!div class="step-by-step"]
> [Předchozí](creating-user-accounts-vb.md)
> [Další](user-based-authorization-vb.md)

---
uid: web-forms/overview/moving-to-aspnet-20/membership
title: Členství | Microsoft Docs
author: microsoft
description: ASP.NET členství sestaví na úspěchu modelu ověřování pomocí formulářů z ASP.NET 1. x. Ověřování pomocí formulářů ASP.NET nabízí pohodlný způsob, jak zamezit...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: f2339485-5d78-4c5e-8c0a-dc9b8a315345
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/membership
msc.type: authoredcontent
ms.openlocfilehash: da6fc205bd852a818d65425586cec38fdb08d310
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78642154"
---
# <a name="membership"></a>Členství

od [Microsoftu](https://github.com/microsoft)

> ASP.NET členství sestaví na úspěchu modelu ověřování pomocí formulářů z ASP.NET 1. x. Ověřování pomocí formulářů ASP.NET poskytuje pohodlný způsob, jak začlenit přihlašovací formulář do vaší aplikace ASP.NET a ověřovat uživatele proti databázi nebo jinému úložišti dat.

ASP.NET členství sestaví na úspěchu modelu ověřování pomocí formulářů z ASP.NET 1. x. Ověřování pomocí formulářů ASP.NET poskytuje pohodlný způsob, jak začlenit přihlašovací formulář do vaší aplikace ASP.NET a ověřovat uživatele proti databázi nebo jinému úložišti dat. Členové třídy FormsAuthentication umožňují zpracovávat soubory cookie pro ověřování, kontrolovat platné přihlašovací údaje, odhlásit uživatele atd. Implementace ověřování pomocí formulářů v aplikaci ASP.NET 1. x ale může vyžadovat spravedlivé množství kódu.

Členství v ASP.NET 2,0 je hlavním postupem při použití samotného ověřování pomocí formulářů. (Členství je nejvíce robustní při kombinaci s ověřováním pomocí formulářů, ale ověřování pomocí formulářů není vyžadováno.) Jak budete brzy vidět, můžete použít členství v ASP.NET a ovládací prvky přihlášení v ASP.NET 2,0 k implementaci výkonného systému členství, aniž byste museli psát mnoho kódu.

## <a name="implementing-membership-in-aspnet-20"></a>Implementace členství v ASP.NET 2,0

Členství je implementováno pomocí následujících čtyř kroků. Mějte na paměti, že existuje mnoho dílčích kroků, které se týkají, a také volitelná konfigurace, kterou je možné implementovat. Tyto kroky jsou určeny k ilustraci velkého obrázku konfigurace členství.

1. Vytvořte databázi členství (Pokud se jako úložiště členství používá SQL Server.)
2. Zadejte možnosti členství v konfiguračních souborech vašich aplikací. (Členství je ve výchozím nastavení povolené.)
3. Určete typ úložiště členství, který chcete použít. Možnosti jsou: 

    - Microsoft SQL Server (verze 7,0 nebo novější)
    - Úložiště služby Active Directory
    - Vlastní zprostředkovatel členství
4. Nakonfigurujte aplikaci pro ověřování ASP.NET Forms. Později je členství navrženo tak, aby využívalo výhod ověřování pomocí formulářů, ale ověřování pomocí formulářů není vyžadováno.
5. Definujte uživatelské účty pro členství a v případě potřeby nakonfigurujte role.

## <a name="creating-the-membership-database"></a>Vytváření databáze členství

Pokud používáte jako úložiště členství SQL Server 7,0 nebo novější, můžete ke konfiguraci databáze použít nástroj ASPNET\_regsql (k dispozici z příkazového řádku Visual Studio .NET 2005). Nástroj ASPNET\_regsql lze použít jako nástroj příkazového řádku nebo pomocí Průvodce grafickým uživatelským rozhraním. Nejjednodušším způsobem konfigurace databáze je metoda průvodce. Chcete-li získat přístup k průvodci, stačí spustit následující příkaz:

`aspnet_regsql W`

Po spuštění tohoto příkazu se zobrazí Průvodce nastavením ASP.NET SQL Server, jak je znázorněno níže.

![](membership/_static/image1.jpg)

**Obrázek 1**

Průvodce instalací SQL Server ASP.NET vytvoří web v instanci, kterou zadáte v průvodci. ASP.NET ale použije připojovací řetězec v souboru Machine. config pro připojení k vaší databázi. Ve výchozím nastavení bude tento připojovací řetězec ukazovat na instanci SQL Server 2005, takže pokud používáte SQL Server 2000 nebo SQL Server 7,0 instance, bude nutné upravit připojovací řetězec v souboru Machine. config. Připojovací řetězec může být umístěn zde:

[!code-xml[Main](membership/samples/sample1.xml)]

Pokud ale připojovací řetězec neupravíte, ASP.NET vám nezobrazí popisnou chybu. Bude pouze pokračovat na stížnosti, že jste databázi nevytvořili. V případě výše jsme změnili připojovací řetězec tak, aby odkazoval na místní instanci SQL Server 2000.

## <a name="specifying-configuration-and-adding-users-and-roles"></a>Určení konfigurace a přidání uživatelů a rolí

Dalším krokem při konfiguraci členství je přidání potřebných informací do souboru Web. config aplikace. V ASP.NET 1. x je změna souboru Web. config někdy obtížné kvůli použití lowerCamelCase a chybějící technologie IntelliSense. Visual Studio .NET 2005 usnadňuje práci s technologií IntelliSense pro konfigurační soubory, ale ASP.NET 2,0 ještě jeden krok provedete tak, že poskytnete webové rozhraní pro úpravu konfiguračních souborů.

Webové rozhraní můžete spustit kliknutím na tlačítko Konfigurace ASP.NET na panelu nástrojů Průzkumník řešení, jak je znázorněno níže. Webové rozhraní můžete také spustit pomocí automaticky otevíraných oken, která se zobrazí, když jsou vloženy ovládací prvky přihlášení.

![](membership/_static/image2.jpg)

**Obrázek 2**

Tím se spustí nástroj pro správu webu ASP.NET zobrazený níže. Správa webu ASP.NET je rozhraní se čtyřmi kartami, které usnadňuje správu nastavení aplikace. K dispozici jsou následující karty:

- **Domovské**
- **Zabezpečení** Nakonfigurujte uživatele, role a přístup.
- **Aplikace** Nakonfigurujte nastavení aplikace.
- **Poskytovatel** Nakonfigurujte a otestujte poskytovatele členství aplikací.

Nástroj pro správu webu umožňuje snadno vytvářet nové uživatele, vytvářet nové role a spravovat uživatele a role. Tato možnost není k dispozici v rozhraní systému Windows. Rozhraní Windows umožňuje snadno definovat autorizační nastavení a přidávat, odstraňovat a spravovat poskytovatele, funkce, které nejsou v nástroji pro správu webu.

Chcete-li spustit rozhraní systému Windows, otevřete modul snap-in Internetová informační služba, klikněte pravým tlačítkem na aplikaci a vyberte možnost Vlastnosti. Klikněte na kartu ASP.NET a potom klikněte na tlačítko Upravit konfiguraci. (Aby se povolilo tlačítko Upravit konfiguraci, musí být aplikace spuštěná pod ASP.NET 2,0. Verzi ASP.NET můžete nakonfigurovat také v dialogovém okně ASP.NET.) Zobrazí se dialogové okno nastavení konfigurace ASP.NET, jak je znázorněno níže.

![](membership/_static/image3.jpg)

**Obrázek 3**

Na kartě Obecné jsou uvedené připojovací řetězce a nastavení aplikace. Všechna nastavení v kurzívě jsou definována v nadřazeném konfiguračním souboru (buď Machine. config nebo Web. config na vyšší úrovni) a nastavení, která nejsou kurzívou, jsou z konfiguračního souboru aplikací. Pokud se nastavení přidá, odebere nebo upraví na úrovni aplikace, ASP.NET místo odebrání nastavení z konfiguračního souboru, ze kterého se dědí, přidá, odebere nebo upraví nastavení na stránce Web. config úrovně aplikace.

Karta ověřování je uvedená níže. Tady budete konfigurovat nastavení členství. Nastavení ověřování formulářů, zprostředkovatelé členství a zprostředkovatelé rolí lze nakonfigurovat zde.

![](membership/_static/image4.jpg)

**Obrázek 4**

## <a name="implementing-membership-in-your-application"></a>Implementace členství v aplikaci

Nejjednodušší způsob, jak implementovat členství v ASP.NET 2,0 ve vaší aplikaci, je použití zadaných přihlašovacích ovládacích prvků. Tato metoda umožňuje implementovat základy členství v ASP.NET 2,0 bez nutnosti psát jakýkoli kód vůbec.

V ASP.NET 2,0 jsou k dispozici následující ovládací prvky přihlášení:

## <a name="login-control"></a>Řízení přihlášení

Ovládací prvek Login poskytuje rozhraní pro někoho, co se přihlašuje do vašeho systému členství. Poskytne vám textové pole uživatelské jméno a heslo a tlačítko pro přihlášení. Řada dalších běžných funkcí, jako je například odkaz k registraci pro lidi, kteří ještě neudělali, zaškrtávací políčko, které uživateli umožňuje automatické přihlášení při následných návštěvách, odkaz na připomenutí hesla atd. Všechny funkce ovládacího prvku Login jsou přizpůsobitelné prostřednictvím vlastností ovládacího prvku.

V ASP.NET 1. x museli vývojáři psát spravedlivé množství kódu, aby mohli vyhledávat při ověřování pomocí formulářů. Pomocí členství v ASP.NET 2,0 můžete ověřovat uživatele bez nutnosti psát jakýkoli kód. ASP.NET automaticky provede hledání uživatele. (Pokud používáte ovládací prvek přihlášení bez použití členství v ASP.NET, můžete k ověření uživatele použít metodu **ověřování** .)

## <a name="loginview-control"></a>Ovládací prvek LoginView

Ovládací prvek LoginView je ovládací prvek bez vizuálního vzhledu, který ve výchozím nastavení poskytuje dvě šablony. AnonymousTemplate a LoggedInTemplate. Zobrazená šablona je určena bez ohledu na to, zda je uživatel přihlášen k systému členství. Tento ovládací prvek se obvykle používá k zobrazení přihlašovacího ovládacího prvku, když uživatel ještě není přihlášený, a ovládací stavu přihlášení ovládací prvek a další přihlašovací ovládací prvky, když se uživatel přihlásí. Pokud používáte správu rolí v aplikaci ASP.NET, ovládací prvek LoginView může zobrazit specifickou šablonu založenou na roli uživatele. (Další informace o správě rolí ASP.NET se týkají později.)

## <a name="passwordrecovery-control"></a>Ovládací prvek PasswordRecovery

Ovládací prvek PasswordRecovery umožňuje uživatelům příjem e-mailů s jeho aktuálním heslem nebo resetování jeho hesla. Nešifrovaný text a šifrovaná hesla se dají obnovit a poslat uživatelům e-mailem. Pokud je heslo nastaveno na hodnotu hash, nelze ho obnovit. Místo toho bude uživatel muset provést resetování hesla.

## <a name="loginstatus-control"></a>Ovládací prvek ovládací stavu přihlášení

Ovládací prvek ovládací stavu přihlášení se používá k zobrazení indikátoru přihlášení pro uživatele, kteří nejsou přihlášení, a indikátor odhlášení pro uživatele, kteří jsou aktuálně přihlášení. Vlastnost Request. neověřená se používá k určení indikátoru, který se má zobrazit. Indikátor zobrazený ovládacím prvkem ovládací stavu přihlášení může být text (implementovaný prostřednictvím vlastností **LoginText** a **LogoutText** ) nebo imagí (implementované prostřednictvím vlastností **LoginImageUrl** a **LogoutImageUrl** ).

Když se uživatel odhlásí prostřednictvím ovládacího prvku ovládací stavu přihlášení, přesměruje na adresu URL určenou vlastností **LogoutPageUrl** . Pokud tato vlastnost není nastavená, aktuální stránka se aktualizuje. Vzhledem k tomu, že lokalita je nejspíš chráněna ověřováním pomocí formulářů, aktualizuje aktuální stránku uživatele na přihlašovací stránku pro daný web.

## <a name="loginname-control"></a>Ovládací prvek LoginName

Ovládací prvek LoginName zobrazuje uživatelské jméno aktuálně přihlášeného k webu.

## <a name="createuserwizard-control"></a>CreateUserWizard Control

Ovládací prvek ovládacím CreateUserWizard poskytuje uživatelům pohodlný způsob, jak si zaregistrovat svůj systém členství. Můžete přidat kroky (implementované jako kolekce WizardStep) prostřednictvím rozhraní uvedeného níže.

![](membership/_static/image5.jpg)

**Obrázek 5**

Ovládacím CreateUserWizard je ovládací prvek bez vizuálního vzhledu, který je odvozený od třídy Wizard a poskytuje následující šablony:

- **Šablona HeaderTemplate** Tato šablona ovládá vzhled záhlaví průvodce.
- **Oddíl SideBarTemplate** Tato šablona ovládá vzhled postranního panelu Průvodce.
- **Oddíl StartNavigationTemplate** Tato šablona ovládá vzhled navigace v úvodním kroku.
- **Oddíl StepNavigationTemplate** Tato šablona ovládá vzhled navigační oblasti, pokud není v kroku zahájení nebo dokončení.
- **Oddíl FinishNavigationTemplate** Tato šablona ovládá vzhled navigační oblasti v kroku dokončení.

V případě každého kroku, který přidáte do průvodce, ASP.NET vytvoří vlastní šablonu, která obsahuje objekt ContentTemplate a oddíl CustomNavigationTemplate pro daný krok. Úplné podrobnosti o přizpůsobení ovládacím CreateUserWizard najdete v dokumentaci k VS.NET 2005:

## <a name="changepassword-control"></a>Ovládací prvek ChangePassword

Ovládací prvek ChangePassword umožňuje uživatelům změnit své heslo. Pokud má vlastnost DisplayUserName hodnotu true (ve výchozím nastavení je to false), může uživatel změnit své heslo, pokud nejsou přihlášeni. Pokud *je* uživatel již přihlášen a vlastnost DisplayUserName je nastavena na hodnotu true, bude uživatel moci změnit heslo jiného uživatele, který není přihlášený, aby znal ID uživatele daného uživatele.

Mějte na paměti, že pokud chcete, aby uživatelé mohli měnit hesla, aniž byste se museli přihlašovat, budete muset zajistit, aby se stránka, na které se ovládací prvek ChangePassword zobrazuje, dala anonymní přístup. Uživatelé budou muset zadat své staré heslo, aby si mohli změnit heslo.

## <a name="role-management"></a>Správa rolí

Správa rolí umožňuje přiřadit uživatele k určité roli a pak omezit přístup k určitým souborům nebo složkám na základě této role. Správa rolí taky poskytuje rozhraní API, pomocí kterého můžete programově určit role uživatelů nebo určit všechny uživatele v určité roli a odpovídajícím způsobem odpovědět.

Správa rolí není požadavkem v členství v ASP.NET, a proto není požadavkem pro použití správy rolí členem členství. Nicméně dva doplňují v tomto dodatku a je pravděpodobnější, že je budou používat společně spolu s nimi.

Chcete-li povolit správu rolí ve vaší aplikaci, proveďte následující změny v souboru Web. config:

[!code-xml[Main](membership/samples/sample2.xml)]

Pokud je atribut **CacheRolesInCookie** nastaven na hodnotu true, ASP.NET ukládá členství v rolích uživatelů do souboru cookie v klientovi. To umožňuje, aby vyhledávání rolí probíhalo bez volání do poskytovatel RoleProvider. Při použití tohoto atributu doporučujeme vývojářům zajistit, aby byl atribut **CookieProtection** nastaven na hodnotu vše. (Toto je výchozí nastavení.) Tím se zajistí, že se data cookie šifrují a napomáhají zajistit, aby se obsah souborů cookie nezměnil. Role je možné přidat pomocí nástroje pro správu webu. Umožňuje snadno definovat role, konfigurovat přístup k částem lokality na základě těchto rolí a přiřazovat uživatele k rolím.

![](membership/_static/image6.jpg)

**Obrázek 6**

Jak vidíte výše, můžete přidat nové role pouhým zadáním názvu role a kliknutím na Přidat roli. Existující role se dají spravovat nebo odstraňovat kliknutím na příslušný odkaz v seznamu existujících rolí.

Při správě role můžete přidat nebo odebrat uživatele, jak je znázorněno níže.

![](membership/_static/image7.jpg)

**Obrázek 7**

Zaškrtnutím políčka Uživatel je v roli můžete snadno přidat uživatele do konkrétní role. ASP.NET bude automaticky aktualizovat vaši databázi členství odpovídajícími položkami. Budete také chtít nakonfigurovat pravidla přístupu pro aplikaci. Vývojáři ASP.NET 1. x jsou obeznámeni s tím, že se to dělá prostřednictvím elementu &lt;Authorization&gt; v souboru Web. config a tato možnost je stále k dispozici v ASP.NET 2,0. Správa pravidel přístupu však usnadňuje správu pomocí nástroje pro správu webu, jak je znázorněno níže.

![](membership/_static/image8.jpg)

**Obrázek 8**

V takovém případě je zvýrazněna složka pro správu (je obtížné ji vidět, protože nástroj je zvýrazní šedě) a má roli správců udělen přístup. Všichni ostatní uživatelé mají odepřený přístup. Můžete kliknout na ikonu záhlaví a vybrat pravidlo a potom pomocí tlačítek nahoru a dolů seřadit pravidla. Stejně jako u elementu ASP.NET &lt;Authorization&gt; se pravidla zpracovávají v pořadí, ve kterém se zobrazují. Jinými slovy, pokud se pořadí pravidel v snímku výše vrátilo zpět, nikdo by neměl přístup ke složce pro správu, protože první pravidlo, které by se ASP.NET, by představovalo pravidlo, které zakazuje všem do složky.

ASP.NET 2,0 přidá soubor Web. config do složky, pro kterou zadáváte přístupové pravidlo. Pravidla přístupu se dají upravovat pomocí konfiguračního souboru nebo pomocí nástroje pro správu webu. Jinými slovy, nástroj pro správu webu je jednoduše rozhraní, pomocí kterého se konfigurační soubor dá upravovat v uživatelsky přívětivém prostředí.

## <a name="using-roles-in-code"></a>Použití rolí v kódu

Rozhraní API pro správu rolí se od verze 1. x nezměnilo. Metoda **IsInRole** slouží k určení, jestli je uživatel v určité roli.

[!code-csharp[Main](membership/samples/sample3.cs)]

ASP.NET také vytvoří instanci tento RolePrincipal jako člena aktuálního kontextu. Objekt tento RolePrincipal lze použít k získání všech rolí, ke kterým uživatel patří, následovně:

[!code-csharp[Main](membership/samples/sample4.cs)]

## <a name="using-rolegroups-with-the-loginview-control"></a>Použití kolekci RoleGroups s ovládacím prvkem LoginView

Teď, když jste obeznámeni se správou rolí a členstvím, umožňuje stručně diskutovat, jak ovládací prvek LoginView využívá tuto funkci v ASP.NET 2,0. Jak už bylo popsáno, ovládací prvek LoginView je ovládací prvek bez vizuálního vzhledu, který ve výchozím nastavení obsahuje dvě šablony; AnonymousTemplate a LoggedInTemplate. V dialogovém okně úlohy LoginView je odkaz (zobrazený níže), který umožňuje upravit kolekci RoleGroups.

![](membership/_static/image9.jpg)

**Obrázek 9**

Každý objekt ve skupinových rolích obsahuje pole řetězců, které definují role, na které se vztahuje role. Chcete-li do ovládacího prvku LoginView přidat novou skupina rolí, klikněte na odkaz upravit kolekci RoleGroups. Na obrázku výše vidíte, že jsem pro správce přidal novou skupinu rolí. Výběrem této skupiny rolí (skupiny rolí [0]) z rozevíracího seznamu zobrazení lze nakonfigurovat šablonu, která bude zobrazena pouze pro členy role správců. Na následujícím obrázku jsem přidal novou roli role, která se vztahuje na členy role Sales a role distribuce. Tím se přidá druhá role do rozevíracího seznamu zobrazení v dialogovém okně úlohy LoginView a cokoli přidané do této šablony uvidí libovolný uživatel v roli Sales nebo Distribution.

![](membership/_static/image10.jpg)

**Obrázek 10**

## <a name="overriding-the-existing-membership-provider"></a>Přepsání stávajícího zprostředkovatele členství

Existuje několik způsobů, jak můžete roztáhnout funkce ASP.NET členství. První z nich můžete zjevně změnit stávající funkce třídy SqlMembershipProvider děděním z ní a přepsáním jejích metod. Například pokud chcete implementovat vlastní funkce při vytváření uživatelů, můžete vytvořit vlastní třídu, která dědí z SqlMembershipProvider následujícím způsobem:

[!code-csharp[Main](membership/samples/sample5.cs)]

Pokud na druhé straně chcete vytvořit vlastního poskytovatele (pro ukládání informací o členství v databázi Access), můžete vytvořit vlastního poskytovatele.

## <a name="creating-your-own-membership-provider"></a>Vytvoření vlastního poskytovatele členství

Chcete-li vytvořit vlastního poskytovatele členství, budete nejprve muset vytvořit třídu, která dědí z třídy MembershipProvider. Pokud používáte VB.NET, Visual Studio 2005 přidá zástupné procedury pro všechny metody, které je třeba přepsat. Pokud používáte C#, můžete přidat zástupné procedury.

Bude nutné přepsat následující:

- ApplicationName – vlastnost
- ChangePassword – funkce
- ChangePasswordQuestionAndAnswer – funkce
- CreateUser – funkce
- DeleteUser – funkce
- Vlastnost EnablePasswordReset
- Vlastnost EnablePasswordRetrieval
- FindUsersByEmail – funkce
- FindUsersByName – funkce
- GetAllUsers – funkce
- GetNumberOfUsersOnline – funkce
- GetPassword – funkce
- GetUser – funkce
- GetUserNameByEmail – funkce
- Vlastnost MaxInvalidPasswordAttempts
- Vlastnost hodnota MinRequiredNonAlphanumericCharacters
- Vlastnost hodnota minRequiredPasswordLength
- Vlastnost PasswordAttemptWindow
- Vlastnost PasswordFormat
- Vlastnost PasswordStrengthRegularExpression
- Vlastnost RequiresQuestionAndAnswer
- Vlastnost RequiresUniqueEmail
- ResetPassword – funkce
- Odemknout funkci uživatele
- UpdateUser – funkce
- ValidateUser – funkce

To je poměrně seznam, který se má implementovat C# jako vývojář. Může být snazší vytvořit třídu v VB.NET bez implementace a pak použít reflektor .NET nebo podobný nástroj k převedení kódu na C#.

Připojovací řetězec a další vlastnosti by měly být nastaveny na výchozí hodnoty v metodě Initialize. (Metoda Initialize je vyvolána, když je poskytovatel načten za běhu.) Druhý parametr metody Initialize je typu System. Collections. specialize. kolekce NameValueCollection a je odkaz na &lt;přidání&gt; elementu, který je přidružen k vašemu vlastnímu poskytovateli v souboru Web. config. Tato položka vypadá takto:

[!code-xml[Main](membership/samples/sample6.xml)]

Tady je příklad metody Initialize.

[!code-csharp[Main](membership/samples/sample7.cs)]

Aby bylo možné uživatele ověřit při odeslání přihlašovacího formuláře, budete muset použít metodu ValidateUser. Tato metoda je aktivována, když uživatel klikne na tlačítko pro přihlášení v ovládacím prvku Login. Umístíte svůj kód, který bude vyhledávat uživatel v této metodě.

Jak vidíte, psaní vlastního poskytovatele členství není obtížné a umožňuje rozšířit tyto výkonné funkce ASP.NET 2,0.

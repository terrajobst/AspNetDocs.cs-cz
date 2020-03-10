---
uid: identity/overview/extensibility/overview-of-custom-storage-providers-for-aspnet-identity
title: Přehled zprostředkovatelů vlastních úložišť pro ASP.NET Identity ASP.NET 4. x
author: Rick-Anderson
description: ASP.NET Identity je rozšiřitelný systém, který umožňuje vytvořit vlastního poskytovatele úložiště a zapojit ho do aplikace bez nutnosti znovu pracovat s aplikace...
ms.author: riande
ms.date: 10/13/2014
ms.assetid: 681a9204-462e-4260-9a0b-19f0644d6ad7
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/overview-of-custom-storage-providers-for-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 21baedf6285b411f89627df9ca25d47a2a42e387
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584411"
---
# <a name="overview-of-custom-storage-providers-for-aspnet-identity"></a>Přehled poskytovatelů vlastního úložiště pro ASP.NET Identity

tím, že [FitzMacken](https://github.com/tfitzmac)

> ASP.NET Identity je rozšiřitelný systém, který umožňuje vytvořit vlastního poskytovatele úložiště a připojit ho k aplikaci bez nutnosti opětovného zpracování aplikace. Toto téma popisuje, jak vytvořit přizpůsobeného poskytovatele úložiště pro ASP.NET Identity. Popisuje důležité koncepty pro vytvoření vlastního poskytovatele úložiště, ale nejedná se o podrobný návod k implementaci vlastního poskytovatele úložiště.
> 
> Příklad implementace vlastního poskytovatele úložiště najdete v tématu [implementace vlastního poskytovatele úložiště ASP.NET identity MySQL](implementing-a-custom-mysql-aspnet-identity-storage-provider.md).
> 
> Toto téma bylo aktualizováno pro ASP.NET Identity 2,0.
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Visual Studio 2013 s aktualizací Update 2
> - ASP.NET Identity 2

## <a name="introduction"></a>Úvod

Ve výchozím nastavení ukládá ASP.NET Identity systém informace o uživatelích do databáze SQL Server a k vytvoření databáze používá Entity Framework Code First. U mnoha aplikací funguje tento přístup dobře. Můžete ale chtít použít jiný typ trvalého mechanismu, jako je například Azure Table Storage, nebo už máte databázové tabulky s velmi odlišnou strukturou, než je výchozí implementace. V obou případech můžete napsat přizpůsobeného poskytovatele úložného mechanismu a připojit tohoto poskytovatele k vaší aplikaci.

ASP.NET Identity je ve výchozím nastavení součástí mnoha šablon Visual Studio 2013. Aktualizace ASP.NET Identity můžete získat prostřednictvím [balíčku Microsoft ASPNET identity EntityFramework NuGet](http://www.nuget.org/packages/Microsoft.AspNet.Identity.EntityFramework/).

Toto téma obsahuje následující oddíly:

- [Pochopení architektury](#architecture)
- [Pochopení dat, která jsou uložena](#data)
- [Vytvoření vrstvy přístupu k datům](#dal)
- [Přizpůsobení třídy uživatele](#user)
- [Přizpůsobení úložiště uživatele](#userstore)
- [Přizpůsobení třídy role](#role)
- [Přizpůsobení úložiště rolí](#rolestore)
- [Překonfigurujte aplikaci tak, aby používala nového poskytovatele úložiště.](#reconfigure)
- [Další implementace vlastních poskytovatelů úložiště](#other)

<a id="architecture"></a>
## <a name="understand-the-architecture"></a>Pochopení architektury

ASP.NET Identity se skládá ze tříd nazvaných manažeři a obchody. Správci jsou třídy vysoké úrovně, které vývojář aplikace používá k provádění operací, jako je například vytvoření uživatele, v systému ASP.NET Identity. Úložiště jsou třídy nižší úrovně, které určují, jak jsou trvalé entity, jako jsou uživatelé a role. Obchody jsou úzce spojeny s mechanismem trvalosti, ale manažeři jsou oddělené od úložišť, což znamená, že můžete nahradit mechanismus trvalosti bez přerušení celé aplikace.

Následující diagram znázorňuje, jak vaše webová aplikace komunikuje s manažery, a ukládá interakce s vrstvami přístupu k datům.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image1.png)

Chcete-li vytvořit přizpůsobeného poskytovatele úložiště pro ASP.NET Identity, je nutné vytvořit zdroj dat, vrstvu přístupu k datům a třídy úložiště, které pracují s touto vrstvou přístupu k datům. Můžete dál používat stejná rozhraní API správce k provádění operací s daty na uživateli, ale teď se data ukládají do jiného úložného systému.

Nemusíte přizpůsobovat třídy manažera, protože při vytváření nové instance UserManager nebo RoleManager poskytnete typ třídy uživatele a předá instanci třídy úložiště jako argument. Tento přístup umožňuje zapojit přizpůsobené třídy do existující struktury. Uvidíte, jak vytvořit instanci UserManager a RoleManager s přizpůsobenými třídami úložiště v oddílu [Změna konfigurace aplikace tak, aby používala nového poskytovatele úložiště](#reconfigure).

<a id="data"></a>
## <a name="understand-the-data-that-is-stored"></a>Pochopení dat, která jsou uložena

Chcete-li implementovat vlastního poskytovatele úložiště, je třeba pochopit typy dat používaných v ASP.NET Identity a rozhodnout, jaké funkce jsou relevantní pro vaši aplikaci.

| Data | Popis |
| --- | --- |
| Uživatelé | Registrovaní uživatelé vašeho webu. Zahrnuje ID uživatele a uživatelské jméno. Může zahrnovat heslo s algoritmem hash, pokud se uživatelé přihlašují pomocí přihlašovacích údajů, které jsou specifické pro vaši lokalitu (místo použití přihlašovacích údajů z externího webu, jako je Facebook), a bezpečnostní razítko, které určuje, jestli se v přihlašovacích údajích uživatele změnila. Může obsahovat taky e-mailovou adresu, telefonní číslo, to, jestli je povolené dvojúrovňové ověřování, aktuální počet neúspěšných přihlášení a údaj o tom, jestli je účet zamčený. |
| Deklarace identity uživatelů | Sada příkazů (nebo deklarací identity) o uživateli, který představuje identitu uživatele. Může povolit větší výraz identity uživatele, než je možné dosáhnout prostřednictvím rolí. |
| Přihlášení uživatelů | Informace o externím poskytovateli ověřování (jako Facebook), který se použije při přihlašování uživatele |
| Role | Skupiny autorizace pro váš web. Zahrnuje ID role a název role (například admin nebo zaměstnanec). |

<a id="dal"></a>
## <a name="create-the-data-access-layer"></a>Vytvoření vrstvy přístupu k datům

V tomto tématu se předpokládá, že jste obeznámeni s mechanismem trvalosti, který budete používat, a vytváření entit pro tento mechanismus. Toto téma neposkytuje podrobné informace o tom, jak vytvořit úložiště nebo třídy přístupu k datům. místo toho poskytuje některé návrhy na rozhodnutích o návrhu, která je potřeba udělat při práci s ASP.NET Identity.

Při navrhování úložišť pro vlastního poskytovatele úložiště máte spoustu volnosti. Stačí vytvořit úložiště pro funkce, které chcete v aplikaci použít. Pokud například v aplikaci nepoužíváte role, nemusíte vytvářet úložiště pro role nebo role uživatelů. Vaše technologie a stávající infrastruktura mohou vyžadovat strukturu, která se velmi liší od výchozí implementace ASP.NET Identity. Ve vrstvě pro přístup k datům poskytnete logiku pro práci se strukturou vašich úložišť.

Implementaci úložišť dat MySQL pro ASP.NET Identity 2,0 naleznete v tématu [MySQLIdentity. SQL](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql).

Ve vrstvě přístupu k datům poskytnete logiku pro uložení dat z ASP.NET Identity do zdroje dat. Vrstva přístupu k datům pro vlastního poskytovatele úložiště může obsahovat následující třídy pro ukládání informací o uživatelích a rolích.

| Třída | Popis | Příklad |
| --- | --- | --- |
| Kontext | Zapouzdřuje informace pro připojení k vašemu mechanismu trvalosti a provádění dotazů. Tato třída je střední až do vaší vrstvy přístupu k datům. Ostatní třídy dat budou vyžadovat, aby instance této třídy prováděla své operace. Vaše třídy úložiště se inicializují také instancí této třídy. | [MySQLDatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) |
| Uživatelské úložiště | Ukládá a načítá informace o uživateli (například uživatelské jméno a hodnota hash hesla). | [Uživatel (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) |
| Úložiště rolí | Ukládá a načítá informace o rolích (například název role). | [Role (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) |
| Úložiště UserClaims | Ukládá a načítá informace o deklaraci identity uživatele (například typ a hodnotu deklarace identity). | [UserClaimsTable (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) |
| Úložiště UserLogins | Ukládá a načítá přihlašovací informace uživatele (například externího poskytovatele ověřování). | [UserLoginsTable (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) |
| Úložiště položky UserRole | Ukládá a načítá, ke kterým rolím je uživatel přiřazen. | [UserRoleTable (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) |

Znovu stačí pouze implementovat třídy, které chcete použít ve své aplikaci.

Ve třídách pro přístup k datům poskytnete kód pro provádění operací s daty pro konkrétní mechanismus trvalosti. Například v rámci implementace MySQL obsahuje Třída User třídu metodu pro vložení nového záznamu do tabulky databáze uživatelé. Proměnná s názvem `_database` je instancí třídy MySQLDatabase.

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample1.cs)]

Po vytvoření třídy pro přístup k datům je nutné vytvořit třídy úložiště, které volají konkrétní metody ve vrstvě přístupu k datům.

<a id="user"></a>
## <a name="customize-the-user-class"></a>Přizpůsobení třídy uživatele

Při implementaci vlastního poskytovatele úložiště je nutné vytvořit třídu uživatele, která je ekvivalentní třídě [IdentityUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityuser(v=vs.108).aspx) v oboru názvů [Microsoft. ASP. NET. identity. EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx) :

Následující diagram znázorňuje třídu IdentityUser, kterou je nutné vytvořit a rozhraní pro implementaci v této třídě.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image2.png)

Rozhraní [&gt;IUser&lt;TKey](https://msdn.microsoft.com/library/dn613291(v=vs.108).aspx) definuje vlastnosti, které se UserManager pokusí zavolat při provádění požadovaných operací. Rozhraní obsahuje dvě vlastnosti – ID a uživatelské jméno. Rozhraní [&gt;IUser&lt;TKey](https://msdn.microsoft.com/library/dn613291(v=vs.108).aspx) umožňuje zadat typ klíče pro uživatele prostřednictvím obecného parametru **TKey** . Typ vlastnosti ID se shoduje s hodnotou parametru TKey.

Architektura identity také poskytuje rozhraní [IUser](https://msdn.microsoft.com/library/microsoft.aspnet.identity.iuser(v=vs.108).aspx) (bez obecného parametru), pokud chcete použít řetězcovou hodnotu pro klíč.

Třída IdentityUser implementuje IUser a obsahuje všechny další vlastnosti nebo konstruktory pro uživatele na vašem webu. Následující příklad ukazuje třídu IdentityUser, která používá celé číslo pro klíč. Pole ID je nastaveno na hodnotu **int** , aby odpovídala hodnotě obecného parametru. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample2.cs)]

 Úplnou implementaci najdete v tématu [IdentityUser (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs). 

<a id="userstore"></a>
## <a name="customize-the-user-store"></a>Přizpůsobení úložiště uživatele

Vytvoříte také třídu UserStore, která poskytuje metody pro všechny operace s daty na uživateli. Tato třída je ekvivalentní k třídě [UserStore&lt;TUser&gt;](https://msdn.microsoft.com/library/dn315446(v=vs.108).aspx) v oboru názvů [Microsoft. ASP. NET. identity. EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx) . Ve třídě UserStore implementujete [IUserStore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613276(v=vs.108).aspx) a kterékoli z volitelných rozhraní. Můžete vybrat, která volitelná rozhraní budou implementována na základě funkcí, které chcete poskytnout do aplikace.

Následující obrázek ukazuje třídu UserStore, kterou je nutné vytvořit, a relevantní rozhraní.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image3.png)

Výchozí šablona projektu v aplikaci Visual Studio obsahuje kód, který předpokládá, že mnoho volitelných rozhraní bylo implementováno v úložišti uživatele. Pokud používáte výchozí šablonu s přizpůsobeným uživatelským úložištěm, musíte buď implementovat volitelná rozhraní v úložišti uživatelů, nebo změnit kód šablony tak, aby již nevolal metody v rozhraních, které jste neimplementovali.

 Následující příklad ukazuje jednoduchou třídu úložiště uživatele. Obecný parametr **TUser** přebírá typ uživatelské třídy, což je obvykle třída IdentityUser, kterou jste definovali. Obecný parametr **TKey** přebírá typ vašeho uživatelského klíče. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample3.cs)]

 V tomto příkladu konstruktor, který přebírá parametr s názvem *databáze* typu ExampleDatabase, je pouze ilustrace, jak předat vaší třídu přístupu k datům. Například v implementaci MySQL tento konstruktor přijímá parametr typu MySQLDatabase. 

V rámci vaší třídy UserStore používáte třídy pro přístup k datům, které jste vytvořili k provádění operací. Například v implementaci MySQL má třída UserStore metodu CreateAsync, která používá instanci uživatele k vložení nového záznamu. Metoda **INSERT** objektu **User** je stejná jako metoda, která byla uvedena v předchozí části. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample4.cs)]

### <a name="interfaces-to-implement-when-customizing-user-store"></a>Rozhraní k implementaci při přizpůsobení úložiště uživatele

Další obrázek ukazuje více podrobností o funkcích definovaných v jednotlivých rozhraních. Všechna volitelná rozhraní dědí od IUserStore.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image4.png)

- **IUserStore**  
  Rozhraní [TKey&gt;IUserStore&lt;TUser](https://msdn.microsoft.com/library/dn613278(v=vs.108).aspx) je jediné rozhraní, které musíte implementovat do svého úložiště uživatele. Definuje metody pro vytváření, aktualizaci, odstraňování a načítání uživatelů.
- **IUserClaimStore**  
  Rozhraní [IUserClaimStore&lt;TUser, rozhraní TKey&gt;](https://msdn.microsoft.com/library/dn613265(v=vs.108).aspx) definuje metody, které je nutné implementovat do úložiště uživatele, aby bylo možné povolit deklarace identity uživatelů. Obsahuje metody nebo přidávání, odebírání a načítání deklarací identity uživatelů.
- **IUserLoginStore**  
  [IUserLoginStore&lt;TUser, TKey&gt;](https://msdn.microsoft.com/library/dn613272(v=vs.108).aspx) definuje metody, které je nutné implementovat do úložiště uživatele, aby bylo možné povolit externí poskytovatele ověřování. Obsahuje metody pro přidání, odebrání a načtení přihlášení uživatelů a metodu pro načtení uživatele na základě přihlašovacích údajů.
- **IUserRoleStore**  
  Rozhraní [IUserRoleStore&lt;TKey, rozhraní TUser&gt;](https://msdn.microsoft.com/library/dn613276(v=vs.108).aspx) definuje metody, které je nutné implementovat do vašeho úložiště uživatelů pro namapování uživatele na roli. Obsahuje metody pro přidání, odebrání a načtení rolí uživatele a metodu, která zkontroluje, jestli je uživatel přiřazený k roli.
- **IUserPasswordStore**  
  Rozhraní [IUserPasswordStore&lt;TUser, rozhraní TKey&gt;](https://msdn.microsoft.com/library/dn613273(v=vs.108).aspx) definuje metody, které je nutné implementovat do úložiště uživatele, aby trvaly hesla s hodnotou hash. Obsahuje metody pro získání a nastavení hash hesla a metodu, která označuje, jestli uživatel nastavil heslo.
- **IUserSecurityStampStore**  
  Rozhraní [IUserSecurityStampStore&lt;TUser, rozhraní TKey&gt;](https://msdn.microsoft.com/library/dn613277(v=vs.108).aspx) definuje metody, které je nutné implementovat do úložiště uživatele, aby bylo možné použít bezpečnostní razítko pro označení, zda se změnily informace o účtu uživatele. Toto razítko se aktualizuje, když uživatel změní heslo, nebo přidá nebo odebere přihlášení. Obsahuje metody pro získání a nastavení razítka zabezpečení.
- **IUserTwoFactorStore**  
  Rozhraní [IUserTwoFactorStore&lt;TUser, rozhraní TKey&gt;](https://msdn.microsoft.com/library/dn613279(v=vs.108).aspx) definuje metody, které je nutné implementovat pro implementaci dvou faktorů ověřování. Obsahuje metody pro získání a nastavení, zda je pro uživatele povoleno dvojúrovňové ověřování.
- **IUserPhoneNumberStore**  
  Rozhraní [IUserPhoneNumberStore&lt;TUser, rozhraní TKey&gt;](https://msdn.microsoft.com/library/dn613275(v=vs.108).aspx) definuje metody, které je nutné implementovat pro ukládání uživatelských telefonních čísel. Obsahuje metody pro získání a nastavení telefonního čísla a zda je telefonní číslo potvrzené.
- **IUserEmailStore**  
  Rozhraní [IUserEmailStore&lt;TUser, rozhraní TKey&gt;](https://msdn.microsoft.com/library/dn613143(v=vs.108).aspx) definuje metody, které je nutné implementovat pro ukládání e-mailových adres uživatele. Obsahuje metody pro získání a nastavení e-mailové adresy a toho, jestli se e-mail potvrdí.
- **IUserLockoutStore**  
  Rozhraní [IUserLockoutStore&lt;TUser, rozhraní TKey&gt;](https://msdn.microsoft.com/library/dn613271(v=vs.108).aspx) definuje metody, které je nutné implementovat pro ukládání informací o zamykání účtu. Obsahuje metody pro získání aktuálního počtu neúspěšných pokusů o přístup, získání a nastavení, zda je možné účet uzamknout, získat a nastavit koncové datum zámku, zvýšit počet neúspěšných pokusů a resetovat počet neúspěšných pokusů.
- **IQueryableUserStore**  
  Rozhraní [IQueryableUserStore&lt;TUser, rozhraní TKey&gt;](https://msdn.microsoft.com/library/dn613267(v=vs.108).aspx) definuje členy, které musíte implementovat k poskytnutí Queryable úložiště uživatele. Obsahuje vlastnost, která obsahuje uživatele Queryable.

  Implementujete rozhraní, která jsou potřebná v aplikaci. například rozhraní IUserClaimStore, IUserLoginStore, IUserRoleStore, IUserPasswordStore a IUserSecurityStampStore, jak je znázorněno níže. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample5.cs)]

Úplnou implementaci (včetně všech rozhraní) najdete v tématu [UserStore (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs).

### <a name="identityuserclaim-identityuserlogin-and-identityuserrole"></a>IdentityUserClaim, IdentityUserLogin a IdentityUserRole

Obor názvů Microsoft. AspNet. identity. EntityFramework obsahuje implementace tříd [IdentityUserClaim](https://msdn.microsoft.com/library/dn613250(v=vs.108).aspx), [IdentityUserLogin](https://msdn.microsoft.com/library/dn613251(v=vs.108).aspx)a [IdentityUserRole](https://msdn.microsoft.com/library/dn613252(v=vs.108).aspx) . Pokud používáte tyto funkce, můžete chtít vytvořit vlastní verze těchto tříd a definovat vlastnosti pro aplikaci. V některých případech je ale při provádění základních operací (například přidání nebo odebrání deklarace identity uživatele) efektivnější tyto entity nečítat do paměti. Místo toho mohou třídy úložiště back-end provádět tyto operace přímo na zdroji dat. Například metoda UserStore. GetClaimsAsync () může volat metodu userClaimTable. FindByUserId (uživatel. ID) pro provedení dotazu přímo v této tabulce a vrácení seznamu deklarací identity.

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample6.cs)]

<a id="role"></a>
## <a name="customize-the-role-class"></a>Přizpůsobení třídy role

Při implementaci vlastního poskytovatele úložiště je nutné vytvořit třídu role, která je ekvivalentní třídě [IdentityRole](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework.identityrole(v=vs.108).aspx) v oboru názvů [Microsoft. ASP. NET. identity. EntityFramework](https://msdn.microsoft.com/library/microsoft.aspnet.identity.entityframework(v=vs.108).aspx) :

Následující diagram znázorňuje třídu IdentityRole, kterou je nutné vytvořit a rozhraní pro implementaci v této třídě.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image5.png)

Rozhraní [&gt;IRole&lt;TKey](https://msdn.microsoft.com/library/dn613268(v=vs.108).aspx) definuje vlastnosti, které se roleManager pokusí zavolat při provádění požadovaných operací. Rozhraní obsahuje dvě vlastnosti – ID a název. Rozhraní [&gt;IRole&lt;TKey](https://msdn.microsoft.com/library/dn613268(v=vs.108).aspx) umožňuje zadat typ klíče pro roli pomocí obecného parametru **TKey** . Typ vlastnosti ID se shoduje s hodnotou parametru TKey.

Architektura identity také poskytuje rozhraní [IRole](https://msdn.microsoft.com/library/microsoft.aspnet.identity.irole(v=vs.108).aspx) (bez obecného parametru), pokud chcete použít řetězcovou hodnotu pro klíč.

Následující příklad ukazuje třídu IdentityRole, která používá celé číslo pro klíč. Pole ID je nastaveno na hodnotu int, aby odpovídala hodnotě obecného parametru. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample7.cs)]

 Úplnou implementaci najdete v tématu [IdentityRole (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs). 

<a id="rolestore"></a>
## <a name="customize-the-role-store"></a>Přizpůsobení úložiště rolí

Vytvoříte také třídu RoleStore, která poskytuje metody pro všechny operace s daty v rolích. Tato třída je ekvivalentní k třídě [RoleStore&lt;TRole&gt;](https://msdn.microsoft.com/library/dn468181(v=vs.108).aspx) v oboru názvů Microsoft. ASP. NET. identity. EntityFramework. Ve třídě RoleStore implementujete [IRoleStore&lt;TRole, TKey&gt;](https://msdn.microsoft.com/library/dn613266(v=vs.108).aspx) a případně [IQueryableRoleStore&lt;TRole, TKey&gt;](https://msdn.microsoft.com/library/dn613262(v=vs.108).aspx) rozhraní.

![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image6.png)

Následující příklad ukazuje třídu úložiště role. Obecný parametr TRole přebírá typ vaší třídy role, což je obvykle třída IdentityRole, kterou jste definovali. Obecný parametr TKey přebírá typ klíče role. 

[!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample8.cs)]

- **IRoleStore&lt;TRole&gt;**  
  Rozhraní [IRoleStore](https://msdn.microsoft.com/library/dn468195.aspx) definuje metody, které se mají implementovat do vaší třídy úložiště rolí. Obsahuje metody pro vytváření, aktualizaci, odstraňování a načítání rolí.
- **RoleStore&lt;TRole&gt;**  
  Chcete-li přizpůsobit RoleStore, vytvořte třídu, která implementuje rozhraní IRoleStore. Tuto třídu je nutné implementovat pouze v případě, že chcete použít role v systému. Konstruktor, který přebírá parametr pojmenovaný *databáze* typu ExampleDatabase, je pouze ilustrací toho, jak předat do vaší třídy přístupu k datům. Například v implementaci MySQL tento konstruktor přijímá parametr typu MySQLDatabase.  
  
  Úplnou implementaci najdete v tématu [RoleStore (MySQL)](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) .

<a id="reconfigure"></a>
## <a name="reconfigure-application-to-use-new-storage-provider"></a>Překonfigurujte aplikaci tak, aby používala nového poskytovatele úložiště.

Implementovali jste nového poskytovatele úložiště. Teď musíte aplikaci nakonfigurovat tak, aby používala tohoto poskytovatele úložiště. Pokud byl do projektu přidán výchozí zprostředkovatel úložiště, je nutné odebrat výchozího zprostředkovatele a nahradit ho vaším poskytovatelem.

### <a name="replace-default-storage-provider-in-mvc-project"></a>Nahradit výchozího poskytovatele úložiště v projektu MVC

1. V okně **Spravovat balíčky NuGet** odinstalujte balíček **Microsoft ASP.NET identity EntityFramework** . Tento balíček můžete najít tak, že vyhledáte nainstalované balíčky identity. EntityFramework.  
    ![](overview-of-custom-storage-providers-for-aspnet-identity/_static/image7.png) se zobrazí dotaz, jestli chcete Entity Framework odinstalovat. Pokud ho nepotřebujete v jiných částech aplikace, můžete ho odinstalovat.
2. V souboru IdentityModels.cs ve složce modely odstraňte nebo pokomentujte třídy **ApplicationUser** a **ApplicationDbContext** . V aplikaci MVC můžete odstranit celý soubor IdentityModels.cs. V aplikaci webových formulářů odstraňte tyto dvě třídy, ale ujistěte se, že jste zachovali pomocnou třídu, která je také umístěna v souboru IdentityModels.cs.
3. Pokud se poskytovatel úložiště nachází v samostatném projektu, přidejte na něj odkaz ve vaší webové aplikaci.
4. Nahraďte všechny odkazy na `using Microsoft.AspNet.Identity.EntityFramework;` pomocí příkazu Using pro obor názvů vašeho poskytovatele úložiště.
5. Ve třídě **Startup.auth.cs** změňte metodu **ConfigureAuth** tak, aby používala jednu instanci příslušného kontextu. 

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample9.cs?highlight=3)]
6. Ve složce App\_Start otevřete složku **IdentityConfig.cs**. Ve třídě ApplicationUserManager změňte metodu **Create** tak, aby vracela správce uživatele, který používá vlastní uživatelské úložiště. 

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample10.cs?highlight=3)]
7. Nahraďte všechny odkazy na **ApplicationUser** pomocí **IdentityUser**.
8. Výchozí projekt obsahuje některé členy třídy User, které nejsou definovány v rozhraní IUser; například e-maily, PasswordHash a GenerateUserIdentityAsync. Pokud vaše třída uživatele nemá tyto členy, je nutné je buď implementovat, nebo změnit kód, který používá tyto členy.
9. Pokud jste vytvořili nějaké instance nástroje RoleManager, změňte kód tak, aby používal novou třídu RoleStore.  

    [!code-csharp[Main](overview-of-custom-storage-providers-for-aspnet-identity/samples/sample11.cs)]
10. Výchozí projekt je navržen pro třídu uživatele, která má řetězcovou hodnotu pro klíč. Pokud má vaše třída uživatele pro klíč jiný typ (například celé číslo), musíte změnit projekt tak, aby fungoval s vaším typem. Přečtěte si téma [Změna primárního klíče pro uživatele v ASP.NET identity](change-primary-key-for-users-in-aspnet-identity.md).
11. V případě potřeby přidejte připojovací řetězec do souboru Web. config.

<a id="other"></a>
## <a name="other-resources"></a>Další prostředky

- Blog: [implementace ASP.NET identity](http://odetocode.com/blogs/scott/archive/2014/01/20/implementing-asp-net-identity.aspx)
- Kurz a kód GIT: [Simple. Data ASP.NET identity provider](http://designcoderelease.blogspot.co.uk/2015/03/simpledata-aspnet-identity-provider.html)
- Kurz:[nastavení základních účtů identit a jejich nasměrování do externí databáze](http://typecastexception.com/post/2013/10/27/Configuring-Db-Connection-and-Code-First-Migration-for-Identity-Accounts-in-ASPNET-MVC-5-and-Visual-Studio-2013.aspx). [@xivSolutions](https://twitter.com/xivSolutions).
- Kurz[: implementace vlastního poskytovatele úložiště ASP.NET identity MySQL](implementing-a-custom-mysql-aspnet-identity-storage-provider.md)
- [Entity CodeFluent](http://blog.codefluententities.com/2014/04/30/asp-net-identity-v2-and-codefluent-entities/) podle [SoftFluent](http://www.softfluent.com/)
- [Azure Table Storage](https://www.nuget.org/packages/accidentalfish.aspnet.identity.azure/) od James Randall.
- Azure Table Storage: [ASPNET. identity. TableStorage](https://github.com/stuartleeks/leeksnet.AspNet.Identity.TableStorage) podle [@stuartleeks](https://twitter.com/stuartleeks).
- [CouchDB/Cloud podle Daniel Wertheim.](https://github.com/danielwertheim/mycouch.aspnet.identity)
- Elastická ledat[h: elastická identita](https://github.com/bmbsqd/elastic-identity) podle Bombsquad AB.
- [MongoDB](http://www.nuget.org/packages/MongoDB.AspNet.Identity/) podle Jonathana Sheely Jonathana Sheely.
- [NHibernate. ASPNET. identity](https://github.com/milesibastos/NHibernate.AspNet.Identity) podle Antônio mil. Bastos.
- [RavenDB](http://www.nuget.org/packages/AspNet.Identity.RavenDB/1.0.0) podle [@tourismgeek](https://twitter.com/tourismgeek).
- [RavenDB. ASPNET. identity](https://github.com/ILMServices/RavenDB.AspNet.Identity) podle [ILMServices](http://www.ilmservice.com/).
- Redis: [Redis. ASPNET. identity](https://github.com/aminjam/Redis.AspNet.Identity)
- Šablony T4 pro generování kódu EF pro "první" databázi úložiště uživatele: [ASPNET. identity. EntityFramework](https://github.com/cbfrank/AspNet.Identity.EntityFramework)

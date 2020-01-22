---
uid: identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity
title: Migrace existujícího webu z členství SQL do ASP.NET Identity-ASP.NET 4. x
author: Rick-Anderson
description: Tento kurz znázorňuje postup migrace stávající webové aplikace s daty uživatelů a rolí vytvořenými pomocí členství SQL pro nové ASP.NET Identity s...
ms.author: riande
ms.date: 12/19/2014
ms.custom: seoapril2019
ms.assetid: 220d3d75-16b2-4240-beae-a5b534f06419
msc.legacyurl: /identity/overview/migrations/migrating-an-existing-website-from-sql-membership-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: eacfbb8a5b2d1aa3678892bc2077a56185fdebbc
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519151"
---
# <a name="migrating-an-existing-website-from-sql-membership-to-aspnet-identity"></a>Migrace stávajícího webu z členství SQL na ASP.NET Identity

[Rick Anderson]((https://twitter.com/RickAndMSFT)), [Suhas Joshi](https://github.com/suhasj)

> Tento kurz znázorňuje postup migrace stávající webové aplikace s daty uživatelů a rolí vytvořenými pomocí členství SQL do nového systému ASP.NET Identity. Tento přístup zahrnuje změnu existujícího schématu databáze na ten, který vyžaduje ASP.NET Identity a jeho zapojení do starých a nových tříd. Po přijetí tohoto přístupu se po migraci databáze budou moci budoucí aktualizace identity považovat za snadnou.

Pro tento kurz budeme pořizovat šablonu webové aplikace (webové formuláře) vytvořené pomocí sady Visual Studio 2010 k vytvoření dat uživatelů a rolí. Pak použijeme skripty SQL k migraci existující databáze do tabulek, které potřebuje systém identit. V dalším kroku nainstalujeme potřebné balíčky NuGet a přidáte nové stránky správy účtů, které používají systém identit pro správu členství. Jako test migrace by se uživatelé, kteří vytvořili pomocí členství SQL, měli být schopni přihlásit a noví uživatelé by měli být schopni se zaregistrovat. Kompletní ukázku najdete [tady](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/). Viz také [migrace z ASP.NET členství na ASP.NET identity](http://travis.io/blog/2015/03/24/migrate-from-aspnet-membership-to-aspnet-identity.html).

## <a name="getting-started"></a>Začínáme

### <a name="creating-an-application-with-sql-membership"></a>Vytvoření aplikace pomocí členství SQL

1. Musíme začít se stávající aplikací, která používá členství SQL, a má data uživatelů a rolí. Pro účely tohoto článku vytvoříme webovou aplikaci v aplikaci Visual Studio 2010.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image1.jpg)
2. Pomocí nástroje pro konfiguraci ASP.NET vytvořte 2 uživatele: **oldAdminUser** a **oldUser.**

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image1.png)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image2.jpg)
3. Vytvořte roli s názvem admin a jako uživatele v této roli přidejte ' oldAdminUser '.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image2.png)
4. Vytvoří v lokalitě oddíl admin s výchozím. aspx. Nastavte autorizační značku v souboru Web. config tak, aby byl přístup povolen pouze uživatelům v rolích správce. Další informace najdete tady [https://www.asp.net/web-forms/tutorials/security/roles/role-based-authorization-cs](../../../web-forms/overview/older-versions-security/roles/role-based-authorization-cs.md)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image3.png)
5. Zobrazte si databázi v Průzkumník serveru, abyste pochopili tabulky vytvořené systémem SQL Membership. Přihlašovací údaje uživatele se ukládají do tabulek ASPNET\_Users a ASPNET\_, zatímco data role jsou uložená v tabulce rolí ASPNET\_. Informace o tom, na kterých uživatelích jsou role uložené v tabulce ASPNET\_UsersInRoles. Pro základní správu členství je dostačující k tomu, aby se informace ve výše uvedených tabulkách nastavoval do ASP.NET Identity systému.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image4.png)

### <a name="migrating-to-visual-studio-2013"></a>Migrace na Visual Studio 2013

1. Nainstalujte Visual Studio Express 2013 pro web nebo Visual Studio 2013 spolu s [nejnovějšími aktualizacemi](https://www.microsoft.com/download/details.aspx?id=44921).
2. Otevřete výše uvedený projekt ve vaší nainstalované verzi sady Visual Studio. Pokud na počítači není nainstalováno SQL Server Express, při otevření projektu se zobrazí výzva, protože připojovací řetězec používá SQL Express. Můžete buď nainstalovat SQL Express, nebo jak chcete, aby se připojovací řetězec změnil na LocalDb. V tomto článku se změní na LocalDb.
3. Otevřete soubor Web. config a změňte připojovací řetězec z. SQLExpress na (LocalDb) v 11.0. Odebere z připojovacího řetězce "User Instance = true".

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image3.jpg)
4. Otevřete Průzkumník serveru a ověřte, že je možné pozorovat schéma a data tabulky.
5. ASP.NET Identity systém funguje s verzí 4,5 nebo vyšší. Změnit cíl aplikace na 4,5 nebo vyšší.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image5.png)

    Sestavte projekt, abyste ověřili, že nejsou k dispozici žádné chyby.

### <a name="installing-the-nuget-packages"></a>Instalace balíčků NuGet

1. V Průzkumník řešení klikněte pravým tlačítkem na projekt &gt; **Spravovat balíčky NuGet**. Do vyhledávacího pole zadejte "Asp.net identity". V seznamu výsledků vyberte balíček a klikněte na nainstalovat. Přijměte licenční smlouvu kliknutím na tlačítko Souhlasím. Všimněte si, že tento balíček nainstaluje balíčky závislostí: EntityFramework a Microsoft ASP.NET identity Core. Obdobně nainstalujte následující balíčky (Pokud nechcete povolit přihlášení k protokolu OAuth, přeskočte poslední 4 balíčky OWIN):

   - Microsoft.AspNet.Identity.Owin
   - Microsoft.Owin.Host.SystemWeb
   - Microsoft.Owin.Security.Facebook
   - Microsoft.Owin.Security.Google
   - Microsoft.Owin.Security.MicrosoftAccount
   - Microsoft.Owin.Security.Twitter

     ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image6.png)

### <a name="migrate-database-to-the-new-identity-system"></a>Migrace databáze do nového systému identity

Dalším krokem je migrace stávající databáze do schématu, které vyžaduje systém ASP.NET Identity. Abychom to dosáhli, spusťte skript SQL, který obsahuje sadu příkazů pro vytvoření nových tabulek a migraci stávajících uživatelských informací do nových tabulek. Soubor skriptu najdete [tady](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/Migrations.sql).

Tento soubor skriptu je specifický pro tuto ukázku. Pokud je schéma pro tabulky vytvořené pomocí členství SQL upraveno nebo upraveno, musí být skripty odpovídajícím způsobem změněny.

### <a name="how-to-generate-the-sql-script-for-schema-migration"></a>Generování skriptu SQL pro migraci schématu

Aby ASP.NET Identity třídy fungovaly s daty stávajících uživatelů, musíme migrovat schéma databáze k tomu, které vyžaduje ASP.NET Identity. To můžeme udělat přidáním nových tabulek a zkopírováním existujících informací do těchto tabulek. Ve výchozím nastavení ASP.NET Identity používá EntityFramework k namapování tříd modelu identity zpět do databáze pro ukládání a načítání informací. Tyto třídy modelů implementují základní rozhraní identity definující objekty uživatelů a rolí. Tabulky a sloupce v databázi jsou založeny na těchto třídách modelu. Třídy modelu EntityFramework v identity v 2.1.0 a jejich vlastnosti jsou definované níže.

| **IdentityUser** | **Typ** | **IdentityRole** | **IdentityUserRole** | **IdentityUserLogin** | **IdentityUserClaim** |
| --- | --- | --- | --- | --- | --- |
| Id | odkazy řetězců | Id | roleId | ProviderKey | Id |
| Uživatelské jméno | odkazy řetězců | Name | UserId | UserId | ClaimType |
| PasswordHash (Hodnota hash hesla) | odkazy řetězců |  |  | LoginProvider | ClaimValue |
| SecurityStamp | odkazy řetězců |  |  |  | ID\_uživatele |
| E-mail | odkazy řetězců |  |  |  |  |
| EmailConfirmed | bool |  |  |  |  |
| PhoneNumber | odkazy řetězců |  |  |  |  |
| PhoneNumberConfirmed | bool |  |  |  |  |
| LockoutEnabled | bool |  |  |  |  |
| LockoutEndDate | Datum a čas |  |  |  |  |
| AccessFailedCount | int |  |  |  |  |

Pro každý z těchto modelů musíme mít tabulky, které odpovídají vlastnostem. Mapování mezi třídami a tabulkami je definováno v metodě `OnModelCreating` `IdentityDBContext`. To se označuje jako metoda konfigurace rozhraní Fluent API a další informace najdete [tady](https://msdn.microsoft.com/data/jj591617.aspx). Konfigurace pro třídy je uvedená níže.

| **Třída** | **Tabulka** | **Primární klíč** | **Cizí klíč** |
| --- | --- | --- | --- |
| IdentityUser | AspnetUsers | Id |  |
| IdentityRole | AspnetRoles | Id |  |
| IdentityUserRole | AspnetUserRole | UserId + RoleId | User\_ID-&gt;AspnetUsers RoleId-&gt;AspnetRoles |
| IdentityUserLogin | AspnetUserLogins | ProviderKey + UserId + LoginProvider | UserId-&gt;AspnetUsers |
| IdentityUserClaim | AspnetUserClaims | Id | User\_Id-&gt;AspnetUsers |

S těmito informacemi můžeme vytvořit příkazy SQL pro vytváření nových tabulek. Každý příkaz můžeme buď zapsat jednotlivě, nebo můžete celý skript vygenerovat pomocí příkazů PowerShellu EntityFramework, které můžeme následně upravit podle potřeby. Provedete to tak, že v sadě VS otevřete **konzolu Správce balíčků** z nabídky zobrazení nebo **nástroje** **.**

- Spuštěním příkazu "Enable-migrations" Povolte migrace EntityFramework.
- Spusťte příkaz "Add-Migration Initial", který vytvoří počáteční kód instalace pro vytvoření databáze v C#/VB.
- Posledním krokem je spuštění příkazu "Update-Database – Script", který generuje skript SQL na základě tříd modelu.

[!INCLUDE[](../../../includes/identity/alter-command-exception.md)]

Tento skript generování databáze se dá použít jako začátek, kde budeme provádět další změny, abyste mohli přidávat nové sloupce a kopírovat data. Výhodou tohoto je, že generujeme `_MigrationHistory` tabulku, kterou používá EntityFramework ke změně schématu databáze, když se třídy modelu mění v budoucích verzích verzí identity.

Informace o uživatelích členů SQL obsahovaly kromě těch, které se nacházejí ve třídě User model identity, konkrétně e-mail, pokusy o zadání hesla, datum posledního přihlášení, datum posledního uzamčení a další, další vlastnosti. To jsou užitečné informace a chceme, aby se přenesly do systému identit. To se dá udělat přidáním dalších vlastností do uživatelského modelu a jejich mapováním zpátky na sloupce tabulky v databázi. To můžeme udělat přidáním třídy, která podtřídí model `IdentityUser`. Do této vlastní třídy můžeme přidat vlastnosti a upravit skript SQL, aby se při vytváření tabulky přidaly odpovídající sloupce. Kód pro tuto třídu je podrobněji popsán v článku. Skript SQL pro vytvoření tabulky `AspnetUsers` po přidání nových vlastností by byl

[!code-sql[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample1.sql)]

Dál musíme zkopírovat existující informace z databáze členství SQL do nově přidaných tabulek pro identitu. To lze provést prostřednictvím SQL kopírováním dat přímo z jedné tabulky do druhé. Chcete-li přidat data do řádků tabulky, používáme konstrukci `INSERT INTO [Table]`. K kopírování z jiné tabulky můžeme použít příkaz `INSERT INTO` spolu s příkazem `SELECT`. Chcete-li získat všechny informace o uživateli, je nutné zadat dotaz na tabulku členství *aspnet\_Users* a *ASPNET\_* a zkopírovat data do tabulky *AspNetUsers* . Používáme `INSERT INTO` a `SELECT` spolu s příkazy `JOIN` a `LEFT OUTER JOIN`. Další informace o dotazování a kopírování dat mezi tabulkami najdete v [tomto](https://technet.microsoft.com/library/ms190750%28v=sql.105%29.aspx) odkazu. Tabulky AspnetUserLogins a AspnetUserClaims jsou navíc prázdné, aby začínaly, protože v členství SQL nejsou žádné informace, které jsou ve výchozím nastavení namapovány. Jediné zkopírované informace jsou pro uživatele a role. Pro projekt vytvořený v předchozích krocích bude dotaz SQL na kopírování informací do tabulky uživatelů

[!code-sql[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample2.sql)]

Ve výše uvedeném příkazu SQL se informace o jednotlivých uživatelích z tabulek *aspnet\_Users* a *ASPNET\_* zkopírují do sloupců tabulky *AspnetUsers* . Jediná úprava, kterou tady provedeme, je, že jsme heslo zkopírovali. Vzhledem k tomu, že šifrovací algoritmus pro hesla ve členství SQL použil ' PasswordSalt ' a ' PasswordFormat ', zkopírujeme to příliš společně s heslem hash, aby bylo možné použít k dešifrování hesla podle identity. To je vysvětleno dále v článku při zapojování vlastního algoritmu hash hesla.

Tento soubor skriptu je specifický pro tuto ukázku. Pro aplikace, které mají další tabulky, mohou vývojáři použít podobný přístup k přidání dalších vlastností třídy uživatelského modelu a jejich mapování na sloupce v tabulce AspnetUsers. Chcete-li spustit skript,

1. Otevřete Průzkumník serveru. Rozbalte připojení ApplicationServices pro zobrazení tabulek. Klikněte pravým tlačítkem na uzel tabulky a vyberte možnost Nový dotaz.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image7.png)
2. V okně dotazu zkopírujte a vložte celý skript SQL z souboru migrations. SQL. Spusťte soubor skriptu tak, že kliknete na tlačítko se šipkou ' spustit '.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image4.jpg)

    Aktualizujte okno Průzkumník serveru. V databázi se vytvoří pět nových tabulek.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image8.png)

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image9.png)

    Níže je uveden způsob, jakým jsou informace v tabulkách členství SQL namapovány na nový systém identity.

    Role ASPNET\_–&gt; AspNetRoles

    ASP\_netUsers a ASP\_netMembership--&gt; AspNetUsers

    aspnet\_UserInRoles --&gt; AspNetUserRoles

    Jak je vysvětleno výše v části, tabulky AspNetUserClaims a AspNetUserLogins jsou prázdné. Pole diskriminátor v tabulce AspNetUser by se mělo shodovat s názvem třídy modelu, který je definován jako další krok. Sloupec PasswordHash je také ve formátu "šifrované heslo | heslo Salt | formát hesla". To vám umožňuje používat speciální logiku šifrování členství SQL, abyste mohli znovu použít stará hesla. To je vysvětleno v části dále v tomto článku.

### <a name="creating-models-and-membership-pages"></a>Vytváření modelů a stránek členství

Jak bylo zmíněno dříve, funkce identita používá Entity Framework ke komunikaci s databází pro ukládání informací o účtu ve výchozím nastavení. Abychom mohli pracovat se stávajícími daty v tabulce, musíme vytvořit třídy modelů, které se mapují zpátky na tabulky a zapojte je do systému identit. V rámci kontraktu identity by třídy modelu měly buď implementovat rozhraní definovaná v knihovně DLL identity. Core, nebo mohou roztáhnout stávající implementaci těchto rozhraní, která jsou k dispozici v souboru Microsoft. AspNet. identity. EntityFramework.

V naší ukázce mají tabulky AspNetRoles, AspNetUserClaims, AspNetLogins a AspNetUserRole sloupce podobné stávající implementaci systému identity. Proto můžeme znovu použít existující třídy pro mapování na tyto tabulky. Tabulka AspNetUser obsahuje několik dalších sloupců, které se používají k ukládání dalších informací z tabulek členství SQL. To lze namapovat vytvořením třídy modelu, která rozšiřuje stávající implementaci ' IdentityUser ' a přidání dalších vlastností.

1. Vytvořte v projektu složku modelů a přidejte uživatele třídy. Název třídy by měl odpovídat datům přidaným do sloupce ' diskriminátor ' tabulky ' AspnetUsers '.

    ![](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/_static/image10.png)

    Třída User by měla rozšířenou třídu IdentityUser, která se nachází v knihovně DLL *Microsoft. ASPNET. identity. EntityFramework* . Deklarujete vlastnosti třídy, které se mapují zpátky na sloupce AspNetUser. Vlastnosti ID, UserName, PasswordHash a SecurityStamp jsou definovány v IdentityUser a jsou proto vynechány. Níže je uvedený kód pro třídu uživatele, která má všechny vlastnosti.

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample3.cs)]
2. Aby bylo možné uchovávat data v modelech zpět do tabulek a načítat data z tabulek, aby bylo možné naplnit modely, je nutné Entity Framework třídu DbContext. Knihovna DLL *Microsoft. ASPNET. identity. EntityFramework* definuje třídu IdentityDbContext, která komunikuje s tabulkami identity pro načítání a ukládání informací. &gt; IdentityDbContext&lt;tuser převezme třídu TUser, která může být libovolná třída, která rozšiřuje třídu IdentityUser.

    Vytvořte novou třídu ApplicationDBContext, která rozšíří IdentityDbContext do složky Models a předává třídu "User" vytvořenou v kroku 1.

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample4.cs)]
3. Správa uživatelů v novém systému identit se provádí pomocí&gt; třídy UserManager&lt;tuser definované v knihovně DLL *Microsoft. ASPNET. identity. EntityFramework* . Musíme vytvořit vlastní třídu, která rozšiřuje UserManager, a předat ji do třídy "User" vytvořené v kroku 1.

    Ve složce modely vytvořte novou třídu UserManager, která rozšiřuje UserManager&lt;User&gt;

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample5.cs)]
4. Hesla uživatelů aplikace jsou zašifrovaná a uložená v databázi. Šifrovací algoritmus používaný v členství SQL se liší od verze v novém systému identity. Aby bylo možné znovu použít stará hesla, potřebujeme selektivně dešifrovat hesla, když se uživatelé přihlásí pomocí algoritmu členství SQL a používají šifrovací algoritmus v identitě pro nové uživatele.

    Třída UserManager má vlastnost PasswordHasher, která ukládá instanci třídy, která implementuje rozhraní IPasswordHasher. Slouží k šifrování/dešifrování hesel během transakcí ověřování uživatelů. Ve třídě UserManager definované v kroku 3 vytvořte novou třídu SQLPasswordHasher a zkopírujte následující kód.

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample6.cs)]

    Vyřešte chyby při kompilaci importem oborů názvů System. text a System. Security. Cryptography.

    Metoda EncodePassword šifruje heslo podle výchozí implementace kryptografie členství SQL. To se provádí z knihovny DLL System. Web. Pokud se stará aplikace použila vlastní implementace, měla by se projevit zde. Musíme definovat dvě další metody *HashPassword* a *VerifyHashedPassword* , které používají metodu *EncodePassword* pro hash a dané heslo, nebo ověřit heslo ve formátu prostého textu s existujícím v databázi.

    Systém členství SQL, který používá PasswordHash, PasswordSalt a PasswordFormat k hash hesla zadaného uživateli při registraci nebo změně hesla. Během migrace se všechna tři pole ukládají do sloupce PasswordHash v tabulce AspNetUser oddělené znakem |. Když se uživatel přihlásí a heslo obsahuje tato pole, používáme ke kontrole hesla šifrování členství SQL. v opačném případě používáme k ověření hesla výchozí šifrování systému identit. Tímto způsobem by staré uživatele po migraci aplikace nemuseli měnit svá hesla.
5. Deklarujte konstruktor pro třídu UserManager a předejte ji jako SQLPasswordHasher do vlastnosti v konstruktoru.

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample7.cs)]

### <a name="create-new-account-management-pages"></a>Vytvořit nové stránky pro správu účtů

Dalším krokem migrace je přidání stránek správy účtů, které umožní uživateli registraci a přihlášení. Původní stránky účtu z členství v SQL používají ovládací prvky, které nefungují s novým systémem identity. Chcete-li přidat nové stránky správy uživatelů, postupujte podle kurzu na tomto odkazu [https://www.asp.net/identity/overview/getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project](../getting-started/adding-aspnet-identity-to-an-empty-or-existing-web-forms-project.md) počínaje krokem "Přidání webových formulářů pro registraci uživatelů do vaší aplikace", protože už jsme vytvořili projekt a přidali jsme balíčky NuGet.

Musíme udělat nějaké změny, aby ukázka pracovala s projektem, který tady máme.

- Register.aspx.cs a Login.aspx.cs kód na pozadí tříd používají `UserManager` z balíčků identity k vytvoření uživatele. V tomto příkladu použijte UserManager přidaný do složky modely pomocí postupu uvedeného výše.
- Použijte třídu uživatele vytvořenou místo IdentityUser v kódu Register.aspx.cs a Login.aspx.cs za třídy. Tato zapojování v naší vlastní třídě uživatele do systému identity.
- Součást pro vytvoření databáze může být vynechána.
- Vývojář musí nastavit ApplicationId pro nového uživatele tak, aby odpovídal aktuálnímu ID aplikace. To lze provést dotazem na ApplicationId pro tuto aplikaci před vytvořením objektu uživatele ve třídě Register.aspx.cs a jeho nastavením před vytvořením uživatele.

    Příklad:

    Definujte metodu na stránce Register.aspx.cs pro dotaz na tabulku ASPNET\_Applications a Získejte ID aplikace podle názvu aplikace.

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample8.cs)]

    Teď to nastavte u objektu User.

    [!code-csharp[Main](migrating-an-existing-website-from-sql-membership-to-aspnet-identity/samples/sample9.cs)]

K přihlášení stávajícího uživatele použijte staré uživatelské jméno a heslo. Pomocí stránky registrace vytvořte nového uživatele. Ověřte také, že uživatelé jsou v rolích podle očekávání.

Přenos do systému identit pomáhá uživateli přidat do aplikace otevřené ověřování (OAuth). Další informace najdete [tady](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/SQLMembership-Identity-OWIN/) v ukázce s povoleným protokolem OAuth.

## <a name="next-steps"></a>Další kroky

V tomto kurzu jsme ukázali, jak na základě členství v SQL serveru přiASP.NET Identity, ale nedostali jsme data profilu portu. V dalším kurzu se podíváme na přenos dat profilu z členství SQL do nového systému identit.

Zpětnou vazbu můžete vynechávat na konci tohoto článku.

*Děkujeme Dykstra a Rick Anderson pro kontrolu článku.*

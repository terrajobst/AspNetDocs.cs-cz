---
uid: identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
title: Implementace vlastního poskytovatele úložiště ASP.NET Identity MySQL – ASP.NET 4. x
author: raquelsa
description: ASP.NET Identity je rozšiřitelný systém, který umožňuje vytvořit vlastního poskytovatele úložiště a zapojit ho do aplikace bez nutnosti znovu pracovat s aplikace...
ms.author: riande
ms.date: 05/22/2015
ms.assetid: 248f5fe7-39ba-40ea-ab1e-71a69b0bd649
ms.custom: seoapril2019
msc.legacyurl: /identity/overview/extensibility/implementing-a-custom-mysql-aspnet-identity-storage-provider
msc.type: authoredcontent
ms.openlocfilehash: 2f0b47d45bce82c71d1864536309f9e2ffed2d63
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519125"
---
# <a name="implementing-a-custom-mysql-aspnet-identity-storage-provider"></a>Implementace vlastního poskytovatele úložiště MySQL ASP.NET Identity

[Raquel Soares de Almeida](https://github.com/raquelsa), [Suhas Joshi](https://github.com/suhasj) [, FitzMacken](https://github.com/tfitzmac)

> ASP.NET Identity je rozšiřitelný systém, který umožňuje vytvořit vlastního poskytovatele úložiště a připojit ho k aplikaci bez nutnosti opětovného zpracování aplikace. Toto téma popisuje, jak vytvořit poskytovatele úložiště MySQL pro ASP.NET Identity. Přehled vytváření vlastních poskytovatelů úložiště najdete v tématu [Přehled vlastních poskytovatelů úložiště pro ASP.NET identity](overview-of-custom-storage-providers-for-aspnet-identity.md).
> 
> K dokončení tohoto kurzu musíte mít Visual Studio 2013 s aktualizací Update 2.
> 
> V tomto kurzu se dozvíte, jak:
> 
> - Ukazuje, jak vytvořit instanci databáze MySQL v Azure.
> - Ukáže, jak pomocí nástroje klienta MySQL (MySQL Workbench) vytvářet tabulky a spravovat vzdálenou databázi v Azure.
> - Podívejte se, jak nahradit výchozí implementaci ASP.NET Identity úložiště pomocí naší vlastní implementace v projektu aplikace MVC.
> 
> Tento kurz původně napsal Raquel Soares de Almeida a Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ). Ukázkový projekt byl aktualizován pro identitu 2,0 od Suhas Joshi. Téma bylo aktualizováno pro identitu 2,0 tím, že FitzMacken.

## <a name="download-completed-project"></a>Stáhnout dokončený projekt

Na konci tohoto kurzu budete mít projekt aplikace MVC s ASP.NET Identity pracovat s databází MySQL hostovanou v Azure.

Kompletního poskytovatele úložiště MySQL si můžete stáhnout v [ASPNET. identity. MySQL (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL).

## <a name="the-steps-you-will-perform"></a>Kroky, které provedete

V tomto kurzu provedete tyto kroky:

1. Vytvoření databáze MySQL v Azure
2. Vytvoření tabulek ASP.NET Identity v MySQL
3. Vytvořte aplikaci MVC a nakonfigurujte ji tak, aby používala poskytovatele MySQL.
4. Spuštění aplikace

Toto téma se nevztahuje na architekturu ASP.NET Identity a na rozhodnutích, která je nutné provést při implementaci poskytovatele úložiště zákazníků. Informace najdete v tématu [Přehled poskytovatelů vlastních úložišť pro ASP.NET identity](overview-of-custom-storage-providers-for-aspnet-identity.md).

## <a name="review-mysql-storage-provider-classes"></a>Kontrola tříd poskytovatele úložiště MySQL

Před přechodem k postupu vytvoření poskytovatele úložiště MySQL se podívejme na třídy, které tvoří poskytovatele úložiště. Budete potřebovat třídy, které spravují databázové operace a třídy, které jsou volány z aplikace pro správu uživatelů a rolí.

### <a name="storage-classes"></a>Třídy úložiště

- [IdentityUser](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityUser.cs) – obsahuje vlastnosti pro uživatele.
- [UserStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserStore.cs) – obsahuje operace pro přidání, aktualizaci nebo načtení uživatelů.
- [IdentityRole](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/IdentityRole.cs) – obsahuje vlastnosti pro role.
- [RoleStore](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleStore.cs) – obsahuje operace přidávání, odstraňování, aktualizace a načítání rolí.

### <a name="data-access-layer-classes"></a>Třídy vrstvy přístupu k datům

V tomto příkladu třídy vrstvy přístupu k datům obsahují příkazy SQL pro práci s tabulkami. Nicméně v kódu můžete chtít použít relační mapování objektu (ORM), například Entity Framework nebo NHibernate. Konkrétně vaše aplikace může docházet k špatnému výkonu bez použití ORM, které zahrnuje opožděné načítání a ukládání objektů do mezipaměti. Další informace najdete v tématu [ASP.NET Identity 2,0 bez Entity Framework?](https://aspnetidentity.codeplex.com/discussions/561828)

- [MySQLDatabase](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLDatabase.cs) – obsahuje připojení a metody databáze MySQL pro provádění databázových operací. Instance UserStore a RoleStore jsou vytvořeny s instancí této třídy.
- [Role](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/RoleTable.cs) – obsahuje databázové operace pro tabulku, která ukládá role.
- [UserClaimsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserClaimsTable.cs) – obsahuje databázové operace pro tabulku, která ukládá deklarace identity uživatelů.
- [UserLoginsTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserLoginsTable.cs) – obsahuje databázové operace pro tabulku, která obsahuje informace o přihlášení uživatele.
- [UserRoleTable](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserRoleTable.cs) – obsahuje databázové operace pro tabulku, ve které se ukládají uživatelé, kteří jsou přiřazeni k rolím.
- [User](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/UserTable.cs) -obsahuje databázové operace pro tabulku, která ukládá uživatele.

## <a name="create-a-mysql-database-instance-on-azure"></a>Vytvoření instance databáze MySQL v Azure

1. Přihlaste se k [webu Azure Portal](https://manage.windowsazure.com/).
2. V dolní části stránky klikněte na **+ Nový** a pak vyberte Store ( **Uložit**).  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.png)
3. V průvodci pro **Výběr a přidání** vyberte **ClearDB databázi MySQL** a klikněte na šipku Další v pravé dolní části dialogového okna.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.png)
4. Ponechte výchozí **bezplatný** plán a změňte **název** na **IdentityMySQLDatabase**. Vyberte oblast, která je nejblíže, a potom klikněte na šipku Další.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.png)
5. Vytvoření databáze dokončíte kliknutím na značku zaškrtnutí.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image4.png)
6. Po vytvoření databáze ji můžete spravovat na kartě **Doplňky** na portálu pro správu.   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image5.png)
7. Informace o připojení k databázi můžete získat kliknutím na **informace o připojení** v dolní části stránky.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image6.png)
8. Zkopírujte připojovací řetězec kliknutím na tlačítko Kopírovat a uložte ho, abyste ho mohli použít později v aplikaci MVC.   
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image7.png)

## <a name="create-the-aspnet-identity-tables-in-a-mysql-database"></a>Vytvoření tabulek ASP.NET Identity v databázi MySQL

### <a name="install-mysql-workbench-tool-to-connect-and-manage-mysql-database"></a>Instalace nástroje MySQL Workbench pro připojení a správu databáze MySQL

1. Instalace nástroje **MySQL Workbench** ze stránky pro [Stažení souborů MySQL](http://dev.mysql.com/downloads/windows/installer/)
2. Spusťte aplikaci a přidejte nové připojení kliknutím na tlačítko **MySQLConnections +** . Použijte data připojovacího řetězce, která jste zkopírovali z databáze Azure MySQL, kterou jste vytvořili dříve v tomto kurzu.
3. Po navázání připojení otevřete novou kartu **dotazu** ; Vložte příkazy z [MySQLIdentity. SQL](https://github.com/aspnet/samples/blob/master/samples/aspnet/Identity/AspNet.Identity.MySQL/MySQLIdentity.sql) do dotazu a spusťte je, aby se vytvořily tabulky databáze.
4. Nyní máte všechny ASP.NET Identity potřebné tabulky vytvořené v databázi MySQL hostované v Azure, jak je znázorněno níže.  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image1.jpg)

## <a name="create-an-mvc-application-project-from-template-and-configure-it-to-use-mysql-provider"></a>Vytvořit projekt aplikace MVC z šablony a nakonfigurovat ho tak, aby používal poskytovatele MySQL

V případě potřeby nainstalujte buď [Visual Studio Express 2013 pro web](https://go.microsoft.com/fwlink/?LinkId=299058) nebo [Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkId=306566) s aktualizací Update 2.

### <a name="download-the-aspnetidentitymysql-project-from-github"></a>Stažení projektu ASP. NET. identity. MySQL z GitHubu

1. Přejděte k adrese URL úložiště v [ASPNET. identity. MySQL (GitHub)](https://github.com/aspnet/samples/tree/master/samples/aspnet/Identity/AspNet.Identity.MySQL/).
2. Stáhněte si zdrojový kód.
3. Extrahujte soubor. zip do místní složky.
4. Otevřete řešení AspNet. identity. MySQL a sestavte ho.

### <a name="create-a-new-mvc-application-project-from-template"></a>Vytvoření nového projektu aplikace MVC ze šablony

1. Klikněte pravým tlačítkem na řešení **ASPNET. identity. MySQL** a **přidejte** **Nový projekt** .
2. V dialogovém okně **Přidat nový projekt** vyberte na levé straně **vizuál C#**  **a pak** vyberte **Webová aplikace ASP.NET**. Pojmenujte projekt **IdentityMySQLDemo**; a pak klikněte na OK.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image2.jpg)
3. V dialogovém okně **Nový projekt ASP.NET** vyberte šablonu MVC s výchozími možnostmi (zahrnující **jednotlivé uživatelské účty** jako metodu ověřování) a klikněte na **OK**.![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image3.jpg)
4. V Průzkumník řešení klikněte pravým tlačítkem myši na projekt IdentityMySQLDemo a vyberte možnost **Spravovat balíčky NuGet**. Do textového pole Hledat zadejte **identity. EntityFramework**. V seznamu výsledků vyberte tento balíček a klikněte na **odinstalovat**. Zobrazí se výzva k odinstalaci balíčku závislostí EntityFramework. Klikněte na Ano, protože tento balíček už nebudete v této aplikaci dál používat.
5. Klikněte pravým tlačítkem myši na projekt IdentityMySQLDemo, vyberte možnost **Přidat**, **odkaz, řešení, projekty** , vyberte projekt ASPNET. identity. MySQL a klikněte na tlačítko **OK**.
6. V projektu IdentityMySQLDemo nahraďte všechny odkazy na  
    `using Microsoft.AspNet.Identity.EntityFramework;`  
   se službou  
     `using AspNet.Identity.MySQL;`
7. V IdentityModels.cs nastavte **ApplicationDbContext** na odvozený od **MySqlDatabase** a přidejte konstruktor, který přijímá jeden parametr s názvem připojení.  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample1.cs)]
8. Otevřete soubor IdentityConfig.cs. V metodě **ApplicationUserManager. Create** nahraďte instanci UserManager následujícím kódem:  

    [!code-csharp[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample2.cs)]
9. Otevřete soubor Web. config a nahraďte řetězec DefaultConnection touto položkou nahrazením zvýrazněných hodnot připojovacím řetězcem databáze MySQL, kterou jste vytvořili v předchozích krocích:  

    [!code-xml[Main](implementing-a-custom-mysql-aspnet-identity-storage-provider/samples/sample3.xml?highlight=2)]

## <a name="run-the-app-and-connect-to-the-mysql-db"></a>Spuštění aplikace a připojení k databázi MySQL

1. Klikněte pravým tlačítkem na projekt **IdentityMySQLDemo** a vyberte **nastavit jako spouštěný projekt** .
2. Stisknutím **kombinace kláves CTRL + F5** Sestavte a spusťte aplikaci.
3. V horní části stránky klikněte na kartu **zaregistrovat** .
4. Zadejte nové uživatelské jméno a heslo a potom klikněte na **zaregistrovat**.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image8.png)
5. Nový uživatel je nyní zaregistrován a přihlášen.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image9.png)
6. Vraťte se do nástroje MySQL Workbench a prozkoumejte obsah tabulky **IdentityMySQLDatabase** . Prozkoumejte tabulku uživatelů pro položky při registraci nových uživatelů.  
  
    ![](implementing-a-custom-mysql-aspnet-identity-storage-provider/_static/image10.png)

## <a name="next-steps"></a>Další kroky

Další informace o tom, jak povolit další metody ověřování v této aplikaci, najdete v tématu [Vytvoření aplikace ASP.NET MVC 5 s možnostmi Facebook a Google OAuth2 a OpenID Signing](../../../mvc/overview/security/create-an-aspnet-mvc-5-app-with-facebook-and-google-oauth2-and-openid-sign-on.md).

Informace o tom, jak integrovat databázi s protokolem OAuth a nastavit role pro omezení přístupu uživatelů k vaší aplikaci, najdete v tématu [nasazení zabezpečené aplikace ASP.NET MVC 5 s členstvím, protokolem OAuth a SQL Database do Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data).

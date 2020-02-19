---
uid: identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
title: Migrace dat Universal Provider pro členství a profily uživatelů do ASP.NET Identity (C#)-ASP.NET 4. x
author: rustd
description: Tento kurz popisuje kroky, které je potřeba k migraci dat uživatelů a rolí a dat profilů uživatelů vytvořených pomocí univerzálních zprostředkovatelů existující aplikace...
ms.author: riande
ms.date: 12/13/2013
ms.custom: seoapril2019
ms.assetid: 2e260430-d13c-4658-bd05-e256fc0d63b8
msc.legacyurl: /identity/overview/migrations/migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity
msc.type: authoredcontent
ms.openlocfilehash: 31f02a0cec3c531c45c37b7aad8456e01e80b5ea
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456111"
---
# <a name="migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity-c"></a>Migrace členských dat od univerzálního zprostředkovatele a uživatelských profilů na ASP.NET Identity (C#)

od [Pranav Rastogi předvádí](https://github.com/rustd), [Rick Anderson](https://twitter.com/RickAndMSFT), [Robert blog](https://github.com/rmcmurray), [Suhas Joshi](https://github.com/suhasj)

> Tento kurz popisuje kroky, které jsou nezbytné k migraci dat uživatelů a rolí a dat profilů uživatelů vytvořených pomocí univerzálních zprostředkovatelů existující aplikace do modelu ASP.NET Identity. Výše zmíněný postup pro migraci dat profilu uživatele lze použít také v aplikaci s členstvím v SQL.

V rámci vydání Visual Studio 2013 představil tým ASP.NET nový ASP.NET Identity systém a další informace o tomto vydání si můžete přečíst [zde](../../index.md). V tomto článku najdete postup, jak migrovat webové aplikace z [členství SQL do nového systému identit](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md). Tento článek popisuje kroky pro migraci stávajících aplikací, které následují po modelu zprostředkovatelů pro správu uživatelů a rolí na nový model identity. Zaměření tohoto kurzu bude primárně zaměřeno na migraci dat profilu uživatele, aby se plynule připojila k novému systému. Migrace informací o uživatelích a rolích je podobná členství SQL. Přístup následovaný k migraci dat profilu lze použít také v aplikaci s členstvím v SQL.

Jako příklad se spustí webová aplikace vytvořená pomocí sady Visual Studio 2012, která používá model poskytovatelů. Pak přidáme kód pro správu profilů, zaregistrujete uživatele, přidáte profil pro uživatele, migrujete schéma databáze a pak změníte aplikaci tak, aby používala systém identit pro správu uživatelů a rolí. Jako test migrace by se uživatelé, kteří vytvořili pomocí univerzálních zprostředkovatelů, mohli přihlásit a noví uživatelé by měli být schopni se zaregistrovat.

> [!NOTE]
> Úplnou ukázku najdete na [https://github.com/suhasj/UniversalProviders-Identity-Migrations](https://github.com/suhasj/UniversalProviders-Identity-Migrations).

## <a name="profile-data-migration-summary"></a>Souhrn migrace dat profilu

Než začnete s migracemi, můžeme se podívat na možnosti ukládání dat profilu do modelu poskytovatelů. Data profilu pro uživatele aplikace je možné ukládat různými způsoby. mezi nimi nejčastěji využívají poskytovatelé předdefinovaných profilů dodávané společně s univerzálními poskytovateli. Tyto kroky by zahrnovaly

1. Přidejte třídu, která má vlastnosti používané k ukládání dat profilu.
2. Přidejte třídu, která rozšiřuje ' ProfileBase ' a implementuje metody pro získání výše uvedených dat profilu pro uživatele.
3. Povolte použití výchozích zprostředkovatelů profilů v souboru *Web. config* a Definujte třídu deklarovanou v kroku #2, která se má použít při přístupu k informacím profilu.

Informace o profilu jsou uloženy jako Serializovaná data XML a binární data v tabulce Profiles v databázi.

Po migraci aplikace, aby používala nový ASP.NET Identity systém, jsou informace o profilu deserializovány a uloženy jako vlastnosti třídy uživatel. Každá vlastnost se pak dá namapovat na sloupce v uživatelské tabulce. Výhodou je, že vlastnosti lze pracovat přímo pomocí třídy uživatele kromě toho, že při přístupu k nim nemusíte serializovat nebo deserializovat informace o datech.

## <a name="getting-started"></a>Začínáme

1. Vytvořte novou aplikaci webových formulářů ASP.NET 4,5 v aplikaci Visual Studio 2012. Aktuální ukázka používá šablonu webových formulářů, ale můžete použít také aplikaci MVC.  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.jpg)
2. Vytvořte novou složku ' modely ' pro uložení informací o profilu  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image1.png)
3. Jako příklad si můžeme uložit datum narození, město, výšku a váhu uživatele v profilu. Výška a váha jsou uloženy jako vlastní třída s názvem ' PersonalStats '. Abychom mohli profil uložit a načíst, potřebujeme třídu, která rozšiřuje ' ProfileBase '. Pojďme vytvořit novou třídu ' AppProfile ' k získání a uložení informací o profilu.

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample1.cs)]
4. Povolte profil v souboru *Web. config* . Zadejte název třídy, který se použije k uložení nebo načtení informací o uživateli vytvořených v kroku #3.

    [!code-xml[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample2.xml)]
5. Přidejte stránku webových formulářů do složky Account (účet), abyste získali data profilu od uživatele a ukládali je. Klikněte pravým tlačítkem na projekt a vyberte Přidat novou položku. Přidejte novou stránku webových formulářů se stránkou předlohy ' AddProfileData. aspx '. V části "MainContent" zkopírujte následující příkaz:

    [!code-html[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample3.html)]

   Do kódu na pozadí přidejte následující kód:

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample4.cs)]

   Přidejte obor názvů, pod kterým je definována třída AppProfile pro odebrání chyb kompilace.
6. Spusťte aplikaci a vytvořte nového uživatele s uživatelským jménem '**olduser '.** Přejděte na stránku ' AddProfileData ' a přidejte informace o profilu pro uživatele.  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.png)

V tabulce Profiles můžete ověřit, že jsou data uložena jako serializovaná XML, a to pomocí okna Průzkumník serveru. V aplikaci Visual Studio v nabídce zobrazení vyberte možnost ' Průzkumník serveru '. Pro databázi, která je definována v souboru *Web. config* , by mělo být datové připojení. Kliknutím na datové připojení se zobrazí různé podkategorie. Rozbalte ' Tables ' pro zobrazení různých tabulek v databázi, klikněte pravým tlačítkem na ' profily ' a zvolte možnost ' Zobrazit data tabulky ' pro zobrazení dat profilu uložených v tabulce profily.

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.png)

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image4.png)

## <a name="migrating-database-schema"></a>Migruje se schéma databáze.

Aby mohla stávající databáze fungovat se systémem identity, musíme aktualizovat schéma v databázi identit tak, aby podporovalo pole, která jsme přidali do původní databáze. To lze provést pomocí skriptů SQL pro vytvoření nových tabulek a zkopírování stávajících informací. V okně ' Průzkumník serveru ' rozbalte ' DefaultConnection ' pro zobrazení tabulek. Klikněte pravým tlačítkem na tabulky a vyberte nový dotaz.

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image5.png)

Vložte skript SQL z [https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt](https://raw.github.com/suhasj/UniversalProviders-Identity-Migrations/master/Migration.txt) a spusťte ho. Pokud se aktualizuje ' DefaultConnection ', uvidíme, že se přidaly nové tabulky. Můžete kontrolovat data v tabulkách, abyste viděli, že se informace migrovali.

![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image6.png)

## <a name="migrating-the-application-to-use-aspnet-identity"></a>Migrace aplikace pro použití ASP.NET Identity

1. Nainstalujte balíčky NuGet potřebné pro ASP.NET Identity:

    - Microsoft.AspNet.Identity.EntityFramework
    - Microsoft.AspNet.Identity.Owin
    - Microsoft.Owin.Host.SystemWeb
    - Microsoft.Owin.Security.Facebook
    - Microsoft.Owin.Security.Google
    - Microsoft.Owin.Security.MicrosoftAccount
    - Microsoft.Owin.Security.Twitter

   Další informace o správě balíčků NuGet najdete [tady](http://docs.nuget.org/docs/start-here/Managing-NuGet-Packages-Using-The-Dialog) .
2. Abychom mohli pracovat se stávajícími daty v tabulce, musíme vytvořit třídy modelů, které se mapují zpátky na tabulky a zapojte je do systému identit. V rámci kontraktu identity by třídy modelu měly buď implementovat rozhraní definovaná v knihovně DLL identity. Core, nebo mohou roztáhnout stávající implementaci těchto rozhraní, která jsou k dispozici v souboru Microsoft. AspNet. identity. EntityFramework. Pro role, přihlášení uživatelů a deklarace identity uživatelů budeme používat existující třídy. Pro naši ukázku musíme použít vlastního uživatele. Klikněte pravým tlačítkem na projekt a vytvořte novou složku ' IdentityModels '. Přidejte novou třídu User, jak je znázorněno níže:

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample5.cs)]

   Všimněte si, že ' ProfileInfo ' je nyní vlastnost třídy User. Proto můžeme použít třídu User k přímé práci s daty profilu.

Zkopírujte soubory ve složkách **IdentityModels** a **IdentityAccount** ze zdroje stahování ( [https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations](https://github.com/suhasj/UniversalProviders-Identity-Migrations/tree/master/UniversalProviders-Identity-Migrations) ). Mají zbývající třídy modelu a nové stránky, které jsou potřeba pro správu uživatelů a rolí pomocí rozhraní API ASP.NET Identity. Použitý přístup je podobný členství SQL a podrobné vysvětlení najdete [tady](migrating-an-existing-website-from-sql-membership-to-aspnet-identity.md).

[!INCLUDE[](../../../includes/identity/alter-command-exception.md)]

## <a name="copying-profile-data-to-the-new-tables"></a>Kopírování dat profilu do nových tabulek

Jak bylo zmíněno dříve, musíme deserializovat data XML v tabulkách profilů a uložit je do sloupců tabulky AspNetUsers. V tabulce uživatelů v předchozím kroku byly vytvořeny nové sloupce, takže všechny zbývá, abyste tyto sloupce naplnili potřebnými daty. K tomu použijeme konzolovou aplikaci, která se spustí jednou k naplnění nově vytvořených sloupců v tabulce Users.

1. Vytvořte novou konzolovou aplikaci ve výstupu řešení.  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image2.jpg)
2. Nainstalujte nejnovější verzi balíčku Entity Framework.
3. Přidejte webovou aplikaci vytvořenou výše jako odkaz na konzolovou aplikaci. Provedete to tak, že kliknete pravým tlačítkem na projekt, pak na Přidat odkazy, pak na řešení a potom kliknete na projekt a kliknete na OK.
4. Zkopírujte následující kód do třídy Program.cs. Tato logika načte data profilu pro každého uživatele, zaregistruje ho jako objekt ProfileInfo a uloží ho zpátky do databáze.

    [!code-csharp[Main](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/samples/sample6.cs)]

   Některé použité modely jsou definovány ve složce ' IdentityModels ' projektu webové aplikace, takže musíte zahrnout odpovídající obory názvů.
5. Výše uvedený kód funguje na databázovém souboru ve složce App\_data projektu webové aplikace, který jste vytvořili v předchozích krocích. Chcete-li se na něj odkazovat, aktualizujte připojovací řetězec v souboru App. config konzolové aplikace pomocí připojovacího řetězce v souboru Web. config webové aplikace. Zadejte také úplnou fyzickou cestu ve vlastnosti ' AttachDbFilename '.
6. Otevřete příkazový řádek a přejděte do složky bin výše uvedené konzolové aplikace. Spusťte spustitelný soubor a zkontrolujte výstup protokolu, jak je znázorněno na následujícím obrázku.  
    ![](migrating-universal-provider-data-for-membership-and-user-profiles-to-aspnet-identity/_static/image3.jpg)
7. Otevřete tabulku ' AspNetUsers ' v Průzkumník serveru a ověřte data v nových sloupcích, které obsahují vlastnosti. Měly by se aktualizovat odpovídajícími hodnotami vlastností.

## <a name="verify-functionality"></a>Ověřit funkčnost

Použijte nově přidané stránky členství, které jsou implementované pomocí ASP.NET Identity pro přihlášení uživatele z původní databáze. Uživatel by měl být schopný přihlásit se pomocí stejných přihlašovacích údajů. Vyzkoušejte jiné funkce, jako je přidání OAuth, vytvoření nového uživatele, změna hesla, přidání rolí, přidání uživatelů do rolí atd.

Data profilu pro starého uživatele a nové uživatele by se měla načíst a uložit v tabulce uživatelé. Na starou tabulku již nelze odkazovat.

## <a name="conclusion"></a>Závěr

Článek popisuje proces migrace webových aplikací, které používaly model poskytovatele pro členství ASP.NET Identity. Článek navíc popisuje migraci dat profilu pro uživatele, kteří se budou připojovat do systému identit. Pro otázky a problémy, které se při migraci vaší aplikace vyskytují, prosím nechejte komentáře uvedené níže.

*Děkujeme Rick Anderson a Robert blog pro kontrolu článku.*

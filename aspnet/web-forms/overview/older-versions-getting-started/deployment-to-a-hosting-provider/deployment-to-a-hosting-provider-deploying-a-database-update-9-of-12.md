---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
title: 'Nasazení webové aplikace SQL Server Compact v ASP.NET s využitím sady Visual Studio nebo Visual Web Developer: nasazení aktualizace databáze 9 z 12 | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a8d776af-4735-4612-87f6-9f326587f2d3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
msc.type: authoredcontent
ms.openlocfilehash: 3385e1019d9e7a9263fd9513c39b25eb85febbb5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78564440"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-database-update---9-of-12"></a>Nasazení webové aplikace SQL Server Compact v ASP.NET s využitím sady Visual Studio nebo Visual Web Developer: nasazení aktualizace databáze 9 z 12

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Studio 2012 RC nebo Visual Studio Express 2012 RC pro web. Můžete také použít Visual Studio 2010, pokud nainstalujete aktualizaci publikování na webu. Úvod k řadě najdete v [prvním kurzu v řadě](deployment-to-a-hosting-provider-introduction-1-of-12.md).
> 
> Kurz, který ukazuje funkce nasazení představené po vydání RC sady Visual Studio 2012, ukazuje, jak nasadit SQL Server edice jiné než SQL Server Compact a ukazuje, jak nasadit na Azure App Service Web Apps, v tématu [nasazení webu ASP.NET pomocí sady Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).

## <a name="overview"></a>Přehled

V tomto kurzu provedete změnu databáze a související změny kódu, otestujete změny v aplikaci Visual Studio a potom nasadíte aktualizaci do prostředí pro testování i provoz.

Připomenutí: Pokud se zobrazí chybová zpráva nebo něco nefunguje při procházení tohoto kurzu, zkontrolujte [stránku řešení potíží](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).

## <a name="adding-a-new-column-to-a-table"></a>Přidání nového sloupce do tabulky

V této části přidáte sloupec data narození do `Person` základní třídy pro entity `Student` a `Instructor`. Pak aktualizujete stránku, která zobrazuje data instruktora, aby zobrazila nový sloupec.

V projektu *ContosoUniversity. dal* otevřete *Person.cs* a na konci třídy `Person` přidejte následující vlastnost (před ní musí být dvě uzavírací složené závorky):

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample1.cs)]

Dále aktualizujte metodu počáteční hodnoty tak, aby poskytovala hodnotu pro nový sloupec. Otevřete *Migrations\Configuration.cs* a nahraďte blok kódu, který začíná `var instructors = new List<Instructor>` s následujícím blokem kódu, který obsahuje informace o datu narození:

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample2.cs)]

V projektu ContosoUniversity otevřete *instruktory. aspx* a přidejte nové pole šablony, abyste zobrazili datum narození. Přidejte ho mezi ty pro datum přijetí a přiřazení kanceláře:

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample3.aspx)]

(Pokud se odsazení kódu nesynchronizuje, můžete stisknutím kláves CTRL-K a potom CTRL-D soubor automaticky znovu zformátovat.)

Sestavte řešení a pak otevřete okno **konzoly Správce balíčků** . Ujistěte se, že je ContosoUniversity. DAL stále vybraný jako **výchozí projekt**.

V okně **konzoly Správce balíčků** vyberte jako **výchozí projekt**možnost **ContosoUniversity. dal** a potom zadejte následující příkaz:

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample4.ps1)]

Po dokončení tohoto příkazu aplikace Visual Studio otevře soubor třídy definující novou třídu `DbMigration` a v metodě `Up` můžete zobrazit kód, který vytvoří nový sloupec.

![AddBirthDate_migration_code](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image1.png)

Sestavte řešení a potom v okně **konzoly Správce balíčků** zadejte následující příkaz (Ujistěte se, že je projekt CONTOSOUNIVERSITY. dal stále vybraný):

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample5.ps1)]

Až se příkaz dokončí, spusťte aplikaci a vyberte stránku instruktoři. Po načtení stránky se zobrazí, že má nové pole data narození.

[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)

## <a name="deploying-the-database-update-to-the-test-environment"></a>Nasazení aktualizace databáze do testovacího prostředí

V **Průzkumník řešení** vyberte projekt ContosoUniversity.

Na panelu nástrojů **publikování webu jedním kliknutím** vyberte profil publikování **testu** a pak klikněte na **Publikovat web**. (Pokud je panel nástrojů zakázaný, vyberte projekt ContosoUniversity v **Průzkumník řešení**.)

Visual Studio nasadí aktualizovanou aplikaci a otevře se v prohlížeči na domovské stránce. Spuštěním stránky instruktory ověřte, zda byla aktualizace úspěšně nasazena. Když se aplikace pokusí o přístup k databázi pro tuto stránku, Code First aktualizuje schéma databáze a spustí metodu `Seed`. Po zobrazení stránky se zobrazí očekávaný sloupec **Datum narození** s kalendářními daty.

[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)

## <a name="deploying-the-database-update-to-the-production-environment"></a>Nasazení aktualizace databáze do provozního prostředí

Nyní se můžete nasadit do produkčního prostředí. Jediným rozdílem je, že pomocí *aplikace\_offline. htm* zabráníte uživatelům v přístupu k webu, a tak k aktualizaci databáze během nasazování změn. V případě produkčního nasazení proveďte následující kroky:

- Nahrajte *aplikaci\_offline souboru. htm* do produkčního webu.
- V sadě Visual Studio vyberte pracovní profil na panelu nástrojů **publikování webu jedním kliknutím** a klikněte na **Publikovat web**.
- Odstraňte *aplikaci\_offline souboru. htm* z produkčního webu.

> [!NOTE]
> I když se vaše aplikace používá v produkčním prostředí, měli byste implementovat plán zálohování. To znamená, že byste měli pravidelně kopírovat soubory *School-prod. sdf* a *ASPNET-prod. sdf* z produkčního serveru do umístění zabezpečeného úložiště a měli byste uchovávat několik generací takových záloh. Při aktualizaci databáze byste měli vytvořit záložní kopii hned před změnou. Pak pokud uděláte chybu a nezjistíte ji, dokud ji nenainstalujete do produkčního prostředí, budete moct databázi obnovit do stavu, ve kterém byla, než se nastala poškozená.

Když aplikace Visual Studio otevře adresu URL domovské stránky v prohlížeči, zobrazí se stránka *aplikace\_offline. htm* . Po odstranění *aplikace\_offline souboru. htm* můžete znovu přejít na domovskou stránku a ověřit, jestli se aktualizace úspěšně nasadila.

[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)

Nyní jste nasadili aktualizaci aplikace, která zahrnovala změnu databáze pro test i produkci. V dalším kurzu se dozvíte, jak migrovat databázi z SQL Server Compact na SQL Server Express a SQL Server.

> [!div class="step-by-step"]
> [Předchozí](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
> [Další](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)

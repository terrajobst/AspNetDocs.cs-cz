---
uid: mvc/overview/getting-started/database-first-development/setting-up-database
title: 'Kurz: Začínáme s EF Database First pomocí MVC 5'
description: V tomto kurzu se dozvíte, jak začít s existující databází a rychle vytvořit webovou aplikaci, která uživatelům umožňuje pracovat s daty.
author: Rick-Anderson
ms.author: riande
ms.date: 01/15/2019
ms.topic: tutorial
ms.assetid: 095abad4-3bfe-4f06-b092-ae6a735b7e49
msc.legacyurl: /mvc/overview/getting-started/database-first-development/setting-up-database
msc.type: authoredcontent
ms.openlocfilehash: a760767839a834a9c7e9fe358a3fd806a833261f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583522"
---
# <a name="tutorial-get-started-with-ef-database-first-using-mvc-5"></a>Kurz: Začínáme s EF Database First pomocí MVC 5

Pomocí MVC, Entity Framework a ASP.NET generování uživatelského rozhraní můžete vytvořit webovou aplikaci, která poskytuje rozhraní pro existující databázi. V této sérii kurzů se dozvíte, jak automaticky vygenerovat kód, který uživatelům umožňuje zobrazit, upravit, vytvořit a odstranit data, která se nacházejí v tabulce databáze. Generovaný kód odpovídá sloupcům v tabulce databáze. V poslední části této série se dozvíte, jak přidat datové poznámky k datovému modelu a zadat požadavky na ověření a formátování zobrazení. Až budete hotovi, můžete přejít na článek Azure, kde se dozvíte, jak nasadit aplikaci .NET a databázi SQL pro Azure App Service.

V tomto kurzu se dozvíte, jak začít s existující databází a rychle vytvořit webovou aplikaci, která uživatelům umožňuje pracovat s daty. Pro sestavení webové aplikace používá Entity Framework 6 a MVC 5. Funkce generování uživatelského rozhraní ASP.NET umožňuje automaticky generovat kód pro zobrazení, aktualizaci, vytváření a odstraňování dat. Pomocí nástrojů pro publikování v rámci sady Visual Studio můžete snadno nasadit lokalitu a databázi do Azure.

Tato část série se zaměřuje na vytvoření databáze a její naplnění daty.

Tato série se vytvořila s příspěvky z Dykstra a Rick Anderson. Vylepšili jsme se na základě zpětné vazby uživatelů v části komentáře.

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Nastavení databáze

## <a name="prerequisites"></a>Předpoklady

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)

## <a name="set-up-the-database"></a>Nastavení databáze

Pro napodobení prostředí existující databáze nejprve vytvoříte databázi s některými předem vyplněnými daty a pak vytvoříte webovou aplikaci, která se připojuje k databázi.

Tento kurz byl vyvinutý pomocí LocalDB se sadou Visual Studio 2017. Můžete použít existující databázový server místo LocalDB, ale v závislosti na vaší verzi sady Visual Studio a typu databáze nemusí být podporovány všechny datové nástroje v aplikaci Visual Studio. Pokud nástroje nejsou pro vaši databázi k dispozici, může být nutné provést některé kroky konkrétní databáze v rámci sady Management Suite pro vaši databázi.

Pokud máte problém s databázovými nástroji ve vaší verzi sady Visual Studio, ujistěte se, že máte nainstalovanou nejnovější verzi databázových nástrojů. Informace o aktualizaci nebo instalaci databázových nástrojů naleznete v tématu [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/hh297027).

Spusťte Visual Studio a vytvořte **projekt databáze SQL Server**. Pojmenujte projekt **ContosoUniversityData**.

![vytvořit databázový projekt](setting-up-database/_static/image1.png)

Nyní máte prázdný databázový projekt. Abyste se ujistili, že tuto databázi můžete nasadit do Azure, nastavíte Azure SQL Database jako cílovou platformu pro projekt. Nastavení cílové platformy neimplementuje databázi ve skutečnosti. To znamená, že databázový projekt ověří, zda je návrh databáze kompatibilní s cílovou platformou. Chcete-li nastavit cílovou platformu, otevřete **vlastnosti** projektu a vyberte **Microsoft Azure SQL Database** pro cílovou platformu.

Tabulky potřebné pro tento kurz můžete vytvořit přidáním skriptů SQL, které definují tabulky. Klikněte pravým tlačítkem na projekt a přidejte novou položku. Vyberte **tabulky a zobrazení** > **tabulce** a pojmenujte ji *student*.

V souboru tabulky nahraďte příkaz T-SQL následujícím kódem pro vytvoření tabulky.

[!code-sql[Main](setting-up-database/samples/sample1.sql)]

Všimněte si, že se okno návrhu automaticky synchronizuje s kódem. Můžete pracovat s kódem nebo návrhářem.

![Zobrazit kód a návrh](setting-up-database/_static/image5.png)

Přidejte další tabulku. Tentokrát pojmenujte tento kurz a použijte následující příkaz T-SQL.

[!code-sql[Main](setting-up-database/samples/sample2.sql)]

A pokud chcete vytvořit tabulku s názvem registrace, opakujte akci později.

[!code-sql[Main](setting-up-database/samples/sample3.sql)]

Databázi můžete naplnit daty prostřednictvím skriptu, který se spustí po nasazení databáze. Přidejte do projektu skript po nasazení. Klikněte pravým tlačítkem na projekt a přidejte novou položku. Vyberte **uživatelské skripty** > **skript po nasazení**. Můžete použít výchozí název.

Do skriptu po nasazení přidejte následující kód T-SQL. Tento skript jednoduše přidá data do databáze, když se nenajde žádný vyhovující záznam. Nepřepisuje ani neodstraní žádná data, která jste mohli do databáze zadat.

[!code-sql[Main](setting-up-database/samples/sample4.sql)]

Je důležité si uvědomit, že skript po nasazení se spustí pokaždé, když nasadíte databázový projekt. Proto je potřeba pečlivě zvážit požadavky při psaní tohoto skriptu. V některých případech můžete chtít začít znovu ze známé sady dat při každém nasazení projektu. V jiných případech možná nebudete chtít měnit stávající data jakýmkoli způsobem. Na základě vašich požadavků se můžete rozhodnout, jestli potřebujete skript po nasazení nebo co potřebujete zahrnout do skriptu. Další informace o naplnění databáze pomocí skriptu po nasazení najdete v tématu [zahrnutí dat do projektu databáze SQL Server](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx).

Teď máte 4 soubory skriptu SQL, ale žádné skutečné tabulky. Jste připraveni nasadit projekt databáze do LocalDB. V aplikaci Visual Studio klikněte na tlačítko Start (nebo F5) a sestavte a nasaďte projekt databáze. Na kartě **výstup** zkontrolujte, že sestavení a nasazení bylo úspěšné.

Chcete-li zjistit, zda byla nová databáze vytvořena, otevřete **Průzkumník objektů systému SQL Server** a vyhledejte název projektu ve správném místním databázovém serveru (v tomto případě **(LocalDB) \ProjectsV13**).

Chcete-li zobrazit, zda jsou tabulky naplněny daty, klikněte pravým tlačítkem myši na tabulku a vyberte možnost **Zobrazit data**.

![Zobrazit data tabulky](setting-up-database/_static/image9.png)

Zobrazí se upravitelné zobrazení dat tabulky. Pokud například vyberete **tabulky** > **dbo. Course** > **Zobrazit data**, zobrazí se tabulka se třemi sloupci (**kurz**, **název**a **kredity**) a čtyřmi řádky.

## <a name="additional-resources"></a>Další zdroje

Úvodní příklad Code First vývoje najdete v článku [Začínáme s ASP.NET MVC 5](../introduction/getting-started.md). Pokročilejší příklad najdete v tématu [vytvoření datového modelu Entity Framework pro aplikaci ASP.NET MVC 4](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).

Pokyny k výběru toho, který Entity Framework přístupu k použití, najdete v tématu věnovaném přístupům k [vývoji Entity Framework](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).

## <a name="next-steps"></a>Další kroky

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Nastavení databáze

Přejděte k dalšímu kurzu, kde se dozvíte, jak vytvořit webovou aplikaci a datové modely.
> [!div class="nextstepaction"]
> [Vytvoření webové aplikace a datových modelů](creating-the-web-application.md)

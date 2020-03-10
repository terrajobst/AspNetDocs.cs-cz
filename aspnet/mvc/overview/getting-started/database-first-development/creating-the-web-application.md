---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: 'Kurz: Vytvoření webové aplikace a datových modelů pro EF Database First pomocí ASP.NET MVC'
description: Tento kurz se zaměřuje na vytvoření webové aplikace a generování datových modelů založených na vašich databázových tabulkách.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 30fd42be5677df6fa6ee0630914098c30d21385b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616268"
---
# <a name="tutorial-create-the-web-application-and-data-models-for-ef-database-first-with-aspnet-mvc"></a>Kurz: Vytvoření webové aplikace a datových modelů pro EF Database First pomocí ASP.NET MVC

 Pomocí MVC, Entity Framework a ASP.NET generování uživatelského rozhraní můžete vytvořit webovou aplikaci, která poskytuje rozhraní pro existující databázi. V této sérii kurzů se dozvíte, jak automaticky vygenerovat kód, který uživatelům umožňuje zobrazit, upravit, vytvořit a odstranit data, která se nacházejí v tabulce databáze. Generovaný kód odpovídá sloupcům v tabulce databáze.

Tento kurz se zaměřuje na vytvoření webové aplikace a generování datových modelů založených na vašich databázových tabulkách.

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Vytvoření webové aplikace v ASP.NET
> * Generování modelů

## <a name="prerequisites"></a>Předpoklady

* [Začínáme s Entity Framework 6 Database First pomocí MVC 5](setting-up-database.md)

## <a name="create-an-aspnet-web-app"></a>Vytvoření webové aplikace v ASP.NET

V novém řešení nebo stejném řešení jako databázový projekt vytvořte v aplikaci Visual Studio nový projekt a vyberte šablonu **webové aplikace ASP.NET** . Pojmenujte projekt **ContosoSite**.

![vytvořit projekt](creating-the-web-application/_static/image1.png)

Klikněte na tlačítko **OK**.

V okně Nový projekt ASP.NET vyberte šablonu **MVC** . Nyní můžete zrušit výběr možnosti **hostitel v cloudu** , protože budete aplikaci nasazovat do cloudu později. Kliknutím na tlačítko **OK** vytvořte aplikaci.

Projekt se vytvoří s výchozími soubory a složkami.

V tomto kurzu budete používat Entity Framework 6. V projektu můžete pomocí okna spravovat balíčky NuGet dvakrát kontrolovat verzi Entity Framework. V případě potřeby aktualizujte svou verzi Entity Framework.

![Zobrazit verzi](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a>Generování modelů

Nyní budete vytvářet Entity Framework modely z databázových tabulek. Tyto modely jsou třídy, které použijete pro práci s daty. Každý model zrcadlí tabulku v databázi a obsahuje vlastnosti, které odpovídají sloupcům v tabulce.

Klikněte pravým tlačítkem na složku **modely** a vyberte položku **Přidat** a **Nová položka**.

V okně Přidat novou položku vyberte v levém podokně **data** a **ADO.NET model EDM (Entity Data Model)** z možností v prostředním podokně. Pojmenujte nový soubor modelu **ContosoModel**.

Klikněte na **Přidat**.

V průvodci model EDM (Entity Data Model) vyberte **EF Designer z databáze**.

Klikněte na **Další**.

Pokud máte databázová připojení definovaná v rámci vašeho vývojového prostředí, může se stát, že jedno z těchto připojení je předem vybrané. Chcete však vytvořit nové připojení k databázi, kterou jste vytvořili v první části tohoto kurzu. Klikněte na tlačítko **nové připojení** .

V okno Vlastnosti připojení zadejte název místního serveru, na kterém byla databáze vytvořena (v tomto případě **(LocalDB) \ProjectsV13**). Po zadání názvu serveru vyberte ContosoUniversityData z dostupných databází.

![nastavit vlastnosti připojení](creating-the-web-application/_static/image8.png)

Klikněte na tlačítko **OK**.

Nyní jsou zobrazeny správné vlastnosti připojení. Můžete použít výchozí název pro připojení v souboru Web. config.

Klikněte na **Další**.

Vyberte nejnovější verzi Entity Framework.

Klikněte na **Další**.

Vyberte **tabulky** a vygenerujte modely pro všechny tři tabulky.

Klikněte na **Finish** (Dokončit).

Pokud se zobrazí upozornění zabezpečení, vyberte **OK** a pokračujte v práci s šablonou.

Modely jsou generovány z tabulek databáze a zobrazí se diagram, který zobrazuje vlastnosti a vztahy mezi tabulkami.

![Diagram modelu](creating-the-web-application/_static/image11.png)

Složka modely nyní obsahuje mnoho nových souborů souvisejících s modely, které byly vygenerovány z databáze.

Soubor **ContosoModel.Context.cs** obsahuje třídu, která je odvozena od třídy **DbContext** , a poskytuje vlastnost pro každou třídu modelu, která odpovídá databázové tabulce. Soubory **Course.cs**, **Enrollment.cs**a **student.cs** obsahují třídy modelů, které reprezentují tabulky databáze. Při práci s generováním uživatelského rozhraní použijete třídu Context a třídy modelu.

Než budete pokračovat v tomto kurzu, sestavte projekt. V další části vygenerujete kód založený na datových modelech, ale tento oddíl nebude fungovat, pokud projekt nebyl sestaven.

## <a name="next-steps"></a>Další kroky

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Vytvořená webová aplikace v ASP.NET
> * Generované modely

Přejděte k dalšímu kurzu, kde se dozvíte, jak vytvořit generovaný kód na základě datových modelů.
> [!div class="nextstepaction"]
> [Generování zobrazení](generating-views.md)

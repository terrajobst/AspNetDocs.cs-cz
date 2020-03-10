---
uid: mvc/overview/getting-started/database-first-development/changing-the-database
title: 'Kurz: Změna databáze pro EF Database First pomocí aplikace ASP.NET MVC'
description: Tento kurz se zaměřuje na zajištění aktualizace struktury databáze a rozšíření této změny v rámci webové aplikace.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: cfd5c083-a319-482e-8f25-5b38caa93954
msc.legacyurl: /mvc/overview/getting-started/database-first-development/changing-the-database
msc.type: authoredcontent
ms.openlocfilehash: 52cad1120908cf0d4f85770f8e2690f9415c5f56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616261"
---
# <a name="tutorial-change-the-database-for-ef-database-first-with-aspnet-mvc-app"></a>Kurz: Změna databáze pro EF Database First pomocí aplikace ASP.NET MVC

Pomocí MVC, Entity Framework a ASP.NET generování uživatelského rozhraní můžete vytvořit webovou aplikaci, která poskytuje rozhraní pro existující databázi. V této sérii kurzů se dozvíte, jak automaticky vygenerovat kód, který uživatelům umožňuje zobrazit, upravit, vytvořit a odstranit data, která se nacházejí v tabulce databáze. Generovaný kód odpovídá sloupcům v tabulce databáze.

Tento kurz se zaměřuje na zajištění aktualizace struktury databáze a rozšíření této změny v rámci webové aplikace.

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Přidání sloupce
> * Přidat vlastnost do zobrazení

## <a name="prerequisites"></a>Předpoklady

* [Generování zobrazení](generating-views.md)

## <a name="add-a-column"></a>Přidání sloupce

Pokud aktualizujete strukturu tabulky v databázi, je nutné zajistit, aby se vaše změna rozšířila na datový model, zobrazení a kontroler.

Pro účely tohoto kurzu přidáte do tabulky student nový sloupec, kde poznamenejte prostřední jméno studenta. Chcete-li přidat tento sloupec, otevřete databázový projekt a otevřete soubor student. SQL. Pomocí návrháře nebo kódu T-SQL přidejte sloupec s názvem **MiddleName** , který je nvarchar (50) a povoluje hodnoty null.

Tuto změnu nasaďte do místní databáze spuštěním databázového projektu (nebo F5). Nové pole je přidáno do tabulky. Pokud ji v Průzkumník objektů systému SQL Server nevidíte, klikněte na tlačítko Aktualizovat v podokně.

![Zobrazit nový sloupec](changing-the-database/_static/image2.png)

Nový sloupec v databázové tabulce existuje, ale v současné době neexistuje ve třídě datového modelu. Model musíte aktualizovat tak, aby obsahoval nový sloupec. Ve složce **modely** otevřete soubor **ContosoModel. edmx** pro zobrazení diagramu modelu. Všimněte si, že model student neobsahuje vlastnost MiddleName. Klikněte pravým tlačítkem myši kamkoli na návrhovou plochu a vyberte **aktualizovat model z databáze**.

V Průvodci aktualizací vyberte kartu **aktualizovat** a pak vyberte **tabulky** > **dbo** > **student**. Klikněte na **Finish** (Dokončit).

Po dokončení procesu aktualizace obsahuje databázový diagram novou vlastnost **MiddleName** . Uložte soubor **ContosoModel. edmx** . Tento soubor musíte uložit, aby se nová vlastnost rozšířila na třídu **student.cs** . Nyní jste aktualizovali databázi a model.

Sestavte řešení.

## <a name="add-the-property-to-the-views"></a>Přidat vlastnost do zobrazení

Zobrazení však stále neobsahují novou vlastnost. Chcete-li aktualizovat zobrazení, máte dvě možnosti – můžete buď znovu vygenerovat zobrazení, a to tak, že znovu přidáte generování uživatelského rozhraní pro třídu studenta, nebo můžete do stávajících zobrazení přidat novou vlastnost ručně. V tomto kurzu znovu přidáte generování uživatelského rozhraní, protože jste neudělali žádné přizpůsobené změny v automaticky generovaných zobrazeních. Můžete zvážit ruční přidání vlastnosti, když jste provedli změny zobrazení a nechcete přijít o tyto změny.

Chcete-li zajistit opětovné vytvoření zobrazení, odstraňte složku **studenti** v **zobrazeních**a odstraňte **StudentsController**. Pak klikněte pravým tlačítkem na složku **Controllers** a přidejte pro model **studenta** generování uživatelského rozhraní. Znovu pojmenujte kontroler **StudentsController**. Vyberte **Přidat**.

Znovu sestavte řešení. Zobrazení teď obsahují vlastnost MiddleName.

![Zobrazit prostřední jméno](changing-the-database/_static/image5.png)

## <a name="next-steps"></a>Další kroky

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Přidání sloupce
> * Přidání vlastnosti do zobrazení

Přejděte k dalšímu kurzu, kde se dozvíte, jak přizpůsobit zobrazení pro zobrazení podrobností o záznamu studenta.
> [!div class="nextstepaction"]
> [Přizpůsobení zobrazení](customizing-a-view.md)
---
uid: mvc/overview/getting-started/database-first-development/customizing-a-view
title: 'Kurz: přizpůsobení zobrazení pro EF Database First pomocí aplikace ASP.NET MVC'
description: Tento kurz se zaměřuje na změnu automaticky generovaných zobrazení pro vylepšení prezentace.
author: Rick-Anderson
ms.author: riande
ms.date: 01/24/2019
ms.topic: tutorial
ms.assetid: 269380ff-d7e1-4035-8ad1-fe1316a25f76
msc.legacyurl: /mvc/overview/getting-started/database-first-development/customizing-a-view
msc.type: authoredcontent
ms.openlocfilehash: 89b8a0eb84b6e287c45bc141c68a2c76e63b0e41
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583592"
---
# <a name="tutorial-customize-view-for-ef-database-first-with-aspnet-mvc-app"></a>Kurz: přizpůsobení zobrazení pro EF Database First pomocí aplikace ASP.NET MVC

Pomocí MVC, Entity Framework a ASP.NET generování uživatelského rozhraní můžete vytvořit webovou aplikaci, která poskytuje rozhraní pro existující databázi. V této sérii kurzů se dozvíte, jak automaticky vygenerovat kód, který uživatelům umožňuje zobrazit, upravit, vytvořit a odstranit data, která se nacházejí v tabulce databáze. Generovaný kód odpovídá sloupcům v tabulce databáze.

Tento kurz se zaměřuje na změnu automaticky generovaných zobrazení pro vylepšení prezentace.

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Přidání kurzů na stránku podrobností studenta
> * Potvrďte, že jsou kurzy přidané na stránku.

## <a name="prerequisites"></a>Předpoklady

* [Změna databáze](changing-the-database.md)

## <a name="add-courses-to-student-detail"></a>Přidání kurzů k podrobnostem studenta

Generovaný kód poskytuje dobrý výchozí bod pro vaši aplikaci, ale nutně neposkytuje všechny funkce, které v aplikaci potřebujete. Kód můžete přizpůsobit tak, aby splňoval konkrétní požadavky vaší aplikace. V současné době vaše aplikace nezobrazuje zaregistrované kurzy pro vybraného studenta. V této části přidáte zaregistrované kurzy pro každého studenta do zobrazení **podrobností** pro studenta.

Otevřete **zobrazení** > **Students** > *Details. cshtml*. Pod poslední &lt;značka&gt;/DL, ale před uzavírací &lt;/div&gt; značky přidejte následující kód.

[!code-cshtml[Main](customizing-a-view/samples/sample1.cshtml)]

Tento kód vytvoří tabulku, která zobrazí řádek pro každý záznam v tabulce zápisu pro vybraného studenta. Metoda **Display** vykresluje HTML pro objekt (ModelItem), který představuje výraz. Použijte metodu Display (místo pouhého vložení hodnoty vlastnosti v kódu), abyste se ujistili, že je hodnota formátována správně na základě jejího typu a šablony pro daný typ. V tomto příkladu každý výraz vrátí jednu vlastnost z aktuálního záznamu ve smyčce a hodnoty jsou primitivní typy, které se vykreslují jako text.

## <a name="confirm-courses-are-added"></a>Přidávají se potvrzení kurzů.

Spusťte řešení. Klikněte na **seznam studentů** a vyberte **Podrobnosti** pro jednoho z studentů. V zobrazení se zobrazí zaregistrované kurzy.

![student s registrací](customizing-a-view/_static/image1.png)

## <a name="next-steps"></a>Další kroky
V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Přidání kurzů na stránku podrobností studenta
> * Potvrzení, že se kurzy přidávají na stránku

Přejděte k dalšímu kurzu, kde se dozvíte, jak přidat datové poznámky, abyste určili požadavky na ověření a formátování zobrazení.
> [!div class="nextstepaction"]
> [Vylepšení ověřování dat](enhancing-data-validation.md)

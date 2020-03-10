---
uid: mvc/overview/getting-started/database-first-development/generating-views
title: 'Kurz: generování zobrazení pro EF Database First pomocí aplikace ASP.NET MVC'
description: Tento kurz se zaměřuje na použití generování uživatelského rozhraní ASP.NET k vygenerování řadičů a zobrazení.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 669367cf-8e30-4eb6-821d-10a7d9bb906c
msc.legacyurl: /mvc/overview/getting-started/database-first-development/generating-views
msc.type: authoredcontent
ms.openlocfilehash: e71e13e22d8a72e1699cfc70d4d93af603edba5b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616205"
---
# <a name="tutorial-generate-views-for-ef-database-first-with-aspnet-mvc-app"></a>Kurz: generování zobrazení pro EF Database First pomocí aplikace ASP.NET MVC

Pomocí MVC, Entity Framework a ASP.NET generování uživatelského rozhraní můžete vytvořit webovou aplikaci, která poskytuje rozhraní pro existující databázi. V této sérii kurzů se dozvíte, jak automaticky vygenerovat kód, který uživatelům umožňuje zobrazit, upravit, vytvořit a odstranit data, která se nacházejí v tabulce databáze. Generovaný kód odpovídá sloupcům v tabulce databáze.

Tento kurz se zaměřuje na použití generování uživatelského rozhraní ASP.NET k vygenerování řadičů a zobrazení.

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Přidat generování uživatelského rozhraní
> * Přidat odkazy na nová zobrazení
> * Zobrazit zobrazení studenta
> * Zobrazit zobrazení pro zápis

## <a name="prerequisite"></a>Požadavek

* [Vytvoření webové aplikace a datových modelů](creating-the-web-application.md)

## <a name="add-scaffold"></a>Přidat generování uživatelského rozhraní

Jste připraveni vygenerovat kód, který bude poskytovat standardní operace s daty pro třídy modelu. Kód přidáte přidáním položky uživatelského rozhraní. Existuje mnoho možností pro typ generování uživatelského rozhraní, které můžete přidat; v tomto kurzu bude toto uživatelské rozhraní zahrnovat kontroler a zobrazení, které odpovídají modelům student a registrace, které jste vytvořili v předchozí části.

Chcete-li zachovat konzistenci projektu, přidejte nový kontroler do složky existující **řadiče** . Klikněte pravým tlačítkem na složku **řadiče** a vyberte **Přidat** > **Nová vygenerovaná položka**.

Pomocí možnosti **Entity Framework vyberte kontroler MVC 5 se zobrazeními** . Tato možnost vygeneruje kontroler a zobrazení pro aktualizaci, odstranění, vytváření a zobrazování dat v modelu.

![Přidat kontroler MVC](generating-views/_static/image2.png)

Vyberte **student (ContosoSite. Models)** pro třídu modelu a vyberte **ContosoUniversityDataEntities (ContosoSite. Models)** pro třídu kontextu. Ponechte název kontroleru jako **StudentsController**.

Klikněte na **Přidat**.

Pokud se zobrazí chyba, může to být způsobeno tím, že jste projekt nesestavili v předchozí části. Pokud ano, zkuste sestavit projekt a pak znovu přidat vygenerované položky.

Po dokončení procesu generování kódu se zobrazí nový kontroler a zobrazení v **řadičích** a **zobrazeních** projektu > složky **studentů** .

Proveďte stejné kroky znovu, ale přidejte uživatelské rozhraní pro třídu **zápisu** . Po dokončení budete mít k dispozici soubor **EnrollmentsController.cs** a složku v **zobrazení** s názvem **registrace** pomocí zobrazení vytvořit, odstranit, podrobnosti, úpravy a rejstřík.

## <a name="add-links-to-new-views"></a>Přidat odkazy na nová zobrazení

Aby bylo snazší přejít na nová zobrazení, můžete přidat několik hypertextových odkazů do zobrazení indexu pro studenty a registrace. Otevřete soubor v **zobrazeních** > **Home** > *index. cshtml*, což je Domovská stránka vašeho webu. Pod JumboTron přidejte následující kód.

[!code-cshtml[Main](generating-views/samples/sample1.cshtml)]

Pro metodu ActionLink je prvním parametrem text, který se má zobrazit v odkazu. Druhým parametrem je akce a třetí parametr je název kontroleru. Například první odkaz odkazuje na akci indexu v StudentsController. Skutečný hypertextový odkaz je vytvořen z těchto hodnot. První odkaz nakonec převezme uživatele do souboru **index. cshtml** v rámci složky **views/Students** .

## <a name="display-student-views"></a>Zobrazit zobrazení studenta

Ověřte, že kód přidaný do projektu správně zobrazuje seznam studentů a umožňuje uživatelům upravovat, vytvářet nebo odstraňovat záznamy studenta v databázi.

Klikněte pravým tlačítkem na **zobrazení** > soubor *. cshtml* pro **domovskou** > index a **v prohlížeči vyberte Zobrazit**. Na domovské stránce aplikace vyberte **seznam studentů**.

![](generating-views/_static/image6.png)

Na stránce **index** si všimněte seznamu studentů a odkazů pro úpravu těchto dat. Vyberte odkaz **vytvořit nový** a zadejte některé hodnoty pro nového studenta. Klikněte na **vytvořit**a Všimněte si, že se do seznamu přidá nový student.

Zpět na stránce **index** vyberte odkaz **Upravit** a změňte některé hodnoty pro studenta. Klikněte na **Uložit**a Všimněte si, že se změnil záznam studenta.

Nakonec vyberte odkaz **Odstranit** a potvrďte, že chcete záznam odstranit kliknutím na tlačítko **Odstranit** .

Bez psaní kódu jste přidali zobrazení, která provádějí běžné operace s daty v tabulce student.

Možná jste si všimli, že textový popisek pro pole je založen na vlastnosti databáze (například **LastName**), která není nutně ta, co chcete zobrazit na webové stránce. Například můžete chtít, aby popisek byl **Poslední název**. Tento problém se zobrazením opravíte později v tomto kurzu.

## <a name="display-enrollment-views"></a>Zobrazit zobrazení pro zápis

Vaše databáze obsahuje vztah 1:1 mezi tabulkami studentů a registrací a vztah 1: n mezi tabulkami kurzů a zápisů. Zobrazení pro registraci správně zpracovávají tyto vztahy. Přejděte na domovskou stránku vašeho webu a vyberte odkaz **seznam** registrací a pak klikněte na odkaz pro **Vytvoření nového** .

Zobrazení obsahuje formulář pro vytvoření nového záznamu registrace. Zejména si všimněte, že formulář obsahuje rozevírací seznam **CourseID** a rozevírací seznam **StudentID** . Obě jsou vyplněny hodnotami ze souvisejících tabulek.

Kromě toho se ověření zadaných hodnot automaticky použije na základě datového typu pole. Pro **třídu** je vyžadováno číslo, takže se zobrazí chybová zpráva, pokud se pokusíte zadat nekompatibilní hodnotu: hodnota *pole musí být číslo.*

Ověřili jste, že automaticky vygenerovaná zobrazení umožňují uživatelům pracovat s daty v databázi. V dalším kurzu v této sérii aktualizujete databázi a provedete příslušné změny ve webové aplikaci.

## <a name="next-steps"></a>Další kroky

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Přidání uživatelského rozhraní
> * Přidané odkazy na nová zobrazení
> * Zobrazení zobrazení studenta
> * Zobrazení zápisu

Přejděte k dalšímu kurzu, kde se dozvíte, jak změnit databázi.
> [!div class="nextstepaction"]
> [Změna databáze](changing-the-database.md)
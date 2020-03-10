---
uid: mvc/overview/getting-started/database-first-development/enhancing-data-validation
title: 'Kurz: vylepšení ověřování dat pro EF Database First pomocí aplikace ASP.NET MVC'
description: Tento kurz se zaměřuje na přidání datových poznámek k datovému modelu a určení požadavků na ověření a formátování zobrazení.
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: 0ed5e67a-34c0-4b57-84a6-802b0fb3cd00
msc.legacyurl: /mvc/overview/getting-started/database-first-development/enhancing-data-validation
msc.type: authoredcontent
ms.openlocfilehash: 897cd7c6a40445e2a4abede50d81e101372d3233
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616275"
---
# <a name="tutorial-enhance-data-validation-for-ef-database-first-with-aspnet-mvc-app"></a>Kurz: vylepšení ověřování dat pro EF Database First pomocí aplikace ASP.NET MVC

Pomocí MVC, Entity Framework a ASP.NET generování uživatelského rozhraní můžete vytvořit webovou aplikaci, která poskytuje rozhraní pro existující databázi. V této sérii kurzů se dozvíte, jak automaticky vygenerovat kód, který uživatelům umožňuje zobrazit, upravit, vytvořit a odstranit data, která se nacházejí v tabulce databáze. Generovaný kód odpovídá sloupcům v tabulce databáze.

Tento kurz se zaměřuje na přidání datových poznámek k datovému modelu a určení požadavků na ověření a formátování zobrazení. Vylepšili jsme se na základě zpětné vazby uživatelů v části komentáře.

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Přidat datové poznámky
> * Přidat třídy metadat

## <a name="prerequisites"></a>Předpoklady

* [Přizpůsobení zobrazení](customizing-a-view.md)

## <a name="add-data-annotations"></a>Přidat datové poznámky

Jak jste viděli v předchozím tématu, některá pravidla ověření dat se automaticky aplikují na vstup uživatele. Můžete například zadat jenom číslo vlastnosti třídy. Chcete-li zadat další pravidla pro ověřování dat, můžete do třídy modelu přidat datové poznámky. Tyto poznámky jsou v rámci vaší webové aplikace aplikovány na zadanou vlastnost. Můžete také použít atributy formátování, které mění způsob zobrazení vlastností; například změna hodnoty používané pro textové popisky.

V tomto kurzu přidáte poznámky k datům, abyste omezili délku hodnot poskytnutých pro vlastnosti FirstName, LastName a MiddleName. V databázi jsou tyto hodnoty omezeny na 50 znaků; ve vaší webové aplikaci se ale omezení počtu znaků aktuálně nevynutilo. Pokud uživatel zadá pro jednu z těchto hodnot více než 50 znaků, stránka při pokusu o uložení hodnoty do databáze dojde k chybě. Také omezíte hodnotu pro hodnoty mezi 0 a 4.

Vyberte **modely** > **ContosoModel. edmx** > **ContosoModel.TT** a otevřete soubor *student.cs* . Do třídy přidejte následující zvýrazněný kód.

[!code-csharp[Main](enhancing-data-validation/samples/sample1.cs?highlight=5,15,17,20)]

Otevřete *Enrollment.cs* a přidejte následující zvýrazněný kód.

[!code-csharp[Main](enhancing-data-validation/samples/sample2.cs?highlight=5,10)]

Sestavte řešení.

Klikněte na **seznam studentů** a vyberte **Upravit**. Pokud se pokusíte zadat více než 50 znaků, zobrazí se chybová zpráva.

![zobrazit chybovou zprávu](enhancing-data-validation/_static/image1.png)

Vraťte se na domovskou stránku. Klikněte na **seznam** registrací a vyberte **Upravit**. Došlo k pokusu o poskytnutí třídy nad 4. Tato chyba se zobrazí: *hodnota třídy musí být mezi 0 a 4.*

## <a name="add-metadata-classes"></a>Přidat třídy metadat

Přidávání ověřovacích atributů přímo do třídy modelu funguje, když neočekáváte, že se databáze mění; Pokud se ale vaše databáze změní a potřebujete znovu vygenerovat třídu modelu, ztratíte všechny atributy, které jste použili u třídy modelu. Tento přístup může být velice neefektivní a náchylný ke ztrátě důležitých ověřovacích pravidel.

Chcete-li se tomuto problému vyhnout, můžete přidat třídu metadat obsahující atributy. Při přidružení třídy modelu k třídě metadat se tyto atributy aplikují na model. V tomto přístupu třída modelu může být znovu vygenerována bez ztráty všech atributů, které byly aplikovány na třídu metadat.

Ve složce **modely** přidejte třídu s názvem *metadata.cs*.

Nahraďte kód v *metadata.cs* následujícím kódem.

[!code-csharp[Main](enhancing-data-validation/samples/sample3.cs)]

Tyto třídy metadat obsahují všechny atributy ověřování, které jste předtím použili u tříd modelu. Atribut **zobrazení** se používá ke změně hodnoty používané pro textové popisky.

Nyní je třeba přidružit třídy modelů k třídám metadat.

Ve složce **modely** přidejte třídu s názvem *PartialClasses.cs*.

Obsah souboru nahraďte následujícím kódem.

[!code-csharp[Main](enhancing-data-validation/samples/sample4.cs)]

Všimněte si, že každá třída je označena jako třída `partial` a každý odpovídá názvu a oboru názvů jako třída, která je automaticky vygenerována. Použitím atributu metadata na částečnou třídu zajistíte, aby atributy ověřování dat byly použity na automaticky generovanou třídu. Tyto atributy nebudou ztraceny při opětovném vygenerování tříd modelu, protože atribut metadata je použit v dílčích třídách, které nejsou znovu vygenerovány.

Chcete-li znovu vygenerovat automaticky generované třídy, otevřete soubor *ContosoModel. edmx* . Znovu klikněte pravým tlačítkem myši na návrhovou plochu a vyberte **aktualizovat model z databáze**. I když jste databázi nezměnili, tento proces znovu vygeneruje třídy. Na kartě **aktualizovat** vyberte **tabulky** a **Dokončit**.

Uložte soubor *ContosoModel. edmx* , aby se změny projevily.

Otevřete soubor *student.cs* nebo soubor *Enrollment.cs* a Všimněte si, že výše použité atributy ověření dat již nejsou v souboru. Spusťte ale aplikaci a Všimněte si, že ověřovací pravidla se při zadávání dat pořád používají.

## <a name="conclusion"></a>Závěr

Tato série poskytuje jednoduchý příklad, jak generovat kód z existující databáze, která umožňuje uživatelům upravovat, aktualizovat, vytvářet a odstraňovat data. Používá ASP.NET MVC 5, Entity Framework a ASP.NET generování uživatelského rozhraní pro vytvoření projektu. 

Úvodní příklad Code First vývoje najdete v článku [Začínáme s ASP.NET MVC 5](../introduction/getting-started.md). 

Pokročilejší příklad najdete v tématu [vytvoření datového modelu Entity Framework pro aplikaci ASP.NET MVC 4](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Všimněte si, že rozhraní API DbContext, které používáte pro práci s daty v Database First, je stejné jako rozhraní API, které používáte pro práci s daty v Code First. I v případě, že máte v úmyslu použít Database First, můžete se dozvědět, jak zpracovávat složitější scénáře, jako je čtení a aktualizace souvisejících dat, zpracování konfliktů souběžnosti a tak dále v kurzu Code First. Jediný rozdíl je v tom, jak jsou vytvořeny databáze, třídy kontextu a třídy entit.

## <a name="additional-resources"></a>Další zdroje

Úplný seznam poznámek k ověření dat, které můžete použít pro vlastnosti a třídy, naleznete v tématu [System. ComponentModel. DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx).

## <a name="next-steps"></a>Další kroky

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Přidané datové poznámky
> * Přidané třídy metadat

Další informace o tom, jak nasadit webovou aplikaci a databázi SQL pro Azure App Service, najdete v tomto kurzu:
> [!div class="nextstepaction"]
> [Nasazení aplikace .NET pro Azure App Service](/azure/app-service/app-service-web-tutorial-dotnet-sqldatabase/)

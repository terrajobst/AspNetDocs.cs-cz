---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
title: '4\. část: Přidání zobrazení Správce | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 792f4513-a508-4d14-a0dd-1a2fe282c7bb
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-4
msc.type: authoredcontent
ms.openlocfilehash: 664aeb33031e933322886a6d6bdd989277e9fda2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556012"
---
# <a name="part-4-adding-an-admin-view"></a>4\. část: Přidání zobrazení pro správu

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-view"></a>Přidat zobrazení Správce

Teď se změní na stranu klienta a přidá se stránka, která může využívat data z kontroleru správce. Stránka umožní uživatelům vytvářet, upravovat nebo odstraňovat produkty, a to odesláním požadavků AJAX do kontroleru.

V Průzkumník řešení rozbalte složku řadiče a otevřete soubor s názvem HomeController.cs. Tento soubor obsahuje kontroler MVC. Přidejte metodu s názvem `Admin`:

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample1.cs)]

Metoda **HttpRouteUrl** vytvoří identifikátor URI webového rozhraní API a uložíme ho do balíčku zobrazení pro pozdější verzi.

Dále umístěte kurzor na text do metody `Admin` akce, klikněte pravým tlačítkem myši a vyberte možnost **Přidat zobrazení**. Tím se zobrazí dialogové okno **Přidat zobrazení** .

![](using-web-api-with-entity-framework-part-4/_static/image1.png)

V dialogovém okně **Přidat zobrazení** pojmenujte zobrazení "admin". Zaškrtněte políčko s názvem **vytvořit zobrazení silného typu**. V části **třída modelu**vyberte produkt (ProductStore. Models). U ostatních možností ponechte výchozí hodnoty.

![](using-web-api-with-entity-framework-part-4/_static/image2.png)

Kliknutím na **Přidat** přidáte do zobrazení/domů soubor s názvem admin. cshtml. Otevřete tento soubor a přidejte následující kód HTML. Tento kód HTML definuje strukturu stránky, ale ještě není kabelem funkční.

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample2.cshtml)]

## <a name="create-a-link-to-the-admin-page"></a>Vytvoří odkaz na stránku správce.

V Průzkumník řešení rozbalte složku zobrazení a potom rozbalte sdílenou složku. Otevřete soubor s názvem \_layout. cshtml. Vyhledejte element **ul** s ID = "nabídka" a odkaz akce pro zobrazení Správce:

[!code-cshtml[Main](using-web-api-with-entity-framework-part-4/samples/sample3.cshtml)]

> [!NOTE]
> V ukázkovém projektu jsem udělal několik dalších změn kosmetických prostředků, jako je například nahrazení řetězce "vaše logo". Neovlivňují funkce aplikace. Můžete stáhnout projekt a porovnat soubory.

Spusťte aplikaci a klikněte na odkaz správce, který se zobrazí v horní části domovské stránky. Stránka pro správu by měla vypadat takto:

![](using-web-api-with-entity-framework-part-4/_static/image3.png)

V tuto chvíli stránka není cokoli dělat. V další části použijeme vyseknutí. js k vytvoření dynamického uživatelského rozhraní.

## <a name="add-authorization"></a>Přidat autorizaci

Stránka pro správu je aktuálně přístupná všem návštěvníkům webu. Pojďme to změnit, aby se omezilo oprávnění pro správce.

Začněte přidáním role správce a uživatele správce. V Průzkumník řešení rozbalte složku filtry a otevřete soubor s názvem InitializeSimpleMembershipAttribute.cs. Vyhledejte konstruktor `SimpleMembershipInitializer`. Po volání metody **WebSecurity. InitializeDatabaseConnection**přidejte následující kód:

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample4.cs)]

Toto je rychlý a špinavý způsob, jak přidat roli správce a vytvořit uživatele pro tuto roli.

V Průzkumník řešení rozbalte složku řadiče a otevřete soubor HomeController.cs. Přidejte atribut **autorizace** do metody `Admin`.

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample5.cs)]

Otevřete soubor AdminController.cs a přidejte atribut **autorizuje** do celé `AdminController` třídy.

[!code-csharp[Main](using-web-api-with-entity-framework-part-4/samples/sample6.cs)]

> [!NOTE]
> MVC a webové rozhraní API definují **autorizační** atributy v různých oborech názvů. MVC používá **System. Web. Mvc. AuthorizeAttribute**, zatímco webové rozhraní API používá **System. Web. http. AuthorizeAttribute**.

Stránku Správce teď můžou zobrazit jenom správci. Pokud odešlete požadavek HTTP kontroleru správce, musí požadavek obsahovat ověřovací soubor cookie. V takovém případě pošle Server odpověď HTTP 401 (Neautorizovaná). Můžete to zobrazit v Fiddler odesláním žádosti o získání `http://localhost:*port*/api/admin`.

> [!div class="step-by-step"]
> [Předchozí](using-web-api-with-entity-framework-part-3.md)
> [Další](using-web-api-with-entity-framework-part-5.md)

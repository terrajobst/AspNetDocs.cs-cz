---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
title: 'Část 1: Přehled a vytvoření projektu | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: 94421d86-68c4-4471-bf5f-82d654a17252
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-1
msc.type: authoredcontent
ms.openlocfilehash: a76a18f2bd95969358452085ef342fdca8a386e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556075"
---
# <a name="part-1-overview-and-creating-the-project"></a>Část 1: Přehled a vytvoření projektu

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

Entity Framework je rozhraní pro mapování objektů a relačních objektů. Mapuje doménové objekty ve vašem kódu na entity v relační databázi. Ve většině případů se nemusíte starat o databázovou vrstvu, protože ji Entity Framework postará za vás. Kód zpracovává objekty a změny jsou uchovány v databázi.

## <a name="about-the-tutorial"></a>O tomto kurzu

V tomto kurzu vytvoříte jednoduchou aplikaci ze Storu. Existují dvě hlavní části aplikace. Normální uživatelé mohou zobrazit produkty a vytvářet objednávky:

![](using-web-api-with-entity-framework-part-1/_static/image1.png)

Správci můžou vytvořit, odstranit nebo upravit produkty:

![](using-web-api-with-entity-framework-part-1/_static/image2.png)

## <a name="skills-youll-learn"></a>Dovednosti, se kterými se naučíte

Tady je seznam toho, co se naučíte:

- Jak používat Entity Framework s webovým rozhraním API ASP.NET
- Jak použít vyseknutí. js k vytvoření dynamického uživatelského rozhraní klienta.
- Jak používat ověřování pomocí formulářů s webovým rozhraním API k ověřování uživatelů.

I když je tento kurz samostatný, možná si budete chtít nejdřív přečíst následující kurzy:

- [Vaše první webové rozhraní API ASP.NET](../../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md)
- [Vytvoření webového rozhraní API, které podporuje operace CRUD](../creating-a-web-api-that-supports-crud-operations.md)

K [disASP.NET](../../../../mvc/index.md) je také užitečné některé znalosti o MVC.

## <a name="overview"></a>Přehled

V nejvyšší úrovni je tady architektura aplikace:

- ASP.NET MVC vygeneruje stránky HTML pro klienta.
- Webové rozhraní API ASP.NET zpřístupňuje operace CRUD s daty (produkty a objednávky).
- Entity Framework překládá C# modely používané WEBOVÝm rozhraním API do databázových entit.

![](using-web-api-with-entity-framework-part-1/_static/image3.png)

Následující diagram znázorňuje způsob reprezentace objektů domény v různých vrstvách aplikace: databázová vrstva, objektový model a nakonec formát drátu, který slouží k přenosu dat do klienta prostřednictvím protokolu HTTP.

![](using-web-api-with-entity-framework-part-1/_static/image4.png)

## <a name="create-the-visual-studio-project"></a>Vytvoření projektu sady Visual Studio

Můžete vytvořit projekt kurzu pomocí aplikace Visual Web Developer Express nebo plné verze sady Visual Studio.

Na **úvodní** stránce klikněte na **Nový projekt**.

V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte uzel  **C# vizuál** . V **části C#vizuál** vyberte **Web**. V seznamu šablon projektu vyberte **ASP.NET webová aplikace MVC 4**. Pojmenujte projekt "ProductStore" a klikněte na tlačítko **OK**.

![](using-web-api-with-entity-framework-part-1/_static/image5.png)

V dialogovém okně **Nový projekt ASP.NET MVC 4** vyberte možnost **Internet aplikace** a klikněte na tlačítko **OK**.

![](using-web-api-with-entity-framework-part-1/_static/image6.png)

Šablona "Internetová aplikace" vytvoří aplikaci ASP.NET MVC, která podporuje ověřování formulářů. Pokud teď aplikaci spustíte, už obsahuje některé funkce:

- Noví uživatelé se můžou zaregistrovat kliknutím na odkaz zaregistrovat v pravém horním rohu.
- Registrovaní uživatelé se můžou přihlásit kliknutím na odkaz Přihlásit se.

Informace o členství jsou trvalé v databázi, která je vytvořena automaticky. Další informace o ověřování pomocí formulářů v ASP.NET MVC najdete v tématu [Návod: použití ověřování pomocí formulářů v ASP.NET MVC](https://msdn.microsoft.com/library/ff398049(VS.98).aspx).

## <a name="update-the-css-file"></a>Aktualizovat soubor CSS

Tento krok je kosmetický, ale stránky se vykreslí jako dřívější snímky obrazovky.

V Průzkumník řešení rozbalte složku obsahu a otevřete soubor s názvem site. CSS. Přidejte následující styly CSS:

[!code-css[Main](using-web-api-with-entity-framework-part-1/samples/sample1.css)]

> [!div class="step-by-step"]
> [Next](using-web-api-with-entity-framework-part-2.md)

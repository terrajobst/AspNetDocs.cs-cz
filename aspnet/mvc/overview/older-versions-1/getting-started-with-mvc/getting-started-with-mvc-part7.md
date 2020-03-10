---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
title: Přidání ověření do modelu | Microsoft Docs
author: shanselman
description: Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvořte jednoduchou webovou aplikaci, která čte a zapisuje z databáze.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: aa7b3e8e-e23d-49f1-b160-f99a7f2982bd
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
msc.type: authoredcontent
ms.openlocfilehash: 9403be574324c34edf93bef1e0e4fd7ba68a3a9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543643"
---
# <a name="adding-validation-to-the-model"></a>Přidání ověření do modelu

[Scott Hanselman](https://github.com/shanselman)

> Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvoříte jednoduchou webovou aplikaci, která čte a zapisuje z databáze. Navštivte [centrum učení služby ASP.NET MVC](../../../index.md) , kde najdete další kurzy a ukázky pro ASP.NET MVC.

V této části budeme implementovat podporu nutnou k povolení ověřování vstupu v rámci naší aplikace. Zajistíme, aby byl obsah databáze vždycky správný, a při pokusu o zadání užitečných chybových zpráv, které se pokoušejí, a zadání filmových dat, která nejsou platná. Začneme přidáním malé logiky ověřování do třídy video.

Klikněte pravým tlačítkem na složku modelu a vyberte Přidat třídu. Pojmenujte film vaší třídy.

Po předchozím vytvoření modelu entity filmu rozhraní IDE vytvořilo třídu filmu. Ve skutečnosti může být součástí třídy video v jednom souboru a částečně v jiném. Toto se nazývá částečná třída. Chystáme se třídu Movie rozšiřuje z jiného souboru.

Vytvoříme částečnou třídu filmu, která odkazuje na "přítel Class" s některými atributy, které budou poskytovat pomocný parametr ověřování systému. Název a cenu budeme označovat jako povinnou a také si Navedeme, že cena bude v určitém rozsahu. Klikněte pravým tlačítkem na složku modely a vyberte Přidat třídu. Pojmenujte film na třídu a klikněte na tlačítko OK. Tady je, jak má naše částečná třída filmu vypadat.

[!code-csharp[Main](getting-started-with-mvc-part7/samples/sample1.cs)]

Spusťte aplikaci znovu a zkuste zadat film s cenou vyšší než 100. Po odeslání formuláře se zobrazí chybová zpráva. Tato chyba se zachycuje na straně serveru a nastane po publikování formuláře. Všimněte si, jak byly integrované pomocníky HTML v ASP.NET MVC dostatečně inteligentní pro zobrazení chybové zprávy a udržování hodnot pro nás v rámci elementů TextBox:

[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)

To funguje skvěle, ale v případě, že se na straně klienta může informovat uživatel hned po straně klienta.

Pojďme povolit ověřování na straně klienta pomocí JavaScriptu.

## <a name="adding-client-side-validation"></a>Přidání ověřování na straně klienta

Vzhledem k tomu, že naše třída filmu již obsahuje některé atributy ověřování, stačí do naší šablony zobrazení Create. aspx přidat několik souborů JavaScriptu a přidat řádek kódu, který povolí ověřování na straně klienta.

V souboru vwd se podívejte na naše zobrazení/složku videa a otevřete vytvořit. aspx.

Otevřete složku skripty v Průzkumník řešení a přetáhněte následující tři skripty do značky &lt;Head&gt;.

- MicrosoftAjax.js
- MicrosoftMvcValidation.js

Chcete, aby se tyto soubory skriptu zobrazovaly v tomto pořadí.

[!code-html[Main](getting-started-with-mvc-part7/samples/sample2.html)]

Přidejte také tento jediný řádek nad HTML. BeginForm:

[!code-aspx[Main](getting-started-with-mvc-part7/samples/sample3.aspx)]

Zde je kód zobrazený v rámci integrovaného vývojového prostředí (IDE).

[Filmy ![– Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)

Spusťte aplikaci a znovu navštivte/Movies/Create a klikněte na vytvořit bez zadání jakýchkoli dat. Chybové zprávy se zobrazí okamžitě bez blikání stránky, které přiřadíme k posílání dat zpět na server. Důvodem je to, že ASP.NET MVC nyní ověřuje vstup na straně klienta (pomocí JavaScriptu) i na serveru.

[![vytvoření – Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)

To je dobré. Nyní přidáme do databáze jeden další sloupec.

> [!div class="step-by-step"]
> [Předchozí](getting-started-with-mvc-part6.md)
> [Další](getting-started-with-mvc-part8.md)

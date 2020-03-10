---
uid: mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
title: Úvod do kurzu NerdDinner | Microsoft Docs
author: shanselman
description: Nejlepším způsobem, jak se naučit nové rozhraní, je vytvořit s ním něco. Tento kurz vás provede vytvořením malé, ale dokončené aplikace s využitím ASP.NE...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 397522d5-0402-4b94-b810-a2fb564f869d
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/introducing-the-nerddinner-tutorial
msc.type: authoredcontent
ms.openlocfilehash: 154cfe6694cf723c0a1f8e33bfdb42c97594518f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580575"
---
# <a name="introducing-the-nerddinner-tutorial"></a>Úvod do kurzu NerdDinner

[Scott Hanselman](https://github.com/shanselman)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Nejlepším způsobem, jak se naučit nové rozhraní, je vytvořit s ním něco. V tomto kurzu se dozvíte, jak vytvořit malou, ale ucelenou aplikaci s využitím ASP.NET MVC 1 a přináší některé základní koncepty.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme vám postupovat podle [Začínáme s kurzy pro](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [hudební úložiště](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) MVC 3 nebo MVC.

## <a name="nerddinner-tutorial"></a>Kurz k NerdDinner

Nejlepším způsobem, jak se naučit nové rozhraní, je vytvořit s ním něco. V tomto kurzu se dozvíte, jak vytvořit malou, ale ucelenou aplikaci s využitím ASP.NET MVC a přináší některé základní koncepty.

Aplikace, kterou se chystáme sestavit, se nazývá "NerdDinner". NerdDinner poskytuje snadný způsob, jak lidem najít a uspořádat večeři online:

![](introducing-the-nerddinner-tutorial/_static/image1.png)

NerdDinner umožňuje registrovaným uživatelům vytvářet, upravovat a odstraňovat večeře. Vynutila konzistentní sadu ověřovacích a obchodních pravidel napříč aplikací:

![](introducing-the-nerddinner-tutorial/_static/image2.png)

Návštěvníci můžou k hledání nadcházejících večeře v blízkosti použít mapu založenou na AJAX:

![](introducing-the-nerddinner-tutorial/_static/image3.png)

Kliknutím na večeři přejdete na stránku s podrobnostmi, na které se můžou dozvědět víc.

![](introducing-the-nerddinner-tutorial/_static/image4.png)

Pokud vás zajímá účast na večeři, můžou se na webu přihlásit nebo zaregistrovat:

![](introducing-the-nerddinner-tutorial/_static/image5.png)

Potom můžou kliknout na odkaz na protokol RSVP na základě AJAX a zúčastnit se události:

![](introducing-the-nerddinner-tutorial/_static/image6.png)

![](introducing-the-nerddinner-tutorial/_static/image7.png)

### <a name="implementing-nerddinner"></a>Implementace NerdDinner

Spustíme naši aplikaci NerdDinner pomocí příkazu soubor-&gt;nový projekt v sadě Visual Studio k vytvoření značky nového projektu ASP.NET MVC. Postupně budeme přidávat funkce a funkce. Jak pokryjeme:

1. [Vytvoření nového projektu ASP.NET MVC](create-a-new-aspnet-mvc-project.md)
2. [Vytvoření databáze](create-a-database.md)
3. [Jak vytvořit model s ověřováním obchodních pravidel](build-a-model-with-business-rule-validations.md)
4. [Použití řadičů a zobrazení k implementaci uživatelského rozhraní pro výpisy a podrobnosti](use-controllers-and-views-to-implement-a-listingdetails-ui.md)
5. [Jak poskytnout položku CRUD (vytvořit, číst, aktualizovat, odstranit) podporu zadávání datových formulářů](provide-crud-create-read-update-delete-data-form-entry-support.md)
6. [Jak používat ViewData a implementovat třídy ViewModel](use-viewdata-and-implement-viewmodel-classes.md)
7. [Postup opětovného použití uživatelského rozhraní pomocí stránek předlohy a částečně](re-use-ui-using-master-pages-and-partials.md)
8. [Implementace efektivního stránkování dat](implement-efficient-data-paging.md)
9. [Zabezpečení aplikací pomocí ověřování a autorizace](secure-applications-using-authentication-and-authorization.md)
10. [Použití jazyka AJAX k doručování dynamických aktualizací](use-ajax-to-deliver-dynamic-updates.md)
11. [Použití jazyka AJAX k implementaci scénářů mapování](use-ajax-to-implement-mapping-scenarios.md)
12. [Jak povolit automatizované testování částí](enable-automated-unit-testing.md)

Můžete vytvořit vlastní kopii NerdDinner od začátku, a to tak, že v této kapitole provedete všechny kroky. Případně můžete stáhnout dokončenou verzi zdrojového kódu zde: [NerdDinner na GitHubu](https://github.com/AspNetMVPSamples/NerdDinner). Pokud chcete tento kurz Přečtěte offline, můžete také volitelně [Stáhnout bezplatnou verzi tohoto kurzu ve formátu PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf) .

K sestavení aplikace můžete použít buď Visual Studio 2008, nebo bezplatný Visual Web Developer 2008 Express. Pro databázi můžete použít buď SQL Server, nebo bezplatný SQL Server Express.

ASP.NET MVC, Visual Web Developer 2008 Express a SQL Server Express (zdarma) můžete nainstalovat pomocí v2 [Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx)

### <a name="now-lets-get-started"></a>Pojďme začít....

Teď, když jsme pokryli, co je to NerdDinner, připravujeme naše rukávy a napíšeme kód.

Zahájíme použití souborového&gt;nového projektu v sadě Visual Studio k vytvoření aplikace v NerdDinner.

> [!div class="step-by-step"]
> [Next](create-a-new-aspnet-mvc-project.md)

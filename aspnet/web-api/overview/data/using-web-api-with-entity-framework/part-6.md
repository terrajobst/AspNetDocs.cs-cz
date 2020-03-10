---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-6
title: Vytvoření klienta JavaScriptu | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 20360326-b123-4b1e-abae-1d350edf4ce4
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-6
msc.type: authoredcontent
ms.openlocfilehash: 74f2cc4e5e401d690042b05b028dfc0c46ae282a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622344"
---
# <a name="create-the-javascript-client"></a>Vytvoření javascriptového klienta

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://github.com/MikeWasson/BookService)

V této části vytvoříte klienta pro aplikaci pomocí HTML, JavaScriptu a knihovny [vykrojení. js](http://knockoutjs.com/) . Vytvoříme klientskou aplikaci ve fázích:

- Zobrazuje se seznam knih.
- Zobrazení podrobností knihy.
- Přidává se nová kniha.

Knihovna vykrojení používá vzor Model-View-ViewModel (MVVM):

- **Model** je reprezentace dat v obchodní doméně (v našem případě v knihách a autorech) na straně serveru.
- **Zobrazení** je prezentační vrstva (HTML).
- **Model zobrazení** je objekt JavaScriptu, který obsahuje modely. Model zobrazení je abstrakcí kódu uživatelského rozhraní. Neobsahuje žádné znalosti reprezentace HTML. Místo toho představuje abstraktní funkce zobrazení, například &quot;seznam knih&quot;.

Zobrazení je vázáno na data pro model zobrazení. Aktualizace modelu zobrazení se automaticky projeví v zobrazení. Model zobrazení také načítá události ze zobrazení, například kliknutí na tlačítko.

![](part-6/_static/image1.png)

Tento přístup usnadňuje změnu rozložení a uživatelského rozhraní vaší aplikace, protože můžete změnit vazby bez nutnosti přepisovat kód. Můžete například zobrazit seznam položek jako `<ul>`a pak ho později změnit na tabulku.

## <a name="add-the-knockout-library"></a>Přidat vyseknutí knihovny

V aplikaci Visual Studio v nabídce **nástroje** vyberte **Správce balíčků NuGet**. Pak vyberte **Konzola správce balíčků**. V okně konzoly Správce balíčků zadejte následující příkaz:

[!code-console[Main](part-6/samples/sample1.cmd)]

Tento příkaz přidá soubory vykrojení do složky Scripts.

## <a name="create-the-view-model"></a>Vytvoření modelu zobrazení

Do složky Scripts přidejte soubor JavaScriptu s názvem App. js. (V Průzkumník řešení klikněte pravým tlačítkem myši na složku skripty, vyberte **Přidat**a pak vyberte **soubor JavaScriptu**.) Vložte následující kód:

[!code-javascript[Main](part-6/samples/sample2.js)]

V vykrojení třída `observable` povoluje datovou vazbu. Když obsah pozorovatelované změny, pozorovatelně upozorní všechny ovládací prvky vázané na data, aby se mohly aktualizovat sami. (Třída `observableArray` je verze pole, která se má *propozorovatelit*.) Aby bylo možné začít s, náš model zobrazení má dva observables:

- `books` obsahuje seznam knih.
- `error` obsahuje chybovou zprávu, pokud se volání jazyka AJAX nezdařilo.

Metoda `getAllBooks` provede volání AJAX pro získání seznamu knih. Poté výsledek vloží do pole `books`.

Metoda `ko.applyBindings` je součástí knihovny vyseknutí. Převezme model zobrazení jako parametr a nastaví datovou vazbu.

## <a name="add-a-script-bundle"></a>Přidání sady skriptů

Sdružování je funkce v ASP.NET 4,5, která usnadňuje kombinování nebo rozčlenění více souborů do jednoho souboru. Sdružování snižuje počet požadavků na server, což může zlepšit dobu načítání stránky.

Otevřete soubor App\_Start/BundleConfig. cs. Do metody RegisterBundles přidejte následující kód.

[!code-csharp[Main](part-6/samples/sample3.cs)]

> [!div class="step-by-step"]
> [Předchozí](part-5.md)
> [Další](part-7.md)

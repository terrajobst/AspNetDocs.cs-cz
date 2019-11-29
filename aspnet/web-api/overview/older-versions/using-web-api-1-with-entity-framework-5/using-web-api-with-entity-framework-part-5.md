---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: 'Část 5: vytvoření dynamického uživatelského rozhraní s vykrojení. js | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: bbdeba756de7986cfeb92aa10a57f4f101382f99
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600000"
---
# <a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a>Část 5: vytvoření dynamického uživatelského rozhraní pomocí vykrojení. js

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a>Vytvoření dynamického uživatelského rozhraní s knihovnou Knockout.js

V této části použijeme vyseknutí. js k přidání funkcí do zobrazení správce.

[Vykrojení. js](http://knockoutjs.com/) je knihovna JavaScriptu, která usnadňuje navázání ovládacích prvků HTML na data. Vyseknutí. js používá vzor Model-View-ViewModel (MVVM).

- *Model* je reprezentace dat v obchodní doméně (v našem případě produktů a objednávek) na straně serveru.
- *Zobrazení* je prezentační vrstva (HTML).
- *Model zobrazení* je JavaScriptový objekt, který uchovává data modelu. Model zobrazení je abstrakcí kódu uživatelského rozhraní. Neobsahuje žádné znalosti reprezentace HTML. Místo toho představuje abstraktní funkce zobrazení, jako je například seznam položek.

Zobrazení je vázáno na data na model zobrazení. Aktualizace zobrazení – model se automaticky projeví v zobrazení. Model zobrazení také získává události ze zobrazení, například kliknutí na tlačítko a provádí operace v modelu, například vytvoření objednávky.

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

Nejdřív definujeme model zobrazení. Následně navážeme značku HTML na model zobrazení.

Do správce. cshtml přidejte následující oddíl Razor:

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

Tuto část můžete přidat kdekoli v souboru. Po vykreslení zobrazení se část zobrazí v dolní části stránky HTML hned před uzavírací &lt;značka&gt;/body.

Všechny skripty pro tuto stránku se přejdou do značky skriptu označené komentářem:

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

Nejprve definujte třídu zobrazení-model:

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

**Ko. observableArray** je speciální druh objektu v vykrojení, který se nazývá *pozorovatelný*. Z [dokumentace k vyseknutí. js](http://knockoutjs.com/documentation/observables.html): pozorovatelný je objekt JavaScriptu, který může upozornit předplatitele na změny. Když je obsah pozorovatelované změny, zobrazení se automaticky aktualizuje tak, aby odpovídalo.

Chcete-li naplnit `products` pole, proveďte požadavek AJAX na webové rozhraní API. Odvoláme, že jsme uložili základní identifikátor URI pro rozhraní API v kontejneru zobrazení (viz [část 4](using-web-api-with-entity-framework-part-4.md) tohoto kurzu).

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

Dále přidejte funkce do zobrazení-model pro vytváření, aktualizaci a odstraňování produktů. Tyto funkce odesílají volání AJAX do webového rozhraní API a výsledky se používají k aktualizaci modelu zobrazení.

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

Teď nejdůležitější část: když je model DOM plně načtený, zavolejte funkci **Ko. applyBindings** a předejte novou instanci `ProductsViewModel`:

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

Metoda **Ko. applyBindings** aktivuje vykrojení a vodiče v zobrazení modelu zobrazení.

Teď, když máme model zobrazení, můžeme vytvořit vazby. V vykrojení. js to provedete přidáním atributů `data-bind` do elementů jazyka HTML. Chcete-li například svázat seznam HTML s polem, použijte `foreach` vazby:

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

Vazba `foreach` projde pole a vytvoří podřízené prvky pro každý objekt v poli. Vazby podřízených elementů mohou odkazovat na vlastnosti objektů Array.

Přidejte následující vazby do seznamu "aktualizace produktů":

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

Element `<li>` se vyskytuje v rámci rozsahu vazby **foreach** . To znamená, že vykrojení vykreslí prvek jednou pro každý produkt v poli `products`. Všechny vazby v rámci elementu `<li>` odkazují na tuto instanci produktu. `$data.Name` například odkazuje na vlastnost `Name` v produktu.

Chcete-li nastavit hodnoty textových vstupů, použijte `value` vazby. Tlačítka jsou svázána s funkcemi v zobrazení model pomocí `click` vazby. Instance produktu je předána do každé funkce jako parametr. Další informace naleznete v [dokumentaci vyseknutí. js](http://knockoutjs.com/documentation/observables.html) s dobrým popisem různých vazeb.

Dále přidejte vazbu pro událost **odeslání** ve formuláři přidat produkt:

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

Tato vazba volá funkci `create` v modelu zobrazení-model pro vytvoření nového produktu.

Tady je kompletní kód pro zobrazení Správce:

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

Spusťte aplikaci, přihlaste se pomocí účtu správce a klikněte na odkaz admin (správce). Měl by se zobrazit seznam produktů a může vytvářet, aktualizovat nebo odstraňovat produkty.

> [!div class="step-by-step"]
> [Předchozí](using-web-api-with-entity-framework-part-4.md)
> [Další](using-web-api-with-entity-framework-part-6.md)

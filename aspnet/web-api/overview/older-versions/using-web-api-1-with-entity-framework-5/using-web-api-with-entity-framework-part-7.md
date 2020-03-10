---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: '7\. část: vytvoření hlavní stránky | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: fe4074c701159a137be3644d65ca844f160c2399
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598677"
---
# <a name="part-7-creating-the-main-page"></a>7\. část: vytvoření hlavní stránky

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a>Vytvoření hlavní stránky

V této části vytvoříte hlavní stránku aplikace. Tato stránka bude složitější než stránka pro správu, takže se k ní přiblížíme několika kroky. V takovém případě uvidíte několik pokročilejších technik vyseknutí. js. Toto je základní rozložení stránky:

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- "Products" uchovává pole produktů.
- "Košík" obsahuje pole produktů s množstvím. Kliknutím na Přidat do košíku aktualizujete košík.
- "Orders" obsahuje pole ID objednávek.
- "Details" obsahuje podrobnosti objednávky, což je pole položek (produkty s množstvím).

Začneme definováním základního rozložení ve formátu HTML bez vazby dat nebo skriptu. Otevřete soubor views/Home/index. cshtml a nahraďte celý obsah následujícím způsobem:

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

Dále přidejte oddíl skripty a vytvořte prázdný model zobrazení:

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

V závislosti na návrhu, který jsme si vyznamenali dříve, náš model zobrazení potřebuje observables pro produkty, košík, objednávky a podrobnosti. Do objektu `AppViewModel` přidejte následující proměnné:

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

Uživatelé mohou přidat položky ze seznamu produktů do košíku a odebrat položky z košíku. Pokud chcete tyto funkce zapouzdřit, vytvoříme další třídu zobrazení-model reprezentující produkt. Přidejte následující kód pro `AppViewModel`:

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

Třída `ProductViewModel` obsahuje dvě funkce, které se používají k přesunu produktu do a ze vozíku: `addItemToCart` na vozík přidá jednu jednotku produktu a `removeAllFromCart` odstraní všechna množství produktu.

Uživatelé můžou vybrat existující objednávku a získat podrobnosti o objednávce. Tuto funkci zapouzdří do jiného zobrazení – model:

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

`OrderDetailsViewModel` je inicializována s objednávkou a načítá podrobnosti o objednávce odesláním požadavku AJAX na server.

Všimněte si také, že vlastnost `total` v `OrderDetailsViewModel`. Tato vlastnost je speciální druh, který je k pozorovateli, který se používá jako [vypočítaná](http://knockoutjs.com/documentation/computedObservables.html). Jak název implikuje, vypočítaná pozorovatel umožňuje vytvořit datovou vazby k vypočítané hodnotě&#8212;v tomto případě celková cena za objednávku.

Pak přidejte tyto funkce do `AppViewModel`:

- `resetCart` odebere všechny položky z košíku.
- `getDetails` Získá podrobnosti o objednávce (vložením nového `OrderDetailsViewModel` do seznamu `details`).
- `createOrder` vytvoří nové pořadí a vyprázdní košík.

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

Nakonec inicializujte model zobrazení tak, že provedete požadavky AJAX na produkty a objednávky:

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

OK, to je velké množství kódu, ale sestavili jsme ho krok za krokem, takže snad návrh je jasný. Nyní můžeme do kódu HTML přidat několik vazeb vyseknutí. js.

**Produkty**

Tady jsou vazby pro seznam produktů:

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

Tato iterace přechází přes pole Products a zobrazí název a cenu. Tlačítko Přidat do objednávky je viditelné pouze v případě, že je uživatel přihlášen.

Tlačítko "Přidat k objednávce" volá `addItemToCart` instance `ProductViewModel` pro daný produkt. Tím se ukazuje dobrá funkce vyseknutí. js: když model zobrazení obsahuje další modely zobrazení, můžete vazby použít na vnitřní model. V tomto příkladu jsou vazby v rámci `foreach` aplikovány na každou z `ProductViewModel` instancí. Tento přístup je mnohem čistší než všechny funkce do jediného modelu zobrazení.

**Nákupního**

Tady jsou vazby pro košík:

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

Tato iterace prochází přes pole vozíku a zobrazuje název, cenu a množství. Všimněte si, že odkaz odebrat a tlačítko vytvořit objednávku jsou svázané s funkcemi zobrazení modelu.

**Fakt**

Tady jsou vazby pro seznam objednávky:

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

Tato iterace projde objednávkami a zobrazí ID objednávky. Událost Click na odkazu je svázána s funkcí `getDetails`.

**Podrobnosti objednávky**

Tady jsou vazby pro podrobnosti objednávky:

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

Tím se prochází nad položkami v objednávce a zobrazuje produkt, cenu a množství. Okolní div je viditelné pouze v případě, že pole podrobností obsahuje jednu nebo více položek.

## <a name="conclusion"></a>Závěr

V tomto kurzu jste vytvořili aplikaci, která používá Entity Framework ke komunikaci s databází a webové rozhraní API ASP.NET k zajištění rozhraní, které se nachází na datové vrstvě jako veřejné. ASP.NET MVC 4 používáme k vykreslování stránek HTML a vyseknutí. js plus jQuery k poskytnutí dynamické interakce bez nutnosti opětovného načtení stránky.

Další zdroje informací:

- [Mapa obsahu ASP.NET Data Access](https://msdn.microsoft.com/library/6759sth4.aspx)
- [Centrum pro vývojáře Entity Framework](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [Předchozí](using-web-api-with-entity-framework-part-6.md)

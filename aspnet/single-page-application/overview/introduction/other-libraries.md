---
uid: single-page-application/overview/introduction/other-libraries
title: Znáte jiné knihovny než Knockout? | Dokumenty Microsoft
author: madskristensen
description: Znáte jiné knihovny než Knockout?
ms.author: riande
ms.date: 02/05/2013
ms.assetid: a8367c6d-ef94-4dff-a010-5eff9e6eea96
msc.legacyurl: /single-page-application/overview/introduction/other-libraries
msc.type: authoredcontent
ms.openlocfilehash: 64a4ad1fb411f7291a5cba634afdf4d2fdb16d55
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578545"
---
# <a name="know-a-library-other-than-knockout"></a>Znáte jiné knihovny než Knockout?

od [Madse Kristensena](https://github.com/madskristensen)

[Šablona jednostránkové aplikace (Spa)](knockoutjs-template.md) představuje skvělý způsob, jak začít psát jednostránkové aplikace. Šablona používá [KnockoutJS](http://knockoutjs.com/) k vázání dat aplikace k ELEMENTŮM modelu DOM.

Ale pro vytváření bohatých klientských aplikací není vykrojení jedinou knihovnou JavaScriptu. Jiné knihovny řeší podobné výzvy různými způsoby. Je možné, že jednu knihovnu upřednostňujete v jiném, takže jsme k dispozici několik šablon vytvořených komunitou ke stažení. Každá z těchto šablon používá jinou kombinaci klientských knihoven JavaScript.

Chcete-li nainstalovat šablonu vytvořenou komunitou, navštivte jednu z níže uvedených stránek šablony a klikněte na tlačítko Stáhnout. Šablony jsou k dispozici jako soubory VSIX.

## <a name="backbonejs"></a>BackboneJS

[Šablona hesla pro páteřní šablonu. js](../templates/backbonejs-template.md) Tato šablona poskytuje počáteční kostru pro vývoj aplikace v [páteřním formátu. js](http://backbonejs.org/) v ASP.NET MVC. Mimo pole poskytuje základní funkce pro přihlášení uživatelů, včetně registrace uživatelů, přihlášení, resetování hesla a potvrzení uživatele se základními e-mailovými šablonami.

## <a name="breezejs"></a>BreezeJS

[BreezeJS](http://www.breezejs.com/?utm_source=ms-spa) je open source knihovna pro správu bohatých dat v klientovi JavaScript. Breeze zpracovává dotazování, ukládání do mezipaměti, sledování změn, ověřování a další. Dvě šablony funkce Breeze:

- Šablona [Breeze/vykrojení](../templates/breezeknockout-template.md) rozšiřuje šablonu pro vyseknutí hesla, která ukazuje, jak snadno můžete vytvořit jednostránkovou aplikaci s Breeze pro správu dat a KnockoutJS pro vytváření datových vazeb.
- Šablona [Breeze/úhlová](../templates/breezeangular-template.md) také rozšiřuje šablonu zabezpečeného hesla pomocí Breeze, ale pomocí knihovny [AngularJS](http://angularjs.org) pro datové vazby, vkládání závislostí a správu obrazovky.

Kromě toho [Šablona Hot navrhování RUČNÍKŮ Spa](../templates/hottowel-template.md) používá BreezeJS.

## <a name="emberjs"></a>EmberJS

[Šablona zabezpečeného hesla EmberJS](../templates/emberjs-template.md) Tato šablona používá [života](http://emberjs.com/), výkonné knihovny JavaScript MVC, která řeší širokou škálu výzev pro vytváření bohatých klientských aplikací.

Šablona života SPA je znovu implementovaná šablona pro vyseknutí hesla pomocí EmberJS a handlebars šablonování.

## <a name="hot-towel"></a>Horká navrhování ručníků

[Hot navrhování RUČNÍKŮ Spa – šablona](../templates/hottowel-template.md). Tato šablona přináší několik knihoven JavaScriptu, včetně Breeze, vyseknutí, RequireJS a spuštění Twitteru.

V porovnání s dalšími šablonami, které jsou zde uvedeny, poskytuje Hot navrhování ručníků šablonu úplnější aplikaci, ze které můžete sestavit vlastní. Existuje více konceptů, o kterých byste měli vědět, ale jakmile je poznáte, může tato šablona přesně odpovídat tomu, co hledáte. Pokud chcete sestavit SPA, ale nemůžete se rozhodnout, kde začít, používejte horké navrhování ručníků a v sekundách budete mít zabezpečené a všechny nástroje, které pro něj budete potřebovat k sestavování.

## <a name="feature-table"></a>Tabulka funkcí

Tady jsou funkce poskytované každou šablonou SPA:

|                        | ASP.NET SPA | Páteřní | Breeze/úhlové | Breeze/KO |  Ember   | Horká navrhování ručníků |
|------------------------|-------------|----------|----------------|-----------|----------|-----------|
|      Ukázka ToDo       |  &#10003;   |          |    &#10003;    | &#10003;  | &#10003; |           |
|     Úplné šablony      |             | &#10003; |                |           |          | &#10003;  |
| Navigace a historie |             | &#10003; |    &#10003;    |           | &#10003; | &#10003;  |
|        Knihovny       |             |          |                |           |          |           |
|        Úhlová         |             |          |    &#10003;    |           |          |           |
|    &#8195;Páteřní     |             | &#10003; |                |           |          |           |
|         Breeze         |             |          |    &#10003;    | &#10003;  |          | &#10003;  |
|        durandal        |             |          |                |           |          | &#10003;  |
|         Ember          |             |          |                |           | &#10003; |           |
|        Tomuto        |  &#10003;   |          |                | &#10003;  |          | &#10003;  |

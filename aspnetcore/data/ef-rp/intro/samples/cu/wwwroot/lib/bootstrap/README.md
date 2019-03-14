---
ms.openlocfilehash: 3be420696add54094f24424285a905e7e7963bad
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57069364"
---
# <a name="bootstraphttpgetbootstrapcom"></a>[Bootstrap](http://getbootstrap.com)

[![Slack](https://bootstrap-slack.herokuapp.com/badge.svg)](https://bootstrap-slack.herokuapp.com)
![Bower verze](https://img.shields.io/bower/v/bootstrap.svg)
[![npm verze](https://img.shields.io/npm/v/bootstrap.svg)](https://www.npmjs.com/package/bootstrap)
[![stav sestavení](https://img.shields.io/travis/twbs/bootstrap/master.svg)](https://travis-ci.org/twbs/bootstrap) 
 [ ![devDependency stav](https://img.shields.io/david/dev/twbs/bootstrap.svg)](https://david-dm.org/twbs/bootstrap#info=devDependencies)
[![NuGet](https://img.shields.io/nuget/v/bootstrap.svg)](https://www.nuget.org/packages/Bootstrap)
[![stav testu Selenium](https://saucelabs.com/browser-matrix/bootstrap.svg)](https://saucelabs.com/u/bootstrap)

Bootstrap je rychlejší a jednodušší pro vývoj pro web, vytvořil Elegantní, intuitivní a výkonný front-endové rozhraní [označit Otto](https://twitter.com/mdo) a [Jakub Thornton](https://twitter.com/fat)a udržuje [základní týmu](https://github.com/orgs/twbs/people) s masivní podpory a účast v komunitě.

Abyste mohli začít, podívejte se na <http://getbootstrap.com>!


## <a name="table-of-contents"></a>Obsah

* [Rychlý start](#quick-start)
* [Chyby a žádostí o funkce](#bugs-and-feature-requests)
* [Dokumentace](#documentation)
* [Přispívání](#contributing)
* [Community](#community)
* [Správa verzí](#versioning)
* [Tvůrce](#creators)
* [Autorská práva a licence](#copyright-and-license)


## <a name="quick-start"></a>Rychlý start

Jsou k dispozici několik možností, jak rychlý start:

* [Stáhněte si nejnovější verzi](https://github.com/twbs/bootstrap/archive/v3.3.7.zip).
* Naklonujte úložiště: `git clone https://github.com/twbs/bootstrap.git`.
* Instalace pomocí [Bower](http://bower.io): `bower install bootstrap`.
* Instalace pomocí [npm](https://www.npmjs.com): `npm install bootstrap@3`.
* Instalace pomocí [meteor službě](https://www.meteor.com): `meteor add twbs:bootstrap`.
* Instalace pomocí [Composer](https://getcomposer.org): `composer require twbs/bootstrap`.

Čtení [stránku Začínáme](http://getbootstrap.com/getting-started/) informace o rozhraní framework obsah, šablony a příklady a další.

### <a name="whats-included"></a>Co je součástí

Ve staženém souboru najdete následující adresáře a soubory, logicky seskupení společných datových zdrojů a poskytuje i zkompilován a minifikovaný variace. Zobrazí se vám vypadat přibližně takto:

```
bootstrap/
├── css/
│   ├── bootstrap.css
│   ├── bootstrap.css.map
│   ├── bootstrap.min.css
│   ├── bootstrap.min.css.map
│   ├── bootstrap-theme.css
│   ├── bootstrap-theme.css.map
│   ├── bootstrap-theme.min.css
│   └── bootstrap-theme.min.css.map
├── js/
│   ├── bootstrap.js
│   └── bootstrap.min.js
└── fonts/
    ├── glyphicons-halflings-regular.eot
    ├── glyphicons-halflings-regular.svg
    ├── glyphicons-halflings-regular.ttf
    ├── glyphicons-halflings-regular.woff
    └── glyphicons-halflings-regular.woff2
```

Poskytujeme zkompilovaných šablon stylů CSS a JS (`bootstrap.*`), a jak je zkompilován a minifikovaný šablon stylů CSS a JS (`bootstrap.min.*`). Šablony stylů CSS [zdrojového mapování](https://developer.chrome.com/devtools/docs/css-preprocessors) (`bootstrap.*.map`) jsou k dispozici pro použití s nástroji pro vývoj některé prohlížeče. Písma z Glyphicons jsou zahrnuty, jako je volitelné motivu spuštění, který.


## <a name="bugs-and-feature-requests"></a>Chyby a žádostí o funkce

Máte chybu nebo žádost o funkci? Přečtěte si nejprve [vydat pokyny](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md#using-the-issue-tracker) a vyhledejte existující a uzavřené problémy. Pokud ještě, ale problém nebo podnětů [nový problém, otevřete prosím](https://github.com/twbs/bootstrap/issues/new).

Všimněte si, že **žádosti o funkce, musí jako cíl [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev),** protože Bootstrap v3 je nyní v režimu údržby a zavření vypnout k novým funkcím. Je to tak, aby se můžeme zaměřit naše úsilí na spuštění v4.


## <a name="documentation"></a>Dokumentace

Využívá rozhraní Bootstrap pro dokumentaci v tomto úložišti v kořenovém adresáři [Jekyll](http://jekyllrb.com) a veřejně hostované na stránkách Githubu v <http://getbootstrap.com>. Dokumenty můžou také spouštět místně.

### <a name="running-documentation-locally"></a>Místně spuštěná dokumentace

1. V případě potřeby [nainstalovat Jekyll](http://jekyllrb.com/docs/installation) a dalších poznámek Ruby závislostí s `bundle install`.
   **Poznámka: pro uživatele Windows:** Čtení [příručku neoficiální](http://jekyll-windows.juthilo.com/) pro uvedení do provozu Jekyll bez problémů.
2. Z kořenového adresáře `/bootstrap` adresáře, spusťte `bundle exec jekyll serve` na příkazovém řádku.
4. Otevřít `http://localhost:9001` ve svém prohlížeči a voilà.

Další informace o používání Jekyll načtením jeho [dokumentaci](http://jekyllrb.com/docs/home/).

### <a name="documentation-for-previous-releases"></a>Dokumentace ke službě pro dřívější verze

Dokumentace k v2.3.2 byl zpřístupněn prozatím v <http://getbootstrap.com/2.3.2/> při přechodu poprosil Bootstrap 3.

[Předchozí verze](https://github.com/twbs/bootstrap/releases) a jejich dokumentaci jsou také k dispozici ke stažení.


## <a name="contributing"></a>Přispívání

Přečtěte si prosím našich [přispívání pokyny](https://github.com/twbs/bootstrap/blob/master/CONTRIBUTING.md). Zahrnuty jsou pokyny pro otevření problémy kódování standardy a poznámky na vývoj.

Navíc pokud vaše žádost o přijetí změn obsahuje opravy JavaScript nebo funkce, je nutné zahrnout [odpovídající testy příslušných jednotek](https://github.com/twbs/bootstrap/tree/master/js/tests). Všechny HTML a CSS odpovídat [kód průvodce](https://github.com/mdo/code-guide), udržováno podle [označit Otto](https://github.com/mdo).

**Bootstrap v3 je teď uzavřen vypnout, aby nové funkce.** To přešel do režimu údržby tak, aby se můžeme zaměřit naše úsilí na [Bootstrap v4](https://github.com/twbs/bootstrap/tree/v4-dev), budoucnost rozhraní framework. Žádosti o přijetí změn, které přidávání nových funkcí (a ne opravovat chyby) zaměřit [Bootstrap v4 ( `v4-dev` větev git)](https://github.com/twbs/bootstrap/tree/v4-dev) místo.

Předvolby editoru jsou k dispozici v [editor konfigurace](https://github.com/twbs/bootstrap/blob/master/.editorconfig) pro snadné použití v běžných textových editorů. Další informace a Stáhnout moduly plug-in na <http://editorconfig.org>.


## <a name="community"></a>Komunita

Získáte aktualizace na Bootstrap pro vývoj a konverzace s projektu programu a členů komunity.

* Postupujte podle [ @getbootstrap na Twitteru](https://twitter.com/getbootstrap).
* Přečtěte si a přihlaste se k odběru [oficiálním blogu Bootstrap](http://blog.getbootstrap.com).
* Připojte se k [oficiální Slack místnosti](https://bootstrap-slack.herokuapp.com).
* Chat s fellow Bootstrapperů v IRC. Na `irc.freenode.net` serveru v `##bootstrap` kanálu.
* Implementace nápovědy najdete na webu Stack Overflow (označené [ `twitter-bootstrap-3` ](https://stackoverflow.com/questions/tagged/twitter-bootstrap-3)).
* Vývojáři měli použít klíčové slovo `bootstrap` na balíčky, které úprava nebo přidání funkcí Bootstrap při distribuci přes [npm](https://www.npmjs.com/browse/keyword/bootstrap) nebo podobné doručování mechanismy pro maximální zjistitelnost.


## <a name="versioning"></a>Správa verzí

Transparentnosti do našich cyklu vydávání verzí a uživatele pro zachování zpětné kompatibility se udržuje Bootstrap pod [pokyny Semantic Versioning](http://semver.org/). V některých případech můžeme Přišroubujte, ale můžeme budete dodržovat tato pravidla, kdykoli je to možné.

Zobrazit [část verze našich projektu z Githubu](https://github.com/twbs/bootstrap/releases) pro changelogs pro každou verzi Bootstrap. Verze oznámení příspěvky na [oficiálním blogu Bootstrap](http://blog.getbootstrap.com) obsahovat souhrny nejvíce zajímavosti změny provedené v jednotlivých verzích.


## <a name="creators"></a>Tvůrce

**Mark Otto**

* <https://twitter.com/mdo>
* <https://github.com/mdo>

**Jacob Thornton**

* <https://twitter.com/fat>
* <https://github.com/fat>


## <a name="copyright-and-license"></a>Autorská práva a licence

Kód a dokumentace o autorských právech 2011-2016 Twitter, Inc. Kód vydávaný v rámci [licencí MIT](https://github.com/twbs/bootstrap/blob/master/LICENSE). Dokumentace vydávaný v rámci [licence Creative Commons](https://github.com/twbs/bootstrap/blob/master/docs/LICENSE).

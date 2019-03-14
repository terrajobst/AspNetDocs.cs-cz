---
ms.openlocfilehash: 610b16b181422978dc143b95f28658bbdf177fdd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067096"
---
# <a name="jquery"></a>jQuery

> jQuery je rychlý, malé a plně funkční knihovna jazyka JavaScript.

Informace o tom, jak začít a jak pomocí jQuery, najdete v tématu [dokumentaci společnosti jQuery](http://api.jquery.com/).
Zdrojové soubory a problémů, najdete [jQuery úložiště](https://github.com/jquery/jquery).

Pokud upgrade, najdete [blogovém příspěvku o 3.3.1](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/). To zahrnuje významný rozdíl oproti předchozí verzi a čitelnější protokolu změn.

## <a name="including-jquery"></a>Včetně jQuery

Níže jsou uvedeny některé z nejběžnějších způsobů, jak přidat jQuery.

### <a name="browser"></a>Prohlížeč

#### <a name="script-tag"></a>Značka skriptu

```html
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
```

#### <a name="babel"></a>Babel

[Babel](http://babeljs.io/) je další generace kompilátor jazyka JavaScript. Jednou z funkcí je možnost použití modulů ES6/ES2015 teď, i když prohlížeče ještě tato funkce nativně nepodporují.

```js
import $ from "jquery";
```

#### <a name="browserifywebpack"></a>Browserify/Webpacku

Existuje několik způsobů, jak používat [Browserify](http://browserify.org/) a [Webpacku](https://webpack.github.io/). Další informace o použití těchto nástrojů najdete v dokumentaci k odpovídajícího projektu. Ve skriptu včetně jQuery bude obvykle vypadat například takto...

```js
var $ = require("jquery");
```

#### <a name="amd-asynchronous-module-definition"></a>AMD (asynchronního modulu definice)

AMD je modul formát pro prohlížeč integrované. Další informace, doporučujeme [require.js' dokumentace](http://requirejs.org/docs/whyamd.html).

```js
define(["jquery"], function($) {

});
```

### <a name="node"></a>Uzel

Zahrnout jQuery v [uzel](nodejs.org), nejprve nainstalujte pomocí npm.

```sh
npm install jquery
```

U jQuery pro práci v uzlu se vyžaduje oken s dokumentem. Protože žádný takový interval existuje nativně v uzlu, jedna může být imitace pomocí nástrojů, jako [jsdom](https://github.com/tmpvar/jsdom). To může být užitečné pro účely testování.

```js
require("jsdom").env("", function(err, window) {
    if (err) {
        console.error(err);
        return;
    }

    var $ = require("jquery")(window);
});
```

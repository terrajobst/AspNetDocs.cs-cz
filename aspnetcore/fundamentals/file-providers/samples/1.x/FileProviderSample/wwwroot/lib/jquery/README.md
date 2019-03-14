---
ms.openlocfilehash: 610b16b181422978dc143b95f28658bbdf177fdd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57067096"
---
# <a name="jquery"></a><span data-ttu-id="81dcc-101">jQuery</span><span class="sxs-lookup"><span data-stu-id="81dcc-101">jQuery</span></span>

> <span data-ttu-id="81dcc-102">jQuery je rychlý, malé a plně funkční knihovna jazyka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="81dcc-102">jQuery is a fast, small, and feature-rich JavaScript library.</span></span>

<span data-ttu-id="81dcc-103">Informace o tom, jak začít a jak pomocí jQuery, najdete v tématu [dokumentaci společnosti jQuery](http://api.jquery.com/).</span><span class="sxs-lookup"><span data-stu-id="81dcc-103">For information on how to get started and how to use jQuery, please see [jQuery's documentation](http://api.jquery.com/).</span></span>
<span data-ttu-id="81dcc-104">Zdrojové soubory a problémů, najdete [jQuery úložiště](https://github.com/jquery/jquery).</span><span class="sxs-lookup"><span data-stu-id="81dcc-104">For source files and issues, please visit the [jQuery repo](https://github.com/jquery/jquery).</span></span>

<span data-ttu-id="81dcc-105">Pokud upgrade, najdete [blogovém příspěvku o 3.3.1](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/).</span><span class="sxs-lookup"><span data-stu-id="81dcc-105">If upgrading, please see the [blog post for 3.3.1](https://blog.jquery.com/2017/03/20/jquery-3.3.1-now-available/).</span></span> <span data-ttu-id="81dcc-106">To zahrnuje významný rozdíl oproti předchozí verzi a čitelnější protokolu změn.</span><span class="sxs-lookup"><span data-stu-id="81dcc-106">This includes notable differences from the previous version and a more readable changelog.</span></span>

## <a name="including-jquery"></a><span data-ttu-id="81dcc-107">Včetně jQuery</span><span class="sxs-lookup"><span data-stu-id="81dcc-107">Including jQuery</span></span>

<span data-ttu-id="81dcc-108">Níže jsou uvedeny některé z nejběžnějších způsobů, jak přidat jQuery.</span><span class="sxs-lookup"><span data-stu-id="81dcc-108">Below are some of the most common ways to include jQuery.</span></span>

### <a name="browser"></a><span data-ttu-id="81dcc-109">Prohlížeč</span><span class="sxs-lookup"><span data-stu-id="81dcc-109">Browser</span></span>

#### <a name="script-tag"></a><span data-ttu-id="81dcc-110">Značka skriptu</span><span class="sxs-lookup"><span data-stu-id="81dcc-110">Script tag</span></span>

```html
<script src="https://code.jquery.com/jquery-3.3.1.min.js"></script>
```

#### <a name="babel"></a><span data-ttu-id="81dcc-111">Babel</span><span class="sxs-lookup"><span data-stu-id="81dcc-111">Babel</span></span>

<span data-ttu-id="81dcc-112">[Babel](http://babeljs.io/) je další generace kompilátor jazyka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="81dcc-112">[Babel](http://babeljs.io/) is a next generation JavaScript compiler.</span></span> <span data-ttu-id="81dcc-113">Jednou z funkcí je možnost použití modulů ES6/ES2015 teď, i když prohlížeče ještě tato funkce nativně nepodporují.</span><span class="sxs-lookup"><span data-stu-id="81dcc-113">One of the features is the ability to use ES6/ES2015 modules now, even though browsers do not yet support this feature natively.</span></span>

```js
import $ from "jquery";
```

#### <a name="browserifywebpack"></a><span data-ttu-id="81dcc-114">Browserify/Webpacku</span><span class="sxs-lookup"><span data-stu-id="81dcc-114">Browserify/Webpack</span></span>

<span data-ttu-id="81dcc-115">Existuje několik způsobů, jak používat [Browserify](http://browserify.org/) a [Webpacku](https://webpack.github.io/).</span><span class="sxs-lookup"><span data-stu-id="81dcc-115">There are several ways to use [Browserify](http://browserify.org/) and [Webpack](https://webpack.github.io/).</span></span> <span data-ttu-id="81dcc-116">Další informace o použití těchto nástrojů najdete v dokumentaci k odpovídajícího projektu.</span><span class="sxs-lookup"><span data-stu-id="81dcc-116">For more information on using these tools, please refer to the corresponding project's documention.</span></span> <span data-ttu-id="81dcc-117">Ve skriptu včetně jQuery bude obvykle vypadat například takto...</span><span class="sxs-lookup"><span data-stu-id="81dcc-117">In the script, including jQuery will usually look like this...</span></span>

```js
var $ = require("jquery");
```

#### <a name="amd-asynchronous-module-definition"></a><span data-ttu-id="81dcc-118">AMD (asynchronního modulu definice)</span><span class="sxs-lookup"><span data-stu-id="81dcc-118">AMD (Asynchronous Module Definition)</span></span>

<span data-ttu-id="81dcc-119">AMD je modul formát pro prohlížeč integrované.</span><span class="sxs-lookup"><span data-stu-id="81dcc-119">AMD is a module format built for the browser.</span></span> <span data-ttu-id="81dcc-120">Další informace, doporučujeme [require.js' dokumentace](http://requirejs.org/docs/whyamd.html).</span><span class="sxs-lookup"><span data-stu-id="81dcc-120">For more information, we recommend [require.js' documentation](http://requirejs.org/docs/whyamd.html).</span></span>

```js
define(["jquery"], function($) {

});
```

### <a name="node"></a><span data-ttu-id="81dcc-121">Uzel</span><span class="sxs-lookup"><span data-stu-id="81dcc-121">Node</span></span>

<span data-ttu-id="81dcc-122">Zahrnout jQuery v [uzel](nodejs.org), nejprve nainstalujte pomocí npm.</span><span class="sxs-lookup"><span data-stu-id="81dcc-122">To include jQuery in [Node](nodejs.org), first install with npm.</span></span>

```sh
npm install jquery
```

<span data-ttu-id="81dcc-123">U jQuery pro práci v uzlu se vyžaduje oken s dokumentem.</span><span class="sxs-lookup"><span data-stu-id="81dcc-123">For jQuery to work in Node, a window with a document is required.</span></span> <span data-ttu-id="81dcc-124">Protože žádný takový interval existuje nativně v uzlu, jedna může být imitace pomocí nástrojů, jako [jsdom](https://github.com/tmpvar/jsdom).</span><span class="sxs-lookup"><span data-stu-id="81dcc-124">Since no such window exists natively in Node, one can be mocked by tools such as [jsdom](https://github.com/tmpvar/jsdom).</span></span> <span data-ttu-id="81dcc-125">To může být užitečné pro účely testování.</span><span class="sxs-lookup"><span data-stu-id="81dcc-125">This can be useful for testing purposes.</span></span>

```js
require("jsdom").env("", function(err, window) {
    if (err) {
        console.error(err);
        return;
    }

    var $ = require("jquery")(window);
});
```

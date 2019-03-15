---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57078121"
---
<a name="open-iconic-v111httpuseiconiccomopen"></a>[Otevřete Ikonickým verze 1.1.1](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconichttpuseiconiccom-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collectionhttpuseiconiccomopenicons"></a>Otevřít Iconic je na stejné opensourcové nástroje [Iconic](http://useiconic.com). Jde o hyper čitelné kolekci 223 ikon s malými nároky na paměť&mdash;připravený k použití s Bootstrap a Foundation. [Zobrazení kolekce](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a>Co je v programu Open Ikonickým?

* 223 ikony, které jsou navržené tak, aby se čitelné až 8 pixelech
* Mimořádně světla soubory SVG - 61.8 pro celou sadu 
* SVG sprite&mdash;moderní náhrada ikona písma
* Webfont (EOT, OTF, SVG, písem TTF, WOFF) a PNG, WebP formáty
* Webfont šablony stylů (včetně verzí pro spuštění a Foundation) v jazyce CSS, méně, SCSS a Stylus formáty
* PNG a WebP rastrové obrázky v 8px, 16px, 24px, 32px, 48px a 64px.


## <a name="getting-started"></a>Začínáme

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-iconshttpuseiconiccomopenicons-and-referencehttpuseiconiccomopenreference-sections"></a>Ukázky kódu a všechno ostatní je potřeba začít pracovat s Open ikony, podívejte se na naše [ikony](http://useiconic.com/open#icons) a [odkaz](http://useiconic.com/open#reference) oddíly.

### <a name="general-usage"></a>Obecné použití

#### <a name="using-open-iconics-svgs"></a>Pomocí SVGs Open ikony.

Rádi SVGs a myslíme si, že jsou to způsob, jak zobrazit ikony na webu. Vzhledem k tomu, že otevřete ikony jsou pouze základní SVGs, doporučujeme je zobrazit stejně, jako byste jiného obrázku (nezapomeňte `alt` atributu).

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a>Pomocí Sprite SVG Open ikony.

Otevřít Iconic je dostupná také v sprite SVG, který umožňuje zobrazit všechny ikony v sadě jedním požadavkem. Je to jako ikonu písmo, aniž by musel pracovat vyzkouším.

Přidání ikony ze SVG sprite je trochu jiné, než jaký jste zvyklí, ale je stále dort. *Tip: Chcete-li ikony snadno styl možné, doporučujeme přidání obecné třídy k* `<svg>` *značku a jedinečný název třídy pro každou jinou ikonu v* `<use>` *značky.*  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

Velikost ikony musí jen základní šablony stylů CSS. Všechny ikony jsou ve formátu čtvereček, takže stačí nastavit `<svg>` značka s stejné rozměry šířky a výšky.

```
.icon {
  width: 16px;
  height: 16px;
}
```

Barevné zvýrazňování ikony je ještě snadnější. Všechno, co potřebujete udělat je nastavena `fill` pravidla u `<use>` značky.

```
.icon-account-login {
  fill: #f00;
}
```

Další informace o prvky, které budou SVG, [Chris Coyier průvodce](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).

#### <a name="using-open-iconics-icon-font"></a>Pomocí Open ikony ikona písma...


##### <a name="with-bootstrap"></a>...nehody bootstrap

Můžete najít v našich spuštění šablony stylů `font/css/open-iconic-bootstrap.{css, less, scss, styl}`


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a>...nehody foundation

Můžete najít naše šablony stylů Foundation v `font/css/open-iconic-foundation.{css, less, scss, styl}`

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a>...Po zobrazení obrazovky vlastní

Můžete najít naší výchozí šablony stylů v `font/css/open-iconic.{css, less, scss, styl}`

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a>Licence

### <a name="icons"></a>Ikony

Veškerý kód (včetně SVG značek) je v části [licencí MIT](http://opensource.org/licenses/MIT).

### <a name="fonts"></a>Písma

Všechna písma se v části [licenci SIL](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).

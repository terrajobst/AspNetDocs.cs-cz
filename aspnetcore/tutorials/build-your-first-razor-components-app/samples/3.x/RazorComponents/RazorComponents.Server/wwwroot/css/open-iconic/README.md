---
ms.openlocfilehash: 3965884c8e0d7116f5d8a42e6aefb0dc5be94f1e
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57078121"
---
<a name="open-iconic-v111httpuseiconiccomopen"></a>[<span data-ttu-id="b7142-101">Otevřete Ikonickým verze 1.1.1</span><span class="sxs-lookup"><span data-stu-id="b7142-101">Open Iconic v1.1.1</span></span>](http://useiconic.com/open)
===========

### <a name="open-iconic-is-the-open-source-sibling-of-iconichttpuseiconiccom-it-is-a-hyper-legible-collection-of-223-icons-with-a-tiny-footprintmdashready-to-use-with-bootstrap-and-foundation-view-the-collectionhttpuseiconiccomopenicons"></a><span data-ttu-id="b7142-102">Otevřít Iconic je na stejné opensourcové nástroje [Iconic](http://useiconic.com).</span><span class="sxs-lookup"><span data-stu-id="b7142-102">Open Iconic is the open source sibling of [Iconic](http://useiconic.com).</span></span> <span data-ttu-id="b7142-103">Jde o hyper čitelné kolekci 223 ikon s malými nároky na paměť&mdash;připravený k použití s Bootstrap a Foundation.</span><span class="sxs-lookup"><span data-stu-id="b7142-103">It is a hyper-legible collection of 223 icons with a tiny footprint&mdash;ready to use with Bootstrap and Foundation.</span></span> [<span data-ttu-id="b7142-104">Zobrazení kolekce</span><span class="sxs-lookup"><span data-stu-id="b7142-104">View the collection</span></span>](http://useiconic.com/open#icons)



## <a name="whats-in-open-iconic"></a><span data-ttu-id="b7142-105">Co je v programu Open Ikonickým?</span><span class="sxs-lookup"><span data-stu-id="b7142-105">What's in Open Iconic?</span></span>

* <span data-ttu-id="b7142-106">223 ikony, které jsou navržené tak, aby se čitelné až 8 pixelech</span><span class="sxs-lookup"><span data-stu-id="b7142-106">223 icons designed to be legible down to 8 pixels</span></span>
* <span data-ttu-id="b7142-107">Mimořádně světla soubory SVG - 61.8 pro celou sadu</span><span class="sxs-lookup"><span data-stu-id="b7142-107">Super-light SVG files - 61.8 for the entire set</span></span> 
* <span data-ttu-id="b7142-108">SVG sprite&mdash;moderní náhrada ikona písma</span><span class="sxs-lookup"><span data-stu-id="b7142-108">SVG sprite&mdash;the modern replacement for icon fonts</span></span>
* <span data-ttu-id="b7142-109">Webfont (EOT, OTF, SVG, písem TTF, WOFF) a PNG, WebP formáty</span><span class="sxs-lookup"><span data-stu-id="b7142-109">Webfont (EOT, OTF, SVG, TTF, WOFF), PNG and WebP formats</span></span>
* <span data-ttu-id="b7142-110">Webfont šablony stylů (včetně verzí pro spuštění a Foundation) v jazyce CSS, méně, SCSS a Stylus formáty</span><span class="sxs-lookup"><span data-stu-id="b7142-110">Webfont stylesheets (including versions for Bootstrap and Foundation) in CSS, LESS, SCSS and Stylus formats</span></span>
* <span data-ttu-id="b7142-111">PNG a WebP rastrové obrázky v 8px, 16px, 24px, 32px, 48px a 64px.</span><span class="sxs-lookup"><span data-stu-id="b7142-111">PNG and WebP raster images in 8px, 16px, 24px, 32px, 48px and 64px.</span></span>


## <a name="getting-started"></a><span data-ttu-id="b7142-112">Začínáme</span><span class="sxs-lookup"><span data-stu-id="b7142-112">Getting Started</span></span>

#### <a name="for-code-samples-and-everything-else-you-need-to-get-started-with-open-iconic-check-out-our-iconshttpuseiconiccomopenicons-and-referencehttpuseiconiccomopenreference-sections"></a><span data-ttu-id="b7142-113">Ukázky kódu a všechno ostatní je potřeba začít pracovat s Open ikony, podívejte se na naše [ikony](http://useiconic.com/open#icons) a [odkaz](http://useiconic.com/open#reference) oddíly.</span><span class="sxs-lookup"><span data-stu-id="b7142-113">For code samples and everything else you need to get started with Open Iconic, check out our [Icons](http://useiconic.com/open#icons) and [Reference](http://useiconic.com/open#reference) sections.</span></span>

### <a name="general-usage"></a><span data-ttu-id="b7142-114">Obecné použití</span><span class="sxs-lookup"><span data-stu-id="b7142-114">General Usage</span></span>

#### <a name="using-open-iconics-svgs"></a><span data-ttu-id="b7142-115">Pomocí SVGs Open ikony.</span><span class="sxs-lookup"><span data-stu-id="b7142-115">Using Open Iconic's SVGs</span></span>

<span data-ttu-id="b7142-116">Rádi SVGs a myslíme si, že jsou to způsob, jak zobrazit ikony na webu.</span><span class="sxs-lookup"><span data-stu-id="b7142-116">We like SVGs and we think they're the way to display icons on the web.</span></span> <span data-ttu-id="b7142-117">Vzhledem k tomu, že otevřete ikony jsou pouze základní SVGs, doporučujeme je zobrazit stejně, jako byste jiného obrázku (nezapomeňte `alt` atributu).</span><span class="sxs-lookup"><span data-stu-id="b7142-117">Since Open Iconic are just basic SVGs, we suggest you display them like you would any other image (don't forget the `alt` attribute).</span></span>

```
<img src="/open-iconic/svg/icon-name.svg" alt="icon name">
```

#### <a name="using-open-iconics-svg-sprite"></a><span data-ttu-id="b7142-118">Pomocí Sprite SVG Open ikony.</span><span class="sxs-lookup"><span data-stu-id="b7142-118">Using Open Iconic's SVG Sprite</span></span>

<span data-ttu-id="b7142-119">Otevřít Iconic je dostupná také v sprite SVG, který umožňuje zobrazit všechny ikony v sadě jedním požadavkem.</span><span class="sxs-lookup"><span data-stu-id="b7142-119">Open Iconic also comes in a SVG sprite which allows you to display all the icons in the set with a single request.</span></span> <span data-ttu-id="b7142-120">Je to jako ikonu písmo, aniž by musel pracovat vyzkouším.</span><span class="sxs-lookup"><span data-stu-id="b7142-120">It's like an icon font, without being a hack.</span></span>

<span data-ttu-id="b7142-121">Přidání ikony ze SVG sprite je trochu jiné, než jaký jste zvyklí, ale je stále dort.</span><span class="sxs-lookup"><span data-stu-id="b7142-121">Adding an icon from an SVG sprite is a little different than what you're used to, but it's still a piece of cake.</span></span> <span data-ttu-id="b7142-122">*Tip: Chcete-li ikony snadno styl možné, doporučujeme přidání obecné třídy k* `<svg>` *značku a jedinečný název třídy pro každou jinou ikonu v* `<use>` *značky.*</span><span class="sxs-lookup"><span data-stu-id="b7142-122">*Tip: To make your icons easily style able, we suggest adding a general class to the* `<svg>` *tag and a unique class name for each different icon in the* `<use>` *tag.*</span></span>  

```
<svg class="icon">
  <use xlink:href="open-iconic.svg#account-login" class="icon-account-login"></use>
</svg>
```

<span data-ttu-id="b7142-123">Velikost ikony musí jen základní šablony stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="b7142-123">Sizing icons only needs basic CSS.</span></span> <span data-ttu-id="b7142-124">Všechny ikony jsou ve formátu čtvereček, takže stačí nastavit `<svg>` značka s stejné rozměry šířky a výšky.</span><span class="sxs-lookup"><span data-stu-id="b7142-124">All the icons are in a square format, so just set the `<svg>` tag with equal width and height dimensions.</span></span>

```
.icon {
  width: 16px;
  height: 16px;
}
```

<span data-ttu-id="b7142-125">Barevné zvýrazňování ikony je ještě snadnější.</span><span class="sxs-lookup"><span data-stu-id="b7142-125">Coloring icons is even easier.</span></span> <span data-ttu-id="b7142-126">Všechno, co potřebujete udělat je nastavena `fill` pravidla u `<use>` značky.</span><span class="sxs-lookup"><span data-stu-id="b7142-126">All you need to do is set the `fill` rule on the `<use>` tag.</span></span>

```
.icon-account-login {
  fill: #f00;
}
```

<span data-ttu-id="b7142-127">Další informace o prvky, které budou SVG, [Chris Coyier průvodce](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).</span><span class="sxs-lookup"><span data-stu-id="b7142-127">To learn more about SVG Sprites, read [Chris Coyier's guide](http://css-tricks.com/svg-sprites-use-better-icon-fonts/).</span></span>

#### <a name="using-open-iconics-icon-font"></a><span data-ttu-id="b7142-128">Pomocí Open ikony ikona písma...</span><span class="sxs-lookup"><span data-stu-id="b7142-128">Using Open Iconic's Icon Font...</span></span>


##### <a name="with-bootstrap"></a><span data-ttu-id="b7142-129">...nehody bootstrap</span><span class="sxs-lookup"><span data-stu-id="b7142-129">…with Bootstrap</span></span>

<span data-ttu-id="b7142-130">Můžete najít v našich spuštění šablony stylů `font/css/open-iconic-bootstrap.{css, less, scss, styl}`</span><span class="sxs-lookup"><span data-stu-id="b7142-130">You can find our Bootstrap stylesheets in `font/css/open-iconic-bootstrap.{css, less, scss, styl}`</span></span>


```
<link href="/open-iconic/font/css/open-iconic-bootstrap.css" rel="stylesheet">
```


```
<span class="oi oi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="with-foundation"></a><span data-ttu-id="b7142-131">...nehody foundation</span><span class="sxs-lookup"><span data-stu-id="b7142-131">…with Foundation</span></span>

<span data-ttu-id="b7142-132">Můžete najít naše šablony stylů Foundation v `font/css/open-iconic-foundation.{css, less, scss, styl}`</span><span class="sxs-lookup"><span data-stu-id="b7142-132">You can find our Foundation stylesheets in `font/css/open-iconic-foundation.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic-foundation.css" rel="stylesheet">
```


```
<span class="fi-icon-name" title="icon name" aria-hidden="true"></span>
```

##### <a name="on-its-own"></a><span data-ttu-id="b7142-133">...Po zobrazení obrazovky vlastní</span><span class="sxs-lookup"><span data-stu-id="b7142-133">…on its own</span></span>

<span data-ttu-id="b7142-134">Můžete najít naší výchozí šablony stylů v `font/css/open-iconic.{css, less, scss, styl}`</span><span class="sxs-lookup"><span data-stu-id="b7142-134">You can find our default stylesheets in `font/css/open-iconic.{css, less, scss, styl}`</span></span>

```
<link href="/open-iconic/font/css/open-iconic.css" rel="stylesheet">
```

```
<span class="oi" data-glyph="icon-name" title="icon name" aria-hidden="true"></span>
```


## <a name="license"></a><span data-ttu-id="b7142-135">Licence</span><span class="sxs-lookup"><span data-stu-id="b7142-135">License</span></span>

### <a name="icons"></a><span data-ttu-id="b7142-136">Ikony</span><span class="sxs-lookup"><span data-stu-id="b7142-136">Icons</span></span>

<span data-ttu-id="b7142-137">Veškerý kód (včetně SVG značek) je v části [licencí MIT](http://opensource.org/licenses/MIT).</span><span class="sxs-lookup"><span data-stu-id="b7142-137">All code (including SVG markup) is under the [MIT License](http://opensource.org/licenses/MIT).</span></span>

### <a name="fonts"></a><span data-ttu-id="b7142-138">Písma</span><span class="sxs-lookup"><span data-stu-id="b7142-138">Fonts</span></span>

<span data-ttu-id="b7142-139">Všechna písma se v části [licenci SIL](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).</span><span class="sxs-lookup"><span data-stu-id="b7142-139">All fonts are under the [SIL Licensed](http://scripts.sil.org/cms/scripts/page.php?item_id=OFL_web).</span></span>

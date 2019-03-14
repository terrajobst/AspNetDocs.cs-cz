---
title: Menší, Sass a knihovnou aplikací Font Awesome v ASP.NET Core
author: ardalis
description: Další informace o použití nižší, Sass a knihovnou aplikací Font Awesome v aplikacích ASP.NET Core.
ms.author: tdykstra
ms.date: 10/14/2016
uid: client-side/less-sass-fa
ms.openlocfilehash: 2229c4e3b0238ff17c15e78f657b9acb10495c72
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57078334"
---
# <a name="less-sass-and-font-awesome-in-aspnet-core"></a><span data-ttu-id="377e4-103">Menší, Sass a knihovnou aplikací Font Awesome v ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="377e4-103">Less, Sass, and Font Awesome in ASP.NET Core</span></span>

<span data-ttu-id="377e4-104">Podle [Steve Smith](https://ardalis.com/)</span><span class="sxs-lookup"><span data-stu-id="377e4-104">By [Steve Smith](https://ardalis.com/)</span></span>

<span data-ttu-id="377e4-105">Uživatelé webových aplikací mají stále vysoká očekávání při rozhodování o stylu a celkové prostředí.</span><span class="sxs-lookup"><span data-stu-id="377e4-105">Users of web applications have increasingly high expectations when it comes to style and overall experience.</span></span> <span data-ttu-id="377e4-106">Moderní webové aplikace často využívat bohaté možnosti nástrojů a architektur definují a spravují jejich vzhled a chování konzistentním způsobem.</span><span class="sxs-lookup"><span data-stu-id="377e4-106">Modern web applications frequently leverage rich tools and frameworks for defining and managing their look and feel in a consistent manner.</span></span> <span data-ttu-id="377e4-107">Architektury, jako jsou [Bootstrap](http://getbootstrap.com/) můžete urazily dlouhou cestu k definování společnou sadu – styly a možnosti rozložení pro weby.</span><span class="sxs-lookup"><span data-stu-id="377e4-107">Frameworks like [Bootstrap](http://getbootstrap.com/) can go a long way toward defining a common set of styles and layout options for web sites.</span></span> <span data-ttu-id="377e4-108">Většina serverů nejsou v netriviálních však také těžit z dokáže efektivně definovat a udržovat stylů a soubory kaskádových stylů (CSS) a také snadný přístup k ikony bitové kopie, které pomůžou intuitivnější rozhraní webu.</span><span class="sxs-lookup"><span data-stu-id="377e4-108">However, most non-trivial sites also benefit from being able to effectively define and maintain styles and cascading style sheet (CSS) files, as well as having easy access to non-image icons that help make the site's interface more intuitive.</span></span> <span data-ttu-id="377e4-109">Tam se jazyky a nástroje, které podporují [méně](http://lesscss.org/) a [Sass](http://sass-lang.com/), a knihoven, jako jsou [knihovnou aplikací Font Awesome](http://fontawesome.io/), se dělí na.</span><span class="sxs-lookup"><span data-stu-id="377e4-109">That's where languages and tools that support [Less](http://lesscss.org/) and [Sass](http://sass-lang.com/), and libraries like [Font Awesome](http://fontawesome.io/), come in.</span></span>

## <a name="css-preprocessor-languages"></a><span data-ttu-id="377e4-110">Preprocesor jazyků šablon stylů CSS</span><span class="sxs-lookup"><span data-stu-id="377e4-110">CSS preprocessor languages</span></span>

<span data-ttu-id="377e4-111">Jazyky, které jsou kompilovány do jiných jazyků, za účelem zlepšení možností práce s základní jazyk, se označují jako preprocesory.</span><span class="sxs-lookup"><span data-stu-id="377e4-111">Languages that are compiled into other languages, in order to improve the experience of working with the underlying language, are referred to as preprocessors.</span></span> <span data-ttu-id="377e4-112">Existují dvě oblíbené preprocesory pro šablony stylů CSS: Menší a Sass.</span><span class="sxs-lookup"><span data-stu-id="377e4-112">There are two popular preprocessors for CSS: Less and Sass.</span></span>  <span data-ttu-id="377e4-113">Tyto preprocesory přidat funkce do šablony stylů CSS, jako třeba podporu pro proměnné a vnořené pravidla, která zlepšit udržovatelnosti velké a komplexní šablony stylů.</span><span class="sxs-lookup"><span data-stu-id="377e4-113">These preprocessors add features to CSS, such as support for variables and nested rules, which improve the maintainability of large, complex stylesheets.</span></span> <span data-ttu-id="377e4-114">Šablon stylů CSS jako jazyk je velmi základní chybí podporu ještě něco stejně jednoduché jako proměnné, a to může vytvořit soubory šablon stylů CSS opakující se a opakovaném.</span><span class="sxs-lookup"><span data-stu-id="377e4-114">CSS as a language is very basic, lacking support even for something as simple as variables, and this tends to make CSS files repetitive and bloated.</span></span> <span data-ttu-id="377e4-115">Přidání funkcí reálné programovacích jazyků přes preprocesory můžou pomoct snížit duplikace a poskytují lepší uspořádání pravidel stylů.</span><span class="sxs-lookup"><span data-stu-id="377e4-115">Adding real programming language features via preprocessors can help reduce duplication and provide better organization of styling rules.</span></span> <span data-ttu-id="377e4-116">Visual Studio poskytuje integrovanou podporu pro obě Less a Sass, jakož i rozšíření, která ještě vylepšit vývojové prostředí při práci s těchto jazyků.</span><span class="sxs-lookup"><span data-stu-id="377e4-116">Visual Studio provides built-in support for both Less and Sass, as well as extensions that can further improve the development experience when working with these languages.</span></span>

<span data-ttu-id="377e4-117">Jako krátká ukázka toho, jak preprocesory zlepšit čitelnost a udržovatelnosti informací o stylu vezměte v úvahu CSS:</span><span class="sxs-lookup"><span data-stu-id="377e4-117">As a quick example of how preprocessors can improve readability and maintainability of style information, consider this CSS:</span></span>

```css
.header {
    color: black;
    font-weight: bold;
    font-size: 18px;
    font-family: Helvetica, Arial, sans-serif;
}

.small-header {
    color: black;
    font-weight: bold;
    font-size: 14px;
    font-family: Helvetica, Arial, sans-serif;
}
```

<span data-ttu-id="377e4-118">Použití nižší, to může být přepsán Chcete-li odstranit všechny duplicity, pomocí *mixin* (tedy s názvem, protože umožňuje "kombinovat" vlastnosti z jedné třídy nebo sada pravidel do jiné):</span><span class="sxs-lookup"><span data-stu-id="377e4-118">Using Less, this can be rewritten to eliminate all of the duplication, using a *mixin* (so named because it allows you to "mix in" properties from one class or rule-set into another):</span></span>

```less
.header {
    color: black;
    font-weight: bold;
    font-size: 18px;
    font-family: Helvetica, Arial, sans-serif;
}

.small-header {
    .header;
    font-size: 14px;
}
```

## <a name="less"></a><span data-ttu-id="377e4-119">méně</span><span class="sxs-lookup"><span data-stu-id="377e4-119">Less</span></span>

<span data-ttu-id="377e4-120">Spuštění preprocesoru méně šablon stylů CSS pomocí Node.js.</span><span class="sxs-lookup"><span data-stu-id="377e4-120">The Less CSS preprocessor runs using Node.js.</span></span> <span data-ttu-id="377e4-121">K instalaci menší, pomocí Node Package Manageru (npm) z příkazového řádku (-g znamená "globální"):</span><span class="sxs-lookup"><span data-stu-id="377e4-121">To install Less, use Node Package Manager (npm) from a command prompt (-g means "global"):</span></span>

```console
npm install -g less
```

<span data-ttu-id="377e4-122">Pokud používáte Visual Studio, můžete začít s menší přidáním jednoho nebo více méně souborů do projektu a pak nakonfigurujete Gulp (ani Grunt) ke zpracování v době kompilace.</span><span class="sxs-lookup"><span data-stu-id="377e4-122">If you're using Visual Studio, you can get started with Less by adding one or more Less files to your project, and then configuring Gulp (or Grunt) to process them at compile-time.</span></span> <span data-ttu-id="377e4-123">Přidat *styly* složku pro váš projekt a přidejte nový soubor s názvem Less *main.less* do této složky.</span><span class="sxs-lookup"><span data-stu-id="377e4-123">Add a *Styles* folder to your project, and then add a new Less file named *main.less* to this folder.</span></span>

![Přidání souboru less](less-sass-fa/_static/add-less-file.png)

<span data-ttu-id="377e4-125">Po přidání struktury složky by měl vypadat přibližně takto:</span><span class="sxs-lookup"><span data-stu-id="377e4-125">Once added, your folder structure should look something like this:</span></span>

![struktura složek](less-sass-fa/_static/folder-structure.png)

<span data-ttu-id="377e4-127">Nyní můžete přidat některé stylování základní do souboru, který bude zkompilována do šablon stylů CSS a nasadil do složky wwwroot Gulp.</span><span class="sxs-lookup"><span data-stu-id="377e4-127">Now you can add some basic styling to the file, which will be compiled into CSS and deployed to the wwwroot folder by Gulp.</span></span>

<span data-ttu-id="377e4-128">Upravit *main.less* zahrnout následující obsah, který vytvoří jednoduchý barevné palety z jedné základní barvy.</span><span class="sxs-lookup"><span data-stu-id="377e4-128">Modify *main.less* to include the following content, which creates a simple color palette from a single base color.</span></span>

```less
@base: #663333;
@background: spin(@base, 180);
@lighter: lighten(spin(@base, 5), 10%);
@lighter2: lighten(spin(@base, 10), 20%);
@darker: darken(spin(@base, -5), 10%);
@darker2: darken(spin(@base, -10), 20%);

body {
    background-color:@background;
}
.baseColor  {color:@base}
.bgLight    {color:@lighter}
.bgLight2   {color:@lighter2}
.bgDark     {color:@darker}
.bgDark2    {color:@darker2}
```

<span data-ttu-id="377e4-129">`@base` a druhý @-prefixed položky jsou proměnné.</span><span class="sxs-lookup"><span data-stu-id="377e4-129">`@base` and the other @-prefixed items are variables.</span></span> <span data-ttu-id="377e4-130">Každý z nich představuje barvu.</span><span class="sxs-lookup"><span data-stu-id="377e4-130">Each of them represents a color.</span></span> <span data-ttu-id="377e4-131">S výjimkou `@base`, se nastavují pomocí funkce barva: zesvětlení a ztmavení, aktivovat.</span><span class="sxs-lookup"><span data-stu-id="377e4-131">Except for `@base`, they're set using color functions: lighten, darken, and spin.</span></span> <span data-ttu-id="377e4-132">Zesvětlení a ztmavení dělat v podstatě co očekáváte; Číselník upraví odstín barvy počet stupňů (kolem barevné kolo).</span><span class="sxs-lookup"><span data-stu-id="377e4-132">Lighten and darken do pretty much what you would expect; spin adjusts the hue of a color by a number of degrees (around the color wheel).</span></span> <span data-ttu-id="377e4-133">Méně procesor je dostatečně inteligentní, aby ignorovat proměnné, které nejsou používány, abychom si předvedli, jak tyto proměnné pracovat, musíme někde jejich použití.</span><span class="sxs-lookup"><span data-stu-id="377e4-133">The Less processor is smart enough to ignore variables that aren't used, so to demonstrate how these variables work, we need to use them somewhere.</span></span> <span data-ttu-id="377e4-134">Třídy `.baseColor`, vám ukáže počítaných hodnot všech proměnných v souboru šablony stylů CSS, který je vytvořen, atd.</span><span class="sxs-lookup"><span data-stu-id="377e4-134">The classes `.baseColor`, etc. will demonstrate the calculated values of each of the variables in the CSS file that's produced.</span></span>

### <a name="get-started"></a><span data-ttu-id="377e4-135">Začínáme</span><span class="sxs-lookup"><span data-stu-id="377e4-135">Get started</span></span>

<span data-ttu-id="377e4-136">Vytvoření **konfigurační soubor npm** (*package.json*) ve složce vašeho projektu a upravte jej tak, aby odkazovaly `gulp` a `gulp-less`:</span><span class="sxs-lookup"><span data-stu-id="377e4-136">Create an **npm Configuration File** (*package.json*) in your project folder and edit it to reference `gulp` and `gulp-less`:</span></span>

```json
{
  "version": "1.0.0",
  "name": "asp.net",
  "private": true,
  "devDependencies": {
    "gulp": "3.9.1",
    "gulp-less": "3.3.0"
  }
}
```

<span data-ttu-id="377e4-137">Nainstalovat závislosti buď na příkazovém řádku ve složce projektu nebo v sadě Visual Studio **Průzkumníka řešení** (**závislosti > npm > Obnovení balíčků**).</span><span class="sxs-lookup"><span data-stu-id="377e4-137">Install the dependencies either at a command prompt in your project folder, or in Visual Studio **Solution Explorer** (**Dependencies > npm > Restore packages**).</span></span>

```console
npm install
```

![VS obnovení balíčků](less-sass-fa/_static/restore-packages.png)

<span data-ttu-id="377e4-139">Vytvořte ve složce projektu **konfigurační soubor Gulp** (*gulpfile.js*) k definování automatizovaného procesu.</span><span class="sxs-lookup"><span data-stu-id="377e4-139">In the project folder, create a **Gulp Configuration File** (*gulpfile.js*) to define the automated process.</span></span>  <span data-ttu-id="377e4-140">Přidáte proměnnou v horní části souboru, který má představovat menší a menší spuštění úlohy:</span><span class="sxs-lookup"><span data-stu-id="377e4-140">Add a variable at the top of the file to represent Less, and a task to run Less:</span></span>

```javascript
var gulp = require("gulp"),
  fs = require("fs"),
  less = require("gulp-less");

gulp.task("less", function () {
  return gulp.src('Styles/main.less')
    .pipe(less())
    .pipe(gulp.dest('wwwroot/css'));
});
```

<span data-ttu-id="377e4-141">Otevřít **Task Runner Explorer** (**zobrazení > ostatní Windows > Task Runner Explorer**).</span><span class="sxs-lookup"><span data-stu-id="377e4-141">Open the **Task Runner Explorer** (**View > Other Windows > Task Runner Explorer**).</span></span> <span data-ttu-id="377e4-142">Mezi úkoly, měli byste vidět nový úkol s názvem `less`.</span><span class="sxs-lookup"><span data-stu-id="377e4-142">Among the tasks, you should see a new task named `less`.</span></span> <span data-ttu-id="377e4-143">Budete muset aktualizovat okno.</span><span class="sxs-lookup"><span data-stu-id="377e4-143">You might have to refresh the window.</span></span>

<span data-ttu-id="377e4-144">Spustit `less` úloh a zobrazit výstup podobný co je znázorněna zde:</span><span class="sxs-lookup"><span data-stu-id="377e4-144">Run the `less` task, and you see output similar to what is shown here:</span></span>

![méně Spouštěč úloh](less-sass-fa/_static/less-task-runner.png)

<span data-ttu-id="377e4-146">*Wwwroot/css* nyní obsahuje nový soubor, složku *main.css*:</span><span class="sxs-lookup"><span data-stu-id="377e4-146">The *wwwroot/css* folder now contains a new file, *main.css*:</span></span>

![hlavní šablony stylů css vytvořili](less-sass-fa/_static/main-css-created.png)

<span data-ttu-id="377e4-148">Otevřít *main.css* a vypadat nějak takto:</span><span class="sxs-lookup"><span data-stu-id="377e4-148">Open *main.css* and you see something like the following:</span></span>

```css
body {
    background-color: #336666;
}
.baseColor {
    color: #663333;
}
.bgLight {
    color: #884a44;
}
.bgLight2 {
    color: #aa6355;
}
.bgDark {
    color: #442225;
}
.bgDark2 {
    color: #221114;
}
```

<span data-ttu-id="377e4-149">Jednoduché stránky HTML pro přidání *wwwroot* složky a odkaz *main.css* zobrazíte paletu barev v akci.</span><span class="sxs-lookup"><span data-stu-id="377e4-149">Add a simple HTML page to the *wwwroot* folder, and reference *main.css* to see the color palette in action.</span></span>

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <link href="css/main.css" rel="stylesheet" />
    <title></title>
</head>
<body>
    <div>
        <div class="baseColor">BaseColor</div>
        <div class="bgLight">Light</div>
        <div class="bgLight2">Light2</div>
        <div class="bgDark">Dark</div>
        <div class="bgDark2">Dark2</div>
    </div>
</body>
</html>
```

<span data-ttu-id="377e4-150">Uvidíte, že na číselníku 180 stupňů `@base` používán k tvorbě `@background` výsledkem barevné kolo protikladné barva `@base`:</span><span class="sxs-lookup"><span data-stu-id="377e4-150">You can see that the 180 degree spin on `@base` used to produce `@background` resulted in the color wheel opposing color of `@base`:</span></span>

![Příklad méně testování](less-sass-fa/_static/less-test-screenshot.png)

<span data-ttu-id="377e4-152">Menší také poskytuje podporu pro vnořené pravidla i dotazy vnořené média.</span><span class="sxs-lookup"><span data-stu-id="377e4-152">Less also provides support for nested rules, as well as nested media queries.</span></span> <span data-ttu-id="377e4-153">Například definující vnořené hierarchie, jako jsou nabídky může vést k podrobné pravidel šablon stylů CSS, jako jsou tyto:</span><span class="sxs-lookup"><span data-stu-id="377e4-153">For example, defining nested hierarchies like menus can result in verbose CSS rules like these:</span></span>

```css
nav {
    height: 40px;
    width: 100%;
}
nav li {
    height: 38px;
    width: 100px;
}
nav li a:link {
    color: #000;
    text-decoration: none;
}
nav li a:visited {
    text-decoration: none;
    color: #CC3333;
}
nav li a:hover {
    text-decoration: underline;
    font-weight: bold;
}
nav li a:active {
    text-decoration: underline;
}
```

<span data-ttu-id="377e4-154">V ideálním případě všechna pravidla související styl budou umístěny společně v rámci souboru šablon stylů CSS, ale v praxi není nic vynucování toto pravidlo s výjimkou úmluva a třeba komentáře bloku.</span><span class="sxs-lookup"><span data-stu-id="377e4-154">Ideally all of the related style rules will be placed together within the CSS file, but in practice there's nothing enforcing this rule except convention and perhaps block comments.</span></span>

<span data-ttu-id="377e4-155">Definování těchto stejnými pravidly používání menší vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="377e4-155">Defining these same rules using Less looks like this:</span></span>

```less
nav {
    height: 40px;
    width: 100%;
    li {
        height: 38px;
        width: 100px;
        a {
            color: #000;
            &:link { text-decoration:none}
            &:visited { color: #CC3333; text-decoration:none}
            &:hover { text-decoration:underline; font-weight:bold}
            &:active {text-decoration:underline}
        }
    }
}
```

<span data-ttu-id="377e4-156">Všimněte si, že se v takovém případě všechny podřízené prvky `nav` jsou obsaženy v rámci svého oboru.</span><span class="sxs-lookup"><span data-stu-id="377e4-156">Note that in this case, all of the subordinate elements of `nav` are contained within its scope.</span></span> <span data-ttu-id="377e4-157">Již neplatí žádné opakování nadřazené elementy (`nav`, `li`, `a`), a počet celkový počet řádků má také vyřadit (i když některé, která je výsledkem sestavení hodnot na stejné řádky v druhém příkladu).</span><span class="sxs-lookup"><span data-stu-id="377e4-157">There's no longer any repetition of parent elements (`nav`, `li`, `a`), and the total line count has dropped as well (though some of that's a result of putting values on the same lines in the second example).</span></span> <span data-ttu-id="377e4-158">Může být velmi užitečné, používání, zobrazíte všechna pravidla pro daný prvek uživatelského rozhraní v rámci explicitně ohraničené oboru, v tomto případě nastavte od zbývající části souboru ve složených závorkách.</span><span class="sxs-lookup"><span data-stu-id="377e4-158">It can be very helpful, organizationally, to see all of the rules for a given UI element within an explicitly bounded scope, in this case set off from the rest of the file by curly braces.</span></span>

<span data-ttu-id="377e4-159">`&` Syntaxe je méně selektor funkce, s & představující aktuální výběr nadřazené.</span><span class="sxs-lookup"><span data-stu-id="377e4-159">The `&` syntax is a Less selector feature, with & representing the current selector parent.</span></span> <span data-ttu-id="377e4-160">Ano, v rámci {...}</span><span class="sxs-lookup"><span data-stu-id="377e4-160">So, within the a {...}</span></span> <span data-ttu-id="377e4-161">blok, `&` představuje `a` značky a proto `&:link` je ekvivalentní `a:link`.</span><span class="sxs-lookup"><span data-stu-id="377e4-161">block, `&` represents an `a` tag, and thus `&:link` is equivalent to `a:link`.</span></span>

<span data-ttu-id="377e4-162">Dotazy na média, velmi užitečné při vytváření reagovat návrhy, můžete přispívat také silně opakování a složitosti v jazyce CSS.</span><span class="sxs-lookup"><span data-stu-id="377e4-162">Media queries, extremely useful in creating responsive designs, can also contribute heavily to repetition and complexity in CSS.</span></span> <span data-ttu-id="377e4-163">Menší umožňuje dotazy na média na být vnořen v rámci třídy, tak, aby definice celou třídu není potřeba opakovat v rámci různých nejvyšší úrovně `@media` elementy.</span><span class="sxs-lookup"><span data-stu-id="377e4-163">Less allows media queries to be nested within classes, so that the entire class definition doesn't need to be repeated within different top-level `@media` elements.</span></span> <span data-ttu-id="377e4-164">Tady je příklad, šablon stylů CSS responzivní nabídky:</span><span class="sxs-lookup"><span data-stu-id="377e4-164">For example, here is CSS for a responsive menu:</span></span>

```css
.navigation {
    margin-top: 30%;
    width: 100%;
}
@media screen and (min-width: 40em) {
    .navigation {
        margin: 0;
    }
}
@media screen and (min-width: 62em) {
    .navigation {
        width: 960px;
        margin: 0;
    }
}
```

<span data-ttu-id="377e4-165">Toto může být lepší definováno v menší jako:</span><span class="sxs-lookup"><span data-stu-id="377e4-165">This can be better defined in Less as:</span></span>

```less
.navigation {
    margin-top: 30%;
    width: 100%;
    @media screen and (min-width: 40em) {
        margin: 0;
    }
    @media screen and (min-width: 62em) {
        width: 960px;
        margin: 0;
    }
}
```

<span data-ttu-id="377e4-166">Další funkcí nižší, který jsme viděli už je jeho podpora matematické operace a atributy stylu z předdefinovaných proměnných.</span><span class="sxs-lookup"><span data-stu-id="377e4-166">Another feature of Less that we have already seen is its support for mathematical operations, allowing style attributes to be constructed from pre-defined variables.</span></span> <span data-ttu-id="377e4-167">Díky tomu aktualizace související styly mnohem jednodušší, protože je možné upravit proměnnou základní a všechny závislé hodnoty automaticky změní.</span><span class="sxs-lookup"><span data-stu-id="377e4-167">This makes updating related styles much easier, since the base variable can be modified and all dependent values change automatically.</span></span>

<span data-ttu-id="377e4-168">Soubory šablon stylů CSS, zejména u velkých webů (a zejména v případě, že se používají dotazy na média), mají tendenci získat poměrně velké v průběhu času provádění těžkopádným práci s nimi.</span><span class="sxs-lookup"><span data-stu-id="377e4-168">CSS files, especially for large sites (and especially if media queries are being used), tend to get quite large over time, making working with them unwieldy.</span></span> <span data-ttu-id="377e4-169">Soubory Less lze definovat samostatně, pak dali dohromady pomocí `@import` direktivy.</span><span class="sxs-lookup"><span data-stu-id="377e4-169">Less files can be defined separately, then pulled together using `@import` directives.</span></span> <span data-ttu-id="377e4-170">Menší také slouží k importu jednotlivých souborů CSS, i, v případě potřeby.</span><span class="sxs-lookup"><span data-stu-id="377e4-170">Less can also be used to import individual CSS files, as well, if desired.</span></span>

<span data-ttu-id="377e4-171">*Objekty Mixin* mohou přijímat parametry a menší podporuje podmíněnou logiku v podobě mixin ochrany, které poskytují deklarativní způsob, jak definovat, kdy se určité objekty mixin platit.</span><span class="sxs-lookup"><span data-stu-id="377e4-171">*Mixins* can accept parameters, and Less supports conditional logic in the form of mixin guards, which provide a declarative way to define when certain mixins take effect.</span></span> <span data-ttu-id="377e4-172">Běžným účelem pro mixin chrání je upravit barvy na základě jak slabá nebo tmavý zdrojové barvy.</span><span class="sxs-lookup"><span data-stu-id="377e4-172">A common use for mixin guards is to adjust colors based on how light or dark the source color is.</span></span> <span data-ttu-id="377e4-173">Zadaný mixin –, který přijímá parametr pro barvu, mixin guard je možné upravit mixin na základě této barvy:</span><span class="sxs-lookup"><span data-stu-id="377e4-173">Given a mixin that accepts a parameter for color, a mixin guard can be used to modify the mixin based on that color:</span></span>

```less
.box (@color) when (lightness(@color) >= 50%) {
    background-color: #000;
}
.box (@color) when (lightness(@color) < 50%) {
    background-color: #FFF;
}
.box (@color) {
    color: @color;
}

.feature {
    .box (@base);
}
```

<span data-ttu-id="377e4-174">Zadaný naše aktuální `@base` hodnotu `#663333`, méně tento skript vytvoří následující šablony stylů CSS:</span><span class="sxs-lookup"><span data-stu-id="377e4-174">Given our current `@base` value of `#663333`, this Less script will produce the following CSS:</span></span>

```css
.feature {
    background-color: #FFF;
    color: #663333;
}
```

<span data-ttu-id="377e4-175">Menší nabízí celou řadu dalších funkcí, ale to by vám měl dát představu o sílu to předzpracování jazyka.</span><span class="sxs-lookup"><span data-stu-id="377e4-175">Less provides a number of additional features, but this should give you some idea of the power of this preprocessing language.</span></span>

## <a name="sass"></a><span data-ttu-id="377e4-176">Sass</span><span class="sxs-lookup"><span data-stu-id="377e4-176">Sass</span></span>

<span data-ttu-id="377e4-177">Sass je podobně jako na hodnotu menší, poskytuje podporu pro mnoho stejných funkcí, ale s mírně odlišnou syntaxi.</span><span class="sxs-lookup"><span data-stu-id="377e4-177">Sass is similar to Less, providing support for many of the same features, but with slightly different syntax.</span></span> <span data-ttu-id="377e4-178">Je vytvořen pomocí Ruby, nikoli jazyka JavaScript a má různé instalační požadavky.</span><span class="sxs-lookup"><span data-stu-id="377e4-178">It's built using Ruby, rather than JavaScript, and so has different setup requirements.</span></span> <span data-ttu-id="377e4-179">Původní jazyk Sass nepoužili složených závorek nebo středníky, ale místo definice oboru pomocí mezer a odsazení.</span><span class="sxs-lookup"><span data-stu-id="377e4-179">The original Sass language didn't use curly braces or semicolons, but instead defined scope using white space and indentation.</span></span> <span data-ttu-id="377e4-180">Ve verzi 3 Sass, byla zavedena nová syntaxe, **SCSS** ("Sassy CSS").</span><span class="sxs-lookup"><span data-stu-id="377e4-180">In version 3 of Sass, a new syntax was introduced, **SCSS** ("Sassy CSS").</span></span> <span data-ttu-id="377e4-181">SCSS je podobný šablon stylů CSS ignoruje zadaných úrovní odsazení a mezery a místo toho používá středníky a složené závorky.</span><span class="sxs-lookup"><span data-stu-id="377e4-181">SCSS is similar to CSS in that it ignores indentation levels and whitespace, and instead uses semicolons and curly braces.</span></span>

<span data-ttu-id="377e4-182">K instalaci Sass, obvykle by nejdřív nainstalujte Ruby (předem nainstalované v systému macOS) a potom spusťte:</span><span class="sxs-lookup"><span data-stu-id="377e4-182">To install Sass, typically you would first install Ruby (pre-installed on macOS), and then run:</span></span>

```console
gem install sass
```

<span data-ttu-id="377e4-183">Ale pokud používáte Visual Studio, můžete začít s Sass prakticky stejně jako stejně jako s menší.</span><span class="sxs-lookup"><span data-stu-id="377e4-183">However, if you're running Visual Studio, you can get started with Sass in much the same way as you would with Less.</span></span> <span data-ttu-id="377e4-184">Otevřít *package.json* a přidejte balíček "gulp sass" `devDependencies`:</span><span class="sxs-lookup"><span data-stu-id="377e4-184">Open *package.json* and add the "gulp-sass" package to `devDependencies`:</span></span>

```json
"devDependencies": {
  "gulp": "3.9.1",
  "gulp-less": "3.3.0",
  "gulp-sass": "3.1.0"
}
```

<span data-ttu-id="377e4-185">V dalším kroku změnit *gulpfile.js* k přidání proměnné sass a úlohy kompilace soubory Sass a umístěte do složky wwwroot výsledky:</span><span class="sxs-lookup"><span data-stu-id="377e4-185">Next, modify *gulpfile.js* to add a sass variable and a task to compile your Sass files and place the results in the wwwroot folder:</span></span>

```javascript
var gulp = require("gulp"),
  fs = require("fs"),
  less = require("gulp-less"),
  sass = require("gulp-sass");

// other content removed

gulp.task("sass", function () {
  return gulp.src('Styles/main2.scss')
    .pipe(sass())
    .pipe(gulp.dest('wwwroot/css'));
});
```

<span data-ttu-id="377e4-186">Teď můžete přidat soubor Sass *main2.scss* k *styly* složku v kořenovém adresáři projektu:</span><span class="sxs-lookup"><span data-stu-id="377e4-186">Now you can add the Sass file *main2.scss* to the *Styles* folder in the root of the project:</span></span>

![Přidání souboru scss](less-sass-fa/_static/add-scss-file.png)

<span data-ttu-id="377e4-188">Otevřít *main2.scss* a přidejte následující:</span><span class="sxs-lookup"><span data-stu-id="377e4-188">Open *main2.scss* and add the following:</span></span>

```sass
$base: #CC0000;
body {
    background-color: $base;
}
```

<span data-ttu-id="377e4-189">Uložte všechny soubory.</span><span class="sxs-lookup"><span data-stu-id="377e4-189">Save all of your files.</span></span> <span data-ttu-id="377e4-190">Nyní při aktualizaci **Task Runner Explorer**, uvidíte `sass` úloh.</span><span class="sxs-lookup"><span data-stu-id="377e4-190">Now when you refresh **Task Runner Explorer**, you see a `sass` task.</span></span> <span data-ttu-id="377e4-191">Spusťte ho a podívejte se */wwwroot/css* složky.</span><span class="sxs-lookup"><span data-stu-id="377e4-191">Run it, and look in the */wwwroot/css* folder.</span></span> <span data-ttu-id="377e4-192">Teď *main2.css* soubor s tímto obsahem:</span><span class="sxs-lookup"><span data-stu-id="377e4-192">There's now a *main2.css* file, with these contents:</span></span>

```css
body {
    background-color: #CC0000;
}
```

<span data-ttu-id="377e4-193">Sass podporuje vnoření prakticky stejné se, že menší nemá, poskytují podobné výhody.</span><span class="sxs-lookup"><span data-stu-id="377e4-193">Sass supports nesting in much the same was that Less does, providing similar benefits.</span></span> <span data-ttu-id="377e4-194">Soubory můžete rozdělit podle funkce a zahrnuty pomocí `@import` – direktiva:</span><span class="sxs-lookup"><span data-stu-id="377e4-194">Files can be split up by function and included using the `@import` directive:</span></span>

```sass
@import 'anotherfile';
```

<span data-ttu-id="377e4-195">Sass podporuje také, objekty mixin používání `@mixin` – klíčové slovo se definovat a `@include` pro zahrnutí, jako v následujícím příkladu od [sass lang.com](http://sass-lang.com):</span><span class="sxs-lookup"><span data-stu-id="377e4-195">Sass supports mixins as well, using the `@mixin` keyword to define them and `@include` to include them, as in this example from [sass-lang.com](http://sass-lang.com):</span></span>

```sass
@mixin border-radius($radius) {
    -webkit-border-radius: $radius;
    -moz-border-radius: $radius;
    -ms-border-radius: $radius;
    border-radius: $radius;
}

.box { @include border-radius(10px); }
```

<span data-ttu-id="377e4-196">Kromě objekty mixin Sass také podporuje koncept dědičnosti, povolení jednu třídu jiného rozšíření.</span><span class="sxs-lookup"><span data-stu-id="377e4-196">In addition to mixins, Sass also supports the concept of inheritance, allowing one class to extend another.</span></span> <span data-ttu-id="377e4-197">To se koncepčně podobá mixin, ale má za následek méně kód šablony stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="377e4-197">It's conceptually similar to a mixin, but results in less CSS code.</span></span> <span data-ttu-id="377e4-198">Použití se provádí `@extend` – klíčové slovo.</span><span class="sxs-lookup"><span data-stu-id="377e4-198">It's accomplished using the `@extend` keyword.</span></span> <span data-ttu-id="377e4-199">Vyzkoušet objekty mixin, přidejte následující text do vašeho *main2.scss* souboru:</span><span class="sxs-lookup"><span data-stu-id="377e4-199">To try out mixins, add the following to your *main2.scss* file:</span></span>

```sass
@mixin alert {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    @include alert;
    border-color: green;
}

.error {
    @include alert;
    color: red;
    border-color: red;
    font-weight:bold;
}
```

<span data-ttu-id="377e4-200">Prohlédněte si výstup v *main2.css* po spuštění `sass` úlohy v **Task Runner Explorer**:</span><span class="sxs-lookup"><span data-stu-id="377e4-200">Examine the output in *main2.css* after running the `sass` task in **Task Runner Explorer**:</span></span>

```css
.success {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
    border-color: green;
 }

.error {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
    color: red;
    border-color: red;
    font-weight: bold;
}
```

<span data-ttu-id="377e4-201">Všimněte si, že všechny společné vlastnosti výstrahy mixin se opakují v každé třídě.</span><span class="sxs-lookup"><span data-stu-id="377e4-201">Notice that all of the common properties of the alert mixin are repeated in each class.</span></span> <span data-ttu-id="377e4-202">Mixin nebyla dobrou práci, pomáhá eliminovat duplikace v době vývoje, ale stále se vytváří šablon stylů CSS s velkým množstvím duplicity, což vede k větší než potřebné soubory šablon stylů CSS – potenciální problém s výkonem.</span><span class="sxs-lookup"><span data-stu-id="377e4-202">The mixin did a good job of helping eliminate duplication at development time, but it's still creating CSS with a lot of duplication in it, resulting in larger than necessary CSS files - a potential performance issue.</span></span>

<span data-ttu-id="377e4-203">Nyní nahraďte upozornění mixin s `.alert` třídy a změňte parametr `@include` k `@extend` (zapamatování rozšířit `.alert`, nikoli `alert`):</span><span class="sxs-lookup"><span data-stu-id="377e4-203">Now replace the alert mixin with a `.alert` class, and change `@include` to `@extend` (remembering to extend `.alert`, not `alert`):</span></span>

```sass
.alert {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    @extend .alert;
    border-color: green;
}

.error {
    @extend .alert;
    color: red;
    border-color: red;
    font-weight:bold;
}
```

<span data-ttu-id="377e4-204">Ještě jednou spustit Sass a zkontrolujte výsledné šablon stylů CSS:</span><span class="sxs-lookup"><span data-stu-id="377e4-204">Run Sass once more, and examine the resulting CSS:</span></span>

```css
.alert, .success, .error {
    border: 1px solid black;
    padding: 5px;
    color: #333333;
}

.success {
    border-color: green;
}

.error {
    color: red;
    border-color: red;
    font-weight: bold;
}
```

<span data-ttu-id="377e4-205">Nyní jsou definovány vlastnosti pouze tolikrát, kolikrát podle potřeby a lépe se vygeneruje šablon stylů CSS.</span><span class="sxs-lookup"><span data-stu-id="377e4-205">Now the properties are defined only as many times as needed, and better CSS is generated.</span></span>

<span data-ttu-id="377e4-206">Sass také zahrnuje funkce a podmíněné logiky operace, podobně jako na hodnotu menší.</span><span class="sxs-lookup"><span data-stu-id="377e4-206">Sass also includes functions and conditional logic operations, similar to Less.</span></span> <span data-ttu-id="377e4-207">Ve skutečnosti jsou velmi podobné možnosti dva jazyků.</span><span class="sxs-lookup"><span data-stu-id="377e4-207">In fact, the two languages' capabilities are very similar.</span></span>

## <a name="less-or-sass"></a><span data-ttu-id="377e4-208">Menší nebo Sass?</span><span class="sxs-lookup"><span data-stu-id="377e4-208">Less or Sass?</span></span>

<span data-ttu-id="377e4-209">Ještě není shoda, zda je obecně vhodnější použít méně nebo Sass (nebo dokonce, jestli se má přednost původní Sass nebo novější syntaxe SCSS v rámci Sass).</span><span class="sxs-lookup"><span data-stu-id="377e4-209">There's still no consensus as to whether it's generally better to use Less or Sass (or even whether to prefer the original Sass or the newer SCSS syntax within Sass).</span></span> <span data-ttu-id="377e4-210">Pravděpodobně je nejdůležitější rozhodnutí **použijte jednu z těchto nástrojů**, na rozdíl od jenom kódování souborů CSS ručně.</span><span class="sxs-lookup"><span data-stu-id="377e4-210">Probably the most important decision is to **use one of these tools**, as opposed to just hand-coding your CSS files.</span></span> <span data-ttu-id="377e4-211">Jakmile jste udělali, který rozhodnutí, i menší a Sass jsou vhodná rozhodnutí.</span><span class="sxs-lookup"><span data-stu-id="377e4-211">Once you've made that decision, both Less and Sass are good choices.</span></span>

## <a name="font-awesome"></a><span data-ttu-id="377e4-212">Knihovnou aplikací Font Awesome</span><span class="sxs-lookup"><span data-stu-id="377e4-212">Font Awesome</span></span>

<span data-ttu-id="377e4-213">Kromě preprocesory šablon stylů CSS je knihovnou aplikací Font Awesome dalším skvělým zdrojem pro používání stylů pro moderní webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="377e4-213">In addition to CSS preprocessors, another great resource for styling modern web applications is Font Awesome.</span></span> <span data-ttu-id="377e4-214">Písmo Super je sada nástrojů obsahuje více než 500 scalable vector ikony, které se můžou volně používat ve vašich webových aplikacích.</span><span class="sxs-lookup"><span data-stu-id="377e4-214">Font Awesome is a toolkit that provides over 500 scalable vector icons that can be freely used in your web applications.</span></span> <span data-ttu-id="377e4-215">Původně byla navržena pro práci s Bootstrap, ale nemá žádné závislosti na tímto rozhraním nebo na žádné knihovny jazyka JavaScript.</span><span class="sxs-lookup"><span data-stu-id="377e4-215">It was originally designed to work with Bootstrap, but it has no dependency on that framework or on any JavaScript libraries.</span></span>

<span data-ttu-id="377e4-216">Nejjednodušší způsob, jak začít pracovat s knihovnou aplikací Font Awesome je přidání odkazu do něj pomocí jeho veřejné content delivery network (CDN) umístění:</span><span class="sxs-lookup"><span data-stu-id="377e4-216">The easiest way to get started with Font Awesome is to add a reference to it, using its public content delivery network (CDN) location:</span></span>

```html
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">
```

<span data-ttu-id="377e4-217">Můžete také přidat ho do projektu sady Visual Studio tak, že přidáte "závislostí" v *bower.json*:</span><span class="sxs-lookup"><span data-stu-id="377e4-217">You can also add it to your Visual Studio project by adding it to the "dependencies" in *bower.json*:</span></span>

```json
{
  "name": "ASP.NET",
  "private": true,
  "dependencies": {
    "bootstrap": "3.0.0",
    "jquery": "1.10.2",
    "jquery-validation": "1.11.1",
    "jquery-validation-unobtrusive": "3.2.2",
    "hammer.js": "2.0.4",
    "bootstrap-touch-carousel": "0.8.0",
    "Font-Awesome": "4.3.0"
  }
}
```

<span data-ttu-id="377e4-218">Až budete mít odkaz na knihovnou aplikací Font Awesome na stránce, můžete přidat ikony pro vaši aplikaci s použitím třídy knihovnou aplikací Font Awesome, obvykle s předponou "DM-" prvkům vložené HTML (například `<span>` nebo `<i>`).</span><span class="sxs-lookup"><span data-stu-id="377e4-218">Once you have a reference to Font Awesome on a page, you can add icons to your application by applying Font Awesome classes, typically prefixed with "fa-", to your inline HTML elements (such as `<span>` or `<i>`).</span></span>  <span data-ttu-id="377e4-219">Můžete například přidat ikony jednoduché seznamy a nabídky pomocí kódu takto:</span><span class="sxs-lookup"><span data-stu-id="377e4-219">For example, you can add icons to simple lists and menus using code like this:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8" />
    <title></title>
    <link href="lib/font-awesome/css/font-awesome.css" rel="stylesheet" />
</head>
<body>
    <ul class="fa-ul">
        <li><i class="fa fa-li fa-home"></i> Home</li>
        <li><i class="fa fa-li fa-cog"></i> Settings</li>
    </ul>
</body>
</html>
```

<span data-ttu-id="377e4-220">Tímto se vytvoří následující v prohlížeči – Poznámka: na ikonu vedle každé položky:</span><span class="sxs-lookup"><span data-stu-id="377e4-220">This produces the following in the browser - note the icon beside each item:</span></span>

![seznam ikon](less-sass-fa/_static/list-icons-screenshot.png)

<span data-ttu-id="377e4-222">Můžete zobrazit úplný seznam dostupných ikon:</span><span class="sxs-lookup"><span data-stu-id="377e4-222">You can view a complete list of the available icons here:</span></span>

http://fontawesome.io/icons/

## <a name="summary"></a><span data-ttu-id="377e4-223">Souhrn</span><span class="sxs-lookup"><span data-stu-id="377e4-223">Summary</span></span>

<span data-ttu-id="377e4-224">Moderní webové aplikace stále vyžadují rychlou odezvou, plynulé návrhy, které jsou čisté, intuitivní a snadno se používá z různých zařízení.</span><span class="sxs-lookup"><span data-stu-id="377e4-224">Modern web applications increasingly demand responsive, fluid designs that are clean, intuitive, and easy to use from a variety of devices.</span></span> <span data-ttu-id="377e4-225">Správa složitosti šablon stylů CSS, potřebná k dosažení těchto cílů se nejlépe provádí pomocí preprocesoru je menší nebo Sass.</span><span class="sxs-lookup"><span data-stu-id="377e4-225">Managing the complexity of the CSS stylesheets required to achieve these goals is best done using a preprocessor like Less or Sass.</span></span> <span data-ttu-id="377e4-226">Kromě toho sady nástrojů, jako je knihovnou aplikací Font Awesome rychle poskytnout dobře známé ikony textové navigační nabídky a tlačítka, zlepšení celkové uživatelské prostředí vaší aplikace.</span><span class="sxs-lookup"><span data-stu-id="377e4-226">In addition, toolkits like Font Awesome quickly provide well-known icons to textual navigation menus and buttons, improving the overall user experience of your application.</span></span>

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
# <a name="less-sass-and-font-awesome-in-aspnet-core"></a>Menší, Sass a knihovnou aplikací Font Awesome v ASP.NET Core

Podle [Steve Smith](https://ardalis.com/)

Uživatelé webových aplikací mají stále vysoká očekávání při rozhodování o stylu a celkové prostředí. Moderní webové aplikace často využívat bohaté možnosti nástrojů a architektur definují a spravují jejich vzhled a chování konzistentním způsobem. Architektury, jako jsou [Bootstrap](http://getbootstrap.com/) můžete urazily dlouhou cestu k definování společnou sadu – styly a možnosti rozložení pro weby. Většina serverů nejsou v netriviálních však také těžit z dokáže efektivně definovat a udržovat stylů a soubory kaskádových stylů (CSS) a také snadný přístup k ikony bitové kopie, které pomůžou intuitivnější rozhraní webu. Tam se jazyky a nástroje, které podporují [méně](http://lesscss.org/) a [Sass](http://sass-lang.com/), a knihoven, jako jsou [knihovnou aplikací Font Awesome](http://fontawesome.io/), se dělí na.

## <a name="css-preprocessor-languages"></a>Preprocesor jazyků šablon stylů CSS

Jazyky, které jsou kompilovány do jiných jazyků, za účelem zlepšení možností práce s základní jazyk, se označují jako preprocesory. Existují dvě oblíbené preprocesory pro šablony stylů CSS: Menší a Sass.  Tyto preprocesory přidat funkce do šablony stylů CSS, jako třeba podporu pro proměnné a vnořené pravidla, která zlepšit udržovatelnosti velké a komplexní šablony stylů. Šablon stylů CSS jako jazyk je velmi základní chybí podporu ještě něco stejně jednoduché jako proměnné, a to může vytvořit soubory šablon stylů CSS opakující se a opakovaném. Přidání funkcí reálné programovacích jazyků přes preprocesory můžou pomoct snížit duplikace a poskytují lepší uspořádání pravidel stylů. Visual Studio poskytuje integrovanou podporu pro obě Less a Sass, jakož i rozšíření, která ještě vylepšit vývojové prostředí při práci s těchto jazyků.

Jako krátká ukázka toho, jak preprocesory zlepšit čitelnost a udržovatelnosti informací o stylu vezměte v úvahu CSS:

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

Použití nižší, to může být přepsán Chcete-li odstranit všechny duplicity, pomocí *mixin* (tedy s názvem, protože umožňuje "kombinovat" vlastnosti z jedné třídy nebo sada pravidel do jiné):

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

## <a name="less"></a>méně

Spuštění preprocesoru méně šablon stylů CSS pomocí Node.js. K instalaci menší, pomocí Node Package Manageru (npm) z příkazového řádku (-g znamená "globální"):

```console
npm install -g less
```

Pokud používáte Visual Studio, můžete začít s menší přidáním jednoho nebo více méně souborů do projektu a pak nakonfigurujete Gulp (ani Grunt) ke zpracování v době kompilace. Přidat *styly* složku pro váš projekt a přidejte nový soubor s názvem Less *main.less* do této složky.

![Přidání souboru less](less-sass-fa/_static/add-less-file.png)

Po přidání struktury složky by měl vypadat přibližně takto:

![struktura složek](less-sass-fa/_static/folder-structure.png)

Nyní můžete přidat některé stylování základní do souboru, který bude zkompilována do šablon stylů CSS a nasadil do složky wwwroot Gulp.

Upravit *main.less* zahrnout následující obsah, který vytvoří jednoduchý barevné palety z jedné základní barvy.

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

`@base` a druhý @-prefixed položky jsou proměnné. Každý z nich představuje barvu. S výjimkou `@base`, se nastavují pomocí funkce barva: zesvětlení a ztmavení, aktivovat. Zesvětlení a ztmavení dělat v podstatě co očekáváte; Číselník upraví odstín barvy počet stupňů (kolem barevné kolo). Méně procesor je dostatečně inteligentní, aby ignorovat proměnné, které nejsou používány, abychom si předvedli, jak tyto proměnné pracovat, musíme někde jejich použití. Třídy `.baseColor`, vám ukáže počítaných hodnot všech proměnných v souboru šablony stylů CSS, který je vytvořen, atd.

### <a name="get-started"></a>Začínáme

Vytvoření **konfigurační soubor npm** (*package.json*) ve složce vašeho projektu a upravte jej tak, aby odkazovaly `gulp` a `gulp-less`:

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

Nainstalovat závislosti buď na příkazovém řádku ve složce projektu nebo v sadě Visual Studio **Průzkumníka řešení** (**závislosti > npm > Obnovení balíčků**).

```console
npm install
```

![VS obnovení balíčků](less-sass-fa/_static/restore-packages.png)

Vytvořte ve složce projektu **konfigurační soubor Gulp** (*gulpfile.js*) k definování automatizovaného procesu.  Přidáte proměnnou v horní části souboru, který má představovat menší a menší spuštění úlohy:

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

Otevřít **Task Runner Explorer** (**zobrazení > ostatní Windows > Task Runner Explorer**). Mezi úkoly, měli byste vidět nový úkol s názvem `less`. Budete muset aktualizovat okno.

Spustit `less` úloh a zobrazit výstup podobný co je znázorněna zde:

![méně Spouštěč úloh](less-sass-fa/_static/less-task-runner.png)

*Wwwroot/css* nyní obsahuje nový soubor, složku *main.css*:

![hlavní šablony stylů css vytvořili](less-sass-fa/_static/main-css-created.png)

Otevřít *main.css* a vypadat nějak takto:

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

Jednoduché stránky HTML pro přidání *wwwroot* složky a odkaz *main.css* zobrazíte paletu barev v akci.

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

Uvidíte, že na číselníku 180 stupňů `@base` používán k tvorbě `@background` výsledkem barevné kolo protikladné barva `@base`:

![Příklad méně testování](less-sass-fa/_static/less-test-screenshot.png)

Menší také poskytuje podporu pro vnořené pravidla i dotazy vnořené média. Například definující vnořené hierarchie, jako jsou nabídky může vést k podrobné pravidel šablon stylů CSS, jako jsou tyto:

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

V ideálním případě všechna pravidla související styl budou umístěny společně v rámci souboru šablon stylů CSS, ale v praxi není nic vynucování toto pravidlo s výjimkou úmluva a třeba komentáře bloku.

Definování těchto stejnými pravidly používání menší vypadá takto:

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

Všimněte si, že se v takovém případě všechny podřízené prvky `nav` jsou obsaženy v rámci svého oboru. Již neplatí žádné opakování nadřazené elementy (`nav`, `li`, `a`), a počet celkový počet řádků má také vyřadit (i když některé, která je výsledkem sestavení hodnot na stejné řádky v druhém příkladu). Může být velmi užitečné, používání, zobrazíte všechna pravidla pro daný prvek uživatelského rozhraní v rámci explicitně ohraničené oboru, v tomto případě nastavte od zbývající části souboru ve složených závorkách.

`&` Syntaxe je méně selektor funkce, s & představující aktuální výběr nadřazené. Ano, v rámci {...} blok, `&` představuje `a` značky a proto `&:link` je ekvivalentní `a:link`.

Dotazy na média, velmi užitečné při vytváření reagovat návrhy, můžete přispívat také silně opakování a složitosti v jazyce CSS. Menší umožňuje dotazy na média na být vnořen v rámci třídy, tak, aby definice celou třídu není potřeba opakovat v rámci různých nejvyšší úrovně `@media` elementy. Tady je příklad, šablon stylů CSS responzivní nabídky:

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

Toto může být lepší definováno v menší jako:

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

Další funkcí nižší, který jsme viděli už je jeho podpora matematické operace a atributy stylu z předdefinovaných proměnných. Díky tomu aktualizace související styly mnohem jednodušší, protože je možné upravit proměnnou základní a všechny závislé hodnoty automaticky změní.

Soubory šablon stylů CSS, zejména u velkých webů (a zejména v případě, že se používají dotazy na média), mají tendenci získat poměrně velké v průběhu času provádění těžkopádným práci s nimi. Soubory Less lze definovat samostatně, pak dali dohromady pomocí `@import` direktivy. Menší také slouží k importu jednotlivých souborů CSS, i, v případě potřeby.

*Objekty Mixin* mohou přijímat parametry a menší podporuje podmíněnou logiku v podobě mixin ochrany, které poskytují deklarativní způsob, jak definovat, kdy se určité objekty mixin platit. Běžným účelem pro mixin chrání je upravit barvy na základě jak slabá nebo tmavý zdrojové barvy. Zadaný mixin –, který přijímá parametr pro barvu, mixin guard je možné upravit mixin na základě této barvy:

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

Zadaný naše aktuální `@base` hodnotu `#663333`, méně tento skript vytvoří následující šablony stylů CSS:

```css
.feature {
    background-color: #FFF;
    color: #663333;
}
```

Menší nabízí celou řadu dalších funkcí, ale to by vám měl dát představu o sílu to předzpracování jazyka.

## <a name="sass"></a>Sass

Sass je podobně jako na hodnotu menší, poskytuje podporu pro mnoho stejných funkcí, ale s mírně odlišnou syntaxi. Je vytvořen pomocí Ruby, nikoli jazyka JavaScript a má různé instalační požadavky. Původní jazyk Sass nepoužili složených závorek nebo středníky, ale místo definice oboru pomocí mezer a odsazení. Ve verzi 3 Sass, byla zavedena nová syntaxe, **SCSS** ("Sassy CSS"). SCSS je podobný šablon stylů CSS ignoruje zadaných úrovní odsazení a mezery a místo toho používá středníky a složené závorky.

K instalaci Sass, obvykle by nejdřív nainstalujte Ruby (předem nainstalované v systému macOS) a potom spusťte:

```console
gem install sass
```

Ale pokud používáte Visual Studio, můžete začít s Sass prakticky stejně jako stejně jako s menší. Otevřít *package.json* a přidejte balíček "gulp sass" `devDependencies`:

```json
"devDependencies": {
  "gulp": "3.9.1",
  "gulp-less": "3.3.0",
  "gulp-sass": "3.1.0"
}
```

V dalším kroku změnit *gulpfile.js* k přidání proměnné sass a úlohy kompilace soubory Sass a umístěte do složky wwwroot výsledky:

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

Teď můžete přidat soubor Sass *main2.scss* k *styly* složku v kořenovém adresáři projektu:

![Přidání souboru scss](less-sass-fa/_static/add-scss-file.png)

Otevřít *main2.scss* a přidejte následující:

```sass
$base: #CC0000;
body {
    background-color: $base;
}
```

Uložte všechny soubory. Nyní při aktualizaci **Task Runner Explorer**, uvidíte `sass` úloh. Spusťte ho a podívejte se */wwwroot/css* složky. Teď *main2.css* soubor s tímto obsahem:

```css
body {
    background-color: #CC0000;
}
```

Sass podporuje vnoření prakticky stejné se, že menší nemá, poskytují podobné výhody. Soubory můžete rozdělit podle funkce a zahrnuty pomocí `@import` – direktiva:

```sass
@import 'anotherfile';
```

Sass podporuje také, objekty mixin používání `@mixin` – klíčové slovo se definovat a `@include` pro zahrnutí, jako v následujícím příkladu od [sass lang.com](http://sass-lang.com):

```sass
@mixin border-radius($radius) {
    -webkit-border-radius: $radius;
    -moz-border-radius: $radius;
    -ms-border-radius: $radius;
    border-radius: $radius;
}

.box { @include border-radius(10px); }
```

Kromě objekty mixin Sass také podporuje koncept dědičnosti, povolení jednu třídu jiného rozšíření. To se koncepčně podobá mixin, ale má za následek méně kód šablony stylů CSS. Použití se provádí `@extend` – klíčové slovo. Vyzkoušet objekty mixin, přidejte následující text do vašeho *main2.scss* souboru:

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

Prohlédněte si výstup v *main2.css* po spuštění `sass` úlohy v **Task Runner Explorer**:

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

Všimněte si, že všechny společné vlastnosti výstrahy mixin se opakují v každé třídě. Mixin nebyla dobrou práci, pomáhá eliminovat duplikace v době vývoje, ale stále se vytváří šablon stylů CSS s velkým množstvím duplicity, což vede k větší než potřebné soubory šablon stylů CSS – potenciální problém s výkonem.

Nyní nahraďte upozornění mixin s `.alert` třídy a změňte parametr `@include` k `@extend` (zapamatování rozšířit `.alert`, nikoli `alert`):

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

Ještě jednou spustit Sass a zkontrolujte výsledné šablon stylů CSS:

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

Nyní jsou definovány vlastnosti pouze tolikrát, kolikrát podle potřeby a lépe se vygeneruje šablon stylů CSS.

Sass také zahrnuje funkce a podmíněné logiky operace, podobně jako na hodnotu menší. Ve skutečnosti jsou velmi podobné možnosti dva jazyků.

## <a name="less-or-sass"></a>Menší nebo Sass?

Ještě není shoda, zda je obecně vhodnější použít méně nebo Sass (nebo dokonce, jestli se má přednost původní Sass nebo novější syntaxe SCSS v rámci Sass). Pravděpodobně je nejdůležitější rozhodnutí **použijte jednu z těchto nástrojů**, na rozdíl od jenom kódování souborů CSS ručně. Jakmile jste udělali, který rozhodnutí, i menší a Sass jsou vhodná rozhodnutí.

## <a name="font-awesome"></a>Knihovnou aplikací Font Awesome

Kromě preprocesory šablon stylů CSS je knihovnou aplikací Font Awesome dalším skvělým zdrojem pro používání stylů pro moderní webové aplikace. Písmo Super je sada nástrojů obsahuje více než 500 scalable vector ikony, které se můžou volně používat ve vašich webových aplikacích. Původně byla navržena pro práci s Bootstrap, ale nemá žádné závislosti na tímto rozhraním nebo na žádné knihovny jazyka JavaScript.

Nejjednodušší způsob, jak začít pracovat s knihovnou aplikací Font Awesome je přidání odkazu do něj pomocí jeho veřejné content delivery network (CDN) umístění:

```html
<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/font-awesome/4.3.0/css/font-awesome.min.css">
```

Můžete také přidat ho do projektu sady Visual Studio tak, že přidáte "závislostí" v *bower.json*:

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

Až budete mít odkaz na knihovnou aplikací Font Awesome na stránce, můžete přidat ikony pro vaši aplikaci s použitím třídy knihovnou aplikací Font Awesome, obvykle s předponou "DM-" prvkům vložené HTML (například `<span>` nebo `<i>`).  Můžete například přidat ikony jednoduché seznamy a nabídky pomocí kódu takto:

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

Tímto se vytvoří následující v prohlížeči – Poznámka: na ikonu vedle každé položky:

![seznam ikon](less-sass-fa/_static/list-icons-screenshot.png)

Můžete zobrazit úplný seznam dostupných ikon:

http://fontawesome.io/icons/

## <a name="summary"></a>Souhrn

Moderní webové aplikace stále vyžadují rychlou odezvou, plynulé návrhy, které jsou čisté, intuitivní a snadno se používá z různých zařízení. Správa složitosti šablon stylů CSS, potřebná k dosažení těchto cílů se nejlépe provádí pomocí preprocesoru je menší nebo Sass. Kromě toho sady nástrojů, jako je knihovnou aplikací Font Awesome rychle poskytnout dobře známé ikony textové navigační nabídky a tlačítka, zlepšení celkové uživatelské prostředí vaší aplikace.

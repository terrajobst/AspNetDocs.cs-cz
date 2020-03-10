---
uid: mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
title: Použití ViewData a implementace tříd ViewModel | Microsoft Docs
author: microsoft
description: Krok 6 ukazuje, jak povolit podporu pro bohatší scénáře úprav formulářů a také popisuje dva přístupy, které lze použít k předávání dat z řadičů do zobrazení:...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 5755ec4c-60f1-4057-9ec0-3a5de3a20e23
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-viewdata-and-implement-viewmodel-classes
msc.type: authoredcontent
ms.openlocfilehash: ca9775417c2e25952511a73096fb76d5d4edaea2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541606"
---
# <a name="use-viewdata-and-implement-viewmodel-classes"></a>Použití slovníku ViewData a implementace tříd ViewModel

od [Microsoftu](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 6 bezplatného [kurzu aplikace "NerdDinner"](introducing-the-nerddinner-tutorial.md) , který vás provede procesem vytvoření malé, ale dokončené webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 6 ukazuje, jak povolit podporu pro rozsáhlejší scénáře úprav formuláře a také popisuje dva přístupy, které lze použít k předávání dat z řadičů do zobrazení: ViewData a ViewModel.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme vám postupovat podle [Začínáme s kurzy pro](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [hudební úložiště](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) MVC 3 nebo MVC.

## <a name="nerddinner-step-6-viewdata-and-viewmodel"></a>NerdDinner krok 6: ViewData a ViewModel

Pokryli jsme řadu scénářů vydaných formuláře a zjistili jsme, jak implementovat podporu vytváření, aktualizace a odstranění (CRUD). Nyní budeme provádět naši implementaci DinnersController a umožníme podporu rozsáhlejších scénářů úprav formulářů. Při tomto postupu se podíváme na dva přístupy, které se dají použít k předávání dat z řadičů do zobrazení: ViewData a ViewModel.

### <a name="passing-data-from-controllers-to-view-templates"></a>Předávání dat z řadičů do zobrazení šablon

Jednou z definicí vlastností modelu MVC je striktní "oddělení obav", které pomáhá vyhovět mezi různými součástmi aplikace. Modely, řadiče a pohledy mají dobře definované role a zodpovědnosti a spolu vzájemně komunikují i mezi nimi definovanými způsoby. To pomáhá zvýšit úroveň testování a opětovného použití kódu.

Když se třída kontroleru rozhodne vykreslit odpověď HTML zpátky na klienta, zodpovídá za explicitní předání do šablony zobrazení všechna data potřebná k vykreslení odpovědi. Šablony zobrazení by nikdy neměly provádět žádné načítání dat nebo aplikační logiku – a místo toho byste měli omezit jenom vykreslování kódu, který je řízený z modelu nebo dat předaných řadičem.

Hned teď, když jsou data modelu předávaná naší třídou DinnersController do našich šablon zobrazení, jednoduchá a přímá předána – seznam objektů večeře v případě indexu () a jeden objekt večeře v případě podrobností (), upravit (), vytvořit () a odstranit (). Když do naší aplikace přidáváme více funkcí uživatelského rozhraní, často budeme potřebovat předat více než jen tato data pro vykreslování odpovědí HTML v našich šablonách zobrazení. Například můžeme chtít změnit pole země v rámci našich zobrazení pro úpravy a vytváření, aby se zobrazilo jako textové pole HTML pro DropDownList. Místo pevně zakódovat rozevírací seznam názvů zemí v šabloně zobrazení můžeme chtít vygenerovat ze seznamu podporovaných zemí, které dynamicky naplníme. Budeme potřebovat způsob, jak předat objekt večeře *a* seznam podporovaných zemí z našeho řadiče do našich šablon zobrazení.

Pojďme se podívat na dva způsoby, jak to můžeme provést.

### <a name="using-the-viewdata-dictionary"></a>Použití slovníku ViewData

Základní třída kontroleru zpřístupňuje vlastnost slovníku "ViewData", kterou lze použít k předání dalších datových položek z řadičů do zobrazení.

Například pro podporu scénáře, kdy chceme změnit textové pole země v rámci našeho zobrazení pro úpravy, aby se zobrazilo jako textové pole HTML pro DropDownList, můžeme aktualizovat objekt SelectList, který se dá použít jako m. Odel země DropDownList.

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample1.cs)]

Konstruktor SelectList výše přijímá seznam okresů k naplnění downlist s a také aktuálně vybrané hodnoty.

Potom můžeme šablonu zobrazení Edit. aspx aktualizovat tak, aby používala pomocnou metodu HTML. DropDownList () namísto pomocné metody HTML. TextBox (), kterou jsme použili dříve:

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample2.aspx)]

Pomocná metoda HTML. DropDownList () výše přijímá dva parametry. První je název elementu HTML Form pro výstup. Druhým je model "SelectList", který jsme předali prostřednictvím slovníku ViewData. K přetypování typu C# v rámci slovníku jako SelectList používáme klíčové slovo As.

A teď když spouštíme naši aplikaci a přistupuje se k adrese URL */Dinners/Edit/1* v našem prohlížeči, uvidíme, že jsme aktualizovali naše uživatelské rozhraní pro úpravy, aby se zobrazila DropDownList země namísto textového pole:

![](use-viewdata-and-implement-viewmodel-classes/_static/image1.png)

Vzhledem k tomu, že jsme vygenerovali šablonu zobrazení pro úpravy z metody úprav HTTP-POST (ve scénářích, kdy dojde k chybám), chceme, abyste se ujistili, že tuto metodu také aktualizujeme a přidáte SelectList do ViewData, když se šablona zobrazení vykresluje v chybových scénářích:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample3.cs)]

A teď náš scénář úprav DinnersController podporuje DropDownList.

### <a name="using-a-viewmodel-pattern"></a>Použití vzoru ViewModel

Přístup ke slovníku ViewData má výhodu poměrně rychlé a snadné implementace. Někteří vývojáři nepoužívají slovníky založené na řetězcích, ale vzhledem k tomu, že překlepy mohou vést k chybám, které nebudou zachyceny v době kompilace. Slovník ViewData bez typu také vyžaduje použití operátoru "as" nebo přetypování při použití jazyka silného typu, jako C# v šabloně zobrazení.

Alternativním postupem, který můžeme použít, je, že se jedná o jeden často označovaný jako vzor "ViewModel". Při použití tohoto modelu vytvoříme třídy silného typu, které jsou optimalizované pro naše konkrétní scénáře zobrazení a které zveřejňují vlastnosti pro dynamické hodnoty/obsah, které jsou potřebné pro naše šablony zobrazení. Naše třídy kontroleru pak mohou naplnit a předávat tyto třídy optimalizované pro zobrazení do naší šablony zobrazení, která se má použít. To umožňuje v šablonách zobrazení používat technologii IntelliSense pro ověřování, kontrolu doby kompilace a editory.

Pokud například chcete povolit scénáře úprav formulářů na večeři, můžeme vytvořit třídu "DinnerFormViewModel", která je níže, která zveřejňuje dvě vlastnosti silného typu: objekt večeře a model SelectList potřebný k naplnění zemí DropDownList:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample4.cs)]

Pak můžeme aktualizovat metodu akce Edit () a vytvořit DinnerFormViewModel pomocí objektu večeře, který načteme z našeho úložiště, a pak ho předat naší šabloně zobrazení:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample5.cs)]

Pak aktualizujeme naši šablonu zobrazení tak, že očekává "DinnerFormViewModel" místo "večeře" tím, že se změní atribut inherits v horní části stránky Edit. aspx, například:

[!code-cshtml[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample6.cshtml)]

Jakmile to uděláte, bude IntelliSense pro vlastnost "model" v rámci šablony zobrazení aktualizován, aby odrážel objektový model DinnerFormViewModel typu, který předáváme:

![](use-viewdata-and-implement-viewmodel-classes/_static/image2.png)

![](use-viewdata-and-implement-viewmodel-classes/_static/image3.png)

Náš kód pro zobrazení můžeme potom aktualizovat, aby se tam pracoval. Všimněte si, že neměníme názvy vstupních elementů, které vytváříme (prvky formuláře se budou pořád jmenovat "title", "země") – ale aktualizujeme pomocné metody HTML pro načtení hodnot pomocí třídy DinnerFormViewModel:

[!code-aspx[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample7.aspx)]

Také aktualizujeme metodu pro úpravu post na použití třídy DinnerFormViewModel při vykreslování chyb:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample8.cs)]

Můžeme také aktualizovat naše metody akce Create () pro opětovné použití přesně stejné třídy *DinnerFormViewModel* , aby bylo možné v nich povolit země DropDownList. Níže je uvedená implementace HTTP-GET:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample9.cs)]

Níže je implementace metody HTTP-POST Create:

[!code-csharp[Main](use-viewdata-and-implement-viewmodel-classes/samples/sample10.cs)]

A teď i naše obrazovky pro úpravy a vytváření podporují downlists pro výběr země.

### <a name="custom-shaped-viewmodel-classes"></a>Vlastní třídy ViewModel ve tvaru

Ve výše uvedeném scénáři DinnerFormViewModel třída přímo zpřístupňuje objekt modelu večeře jako vlastnost spolu s podpůrnou vlastností modelu SelectList. Tento přístup funguje u scénářů, kde uživatelské rozhraní HTML, které chceme vytvořit v rámci naší šablony zobrazení, odpovídá poměrně blízko k našemu objektu doménového modelu.

V případech, kdy se nejedná o případ, jednu z možností, kterou můžete použít, je vytvořit vlastní třídu ViewModel, jejíž objektový model je více optimalizováno pro spotřebu zobrazením – a který by se mohl zcela lišit od objektu základního doménového modelu. Může například potenciálně vystavovat různé názvy vlastností nebo agregované vlastnosti shromážděné z více objektů modelu.

Vlastní třídy ViewModel se dají použít k předávání dat z řadičů do zobrazení pro vykreslování a také k tomu, aby pomohly zpracovávat data formuláře odeslaná zpět na metodu akce kontroleru. V tomto případě se může jednat o metodu akce aktualizovat objekt ViewModel s daty publikovanými formulářem a pak pomocí instance ViewModel namapovat nebo načíst skutečný objekt doménového modelu.

Vlastní třídy ViewModel můžou poskytovat skvělou flexibilitu a je možné je prozkoumat kdykoli, co v šablonách zobrazení vyhledáte kód pro vykreslení, nebo pomocí kódu formuláře, který je v rámci vašich akcí, a to tak, aby se dosáhlo příliš složitosti. Často se jedná o znaménko, že vaše doménové modely nedokonale neodpovídají uživatelskému rozhraní, které vygenerujete, a že vám může pomáhat mezilehlě ViewModel třída s vlastním tvarem.

### <a name="next-step"></a>Další krok

Teď se podíváme na to, jak můžeme použít částečné a hlavní stránky k opakovanému použití a sdílení uživatelského rozhraní napříč naší aplikací.

> [!div class="step-by-step"]
> [Předchozí](provide-crud-create-read-update-delete-data-form-entry-support.md)
> [Další](re-use-ui-using-master-pages-and-partials.md)

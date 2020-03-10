---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: Implementace efektivního stránkování dat | Microsoft Docs
author: microsoft
description: Krok 8 ukazuje, jak přidat podporu stránkování do naší adresy URL/Dinners, aby se místo zobrazení tisíců večeře najednou zobrazil jenom 10 nadcházejících večeři na...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: 2d9a0dba381b71755ac626f76d52bc5bcb434447
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601050"
---
# <a name="implement-efficient-data-paging"></a>Implementace efektivního stránkování dat

od [Microsoftu](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 8 bezplatného [kurzu aplikace "NerdDinner"](introducing-the-nerddinner-tutorial.md) , který vás provede procesem vytvoření malé, ale dokončené webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 8 ukazuje, jak přidat podporu stránkování k naší adrese URL/Dinners, aby se místo zobrazení tisíců večeře najednou zobrazovaly jenom 10 nadcházejících večeře najednou a aby koncoví uživatelé mohli vracet zpět a předávat dál celý seznam v uživatelsky přívětivém způsobu.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme vám postupovat podle [Začínáme s kurzy pro](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [hudební úložiště](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) MVC 3 nebo MVC.

## <a name="nerddinner-step-8-paging-support"></a>NerdDinner krok 8: Podpora stránkování

Pokud je náš web úspěšný, bude mít tisíce nadcházejících večeři. Musíme zajistit, aby se toto uživatelské rozhraní nacházelo tak, aby zpracovávala všechny tyto hostiny, a umožní uživatelům jejich procházení. Pokud to chcete povolit, přidáme podporu stránkování na naši adresu URL */Dinners* , aby se místo zobrazení tisíců večeře najednou zobrazovaly jenom 10 nadcházejících večeře najednou a aby koncoví uživatelé mohli vracet zpět a předávat dál celý seznam v uživatelsky přívětivém způsobu.

### <a name="index-action-method-recap"></a>Index () akce metody rekapitulace

Metoda Action () v rámci naší třídy DinnersController v současné době vypadá následovně:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

Při odeslání požadavku na adresu URL */Dinners* se načte seznam všech nadcházejících večeře a potom se vykreslí jejich seznam:

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a>Principy IQueryable&lt;T&gt;

*IQueryable&lt;t&gt;* je rozhraní, které bylo zavedeno pomocí LINQ jako součást .NET 3,5. Umožňuje výkonné scénáře odloženého provádění, které můžeme využít k implementaci podpory stránkování.

V našem DinnerRepository vracíme&gt; sekvenci IQueryable&lt;večeře z naší metody FindUpcomingDinners ():

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

Objekt IQueryable&lt;večeře&gt; vrácený metodou FindUpcomingDinners () zapouzdřuje dotaz k načtení objektů večeře z naší databáze pomocí LINQ to SQL. Důležité je, aby se dotaz nespouštěl proti databázi, dokud se nepokusíme o přístup k datům v dotazu, nebo dokud na ni nevoláme metodu ToList – (). Kód, který volá naši metodu FindUpcomingDinners (), může volitelně zvolit přidání dalších "zřetězených" operací/filtrů do objektu IQueryable&lt;večeře&gt; před provedením dotazu. LINQ to SQL je pak dostatečně inteligentní, aby se při požadavku na data spustil Kombinovaný dotaz na databázi.

Aby bylo možné implementovat logiku stránkování, můžeme aktualizovat metodu akce index () naší DinnersController tak, aby platila další "Skip" a "přenést" operátory pro vrácenou aktualizaci&lt;IQueryable&gt; sekvenci před voláním ToList – ():

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

Výše uvedený kód přeskočí za prvních 10 nadcházejících večeři v databázi a vrátí zpět 20 večeři. LINQ to SQL je dostatečně inteligentní, aby bylo možné vytvořit optimalizovaný dotaz SQL, který provede tuto logiku v databázi SQL, a ne na webovém serveru. To znamená, že i když máme miliony nadcházejících večeře v databázi, v rámci této žádosti se načte jenom 10, které chceme (což zajistí efektivní a škálovatelné).

### <a name="adding-a-page-value-to-the-url"></a>Přidání hodnoty "Page" do adresy URL

Místo pevného kódování konkrétního rozsahu stránky chceme, aby naše adresy URL zahrnovaly parametr "stránka", který označuje, který rozsah večeře uživatel požaduje.

#### <a name="using-a-querystring-value"></a>Použití hodnoty QueryString

Následující kód demonstruje, jak můžeme aktualizovat metodu akce index () na podporu parametru QueryString a povolit adresy URL jako */Dinners? Page = 2*:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

Výše uvedená metoda akce index () obsahuje parametr s názvem "Page". Parametr je deklarován jako celé číslo s možnou hodnotou null (to znamená to, co int? označuje). To znamená, že */Dinners? Page = 2* URL způsobí, že hodnota "2" bude předána jako hodnota parametru. Adresa URL */Dinners* (bez hodnoty řetězce dotazu) způsobí předání hodnoty null.

Hodnota stránky se vynásobí velikostí stránky (v tomto případě 10 řádků) a určíte, kolik večeře se má přeskočit. Používáme [ C# "slučovací" operátor (??)](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) , který je užitečný při práci s typy s možnou hodnotou null. Výše uvedený kód přiřadí hodnotu 0, pokud má parametr stránky hodnotu null.

#### <a name="using-embedded-url-values"></a>Použití vložených hodnot URL

Alternativou k použití hodnoty QueryString by bylo vložit parametr stránky do samotné vlastní adresy URL. Například: */Dinners/Page/2* nebo */Dinners/2*. ASP.NET MVC zahrnuje výkonný modul pro směrování adres URL, který usnadňuje podporu podobných scénářů.

Můžeme registrovat vlastní pravidla směrování, která mapují všechny příchozí adresy URL nebo formát adresy URL na libovolnou třídu kontroleru nebo metodu akce, kterou chceme. Vše, co musíme udělat, je otevřít soubor Global. asax v rámci našeho projektu:

![](implement-efficient-data-paging/_static/image2.png)

A pak zaregistrujte nové pravidlo mapování pomocí pomocné metody MapRoute (), jako je první volání tras. MapRoute () níže:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

Výše je registrace nového pravidla směrování s názvem "UpcomingDinners". Oznamujeme, že má formát adresy URL "večeře/stránka/{Page}" – kde {Page} je hodnota parametru vložená v rámci adresy URL. Třetí parametr metody MapRoute () označuje, že by měly být mapovány adresy URL, které odpovídají tomuto formátu, metodě akce index () třídy DinnersController.

Můžeme použít přesný index () kód, který jsme předtím používali ve scénáři QueryString – s výjimkou toho, že tento parametr Page bude pocházet z adresy URL, nikoli řetězce dotazu:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

A teď když aplikaci spustíme a zadáte do */Dinners* , zobrazí se prvních 10 nadcházejících večeři:

![](implement-efficient-data-paging/_static/image3.png)

A když zadáte v */Dinners/Page/1* , zobrazí se další stránka večeře:

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a>Přidávání uživatelského rozhraní pro navigaci stránky

Posledním krokem k dokončení našeho scénáře stránkování bude implementace "Next" a "předchozí" navigační uživatelské rozhraní v naší šabloně zobrazení, aby uživatelé mohli snadno přeskočit data z večeře.

Abychom to správně implementovali, budeme potřebovat znát celkový počet večeře v databázi a také počet stránek dat, ke kterým se tato data vztahují. Pak bude potřeba počítat s tím, jestli je aktuálně požadovaná hodnota "stránka" na začátku nebo na konci dat, a odpovídajícím způsobem zobrazit nebo skrýt uživatelské rozhraní "předchozí" a "Další". Tuto logiku můžeme implementovat v rámci naší metody akce index (). Alternativně můžeme do našeho projektu přidat pomocnou třídu, která zapouzdřuje tuto logiku ve více opakovaně použitelném způsobu.

Níže je jednoduchá pomocná třída "PaginatedList", která je odvozena od třídy seznamu&lt;T&gt; kolekce integrovaná do .NET Framework. Implementuje znovu použitelnou třídu kolekce, kterou lze použít k stránkování jakékoli sekvence dat IQueryable. V naší aplikaci NerdDinner budeme mít k dispozici práci prostřednictvím rozhraní IQueryable&lt;večeře&gt; výsledky, ale je možné, že se to dá jednoduše snadno použít proti rozhraní IQueryable&lt;produkt&gt; nebo IQueryable&lt;&gt; výsledky v jiných scénářích aplikací:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

Všimněte si nad tím, jak se počítá a potom zpřístupňuje vlastnosti jako "PageIndex", "PageSize", "TotalCount" a "TotalPages". Pak zpřístupní dvě pomocné vlastnosti "HasPreviousPage" a "HasNextPage", které označují, zda je stránka dat v kolekci na začátku nebo na konci původní sekvence. Výše uvedený kód způsobí, že budou spuštěny dva dotazy SQL – první z nich získá celkový počet objektů večeře (nevrátí objekty – místo toho provede příkaz SELECT COUNT, který vrátí celé číslo) a druhý pro načtení pouze řádků data, která potřebujeme z naší databáze pro aktuální stránku dat.

Pak můžeme aktualizovat pomocnou metodu DinnersController. index () a vytvořit PaginatedList&lt;večeře&gt; z našeho výsledku DinnerRepository. FindUpcomingDinners () a předat ji do naší šablony zobrazení:

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

Pak můžeme aktualizovat šablonu zobrazení \Views\Dinners\Index.aspx tak, aby dědila z ViewPage&lt;NerdDinner. helps. PaginatedList&lt;večeře&gt;&gt; místo ViewPage&lt;IEnumerable&lt;večeře&gt;&gt;a potom přidat následující kód do dolní části našeho zobrazení – šablony pro zobrazení nebo skrytí dalšího a předchozího navigačního rozhraní:

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

Všimněte si, jak se používá pomocná metoda HTML. RouteLink () ke generování našich hypertextových odkazů. Tato metoda je podobná pomocné metodě HTML. ActionLink (), kterou jsme používali dřív. Rozdílem je, že generujeme adresu URL pomocí pravidla směrování "UpcomingDinners", které jsme nastavili v rámci našeho souboru Global. asax. Tím se zajistí, že vygenerujeme adresy URL pro metodu akce index (), která má formát: */Dinners/Page/{Page}* – kde hodnota {Page} je proměnná, kterou poskytujeme výše v závislosti na aktuální vlastnosti pageIndex.

A teď i po opětovném spuštění naší aplikace se v našem prohlížeči zobrazí 10 večeři v čase:

![](implement-efficient-data-paging/_static/image5.png)

V dolní části stránky máme taky &lt;&lt;&lt; a &gt;uživatelské rozhraní pro navigaci v &gt;, které nám umožňuje přeskočit dopředu a zpět na naše data pomocí adres URL přístupného pro vyhledávač:&gt;

![](implement-efficient-data-paging/_static/image6.png)

| **Vedlejší téma: princip dopadu sady IQueryable&lt;T&gt;** |
| --- |
| IQueryable&lt;T&gt; je velmi výkonná funkce, která umožňuje řadu zajímavých odložených scénářů provádění (například dotazy na stránkování a skládání). Stejně jako u všech výkonných funkcí chcete být opatrní při jejich používání a zajistěte, aby nemohly být zneužití. Je důležité rozpoznat, že vrácení sady IQueryable&lt;T&gt; výsledek z úložiště umožňuje volajícímu kódu připojit k metodám zřetězených operátorů, a tak se zúčastnit v konečném provádění dotazu. Pokud nechcete, aby tato možnost poskytovala volající kód, měli byste vrátit objekty IList&lt;T&gt; nebo IEnumerable&lt;T&gt; výsledky, které obsahují výsledky dotazu, který již byl proveden. V případě scénářů stránkování by to vyžadovalo vložení skutečné logiky stránkování dat do metody úložiště, která se volá. V tomto scénáři můžeme aktualizovat naši vyhledávací metodu FindUpcomingDinners () tak, aby měla signaturu, která vrátila hodnotu PaginatedList: PaginatedList&lt; večeře&gt; FindUpcomingDinners (int pageIndex, int pageSize) {} nebo vraťte zpět objekt IList&lt;večeře&gt;a použijte parametr "totalCount" out, který vrátí celkový počet večeře: IList&lt;večeře&gt; FindUpcomingDinners (int pageIndex, int pageSize, out int totalCount) {} |

### <a name="next-step"></a>Další krok

Teď se podíváme, jak můžeme do naší aplikace přidat podporu ověřování a autorizace.

> [!div class="step-by-step"]
> [Předchozí](re-use-ui-using-master-pages-and-partials.md)
> [Další](secure-applications-using-authentication-and-authorization.md)

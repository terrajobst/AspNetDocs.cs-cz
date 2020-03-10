---
uid: web-forms/overview/data-access/caching-data/caching-data-in-the-architecture-cs
title: Ukládání dat do mezipaměti v architektuřeC#() | Microsoft Docs
author: rick-anderson
description: V předchozím kurzu jsme zjistili, jak používat ukládání do mezipaměti v prezentační vrstvě. V tomto kurzu se naučíme, jak využít naši vrstvený architekt...
ms.author: riande
ms.date: 05/30/2007
ms.assetid: d29a7c41-0628-4a23-9dfc-bfea9c6c1054
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-in-the-architecture-cs
msc.type: authoredcontent
ms.openlocfilehash: 192cadb8e2f862ac2a97a36b375e247b281ece93
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78551168"
---
# <a name="caching-data-in-the-architecture-c"></a>Ukládání dat do mezipaměti v architektuře (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_59_CS.exe) nebo [Stáhnout PDF](caching-data-in-the-architecture-cs/_static/datatutorial59cs1.pdf)

> V předchozím kurzu jsme zjistili, jak používat ukládání do mezipaměti v prezentační vrstvě. V tomto kurzu se naučíme, jak využít naši vrstvenou architekturu pro ukládání dat do mezipaměti v rámci vrstvy obchodní logiky. To provedeme rozšířením architektury, aby zahrnovala vrstvu ukládání do mezipaměti.

## <a name="introduction"></a>Úvod

Jak jsme viděli v předchozím kurzu, ukládání dat v prvku ObjectDataSource s do mezipaměti je tak jednoduché jako nastavení několika vlastností. Prvek ObjectDataSource bohužel aplikuje ukládání do mezipaměti do prezentační vrstvy, která úzce Couples zásady ukládání do mezipaměti pomocí stránky ASP.NET. Jedním z důvodů, proč vytvořit vrstvenou architekturu, je to, aby bylo možné tyto vazby přerušit. Vrstva obchodní logiky například odděluje obchodní logiku ze stránek ASP.NET, zatímco vrstva přístupu k datům odděluje údaje o přístupu k datům. Toto odpojujení obchodní logiky a podrobností přístupu k datům je preferované, protože díky tomu je systém čitelnější, udržovatelnější a flexibilnější, aby se změnila. Umožňuje taky znalosti v doméně a rozdělení práce, které vývojář pracuje na prezentační vrstvě. nemusíte být obeznámeni s podrobnostmi o databázi, aby bylo možné svoji úlohu provést. Oddělení zásad ukládání do mezipaměti z prezentační vrstvy nabízí podobné výhody.

V tomto kurzu rozsadíme naši architekturu tak, aby zahrnovala *vrstvu ukládání do mezipaměti* (nebo CL pro krátké), která využívá naše zásady pro ukládání do mezipaměti. Vrstva ukládání do mezipaměti bude zahrnovat `ProductsCL` třídu, která poskytuje přístup k informacím o produktech pomocí metod jako `GetProducts()`, `GetProductsByCategoryID(categoryID)`a tak dále, které při vyvolání se nejprve pokusí načíst data z mezipaměti. Pokud je mezipaměť prázdná, tyto metody vyvolá příslušnou metodu `ProductsBLL` v knihoven BLL, která by pak získala data z DAL. Metody `ProductsCL` mezipaměť dat načtených z knihoven BLL před jejich vrácením.

Jak ukazuje obrázek 1, CL se nachází mezi vrstvami prezentace a obchodní logiky.

![Vrstva ukládání do mezipaměti (CL) je další vrstva v naší architektuře.](caching-data-in-the-architecture-cs/_static/image1.png)

**Obrázek 1**: vrstva ukládání do mezipaměti (CL) je další vrstva v naší architektuře.

## <a name="step-1-creating-the-caching-layer-classes"></a>Krok 1: vytvoření tříd vrstev pro ukládání do mezipaměti

V tomto kurzu vytvoříme velmi jednoduchý CL s jednou třídou `ProductsCL`, která má jenom několik metody. Sestavení kompletní vrstvy ukládání do mezipaměti pro celou aplikaci bude vyžadovat vytváření tříd `CategoriesCL`, `EmployeesCL`a `SuppliersCL` a poskytnutí metody v těchto třídách vrstev pro ukládání do mezipaměti pro jednotlivé metody přístupu k datům nebo úprav v knihoven BLL. Stejně jako u knihoven BLL a DAL by vrstva ukládání do mezipaměti měla být ideálním způsobem implementována jako samostatný projekt knihovny tříd; budeme ho ale implementovat jako třídu ve složce `App_Code`.

Chcete-li efektivněji oddělit třídy CL z tříd DAL a knihoven BLL, nechte vytvořit novou podsložku ve složce `App_Code`. Pravým tlačítkem myši klikněte na složku `App_Code` v Průzkumník řešení, vyberte možnost Nová složka a pojmenujte novou složku `CL`. Po vytvoření této složky do ní přidejte novou třídu s názvem `ProductsCL.cs`.

![Přidejte novou složku s názvem CL a třídu s názvem ProductsCL.cs.](caching-data-in-the-architecture-cs/_static/image2.png)

**Obrázek 2**: přidejte novou složku s názvem `CL` a třídu s názvem `ProductsCL.cs`

Třída `ProductsCL` by měla obsahovat stejnou sadu metod přístupu k datům a úprav, jak se nachází v odpovídající třídě vrstvy obchodní logiky (`ProductsBLL`). Místo vytváření všech těchto metod teď stačí sestavit pár, abyste se mohli cítit vzory, které používá CL. Konkrétně přidáte do kroku 3 metody `GetProducts()` a `GetProductsByCategoryID(categoryID)` a `UpdateProduct` přetížení v kroku 4. Zbývající metody `ProductsCL` a třídy `CategoriesCL`, `EmployeesCL`a `SuppliersCL` můžete přidat do svého volného místa.

## <a name="step-2-reading-and-writing-to-the-data-cache"></a>Krok 2: čtení a zápis do mezipaměti dat

Funkce ukládání ObjectDataSource do mezipaměti v předchozím kurzu interně používá mezipaměť dat ASP.NET k ukládání dat načtených z knihoven BLL. Mezipaměť dat je také k dispozici programově ze tříd ASP.NET stránky kódu na pozadí nebo z tříd v architektuře webové aplikace s. Pro čtení a zápis do mezipaměti dat ze třídy ASP.NET stránky s kódem na pozadí použijte následující vzor:

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample1.cs)]

Metoda [`Cache` třídy](https://msdn.microsoft.com/library/system.web.caching.cache.aspx) s [`Insert`](https://msdn.microsoft.com/library/system.web.caching.cache.insert.aspx) má mnoho přetížení. `Cache["key"] = value` a `Cache.Insert(key, value)` jsou synonyma a obě do mezipaměti přidají položku pomocí zadaného klíče bez definovaného vypršení platnosti. Obvykle chceme zadat vypršení platnosti při přidávání položky do mezipaměti, buď jako závislosti, vypršení časového limitu nebo obojího. K poskytnutí informací o vypršení platnosti závislosti nebo času použijte jedno z dalších přetížení `Insert` metody.

Metody vrstev pro ukládání do mezipaměti musí nejdřív ověřit, jestli jsou požadovaná data v mezipaměti, a pokud ano, vrátí se z ní. Pokud požadovaná data nejsou v mezipaměti, musí být vyvolána odpovídající metoda knihoven BLL. Návratová hodnota by měla být uložená v mezipaměti a pak se vrátila, jak ukazuje následující sekvenční diagram.

![Metody ukládání vrstvy do mezipaměti vrací data z mezipaměti, pokud je k dispozici.](caching-data-in-the-architecture-cs/_static/image3.png)

**Obrázek 3**: metody vrstvy ukládání do mezipaměti vrací data z mezipaměti, pokud jsou k dispozici.

Pořadí znázorněné na obrázku 3 je provedeno v třídách CL pomocí následujícího vzoru:

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample2.cs)]

Tady je *typ* dat ukládaných do mezipaměti `Northwind.ProductsDataTable`, například když *klíč* je klíč, který jedinečně identifikuje položku mezipaměti. Pokud položka se zadaným *klíčem* není v mezipaměti, pak se *instance* `null` a data se načtou z příslušné metody knihoven BLL a přidají se do mezipaměti. Při dosažení `return instance` *instance* obsahuje odkaz na data, buď z mezipaměti, nebo z knihoven BLL.

Při přístupu k datům z mezipaměti nezapomeňte použít výše uvedený vzor. Následující vzor, který je na první pohled, vypadá jako ekvivalent, obsahuje drobný rozdíl, který představuje podmínku časování. Konflikty časování je obtížné ladit, protože se odhalují zřídka a je obtížné je reprodukována.

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample3.cs)]

Rozdíl v této druhé, nesprávný fragment kódu je místo uložení odkazu na položku v mezipaměti v místní proměnné, k datové mezipaměti se dostanete přímo v podmíněném příkazu *a* v `return`. Představte si, že po dosažení tohoto kódu je `Cache["key"]` ne`null`, ale před dosažením příkazu `return` systém vyloučí *klíč* z mezipaměti. V tomto vzácném případě kód vrátí `null` hodnotu, nikoli objekt očekávaného typu.

> [!NOTE]
> Mezipaměť dat je bezpečná pro přístup z více vláken, takže nemusíte synchronizovat přístup k vláknům pro jednoduché čtení nebo zápisy. Pokud ale potřebujete provést více operací s daty v mezipaměti, které je potřeba atomicky, zodpovídáte za implementaci zámku nebo nějakého jiného mechanismu, abyste zajistili bezpečnost vlákna. Další informace najdete v tématu [synchronizace přístupu ke službě ASP.NET Cache](http://www.ddj.com/184406369) .

Položka může být programově vyřazena z mezipaměti dat pomocí [metody`Remove`](https://msdn.microsoft.com/library/system.web.caching.cache.remove.aspx) , například takto:

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample4.cs)]

## <a name="step-3-returning-product-information-from-theproductsclclass"></a>Krok 3: vrácení informací o produktu z`ProductsCL`třídy

Pro tento kurz umožňuje implementovat dvě metody pro vracení informací o produktu z `ProductsCL` třídy: `GetProducts()` a `GetProductsByCategoryID(categoryID)`. Podobně jako u `ProductsBL` třídy v vrstvě obchodní logiky metoda `GetProducts()` v CL vrátí informace o všech produktech jako objekt `Northwind.ProductsDataTable`, zatímco `GetProductsByCategoryID(categoryID)` vrátí všechny produkty ze zadané kategorie.

Následující kód ukazuje část metod v `ProductsCL` třídy:

[!code-vb[Main](caching-data-in-the-architecture-cs/samples/sample5.vb)]

Nejprve si poznamenejte atributy `DataObject` a `DataObjectMethodAttribute` použité pro třídu a metody. Tyto atributy poskytují informace průvodci ObjectDataSource s, který označuje, jaké třídy a metody by se měly zobrazit v krocích průvodce s. Vzhledem k tomu, že třídy CL a metody budou k dispozici z prvku ObjectDataSource v prezentační vrstvě, byly přidány tyto atributy pro zlepšení prostředí v době návrhu. Přečtěte si kurz [Vytvoření vrstvy obchodní logiky](../introduction/creating-a-business-logic-layer-cs.md) a podrobnější popis těchto atributů a jejich efektů.

V metodách `GetProducts()` a `GetProductsByCategoryID(categoryID)` je data vrácená z metody `GetCacheItem(key)` přiřazena místní proměnné. Metoda `GetCacheItem(key)`, kterou prověříme krátce, vrátí konkrétní položku z mezipaměti na základě zadaného *klíče*. Pokud nejsou taková data v mezipaměti nalezena, jsou načtena z odpovídající metody třídy `ProductsBLL` a poté přidány do mezipaměti pomocí metody `AddCacheItem(key, value)`.

Rozhraní metody `GetCacheItem(key)` a `AddCacheItem(key, value)` s mezipamětí dat, čtení a zápis hodnot v uvedeném pořadí. Metoda `GetCacheItem(key)` je jednodušší z těchto dvou. Jednoduše vrátí hodnotu z třídy Cache pomocí *klíče*předaného:

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample6.cs)]

`GetCacheItem(key)` nepoužívá hodnotu *klíče* jako dodané, ale místo toho volá metodu `GetCacheKey(key)`, která vrací *klíč* , který je v ProductsCache-. `MasterCacheKeyArray`, která obsahuje řetězec ProductsCache, je také používána metodou `AddCacheItem(key, value)`, jak uvidíme za chvíli.

Z třídy ASP.NET s kódem na pozadí lze mezipaměť dat použít pomocí vlastnosti `Page` třídy s [`Cache`](https://msdn.microsoft.com/library/system.web.ui.page.cache.aspx)a umožňuje syntaxi jako `Cache["key"] = value`, jak je popsáno v kroku 2. Z třídy v rámci architektury je k datové mezipaměti možné přistupovat buď pomocí `HttpRuntime.Cache`, nebo `HttpContext.Current.Cache`. Seznámení s modulem pro zápis na blogu [Johnsonem](https://weblogs.asp.net/pjohnson/default.aspx) [. cache vs. HttpContext. Current. cache](https://weblogs.asp.net/pjohnson/httpruntime-cache-vs-httpcontext-current-cache) poznámky k mírnému využití výkonu při použití `HttpRuntime` místo `HttpContext.Current`; v důsledku toho `ProductsCL` používá `HttpRuntime`.

> [!NOTE]
> Pokud je vaše architektura implementována pomocí projektů knihovny tříd, budete muset přidat odkaz na sestavení `System.Web`, aby bylo možné použít třídy [httpRuntime](https://msdn.microsoft.com/library/system.web.httpruntime.aspx) a [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx) .

Pokud se položka v mezipaměti nenajde, metody `ProductsCL` třídy s získají data z knihoven BLL a do mezipaměti přidáte pomocí metody `AddCacheItem(key, value)`. K přidání *hodnoty* do mezipaměti můžeme použít následující kód, který používá vypršení druhé doby 60:

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample7.cs)]

`DateTime.Now.AddSeconds(CacheDuration)` určuje časový limit vypršení platnosti 60 sekund v budoucnosti, zatímco [`System.Web.Caching.Cache.NoSlidingExpiration`](https://msdn.microsoft.com/library/system.web.caching.cache.noslidingexpiration(vs.80).aspx) označuje, že neexistují žádné klouzavé vypršení platnosti. I když toto přetížení `Insert` metody obsahuje vstupní parametry pro absolutní i klouzavé vypršení platnosti, můžete zadat pouze jednu z těchto dvou. Pokud se pokusíte zadat absolutní a časový rozsah, metoda `Insert` vyvolá výjimku `ArgumentException`.

> [!NOTE]
> Tato implementace metody `AddCacheItem(key, value)` v současnosti obsahuje nějaké nedostatky. Tyto problémy budeme řešit a překonat v kroku 4.

## <a name="step-4-invalidating-the-cache-when-the-data-is-modified-through-the-architecture"></a>Krok 4: zrušení platnosti mezipaměti při změně dat pomocí architektury

Spolu s metodami načítání dat musí vrstva ukládání do mezipaměti poskytovat stejné metody jako knihoven BLL pro vkládání, aktualizaci a odstraňování dat. Metody změny dat CL. nemění data uložená v mezipaměti, ale místo toho volají knihoven BLL s odpovídající metodou změny dat a pak neověřuje mezipaměť. Jak jsme viděli v předchozím kurzu, jedná se o stejné chování, které prvek ObjectDataSource použije, když jsou povolené jeho funkce ukládání do mezipaměti a jsou vyvolány `Insert`, `Update`nebo `Delete` metody.

Následující přetížení `UpdateProduct` ukazuje, jak implementovat metody změny dat v CL:

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample8.cs)]

Je vyvolána vhodná metoda vrstvy pro úpravu dat, ale předtím, než se vrátí jeho odpověď, musíme tuto mezipaměť znehodnotit. Neověřování mezipaměti bohužel není jednoduché, protože `ProductsCL` třídy s `GetProducts()` a `GetProductsByCategoryID(categoryID)` metody každý přidávají položky do mezipaměti s různými klíči a metoda `GetProductsByCategoryID(categoryID)` pro každou jedinečnou hodnotu *KódKategorie*přidá jinou položku mezipaměti.

Při devalidaci mezipaměti musíme odebrat *všechny* položky, které mohou být přidány třídou `ProductsCL`. To lze provést přidružením *závislosti mezipaměti* ke každé položce přidané do mezipaměti v metodě `AddCacheItem(key, value)`. V zásadě může být závislost mezipaměti jinou položkou v mezipaměti, souborem v systému souborů nebo daty z databáze Microsoft SQL Server. Když se závislost změní nebo odebere z mezipaměti, položky mezipaměti, ke kterým je přidružená, se automaticky vyloučí z mezipaměti. Pro tento kurz chceme v mezipaměti vytvořit další položku, která slouží jako závislost mezipaměti pro všechny položky přidané prostřednictvím třídy `ProductsCL`. Tímto způsobem lze z mezipaměti odebrat všechny tyto položky pouhým odebráním závislosti mezipaměti.

Aktualizujte metodu `AddCacheItem(key, value)` tak, aby se všechny položky přidané do mezipaměti prostřednictvím této metody přidružil k závislosti jedné mezipaměti:

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample9.cs)]

`MasterCacheKeyArray` je pole řetězců, které obsahuje jednu hodnotu ProductsCache. Nejprve se položka mezipaměti přidá do mezipaměti a přiřadí se aktuální datum a čas. Pokud položka mezipaměti již existuje, je aktualizována. V dalším kroku se vytvoří závislost mezipaměti. Konstruktor [`CacheDependency` třídy](https://msdn.microsoft.com/library/system.web.caching.cachedependency(VS.80).aspx) s má několik přetížení, ale ta, která se používá tady, očekává dva vstupy `string` pole. První z nich určuje sadu souborů, které mají být použity jako závislosti. Vzhledem k tomu, že nechceme použít žádné závislosti založené na souborech, je pro první vstupní parametr použita hodnota `null`. Druhý vstupní parametr určuje sadu klíčů mezipaměti, které se mají použít jako závislosti. Tady určíme naši jedinou závislost `MasterCacheKeyArray`. `CacheDependency` pak předává do metody `Insert`.

S touto úpravou `AddCacheItem(key, value)`je zrušení platnosti mezipaměti stejně jednoduché jako odebrání závislosti.

[!code-csharp[Main](caching-data-in-the-architecture-cs/samples/sample10.cs)]

## <a name="step-5-calling-the-caching-layer-from-the-presentation-layer"></a>Krok 5: volání vrstvy ukládání do mezipaměti z prezentační vrstvy

Třídy a metody pro ukládání do mezipaměti lze použít pro práci s daty pomocí technik, které jsme prozkoumali v těchto kurzech. Chcete-li znázornit práci s daty uloženými v mezipaměti, uložte změny do třídy `ProductsCL` a poté otevřete stránku `FromTheArchitecture.aspx` ve složce `Caching` a přidejte prvek GridView. Z inteligentní značky GridView s vytvořte nový prvek ObjectDataSource. V prvním kroku průvodce s byste měli vidět třídu `ProductsCL` jako jednu z možností z rozevíracího seznamu.

[![třída ProductsCL je obsažena v rozevíracím seznamu obchodních objektů.](caching-data-in-the-architecture-cs/_static/image5.png)](caching-data-in-the-architecture-cs/_static/image4.png)

**Obrázek 4**: třída `ProductsCL` je obsažena v rozevíracím seznamu obchodních objektů ([kliknutím zobrazíte obrázek v plné velikosti](caching-data-in-the-architecture-cs/_static/image6.png)).

Po výběru `ProductsCL`klikněte na další. Rozevírací seznam na kartě vybrat má dvě položky – `GetProducts()` a `GetProductsByCategoryID(categoryID)` a karta aktualizace má jediné `UpdateProduct` přetížení. Vyberte metodu `GetProducts()` z karty vybrat a `UpdateProducts` metodou na kartě aktualizace a klikněte na Dokončit.

[![metody třídy s ProductsCL jsou uvedené v rozevíracích seznamech.](caching-data-in-the-architecture-cs/_static/image8.png)](caching-data-in-the-architecture-cs/_static/image7.png)

**Obrázek 5**: metody třídy `ProductsCL` jsou uvedeny v rozevíracích seznamech ([kliknutím zobrazíte obrázek v plné velikosti](caching-data-in-the-architecture-cs/_static/image9.png)).

Po dokončení průvodce nastaví Visual Studio vlastnost ObjectDataSource `OldValuesParameterFormatString` na `original_{0}` a přidá příslušná pole do prvku GridView. Změňte vlastnost `OldValuesParameterFormatString` zpět na její výchozí hodnotu, `{0}`a nakonfigurujte prvek GridView tak, aby podporoval stránkování, řazení a úpravy. Vzhledem k tomu, že přetížení `UploadProducts` používané v CL přijme pouze upravený název produktu a cenu, omezí prvek GridView tak, aby byla pouze tato pole upravitelná.

V předchozím kurzu jsme definovali prvek GridView, který bude obsahovat pole pro pole `ProductName`, `CategoryName`a `UnitPrice`. Chcete-li replikovat toto formátování a strukturu, v takovém případě by deklarativní označení prvku GridView a ObjectDataSource s mělo vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](caching-data-in-the-architecture-cs/samples/sample11.aspx)]

V tuto chvíli máme stránku, která používá vrstvu ukládání do mezipaměti. Chcete-li zobrazit mezipaměť v akci, nastavte zarážky v `ProductsCL` třídy s `GetProducts()` a metody `UpdateProduct`. Přejděte na stránku v prohlížeči a procházejte kódem při řazení a stránkování, aby se zobrazila data získaná z mezipaměti. Pak aktualizujte záznam a Všimněte si, že mezipaměť je neověřená a v důsledku toho se načte z knihoven BLL při převázání dat na prvek GridView.

> [!NOTE]
> Vrstva ukládání do mezipaměti uvedená v tomto článku ke stažení, která je přiložena k tomuto článku, není dokončena. Obsahuje pouze jednu třídu, `ProductsCL`, která pouze sport několik metody. Kromě toho pouze jedna stránka ASP.NET používá CL (`~/Caching/FromTheArchitecture.aspx`) všichni ostatní, stále na knihoven BLL odkazují přímo. Pokud plánujete použití CL ve vaší aplikaci, všechna volání z prezentační vrstvy by měla přejít na CL, což by vyžadovalo, aby se třídy CL a metody pokryly s těmito třídami a metodami v knihoven BLL aktuálně používané prezentační vrstvou.

## <a name="summary"></a>Souhrn

I když lze ukládání do mezipaměti použít v prezentační vrstvě pomocí ovládacích prvků ASP.NET 2,0 s SqlDataSource a ObjectDataSource, v ideálním případě by se odpovědnosti do mezipaměti přenesly na samostatnou vrstvu v architektuře. V tomto kurzu jsme vytvořili vrstvu ukládání do mezipaměti, která se nachází mezi prezentační vrstvou a vrstvou obchodní logiky. Vrstva ukládání do mezipaměti musí poskytovat stejnou sadu tříd a metod, které existují v knihoven BLL a jsou volány z prezentační vrstvy.

Příklady vrstev do mezipaměti, které jsme prozkoumali a v předchozích kurzech se projeví *reaktivní načítání*. Při reaktivním načítání se data načtou do mezipaměti jenom v případě, že se vytvoří požadavek na data a v mezipaměti chybí data. Data je také možné *aktivně načíst* do mezipaměti, což je technika, která načte data do mezipaměti, než je skutečně potřeba. V dalším kurzu uvidíme příklad proaktivní načítání, když se podíváme na to, jak ukládat statické hodnoty do mezipaměti při spuštění aplikace.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Teresa Murph. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](caching-data-with-the-objectdatasource-cs.md)
> [Další](caching-data-at-application-startup-cs.md)

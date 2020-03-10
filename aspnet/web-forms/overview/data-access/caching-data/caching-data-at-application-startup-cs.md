---
uid: web-forms/overview/data-access/caching-data/caching-data-at-application-startup-cs
title: Ukládání dat do mezipaměti při spuštěníC#aplikace () | Microsoft Docs
author: rick-anderson
description: V jakékoli webové aplikaci se často používají data a některá data se nepoužívají zřídka. Můžeme vylepšit výkon naší aplikace ASP.NET b...
ms.author: riande
ms.date: 05/30/2007
ms.assetid: 22ca8efa-7cd1-45a7-b9ce-ce6eb3b3ff95
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-at-application-startup-cs
msc.type: authoredcontent
ms.openlocfilehash: a0b55b0df1b7843120de284891e16178df23fabe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78576907"
---
# <a name="caching-data-at-application-startup-c"></a>Ukládání dat do mezipaměti při spuštění aplikace (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout PDF](caching-data-at-application-startup-cs/_static/datatutorial60cs1.pdf)

> V jakékoli webové aplikaci se často používají data a některá data se nepoužívají zřídka. Výkon naší aplikace ASP.NET můžeme vylepšit načtením předem používaných dat, technika známá jako ukládání do mezipaměti. V tomto kurzu se dozvíte o jednom z přístupů k proaktivnímu načítání, které slouží k načtení dat do mezipaměti při spuštění aplikace.

## <a name="introduction"></a>Úvod

Dva předchozí kurzy se prohlédly při ukládání dat do mezipaměti v prezentačních a mezipamětních vrstvách. Při [ukládání dat do mezipaměti](caching-data-with-the-objectdatasource-cs.md)v prvku ObjectDataSource jsme se podívali na použití funkcí pro ukládání do mezipaměti prvku ObjectDataSource k ukládání dat do mezipaměti v prezentační vrstvě. [Ukládání dat do mezipaměti v architektuře](caching-data-in-the-architecture-cs.md) v rámci přezkoumané mezipaměti v nové oddělené vrstvě pro ukládání do mezipaměti. Oba tyto kurzy používaly *reaktivní načítání* při práci s datovou mezipamětí. Při reaktivním načítání pokaždé, když se vyžadují data, systém nejdřív zkontroluje, jestli je v mezipaměti. Pokud ne, přičtou data z původního zdroje, jako je databáze, a pak je uloží do mezipaměti. Hlavní výhodou pro reaktivní načítání je jeho snadné implementace. Jednou z jeho nevýhody je nerovnoměrné výkon napříč požadavky. Představte si stránku, která používá vrstvu ukládání do mezipaměti z předchozího kurzu pro zobrazení informací o produktu. Pokud je tato stránka navštívena poprvé nebo navštívena poprvé po vyřazení dat uložených v mezipaměti z důvodu omezení paměti nebo zadaného vypršení platnosti, musí být data načtena z databáze. Proto tyto požadavky uživatelů budou trvat déle než požadavky uživatelů, které může mezipaměť zpracovat.

*Proaktivní načítání* poskytuje alternativní strategii pro správu mezipaměti, která vyhlazuje výkon napříč požadavky načtením dat uložených v mezipaměti, než je budete potřebovat. Proaktivní načítání obvykle používá určitý proces, který buď pravidelně kontroluje, nebo je oznámení, když došlo k aktualizaci podkladových dat. Tento proces pak aktualizuje mezipaměť, aby se zachovala její aktuálnost. Proaktivní načítání je užitečné hlavně v případě, že podkladová data pocházejí z pomalého připojení k databázi, webové služby nebo jiného zdroje dat, zejména pomalá. Ale tento přístup k proaktivnímu načítání je obtížnější implementovat, protože vyžaduje vytváření, správu a nasazování procesu pro kontrolu změn a aktualizaci mezipaměti.

Dalším charakterem proaktivního načítání a typu, který prozkoumáme v tomto kurzu, je načítání dat do mezipaměti při spuštění aplikace. Tento přístup je zvláště užitečný pro ukládání statických dat do mezipaměti, jako jsou záznamy v tabulkách pro vyhledávání databáze.

> [!NOTE]
> Podrobnější přehled o rozdílech mezi aktivním a reaktivním načítáním a také se seznamy doporučení pro odborníky, nevýhody a implementaci najdete v části [Správa obsahu mezipaměti](https://msdn.microsoft.com/library/ms978503.aspx) v [Průvodci architekturou mezipaměti pro aplikace .NET Framework](https://msdn.microsoft.com/library/ms978498.aspx).

## <a name="step-1-determining-what-data-to-cache-at-application-startup"></a>Krok 1: určení dat pro ukládání do mezipaměti při spuštění aplikace

Příklady ukládání do mezipaměti pomocí reaktivního načítání, které jsme prozkoumali v předchozích dvou kurzech, dobře fungují s daty, která se můžou pravidelně měnit a exorbitantly dlouho netrvá. Pokud se ale data uložená v mezipaměti nikdy nezmění, vyprší platnost používaná reaktivním načítáním nadbytečným. Podobně platí, že pokud se data ukládají do mezipaměti delší dobu, bude nutné, aby uživatelé, jejichž požadavky vyhledali mezipaměť prázdné, musely dlouhodobě počkat, dokud se načtou základní data. Zvažte ukládání statických dat a dat, která při spuštění aplikace přebírají výjimečně dlouhou dobu.

I když databáze obsahují mnoho dynamických, často se měnících hodnot, má většina také spravedlivé množství statických dat. Prakticky všechny datové modely mají například jeden nebo více sloupců, které obsahují určitou hodnotu z pevné sady možností. Databázová tabulka `Patients` může mít `PrimaryLanguage` sloupec, jehož sada hodnot by mohla být angličtina, španělština, francouzština, ruština, japonština a tak dále. Často tyto typy sloupců jsou implementovány pomocí *vyhledávacích tabulek*. Místo ukládání řetězcové angličtiny nebo francouzštiny do tabulky `Patients` je vytvořena druhá tabulka, která má obvykle dva sloupce – jedinečný identifikátor a popis řetězce – s záznamem pro každou možnou hodnotu. Sloupec `PrimaryLanguage` v tabulce `Patients` ukládá odpovídající jedinečný identifikátor ve vyhledávací tabulce. Na obrázku 1 je primárním jazykem pacienta Jan Novák, ale Johnsonem je ruština.

![Tabulka jazyky je vyhledávací tabulka, kterou používá tabulka pacientů.](caching-data-at-application-startup-cs/_static/image1.png)

**Obrázek 1**: `Languages` tabulka je vyhledávací tabulka, kterou používá tabulka `Patients`.

Uživatelské rozhraní pro úpravy nebo vytvoření nového pacienta by zahrnovalo rozevírací seznam povolených jazyků vyplněný záznamy v `Languages` tabulce. Bez ukládání do mezipaměti, při každém navštívení tohoto rozhraní systém musí zadat dotaz na `Languages` tabulku. To je wasteful a zbytečné, protože se hodnoty vyhledávací tabulky velmi nečasto mění, pokud je to dřív.

Data `Languages` můžeme ukládat do mezipaměti pomocí stejných technik reaktivního načítání, které jsou zkoumány v předchozích kurzech. Opětovné aktivní načítání ale používá vypršení platnosti založené na čase, které není nutné pro data statické vyhledávací tabulky. I když je ukládání do mezipaměti pomocí reaktivního načítání lepší než ukládání do mezipaměti, nejlepším řešením je proaktivně načíst data vyhledávací tabulky do mezipaměti při spuštění aplikace.

V tomto kurzu se podíváme na to, jak ukládat data vyhledávací tabulky do mezipaměti a dalších statických informací.

## <a name="step-2-examining-the-different-ways-to-cache-data"></a>Krok 2: prozkoumání různých způsobů ukládání dat do mezipaměti

Informace mohou být programově uloženy v mezipaměti aplikace ASP.NET pomocí různých přístupů. V předchozích kurzech jsme už viděli, jak používat mezipaměť dat. Alternativně lze objekty programově ukládat do mezipaměti pomocí *statických členů* nebo *stavu aplikace*.

Při práci s třídou musí být obvykle nejprve vytvořena instance před tím, než je možné k nim přistupovat její členové. Chcete-li například vyvolat metodu z jedné ze tříd v naší vrstvě obchodní logiky, je nutné nejprve vytvořit instanci třídy:

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample1.cs)]

Předtím, než můžeme vyvolat *SomeMethod* nebo pracovat s *SomeProperty*, je nutné nejprve vytvořit instanci třídy pomocí klíčového slova `new`. *SomeMethod* a *SomeProperty* jsou spojeny s konkrétní instancí. Životnost těchto členů je svázána s životností jejich přidruženého objektu. *Statické členy*na druhé straně jsou proměnné, vlastnosti a metody, které jsou sdíleny mezi *všemi* instancemi třídy, a v důsledku toho mají životnost, pokud je třída. Statické členy jsou označeny klíčovým slovem `static`.

Kromě statických členů lze data ukládat do mezipaměti pomocí stavu aplikace. Každá aplikace ASP.NET udržuje kolekci název/hodnota, která je sdílena napříč všemi uživateli a stránkami aplikace. Tato kolekce je k dispozici pomocí [vlastnosti`Application`](https://msdn.microsoft.com/library/system.web.httpcontext.application.aspx) [třídy`HttpContext`](https://msdn.microsoft.com/library/system.web.httpcontext.aspx)a používá se ve třídě kódu na pozadí stránky ASP.NET, například:

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample2.cs)]

Mezipaměť dat poskytuje mnohem rozsáhlejší rozhraní API pro ukládání dat do mezipaměti, poskytování mechanismů pro vypršení platnosti a časově omezené závislosti na základě časových limitů, priorit položek mezipaměti a tak dále. U statických členů a stavu aplikace musí být takové funkce přidány ručně vývojářem stránky. Při ukládání dat do mezipaměti při spuštění aplikace po dobu života aplikace se ale výhody datové mezipaměti moot. V tomto kurzu se podíváme na kód, který používá všechny tři techniky pro ukládání statických dat do mezipaměti.

## <a name="step-3-caching-thesupplierstable-data"></a>Krok 3: ukládání dat`Suppliers`tabulky do mezipaměti

Tabulky databáze Northwind, které jsme v tomto datu implementovali, neobsahují žádné tradiční vyhledávací tabulky. Čtyři tabulky DataTables implementované v naší úrovni DAL všechny tabulky modelů, jejichž hodnoty nejsou statické. Místo toho, aby bylo možné přidat nový objekt DataTable k objektu DAL a následně novou třídu a metody do knihoven BLL, vám pro tento kurz stačí předstírat, že data `Suppliers` tabulky jsou statická. Proto můžeme tato data ukládat do mezipaměti při spuštění aplikace.

Začněte tím, že ve `CL` složce vytvoříte novou třídu s názvem `StaticCache.cs`.

![Vytvoření třídy StaticCache.cs ve složce CL](caching-data-at-application-startup-cs/_static/image2.png)

**Obrázek 2**: vytvoření třídy `StaticCache.cs` ve složce `CL`

Musíme přidat metodu, která načte data při spuštění do příslušného úložiště mezipaměti, a také metody, které vracejí data z této mezipaměti.

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample3.cs)]

Výše uvedený kód používá statickou členskou proměnnou `suppliers`pro uchování výsledků z metody `GetSuppliers()` `SuppliersBLL` třídy, která je volána z metody `LoadStaticCache()`. Metoda `LoadStaticCache()` je určena pro volání během spuštění aplikace. Jakmile budou tato data načtena při spuštění aplikace, jakákoliv stránka, která potřebuje pracovat s daty dodavatele, může volat metodu `GetSuppliers()` `StaticCache` třídy. Proto volání databáze k získání dodavatelů proběhne pouze jednou, při spuštění aplikace.

Místo toho, abyste jako úložiště mezipaměti použili statickou členskou proměnnou, můžeme použít taky stav aplikace nebo mezipaměť dat. Následující kód ukazuje třídu, která je předaná, aby používala stav aplikace:

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample4.cs)]

V `LoadStaticCache()`jsou informace o dodavatelích uloženy do *klíče*proměnné aplikace. Vrátí se jako příslušný typ (`Northwind.SuppliersDataTable`) z `GetSuppliers()`. I když je stav aplikace k dispozici v třídách kódu na pozadí stránek ASP.NET pomocí `Application["key"]`, musí být v architektuře pro získání aktuálního `HttpContext`použita `HttpContext.Current.Application["key"]`.

Podobně lze mezipaměť dat použít jako úložiště mezipaměti, jak ukazuje následující kód:

[!code-csharp[Main](caching-data-at-application-startup-cs/samples/sample5.cs)]

Chcete-li přidat položku do mezipaměti dat bez vypršení platnosti založené na čase, použijte hodnoty `System.Web.Caching.Cache.NoAbsoluteExpiration` a `System.Web.Caching.Cache.NoSlidingExpiration` jako vstupní parametry. Toto konkrétní přetížení metody `Insert` datové mezipaměti bylo vybráno, aby bylo možné zadat *prioritu* položky mezipaměti. Priorita se používá k určení položek, které se mají uklidit z mezipaměti, když dojde k nízké velikosti dostupné paměti. Tady používáme prioritní `NotRemovable`, která zajišťuje, že se tato položka mezipaměti nebude uklidit.

> [!NOTE]
> Stažení tohoto kurzu implementuje třídu `StaticCache` s použitím přístupu ke statické členské proměnné. Kód pro techniky stavu aplikace a mezipaměti dat je k dispozici v komentářích v souboru třídy.

## <a name="step-4-executing-code-at-application-startup"></a>Krok 4: spouštění kódu při spuštění aplikace

Aby bylo možné spustit kód při prvním spuštění webové aplikace, musíme vytvořit speciální soubor s názvem `Global.asax`. Tento soubor může obsahovat obslužné rutiny událostí pro události aplikace, relace a na úrovni požadavku a je tady, kde můžeme přidat kód, který se spustí při každém spuštění aplikace.

Přidejte soubor `Global.asax` do kořenového adresáře webové aplikace tak, že kliknete pravým tlačítkem na název projektu webu v Průzkumník řešení sady Visual Studio a zvolíte možnost Přidat novou položku. V dialogovém okně Přidat novou položku vyberte typ položky globální třída aplikace a pak klikněte na tlačítko Přidat.

> [!NOTE]
> Pokud již máte soubor `Global.asax` ve vašem projektu, typ položky globální třídy aplikace nebude uveden v dialogovém okně Přidat novou položku.

[![přidat soubor Global. asax do kořenového adresáře vaší webové aplikace](caching-data-at-application-startup-cs/_static/image4.png)](caching-data-at-application-startup-cs/_static/image3.png)

**Obrázek 3**: přidejte soubor `Global.asax` do kořenového adresáře webové aplikace ([kliknutím zobrazíte obrázek v plné velikosti).](caching-data-at-application-startup-cs/_static/image5.png)

Výchozí šablona souboru `Global.asax` obsahuje pět metod v rámci značky `<script>` na straně serveru:

- **`Application_Start`** se spustí při prvním spuštění webové aplikace
- **`Application_End`** se spustí, když se aplikace vypíná.
- **`Application_Error`** se spustí pokaždé, když Neošetřená výjimka dosáhne aplikace.
- **`Session_Start`** se spustí při vytvoření nové relace.
- **`Session_End`** se spustí, když vypršela platnost relace.

Obslužná rutina události `Application_Start` se během životního cyklu aplikace volá jenom jednou. Aplikace se spustí při prvním vyžádání prostředku ASP.NET z aplikace a pokračuje v jeho spuštění, dokud se aplikace nerestartuje, což může nastat úpravou obsahu složky `/Bin`, úpravou `Global.asax`, úpravou obsahu ve složce `App_Code` nebo úpravou souboru `Web.config` mimo jiné příčiny. Podrobnější diskuzi o životním cyklu aplikace najdete v tématu [Přehled životního cyklu aplikací ASP.NET](https://msdn.microsoft.com/library/ms178473.aspx) .

V těchto kurzech potřebujeme přidat kód do metody `Application_Start`, takže nemusíte ostatní odebrat. V `Application_Start`jednoduše zavolejte metodu `LoadStaticCache()` `StaticCache` třídy, která načte a uloží do mezipaměti informace o dodavateli:

[!code-aspx[Main](caching-data-at-application-startup-cs/samples/sample6.aspx)]

A je to! Při spuštění aplikace `LoadStaticCache()` metoda předává informace o dodavateli z knihoven BLL a uloží ji do statické členské proměnné (nebo jakéhokoli úložiště mezipaměti, které jste při použití ve třídě `StaticCache` vyukončili.). Chcete-li toto chování ověřit, nastavte zarážku v metodě `Application_Start` a spusťte aplikaci. Všimněte si, že zarážka je dosaženo na začátku aplikace. Následné požadavky však nezpůsobí spuštění metody `Application_Start`.

[![použít zarážku k ověření, zda je prováděna obslužná rutina události Application_Start](caching-data-at-application-startup-cs/_static/image7.png)](caching-data-at-application-startup-cs/_static/image6.png)

**Obrázek 4**: pomocí zarážky ověřte, zda je spuštěna obslužná rutina události `Application_Start` ([kliknutím zobrazíte obrázek v plné velikosti).](caching-data-at-application-startup-cs/_static/image8.png)

> [!NOTE]
> Pokud při prvním spuštění ladění nebudete mít `Application_Start` zarážku, je to proto, že vaše aplikace už je spuštěná. Vynuťte restartování aplikace úpravou `Global.asax` nebo `Web.config` souborů a potom akci opakujte. K rychlému restartování aplikace můžete jednoduše přidat (nebo odebrat) prázdný řádek na konci jednoho z těchto souborů.

## <a name="step-5-displaying-the-cached-data"></a>Krok 5: zobrazení dat uložených v mezipaměti

V tomto okamžiku má třída `StaticCache` verzi dat dodavatele v mezipaměti při spuštění aplikace, ke kterému je možné přistupovat prostřednictvím její `GetSuppliers()` metody. Pro práci s těmito daty z prezentační vrstvy můžeme použít prvek ObjectDataSource nebo programově vyvolat `GetSuppliers()` metodu `StaticCache` třídy z třídy kódu na pozadí stránky ASP.NET. Pojďme se podívat na použití ovládacích prvků ObjectDataSource a GridView k zobrazení informací o dodavateli v mezipaměti.

Začněte tím, že otevřete stránku `AtApplicationStartup.aspx` ve složce `Caching`. Přetáhněte prvek GridView z panelu nástrojů do návrháře, nastavením jeho vlastnosti `ID` na hodnotu `Suppliers`. Dále můžete z inteligentní značky prvku GridView vytvořit nový prvek ObjectDataSource s názvem `SuppliersCachedDataSource`. Nakonfigurujte prvek ObjectDataSource tak, aby používal metodu `GetSuppliers()` `StaticCache` třídy.

[![nakonfigurovat prvek ObjectDataSource tak, aby používal třídu StaticCache](caching-data-at-application-startup-cs/_static/image10.png)](caching-data-at-application-startup-cs/_static/image9.png)

**Obrázek 5**: Konfigurace prvku ObjectDataSource, aby používal třídu `StaticCache` ([kliknutím zobrazíte obrázek v plné velikosti](caching-data-at-application-startup-cs/_static/image11.png))

[![pomocí metody getsuppliers () načíst data dodavatele v mezipaměti](caching-data-at-application-startup-cs/_static/image13.png)](caching-data-at-application-startup-cs/_static/image12.png)

**Obrázek 6**: použití metody `GetSuppliers()` k načtení dat dodavatele uložených v mezipaměti ([kliknutím zobrazíte obrázek v plné velikosti](caching-data-at-application-startup-cs/_static/image14.png))

Po dokončení průvodce bude Visual Studio automaticky přidávat BoundFields pro každé datové pole v `SuppliersDataTable`. Deklarativní značky GridView a ObjectDataSource by měly vypadat podobně jako následující:

[!code-aspx[Main](caching-data-at-application-startup-cs/samples/sample7.aspx)]

Obrázek 7 zobrazuje stránku při prohlížení v prohlížeči. Výstup je stejný, ale data byla získána z `SuppliersBLL` třídy knihoven BLL, ale použití třídy `StaticCache` vrátí data dodavatelů jako mezipaměť při spuštění aplikace. Můžete nastavit zarážky v metodě `GetSuppliers()` `StaticCache` třídy, chcete-li toto chování ověřit.

[![data dodavatele v mezipaměti se zobrazí v prvku GridView.](caching-data-at-application-startup-cs/_static/image16.png)](caching-data-at-application-startup-cs/_static/image15.png)

**Obrázek 7**: v prvku GridView se zobrazí data dodavatele uložená v mezipaměti ([kliknutím zobrazíte obrázek v plné velikosti](caching-data-at-application-startup-cs/_static/image17.png)).

## <a name="summary"></a>Souhrn

Většina datových modelů obsahuje korektní množství statických dat, která jsou obvykle implementována ve formě vyhledávacích tabulek. Vzhledem k tomu, že jsou tyto informace statické, neexistuje žádný důvod k nepřetržitému přístupu k databázi pokaždé, když se tyto informace musí zobrazit. Kromě toho, vzhledem ke své statické podstatě, při ukládání dat do mezipaměti není nutné, aby vypršela platnost. V tomto kurzu jsme viděli, jak provést taková data a uložit je do mezipaměti v datové mezipaměti, stavu aplikace a prostřednictvím statické členské proměnné. Tyto informace jsou ukládány do mezipaměti při spuštění aplikace a zůstávají v mezipaměti v průběhu životního cyklu aplikace.

V tomto kurzu a minulých dvou jsme se vyhledali při ukládání dat do mezipaměti po dobu životnosti aplikace a také při použití vypršení platnosti. Při ukládání databázových dat do mezipaměti může i vypršení časového limitu trvat méně, než je ideální. Místo pravidelného vyprázdnění mezipaměti by bylo optimální vyřadit položku z mezipaměti pouze v případě, že jsou upravena podkladová data databáze. Ideální možností je použití závislostí mezipaměti SQL, které probereme v našem dalším kurzu.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Teresa Murphy a Zack Novotný. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](caching-data-in-the-architecture-cs.md)
> [Další](using-sql-cache-dependencies-cs.md)

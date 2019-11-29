---
uid: web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-cs
title: Ukládání dat do mezipaměti v prvkuC#ObjectDataSource () | Microsoft Docs
author: rick-anderson
description: Ukládání do mezipaměti může znamenat rozdíl mezi pomalým a rychlou webovou aplikací. Tento kurz je první ze čtyř, které se podrobněji podíváte na ukládání do mezipaměti v ASP.NET...
ms.author: riande
ms.date: 05/30/2007
ms.assetid: bd87413c-8160-4520-a8a2-43b555c4183a
msc.legacyurl: /web-forms/overview/data-access/caching-data/caching-data-with-the-objectdatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: c9883314d6153b9816d9bad2a281ab3c0a816448
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74612410"
---
# <a name="caching-data-with-the-objectdatasource-c"></a>Ukládání dat do mezipaměti ovládacím prvkem ObjectDataSource (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_58_CS.exe) nebo [Stáhnout PDF](caching-data-with-the-objectdatasource-cs/_static/datatutorial58cs1.pdf)

> Ukládání do mezipaměti může znamenat rozdíl mezi pomalým a rychlou webovou aplikací. Tento kurz je první ze čtyř, které se podrobněji podíváte na ukládání do mezipaměti v ASP.NET. Seznamte se s klíčovými koncepty ukládání do mezipaměti a postupem, jak používat ukládání do mezipaměti do prezentační vrstvy prostřednictvím ovládacího prvku ObjectDataSource.

## <a name="introduction"></a>Úvod

V počítačové vědy je *ukládání do mezipaměti* náročné na data nebo informace, které jsou nákladné pro získání a uložení kopie IT v umístění, ve kterém je rychlejší přístup. Pro aplikace řízené daty velké a složité dotazy běžně využívají většinu doby spuštění aplikace. Výkon aplikace se pak dá často zlepšit tím, že se výsledky nákladných databázových dotazů ukládají do paměti aplikace.

ASP.NET 2,0 nabízí celou řadu možností ukládání do mezipaměti. Pomocí *ukládání výstupu do mezipaměti*lze uložit celou webovou stránku nebo uživatelský ovládací prvek s vykreslenými značkami. Ovládací prvky ObjectDataSource a SqlDataSource poskytují také možnosti ukládání do mezipaměti, což umožňuje ukládat data do mezipaměti na úrovni ovládacího prvku. A ASP.NET s *data cache* poskytuje BOHATÝCH rozhraní API pro ukládání do mezipaměti, které umožňuje vývojářům stránek programově ukládat objekty do mezipaměti. V tomto kurzu a dalších třech prověříme použití funkcí pro ukládání do mezipaměti ObjectDataSource s a také do mezipaměti dat. Také si probereme, jak ukládat data v rámci aplikace do mezipaměti při spuštění a jak zajistit aktuálnost dat v mezipaměti pomocí závislostí mezipaměti SQL. Tyto kurzy nezkoumá ukládání výstupu do mezipaměti. Podrobný pohled na výstup do mezipaměti najdete v tématu [ukládání výstupu do mezipaměti v ASP.NET 2,0](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx).

Ukládání do mezipaměti je možné v rámci architektury použít na jakémkoli místě, od vrstvy přístupu k datům až po prezentační vrstvu. V tomto kurzu se podíváme na použití ukládání do mezipaměti do prezentační vrstvy prostřednictvím ovládacího prvku ObjectDataSource. V dalším kurzu prověříme ukládání dat do mezipaměti do vrstvy obchodní logiky.

## <a name="key-caching-concepts"></a>Koncepty ukládání klíčů do mezipaměti

Ukládání do mezipaměti může výrazně zlepšit celkový výkon a škálovatelnost aplikace tím, že vybírá data, která jsou náročná na generování a ukládání kopie IT, do umístění, ke kterému se dá efektivněji připínat. Vzhledem k tomu, že mezipaměť obsahuje pouze kopii skutečných, podkladových dat, může být zastaralá nebo *zastaralá*, pokud se změní podkladová data. Pro boj proti tomu může vývojář stránky určit kritéria, podle kterých bude položka mezipaměti z mezipaměti *vyřazena* , a to pomocí:

- **Kritéria založené na čase** : položka může být přidána do mezipaměti pro absolutní nebo posuvnou dobu trvání. Například vývojář stránky může indikovat dobu trvání, například 60 sekund. Po absolutní době se položka uložená v mezipaměti vyřadí 60 sekund po přidání do mezipaměti, bez ohledu na to, jak často k nim došlo. Po klouzavé době je položka uložená v mezipaměti vyřazena 60 sekund po posledním přístupu.
- **Kritéria založená na závislostech** : při přidání do mezipaměti může být k položce přidružena závislost. Pokud se závislost položky změní, je vyřazena z mezipaměti. Závislost může být soubor, jiná položka v mezipaměti nebo kombinace těchto dvou. ASP.NET 2,0 také umožňuje závislosti mezipaměti SQL, které vývojářům umožňují přidat položku do mezipaměti a nechat ji vyřadit, když se změní podkladová data databáze. Závislosti mezipaměti SQL prověříme v kurzu [použití závislostí mezipaměti SQL](using-sql-cache-dependencies-cs.md) .

Bez ohledu na zadané kritérium vyřazení může být položka v mezipaměti *uklizena* předtím, než byla splněna kritéria založená na čase nebo závislosti. Pokud mezipaměť dosáhla své kapacity, je nutné odebrat existující položky, aby bylo možné přidat nové. V důsledku toho při práci s daty uloženými v mezipaměti je důležité, abyste vždycky předpokládali, že data uložená v mezipaměti nemusí být k dispozici. Podíváme se na vzor, který se použije při přístupu k datům z mezipaměti programově v našem dalším kurzu, který ukládá *data do mezipaměti v architektuře*.

Ukládání do mezipaměti poskytuje ekonomické prostředky pro zlepšení výkonu aplikace. Jako [Steven Smith](http://aspadvice.com/blogs/ssmith/) klouby ve svém článku [ukládání do mezipaměti ASP.NET: techniky a osvědčené postupy](https://msdn.microsoft.com/library/aa478965.aspx):

Ukládání do mezipaměti může být dobrým způsobem, jak dosáhnout dostatečného výkonu, aniž by bylo potřeba provádět spoustu času a analýzy. Paměť je levné, takže pokud můžete získat potřebný výkon uložením výstupu do mezipaměti po dobu 30 sekund, nikoli za den nebo týden, kde se snažíte optimalizovat váš kód nebo databázi, udělejte řešení ukládání do mezipaměti (za předpokladu, že staré údaje 30 sekund jsou ok) a přesun na. Nekvalitní návrh bude pravděpodobně třeba zachytit, takže samozřejmě byste se měli pokusit aplikace navrhovat správně. Pokud ale budete potřebovat dobrý výkon ještě dnes, ukládání do mezipaměti může být skvělým [přístupem] a koupit si čas k refaktorování aplikace v pozdější době, kdy k tomu budete mít čas.

I když ukládání do mezipaměti může poskytovat výrazné zvýšení výkonu, není použitelné ve všech situacích, jako je třeba u aplikací, které používají často aktualizovaná data v reálném čase, nebo v případech, kdy se zastaralá data nepřijala v krátké době. U většiny aplikací je však vhodné použít ukládání do mezipaměti. Další informace o ukládání do mezipaměti v ASP.NET 2,0 najdete v části [ukládání do mezipaměti pro výkon](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/default.aspx) v [kurzech pro rychlé zprovoznění ASP.NET 2,0](https://quickstarts.asp.net/QuickStartv20/aspnet/).

## <a name="step-1-creating-the-caching-web-pages"></a>Krok 1: vytvoření webových stránek pro ukládání do mezipaměti

Před zahájením průzkumu funkcí pro ukládání do mezipaměti ObjectDataSource s a pojďme nejdřív chvíli trvat, než se vytvoří stránky ASP.NET v našem projektu webu, který budeme potřebovat pro tento kurz a další tři. Začněte přidáním nové složky s názvem `Caching`. Dále přidejte následující stránky ASP.NET do této složky a nezapomeňte přidružit jednotlivé stránky k `Site.master` hlavní stránce:

- `Default.aspx`
- `ObjectDataSource.aspx`
- `FromTheArchitecture.aspx`
- `AtApplicationStartup.aspx`
- `SqlCacheDependencies.aspx`

![Přidání stránek ASP.NET pro kurzy související s ukládáním do mezipaměti](caching-data-with-the-objectdatasource-cs/_static/image1.png)

**Obrázek 1**: přidání stránek ASP.NET pro kurzy související s ukládáním do mezipaměti

Podobně jako v ostatních složkách `Default.aspx` ve složce `Caching` vypíše kurzy v části. Zajistěte, aby tato funkce poskytovala `SectionLevelTutorialListing.ascx` uživatelský ovládací prvek. Proto tento uživatelský ovládací prvek přidejte do `Default.aspx` tím, že ho přetáhnete z Průzkumník řešení na zobrazení Návrh stránky.

[![obrázek 2: Přidání uživatelského ovládacího prvku SectionLevelTutorialListing. ascx do default. aspx](caching-data-with-the-objectdatasource-cs/_static/image3.png)](caching-data-with-the-objectdatasource-cs/_static/image2.png)

**Obrázek 2**: obrázek 2: Přidání uživatelského ovládacího prvku `SectionLevelTutorialListing.ascx` do `Default.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](caching-data-with-the-objectdatasource-cs/_static/image4.png))

Nakonec tyto stránky přidejte jako položky do souboru `Web.sitemap`. Konkrétně přidejte následující kód po práci s binárními daty `<siteMapNode>`:

[!code-xml[Main](caching-data-with-the-objectdatasource-cs/samples/sample1.xml)]

Po aktualizaci `Web.sitemap`chvíli počkejte, než se zobrazí web kurzy prostřednictvím prohlížeče. V nabídce na levé straně teď najdete položky kurzů pro ukládání do mezipaměti.

![Mapa webu teď obsahuje položky kurzů pro ukládání do mezipaměti.](caching-data-with-the-objectdatasource-cs/_static/image5.png)

**Obrázek 3**: Mapa webu teď obsahuje položky kurzů pro ukládání do mezipaměti.

## <a name="step-2-displaying-a-list-of-products-in-a-web-page"></a>Krok 2: zobrazení seznamu produktů na webové stránce

V tomto kurzu se seznámíte s použitím integrovaných funkcí ukládání do mezipaměti v rámci ovládacího prvku ObjectDataSource. Předtím, než se můžeme podívat na tyto funkce, musíme nejdřív potřebovat stránku, ze které můžete pracovat. Umožňuje vytvořit webovou stránku, která používá prvek GridView k vypsání informací o produktu načtených prvkem ObjectDataSource z třídy `ProductsBLL`.

Začněte tím, že otevřete stránku `ObjectDataSource.aspx` ve složce `Caching`. Přetáhněte prvek GridView z panelu nástrojů do návrháře, nastavte jeho vlastnost `ID` na `Products`a z jeho inteligentní značky vyberte možnost svázání s novým ovládacím prvkem ObjectDataSource s názvem `ProductsDataSource`. Nakonfigurujte prvek ObjectDataSource pro práci s třídou `ProductsBLL`.

[![nakonfigurovat prvek ObjectDataSource tak, aby používal třídu ProductsBLL](caching-data-with-the-objectdatasource-cs/_static/image7.png)](caching-data-with-the-objectdatasource-cs/_static/image6.png)

**Obrázek 4**: Konfigurace prvku ObjectDataSource, aby používal třídu `ProductsBLL` ([kliknutím zobrazíte obrázek v plné velikosti](caching-data-with-the-objectdatasource-cs/_static/image8.png))

Pro tuto stránku vytvoříme upravitelný prvek GridView, abyste mohli prošetřit, co se stane, když se data uložená v ovládacím prvku ObjectDataSource upraví prostřednictvím rozhraní GridView s. Nechejte rozevírací seznam na kartě vybrat nastavený na výchozí `GetProducts()`, ale změňte vybranou položku na kartě aktualizace na `UpdateProduct` přetížení, které přijímá `productName`, `unitPrice`a `productID` jako vstupní parametry.

[![v rozevíracím seznamu karta aktualizace nastavit odpovídající přetížení UpdateProduct](caching-data-with-the-objectdatasource-cs/_static/image10.png)](caching-data-with-the-objectdatasource-cs/_static/image9.png)

**Obrázek 5**: rozevírací seznam karty aktualizace nastavte na odpovídající `UpdateProduct` přetížení ([kliknutím zobrazíte obrázek v plné velikosti).](caching-data-with-the-objectdatasource-cs/_static/image11.png)

Nakonec nastavte rozevírací seznamy na kartách vložit a odstranit na (žádné) a klikněte na Dokončit. Po dokončení Průvodce konfigurací zdroje dat sada Visual Studio nastaví vlastnost ObjectDataSource s `OldValuesParameterFormatString` na `original_{0}`. Jak je popsáno v kurzu [vložení, aktualizace a odstranění dat](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md) , je nutné tuto vlastnost odebrat z deklarativní syntaxe nebo nastavit zpět na výchozí hodnotu, `{0}`, aby mohl náš pracovní postup aktualizace pokračovat bez chyby.

Kromě toho, po dokončení průvodce, Visual Studio přidá pole do prvku GridView pro každé pole dat produktu. Odeberte všechny kromě `ProductName`, `CategoryName`a `UnitPrice` BoundFields. Dále aktualizujte `HeaderText` vlastnosti každého z těchto BoundFields na produkt, kategorii a cenu. Vzhledem k tomu, že je vyžadováno pole `ProductName`, převeďte vlastnost BoundField na TemplateField a přidejte RequiredFieldValidator do `EditItemTemplate`. Podobně převeďte `UnitPrice` vlastnost BoundField na TemplateField a přidejte CompareValidator, abyste zajistili, že hodnota zadaná uživatelem je platná hodnota měny, která je větší nebo rovna nule. Kromě těchto úprav si klidně provedete všechny estetické změny, jako je například zarovnání doprava `UnitPrice` hodnoty, nebo určení formátování `UnitPrice`ho textu v rozhraních jen pro čtení a úpravách.

Nastavte upravitelný prvek GridView zaškrtnutím políčka Povolit úpravy v inteligentní značce GridView. Zaškrtněte také políčka Povolit stránkování a Povolit řazení.

> [!NOTE]
> Potřebujete zkontrolovat, jak přizpůsobit rozhraní pro úpravy prvku GridView s? Pokud ano, přečtěte si kurz [přizpůsobení rozhraní pro úpravu dat](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) .

[![povolit podporu prvku GridView pro úpravy, řazení a stránkování](caching-data-with-the-objectdatasource-cs/_static/image13.png)](caching-data-with-the-objectdatasource-cs/_static/image12.png)

**Obrázek 6**: povolení podpory prvku GridView pro úpravy, řazení a stránkování ([kliknutím zobrazíte obrázek v plné velikosti](caching-data-with-the-objectdatasource-cs/_static/image14.png))

Po provedení úprav těchto prvků GridView by deklarativní označení GridView a ObjectDataSource s mělo vypadat podobně jako následující:

[!code-aspx[Main](caching-data-with-the-objectdatasource-cs/samples/sample2.aspx)]

Jak ukazuje obrázek 7, upravitelný GridView zobrazí název, kategorii a cenu každého z produktů v databázi. Chvíli počkejte, než otestujete funkčnost stránky a seřaďte výsledky, stránky a upravte záznam.

[![každý název produktu, kategorie a cena se zobrazí ve stejném, upravitelném, upravitelném prvku GridView.](caching-data-with-the-objectdatasource-cs/_static/image16.png)](caching-data-with-the-objectdatasource-cs/_static/image15.png)

**Obrázek 7**: každý název produktu, kategorie a cena jsou uvedené ve stejném, upravitelném, upravitelném prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](caching-data-with-the-objectdatasource-cs/_static/image17.png)).

## <a name="step-3-examining-when-the-objectdatasource-is-requesting-data"></a>Krok 3: prozkoumání, kdy prvek ObjectDataSource požaduje data

`Products` GridView načte svá data pro zobrazení vyvoláním metody `Select` prvku `ProductsDataSource` ObjectDataSource. Tento prvek ObjectDataSource vytvoří instanci třídy Business Logic Layer s `ProductsBLL` a zavolá jeho metodu `GetProducts()`, která zase zavolá metodu `GetProducts()` Data Access Layer s `ProductsTableAdapter` s. Metoda DAL se připojí k databázi Northwind a vydá nakonfigurovaný dotaz `SELECT`. Tato data se pak vrátí na DAL, který je zabalí do `NorthwindDataTable`. Objekt DataTable je vrácen do knihoven BLL, který jej vrátí do prvku ObjectDataSource, který jej vrátí do prvku GridView. Prvek GridView potom vytvoří objekt `GridViewRow` pro každý `DataRow` v objektu DataTable a každý `GridViewRow` se nakonec vykreslí do kódu HTML vráceného klientovi a zobrazí se v prohlížeči návštěvníka.

Tato posloupnost událostí probíhá každý a pokaždé, když prvek GridView musí vytvořit vazby na podkladová data. K tomu dojde při prvním navštívení stránky, při přesunu z jedné stránky dat do druhé při řazení prvku GridView nebo při úpravě dat GridView s pomocí vestavěných úprav nebo odstranění rozhraní. Je-li stav zobrazení GridView. je zakázán, bude prvek GridView také při každém zpětném odeslání svázán. Prvek GridView lze také explicitně převázat na jeho data voláním jeho `DataBind()` metody.

Aby bylo možné plně vyhodnotit četnost, s jakou jsou data načítána z databáze, zobrazí se zpráva s oznámením, že se data znovu načítají. Přidejte ovládací prvek popisek webu nad prvek GridView s názvem `ODSEvents`. Vymažte vlastnost `Text` a nastavte její vlastnost `EnableViewState` na `false`. Pod popiskem přidejte webový ovládací prvek tlačítko a nastavte jeho vlastnost `Text` na postback.

[![přidání popisku a tlačítka na stránku nad ovládací prvek GridView](caching-data-with-the-objectdatasource-cs/_static/image19.png)](caching-data-with-the-objectdatasource-cs/_static/image18.png)

**Obrázek 8**: Přidání popisku a tlačítka na stránku nad prvek GridView ([kliknutím zobrazíte obrázek v plné velikosti](caching-data-with-the-objectdatasource-cs/_static/image20.png))

Během pracovního postupu přístupu k datům se v prvku ObjectDataSource s `Selecting` událost aktivuje před vytvořením podkladového objektu a vyvoláním jeho nakonfigurované metody. Vytvořte obslužnou rutinu události pro tuto událost a přidejte následující kód:

[!code-csharp[Main](caching-data-with-the-objectdatasource-cs/samples/sample3.cs)]

Pokaždé, když prvek ObjectDataSource vytvoří požadavek na architekturu dat, zobrazí se v popisku text, který vybral událost.

Navštivte tuto stránku v prohlížeči. Při prvním navštívení stránky se zobrazí text výběr události. Klikněte na tlačítko pro odeslání a Všimněte si, že text zmizí (za předpokladu, že vlastnost GridView `EnableViewState` je nastavena na hodnotu `true`, výchozí). Důvodem je, že při postbacku je prvek GridView znovu sestaven z jeho stavu zobrazení, a proto neměňte prvek ObjectDataSource pro jeho data. Řazení, stránkování nebo upravování dat ale způsobí, že se prvek GridView znovu připojí ke zdroji dat, a proto se text vypálené události vygeneruje znovu.

[![pokaždé, když je prvek GridView svázán s jeho zdrojem dat, zobrazí se výběr aktivované události.](caching-data-with-the-objectdatasource-cs/_static/image22.png)](caching-data-with-the-objectdatasource-cs/_static/image21.png)

**Obrázek 9**: pokaždé, když je prvek GridView svázán s jeho zdrojem dat, je zobrazena událost vyvolaná události ([kliknutím zobrazíte obrázek v plné velikosti).](caching-data-with-the-objectdatasource-cs/_static/image23.png)

[![kliknutí na tlačítko pro odeslání způsobí, že prvek GridView bude znovu vytvořen z jeho stavu zobrazení.](caching-data-with-the-objectdatasource-cs/_static/image25.png)](caching-data-with-the-objectdatasource-cs/_static/image24.png)

**Obrázek 10**: kliknutím na tlačítko pro odeslání dojde k rekonstrukci prvku GridView ze stavu zobrazení ([kliknutím zobrazíte obrázek v plné velikosti](caching-data-with-the-objectdatasource-cs/_static/image26.png)).

Může se zdát, že wasteful načíst data databáze pokaždé, když jsou data stránkovaná nebo seřazená. Po všech případech, vzhledem k opakovanému použití výchozího stránkování, prvek ObjectDataSource načetl všechny záznamy při zobrazení první stránky. I v případě, že prvek GridView neposkytuje podporu řazení a stránkování, data musí být načítána z databáze pokaždé, když je stránka poprvé navštívena jakýmkoli uživatelem (a při každém postbacku, pokud je stav zobrazení zakázán). Pokud však prvek GridView zobrazuje stejná data pro všechny uživatele, tyto dodatečné žádosti o databázi jsou nadbytečné. Proč Neukládat do mezipaměti výsledky vrácené z metody `GetProducts()` a navážete prvek GridView na tyto výsledky v mezipaměti?

## <a name="step-4-caching-the-data-using-the-objectdatasource"></a>Krok 4: ukládání dat do mezipaměti pomocí prvku ObjectDataSource

Pouhým nastavením několika vlastností lze prvek ObjectDataSource nakonfigurovat tak, aby automaticky do mezipaměti načetl data v mezipaměti ASP.NET data. Následující seznam shrnuje vlastnosti prvku ObjectDataSource související s mezipamětí:

- Aby bylo možné povolit ukládání do mezipaměti, musí být [EnableCaching](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.enablecaching.aspx) nastavené na `true`. Výchozí hodnota je `false`.
- [CacheDuration](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cacheduration.aspx) velikost času v sekundách, po kterou jsou data uložena do mezipaměti. Výchozí hodnota je 0. Prvek ObjectDataSource bude ukládat data do mezipaměti pouze v případě, že je `EnableCaching` `true` a `CacheDuration` je nastavena na hodnotu větší než nula.
- [CacheExpirationPolicy](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cacheexpirationpolicy.aspx) může být nastavená na `Absolute` nebo `Sliding`. Pokud `Absolute`, prvek ObjectDataSource uloží získaná data do mezipaměti pro `CacheDuration` sekund. Pokud `Sliding`, vyprší platnost dat až po `CacheDuration` sekund. Výchozí hodnota je `Absolute`.
- [CacheKeyDependency](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.cachekeydependency.aspx) tuto vlastnost použijte k přidružení položek mezipaměti ObjectDataSource s ke stávající závislosti mezipaměti. Datové položky ObjectDataSource s lze předčasně vyřadit z mezipaměti tím, že vyprší její přidružená `CacheKeyDependency`. Tato vlastnost se nejčastěji používá k přidružení závislosti mezipaměti SQL s mezipamětí ObjectDataSource s, což je téma v budoucnu v kurzu [použití závislostí mezipaměti SQL](using-sql-cache-dependencies-cs.md) .

Umožňuje konfigurovat `ProductsDataSource` ObjectDataSource, aby data mohla ukládat do mezipaměti na 30 sekund na absolutním měřítku. Vlastnost ObjectDataSource `EnableCaching` nastavte na hodnotu `true` a vlastnost `CacheDuration` na hodnotu 30. Ponechte vlastnost `CacheExpirationPolicy` nastavenou na výchozí hodnotu `Absolute`.

[![nakonfigurovat prvek ObjectDataSource tak, aby data mohla ukládat do mezipaměti po dobu 30 sekund](caching-data-with-the-objectdatasource-cs/_static/image28.png)](caching-data-with-the-objectdatasource-cs/_static/image27.png)

**Obrázek 11**: Konfigurace prvku ObjectDataSource pro ukládání dat do mezipaměti po dobu 30 sekund ([kliknutím zobrazíte obrázek v plné velikosti](caching-data-with-the-objectdatasource-cs/_static/image29.png))

Uložte změny a znovu navštivte tuto stránku v prohlížeči. Při první návštěvě stránky se zobrazí text výběr události, který vyvolala událost, protože data nejsou v mezipaměti. Ale následné postbacky spouštěné kliknutím na tlačítko pro odeslání, řazení, stránkování nebo kliknutí na tlačítka pro úpravy nebo zrušení *nezobrazují* příkaz pro výběr události, který vyvolal událost. Důvodem je, že událost `Selecting` je aktivována pouze v případě, že prvek ObjectDataSource získá data z jeho podkladového objektu; událost `Selecting` se neaktivuje, pokud jsou data načítána z mezipaměti dat.

Po 30 sekundách budou data z mezipaměti vyřazena. Data budou také vyřazena z mezipaměti, pokud jsou vyvolány metody ObjectDataSource `Insert`, `Update`nebo `Delete`. V důsledku toho po uplynutí 30 sekund nebo kliknutí na tlačítko Aktualizovat, řazení, stránkování nebo kliknutí na tlačítka pro úpravy nebo zrušení způsobí, že prvek ObjectDataSource získá data z jeho podkladového objektu a zobrazí text, který událost výběru vyvolala, když `Selecting` událost aktivuje. Tyto vrácené výsledky jsou umístěny zpátky do mezipaměti dat.

> [!NOTE]
> Pokud se zobrazí text, který událost výběru vyvolala často, i když očekáváte, že prvek ObjectDataSource bude pracovat s daty uloženými v mezipaměti, může to být způsobeno omezeními paměti. Pokud není dostatek volné paměti, data přidaná do mezipaměti prvku ObjectDataSource mohla být uklizena. Pokud se v prvku ObjectDataSource nejeví správně ukládat data do mezipaměti, nebo je jenom ukládat do mezipaměti, ukončete některé aplikace a uvolněte paměť a zkuste to znovu.

Obrázek 12 znázorňuje pracovní postup pro ukládání do mezipaměti ObjectDataSource s. Když se na obrazovce zobrazí text, který vyvolal událost, je to způsobeno tím, že data nebyla v mezipaměti a musela být načtena z podkladového objektu. V případě, že tento text chybí, ale s tím, že data byla k dispozici z mezipaměti. Když se data vrátí z mezipaměti, neproběhne žádné volání podkladového objektu a proto se neprovede žádné dotazy databáze.

![Prvek ObjectDataSource ukládá a načítá jeho data z mezipaměti dat.](caching-data-with-the-objectdatasource-cs/_static/image30.png)

**Obrázek 12**: prvek ObjectDataSource uchovává a načítá jeho data z mezipaměti dat.

Každá aplikace ASP.NET má svou vlastní instanci mezipaměti dat, která se sdílí se všemi stránkami a návštěvníky. To znamená, že data uložená v mezipaměti dat v prvku ObjectDataSource jsou podobně sdílena ve všech uživatelích, kteří stránku navštívili. Pokud to chcete ověřit, otevřete stránku `ObjectDataSource.aspx` v prohlížeči. Při první návštěvě stránky se zobrazí text vyvolaná událost, která se zobrazí (za předpokladu, že byla data přidaná do mezipaměti pomocí předchozích testů) vyřazením z tohoto okamžiku vyřazena. Otevřete druhou instanci prohlížeče a zkopírujte a vložte adresu URL z první instance prohlížeče do druhé. Ve druhé instanci prohlížeče není zobrazen text vyvolaný událostmi, protože používá stejná data uložená v mezipaměti jako první.

Při vkládání načtených dat do mezipaměti prvek ObjectDataSource používá hodnotu klíče mezipaměti, která zahrnuje: hodnoty vlastností `CacheDuration` a `CacheExpirationPolicy`; typ základního byznys objektu používaného prvkem ObjectDataSource, který je zadán prostřednictvím [vlastnosti`TypeName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.typename.aspx) (`ProductsBLL`v tomto příkladu); hodnota vlastnosti `SelectMethod` a název a hodnoty parametrů v kolekci `SelectParameters`; a hodnoty jeho `StartRowIndex` a `MaximumRows` vlastností, které se používají při implementaci [vlastního stránkování.](../paging-and-sorting/paging-and-sorting-report-data-cs.md)

Vytvoření hodnoty klíče mezipaměti jako kombinace těchto vlastností zajistí při změně těchto hodnot jedinečnou položku mezipaměti. Například v minulých kurzech jsme se podívali na použití `GetProductsByCategoryID(categoryID)``ProductsBLL` třídy s, který vrátí všechny produkty zadané kategorie. Jeden uživatel může přijít na stránku a zobrazit nápoje, jejichž `CategoryID` je 1. Pokud prvek ObjectDataSource ukládá výsledky do mezipaměti bez ohledu na `SelectParameters` hodnoty, když jiný uživatel přestal na stránku a zobrazit koření v době, kdy byly v mezipaměti uložené nápoje, d uvidí nealkoholické produkty v mezipaměti, nikoli koření. Změnou klíče mezipaměti pomocí těchto vlastností, které zahrnují hodnoty `SelectParameters`, prvek ObjectDataSource udržuje samostatnou položku mezipaměti pro nápoje a koření.

## <a name="stale-data-concerns"></a>Obavy o zastaralá data

Prvek ObjectDataSource automaticky vyřadí své položky z mezipaměti, když je vyvolána kterákoli z jeho `Insert`, `Update`nebo `Delete` metod. To pomáhá chránit před zastaralými daty tím, že při změně dat na stránce vymaže položky mezipaměti. Je však možné, že prvek ObjectDataSource používá ukládání do mezipaměti a stále zobrazuje zastaralá data. V nejjednodušším případě může to být způsobeno tím, že se data mění přímo v rámci databáze. Správce databáze pravděpodobně právě spustil skript, který mění některé záznamy v databázi.

Tento scénář může také odložení jemným způsobem. I když prvek ObjectDataSource vyloučí své položky z mezipaměti, když je volána jedna z jeho metod změny dat, odebrané položky v mezipaměti jsou pro konkrétní kombinaci vlastností prvků ObjectDataSource (`CacheDuration`, `TypeName`, `SelectMethod`a tak dále). Pokud máte dvě ObjectDataSource, které používají různé `SelectMethods` nebo `SelectParameters`, ale stále mohou aktualizovat stejná data, pak jedna prvek ObjectDataSource může aktualizovat řádek a zrušit platnost svých záznamů v mezipaměti, ale odpovídající řádek pro druhý prvek ObjectDataSource bude i nadále obsluhován z mezipaměti. Doporučuje se vytvářet stránky, na které se tato funkce projeví. Vytvořte stránku, která zobrazí upravitelnou datovou prvek GridView, který načte svá data z prvku ObjectDataSource, který používá ukládání do mezipaměti a je nakonfigurován pro získání dat z `GetProducts()` metody `ProductsBLL` třídy s. Přidejte další upravitelný prvek GridView a prvek ObjectDataSource na tuto stránku (nebo jinou), ale pro tuto druhou prvek ObjectDataSource použijte metodu `GetProductsByCategoryID(categoryID)`. Vzhledem k tomu, že se tyto dva ObjectDataSource `SelectMethod` vlastnosti liší, každá z nich má své vlastní hodnoty uložené v mezipaměti. Pokud upravíte produkt v jedné mřížce, při příštím navázání dat zpět do jiné mřížky (po stránkování, řazení atd.) bude i nadále fungovat stará data uložená v mezipaměti a nebudou odrážet změny provedené z jiné mřížky.

V krátké době vyprší jenom vypršení platnosti, pokud jste si ochotni mít možnost mít zastaralá data a využijete kratší vypršení platnosti pro scénáře, ve kterých je aktuálnost dat důležité. Pokud nejsou zastaralá data přijatelná, buď nepovolí ukládání do mezipaměti, nebo použití závislostí mezipaměti SQL (za předpokladu, že se jedná o databázová data, která jste Závislosti mezipaměti SQL prozkoumáme v budoucím kurzu.

## <a name="summary"></a>Přehled

V tomto kurzu jsme prozkoumali integrované možnosti ukládání do mezipaměti v prvku ObjectDataSource s. Pouhým nastavením několika vlastností můžeme ovládacím prvkem ObjectDataSource dát do mezipaměti výsledky vrácené ze zadaného `SelectMethod` do mezipaměti dat ASP.NET. Vlastnosti `CacheDuration` a `CacheExpirationPolicy` označují dobu, po kterou je položka ukládána do mezipaměti, a zda se jedná o absolutní nebo klouzavé vypršení platnosti. Vlastnost `CacheKeyDependency` přidružuje všechny položky mezipaměti ObjectDataSource s existující závislostí mezipaměti. To lze použít k vyřazení položek ObjectDataSource s z mezipaměti před dosažením vypršení časového limitu, který se obvykle používá u závislostí mezipaměti SQL.

Vzhledem k tomu, že prvek ObjectDataSource jednoduše ukládá do mezipaměti své hodnoty do mezipaměti dat, můžeme programově replikovat vestavěnou funkci ObjectDataSource s. Nevyužívá smysl k tomu, aby to provedla v prezentační vrstvě, protože prvek ObjectDataSource tuto funkci nabízí mimo pole, ale v samostatné vrstvě architektury můžeme implementovat funkce ukládání do mezipaměti. K tomu musíme opakovat stejnou logiku, jakou používá prvek ObjectDataSource. Podíváme se, jak programově pracovat s datovou mezipamětí v rámci architektury v našem dalším kurzu.

Šťastné programování!

## <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [ASP.NET Caching: postupy a osvědčené postupy](https://msdn.microsoft.com/library/aa478965.aspx)
- [Průvodce architekturou ukládání do mezipaměti pro aplikace .NET Framework](https://msdn.microsoft.com/library/ee817645.aspx)
- [Ukládání výstupu do mezipaměti v ASP.NET 2,0](http://aspnet.4guysfromrolla.com/articles/121306-1.aspx)

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Teresa Murphy. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](caching-data-in-the-architecture-cs.md)

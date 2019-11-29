---
uid: web-forms/overview/data-access/paging-and-sorting/sorting-custom-paged-data-cs
title: Řazení vlastních stránkovaných dat (C#) | Microsoft Docs
author: rick-anderson
description: V předchozím kurzu jsme zjistili, jak implementovat vlastní stránkování při prezentaci dat na webové stránce. V tomto kurzu se naučíme, jak výše uvedený postup zvětšit...
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 778baa4e-4af8-4665-947e-7a01d1a4dff2
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/sorting-custom-paged-data-cs
msc.type: authoredcontent
ms.openlocfilehash: e55ed9b92814753e95bdfdf26c2f051df6f2630d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74642407"
---
# <a name="sorting-custom-paged-data-c"></a>Řazení dat s vlastním stránkováním (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_26_CS.exe) nebo [Stáhnout PDF](sorting-custom-paged-data-cs/_static/datatutorial26cs1.pdf)

> V předchozím kurzu jsme zjistili, jak implementovat vlastní stránkování při prezentaci dat na webové stránce. V tomto kurzu se naučíme, jak výše uvedený příklad zvětšit, aby zahrnoval podporu pro řazení vlastního stránkování.

## <a name="introduction"></a>Úvod

Ve srovnání s výchozím stránkováním může vlastní stránkování zlepšit výkon stránkování prostřednictvím dat několika různými objednávkami a udělat si vlastní stránkování – volba de facto stránkování implementace při stránkování prostřednictvím velkých objemů dat. Implementace vlastního stránkování je větší než implementace výchozího stránkování, ale zejména při přidávání řazení do kombinace. V tomto kurzu rozšíříme příklad z předchozí verze, aby se zahrnula podpora pro řazení *a* vlastní stránkování.

> [!NOTE]
> Vzhledem k tomu, že tento kurz sestaví na předchozí straně, před začátkem kopírování deklarativní syntaxe v rámci `<asp:Content>` elementu z předchozí webové stránky kurzu (`EfficientPaging.aspx`) a vložení mezi `<asp:Content>` elementu na stránce `SortParameter.aspx`. Podívejte se zpátky na krok 1 v tématu [Přidání ovládacích prvků ověřování do kurzu pro úpravy a vkládání rozhraní](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md) , kde najdete podrobnější diskuzi o replikaci funkčnosti jedné stránky ASP.NET do druhé.

## <a name="step-1-reexamining-the-custom-paging-technique"></a>Krok 1: Kontrola vlastní techniky stránkování

Aby vlastní stránkování fungovalo správně, je nutné implementovat určitou techniku, která může efektivně připustit konkrétní podmnožinu záznamů s indexem počátečního řádku a maximálním počtem parametrů řádků. Existuje několik postupů, které lze použít k dosažení tohoto cíle. V předchozím kurzu jsme se vyhledali pomocí Microsoft SQL Server 2005 s nové funkce hodnocení `ROW_NUMBER()`. V krátkém případě funkce třídění `ROW_NUMBER()` přiřadí číslo řádku každému řádku vrácenému dotazem, který je seřazen podle zadaného pořadí řazení. Příslušná podmnožina záznamů se pak získá tak, že se vrátí konkrétní část očíslovaných výsledků. Následující dotaz znázorňuje, jak použít tuto techniku k vrácení těchto produktů číslovaných 11 až 20 při řazení výsledků seřazené podle abecedy podle `ProductName`:

[!code-sql[Main](sorting-custom-paged-data-cs/samples/sample1.sql)]

Tato technika funguje dobře pro stránkování pomocí konkrétního pořadí řazení (`ProductName` v tomto případě seřazené podle abecedy), ale dotaz musí být upraven, aby zobrazoval výsledky seřazené podle jiného výrazu řazení. V ideálním případě lze výše uvedený dotaz přepsat tak, aby používal parametr v klauzuli `OVER`, například:

[!code-sql[Main](sorting-custom-paged-data-cs/samples/sample2.sql)]

Nicméně parametrizované klauzule `ORDER BY` nejsou povoleny. Místo toho je nutné vytvořit uloženou proceduru, která přijímá vstupní parametr `@sortExpression`, ale používá jedno z následujících řešení:

- Zápis pevně kódovaných dotazů pro každý výraz řazení, který může být použit; pak pomocí `IF/ELSE` příkazů T-SQL určete, který dotaz se má provést.
- Pomocí příkazu `CASE` můžete poskytnout dynamické `ORDER BY` výrazy založené na vstupním parametru `@sortExpressio` n. Další informace najdete v části využívané k dynamickému řazení výsledků dotazu v tématu [výkon příkazů SQL `CASE`](http://www.4guysfromrolla.com/webtech/102704-1.shtml) .
- Vyplní příslušný dotaz jako řetězec v uložené proceduře a pak pomocí [uložené procedury `sp_executesql` systému](https://msdn.microsoft.com/library/ms188001.aspx) spusťte dynamický dotaz.

Každé z těchto alternativních řešení obsahuje některé nevýhody. První možnost není stejná jako druhá druhá, protože vyžaduje, abyste vytvořili dotaz pro každý možný výraz řazení. Proto pokud se později rozhodnete přidat nová pole, která lze seřadit na prvek GridView, budete také muset vrátit zpět a aktualizovat uloženou proceduru. Druhý přístup má několik odlišností, které zavádějí problémy související s výkonem při řazení neřetězcovými sloupci databáze a zároveň trpí stejnými problémy udržovatelnosti jako první. A třetí volba, která používá dynamický SQL, zavádí riziko pro útok prostřednictvím injektáže SQL, pokud útočník může spustit uloženou proceduru procházející v hodnotách vstupních parametrů jejich výběru.

I když žádný z těchto přístupů není ideální, myslíme na to, že třetí možnost je nejlepší z těchto tří možností. S využitím dynamického SQL nabízí úroveň flexibility, které ostatní dva nemají. Útok na injektáže SQL je navíc možné zneužít pouze v případě, že útočník může spustit uloženou proceduru procházející vstupními parametry svého výběru. Vzhledem k tomu, že DAL používá parametrizované dotazy, ADO.NET bude chránit tyto parametry, které se odesílají do databáze prostřednictvím architektury, což znamená, že zranitelnost proti útokům prostřednictvím injektáže SQL existuje jenom v případě, že by útočník mohl přímo spustit uloženou proceduru.

K implementaci této funkce vytvořte v databázi Northwind novou uloženou proceduru s názvem `GetProductsPagedAndSorted`. Tato uložená procedura by měla přijímat tři vstupní parametry: `@sortExpression`, vstupní parametr typu `nvarchar(100`), který určuje, jak by měly být výsledky seřazeny a vloženy přímo po `ORDER BY` textu v klauzuli `OVER`; a `@startRowIndex` a `@maximumRows`, stejné dva celočíselné vstupní parametry z `GetProductsPaged` uložené procedury byly zkontrolovány v předchozím kurzu. Pomocí následujícího skriptu vytvořte `GetProductsPagedAndSorted` uloženou proceduru:

[!code-sql[Main](sorting-custom-paged-data-cs/samples/sample3.sql)]

Uložená procedura začíná tím, že zajistí, že je zadána hodnota parametru `@sortExpression`. Pokud chybí, výsledky jsou seřazené podle `ProductID`. Dále je vytvořen dynamický dotaz SQL. Všimněte si, že se tady dynamický dotaz SQL mírně liší od předchozích dotazů použitých k načtení všech řádků z tabulky Products. V předchozích příkladech jsme získali jednotlivé typy přidružených kategorií s a dodavatelů s použitím poddotazu. Toto rozhodnutí bylo provedeno zpět v kurzu [Vytvoření vrstvy přístupu k datům](../introduction/creating-a-data-access-layer-cs.md) a bylo provedeno místo použití `JOIN` s, protože TableAdapter nemůže automaticky vytvořit související metody vložení, aktualizace a odstranění pro takové dotazy. `GetProductsPagedAndSorted` uloženou proceduru ale musí použít `JOIN` s, aby se výsledky objednaly podle kategorií nebo názvů dodavatelů.

Tento dynamický dotaz je sestaven zřetězením částí statických dotazů a parametrů `@sortExpression`, `@startRowIndex`a `@maximumRows`. Vzhledem k tomu, že `@startRowIndex` a `@maximumRows` jsou parametry typu Integer, je nutné je převést na hodnoty nvarchar, aby byly správně zřetězeny. Po sestavení tohoto dynamického dotazu SQL je provedeno prostřednictvím `sp_executesql`.

Chvíli počkejte, než tuto uloženou proceduru otestujete s různými hodnotami parametrů `@sortExpression`, `@startRowIndex`a `@maximumRows`. V Průzkumník serveru klikněte pravým tlačítkem na název uložené procedury a vyberte spustit. Tím se zobrazí dialogové okno spustit uloženou proceduru, do kterého můžete zadat vstupní parametry (viz obrázek 1). Pro seřazení výsledků podle názvu kategorie použijte NázevKategorie pro hodnotu parametru `@sortExpression`. Chcete-li seřadit podle názvu společnosti dodavatele s, použijte CompanyName. Po zadání hodnot parametrů klikněte na OK. Výsledky se zobrazí v okně výstup. Na obrázku 2 se zobrazují výsledky při vracení produktů při řazení podle `UnitPrice` v sestupném pořadí podle hodnocení 11 až 20.

![Zkuste jiné hodnoty pro uložené procedury s třemi vstupními parametry.](sorting-custom-paged-data-cs/_static/image1.png)

**Obrázek 1**: zkuste použít jiné hodnoty pro uložené procedury s třemi vstupními parametry.

[![uložené procedury s výsledky se zobrazují v okno Výstup](sorting-custom-paged-data-cs/_static/image3.png)](sorting-custom-paged-data-cs/_static/image2.png)

**Obrázek 2**: výsledky uložené procedury s jsou zobrazeny v okno výstup ([kliknutím zobrazíte obrázek v plné velikosti).](sorting-custom-paged-data-cs/_static/image4.png)

> [!NOTE]
> Při řazení výsledků podle zadaného `ORDER BY` sloupce v klauzuli `OVER` musí SQL Server seřadit výsledky. Jedná se o rychlou operaci, pokud je ve sloupcích clusterovaný index, výsledky jsou seřazeny podle nebo v případě, že existuje pokrýváný index, ale může být levnější v jiném. Pro zlepšení výkonu pro dostatečně velké dotazy zvažte přidání neclusterovaných indexů pro sloupec, podle kterého jsou výsledky seřazeny. Další podrobnosti najdete v tématu věnovaném [funkcím řazení a výkonu v SQL Server 2005](http://www.sql-server-performance.com/ak_ranking_functions.asp) .

## <a name="step-2-augmenting-the-data-access-and-business-logic-layers"></a>Krok 2: rozšíření vrstvy přístupu k datům a obchodní logiky

Když je vytvořená uložená procedura `GetProductsPagedAndSorted`, je dalším krokem poskytnutí prostředků ke spuštění této uložené procedury prostřednictvím naší aplikační architektury. To zahrnuje přidání vhodné metody do DAL i do knihoven BLL. Nechte začít přidáním metody do DAL. Otevřete `Northwind.xsd` typovou datovou sadu, klikněte pravým tlačítkem na `ProductsTableAdapter`a v místní nabídce vyberte možnost Přidat dotaz. Stejně jako v předchozím kurzu chceme tuto novou metodu DAL nakonfigurovat tak, aby používala existující uloženou proceduru – `GetProductsPagedAndSorted`v tomto případě. Začněte tím, že chcete, aby nová metoda TableAdapter používala existující uloženou proceduru.

![Zvolit použití existující uložené procedury](sorting-custom-paged-data-cs/_static/image5.png)

**Obrázek 3**: Volba použití existující uložené procedury

Chcete-li určit uloženou proceduru, kterou chcete použít, vyberte v rozevíracím seznamu na další obrazovce `GetProductsPagedAndSorted` uloženou proceduru.

![Použít uloženou proceduru GetProductsPagedAndSorted](sorting-custom-paged-data-cs/_static/image6.png)

**Obrázek 4**: použijte uloženou proceduru GetProductsPagedAndSorted.

Tato uložená procedura vrátí sadu záznamů jako výsledek tak, aby na další obrazovce označovala, že vrátí tabulková data.

![Označení, že uložená procedura vrátí tabulková data](sorting-custom-paged-data-cs/_static/image7.png)

**Obrázek 5**: označení, že uložená procedura vrátí tabulková data

Nakonec vytvořte metody DAL, které používají naplnit DataTable a vracejí vzor DataTable, a pojmenujte metody `FillPagedAndSorted` a `GetProductsPagedAndSorted`, v uvedeném pořadí.

![Zvolit názvy metod](sorting-custom-paged-data-cs/_static/image8.png)

**Obrázek 6**: volba názvů metod

Teď, když jsme rozšířili DAL, jsme znovu připraveni na knihoven BLL. Otevřete soubor `ProductsBLL` třídy a přidejte novou metodu `GetProductsPagedAndSorted`. Tato metoda musí přijmout tři vstupní parametry `sortExpression`, `startRowIndex`a `maximumRows` a měla by se jednoduše zavolat do `GetProductsPagedAndSorted`é metody DAL s, například takto:

[!code-csharp[Main](sorting-custom-paged-data-cs/samples/sample4.cs)]

## <a name="step-3-configuring-the-objectdatasource-to-pass-in-the-sortexpression-parameter"></a>Krok 3: Konfigurace prvku ObjectDataSource, který bude předávat parametr SortExpression

Po rozšíření DAL a knihoven BLL, aby zahrnovaly metody, které využívají `GetProductsPagedAndSorted` uloženou proceduru, vše zůstává ke konfiguraci prvku ObjectDataSource na stránce `SortParameter.aspx`, aby používala novou metodu knihoven BLL a předávala parametr `SortExpression` na základě sloupce, podle kterého uživatel požadoval řazení výsledků.

Začněte změnou `SelectMethod` ObjectDataSource s z `GetProductsPaged` na `GetProductsPagedAndSorted`. To lze provést pomocí Průvodce konfigurací zdroje dat, z okno Vlastnosti nebo přímo prostřednictvím deklarativní syntaxe. Dále je potřeba zadat hodnotu [vlastnosti`SortParameterName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sortparametername.aspx)ObjectDataSource s. Je-li tato vlastnost nastavena, prvek ObjectDataSource se pokusí předat do `SelectMethod`vlastnosti `SortExpression` prvku GridView. Konkrétně prvek ObjectDataSource hledá vstupní parametr, jehož název je roven hodnotě vlastnosti `SortParameterName`. Vzhledem k tomu, že metoda knihoven BLL s `GetProductsPagedAndSorted` obsahuje vstupní parametr výrazu řazení s názvem `sortExpression`, nastavte vlastnost ObjectDataSource s `SortExpression` na sortExpression.

Po provedení těchto dvou změn by deklarativní syntaxe ObjectDataSource s měla vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](sorting-custom-paged-data-cs/samples/sample5.aspx)]

> [!NOTE]
> Stejně jako v předchozím kurzu zajistěte, aby prvek ObjectDataSource *nezahrnul vstupní* parametry SortExpression, StartRowIndex nebo MaximumRows do své kolekce SelectParameters.

Chcete-li v prvku GridView Povolit řazení, stačí zaškrtnout políčko Povolit řazení v inteligentní značce GridView s, která nastaví vlastnost `AllowSorting` prvku GridView, aby `true` a způsobila, že text záhlaví každého sloupce bude vykreslen jako LinkButton. Když koncový uživatel klikne na jednu z hlaviček LinkButtons, vystavení se podstaví a následující kroky se zobrazí:

1. Prvek GridView aktualizuje svou [vlastnost`SortExpression`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx) na hodnotu `SortExpression` pole, jehož odkaz na hlavičku byl kliknuto.
2. Prvek ObjectDataSource vyvolá metodu `GetProductsPagedAndSorted` knihoven BLL s, která předá vlastnost GridView s `SortExpression` jako hodnotu pro vstupní parametr metody `sortExpression` (spolu s příslušnými `startRowIndex` a `maximumRows` hodnotami vstupních parametrů).
3. KNIHOVEN BLL vyvolá metodu DAL s `GetProductsPagedAndSorted`.
4. DAL spustí `GetProductsPagedAndSorted` uloženou proceduru, předává parametr `@sortExpression` (spolu s `@startRowIndex`mi a `@maximumRows` hodnotami vstupních parametrů).
5. Uložená procedura vrátí příslušnou podmnožinu dat do knihoven BLL, která je vrátí do prvku ObjectDataSource; Tato data jsou následně svázána s prvku GridView, vykreslena do kódu HTML a odeslána koncovému uživateli.

Obrázek 7 zobrazuje první stránku výsledků při řazení podle `UnitPrice` ve vzestupném pořadí.

[![výsledky jsou seřazené podle JednotkováCena.](sorting-custom-paged-data-cs/_static/image10.png)](sorting-custom-paged-data-cs/_static/image9.png)

**Obrázek 7**: výsledky jsou seřazené podle hodnoty UnitPrice ([kliknutím zobrazíte obrázek v plné velikosti](sorting-custom-paged-data-cs/_static/image11.png)).

I když aktuální implementace může správně seřadit výsledky podle názvu produktu, názvu kategorie, množství na jednotku a jednotkové ceny a při pokusu o seřazení výsledků podle názvu dodavatele dojde k výjimce za běhu (viz obrázek 8).

![Při pokusu o seřazení výsledků dodavatelem dojde k následující výjimce za běhu.](sorting-custom-paged-data-cs/_static/image12.png)

**Obrázek 8**: při pokusu o seřazení výsledků dodavatelem dojde k následující výjimce za běhu.

K této výjimce dojde, protože `SortExpression` prvku GridView `SupplierName` vlastnost BoundField je nastavena na `SupplierName`. Název dodavatele v `Suppliers` tabulce se ale ve skutečnosti označuje jako `CompanyName` pro tento název sloupce jsme jako `SupplierName`i alias. Klauzule `OVER` používaná funkcí `ROW_NUMBER()` ale nemůže alias použít a musí používat skutečný název sloupce. Proto změňte `SupplierName` vlastnost BoundField s `SortExpression` z hodnoty dodavatel na CompanyName (viz obrázek 9). Jak ukazuje obrázek 10, po této změně se výsledky dají seřadit podle dodavatele.

![Změňte pole dodavatel vlastnost BoundField s SortExpression na CompanyName.](sorting-custom-paged-data-cs/_static/image13.png)

**Obrázek 9**: Změna vlastnost BoundField dodavatele s SortExpression na CompanyName

[![výsledků se teď dají seřadit podle dodavatele.](sorting-custom-paged-data-cs/_static/image15.png)](sorting-custom-paged-data-cs/_static/image14.png)

**Obrázek 10**: výsledky se teď dají seřadit podle dodavatele ([kliknutím zobrazíte obrázek v plné velikosti).](sorting-custom-paged-data-cs/_static/image16.png)

## <a name="summary"></a>Přehled

Implementace vlastního stránkování, kterou jsme prozkoumali v předchozím kurzu, vyžaduje, aby bylo v době návrhu zadáno pořadí, podle kterého byly výsledky seřazeny. V krátké době to znamenalo, že implementace vlastního stránkování, kterou jsme implementovali, se ve stejnou chvíli nepovedla, ale nabízí možnosti řazení. V tomto kurzu toto omezení overcame rozšířením úložné procedury z prvního na zahrnutí vstupního parametru `@sortExpression`, podle kterého by bylo možné seřadit výsledky.

Po vytvoření této uložené procedury a vytvoření nových metod v rámci DAL a knihoven BLL jsme dokázali implementovat ovládací prvek GridView, který nabídl řazení i vlastní stránkování, a to tak, že se prvek ObjectDataSource nastaví tak, aby předával v rámci vlastnosti GridViewa s aktuálním `SortExpression` do `SelectMethod`knihoven BLL.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Carlos Santos. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](efficiently-paging-through-large-amounts-of-data-cs.md)
> [Další](creating-a-customized-sorting-user-interface-cs.md)

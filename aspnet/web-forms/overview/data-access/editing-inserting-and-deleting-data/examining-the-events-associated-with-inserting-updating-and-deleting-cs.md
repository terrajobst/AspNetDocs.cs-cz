---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs
title: Prozkoumání událostí spojených s vložením, aktualizací a odstraněnímC#() | Microsoft Docs
author: rick-anderson
description: V tomto kurzu prověříme události, ke kterým dojde před, během a po operaci vložení, aktualizace nebo odstranění webového ovládacího prvku ASP.NET data. W...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: dab291a0-a8b5-46fa-9dd8-3d35b249201f
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-cs
msc.type: authoredcontent
ms.openlocfilehash: a8c1388b73524a8bb918b67aa265db894c07636f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78609149"
---
# <a name="examining-the-events-associated-with-inserting-updating-and-deleting-c"></a>Zkoumání událostí spojených s vložením, aktualizací a odstraněním (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_17_CS.exe) nebo [Stáhnout PDF](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/datatutorial17cs1.pdf)

> V tomto kurzu prověříme události, ke kterým dojde před, během a po operaci vložení, aktualizace nebo odstranění webového ovládacího prvku ASP.NET data. Také se dozvíte, jak přizpůsobit rozhraní pro úpravy tak, aby se aktualizovala pouze podmnožina polí produktu.

## <a name="introduction"></a>Úvod

Při použití vestavěných funkcí pro vkládání, úpravy nebo odstraňování funkcí ovládacího prvku GridView, DetailsView nebo FormView se celá řada kroků zobrazí, když koncový uživatel dokončí proces přidání nového záznamu nebo aktualizace nebo odstranění existujícího záznamu. Jak jsme probrali v [předchozím kurzu](an-overview-of-inserting-updating-and-deleting-data-cs.md), když se v prvku GridView upraví řádek, tlačítko Upravit je nahrazeno tlačítky aktualizovat a zrušit a BoundFields přepínat na textová pole. Jakmile koncový uživatel aktualizuje data a klikne na aktualizovat, provedou se následující kroky při zpětném odeslání:

1. Prvek GridView naplní své prvky ObjectDataSource `UpdateParameters` s jedinečným identifikačním polem (přes vlastnost `DataKeyNames`) upravovaného záznamu spolu s hodnotami zadanými uživatelem.
2. Prvek GridView Vyvolá metodu `Update()` prvku ObjectDataSource, která zase vyvolá příslušnou metodu v podkladovém objektu (`ProductsDAL.UpdateProduct`, v našem předchozím kurzu).
3. Podkladová data, která nyní obsahují aktualizované změny, jsou svázána s prvku GridView.

Během této sekvence kroků se může vyvolávat několik událostí, což nám umožní vytvářet obslužné rutiny událostí pro přidání vlastní logiky tam, kde je to potřeba. Například před krokem 1 se aktivuje událost `RowUpdating` prvku GridView. V tuto chvíli můžeme žádost o aktualizaci zrušit, pokud došlo k chybě ověřování. Když je vyvolána metoda `Update()`, aktivuje se událost `Updating` prvku ObjectDataSource, která poskytuje příležitost k přidání nebo přizpůsobení hodnot všech `UpdateParameters`. Po dokončení provádění metody základního objektu ObjectDataSource je vyvolána událost `Updated` prvku ObjectDataSource. Obslužná rutina události `Updated` může zkontrolovat podrobnosti o operaci aktualizace, například kolik řádků bylo ovlivněno a zda došlo k výjimce. Nakonec po kroku 2 se aktivuje událost `RowUpdated` prvku GridView; Obslužná rutina události pro tuto událost může prošetřit další informace o právě provedené operaci aktualizace.

Obrázek 1 znázorňuje tuto řadu událostí a kroků při aktualizaci prvku GridView. Vzor události na obrázku 1 není jedinečný pro aktualizaci pomocí prvku GridView. Vložení, aktualizace nebo odstranění dat z prvku GridView, DetailsView nebo FormView sestaví stejnou sekvenci událostí před a po úrovni pro webový ovládací prvek data i ObjectDataSource.

[![řady událostí spouštěných před a po událostech při aktualizaci dat v prvku GridView.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image2.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image1.png)

**Obrázek 1**: řada aktiv před a po událostech při aktualizaci dat v prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image3.png))

V tomto kurzu prověříme tyto události a rozšíříme možnosti vkládání, aktualizace a odstraňování webových ovládacích prvků ASP.NET data. Také se dozvíte, jak přizpůsobit rozhraní pro úpravy tak, aby se aktualizovala pouze podmnožina polí produktu.

## <a name="step-1-updating-a-productsproductnameandunitpricefields"></a>Krok 1: aktualizace polí`ProductName`a`UnitPrice`produktu

V rozhraní pro úpravy z předchozího kurzu musela být zahrnutá *všechna* pole produktu, která byla jen pro čtení. Pokud jsme chtěli odebrat pole z prvku GridView – řekněme `QuantityPerUnit` – při aktualizaci dat webový ovládací prvek data by nastavil `UpdateParameters` hodnotu prvku ObjectDataSource `QuantityPerUnit`. Prvek ObjectDataSource pak předáte `null` hodnotu do metody `UpdateProduct` knihoven BLL (Business Logic Layer), která by změnila sloupec `QuantityPerUnit` upravovaného databázového záznamu na `NULL` hodnotu. Podobně platí, že pokud je požadované pole, například `ProductName`, odebráno z rozhraní pro úpravy, aktualizace se nezdaří a "*sloupec" ProductName "nepovoluje hodnotu null*". Důvodem tohoto chování bylo, že prvek ObjectDataSource byl nakonfigurován tak, aby volal metodu `UpdateProduct` třídy `ProductsBLL`, která očekávala vstupní parametr pro každé pole produktu. Proto kolekce `UpdateParameters` ObjectDataSource obsahuje parametr pro každý vstupní parametr metody.

Pokud chceme poskytnout datovou datovou datovou položku, která umožňuje koncovému uživateli aktualizovat pouze podmnožinu polí, je nutné buď programově nastavit chybějící `UpdateParameters` hodnoty v obslužné rutině události `Updating` ObjectDataSource nebo vytvořit a volat metodu knihoven BLL, která očekává pouze podmnožinu polí. Pojďme tento přístup prozkoumat.

Konkrétně vytvoříme stránku, která zobrazí pouze pole `ProductName` a `UnitPrice` v upravitelném prvku GridView. Rozhraní pro úpravy tohoto prvku GridView umožní uživateli aktualizovat pouze dvě zobrazená pole `ProductName` a `UnitPrice`. Vzhledem k tomu, že toto rozhraní pro úpravy poskytuje pouze podmnožinu polí produktu, je nutné vytvořit prvek ObjectDataSource, který používá existující `UpdateProduct` metodu knihoven BLL a má chybějící hodnoty pole produktu, které jsou nastaveny programově ve své obslužné rutině události `Updating`, nebo musíme vytvořit novou metodu knihoven BLL, která očekává pouze podmnožinu polí definovaných v prvku GridView. Pro účely tohoto kurzu použijeme druhou možnost a vytvoříme přetížení metody `UpdateProduct`, kterou používá jenom tři vstupní parametry: `productName`, `unitPrice`a `productID`:

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample1.cs)]

Podobně jako původní metoda `UpdateProduct` se toto přetížení spustí tak, že zkontroluje, jestli v databázi není nějaký produkt se zadaným `ProductID`. V takovém případě vrátí `false`, což znamená, že žádost o aktualizaci informací o produktu se nezdařila. V opačném případě aktualizuje existující `ProductName` a `UnitPrice` pole záznamu produktu a potvrdí aktualizaci voláním `Update()` metody TableAdapter, která předává instanci `ProductsRow`.

S tímto přidáním do naší `ProductsBLL` třídy jsme připraveni vytvořit zjednodušené rozhraní GridView. Otevřete `DataModificationEvents.aspx` ve složce `EditInsertDelete` a přidejte prvek GridView do stránky. Vytvořte nový prvek ObjectDataSource a nakonfigurujte ho tak, aby používal třídu `ProductsBLL` s mapováním jeho `Select()`ch metod na `GetProducts` a jeho `Update()`ou metodou mapování na `UpdateProduct` přetížení, které používá pouze `productName`, `unitPrice`a `productID` vstupních parametrů. Obrázek 2 ukazuje Průvodce vytvořením zdroje dat při mapování `Update()` metody prvku ObjectDataSource na nové přetížení metody `UpdateProduct` `ProductsBLL` třídy.

[![namapovat metodu Update () prvku ObjectDataSource na nové přetížení UpdateProduct](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image5.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image4.png)

**Obrázek 2**: namapujte metodu `Update()` prvku ObjectDataSource na nové přetížení `UpdateProduct` ([kliknutím zobrazíte obrázek v plné velikosti).](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image6.png)

Vzhledem k tomu, že náš příklad bude zpočátku potřebovat možnost upravovat data, ale ne vkládat nebo odstraňovat záznamy, je nutné explicitně určit, že metody `Insert()` a `Delete()` elementu ObjectDataSource by neměly být namapovány na žádnou z metod třídy `ProductsBLL`, a to tak, že přejdete na karty Vložit a odstranit a v rozevíracím seznamu zvolíte možnost (žádné).

[z rozevíracího seznamu pro karty Vložit a odstranit ![zvolit (žádné).](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image8.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image7.png)

**Obrázek 3**: vyberte (žádný) z rozevíracího seznamu pro záložky INSERT a Delete ([kliknutím zobrazíte obrázek v plné velikosti).](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image9.png)

Po dokončení tohoto průvodce zaškrtněte políčko Povolit úpravy z inteligentní značky prvku GridView.

Při dokončení Průvodce vytvořením zdroje dat a vázání na prvek GridView vytvořila aplikace Visual Studio deklarativní syntaxi pro oba ovládací prvky. Přejít do zobrazení zdroje a zkontrolovat deklarativní označení prvku ObjectDataSource, které je zobrazeno níže:

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample2.aspx)]

Vzhledem k tomu, že nejsou k dispozici žádná mapování pro metody `Insert()` a `Delete()` prvku ObjectDataSource, nejsou žádné `InsertParameters` ani oddíly `DeleteParameters`. Kromě toho, vzhledem k tomu, že `Update()` metoda je namapována na přetížení metody `UpdateProduct`, která přijímá pouze tři vstupní parametry, oddíl `UpdateParameters` má pouze tři instance `Parameter`.

Všimněte si, že vlastnost `OldValuesParameterFormatString` prvku ObjectDataSource je nastavena na hodnotu `original_{0}`. Tato vlastnost je automaticky nastavena sadou Visual Studio při použití Průvodce konfigurací zdroje dat. Vzhledem k tomu, že naše metody knihoven BLL neočekávají, že původní hodnota `ProductID` má být předána, odeberte přiřazení této vlastnosti z deklarativní syntaxe prvku ObjectDataSource.

> [!NOTE]
> Pokud jednoduše vymažete hodnotu vlastnosti `OldValuesParameterFormatString` z okno Vlastnosti ve zobrazení Návrh, bude vlastnost stále existovat v deklarativní syntaxi, ale bude nastavena na prázdný řetězec. Buď odeberte vlastnost zcela z deklarativní syntaxe nebo z okno Vlastnosti nastavte výchozí hodnotu `{0}`.

I když prvek ObjectDataSource má pouze `UpdateParameters` pro název produktu, cenu a ID, Visual Studio přidalo do prvku GridView hodnotu vlastnost BoundField nebo třídě CheckBoxField podporována pro každé pole produktu.

[![prvek GridView obsahuje pro každé pole produktu vlastnost BoundField nebo třídě CheckBoxField podporována.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image11.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image10.png)

**Obrázek 4**: prvek GridView obsahuje vlastnost BoundField nebo třídě CheckBoxField podporována pro každé pole produktu ([kliknutím zobrazíte obrázek v plné velikosti).](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image12.png)

Když koncový uživatel upraví produkt a klikne na jeho tlačítko aktualizace, prvek GridView vytvoří výčet těchto polí, která nebyla jen pro čtení. Potom nastaví hodnotu odpovídající parametr v kolekci `UpdateParameters` ObjectDataSource na hodnotu zadanou uživatelem. Pokud není k dispozici odpovídající parametr, prvek GridView ho přidá do kolekce. Proto pokud v našem prvku GridView obsahuje BoundFields a CheckBoxFields pro všechna pole produktu, prvek ObjectDataSource ukončí vyvolání `UpdateProduct` přetížení, které převezme všechny tyto parametry, navzdory tomu, že deklarativní označení ovládacího prvku ObjectDataSource určuje pouze tři vstupní parametry (viz obrázek 5). Podobně, pokud je v prvku GridView nějaká kombinace polí produktu, která nejsou jen pro čtení, která neodpovídá vstupním parametrům pro `UpdateProduct` přetížení, při pokusu o aktualizaci se vyvolá výjimka.

[![bude prvek GridView přidávat parametry do kolekce UpdateParameters ObjectDataSource](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image14.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image13.png)

**Obrázek 5**: prvek GridView přidá parametry do kolekce `UpdateParameters` ObjectDataSource ([kliknutím zobrazíte obrázek v plné velikosti).](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image15.png)

Chcete-li zajistit, aby prvek ObjectDataSource vyvolal přetížení `UpdateProduct`, které přebírá pouze název produktu, cenu a ID, je nutné omezit prvek GridView tak, aby měl upravitelná pole pro pouze `ProductName` a `UnitPrice`. To lze provést odebráním ostatních BoundFields a CheckBoxFields nastavením vlastností `ReadOnly` na hodnotu `true`nebo kombinací dvou polí. Pro tento kurz můžeme jednoduše odebrat všechna pole GridView s výjimkou `ProductName` a `UnitPrice` BoundFields, po které bude deklarativní označení prvku GridView vypadat takto:

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample3.aspx)]

I když přetížení `UpdateProduct` očekává tři vstupní parametry, máme v našem prvku GridView pouze dvě BoundFields. Důvodem je, že vstupní parametr `productID` je hodnota primárního klíče a byla předána prostřednictvím hodnoty vlastnosti `DataKeyNames` upravovaného řádku.

Náš prvek GridView, společně s `UpdateProduct` přetížením, umožňuje uživateli upravit pouze název a cenu produktu, aniž by ztratili jakékoli jiné pole produktu.

[![rozhraní umožňuje upravovat pouze název a cenu produktu.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image17.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image16.png)

**Obrázek 6**: rozhraní umožňuje upravovat pouze název a cenu produktu ([kliknutím zobrazíte obrázek v plné velikosti](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image18.png)).

> [!NOTE]
> Jak je popsáno v předchozím kurzu, je důležité, aby byl povolen stav zobrazení GridView s (výchozí chování). Pokud nastavíte vlastnost `EnableViewState` prvku GridView s na hodnotu `false`, spustíte riziko, že neúmyslně odstraní nebo upraví záznamy v souběžných uživatelích. Viz [Upozornění: problém souběžnosti s ASP.NET 2,0 gridviews/DetailsView/formviews, které podporují úpravy a/nebo odstraňování a jejichž stav zobrazení je zakázán](http://scottonwriting.net/sowblog/archive/2006/10/03/163215.aspx) pro další informace.

## <a name="improving-theunitpriceformatting"></a>Vylepšení formátování`UnitPrice`

I když příklad prvku GridView zobrazený na obrázku 6 funguje, pole `UnitPrice` není vůbec zformátováno, což vede k tomu, že má za následek zobrazení ceny, které neobsahuje žádné symboly měny a má čtyři desetinná místa. Chcete-li použít formátování měny pro neupravitelné řádky, jednoduše nastavte vlastnost `DataFormatString` `UnitPrice` vlastnost BoundField na hodnotu `{0:c}` a její vlastnost `HtmlEncode` na `false`.

[![nastavte odpovídající vlastnosti DataFormatString a HtmlEncode.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image20.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image19.png)

**Obrázek 7**: odpovídajícím způsobem nastavte vlastnosti `UnitPrice``DataFormatString` a `HtmlEncode` ([kliknutím zobrazíte obrázek v plné velikosti](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image21.png)).

V důsledku této změny formát řádků, které nemůžete upravovat, ceníte jako měnu. upravený řádek však stále zobrazuje hodnotu bez symbolu měny a se čtyřmi desetinnými místy.

[![neupravitelné řádky jsou nyní formátovány jako hodnoty měny.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image23.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image22.png)

**Obrázek 8**: neupravitelné řádky jsou nyní formátovány jako hodnoty měny ([kliknutím zobrazíte obrázek v plné velikosti).](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image24.png)

Pokyny pro formátování zadané ve vlastnosti `DataFormatString` lze použít pro rozhraní úprav nastavením vlastnosti `ApplyFormatInEditMode` vlastnost BoundField na hodnotu `true` (výchozí hodnota je `false`). Nastavte tuto vlastnost na `true`chvíli počkejte.

[![nastavte vlastnost ApplyFormatInEditMode UnitPrice vlastnost BoundField na hodnotu true.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image26.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image25.png)

**Obrázek 9**: nastavte vlastnost `ApplyFormatInEditMode` `UnitPrice` vlastnost BoundField na hodnotu `true` ([kliknutím zobrazíte obrázek v plné velikosti).](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image27.png)

Tato změna znamená, že hodnota `UnitPrice` zobrazená na upravovaném řádku je také formátována jako měna.

[![hodnota UnitPrice upravovaného řádku je teď naformátovaná jako měna.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image29.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image28.png)

**Obrázek 10**: hodnota `UnitPrice` upravovaného řádku se teď formátuje jako měna ([kliknutím zobrazíte obrázek v plné velikosti).](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image30.png)

Aktualizace produktu pomocí symbolu měny v textovém poli, jako je $19,00, ale vyvolá `FormatException`. Když se GridView pokusí přiřadit uživatelsky zadané hodnoty do kolekce `UpdateParameters` ObjectDataSource, není schopen převést řetězec `UnitPrice` "$19,00" do `decimal` požadovaného parametrem (viz obrázek 11). Chcete-li tento problém vyřešit, můžeme vytvořit obslužnou rutinu události pro událost `RowUpdating` prvku GridView a nechat ji analyzovat uživatelem zadanou `UnitPrice` jako `decimal`ve formátu měny.

Událost `RowUpdating` prvku GridView přijímá jako svůj druhý parametr objekt typu [GridViewUpdateEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewupdateeventargs(VS.80).aspx), který obsahuje `NewValues` slovníku jako jednu z vlastností, která obsahuje uživatelem zadané hodnoty, které mají být přiřazeny do kolekce `UpdateParameters` prvku ObjectDataSource. Existující hodnotu `UnitPrice` v kolekci `NewValues` můžeme přepsat pomocí desítkové hodnoty, která je analyzovaná pomocí formátu měny s následujícími řádky kódu v obslužné rutině události `RowUpdating`:

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample4.cs)]

Pokud uživatel zadal `UnitPrice` hodnotu (například "$19,00"), bude tato hodnota přepsána hodnotou typu Decimal, vypočítanou [argumentem Decimal. Parse](https://msdn.microsoft.com/library/system.decimal.parse(VS.80).aspx)a analýzou hodnoty jako měny. Tato akce správně analyzuje desetinné číslo v případě symbolů měn, čárky, desetinných míst atd. a používá [výčty NumberStyles](https://msdn.microsoft.com/library/system.globalization.numberstyles(VS.80).aspx) v oboru názvů [System. Globalization](https://msdn.microsoft.com/library/abeh092z(VS.80).aspx) .

Obrázek 11 ukazuje problém způsobený symboly měny v uživatelsky dodávaném `UnitPrice`, spolu s tím, jak lze využít obslužnou rutinu události `RowUpdating` prvku GridView pro správné analyzování tohoto vstupu.

[![hodnota UnitPrice upravovaného řádku je teď naformátovaná jako měna.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image32.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image31.png)

**Obrázek 11**: hodnota `UnitPrice` upravovaného řádku se teď formátuje jako měna ([kliknutím zobrazíte obrázek v plné velikosti).](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image33.png)

## <a name="step-2-prohibitingnull-unitprices"></a>Krok 2: zákaz`NULL UnitPrices`

I když je databáze nakonfigurovaná tak, aby povolovala `NULL` hodnoty ve sloupci `UnitPrice` `Products` tabulky, můžeme uživatelům, kteří navštíví tuto konkrétní stránku, zabránit v zadání hodnoty `NULL` `UnitPrice`. To znamená, že pokud se uživateli nepodaří zadat `UnitPrice` hodnotu při úpravě řádku produktu, místo uložení výsledků do databáze chceme zobrazit zprávu informující o uživateli, který prostřednictvím této stránky musí mít všechny upravené produkty v ceně.

Objekt `GridViewUpdateEventArgs` předaný do obslužné rutiny události `RowUpdating` prvku GridView obsahuje vlastnost `Cancel`, která, pokud je nastavena na `true`, ukončí proces aktualizace. Nyní rozšíříme obslužnou rutinu `RowUpdating`, aby se nastavila `e.Cancel` na `true`, a zobrazila se zpráva s vysvětlením, proč je `NewValues` hodnota `UnitPrice` v `null`Collection.

Začněte přidáním webového ovládacího prvku popisek na stránku s názvem `MustProvideUnitPriceMessage`. Tento ovládací prvek popisek se zobrazí, pokud uživatel při aktualizaci produktu nezadá `UnitPrice`ovou hodnotu. Nastavte vlastnost `Text` popisku na hodnotu pro produkt musíte zadat cenu. Také jsem vytvořil novou třídu CSS v `Styles.css` s názvem `Warning` s následující definicí:

[!code-css[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample5.css)]

Nakonec nastavte vlastnost `CssClass` popisku na hodnotu `Warning`. V tomto okamžiku by měl Návrhář zobrazit varovnou zprávu červeně, tučně, kurzívou a velmi velkou velikostí písma nad prvek GridView, jak je znázorněno na obrázku 12.

[do prvku GridView bylo přidáno ![popisku.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image35.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image34.png)

**Obrázek 12**: popisek byl přidán nad prvek GridView ([kliknutím zobrazíte obrázek v plné velikosti](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image36.png)).

Ve výchozím nastavení by tento popisek měl být skrytý, proto nastavte jeho vlastnost `Visible` na `false` v obslužné rutině události `Page_Load`:

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample6.cs)]

Pokud se uživatel pokusí aktualizovat produkt bez zadání `UnitPrice`, chceme aktualizaci zrušit a zobrazit popisek upozornění. Rozšiřte obslužnou rutinu události `RowUpdating` prvku GridView následujícím způsobem:

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample7.cs)]

Pokud se uživatel pokusí uložit produkt bez zadání ceny, aktualizace se zruší a zobrazí se užitečná zpráva. I když databáze (a obchodní logika) umožňuje `NULL` `UnitPrice` s, tato konkrétní ASP.NET stránka ne.

[![uživatel nemůže ponechat prázdné pole UnitPrice.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image38.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image37.png)

**Obrázek 13**: uživatel nesmí opustit `UnitPrice` prázdné ([kliknutím zobrazíte obrázek v plné velikosti](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image39.png)).

Zatím jsme viděli, jak pomocí události `RowUpdating` prvku GridView programově změnit hodnoty parametrů přiřazené kolekci `UpdateParameters` ObjectDataSource a jak úplně zrušit proces aktualizace. Tyto koncepty přenesou ovládací prvky DetailsView a FormView a také platí pro vkládání a odstraňování.

Tyto úlohy lze také provést na úrovni ObjectDataSource prostřednictvím obslužných rutin událostí pro své `Inserting`, `Updating`a `Deleting` událostí. Tyto události se aktivují před tím, než se vyvolá přidružená metoda podkladového objektu, a nabídne poslední možnost, jak změnit kolekci vstupních parametrů, nebo zrušit operaci přímo. Obslužné rutiny událostí pro tyto tři události jsou předány objektu typu [ObjectDataSourceMethodEventArgs](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs(VS.80).aspx) , který má dvě vlastnosti zájmu:

- [Cancel](https://msdn.microsoft.com/library/system.componentmodel.canceleventargs.cancel(VS.80).aspx), pokud je nastavená na `true`, zruší prováděnou operaci.
- [Vstupní parametry](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasourcemethodeventargs.inputparameters(VS.80).aspx), což je kolekce `InsertParameters`, `UpdateParameters`nebo `DeleteParameters`, v závislosti na tom, zda je obslužná rutina události pro událost `Inserting`, `Updating`nebo `Deleting`

Chcete-li znázornit práci s hodnotami parametrů na úrovni ObjectDataSource, vložte do naší stránky prvek DetailsView, který umožňuje uživatelům přidat nový produkt. Tento prvek DetailsView bude sloužit k poskytnutí rozhraní pro rychlé přidání nového produktu do databáze. Pokud chcete zachovat konzistentní uživatelské rozhraní při přidávání nového produktu, umožněte uživateli, aby zadal jenom hodnoty pro pole `ProductName` a `UnitPrice`. Ve výchozím nastavení se hodnoty, které nejsou zadány v rozhraní vložení ovládacího prvku DetailsView, nastaví na hodnotu `NULL` databáze. Můžeme však použít událost `Inserting` ObjectDataSource k vložení různých výchozích hodnot, jak uvidíme krátce.

## <a name="step-3-providing-an-interface-to-add-new-products"></a>Krok 3: poskytnutí rozhraní pro přidání nových produktů

Přetáhněte prvek DetailsView z panelu nástrojů do návrháře nad prvkem GridView, vymažte jeho `Height` a `Width` vlastností a vytvořte jeho vazby na prvek ObjectDataSource, který je již přítomen na stránce. Tím se pro každé pole produktu přidá vlastnost BoundField nebo třídě CheckBoxField podporována. Vzhledem k tomu, že chceme pomocí tohoto prvku DetailsView přidat nové produkty, musíme z inteligentní značky zaškrtnout možnost Povolit vkládání; Nicméně neexistuje žádná taková možnost, protože `Insert()` metoda ObjectDataSource není namapována na metodu třídy `ProductsBLL` (odvolání tohoto mapování na hodnotu (žádné) při konfiguraci zdroje dat viz obrázek 3).

Chcete-li prvek ObjectDataSource nakonfigurovat, vyberte odkaz konfigurace zdroje dat z jeho inteligentní značky a spuštění průvodce. První obrazovka umožňuje změnit základní objekt, ke kterému je prvek ObjectDataSource svázán; Nechejte nastavenou na `ProductsBLL`. Na další obrazovce jsou uvedena mapování z metod prvku ObjectDataSource na základní objekt. I když explicitně uvádíme, že metody `Insert()` a `Delete()` by neměly být namapované na žádné metody, pokud přejdete na karty pro vložení a odstranění, uvidíte, že je zde mapování. Důvodem je, že metody `AddProduct` a `DeleteProduct` `ProductsBLL`používají atribut `DataObjectMethodAttribute` k označení toho, že jsou výchozími metodami pro `Insert()` a `Delete()`v uvedeném pořadí. Proto Průvodce ObjectDataSource při každém spuštění Průvodce vybere pouze v případě, že není explicitně zadána nějaká hodnota.

Ponechte `Insert()` metodu ukazující na metodu `AddProduct`, ale znovu nastavte rozevírací seznam odstranit kartu na (žádné).

[![nastavit rozevírací seznam na kartě Vložení na metodu AddProduct](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image41.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image40.png)

**Obrázek 14**: nastavte rozevírací seznam karty vložit na `AddProduct` metodu ([kliknutím zobrazíte obrázek v plné velikosti).](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image42.png)

[![nastavit rozevírací seznam na kartě odstranit na (žádné)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image44.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image43.png)

**Obrázek 15**: Nastavení rozevíracího seznamu na kartě odstranit na (žádné) ([kliknutím zobrazíte obrázek v plné velikosti](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image45.png))

Po provedení těchto změn bude deklarativní syntaxe ObjectDataSource rozbalena tak, aby zahrnovala kolekci `InsertParameters`, jak je znázorněno níže:

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample8.aspx)]

Opětovné spuštění průvodce znovu přidal vlastnost `OldValuesParameterFormatString`. Chvíli počkejte, než tuto vlastnost vymažete, nastavením výchozí hodnoty (`{0}`) nebo jejím odebráním z deklarativní syntaxe.

V prvku ObjectDataSource, který poskytuje možnosti vložení, inteligentní značka ovládacího prvku DetailsView nyní obsahuje zaškrtávací políčko Povolit vkládání; Vraťte se do návrháře a podívejte se na tuto možnost. Dále zredukovali ovládací prvek DetailsView tak, aby měl pouze dvě BoundFields-`ProductName` a `UnitPrice`-a CommandField. V tomto okamžiku by deklarativní syntaxe ovládacího prvku DetailsView vypadala takto:

[!code-aspx[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample9.aspx)]

Obrázek 16 ukazuje tuto stránku při prohlížení v prohlížeči v tomto okamžiku. Jak vidíte, DetailsView zobrazí název a cenu prvního produktu (Chai). To je ale rozhraní pro vložení, které poskytuje způsob, jak uživateli rychle přidat nový produkt do databáze.

[![prvek DetailsView je aktuálně vykreslen v režimu jen pro čtení.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image47.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image46.png)

**Obrázek 16**: element DetailsView je aktuálně vykreslen v režimu jen pro čtení ([kliknutím zobrazíte obrázek v plné velikosti).](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image48.png)

Aby bylo možné zobrazit prvek DetailsView v režimu vložení, musíme nastavit vlastnost `DefaultMode` na hodnotu `Inserting`. Tím se v režimu vkládání vykreslí prvek DetailsView při prvním navštívení a po vložení nového záznamu ho zachová. Jak ukazuje obrázek 17, například prvek DetailsView poskytuje rychlé rozhraní pro přidání nového záznamu.

[![ovládacího prvku DetailsView poskytuje rozhraní pro rychlé přidání nového produktu.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image50.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image49.png)

**Obrázek 17**: element DetailsView poskytuje rozhraní pro rychlé přidání nového produktu ([kliknutím zobrazíte obrázek v plné velikosti).](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image51.png)

Když uživatel zadá název produktu a cenu (například "Acme voda" a 1,99, jako na obrázku 17), a klikne na tlačítko Vložit, vystavení se provede a vloží se pracovní postup, který vyvolal nový záznam produktu přidaný do databáze. Prvek DetailsView udržuje své rozhraní pro vložení a prvek GridView je automaticky svázán se zdrojem dat, aby mohl zahrnout nový produkt, jak je znázorněno na obrázku 18.

![Produkt](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image52.png)

**Obrázek 18**: produkt "Acme voda" byl přidán do databáze.

I když v prvku GridView na obrázku 18 není zobrazený, pole produktu, které chybí z rozhraní DetailsView `CategoryID`, `SupplierID`, `QuantityPerUnit`a tak dále, jsou přiřazena `NULL` hodnoty databáze. Můžete to zobrazit provedením následujících kroků:

1. Přejít na Průzkumník serveru v aplikaci Visual Studio
2. Rozbalení uzlu databáze `NORTHWND.MDF`
3. Pravým tlačítkem myši klikněte na uzel `Products` databázová tabulka.
4. Vyberte možnost zobrazit data tabulky.

Zobrazí se seznam všech záznamů v `Products` tabulce. Jak ukazuje obrázek 19, všechny sloupce nového produktu, které jsou jiné než `ProductID`, `ProductName`a `UnitPrice` mají `NULL` hodnoty.

[![pole produktu, která nejsou k dispozici v ovládacím prvku DetailsView, jsou přiřazeny hodnoty NULL.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image54.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image53.png)

**Obrázek 19**: pole produktu, která nejsou k dispozici v ovládacím prvku DetailsView, jsou přiřazena `NULL` hodnoty ([kliknutím zobrazíte obrázek v plné velikosti).](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image55.png)

Pro jednu nebo více hodnot tohoto sloupce můžeme zadat výchozí hodnotu, která je jiná než `NULL`, protože `NULL` není nejlepší výchozí možností nebo protože sloupec databáze sám nepovoluje `NULL` s. K tomu můžeme programově nastavit hodnoty parametrů kolekce `InputParameters` ovládacího prvku DetailsView. Toto přiřazení lze provést buď v obslužné rutině události `ItemInserting` ovládacího prvku DetailsView nebo v události `Inserting` elementu ObjectDataSource. Vzhledem k tomu, že jsme se už seznámili s použitím událostí předběžného a post na úrovni webového ovládacího prvku dat, pojďme tento čas prozkoumat pomocí událostí ObjectDataSource.

## <a name="step-4-assigning-values-to-thecategoryidandsupplieridparameters"></a>Krok 4: přiřazení hodnot k parametrům`CategoryID`a`SupplierID`

Pro účely tohoto kurzu si představte, že pro naši aplikaci při přidávání nového produktu prostřednictvím tohoto rozhraní je potřeba přiřadit `CategoryID` a `SupplierID` hodnotu 1. Jak bylo zmíněno dříve, prvek ObjectDataSource má dvojici událostí před a po úrovni, které se aktivují během procesu změny dat. Když je vyvolána jeho `Insert()` metoda, prvek ObjectDataSource nejprve vyvolá událost `Inserting` a pak zavolá metodu, na kterou byla `Insert()` metoda namapována, a nakonec vyvolá událost `Inserted`. Obslužná rutina události `Inserting` poskytne nám poslední příležitost k vylepšení vstupních parametrů nebo zrušení operace.

> [!NOTE]
> V reálné aplikaci byste pravděpodobně chtěli dát uživateli možnost zadat kategorii a dodavatele, nebo by tuto hodnotu vybrali na základě některých kritérií nebo obchodní logiky (místo toho, abyste vybrali ID 1). Bez ohledu na tento příklad ukazuje, jak programově nastavit hodnotu vstupního parametru z události předběžné úrovně prvku ObjectDataSource.

Chvíli počkejte, než se vytvoří obslužná rutina události pro událost `Inserting` ObjectDataSource. Všimněte si, že druhý vstupní parametr obslužné rutiny události je objekt typu `ObjectDataSourceMethodEventArgs`, který má vlastnost pro přístup k kolekci Parameters (`InputParameters`) a vlastnost pro zrušení operace (`Cancel`).

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample10.cs)]

V tomto okamžiku vlastnost `InputParameters` obsahuje kolekci `InsertParameters` prvku ObjectDataSource s hodnotami přiřazenými z prvku DetailsView. Chcete-li změnit hodnotu jednoho z těchto parametrů, stačí použít: `e.InputParameters["paramName"] = value`. Proto chcete-li nastavit `CategoryID` a `SupplierID` na hodnotu 1, upravte `Inserting` obslužnou rutinu události tak, aby vypadala takto:

[!code-csharp[Main](examining-the-events-associated-with-inserting-updating-and-deleting-cs/samples/sample11.cs)]

Tentokrát při přidávání nového produktu (například Acme soda) se sloupce `CategoryID` a `SupplierID` nového produktu nastaví na hodnotu 1 (viz obrázek 20).

[![nových produktů teď mají hodnoty KódKategorie a KódDodavatele nastavené na 1.](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image57.png)](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image56.png)

**Obrázek 20**: nové produkty mají nyní své `CategoryID` a `SupplierID` hodnoty nastaveny na hodnotu 1 ([kliknutím zobrazíte obrázek v plné velikosti).](examining-the-events-associated-with-inserting-updating-and-deleting-cs/_static/image58.png)

## <a name="summary"></a>Souhrn

Během úprav, vkládání a odstraňování procesu může ovládací prvek data web i ObjectDataSource pokračovat prostřednictvím řady událostí před a po úrovni. V tomto kurzu jsme prozkoumali události na úrovni služby a zjistili jsme, jak je použít k přizpůsobení vstupních parametrů nebo k tomu, aby se operace změny dat zcela zrušila jak z ovládacího prvku data Control, tak z událostí ObjectDataSource. V dalším kurzu se podíváme na vytváření a používání obslužných rutin událostí pro události na úrovni post.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Jackie Goor a Liz Shulok. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](an-overview-of-inserting-updating-and-deleting-data-cs.md)
> [Další](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)

---
uid: web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-vb
title: Interakce stránky obsahu se stránkou předlohy (VB) | Microsoft Docs
author: rick-anderson
description: Prověřuje způsob volání metod, nastavení vlastností atd. stránky obsahu z kódu na stránce předlohy.
ms.author: riande
ms.date: 07/11/2008
ms.assetid: a6e2e1a0-c925-43e9-b711-1f178fdd72d7
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/interacting-with-the-content-page-from-the-master-page-vb
msc.type: authoredcontent
ms.openlocfilehash: 5367ad1b7f2fa11c635ad95754c9bcc1edcb6c1d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74615630"
---
# <a name="interacting-with-the-content-page-from-the-master-page-vb"></a>Interakce stránky předlohy se stránkou obsahu (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/1/8/4/184e24fa-fcc8-47fa-ac99-4b6a52d41e97/ASPNET_MasterPages_Tutorial_07_VB.zip) nebo [stažení PDF](https://download.microsoft.com/download/e/b/4/eb4abb10-c416-4ba4-9899-32577715b1bd/ASPNET_MasterPages_Tutorial_07_VB.pdf)

> Prověřuje způsob volání metod, nastavení vlastností atd. stránky obsahu z kódu na stránce předlohy.

## <a name="introduction"></a>Úvod

Předchozí kurz zkoumal, jak stránka obsahu programově spolupracuje se stránkou předlohy. Odvoláme, že jsme stránku předlohy aktualizovali tak, aby zahrnovala ovládací prvek GridView, který uvádí pět naposledy přidaných produktů. Pak jsme vytvořili stránku obsahu, ze které může uživatel přidat nový produkt. Po přidání nového produktu je nutné stránku obsahu, která je potřebná k tomu, aby stránka předlohy aktualizovala prvek GridView tak, aby obsahovala právě přidaný produkt. Tato funkce byla dosažena přidáním veřejné metody do stránky předlohy, která obnovila data vázaná na prvek GridView a následně vyvolá tuto metodu ze stránky obsahu.

Nejběžnější forma interakce obsahu a stránky předlohy pochází ze stránky obsahu. Je však možné, že stránka předlohy Rouse aktuální stránku obsahu na akci a tato funkce může být nutná, pokud stránka předlohy obsahuje prvky uživatelského rozhraní, které umožňují uživatelům upravovat data, která jsou také zobrazena na stránce obsahu. Zvažte stránku obsahu, která zobrazuje informace o produktech v ovládacím prvku GridView, a na stránce předlohy, která obsahuje ovládací prvek tlačítko, který po kliknutí zdvojnásobí ceny všech produktů. Podobně jako v předchozím kurzu je nutné prvek GridView aktualizovat po kliknutí na tlačítko dvojitá cena, aby se zobrazily nové ceny, ale v tomto scénáři je to hlavní stránka, která potřebuje, aby Rouse stránku obsahu na akci.

V tomto kurzu se seznámíte s tím, jak má hlavní stránka vyvolat funkce definované na stránce obsahu.

### <a name="instigating-programmatic-interaction-via-an-event-and-event-handlers"></a>Návod k programové interakci prostřednictvím obslužných rutin událostí a událostí

Vyvolání funkcí stránky obsahu ze stránky předlohy je náročnější než jiné. Vzhledem k tomu, že stránka obsahu má jedinou hlavní stránku, při vysvětlení programové interakce ze stránky obsahu víme, které veřejné metody a vlastnosti jsou v naší likvidaci. Stránka předlohy ale může mít mnoho různých stránek obsahu, z nichž každá má vlastní sadu vlastností a metod. Jak a potom můžeme napsat kód na stránce předlohy, aby se na stránce obsahu prováděla nějaká akce, když nevíte, jaká stránka obsahu bude vyvolána až do doby běhu?

Vezměte v úvahu webový ovládací prvek ASP.NET, jako je například ovládací prvek tlačítko. Ovládací prvek tlačítko se může zobrazit na jakémkoli počtu stránek ASP.NET a potřebuje mechanismus, pomocí kterého může upozorňovat na stránku, na kterou byl kliknuto. To se provádí pomocí *událostí*. Konkrétně ovládací prvek tlačítko při kliknutí vyvolá událost `Click`; Stránka ASP.NET, která obsahuje tlačítko, může volitelně reagovat na toto oznámení prostřednictvím *obslužné rutiny události*.

Stejný vzor se dá použít k tomu, aby se na stránkách obsahu spouštěla funkce triggeru hlavní stránky:

1. Přidejte událost do hlavní stránky.
2. Vyvolejte událost vždy, když stránka předlohy potřebuje komunikovat se stránkou obsahu. Například pokud hlavní stránka potřebuje upozornit na stránku obsahu, kterou uživatel zdvojnásobí ceny, událost se vyvolá ihned po zdvojnásobení cen.
3. V těchto stránkách obsahu, které potřebují provést určitou akci, vytvořte obslužnou rutinu události.

Tento zbytek kurzu implementuje příklad, jak je uvedeno v úvodu; konkrétně stránka obsahu obsahující seznam produktů v databázi a stránku předlohy, která obsahuje ovládací prvek tlačítko pro dvojnásobek cen.

## <a name="step-1-displaying-products-in-a-content-page"></a>Krok 1: zobrazení produktů na stránce obsahu

Naším prvním pořadím podnikání je vytvoření stránky obsahu, která obsahuje seznam produktů z databáze Northwind. (Do projektu jsme přidali databázi Northwind v předchozím kurzu, která [*spolupracuje se stránkou předlohy ze stránky obsahu*](interacting-with-the-master-page-from-the-content-page-vb.md).) Začněte přidáním nové stránky ASP.NET do složky `~/Admin` s názvem `Products.aspx`a ujistěte se, že jste ji navázali na `Site.master` hlavní stránku. Obrázek 1 ukazuje Průzkumník řešení po přidání této stránky na web.

[![přidat novou stránku ASP.NET do složky pro správu](interacting-with-the-content-page-from-the-master-page-vb/_static/image2.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image1.png)

**Obrázek 01**: Přidání nové stránky ASP.NET do složky `Admin` ([kliknutím zobrazíte obrázek v plné velikosti](interacting-with-the-content-page-from-the-master-page-vb/_static/image3.png))

[*V kurzu zadání názvu, meta značek a dalších hlaviček HTML v kurzu pro hlavní stránku*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-vb.md) se dá vytvořit vlastní třída základní stránky s názvem `BasePage`, která vygeneruje nadpis stránky, pokud není explicitně nastavený. Přejít na třídu kódu na pozadí `Products.aspx` stránky a nechat ji odvozovat z `BasePage` (místo z `System.Web.UI.Page`).

Nakonec aktualizujte soubor `Web.sitemap` tak, aby obsahoval položku pro tuto lekci. Přidejte následující kód pod `<siteMapNode>` v lekci interakce obsahu s stránkou předlohy:

[!code-xml[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample1.xml)]

Přidání tohoto `<siteMapNode>` elementu se projeví v seznamu lekcí (viz obrázek 5).

Vraťte se na `Products.aspx`. V ovládacím prvku obsah pro `MainContent`přidejte ovládací prvek GridView a pojmenujte ho `ProductsGrid`. Vytvořte vazby prvku GridView k novému ovládacímu prvku SqlDataSource s názvem `ProductsDataSource`.

[![svázání prvku GridView s novým ovládacím prvkem SqlDataSource](interacting-with-the-content-page-from-the-master-page-vb/_static/image5.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image4.png)

**Obrázek 02**: Svázání prvku GridView s novým ovládacím prvkem SqlDataSource ([kliknutím zobrazíte obrázek v plné velikosti](interacting-with-the-content-page-from-the-master-page-vb/_static/image6.png))

Nakonfigurujte Průvodce tak, aby používal databázi Northwind. Pokud jste v předchozím kurzu pracovali, měli byste už mít připojovací řetězec s názvem `NorthwindConnectionString` v `Web.config`. V rozevíracím seznamu vyberte tento připojovací řetězec, jak je znázorněno na obrázku 3.

[![konfigurace SqlDataSource pro použití databáze Northwind](interacting-with-the-content-page-from-the-master-page-vb/_static/image8.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image7.png)

**Obrázek 03**: Konfigurace SqlDataSource pro použití databáze Northwind ([kliknutím zobrazíte obrázek v plné velikosti](interacting-with-the-content-page-from-the-master-page-vb/_static/image9.png))

Dále zadejte příkaz `SELECT` ovládacího prvku zdroje dat výběrem tabulky Products z rozevíracího seznamu a vrácení `UnitPrice` sloupců `ProductName` a (viz obrázek 4). Klikněte na další a pak na Dokončit a dokončete Průvodce konfigurací zdroje dat.

[![vrátit pole NázevVýrobku a JednotkováCena z tabulky Products](interacting-with-the-content-page-from-the-master-page-vb/_static/image11.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image10.png)

**Obrázek 04**: vrácení polí `ProductName` a `UnitPrice` z tabulky `Products` ([kliknutím zobrazíte obrázek v plné velikosti](interacting-with-the-content-page-from-the-master-page-vb/_static/image12.png))

A je to! Po dokončení Průvodce přidá aplikace Visual Studio do prvku GridView dva BoundFieldsy, které zrcadlí dvě pole vrácená ovládacím prvkem SqlDataSource. Následuje označení ovládacích prvků GridView a SqlDataSource. Obrázek 5 zobrazuje výsledky při prohlížení v prohlížeči.

[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample2.aspx)]

[![každý produkt a jeho cena je uvedena v prvku GridView.](interacting-with-the-content-page-from-the-master-page-vb/_static/image14.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image13.png)

**Obrázek 05**: v prvku GridView je uveden každý produkt a jeho cena ([kliknutím zobrazíte obrázek v plné velikosti](interacting-with-the-content-page-from-the-master-page-vb/_static/image15.png)).

> [!NOTE]
> Klidně můžete vyčistit vzhled prvku GridView. Mezi návrhy patří formátování zobrazené hodnoty UnitPrice jako měny a použití barev a písem pozadí ke zlepšení vzhledu mřížky. Další informace o zobrazení a formátování dat v ASP.NET najdete v tématu [Working with data tutorial Series](../../data-access/index.md).

## <a name="step-2-adding-a-double-prices-button-to-the-master-page"></a>Krok 2: Přidání tlačítka pro dvojitou cenu do stránky předlohy

Naším dalším úkolem je přidat webový ovládací prvek tlačítko do hlavní stránky, který při kliknutí na něj pozastaví cenu všech produktů v databázi. Otevřete stránku předlohy `Site.master` a přetáhněte tlačítko ze sady nástrojů do návrháře a umístěte ho pod ovládací prvek `RecentProductsDataSource` SqlDataSource, který jsme přidali v předchozím kurzu. Nastavte vlastnost `ID` tlačítka na `DoublePrice` a jeho vlastnost `Text` na hodnotu "dvojité ceny produktů".

Dále přidejte ovládací prvek SqlDataSource do stránky předlohy a pojmenujte jej `DoublePricesDataSource`. Tato třída SqlDataSource se použije ke spuštění příkazu `UPDATE` ke zdvojnásobení všech cen. Konkrétně je potřeba nastavit jeho `ConnectionString` a `UpdateCommand` vlastnosti na příslušný připojovací řetězec a příkaz `UPDATE`. Pak musíme při kliknutí na tlačítko `DoublePrice` zavolat tuto metodu `Update` ovládacího prvku SqlDataSource. Chcete-li nastavit vlastnosti `ConnectionString` a `UpdateCommand`, vyberte ovládací prvek SqlDataSource a pak přejít na okno Vlastnosti. Vlastnost `ConnectionString` uvádí seznam připojovacích řetězců, které jsou již uloženy v `Web.config` v rozevíracím seznamu. Vyberte možnost `NorthwindConnectionString`, jak je znázorněno na obrázku 6.

[![nakonfigurovat SqlDataSource pro použití NorthwindConnectionString](interacting-with-the-content-page-from-the-master-page-vb/_static/image17.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image16.png)

**Obrázek 6**: Konfigurace SqlDataSource pro použití `NorthwindConnectionString` ([kliknutím zobrazíte obrázek v plné velikosti](interacting-with-the-content-page-from-the-master-page-vb/_static/image18.png))

Chcete-li nastavit vlastnost `UpdateCommand`, vyhledejte v okno Vlastnosti možnost UpdateQuery. Tato vlastnost, pokud je vybrána, zobrazí tlačítko se třemi tečkami. Kliknutím na toto tlačítko zobrazíte dialogové okno Editor příkazů a parametrů zobrazené na obrázku 7. Do textového pole dialogového okna zadejte následující příkaz `UPDATE`:

[!code-sql[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample3.sql)]

Při spuštění tohoto příkazu se hodnota `UnitPrice` pro každý záznam v tabulce `Products` zdvojnásobí.

[![nastavit vlastnost UpdateCommand třídy SqlDataSource](interacting-with-the-content-page-from-the-master-page-vb/_static/image20.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image19.png)

**Obrázek 07**: nastavení vlastnosti `UpdateCommand` třídy SqlDataSource ([kliknutím zobrazíte obrázek v plné velikosti](interacting-with-the-content-page-from-the-master-page-vb/_static/image21.png))

Po nastavení těchto vlastností by vaše tlačítko a deklarativní označení ovládacího prvku SqlDataSource měly vypadat podobně jako následující:

[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample4.aspx)]

Vše, co zůstává, je zavolat metodu `Update` při kliknutí na tlačítko `DoublePrice`. Vytvořte obslužnou rutinu události `Click` pro tlačítko `DoublePrice` a přidejte následující kód:

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample5.vb)]

Pokud chcete tuto funkci otestovat, navštivte stránku `~/Admin/Products.aspx`, kterou jsme vytvořili v kroku 1, a klikněte na tlačítko "ceny za dvojité produkty". Kliknutím na tlačítko dojde k postbacku a spustí se obslužná rutina události `Click` `DoublePrice`ho tlačítka, přičemž se zdvojnásobí ceny všech produktů. Stránka se pak znovu vykreslí a v prohlížeči se vrátí a znovu zobrazí kód. Prvek GridView na stránce obsahu však obsahuje stejné ceny jako před tím, než bylo kliknuto na tlačítko "ceny za dvojité produkty". Důvodem je skutečnost, že data zpočátku načtená v prvku GridView měla svůj stav uložený ve stavu zobrazení, takže se při postbackech znovu nenačte, pokud nevydá pokyn jinak. Pokud navštívíte jinou stránku a vrátíte se na stránku `~/Admin/Products.aspx` uvidíte aktualizované ceny.

## <a name="step-3-raising-an-event-when-the-prices-are-doubled"></a>Krok 3: vyvolání události při zdvojnásobení cen

Vzhledem k tomu, že prvek GridView na stránce `~/Admin/Products.aspx` přímo neodráží zdvojnásobení ceny, může uživatel pochopit, že nekliká na tlačítko "dvojité ceny za produkt" nebo že nepracoval. Můžou zkusit kliknout několikrát na tlačítko a znovu zdvojnásobit ceny a znovu. Aby bylo možné tuto situaci opravit, potřebujeme, aby se na stránce obsah zobrazovaly nové ceny ihned po jejich zdvojnásobení.

Jak je popsáno výše v tomto kurzu, musíme vyvolat událost na hlavní stránce vždy, když uživatel klikne na tlačítko `DoublePrice`. Událost je způsob, jak jednu třídu (vydavatel události) upozornit na jinou sadu dalších tříd (předplatitele událostí), ke které došlo něco zajímavého. V tomto příkladu je hlavní stránkou Vydavatel události; Tyto stránky obsahu, které vás zajímají při kliknutí na tlačítko `DoublePrice`, jsou předplatitelé.

Třída se přihlašuje k odběru události vytvořením *obslužné rutiny události*, což je metoda, která je spuštěna v reakci na vyvolanou událost. Vydavatel definuje události, které vyvolává, definováním *delegáta události*. Delegát události Určuje, jaké vstupní parametry musí obslužná rutina události přijmout. V .NET Framework delegáti událostí nevrací žádnou hodnotu a nepřijímají dva vstupní parametry:

- `Object`, který identifikuje zdroj události a
- Třída odvozená z `System.EventArgs`

Druhý parametr předaný obslužné rutině události může obsahovat další informace o události. I když základní `EventArgs` třída neprojde žádné informace, .NET Framework obsahuje několik tříd, které přesahují `EventArgs` a zahrnují další vlastnosti. Například instance `CommandEventArgs` je předána obslužným rutinám událostí, které reagují na událost `Command` a obsahuje dvě informativní vlastnosti: `CommandArgument` a `CommandName`.

> [!NOTE]
> Další informace o vytváření, vyvolávání a zpracování událostí naleznete v tématu [události a Delegáti](https://msdn.microsoft.com/library/17sde2xt.aspx) a [Delegáti událostí v jednoduché angličtině](http://www.codeproject.com/KB/cs/eventdelegates.aspx).

K definování události použijte následující syntaxi:

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample6.vb)]

Vzhledem k tomu, že potřebujeme upozornit stránku obsahu pouze v případě, že uživatel klikl na tlačítko `DoublePrice` a nemusíte předat žádné další Další informace, můžeme použít `EventHandler`delegáta události, který definuje obslužnou rutinu události, která přijímá jako druhý parametr objekt typu `System.EventArgs`. Chcete-li vytvořit událost na stránce předlohy, přidejte následující řádek kódu do třídy kódu na pozadí hlavní stránky:

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample7.vb)]

Výše uvedený kód přidá veřejnou událost do hlavní stránky s názvem `PricesDoubled`. Tuto událost teď musíte vyvolat po zdvojnásobení cen. Chcete-li vyvolat událost, použijte následující syntaxi:

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample8.vb)]

Kde *sender* a *EventArgs* jsou hodnoty, které chcete předat obslužné rutině události odběratele.

Aktualizujte obslužnou rutinu události `DoublePrice` `Click` s následujícím kódem:

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample9.vb)]

Stejně jako dříve se obslužná rutina události `Click` spustí voláním metody `Update` `DoublePricesDataSource` ovládacího prvku SqlDataSource pro dvojnásobek cen všech produktů. Následuje dva dodatky k obslužné rutině události. Nejprve se aktualizují data ovládacího prvku GridView `RecentProducts`. Tento prvek GridView byl přidán na stránku předlohy v předchozím kurzu a zobrazí pět naposledy přidaných produktů. Musíme tuto mřížku aktualizovat tak, aby se pro tyto pět produktů zobrazovaly přesně dvojnásobné ceny. Po tomto případě je vyvolána událost `PricesDoubled`. Odkaz na samotný hlavní stránku (`Me`) je odeslán obslužné rutině události jako zdroj události a prázdný objekt `EventArgs` je odeslán jako argumenty události.

## <a name="step-4-handling-the-event-in-the-content-page"></a>Krok 4: zpracování události na stránce obsahu

V tomto okamžiku stránka předlohy vyvolá událost `PricesDoubled` vždy, když se klikne na ovládací prvek tlačítko `DoublePrice`. Toto je ale jenom polovina výročí a pořád potřebujeme tuto událost v předplatiteli zpracovat. To zahrnuje dva kroky: vytvoření obslužné rutiny události a přidání kódu pro kabeláž události, aby při vyvolání události byla provedena obslužná rutina události.

Začněte vytvořením obslužné rutiny události s názvem `Master_PricesDoubled`. Vzhledem k tomu, jak jsme definovali událost `PricesDoubled` na stránce předlohy, dva vstupní parametry obslužné rutiny události musí být typu `Object` a `EventArgs`, v uvedeném pořadí. V obslužné rutině události zavolejte metodu `DataBind` prvku `ProductsGrid` GridView, aby se data znovu navázala na mřížku.

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample10.vb)]

Kód pro obslužnou rutinu události je dokončen, ale přesto jsme pro tuto obslužnou rutinu události nasdíleli událost `PricesDoubled` hlavní stránky. Předplatitel naplňuje událost obslužné rutině události prostřednictvím následující syntaxe:

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample11.vb)]

*Vydavatel* je odkaz na objekt, který nabízí událost *EventName*a *methodName* je název obslužné rutiny události definované v odběrateli.

Tento kód kabeláže události musí být proveden na první návštěvě stránky a následném postbacku a měl by nastat v bodě v životním cyklu stránky, který předchází době, kdy může být událost vyvolána. Vhodný čas pro přidání kódu pro zapojení do událostí je ve fázi předinicializace, která se v životním cyklu stránky velmi brzy vyskytuje.

Otevřete `~/Admin/Products.aspx` a vytvořte obslužnou rutinu události `Page_PreInit`:

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample12.vb)]

Aby bylo možné tento kód kabeláže dokončit, potřebujeme pro stránku předlohy ze stránky obsahu programový odkaz. Jak je uvedeno v předchozím kurzu, existují dva způsoby:

- Přetypováním vlastnosti `Page.Master` volného typu na příslušný typ stránky předlohy nebo
- Přidáním direktivy `@MasterType` na stránce `.aspx` a poté pomocí vlastnosti `Master` silného typu.

Pojďme použít druhý přístup. Do horní části deklarativního značení stránky přidejte následující direktivu `@MasterType`:

[!code-aspx[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample13.aspx)]

Poté do obslužné rutiny události `Page_PreInit` přidejte následující kód pro zapojení událostí:

[!code-vb[Main](interacting-with-the-content-page-from-the-master-page-vb/samples/sample14.vb)]

Když je tento kód na místě, prvek GridView na stránce obsahu se při každém kliknutí na tlačítko `DoublePrice` aktualizuje.

Obrázky 8 a 9 ilustrují toto chování. Obrázek 8 ukazuje stránku při prvním navštívení. Všimněte si, že cenové hodnoty v `RecentProducts` GridView (v levém sloupci stránky předlohy) a `ProductsGrid` GridView (na stránce obsahu). Obrázek 9 ukazuje stejnou obrazovku hned po kliknutí na tlačítko `DoublePrice`. Jak vidíte, nové ceny se okamžitě odrážejí v obou GridViews.

[![počátečních hodnot ceny](interacting-with-the-content-page-from-the-master-page-vb/_static/image23.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image22.png)

**Obrázek 08**: počáteční cenové hodnoty ([kliknutím zobrazíte obrázek v plné velikosti](interacting-with-the-content-page-from-the-master-page-vb/_static/image24.png))

[![se v prvku GridViewy zobrazí právě dvojité ceny](interacting-with-the-content-page-from-the-master-page-vb/_static/image26.png)](interacting-with-the-content-page-from-the-master-page-vb/_static/image25.png)

**Obrázek 09**: právě dvojnásobné ceny jsou zobrazeny v prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](interacting-with-the-content-page-from-the-master-page-vb/_static/image27.png)).

## <a name="summary"></a>Přehled

V ideálním případě jsou hlavní stránka a její stránky obsahu zcela oddělené od sebe a nevyžadují žádnou úroveň interakce. Pokud však máte stránku předlohy nebo stránku obsahu, která zobrazuje data, která lze upravovat ze stránky předlohy nebo obsahu stránky, může být nutné, aby stránka předlohy při změně dat zobrazila výstrahu stránky obsahu (nebo naopak), aby bylo možné zobrazení aktualizovat. V předchozím kurzu jsme viděli, jak stránku obsahu programově interagovat s hlavní stránkou. v tomto kurzu jsme se podívali na to, jak má hlavní stránka zahájit interakci.

Zatímco programové interakce mezi obsahem a stránkou předlohy může pocházet z obsahu nebo stránky předlohy, použitý vzor interakce závisí na původu. Rozdíly jsou způsobeny skutečností, že stránka obsahu má jedinou hlavní stránku, ale stránka předlohy může mít mnoho různých stránek obsahu. Místo toho, aby stránka předlohy přímo spolupracovala se stránkou obsahu, je lepší přístup k tomu, aby hlavní stránka vyvolala událost k signalizaci, že došlo k nějaké akci. Tyto stránky obsahu, které se týkají akce, mohou vytvářet obslužné rutiny událostí.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Přístup k datům v ASP.NET a jejich aktualizace](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [Události a Delegáti](https://msdn.microsoft.com/library/17sde2xt.aspx)
- [Předávání informací mezi obsahem a stránkami předlohy](http://aspnet.4guysfromrolla.com/articles/013107-1.aspx)
- [Práce s daty v kurzech ASP.NET](../../data-access/index.md)

### <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 3,5 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco). Scott se dá kontaktovat [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Vedoucí recenzent pro tento kurz byl takový Banerjee. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](interacting-with-the-master-page-from-the-content-page-vb.md)
> [Další](master-pages-and-asp-net-ajax-vb.md)

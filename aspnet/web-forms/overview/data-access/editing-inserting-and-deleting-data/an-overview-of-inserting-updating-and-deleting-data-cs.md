---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs
title: Přehled vložení, aktualizace a odstranění dat (C#) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se dozvíte, jak namapovat metody vložení (), Update () a Delete () prvku ObjectDataSource na metody tříd knihoven BLL a také jak konfigurovat...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: b651dc58-93c7-4f83-a74e-3b99f6d60848
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs
msc.type: authoredcontent
ms.openlocfilehash: e26b8e841f86272a158b0c09b62ab2790d01d191
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78592741"
---
# <a name="an-overview-of-inserting-updating-and-deleting-data-c"></a>Přehled vložení, aktualizace a odstranění dat (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_16_CS.exe) nebo [Stáhnout PDF](an-overview-of-inserting-updating-and-deleting-data-cs/_static/datatutorial16cs1.pdf)

> V tomto kurzu se dozvíte, jak namapovat metody vložení (), Update () a Delete () prvku ObjectDataSource na metody tříd knihoven BLL a jak nakonfigurovat ovládací prvky GridView, DetailsView a FormView pro zajištění možností změny dat.

## <a name="introduction"></a>Úvod

V posledních několika kurzech jsme prozkoumali, jak zobrazit data na stránce ASP.NET pomocí ovládacích prvků GridView, DetailsView a FormView. Tyto ovládací prvky jednoduše fungují s daty, která jsou jim dodána. Běžně tyto ovládací prvky přistupují k datům pomocí ovládacího prvku zdroje dat, jako je například ObjectDataSource. Zjistili jsme, jak prvek ObjectDataSource funguje jako proxy mezi stránkou ASP.NET a podkladovým datům. Když prvek GridView potřebuje zobrazit data, vyvolá jeho `Select()` metodu ObjectDataSource, která zase vyvolá metodu z naší vrstvy obchodní logiky (knihoven BLL), která volá metodu v příslušné vrstvě pro přístup k datům (DAL) TableAdapter, která zase odesílá dotaz `SELECT` do databáze Northwind.

Pokud jste v [našem prvním kurzu](../introduction/creating-a-data-access-layer-cs.md)naplnili objekty tableadaptery na dal, Visual Studio automaticky přidalo metody pro vkládání, aktualizaci a odstraňování dat z podkladové databázové tabulky. Kromě toho při [vytváření vrstvy obchodní logiky](../introduction/creating-a-business-logic-layer-cs.md) jsme navrhli metody v knihoven BLL, které se do těchto dat zavolaly, do těchto metod úprav dal.

Kromě jeho metody `Select()` má prvek ObjectDataSource také metody `Insert()`, `Update()`a `Delete()`. Podobně jako u metody `Select()` mohou být tyto tři metody namapovány na metody v podkladovém objektu. Pokud je nakonfigurována pro vložení, aktualizaci nebo odstranění dat, ovládací prvky GridView, DetailsView a FormView poskytují uživatelské rozhraní pro úpravu podkladových dat. Toto uživatelské rozhraní volá metody `Insert()`, `Update()`a `Delete()` prvku ObjectDataSource, které následně vyvolávají přidružené metody objektu (viz obrázek 1).

[![metody Insert (), Update () a Delete () prvku ObjectDataSource slouží jako proxy do knihoven BLL](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image2.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image1.png)

**Obrázek 1**: metody `Insert()`, `Update()`a `Delete()` prvku ObjectDataSource slouží jako proxy do knihoven BLL ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image3.png)

V tomto kurzu se dozvíte, jak namapovat metody `Insert()`, `Update()`a `Delete()` prvku ObjectDataSource na metody tříd v knihoven BLL, a jak nakonfigurovat ovládací prvky GridView, DetailsView a FormView pro poskytování možností změny dat.

## <a name="step-1-creating-the-insert-update-and-delete-tutorials-web-pages"></a>Krok 1: vytvoření webových stránek kurzy INSERT, Update a DELETE

Předtím, než začneme zkoumat, jak vkládat, aktualizovat a odstraňovat data, si nejdřív chvíli počkejte, než vytvoříte stránky ASP.NET v našem projektu webu, který budeme potřebovat pro tento kurz, a dalších. Začněte přidáním nové složky s názvem `EditInsertDelete`. Dále přidejte následující stránky ASP.NET do této složky a nezapomeňte přidružit jednotlivé stránky k `Site.master` hlavní stránce:

- `Default.aspx`
- `Basics.aspx`
- `DataModificationEvents.aspx`
- `ErrorHandling.aspx`
- `UIValidation.aspx`
- `CustomizedUI.aspx`
- `OptimisticConcurrency.aspx`
- `ConfirmationOnDelete.aspx`
- `UserLevelAccess.aspx`

![Přidání stránek ASP.NET pro kurzy týkající se úprav dat](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image4.png)

**Obrázek 2**: přidání stránek ASP.NET pro kurzy týkající se úprav dat

Podobně jako v ostatních složkách `Default.aspx` ve složce `EditInsertDelete` vypíše kurzy v části. Zajistěte, aby tato funkce poskytovala `SectionLevelTutorialListing.ascx` uživatelský ovládací prvek. Proto tento uživatelský ovládací prvek přidejte do `Default.aspx` tím, že ho přetáhnete z Průzkumník řešení na zobrazení Návrh stránky.

[![přidat uživatelský ovládací prvek SectionLevelTutorialListing. ascx do default. aspx](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image6.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image5.png)

**Obrázek 3**: Přidání uživatelského ovládacího prvku `SectionLevelTutorialListing.ascx` do `Default.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image7.png))

Nakonec přidejte stránky jako položky do souboru `Web.sitemap`. Konkrétně přidejte následující značku po přizpůsobeném formátování `<siteMapNode>`:

[!code-xml[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample1.xml)]

Po aktualizaci `Web.sitemap`chvíli počkejte, než se zobrazí web kurzy prostřednictvím prohlížeče. Nabídka na levé straně teď obsahuje položky pro kurzy pro úpravy, vkládání a odstraňování.

![Mapa webu teď obsahuje položky pro kurzy pro úpravy, vkládání a odstraňování.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image8.png)

**Obrázek 4**: Mapa webu teď obsahuje položky pro kurzy pro úpravy, vkládání a odstraňování.

## <a name="step-2-adding-and-configuring-the-objectdatasource-control"></a>Krok 2: Přidání a konfigurace ovládacího prvku ObjectDataSource

Vzhledem k tomu, že se ovládací prvek GridView, DetailsView a FormView liší v možnosti úprav dat a rozložení, Podívejme se každou jednotlivě. Místo toho, aby každý ovládací prvek používal vlastní prvek ObjectDataSource, ale pojďme pouze vytvořit jediný prvek ObjectDataSource, který mohou sdílet všechny tři ukázkové příklady.

Otevřete stránku `Basics.aspx`, přetáhněte prvek ObjectDataSource z panelu nástrojů do návrháře a klikněte na odkaz konfigurace zdroje dat z jeho inteligentní značky. Vzhledem k tomu, že `ProductsBLL` je jediná třída knihoven BLL, která poskytuje úpravy, vkládání a odstraňování metod, nakonfigurujte prvek ObjectDataSource, aby používal tuto třídu.

[![nakonfigurovat prvek ObjectDataSource tak, aby používal třídu ProductsBLL](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image10.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image9.png)

**Obrázek 5**: Konfigurace prvku ObjectDataSource, aby používal třídu `ProductsBLL` ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image11.png))

Na další obrazovce můžeme určit, jaké metody `ProductsBLL` třídy jsou namapovány na `Select()`, `Insert()`, `Update()`a `Delete()` prvku ObjectDataSource, a to tak, že vyberete příslušnou kartu a zvolíte metodu z rozevíracího seznamu. Obrázek 6, který by měl nyní vypadat dobře, mapuje metodu `Select()` prvku ObjectDataSource na metodu `GetProducts()` `ProductsBLL` třídy. Metody `Insert()`, `Update()`a `Delete()` lze nakonfigurovat výběrem příslušné karty ze seznamu podél horního okraje.

[![mají-li prvek ObjectDataSource vracet všechny produkty](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image13.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image12.png)

**Obrázek 6**: Chcete-li, aby prvek ObjectDataSource vrátil všechny produkty ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image14.png))

Na obrázcích 7, 8 a 9 se zobrazí karty aktualizace, vložení a odstranění prvku ObjectDataSource. Tyto karty nakonfigurujte tak, aby metody `Insert()`, `Update()`a `Delete()` vyvolaly `UpdateProduct`, `AddProduct`a `DeleteProduct` metody třídy `ProductsBLL`, v uvedeném pořadí.

[![namapovat metodu Update () prvku ObjectDataSource na UpdateProduct metodu třídy ProductBLL](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image16.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image15.png)

**Obrázek 7**: namapujte metodu `Update()` prvku ObjectDataSource na `UpdateProduct` metodu `ProductBLL` třídy ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image17.png)

[![namapovat metodu Insert () prvku ObjectDataSource na AddProduct metodu třídy ProductBLL](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image19.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image18.png)

**Obrázek 8**: namapujte metodu `Insert()` prvku ObjectDataSource na metodu Add `Product` `ProductBLL` třídy ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image20.png)

[![namapovat metodu DELETE () prvku ObjectDataSource na DeleteProduct metodu třídy ProductBLL](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image22.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image21.png)

**Obrázek 9**: namapujte metodu `Delete()` prvku ObjectDataSource na `DeleteProduct` metodu `ProductBLL` třídy ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image23.png)

Možná jste si všimli, že v rozevíracích seznamech na kartách aktualizace, vložení a odstranění již byly vybrány tyto metody. To je díky našemu využití `DataObjectMethodAttribute`, které upraví metody `ProductsBLL`. Například metoda DeleteProduct má následující signaturu:

[!code-csharp[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample2.cs)]

Atribut `DataObjectMethodAttribute` označuje účel jednotlivých metod, zda je určena pro výběr, vložení, aktualizaci nebo odstranění a zda se jedná o výchozí hodnotu. Pokud jste tyto atributy při vytváření tříd knihoven BLL vynechali, budete muset ručně vybrat metody z karet aktualizace, vložení a odstranění.

Po zajistěte, aby byly odpovídající metody `ProductsBLL` namapovány na `Insert()`, `Update()`a `Delete()` prvku ObjectDataSource, kliknutím na Dokončit dokončete průvodce.

## <a name="examining-the-objectdatasources-markup"></a>Zkoumání značek ObjectDataSource

Po nakonfigurování prvku ObjectDataSource prostřednictvím Průvodce přejdete do zobrazení zdroje a Prohlédněte si vygenerované deklarativní označení. Značka `<asp:ObjectDataSource>` určuje podkladový objekt a metody, které mají být vyvolány. Kromě toho existují `DeleteParameters`, `UpdateParameters`a `InsertParameters`, které jsou mapovány na vstupní parametry pro `AddProduct`, `UpdateProduct`a `DeleteProduct` metody třídy `ProductsBLL`:

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample3.aspx)]

Prvek ObjectDataSource obsahuje parametr pro každý vstupní parametr pro jeho přidružené metody, stejně jako seznam `SelectParameter` s je přítomen, pokud je prvek ObjectDataSource nakonfigurován pro volání metody Select, která očekává vstupní parametr (například `GetProductsByCategoryID(categoryID)`). Jak vidíte za chvilku, hodnoty pro tyto `DeleteParameters`, `UpdateParameters`a `InsertParameters` jsou nastaveny automaticky pomocí prvku GridView, DetailsView a FormView před vyvoláním metody `Insert()`, `Update()`nebo `Delete()` prvku ObjectDataSource. Tyto hodnoty se dají v budoucím kurzu nastavit i programově, protože budeme projednávat v budoucím kurzu.

Jedním z vedlejších účinků použití Průvodce pro konfiguraci na prvek ObjectDataSource je, že sada Visual Studio nastavuje [vlastnost OldValuesParameterFormatString na hodnotu](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.oldvaluesparameterformatstring(VS.80).aspx) `original_{0}`. Tato hodnota vlastnosti slouží k zahrnutí původních hodnot upravovaných dat a je užitečná ve dvou scénářích:

- Pokud při úpravách záznamu může uživatel změnit hodnotu primárního klíče. V takovém případě je nutné zadat jak novou hodnotu primárního klíče, tak původní hodnotu primárního klíče, aby se mohl najít záznam s původní hodnotou primárního klíče a odpovídajícím způsobem aktualizovat jeho hodnotu.
- Při použití optimistické souběžnosti. Optimistická souběžnost je technika, která zajistí, že dva souběžní uživatelé nepřepisují jiné změny, a je téma pro budoucí kurz.

Vlastnost `OldValuesParameterFormatString` označuje název vstupních parametrů v metodách aktualizace a odstranění podkladového objektu pro původní hodnoty. Tuto vlastnost a její účel podíváme podrobněji, když prozkoumáme optimistickou souběžnost. Dá se to ale udělat, protože naše knihoven BLL metody neočekávají původní hodnoty, takže je důležité, abyste tuto vlastnost odstranili. Ponecháním vlastnosti `OldValuesParameterFormatString` nastavenou na jinou hodnotu než výchozí (`{0}`) dojde k chybě, když se webový ovládací prvek data pokusí vyvolat `Update()` nebo `Delete()` metody prvku ObjectDataSource, protože prvek ObjectDataSource se pokusí předat jak v `UpdateParameters`, tak i `DeleteParameters`, tak i v parametrech původní hodnoty.

Pokud se to v tomto situaci vážně selhalo jasně, nedělejte si starosti, tato vlastnost a její nástroj se podíváme v budoucím kurzu. Prozatím je třeba určit, že se má tato deklarace vlastnosti odebrat zcela z deklarativní syntaxe, nebo nastavit hodnotu na výchozí hodnotu ({0}).

> [!NOTE]
> Pokud jednoduše vymažete hodnotu vlastnosti `OldValuesParameterFormatString` z okno Vlastnosti ve zobrazení Návrh, bude vlastnost stále existovat v deklarativní syntaxi, ale musí být nastavena na prázdný řetězec. To bohužel pořád vede ke stejnému problému, který je popsaný výše. Proto buď odeberte vlastnost zcela z deklarativní syntaxe nebo z okno Vlastnosti nastavte výchozí hodnotu `{0}`.

## <a name="step-3-adding-a-data-web-control-and-configuring-it-for-data-modification"></a>Krok 3: Přidání webového ovládacího prvku data a jeho konfigurace pro úpravu dat

Po přidání ovládacího prvku ObjectDataSource na stránku a nakonfigurovaném na stránce jsme připraveni přidat data webové ovládací prvky do stránky, jak budou zobrazovat data, a poskytnout tak pro koncové uživatele prostředky pro jeho úpravu. Podíváme se na prvky GridView, DetailsView a FormView samostatně, protože se tyto webové ovládací prvky dat liší v možnosti úprav dat a konfiguraci.

Jak je uvedeno ve zbývající části tohoto článku, přidávání velmi základních úprav, vkládání a odstraňování podpory prostřednictvím ovládacích prvků GridView, DetailsView a FormView je skutečně jednoduché jako kontrola několika zaškrtávacích políček. V reálném světě existuje mnoho odlišnostích a okrajových případů, které poskytují více funkcí, než stačí Ukázat a klikní. Tento kurz se ale zaměřuje výhradně na prokázání možností změny dat zjednodušený. V budoucích kurzech se budou posuzovat obavy, které se projeví v reálném čase.

## <a name="deleting-data-from-the-gridview"></a>Odstranění dat z prvku GridView.

Začněte přetažením prvku GridView z panelu nástrojů do návrháře. Dále navažte prvek ObjectDataSource na prvek GridView tím, že ho vyberete z rozevíracího seznamu v inteligentní značce prvku GridView. V tomto okamžiku deklarativní označení ovládacího prvku GridView bude:

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample4.aspx)]

Svázání prvku GridView s ovládacím prvkem ObjectDataSource prostřednictvím inteligentní značky má dvě výhody:

- BoundFields a CheckBoxFields jsou automaticky vytvořeny pro každé pole vrácené prvkem ObjectDataSource. Kromě toho jsou vlastnosti vlastnost BoundField a třídě CheckBoxField podporována nastaveny na základě metadat podkladového pole. Například pole `ProductID`, `CategoryName`a `SupplierName` jsou v `ProductsDataTable` označena jako jen pro čtení, která by proto neměla být při úpravách aktualizovatelná. Aby to bylo možné, tyto vlastnosti BoundFields ' [ReadOnly](https://msdn.microsoft.com/library/system.web.ui.webcontrols.boundfield.readonly(VS.80).aspx) jsou nastaveny na `true`.
- [Vlastnost DataKeyNames](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames(VS.80).aspx) je přiřazena k primárním klíčovým polím (y) podkladového objektu. To je nezbytné při použití prvku GridView pro úpravu nebo odstranění dat, protože tato vlastnost označuje pole (nebo sadu polí), které jedinečný identifikuje každý záznam. Další informace o vlastnosti `DataKeyNames` naleznete v tématu návrat k [hlavnímu a podrobnému odkazu pomocí selektivního hlavního prvku GridView s podrobnostmi o prvku detailview](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) kurzu.

I když prvek GridView může být svázán s prvkem ObjectDataSource prostřednictvím okno Vlastnosti nebo deklarativní syntaxe, je třeba ručně přidat odpovídající kód pro vlastnost BoundField a `DataKeyNames`.

Ovládací prvek GridView nabízí integrovanou podporu pro úpravy a odstranění na úrovni řádků. Konfigurace prvku GridView, aby podporovala odstranění, přidává sloupec odstranění tlačítek. Když koncový uživatel klikne na tlačítko Odstranit pro určitý řádek, postback provede a prvek GridView provede následující kroky:

1. Přiřadí se hodnoty `DeleteParameters` prvku ObjectDataSource.
2. Je vyvolána metoda `Delete()` prvku ObjectDataSource a odstraní se zadaný záznam.
3. Prvek GridView se znovu sváže s ovládacím prvkem ObjectDataSource vyvoláním jeho `Select()` metody.

Hodnoty přiřazené k `DeleteParameters` jsou hodnoty polí `DataKeyNames` pro řádek, na kterém bylo tlačítko Odstranit. Proto je důležité, aby byla správně nastavena vlastnost `DataKeyNames` prvku GridView. Pokud chybí, `DeleteParameters` se mu v kroku 1 přiřadí hodnota `null`, která zase nevytvoří žádné odstraněné záznamy v kroku 2.

> [!NOTE]
> Kolekce `DataKeys` je uložena ve stavu ovládacího prvku GridView s, což znamená, že hodnoty `DataKeys` budou zapamatovatný v rámci postbacku i v případě, že je stav zobrazení GridView. Je však velmi důležité, aby stav zobrazení zůstal povolen pro GridViews, které podporují úpravy nebo odstranění (výchozí chování). Pokud nastavíte vlastnost `EnableViewState` prvku GridView s na `false`, bude chování při úpravách a odstraňování fungovat pro jednoho uživatele, ale pokud existují souběžní uživatelé, kteří odstraňují data, existuje možnost, že tyto souběžní uživatelé mohou omylem odstranit nebo upravit záznamy, které nechtěly. Další informace najdete v tématu moje položka blogu, [Upozornění: problémy s Concurrency s ASP.NET 2,0 gridviews/DetailsView/formviews, které podporují úpravy a/nebo odstraňování a jejichž stav zobrazení je zakázaný](http://scottonwriting.net/sowblog/archive/2006/10/03/163215.aspx).

Stejné upozornění platí také pro ovládací prvek DetailsView a FormView.

Chcete-li přidat možnosti odstranění do prvku GridView, stačí přejít na jeho inteligentní značku a zaškrtnout políčko Povolit odstranění.

![Zaškrtněte políčko Povolit odstranění.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image24.png)

**Obrázek 10**: zaškrtněte políčko Povolit odstranění.

Zaškrtnutí políčka Povolit odstranění z inteligentní značky přidá do prvku GridView (CommandField). CommandField vykreslí sloupec v prvku GridView pomocí tlačítek pro provádění jednoho nebo více z následujících úkolů: výběr záznamu, úprava záznamu a odstranění záznamu. Dříve jsme viděli CommandField v akci s výběrem záznamů v seznamu [hlavní a podrobnosti pomocí selektivního hlavního prvku GridView s podrobným](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-cs.md) kurzem prvku detailview.

CommandField obsahuje řadu vlastností `ShowXButton`, které určují, jaké série tlačítek se zobrazí v CommandField. Zaškrtnutím políčka Povolit odstranění je CommandField, jehož vlastnost `ShowDeleteButton` je `true` přidána do kolekce sloupců prvku GridView.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample5.aspx)]

V tomto okamžiku se domníváte, že je, nebo ne, jsme hotovi s přidáním podpory odstranění do prvku GridView. Jak ukazuje obrázek 11, při návštěvě této stránky v prohlížeči se zobrazí sloupec s tlačítky pro odstranění.

[![CommandField přidá sloupec tlačítek pro odstranění.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image26.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image25.png)

**Obrázek 11**: CommandField přidá sloupec tlačítek pro odstranění ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image27.png)).

Pokud jste tento kurz sestavili od sebe na vlastní, při testování této stránky klikněte na tlačítko Odstranit a vyvolá se výjimka. Pokračujte ve čtení, abyste se dozvěděli, proč byly tyto výjimky vyvolány a jak je opravit.

> [!NOTE]
> Pokud sledujete pomocí stahování, které je přiloženo v tomto kurzu, již byly tyto problémy pro. Doporučujeme si ale přečíst si níže uvedené podrobnosti, které vám pomůžou identifikovat problémy, které mohou nastat, a vhodná alternativní řešení.

Pokud při pokusu o odstranění produktu dojde k výjimce, jejíž zpráva je podobná řetězci "*ObjectDataSource" ObjectDataSource1 nebylo možné najít neobecnou metodu "DeleteProduct", která má parametry: ProductID, původní\_ProductID*, "pravděpodobně jste zapomněli odebrat vlastnost `OldValuesParameterFormatString` z prvku ObjectDataSource. Při zadání vlastnosti `OldValuesParameterFormatString` se prvek ObjectDataSource pokusí předat vstupní parametry `productID` a `original_ProductID` do metody `DeleteProduct`. `DeleteProduct`však akceptuje pouze jeden vstupní parametr, a proto výjimku. Odebrání vlastnosti `OldValuesParameterFormatString` (nebo její nastavení na `{0}`) instruuje prvek ObjectDataSource, aby se nepokoušel předat původní vstupní parametr.

[![zajistěte, aby byla vlastnost OldValuesParameterFormatString vyčištěna.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image29.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image28.png)

**Obrázek 12**: Ujistěte se, že se vlastnost `OldValuesParameterFormatString` vymazala ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image30.png)

I když jste odebrali vlastnost `OldValuesParameterFormatString`, při pokusu o odstranění produktu s touto zprávou se stále zobrazí výjimka:*příkaz DELETE koliduje s omezením reference ' FK\_Order\_details\_Products*). Databáze Northwind obsahuje omezení cizího klíče mezi `Order Details` a `Products` tabulce, což znamená, že produkt nelze odstranit ze systému, pokud pro něj existuje jeden nebo více záznamů v tabulce `Order Details`. Vzhledem k tomu, že každý produkt v databázi Northwind obsahuje minimálně jeden záznam v `Order Details`, nemůžeme odstranit žádné produkty, dokud neodstraníme záznamy s přidruženými objednávkami daného produktu.

[![omezení cizího klíče zakáže odstraňování produktů.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image32.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image31.png)

**Obrázek 13**: omezení cizího klíče znemožňuje odstranění produktů ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image33.png)).

Pro náš kurz můžeme jednoduše odstranit všechny záznamy z `Order Details` tabulky. V reálné aplikaci budeme potřebovat:

- Mít další obrazovku pro správu informací o objednávkách.
- Rozšiřte metodu `DeleteProduct` tak, aby zahrnovala logiku pro odstranění podrobností o objednávce zadaného produktu.
- Upravte dotaz SQL používaný TableAdapter, aby zahrnoval odstranění podrobností o objednávce zadaného produktu.

Pojďme jenom odstranit všechny záznamy z tabulky `Order Details`, abyste obcházeli omezení cizího klíče. Přejděte na Průzkumník serveru v aplikaci Visual Studio, klikněte pravým tlačítkem na uzel `NORTHWND.MDF` a vyberte nový dotaz. Pak v okně dotazu spusťte následující příkaz SQL: `DELETE FROM [Order Details]`

[![odstranit všechny záznamy z tabulky Order details](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image35.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image34.png)

**Obrázek 14**: odstranění všech záznamů z `Order Details` tabulky ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image36.png))

Po vymazání `Order Details` tabulky klikněte na tlačítko Odstranit a produkt se odstraní bez chyby. Pokud při kliknutí na tlačítko Odstranit produkt neodstraníte, zkontrolujte, zda je vlastnost `DataKeyNames` prvku GridView nastavena na pole primárního klíče (`ProductID`).

> [!NOTE]
> Když kliknete na tlačítko Odstranit, vystavení se odstraní a záznam se odstraní. To může být nebezpečné, protože je snadné omylem kliknout na tlačítko Odstranit nesprávný řádek. V budoucím kurzu se dozvíte, jak přidat potvrzení na straně klienta při odstraňování záznamu.

## <a name="editing-data-with-the-gridview"></a>Úprava dat pomocí prvku GridView.

Kromě odstranění poskytuje ovládací prvek GridView také integrovanou podporu pro úpravy na úrovni řádků. Konfigurace prvku GridView pro podporu úprav přidá sloupec editačních tlačítek. V perspektivě koncového uživatele způsobí kliknutí na tlačítko pro úpravy řádku, aby se řádek stal upravitelný, přepnuli buňky do textových polí, které obsahují existující hodnoty, a nahradí tlačítko Upravit tlačítky aktualizovat a zrušit. Po provedení požadovaných změn může koncový uživatel kliknout na tlačítko Aktualizovat a potvrdit změny nebo tlačítko Storno, které je zahodí. V obou případech po kliknutí na aktualizovat nebo zrušit se prvek GridView vrátí do stavu před úpravou.

V naší perspektivě jako vývojář stránky, když koncový uživatel klikne na tlačítko pro úpravy pro určitý řádek, postback provede a prvek GridView provede následující kroky:

1. Vlastnost `EditItemIndex` prvku GridView je přiřazena k indexu řádku, jehož tlačítko pro úpravy bylo kliknuto.
2. Prvek GridView se znovu sváže s ovládacím prvkem ObjectDataSource vyvoláním jeho `Select()` metody.
3. Index řádku, který se shoduje s `EditItemIndex` je vykreslený v režimu úprav. V tomto režimu je tlačítko Upravit nahrazeno tlačítky aktualizovat a zrušit a BoundFields, jejichž vlastnosti `ReadOnly` jsou false (výchozí) se vykreslují jako webové ovládací prvky TextBox, jejichž `Text` vlastnosti jsou přiřazeny hodnotám datových polí.

V tomto okamžiku je kód vrácen do prohlížeče, což umožňuje koncovému uživateli provádět změny dat v řádku. Když uživatel klikne na tlačítko Aktualizovat, dojde k postbacku a prvek GridView provede následující kroky:

1. Hodnotám `UpdateParameters` prvku ObjectDataSource jsou přiřazeny hodnoty zadané koncovým uživatelem do rozhraní pro úpravy ovládacího prvku GridView.
2. Je vyvolána metoda `Update()` prvku ObjectDataSource, aktualizace zadaného záznamu
3. Prvek GridView se znovu sváže s ovládacím prvkem ObjectDataSource vyvoláním jeho `Select()` metody.

Hodnoty primárního klíče přiřazené `UpdateParameters` v kroku 1 pocházejí z hodnot zadaných ve vlastnosti `DataKeyNames`, zatímco hodnoty neprimárních klíčů pocházejí z textu ve webových ovládacích prvcích TextBox pro upravený řádek. Stejně jako při odstraňování je důležité, aby byla správně nastavena vlastnost `DataKeyNames` prvku GridView. Pokud chybí, hodnota `UpdateParameters` primární klíč se mu v kroku 1 přiřadí hodnota `null`, která zase nebude mít za následek aktualizované záznamy v kroku 2.

Funkčnost úprav se dá aktivovat pouhým zaškrtnutím políčka Povolit úpravy v inteligentní značce ovládacího prvku GridView.

![Zaškrtněte políčko Povolit úpravy.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image37.png)

**Obrázek 15**: zaškrtněte políčko Povolit úpravy.

Zaškrtnutím políčka Povolit úpravy přidáte CommandField (v případě potřeby) a nastavíte jeho vlastnost `ShowEditButton` na `true`. Jak jsme viděli dříve, CommandField obsahuje řadu vlastností `ShowXButton`, které určují, jaké série tlačítek se zobrazí v CommandField. Zaškrtnutím políčka Povolit úpravy přidáte do existujícího CommandField vlastnost `ShowEditButton`:

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample6.aspx)]

To je vše, co je přidání podpory základní pro úpravy. Jak Figure16 ukazuje, rozhraní pro úpravy je místo všech vlastnost BoundField, jejichž vlastnost `ReadOnly` nastavena na `false` (výchozí) je vykreslena jako textové pole. To zahrnuje pole jako `CategoryID` a `SupplierID`, což jsou klíče na jiné tabulky.

[![kliknutí na tlačítko Chai s úpravou řádku se zobrazí řádek v režimu úprav.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image39.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image38.png)

**Obrázek 16**: kliknutí na tlačítko Chai s úpravou zobrazí řádek v režimu úprav ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image40.png)

Kromě toho, že uživatelé žádají přímo o úpravu hodnot cizích klíčů, nemá rozhraní pro úpravu rozhraní následující možnosti:

- Pokud uživatel zadá `CategoryID` nebo `SupplierID`, které v databázi neexistují, `UPDATE` bude porušovat omezení cizího klíče, což způsobí, že se vyvolá výjimka.
- Rozhraní pro úpravy neobsahuje žádné ověřování. Pokud neposkytnete požadovanou hodnotu (například `ProductName`), nebo zadejte hodnotu řetězce, kde je očekávána číselná hodnota (například zadání "příliš velkého množství!" do textového pole `UnitPrice`) bude vyvolána výjimka. V budoucím kurzu se podíváme, jak přidat ověřovací ovládací prvky do uživatelského rozhraní pro úpravy.
- V současné době musí být *všechna* pole produktu, která nejsou jen pro čtení, obsažena v prvku GridView. Pokud jsme chtěli odebrat pole z prvku GridView, řekněme `UnitPrice`, když aktualizujete data, v prvku GridView nebude nastavena hodnota `UpdateParameters` `UnitPrice`, která by změnila `UnitPrice` záznamu databáze na `NULL` hodnotu. Podobně platí, že pokud je požadované pole, například `ProductName`, odebráno z prvku GridView, aktualizace selže se stejným "*sloupcem" NázevVýrobku "nepovoluje hodnoty null*". výše zmíněná výjimka je uvedena výše.
- Formátování rozhraní pro úpravy ponechá hodně požadovaných. `UnitPrice` se zobrazí se čtyřmi desetinnými místy. V ideálním případě by hodnoty `CategoryID` a `SupplierID` obsahovaly DropDownList, které uvádějí kategorie a dodavatele v systému.

Jedná se o všechny nedostatky, které budeme muset hned začít používat, ale budou řešeny v budoucích kurzech.

## <a name="inserting-editing-and-deleting-data-with-the-detailsview"></a>Vkládání, úpravy a odstraňování dat pomocí ovládacího prvku DetailsView

Jak jsme viděli v předchozích kurzech, ovládací prvek DetailsView zobrazuje jeden záznam v čase a, podobně jako v prvku GridView, umožňuje upravovat a odstraňovat aktuálně zobrazený záznam. Činnost koncového uživatele při úpravách a odstraňování položek z prvku DetailsView a pracovního postupu ze strany ASP.NET jsou stejné jako v prvku GridView. Tam, kde se ovládací prvek DetailsView liší od prvku GridView, je také k dispozici integrovaná podpora vkládání.

Chcete-li předvést možnosti změny dat prvku GridView, Začněte přidáním prvku DetailsView na stránku `Basics.aspx` nad existující prvek GridView a vytvořit jeho svázání s existujícím prvkem ObjectDataSource prostřednictvím inteligentní značky prvku DetailsView. Dále vymažte vlastnosti ovládacího prvku `Height` a `Width` a zaškrtněte možnost Povolit stránkování z inteligentní značky. Chcete-li povolit úpravy, vkládání a odstraňování podpory, stačí zaškrtnout políčka Povolit úpravy, povolit vkládání a povolit odstranění v inteligentní značce.

![Konfigurace ovládacího prvku DetailsView pro podporu úprav, vkládání a odstraňování](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image41.png)

**Obrázek 17**: konfigurace ovládacího prvku DetailsView pro podporu úprav, vkládání a odstraňování

Stejně jako u prvku GridView, přidání úpravy, vložení nebo odstranění podpory přidá do ovládacího prvku CommandField, jak ukazuje následující deklarativní syntaxe:

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample7.aspx)]

Všimněte si, že pro prvek DetailsView se CommandField na konci kolekce Columns zobrazuje ve výchozím nastavení. Vzhledem k tomu, že se pole ovládacího prvku DetailsView vykreslují jako řádky, CommandField se zobrazí jako řádek s tlačítky vložit, upravit a odstranit v dolní části ovládacího prvku DetailsView.

[![nakonfigurovat prvek DetailsView na podporu úprav, vkládání a odstraňování](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image43.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image42.png)

**Obrázek 18**: konfigurace ovládacího prvku DetailsView pro podporu úprav, vkládání a odstraňování ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image44.png))

Kliknutí na tlačítko Odstranit spustí stejnou posloupnost událostí jako u prvku GridView: postback; následováno ovládacím prvkem DetailsView naplněný `DeleteParameters` prvku ObjectDataSource na základě hodnot `DataKeyNames`; a jsou dokončeny voláním metody `Delete()` prvku ObjectDataSource, která ve skutečnosti odebere produkt z databáze. Úpravy v ovládacím prvku DetailsView také fungují způsobem, který se shoduje s prvku GridView.

Pro vložení se koncovému uživateli zobrazí nové tlačítko, které při kliknutí vykreslí ovládací prvek DetailsView v režimu vkládání. Pomocí příkazu "vložit režim" nové tlačítko je nahrazeno tlačítky vložit a zrušit a pouze ty BoundFields, jejichž vlastnost `InsertVisible` je nastavena na hodnotu `true` (výchozí) se zobrazí. Tato datová pole, která jsou identifikována jako pole s automatickým přírůstkem, jako je například `ProductID`, mají [vlastnost InsertVisible](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datacontrolfield.insertvisible(VS.80).aspx) nastavenou na `false` při vazbě prvku DetailsView ke zdroji dat pomocí inteligentní značky.

Když vytvoříte vazbu zdroje dat k prvku DetailsView prostřednictvím inteligentní značky, sada Visual Studio nastaví vlastnost `InsertVisible` tak, aby `false` pouze pro pole s automatickým přírůstkem. Pole jen pro čtení, například `CategoryName` a `SupplierName`, se zobrazí v uživatelském rozhraní "režim vkládání", pokud jejich vlastnost `InsertVisible` není explicitně nastavena na `false`. Chvíli počkejte, než se nastaví tato dvě pole `InsertVisible` vlastnosti na `false`, a to buď prostřednictvím deklarativní syntaxe ovládacího prvku DetailsView, nebo prostřednictvím odkazu upravit pole v inteligentní značce. Obrázek 19 ukazuje nastavení vlastností `InsertVisible` na `false` kliknutím na odkaz upravit pole.

[![Northwind Traders teď nabízí Acme čaj](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image46.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image45.png)

**Obrázek 19**: Northwind Traders teď nabízí Acme čaj ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image47.png)

Po nastavení vlastností `InsertVisible` zobrazte stránku `Basics.aspx` v prohlížeči a klikněte na tlačítko Nový. Obrázek 20 ukazuje prvek DetailsView při přidávání nového nápoje, Acme čaj na naši produktovou řadu.

[![Northwind Traders teď nabízí Acme čaj](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image49.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image48.png)

**Obrázek 20**: Northwind Traders teď nabízí Acme čaj ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image50.png)

Po zadání podrobností pro Acme čaj a kliknutí na tlačítko Vložit dojde k postbacku a nový záznam se přidá do tabulky `Products` databáze. Vzhledem k tomu, že tento prvek DetailsView uvádí produkty v pořadí, ve kterém v tabulce databáze existují, je nutné, aby se na poslední produkt zobrazila stránka, aby bylo možné nový produkt zobrazit.

[Podrobnosti ![pro Acme čaj](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image52.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image51.png)

**Obrázek 21**: podrobnosti pro Acme čaj ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image53.png))

> [!NOTE]
> [Vlastnost CurrentMode](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.currentmode(VS.80).aspx) prvku DetailsView indikuje zobrazované rozhraní a může mít jednu z následujících hodnot: `Edit`, `Insert`nebo `ReadOnly`. [Vlastnost DefaultMode](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.defaultmode(VS.80).aspx) označuje režim, po který se prvek DetailsView vrátí po dokončení úprav nebo vložení a je vhodný pro zobrazení prvku DetailsView, který je trvale v režimu úprav nebo vložení.

Bod a kliknutí na možnosti vkládání a úprav ovládacího prvku DetailsView mají stejná omezení jako v prvku GridView: uživatel musí zadat existující `CategoryID` a `SupplierID` hodnoty prostřednictvím textového pole. rozhraní nemá žádnou logiku ověřování. všechna pole produktu, která neumožňují `NULL` hodnoty nebo nemají výchozí hodnotu zadanou na úrovni databáze, musí být součástí rozhraní pro vkládání a tak dále.

Techniky, které jsme prověříme pro rozšíření a vylepšení rozhraní pro úpravy prvku GridView v budoucích článcích, se dají použít i pro úpravy a vkládání rozhraní ovládacího prvku DetailsView.

## <a name="using-the-formview-for-a-more-flexible-data-modification-user-interface"></a>Použití třídy FormView pro flexibilnější uživatelské rozhraní pro úpravu dat

Třída FormView nabízí integrovanou podporu pro vkládání, úpravu a odstraňování dat, ale vzhledem k tomu, že používá šablony namísto polí, není k dispozici žádné místo pro přidání BoundFields nebo CommandField, které jsou použity ovládacími prvky GridView a DetailsView k poskytnutí dat. rozhraní úprav. Místo toho je nutné, aby toto rozhraní webové ovládací prvky shromažďující vstup uživatele při přidávání nové položky nebo úpravách existujících položek spolu s tlačítky nová, upravit, odstranit, vložit, aktualizovat a Storno musely být ručně přidány do odpovídajících šablon. Aplikace Visual Studio naštěstí automaticky vytvoří potřebné rozhraní při vázání třídy FormView na zdroj dat v rozevíracím seznamu v jeho inteligentní značce.

Pro ilustraci těchto technik Začněte přidáním třídy FormView na `Basics.aspx` stránku a z inteligentní značky třídy FormView ji navažte na prvek ObjectDataSource, který je už vytvořený. Tím dojde k vygenerování `EditItemTemplate`, `InsertItemTemplate`a `ItemTemplate` pro ovládací prvky FormView with TextBox pro shromažďování webových ovládacích prvků vstupu a tlačítka pro nové tlačítka, úpravy, odstranění, vložení, aktualizaci a zrušení. Kromě toho vlastnost `DataKeyNames` třídy FormView je nastavena na pole primárního klíče (`ProductID`) objektu vráceného prvkem ObjectDataSource. Nakonec zaškrtněte v inteligentní značce FormView možnost Povolit stránkování.

Následující příklad ukazuje deklarativní označení pro `ItemTemplate` třídy FormView poté, co byla třída FormView svázána s prvkem ObjectDataSource. Ve výchozím nastavení je každé pole produktu, které není logické hodnoty, svázáno s vlastností `Text` webového ovládacího prvku popisek, zatímco každé pole s logickou hodnotou (`Discontinued`) je svázáno s vlastností `Checked` ovládacího prvku webového ovládacího prvku Disabled. Aby tlačítka nová, upravit a odstranit aktivovala určité chování FormView při kliknutí, je nutné, aby jejich `CommandName` hodnoty byly nastavené na `New`, `Edit`a `Delete`v uvedeném pořadí.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample8.aspx)]

Obrázek 22 zobrazuje `ItemTemplate` třídy FormView při prohlížení v prohlížeči. Každé pole produktu je v dolní části uvedeno v tlačítku nová, upravit a odstranit.

[![defaut FormView ItemTemplate zobrazuje každé pole produktu spolu s tlačítky nový, upravit a odstranit.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image55.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image54.png)

**Obrázek 22**: Defaut FormView `ItemTemplate` uvádí každé pole produktu spolu s tlačítky nový, upravit a odstranit ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image56.png)

Podobně jako u prvku GridView a DetailsView, kliknutí na tlačítko Odstranit nebo jakékoli tlačítko, LinkButton nebo obrázkové, jehož vlastnost `CommandName` je nastavena na hodnotu odstranit způsobí postback, naplní `DeleteParameters` ovládacího prvku ObjectDataSource na základě hodnoty `DataKeyNames` třídy FormView a vyvolá `Delete()` ovládacího prvku ObjectDataSource.

Po kliknutí na tlačítko pro úpravy dojde k provedení postbacku a data jsou znovu svázána s `EditItemTemplate`, což zodpovídá za vykreslování rozhraní pro úpravy. Toto rozhraní zahrnuje webové ovládací prvky pro úpravu dat spolu s tlačítky aktualizovat a zrušit. Výchozí `EditItemTemplate` vygenerované aplikací Visual Studio obsahuje popisek pro všechna pole s automatickým přírůstku (`ProductID`), textové pole pro každé nelogické hodnoty a zaškrtávací políčko pro každé pole logické hodnoty. Toto chování je velmi podobné automaticky generovanému BoundFields v ovládacích prvcích GridView a DetailsView.

> [!NOTE]
> Jedním z malých problémů s automatickou generací `EditItemTemplate` FormView je, že vykresluje webové ovládací prvky TextBox pro tato pole, která jsou jen pro čtení, jako je například `CategoryName` a `SupplierName`. Podíváme se, jak se to bude brzy vyhlížet.

Ovládací prvky TextBox v `EditItemTemplate` mají svou vlastnost `Text` svázány s hodnotou jejich odpovídajícího datového pole pomocí *obousměrné datové*sady. Obousměrná vazba, označená `<%# Bind("dataField") %>`, provádí datovou vazbu při vázání dat na šablonu a při naplňování parametrů ObjectDataSource pro vkládání nebo upravování záznamů. To znamená, že když uživatel klikne na tlačítko Upravit z `ItemTemplate`, vrátí metoda `Bind()` zadanou hodnotu datového pole. Poté, co uživatel provede změny a klikne na aktualizovat, jsou hodnoty odeslané zpět, které odpovídají datovým polím zadaným pomocí `Bind()`, použity pro `UpdateParameters`prvku ObjectDataSource. Případně jednosměrná vazba, označená `<%# Eval("dataField") %>`, načítá pouze hodnoty datových polí při vázání dat na šablonu a *nevrací uživatelem* zadané hodnoty do parametrů zdroje dat při zpětném volání.

Následující deklarativní kód ukazuje `EditItemTemplate`třídy FormView. Všimněte si, že metoda `Bind()` se používá v syntaxi DataBinding a že webové ovládací prvky tlačítka aktualizovat a Storno mají odpovídající nastavení vlastností `CommandName`.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample9.aspx)]

Náš `EditItemTemplate`, v tomto okamžiku způsobí, že bude vyvolána výjimka, pokud se ji pokusíme použít. Problémem je, že pole `CategoryName` a `SupplierName` se vykreslují jako webové ovládací prvky TextBox v `EditItemTemplate`. Musíme buď změnit tato textová pole na popisky, nebo je úplně odebrat. Pojďme je jednoduše odstranit úplně z `EditItemTemplate`.

Obrázek 23 ukazuje zobrazení FormView v prohlížeči po kliknutí na tlačítko Upravit pro příkaz Chai. Všimněte si, že pole `SupplierName` a `CategoryName` zobrazená v `ItemTemplate` již nejsou k dispozici, protože je právě odebrala z `EditItemTemplate`. Když kliknete na tlačítko Aktualizovat, třída FormView pokračuje přes stejné pořadí kroků jako ovládací prvky GridView a DetailsView.

[![ve výchozím nastavení, hodnota EditItemTemplate zobrazuje každé upravitelné pole produktu jako textové pole nebo zaškrtávací políčko.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image58.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image57.png)

**Obrázek 23**: ve výchozím nastavení `EditItemTemplate` zobrazuje každé upravitelné pole produktu jako textové pole nebo zaškrtávací políčko ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image59.png)

Po kliknutí na tlačítko Vložit `ItemTemplate` FormView dojde k vystavení. Žádná data však nejsou svázána se standardem FormView, protože probíhá přidávání nového záznamu. Rozhraní `InsertItemTemplate` zahrnuje webové ovládací prvky pro přidání nového záznamu spolu s tlačítky vložit a Storno. Výchozí `InsertItemTemplate` vygenerované v aplikaci Visual Studio obsahuje textové pole pro každé pole, které není typu Boolean, a zaškrtávací políčko pro každé pole s logickou hodnotou, podobně jako rozhraní `EditItemTemplate`generovaného automaticky. Ovládací prvky TextBox mají svou `Text` vlastnost vázané na hodnotu jejich odpovídajícího datového pole pomocí obousměrné datové sady.

Následující deklarativní kód ukazuje `InsertItemTemplate`třídy FormView. Všimněte si, že metoda `Bind()` se používá v syntaxi DataBinding a že webové ovládací prvky tlačítka Vložit a Storno mají odpovídající nastavení vlastností `CommandName`.

[!code-aspx[Main](an-overview-of-inserting-updating-and-deleting-data-cs/samples/sample10.aspx)]

Je k dispozici Subtlety s `InsertItemTemplate`automatické generace třídy FormView. Konkrétně jsou webové ovládací prvky TextBox vytvořeny i pro pole, která jsou jen pro čtení, například `CategoryName` a `SupplierName`. Podobně jako u `EditItemTemplate`musíme tato textová pole z `InsertItemTemplate`odebrat.

Obrázek 24 zobrazuje FormView v prohlížeči při přidávání nového produktu, Acme kávy. Všimněte si, že pole `SupplierName` a `CategoryName` zobrazená v `ItemTemplate` již nejsou přítomna, protože jsme je právě odstranili. Když kliknete na tlačítko Vložit, třída FormView pokračuje stejným způsobem jako v ovládacím prvku DetailsView a přidá nový záznam do tabulky `Products`. Obrázek 25 znázorňuje po vložení ve třídě FormView informace o pokusných produktech z kávy.

[![šablona InsertItemTemplate určuje rozhraní pro vložení třídy FormView.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image61.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image60.png)

**Obrázek 24**: `InsertItemTemplate` určuje rozhraní pro vložení třídy FormView ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image62.png)).

[![podrobnosti nového produktu, Acme kávy, se zobrazí ve třídě FormView.](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image64.png)](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image63.png)

**Obrázek 25**: podrobnosti o novém produktu, Acme kávy, se zobrazí ve třídě FormView ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-inserting-updating-and-deleting-data-cs/_static/image65.png)

Oddělením karet pro čtení, úpravy a vkládání rozhraní do tří samostatných šablon umožňuje třída FormView lepší kontrolu nad těmito rozhraními než ovládací prvek DetailsView a GridView.

> [!NOTE]
> Podobně jako prvek DetailsView, vlastnost `CurrentMode` třídy FormView indikuje zobrazené rozhraní a jeho vlastnost `DefaultMode` označuje režim, po kterém se třída FormView vrátí na po dokončení úpravy nebo vložení.

## <a name="summary"></a>Souhrn

V tomto kurzu jsme prozkoumali základy vkládání, úprav a odstraňování dat pomocí prvku GridView, DetailsView a FormView. Všechny tři z těchto ovládacích prvků poskytují určitou úroveň předdefinovaných možností změny dat, které lze využít bez nutnosti psát jediný řádek kódu na ASP.NET stránce díky webovým ovládacím prvkům data a prvku ObjectDataSource. Nicméně jednoduché a kliknutí na techniky vykreslují poměrně Frail a Naive uživatelské rozhraní pro úpravu dat. Abychom zajistili ověřování, vkládání programových hodnot, řádné zpracování výjimek, přizpůsobení uživatelského rozhraní a tak dále, budeme muset spoléhat na řadou reálných techniky, které se budou probrat v dalších několika kurzech.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Next](examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)

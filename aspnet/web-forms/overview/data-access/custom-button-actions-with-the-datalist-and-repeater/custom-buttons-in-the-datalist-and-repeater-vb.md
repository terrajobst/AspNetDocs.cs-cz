---
uid: web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-vb
title: Vlastní tlačítka v DataList a Repeater (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu sestavíme rozhraní, které pomocí opakovače vypíše kategorie v systému, a každou kategorii, která vám poskytne tlačítko pro zobrazení jeho přidružení...
ms.author: riande
ms.date: 11/13/2006
ms.assetid: 1afdb14d-6e49-4e1f-aead-2934730d472e
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions-with-the-datalist-and-repeater/custom-buttons-in-the-datalist-and-repeater-vb
msc.type: authoredcontent
ms.openlocfilehash: bc7e94e59226b739c2948434c1bfecb46b3d7856
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74607574"
---
# <a name="custom-buttons-in-the-datalist-and-repeater-vb"></a>Vlastní tlačítka v ovládacích prvcích DataList a Repeater (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_46_VB.exe) nebo [Stáhnout PDF](custom-buttons-in-the-datalist-and-repeater-vb/_static/datatutorial46vb1.pdf)

> V tomto kurzu sestavíme rozhraní, které pomocí opakovače vypíše kategorie v systému, a každou kategorii, která vám poskytne tlačítko pro zobrazení přidružených produktů pomocí ovládacího prvku BulletedList.

## <a name="introduction"></a>Úvod

V posledních sedmnáctch kurzech DataList a Repeater jsme vytvořili příklady jen pro čtení i příklady úprav a mazání. Pro usnadnění úprav a odstranění schopností v rámci prvku DataList jsme přidali tlačítka do prvku DataList s `ItemTemplate`, že při kliknutí způsobil postback a vyvolal událost DataList odpovídající vlastnosti Button s `CommandName`. Například přidání tlačítka do `ItemTemplate` s hodnotou `CommandName` vlastnosti Edit způsobí, že se `EditCommand` prvku DataList s aktivuje při postbacku; jeden s `CommandName` odstranit vyvolá `DeleteCommand`.

Kromě tlačítek upravit a odstranit mohou ovládací prvky DataList a Repeater také zahrnovat tlačítka, LinkButtons nebo ImageButtons, které při kliknutí vykonává vlastní logiku na straně serveru. V tomto kurzu sestavíme rozhraní, které používá Repeater k vypsání kategorií v systému. U každé kategorie bude opakovat zahrnutí tlačítka pro zobrazení přidružených produktů kategorie s použitím ovládacího prvku BulletedList (viz obrázek 1).

[![kliknutí na odkaz Zobrazit produkty zobrazí v seznamu s odrážkami produkty kategorie s.](custom-buttons-in-the-datalist-and-repeater-vb/_static/image2.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image1.png)

**Obrázek 1**: kliknutím na odkaz Zobrazit produkty zobrazíte v seznamu s odrážkami produkty kategorie s s odrážkami ([kliknutím zobrazíte obrázek v plné velikosti).](custom-buttons-in-the-datalist-and-repeater-vb/_static/image3.png)

## <a name="step-1-adding-the-custom-button-tutorial-web-pages"></a>Krok 1: Přidání webových stránek kurzu pro vlastní tlačítko

Předtím, než se podíváme na postup, jak přidat vlastní tlačítko, si nejdřív chvíli počkejte, než se vytvoří stránky ASP.NET v našem projektu webu, který budeme potřebovat pro tento kurz. Začněte přidáním nové složky s názvem `CustomButtonsDataListRepeater`. Dále přidejte do této složky následující dvě ASP.NET stránky a nezapomeňte přidružit jednotlivé stránky k hlavní stránce `Site.master`:

- `Default.aspx`
- `CustomButtons.aspx`

![Přidejte stránky ASP.NET pro vlastní kurzy související s tlačítky.](custom-buttons-in-the-datalist-and-repeater-vb/_static/image4.png)

**Obrázek 2**: přidejte stránky ASP.NET pro vlastní kurzy související s tlačítky.

Podobně jako v ostatních složkách `Default.aspx` ve složce `CustomButtonsDataListRepeater` vypíše kurzy v části. Zajistěte, aby tato funkce poskytovala `SectionLevelTutorialListing.ascx` uživatelský ovládací prvek. Přidejte tento uživatelský ovládací prvek do `Default.aspx` přetažením z Průzkumník řešení na zobrazení Návrh stránky.

[![přidat uživatelský ovládací prvek SectionLevelTutorialListing. ascx do default. aspx](custom-buttons-in-the-datalist-and-repeater-vb/_static/image6.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image5.png)

**Obrázek 3**: Přidání uživatelského ovládacího prvku `SectionLevelTutorialListing.ascx` do `Default.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](custom-buttons-in-the-datalist-and-repeater-vb/_static/image7.png))

Nakonec přidejte stránky jako položky do souboru `Web.sitemap`. Konkrétně přidejte následující značky po stránkování a řazení pomocí prvku DataList a Repeater `<siteMapNode>`:

[!code-xml[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample1.xml)]

Po aktualizaci `Web.sitemap`chvíli počkejte, než se zobrazí web kurzy prostřednictvím prohlížeče. Nabídka na levé straně teď obsahuje položky pro kurzy pro úpravy, vkládání a odstraňování.

![Mapa webu teď obsahuje položku pro úvodní kurz pro vlastní tlačítka.](custom-buttons-in-the-datalist-and-repeater-vb/_static/image8.png)

**Obrázek 4**: Mapa webu teď obsahuje položku kurzu pro vlastní tlačítka.

## <a name="step-2-adding-the-list-of-categories"></a>Krok 2: Přidání seznamu kategorií

Pro tento kurz musíme vytvořit Repeater, který obsahuje seznam všech kategorií společně s možnostmi Zobrazit produkty LinkButton, které po kliknutí zobrazí přidružené produkty kategorie s s odrážkami. Nejdříve vytvoříme jednoduchý opakovač, který obsahuje seznam kategorií v systému. Začněte tím, že otevřete stránku `CustomButtons.aspx` ve složce `CustomButtonsDataListRepeater`. Přetáhněte Repeater z panelu nástrojů do návrháře a nastavte jeho vlastnost `ID` na hodnotu `Categories`. Dále vytvořte nový ovládací prvek zdroje dat z inteligentní značky s opakováním. Konkrétně vytvořte nový ovládací prvek ObjectDataSource s názvem `CategoriesDataSource`, který vybere jeho data z metody `GetCategories()` `CategoriesBLL` třídy s.

[![nakonfigurovat prvek ObjectDataSource tak, aby používal metodu CategoriesBLL třídy s GetCategories ()](custom-buttons-in-the-datalist-and-repeater-vb/_static/image10.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image9.png)

**Obrázek 5**: Konfigurace prvku ObjectDataSource pro použití `GetCategories()` metody `CategoriesBLL` třídy s ([kliknutím zobrazíte obrázek v plné velikosti](custom-buttons-in-the-datalist-and-repeater-vb/_static/image11.png))

Na rozdíl od ovládacího prvku DataList, pro který Visual Studio vytvoří výchozí `ItemTemplate` založenou na zdroji dat, je nutné ručně definovat šablony opakování. Kromě toho musí být šablony Repeat vytvořeny a upravovány deklarativně (tj. neexistují žádné možnosti úprav šablon v rámci inteligentní značky Repeater).

V levém dolním rohu klikněte na kartu zdroj a přidejte `ItemTemplate`, která zobrazuje název kategorie v elementu `<h3>` a jeho popis v označení odstavce. Zahrňte `SeparatorTemplate`, který zobrazuje horizontální pravidlo (`<hr />`) mezi jednotlivými kategoriemi. Přidejte také LinkButton s vlastností `Text` nastavenou na Zobrazit produkty. Po dokončení těchto kroků by deklarativní označení stránky mělo vypadat takto:

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample2.aspx)]

Obrázek 6 zobrazuje stránku při prohlížení v prohlížeči. V seznamu jsou uvedeny všechny názvy a popisy kategorií. Tlačítko Zobrazit produkty po kliknutí způsobí postback, ale ještě neprovádí žádnou akci.

[![se zobrazí všechny kategorie s názvem a popis, společně s názvem Zobrazit produkty LinkButton.](custom-buttons-in-the-datalist-and-repeater-vb/_static/image13.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image12.png)

**Obrázek 6**: zobrazuje se každá kategorie s názvem a popisem spolu s pořadovým číslem "show Products" ([kliknutím zobrazíte obrázek v plné velikosti](custom-buttons-in-the-datalist-and-repeater-vb/_static/image14.png)).

## <a name="step-3-executing-server-side-logic-when-the-show-products-linkbutton-is-clicked"></a>Krok 3: provedení logiky na straně serveru při kliknutí na položku Zobrazit produkty na LinkButton

Kdykoli se klikne na tlačítko, LinkButton nebo obrázkové v rámci šablony v prvku DataList nebo Repeater, dojde k postbacku a událost DataList nebo Repeat `ItemCommand`. Kromě události `ItemCommand` může ovládací prvek DataList také vyvolat další, konkrétnější událost, pokud je vlastnost tlačítka s `CommandName` nastavena na jeden z rezervovaných řetězců (odstranit, upravit, zrušit, aktualizovat nebo vybrat), ale událost `ItemCommand` je *vždy* aktivována.

Když se na tlačítko klikne v rámci prvku DataList nebo Repeater, často musíme přesměrovat, na které tlačítko bylo kliknuto (v případě, že v ovládacím prvku může být více tlačítek, jako je tlačítko Upravit a odstranit), a případně některé další informace (například hodnota primárního klíče položky, jejíž tlačítko bylo kliknuto. Tlačítko, LinkButton a obrázkové poskytují dvě vlastnosti, jejichž hodnoty jsou předány do obslužné rutiny události `ItemCommand`:

- `CommandName` řetězec, který se obvykle používá k identifikaci každého tlačítka v šabloně
- `CommandArgument` běžně používá k uchování hodnoty některých datových polí, například hodnoty primárního klíče.

V tomto příkladu nastavte vlastnost `CommandName` LinkButton s na ShowProducts a vytvořte vazbu hodnoty primárního klíče v záznamu s `CategoryID` na vlastnost `CommandArgument` pomocí `CategoryArgument='<%# Eval("CategoryID") %>'`syntaxe datové vazby. Po zadání těchto dvou vlastností by deklarativní syntaxe LinkButton s měla vypadat takto:

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample3.aspx)]

Po kliknutí na tlačítko dojde k postbacku a událost DataList nebo Repeater `ItemCommand` je aktivována. Obslužné rutině události jsou předány tlačítko s `CommandName` a `CommandArgument` hodnoty.

Vytvořte obslužnou rutinu události pro událost Repeater s `ItemCommand` a poznamenejte si druhý parametr předaný do obslužné rutiny události (s názvem `e`). Tento druhý parametr je typu [`RepeaterCommandEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeatercommandeventargs.aspx) a má následující čtyři vlastnosti:

- `CommandArgument` hodnotu vlastnosti klikli na tlačítko s `CommandArgument`
- `CommandName` hodnotu vlastnosti tlačítko s `CommandName`
- `CommandSource` odkaz na ovládací prvek tlačítko, na který se kliklo
- `Item` odkaz na [`RepeaterItem`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeateritem.aspx) obsahující tlačítko, které bylo kliknuto; Každý záznam vázaný k tomuto OPAKOVAČI se projevuje jako `RepeaterItem`.

Vzhledem k tomu, že se vybrané kategorie `CategoryID` předávají prostřednictvím vlastnosti `CommandArgument`, můžeme získat sadu produktů přidružených k vybrané kategorii v obslužné rutině události `ItemCommand`. Tyto produkty pak mohou být vázány na ovládací prvek BulletedList v `ItemTemplate` (který jsme ještě přidali). To vše zůstává a pak je přidání BulletedList, odkazování v obslužné rutině události `ItemCommand` a vytvoření vazby na skupinu produktů pro vybranou kategorii, kterou provedeme v kroku 4.

> [!NOTE]
> Obslužná rutina události `ItemCommand` DataList s je předána objektu typu [`DataListCommandEventArgs`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistcommandeventargs.aspx), který nabízí stejné čtyři vlastnosti jako třída `RepeaterCommandEventArgs`.

## <a name="step-4-displaying-the-selected-category-s-products-in-a-bulleted-list"></a>Krok 4: zobrazení vybraných produktů kategorií s v seznamu s odrážkami

Vybrané produkty kategorie s se dají zobrazit v rámci `ItemTemplate` Repeater s použitím libovolného počtu ovládacích prvků. Mohli bychom přidat další vnořený Repeater, prvek DataList, DropDownList, prvek GridView a tak dále. Vzhledem k tomu, že chceme Zobrazit produkty jako seznam s odrážkami, použijeme ovládací prvek BulletedList. Návrat k deklarativnímu označení stránky `CustomButtons.aspx` přidejte ovládací prvek BulletedList do `ItemTemplate` za Zobrazit produkty LinkButton. Nastavte `ID` BulletedLists s `ProductsInCategory`. BulletedList zobrazí hodnotu datového pole zadaného prostřednictvím vlastnosti `DataTextField`; vzhledem k tomu, že tento ovládací prvek bude mít na něj vázané informace, nastavte vlastnost `DataTextField` na hodnotu `ProductName`.

[!code-aspx[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample4.aspx)]

V obslužné rutině události `ItemCommand` odkazujte na tento ovládací prvek pomocí `e.Item.FindControl("ProductsInCategory")` a vytvořte jeho vazby se sadou produktů přidružených k vybrané kategorii.

[!code-vb[Main](custom-buttons-in-the-datalist-and-repeater-vb/samples/sample5.vb)]

Před provedením jakékoli akce v obslužné rutině `ItemCommand` události je vhodné nejprve ověřit hodnotu příchozí `CommandName`. Vzhledem k tomu, že se obslužná rutina události `ItemCommand` aktivuje při kliknutí na tlačítko *, pokud je* v šabloně více tlačítek, použijte hodnotu `CommandName` a nerozlišuje, jakou akci chcete provést. Kontroluje se `CommandName` tady je moot, protože máme jenom jedno tlačítko, ale je dobrým zvykem formuláře. V dalším kroku se `CategoryID` z vybrané kategorie načte z vlastnosti `CommandArgument`. Pak se na ovládací prvek BulletedList v šabloně odkazuje a naváže na výsledky `ProductsBLL` třídy s `GetProductsByCategoryID(categoryID)` metody.

V předchozích kurzech, které používaly tlačítka v rámci prvku DataList, jako je například [Přehled úprav a odstranění dat v prvku DataList](../editing-and-deleting-data-through-the-datalist/an-overview-of-editing-and-deleting-data-in-the-datalist-vb.md), jsme určili hodnotu primárního klíče dané položky prostřednictvím kolekce `DataKeys`. I když tento přístup dobře funguje s ovládacím prvekem DataList, nemá tento ovládací prvek vlastnost `DataKeys`. Místo toho je nutné použít alternativní přístup pro zadání hodnoty primárního klíče, jako je například prostřednictvím vlastnosti `CommandArgument` tlačítka nebo přiřazením hodnoty primárního klíče k ovládacímu prvku skrytého popisku v rámci šablony a načtením jeho hodnoty zpět v obslužné rutině události `ItemCommand` pomocí `e.Item.FindControl("LabelID")`.

Po dokončení obslužné rutiny události `ItemCommand` chvíli počkejte, než otestujete tuto stránku v prohlížeči. Jak ukazuje obrázek 7, po kliknutí na odkaz Zobrazit produkty dojde k zpětnému odeslání a zobrazení produktů pro vybranou kategorii ve skupině BulletedList. Kromě toho si všimněte, že tyto informace o produktu zůstanou i v případě, že se kliknou na jiné kategorie s odkazy na produkty.

> [!NOTE]
> Chcete-li upravit chování této sestavy, je-li v seznamu uveden pouze jeden produkt kategorie s, jednoduše nastavte vlastnost `EnableViewState` ovládacího prvku BulletedList na hodnotu `False`.

[![se pro zobrazení produktů vybrané kategorie používá ovládací objekt BulletedList](custom-buttons-in-the-datalist-and-repeater-vb/_static/image16.png)](custom-buttons-in-the-datalist-and-repeater-vb/_static/image15.png)

**Obrázek 7**: pomocí ovládacího panelu se zobrazí produkty vybrané kategorie ([kliknutím zobrazíte obrázek v plné velikosti](custom-buttons-in-the-datalist-and-repeater-vb/_static/image17.png)).

## <a name="summary"></a>Přehled

Ovládací prvky DataList a Repeater mohou v rámci svých šablon obsahovat libovolný počet tlačítek, LinkButtons nebo ImageButtons. Taková tlačítka, když kliknete, způsobí postback a vyvolávají událost `ItemCommand`. Chcete-li přidružit vlastní akci na straně serveru k tlačítku, které je kliknuto, vytvořte obslužnou rutinu události pro událost `ItemCommand`. V této obslužné rutině události nejprve zkontrolujte hodnotu příchozí `CommandName` a určete, na které tlačítko bylo kliknuto. Další informace lze volitelně zadat prostřednictvím vlastnosti `CommandArgument` s tlačítkem.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Dennis Patterson. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](custom-buttons-in-the-datalist-and-repeater-cs.md)

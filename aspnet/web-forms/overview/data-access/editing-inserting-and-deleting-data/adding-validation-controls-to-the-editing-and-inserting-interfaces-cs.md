---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs
title: Přidání ověřovacích ovládacích prvků do rozhraní pro úpravy aC#vložení () | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se dozvíte, jak snadné je přidat ověřovací ovládací prvky do EditItemTemplate a šablona InsertItemTemplate webového ovládacího prvku, aby se zajistilo další...
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 2086cb1a-ab78-49ae-9c0b-03891c69776a
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs
msc.type: authoredcontent
ms.openlocfilehash: 110ee08f1d0707664ef6268f34ceab9da30a3e61
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74589755"
---
# <a name="adding-validation-controls-to-the-editing-and-inserting-interfaces-c"></a>Přidání validačních ovládacích prvků do rozhraní pro úpravy a vložení (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_19_CS.exe) nebo [Stáhnout PDF](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/datatutorial19cs1.pdf)

> V tomto kurzu se dozvíte, jak snadné je přidat ověřovací ovládací prvky do EditItemTemplate a šablona InsertItemTemplate webového ovládacího prvku dat a poskytnout tak další uživatelské rozhraní foolproof.

## <a name="introduction"></a>Úvod

Ovládací prvky GridView a DetailsView v ukázkách, které jsme prozkoumali v posledních třech kurzech, se všechny skládají z BoundFields a CheckBoxFields (typy polí automaticky přidané pomocí sady Visual Studio při vázání prvku GridView nebo DetailsView na zdroj dat. řízení prostřednictvím inteligentní značky). Při úpravách řádku v prvku GridView nebo DetailsView jsou tato BoundFields, která nejsou jen pro čtení, převedena do textových polí, ze kterých může koncový uživatel upravovat stávající data. Podobně při vložení nového záznamu do ovládacího prvku DetailsView se u těch BoundFields, jejichž vlastnost `InsertVisible` je nastavena na `true` (výchozí), vykreslují jako prázdná textová pole, do kterých může uživatel zadat hodnoty pole nového záznamu. Stejně tak CheckBoxFields, které jsou zakázány ve standardním rozhraní, jen pro čtení, se v rozhraních pro úpravy a vkládání převedou na povolená zaškrtávací políčka.

Zatímco výchozí rozhraní pro úpravy a vkládání pro vlastnost BoundField a třídě CheckBoxField podporována mohou být užitečná, rozhraní nemá žádné řazení ověřování. Pokud uživatel zadá omylem datovou položku, například vynechání pole `ProductName` nebo zadání neplatné hodnoty pro `UnitsInStock` (například-50), bude vyvolána výjimka z hloubky architektury aplikace. I když tato výjimka může být řádně zpracována tak, jak je znázorněno v [předchozím kurzu](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md), v ideálním případě úpravy nebo vložení uživatelského rozhraní by zahrnovala ovládací prvky ověřování, které uživateli brání v zadání takových neplatných dat na prvním místě.

Aby bylo možné poskytnout přizpůsobené úpravy nebo vložení rozhraní, je nutné nahradit vlastnost BoundField nebo třídě CheckBoxField podporována pomocí TemplateField. TemplateFields, které byly tématem diskuze v [ovládacím prvku GridView](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md) a používají templatefields v výukových kurzech [ovládacího prvku DetailsView](../custom-formatting/using-templatefields-in-the-detailsview-control-cs.md) , mohou sestávat z několika šablon definujících samostatná rozhraní pro různé stavy řádků. `ItemTemplate` TemplateField se používá k při vykreslování polí nebo řádků jen pro čtení v ovládacích prvcích DetailsView nebo GridView, zatímco `EditItemTemplate` a `InsertItemTemplate` označují rozhraní, která se mají použít pro režimy úprav a vkládání.

V tomto kurzu se dozvíte, jak snadné je přidat ověřovací ovládací prvky do `EditItemTemplate` TemplateField a `InsertItemTemplate` tak, aby poskytovalo další uživatelské rozhraní foolproof. Konkrétně tento kurz využívá příklad vytvořený při [zkoumání událostí souvisejících s vložením, aktualizací a odstraněním](examining-the-events-associated-with-inserting-updating-and-deleting-cs.md) kurzu a rozšiřuje rozhraní pro úpravy a vkládání, aby zahrnovala příslušné ověření.

## <a name="step-1-replicating-the-example-fromexamining-the-events-associated-with-inserting-updating-and-deletingexamining-the-events-associated-with-inserting-updating-and-deleting-csmd"></a>Krok 1: replikace příkladu z[zkoumání událostí spojených s vložením, aktualizací a odstraněním](examining-the-events-associated-with-inserting-updating-and-deleting-cs.md)

Při [zkoumání událostí spojených s vložením, aktualizací a odstraněním](examining-the-events-associated-with-inserting-updating-and-deleting-cs.md) kurzu jsme vytvořili stránku, která uvádí názvy a ceny produktů ve upravitelném prvku GridView. Kromě toho stránka obsahovala prvek DetailsView, jehož vlastnost `DefaultMode` byla nastavena na hodnotu `Insert`, takže vždy vykresluje v režimu vkládání. Od tohoto prvku DetailsView může uživatel zadat název a cenu nového produktu, kliknout na Vložit a přidat ho do systému (viz obrázek 1).

[![předchozí příklad umožňuje uživatelům přidávat nové produkty a upravovat stávající.](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image2.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image1.png)

**Obrázek 1**: předchozí příklad umožňuje uživatelům přidávat nové produkty a upravovat stávající ([kliknutím zobrazíte obrázek v plné velikosti).](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image3.png)

Naším cílem tohoto kurzu je rozšířit ovládací prvky DetailsView a GridView k poskytnutí ověřovacích ovládacích prvků. Konkrétně naše logika ověřování bude:

- Vyžadovat, aby se při vkládání nebo úpravách produktu zadal název
- Vyžaduje, aby byla při vkládání záznamu zadána cena. Při úpravách záznamu budeme stále vyžadovat cenu, ale použije programovou logiku v obslužné rutině `RowUpdating` ovládacího prvku GridView, která už je přítomna v předchozím kurzu.
- Ujistěte se, že zadaná hodnota ceny je platný formát měny.

Předtím, než se můžeme podívat na rozšíření předchozího příkladu, aby bylo ověřování zahrnuto, nejdřív je potřeba replikovat příklad ze stránky `DataModificationEvents.aspx` na stránku pro tento kurz, `UIValidation.aspx`. Aby bylo možné tento postup provést, je nutné zkopírovat jak deklarativní značku, tak i zdrojový kód stránky `DataModificationEvents.aspx`. Nejdřív zkopírujte přes deklarativní označení provedením následujících kroků:

1. Otevření stránky `DataModificationEvents.aspx` v aplikaci Visual Studio
2. Přejděte na deklarativní značku stránky (klikněte na tlačítko zdroj v dolní části stránky).
3. Zkopírujte text v rámci značek `<asp:Content>` a `</asp:Content>` (řádky 3 až 44), jak je znázorněno na obrázku 2.

[![zkopírovat text v &lt;ASP: ovládací prvek Content&gt;](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image5.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image4.png)

**Obrázek 2**: zkopírování textu v ovládacím prvku `<asp:Content>` ([kliknutím zobrazíte obrázek v plné velikosti](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image6.png))

1. Otevřete stránku `UIValidation.aspx`
2. Přejít na deklarativní značku stránky
3. Vložte text do ovládacího prvku `<asp:Content>`.

Chcete-li zkopírovat zdrojový kód, otevřete stránku `DataModificationEvents.aspx.cs` a zkopírujte pouze text *v rámci* `EditInsertDelete_DataModificationEvents` třídy. Zkopírujte tři obslužné rutiny události (`Page_Load`, `GridView1_RowUpdating`a `ObjectDataSource1_Inserting`), ale **nekopírujte** deklaraci třídy ani příkazy `using`. Vložte *zkopírovaný text do `EditInsertDelete_UIValidation` třídy v `UIValidation.aspx.cs`* .

Po přesunutí obsahu a kódu z `DataModificationEvents.aspx` na `UIValidation.aspx`chvíli počkejte, než se otestuje pokrok v prohlížeči. V každé z těchto dvou stránek byste měli vidět stejný výstup a vyzkoušet stejné funkce (pro snímek obrazovky `DataModificationEvents.aspx` v akci se podívejte zpátky na obrázek 1).

## <a name="step-2-converting-the-boundfields-into-templatefields"></a>Krok 2: převod BoundFields na TemplateFields

Chcete-li přidat ověřovací ovládací prvky do rozhraní pro úpravy a vkládání, je nutné převést BoundFields používané ovládacími prvky DetailsView a GridView na TemplateFields. Chcete-li to dosáhnout, klikněte na odkazy upravit sloupce a upravit pole v inteligentních značkách GridView a DetailsView. Vyberte jednotlivé BoundFields a klikněte na odkaz převést toto pole na TemplateField.

[![převést všechny BoundFields ovládacího prvku DetailsView a GridView na TemplateFields](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image8.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image7.png)

**Obrázek 3**: převeďte všechny BoundFields ovládacího prvku DetailsView a GridView na pole TemplateField ([kliknutím zobrazíte obrázek v plné velikosti).](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image9.png)

Převod vlastnost BoundField na TemplateField prostřednictvím dialogového okna pole vygeneruje TemplateField, který vykazuje stejné rozhraní jako jen pro čtení, úpravy a vkládání rozhraní jako vlastnost BoundField sám. Následující kód ukazuje deklarativní syntaxi pro pole `ProductName` v prvku DetailsView poté, co byl převeden na TemplateField:

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/samples/sample1.aspx)]

Všimněte si, že u tohoto TemplateField se automaticky vytvořily tři šablony `ItemTemplate`, `EditItemTemplate`a `InsertItemTemplate`. `ItemTemplate` zobrazuje jednu hodnotu datového pole (`ProductName`) pomocí webového ovládacího prvku popisek, zatímco `EditItemTemplate` a `InsertItemTemplate` prezentují hodnotu datového pole ve webovém ovládacím prvku TextBox, který přidruží datové pole k vlastnosti `Text` textového pole pomocí obousměrné datové vazby. Vzhledem k tomu, že při vkládání pouze používáme ovládací prvek DetailsView na této stránce, můžete `ItemTemplate` a `EditItemTemplate` odebrat ze dvou vlastností TemplateField, i když v nich nedochází k žádnému poškození.

Vzhledem k tomu, že prvek GridView nepodporuje integrované funkce vkládání prvku DetailsView, převod pole `ProductName` prvku GridView na hodnotu TemplateField má za následek pouze `ItemTemplate` a `EditItemTemplate`:

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/samples/sample2.aspx)]

Kliknutím na převést toto pole na TemplateField vytvoří Visual Studio TemplateField, jehož šablony napodobují uživatelské rozhraní převedené vlastnost BoundField. Můžete to ověřit tak, že navštívíte tuto stránku prostřednictvím prohlížeče. Zjistíte, že vzhled a chování vlastností TemplateField je stejné jako při použití BoundFields.

> [!NOTE]
> V případě potřeby můžete přizpůsobit rozhraní úprav v šablonách. Například můžeme chtít, aby textové pole v `UnitPrice`ech TemplateField bylo vykresleno jako menší textové pole, než `ProductName` TextBox. Chcete-li to dosáhnout, můžete nastavit vlastnost `Columns` textového pole na odpovídající hodnotu nebo zadat absolutní šířku prostřednictvím vlastnosti `Width`. V dalším kurzu se dozvíte, jak zcela přizpůsobit rozhraní pro úpravu tím, že nahradíte textové pole alternativním webovým ovládacím prvkem pro zadávání dat.

## <a name="step-3-adding-the-validation-controls-to-the-gridviewsedititemtemplate-s"></a>Krok 3: Přidání ovládacích prvků ověřování do`EditItemTemplate` prvku GridView

Při vytváření formulářů pro zadávání dat je důležité, aby uživatelé zadali všechna povinná pole a aby všechny zadané vstupy byly právní a správně formátované hodnoty. Aby bylo zajištěno, že vstupy uživatele jsou platné, ASP.NET poskytuje pět předdefinovaných ověřovacích ovládacích prvků, které jsou navrženy pro použití k ověření hodnoty jednoho vstupního ovládacího prvku:

- [RequiredFieldValidator](https://msdn.microsoft.com/library/5hbw267h(VS.80).aspx) zajistí, že byla zadána hodnota.
- [CompareValidator](https://msdn.microsoft.com/library/db330ayw(VS.80).aspx) ověří hodnotu pro jinou hodnotu webového ovládacího prvku nebo konstantní hodnotu nebo zajistí, že formát hodnoty je platný pro zadaný datový typ.
- [RangeValidator](https://msdn.microsoft.com/library/f70d09xt.aspx) zajišťuje, že hodnota spadá do rozsahu hodnot
- [RegularExpressionValidator](https://msdn.microsoft.com/library/eahwtc9e.aspx) ověří hodnotu oproti [regulárnímu výrazu](http://en.wikipedia.org/wiki/Regular_expression) .
- [CustomValidator](https://msdn.microsoft.com/library/9eee01cx(VS.80).aspx) ověří hodnotu podle vlastní uživatelem definované metody

Další informace o těchto pěti ovládacích prvcích najdete v [části ovládací prvky ověřování](https://quickstarts.asp.net/quickstartv20/aspnet/doc/ctrlref/validation/default.aspx) v [kurzech rychlý Start ASP.NET](https://asp.net/QuickStart/aspnet/).

Pro náš kurz budeme muset použít RequiredFieldValidator jak v ovládacím prvku DetailsView, tak v `ProductName` prvku GridView a v RequiredFieldValidator v prvku TemplateField `UnitPrice` DetailsView. Kromě toho bude nutné přidat CompareValidator do obou ovládacích prvků ' ovládací prvky ' `UnitPrice`, které zajistí, že zadaná cena má hodnotu větší než nebo rovna 0 a je prezentována v platném formátu měny.

> [!NOTE]
> Zatímco ASP.NET 1. x má stejné pět ověřovacích ovládacích prvků, ASP.NET 2,0 přináší řadu vylepšení, což je hlavní dvě Podpora skriptů na straně klienta pro jiné prohlížeče než Internet Explorer a možnost rozdělit ovládací prvky ověřování na stránku na skupiny ověření. Další informace o nových funkcích ovládacího prvku ověřování v 2,0 najdete v tématu přeASP.NET [ovládacích prvků ověřování v nástroji 2,0](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx).

Pojďme začít přidáním nezbytných ověřovacích ovládacích prvků do `EditItemTemplate` s v poli TemplateFields prvku GridView. Chcete-li to provést, klikněte na odkaz Upravit šablony z inteligentní značky GridView a zobrazte rozhraní pro úpravu šablony. Odtud můžete v rozevíracím seznamu vybrat šablonu, kterou chcete upravit. Vzhledem k tomu, že chceme rozšířit rozhraní pro úpravy, potřebujeme přidat ověřovací ovládací prvky do `ProductName` a `UnitPrice``EditItemTemplate` s.

[![potřebujeme, abychom rozšířili pole NázevVýrobku a JednotkováCena.](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image11.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image10.png)

**Obrázek 4**: musíme zvětšit `ProductName` a `UnitPrice``EditItemTemplate` s ([kliknutím zobrazíte obrázek v plné velikosti).](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image12.png)

V `EditItemTemplate``ProductName` přidejte RequiredFieldValidator přetažením z panelu nástrojů do rozhraní pro úpravu šablony a umístěte ho za textové pole.

[![přidat RequiredFieldValidator do NázevVýrobku EditItemTemplate](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image14.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image13.png)

**Obrázek 5**: Přidání RequiredFieldValidator do `EditItemTemplate` `ProductName` ([kliknutím zobrazíte obrázek v plné velikosti](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image15.png))

Všechny ovládací prvky ověřování fungují při ověřování vstupu jednoho ASP.NET webového ovládacího prvku. Proto musíme naznačit, že RequiredFieldValidator, který jste právě přidali, by měl ověřit proti textovému poli v `EditItemTemplate`; toho lze dosáhnout nastavením [vlastnosti ControlToValidate](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.controltovalidate(VS.80).aspx) ovládacího prvku ověřování na `ID` příslušného webového ovládacího prvku. Textové pole teď má nondescript `ID` `TextBox1`, ale pojďme ho změnit na něco vhodnějšího. Klikněte na textové pole v šabloně a potom v okno Vlastnosti změňte `ID` z `TextBox1` na `EditProductName`.

[![změnit ID textového pole na EditProductName](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image17.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image16.png)

**Obrázek 6**: Změňte `ID` textového pole na `EditProductName` ([kliknutím zobrazíte obrázek v plné velikosti](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image18.png)).

Dále nastavte vlastnost `ControlToValidate` RequiredFieldValidator na hodnotu `EditProductName`. Nakonec nastavte [vlastnost ErrorMessage](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.errormessage(VS.80).aspx) na hodnotu "je nutné zadat název produktu a [vlastnost Text](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.text(VS.80).aspx) na"\*". Hodnota vlastnosti `Text`, je-li k dispozici, je text, který je zobrazen ovládacím prvkem ověřování v případě, že se ověření nepovede. Hodnota vlastnosti `ErrorMessage`, která je povinná, je používána ovládacím prvkem ovládací souhrnu ověření; Pokud je hodnota vlastnosti `Text` vynechána, hodnota vlastnosti `ErrorMessage` je také text zobrazený ovládacím prvkem ověřování na neplatném vstupu.

Po nastavení těchto tří vlastností RequiredFieldValidator by měla obrazovka vypadat podobně jako na obrázku 7.

[![nastavit vlastnosti ControlToValidate, ErrorMessage a text RequiredFieldValidator](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image20.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image19.png)

**Obrázek 7**: nastavení vlastností `ControlToValidate`, `ErrorMessage`a `Text` ([kliknutím zobrazíte obrázek v plné velikosti](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image21.png))

Když se RequiredFieldValidator přidá do `EditItemTemplate``ProductName`, vše zůstává k přidání nezbytného ověření do `EditItemTemplate``UnitPrice`. Vzhledem k tomu, že jsme se rozhodli, že pro tuto stránku je `UnitPrice` při úpravách záznamu volitelný, nepotřebujeme přidat RequiredFieldValidator. Je ale potřeba přidat CompareValidator, aby se zajistilo, že `UnitPrice`, pokud je zadaný, je správně naformátovaná jako měna a je větší nebo rovna 0.

Než přidáme CompareValidator do `EditItemTemplate``UnitPrice`, pojďme nejdřív změnit ID webového ovládacího prvku TextBox z `TextBox2` na `EditUnitPrice`. Po provedení této změny přidejte CompareValidator, nastaví jeho vlastnost `ControlToValidate` na `EditUnitPrice`, jeho vlastnost `ErrorMessage` na hodnotu "cena musí být větší než nebo rovna nule a nesmí obsahovat symbol měny" a jeho `Text` vlastnost na hodnotu "\*".

Chcete-li určit, že hodnota `UnitPrice` musí být větší nebo rovna 0, nastavte [vlastnost operator](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.operator(VS.80).aspx) CompareValidator na hodnotu `GreaterThanEqual`, [Vlastnost ValueToCompare](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.valuetocompare(VS.80).aspx) na hodnotu "0" a jeho [vlastnost Type](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basecomparevalidator.type.aspx) na `Currency`. Následující deklarativní syntaxe ukazuje `UnitPrice` TemplateField `EditItemTemplate` poté, co byly provedeny tyto změny:

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/samples/sample3.aspx)]

Po provedení těchto změn otevřete stránku v prohlížeči. Pokud se pokusíte vynechat název nebo zadat neplatnou hodnotu ceny při úpravě produktu, zobrazí se vedle textového pole hvězdička. Jak ukazuje obrázek 8, hodnota ceny zahrnující symbol měny, jako je například $19,95, se považuje za neplatnou. CompareValidator `Currency` `Type` umožňuje oddělovačům číslic (například čárky nebo teček, v závislosti na nastavení jazykové verze) a úvodní znaménko plus nebo mínus, ale *nepovoluje symbol* měny. Toto chování může perplex uživatele, protože rozhraní pro úpravy aktuálně vykresluje `UnitPrice` pomocí formátu měny.

> [!NOTE]
> V *událostech souvisejících s vložením, aktualizací a odstraněním* kurzu nastavíme vlastnost `DataFormatString` vlastnost boundfield na `{0:c}`, aby se naformátoval jako měna. Kromě toho nastavíme vlastnost `ApplyFormatInEditMode` na hodnotu true, což způsobí, že rozhraní pro úpravy ovládacího prvku GridView naformátuje `UnitPrice` jako měnu. Při převodu vlastnost BoundField na TemplateField, Visual Studio poznamenalo tato nastavení a naformátují vlastnost `Text` TextBox jako měnu pomocí `<%# Bind("UnitPrice", "{0:c}") %>`syntaxe datové vazby.

[![se zobrazí hvězdička vedle textových polí s neplatným vstupem.](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image23.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image22.png)

**Obrázek 8**: u textových polí s neplatným vstupem se zobrazí hvězdička ([kliknutím zobrazíte obrázek v plné velikosti).](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image24.png)

I když ověřování funguje tak, jak je, uživatel musí při úpravách záznamu ručně odebrat symbol měny, což není přijatelné. K nápravě máme tři možnosti:

1. Nakonfigurujte `EditItemTemplate` tak, aby se hodnota `UnitPrice` neformátovala jako měna.
2. Umožní uživateli zadat symbol měny odebráním CompareValidator a jeho nahrazením RegularExpressionValidator, který správně kontroluje správně naformátovanou hodnotu měny. Problém je v tom, že regulární výraz pro ověření hodnoty měny není v podstatě a při pokusu o začlenění nastavení jazykové verze by vyžadoval psaní kódu.
3. Odeberte ovládací prvek ověřování zcela a v obslužné rutině události `RowUpdating` prvku GridView spoléhá na na na straně serveru logiku ověřování.

Pojďme pro toto cvičení použít možnost #1. V současné době je `UnitPrice` formátován jako měna z důvodu výrazu datové vazby pro textové pole v `EditItemTemplate`: `<%# Bind("UnitPrice", "{0:c}") %>`. Změňte příkaz BIND na `Bind("UnitPrice", "{0:n2}")`, který formátuje výsledek jako číslo se dvěma číslicemi přesnosti. To lze provést přímo prostřednictvím deklarativní syntaxe nebo kliknutím na odkaz Upravit datové vazby z `EditUnitPrice` textového pole v `EditItemTemplate` `UnitPrice` TemplateField (viz obrázek 9 a 10).

[![klikněte na odkaz Upravit datové vazby v textovém poli.](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image26.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image25.png)

**Obrázek 9**: klikněte na odkaz Upravit datové vazby v textovém poli ([kliknutím zobrazíte obrázek v plné velikosti](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image27.png)).

[![určení specifikátoru formátu v příkazu BIND](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image29.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image28.png)

**Obrázek 10**: určení specifikátoru formátu v příkazu `Bind` ([kliknutím zobrazíte obrázek v plné velikosti](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image30.png))

V důsledku této změny formátovaná cena v rozhraní pro úpravy zahrnuje čárky jako oddělovač skupin a tečku jako oddělovač desetinných míst, ale ponechá symbol měny.

> [!NOTE]
> `UnitPrice` `EditItemTemplate` neobsahuje RequiredFieldValidator, což umožňuje zpětné odeslání do následovat a zahájení logiky aktualizace. Nicméně obslužná rutina události `RowUpdating` zkopírovala z *zkoumání událostí přidružených k vložení, aktualizaci a odstranění* kurzu obsahuje programovou kontrolu, která zajišťuje, že `UnitPrice` k dispozici. Pokud chcete tuto logiku odebrat, nechte ji v tom, jak je, nebo přidejte RequiredFieldValidator do `EditItemTemplate``UnitPrice`.

## <a name="step-4-summarizing-data-entry-problems"></a>Krok 4: sumarizace problémů se zadáváním dat

Kromě pěti ovládacích prvků ověřování obsahuje ASP.NET [ovládací prvek ovládací souhrnu ověření](https://msdn.microsoft.com/library/f9h59855(VS.80).aspx), který zobrazuje `ErrorMessage` s těmito ověřovacími ovládacími prvky, které zjistila neplatná data. Tato souhrnná data lze zobrazit jako text na webové stránce nebo modálním objektem MessageBox na straně klienta. Pojďme tento kurz vylepšit, aby se zahrnuly funkce MessageBox na straně klienta, které shrnují jakékoli problémy s ověřením.

Chcete-li to provést, přetáhněte ovládací prvek ovládací souhrnu ověření z panelu nástrojů na Návrhář. Umístění ovládacího prvku ověřování není ve skutečnosti, protože ho nakonfigurujeme tak, aby zobrazoval pouze souhrn jako MessageBox. Po přidání ovládacího prvku nastavte jeho [vlastnost ShowSummary](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showsummary(VS.80).aspx) na `false` a jeho [vlastnost ShowMessageBox na hodnotu](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showmessagebox(VS.80).aspx) `true`. S tímto sčítáním jsou všechny chyby ověřování shrnuty ve MessageBox na straně klienta.

[![chyby ověřování jsou shrnuty ve MessageBox na straně klienta.](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image32.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image31.png)

**Obrázek 11**: Chyby ověřování jsou shrnuty v prvku MessageBox na straně klienta ([kliknutím zobrazíte obrázek v plné velikosti).](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image33.png)

## <a name="step-5-adding-the-validation-controls-to-the-detailsviewsinsertitemtemplate"></a>Krok 5: Přidání ovládacích prvků ověřování do`InsertItemTemplate` ovládacího prvku DetailsView

Vše, co pro tento kurz zbývá, je přidání ověřovacích ovládacích prvků do rozhraní pro vložení ovládacího prvku DetailsView. Proces přidání ovládacích prvků ověřování do šablon ovládacího prvku DetailsView je totožný s tím, že byl zkontrolován v kroku 3; Proto budeme Breeze prostřednictvím úkolu v tomto kroku. Stejně jako u `EditItemTemplate` prvků prvku GridView, doporučujeme, abyste přejmenovali `ID` s textovým polem nondescript `TextBox1` a `TextBox2` na `InsertProductName` a `InsertUnitPrice`.

Přidejte RequiredFieldValidator do `InsertItemTemplate``ProductName`. Nastavte `ControlToValidate` na `ID` textového pole v šabloně, vlastnost `Text` na "\*" a jeho vlastnost `ErrorMessage` na "je nutné zadat název produktu."

Vzhledem k tomu, že při přidávání nového záznamu se `UnitPrice` vyžaduje pro tuto stránku, přidejte do `InsertItemTemplate``UnitPrice`u RequiredFieldValidator a patřičně nastavte vlastnosti `ControlToValidate`, `Text`a `ErrorMessage`. Nakonec přidejte do `UnitPrice` `InsertItemTemplate` také CompareValidator a nakonfigurujte jeho `ControlToValidate`, `Text`, `ErrorMessage`, `Type`, `Operator`a `ValueToCompare` vlastnosti stejně jako v `UnitPrice`prvku GridView na `EditItemTemplate`CompareValidator.

Po přidání těchto ovládacích prvků ověřování nelze do systému přidat nový produkt, pokud jeho název není zadán nebo pokud je jeho cena záporná nebo má neplatně naformátované číslo.

[do rozhraní pro vkládání prvku DetailsView se přidala ![logika ověřování.](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image35.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image34.png)

**Obrázek 12**: logika ověřování byla přidána do rozhraní pro vkládání prvku DetailsView ([kliknutím zobrazíte obrázek v plné velikosti).](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image36.png)

## <a name="step-6-partitioning-the-validation-controls-into-validation-groups"></a>Krok 6: dělení ovládacích prvků ověřování do skupin ověřování

Naše stránka se skládá ze dvou logických různorodých sad ověřovacích ovládacích prvků: těch, které odpovídají rozhraní pro úpravy prvku GridView a těch, které odpovídají rozhraní pro vložení ovládacího prvku DetailsView. Ve výchozím nastavení, když dojde k postbacku, jsou kontrolovány *všechny* ovládací prvky ověřování na stránce. Při úpravách záznamu ale nechcete, aby se ovládací prvky pro ověřování rozhraní vloženého prvku vložily k ověření. Obrázek 13 znázorňuje naše aktuální dilematem, když uživatel upravuje produkt s dokonale přípustnými hodnotami. Kliknutím na aktualizovat dojde k chybě ověřování, protože hodnoty název a cena v rozhraní pro vložení jsou prázdné.

[![aktualizace produktu způsobí, že se ovládací prvky vložení rozhraní připraví na oheň.](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image38.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image37.png)

**Obrázek 13**: aktualizace produktu způsobí, že se ovládací prvky pro vložení rozhraní při ověřování aktivují ([kliknutím zobrazíte obrázek v plné velikosti).](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image39.png)

Ovládací prvky ověřování v ASP.NET 2,0 lze rozdělit do skupin ověřování prostřednictvím jejich vlastnosti `ValidationGroup`. Chcete-li přidružit sadu ověřovacích ovládacích prvků ve skupině, jednoduše nastavte jejich vlastnost `ValidationGroup` na stejnou hodnotu. Pro náš kurz nastavte vlastnosti `ValidationGroup` ovládacích prvků ověřování v prvcích TemplateField prvku GridView na `EditValidationControls` a `ValidationGroup` vlastnosti vlastností TemplateField prvku DetailsView na `InsertValidationControls`. Tyto změny lze provést přímo v deklarativním označení nebo prostřednictvím okno Vlastnosti při použití rozhraní Edit šablony návrháře.

Kromě ovládacích prvků ověřování obsahuje ovládací prvky s tlačítky a tlačítky v ASP.NET 2,0 také vlastnost `ValidationGroup`. Validátory ověřovací skupiny jsou kontrolovány pouze v případě, že je zpětně vyvoláno tlačítko se stejným nastavením vlastnosti `ValidationGroup`. Například pokud chcete, aby tlačítko pro vložení ovládacího prvku DetailsView aktivovalo `InsertValidationControls` skupinu ověření, potřebujeme nastavit vlastnost `ValidationGroup` CommandField na hodnotu `InsertValidationControls` (viz obrázek 14). Kromě toho nastavte vlastnost CommandField's `ValidationGroup` prvku GridView na hodnotu `EditValidationControls`.

[![nastavte vlastnost CommandField's Validation elementu ovládacího prvku na InsertValidationControls](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image41.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image40.png)

**Obrázek 14**: nastavte vlastnost CommandField's `ValidationGroup` ovládacího prvku na hodnotu `InsertValidationControls` ([kliknutím zobrazíte obrázek v plné velikosti).](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/_static/image42.png)

Po provedení těchto změn by pole TemplateField a CommandFields ovládacího prvku GridView a měly vypadat podobně jako následující:

Pole TemplateField a CommandField prvku DetailsView

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/samples/sample4.aspx)]

CommandField a TemplateField prvku GridView

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/samples/sample5.aspx)]

V tuto chvíli se ovládací prvky ověřování specifické pro úpravy aktivují jenom v případě, že se klikne na tlačítko pro aktualizaci prvku GridView a ovládací prvky pro ověření specifické pro vložení se aktivují jenom v případě, že se klikne na tlačítko pro vložení ovládacího prvku DetailsView, řešení problému zvýrazněného obrázek Tato změna ale ovládací souhrnu ověření ovládací prvek se už nezobrazuje při zadávání neplatných dat. Ovládací prvek ovládací souhrnu ověření obsahuje také vlastnost `ValidationGroup` a zobrazuje pouze souhrnné informace o těchto ovládacích prvcích ověřování v příslušné ověřovací skupině. Proto musíme na této stránce mít dva ovládací prvky ověřování, jednu pro skupinu ověření `InsertValidationControls` a jednu pro `EditValidationControls`.

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-cs/samples/sample6.aspx)]

Tento kurz se dokončí.

## <a name="summary"></a>Přehled

I když BoundFields může poskytovat rozhraní pro vložení i úpravy, rozhraní není přizpůsobitelné. Obecně chceme do rozhraní pro úpravy a vkládání přidat ovládací prvky ověřování, abyste zajistili, že uživatel zadá požadované vstupy do právního formátu. Aby bylo možné tento postup provést, je nutné převést BoundFields na TemplateFields a přidat ověřovací ovládací prvky do odpovídajících šablon. V tomto kurzu jsme rozšířili příklad z *hlediska událostí souvisejících s vložením, aktualizací a odstraněním* kurzu a přidáte ovládací prvky ověřování do rozhraní pro vložení ovládacího prvku DetailsView i do rozhraní pro úpravy ovládacího prvku GridView. Kromě toho jsme viděli, jak zobrazit souhrnné informace o ověřování pomocí ovládacího prvku ovládací souhrnu ověření a jak rozdělit ovládací prvky ověřování na stránku do různých ověřovacích skupin.

Jak jsme viděli v tomto kurzu, TemplateField umožňují rozšířit rozhraní pro úpravy a vkládání, aby zahrnovala ověřovací ovládací prvky. TemplateFields lze také rozšířit tak, aby zahrnovaly další vstupní webové ovládací prvky, které umožňují nahradit textové pole vhodnějším webovým ovládacím prvkem. V našem dalším kurzu se dozvíte, jak nahradit ovládací prvek TextBox ovládacím prvkem DropDownList vázaného na data, který je ideální při úpravách cizího klíče (například `CategoryID` nebo `SupplierID` v tabulce `Products`).

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Liz Shulok a Zack Novotný. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)
> [Další](customizing-the-data-modification-interface-cs.md)

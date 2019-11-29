---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-radio-buttons-vb
title: Přidání sloupce přepínacích tlačítek (VB) do prvku GridView | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se podíváme na postup přidání sloupce přepínačů do ovládacího prvku GridView, který uživateli poskytuje intuitivnější možnosti výběru jednoho řádku...
ms.author: riande
ms.date: 03/06/2007
ms.assetid: 2e31b60b-8723-4f14-b7ee-37859454dc3b
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-radio-buttons-vb
msc.type: authoredcontent
ms.openlocfilehash: ee67a4556c65d2c9570bf15b42fc3c8e5f555bda
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74593192"
---
# <a name="adding-a-gridview-column-of-radio-buttons-vb"></a>Přidání sloupce přepínačů do ovládacího prvku GridView (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_51_VB.exe) nebo [Stáhnout PDF](adding-a-gridview-column-of-radio-buttons-vb/_static/datatutorial51vb1.pdf)

> V tomto kurzu se podíváme na postup přidání sloupce přepínačů do ovládacího prvku GridView, který uživateli poskytuje intuitivnější možnosti výběru jednoho řádku prvku GridView.

## <a name="introduction"></a>Úvod

Ovládací prvek GridView nabízí skvělou sadu integrovaných funkcí. Obsahuje řadu různých polí pro zobrazení textu, obrázků, hypertextových odkazů a tlačítek. Podporuje šablony pro další přizpůsobení. Pomocí několika kliknutí myši je možné vytvořit prvek GridView, kde lze jednotlivé řádky vybrat pomocí tlačítka, nebo povolit možnosti úprav nebo odstranění. Navzdory spoustu poskytovaných funkcí často dochází k situaci, kdy bude potřeba přidat další nepodporované funkce. V tomto kurzu a dalších dvou jsme prozkoumali, jak vylepšit funkčnost prvku GridView s tím, aby zahrnovalo další funkce.

Tento kurz a další krok se zaměřuje na vylepšení procesu výběru řádků. Jak bylo zkontrolováno v [hlavní/podrobné pomocí selektivního hlavního prvku GridView s podrobnostmi prvku detailview](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md), můžeme přidat CommandField do prvku GridView, který obsahuje tlačítko pro výběr. Po kliknutí na něj postback nachází a vlastnost GridView s `SelectedIndex` je aktualizována na index řádku, jehož tlačítko vybrat bylo kliknuto. V seznamu [a podrobnostech pomocí selektivního hlavního prvku GridView s podrobným](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md) kurzem prvku detailview jsme viděli, jak tuto funkci použít k zobrazení podrobností pro vybraný řádek GridView.

Zatímco tlačítko vybrat funguje v mnoha situacích, nemusí fungovat i pro ostatní. Místo použití tlačítka se pro výběr obvykle používají dva další prvky uživatelského rozhraní: přepínač a zaškrtávací políčko. Ovládací prvek GridView můžeme rozšířit tak, aby místo tlačítka pro výběr obsahoval každý řádek přepínač nebo zaškrtávací políčko. Ve scénářích, kdy uživatel může vybrat pouze jeden ze záznamů GridView, může být přepínač upřednostňován přes tlačítko vybrat. V situacích, kdy může uživatel vybrat více záznamů, jako je například webová e-mailová aplikace, kde může uživatel chtít vybrat více zpráv, aby bylo možné odstranit zaškrtávací políčko, nabízí funkce, které nejsou k dispozici na tlačítku pro výběr nebo na přepínači. uživatelská rozhraní.

V tomto kurzu se podíváme na postup přidání sloupce přepínačů do prvku GridView. Kurz pokračování zkoumá použití zaškrtávacích políček.

## <a name="step-1-creating-the-enhancing-the-gridview-web-pages"></a>Krok 1: Vytvoření rozšíření webových stránek GridView

Předtím, než začneme s rozšířením prvku GridView, aby zahrnovalo sloupec přepínačů, je nejdříve potřeba chvíli vytvořit ASP.NET stránky v našem projektu webu, který budeme potřebovat pro tento kurz a další dva. Začněte přidáním nové složky s názvem `EnhancedGridView`. Dále přidejte následující stránky ASP.NET do této složky a nezapomeňte přidružit jednotlivé stránky k `Site.master` hlavní stránce:

- `Default.aspx`
- `RadioButtonField.aspx`
- `CheckBoxField.aspx`
- `InsertThroughFooter.aspx`

![Přidání stránek ASP.NET pro kurzy týkající se SqlDataSource](adding-a-gridview-column-of-radio-buttons-vb/_static/image1.gif)

**Obrázek 1**: přidání stránek ASP.NET pro kurzy týkající se SqlDataSource

Podobně jako v ostatních složkách `Default.aspx` ve složce `EnhancedGridView` vypíše kurzy v části. Zajistěte, aby tato funkce poskytovala `SectionLevelTutorialListing.ascx` uživatelský ovládací prvek. Proto tento uživatelský ovládací prvek přidejte do `Default.aspx` tím, že ho přetáhnete z Průzkumník řešení na zobrazení Návrh stránky.

[![přidat uživatelský ovládací prvek SectionLevelTutorialListing. ascx do default. aspx](adding-a-gridview-column-of-radio-buttons-vb/_static/image2.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image1.png)

**Obrázek 2**: Přidání uživatelského ovládacího prvku `SectionLevelTutorialListing.ascx` do `Default.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-radio-buttons-vb/_static/image2.png))

Nakonec tyto čtyři stránky přidejte jako položky do souboru `Web.sitemap`. Konkrétně přidejte následující značku po použití ovládacího prvku SqlDataSource `<siteMapNode>`:

[!code-xml[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample1.xml)]

Po aktualizaci `Web.sitemap`chvíli počkejte, než se zobrazí web kurzy prostřednictvím prohlížeče. Nabídka na levé straně teď obsahuje položky pro kurzy pro úpravy, vkládání a odstraňování.

![Mapa webu teď obsahuje položky pro rozšíření kurzů GridView.](adding-a-gridview-column-of-radio-buttons-vb/_static/image3.gif)

**Obrázek 3**: Mapa webu teď obsahuje položky pro rozšíření kurzů GridView.

## <a name="step-2-displaying-the-suppliers-in-a-gridview"></a>Krok 2: zobrazení dodavatelů v prvku GridView

V tomto kurzu vytvoříme prvek GridView, který zobrazí seznam dodavatelů z USA, přičemž každý řádek prvku GridView, který poskytuje přepínač. Po výběru dodavatele pomocí přepínače může uživatel zobrazit produkty dodavatele kliknutím na tlačítko. I když tato úloha může být zdravá, existuje mnoho odlišností, které by to mělo obzvlášť obtížné. Než se pustíme do těchto odlišností, pojďme nejdřív načíst GridView, který uvádí seznam dodavatelů.

Začněte tím, že otevřete stránku `RadioButtonField.aspx` ve složce `EnhancedGridView` přetažením prvku GridView z panelu nástrojů do návrháře. Nastavte `ID` prvku GridView s `Suppliers` a ze své inteligentní značky vyberte možnost vytvořit nový zdroj dat. Konkrétně vytvořte prvek ObjectDataSource s názvem `SuppliersDataSource`, který načte jeho data z objektu `SuppliersBLL`.

[![vytvořit nový prvek ObjectDataSource s názvem SuppliersDataSource](adding-a-gridview-column-of-radio-buttons-vb/_static/image4.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image3.png)

**Obrázek 4**: vytvoření nového prvku ObjectDataSource s názvem `SuppliersDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-radio-buttons-vb/_static/image4.png))

[![nakonfigurovat prvek ObjectDataSource tak, aby používal třídu SuppliersBLL](adding-a-gridview-column-of-radio-buttons-vb/_static/image5.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image5.png)

**Obrázek 5**: Konfigurace prvku ObjectDataSource, aby používal třídu `SuppliersBLL` ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-radio-buttons-vb/_static/image6.png))

Vzhledem k tomu, že chceme pouze seznam dodavatelů v USA, zvolte v rozevíracím seznamu na kartě vybrat metodu `GetSuppliersByCountry(country)`.

[![nakonfigurovat prvek ObjectDataSource tak, aby používal třídu SuppliersBLL](adding-a-gridview-column-of-radio-buttons-vb/_static/image6.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image7.png)

**Obrázek 6**: Konfigurace prvku ObjectDataSource, aby používal třídu `SuppliersBLL` ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-radio-buttons-vb/_static/image8.png))

Na kartě aktualizace vyberte možnost (žádné) a klikněte na tlačítko Další.

[![nakonfigurovat prvek ObjectDataSource tak, aby používal třídu SuppliersBLL](adding-a-gridview-column-of-radio-buttons-vb/_static/image7.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image9.png)

**Obrázek 7**: Konfigurace prvku ObjectDataSource, aby používal třídu `SuppliersBLL` ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-radio-buttons-vb/_static/image10.png))

Vzhledem k tomu, že metoda `GetSuppliersByCountry(country)` akceptuje parametr, Průvodce konfigurací zdroje dat vyzve nás ke zdroji tohoto parametru. Chcete-li zadat pevně kódované hodnoty (USA, v tomto příkladu), ponechte rozevírací seznam zdroj parametrů nastavený na hodnotu None a zadejte výchozí hodnotu v textovém poli. Kliknutím na Dokončit dokončete průvodce.

[jako výchozí hodnotu pro parametr země ![použít USA.](adding-a-gridview-column-of-radio-buttons-vb/_static/image8.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image11.png)

**Obrázek 8**: jako výchozí hodnotu pro parametr `country` použijte USA ([kliknutím zobrazíte obrázek v plné velikosti).](adding-a-gridview-column-of-radio-buttons-vb/_static/image12.png)

Po dokončení průvodce bude prvek GridView obsahovat vlastnost BoundField pro každé pole dat dodavatele. Odeberte všechny kromě `CompanyName`, `City`a `Country` BoundFields a přejmenujte vlastnost `CompanyName` BoundFields `HeaderText` na dodavatel. Po tom by deklarativní syntaxe GridView a ObjectDataSource měla vypadat podobně jako následující.

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample2.aspx)]

V tomto kurzu umožníte uživateli zobrazit vybrané produkty dodavatele na stejné stránce jako seznam dodavatelů nebo na jiné stránce. Chcete-li to přizpůsobit, přidejte na stránku dvě webové ovládací prvky tlačítka. Nastavili `ID` s těchto dvou tlačítek na `ListProducts` a `SendToProducts`s nápadem, že po kliknutí na `ListProducts` se spustí postback a vybrané produkty dodavatele budou uvedené na stejné stránce, ale když se klikne na `SendToProducts`, uživatel se zaznamená na jinou stránku, která obsahuje seznam produktů.

Obrázek 9 ukazuje `Suppliers` GridView a dvě webové ovládací prvky, které se zobrazí v prohlížeči.

[![dodavatelé z USA mají uvedené informace o jménech, městech a zemích.](adding-a-gridview-column-of-radio-buttons-vb/_static/image9.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image13.png)

**Obrázek 9**: dodavatelé z USA mají uvedené jméno, město a informace o zemi ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-radio-buttons-vb/_static/image14.png)).

## <a name="step-3-adding-a-column-of-radio-buttons"></a>Krok 3: Přidání sloupce přepínacích tlačítek

V tomto okamžiku `Suppliers` GridView má tři BoundFields, kde se zobrazuje název společnosti, město a země každého dodavatele v USA. Stále ale chybí sloupec přepínačů. Ovládací prvek GridView bohužel nezahrnuje vestavěný RadioButtonField, jinak ho můžeme jednoduše přidat do mřížky a provést. Místo toho můžeme přidat TemplateField a nakonfigurovat jeho `ItemTemplate` pro vykreslení přepínače, což vede k přepínacímu tlačítku pro každý řádek prvku GridView.

Zpočátku můžeme předpokládat, že požadované uživatelské rozhraní může být implementováno přidáním webového ovládacího prvku RadioButton do `ItemTemplate` ovládacího prvku TemplateField. I když se to bude muset přidat jeden přepínač na každý řádek prvku GridView, přepínače nelze seskupovat, a proto se vzájemně nevylučují. To znamená, že koncový uživatel může v prvku GridView vybrat více přepínačů současně.

I když použití pole TemplateField webových ovládacích prvků RadioButton nenabízí funkcionalitu, kterou potřebujeme, můžeme implementovat tento přístup, protože je vhodné posuzovat, proč nejsou výsledná přepínací tlačítka seskupena. Začněte přidáním prvku TemplateField do prvku GridView dodavatelé, takže se zobrazí pole nejvíce vlevo. Dále z inteligentní značky GridView. klikněte na odkaz Upravit šablony a přetáhněte ovládací prvek web RadioButton ze sady nástrojů do `ItemTemplate` TemplateField s (viz obrázek 10). Nastavte vlastnost `ID` RadioButton na `RowSelector` a vlastnost `GroupName` na `SuppliersGroup`.

[![přidání webového ovládacího prvku RadioButton do šablony ItemTemplate](adding-a-gridview-column-of-radio-buttons-vb/_static/image10.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image15.png)

**Obrázek 10**: Přidání webového ovládacího prvku RadioButton do `ItemTemplate` ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-radio-buttons-vb/_static/image16.png))

Po tom, co tyto položky provedete pomocí návrháře, by vaše značka GridViewu měla vypadat nějak takto:

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample3.aspx)]

[Vlastnost RadioButton`GroupName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.radiobutton.groupname(VS.80).aspx) je to, co se používá k seskupení řady přepínacích tlačítek. Všechny ovládací prvky RadioButton se stejnou hodnotou `GroupName` jsou považovány za seskupené. v jednom okamžiku může být vybráno pouze jedno přepínač. Vlastnost `GroupName` Určuje hodnotu pro vygenerované `name` atribut přepínacího tlačítka. Prohlížeč projde přepínači `name` atributů a určí seskupení přepínačů.

Po přidání webového ovládacího prvku RadioButton do `ItemTemplate`navštivte tuto stránku v prohlížeči a klikněte na přepínače v řádcích Grid. Všimněte si, jak přepínače nejsou seskupeny, takže je možné vybrat všechny řádky, jak ukazuje obrázek 11.

[![přepínačů GridView s nejsou seskupeny.](adding-a-gridview-column-of-radio-buttons-vb/_static/image11.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image17.png)

**Obrázek 11**: přepínače GridView s nejsou seskupeny ([kliknutím zobrazíte obrázek v plné velikosti).](adding-a-gridview-column-of-radio-buttons-vb/_static/image18.png)

Důvodem, proč přepínače nejsou seskupeny, je, že se jejich vykreslené `name` atributy liší, i když mají stejné nastavení `GroupName` vlastností. Chcete-li tyto rozdíly zobrazit, proveďte v prohlížeči zobrazení a zdroj a Prohlédněte si značku přepínacího tlačítka:

[!code-html[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample4.html)]

Všimněte si, jak atributy `name` i `id` nejsou přesné hodnoty, jak je uvedeno v okno Vlastnosti, ale jsou součástí několika dalších `ID` hodnot. Další `ID` hodnoty přidané na začátek `id` a `name` atributů jsou `ID` s přepínači nadřazenými ovládacími prvky: `GridViewRow` s `ID` s, GridView s `ID`, ovládací prvek obsahu s `ID`a webový formulář s `ID`. Tyto `ID` s jsou přidány tak, že každý vykreslený webový ovládací prvek v prvku GridView má jedinečné `id` a `name` hodnoty.

Každý vykreslený ovládací prvek potřebuje jiné `name` a `id`, protože se jedná o způsob, jakým prohlížeč jednoznačně identifikuje každý ovládací prvek na straně klienta a jak ho identifikuje na webovém serveru, ke kterému došlo při zpětném volání k akci nebo změně. Představte si například, že jsme chtěli spustit některý kód na straně serveru pokaždé, když došlo ke změně stavu zaškrtnutí komponenty RadioButton. To můžeme provést nastavením vlastnosti `AutoPostBack` RadioButton na `True` a vytvořením obslužné rutiny události pro událost `CheckChanged`. Pokud však vykreslené `name` a hodnoty `id` pro všechna přepínací tlačítka byly stejné, při zpětném odeslání nemůžeme určit, jaký konkrétní přepínač RadioButton jste klikli.

To je krátké, že nemůžeme vytvořit sloupec přepínacích tlačítek v prvku GridView pomocí ovládacího prvku web RadioButton. Místo toho je nutné použít spíše archaickým systémem techniky, aby se zajistilo, že se do každého řádku GridView vloží odpovídající kód.

> [!NOTE]
> Podobně jako ovládací prvek web RadioButton, ovládací prvek pro přepínač HTML, který je přidán do šablony, bude obsahovat jedinečný atribut `name`, aby se přepínače v mřížce nepřidaly do skupin. Pokud nejste obeznámeni s ovládacími prvky HTML, nebojte si tuto poznámku bez ohledu na to, že se používají zřídka pouze ovládací prvky HTML, zejména v ASP.NET 2,0. Pokud vás ale zajímá více, přečtěte si téma K [webové ovládací prvky blogu a ovládací prvky HTML](http://www.odetocode.com/Articles/348.aspx)pro záznam blogu [. Scott Allen](http://odetocode.com/blogs/scott/default.aspx) s.

## <a name="using-a-literal-control-to-inject-radio-button-markup"></a>Použití ovládacího prvku literálu k vložení značky přepínacího tlačítka

Aby bylo možné správně seskupit všechna přepínací tlačítka v prvku GridView, je nutné ručně vložit do `ItemTemplate`označení přepínacích tlačítek. Každé přepínací tlačítko potřebuje stejný atribut `name`, ale měl by mít jedinečný atribut `id` (pro případ, že chceme získat přístup k přepínači prostřednictvím skriptu na straně klienta). Poté, co uživatel vybere přepínač a odešle zpět stránku, prohlížeč pošle zpět hodnotu vybraného přepínače `value` atributu. Proto každý přepínač bude potřebovat jedinečný atribut `value`. V případě zpětného odeslání je potřeba zajistit, aby byl atribut `checked` na vybraný přepínač, který je vybrán, v opačném případě, když uživatel provede výběr a vrátí zpět, se přepínače vrátí do výchozího stavu (všechny nevybrané).

Existují dva přístupy, které je možné provést za účelem vložení značek nízké úrovně do šablony. Jedním z nich je provedení kombinace značek a volání metod formátování definovaných v třídě kódu na pozadí. Tato technika byla poprvé popsána v tématu [použití templatefields v kurzu ovládacího prvku GridView](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) . V našem případě může vypadat nějak takto:

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample5.aspx)]

V tomto případě `GetUniqueRadioButton` a `GetRadioButtonValue` by byly metody definované v třídě kódu na pozadí, které vrátily příslušné hodnoty atributu `id` a `value` pro každé přepínač. Tento přístup funguje dobře pro přiřazení atributů `id` a `value`, ale je krátký, pokud je potřeba zadat hodnotu atributu `checked`, protože syntaxe datové vazby se spustí pouze v případě, že jsou data nejprve svázána s objektem GridView. Proto pokud má prvek GridView povolený stav zobrazení, metody formátování budou aktivovány pouze při prvním načtení stránky (nebo pokud je prvek GridView explicitně svázán se zdrojem dat), a proto funkce, která nastaví atribut `checked`, nebude při zpětném volání volána. Je to spíše drobný problém a bit nad rámec tohoto článku, takže ho ponecháme. Ale doporučujeme, abyste se pokusili použít výše uvedený postup a pracovat s nimi až do chvíle, kdy se dostanete k zablokování. I když takové cvičení nezíská žádné bližší informace k pracovní verzi, pomůže vám pochopit hlubší porozumění prvku GridView a životního cyklu datové vazby.

Druhý přístup k vložení vlastního kódu, značky nízké úrovně v šabloně a přístupu, který budeme používat pro tento kurz, je přidání [ovládacího prvku literálu](https://msdn.microsoft.com/library/sz4949ks(VS.80).aspx) do šablony. Poté v obslužné rutině události GridView `RowCreated` nebo `RowDataBound` lze k ovládacímu prvku literálu přistupovat prostřednictvím kódu programu a jeho vlastnost `Text` nastavena na značku pro vygenerování.

Začněte odebráním prvku RadioButton z `ItemTemplate`TemplateField s a jeho nahrazením ovládacím prvkem literál. Nastavte `ID` ovládacího prvku literálu na `RadioButtonMarkup`.

[![přidat do šablony ItemTemplate ovládací prvek literálu](adding-a-gridview-column-of-radio-buttons-vb/_static/image12.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image19.png)

**Obrázek 12**: Přidání ovládacího prvku literálu do `ItemTemplate` ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-radio-buttons-vb/_static/image20.png))

Dále vytvořte obslužnou rutinu události pro `RowCreated` událost GridView. Událost `RowCreated` je aktivována jednou pro každý přidaný řádek, bez ohledu na to, zda jsou data převázána na prvek GridView. To znamená, že i při zpětném volání, když jsou data znovu načtena ze stavu zobrazení, je `RowCreated` událost stále aktivována a jedná se o důvod, proč ji používáme místo `RowDataBound` (která se aktivuje pouze v případě, že jsou data explicitně svázána s datovým ovládacím prvkem web data).

V této obslužné rutině události chceme pokračovat pouze v případě, že budeme znovu pracovat s datovým řádkem. Pro každý řádek dat, který chceme programově odkazovat na ovládací prvek literálu `RadioButtonMarkup` a nastavte jeho vlastnost `Text` na hodnotu emited. Jak ukazuje následující kód, vygenerované označení vytvoří přepínač, jehož atribut `name` je nastaven na `SuppliersGroup`, jehož atribut `id` je nastaven na `RowSelectorX`, kde *X* je index řádku GridView a jehož atribut `value` je nastaven na index řádku GridView.

[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample6.vb)]

Když je vybrán řádek GridView a dojde k postbacku, zajímá Vás `SupplierID` vybraného dodavatele. Proto jeden z nich může znamenat, že hodnota každého přepínacího tlačítka by měla být skutečným `SupplierID` (spíše než index řádku GridView). I když to může v určitých případech fungovat, mohlo by se jednat o bezpečnostní riziko pro nevidomé a nezpracované `SupplierID`. V našem prvku GridView například zobrazí seznam pouze dodavatelů v USA. Pokud se ale `SupplierID` předává přímo z přepínače, co se stane s tím, že se uživateli zastaví manipulace s `SupplierID` hodnota, která se při postbacku posílá zpátky? Když použijete index řádku jako `value`a pak `SupplierID` při postbacku z kolekce `DataKeys`, můžeme zajistit, aby uživatel používal jenom jednu z `SupplierID` hodnot, které jsou přidružené k jednomu z řádků GridView.

Po přidání tohoto kódu obslužné rutiny události si vyzkoušíte minutu, abyste si vyzkoušeli stránku v prohlížeči. Nejdřív si všimněte, že v jednom okamžiku může být vybraný jenom jeden přepínač v mřížce. Když však vybíráte přepínač a kliknete na jedno z tlačítek, dojde k postbacku a přepínače se vrátí do jejich počátečního stavu (tj. při zpětném odeslání vybraný přepínač už není vybraný). Chcete-li tento problém vyřešit, musíme rozšířit obslužnou rutinu události `RowCreated` tak, aby zkontrolovala vybraný index přepínačů odeslaných z zpětného volání a přidala `checked="checked"` atribut do vygenerovaného kódu shody indexu řádků.

Když dojde k postbacku, prohlížeč pošle zpátky `name` a `value` vybraného přepínače. Hodnotu lze programově načíst pomocí `Request.Form("name")`. [Vlastnost`Request.Form`](https://msdn.microsoft.com/library/system.web.httprequest.form.aspx) poskytuje [`NameValueCollection`](https://msdn.microsoft.com/library/system.collections.specialized.namevaluecollection.aspx) reprezentující proměnné formuláře. Proměnné formuláře jsou názvy a hodnoty polí formuláře na webové stránce a jsou odesílány zpět webovým prohlížečem při každém provedení postbacku. Vzhledem k tomu, že atribut vykreslený `name` přepínačů v prvku GridView je `SuppliersGroup`, když je webová stránka publikována zpět, prohlížeč pošle `SuppliersGroup=valueOfSelectedRadioButton` zpátky na webový server (spolu s dalšími poli formuláře). Tyto informace lze následně získat z vlastnosti `Request.Form` pomocí: `Request.Form("SuppliersGroup")`.

Vzhledem k tomu, že je potřeba určit, který index přepínačů není pouze v obslužné rutině události `RowCreated`, ale v obslužných rutinách události `Click` pro webové ovládací prvky tlačítka, `SuppliersSelectedIndex` přidejte do třídy kódu na pozadí, která vrací `-1`, pokud nebyl vybrán přepínač a vybraný index, pokud je vybrán jeden z přepínačů.

[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample7.vb)]

Po přidání této vlastnosti ví, že přidáte značku `checked="checked"` do obslužné rutiny události `RowCreated`, když `SuppliersSelectedIndex` rovná `e.Row.RowIndex`. Aktualizujte obslužnou rutinu události tak, aby zahrnovala tuto logiku:

[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample8.vb)]

Při této změně zůstane vybraný přepínač po postbacku vybraný. Teď, když máme možnost zadat, který přepínač je vybraný, můžeme změnit chování tak, aby bylo při prvním navštívení stránky vybráno první přepínač řádku GridView (místo toho, aby ve výchozím nastavení nebyly žádné přepínače vybrány, což je aktuální chování). Chcete-li mít první přepínač vybraný jako výchozí, jednoduše změňte příkaz `If SuppliersSelectedIndex = e.Row.RowIndex Then` na následující: `If SuppliersSelectedIndex = e.Row.RowIndex OrElse (Not Page.IsPostBack AndAlso e.Row.RowIndex = 0) Then`.

V tomto okamžiku jsme přidali sloupec seskupených přepínačů do prvku GridView, který umožňuje vybrat jeden řádek prvku GridView a začlenit je mezi jednotlivými zpětnými odesláními. Naším dalším postupem je zobrazení produktů poskytovaných vybraným dodavatelem. V kroku 4 se dozvíte, jak přesměrovat uživatele na jinou stránku, která posílá na vybraný `SupplierID`. V kroku 5 se dozvíte, jak zobrazit vybrané produkty dodavatele v prvku GridView na stejné stránce.

> [!NOTE]
> Namísto použití TemplateField (zaměřuje se na tento zdlouhavý krok 3) můžeme vytvořit vlastní třídu `DataControlField`, která vykresluje příslušné uživatelské rozhraní a funkce. [Třída`DataControlField`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datacontrolfield.aspx) je základní třída, ze které jsou odvozeny pole vlastnost BoundField, třídě CheckBoxField podporována, TemplateField a další předdefinovaná pole GridView a DetailsView. Vytvoření vlastní `DataControlField` třídy by znamenalo, že sloupec přepínacích tlačítek by mohl být přidán pouze pomocí deklarativní syntaxe a také významně jednodušší replikaci funkcí na jiné webové stránky a další webové aplikace.

Pokud jste někdy vytvořili vlastní, zkompilované ovládací prvky v ASP.NET, ale víte, že by to mělo být reálné množství samotnému a s ním nese hostitel odlišností a hraničních případů, které je nutné pečlivě zpracovat. Proto nebudeme pro teď implementovat sloupec přepínačů jako vlastní třídu `DataControlField` a vytvořit tak možnost TemplateField. Možná budeme mít možnost prozkoumat vytváření, používání a nasazování vlastních tříd `DataControlField` v budoucím kurzu.

## <a name="step-4-displaying-the-selected-supplier-s-products-in-a-separate-page"></a>Krok 4: zobrazení vybraných produktů dodavatele s na samostatné stránce

Jakmile uživatel vybere řádek prvku GridView, musíme Zobrazit vybrané produkty dodavatele. V některých případech můžeme chtít zobrazit tyto produkty na samostatné stránce, a to i v jiných případech, jako by to bylo vhodné na stejné stránce. Nejdřív si podíváme, jak zobrazit produkty na samostatné stránce. v kroku 5 se podíváme na přidání prvku GridView, aby se zobrazily vybrané produkty dodavatele s `RadioButtonField.aspx`.

V současné době existují dva ovládací prvky na tlačítku na stránce `ListProducts` a `SendToProducts`. Když kliknete na tlačítko `SendToProducts`, chceme uživateli odeslat `~/Filtering/ProductsForSupplierDetails.aspx`. Tato stránka se vytvořila v kurzu zobrazení [hlavního/podrobného filtrování napříč dvěma stránkami](../masterdetail/master-detail-filtering-across-two-pages-vb.md) a zobrazuje produkty pro dodavatele, jejichž `SupplierID` se předaly prostřednictvím pole QueryString s názvem `SupplierID`.

Chcete-li tuto funkci poskytnout, vytvořte obslužnou rutinu události pro událost `Click` `SendToProducts` tlačítkem. V kroku 3 jsme přidali vlastnost `SuppliersSelectedIndex`, která vrací index řádku, jehož přepínač je vybrán. Odpovídající `SupplierID` lze načíst z kolekce prvku GridView s `DataKeys` a uživatel je pak možné odeslat do `~/Filtering/ProductsForSupplierDetails.aspx?SupplierID=SupplierID` pomocí `Response.Redirect("url")`.

[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample9.vb)]

Tento kód funguje, pokud je jeden z přepínačů vybrán z prvku GridView. Pokud zpočátku v prvku GridView není vybrána žádná přepínač a uživatel klikne na tlačítko `SendToProducts`, `SuppliersSelectedIndex` bude `-1`, což způsobí vyvolání výjimky, protože `-1` je mimo rozsah indexu `DataKeys` kolekce. Nejedná se však o obavy, pokud jste se rozhodli aktualizovat `RowCreated` obslužnou rutinu události, jak je popsáno v kroku 3, abyste měli první přepínač v původně vybraném prvku GridView.

Chcete-li přizpůsobit hodnotu `SuppliersSelectedIndex` `-1`, přidejte ovládací prvek web Label na stránku nad prvek GridView. Vlastnost `ID` nastavte na `ChooseSupplierMsg`, jeho vlastnost `CssClass` na `Warning`, vlastnosti `EnableViewState` a `Visible` na `False`a jeho vlastnost `Text` pro výběr dodavatele z mřížky. Třída CSS `Warning` zobrazuje text červeným, kurzívou, tučně, velkým písmem a je definován v `Styles.css`. Nastavením vlastností `EnableViewState` a `Visible` na `False`není popisek vykreslen s výjimkou pouze těch postbacků, kde je vlastnost ovládacího prvku `Visible` programově nastavena na hodnotu `True`.

[![přidání webového ovládacího prvku Popisek nad prvek GridView](adding-a-gridview-column-of-radio-buttons-vb/_static/image13.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image21.png)

**Obrázek 13**: Přidání webového ovládacího prvku Popisek nad prvek GridView ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-radio-buttons-vb/_static/image22.png))

Dále Rozšiřte `Click` obslužnou rutinu události, aby zobrazila popisek `ChooseSupplierMsg`, pokud je `SuppliersSelectedIndex` menší než nula, a přesměrujte uživatele na `~/Filtering/ProductsForSupplierDetails.aspx?SupplierID=SupplierID` jinak.

[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample10.vb)]

Přejděte na stránku v prohlížeči a před výběrem dodavatele z prvku GridView klikněte na tlačítko `SendToProducts`. Jak ukazuje obrázek 14, zobrazuje popisek `ChooseSupplierMsg`. Potom vyberte dodavatele a klikněte na tlačítko `SendToProducts`. Zobrazí se vám stránka se seznamem produktů poskytovaných vybraným dodavatelem. Obrázek 15 ukazuje stránku `ProductsForSupplierDetails.aspx`, když byl vybrán dodavatel Bigfoot pivovary.

[![popisek ChooseSupplierMsg se zobrazí, pokud není vybraný žádný dodavatel.](adding-a-gridview-column-of-radio-buttons-vb/_static/image14.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image23.png)

**Obrázek 14**: popisek `ChooseSupplierMsg` se zobrazí, pokud není vybrán žádný dodavatel ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-radio-buttons-vb/_static/image24.png)).

[![se vybrané produkty dodavatele zobrazují v ProductsForSupplierDetails. aspx.](adding-a-gridview-column-of-radio-buttons-vb/_static/image15.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image25.png)

**Obrázek 15**: vybrané produkty dodavatele se zobrazují v `ProductsForSupplierDetails.aspx` ([kliknutím zobrazíte obrázek v plné velikosti).](adding-a-gridview-column-of-radio-buttons-vb/_static/image26.png)

## <a name="step-5-displaying-the-selected-supplier-s-products-on-the-same-page"></a>Krok 5: zobrazení vybraných produktů dodavatele s na stejné stránce

V kroku 4 jsme viděli, jak odeslat uživatele na jinou webovou stránku, aby se zobrazily vybrané produkty dodavatele. Další možností je, že vybraný produkt dodavatele se může zobrazit na stejné stránce. K ilustraci přidáme další prvek GridView pro `RadioButtonField.aspx` pro zobrazení vybraných produktů dodavatele.

Vzhledem k tomu, že chceme, aby se tento prvek GridViewy zobrazoval po výběru dodavatele, přidejte ovládací prvek Panel web pod `Suppliers` GridView, nastavením jeho `ID` na `ProductsBySupplierPanel` a jeho vlastnost `Visible` na `False`. V rámci tohoto panelu přidejte textové produkty pro vybraného dodavatele a potom prvek GridView s názvem `ProductsBySupplier`. Z inteligentní značky GridView s vyberte, že se má vytvořit vazba s novým prvkem ObjectDataSource s názvem `ProductsBySupplierDataSource`.

[![svázání prvku GridView ProductsBySupplier s novým prvkem ObjectDataSource](adding-a-gridview-column-of-radio-buttons-vb/_static/image16.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image27.png)

**Obrázek 16**: vazba prvku `ProductsBySupplier` GridView na nový prvek ObjectDataSource ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-radio-buttons-vb/_static/image28.png))

Dále nakonfigurujte prvek ObjectDataSource tak, aby používal třídu `ProductsBLL`. Vzhledem k tomu, že chceme načíst pouze tyto produkty poskytované vybraným dodavatelem, určete, že prvek ObjectDataSource by měl vyvolat metodu `GetProductsBySupplierID(supplierID)` pro načtení dat. V rozevíracích seznamech na kartách aktualizace, vložení a odstranění vyberte (žádné).

[![nakonfigurovat prvek ObjectDataSource na použití metody GetProductsBySupplierID (KódDodavatele)](adding-a-gridview-column-of-radio-buttons-vb/_static/image17.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image29.png)

**Obrázek 17**: Konfigurace prvku ObjectDataSource pro použití metody `GetProductsBySupplierID(supplierID)` ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-radio-buttons-vb/_static/image30.png))

[![nastavení rozevíracích seznamů na (žádné) na kartách aktualizace, vložení a odstranění](adding-a-gridview-column-of-radio-buttons-vb/_static/image18.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image31.png)

**Obrázek 18**: nastavení rozevíracích seznamů na (žádné) na kartách aktualizace, vložení a odstranění ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-radio-buttons-vb/_static/image32.png))

Po konfiguraci karet vybrat, aktualizovat, vložit a odstranit klikněte na další. Vzhledem k tomu, že metoda `GetProductsBySupplierID(supplierID)` očekává vstupní parametr, Průvodce vytvořením zdroje dat vyzve nás k zadání zdroje pro hodnotu parametru s.

K dispozici je několik možností, jak zadat zdroj hodnoty parametru s. Mohli bychom použít výchozí objekt parametrů a programově přiřadit hodnotu vlastnosti `SuppliersSelectedIndex` parametru `DefaultValue` vlastnosti v obslužné rutině události ObjectDataSource s `Selecting`. Přečtěte si [programové nastavení kurzu hodnoty parametru ObjectDataSource](../basic-reporting/programmatically-setting-the-objectdatasource-s-parameter-values-vb.md) pro aktualizační program pro aktualizační program, který přiřadí hodnoty parametrům ObjectDataSource s.

Alternativně můžeme použít třídě ControlParameter a odkazovat na vlastnost `Suppliers` GridView s [`SelectedValue`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedvalue.aspx) (viz obrázek 19). Vlastnost `SelectedValue` ovládacího prvku GridView vrací hodnotu `DataKey` odpovídající [vlastnosti`SelectedIndex`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindex.aspx). Aby tato možnost fungovala, musíme při kliknutí na tlačítko `ListProducts` nastavit vlastnost `SelectedIndex` prvku GridView s na vybraný řádek. Když `SelectedIndex`přidáte výhodu, bude vybraný záznam přebírat `SelectedRowStyle` definované v motivu `DataWebControls` (žluté pozadí).

[![použít třídě ControlParameter k určení prvku GridView s SelectedValue jako zdroje parametru](adding-a-gridview-column-of-radio-buttons-vb/_static/image19.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image33.png)

**Obrázek 19**: použití třídě ControlParameter k určení SelectedValue prvku GridView s jako zdroje parametru ([kliknutím zobrazíte obrázek v plné velikosti](adding-a-gridview-column-of-radio-buttons-vb/_static/image34.png))

Po dokončení průvodce bude Visual Studio automaticky přidávat pole pro datová pole produktu. Odeberte všechny kromě `ProductName`, `CategoryName`a `UnitPrice` BoundFields a změňte `HeaderText` vlastnosti na produkt, kategorii a cenu. Nakonfigurujte `UnitPrice` vlastnost BoundField, aby se jeho hodnota formátovala jako měna. Po provedení těchto změn by deklarativní značky panelu, prvku GridView a ObjectDataSource s měly vypadat takto:

[!code-aspx[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample11.aspx)]

Pro dokončení tohoto cvičení musíme nastavit vlastnost GridView `SelectedIndex` na `SelectedSuppliersIndex` a vlastnost `ProductsBySupplierPanel` panel s `Visible` na `True` při kliknutí na tlačítko `ListProducts`. Chcete-li to provést, vytvořte obslužnou rutinu události pro webový ovládací prvek tlačítko `ListProducts` `Click` událost a přidejte následující kód:

[!code-vb[Main](adding-a-gridview-column-of-radio-buttons-vb/samples/sample12.vb)]

Pokud dodavatel nebyl vybrán z prvku GridView, zobrazí se popisek `ChooseSupplierMsg` a panel `ProductsBySupplierPanel` skrytý. V opačném případě, pokud byl vybrán dodavatel, je zobrazen `ProductsBySupplierPanel` a je aktualizována vlastnost GridView `SelectedIndex`.

Obrázek 20 zobrazuje výsledky po výběru dodavatele Bigfoot Pivovars a kliknutí na tlačítko Zobrazit produkty na stránce.

[![produkty dodávané pomocí Bigfoot pivovary jsou uvedené na stejné stránce.](adding-a-gridview-column-of-radio-buttons-vb/_static/image20.gif)](adding-a-gridview-column-of-radio-buttons-vb/_static/image35.png)

**Obrázek 20**: produkty dodávané společností Bigfoot pivovars jsou uvedeny na stejné stránce ([kliknutím zobrazíte obrázek v plné velikosti).](adding-a-gridview-column-of-radio-buttons-vb/_static/image36.png)

## <a name="summary"></a>Přehled

Jak je popsáno v části [hlavní a podrobnosti pomocí selektivního hlavního prvku GridView s podrobným](../masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb.md) kurzem prvku detailview, lze záznamy vybrat z prvku GridView pomocí CommandField, jehož vlastnost `ShowSelectButton` je nastavena na hodnotu `True`. Ale CommandField zobrazí jeho tlačítka buď jako standardní tlačítka pro vložení, odkazy nebo obrázky. Alternativním uživatelským rozhraním pro výběr řádků je poskytnout přepínač nebo zaškrtávací políčko v každém řádku GridView. V tomto kurzu jsme prozkoumali, jak přidat sloupec přepínacích tlačítek.

Bohužel přidání sloupce přepínačů nestačí jako jednoduché nebo jednoduché, protože může očekávat. Není k dispozici žádná integrovaná RadioButtonField, která by mohla být přidána na kliknutí na tlačítko a použití ovládacího prvku RadioButton v rámci TemplateField zavádí vlastní sadu problémů. Aby toto rozhraní poskytovalo takové rozhraní, musí buď vytvořit vlastní třídu `DataControlField`, nebo použít k vložení příslušného kódu HTML do objektu TemplateField během `RowCreated` události.

Seznámili jste se s tím, jak přidat sloupec přepínačů, abychom nám mohli dát pozor na přidání sloupce zaškrtávacích políček. U sloupce zaškrtávacích políček může uživatel vybrat jeden nebo více řádků GridView a pak provést určitou operaci na všech vybraných řádcích (například vybrat sadu e-mailů z webového e-mailového klienta a pak zvolit odstranění všech vybraných e-mailů). V dalším kurzu uvidíte, jak takový sloupec přidat.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolorovi realizace tohoto kurzu bylo David Suru. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](inserting-a-new-record-from-the-gridview-s-footer-cs.md)
> [Další](adding-a-gridview-column-of-checkboxes-vb.md)

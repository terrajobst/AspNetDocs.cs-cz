---
uid: web-forms/overview/moving-to-aspnet-20/data-bound-controls
title: Ovládací prvky vázané na data | Microsoft Docs
author: microsoft
description: Většina ASP.NETch aplikací spoléhá na určitý stupeň prezentace dat ze zdroje dat back-endu. Ovládací prvky vázané na data byly pivotické části interakce s...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 0e23ff32-646d-43f3-8bec-6b2313d3abd6
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/data-bound-controls
msc.type: authoredcontent
ms.openlocfilehash: 1154b38e0fa3d9d56cb407ae659c3b0d69871fda
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78603836"
---
# <a name="data-bound-controls"></a>Ovládací prvky svázané s daty

od [Microsoftu](https://github.com/microsoft)

> Většina ASP.NETch aplikací spoléhá na určitý stupeň prezentace dat ze zdroje dat back-endu. Ovládací prvky vázané na data jsou kontingenční součástí interakce s daty v dynamických webových aplikacích. ASP.NET 2,0 zavádí několik podstatných vylepšení ovládacích prvků vázaných na data, včetně nové třídy BaseDataBoundControl a deklarativní syntaxe.

Většina ASP.NETch aplikací spoléhá na určitý stupeň prezentace dat ze zdroje dat back-endu. Ovládací prvky vázané na data jsou kontingenční součástí interakce s daty v dynamických webových aplikacích. ASP.NET 2,0 zavádí několik podstatných vylepšení ovládacích prvků vázaných na data, včetně nové třídy BaseDataBoundControl a deklarativní syntaxe.

BaseDataBoundControl funguje jako základní třída pro třídu objekt DataBoundControl povoleno a třídu Třída HierarchicalDataBoundControl přijímá. V tomto modulu se budeme zabývat následujícími třídami odvozenými z objekt DataBoundControl povoleno:

- Ovládacím
- Seznam ovládacích prvků
- GridView
- Třídě
- DetailsView

Probereme také následující třídy, které se odvozují z třídy třída HierarchicalDataBoundControl přijímá:

- TreeView
- Nabídka
- SiteMapPath

## <a name="databoundcontrol-class"></a>Objekt DataBoundControl povoleno – třída

Třída objekt DataBoundControl povoleno je abstraktní třída (označena jako MustInherit v jazyce VB), která slouží k interakci s daty typu tabulka nebo seznam. Následující ovládací prvky jsou některé z ovládacích prvků, které jsou odvozeny z objekt DataBoundControl povoleno.

## <a name="adrotator"></a>Ovládacím

Ovládací prvek AdRotator umožňuje zobrazit proužek grafiky na webové stránce, která je propojena s konkrétní adresou URL. Obrázek, který se zobrazí, je otočen pomocí vlastností ovládacího prvku. Frekvence konkrétní reklamy, která se zobrazuje na stránce, se dá nakonfigurovat **pomocí vlastnosti "** počet potlačení" a reklamu je možné filtrovat pomocí filtrování klíčových slov.

Ovládací prvky AdRotator používají buď soubor XML, nebo tabulku v databázi pro data. Následující atributy se používají v souborech XML ke konfiguraci ovládacího prvku AdRotator.

### <a name="imageurl"></a>ImageUrl
Adresa URL obrázku, který má být zobrazen pro reklamu

### <a name="navigateurl"></a>NavigateUrl
Adresa URL, na kterou se má uživatel vzít při kliknutí na reklamu Mělo by se jednat o kódování URL.

### <a name="alternatetext"></a>AlternateText
Alternativní text, který se zobrazí v popisu tlačítka a který přečtou čtečky obrazovky. Zobrazí se také v případě, že není k dispozici bitová kopie určená nástrojem ImageUrl.

### <a name="keyword"></a>Klíčové slovo
Definuje klíčové slovo, které lze použít při použití filtrování klíčového slova. Je-li tento parametr zadán, zobrazí se pouze ty reklamy s klíčovým slovem, které odpovídá filtru klíčového slova.

### <a name="impressions"></a>Imprese
Číslo váhy, které určuje, jak často se bude pravděpodobně zobrazovat konkrétní reklama. Je relativní vzhledem ke dojmu dalších reklam ve stejném souboru. Maximální hodnota pro společná nestisknutí pro všechny reklamy v souboru XML je 2 048 000 000 1.

### <a name="height"></a>Výška
Výška reklamy v pixelech

### <a name="width"></a>impulzu
Šířka reklamy v pixelech.

> [!NOTE]
> Atributy Height a Width přepíší výšku a šířku pro samotný ovládací prvek AdRotator.

Typický soubor XML může vypadat takto:

[!code-xml[Main](data-bound-controls/samples/sample1.xml)]

Ve výše uvedeném příkladu je služba AD pro contoso dvakrát, aby se mohla zobrazit jako služba AD pro web ASP.NET z důvodu hodnoty atributu pro nestisknutí.

Chcete-li zobrazit reklamy z výše uvedeného souboru XML, přidejte ovládací prvek AdRotator na stránku a nastavte vlastnost **nenalezla soubor AdvertisementFile** tak, aby odkazovala na soubor XML, jak je znázorněno níže:

[!code-aspx[Main](data-bound-controls/samples/sample2.aspx)]

Pokud se rozhodnete použít databázovou tabulku jako zdroj dat pro ovládací prvek AdRotator, budete nejprve muset nastavit databázi pomocí následujícího schématu:

| **Název sloupce** | **Datový typ** | **Popis** |
| --- | --- | --- |
| ID | int | Primární klíč. Tento sloupec může mít libovolný název. |
| ImageUrl | nvarchar (*Délka*) | Relativní nebo absolutní adresa URL obrázku, který má být zobrazen pro službu AD. |
| NavigateUrl | nvarchar (*Délka*) | Cílová adresa URL pro AD Pokud nezadáte žádnou hodnotu, reklama není hypertextový odkaz. |
| AlternateText | nvarchar (*Délka*) | Text zobrazený v případě, že nelze najít obrázek V některých prohlížečích se text zobrazuje jako popis. Alternativní text se také používá pro usnadnění, aby uživatelé, kteří obrázek nevidí, mohli slyšet popis číst nahlas. |
| Klíčové slovo | nvarchar (*Délka*) | Kategorie pro reklamu, na které může stránka filtrovat. |
| Imprese | int(4) | Číslo, které označuje pravděpodobnost, jak často se AD zobrazuje. Čím větší je číslo, tím častěji se bude zobrazovat reklama. Celkový počet všech netiskových hodnot v souboru XML nesmí překročit 2 048 000 000-1. |
| impulzu | int(4) | Šířka obrázku v pixelech |
| Výška | int(4) | Výška obrázku v pixelech |

V případech, kdy už máte databázi s jiným schématem, můžete pomocí vlastností **AlternateTextField**, **ImageUrlField**a **NavigateUrlField** namapovat atributy AdRotator na stávající databázi. Chcete-li zobrazit data z databáze v ovládacím prvku AdRotator, přidejte na ni ovládací prvek zdroje dat, nakonfigurujte připojovací řetězec pro ovládací prvek zdroje dat tak, aby odkazoval na vaši databázi, a nastavte vlastnost **DataSourceID** ovládacího prvku ADROTATOR na ID ovládacího prvku zdroje dat. V případech, kdy potřebujete konfigurovat reklamu AdRotator prostřednictvím kódu programu, použijte událost AdCreated. Událost AdCreated přijímá dva parametry; jeden objekt a druhá instance třídy AdCreatedEventArgs. AdCreatedEventArgs je odkaz na vytvářený inzerát.

Následující fragment kódu nastaví ImageUrl, NavigateUrl a AlternateText pro službu AD programově:

[!code-csharp[Main](data-bound-controls/samples/sample3.cs)]

## <a name="list-controls"></a>Seznam ovládacích prvků

Ovládací prvky seznamu zahrnují seznam, DropDownList, CheckBoxList, RadioButtonList a BulletedList. Každý z těchto ovládacích prvků může být data vázaná na zdroj dat. Používají jedno pole ve zdroji dat jako text zobrazení a mohou volitelně použít druhé pole jako hodnotu položky. Položky lze také přidat staticky v době návrhu a můžete kombinovat statické položky a dynamické položky přidané ze zdroje dat.

Pro svázání dat s ovládacím prvkem seznam přidejte ovládací prvek zdroje dat na stránku. Zadejte příkaz SELECT pro ovládací prvek zdroje dat a poté nastavte vlastnost DataSourceID ovládacího prvku seznam na ID ovládacího prvku zdroje dat. Použijte vlastnosti **DataTextField** a **DataValueField** k definování zobrazovaného textu a hodnoty ovládacího prvku. Kromě toho můžete pomocí vlastnosti **DataTextFormatString** řídit vzhled zobrazovaného textu následujícím způsobem:

| **Vyjádření** | **Popis** |
| --- | --- |
| Cena: {0:C} | Pro číselná/Desítková data. Zobrazí literál "Price" následovaný čísly ve formátu měny. Formát měny závisí na nastavení jazykové verze zadaného v atributu Culture v direktivě **stránky** nebo v souboru Web. config. |
| {0:D4} | Pro data typu Integer. Nelze použít s desetinnými čísly. Celá čísla se zobrazí v poli s nulovým čalouněním, které má 4 znaky na šířku. |
| {0:N2}% | Pro číselná data. Zobrazí číslo s přesností na dvě desetinná místa následovaná literálem "%". |
| {0:000.0} | Pro číselná/Desítková data. Čísla se zaokrouhlují na jedno desetinné místo. Čísla menší než tři číslice jsou doplněna nulami. |
| {0:D} | Pro data data a času. Zobrazí formát dlouhého data ("čtvrtek, srpen 06, 1996"). Formát data závisí na nastavení jazykové verze stránky nebo souboru Web. config. |
| {0:d} | Pro data data a času. Zobrazí krátký formát data ("12/31/99"). |
| {0: RR-MM-DD} | Pro data data a času. Zobrazí datum v číselném formátu roku-měsíc-den (96-08-06). |

## <a name="gridview"></a>GridView

Ovládací prvek GridView umožňuje zobrazit tabulková data a upravovat je pomocí deklarativního přístupu a je následníkem ovládacího prvku DataGrid. V ovládacím prvku GridView jsou k dispozici následující funkce.

- Vytvoření vazby na ovládací prvky zdroje dat, jako je SqlDataSource.
- Integrované možnosti řazení.
- Integrované aktualizace a odstraňování možností.
- Vestavěné možnosti stránkování.
- Integrované možnosti výběru řádků
- Programový přístup k objektovému modelu GridView, který umožňuje dynamicky nastavovat vlastnosti, zpracovávat události a tak dále.
- Více klíčových polí.
- Několik datových polí pro sloupce hypertextových odkazů
- Přizpůsobitelný vzhled pomocí motivů a stylů.

**Sloupcová pole**

Každý sloupec v ovládacím prvku GridView je reprezentován objektem DataControlField. Ve výchozím nastavení je vlastnost AutoGenerateColumns nastavena na **hodnotu true**, která vytvoří objekt AutoGeneratedField pro každé pole ve zdroji dat. Každé pole se pak vykreslí jako sloupec v ovládacím prvku GridView v pořadí, ve kterém se všechna pole zobrazí ve zdroji dat. Můžete také ručně určit, která sloupcová pole se zobrazí v ovládacím prvku **GridView** , nastavením vlastnosti **AutoGenerateColumns** na **hodnotu false** a následnou definicí vlastní kolekce polí sloupců. Různé typy sloupcových polí určují chování sloupců v ovládacím prvku.

V následující tabulce jsou uvedeny různé typy polí sloupců, které lze použít.

| **Typ sloupcového pole** | **Popis** |
| --- | --- |
| Vlastnost BoundField | Zobrazí hodnotu pole ve zdroji dat. Toto je výchozí typ sloupce ovládacího prvku GridView. |
| ButtonField | Zobrazí příkazové tlačítko pro každou položku v ovládacím prvku GridView. To vám umožní vytvořit sloupec vlastních ovládacích prvků tlačítko, jako je například přidání nebo tlačítko Odebrat. |
| CheckBoxField | Zobrazí zaškrtávací políčko pro každou položku v ovládacím prvku GridView. Tento typ sloupcového pole se běžně používá k zobrazení polí s logickou hodnotou. |
| CommandField | Zobrazí předdefinovaná příkazová tlačítka k provedení výběru, úprav nebo odstranění operací. |
| HyperLinkField | Zobrazí hodnotu pole ve zdroji dat jako hypertextový odkaz. Tento typ sloupcového pole umožňuje navazovat druhé pole na adresu URL hypertextového odkazu. |
| ImageField | Zobrazí obrázek pro každou položku v ovládacím prvku GridView. |
| Pole TemplateField | Zobrazuje uživatelsky definovaný obsah pro každou položku v ovládacím prvku GridView v závislosti na zadané šabloně. Tento typ sloupcového pole umožňuje vytvořit pole vlastního sloupce. |

Chcete-li definovat sloupcovou kolekci polí deklarativně, přidejte nejprve počáteční a uzavírací **&lt;sloupce&gt;** značky mezi otevírací a uzavírací značkou ovládacího prvku GridView. Dále uveďte pole sloupců, která chcete zahrnout mezi otevírací a uzavírací **&lt;sloupce&gt;** značky. Zadané sloupce se přidají do kolekce Columns v uvedeném pořadí. Kolekce **Columns** ukládá všechna pole sloupců v ovládacím prvku a umožňuje programově spravovat sloupcová pole v ovládacím prvku GridView.

Explicitně deklarovaná pole sloupce lze zobrazit v kombinaci s automaticky generovanými poli sloupců. Při použití obou se nejprve vykreslují explicitně deklarovaná pole sloupce a následně automaticky generovaná pole sloupců.

## <a name="binding-to-data"></a>Vytvoření vazby na data

Ovládací prvek GridView může být svázán s ovládacím prvkem zdroje dat (například **SqlDataSource**, **ObjectDataSource**atd.) a také jakýmkoli zdrojem dat, který implementuje rozhraní System. Collections. IEnumerable (například System. data. DataView, System. Collections. ArrayList nebo System. Collections. hash). K navázání ovládacího prvku GridView na příslušný typ zdroje dat použijte jednu z následujících metod:

- Chcete-li vytvořit vazby na ovládací prvek zdroje dat, nastavte vlastnost DataSourceID ovládacího prvku GridView na hodnotu ID ovládacího prvku zdroje dat. Ovládací prvek GridView se automaticky váže k určenému ovládacímu prvku zdroje dat a může využít možnosti ovládacího prvku zdroje dat k provádění řazení, aktualizace, odstranění a stránkování. Toto je upřednostňovaná metoda pro vytvoření vazby na data.
- Chcete-li vytvořit vazbu na zdroj dat, který implementuje rozhraní System. Collections. IEnumerable, programově nastavte vlastnost DataSource ovládacího prvku GridView na zdroj dat a zavolejte metodu DataBind. Při použití této metody ovládací prvek GridView neposkytuje integrované funkce řazení, aktualizace, odstranění a stránkování. Tuto funkci je potřeba poskytnout sami.

## <a name="data-operations"></a>Operace s daty

Ovládací prvek GridView poskytuje mnoho vestavěných funkcí, které umožňují uživateli řadit, aktualizovat, odstraňovat, vybírat a stránkovat prostřednictvím položek v ovládacím prvku. Když je ovládací prvek GridView svázán s ovládacím prvkem zdroje dat, může ovládací prvek GridView využít možnosti ovládacího prvku zdroje dat a poskytovat automatické řazení, aktualizaci a odstraňování funkcí.

> [!NOTE]
> Ovládací prvek GridView může poskytovat podporu pro řazení, aktualizaci a odstraňování s jinými typy zdrojů dat; k implementaci těchto operací ale budete muset poskytnout odpovídající obslužnou rutinu události.

Řazení umožňuje uživateli seřadit položky v ovládacím prvku GridView s ohledem na konkrétní sloupec kliknutím na záhlaví sloupce. Chcete-li povolit řazení, nastavte vlastnost AllowSorting na **hodnotu true**.

Funkce automatických aktualizací, odstraňování a výběru jsou povolené, když se na tlačítko ve sloupcovém poli **ButtonField** nebo **TemplateField** klikne s názvem příkazu "Upravit", "odstranit" a "vybrat", v uvedeném pořadí. Ovládací prvek GridView může automaticky přidat pole **CommandField** sloupce s tlačítkem upravit, odstranit nebo vybrat, pokud je vlastnost AutoGenerateEditButton, AutoGenerateDeleteButton nebo AutoGenerateSelectButton nastavena na **hodnotu true**(v uvedeném pořadí).

> [!NOTE]
> Vkládání záznamů do zdroje dat není přímo podporováno ovládacím prvkem GridView. Je však možné vkládat záznamy pomocí ovládacího prvku GridView ve spojení s ovládacím prvkem DetailsView nebo FormView.

Namísto zobrazení všech záznamů ve zdroji dat současně může ovládací prvek GridView automaticky rozdělit záznamy na stránky. Chcete-li povolit stránkování, nastavte vlastnost li AllowPaging nastavena na **hodnotu true**.

## <a name="customizing-the-user-interface"></a>Přizpůsobení uživatelského rozhraní

Vzhled ovládacího prvku GridView lze přizpůsobit nastavením vlastností stylu pro různé části ovládacího prvku. V následující tabulce jsou uvedeny různé vlastnosti stylu.

| **Vlastnost Style** | **Popis** |
| --- | --- |
| AlternatingRowStyle | Nastavení stylu pro řádky střídavých dat v ovládacím prvku GridView. Když je tato vlastnost nastavená, řádky dat se zobrazují střídavě mezi nastaveními RowStyle a nastavením **AlternatingRowStyle** . |
| EditRowStyle | Nastavení stylu pro upravovaný řádek v ovládacím prvku GridView. |
| EmptyDataRowStyle | Nastavení stylu pro prázdný řádek dat zobrazený v ovládacím prvku GridView, pokud zdroj dat neobsahuje žádné záznamy. |
| FooterStyle | Nastavení stylu pro řádek zápatí ovládacího prvku GridView. |
| HeaderStyle | Nastavení stylu řádku záhlaví ovládacího prvku GridView. |
| PagerStyle | Nastavení stylu řádku stránkování ovládacího prvku GridView. |
| RowStyle | Nastavení stylu pro datové řádky v ovládacím prvku GridView. Když je také nastavena vlastnost **AlternatingRowStyle** , řádky dat se zobrazují mezi nastaveními **RowStyle** a nastavením **AlternatingRowStyle** . |
| SelectedRowStyle | Nastavení stylu pro vybraný řádek v ovládacím prvku GridView. |

Můžete také zobrazit nebo skrýt různé části ovládacího prvku. V následující tabulce jsou uvedeny vlastnosti, které určují, které části se mají zobrazovat nebo skrývat.

| **Vlastnost** | **Popis** |
| --- | --- |
| ShowFooter | Zobrazí nebo skryje část zápatí ovládacího prvku GridView. |
| ShowHeader | Zobrazí nebo skryje oddíl záhlaví ovládacího prvku GridView. |

### <a name="events"></a>Události

Ovládací prvek GridView poskytuje několik událostí, které lze programovat proti. To umožňuje spuštění vlastní rutiny při každém výskytu události. V následující tabulce jsou uvedeny události, které ovládací prvek GridView podporuje.

| **Události** | **Popis** |
| --- | --- |
| PageIndexChanged | Nastane při kliknutí na jeden z tlačítek stránkování, ale poté, co ovládací prvek GridView zpracuje operaci stránkování. Tato událost se běžně používá v případě, že je potřeba provést úlohu, když uživatel přejde na jinou stránku v ovládacím prvku. |
| PageIndexChanging | Nastane při kliknutí na jeden z tlačítek stránkování, ale před tím, než ovládací prvek GridView zpracuje operaci stránkování. Tato událost se často používá ke zrušení operace stránkování. |
| RowCancelingEdit | Vyvolá se při kliknutí na tlačítko Storno řádku, ale před tím, než ovládací prvek GridViewu ukončí režim úprav. Tato událost se často používá k zastavení operace zrušení. |
| RowCommand | Nastane, pokud se klikne na tlačítko v ovládacím prvku GridView. Tato událost se často používá k provedení úkolu při kliknutí na tlačítko v ovládacím prvku. |
| RowCreated | Nastane, pokud se v ovládacím prvku GridView vytvoří nový řádek. Tato událost se často používá k úpravě obsahu řádku při vytvoření řádku. |
| RowDataBound | Vyvolá se v případě, že je datový řádek svázán s daty v ovládacím prvku GridView. Tato událost se často používá k úpravě obsahu řádku, pokud je řádek svázán s daty. |
| RowDeleted | Vyvolá se při kliknutí na tlačítko pro odstranění řádku, ale poté, co ovládací prvek GridView odstraní záznam ze zdroje dat. Tato událost se často používá ke kontrole výsledků operace odstranění. |
| RowDeleting | Vyvolá se při kliknutí na tlačítko pro odstranění řádku, ale před tím, než ovládací prvek GridView odstraní záznam ze zdroje dat. Tato událost se často používá ke zrušení operace odstranění. |
| RowEditing | Nastane, pokud se klikne na tlačítko pro úpravy řádku, ale před tím, než ovládací prvek GridView vstoupí do režimu úprav. Tato událost se často používá k zrušení operace úprav. |
| RowUpdated metody Update | Vyvolá se při kliknutí na tlačítko pro aktualizaci řádku, ale poté, co ovládací prvek GridView aktualizuje řádek. Tato událost se často používá ke kontrole výsledků operace aktualizace. |
| RowUpdating | Nastane, pokud se klikne na tlačítko pro aktualizaci řádku, ale ještě před tím, než ovládací prvek GridView aktualizuje řádek. Tato událost se často používá ke zrušení operace aktualizace. |
| SelectedIndexChanged | Vyvolá se při kliknutí na tlačítko pro výběr řádku, ale poté, co ovládací prvek GridView zpracuje operaci SELECT. Tato událost se často používá k provedení úkolu po výběru řádku v ovládacím prvku. |
| SelectedIndexChanging | Vyvolá se při kliknutí na tlačítko pro výběr řádku, ale před tím, než ovládací prvek GridView zpracuje operaci SELECT. Tato událost se často používá k zrušení operace výběru. |
| Standard | Nastane, pokud se klikne na hypertextový odkaz na řazení sloupce, ale poté, co ovládací prvek GridView zpracuje operaci řazení. Tato událost se běžně používá k provedení úkolu poté, co uživatel klikne na hypertextový odkaz k seřazení sloupce. |
| Řazení | Nastane, pokud se klikne na hypertextový odkaz na řazení sloupce, ale před tím, než ovládací prvek GridView zpracuje operaci řazení. Tato událost se často používá k zrušení operace řazení nebo k provedení vlastní rutiny řazení. |

## <a name="formview"></a>Třídě

Ovládací prvek FormView slouží k zobrazení jednoho záznamu ze zdroje dat. Je podobný ovládacímu prvku DetailsView s tím rozdílem, že zobrazuje uživatelsky definované šablony namísto polí řádků. Vytváření vlastních šablon nabízí větší flexibilitu při řízení způsobu zobrazení dat. Ovládací prvek FormView podporuje následující funkce:

- Vytvoření vazby na ovládací prvky zdroje dat, jako je SqlDataSource a ObjectDataSource.
- Integrované možnosti vkládání.
- Integrované aktualizace a odstraňování možností.
- Vestavěné možnosti stránkování.
- Programový přístup k objektovému modelu FormView, který umožňuje dynamicky nastavovat vlastnosti, zpracovávat události a tak dále.
- Přizpůsobitelný vzhled prostřednictvím uživatelsky definovaných šablon, motivů a stylů.

## <a name="templates"></a>Šablony

Pro ovládací prvek FormView pro zobrazení obsahu je nutné vytvořit šablony pro různé části ovládacího prvku. Většina šablon je volitelná; je však nutné vytvořit šablonu pro režim, ve kterém je ovládací prvek nakonfigurován. Například ovládací prvek FormView, který podporuje vkládání záznamů, musí mít definovanou šablonu pro vložení položky. Následující tabulka obsahuje seznam různých šablon, které můžete vytvořit.

| **Typ šablony** | **Popis** |
| --- | --- |
| EditItemTemplate | Definuje obsah pro řádek dat, pokud je ovládací prvek FormView v režimu úprav. Tato šablona obvykle obsahuje vstupní ovládací prvky a příkazová tlačítka, pomocí kterých může uživatel upravit existující záznam. |
| EmptyDataTemplate | Definuje obsah pro prázdný řádek dat zobrazený v případě, že je ovládací prvek FormView svázán se zdrojem dat, který neobsahuje žádné záznamy. Tato šablona obvykle obsahuje obsah, který uživateli upozorní, že zdroj dat neobsahuje žádné záznamy. |
| Šablona FooterTemplate | Definuje obsah pro řádek zápatí. Tato šablona obvykle obsahuje další obsah, který byste chtěli zobrazit v řádku zápatí. Jako alternativu můžete jednoduše zadat text, který se má zobrazit v řádku zápatí, nastavením vlastnosti FooterText. |
| Šablona HeaderTemplate | Definuje obsah pro řádek záhlaví. Tato šablona obvykle obsahuje další obsah, který byste chtěli zobrazit v řádku záhlaví. Jako alternativu můžete jednoduše zadat text, který se má zobrazit v řádku záhlaví nastavením vlastnosti HeaderText. |
| ItemTemplate | Definuje obsah pro řádek dat, pokud je ovládací prvek FormView v režimu jen pro čtení. Tato šablona obvykle obsahuje obsah pro zobrazení hodnot existujícího záznamu. |
| InsertItemTemplate | Definuje obsah pro řádek dat, pokud je ovládací prvek FormView v režimu vkládání. Tato šablona obvykle obsahuje vstupní ovládací prvky a příkazová tlačítka, pomocí kterých může uživatel přidat nový záznam. |
| PagerTemplate | Definuje obsah pro řádek stránkování zobrazený v případě, že je povolená funkce stránkování (Pokud je vlastnost li AllowPaging nastavena nastavena na **hodnotu true**). Tato šablona obvykle obsahuje ovládací prvky, se kterými může uživatel přejít na jiný záznam. |

Vstupní ovládací prvky v šabloně upravit položku a šablona vložení položky mohou být svázány s poli zdroje dat pomocí obousměrného výrazu vazby. To umožňuje ovládacímu prvku FormView automaticky extrahovat hodnoty ovládacího prvku vstupu pro operaci aktualizace nebo vložení. Obousměrné výrazy vazby také umožňují vstupní ovládací prvky v šabloně upravit položku pro automatické zobrazení původních hodnot polí.

### <a name="binding-to-data"></a>Vytvoření vazby na data

Ovládací prvek FormView může být svázán s ovládacím prvkem zdroje dat (například **SqlDataSource**, AccessDataSource, **ObjectDataSource** atd.) nebo k jakémukoli zdroji dat, který implementuje rozhraní System. Collections. IEnumerable (například System. data. DataView, System. Collections. ArrayList a System. Collections. hash). K navázání ovládacího prvku FormView na příslušný typ zdroje dat použijte jednu z následujících metod:

- Chcete-li vytvořit vazby na ovládací prvek zdroje dat, nastavte vlastnost DataSourceID ovládacího prvku FormView na hodnotu ID ovládacího prvku zdroje dat. Ovládací prvek FormView se automaticky váže k určenému ovládacímu prvku zdroje dat a může využít možnosti ovládacího prvku zdroje dat k provádění operací vložení, aktualizace, odstranění a stránkování. Toto je upřednostňovaná metoda pro vytvoření vazby na data.
- Chcete-li vytvořit vazbu na zdroj dat, který implementuje rozhraní **System. Collections. IEnumerable** , programově nastavte vlastnost DataSource ovládacího prvku FormView na zdroj dat a zavolejte metodu DataBind. Při použití této metody ovládací prvek FormView neposkytuje integrované funkce vkládání, aktualizace, odstranění a stránkování. Tuto funkci je potřeba poskytnout pomocí příslušné události.

## <a name="data-operations"></a>Operace s daty

Ovládací prvek FormView poskytuje mnoho vestavěných funkcí, které umožňují uživateli aktualizovat, odstraňovat, vkládat a stránkovat položky v ovládacím prvku. Když je ovládací prvek FormView svázán s ovládacím prvkem zdroje dat, může ovládací prvek FormView využít možnosti ovládacího prvku zdroje dat a poskytnout automatické aktualizace, odstranění, vložení a stránkování. Ovládací prvek FormView může poskytovat podporu pro operace aktualizace, odstranění, vložení a stránkování s jinými typy zdrojů dat; je však nutné poskytnout příslušnou obslužnou rutinu události s implementací pro tyto operace.

Vzhledem k tomu, že ovládací prvek FormView používá šablony, neposkytuje způsob, jak automaticky generovat příkazová tlačítka pro provádění aktualizací, odstraňování nebo vkládání operací. Tato příkazová tlačítka musíte do příslušné šablony přidat ručně. Ovládací prvek FormView rozpoznává určitá tlačítka, jejichž vlastnosti **příkazu** jsou nastaveny na konkrétní hodnoty. V následující tabulce jsou uvedena příkazová tlačítka, která ovládací prvek FormView rozpoznává.

| **Tlačítko** | **Hodnota příkazu Command** | **Popis** |
| --- | --- | --- |
| Zrušit | Operaci | Používá se při aktualizaci nebo vkládání operací k zrušení operace a k zahození hodnot zadaných uživatelem. Ovládací prvek FormView se pak vrátí do režimu určeného vlastností DefaultMode. |
| Odstranit | Dstranit | Používá se při odstraňování operací k odstranění zobrazeného záznamu ze zdroje dat. Vyvolává události ItemDeleting a ItemDeleted. |
| Upravit | Úpravě | Používá se při aktualizaci operací k umístění ovládacího prvku FormView do režimu úprav. Pro řádek dat se zobrazí obsah určený ve vlastnosti **EditItemTemplate** . |
| Vložit | Zadat | Používá se při vkládání operací k pokusu o vložení nového záznamu ve zdroji dat s použitím hodnot poskytnutých uživatelem. Vyvolává události ItemInserting a ItemInserted. |
| Nová | New | Používá se při vkládání operací k umístění ovládacího prvku FormView do režimu vkládání. Pro řádek dat se zobrazí obsah zadaný ve vlastnosti **Šablona InsertItemTemplate** . |
| Stránka | Page | Používá se v operacích stránkování k reprezentaci tlačítka v řádku pageru, který provádí stránkování. Chcete-li určit operaci stránkování, nastavte vlastnost **CommandArgument** tlačítka na "Next", "předchozí", "první", "poslední" nebo na index stránky, na kterou chcete přejít. Vyvolává události PageIndexChanging a PageIndexChanged. |
| Aktualizace | Update | Používá se při aktualizaci operací k pokusu o aktualizaci zobrazeného záznamu ve zdroji dat s hodnotami poskytnutými uživatelem. Vyvolává události ItemUpdating a ItemUpdated. |

Na rozdíl od tlačítka odstranit (který okamžitě odstraní zobrazený záznam) se při kliknutí na tlačítko Upravit nebo nový přejde ovládací prvek FormView do režimu úprav nebo vložení. V režimu úprav se pro aktuální datovou položku zobrazí obsah obsažený ve vlastnosti **EditItemTemplate** . Šablona upravit položku je obvykle definována tak, že tlačítko Upravit je nahrazeno pomocí aktualizace a tlačítka Storno. Vstupní ovládací prvky, které jsou vhodné pro datový typ pole (například textové pole nebo ovládací prvek CheckBox), se obvykle zobrazují s hodnotou pole pro uživatele, který chcete upravit. Kliknutím na tlačítko Aktualizovat aktualizujete záznam ve zdroji dat a kliknete-li na tlačítko Storno, zrušíte všechny změny.

Podobně platí, že obsah obsažený ve vlastnosti **Šablona InsertItemTemplate** je zobrazen pro datovou položku, pokud je ovládací prvek v režimu vkládání. Šablona vložení položky je obvykle definována tak, že nové tlačítko je nahrazeno tlačítkem INSERT a tlačítko Storno. pro uživatele jsou zobrazeny prázdné vstupní ovládací prvky pro zadání hodnot nového záznamu. Kliknutím na tlačítko Vložit vložíte záznam ve zdroji dat a kliknete na tlačítko zrušit a zrušíte všechny změny.

Ovládací prvek FormView poskytuje funkci stránkování, která umožňuje uživateli přejít na jiné záznamy ve zdroji dat. Je-li tato možnost povolena, je v ovládacím prvku FormView, který obsahuje ovládací prvky navigace stránky, zobrazen řádek stránkování. Chcete-li povolit stránkování, nastavte vlastnost **li AllowPaging nastavena** na **hodnotu true**. Řádek stránkování lze přizpůsobit nastavením vlastností objektů obsažených v PagerStyle a vlastnosti PagerSettings. Místo používání integrovaného uživatelského rozhraní řádku stránkování můžete vytvořit vlastní uživatelské rozhraní pomocí vlastnosti **PagerTemplate** .

## <a name="customizing-the-user-interface"></a>Přizpůsobení uživatelského rozhraní

Můžete přizpůsobit vzhled ovládacího prvku FormView nastavením vlastností stylu pro různé části ovládacího prvku. V následující tabulce jsou uvedeny různé vlastnosti stylu.

| **Vlastnost Style** | **Popis** |
| --- | --- |
| EditRowStyle | Nastavení stylu pro řádek dat, když je ovládací prvek FormView v režimu úprav. |
| EmptyDataRowStyle | Nastavení stylu pro prázdný řádek dat zobrazený v ovládacím prvku FormView, pokud zdroj dat neobsahuje žádné záznamy. |
| FooterStyle | Nastavení stylu pro řádek zápatí ovládacího prvku FormView |
| HeaderStyle | Nastavení stylu řádku záhlaví ovládacího prvku FormView |
| InsertRowStyle | Nastavení stylu pro řádek dat, když je ovládací prvek FormView v režimu vkládání. |
| PagerStyle | Nastavení stylu řádku stránkování zobrazeného v ovládacím prvku FormView, pokud je povolena funkce stránkování. |
| RowStyle | Nastavení stylu pro řádek dat, je-li ovládací prvek FormView v režimu jen pro čtení. |

## <a name="events"></a>Události

Ovládací prvek FormView poskytuje několik událostí, které lze programovat proti. To umožňuje spuštění vlastní rutiny při každém výskytu události. V následující tabulce jsou uvedeny události podporované ovládacím prvkem FormView.

| **Události** | **Popis** |
| --- | --- |
| ItemCommand | Nastane, pokud se klikne na tlačítko v rámci ovládacího prvku FormView. Tato událost se často používá k provedení úkolu při kliknutí na tlačítko v ovládacím prvku. |
| ItemCreated | Nastane po vytvoření všech objektů FormViewRow v ovládacím prvku FormView. Tato událost se často používá k úpravě hodnot záznamu před jeho zobrazením. |
| ItemDeleted | Nastane, pokud se klikne na tlačítko pro odstranění (tlačítko s vlastností **příkazového řádku** nastavenou na "odstranit"), ale poté, co ovládací prvek FormView odstraní záznam ze zdroje dat. Tato událost se často používá ke kontrole výsledků operace odstranění. |
| ItemDeleting | Nastane, pokud se klikne na tlačítko Odstranit, ale před tím, než ovládací prvek FormView odstraní záznam ze zdroje dat. Tato událost se často používá ke zrušení operace odstranění. |
| ItemInserted | Nastane, pokud se klikne na tlačítko pro vložení (na tlačítko s vlastností **příkazového řádku** nastavenou na "Insert"), ale poté, co ovládací prvek FormView vloží záznam. Tato událost se často používá ke kontrole výsledků operace vložení. |
| ItemInserting | Nastane, pokud se klikne na tlačítko Vložit, ale před tím, než ovládací prvek FormView vloží záznam. Tato událost se často používá ke zrušení operace INSERT. |
| ItemUpdated | Nastane, pokud se klikne na tlačítko pro aktualizaci (tlačítko s vlastností **příkazového řádku** nastavenou na "aktualizovat"), ale po aktualizaci řádku ovládací prvek FormView. Tato událost se často používá ke kontrole výsledků operace aktualizace. |
| ItemUpdating | Nastane, pokud se klikne na tlačítko Aktualizovat, ale předtím, než ovládací prvek FormView aktualizuje záznam. Tato událost se často používá k zrušení operace aktualizace. |
| ModeChanged | Vyvolá se poté, co ovládací prvek FormView mění režimy (pro úpravy, vložení nebo režim jen pro čtení). Tato událost se často používá k provedení úkolu, když ovládací prvek FormView mění režimy. |
| ModeChanging | Vyvolá se předtím, než ovládací prvek FormView mění režimy (pro úpravy, vložení nebo režim jen pro čtení). Tato událost se často používá ke zrušení změny režimu. |
| PageIndexChanged | Nastane při kliknutí na jeden z tlačítek stránkování, ale poté, co ovládací prvek FormView zpracuje operaci stránkování. Tato událost se běžně používá v případě, že je potřeba provést úlohu, když uživatel přejde na jiný záznam v ovládacím prvku. |
| PageIndexChanging | Nastane při kliknutí na jeden z tlačítek stránkování, ale před tím, než ovládací prvek FormView zpracuje operaci stránkování. Tato událost se často používá ke zrušení operace stránkování. |

## <a name="detailsview"></a>DetailsView

Ovládací prvek DetailsView slouží k zobrazení jednoho záznamu ze zdroje dat v tabulce, kde se každé pole záznamu zobrazuje v řádku tabulky. Dá se použít v kombinaci s ovládacím prvkem GridView pro scénáře hlavní-podrobnosti. Ovládací prvek DetailsView podporuje následující funkce:

- Vytvoření vazby na ovládací prvky zdroje dat, jako je SqlDataSource.
- Integrované možnosti vkládání.
- Integrované aktualizace a odstraňování možností.
- Vestavěné možnosti stránkování.
- Programový přístup k objektovému modelu DetailsView, který umožňuje dynamicky nastavovat vlastnosti, zpracovávat události a tak dále.
- Přizpůsobitelný vzhled pomocí motivů a stylů.

## <a name="row-fields"></a>Řádková pole

Každý řádek dat v ovládacím prvku DetailsView je vytvořen deklarováním ovládacího prvku pole. Různé typy polí řádků určují chování řádků v ovládacím prvku. Ovládací prvky pole jsou odvozeny z DataControlField. V následující tabulce jsou uvedeny různé typy polí řádků, které lze použít.

| **Typ sloupcového pole** | **Popis** |
| --- | --- |
| Vlastnost BoundField | Zobrazí hodnotu pole ve zdroji dat jako text. |
| ButtonField | Zobrazí příkazové tlačítko v ovládacím prvku DetailsView. To vám umožní zobrazit řádek s vlastním ovládacím prvkem tlačítka, jako je tlačítko Přidat nebo odebrat. |
| CheckBoxField | Zobrazí zaškrtávací políčko v ovládacím prvku DetailsView. Tento typ řádkového pole se běžně používá k zobrazení polí s logickou hodnotou. |
| CommandField | Zobrazí předdefinovaná příkazová tlačítka pro provádění operací úpravy, vložení nebo odstranění v ovládacím prvku DetailsView. |
| HyperLinkField | Zobrazí hodnotu pole ve zdroji dat jako hypertextový odkaz. Tento typ pole řádku umožňuje navazovat druhé pole na adresu URL hypertextového odkazu. |
| ImageField | Zobrazí obrázek v ovládacím prvku DetailsView. |
| Pole TemplateField | Zobrazuje uživatelsky definovaný obsah pro řádek v ovládacím prvku DetailsView v závislosti na zadané šabloně. Tento typ řádkového pole umožňuje vytvořit vlastní pole řádku. |

Ve výchozím nastavení je vlastnost AutoGenerateRows nastavena na **hodnotu true**, která automaticky generuje objekt vázaného řádkového pole pro každé pole typu s možností vazby ve zdroji dat. Platné typy s možností vazby jsou řetězce, hodnoty DateTime, Decimal, GUID a sady primitivních typů. Každé pole se pak zobrazí v řádku jako text v pořadí, ve kterém se jednotlivá pole zobrazí ve zdroji dat.

Automatické generování řádků poskytuje rychlý a snadný způsob, jak zobrazit všechna pole v záznamu. Chcete-li však použít pokročilé funkce ovládacího prvku DetailsView, je nutné explicitně deklarovat řádková pole, která mají být zahrnuta v ovládacím prvku DetailsView. Chcete-li deklarovat řádková pole, nejprve nastavte vlastnost **AutoGenerateRows** na **hodnotu false**. Dále přidejte pole pro otevření a zavření **&lt;&gt;** značky mezi otevíracími a ukončovacími značkami ovládacího prvku DetailsView. Nakonec uveďte řádková pole, která chcete zahrnout mezi otevírací a uzavírací **&lt;pole&gt;** značky. Zadaná řádková pole jsou přidána do kolekce Fields v uvedeném pořadí. Kolekce **pole** umožňuje programově spravovat řádková pole v ovládacím prvku DetailsView.

> [!NOTE]
> Automaticky generovaná pole řádků nejsou přidána do kolekce Fields.

## <a name="binding-to-data"></a>Vytvoření vazby na data

Ovládací prvek DetailsView může být svázán s ovládacím prvkem zdroje dat, jako je **SqlDataSource** nebo AccessDataSource, nebo na jakýkoli zdroj dat, který implementuje rozhraní System. Collections. IEnumerable, jako je System. data. DataView, System. Collections. ArrayList a System. Collections. hash.

Použijte jednu z následujících metod pro svázání ovládacího prvku DetailsView s příslušným typem zdroje dat:

- Chcete-li vytvořit vazby na ovládací prvek zdroje dat, nastavte vlastnost DataSourceID ovládacího prvku DetailsView na hodnotu ID ovládacího prvku zdroje dat. Ovládací prvek DetailsView se automaticky váže k určenému ovládacímu prvku zdroje dat. Toto je upřednostňovaná metoda pro vytvoření vazby na data.
- Chcete-li vytvořit vazbu na zdroj dat, který implementuje rozhraní **System. Collections. IEnumerable** , programově nastavte vlastnost DataSource ovládacího prvku DetailsView na zdroj dat a potom zavolejte metodu DataBind.

## <a name="security"></a>Zabezpečení

Tento ovládací prvek lze použít k zobrazení vstupu uživatele, který může obsahovat škodlivý klientský skript. Před zobrazením v aplikaci si Projděte všechny informace, které jsou odeslány z klienta pro spustitelný skript, příkazy jazyka SQL nebo jiný kód. ASP.NET poskytuje funkci ověřování vstupní žádosti pro blokování skriptu a HTML ve vstupu uživatele.

## <a name="data-operations"></a>Operace s daty

Ovládací prvek DetailsView poskytuje předdefinované možnosti, které uživateli umožňují aktualizovat, odstranit, vložit a umístit stránku pomocí položek v ovládacím prvku. Když je ovládací prvek DetailsView svázán s ovládacím prvkem zdroje dat, může ovládací prvek DetailsView využít možnosti ovládacího prvku zdroje dat a poskytnout automatické aktualizace, odstranění, vložení a stránkování.

Ovládací prvek DetailsView může poskytovat podporu pro operace aktualizace, odstranění, vložení a stránkování s jinými typy zdrojů dat; Nicméně je nutné poskytnout implementaci pro tyto operace v příslušné obslužné rutině události.

Ovládací prvek DetailsView může automaticky přidat pole **CommandField** řádku s tlačítkem upravit, odstranit nebo nový nastavením vlastností AutoGenerateEditButton, AutoGenerateDeleteButton nebo AutoGenerateInsertButton na **hodnotu true**(v uvedeném pořadí). Na rozdíl od tlačítka odstranit (který okamžitě odstraní vybraný záznam) se při kliknutí na tlačítko Upravit nebo nový přejde ovládací prvek DetailsView do režimu úprav nebo vložení v uvedeném pořadí. V režimu úprav je tlačítko Upravit nahrazeno pomocí aktualizace a tlačítka Storno. Vstupní ovládací prvky, které jsou vhodné pro datový typ pole (například textové pole nebo ovládací prvek CheckBox), se zobrazí s hodnotou pole pro uživatele, který chcete upravit. Kliknutím na tlačítko Aktualizovat aktualizujete záznam ve zdroji dat a kliknete-li na tlačítko Storno, zrušíte všechny změny. Podobně v režimu vkládání je tlačítko Nový nahrazeno tlačítkem INSERT a tlačítko Storno a pro uživatele jsou zobrazeny prázdné vstupní ovládací prvky pro zadání hodnot nového záznamu.

Ovládací prvek DetailsView poskytuje funkci stránkování, která umožňuje uživateli přejít na jiné záznamy ve zdroji dat. Pokud je povoleno, ovládací prvky pro navigaci na stránce se zobrazí v řádku stránkování. Chcete-li povolit stránkování, nastavte vlastnost li AllowPaging nastavena na **hodnotu true**. Řádek pageru se dá přizpůsobit pomocí vlastností PagerStyle a PagerSettings.

## <a name="customizing-the-user-interface"></a>Přizpůsobení uživatelského rozhraní

Můžete přizpůsobit vzhled ovládacího prvku DetailsView nastavením vlastností stylu pro různé části ovládacího prvku. V následující tabulce jsou uvedeny různé vlastnosti stylu.

| **Vlastnost Style** | **Popis** |
| --- | --- |
| AlternatingRowStyle | Nastavení stylu pro řádky střídavých dat v ovládacím prvku DetailsView. Když je tato vlastnost nastavená, řádky dat se zobrazují střídavě mezi nastaveními RowStyle a nastavením **AlternatingRowStyle** . |
| CommandRowStyle | Nastavení stylu řádku obsahujícího Vestavěná příkazová tlačítka v ovládacím prvku DetailsView. |
| EditRowStyle | Nastavení stylu pro datové řádky, je-li ovládací prvek DetailsView v režimu úprav. |
| EmptyDataRowStyle | Nastavení stylu pro prázdný řádek dat zobrazený v ovládacím prvku DetailsView, pokud zdroj dat neobsahuje žádné záznamy. |
| FooterStyle | Nastavení stylu pro řádek zápatí ovládacího prvku DetailsView. |
| HeaderStyle | Nastavení stylu řádku záhlaví ovládacího prvku DetailsView |
| InsertRowStyle | Nastavení stylu pro datové řádky, je-li ovládací prvek DetailsView v režimu vkládání. |
| PagerStyle | Nastavení stylu řádku stránkování ovládacího prvku DetailsView. |
| RowStyle | Nastavení stylu pro datové řádky v ovládacím prvku DetailsView. Když je také nastavena vlastnost **AlternatingRowStyle** , řádky dat se zobrazují mezi nastaveními **RowStyle** a nastavením **AlternatingRowStyle** . |
| FieldHeaderStyle | Nastavení stylu sloupce záhlaví ovládacího prvku DetailsView |

## <a name="events"></a>Události

Ovládací prvek DetailsView poskytuje několik událostí, které lze programovat proti. To umožňuje spuštění vlastní rutiny při každém výskytu události. V následující tabulce jsou uvedeny události, které ovládací prvek DetailsView podporuje. Ovládací prvek DetailsView také dědí tyto události z jeho základních tříd: DataBinding, DataBound, vyřazeno, init, Load, PreRender a Render.

| **Události** | **Popis** |
| --- | --- |
| ItemCommand | Nastane, pokud se klikne na tlačítko v ovládacím prvku DetailsView. |
| ItemCreated | Nastane po vytvoření všech objektů DetailsViewRow v ovládacím prvku DetailsView. Tato událost se často používá k úpravě hodnot záznamu před jeho zobrazením. |
| ItemDeleted | Nastane při kliknutí na tlačítko pro odstranění, ale poté, co ovládací prvek DetailsView odstraní záznam ze zdroje dat. Tato událost se často používá ke kontrole výsledků operace odstranění. |
| ItemDeleting | Nastane, pokud se klikne na tlačítko Odstranit, ale před tím, než ovládací prvek DetailsView odstraní záznam ze zdroje dat. Tato událost se často používá ke zrušení operace odstranění. |
| ItemInserted | Nastane, pokud se klikne na tlačítko vložení, ale po vložení záznamu ovládacím prvkem DetailsView. Tato událost se často používá ke kontrole výsledků operace vložení. |
| ItemInserting | Nastane, pokud se klikne na tlačítko Insert, ale před tím, než ovládací prvek DetailsView vloží záznam. Tato událost se často používá ke zrušení operace INSERT. |
| ItemUpdated | Nastane, pokud se klikne na tlačítko Aktualizovat, ale po aktualizaci řádku ovládacím prvkem DetailsView. Tato událost se často používá ke kontrole výsledků operace aktualizace. |
| ItemUpdating | Nastane, pokud se klikne na tlačítko pro aktualizaci, ale před aktualizací záznamu ovládacím prvkem DetailsView. Tato událost se často používá k zrušení operace aktualizace. |
| ModeChanged | Vyvolá se po změnách režimů ovládacího prvku DetailsView (režim úprav, vložení nebo režimu jen pro čtení). Tato událost se často používá k provedení úkolu, když ovládací prvek DetailsView mění režimy. |
| ModeChanging | Vyvolá se před změnou režimů ovládacího prvku DetailsView (režim úprav, vložení nebo režimu jen pro čtení). Tato událost se často používá ke zrušení změny režimu. |
| PageIndexChanged | Nastane při kliknutí na jeden z tlačítek stránkování, ale poté, co ovládací prvek DetailsView zpracuje operaci stránkování. Tato událost se běžně používá v případě, že je potřeba provést úlohu, když uživatel přejde na jiný záznam v ovládacím prvku. |
| PageIndexChanging | Nastane při kliknutí na jeden z tlačítek stránkování, ale před tím, než ovládací prvek DetailsView zpracuje operaci stránkování. Tato událost se často používá ke zrušení operace stránkování. |

## <a name="the-menu-control"></a>Ovládací prvek nabídky

Ovládací prvek nabídky v ASP.NET 2,0 je navržen jako plně vybavený navigační systém. Může to být snadno vázané na hierarchické zdroje dat, jako je například SiteMapDataSource.

Strukturu ovládacího prvku nabídky lze definovat deklarativně nebo dynamicky a skládá se z jednoho kořenového uzlu a libovolného počtu podřízených uzlů. Následující kód deklarativně definuje nabídku pro ovládací prvek nabídky.

[!code-aspx[Main](data-bound-controls/samples/sample4.aspx)]

V předchozím příkladu je uzel Home. aspx kořenovým uzlem. Všechny ostatní uzly jsou vnořené v rámci kořenového uzlu na různých úrovních.

Existují dva typy nabídek, které lze v ovládacím prvku nabídky vykreslit. statické nabídky a dynamické nabídky. Statické nabídky se skládají z položek nabídky, které jsou vždy viditelné. Dynamické nabídky se skládají z položek nabídky, které jsou viditelné pouze v případě, že na ně uživatel najede myší. Zákazníci mohou často Zaměňujte statické nabídky s nabídkami definovanými deklarativně a dynamickými nabídkami s nabídkami, které jsou datové vazby za běhu. Ve faktech se dynamická a statická menu nevztahují k metodě naplnění. Výrazy *static* a *Dynamic* odkazují pouze na to, zda je nabídka staticky zobrazená nebo se zobrazila pouze v případě, že uživatel provede nějakou akci.

Vlastnost **StaticDisplayLevels** se používá ke konfiguraci, kolik úrovní nabídky je statických a proto se ve výchozím nastavení zobrazuje. V příkladu výše by vlastnost **StaticDisplayLevels** nastavená na hodnotu 2 způsobila, že se v nabídce staticky zobrazí uzel domů, uzel hudba a uzel filmy. Všechny ostatní uzly budou dynamicky zobrazeny, když uživatel najede myší na nadřazený uzel.

Vlastnost **vlastností MaximumDynamicDisplayLevels** konfiguruje maximální počet dynamických úrovní, které nabídka umožňuje zobrazit. Všechny dynamické nabídky na úrovni vyšší než hodnota zadaná vlastností **vlastností MaximumDynamicDisplayLevels** jsou zahozeny.

> [!NOTE]
> Skoro se může stát, že se vám můžou objevit situace, kdy se nabídky nezobrazují z důvodu vlastnosti vlastností MaximumDynamicDisplayLevels. V těchto případech zajistěte, aby byla vlastnost dostatečně nastavená tak, aby umožňovala Zobrazit nabídky zákazníků.

## <a name="data-binding-the-menu-control"></a>Vázání dat do ovládacího prvku nabídky

Ovládací prvek nabídky může být svázán s libovolným hierarchickým zdrojem dat, například ovládacím prvkem SiteMapDataSource nebo XMLDataSource. Prvek SiteMapDataSource je nejčastěji používanou metodou pro datovou vazbu k ovládacímu prvku nabídky, protože v něm byly mimo soubor Web. sitemap a jeho schéma poskytuje známé rozhraní API k ovládacímu prvku nabídky. Níže uvedený výpis ukazuje jednoduchý soubor Web. sitemap.

[!code-xml[Main](data-bound-controls/samples/sample5.xml)]

Všimněte si, že v tomto případě je k dispozici pouze jeden kořenový element siteMapNode, v tomto případě domovského prvku. Pro každý z siteMapNode lze nakonfigurovat několik atributů. Nejběžněji používané atributy jsou:

- **Adresa URL** Určuje adresu URL, která se zobrazí, když uživatel klikne na položku nabídky. Pokud tento atribut není k dispozici, uzel bude po kliknutí jednoduše vrácen zpět.
- **název** Určuje text, který se zobrazí v položce nabídky.
- **Popis** Používá se jako dokumentace pro uzel. Také se zobrazí jako popis tlačítka, když je ukazatel myši umístěn nad uzlem.
- **siteMapFile** Povoluje vnořené mapy webu. Tento atribut musí odkazovat na soubor ASP.NET mapy webu ve správném formátu.
- **role** Umožňuje, aby se vzhled uzlu řídil ASP.NET oříznutím zabezpečení.

Všimněte si, že i když jsou tyto atributy všechny volitelné, chování nabídky nemusí být očekávané, pokud nejsou určeny. Například pokud atribut *URL* je zadán, ale atribut *Description* není, uzel nebude viditelný a neexistuje žádný způsob, jak přejít na zadanou adresu URL.

## <a name="controlling-a-menus-operation"></a>Řízení operace nabídek

Existuje několik vlastností, které mají vliv na provoz ovládacího prvku nabídky ASP.NET. vlastnost **Orientation** , vlastnost **DisappearAfter** , vlastnost **StaticItemFormatString** a vlastnost **StaticPopoutImageUrl** jsou pouze pár z nich.

- **Orientaci** lze nastavit buď *horizontálně* , nebo *vertikálně* , a určuje, zda jsou statické položky nabídky rozloženy vodorovně v řádku nebo svisle a navrstveny na sebe. Tato vlastnost nemá vliv na dynamické nabídky.
- Vlastnost **DisappearAfter** konfiguruje, jak dlouho by měla dynamická nabídka zůstat viditelná, i když je myš přesunuta z ní. Hodnota se zadává v milisekundách a výchozí hodnota je 500. Nastavení této vlastnosti na hodnotu-1 způsobí, že nabídka nebude automaticky zmizet. V takovém případě bude nabídka zmizí pouze v případě, že uživatel klikne mimo nabídku.
- Vlastnost **StaticItemFormatString** usnadňuje udržování konzistentních verbiage v systému nabídek. Když zadáte tuto vlastnost, *{0}* mělo by být zadáno místo popisu, který se zobrazí ve zdroji dat. Například pokud chcete, aby položka nabídky z cvičení vyvolala 1, navštivte stránku produkty atd. zadejte na {0} stránku pro StaticItemFormatString. Za běhu nahradí ASP.NET všechny výskyty {0} se správným popisem položky nabídky.
- Vlastnost **StaticPopoutImageUrl** určuje obrázek, který se používá k označení toho, že konkrétní uzel nabídky má podřízené uzly, na které je možné přistupovat najetím myší. Dynamické nabídky budou dál používat výchozí image.

## <a name="templated-menu-controls"></a>Ovládací prvky nabídky šablony

Ovládací prvek nabídky je ovládací prvek bez vizuálního vzhledu a umožňuje dva různé šablony ItemTemplate. Třídu StaticItemTemplate a třídu DynamicItemTemplate. Pomocí těchto šablon můžete do nabídek snadno přidat serverové ovládací prvky nebo uživatelské ovládací prvky.

Chcete-li upravit šablony v aplikaci Visual Studio .NET, klikněte na tlačítko Inteligentní značka v nabídce a vyberte možnost Upravit šablony. Pak si můžete vybrat mezi úpravou třídu StaticItemTemplate nebo třídu DynamicItemTemplate.

Jakékoli ovládací prvky přidané do třídu StaticItemTemplate se zobrazí v nabídce static při načtení stránky. Všechny ovládací prvky přidané do třídu DynamicItemTemplate se zobrazí ve všech místních nabídkách.

## <a name="menu-events"></a>Události nabídky

Ovládací prvek nabídky má dvě události, které jsou pro něj jedinečné; **MenuItemClicked** a událost **MenuItemDatabound** .

Událost MenuItemClicked se vyvolá při kliknutí na položku nabídky. Událost MenuItemDatabound se vyvolá, když je položka nabídky svázána s daty. **MenuEventArgs** , která je předána obslužné rutině události, poskytuje přístup k položce nabídky přes vlastnost Item.

## <a name="controlling-a-menus-appearance"></a>Řízení vzhledu nabídek

Můžete také ovlivnit vzhled ovládacího prvku nabídky pomocí jednoho nebo více různých stylů dostupných pro formátování nabídek. Mezi ně patří **StaticMenuStyle**, **DynamicMenuStyle**, **DynamicMenuItemStyle**, **DynamicSelectedStyle**a **DynamicHoverStyle**. Tyto vlastnosti jsou konfigurovány pomocí standardního řetězce ve stylu jazyka HTML. Například následující bude mít vliv na styl dynamických nabídek.

[!code-aspx[Main](data-bound-controls/samples/sample6.aspx)]

> [!NOTE]
> Pokud používáte některý z stylů najetí myší, je nutné přidat prvek &lt;&gt; Head do stránky s prvkem *runat* nastaveným na *Server*.

Ovládací prvky nabídky také podporují používání motivů ASP.NET 2,0.

## <a name="the-treeview-control"></a>Ovládací prvek TreeView

Ovládací prvek TreeView zobrazuje data ve stromové struktuře podobné. Stejně jako u ovládacího prvku nabídky lze snadno data svázat s libovolným hierarchickým zdrojem dat, jako je například prvek SiteMapDataSource.

První otázka, kterou zákazníci mohou položit na ovládacím prvku TreeView v ASP.NET 2,0, je, zda se vztahuje na WebControl ovládacího prvku TreeView IE, který byl k dispozici pro ASP.NET 1. x. Nejedná se o. Ovládací prvek TreeView ASP.NET 2,0 byl napsaný od základu a nabízí výrazné zlepšení nad ovládacím prvkem WebControl prvku TreeView služby IE, který byl dříve k dispozici.

Nezobrazuje se podrobnosti o navázání ovládacího prvku TreeView na mapu webu, protože je proveden přesně stejným způsobem jako ovládací prvek nabídky. Nicméně ovládací prvek TreeView má odlišná rozdíl v způsobu, jakým funguje.

Ve výchozím nastavení se ovládací prvek TreeView zobrazuje plně rozbalený. Chcete-li změnit úroveň rozšíření při počátečním zatížení, upravte vlastnost **ExpandDepth** ovládacího prvku. To je obzvláště důležité v případech, kdy je TreeView svázán s daty při rozšiřování konkrétních uzlů.

## <a name="databinding-the-treeview-control"></a>Vázání dat na ovládací prvek TreeView

Na rozdíl od ovládacího prvku nabídky se strom TreeView sám hodí ke zpracování velkých objemů dat. Kromě vázání dat na prvek SiteMapDataSource nebo XMLDataSource je tedy TreeView často datová vazba na datovou sadu nebo jiná relační data. V případech, kdy je ovládací prvek TreeView svázán s velkými objemy dat, je nejlepší vytvořit vazbu pouze na data, která jsou ve skutečnosti viditelná v ovládacím prvku. Pak můžete vytvořit datovou vazby na další data, protože uzly TreeView budou rozbaleny.

V těchto případech by vlastnost **vlastnost PopulateOnDemand** prvku TreeView měla být nastavena na *hodnotu true*. Pak budete muset zadat implementaci metody **TreeNodePopulate** .

## <a name="data-binding-without-postback"></a>Datová vazba bez zpětného odeslání

Všimněte si, že když rozbalíte uzel v předchozím příkladu, stránka se vrátí zpátky a aktualizuje. Nejedná se o problém v tomto příkladu, ale můžete si představit, že se může nacházet v produkčním prostředí s velkým množstvím dat. Lepším scénářem je jeden z nich, ve kterém bude TreeView pořád dynamicky plnit své uzly, ale bez odeslání zpět na server.

Nastavením **PopulateNodesFromClient** a vlastností **vlastnost PopulateOnDemand** na hodnotu true bude ovládací prvek ASP.NET TreeView dynamicky naplnit uzly bez zpětného odeslání. Při rozbalení nadřazeného uzlu se z klienta provede požadavek XMLHttp a aktivuje se událost OnTreeNodePopulate. Server odpoví pomocí datového ostrůvku XML, který je pak použit k vytváření datových vazeb podřízených uzlů.

ASP.NET dynamicky vytvoří klientský kód, který implementuje tuto funkci. Skript &lt;&gt; značky, které obsahují skript, jsou vygenerovány ukazující na soubor AXD. Například níže uvedený výpis zobrazuje odkazy skriptu pro kód skriptu, který generuje požadavek XMLHttp.

[!code-html[Main](data-bound-controls/samples/sample7.html)]

Pokud v prohlížeči procházíte soubor AXD výše a otevřete ho, zobrazí se kód, který implementuje požadavek XMLHttp. Tato metoda brání zákazníkům v úpravách souboru skriptu.

## <a name="controlling-the-operation-of-the-treeview-control"></a>Řízení operace ovládacího prvku TreeView

Ovládací prvek TreeView má několik vlastností, které mají vliv na provoz ovládacího prvku. Nejzřejmější vlastnosti jsou **ShowCheckBoxes**, **ShowExpandCollapse**a **ShowLines**.

Vlastnost **ShowCheckBoxes** má vliv na to, zda se při vykreslení v uzlech zobrazí zaškrtávací políčko. Platné hodnoty této vlastnosti jsou **none**, **root**, **nadřazený**, **list**a **All**. Tyto prvky ovlivňují ovládací prvek TreeView následujícím způsobem:

| **Hodnota vlastnosti** | **Účinek** |
| --- | --- |
| Žádná | V žádných uzlech se nezobrazují zaškrtávací políčka. Toto je výchozí nastavení. |
| Kořen | Zaškrtávací políčko se zobrazí pouze v kořenovém uzlu. |
| Nadřazené | Zaškrtávací políčko se zobrazí pouze v uzlech s podřízenými uzly. Tyto podřízené uzly mohou být nadřazené uzly nebo uzly typu list. |
| Listu | Zaškrtávací políčko se zobrazí pouze v uzlech bez podřízených uzlů. |
| Vše | Zaškrtávací políčko se zobrazí na všech uzlech. |

Když se používají zaškrtávací políčka, vlastnost **CheckedNodes** vrátí kolekci uzlů TreeView, které jsou kontrolovány při zpětném odeslání.

Vlastnost **ShowExpandCollapse** ovládá vzhled obrázku rozbalení nebo sbalení vedle kořenových a nadřazených uzlů. Pokud je tato vlastnost nastavená na **false**, uzly TreeView se vykreslují jako hypertextové odkazy a rozbalí se a sbalí kliknutím na odkaz.

Vlastnost **ShowLines** určuje, zda jsou řádky zobrazovány s připojením nadřazených uzlů k podřízeným uzlům. Pokud má **hodnotu false** (výchozí), nezobrazí se žádné řádky. Při **hodnotě true**bude ovládací prvek TreeView používat obrázky čar ve složce určené vlastností **LineImagesFolder** .

Chcete-li přizpůsobit vzhled čar TreeView, Visual Studio .NET 2005 obsahuje nástroj pro návrháře čar. K tomuto nástroji můžete přistupovat pomocí tlačítka inteligentní značka v ovládacím prvku TreeView, jak je uvedeno níže.

![](data-bound-controls/_static/image1.jpg)

**Obrázek 1**

Když vyberete možnost nabídky **Přizpůsobit obrázky čáry** , spustí se nástroj Návrhář čáry, který vám umožní nakonfigurovat vzhled řádků TreeView.

## <a name="treeview-events"></a>Události TreeView

Ovládací prvek TreeView má následující jedinečné události:

- K SelectedNodeChanged dojde, když je vybrán uzel založený na vlastnosti **SelectAction** .
- K TreeNodeCheckChanged dojde, když se změní stav uzlů.
- K TreeNodeExpanded dojde, když je uzel rozbalený na základě vlastnosti **SelectAction** .
- K TreeNodeCollapsed dojde, když je uzel sbalen.
- K TreeNodeDataBound dojde, když je uzel vázaný na data.
- K TreeNodePopulate dojde, když se naplní uzel.

Vlastnost **SelectAction** umožňuje nakonfigurovat událost, která se aktivuje při výběru uzlu. Vlastnost SelectAction poskytuje následující akce:

- TreeNodeSelectAction. expand vyvolá TreeNodeExpanded při výběru uzlu.
- TreeNodeSelectAction. None nevyvolává žádnou událost, pokud je vybrán uzel.
- TreeNodeSelectAction. Select vyvolá událost SelectedNodeChanged, když je vybrán uzel.
- TreeNodeSelectAction. SelectExpand vyvolá událost SelectedNodeChanged a událost TreeNodeExpanded při výběru uzlu.

## <a name="controlling-appearance-with-styles"></a>Řízení vzhledu pomocí stylů

Ovládací prvek TreeView poskytuje mnoho vlastností pro řízení vzhledu ovládacího prvku pomocí stylů. K dispozici jsou následující vlastnosti.

| **Název vlastnosti** | **Ovládací prvky** |
| --- | --- |
| HoverNodeStyle | Určuje styl uzlů v případě, že je ukazatel myši umístěn nad nimi. |
| LeafNodeStyle | Určuje styl listů uzlů. |
| NodeStyle | Určuje styl pro všechny uzly. Konkrétní styly uzlů (například LeafNodeStyle) přepíší tento styl. |
| ParentNodeStyle | Určuje styl pro všechny nadřazené uzly. |
| RootNodeStyle | Určuje styl kořenového uzlu. |
| SelectedNodeStyle | Určuje styl pro vybraný uzel. |

Každá z těchto vlastností je určena jen pro čtení. Všechny však vrátí objekt **TreeNodeStyle** a vlastnosti tohoto objektu lze upravit pomocí formátu *podvlastností vlastnosti* . Například pro nastavení vlastnosti **ForeColor** pro **SelectedNodeStyle**byste měli použít následující syntaxi:

[!code-aspx[Main](data-bound-controls/samples/sample8.aspx)]

Všimněte si, že výše uvedená značka není uzavřená. To znamená, že při použití deklarativní syntaxe, kterou tady vidíte, byste měli také uzly TreeView v kódu HTML.

Vlastnosti stylu lze také zadat v kódu pomocí *vlastnosti vlastnost. Subproperty* . Chcete-li například nastavit vlastnost **ForeColor** **RootNodeStyle** v kódu, použijte následující syntaxi:

[!code-csharp[Main](data-bound-controls/samples/sample9.cs)]

> [!NOTE]
> Úplný seznam různých vlastností stylu naleznete v dokumentaci MSDN k objektu TreeNodeStyle.

## <a name="the-sitemappath-control"></a>Ovládací prvek SiteMapPath

Ovládací prvek SiteMapPath poskytuje chléb cesty navigační ovládací prvek pro vývojáře ASP.NET. Stejně jako ostatní navigační ovládací prvky lze snadno data svázat s hierarchickými zdroji dat, jako jsou například SiteMapDataSource nebo XmlDataSource.

Ovládací prvek SiteMapPath je tvořen objekty SiteMapNodeItem. Existují tři typy uzlů. Kořenový uzel, nadřazené uzly a aktuální uzel. Kořenový uzel je uzel v horní části hierarchické struktury. Aktuální uzel představuje aktuální stránku. Všechny ostatní uzly jsou nadřazené uzly.

## <a name="controlling-the-operation-of-the-sitemappath-control"></a>Řízení operace ovládacího prvku SiteMapPath

Vlastnosti, které řídí fungování ovládacího prvku SiteMapPath, jsou následující:

| **Vlastnost** | **Popis vlastnosti** |
| --- | --- |
| ParentLevelsDisplayed | Určuje, kolik nadřazených uzlů se zobrazuje. Výchozí hodnota je-1, což znamená, že počet zobrazených nadřazených uzlů není nijak omezen. |
| PathDirection | Řídí směr prvku SiteMapPath. Platné hodnoty jsou RootToCurrent (výchozí) a CurrentToRoot. |
| PathSeparator | Řetězec, který řídí znak, který odděluje uzly v ovládacím prvku SiteMapPath. Výchozí hodnota je:. |
| RenderCurrentNodeAsLink | Logická hodnota, která určuje, zda je aktuální uzel vykreslen jako odkaz. Výchozí hodnota je False. |
| SkipLinkText | Pomáhá s přístupností při zobrazení stránky čtečkami obrazovky. Tato vlastnost umožňuje čtenářům obrazovky přeskočit ovládací prvek SiteMapPath. Chcete-li tuto funkci zakázat, nastavte vlastnost na hodnotu String. Empty. |

## <a name="templated-sitemappath-controls"></a>Šablony ovládací prvky SiteMapPath

SiteMapControl je ovládací prvek bez vizuálního vzhledu a jako takový lze definovat různé šablony pro použití při zobrazení ovládacího prvku. Chcete-li upravit šablony v ovládacím prvku SiteMapPath, klikněte na tlačítko Inteligentní značka na ovládacím prvku a v nabídce vyberte možnost Upravit šablony. Tím se zobrazí nabídka SiteMapTasks, jak je uvedeno níže, kde si můžete vybrat z různých dostupných šablon.

![](data-bound-controls/_static/image2.jpg)

**Obrázek 2**

Šablona **NodeTemplate** odkazuje na libovolný uzel v rámci SiteMapPath. Pokud je uzel kořenovým uzlem, nebo aktuální uzel a je nakonfigurován **RootNodeTemplate** nebo **CurrentNodeTemplate** , bude NodeTemplate přepsán.

## <a name="sitemappath-events"></a>Události SiteMapPath

Ovládací prvek SiteMapPath má dvě události, které nejsou odvozeny od třídy ovládacího prvku; událost **ItemCreated** a událost **ItemDataBound** . Událost ItemCreated se vyvolá při vytvoření položky SiteMapPath. ItemDataBound je vyvolána při volání metody DataBind během datové vazby uzlu SiteMapPath. Objekt **SiteMapNodeItemEventArgs** poskytuje přístup ke konkrétnímu SiteMapNodeItem prostřednictvím vlastnosti Item.

## <a name="controlling-appearance-with-styles"></a>Řízení vzhledu pomocí stylů

Následující styly jsou k dispozici pro formátování ovládacího prvku SiteMapPath.

| **Název vlastnosti** | **Ovládací prvky** |
| --- | --- |
| CurrentNodeStyle | Určuje styl textu pro aktuální uzel. |
| RootNodeStyle | Určuje styl textu pro kořenový uzel. |
| NodeStyle | Určuje styl textu pro všechny uzly za předpokladu, že se nepoužije CurrentNodeStyle nebo RootNodeStyle. |

Vlastnost NodeStyle je přepsána buď CurrentNodeStyle, nebo RootNodeStyle. Každá z těchto vlastností je jen pro čtení a vrátí objekt **style** . Chcete-li ovlivnit vzhled uzlu pomocí jedné z těchto vlastností, budete muset nastavit vlastnosti vráceného objektu Style. Například kód níže změní vlastnost ForeColor aktuálního uzlu.

[!code-aspx[Main](data-bound-controls/samples/sample10.aspx)]

Vlastnost lze také použít programově následujícím způsobem:

[!code-csharp[Main](data-bound-controls/samples/sample11.cs)]

> [!NOTE]
> Pokud se použije šablona, styl se nepoužije.

## <a name="lab-1-configuring-an-aspnet-menu-control"></a>Testovací prostředí 1: konfigurace ovládacího prvku nabídky ASP.NET

1. Vytvoří nový web.
2. Přidejte soubor mapy webu tak, že vyberete soubor, nový, soubor a kliknete na mapa webu ze seznamu šablon souborů.
3. Otevřete mapu webu (ve výchozím nastavení Web. sitemap) a upravte ji tak, aby vypadala jako v následujícím seznamu. Stránky, na které propojujete v souboru mapy webu, neexistují, ale nejedná se o problém tohoto cvičení.

    [!code-xml[Main](data-bound-controls/samples/sample12.xml)]
4. Otevřete výchozí webový formulář v zobrazení Návrh.
5. V navigační oblasti sady nástrojů přidejte na stránku nový ovládací prvek nabídky.
6. V části data v sadě nástrojů přidejte nové ovládací prvky SiteMapDataSource. SiteMapDataSource bude automaticky používat soubor Web. Sitemap na vašem webu. (Soubor Web. sitemap *musí* být v kořenové složce webu.)
7. Klikněte na ovládací prvek nabídky a potom klikněte na tlačítko Inteligentní značka. zobrazí se dialogové okno úlohy nabídky.
8. V rozevíracím seznamu zvolit zdroj dat vyberte možnost SiteMapDataSource1.
9. Klikněte na odkaz automatický formát a vyberte formát pro nabídku.
10. V podokně Vlastnosti nastavte vlastnost **StaticDisplayLevels** na hodnotu 2. Ovládací prvek nabídky by nyní měl v Návrháři zobrazit uzel domů, produkty a služby.
11. Přejděte na stránku v prohlížeči a použijte nabídku. (Vzhledem k tomu, že stránky, které jste přidali do mapy webu, ve skutečnosti neexistují, při pokusu o jejich procházení se zobrazí chyba.)

Experimentujte se změnou StaticDisplayLevels a vlastností vlastností MaximumDynamicDisplayLevels a podívejte se, jak mají vliv na to, jak se nabídka vykreslí.

## <a name="lab-2-dynamically-binding-a-treeview-control"></a>Lab 2: dynamické vázání ovládacího prvku TreeView

Toto cvičení předpokládá, že máte SQL Server spuštěno místně a že databáze Northwind je k dispozici v instanci SQL Server. Pokud tyto podmínky nejsou splněné, změňte prosím připojovací řetězec v ukázce. Všimněte si, že možná budete muset místo důvěryhodného připojení zadat SQL Server ověřování.

1. Vytvoří nový web.
2. Přepněte do zobrazení kódu pro default. aspx a nahraďte veškerý kód následujícím kódem uvedeným níže. 

    [!code-aspx[Main](data-bound-controls/samples/sample13.aspx)]
3. Uložte stránku jako TreeView. aspx.
4. Procházejte stránku.
5. Po prvním zobrazení stránky zobrazte zdroj stránky v prohlížeči. Všimněte si, že klientovi byly odeslány pouze viditelné uzly.
6. Klikněte na symbol plus vedle libovolného uzlu.
7. Znovu zobrazit zdroj na stránce. Všimněte si, že nově zobrazené uzly jsou nyní k dispozici.

## <a name="lab-3-details-view-and-editing-data-using-a-gridview-and-detailsview"></a>Lab 3: zobrazení podrobností a úprava dat pomocí prvku GridView a DetailsView

1. Vytvoří nový web.
2. Přidejte do webu nový web. config.
3. Přidejte připojovací řetězec do souboru Web. config, jak je znázorněno níže: 

    [!code-xml[Main](data-bound-controls/samples/sample14.xml)]

    > [!NOTE]
    > V závislosti na vašem prostředí možná budete muset změnit připojovací řetězec.
4. Uložte a zavřete soubor Web. config.
5. Otevřete default. aspx a přidejte nový ovládací prvek SqlDataSource.
6. Změňte ID ovládacího prvku SqlDataSource na **Products**.
7. V nabídce **Úkoly SqlDataSource** klikněte na **Konfigurovat zdroj dat**.
8. V rozevíracím seznamu připojení vyberte **Northwind** a klikněte na další.
9. V rozevíracím seznamu **název** vyberte **produkty** a zaškrtněte políčka **ProductID**, **ProductName**, **UnitPrice**a **JednotkyNaSkladě** , jak je znázorněno níže. 

![](data-bound-controls/_static/image3.jpg)

    **Figure 3**
10. Klikněte na **Další**.
11. Klikněte na **Finish** (Dokončit).
12. Přepněte do zobrazení zdroje a Prohlédněte si kód, který byl vygenerován. Všimněte si vlastnosti **SelectCommand**, **DeleteCommand**, **InsertCommand**a **UpdateCommand** , které byly přidány do ovládacího prvku SqlDataSource. Všimněte si také přidaných parametrů.
13. Přepněte na zobrazení Návrh a přidejte na stránku nový ovládací prvek GridView.
14. V rozevíracím seznamu **Zvolit zdroj dat** vyberte **produkty** .
15. Zaškrtněte **možnost Povolit stránkování** a **Povolit výběr** , jak je znázorněno níže. 

![](data-bound-controls/_static/image4.jpg)

    **Figure 4**
16. Klikněte na odkaz **Upravit sloupce** a ujistěte se, že je zaškrtnuté políčko **automaticky generovat pole** .
17. Klikněte na tlačítko **OK**.
18. Po výběru ovládacího prvku GridView klikněte na tlačítko vedle vlastnosti **DataKeyNames** v podokně Vlastnosti.
19. Vyberte **ProductID** ze seznamu **dostupná datová pole** a kliknutím na tlačítko **&gt;** ho přidejte.
20. Klikněte na tlačítko OK.
21. Přidejte na stránku nový ovládací prvek SqlDataSource.
22. Změňte ID ovládacího prvku SqlDataSource na **Podrobnosti**.
23. V nabídce Úkoly SqlDataSource vyberte **Konfigurovat zdroj dat**.
24. V rozevíracím seznamu vyberte **Northwind** a klikněte na **Další**.
25. V rozevíracím seznamu <strong>název</strong> vyberte <strong>produkty</strong> a zaškrtněte políčko <strong>\</Strong > * v seznamu <strong>sloupce</strong> .
26. Klikněte na tlačítko **kde** .
27. Z rozevíracího seznamu **sloupec** vyberte **ProductID** .
28. V rozevíracím seznamu Operátor vyberte **=** .
29. V rozevíracím seznamu **zdroj** vyberte **ovládací prvek** .
30. Z rozevíracího seznamu **ID ovládacího prvku** vyberte **GridView1** .
31. Kliknutím na tlačítko **Přidat** přidejte klauzuli WHERE.
32. Klikněte na tlačítko **OK**.
33. Klikněte na tlačítko **Upřesnit** a zaškrtněte políčko **Generovat příkazy INSERT, Update a DELETE** .
34. Klikněte na tlačítko **OK**.
35. Klikněte na **Další** a potom na **Dokončit**.
36. Přidejte ovládací prvek DetailsView na stránku.
37. V rozevíracím seznamu **Zvolit zdroj dat** vyberte možnost **Podrobnosti**.
38. Zaškrtněte políčko **Povolit úpravy** , jak je uvedeno níže. 

![](data-bound-controls/_static/image1.gif)

    **Figure 5**
39. Uložte stránku a přejděte na Default. aspx.
40. Kliknutím na odkaz **Vybrat** vedle různých záznamů zobrazíte automatické aktualizace ovládacího prvku DetailsView.
41. Klikněte na odkaz **Upravit** v ovládacím prvku DetailsView.
42. Proveďte změnu záznamu a klikněte na **aktualizovat**.

---
uid: web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs
title: Provádění dávkových aktualizacíC#() | Microsoft Docs
author: rick-anderson
description: Naučte se, jak vytvořit plně upravitelný prvek DataList, kde jsou všechny jeho položky v režimu úprav a jejichž hodnoty se dají uložit kliknutím na tlačítko Aktualizovat vše na...
ms.author: riande
ms.date: 10/30/2006
ms.assetid: 57743ca7-5695-4e07-aed1-44b297f245a9
msc.legacyurl: /web-forms/overview/data-access/editing-and-deleting-data-through-the-datalist/performing-batch-updates-cs
msc.type: authoredcontent
ms.openlocfilehash: cde12a4d24555216adc49dd02818901278932eaa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78593539"
---
# <a name="performing-batch-updates-c"></a>Provádění dávkových aktualizací (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_37_CS.exe) nebo [Stáhnout PDF](performing-batch-updates-cs/_static/datatutorial37cs1.pdf)

> Naučte se, jak vytvořit plně upravitelný prvek DataList, kde jsou všechny jeho položky v režimu úprav a jejichž hodnoty se dají uložit kliknutím na tlačítko Aktualizovat vše na stránce.

## <a name="introduction"></a>Úvod

V [předchozím kurzu](an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md) jsme prozkoumali, jak vytvořit prvek DataList na úrovni položky. Podobně jako u standardních upravitelných prvků GridView, každá položka v prvku DataList zahrnovala tlačítko pro úpravy, které po kliknutí umožní upravit položku. I když tato úprava na úrovni položek funguje dobře pro data, která se aktualizují pouze občas, některé scénáře použití vyžadují, aby uživatel upravoval mnoho záznamů. Pokud uživatel potřebuje upravit desítky záznamů a je nucen kliknout na upravit, provést změny a kliknout na tlačítko Aktualizovat pro každé z nich, může se po kliknutí na tuto produktivitu považovat za překážku. V takových situacích lepší možností je poskytnout plně upravitelný prvek DataList *, který je* v režimu úprav a jehož hodnoty lze upravit kliknutím na tlačítko Aktualizovat vše na stránce (viz obrázek 1).

[![každou položku v plně upravitelném prvku DataList je možné upravit.](performing-batch-updates-cs/_static/image2.png)](performing-batch-updates-cs/_static/image1.png)

**Obrázek 1**: každou položku v plně upravitelném prvku DataList je možné upravit ([kliknutím zobrazíte obrázek v plné velikosti).](performing-batch-updates-cs/_static/image3.png)

V tomto kurzu podíváme se, jak uživatelům umožnit aktualizovat informace o adresách dodavatelů pomocí plně upravitelného prvku DataList.

## <a name="step-1-create-the-editable-user-interface-in-the-datalist-s-itemtemplate"></a>Krok 1: vytvoření upravitelného uživatelského rozhraní v DataList s ItemTemplate

V předchozím kurzu, kde vytvoříme standardní a upravitelný prvek DataList na úrovni položky, jsme použili dvě šablony:

- `ItemTemplate` obsahuje uživatelské rozhraní jen pro čtení (webové ovládací prvky Label pro zobrazení jednotlivých názvů a cen produktů).
- `EditItemTemplate` obsahuje uživatelské rozhraní režimu úprav (dva webové ovládací prvky TextBox).

Vlastnost DataList s `EditItemIndex` určuje, co `DataListItem` (pokud existuje) je vykresleno pomocí `EditItemTemplate`. Konkrétně `DataListItem`, jehož `ItemIndex` hodnota odpovídá vlastnosti `EditItemIndex` prvku DataList s, je vykreslen pomocí `EditItemTemplate`. Tento model funguje dobře, když se dá upravovat jenom jedna položka, ale při vytváření plně upravitelného prvku DataList dojde k rozběhu.

Pro plně upravitelný prvek DataList chceme, aby *všechny* `DataListItem` s byly vykresleny pomocí upravitelného rozhraní. Nejjednodušší způsob, jak to provést, je definovat upravitelné rozhraní v `ItemTemplate`. Pro úpravu informací o adrese dodavatele obsahuje upravitelné rozhraní název dodavatele jako text a potom textová pole pro hodnoty adresa, město a země.

Začněte tím, že otevřete stránku `BatchUpdate.aspx`, přidáte ovládací prvek DataList a nastavíte jeho vlastnost `ID` na `Suppliers`. Z inteligentní značky DataList s Přihlaste se k přidání nového ovládacího prvku ObjectDataSource s názvem `SuppliersDataSource`.

[![vytvořit nový prvek ObjectDataSource s názvem SuppliersDataSource](performing-batch-updates-cs/_static/image5.png)](performing-batch-updates-cs/_static/image4.png)

**Obrázek 2**: vytvoření nového prvku ObjectDataSource s názvem `SuppliersDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](performing-batch-updates-cs/_static/image6.png))

Nakonfigurujte prvek ObjectDataSource tak, aby načetl data pomocí metody `SuppliersBLL` třídy s `GetSuppliers()` (viz obrázek 3). Stejně jako v předchozím kurzu, namísto aktualizace informací o dodavatelích prostřednictvím ObjectDataSource, budeme pracovat přímo s vrstvou obchodní logiky. Proto na kartě aktualizace nastavte rozevírací seznam na (žádné) (viz obrázek 4).

[![načíst informace o dodavateli pomocí metody getsuppliers ()](performing-batch-updates-cs/_static/image8.png)](performing-batch-updates-cs/_static/image7.png)

**Obrázek 3**: načtení informací o dodavateli pomocí metody `GetSuppliers()` ([kliknutím zobrazíte obrázek v plné velikosti](performing-batch-updates-cs/_static/image9.png))

[![nastavte rozevírací seznam na (žádné) na kartě aktualizace.](performing-batch-updates-cs/_static/image11.png)](performing-batch-updates-cs/_static/image10.png)

**Obrázek 4**: Nastavení rozevíracího seznamu na (žádné) na kartě aktualizace ([kliknutím zobrazíte obrázek v plné velikosti](performing-batch-updates-cs/_static/image12.png))

Po dokončení Průvodce aplikace Visual Studio automaticky vygeneruje `ItemTemplate` DataList s pro zobrazení každého datového pole vráceného zdrojem dat ve webovém ovládacím prvku popisek. Musíme tuto šablonu upravit, aby místo toho poskytovala rozhraní pro úpravy. `ItemTemplate` lze přizpůsobit pomocí návrháře pomocí možnosti Upravit šablony z inteligentní značky DataList s nebo přímo prostřednictvím deklarativní syntaxe.

Počkejte, než se vytvoří rozhraní pro úpravy, které zobrazí název dodavatele jako text, ale obsahuje textová pole pro hodnoty dodavatel s adresami, města a země. Po provedení těchto změn by deklarativní syntaxe stránky s vypadala podobně jako v následujícím příkladu:

[!code-aspx[Main](performing-batch-updates-cs/samples/sample1.aspx)]

> [!NOTE]
> Podobně jako v předchozím kurzu musí mít DataList v tomto kurzu povolený stav zobrazení.

Ve `ItemTemplate` I m používá dvě nové třídy CSS, `SupplierPropertyLabel` a `SupplierPropertyValue`, které byly přidány do třídy `Styles.css` a nakonfigurovány tak, aby používaly stejné nastavení stylu jako `ProductPropertyLabel` a `ProductPropertyValue` třídy CSS.

[!code-css[Main](performing-batch-updates-cs/samples/sample2.css)]

Po provedení těchto změn navštivte tuto stránku v prohlížeči. Jak je znázorněno na obrázku 5, každá položka DataList zobrazuje název dodavatele jako text a používá textová pole k zobrazení adresy, města a země.

[![každý dodavatel v prvku DataList je upravitelný](performing-batch-updates-cs/_static/image14.png)](performing-batch-updates-cs/_static/image13.png)

**Obrázek 5**: každý dodavatel v prvku DataList je upravitelný ([kliknutím zobrazíte obrázek v plné velikosti).](performing-batch-updates-cs/_static/image15.png)

## <a name="step-2-adding-an-update-all-button"></a>Krok 2: Přidání tlačítka Aktualizovat vše

Každý dodavatel na obrázku 5 má pole adresa, město a země zobrazená v textovém poli. momentálně není k dispozici žádné tlačítko Aktualizovat. Místo toho, aby bylo tlačítko aktualizace na položku s plně upravitelnými datalisty, obvykle je na stránce k dispozici jediné tlačítko Aktualizovat vše, které po kliknutí aktualizuje *všechny* záznamy v prvku DataList. Pro účely tohoto kurzu přidejte dvě možnost aktualizovat všechna tlačítka – jednu v horní části stránky a jednu v dolní části (i když kliknete na tlačítko buď bude mít stejný účinek).

Začněte přidáním webového ovládacího prvku tlačítko nad prvkem DataList a nastavením jeho vlastnosti `ID` na `UpdateAll1`. Dále přidejte ovládací prvek pro druhé tlačítko pod prvkem DataList a nastavte jeho `ID` na `UpdateAll2`. Nastavte vlastnosti `Text` u dvou tlačítek na hodnotu Aktualizovat vše. Nakonec vytvořte obslužné rutiny událostí pro obě tlačítka `Click` události. Namísto duplikování logiky aktualizace v každé obslužné rutině události je možné, že s logikou pro třetí metodu, `UpdateAllSupplierAddresses`, mají obslužné rutiny události jednoduše vyvolání této třetí metody.

[!code-csharp[Main](performing-batch-updates-cs/samples/sample3.cs)]

Obrázek 6 znázorňuje stránku po přidání všech tlačítek aktualizovat.

[na stránku se přidala dvě tlačítka aktualizace pro všechna ![.](performing-batch-updates-cs/_static/image17.png)](performing-batch-updates-cs/_static/image16.png)

**Obrázek 6**: na stránku bylo přidáno dvě aktualizace všech tlačítek ([kliknutím zobrazíte obrázek v plné velikosti](performing-batch-updates-cs/_static/image18.png)).

## <a name="step-3-updating-all-of-the-suppliers-address-information"></a>Krok 3: aktualizace všech informací o adrese dodavatele

Se všemi položkami DataList a zobrazujícími rozhraní pro úpravy a přidáním všech tlačítek Aktualizovat vše zůstane zápis kódu pro provedení aktualizace dávky. Konkrétně musíme projít položky DataList s a volat metodu `SuppliersBLL` třídy s `UpdateSupplierAddress` pro každé z nich.

Kolekce instancí `DataListItem`, ke kterým je strukturu k prvku DataList, je k dispozici prostřednictvím vlastnosti DataList s [`Items`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.items.aspx). S odkazem na `DataListItem`můžeme přesměrovat odpovídající `SupplierID` z kolekce `DataKeys` a programově odkazovat na webové ovládací prvky TextBox v rámci `ItemTemplate`, jak ukazuje následující kód:

[!code-csharp[Main](performing-batch-updates-cs/samples/sample4.cs)]

Když uživatel klikne na jedno z tlačítek Aktualizovat vše, metoda `UpdateAllSupplierAddresses` projde každým `DataListItem` v `Suppliers` DataList a zavolá metodu `UpdateSupplierAddress` třídy `SuppliersBLL`, která předává příslušné hodnoty. Nevložená hodnota pro předávání adresa, město nebo země je hodnota `Nothing` pro `UpdateSupplierAddress` (místo prázdného řetězce), která má za následek `NULL` databáze pro podkladová pole záznamů.

> [!NOTE]
> Jako vylepšení můžete chtít přidat webový ovládací prvek popisek stavu na stránku, která poskytuje zprávu s potvrzením po provedení aktualizace dávky.

## <a name="updating-only-those-addresses-that-have-been-modified"></a>Aktualizace pouze těch adres, které byly změněny

Algoritmus dávkové aktualizace použitý pro tento kurz volá metodu `UpdateSupplierAddress` pro *každého* dodavatele v prvku DataList, a to bez ohledu na to, jestli se změnily informace o adrese. I když tyto nevidomé aktualizace většinou nedochází k problémům s výkonem, můžou vést k nadbytečným záznamům, pokud převedete změny auditování v tabulce databáze. Pokud například použijete triggery k zaznamenání všech `UPDATE` s do tabulky `Suppliers` do tabulky auditování, pokaždé, když uživatel klikne na tlačítko Aktualizovat vše, vytvoří se nový záznam auditu pro každého dodavatele v systému bez ohledu na to, jestli uživatel provedl nějaké změny.

Třídy DataTable a DataAdapter ADO.NET jsou navržené tak, aby podporovaly dávkové aktualizace, kde pouze změny, odstranění a nové záznamy mají za následek jakoukoli databázovou komunikaci. Každý řádek v objektu DataTable má [vlastnost`RowState`](https://msdn.microsoft.com/library/system.data.datarow.rowstate.aspx) , která označuje, zda byl řádek přidán do objektu DataTable, odstraněn z něj, změněn nebo zůstane beze změny. Při počátečním naplnění objektu DataTable budou všechny řádky označeny beze změny. Když změníte hodnotu některého sloupce řádek s, řádek se označí jako změněný.

Ve třídě `SuppliersBLL` aktualizujeme zadané informace o dodavatelích na základě prvního čtení záznamu jednoho dodavatele do `SuppliersDataTable` a pak nastavíte hodnoty sloupce `Address`, `City`a `Country` pomocí následujícího kódu:

[!code-csharp[Main](performing-batch-updates-cs/samples/sample5.cs)]

Tento kód naively přiřadí hodnoty předané adresy, města a země `SuppliersRow` v `SuppliersDataTable` bez ohledu na to, jestli se hodnoty změnily. Tyto úpravy způsobí, že vlastnost `SuppliersRow` s `RowState` bude označena jako upravená. Když je zavolána metoda přístup k datům `Update` vrstvě, zjistí, že `SupplierRow` byla upravena a proto pošle příkaz `UPDATE` do databáze.

Představme si ale, že jsme do této metody přidali kód pro přiřazení hodnot předaných adres, měst a zemí, pokud se liší od stávajících hodnot `SuppliersRow` s. V případě, že adresa, město a země jsou stejné jako stávající data, nebudou provedeny žádné změny a `RowState` `SupplierRow` s zůstane označena jako nezměněná. Výsledkem netto je, že při volání metody DAL s `Update` se neprovede žádné volání databáze, protože `SuppliersRow` nebyla upravena.

Chcete-li tuto změnu přijmout, nahraďte příkazy, které neumožňují geograficky přiřadit hodnoty předané adresy, města a země následujícímu kódu:

[!code-csharp[Main](performing-batch-updates-cs/samples/sample6.cs)]

S tímto přidaným kódem pošle metoda `Update` DAL do databáze příkaz `UPDATE` pro všechny záznamy, jejichž hodnoty související s adresou se změnily.

Alternativně můžeme sledovat, zda existují nějaké rozdíly mezi předanými poli adres a databázovými daty, a pokud žádný není, jednoduše obejít volání metody DAL s `Update`. Tento přístup funguje i v případě, že znovu použijete metodu Direct DB, protože metoda DB Direct t předala `SuppliersRow` instanci, jejíž `RowState` může být zaškrtnuto, aby bylo možné určit, zda je volání databáze skutečně požadováno.

> [!NOTE]
> Pokaždé, když je vyvolána metoda `UpdateSupplierAddress`, se do databáze přivede volání, aby se načetly informace o aktualizovaném záznamu. Pokud jsou v datech nějaké změny, provedou se další volání databáze, aby se aktualizoval řádek tabulky. Tento pracovní postup může být optimalizován vytvořením přetížení metody `UpdateSupplierAddress`, které přijímá instanci `EmployeesDataTable`, která obsahuje *všechny* změny ze stránky `BatchUpdate.aspx`. Potom může provést jedno volání databáze a získat všechny záznamy z `Suppliers` tabulky. Tyto dvě sady výsledků by se pak mohly zobrazit a jenom záznamy, ve kterých došlo ke změnám, se daly aktualizovat.

## <a name="summary"></a>Souhrn

V tomto kurzu jsme viděli, jak vytvořit plně upravitelný prvek DataList, který uživateli umožňuje rychle upravit informace o adrese pro více dodavatelů. Začali jsme definováním rozhraní pro úpravy webovým ovládacím prvkem TextBox pro hodnoty adresa dodavatele, města a země v `ItemTemplate`DataList. Dále jsme přidali všechna tlačítka nad a pod rámec DataList. Poté, co uživatel provedl změny a klikli na jedno z tlačítek Aktualizovat vše, jsou `DataListItem`y výčty a je provedeno volání metody `SuppliersBLL` třídy s `UpdateSupplierAddress`.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Zack Novotný a Ken Pespisa. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](an-overview-of-editing-and-deleting-data-in-the-datalist-cs.md)
> [Další](handling-bll-and-dal-level-exceptions-cs.md)

---
uid: web-forms/overview/data-access/working-with-batched-data/batch-inserting-vb
title: Dávkové vkládání (VB) | Microsoft Docs
author: rick-anderson
description: Naučte se, jak vložit více záznamů databáze v rámci jedné operace. Ve vrstvě uživatelského rozhraní rozšiřujeme prvek GridView tak, aby umožňoval uživateli zadat více n...
ms.author: riande
ms.date: 06/26/2007
ms.assetid: 48e2a4ae-77ca-4208-a204-c38c690ffb59
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-inserting-vb
msc.type: authoredcontent
ms.openlocfilehash: 413a0e209b1899414eaab70aff07ee0d3223f28f
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74643125"
---
# <a name="batch-inserting-vb"></a>Dávkové vkládání (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_66_VB.zip) nebo [stažení PDF](batch-inserting-vb/_static/datatutorial66vb1.pdf)

> Naučte se, jak vložit více záznamů databáze v rámci jedné operace. Ve vrstvě uživatelského rozhraní rozšiřujeme prvek GridView tak, aby umožňoval uživateli zadat více nových záznamů. Ve vrstvě přístupu k datům rozbalíme operace více operací vložení v rámci transakce, aby se zajistilo, že všechna vložení budou úspěšná, nebo se všechna vložení vrátí zpět.

## <a name="introduction"></a>Úvod

V kurzu [dávkové aktualizace](batch-updating-vb.md) jsme se podívali na přizpůsobení ovládacího prvku GridView, který prezentuje rozhraní, kde se dá upravovat víc záznamů. Uživatel, který navštívil stránku, může provést řadu změn a pak jediným kliknutím na tlačítko provést dávkovou aktualizaci. V situacích, kdy uživatelé běžně aktualizují mnoho záznamů v jednom z nich, může toto rozhraní ukládat dlouhé kliknutí a přepínání mezi jednotlivými jednotlivými řádky, když jsou v porovnání s výchozími funkcemi pro úpravu řádků, které se poprvé prozkoumaly v kurzu [Přehled vložení, aktualizace a odstranění dat](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) .

Tento koncept se dá použít i při přidávání záznamů. Představte si, že v článku Northwind Traders jsme běžně dostávali dodávky od dodavatelů, kteří pro konkrétní kategorii obsahují řadu produktů. Příkladem může být doručení šesti různých produktů čaje a kávy od hospodářských obchodníků z Brna. Pokud uživatel zadá šest produktů po jednom prostřednictvím ovládacího prvku DetailsView, bude muset zvolit mnoho stejných hodnot znovu a znovu: bude muset zvolit stejnou kategorii (nápoje), stejného dodavatele (Brno obchodníci), stejnou Nepokračující hodnotu ( False) a stejné jednotky v hodnotě pořadí (0). Tato opakující se položka dat je časově náročná, ale je náchylná k chybám.

S malým množstvím práce můžeme vytvořit dávkové vkládání rozhraní, které umožňuje uživateli zvolit dodavatel a kategorii jednou, zadat řady názvů produktů a jednotkové ceny a potom kliknutím na tlačítko Přidat nové produkty do databáze (viz obrázek 1). Při přidání každého produktu se jeho `ProductName` a datová pole `UnitPrice` přiřazují hodnoty zadané v textových polích, zatímco `CategoryID` a `SupplierID` hodnoty jsou přiřazeny hodnoty z ovládacích prvků DropDownList v horní části formuláře. Hodnoty `Discontinued` a `UnitsOnOrder` jsou nastaveny na pevně zakódované hodnoty `False` a 0 v uvedeném pořadí.

[![rozhraní Batch pro vložení](batch-inserting-vb/_static/image2.png)](batch-inserting-vb/_static/image1.png)

**Obrázek 1**: dávkové vkládání rozhraní ([kliknutím zobrazíte obrázek v plné velikosti](batch-inserting-vb/_static/image3.png))

V tomto kurzu vytvoříme stránku, která implementuje rozhraní Batch pro vložení zobrazené na obrázku 1. Stejně jako v předchozích dvou kurzech zabalíme vložení do rozsahu transakce, aby se zajistila nedělitelnost. Pojďme začít!

## <a name="step-1-creating-the-display-interface"></a>Krok 1: vytvoření rozhraní pro zobrazení

Tento kurz se skládá z jedné stránky, která je rozdělená do dvou oblastí: oblast zobrazení a oblast vložení. Rozhraní zobrazení, které v tomto kroku vytvoříte, zobrazuje produkty v prvku GridView a obsahuje tlačítko s názvem dodávka produktu. Po kliknutí na toto tlačítko je rozhraní zobrazení nahrazeno rozhraním pro vložení, které je zobrazeno na obrázku 1. Rozhraní zobrazení se vrátí po kliknutí na tlačítka Přidat produkty z odeslání nebo zrušit. Rozhraní pro vložení vytvoříme v kroku 2.

Při vytváření stránky, která má dvě rozhraní, pouze jedna, která je viditelná současně, každé rozhraní je obvykle umístěno v rámci [webového ovládacího prvku panelu](http://www.w3schools.com/aspnet/control_panel.asp), který slouží jako kontejner pro jiné ovládací prvky. Proto má naše stránka dva ovládací prvky panelu pro každé rozhraní.

Začněte otevřením stránky `BatchInsert.aspx` ve složce `BatchData` a přetažením panelu z panelu nástrojů do návrháře (viz obrázek 2). Nastavte vlastnost panel s `ID` na `DisplayInterface`. Když přidáte panel do návrháře, jeho `Height` a vlastnosti `Width` jsou nastaveny na 50px a 125px, v uvedeném pořadí. Vymažte z okno Vlastnosti tyto hodnoty vlastností.

[![přetáhněte panel z panelu nástrojů na Návrhář.](batch-inserting-vb/_static/image5.png)](batch-inserting-vb/_static/image4.png)

**Obrázek 2**: přetáhněte panel z panelu nástrojů do návrháře ([kliknutím zobrazíte obrázek v plné velikosti](batch-inserting-vb/_static/image6.png)).

Potom přetáhněte tlačítko a ovládací prvek GridView do panelu. Nastavte vlastnost `ID` tlačítko na `ProcessShipment` a jeho vlastnost `Text` na zpracovávání dodávky produktu. Nastavte vlastnost `ID` ovládacího prvku GridView na `ProductsGrid` a ze své inteligentní značky ji navažte na nový prvek ObjectDataSource s názvem `ProductsDataSource`. Nakonfigurujte prvek ObjectDataSource tak, aby vyčetl data z `ProductsBLL` třídy s `GetProducts` metody. Vzhledem k tomu, že se tento prvek GridView používá jenom k zobrazení dat, nastavte rozevírací seznamy na kartách aktualizace, vložení a odstranění na (žádné). Kliknutím na Dokončit dokončete Průvodce konfigurací zdroje dat.

[![zobrazení dat vrácených z metody ProductsBLL třídy s GetProducts](batch-inserting-vb/_static/image8.png)](batch-inserting-vb/_static/image7.png)

**Obrázek 3**: zobrazení dat vrácených z `GetProducts` metody `ProductsBLL` třídy s ([kliknutím zobrazíte obrázek v plné velikosti](batch-inserting-vb/_static/image9.png))

[![nastavení rozevíracích seznamů na kartách aktualizace, vložení a odstranění na (žádné)](batch-inserting-vb/_static/image11.png)](batch-inserting-vb/_static/image10.png)

**Obrázek 4**: nastavení rozevíracích seznamů na kartách aktualizace, vložení a odstranění na (žádné) ([kliknutím zobrazíte obrázek v plné velikosti).](batch-inserting-vb/_static/image12.png)

Po dokončení průvodce ObjectDataSource bude Visual Studio přidávat BoundFields a třídě CheckBoxField podporována pro pole dat produktu. Odeberte všechna pole s výjimkou `ProductName`, `CategoryName`, `SupplierName`, `UnitPrice`a `Discontinued`. Nebojte se dělat všechna estetická přizpůsobení. Rozhodli jste se formátovat pole `UnitPrice` jako hodnotu měny, změnit pořadí polí a přejmenovat několik polí `HeaderText` hodnot. Také nakonfigurujete prvek GridView tak, aby zahrnoval podporu stránkování a řazení, zaškrtnutím políčka Povolit stránkování a Povolit řazení v inteligentní značce GridView s.

Po přidání ovládacího prvku panel, tlačítko, GridView a ObjectDataSource a přizpůsobení polí prvku GridView, by vaše deklarativní označení stránky mělo vypadat podobně jako následující:

[!code-aspx[Main](batch-inserting-vb/samples/sample1.aspx)]

Všimněte si, že značky pro tlačítko a GridView se zobrazí v rámci značek pro otevírání a zavírání `<asp:Panel>`. Vzhledem k tomu, že se tyto ovládací prvky nacházejí v `DisplayInterface`m panelu, můžeme je skrýt jednoduše nastavením vlastnosti panel s `Visible` na `False`. Krok 3: při překrytí vlastnosti panel s `Visible` v reakci na tlačítko můžete zobrazit jedno rozhraní a zároveň ho skrýt.

Chvilku si můžete prohlédnout v prohlížeči. Jak ukazuje obrázek 5, měli byste vidět tlačítko zpracovat produktovou dodávku nad prvek GridView, ve kterém jsou uvedené produkty deset v čase.

[![ovládacího prvku GridView zobrazí seznam produktů a nabízí možnosti řazení a stránkování.](batch-inserting-vb/_static/image14.png)](batch-inserting-vb/_static/image13.png)

**Obrázek 5**: prvek GridView obsahuje seznam produktů a nabízí možnosti řazení a stránkování ([kliknutím zobrazíte obrázek v plné velikosti](batch-inserting-vb/_static/image15.png)).

## <a name="step-2-creating-the-inserting-interface"></a>Krok 2: vytvoření rozhraní pro vložení

Po dokončení rozhraní zobrazení jsme připraveni vytvořit rozhraní pro vložení. V tomto kurzu vytvoříme rozhraní pro vložení, které vyzve k zadání jedné hodnoty dodavatele a kategorie a potom umožní uživateli zadat až pět názvů produktů a hodnot jednotkových cen. Pomocí tohoto rozhraní může uživatel přidat jeden až pět nových produktů, které sdílejí stejnou kategorii a dodavatele, ale mají jedinečné názvy produktů a ceny.

Začněte přetažením panelu z panelu nástrojů do návrháře a jeho umístěním pod existující `DisplayInterface` panel. Nastavte vlastnost `ID` tohoto nově přidaného panelu na `InsertingInterface` a nastavte jeho vlastnost `Visible` na `False`. Přidáme kód, který nastaví vlastnost `InsertingInterface` panel s `Visible` na `True` v kroku 3. Také vymažte `Height` panelů a `Width` hodnoty vlastností.

Dál je potřeba vytvořit rozhraní pro vložení, které bylo na obrázku 1 zobrazeno zpátky. Toto rozhraní je možné vytvořit pomocí nejrůznějších technik jazyka HTML, ale budeme používat poměrně jednoduchý řádek: tabulka se čtyřmi řádky se čtyřmi sloupci.

> [!NOTE]
> Při zadávání značek pro prvky HTML `<table>` raději použít zobrazení zdroje. I když má aplikace Visual Studio nástroje pro přidání `<table>` prvků prostřednictvím návrháře, zdá se, že se Návrhář jeví jako příliš ochotno vložit nepožádat o `style` nastavení do značky. Po vytvoření značky `<table>` se obvykle vrátíte do návrháře a přidáte webové ovládací prvky a nastavíte jejich vlastnosti. Při vytváření tabulek s předem určenými sloupci a řádky, které dáváte přednost použití statického HTML místo [webového ovládacího prvku tabulka](https://msdn.microsoft.com/library/system.web.ui.webcontrols.table.aspx) , protože jakékoli webové ovládací prvky umístěné v rámci webového ovládacího prvku tabulka lze použít pouze pomocí `FindControl("controlID")`ho vzoru. K tomu ale použijte webové ovládací prvky tabulky pro dynamicky se velikost tabulek (ty, jejichž řádky nebo sloupce jsou založené na některých kritériích pro databázi nebo uživatele), protože ovládací prvek web Table lze sestavit programově.

Do `<asp:Panel>` značek `InsertingInterface` panelu zadejte následující kód:

[!code-html[Main](batch-inserting-vb/samples/sample2.html)]

Toto `<table>` označení zatím neobsahuje žádné webové ovládací prvky, přidáme je za chvíli. Všimněte si, že každý prvek `<tr>` obsahuje konkrétní nastavení třídy CSS: `BatchInsertHeaderRow` pro řádek záhlaví, kde se dostanou DropDownList dodavatele a kategorie. `BatchInsertFooterRow` pro řádek zápatí, ve kterém budou tlačítka Přidat produkty z expedice a Storno přecházet. a střídavě `BatchInsertRow` a `BatchInsertAlternatingRow` hodnoty pro řádky, které budou obsahovat ovládací prvky TextBox pro produkt a jednotkové ceny. V souboru `Styles.css` jsem vytvořil odpovídající třídy šablony stylů CSS, aby rozhraní pro vložení mělo vzhled podobné ovládacím prvkům GridView a DetailsView, které jsme použili v těchto kurzech. Níže jsou uvedeny tyto třídy CSS.

[!code-css[Main](batch-inserting-vb/samples/sample3.css)]

Po zadání tohoto kódu se vraťte do zobrazení Návrh. Tato `<table>` by se měla v Návrháři zobrazovat jako tabulka se čtyřmi sloupci a sedmi řádky, jak ukazuje obrázek 6.

[![rozhraní pro vložení se skládá ze čtyř sloupců tabulky se sedmi řádky](batch-inserting-vb/_static/image17.png)](batch-inserting-vb/_static/image16.png)

**Obrázek 6**: rozhraní pro vložení se skládá ze čtyř sloupců tabulky se sedmi řádky ([kliknutím zobrazíte obrázek v plné velikosti).](batch-inserting-vb/_static/image18.png)

Nově jsme teď připraveni přidat webové ovládací prvky do rozhraní pro vložení. Přetáhněte ze sady nástrojů dvě DropDownListy do příslušných buněk v tabulce jedna pro dodavatele a jednu pro kategorii.

Nastavte vlastnost `ID` DropDownList pro dodavatele na `Suppliers` a navažte ji na nový prvek ObjectDataSource s názvem `SuppliersDataSource`. Nakonfigurujte nový prvek ObjectDataSource tak, aby načetl jeho data z `SuppliersBLL` třídy s `GetSuppliers` a nastavte rozevírací seznam s kartami aktualizace na hodnotu (žádné). Kliknutím na Dokončit dokončete průvodce.

[![nakonfigurovat prvek ObjectDataSource tak, aby používal metodu SuppliersBLL třídy s getdodavatelé](batch-inserting-vb/_static/image20.png)](batch-inserting-vb/_static/image19.png)

**Obrázek 7**: Konfigurace prvku ObjectDataSource pro použití `GetSuppliers` metody `SuppliersBLL` třídy s ([kliknutím zobrazíte obrázek v plné velikosti](batch-inserting-vb/_static/image21.png))

Musí `Suppliers` DropDownList zobrazit `CompanyName` datová pole a jako hodnoty `ListItem` s používat pole `SupplierID` data.

[![zobrazení datového pole CompanyName a jako hodnotu použít ČísloDodavatele.](batch-inserting-vb/_static/image23.png)](batch-inserting-vb/_static/image22.png)

**Obrázek 8**: zobrazení datového pole `CompanyName` a použití `SupplierID` jako hodnoty ([kliknutím zobrazíte obrázek v plné velikosti](batch-inserting-vb/_static/image24.png))

Pojmenujte druhý `Categories` DropDownList a navažte jej na nový prvek ObjectDataSource s názvem `CategoriesDataSource`. Nakonfigurujte `CategoriesDataSource` ObjectDataSource tak, aby používala metodu `CategoriesBLL` třídy s `GetCategories`; nastavte rozevírací seznamy na kartách aktualizovat a odstranit na (žádné) a kliknutím na Dokončit dokončete průvodce. Nakonec má DropDownList zobrazit `CategoryName` data pole a jako hodnotu použít `CategoryID`.

Po přidání těchto dvou ovládacích prvků DropDownList a jejich svázání s vhodně nakonfigurovanými ObjectDataSources by měla obrazovka vypadat podobně jako obrázek 9.

[![řádek hlavičky teď obsahuje DropDownList a kategorie DropDownList.](batch-inserting-vb/_static/image26.png)](batch-inserting-vb/_static/image25.png)

**Obrázek 9**: řádek záhlaví obsahuje nyní `Suppliers` a `Categories` DropDownList ([kliknutím zobrazíte obrázek v plné velikosti).](batch-inserting-vb/_static/image27.png)

Teď je potřeba vytvořit textová pole, abyste mohli shromažďovat název a cenu každého nového produktu. Přetáhněte ovládací prvek TextBox ze sady nástrojů do návrháře pro každý z pěti názvů produktů a cenových řádků. Nastavte vlastnosti `ID` textových polí na `ProductName1`, `UnitPrice1`, `ProductName2`, `UnitPrice2`, `ProductName3`, `UnitPrice3`atd.

Přidejte CompareValidator za každé textové pole s jednotkovými cenami a nastavte vlastnost `ControlToValidate` na odpovídající `ID`. Nastavte také vlastnost `Operator` na `GreaterThanEqual`, `ValueToCompare` na 0 a `Type` na `Currency`. Tato nastavení instruují CompareValidator, aby zajistila, že cena, je-li zadána, je platná hodnota měny, která je větší nebo rovna nule. Nastavte vlastnost `Text` na \*a `ErrorMessage` na cenu musí být větší nebo rovna nule. Vynechejte také žádné symboly měny.

> [!NOTE]
> Rozhraní pro vložení neobsahuje žádné ovládací prvky RequiredFieldValidator, i když pole `ProductName` v databázové tabulce `Products` nepovoluje hodnoty `NULL`. Důvodem je to, že chceme, aby uživatel mohl zadat až pět produktů. Pokud by například uživatel pro první tři řádky poskytoval název produktu a jednotkovou cenu, ponechají si poslední dva řádky, ale do systému přidá tři nové produkty. Vzhledem k tomu, že je potřeba `ProductName`, budeme muset programově zkontrolovat, jestli je k dispozici odpovídající hodnota názvu produktu, aby bylo zajištěno, že bude zadána Jednotková cena. Tuto kontrolu provedeme v kroku 4.

Při ověřování vstupu uživatele, CompareValidator hlásí neplatná data, pokud hodnota obsahuje symbol měny. Přidejte $ před každé textové pole s jednotkovými cenami, které slouží jako vizuální upozornění, které uživateli dává pokyn, aby při zadávání ceny vynechal symbol měny.

Nakonec přidejte ovládací prvek ovládací souhrnu ověření do panelu `InsertingInterface`, nastavení jeho vlastnosti `ShowMessageBox` na `True` a jeho vlastnost `ShowSummary` na `False`. Pokud uživatel zadá neplatnou hodnotu jednotkové ceny, zobrazí se u těchto nastavení hvězdička vedle problematických ovládacích prvků TextBox a ovládací souhrnu ověření zobrazí objekt MessageBox na straně klienta, který zobrazuje chybovou zprávu, kterou jsme zadali dříve.

V tomto okamžiku by měla obrazovka vypadat podobně jako obrázek 10.

[![rozhraní pro vložení teď obsahuje textová pole pro názvy produktů a jejich ceny.](batch-inserting-vb/_static/image29.png)](batch-inserting-vb/_static/image28.png)

**Obrázek 10**: rozhraní pro vložení obsahuje textové pole pro názvy produktů a jejich ceny ([kliknutím zobrazíte obrázek v plné velikosti).](batch-inserting-vb/_static/image30.png)

Dál je potřeba přidat do řádku zápatí tlačítko Přidat produkty z expedice a zrušit. Přetáhněte ze sady nástrojů dva ovládací prvky tlačítka do zápatí rozhraní pro vložení, nastavením tlačítek `ID` vlastností `AddProducts` a `CancelButton` a `Text` vlastností přidejte produkty z expedice a zrušit v uvedeném pořadí. Kromě toho nastavte vlastnost `CancelButton` ovládací prvek s `CausesValidation` na `false`.

Nakonec musíme přidat webový ovládací prvek popisku, který zobrazí stavové zprávy pro dvě rozhraní. Například když uživatel úspěšně přidá novou zásilku produktů, chceme se vrátit na zobrazovací rozhraní a zobrazit potvrzovací zprávu. Pokud ale uživatel zadá cenu za nový produkt, ale ponechá název produktu, musíme zobrazit upozornění, protože pole `ProductName` je povinné. Vzhledem k tomu, že potřebujeme, aby se tato zpráva zobrazovala pro obě rozhraní, umístěte ji v horní části stránky mimo panely.

Přetáhněte ovládací prvek web Label ze sady nástrojů na začátek stránky v návrháři. Nastavte vlastnost `ID` na `StatusLabel`, vymažte vlastnost `Text` a nastavte vlastnosti `Visible` a `EnableViewState` na `False`. Jak jsme viděli v předchozích kurzech, nastavením vlastnosti `EnableViewState` na `False` umožníme programově změnit hodnoty vlastnosti Label a tak, aby se automaticky vrátily zpět na výchozí hodnoty při následném odeslání. Tím se zjednoduší kód pro zobrazení stavové zprávy v reakci na určitou akci uživatele, která zmizí při následném zpětném odeslání. Nakonec nastavte vlastnost `StatusLabel` Control s `CssClass` na Warning, což je název třídy CSS definované v `Styles.css`, která zobrazuje text ve velkém, kurzívě, tučně červené písmo.

Obrázek 11 znázorňuje Návrháře sady Visual Studio po přidání a konfiguraci popisku.

[![umístit ovládací prvek StatusLabel nad dva ovládací prvky panelu](batch-inserting-vb/_static/image32.png)](batch-inserting-vb/_static/image31.png)

**Obrázek 11**: ovládací prvek `StatusLabel` nad dvěma ovládacími prvky panelu ([kliknutím zobrazíte obrázek v plné velikosti](batch-inserting-vb/_static/image33.png)).

## <a name="step-3-switching-between-the-display-and-inserting-interfaces"></a>Krok 3: přepínání mezi rozhraními Display a vložení

V tuto chvíli jsme dokončili značky pro naše rozhraní zobrazení a vkládání, ale pořád zbývá dvě úlohy:

- Přepínání mezi rozhraními Display a vložení
- Přidání produktů v dodávce do databáze

V současné době je rozhraní zobrazení viditelné, ale rozhraní pro vložení je skryté. Důvodem je, že vlastnost `DisplayInterface` panel s `Visible` je nastavena na hodnotu `True` (výchozí hodnota), zatímco vlastnost `InsertingInterface` panel s `Visible` je nastavena na hodnotu `False`. Pro přepínání mezi oběma rozhraními stačí jednoduše přepnout jednotlivé ovládací prvky s `Visible` hodnotou vlastnosti.

Po kliknutí na tlačítko pro expedici procesu produktu se chceme přesunout z rozhraní pro zobrazení na rozhraní pro vložení. Proto vytvořte obslužnou rutinu události pro toto tlačítko s `Click` událost, která obsahuje následující kód:

[!code-vb[Main](batch-inserting-vb/samples/sample4.vb)]

Tento kód jednoduše skryje panel `DisplayInterface` a zobrazí `InsertingInterface` panel.

Dále vytvořte obslužné rutiny události pro ovládací prvky přidat produkty z expedice a zrušit v rozhraní pro vložení. Po kliknutí na některé z těchto tlačítek se musíme vrátit zpátky na zobrazovací rozhraní. Vytvořte obslužné rutiny událostí `Click` pro obě ovládací prvky tlačítko tak, aby volaly `ReturnToDisplayInterface`, metoda, kterou přidáme za chvíli. Kromě skrytí `InsertingInterface`ho panelu a zobrazení `DisplayInterface`ho panelu musí metoda `ReturnToDisplayInterface` vracet webové ovládací prvky do stavu před úpravou. To zahrnuje nastavení vlastností DropDownList `SelectedIndex` na hodnotu 0 a vymazávání vlastností `Text` ovládacích prvků TextBox.

> [!NOTE]
> Zvažte, co se může stát, když jsme ovládací prvky před návratem do rozhraní zobrazení nevrátili do stavu před úpravou. Uživatel může kliknout na tlačítko Zpracovat dodávku produktu, zadat produkty z dodávky a pak kliknout na Přidat produkty z dodávky. To by mohlo přidat produkty a vrátit uživatele do rozhraní zobrazení. V tomto okamžiku může uživatel chtít přidat další dodávku. Po kliknutí na tlačítko Zpracovat dodávku produktu by se vrátila do rozhraní pro vložení, ale výběry DropDownList a hodnoty TextBox by se měly pořád naplnit jejich předchozími hodnotami.

[!code-vb[Main](batch-inserting-vb/samples/sample5.vb)]

Oba obslužné rutiny událostí `Click` jednoduše volají metodu `ReturnToDisplayInterface`, ale v kroku 4 se vrátíme k obslužné rutině události přidat produkty z dodávky `Click` a přidáte kód pro uložení produktů. `ReturnToDisplayInterface` spustí vrácením `Suppliers` a `Categories` DropDownList na první možnosti. Tyto dvě konstanty `firstControlID` a `lastControlID` označují počáteční a koncové hodnoty indexu ovládacího prvku používané při pojmenování názvu produktu a textových polí s cenami v rozhraní vkládání a používají se v hranicích `For` smyčky, která nastavuje `Text` vlastnosti ovládacího prvku TextBox zpět na prázdný řetězec. Nakonec se panely `Visible` vlastnosti resetují, aby bylo vkládání rozhraní skryté a zobrazené rozhraní zobrazení.

Chvíli počkejte, než otestujete tuto stránku v prohlížeči. Při první návštěvě stránky by se mělo zobrazit rozhraní pro zobrazení zobrazené na obrázku 5. Klikněte na tlačítko Zpracovat dodávku produktu. Stránka se odešle zpět a mělo by se teď zobrazit rozhraní pro vložení, jak je znázorněno na obrázku 12. Kliknutím na tlačítko Přidat produkty z expedice nebo zrušit se vrátíte k rozhraní zobrazení.

> [!NOTE]
> Při prohlížení rozhraní pro vkládání si chvíli počkejte, než CompareValidators otestujete v textových polích s cenami za jednotku. Když kliknete na tlačítko Přidat produkty z dodávky s neplatnými hodnotami měny nebo ceny s hodnotou menší než nula, mělo by se zobrazit upozornění na straně klienta.

[Po kliknutí na tlačítko Zpracovat dodávku produktu se zobrazí ![rozhraní pro vložení.](batch-inserting-vb/_static/image35.png)](batch-inserting-vb/_static/image34.png)

**Obrázek 12**: rozhraní pro vložení se zobrazí po kliknutí na tlačítko Zpracovat dodávku produktu ([kliknutím zobrazíte obrázek v plné velikosti](batch-inserting-vb/_static/image36.png)).

## <a name="step-4-adding-the-products"></a>Krok 4: Přidání produktů

Vše, co pro tento kurz zbývá, je uložit produkty do databáze v okně Přidat produkty z tlačítka pro expedici s `Click` obslužné rutiny události. To lze provést vytvořením `ProductsDataTable` a přidáním instance `ProductsRow` pro každý zadaný název produktu. Po přidání těchto `ProductsRow` se provede volání metody `ProductsBLL` třídy s `UpdateWithTransaction` předání do `ProductsDataTable`. Odvolat, že metoda `UpdateWithTransaction`, která byla vytvořena zpátky v [rámci kurzu transakce](wrapping-database-modifications-within-a-transaction-vb.md) , předává `ProductsDataTable` do metody `UpdateWithTransaction` `ProductsTableAdapter`. Odtud se spustí transakce ADO.NET a TableAdapter vydá příkaz `INSERT` do databáze pro každý přidaný `ProductsRow` v objektu DataTable. Za předpokladu, že jsou všechny produkty přidány bez chyby, transakce je potvrzena, jinak se vrátí zpět.

Kód pro obslužnou rutinu tlačítka pro přidání produktů z `Click` pro příjem také musí provést kontrolu chyb. Vzhledem k tomu, že v rozhraní pro vkládání nejsou použité žádné RequiredFieldValidators, může uživatel zadat cenu za produkt a zároveň ho vynechat. Vzhledem k tomu, že je název produktu povinný, pokud taková podmínka odloží, musíme uživateli upozornit a nepokračovat v vkládání. Úplný kód obslužné rutiny události `Click` následuje:

[!code-vb[Main](batch-inserting-vb/samples/sample6.vb)]

Obslužná rutina události začíná tím, že zajistí, že vlastnost `Page.IsValid` vrátí hodnotu `True`. Pokud vrátí `False`, znamená to, že jeden nebo více CompareValidators vydává neplatné údaje. v takovém případě se nechcete pokusit vložit zadané produkty. při pokusu o přiřazení hodnoty jednotkové ceny zadané uživatelem do vlastnosti `ProductsRow` s `UnitPrice` se ale ukončí výjimka.

V dalším kroku se vytvoří nová instance `ProductsDataTable` (`products`). Smyčka `For` slouží k iterování v názvu produktu a textových polích s cenami za jednotku a vlastnosti `Text` jsou čteny do místních proměnných `productName` a `unitPrice`. Pokud uživatel zadal hodnotu pro jednotkovou cenu, ale ne pro odpovídající název produktu, `StatusLabel` zobrazí zprávu, pokud zadáte jednotkovou cenu, musíte také uvést název produktu a obslužné rutiny události se ukončí.

Pokud byl zadán název produktu, vytvoří se nová instance `ProductsRow` pomocí metody `ProductsDataTable` s `NewProductsRow`. Tato nová vlastnost `ProductsRow` instance `ProductName` je nastavena na textové pole s aktuálním názvem produktu, zatímco vlastnosti `SupplierID` a `CategoryID` jsou přiřazeny k `SelectedValue` vlastnostem ovládacích prvků DropDownList v hlavičce vložení rozhraní s. Pokud uživatel zadal hodnotu ceny produktu, je přiřazen k vlastnosti `ProductsRow` instance s `UnitPrice`; v opačném případě zůstane vlastnost ponecháno Nepřiřazeno. výsledkem bude `NULL` hodnota `UnitPrice` v databázi. Nakonec jsou vlastnosti `Discontinued` a `UnitsOnOrder` přiřazeny pevně zakódované hodnoty `False` a 0 v uvedeném pořadí.

Až se vlastnosti přiřadí do instance `ProductsRow`, přidají se do `ProductsDataTable`.

Po dokončení smyčky `For` zkontrolujeme, jestli se nějaké produkty přidaly. Uživatel může po všech případech kliknout na položku Přidat produkty z dodávky a teprve potom zadat názvy produktů nebo ceny. Pokud je v `ProductsDataTable`alespoň jeden produkt, je volána metoda `ProductsBLL` třídy `UpdateWithTransaction`. Dále jsou data znovu svázána s `ProductsGrid` GridView, takže nově přidané produkty se zobrazí v rozhraní zobrazení. `StatusLabel` se aktualizuje, aby se zobrazila potvrzovací zpráva a vyvolalo se `ReturnToDisplayInterface`, aby se přestalo rozhraní pro vkládání a zobrazení rozhraní.

Pokud nebyly zadány žádné produkty, rozhraní pro vložení zůstane zobrazeno, ale zpráva nebyla přidána žádná zboží. Zadejte prosím názvy produktů a jednotkové ceny v textových polích, které se zobrazí.

Obrázek s 13, 14 a 15 zobrazuje rozhraní pro vkládání a zobrazování v akci. Na obrázku 13 zadal uživatel hodnotu jednotkové ceny bez odpovídajícího názvu produktu. Obrázek 14 ukazuje rozhraní zobrazení po úspěšném přidání tří nových produktů, zatímco obrázek 15 ukazuje dva z nově přidaných produktů v prvku GridView (třetí z nich je na předchozí stránce).

[Při zadání jednotkové ceny se ![vyžaduje název produktu.](batch-inserting-vb/_static/image38.png)](batch-inserting-vb/_static/image37.png)

**Obrázek 13**: při zadávání ceny za jednotku se vyžaduje název produktu ([kliknutím zobrazíte obrázek v plné velikosti](batch-inserting-vb/_static/image39.png)).

[pro dodavatele Mayumi se přidal tento ![tři nové veggies.](batch-inserting-vb/_static/image41.png)](batch-inserting-vb/_static/image40.png)

**Obrázek 14**: Přidali jsme tři nové veggies pro dodavatele Mayumi s ([kliknutím zobrazíte obrázek v plné velikosti).](batch-inserting-vb/_static/image42.png)

[![nové produkty najdete na poslední stránce prvku GridView.](batch-inserting-vb/_static/image44.png)](batch-inserting-vb/_static/image43.png)

**Obrázek 15**: nové produkty lze najít na poslední stránce prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](batch-inserting-vb/_static/image45.png)).

> [!NOTE]
> Dávková vložení logiky použité v tomto kurzu zabalí vložení do oboru transakce. Pokud to chcete ověřit, záměrně zavádí chybu na úrovni databáze. Například namísto přiřazení nové vlastnosti `ProductsRow` instance s `CategoryID` k vybrané hodnotě v `Categories` DropDownList, přiřaďte ji k hodnotě, jako je `i * 5`. Tady `i` je indexer smyčky a má hodnoty od 1 do 5. Proto při přidávání dvou nebo více produktů do dávky vloží první produkt platnou hodnotu `CategoryID` (5), ale další produkty budou mít `CategoryID` hodnoty, které neodpovídají hodnotám `CategoryID` v tabulce `Categories`. Čistým účinkem je to, že zatímco první `INSERT` bude úspěšná, dojde při selhání k porušení omezení cizího klíče. Vzhledem k tomu, že dávková operace INSERT je atomická, první `INSERT` se vrátí zpět a vrátí databázi do stavu před zahájením procesu dávkového vkládání.

## <a name="summary"></a>Přehled

V tomto a předchozích dvou kurzech jsme vytvořili rozhraní, která umožňují aktualizovat, odstraňovat a vkládat dávky dat, a to vše, co používalo podporu transakcí, kterou jsme přidali do vrstvy přístupu k datům v [rámci](wrapping-database-modifications-within-a-transaction-vb.md) kurzových úprav v transakci. V některých scénářích Tato uživatelská rozhraní dávkového zpracování významně zlepšují efektivitu koncových uživatelů tím, že rozchází na počet kliknutí, postbacků a přepínačů kontextu klávesnice na myš a zároveň zachovává integritu podkladových dat.

V tomto kurzu se dokončí náš pohled na práci s daty v dávce. V další sadě kurzů se seznámíte s řadou pokročilých scénářů vrstev přístupu k datům, včetně použití uložených procedur v metodách TableAdapter s, konfigurace nastavení na úrovni připojení a příkazů v DAL, šifrování připojovacích řetězců a dalších akcí.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Hilton Giesenow a S Ren Jacob Lauritsen. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](batch-deleting-vb.md)

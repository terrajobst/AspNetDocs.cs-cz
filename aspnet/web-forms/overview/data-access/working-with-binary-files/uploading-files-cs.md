---
uid: web-forms/overview/data-access/working-with-binary-files/uploading-files-cs
title: Nahrávají seC#soubory () | Microsoft Docs
author: rick-anderson
description: Naučte se, jak uživatelům dovolit ukládat binární soubory (například dokumenty Word nebo PDF) na web, kde se můžou ukládat do systému souborů serveru...
ms.author: riande
ms.date: 03/27/2007
ms.assetid: b381b1da-feb3-4776-bc1b-75db53eb90ab
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/uploading-files-cs
msc.type: authoredcontent
ms.openlocfilehash: 4e3e32a829de386a681504c8d5d61dd258b8b2e6
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74581878"
---
# <a name="uploading-files-c"></a>Nahrávání souborů (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_54_CS.exe) nebo [Stáhnout PDF](uploading-files-cs/_static/datatutorial54cs1.pdf)

> Naučte se, jak uživatelům dovolit ukládat binární soubory (například dokumenty Word nebo PDF) na web, kde se můžou ukládat buď do systému souborů serveru, nebo do databáze.

## <a name="introduction"></a>Úvod

Všechny kurzy, které jsme doposud zkoumali, pracovaly výhradně s textovými daty. Mnoho aplikací však má datové modely, které zachycují textová i binární data. Online Web dating může uživatelům dovolit nahrát obrázek, který se má přidružit k profilu. Náborový web může umožnit uživatelům odeslat svůj životopis jako dokument Microsoft Word nebo PDF.

Práce s binárními daty přidává novou sadu výzev. Je nutné rozhodnout, jak jsou binární data uložena v aplikaci. Rozhraní, které se používá pro vkládání nových záznamů, je třeba aktualizovat, aby mohl uživatel odeslat soubor ze svého počítače. je nutné provést další kroky pro zobrazení nebo poskytnutí prostředků pro stažení přidružených binárních dat záznamu. V tomto kurzu a dalších třech prozkoumáme, jak tyto výzvy nakládat. Na konci těchto kurzů sestavíme plně funkční aplikaci, která přidruží obrázek a brožuru PDF k jednotlivým kategoriím. V tomto konkrétním kurzu se podíváme na různé techniky ukládání binárních dat a prozkoumejte, jak uživatelům umožnit nahrání souboru ze svého počítače a jeho uložení v systému souborů webového serveru s.

> [!NOTE]
> Binární data, která jsou součástí datového modelu aplikace s, jsou někdy označována jako [objekt BLOB](http://en.wikipedia.org/wiki/Binary_large_object), což je zkratka pro binární rozsáhlý objekt. V těchto kurzech jsem zvolil použití binárních dat terminologie, i když pojem BLOB je synonymum.

## <a name="step-1-creating-the-working-with-binary-data-web-pages"></a>Krok 1: Vytvoření webové stránky práce s binárními daty

Předtím, než začneme prozkoumat výzvy spojené s přidáním podpory pro binární data, si nejdřív věnujte chvilku vytvoření stránek ASP.NET v našem projektu webu, který budeme potřebovat pro tento kurz a další tři. Začněte přidáním nové složky s názvem `BinaryData`. Dále přidejte následující stránky ASP.NET do této složky a nezapomeňte přidružit jednotlivé stránky k `Site.master` hlavní stránce:

- `Default.aspx`
- `FileUpload.aspx`
- `DisplayOrDownloadData.aspx`
- `UploadInDetailsView.aspx`
- `UpdatingAndDeleting.aspx`

![Přidání stránek ASP.NET pro binární kurzy související s daty](uploading-files-cs/_static/image1.gif)

**Obrázek 1**: přidejte stránky ASP.NET pro binární kurzy související s daty.

Podobně jako v ostatních složkách `Default.aspx` ve složce `BinaryData` vypíše kurzy v části. Zajistěte, aby tato funkce poskytovala `SectionLevelTutorialListing.ascx` uživatelský ovládací prvek. Proto tento uživatelský ovládací prvek přidejte do `Default.aspx` tím, že ho přetáhnete z Průzkumník řešení na zobrazení Návrh stránky.

[![přidat uživatelský ovládací prvek SectionLevelTutorialListing. ascx do default. aspx](uploading-files-cs/_static/image2.gif)](uploading-files-cs/_static/image1.png)

**Obrázek 2**: Přidání uživatelského ovládacího prvku `SectionLevelTutorialListing.ascx` do `Default.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](uploading-files-cs/_static/image2.png))

Nakonec tyto stránky přidejte jako položky do souboru `Web.sitemap`. Konkrétně přidejte následující značky po rozšíření ovládacího prvku GridView `<siteMapNode>`:

[!code-xml[Main](uploading-files-cs/samples/sample1.xml)]

Po aktualizaci `Web.sitemap`chvíli počkejte, než se zobrazí web kurzy prostřednictvím prohlížeče. Nabídka na levé straně teď obsahuje položky pro práci s binárními kurzy dat.

![Mapa webu teď obsahuje položky pro práci s binárními kurzy dat](uploading-files-cs/_static/image3.gif)

**Obrázek 3**: Mapa webu teď obsahuje položky pro práci s binárními kurzy dat.

## <a name="step-2-deciding-where-to-store-the-binary-data"></a>Krok 2: rozhodnutí, kam uložit binární data

Binární data spojená s datovým modelem aplikace s mohou být uložena na jednom ze dvou míst: v systému souborů webového serveru s odkazem na soubor uložený v databázi. nebo přímo v samotné databázi (viz obrázek 4). Každý přístup má svou vlastní sadu specialistů a nevýhody a je podrobnější diskuzi.

[![binární data mohou být uložena v systému souborů nebo přímo v databázi.](uploading-files-cs/_static/image4.gif)](uploading-files-cs/_static/image3.png)

**Obrázek 4**: binární data se můžou ukládat do systému souborů nebo přímo do databáze ([kliknutím zobrazíte obrázek v plné velikosti).](uploading-files-cs/_static/image4.png)

Představte si, že chceme databázi Northwind rozšíříme, aby k jednotlivým produktům přidružil obrázek. Jednou z možností je uložit tyto soubory obrázků do systému souborů webového serveru s a zaznamenat cestu v `Products` tabulce. S tímto přístupem přidáme sloupec `ImagePath` do tabulky `Products` typu `varchar(200)`, možná. Když uživatel nahrál obrázek pro adresu Chai, může být tento obrázek uložený v systému souborů webového serveru s na `~/Images/Tea.jpg`, kde `~` představuje fyzickou cestu aplikace. To znamená, že pokud je web rootem na fyzické cestě `C:\Websites\Northwind\`, `~/Images/Tea.jpg` by byl ekvivalentní `C:\Websites\Northwind\Images\Tea.jpg`. Po nahrání souboru obrázku aktualizujeme záznam Chai v tabulce `Products`, aby se jeho `ImagePath` sloupec odkazoval na cestu k novému obrázku. Můžeme použít `~/Images/Tea.jpg` nebo jenom `Tea.jpg`, pokud jsme se rozhodli, že se všechny image produktů umístí do složky `Images` aplikací.

Mezi hlavní výhody ukládání binárních dat v systému souborů patří:

- **Snadné implementace** při krátkém výskytu, ukládání a načítání binárních dat uložených přímo v databázi zahrnuje trochu větší kód než při práci s daty prostřednictvím systému souborů. Aby mohl uživatel zobrazit nebo stáhnout binární data, musí být předložen s adresou URL těchto dat. Pokud se data nachází v systému souborů webového serveru s, adresa URL je jednoduchá. Pokud jsou data uložena v databázi, je třeba vytvořit webovou stránku, která načte a vrátí data z databáze.
- **Širší přístup k binárním datům** může být potřeba, aby binární data byla dostupná pro jiné služby nebo aplikace, které nemůžou přečítat data z databáze. Například Image přidružené k jednotlivým produktům můžou být k dispozici také uživatelům prostřednictvím [FTP](http://en.wikipedia.org/wiki/File_Transfer_Protocol). v takovém případě je třeba uložit binární data do systému souborů.
- **Výkon** v případě, že jsou binární data uložena v systému souborů, bude zatížení a zahlcení sítě mezi databázovým serverem a webovým serverem menší než v případě, že jsou binární data ukládána přímo v rámci databáze.

Hlavní nevýhodou ukládání binárních dat v systému souborů je, že odděluje data z databáze. Pokud se záznam z `Products` tabulky odstraní, přidružený soubor v systému souborů webového serveru s se automaticky neodstraní. Abychom mohli soubor odstranit, je potřeba napsat další kód, jinak se soubor nepoužívá v nepoužitém, osamoceném souboru. Při zálohování databáze musíme také zajistit, aby se v systému souborů musely zálohovat související binární data. Přesunutí databáze na jiný web nebo na server přináší podobné problémy.

Případně lze binární data uložit přímo do databáze Microsoft SQL Server 2005 vytvořením sloupce typu `varbinary`. Podobně jako u jiných datových typů s proměnlivou délkou můžete zadat maximální délku binárních dat, která lze v tomto sloupci uchovávat. Například pro vyhradení na maximum 5 000 bajtů použijte `varbinary(5000)`; `varbinary(MAX)` umožňuje maximální velikost úložiště, přibližně 2 GB.

Hlavní výhodou ukládání binárních dat přímo v databázi je těsné spojení mezi binárními daty a záznamem databáze. Tím se značně zjednodušily úlohy správy databáze, jako je zálohování nebo přesun databáze na jiný web nebo server. Odstraněním záznamu se také automaticky odstraní odpovídající binární data. Existují také složitější výhody ukládání binárních dat v databázi. Podrobnější diskuzi najdete v tématu [ukládání binárních souborů přímo v databázi pomocí ASP.NET 2,0](http://aspnet.4guysfromrolla.com/articles/120606-1.aspx) .

> [!NOTE]
> V Microsoft SQL Server 2000 a starších verzích měl `varbinary` datový typ maximální limit 8 000 bajtů. Chcete-li uložit až 2 GB binárních dat, je třeba místo toho použít [datový typ`image`](https://msdn.microsoft.com/library/ms187993.aspx) . Při přidání `MAX` v SQL Server 2005 se ale datový typ `image` už nepoužívá. Podporuje se i pro zpětnou kompatibilitu, ale společnost Microsoft oznámila, že datový typ `image` bude v budoucí verzi SQL Server odebraný.

Pokud pracujete se starším datovým modelem, může se zobrazit `image` datový typ. Tabulka Northwind Database s `Categories` obsahuje sloupec `Picture`, který se dá použít k uložení binárních dat souboru obrázku pro danou kategorii. Vzhledem k tomu, že databáze Northwind má své kořeny v aplikaci Microsoft Access a starších verzích SQL Server, je tento sloupec typu `image`.

Pro tento kurz a další tři budeme používat oba přístupy. Tabulka `Categories` již obsahuje `Picture` sloupec pro ukládání binárního obsahu obrázku pro kategorii. Přidáme další sloupec `BrochurePath`pro uložení cesty k souboru PDF v systému souborů webového serveru s, který se dá použít k zajištění kvalitního přehledu o kategorii pro tisk.

## <a name="step-3-adding-thebrochurepathcolumn-to-thecategoriestable"></a>Krok 3: Přidání sloupce`BrochurePath`do tabulky`Categories`

V současné době má tabulka Categories pouze čtyři sloupce: `CategoryID`, `CategoryName`, `Description`a `Picture`. Kromě těchto polí musíme přidat nový, který bude odkazovat na brožuru kategorie s (pokud existuje). Chcete-li přidat tento sloupec, přejděte na Průzkumník serveru, přejděte k podrobnostem tabulky, klikněte pravým tlačítkem myši na tabulku `Categories` a vyberte možnost otevřít definici tabulky (viz obrázek 5). Pokud nevidíte Průzkumník serveru, udělejte to tak, že vyberete možnost Průzkumník serveru v nabídce zobrazení, nebo stiskněte CTRL + ALT + S.

Do tabulky `Categories` s názvem `BrochurePath` přidejte nový sloupec `varchar(200)` a povolí `NULL` a klikněte na ikonu Uložit (nebo stiskněte klávesu CTRL + S).

[![přidat sloupec BrochurePath do tabulky Categories](uploading-files-cs/_static/image5.gif)](uploading-files-cs/_static/image5.png)

**Obrázek 5**: přidání sloupce `BrochurePath` do tabulky `Categories` ([kliknutím zobrazíte obrázek v plné velikosti](uploading-files-cs/_static/image6.png))

## <a name="step-4-updating-the-architecture-to-use-thepictureandbrochurepathcolumns"></a>Krok 4: Aktualizace architektury pro použití sloupců`Picture`a`BrochurePath`

`CategoriesDataTable` ve vrstvě pro přístup k datům (DAL) v současné době má definováno čtyři `DataColumn` s: `CategoryID`, `CategoryName`, `Description`a `NumberOfProducts`. Když jsme tento DataTable původně navrhli v kurzu [Vytvoření vrstvy přístupu k datům](../introduction/creating-a-data-access-layer-cs.md) , `CategoriesDataTable` mít jenom první tři sloupce; `NumberOfProducts` sloupec byl přidán v [seznamu hlavní/podrobnosti pomocí seznamu hlavních záznamů s odrážkami s kurzem podrobností DataList](../filtering-scenarios-with-the-datalist-and-repeater/master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md) .

Jak je popsáno v tématu *Vytvoření vrstvy přístupu k datům*, tvoří datové tabulky v zadané datové sadě obchodní objekty. Objekty TableAdapter zodpovídá za komunikaci s databází a naplnění obchodních objektů pomocí výsledků dotazu. `CategoriesDataTable` vyplní `CategoriesTableAdapter`, která má tři metody načítání dat:

- `GetCategories()` spustí hlavní dotaz TableAdapter s a vrátí pole `CategoryID`, `CategoryName`a `Description` všech záznamů v tabulce `Categories`. Hlavní dotaz je používán automaticky generovanými `Insert` a metodami `Update`.
- `GetCategoryByCategoryID(categoryID)` vrátí pole `CategoryID`, `CategoryName`a `Description` kategorie, jejichž `CategoryID` se rovná hodnotě *KódKategorie*.
- `GetCategoriesAndNumberOfProducts()` – vrátí pole `CategoryID`, `CategoryName`a `Description` pro všechny záznamy v tabulce `Categories`. Používá také poddotaz k vrácení počtu produktů přidružených ke každé kategorii.

Všimněte si, že žádný z těchto dotazů nevrátí `Categories` tabulce `Picture` nebo `BrochurePath` sloupců; ani `CategoriesDataTable` pro tato pole zadat `DataColumn`. Aby bylo možné pracovat s vlastnostmi obrázku a `BrochurePath`, je nutné je nejprve přidat do `CategoriesDataTable` a poté aktualizovat třídu `CategoriesTableAdapter`, aby tyto sloupce vracela.

## <a name="adding-thepictureandbrochurepathdatacolumn-s"></a>Přidání`Picture`a`BrochurePath``DataColumn` s

Začněte přidáním těchto dvou sloupců do `CategoriesDataTable`. Klikněte pravým tlačítkem na záhlaví `CategoriesDataTable` s, v místní nabídce vyberte Přidat a pak zvolte možnost sloupec. Tím se vytvoří nový `DataColumn` v objektu DataTable s názvem `Column1`. Přejmenujte tento sloupec na `Picture`. V okno Vlastnosti nastavte vlastnost `DataColumn` s `DataType` na `System.Byte[]` (nejedná se o možnost v rozevíracím seznamu, je nutné ji zadat).

[![vytvořit datový sloupec s názvem Picture, jehož datový typ je System. Byte []](uploading-files-cs/_static/image6.gif)](uploading-files-cs/_static/image7.png)

**Obrázek 6**: vytvoření `DataColumn` s názvem `Picture`, jehož `DataType` je `System.Byte[]` ([kliknutím zobrazíte obrázek v plné velikosti](uploading-files-cs/_static/image8.png))

Přidejte do objektu DataTable další `DataColumn` a pojmenujte ji `BrochurePath` pomocí výchozí `DataType` hodnoty (`System.String`).

## <a name="returning-thepictureandbrochurepathvalues-from-the-tableadapter"></a>Vrácení`Picture`a`BrochurePath`hodnot z TableAdapter

Po přidání těchto dvou `DataColumn`ů do `CategoriesDataTable`jsme připraveni aktualizovat `CategoriesTableAdapter`. V hlavním dotazu TableAdapter můžeme mít oba tyto hodnoty sloupců, ale to by při každém vyvolání metody `GetCategories()` vrátilo binární data. Místo toho aktualizujte hlavní dotaz TableAdapter tak, aby vracel `BrochurePath` a vytvořil další metodu načtení dat, která vrátí konkrétní kategorii `Picture` sloupci.

Chcete-li aktualizovat hlavní dotaz TableAdapter, klikněte pravým tlačítkem myši na hlavičku `CategoriesTableAdapter` s a v místní nabídce vyberte možnost konfigurovat. Tím se zobrazí Průvodce konfigurací adaptéru tabulky, který jsme viděli v několika minulých kurzech. Aktualizujte dotaz tak, aby se vrátil `BrochurePath` a klikněte na Dokončit.

[![aktualizujte seznam sloupců v příkazu SELECT tak, aby vracel také BrochurePath](uploading-files-cs/_static/image7.gif)](uploading-files-cs/_static/image9.png)

**Obrázek 7**: aktualizace seznamu sloupců v příkazu `SELECT`, aby se vracely taky `BrochurePath` ([kliknutím zobrazíte obrázek v plné velikosti](uploading-files-cs/_static/image10.png))

Při použití příkazů SQL ad hoc pro TableAdapter aktualizuje seznam sloupců v hlavním dotazu seznam sloupců pro všechny metody `SELECT` dotazů v TableAdapter. To znamená, že `GetCategoryByCategoryID(categoryID)` metoda byla aktualizována tak, aby vracela sloupec `BrochurePath`, což může být to, co zamýšleli. Ale aktualizoval také seznam sloupců v metodě `GetCategoriesAndNumberOfProducts()` a odebrali jsme tak poddotaz, který vrátí počet produktů pro každou kategorii. Proto musíme tuto metodu s `SELECT` dotazem aktualizovat. Klikněte pravým tlačítkem na metodu `GetCategoriesAndNumberOfProducts()`, vyberte konfigurovat a vraťte `SELECT` dotaz zpátky na původní hodnotu:

[!code-sql[Main](uploading-files-cs/samples/sample2.sql)]

Dále vytvořte novou metodu TableAdapter, která vrátí určitou kategorii s `Picture` hodnotou sloupce. Klikněte pravým tlačítkem na záhlaví `CategoriesTableAdapter` s a vyberte možnost Přidat dotaz. spustí se Průvodce konfigurací dotazu TableAdapter. První krok tohoto průvodce se zeptá, jestli chceme dotazovat data pomocí příkazu SQL ad hoc, nové uložené procedury nebo existující. Vyberte možnost použít příkazy jazyka SQL a klikněte na tlačítko Další. Vzhledem k tomu, že vrátíme řádek, zvolte v druhém kroku možnost vybrat, která vrací řádky.

[![výběru možnosti použít příkazy SQL](uploading-files-cs/_static/image8.gif)](uploading-files-cs/_static/image11.png)

**Obrázek 8**: vyberte možnost použít příkazy SQL ([kliknutím zobrazíte obrázek v plné velikosti](uploading-files-cs/_static/image12.png)).

[![vzhledem k tomu, že dotaz vrátí záznam z tabulky Categories, zvolte vybrat, který vrátí řádky.](uploading-files-cs/_static/image9.gif)](uploading-files-cs/_static/image13.png)

**Obrázek 9**: vzhledem k tomu, že dotaz vrátí záznam z tabulky Categories, zvolte vybrat, který vrátí řádky ([kliknutím zobrazíte obrázek v plné velikosti).](uploading-files-cs/_static/image14.png)

V třetím kroku zadejte následující dotaz SQL a klikněte na další:

[!code-sql[Main](uploading-files-cs/samples/sample3.sql)]

Posledním krokem je výběr názvu nové metody. Pro naplnění objektu DataTable použijte `FillCategoryWithBinaryDataByCategoryID` a `GetCategoryWithBinaryDataByCategoryID` a vraťte se ke vzorům DataTable. Kliknutím na Dokončit dokončete průvodce.

[![zvolit názvy pro metody TableAdapter s](uploading-files-cs/_static/image10.gif)](uploading-files-cs/_static/image15.png)

**Obrázek 10**: vyberte názvy pro metody TableAdapter s ([kliknutím zobrazíte obrázek v plné velikosti](uploading-files-cs/_static/image16.png)).

> [!NOTE]
> Po dokončení Průvodce konfigurací dotazu na tabulkový adaptér se může zobrazit dialogové okno s dotazem, že nový text příkazu vrátí data se schématem, které se liší od schématu hlavního dotazu. V krátkém případě Průvodce zaznamená, že hlavní `GetCategories()` dotaz TableAdapter s vrací jiné schéma než ten, který jsme právě vytvořili. Ale to je to, co chceme, takže můžete tuto zprávu ignorovat.

Mějte na paměti, že pokud používáte příkazy SQL ad hoc a pomocí Průvodce změníte hlavní dotaz TableAdapter s v pozdějším časovém okamžiku, změní se seznam sloupců `GetCategoryWithBinaryDataByCategoryID` metoda s `SELECT`, aby se zahrnuly jenom tyto sloupce z hlavního dotazu (to znamená, že se z dotazu odebere sloupec `Picture`). Seznam sloupců bude nutné aktualizovat ručně, aby vracel sloupec `Picture`, podobně jako v předchozích krocích v tomto kroku jsme použili metodu `GetCategoriesAndNumberOfProducts()`.

Po přidání dvou `DataColumn` s do `CategoriesDataTable` a metody `GetCategoryWithBinaryDataByCategoryID` do `CategoriesTableAdapter`by tyto třídy v Návrháři typované datové sady měly vypadat jako snímek obrazovky na obrázku 11.

![Návrhář DataSet obsahuje nové sloupce a metodu.](uploading-files-cs/_static/image11.gif)

**Obrázek 11**: Návrhář datových sad zahrnuje nové sloupce a metodu.

## <a name="updating-the-business-logic-layer-bll"></a>Aktualizace vrstvy obchodní logiky (knihoven BLL)

Po aktualizaci DAL je vše potřeba rozšířit vrstvu obchodní logiky (knihoven BLL) tak, aby zahrnovala metodu pro novou metodu `CategoriesTableAdapter`. Do `CategoriesBLL` třídy přidejte následující metodu:

[!code-csharp[Main](uploading-files-cs/samples/sample4.cs)]

## <a name="step-5-uploading-a-file-from-the-client-to-the-web-server"></a>Krok 5: nahrání souboru z klienta na webový server

Při shromažďování binárních dat často tato data dodávají koncovým uživatelem. Aby bylo možné tyto informace zachytit, musí být uživatel schopný nahrávat soubor ze svého počítače na webový server. Nahraná data pak musí být integrovaná s datovým modelem, což může znamenat, že soubor se uloží do systému souborů webového serveru s a přidá cestu k souboru do databáze nebo zapíše binární obsah přímo do databáze. V tomto kroku se podíváme na to, jak uživateli dovolit nahrávat soubory ze svého počítače na server. V dalším kurzu zapnete naši pozornost pro integraci nahraného souboru s datovým modelem.

[Webový ovládací prvek](https://msdn.microsoft.com/library/ms227677(VS.80).aspx) ASP.NET 2,0 s New Upload poskytuje mechanismus pro uživatele, kteří odesílají soubor ze svého počítače na webový server. Ovládací prvek nahrání souboru se vykresluje jako `<input>` element, jehož atribut `type` je nastaven na soubor, které prohlížeče se zobrazí jako textové pole s tlačítkem Procházet. Kliknutím na tlačítko Procházet zobrazíte dialogové okno, ve kterém může uživatel vybrat soubor. Když se formulář publikuje zpátky, vybraný obsah souborů s se pošle spolu s zpětným voláním. Na straně serveru jsou informace o nahraném souboru přístupné prostřednictvím vlastností ovládacího prvku pro nahrání souboru.

Chcete-li předvést nahrávání souborů, otevřete stránku `FileUpload.aspx` ve složce `BinaryData`, přetáhněte ovládací prvek pro nahrání souboru ze sady nástrojů do návrháře a nastavte vlastnost `ID` ovládacího prvku na `UploadTest`. Dále přidejte ovládací prvek web Button nastavení `ID` a `Text` vlastností na `UploadButton` a nahrajte vybraný soubor v uvedeném pořadí. Nakonec umístěte ovládací prvek popisek webu pod tlačítko, vymažte jeho vlastnost `Text` a nastavte jeho vlastnost `ID` na `UploadDetails`.

[![přidat na stránku ASP.NET ovládací prvek pro nahrání souborů](uploading-files-cs/_static/image12.gif)](uploading-files-cs/_static/image17.png)

**Obrázek 12**: Přidání ovládacího prvku nahrání souborů na stránku ASP.NET ([kliknutím zobrazíte obrázek v plné velikosti](uploading-files-cs/_static/image18.png))

Obrázek 13 ukazuje tuto stránku při prohlížení v prohlížeči. Všimněte si, že kliknutím na tlačítko Procházet zobrazíte dialogové okno Výběr souboru, které uživateli umožňuje vybrat soubor ze svého počítače. Po výběru souboru dojde po kliknutí na tlačítko nahrát vybraný soubor k odeslání zpětného volání, které pošle vybraný binární obsah souboru s na webový server.

[![může uživatel vybrat soubor, který se má odeslat ze svého počítače na server.](uploading-files-cs/_static/image13.gif)](uploading-files-cs/_static/image19.png)

**Obrázek 13**: uživatel může vybrat soubor, který se má nahrát z počítače na server ([kliknutím zobrazíte obrázek v plné velikosti).](uploading-files-cs/_static/image20.png)

Při zpětném odeslání se nahraný soubor může uložit do systému souborů nebo jeho binární data může pracovat přímo přes datový proud. V tomto příkladu vytvoříme složku `~/Brochures` a uložíte tam uložený soubor. Začněte přidáním `Brochures` složky do lokality jako podsložky kořenového adresáře. Dále vytvořte obslužnou rutinu události pro událost `Click` `UploadButton` s a přidejte následující kód:

[!code-csharp[Main](uploading-files-cs/samples/sample5.cs)]

Ovládací prvek nahrání souborů poskytuje celou řadu vlastností pro práci s nahranými daty. Například [vlastnost`HasFile`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload.hasfile.aspx) označuje, zda byl soubor nahrán uživatelem, zatímco [vlastnost`FileBytes`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.fileupload.filebytes.aspx) poskytuje přístup k nahraným binárním datům jako pole bajtů. Obslužná rutina události `Click` se spustí tím, že zajistí, že se soubor nahrál. Pokud byl soubor nahrán, popisek zobrazuje název nahraného souboru, jeho velikost v bajtech a jeho typ obsahu.

> [!NOTE]
> Chcete-li zajistit, aby uživatel načetl soubor, můžete zkontrolovat vlastnost `HasFile` a zobrazit upozornění, pokud se `false`, nebo můžete místo toho použít [ovládací prvek RequiredFieldValidator](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/validation/default.aspx) .

Soubor upload s `SaveAs(filePath)` uloží nahraný soubor do zadaného souboru *FilePath*. *FilePath* musí být *fyzická cesta* (`C:\Websites\Brochures\SomeFile.pdf`) místo *virtuální* *cesty* (`/Brochures/SomeFile.pdf`). [Metoda`Server.MapPath(virtPath)`](https://msdn.microsoft.com/library/system.web.httpserverutility.mappath.aspx) přebírá virtuální cestu a vrátí její odpovídající fyzickou cestu. Tady je virtuální cesta `~/Brochures/fileName`, kde *filename* je název nahraného souboru. Další informace o virtuálních a fyzických cestách a použití `Server.MapPath`najdete v tématu [použití serveru. MapPath](http://www.4guysfromrolla.com/webtech/121799-1.shtml) .

Po dokončení obslužné rutiny události `Click` chvíli počkejte, než se otestuje stránka v prohlížeči. Klikněte na tlačítko Procházet a vyberte soubor z pevného disku a pak klikněte na tlačítko nahrát vybraný soubor. Postback odešle obsah vybraného souboru na webový server, který zobrazí informace o souboru před jeho uložením do složky `~/Brochures`. Po nahrání souboru se vraťte do sady Visual Studio a klikněte na tlačítko Aktualizovat v Průzkumník řešení. Měli byste vidět soubor, který jste právě Nahráli ve složce ~/Brochures.

[![soubor EvolutionValley. jpg byl nahrán na webový server.](uploading-files-cs/_static/image14.gif)](uploading-files-cs/_static/image21.png)

**Obrázek 14**: soubor `EvolutionValley.jpg` byl nahrán na webový server ([kliknutím zobrazíte obrázek v plné velikosti](uploading-files-cs/_static/image22.png)).

![EvolutionValley. jpg se uložil do složky ~/Brochures.](uploading-files-cs/_static/image15.gif)

**Obrázek 15**: `EvolutionValley.jpg` byl uložen do složky `~/Brochures`

## <a name="subtleties-with-saving-uploaded-files-to-the-file-system"></a>Odlišností s uložením nahraných souborů do systému souborů

Při ukládání nahrávání souborů do systému souborů webového serveru s je třeba řešit několik odlišností. Za prvé se vyskytl problém s zabezpečením. Aby bylo možné uložit soubor do systému souborů, musí mít kontext zabezpečení, pod kterým je stránka ASP.NET spuštěná, oprávnění k zápisu. Webový server ASP.NET Development běží v kontextu aktuálního uživatelského účtu. Pokud jako webový server používáte Microsoft s Internetová informační služba (IIS), závisí kontext zabezpečení na verzi služby IIS a její konfiguraci.

Další výzvou k ukládání souborů do systému souborů se otáčí kolem názvů souborů. V současné době stránka ukládá všechny nahrané soubory do adresáře `~/Brochures` pomocí stejného názvu jako soubor v počítači klienta s. Pokud uživatel A nahraje brožuru s názvem `Brochure.pdf`, soubor se uloží jako `~/Brochure/Brochure.pdf`. Ale co když někdy později uživatel B nahraje jiný soubor brožury, ke kterému má stejný název souboru (`Brochure.pdf`)? S kódem, který teď máme, se soubor User A s přepíše pomocí nahrávání uživatele B s.

Existuje několik postupů pro řešení konfliktů názvů souborů. Jednou z možností je zakázat nahrávání souboru, pokud už existuje jeden se stejným názvem. Když se v tomto postupu uživatel B pokusí odeslat soubor s názvem `Brochure.pdf`, systém ho neuloží a místo toho se zobrazí zpráva s oznámením, že soubor přejmenoval uživatel B, a zkuste to znovu. Další možností je uložit soubor s jedinečným názvem souboru, což může být [globálně jedinečný identifikátor (GUID)](http://en.wikipedia.org/wiki/Globally_Unique_Identifier) nebo hodnota z odpovídajících sloupců záznamů databáze s primárními klíči (za předpokladu, že je odeslání přidruženo k určitému řádku v datovém modelu). V dalším kurzu podrobněji prozkoumáme tyto možnosti.

## <a name="challenges-involved-with-very-large-amounts-of-binary-data"></a>Problémy související s velmi velkým objemem binárních dat

V těchto kurzech se předpokládá, že zaznamenaná binární data jsou velmi velmi velká. Práce s velmi velkým objemem binárních datových souborů, které jsou v několika megabajtech nebo větší, přináší nové výzvy, které přesahují rámec těchto kurzů. Například ve výchozím nastavení ASP.NET odmítne odesílání více než 4 MB, i když lze nakonfigurovat prostřednictvím [elementu`<httpRuntime>`](https://msdn.microsoft.com/library/e1f13641.aspx) v `Web.config`. Služba IIS ukládá i vlastní omezení velikosti nahrávání souborů. Další informace najdete v tématu o [velikosti souboru pro nahrání služby IIS](http://vandamme.typepad.com/development/2005/09/iis_upload_file.html) . Kromě toho může čas potřebný k nahrání velkých souborů překročit výchozí 110 sekund, než se ASP.NET počká na požadavek. K dispozici jsou také problémy s pamětí a výkonem, které vznikají při práci s velkými soubory.

Ovládací prvek nahrání souboru je nepraktický pro nahrávání velkých souborů. Vzhledem k tomu, že se obsah souborů odesílá na server, musí koncový uživatel sami čekat bez potvrzení, že jejich nahrávání probíhá. Nejedná se tedy o problém při práci s menšími soubory, které je možné nahrát během několika sekund, ale může se jednat o problém při práci s většími soubory, které mohou trvat déle než jedna minuta. Existují různé ovládací prvky pro nahrávání souborů třetích stran, které jsou vhodnější pro zpracování rozsáhlých nahrávání a mnohé z těchto dodavatelů poskytují indikátory průběhu a Správce nahrávání ActiveX, kteří představují mnohem pokročilejší prostředí pro uživatele.

Pokud vaše aplikace potřebuje zpracovat velké soubory, budete muset pečlivě prozkoumat výzvy a najít vhodná řešení pro vaše konkrétní potřeby.

## <a name="summary"></a>Přehled

Sestavování aplikace, která potřebuje zachytit binární data, zavádí řadu problémů. V tomto kurzu jsme prozkoumali první dvě: rozhodnutí, kam uložit binární data a umožníte uživateli nahrávat binární obsah prostřednictvím webové stránky. V dalších třech kurzech se dozvíte, jak přidružit nahraná data k záznamu v databázi a jak zobrazit binární data společně s textovými datovými poli.

Šťastné programování!

## <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Použití datových typů s velkými hodnotami](https://msdn.microsoft.com/library/ms178158.aspx)
- [Rychlé zprovoznění ovládacího prvku nahrání souborů](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/standard/fileupload.aspx)
- [Serverový ovládací prvek pro nahrávání souborů ASP.NET 2,0](http://www.wrox.com/WileyCDA/Section/id-292158.html)
- [Tmavá strana nahrávání souborů](http://www.aspnetresources.com/articles/dark_side_of_file_uploads.aspx)

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Teresa Murphy a Bernadette Leigh. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](displaying-binary-data-in-the-data-web-controls-cs.md)

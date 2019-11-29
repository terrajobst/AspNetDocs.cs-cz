---
uid: web-forms/overview/data-access/introduction/creating-a-data-access-layer-vb
title: Vytvoření vrstvy přístupu k datům (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu začneme od začátku a vytvoříme vrstvy přístupu k datům (DAL) pomocí zadaných datových sad pro přístup k informacím v databázi.
ms.author: riande
ms.date: 04/05/2010
ms.assetid: 6227233a-6254-4b6b-9a89-947efef22330
msc.legacyurl: /web-forms/overview/data-access/introduction/creating-a-data-access-layer-vb
msc.type: authoredcontent
ms.openlocfilehash: 51c9255f80f83a68cf26decf318347752498491a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74635140"
---
# <a name="creating-a-data-access-layer-vb"></a>Vytvoření vrstvy přístupu k datům (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_1_VB.exe) nebo [Stáhnout PDF](creating-a-data-access-layer-vb/_static/datatutorial01vb1.pdf)

> V tomto kurzu začneme od začátku a vytvoříme vrstvy přístupu k datům (DAL) pomocí zadaných datových sad pro přístup k informacím v databázi.

## <a name="introduction"></a>Úvod

Jako vývojáři webu se naše pracoviště roztéká na práci s daty. Vytvoříme databáze pro ukládání dat, kód, který se má načíst a upravit, a webové stránky pro shromáždění a shrnutí. Toto je první kurz v řadě dlouhé řady, který bude prozkoumat techniky pro implementaci těchto běžných vzorů v ASP.NET 2,0. Začneme vytvořením [softwarové architektury](http://en.wikipedia.org/wiki/Software_architecture) složené z vrstvy přístupu k datům (dal) pomocí typových datových sad, vrstvy obchodní logiky (knihoven BLL), která vynutila vlastní obchodní pravidla, a prezentační vrstvu složenou ze stránek ASP.NET, které sdílejí společné rozložení stránky. Po navýšení back-endu základy se přesunete do vytváření sestav a ukážeme, jak zobrazit, shrnout, shromáždit a ověřit data z webové aplikace. Tyto kurzy jsou stručné a poskytují podrobné pokyny s mnoha snímky obrazovky, které vás provedou procesem vizuálně. Každý kurz je k dispozici v C# a Visual Basic verzích a zahrnuje stažení kompletního používaného kódu. (Tento první kurz je poměrně dlouhý, ale zbytek se prezentuje mnohem více digestible bloků dat.)

V těchto kurzech budeme používat verzi databáze Northwind verze Microsoft SQL Server 2005 Express, která je umístěná v adresáři `App_Data`. Kromě databázového souboru obsahuje `App_Data` složka také skripty SQL pro vytvoření databáze pro případ, že chcete použít jinou verzi databáze. Tyto skripty je možné stáhnout také [přímo od Microsoftu](https://www.microsoft.com/downloads/details.aspx?FamilyID=06616212-0356-46a0-8da2-eebc53a68034&amp;DisplayLang=en), pokud chcete. Pokud používáte jinou SQL Server verzi databáze Northwind, budete muset aktualizovat nastavení `NORTHWNDConnectionString` v souboru `Web.config` aplikace. Webová aplikace byla sestavena pomocí sady Visual Studio 2005 Professional Edition jako projekt webu založeného na systému souborů. Nicméně všechny kurzy budou fungovat stejně dobře i v bezplatné verzi sady Visual Studio 2005, [Visual Web Developer](https://msdn.microsoft.com/vstudio/express/vwd/).

V tomto kurzu začneme od začátku a vytvoříme vrstvy přístupu k datům (DAL) následovaný vytvořením [vrstvy obchodní logiky (knihoven BLL)](creating-a-business-logic-layer-vb.md) v druhém kurzu a při práci na [rozložení stránky a navigaci](master-pages-and-site-navigation-vb.md) ve třetí části. Kurzy po třetí straně budou sestaveny na základech, které jsou uvedeny v prvních třech. V tomto prvním kurzu máme spoustu pokrytí, takže můžete spustit Visual Studio a můžeme začít!

## <a name="step-1-creating-a-web-project-and-connecting-to-the-database"></a>Krok 1: Vytvoření webového projektu a připojení k databázi

Než můžeme vytvořit naši vrstvu přístupu k datům (DAL), musíme nejdřív vytvořit web a nastavit naši databázi. Začněte vytvořením nového webu ASP.NET založeného na systému souborů. To lze provést tak, že přejdete do nabídky soubor a zvolíte možnost Nový web a zobrazí se dialogové okno Nový web. Vyberte šablonu webu ASP.NET, nastavte rozevírací seznam umístění na systém souborů, vyberte složku, kam chcete umístit web, a nastavte jazyk na Visual Basic.

[![vytvoření nového webu založeného na systému souborů](creating-a-data-access-layer-vb/_static/image2.png)](creating-a-data-access-layer-vb/_static/image1.png)

**Obrázek 1**: vytvoření nového webu založeného na systému souborů ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-vb/_static/image3.png))

Tím se vytvoří nový web s `Default.aspx` stránkou ASP.NET, `App_Data` složkou a souborem `Web.config`.

Při vytvoření webu je dalším krokem přidání odkazu na databázi v Průzkumník serveru sady Visual Studio. Přidáním databáze do Průzkumník serveru můžete do sady Visual Studio přidat tabulky, uložené procedury, zobrazení a tak dále. Můžete také zobrazit data tabulky nebo vytvořit vlastní dotazy buď ručně, nebo graficky prostřednictvím Tvůrce dotazů. Kromě toho, když sestavíme typové datové sady pro DAL, bude nutné, aby sada Visual Studio odkazovala na databázi, ze které by měly být vytvořeny typové datové sady. I když můžeme poskytnout tyto informace o připojení v tomto okamžiku, Visual Studio automaticky naplní rozevírací seznam databází již registrovaných v Průzkumník serveru.

Postup přidání databáze Northwind do Průzkumník serveru závisí na tom, zda chcete použít databázi SQL Server 2005 Express Edition ve složce `App_Data` nebo pokud máte instalační program databázového serveru Microsoft SQL Server 2000 nebo 2005, který chcete použít místo toho.

## <a name="using-a-database-in-theapp_datafolder"></a>Použití databáze ve složce`App_Data`

Pokud nemáte databázový server SQL Server 2000 nebo 2005, ke kterému se chcete připojit, nebo chcete jednoduše zabránit nutnosti přidat databázi do databázového serveru, můžete použít SQL Server 2005 Express Edition verzi databáze Northwind, která je umístěná ve složce `App_Data` staženého webu (`NORTHWND.MDF`).

Databáze umístěná ve složce `App_Data` je automaticky přidána do Průzkumník serveru. Za předpokladu, že máte na svém počítači nainstalovanou SQL Server 2005 Express Edition, měli byste vidět uzel s názvem NORTHWND. MDF v Průzkumník serveru, který můžete rozbalit a prozkoumat jeho tabulky, zobrazení, uloženou proceduru atd. (viz obrázek 2).

Složka `App_Data` může také obsahovat soubory `.mdb` Microsoft Access, které se stejně jako jejich SQL Server protějšky automaticky přidávají do Průzkumník serveru. Pokud nechcete používat žádnou z možností SQL Server, můžete vždy [Stáhnout verzi Microsoft Access souboru databáze Northwind](https://www.microsoft.com/downloads/details.aspx?FamilyID=C6661372-8DBE-422B-8676-C632D66C529C&amp;displaylang=EN) a umístit ji do adresáře `App_Data`. Mějte ale na paměti, že přístup k databázím není jako SQL Server bez funkcí a není navržený tak, aby se používal ve scénářích webů. Kromě toho několik dalších 35 kurzů bude využívat některé funkce na úrovni databáze, které nejsou podporovány aplikací Access.

## <a name="connecting-to-the-database-in-a-microsoft-sql-server-2000-or-2005-database-server"></a>Připojení k databázi na databázovém serveru s Microsoft SQL Server 2000 nebo 2005

Případně se můžete připojit k databázi Northwind nainstalované na databázovém serveru. Pokud na databázovém serveru ještě není nainstalovaná databáze Northwind, musíte ji nejdřív přidat do databázového serveru spuštěním instalačního skriptu, který je součástí stažení tohoto kurzu, nebo [stažením verze SQL Server 2000 rozhraní Northwind a instalačního skriptu](https://www.microsoft.com/downloads/details.aspx?FamilyID=06616212-0356-46a0-8da2-eebc53a68034&amp;DisplayLang=en) přímo z webu společnosti Microsoft.

Po instalaci databáze přejděte na Průzkumník serveru v aplikaci Visual Studio, klikněte pravým tlačítkem na uzel datová připojení a vyberte Přidat připojení. Pokud se Průzkumník serveru nezobrazuje, přejděte do zobrazení/Průzkumník serveru nebo stiskněte kombinaci kláves CTRL + ALT + S. Tím se zobrazí dialogové okno Přidat připojení, kde můžete zadat server, ke kterému se chcete připojit, informace o ověřování a název databáze. Po úspěšné konfiguraci informací o připojení databáze a kliknutí na tlačítko OK bude databáze přidána jako uzel pod uzlem datová připojení. Uzel databáze můžete rozšířit a prozkoumat jeho tabulky, zobrazení, uložené procedury atd.

![Přidání připojení k databázi Northwind vašeho databázového serveru](creating-a-data-access-layer-vb/_static/image4.png)

**Obrázek 2**: Přidání připojení k databázi Northwind vašeho databázového serveru

## <a name="step-2-creating-the-data-access-layer"></a>Krok 2: vytvoření vrstvy přístupu k datům

Při práci s daty jedna z možností je vložení logiky specifické pro data přímo do prezentační vrstvy (ve webové aplikaci se ASP.NET stránky tvoří prezentační vrstvu). To může mít formu psaní kódu ADO.NET v části kódu stránky ASP.NET nebo použití ovládacího prvku SqlDataSource z části s označením. V obou případech tento přístup těsně Couples logiku přístupu k datům pomocí prezentační vrstvy. Doporučený postup je ale oddělit logiku přístupu k datům z prezentační vrstvy. Tato samostatná vrstva je označována jako vrstva přístupu k datům, je dál pro krátké a je obvykle implementována jako samostatný projekt knihovny tříd. Výhody této vrstvené architektury jsou dobře zdokumentováné (Další informace najdete v části "Další informace" na konci tohoto kurzu) a jedná se o přístup, který v této sérii provedeme.

Veškerý kód, který je specifický pro základní zdroj dat, jako je například vytvoření připojení k databázi, vydávání `SELECT`, `INSERT`, `UPDATE`a `DELETE` příkazů a tak dále by měl být umístěn ve složce DAL. Prezentační vrstva nesmí obsahovat odkazy na takový kód pro přístup k datům, ale místo toho by se mělo volat na DAL pro všechny a všechny požadavky na data. Vrstvy přístupu k datům typicky obsahují metody pro přístup k podkladovým datům databáze. Databáze Northwind obsahuje například `Products` a `Categories` tabulky, které zaznamenají produkty k prodeji a kategorie, do kterých patří. V naší DAL metody, jako jsou:

- `GetCategories(),`, které budou vracet informace o všech kategoriích
- `GetProducts()`, které budou vracet informace o všech produktech
- `GetProductsByCategoryID(categoryID)`, které budou vracet všechny produkty patřící do určité kategorie
- `GetProductByProductID(productID)`, které vrátí informace o konkrétním produktu

Tyto metody, pokud jsou vyvolány, se připojí k databázi, vydávají příslušný dotaz a vrátí výsledky. Způsob, jakým vracíme tyto výsledky, je důležitý. Tyto metody mohou jednoduše vracet datovou sadu nebo objekt DataReader vyplněný databázovým dotazem, ale v ideálním případě by měly být vráceny pomocí *objektů silně typovaného*typu. Silně typované objekty je jeden, jehož schéma je pevně definováno v době kompilace, zatímco opačný objekt s volným typem je jeden, jehož schéma není známo až do doby běhu.

Například objekt DataReader a datová sada (ve výchozím nastavení) jsou objekty volně typované, protože jejich schéma je definováno sloupci vrácenými databázovým dotazem použitým k naplnění. Pro přístup ke konkrétnímu sloupci z volně typovaného objektu DataTable potřebujeme použít syntaxi jako: `DataTable.Rows(index)("columnName")`. V tomto příkladu se v tomto příkladu projeví volné zadání, které potřebujeme pro přístup k názvu sloupce pomocí řetězce nebo pořadového indexu. Silně typované DataTable, na druhé straně, bude mít každý ze svých sloupců implementovaných jako vlastnosti, což vede k psaní kódu, který vypadá takto: `DataTable.Rows(index).columnName`.

Chcete-li vracet objekty silného typu, mohou vývojáři vytvořit své vlastní obchodní objekty nebo použít typové datové sady. Obchodní objekt je implementován vývojářem jako třída, jejíž vlastnosti typicky odrážejí sloupce podkladové databázové tabulky, kterou obchodní objekt představuje. Typová datová sada je třída vygenerovaná pro vás sadou Visual Studio na základě schématu databáze a jejíž členové jsou silně typované podle tohoto schématu. Zadaná datová sada obsahuje třídy, které přesahují třídy ADO.NET DataSet, DataTable a DataRow. Kromě typů DataTables se silnými typy teď typované datové sady teď zahrnují také objekty TableAdapter, což jsou třídy s metodami pro naplnění DataTables datové sady a rozšiřování úprav v rámci datových tabulek zpátky do databáze.

> [!NOTE]
> Další informace o výhodách a nevýhodách používání typových datových sad a vlastních obchodních objektů najdete v tématu [navrhování komponent datové vrstvy a předávání dat přes úrovně](https://msdn.microsoft.com/library/ms978496.aspx).

Pro tuto architekturu kurzů použijeme datové sady silného typu. Obrázek 3 znázorňuje pracovní postup mezi různými vrstvami aplikace, které používají typové datové sady.

[![veškerého kódu přístupu k datům je Relegated na DAL.](creating-a-data-access-layer-vb/_static/image6.png)](creating-a-data-access-layer-vb/_static/image5.png)

**Obrázek 3**: veškerý kód pro přístup k datům je RELEGATED na dal ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-vb/_static/image7.png)

## <a name="creating-a-typed-dataset-and-table-adapter"></a>Vytvoření typové datové sady a adaptéru tabulky

Pokud chcete začít vytvářet DAL, začněte tím, že do projektu přidáte typovou datovou sadu. Chcete-li to provést, klikněte pravým tlačítkem myši na uzel projektu v Průzkumník řešení a vyberte možnost Přidat novou položku. V seznamu šablon vyberte možnost datová sada a pojmenujte ji `Northwind.xsd`.

[![se rozhodnout přidat novou datovou sadu do projektu](creating-a-data-access-layer-vb/_static/image9.png)](creating-a-data-access-layer-vb/_static/image8.png)

**Obrázek 4**: vyberte, chcete-li do projektu přidat novou datovou sadu ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-vb/_static/image10.png)).

Po kliknutí na tlačítko Přidat se po zobrazení výzvy k přidání datové sady do složky `App_Code` klikněte na tlačítko Ano. Zobrazí se Návrhář pro typovou datovou sadu a spustí se Průvodce konfigurací TableAdapter, který vám umožní přidat svůj první TableAdapter do typované datové sady.

Typová datová sada slouží jako silně typované kolekce dat; skládá se ze silně typované instance DataTable, z nichž každá je tvořena instancemi DataRow se silnými typy. Vytvoříme silně typované datové tabulky pro každou z podkladových databázových tabulek, se kterými potřebujeme pracovat v této sérii kurzů. Začněte vytvořením DataTable pro tabulku `Products`.

Pamatujte, že datatabulka se silným typem neobsahuje žádné informace o tom, jak přistupovat k datům z jejich podkladové databázové tabulky. Aby bylo možné načíst data k naplnění objektu DataTable, používáme třídu TableAdapter, která funguje jako naše vrstva přístupu k datům. Pro náš `Products` DataTable bude TableAdapter obsahovat metody `GetProducts()`, `GetProductByCategoryID(categoryID)`a tak dále, které budeme vyvolávat z prezentační vrstvy. Role DataTable slouží jako objekty silného typu, které slouží k předávání dat mezi vrstvami.

Průvodce konfigurací TableAdapter začíná výzvou k výběru databáze, se kterou chcete pracovat. Rozevírací seznam zobrazuje tyto databáze v Průzkumník serveru. Pokud jste databázi Northwind nepřidali do Průzkumník serveru, můžete v tuto chvíli kliknout na tlačítko nové připojení.

[![zvolit databázi Northwind z rozevíracího seznamu](creating-a-data-access-layer-vb/_static/image12.png)](creating-a-data-access-layer-vb/_static/image11.png)

**Obrázek 5**: v rozevíracím seznamu vyberte databázi Northwind ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-vb/_static/image13.png)).

Po výběru databáze a kliknutí na tlačítko Další se zobrazí dotaz, zda chcete uložit připojovací řetězec do souboru `Web.config`. Uložením připojovacího řetězce se vyhnete tomu, aby byl pevně kódovaný v třídách TableAdapter, což zjednodušuje věci, pokud se v budoucnu změní informace připojovacího řetězce. Pokud se přihlásíte k uložení připojovacího řetězce v konfiguračním souboru, který je umístěn v části `<connectionStrings>`, která může být [volitelně zašifrovaná](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx) pro zvýšení zabezpečení nebo později upravena prostřednictvím nové stránky vlastností ASP.NET 2,0 v rámci nástroje pro správu grafického uživatelského rozhraní služby IIS, což je pro správce lépe ideální.

[![Uložit připojovací řetězec do souboru Web. config](creating-a-data-access-layer-vb/_static/image15.png)](creating-a-data-access-layer-vb/_static/image14.png)

**Obrázek 6**: uložení připojovacího řetězce do `Web.config` ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-vb/_static/image16.png))

Dále je potřeba definovat schéma pro první typ DataTable se silnými typy a zadat první metodu pro naše TableAdapter, která se má použít při naplňování silně typované datové sady. Tyto dva kroky jsou provedeny současně vytvořením dotazu, který vrací sloupce z tabulky, kterou chcete reflektovat v našem objektu DataTable. Na konci Průvodce poskytneme tomuto dotazu název metody. Po dokončení této metody lze tuto metodu vyvolat z naší prezentační vrstvy. Metoda spustí definovaný dotaz a naplní objekt DataTable silného typu.

Abyste mohli začít definovat dotaz SQL, musíte nejdřív určit, jak chceme, aby TableAdapter dotaz vydával. Můžeme použít příkaz SQL ad hoc, vytvořit novou uloženou proceduru nebo použít existující uloženou proceduru. V těchto kurzech budeme používat příkazy SQL ad hoc. Příklad použití uložených procedur najdete v článku [Brian Noyes](http://briannoyes.net/), [sestavení vrstvy přístupu k datům pomocí návrháře DataSet sady Visual Studio 2005](http://www.theserverside.net/articles/showarticle.tss?id=DataSetDesigner) .

[![dotazování na data pomocí příkazu SQL ad hoc](creating-a-data-access-layer-vb/_static/image18.png)](creating-a-data-access-layer-vb/_static/image17.png)

**Obrázek 7**: dotazování na data pomocí příkazu SQL ad hoc ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-vb/_static/image19.png))

V tuto chvíli můžeme zadat dotaz SQL ručně. Při vytváření první metody v TableAdapter, která obvykle chcete, aby dotaz vrátil tyto sloupce, které je nutné vyjádřit v odpovídajícím objektu DataTable. To můžete udělat tak, že vytvoříte dotaz, který vrátí všechny sloupce a všechny řádky z `Products` tabulky:

[![zadejte dotaz SQL do textového pole.](creating-a-data-access-layer-vb/_static/image21.png)](creating-a-data-access-layer-vb/_static/image20.png)

**Obrázek 8**: zadejte dotaz SQL do textového pole ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-vb/_static/image22.png)).

Případně můžete použít Tvůrce dotazů a graficky sestavit dotaz, jak je znázorněno na obrázku 9.

[![vytvořit dotaz graficky pomocí Editoru dotazů](creating-a-data-access-layer-vb/_static/image24.png)](creating-a-data-access-layer-vb/_static/image23.png)

**Obrázek 9**: vytvoření dotazu graficky pomocí Editoru dotazů ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-vb/_static/image25.png))

Po vytvoření dotazu, ale před přechodem na další obrazovku, klikněte na tlačítko Upřesnit možnosti. V projektech webů je jako jediná možnost pokročilé vybraná jako výchozí vybraná možnost Generovat příkazy INSERT, Update a DELETE. Pokud spustíte tohoto průvodce z knihovny tříd nebo projektu Windows, bude vybrána také možnost použít optimistickou souběžnost. Ponechte možnost použít optimistickou souběžnost pro teď nezaškrtnutou. V budoucích kurzech prověříme optimistickou souběžnost.

[![vyberte jenom možnost Generovat příkazy INSERT, Update a DELETE.](creating-a-data-access-layer-vb/_static/image27.png)](creating-a-data-access-layer-vb/_static/image26.png)

**Obrázek 10**: vyberte jenom možnost Generovat příkazy INSERT, Update a Delete ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-vb/_static/image28.png)

Po ověření rozšířených možností kliknutím na tlačítko Další přejděte na poslední obrazovku. Tady se zobrazí výzva k výběru metod, které se mají přidat do TableAdapter. Existují dva vzory pro naplnění dat:

- **Naplnit DataTable** pomocí tohoto přístupu metoda, která je vytvořena v objektu DataTable jako parametr a naplní ji na základě výsledků dotazu. Třída ADO.NET DataAdapter například implementuje tento model pomocí metody `Fill()`.
- **Vrátí DataTable** s tímto přístupem metoda vytvoří a vyplní objekt DataTable za vás a vrátí jej jako návratovou hodnotu metody.

Je možné, že TableAdapter implementuje jeden nebo oba tyto vzory. Zde uvedené metody lze také přejmenovat. Nechte obě zaškrtávací políčka zaškrtnutá, i když v těchto kurzech budeme používat jenom druhý vzor. Přejmenujte raději obecnou `GetData` metodu, která bude `GetProducts`.

Pokud je zaškrtnuto, konečné zaškrtávací políčko "GenerateDBDirectMethods" vytvoří `Insert()`, `Update()`a `Delete()` metody pro TableAdapter. Pokud necháte tuto možnost nezaškrtnutou, všechny aktualizace budou muset být provedeny prostřednictvím `Update()` metody, která přebírá typovou datovou sadu, objekt DataTable, jediný objekt DataRow nebo pole datových řádků. (Pokud jste nezaškrtli možnost Generovat příkazy INSERT, Update a DELETE z rozšířených vlastností na obrázku 9, nebude toto nastavení zaškrtávacího políčka nijak ovlivněno.) Pojďme toto políčko nechat zaškrtnuté.

[![změnit název metody z GetData na GetProducts](creating-a-data-access-layer-vb/_static/image30.png)](creating-a-data-access-layer-vb/_static/image29.png)

**Obrázek 11**: Změňte název metody z `GetData` na `GetProducts` ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-vb/_static/image31.png)

Dokončete průvodce kliknutím na tlačítko Dokončit. Po ukončení průvodce se vrátí do návrháře DataSet, který zobrazuje objekt DataTable, který jsme právě vytvořili. Můžete zobrazit seznam sloupců v `Products` DataTable (`ProductID`, `ProductName`a tak dále), a také metody `ProductsTableAdapter` (`Fill()` a `GetProducts()`).

[![do typové datové sady byly přidány objekty DataTable a ProductsTableAdapter.](creating-a-data-access-layer-vb/_static/image33.png)](creating-a-data-access-layer-vb/_static/image32.png)

**Obrázek 12**: `Products` DataTable a `ProductsTableAdapter` byla přidána do typové datové sady ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-vb/_static/image34.png)

V tuto chvíli máme typovou datovou sadu s jedním objektem DataTable (`Northwind.Products`) a třídou DataAdapter (`NorthwindTableAdapters.ProductsTableAdapter`) se silnými typy s metodou `GetProducts()`. Tyto objekty lze použít pro přístup k seznamu všech produktů z kódu, jako je:

[!code-vb[Main](creating-a-data-access-layer-vb/samples/sample1.vb)]

Tento kód nám nevyžadoval zápis jednoho bitu kódu specifického pro přístup k datům. Nemuseli bychom vytvářet instance žádné třídy ADO.NET, nemuseli by odkazovat na žádné připojovací řetězce, dotazy SQL nebo uložené procedury. Místo toho poskytuje TableAdapter kód pro přístup k datům na nízké úrovni pro nás.

Každý objekt použitý v tomto příkladu je také silného typu, což aplikaci Visual Studio umožňuje poskytovat technologii IntelliSense a kontrolu typu při kompilaci. A nejlepší ze všech datových tabulek vrácených TableAdapter může být svázán s datovými ovládacími prvky ASP.NET dat, jako je například GridView, DetailsView, DropDownList, CheckBoxList a několik dalších. Následující příklad znázorňuje vazbu objektu DataTable vráceného metodou `GetProducts()` do prvku GridView v pouze scant třech řádcích kódu v rámci obslužné rutiny události `Page_Load`.

AllProducts. aspx

[!code-aspx[Main](creating-a-data-access-layer-vb/samples/sample2.aspx)]

AllProducts. aspx. vb

[!code-vb[Main](creating-a-data-access-layer-vb/samples/sample3.vb)]

[![se seznam produktů zobrazuje v prvku GridView.](creating-a-data-access-layer-vb/_static/image36.png)](creating-a-data-access-layer-vb/_static/image35.png)

**Obrázek 13**: seznam produktů je zobrazen v prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-vb/_static/image37.png)).

I když tento příklad vyžaduje, abychom v budoucích kurzech zapsali tři řádky kódu v rámci obslužné rutiny události `Page_Load` stránky ASP.NET, prověříme, jak použít prvek ObjectDataSource k deklarativnímu načtení dat z DAL. V prvku ObjectDataSource nebudeme muset psát žádný kód a Podpora stránkování a řazení bude také.

## <a name="step-3-adding-parameterized-methods-to-the-data-access-layer"></a>Krok 3: Přidání parametrizovaných metod do vrstvy přístupu k datům

V tomto okamžiku naše `ProductsTableAdapter` třídy obsahuje ale jednu metodu, `GetProducts()`, která vrátí všechny produkty v databázi. I když je možné pracovat se všemi produkty, jsou v tuto chvíli k dispozici čas, kdy budeme chtít načíst informace o konkrétním produktu nebo všech produktech, které patří do určité kategorie. Pro přidání takových funkcí do naší vrstvy přístupu k datům můžeme přidat parametrizované metody do TableAdapter.

Pojďme přidat metodu `GetProductsByCategoryID(categoryID)`. Chcete-li do DAL přidat novou metodu, vraťte se do návrháře DataSet, klikněte pravým tlačítkem myši v části `ProductsTableAdapter` a vyberte možnost Přidat dotaz.

![Klikněte pravým tlačítkem na TableAdapter a vyberte Přidat dotaz.](creating-a-data-access-layer-vb/_static/image38.png)

**Obrázek 14**: klikněte pravým tlačítkem na TableAdapter a vyberte Přidat dotaz.

Nejdřív se zobrazí dotaz, jestli chceme získat přístup k databázi pomocí příkazu ad-hoc SQL nebo nové nebo existující uložené procedury. Zkusíme znovu použít příkaz SQL ad hoc. V dalším kroku se zobrazí dotaz, jaký typ dotazu SQL chceme použít. Vzhledem k tomu, že chceme vracet všechny produkty, které patří do určité kategorie, chceme napsat příkaz `SELECT`, který vrací řádky.

[![zvolit vytvoření příkazu SELECT, který vrátí řádky](creating-a-data-access-layer-vb/_static/image40.png)](creating-a-data-access-layer-vb/_static/image39.png)

**Obrázek 15**: volba pro vytvoření příkazu `SELECT`, který vrátí řádky ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-vb/_static/image41.png))

Dalším krokem je definování dotazu SQL, který se používá pro přístup k datům. Vzhledem k tomu, že chceme vracet pouze produkty, které patří do konkrétní kategorie, používám stejný příkaz `SELECT` z `GetProducts()`, ale přidejte následující klauzuli `WHERE`: `WHERE CategoryID = @CategoryID`. Parametr `@CategoryID` informuje Průvodce TableAdapter, že metoda, kterou vytváříme, bude vyžadovat vstupní parametr odpovídajícího typu (tj. celé číslo s možnou hodnotou null).

[![zadejte dotaz, který bude vracet jenom produkty v zadané kategorii.](creating-a-data-access-layer-vb/_static/image43.png)](creating-a-data-access-layer-vb/_static/image42.png)

**Obrázek 16**: zadejte dotaz, který bude vracet pouze produkty v zadané kategorii ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-vb/_static/image44.png)

V posledním kroku můžeme zvolit, které vzory přístupu k datům se mají použít, a také přizpůsobit názvy generovaných metod. Pro vzorek výplně změňte název na `FillByCategoryID` a pro návrat návratového vzoru DataTable (metody `GetX`), použijte `GetProductsByCategoryID`.

[![zvolit názvy pro metody TableAdapter](creating-a-data-access-layer-vb/_static/image46.png)](creating-a-data-access-layer-vb/_static/image45.png)

**Obrázek 17**: vyberte názvy pro metody TableAdapter ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-vb/_static/image47.png)).

Po dokončení průvodce obsahuje Návrhář DataSet nové metody TableAdapter.

![V produktech se teď dají dotazovat podle kategorie.](creating-a-data-access-layer-vb/_static/image48.png)

**Obrázek 18**: produkty se teď dají dotazovat podle kategorie

Chvíli přidejte `GetProductByProductID(productID)` metodu pomocí stejné techniky.

Tyto parametrizované dotazy mohou být testovány přímo z návrháře DataSet. Klikněte pravým tlačítkem na metodu v TableAdapter a vyberte možnost Náhled dat. Potom zadejte hodnoty, které chcete použít pro parametry, a klikněte na náhled.

[Zobrazí se ![těchto produktů patřících ke kategorii nápoje.](creating-a-data-access-layer-vb/_static/image50.png)](creating-a-data-access-layer-vb/_static/image49.png)

**Obrázek 19**: zobrazí se tyto produkty patřící do kategorie nápoje ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-vb/_static/image51.png)

Pomocí metody `GetProductsByCategoryID(categoryID)` v naší DAL teď můžeme vytvořit stránku ASP.NET, která zobrazí jenom produkty v zadané kategorii. Následující příklad ukazuje všechny produkty, které jsou v kategorii nápoje, které mají `CategoryID` 1.

Nápoje. aspx

[!code-aspx[Main](creating-a-data-access-layer-vb/samples/sample4.aspx)]

Nápoje. aspx. vb

[!code-vb[Main](creating-a-data-access-layer-vb/samples/sample5.vb)]

[![se zobrazí tyto produkty v kategorii nápoje.](creating-a-data-access-layer-vb/_static/image53.png)](creating-a-data-access-layer-vb/_static/image52.png)

**Obrázek 20**: zobrazí se tyto produkty v kategorii nápoje ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-vb/_static/image54.png)

## <a name="step-4-inserting-updating-and-deleting-data"></a>Krok 4: vkládání, aktualizace a odstraňování dat

Existují dva vzory, které se běžně používají pro vkládání, aktualizaci a odstraňování dat. První vzor, který bude volat přímý vzor databáze, zahrnuje vytváření metod, které při vyvolání vydávají příkaz `INSERT`, `UPDATE`nebo `DELETE` do databáze, která pracuje na jednom záznamu databáze. Tyto metody se obvykle předávají v řadě skalárních hodnot (celá čísla, řetězce, logické hodnoty, DateTime atd.), které odpovídají hodnotám pro vložení, aktualizaci nebo odstranění. Například s tímto modelem pro `Products` Table by Metoda Delete měla převzít parametr typu Integer, který označuje `ProductID` záznamu, který se má odstranit, zatímco metoda INSERT by převzala v řetězci pro `ProductName`, desetinnou čárkou pro `UnitPrice`, celé číslo pro `UnitsOnStock`a tak dále.

[![se každou žádost o vložení, aktualizaci a odstranění pošle do databáze hned](creating-a-data-access-layer-vb/_static/image56.png)](creating-a-data-access-layer-vb/_static/image55.png)

**Obrázek 21**: každý požadavek na vložení, aktualizaci a odstranění se pošle do databáze hned ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-vb/_static/image57.png)

Druhý model, na který se odkazuje jako na vzor aktualizace služby Batch, je aktualizovat celou datovou sadu, DataTable nebo kolekci datových řádků v jednom volání metody. V tomto vzoru vývojář odstraní, vloží a upraví datové řádky v objektu DataTable a pak tyto datové řádky nebo DataTable předá metodě aktualizace. Tato metoda potom vytvoří výčet předaných dat, určí, zda byly změněny, přidány nebo odstraněny (prostřednictvím hodnoty [vlastnosti RowState](https://msdn.microsoft.com/library/system.data.datarow.rowstate.aspx) objektu DataRow), a vydá požadavek odpovídající databáze pro každý záznam.

[![všechny změny jsou synchronizovány s databází při vyvolání metody Update](creating-a-data-access-layer-vb/_static/image59.png)](creating-a-data-access-layer-vb/_static/image58.png)

**Obrázek 22**: všechny změny jsou synchronizovány s databází při vyvolání metody Update ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-vb/_static/image60.png)

TableAdapter používá ve výchozím nastavení vzor dávkové aktualizace, ale podporuje také přímý vzor databáze. Vzhledem k tomu, že jsme při vytváření TableAdapter vybrali možnost Generovat příkazy INSERT, Update a DELETE z rozšířených vlastností, `ProductsTableAdapter` obsahuje `Update()` metodu, která implementuje vzor aktualizace služby Batch. Konkrétně TableAdapter obsahuje metodu `Update()`, kterou lze předat typovou datovou sadu, silně typované DataTable nebo jeden nebo více datových řádků. Pokud jste ponechali zaškrtávací políčko "GenerateDBDirectMethods" zaškrtnuté při prvním vytvoření TableAdapter, bude vzor DB Direct také implementován prostřednictvím metod `Insert()`, `Update()`a `Delete()`.

Jak vzorce změny dat používají vlastnosti `InsertCommand`, `UpdateCommand`a `DeleteCommand` k vystavení jejich `INSERT`, `UPDATE`a `DELETE` příkazů do databáze. Můžete zkontrolovat a upravit vlastnosti `InsertCommand`, `UpdateCommand`a `DeleteCommand` kliknutím na TableAdapter v Návrháři DataSet a pak na okno Vlastnosti. (Ujistěte se, že jste vybrali TableAdapter a že objekt `ProductsTableAdapter` je ten vybraný v rozevíracím seznamu okno Vlastnosti.)

[![vlastnost TableAdapter má vlastnosti InsertCommand, UpdateCommand a DeleteCommand.](creating-a-data-access-layer-vb/_static/image62.png)](creating-a-data-access-layer-vb/_static/image61.png)

**Obrázek 23**: TableAdapter obsahuje vlastnosti `InsertCommand`, `UpdateCommand`a `DeleteCommand` ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-vb/_static/image63.png)

Chcete-li prostudovat nebo změnit některou z těchto vlastností příkazu databáze, klikněte na podvlastnost `CommandText`, která zobrazí Tvůrce dotazů.

[![nakonfigurovat příkazy INSERT, UPDATE a DELETE v Tvůrce dotazů](creating-a-data-access-layer-vb/_static/image65.png)](creating-a-data-access-layer-vb/_static/image64.png)

**Obrázek 24**: nakonfigurujte příkazy `INSERT`, `UPDATE`a `DELETE` v Tvůrce dotazů ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-vb/_static/image66.png)).

Následující příklad kódu ukazuje, jak použít vzor dávkové aktualizace k dvojnásobku ceny za všechny produkty, které nejsou ukončené a které mají 25 jednotek na skladě nebo méně:

[!code-vb[Main](creating-a-data-access-layer-vb/samples/sample6.vb)]

Následující kód ukazuje, jak pomocí vzoru DB Direct programově odstranit konkrétní produkt, jak ho aktualizovat, a pak přidat nové:

[!code-vb[Main](creating-a-data-access-layer-vb/samples/sample7.vb)]

## <a name="creating-custom-insert-update-and-delete-methods"></a>Vytváření vlastních metod vložení, aktualizace a odstranění

Metody `Insert()`, `Update()`a `Delete()` vytvořené metodou DB Direct můžou být náročné na bit, zejména u tabulek s mnoha sloupci. V předchozím příkladu kódu, bez pomocníka IntelliSense, není obzvláště jasné, co `Products` sloupec tabulky mapuje na každý vstupní parametr na metody `Update()` a `Insert()`. Můžou nastat situace, kdy chceme aktualizovat jenom jeden sloupec nebo dva, nebo chcete, aby se přizpůsobená `Insert()` metoda, která bude možná vracet hodnotu pole `IDENTITY` (automatické zvýšení) vloženého záznamu.

Chcete-li vytvořit takovou vlastní metodu, vraťte se do návrháře DataSet. Klikněte pravým tlačítkem na TableAdapter a vyberte Přidat dotaz a vraťte se do Průvodce TableAdapter. Na druhé obrazovce můžeme určit typ dotazu, který se má vytvořit. Pojďme vytvořit metodu, která přidá nový produkt a potom vrátí hodnotu nově přidaného `ProductID`záznamu. Proto se můžete rozhodnout vytvořit dotaz `INSERT`.

[![vytvořit metodu pro přidání nového řádku do tabulky Products](creating-a-data-access-layer-vb/_static/image68.png)](creating-a-data-access-layer-vb/_static/image67.png)

**Obrázek 25**: vytvoření metody pro přidání nového řádku do tabulky `Products` ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-vb/_static/image69.png))

Na další obrazovce se zobrazí `CommandText` `InsertCommand`. Rozšířit tento dotaz přidáním `SELECT SCOPE_IDENTITY()` na konci dotazu, který vrátí poslední hodnotu identity vloženou do sloupce `IDENTITY` ve stejném oboru. (Další informace o `SCOPE_IDENTITY()` a o tom, proč pravděpodobně budete chtít [místo @@IDENTITYpoužít obor\_identity () ](http://weblogs.sqlteam.com/travisl/archive/2003/10/29/405.aspx), najdete v [technické dokumentaci](https://msdn.microsoft.com/library/ms190315.aspx) .) Před přidáním příkazu `SELECT` se ujistěte, že jste ukončili příkaz `INSERT` středníkem.

[![rozšířit dotaz tak, aby vracel hodnotu SCOPE_IDENTITY ()](creating-a-data-access-layer-vb/_static/image71.png)](creating-a-data-access-layer-vb/_static/image70.png)

**Obrázek 26**: rozšíření dotazu pro návrat hodnoty `SCOPE_IDENTITY()` ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-vb/_static/image72.png))

Nakonec pojmenujte novou metodu `InsertProduct`.

[![nastavte nový název metody na InsertProduct](creating-a-data-access-layer-vb/_static/image74.png)](creating-a-data-access-layer-vb/_static/image73.png)

**Obrázek 27**: Nastavte nový název metody na `InsertProduct` ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-vb/_static/image75.png)).

Když se vrátíte do návrháře DataSet, uvidíte, že `ProductsTableAdapter` obsahuje novou metodu `InsertProduct`. Pokud tato nová metoda nemá parametr pro každý sloupec v tabulce `Products`, je pravděpodobné, že jste zapomněli příkaz `INSERT` ukončit středníkem. Nakonfigurujte metodu `InsertProduct` a ujistěte se, že máte středníkem vymezené příkazy `INSERT` a `SELECT`.

Ve výchozím nastavení metody vložení vydávají nedotazové metody, což znamená, že vrací počet ovlivněných řádků. Chceme však, aby metoda `InsertProduct` vrátila hodnotu vrácenou dotazem, ne počet ovlivněných řádků. Chcete-li to provést, upravte vlastnost `ExecuteMode` metody `InsertProduct` na `Scalar`.

[![změnit vlastnost ExecuteMode na skalární](creating-a-data-access-layer-vb/_static/image77.png)](creating-a-data-access-layer-vb/_static/image76.png)

**Obrázek 28**: změňte vlastnost `ExecuteMode` na `Scalar` ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-vb/_static/image78.png)

Následující kód ukazuje tuto novou `InsertProduct` metodu v akci:

[!code-vb[Main](creating-a-data-access-layer-vb/samples/sample8.vb)]

## <a name="step-5-completing-the-data-access-layer"></a>Krok 5: dokončení vrstvy přístupu k datům

Všimněte si, že třída `ProductsTableAdapters` vrací `CategoryID` a `SupplierID` hodnoty z tabulky `Products`, ale nezahrnuje sloupec `CategoryName` z tabulky `Categories` nebo `CompanyName` sloupce z tabulky `Suppliers`, i když jsou nejspíš sloupce, které se mají zobrazit při zobrazení informací o produktu. TableAdapter je možné rozšířit počáteční metodu, `GetProducts()`, aby zahrnovala hodnoty `CompanyName` sloupců `CategoryName` a, které budou aktualizovat objekt DataTable silně typovaného typu tak, aby zahrnoval tyto nové sloupce také.

To může představovat nějaký problém, ale TableAdapter metody pro vkládání, aktualizaci a odstraňování dat vycházejí z této prvotní metody. Automaticky generované metody pro vkládání, aktualizaci a odstraňování nejsou ovlivněny poddotazy v klauzuli `SELECT`. Pokud se rozhodnete přidat naše dotazy do `Categories` a `Suppliers` jako poddotazy namísto `JOIN` s, nemusíme tyto metody pro úpravu dat znovu dopracovat. Klikněte pravým tlačítkem na metodu `GetProducts()` v `ProductsTableAdapter` a vyberte Konfigurovat. Pak upravte klauzuli `SELECT` tak, aby vypadala takto:

[!code-sql[Main](creating-a-data-access-layer-vb/samples/sample9.sql)]

[![aktualizace příkazu SELECT pro metodu GetProducts ()](creating-a-data-access-layer-vb/_static/image80.png)](creating-a-data-access-layer-vb/_static/image79.png)

**Obrázek 29**: aktualizace příkazu `SELECT` pro metodu `GetProducts()` ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-vb/_static/image81.png))

Po aktualizaci metody `GetProducts()` pro použití tohoto nového dotazu bude objekt DataTable obsahovat dva nové sloupce: `CategoryName` a `SupplierName`.

![Objekt DataTable obsahuje dva nové sloupce.](creating-a-data-access-layer-vb/_static/image82.png)

**Obrázek 30**: `Products` DataTable obsahuje dva nové sloupce

Věnujte prosím chvilku aktualizaci klauzule `SELECT` v metodě `GetProductsByCategoryID(categoryID)` taky.

Pokud aktualizujete `GetProducts()` `SELECT` pomocí syntaxe `JOIN`, Návrhář DataSet nebude moci automaticky generovat metody pro vkládání, aktualizaci a odstraňování dat databáze pomocí modelu přímé databáze. Místo toho je budete muset ručně vytvořit stejně jako u metody `InsertProduct` dříve v tomto kurzu. V případě, že chcete použít vzor pro aktualizaci dávkových aktualizací, budete muset ručně zadat hodnoty vlastností `InsertCommand`, `UpdateCommand`a `DeleteCommand`.

## <a name="adding-the-remaining-tableadapters"></a>Přidání zbývajících objekty TableAdapter

Až do té doby jsme si prohlíželi práci s jedním TableAdapter pro jednu databázovou tabulku. Databáze Northwind ale obsahuje několik souvisejících tabulek, se kterými budeme v naší webové aplikaci pracovat. Typová datová sada může obsahovat více souvisejících datových tabulek. Proto je potřeba přidat do těchto kurzů DataTables pro další tabulky, které budeme používat. Chcete-li přidat novou TableAdapter do typové datové sady, otevřete návrháře DataSet, klikněte pravým tlačítkem myši v návrháři a vyberte možnost Přidat/TableAdapter. Tím se vytvoří nový objekt DataTable a TableAdapter a provede vás průvodcem, který jsme prozkoumali dříve v tomto kurzu.

Vytvoření následujících objekty TableAdapter a metod pomocí následujících dotazů vám může trvat několik minut. Všimněte si, že dotazy v `ProductsTableAdapter` zahrnují poddotazy pro převzetí názvů kategorií a dodavatelů jednotlivých produktů. Kromě toho, pokud jste spolu popracovali společně, již jste přidali metody `GetProducts()` a `GetProductsByCategoryID(categoryID)` třídy `ProductsTableAdapter`.

- **ProductsTableAdapter**

  - **GetProducts**: 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample10.sql)]
  - **GetProductsByCategoryID**: 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample11.sql)]
  - **GetProductsBySupplierID**: 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample12.sql)]
  - **GetProductByProductID**: 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample13.sql)]
- **CategoriesTableAdapter**

  - **GetCategories**: 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample14.sql)]
  - **GetCategoryByCategoryID**: 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample15.sql)]
- **SuppliersTableAdapter**

  - **Getdodavatelé**: 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample16.sql)]
  - **GetSuppliersByCountry**: 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample17.sql)]
  - **GetSupplierBySupplierID**: 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample18.sql)]
- **EmployeesTableAdapter**

  - **Getzaměstnanci**: 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample19.sql)]
  - **GetEmployeesByManager**: 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample20.sql)]
  - **GetEmployeeByEmployeeID**: 

      [!code-sql[Main](creating-a-data-access-layer-vb/samples/sample21.sql)]

[![návrháře DataSet po přidání čtyř objekty TableAdapter](creating-a-data-access-layer-vb/_static/image84.png)](creating-a-data-access-layer-vb/_static/image83.png)

**Obrázek 31**: Návrhář datových sad po přidání čtyř objekty TableAdapter ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-vb/_static/image85.png))

## <a name="adding-custom-code-to-the-dal"></a>Přidání vlastního kódu do DAL

Objekty TableAdapter a DataTable přidané do typované datové sady jsou vyjádřeny jako definiční soubor schématu XML (`Northwind.xsd`). Informace o tomto schématu můžete zobrazit tak, že kliknete pravým tlačítkem na soubor `Northwind.xsd` v Průzkumník řešení a zvolíte zobrazit kód.

[![soubor XSD (XML Schema Definition) pro typovou datovou sadu Northwind](creating-a-data-access-layer-vb/_static/image87.png)](creating-a-data-access-layer-vb/_static/image86.png)

**Obrázek 32**: soubor XSD (XML Schema Definition) pro datovou sadu Northwinds ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-vb/_static/image88.png))

Tyto informace o schématu jsou přeloženy do C# nebo Visual Basic kódu v době návrhu při kompilaci nebo v době běhu (v případě potřeby), kde je lze procházet pomocí ladicího programu. Chcete-li zobrazit tento automaticky generovaný kód, přejděte na Zobrazení tříd a přejděte k podrobnostem o třídách DataSet typu TableAdapter nebo. Pokud se Zobrazení tříd na obrazovce nezobrazuje, přejděte do nabídky zobrazení a vyberte ji tam nebo stiskněte kombinaci kláves CTRL + SHIFT + C. Z Zobrazení tříd můžete zobrazit vlastnosti, metody a události typové datové sady a třídy TableAdapter. Chcete-li zobrazit kód pro určitou metodu, poklikejte na název metody v Zobrazení tříd, klikněte na něj pravým tlačítkem myši a vyberte možnost přejít k definici.

![Zkontrolujte automaticky generovaný kód výběrem možnosti přejít k definici z Zobrazení tříd](creating-a-data-access-layer-vb/_static/image89.png)

**Obrázek 33**: Zkontrolujte automaticky generovaný kód výběrem možnosti přejít k definici z zobrazení tříd

I když se automaticky generovaný kód může jednat o skvělý čas, kód je často velmi obecný a musí být přizpůsoben, aby splňoval jedinečné potřeby aplikace. Riziko rozšíření automaticky generovaného kódu je ale tím, že nástroj, který kód vygeneroval, může rozhodnout, že je čas na "znovu vygenerovat" a přepsat vlastní nastavení. Pomocí nového konceptu částečné třídy .NET 2.0 je snadné rozdělit třídu napříč více soubory. Díky tomu můžeme přidat vlastní metody, vlastnosti a události do automaticky generovaných tříd, aniž byste si museli dělat starosti se zapisováním vlastních úprav do sady Visual Studio.

Abychom ukázali, jak přizpůsobit DAL, přidáme do `SuppliersRow` třídy metodu `GetProducts()`. Třída `SuppliersRow` představuje jeden záznam v tabulce `Suppliers`; každý dodavatel může u mnoha produktů získat nulu, takže `GetProducts()` vrátí tyto produkty zadaného dodavatele. K tomuto účelu vytvořte nový soubor třídy ve složce `App_Code` s názvem `SuppliersRow.vb` a přidejte následující kód:

[!code-vb[Main](creating-a-data-access-layer-vb/samples/sample22.vb)]

Tato částečná třída instruuje kompilátor, který při vytváření `Northwind.SuppliersRow` třídy obsahuje metodu `GetProducts()`, kterou jsme právě definovali. Pokud projekt sestavíte a pak se vrátíte k Zobrazení tříd uvidíte, že `GetProducts()` nyní uvedena jako metoda `Northwind.SuppliersRow`.

![Metoda GetProducts () je teď součástí třídy Northwind. SuppliersRow.](creating-a-data-access-layer-vb/_static/image90.png)

**Obrázek 34**: metoda `GetProducts()` je teď součástí třídy `Northwind.SuppliersRow`

Metodu `GetProducts()` lze nyní použít k zobrazení výčtu sady produktů pro konkrétního dodavatele, jak ukazuje následující kód:

[!code-vb[Main](creating-a-data-access-layer-vb/samples/sample23.vb)]

Tato data je možné zobrazit také v jakémkoli z ASP. Webové ovládací prvky pro data netto. Následující stránka používá ovládací prvek GridView se dvěma poli:

- Vlastnost BoundField, který zobrazuje jméno každého dodavatele a
- TemplateField, který obsahuje ovládací prvek BulletedList, který je svázán s výsledky vrácenými metodou `GetProducts()` pro každého dodavatele.

Podíváme se, jak tyto sestavy hlavní-podrobnosti zobrazit v budoucích kurzech. Nyní je tento příklad navržen pro ilustraci pomocí vlastní metody přidané do třídy `Northwind.SuppliersRow`.

SuppliersAndProducts. aspx

[!code-aspx[Main](creating-a-data-access-layer-vb/samples/sample24.aspx)]

SuppliersAndProducts. aspx. vb

[!code-vb[Main](creating-a-data-access-layer-vb/samples/sample25.vb)]

[![název společnosti dodavatele je uveden v levém sloupci a jejich produkty napravo.](creating-a-data-access-layer-vb/_static/image92.png)](creating-a-data-access-layer-vb/_static/image91.png)

**Obrázek 35**: název společnosti dodavatele je uveden v levém sloupci a jejich produkty napravo ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-vb/_static/image93.png)

## <a name="summary"></a>Přehled

Při sestavování webové aplikace, která vytvořila DAL, by měl být jedním z vašich prvních kroků, ke kterým došlo před tím, než začnete vytvářet prezentační vrstvu. V sadě Visual Studio je vytvořením DAL na základě typových datových sad úkol, který je možné provést během 10-15 minut, aniž byste museli psát řádek kódu. Kurzy, které se přesunou dál, se na tomto DAL vytvoří. V [dalším kurzu](creating-a-business-logic-layer-vb.md) definujeme několik obchodních pravidel a zjistíte, jak je implementovat do samostatné vrstvy obchodní logiky.

Šťastné programování!

## <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Vytvoření DAL pomocí objekty TableAdapter silného typu a DataTables v sadě VS 2005 a ASP.NET 2,0](https://weblogs.asp.net/scottgu/435498)
- [Návrh komponent datových vrstev a předávání dat přes úrovně](https://msdn.microsoft.com/library/ms978496.aspx)
- [Vytvoření vrstvy přístupu k datům pomocí návrháře DataSet sady Visual Studio 2005](http://www.theserverside.net/articles/showarticle.tss?id=DataSetDesigner)
- [Šifrování informací o konfiguraci v aplikacích ASP.NET 2,0](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx)
- [TableAdapter – přehled](https://msdn.microsoft.com/library/bz9tthwx.aspx)
- [Práce s typovou datovou sadou](https://msdn.microsoft.com/library/esbykkzb.aspx)
- [Používání přístupu k datům se silným typem v systému Visual Studio 2005 a ASP.NET 2,0](http://aspnet.4guysfromrolla.com/articles/020806-1.aspx)
- [Postup rozšiřování metod TableAdapter](https://blogs.msdn.com/vbteam/archive/2005/05/04/ExtendingTableAdapters.aspx)
- [Načítání skalárních dat z uložené procedury](http://aspnet.4guysfromrolla.com/articles/062905-1.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>Výukové video o tématech obsažených v tomto kurzu

- [Vrstvy přístupu k datům v aplikacích ASP.NET](../../../videos/data-access/adonet-data-services/data-access-layers-in-aspnet-applications.md)
- [Ruční svázání datové sady s objektem DataGrid](../../../videos/data-access/adonet-data-services/how-to-manually-bind-a-dataset-to-a-datagrid.md)
- [Jak pracovat s datovými sadami a filtry z aplikace ASP](../../../videos/data-access/adonet-data-services/how-to-work-with-datasets-and-filters-from-an-asp-application.md)

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Ron zelenou, Hilton Giesenow, Dennis Patterson, Liz Shulok, Abel Gomez a Carlos Santos. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](master-pages-and-site-navigation-cs.md)
> [Další](creating-a-business-logic-layer-vb.md)

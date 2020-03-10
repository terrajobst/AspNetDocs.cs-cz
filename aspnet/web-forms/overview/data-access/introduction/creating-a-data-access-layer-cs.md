---
uid: web-forms/overview/data-access/introduction/creating-a-data-access-layer-cs
title: Vytvoření vrstvy přístupu k datům (C#) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu začneme od začátku a vytvoříme vrstvy přístupu k datům (DAL) pomocí zadaných datových sad pro přístup k informacím v databázi.
ms.author: riande
ms.date: 04/05/2010
ms.assetid: cfe2a6a0-1e56-4dc8-9537-c8ec76ba96a4
msc.legacyurl: /web-forms/overview/data-access/introduction/creating-a-data-access-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: 5aaf97dc8448dcb7b94ef2e4e23f34fd37ac4426
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78605040"
---
# <a name="creating-a-data-access-layer-c"></a>Vytvoření vrstvy přístupu k datům (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout PDF](creating-a-data-access-layer-cs/_static/datatutorial01cs1.pdf)

> V tomto kurzu začneme od začátku a vytvoříme vrstvy přístupu k datům (DAL) pomocí zadaných datových sad pro přístup k informacím v databázi.

## <a name="introduction"></a>Úvod

Jako vývojáři webu se naše pracoviště roztéká na práci s daty. Vytvoříme databáze pro ukládání dat, kód, který se má načíst a upravit, a webové stránky pro shromáždění a shrnutí. Toto je první kurz v řadě dlouhé řady, který bude prozkoumat techniky pro implementaci těchto běžných vzorů v ASP.NET 2,0. Začneme vytvořením [softwarové architektury](http://en.wikipedia.org/wiki/Software_architecture) složené z vrstvy přístupu k datům (dal) pomocí typových datových sad, vrstvy obchodní logiky (knihoven BLL), která vynutila vlastní obchodní pravidla, a prezentační vrstvu složenou ze stránek ASP.NET, které sdílejí společné rozložení stránky. Po navýšení back-endu základy se přesunete do vytváření sestav a ukážeme, jak zobrazit, shrnout, shromáždit a ověřit data z webové aplikace. Tyto kurzy jsou stručné a poskytují podrobné pokyny s mnoha snímky obrazovky, které vás provedou procesem vizuálně. Každý kurz je k dispozici v C# a Visual Basic verzích a zahrnuje stažení kompletního používaného kódu. (Tento první kurz je poměrně dlouhý, ale zbytek se prezentuje mnohem více digestible bloků dat.)

V těchto kurzech budeme používat verzi databáze Northwind verze Microsoft SQL Server 2005 Express, která je umístěna v adresáři **\_dat aplikace** . Kromě databázového souboru **aplikace\_data** také obsahuje skripty SQL pro vytvoření databáze pro případ, že chcete použít jinou verzi databáze. Tyto skripty je možné stáhnout také [přímo od Microsoftu](https://www.microsoft.com/downloads/details.aspx?FamilyID=06616212-0356-46a0-8da2-eebc53a68034&amp;DisplayLang=en), pokud chcete. Pokud používáte jinou SQL Server verzi databáze Northwind, budete muset aktualizovat nastavení **NORTHWNDConnectionString** v souboru **Web. config** aplikace. Webová aplikace byla sestavena pomocí sady Visual Studio 2005 Professional Edition jako projekt webu založeného na systému souborů. Nicméně všechny kurzy budou fungovat stejně dobře i v bezplatné verzi sady Visual Studio 2005, [Visual Web Developer](https://msdn.microsoft.com/vstudio/express/vwd/).  
  
V tomto kurzu začneme od začátku a vytvoříme vrstvy přístupu k datům (DAL) následovaný vytvořením vrstvy obchodní logiky (knihoven BLL) v druhém kurzu a při práci na rozložení stránky a navigaci ve třetí části. Kurzy po třetí straně budou sestaveny na základech, které jsou uvedeny v prvních třech. V tomto prvním kurzu máme spoustu pokrytí, takže můžete spustit Visual Studio a můžeme začít!

## <a name="step-1-creating-a-web-project-and-connecting-to-the-database"></a>Krok 1: Vytvoření webového projektu a připojení k databázi

Než můžeme vytvořit naši vrstvu přístupu k datům (DAL), musíme nejdřív vytvořit web a nastavit naši databázi. Začněte vytvořením nového webu ASP.NET založeného na systému souborů. To lze provést tak, že přejdete do nabídky soubor a zvolíte možnost Nový web a zobrazí se dialogové okno Nový web. Vyberte šablonu webu ASP.NET, nastavte rozevírací seznam umístění na systém souborů, vyberte složku, kam chcete umístit web, a nastavte jazyk na C#.

[![vytvoření nového webu založeného na systému souborů](creating-a-data-access-layer-cs/_static/image2.png)](creating-a-data-access-layer-cs/_static/image1.png)

**Obrázek 1**: vytvoření nového webu založeného na systému souborů ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-cs/_static/image3.png))

Tím se vytvoří nový web s výchozí stránkou **. aspx** ASP.NET a **datovou složkou aplikace\_** .

Při vytvoření webu je dalším krokem přidání odkazu na databázi v Průzkumník serveru sady Visual Studio. Přidáním databáze do Průzkumník serveru můžete do sady Visual Studio přidat tabulky, uložené procedury, zobrazení a tak dále. Můžete také zobrazit data tabulky nebo vytvořit vlastní dotazy buď ručně, nebo graficky prostřednictvím Tvůrce dotazů. Kromě toho, když sestavíme typové datové sady pro DAL, bude nutné, aby sada Visual Studio odkazovala na databázi, ze které by měly být vytvořeny typové datové sady. I když můžeme poskytnout tyto informace o připojení v tomto okamžiku, Visual Studio automaticky naplní rozevírací seznam databází již registrovaných v Průzkumník serveru.

Postup přidání databáze Northwind do Průzkumník serveru závisí na tom, jestli chcete použít databázi SQL Server 2005 Express Edition ve složce **\_dat aplikace** , nebo pokud máte instalační program databázového serveru Microsoft SQL Server 2000 nebo 2005, který chcete použít místo toho.

## <a name="using-a-database-in-the-app_data-folder"></a>Použití databáze ve složce\_dat aplikace

Pokud nemáte databázový server SQL Server 2000 nebo 2005, ke kterému se chcete připojit, nebo chcete, aby se databáze nemusela přidávat do databázového serveru, můžete použít SQL Server 2005 Express Edition verzi databáze Northwind, která je umístěná ve složce dat staženého webu **\_aplikace** (**northwnd). MDF**).

Do Průzkumník serveru se automaticky přidá databáze umístěná ve složce **App\_data** . Za předpokladu, že máte na svém počítači nainstalovanou SQL Server 2005 Express Edition, měli byste vidět uzel s názvem NORTHWND. MDF v Průzkumník serveru, který můžete rozbalit a prozkoumat jeho tabulky, zobrazení, uloženou proceduru atd. (viz obrázek 2).

Složka **App\_data** může obsahovat také soubory aplikace Microsoft Access **. mdb** , které se stejně jako jejich SQL Server protějšky automaticky přidávají do Průzkumník serveru. Pokud nechcete používat žádnou z možností SQL Server, můžete vždy [Stáhnout verzi Microsoft Access souboru databáze Northwind](https://www.microsoft.com/downloads/details.aspx?FamilyID=C6661372-8DBE-422B-8676-C632D66C529C&amp;displaylang=EN) a umístit ji do **datového adresáře aplikace\_** . Mějte ale na paměti, že přístup k databázím není jako SQL Server bez funkcí a není navržený tak, aby se používal ve scénářích webů. Kromě toho několik dalších 35 kurzů bude využívat některé funkce na úrovni databáze, které nejsou podporovány aplikací Access.

## <a name="connecting-to-the-database-in-a-microsoft-sql-server-2000-or-2005-database-server"></a>Připojení k databázi na databázovém serveru s Microsoft SQL Server 2000 nebo 2005

Případně se můžete připojit k databázi Northwind nainstalované na databázovém serveru. Pokud na databázovém serveru ještě není nainstalovaná databáze Northwind, musíte ji nejdřív přidat do databázového serveru spuštěním instalačního skriptu, který je součástí stažení tohoto kurzu, nebo [stažením verze SQL Server 2000 rozhraní Northwind a instalačního skriptu](https://www.microsoft.com/downloads/details.aspx?FamilyID=06616212-0356-46a0-8da2-eebc53a68034&amp;DisplayLang=en) přímo z webu společnosti Microsoft.

Po instalaci databáze přejděte na Průzkumník serveru v aplikaci Visual Studio, klikněte pravým tlačítkem na uzel datová připojení a vyberte Přidat připojení. Pokud se Průzkumník serveru nezobrazuje, přejděte do zobrazení/Průzkumník serveru nebo stiskněte kombinaci kláves CTRL + ALT + S. Tím se zobrazí dialogové okno Přidat připojení, kde můžete zadat server, ke kterému se chcete připojit, informace o ověřování a název databáze. Po úspěšné konfiguraci informací o připojení databáze a kliknutí na tlačítko OK bude databáze přidána jako uzel pod uzlem datová připojení. Uzel databáze můžete rozšířit a prozkoumat jeho tabulky, zobrazení, uložené procedury atd.

![Přidání připojení k databázi Northwind vašeho databázového serveru](creating-a-data-access-layer-cs/_static/image4.png)

**Obrázek 2**: Přidání připojení k databázi Northwind vašeho databázového serveru

## <a name="step-2-creating-the-data-access-layer"></a>Krok 2: vytvoření vrstvy přístupu k datům

Při práci s daty jedna z možností je vložení logiky specifické pro data přímo do prezentační vrstvy (ve webové aplikaci se ASP.NET stránky tvoří prezentační vrstvu). To může mít formu psaní kódu ADO.NET v části kódu stránky ASP.NET nebo použití ovládacího prvku SqlDataSource z části s označením. V obou případech tento přístup těsně Couples logiku přístupu k datům pomocí prezentační vrstvy. Doporučený postup je ale oddělit logiku přístupu k datům z prezentační vrstvy. Tato samostatná vrstva je označována jako vrstva přístupu k datům, je dál pro krátké a je obvykle implementována jako samostatný projekt knihovny tříd. Výhody této vrstvené architektury jsou dobře zdokumentováné (Další informace najdete v části "Další informace" na konci tohoto kurzu) a jedná se o přístup, který v této sérii provedeme.

Veškerý kód, který je specifický pro základní zdroj dat, jako je například vytvoření připojení k databázi, příkazy pro **Výběr**, **vložení**, **aktualizaci**a **odstranění** , by měl být umístěn v rámci dal. Prezentační vrstva nesmí obsahovat odkazy na takový kód pro přístup k datům, ale místo toho by se mělo volat na DAL pro všechny a všechny požadavky na data. Vrstvy přístupu k datům typicky obsahují metody pro přístup k podkladovým datům databáze. Databáze Northwind obsahuje například tabulky **Products** a **Categories** , které zaznamenávají produkty k prodeji a kategorie, do kterých patří. V naší DAL metody, jako jsou:

- **GetCategories (),** který vrátí informace o všech kategoriích
- **GetProducts ()** , ve kterém budou vráceny informace o všech produktech
- **GetProductsByCategoryID (*KódKategorie*)** , který vrátí všechny produkty patřící do zadané kategorie
- **GetProductByProductID (*ProductID*)** , který vrátí informace o konkrétním produktu

Tyto metody, pokud jsou vyvolány, se připojí k databázi, vydávají příslušný dotaz a vrátí výsledky. Způsob, jakým vracíme tyto výsledky, je důležitý. Tyto metody mohou jednoduše vracet datovou sadu nebo objekt DataReader vyplněný databázovým dotazem, ale v ideálním případě by měly být vráceny pomocí *objektů silně typovaného*typu. Silně typované objekty je jeden, jehož schéma je pevně definováno v době kompilace, zatímco opačný objekt s volným typem je jeden, jehož schéma není známo až do doby běhu.

Například objekt DataReader a datová sada (ve výchozím nastavení) jsou objekty volně typované, protože jejich schéma je definováno sloupci vrácenými databázovým dotazem použitým k naplnění. Pro přístup ke konkrétnímu sloupci z volně typovaného objektu DataTable potřebujeme použít syntaxi jako:  <strong><em>DataTable</em>. Řádky [<em>index</em>] ["<em>ColumnName</em>"]</strong>. V tomto příkladu se v tomto příkladu projeví volné zadání, které potřebujeme pro přístup k názvu sloupce pomocí řetězce nebo pořadového indexu. Silně typované DataTable, na druhé straně, budou mít všechny jeho sloupce implementované jako vlastnosti, což vede k psaní kódu, který vypadá takto:  <strong><em>DataTable</em>. Řádky [<em>index</em>]. *ColumnName</strong>* .

Chcete-li vracet objekty silného typu, mohou vývojáři vytvořit své vlastní obchodní objekty nebo použít typové datové sady. Obchodní objekt je implementován vývojářem jako třída, jejíž vlastnosti typicky odrážejí sloupce podkladové databázové tabulky, kterou obchodní objekt představuje. Typová datová sada je třída vygenerovaná pro vás sadou Visual Studio na základě schématu databáze a jejíž členové jsou silně typované podle tohoto schématu. Zadaná datová sada obsahuje třídy, které přesahují třídy ADO.NET DataSet, DataTable a DataRow. Kromě typů DataTables se silnými typy teď typované datové sady teď zahrnují také objekty TableAdapter, což jsou třídy s metodami pro naplnění DataTables datové sady a rozšiřování úprav v rámci datových tabulek zpátky do databáze.

> [!NOTE]
> Další informace o výhodách a nevýhodách používání typových datových sad a vlastních obchodních objektů najdete v tématu [navrhování komponent datové vrstvy a předávání dat přes úrovně](https://msdn.microsoft.com/library/ms978496.aspx).

Pro tuto architekturu kurzů použijeme datové sady silného typu. Obrázek 3 znázorňuje pracovní postup mezi různými vrstvami aplikace, které používají typové datové sady.

[![veškerého kódu přístupu k datům je Relegated na DAL.](creating-a-data-access-layer-cs/_static/image6.png)](creating-a-data-access-layer-cs/_static/image5.png)

**Obrázek 3**: veškerý kód pro přístup k datům je RELEGATED na dal ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-cs/_static/image7.png)

## <a name="creating-a-typed-dataset-and-table-adapter"></a>Vytvoření typové datové sady a adaptéru tabulky

Pokud chcete začít vytvářet DAL, začněte tím, že do projektu přidáte typovou datovou sadu. Chcete-li to provést, klikněte pravým tlačítkem myši na uzel projektu v Průzkumník řešení a vyberte možnost Přidat novou položku. V seznamu šablon vyberte možnost datová sada a pojmenujte ji **Northwind. xsd**.

[![se rozhodnout přidat novou datovou sadu do projektu](creating-a-data-access-layer-cs/_static/image9.png)](creating-a-data-access-layer-cs/_static/image8.png)

**Obrázek 4**: vyberte, chcete-li do projektu přidat novou datovou sadu ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-cs/_static/image10.png)).

Po kliknutí na Přidat se po zobrazení výzvy k přidání datové sady do složky **\_ho kódu aplikace** vyberte Ano. Zobrazí se Návrhář pro typovou datovou sadu a spustí se Průvodce konfigurací TableAdapter, který vám umožní přidat svůj první TableAdapter do typované datové sady.

Typová datová sada slouží jako silně typované kolekce dat; skládá se ze silně typované instance DataTable, z nichž každá je tvořena instancemi DataRow se silnými typy. Vytvoříme silně typované datové tabulky pro každou z podkladových databázových tabulek, se kterými potřebujeme pracovat v této sérii kurzů. Začněte vytvořením DataTable pro tabulku **Products** .

Pamatujte, že datatabulka se silným typem neobsahuje žádné informace o tom, jak přistupovat k datům z jejich podkladové databázové tabulky. Aby bylo možné načíst data k naplnění objektu DataTable, používáme třídu TableAdapter, která funguje jako naše vrstva přístupu k datům. Pro naše **objekty DataTable bude** TableAdapter obsahovat metody **GetProducts ()** , **GetProductByCategoryID (*CategoryID*)** , a tak dále, kterou vyvoláme z prezentační vrstvy. Role DataTable slouží jako objekty silného typu, které slouží k předávání dat mezi vrstvami.

Průvodce konfigurací TableAdapter začíná výzvou k výběru databáze, se kterou chcete pracovat. Rozevírací seznam zobrazuje tyto databáze v Průzkumník serveru. Pokud jste databázi Northwind nepřidali do Průzkumník serveru, můžete v tuto chvíli kliknout na tlačítko nové připojení.

[![zvolit databázi Northwind z rozevíracího seznamu](creating-a-data-access-layer-cs/_static/image12.png)](creating-a-data-access-layer-cs/_static/image11.png)

**Obrázek 5**: v rozevíracím seznamu vyberte databázi Northwind ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-cs/_static/image13.png)).

Po výběru databáze a kliknutí na tlačítko Další se zobrazí dotaz, zda chcete uložit připojovací řetězec do souboru **Web. config** . Uložením připojovacího řetězce se vyhnete tomu, aby byl pevně kódovaný v třídách TableAdapter, což zjednodušuje věci, pokud se v budoucnu změní informace připojovacího řetězce. Pokud se přihlásíte k uložení připojovacího řetězce v konfiguračním souboru, je umístěn v části **&lt;connectionstrings&gt;** , která může být [volitelně šifrována](http://aspnet.4guysfromrolla.com/articles/021506-1.aspx) pro zlepšení zabezpečení nebo později upravena prostřednictvím nové stránky vlastností ASP.NET 2,0 v nástroji pro správu grafického uživatelského rozhraní služby IIS, což je pro správce důležitější.

[![Uložit připojovací řetězec do souboru Web. config](creating-a-data-access-layer-cs/_static/image15.png)](creating-a-data-access-layer-cs/_static/image14.png)

**Obrázek 6**: uložení připojovacího řetězce do souboru **Web. config** ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-cs/_static/image16.png))

Dále je potřeba definovat schéma pro první typ DataTable se silnými typy a zadat první metodu pro naše TableAdapter, která se má použít při naplňování silně typované datové sady. Tyto dva kroky jsou provedeny současně vytvořením dotazu, který vrací sloupce z tabulky, kterou chcete reflektovat v našem objektu DataTable. Na konci Průvodce poskytneme tomuto dotazu název metody. Po dokončení této metody lze tuto metodu vyvolat z naší prezentační vrstvy. Metoda spustí definovaný dotaz a naplní objekt DataTable silného typu.

Abyste mohli začít definovat dotaz SQL, musíte nejdřív určit, jak chceme, aby TableAdapter dotaz vydával. Můžeme použít příkaz SQL ad hoc, vytvořit novou uloženou proceduru nebo použít existující uloženou proceduru. V těchto kurzech budeme používat příkazy SQL ad hoc. Příklad použití uložených procedur najdete v článku [Brian Noyes](http://briannoyes.net/), [sestavení vrstvy přístupu k datům pomocí návrháře DataSet sady Visual Studio 2005](http://www.theserverside.net/articles/showarticle.tss?id=DataSetDesigner) .

[![dotazování na data pomocí příkazu SQL ad hoc](creating-a-data-access-layer-cs/_static/image18.png)](creating-a-data-access-layer-cs/_static/image17.png)

**Obrázek 7**: dotazování na data pomocí příkazu SQL ad hoc ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-cs/_static/image19.png))

V tuto chvíli můžeme zadat dotaz SQL ručně. Při vytváření první metody v TableAdapter, která obvykle chcete, aby dotaz vrátil tyto sloupce, které je nutné vyjádřit v odpovídajícím objektu DataTable. To lze provést vytvořením dotazu, který vrátí všechny sloupce a všechny řádky z tabulky **Products** :

[![zadejte dotaz SQL do textového pole.](creating-a-data-access-layer-cs/_static/image21.png)](creating-a-data-access-layer-cs/_static/image20.png)

**Obrázek 8**: zadejte dotaz SQL do textového pole ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-cs/_static/image22.png)).

Případně můžete použít Tvůrce dotazů a graficky sestavit dotaz, jak je znázorněno na obrázku 9.

[![vytvořit dotaz graficky pomocí Editoru dotazů](creating-a-data-access-layer-cs/_static/image24.png)](creating-a-data-access-layer-cs/_static/image23.png)

**Obrázek 9**: vytvoření dotazu graficky pomocí Editoru dotazů ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-cs/_static/image25.png))

Po vytvoření dotazu, ale před přechodem na další obrazovku, klikněte na tlačítko Upřesnit možnosti. V projektech webů je jako jediná možnost pokročilé vybraná jako výchozí vybraná možnost Generovat příkazy INSERT, Update a DELETE. Pokud spustíte tohoto průvodce z knihovny tříd nebo projektu Windows, bude vybrána také možnost použít optimistickou souběžnost. Ponechte možnost použít optimistickou souběžnost pro teď nezaškrtnutou. V budoucích kurzech prověříme optimistickou souběžnost.

[![vyberte jenom možnost Generovat příkazy INSERT, Update a DELETE.](creating-a-data-access-layer-cs/_static/image27.png)](creating-a-data-access-layer-cs/_static/image26.png)

**Obrázek 10**: vyberte jenom možnost Generovat příkazy INSERT, Update a Delete ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-cs/_static/image28.png)

Po ověření rozšířených možností kliknutím na tlačítko Další přejděte na poslední obrazovku. Tady se zobrazí výzva k výběru metod, které se mají přidat do TableAdapter. Existují dva vzory pro naplnění dat:

- **Naplnit DataTable** pomocí tohoto přístupu metoda, která je vytvořena v objektu DataTable jako parametr a naplní ji na základě výsledků dotazu. Třída ADO.NET DataAdapter například implementuje tento vzor s metodou **Fill ()** .
- **Vrátí DataTable** s tímto přístupem metoda vytvoří a vyplní objekt DataTable za vás a vrátí jej jako návratovou hodnotu metody.

Je možné, že TableAdapter implementuje jeden nebo oba tyto vzory. Zde uvedené metody lze také přejmenovat. Nechte obě zaškrtávací políčka zaškrtnutá, i když v těchto kurzech budeme používat jenom druhý vzor. Přejmenujte raději obecnou metodu **GetData** na **GetProducts**.

Pokud je zaškrtnuto, poslední zaškrtávací políčko "GenerateDBDirectMethods" vytvoří metody **Insert ()** , **Update ()** a **Delete ()** pro TableAdapter. Pokud tuto možnost nezaškrtnete, budou se všechny aktualizace muset provádět prostřednictvím metody TableAdapter **()** s jedinou aktualizací, která přebírá typovou datovou sadu, objekt DataTable, jediný objekt DataRow nebo pole datových řádků. (Pokud jste nezaškrtli možnost Generovat příkazy INSERT, Update a DELETE z rozšířených vlastností na obrázku 9, nebude toto nastavení zaškrtávacího políčka nijak ovlivněno.) Pojďme toto políčko nechat zaškrtnuté.

[![změnit název metody z GetData na GetProducts](creating-a-data-access-layer-cs/_static/image30.png)](creating-a-data-access-layer-cs/_static/image29.png)

**Obrázek 11**: Změňte název metody z **GetData** na **GetProducts** ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-cs/_static/image31.png)

Dokončete průvodce kliknutím na tlačítko Dokončit. Po ukončení průvodce se vrátí do návrháře DataSet, který zobrazuje objekt DataTable, který jsme právě vytvořili. Můžete zobrazit seznam sloupců v objektu DataTable **Products** (**ProductID**, **ProductName**atd.) a také metody **ProductsTableAdapter** (**Fill ()** a **GetProducts ()** ).

[![do typové datové sady byly přidány objekty DataTable a ProductsTableAdapter.](creating-a-data-access-layer-cs/_static/image33.png)](creating-a-data-access-layer-cs/_static/image32.png)

**Obrázek 12**: do typované datové sady byly přidány **produkty** DataTable a **ProductsTableAdapter** ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-cs/_static/image34.png)

V tuto chvíli máme typovou datovou sadu s jedním objektem DataTable (**Northwind. Products**) a třídou DataAdapter se silným typem (**NorthwindTableAdapters. ProductsTableAdapter**) s metodou **GetProducts ()** . Tyto objekty lze použít pro přístup k seznamu všech produktů z kódu, jako je:

[!code-html[Main](creating-a-data-access-layer-cs/samples/sample1.html)]

Tento kód nám nevyžadoval zápis jednoho bitu kódu specifického pro přístup k datům. Nemuseli bychom vytvářet instance žádné třídy ADO.NET, nemuseli by odkazovat na žádné připojovací řetězce, dotazy SQL nebo uložené procedury. Místo toho poskytuje TableAdapter kód pro přístup k datům na nízké úrovni pro nás.

Každý objekt použitý v tomto příkladu je také silného typu, což aplikaci Visual Studio umožňuje poskytovat technologii IntelliSense a kontrolu typu při kompilaci. A nejlepší ze všech datových tabulek vrácených TableAdapter může být svázán s datovými ovládacími prvky ASP.NET dat, jako je například GridView, DetailsView, DropDownList, CheckBoxList a několik dalších. Následující příklad znázorňuje vazbu objektu DataTable vráceného metodou **GetProducts ()** do prvku GridView v pouze scant třech řádcích kódu v rámci **stránky\_načtení** obslužné rutiny události.

AllProducts.aspx

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample2.aspx)]

AllProducts.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample3.cs)]

[![se seznam produktů zobrazuje v prvku GridView.](creating-a-data-access-layer-cs/_static/image36.png)](creating-a-data-access-layer-cs/_static/image35.png)

**Obrázek 13**: seznam produktů je zobrazen v prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-cs/_static/image37.png)).

I když tento příklad vyžaduje, abychom na stránce ASP.NET stránky na stránce **\_načítání** obslužné rutiny události napsali tři řádky kódu, v budoucích kurzech probereme, jak použít prvek ObjectDataSource k deklarativnímu načtení dat z dal. V prvku ObjectDataSource nebudeme muset psát žádný kód a Podpora stránkování a řazení bude také.

## <a name="step-3-adding-parameterized-methods-to-the-data-access-layer"></a>Krok 3: Přidání parametrizovaných metod do vrstvy přístupu k datům

V této fázi má naše třída **ProductsTableAdapter** ale jednu **metodu, která**vrátí všechny produkty v databázi. I když je možné pracovat se všemi produkty, jsou v tuto chvíli k dispozici čas, kdy budeme chtít načíst informace o konkrétním produktu nebo všech produktech, které patří do určité kategorie. Pro přidání takových funkcí do naší vrstvy přístupu k datům můžeme přidat parametrizované metody do TableAdapter.

Pojďme přidat metodu **GetProductsByCategoryID (*KódKategorie*)** . Chcete-li přidat novou metodu k DAL, vraťte se do návrháře DataSet, klikněte pravým tlačítkem myši v části **ProductsTableAdapter** a vyberte možnost Přidat dotaz.

![Klikněte pravým tlačítkem na TableAdapter a vyberte Přidat dotaz.](creating-a-data-access-layer-cs/_static/image38.png)

**Obrázek 14**: klikněte pravým tlačítkem na TableAdapter a vyberte Přidat dotaz.

Nejdřív se zobrazí dotaz, jestli chceme získat přístup k databázi pomocí příkazu ad-hoc SQL nebo nové nebo existující uložené procedury. Zkusíme znovu použít příkaz SQL ad hoc. V dalším kroku se zobrazí dotaz, jaký typ dotazu SQL chceme použít. Vzhledem k tomu, že chceme vrátit všechny produkty, které patří do určité kategorie, chceme napsat příkaz **Select** , který vrátí řádky.

[![zvolit vytvoření příkazu SELECT, který vrátí řádky](creating-a-data-access-layer-cs/_static/image40.png)](creating-a-data-access-layer-cs/_static/image39.png)

**Obrázek 15**: zvolte možnost vytvoření příkazu **Select** , který vrátí řádky ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-cs/_static/image41.png)

Dalším krokem je definování dotazu SQL, který se používá pro přístup k datům. Vzhledem k tomu, že chceme vracet pouze produkty, které patří do konkrétní kategorie, používám stejný příkaz <strong>Select</strong> z <strong>GetProducts ()</strong>, ale přidejte následující klauzuli <strong>WHERE</strong> : <strong>WHERE KódKategorie = @CategoryID</strong>. Parametr <strong>@CategoryID</strong> informuje Průvodce TableAdapter, že metoda, kterou vytváříme, bude vyžadovat vstupní parametr odpovídajícího typu (tj. celé číslo s možnou hodnotou null).

[![zadejte dotaz, který bude vracet jenom produkty v zadané kategorii.](creating-a-data-access-layer-cs/_static/image43.png)](creating-a-data-access-layer-cs/_static/image42.png)

**Obrázek 16**: zadejte dotaz, který bude vracet pouze produkty v zadané kategorii ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-cs/_static/image44.png)

V posledním kroku můžeme zvolit, které vzory přístupu k datům se mají použít, a také přizpůsobit názvy generovaných metod. Pro vzorek výplně změňte název na <strong>FillByCategoryID</strong> a pro návrat návratového vzoru DataTable (metody <strong>Get*X</strong>*  ), který používá <strong>GetProductsByCategoryID</strong>.

[![zvolit názvy pro metody TableAdapter](creating-a-data-access-layer-cs/_static/image46.png)](creating-a-data-access-layer-cs/_static/image45.png)

**Obrázek 17**: vyberte názvy pro metody TableAdapter ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-cs/_static/image47.png)).

Po dokončení průvodce obsahuje Návrhář DataSet nové metody TableAdapter.

![V produktech se teď dají dotazovat podle kategorie.](creating-a-data-access-layer-cs/_static/image48.png)

**Obrázek 18**: produkty se teď dají dotazovat podle kategorie

Věnujte prosím chvilku přidání metody **GetProductByProductID (*ProductID*)** pomocí stejné techniky.

Tyto parametrizované dotazy mohou být testovány přímo z návrháře DataSet. Klikněte pravým tlačítkem na metodu v TableAdapter a vyberte možnost Náhled dat. Potom zadejte hodnoty, které chcete použít pro parametry, a klikněte na náhled.

[Zobrazí se ![těchto produktů patřících ke kategorii nápoje.](creating-a-data-access-layer-cs/_static/image50.png)](creating-a-data-access-layer-cs/_static/image49.png)

**Obrázek 19**: zobrazí se tyto produkty patřící do kategorie nápoje ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-cs/_static/image51.png)

S metodou **GetProductsByCategoryID (*KódKategorie*)** v naší dal teď můžeme vytvořit stránku ASP.NET, která zobrazí jenom produkty v zadané kategorii. Následující příklad ukazuje všechny produkty, které jsou v kategorii nápoje, které mají **ČísloKategorie** 1.

Nápoje. ASP

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample4.aspx)]

Beverages.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample5.cs)]

[![se zobrazí tyto produkty v kategorii nápoje.](creating-a-data-access-layer-cs/_static/image53.png)](creating-a-data-access-layer-cs/_static/image52.png)

**Obrázek 20**: zobrazí se tyto produkty v kategorii nápoje ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-cs/_static/image54.png)

## <a name="step-4-inserting-updating-and-deleting-data"></a>Krok 4: vkládání, aktualizace a odstraňování dat

Existují dva vzory, které se běžně používají pro vkládání, aktualizaci a odstraňování dat. První vzor, který bude volat přímý vzor databáze, zahrnuje vytváření metod, které při vyvolání vydávají příkaz **INSERT**, **Update**nebo **Delete** , pro databázi, která pracuje na jednom záznamu databáze. Tyto metody se obvykle předávají v řadě skalárních hodnot (celá čísla, řetězce, logické hodnoty, DateTime atd.), které odpovídají hodnotám pro vložení, aktualizaci nebo odstranění. Například s tímto vzorem pro tabulku **Products** by Metoda Delete měla převzít parametr typu Integer, který označuje **ProductID** záznamu, který se má odstranit, zatímco metoda INSERT by poznamenala v řetězci pro **NázevVýrobku** **, celé**číslo pro **UnitsOnStock**, a tak dále.

[![se každou žádost o vložení, aktualizaci a odstranění pošle do databáze hned](creating-a-data-access-layer-cs/_static/image56.png)](creating-a-data-access-layer-cs/_static/image55.png)

**Obrázek 21**: každý požadavek na vložení, aktualizaci a odstranění se pošle do databáze hned ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-cs/_static/image57.png)

Druhý model, na který se odkazuje jako na vzor aktualizace služby Batch, je aktualizovat celou datovou sadu, DataTable nebo kolekci datových řádků v jednom volání metody. V tomto vzoru vývojář odstraní, vloží a upraví datové řádky v objektu DataTable a pak tyto datové řádky nebo DataTable předá metodě aktualizace. Tato metoda potom vytvoří výčet předaných dat, určí, zda byly změněny, přidány nebo odstraněny (prostřednictvím hodnoty [vlastnosti RowState](https://msdn.microsoft.com/library/system.data.datarow.rowstate.aspx) objektu DataRow), a vydá požadavek odpovídající databáze pro každý záznam.

[![všechny změny jsou synchronizovány s databází při vyvolání metody Update](creating-a-data-access-layer-cs/_static/image59.png)](creating-a-data-access-layer-cs/_static/image58.png)

**Obrázek 22**: všechny změny jsou synchronizovány s databází při vyvolání metody Update ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-cs/_static/image60.png)

TableAdapter používá ve výchozím nastavení vzor dávkové aktualizace, ale podporuje také přímý vzor databáze. Vzhledem k tomu, že jsme při vytváření našeho TableAdapter vybrali možnost Generovat příkazy INSERT, Update a DELETE z rozšířených vlastností, **ProductsTableAdapter** obsahuje metodu **Update ()** , která implementuje vzor aktualizace služby Batch. Konkrétně TableAdapter obsahuje metodu **Update ()** , která může být předána typovou datovou sadu, silně typované DataTable nebo jedním nebo více datařádků. Pokud jste ponechali zaškrtávací políčko "GenerateDBDirectMethods" zaškrtnuté při prvním vytvoření TableAdapter, bude vzor DB Direct také implementován prostřednictvím metod **Insert ()** , **Update (** ) a **Delete ()** .

Jak vzorce změny dat používají vlastnosti **InsertCommand**, **UpdateCommand**a **DeleteCommand** TableAdapter k vystavení příkazů **INSERT**, **Update**a **Delete** do databáze. Kliknutím na TableAdapter v Návrháři DataSet a následně na okno Vlastnosti můžete zkontrolovat a upravit vlastnosti **InsertCommand**, **UpdateCommand**a **DeleteCommand** . (Ujistěte se, že jste vybrali TableAdapter a že objekt **ProductsTableAdapter** je ten vybraný v rozevíracím seznamu v okno Vlastnosti.)

[![vlastnost TableAdapter má vlastnosti InsertCommand, UpdateCommand a DeleteCommand.](creating-a-data-access-layer-cs/_static/image62.png)](creating-a-data-access-layer-cs/_static/image61.png)

**Obrázek 23**: TableAdapter má vlastnosti **InsertCommand**, **UpdateCommand**a **DeleteCommand** ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-cs/_static/image63.png)).

Chcete-li prostudovat nebo změnit některou z těchto vlastností příkazu databáze, klikněte na podvlastnost **CommandText** , která zobrazí Tvůrce dotazů.

[![nakonfigurovat příkazy INSERT, UPDATE a DELETE v Tvůrce dotazů](creating-a-data-access-layer-cs/_static/image65.png)](creating-a-data-access-layer-cs/_static/image64.png)

**Obrázek 24**: Konfigurace příkazů **INSERT**, **Update**a **Delete** v Tvůrce dotazů ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-cs/_static/image66.png))

Následující příklad kódu ukazuje, jak použít vzor dávkové aktualizace k dvojnásobku ceny za všechny produkty, které nejsou ukončené a které mají 25 jednotek na skladě nebo méně:

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample6.cs)]

Následující kód ukazuje, jak pomocí vzoru DB Direct programově odstranit konkrétní produkt, jak ho aktualizovat, a pak přidat nové:

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample7.cs)]

## <a name="creating-custom-insert-update-and-delete-methods"></a>Vytváření vlastních metod vložení, aktualizace a odstranění

Metody **Insert ()** , **Update ()** a **Delete ()** vytvořené metodou DB Direct můžou být náročné na bit, hlavně pro tabulky s mnoha sloupci. V předchozím příkladu kódu, bez pomocníka IntelliSense, není obzvláště jasné, které sloupce tabulky **Products** se namapuje na každý vstupní parametr do metody **Update ()** a **Insert ()** . Můžou nastat situace, kdy chceme aktualizovat jenom jeden sloupec nebo dvě, nebo chcete, aby byla přizpůsobená metoda **Insert ()** , která bude možná vracet hodnotu pole **identity** nově vloženého záznamu (automatické zvýšení).

Chcete-li vytvořit takovou vlastní metodu, vraťte se do návrháře DataSet. Klikněte pravým tlačítkem na TableAdapter a vyberte Přidat dotaz a vraťte se do Průvodce TableAdapter. Na druhé obrazovce můžeme určit typ dotazu, který se má vytvořit. Pojďme vytvořit metodu, která přidá nový produkt a potom vrátí hodnotu nově přidaného záznamu **ProductID**. Proto se můžete rozhodnout vytvořit dotaz pro **vložení** .

[![vytvořit metodu pro přidání nového řádku do tabulky Products](creating-a-data-access-layer-cs/_static/image68.png)](creating-a-data-access-layer-cs/_static/image67.png)

**Obrázek 25**: vytvoření metody pro přidání nového řádku do tabulky **Products** ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-cs/_static/image69.png))

Na další obrazovce se zobrazí vlastnost **CommandText** pro **InsertCommand**. Rozšířit tento dotaz přidáním **rozsahu\_identity ()** na konci dotazu, který vrátí poslední hodnotu identity vloženou do sloupce **identity** ve stejném oboru. (Další informace o **oboru\_identity ()** najdete v [technické dokumentaci](https://msdn.microsoft.com/library/ms190315.aspx) a proč byste pravděpodobně chtěli [použít obor\_identity () místo @@IDENTITY](http://weblogs.sqlteam.com/travisl/archive/2003/10/29/405.aspx).) Před přidáním příkazu **Select** je nutné ukončit příkaz **INSERT** středníkem.

[![rozšířit dotaz tak, aby vracel hodnotu SCOPE_IDENTITY ()](creating-a-data-access-layer-cs/_static/image71.png)](creating-a-data-access-layer-cs/_static/image70.png)

**Obrázek 26**: rozšíření dotazu pro návrat **rozsahu\_hodnoty identity ()** ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-cs/_static/image72.png))

Nakonec pojmenujte novou metodu **InsertProduct**.

[![nastavte nový název metody na InsertProduct](creating-a-data-access-layer-cs/_static/image74.png)](creating-a-data-access-layer-cs/_static/image73.png)

**Obrázek 27**: Nastavte nový název metody na **InsertProduct** ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-cs/_static/image75.png)).

Když se vrátíte do návrháře DataSet, uvidíte, že **ProductsTableAdapter** obsahuje novou metodu **InsertProduct**. Pokud tato nová metoda nemá parametr pro každý sloupec v tabulce **Products** , je pravděpodobné, že jste zapomněli příkaz **INSERT** uzavřít středníkem. Nakonfigurujte metodu **InsertProduct** a ujistěte se, že máte středníkem vymezené příkazy **INSERT** a **Select** .

Ve výchozím nastavení metody vložení vydávají nedotazové metody, což znamená, že vrací počet ovlivněných řádků. Chceme však, aby metoda **InsertProduct** vrátila hodnotu vrácenou dotazem, nikoli počet ovlivněných řádků. Chcete-li to dosáhnout, upravte vlastnost **ExecuteMode** metody **InsertProduct** na **skalární**.

[![změnit vlastnost ExecuteMode na skalární](creating-a-data-access-layer-cs/_static/image77.png)](creating-a-data-access-layer-cs/_static/image76.png)

**Obrázek 28**: Změňte vlastnost **ExecuteMode** na **skalární** ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-cs/_static/image78.png)).

Následující kód ukazuje tuto novou metodu **InsertProduct** v akci:

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample8.cs)]

## <a name="step-5-completing-the-data-access-layer"></a>Krok 5: dokončení vrstvy přístupu k datům

Všimněte si, že třída **ProductsTableAdapters** vrací hodnoty **KódKategorie** a **KódDodavatele** z tabulky **Products** , ale nezahrnuje sloupec **NázevKategorie** z tabulky **Categories** nebo ze sloupce **CompanyName** z tabulky **Dodavatelé** , i když se ale jedná o sloupce, které chceme zobrazit při zobrazení informací o produktu. Je možné rozšířit počáteční metodu TableAdapter, **GetProducts ()** , aby zahrnovala hodnoty sloupce **CategoryName** i **CompanyName** , které budou aktualizovat silně typované objekty DataTable, aby zahrnovaly i tyto nové sloupce.

To může představovat nějaký problém, ale TableAdapter metody pro vkládání, aktualizaci a odstraňování dat vycházejí z této prvotní metody. Automaticky generované metody pro vkládání, aktualizaci a odstraňování nejsou ovlivněny poddotazy v klauzuli **Select** . Pokud se rozhodnete přidat dotazy do **kategorií** a **dodavatelů** jako poddotazy, nemusíte se **připojit** k těmto metodám pro úpravu dat. V **ProductsTableAdapter** klikněte pravým tlačítkem na metodu **GetProducts ()** a vyberte Konfigurovat. Pak upravte klauzuli **Select** tak, aby vypadala takto:

[!code-sql[Main](creating-a-data-access-layer-cs/samples/sample9.sql)]

[![aktualizace příkazu SELECT pro metodu GetProducts ()](creating-a-data-access-layer-cs/_static/image80.png)](creating-a-data-access-layer-cs/_static/image79.png)

**Obrázek 29**: aktualizace příkazu **Select** pro metodu **GetProducts ()** ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-cs/_static/image81.png))

Po aktualizaci metody **GetProducts ()** pro použití tohoto nového dotazu bude objekt DataTable obsahovat dva nové sloupce: **CategoryName** a **ČísloDodavatele**.

![Objekt DataTable obsahuje dva nové sloupce.](creating-a-data-access-layer-cs/_static/image82.png)

**Obrázek 30**: DataTable **Products** obsahuje dva nové sloupce.

Aktualizujte klauzuli **Select** v metodě **GetProductsByCategoryID (*CategoryID*)** a chvíli počkejte.

Pokud provedete aktualizaci **GetProducts ()** **Výběr** pomocí syntaxe **Join** , Návrhář DataSet nebude moci automaticky generovat metody pro vkládání, aktualizaci a odstraňování dat databáze pomocí modelu přímé databáze. Místo toho je budete muset ručně vytvořit stejně jako u metody **InsertProduct** dříve v tomto kurzu. Pokud chcete použít vzor pro aktualizaci dávkových aktualizací, budete muset ručně zadat hodnoty vlastností **InsertCommand**, **UpdateCommand**a **DeleteCommand** .

## <a name="adding-the-remaining-tableadapters"></a>Přidání zbývajících objekty TableAdapter

Až do té doby jsme si prohlíželi práci s jedním TableAdapter pro jednu databázovou tabulku. Databáze Northwind ale obsahuje několik souvisejících tabulek, se kterými budeme v naší webové aplikaci pracovat. Typová datová sada může obsahovat více souvisejících datových tabulek. Proto je potřeba přidat do těchto kurzů DataTables pro další tabulky, které budeme používat. Chcete-li přidat novou TableAdapter do typové datové sady, otevřete návrháře DataSet, klikněte pravým tlačítkem myši v návrháři a vyberte možnost Přidat/TableAdapter. Tím se vytvoří nový objekt DataTable a TableAdapter a provede vás průvodcem, který jsme prozkoumali dříve v tomto kurzu.

Vytvoření následujících objekty TableAdapter a metod pomocí následujících dotazů vám může trvat několik minut. Všimněte si, že dotazy v **ProductsTableAdapter** zahrnují poddotazy pro převzetí názvů kategorií a dodavatelů jednotlivých produktů. Kromě toho, pokud jste spolu popracovali společně, již jste přidali metody **GetProducts ()** a **GetProductsByCategoryID (*KódKategorie*)** třídy **ProductsTableAdapter** .

- **ProductsTableAdapter**

  - **GetProducts**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample10.sql)]
  - **GetProductsByCategoryID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample11.sql)]
  - **GetProductsBySupplierID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample12.sql)]
  - **GetProductByProductID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample13.sql)]
- **CategoriesTableAdapter**

  - **GetCategories**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample14.sql)]
  - **GetCategoryByCategoryID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample15.sql)]
- **SuppliersTableAdapter**

  - **Getdodavatelé**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample16.sql)]
  - **GetSuppliersByCountry**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample17.sql)]
  - **GetSupplierBySupplierID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample18.sql)]
- **EmployeesTableAdapter**

  - **Getzaměstnanci**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample19.sql)]
  - **GetEmployeesByManager**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample20.sql)]
  - **GetEmployeeByEmployeeID**: 

      [!code-sql[Main](creating-a-data-access-layer-cs/samples/sample21.sql)]

[![návrháře DataSet po přidání čtyř objekty TableAdapter](creating-a-data-access-layer-cs/_static/image84.png)](creating-a-data-access-layer-cs/_static/image83.png)

**Obrázek 31**: Návrhář datových sad po přidání čtyř objekty TableAdapter ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-cs/_static/image85.png))

## <a name="adding-custom-code-to-the-dal"></a>Přidání vlastního kódu do DAL

Objekty TableAdapter a DataTable přidané do typované datové sady jsou vyjádřeny jako definiční soubor schématu XML (**Northwind. xsd**). Informace o tomto schématu můžete zobrazit tak, že kliknete pravým tlačítkem na soubor **Northwind. xsd** v Průzkumník řešení a zvolíte zobrazit kód.

[![soubor XSD (XML Schema Definition) pro typovou datovou sadu Northwind](creating-a-data-access-layer-cs/_static/image87.png)](creating-a-data-access-layer-cs/_static/image86.png)

**Obrázek 32**: soubor XSD (XML Schema Definition) pro datovou sadu Northwinds ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-data-access-layer-cs/_static/image88.png))

Tyto informace o schématu jsou přeloženy do C# nebo Visual Basic kódu v době návrhu při kompilaci nebo v době běhu (v případě potřeby), kde je lze procházet pomocí ladicího programu. Chcete-li zobrazit tento automaticky generovaný kód, přejděte na Zobrazení tříd a přejděte k podrobnostem o třídách DataSet typu TableAdapter nebo. Pokud se Zobrazení tříd na obrazovce nezobrazuje, přejděte do nabídky zobrazení a vyberte ji tam nebo stiskněte kombinaci kláves CTRL + SHIFT + C. Z Zobrazení tříd můžete zobrazit vlastnosti, metody a události typové datové sady a třídy TableAdapter. Chcete-li zobrazit kód pro určitou metodu, poklikejte na název metody v Zobrazení tříd, klikněte na něj pravým tlačítkem myši a vyberte možnost přejít k definici.

![Zkontrolujte automaticky generovaný kód výběrem možnosti přejít k definici z Zobrazení tříd](creating-a-data-access-layer-cs/_static/image89.png)

**Obrázek 33**: Zkontrolujte automaticky generovaný kód výběrem možnosti přejít k definici z zobrazení tříd

I když se automaticky generovaný kód může jednat o skvělý čas, kód je často velmi obecný a musí být přizpůsoben, aby splňoval jedinečné potřeby aplikace. Riziko rozšíření automaticky generovaného kódu je ale tím, že nástroj, který kód vygeneroval, může rozhodnout, že je čas na "znovu vygenerovat" a přepsat vlastní nastavení. Pomocí nového konceptu částečné třídy .NET 2.0 je snadné rozdělit třídu napříč více soubory. Díky tomu můžeme přidat vlastní metody, vlastnosti a události do automaticky generovaných tříd, aniž byste si museli dělat starosti se zapisováním vlastních úprav do sady Visual Studio.

Abychom ukázali, jak přizpůsobit DAL, přidáme metodu **GetProducts ()** do třídy **SuppliersRow** . Třída **SuppliersRow** představuje jeden záznam v tabulce **Dodavatelé** ; každý dodavatel může u mnoha produktů získat nulu, takže **GetProducts ()** bude tyto produkty zadaného dodavatele vracet. K tomuto účelu vytvořte nový soubor třídy ve složce **aplikace\_kódu** s názvem **SuppliersRow.cs** a přidejte následující kód:

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample22.cs)]

Tato částečná třída instruuje kompilátor, který při sestavování třídy **Northwind. SuppliersRow** zahrnuje metodu **GetProducts ()** , kterou jsme právě definovali. Pokud projekt sestavíte a pak se vrátíte k Zobrazení tříd uvidíte **GetProducts ()** nyní uvedené jako metoda **Northwind. SuppliersRow**.

![Metoda GetProducts () je teď součástí třídy Northwind. SuppliersRow.](creating-a-data-access-layer-cs/_static/image90.png)

**Obrázek 34**: metoda **GetProducts ()** je teď součástí třídy **Northwind. SuppliersRow.**

Metoda **GetProducts ()** se teď dá použít k zobrazení výčtu sady produktů pro konkrétního dodavatele, jak ukazuje následující kód:

[!code-html[Main](creating-a-data-access-layer-cs/samples/sample23.html)]

Tato data je možné zobrazit také v jakémkoli z ASP. Webové ovládací prvky pro data netto. Následující stránka používá ovládací prvek GridView se dvěma poli:

- Vlastnost BoundField, který zobrazuje jméno každého dodavatele a
- TemplateField, který obsahuje ovládací prvek BulletedList, který je svázán s výsledky vrácenými metodou **GetProducts ()** pro každého dodavatele.

Podíváme se, jak tyto sestavy hlavní-podrobnosti zobrazit v budoucích kurzech. Nyní je tento příklad navržen pro ilustraci pomocí vlastní metody přidané do třídy **Northwind. SuppliersRow** .

SuppliersAndProducts.aspx

[!code-aspx[Main](creating-a-data-access-layer-cs/samples/sample24.aspx)]

SuppliersAndProducts.aspx.cs

[!code-csharp[Main](creating-a-data-access-layer-cs/samples/sample25.cs)]

[![název společnosti dodavatele je uveden v levém sloupci a jejich produkty napravo.](creating-a-data-access-layer-cs/_static/image92.png)](creating-a-data-access-layer-cs/_static/image91.png)

**Obrázek 35**: název společnosti dodavatele je uveden v levém sloupci a jejich produkty napravo ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-data-access-layer-cs/_static/image93.png)

## <a name="summary"></a>Souhrn

Při sestavování webové aplikace, která vytvořila DAL, by měl být jedním z vašich prvních kroků, ke kterým došlo před tím, než začnete vytvářet prezentační vrstvu. V sadě Visual Studio je vytvořením DAL na základě typových datových sad úkol, který je možné provést během 10-15 minut, aniž byste museli psát řádek kódu. Kurzy, které se přesunou dál, se na tomto DAL vytvoří. V [dalším kurzu](creating-a-business-logic-layer-cs.md) definujeme několik obchodních pravidel a zjistíte, jak je implementovat do samostatné vrstvy obchodní logiky.

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
> [Next](creating-a-business-logic-layer-cs.md)

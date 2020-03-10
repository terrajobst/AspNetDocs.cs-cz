---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/working-with-computed-columns-vb
title: Práce s počítanými sloupci (VB) | Microsoft Docs
author: rick-anderson
description: Při vytváření tabulky databáze Microsoft SQL Server umožňuje definovat počítaný sloupec, jehož hodnota je vypočítána z výrazu, který je obvykle referen...
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 5811b8ff-ed56-40fc-9397-6b69ae09a8f6
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/working-with-computed-columns-vb
msc.type: authoredcontent
ms.openlocfilehash: e425d7363c2cdea6efb0ba51f3fc2b6a5330bf2a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78524484"
---
# <a name="working-with-computed-columns-vb"></a>Práce s vypočítanými sloupci (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_71_VB.zip) nebo [stažení PDF](working-with-computed-columns-vb/_static/datatutorial71vb1.pdf)

> Při vytváření tabulky databáze Microsoft SQL Server umožňuje definovat počítaný sloupec, jehož hodnota je vypočítána z výrazu, který obvykle odkazuje na jiné hodnoty ve stejném záznamu databáze. Tyto hodnoty jsou v databázi jen pro čtení, což vyžaduje zvláštní požadavky při práci s objekty TableAdapter. V tomto kurzu se dozvíte, jak splnit problémy, které představují vypočítané sloupce.

## <a name="introduction"></a>Úvod

Microsoft SQL Server umožňuje *[vypočítané sloupce](https://msdn.microsoft.com/library/ms191250.aspx)* , které jsou sloupce, jejichž hodnoty jsou vypočítány z výrazu, který obvykle odkazuje na hodnoty z jiných sloupců ve stejné tabulce. Například datový model sledování času může mít tabulku s názvem `ServiceLog` se sloupci, včetně `ServicePerformed`, `EmployeeID`, `Rate`a `Duration`, mimo jiné. I když může být částka splatná na jednu z položek služby (sazba vynásobená dobou trvání) pomocí webové stránky nebo jiného programového rozhraní, může být užitečné zahrnout sloupec do `ServiceLog` tabulky s názvem `AmountDue`, která tyto informace ohlásila. Tento sloupec se dá vytvořit jako normální sloupec, ale je potřeba ho aktualizovat, aby se změnily hodnoty `Rate` nebo `Duration` sloupce. Lepším řešením je nastavit `AmountDue` sloupec jako počítaný sloupec pomocí `Rate * Duration`výrazů. To by způsobilo, SQL Server automaticky vypočítat hodnotu `AmountDue` sloupce pokaždé, když se na ni odkazuje v dotazu.

Vzhledem k tomu, že hodnota počítaného sloupce je určena výrazem, jsou tyto sloupce určeny pouze pro čtení, a proto nemohou mít přiřazené hodnoty v `INSERT` nebo `UPDATE`ch příkazech. Pokud jsou však vypočítané sloupce součástí hlavního dotazu pro TableAdapter, který používá příkazy SQL ad hoc, jsou automaticky zahrnuty do automaticky generovaných příkazů `INSERT` a `UPDATE`. V důsledku toho je nutné aktualizovat TableAdapter s `INSERT` a `UPDATE` dotazy a `InsertCommand` a `UpdateCommand` vlastnosti pro odebrání odkazů na vypočítané sloupce.

Jednou z výzev k použití počítaných sloupců s TableAdapter, který používá příkazy SQL ad-hoc, je, že se automaticky znovu vygenerovaly dotazy TableAdapter s `INSERT` a `UPDATE`, kdykoli Průvodce konfigurací TableAdapter dokončen. Proto se vypočítané sloupce ručně odeberou z `INSERT` a dotazy `UPDATE` se znovu zobrazí, pokud se průvodce znovu spustí. I když objekty TableAdapter, které používají uložené procedury, od tohoto brittleness nepřijde, mají vlastní adaptivní, které budeme řešit v kroku 3.

V tomto kurzu přidáme vypočítaný sloupec do tabulky `Suppliers` v databázi Northwind a pak vytvoříte odpovídající TableAdapter pro práci s touto tabulkou a jejím vypočítaným sloupcem. Naše TableAdapter použije uložené procedury místo ad-hoc příkazů SQL, takže naše přizpůsobení nebudou po použití Průvodce konfigurací TableAdapter ztracena.

Pojďme začít!

## <a name="step-1-adding-a-computed-column-to-thesupplierstable"></a>Krok 1: Přidání vypočítaného sloupce do tabulky`Suppliers`

Databáze Northwind neobsahuje žádné počítané sloupce, takže je potřeba přidat jednu dodržovali. V tomto kurzu přidáme vypočítaný sloupec do tabulky `Suppliers` s názvem `FullContactName`, která vrací kontakt s názvem, názvem a společností, pro kterou pracují, v následujícím formátu: `ContactName` (`ContactTitle`, `CompanyName`). Tento počítaný sloupec může být použit v sestavách při zobrazení informací o dodavatelích.

Začněte otevřením `Suppliers` definice tabulky kliknutím pravým tlačítkem myši na tabulku `Suppliers` v Průzkumník serveru a výběrem možnosti otevřít definici tabulky z kontextové nabídky. Zobrazí se sloupce tabulky a jejich vlastnosti, jako je například datový typ, ať už `NULL` s a tak dále. Chcete-li přidat vypočítaný sloupec, začněte zadáním názvu sloupce do definice tabulky. V dalším kroku zadejte svůj výraz do textového pole (vzorec) pod oddílem specifikace vypočítaného sloupce ve sloupci okno Vlastnosti (viz obrázek 1). Vypočítaný sloupec pojmenujte `FullContactName` a použijte následující výraz:

[!code-sql[Main](working-with-computed-columns-vb/samples/sample1.sql)]

Všimněte si, že řetězce lze zřetězit v SQL pomocí operátoru `+`. Příkaz `CASE` lze použít jako podmíněný v tradičním programovacím jazyce. Ve výrazu výše lze příkaz `CASE` přečíst jako: Pokud `ContactTitle` není `NULL` pak výstup hodnoty `ContactTitle` zřetězené s čárkou, jinak vygeneruje nic. Další informace o užitečnosti `CASE` příkazu naleznete v tématu [výkon příkazů SQL `CASE`](http://www.4guysfromrolla.com/webtech/102704-1.shtml).

> [!NOTE]
> Místo použití `CASE`ho příkazu zde můžeme použít jinou `ISNULL(ContactTitle, '')`. [`ISNULL(checkExpression, replacementValue)`](https://msdn.microsoft.com/library/ms184325.aspx) vrátí *checkExpression* , pokud není null, jinak vrátí *replacementValue*. I když `ISNULL` nebo `CASE` v této instanci budou fungovat, existují složitější scénáře, kdy flexibilitu příkazu `CASE` nemůže odpovídat `ISNULL`.

Po přidání tohoto vypočítaného sloupce by vaše obrazovka měla vypadat jako snímek obrazovky na obrázku 1.

[![do tabulky Dodavatelé přidat vypočítaný sloupec s názvem FullContactName](working-with-computed-columns-vb/_static/image2.png)](working-with-computed-columns-vb/_static/image1.png)

**Obrázek 1**: přidejte do tabulky `Suppliers` vypočítaný sloupec s názvem `FullContactName` ([kliknutím zobrazíte obrázek v plné velikosti).](working-with-computed-columns-vb/_static/image3.png)

Po pojmenování vypočítaného sloupce a zadání jeho výrazu uložte změny v tabulce kliknutím na ikonu Uložit na panelu nástrojů, podržením klávesy CTRL + S nebo přechodem do nabídky soubor a výběrem možnosti Uložit `Suppliers`.

Uložení tabulky by mělo aktualizovat Průzkumník serveru, včetně právě přidaného sloupce v seznamu sloupců `Suppliers` tabulky s. Kromě toho se výraz zadaný do textového pole (vzorec) automaticky upraví na ekvivalentní výraz, který odstraní nadbytečné prázdné znaky, obklopuje názvy sloupců s hranatými závorkami (`[]`) a obsahuje závorky k explicitnímu zobrazení pořadí operací:

[!code-sql[Main](working-with-computed-columns-vb/samples/sample2.sql)]

Další informace o vypočítaných sloupcích v Microsoft SQL Server najdete v [technické dokumentaci](https://msdn.microsoft.com/library/ms191250.aspx). Také si přečtěte téma [Postupy: určení vypočítaných sloupců](https://msdn.microsoft.com/library/ms188300.aspx) pro podrobný návod k vytváření počítaných sloupců.

> [!NOTE]
> Ve výchozím nastavení nejsou vypočítané sloupce fyzicky uloženy v tabulce, ale místo toho jsou přepočítány pokaždé, když jsou odkazovány v dotazu. Zaškrtnutím políčka je trvalé, ale můžete dát SQL Server k fyzickému uložení vypočítaného sloupce v tabulce. To umožňuje vytvořit index pro vypočítaný sloupec, což může zlepšit výkon dotazů, které používají vypočítanou hodnotu sloupce ve svých `WHERE` klauzulích. Další informace najdete v tématu [vytváření indexů na počítaných sloupcích](https://msdn.microsoft.com/library/ms189292.aspx) .

## <a name="step-2-viewing-the-computed-column-s-values"></a>Krok 2: zobrazení hodnot počítaných sloupců

Předtím, než začneme pracovat na vrstvě pro přístup k datům, může trvat několik minut, než se zobrazí `FullContactName` hodnoty. Z Průzkumník serveru klikněte pravým tlačítkem myši na název tabulky `Suppliers` a v místní nabídce vyberte možnost Nový dotaz. Tím zobrazíte okno dotazu, které vás vyzve k výběru tabulek, které se mají zahrnout do dotazu. Přidejte `Suppliers`ovou tabulku a klikněte na Zavřít. Dále v tabulce Dodavatelé vyhledejte sloupce `CompanyName`, `ContactName`, `ContactTitle`a `FullContactName`. Nakonec klikněte na ikonu červeného vykřičníku na panelu nástrojů a spusťte dotaz a zobrazte výsledky.

Jak ukazuje obrázek 2, výsledky zahrnují `FullContactName`, které obsahují sloupce `CompanyName`, `ContactName`a `ContactTitle` ve formátu `ContactName` (`ContactTitle`, `CompanyName`).

[![FullContactName používá formát kontakt (ContactTitle, CompanyName).](working-with-computed-columns-vb/_static/image5.png)](working-with-computed-columns-vb/_static/image4.png)

**Obrázek 2**: `FullContactName` používá formát `ContactName` (`ContactTitle`, `CompanyName`) ([kliknutím zobrazíte obrázek v plné velikosti).](working-with-computed-columns-vb/_static/image6.png)

## <a name="step-3-adding-thesupplierstableadapterto-the-data-access-layer"></a>Krok 3: Přidání`SuppliersTableAdapter`do vrstvy přístupu k datům

Aby bylo možné pracovat s informacemi o dodavatelích v naší aplikaci, musíme nejdřív vytvořit TableAdapter a DataTable v naší DAL. V ideálním případě by to bylo provedeno pomocí stejných přímočarých kroků, které byly zkontrolovány v předchozích kurzech. Práce s počítanými sloupci ale zavádí několik wrinklesů, které je dobré diskutovat.

Pokud používáte TableAdapter, který používá příkazy SQL ad hoc, můžete do hlavního dotazu TableAdaptery jednoduše vložit vypočítaný sloupec prostřednictvím Průvodce konfigurací TableAdapter. Tato akce však automaticky generuje `INSERT` a `UPDATE` příkazy, které obsahují vypočítaný sloupec. Pokud se pokusíte spustit jednu z těchto metod, `SqlException` se zprávou sloupec *ColumnName* sloupce nelze změnit, protože se jedná o vypočítaný sloupec nebo je vyvolána výsledek OPERÁTORu sjednocení. I když lze příkaz `INSERT` a `UPDATE` ručně upravit prostřednictvím `InsertCommand` TableAdapter s a `UpdateCommand` vlastností, budou při každém opětovném spuštění Průvodce konfigurací TableAdapter ztraceny tyto vlastní úpravy.

Vzhledem k tomu, že brittleness objekty TableAdapter, které používají příkazy SQL ad-hoc, se doporučuje použít uložené procedury při práci s vypočítanými sloupci. Pokud používáte stávající uložené procedury, jednoduše nakonfigurujte TableAdapter, jak je popsáno v kurzu [použití existujících uložených procedur pro typový objekty TableAdapter sady typů](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md) . Máte-li Průvodce TableAdapter vytvořit uložené procedury pro vás, je důležité nejprve vynechat všechny vypočítané sloupce z hlavního dotazu. Pokud zahrnete do hlavního dotazu vypočítaný sloupec, Průvodce konfigurací TableAdapter vám po dokončení upozorní, že nemůže vytvořit odpovídající uložené procedury. V krátkém případě je potřeba nejdřív nakonfigurovat TableAdapter pomocí vypočítaného hlavního dotazu bez sloupců a pak ručně aktualizovat odpovídající uloženou proceduru a `SelectCommand` TableAdapter s, aby zahrnovaly vypočítaný sloupec. Tento přístup je podobný jako ten, který se používá v kurzu [aktualizace TableAdapter pro použití](updating-the-tableadapter-to-use-joins-vb.md)`JOIN`*s* .

Pro tento kurz přidejte nové TableAdapter a nechte si automaticky vytvořit uložené procedury pro nás. V důsledku toho bude nutné zpočátku z hlavního dotazu vynechat vypočítaný sloupec `FullContactName`.

Začněte tím, že otevřete `NorthwindWithSprocs` datovou sadu ve složce `~/App_Code/DAL`. Klikněte pravým tlačítkem myši v návrháři a v místní nabídce vyberte možnost Přidat nový TableAdapter. Tím se spustí Průvodce konfigurací TableAdapter. Zadejte databázi, ze které se mají dotazovat data (`NORTHWNDConnectionString` z `Web.config`) a klikněte na další. Vzhledem k tomu, že jsme ještě nevytvořili žádné uložené procedury pro dotazování nebo úpravu `Suppliers` tabulky, vyberte možnost vytvořit nové uložené procedury, aby ji průvodce vytvořil pro nás a klikněte na další.

[![zvolit možnost vytvořit nové uložené procedury](working-with-computed-columns-vb/_static/image8.png)](working-with-computed-columns-vb/_static/image7.png)

**Obrázek 3**: vyberte možnost vytvořit nové uložené procedury ([kliknutím zobrazíte obrázek v plné velikosti).](working-with-computed-columns-vb/_static/image9.png)

V dalším kroku se zobrazí výzva pro hlavní dotaz. Zadejte následující dotaz, který vrací sloupce `SupplierID`, `CompanyName`, `ContactName`a `ContactTitle` pro každého dodavatele. Všimněte si, že tento dotaz záměrně vynechá vypočítaný sloupec (`FullContactName`); odpovídající uloženou proceduru aktualizujeme tak, aby obsahovala tento sloupec v kroku 4.

[!code-sql[Main](working-with-computed-columns-vb/samples/sample3.sql)]

Po zadání hlavního dotazu a kliknutí na tlačítko Další vám Průvodce umožní pojmenovat čtyři uložené procedury, které budou vygenerovány. Pojmenujte tyto uložené procedury `Suppliers_Select`, `Suppliers_Insert`, `Suppliers_Update`a `Suppliers_Delete`, jak ukazuje obrázek 4.

[![přizpůsobení názvů automaticky generovaných uložených procedur](working-with-computed-columns-vb/_static/image11.png)](working-with-computed-columns-vb/_static/image10.png)

**Obrázek 4**: Přizpůsobení názvů automaticky generovaných uložených procedur ([kliknutím zobrazíte obrázek v plné velikosti](working-with-computed-columns-vb/_static/image12.png))

Další krok průvodce vám umožní pojmenovat metody TableAdapter s a zadat vzory používané pro přístup k datům a jejich aktualizaci. Nechejte zaškrtnutá všechna tři zaškrtávací políčka, ale přejmenujte metodu `GetData` na `GetSuppliers`. Kliknutím na Dokončit dokončete průvodce.

[![přejmenovat metodu GetData na getsuppliers](working-with-computed-columns-vb/_static/image14.png)](working-with-computed-columns-vb/_static/image13.png)

**Obrázek 5**: Přejmenujte metodu `GetData` na `GetSuppliers` ([kliknutím zobrazíte obrázek v plné velikosti).](working-with-computed-columns-vb/_static/image15.png)

Po kliknutí na tlačítko Dokončit průvodce vytvoří čtyři uložené procedury a přidá TableAdapter a odpovídající DataTable do typované datové sady.

## <a name="step-4-including-the-computed-column-in-the-tableadapter-s-main-query"></a>Krok 4: zahrnutí vypočítaného sloupce do hlavního dotazu TableAdapter s

Teď je potřeba aktualizovat TableAdapter a DataTable vytvořené v kroku 3, aby zahrnovaly vypočítaný sloupec `FullContactName`. To zahrnuje dva kroky:

1. Aktualizace uložené procedury `Suppliers_Select` pro vrácení `FullContactName` vypočítaného sloupce a
2. Aktualizace objektu DataTable tak, aby zahrnovala odpovídající sloupec `FullContactName`.

Začněte tím, že přejdete na Průzkumník serveru a rozcházíte do složky uložené procedury. Otevřete `Suppliers_Select` uloženou proceduru a aktualizujte dotaz `SELECT` tak, aby zahrnoval `FullContactName` počítaný sloupec:

[!code-sql[Main](working-with-computed-columns-vb/samples/sample4.sql)]

Uložte změny uložené procedury kliknutím na ikonu Uložit na panelu nástrojů, podržením klávesy CTRL + S nebo výběrem možnosti Uložit `Suppliers_Select` v nabídce soubor.

Potom se vraťte do návrháře DataSet, klikněte pravým tlačítkem na `SuppliersTableAdapter`a v místní nabídce vyberte Konfigurovat. Všimněte si, že sloupec `Suppliers_Select` nyní obsahuje sloupec `FullContactName` v kolekci datových sloupců.

[Pokud chcete aktualizovat sloupce DataTable s, ![spusťte Průvodce konfigurací TableAdapter s.](working-with-computed-columns-vb/_static/image17.png)](working-with-computed-columns-vb/_static/image16.png)

**Obrázek 6**: spusťte Průvodce konfigurací TableAdapter s a aktualizujte sloupce DataTable s ([kliknutím zobrazíte obrázek v plné velikosti).](working-with-computed-columns-vb/_static/image18.png)

Kliknutím na Dokončit dokončete průvodce. Tím se automaticky přidá odpovídající sloupec do `SuppliersDataTable`. Průvodce TableAdapter je dostatečně inteligentní, aby zjistil, že `FullContactName` sloupec je vypočítaný sloupec, a proto jen pro čtení. V důsledku toho nastaví vlastnost `ReadOnly` sloupců na hodnotu `true`. Pokud to chcete ověřit, vyberte sloupec z `SuppliersDataTable` a potom přejděte na okno Vlastnosti (viz obrázek 7). Všimněte si, že vlastnosti `FullContactName` sloupce s `DataType` a `MaxLength` jsou nastaveny také odpovídajícím způsobem.

[![sloupec FullContactName je označen jen pro čtení.](working-with-computed-columns-vb/_static/image20.png)](working-with-computed-columns-vb/_static/image19.png)

**Obrázek 7**: `FullContactName` sloupec je označen jen pro čtení ([kliknutím zobrazíte obrázek v plné velikosti](working-with-computed-columns-vb/_static/image21.png)).

## <a name="step-5-adding-agetsupplierbysupplieridmethod-to-the-tableadapter"></a>Krok 5: Přidání metody`GetSupplierBySupplierID`do TableAdapter

V tomto kurzu vytvoříme stránku ASP.NET, která zobrazí dodavatele v mřížce s aktualizovatelným zobrazením. V minulých kurzech aktualizovali jeden záznam z vrstvy obchodní logiky načtením tohoto konkrétního záznamu z DAL jako silně typovaného objektu DataTable, aktualizací vlastností a následným odesláním aktualizovaného objektu DataTable zpátky zpět na DAL, aby se změny rozšířily. databáze. Abyste mohli provést tento první krok – načte se záznam, který se aktualizuje z DAL, musíme nejdřív do DAL přidat metodu `GetSupplierBySupplierID(supplierID)`.

Pravým tlačítkem myši klikněte na `SuppliersTableAdapter` v návrhu datové sady a vyberte možnost Přidat dotaz z kontextové nabídky. Stejně jako v kroku 3 nechejte průvodce pro nás vytvořit novou úložnou proceduru, a to tak, že vyberete možnost vytvořit novou uloženou proceduru (snímek obrazovky tohoto kroku průvodce najdete zpátky na obrázek 3). Vzhledem k tomu, že tato metoda vrátí záznam s více sloupci, určete, že chceme použít dotaz SQL, který je SELECT, který vrací řádky a klikněte na tlačítko Další.

[![zvolte možnost vybrat, které vrací řádky.](working-with-computed-columns-vb/_static/image23.png)](working-with-computed-columns-vb/_static/image22.png)

**Obrázek 8**: zvolte možnost vybrat, které vrací řádky ([kliknutím zobrazíte obrázek v plné velikosti](working-with-computed-columns-vb/_static/image24.png)).

V dalším kroku se zobrazí výzva pro dotaz, který se má použít pro tuto metodu. Zadejte následující příkaz, který vrátí stejná datová pole jako hlavní dotaz, ale pro konkrétního dodavatele.

[!code-sql[Main](working-with-computed-columns-vb/samples/sample5.sql)]

Na další obrazovce se dozvíte, jak pojmenovat uloženou proceduru, která se vygeneruje automaticky. Pojmenujte tuto uloženou proceduru `Suppliers_SelectBySupplierID` a klikněte na tlačítko Další.

[![uloženou proceduru pojmenovat Suppliers_SelectBySupplierID](working-with-computed-columns-vb/_static/image26.png)](working-with-computed-columns-vb/_static/image25.png)

**Obrázek 9**: pojmenujte uloženou proceduru `Suppliers_SelectBySupplierID` ([kliknutím zobrazíte obrázek v plné velikosti).](working-with-computed-columns-vb/_static/image27.png)

Nakonec průvodce vyzve k zadání vzorů přístupu k datům a názvů metod, které se mají použít pro TableAdapter. Ponechte zaškrtnuté obě políčka, ale přejmenujte `FillBy` a `GetDataBy` metody na `FillBySupplierID` a `GetSupplierBySupplierID`, v uvedeném pořadí.

[![pojmenovat metody TableAdapter FillBySupplierID a GetSupplierBySupplierID](working-with-computed-columns-vb/_static/image29.png)](working-with-computed-columns-vb/_static/image28.png)

**Obrázek 10**: pojmenování metod TableAdapter `FillBySupplierID` a `GetSupplierBySupplierID` ([kliknutím zobrazíte obrázek v plné velikosti](working-with-computed-columns-vb/_static/image30.png))

Kliknutím na Dokončit dokončete průvodce.

## <a name="step-6-creating-the-business-logic-layer"></a>Krok 6: vytvoření vrstvy obchodní logiky

Než vytvoříme stránku ASP.NET, která používá vypočítaný sloupec vytvořený v kroku 1, nejdřív je potřeba přidat odpovídající metody do knihoven BLL. Naše stránka ASP.NET, kterou vytvoříme v kroku 7, umožní uživatelům zobrazit a upravit dodavatele. Proto potřebujeme, aby naše knihoven BLL poskytovala minimálně metodu pro získání všech dodavatelů a dalšího pro aktualizaci konkrétního dodavatele.

Ve složce `~/App_Code/BLL` vytvořte nový soubor třídy s názvem `SuppliersBLLWithSprocs` a přidejte následující kód:

[!code-vb[Main](working-with-computed-columns-vb/samples/sample6.vb)]

Podobně jako ostatní třídy knihoven BLL má `SuppliersBLLWithSprocs` vlastnost `Protected` `Adapter`, která vrací instanci `SuppliersTableAdapter` společně se dvěma `Public` metodami: `GetSuppliers` a `UpdateSupplier`. Metoda `GetSuppliers` volá a vrátí `SuppliersDataTable` vracené odpovídající `GetSupplier` metodou ve vrstvě přístupu k datům. Metoda `UpdateSupplier` načte informace o určitém dodavateli, který je aktualizován prostřednictvím volání metody DAL s `GetSupplierBySupplierID(supplierID)`. Poté aktualizuje vlastnosti `CategoryName`, `ContactName`a `ContactTitle` a potvrdí tyto změny v databázi voláním metody pro přístup k datům v metodě `Update` a předáním upraveného objektu `SuppliersRow`.

> [!NOTE]
> S výjimkou `SupplierID` a `CompanyName`všechny sloupce v tabulce Dodavatelé povolují `NULL` hodnoty. Proto pokud jsou předané `contactName` nebo `contactTitle` parametry `Nothing` potřebujeme nastavit odpovídající `ContactName` a `ContactTitle` vlastnosti na hodnotu databáze `NULL` pomocí `SetContactNameNull` a `SetContactTitleNull`ch metod, v uvedeném pořadí.

## <a name="step-7-working-with-the-computed-column-from-the-presentation-layer"></a>Krok 7: práce s vypočítaným sloupcem z prezentační vrstvy

Když je vypočítaný sloupec přidaný do tabulky `Suppliers` a odpovídajícím způsobem se aktualizuje a knihoven BLL, budeme připraveni vytvořit stránku ASP.NET, která funguje s vypočítaným sloupcem `FullContactName`. Začněte otevřením stránky `ComputedColumns.aspx` ve složce `AdvancedDAL` a přetažením prvku GridView z panelu nástrojů do návrháře. Nastavte vlastnost `ID` ovládacího prvku GridView na `Suppliers` a ze své inteligentní značky ji navažte na nový prvek ObjectDataSource s názvem `SuppliersDataSource`. Nakonfigurujte prvek ObjectDataSource tak, aby používal třídu `SuppliersBLLWithSprocs`, kterou jsme přidali zpátky v kroku 6, a klikněte na další.

[![nakonfigurovat prvek ObjectDataSource tak, aby používal třídu SuppliersBLLWithSprocs](working-with-computed-columns-vb/_static/image32.png)](working-with-computed-columns-vb/_static/image31.png)

**Obrázek 11**: Konfigurace prvku ObjectDataSource, aby používal třídu `SuppliersBLLWithSprocs` ([kliknutím zobrazíte obrázek v plné velikosti](working-with-computed-columns-vb/_static/image33.png))

V `SuppliersBLLWithSprocs` třídy jsou definovány pouze dvě metody: `GetSuppliers` a `UpdateSupplier`. Zajistěte, aby byly tyto dvě metody zadány na kartách vybrat a aktualizovat, a kliknutím na tlačítko Dokončit dokončíte konfiguraci prvku ObjectDataSource.

Po dokončení Průvodce konfigurací zdroje dat přidá Visual Studio vlastnost BoundField pro každé vracená datová pole. Odeberte `SupplierID` vlastnost BoundField a změňte vlastnosti `HeaderText` `CompanyName`, `ContactName`, `ContactTitle`a `FullContactName` BoundFields na společnost, jméno kontaktu, název a jméno a příjmení kontaktní osoby v uvedeném pořadí. Z inteligentní značky zaškrtněte políčko Povolit úpravy a zapněte možnosti úprav integrované v prvku GridView.

Kromě přidání BoundFields do prvku GridView, doplňování Průvodce zdrojem dat také způsobí, že sada Visual Studio nastaví vlastnost ObjectDataSource `OldValuesParameterFormatString` na původní\_{0}. Vrátí toto nastavení zpět na výchozí hodnotu {0}.

Po provedení těchto úprav prvku GridView a ObjectDataSource by jejich deklarativní označení mělo vypadat podobně jako následující:

[!code-aspx[Main](working-with-computed-columns-vb/samples/sample7.aspx)]

Potom navštivte tuto stránku v prohlížeči. Jak ukazuje obrázek 12, je každý dodavatel uveden v mřížce, která obsahuje sloupec `FullContactName`, jehož hodnota je jednoduše zřetězení dalších tří sloupců formátovaných jako `ContactName` (`ContactTitle`, `CompanyName`).

[![je každý dodavatel uveden v mřížce.](working-with-computed-columns-vb/_static/image35.png)](working-with-computed-columns-vb/_static/image34.png)

**Obrázek 12**: v mřížce je uveden každý dodavatel ([kliknutím zobrazíte obrázek v plné velikosti](working-with-computed-columns-vb/_static/image36.png)).

Kliknutím na tlačítko Upravit u určitého dodavatele dojde k postbacku a tento řádek je vykreslen v rozhraní pro úpravy (viz obrázek 13). První tři sloupce vykreslí v jejich výchozím rozhraní pro úpravy – ovládací prvek TextBox, jehož vlastnost `Text` je nastavena na hodnotu datového pole. Sloupec `FullContactName` však zůstává jako text. Po přidání BoundFields do prvku GridView při dokončování Průvodce konfigurací zdroje dat byla vlastnost `ReadOnly` `FullContactName` vlastnost BoundField s nastavena na hodnotu `True`, protože odpovídající sloupec `FullContactName` v `SuppliersDataTable` má vlastnost `ReadOnly` nastavena na `True`. Jak je uvedeno v kroku 4, vlastnost `FullContactName` s `ReadOnly` byla nastavena na hodnotu `True`, protože sloupec zjistil, že sloupec byl vypočítaným sloupcem.

[![sloupec FullContactName nelze upravovat.](working-with-computed-columns-vb/_static/image38.png)](working-with-computed-columns-vb/_static/image37.png)

**Obrázek 13**: sloupec `FullContactName` není upravitelný ([kliknutím zobrazíte obrázek v plné velikosti](working-with-computed-columns-vb/_static/image39.png)).

Pokračujte a aktualizujte hodnotu jednoho nebo více upravitelných sloupců a klikněte na aktualizovat. Všimněte si, jak je hodnota `FullContactName` s automaticky aktualizována, aby odrážela změnu.

> [!NOTE]
> Prvek GridView aktuálně používá BoundFields pro upravitelná pole, což vede k výchozímu rozhraní pro úpravy. Vzhledem k tomu, že pole `CompanyName` je požadováno, mělo by být převedeno na TemplateField, který obsahuje RequiredFieldValidator. Ponechám se to jako cvičení pro zúčastněný čtenář. Podrobné pokyny k převodu vlastnost BoundField na TemplateField a přidání ovládacích prvků ověřování najdete v kurzu [Přidání ovládacích prvků ověřování do kurzu pro úpravy a vložení rozhraní](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md) .

## <a name="summary"></a>Souhrn

Při definování schématu pro tabulku Microsoft SQL Server umožňuje zahrnutí počítaných sloupců. Jedná se o sloupce, jejichž hodnoty se počítají z výrazu, který obvykle odkazuje na hodnoty z jiných sloupců ve stejném záznamu. Vzhledem k tomu, že hodnoty pro vypočítané sloupce jsou založené na výrazu, jsou jen pro čtení a nelze jí přiřadit hodnotu v `INSERT` nebo v příkazu `UPDATE`. To přináší problémy při použití vypočítaného sloupce v hlavním dotazu TableAdapter, který se pokusí automaticky vygenerovat odpovídající příkazy `INSERT`, `UPDATE`a `DELETE`.

V tomto kurzu jsme probrali techniky pro obcházení výzev, které představují vypočítané sloupce. Konkrétně jsme použili uložené procedury v našich TableAdapter k překonání brittlenesse v objekty TableAdapter, které používají ad-hoc příkazy SQL. Když Průvodce TableAdapter vytvoří nové uložené procedury, je důležité, aby hlavní dotaz zpočátku vynechal vypočítané sloupce, protože jejich přítomnost brání vygenerování uložených procedur úprav dat. Po navýšení konfigurace TableAdapter můžete znovu použít jeho `SelectCommand` uloženou proceduru, aby zahrnovala všechny vypočítané sloupce.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Hilton Geisenow a Teresa Murphy. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](adding-additional-datatable-columns-vb.md)
> [Další](configuring-the-data-access-layer-s-connection-and-command-level-settings-vb.md)

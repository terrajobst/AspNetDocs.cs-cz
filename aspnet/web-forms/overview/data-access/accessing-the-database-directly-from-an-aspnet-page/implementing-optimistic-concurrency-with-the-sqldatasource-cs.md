---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/implementing-optimistic-concurrency-with-the-sqldatasource-cs
title: Implementace optimistického řízení souběžnosti pomocí SqlDataSourceC#() | Microsoft Docs
author: rick-anderson
description: V tomto kurzu si projdeme základy optimistického řízení souběžnosti a potom si Prozkoumejte, jak ho implementovat pomocí ovládacího prvku SqlDataSource.
ms.author: riande
ms.date: 02/20/2007
ms.assetid: df999966-ac48-460e-b82b-4877a57d6ab9
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/implementing-optimistic-concurrency-with-the-sqldatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: 87fca52e2e8be844411b2fff8382c6002eccbe09
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78553233"
---
# <a name="implementing-optimistic-concurrency-with-the-sqldatasource-c"></a>Implementace optimistického řízení souběžnosti ovládacím prvkem SqlDataSource (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_50_CS.exe) nebo [Stáhnout PDF](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/datatutorial50cs1.pdf)

> V tomto kurzu si projdeme základy optimistického řízení souběžnosti a potom si Prozkoumejte, jak ho implementovat pomocí ovládacího prvku SqlDataSource.

## <a name="introduction"></a>Úvod

V předchozím kurzu jsme prozkoumali, jak přidat do ovládacího prvku SqlDataSource možnosti vkládání, aktualizace a odstraňování. V krátkém případě je potřeba zadat odpovídající funkce `INSERT`, `UPDATE`nebo `DELETE` jazyka SQL ve vlastnostech ovládacího prvku `InsertCommand`, `UpdateCommand`nebo `DeleteCommand`, společně s příslušnými parametry v `InsertParameters`, `UpdateParameters`a `DeleteParameters` kolekcích. I když lze tyto vlastnosti a kolekce zadat ručně, tlačítko Konfigurovat Průvodce konfigurací zdroje dat nabízí zaškrtávací políčko Generovat `INSERT`, `UPDATE`a `DELETE`, které automaticky vytvoří tyto příkazy na základě příkazu `SELECT`.

Společně s zaškrtnutím políčka Generovat `INSERT`, `UPDATE`a `DELETE` se zobrazí dialogové okno Pokročilé možnosti generování SQL, které obsahuje možnost použití optimistického řízení souběžnosti (viz obrázek 1). Pokud je zaškrtnuto, klauzule `WHERE` v automaticky vygenerovaných `UPDATE` a `DELETE` příkazy se upraví tak, aby se prováděly pouze aktualizace, nebo odstranění, pokud se podkladová data databáze nezměnila, protože uživatel data naposledy načetl do mřížky.

![Můžete přidat podporu optimistického řízení souběžnosti z dialogového okna Upřesnit možnosti generování SQL.](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image1.gif)

**Obrázek 1**: z dialogového okna Upřesnit možnosti generování SQL můžete přidat podporu optimistického řízení souběžnosti.

Zpátky v [implementaci optimistického kurzu pro souběžnost](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs.md) jsme prozkoumali základy optimistického řízení souběžnosti a způsob, jak ho přidat do prvku ObjectDataSource. V tomto kurzu se podíváme na základy optimistického řízení souběžnosti a potom si Prozkoumejte, jak ho implementovat pomocí SqlDataSource.

## <a name="a-recap-of-optimistic-concurrency"></a>Rekapitulace optimistické souběžnosti

U webových aplikací, které umožňují více souběžným uživatelům upravovat nebo odstraňovat stejná data, existuje možnost, že jeden uživatel může omylem přepsat další změny. V kurzu [implementace optimistického řízení souběžnosti](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs.md) jsem zadali následující příklad:

Představte si, že dva uživatelé, Jisun a Sam, navštívili stránku v aplikaci, která umožňuje návštěvníkům aktualizovat a odstraňovat produkty prostřednictvím ovládacího prvku GridView. Klikněte na tlačítko Upravit pro příkaz Chai přibližně po stejnou dobu. Jisun změní název produktu na Chai čaj a klikne na tlačítko Aktualizovat. Čistým výsledkem je příkaz `UPDATE`, který se pošle do databáze, která nastaví *všechna* pole, která lze aktualizovat, a to i v případě, že Jisun aktualizuje jenom jedno pole `ProductName`). V tomto okamžiku má databáze hodnoty Chai čaj, kategorie nápoje, exotické kapaliny dodavatele a tak dále pro tento konkrétní produkt. Na obrazovce GridView v Sam s se však stále zobrazuje název produktu v upravitelném řádku GridView jako Chai. Za několik sekund po potvrzení změn Jisun se Sam aktualizuje kategorie na koření a klikne na aktualizovat. Výsledkem je příkaz `UPDATE` odeslaný do databáze, která nastaví název produktu na Chai, `CategoryID` na odpovídající ID kategorie koření, a tak dále. Změny názvu produktu Jisun s byly přepsány.

Tato interakce je znázorněna na obrázku 2.

[![, když dva uživatelé současně aktualizují záznam, u kterých se může změnit jeden uživatel a přepsat ostatní s.](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image2.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image1.png)

**Obrázek 2**: když dva uživatelé současně aktualizují záznam, který je potenciální pro změny jednoho uživatele, aby přepsal ostatní s ([kliknutím zobrazíte obrázek v plné velikosti](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image2.png))

Chcete-li zabránit tomuto scénáři v odložení, musí být implementována forma [řízení souběžnosti](http://en.wikipedia.org/wiki/Concurrency_control) . [Optimistická souběžnost](http://en.wikipedia.org/wiki/Optimistic_concurrency_control) v tomto kurzu pracuje na předpokladu, že v současné době může dojít ke konfliktům souběžnosti, a to v případě, že dojde k neúspěšnému výskytu takových konfliktů. Proto pokud dojde ke konfliktu, optimistické řízení souběžnosti jednoduše informuje uživatele o tom, že je možné uložit změny, protože stejná data změnil jiný uživatel.

> [!NOTE]
> U aplikací, kde se předpokládá, že dojde ke konfliktu souběžnosti, nebo pokud tyto konflikty nejsou přípustné, lze místo toho použít pesimistické řízení souběžnosti. Přečtěte si kurz [implementace optimistického řízení souběžnosti](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs.md) pro podrobnější diskuzi o pesimistické kontrole souběžnosti.

Optimistické řízení souběžnosti funguje tak, že zajistí, že záznam, který má být aktualizován nebo odstraněn, má stejné hodnoty jako při zahájení procesu aktualizace nebo odstranění. Například když kliknete na tlačítko Upravit ve upravitelném prvku GridView, hodnoty záznamu s se čtou z databáze a zobrazují se v textových polích a dalších webových ovládacích prvcích. Tyto původní hodnoty jsou uloženy v prvku GridView. Později poté, co uživatel provede změny a klikne na tlačítko Aktualizovat, musí použitý příkaz `UPDATE` vzít v úvahu původní hodnoty a nové hodnoty a aktualizovat pouze podkladový záznam databáze pouze v případě, že původní hodnoty, které uživatel začal upravovat, jsou shodné s hodnotami stále v databázi. Obrázek 3 znázorňuje tuto posloupnost událostí.

[![aby se aktualizace nebo odstranění zdařily, měly by se původní hodnoty rovnat aktuálním hodnotám databáze.](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image3.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image3.png)

**Obrázek 3**: aby byla aktualizace nebo odstranění úspěšná, původní hodnoty se musí rovnat aktuálním hodnotám databáze ([kliknutím zobrazíte obrázek v plné velikosti).](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image4.png)

Existují různé přístupy k implementaci optimistického řízení souběžnosti (viz [Petra a. Bromberg](http://www.eggheadcafe.com/articles/pbrombergresume.asp) [optimistická logika souběžného zpracování](http://www.eggheadcafe.com/articles/20050719.asp) pro Stručný pohled na řadu možností). Technika, kterou používá třída SqlDataSource (stejně jako datové sady ADO.NET typu používané v naší vrstvě přístupu k datům) rozšiřuje klauzuli `WHERE`, aby zahrnovala porovnání všech původních hodnot. Následující příkaz `UPDATE` například aktualizuje název a cenu produktu pouze v případě, že aktuální hodnoty databáze jsou rovny hodnotám, které byly původně načteny při aktualizaci záznamu v prvku GridView. Parametry `@ProductName` a `@UnitPrice` obsahují nové hodnoty zadané uživatelem, zatímco `@original_ProductName` a `@original_UnitPrice` obsahují hodnoty, které byly původně načteny do prvku GridView při kliknutí na tlačítko pro úpravy:

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample1.sql)]

Jak je uvedeno v tomto kurzu, povolení optimistického řízení souběžnosti se sadou SqlDataSource je stejně jednoduché jako zaškrtnutí políčka.

## <a name="step-1-creating-a-sqldatasource-that-supports-optimistic-concurrency"></a>Krok 1: vytvoření SqlDataSource podporující optimistické řízení souběžnosti

Začněte tím, že otevřete stránku `OptimisticConcurrency.aspx` ze složky `SqlDataSource`. Přetáhněte ovládací prvek SqlDataSource ze sady nástrojů do návrháře, nastavení vlastnosti `ID` na `ProductsDataSourceWithOptimisticConcurrency`. Potom klikněte na odkaz konfigurace zdroje dat z inteligentní značky Control s. Na první obrazovce průvodce vyberte možnost pracovat s `NORTHWINDConnectionString` a klikněte na tlačítko Další.

[![se rozhodnout, jak pracovat s NORTHWINDConnectionString](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image4.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image5.png)

**Obrázek 4**: volba pro práci s `NORTHWINDConnectionString`m ([kliknutím zobrazíte obrázek v plné velikosti](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image6.png))

V tomto příkladu přidáme prvek GridView, který umožní uživatelům upravovat `Products` tabulku. Proto z obrazovky konfigurace příkazu SELECT vyberte v rozevíracím seznamu tabulku `Products` a vyberte sloupce `ProductID`, `ProductName`, `UnitPrice`a `Discontinued`, jak je znázorněno na obrázku 5.

[![z tabulky Products vrátí sloupce ProductID, ProductName, UnitPrice a vyřazeno.](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image5.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image7.png)

**Obrázek 5**: v tabulce `Products` vrátíte sloupce `ProductID`, `ProductName`, `UnitPrice`a `Discontinued` ([kliknutím zobrazíte obrázek v plné velikosti).](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image8.png)

Po výběru sloupců klikněte na tlačítko Upřesnit a zobrazte tak dialogové okno Upřesnit možnosti generování kódu SQL. Zaškrtněte příkazy generovat `INSERT`, `UPDATE`a `DELETE` a použijte políčka Optimistická souběžnost a klikněte na tlačítko OK (pro snímek obrazovky přejděte zpět na obrázek 1). Dokončete průvodce kliknutím na tlačítko Další a potom na Dokončit.

Po dokončení Průvodce konfigurací zdroje dat si Projděte výsledný `DeleteCommand` a `UpdateCommand` vlastnosti a kolekce `DeleteParameters` a `UpdateParameters`. Nejjednodušší způsob, jak to provést, je kliknout na kartu zdroj v levém dolním rohu, aby se zobrazila deklarativní syntaxe stránky. Vyhledá se `UpdateCommand` hodnota:

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample2.sql)]

Se sedmi parametry v kolekci `UpdateParameters`:

[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample3.aspx)]

Podobně `DeleteCommand` vlastnost a kolekce `DeleteParameters` by měly vypadat takto:

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample4.sql)]

[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample5.aspx)]

Kromě rozšíření `WHERE`ch klauzulí vlastností `UpdateCommand` a `DeleteCommand` (a přidání dalších parametrů do odpovídajících kolekcí parametrů), výběrem možnosti použít optimistickou souběžnost upraví dvě další vlastnosti:

- Změní [vlastnost`ConflictDetection`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.conflictdetection.aspx) z `OverwriteChanges` (výchozí) na `CompareAllValues`
- Změní [vlastnost`OldValuesParameterFormatString`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.oldvaluesparameterformatstring.aspx) z {0} (výchozí) na původní\_{0}.

Když webová ovládací prvek data vyvolá metodu SqlDataSource s `Update()` nebo `Delete()`, projde původními hodnotami. Je-li vlastnost `ConflictDetection` SqlDataSource nastavena na hodnotu `CompareAllValues`, jsou tyto původní hodnoty přidány do příkazu. Vlastnost `OldValuesParameterFormatString` poskytuje vzor pro pojmenování, který se používá pro tyto původní hodnoty parametrů. Průvodce konfigurací zdroje dat používá původní\_{0} a odpovídajícím způsobem pojmenuje všechny původní parametry v `UpdateCommand` a `DeleteCommand` vlastnosti a `UpdateParameters` a `DeleteParameters` kolekcí.

> [!NOTE]
> Vzhledem k tomu, že nepoužíváme možnosti vložení ovládacího prvku SqlDataSource, můžete odebrat vlastnost `InsertCommand` a její `InsertParameters` kolekci.

## <a name="correctly-handlingnullvalues"></a>Správné zpracování hodnot`NULL`

Nicméně rozšířené `UPDATE` a `DELETE` příkazy automaticky generované průvodcem konfigurovat zdroj dat při použití optimistické souběžnosti *nefungují se* záznamy, které obsahují `NULL` hodnoty. Chcete-li zjistit, proč, zvažte naši `UpdateCommand`SqlDataSource:

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample6.sql)]

`UnitPrice` sloupec v tabulce `Products` může mít `NULL` hodnoty. Pokud má konkrétní záznam `NULL` hodnotu pro `UnitPrice`, `WHERE` část klauzule `[UnitPrice] = @original_UnitPrice` se *vždycky* vyhodnotí jako false, protože `NULL = NULL` vždycky vrátí hodnotu false. Záznamy obsahující `NULL` hodnoty proto nelze upravovat ani odstraňovat, protože příkazy `UPDATE` a `DELETE` `WHERE` klauzule nevrátí žádné řádky, které by se měly aktualizovat nebo odstranit.

> [!NOTE]
> Tato chyba byla poprvé oznámena společností Microsoft v červnu 2004 ve [třídě SqlDataSource generuje nesprávné příkazy SQL](https://connect.microsoft.com/VisualStudio/feedback/ViewFeedback.aspx?FeedbackID=93937) a je naplánovaná tak, aby byla opravena v další verzi ASP.NET.

Chcete-li tento problém vyřešit, je nutné ručně aktualizovat klauzule `WHERE` ve vlastnostech `UpdateCommand` a `DeleteCommand` pro **všechny** sloupce, které mohou mít hodnoty `NULL`. V obecném případě změňte `[ColumnName] = @original_ColumnName` na:

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample7.sql)]

Tuto úpravu lze provést přímo prostřednictvím deklarativní značky, prostřednictvím možností UpdateQuery nebo DeleteQuery z okno Vlastnosti, nebo prostřednictvím karet UPDATE a DELETE v příkazu zadat vlastní příkaz SQL nebo v možnosti uložená procedura v části Konfigurace dat. Průvodce zdrojem Tuto změnu je třeba provést pro *všechny* sloupce v klauzuli `UpdateCommand` a `DeleteCommand` s `WHERE`, které mohou obsahovat hodnoty `NULL`.

Použití tohoto příkladu v našem příkladu vede k následujícím upraveným `UpdateCommand` a `DeleteCommand`m hodnotám:

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample8.sql)]

## <a name="step-2-adding-a-gridview-with-edit-and-delete-options"></a>Krok 2: Přidání prvku GridView s možnostmi Upravit a odstranit

U prvku SqlDataSource nakonfigurovaného pro podporu optimistické souběžnosti je vše k disměně pro přidání webového ovládacího prvku pro datovou stránku, který využívá toto řízení souběžnosti. Pro tento kurz přidejte ovládací prvek GridView, který poskytuje funkce úprav i odstranění. Chcete-li toho dosáhnout, přetáhněte prvek GridView z panelu nástrojů do návrháře a nastavte jeho `ID` na `Products`. Z inteligentní značky GridView s, navažte ji k ovládacímu prvku `ProductsDataSourceWithOptimisticConcurrency` SqlDataSource přidanému v kroku 1. Nakonec zaškrtněte možnosti Povolit úpravy a povolit odstraňování z inteligentní značky.

[![vytvořit vazby prvku GridView ke třídě SqlDataSource a povolit úpravy a odstranění](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image6.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image9.png)

**Obrázek 6**: vazba prvku GridView ke třídě SqlDataSource a povolení úprav a odstranění ([kliknutím zobrazíte obrázek v plné velikosti](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image10.png))

Po přidání prvku GridView nakonfigurujte jeho vzhled tak, že odeberete `ProductID` vlastnost BoundField, změníte vlastnost `ProductName` vlastnost BoundField s `HeaderText` na produkt a aktualizujete `UnitPrice` vlastnost BoundField tak, aby jeho `HeaderText`ová vlastnost byla jednoduše Price. V ideálním případě jsme vylepšili rozhraní pro úpravy, aby zahrnovalo RequiredFieldValidator hodnotu `ProductName` a CompareValidator pro hodnotu `UnitPrice` (aby se zajistilo, že je správně naformátovaná číselná hodnota). Podrobnější informace o přizpůsobení rozhraní pro úpravy prvku GridView naleznete v kurzu [přizpůsobení rozhraní pro úpravu dat](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md) .

> [!NOTE]
> Stav zobrazení GridView s musí být povolen, protože původní hodnoty předané z prvku GridView do SqlDataSource jsou uloženy ve stavu zobrazení.

Po provedení těchto úprav prvku GridView by deklarativní označení GridView a SqlDataSource mělo vypadat podobně jako následující:

[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample9.aspx)]

Chcete-li zobrazit optimistické řízení souběžnosti v akci, otevřete dvě okna prohlížeče a načtěte `OptimisticConcurrency.aspx` stránku v obou. Klikněte na tlačítka pro úpravy prvního produktu v obou prohlížečích. V jednom prohlížeči změňte název produktu a klikněte na aktualizovat. Prohlížeč odešle zpět a GridView se vrátí do režimu před úpravou, který zobrazuje nový název produktu pro záznam, který je právě upravován.

V druhém okně prohlížeče změňte cenu (ale ponechte název produktu jako původní hodnotu) a klikněte na aktualizovat. Při zpětném volání se mřížka vrátí do režimu před úpravou, ale změna ceny se nezaznamená. Druhý prohlížeč zobrazí stejnou hodnotu jako první název nového produktu se starou cenou. Změny provedené v druhém okně prohlížeče byly ztraceny. Kromě toho se změny ztratily spíše, protože nebyla žádná výjimka nebo zpráva oznamující, že došlo k narušení souběžnosti.

[![změny v druhém okně prohlížeče byly Tichy ztraceny](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image7.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image11.png)

**Obrázek 7**: změny ve druhém okně prohlížeče byly tiše ztraceny ([kliknutím zobrazíte obrázek v plné velikosti).](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image12.png)

Důvod, proč změny v druhém prohlížeči nebyly potvrzeny, protože klauzule `UPDATE` s `WHERE` vyfiltroval všechny záznamy, a proto neovlivnila žádné řádky. Pojďme se podívat na příkaz `UPDATE` znovu:

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample10.sql)]

Když druhé okno prohlížeče aktualizuje záznam, původní název produktu zadaný v klauzuli `WHERE` nesouhlasí s existujícím názvem produktu (protože byl změněn prvním prohlížečem). Proto příkaz `[ProductName] = @original_ProductName` vrátí hodnotu false a `UPDATE` nemá vliv na žádné záznamy.

> [!NOTE]
> Odstranění funguje stejným způsobem. Se dvěma otevřenými okny prohlížeče začněte úpravou daného produktu s použitím jednoho a uložením změn. Po uložení změn v jednom prohlížeči klikněte na tlačítko Odstranit pro stejný produkt v druhé. Vzhledem k tomu, že se původní hodnoty neshodují v klauzuli `DELETE` příkazu s `WHERE`, odstranění se v tichém režimu nezdařilo.

V perspektivě koncového uživatele v druhém okně prohlížeče po kliknutí na tlačítko Aktualizovat se mřížka vrátí do režimu před úpravami, ale jejich změny byly ztraceny. Neexistuje ale žádná vizuální zpětná vazba, na kterou se změny nezměnily. V ideálním případě platí, že pokud dojde ke ztrátě změn uživatelů v důsledku porušení souběžnosti, informujte je, že je to třeba, aby byla mřížka v režimu úprav. Pojďme se podívat, jak to provést.

## <a name="step-3-determining-when-a-concurrency-violation-has-occurred"></a>Krok 3: určení, kdy došlo k narušení souběžnosti

Vzhledem k tomu, že porušení souběžnosti odmítne změny provedené v souběžnosti, by bylo skvělé upozornit uživatele, když došlo k narušení souběžnosti. Chcete-li uživatele upozornit, přidejte ovládací prvek web Label na začátek stránky s názvem `ConcurrencyViolationMessage`, jehož vlastnost `Text` zobrazí následující zprávu: Pokusili jste se aktualizovat nebo odstranit záznam, který byl současně aktualizován jiným uživatelem. Zkontrolujte změny provedené ostatními uživateli a znovu proveďte aktualizaci nebo odstranění. Nastavte vlastnost popisku `CssClass` ovládacího prvku na hodnotu Warning, což je Třída CSS definovaná v `Styles.css`, která zobrazuje text červeně, kurzívou, tučně a velkým písmem. Nakonec nastavte vlastnosti Label `Visible` a `EnableViewState` na `false`. Tato operace skryje popisek s výjimkou těch, u kterých jsme explicitně nastavili vlastnost `Visible` na hodnotu `true`.

[![přidání ovládacího prvku popisek na stránku, aby se zobrazilo upozornění](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image8.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image13.png)

**Obrázek 8**: Přidání ovládacího prvku popisek na stránku, aby se zobrazilo upozornění ([kliknutím zobrazíte obrázek v plné velikosti](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image14.png))

Při provádění rutiny Update nebo DELETE se ovládací prvky GridView s `RowUpdated` a `RowDeleted` aktivují poté, co ovládací prvek zdroje dat provede požadovanou aktualizaci nebo odstranění. Můžeme určit, kolik řádků bylo ovlivněno operací z těchto obslužných rutin událostí. Pokud jste ovlivnili nulové řádky, chceme zobrazit `ConcurrencyViolationMessage` popisku.

Vytvořte obslužnou rutinu události pro události `RowUpdated` i `RowDeleted` a přidejte následující kód:

[!code-csharp[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample11.cs)]

V obou obslužných rutinách událostí kontrolujeme vlastnost `e.AffectedRows` a pokud se rovná 0, nastavte vlastnost `ConcurrencyViolationMessage` popisek s `Visible` na `true`. V obslužné rutině události `RowUpdated` také instruujte ovládací prvek GridView, aby zůstal v režimu úprav nastavením vlastnosti `KeepInEditMode` na hodnotu true. V takovém případě musíme data znovu navazovat do mřížky, aby se data ostatních uživatelů načetla do rozhraní pro úpravy. Toho lze dosáhnout voláním metody `DataBind()` GridView.

Jak ukazuje obrázek 9, u těchto dvou obslužných rutin událostí se zobrazí velmi znatelné zpráva, kdykoli dojde k porušení souběžnosti.

[![se zpráva zobrazí na ploše narušení souběžnosti](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image9.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image15.png)

**Obrázek 9**: zpráva se zobrazí na ploše narušení souběžnosti ([kliknutím zobrazíte obrázek v plné velikosti).](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image16.png)

## <a name="summary"></a>Souhrn

Při vytváření webové aplikace, kde více souběžných uživatelů může upravovat stejná data, je důležité zvážit možnosti řízení souběžnosti. Ve výchozím nastavení webové ovládací prvky dat ASP.NET a ovládací prvky zdroje dat nevyužívají žádné řízení souběžnosti. Jak jsme viděli v tomto kurzu, implementace optimistického řízení souběžnosti se sadou SqlDataSource je relativně rychlá a jednoduchá. Třída SqlDataSource zpracovává většinu samotnému pro přidání rozšířených `WHERE` klauzulí do automaticky generovaných příkazů `UPDATE` a `DELETE`, ale existuje několik odlišností ve zpracování `NULL` hodnotových sloupců, jak je popsáno v části správné zpracování `NULL`ch hodnot.

V tomto kurzu se uzavře naše prohlídka na třídě SqlDataSource. Naše zbývající kurzy se vrátí k práci s daty pomocí architektury ObjectDataSource a vrstvené architektury.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

> [!div class="step-by-step"]
> [Předchozí](inserting-updating-and-deleting-data-with-the-sqldatasource-cs.md)
> [Další](querying-data-with-the-sqldatasource-control-vb.md)

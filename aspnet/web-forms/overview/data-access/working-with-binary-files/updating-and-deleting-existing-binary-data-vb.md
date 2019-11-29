---
uid: web-forms/overview/data-access/working-with-binary-files/updating-and-deleting-existing-binary-data-vb
title: Aktualizace a odstranění stávajících binárních dat (VB) | Microsoft Docs
author: rick-anderson
description: V předchozích kurzech jsme viděli, jak ovládací prvek GridView usnadňuje úpravy a odstraňování textových dat. V tomto kurzu uvidíme i to, jak se vytvoří ovládací prvek GridView...
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 3a052ced-9cf5-47b8-a400-934f0b687c26
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/updating-and-deleting-existing-binary-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 27ff6941008b4e7bf6d632e4c248fd1d35fb3589
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621594"
---
# <a name="updating-and-deleting-existing-binary-data-vb"></a>Aktualizace a odstranění stávajících binárních dat (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_57_VB.exe) nebo [Stáhnout PDF](updating-and-deleting-existing-binary-data-vb/_static/datatutorial57vb1.pdf)

> V předchozích kurzech jsme viděli, jak ovládací prvek GridView usnadňuje úpravy a odstraňování textových dat. V tomto kurzu se zobrazuje, jak ovládací prvek GridView umožňuje upravovat a odstraňovat binární data, ať už jsou tato binární data uložená v databázi nebo uložená v systému souborů.

## <a name="introduction"></a>Úvod

V posledních třech kurzech jsme připravujeme poměrně funkční funkčnost pro práci s binárními daty. Začali jsme tím, že do tabulky `Categories` přidáte sloupec `BrochurePath` a odpovídajícím způsobem aktualizujete architekturu. Přidali jsme také metody vrstvy přístupu k datům a obchodní logiky, které vám umožní pracovat s existujícím sloupcem `Picture` v tabulce categories, který obsahuje binární obsah s obrázkem souboru. Vytvořili jsme webové stránky, které prezentují binární data v prvku GridView a odkaz na stažení pro tuto brožuru, s obrázkem kategorie s zobrazeným v prvku `<img>` a Přidali jste prvek DetailsView, který uživatelům umožňuje přidat novou kategorii a nahrát data brožury a obrázku.

Vše, co zbývá k implementaci, je možnost upravit a odstranit existující kategorie, které v tomto kurzu provedeme pomocí integrovaných funkcí úprav a odstranění v prvku GridView. Při úpravě kategorie bude uživatel moci volitelně odeslat nový obrázek nebo nechat kategorii nadále používat stávající. V případě brožury si můžete zvolit, že se má použít stávající brožura, nahrát novou brožuru nebo označit, že k této kategorii už není přidružená brožura. Pojďme začít!

## <a name="step-1-updating-the-data-access-layer"></a>Krok 1: aktualizace vrstvy přístupu k datům

DAL má automaticky generované metody `Insert`, `Update`a `Delete`, ale tyto metody se vygenerovaly na základě hlavního dotazu `CategoriesTableAdapter` s, který nezahrnuje sloupec `Picture`. Proto metody `Insert` a `Update` nezahrnují parametry pro zadání binárních dat pro obrázek kategorie s. Stejně jako v [předchozím kurzu](including-a-file-upload-option-when-adding-a-new-record-vb.md)potřebujeme vytvořit novou metodu TableAdapter pro aktualizaci tabulky `Categories` při zadávání binárních dat.

Otevřete typovou datovou sadu a v návrháři klikněte pravým tlačítkem myši na záhlaví `CategoriesTableAdapter` s a v místní nabídce vyberte možnost Přidat dotaz. spustí se Průvodce konfigurací dotazu TableAdapter. Tento průvodce se spustí tím, že požádáme, jak by měl dotaz TableAdapter získat přístup k databázi. Vyberte možnost použít příkazy jazyka SQL a klikněte na tlačítko Další. V dalším kroku se zobrazí výzva k zadání typu dotazu, který se má vygenerovat. Vzhledem k tomu, že jsme znovu vytvořili dotaz pro přidání nového záznamu do tabulky `Categories`, vyberte aktualizovat a klikněte na další.

[![vyberte možnost aktualizace.](updating-and-deleting-existing-binary-data-vb/_static/image2.png)](updating-and-deleting-existing-binary-data-vb/_static/image1.png)

**Obrázek 1**: vyberte možnost aktualizace ([kliknutím zobrazíte obrázek v plné velikosti](updating-and-deleting-existing-binary-data-vb/_static/image3.png)).

Teď je potřeba zadat příkaz `UPDATE` SQL. Průvodce automaticky navrhne `UPDATE` příkaz, který odpovídá hlavnímu dotazu TableAdapter s (jeden, který aktualizuje `CategoryName`, `Description`a hodnoty `BrochurePath`). Změňte příkaz tak, aby byl zahrnutý sloupec `Picture` společně s parametrem `@Picture`, například takto:

[!code-sql[Main](updating-and-deleting-existing-binary-data-vb/samples/sample1.sql)]

Poslední obrazovka průvodce vás požádá o pojmenování nové metody TableAdapter. Zadejte `UpdateWithPicture` a klikněte na Dokončit.

[![název novou metodu TableAdapter UpdateWithPicture](updating-and-deleting-existing-binary-data-vb/_static/image5.png)](updating-and-deleting-existing-binary-data-vb/_static/image4.png)

**Obrázek 2**: pojmenování nové metody TableAdapter `UpdateWithPicture` ([kliknutím zobrazíte obrázek v plné velikosti](updating-and-deleting-existing-binary-data-vb/_static/image6.png))

## <a name="step-2-adding-the-business-logic-layer-methods"></a>Krok 2: Přidání metod vrstvy obchodní logiky

Kromě aktualizace DAL potřebujeme aktualizovat knihoven BLL a zahrnout do nich metody aktualizace a odstranění kategorie. Jedná se o metody, které budou vyvolány z prezentační vrstvy.

Pro odstranění kategorie můžeme použít automaticky generovanou metodu `Delete` `CategoriesTableAdapter` s. Do `CategoriesBLL` třídy přidejte následující metodu:

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample2.vb)]

Pro účely tohoto kurzu vytvoříme dvě metody aktualizace kategorie – jeden, který očekává binární data obrázku, a vyvolá `UpdateWithPicture` metodu, kterou jsme právě přidali do `CategoriesTableAdapter` a další, která přijímá pouze hodnoty `CategoryName`, `Description`a `BrochurePath` a používá `CategoriesTableAdapter` příkaz automaticky generovaný `Update` třídy. Účelem použití dvou metod je, že v některých případech může uživatel chtít aktualizovat obrázek kategorií spolu s ostatními poli. v takovém případě bude muset uživatel nahrát nový obrázek. Nahraná binární data s obrázkem se pak dají použít v příkazu `UPDATE`. V jiných případech může uživatel zajímat pouze aktualizaci, název a popis. Pokud ale příkaz `UPDATE` očekává i binární data pro `Picture` sloupec, je potřeba tyto informace také poskytnout. To by vyžadovalo další cestu k databázi, aby se vrátila data obrázku pro Upravovaný záznam. Proto chceme, aby byly k dis`UPDATE` dvě metody. Vrstva obchodní logiky určí, která z nich se má použít v závislosti na tom, zda jsou při aktualizaci kategorie k dispozici data obrázku.

Chcete-li to usnadnit, přidejte dvě metody do třídy `CategoriesBLL`, jak s názvem `UpdateCategory`. První z nich by měl přijmout tři `String` s, `Byte` pole a `Integer` jako vstupní parametry; druhý, jenom tři `String` s a `Integer`. Vstupní parametry `String` pro kategorie s názvem, popisem a cestou k souboru brožury jsou `Byte` poli pro binární obsah obrázku kategorie s a `Integer` identifikuje `CategoryID` záznamu, který se má aktualizovat. Všimněte si, že první přetížení vyvolá sekundu, pokud je předané `Byte` pole `Nothing`:

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample3.vb)]

## <a name="step-3-copying-over-the-insert-and-view-functionality"></a>Krok 3: kopírování přes funkce INSERT a View

V [předchozím kurzu](including-a-file-upload-option-when-adding-a-new-record-vb.md) jsme vytvořili stránku s názvem `UploadInDetailsView.aspx`, která uvádí všechny kategorie v prvku GridView a poskytla prvek DetailsView, který do systému přidá nové kategorie. V tomto kurzu rozšíříme prvek GridView, aby zahrnoval úpravy a odstraňování podpory. Místo toho, abyste pokračovali v práci z `UploadInDetailsView.aspx`, místo toho použijte místo toho tento kurz s na `UpdatingAndDeleting.aspx` stránce ze stejné složky `~/BinaryData`. Zkopírujte a vložte deklarativní značky a kód z `UploadInDetailsView.aspx` do `UpdatingAndDeleting.aspx`.

Začněte tím, že otevřete stránku `UploadInDetailsView.aspx`. Zkopírujte všechny deklarativní syntaxe v rámci elementu `<asp:Content>`, jak je znázorněno na obrázku 3. Dále otevřete `UpdatingAndDeleting.aspx` a vložte tento kód do jeho `<asp:Content>` elementu. Podobně zkopírujte kód ze třídy `UploadInDetailsView.aspx` stránky s kódem na pozadí do `UpdatingAndDeleting.aspx`.

[![zkopírovat deklarativní označení z UploadInDetailsView. aspx](updating-and-deleting-existing-binary-data-vb/_static/image8.png)](updating-and-deleting-existing-binary-data-vb/_static/image7.png)

**Obrázek 3**: zkopírování deklarativní značky z `UploadInDetailsView.aspx` ([kliknutím zobrazíte obrázek v plné velikosti](updating-and-deleting-existing-binary-data-vb/_static/image9.png))

Po zkopírování deklarativních značek a kódu, navštivte `UpdatingAndDeleting.aspx`. Měli byste vidět stejný výstup a mít stejné uživatelské prostředí jako s `UploadInDetailsView.aspx` stránkou z předchozího kurzu.

## <a name="step-4-adding-deleting-support-to-the-objectdatasource-and-gridview"></a>Krok 4: Přidání podpory odstraňování do ObjectDataSource a GridView

Jak jsme probrali zpět v článku [Přehled vložení, aktualizace a odstranění dat](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) , prvek GridView nabízí integrované možnosti odstraňování a tyto možnosti je možné povolit na zaškrtnutí zaškrtávacího políčka, pokud je v podkladovém zdroji dat mřížky, který podporuje odstranění. V současné době prvek ObjectDataSource, na který je svázán prvek GridView (`CategoriesDataSource`), nepodporuje odstranění.

Chcete-li tento problém vyřešit, spusťte průvodce kliknutím na možnost Konfigurovat zdroj dat z inteligentní značky ObjectDataSource s. První obrazovka ukazuje, že prvek ObjectDataSource je nakonfigurován pro práci s třídou `CategoriesBLL`. Stiskněte tlačítko Další. V současné době jsou zadány pouze prvky ObjectDataSource `InsertMethod` a vlastnosti `SelectMethod`. Průvodce si ale automaticky vyplní rozevírací seznamy na kartách aktualizace a odstranění pomocí `UpdateCategory` a `DeleteCategory`ch metod, v uvedeném pořadí. Důvodem je to, že ve třídě `CategoriesBLL` jsme tyto metody označili pomocí `DataObjectMethodAttribute` jako výchozí metody pro aktualizaci a odstranění.

Prozatím nastavte rozevírací seznam karta pro aktualizaci na hodnotu (žádné), ale nechte rozevírací seznam odstranit kartu s nastavenou na `DeleteCategory`. Do tohoto průvodce se vrátíme v kroku 6 a přidejte podporu aktualizace.

[![nakonfigurovat prvek ObjectDataSource na použití metody DeleteCategory](updating-and-deleting-existing-binary-data-vb/_static/image11.png)](updating-and-deleting-existing-binary-data-vb/_static/image10.png)

**Obrázek 4**: Konfigurace prvku ObjectDataSource pro použití metody `DeleteCategory` ([kliknutím zobrazíte obrázek v plné velikosti](updating-and-deleting-existing-binary-data-vb/_static/image12.png))

> [!NOTE]
> Po dokončení průvodce může Visual Studio požádat, zda chcete aktualizovat pole a klíče, čímž dojde k opětovnému vygenerování polí webové ovládací prvky dat. Zvolte možnost Ne, protože výběrem možnosti Ano dojde k přepsání všech úprav polí, které jste mohli udělat.

Prvek ObjectDataSource nyní bude obsahovat hodnotu vlastnosti `DeleteMethod` a také `DeleteParameter`. Pokud použijete průvodce k určení metod, sada Visual Studio nastaví vlastnost ObjectDataSource `OldValuesParameterFormatString` na `original_{0}`, což způsobí problémy s voláními metody Update a DELETE. Proto buď úplně vymažte tuto vlastnost, nebo ji resetujte na výchozí `{0}`. Pokud potřebujete aktualizovat paměť v této vlastnosti ObjectDataSource, přečtěte si kurz [vkládání, aktualizace a odstraňování dat](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md) .

Po dokončení průvodce a opravě `OldValuesParameterFormatString`by deklarativní označení ObjectDataSource s mělo vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](updating-and-deleting-existing-binary-data-vb/samples/sample4.aspx)]

Po nakonfigurování prvku ObjectDataSource přidejte možnosti odstranění do prvku GridView zaškrtnutím políčka Povolit odstranění z inteligentní značky GridView. Tím se přidá CommandField do prvku GridView, jehož vlastnost `ShowDeleteButton` je nastavena na hodnotu `True`.

[![povolit podporu odstraňování v prvku GridView.](updating-and-deleting-existing-binary-data-vb/_static/image14.png)](updating-and-deleting-existing-binary-data-vb/_static/image13.png)

**Obrázek 5**: povolení podpory odstraňování v prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](updating-and-deleting-existing-binary-data-vb/_static/image15.png))

Vyzkoušení funkce odstranění chvíli počkejte. Existuje cizí klíč mezi `Products` tabulkou `CategoryID` a `Categories` `CategoryID`tabulek, takže při pokusu o odstranění některé z prvních osmi kategorií se zobrazí výjimka porušení omezení cizího klíče. Pokud chcete tuto funkci otestovat, přidejte novou kategorii, která bude poskytovat brožuru i obrázek. Kategorie můj test zobrazená na obrázku 6 obsahuje soubor zkušební brožury s názvem `Test.pdf` a testovací obrázek. Obrázek 7 ukazuje prvek GridView po přidání kategorie testu.

[![přidat kategorii testu s brožurou a obrázkem](updating-and-deleting-existing-binary-data-vb/_static/image17.png)](updating-and-deleting-existing-binary-data-vb/_static/image16.png)

**Obrázek 6**: Přidání kategorie testu s brožurou a obrázkem ([kliknutím zobrazíte obrázek v plné velikosti](updating-and-deleting-existing-binary-data-vb/_static/image18.png))

[![po vložení kategorie testu se zobrazí v prvku GridView.](updating-and-deleting-existing-binary-data-vb/_static/image20.png)](updating-and-deleting-existing-binary-data-vb/_static/image19.png)

**Obrázek 7**: po vložení kategorie testu se zobrazí v prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](updating-and-deleting-existing-binary-data-vb/_static/image21.png)).

V aplikaci Visual Studio aktualizujte Průzkumník řešení. Teď by se měl zobrazit nový soubor ve složce `~/Brochures` `Test.pdf` (viz obrázek 8).

V dalším kroku klikněte na odkaz odstranit v řádku kategorie testu, což způsobí, že se stránka vystavuje jako postback a metoda `CategoriesBLL` třídy s `DeleteCategory`, která se má aktivovat. Tím dojde k vyvolání metody `Delete` DAL s, což způsobí, že se do databáze pošle příslušný příkaz `DELETE`. Data jsou pak znovu svázána s ovládacím prvek GridView a kód je odeslán zpět klientovi pomocí kategorie testu již není k dispozici.

I když pracovní postup odstranění úspěšně odebral záznam kategorie testu z `Categories` tabulky, neodebral se jeho soubor brožury ze systému souborů webového serveru s. Aktualizujte Průzkumník řešení a uvidíte, že `Test.pdf` stále sedí ve složce `~/Brochures`.

![Soubor test. PDF se neodstranil ze systému souborů webového serveru s.](updating-and-deleting-existing-binary-data-vb/_static/image1.gif)

**Obrázek 8**: soubor `Test.pdf` nebyl odstraněn ze systému souborů webového serveru s

## <a name="step-5-removing-the-deleted-category-s-brochure-file"></a>Krok 5: odebrání odstraněných souborů brožury s kategorií

Jedním z downsides ukládání binárních dat externích do databáze je, že je nutné provést další kroky k vyčištění těchto souborů při odstranění přidruženého záznamu databáze. GridView a ObjectDataSource poskytují události, které se aktivují před a po provedení příkazu DELETE. Ve skutečnosti je potřeba vytvořit obslužné rutiny událostí pro události před a po akci. Předtím, než se odstraní záznam `Categories` musíme určit jeho cestu souboru PDF, ale nebudeme potřebovat odstranit PDF před odstraněním kategorie v případě, že dojde k výjimce a kategorie se neodstraní.

Událost GridView s [`RowDeleting`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleting.aspx) aktivuje před vyvoláním příkazu ObjectDataSource s, zatímco jeho [událost`RowDeleted`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowdeleted.aspx) je aktivována po. Vytvořte obslužné rutiny událostí pro tyto dvě události pomocí následujícího kódu:

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample5.vb)]

V obslužné rutině události `RowDeleting` je `CategoryID` odstraněného řádku převzat z kolekce GridView s `DataKeys`, ke které lze v této obslužné rutině události přistupovat prostřednictvím kolekce `e.Keys`. Dále je vyvolána `GetCategoryByCategoryID(categoryID)` třídy `CategoriesBLL`, která vrací informace o odstraněném záznamu. Pokud vrácený objekt `CategoriesDataRow` má hodnotu, která není`NULL``BrochurePath`, je uložen v proměnné stránky `deletedCategorysPdfPath` tak, že soubor lze odstranit v `RowDeleted` obslužné rutině události.

> [!NOTE]
> Místo načtení podrobností `BrochurePath` pro záznam `Categories`, který se odstraňuje v `RowDeleting` obslužné rutiny události, můžeme použít alternativu `BrochurePath` do vlastnosti `DataKeyNames` GridView. a k získání hodnoty Record s pomocí kolekce `e.Keys`. Tím by se mírně zvýšila velikost stavu zobrazení prvku GridView, ale došlo k omezení množství potřebného kódu a uložení cesty do databáze.

Po vyvolání podkladového příkazu k odstranění prvku ObjectDataSource s `RowDeleted` obslužná rutina události GridView. Pokud nedošlo k žádným výjimkám při odstraňování dat a existuje hodnota pro `deletedCategorysPdfPath`, soubor PDF se odstraní ze systému souborů. Všimněte si, že tento kód navíc není potřeba k vyčištění binárních dat kategorie s, která jsou přidružená k jeho obrázku. To vzhledem k tomu, že data obrázku jsou ukládána přímo v databázi, takže odstraněním řádku `Categories` dojde také k odstranění této kategorie dat obrázků.

Po přidání dvou obslužných rutin událostí spusťte tento testovací případ znovu. Při odstranění kategorie se odstraní také přidružený PDF.

Aktualizace stávajících binárních dat s daty přináší zajímavé problémy. Zbývající část tohoto kurzu se zahájí přidáním možností aktualizace do brožury a obrázku. Krok 6 zkoumá techniky pro aktualizaci informací o brožuře, zatímco krok 7 prohlíží při aktualizaci obrázku.

## <a name="step-6-updating-a-category-s-brochure"></a>Krok 6: aktualizace brožury s kategorií

Jak je popsáno v kurzu vložení, aktualizace a odstranění dat, prvek GridView nabízí integrovanou podporu pro úpravy na úrovni řádků, kterou lze implementovat zaškrtnutím zaškrtávacího políčka, pokud je příslušný zdroj dat vhodně nakonfigurován. V současné době není `CategoriesDataSource` prvek ObjectDataSource ještě nakonfigurovaný tak, aby zahrnoval podporu aktualizace, takže s tím přidávejte.

Klikněte na odkaz Konfigurovat zdroj dat z Průvodce ObjectDataSource s a pokračujte Druhým krokem. Z důvodu `DataObjectMethodAttribute` používaného v `CategoriesBLL`by se měl rozevírací seznam aktualizace automaticky naplnit `UpdateCategory` přetížení, které přijímá čtyři vstupní parametry (pro všechny sloupce, ale `Picture`). Změňte to tak, aby používalo přetížení s pěti parametry.

[![nakonfigurovat prvek ObjectDataSource tak, aby používal metodu UpdateCategory, která obsahuje parametr pro obrázek](updating-and-deleting-existing-binary-data-vb/_static/image23.png)](updating-and-deleting-existing-binary-data-vb/_static/image22.png)

**Obrázek 9**: Konfigurace prvku ObjectDataSource pro použití metody `UpdateCategory`, která obsahuje parametr pro `Picture` ([kliknutím zobrazíte obrázek v plné velikosti](updating-and-deleting-existing-binary-data-vb/_static/image24.png))

Prvek ObjectDataSource nyní bude obsahovat hodnotu pro jeho vlastnost `UpdateMethod` a také odpovídající `UpdateParameter` s. Jak je uvedeno v kroku 4, sada Visual Studio nastaví vlastnost ObjectDataSource s `OldValuesParameterFormatString` na `original_{0}` při použití průvodce Konfigurovat zdroj dat. Tato akce způsobí problémy s voláními metody Update a DELETE. Proto buď úplně vymažte tuto vlastnost, nebo ji resetujte na výchozí `{0}`.

Po dokončení průvodce a opravě `OldValuesParameterFormatString`by deklarativní označení ObjectDataSource s mělo vypadat takto:

[!code-aspx[Main](updating-and-deleting-existing-binary-data-vb/samples/sample6.aspx)]

Chcete-li zapnout integrované funkce úprav ovládacího prvku GridView, zaškrtněte možnost Povolit úpravy z inteligentní značky GridView. Tím se nastaví vlastnost CommandField s `ShowEditButton` na `True`a výsledkem je přidání tlačítka pro úpravy (a tlačítka aktualizovat a zrušit pro upravovaný řádek).

[![konfigurace prvku GridView pro podporu úprav](updating-and-deleting-existing-binary-data-vb/_static/image26.png)](updating-and-deleting-existing-binary-data-vb/_static/image25.png)

**Obrázek 10**: Konfigurace prvku GridView pro podporu úprav ([kliknutím zobrazíte obrázek v plné velikosti](updating-and-deleting-existing-binary-data-vb/_static/image27.png))

Přejděte na stránku v prohlížeči a klikněte na jedno z tlačítek pro úpravu řádku. `CategoryName` a `Description` BoundFields se vykreslují jako textová pole. `BrochurePath` TemplateField chybí `EditItemTemplate`, takže se nadále zobrazuje jeho `ItemTemplate` odkaz na brožuru. `Picture` ImageField vykreslí jako textové pole, jehož vlastnost `Text` je přiřazena hodnotě `DataImageUrlField` ImageField s, v tomto případě `CategoryID`.

[![prvku GridView chybí rozhraní pro úpravu pro BrochurePath](updating-and-deleting-existing-binary-data-vb/_static/image29.png)](updating-and-deleting-existing-binary-data-vb/_static/image28.png)

**Obrázek 11**: v prvku GridView chybí rozhraní pro úpravu pro `BrochurePath` ([kliknutím zobrazíte obrázek v plné velikosti).](updating-and-deleting-existing-binary-data-vb/_static/image30.png)

## <a name="customizing-thebrochurepaths-editing-interface"></a>Přizpůsobení rozhraní pro úpravy`BrochurePath`s

Musíme vytvořit rozhraní pro úpravy pro `BrochurePath` TemplateField, což umožní uživateli jednu z těchto akcí:

- Ponechte si brožuru kategorie s tak, jak je,
- Aktualizujte brožuru kategorie s tak, že nahrajete novou brožuru nebo
- Zcela odebrat brožuru s kategorií (v případě, že kategorie už nemá přidruženou brožuru).

Musíme také aktualizovat rozhraní pro úpravy `Picture` ImageField s, ale v kroku 7 to budeme mít.

Z inteligentní značky GridView s klikněte na odkaz Upravit šablony a v rozevíracím seznamu vyberte `BrochurePath` ' TemplateField s `EditItemTemplate`. Přidejte do této šablony webový ovládací prvek RadioButtonList, nastavením jeho vlastnosti `ID` na `BrochureOptions` a jeho vlastnost `AutoPostBack` na `True`. Z okno Vlastnosti klikněte na elipsy ve vlastnosti `Items`, která zobrazí Editor kolekce `ListItem`. Přidejte následující tři možnosti s `Value` s 1, 2 a 3 v uvedeném pořadí:

- Použít aktuální brožuru
- Odebrat aktuální brožuru
- Nahrát novou brožuru

Nastavte vlastnost First `ListItem` s `Selected` na `True`.

![Přidat tři položky ListItems na RadioButtonList](updating-and-deleting-existing-binary-data-vb/_static/image2.gif)

**Obrázek 12**: přidání tří `ListItem` s na RadioButtonList

Pod ovládacím prvkem RadioButtonList přidejte ovládací prvek nahrání souborů s názvem `BrochureUpload`. Vlastnost `Visible` nastavte na `False`.

[![přidání ovládacího prvku RadioButtonList a FileUpload do EditItemTemplate](updating-and-deleting-existing-binary-data-vb/_static/image32.png)](updating-and-deleting-existing-binary-data-vb/_static/image31.png)

**Obrázek 13**: Přidání ovládacího prvku RadioButtonList a fileupload do `EditItemTemplate` ([kliknutím zobrazíte obrázek v plné velikosti](updating-and-deleting-existing-binary-data-vb/_static/image33.png))

Tato RadioButtonList nabízí tři možnosti pro uživatele. Účelem je, aby se ovládací prvek nahrávání souborů zobrazil jenom v případě, že je vybraná možnost Odeslat novou brožuru. K tomuto účelu vytvořte obslužnou rutinu události pro událost RadioButtonList s `SelectedIndexChanged` a přidejte následující kód:

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample7.vb)]

Vzhledem k tomu, že ovládací prvky RadioButtonList a nahrání jsou v rámci šablony, musíme pro programové získání přístupu k těmto ovládacím prvkům napsat bitovou kopii kódu. Obslužná rutina události `SelectedIndexChanged` je předána odkazem RadioButtonList ve vstupním parametru `sender`. Chcete-li získat ovládací prvek pro nahrání souborů, musíme získat nadřazený ovládací prvek RadioButtonList s a použít z něj metodu `FindControl("controlID")`. Jakmile máme odkaz na ovládací prvky RadioButtonList i upload, vlastnost Control `Visible` pro nahrání je nastavena na `True` pouze v případě, že se ovládací prvek RadioButtonList s `SelectedValue` rovná 3, což je `Value` pro nahrávání nové brožury `ListItem`.

S tímto kódem chvíli počkejte, než otestujete rozhraní pro úpravy. Klikněte na tlačítko Upravit pro řádek. Zpočátku by se měla vybrat možnost použít aktuální brožuru. Změna vybraného indexu způsobí postback. Pokud je vybraná třetí možnost, zobrazí se ovládací prvek nahrání souborů, jinak je skrytý. Obrázek 14 ukazuje rozhraní pro úpravy při prvním kliknutí na tlačítko pro úpravy; Obrázek 15 ukazuje rozhraní po výběru možnosti nahrát novou brožuru.

[![zpočátku je vybraná možnost použít aktuální brožuru](updating-and-deleting-existing-binary-data-vb/_static/image35.png)](updating-and-deleting-existing-binary-data-vb/_static/image34.png)

**Obrázek 14**: zpočátku je vybrána možnost použít aktuální brožuru ([kliknutím zobrazíte obrázek v plné velikosti).](updating-and-deleting-existing-binary-data-vb/_static/image36.png)

[![výběru možnosti nahrát novou brožuru zobrazí ovládací prvek nahrání souborů.](updating-and-deleting-existing-binary-data-vb/_static/image38.png)](updating-and-deleting-existing-binary-data-vb/_static/image37.png)

**Obrázek 15**: Volba možnosti nahrát novou brožuru zobrazí ovládací prvek nahrání souborů (Kliknutím zobrazíte[obrázek v plné velikosti).](updating-and-deleting-existing-binary-data-vb/_static/image39.png)

## <a name="saving-the-brochure-file-and-updating-thebrochurepathcolumn"></a>Uložení souboru brožury a aktualizace sloupce`BrochurePath`

Po kliknutí na tlačítko pro aktualizaci GridView s se aktivuje jeho `RowUpdating` událost. Příkaz pro aktualizaci ObjectDataSource s je vyvolán a poté je vyvolána událost GridView s `RowUpdated`. Podobně jako u odstranění pracovního postupu musíme pro obě tyto události vytvořit obslužné rutiny událostí. V obslužné rutině události `RowUpdating` musíme určit, jakou akci chcete provést, na základě `SelectedValue` ovládacího panelu `BrochureOptions`:

- Pokud je `SelectedValue` 1, chceme dál používat stejné nastavení `BrochurePath`. Proto je nutné nastavit parametr ObjectDataSource s `brochurePath` na existující hodnotu `BrochurePath` aktualizovaného záznamu. Parametr ObjectDataSource s `brochurePath` lze nastavit pomocí `e.NewValues["brochurePath"] = value`.
- Pokud je `SelectedValue` 2, chceme, aby se hodnota `BrochurePath` záznamu nastavila na `NULL`. To lze provést nastavením parametru `brochurePath` ObjectDataSource s `Nothing`, což vede k tomu, že se v příkazu `UPDATE` používá databáze `NULL`. Pokud existuje existující soubor brožury, který se odebírá, musíme odstranit existující soubor. To ale chceme udělat jenom v případě, že se aktualizace dokončuje bez vyvolání výjimky.
- Pokud má `SelectedValue` hodnotu 3, chceme, aby uživatel nahrál soubor PDF a pak ho uložil do systému souborů a aktualizoval hodnotu `BrochurePath` sloupce záznamu. Kromě toho, pokud existuje existující soubor brožury, který se nahrazuje, musíme odstranit předchozí soubor. To ale chceme udělat jenom v případě, že se aktualizace dokončuje bez vyvolání výjimky.

Kroky, které je třeba provést, pokud je ovládací prvek RadioButtonList s `SelectedValue` 3, je prakticky shodný s těmi, které jsou používány obslužnou rutinou události `ItemInserting` ovládacího prvku DetailsView. Tato obslužná rutina události se spustí při přidání záznamu nové kategorie z ovládacího prvku DetailsView, který jsme přidali v [předchozím kurzu](including-a-file-upload-option-when-adding-a-new-record-vb.md). Proto se nám behooves, že se tyto funkce refaktorují do samostatných metod. Konkrétně jsme přesunuli společné funkce do dvou metod:

- `ProcessBrochureUpload(FileUpload, out bool)` akceptuje jako vstup instanci ovládacího prvku pro nahrání souborů a výstupní logickou hodnotu, která určuje, zda má být operace DELETE nebo Edit pokračovat nebo zda by měla být zrušena z důvodu chyby ověřování. Tato metoda vrátí cestu k uloženému souboru nebo `null`, pokud nebyl uložen žádný soubor.
- `DeleteRememberedBrochurePath` odstraní soubor určený cestou v proměnné stránky `deletedCategorysPdfPath` Pokud `deletedCategorysPdfPath` `null`.

Kód těchto dvou metod je následující. Všimněte si podobnosti mezi `ProcessBrochureUpload` a obslužnou rutinou ovládacího prvku DetailsView s `ItemInserting` z předchozího kurzu. V tomto kurzu jsem aktualizoval obslužné rutiny událostí DetailsView s, aby tyto nové metody používaly. Stáhněte si kód přidružený k tomuto kurzu, abyste viděli změny obslužných rutin událostí ovládacího prvku DetailsView s.

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample8.vb)]

Obslužné rutiny událostí `RowUpdating` a `RowUpdated` prvku GridView s používají metody `ProcessBrochureUpload` a `DeleteRememberedBrochurePath`, jak ukazuje následující kód:

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample9.vb)]

Všimněte si, jak obslužná rutina události `RowUpdating` používá sérii podmíněných příkazů k provedení příslušné akce na základě hodnoty vlastnosti `BrochureOptions` RadioButtonList s `SelectedValue`.

Pomocí tohoto kódu můžete upravit kategorii a použít její aktuální brožuru, použít bez brožury nebo nahrát novou. Pokračujte a vyzkoušejte si to. Nastavte zarážky v obslužných rutinách události `RowUpdating` a `RowUpdated`, abyste získali představu o pracovním postupu.

## <a name="step-7-uploading-a-new-picture"></a>Krok 7: nahrání nového obrázku

Rozhraní pro úpravu `Picture` ImageField s se vykresluje jako textové pole naplněné hodnotou z jeho vlastnosti `DataImageUrlField`. Během úprav pracovního postupu prvek GridView předá parametr prvku ObjectDataSource s parametrem s názvem a hodnotou vlastnosti ImageField s `DataImageUrlField` a parametrem value hodnotu zadanou v textovém poli v rozhraní pro úpravy. Toto chování je vhodné, pokud je obrázek uložen jako soubor v systému souborů a `DataImageUrlField` obsahuje úplnou adresu URL obrázku. V takových případech rozhraní pro úpravy zobrazuje v textovém poli adresu URL obrázku s, kterou uživatel může změnit a uložit zpět do databáze. Toto výchozí rozhraní neumožňuje uživateli odeslat nový obrázek, ale umožňuje změnit adresu URL obrázku z aktuální hodnoty na jinou. Pro tento kurz však ImageField s výchozím rozhraním pro úpravy nestačí, protože binární data `Picture` jsou ukládána přímo do databáze a vlastnost `DataImageUrlField` obsahuje pouze `CategoryID`.

Chcete-li lépe pochopit, co se děje v našem kurzu, když uživatel upraví řádek s ImageField, vezměte v úvahu následující příklad: uživatel upraví řádek s `CategoryID` 10, což způsobí, že `Picture` ImageField se vykreslí jako textové pole s hodnotou 10. Představte si, že uživatel změní hodnotu v tomto textovém poli na 50 a klikne na tlačítko Aktualizovat. Dojde k postbacku a ovládací prvek GridView zpočátku vytvoří parametr s názvem `CategoryID` s hodnotou 50. Nicméně předtím, než prvek GridView odešle tento parametr (a parametry `CategoryName` a `Description`), přidá do hodnot z kolekce `DataKeys`. Proto přepíše parametr `CategoryID` hodnotou aktuálního řádku s podkladovou hodnotou `CategoryID`, 10. V krátkém případě rozhraní pro úpravy ImageField s nemá žádný vliv na pracovní postup úpravy pro tento kurz, protože názvy vlastností `DataImageUrlField` ImageField s a mřížka s `DataKey` jsou jedna ve stejné hodnotě.

Zatímco ImageField usnadňuje zobrazení obrázku na základě databázových dat, nebudeme chtít v rozhraní pro úpravy poskytnout textové pole. Místo toho chceme nabídnout ovládací prvek pro nahrání souborů, který může koncový uživatel použít ke změně obrázku kategorie s. Na rozdíl od `BrochurePath` hodnoty se v těchto kurzech rozhodli vyžadovat, aby každá kategorie měla obrázek. Proto musíme uživateli upozornit, že není k dispozici žádný obrázek. uživatel může buď nahrát nový obrázek, nebo nechat aktuální obrázek beze změny.

Abychom mohli přizpůsobit rozhraní pro úpravy ImageField s, musíme ho převést na TemplateField. Z inteligentní značky GridView s klikněte na odkaz Upravit sloupce, vyberte ImageField a klikněte na tlačítko převést toto pole na odkaz TemplateField.

![Převést ImageField na TemplateField](updating-and-deleting-existing-binary-data-vb/_static/image3.gif)

**Obrázek 16**: převod ImageField na TemplateField

Převod ImageField na TemplateField tímto způsobem generuje TemplateField se dvěma šablonami. Jak ukazuje následující deklarativní syntaxe, `ItemTemplate` obsahuje webový ovládací prvek obrázku, jehož vlastnost `ImageUrl` je přiřazena pomocí syntaxe DataBinding založené na `DataImageUrlField` a `DataImageUrlFormatString` vlastnostech ImageField s. `EditItemTemplate` obsahuje pole, jehož vlastnost `Text` je svázána s hodnotou určenou vlastností `DataImageUrlField`.

[!code-aspx[Main](updating-and-deleting-existing-binary-data-vb/samples/sample10.aspx)]

Abychom mohli použít ovládací prvek pro nahrání souborů, musíme `EditItemTemplate` aktualizovat. Z inteligentní značky GridView s klikněte na odkaz Upravit šablony a v rozevíracím seznamu vyberte `Picture` TemplateField `EditItemTemplate`. V šabloně byste měli vidět textové pole odebrat toto. V dalším kroku přetáhněte ovládací prvek FileUpload ze sady nástrojů do šablony a nastavte jeho `ID` na `PictureUpload`. Přidejte také text pro změnu obrázku kategorie s a zadejte nový obrázek. Chcete-li zachovat stejný obrázek kategorie, nechte pole prázdné i v šabloně.

[![přidat ovládací prvek pro nahrání souborů do EditItemTemplate](updating-and-deleting-existing-binary-data-vb/_static/image41.png)](updating-and-deleting-existing-binary-data-vb/_static/image40.png)

**Obrázek 17**: Přidání ovládacího prvku pro nahrání souborů do `EditItemTemplate` ([kliknutím zobrazíte obrázek v plné velikosti](updating-and-deleting-existing-binary-data-vb/_static/image42.png))

Po přizpůsobení rozhraní pro úpravy si prohlédněte svůj průběh v prohlížeči. Při zobrazení řádku v režimu jen pro čtení se kategorie s zobrazuje jako předtím, ale když kliknete na tlačítko Upravit, vykreslí se sloupec obrázku jako text s ovládacím prvkem pro nahrání souborů.

[![rozhraní pro úpravy zahrnuje ovládací prvek nahrání souborů.](updating-and-deleting-existing-binary-data-vb/_static/image44.png)](updating-and-deleting-existing-binary-data-vb/_static/image43.png)

**Obrázek 18**: rozhraní pro úpravy obsahuje ovládací prvek pro nahrání souborů ([kliknutím zobrazíte obrázek v plné velikosti).](updating-and-deleting-existing-binary-data-vb/_static/image45.png)

Odvolání, že prvek ObjectDataSource je nakonfigurován tak, aby volal metodu `CategoriesBLL` třídy s `UpdateCategory`, která přijímá jako vstup binární data obrázku jako pole `Byte`. Pokud je toto pole `Nothing`je však volána alternativní `UpdateCategory` přetížení, což vydává příkaz `UPDATE` jazyka SQL, který nemění sloupec `Picture`, takže stávající obrázek kategorie s zůstane beze změny. Proto v prvku GridView `RowUpdating` obslužná rutina události potřebuje programově odkazovat na ovládací prvek nahrávání `PictureUpload` a určit, jestli se soubor nahrál. Pokud se jeden neodeslal, *nechci pro* parametr `picture` zadat hodnotu. Na druhé straně, pokud byl soubor nahrán v ovládacím prvku `PictureUpload` upload, chceme zajistit, aby se jednalo o soubor s příponou JPG. Pokud je, můžeme odeslat svůj binární obsah do prvku ObjectDataSource prostřednictvím parametru `picture`.

Podobně jako u kódu, který je použit v kroku 6, většina kódu, který je zde potřeba, již v ovládacím prvku DetailsView s `ItemInserting` obslužná rutina události existuje. Proto jsem přepracované společné funkce do nové metody, `ValidPictureUpload`a aktualizovala `ItemInserting` obslužnou rutinu události, aby používala tuto metodu.

Přidejte následující kód na začátek obslužné rutiny události `RowUpdating` GridView. Je důležité, aby tento kód pocházel před kódem, který ukládá soubor brožury, protože nechceme Uložit brožuru do systému souborů webového serveru s, pokud se nahraje neplatný soubor s obrázkem.

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample11.vb)]

Metoda `ValidPictureUpload(FileUpload)` přebírá jako svůj vlastní vstupní parametr jako svůj jediný vstupní parametr a kontroluje nahrané rozšíření souboru, aby bylo zajištěno, že nahraný soubor je JPG; volá se jenom v případě, že se nahraje soubor s obrázkem. Pokud není nahrán žádný soubor, není parametr obrázek nastaven, a proto používá jeho výchozí hodnotu `Nothing`. Pokud se obrázek nahrál a `ValidPictureUpload` vrátí `True`, má parametr `picture` přiřazená binární data nahraného obrázku. Pokud metoda vrátí `False`, pracovní postup aktualizace je zrušen a obslužná rutina události byla ukončena.

Kód metody `ValidPictureUpload(FileUpload)`, který byl refaktored z obslužné rutiny události `ItemInserting` ovládacího prvku DetailsView, je následující:

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample12.vb)]

## <a name="step-8-replacing-the-original-categories-pictures-with-jpgs"></a>Krok 8: nahrazení původních kategorií obrázky pomocí JPGs

Odvolání původních osmi kategorií obrázky jsou rastrové soubory zabalené v hlavičce OLE. Teď, když jsme přidali možnost pro úpravu existujícího obrázku s záznamem, chvíli nahraďte tyto bitmapy pomocí JPGs. Pokud chcete nadále používat aktuální obrázky kategorií, můžete je převést na JPGs provedením následujících kroků:

1. Uložte rastrové obrázky na pevný disk. Navštivte stránku `UpdatingAndDeleting.aspx` v prohlížeči a pro každou z prvních osmi kategorií klikněte pravým tlačítkem na obrázek a vyberte možnost Uložit obrázek.
2. Otevřete obrázek v editoru obrázků podle vlastního výběru. Můžete použít například Microsoft Paint.
3. Uložte bitmapu jako obrázek JPG.
4. Aktualizujte obrázek kategorie s přes rozhraní pro úpravy pomocí souboru JPG.

Když upravíte kategorii a nahrajete image JPG, obrázek se v prohlížeči nevykresluje, protože `DisplayCategoryPicture.aspx` stránka odeberou prvních 78 bajtů z obrázků prvních osmi kategorií. Opravte tento problém odebráním kódu, který provádí odstraňování hlaviček OLE. Poté by obslužná rutina události `DisplayCategoryPicture.aspx``Page_Load` měla mít pouze následující kód:

[!code-vb[Main](updating-and-deleting-existing-binary-data-vb/samples/sample13.vb)]

> [!NOTE]
> Rozhraní pro vložení a úpravu stránky `UpdatingAndDeleting.aspx` můžou používat trochu více práce. `CategoryName` a `Description` BoundFields v ovládacím prvku DetailsView a GridView by měly být převedeny na TemplateFields. Vzhledem k tomu, že `CategoryName` nepovoluje `NULL` hodnoty, je třeba přidat RequiredFieldValidator. A `Description` textové pole by pravděpodobně bylo převedeno do víceřádkového textového pole. Tato dokončíme jako cvičení.

## <a name="summary"></a>Přehled

V tomto kurzu se dokončí náš pohled na práci s binárními daty. V tomto kurzu a předchozích třech jsme viděli, jak můžou být binární data uložená v systému souborů nebo přímo v rámci databáze. Uživatel poskytne systému binární data, a to tak, že vybere soubor z jeho pevného disku a nahraje ho na webový server, kde může být uložený v systému souborů nebo vložený do databáze. ASP.NET 2,0 obsahuje ovládací prvek pro nahrání souborů, který poskytuje takové rozhraní jako snadné a přetahování. Jak je uvedeno v kurzu [nahrávání souborů](uploading-files-vb.md) , je ovládací prvek nahrání souborů vhodný pouze pro relativně malá nahrávání souborů, v ideálním případě nepřekračuje megabajt. Prozkoumali jsme také, jak přidružit nahraná data k základnímu datovému modelu, a jak upravit a odstranit binární data z existujících záznamů.

Naše další sada kurzů zkoumá různé techniky ukládání do mezipaměti. Ukládání do mezipaměti poskytuje způsob, jak zvýšit celkový výkon aplikace tím, že vezme výsledky z nákladných operací a uloží je do umístění, ke kterému se dá rychleji připínat.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Teresa Murphy. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](including-a-file-upload-option-when-adding-a-new-record-vb.md)

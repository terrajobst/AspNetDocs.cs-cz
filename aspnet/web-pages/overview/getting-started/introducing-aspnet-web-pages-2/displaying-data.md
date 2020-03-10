---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
title: Představení ASP.NET webových stránek – zobrazení dat | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se dozvíte, jak vytvořit databázi v WebMatrixu a jak zobrazit databázová data na stránce, když používáte webové stránky ASP.NET (Razor). Předpokládá y...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: b3a006a0-3ea2-4d45-b833-e20e3a3c0a1a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
msc.type: authoredcontent
ms.openlocfilehash: 9e665ca8dd064c23a8b8bd3593014969d0c3da48
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525219"
---
# <a name="introducing-aspnet-web-pages---displaying-data"></a>Představení ASP.NET webových stránek – zobrazení dat

tím, že [FitzMacken](https://github.com/tfitzmac)

> V tomto kurzu se dozvíte, jak vytvořit databázi v WebMatrixu a jak zobrazit databázová data na stránce, když používáte webové stránky ASP.NET (Razor). Předpokládá, že jste dokončili řadu prostřednictvím [úvodu do programování webových stránek ASP.NET](../introducing-razor-syntax-c.md).
> 
> Naučíte se:
> 
> - Jak pomocí nástrojů WebMatrix vytvořit databázi a tabulky databáze.
> - Jak pomocí nástrojů WebMatrix přidat data do databáze.
> - Jak zobrazit data z databáze na stránce.
> - Spuštění příkazů SQL na webových stránkách ASP.NET
> - Postup přizpůsobení pomocníka `WebGrid` pro změnu zobrazení dat a přidání stránkování a řazení
>   
> 
> Popsané funkce a technologie:
> 
> - Nástroje databáze WebMatrix
> - Pomocná `WebGrid`

## <a name="what-youll-build"></a>Co sestavíte

V předchozím kurzu jste se zavedli k ASP.NETí webových stránek (soubory *. cshtml* ) k základům syntaxe Razor a pomocníkům. V tomto kurzu začnete vytvářet vlastní webovou aplikaci, kterou použijete pro zbytek řady. Aplikace je jednoduchá aplikace pro video, která umožňuje zobrazovat, přidávat, měnit a odstraňovat informace o filmech.

Až budete s tímto kurzem hotovi, budete moct zobrazit seznam filmů, který vypadá jako tato stránka:

![Zobrazení webgridu obsahující parametry nastavené na názvy tříd šablon stylů CSS](displaying-data/_static/image1.png)

Chcete-li však začít, je nutné vytvořit databázi.

## <a name="a-very-brief-introduction-to-databases"></a>Velmi stručný úvod k databázím

Tento kurz vám poskytne jenom nejstručnější Úvod k databázím. Pokud máte zkušenosti s databází, můžete tuto krátkou část přeskočit.

Databáze obsahuje jednu nebo více tabulek, které obsahují informace &mdash; například tabulky pro zákazníky, objednávky a dodavatele nebo pro studenty, učitele, třídy a třídy. Struktura databáze je jako tabulka. Představte si typický adresář. Pro každou položku v adresáři (tj. pro jednotlivé osoby) máte několik informací, jako je křestní jméno, příjmení, adresa, e-mailová adresa a telefonní číslo.

![Ukázková databázová tabulka jako jednoduchá mřížka](displaying-data/_static/image2.png)

(Řádky jsou někdy označovány jako *záznamy*a sloupce jsou někdy označovány jako *pole*.)

U většiny tabulek databáze musí mít tabulka sloupec, který obsahuje jedinečnou hodnotu, třeba číslo zákazníka, číslo účtu atd. Tato hodnota se označuje jako *primární klíč*tabulky a používá se k identifikaci každého řádku v tabulce. V tomto příkladu je sloupec ID primárním klíčem pro adresář uvedený v předchozím příkladu.

Většina práce v rámci webových aplikací se skládá z informací o čtení z databáze a jejich zobrazení na stránce. Také často shromáždíte informace od uživatelů a přidáte je do databáze nebo upravíte záznamy, které jsou již v databázi. (Všechny tyto operace pokryjeme v průběhu této sady kurzů.)

Práce v databázi může být mimořádně složitá a může vyžadovat specializované znalosti. V této sadě kurzů je ale potřeba pochopit jenom základní koncepty, které budou vysvětlené.

## <a name="creating-a-database"></a>Vytvoření databáze

WebMatrix obsahuje nástroje, které usnadňují vytváření databází a vytváření tabulek v databázi. (Struktura databáze je označována jako *schéma*databáze.) Pro tuto sadu kurzů vytvoříte databázi, která má v ní jenom jednu tabulku &mdash; filmy.

Otevřete WebMatrix, pokud jste to ještě neudělali, a otevřete web WebPagesMovies, který jste vytvořili v předchozím kurzu.

V levém podokně klikněte na pracovní prostor **databáze** .

![Karta pracovní prostor databáze WebMatrix](displaying-data/_static/image3.png)

Pás karet se změní na Zobrazit úlohy týkající se databáze. Na pásu karet klikněte na možnost **Nová databáze**.

![Tlačítko Nová databáze na pásu karet WebMatrixu](displaying-data/_static/image4.png)

WebMatrix vytvoří databázi SQL Server CE (soubor *. sdf* ), která má stejný název jako web &mdash; *WebPagesMovies. sdf*. (Tady to neuděláte, ale tento soubor můžete přejmenovat na cokoli, co byste chtěli, pokud má příponu *. sdf* .)

## <a name="creating-a-table"></a>Vytvoření tabulky

Na pásu karet klikněte na možnost **Nová tabulka**. WebMatrix otevře Návrháře tabulky na nové kartě. (Pokud možnost Nová tabulka není dostupná, ujistěte se, že je ve stromovém zobrazení vlevo vybraná nová databáze.)

![Tlačítko Nová tabulka na pásu karet WebMatrixu](displaying-data/_static/image5.png)

Do textového pole v horní části (kde vodoznak říká "zadat název tabulky") zadejte "filmy".

![Zadání názvu tabulky v Návrháři databáze WebMatrix](displaying-data/_static/image6.png)

V podokně pod názvem tabulky je místo, kde můžete definovat jednotlivé sloupce. V tabulce *filmy* v tomto kurzu vytvoříte pouze několik sloupců: *ID*, *název*, *Žánr*a *rok*.

Do pole **název** zadejte "ID". Zadáním hodnoty aktivujete všechny ovládací prvky nového sloupce.

Na seznam **datový typ** a vyberte **int**. Tato hodnota určuje, že sloupec ID bude obsahovat data typu Integer (number).

> [!NOTE]
> Tady ji nebudeme volat (mnoho), ale k navigaci v této mřížce můžete použít standardní gesta klávesnice Windows. Například můžete zadat tabulátor mezi poli, stačí začít psát, aby bylo možné vybrat položku v seznamu, a tak dále.

Karta s výchozím polem s **výchozí hodnotou** (tj. ponechte prázdné) Na kartu **je primární klíč** a vyberte ji. Tato možnost oznamuje databázi, že sloupec *ID* bude obsahovat data, která identifikují jednotlivé řádky. (To znamená, že každý řádek bude mít jedinečnou hodnotu ve sloupci ID, který můžete použít k vyhledání tohoto řádku.)

Vyberte možnost **je identita** . Tato možnost oznamuje databázi, že by měla automaticky generovat další sekvenční číslo pro každý nový řádek. (Možnost **is identity** funguje pouze v případě, že jste vybrali také možnost **je primární klíč** .)

Kliknutím na řádek další mřížky nebo dvojím stisknutím klávesy TAB dokončete aktuální řádek. Buď gesto uloží aktuální řádek a spustí další. Všimněte si, že sloupec **Výchozí hodnota** nyní říká **hodnotu null**. (Výchozí hodnota je null, takže se má mluvit.)

Po dokončení definování sloupce nový **identifikátor** bude Návrhář vypadat jako na následujícím obrázku:

![Návrhář databáze WebMatrix po definování sloupce ID pro tabulku filmů](displaying-data/_static/image7.png)

Chcete-li vytvořit další sloupec, klikněte do pole ve sloupci **název** . Zadejte "title" pro sloupec a pak pro hodnotu **datového typu** vyberte **nvarchar** . Část "var" v rámci **nvarchar** oznamuje databázi, že data pro tento sloupec budou řetězcem, jehož velikost se může lišit od záznamu k záznamu. (Předpona "n" představuje "National", což znamená, že pole může obsahovat znaková data pro libovolný abecední nebo systém zápisu – to znamená, že pole obsahuje data v kódování Unicode.)

Když zvolíte **nvarchar**, zobrazí se další okno, kde můžete zadat maximální délku pole. Zadejte 50, na předpokladu, že žádný název videa, se kterým budete v tomto kurzu pracovat, bude delší než 50 znaků.

Přeskočte **výchozí hodnotu** a zrušte zaškrtnutí možnosti **Povolení hodnot null** . Nechcete, aby databáze povolovala zadávání filmů do databáze, která nemá název.

Až skončíte a přejdete na další řádek, Návrhář bude vypadat jako na následujícím obrázku:

![Návrhář databáze WebMatrix po definování sloupce nadpisu pro tabulku filmů](displaying-data/_static/image8.png)

Zopakováním těchto kroků vytvoříte sloupec s názvem "Žánr", s výjimkou délky, nastavíte ho pouze na 30.

Vytvořte další sloupec s názvem "Year". Pro datový typ vyberte možnost **nchar** (ne **nvarchar**) a nastavte délku na 4. V roce budete používat čtyřmístné číslo, například "1995" nebo "2010", takže nebudete potřebovat sloupec s proměnlivou velikostí.

Tento návrh vypadá takto:

![Návrhář databáze WebMatrix po definování všech polí pro tabulku filmů](displaying-data/_static/image9.png)

Stiskněte klávesy CTRL + S nebo klikněte na tlačítko **Uložit** na panelu nástrojů Rychlý přístup. Zavřete okno návrháře databáze zavřením karty.

## <a name="adding-some-example-data"></a>Přidání ukázkových dat

Později v této sérii kurzů vytvoříte stránku, kde můžete do formuláře zadat nové filmy. Teď ale můžete přidat některá ukázková data, která pak můžete zobrazit na stránce.

V pracovním prostoru **databáze** ve WebMatrixu si všimněte, že je k dispozici strom, který vám ukáže soubor *. sdf* , který jste vytvořili dříve. Otevřete uzel nového souboru *. sdf* a pak otevřete uzel **tabulky** .

![Pracovní prostor databáze WebMatrix se stromovou strukturou otevřenou v tabulce filmů](displaying-data/_static/image10.png)

Klikněte pravým tlačítkem myši na uzel **filmy** a pak zvolte **data**. WebMatrix otevře mřížku, kde můžete zadat data pro tabulku *filmů* :

![Mřížka položky databáze ve WebMatrixu (prázdná)](displaying-data/_static/image11.png)

Klikněte na sloupec **název** a zadejte "when Harry Met Sally". Přejděte do sloupce **Žánr** (můžete použít klávesu TAB) a zadat "Romantic komedie". Přejděte do sloupce **year (rok** ) a zadejte "1989":

![Mřížka záznamů databáze ve WebMatrixu s jedním záznamem](displaying-data/_static/image12.png)

Stiskněte klávesu ENTER a WebMatrix uloží nový film. Všimněte si, že sloupec **ID** byl vyplněn.

![Mřížka záznamů databáze ve WebMatrixu s jedním záznamem a automaticky generovaným ID](displaying-data/_static/image13.png)

Zadejte jiný film (například "zmizelo s převinutím", "drama", "1939"). Sloupec ID je vyplněn znovu:

![Mřížka záznamů databáze ve WebMatrixu se dvěma záznamy a automaticky generovanými identifikátory](displaying-data/_static/image14.png)

Zadejte třetí film (například "Ghostbusters", "komedie"). Jako experiment ponechte sloupec **year** prázdný a potom stiskněte klávesu ENTER. Vzhledem k tomu, že jste nevybrali možnost **povolující hodnoty null** , v databázi se zobrazí chyba:

![V případě, že je hodnota požadovaného sloupce ponechána prázdná, se zobrazí chyba neplatná data.](displaying-data/_static/image15.png)

Kliknutím na **OK** se vraťte a opravte položku (rok "Ghostbusters" je 1984) a pak stiskněte ENTER.

Vyplňte několik filmů, dokud nebudete mít 8 nebo ne. (Zadání 8 usnadňuje práci s stránkováním později. Pokud je ale příliš mnoho, zadejte nyní pouze pár.) Skutečná data nezáleží.

![Mřížka záznamů databáze ve WebMatrixu s oběma záznamy](displaying-data/_static/image16.png)

Pokud jste zadali všechny filmy bez chyb, jsou hodnoty ID sekvenční. Pokud jste se pokusili uložit nekompletní záznam filmu, čísla ID nemusí být sekvenční. Pokud ano, je to v pořádku. Tato čísla nemají žádný podstatný význam a jediný aspekt, který je důležitý, je to, že jsou v tabulce *filmů* jedinečné.

Zavřete kartu, která obsahuje návrháře databáze.

Nyní můžete tato data zobrazit na webové stránce.

## <a name="displaying-data-in-a-page-by-using-the-webgrid-helper"></a>Zobrazení dat na stránce pomocí pomocníka WebGrid

Chcete-li zobrazit data na stránce, budete používat pomocníka `WebGrid`. Tento Pomocník vytvoří zobrazení v mřížce nebo tabulce (řádky a sloupce). Jak vidíte, budete moct upravit mřížku s využitím formátování a dalších funkcí.

Chcete-li spustit mřížku, budete muset napsat pár řádků kódu. Tyto pár řádků budou sloužit jako druh vzoru pro téměř všechna přístup k datům, která v tomto kurzu provedete.

> [!NOTE]
> Ve skutečnosti máte spoustu možností, jak zobrazit data na stránce. pomocná rutina `WebGrid` je jenom jedna. Pro tento kurz jsme si ho zvolili, protože je nejjednodušší způsob, jak zobrazit data a protože je rozumně flexibilní. V dalším kurzu se dozvíte, jak použít další "ruční" způsob práce s daty na stránce, což vám umožní lépe nastavit kontrolu nad tím, jak se mají data zobrazovat.

V levém podokně WebMatrix klikněte na pracovní prostor **soubory** .

Nová databáze, kterou jste vytvořili, je ve složce *App\_data* . Pokud složka již neexistuje, vytvoří ji WebMatrix pro novou databázi. (Složka může existovat, pokud jste dříve nainstalovali pomocníky.)

Ve stromovém zobrazení vyberte kořen webu. Musíte vybrat kořen webu. v opačném případě může být nový soubor přidán do složky aplikace\_data.

Na pásu karet klikněte na **Nový**. V poli **zvolit typ souboru** vyberte možnost **cshtml**.

Do pole **název** zadejte novou stránku filmy. cshtml:

![Dialogové okno zvolit typ souboru zobrazující stránku filmy](displaying-data/_static/image17.png)

Klikněte na tlačítko **OK**. WebMatrix otevře nový soubor s některými kostrami prvku. Nejdřív napíšete nějaký kód, který získá data z databáze. Pak přidáte značku na stránku, kde můžete data ve skutečnosti zobrazit.

### <a name="writing-the-data-query-code"></a>Zápis kódu dotazu na data

V horní části stránky mezi znaky `@{` a `}` zadejte následující kód. (Nezapomeňte zadat tento kód mezi levou a pravou závorkou.)

[!code-csharp[Main](displaying-data/samples/sample1.cs)]

První řádek otevře databázi, kterou jste vytvořili dříve, což je vždy první krok před tím, než bude pracovat s databází. Určíte, `Database.Open` se má název metody pro otevření databáze otevřít. Všimněte si, že do názvu nezahrnete *. sdf* . Metoda `Open` předpokládá, že hledá soubor *. sdf* (to znamená *WebPagesMovies. sdf*) a že soubor *. sdf* je ve složce *App\_data* . (Dříve jsme si poznamenali, že je složka *aplikace\_data* rezervovaná. Tento scénář je jedno z míst, kde ASP.NET provede předpoklady tohoto názvu.)

Po otevření databáze je odkaz na ni vložen do proměnné s názvem `db`. (Může se jmenovat cokoli.) `db` proměnná se dozvíte, jak budete pracovat s databází.

Druhý řádek ve skutečnosti načte data databáze pomocí metody `Query`. Všimněte si, jak tento kód funguje: proměnná `db` má odkaz na otevřenou databázi a vyvolat metodu `Query` pomocí proměnné `db` (`db.Query`).

Samotný dotaz je příkaz SQL `Select`. (Pro malé pozadí o SQL se podívejte na vysvětlení později.) V příkazu `Movies` identifikuje tabulku pro dotaz. Znak `*` určuje, že dotaz by měl vracet všechny sloupce z tabulky. (Můžete také vypsat sloupce jednotlivě a oddělit je čárkami.)

Výsledky dotazu, jsou-li nějaké, jsou vráceny a zpřístupněny v proměnné `selectedData`. Proměnnou lze znovu pojmenovat cokoli.

Nakonec třetí řádek oznamuje ASP.NET, že chcete použít instanci pomocné rutiny `WebGrid`. Vytvoříte (vytvořte*instanci*) objektu pomocníka pomocí klíčového slova `new` a předejte ho do výsledků dotazu prostřednictvím proměnné `selectedData`. Nový objekt `WebGrid` společně s výsledky databázového dotazu jsou zpřístupněny v proměnné `grid`. Budete ho potřebovat k tomu, aby se data na stránce skutečně zobrazila.

V této fázi se databáze otevřela, obdrželi jste požadovaná data a Vy jste připravili `WebGrid` pomocná s těmito daty. Dále je možné vytvořit značku na stránce.

> [!TIP] 
> 
> **Jazyk SQL (Structured Query Language) (SQL)**
> 
> SQL je jazyk, který se používá ve většině relačních databází pro správu dat v databázi. Obsahuje příkazy, které umožňují načíst data a aktualizovat je a umožňují vytvářet, upravovat a spravovat data v databázových tabulkách. SQL se liší od programovacího jazyka (například C#). V jazyce SQL říkáte databázi, kterou chcete, a její úlohu, abyste zjistili, jak získat data nebo provést úlohu. Tady jsou příklady některých příkazů SQL a jejich možnosti:
> 
> `Select * From Movies`
> 
> `SELECT ID, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> První příkaz `Select` získá všechny sloupce (určené `*`) z tabulky *filmů* .
> 
> Druhý příkaz `Select` načte sloupce ID, název a ceny ze záznamů v tabulce *produktů* , jejichž hodnota sloupce Price je vyšší než 10. Příkaz vrátí výsledky v abecedním pořadí na základě hodnot sloupce název. Pokud kritéria ceny neodpovídají žádné záznamy, vrátí příkaz prázdnou sadu.
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ('Croissant', 'A flaky delight', 1.99)`
> 
> Tento příkaz vloží nový záznam do tabulky *Product* , nastaví sloupec název na "croissant", sloupec s popisem na "" rozsvítit "a cenu na 1,99.
> 
> Všimněte si, že když zadáváte nečíselnou hodnotu, hodnota je uzavřena v jednoduchých uvozovkách (ne v uvozovkách, jako v C#). Tyto uvozovky se používají kolem hodnot text nebo Date, ale ne kolem čísel.
> 
> `DELETE FROM Product WHERE ExpirationDate < '01/01/2008'`
> 
> Tento příkaz odstraní záznamy v tabulce *produktů* , jejichž sloupec Datum vypršení platnosti je starší než 1. ledna 2008. (Příkaz předpokládá, že tabulka *produktu* má takový sloupec kurzu.) Datum je zadáno ve formátu MM/DD/RRRR, ale mělo by být zadáno ve formátu používaném pro vaše národní prostředí.
> 
> Příkazy `Insert` a `Delete` nevrací sady výsledků dotazu. Místo toho vrátí číslo, které oznamuje, kolik záznamů bylo ovlivněno příkazem.
> 
> Pro některé z těchto operací (jako je vkládání a odstraňování záznamů) musí mít proces, který vyžaduje operaci, příslušná oprávnění v databázi. To je důvod, proč pro produkční databáze, které často potřebujete k zadání uživatelského jména a hesla při připojování k databázi.
> 
> Existují spousty příkazů SQL, ale všechny mají stejný vzor jako příkazy, které tady vidíte. Pomocí příkazů SQL můžete vytvořit tabulky databáze, spočítat počet záznamů v tabulce, vypočítat ceny a provádět spoustu dalších operací.

### <a name="adding-markup-to-display-the-data"></a>Přidání značek pro zobrazení dat

Uvnitř prvku `<head>` nastavte obsah elementu `<title>` na "filmy":

[!code-html[Main](displaying-data/samples/sample2.html?highlight=3)]

Do prvku `<body>` stránky přidejte následující:

[!code-html[Main](displaying-data/samples/sample3.html)]

A to je vše. Proměnná `grid` je hodnota, kterou jste vytvořili při vytváření objektu `WebGrid` v kódu dříve.

Ve stromovém zobrazení WebMatrix klikněte pravým tlačítkem na stránku a vyberte **Spustit v prohlížeči**. Uvidíte něco jako na této stránce:

![Výchozí výstup pomocníka WebGrid z tabulky filmů](displaying-data/_static/image18.png)

Kliknutím na odkaz na záhlaví sloupce seřadíte podle sloupce. Možnost řadit kliknutím na záhlaví je funkce, která je integrovaná do pomocné rutiny **WebGrid** .

Metoda `GetHtml`, jak je navržena názvem, vygeneruje kód, který zobrazí data. Ve výchozím nastavení metoda `GetHtml` generuje element `<table>` HTML. (Pokud chcete, můžete vykreslování ověřit tak, že prohlížíte zdroj stránky v prohlížeči.)

## <a name="modifying-the-look-of-the-grid"></a>Změna vzhledu mřížky

Použití pomocníka `WebGrid`, jako jste právě pracovali, je jednoduché, ale výsledný displej je obyčejný. Pomocná rutina `WebGrid` má nejrůznější možnosti, které vám umožní určit, jak se data zobrazují. V tomto kurzu se dá prozkoumat příliš mnoho, ale v této části získáte představu o některých z těchto možností. V dalších kurzech v této sérii bude zahrnuto několik dalších možností.

### <a name="specifying-individual-columns-to-display"></a>Určení jednotlivých sloupců k zobrazení

Chcete-li začít, můžete určit, že chcete zobrazit pouze některé sloupce. Ve výchozím nastavení mřížka zobrazuje všechny čtyři sloupce z tabulky *filmů* .

V souboru *Movies. cshtml* nahraďte kód `@grid.GetHtml()`, který jste právě přidali, následující:

[!code-css[Main](displaying-data/samples/sample4.css)]

Chcete-li říct, které sloupce se mají zobrazit, přidejte do metody `GetHtml` parametr `columns` a předejte kolekci sloupců. V kolekci určíte jednotlivé sloupce, které chcete zahrnout. Určete jednotlivý sloupec, který se má zobrazit, zahrnutím objektu `grid.Column` a předáním názvu sloupce dat, který chcete. (Tyto sloupce musí být zahrnuté do výsledků dotazu SQL – Pomocník pro `WebGrid` nemůže zobrazit sloupce, které dotaz nevrátil.)

Znovu spusťte stránku *filmy. cshtml* v prohlížeči a tentokrát získáte zobrazení podobné následujícímu (Všimněte si, že se nezobrazuje žádný sloupec ID):

![Zobrazení WebGrid zobrazující pouze vybrané sloupce](displaying-data/_static/image19.png)

### <a name="changing-the-look-of-the-grid"></a>Změna vzhledu mřížky

Existuje několik možností, jak zobrazit sloupce, některé z nich se budou prozkoumat v pozdějších kurzech v této sadě. V této části se teď seznámíte s možnostmi, jak můžete mřížku stylovat jako celek.

V části `<head>` stránky těsně před uzavírací `</head>` značku přidejte následující prvek `<style>`:

[!code-css[Main](displaying-data/samples/sample5.css)]

Tento kód CSS definuje třídy s názvem `grid`, `head`a tak dále. Tyto definice stylu můžete také vložit do samostatného souboru *. CSS* a propojit je se stránkou. (Ve skutečnosti to uděláte později v této sadě kurzů.) Pro usnadnění tohoto kurzu ale budete mít stejnou stránku, která zobrazuje data.

Nyní můžete získat pomoc `WebGrid` pomocníka pro použití těchto tříd stylu. Pomocník má několik vlastností (například `tableStyle`) pouze pro tento účel – přiřadíte mu název třídy stylu CSS a tento název třídy je vykreslen jako součást značky, která je vykreslena pomocí pomocné rutiny.

Změňte kód `grid.GetHtml` tak, aby vypadal teď jako tento kód:

[!code-css[Main](displaying-data/samples/sample6.css)]

Co je nového tady je, že jste do `GetHtml` metody přidali parametry `tableStyle`, `headerStyle`a `alternatingRowStyle`. Tyto parametry byly nastaveny na názvy stylů CSS, které jste přidali před okamžikem.

Spusťte stránku a tentokrát vidíte mřížku, která vypadá mnohem méně Velká než předtím:

![Zobrazení webgridu obsahující parametry nastavené na názvy tříd šablon stylů CSS](displaying-data/_static/image20.png)

Chcete-li zjistit, jaká `GetHtml` metoda vygenerovala, můžete se podívat na zdroj stránky v prohlížeči. Tady nebudeme detailně fungovat, ale důležitým bodem je to, že zadáním parametrů jako `tableStyle`jste způsobili, že mřížka generuje značky HTML jako následující:

`<table class="grid">`

K značce `<table>` se přidal atribut `class`, který odkazuje na jedno z pravidel CSS, která jste přidali dříve. Tento kód vám ukáže základní vzor &mdash; různých parametrů pro metodu `GetHtml` umožňují odkazování na třídy CSS, které Metoda generuje společně s označením. To, co s třídami CSS pracujete, je až vám.

## <a name="adding-paging"></a>Přidávání stránkování

Jako poslední úkol tohoto kurzu přidáte do mřížky stránkování. Momentálně není k dispozici žádný problém k zobrazení všech filmů najednou. Pokud jste ale přidali stovky filmů, bude zobrazení stránky dlouhé.

V kódu stránky změňte řádek, který vytvoří objekt `WebGrid`, na následující kód:

[!code-csharp[Main](displaying-data/samples/sample7.cs)]

Jediným rozdílem od před je, že jste přidali parametr `rowsPerPage`, který je nastavený na 3.

Spusťte stránku. Mřížka zobrazuje 3 řádky najednou a navigační odkazy, které vám umožní stránkovat videa ve vaší databázi:

![Zobrazení webgridu s stránkováním](displaying-data/_static/image21.png)

## <a name="coming-up-next"></a>Připravujeme další

V dalším kurzu se dozvíte, jak pomocí Razor a C# kódu získat vstup uživatele ve formuláři. Přidáte vyhledávací pole na stránku filmy, abyste mohli hledat filmy podle názvu nebo žánru.

## <a name="complete-listing-for-movies-page"></a>Úplný výpis pro stránku filmů

[!code-cshtml[Main](displaying-data/samples/sample8.cshtml)]

## <a name="additional-resources"></a>Další prostředky

- [Seznámení s ASP.NET webovým programováním pomocí syntaxe Razor](https://go.microsoft.com/fwlink/?LinkID=202890)

> [!div class="step-by-step"]
> [Předchozí](intro-to-web-pages-programming.md)
> [Další](form-basics.md)

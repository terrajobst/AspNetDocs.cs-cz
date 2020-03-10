---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
title: Vytvoření vrstvy přístupu k datům | Microsoft Docs
author: Erikre
description: V této sérii kurzů se seznámíte se základy vytváření aplikací webových formulářů ASP.NET pomocí ASP.NET 4,5 a Microsoft Visual Studio Express 2013 pro My...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 0bbf7a6e-d7eb-4091-91e4-fff892777f32
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/create_the_data_access_layer
msc.type: authoredcontent
ms.openlocfilehash: 0fcf050474a57be9ed53ec0783a6d6b7dde2bf4c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544924"
---
# <a name="create-the-data-access-layer"></a>Vytvoření vrstvy přístupu k datům

od [Erik Reitan](https://github.com/Erikre)

[Stáhnout vzorový projekt Wingtip Toys (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) nebo [Stáhnout elektronickou knihu (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> V této sérii kurzů se naučíte základy vytváření webových formulářů ASP.NET pomocí ASP.NET 4,5 a Microsoft Visual Studio Express 2013 pro web. K dispozici je Visual Studio 2013 [projekt se C# zdrojovým kódem](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) , který se doprovází v této sérii kurzů.

V tomto kurzu se dozvíte, jak vytvořit, získat přístup a zkontrolovat data z databáze pomocí webových formulářů ASP.NET a Code First Entity Framework. Tento kurz sestaví v předchozím kurzu "vytvořit projekt" a je součástí série kurzů pro společnost Wingtip Toys. Po dokončení tohoto kurzu budete mít vytvořenou skupinu tříd pro přístup k datům, které jsou ve složce *modely* projektu.

## <a name="what-youll-learn"></a>Naučíte se:

- Jak vytvořit datové modely.
- Jak inicializovat a ohlašovat databázi.
- Jak aktualizovat a nakonfigurovat aplikaci, aby podporovala databázi.

### <a name="these-are-the-features-introduced-in-the-tutorial"></a>Tyto funkce jsou představené v tomto kurzu:

- Entity Framework Code First
- LocalDB
- Datové poznámky

## <a name="creating-the-data-models"></a>Vytváření datových modelů

[Entity Framework](https://msdn.microsoft.com/data/aa937723) je rozhraní pro mapování relačních objektů (ORM). Umožňuje pracovat s relačními daty jako objekty a eliminovat většinu kódu přístupu k datům, který byste obvykle museli psát. Pomocí Entity Framework můžete vydávat dotazy pomocí [LINQ](https://msdn.microsoft.com/library/bb397926.aspx), načítat a manipulovat s daty jako objekty silného typu. LINQ poskytuje vzory pro dotazování a aktualizaci dat. Použití Entity Framework vám umožní soustředit se na vytvoření zbytku aplikace a nemusíte se zaměřit na základy přístupu k datům. Později v této sérii kurzů vám ukážeme, jak používat data k naplnění navigace a dotazů na produkt.

Entity Framework podporuje vývojové paradigma nazvané *Code First*. Code First umožňuje definovat datové modely pomocí tříd. Třída je konstrukce, která umožňuje vytvořit vlastní typy seskupením proměnných jiných typů, metod a událostí. Můžete mapovat třídy na existující databázi nebo je použít k vygenerování databáze. V tomto kurzu vytvoříte datové modely pomocí zápisu tříd datového modelu. Pak z těchto nových tříd umožníte Entity Framework vytvořit databázi průběžně.

Začnete vytvořením tříd entit, které definují datové modely pro aplikaci webových formulářů. Pak vytvoříte kontextovou třídu, která bude spravovat třídy entit a poskytuje přístup k datům databáze. Vytvoří se také Třída inicializátoru, kterou použijete k naplnění databáze.

### <a name="entity-framework-and-references"></a>Entity Framework a odkazy

Ve výchozím nastavení je Entity Framework k dispozici při vytváření nové **webové aplikace ASP.NET** pomocí šablony **webových formulářů** . Entity Framework může být nainstalováno, odinstalováno a aktualizováno jako balíček NuGet.

Tento balíček NuGet obsahuje následující sestavení **modulu runtime** v rámci projektu:

- EntityFramework. dll – všechen Společný běhový kód používaný Entity Framework
- EntityFramework. SqlServer. dll – poskytovatel Microsoft SQL Server pro Entity Framework

### <a name="entity-classes"></a>Třídy entit

Třídy, které vytvoříte pro definování schématu dat, se nazývají třídy entit. Pokud s návrhem databází začínáte, můžete třídy entit představit jako definice tabulek v databázi. Každá vlastnost ve třídě Určuje sloupec v tabulce databáze. Tyto třídy poskytují odlehčené objektově-relační rozhraní mezi objektově orientovaným kódem a strukturou relační tabulky databáze.

V tomto kurzu začnete přidáním jednoduchých tříd entit, které představují schémata pro produkty a kategorie. Třída Products bude obsahovat definice pro každý produkt. Název každého člena třídy produktu bude `ProductID`, `ProductName`, `Description`, `ImagePath`, `UnitPrice`, `CategoryID`a `Category`. Třída Category bude obsahovat definice pro každou kategorii, do které může produkt patřit, jako je auto, člun nebo rovina. Název každého člena třídy Category bude `CategoryID`, `CategoryName`, `Description`a `Products`. Každý produkt bude patřit do jedné z kategorií. Tyto třídy entit budou přidány do existující složky *modelů* projektu.

1. V **Průzkumník řešení**klikněte pravým tlačítkem na složku *modely* a pak vyberte **Přidat** -&gt; **Nová položka**. 

    ![Vytvoření nabídky Data Access Layer-New Item](create_the_data_access_layer/_static/image1.png)

   Zobrazí se dialogové okno **Přidat novou položku** .
2. V **části C# vizuál** z **nainstalovaného** podokna na levé straně vyberte **kód**. 

    ![Vytvoření nabídky Data Access Layer-New Item](create_the_data_access_layer/_static/image2.png)
3. V prostředním podokně vyberte **Třída** a pojmenujte tuto novou třídu *Product.cs*.
4. Klikněte na **Přidat**.  
   V editoru se zobrazí nový soubor třídy.
5. Nahraďte výchozí kód následujícím kódem:   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample1.cs)]
6. Vytvořte další třídu opakováním kroků 1 až 4, ale pojmenujte novou třídu *Category.cs* a nahraďte výchozí kód následujícím kódem:  

    [!code-csharp[Main](create_the_data_access_layer/samples/sample2.cs)]

Jak už jsme uvedli, třída `Category` představuje typ produktu, který je navržený pro prodej (například <a id="a"></a>&quot;auta&quot;, &quot;čluny&quot;, &quot;Rockets&quot;atd.), a třída `Product` představuje jednotlivé produkty (hračky) v databázi. Každá instance `Product` objektu bude odpovídat řádku v relační tabulce databáze a každá vlastnost třídy produkt bude namapována na sloupec v tabulce relační databáze. Později v tomto kurzu zkontrolujete data produktu obsažená v databázi.

### <a name="data-annotations"></a>Datové poznámky

Možná jste si všimli, že někteří členové tříd mají atributy, které určují podrobnosti o členu, například `[ScaffoldColumn(false)]`. Jedná se o *datové poznámky*. Atributy poznámky k datům mohou popsány, jak ověřit vstup uživatele pro daného člena, zadat jeho formátování a určit, jak se má modelovat při vytvoření databáze.

### <a name="context-class"></a>Context – třída

Chcete-li začít používat třídy pro přístup k datům, je nutné definovat třídu kontextu. Jak bylo zmíněno dříve, Třída Context spravuje třídy entit (například třídu `Product` a třídu `Category`) a poskytuje přístup k datům databáze.

Tento postup přidá novou C# kontextovou třídu do složky *modely* .

1. Klikněte pravým tlačítkem na složku *modely* a pak vyberte **Přidat** -&gt; **Nová položka**.   
   Zobrazí se dialogové okno **Přidat novou položku** .
2. V prostředním podokně vyberte **Třída** , pojmenujte ji *ProductContext.cs* a klikněte na **Přidat**.
3. Nahraďte výchozí kód obsažený ve třídě následujícím kódem:   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample3.cs)]

Tento kód přidá obor názvů `System.Data.Entity`, abyste měli přístup ke všem základním funkcím Entity Framework, které zahrnují možnost dotazování, vkládání, aktualizaci a odstraňování dat pomocí objektů se silnými typy.

Třída `ProductContext` představuje kontext databáze Entity Framework produktu, který zpracovává načítání, ukládání a aktualizaci instancí tříd `Product` v databázi. Třída `ProductContext` je odvozena od `DbContext` základní třídy poskytované Entity Framework.

### <a name="initializer-class"></a>Inicializátor – třída

Při prvním použití kontextu bude nutné spustit určitou vlastní logiku pro inicializaci databáze. Tím umožníte přidání počátečních dat do databáze, abyste mohli hned Zobrazit produkty a kategorie.

Tento postup přidá do složky C# *modely* novou třídu inicializátoru.

1. Vytvořte další `Class` ve složce *modely* a pojmenujte ji *ProductDatabaseInitializer.cs*.
2. Nahraďte výchozí kód obsažený ve třídě následujícím kódem:   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample4.cs)]

Jak vidíte z výše uvedeného kódu, při vytvoření a inicializaci databáze je vlastnost `Seed` přepsána a nastavena. Při nastavení vlastnosti `Seed` se k naplnění databáze použijí hodnoty z kategorií a produktů. Pokud se pokusíte aktualizovat počáteční data úpravou výše uvedeného kódu po vytvoření databáze, při spuštění webové aplikace se nezobrazí žádné aktualizace. Důvodem je, že výše uvedený kód používá implementaci třídy `DropCreateDatabaseIfModelChanges` k rozpoznání, zda byl model (schéma) změněn před resetováním počátečních dat. Pokud nejsou provedeny žádné změny `Category` a `Product` třídy entit, databáze nebude znovu inicializována daty počáteční hodnoty.

> [!NOTE] 
> 
> Pokud jste chtěli, aby se databáze znovu nevytvořila při každém spuštění aplikace, můžete místo `DropCreateDatabaseIfModelChanges` třídy použít třídu `DropCreateDatabaseAlways`. Pro tuto řadu kurzů ale použijte třídu `DropCreateDatabaseIfModelChanges`.

V tomto okamžiku v tomto kurzu budete mít složku *modelů* se čtyřmi novými třídami a jednu výchozí třídou:

![Vytvoření složky modelů pro přístup k datům](create_the_data_access_layer/_static/image3.png)

### <a name="configuring-the-application-to-use-the-data-model"></a>Konfigurace aplikace pro použití datového modelu

Nyní, když jste vytvořili třídy, které reprezentují data, je nutné nakonfigurovat aplikaci tak, aby používala třídy. V souboru *Global. asax* přidáte kód, který inicializuje model. V souboru *Web. config* přidáte informace, které aplikaci sdělují, jakou databázi budete používat k ukládání dat reprezentovaných novými datovými třídami. Soubor *Global. asax* lze použít ke zpracování událostí nebo metod aplikace. Soubor *Web. config* umožňuje řídit konfiguraci webové aplikace v ASP.NET.

#### <a name="updating-the-globalasax-file"></a>Aktualizace souboru Global. asax

Chcete-li inicializovat datové modely při spuštění aplikace, aktualizujte obslužnou rutinu `Application_Start` v souboru *Global.asax.cs* .

> [!NOTE] 
> 
> V Průzkumník řešení můžete pro úpravu souboru *Global.asax.cs* vybrat soubor *Global. asax* nebo soubor *Global.asax.cs* .

1. Přidejte následující kód zvýrazněný žlutě do metody `Application_Start` v souboru *Global.asax.cs* .   

    [!code-csharp[Main](create_the_data_access_layer/samples/sample5.cs?highlight=9-10,22-23)]

> [!NOTE] 
> 
> Aby mohl váš prohlížeč zobrazit kód zvýrazněný žlutě při zobrazení této série kurzů v prohlížeči, musí podporovat HTML5.

Jak je znázorněno ve výše uvedeném kódu, aplikace při spuštění aplikace určuje inicializátor, který se spustí při prvním otevření dat. Pro přístup k objektu `Database` a objektu `ProductDatabaseInitializer` jsou vyžadovány dva další obory názvů.

 Úprava souboru Web. config 

I když Entity Framework Code First vygeneruje databázi pro vás ve výchozím umístění v případě, že je databáze naplněná daty o základech, přidání vlastních informací o připojení do vaší aplikace vám umožní řídit umístění databáze. Toto připojení k databázi zadáte pomocí připojovacího řetězce v souboru *Web. config* aplikace v kořenovém adresáři projektu. Přidáním nového připojovacího řetězce můžete směrovat umístění databáze (*wingtiptoys. mdf*), aby byla sestavena v datovém adresáři aplikace (*data aplikace\_* ), nikoli ve výchozím umístění. Tato změna vám umožní vyhledat a prozkoumat databázový soubor později v tomto kurzu.

1. V **Průzkumník řešení**vyhledejte a otevřete soubor *Web. config* .
2. Přidejte připojovací řetězec zvýrazněný žlutě do části `<connectionStrings>` souboru *Web. config* následujícím způsobem:  

    [!code-xml[Main](create_the_data_access_layer/samples/sample6.xml?highlight=4-7)]

Při prvním spuštění aplikace bude databáze sestavena v umístění určeném připojovacím řetězcem. Ale před spuštěním aplikace si ji nejdřív sestavíme.

## <a name="building-the-application"></a>Sestavení aplikace

Chcete-li zajistit, aby všechny třídy a změny fungovaly v rámci vaší webové aplikace, měli byste sestavit aplikaci.

1. V nabídce **ladění** vyberte **sestavení WingtipToys**.  
 Zobrazí se okno **výstup** a pokud se všechno objevilo správně, zobrazí se zpráva o *úspěšném* dokončení.  

    ![Vytvoření výstupních oken vrstvy přístupu k datům](create_the_data_access_layer/_static/image4.png)

Pokud narazíte na chybu, znovu proveďte kontrolu výše uvedených kroků. Informace v okně **výstup** označují, který soubor má problém a kde je požadováno změny v souboru. Tyto informace vám umožní určit, jakou část výše uvedených kroků je potřeba zkontrolovat a opravit v projektu.

## <a name="summary"></a>Souhrn

V tomto kurzu řady, kterou jste vytvořili datový model, a také přidejte kód, který bude použit k inicializaci a osazení databáze. Aplikaci jste také nakonfigurovali tak, aby používala datové modely při spuštění aplikace.

V dalším kurzu aktualizujete uživatelské rozhraní, přidáte navigaci a načtete data z databáze. Výsledkem bude, že se databáze automaticky vytvoří na základě tříd entit, které jste vytvořili v tomto kurzu.

## <a name="additional-resources"></a>Další prostředky

[Přehled Entity Framework](https://msdn.microsoft.com/library/bb399567.aspx)   
[Příručka pro začátečníky k ADO.NET Entity Framework](https://msdn.microsoft.com/data/ee712907)   
[Code First vývoj s](http://www.msteched.com/2010/Europe/DEV212) využitím Entity Framework (video)   
[Code First vztahů – rozhraní API Fluent](https://msdn.microsoft.com/data/hh134698)   
[Code First datové poznámky](https://msdn.microsoft.com/data/gg193958)  
[Vylepšení produktivity Entity Framework](https://blogs.msdn.com/b/efdesign/archive/2010/06/21/productivity-improvements-for-the-entity-framework.aspx?wa=wsignin1.0)

> [!div class="step-by-step"]
> [Předchozí](create-the-project.md)
> [Další](ui_and_navigation.md)

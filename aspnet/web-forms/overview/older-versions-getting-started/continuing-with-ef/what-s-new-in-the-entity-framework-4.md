---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
title: Co je nového v Entity Framework 4,0 | Microsoft Docs
author: tdykstra
description: Tato řada kurzů se sestavuje na webové aplikaci Contoso University, která je vytvořená Začínáme pomocí řady kurzů Entity Framework 4,0. I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: 393df4a8-b1db-44c4-9db7-2b533ca887d0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/what-s-new-in-the-entity-framework-4
msc.type: authoredcontent
ms.openlocfilehash: 29d2bd61e8361b130e7b9415dad4fe1d5b847945
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78642672"
---
# <a name="whats-new-in-the-entity-framework-40"></a>Novinky v sadě Entity Framework 4.0

tím, že [Dykstra](https://github.com/tdykstra)

> Tato řada kurzů se sestavuje na webové aplikaci Contoso University, která je vytvořená [Začínáme pomocí řady Entity Framework](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md) kurzů. Pokud jste nedokončili předchozí kurzy, jako výchozí bod tohoto kurzu si můžete aplikaci, kterou jste vytvořili, [Stáhnout](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) . Můžete si také [Stáhnout aplikaci](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) , která je vytvořená úplnou řadou kurzů. Pokud máte dotazy k kurzům, můžete je publikovat na [fórum ASP.NET Entity Framework](https://forums.asp.net/1227.aspx).

V předchozím kurzu jste viděli některé metody pro maximalizaci výkonu webové aplikace, která používá Entity Framework. V tomto kurzu se seznámíte s některými nejdůležitějšími novými funkcemi ve verzi 4 Entity Framework a odkazuje na prostředky, které poskytují ucelenější Úvod ke všem novým funkcím. Mezi funkce zvýrazněné v tomto kurzu patří následující:

- Přidružení cizího klíče.
- Spouští se uživatelsky definované příkazy SQL.
- Modelem při prvním vývoji.
- Podpora POCO

Kromě toho kurz krátce zavádí *vývoj kódu jako první*, funkce, která je součástí příští verze Entity Framework.

Chcete-li spustit kurz, spusťte aplikaci Visual Studio a otevřete webovou aplikaci Contoso University, se kterou jste pracovali v předchozím kurzu.

## <a name="foreign-key-associations"></a>Přidružení cizího klíče

Verze 3,5 Entity Framework zahrnovala navigační vlastnosti, ale v datovém modelu neobsahovala vlastnosti cizího klíče. Například sloupce `CourseID` a `StudentID` tabulky `StudentGrade` budou v `StudentGrade` entitě vynechány.

[![Image01](what-s-new-in-the-entity-framework-4/_static/image2.png)](what-s-new-in-the-entity-framework-4/_static/image1.png)

Důvodem tohoto přístupu bylo, že při naprosto řečeno, cizí klíče jsou podrobnosti fyzické implementace a nepatří do modelu konceptuálního data. Nicméně jako praktická záležitost je často snazší pracovat s entitami v kódu, když máte přímý přístup k cizím klíčům.

Příklad toho, jak cizí klíče v datovém modelu mohou zjednodušit váš kód, zvažte, jak byste museli kód stránky *DepartmentsAdd. aspx* nastavovat bez nich. V entitě `Department` je vlastnost `Administrator` cizí klíč, který odpovídá `PersonID` v `Person` entitě. Aby bylo možné navázat přidružení mezi novým oddělením a jeho správcem, je nutné nastavit hodnotu vlastnosti `Administrator` v obslužné rutině události `ItemInserting` ovládacího prvku DataBound:

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample1.cs)]

Bez cizích klíčů v datovém modelu byste měli zpracovat událost `Inserting` ovládacího prvku zdroje dat namísto `ItemInserting` události ovládacího prvku datové vazby, aby bylo možné získat odkaz na entitu samu před přidáním entity do sady entit. Když máte tento odkaz, vytvoříte přidružení pomocí kódu, jako v následujících příkladech:

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample2.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample3.cs)]

Jak vidíte v příspěvku na blogu Entity Framework týmu [při přidružení cizího klíče](https://blogs.msdn.com/b/efdesign/archive/2009/03/16/foreign-keys-in-the-entity-framework.aspx), existují i jiné případy, kdy je rozdíl v složitosti kódu mnohem větší. Pro splnění potřeb těch, kteří raději chtějí pracovat s podrobnostmi o implementaci v modelu konceptuálních dat pro účely zjednodušení kódu, vám Entity Framework nyní poskytuje možnost zahrnout cizí klíče v datovém modelu.

Pokud v rámci Entity Framework terminologie zahrnete cizí klíče do datového modelu, ve kterém používáte *přidružení cizího klíče*, a Pokud vyloučíte cizí klíče, používáte *nezávislé přidružení*.

## <a name="executing-user-defined-sql-commands"></a>Provádění uživatelsky definovaných příkazů SQL

V dřívějších verzích Entity Framework neexistoval snadný způsob, jak rychle vytvořit vlastní příkazy SQL a spustit je. Buď Entity Framework dynamicky generované příkazy SQL pro vás, nebo jste museli vytvořit uloženou proceduru a naimportovat ji jako funkci. Verze 4 přidává `ExecuteStoreQuery` a `ExecuteStoreCommand` metody třída `ObjectContext`, která usnadňuje předání jakýchkoli dotazů přímo do databáze.

Předpokládejme, že správci škol společnosti Contoso chtějí provádět hromadné změny v databázi bez nutnosti projít procesem vytvoření uložené procedury a jejich importem do datového modelu. První požadavek je na stránku, která umožňuje změnit počet kreditů pro všechny kurzy v databázi. Na webové stránce chtějí být schopni zadat číslo, které se má použít k vynásobení hodnoty každého sloupce `Credits` sloupce `Course` řádku.

Vytvořte novou stránku, která používá hlavní stránku *Web. Master* a pojmenujte ji *UpdateCredits. aspx*. Pak přidejte následující značku do ovládacího prvku `Content` s názvem `Content2`:

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample4.aspx)]

Tento kód vytvoří ovládací prvek `TextBox`, ve kterém může uživatel zadat hodnotu násobitele, `Button` ovládací prvek pro kliknutí, aby mohl příkaz Spustit, a ovládací prvek `Label` pro určení počtu ovlivněných řádků.

Otevřete *UpdateCredits.aspx.cs*a přidejte následující příkaz `using` a obslužnou rutinu pro událost `Click` tlačítka:

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample5.cs)]

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample6.cs)]

Tento kód spustí příkaz SQL `Update` pomocí hodnoty v textovém poli a pomocí popisku zobrazí počet ovlivněných řádků. Než spustíte stránku, spusťte stránku *kurzy. aspx* a získejte "před" obrázkem některých dat "před".

[![Image02](what-s-new-in-the-entity-framework-4/_static/image4.png)](what-s-new-in-the-entity-framework-4/_static/image3.png)

Spusťte *UpdateCredits. aspx*, jako násobitel zadejte "10" a pak klikněte na **provést**.

[![Image03](what-s-new-in-the-entity-framework-4/_static/image6.png)](what-s-new-in-the-entity-framework-4/_static/image5.png)

Opětovným spuštěním stránky *kurzy. aspx* zobrazíte změněná data.

[![Image04](what-s-new-in-the-entity-framework-4/_static/image8.png)](what-s-new-in-the-entity-framework-4/_static/image7.png)

(Pokud chcete nastavit počet kreditů zpátky na jejich původní hodnoty, v *UpdateCredits.aspx.cs* změnit `Credits * {0}` na `Credits / {0}` a znovu spustit stránku, a to zadáním hodnoty 10 jako dělitele.)

Další informace o provádění dotazů, které definujete v kódu, naleznete v tématu [How to: přímo Execute Commands to a Source (zdroj dat](https://msdn.microsoft.com/library/ee358769.aspx)).

## <a name="model-first-development"></a>Model – při prvním vývoji

V těchto návodech jste nejprve vytvořili databázi a následně vygenerovali datový model na základě struktury databáze. V Entity Framework 4 můžete místo toho začít s datovým modelem a vygenerovat databázi na základě struktury datového modelu. Pokud vytváříte aplikaci, pro kterou databáze ještě neexistuje, přístup k prvnímu modelu vám umožní vytvořit entity a vztahy, které jsou pro aplikaci velmi vhodné, ale nedělejte si starosti s podrobnostmi o fyzické implementaci. . (To ale platí jenom v počátečních fázích vývoje. Nakonec se databáze vytvoří a v ní budou mít produkční data a jejich opětovné vytvoření z modelu už nebude praktické. v tomto okamžiku se vrátíte k přístupu k databázi.)

V této části kurzu vytvoříte jednoduchý datový model a vygenerujete z něj databázi.

V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku *dal* a vyberte možnost **Přidat novou položku**. V dialogovém okně **Přidat novou položku** vyberte v části **Nainstalované šablony** možnost **Data** a pak vyberte šablonu **ADO.NET model EDM (Entity Data Model)** . Pojmenujte nový soubor *AlumniAssociationModel. edmx* a klikněte na **Přidat**.

[![Image06](what-s-new-in-the-entity-framework-4/_static/image10.png)](what-s-new-in-the-entity-framework-4/_static/image9.png)

Tím se spustí Průvodce model EDM (Entity Data Model). V kroku **zvolit obsah modelu** vyberte možnost **prázdný model** a potom klikněte na tlačítko **Dokončit**.

[![Image07](what-s-new-in-the-entity-framework-4/_static/image12.png)](what-s-new-in-the-entity-framework-4/_static/image11.png)

Otevře se **návrhář model EDM (Entity Data Model)** s prázdnou návrhovou plochou. Přetáhněte položku **entity** ze sady **nástrojů** na návrhovou plochu.

[![Image08](what-s-new-in-the-entity-framework-4/_static/image14.png)](what-s-new-in-the-entity-framework-4/_static/image13.png)

Změňte název entity z `Entity1` na `Alumnus`, změňte název vlastnosti `Id` na `AlumnusId`a přidejte novou skalární vlastnost s názvem `Name`. Chcete-li přidat nové vlastnosti, můžete po změně názvu `Id` sloupce stisknout klávesu ENTER, nebo kliknout pravým tlačítkem myši na entitu a vybrat možnost **Přidat skalární vlastnost**. Výchozím typem pro nové vlastnosti je `String`, což je pro tuto jednoduchou ukázku jemné, ale samozřejmě můžete změnit například datový typ v okně **vlastnosti** .

Vytvořte další entitu stejným způsobem a pojmenujte ji `Donation`. Změňte vlastnost `Id` na `DonationId` a přidejte skalární vlastnost s názvem `DateAndAmount`.

[![Image09](what-s-new-in-the-entity-framework-4/_static/image16.png)](what-s-new-in-the-entity-framework-4/_static/image15.png)

Chcete-li přidat přidružení mezi těmito dvěma entitami, klikněte pravým tlačítkem myši na entitu `Alumnus`, vyberte možnost **Přidat**a poté vyberte možnost **přidružení**.

[![Image10](what-s-new-in-the-entity-framework-4/_static/image18.png)](what-s-new-in-the-entity-framework-4/_static/image17.png)

Výchozí hodnoty v dialogovém okně **Přidat přidružení** jsou to, co chcete (jeden-mnoho, zahrnout navigační vlastnosti, zahrnout cizí klíče), takže stačí kliknout na **OK**.

[![Image11](what-s-new-in-the-entity-framework-4/_static/image20.png)](what-s-new-in-the-entity-framework-4/_static/image19.png)

Návrhář přidá čáru přidružení a vlastnost cizího klíče.

[![Image12](what-s-new-in-the-entity-framework-4/_static/image22.png)](what-s-new-in-the-entity-framework-4/_static/image21.png)

Teď jste připraveni vytvořit databázi. Klikněte pravým tlačítkem myši na návrhovou plochu a vyberte možnost **Generovat databázi z modelu**.

[![Image13](what-s-new-in-the-entity-framework-4/_static/image24.png)](what-s-new-in-the-entity-framework-4/_static/image23.png)

Tím se spustí Průvodce generováním databáze. (Pokud se zobrazí upozornění indikující, že tyto entity nejsou namapované, můžete je po dobu ignorovat.)

V kroku **Vyberte datové připojení** klikněte na **nové připojení**.

[![Image14](what-s-new-in-the-entity-framework-4/_static/image26.png)](what-s-new-in-the-entity-framework-4/_static/image25.png)

V dialogovém okně **Vlastnosti připojení** vyberte instanci Local SQL Server Express a pojmenujte `AlumniAssociation`databáze.

[![Image15](what-s-new-in-the-entity-framework-4/_static/image28.png)](what-s-new-in-the-entity-framework-4/_static/image27.png)

Pokud se zobrazí dotaz, zda chcete vytvořit databázi, klikněte na tlačítko **Ano** . Po opětovném zobrazení kroku **Vybrat datové připojení** klikněte na tlačítko **Další**.

V kroku **Souhrn a nastavení** klikněte na **Dokončit**.

[![Image18](what-s-new-in-the-entity-framework-4/_static/image30.png)](what-s-new-in-the-entity-framework-4/_static/image29.png)

Vytvoří se soubor *. SQL* s příkazy jazyka DDL (Data Definition Language), ale příkazy se ještě nespouštěly.

[![Image20](what-s-new-in-the-entity-framework-4/_static/image32.png)](what-s-new-in-the-entity-framework-4/_static/image31.png)

Pomocí nástroje, jako je například **SQL Server Management Studio** , spusťte skript a vytvořte tabulky, jak jste to mohli udělat při vytváření databáze `School` pro [první kurz v řadě kurzů Začínáme](../getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1.md). (Pokud jste nestáhli databázi.)

Model `AlumniAssociation` dat můžete nyní použít na webových stránkách stejným způsobem jako model `School`. Pokud to chcete vyzkoušet, přidejte do tabulek nějaká data a vytvořte webovou stránku, která zobrazí data.

Pomocí **Průzkumník serveru**přidejte následující řádky do tabulek `Alumnus` a `Donation`.

[![Image21](what-s-new-in-the-entity-framework-4/_static/image34.png)](what-s-new-in-the-entity-framework-4/_static/image33.png)

Vytvořte novou webovou stránku s názvem *absolventů. aspx* , která používá hlavní stránku *site. Master* . Přidejte následující značku do ovládacího prvku `Content` s názvem `Content2`:

[!code-aspx[Main](what-s-new-in-the-entity-framework-4/samples/sample7.aspx)]

Tento kód vytvoří vnořené ovládací prvky `GridView`, vnějším, aby zobrazila názvy absolventů a vnitřní název pro zobrazení dat a částek daru.

Otevřete *Alumni.aspx.cs*. Přidejte příkaz `using` pro vrstvu přístupu k datům a obslužnou rutinu události `RowDataBound` vnějšího ovládacího prvku `GridView`:

[!code-csharp[Main](what-s-new-in-the-entity-framework-4/samples/sample8.cs)]

Tento kód sváže ovládací prvek vnitřní `GridView` pomocí vlastnosti `Donations` navigace pro `Alumnus` entitu aktuálního řádku.

Spusťte stránku.

[![Image22](what-s-new-in-the-entity-framework-4/_static/image36.png)](what-s-new-in-the-entity-framework-4/_static/image35.png)

(Poznámka: Tato stránka je součástí projektu ke stažení, ale aby ji bylo možné využít, musíte vytvořit databázi v místní instanci SQL Server Express; databáze není zahrnutá jako soubor *. mdf* ve složce *App\_data* .)

Další informace o použití funkce model-First Entity Framework najdete v tématu [model – první v Entity Framework 4](https://msdn.microsoft.com/data/ff830362.aspx).

## <a name="poco-support"></a>Podpora objektů POCO

Pokud používáte metodologii návrhu založenou na doméně, navrhujete třídy dat, které reprezentují data a chování, které jsou relevantní pro obchodní doménu. Tyto třídy by měly být nezávislé na jakékoli konkrétní technologii, která se používá k uložení (uchování) dat; Jinými slovy, by měly být *ignorovány*. Ignorování trvalosti může také usnadnit testování třídy, protože projekt testování částí může použít jakoukoli technologii trvalosti pro testování. Starší verze Entity Framework nabízely omezené podpory pro ignorování trvalého chování, protože třídy entit musely dědit od `EntityObject` třídy a proto zahrnovaly skvělou možnost Entity Framework specifických funkcí.

Entity Framework 4 zavádí možnost použít třídy entit, které nejsou děděny z `EntityObject` třídy, a proto jsou ignorovány trvalé. V kontextu Entity Framework třídy, jako je toto, jsou obvykle označovány jako *obyčejné, staré objekty CLR* (POCO nebo POCOs). Třídy POCO můžete napsat ručně, nebo je můžete automaticky vygenerovat na základě existujícího datového modelu pomocí šablon sady text Template Transformation Toolkit (T4), které poskytuje Entity Framework.

Další informace o použití POCOs v Entity Framework najdete v následujících zdrojích informací:

- [Práce s entitami POCO](https://msdn.microsoft.com/library/dd456853.aspx) Jedná se o dokument MSDN s přehledem POCOs s odkazy na další dokumenty s podrobnějšími informacemi.
- [Návod: Šablona POCO pro Entity Framework](https://blogs.msdn.com/b/adonet/archive/2010/01/25/walkthrough-poco-template-for-the-entity-framework.aspx) Toto je Blogový příspěvek z Entity Framework vývojového týmu s odkazy na další blogové příspěvky o POCOs.

## <a name="code-first-development"></a>Vývoj pro první kód

Podpora POCO v Entity Framework 4 stále vyžaduje, abyste vytvořili datový model a provedli propojení tříd entit s datovým modelem. Další verze Entity Framework bude obsahovat funkci s názvem *vývoj při prvním vývoji kódu*. Tato funkce umožňuje použít Entity Framework s vlastními třídami POCO bez nutnosti použít buď Návrhář datového modelu, nebo soubor XML datového modelu. (Proto tato možnost byla také volána *pouze kód*; *kód – First* a *Code –* oba odkazují na stejnou funkci Entity Framework.)

Další informace o použití přístupu Code-First k vývoji najdete v následujících zdrojích informací:

- [Vývoj kódu při prvním Entity Framework 4](https://weblogs.asp.net/scottgu/archive/2010/07/16/code-first-development-with-entity-framework-4.aspx). Toto je Blogový příspěvek, který Scott Guthrie zavádí vývoj kódu jako první.
- [Blog vývojového týmu Entity Framework – příspěvky s příznakem CodeOnly](https://blogs.msdn.com/b/efdesign/archive/tags/codeonly/)
- [Blog vývojového týmu Entity Framework – příspěvky s příznakem Code First](https://blogs.msdn.com/b/efdesign/archive/tags/code+first/)
- [Kurz pro hudební úložiště MVC – část 4: modely a přístup k datům](../../../../mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4.md)
- [Začínáme s MVC 3 – část 4: Entity Framework vývoj kódu jako první](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-model.md)

Kromě toho nový kurz pro první kód MVC, který sestaví aplikaci podobnou aplikaci společnosti Contoso University, se zveřejňuje na jaře 2011 v [https://asp.net/entity-framework/tutorials](../../../../entity-framework.md)

## <a name="more-information"></a>Další informace

Tím se dokončí přehled, co je nového v Entity Framework a tím se pokračuje v Entity Framework řadě kurzů. Další informace o nových funkcích v Entity Framework 4, které zde nejsou popsané, najdete v následujících zdrojích informací:

- [Co je nového v ADO.NET](https://msdn.microsoft.com/library/ex6y04yf.aspx) Téma MSDN o nových funkcích ve verzi 4 Entity Framework.
- [Oznamujeme vydání Entity Framework 4](https://blogs.msdn.com/b/efdesign/archive/2010/04/12/announcing-the-release-of-entity-framework-4.aspx) Blogový příspěvek Entity Framework týmu vývoje o nových funkcích verze 4.

> [!div class="step-by-step"]
> [Předchozí](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)

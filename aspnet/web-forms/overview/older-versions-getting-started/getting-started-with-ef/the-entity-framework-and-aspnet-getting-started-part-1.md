---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1
title: Začínáme s Entity Framework 4,0 Database First a webovými formuláři ASP.NET 4 | Microsoft Docs
author: tdykstra
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet ASP.NET aplikace webových formulářů pomocí Entity Framework 4,0 a sady Visual Studio 2010...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 5cb00916-8f46-491f-be25-4739a615d619
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-1
msc.type: authoredcontent
ms.openlocfilehash: fd88b32ad2a65e5b4c7ead15f0d6dc5dc6e97e75
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78630457"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms"></a>Začínáme s webovými formuláři Entity Framework 4,0 Database First a ASP.NET 4

tím, že [Dykstra](https://github.com/tdykstra)

> Ukázková webová aplikace společnosti Contoso University ukazuje, jak pomocí Entity Framework 4,0 a sady Visual Studio 2010 vytvářet aplikace webových formulářů ASP.NET. Ukázková aplikace je web pro fiktivní univerzitě společnosti Contoso. Zahrnuje funkce, jako student přijetí, kurz vytvoření a přiřazení instruktorem.
> 
> V tomto kurzu se zobrazí C#příklady v. [Ukázka ke stažení](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) obsahuje kód v obou C# i Visual Basic.
> 
> ## <a name="database-first"></a>Database First
> 
> Existují tři způsoby, jak můžete pracovat s daty v Entity Framework: *Database First*, *model First*a *Code First*. Tento kurz je určen pro Database First. Informace o rozdílech mezi těmito pracovními postupy a pokyny pro výběr nejvhodnějšího řešení pro váš scénář najdete v tématu [Entity Framework vývojové pracovní postupy](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).
> 
> ## <a name="web-forms"></a>Webové formuláře
> 
> Tato série kurzů používá model webových formulářů ASP.NET a předpokládá, že víte, jak pracovat s webovými formuláři ASP.NET v sadě Visual Studio. Pokud to neuděláte, přečtěte si téma [Začínáme s webovými formuláři ASP.NET 4,5](../../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md). Pokud dáváte přednost práci s architekturou ASP.NET MVC, přečtěte si téma [Začínáme s Entity Framework pomocí ASP.NET MVC](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).
> 
> ## <a name="software-versions"></a>Verze softwaru
> 
> | **Zobrazuje se v tomto kurzu.** | **Funguje taky s** |
> | --- | --- |
> | Windows 7 | Windows 8 |
> | Visual Studio 2010 | Visual Studio 2010 Express for Web. Kurz nebyl testován s novějšími verzemi sady Visual Studio. Výběry nabídek, dialogová okna a šablony obsahují mnoho rozdílů. |
> | .NET 4 | .NET 4,5 je zpětně kompatibilní s .NET 4, ale kurz nebyl testován pomocí .NET 4,5. |
> | Entity Framework 4 | Kurz nebyl testován s novějšími verzemi Entity Framework. Počínaje Entity Framework 5, EF používá ve výchozím nastavení `DbContext API` zavedené pomocí EF 4,1. Ovládací prvek EntityDataSource byl navržený tak, aby používal rozhraní `ObjectContext` API. Informace o tom, jak používat ovládací prvek EntityDataSource s rozhraním `DbContext` API, najdete v [tomto blogovém příspěvku](https://blogs.msdn.com/b/webdev/archive/2012/09/13/how-to-use-the-entitydatasource-control-with-entity-framework-code-first.aspx). |
> 
> ## <a name="questions"></a>Otázky
> 
> Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra ASP.NET Entity Framework](https://forums.asp.net/1227.aspx), [Entity Framework a LINQ to Entities fóra](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)nebo [StackOverflow.com](http://stackoverflow.com/).

## <a name="overview"></a>Přehled

Aplikace, kterou budete sestavovat v těchto kurzech, je jednoduchý web na univerzitě.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-1/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image1.png)

Uživatelé mohou zobrazit a aktualizovat Všichni studenti, kurz a informace instruktorem. Níže jsou uvedené některé obrazovky, které vytvoříte.

[![Image30](the-entity-framework-and-aspnet-getting-started-part-1/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image3.png)

[![Image37](the-entity-framework-and-aspnet-getting-started-part-1/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image5.png)

[![Image31](the-entity-framework-and-aspnet-getting-started-part-1/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image7.png)

[![Image32](the-entity-framework-and-aspnet-getting-started-part-1/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image9.png)

## <a name="creating-the-web-application"></a>Vytvoření webové aplikace

Chcete-li spustit kurz, otevřete aplikaci Visual Studio a pak vytvořte nový projekt webové aplikace ASP.NET pomocí šablony **webové aplikace ASP.NET** :

[![Image01](the-entity-framework-and-aspnet-getting-started-part-1/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image11.png)

Tato šablona vytvoří projekt webové aplikace, který již obsahuje šablonu stylů a stránky předlohy:

[![Image02](the-entity-framework-and-aspnet-getting-started-part-1/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image13.png)

Otevřete soubor *Web. Master* a změňte "moje aplikace ASP.NET" na "contoso University".

[!code-html[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample1.html)]

Vyhledejte ovládací prvek *nabídky* s názvem `NavigationMenu` a nahraďte ho následujícím kódem, který přidá položky nabídky pro stránky, které budete vytvářet.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample2.aspx)]

Otevřete stránku *Default. aspx* a změňte `Content` ovládací prvek s názvem `BodyContent` na toto:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-1/samples/sample3.aspx)]

Teď máte jednoduchou domovskou stránku s odkazy na různé stránky, které budete vytvářet:

[![Image03](the-entity-framework-and-aspnet-getting-started-part-1/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image15.png)

## <a name="creating-the-database"></a>Vytvoření databáze

Pro tyto kurzy použijete návrháře Entity Framework Data Model k automatickému vytvoření datového modelu na základě existující databáze (často označované jako přístup k *databázi* ). Alternativou, která není pokrytá v této sérii kurzů, je vytvořit datový model ručně a potom nechat návrháře vytvořit skripty, které vytvoří databázi (přístup *modelovým a prvním* přístupem).

Pro první metodu databáze použitou v tomto kurzu je dalším krokem přidání databáze do lokality. Nejjednodušší způsob je nejprve stáhnout projekt, který je součástí tohoto kurzu. Pak klikněte pravým tlačítkem na složku *Data\_aplikace* , vyberte **Přidat existující položku**a ze staženého projektu vyberte soubor databáze *School. mdf* .

Alternativou je postup při [vytváření ukázkové databáze School](https://msdn.microsoft.com/library/bb399731.aspx). Bez ohledu na to, jestli si stáhnete databázi nebo ji vytvoříte, zkopírujte soubor *School. mdf* z následující složky do složky aplikace *\_data* aplikace:

`%PROGRAMFILES%\Microsoft SQL Server\MSSQL10.SQLEXPRESS\MSSQL\DATA`

(Toto umístění souboru *. mdf* předpokládá, že používáte SQL Server 2008 Express.)

Pokud vytvoříte databázi ze skriptu, proveďte následující kroky a vytvořte tak databázový diagram:

1. V **Průzkumník serveru**rozbalte **datová připojení**, rozbalte *School. mdf*, klikněte pravým tlačítkem na **databázové diagramy**a vyberte **Přidat nový diagram**.

    [![Image35](the-entity-framework-and-aspnet-getting-started-part-1/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image17.png)
2. Vyberte všechny tabulky a pak klikněte na **Přidat**.

    [![Image36](the-entity-framework-and-aspnet-getting-started-part-1/_static/image20.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image19.png)

    SQL Server vytvoří databázový diagram, který zobrazuje tabulky, sloupce v tabulkách a vztahy mezi tabulkami. Tabulky můžete přesouvat, abyste je mohli uspořádat tak, jak chcete.
3. Uložte diagram jako "SchoolDiagram" a zavřete ho.

Pokud si stáhnete soubor *School. mdf* , který je součástí tohoto kurzu, můžete zobrazit diagram databáze tak, že dvakrát kliknete na **SchoolDiagram** v části **databázové diagramy** v **Průzkumník serveru**.

[![Image38](the-entity-framework-and-aspnet-getting-started-part-1/_static/image22.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image21.png)

Diagram vypadá nějak takto (tabulky můžou být v různých umístěních, z čeho se tady zobrazuje):

[![Image04](the-entity-framework-and-aspnet-getting-started-part-1/_static/image24.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image23.png)

## <a name="creating-the-entity-framework-data-model"></a>Vytvoření datového modelu Entity Framework

Nyní můžete vytvořit datový model Entity Framework z této databáze. Datový model můžete vytvořit v kořenové složce aplikace, ale v tomto kurzu ho umístíte do složky s názvem *dal* (pro přístup k datům).

V **Průzkumník řešení**přidejte složku projektu s názvem *dal* (Ujistěte se, že je v rámci projektu, nikoli v rámci řešení).

Klikněte pravým tlačítkem na složku *dal* a pak vyberte **Přidat** a **Nová položka**. V části **Nainstalované šablony**vyberte **data**, vyberte šablonu **model EDM (Entity Data Model) ADO.NET** , pojmenujte ji *SchoolModel. edmx*a pak klikněte na **Přidat**.

[![Image05](the-entity-framework-and-aspnet-getting-started-part-1/_static/image26.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image25.png)

Spustí se Průvodce model EDM (Entity Data Model). V prvním kroku průvodce je ve výchozím nastavení vybraná možnost **Generovat z databáze** . Klikněte na **Další**.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-1/_static/image28.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image27.png)

V kroku **Vyberte datové připojení** ponechte výchozí hodnoty a klikněte na **Další**. Ve výchozím nastavení je vybrána školní databáze a nastavení připojení je uloženo v souboru *Web. config* jako **SchoolEntities**.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-1/_static/image30.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image29.png)

V kroku průvodce **Zvolte objekty databáze** vyberte všechny tabulky kromě `sysdiagrams` (které byly vytvořeny pro diagram, který jste vygenerovali dříve) a pak klikněte na **Dokončit**.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-1/_static/image32.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image31.png)

Po dokončení vytváření modelu Visual Studio zobrazí grafické znázornění Entity Framework objektů (entity), které odpovídají vašim tabulkám databáze. (Stejně jako u databázového diagramu se umístění jednotlivých prvků může lišit od toho, co vidíte na tomto obrázku. Pokud chcete, můžete přetáhnout prvky kolem obrázku tak, aby odpovídaly ilustraci.)

[![Image09](the-entity-framework-and-aspnet-getting-started-part-1/_static/image34.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image33.png)

## <a name="exploring-the-entity-framework-data-model"></a>Zkoumání Entity Framework datového modelu

Můžete vidět, že diagram entity vypadá velmi podobně jako databázový diagram, s několika rozdíly. Jedním rozdílem je přidání symbolů na konci každého přidružení, které určuje typ přidružení (vztahy mezi tabulkami se nazývají asociace entit v datovém modelu):

- Přidružení 1:1 je reprezentované "1" a "0.. 1".

    [![Image39](the-entity-framework-and-aspnet-getting-started-part-1/_static/image36.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image35.png)

    V takovém případě `Person` entita může nebo nemusí být přidružena k entitě `OfficeAssignment`. Entita `OfficeAssignment` musí být přidružena k entitě `Person`. Jinými slovy, instruktor může nebo nemusí být přiřazen k kanceláři a kterákoli kancelář může být přiřazena pouze jednomu instruktorovi.
- Přidružení 1:1 je reprezentované "1" a "\*".

    [![Image40](the-entity-framework-and-aspnet-getting-started-part-1/_static/image38.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image37.png)

    V takovém případě `Person` entita může nebo nemusí mít přidružené `StudentGrade` entity. Entita `StudentGrade` musí být přidružená k jedné entitě `Person`. `StudentGrade` entity ve skutečnosti reprezentují zaregistrované kurzy v této databázi; Pokud je student zaregistrovaný v kurzu a ještě neexistuje žádná známka, vlastnost `Grade` má hodnotu null. Jinými slovy, student ještě nemusí být zaregistrovaný v žádném kurzu, může být zaregistrovaný v jednom kurzu nebo může být zaregistrovaný ve více kurzech. Každá ze stupňů v zaregistrovaném kurzu se vztahuje jenom na jednoho studenta.
- Přidružení m:n je reprezentované "\*" a "\*".

    [![Image41](the-entity-framework-and-aspnet-getting-started-part-1/_static/image40.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image39.png)

    V takovém případě `Person` entita může nebo nemusí být přidružená `Course` entit a obrácená hodnota je také true: `Course` entita může nebo nemusí mít přidružené `Person` entity. Jinými slovy, instruktor může naučit několik kurzů a kurz může být výukou více instruktorů. (V této databázi se tato relace vztahuje pouze na instruktory; neodkazuje studenty na kurzy. Studenti jsou propojeni s kurzy podle tabulky StudentGrades.)

Dalším rozdílem mezi databázovým diagramem a datovým modelem je další část **navigační vlastnosti** pro každou entitu. Navigační vlastnost entity odkazuje na související entity. Například vlastnost `Courses` v entitě `Person` obsahuje kolekci všech entit `Course`, které souvisejí s entitou `Person`.

[![Image12](the-entity-framework-and-aspnet-getting-started-part-1/_static/image42.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image41.png)

Ještě jiný rozdíl mezi databází a datovým modelem je absence `CourseInstructor` tabulky přidružení, která se používá v databázi k propojení `Person` a `Course` tabulek v relaci m:n. Navigační vlastnosti umožňují získat související `Course` entit od `Person` entitu a související entity `Person` od `Course` entity, takže není nutné zastupovat tabulku přidružení v datovém modelu.

[![Image11](the-entity-framework-and-aspnet-getting-started-part-1/_static/image44.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image43.png)

Pro účely tohoto kurzu Předpokládejme, že sloupec `FirstName` `Person` tabulky ve skutečnosti obsahuje křestní jméno a prostřední jméno osoby. Chcete změnit název pole tak, aby odrážel tuto skutečnost, ale správce databáze (DBA) pravděpodobně nechce změnit databázi. V datovém modelu můžete změnit název vlastnosti `FirstName`, zatímco zůstane její ekvivalent databáze beze změny.

V návrháři klikněte pravým tlačítkem na **FirstName** v entitě `Person` a pak vyberte **Přejmenovat**.

[![Image13](the-entity-framework-and-aspnet-getting-started-part-1/_static/image46.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image45.png)

Zadejte nový název "FirstMidName". Tím se změní způsob, jakým odkazujete na sloupec v kódu beze změny databáze.

[![Image29](the-entity-framework-and-aspnet-getting-started-part-1/_static/image48.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image47.png)

Prohlížeč modelů poskytuje další způsob zobrazení struktury databáze, struktury datového modelu a mapování mezi nimi. Pokud se chcete podívat, klikněte pravým tlačítkem myši na prázdnou oblast v Návrháři entit a pak klikněte na **prohlížeč modelů**.

[![Image18](the-entity-framework-and-aspnet-getting-started-part-1/_static/image50.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image49.png)

Podokno **prohlížeč modelů** zobrazuje stromové zobrazení. (Podokno **prohlížeče modelů** může být ukotveno v podokně **Průzkumník řešení** .) Uzel **SchoolModel** představuje strukturu datového modelu a uzel **SchoolModel. Store** představuje databázovou strukturu.

[![Image26](the-entity-framework-and-aspnet-getting-started-part-1/_static/image52.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image51.png)

Rozbalte **SchoolModel. Store** , abyste viděli tabulky, rozbalíte **tabulky/zobrazení** , zobrazíte tabulky a potom **rozbalíte, abyste** viděli sloupce v tabulce.

[![Image19](the-entity-framework-and-aspnet-getting-started-part-1/_static/image54.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image53.png)

Rozbalte **SchoolModel**, rozbalte položku **typy entit**a potom rozbalte uzel **kurz** , abyste viděli entity a vlastnosti v rámci entit.

[![Image20](the-entity-framework-and-aspnet-getting-started-part-1/_static/image56.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image55.png)

V podokně návrháře nebo v **prohlížeči modelů** vidíte, jak Entity Framework vztahuje objekty dvou modelů. Klikněte pravým tlačítkem na entitu `Person` a vyberte **mapování tabulky**.

[![Image21](the-entity-framework-and-aspnet-getting-started-part-1/_static/image58.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image57.png)

Otevře se okno **Podrobnosti mapování** . Všimněte si, že toto okno vám umožní vidět, že sloupec databáze `FirstName` je namapovaný na `FirstMidName`, což je to, co jste ho přejmenovali v datovém modelu.

[![Image22](the-entity-framework-and-aspnet-getting-started-part-1/_static/image60.png)](the-entity-framework-and-aspnet-getting-started-part-1/_static/image59.png)

Entity Framework používá XML k ukládání informací o databázi, datovém modelu a mapování mezi nimi. Soubor *SchoolModel. edmx* je ve skutečnosti soubor XML, který obsahuje tyto informace. Návrhář vykresluje informace v grafickém formátu, ale můžete také zobrazit soubor XML kliknutím pravým tlačítkem myši na soubor *. edmx* v **Průzkumník řešení**, kliknutím na **otevřít v aplikaci**a výběrem **editoru XML (text)** . (Návrhář datového modelu a editor XML jsou pouhými dvěma různými způsoby otevření a práce se stejným souborem, takže nemůžete mít návrháře otevřený a otevřený soubor v editoru XML.)

Nyní jste vytvořili web, databázi a datový model. V dalším návodu začnete pracovat s daty pomocí datového modelu a ovládacího prvku ASP.NET `EntityDataSource`.

> [!div class="step-by-step"]
> [Next](the-entity-framework-and-aspnet-getting-started-part-2.md)

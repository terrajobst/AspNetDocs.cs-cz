---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
title: Použití místního kalendáře DatePicker HTML5 a jQuery UI s ASP.NET MVC – část 1 | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy práce s šablonami editoru, šablonami zobrazení a místním datepickerm ovládacího prvku jQuery uživatelského rozhraní v ASP.NET MV...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: c23d27f7-b0cf-44f2-8445-fb69e045c674
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1
msc.type: authoredcontent
ms.openlocfilehash: c1c2380f24c72f6aabaaacaf975e95288a384ff1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538988"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-1"></a>Použití místního kalendáře DatePicker HTML5 a jQuery UI s ASP.NET MVC – část 1

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> V tomto kurzu se seznámíte se základy práce s šablonami editoru, šablonami zobrazení a místním datepickerm ovládacího prvku jQuery uživatelského rozhraní ve webové aplikaci ASP.NET MVC.

V tomto kurzu se seznámíte se základy práce s šablonami editoru, šablonami zobrazení a [místním datepickerm](http://plugins.jquery.com/project/datepicker) ovládacího prvku jQuery uživatelského rozhraní ve webové aplikaci ASP.NET MVC. Pro účely tohoto kurzu můžete použít Microsoft Visual Web Developer 2010 Express Service Pack 1 (&quot;Visual Web Developer&quot;), což je bezplatná verze Microsoft Visual Studio, nebo můžete sadu Visual Studio 2010 SP1 použít i v případě, že ji už máte.

Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže. Všechny z nich můžete nainstalovat kliknutím na následující odkaz: instalace [webové platformy](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack). Případně můžete nainstalovat požadovaný software jednotlivě pomocí následujících odkazů:

- [Požadavky sady Visual Studio Web Developer Express SP1](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
- [Aktualizace nástrojů MVC 3 pro ASP.NET](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
- [SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(podpora modulu runtime + nástroje)

Pokud používáte sadu Visual Studio 2010 namísto aplikace Visual Web Developer, nainstalujte požadavky kliknutím na následující odkaz: [požadavky sady Visual studio 2010](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).

V tomto kurzu se předpokládá, že jste dokončili [Začínáme s kurzem MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) nebo jste obeznámeni s vývojem ASP.NET MVC. Tento kurz začíná dokončeným projektem z Začínáme kurzu [MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) .

V tomto kurzu se zobrazuje C#kód v. [Projekt Starter](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800) a dokončený projekt jsou však také k dispozici v Visual Basic.

Projekt sady Visual Studio se C# zdrojovým kódem a Visual Basic je k dispozici pro toto téma: [Stáhnout](https://archive.msdn.microsoft.com/Project/Download/FileDownload.aspx?ProjectName=aspnetmvcsamples&amp;DownloadId=15800).

### <a name="what-youll-build"></a>Co sestavíte

Do jednoduché aplikace pro výpis filmů, která byla vytvořena v kurzu [Začínáme s MVC 3](../getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) , přidáte šablony (konkrétně úpravy a zobrazení šablon). K zjednodušení procesu zadávání dat můžete také přidat místní nabídku [DatePicker uživatelského rozhraní jQuery](http://jqueryui.com/demos/datepicker/) . Následující snímek obrazovky ukazuje upravenou aplikaci se zobrazeným místním kalendářem DatePicker uživatelského rozhraní jQuery.

![dokončeno jQuery](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image1.png)

### <a name="skills-youll-learn"></a>Dovednosti, se kterými se naučíte

Tady je seznam toho, co se naučíte:

- Způsob použití atributů z oboru názvů [DataAnnotations](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.aspx) k řízení formátu dat po zobrazení a v režimu úprav.
- Vytváření šablon (úpravy a zobrazení šablon) k řízení formátování dat.
- Postup přidání [uživatelského rozhraní jQuery DatePicker](http://jqueryui.com/demos/datepicker/) jako způsobu, jak zadat pole data

### <a name="getting-started"></a>začínáme

Pokud ještě nemáte aplikaci se seznamem videí z počátečního projektu, Stáhněte si ji: 

* [Stáhnout](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).
* V Průzkumníku Windows klikněte pravým tlačítkem na soubor *MvcMovie. zip* a vyberte **vlastnosti**. 
* V dialogovém okně **vlastnosti MvcMovie. zip** vyberte **odblokovat**. (Odblokování zabraňuje upozornění zabezpečení, které se vyskytne při pokusu o použití souboru *. zip* , který jste stáhli z webu.)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image2.png)

Klikněte pravým tlačítkem na soubor *MvcMovie. zip* a vyberte **Rozbalit vše pro rozbalení** souboru. V aplikaci Visual Web Developer nebo v aplikaci Visual Studio 2010 otevřete soubor *MvcMovieCS\_. sln* .

V **Průzkumník řešení**dvakrát klikněte na *Views\Shared\\_Layout. cshtml* a otevřete ho. Změňte hlavičku `H1` z **filmové aplikace MVC** na **video jQuery**. Stisknutím kombinace kláves CTRL + F5 spusťte aplikaci a klikněte na kartu **Domů** , která vás přesměruje na `Index` metodu kontroleru videí. Chcete-li vyzkoušet aplikaci, vyberte odkaz **Upravit** a odkaz **Podrobnosti** pro jeden z filmů. Všimněte si, že v zobrazení index, upravit a podrobnosti jsou informace o datu vydání a ceně v tomto formátu:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image3.png)

Formátování data a ceny je výsledkem použití atributu [DisplayFormat](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.displayformatattribute.aspx) u vlastností třídy `Movie`.

Otevřete soubor *Movie.cs* a odkomentujte atribut `DisplayFormat` ve vlastnostech `ReleaseDate` a `Price`. Výsledná `Movie` třída vypadá takto:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample1.cs)]

Stisknutím kombinace kláves CTRL + F5 znovu spusťte aplikaci a výběrem karty **Domů** zobrazte seznam filmů. Tentokrát datum vydání zobrazuje datum a čas a pole Price již nezobrazuje symbol měny. Vaše změny ve třídě `Movie` neudělaly formátování Skvělé, které jste viděli dříve, ale opravíte to za chvíli.

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/_static/image4.png)

### <a name="using-the-dataannotations-datatype-attribute-to-specify-the-data-type"></a>Použití atributu DataType anotace data k určení datového typu

Nahraďte atribut `DisplayFormat` s komentářem pro vlastnost `ReleaseDate` s atributem [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) pomocí výčtu `Date`. Nahraďte atribut `DisplayFormat` pro vlastnost `Price` pomocí atributu [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) znovu, tentokrát pomocí výčtu `Currency`. To je to, jak bude hotový kód vypadat:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-1/samples/sample2.cs)]

Spusťte aplikaci. Datum vydání verze a vlastnosti ceny jsou nyní formátovány správně (tj. pomocí vhodného formátu data a měny). Atribut [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) poskytuje metadata typu pro předdefinované šablony ASP.NET MVC, aby se pole vykreslila ve správném formátu. Použití atributu `DataType` je vhodnější použít atribut `DisplayFormat`, který byl původně v kódu, protože atribut `DataType` vytváří čisticí a flexibilnější model pro účely, jako je mezinárodní.

V další části se dozvíte, jak vytvořit vlastní šablony pro zobrazení datových polí.

> [!div class="step-by-step"]
> [Next](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)

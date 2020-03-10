---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
title: Přidání metody Create a zobrazení vytvořit | Microsoft Docs
author: shanselman
description: Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvořte jednoduchou webovou aplikaci, která čte a zapisuje z databáze.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: a3a90963-0286-4fa0-9b3d-c230cc18b0a3
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
msc.type: authoredcontent
ms.openlocfilehash: 05a281720f76b107fe8d902ef60d5d2e72af3ef5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543657"
---
# <a name="adding-a-create-method-and-create-view"></a>Přidání metody Create a zobrazení Create

[Scott Hanselman](https://github.com/shanselman)

> Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvoříte jednoduchou webovou aplikaci, která čte a zapisuje z databáze. Navštivte [centrum učení služby ASP.NET MVC](../../../index.md) , kde najdete další kurzy a ukázky pro ASP.NET MVC.

V této části budeme implementovat podporu nutnou k tomu, aby uživatelé mohli vytvářet nové filmy v naší databázi. Provedeme to implementací akce/Movies/Create URL.

Implementace adresy URL/Movies/Create je proces dvou kroků. Když uživatel poprvé navštíví adresu URL/Movies/Create, chtěli bychom zobrazit formulář HTML, který může vyplnit a zadat nový film. Až uživatel formulář odešle a odešle data zpátky na server, chceme načíst publikovaný obsah a uložit ho do naší databáze.

Tyto dva kroky implementujeme v rámci dvou metod Create () v rámci naší třídy MoviesController. Jedna z metod zobrazí &lt;formulář&gt;, že uživatel by měl vyplnit a vytvořit nový film. Druhá metoda zpracuje zpracování publikovaných dat, když uživatel odešle formulář &lt;&gt; zpátky na server a uloží nový film v naší databázi.

Níže je kód, který přidáme do naší třídy MoviesController k implementaci:

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample1.cs)]

Výše uvedený kód obsahuje veškerý kód, který budeme potřebovat v rámci našeho kontroleru.

Pojďme teď implementovat šablonu pro vytvoření zobrazení, kterou použijeme k zobrazení formuláře uživateli. Klikneme pravým tlačítkem na první metodu create a výběrem možnosti Přidat zobrazení vytvořte šablonu zobrazení pro náš formulář filmu.

Vybereme, že budeme předat šablonu zobrazení jako "film" jako svou třídu zobrazení dat a označit, že chceme "vytvořit" šablonu.

[![přidat zobrazení](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)

Po kliknutí na tlačítko Přidat se vytvoří šablona zobrazení \Movies\Create.aspx za vás. Vzhledem k tomu, že jsme vybrali možnost vytvořit v rozevíracím seznamu zobrazit obsah, dialogové okno Přidat zobrazení automaticky vygeneruje výchozí obsah pro nás. Generování uživatelského rozhraní vytvořilo&gt;&lt;formuláře, místo pro chybové zprávy o ověřování, a vzhledem k tomu, že generování uživatelského rozhraní ví o videu, vytvořilo popisek a pole pro každou vlastnost naší třídy.

[!code-aspx[Main](getting-started-with-mvc-part6/samples/sample2.aspx)]

Vzhledem k tomu, že naše databáze automaticky poskytuje video s ID, pojďme odebrat ta pole, která odkazují na model. ID z našeho zobrazení pro vytvoření Po zobrazení &lt;&gt;&gt;&lt;pole s ID, které nechcete, odeberte 7 řádků.

Pojďme teď vytvořit nový film a přidat ho do databáze. To provedeme opětovným spuštěním aplikace a návštěvou adresy URL "/Movies" a kliknutím na odkaz "vytvořit" přidáte nový film.

[![vytvoření – Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)

Po kliknutí na tlačítko vytvořit se pošle zpátky (prostřednictvím HTTP POST) data z tohoto formuláře do metody/Movies/Create, kterou jsme právě vytvořili. Stejně jako v případě, že systém automaticky převezme parametr "numTimes" a "Name" z adresy URL a namapovaný na parametry v metodě výše, systém automaticky převezme pole formuláře z příspěvku a namapuje je na objekt. V tomto případě budou hodnoty z polí v HTML, jako je například "ReleaseDate" a "title" automaticky vloženy do správných vlastností nové instance filmu.

Pojďme se podívat na druhý způsob vytvoření z našich MoviesControllerů. Všimněte si, jak přebírá objekt "film" jako argument:

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample3.cs)]

Tento objekt filmu byl poté předán do verze [HttpPost] naší metody Create Action a my jsme ho uložili do databáze a pak přesměroval uživatele zpět na metodu akce index (), která zobrazí uložený výsledek v seznamu filmů:

[![seznam filmů – Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)

Nekontrolujeme, jestli jsou filmy správné, ale i databáze neumožní uložit film bez názvu. To je skvělé, kdybyste mohli sdělit uživateli, že předtím, než databáze vyvolala chybu. To provedeme dalším přidáním podpory ověřování do naší aplikace.

> [!div class="step-by-step"]
> [Předchozí](getting-started-with-mvc-part5.md)
> [Další](getting-started-with-mvc-part7.md)

---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: Přidání sloupce do modelu | Microsoft Docs
author: shanselman
description: Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvořte jednoduchou webovou aplikaci, která čte a zapisuje z databáze.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 1cf092c3db3959d6f47006f1be2ba82833c5dc06
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543580"
---
# <a name="adding-a-column-to-the-model"></a>Přidání sloupce do modelu

[Scott Hanselman](https://github.com/shanselman)

> Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvoříte jednoduchou webovou aplikaci, která čte a zapisuje z databáze. Navštivte [centrum učení služby ASP.NET MVC](../../../index.md) , kde najdete další kurzy a ukázky pro ASP.NET MVC.

V této části se dozvíte, jak můžeme udělat změny schématu naší databáze a zpracovat změny v rámci naší aplikace.

Pojďme do tabulky filmů přidat sloupec hodnocení. Vraťte se do prostředí IDE a klikněte na Průzkumník databáze. Klikněte pravým tlačítkem myši na tabulku filmů a vyberte možnost otevřít definici tabulky.

Přidejte sloupec hodnocení, jak je vidět níže. Vzhledem k tomu, že zatím nemáme žádná hodnocení, může sloupec povolit hodnoty null. Klikněte na Uložit.

[![úprava tabulky filmů](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)

Pak se vraťte do Průzkumník řešení a otevřete soubor video. edmx (který je ve složce \Models). Klikněte pravým tlačítkem na plochu návrhu (bílá oblast) a vyberte aktualizovat model z databáze.

[Filmy ![– Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)

Tím se spustí Průvodce aktualizací. Klikněte na kartu aktualizovat a pak klikněte na Dokončit. Naše třída filmového modelu se pak aktualizuje pomocí nového sloupce.

![Průvodce aktualizací (2)](getting-started-with-mvc-part8/_static/image5.png)

Po kliknutí na Dokončit uvidíte nový sloupec hodnocení, který je v našem modelu přidaný do entity video.

[Entita ![Movie](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)

Přidali jsme do databázového modelu sloupec, ale zobrazení na něm nevědí.

## <a name="update-views-with-model-changes"></a>Aktualizace zobrazení se změnami modelu

Existuje několik způsobů, jak můžeme aktualizovat naše šablony zobrazení tak, aby odpovídaly novému sloupci hodnocení. Vzhledem k tomu, že jsme tato zobrazení vytvořili pomocí dialogového okna Přidat zobrazení, můžeme je odstranit a znovu vytvořit. Obvykle ale lidé už provedli úpravy svých šablon zobrazení z počátečního generování vygenerovaného uživatelského rozhraní a budou chtít přidat nebo odstranit pole ručně, stejně jako u pole ID pro vytvoření.

Otevřete šablonu \Views\Movies\Index.aspx a přidejte &lt;&gt;hodnocení&lt;/th&gt; do hlavičky tabulky filmů. Přidal (a) jsem mi svůj Žánr. Pak ve stejném umístění sloupce, ale dole, přidejte čáru pro výstup našeho nového hodnocení.

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

Poslední šablona index. aspx bude vypadat takto:

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

Pak otevřete šablonu \Views\Movies\Create.aspx a přidejte popisek a textové pole pro naši novou vlastnost hodnocení:

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

Naše finální šablona Create. aspx bude vypadat jako tato a změníme název našeho prohlížeče a sekundární &lt;H2&gt; title na něco, co je třeba "vytvořit film".

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

Spusťte aplikaci a nyní máte nové pole v databázi, které bylo přidáno na stránku vytvořit. Přidejte nový film – tentokrát se hodnocením a klikněte na vytvořit.

[![vytvoření videa – Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)

Po kliknutí na vytvořit se vám pošle na stránku index, kde nový film je uvedený ve sloupci nový hodnocení v databázi.

[Seznam filmů ![– Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)

Tento základní kurz vám umožní začít vytvářet řadiče a přidružit je k zobrazením a prodávat je s využitím pevně zakódovaných dat. Pak jsme vytvořili a navrhli databázi a umístili do ní nějaká data. Data z databáze jsme načetli a zobrazili v tabulce HTML. Pak jsme přidali formulář pro vytvoření, který uživateli umožňuje přidávat data do databáze přímo z webové aplikace. Přidali jsme ověření a pak jsme provedli ověřování pomocí JavaScriptu na straně klienta. Nakonec jsme změnili databázi tak, aby obsahovala nový sloupec dat, a pak jsme aktualizovali naše dvě stránky a vytvořili a zobrazili Tato nová data.

Nyní teď doporučujeme přejít na náš podrobný kurz pro[úložiště hudby "MVC Music](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" a také na mnoho videí a prostředků na [https://asp.net/mvc](https://asp.net/mvc) , abyste se dozvěděli ještě více o ASP.NET MVC!

Užijte si ji!

- Scott Hanselman – [http://hanselman.com](http://hanselman.com) a [@shanselman](http://twitter.com/shanselman) na Twitteru.

> [!div class="step-by-step"]
> [Předchozí](getting-started-with-mvc-part7.md)

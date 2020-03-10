---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: Přístup k datům modelu z kontroleru | Microsoft Docs
author: shanselman
description: Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvořte jednoduchou webovou aplikaci, která čte a zapisuje z databáze.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 207ed880977d794d81efdc1ea458d17a68d501d8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543748"
---
# <a name="accessing-your-models-data-from-a-controller"></a>Přístup k datům modelu z kontroleru

[Scott Hanselman](https://github.com/shanselman)

> Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvoříte jednoduchou webovou aplikaci, která čte a zapisuje z databáze. Navštivte [centrum učení služby ASP.NET MVC](../../../index.md) , kde najdete další kurzy a ukázky pro ASP.NET MVC.

V této části vytvoříme novou třídu MoviesController a napíšeme kód, který načte data z filmu a zobrazí se zpátky do prohlížeče pomocí šablony zobrazení.

Klikněte pravým tlačítkem na složku Controllers a vytvořte novou MoviesController.

[Přidat kontroler ![](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)

Tím se vytvoří nový soubor "MoviesController.cs" pod naší \Controllers složkou v rámci našeho projektu. Pojďme aktualizovat MovieController, aby se načetl seznam filmů z naší nově vyplněné databáze.

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

Provádíme dotaz LINQ, abychom načetli jenom filmy vydané po léto 1984. K vygenerování tohoto seznamu videí budete potřebovat šablonu zobrazení, takže v metodě klikněte pravým tlačítkem myši a vyberte Přidat zobrazení a vytvořte ho.

V dialogovém okně Přidat zobrazení oznamujeme, že předáváme seznam&lt;filmy. Models. Movie&gt; do naší šablony zobrazení. Na rozdíl od předchozích časů jsme použili dialog Přidat zobrazení a rozhodli jste se vytvořit "prázdnou" šablonu. Tento čas oznamujeme, že chceme, aby se v aplikaci Visual Studio automaticky vytvořila šablona zobrazení pro nás s nějakým výchozím obsahem. Provedeme to tak, že v rozevírací nabídce zobrazení obsahu vyberete položku seznam.

Mějte na paměti, že pokud máte vytvořenou novou třídu, budete muset aplikaci zkompilovat, aby se zobrazila v dialogovém okně Přidat zobrazení.

![Přidat zobrazení](getting-started-with-mvc-part5/_static/image3.png)

Klikněte na tlačítko Přidat a systém automaticky vygeneruje kód pro zobrazení pro nás, který zobrazí náš seznam filmů. To je dobrý čas ke změně &lt;H2&gt; nadpisu na něco, co se stalo s zobrazením Hello World.

[Filmy ![– Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)

Spusťte aplikaci a na panelu Adresa navštivte/Movies. Nyní jsme načetli data z databáze pomocí základního dotazu v rámci kontroleru a vrátili data do zobrazení, které ví o videu. Toto zobrazení se pak roztočí seznamem filmů a vytvoří tabulku dat pro nás.

[![seznam filmů – Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)

V této aplikaci nebudeme implementovat funkce Edit, Details a DELETE, takže nepotřebujeme výchozí odkazy, které vytvořila šablona generování uživatelského rozhraní pro nás. Otevřete soubor/Movies/Index.aspx a odeberte ho.

Tady je zdrojový kód, který by naše aktualizovaná šablona zobrazení vypadala po provedení těchto změn:

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

Vytváříme odkazy, které nepotřebujeme, takže je pro tento příklad odstraníme. Náš odkaz pro vytváření nových odkazů budeme uchovávat, i když to bude dál! V našem příkladu vypadá naše aplikace s odebraným sloupcem.

[![seznam filmů – Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)

Teď máme jednoduchý seznam našich filmových dat. Pokud ale klikneme na odkaz vytvořit nový, zobrazí se chyba, protože se nepřipojí. Pojďme implementovat metodu akce vytvoření a umožnit uživateli zadat nové filmy v naší databázi.

> [!div class="step-by-step"]
> [Předchozí](getting-started-with-mvc-part4.md)
> [Další](getting-started-with-mvc-part6.md)

---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
title: Vytvoření databáze | Microsoft Docs
author: shanselman
description: Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvořte jednoduchou webovou aplikaci, která čte a zapisuje z databáze.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 742df67f-484d-4ef3-af6b-8c791e556b43
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
msc.type: authoredcontent
ms.openlocfilehash: 995db714ce6365415d06dc458aee84a31c7c8fd6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581436"
---
# <a name="creating-a-database"></a>Vytvoření databáze

[Scott Hanselman](https://github.com/shanselman)

> Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvoříte jednoduchou webovou aplikaci, která čte a zapisuje z databáze. Navštivte [centrum učení služby ASP.NET MVC](../../../index.md) , kde najdete další kurzy a ukázky pro ASP.NET MVC.

V této části vytvoříme novou databázi SQL Express, kterou použijeme k ukládání a načítání našich filmových dat. V integrovaném vývojovém prostředí sady Visual Web Developer vyberte Zobrazit | Průzkumník serveru. Klikněte pravým tlačítkem na datová připojení a klikněte na Přidat připojení...

![AddConnection](getting-started-with-mvc-part4/_static/image1.png)

V dialogovém okně Zvolit zdroj dat vyberte možnost Microsoft SQL Server a vyberte možnost pokračovat.

![](getting-started-with-mvc-part4/_static/image2.png)

V dialogovém okně Přidat připojení zadejte ".\SQLEXPRESS" pro název vašeho serveru a jako název nové databáze zadejte "filmy".

[dialog ![přidat připojení](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)

Klikněte na OK a zobrazí se dotaz, jestli chcete vytvořit tuto databázi. Vyberte Ano.

[![vytvořit filmy?](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)

Nyní máte v Průzkumník serveru prázdnou databázi.

![Přidat novou tabulku](getting-started-with-mvc-part4/_static/image7.png)

Klikněte pravým tlačítkem na tabulky a klikněte na Přidat tabulku. Zobrazí se Návrhář tabulky. Přidejte sloupce pro ID, název, ReleaseDate, Žánr a cenu. Klikněte pravým tlačítkem na sloupec ID a pak klikněte na nastavit primární klíč. Tady vidíte, jak vypadají moje oblasti návrhu.

[![Editor databázových tabulek](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)

Také vyberte sloupec ID a v části vlastnosti sloupce níže změňte "specifikace identity" na "Ano".

[![vlastnosti identity-Column](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)

Až to bude hotové, klikněte na panelu nástrojů na ikonu Uložit nebo vyberte soubor | Uložte si z nabídky a pojmenujte tabulku "**film**" (v jednotném čísle). Máme databázi a tabulku!

[![zvolit název](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)

Vraťte se na Průzkumník serveru a klikněte pravým tlačítkem myši na tabulku video a pak vyberte možnost zobrazit data tabulky. Zadejte několik filmů, aby naše databáze měla nějaká data.

[![úpravy databázových tabulek](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)

## <a name="creating-a-model"></a>Vytvoření modelu

Nyní přejděte zpět na Průzkumník řešení na pravé straně rozhraní IDE a klikněte pravým tlačítkem na složku modely a vyberte Přidat | Nová položka.

[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)

Z naší nové databáze vytvoříme model entity. Tím se do našeho projektu přidá sada tříd, která nám usnadňuje dotazování na data v naší databázi a manipulaci s nimi. Na levé straně dialogového okna vyberte datový uzel a pak vyberte šablonu ADO.NET model EDM (Entity Data Model) Item. Pojmenujte ho Movies. edmx.

[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)

Klikněte na tlačítko Přidat. Pak se spustí Průvodce model EDM (Entity Data Model).

V novém dialogovém okně, které se zobrazí, vyberte možnost generovat z databáze. Vzhledem k tomu, že jsme právě vytvořili databázi, je potřeba sdělit Entity Framework o naší nové databázi a její tabulce. Kliknutím na tlačítko Další uložíte připojení k databázi v konfiguraci naší webové aplikace. Nyní zaškrtněte políčko tabulky a video a klikněte na tlačítko Dokončit.

[Průvodce model EDM (Entity Data Model) ![](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)

Nyní můžeme zobrazit naši novou tabulku filmů v Entity Framework Designer a přistupovat k ní z kódu.

[Filmy ![– Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)

Na návrhové ploše vidíte třídu "video". Tato třída se mapuje na tabulku "film" v naší databázi a každá vlastnost v ní je namapována na sloupec s tabulkou. Každá instance třídy "video" bude odpovídat řádku v tabulce "video".

Pokud se vám nelíbí výchozí konvence pojmenování a mapování, které používá Entity Framework, můžete k jejich změně nebo přizpůsobení použít návrháře Entity Framework. Pro tuto aplikaci použijeme výchozí hodnoty a jenom soubor uložte tak, jak je.

Teď budeme pracovat s některými skutečnými daty!

> [!div class="step-by-step"]
> [Předchozí](getting-started-with-mvc-part3.md)
> [Další](getting-started-with-mvc-part5.md)

---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-vb
title: Vytvoření kontroleru (VB) | Microsoft Docs
author: StephenWalther
description: V tomto kurzu Stephen Walther ukazuje, jak můžete přidat kontroler do aplikace ASP.NET MVC.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 204b7e86-f560-4611-8adb-785b33e777b9
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-vb
msc.type: authoredcontent
ms.openlocfilehash: 60636b79ab5fc06ca904dee90ce74f256e046d12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601456"
---
# <a name="creating-a-controller-vb"></a>Vytvoření kontroleru (VB)

od [Stephen Walther](https://github.com/StephenWalther)

> V tomto kurzu Stephen Walther ukazuje, jak můžete přidat kontroler do aplikace ASP.NET MVC.

Cílem tohoto kurzu je vysvětlit, jak můžete vytvářet nové řadiče ASP.NET MVC. Naučíte se, jak vytvořit řadiče pomocí možnosti nabídky přidat řadič sady Visual Studio a vytvořit soubor třídy ručně.

### <a name="using-the-add-controller-menu-option"></a>Použití možnosti nabídky přidat řadič

Nejjednodušší způsob, jak vytvořit nový kontroler, je kliknout pravým tlačítkem myši na složku řadiče v okně Visual Studio Průzkumník řešení a vybrat možnost nabídky **Přidat, řadič** (viz obrázek 1). Po výběru této možnosti nabídky se otevře dialogové okno **Přidat řadič** (viz obrázek 2).

[![dialogového okna Nový projekt](creating-a-controller-vb/_static/image1.jpg)](creating-a-controller-vb/_static/image1.png)

**Obrázek 01**: Přidání nového kontroleru ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-controller-vb/_static/image2.png))

[![dialogového okna Nový projekt](creating-a-controller-vb/_static/image2.jpg)](creating-a-controller-vb/_static/image3.png)

**Obrázek 02**: dialogové okno Přidat řadič ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-controller-vb/_static/image4.png))

Všimněte si, že první část názvu kontroleru je zvýrazněna v dialogovém okně **Přidat řadič** . Každý název kontroleru musí končit příponou *řadiče*. Můžete například vytvořit kontrolér s názvem *ProductController* , ale ne kontroler s názvem *Product*.

Pokud vytvoříte kontroler, ve kterém chybí přípona *kontroleru* , nebudete moct tento kontroler vyvolat. Tento postup neprovádějte – po této chybě už nedošlo k dlouhé hodinám svého životního cyklu.

**Výpis 1 – Controllers\ProductController.vb**

[!code-vb[Main](creating-a-controller-vb/samples/sample1.vb)]

Vždy byste měli vytvořit řadiče ve složce Controllers. Jinak budete porušovat konvence ASP.NET MVC a další vývojáři budou mít obtížnější pochopit svou aplikaci.

### <a name="scaffolding-action-methods"></a>Metody akcí generování uživatelského rozhraní

Při vytváření kontroleru máte možnost automaticky generovat metody akcí vytvořit, aktualizovat a podrobnosti (viz obrázek 3). Vyberete-li tuto možnost, je vygenerována třída Controller v seznamu 2.

[Automatické vytváření metod akcí ![](creating-a-controller-vb/_static/image3.jpg)](creating-a-controller-vb/_static/image5.png)

**Obrázek 03**: automatické vytváření metod akcí ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-controller-vb/_static/image6.png))

**Výpis 2 – Controllers\CustomerController.vb**

[!code-vb[Main](creating-a-controller-vb/samples/sample2.vb)]

Tyto generované metody jsou zástupné metody. Musíte přidat skutečnou logiku pro vytváření, aktualizaci a zobrazování podrobností pro zákazníka sami. Ale metody zástupných procedur poskytují dobrý počáteční bod.

### <a name="creating-a-controller-class"></a>Vytvoření třídy kontroleru

Kontroler MVC ASP.NET je pouze třída. Pokud budete chtít, můžete ignorovat praktické generování uživatelského rozhraní kontroleru sady Visual Studio a vytvořit třídu kontroleru ručně. Postupujte následovně:

1. Klikněte pravým tlačítkem na složku řadiče a vyberte možnost nabídky **Přidat, nová položka** a vyberte šablonu **třídy** (viz obrázek 4).
2. Pojmenujte novou třídu PersonController. vb a klikněte na tlačítko **Přidat** .
3. Upravte výsledný soubor třídy tak, aby třída dědila ze třídy Base System. Web. Mvc. Controller (viz výpis 3).

[![vytvoření nové třídy](creating-a-controller-vb/_static/image4.jpg)](creating-a-controller-vb/_static/image7.png)

**Obrázek 04**: vytvoření nové třídy ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-controller-vb/_static/image8.png))

**Výpis 3 – Controllers\PersonController.vb**

[!code-vb[Main](creating-a-controller-vb/samples/sample3.vb)]

Kontroler v seznamu 3 zpřístupňuje jednu akci s názvem index (), která vrací řetězec "Hello World!". Tuto akci kontroleru můžete vyvolat spuštěním aplikace a vyžádáním adresy URL, jako je následující:

`http://localhost:40071/Person`

> [!NOTE]
> 
> ASP.NET Development Server používá náhodné číslo portu (například 40071). Když zadáváte adresu URL pro vyvolání kontroleru, budete muset zadat správné číslo portu. Číslo portu můžete určit tak, že najedete myší na ikonu pro vývojový server ASP.NET v oznamovací oblasti systému Windows (dole vpravo na obrazovce).
> 
> [!div class="step-by-step"]
> [Předchozí](adding-dynamic-content-to-a-cached-page-vb.md)
> [Další](creating-an-action-vb.md)

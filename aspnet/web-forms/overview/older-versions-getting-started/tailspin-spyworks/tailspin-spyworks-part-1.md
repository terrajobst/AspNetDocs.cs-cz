---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
title: 'Část 1: soubor-> Nový projekt | Microsoft Docs'
author: JoeStagner
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 1 pokrývá přehled a soubor/nový projekt.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 15d4652b-d5aa-4172-b186-2c7f96ba316d
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1
msc.type: authoredcontent
ms.openlocfilehash: 05a3ace3d8fef9c1f3593f7948e42b4725d70134
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78636127"
---
# <a name="part-1-file--new-project"></a>1\. část: Soubor > Nový projekt

[Jana Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks ukazuje, jak neobyčejně jednoduché je vytvářet výkonné a škálovatelné aplikace pro platformu .NET. Ukazuje, jak používat Skvělé nové funkce v ASP.NET 4 k vytvoření online obchodu, včetně nákupu, rezervace a správy.
> 
> V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 1 pokrývá přehled a soubor/nový projekt.

## <a id="_Toc260221666"></a>Přehled

Tento kurz představuje úvod k ASP.NET WebForms. Začneme pomaleji, takže prostředí pro vývoj na webu na úrovni začátečník je v pořádku.

Aplikace, kterou budeme sestavovat, je jednoduchý online obchod.

![](tailspin-spyworks-part-1/_static/image1.jpg)

Uživatelé můžou procházet produkty podle kategorie:

![](tailspin-spyworks-part-1/_static/image2.jpg)

Můžou si zobrazit jeden produkt a přidat ho do svého košíku:

![](tailspin-spyworks-part-1/_static/image3.jpg)

Můžou si prohlédnout svůj košík a odebrat položky, které už nepotřebují:

![](tailspin-spyworks-part-1/_static/image4.jpg)

Při pokračování na rezervaci se zobrazí výzva k zadání

![](tailspin-spyworks-part-1/_static/image5.jpg)

![](tailspin-spyworks-part-1/_static/image6.jpg)

Po objednání se zobrazí jednoduchá potvrzovací obrazovka:

![](tailspin-spyworks-part-1/_static/image7.jpg)

Začneme vytvořením nového projektu WebForms ASP.NET v aplikaci Visual Studio 2010 a my postupně přidáváme funkce pro vytvoření kompletní funkční aplikace. Podél toho se podíváme na přístup k databázi, zobrazení seznamu a mřížky, stránky aktualizace dat, ověření dat, použití stránek předloh pro konzistentní rozložení stránky, AJAX, ověřování, členství uživatelů a další.

Můžete postupovat podle kroků nebo si můžete stáhnout dokončenou aplikaci z [http://tailspinspyworks.codeplex.com/](http://tailspinspyworks.codeplex.com/)

Můžete použít buď Visual Studio 2010, nebo bezplatný Visual Web Developer 2010 z [https://www.microsoft.com/express/Web/](https://www.microsoft.com/express/Web/). K sestavení aplikace můžete použít buď SQL Server, nebo bezplatný SQL Server Express k hostování databáze.

## <a id="_Toc260221667"></a>Soubor/nový projekt

Začneme tak, že vybereme nový projekt v nabídce soubor v aplikaci Visual Studio. Tím se otevře dialogové okno Nový projekt.

![](tailspin-spyworks-part-1/_static/image8.jpg)

Na levé straně vybereme skupinu Visual C# /web Templates a potom v prostředním sloupci zvolíte šablonu webová aplikace v ASP.NET. Pojmenujte projekt TailspinSpyworks a stiskněte tlačítko OK.

![](tailspin-spyworks-part-1/_static/image9.jpg)

Tím se vytvoří náš projekt. Pojďme se podívat na složky, které jsou součástí naší aplikace v Průzkumník řešení na pravé straně.

![](tailspin-spyworks-part-1/_static/image10.jpg)

Prázdné řešení není zcela prázdné – přidá základní strukturu složek:

![](tailspin-spyworks-part-1/_static/image1.png)

Poznamenejte si konvence implementované výchozí šablonou projektu ASP.NET 4.

- Složka "Account" implementuje základní uživatelské rozhraní pro ASP. Podsystém členství v síti.
- Složka "skripty" slouží jako úložiště pro soubory JavaScriptu na straně klienta a základní soubory jQuery. js jsou ve výchozím nastavení k dispozici.
- Složka Styles (styly) slouží k uspořádání webových vizuálů webu (šablony stylů CSS).

Po stisknutí klávesy F5 ke spuštění naší aplikace a vykreslení stránky default. aspx se zobrazí následující.

![](tailspin-spyworks-part-1/_static/image11.jpg)

Naše první vylepšení aplikace bude nahradit soubor style. CSS od výchozích šablon WebForms s třídami šablony stylů CSS a přidruženými obrazovými soubory, které vykreslí vizuální asthetics, které chceme pro naši aplikaci Tailspin Spyworks.

Až to uděláte, stránka default. aspx se takto vykreslí.

![](tailspin-spyworks-part-1/_static/image12.jpg)

Všimněte si odkazů na obrázek v pravém horním rohu stránky a položek nabídky, které byly přidány do stránky předlohy. Pouze odkazy "přihlásit" a "účet" odkazují na stránky, které existují (vygenerované výchozí šablonou), a na ostatní stránky, které budeme implementovat při sestavování naší aplikace.

Také přemístím stránku předlohy do adresáře Styles. I když se jedná jenom o předvolbu, může to chvíli udělat, pokud se rozhodnete, že aplikaci bude možné v budoucnu udělat jako srozumitelnou.

Až to uděláte, budete muset změnit odkazy na hlavní stránku ve všech souborech. aspx vygenerovaných výchozími stránkami WebForms ASP.NET.

> [!div class="step-by-step"]
> [Next](tailspin-spyworks-part-2.md)

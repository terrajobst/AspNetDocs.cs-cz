---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
title: 'Část 1: Přehled a soubor > Nový projekt | Microsoft Docs'
author: jongalloway
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 1 pokrývá přehled a soubor > Nový projekt.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: bd356ca3-5bdb-4067-9dac-c9e9923a86e8
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-1
msc.type: authoredcontent
ms.openlocfilehash: 48428ff4ab5888253ed93ac41e79006eec823ad2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559981"
---
# <a name="part-1-overview-and-file-new-project"></a>1\. část: Přehled a Soubor->Nový projekt

o [Jan Galloway](https://github.com/jongalloway)

> Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio pro vývoj webů.  
>   
> Úložiště hudby MVC je zjednodušená ukázka implementace úložiště, která prodává hudební alba online a implementuje základní funkce pro správu webů, přihlašování uživatelů a nákupních košíků.  
>   
> V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 1 pokrývá přehled a soubor&gt;nový projekt.

## <a name="overview"></a>Přehled

Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Web Developer pro vývoj webů. Začneme pomaleji, takže prostředí pro vývoj na webu na úrovni začátečník je v pořádku.

Aplikace, kterou budeme sestavovat, je jednoduchý hudební obchod. Existují tři hlavní části aplikace: nákupy, rezervace a správa.

![](mvc-music-store-part-1/_static/image1.jpg)

Návštěvníci můžou procházet alba podle žánru:

![](mvc-music-store-part-1/_static/image2.jpg)

Můžou zobrazit jedno album a přidat ho do svého košíku:

![](mvc-music-store-part-1/_static/image3.jpg)

Můžou si prohlédnout svůj košík a odebrat položky, které už nepotřebují:

![](mvc-music-store-part-1/_static/image4.jpg)

Při pokračování na rezervaci se zobrazí výzva k přihlášení nebo registraci pro uživatelský účet.

![](mvc-music-store-part-1/_static/image1.png)

![](mvc-music-store-part-1/_static/image2.png)

Po vytvoření účtu můžou Dokončit objednávku vyplněním informací o expedici a platbách. Abychom vám pomohli něco jednoduchého, máme k dispozici úžasné propagační akce: všechno je zdarma, pokud zadáte propagační kód "FREE".

![](mvc-music-store-part-1/_static/image5.jpg)

Po objednání se zobrazí jednoduchá potvrzovací obrazovka:

![](mvc-music-store-part-1/_static/image6.jpg)

Kromě zákaznických stránek také sestavíme oddíl správce, který obsahuje seznam alb, ze kterých můžou správci vytvářet, upravovat a odstraňovat alba:

![](mvc-music-store-part-1/_static/image7.jpg)

## <a name="1-file--gt-new-project"></a>1. soubor-&gt; nový projekt

### <a name="installing-the-software"></a>Instalace softwaru

V tomto kurzu začnete vytvořením nového projektu ASP.NET MVC 3 pomocí bezplatného programu Visual Web Developer 2010 Express (který je zdarma) a pak postupně přidáváme funkce, které vytvoří kompletní funkční aplikaci. Na základě toho se podíváme na přístup k databázi, scénáře pro publikování formulářů, ověřování dat, používání stránek předloh pro konzistentní rozložení stránky, používání AJAX pro aktualizace stránky a ověřování, přihlášení uživatele a další.

Můžete postupovat podle jednotlivých kroků nebo si můžete stáhnout dokončenou aplikaci z [MVC – hudba-Store](https://github.com/evilDave/MVC-Music-Store).

K sestavení aplikace můžete použít buď Visual Studio 2010 SP1 nebo Visual Web Developer 2010 Express SP1 (bezplatnou verzi sady Visual Studio 2010). Pro hostování databáze budeme používat tuto SQL Server Compact (také bezplatnou). Než začnete, ujistěte se, že jste nainstalovali požadavky uvedené níže.

- [Požadavky na Visual Studio Web Developer Express SP1]
- [Aktualizace nástrojů ASP.NET MVC 3]
- [SQL Server Compact 4,0] – včetně podpory modulu runtime a nástrojů

### <a name="creating-a-new-aspnet-mvc-3-project"></a>Vytvoření nového projektu ASP.NET MVC 3

Začneme výběrem možnosti nový projekt v nabídce soubor v aplikaci Visual Web Developer. Tím se otevře dialogové okno Nový projekt.

![](mvc-music-store-part-1/_static/image5.png)

Na levé straně vybereme skupinu Visual C# -&gt; web Templates a potom v prostředním sloupci zvolíte šablonu webová aplikace ASP.NET MVC 3. Pojmenujte projekt MvcMusicStore a stiskněte tlačítko OK.

![](mvc-music-store-part-1/_static/image8.jpg)

Tím se zobrazí sekundární dialog, který nám umožní udělat pro náš projekt určitá nastavení specifická pro MVC. Vyberte následující:

Šablona projektu – vybrat prázdné

Zobrazení modulu – výběr Razor

Použít sémantické označení HTML5 – zaškrtnuto

Ověřte, že nastavení jsou uvedená níže, a pak stiskněte tlačítko OK.

![](mvc-music-store-part-1/_static/image9.jpg)

Tím se vytvoří náš projekt. Pojďme se podívat na složky, které byly přidány do naší aplikace v Průzkumník řešení na pravé straně.

![](mvc-music-store-part-1/_static/image10.jpg)

Prázdná šablona MVC 3 není zcela prázdná – přidá základní strukturu složek:

![](mvc-music-store-part-1/_static/image6.png)

ASP.NET MVC využívá některé základní zásady vytváření názvů pro názvy složek:

| **Složka** | **Účel** |
| --- | --- |
| **/Controllers** | Řadiče reagují na vstup z prohlížeče, rozhodnou se s ním a vrátí odpověď uživateli. |
| **/Views** | Zobrazení obsahují šablony uživatelského rozhraní. |
| **/Models** | Modely uchovávají a manipulují s daty |
| **/Content** | Tato složka obsahuje obrázky, šablony stylů CSS a jakýkoli další statický obsah. |
| **/Scripts** | Tato složka obsahuje naše soubory JavaScriptu. |

Tyto složky jsou zahrnuté i do prázdné aplikace ASP.NET MVC, protože rozhraní ASP.NET MVC ve výchozím nastavení používá přístup "konvence před konfigurací" a vytváří některé výchozí předpoklady založené na zásadách vytváření názvů složek. Například řadiče ve výchozím nastavení vyhledávají zobrazení ve složce views, aniž byste je museli explicitně zadat ve svém kódu. Dodávání s výchozími konvencemi omezuje množství kódu, který musíte napsat, a může také usnadnit ostatním vývojářům pochopení vašeho projektu. Tyto konvence vyvysvětlíme podrobněji, protože sestavíme naši aplikaci.

> [!div class="step-by-step"]
> [Next](mvc-music-store-part-2.md)

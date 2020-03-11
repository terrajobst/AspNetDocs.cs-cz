---
uid: mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-vb
title: Principy modelů, zobrazení a řadičů (VB) | Microsoft Docs
author: StephenWalther
description: Zaměňujte si modely, zobrazení a řadiče? V tomto kurzu Stephen Walther vás seznámí s různými částmi aplikace ASP.NET MVC.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: a106374a-5e74-4fd0-9ac0-1a32280e5d0d
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-models-views-and-controllers-vb
msc.type: authoredcontent
ms.openlocfilehash: cc7988e0c9802e8cd376396eb5da15b5393d6088
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600448"
---
# <a name="understanding-models-views-and-controllers-vb"></a>Principy modelů, zobrazení a kontrolerů (VB)

od [Stephen Walther](https://github.com/StephenWalther)

> Zaměňujte si modely, zobrazení a řadiče? V tomto kurzu Stephen Walther vás seznámí s různými částmi aplikace ASP.NET MVC.

Tento kurz vám poskytne přehled o ASP.NET modelech, zobrazeních a řadičích MVC na nejvyšší úrovni. Jinými slovy, vysvětluje M ", V" a C "v ASP.NET MVC.

Po přečtení tohoto kurzu byste měli pochopit, jak různé části aplikace ASP.NET MVC spolupracují. Měli byste taky porozumět tomu, jak se architektura aplikace ASP.NET MVC liší od aplikace webových formulářů ASP.NET nebo aplikace Active Server Pages.

## <a name="the-sample-aspnet-mvc-application"></a>Ukázková aplikace ASP.NET MVC

Výchozí šablona sady Visual Studio pro vytváření webových aplikací ASP.NET MVC obsahuje extrémně jednoduchou ukázkovou aplikaci, kterou lze použít k pochopení různých částí aplikace ASP.NET MVC. Tuto jednoduchou aplikaci využíváme v tomto kurzu.

Vytvoříte novou aplikaci ASP.NET MVC se šablonou MVC spuštěním sady Visual Studio 2008 a výběrem souboru možnosti nabídky, nový projekt (viz obrázek 1). V dialogovém okně Nový projekt vyberte v části typy projektů (Visual Basic nebo C#) svůj oblíbený programovací jazyk a v části šablony vyberte **Webová aplikace ASP.NET MVC** . Klikněte na tlačítko OK.

[Dialog ![nový projekt](understanding-models-views-and-controllers-vb/_static/image1.jpg)](understanding-models-views-and-controllers-vb/_static/image1.png)

**Obrázek 01**: dialogové okno Nový projekt ([kliknutím zobrazíte obrázek v plné velikosti](understanding-models-views-and-controllers-vb/_static/image2.png))

Při vytváření nové aplikace ASP.NET MVC se zobrazí dialogové okno **vytvořit projekt testování částí** (viz obrázek 2). Toto dialogové okno umožňuje ve vašem řešení vytvořit samostatný projekt pro testování aplikace ASP.NET MVC. Vyberte možnost **Ne, nevytvářejte projekt testování částí** a klikněte na tlačítko **OK** .

[Dialogové okno pro vytvoření testu jednotek ![](understanding-models-views-and-controllers-vb/_static/image2.jpg)](understanding-models-views-and-controllers-vb/_static/image3.png)

**Obrázek 02**: dialogové okno pro vytvoření testu jednotek ([kliknutím zobrazíte obrázek v plné velikosti](understanding-models-views-and-controllers-vb/_static/image4.png))

Po vytvoření nové aplikace ASP.NET MVC. V okně Průzkumník řešení se zobrazí několik složek a souborů. Konkrétně se zobrazí tři složky s názvem modely, zobrazení a řadiče. Jak se můžete považovat za názvy složek, tyto složky obsahují soubory pro implementaci modelů, zobrazení a řadičů.

Pokud rozbalíte složku Controllers, měl by se zobrazit soubor s názvem AccountController. vb a soubor s názvem HomeController. vb. Pokud rozbalíte složku zobrazení, měli byste vidět tři podsložky s názvem Account, Home a Shared. Pokud rozbalíte domovskou složku, zobrazí se dva další soubory s názvem About. aspx a index. aspx (viz obrázek 3). Tyto soubory tvoří ukázkovou aplikaci, která je součástí výchozí šablony ASP.NET MVC.

[![Průzkumník řešení okně](understanding-models-views-and-controllers-vb/_static/image3.jpg)](understanding-models-views-and-controllers-vb/_static/image5.png)

**Obrázek 03**: okno Průzkumník řešení ([kliknutím zobrazíte obrázek v plné velikosti](understanding-models-views-and-controllers-vb/_static/image6.png))

Ukázkovou aplikaci můžete spustit výběrem možnosti nabídky **ladění a spustit ladění**. Případně můžete stisknout klávesu F5.

Při prvním spuštění aplikace ASP.NET se zobrazí dialogové okno na obrázku 4, které doporučuje povolit režim ladění. Klikněte na tlačítko OK a aplikace se spustí.

[dialog ![ladění není povolený](understanding-models-views-and-controllers-vb/_static/image4.jpg)](understanding-models-views-and-controllers-vb/_static/image7.png)

**Obrázek 04**: dialogové okno ladění není povoleno ([kliknutím zobrazíte obrázek v plné velikosti).](understanding-models-views-and-controllers-vb/_static/image8.png)

Když spustíte aplikaci ASP.NET MVC, Visual Studio spustí aplikaci ve webovém prohlížeči. Ukázková aplikace se skládá pouze ze dvou stránek: stránky index a stránka o produktu. Po prvním spuštění aplikace se zobrazí stránka index (viz obrázek 5). Kliknutím na odkaz nabídky v pravém horním rohu aplikace můžete přejít na stránku o aplikaci.

[![stránku indexu](understanding-models-views-and-controllers-vb/_static/image5.jpg)](understanding-models-views-and-controllers-vb/_static/image9.png)

**Obrázek 05**: stránka index ([kliknutím zobrazíte obrázek v plné velikosti](understanding-models-views-and-controllers-vb/_static/image10.png))

Všimněte si adres URL v adresním řádku prohlížeče. Když například kliknete na odkaz o nabídku o, adresa URL v adresním řádku prohlížeče se změní na **/Home/about**.

Pokud zavřete okno prohlížeče a vrátíte se do sady Visual Studio, nebudete moci najít soubor s cestou domů/o. Soubory neexistují. Jak je to možné?

## <a name="a-url-does-not-equal-a-page"></a>Adresa URL se neshoduje s stránkou.

Při vytváření tradiční aplikace webových formulářů ASP.NET nebo aplikace Active Server Pages existuje korespondence 1:1 mezi adresou URL a stránkou. Pokud si vyžádáte stránku s názvem SomePage. aspx ze serveru, měli byste mít lepší stránku na disku s názvem SomePage. aspx. Pokud soubor SomePage. aspx neexistuje, zobrazí se chyba ošklivá **404 – Stránka nebyla nalezena** .

Při sestavování aplikace ASP.NET MVC neexistuje žádná korespondence mezi adresou URL, kterou zadáte do adresního řádku prohlížeče, a soubory, které v aplikaci najdete. V aplikaci ASP.NET MVC adresa URL odpovídá akci kontroleru Namísto stránky na disku.

V tradiční aplikaci ASP.NET nebo ASP jsou požadavky prohlížeče mapovány na stránky. V aplikaci ASP.NET MVC jsou požadavky prohlížeče namapovány na akce kontroleru. Aplikace webových formulářů ASP.NET je zaměřená na obsah. Aplikace ASP.NET MVC je naopak na orientovaném Application Logic.

## <a name="understanding-aspnet-routing"></a>Principy směrování ASP.NET

Požadavek prohlížeče se namapuje na akci kontroleru prostřednictvím funkce ASP.NET Framework s názvem *směrování ASP.NET*. ASP.NET směrování používá rozhraní ASP.NET MVC ke *Směrování* příchozích požadavků na akce kontroleru.

ASP.NET směrování používá směrovací tabulku pro zpracování příchozích požadavků. Tato směrovací tabulka se vytvoří při prvním spuštění webové aplikace. Směrovací tabulka je nastavena v souboru Global. asax. Výchozí soubor Global. asax sady MVC je obsažen v seznamu 1.

**Výpis 1 – Global. asax**

[!code-vb[Main](understanding-models-views-and-controllers-vb/samples/sample1.vb)]

Při prvním spuštění aplikace ASP.NET je volána metoda aplikace\_Start (). V výpisu 1 Tato metoda volá metodu RegisterRoutes () a metoda RegisterRoutes () vytvoří výchozí směrovací tabulku.

Výchozí směrovací tabulka se skládá z jedné trasy. Tato výchozí trasa zruší všechny příchozí požadavky na tři segmenty (segment adresy URL je cokoli mezi lomítky). První segment je namapován na název kontroleru, druhý segment je namapován na název akce a konečný segment je namapován na parametr předaný akci s názvem ID.

Podívejte se například na následující adresu URL:

/Product/Details/3

Tato adresa URL se analyzuje do tří parametrů, například takto:

Controller = produkt

Action = details

Id = 3

Výchozí trasa definovaná v souboru Global. asax obsahuje výchozí hodnoty pro všechny tři parametry. Výchozí kontroler je Home, výchozí akce je index a výchozí ID je prázdný řetězec. S těmito výchozími nastaveními zvažte, jak se analyzuje následující adresa URL:

/Employee

Tato adresa URL se analyzuje do tří parametrů, například takto:

Controller = zaměstnanec

Action = index

Id = ��

Nakonec, pokud otevřete aplikaci ASP.NET MVC bez zadání adresy URL (například `http://localhost`), adresa URL bude analyzována takto:

Controller = domů

Action = index

Id = ��

Požadavek se směruje do akce index () ve třídě HomeController.

## <a name="understanding-controllers"></a>Principy řadičů

Kontroler je zodpovědný za řízení způsobu, jakým uživatel komunikuje s aplikací MVC. Kontroler obsahuje logiku řízení toku pro aplikaci ASP.NET MVC. Kontroler určuje, jaká odpověď se má poslat zpátky uživateli, když uživatel odešle požadavek na prohlížeč.

Kontroler je pouze třída (například Visual Basic nebo C# třída). Ukázková aplikace ASP.NET MVC obsahuje kontroler s názvem HomeController. vb umístěný ve složce Controllers. Obsah souboru HomeController. vb je reprodukován v seznamu 2.

**Výpis 2 – HomeController.cs**

[!code-vb[Main](understanding-models-views-and-controllers-vb/samples/sample2.vb)]

Všimněte si, že HomeController má dvě metody pojmenované index () a About (). Tyto dvě metody odpovídají dvěma akcím, které kontroler zveřejňuje. Adresa URL/Home/Index vyvolá metodu HomeController. index () a adresa URL/Home/About vyvolá metodu HomeController. about ().

Všechny veřejné metody v kontroleru se zveřejňují jako akce kontroleru. Je potřeba, abyste byli opatrní. To znamená, že všechny veřejné metody obsažené v řadiči můžou být vyvolány kýmkoli, kdo má přístup k Internetu, zadáním správné adresy URL do prohlížeče.

## <a name="understanding-views"></a>Porozumění zobrazením

Obě akce kontroleru vystavené třídou HomeController, index () a About () vrátí zobrazení. Zobrazení obsahuje značku HTML a obsah, který je odeslán do prohlížeče. Zobrazení je ekvivalent stránky při práci s aplikací ASP.NET MVC.

Zobrazení je nutné vytvořit ve správném umístění. Akce HomeController. index () vrátí zobrazení umístěné v následující cestě:

\Views\Home\Index.aspx

Akce HomeController. about () vrátí zobrazení umístěné v následující cestě:

\Views\Home\About.aspx

Obecně platí, že pokud chcete vrátit zobrazení pro akci kontroleru, musíte vytvořit podsložku ve složce views se stejným názvem jako má váš kontroler. V podsložce je nutné vytvořit soubor. aspx se stejným názvem, jako má akce kontroleru.

Soubor v seznamu 3 obsahuje zobrazení About. aspx.

**Výpis 3 – About. aspx**

[!code-aspx[Main](understanding-models-views-and-controllers-vb/samples/sample3.aspx)]

Pokud v seznamu 3 přeskočíte první řádek, většina ze zbývajících zobrazení se skládá ze standardního HTML. Obsah zobrazení můžete upravit zadáním libovolného HTML, který chcete.

Zobrazení je velmi podobné jako stránka na Active Server stránkách nebo webových formulářích ASP.NET. Zobrazení může obsahovat obsah a skripty HTML. Skripty můžete napsat do svého oblíbeného programovacího jazyka .NET (například C# nebo Visual Basic .NET). Pomocí skriptů můžete zobrazit dynamický obsah, jako jsou data databáze.

## <a name="understanding-models"></a>Porozumění modelům

Provedli jsme pojednávající řadiče a my jsme povedli zobrazení. Poslední téma, které potřebujeme diskutovat, je modely. Co je model MVC?

Model MVC obsahuje veškerou logiku vaší aplikace, která není obsažena v zobrazení nebo řadiči. Model by měl obsahovat veškerou obchodní logiku vaší aplikace, logiku ověřování a logiku přístupu k databázi. Pokud například používáte Microsoft Entity Framework pro přístup k databázi, pak byste ve složce modely vytvořili vaše Entity Framework třídy (soubor. edmx).

Zobrazení by mělo obsahovat pouze logiku vztahující se k vygenerování uživatelského rozhraní. Kontroler by měl obsahovat pouze minimální logiku potřebnou k vrácení pravého zobrazení nebo přesměrování uživatele na jinou akci (řízení toku). Vše ostatní by mělo být obsaženo v modelu.

Obecně platí, že byste se měli snažit pro modely FAT a řadiče pro změny vzhledu. Vaše metody kontroleru by měly obsahovat pouze pár řádků kódu. Pokud akce kontroleru získá příliš systém souborů FAT, měli byste zvážit přesunutí logiky na novou třídu ve složce modely.

## <a name="summary"></a>Souhrn

Tento kurz vám poskytne přehled o různých částech webové aplikace ASP.NET MVC. Zjistili jste, jak směrování ASP.NET mapuje příchozí požadavky prohlížeče na konkrétní akce kontroleru. Zjistili jste, jak řadiče organizují způsob, jakým se vracejí zobrazení do prohlížeče. Nakonec jste zjistili, jak modely obsahují logiku aplikace, ověřování a přístup k databázi.

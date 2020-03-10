---
uid: web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
title: Vytvoření a použití pomocné rutiny na webu ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Tento článek popisuje, jak vytvořit pomocníka na webu ASP.NET Web Pages (Razor). Pomocná komponenta je opakovaně použitelná součást, která zahrnuje kód a označení ke výkonu...
ms.author: riande
ms.date: 02/17/2014
ms.assetid: 46bff772-01e0-40f0-9ae6-9e18c5442ee6
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/creating-and-using-a-helper-in-an-aspnet-web-pages-site
msc.type: authoredcontent
ms.openlocfilehash: 380663951094c9fc7d5f0601e30995fa073a204b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563509"
---
# <a name="creating-and-using-a-helper-in-an-aspnet-web-pages-razor-site"></a>Vytvoření a použití pomocné rutiny na webu ASP.NET Web Pages (Razor)

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek popisuje, jak vytvořit pomocníka na webu ASP.NET Web Pages (Razor). *Pomocná* komponenta je opakovaně použitelná součást, která obsahuje kód a kód k provedení úlohy, která může být zdlouhavá nebo složitá.
> 
> **Co se naučíte:** 
> 
> - Vytvoření a použití jednoduché pomocné rutiny.
> 
> Jedná se o funkce ASP.NET, které jsou představené v článku:
> 
> - Syntaxe `@helper`.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 3
>   
> 
> Tento kurz funguje také s ASP.NET webovými stránkami 2.

## <a name="overview-of-helpers"></a>Přehled pomocníků

Pokud potřebujete na různých stránkách na webu provádět stejné úlohy, můžete použít pomocníka. Webové stránky ASP.NET obsahují celou řadu pomocníků a je možné si je stáhnout a nainstalovat. (Seznam integrovaných pomocníků v ASP.NET Web Pages najdete v tématu [rychlý přehled rozhraní API pro ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202907).) Pokud žádný z stávajících pomocných rutin nevyhovuje vašim potřebám, můžete si vytvořit vlastní pomoc.

Pomocná pomůcka umožňuje použít společný blok kódu na více stránkách. Předpokládejme, že na stránce často chcete vytvořit položku poznámky, která je nastavena od normálních odstavců. Možná je Poznámka vytvořena jako prvek `<div>`, který je stylem pole s ohraničením. Místo toho, aby se stejný kód přidal na stránku pokaždé, když chcete zobrazit poznámku, můžete kód zabalit jako pomocný objekt. Pak můžete poznámku vložit s jedním řádkem kódu kdekoliv, kde ji potřebujete.

Použití pomocné rutiny umožňuje, aby byl kód v každé stránce jednodušší a čitelnější. Také usnadňuje údržbu webu, protože pokud potřebujete změnit vzhled poznámek, můžete změnit označení na jednom místě.

## <a name="creating-a-helper"></a>Vytvoření pomocné rutiny

V tomto postupu se dozvíte, jak vytvořit pomoc, která vytváří poznámku, jak je popsáno výše. Toto je jednoduchý příklad, ale vlastní pomoc může obsahovat jakýkoli kód kódu a ASP.NET, který potřebujete.

1. V kořenové složce webu vytvořte složku s názvem *App\_Code*. Toto je vyhrazený název složky v ASP.NET, kde můžete umístit kód pro součásti, jako jsou například pomocníky.
2. Ve složce *App\_Code* vytvořte nový soubor *. cshtml* a pojmenujte ho *MyHelpers. cshtml*.
3. Existující obsah nahraďte následujícím:

    [!code-cshtml[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample1.cshtml)]

    Kód používá syntaxi `@helper` k deklaraci nové pomocné rutiny s názvem `MakeNote`. Tato konkrétní pomocná pomoc vám umožní předat parametr s názvem `content`, který může obsahovat kombinaci textu a značky. Pomocník vloží řetězec do těla poznámky pomocí proměnné `@content`.

    Všimněte si, že soubor má název *MyHelpers. cshtml*, ale pomocník má název `MakeNote`. Do jednoho souboru můžete vložit několik vlastních pomocníků.
4. Uložte soubor a zavřete ho.

## <a name="using-the-helper-in-a-page"></a>Použití pomocné rutiny na stránce

1. V kořenové složce vytvořte nový prázdný soubor s názvem *TestHelper. cshtml*.
2. Do souboru přidejte následující kód:

    [!code-html[Main](creating-and-using-a-helper-in-an-aspnet-web-pages-site/samples/sample2.html)]

    Pokud chcete zavolat pomoc, kterou jste vytvořili, použijte `@` následovaný názvem souboru, kde je pomoc, tečka a pak název pomocné rutiny. (Pokud jste měli ve složce *App\_Code* více složek, můžete použít syntaxi `@FolderName.FileName.HelperName` k volání pomocné rutiny v rámci libovolné vnořené úrovně složky). Text, který přidáte do uvozovek v závorkách, je text, který pomocníka zobrazí jako součást poznámky na webové stránce.
3. Uložte stránku a spusťte ji v prohlížeči. Pomocná položka poznámky vygeneruje přímo tam, kde jste volali pomoc: mezi dvěma odstavci.

    ![Snímek obrazovky se stránkou v prohlížeči a způsob, jakým pomocník vygeneroval značku, která umístí kolem zadaného textu rámeček.](creating-and-using-a-helper-in-an-aspnet-web-pages-site/_static/image1.png)

## <a name="additional-resources"></a>Další prostředky

[Horizontální nabídka jako pomocníka Razor](http://mikepope.com/blog/DisplayBlog.aspx?permalink=2341) Tento záznam blogu pomocí Jan Pope ukazuje, jak vytvořit horizontální nabídku jako pomoc pomocí značek, šablon stylů CSS a kódu.

[Využití HTML5 v ASP.NET pomocníkech pro webové stránky pro WebMatrix a ASP.NET MvC3](http://geekswithblogs.net/wildturtle/archive/2010/11/08/html5-in-asp.net-web-pages-helpers-for-webmatrix-and_aspnet_mvc3.aspx). Tento záznam blogu pomocí Sam Abraham ukazuje pomoc, která vykresluje element HTML5 `Canvas`.

[Rozdíl mezi @Helpers a @Functions ve WebMatrixu](http://www.mikesdotnetting.com/Article/173/The-Difference-Between-@Helpers-and-@Functions-In-WebMatrix). Tento záznam blogu pomocí Jan slaného popisu popisuje `@helper` syntaxi syntaxe a `@function` a kdy je použít.

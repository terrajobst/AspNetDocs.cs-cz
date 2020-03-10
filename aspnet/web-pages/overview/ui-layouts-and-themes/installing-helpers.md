---
uid: web-pages/overview/ui-layouts-and-themes/installing-helpers
title: Instalace pomocné rutiny na webu ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Tento článek popisuje, jak nainstalovat pomocníka na webu ASP.NET Web Pages (Razor). Pomocná součást je opakovaně použitelná komponenta, která obsahuje kód a kód pro...
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 5e968ead-906a-45ea-ac2a-c70e57e1a9b1
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/installing-helpers
msc.type: authoredcontent
ms.openlocfilehash: 41e33c04a53a6ad257c3937cdadcec767e9217c8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638584"
---
# <a name="installing-a-helper-in-an-aspnet-web-pages-razor-site"></a>Instalace pomocné rutiny na webu ASP.NET Web Pages (Razor)

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek popisuje, jak nainstalovat pomocníka na webu ASP.NET Web Pages (Razor). *Pomocná* komponenta je opakovaně použitelná součást, která obsahuje kód a kód k provedení úlohy, která může být zdlouhavá nebo složitá.
> 
> Naučíte se:
> 
> - Postup instalace Pomocníka na webu vytvořeném pomocí WebMatrixu 3.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - WebMatrix 3

## <a name="overview-of-helpers"></a>Přehled pomocníků

Některé úlohy, které uživatelé často chtějí dělat na webových stránkách, vyžadují velké množství kódu nebo vyžadují další znalosti. Mezi příklady patří zobrazení grafu pro data; na stránce se zobrazí tlačítko sledování na Twitteru. odesílání e-mailů z webu oříznutí a změna velikosti imagí; používání služby PayPal pro váš web. Aby bylo možné tyto druhy věcí snadno provést, ASP.NET webové stránky vám umožní používat *pomocníka*. Pomocníky jsou komponenty, které nainstalujete pro lokalitu a umožňují provádět typické úlohy pomocí pouze řádku nebo dvou kódů Razor.

ASP.NET webové stránky mají několik vestavěných pomocníků. Mnoho pomocníků je však dostupných v balíčcích (Doplňky), které jsou k dispozici pomocí Správce balíčků NuGet. NuGet umožňuje vybrat balíček, který se má nainstalovat, a pak se postará o všechny podrobnosti o instalaci.

## <a name="installing-a-helper-in-webmatrix-3"></a>Instalace pomocné rutiny v WebMatrixu 3

1. V části WebMatrix 3 klikněte na tlačítko **NuGet** .

    ![Dialogové okno galerie NuGet v WebMatrixu](installing-helpers/_static/image1.png)
2. Spustí se správce balíčků NuGet a zobrazí dostupné balíčky. Do vyhledávacího pole zadejte klíčové slovo pro pomoc, kterou chcete nainstalovat.

    ![Dialogové okno galerie NuGet v WebMatrixu](installing-helpers/_static/image2.png)
3. Vyberte balíček a pak klikněte na **nainstalovat**. Po zobrazení výzvy klikněte na tlačítko **Ano** , pokud chcete balíček nainstalovat a označit, že souhlasíte s podmínkami.

     Pokud jste pomocníka nainstalovali poprvé, vytvoří NuGet ve vašem webu složky pro kód, který tvoří pomoc.
4. Chcete-li odinstalovat pomocníka, klikněte na tlačítko **Galerie** , klikněte na kartu **nainstalované** a vyberte balíček, který chcete odinstalovat.

## <a name="installing-the-twitter-helper"></a>Instalace pomocníka pro Twitter

Nejnovější verze rozhraní Twitter API není kompatibilní s pomocníkem pro Twitter, který nainstalujete přes NuGet. Místo toho se podívejte na informace o tom, jak v projektu nastavit pomocníka pro Twitter, v tématu [WebMatrix Pomocník pro Twitter](twitter-helper.md) .

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Další prostředky

[Představujeme ASP.NET webové stránky 2 – základy programování](../getting-started/introducing-razor-syntax-c.md)

[Pomocník pro Twitter s webmatrixem](twitter-helper.md)

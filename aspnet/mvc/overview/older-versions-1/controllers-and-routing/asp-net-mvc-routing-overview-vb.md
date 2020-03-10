---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
title: ASP.NET MVC – Přehled směrování (VB) | Microsoft Docs
author: StephenWalther
description: V tomto kurzu Stephen Walther ukazuje, jak Framework ASP.NET MVC mapuje požadavky prohlížeče na akce kontroleru.
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 4bc8d19a-80f1-44b4-adbf-95ed22d691ca
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: ed043d76b89ce31945cf3423b0c5afca9383cc21
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601533"
---
# <a name="aspnet-mvc-routing-overview-vb"></a>ASP.NET MVC – přehled směrování (VB)

od [Stephen Walther](https://github.com/StephenWalther)

> V tomto kurzu Stephen Walther ukazuje, jak Framework ASP.NET MVC mapuje požadavky prohlížeče na akce kontroleru.

V tomto kurzu se zavedete na důležitou funkci každé aplikace ASP.NET MVC s názvem *směrování ASP.NET*. Modul směrování ASP.NET zodpovídá za mapování příchozích požadavků prohlížeče na konkrétní akce kontroleru MVC. Na konci tohoto kurzu budete rozumět tomu, jak standardní směrovací tabulka vyžádá požadavky na akce kontroleru.

## <a name="using-the-default-route-table"></a>Použití výchozí směrovací tabulky

Když vytvoříte novou aplikaci ASP.NET MVC, aplikace je už nakonfigurovaná tak, aby používala směrování ASP.NET. Směrování ASP.NET se nastaví na dvou místech.

V konfiguračním souboru webu aplikace (soubor Web. config) je nejprve povoleno směrování ASP.NET. Konfigurační soubor obsahuje čtyři části, které jsou důležité pro směrování: oddíl System. Web. httpModules, System. Web. httpHandlers, System. webServer. Modules a System. webServer. handlers. Dejte pozor, abyste tyto oddíly neodstranili, protože bez těchto oddílů nebude směrování nadále fungovat.

Druhé a důležitější je, že směrovací tabulka se vytvoří v souboru Global. asax aplikace. Soubor Global. asax je speciální soubor, který obsahuje obslužné rutiny událostí pro události životního cyklu aplikace ASP.NET. Směrovací tabulka se vytvoří během události spuštění aplikace.

Soubor v seznamu 1 obsahuje výchozí soubor Global. asax pro aplikaci ASP.NET MVC.

**Výpis 1 – Global. asax. vb**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample1.vb)]

Při prvním spuštění aplikace MVC je volána metoda aplikace\_Start (). Tato metoda pak zavolá metodu RegisterRoutes (). Metoda RegisterRoutes () vytvoří směrovací tabulku.

Výchozí směrovací tabulka obsahuje jednu trasu (s názvem Default). Výchozí trasa namapuje první segment adresy URL na název kontroleru, druhý segment adresy URL na akci kontroleru a třetí segment na parametr s názvem **ID**.

Představte si, že do adresního řádku webového prohlížeče zadáte následující adresu URL:

/Home/Index/3

Výchozí trasa mapuje tuto adresu URL na následující parametry:

- Controller = domů

- Action = index

- id = 3

Po vyžádání adresy URL/Home/Index/3 se spustí následující kód:

HomeController. index (3)

Výchozí trasa obsahuje výchozí hodnoty pro všechny tři parametry. Pokud řadič nezadáte, použije se výchozí hodnota parametru Controller na hodnotu **Home**. Pokud akci nezadáte, použije se jako výchozí parametr akce **index**hodnoty. Nakonec, pokud nezadáte ID, parametr ID se nastaví jako prázdný řetězec.

Pojďme se podívat na několik příkladů, jak výchozí trasa mapuje adresy URL na akce kontroleru. Představte si, že do adresního řádku prohlížeče zadáte následující adresu URL:

/Home

Z důvodu výchozí výchozí hodnoty parametrů trasy bude zadání této adresy URL způsobit volání metody index () třídy HomeController v seznamu 2.

**Výpis 2-HomeController. vb**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample2.vb)]

V seznamu 2 třída HomeController obsahuje metodu s názvem index (), která přijímá jeden parametr s názvem ID. Adresa URL/Home způsobí, že metoda index () bude volána s hodnotou Nothing jako hodnota parametru ID.

Z důvodu způsobu, jakým rozhraní MVC Framework vyvolá akce kontroleru, adresa URL/Home také odpovídá metodě index () třídy HomeController v seznamu 3.

**Výpis 3-HomeController. vb (akce indexu bez parametru)**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample3.vb)]

Metoda index () v seznamu 3 nepřijímá žádné parametry. Adresa URL/Home způsobí volání této metody index (). Adresa URL/Home/Index/3 také vyvolá tuto metodu (ID je ignorováno).

Adresa URL/Home také odpovídá metodě index () třídy HomeController v seznamu 4.

**Výpis 4-HomeController. vb (akce indexu s parametrem s možnou hodnotou null)**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample4.vb)]

V seznamu 4 má metoda index () jeden celočíselný parametr. Vzhledem k tomu, že parametr je parametr s možnou hodnotou null (může mít hodnotu Nothing), index () lze volat bez vyvolání chyby.

Nakonec volání metody index () v seznamu 5 s adresou URL/Home způsobí výjimku, protože parametr *ID není parametr s* možnou hodnotou null. Pokud se pokusíte vyvolat metodu index (), zobrazí se chyba na obrázku 1.

**Výpis 5-HomeController. vb (akce indexu s parametrem ID)**

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample5.vb)]

[![volání akce kontroleru, která očekává hodnotu parametru.](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)

**Obrázek 01**: vyvolání akce kontroleru, která očekává hodnotu parametru ([kliknutím zobrazíte obrázek v plné velikosti](asp-net-mvc-routing-overview-vb/_static/image2.png)).

Adresa URL/Home/Index/3 na druhé straně funguje pouze v případě, že se jedná o akci řadiče indexu v seznamu 5. Požadavek/Home/Index/3 způsobí, že metoda index () bude volána s parametrem ID, který má hodnotu 3.

## <a name="summary"></a>Souhrn

Cílem tohoto kurzu je poskytnout stručný úvod k ASP.NET směrování. Prozkoumali jsme výchozí směrovací tabulku, kterou získáte pomocí nové aplikace ASP.NET MVC. Zjistili jste, jak výchozí trasa mapuje adresy URL na akce kontroleru.

> [!div class="step-by-step"]
> [Předchozí](creating-an-action-cs.md)
> [Další](understanding-action-filters-vb.md)

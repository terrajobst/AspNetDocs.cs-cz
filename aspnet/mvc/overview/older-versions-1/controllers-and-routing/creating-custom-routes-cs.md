---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
title: Vytváření vlastních tras (C#) | Microsoft Docs
author: microsoft
description: Naučte se přidávat vlastní trasy do aplikace ASP.NET MVC. V tomto kurzu se naučíte, jak změnit výchozí směrovací tabulku v souboru Global. asax.
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 3cd08f02-8763-490a-b625-2ac96a24b73f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-cs
msc.type: authoredcontent
ms.openlocfilehash: 58f72e390f0053d136ef00ddbda0b071ba225d98
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601330"
---
# <a name="creating-custom-routes-c"></a>Vytváření vlastních tras (C#)

od [Microsoftu](https://github.com/microsoft)

> Naučte se přidávat vlastní trasy do aplikace ASP.NET MVC. V tomto kurzu se naučíte, jak změnit výchozí směrovací tabulku v souboru Global. asax.

V tomto kurzu se dozvíte, jak přidat vlastní trasu do aplikace ASP.NET MVC. Naučíte se, jak upravit výchozí směrovací tabulku v souboru Global. asax pomocí vlastní trasy.

Pro spoustu jednoduchých aplikací ASP.NET MVC bude výchozí směrovací tabulka fungovat přesně přesně. Můžete ale zjistit, že máte specializované požadavky na směrování. V takovém případě můžete vytvořit vlastní trasu.

Představte si například, že vytváříte aplikaci blogu. Můžete chtít zpracovat příchozí požadavky, které vypadají takto:

/Archive/12-25-2009

Když uživatel zadá tuto žádost, budete chtít vrátit položku blogu, která odpovídá datu 12/25/2009. Aby bylo možné tento typ žádosti zpracovat, je nutné vytvořit vlastní trasu.

Soubor Global. asax v seznamu 1 obsahuje novou vlastní trasu s názvem blog, která zpracovává požadavky, které vypadají jako/Archive/*Datum vstupu*.

**Výpis 1-Global. asax (s vlastním směrováním)**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample1.cs)]

Pořadí tras, které přidáte do směrovací tabulky, je důležité. Do existující výchozí trasy se přidá nová vlastní trasa blogu. Pokud jste objednávku přeměnili, bude se výchozí trasa místo vlastní trasy volat vždy.

Vlastní trasa blogu odpovídá všem žádostem, které začínají na/Archive/. Proto odpovídá všem následujícím adresám URL:

- /Archive/12-25-2009

- /Archive/10-6-2004

- /Archive/apple

Vlastní trasa mapuje příchozí požadavek na kontroler s názvem Archive a vyvolá akci entry (). Při volání metody entry () se datum položky předává jako parametr s názvem entryDate.

Můžete použít vlastní trasu blogu s řadičem v seznamu 2.

**Výpis 2 – ArchiveController.cs**

[!code-csharp[Main](creating-custom-routes-cs/samples/sample2.cs)]

Všimněte si, že metoda Entry () v seznamu 2 přijímá parametr typu DateTime. Rozhraní MVC je dostatečně inteligentní, aby bylo možné převést datum zadání z adresy URL na hodnotu DateTime automaticky. Pokud nelze parametr data entry z adresy URL převést na typ DateTime, je vyvolána chyba (viz obrázek 1).

**Obrázek 1 – Chyba při převádění parametru**

[![dialogového okna Nový projekt](creating-custom-routes-cs/_static/image1.jpg)](creating-custom-routes-cs/_static/image1.png)

**Obrázek 01**: Chyba při převádění parametru ([kliknutím zobrazíte obrázek v plné velikosti](creating-custom-routes-cs/_static/image2.png))

## <a name="summary"></a>Souhrn

Cílem tohoto kurzu je Ukázat, jak můžete vytvořit vlastní trasu. Zjistili jste, jak přidat vlastní trasu do směrovací tabulky v souboru Global. asax, který představuje položky blogu. Probrali jsme, jak mapovat požadavky na položky blogu na kontroler s názvem ArchiveController a akci kontroleru s názvem entry ().

> [!div class="step-by-step"]
> [Předchozí](aspnet-mvc-controllers-overview-cs.md)
> [Další](creating-a-route-constraint-cs.md)

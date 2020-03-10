---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
title: Vytvoření akce (C#) | Microsoft Docs
author: microsoft
description: Přečtěte si, jak přidat novou akci k řadiči ASP.NET MVC. Seznamte se s požadavky na metodu, která může být akcí.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: cb33b28c-3025-4bd1-a1fa-eaa3af7bb56f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-cs
msc.type: authoredcontent
ms.openlocfilehash: ebba935383819935ad85c95245666f4eaf6a0dca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582052"
---
# <a name="creating-an-action-c"></a>Vytvoření akce (C#)

od [Microsoftu](https://github.com/microsoft)

> Přečtěte si, jak přidat novou akci k řadiči ASP.NET MVC. Seznamte se s požadavky na metodu, která může být akcí.

Cílem tohoto kurzu je vysvětlit, jak můžete vytvořit novou akci kontroleru. Získáte informace o požadavcích metody akce. Naučíte se také, jak zabránit tomu, aby byla metoda vystavena jako akce.

## <a name="adding-an-action-to-a-controller"></a>Přidání akce do kontroleru

Přidáte novou akci do kontroleru přidáním nové metody do kontroleru. Například kontroler v výpisu 1 obsahuje akci s názvem index () a akci s názvem SayHello (). Obě metody jsou zpřístupněny jako akce.

**Výpis 1 – souboru controllers\homecontroller.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample1.cs)]

Aby bylo možné zveřejnit celému základnímu objektu jako akci, metoda musí splňovat určité požadavky:

- Metoda musí být veřejná.
- Metoda nemůže být statickou metodou.
- Metoda nemůže být metodou rozšíření.
- Metoda nemůže být konstruktor, getter nebo setter.
- Metoda nemůže mít otevřené obecné typy.
- Metoda není metodou základní třídy kontroleru.
- Metoda nemůže obsahovat parametry **ref** nebo **out** .

Všimněte si, že pro návratový typ akce kontroleru neexistují žádná omezení. Akce kontroleru může vracet řetězec, datum a čas, instanci náhodné třídy nebo void. Rozhraní ASP.NET MVC převede libovolný návratový typ, který není výsledkem akce, do řetězce a vykreslí řetězec do prohlížeče.

Když přidáte libovolnou metodu, která porušuje tyto požadavky na kontroler, je metoda vystavena jako akce kontroleru. Buďte opatrní. Akci kontroleru může vyvolat kdokoli připojený k Internetu. Nevytvářejte například akci kontroleru DeleteMyWebsite ().

## <a name="preventing-a-public-method-from-being-invoked"></a>Zabránění vyvolání veřejné metody

Pokud potřebujete vytvořit veřejnou metodu ve třídě kontroleru a nechcete ji zveřejnit jako akci kontroleru, můžete zabránit vyvolání metody pomocí atributu [neaction]. Například kontroler v seznamu 2 obsahuje veřejnou metodu s názvem CompanySecrets (), která je upravena atributem [neaction].

**Výpis 2 – Controllers\WorkController.cs**

[!code-csharp[Main](creating-an-action-cs/samples/sample2.cs)]

Pokud se pokusíte vyvolat akci kontroleru CompanySecrets () tak, že do panelu Adresa v prohlížeči zadáte/Work/CompanySecrets, zobrazí se chybová zpráva na obrázku 1.

[![vyvolání metody nečinnosti](creating-an-action-cs/_static/image1.jpg)](creating-an-action-cs/_static/image1.png)

**Obrázek 01**: vyvolání metody nečinnosti ([kliknutím zobrazíte obrázek v plné velikosti](creating-an-action-cs/_static/image2.png))

> [!div class="step-by-step"]
> [Předchozí](creating-a-controller-cs.md)
> [Další](asp-net-mvc-routing-overview-vb.md)

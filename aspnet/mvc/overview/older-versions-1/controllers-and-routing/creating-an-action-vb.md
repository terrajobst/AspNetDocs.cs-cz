---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: Vytvoření akce (VB) | Microsoft Docs
author: microsoft
description: Přečtěte si, jak přidat novou akci k řadiči ASP.NET MVC. Seznamte se s požadavky na metodu, která může být akcí.
ms.author: riande
ms.date: 03/02/2009
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: b1b53bea899deecef203551b23c087944e3990ab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582003"
---
# <a name="creating-an-action-vb"></a>Vytvoření akce (VB)

od [Microsoftu](https://github.com/microsoft)

> Přečtěte si, jak přidat novou akci k řadiči ASP.NET MVC. Seznamte se s požadavky na metodu, která může být akcí.

Cílem tohoto kurzu je vysvětlit, jak můžete vytvořit novou akci kontroleru. Získáte informace o požadavcích metody akce. Naučíte se také, jak zabránit tomu, aby byla metoda vystavena jako akce.

## <a name="adding-an-action-to-a-controller"></a>Přidání akce do kontroleru

Přidáte novou akci do kontroleru přidáním nové metody do kontroleru. Například kontroler v výpisu 1 obsahuje akci s názvem index () a akci s názvem SayHello (). Obě metody jsou zpřístupněny jako akce.

**Výpis 1 – Controllers\HomeController.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

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

Pokud potřebujete vytvořit veřejnou metodu ve třídě kontroleru a nechcete tuto metodu vystavit jako akci kontroleru, můžete zabránit vyvolání metody pomocí&gt; atributu &lt;nečinnosti. Například kontroler v seznamu 2 obsahuje veřejnou metodu s názvem CompanySecrets (), která je upravena pomocí&gt; atributu &lt;nečinnosti.

**Výpis 2 – Controllers\WorkController.vb**

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

Pokud se pokusíte vyvolat akci kontroleru CompanySecrets () tak, že do panelu Adresa v prohlížeči zadáte/Work/CompanySecrets, zobrazí se chybová zpráva na obrázku 1.

[![vyvolání metody nečinnosti](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)

**Obrázek 01**: vyvolání metody nečinnosti ([kliknutím zobrazíte obrázek v plné velikosti](creating-an-action-vb/_static/image2.png))

> [!div class="step-by-step"]
> [Předchozí](creating-a-controller-vb.md)
> [Další](aspnet-mvc-controllers-overview-cs.md)

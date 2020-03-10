---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-cs
title: Vytváření vlastního omezení trasy (C#) | Microsoft Docs
author: StephenWalther
description: Stephen Walther ukazuje, jak můžete vytvořit vlastní omezení trasy. Implementujeme jednoduché vlastní omezení, které brání tomu, aby se trasa shodovala s...
ms.author: riande
ms.date: 02/16/2009
ms.assetid: a4f4bf4e-abcc-4650-8f43-527e48b52fe6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 98d5839e3d2623665770ccc5689c28f9eb29c8f6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601449"
---
# <a name="creating-a-custom-route-constraint-c"></a>Vytvoření vlastního omezení trasy (C#)

od [Stephen Walther](https://github.com/StephenWalther)

> Stephen Walther ukazuje, jak můžete vytvořit vlastní omezení trasy. Implementujeme jednoduché vlastní omezení, které zabrání tomu, aby se trasa shodovala s tím, jak se ze vzdáleného počítače provede požadavek prohlížeče.

Cílem tohoto kurzu je Ukázat, jak můžete vytvořit vlastní omezení trasy. Vlastní omezení trasy vám umožní zabránit tomu, aby se trasa shodovala, pokud se neshoduje nějaká vlastní podmínka.

V tomto kurzu vytvoříme omezení trasy localhost. Omezení trasy localhost se shoduje pouze s požadavky provedenými z místního počítače. Vzdálené požadavky přes Internet se neshodují.

Vlastní omezení trasy implementujete implementací rozhraní omezení IRouteConstraint. Toto je extrémně jednoduché rozhraní, které popisuje jedinou metodu:

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample1.cs)]

Metoda vrací logickou hodnotu. Pokud vrátíte hodnotu false, trasa přidružená k omezení nebude odpovídat požadavku prohlížeče.

Omezení localhost je obsaženo v seznamu 1.

**Výpis 1 – LocalhostConstraint.cs**

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample2.cs)]

Omezení v výpisu 1 využívá vlastnost místní vystavenou třídou HttpRequest. Tato vlastnost vrátí hodnotu true, pokud je IP adresa požadavku buď 127.0.0.1, nebo pokud je IP adresa požadavku shodná s IP adresou serveru.

Použijete vlastní omezení v rámci trasy definované v souboru Global. asax. Soubor Global. asax v seznamu 2 používá omezení localhost k tomu, aby nikdo nemohl požádat o stránku správce, pokud nevytvoří požadavek z místního serveru. Například požadavek na/Admin/DeleteAll selže při provedení ze vzdáleného serveru.

**Výpis 2 – Global. asax**

[!code-csharp[Main](creating-a-custom-route-constraint-cs/samples/sample3.cs)]

V definici trasy správce se používá omezení localhost. Tato trasa nebude odpovídat požadavku vzdáleného prohlížeče. Upozorňujeme však, že jiné trasy definované v Global. asax mohou odpovídat stejné žádosti. Je důležité pochopit, že omezení brání konkrétní trase v porovnání s požadavkem, a ne všechny trasy definované v souboru Global. asax.

Všimněte si, že výchozí trasa byla zakomentována ze souboru Global. asax v seznamu 2. Pokud zahrnete výchozí trasu, bude výchozí trasa odpovídat požadavkům pro kontroler správce. V takovém případě mohou vzdálení uživatelé i přesto vyvolat akce kontroleru správce, i když jejich požadavky by neodpovídaly trase správce.

> [!div class="step-by-step"]
> [Předchozí](creating-a-route-constraint-cs.md)
> [Další](asp-net-mvc-controller-overview-vb.md)

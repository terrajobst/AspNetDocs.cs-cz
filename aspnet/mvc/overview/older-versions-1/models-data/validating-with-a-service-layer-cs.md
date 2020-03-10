---
uid: mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
title: Ověřování pomocí vrstvy služby (C#) | Microsoft Docs
author: StephenWalther
description: Naučte se, jak přesunout logiku ověřování z akcí kontroleru a do samostatné vrstvy služby. V tomto kurzu Stephen Walther vysvětluje, jak vás...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 4eabc535-b8a1-43f5-bb99-cfeb86db0fca
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validating-with-a-service-layer-cs
msc.type: authoredcontent
ms.openlocfilehash: da1a1c9cc79a452eb0d7597810e86f7bcf6cd179
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542859"
---
# <a name="validating-with-a-service-layer-c"></a>Ověřování vrstvou služby (C#)

od [Stephen Walther](https://github.com/StephenWalther)

> Naučte se, jak přesunout logiku ověřování z akcí kontroleru a do samostatné vrstvy služby. V tomto kurzu Stephen Walther vysvětluje, jak můžete udržovat ostré oddělení potíží tím, že izolujete vrstvu služby od vrstvy řadiče.

Cílem tohoto kurzu je popsat jednu metodu provádění ověřování v aplikaci ASP.NET MVC. V tomto kurzu se naučíte přesunout logiku ověřování z vašich řadičů a do samostatné vrstvy služby.

## <a name="separating-concerns"></a>Oddělení obav

Při sestavování aplikace ASP.NET MVC byste neměli umístit logiku databáze do akcí kontroleru. Kombinování databáze a logiky kontroleru usnadňuje údržbu vaší aplikace v průběhu času. Doporučení je, abyste všechny své databázové logiky umístili do samostatné vrstvy úložiště.

Například výpis 1 obsahuje jednoduché úložiště s názvem ProductRepository. Úložiště produktu obsahuje veškerý kód pro přístup k datům pro aplikaci. Výpis zahrnuje také rozhraní IProductRepository, které implementuje úložiště produktu.

**Výpis 1 – Models\ProductRepository.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample1.cs)]

Kontroler v seznamu 2 používá vrstvu úložiště v akcích index () a Create (). Všimněte si, že tento kontroler neobsahuje žádnou databázovou logiku. Vytvoření vrstvy úložiště vám umožní udržovat čisté oddělení obav. Řadiče jsou zodpovědné za logiku řízení toku aplikace a úložiště zodpovídá za logiku přístupu k datům.

**Výpis 2 – Controllers\ProductController.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample2.cs)]

## <a name="creating-a-service-layer"></a>Vytvoření vrstvy služby

Takže logika řízení toku aplikace patří do řadiče a logika přístupu k datům patří do úložiště. V takovém případě, kam umístíte logiku ověřování? Jednou z možností je umístit logiku ověřování ve *vrstvě služeb*.

Vrstva služeb je další vrstva v aplikaci ASP.NET MVC, která řeší komunikaci mezi řadičem a vrstvou úložiště. Vrstva služby obsahuje obchodní logiku. Konkrétně obsahuje logiku ověřování.

Například vrstva produktové služby v seznamu 3 má metodu CreateProduct (). Metoda CreateProduct () volá metodu ValidateProduct () pro ověření nového produktu před předáním produktu do úložiště produktu.

**Výpis 3 – Models\ProductService.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample3.cs)]

V seznamu 4 byl aktualizován produkt, aby místo vrstvy úložiště používal vrstvu služby. Vrstva kontroleru mluví do vrstvy služeb. Vrstva služby mluví s vrstvou úložiště. Každá vrstva má samostatnou zodpovědnost.

**Výpis 4 – Controllers\ProductController.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample4.cs)]

Všimněte si, že Produktová služba je vytvořena v konstruktoru produktového kontroleru. Po vytvoření produktové služby je slovník stavu modelu předán službě. Produktová služba používá stav modelu k předání chybových zpráv ověřování zpět do kontroleru.

## <a name="decoupling-the-service-layer"></a>Oddělení vrstvy služby

Nepovedlo se nám izolovat řadiče a vrstvy služeb v jednom ohledu. Vrstva řadiče a služeb komunikuje přes stav modelu. Jinými slovy, vrstva služby má závislost na konkrétní funkci architektury ASP.NET MVC.

Doporučujeme izolovat vrstvu služby z naší vrstvy řadiče co nejvíce. Teoreticky byste měli být schopni používat vrstvu služby s jakýmkoli typem aplikace, a ne pouze aplikace ASP.NET MVC. V budoucnu můžeme například pro naši aplikaci vytvořit front-end pro WPF. Měli bychom najít způsob, jak z naší vrstvy služby odebrat závislost na stav modelu ASP.NET MVC.

V seznamu 5 se vrstva služby aktualizovala tak, aby už nepoužívala stav modelu. Místo toho používá libovolnou třídu, která implementuje rozhraní IValidationDictionary.

**Výpis 5-Models\ProductService.cs (oddělené)**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample5.cs)]

Rozhraní IValidationDictionary je definováno v výpisu 6. Toto jednoduché rozhraní má jedinou metodu a jedinou vlastnost.

**Výpis 6 – Models\IValidationDictionary.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample6.cs)]

Třída v seznamu 7 s názvem třídy ModelStateWrapper implementuje rozhraní IValidationDictionary. Můžete vytvořit instanci třídy ModelStateWrapper předáním slovníku stavu modelu do konstruktoru.

**Výpis 7 – Models\ModelStateWrapper.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample7.cs)]

Nakonec aktualizovaný kontroler v seznamu 8 používá ModelStateWrapper při vytváření vrstvy služby ve svém konstruktoru.

**Výpis 8 – Controllers\ProductController.cs**

[!code-csharp[Main](validating-with-a-service-layer-cs/samples/sample8.cs)]

Použití rozhraní IValidationDictionary a třídy ModelStateWrapper nám umožňuje zcela izolovat naši vrstvu služeb od naší vrstvy kontroleru. Vrstva služby již není závislá na stavu modelu. Můžete předat libovolnou třídu, která implementuje rozhraní IValidationDictionary, do vrstvy služby. Například aplikace WPF může implementovat rozhraní IValidationDictionary s jednoduchou třídou kolekce.

## <a name="summary"></a>Souhrn

Cílem tohoto kurzu bylo projednat jeden přístup k provádění ověřování v aplikaci ASP.NET MVC. V tomto kurzu jste zjistili, jak přesunout veškerou logiku ověřování z vašich řadičů do samostatné vrstvy služby. Zjistili jste také, jak izolovat vrstvu služby z vaší vrstvy kontroleru vytvořením třídy ModelStateWrapper.

> [!div class="step-by-step"]
> [Předchozí](validating-with-the-idataerrorinfo-interface-cs.md)
> [Další](validation-with-the-data-annotation-validators-cs.md)

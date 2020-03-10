---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
title: Vytváření testů jednotek pro aplikace ASP.NET MVC (C#) | Microsoft Docs
author: StephenWalther
description: Naučte se vytvářet testy jednotek pro akce kontroleru. V tomto kurzu Stephen Walther ukazuje, jak otestovat, zda akce kontroleru vrátí Parti...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: d3a270b9-d7b1-47f2-8775-fc3beb518b5c
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-cs
msc.type: authoredcontent
ms.openlocfilehash: 35fd0d85c63e5bd196394ce11b851c822a6405d9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623940"
---
# <a name="creating-unit-tests-for-aspnet-mvc-applications-c"></a>Vytváření testů jednotek pro aplikace ASP.NET MVC (C#)

od [Stephen Walther](https://github.com/StephenWalther)

[Stáhnout PDF](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_CS.pdf)

> Naučte se vytvářet testy jednotek pro akce kontroleru. V tomto kurzu Stephen Walther ukazuje, jak otestovat, zda akce kontroleru vrátí konkrétní zobrazení, vrátí konkrétní sadu dat nebo vrátí jiný typ výsledku akce.

Cílem tohoto kurzu je Ukázat, jak můžete napsat testy jednotek pro řadiče v aplikacích ASP.NET MVC. Probereme, jak sestavit tři různé typy testů jednotek. Zjistíte, jak otestovat zobrazení vrácené akcí kontroleru, jak otestovat zobrazení dat vrácených akcí kontroleru a jak otestovat, jestli jedna akce kontroleru vás přesměruje na druhou akci kontroleru.

## <a name="creating-the-controller-under-test"></a>Vytváření kontroleru v rámci testu

Pojďme začít vytvořením kontroleru, který chcete otestovat. Kontroler s názvem `ProductController`je obsažený v seznamu 1.

**Výpis 1 – `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample1.cs)]

`ProductController` obsahuje dvě metody akcí s názvem `Index()` a `Details()`. Obě metody akcí vrací zobrazení. Všimněte si, že akce `Details()` přijímá parametr s názvem ID.

## <a name="testing-the-view-returned-by-a-controller"></a>Testování zobrazení vráceného řadičem

Představte si, že chceme testovat, zda `ProductController` vrátí pravé zobrazení. Chceme zajistit, aby při vyvolání `ProductController.Details()` akce se zobrazilo zobrazení podrobností. Třída testu v seznamu 2 obsahuje test jednotky pro testování zobrazení vráceného akcí `ProductController.Details()`.

**Výpis 2 – `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample2.cs)]

Třída v seznamu 2 obsahuje testovací metodu s názvem `TestDetailsView()`. Tato metoda obsahuje tři řádky kódu. První řádek kódu vytvoří novou instanci třídy `ProductController`. Druhý řádek kódu vyvolá metodu `Details()` akce kontroleru. Nakonec poslední řádek kódu ověří, zda zobrazení vrácené akcí `Details()` je zobrazení podrobností.

Vlastnost `ViewResult.ViewName` představuje název zobrazení vráceného řadičem. Jedno velké upozornění na testování této vlastnosti. Existují dva způsoby, jak může kontroler vrátit zobrazení. Kontroler může explicitně vrátit zobrazení takto:

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample3.cs)]

Případně můžete název zobrazení odvodit z názvu akce řadiče, jako je tato:

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample4.cs)]

Tato akce kontroleru také vrátí zobrazení s názvem `Details`. Název zobrazení je ale odvozený od názvu akce. Chcete-li otestovat název zobrazení, je nutné explicitně vrátit název zobrazení z akce kontroleru.

Test jednotky můžete spustit v seznamu 2 zadáním kombinace kláves **CTRL-R,** nebo kliknutím na tlačítko **Spustit všechny testy v řešení** (viz obrázek 1). Pokud se test projde, zobrazí se okno Výsledky testů na obrázku 2.

[![spustit všechny testy v řešení](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image1.png)

**Obrázek 01**: spuštění všech testů v řešení ([kliknutím zobrazíte obrázek v plné velikosti](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image3.png))

[![úspěch!](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image4.png)

**Obrázek 02**: úspěch! ([Kliknutím zobrazíte obrázek v plné velikosti.](creating-unit-tests-for-asp-net-mvc-applications-cs/_static/image6.png))

## <a name="testing-the-view-data-returned-by-a-controller"></a>Testování zobrazení dat vrácených řadičem

Kontroler MVC předává data do zobrazení pomocí objektu s názvem *`View Data`* . Představte si například, že chcete zobrazit podrobnosti o konkrétním produktu při vyvolání akce `ProductController Details()`. V takovém případě můžete vytvořit instanci `Product` třídy (definované v modelu) a předat instanci do zobrazení `Details` tím, že využijete `View Data`.

Upravený `ProductController` v seznamu 3 obsahuje aktualizovanou `Details()` akci, která vrátí produkt.

**Výpis 3 – `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample5.cs)]

Nejprve akce `Details()` vytvoří novou instanci třídy `Product`, která představuje přenosný počítač. Dále instance třídy `Product` je předána jako druhý parametr metodě `View()`.

Můžete napsat testy jednotek k otestování, zda jsou očekávaná data obsažena v zobrazení dat. Testování částí v seznamu 4 testuje, zda je při volání metody `ProductController Details()` akce vrácen produkt představující přenosný počítač.

**Výpis 4 – `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample6.cs)]

V výpisu 4 `TestDetailsView()` metoda Testuje data zobrazení vrácená voláním metody `Details()`. `ViewData` je vystavena jako vlastnost `ViewResult` vrácená voláním metody `Details()`. Vlastnost `ViewData.Model` obsahuje produkt předaný do zobrazení. Test jednoduše ověří, že produkt obsažený v zobrazení dat má název přenosného počítače.

## <a name="testing-the-action-result-returned-by-a-controller"></a>Testování výsledku akce vráceného řadičem

Složitější akce kontroleru může vracet různé typy výsledků akce v závislosti na hodnotách parametrů předaných do akce kontroleru. Akce kontroleru může vracet různé typy výsledků akce včetně `ViewResult`, `RedirectToRouteResult`nebo `JsonResult`.

Například upravená akce `Details()` v seznamu 5 vrátí zobrazení `Details` při předání platného ID produktu do akce. Pokud předáte neplatné ID produktu – ID s hodnotou menší než 1 –, budete přesměrováni na `Index()` akci.

**Výpis 5 – `ProductController.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample7.cs)]

Chování `Details()` akce můžete otestovat pomocí testu jednotek v seznamu 6. Testování částí v seznamu 6 ověřuje, že jste přesměrováni do zobrazení `Index`, když je ID s hodnotou-1 předáno metodě `Details()`.

**Výpis 6 – `ProductControllerTest.cs`**

[!code-csharp[Main](creating-unit-tests-for-asp-net-mvc-applications-cs/samples/sample8.cs)]

Když zavoláte metodu `RedirectToAction()` v akci kontroleru, akce kontroleru vrátí `RedirectToRouteResult`. Test ověří, zda `RedirectToRouteResult` přesměruje uživatele na akci kontroleru s názvem `Index`.

## <a name="summary"></a>Souhrn

V tomto kurzu jste zjistili, jak sestavit testy jednotek pro akce kontroleru MVC. Nejprve jste zjistili, jak ověřit, zda je vráceno správné zobrazení pomocí akce kontroleru. Zjistili jste, jak použít vlastnost `ViewResult.ViewName` k ověření názvu zobrazení.

Dále jsme zkoumali, jak můžete testovat obsah `View Data`. Zjistili jste, jak ověřit, zda byl po volání akce kontroleru vrácen správný produkt v `View Data`.

Nakonec jsme probrali, jak můžete testovat, zda jsou z akce kontroleru vráceny různé typy výsledků akce. Zjistili jste, jak otestovat, zda kontroler vrací `ViewResult` nebo `RedirectToRouteResult`.

> [!div class="step-by-step"]
> [Next](creating-unit-tests-for-asp-net-mvc-applications-vb.md)

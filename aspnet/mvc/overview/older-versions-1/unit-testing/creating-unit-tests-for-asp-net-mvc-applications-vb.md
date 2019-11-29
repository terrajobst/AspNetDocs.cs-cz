---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-vb
title: Vytváření testů jednotek pro aplikace ASP.NET MVC (VB) | Microsoft Docs
author: StephenWalther
description: Naučte se vytvářet testy jednotek pro akce kontroleru. V tomto kurzu Stephen Walther ukazuje, jak otestovat, zda akce kontroleru vrátí Parti...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: eb35710d-1d99-44ac-b61f-e50af8cb328a
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-vb
msc.type: authoredcontent
ms.openlocfilehash: 643faddaf6f9cd075131e8e5a9cccb303e355ceb
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594694"
---
# <a name="creating-unit-tests-for-aspnet-mvc-applications-vb"></a>Vytváření testů jednotek pro aplikace ASP.NET MVC (VB)

od [Stephen Walther](https://github.com/StephenWalther)

[Stáhnout PDF](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_VB.pdf)

> Naučte se vytvářet testy jednotek pro akce kontroleru. V tomto kurzu Stephen Walther ukazuje, jak otestovat, zda akce kontroleru vrátí konkrétní zobrazení, vrátí konkrétní sadu dat nebo vrátí jiný typ výsledku akce.

Cílem tohoto kurzu je Ukázat, jak můžete napsat testy jednotek pro řadiče v aplikacích ASP.NET MVC. Probereme, jak sestavit tři různé typy testů jednotek. Zjistíte, jak otestovat zobrazení vrácené akcí kontroleru, jak otestovat zobrazení dat vrácených akcí kontroleru a jak otestovat, jestli jedna akce kontroleru vás přesměruje na druhou akci kontroleru.

## <a name="creating-the-controller-under-test"></a>Vytváření kontroleru v rámci testu

Pojďme začít vytvořením kontroleru, který chcete otestovat. Kontroler s názvem `ProductController`je obsažený v seznamu 1.

**Výpis 1 – `ProductController.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample1.vb)]

`ProductController` obsahuje dvě metody akcí s názvem `Index()` a `Details()`. Obě metody akcí vrací zobrazení. Všimněte si, že akce `Details()` přijímá parametr s názvem ID.

## <a name="testing-the-view-returned-by-a-controller"></a>Testování zobrazení vráceného řadičem

Představte si, že chceme testovat, zda `ProductController` vrátí pravé zobrazení. Chceme zajistit, aby při vyvolání `ProductController.Details()` akce se zobrazilo zobrazení podrobností. Třída testu v seznamu 2 obsahuje test jednotky pro testování zobrazení vráceného akcí `ProductController.Details()`.

**Výpis 2 – `ProductControllerTest.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample2.vb)]

Třída v seznamu 2 obsahuje testovací metodu s názvem `TestDetailsView()`. Tato metoda obsahuje tři řádky kódu. První řádek kódu vytvoří novou instanci třídy `ProductController`. Druhý řádek kódu vyvolá metodu `Details()` akce kontroleru. Nakonec poslední řádek kódu ověří, zda zobrazení vrácené akcí `Details()` je zobrazení podrobností.

Vlastnost `ViewResult.ViewName` představuje název zobrazení vráceného řadičem. Jedno velké upozornění na testování této vlastnosti. Existují dva způsoby, jak může kontroler vrátit zobrazení. Kontroler může explicitně vrátit zobrazení takto:

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample3.vb)]

Případně můžete název zobrazení odvodit z názvu akce řadiče, jako je tato:

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample4.vb)]

Tato akce kontroleru také vrátí zobrazení s názvem `Details`. Název zobrazení je ale odvozený od názvu akce. Chcete-li otestovat název zobrazení, je nutné explicitně vrátit název zobrazení z akce kontroleru.

Test jednotky můžete spustit v seznamu 2 zadáním kombinace kláves **CTRL-R,** nebo kliknutím na tlačítko **Spustit všechny testy v řešení** (viz obrázek 1). Pokud se test projde, zobrazí se okno Výsledky testů na obrázku 2.

[![spustit všechny testy v řešení](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image1.png)

**Obrázek 01**: spuštění všech testů v řešení ([kliknutím zobrazíte obrázek v plné velikosti](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image3.png))

[![úspěch!](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image4.png)

**Obrázek 02**: úspěch! ([Kliknutím zobrazíte obrázek v plné velikosti.](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image6.png))

## <a name="testing-the-view-data-returned-by-a-controller"></a>Testování zobrazení dat vrácených řadičem

Kontroler MVC předává data do zobrazení pomocí objektu s názvem *`View Data`* . Představte si například, že chcete zobrazit podrobnosti o konkrétním produktu při vyvolání akce `ProductController Details()`. V takovém případě můžete vytvořit instanci `Product` třídy (definované v modelu) a předat instanci do zobrazení `Details` tím, že využijete `View Data`.

Upravený `ProductController` v seznamu 3 obsahuje aktualizovanou `Details()` akci, která vrátí produkt.

**Výpis 3 – `ProductController.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample5.vb)]

Nejprve akce `Details()` vytvoří novou instanci třídy `Product`, která představuje přenosný počítač. Dále instance třídy `Product` je předána jako druhý parametr metodě `View()`.

Můžete napsat testy jednotek k otestování, zda jsou očekávaná data obsažena v zobrazení dat. Testování částí v seznamu 4 testuje, zda je při volání metody `ProductController Details()` akce vrácen produkt představující přenosný počítač.

**Výpis 4 – `ProductControllerTest.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample6.vb)]

V výpisu 4 `TestDetailsView()` metoda Testuje data zobrazení vrácená voláním metody `Details()`. `ViewData` je vystavena jako vlastnost `ViewResult` vrácená voláním metody `Details()`. Vlastnost `ViewData.Model` obsahuje produkt předaný do zobrazení. Test jednoduše ověří, že produkt obsažený v zobrazení dat má název přenosného počítače.

## <a name="testing-the-action-result-returned-by-a-controller"></a>Testování výsledku akce vráceného řadičem

Složitější akce kontroleru může vracet různé typy výsledků akce v závislosti na hodnotách parametrů předaných do akce kontroleru. Akce kontroleru může vracet různé typy výsledků akce včetně `ViewResult`, `RedirectToRouteResult`nebo `JsonResult`.

Například upravená akce `Details()` v seznamu 5 vrátí zobrazení `Details` při předání platného ID produktu do akce. Pokud předáte neplatné ID produktu – ID s hodnotou menší než 1 –, budete přesměrováni na `Index()` akci.

**Výpis 5 – `ProductController.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample7.vb)]

Chování `Details()` akce můžete otestovat pomocí testu jednotek v seznamu 6. Testování částí v seznamu 6 ověřuje, že jste přesměrováni do zobrazení `Index`, když je ID s hodnotou-1 předáno metodě `Details()`.

**Výpis 6 – `ProductControllerTest.vb`**

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample8.vb)]

Když zavoláte metodu `RedirectToAction()` v akci kontroleru, akce kontroleru vrátí `RedirectToRouteResult`. Test ověří, zda `RedirectToRouteResult` přesměruje uživatele na akci kontroleru s názvem `Index`.

## <a name="summary"></a>Přehled

V tomto kurzu jste zjistili, jak sestavit testy jednotek pro akce kontroleru MVC. Nejprve jste zjistili, jak ověřit, zda je vráceno správné zobrazení pomocí akce kontroleru. Zjistili jste, jak použít vlastnost `ViewResult.ViewName` k ověření názvu zobrazení.

Dále jsme zkoumali, jak můžete testovat obsah `View Data`. Zjistili jste, jak ověřit, zda byl po volání akce kontroleru vrácen správný produkt v `View Data`.

Nakonec jsme probrali, jak můžete testovat, zda jsou z akce kontroleru vráceny různé typy výsledků akce. Zjistili jste, jak otestovat, zda kontroler vrací `ViewResult` nebo `RedirectToRouteResult`.

> [!div class="step-by-step"]
> [Předchozí](creating-unit-tests-for-asp-net-mvc-applications-cs.md)

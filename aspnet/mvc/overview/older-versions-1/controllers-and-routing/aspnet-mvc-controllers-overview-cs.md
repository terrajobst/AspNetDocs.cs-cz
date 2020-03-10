---
uid: mvc/overview/older-versions-1/controllers-and-routing/aspnet-mvc-controllers-overview-cs
title: ASP.NET kontroler MVC –C#přehled () | Microsoft Docs
author: StephenWalther
description: V tomto kurzu vás Stephen Walther seznámí s řadiči pro ASP.NET MVC. Naučíte se vytvářet nové řadiče a vracet různé typy zdrojů akcí...
ms.author: riande
ms.date: 02/16/2008
ms.assetid: b985c49a-3668-455c-a366-f85f6bc64b12
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/aspnet-mvc-controllers-overview-cs
msc.type: authoredcontent
ms.openlocfilehash: 1a287b37742400a17c2ed53cfd00bfb053b4f3d2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544112"
---
# <a name="aspnet-mvc-controller-overview-c"></a>ASP.NET MVC – přehled kontrolerů (C#)

od [Stephen Walther](https://github.com/StephenWalther)

> V tomto kurzu vás Stephen Walther seznámí s řadiči pro ASP.NET MVC. Naučíte se vytvářet nové řadiče a vracet různé typy výsledků akcí.

V tomto kurzu se seznámíte s tématem řadičů ASP.NET MVC, akcemi kontrol a výsledků akcí. Po dokončení tohoto kurzu budete rozumět tomu, jak se řadiče používají k řízení způsobu, jakým návštěvník komunikuje s webem ASP.NET MVC.

## <a name="understanding-controllers"></a>Principy řadičů

Řadiče MVC zodpovídají za reakci na požadavky vytvořené na webu ASP.NET MVC. Každá žádost prohlížeče je namapovaná na konkrétní kontroler. Představte si například, že na adresní řádek v prohlížeči zadáte následující adresu URL:

`http://localhost/Product/Index/3`

V tomto případě je vyvolán kontroler s názvem ProductController. ProductController zodpovídá za generování odpovědi na požadavek prohlížeče. Kontroler může například vrátit konkrétní zobrazení zpět do prohlížeče nebo může správce přesměrovat uživatele na jiný kontroler.

Výpis 1 obsahuje jednoduchý řadič s názvem ProductController.

**Listing1 - Controllers\ProductController.cs**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample1.cs)]

Jak vidíte z výpisu 1, kontroler je pouze třída (Visual Basic .NET nebo C# třída). Kontrolér je třída, která je odvozena od třídy Base System. Web. Mvc. Controller. Vzhledem k tomu, že kontroler dědí z této základní třídy, kontroler zdědí několik užitečných metod (v průběhu chvilky probereme tyto metody).

## <a name="understanding-controller-actions"></a>Principy akcí kontroleru

Kontroler zveřejňuje akce kontroleru. Akce je metoda na řadiči, který se volá při zadání konkrétní adresy URL v adresním řádku prohlížeče. Představte si například, že vytvoříte požadavek na následující adresu URL:

`http://localhost/Product/Index/3`

V tomto případě je metoda index () volána na třídu ProductController. Metoda index () je příkladem akce kontroleru.

Akce kontroleru musí být veřejnou metodou třídy Controller. C#metody jsou ve výchozím nastavení soukromé metody. Mějte na paměti, že všechny veřejné metody, které přidáte do třídy Controller, se vystaví jako akce kontroleru automaticky (musíte být opatrní, protože akci kontroleru může vyvolat kdokoli v hlavním panelu jednoduše zadáním správné adresy URL do adresního řádku prohlížeče).

K dispozici jsou některé další požadavky, které musí splnit akce kontroleru. Metoda použitá jako akce kontroleru nemůže být přetížena. Kromě toho nemůže být akce kontroleru statickou metodou. Kromě toho můžete jako akci kontroleru použít jenom tuto metodu.

## <a name="understanding-action-results"></a>Porozumění výsledkům akcí

Akce kontroleru vrátí něco označovaného jako *výsledek akce*. Výsledkem akce je to, co se akce kontroleru vrátí v reakci na požadavek prohlížeče.

Rozhraní ASP.NET MVC podporuje několik typů výsledků akcí, včetně:

1. ViewResult – reprezentuje HTML a značky.
2. EmptyResult – nepředstavuje žádný výsledek.
3. RedirectResult – představuje přesměrování na novou adresu URL.
4. JsonResult – představuje výsledek JavaScript Object Notation, který lze použít v aplikaci AJAX.
5. JavaScriptResult – představuje skript JavaScriptu.
6. ContentResult – představuje výsledek textu.
7. FileContentResult – představuje soubor ke stažení (s binárním obsahem).
8. FilePathResult – představuje soubor ke stažení (s cestou).
9. FileStreamResult – představuje soubor ke stažení (s datovým proudem souboru).

Všechny tyto výsledky akce dědí ze základní třídy ActionResult.

Ve většině případů akce kontroleru vrátí ViewResult. Například akce řadiče indexu v seznamu 2 vrátí hodnotu ViewResult.

**Výpis 2 – Controllers\BookController.cs**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample2.cs)]

Když akce vrátí ViewResult, do prohlížeče se vrátí HTML. Metoda index () v seznamu 2 vrátí zobrazení s názvem index do prohlížeče.

Všimněte si, že akce index () v seznamu 2 nevrací ViewResult (). Místo toho je volána metoda View () základní třídy kontroleru. Za normálních okolností nevrátíte výsledek akce přímo. Místo toho zavoláte jednu z následujících metod základní třídy Controller:

1. Zobrazit – vrátí výsledek akce ViewResult.
2. Redirect – vrátí výsledek akce RedirectResult.
3. RedirectToAction – vrátí výsledek akce RedirectToRouteResult.
4. Metodu RedirectToRoute – vrátí výsledek akce RedirectToRouteResult.
5. JSON – vrátí výsledek akce JsonResult.
6. JavaScriptResult – vrátí JavaScriptResult.
7. Content – vrátí výsledek ContentResult akce.
8. File-vrátí FileContentResult, FilePathResult nebo FileStreamResult v závislosti na parametrech předaných metodě.

Takže pokud chcete vrátit zobrazení do prohlížeče, zavolejte metodu View (). Pokud chcete uživatele přesměrovat z jedné akce kontroleru na jiný, zavoláte metodu RedirectToAction (). Například akce podrobnosti () v seznamu 3 buď zobrazí zobrazení nebo přesměruje uživatele na akci index () v závislosti na tom, zda parametr ID má hodnotu.

**Výpis 3 – CustomerController.cs**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample3.cs)]

Výsledek akce ContentResult je zvláštní. Výsledek akce ContentResult můžete použít k vrácení výsledku akce jako prostý text. Například metoda index () v seznamu 4 vrátí zprávu jako prostý text a ne jako HTML.

**Výpis 4 – Controllers\StatusController.cs**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample4.cs)]

Při vyvolání akce StatusController. index () se zobrazení nevrátí. Místo toho je nezpracovaný text "Hello World!" se vrátí do prohlížeče.

Pokud akce kontroleru vrátí výsledek, který není výsledkem akce – například datum nebo celé číslo, pak je výsledek zabalen do ContentResult automaticky. Například při vyvolání akce index () WorkController v seznamu 5 se datum vrátí jako ContentResult automaticky.

**Výpis 5 – WorkController.cs**

[!code-csharp[Main](aspnet-mvc-controllers-overview-cs/samples/sample5.cs)]

Akce index () v výpisu 5 vrátí objekt DateTime. Rozhraní ASP.NET MVC převede objekt DateTime na řetězec a automaticky zabalí hodnotu DateTime do ContentResult. Prohlížeč obdrží jako prostý text Datum a čas.

## <a name="summary"></a>Souhrn

Účelem tohoto kurzu je předvést vás koncepty řadičů ASP.NET MVC, akcí kontrol a výsledků akcí kontroleru. V první části jste se dozvěděli, jak přidat nové řadiče do projektu ASP.NET MVC. V dalším kroku jste zjistili, jak se veřejné metody kontroleru zveřejňují jako akce kontroleru. Nakonec jsme probrali různé typy výsledků akcí, které je možné vrátit z akce kontroleru. Konkrétně jsme probrali, jak vrátit ViewResult, RedirectToActionResult a ContentResult z akce kontroleru.

> [!div class="step-by-step"]
> [Předchozí](creating-an-action-vb.md)
> [Další](creating-custom-routes-cs.md)

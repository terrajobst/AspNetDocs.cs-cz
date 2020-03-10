---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
title: Principy filtrů akcí (VB) | Microsoft Docs
author: microsoft
description: Cílem tohoto kurzu je vysvětlit filtry akcí. Filtr akcí je atribut, který můžete použít pro akci kontroleru, nebo pro celý kontroler...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: e83812f2-c53e-4a43-a7c1-d64c59ecf694
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-vb
msc.type: authoredcontent
ms.openlocfilehash: 263658231ccaa7863508c691a3570bc00b9e8039
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601169"
---
# <a name="understanding-action-filters-vb"></a>Principy filtrů akcí (VB)

od [Microsoftu](https://github.com/microsoft)

[Stáhnout PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_VB.pdf)

> Cílem tohoto kurzu je vysvětlit filtry akcí. Filtr akcí je atribut, který můžete použít pro akci kontroleru, nebo pro celý kontroler, který mění způsob, jakým se akce provádí.

## <a name="understanding-action-filters"></a>Porozumění filtrům akcí

Cílem tohoto kurzu je vysvětlit filtry akcí. Filtr akcí je atribut, který můžete použít pro akci kontroleru, nebo pro celý kontroler, který mění způsob, jakým se akce provádí. Rozhraní ASP.NET MVC obsahuje několik filtrů akcí:

- OutputCache – tento filtr akcí ukládá do mezipaměti výstup akce kontroleru po zadanou dobu.
- HandleError – tento filtr akcí zpracovává chyby vyvolané při spuštění akce kontroleru.
- Autorizovat – tento filtr akcí vám umožňuje omezit přístup k určitému uživateli nebo roli.

Můžete také vytvořit vlastní filtry akcí. Například můžete chtít vytvořit vlastní filtr akcí, abyste mohli implementovat vlastní ověřovací systém. Nebo můžete chtít vytvořit filtr akcí, který upraví zobrazení dat vrácených akcí kontroleru.

V tomto kurzu se naučíte, jak vytvořit filtr akcí od základu. Vytvoříme filtr akcí protokolu, který bude protokolovat různé fáze zpracování akce v okně výstupu sady Visual Studio.

### <a name="using-an-action-filter"></a>Použití filtru akcí

Filtr akcí je atribut. Většinu filtrů akcí můžete použít buď na akci samostatného kontroleru, nebo na celý kontroler.

Například řadič dat v seznamu 1 zpřístupňuje akci s názvem `Index()`, která vrací aktuální čas. Tato akce je upravena pomocí filtru akcí `OutputCache`. Tento filtr způsobí, že hodnota vrácená akcí bude ukládána do mezipaměti po dobu 10 sekund.

**Výpis 1 – `Controllers\DataController.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample1.vb)]

Pokud `Index()` akci opakovaně vyvoláte tak, že zadáte adresu URL/Data/Index do panelu Adresa v prohlížeči a několikrát kliknete na tlačítko Aktualizovat, bude se vám po dobu 10 sekund zobrazovat stejný čas. Výstup akce `Index()` je uložen do mezipaměti po dobu 10 sekund (viz obrázek 1).

[čas ![v mezipaměti](understanding-action-filters-vb/_static/image2.png)](understanding-action-filters-vb/_static/image1.png)

**Obrázek 01**: čas v mezipaměti ([kliknutím zobrazíte obrázek v plné velikosti](understanding-action-filters-vb/_static/image3.png))

V seznamu 1 se pro metodu `Index()` používá filtr akcí `OutputCache` –. Pokud potřebujete, můžete pro stejnou akci použít více filtrů akcí. Můžete například chtít, aby se pro stejnou akci mohla použít filtr akcí `OutputCache` i `HandleError`.

V seznamu 1 se pro akci `Index()` použije filtr akce `OutputCache`. Tento atribut můžete použít také pro třídu `DataController` samotné. V takovém případě by výsledek vrácený všemi akcemi vystavenými řadičem byl uložen do mezipaměti po dobu 10 sekund.

### <a name="the-different-types-of-filters"></a>Různé typy filtrů

Rozhraní ASP.NET MVC podporuje čtyři různé typy filtrů:

1. Autorizační filtry – implementuje atribut `IAuthorizationFilter`.
2. Filtry akcí – implementuje atribut `IActionFilter`.
3. Filtry výsledků – implementuje atribut `IResultFilter`.
4. Filtry výjimek – implementuje atribut `IExceptionFilter`.

Filtry se spouštějí v uvedeném pořadí. Například filtry autorizace jsou vždy spouštěny před filtry akcí a filtry výjimek jsou vždy provedeny po každém jiném typu filtru.

Filtry autorizace slouží k implementaci ověřování a autorizace pro akce kontroleru. Například filtr autorizace je příkladem autorizačního filtru.

Filtry akcí obsahují logiku, která se spustí před a po spuštění akce kontroleru. Filtr akcí můžete například použít k úpravě dat zobrazení, která akce kontroleru vrátí.

Filtry výsledků obsahují logiku, která se spustí před a po provedení výsledku zobrazení. Například můžete chtít upravit výsledek zobrazení přímo před tím, než se zobrazení vykreslí do prohlížeče.

Filtry výjimek jsou poslední typ filtru, který má být spuštěn. Filtr výjimek můžete použít ke zpracování chyb vyvolaných akcemi kontroleru nebo výsledky akce kontroleru. Filtry výjimek můžete použít také k protokolování chyb.

Každý jiný typ filtru se spustí v určitém pořadí. Pokud chcete řídit pořadí, ve kterém se spouštějí filtry stejného typu, můžete nastavit vlastnost Order objektu Filter.

Základní třídou pro všechny filtry akcí je třída `System.Web.Mvc.FilterAttribute`. Pokud chcete implementovat konkrétní typ filtru, je nutné vytvořit třídu, která dědí z třídy základního filtru a implementuje jedno nebo více rozhraní IAuthorizationFilter, IActionFilter, IResultFilter nebo ExceptionFilter.

### <a name="the-base-actionfilterattribute-class"></a>Základní třída ActionFilterAttribute

Aby bylo snazší implementovat vlastní filtr akcí, rozhraní ASP.NET MVC zahrnuje základní třídu `ActionFilterAttribute`. Tato třída implementuje rozhraní `IActionFilter` i `IResultFilter` a dědí z třídy `Filter`.

Tato terminologie není zcela konzistentní. Technicky, třída, která dědí z třídy ActionFilterAttribute, je filtr akcí a filtr výsledků. Ale ve volném smyslu se k odkazování na libovolný typ filtru v rozhraní ASP.NET MVC používá filtr akcí Wordu.

Základní třída ActionFilterAttribute má následující metody, které lze přepsat:

- OnActionExecuting – Tato metoda je volána před provedením akce kontroleru.
- OnActionExecuted – Tato metoda se volá po provedení akce kontroleru.
- OnResultExecuting – Tato metoda je volána před provedením výsledku akce kontroleru.
- OnResultExecuted – Tato metoda se volá poté, co se spustí výsledek akce kontroleru.

V další části uvidíte, jak můžete implementovat každou z těchto různých metod.

### <a name="creating-a-log-action-filter"></a>Vytvoření filtru akce protokolu

Pro ilustraci, jak můžete vytvořit vlastní filtr akcí, vytvoříme vlastní filtr akcí, který bude protokolovat fáze zpracování akce kontroleru v okně výstupu sady Visual Studio. Náš `LogActionFilter` je obsažený v seznamu 2.

**Výpis 2 – `ActionFilters\LogActionFilter.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample2.vb)]

V výpisu 2 jsou `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`a `OnResultExecuted()` metody všechny volat metodu `Log()`. Název metody a data aktuální trasy jsou předány metodě `Log()`. Metoda `Log()` zapisuje zprávu do okna výstupu sady Visual Studio (viz obrázek 2).

[![zápis do okna výstup aplikace Visual Studio](understanding-action-filters-vb/_static/image5.png)](understanding-action-filters-vb/_static/image4.png)

**Obrázek 02**: zápis do okna výstup aplikace Visual Studio ([kliknutím zobrazíte obrázek v plné velikosti](understanding-action-filters-vb/_static/image6.png))

Domovský kontroler v seznamu 3 ukazuje, jak můžete použít filtr akce protokolu na celou třídu kontroleru. Vždy, když jsou vyvolány jakékoli akce vystavené domovským řadičem – buď metoda `Index()`, nebo metoda `About()` – fáze zpracování akce jsou protokolovány do okna výstup sady Visual Studio.

**Výpis 3 – `Controllers\HomeController.vb`**

[!code-vb[Main](understanding-action-filters-vb/samples/sample3.vb)]

### <a name="summary"></a>Souhrn

V tomto kurzu jste se zavedli k ASP.NETm filtrům akcí MVC. Seznámili jste se se čtyřmi různými typy filtrů: filtry autorizace, filtry akcí, filtry výsledků a filtry výjimek. Zjistili jste také základní třídu `ActionFilterAttribute`.

Nakonec jste zjistili, jak implementovat jednoduchý filtr akcí. Vytvořili jsme filtr akcí protokolu, který zapisuje fáze zpracování akce kontroleru do okna výstup sady Visual Studio.

> [!div class="step-by-step"]
> [Předchozí](asp-net-mvc-routing-overview-vb.md)
> [Další](improving-performance-with-output-caching-vb.md)

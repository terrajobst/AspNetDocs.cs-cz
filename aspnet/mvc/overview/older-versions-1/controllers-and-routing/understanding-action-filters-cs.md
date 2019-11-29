---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: Principy filtrů akcí (C#) | Microsoft Docs
author: microsoft
description: Cílem tohoto kurzu je vysvětlit filtry akcí. Filtr akcí je atribut, který můžete použít pro akci kontroleru, nebo pro celý kontroler...
ms.author: riande
ms.date: 10/16/2008
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: d1c72c2355c6122f851351a8c1e8f04fa63ae04e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74590112"
---
# <a name="understanding-action-filters-c"></a>Principy filtrů akcí (C#)

od [Microsoftu](https://github.com/microsoft)

[Stáhnout PDF](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

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

**Výpis 1 – `Controllers\DataController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

Pokud `Index()` akci opakovaně vyvoláte tak, že zadáte adresu URL/Data/Index do panelu Adresa v prohlížeči a několikrát kliknete na tlačítko Aktualizovat, bude se vám po dobu 10 sekund zobrazovat stejný čas. Výstup akce `Index()` je uložen do mezipaměti po dobu 10 sekund (viz obrázek 1).

[čas ![v mezipaměti](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)

**Obrázek 01**: čas v mezipaměti ([kliknutím zobrazíte obrázek v plné velikosti](understanding-action-filters-cs/_static/image3.png))

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

Základní třídou pro všechny filtry akcí je třída `System.Web.Mvc.FilterAttribute`. Pokud chcete implementovat konkrétní typ filtru, je nutné vytvořit třídu, která dědí ze základní třídy filtru a implementuje jedno nebo více `IAuthorizationFilter`, `IActionFilter`, `IResultFilter`nebo `IExceptionFilter` rozhraní.

### <a name="the-base-actionfilterattribute-class"></a>Základní třída ActionFilterAttribute

Aby bylo snazší implementovat vlastní filtr akcí, rozhraní ASP.NET MVC zahrnuje základní třídu `ActionFilterAttribute`. Tato třída implementuje rozhraní `IActionFilter` i `IResultFilter` a dědí z třídy `Filter`.

Tato terminologie není zcela konzistentní. Technicky, třída, která dědí z třídy ActionFilterAttribute, je filtr akcí a filtr výsledků. Ale ve volném smyslu se k odkazování na libovolný typ filtru v rozhraní ASP.NET MVC používá filtr akcí Wordu.

Základní `ActionFilterAttribute` třída má následující metody, které lze přepsat:

- OnActionExecuting – Tato metoda je volána před provedením akce kontroleru.
- OnActionExecuted – Tato metoda se volá po provedení akce kontroleru.
- OnResultExecuting – Tato metoda je volána před provedením výsledku akce kontroleru.
- OnResultExecuted – Tato metoda se volá poté, co se spustí výsledek akce kontroleru.

V další části uvidíte, jak můžete implementovat každou z těchto různých metod.

### <a name="creating-a-log-action-filter"></a>Vytvoření filtru akce protokolu

Pro ilustraci, jak můžete vytvořit vlastní filtr akcí, vytvoříme vlastní filtr akcí, který bude protokolovat fáze zpracování akce kontroleru v okně výstupu sady Visual Studio. Náš `LogActionFilter` je obsažený v seznamu 2.

**Výpis 2 – `ActionFilters\LogActionFilter.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

V výpisu 2 jsou `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`a `OnResultExecuted()` metody všechny volat metodu `Log()`. Název metody a data aktuální trasy jsou předány metodě `Log()`. Metoda `Log()` zapisuje zprávu do okna výstupu sady Visual Studio (viz obrázek 2).

[![zápis do okna výstup aplikace Visual Studio](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)

**Obrázek 02**: zápis do okna výstup aplikace Visual Studio ([kliknutím zobrazíte obrázek v plné velikosti](understanding-action-filters-cs/_static/image6.png))

Domovský kontroler v seznamu 3 ukazuje, jak můžete použít filtr akce protokolu na celou třídu kontroleru. Vždy, když jsou vyvolány jakékoli akce vystavené domovským řadičem – buď metoda `Index()`, nebo metoda `About()` – fáze zpracování akce jsou protokolovány do okna výstup sady Visual Studio.

**Výpis 3 – `Controllers\HomeController.cs`**

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a>Přehled

V tomto kurzu jste se zavedli k ASP.NETm filtrům akcí MVC. Seznámili jste se se čtyřmi různými typy filtrů: filtry autorizace, filtry akcí, filtry výsledků a filtry výjimek. Zjistili jste také základní třídu `ActionFilterAttribute`.

Nakonec jste zjistili, jak implementovat jednoduchý filtr akcí. Vytvořili jsme filtr akcí protokolu, který zapisuje fáze zpracování akce kontroleru do okna výstup sady Visual Studio.

> [!div class="step-by-step"]
> [Předchozí](asp-net-mvc-routing-overview-cs.md)
> [Další](improving-performance-with-output-caching-cs.md)

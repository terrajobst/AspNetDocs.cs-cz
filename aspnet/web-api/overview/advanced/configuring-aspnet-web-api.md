---
uid: web-api/overview/advanced/configuring-aspnet-web-api
title: Konfigurace webového rozhraní API ASP.NET 2 – ASP.NET 4. x
author: MikeWasson
description: 'Konfigurace webového rozhraní API 2 pro ASP.NET 4. x: Konfigurace nastavení, hostování ASP.NET 4. x, OWIN pro samoobslužné hostování, globální služby a konfigurace předběžného kontroleru.'
ms.author: riande
ms.date: 03/31/2014
ms.custom: seoapril2019
ms.assetid: 9e10a700-8d91-4d2e-a31e-b8b569fe867c
msc.legacyurl: /web-api/overview/advanced/configuring-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 4f76728fa5e4602e35e1b7cb2d41b2245093cad8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557720"
---
# <a name="configuring-aspnet-web-api-2"></a>Konfigurace webového rozhraní API 2 pro ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

Toto téma popisuje, jak nakonfigurovat webové rozhraní API ASP.NET.

- [Nastavení konfigurace](#settings)
- [Konfigurace webového rozhraní API s hostováním ASP.NET](#webhost)
- [Konfigurace webového rozhraní API pomocí samoobslužného hostování OWIN](#selfhost)
- [Globální služby webového rozhraní API](#services)
- [Konfigurace pro jednotlivé řadiče](#percontrollerconfig)

<a id="settings"></a>
## <a name="configuration-settings"></a>Nastavení konfigurace

Nastavení konfigurace webového rozhraní API jsou definovaná ve třídě [HttpConfiguration](https://msdn.microsoft.com/library/system.web.http.httpconfiguration.aspx) .

| Člen | Popis |
| --- | --- |
| **DependencyResolver** | Povoluje vkládání závislostí pro řadiče. Viz [použití překladače závislostí webového rozhraní API](dependency-injection.md). |
| **Filtry** | Filtry akcí. |
| **Formátovací modul SEQ** | [Formátovací moduly typu média](../formats-and-model-binding/media-formatters.md). |
| **IncludeErrorDetailPolicy** | Určuje, zda má server obsahovat podrobnosti o chybě, například zprávy výjimek a trasování zásobníku, ve zprávách s odpovědí HTTP. Viz [IncludeErrorDetailPolicy](https://msdn.microsoft.com/library/system.web.http.includeerrordetailpolicy(v=vs.108)). |
| **Inicializátor** | Funkce, která provádí konečnou inicializaci rozhraní **HttpConfiguration**. |
| **MessageHandlers** | [Obslužné rutiny zpráv HTTP](http-message-handlers.md). |
| **ParameterBindingRules** | Kolekce pravidel pro parametry vazby u akcí kontroleru. |
| **Vlastnosti** | Obecný kontejner objektů A dat. |
| **Tras** | Kolekce tras. Podívejte [se na téma směrování ve webovém rozhraní API ASP.NET](../web-api-routing-and-actions/routing-in-aspnet-web-api.md). |
| **Služby** | Kolekce služeb. Viz [služby](#services). |

## <a name="prerequisites"></a>Předpoklady

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Komunita, edice Professional nebo Enterprise.

<a id="webhost"></a>
## <a name="configuring-web-api-with-aspnet-hosting"></a>Konfigurace webového rozhraní API s hostováním ASP.NET

V aplikaci ASP.NET nakonfigurujte webové rozhraní API voláním [GlobalConfiguration. Configure](https://msdn.microsoft.com/library/system.web.http.globalconfiguration.configure.aspx) v **aplikaci\_spustit** metodu. Metoda **Configure** přebírá delegáta s jedním parametrem typu **HttpConfiguration**. Proveďte veškerou konfiguraci v rámci delegáta.

Tady je příklad použití anonymního delegáta:

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample1.cs)]

V sadě Visual Studio 2017 šablona projektu "webová aplikace v ASP.NET" automaticky nastaví konfigurační kód, pokud v dialogovém okně **Nový projekt ASP.NET** vyberete možnost webové rozhraní API.

[![](configuring-aspnet-web-api/_static/image2.png)](configuring-aspnet-web-api/_static/image1.png)

Šablona projektu vytvoří ve složce App\_Start soubor s názvem WebApiConfig.cs. Tento soubor kódu definuje delegáta, kam byste měli umístit konfigurační kód webového rozhraní API.

![](configuring-aspnet-web-api/_static/image3.png)

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample2.cs?highlight=12)]

Šablona projektu také přidá kód, který volá delegáta z **aplikace\_Start**.

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample3.cs?highlight=5)]

<a id="selfhost"></a>
## <a name="configuring-web-api-with-owin-self-hosting"></a>Konfigurace webového rozhraní API pomocí samoobslužného hostování OWIN

Pokud provádíte samoobslužné hostování s OWIN, vytvořte novou instanci **HttpConfiguration** . Proveďte jakoukoli konfiguraci této instance a pak předejte instanci do metody rozšíření **Owin. UseWebApi** .

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample4.cs)]

Tento kurz [používá Owin k samoobslužnému hostování ASP.NET webového rozhraní API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md) ukazuje kompletní kroky.

<a id="services"></a>
## <a name="global-web-api-services"></a>Globální služby webového rozhraní API

Kolekce **HttpConfiguration. Services** obsahuje sadu globálních služeb, které webové rozhraní API používá k provádění různých úloh, jako je výběr kontroleru a vyjednávání obsahu.

> [!NOTE]
> Kolekce **služeb** není obecným mechanismem pro účely zjišťování a vkládání závislostí. Ukládá pouze typy služeb, které jsou známy rozhraní Web API Framework.

Kolekce **služeb** je inicializována s výchozí sadou služeb a můžete poskytnout vlastní implementace. Některé služby podporují víc instancí, zatímco jiné můžou mít jenom jednu instanci. (Můžete ale také poskytovat služby na úrovni kontroleru, viz [konfigurace pro jednotlivé řadiče](#percontrollerconfig).

Služby s jednou instancí

| Služba | Popis |
| --- | --- |
| **IActionValueBinder** | Získá vazbu pro parametr. |
| **IApiExplorer** | Získá popisy rozhraní API vystavených aplikací. Další informace najdete v tématu [Vytvoření stránky s nápovědu pro webové rozhraní API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md). |
| **IAssembliesResolver** | Načte seznam sestavení pro aplikaci. Viz [Směrování a výběr akcí](../web-api-routing-and-actions/routing-and-action-selection.md). |
| **IBodyModelValidator** | Ověří model, který je čten z textu žádosti pomocí formátovacího modulu typu média. |
| **IContentNegotiator** | Provede vyjednávání obsahu. |
| **IDocumentationProvider** | Poskytuje dokumentaci pro rozhraní API. Výchozí hodnota je **null**. Další informace najdete v tématu [Vytvoření stránky s nápovědu pro webové rozhraní API](../getting-started-with-aspnet-web-api/creating-api-help-pages.md). |
| **IHostBufferPolicySelector** | Určuje, zda má hostitel ukládat tělo entity zprávy HTTP. |
| **IHttpActionInvoker** | Vyvolá akci kontroleru. Viz [Směrování a výběr akcí](../web-api-routing-and-actions/routing-and-action-selection.md). |
| **IHttpActionSelector** | Vybere akci kontroleru. Viz [Směrování a výběr akcí](../web-api-routing-and-actions/routing-and-action-selection.md). |
| **IHttpControllerActivator** | Aktivuje kontroler. Viz [Směrování a výběr akcí](../web-api-routing-and-actions/routing-and-action-selection.md). |
| **IHttpControllerSelector** | Vybere kontroler. Viz [Směrování a výběr akcí](../web-api-routing-and-actions/routing-and-action-selection.md). |
| **IHttpControllerTypeResolver** | Poskytuje seznam typů kontroleru webového rozhraní API v aplikaci. Viz [Směrování a výběr akcí](../web-api-routing-and-actions/routing-and-action-selection.md). |
| **ITraceManager** | Inicializuje rozhraní trasování. Viz [trasování ve webovém rozhraní API ASP.NET](../testing-and-debugging/tracing-in-aspnet-web-api.md). |
| **ITraceWriter** | Poskytuje zapisovač trasování. Výchozím nastavením je zapisovač trasování "No-op". Viz [trasování ve webovém rozhraní API ASP.NET](../testing-and-debugging/tracing-in-aspnet-web-api.md). |
| **IModelValidatorCache** | Poskytuje mezipaměť validátorů modelů. |

Služby s více instancemi

|                 Služba                 |                                                                                                              Popis                                                                                                               |
|-----------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|    <strong>IFilterProvider</strong>     |                                                                                           Vrátí seznam filtrů pro akci kontroleru.                                                                                           |
|  <strong>ModelBinderProvider</strong>   |                                                                                                Vrátí pořadač modelu pro daný typ.                                                                                                |
| <strong>ModelMetadataProvider</strong>  |                                                                                                     Poskytuje metadata pro model.                                                                                                     |
| <strong>ModelValidatorProvider</strong> |                                                                                                   Poskytuje validátor pro model.                                                                                                    |
|  <strong>ValueProviderFactory</strong>  | Vytvoří zprostředkovatele hodnoty. Další informace najdete v příspěvku na blogu Mike Stallion, [jak vytvořit vlastního zprostředkovatele hodnoty v WebApi](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx) . |

Chcete-li přidat vlastní implementaci do služby s více instancemi, zavolejte do kolekce **Services** příkaz **Add** nebo **INSERT** :

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample5.cs)]

Chcete-li nahradit službu s jednou instancí vlastní implementací, zavolejte **nahradit** v kolekci **služeb** :

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample6.cs)]

<a id="percontrollerconfig"></a>
## <a name="per-controller-configuration"></a>Konfigurace pro jednotlivé řadiče

Pro jednotlivé řadiče můžete přepsat následující nastavení:

- Formátování mediálního typu
- Pravidla vazeb parametrů
- Služby

Uděláte to tak, že definujete vlastní atribut, který implementuje rozhraní **IControllerConfiguration** . Pak použijte atribut pro kontroler.

Následující příklad nahrazuje výchozí formátovací modul typu média vlastním formátovacím modulem.

[!code-csharp[Main](configuring-aspnet-web-api/samples/sample7.cs)]

Metoda **IControllerConfiguration. Initialize** používá dva parametry:

- Objekt **HttpControllerSettings**
- Objekt **HttpControllerDescriptor**

**HttpControllerDescriptor** obsahuje popis kontroleru, který můžete kontrolovat pro informativní účely (například pro rozlišení mezi dvěma řadiči).

Ke konfiguraci kontroleru použijte objekt **HttpControllerSettings** . Tento objekt obsahuje podmnožinu konfiguračních parametrů, které lze přepsat podle jednotlivých řadičů. Všechna nastavení, která nemění výchozí hodnotu pro globální objekt **HttpConfiguration** .

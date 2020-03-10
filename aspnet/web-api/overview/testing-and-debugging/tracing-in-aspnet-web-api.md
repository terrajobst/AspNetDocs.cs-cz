---
uid: web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
title: Trasování ve webovém rozhraní API 2 pro ASP.NET | Microsoft Docs
author: MikeWasson
description: Ukazuje, jak povolit trasování v ASP.NET webovém rozhraní API.
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 66a837e9-600b-4b72-97a9-19804231c64a
msc.legacyurl: /web-api/overview/testing-and-debugging/tracing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: a01acb649556d06ab9828ceab0fcbdf363bbc0d1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598551"
---
# <a name="tracing-in-aspnet-web-api-2"></a>Trasování ve webovém rozhraní API 2 ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

> Při pokusu o ladění webové aplikace nenahrazujete správnou sadu protokolů trasování. V tomto kurzu se dozvíte, jak povolit trasování v ASP.NET webovém rozhraní API. Pomocí této funkce můžete sledovat, co rozhraní Web API funguje před a poté, co vyvolá kontroler. Můžete ho také použít k trasování vlastního kódu.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
>
> - [Visual studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) (také funguje se sadou visual Studio 2015)
> - Webové rozhraní API 2
> - [Microsoft. AspNet. WebApi. Tracing](http://www.nuget.org/packages/Microsoft.AspNet.WebApi.Tracing)

## <a name="enable-systemdiagnostics-tracing-in-web-api"></a>Povolit trasování System. Diagnostics ve webovém rozhraní API

Nejprve vytvoříme nový projekt webové aplikace ASP.NET. V aplikaci Visual Studio v nabídce **soubor** vyberte **Nový** > **projekt**. V části **šablony**, **Web**vyberte **ASP.NET webová aplikace**.

[![](tracing-in-aspnet-web-api/_static/image2.png)](tracing-in-aspnet-web-api/_static/image1.png)

Vyberte šablonu projektu webového rozhraní API.

[![](tracing-in-aspnet-web-api/_static/image4.png)](tracing-in-aspnet-web-api/_static/image3.png)

V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak **balíček spravovat konzolu**.

V okně konzoly Správce balíčků zadejte následující příkazy.

[!code-console[Main](tracing-in-aspnet-web-api/samples/sample1.cmd)]

První příkaz nainstaluje nejnovější balíček trasování webového rozhraní API. Také aktualizuje základní balíčky webového rozhraní API. Druhý příkaz aktualizuje balíček WebApi. webhost na nejnovější verzi.

> [!NOTE]
> Pokud chcete cílit na konkrétní verzi webového rozhraní API, použijte příznak-Version při instalaci balíčku trasování.

Otevřete soubor WebApiConfig.cs ve složce App\_Start. Do metody **Register** přidejte následující kód.

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample2.cs?highlight=6)]

Tento kód přidá do kanálu webového rozhraní API třídu [SystemDiagnosticsTraceWriter](https://msdn.microsoft.com/library/system.web.http.tracing.systemdiagnosticstracewriter.aspx) . Třída **SystemDiagnosticsTraceWriter** zapisuje trasování do [System. Diagnostics. Trace](https://msdn.microsoft.com/library/system.diagnostics.trace).

Chcete-li zobrazit trasování, spusťte aplikaci v ladicím programu. V prohlížeči přejděte na adresu `/api/values`.

![](tracing-in-aspnet-web-api/_static/image5.png)

Příkazy trasování jsou zapsány do okna výstup v aplikaci Visual Studio. (V nabídce **zobrazení** vyberte **výstup**).

[![](tracing-in-aspnet-web-api/_static/image7.png)](tracing-in-aspnet-web-api/_static/image6.png)

Vzhledem k tomu, že **SystemDiagnosticsTraceWriter** zapisuje trasování do **System. Diagnostics. Trace**, můžete registrovat další naslouchací procesy trasování; například pro zápis trasování do souboru protokolu. Další informace o zapisovačích trasování naleznete v tématu [naslouchací procesy trasování](https://msdn.microsoft.com/library/4y5y10s7.aspx) na webu MSDN.

### <a name="configuring-systemdiagnosticstracewriter"></a>Konfigurace SystemDiagnosticsTraceWriter

Následující kód ukazuje, jak nakonfigurovat zapisovač trasování.

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample3.cs)]

Můžete řídit dvě nastavení:

- Verbose: Pokud má hodnotu false, každé trasování obsahuje minimální informace. Je-li nastavena hodnota true, trasování obsahují více informací.
- MinimumLevel: nastaví minimální úroveň trasování. Úrovně trasování jsou v pořadí ladění, informace, varování, chyba a závažná.

## <a name="adding-traces-to-your-web-api-application"></a>Přidání trasování do aplikace webového rozhraní API

Přidáním zapisovače trasování získáte okamžitý přístup k trasování vytvořeným kanálem webového rozhraní API. Můžete také použít zapisovač trasování k trasování vlastního kódu:

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample4.cs)]

Chcete-li získat zapisovač trasování, zavolejte **HttpConfiguration. Services. GetTraceWriter**. Z kontroleru je tato metoda přístupná prostřednictvím vlastnosti **ApiController. Configuration** .

Chcete-li napsat trasování, můžete zavolat metodu **ITraceWriter. Trace** přímo, ale třída [ITraceWriterExtensions](https://msdn.microsoft.com/library/system.web.http.tracing.itracewriterextensions.aspx) definuje některé rozšiřující metody, které jsou výstižnější. Například metoda **info** zobrazená výše vytvoří trasování s **informacemi**úrovně trasování.

## <a name="web-api-tracing-infrastructure"></a>Infrastruktura trasování webového rozhraní API

Tato část popisuje, jak napsat vlastní zapisovač trasování pro webové rozhraní API.

Balíček Microsoft. AspNet. WebApi. Tracing je postaven na obecnější trasovací infrastruktuře ve webovém rozhraní API. Místo použití Microsoft. AspNet. WebApi. Tracing můžete také připojit jiné knihovny trasování nebo protokolování, jako je například [nLOG](http://nlog-project.org/) nebo [log4net](http://logging.apache.org/log4net/).

Chcete-li shromažďovat trasování, implementujte rozhraní **ITraceWriter** . Tady je jednoduchý příklad:

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample5.cs)]

Metoda **ITraceWriter. Trace** vytvoří trasování. Volající určuje kategorii a úroveň trasování. Kategorie může být libovolný uživatelsky definovaný řetězec. Vaše implementace **trasování** by měla provádět následující akce:

1. Vytvořte nový **TraceRecord**. Inicializujte ji pomocí úrovně žádosti, kategorie a trasování, jak je znázorněno na obrázku. Tyto hodnoty poskytuje volající.
2. Vyvolat delegáta *traceAction* Uvnitř tohoto delegáta se očekává, že volající vyplní zbytek **TraceRecord**.
3. Napište **TraceRecord**pomocí jakékoli metody protokolování, kterou chcete. Zde uvedený příklad jednoduše volá do **System. Diagnostics. Trace**.

## <a name="setting-the-trace-writer"></a>Nastavení zapisovače trasování

Chcete-li povolit trasování, je nutné nakonfigurovat webové rozhraní API tak, aby používalo implementaci **ITraceWriter** . Provedete to pomocí objektu **HttpConfiguration** , jak je znázorněno v následujícím kódu:

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample6.cs)]

Aktivní může být pouze jeden zapisovač trasování. Ve výchozím nastavení webové rozhraní API nastaví &quot;trasování no-op&quot;, které nedělá nic. (&quot;trasování no-op&quot; existuje, aby trasovací kód nemusel před zápisem trasování kontrolovat, zda má zapisovač trasování **hodnotu null** .)

## <a name="how-web-api-tracing-works"></a>Jak funguje trasování webového rozhraní API

Trasování ve webovém rozhraní API používá vzor *fasády* : Pokud je povoleno trasování, webové rozhraní API zalomí různé části kanálu požadavků se třídami, které provádějí volání trasování.

Když například vyberete kontroler, kanál používá rozhraní **IHttpControllerSelector** . Pokud je povoleno trasování, kanál vloží třídu, která implementuje **IHttpControllerSelector** , ale volá do reálné implementace:

![Trasování webového rozhraní API používá vzorek fasády.](tracing-in-aspnet-web-api/_static/image8.png)

Mezi výhody tohoto návrhu patří:

- Pokud nepřidáte zapisovač trasování, nebudou vytvořeny instance trasování a nebude mít žádný vliv na výkon.
- Pokud nahradíte výchozí služby, jako je například **IHttpControllerSelector** , vlastní implementací, trasování není ovlivněno, protože trasování je provedeno pomocí objektu obálky.

Můžete také nahradit celé rozhraní trasování API pro web pomocí vlastního rozhraní, a to nahrazením výchozí služby **ITraceManager** :

[!code-csharp[Main](tracing-in-aspnet-web-api/samples/sample7.cs)]

Implementujte **ITraceManager. Initialize** pro inicializaci vašeho sledovacího systému. Uvědomte si, že to nahrazuje *celé* rozhraní trasování, včetně veškerého trasovacího kódu, který je součástí webového rozhraní API.

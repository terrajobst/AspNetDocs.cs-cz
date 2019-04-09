---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Použití sady Katana | Dokumentace Microsoftu
author: microsoft
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 1238f7d09492a6856d49dece5de75184ccfa4838
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59379066"
---
# <a name="katana-samples"></a>Příklady použití sady Katana

by [Microsoft](https://github.com/microsoft)

## <a name="katana-samples"></a>Příklady použití sady Katana

**ASP.NET směruje ukázka** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)  
V některých aplikacích budete chtít připojení komponenty OWIN v tabulce směrování Asp.Net vedle komponenty bez OWIN. Tento příklad ukazuje, jak použít rozšiřující metody RouteCollection MapOwinPath a MapOwinRoute poskytované Microsoft.Owin.Host.SystemWeb.

**Větvení ukázkové kanály** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)  
Není potřeba mít lineární kanály zpracování žádostí OWIN, je možné větvit ke zpracování požadavků různými způsoby. Tento příklad ukazuje, jak vytvořit větvení profilace na základě cesty k požadavkům nebo jiné žádosti o data, jako jsou hlavičky. Tyto součásti jsou k dispozici v balíčku nuget Microsoft.Owin.Mapping.

**Ukázka vlastních serverových** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer)   
Ukazuje, jak použít vlastní server OWIN při vlastním hostování OWIN.

**Vložit ukázková** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)  
Některé servery OWIN lze spustit ve vašem vlastním procesu (&quot;v místním prostředí&quot;). Tato ukázka předvádí, jak můžete začít pomocí nástroje poskytované subsystémem balíček nuget Microsoft.Owin.Hosting aplikace OWIN.

**Ukázka Hello World** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)  
OWIN je HTTP server abstrakce rozhraní API, která umožňuje přenositelnost aplikací napříč různými servery. Tato ukázka předvádí, jak psát aplikace Hello World pomocí několika **jednoduché obálky** kolem nezpracovaná abstrakce OWIN a spusťte ho na webovém serveru, jako je ASP.NET.

**Ukázka programu Hello World nezpracovaná OWIN** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)  
Tato ukázka předvádí, jak psát aplikace Hello World pomocí **nezpracovaná** abstrakce OWIN a spusťte ho na webovém serveru, jako je Asp.Net.

**Ukázka SignalR** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)  
Ukazuje, jak hostování na vlastním serveru SignalR používá OWIN a Katana. Další informace o samoobslužné hostování funkci SignalR naleznete v tématu [kurzu: SignalR v místním](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

**Statické soubory ukázka** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample)   
Ukazuje, jak pro podporu požadavků HTTP pro statické soubory, které používá OWIN a Katana.

**Webové rozhraní API** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi)   
Tento příklad ukazuje, jak k hostování OWIN ve službě IIS a webového rozhraní API přidat do kanálu OWIN.

**Webových soketů ukázka** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample)   
Ukazuje, jak pomocí podporují webové sokety OWIN [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) třídy.

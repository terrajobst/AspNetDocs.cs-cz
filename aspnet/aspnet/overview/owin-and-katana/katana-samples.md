---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Ukázky Katana | Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 1238f7d09492a6856d49dece5de75184ccfa4838
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584558"
---
# <a name="katana-samples"></a>Příklady použití sady Katana

od [Microsoftu](https://github.com/microsoft)

## <a name="katana-samples"></a>Příklady použití sady Katana

**ASP.NET Routes Sample** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)  
V některých aplikacích budete chtít zapojit součásti OWIN do tabulky směrování Asp.Net vedle sebe pomocí jiných než OWIN komponent. V této ukázce se dozvíte, jak používat metody rozšíření RouteCollection MapOwinPath a MapOwinRoute, které poskytuje Microsoft. Owin. Host. SystemWeb.

**Ukázka zřetězení kanálů** | [zdrojového kódu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)  
Kanály zpracování požadavků OWIN nemusí být lineární, můžou být větví na zpracování požadavků různými způsoby. V této ukázce se dozvíte, jak vytvořit větvení kanál na základě cest požadavků nebo jiných dat požadavků, jako jsou hlavičky. Tyto součásti jsou k dispozici v balíčku NuGet Microsoft. Owin. Mapping.

Ukázka [zdrojového kódu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) | **vlastního serveru**   
Ukazuje, jak používat vlastní server OWIN při vlastním hostování OWIN.

**Vložený vzorový ukázkový** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)  
Některé servery OWIN lze spustit v rámci vlastního procesu (&quot;&quot;v místním prostředí). V této ukázce se dozvíte, jak spustit aplikaci OWIN pomocí nástrojů poskytovaných balíčkem NuGet Microsoft. Owin. Hosting.

**Ukázka HelloWorld** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)  
OWIN je abstrakce rozhraní API HTTP serveru, která umožňuje přenositelnost aplikace napříč různými servery. Tato ukázka předvádí, jak psát Hello World aplikace pomocí některých **jednoduchých obálek** kolem nezpracovaného Owin abstrakce a jak ji spustit na webovém serveru, jako je ASP.NET.

Ukázkový [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin) **Hello World Owin RAW** |   
Tato ukázka předvádí, jak napsat aplikaci Hello World s využitím **nezpracovaného** abstrakce Owin a jak ji spustit na webovém serveru, jako je ASP.NET.

**Ukázka signalizace** | [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)  
Ukazuje, jak používat k samoobslužnému hostování signál pomocí OWIN/Katana. Další informace o signálu pro samoobslužné hostování najdete v tématu [kurz: samoobslužný hostitel signálu](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).

Ukázka  [zdrojového kódu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) | **statických souborů**  
Ukazuje, jak podporovat požadavky HTTP pro statické soubory pomocí OWIN/Katana.

 | [zdrojového kódu](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) **webového rozhraní API**   
V této ukázce se dozvíte, jak hostovat OWIN ve službě IIS a přidat webové rozhraní API do kanálu OWIN.

Ukázkový [zdrojový kód](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) | **webového soketu**   
Ukazuje, jak podporovat webové sokety v OWIN pomocí třídy [System .NET. WebSockets.](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) WebSocket.

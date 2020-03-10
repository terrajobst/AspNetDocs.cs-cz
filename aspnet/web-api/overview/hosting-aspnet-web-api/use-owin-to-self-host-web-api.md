---
uid: web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
title: Použití OWIN k samoobslužnému hostování ASP.NET webového rozhraní API – ASP.NET 4. x
author: rick-anderson
description: Kurz s kódem ukazujícím, jak hostovat webové rozhraní API ASP.NET v konzolové aplikaci.
ms.author: riande
ms.date: 07/09/2013
ms.custom: seoapril2019
ms.assetid: a90a04ce-9d07-43ad-8250-8a92fb2bd3d5
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api
msc.type: authoredcontent
ms.openlocfilehash: 872b931391a63ef82b96e5b264c070c0b5e9605d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556537"
---
# <a name="use-owin-to-self-host-aspnet-web-api"></a>Použití OWIN k samoobslužnému hostování ASP.NET webového rozhraní API 

> V tomto kurzu se dozvíte, jak hostovat webové rozhraní API v ASP.NET v konzolové aplikaci pomocí OWIN pro samoobslužné hostování rozhraní Web API.
>
> [Open Web Interface for .NET](http://owin.org) (Owin) definuje abstrakci mezi webovými servery .NET a webovými aplikacemi. OWIN odpojí webovou aplikaci od serveru, což OWIN je ideální pro samoobslužné hostování webové aplikace ve vlastním procesu mimo službu IIS.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) 
> - Webové rozhraní API 5.2.7

> [!NOTE]
> Úplný zdrojový kód pro tento kurz najdete na adrese [GitHub.com/ASPNET/Samples](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/OwinSelfhostSample).

## <a name="create-a-console-application"></a>Vytvoření konzolové aplikace

V nabídce **soubor** klikněte na příkaz **Nový**a vyberte možnost **projekt**. Z **instalace**vyberte v **části C#vizuál** možnost **Windows Desktop** a pak vyberte **Konzolová aplikace (.NET Framework)** . Pojmenujte projekt "OwinSelfhostSample" a vyberte **OK**.

[![](use-owin-to-self-host-web-api/_static/image7.png)](use-owin-to-self-host-web-api/_static/image7.png)

## <a name="add-the-web-api-and-owin-packages"></a>Přidat webové rozhraní API a balíčky OWIN

V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**. V okně konzoly Správce balíčků zadejte následující příkaz:

`Install-Package Microsoft.AspNet.WebApi.OwinSelfHost`

Tím se nainstaluje balíček SelfHost OWIN pro WebAPI a všechny požadované balíčky OWIN.

[![](use-owin-to-self-host-web-api/_static/image4.png)](use-owin-to-self-host-web-api/_static/image3.png)

## <a name="configure-web-api-for-self-host"></a>Konfigurace webového rozhraní API pro samoobslužné hostování

V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a výběrem **přidat** / **třídu** přidejte novou třídu. Pojmenujte `Startup`třídy.

![](use-owin-to-self-host-web-api/_static/image5.png)

Celý často používaný kód nahraďte tímto souborem:

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample1.cs)]

## <a name="add-a-web-api-controller"></a>Přidat kontroler webového rozhraní API

Dále přidejte třídu kontroleru webového rozhraní API. V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a výběrem **přidat** / **třídu** přidejte novou třídu. Pojmenujte `ValuesController`třídy.

Celý často používaný kód nahraďte tímto souborem:

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample2.cs)]

## <a name="start-the-owin-host-and-make-a-request-with-httpclient"></a>Spuštění hostitele OWIN a vytvoření žádosti pomocí HttpClient

Nahraďte celý často používaný kód v souboru Program.cs následujícím způsobem:

[!code-csharp[Main](use-owin-to-self-host-web-api/samples/sample3.cs)]

## <a name="run-the-application"></a>Spuštění aplikace

Chcete-li spustit aplikaci, stiskněte klávesu F5 v aplikaci Visual Studio. Výstup by měl vypadat nějak takto:

[!code-console[Main](use-owin-to-self-host-web-api/samples/sample4.cmd)]

![](use-owin-to-self-host-web-api/_static/image6.png)

## <a name="additional-resources"></a>Další zdroje

[Přehled projektu Katana](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)

[Hostování webového rozhraní API v ASP.NET v roli pracovního procesu Azure](host-aspnet-web-api-in-an-azure-worker-role.md)

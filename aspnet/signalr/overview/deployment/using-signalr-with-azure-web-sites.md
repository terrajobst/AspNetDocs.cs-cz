---
uid: signalr/overview/deployment/using-signalr-with-azure-web-sites
title: Použití signalizace s Web Apps v Azure App Service | Microsoft Docs
author: bradygaster
description: Tento dokument popisuje, jak nakonfigurovat aplikaci signalizace, která běží na Microsoft Azure. Verze softwaru používané v tomto kurzu Visual Studio 2013 nebo VIS...
ms.author: bradyg
ms.date: 07/01/2015
ms.assetid: 2a7517a0-b88c-4162-ade3-9bf6ca7062fd
msc.legacyurl: /signalr/overview/deployment/using-signalr-with-azure-web-sites
msc.type: authoredcontent
ms.openlocfilehash: 0e6a18bdbe9cc47e89b5a458753845afb53595f1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558700"
---
# <a name="using-signalr-with-web-apps-in-azure-app-service"></a>Použití aplikace SignalR s webovými aplikacemi ve službě Azure App Service

Po [Fletcheru](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> Tento dokument popisuje, jak nakonfigurovat aplikaci signalizace, která běží na Microsoft Azure.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013) nebo Visual Studio 2012
> - .NET 4.5
> - Signal – verze 2
> - Sada Azure SDK 2,3 pro Visual Studio 2013 nebo 2012
>
>
>
> ## <a name="questions-and-comments"></a>Dotazy a komentáře
>
> Přečtěte si prosím svůj názor na to, jak se vám tento kurz líbí a co bychom mohli vylepšit v komentářích v dolní části stránky. Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat na [fórum ASP.NET signálu](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR), [StackOverflow.com](http://stackoverflow.com/)nebo [fóra pro Microsoft Azure](https://social.msdn.microsoft.com/Forums/windowsazure/home?category=windowsazureplatform).

## <a name="table-of-contents"></a>Obsah

- [Úvod](#introduction)
- [Nasazení webové aplikace Signaler k Azure App Service](#deploying)
- [Povolování WebSockets na Azure App Service](#websocket)
- [Použití Azure Redis Cacheho plánu](#backplane)
- [Další kroky](#nextsteps)

<a id="introduction"></a>
## <a name="introduction"></a>Úvod

Signál ASP.NET lze použít k zajištění nové úrovně interaktivity mezi servery a webovými klienty rozhraní .NET. Při hostování v Azure můžou aplikace služby Signal využít vysoce dostupné, škálovatelné a výkonné prostředí běžící v cloudu.

<a id="deploying"></a>
## <a name="deploying-a-signalr-web-app-to-azure-app-service"></a>Nasazení webové aplikace Signaler k Azure App Service

Návěstí nepřidává žádné konkrétní komplikace k nasazení aplikace do Azure a nasazování na místní server. Aplikace, která používá signalizaci, může být hostována v Azure bez jakýchkoli změn v konfiguraci a dalších nastaveních (i když podpora soketů WebSockets najdete v tématu [Povolení WebSockets na Azure App Service](#websocket) níže). V tomto kurzu nasadíte aplikaci vytvořenou v [Začínáme kurzu](../getting-started/tutorial-getting-started-with-signalr.md) do Azure.

**Požadavky**

- Visual Studio 2013. Pokud nemáte sadu Visual Studio, Visual Studio 2013 Express for Web je zahrnutý v instalaci sady Azure SDK.
- [Sada Azure sdk 2,3 pro Visual Studio 2013](https://go.microsoft.com/fwlink/?linkid=324322&clcid=0x409) nebo [Azure SDK 2,3 pro Visual Studio 2012](https://go.microsoft.com/fwlink/p/?linkid=323511).
- K dokončení tohoto kurzu budete potřebovat předplatné Azure. Můžete [si aktivovat výhody pro předplatitele MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)nebo si [zaregistrovat zkušební předplatné](https://azure.microsoft.com/pricing/free-trial/).

### <a name="deploying-a-signalr-web-app-to-azure"></a>Nasazení webové aplikace Signaler do Azure

1. Dokončete [kurz Začínáme](../getting-started/tutorial-getting-started-with-signalr.md)nebo si stáhněte dokončený projekt z [Galerie kódu](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9).
2. V aplikaci Visual Studio vyberte **sestavení**, **publikovat signál chat**.
3. V dialogovém okně Publikovat web vyberte web Windows Azure weby.

    ![Vybrat weby Azure](using-signalr-with-azure-web-sites/_static/image1.png)
4. Pokud nejste přihlášení k vašemu účet Microsoft, klikněte na **Přihlásit se...** v dialogovém okně vybrat existující web a přihlaste se.

    ![Vybrat existující web](using-signalr-with-azure-web-sites/_static/image2.png)    ![Přihlášení k Azure](using-signalr-with-azure-web-sites/_static/image3.png)
5. V dialogovém okně vybrat existující web klikněte na **Nový**.

    ![Nový web](using-signalr-with-azure-web-sites/_static/image4.png)
6. V dialogovém okně vytvořit web v systému Windows Azure zadejte jedinečný název aplikace. V rozevíracím seznamu oblast vyberte oblast, která je nejblíže. Klikněte na možnost **Vytvořit**.

    ![Vytvoření webu v Azure](using-signalr-with-azure-web-sites/_static/image5.png)
7. V dialogovém okně Publikovat web klikněte na **publikovat**.

    ![Publikování webu](using-signalr-with-azure-web-sites/_static/image6.png)
8. Jakmile se aplikace dokončí, otevře se v prohlížeči aplikace chatu signálu, která je hostovaná v Azure App Service Web Apps.

    ![Otevření webu v prohlížeči](using-signalr-with-azure-web-sites/_static/image7.png)

<a id="websocket"></a>
### <a name="enabling-websockets-on-azure-app-service-web-apps"></a>Povolování WebSockets na Azure App Service Web Apps

V aplikaci signalizace je nutné explicitně povolit objekty WebSockets, aby je bylo možné použít v aplikaci signalizace. v opačném případě budou použity jiné protokoly (podrobnosti viz [přenosové a záložní](../getting-started/introduction-to-signalr.md#transports) verze).

Aby bylo možné použít objekty WebSocket v Azure App Service Web Apps, povolte ji v konfiguračním oddílu webové aplikace. Uděláte to tak, že otevřete webovou aplikaci ve [službě Azure portál pro správu](https://manage.windowsazure.com/)a pak vyberete konfigurovat.

![Karta Konfigurace](using-signalr-with-azure-web-sites/_static/image8.png)

V horní části stránky konfigurace ověřte, že se pro vaši webovou aplikaci používá .NET 4,5.

![Nastavení rozhraní .NET Framework verze 4,5](using-signalr-with-azure-web-sites/_static/image9.png)

Na stránce konfigurace v nastavení **WebSockets** vyberte **zapnuto**.

![Nastavení WebSockets: zapnuto](using-signalr-with-azure-web-sites/_static/image10.png)

V dolní části stránky konfigurace vyberte **Uložit** a uložte provedené změny.

![Uložit nastavení](using-signalr-with-azure-web-sites/_static/image11.png)

<a id="backplane"></a>
## <a name="using-the-azure-redis-cache-backplane"></a>Použití Azure Redis Cacheho plánu

Pokud pro svou webovou aplikaci použijete více instancí a uživatelé těchto instancí musí vzájemně komunikovat (takže například zprávy chatu vytvořené v jedné instanci mohou kontaktovat uživatele připojené k jiným instancím), musí být v aplikaci implementováno [Azure Redis Cache pro replánování](../performance/scaleout-with-redis.md) .

<a id="nextsteps"></a>
## <a name="next-steps"></a>Další kroky

Další informace o Web Apps v Azure App Service najdete v tématu [přehled Web Apps](https://azure.microsoft.com/documentation/articles/app-service-web-overview/).

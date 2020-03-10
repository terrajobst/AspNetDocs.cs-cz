---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: Hostování ASP.NET webového rozhraní API 2 v roli pracovního procesu Azure – ASP.NET 4. x
author: MikeWasson
description: 'Kurz: hostování webového rozhraní API ASP.NET v roli pracovního procesu Azure pomocí OWIN k samoobslužnému hostování rozhraní Web API Framework.'
ms.author: riande
ms.date: 04/02/2014
ms.custom: seoapril2019
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: ec9904e0bff090be0f504036ae73977cfca0cb31
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556628"
---
# <a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a>Hostování ASP.NET webového rozhraní API 2 v roli pracovního procesu Azure

o [Jan Wasson](https://github.com/MikeWasson)

> V tomto kurzu se dozvíte, jak hostovat webové rozhraní API ASP.NET v roli pracovního procesu Azure pomocí OWIN k samoobslužnému hostování rozhraní Web API.
>
> [Open Web Interface for .NET](http://owin.org/) (Owin) definuje abstrakci mezi webovými servery .NET a webovými aplikacemi. OWIN odpojí webovou aplikaci od serveru, což OWIN je ideální pro samoobslužné hostování webové aplikace ve vlastním procesu mimo službu IIS – například v rámci role pracovního procesu Azure.
>
> V tomto kurzu použijete balíček Microsoft. Owin. Host. HttpListener, který poskytuje server HTTP, který se používá k samoobslužnému hostování aplikací OWIN.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - Webové rozhraní API 2
> - [Sada Azure SDK pro .NET 2,3](https://azure.microsoft.com/downloads/)

## <a name="create-a-microsoft-azure-project"></a>Vytvoření projektu Microsoft Azure

Spusťte aplikaci Visual Studio s oprávněními správce. K místnímu ladění aplikace pomocí emulátoru služby COMPUTE Azure jsou nutná oprávnění správce.

V nabídce **soubor** klikněte na příkaz **Nový**a potom na **projekt**. Z **nainstalovaných šablon**v části C#vizuál klikněte na **Cloud** a pak klikněte na **cloudová služba Windows Azure**. Pojmenujte projekt "soubor azureapp" a klikněte na tlačítko **OK**.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

V dialogovém okně **Nová cloudová služba Microsoft Azure** poklikejte na **role pracovního procesu**. Ponechte výchozí název ("WorkerRole1"). Tento krok přidá do řešení pracovní roli. Klikněte na tlačítko **OK**.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

Vytvořené řešení sady Visual Studio obsahuje dva projekty:

- &quot;soubor azureapp&quot; definuje role a konfiguraci pro aplikaci Azure.
- &quot;WorkerRole1&quot; obsahuje kód role pracovního procesu.

Obecně platí, že aplikace Azure může obsahovat více rolí, i když tento kurz používá jedinou roli.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a>Přidat webové rozhraní API a balíčky OWIN

V nabídce **nástroje** klikněte na **Správce balíčků NuGet**a pak klikněte na **Konzola správce balíčků**.

V okně konzoly Správce balíčků zadejte následující příkaz:

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a>Přidat koncový bod HTTP

V Průzkumník řešení rozbalte projekt soubor azureapp. Rozbalte uzel role, klikněte pravým tlačítkem na WorkerRole1 a vyberte **vlastnosti**.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

Klikněte na **koncové body**a pak klikněte na **přidat koncový bod**.

V rozevíracím seznamu **protokol** vyberte http. Do **veřejného portu** a **privátního portu**zadejte 80. Tato čísla portů se mohou lišit. Veřejný port je používán klienty při odesílání žádosti do role.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a>Konfigurace webového rozhraní API pro samoobslužné hostování

V Průzkumník řešení klikněte pravým tlačítkem na projekt WorkerRole1 a výběrem **přidat** / **třídu** přidejte novou třídu. Pojmenujte `Startup`třídy.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

Celý často používaný kód nahraďte tímto souborem:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a>Přidat kontroler webového rozhraní API

Dále přidejte třídu kontroleru webového rozhraní API. Klikněte pravým tlačítkem na projekt WorkerRole1 a vyberte **přidat** / **třídy**. Pojmenujte třídu TestController. Celý často používaný kód nahraďte tímto souborem:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

Pro zjednodušení tento kontroler jenom definuje dvě metody GET, které vracejí prostý text.

## <a name="start-the-owin-host"></a>Spustit hostitele OWIN

Otevřete soubor WorkerRole.cs. Tato třída definuje kód, který se spustí při spuštění a zastavení role pracovního procesu.

Přidejte následující příkaz using:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

Přidejte člena **IDisposable** do třídy `WorkerRole`:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

Do `OnStart` metody přidejte následující kód pro spuštění hostitele:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

Metoda **WebApp. Start** SPUSTÍ hostitele Owin. Název třídy `Startup` je parametr typu metody. Podle konvence hostitel zavolá metodu `Configure` této třídy.

Přepište `OnStop` k Dispose instance *\_aplikace* :

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

Zde je kompletní kód pro WorkerRole.cs:

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

Sestavte řešení a stisknutím klávesy F5 spusťte aplikaci místně v emulátoru služby COMPUTE Azure. V závislosti na nastavení brány firewall možná budete muset emulátor zapnout přes bránu firewall.

> [!NOTE]
> Pokud získáte výjimku, jak je vidět níže, přečtěte si [Tento Blogový příspěvek](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) , kde najdete alternativní řešení. Nepovedlo se načíst soubor nebo sestavení Microsoft. Owin, Version = 2.0.2.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 nebo jedna z jejích závislostí. Nalezená definice manifestu sestavení neodpovídá odkazu na sestavení. (Výjimka z HRESULT: 0x80131040)

Emulátor služby COMPUTE přiřadí koncovému bodu místní IP adresu. IP adresu najdete v uživatelském rozhraní emulátoru Compute. Klikněte pravým tlačítkem myši na ikonu emulátoru v oznamovací oblasti na hlavním panelu a vyberte **Zobrazit uživatelské rozhraní emulátoru COMPUTE**.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

Vyhledejte IP adresu v části nasazení služeb, nasazení [ID], Podrobnosti služby. Otevřete webový prohlížeč a přejděte na<em>adresu http:///Test/1</em>, kde <em>adresa</em> je IP adresa přiřazená emulátorem COMPUTE; například `http://127.0.0.1:80/test/1`. Měla by se zobrazit odpověď z kontroleru webového rozhraní API:

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a>Nasazení do Azure

Pro tento krok musíte mít účet Azure. Pokud ho ještě nemáte, můžete si během několika minut vytvořit bezplatný zkušební účet. Podrobnosti najdete v tématu [Microsoft Azure bezplatné zkušební verze](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).

V Průzkumník řešení klikněte pravým tlačítkem myši na projekt soubor azureapp. Vyberte **Publikovat**.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

Pokud nejste přihlášení ke svému účtu Azure, klikněte na **Přihlásit**se.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

Po přihlášení vyberte předplatné a klikněte na **Další**.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

Zadejte název cloudové služby a vyberte oblast. Klikněte na možnost **Vytvořit**.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

Klikněte na **Publikovat**.

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

V okně Protokol aktivit Azure se zobrazuje průběh nasazení. Po nasazení aplikace přejděte na http://appname.cloudapp.net/test/1.

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a>Další prostředky

- [Přehled projektu Katana](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [Projekt Katana na GitHubu](https://github.com/aspnet/AspNetKatana)

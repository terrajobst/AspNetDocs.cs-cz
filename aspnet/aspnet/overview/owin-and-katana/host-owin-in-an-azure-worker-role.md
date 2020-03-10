---
uid: aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
title: Hostování OWIN v roli pracovního procesu Azure | Microsoft Docs
author: MikeWasson
description: V tomto kurzu se dozvíte, jak můžete OWIN sebe samostatně hostovat do role pracovního procesu Microsoft Azure. Open Web Interface for .NET (OWIN) definuje abstrakci mezi webovým serverem .NET...
ms.author: riande
ms.date: 04/11/2014
ms.assetid: 07aa855a-92ee-4d43-ba66-5bfd7de20ee6
msc.legacyurl: /aspnet/overview/owin-and-katana/host-owin-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: 59d2e0d549427093f8a2424b17af81169b78ef30
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584614"
---
# <a name="host-owin-in-an-azure-worker-role"></a>Hostování specifikace OWIN v rolích pracovního procesu v Azure

o [Jan Wasson](https://github.com/MikeWasson)

> V tomto kurzu se dozvíte, jak můžete OWIN sebe samostatně hostovat do role pracovního procesu Microsoft Azure.
>
> [Open Web Interface for .NET](http://owin.org/) (Owin) definuje abstrakci mezi webovými servery .NET a webovými aplikacemi. OWIN odpojí webovou aplikaci od serveru, což OWIN je ideální pro samoobslužné hostování webové aplikace ve vlastním procesu mimo službu IIS – například v rámci role pracovního procesu Azure.
>
> V tomto kurzu se naučíte, jak sami hostovat aplikace OWIN v rámci role pracovního procesu Microsoft Azure. Další informace o rolích pracovního procesu najdete v tématu [modely spouštění Azure](https://azure.microsoft.com/documentation/articles/fundamentals-application-models/#CloudServices).
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - [Sada Azure SDK pro .NET 2,3](https://azure.microsoft.com/downloads/)
> - [Microsoft. Owin. SelfHost 2.1.0](http://www.nuget.org/packages/Microsoft.Owin.SelfHost/2.1.0)

## <a name="create-a-microsoft-azure-project"></a>Vytvoření projektu Microsoft Azure

Spusťte aplikaci Visual Studio s oprávněními správce. K místnímu ladění aplikace pomocí emulátoru služby COMPUTE Azure jsou nutná oprávnění správce.

V nabídce **soubor** klikněte na příkaz **Nový**a potom na **projekt**. Z **nainstalovaných šablon**v části C#vizuál klikněte na **Cloud** a pak klikněte na **cloudová služba Windows Azure**. Pojmenujte projekt "soubor azureapp" a klikněte na tlačítko **OK**.

[![](host-owin-in-an-azure-worker-role/_static/image2.png)](host-owin-in-an-azure-worker-role/_static/image1.png)

V dialogovém okně **Nová cloudová služba Microsoft Azure** poklikejte na **role pracovního procesu**. Ponechte výchozí název ("WorkerRole1"). Tento krok přidá do řešení pracovní roli. Klikněte na tlačítko **OK**.

[![](host-owin-in-an-azure-worker-role/_static/image4.png)](host-owin-in-an-azure-worker-role/_static/image3.png)

Vytvořené řešení sady Visual Studio obsahuje dva projekty:

- &quot;soubor azureapp&quot; definuje role a konfiguraci pro aplikaci Azure.
- &quot;WorkerRole1&quot; obsahuje kód role pracovního procesu.

Obecně platí, že aplikace Azure může obsahovat více rolí, i když tento kurz používá jedinou roli.

![](host-owin-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-owin-self-host-packages"></a>Přidání balíčků pro samoobslužné hostování OWIN

V nabídce **nástroje** klikněte na **Správce balíčků NuGet**a pak klikněte na **Konzola správce balíčků**.

V okně konzoly Správce balíčků zadejte následující příkaz:

[!code-console[Main](host-owin-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a>Přidat koncový bod HTTP

V Průzkumník řešení rozbalte projekt soubor azureapp. Rozbalte uzel role, klikněte pravým tlačítkem na WorkerRole1 a vyberte **vlastnosti**.

![](host-owin-in-an-azure-worker-role/_static/image6.png)

Klikněte na **koncové body**a pak klikněte na **přidat koncový bod**.

V rozevíracím seznamu **protokol** vyberte http. Do **veřejného portu** a **privátního portu**zadejte 80. Tato čísla portů se mohou lišit. Veřejný port je používán klienty při odesílání žádosti do role.

[![](host-owin-in-an-azure-worker-role/_static/image8.png)](host-owin-in-an-azure-worker-role/_static/image7.png)

## <a name="create-the-owin-startup-class"></a>Vytvoření třídy pro spuštění OWIN

V Průzkumník řešení klikněte pravým tlačítkem na projekt WorkerRole1 a výběrem **přidat** / **třídu** přidejte novou třídu. Pojmenujte `Startup`třídy.

Celý často používaný kód nahraďte následujícím kódem:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample2.cs)]

Metoda rozšíření `UseWelcomePage` přidá do aplikace jednoduchou stránku HTML, aby bylo možné ověřit, zda lokalita funguje.

## <a name="start-the-owin-host"></a>Spustit hostitele OWIN

Otevřete soubor WorkerRole.cs. Tato třída definuje kód, který se spustí při spuštění a zastavení role pracovního procesu.

Přidejte následující příkaz using:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample3.cs)]

Přidejte člena **IDisposable** do třídy `WorkerRole`:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample4.cs)]

Do `OnStart` metody přidejte následující kód pro spuštění hostitele:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample5.cs?highlight=5)]

Metoda **WebApp. Start** SPUSTÍ hostitele Owin. Název třídy `Startup` je parametr typu metody. Podle konvence hostitel zavolá metodu `Configure` této třídy.

Přepište `OnStop` k Dispose instance *\_aplikace* :

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample6.cs)]

Zde je kompletní kód pro WorkerRole.cs:

[!code-csharp[Main](host-owin-in-an-azure-worker-role/samples/sample7.cs)]

Sestavte řešení a stisknutím klávesy F5 spusťte aplikaci místně v emulátoru služby COMPUTE Azure. V závislosti na nastavení brány firewall možná budete muset emulátor zapnout přes bránu firewall.

Emulátor služby COMPUTE přiřadí koncovému bodu místní IP adresu. IP adresu najdete v uživatelském rozhraní emulátoru Compute. Klikněte pravým tlačítkem myši na ikonu emulátoru v oznamovací oblasti na hlavním panelu a vyberte **Zobrazit uživatelské rozhraní emulátoru COMPUTE**.

[![](host-owin-in-an-azure-worker-role/_static/image10.png)](host-owin-in-an-azure-worker-role/_static/image9.png)

Vyhledejte IP adresu v části nasazení služeb, nasazení [ID], Podrobnosti služby. Otevřete webový prohlížeč a přejděte na adresu http:\/\/*adresa*, kde *adresa* je IP adresa přiřazená emulátorem COMPUTE; například `http://127.0.0.1:80`. Měla by se zobrazit úvodní stránka OWIN:

![](host-owin-in-an-azure-worker-role/_static/image11.png)

## <a name="deploy-to-azure"></a>Nasazení do Azure

Pro tento krok musíte mít účet Azure. Pokud ho ještě nemáte, můžete si během několika minut vytvořit bezplatný zkušební účet. Podrobnosti najdete v tématu [Microsoft Azure bezplatné zkušební verze](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).

V Průzkumník řešení klikněte pravým tlačítkem myši na projekt soubor azureapp. Vyberte **Publikovat**.

![](host-owin-in-an-azure-worker-role/_static/image12.png)

Pokud nejste přihlášení ke svému účtu Azure, klikněte na **Přihlásit**se.

[![](host-owin-in-an-azure-worker-role/_static/image14.png)](host-owin-in-an-azure-worker-role/_static/image13.png)

Po přihlášení vyberte předplatné a klikněte na **Další**.

[![](host-owin-in-an-azure-worker-role/_static/image16.png)](host-owin-in-an-azure-worker-role/_static/image15.png)

Zadejte název cloudové služby a vyberte oblast. Klikněte na možnost **Vytvořit**.

![](host-owin-in-an-azure-worker-role/_static/image17.png)

Klikněte na **Publikovat**.

[![](host-owin-in-an-azure-worker-role/_static/image19.png)](host-owin-in-an-azure-worker-role/_static/image18.png)

V okně Protokol aktivit Azure se zobrazuje průběh nasazení. Po nasazení aplikace přejděte na adresu `http://appname.cloudapp.net/`, kde *AppName* je název vaší cloudové služby.

## <a name="additional-resources"></a>Další prostředky

- [Přehled projektu Katana](an-overview-of-project-katana.md)
- [Projekt Katana na GitHubu](https://github.com/aspnet/AspNetKatana/)

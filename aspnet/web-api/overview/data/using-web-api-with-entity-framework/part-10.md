---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-10
title: Publikování aplikace do Azure Azure App Service | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 10fd812b-94d6-4967-be97-a31ce9c45e2c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-10
msc.type: authoredcontent
ms.openlocfilehash: a9a7b74a07c71b47253c0af304c7a26ffa4eaae5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622386"
---
# <a name="publish-the-app-to-azure-azure-app-service"></a>Publikování aplikace do Azure Azure App Service

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://github.com/MikeWasson/BookService)

V posledním kroku budete aplikaci publikovat do Azure. V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a vyberte **publikovat**.

![](part-10/_static/image1.png)

Kliknutí na **publikovat** vyvolá dialog **Publikovat web** . Pokud jste při prvním vytvoření projektu zaškrtli políčko **hostitel v cloudu** , připojení a nastavení jsou už nakonfigurované. V takovém případě stačí kliknout na kartu **Nastavení** a zaškrtnout &quot;spustit migrace Code First&quot;. (Pokud jste na začátku nezkontrolovali **hostitele v cloudu** , postupujte podle pokynů v [následující části](#new-website).)

[![](part-10/_static/image3.png)](part-10/_static/image2.png)

Pokud chcete aplikaci nasadit, klikněte na **publikovat**. Průběh publikování můžete zobrazit v okně **aktivity publikování na webu** . (V nabídce **zobrazení** vyberte **jiné okna**a pak vyberte **aktivita publikování webu**.)

![](part-10/_static/image4.png)

Když Visual Studio dokončí nasazení aplikace, výchozí prohlížeč se automaticky otevře na adrese URL nasazeného webu a aplikace, kterou jste vytvořili, je teď spuštěná v cloudu. Adresa URL v adresním řádku prohlížeče ukazuje, že lokalita je načítána z Internetu.

[![](part-10/_static/image6.png)](part-10/_static/image5.png)

<a id="new-website"></a>
## <a name="deploying-to-a-new-website"></a>Nasazení na nový web

Pokud jste při prvním vytvoření projektu nezkontrolovali možnost **hostitel v cloudu** , můžete teď nakonfigurovat novou webovou aplikaci. V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a vyberte **publikovat**. Vyberte kartu **profil** a klikněte na **Microsoft Azure websites**. Pokud v tuto chvíli nejste přihlášení k Azure, budete vyzváni k přihlášení.

[![](part-10/_static/image8.png)](part-10/_static/image7.png)

V dialogovém okně **existující weby** klikněte na **Nový**.

![](part-10/_static/image9.png)

Zadejte název webu. Vyberte své předplatné Azure a oblast. V části **databázový server**vyberte **vytvořit nový server**nebo vyberte existující server. Klikněte na možnost **Vytvořit**.

[![](part-10/_static/image11.png)](part-10/_static/image10.png)

Klikněte na kartu **Nastavení** a zaškrtněte &quot;spustit migrace Code First&quot;. Pak klikněte na **publikovat**.

> [!div class="step-by-step"]
> [Předchozí](part-9.md)

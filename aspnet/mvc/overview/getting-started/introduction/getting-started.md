---
uid: mvc/overview/getting-started/introduction/getting-started
title: Začínáme s ASP.NET MVC 5 | Microsoft Docs
author: Rick-Anderson
ms.author: riande
ms.date: 10/04/2018
ms.assetid: f3d8adbe-55e7-4fd4-84a8-7155bc45c676
msc.legacyurl: /mvc/overview/getting-started/introduction/getting-started
msc.type: authoredcontent
ms.openlocfilehash: ca39bc37c757c0452cf56624c8e37c04df4b41f2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78602765"
---
# <a name="getting-started-with-aspnet-mvc-5"></a>Začínáme s ASP.NET MVC 5

od [Rick Anderson](https://twitter.com/RickAndMSFT)

[!INCLUDE [consider RP](../../../../includes/razor.md)]

V tomto kurzu se naučíte základy vytvoření webové aplikace ASP.NET MVC 5 pomocí sady [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017). Konečný zdrojový kód tohoto kurzu najdete na [GitHubu](https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie/MvcMovie).

Tento kurz napsal [Scott Guthrie](https://weblogs.asp.net/scottgu/) (Twitter[@scottgu](https://twitter.com/scottgu) ), [scott Hanselman](http://www.hanselman.com/blog/) (Twitter: [@shanselman](https://twitter.com/shanselman) ) a [Rick Anderson](https://twitter.com/RickAndMSFT) ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ).

K nasazení této aplikace do Azure potřebujete účet Azure:

- Můžete si [otevřít účet Azure zdarma](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) – získáte kredity, které můžete použít k vyzkoušení placených služeb Azure a dokonce i po jejich použití, můžete účet ponechat a používat bezplatné služby Azure.
- Můžete [aktivovat výhody pro předplatitele MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) – vaše předplatné MSDN vám každý měsíc dává kredity, které můžete použít pro placené služby Azure.

## <a name="get-started"></a>Začínáme

Začněte [instalací sady Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017). Pak otevřete aplikaci Visual Studio.

Visual Studio je integrované vývojové prostředí (IDE) nebo integrované vývojové prostředí. Stejně jako při psaní dokumentů v aplikaci Microsoft Word použijete k vytvoření aplikací rozhraní IDE. V aplikaci Visual Studio je seznam v dolní části znázorňující různé možnosti, které máte k dispozici. K dispozici je také nabídka, která poskytuje další způsob, jak provádět úlohy v integrovaném vývojovém prostředí. Například namísto výběru **nového projektu** na **úvodní stránce**můžete použít řádek nabídek a vybrat **soubor** > **Nový projekt**.

![](getting-started/_static/image1.png)

## <a name="create-your-first-app"></a>Vytvoření první aplikace

Na **úvodní stránce**vyberte **Nový projekt**. V dialogovém okně **Nový projekt** vyberte kategorii **vizuálu C#**  na levé straně, pak **Web**a pak vyberte šablonu projektu **Webová aplikace ASP.NET (.NET Framework)** . Pojmenujte projekt "MvcMovie" a klikněte na **tlačítko OK**.

![](getting-started/_static/image2.png)

V dialogovém okně **Nová webová aplikace v ASP.NET** zvolte **MVC** a pak zvolte **OK**.

![](getting-started/_static/image3.png)

Aplikace Visual Studio použila pro projekt ASP.NET MVC, který jste právě vytvořili, výchozí šablonu, takže teď máte funkční aplikaci, aniž byste museli cokoli dělat! Toto je jednoduché "Hello World!" a je to vhodné místo pro spuštění vaší aplikace.

![](getting-started/_static/image4.png)

Stisknutím klávesy **F5** spusťte ladění. Když stisknete klávesu **F5**, Visual Studio spustí [IIS Express](/iis/extensions/introduction-to-iis-express/iis-express-overview) a spustí vaši webovou aplikaci. Visual Studio potom spustí prohlížeč a otevře domovskou stránku aplikace. Všimněte si, že adresní řádek prohlížeče uvádí `localhost:port#` a ne něco jako `example.com`. To je proto, že `localhost` vždy odkazuje na vlastní místní počítač, v tomto případě je spuštěná aplikace, kterou jste právě sestavili. Když Visual Studio spustí webový projekt, pro webový server se použije náhodný port. Na následujícím obrázku je číslo portu 1234. Při spuštění aplikace se zobrazí jiné číslo portu.

![](getting-started/_static/image5.png)

Přímo z tohoto pole vám tato výchozí šablona umožňuje `Home`, `Contact`a `About` stránek. Následující obrázek nezobrazuje odkazy **Domů**, **o**a **kontaktů** . V závislosti na velikosti okna prohlížeče může být nutné kliknutím na ikonu navigace zobrazit tyto odkazy.

![](getting-started/_static/image6.png)

Aplikace také poskytuje podporu pro registraci a přihlášení. Dalším krokem je změna toho, jak tato aplikace funguje, a dozvíte se trochu o ASP.NET MVC. Zavřete aplikaci ASP.NET MVC a Pojďme změnit nějaký kód.

Seznam aktuálních kurzů najdete v tématu [Doporučené články MVC](../mvc-learning-sequence.md).

## <a name="see-this-app-running-on-azure"></a>Podívejte se na tuto aplikaci spuštěnou v Azure

Chcete zobrazit dokončený web běžící jako živá webová aplikace? Úplnou verzi aplikace můžete nasadit do svého účtu Azure pouhým kliknutím na následující tlačítko.

[![](https://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?repository=https://github.com/dotnet/AspNetDocs/tree/master/aspnet/mvc/overview/getting-started/introduction/sample/MvcMovie&amp;WT.mc_id=deploy_azure_aspnet)

K nasazení tohoto řešení do Azure potřebujete účet Azure. Pokud ještě nemáte účet, použijte k vytvoření jednu z následujících možností:

- [Otevřete si bezplatný účet Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) – získáte kredity, které můžete použít k vyzkoušení placených služeb Azure a dokonce i po jejich použití, můžete účet ponechat a používat bezplatné služby Azure.
- [Aktivujte výhody pro předplatitele Visual studia](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers) – vaše předplatné sady Visual Studio vám každý měsíc poskytne kredity, které můžete použít pro placené služby Azure.

> [!div class="step-by-step"]
> [Next](adding-a-controller.md)

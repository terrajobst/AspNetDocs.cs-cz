---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-1
title: Používání webového rozhraní API 2 s Entity Framework 6 | Microsoft Docs
author: MikeWasson
description: V tomto kurzu se naučíte základy vytváření webových aplikací pomocí back-endu webového rozhraní API ASP.NET. Tento kurz používá pro stanovení dat Entity Framework 6...
ms.author: riande
ms.date: 01/17/2019
ms.assetid: e879487e-dbcd-4b33-b092-d67c37ae768c
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-1
msc.type: authoredcontent
ms.openlocfilehash: 0f5dc960f494af5bd4ce87863a510d1892319908
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622477"
---
# <a name="using-web-api-2-with-entity-framework-6"></a>Použití webového rozhraní API 2 se sadou Entity Framework 6

[Stáhnout dokončený projekt](https://github.com/MikeWasson/BookService)

> V tomto kurzu se naučíte základy vytváření webových aplikací pomocí back-endu ASP.NET webového rozhraní API. Kurz používá pro datovou vrstvu Entity Framework 6 a vyseknutí. js pro aplikaci JavaScriptu na straně klienta. Tento kurz také ukazuje, jak nasadit aplikaci do Azure App Service Web Apps.
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
>
> - Webové rozhraní API 2,1
> - Visual Studio 2017 ( [tady si můžete](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)stáhnout visual Studio 2017)
> - Entity Framework 6
> - .NET 4.7
> - [Vyseknutí. js](http://knockoutjs.com/) 3,1

V tomto kurzu se používá webové rozhraní API 2 ASP.NET s Entity Framework 6 k vytvoření webové aplikace, která pracuje s back-end databází. Tady je snímek obrazovky aplikace, kterou vytvoříte.

[![](part-1/_static/image2.png)](part-1/_static/image1.png)

Aplikace používá návrh jednostránkové aplikace (SPA). "Jednostránková aplikace" je obecný termín pro webovou aplikaci, která načte jednu stránku HTML a pak dynamicky aktualizuje stránku místo načtení nových stránek. Po počátečním načtení stránky aplikace mluví se serverem prostřednictvím požadavků AJAX. AJAX požaduje návratová data JSON, která aplikace používá k aktualizaci uživatelského rozhraní.

AJAX není novinkou, ale dnes existují rozhraní JavaScript, která usnadňují vytváření a údržbu rozsáhlých sofistikovaných aplikací SPA. V tomto kurzu se používá [vyseknutí. js](http://knockoutjs.com/), ale můžete použít libovolné klientské rozhraní JavaScript.

Tady jsou hlavní stavební kameny této aplikace:

- ASP.NET MVC vytvoří stránku HTML.
- Webové rozhraní API ASP.NET zpracovává požadavky AJAX a vrací data JSON.
- Vyseknutí dat. js – sváže prvky HTML s daty JSON.
- Entity Framework mluví s databází.

## <a name="see-this-app-running-on-azure"></a>Podívejte se na tuto aplikaci spuštěnou v Azure

Chcete zobrazit dokončený web běžící jako živá webová aplikace? Úplnou verzi aplikace můžete nasadit do svého účtu Azure tak, že vyberete následující tlačítko.

[![](http://azuredeploy.net/deploybutton.png)](https://azuredeploy.net/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/BookService)

K nasazení tohoto řešení do Azure potřebujete účet Azure. Pokud ještě nemáte účet, máte následující možnosti:

- [Otevřete si bezplatný účet Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) – získáte kredity, které můžete použít k vyzkoušení placených služeb Azure a dokonce i po jejich použití, můžete účet ponechat a používat bezplatné služby Azure.
- [Aktivujte výhody pro předplatitele MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) – vaše předplatné MSDN vám každý měsíc dává kredity, které můžete použít pro placené služby Azure.

## <a name="create-the-project"></a>Vytvoření projektu

Otevřete sadu Visual Studio. V nabídce **soubor** vyberte **Nový**a pak vyberte **projekt**. (Nebo na úvodní stránce vyberte **Nový projekt** .)

V dialogovém okně **Nový projekt** vyberte v levém podokně možnost **Web** a v prostředním podokně **ASP.NET webová aplikace (.NET Framework)** . Pojmenujte projekt **BookService** a vyberte **OK**.

[![](part-1/_static/image11.png)](part-1/_static/image11.png)

V dialogovém okně **Nový projekt ASP.NET** vyberte šablonu **webové rozhraní API** .

[![](part-1/_static/image12.png)](part-1/_static/image12.png)

Vyberte **OK** a vytvořte projekt.

## <a name="configure-azure-settings-optional"></a>Konfigurace nastavení Azure (volitelné)

Po vytvoření projektu můžete zvolit, že se má Azure App Service Web Apps kdykoli nasadit. 

1. V Průzkumník řešení klikněte pravým tlačítkem na projekt a vyberte **publikovat**.

2. V okně, které se zobrazí, vyberte **Spustit**. Zobrazí se dialogové okno **vybrat cíl publikování** .

   [![](part-1/_static/image14.png)](part-1/_static/image14.png)

3. Vyberte **vytvořit profil**. Zobrazí se dialogové okno **vytvořit App Service** .

   [![](part-1/_static/image15.png)](part-1/_static/image15.png)

   Přijměte výchozí hodnoty nebo zadejte jiné hodnoty pro název aplikace, skupinu prostředků, plán hostování, předplatné Azure a geografickou oblast. 

4. Vyberte **vytvořit databázi SQL**. Zobrazí se dialogové okno **konfigurace SQL Server** . 

   [![](part-1/_static/image16.png)](part-1/_static/image16.png)

   Přijměte výchozí hodnoty nebo zadejte jiné hodnoty. Zadejte **uživatelské jméno správce** a **heslo správce** pro novou databázi. Až budete hotovi, vyberte **OK** . Znovu se zobrazí stránka **vytvořit App Service** .

5. Vyberte **vytvořit** a vytvořte svůj profil. V pravém dolním rohu se zobrazí zpráva s informacemi o tom, že nasazení probíhá. Po krátké době se okno **publikování** znovu zobrazí.

    [![](part-1/_static/image17.png)](part-1/_static/image17.png)
   
    Profil, který jste vytvořili pro nasazení aplikace, je nyní k dispozici. 

> [!div class="step-by-step"]
> [Next](part-2.md)

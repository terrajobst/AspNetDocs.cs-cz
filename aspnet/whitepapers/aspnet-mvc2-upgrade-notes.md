---
uid: whitepapers/aspnet-mvc2-upgrade-notes
title: Upgrade aplikace ASP.NET MVC 1,0 na ASP.NET MVC 2 | Microsoft Docs
author: rick-anderson
description: Tento dokument popisuje, jak ručně upgradovat a pomocí Průvodce aplikaci ASP.NET MVC 1,0 na ASP.NET MVC 2. Tento dokument je také k dispozici pro d...
ms.author: riande
ms.date: 04/08/2010
ms.assetid: f1a01759-d251-4b09-8835-e112e336c6dd
msc.legacyurl: /whitepapers/aspnet-mvc2-upgrade-notes
msc.type: content
ms.openlocfilehash: 27589f1b1c9d5038118e5ff0cc2e7cecae17d5ed
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637016"
---
# <a name="upgrading-an-aspnet-mvc-10-application-to-aspnet-mvc-2"></a>Upgrade aplikace ASP.NET MVC 1.0 na ASP.NET MVC 2

> Tento dokument popisuje, jak ručně upgradovat a pomocí Průvodce aplikaci ASP.NET MVC 1,0 na ASP.NET MVC 2. Tento dokument je také k dispozici ke [stažení](https://download.microsoft.com/download/F/1/6/F16F9AF9-8EF4-4845-BC97-639791D5699C/MVC2-Upgrade-Notes.pdf) .

## <a name="introduction"></a>Úvod

ASP.NET MVC 2 se dá nainstalovat vedle sebe s ASP.NET MVC 1,0 na stejném serveru. To dává vývojářům aplikací flexibilitu při rozhodování o upgradu aplikace ASP.NET MVC 1,0 na ASP.NET MVC 2.

Visual Studio 2010 obsahuje průvodce, který upgraduje stávající projekty ASP.NET MVC 1,0 vytvořené pomocí sady Visual Studio 2008 na ASP.NET MVC 2. Průvodce upgradem se spouští otevřením projektu ASP.NET MVC 1,0 v aplikaci Visual Studio 2010.

## <a name="upgrade-wizard-for-aspnet-mvc-10-on-visual-studio-2008-sp1"></a>Průvodce upgradem pro ASP.NET MVC 1,0 ve Visual Studiu 2008 SP1

K upgradu aplikace ASP.NET MVC 1,0 na ASP.NET MVC 2 v aplikaci Visual Studio 2008 SP1 použijte MvcAppConverter aplikaci (nepodporované). Tuto aplikaci si můžete stáhnout z následující adresy URL:

[https://go.microsoft.com/fwlink/?LinkID=185351](https://go.microsoft.com/fwlink/?LinkID=185351)

## <a name="manually-upgrading-an-aspnet-mvc-10-project"></a>Ruční upgrade projektu ASP.NET MVC 1,0

Pokud chcete ručně upgradovat existující aplikaci ASP.NET MVC 1,0 na verzi 2, postupujte takto:

1. Vytvořte zálohu existujícího projektu.
2. V textovém editoru otevřete soubor projektu (soubor s příponou souboru. csproj nebo. vbproj) a vyhledejte element ProjectTypeGuid. Jako hodnotu tohoto elementu nahraďte GUID {603c0e0b-db56-11dc-be95-000d561079b0} hodnotou {F85E285D-A4E0-4152-9332-AB1D724D3325}. Až budete hotovi, hodnota tohoto prvku by měla být následující: 

    `{F85E285D-A4E0-4152-9332-AB1D724D3325};{349c5851-65df-11da-9384-00065b846f21};{fae04ec0-301f-11d3-bf4b-00c04f79efbc}`
3. V kořenové složce webové aplikace upravte soubor Web. config. Vyhledejte System. Web. Mvc, Version = 1.0.0.0 a nahraďte všechny instance pomocí System. Web. Mvc, Version = 2.0.0.0.
4. Opakujte předchozí krok pro soubor Web. config umístěný ve složce views.
5. Otevřete projekt pomocí sady Visual Studio a v **Průzkumník řešení**rozbalte uzel **odkazy** . Odstraňte odkaz na System. Web. Mvc (který odkazuje na sestavení verze 1,0). Přidejte odkaz na System. Web. Mvc (v 2.0.0.0).
6. Přidejte následující element bindingRedirect do souboru Web. config v kořenovém adresáři aplikace v části zobrazí dostupných:   

    [!code-xml[Main](aspnet-mvc2-upgrade-notes/samples/sample1.xml)]
7. Vytvořte novou prázdnou aplikaci ASP.NET MVC 2. Zkopírujte soubory ze složky skripty nové aplikace do složky skripty v existující aplikaci.
8. Aktualizujte existující soubor aplikace. €™ s CSS definicemi stylů CSS v souboru Web. CSS.
9. Zkompilujte aplikaci a spusťte ji. Pokud dojde k nějakým chybám, přečtěte si část důležité změny na stránce [co je nového v ASP.NET MVC 2](https://go.microsoft.com/fwlink/?LinkID=185038) .

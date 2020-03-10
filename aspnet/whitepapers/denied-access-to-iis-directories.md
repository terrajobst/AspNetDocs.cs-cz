---
uid: whitepapers/denied-access-to-iis-directories
title: ASP.NET odepřel přístup k adresářům služby IIS | Microsoft Docs
author: rick-anderson
description: Tento dokument white paper popisuje, co je třeba udělat, pokud požadavek na vaši aplikaci ASP.NET vrátí chybu, "odepřený přístup k adresáři adresáře. Nepovedlo se s...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: 3cb27b8a-354f-4332-bfe0-232b13bbf8aa
msc.legacyurl: /whitepapers/denied-access-to-iis-directories
msc.type: content
ms.openlocfilehash: a3a53aa88abbe1bcaaea7d691406800c8f9b988b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638500"
---
# <a name="aspnet-denied-access-to-iis-directories"></a>Aplikace ASP.NET zamítla přístup k adresářům služby IIS

> Tento dokument white paper popisuje, co je třeba udělat, pokud požadavek na vaši aplikaci ASP.NET vrátí chybu, "odepřený přístup k adresáři *adresáře* . Nepovedlo se spustit monitorování změn adresáře.
> 
> Platí pro ASP.NET 1,0 a ASP.NET 1,1.

ASP.NET v1 RTM teď používá méně privilegovaný účet systému Windows, který je zaregistrován jako účet ASPNET na místním počítači.

V některých uzamčených systémech nemusí tento účet ve výchozím nastavení mít přístup pro čtení k adresářům obsahu webu, kořenovému adresáři aplikace nebo kořenovému adresáři webu. V takovém případě se při žádosti o stránky z dané webové aplikace zobrazí následující chyba:

![](denied-access-to-iis-directories/_static/image1.jpg)

Chcete-li tento problém vyřešit, budete muset změnit oprávnění zabezpečení pro příslušné adresáře.

Konkrétně ASP.NET vyžaduje přístup pro čtení, spouštění a výpis pro účet ASPNET pro kořen webu (například c:\Inetpub\Wwwroot nebo libovolný alternativní adresář webu, který jste mohli nakonfigurovat ve službě IIS), adresář obsahu a kořenový adresář aplikace. aby bylo možné monitorovat změny konfiguračního souboru. Kořen aplikace odpovídá cestě ke složce přidružené k virtuálnímu adresáři aplikace v nástroji pro správu služby IIS (inetmgr).

Podívejte se například na následující hierarchii aplikací ve složce Wwwroot.

`C:\inetpub\wwwroot\myapp\default.aspx`

V tomto příkladu účet ASPNET potřebuje oprávnění ke čtení definovaná výše pro obsah v adresáři MyApp i Wwwroot. Jeden zděděný seznam řízení přístupu (ACL) kořenové složky se dá volitelně použít i pro oba adresáře, pokud jsou vnořené.

Chcete-li přidat oprávnění k adresáři, proveďte následující kroky:

- Pomocí Průzkumníka Windows přejděte do adresáře.
- Klikněte pravým tlačítkem na složku adresáře a vyberte vlastnosti.
- Přejděte na kartu zabezpečení v dialogovém okně Vlastnosti.
- Klikněte na tlačítko Přidat a zadejte název počítače následovaný názvem účtu ASPNET. Například v počítači s názvem "webdev" zadáte webdev\ASPNET a získáte "OK".
- Ujistěte se, že má účet ASPNET zaškrtnuté políčko číst &amp; spustit, zobrazovat obsah složky a číst.
- Kliknutím na OK zavřete dialogové okno a změny uložte.

![](denied-access-to-iis-directories/_static/image2.jpg)

V případě potřeby je možné tyto změny automatizovat pomocí skriptů nebo nástroje Cacls. exe, který se dodává se systémem Windows. Další informace o účtu ASPNET najdete v [dokumentu nejčastějších dotazů](https://go.microsoft.com/fwlink/?LinkId=5828).

Pokud daná webová aplikace spoléhá na konkrétní složku nebo soubor oprávnění pro zápis nebo změnu, může to být uděleno stejným postupem a zaškrtnutím políček "zapsat" nebo "Upravit".

V počítačích, které povolují všem uživatelům nebo skupinám přístup pro čtení k těmto adresářům (což je výchozí konfigurace), nebudou zjištěny žádné problémy a výše uvedené kroky nebudou nutné.

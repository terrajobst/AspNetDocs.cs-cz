---
uid: single-page-application/overview/templates/hottowel-template
title: Hot navrhování ručníků Template | Microsoft Docs
author: madskristensen
description: Šablona HotTowel
ms.author: riande
ms.date: 02/09/2013
ms.assetid: 75af2e17-6ed3-4d24-8ea1-bc340027c318
msc.legacyurl: /single-page-application/overview/templates/hottowel-template
msc.type: authoredcontent
ms.openlocfilehash: eeab69e75546791978bb09d7823d95caf9dca1a0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578482"
---
# <a name="hot-towel-template"></a>Šablona Hot Towel

od [Madse Kristensena](https://github.com/madskristensen)

> Hot navrhování ručníků se šablona MVC zapisuje Jan Papa
> 
> Vyberte verzi, kterou chcete stáhnout:
> 
> [Šablona MVC Hot navrhování ručníků pro Visual Studio 2012](https://visualstudiogallery.msdn.microsoft.com/1f68fbe8-b4e9-4968-9fd3-ddc7cbc52dca)
> 
> [Šablona MVC Hot navrhování ručníků pro Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/1eb8780d-d522-4dcf-bf56-56f0eab305c2)
> 
> 
> Hot navrhování ručníků: vzhledem k tomu, že nechcete, aby bylo možné přejít na zabezpečené ověřování pro hesla bez použití!

Chcete sestavit SPA, ale nemůžete se rozhodnout, kde začít? Používejte horké navrhování ručníků a v sekundách budete mít zabezpečené a všechny nástroje, které potřebujete k sestavení na počítači!.

Hot navrhování ručníků vytvoří skvělý výchozí bod pro vytváření jednostránkové aplikace (SPA) s ASP.NET. V tomto poli poskytuje modulární strukturu pro váš kód, zobrazení navigace, datovou vazbu, bohatou správu dat a jednoduché, ale elegantní styly. Hot navrhování ručníků poskytuje vše, co potřebujete k vytvoření zabezpečeného hesla, takže se můžete soustředit na svou aplikaci, ne na instalace.

> Přečtěte si další informace o vytváření zabezpečeného hesla z [Jan Papa videa, výukových kurzů a Pluralsight kurzů](http://johnpapa.net/spa?vsix).

## <a name="application-structure"></a>Struktura aplikace

Hot navrhování ručníků SPA poskytuje složku aplikace, která obsahuje JavaScript a soubory HTML, které definují vaši aplikaci.

Ve složce aplikace:

- durandal
- services
- viewmodels
- views

Složka aplikace obsahuje kolekci modulů. Tyto moduly zapouzdřují funkce a deklaruje závislosti na dalších modulech. Složka zobrazení obsahuje HTML pro vaši aplikaci a složka ViewModels obsahuje logiku prezentace pro zobrazení (společný vzor MVVM). Složka služby je ideální pro uchovávání všech běžných služeb, které vaše aplikace může potřebovat, jako je například načtení dat HTTP nebo interakce místního úložiště. Je běžné, že více ViewModels opakovaně používá kód z modulů služby.

## <a name="aspnet-mvc-server-side-application-structure"></a>Struktura aplikace na straně serveru ASP.NET MVC

Horká navrhování ručníků se staví na známé a výkonné struktuře ASP.NET MVC.

- Začátek aplikace\_
- Obsah
- Kontrolery
- Modely
- Scripts
- Zobrazení

## <a name="featured-libraries"></a>Doporučené knihovny

- ASP.NET MVC
- Webové rozhraní API ASP.NET
- ASP.NET Web Optimization – sdružování a minifikace
- [Breeze. js](http://Breezejs.com) – Správa dat ve bohatě
- [Durandal. js](http://Durandaljs.com) – navigace a zobrazení – kompozice
- [Vyseknutí. js](http://Knockoutjs.com) – datové vazby
- [Vyžadování modularity. js](http://requirejs.org) s využitím AMD a optimalizace
- [Informační zpráva. js](http://jpapa.me/c7toastr) – překryvné zprávy
- Spuštění [Twitteru](https://twitter.github.com/bootstrap/) – robustní styly CSS

## <a name="installing-via-the-visual-studio-2012-hot-towel-spa-template"></a>Instalace prostřednictvím šablony zabezpečeného hesla sady Visual Studio 2012 Hot navrhování ručníků

Hot navrhování ručníků se dá nainstalovat jako šablona sady Visual Studio 2012. Stačí kliknout na `File` | `New Project` a zvolit `ASP.NET MVC 4 Web Application`. Pak vyberte šablonu Hot navrhování ručníků Page a spusťte ji!

## <a name="installing-via-the-nuget-package"></a>Instalace prostřednictvím balíčku NuGet

Hot navrhování ručníků je také balíček NuGet, který rozšiřuje existující prázdný projekt ASP.NET MVC. Stačí jenom nainstalovat pomocí NuGet a pak spustit.

[!code-powershell[Main](hottowel-template/samples/sample1.ps1)]

## <a name="how-do-i-build-on-hot-towel"></a>Jak na Hot navrhování ručníků vytvořit?

Stačí začít přidávat kód!

1. Přidejte vlastní kód na straně serveru, nejlépe Entity Framework a WebAPI (což skutečně září Breeze. js).
2. Přidat zobrazení do složky `App/views`
3. Přidat ViewModels do složky `App/viewmodels`
4. Přidání datových vazeb HTML a vykrojení do nových zobrazení
5. Aktualizovat navigační trasy v `shell.js`

## <a name="walkthrough-of-the-htmljavascript"></a>Návod pro HTML/JavaScript

### <a name="viewshottowelindexcshtml"></a>Views/HotTowel/index.cshtml

index. cshtml je počáteční trasa a zobrazení pro aplikaci MVC. Obsahuje všechny standardní metaznačky, odkazy CSS a reference JavaScriptu, které byste očekávali. Tělo obsahuje jednu `<div>`, kde se při vyžádání umístí veškerý obsah (vaše zobrazení). `@Scripts.Render` používá pro spuštění úvodního bodu pro kód aplikace, který je obsažen v souboru `main.js`, požadavek. js. K dispozici je úvodní obrazovka, která ukazuje, jak během načítání aplikace vytvořit úvodní obrazovku.

[!code-cshtml[Main](hottowel-template/samples/sample2.cshtml)]

### <a name="appmainjs"></a>App/main.js

`main.js` soubor obsahuje kód, který se spustí hned po načtení vaší aplikace. Tady je místo, kde chcete definovat vaše navigační trasy, nastavit zobrazení pro spuštění a provádět libovolné instalační a zaváděcí operace, jako je například vytváření dat aplikace.

`main.js` soubor definuje několik modulů durandal, které pomůžou aplikaci začít spouštět. Příkaz define pomáhá vyhodnotit závislosti modulů, aby byly k dispozici pro funkci. Nejprve jsou povoleny ladicí zprávy, které odesílají zprávy o událostech, které aplikace provádí v okně konzoly. Aplikace. Start Code instruuje durandal Framework pro spuštění aplikace. Konvence jsou nastaveny tak, aby durandal ví, že všechna zobrazení a ViewModels jsou obsaženy ve stejných pojmenovaných složkách v uvedeném pořadí. Nakonec `app.setRoot` načte `shell` pomocí předdefinované animace `entrance`.

[!code-javascript[Main](hottowel-template/samples/sample3.js)]

## <a name="views"></a>Zobrazení

Zobrazení se nacházejí ve složce `App/views`.

### <a name="shellhtml"></a>shell.html

`shell.html` obsahuje rozložení předlohy pro váš kód HTML. Všechna ostatní zobrazení se budou skládat někam do zobrazení `shell`. Hot navrhování ručníků poskytuje `shell` se třemi takovými oblastmi: záhlaví, oblast obsahu a zápatí. Každá z těchto oblastí je načtena s obsahem, který je v případě potřeby v jiných zobrazeních.

Vazby `compose` pro záhlaví a zápatí jsou pevně kódované v Hot navrhování ručníků, aby odkazovaly na zobrazení `nav` a `footer`, v uvedeném pořadí. Vazba pro psaní oddílu `#content` je vázána na aktivní položku modulu `router`. Jinými slovy, když kliknete na navigační odkaz, v této oblasti se načte odpovídající zobrazení.

[!code-html[Main](hottowel-template/samples/sample4.html)]

### <a name="navhtml"></a>nav.html

`nav.html` obsahuje navigační odkazy pro SPA. Zde lze umístit strukturu nabídky, například. Často se jedná o datovou vazbu (pomocí vykrojení) do modulu `router` pro zobrazení navigace, kterou jste definovali v `shell.js`. Vyseknutí vyhledá atributy vazby dat a váže je na `shell` ViewModel, aby zobrazila navigační trasy a zobrazila ProgressBar (pomocí služby Twitter Bootstrap), pokud je modul `router` uprostřed přechodu z jednoho zobrazení na jiný (viz `router.isNavigating`).

[!code-html[Main](hottowel-template/samples/sample5.html)]

### <a name="homehtml-and-detailshtml"></a>Home. html a details. html

Tato zobrazení obsahují HTML pro vlastní zobrazení. Pokud se klikne na odkaz `home` v nabídce zobrazení `nav`, bude zobrazení `home` umístěno v oblasti obsahu `shell` zobrazení. Tato zobrazení lze rozšířit nebo nahradit vlastními zobrazeními.

### <a name="footerhtml"></a>footer.html

`footer.html` obsahuje kód HTML, který se zobrazí v zápatí, v dolní části `shell` zobrazení.

## <a name="viewmodels"></a>ViewModels

ViewModels se nachází ve složce `App/viewmodels`.

### <a name="shelljs"></a>shell.js

`shell` ViewModel obsahuje vlastnosti a funkce, které jsou vázány na zobrazení `shell`. Často je to místo, kde se nacházejí navigační vazby nabídky (viz logika `router.mapNav`).

[!code-javascript[Main](hottowel-template/samples/sample6.js)]

### <a name="homejs-and-detailsjs"></a>Home. js a details. js

Tyto ViewModels obsahují vlastnosti a funkce, které jsou vázány na zobrazení `home`. obsahuje také logiku prezentace pro zobrazení a je připevněn mezi daty a zobrazením.

[!code-javascript[Main](hottowel-template/samples/sample7.js)]

## <a name="services"></a>Služby

Služby se nacházejí ve složce App/Services. V ideálním případě by bylo možné umístit budoucí služby, jako je například modul DataService, který je zodpovědný za získání a odeslání vzdálených dat.

### <a name="loggerjs"></a>logger.js

Hot navrhování ručníků poskytuje modul `logger` ve složce služby. Modul `logger` je ideální pro protokolování zpráv do konzoly a uživatele v překryvném okně informační zprávy.

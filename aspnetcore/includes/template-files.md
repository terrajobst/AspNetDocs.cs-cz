---
ms.openlocfilehash: eb2f83504129ae2b19ff5d85a2bc7d90293b43d6
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57071656"
---
* Startup.cs: [Počáteční třída](xref:fundamentals/startup) – třída nakonfiguruje kanál požadavku, která zpracovává všechny požadavky vytvořené pro aplikaci.
* Soubor program.cs: [Program třídy](xref:fundamentals/index) obsahující hlavní vstupní bod aplikace.
* firstapp.csproj : [Soubor projektu](/dotnet/articles/core/preview3/tools/csproj) formát souboru projektu nástroje MSBuild pro aplikace ASP.NET Core. Odkazy typu projekt na projekt, obsahuje odkazy na NuGet a další související položky projektu.
* appSettings.JSON / appsettings. Development.JSON: Soubor s nastavením konfigurace prostředí základní aplikace. [V tématu Konfigurace](xref:fundamentals/configuration/index).
* bower.json : Bower závislosti balíčků pro projekt.
* .bowerrc : Konfigurační soubor bower, který definuje vhodného místa pro instalaci součástí při stahování Bower prostředky.
* bundleconfig.JSON: konfigurační soubory pro sdružování a minifikace front-endových prostředků jazyka JavaScript a CSS.
* Zobrazení: Obsahuje zobrazení syntaxe Razor. Zobrazení jsou komponenty, které zobrazují aplikace uživatelského rozhraní (UI). Obecně platí toto uživatelské rozhraní zobrazí data modelu.
* Řadiče zařízení: Zpočátku obsahuje řadiče MVC *HomeController.cs*. Kontrolery jsou třídy, které zpracovávají požadavky prohlížeče.
* Wwwroot: Kořenovou složku webové aplikace.

Další informace najdete v části [vzor The MVC](xref:mvc/overview).

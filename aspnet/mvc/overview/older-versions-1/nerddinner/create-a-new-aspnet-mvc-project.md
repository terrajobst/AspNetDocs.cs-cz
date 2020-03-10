---
uid: mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
title: Vytvořit nový projekt ASP.NET MVC | Microsoft Docs
author: microsoft
description: V kroku 1 se dozvíte, jak umístit základní strukturu aplikace NerdDinner.
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 7e0e9928-8fdc-4b74-9882-55fac0976628
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-new-aspnet-mvc-project
msc.type: authoredcontent
ms.openlocfilehash: 189ddc187fc83db14106b2da199ba12a70a32b45
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580932"
---
# <a name="create-a-new-aspnet-mvc-project"></a>Vytvoření nového projektu ASP.NET MVC

od [Microsoftu](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 1 bezplatného [kurzu aplikace "NerdDinner"](introducing-the-nerddinner-tutorial.md) , který vás provede procesem vytvoření malé, ale dokončené webové aplikace pomocí ASP.NET MVC 1.
> 
> V kroku 1 se dozvíte, jak umístit základní strukturu aplikace NerdDinner.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme vám postupovat podle [Začínáme s kurzy pro](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [hudební úložiště](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) MVC 3 nebo MVC.

## <a name="nerddinner-step-1-file-gtnew-project"></a>NerdDinner krok 1: soubor –&gt;nový projekt

Aplikaci NerdDinner zahájíme tak, že vyberete položku nabídky **soubor&gt;nový projekt** v rámci sady visual Studio 2008 nebo Free Visual Web Developer 2008 Express.

Tím se zobrazí dialogové okno Nový projekt. Pokud chcete vytvořit novou aplikaci ASP.NET MVC, na levé straně dialogového okna vyberte uzel web a pak na pravé straně vyberte šablonu projektu webová aplikace ASP.NET MVC:

![](create-a-new-aspnet-mvc-project/_static/image1.png)

*Důležité: Ujistěte se, že jste stáhli a nainstalovali ASP.NET MVC – v opačném případě se nezobrazí v dialogovém okně Nový projekt. V2 [Instalace webové platformy Microsoft](https://www.microsoft.com/web/downloads/platform.aspx) můžete použít, pokud jste ho ještě nenainstalovali (ASP.NET MVC je k dispozici v části "webová platforma –&gt;architektury a moduly runtime").*

Pojmenujte nový projekt, který vytvoříme "NerdDinner" a potom kliknutím na tlačítko OK ho vytvoříte.

Po kliknutí na OK se zobrazí další dialogové okno s výzvou, aby bylo možné volitelně vytvořit projekt testování částí pro novou aplikaci. Tento projekt testů jednotek nám umožňuje vytvářet automatizované testy, které ověřují funkčnost a chování naší aplikace (něco si ukážeme, jak postupovat později v tomto kurzu).

![](create-a-new-aspnet-mvc-project/_static/image2.png)

V rozevíracím seznamu "testovací rozhraní" v rámci výše uvedeného dialogového okna se naplní všechny dostupné šablony projektů testu jednotek ASP.NET MVC nainstalované v počítači. Verze je možné stáhnout pro NUnit, MBUnit a XUnit. Podporuje se taky integrované rozhraní test Unit pro testování částí sady Visual Studio.

*Poznámka: rozhraní Visual Studio Unit Test Framework je k dispozici pouze v edici Visual Studio 2008 Professional a vyšších verzích. Pokud používáte VS 2008 Standard Edition nebo Visual Web Developer 2008 Express, budete si muset stáhnout a nainstalovat rozšíření NUnit, MBUnit nebo XUnit pro ASP.NET MVC, aby se toto dialogové okno zobrazilo. Dialogové okno se nezobrazí, pokud nejsou nainstalovány žádné testovací rozhraní.*

Pro testovací projekt, který vytvoříme, použijeme výchozí název "NerdDinner. Tests" a použijeme možnost rozhraní "test jednotek sady Visual Studio". Když klikneme na tlačítko OK, Visual Studio vytvoří řešení pro nás se dvěma projekty – jednu pro naši webovou aplikaci a jednu pro naše testy jednotek:

![](create-a-new-aspnet-mvc-project/_static/image3.png)

### <a name="examining-the-nerddinner-directory-structure"></a>Zkoumání struktury adresáře NerdDinner

Při vytváření nové aplikace ASP.NET MVC se sadou Visual Studio automaticky přidá do projektu řadu souborů a adresářů:

![](create-a-new-aspnet-mvc-project/_static/image4.png)

Projekty ASP.NET MVC mají ve výchozím nastavení šest adresářů nejvyšší úrovně:

| **Službě** | **Účel** |
| --- | --- |
| **/Controllers** | Kam vložíte třídy kontroleru, které zpracovávají požadavky URL |
| **/Models** | Kam vložíte třídy, které reprezentují a manipulují s daty |
| **/Views** | Kam vložíte soubory šablon uživatelského rozhraní, které jsou zodpovědné za vykreslování výstupu |
| **/Scripts** | Kam vložíte soubory knihovny JavaScriptu a skripty (. js) |
| **/Content** | Kam vložíte soubory CSS a obrázky a další nedynamický nebo nejavascriptový obsah |
| **Data\_/App** | Kam ukládáte datové soubory, které chcete číst a zapisovat. |

ASP.NET MVC nevyžaduje tuto strukturu. Vývojáři, kteří pracují na rozsáhlých aplikacích, obvykle rozdělí aplikaci na více projektů, aby ji bylo možné snadněji spravovat (například třídy datového modelu často přecházejí do samostatného projektu knihovny tříd z webové aplikace). Výchozí struktura projektu ale poskytuje dobrý výchozí adresářovou konvenci, kterou můžeme použít k vyčištění naší aplikace.

Po rozbalení adresáře/Controllers zjistíme, že Visual Studio přidalo dvě třídy kontroleru – HomeController a AccountController – ve výchozím nastavení do projektu:

![](create-a-new-aspnet-mvc-project/_static/image5.png)

Když rozšíříme adresář/views, najdete tři podsložky –/Home,/Account a/Shared – a do projektu se ve výchozím nastavení přidaly taky několik souborů šablon, které jsou v nich taky přidané:

![](create-a-new-aspnet-mvc-project/_static/image6.png)

Když rozbalíme adresáře/Content a/Scripts, zjistíme soubor Web. CSS, který se používá k vytvoření stylu HTML na webu, a také ke knihovnám JavaScriptu, které umožňují podporu ASP.NET AJAX a jQuery v rámci aplikace:

![](create-a-new-aspnet-mvc-project/_static/image7.png)

Když rozbalíte projekt NerdDinner. Tests, najdete dvě třídy, které obsahují testy jednotek pro naše třídy kontroleru:

![](create-a-new-aspnet-mvc-project/_static/image8.png)

Tyto výchozí soubory přidané sadou Visual Studio poskytují základní strukturu pro funkční aplikaci – dokončeno s domovskou stránkou, stránka, přihlašovací stránky/odhlášení/registrace účtu a Neošetřená chybová stránka (všechna drátová a funkční).

### <a name="running-the-nerddinner-application"></a>Spuštění aplikace NerdDinner

Projekt můžeme spustit tak, že vyberete buď ladění **&gt;spustit ladění** nebo **ladění –&gt;spustit bez ladění** položek nabídky:

![](create-a-new-aspnet-mvc-project/_static/image9.png)

Tím se spustí integrovaný webový server ASP.NET, který je součástí sady Visual Studio, a spusťte naši aplikaci:

![](create-a-new-aspnet-mvc-project/_static/image10.png)

Níže je Domovská stránka našeho nového projektu (adresa URL: "/") při spuštění:

![](create-a-new-aspnet-mvc-project/_static/image11.png)

Kliknutím na kartu o se zobrazí stránka about (adresa URL: "/Home/About"):

![](create-a-new-aspnet-mvc-project/_static/image12.png)

Kliknutím na odkaz přihlásit v pravém horním rohu se dostanete na přihlašovací stránku (adresa URL: "/Account/LogOn").

![](create-a-new-aspnet-mvc-project/_static/image13.png)

Pokud nemáme přihlašovací účet, můžeme kliknout na odkaz zaregistrovat (URL: "/Account/Register") a vytvořit ho:

![](create-a-new-aspnet-mvc-project/_static/image14.png)

Kód, který implementuje výše uvedenou funkci domů, o a odhlášení nebo registrace, se ve výchozím nastavení přidal, když jsme vytvořili náš nový projekt. Použijeme ho jako výchozí bod naší aplikace.

### <a name="testing-the-nerddinner-application"></a>Testování aplikace NerdDinner

Pokud používáme edici Professional nebo vyšší verze sady Visual Studio 2008, můžeme použít integrovanou podporu IDE pro testování částí v rámci sady Visual Studio k otestování projektu:

![](create-a-new-aspnet-mvc-project/_static/image15.png)

Když vyberete jednu z výše uvedených možností, otevře se v prostředí IDE podokno "Výsledky testů" a poskytneme nám stav úspěch/selhání na 27 jednotkových testů, které jsou součástí našeho nového projektu, který se zabývá integrovanými funkcemi:

![](create-a-new-aspnet-mvc-project/_static/image16.png)

Později v tomto kurzu budeme hovořit o automatizovaném testování a přidat další testy jednotek, které pokrývají funkčnost aplikace, kterou implementujeme.

### <a name="next-step"></a>Další krok

Teď máme základní strukturu aplikace. Teď [vytvoříme databázi, do které se budou ukládat data aplikací](create-a-database.md).

> [!div class="step-by-step"]
> [Předchozí](introducing-the-nerddinner-tutorial.md)
> [Další](create-a-database.md)

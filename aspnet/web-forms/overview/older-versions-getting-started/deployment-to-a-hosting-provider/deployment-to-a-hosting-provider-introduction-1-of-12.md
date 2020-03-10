---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
title: 'Nasazení webové aplikace v ASP.NET s SQL Server Compact pomocí sady Visual Studio: Úvod – 1 z 12 | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a2d7f33b-8c4a-4b48-9fb1-9139cf9b9878
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12
msc.type: authoredcontent
ms.openlocfilehash: ea88da1e6d510f706fc7ca370cfa32974c1243f8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525632"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-introduction---1-of-12"></a>Nasazení webové aplikace v ASP.NET s SQL Server Compact pomocí sady Visual Studio: Úvod – 1 z 12

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Studio 2012 RC nebo Visual Studio Express 2012 RC pro web. Můžete také použít Visual Studio 2010, pokud nainstalujete aktualizaci publikování na webu.
> 
> Kurz, který ukazuje funkce nasazení představené po vydání RC sady Visual Studio 2012, ukazuje, jak nasadit SQL Server edice jiné než SQL Server Compact a ukazuje, jak nasadit na Azure App Service Web Apps, v tématu [nasazení webu ASP.NET pomocí sady Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).
> 
> Tyto kurzy vás provedou nasazením služby IIS na místním vývojovém počítači pro testování a pak poskytovateli hostování třetí strany. Aplikace, kterou nasadíte, používá aplikační databázi a databázi členství v ASP.NET. Začnete s používáním SQL Server Compact a nasazením do SQL Server Compact a později se dozvíte, jak nasadit změny databáze a jak migrovat na SQL Server.
> 
> Kurzy předpokládají, jak pracovat s ASP.NET v aplikaci Visual Studio. Pokud to neuděláte, dobrým místem, kde začít, je [Základní kurz pro webové formuláře v ASP.NET](../tailspin-spyworks/tailspin-spyworks-part-1.md) nebo [základní kurz pro ASP.NET MVC](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md).
> 
> Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra nasazení ASP.NET](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment).

## <a name="overview"></a>Přehled

Tyto kurzy vás provedou nasazením služby IIS na místním vývojovém počítači pro testování a pak poskytovateli hostování třetí strany. Aplikace, kterou nasadíte, používá aplikační databázi a databázi členství v ASP.NET. Začnete s používáním SQL Server Compact a nasazením do SQL Server Compact a později se dozvíte, jak nasadit změny databáze a jak migrovat na SQL Server.

Počet kurzů – 11 na všech Plus na stránce Poradce při potížích – může vést k tomu, že se proces nasazení zdá těžké. Základní postupy pro nasazení lokality tvoří poměrně malou část sady kurzů. V reálných situacích ale často potřebujete informace o některých malých, ale důležitých aspektech nasazení, například o nastavení oprávnění složky na cílovém serveru. Do těchto výukových kurzů jsme zahrnuli spoustu těchto dalších technik. doufáme, že kurzy neopustí informace, které by vám mohly zabránit v úspěšném nasazení reálné aplikace.

Kurzy jsou navržené tak, aby běžely v pořadí, a každá část sestavuje v předchozí části. Můžete však přeskočit části, které nejsou relevantní pro vaši situaci. (Přeskočení částí může vyžadovat úpravu postupů v pozdějších kurzech.)

## <a name="intended-audience"></a>Zamýšlená cílová skupina

Kurzy jsou zaměřené na ASP.NET vývojářů, kteří pracují v malých organizacích nebo v jiných prostředích, kde:

- Proces průběžné integrace (automatizované sestavení a nasazení) se nepoužívá.
- Produkční prostředí je poskytovatel hostingu třetí strany.
- Jedna osoba obvykle vyplní více rolí (stejná osoba se vyvíjí, testuje a nasazuje).

V podnikových prostředích je obvyklejší implementovat procesy kontinuální integrace a provozní prostředí je obvykle hostováno vlastními servery společnosti. Různí lidé také obvykle provádějí různé role. Informace o podnikovém nasazení najdete v tématu [nasazení webových aplikací v podnikových scénářích](../../deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md).

Organizace všech velikostí můžou nasadit taky webové aplikace do Azure a většina postupů uvedených v těchto kurzech se vztahuje také na Azure App Services Web Apps. Úvod do Azure najdete v tématu [https://azure.microsoft.com](https://azure.microsoft.com).

## <a name="the-hosting-provider-shown-in-the-tutorials"></a>Poskytovatel hostingu zobrazený v kurzech

Kurzy vás provedou procesem vytvoření účtu s hostující firmou a nasazením aplikace do tohoto poskytovatele hostingu. Zvolili jste konkrétní hostingovou společnost, která by kurzy mohla Ukázat na ucelené možnosti nasazení na živý Web. Každá hostující společnost poskytuje různé funkce a prostředí nasazení na jejich servery se trochu liší. proces popsaný v tomto kurzu je ale typický pro celý proces.

Poskytovatel hostingu, který se používá pro účely tohoto kurzu, Cytanium.com, je jedním z mnoha dostupných a jeho použití v tomto kurzu nepředstavuje potvrzení ani doporučení.

## <a name="deploying-web-site-projects"></a>Nasazení projektů webu

Contoso University je projekt webové aplikace Visual Studio. Většina metod nasazení a nástrojů, které jsou znázorněné v tomto kurzu, se nevztahují na [projekty](https://msdn.microsoft.com/library/dd547590.aspx)webu. Informace o nasazení projektů webu najdete v tématu [Mapa obsahu nasazení ASP.NET](https://msdn.microsoft.com/library/bb386521.aspx#deployment_for_web_site_projects).

## <a name="deploying-aspnet-mvc-projects"></a>Nasazení projektů ASP.NET MVC

V tomto kurzu nasadíte projekt webových formulářů ASP.NET, ale všechno, co se naučíte, se vztahuje také na ASP.NET MVC. Projekt sady Visual Studio MVC je pouze další forma projektu webové aplikace. Jediným rozdílem je to, že pokud nasazujete pro poskytovatele hostingu, který nepodporuje ASP.NET MVC nebo cílovou verzi, musíte se ujistit, že máte v projektu nainstalovaný příslušný balíček NuGet ([MVC 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0) nebo [MVC 4](http://nuget.org/packages/aspnetmvc)).

## <a name="programming-language"></a>Programovací jazyk

Ukázková aplikace používá C# C#, ale kurzy nevyžadují znalosti a techniky nasazení zobrazené kurzy nejsou specifické pro jazyk.

## <a name="troubleshooting-during-this-tutorial"></a>Řešení potíží během tohoto kurzu

Pokud během nasazení dojde k chybě nebo pokud nasazená lokalita neběží správně, chybové zprávy vždy neposkytují řešení. Pro pomoc s některými běžnými scénáři problémů je k dispozici [referenční stránka pro řešení potíží](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md) . Pokud obdržíte chybovou zprávu nebo něco nefunguje při procházení kurzů, nezapomeňte na stránku Poradce při potížích.

## <a name="comments-welcome"></a>Komentáře – Vítejte

Komentáře k kurzům jsou úvodní a při aktualizaci tohoto kurzu se budou brát v úvahu opravy nebo návrhy na vylepšení, která jsou k dispozici v komentářích kurzu.

## <a name="prerequisites"></a>Předpoklady

Než začnete, ujistěte se, že máte v počítači nainstalovaný systém Windows 7 nebo novější a jeden z následujících produktů:

- [Visual Studio 2010 SP1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)
- [Visual Web Developer Express 2010 SP1](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VWD2010SP1Pack)
- [Visual Studio 2012 RC nebo Visual Studio Express 2012 RC for Web](https://go.microsoft.com/fwlink/?LinkId=240162)

Pokud máte Visual Studio 2010 SP1 nebo Visual Web Developer Express 2010 SP1, nainstalujte také následující produkty:

- [Azure SDK pro .NET (VS 2010 SP1)](https://go.microsoft.com/fwlink/?LinkID=208120) (zahrnuje aktualizaci publikování na webu)
- [Nástroje Microsoft Visual Studio 2010 SP1 pro SQL Server Compact 4,0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCEVSTools)

K dokončení tohoto kurzu je nutný nějaký jiný software, ale není nutné, abyste ho načetli ještě předtím. Tento kurz vás provede kroky potřebnými k jeho instalaci, když ho potřebujete.

## <a name="downloading-the-sample-application"></a>Stahuje se ukázková aplikace.

Aplikace, kterou nasadíte, se jmenuje contoso University a už se pro vás vytvořila. Jedná se o zjednodušenou verzi webu na univerzitě, která je založená na společnosti Contoso, která je popsaná v [Entity Framework kurzech na webu ASP.NET](https://asp.net/entity-framework/tutorials).

Když máte nainstalované požadované součásti, Stáhněte si [webovou aplikaci Contoso University](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b). Soubor *. zip* obsahuje několik verzí projektu a soubor PDF, který obsahuje všechny 12 kurzů. K provedení kroků v tomto kurzu začněte ContosoUniversity-Begin. Chcete-li zjistit, co projekt vypadá na konci kurzů, otevřete ContosoUniversity-end. Pokud chcete zjistit, co projekt vypadá před migrací na plnou SQL Server v kurzu 10 otevřete ContosoUniversity-AfterTutorial09.

Pro přípravu na práci v rámci kroků kurzu uložte ContosoUniversity – začněte do jakékoli složky, kterou používáte pro práci s projekty sady Visual Studio. Ve výchozím nastavení je to tato složka:

`C:\Users\<username>\Documents\Visual Studio 2012\Projects`

(Pro snímky obrazovky v tomto kurzu se složka projektu nachází v kořenovém adresáři na `C`: jednotka).

Spusťte Visual Studio, otevřete projekt a stisknutím klávesy CTRL + F5 ho spusťte.

[![Home_page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image2.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image1.png)

Stránky webu jsou přístupné z řádku nabídek a umožňují vám provádět následující funkce:

- Zobrazit údaje o studentovi (stránka o produktu).
- Zobrazovat, upravovat, odstraňovat a přidávat studenty.
- Zobrazení a úpravy kurzů.
- Zobrazit a upravit instruktory.
- Zobrazit a upravit oddělení.

Níže jsou uvedené snímky obrazovky s několika reprezentativními stránkami.

[![Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image4.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image3.png)

[![Add_Students_Page](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image6.png)](deployment-to-a-hosting-provider-introduction-1-of-12/_static/image5.png)

## <a name="reviewing-application-features-that-affect-deployment"></a>Kontrola funkcí aplikace, které mají vliv na nasazení

Následující funkce aplikace mají vliv na jejich nasazení nebo na to, co musíte udělat, abyste je nasadili. Každá z nich je podrobněji vysvětlena v následujících kurzech v řadě.

- Společnost Contoso University používá k ukládání dat aplikací, jako jsou názvy studentů a instruktorů, databázi SQL Server Compact. Databáze obsahuje kombinaci testovacích dat a produkčních dat a při nasazení do produkčního prostředí potřebujete vyloučit testovací data. Později v sérii kurzů migrujete z SQL Server Compact na SQL Server.
- Aplikace používá ASP.NET systém členství, který ukládá informace o uživatelském účtu do SQL Server Compact databáze. Aplikace definuje uživatele správce, který má přístup k některým omezeným informacím. Je nutné nasadit databázi členství bez testovacích účtů, ale s jedním účtem správce.
- Vzhledem k tomu, že aplikační databáze a databáze členství používají SQL Server Compact jako databázový stroj, je nutné nasadit databázový stroj do poskytovatele hostingu i samotných databází.
- Aplikace používá ASP.NET univerzálního poskytovatele členství, aby systém členství mohl ukládat svá data do databáze SQL Server Compact. Sestavení obsahující poskytovatele univerzálních členství musí být nasazeno spolu s aplikací.
- Aplikace používá Entity Framework 5,0 pro přístup k datům v databázi aplikace. Sestavení obsahující Entity Framework 5,0 musí být nasazeno spolu s aplikací.
- Aplikace používá protokolování chyb a nástroj pro generování sestav třetí strany. Tento nástroj je k dispozici v sestavení, které musí být nasazeno s aplikací.
- Nástroj pro protokolování chyb zapisuje informace o chybě do souborů XML do složky souborů. Musíte zajistit, aby účet, ke kterému ASP.NET běžet v nasazeném webu, měl oprávnění k zápisu do této složky a Vy musíte tuto složku z nasazení vyloučit. (Jinak se můžou odstranit data protokolu chyb z testovacího prostředí do produkčního nebo produkčního souboru protokolu chyb.)
- Aplikace zahrnuje některá nastavení, která je nutné změnit v nasazeném souboru *Web. config* v závislosti na cílovém prostředí (testování nebo produkční), a dalších nastaveních, která je nutné změnit v závislosti na konfiguraci sestavení (ladění nebo vydání).
- Řešení sady Visual Studio zahrnuje projekt knihovny tříd. Je třeba nasadit pouze sestavení, které tento projekt vygeneruje, ne samotný projekt.

V tomto prvním kurzu v řadě jste stáhli vzorový projekt sady Visual Studio a zkontrolovali funkce lokality, které mají vliv na nasazení aplikace. V následujících kurzech se připravíte na nasazení tím, že nastavíte některé z těchto akcí, které se mají automaticky zpracovat. Ostatní uživatelé se postarou o ruční provedení.

> [!div class="step-by-step"]
> [Next](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)

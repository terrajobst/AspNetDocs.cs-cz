---
uid: web-forms/overview/deployment/visual-studio-web-deployment/introduction
title: 'ASP.NET nasazení webu pomocí sady Visual Studio: Úvod | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci v ASP.NET pro Azure App Service Web Apps nebo poskytovatele hostingu třetí strany pomocí V...
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 24ad086d-865e-433c-9ac9-05f1a553da16
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/introduction
msc.type: authoredcontent
ms.openlocfilehash: 96dd31d949633e001fc595621bedbf74e98000fc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640240"
---
# <a name="aspnet-web-deployment-using-visual-studio-introduction"></a>Nasazení webu ASP.NET pomocí sady Visual Studio: Úvod

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci v ASP.NET pro Azure App Service Web Apps nebo poskytovatele hostování třetí strany pomocí sady Visual Studio 2012 se sadou Azure SDK pro .NET. Většina postupů je obdobná pro Visual Studio 2013.
> 
> Vyvíjíte webovou aplikaci, aby ji uživatelé mohli zpřístupnit prostřednictvím Internetu. Nicméně kurzy pro webové programování se obvykle zastaví, jakmile se zobrazí, jak na vývojovém počítači něco pracovat. Tato série kurzů začíná, kde ostatní odejdou: právě jste vytvořili webovou aplikaci, otestovali ji a je připravená k použití. Co dál? V těchto kurzech se dozvíte, jak nejdřív nasadit službu IIS na místním vývojovém počítači pro účely testování a potom do Azure nebo poskytovatele hostování třetí strany pro přípravu a výrobu. Ukázková aplikace, kterou nasadíte, je projekt webové aplikace, který používá Entity Framework, SQL Server a systém členství v ASP.NET. Ukázková aplikace používá webové formuláře ASP.NET, ale uvedené postupy platí také pro ASP.NET MVC a webové rozhraní API.
> 
> V těchto kurzech se předpokládá, jak pracovat s ASP.NET v aplikaci Visual Studio. Pokud to neuděláte, dobrým místem, kde začít, je [Základní kurz pro webové formuláře v ASP.NET](../../older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1.md) nebo [základní kurz pro ASP.NET MVC](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md).
> 
> Pokud máte dotazy, které přímo nesouvisejí s kurzem, můžete je publikovat do [fóra nasazení ASP.NET](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) nebo [StackOverflow](http://stackoverflow.com).
> 
> Tento obsah je také k dispozici jako bezplatná elektronická kniha v [galerii e-knih TechNet](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#ASPNETWebDeploymentusingVisualStudio).

## <a name="overview"></a>Přehled

Tyto kurzy vás provedou nasazením webové aplikace v ASP.NET, která zahrnuje databáze SQL Server. Nejdříve se nasadíte do služby IIS na místním vývojovém počítači pro účely testování a pak Web Apps v Azure App Service a Azure SQL Database pro přípravu a produkci. Uvidíte, jak nasadit pomocí nástroje Visual Studio pro publikování jedním kliknutím a uvidíte, jak nasadit pomocí příkazového řádku.

Počet kurzů může mít za to, že se proces nasazení jeví jako těžkéý. Základní postupy jsou ve skutečnosti jednoduché. V reálných situacích ale často potřebujete provádět dodatečné úlohy nasazení – například nastavení oprávnění složky na cílovém serveru. Provedli jsme některé z těchto dalších úkolů, a to v případě, že vám kurzy nenechají informace, které by vám mohly zabránit v úspěšném nasazení skutečné aplikace.

Kurzy jsou navržené tak, aby běžely v pořadí, a každá část sestavuje v předchozí části. Můžete přeskočit části, které nejsou relevantní pro vaši situaci, ale možná budete muset upravit postupy v pozdějších kurzech.

## <a name="intended-audience"></a>Zamýšlená cílová skupina

Kurzy jsou zaměřené na ASP.NET vývojářů, kteří pracují v prostředích, kde:

- Provozní prostředí je Azure App Service Web Apps nebo poskytovatel hostingu třetí strany.
- Nasazení není omezeno na proces průběžné integrace, ale může být provedeno přímo ze sady Visual Studio.

Nasazení ze [správy zdrojového kódu](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md) pomocí procesu [průběžného doručování](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) se v těchto kurzech nezabývá s výjimkou jednoho kurzu, který ukazuje, jak nasadit z příkazového řádku. Informace o průběžném doručování najdete v následujících zdrojích informací:

- [Průběžná integrace a průběžné doručování (vytváření skutečných cloudových aplikací s využitím Windows Azure)](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)
- [Nasazení webové aplikace v Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-deploy/)
- [Nasazení webových aplikací v podnikových scénářích](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md) (starší sada kurzů napsaných pro Visual Studio 2010, které mají stále užitečné informace pro podniková prostředí.)

## <a name="using-a-third-party-hosting-provider"></a>Použití poskytovatele hostování třetí strany

Kurzy vás provedou procesem nastavení účtu Azure a nasazením aplikace, aby Web Apps v Azure App Service pro přípravu a produkci. Můžete ale použít stejné základní postupy pro nasazení poskytovatele hostování třetí strany podle vašeho výběru. Tam, kde kurzy přecházejí na procesy, které jsou v Azure jedinečné, vysvětlují, jaké rozdíly můžete očekávat od poskytovatele hostingu třetích stran.

## <a name="deploying-web-app-projects"></a>Nasazení projektů webové aplikace

Ukázková aplikace, kterou stáhnete a nasadíte pro tyto kurzy, je projekt webové aplikace Visual Studio. Pokud však nainstalujete nejnovější aktualizaci web Publish pro Visual Studio, můžete použít stejné metody nasazení a nástroje pro projekty webových aplikací.

## <a name="deploying-aspnet-mvc-projects"></a>Nasazení projektů ASP.NET MVC

Ukázková aplikace je projekt webových formulářů ASP.NET, ale všechno, co se naučíte udělat, se vztahuje také na ASP.NET MVC. Projekt sady Visual Studio MVC je pouze další forma projektu webové aplikace. Jediným rozdílem je to, že pokud nasazujete pro poskytovatele hostingu, který nepodporuje ASP.NET MVC nebo cílovou verzi, musíte se ujistit, že jste v projektu nainstalovali příslušný balíček NuGet ([MVC 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0), [MVC 4](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/4.0.30506.0)nebo [MVC 5](http://www.nuget.org/packages/Microsoft.AspNet.Mvc)).

## <a name="programming-language"></a>Programovací jazyk

Ukázková aplikace používá C# C#, ale kurzy nevyžadují znalosti a techniky nasazení zobrazené kurzy nejsou specifické pro jazyk.

## <a name="database-deployment-methods"></a>Metody nasazení databáze

Existují tři způsoby, jak můžete nasadit databázi SQL Server společně s nasazením webu v aplikaci Visual Studio:

- Migrace Entity Framework Code First
- Poskytovatel Nasazení webu dbDacFx
- Poskytovatel Nasazení webu dbFullSql

V tomto kurzu použijete první dvě z těchto metod. Zprostředkovatel dbFullSql Nasazení webu je starší metoda, která se už nedoporučuje, s výjimkou některých specifických scénářů, jako je třeba migrace z SQL Server Compact na SQL Server.

Metody uvedené v tomto kurzu jsou pro databáze SQL Server, ne SQL Server Compact. Informace o tom, jak nasadit databázi SQL Server Compact, najdete v tématu [nasazení webu pomocí sady Visual Studio s SQL Server Compact](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md).

Metody uvedené v tomto kurzu vyžadují, abyste použili metodu Nasazení webu publikovat. Pokud upřednostňujete jinou metodu publikování, třeba FTP, souborový systém nebo rozšíření FPSE, přečtěte si téma [nasazení databáze odděleně od nasazení webové aplikace](https://go.microsoft.com/fwlink/p/?LinkId=282413#databaseseparate) v mapě obsahu nasazení webu pro Visual Studio a ASP.NET.

### <a name="entity-framework-code-first-migrations"></a>Migrace Entity Framework Code First

V Entity Framework verze 4,3 Společnost Microsoft představila Migrace Code First. Migrace Code First automatizuje proces provádění přírůstkových změn v datovém modelu a šíření těchto změn do databáze. V dřívějších verzích Code First obvykle můžete Entity Framework vyřadit a znovu vytvořit databázi pokaždé, když změníte datový model. Nejedná se o problém při vývoji, protože testovací data se snadno znovu vytvoří, ale v produkčním prostředí byste obvykle chtěli aktualizovat schéma databáze bez vyřazení databáze. Funkce migrace umožňuje Code First aktualizovat databázi, aniž by byla vyhozena a znovu vytvořena. Můžete nechat Code First automaticky rozhodnout, jak provést požadované změny schématu, nebo můžete napsat kód, který upraví změny. Úvod do Migrace Code First najdete v tématu [migrace Code First](https://msdn.microsoft.com/library/hh770484.aspx).

Při nasazení webového projektu může Visual Studio automatizovat proces nasazení databáze spravované pomocí Migrace Code First. Při vytváření profilu publikování zaškrtněte políčko, které je označeno jako spouštěné Migrace Code First (spouští při spuštění aplikace). Toto nastavení způsobí, že proces nasazení automaticky konfiguruje soubor Web. config aplikace na cílovém serveru tak, aby Code First používal třídu inicializátoru `MigrateDatabaseToLatestVersion`.

Aplikace Visual Studio během procesu nasazení neprovede žádné akce s databází. Když nasazená aplikace přistupuje k databázi poprvé po nasazení, Code First automaticky vytvoří databázi nebo aktualizuje schéma databáze na nejnovější verzi. Pokud aplikace implementuje metodu počátečních hodnot migrace, metoda se spustí po vytvoření databáze nebo aktualizaci schématu.

V tomto kurzu použijete Migrace Code First k nasazení aplikační databáze.

### <a name="the-dbdacfx-web-deploy-provider"></a>Poskytovatel Nasazení webu dbDacFx

Pro databázi SQL Server, která není spravovaná pomocí Entity Framework Code First, můžete zaškrtnout políčko, které je označeno jako aktualizace databáze při konfiguraci publikačního profilu. Při počátečním nasazení vytvoří poskytovatel dbDacFx tabulky a další databázové objekty v cílové databázi tak, aby odpovídaly zdrojové databázi. V následných nasazeních určí poskytovatel, co se liší mezi zdrojovou a cílovou databází, a aktualizuje schéma cílové databáze tak, aby odpovídalo zdrojové databázi. Ve výchozím nastavení zprostředkovatel neprovede žádné změny, které způsobují ztrátu dat, například při vyřazení tabulky nebo sloupce.

Tato metoda neautomatizuje nasazení dat v databázových tabulkách, ale můžete vytvořit skripty, které to uděláte, a nakonfigurovat sadu Visual Studio tak, aby je spouštěla během nasazení. Dalším důvodem ke spouštění skriptů během nasazení je provedení změn schématu, které nelze provést automaticky, protože by to způsobilo ztrátu dat.

V tomto kurzu použijete poskytovatele dbDacFx k nasazení databáze členství ASP.NET.

## <a name="troubleshooting-during-this-tutorial"></a>Řešení potíží během tohoto kurzu

Pokud během nasazení dojde k chybě nebo pokud nasazená lokalita neběží správně, chybové zprávy vždy neposkytují zjevné řešení. Pro pomoc s některými běžnými scénáři problémů je k dispozici [referenční stránka pro řešení potíží](troubleshooting.md) . Pokud obdržíte chybovou zprávu nebo něco nefunguje při procházení kurzů, nezapomeňte na stránku Poradce při potížích.

## <a name="comments-welcome"></a>Komentáře – Vítejte

Komentáře k kurzům jsou úvodní a při aktualizaci tohoto kurzu se budou brát v úvahu opravy nebo návrhy na vylepšení, která jsou k dispozici v komentářích kurzu.

<a id="prerequisites"></a>

## <a name="prerequisites"></a>Požadavky

Tento kurz byl napsán pro následující produkty:

- Windows 8 nebo Windows 7.
- Visual Studio 2012 nebo Visual Studio 2012 Express pro web s [nejnovější aktualizací](https://go.microsoft.com/fwlink/?LinkId=272486)
- [Sada Azure SDK pro Visual Studio 2012](https://go.microsoft.com/fwlink/?LinkId=254364)

Můžete postupovat podle kurzu pomocí sady Visual Studio 2010 SP1 nebo Visual Studio 2013, ale některé snímky obrazovky se budou lišit a některé funkce se budou lišit.

Pokud používáte Visual Studio 2013, nainstalujte [sadu Azure SDK pro Visual Studio 2013](https://go.microsoft.com/fwlink/?LinkID=324322).

Pokud používáte Visual Studio 2010 SP1, nainstalujte následující software:

- [Sada Azure SDK pro Visual Studio 2010](https://go.microsoft.com/fwlink/?LinkID=254269)
- [SQL Server Express LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=SQLLocalDBOnly_11_0)
- [SQL Server Data Tools](https://msdn.microsoft.com/library/hh500335.aspx).

V závislosti na tom, kolik závislostí sady SDK už na počítači máte, může instalace sady Azure SDK trvat dlouhou dobu, od několika minut až po půl hodiny. Sadu Azure SDK budete potřebovat i v případě, že plánujete publikovat jako poskytovatele hostování třetí strany místo do Azure, protože sada SDK obsahuje nejnovější aktualizace funkcí publikování na webu sady Visual Studio.

> [!NOTE]
> Tento kurz byl napsán s 1.8.1 verzí sady Azure SDK. Od té doby byly vydány novější verze s dalšími funkcemi. Kurzy byly aktualizovány, aby uváděly tyto funkce a propojí se s prostředky, které obsahují další informace o těchto funkcích.

Pokyny a snímky obrazovky jsou založené na systému Windows 8, ale kurzy vysvětlují rozdíly v systému Windows 7.

K dokončení tohoto kurzu je nutný nějaký jiný software, ale není nutné, aby se nainstaloval ještě. Tento kurz vás provede kroky potřebnými k jeho instalaci, když ho potřebujete.

## <a name="download-the-sample-application"></a>Stažení ukázkové aplikace

Aplikace, kterou nasadíte, se jmenuje contoso University a už se pro vás vytvořila. Jedná se o zjednodušenou verzi webu na univerzitě, která je založená na společnosti Contoso, která je popsaná v [Entity Framework kurzech na webu ASP.NET](https://asp.net/entity-framework/tutorials).

Když máte nainstalované požadované součásti, Stáhněte si [webovou aplikaci Contoso University](https://go.microsoft.com/fwlink/p/?LinkId=282627). Soubor *. zip* obsahuje více verzí projektu. K provedení kroků v tomto kurzu začněte s projektem umístěným ve C# složce. Chcete-li zjistit, co projekt vypadá na konci kurzů, otevřete projekt ve složce ContosoUniversity-end.

K přípravě projektu pro práci v rámci kroků kurzu proveďte následující kroky:

1. Uložte soubory řešení ContosoUniversity ze C# složky ve složce s názvem ContosoUniversity v jakékoli složce, kterou používáte pro práci s projekty sady Visual Studio.

    Ve výchozím nastavení je to následující složka pro Visual Studio 2012:

    `C:\Users\<username>\Documents\Visual Studio 2012\Projects`

    (Pro snímky obrazovky v tomto kurzu se složka projektu nachází v kořenovém adresáři na `C`: jednotka).
2. Spusťte Visual Studio a otevřete projekt.
3. V **Průzkumník řešení**klikněte pravým tlačítkem na řešení a potom klikněte na **EnableNuGetovat balíček obnovit**.
4. Sestavte řešení.
5. Pokud se zobrazí chyby kompilace, ručně obnovte balíčky NuGet:

    1. V **Průzkumník řešení**klikněte pravým tlačítkem na řešení a potom klikněte na **Spravovat balíčky NuGet pro řešení**.
    2. V horní části dialogového okna **Spravovat balíčky NuGet** **se v tomto řešení nezobrazí některé balíčky NuGet. Kliknutím obnovíte.** Klikněte na tlačítko **obnovit** .
    3. Znovu sestavte řešení.
6. Spusťte aplikaci stisknutím kombinace kláves CTRL + F5.

    Aplikace se otevře na domovské stránce společnosti Contoso University.

    ![Vývoj domovské stránky](introduction/_static/image1.png)

    (V době, kdy Visual Studio spouští instanci SQL Server Express LocalDB, může dojít k čekací době, a pokud tento proces trvá příliš dlouho, může se zobrazit chyba časového limitu. V takovém případě stačí znovu spustit projekt.)

Stránky webu jsou přístupné z řádku nabídek a umožňují vám provádět následující funkce:

- Zobrazit údaje o studentovi (stránka o produktu).
- Zobrazovat, upravovat, odstraňovat a přidávat studenty.
- Zobrazení a úpravy kurzů.
- Zobrazit a upravit instruktory.
- Zobrazit a upravit oddělení.

Níže jsou uvedené snímky obrazovky s několika reprezentativními stránkami.

![Vývojové stránky studentů](introduction/_static/image2.png)

![Přidat vývojové stránky studentů](introduction/_static/image3.png)

## <a name="review-application-features-that-affect-deployment"></a>Kontrola funkcí aplikace, které mají vliv na nasazení

Následující funkce aplikace mají vliv na jejich nasazení nebo na to, co musíte udělat, abyste je nasadili. Každá z nich je podrobněji vysvětlena v následujících kurzech v řadě.

- Společnost Contoso University používá k ukládání dat aplikací, jako jsou názvy studentů a instruktorů, databázi SQL Server. Databáze obsahuje kombinaci testovacích dat a produkčních dat a při nasazení do produkčního prostředí potřebujete vyloučit testovací data.
- Aplikace používá ASP.NET systém členství, který ukládá informace o uživatelském účtu do SQL Server databáze. Aplikace definuje uživatele správce, který má přístup k některým omezeným informacím. Je nutné nasadit databázi členství bez testovacích účtů, ale s účtem správce.
- Aplikace používá protokolování chyb a nástroj pro generování sestav třetí strany. Tento nástroj je k dispozici v sestavení, které musí být nasazeno s aplikací.
- Nástroj pro protokolování chyb zapisuje informace o chybě do souborů XML do složky souborů. Musíte zajistit, aby účet, ke kterému ASP.NET běžet v nasazeném webu, měl oprávnění k zápisu do této složky a Vy musíte tuto složku z nasazení vyloučit. (Jinak se můžou odstranit data protokolu chyb z testovacího prostředí do produkčního nebo produkčního souboru protokolu chyb.)
- Aplikace zahrnuje některá nastavení, která je nutné změnit v nasazeném souboru *Web. config* v závislosti na cílovém prostředí (test, fázování nebo produkční), a dalších nastaveních, která je nutné změnit v závislosti na konfiguraci sestavení (ladění nebo vydání).
- Řešení sady Visual Studio zahrnuje projekt knihovny tříd. Je třeba nasadit pouze sestavení, které tento projekt vygeneruje, ne samotný projekt.

## <a name="summary"></a>Přehled

V tomto prvním kurzu v řadě jste stáhli vzorový projekt sady Visual Studio a zkontrolovali funkce lokality, které mají vliv na nasazení aplikace. V následujících kurzech se připravíte na nasazení tím, že nastavíte některé z těchto akcí, které se mají automaticky zpracovat. Ostatní uživatelé se postarou o ruční provedení.

> [!div class="step-by-step"]
> [Next](preparing-databases.md)

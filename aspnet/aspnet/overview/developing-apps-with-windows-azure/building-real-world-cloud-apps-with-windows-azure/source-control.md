---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
title: Správa zdrojového kódu (vytváření skutečných cloudových aplikací s Azure) | Microsoft Docs
author: MikeWasson
description: Vytváření reálných cloudových aplikací pomocí Azure je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které mohou...
ms.author: riande
ms.date: 06/23/2015
ms.assetid: 2a0370d3-c2fb-4bf3-88b8-aad5a736c793
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control
msc.type: authoredcontent
ms.openlocfilehash: a6f445e46d41b646cf6c25af2e65bc73e831d5ed
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74583701"
---
# <a name="source-control-building-real-world-cloud-apps-with-azure"></a>Správa zdrojového kódu (vytváření skutečných cloudových aplikací s Azure)

[Jan Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Dykstra](https://github.com/tdykstra)

[Stažení opravy projektu IT](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stažení elektronické knihy](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **Vytváření reálných cloudových aplikací pomocí Azure** je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které vám pomůžou úspěšně vyvíjet webové aplikace pro Cloud. Informace o elektronické příručce najdete v [první kapitole](introduction.md).

Správa zdrojového kódu je zásadní pro všechny projekty vývoje v cloudu, ne jenom pro Týmová prostředí. Nemůžete si představit, že upravíte zdrojový kód nebo dokonce i wordový dokument bez funkce vrácení a automatického zálohování, a Správa zdrojového kódu poskytuje tyto funkce na úrovni projektu, kde mohou ušetřit ještě více času, když se něco nepovede. Pomocí služeb správy zdrojového kódu v cloudu už nemusíte dělat starosti se složitým nastavování a můžete použít Azure Repos správy zdrojového kódu zdarma až na 5 uživatelů.

První část této kapitoly vysvětluje tři klíčové postupy, které je potřeba vzít v úvahu:

- [Považovat skripty pro automatizaci jako zdrojový kód](#scripts) a jejich verze společně s kódem vaší aplikace.
- [Nikdy nevyhledávat tajné klíče](#secrets) (citlivá data jako přihlašovací údaje) do úložiště zdrojového kódu.
- [Nastavte zdrojové větve](#devops) , aby se povolil pracovní postup DevOps.

Zbytek kapitoly poskytuje několik ukázkových implementací těchto vzorů v aplikaci Visual Studio, Azure a Azure Repos:

- [Přidání skriptů do správy zdrojového kódu v aplikaci Visual Studio](#vsscripts)
- [Ukládání citlivých dat v Azure](#appsettings)
- [Použití Gitu v aplikaci Visual Studio a Azure Repos](#gittfs)

<a id="scripts"></a>
## <a name="treat-automation-scripts-as-source-code"></a>Považovat skripty pro automatizaci jako zdrojový kód

Když pracujete na cloudovém projektu, často měníte věci a chcete být schopni rychle reagovat na problémy nahlášené vašimi zákazníky. Rychlé použití skriptů pro automatizaci, jak je vysvětleno v kapitole automatizace [všeho](automate-everything.md) . Všechny skripty, které slouží k vytvoření prostředí, nasazení na něj, jejich škálování atd., je nutné synchronizovat se zdrojovým kódem vaší aplikace.

Chcete-li udržovat skripty synchronizované s kódem, uložte je do systému správy zdrojového kódu. Pokud budete někdy potřebovat vrátit změny nebo provést rychlou opravu produkčního kódu, který se liší od vývojového kódu, nemusíte ztrácet čas při pokusu o sledování, která nastavení se změnila nebo které členové týmu mají kopie verze, kterou potřebujete. Máte jistotu, že skripty, které potřebujete, jsou synchronizované se základem kódu, pro který je potřebujete, a máte jistotu, že všichni členové týmu pracují se stejnými skripty. Pak budete mít správný skript pro kód, který se má aktualizovat, a to bez ohledu na to, jestli potřebujete automatizovat testování a nasazení horké opravy do produkčního nebo nového vývoje funkcí.

<a id="secrets"></a>
## <a name="dont-check-in-secrets"></a>Nekontrolovat tajné klíče

Úložiště zdrojového kódu je obvykle přístupné pro příliš mnoho uživatelů, aby bylo správně bezpečné místo pro citlivá data, jako jsou hesla. Pokud se skripty spoléhají na tajné kódy, jako jsou hesla, parametrizovat tato nastavení tak, aby se neukládala ve zdrojovém kódu, a vaše tajná klíče ukládejte jinde.

Azure například umožňuje stahovat soubory, které obsahují nastavení publikování, aby bylo možné automatizovat vytváření profilů publikování. Mezi tyto soubory patří uživatelská jména a hesla, která mají oprávnění ke správě služeb Azure. Pokud použijete tuto metodu k vytváření profilů publikování a pokud tyto soubory zařadíte do správy zdrojových kódů, kdokoli s přístupem k úložišti uvidí Tato uživatelská jména a hesla. Heslo můžete bezpečně uložit do samotného profilu publikování, protože je zašifrované a je v souboru *. pubxml. User* , který ve výchozím nastavení není zahrnutý ve správě zdrojového kódu.

<a id="devops"></a>
## <a name="structure-source-branches-to-facilitate-devops-workflow"></a>Struktury zdrojových větví pro usnadnění DevOps pracovního postupu

Způsob implementace větví ve vašem úložišti má vliv na schopnost vyvíjet nové funkce a opravovat problémy v produkčním prostředí. Tady je vzor, který využívá spousta středně velkých týmů:

![Struktura zdrojové větve](source-control/_static/image1.png)

Hlavní větev vždy odpovídá kódu, který je v produkčním prostředí. Větve pod hlavní složkou odpovídají různým fázím vývojového cyklu. Vývojová větev je místo, kde implementujete nové funkce. Pro malý tým byste mohli mít jenom hlavní a vývoj, ale často doporučujeme, aby lidé měli pracovní větev mezi vývojem a hlavním serverem. Před přesunutím aktualizace do produkčního prostředí můžete použít fázování pro finální testování Integration.

Pro velké týmy můžou být pro každou novou funkci oddělené větvení; v případě menšího týmu můžete mít všechny rezervace do vývojové větve.

Máte-li větev pro každou funkci, je-li funkce A připravena sloučit změny zdrojového kódu do vývojové větve a dolů do ostatních větví funkcí. Tento proces sloučení zdrojového kódu může být časově náročný a aby se zabránilo tomu, že se pořád udržuje funkce oddělené, některé týmy implementují alternativu s názvem *[přepínacích](http://en.wikipedia.org/wiki/Feature_toggle)* funkcí (označují se také jako *příznaky funkcí*). To znamená, že veškerý kód pro všechny funkce je ve stejné větvi, ale povolíte nebo zakážete jednotlivé funkce pomocí přepínačů v kódu. Předpokládejme například, že funkce A je nové pole pro opravy úkolů aplikace IT a funkce B přidává funkce pro ukládání do mezipaměti. Kód pro obě funkce může být ve vývojové větvi, ale aplikace zobrazí pouze nové pole, když je proměnná nastavena na hodnotu true, a bude používat ukládání do mezipaměti pouze v případě, že je jiná proměnná nastavena na hodnotu true. Pokud funkce A není připravená na zvýšení úrovně, ale funkce B je připravená, můžete zvýšit úroveň všech kódů na produkční, a to tak, že vypnete přepínač a funkci B na. Potom můžete dokončit funkci a a později ji zvýšit, vše bez sloučení zdrojového kódu.

Bez ohledu na to, jestli používáte větve nebo přepínáte na funkce, větvení struktura, jako je to, umožňuje flowovat kód z vývoje do produkčního prostředí v agilním a snadno možném způsobu.

Tato struktura také umožňuje rychle reagovat na zpětnou vazbu od zákazníků. Pokud potřebujete provést rychlou opravu produkčního prostředí, můžete to udělat také agilním způsobem. Můžete vytvořit větev z hlavního nebo přípravného prostředí a když je připravený, sloučit ho do hlavní větve a do fází vývoje a funkcí.

![větev hotfix](source-control/_static/image2.png)

Bez větvení struktury, jako je to s oddělením produkčních a vývojových větví, by vám výrobní problém mohl klást v situaci, kdy je nutné zvýšit úroveň nového kódu funkce společně s opravou produkčního prostředí. Nový kód funkce nemusí být plně testován a připravený pro produkční prostředí. možná budete muset udělat spoustu práce, která není připravena. Nebo je možné, že budete muset odložit opravu a otestovat změny a připravit je na nasazení.

Dále uvidíte příklady implementace těchto tří vzorů v aplikaci Visual Studio, Azure a Azure Repos. Tady jsou příklady, nikoli podrobné pokyny k tomu, jak postupovat podle svých kroků. Podrobné pokyny, které poskytují všechny nezbytné kontexty, naleznete v části [Resources (prostředky](#resources) ) na konci kapitoly.

<a id="vsscripts"></a>
## <a name="add-scripts-to-source-control-in-visual-studio"></a>Přidání skriptů do správy zdrojového kódu v aplikaci Visual Studio

Můžete přidat skripty do správy zdrojového kódu v aplikaci Visual Studio zahrnutím do složky řešení sady Visual Studio (za předpokladu, že projekt je ve správě zdrojového kódu). Tady je jeden ze způsobů, jak to provést.

Vytvořte složku pro skripty ve složce řešení (stejnou složku, která má soubor *. sln* ).

![Složka Automation](source-control/_static/image3.png)

Zkopírujte soubory skriptu do složky.

![Obsah složky automatizace](source-control/_static/image4.png)

V aplikaci Visual Studio přidejte do projektu složku řešení.

![Výběr nabídky nové složky řešení](source-control/_static/image5.png)

A přidejte soubory skriptu do složky řešení.

![Přidat existující výběr nabídky položek](source-control/_static/image6.png)

![Dialogové okno Přidat existující položku](source-control/_static/image7.png)

Soubory skriptu jsou nyní součástí projektu a Správa zdrojového kódu sleduje změny verzí spolu s odpovídajícími změnami zdrojového kódu.

<a id="appsettings"></a>
## <a name="store-sensitive-data-in-azure"></a>Ukládání citlivých dat v Azure

Pokud spouštíte aplikaci na webu Azure, jedním ze způsobů, jak zabránit ukládání přihlašovacích údajů ve správě zdrojového kódu, je místo toho ukládat je do Azure.

Například oprava IT aplikace ukládá do svého souboru Web. config dva připojovací řetězce, které budou mít hesla v produkčním prostředí, a klíč, který poskytuje přístup k vašemu účtu úložiště Azure.

[!code-xml[Main](source-control/samples/sample1.xml?highlight=2-3,11)]

Pokud do souboru *Web. config* vložíte skutečné produkční hodnoty, nebo pokud je umístíte do souboru *Web. Release. config* a nakonfigurujete transformaci Web. config tak, aby byly vloženy během nasazení, budou uloženy ve zdrojovém úložišti. Pokud zadáte připojovací řetězce databáze do produkčního publikačního profilu, heslo bude v souboru *. pubxml* . (Soubor *. pubxml* můžete vyloučit ze správy zdrojového kódu, ale potom ztratíte výhody sdílení všech ostatních nastavení nasazení.)

Azure nabízí alternativu pro části **appSettings** a připojovací řetězce v souboru *Web. config* . Tady je relevantní část karty **Konfigurace** webu na portálu pro správu Azure:

![appSettings a connectionStrings na portálu](source-control/_static/image8.png)

Když nasadíte projekt na tento web a aplikace se spustí, jakékoli hodnoty, které jste uložili v Azure, přepíší jakékoli hodnoty v souboru Web. config.

Tyto hodnoty můžete v Azure nastavit buď pomocí portálu pro správu, nebo pomocí skriptů. Skript pro automatizaci vytváření prostředí, který jste viděli v kapitole [Automatizace všeho](automate-everything.md) , vytvoří Azure SQL Database, získá připojovací řetězce a připojovací řetězce SQL Database a uloží je do nastavení webu.

[!code-powershell[Main](source-control/samples/sample2.ps1)]

[!code-powershell[Main](source-control/samples/sample3.ps1)]

Všimněte si, že skripty jsou parametrizované tak, aby se skutečné hodnoty nezachovaly do zdrojového úložiště.

Při místním spuštění ve vývojovém prostředí načte aplikace místní soubor Web. config a váš připojovací řetězec odkazuje na databázi LocalDB SQL Server ve složce *app\_data* vašeho webového projektu. Když aplikaci spustíte v Azure a aplikace se pokusí přečíst tyto hodnoty ze souboru Web. config, co se vrátí a používá, jsou hodnoty uložené pro web, ne to, co je ve skutečnosti v souboru Web. config.

<a id="gittfs"></a>
## <a name="use-git-in-visual-studio-and-azure-devops"></a>Použití Gitu v aplikaci Visual Studio a Azure DevOps

K implementaci struktury větvení DevOps uvedené výše můžete použít libovolné prostředí pro správu zdrojového kódu. Pro distribuované týmy může fungovat nejlepší [systém správy distribuovaných verzí](http://en.wikipedia.org/wiki/Distributed_revision_control) (DVCS). pro jiné týmy může [centralizovaný systém](http://en.wikipedia.org/wiki/Revision_control) lépe fungovat.

[Git](http://git-scm.com/) je oblíbený distribuovaný systém správy verzí. Když použijete Git pro správu zdrojového kódu, budete mít úplnou kopii úložiště se všemi jeho historií na místním počítači. Mnoho lidí má přednost před tím, že je snazší pracovat, i když nejste připojeni k síti. můžete pokračovat v provádění změn a vrácení zpět, vytváření a přepínání větví a tak dále. I když jste připojeni k síti, je snazší a rychlejší vytvářet větve a přepínat větve, pokud je vše místní. Můžete také provádět místní potvrzení a vrácení zpět bez dopadu na jiné vývojáře. A můžete je před odesláním na server Batch zapsat.

[Azure Repos](/azure/devops/repos/index?view=vsts) nabízí jak [Git](/azure/devops/repos/git/?view=vsts) , tak [Správa verzí Team Foundation](/azure/devops/repos/tfvc/index?view=vsts) (TFVC; centralizované řízení zdrojového kódu). Začněte s Azure DevOps [tady](https://app.vsaex.visualstudio.com/signup).

Visual Studio 2017 obsahuje integrovanou, první třídu [podpory Git](https://msdn.microsoft.com/library/hh850437.aspx). Tady je Stručná ukázka toho, jak to funguje.

Otevřete projekt v aplikaci Visual Studio, klikněte pravým tlačítkem na řešení v **Průzkumník řešení**a pak zvolte **Přidat řešení do správy zdrojového kódu**.

![Přidat řešení do správy zdrojového kódu](source-control/_static/image9.png)

Visual Studio se zeptá, jestli chcete používat TFVC (centralizovanou správu verzí) nebo Git.

![Zvolit správu zdrojového kódu](source-control/_static/image10.png)

Když vyberete Git a kliknete na **OK**, Visual Studio ve složce řešení vytvoří nové místní úložiště Git. Nové úložiště ještě neobsahuje žádné soubory. je nutné je přidat do úložiště pomocí potvrzení Git. Klikněte pravým tlačítkem na řešení v **Průzkumník řešení**a pak klikněte na **Potvrdit**.

![Potvrdit](source-control/_static/image11.png)

Visual Studio automaticky vymění všechny soubory projektu pro potvrzení a zobrazí je v **Team Explorer** v podokně **Zahrnuté změny** . (Pokud jste některé z nich nechtěli zahrnout do potvrzení změn, můžete je vybrat, kliknout pravým tlačítkem a kliknout na **vyloučit**.)

![Team Explorer](source-control/_static/image12.png)

Zadejte komentář pro potvrzení a klikněte na **Potvrdit**a Visual Studio spustí potvrzení a zobrazí ID potvrzení.

![Team Explorer změny](source-control/_static/image13.png)

Když teď změníte kód tak, aby se lišil od toho, co je v úložišti, můžete snadno zobrazit rozdíly. Klikněte pravým tlačítkem na soubor, který jste změnili, vyberte možnost **Porovnat s nezměněnými**a zobrazí se zobrazení porovnání, které zobrazuje nepotvrzené změny.

![Porovnat s verzí bez úprav](source-control/_static/image14.png)

![Rozdíl zobrazující změny](source-control/_static/image15.png)

Můžete snadno zjistit, jaké změny provedete, a vrátit je se změnami.

Předpokládejme, že potřebujete vytvořit větev – můžete to udělat i v aplikaci Visual Studio. V **Team Explorer**klikněte na možnost **Nová větev**.

![Team Explorer novou větev](source-control/_static/image16.png)

Zadejte název větve, klikněte na **vytvořit větev**a pokud jste vybrali **rezervovat větev**, Visual Studio automaticky ověří novou větev.

![Team Explorer novou větev](source-control/_static/image17.png)

Nyní můžete provádět změny souborů a vrátit je do této větve. A můžete snadno přepínat mezi větvemi a aplikace Visual Studio automaticky synchronizuje soubory do libovolné větve, kterou jste si rezervovali. V tomto příkladu se název webové stránky v *\_layout. cshtml* změnil na "Hot Fix 1" ve větvi HotFix1.

![Větev Hotfix1](source-control/_static/image18.png)

Pokud přepnete zpět do hlavní větve, obsah souboru *\_layout. cshtml* se automaticky vrátí k tomu, co se nachází ve větvi Master.

![Hlavní větev](source-control/_static/image19.png)

Toto je jednoduchý příklad, jak můžete rychle vytvořit větev a převrátit se mezi větvemi. Tato funkce umožňuje vysoce agilní pracovní postup pomocí struktury větví a skriptů pro automatizaci, které jsou k dispozici v kapitole [automatizovat vše](automate-everything.md) . Můžete například pracovat ve větvi pro vývoj, vytvořit větev Hot Fix z hlavní větve, přepnout do nové větve, provést změny a potvrdit je a pak přejít zpátky do vývojové větve a pokračovat v práci.

Tady vidíte, jak pracujete s místním úložištěm Git v aplikaci Visual Studio. V prostředí týmu se obvykle také doručí změny až do společného úložiště. Nástroje sady Visual Studio umožňují také nasměrovat na vzdálené úložiště Git. Pro tento účel můžete použít GitHub.com nebo můžete použít [Git a Azure Repos](/azure/devops/repos/git/overview?view=vsts) integrovány se všemi ostatními funkcemi Azure DevOps, jako je například pracovní položka a sledování chyb.

Nejedná se o jediný způsob, jak můžete implementovat strategii agilního větvení, samozřejmě. Můžete povolit stejný agilní pracovní postup pomocí centralizovaného úložiště správy zdrojového kódu.

## <a name="summary"></a>Přehled

Změřte úspěšnost svého systému správy zdrojů na základě toho, jak rychle můžete provést změnu a začít bezpečně a předvídatelným způsobem. Pokud zjistíte, že jste se děsilii změnou, protože je třeba provést jeden den nebo dva ruční testování, můžete se zeptat, co je potřeba udělat, nebo vyzkoušet, abyste tuto změnu mohli udělat v řádu minut nebo v nejhorším rozsahu po dobu delší než hodinu. Jedna strategie, která umožňuje implementovat průběžnou integraci a průběžné doručování, které pokryjeme v [Další části](continuous-integration-and-continuous-delivery.md).

<a id="resources"></a>
## <a name="resources"></a>Prostředky

Další informace o strategiích větvení najdete v následujících zdrojích informací:

- [Vytvoření kanálu pro vydání s Team Foundation Server 2012](https://msdn.microsoft.com/library/dn449957.aspx). Dokumentace ke vzorům a postupům Microsoftu Diskuzi o strategiích větvení najdete v kapitole 6. Funkce poradců přepíná přes větve funkcí a pokud se používají pobočky pro funkce, poradce si je zachovává jako krátkodobé (hodiny nebo dny).
- [Příručka pro správu verzí](https://aka.ms/vsarsolutions). Průvodce strategiemi větvení podle ALMch rozsahů Viz strategie větvení. PDF na kartě stažení.
- [Vývoj softwaru s přepínači funkcí](https://msdn.microsoft.com/magazine/dn683796.aspx) Článek na webu MSDN Magazine.
- [Přepínač funkce](http://martinfowler.com/bliki/FeatureToggle.html). Seznámení s možnostmi přepínání funkcí/příznaků funkcí na blogu Martinu Fowlera.
- [Přepínání funkcí – větve funkcí vs](http://geekswithblogs.net/Optikal/archive/2013/02/10/152069.aspx). Další Blogový příspěvek o přepínačích funkcí Dylan Smith.

Další informace o tom, jak zpracovávat citlivé informace, které by neměly být uchovávány v úložištích správy zdrojového kódu, najdete v následujících zdrojích informací:

- [Osvědčené postupy pro nasazování hesel a dalších citlivých dat do ASP.NET a Azure App Service](../../../../identity/overview/features-api/best-practices-for-deploying-passwords-and-other-sensitive-data-to-aspnet-and-azure.md).
- [Weby Azure: jak fungují řetězce aplikace a připojovací řetězce](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/). Vysvětluje funkci Azure, která přepisuje `appSettings` a `connectionStrings` data v souboru *Web. config* .
- [Vlastní nastavení konfigurace a aplikace na webech Azure – pomocí Stefan Schackow](https://azure.microsoft.com/documentation/videos/configuration-and-app-settings-of-azure-web-sites/).

Informace o dalších metodách zachování citlivých informací ze správy zdrojového kódu najdete v tématu [ASP.NET MVC: zachování privátního nastavení ze správy zdrojového kódu](http://typecastexception.com/post/2014/04/06/ASPNET-MVC-Keep-Private-Settings-Out-of-Source-Control.aspx).

> [!div class="step-by-step"]
> [Předchozí](automate-everything.md)
> [Další](continuous-integration-and-continuous-delivery.md)

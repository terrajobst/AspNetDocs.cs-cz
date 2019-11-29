---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
title: Automatizace všeho (vytváření skutečných cloudových aplikací s Azure) | Microsoft Docs
author: MikeWasson
description: Vytváření reálných cloudových aplikací pomocí Azure je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které mohou...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: ba6e6baa-9b9f-471f-b39d-b007a3addadc
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
msc.type: authoredcontent
ms.openlocfilehash: d5c8190d0b0c91bf9e42f6ef03adc5b07a65359a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74582888"
---
# <a name="automate-everything-building-real-world-cloud-apps-with-azure"></a>Automatizace všeho (vytváření skutečných cloudových aplikací s Azure)

[Jan Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Dykstra](https://github.com/tdykstra)

[Stažení opravy projektu IT](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stažení elektronické knihy](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **Vytváření reálných cloudových aplikací pomocí Azure** je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které vám pomůžou úspěšně vyvíjet webové aplikace pro Cloud. Úvod do elektronické knihy najdete v [první kapitole](introduction.md).

První tři vzory se ve skutečnosti podíváme na jakýkoli projekt vývoje softwaru, ale hlavně na cloudové projekty. Tento model se týká automatizace úloh vývoje. Jedná se o důležité téma, protože ruční procesy jsou pomalé a náchylné k chybám; automatizace co nejvíce z nich pomáhá nastavit rychlý, spolehlivý a agilní pracovní postup. Pro vývoj v cloudu je jednoznačně důležité, protože je možné snadno automatizovat mnoho úloh, které jsou obtížné nebo nemožné automatizovat v místním prostředí. Můžete například nastavit celá testovací prostředí včetně nového webového serveru a back-endové virtuálních počítačů, databází, úložiště objektů BLOB (úložiště souborů), front atd.

## <a name="devops-workflow"></a>Pracovní postup DevOps

Stále častěji uslyšíte pojem "DevOps". Pojem vyvine z rozpoznávání, který je potřeba k zajištění efektivního vývoje úloh vývoje a provozu. Typ pracovního postupu, který chcete povolit, je jedním z nich, kde můžete vyvíjet aplikace, nasazovat je, učit se z produkčního využití, měnit je v reakci na to, co jste se naučili, a rychle a spolehlivě opakovat cyklus.

Některé úspěšné týmy vývoje cloudu se nasazují několikrát denně do živého prostředí. Tým Azure, který se používá k nasazení hlavní aktualizace každých 2-3 měsíců, ale teď uvolňuje drobné aktualizace každých 2-3 dnů a hlavní verze každých 2-3 týdnů. Přihlaste se k tomuto tempo, který vám ve skutečnosti pomůže reagovat na názory zákazníků.

Abyste to mohli udělat, musíte povolit cyklus vývoje a nasazení, který je možné opakovat, spolehlivě, předvídatelný a má nízký čas.

![Pracovní postup DevOps](automate-everything/_static/image1.png)

Jinými slovy, časová prodleva mezi tím, kdy máte představu o funkci, a když ji zákazníci používají a poskytování zpětné vazby musí být co nejkratší. První tři vzory – automatizace všeho, správy zdrojového kódu a průběžná integrace a doručování – jsou všechny osvědčené postupy, které doporučujeme, abyste tento druh procesu povolili.

## <a name="azure-management-scripts"></a>Skripty pro správu Azure

V [úvodu k této elektronické knize](introduction.md)jste viděli webovou konzolu, Azure portál pro správu. Portál pro správu umožňuje monitorovat a spravovat všechny prostředky, které jste nasadili v Azure. Je to snadný způsob, jak vytvořit a odstranit služby, jako jsou webové aplikace a virtuální počítače, konfigurovat tyto služby, monitorovat provoz služby a tak dále. Je to skvělý nástroj, ale jeho použití je ruční proces. Pokud budete vyvíjet produkční aplikaci libovolné velikosti a zejména v týmovém prostředí, doporučujeme projít si uživatelské rozhraní portálu, abyste se seznámili a prozkoumali Azure a pak prováděli automatizaci procesů, které budete opakovaně.

Téměř všechno, co můžete ručně provést na portálu pro správu nebo v sadě Visual Studio, můžete také provést voláním rozhraní API pro správu REST. Můžete psát skripty pomocí [prostředí Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx)nebo můžete použít Open Source rozhraní, jako je například Puppet [nebo](http://www.opscode.com/chef/) . [](http://puppetlabs.com/puppet/what-is-puppet) Nástroj příkazového řádku bash můžete použít také v prostředí Mac nebo Linux. Azure obsahuje skriptovací rozhraní API pro všechna různá prostředí a má [rozhraní API pro správu .NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx) pro případ, že chcete místo skriptu napsat kód.

Pro aplikaci opravit IT jsme vytvořili několik skriptů prostředí Windows PowerShell, které automatizují procesy vytvoření testovacího prostředí a nasazení projektu do tohoto prostředí, a my si probereme obsah těchto skriptů.

## <a name="environment-creation-script"></a>Skript pro vytváření prostředí

První skript, který podíváme na, má název *New-AzureWebsiteEnv. ps1*. Vytvoří prostředí Azure, ve kterém můžete nasadit aplikaci Fix it na pro účely testování. Hlavní úlohy, které tento skript provede, jsou následující:

- Vytvořte webovou aplikaci.
- Vytvořte účet úložiště. (Vyžaduje se pro objekty BLOB a fronty, jak uvidíte v pozdějších kapitolách.)
- Vytvoření serveru SQL Database a dvou databází: aplikační databáze a databáze členství.
- Nastavení úložiště v Azure, které bude aplikace používat pro přístup k účtu úložiště a databázím.
- Vytvořte soubory nastavení, které budou použity k automatizaci nasazení.

### <a name="run-the-script"></a>Spuštění skriptu

> [!NOTE]
> Tato část kapitoly ukazuje příklady skriptů a příkazů, které zadáte, aby je bylo možné spustit. Tato ukázka a neposkytuje vše, co potřebujete znát, aby bylo možné spouštět skripty. Podrobné pokyny k tomu, jak postupovat, najdete v [dodatku: Oprava ukázkové aplikace](the-fix-it-sample-application.md#deploybase).

Pokud chcete spustit skript PowerShellu, který spravuje služby Azure, musíte nainstalovat konzolu Azure PowerShell a nakonfigurovat ji tak, aby fungovala s vaším předplatným Azure. Po nastavení můžete spustit skript opravit IT prostředí pomocí příkazu, jako je tento:

`.\New-AzureWebsiteEnv.ps1 -Name <websitename> -SqlDatabasePassword <password>`

Parametr `Name` Určuje název, který se má použít při vytváření databáze a účtů úložiště, a parametr `SqlDatabasePassword` Určuje heslo pro účet správce, který se vytvoří pro SQL Database. K dispozici jsou další parametry, které můžete použít, když se podíváme později.

![Okno PowerShellu](automate-everything/_static/image2.png)

Po dokončení skriptu se můžete na portálu pro správu podívat na to, co bylo vytvořeno. Najdete dvě databáze:

![Databáze](automate-everything/_static/image3.png)

Účet úložiště:

![Účet úložiště](automate-everything/_static/image4.png)

A webová aplikace:

![Web](automate-everything/_static/image5.png)

Na kartě **Konfigurovat** u webové aplikace vidíte, že má nastavení účtu úložiště a připojovací řetězce služby SQL Database nastavené pro aplikaci opravit IT.

![appSettings a connectionStrings](automate-everything/_static/image6.png)

Složka *Automation* teď obsahuje taky *&lt;&gt;pubxml souboru wEBWeb* . Tento soubor obsahuje nastavení, která nástroj MSBuild použije k nasazení aplikace do prostředí Azure, které jste právě vytvořili. Příklad:

[!code-xml[Main](automate-everything/samples/sample1.xml)]

Jak vidíte, skript vytvořil kompletní testovací prostředí a celý proces se provede přibližně 90 sekund.

Pokud chce jiný tým v týmu vytvořit testovací prostředí, může skript spustit pouze. Nejenom je to rychlá, ale taky si můžou být jistí, že používají prostředí stejné jako ten, který používáte. Nemůžete mít poměrně jistotu, že pokud všechno nastavilo ručně pomocí uživatelského rozhraní portálu pro správu.

### <a name="a-look-at-the-scripts"></a>Podívejte se na skripty.

Existují skutečně tři skripty, které tuto práci dělají. Zavoláte ho z příkazového řádku a automaticky se použije druhá dvě k provedení některých úkolů:

- *New-AzureWebSiteEnv. ps1* je hlavní skript.

    - *New-AzureStorage. ps1* vytvoří účet úložiště.
    - *New-AzureSql. ps1* vytvoří databáze.

### <a name="parameters-in-the-main-script"></a>Parametry hlavního skriptu

Hlavní skript *New-AzureWebSiteEnv. ps1*definuje několik parametrů:

[!code-powershell[Main](automate-everything/samples/sample2.ps1)]

Jsou vyžadovány dva parametry:

- Název webové aplikace, kterou skript vytvoří. (Používá se také pro adresu URL: `<name>.azurewebsites.net`.)
- Heslo pro nového administrativního uživatele databázového serveru, který skript vytvoří.

Volitelné parametry umožňují zadat umístění datového centra (výchozí nastavení je "Západní USA"), název správce databázového serveru (výchozí hodnota je "DbUser") a pravidlo brány firewall pro databázový server.

### <a name="create-the-web-app"></a>Vytvoření webové aplikace

První věc, kterou skript vytvoří, je vytvoření webové aplikace voláním rutiny `New-AzureWebsite`, do které se předává název webové aplikace a hodnoty parametrů umístění:

[!code-powershell[Main](automate-everything/samples/sample3.ps1?highlight=2)]

### <a name="create-the-storage-account"></a>Vytvoření účtu úložiště

Pak hlavní skript spustí skript *New-AzureStorage. ps1* , který jako název účtu úložiště určí "&lt;webnázev *&gt;* Storage" a stejné umístění datového centra jako webová aplikace.

[!code-powershell[Main](automate-everything/samples/sample4.ps1?highlight=3)]

*New-AzureStorage. ps1* volá rutinu `New-AzureStorageAccount` pro vytvoření účtu úložiště a vrátí hodnoty názvu účtu a přístupové klíče. Aby aplikace mohla přistupovat k objektům blob a frontám v účtu úložiště, bude tyto hodnoty potřebovat.

[!code-powershell[Main](automate-everything/samples/sample5.ps1?highlight=2)]

Možná nebudete vždy chtít vytvořit nový účet úložiště. skript můžete rozšířit přidáním parametru, který ho případně nasměruje na používání existujícího účtu úložiště.

### <a name="create-the-databases"></a>Vytvoření databází

Hlavní skript potom po nastavení výchozích databází a názvů pravidel brány firewall spustí skript pro vytváření databáze *New-AzureSql. ps1*:

[!code-powershell[Main](automate-everything/samples/sample6.ps1)]

[!code-powershell[Main](automate-everything/samples/sample7.ps1?highlight=2)]

Skript pro vytvoření databáze načte IP adresu vývojového počítače a nastaví pravidlo brány firewall, aby se počítač pro vývoj mohl připojit k serveru a spravovat ho. Skript pro vytvoření databáze pak projde několika kroky pro nastavení databází:

- Vytvoří server pomocí rutiny `New-AzureSqlDatabaseServer`.

    [!code-powershell[Main](automate-everything/samples/sample8.ps1?highlight=1)]
- Vytvoří pravidla brány firewall, která umožní počítači pro vývoj spravovat server a povolit připojení k webové aplikaci. 

    [!code-powershell[Main](automate-everything/samples/sample9.ps1?highlight=3,5)]
- Vytvoří kontext databáze, který obsahuje název serveru a přihlašovací údaje, pomocí rutiny `New-AzureSqlDatabaseServerContext`.

    [!code-powershell[Main](automate-everything/samples/sample10.ps1?highlight=4)]

    `New-PSCredentialFromPlainText` je funkce ve skriptu, který volá rutinu `ConvertTo-SecureString` k zašifrování hesla a vrátí objekt `PSCredential`, stejný typ, který rutina `Get-Credential` vrátí.
- Vytvoří aplikační databázi a databázi členství pomocí rutiny `New-AzureSqlDatabase`.

    [!code-powershell[Main](automate-everything/samples/sample11.ps1?highlight=2,5)]
- Volá místně definovanou funkci pro vytvoření připojovacího řetězce pro každou databázi. Aplikace bude tyto připojovací řetězce používat pro přístup k databázím. 

    [!code-powershell[Main](automate-everything/samples/sample12.ps1?highlight=1-2)]

    Get-SQLAzureDatabaseConnectionString je funkce definovaná ve skriptu, který vytváří připojovací řetězec z hodnot parametrů, které jsou k němu dodány.

    [!code-powershell[Main](automate-everything/samples/sample13.ps1?highlight=1)]
- Vrátí tabulku hash s názvem databázového serveru a připojovacími řetězci.

    [!code-powershell[Main](automate-everything/samples/sample14.ps1)]

Aplikace pro opravu IT používá samostatné databáze členství a aplikací. Je také možné umístit data členství i aplikace do jediné databáze.

### <a name="store-app-settings-and-connection-strings"></a>Nastavení aplikace a připojovací řetězce pro Store

Azure obsahuje funkci, která umožňuje ukládat nastavení a připojovací řetězce, které automaticky přepisují, co se vrátí do aplikace, když se pokusí přečíst `appSettings` nebo `connectionStrings` kolekce v souboru Web. config. Jedná se o alternativu k použití [transformací Web. config](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md) při nasazení. Další informace najdete v tématu [uložení citlivých dat v Azure](source-control.md#appsettings) později v této elektronické knize.

Skript pro vytváření prostředí ukládá do Azure všechny `appSettings` a `connectionStrings` hodnoty, které aplikace potřebuje pro přístup k účtu úložiště a databázím, když běží v Azure.

[!code-powershell[Main](automate-everything/samples/sample15.ps1)]

[!code-powershell[Main](automate-everything/samples/sample16.ps1)]

[!code-powershell[Main](automate-everything/samples/sample17.ps1?highlight=2)]

[New Relic](http://newrelic.com/) je rozhraní telemetrie, které demonstruje v kapitole [monitorování a telemetrie](monitoring-and-telemetry.md) . Skript pro vytváření prostředí také restartuje webovou aplikaci, aby se zajistilo, že bude mít nové nastavení Relic.

[!code-powershell[Main](automate-everything/samples/sample18.ps1?highlight=2)]

### <a name="preparing-for-deployment"></a>Příprava na nasazení

Na konci procesu skript pro vytváření prostředí volá dvě funkce a vytvoří soubory, které budou použity skriptem nasazení.

Jedna z těchto funkcí vytvoří profil publikování *(&lt;soubor website&gt;. pubxml* ). Kód volá REST API Azure, aby získal nastavení publikování a uloží informace do souboru *. publishsettings* . Pak použije informace z tohoto souboru spolu se souborem šablony (*pubxml. template*) k vytvoření souboru *. pubxml* , který obsahuje profil publikování. Tento proces se dvěma kroky simuluje to, co v aplikaci Visual Studio provedete: Stáhněte soubor *. publishsettings* a importujte ho a vytvořte profil publikování.

Druhá funkce používá jiný soubor šablony (Web-Environment. Template) k vytvoření souboru *website-Environment. XML* , který obsahuje nastavení, které bude skript nasazení používat společně se souborem *. pubxml* .

### <a name="troubleshooting-and-error-handling"></a>Řešení potíží a zpracování chyb

Skripty jsou podobné programům: můžou selhat a když chcete, aby se o selhání dozvěděla co nejvíce, a co to způsobilo. Z tohoto důvodu skript pro vytvoření prostředí změní hodnotu proměnné `VerbosePreference` z `SilentlyContinue` na `Continue`, aby se zobrazily všechny podrobné zprávy. Změní také hodnotu proměnné `ErrorActionPreference` z `Continue` na `Stop`, takže se skript zastaví i v případě, že dojde k neukončujícím chybám:

[!code-powershell[Main](automate-everything/samples/sample19.ps1)]

Předtím, než bude fungovat, bude skript obsahovat čas spuštění, aby mohl vypočítat uplynulý čas, kdy se dokončila:

[!code-powershell[Main](automate-everything/samples/sample20.ps1)]

Po dokončení práce skript zobrazí uplynulý čas:

[!code-powershell[Main](automate-everything/samples/sample21.ps1)]

A pro každou operaci klíče skript zapisuje podrobné zprávy, například:

[!code-powershell[Main](automate-everything/samples/sample22.ps1)]

## <a name="deployment-script"></a>Skript nasazení

Skript *New-AzureWebsiteEnv. ps1* pro vytváření prostředí provádí skript *Publish-AzureWebsite. ps1* pro nasazení aplikace.

Skript nasazení Získá název webové aplikace ze souboru *website-Environment. XML* vytvořeného skriptem pro vytváření prostředí.

[!code-powershell[Main](automate-everything/samples/sample23.ps1)]

Získá heslo uživatele nasazení ze souboru *. publishsettings* :

[!code-powershell[Main](automate-everything/samples/sample24.ps1)]

Spustí příkaz [MSBuild](http://msbuildbook.com/) , který sestaví a nasadí projekt:

[!code-powershell[Main](automate-everything/samples/sample25.ps1)]

A pokud jste na příkazovém řádku zadali parametr `Launch`, volá rutinu `Show-AzureWebsite`, která otevře výchozí prohlížeč na adrese URL webu.

[!code-powershell[Main](automate-everything/samples/sample26.ps1?highlight=3)]

Skript nasazení můžete spustit pomocí příkazu, jako je tento:

`.\Publish-AzureWebsite.ps1 ..\MyFixIt\MyFixIt.csproj -Launch`

A až se to dokončí, otevře se prohlížeč s webem spuštěným v cloudu na adrese `<websitename>.azurewebsites.net` URL.

![Opravit aplikaci IT nasazenou v Microsoft Azure](automate-everything/_static/image7.png)

## <a name="summary"></a>Přehled

Pomocí těchto skriptů si můžete být jistí, že stejný postup bude vždycky proveden ve stejném pořadí pomocí stejných možností. To pomáhá zajistit, že každý vývojář týmu nebude přijít o něco nebo si může něco vyzkoušet nebo nasazovat něco vlastního na svém vlastním počítači, který ve skutečnosti nebude fungovat v prostředí jiného člena týmu nebo v produkčním prostředí.

Podobným způsobem můžete automatizovat většinu funkcí správy Azure, které můžete provádět na portálu pro správu, pomocí REST API, skriptů prostředí Windows PowerShell, rozhraní API jazyka .NET nebo nástroje bash, který můžete spustit v systému Linux nebo Mac.

V [další kapitole](source-control.md) se podíváme na zdrojový kód a vysvětlete, proč je důležité zahrnout skripty do úložiště zdrojového kódu.

## <a name="resources"></a>Prostředky

- [Nainstalujte a nakonfigurujte Windows PowerShell pro Azure](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1). Vysvětluje, jak nainstalovat rutiny Azure PowerShell a jak nainstalovat certifikát, který potřebujete do vašeho počítače, abyste mohli spravovat účet Azure. To je skvělé místo, kde můžete začít, protože obsahuje také odkazy na prostředky pro učení samotného prostředí PowerShell.
- [Centrum skriptů Azure](https://docs.microsoft.com/azure/automation/automation-runbook-gallery). Portál WindowsAzure.com k prostředkům pro vývoj skriptů, které spravují služby Azure, s odkazy na kurzy Začínáme, Referenční dokumentace k rutinám a zdrojový kód a ukázkové skripty
- [Víkendový skript: Začínáme pomocí Azure a PowerShellu](https://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx). V blogu vyhrazeném pro Windows PowerShell poskytuje tento příspěvek skvělý úvod k používání PowerShellu pro funkce správy Azure.
- [Instalace a konfigurace rozhraní příkazového řádku Azure pro více platforem](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest). Úvodní kurz pro skriptovací rozhraní Azure, které funguje na počítačích Mac a Linux i v systémech Windows.
- [Část nástroje příkazového řádku v tématu Stažení sad SDK a nástrojů Azure](https://azure.microsoft.com/downloads/) Stránka portálu pro dokumentaci a soubory ke stažení související s nástroji příkazového řádku pro Azure.
- [Automatizace všeho pomocí knihoven pro správu Azure a .NET](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx). Scott Hanselman zavádí rozhraní API pro správu .NET pro Azure.
- [Použití skriptů Windows PowerShellu k publikování do vývojových a testovacích prostředí](https://msdn.microsoft.com/library/azure/dn642480.aspx). Dokumentace MSDN, která vysvětluje, jak používat skripty pro publikování, které Visual Studio automaticky generuje pro webové projekty.
- [PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597). Rozšíření sady Visual Studio, které přidává jazykovou podporu pro prostředí Windows PowerShell v aplikaci Visual Studio.

> [!div class="step-by-step"]
> [Předchozí](introduction.md)
> [Další](source-control.md)

---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-database-projects
title: Nasazení databázových projektů | Microsoft Docs
author: jrjlee
description: 'Poznámka: v mnoha scénářích podnikového nasazení potřebujete možnost publikovat přírůstkové aktualizace do nasazené databáze. Alternativou je znovu vytvořit...'
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 832f226a-1aa3-4093-8c29-ce4196793259
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-database-projects
msc.type: authoredcontent
ms.openlocfilehash: 221808758492aedb8e8329364e511df28fd11105
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634265"
---
# <a name="deploying-database-projects"></a>Nasazení databázových projektů

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> [!NOTE]
> V mnoha scénářích podnikového nasazení potřebujete možnost publikovat přírůstkové aktualizace do nasazené databáze. Alternativou je opětovné vytvoření databáze při každém nasazení, což znamená, že ztratíte jakákoli data ve stávající databázi. Při práci se sadou Visual Studio 2010 je doporučený postup pro přírůstkové publikování databáze pomocí VSDBCMD. Další verze sady Visual Studio a kanál pro publikování na webu (WPP) ale budou obsahovat nástroje, které přímo podporují přírůstkové publikování.

Pokud otevřete ukázkové řešení Contact Manageru v aplikaci Visual Studio 2010, bude se vám zobrazit, že databázový projekt obsahuje složku vlastností, která obsahuje čtyři soubory.

![](deploying-database-projects/_static/image1.png)

Společně se souborem projektu (*ContactManager. Database. dbproj* v tomto případě) řídí tyto soubory různé aspekty procesu sestavení a nasazení:

- Soubor *Database. sqlcmdvars* poskytuje hodnoty pro všechny proměnné sqlcmd, které používáte při nasazení projektu. Každá konfigurace řešení (například ladit a vydaná verze) může určovat jiný soubor. sqlcmdvars.
- Soubor *Database. SqlDeployment* poskytuje nastavení specifická pro nasazení, jako je třeba použití kolace definované v projektu nebo kolaci cílového serveru, bez ohledu na to, jestli se má cílová databáze znovu vytvořit pokaždé, nebo jednoduše změnit existující databázi, aby byla aktuální, a tak dále. Každé nastavení řešení může určovat jiný soubor. SqlDeployment.
- Soubor *Database. sqlpermissions* je dokument XML, který můžete použít k definování libovolných oprávnění, která chcete přidat do cílové databáze. Všechny konfigurace řešení sdílejí stejný soubor. sqlpermissions.
- Soubor *Database. sqlsettings* určuje vlastnosti na úrovni databáze, které budou použity při vytváření databáze, jako je kolace, která se má použít, chování operátorů porovnání a tak dále. Všechny konfigurace řešení sdílejí stejný soubor. sqlsettings.

Je to chvilku, než se otevřou tyto soubory v aplikaci Visual Studio a seznámení s obsahem.

Při sestavování databázového projektu vytvoří proces sestavení dva soubory:

- *Schéma databáze* (soubor. dbschema). V této části najdete popis schématu databáze, kterou chcete vytvořit ve formátu XML.
- *Manifest nasazení* (soubor. DeployManifest). Obsahuje všechny informace potřebné k vytvoření a nasazení databáze. Odkazuje na soubor. dbschema spolu s dalšími prostředky, jako jsou pokyny pro nasazení (soubor. SqlDeployment) a všechny skripty SQL před nasazením nebo po nasazení.

Zobrazuje vztah mezi těmito prostředky:

![](deploying-database-projects/_static/image2.png)

Jak vidíte, soubor. sqlsettings a soubor. sqlpermissions jsou vstupy procesu sestavení. Spolu se souborem databázového projektu jsou tyto soubory použity k vytvoření souboru schématu databáze. Soubor. SqlDeployment a soubor. sqlcmdvars projde procesem sestavení beze změny. Manifest nasazení označuje umístění schématu databáze, souboru. SqlDeployment, souboru. sqlcmdvars a všech skriptů SQL spouštěných před nasazením nebo po nasazení.

## <a name="why-use-vsdbcmd-to-deploy-a-database-project"></a>Proč použít VSDBCMD k nasazení databázového projektu?

Existují různé přístupy k nasazení databázových projektů. Některé z nich ale nejsou vhodné k nasazení databázového projektu na vzdálené servery v podnikovém prostředí. Zvažte, co požadujete z nasazení databázového projektu. Ve scénářích podnikového nasazení budete pravděpodobně chtít:

- Možnost nasadit databázový projekt ze vzdáleného umístění.
- Možnost provádět přírůstkové aktualizace existující databáze.
- Možnost zahrnout skripty předběžného nasazení nebo skripty po nasazení.
- Možnost přizpůsobit nasazení na více cílových prostředí.
- Možnost nasadit databázový projekt jako součást většího, obvykle spouštěného s jedním krokem nasazením řešení.

Existují tři hlavní přístupy, které můžete použít k nasazení databázového projektu:

- Můžete použít funkci nasazení s typem databázového projektu v aplikaci Visual Studio 2010. Při sestavování a nasazování databázového projektu v aplikaci Visual Studio 2010 proces nasazení používá manifest nasazení ke generování souboru nasazení založeného na jazyce SQL specifického pro konfiguraci sestavení. Tím se vytvoří databáze, pokud ještě neexistuje, nebo pokud už existuje, proveďte potřebné změny v databázi. Nástroj SQLCMD. exe můžete použít ke spuštění tohoto souboru na cílovém serveru, nebo můžete nastavit sadu Visual Studio pro vytvoření a spuštění souboru. Nevýhodou tohoto přístupu je, že máte pouze omezené řízení pro nastavení nasazení. Často je také nutné upravit soubor nasazení SQL tak, aby poskytoval hodnoty proměnných specifických pro prostředí. Tento přístup můžete použít jenom z počítače s nainstalovanou sadou Visual Studio 2010 a vývojář by musel znát a poskytovat připojovací řetězce a přihlašovací údaje pro všechna cílová prostředí.
- K [nasazení databáze jako součásti projektu webové aplikace](https://msdn.microsoft.com/library/dd465343.aspx)můžete použít nástroj pro nasazení webu Internetová informační služba (IIS) (nasazení webu). Tento přístup je ale složitější, pokud chcete nasadit projekt databáze místo pouhého replikování existující místní databáze na cílovém serveru. Můžete nakonfigurovat Nasazení webu pro spuštění skriptu pro nasazení systému SQL, který databázový projekt vygeneruje, ale aby to bylo možné, musíte pro svůj projekt webové aplikace vytvořit vlastní soubor cílů WPP. Tím se do procesu nasazení přidá značná část složitosti. Nasazení webu navíc přímo nepodporuje přírůstkové aktualizace stávajících databází. Další informace o tomto přístupu najdete v tématu [rozšíření kanálu publikování na webu do souboru SQL nasazeného projektu databáze](https://go.microsoft.com/?linkid=9805121).
- K nasazení databáze pomocí nástroje VSDBCMD můžete použít buď schéma databáze, nebo manifest nasazení. Můžete volat VSDBCMD. exe z cíle MSBuild, který umožňuje publikovat databáze jako součást rozsáhlejšího skriptu nasazení. Můžete přepsat proměnné v souboru. sqlcmdvars a spoustě dalších vlastností databáze z příkazu VSDBCMD, který umožňuje přizpůsobení nasazení pro různá prostředí, aniž by bylo nutné vytvářet více konfigurací sestavení. VSDBCMD poskytuje funkce pro odlišení, což znamená, že bude provádět pouze nezbytné změny pro zarovnávání cílové databáze se schématem databáze. VSDBCMD také nabízí široké spektrum možností příkazového řádku, které vám poskytnou jemně odstupňovanou kontrolu nad procesem nasazení.

Z tohoto přehledu vidíte, že použití VSDBCMD s nástrojem MSBuild je to nejlepší způsob, který nejlépe vyhovuje typickému scénáři podnikového nasazení:

|  | Visual Studio 2010 | Nasazení webu 2.0 | VSDBCMD.exe |
| --- | --- | --- | --- |
| Podporuje vzdálené nasazení? | Ano | Ano | Ano |
| Podporuje přírůstkové aktualizace? | Ano | Ne | Ano |
| Podporuje skripty předběžného nebo po nasazení? | Ano | Ano | Ano |
| Podporuje nasazení ve více prostředích? | Limitovan | Limitovan | Ano |
| Podporuje skriptované nasazení? | Limitovan | Ano | Ano |

Zbývající část tohoto tématu popisuje použití VSDBCMD s nástrojem MSBuild k nasazení databázových projektů.

## <a name="understanding-the-deployment-process"></a>Princip procesu nasazení

Nástroj VSDBCMD umožňuje nasadit databázi buď pomocí schématu databáze (soubor. dbschema), nebo manifestu nasazení (soubor. DeployManifest). V praxi skoro vždy použijete manifest nasazení, protože manifest nasazení umožňuje zadat výchozí hodnoty pro různé vlastnosti nasazení a identifikovat všechny skripty SQL před nasazením nebo po nasazení, které chcete spustit. Například tento příkaz VSDBCMD slouží k nasazení databáze **ContactManager** do databázového serveru v testovacím prostředí:

[!code-console[Main](deploying-database-projects/samples/sample1.cmd)]

V tomto případě:

- Přepínač **/a** (nebo **za akci**) určuje, co má VSDBCMD dělat. Tuto možnost můžete nastavit pro **Import** nebo **nasazení**. Možnost **Import** slouží k vygenerování souboru. dbschema z existující databáze a možnost **nasazení** se používá k nasazení souboru. dbschema do cílové databáze.
- Přepínač **/manifest** (nebo **/MANIFESTFILE**) identifikuje soubor. DeployManifest, který chcete nasadit. Pokud jste místo toho chtěli použít soubor. dbschema, použijte přepínač **/model** (nebo **/ModelFile**).
- Přepínač **/cs** (nebo **/ConnectionString**) poskytuje připojovací řetězec pro cílový databázový server. Všimněte si, že to nezahrnuje název databáze&#x2014;VSDBCMD se musí připojit k serveru, aby se vytvořila databáze. není nutné se připojit k individuální databázi. Pokud soubor. DeployManifest obsahuje připojovací řetězec, můžete tento přepínač vynechat. Pokud použijete přepínač, přepíše hodnota switch hodnotu. DeployManifest.
- Vlastnost <strong>/p: TargetDatabase</strong> poskytuje název, který chcete přiřadit cílové databázi při vytváření. Tím se přepíše hodnota vlastnosti <strong>TargetDatabase</strong> v souboru. DeployManifest. Syntaxi <strong>/p:</strong> <em>[vlastnost name]</em>můžete použít k nastavení široké škály vlastností nasazení a k přepsání všech proměnných Sqlcmd deklarovaných v souboru. sqlcmdvars.
- Přepínač **/DD +** (nebo **/DeployToDatabase +** ) označuje, že chcete vytvořit nasazení a nasadit ho do cílového prostředí. Pokud zadáte **/DD-** nebo přepínač vynecháte, VSDBCMD vygeneruje skript nasazení, ale neprovede nasazení do cílového prostředí. Tento přepínač je často zdrojem nejasností a je podrobněji vysvětlen v další části.
- Přepínač **/Script** (nebo **/DeploymentScriptFile**) určuje, kde chcete vygenerovat skript nasazení. Tato hodnota nemá vliv na proces nasazení.

Další informace o VSDBCMD najdete v tématu [Reference k příkazovému řádku pro VSDBCMD. EXE (nasazení a import schématu)](https://msdn.microsoft.com/library/dd193283.aspx) a [Postupy: příprava databáze pro nasazení z příkazového řádku pomocí VSDBCMD. EXE](https://msdn.microsoft.com/library/dd193258.aspx).

Příklad toho, jak lze použít VSDBCMD ze souboru projektu MSBuild, naleznete v tématu [Principy procesu sestavení](understanding-the-build-process.md). Příklady, jak nakonfigurovat nastavení nasazení databáze pro více prostředí, najdete v tématu [přizpůsobení nasazení databáze pro více prostředí](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md).

## <a name="understanding-the-deploytodatabase-switch"></a>Princip přepínače DeployToDatabase

Chování přepínače **/DD** nebo **/DeployToDatabase** závisí na tom, zda používáte VSDBCMD se souborem. dbschema nebo souborem. DeployManifest. Pokud používáte soubor. dbschema, chování je poměrně jasné:

- Pokud zadáte **/DD +** nebo **/DD**, VSDBCMD vygeneruje skript nasazení a nasadí databázi.
- Pokud zadáte **/DD-** nebo vynecháte přepínač, vytvoří VSDBCMD pouze skript nasazení.

Pokud používáte soubor. DeployManifest, je chování mnohem složitější. Důvodem je, že soubor. DeployManifest obsahuje název vlastnosti **DeployToDatabase** , který také určuje, zda je databáze nasazena.

[!code-xml[Main](deploying-database-projects/samples/sample2.xml)]

Hodnota této vlastnosti je nastavena podle vlastností databázového projektu. Nastavíte-li **akci nasadit** pro **Vytvoření skriptu nasazení (. SQL)** , bude hodnota **false**. Nastavíte-li **akci nasadit** pro **Vytvoření skriptu nasazení (. SQL) a nasazení do databáze**, bude hodnota **true**.

> [!NOTE]
> Tato nastavení jsou spojena s konkrétní konfigurací a platformou sestavení. Pokud například nakonfigurujete nastavení pro konfiguraci **ladění** a pak publikujete pomocí konfigurace **vydané verze** , vaše nastavení se nepoužijí.

![](deploying-database-projects/_static/image3.png)

> [!NOTE]
> V tomto scénáři by měla být **Akce nasadit** vždy nastavena na **Vytvoření skriptu nasazení (. SQL)** , protože nechcete, aby sada Visual Studio 2010 nasadila vaši databázi. Jinými slovy, vlastnost **DeployToDatabase** by měla být vždy **false**.

Pokud je zadána vlastnost **DeployToDatabase** , přepínač **/DD** přepíše pouze vlastnost, pokud je hodnota vlastnosti **false**:

- Pokud má vlastnost **DeployToDatabase** **hodnotu false**a zadáte **/DD +** nebo **/DD**, VSDBCMD přepíše vlastnost **DeployToDatabase** a nasadí databázi.
- Pokud má vlastnost **DeployToDatabase** **hodnotu false**a zadáte **/DD-** nebo vynecháte přepínač, VSDBCMD neprovede nasazení databáze.
- Pokud má vlastnost **DeployToDatabase** **hodnotu true**, VSDBCMD přepínač přeskočí a nasadí databázi.
- Skript nasazení se vygeneruje v každém případě bez ohledu na to, jestli nasazujete i databázi.

## <a name="conclusion"></a>Závěr

Toto téma poskytuje přehled procesu sestavení a nasazení pro databázové projekty v aplikaci Visual Studio 2010. Také popisuje, jak můžete pomocí nástroje VSDBCMD. exe s nástrojem MSBuild podporovat nasazení databáze na podnikové úrovni.

Další informace o tom, jak funguje v praxi, najdete v tématu [přizpůsobení nasazení databáze pro více prostředí](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md).

## <a name="further-reading"></a>Další čtení

Informace o tom, jak přizpůsobit nasazení databáze vytvořením samostatného konfiguračního souboru nasazení pro každé prostředí, najdete v tématu [přizpůsobení nasazení databáze pro více prostředí](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md). Pokyny ke konfiguraci členství v databázových rolích spuštěním skriptu po nasazení najdete v tématu [nasazení členství databázové role do testovacích prostředí](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md). Pokyny ke správě některých jedinečných výzev, které databáze členství ukládají, najdete v tématu [nasazení databází členství v podnikových prostředích](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md).

Tato témata na webu MSDN poskytují širší doprovodné materiály a základní informace o projektech databáze sady Visual Studio a procesu nasazení databáze:

- [Projekty databáze sady Visual Studio 2010 SQL Server](https://msdn.microsoft.com/library/ff678491.aspx)
- [Správa změny databáze](https://msdn.microsoft.com/library/aa833404.aspx)
- [Postupy: příprava databáze pro nasazení z příkazového řádku pomocí VSDBCMD. PROGRAMU](https://msdn.microsoft.com/library/dd193258.aspx)
- [Přehled Build and Deployment databáze](https://msdn.microsoft.com/library/aa833165.aspx)

> [!div class="step-by-step"]
> [Předchozí](deploying-web-packages.md)
> [Další](creating-and-running-a-deployment-command-file.md)

---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
title: Spuštění skriptů prostředí Windows PowerShell ze souborů projektu nástroje MSBuild | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak spustit skript prostředí Windows PowerShell jako součást procesu sestavení a nasazení. Můžete spustit skript místně (jinými slovy, na b...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 55f1ae45-fcb5-43a9-8415-fa5b935fc9c9
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
msc.type: authoredcontent
ms.openlocfilehash: 7b09c07b8b7c2a61ca534f7a66a929593f3d04ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78548508"
---
# <a name="running-windows-powershell-scripts-from-msbuild-project-files"></a>Spuštění skriptů Windows PowerShellu ze souborů projektu MSBuild

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak spustit skript prostředí Windows PowerShell jako součást procesu sestavení a nasazení. Můžete spustit skript místně (jinými slovy, na serveru sestavení) nebo vzdáleně, jako na cílovém webovém serveru nebo databázovém serveru.
> 
> K dispozici máte spoustu důvodů, proč byste mohli chtít spustit skript Windows PowerShellu po nasazení. Můžete například potřebovat:
> 
> - Přidejte vlastní zdroj události do registru.
> - Vygenerujte adresář systému souborů pro nahrávání.
> - Vyčištění adresářů sestavení.
> - Zápis položek do vlastního souboru protokolu.
> - Odesílat e-maily, které uživatele zvou k nově zřízené webové aplikaci.
> - Vytvořte uživatelské účty s příslušnými oprávněními.
> - Nakonfigurujte replikaci mezi instancemi SQL Server.
> 
> V tomto tématu se dozvíte, jak místně a vzdáleně spouštět skripty Windows PowerShellu z vlastního cíle v souboru projektu Microsoft Build Engine (MSBuild).

Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého [řešení](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.

Metoda nasazení na srdce těchto kurzů je založena na způsobu rozdělení souborů projektu popsaných v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md), ve kterém je proces sestavení řízen dvěma soubory&#x2014;projektu jeden, který obsahuje pokyny pro sestavení, které platí pro každé cílové prostředí, a jedno obsahující nastavení sestavení a nasazení specifické pro konkrétní prostředí. V době sestavení je soubor projektu specifický pro prostředí sloučen do souboru projektu prostředí – nezávislá a vytvoří kompletní sadu instrukcí pro sestavení.

## <a name="task-overview"></a>Přehled úlohy

Chcete-li spustit skript prostředí Windows PowerShell jako součást procesu automatického nebo jednoduchého nasazení, je třeba provést tyto úlohy vysoké úrovně:

- Přidejte skript Windows PowerShellu do svého řešení a do správy zdrojového kódu.
- Vytvořte příkaz, který vyvolá skript Windows PowerShellu.
- Ve svém příkazu vydejte všechny vyhrazené znaky XML.
- Vytvořte cíl ve vlastním souboru projektu MSBuild a použijte úlohu **exec** ke spuštění příkazu.

V tomto tématu se dozvíte, jak provádět tyto postupy. V úlohách a návodech v tomto tématu se předpokládá, že jste již obeznámeni s cíli a vlastnostmi nástroje MSBuild a že rozumíte tomu, jak použít vlastní soubor projektu MSBuild k řízení procesu sestavení a nasazení. Další informace naleznete v tématu [porozumění souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md) a [porozumění procesu sestavení](../web-deployment-in-the-enterprise/understanding-the-build-process.md).

## <a name="creating-and-adding-windows-powershell-scripts"></a>Vytváření a přidávání skriptů prostředí Windows PowerShell

Úlohy v tomto tématu používají ukázkový skript prostředí Windows PowerShell s názvem **LogDeploy. ps1** , který ukazuje, jak spouštět skripty z MSBuild. Skript **LogDeploy. ps1** obsahuje jednoduchou funkci, která zapisuje jednořádkový zápis do souboru protokolu:

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample1.ps1)]

Skript **LogDeploy. ps1** přijímá dva parametry. První parametr představuje úplnou cestu k souboru protokolu, ke kterému chcete přidat položku, a druhý parametr představuje cíl nasazení, který chcete zaznamenat do souboru protokolu. Když skript spustíte, přidá se do souboru protokolu řádek v tomto formátu:

[!code-html[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample2.html)]

Aby byl skript **LogDeploy. ps1** dostupný pro MSBuild, je nutné provést následující kroky:

- Přidejte skript do správy zdrojových kódů.
- Přidejte skript do řešení v aplikaci Visual Studio 2010.

Nemusíte nasazovat skript s obsahem řešení bez ohledu na to, jestli plánujete spustit skript na serveru sestavení nebo na vzdáleném počítači. Jednou z možností je přidání skriptu do složky řešení. V příkladu správce kontaktů, protože chcete použít skript prostředí Windows PowerShell jako součást procesu nasazení, dává smysl přidat skript do složky řešení publikování.

![](running-windows-powershell-scripts-from-msbuild-project-files/_static/image1.png)

Obsah složek řešení je zkopírován na servery sestavení jako zdrojový materiál. Ale netvoří žádné součásti výstupu projektu.

## <a name="executing-a-windows-powershell-script-on-the-build-server"></a>Spuštění skriptu prostředí Windows PowerShell na serveru sestavení

V některých scénářích můžete chtít spouštět skripty prostředí Windows PowerShell v počítači, který vytváří vaše projekty. Například můžete použít skript prostředí Windows PowerShell k vyčištění složek sestavení nebo zápisu položek do vlastního souboru protokolu.

Z hlediska syntaxe je spuštění skriptu prostředí Windows PowerShell ze souboru projektu MSBuild stejné jako spuštění skriptu prostředí Windows PowerShell z normálního příkazového řádku. Je potřeba vyvolat spustitelný soubor PowerShell. exe a pomocí přepínače **– Command** poskytnout příkazy, které má Windows PowerShell spouštět. (V prostředí Windows PowerShell V2 můžete také použít přepínač **– File** ). Příkaz by měl mít tento formát:

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample3.cmd)]

Příklad:

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample4.cmd)]

Pokud cesta ke skriptu obsahuje mezery, je nutné uzavřít cestu k souboru do jednoduchých uvozovek, které předcházejí ampersand. Nemůžete použít dvojité uvozovky, protože jste je už použili k uzavření příkazu:

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample5.cmd)]

Při vyvolání tohoto příkazu z nástroje MSBuild existuje několik dalších doporučení. Nejdřív byste měli přidat příznak **– neinteraktivní** , abyste zajistili, že se skript spustí v tichém režimu. Dále byste měli přidat příznak **– ExecutionPolicy** s odpovídající hodnotou argumentu. Tato možnost určuje zásady spouštění, které Windows PowerShell použije pro váš skript, a umožní přepsat výchozí zásady spouštění, které můžou zabránit spuštění skriptu. Můžete si vybrat z těchto hodnot argumentů:

- Hodnota bez **omezení** umožní prostředí Windows PowerShell spustit skript bez ohledu na to, jestli je skript podepsaný.
- Hodnota **RemoteSigned** umožní prostředí Windows PowerShell spouštět nepodepsané skripty, které byly vytvořeny na místním počítači. Skripty, které byly vytvořeny jinde, však musí být podepsány. (V praxi je velmi pravděpodobné, že jste na serveru sestavení místně nevytvořili skript prostředí Windows PowerShell.
- Hodnota **AllSigned** umožní prostředí Windows PowerShell spouštět pouze podepsané skripty.

Výchozí zásada spouštění je **omezená**, což zabrání prostředí Windows PowerShell ve spouštění jakýchkoli souborů skriptu.

Nakonec musíte všechny rezervované znaky XML, které se objeví v příkazu Windows PowerShellu:

- Nahraďte jednoduché uvozovky **&amp;;**
- Nahradit dvojité uvozovky pomocí **&amp;quot;**
- Nahraďte ampersandy pomocí **&amp;amp;**

- Když provedete tyto změny, váš příkaz bude vypadat přibližně takto:

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample6.cmd)]

V rámci vlastního souboru projektu MSBuild můžete vytvořit nový cíl a pomocí úlohy **exec** spustit tento příkaz:

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample7.xml)]

V tomto příkladu si všimněte, že:

- Jakékoli proměnné, například hodnoty parametrů a umístění spustitelného souboru prostředí Windows PowerShell, jsou deklarovány jako vlastnosti nástroje MSBuild.
- Jsou zahrnuty podmínky, které uživatelům umožňují přepsat tyto hodnoty z příkazového řádku.
- Vlastnost **MSDeployComputerName** je deklarována jinde v souboru projektu.

Když tento cíl spustíte jako součást procesu sestavení, Windows PowerShell spustí příkaz a zapíše položku protokolu do zadaného souboru.

## <a name="executing-a-windows-powershell-script-on-a-remote-computer"></a>Spuštění skriptu prostředí Windows PowerShell na vzdáleném počítači

Prostředí Windows PowerShell umožňuje spouštět skripty na vzdálených počítačích prostřednictvím [Vzdálená správa systému Windows](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx) (WinRM). K tomu je nutné použít rutinu [Invoke-Command](https://technet.microsoft.com/library/dd347578.aspx) . To vám umožní spustit skript na jednom nebo několika vzdálených počítačích bez kopírování skriptu do vzdálených počítačů. Všechny výsledky se vrátí do místního počítače, ze kterého jste spustili skript.

> [!NOTE]
> Předtím, než použijete rutinu **Invoke-Command** ke spouštění skriptů prostředí Windows PowerShell na vzdáleném počítači, je třeba nakonfigurovat naslouchací proces WinRM, aby přijímal vzdálené zprávy. To můžete provést spuštěním příkazu **winrm quickconfig** ve vzdáleném počítači. Další informace najdete v tématu [instalace a konfigurace pro vzdálená správa systému Windows](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx).

V okně Windows PowerShellu použijete tuto syntaxi ke spuštění skriptu **LogDeploy. ps1** na vzdáleném počítači:

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample8.ps1)]

> [!NOTE]
> Existují různé způsoby použití **příkazu Invoke-Command** ke spuštění souboru skriptu, ale tento přístup je nejpřímější, pokud potřebujete zadat hodnoty parametrů a spravovat cesty s mezerami.

Když spustíte tento příkaz z příkazového řádku, musíte vyvolat spustitelný soubor prostředí Windows PowerShell a pomocí parametru **– Command** zadat pokyny:

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample9.cmd)]

Stejně jako předtím je potřeba poskytnout nějaké další přepínače a při spuštění příkazu z nástroje MSBuild zadat všechny vyhrazené znaky XML.

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample10.cmd)]

A nakonec můžete použít úlohu **exec** v rámci vlastního cíle MSBuild ke spuštění příkazu:

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample11.xml)]

Když tento cíl provedete jako součást procesu sestavení, Windows PowerShell spustí skript na počítači, který jste zadali v argumentu **– ComputerName** .

## <a name="conclusion"></a>Závěr

Toto téma popisuje, jak spustit skript prostředí Windows PowerShell ze souboru projektu MSBuild. Tento postup můžete použít ke spuštění skriptu prostředí Windows PowerShell, a to buď místně, nebo na vzdáleném počítači, jako součást procesu sestavení a nasazení v jednom kroku.

## <a name="further-reading"></a>Další čtení

Pokyny k podepisování skriptů prostředí Windows PowerShell a správě zásad spouštění najdete v tématu [spuštění skriptů prostředí Windows PowerShell](https://technet.microsoft.com/library/ee176949.aspx). Pokyny ke spouštění příkazů prostředí Windows PowerShell ze vzdáleného počítače najdete v tématu [spouštění vzdálených příkazů](https://technet.microsoft.com/library/dd819505.aspx).

Další informace o použití vlastních souborů projektu MSBuild pro řízení procesu nasazení naleznete v tématu [porozumění souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md) a [porozumění procesu sestavení](../web-deployment-in-the-enterprise/understanding-the-build-process.md).

> [!div class="step-by-step"]
> [Předchozí](taking-web-applications-offline-with-web-deploy.md)
> [Další](troubleshooting-the-packaging-process.md)

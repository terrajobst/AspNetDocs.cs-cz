---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-web-packages
title: Nasazení webových balíčků | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak můžete publikovat balíčky pro nasazení webu na vzdáleném serveru pomocí nástroje pro nasazení webu Internetová informační služba (IIS) (Web...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: a5c5eed2-8683-40a5-a2e1-35c9f8d17c29
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-web-packages
msc.type: authoredcontent
ms.openlocfilehash: 91b99e6e250342851aea6860164b6f6af54818d1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78575948"
---
# <a name="deploying-web-packages"></a>Nasazení webových balíčků

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak můžete publikovat balíčky pro nasazení webu na vzdáleném serveru pomocí nástroje pro nasazení webu Internetová informační služba (IIS) (Nasazení webu) 2,0.
> 
> Existují dva hlavní způsoby, kterými můžete nasadit webový balíček na vzdálený server:
> 
> - Můžete použít nástroj příkazového řádku MSDeploy. exe přímo.
> - Můžete spustit soubor *[název projektu]. deploy. cmd* , který generuje proces sestavení.
> 
> Konečný výsledek je stejný bez ohledu na to, který přístup používáte. V podstatě se souborem *. deploy. cmd* spouští soubor MSDeploy. exe s některými předem určenými hodnotami, takže nemusíte poskytovat tolik informací, než aby bylo možné balíček nasadit. Tím se zjednoduší proces nasazení. Na druhé straně použití souboru MSDeploy. exe přímo přináší větší flexibilitu nad přesně tím, jak je balíček nasazený.
> 
> To, jaký přístup použijete, bude záviset na nejrůznějších faktorech, včetně toho, kolik ovládacích prvků vyžadujete v rámci procesu nasazení a zda cílíte na Nasazení webu službu vzdáleného agenta nebo obslužnou rutinu Nasazení webu. Toto téma vysvětluje, jak použít jednotlivé postupy a které identifikují, kdy je každý přístup vhodný.
> 
> V úlohách a návodech v tomto tématu se předpokládá, že:
> 
> - Vaše webová aplikace je sestavená a zabalená, jak je popsáno v tématu [sestavování a balení projektů webových aplikací](building-and-packaging-web-application-projects.md).
> - Změnili jste soubor *SetParameters. XML* , který poskytuje správné hodnoty parametrů pro cílové prostředí, jak je popsáno v tématu [Konfigurace parametrů pro nasazení webového balíčku](configuring-parameters-for-web-package-deployment.md).

Spuštění souboru [*název projektu*] *. deploy. cmd* je nejjednodušší způsob, jak nasadit webový balíček. Konkrétně použití souboru *. deploy. cmd* nabízí tyto výhody při použití nástroje msdeploy. exe přímo:

- Není nutné zadávat umístění balíčku&#x2014;pro nasazení webu. *Deploy. cmd* již ví, kde se nachází.
- Nemusíte určovat umístění souboru&#x2014; *SetParameters. XML* , který soubor *. deploy. cmd* již ví, kde je.
- Nemusíte určovat zdrojový a cílový poskytovatelé&#x2014;MSDeploy, který soubor *. deploy. cmd* už ví, které hodnoty se mají použít.
- Nemusíte určovat nastavení&#x2014;operace MSDeploy. soubor *. deploy. cmd* přidá obvykle požadované hodnoty do příkazu MSDeploy. exe automaticky.

Předtím, než použijete soubor *. deploy. cmd* k nasazení webového balíčku, je nutné zajistit, aby:

- Soubor *. deploy. cmd* , [*název projektu*]. *SetParameters. XML* soubor a webový balíček ([*název projektu*]. *zip*) jsou ve stejné složce.
- V počítači se spuštěným souborem *. deploy. cmd* je nainstalovaná nasazení webu (msdeploy. exe).

Soubor *. deploy. cmd* podporuje různé možnosti příkazového řádku. Když soubor spustíte z příkazového řádku, jedná se o základní syntaxi:

[!code-console[Main](deploying-web-packages/samples/sample1.cmd)]

Je nutné zadat příznak **/t** nebo příznak **/y** , aby bylo možné určit, zda chcete provést zkušební spuštění nebo živé nasazení (nepoužívejte oba příznaky ve stejném příkazu). Tato tabulka vysvětluje účel každého z těchto příznaků.

| Příznak | Popis |
| --- | --- |
| **Parametr** | Volá MSDeploy. exe s příznakem **-whatIf** , který indikuje zkušební běh. Místo nasazení balíčku vytvoří zprávu o tom, co se stane, když jste balíček nasadili. |
| **/Y** | Zavolá MSDeploy. exe bez příznaku **– whatIf** . Tím se balíček nasadí do místního počítače nebo na určený cílový server. |
| **Řetězec** | Určuje název cílového serveru nebo adresu URL služby. Další informace o hodnotách, které tady můžete zadat, najdete v části věnované **hlediskům koncových bodů** v tomto tématu. Pokud vynecháte příznak **/m** , balíček se nasadí do místního počítače. |
| **Parametr** | Určuje typ ověřování, který má soubor MSDeploy. exe použít k provedení nasazení. Možné hodnoty jsou **NTLM** a **Basic**. Pokud vynecháte příznak **/a** , typ ověřování se ve výchozím nastavení použije na **NTLM** pro nasazení do služby nasazení webu vzdáleného agenta a na **Basic** pro nasazení do nasazení webu obslužné rutiny. |
| **Přepínač** | Určuje uživatelské jméno. To platí jenom v případě, že používáte základní ověřování. |
| **/P** | Určuje heslo. To platí jenom v případě, že používáte základní ověřování. |
| **/L** | Označuje, že balíček by měl být nasazený do místní instance IIS Express. |
| **/G** | Určuje, že je balíček nasazený pomocí [Nastavení poskytovatele tempAgent](https://technet.microsoft.com/library/ee517345(WS.10).aspx). Vynecháte-li příznak **/g** , hodnota je nastavena na hodnotu **false**. |

> [!NOTE]
> Pokaždé, když proces sestavení vytvoří webový balíček, vytvoří také soubor s názvem *[název projektu]. deploy-Readme. txt* , který tyto možnosti nasazení vysvětluje.

Kromě těchto příznaků můžete zadat nastavení operace Nasazení webu jako další parametry *. deploy. cmd* . Všechna další nastavení, která zadáte, se jednoduše přenesou do základního příkazu MSDeploy. exe. Další informace o těchto nastaveních najdete v tématu [nastavení operace nasazení webu](https://technet.microsoft.com/library/dd569089(WS.10).aspx).

Předpokládejme, že chcete nasadit projekt webové aplikace ContactManager. Mvc do testovacího prostředí spuštěním souboru *. deploy. cmd* . Vaše testovací prostředí je nakonfigurované tak, aby používalo službu Nasazení webu Remote Agent, jak je popsáno v tématu [Konfigurace webového serveru pro nasazení webu publikování (vzdálený Agent)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md). Chcete-li nasadit webovou aplikaci, je nutné provést následující kroky.

**Nasazení webové aplikace pomocí souboru. deploy. cmd**

1. Sestavte a zabalit projekt webové aplikace, jak je popsáno v tématu [sestavování a balení projektů webových aplikací](building-and-packaging-web-application-projects.md).
2. Upravte soubor *ContactManager. Mvc. SetParameters. XML* tak, aby obsahoval správné hodnoty parametrů pro testovací prostředí, jak je popsáno v tématu [Konfigurace parametrů pro nasazení webového balíčku](configuring-parameters-for-web-package-deployment.md).
3. Otevřete okno příkazového řádku a přejděte do umístění souboru *ContactManager. Mvc. deploy. cmd* .
4. Zadejte tento příkaz a stiskněte klávesu ENTER:

    [!code-console[Main](deploying-web-packages/samples/sample2.cmd)]

V tomto příkladu:

- Příznak **/y** označuje, že chcete balíček skutečně nasadit, nikoli provést zkušební spuštění.
- Příznak **/m** označuje, že chcete balíček nasadit na server s názvem TESTWEB1. Z této hodnoty se nástroj MSDeploy. exe pokusí nasadit balíček do služby Nasazení webu Vzdálený agent na http://TESTWEB1/MSDeployAgentService.
- Příznak **/a** označuje, že chcete použít ověřování NTLM. V takovém případě nemusíte zadávat uživatelské jméno a heslo.

K ilustraci, jak použít soubor *. deploy. cmd* zjednodušuje proces nasazení, se podívejte na příkaz msdeploy. exe, který se vygeneroval a spustí při spuštění *ContactManager. Mvc. deploy. cmd* pomocí výše uvedených možností.

[!code-console[Main](deploying-web-packages/samples/sample3.cmd)]

Další informace o použití souboru *. deploy. cmd* pro nasazení webového balíčku naleznete v tématu [How to: install a Deployment Package by using a Deploy. cmd File](https://msdn.microsoft.com/library/ff356104.aspx).

## <a name="using-msdeployexe"></a>Použití souboru MSDeploy. exe

I když použití souboru *. deploy. cmd* obecně zjednodušuje proces nasazení, existují situace, kdy je vhodnější použít soubor MSDeploy. exe přímo. Příklad:

- Pokud chcete nasadit do obslužné rutiny Nasazení webu jako uživatel bez oprávnění správce, nemůžete použít soubor *. deploy. cmd* . Důvodem je chyba v Nasazení webu 2,0, jak je popsáno v části **požadavky na koncový bod**.
- Pokud chcete ručně přepínat mezi různými soubory *SetParameters. XML* v různých umístěních, můžete chtít použít soubor MSDeploy. exe přímo.
- Pokud chcete přepsat několik argumentů příkazového řádku MSDeploy. exe, můžete chtít použít soubor MSDeploy. exe přímo.

Pokud používáte soubor MSDeploy. exe, je třeba zadat tři klíčové informace:

- Parametr **– source** , který určuje, odkud data pocházejí.
- Parametr **– cílový** , který označuje, kde se data budou.
- A **– parametr příkazu** , který určuje [operaci](https://technet.microsoft.com/library/dd568989(WS.10).aspx) , kterou chcete provést.

MSDeploy. exe spoléhá na [zprostředkovatele nasazení webu](https://technet.microsoft.com/library/dd569040(WS.10).aspx) pro zpracování zdrojových a cílových dat. Nasazení webu obsahuje velké množství poskytovatelů, kteří představují rozsah aplikací a zdrojů dat, které může pracovat&#x2014;, například existují poskytovatelé pro databáze SQL Server, webové servery služby IIS, certifikáty, sestavení globální mezipaměti sestavení (GAC), různé různé konfigurační soubory a spoustu jiných typů dat. Parametr **– source** i parametr **-cíl** musí určovat zprostředkovatele ve formě **– zdroj**: [*ProviderName*] = [*Location*]. Pokud nasazujete webový balíček na web služby IIS, měli byste použít tyto hodnoty:

- Poskytovatel **– zdroj** je vždycky [zabalit](https://technet.microsoft.com/library/dd569019(WS.10).aspx). Příklad:

    [!code-console[Main](deploying-web-packages/samples/sample4.cmd)]
- Poskytovatel **– cíl** je vždycky [Automatický](https://technet.microsoft.com/library/dd569016(WS.10).aspx). Například:

    [!code-console[Main](deploying-web-packages/samples/sample5.cmd)]
- **Příkaz – příkaz** je vždy **Synchronizovaný**.

    [!code-console[Main](deploying-web-packages/samples/sample6.cmd)]

Kromě toho budete muset zadat různá [nastavení specifická pro konkrétního poskytovatele](https://technet.microsoft.com/library/dd569001(WS.10).aspx) a obecná [Nastavení operací](https://technet.microsoft.com/library/dd569089(WS.10).aspx). Předpokládejme například, že chcete nasadit webovou aplikaci ContactManager. Mvc do přípravného prostředí. Nasazení bude zacíleno na obslužnou rutinu Nasazení webu a musí používat základní ověřování. Chcete-li nasadit webovou aplikaci, je nutné provést následující kroky.

**Nasazení webové aplikace pomocí nástroje MSDeploy. exe**

1. Sestavte a zabalit projekt webové aplikace, jak je popsáno v tématu [sestavování a balení projektů webových aplikací](building-and-packaging-web-application-projects.md).
2. Upravte soubor *ContactManager. Mvc. SetParameters. XML* tak, aby obsahoval správné hodnoty parametrů vašeho přípravného prostředí, jak je popsáno v tématu [Konfigurace parametrů pro nasazení webového balíčku](configuring-parameters-for-web-package-deployment.md).
3. Otevřete okno příkazového řádku a přejděte do umístění souboru MSDeploy. exe. Obvykle se jedná o%PROGRAMFILES%\IIS\Microsoft Nasazení webu V2\msdeploy.exe.
4. Zadejte tento příkaz a potom stiskněte klávesu ENTER (neberete zalomení řádků):

    [!code-console[Main](deploying-web-packages/samples/sample7.cmd)]

V tomto příkladu:

- Parametr **– source** Určuje poskytovatele **balíčku** a označuje umístění webového balíčku.
- Parametr **– cíl** Určuje **automatického** zprostředkovatele. Nastavení **ComputerName** poskytuje adresu URL služby nasazení webu obslužné rutiny na cílovém serveru. Nastavení **typ authType** označuje, že chcete použít základní ověřování a že je třeba zadat **uživatelské jméno** a **heslo**. Nakonec nastavení **includeAcls = "false"** znamená, že nechcete kopírovat seznamy řízení přístupu (ACL) souborů ve zdrojové webové aplikaci na cílový server.
- Argument **– příkaz: Sync** označuje, že chcete replikovat zdrojový obsah na cílovém serveru.
- Argumenty **– disableLink** označují, že nechcete replikovat fondy aplikací, konfiguraci virtuálních adresářů nebo SSL (Secure SOCKETS Layer) (SSL) na cílovém serveru. Další informace najdete v tématu [rozšíření nasazení webu Links](https://technet.microsoft.com/library/dd569028(WS.10).aspx).
- Parametr **– setParamFile** poskytuje umístění souboru *SetParameters. XML* .
- Přepínač **– allowUntrusted** označuje, že nasazení webu by měl přijímat certifikáty SSL, které nebyly vydané důvěryhodnou certifikační autoritou. Pokud nasazujete do obslužné rutiny Nasazení webu a k zabezpečení adresy URL služby jste použili certifikát podepsaný svým držitelem, je nutné tento přepínač zahrnout.

## <a name="automating-web-package-deployment"></a>Automatizace nasazení webového balíčku

V rozsáhlých podnikových scénářích budete chtít nasadit webové balíčky jako součást rozsáhlejšího nebo automatizovaného nasazení. Bez ohledu na to, zda se rozhodnete nasadit webové balíčky, spuštěním souboru *. deploy. cmd* nebo pomocí příkazu MSDeploy. exe přímo, můžete příkazy parametrizovat a volat z cíle v souboru projektu Microsoft Build Engine (MSBuild).

V ukázkovém řešení Contact Manageru se podívejte na cíl **PublishWebPackages** v souboru *Publish. proj* . Tento cíl se spustí jednou pro každý soubor *. deploy. cmd* identifikovaný seznamem položek s názvem **PublishPackages**. Cíl pomocí vlastností a metadat položky sestaví úplnou sadu hodnot argumentů pro každý soubor *. deploy. cmd* a poté pomocí úlohy **exec** spustí příkaz.

[!code-xml[Main](deploying-web-packages/samples/sample8.xml)]

> [!NOTE]
> Další informace o modelu projektu projektu v ukázkovém řešení a Úvod do vlastních souborů projektu obecně naleznete v tématu [porozumění souboru projektu](understanding-the-project-file.md) a [porozumění procesu sestavení](understanding-the-build-process.md).

## <a name="endpoint-considerations"></a>Předpoklady pro koncové body

Bez ohledu na to, zda nasazujete webový balíček spuštěním souboru *. deploy. cmd* nebo pomocí příkazu MSDeploy. exe přímo, je nutné zadat název počítače nebo koncový bod služby pro nasazení.

Pokud je cílový webový server nakonfigurovaný pro nasazení pomocí služby Nasazení webu vzdáleného agenta, zadáte cílovou adresu URL služby jako cíl.

[!code-console[Main](deploying-web-packages/samples/sample9.cmd)]

Případně můžete zadat název serveru samostatně jako cíl a Nasazení webu odvodit adresu URL služby vzdáleného agenta.

[!code-console[Main](deploying-web-packages/samples/sample10.cmd)]

Pokud je cílový webový server nakonfigurovaný pro nasazení pomocí obslužné rutiny Nasazení webu, musíte jako cíl zadat adresu koncového bodu služby IIS Web Management (WMSvc). Ve výchozím nastavení má podobu:

[!code-console[Main](deploying-web-packages/samples/sample11.cmd)]

Libovolný z těchto koncových bodů můžete cílit přímo pomocí souboru *. deploy. cmd* nebo MSDeploy. exe. Pokud však chcete nasadit do obslužné rutiny Nasazení webu jako uživatel bez oprávnění správce, jak je popsáno v tématu [Konfigurace webového serveru pro nasazení webu publikování (nasazení webu obslužné rutiny)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md), je nutné přidat řetězec dotazu do adresy koncového bodu služby.

[!code-console[Main](deploying-web-packages/samples/sample12.cmd)]

Důvodem je to, že uživatel bez oprávnění správce nemá přístup na úrovni serveru ke službě IIS. má přístup jenom k určitému webu IIS. V době psaní se v důsledku chyby v kanálu publikování na webu (WPP) nedá spustit soubor *. deploy. cmd* pomocí adresy koncového bodu, která obsahuje řetězec dotazu. V tomto scénáři je nutné nasadit webový balíček přímo pomocí souboru MSDeploy. exe.

> [!NOTE]
> Další informace o Nasazení webu službě vzdáleného agenta a obslužné rutině Nasazení webu najdete v tématu [Volba správného přístupu k nasazení webu](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md). Pokyny ke konfiguraci souborů projektu specifických pro prostředí pro nasazení do těchto koncových bodů najdete v tématu [Konfigurace vlastností nasazení pro cílové prostředí](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).

## <a name="authentication-considerations"></a>Požadavky na ověření

Bez ohledu na to, zda nasazujete webový balíček spuštěním souboru *. deploy. cmd* nebo pomocí příkazu MSDeploy. exe přímo, je nutné zadat typ ověřování. Nasazení webu přijímá dvě možné hodnoty: **NTLM** nebo **Basic**. Pokud zadáte základní ověřování, musíte také zadat uživatelské jméno a heslo. Když vyberete typ ověřování, musíte mít na paměti různé faktory:

- Pokud nasazujete do služby Nasazení webu Vzdálený agent, musíte použít ověřování NTLM. Služba Vzdálený agent nepřijímá přihlašovací údaje základního ověřování.
- Pokud nasazujete do obslužné rutiny Nasazení webu, můžete použít buď ověřování NTLM, nebo základní ověřování. Výchozím nastavením je základní ověřování. I když základní ověřování spoléhá na uživatelská jména a hesla přenášená v prostém textu, vaše přihlašovací údaje jsou chráněné, protože Nasazení webu obslužná rutina vždy používá šifrování SSL.
- Pokud váš webový balíček obsahuje databázi a webový server a databázový server jsou samostatné počítače, nebudete moci nasadit databázi pomocí ověřování NTLM z důvodu [omezení "dvojího směrování NTLM](https://go.microsoft.com/?linkid=9805120)". Musíte použít SQL Server přihlašovací údaje v připojovacím řetězci nasazení nebo zadat přihlašovací údaje pro základní ověřování, které Nasazení webu. Tento problém je podrobněji popsaný v tématu [nasazení databází členství v podnikových prostředích](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md).

## <a name="conclusion"></a>Závěr

Toto téma popisuje, jak lze nasadit webový balíček buď spuštěním souboru *. deploy. cmd* nebo pomocí nástroje msdeploy. exe přímo. Vysvětluje, kdy může být každý přístup vhodný, a popisuje, jak můžete parametrizovat a spustit příkaz pro nasazení v rámci většího jednoho kroku nebo procesu automatického sestavování.

## <a name="further-reading"></a>Další čtení

Pokyny k vytvoření a použití webového balíčku pro nasazení najdete v tématu [sestavování a zabalení projektů webových aplikací](building-and-packaging-web-application-projects.md) a [Konfigurace parametrů pro nasazení webového balíčku](configuring-parameters-for-web-package-deployment.md). Pokyny k vytváření a nasazování webových balíčků z instance Team Foundation Server (TFS) najdete v tématu [konfigurace Team Foundation Server pro automatizované nasazení webu](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md). Informace o tom, jak přizpůsobit a řešit potíže s procesem nasazení, najdete v tématu [vyloučení souborů a složek z nasazení](../advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment.md).

> [!div class="step-by-step"]
> [Předchozí](configuring-parameters-for-web-package-deployment.md)
> [Další](deploying-database-projects.md)

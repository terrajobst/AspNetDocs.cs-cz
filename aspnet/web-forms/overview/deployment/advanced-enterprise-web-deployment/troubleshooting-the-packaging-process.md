---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
title: Řešení potíží s procesem balení | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak můžete shromáždit podrobné informace o procesu balení pomocí vlastnosti EnablePackageProcessLoggingAndAssert v M...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 794bd819-00fc-47e2-876d-fc5d15e0de1c
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
msc.type: authoredcontent
ms.openlocfilehash: 8ad649dfff085a8774cc13c11d8a3e3d48277d66
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628210"
---
# <a name="troubleshooting-the-packaging-process"></a>Řešení potíží s procesem vytváření balíčku

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak můžete shromáždit podrobné informace o procesu balení pomocí vlastnosti **EnablePackageProcessLoggingAndAssert** v Microsoft Build Engine (MSBuild).
> 
> Když nastavíte vlastnost **EnablePackageProcessLoggingAndAssert** na **hodnotu true**, MSBuild provede:
> 
> - Do protokolů sestavení přidejte další informace o procesu balení.
> - Protokoluje chyby za určitých podmínek, například pokud jsou v seznamu balení nalezeny duplicitní soubory.
> - Vytvořte adresář protokolu ve složce *ProjectName*\_balíčku a použijte ho k zaznamenání informací o souborech, které zabalíte.
> 
> Pokud se proces balíčku nedaří, nebo vaše balíčky pro nasazení webu neobsahují soubory, které očekáváte, můžete tyto informace použít k řešení potíží s procesem a určení, kde jsou věci chybné.
> 
> > [!NOTE]
> > Vlastnost **EnablePackageProcessLoggingAndAssert** funguje pouze v případě, že projekt sestavíte pomocí konfigurace **ladění** . Vlastnost je ignorována v jiných konfiguracích.

Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého [řešení](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.

Metoda nasazení na srdce těchto kurzů je založena na způsobu rozdělení souborů projektu popsaných v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md), ve kterém je proces sestavení řízen dvěma soubory&#x2014;projektu jeden, který obsahuje pokyny pro sestavení, které platí pro každé cílové prostředí, a jedno obsahující nastavení sestavení a nasazení specifické pro konkrétní prostředí. V době sestavení je soubor projektu specifický pro prostředí sloučen do souboru projektu prostředí – nezávislá a vytvoří kompletní sadu instrukcí pro sestavení.

## <a name="understanding-the-enablepackageprocessloggingandassert-property"></a>Princip vlastnosti EnablePackageProcessLoggingAndAssert

[Vytváření a balení projektů webových aplikací](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md) , které popisují, jak kanál pro publikování na webu (WPP) poskytuje sadu cílů MSBuild, které zvyšují funkčnost nástroje MSBuild a umožňují integraci s nástrojem Internetová informační služba (IIS) web pro nasazení webu (nasazení webu). Při zabalení projektu webové aplikace voláte cíle WPP.

Mnoho těchto cílů WPP zahrnuje podmíněnou logiku, která zapisuje Další informace, pokud je vlastnost **EnablePackageProcessLoggingAndAssert** nastavena na **hodnotu true**. Pokud například zkontrolujete cíl **balíčku** , vidíte, že vytvoří další adresář protokolu a zapíše seznam souborů do textového souboru, pokud je **EnablePackageProcessLoggingAndAssert** rovno hodnotě **true**.

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample1.xml)]

> [!NOTE]
> Cíle WPP jsou definované v souboru *Microsoft. Web. Publishing. targets* ve složce% ProgramFiles (x86)% \ MSBuild\Microsoft\VisualStudio\v10.0\Web. Tento soubor můžete otevřít a zkontrolovat cíle v aplikaci Visual Studio 2010 nebo v libovolném editoru XML. Je potřeba se starat o úpravu obsahu souboru.

## <a name="enabling-the-additional-logging"></a>Povolení dalšího protokolování

Hodnotu vlastnosti **EnablePackageProcessLoggingAndAssert** můžete určit různými způsoby v závislosti na tom, jak projekt sestavíte.

Pokud projekt sestavíte z příkazového řádku, můžete hodnotu vlastnosti **EnablePackageProcessLoggingAndAssert** dodat jako argument příkazového řádku:

[!code-console[Main](troubleshooting-the-packaging-process/samples/sample2.cmd)]

Pokud k sestavení projektů používáte vlastní soubor projektu, můžete zahrnout hodnotu **EnablePackageProcessLoggingAndAssert** do atributu **Properties (vlastnosti** ) úlohy **MSBuild** :

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample3.xml)]

Pokud k sestavení projektů používáte definici sestavení Team Foundation Server (TFS), můžete do řádku **argumenty msbuildu** zadejte hodnotu pro vlastnost **EnablePackageProcessLoggingAndAssert** :![](troubleshooting-the-packaging-process/_static/image1.png)

> [!NOTE]
> Další informace o vytváření a konfiguraci definic sestavení naleznete v tématu [Vytvoření definice sestavení, která podporuje nasazení](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md).

Případně, pokud chcete zahrnout balíček do každého sestavení, můžete upravit soubor projektu pro projekt webové aplikace a nastavit vlastnost **EnablePackageProcessLoggingAndAssert** na **hodnotu true**. Měli byste přidat vlastnost do prvního prvku **Property Property** v rámci souboru. csproj nebo. vbproj.

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample4.xml)]

## <a name="reviewing-the-log-files"></a>Kontrola souborů protokolu

Když sestavíte a zabalíte projekt webové aplikace s **EnablePackageProcessLoggingAndAssert** nastavenou na **hodnotu true**, nástroj MSBuild vytvoří další složku s názvem Log ve složce *ProjectName*\_balíčku. Složka protokolu obsahuje různé soubory:

![](troubleshooting-the-packaging-process/_static/image2.png)

Seznam souborů, které vidíte, se budou lišit v závislosti na akcích v projektu a procesu sestavení. Tyto soubory se ale obvykle používají k záznamu seznamu souborů, které WPP shromažďuje pro balení, v různých fázích procesu:

- Soubor *PreExcludePipelineCollectFilesPhaseFileList. txt* obsahuje seznam souborů, které nástroj MSBuild shromažďuje pro sbalení před odebráním souborů, které jsou určeny pro vyloučení.
- Soubor *AfterExcludeFilesFilesList. txt* obsahuje seznam upravených souborů po odebrání všech souborů, které jsou zadány pro vyloučení.

    > [!NOTE]
    > Další informace o vyloučení souborů a složek z procesu balení najdete v tématu [vyloučení souborů a složek z nasazení](excluding-files-and-folders-from-deployment.md).
- V souboru *AfterTransformWebConfig. txt* jsou uvedeny soubory shromážděné pro balení po provedení jakýchkoli transformací *Web. config* . V tomto seznamu jsou všechny transformační soubory *Web. config* specifické pro konkrétní konfiguraci, jako je *Web. Debug. config* a *Web. Release. config*, vyloučeny ze seznamu souborů pro balení. Na jejich místě je obsažen jediný transformovaný soubor *Web. config* .
- Soubor *PostAutoParameterizationWebConfigConnectionStrings. txt* obsahuje seznam souborů po připojovacích řetězcích v souboru *Web. config* , které byly parametrizované. To je proces, který umožňuje nahradit připojovací řetězce správným nastavením pro cílové prostředí při nasazení balíčku.
- Soubor připraveného souboru *. txt* obsahuje finální seznam souborů, které se mají zahrnout do balíčku.

> [!NOTE]
> Názvy dalších souborů protokolu obvykle odpovídají cílům WPP. Tyto cíle si můžete projít prozkoumáním souboru *Microsoft. Web. Publishing. targets* ve složce% ProgramFiles (x86)% \ MSBuild\Microsoft\VisualStudio\v10.0\Web.

Pokud obsah vašeho webového balíčku nevíte, co jste očekávali, může být při kontrole těchto souborů užitečný způsob, jak zjistit, v jakém okamžiku došlo k chybě.

## <a name="conclusion"></a>Závěr

Toto téma popisuje, jak můžete použít vlastnost **EnablePackageProcessLoggingAndAssert** v nástroji MSBuild k řešení potíží s procesem vytváření balíčků. Vysvětluje různé způsoby, kterými můžete zadat hodnotu vlastnosti procesu sestavení a popisuje další informace, které jsou zaznamenány při nastavení vlastnosti na **hodnotu true**.

## <a name="further-reading"></a>Další čtení

Další informace o použití vlastních souborů projektu MSBuild pro řízení procesu nasazení naleznete v tématu [porozumění souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md) a [porozumění procesu sestavení](../web-deployment-in-the-enterprise/understanding-the-build-process.md). Další informace o WPP a o tom, jak spravuje proces balení, naleznete v tématu [sestavování a balení projektů webových aplikací](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md). Pokyny, jak vyloučit konkrétní soubory a složky z balíčků pro nasazení webu, najdete v tématu [vyloučení souborů a složek z nasazení](excluding-files-and-folders-from-deployment.md).

> [!div class="step-by-step"]
> [Předchozí](running-windows-powershell-scripts-from-msbuild-project-files.md)

---
uid: whitepapers/aspnet-web-deployment-content-map
title: Nasazení webu ASP.NET – doporučené prostředky | Microsoft Docs
author: rick-anderson
description: Toto téma obsahuje odkazy na materiály k dokumentaci týkající se nasazení (publikování) ASP.NET webových aplikací do služby IIS pomocí sady Visual Studio 2010, Visual Web de...
ms.author: riande
ms.date: 03/14/2014
ms.assetid: 58b583cd-c4ab-47a3-8527-8c92c298c91f
msc.legacyurl: /whitepapers/aspnet-web-deployment-content-map
msc.type: content
ms.openlocfilehash: 96873c8f2b0ad2415f371aceb651400c801a3338
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78636988"
---
# <a name="aspnet-web-deployment---recommended-resources"></a>Nasazení webu ASP.NET – doporučené zdroje informací

> Toto téma obsahuje odkazy na materiály k dokumentaci týkající se nasazení (publikování) ASP.NET webových aplikací do služby IIS pomocí sady Visual Studio 2010, Visual Web Developer 2010 a novějších verzí.
> 
> Pokud znáte skvělý Blogový příspěvek, vlákno [StackOverflow](http://stackoverflow.com) nebo jakýkoli jiný odkaz, který by byl užitečný, [pošlete nám e-mail](mailto:aspnetue@microsoft.com?subject=Deployment%20Content%20Map) s odkazem.
> 
> > [!NOTE] 
> > 
> > Mnohé z těchto prostředků popisují funkce nasazení, které jsou k dispozici pouze v případě, že instalujete poslední vydání [aktualizace publikování webu sady Visual Studio](https://go.microsoft.com/fwlink/?LinkID=208120). Některé funkce jsou k dispozici pouze v aplikaci Visual Studio 2012 nebo Visual Studio 2013.

Toto téma obsahuje následující oddíly:

- [Principy možností nasazení pro webové projekty](#understanding)
- [Hledání zprostředkovatelů hostování pro aplikaci ASP.NET](#findinghosting)
- [Nasazení webové aplikace ze sady Visual Studio](#fromvs)
- [Nasazení webové aplikace vytvořením a instalací balíčku pro nasazení webu](#package)
- [Nasazení webové aplikace pomocí procesu průběžné integrace (CI)](#ci)
- [Použití transformací Web. config ke změně nastavení v cílovém souboru Web. config nebo App. config během nasazení](#transforms)
- [Použití parametrů Nasazení webu ke změně nastavení v cílové webové aplikaci během nasazení](#webdeployparms)
- [Ověření, že je aplikace v průběhu nasazení mimo řádek](#appoffline)
- [Nasazení databáze nebo změn v databázi jako součást nasazení webové aplikace](#databasewithweb)
- [Nasazení databáze odděleně od nasazení webové aplikace](#databaseseparate)
- [Nasazení webové aplikace, která používá ASP.NET Application Services, jako je například členství a profilace](#aspnetmembership)
- [Předkompilace pro nasazení](#precompiling)
- [Nasazení intranetové webové aplikace](#intranet)
- [Automatizace běžných úloh nasazení, které nejsou automatizovány](#automating)
- [Konfigurace webových serverů, aby vývojáři mohli do nich nasazovat webové aplikace pomocí Nasazení webu](#configuringservers)
- [Konfigurace serverů pro poskytovatele hostingu](#hostingprovider)
- [Řešení potíží s nasazením](#troubleshooting)
- [Získání Nápověda ke konkrétní otázce nasazení](#gettinghelp)
- [Další zdroje](#additional)

<a id="understanding"></a>

## <a name="understanding-deployment-options-for-web-projects"></a>Principy možností nasazení pro webové projekty

- [Přehled nasazení webu pro Visual Studio a ASP.NET](https://msdn.microsoft.com/library/dd394698.aspx) (MSDN).
- [Postup nasazení webu Windows Azure](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy). Vysvětluje možnosti a odkazy na prostředky pro nasazení webových projektů do webů Windows Azure, včetně [průběžného doručování](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) (automatizovaného ze [správy zdrojového kódu](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)) a také při používání sady Visual Studio.
- [Vylepšení publikování na webu sady Visual Studio 2012](../visual-studio/overview/2012/visual-studio-2012-web-publishing-improvements.md) (video od Scottu Hanselman).
- [Přehled příspěvku pro nasazení webu v VS 2010](http://vishaljoshi.blogspot.com/2009/09/overview-post-for-web-deployment-in-vs.html) (blog Vishal Joshi). Starší Blogový příspěvek, ale některé z prostředků sady Visual Studio 2010 odkazuje na informace, které jsou stále relevantní pro sadu Visual Studio 2012.

<a id="findinghosting"></a>

## <a name="finding-hosting-providers-for-an-aspnet-application"></a>Hledání zprostředkovatelů hostování pro aplikaci ASP.NET

- [Hostování ASP.NET](https://asp.net/hosting)

<a id="fromvs"></a>

## <a name="deploying-a-web-application-from-visual-studio"></a>Nasazení webové aplikace ze sady Visual Studio

- [Postup nasazení webu Windows Azure](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy). Vysvětluje možnosti a obsahuje odkazy na zdroje pro nasazení webových projektů do webů Windows Azure. Obsahuje část o nasazení ze sady Visual Studio.
- [ASP.NET nasazení webu pomocí sady Visual Studio](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md). 12. série kurzů ukazuje, jak nasadit webové aplikace s využitím SQL Serverch databází. Pro nasazení databáze používá poskytovatele dbDacFx i Migrace Entity Framework Code First. Obsahuje také informace o [transformacích souborů Web. config](../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md), [nasazování jednotlivých souborů](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md#specificfiles), [nasazení z příkazového řádku](../web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment.md)a [způsobu přizpůsobení kanálu publikování webu sady Visual Studio úpravou souborů. pubxml](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files.md). Platí pro všechny webové projekty ASP.NET, včetně webových formulářů, MVC a webového rozhraní API.)
- [Postupy: nasazení webového projektu pomocí publikování jedním kliknutím v aplikaci Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx) (referenční informace pro Průvodce publikováním webu sady Visual Studio)
- [Nasazení webové aplikace v ASP.NET s SQL Server Compact pomocí sady Visual Studio](../web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md). Toto je starší verze **nasazení webu ASP.NET pomocí sady Visual Studio** , která je uvedená v horní části této části. Hlavně užitečné pro informace o tom, jak nasadit databáze SQL Server Compact a jak migrovat z SQL Server Compact na plnou edici SQL Server.
- [Vícevrstvá aplikace .NET, která používá tabulky, fronty a objekty blob služby úložiště](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36) (Microsoft Azure lokality). 5\. série kurzů ukazuje, jak vytvořit projekt MVC a jak ho nasadit do cloudové služby Microsoft Azure.

<a id="package"></a>
## <a name="deploying-a-web-application-by-creating-and-installing-a-web-deployment-package"></a>Nasazení webové aplikace vytvořením a instalací balíčku pro nasazení webu

- [Postupy: vytvoření balíčku pro nasazení webu v aplikaci Visual Studio](https://msdn.microsoft.com/library/dd465323.aspx) (MSDN).
- [Postupy: instalace balíčku pro nasazení pomocí souboru Deploy. cmd vytvořeného pomocí sady Visual Studio](https://msdn.microsoft.com/library/ff356104.aspx) (MSDN).
- [Použití nasazení webu balíčku pro nasazení do služby IIS v poli pro vývoj a na hostitele třetí strany](http://sedodream.com/2011/11/08/UsingAWebDeployPackageToDeployToIISOnTheDevBoxAndToAThirdPartyHost.aspx) (blog Hashimi pro Sayed). Jak použít Správce služby IIS k instalaci balíčku pro nasazení do služby IIS v místním počítači a v hostující společnosti, která podporuje Správce služby IIS pro vzdálenou správu.
- [Sestavení balíčku nasazení webu ze sady Visual Studio 2010](https://www.iis.net/learn/publish/using-web-deploy/building-a-web-deploy-package-from-visual-studio-2010) (web IIS.NET). Obsahuje pokyny pro vytvoření a instalaci balíčku příkazového řádku.
- [Sbalení po publikování kdekoli](http://sedodream.com/2012/03/14/PackageWebUpdatedAndVideoBelow.aspx) (blog Sayed Hashimi) Zavádí balíček NuGet, který automatizuje proces transformace souboru Web. config pro více cílových prostředí, takže můžete nasadit jeden balíček na více serverů. Viz také [PackageWeb video](https://www.youtube.com/watch?v=-LvUJFI8CzM) podle Sayed Hashimi.

Viz také následující část.

<a id="ci"></a>

## <a name="deploying-a-web-application-using-a-continuous-integration-ci-process"></a>Nasazení webové aplikace pomocí procesu průběžné integrace (CI)

- [Průběžná integrace a průběžné doručování (vytváření skutečných cloudových aplikací s využitím Windows Azure).](../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) Kapitola E-knihy, která zavádí průběžnou integraci a průběžné doručování.
- [Postup nasazení webu Windows Azure](https://docs.microsoft.com/azure/app-service-web/web-sites-deploy). Vysvětluje možnosti a odkazy na prostředky pro nasazení webových projektů do webů Windows Azure. Obsahuje část týkající se automatizace nasazení ze správy zdrojového kódu.
- [Nasazení webových aplikací v podnikových scénářích](../web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md). Série kurzů 40 – část ukazuje, jak automatizovat nasazení v procesu CI pomocí sady Visual Studio 2010 a Team Foundation Server 2010.
- [Uvnitř Microsoft Build Engine: použití nástroje MSBuild a Team Foundation Build, od Sayed Hashimi a William Bartholomew](http://msbuildbook.com). Toto je kniha, nikoli webový prostředek, ale je to základní průvodce pro učení, jak nakonfigurovat nástroj MSBuild pro scénáře průběžné integrace.
- [Balíček rozšíření MSBuild](https://github.com/mikefourie/MSBuildExtensionPack). Zahrnuje úlohy nasazení.
- [Průvodce vlastním nastavením sestavení Team Foundation](https://aka.ms/vsarsolutions). Dokumentace podle ALM v sestavách Team Foundation Server pokrývá nasazení webu a zahrnuje kurzy a videa.
- [SlowCheetah transformace XML ze serveru CI](http://sedodream.com/2011/12/12/SlowCheetahXMLTransformsFromACIServer.aspx) (blog Sayed Hashimi). Vysvětluje, jak používat SlowCheetah, Visual Studio Add-in pro transformaci App. config a dalších souborů XML.

Viz také informace o tom, [zda je aplikace v průběhu nasazení](aspnet-web-deployment-content-map.md#appoffline) v pozdější době na této stránce.

<a id="transforms"></a>

## <a name="using-webconfig-transformations-to-change-settings-in-the-destination-webconfig-file-or-appconfig-file-during-deployment"></a>Použití transformací Web. config ke změně nastavení v cílovém souboru Web. config nebo App. config během nasazení

- [Transformace souboru Web. config](../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md).
- [Syntaxe transformace Web. config pro nasazení webového projektu pomocí sady Visual Studio](https://msdn.microsoft.com/library/dd465326.aspx) (MSDN).
- [Web Tools 2012,2 – transformace Web. config](https://www.youtube.com/watch?v=HdPK8mxpKEI) (YouTube video podle Sayed Hashimi). Ukazuje, jak nastavit a zobrazit náhled transformací Web. config.
- [Návody zakázat transformaci souboru Web. config?](https://msdn.microsoft.com/library/ee942158.aspx#disable_web_config_transformation) (MSDN).
- [Kdy použít Nasazení webu parametry namísto transformací Web. config?](https://msdn.microsoft.com/library/ee942158.aspx#web_deploy_parameters) (MSDN).
- [Xdt (transformace dokumentu XML) vydané na CodePlex.com](https://blogs.msdn.com/b/webdev/archive/2013/04/23/xdt-xml-document-transform-released-on-codeplex-com.aspx) (blog pro vývoj webových aplikací a nástrojů .NET). Oznamuje dostupnost zdrojového kódu pro transformační modul souboru Web. config a uvádí některé nástroje, které ho používají.
- [Weby Windows Azure: jak fungují řetězce aplikace a připojovací řetězce](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx) (Microsoft Azure blog). Alternativa k souboru Web. config transformuje, jestli vaše cílové prostředí používá weby Windows Azure a chcete transformovat `appSettings` nebo `connectionStrings`.

<a id="webdeployparms"></a>

## <a name="using-web-deploy-parameters-to-change-settings-in-the-destination-web-application-during-deployment"></a>Použití parametrů Nasazení webu ke změně nastavení v cílové webové aplikaci během nasazení

- [Postupy: použití parametrů nasazení webu v balíčku pro nasazení webu](https://msdn.microsoft.com/library/ff398068.aspx) (MSDN).
- [MSDeploy: jak aktualizovat nastavení aplikace při publikování na základě profilu publikování](http://sedodream.com/2013/03/02/MSDeployHowToUpdateAppSettingsOnPublishBasedOnThePublishProfile.aspx) (blog Sayed Hashimi). Ukazuje, jak integrovat parametry nasazení webu do profilů publikování v aplikaci Visual Studio.
- [Nasazení webu Parametrizace](https://www.iis.net/learn/publish/using-web-deploy/web-deploy-parameterization) (IIS.NET Web).
- [Nasazení webu parametrizace v akci](http://vishaljoshi.blogspot.com/2010/07/web-deploy-parameterization-in-action.html) (blog Vishal Joshi).
- [Nasazení webu transformaci Parametrizace vs. Web. config](http://vishaljoshi.blogspot.com/2010/06/parameterization-vs-webconfig.html) (blog Vishal Joshi).
- [Weby Windows Azure: jak fungují řetězce aplikace a připojovací řetězce](https://blogs.msdn.com/b/windowsazure/archive/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work.aspx) (Microsoft Azure blog). Alternativa k parametrům nasazení webu, pokud je vaše cílové prostředí weby Windows Azure a chcete parametrizovat `appSettings` nebo `connectionStrings`.

<a id="appoffline"></a>

## <a name="making-sure-an-application-is-off-line-during-deployment"></a>Ověření, že je aplikace v průběhu nasazení mimo řádek

- [Nasazení webu ASP.NET pomocí sady Visual Studio: nasazení aktualizace kódu](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md). Přečtěte si část **použití aplikace při nasazení v režimu offline.**
- [Převedení aplikace do režimu offline před publikováním](https://www.iis.net/learn/publish/deploying-application-packages/taking-an-application-offline-before-publishing) (IIS.NET Web) Vysvětluje funkci integrovanou do Nasazení webu 3,0, která automatizuje zpracování aplikace\_offline souboru. htm. Tato funkce nefunguje s vlastní aplikací\_offline soubory. htm.
- [Jak převést svou webovou aplikaci do offline režimu během publikování](http://sedodream.com/2012/01/08/HowToTakeYourWebAppOfflineDuringPublishing.aspx) (blog Sayed Hashimi). Postup automatizace procesu použití vlastní aplikace\_offline souboru. htm.
- [Aktualizace publikování na webu pro aplikace v režimu offline a usechecksum](https://blogs.msdn.com/b/webdev/archive/2013/10/30/web-publishing-updates-for-app-offline-and-usechecksum.aspx) (blog pro vývoj webů Microsoftu) Další možností pro automatizaci použití aplikace\_offline souboru. htm.
- [Nasazení webu 3,5 RTW](https://blogs.iis.net/msdeploy/archive/2013/07/09/webdeploy-3-5-rtw.aspx) (web IIS.NET). Nová funkce v Nasazení webu 3,5 pro vlastní aplikace\_offline soubory. htm.

<a id="databasewithweb"></a>

## <a name="deploying-a-database-or-changes-to-a-database-as-part-of-web-application-deployment"></a>Nasazení databáze nebo změn v databázi jako součást nasazení webové aplikace

- [Konfigurace nasazení databáze v aplikaci Visual Studio](https://msdn.microsoft.com/library/dd394698.aspx#dbdeployment) (MSDN). Přehled možností pro nasazení databáze pomocí webového projektu.
- [ASP.NET nasazení webu pomocí sady Visual Studio](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md). 12 částí série kurzů, zobrazení nasazení databáze pomocí poskytovatele dbDacFx a Migrace Entity Framework Code First.
- [Postupy: nasazení webového projektu pomocí publikování jedním kliknutím v aplikaci Visual Studio](https://msdn.microsoft.com/library/dd465337.aspx) (MSDN).
- [Nasaďte zabezpečenou aplikaci ASP.NET MVC 5 s členstvím, protokolem OAuth a SQL Database na web Windows Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Dlouhý kurz, který sestaví a nasadí aplikaci, která používá jednu SQL Server databázi jak pro data členství, tak pro data aplikací.
- [Nasazení webové aplikace v ASP.NET s SQL Server Compact pomocí sady Visual Studio](../web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md). 12. série kurzů ukazuje, jak nasadit databáze SQL Server Compact a jak migrovat z SQL Server Compact na plnou edici SQL Server.

Viz také nasazení webové aplikace vytvořením a instalací balíčku pro nasazení webu a nasazení webové aplikace pomocí procesu průběžné integrace (CI) dříve na této stránce.

<a id="databaseseparate"></a>

## <a name="deploying-a-database-separately-from-web-application-deployment"></a>Nasazení databáze odděleně od nasazení webové aplikace

- [Nástroje pro SQL Server Data Tools](https://msdn.microsoft.com/library/hh272686(v=vs.103).aspx) (MSDN).
- [Zahrnutí dat do projektu databáze SQL Server](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx) (blog týmu SQL Server Data Tools). Jak nasadit schéma i data při nasazení databáze.
- [Jak nasadit databázi do Windows Azure](https://docs.microsoft.com/azure/sql-database/sql-database-cloud-migrate) (Microsoft Azure Web)
- [Migrují se databáze do Windows Azure SQL Database (dřív SQL Azure)](https://msdn.microsoft.com/library/windowsazure/ee730904.aspx) (MSDN).
- [Migrace databáze do SQL Azure pomocí SSDT](https://blogs.msdn.com/b/ssdt/archive/2012/04/19/migrating-a-database-to-sql-azure-using-ssdt.aspx) (blog týmu nástroje SQL Server data).
- [Migrace aplikací orientovaných na data do Windows Azure](https://msdn.microsoft.com/library/jj156154.aspx) (MSDN).
- [Migrace SQL Server databází do Windows Azure SQL Database](https://msdn.microsoft.com/library/windowsazure/jj156160.aspx) (MSDN).

<a id="aspnetmembership"></a>

## <a name="deploying-a-web-application-that-uses-aspnet-application-services-such-as-membership-and-profiling"></a>Nasazení webové aplikace, která používá ASP.NET Application Services, jako je například členství a profilace

- [Nasaďte zabezpečenou aplikaci ASP.NET MVC 5 s členstvím, protokolem OAuth a SQL Database na web Windows Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data). Dlouhý kurz, který sestaví a nasadí aplikaci, která používá jednu SQL Server databázi jak pro data členství, tak pro data aplikací.
- [ASP.NET identity](https://asp.net/identity/). Prostředky pro ASP.NET Identity.
- [ASP.NET nasazení webu pomocí sady Visual Studio](../web-forms/overview/deployment/visual-studio-web-deployment/introduction.md). 12. série kurzů ukazuje, jak nasadit databázi členství v ASP.NET.
- [Konfigurace webu, který používá aplikační služby](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/configuring-a-website-that-uses-application-services-cs.md). Pro projekty webu, ale také relevantní pro projekty webových aplikací.
- [Uživatelé a role na provozním webu](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/users-and-roles-on-the-production-website-cs.md). Pro projekty webu, ale také relevantní pro projekty webových aplikací.

<a id="precompiling"></a>

## <a name="precompiling-for-deployment"></a>Předkompilace pro nasazení

- [Přehled Předkompilace projektu webové aplikace ASP.NET](https://msdn.microsoft.com/library/aa983464.aspx) (MSDN)
- [Karta Balení/publikování webu, vlastnosti projektu](https://msdn.microsoft.com/library/dd410108.aspx) (MSDN).
- [Dialogové okno Pokročilé nastavení předkompilace](https://msdn.microsoft.com/library/hh475319.aspx) (MSDN).

<a id="intranet"></a>

## <a name="deploying-an-intranet-web-application"></a>Nasazení intranetové webové aplikace

- [Použijte možnost místní ověřování organizace (ADFS) s ASP.NET v Visual Studio 2013](http://www.cloudidentity.com/blog/2014/02/12/use-the-on-premises-organizational-authentication-option-adfs-with-asp-net-in-visual-studio-2013/) (blog Vittorio Bertocci.).
- [Vytvoření intranetového webu pomocí ASP.NET MVC](https://msdn.microsoft.com/library/gg703322(VS.98).aspx) (MSDN). Starší návod WRITEN pro Visual Studio 2010 neodráží významné změny v šablonách projektů v intranetu, které jsou představené v Visual Studio 2013.

<a id="automating"></a>

## <a name="automating-common-deployment-tasks-that-are-not-automated-out-of-the-box"></a>Automatizace běžných úloh nasazení, které nejsou automatizovány

- [ASP.NET nasazení webu pomocí sady Visual Studio: nasazování dalších souborů](../web-forms/overview/deployment/visual-studio-web-deployment/deploying-extra-files.md).
- [Nastavení oprávnění složky na webu publikovat](http://sedodream.com/2011/11/08/SettingFolderPermissionsOnWebPublish.aspx) (Sayed Hashimi 's blog).
- [Postup rozšiřování souboru cílů tak, aby zahrnoval nastavení registru pro balíček webového projektu](https://blogs.msdn.com/webdevtools/archive/2010/02/09/how-to-extend-target-file-to-include-registry-settings-for-web-project-package.aspx) (blog nástrojů pro vývoj webu).
- [Rozšíření transformace XML (Web. config)](http://sedodream.com/2010/09/09/ExtendingXMLWebconfigConfigTransformation.aspx) (blog Sayed Hashimi). Ukazuje, jak vytvořit vlastní transformace XDT.
- [Vlastní zprostředkovatel nástroje pro nasazení webu (MSDeploy) přijímá 1](http://sedodream.com/2010/03/11/WebDeploymentToolMSDeployCustomProviderTake1.aspx) (blog Sayed Hashimi). Ukazuje, jak vytvořit vlastního poskytovatele Nasazení webu.
- [Jak zabalit a nasadit komponenty modelu COM](https://blogs.msdn.com/webdevtools/archive/2010/03/03/how-to-package-and-deploy-com-component.aspx) (blog webové nástroje pro vývoj)
- [Jak zabalit sestavení .NET](https://blogs.msdn.com/webdevtools/archive/2010/02/19/how-to-package-com-component.aspx) (blog webové vývojové nástroje). Jak nasadit sestavení do globální mezipaměti sestavení (GAC).
- Vyhledá [vše – inicializujte si virtuální počítač s Windows Azure pro svůj webový server se službou IIS, nasazení webu a dalšími věci](http://www.tugberkugurlu.com/archive/script-out-everything-initialize-your-windows-azure-vm-for-your-web-server-with-iis-web-deploy-and-other-stuff) (blog Ugurlu pro Tugberk).

<a id="configuringservers"></a>

## <a name="configuring-web-servers-so-that-developers-can-deploy-web-applications-to-them-using-web-deploy"></a>Konfigurace webových serverů, aby vývojáři mohli do nich nasazovat webové aplikace pomocí Nasazení webu

- [Instalace a konfigurace nasazení webu pro nasazení správců a jiných správců](https://www.iis.net/learn/install/installing-publishing-technologies/installing-and-configuring-web-deploy) (web IIS.NET).

<a id="hostingprovider"></a>

## <a name="configuring-servers-for-a-hosting-provider"></a>Konfigurace serverů pro poskytovatele hostingu

- [Microsoft ASP.NET 4 Průvodce nasazením hostování](https://go.microsoft.com/fwlink/?LinkId=191365) (Stažení softwaru společnosti Microsoft).
- [Vygeneruje soubor XML profilu](https://www.iis.net/learn/web-hosting/joining-the-web-hosting-gallery/generate-a-profile-xml-file) (web IIS.NET).

<a id="troubleshooting"></a>

## <a name="troubleshooting-deployment-problems"></a>Řešení potíží s nasazením

- [Řešení potíží s weby Windows Azure v aplikaci Visual Studio](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio) (Microsoft Azure lokality).
- [ASP.NET nasazení webu pomocí sady Visual Studio: řešení potíží](../web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting.md).
- [Řešení běžných potíží s nasazení webu](https://www.iis.net/learn/publish/troubleshooting-web-deploy/troubleshooting-common-problems-with-web-deploy).
- [Kódy chyb nasazení webu](https://www.iis.net/learn/publish/troubleshooting-web-deploy/web-deploy-error-codes) (web IIS.NET).
- [Nejčastější dotazy k nasazení webu pro Visual Studio a ASP.NET](https://msdn.microsoft.com/library/ee942158.aspx) (MSDN).
- [Základní rozdíly mezi službou IIS a vývojovým serverem ASP.NET](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md)
- [Běžné rozdíly v konfiguraci mezi vývojem a výrobou](../web-forms/overview/older-versions-getting-started/deploying-web-site-projects/common-configuration-differences-between-development-and-production-cs.md).
- [Hostování aplikací ASP.NET ve středním vztahu důvěryhodnosti](http://www.4guysfromrolla.com/articles/100307-1.aspx) (4 kyberbezpečnosti z webu Rolla).

<a id="gettinghelp"></a>

## <a name="getting-help-with-a-specific-deployment-question"></a>Získání Nápověda ke konkrétní otázce nasazení

- [Fórum pro konfiguraci a nasazení ASP.NET](https://forums.asp.net/26.aspx/1?Configuration and Deployment).
- [StackOverflow.com](http://www.StackOverflow.com).

<a id="additional"></a>

## <a name="additional-resources"></a>Další prostředky

V této části najdete odkazy na další zdroje informací, které jsou užitečné pro další informace o tom, jak používat Visual Studio a nástroje pro nasazení služby IIS.

Následující Blogy často obsahují informace o nasazení webu sady Visual Studio:

- [Vývojové nástroje pro web na blogu Microsoftu](https://blogs.msdn.com/b/webdevtools/).
- [Blog Sayed Hashimi](http://www.sedodream.com/)

Následující zdroje poskytují dokumentaci o Nasazení webu, rozhraní IIS, které Visual Studio používá k provádění úloh nasazení projektu webové aplikace. Otázky týkající se Nasazení webu můžete klást na [fóru nástroje Web Deployment](https://go.microsoft.com/fwlink/?LinkId=149411) na webu IIS.NET.

- [Seznámení s nasazení webu](https://www.iis.net/learn/publish/using-web-deploy/introduction-to-web-deploy).
- [Instalace a konfigurace nasazení webu](https://www.iis.net/learn/install/installing-publishing-technologies/installing-and-configuring-web-deploy).
- [Powershellové skripty pro automatizaci nasazení webuho nastavení](https://www.iis.net/learn/publish/using-web-deploy/powershell-scripts-for-automating-web-deploy-setup).
- [Nástroj pro nasazení webu](https://go.microsoft.com/fwlink/?LinkId=151481). Uzel obsahu nejvyšší úrovně pro Nasazení webu dokumentaci na webu TechNet. Obsahuje užitečné referenční informace, ale většina stránek TechNet se neaktualizovala na roky.
- [Obor názvů Microsoft. Web. Deployment](https://go.microsoft.com/fwlink/?LinkId=148630). Dokumentace k rozhraní API se od verze 1,0 neaktualizovala.
- [Blog týmu pro nasazení webu společnosti Microsoft](https://blogs.iis.net/msdeploy/default.aspx).
- [Karta publikovat na webu IIS.NET](https://www.iis.net/learn/publish).

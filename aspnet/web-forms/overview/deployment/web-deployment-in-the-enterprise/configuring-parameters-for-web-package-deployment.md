---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
title: Konfigurace parametrů pro nasazení webového balíčku | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak nastavit hodnoty parametrů, jako jsou názvy webových aplikací Internetová informační služba (IIS), připojovací řetězce a koncové body služby,...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 37947d79-ab1e-4ba9-9017-52e7a2757414
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
msc.type: authoredcontent
ms.openlocfilehash: f04ace98d81a33053b10cab7e40dbd75a6c0992c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544952"
---
# <a name="configuring-parameters-for-web-package-deployment"></a>Konfigurace parametrů nasazení webového balíčku

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak nastavit hodnoty parametrů, jako jsou názvy webových aplikací Internetová informační služba (IIS), připojovací řetězce a koncové body služby při nasazení webového balíčku na vzdálený webový server služby IIS.

Při sestavování projektu webové aplikace generuje proces sestavení a vytváření balíčku tři soubory klíče:

- Soubor *[název projektu]. zip* . Toto je balíček pro nasazení webu pro váš projekt webové aplikace. Tento balíček obsahuje všechna sestavení, soubory, databázové skripty a prostředky potřebné k opětovnému vytvoření webové aplikace na vzdáleném webovém serveru služby IIS.
- Soubor *[název projektu]. deploy. cmd* . Obsahuje sadu příkazů parametrizovaného Nasazení webu (MSDeploy. exe), které publikují balíček pro nasazení webu na vzdáleném webovém serveru služby IIS.
- *[Název projektu]. SetParameters. XML* soubor. To poskytuje sadu hodnot parametrů pro příkaz MSDeploy. exe. Hodnoty v tomto souboru můžete aktualizovat a předat Nasazení webu jako parametr příkazového řádku při nasazení webového balíčku.

> [!NOTE]
> Další informace o procesu sestavení a balení naleznete v tématu [sestavování a balení projektů webových aplikací](building-and-packaging-web-application-projects.md).

Soubor *SetParameters. XML* je dynamicky generován ze souboru projektu webové aplikace a všech konfiguračních souborů v rámci projektu. Když sestavíte a zabalíte svůj projekt, kanál pro publikování na webu (WPP) automaticky detekuje spoustu proměnných, které se pravděpodobně mění mezi prostředími nasazení, jako je cílová webová aplikace služby IIS a všechny databázové připojovací řetězce. Tyto hodnoty jsou automaticky parametrizované v balíčku pro nasazení webu a přidají se do souboru *SetParameters. XML* . Například pokud přidáte připojovací řetězec do souboru *Web. config* v projektu webové aplikace, proces sestavení tuto změnu detekuje a přidá odpovídající položku do souboru *SetParameters. XML* .

V mnoha případech bude tento automatický Parametrizace dostačující. Pokud ale uživatelé potřebují měnit jiná nastavení mezi prostředími nasazení, jako je nastavení aplikace nebo adresy URL koncového bodu služby, je potřeba sdělit, že WPP tyto hodnoty v balíčku pro nasazení, a přidat odpovídající položky do souboru *SetParameters. XML* . Následující části popisují, jak to provést.

### <a name="automatic-parameterization"></a>Automaticky Parametrizace

Při sestavování a zabalení webové aplikace bude funkce WPP tyto věci automaticky parametrizovat:

- Cesta a název cílové webové aplikace služby IIS.
- Všechny připojovací řetězce v souboru *Web. config* .
- Připojovací řetězce pro všechny databáze, které přidáte na kartu **Package/PUBLISH SQL** na stránkách vlastností projektu.

Pokud byste například chtěli sestavit a zabalit ukázkové řešení [Contact Manageru](the-contact-manager-solution.md) , aniž byste se dodotkli Parametrizace procesu jakýmkoli způsobem, modul WPP by vygeneroval tento *ContactManager soubor. Mvc. SetParameters. XML* :

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample1.xml)]

V tomto případě:

- Parametr **názvu webové aplikace služby IIS** je cesta služby IIS, kam chcete nasadit webovou aplikaci. Výchozí hodnota je pořízena z **webové stránky balení/publikování** na stránkách vlastností projektu.
- Parametr **připojovacího řetězce ApplicationServices-Web. config** byl vygenerován z prvku **connectionStrings/Add** v souboru *Web. config* . Představuje připojovací řetězec, který má aplikace použít pro kontaktování databáze členství. Hodnota, kterou zde zadáte, bude nahrazena nasazeným souborem *Web. config* . Výchozí hodnota je pořízena ze souboru *Web. config* předběžného nasazení.

WPP také parameterizes tyto vlastnosti v balíčku pro nasazení, který generuje. Hodnoty těchto vlastností můžete zadat při instalaci balíčku pro nasazení. Pokud balíček nainstalujete ručně pomocí Správce služby IIS, jak je popsáno v tématu [Ruční instalace webových balíčků](manually-installing-web-packages.md), Průvodce instalací vás vyzve k zadání hodnot pro všechny parametry. Pokud nainstalujete balíček vzdáleně pomocí souboru *. deploy. cmd* , jak je popsáno v tématu [nasazení webových balíčků](deploying-web-packages.md), nasazení webu se podíváme na tento soubor *SetParameters. XML* za účelem zadání hodnot parametrů. Hodnoty v souboru *SetParameters. XML* lze upravit ručně nebo můžete přizpůsobit soubor jako součást procesu automatizovaného sestavení a nasazení. Tento postup je podrobněji popsán dále v tomto tématu.

### <a name="custom-parameterization"></a>Vlastní Parametrizace

Ve složitějších scénářích nasazení často budete chtít před nasazením projektu parametrizovat další vlastnosti. Obecně řečeno byste měli parametrizovat jakékoli vlastnosti a nastavení, které se budou lišit mezi cílovými prostředími. To může zahrnovat:

- Koncové body služby v souboru *Web. config* .
- Nastavení aplikace v souboru *Web. config* .
- Všechny další deklarativní vlastnosti, které chcete vyzvat uživatele k zadání.

Nejjednodušší způsob, jak parametrizovat tyto vlastnosti, je přidat soubor *Parameters. XML* do kořenové složky projektu webové aplikace. Například v řešení Správce kontaktů obsahuje projekt ContactManager. Mvc soubor *Parameters. XML* v kořenové složce.

![](configuring-parameters-for-web-package-deployment/_static/image1.png)

Pokud tento soubor otevřete, uvidíte, že obsahuje jednu položku **parametru** . Položka používá dotaz jazyka XML Path (XPath) k vyhledání a zadání adresy URL koncového bodu služby ContactService Windows Communication Foundation (WCF) v souboru *Web. config* .

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample2.xml)]

Kromě toho, že Parametrizace adresa URL koncového bodu v balíčku pro nasazení, modul WPP také přidá odpovídající položku do souboru *SetParameters. XML* , který se vygeneroval společně s balíčkem pro nasazení.

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample3.xml)]

Při ruční instalaci balíčku pro nasazení vás Správce služby IIS vyzve k zadání adresy koncového bodu služby spolu s vlastnostmi, které byly parametrizované automaticky. Pokud nainstalujete balíček pro nasazení spuštěním souboru *. deploy. cmd* , můžete upravit soubor *SetParameters. XML* a zadat hodnotu pro adresu koncového bodu služby společně s hodnotami pro vlastnosti, které byly parametrizovany automaticky.

Úplné informace o tom, jak vytvořit soubor *Parameters. XML* , naleznete v tématu [How to: use Parameters to Configure Settings Deployment Settings to When a Package](https://msdn.microsoft.com/library/ff398068.aspx). Podrobné pokyny najdete v proceduře s názvem pro **použití parametrů nasazení pro soubor Web. config** .

## <a name="modifying-the-setparametersxml-file"></a>Úprava souboru SetParameters. XML

Pokud máte v úmyslu nasadit balíček webové aplikace ručně&#x2014;spuštěním souboru *. deploy. cmd* nebo spuštěním příkazu MSDeploy. exe z příkazového řádku&#x2014;, není k dispozici žádný stav, který by bylo možné před nasazením ručně upravovat v souboru *SetParameters. XML* . Pokud však pracujete na podnikovém řešení, bude pravděpodobně nutné nasadit balíček webové aplikace v rámci většího, automatizovaného procesu sestavení a nasazení. V tomto scénáři potřebujete Microsoft Build Engine (MSBuild) pro úpravu souboru *SetParameters. XML* za vás. To můžete provést pomocí úlohy **XmlPoke –** MSBuild.

Tento proces je znázorněno v [ukázkovém řešení Správce kontaktů](the-contact-manager-solution.md) . Příklady kódu, které následují, byly upraveny tak, aby zobrazovaly pouze podrobnosti, které jsou relevantní pro tento příklad.

> [!NOTE]
> Další informace o modelu projektu projektu v ukázkovém řešení a Úvod do vlastních souborů projektu obecně naleznete v tématu [porozumění souboru projektu](understanding-the-project-file.md) a [porozumění procesu sestavení](understanding-the-build-process.md).

Za prvé jsou hodnoty parametru zájmu definovány jako vlastnosti v souboru projektu konkrétního prostředí (například *ENV-dev. proj*).

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample4.xml)]

> [!NOTE]
> Pokyny k přizpůsobení souborů projektu specifických pro prostředí pro vlastní serverová prostředí najdete v tématu [Konfigurace vlastností nasazení pro cílové prostředí](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).

Dále soubor *Publish. proj* importuje tyto vlastnosti. Vzhledem k tomu, že každý soubor *SetParameters. XML* je přidružen k souboru *. deploy. cmd* a nakonec chceme, aby soubor projektu vyvolal každý soubor *. deploy. cmd* , soubor projektu vytvoří *položku* MSBuild pro každý soubor *. deploy. cmd* a definuje vlastnosti zájmu jako *Metadata položek*.

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample5.xml)]

V tomto případě:

- Hodnota metadat **ParametersXml** označuje umístění souboru *SetParameters. XML* .
- Hodnota **IisWebAppName** je cesta služby IIS, na kterou chcete nasadit webovou aplikaci.
- Hodnota **MembershipDBConnectionString** je připojovací řetězec pro databázi členství a hodnota **MembershipDBConnectionName** je atributem **názvu** odpovídajícího parametru v souboru *SetParameters. XML* .
- Hodnota **ServiceEndpointValue** je adresa koncového bodu pro službu WCF na cílovém serveru a hodnota **ServiceEndpointParamName** je atributem názvu odpovídajícího parametru v souboru *SetParameters. XML* .

Nakonec v souboru *Publish. proj* **PublishWebPackages** cíl používá úlohu **XmlPoke –** pro úpravu těchto hodnot v souboru *SetParameters. XML* .

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample6.xml)]

Všimnete si, že každá úloha **XmlPoke –** určuje čtyři hodnoty atributu:

- Atribut **XmlInputPath** informuje úlohu, kde má být nalezen soubor, který chcete upravit.
- Atribut **dotazu** je dotaz XPath, který IDENTIFIKUJE uzel XML, který chcete změnit.
- **Hodnota** atributu je nová hodnota, kterou chcete vložit do vybraného uzlu XML.
- Atribut **Condition** je kritéria, podle kterých se má úloha spustit, nebo není spuštěná. V těchto případech podmínka zajistí, že se do souboru *SetParameters. XML* nepokoušíte vložit hodnotu null nebo prázdnou hodnotu.

## <a name="conclusion"></a>Závěr

Toto téma popisuje roli souboru *SetParameters. XML* a vysvětluje, jak se generuje při sestavování projektu webové aplikace. Vysvětluje, jak můžete parametrizovat další nastavení přidáním souboru *Parameters. XML* do projektu. Také popisuje, jak lze upravit soubor *SetParameters. XML* v rámci většího, automatizovaného procesu sestavení pomocí úlohy **XmlPoke –** v souborech projektu.

Další téma [nasazení webových balíčků](deploying-web-packages.md)popisuje, jak lze nasadit webový balíček buď spuštěním souboru *. deploy. cmd* nebo pomocí příkazu MSDeploy. exe přímo. V obou případech můžete jako parametr nasazení zadat soubor *SetParameters. XML* .

## <a name="further-reading"></a>Další čtení

Informace o tom, jak vytvořit webové balíčky, naleznete v tématu [sestavování a balení projektů webových aplikací](building-and-packaging-web-application-projects.md). Pokyny ke skutečnému nasazení webového balíčku najdete v tématu [nasazení webových balíčků](deploying-web-packages.md). Podrobný návod, jak vytvořit soubor *Parameters. XML* , naleznete v tématu [How to: use Parameters to Configure Deployment Settings to When a Package](https://msdn.microsoft.com/library/ff398068.aspx).

Obecnější informace o parametrizace v Nasazení webu najdete v tématu [nasazení webu parametrizace v akci](https://go.microsoft.com/?linkid=9805119) (Blogový příspěvek).

> [!div class="step-by-step"]
> [Předchozí](building-and-packaging-web-application-projects.md)
> [Další](deploying-web-packages.md)

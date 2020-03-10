---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
title: Vytvoření a spuštění souboru příkazů nasazení | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak vytvořit soubor příkazů, který vám umožní spustit nasazení pomocí souborů projektu Microsoft Build Engine (MSBuild) v jednom kroku, znovu...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c61560e9-9f6c-4985-834a-08a3eabf9c3c
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
msc.type: authoredcontent
ms.openlocfilehash: f1477ff423e4898385066a35b42503f3c70dcc68
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634307"
---
# <a name="creating-and-running-a-deployment-command-file"></a>Vytvoření a spuštění souboru příkazů k nasazení

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak vytvořit soubor příkazů, který vám umožní spustit nasazení pomocí souborů projektu Microsoft Build Engine (MSBuild) jako jeden krok s možností opakování.

Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého řešení [](the-contact-manager-solution.md) &#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.

Metoda nasazení na srdce těchto výukových programů je založena na způsobu sestavení rozděleného projektu popsaných v tématu [Principy procesu sestavení](understanding-the-build-process.md), ve kterém je proces sestavení řízen dvěma soubory&#x2014;projektu jeden, který obsahuje pokyny pro sestavení, které platí pro každé cílové prostředí, a jedno obsahující nastavení sestavení a nasazení specifické pro prostředí. V době sestavení je soubor projektu specifický pro prostředí sloučen do souboru projektu prostředí – nezávislá a vytvoří kompletní sadu instrukcí pro sestavení.

## <a name="process-overview"></a>Přehled procesu

V tomto tématu se dozvíte, jak vytvořit a spustit soubor příkazů, který pomocí těchto souborů projektu provede opakované nasazení do cílového prostředí. V podstatě musí soubor příkazů jednoduše obsahovat příkaz MSBuild, který:

- Instruuje nástroj MSBuild, aby spustil soubor nezávislá *Publish. proj* .
- Informuje soubor *Publish. proj* , který obsahuje nastavení projektu konkrétního prostředí a kde se má najít.

## <a name="create-an-msbuild-command"></a>Vytvoření příkazu MSBuild

Jak je popsáno v tématu [Principy procesu sestavení](understanding-the-build-process.md), soubor&#x2014;projektu specifický pro prostředí, například *ENV-dev. proj*&#x2014;, je navržen pro import do souboru Publish-nezávislá *Publish. proj* v čase sestavení. Společně tyto dva soubory poskytují kompletní sadu instrukcí, které nástroj MSBuild sdělí, jak sestavit a nasadit vaše řešení.

Soubor *Publish. proj* používá prvek **Import** pro import souboru projektu specifického pro prostředí.

[!code-xml[Main](creating-and-running-a-deployment-command-file/samples/sample1.xml)]

V takovém případě, když k sestavení a nasazení řešení Contact Manager použijete nástroj MSBuild. exe, musíte:

- Spusťte nástroj MSBuild. exe v souboru *Publish. proj* .
- Zadáním parametru příkazového řádku s názvem **TargetEnvPropsFile**zadejte umístění souboru projektu specifického pro prostředí.

Chcete-li to provést, váš příkaz MSBuild by měl vypadat takto:

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample2.cmd)]

Tady je jednoduchý krok pro přechod k opakovanému nasazení v jednom kroku. Vše, co potřebujete udělat, je přidání příkazu MSBuild do souboru. cmd. V řešení Správce kontaktů obsahuje složka pro publikování soubor s názvem *Publish-dev. cmd* , který to přesně dělá.

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample3.cmd)]

> [!NOTE]
> Přepínač **/FL** instruuje nástroj MSBuild, aby vytvořil soubor protokolu s názvem *MSBuild. log* v pracovním adresáři, ve kterém byl spuštěn nástroj MSBuild. exe.

K nasazení nebo opětovnému nasazení řešení Contact Manager stačí, když spustíte soubor *Publish-dev. cmd* . Když soubor spustíte, MSBuild provede:

- Sestavujte všechny projekty v řešení.
- Vygenerujte nasazené webové balíčky pro projekty webových aplikací.
- Vygenerujte soubory. dbschema a. DeployManifest pro databázové projekty.
- Nasaďte webové balíčky na webový server.
- Nasaďte databázi na databázový server.

## <a name="run-the-deployment"></a>Spustit nasazení

Když jste vytvořili soubor příkazů pro cílové prostředí, měli byste být schopni dokončit celé nasazení pouhým spuštěním souboru.

**Nasazení řešení Contact Manageru do testovacího prostředí**

1. Na pracovní stanici pro vývojáře otevřete Průzkumníka Windows a přejděte do umístění souboru *Publish-dev. cmd* .
2. Dvakrát klikněte na soubor a spusťte ho.
3. Pokud se zobrazí dialogové okno **otevřít soubor – upozornění zabezpečení** , klikněte na **Spustit**.
4. Pokud jsou nastavení konfigurace a testovací servery správně nastaveny, okno příkazového řádku zobrazí zprávu o **úspěšném sestavení** po dokončení zpracování souborů projektu v nástroji MSBuild.

    ![](creating-and-running-a-deployment-command-file/_static/image1.png)
5. Pokud toto řešení nasadíte poprvé do tohoto prostředí, budete muset přidat účet počítače testovacího webového serveru do role databáze **\_datawrite** a **DB\_DataReader** v databázi **ContactManager** . Tento postup je popsaný v tématu [Konfigurace databázového serveru pro publikování nasazení webu](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).

    > [!NOTE]
    > Tato oprávnění je potřeba přiřadit jenom při vytváření databáze. Ve výchozím nastavení vytvoří proces sestavení databázi znovu při každém nasazení&#x2014;, porovná stávající databázi s nejnovějším schématem a provede pouze změny. V důsledku toho byste měli tyto databázové role namapovat jenom při prvním nasazení řešení.
6. Spusťte Internet Explorer a přejděte na adresu URL aplikace Správce kontaktů (například `http://testweb1:85/ContactManager/`).
7. Ověřte, že aplikace funguje podle očekávání a že je možné přidat kontakty.

    ![](creating-and-running-a-deployment-command-file/_static/image2.png)

## <a name="conclusion"></a>Závěr

Vytvoření souboru příkazů obsahujícího pokyny MSBuild vám poskytne rychlý a snadný způsob, jak sestavit a nasadit řešení pro více projektů do konkrétního cílového prostředí. Pokud potřebujete řešení opakovaně nasadit do více cílových prostředí, můžete vytvořit více souborů příkazů. V každém souboru příkazů příkaz MSBuild sestaví stejný soubor univerzálního projektu, ale určí jiný projekt specifický pro prostředí. Například soubor příkazů pro publikování do vývojového nebo testovacího prostředí může obsahovat tento příkaz MSBuild:

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample4.cmd)]

Soubor příkazů pro publikování do přípravného prostředí může obsahovat tento příkaz MSBuild:

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample5.cmd)]

> [!NOTE]
> Pokyny k přizpůsobení souborů projektu specifických pro prostředí pro vlastní serverová prostředí najdete v tématu [Konfigurace vlastností nasazení pro cílové prostředí](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).

Proces sestavení můžete také přizpůsobit pro každé prostředí přepsáním vlastností nebo nastavením různých dalších přepínačů v příkazu MSBuild. Další informace najdete v tématu [Reference k příkazovému řádku MSBuild](https://msdn.microsoft.com/library/ms164311.aspx).

> [!div class="step-by-step"]
> [Předchozí](deploying-database-projects.md)
> [Další](manually-installing-web-packages.md)

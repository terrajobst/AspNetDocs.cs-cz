---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments
title: Přizpůsobení nasazení databáze pro více prostředí | Microsoft Docs
author: jrjlee
description: 'Toto téma popisuje, jak přizpůsobit vlastnosti databáze na konkrétní cílová prostředí v rámci procesu nasazení. Poznámka: téma předpokládá, že je to th...'
ms.author: riande
ms.date: 05/04/2012
ms.assetid: a172979a-1318-4318-a9c6-4f9560d26267
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments
msc.type: authoredcontent
ms.openlocfilehash: 8ae8cb1a322afb95c5d2e8d5e73c7825c7b2fe5a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78604025"
---
# <a name="customizing-database-deployments-for-multiple-environments"></a>Přizpůsobení nasazené databáze pro různá prostředí

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak přizpůsobit vlastnosti databáze na konkrétní cílová prostředí v rámci procesu nasazení.
> 
> > [!NOTE]
> > Téma předpokládá, že nasazujete databázový projekt sady Visual Studio 2010 pomocí nástroje MSBuild. exe a VSDBCMD. exe. Další informace o tom, proč můžete zvolit tento přístup, najdete v tématu [nasazení webu v podniku](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md) a [nasazení databázových projektů](../web-deployment-in-the-enterprise/deploying-database-projects.md).
> 
> 
> Když nasadíte databázový projekt do více cílů, často budete chtít přizpůsobit vlastnosti nasazení databáze pro každé cílové prostředí. Například v testovacích prostředích byste při každém nasazení obvykle znovu vytvořili databázi, zatímco v pracovních nebo produkčních prostředích byste měli větší mnohem více pravděpodobných přírůstkových aktualizací, abyste zachovali data.
> 
> V projektu databáze sady Visual Studio 2010 jsou nastavení nasazení obsažena v rámci konfiguračního souboru nasazení (. SqlDeployment). V tomto tématu se dozvíte, jak vytvořit soubory konfigurace nasazení specifické pro konkrétní prostředí a zadat tu, kterou chcete použít jako parametr VSDBCMD.

Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého [řešení](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.

Metoda nasazení na srdce těchto kurzů je založena na způsobu rozdělení souborů projektu popsaných v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md), ve kterém je proces sestavení řízen dvěma soubory&#x2014;projektu jeden, který obsahuje pokyny pro sestavení, které platí pro každé cílové prostředí, a jedno obsahující nastavení sestavení a nasazení specifické pro konkrétní prostředí. V době sestavení je soubor projektu specifický pro prostředí sloučen do souboru projektu prostředí – nezávislá a vytvoří kompletní sadu instrukcí pro sestavení.

## <a name="task-overview"></a>Přehled úlohy

V tomto tématu se předpokládá, že:

- Použijete přístup k rozdělenému souboru projektu k nasazení řešení, jak je popsáno v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md).
- Zavoláte VSDBCMD ze souboru projektu pro nasazení databázového projektu, jak je popsáno v tématu [Principy procesu sestavení](../web-deployment-in-the-enterprise/understanding-the-build-process.md).

Pokud chcete vytvořit systém nasazení, který podporuje různé vlastnosti nasazení databáze mezi cílovými prostředími, budete muset:

- Vytvořte soubor konfigurace nasazení (. SqlDeployment) pro každé cílové prostředí.
- Vytvořte příkaz VSDBCMD, který určuje konfigurační soubor nasazení jako přepínač příkazového řádku.
- Parametrizovat příkaz VSDBCMD v souboru projektu Microsoft Build Engine (MSBuild), aby VSDBCMD možnosti byly vhodné pro cílové prostředí.

V tomto tématu se dozvíte, jak provádět jednotlivé postupy.

## <a name="creating-environment-specific-deployment-configuration-files"></a>Vytváření konfiguračních souborů nasazení specifických pro konkrétní prostředí

Ve výchozím nastavení databázový projekt obsahuje jeden konfigurační soubor nasazení s názvem *Database. SqlDeployment*. Pokud tento soubor otevřete v aplikaci Visual Studio 2010, můžete zobrazit různé možnosti nasazení, které máte k dispozici:

- **Kolace porovnání nasazení** To vám umožní vybrat, jestli se má použít kolace databáze vašeho projektu ( *zdrojová* kolace) nebo kolace databáze cílového serveru ( *cílová* kolace). Ve většině případů budete chtít použít zdrojovou kolaci při nasazení do vývojového nebo testovacího prostředí. Při nasazení do pracovního nebo produkčního prostředí obvykle budete chtít opustit cílovou kolaci beze změny, abyste se vyhnuli problémům s interoperabilitou.
- **Nasaďte vlastnosti databáze**. To vám umožní vybrat, jestli se mají použít vlastnosti databáze, jak jsou definované v souboru *Database. sqlsettings* . Při prvním nasazení databáze byste měli nasadit vlastnosti databáze. Pokud aktualizujete existující databázi, vlastnosti by již měly být na místě a nemuseli byste je znovu nasazovat.
- **Vždy znovu vytvořit databázi**. To vám umožní vybrat, jestli se má znovu vytvořit cílová databáze pokaždé, když nasadíte nebo provedete přírůstkové změny, aby se cílová databáze zajistila v aktuálním stavu pomocí schématu. Pokud databázi znovu vytvoříte, ztratíte všechna data ve stávající databázi. V takovém případě byste je měli obvykle nastavit na **hodnotu false** pro nasazení do pracovních nebo produkčních prostředí.
- **Zablokuje přírůstkové nasazení, pokud může dojít ke ztrátě dat**. To vám umožní vybrat, jestli se má nasazení zastavit, pokud Změna schématu databáze způsobí ztrátu dat. Pro nasazení do produkčního prostředí je obvykle nastavena **hodnota true** , abyste měli možnost zasáhnout a chránit veškerá důležitá data. Pokud jste nastavili možnost **vždy znovu vytvořit databázi** na **hodnotu NEPRAVDA**, toto nastavení nebude mít žádný vliv.
- **Spustit nasazení v režimu jednoho uživatele**. To obvykle není problém ve vývojových nebo testovacích prostředích. Nicméně tuto hodnotu nastavte na **true** pro nasazení do pracovních nebo produkčních prostředí. To uživatelům brání v provádění změn v databázi během probíhajícího nasazení.
- **Před nasazením zálohujte databázi**. Toto nastavení je obvykle nastaveno na **hodnotu true** při nasazení do provozního prostředí, jako preventivní opatření před ztrátou dat. Můžete ji také nastavit na **hodnotu true** při nasazení do přípravného prostředí, pokud vaše pracovní databáze obsahuje velké množství dat.
- **Generujte příkazy drop pro objekty, které jsou v cílové databázi, ale které nejsou v projektu databáze**. Ve většině případů jde o nedílnou a podstatnou součást provádění přírůstkových změn v databázi. Pokud jste nastavili možnost **vždy znovu vytvořit databázi** na **hodnotu NEPRAVDA**, toto nastavení nebude mít žádný vliv.
- **Nepoužívejte příkazy ALTER ASSEMBLY k aktualizaci typů CLR**. Toto nastavení určuje, jak má SQL Server aktualizovat typy modulu CLR (Common Language Runtime) na novější verze sestavení. Ve většině scénářů by měl být nastaven na **hodnotu false** .

V této tabulce jsou uvedena typická nastavení nasazení pro různá cílová prostředí. Nastavení se ale může lišit v závislosti na vašich přesných požadavcích.

|  | Vývojář a testování | Příprava/integrace | Výroba |
| --- | --- | --- | --- |
| **Kolace porovnání nasazení** | Zdroj | Cíl | Cíl |
| **Nasadit vlastnosti databáze** | True | Pouze poprvé | Pouze poprvé |
| **Vždy znovu vytvořit databázi** | True | False | False |
| **Blokovat přírůstkové nasazení, pokud může dojít ke ztrátě dat** | False | Možná | True |
| **Spustit skript nasazení v režimu jednoho uživatele** | False | True | True |
| **Zálohování databáze před nasazením** | False | Možná | True |
| **Generovat příkazy DROP pro objekty, které jsou v cílové databázi, ale které nejsou v projektu databáze** | False | True | True |
| **Nepoužívejte příkazy ALTER ASSEMBLY k aktualizaci typů CLR.** | False | False | False |

> [!NOTE]
> Další informace o vlastnostech nasazení databáze a ohledech na prostředí najdete v tématu [Přehled nastavení databázového projektu](https://msdn.microsoft.com/library/aa833291(v=VS.100).aspx), [Postupy: Konfigurace vlastností pro podrobnosti o nasazení](https://msdn.microsoft.com/library/dd172125.aspx), [sestavení a nasazení databáze do izolovaného vývojového prostředí](https://msdn.microsoft.com/library/dd193409.aspx)a [vytváření a nasazování databází do pracovního nebo produkčního prostředí](https://msdn.microsoft.com/library/dd193413.aspx).

Pro podporu nasazení databázového projektu na více cílů byste měli vytvořit konfigurační soubor nasazení pro každé cílové prostředí.

**Vytvoření konfiguračního souboru specifického pro prostředí**

1. V aplikaci Visual Studio 2010 v okně **Průzkumník řešení** klikněte pravým tlačítkem na projekt databáze a pak klikněte na **vlastnosti**.
2. Na stránce Vlastnosti projektu databáze na kartě **nasadit** na řádku **konfigurační soubor nasazení** klikněte na **Nový**.

    ![](customizing-database-deployments-for-multiple-environments/_static/image1.png)
3. V dialogovém okně **Nový konfigurační soubor nasazení** dejte souboru smysluplný název (například **TestEnvironment. SqlDeployment**) a pak klikněte na **Uložit**.
4. Na stránce *[filename] * * * *. SqlDeployment** nastavte vlastnosti nasazení tak, aby odpovídaly požadavkům vašeho cílového prostředí, a pak soubor uložte.

    ![](customizing-database-deployments-for-multiple-environments/_static/image2.png)
5. Všimněte si, že nový soubor je přidán do složky Properties (vlastnosti) projektu databáze.

    ![](customizing-database-deployments-for-multiple-environments/_static/image3.png)

## <a name="specifying-the-deployment-configuration-file-in-vsdbcmd"></a>Určení konfiguračního souboru nasazení v VSDBCMD

Použijete-li konfigurace řešení (například ladění a vydání) v rámci sady Visual Studio 2010, můžete k každé konfiguraci přidružit konfigurační soubor nasazení. Když sestavíte určitou konfiguraci, proces sestavení vygeneruje soubor manifestu nasazení specifický pro konfiguraci, který odkazuje na konfigurační soubor nasazení specifický pro konkrétní konfiguraci. Jedním z hlavních cílů přístupu k nasazení, které jsou popsány v těchto kurzech, je však poskytnout lidem možnost řídit proces nasazení bez použití sady Visual Studio 2010 a konfigurací řešení. V tomto přístupu je konfigurace řešení stejná bez ohledu na cílové prostředí nasazení. K přizpůsobení nasazení databáze na konkrétní cílové prostředí můžete použít možnosti příkazového řádku VSDBCMD k určení konfiguračního souboru nasazení.

Chcete-li zadat konfigurační soubor nasazení v VSDBCMD, použijte přepínač **p:/DeploymentConfigurationFile** a zadejte úplnou cestu k souboru. Tím dojde k přepsání konfiguračního souboru nasazení, který identifikuje manifest nasazení. Například můžete použít tento příkaz VSDBCMD k nasazení databáze **ContactManager** do testovacího prostředí:

[!code-console[Main](customizing-database-deployments-for-multiple-environments/samples/sample1.cmd)]

> [!NOTE]
> Všimněte si, že proces sestavení může přejmenovat soubor. SqlDeployment při zkopírování souboru do výstupního adresáře.

Pokud používáte proměnné příkazů SQL ve skriptech SQL pro předběžné nasazení nebo po nasazení, můžete použít podobný přístup k přidružení souboru. sqlcmdvars specifického pro prostředí k vašemu nasazení. V tomto případě použijete přepínač **p:/SqlCommandVariablesFile** k identifikaci souboru. sqlcmdvars.

## <a name="running-the-vsdbcmd-command-from-an-msbuild-project-file"></a>Spuštění příkazu VSDBCMD ze souboru projektu MSBuild

Můžete vyvolat příkaz VSDBCMD ze souboru projektu MSBuild pomocí úlohy **exec** v rámci cíle MSBuild. V nejjednodušším tvaru by vypadalo takto:

[!code-xml[Main](customizing-database-deployments-for-multiple-environments/samples/sample2.xml)]

- V praxi, aby bylo možné soubory projektu snadno číst a opakovaně používat, budete chtít vytvořit vlastnosti pro uložení různých parametrů příkazového řádku. To usnadňuje uživatelům zadání hodnot vlastností do souboru projektu specifického pro prostředí nebo přepisu výchozích hodnot z příkazového řádku MSBuild. Použijete-li přístup k rozdělenému souboru projektu, který je popsaný v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md), měli byste odpovídajícím způsobem rozdělit pokyny a vlastnosti sestavení mezi tyto dva soubory:
- Nastavení specifické pro prostředí, jako je název souboru konfigurace nasazení, připojovací řetězec databáze a název cílové databáze, by měly přejít do souboru projektu specifického pro prostředí.
- Cíl nástroje MSBuild, který spouští příkaz VSDBCMD, spolu s jakýmikoli univerzálními vlastnostmi, jako je umístění spustitelného souboru VSDBCMD, by měl přejít do souboru univerzálního projektu.

Měli byste také zajistit, aby projekt databáze byl vytvořen před vyvoláním VSDBCMD, aby byl vytvořen soubor. DeployManifest a byl připraven k použití. Úplný příklad tohoto přístupu si můžete prohlédnout v tématu [Principy procesu sestavení](../web-deployment-in-the-enterprise/understanding-the-build-process.md), který vás provede soubory projektu v [ukázkovém řešení Správce kontaktů](../web-deployment-in-the-enterprise/the-contact-manager-solution.md).

## <a name="conclusion"></a>Závěr

Toto téma popisuje, jak můžete přizpůsobit vlastnosti databáze na jiná cílová prostředí při nasazení databázových projektů pomocí nástroje MSBuild a VSDBCMD. Tento přístup je užitečný v případě, že potřebujete nasadit databázové projekty jako součást větších podnikových řešení na úrovni podniku. Tato řešení se často nasazují na více cílů, jako jsou například vývojové nebo testovací prostředí v izolovaném prostoru, pracovní nebo integrační platformy a produkční nebo aktivní prostředí. Každé z těchto cílových prostředí obvykle vyžaduje jedinečnou sadu vlastností nasazení databáze.

## <a name="further-reading"></a>Další čtení

Další informace o nasazení databázových projektů pomocí VSDBCMD. exe najdete v tématu [nasazení databázových projektů](../web-deployment-in-the-enterprise/deploying-database-projects.md). Další informace o použití vlastních souborů projektu MSBuild pro řízení procesu nasazení naleznete v tématu [porozumění souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md) a [porozumění procesu sestavení](../web-deployment-in-the-enterprise/understanding-the-build-process.md).

Tyto články na webu MSDN poskytují obecnější pokyny k nasazení databáze:

- [Přehled nastavení databázového projektu](https://msdn.microsoft.com/library/aa833291(v=VS.100).aspx)
- [Postupy: Konfigurace vlastností pro podrobnosti nasazení](https://msdn.microsoft.com/library/dd172125.aspx)
- [Sestavování a nasazování databází do izolovaného vývojového prostředí](https://msdn.microsoft.com/library/dd193409.aspx)
- [Sestavování a nasazování databází do pracovního nebo produkčního prostředí](https://msdn.microsoft.com/library/dd193413.aspx)

> [!div class="step-by-step"]
> [Předchozí](performing-a-what-if-deployment.md)
> [Další](deploying-database-role-memberships-to-test-environments.md)

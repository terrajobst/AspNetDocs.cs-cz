---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
title: Nasazení členství databázové role do testovacích prostředí | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak přidat uživatelské účty do databázových rolí jako součást nasazení řešení do testovacího prostředí. Když nasadíte řešení obsahující...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 9b2af539-7ad9-47aa-b66e-873bd9906e79
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments
msc.type: authoredcontent
ms.openlocfilehash: a15f5bf5f659d151e91ef9e53c5ad55bcd8e2b01
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78587589"
---
# <a name="deploying-database-role-memberships-to-test-environments"></a>Nasazení členství v databázových rolích do testovacího prostředí

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak přidat uživatelské účty do databázových rolí jako součást nasazení řešení do testovacího prostředí.
> 
> Když nasadíte řešení obsahující databázový projekt do pracovního nebo produkčního prostředí, obvykle nechcete, aby vývojář mohl automatizovat přidávání uživatelských účtů do databázových rolí. Ve většině případů vývojář neví, které uživatelské účty je potřeba přidat do kterých databázových rolí a že tyto požadavky se můžou kdykoli změnit. Nicméně když nasadíte řešení, které obsahuje databázový projekt, do vývojového nebo testovacího prostředí, je obvykle situace odlišná:
> 
> - Vývojář obvykle znovu nasadí řešení pravidelně, často za den.
> - Databáze je obvykle znovu vytvořena při každém nasazení, což znamená, že uživatelé databáze musí být vytvořeni a přidáni do rolí po každém nasazení.
> - Vývojář má obvykle plnou kontrolu nad cílovým vývojovým nebo testovacím prostředím.
> 
> V tomto scénáři je často výhodné automaticky vytvářet uživatele databáze a přiřazovat členství v databázových rolích jako součást procesu nasazení.
> 
> Klíčovým faktorem je, že tato operace musí být podmíněná na základě cílového prostředí. Pokud provádíte nasazení do pracovního nebo produkčního prostředí, chcete tuto operaci přeskočit. Pokud provádíte nasazení do vývojového nebo testovacího prostředí, chcete nasadit členství v rolích bez dalšího zásahu. Toto téma popisuje jeden přístup, který můžete použít k vyřešení této výzvy.

Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého [řešení](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.

Metoda nasazení na srdce těchto kurzů je založena na způsobu rozdělení souborů projektu popsaných v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md), ve kterém je proces sestavení řízen dvěma soubory&#x2014;projektu jeden, který obsahuje pokyny pro sestavení, které platí pro každé cílové prostředí, a jedno obsahující nastavení sestavení a nasazení specifické pro konkrétní prostředí. V době sestavení je soubor projektu specifický pro prostředí sloučen do souboru projektu prostředí – nezávislá a vytvoří kompletní sadu instrukcí pro sestavení.

## <a name="task-overview"></a>Přehled úlohy

V tomto tématu se předpokládá, že:

- Použijete přístup k rozdělenému souboru projektu k nasazení řešení, jak je popsáno v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md).
- Zavoláte VSDBCMD ze souboru projektu pro nasazení databázového projektu, jak je popsáno v tématu [Principy procesu sestavení](../web-deployment-in-the-enterprise/understanding-the-build-process.md).

Chcete-li vytvořit uživatele databáze a přiřadit členství v rolích při nasazení databázového projektu do testovacího prostředí, budete muset:

- Vytvořte skript Transact jazyk SQL (Structured Query Language) (Transact-SQL), který provede potřebné změny databáze.
- Vytvořte cíl Microsoft Build Engine (MSBuild), který pomocí nástroje Sqlcmd. exe spustí skript SQL.
- Nakonfigurujte soubory projektu tak, aby při nasazení vašeho řešení do testovacího prostředí vyvolaly cíl.

V tomto tématu se dozvíte, jak provádět jednotlivé postupy.

## <a name="scripting-the-database-role-memberships"></a>Vytváření skriptů pro členství v databázových rolích

Skript Transact-SQL můžete vytvořit mnoha různými způsoby a v jakémkoli umístění, které zvolíte. Nejjednodušším řešením je vytvořit skript v rámci řešení v sadě Visual Studio 2010.

**Vytvoření skriptu SQL**

1. V okně **Průzkumník řešení** rozbalte uzel projekt databáze.
2. Klikněte pravým tlačítkem na složku **skripty** , přejděte na **Přidat**a pak klikněte na **Nová složka**.
3. Jako název složky zadejte **test** a potom stiskněte klávesu ENTER.
4. Klikněte pravým tlačítkem na **testovací** složku, přejděte na **Přidat**a pak klikněte na **skript**.
5. V dialogovém okně **Přidat novou položku** poskytněte vašemu skriptu smysluplný název (například **AddRoleMemberships. SQL**) a pak klikněte na **Přidat**.

    ![](deploying-database-role-memberships-to-test-environments/_static/image1.png)
6. V souboru *AddRoleMemberships. SQL* přidejte příkazy jazyka Transact-SQL, které:

    1. Vytvořte uživatele databáze pro SQL Server přihlašovací jméno, které bude mít přístup k vaší databázi.
    2. Přidejte uživatele databáze do požadovaných databázových rolí.
7. Soubor by měl vypadat takto:

    [!code-sql[Main](deploying-database-role-memberships-to-test-environments/samples/sample1.sql)]
8. Uložte soubor.

## <a name="executing-the-script-on-the-target-database"></a>Spuštění skriptu v cílové databázi

V ideálním případě byste spustili všechny požadované skripty jazyka Transact-SQL jako součást skriptu po nasazení při nasazení databázového projektu. Skripty po nasazení ale neumožňují provádět logiku podmíněně na základě konfigurací řešení nebo vlastností sestavení. Alternativou je spuštění skriptů SQL přímo ze souboru projektu MSBuild vytvořením **cílového** prvku, který provede příkaz Sqlcmd. exe. Tento příkaz můžete použít ke spuštění skriptu v cílové databázi:

[!code-console[Main](deploying-database-role-memberships-to-test-environments/samples/sample2.cmd)]

> [!NOTE]
> Další informace o možnostech příkazového řádku Sqlcmd najdete v tématu [Nástroj Sqlcmd](https://msdn.microsoft.com/library/ms162773.aspx).

Před vložením tohoto příkazu v cíli MSBuild musíte zvážit, za jakých podmínek chcete skript spustit:

- Cílová databáze musí existovat, než změníte její členství v roli. V takovém případě je třeba spustit tento skript *po* nasazení databáze.
- Musíte zahrnout podmínku, aby se skript spustil jenom pro testovací prostředí.
- Pokud spouštíte "Co když"&#x2014;v jiných slovech, pokud generujete skripty pro nasazení, ale ve skutečnosti je nespouštíte, neměli&#x2014;byste spustit skript SQL.

Pokud používáte přístup k souboru rozděleného projektu, který je popsaný v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md), jak je znázorněno v ukázkovém řešení Contact Manager, můžete rozdělit pokyny sestavení pro skript SQL takto:

- Všechny požadované vlastnosti specifické pro prostředí spolu s vlastností, která určuje, zda mají být nasazena oprávnění, by měly přejít do souboru projektu specifického pro prostředí (například *ENV-dev. proj*).
- Samotný cíl MSBuild spolu s vlastnostmi, které se nemění mezi cílovými prostředími, by měl přejít do souboru univerzálního projektu (například *Publish. proj*).

V souboru projektu specifického pro prostředí je nutné definovat název databázového serveru, název cílové databáze a vlastnost Boolean, která uživateli umožňuje určit, jestli se mají nasadit členství v rolích.

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample3.xml)]

V souboru univerzálního projektu je nutné zadat umístění spustitelného souboru Sqlcmd a umístění skriptu SQL, který chcete spustit. Tyto vlastnosti zůstanou stejné bez ohledu na cílové prostředí. Také je nutné vytvořit cíl MSBuild pro provedení příkazu Sqlcmd.

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample4.xml)]

Všimněte si, že přidáte umístění spustitelného souboru Sqlcmd jako statické vlastnosti, protože to může být užitečné pro jiné cíle. Naproti tomu definujete umístění skriptu SQL a syntaxi příkazu Sqlcmd jako dynamické vlastnosti v rámci cíle, protože nebudou nutné před provedením cíle. V takovém případě bude cíl **DeployTestDBPermissions** proveden pouze v případě, že jsou splněny tyto podmínky:

- Vlastnost **DeployTestDBRoleMemberships** je nastavena na **hodnotu true**.
- Uživatel nezadal příznak **whatIf = true** .

Nakonec nezapomeňte vyvolat cíl. V souboru *Publish. proj* to můžete udělat tak, že přidáte cíl do seznamu závislostí výchozího cíle **FullPublish** . Je nutné zajistit, aby cíl **DeployTestDBPermissions** nebyl proveden, dokud není proveden cíl **PublishDbPackages** .

[!code-xml[Main](deploying-database-role-memberships-to-test-environments/samples/sample5.xml)]

## <a name="conclusion"></a>Závěr

Toto téma popisuje jeden ze způsobů, ve kterém můžete přidávat uživatele databáze a členství v rolích jako akci po nasazení při nasazení databázového projektu. To je obvykle užitečné v případě, že pravidelně znovu vytvoříte databázi v testovacím prostředí, ale při nasazování databází do pracovních nebo produkčních prostředí by se obvykle měla vyhýbat. V takovém případě byste měli zajistit, abyste používali nezbytnou podmíněný logiku, aby se uživatelé a členství v rolích mohli vytvářet jenom v případě, že je to vhodné.

## <a name="further-reading"></a>Další čtení

Další informace o použití VSDBCMD k nasazení databázových projektů naleznete v tématu [Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md). Pokyny k přizpůsobení nasazení databáze pro různá cílová prostředí najdete v tématu [přizpůsobení nasazení databáze pro více prostředí](customizing-database-deployments-for-multiple-environments.md). Další informace o použití vlastních souborů projektu MSBuild pro řízení procesu nasazení naleznete v tématu [porozumění souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md) a [porozumění procesu sestavení](../web-deployment-in-the-enterprise/understanding-the-build-process.md). Další informace o možnostech příkazového řádku Sqlcmd najdete v tématu [Nástroj Sqlcmd](https://msdn.microsoft.com/library/ms162773.aspx).

> [!div class="step-by-step"]
> [Předchozí](customizing-database-deployments-for-multiple-environments.md)
> [Další](deploying-membership-databases-to-enterprise-environments.md)

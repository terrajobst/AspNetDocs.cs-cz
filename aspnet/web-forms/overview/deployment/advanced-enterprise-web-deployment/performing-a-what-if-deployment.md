---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
title: Probíhá nasazení What If | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak pomocí nástroje pro nasazení webu Internetová informační služba (IIS) (Nasazení webu) a V V systému provést nasazení typu "co if" (nebo simulované)...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c711b453-01ac-4e65-a48c-93d99bf22e58
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
msc.type: authoredcontent
ms.openlocfilehash: 73a0e038cc0d4ebae0ffc8ed3fd2de4c9dad673c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628889"
---
# <a name="performing-a-what-if-deployment"></a>Nasazení typu „What If“

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> V tomto tématu se dozvíte, jak pomocí Nasazení webu nástroje pro nasazení webu Internetová informační služba (IIS) a VSDBCMD provádět nasazení typu "Co když" (nebo simulované). To vám umožní určit důsledky logiky nasazení v konkrétním cílovém prostředí před samotným nasazením aplikace.

Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého [řešení](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.

Metoda nasazení na srdce těchto kurzů je založena na způsobu rozdělení souboru projektu popsaného v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md), ve kterém je proces sestavení a nasazení řízen dvěma soubory&#x2014;projektu, které obsahují pokyny pro sestavení, které platí pro každé cílové prostředí, a jedno obsahující nastavení sestavení a nasazení specifické pro konkrétní prostředí. V době sestavení je soubor projektu specifický pro prostředí sloučen do souboru projektu prostředí – nezávislá a vytvoří kompletní sadu instrukcí pro sestavení.

## <a name="performing-a-what-if-deployment-for-web-packages"></a>Provádění nasazení What If pro webové balíčky

Nasazení webu obsahuje funkce, které vám umožní provádět nasazení v režimu "co if" (nebo zkušebního). Když v režimu "co if" nasadíte artefakty, Nasazení webu vygeneruje soubor protokolu, jako kdyby jste provedli nasazení, ale ve skutečnosti se na cílovém serveru nemění cokoli. Kontrola souboru protokolu vám může pomáhat pochopit, jaký dopad má vaše nasazení na cílový server, zejména:

- Co se přidá.
- Co se aktualizuje.
- Co se odstraní.

Vzhledem k tomu, že nasazení "citlivostní změny" ve skutečnosti na cílovém serveru nemění cokoli, co nemůže vždycky udělat, je předpověď bez ohledu na to, jestli se nasazení nezdaří.

Jak je popsáno v tématu [nasazení webových balíčků](../web-deployment-in-the-enterprise/deploying-web-packages.md), můžete nasadit webové balíčky pomocí nasazení webu dvěma způsoby&#x2014;pomocí nástroje příkazového řádku MSDeploy. exe přímo nebo spuštěním souboru *. deploy. cmd* , který generuje proces sestavení.

Pokud používáte soubor MSDeploy. exe přímo, můžete spustit nasazení "Co když" přidáním příznaku **– whatIf** do příkazu. Například pro vyhodnocení toho, co se stane, když jste nasadili balíček ContactManager. Mvc. zip do přípravného prostředí, příkaz MSDeploy by měl vypadat takto:

[!code-console[Main](performing-a-what-if-deployment/samples/sample1.cmd)]

Až budete spokojeni s výsledky nasazení "citlivostní zpracování", můžete odebrat příznak **– whatIf** pro spuštění živého nasazení.

> [!NOTE]
> Další informace o možnostech příkazového řádku pro soubor MSDeploy. exe najdete v tématu [nastavení operace nasazení webu](https://technet.microsoft.com/library/dd569089(WS.10).aspx).

Pokud používáte soubor *. deploy. cmd* , můžete v příkazu spustit místo příznaku **/y** ("Ano," nebo režim aktualizace) příznak "citlivostní aktualizace", a to pomocí příznaku **/t** (režim zkušebního režimu). Například pro vyhodnocení toho, co se stane, když nasadíte balíček ContactManager. Mvc. zip spuštěním souboru *. deploy. cmd* , váš příkaz by měl vypadat takto:

[!code-console[Main](performing-a-what-if-deployment/samples/sample2.cmd)]

Až budete spokojeni s výsledky nasazení zkušebního režimu, můžete nahradit příznak **/t** pomocí příznaku **/y** pro spuštění nasazení v reálném čase:

[!code-console[Main](performing-a-what-if-deployment/samples/sample3.cmd)]

> [!NOTE]
> Další informace o možnostech příkazového řádku pro soubory *. deploy. cmd* naleznete v tématu [How to: install a Deployment Package by using a Deploy. cmd File](https://msdn.microsoft.com/library/ff356104.aspx). Pokud spustíte soubor *. deploy. cmd* bez zadání příznaků, příkazový řádek zobrazí seznam dostupných příznaků.

## <a name="performing-a-what-if-deployment-for-databases"></a>Provádění nasazení "What If" pro databáze

V této části se předpokládá, že používáte nástroj VSDBCMD k provádění přírůstkového nasazení databáze založené na schématu. Tento přístup je podrobněji popsán v tématu [nasazení databázových projektů](../web-deployment-in-the-enterprise/deploying-database-projects.md). Doporučujeme, abyste se seznámili s tímto tématem dřív, než použijete níže popsané koncepty.

Při použití VSDBCMD v režimu **nasazení** můžete pomocí příznaku **/DD** (nebo **/DEPLOYTODATABASE**) řídit, zda VSDBCMD skutečně nasadí databázi nebo pouze generuje skript nasazení. Pokud nasazujete soubor. dbschema, jedná se o chování:

- Pokud zadáte **/DD +** nebo **/DD**, VSDBCMD vygeneruje skript nasazení a nasadí databázi.
- Pokud zadáte **/DD-** nebo vynecháte přepínač, vytvoří VSDBCMD pouze skript nasazení.

> [!NOTE]
> Pokud nasazujete soubor. DeployManifest namísto souboru. dbschema, chování přepínače **/DD** je mnohem složitější. V podstatě bude VSDBCMD ignorovat hodnotu přepínače **/DD** , pokud soubor. DeployManifest obsahuje prvek **DeployToDatabase** s hodnotou **true**. [Nasazení databázových projektů](../web-deployment-in-the-enterprise/deploying-database-projects.md) popisuje toto chování v plném rozsahu.

Chcete-li například vygenerovat skript nasazení pro databázi **ContactManager** bez toho, aby byla databáze skutečně nasazena, příkaz VSDBCMD by měl vypadat takto:

[!code-console[Main](performing-a-what-if-deployment/samples/sample4.cmd)]

VSDBCMD je rozdílový Nástroj pro nasazení databáze a takový skript nasazení se dynamicky generuje tak, aby obsahoval všechny příkazy SQL, které jsou nutné k aktualizaci aktuální databáze, pokud existuje, do zadaného schématu. Kontrola skriptu nasazení je užitečný způsob, jak určit, jaký dopad má vaše nasazení na aktuální databázi a data, která obsahuje. Můžete například chtít určit:

- Zda budou odebrány všechny existující tabulky a zda budou mít za následek ztrátu dat.
- Určuje, zda pořadí operací přenese riziko ztráty dat, například pokud provádíte rozdělení nebo sloučení tabulek.

Pokud jste s skriptem nasazení spokojeni, můžete VSDBCMD opakovat pomocí příznaku **/DD +** , aby se změny provedly. Případně můžete upravit skript nasazení tak, aby splňoval vaše požadavky, a pak ho spustit ručně na databázovém serveru.

## <a name="integrating-what-if-functionality-into-custom-project-files"></a>Integrace funkce "What If" do vlastních souborů projektu

Ve složitějších scénářích nasazení budete chtít použít vlastní soubor projektu Microsoft Build Engine (MSBuild) k zapouzdření logiky sestavení a nasazení, jak je popsáno v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md). Například v ukázkovém řešení [Contact Manageru](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) soubor *Publish. proj* :

- Sestavení řešení.
- Používá Nasazení webu k zabalení a nasazení aplikace ContactManager. Mvc.
- Nástroj používá Nasazení webu k zabalení a nasazení aplikace ContactManager. Service.
- Nasadí databázi **ContactManager** .

Když integruje nasazení více webových balíčků a/nebo databází do procesu s jedním krokem tímto způsobem, může být také vhodné provést celé nasazení v režimu "co if".

Soubor *Publish. proj* ukazuje, jak to lze provést. Nejprve je třeba vytvořit vlastnost pro uložení hodnoty "citlivostní informace":

[!code-xml[Main](performing-a-what-if-deployment/samples/sample5.xml)]

V tomto případě jste vytvořili vlastnost s názvem **whatIf** s výchozí hodnotou **false**. Uživatelé mohou tuto hodnotu přepsat nastavením vlastnosti na **hodnotu true** v parametru příkazového řádku, protože se zobrazí krátce.

Další fází je parametrizovat jakékoli příkazy Nasazení webu a VSDBCMD, aby příznaky odrážely hodnotu vlastnosti **whatIf** . Například další cíl (pořízený ze souboru *Publish. proj* a zjednodušená) spustí soubor *. deploy. cmd* pro nasazení webového balíčku. Ve výchozím nastavení příkaz obsahuje přepínač **/y** ("Ano" nebo režim aktualizace). Pokud je vlastnost **whatIf** nastavená na **hodnotu true**, nahradí se tento parametr přepínačem **/t** (zkušební verze nebo "Co kdyby").

[!code-xml[Main](performing-a-what-if-deployment/samples/sample6.xml)]

Podobně další cíl používá nástroj VSDBCMD k nasazení databáze. Ve výchozím nastavení není k dispozici přepínač **/DD** . To znamená, že VSDBCMD vygeneruje skript nasazení, ale neimplementuje databázi&#x2014;jinými slovy, scénář "Co je potřeba". Pokud vlastnost **whatIf** není nastavena na **hodnotu true**, je přidán přepínač **/DD** a VSDBCMD bude nasazena databáze.

[!code-xml[Main](performing-a-what-if-deployment/samples/sample7.xml)]

Stejný přístup můžete použít k použití parametrizovat všechny relevantní příkazy v souboru projektu. Pokud chcete spustit nasazení "Co je potřeba", můžete jednoduše zadat hodnotu vlastnosti **whatIf** z příkazového řádku:

[!code-console[Main](performing-a-what-if-deployment/samples/sample8.cmd)]

Tímto způsobem můžete spustit nasazení "to if" pro všechny komponenty projektu v jednom kroku.

## <a name="conclusion"></a>Závěr

Toto téma popisuje, jak pomocí Nasazení webu, VSDBCMD a MSBuild spustit nasazení "Co je potřeba". Nasazení "Co když je" umožňuje vyhodnotit dopad navrhovaného nasazení před tím, než ve skutečnosti provedete změny v cílovém prostředí.

## <a name="further-reading"></a>Další čtení

Další informace o Nasazení webu syntaxi příkazového řádku najdete v tématu [nasazení webu nastavení operací](https://technet.microsoft.com/library/dd569089(WS.10).aspx). Pokyny k možnostem příkazového řádku při použití souboru *. deploy. cmd* naleznete v tématu [How to: install a Deployment Package by using a Deploy. cmd File](https://msdn.microsoft.com/library/ff356104.aspx). Pokyny k syntaxi příkazového řádku VSDBCMD najdete v tématu [Reference k příkazovému řádku pro VSDBCMD. EXE (nasazení a import schématu)](https://msdn.microsoft.com/library/dd193283.aspx).

> [!div class="step-by-step"]
> [Předchozí](advanced-enterprise-web-deployment.md)
> [Další](customizing-database-deployments-for-multiple-environments.md)

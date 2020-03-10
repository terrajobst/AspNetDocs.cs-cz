---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
title: 'Nasazení podnikového webu: Přehled scénářů | Microsoft Docs'
author: jrjlee
description: Tato sada kurzů používá ukázkové řešení s realistickou úrovní složitosti spolu se scénářem fiktivního podnikového nasazení, které poskytuje odkaz...
ms.author: riande
ms.date: 05/03/2012
ms.assetid: aa862153-4cd8-4e33-beeb-abf502c6664f
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview
msc.type: authoredcontent
ms.openlocfilehash: 9786879844da13c21e6a953b1ab24b29ca8121e2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574128"
---
# <a name="enterprise-web-deployment-scenario-overview"></a>Nasazení podnikového webu: Přehledný scénář

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Tato sada kurzů používá ukázkové řešení s realistickým stupněm složitosti spolu se scénářem fiktivního podnikového nasazení, které poskytuje referenční implementaci a poskytuje úlohy a návody ke společnému kontextu. Toto téma popisuje scénář kurzu a zavádí ukázkové řešení.

## <a name="scenario-description"></a>Popis scénáře

Společnost Fabrikam, Inc., fiktivní společnost, vytváří řešení, které umožňuje vzdáleným prodejním týmům ukládat a načítat kontaktní údaje z webového rozhraní.

Procesy správy životního cyklu aplikací (ALM) ve společnosti Fabrikam, Inc. vyžadují, aby bylo řešení nasazeno do tří serverových prostředí v různých fázích procesu vývoje softwaru:

- Vývojářský test nebo prostředí "Sandbox".
- Intranetové přípravné prostředí.
- Internetové prostředí s přístupem k Internetu.

Každé z těchto prostředí má jiné požadavky na konfiguraci a zabezpečení a každá z nich přináší jedinečné výzvy k nasazení.

### <a name="the-fabrikam-inc-server-infrastructure"></a>Infrastruktura serveru Fabrikam, Inc.

Toto je infrastruktura pro vývoj a nasazení vysoké úrovně na společnosti Fabrikam, Inc.

![](enterprise-web-deployment-scenario-overview/_static/image1.png)

Pracovní stanice pro vývojáře, infrastruktura správy zdrojového kódu, vývojové prostředí pro vývojáře a přípravné prostředí se nacházejí v intranetové síti v rámci domény Fabrikam.net. Provozní prostředí se nachází v hraniční síti (označované také jako DMZ, demilitarizovaná zóna a monitorovaná podsíť), která je izolovaná od intranetové sítě bránou firewall. Toto je obvyklý scénář nasazení: obvykle izolujete internetové webové servery od interní serverové infrastruktury pomocí bran firewall nebo serverů brány.

V tomto příkladu:

- Server Team Foundation Server (TFS) 2010 se samostatným serverem sestavení poskytuje funkce správy zdrojového kódu a průběžné integrace (CI).
- Testovací prostředí pro vývojáře zahrnuje webový server Internetová informační služba (IIS) 7,5 a databázový server SQL Server 2008 R2.
- Provozní prostředí obsahuje několik webových serverů služby IIS 7,5 synchronizovaných serverem kontroleru WFF (Web Farm Framework) společně s databázovým serverem SQL Server 2008 R2. V praxi může databázový server pomocí clusteringu nebo zrcadlení zlepšit škálovatelnost a dostupnost.
- Pracovní prostředí je navrženo tak, aby co nejpřesněji provádělo konfiguraci produkčního prostředí.
- Zásady izolace brány firewall a sítě neumožňují přímé automatizované nasazení z intranetu do hraniční sítě.

Konfigurace každého z těchto prostředí je podrobněji popsána v druhém kurzu [Konfigurace serverových prostředí pro nasazení webu](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).

### <a name="team-roles-for-alm"></a>Role týmu pro ALM

Tito uživatelé se podílejí na vytváření, správě, sestavování a publikování řešení Contact Manageru:

- Matný Hink je Vývojář webové aplikace ve společnosti Fabrikam, Inc. Je součástí týmu, který vyvinul řešení Contact Manager pomocí sady Visual Studio 2010. Matný má úplná práva správce na serverech v testovacím prostředí pro vývojáře, které umožňuje nakonfigurovat prostředí tak, aby vyhovovalo vašim potřebám. Má také přístup uživatelů k instanci sady Visual Studio 2010 TFS, kde uložený zdrojový kód pro řešení Contact Manager.
- Rob Walters je správcem serveru pro vývojový tým společnosti Fabrikam, Inc. Rob má na serveru TFS přístup správce, aby mohl nakonfigurovat všechny aspekty TFS a sestavení týmu. Rob má taky přístup správce k testovacím a přípravným webovým serverům a funguje jako správce databáze (DBA) pro databázové servery v testovacích a testovacích prostředích. Rob nakonfiguroval sestavení týmu na serveru TFS, aby mohl provádět tyto úlohy:

    - Sestavujte a spusťte testy jednotek v aplikaci vždy, když uživatel vrátí soubor do TFS. To se označuje jako CI.
    - Nasaďte aplikaci Contact Manager do testovacího prostředí automaticky, jakmile aplikace projde testy jednotek. To zahrnuje publikování databáze na testovací servery při počátečním nasazení a všechny aktualizace databáze po počátečním nasazení.
    - Nasaďte aplikaci Správce kontaktů do přípravného prostředí v procesu s jedním krokem.
    - Vytvořte webový balíček, který může použít k publikování aplikace v produkčním prostředí.
- Lisa Andrews je správce serveru zodpovědný za nasazení aplikací na produkční servery společnosti Fabrikam, Inc. Má oprávnění ke čtení pro sdílenou složku, ve které sestavení týmu TFS po sestavení aplikace Správce kontaktů uloží balíček pro nasazení webu. Má také přístup správce k provozním webovým serverům, aby mohla aplikace nasadit do produkčního prostředí. Navíc funguje jako DBA, který nasazuje databáze a aktualizace databáze na databázový server v provozním prostředí.

<a id="_The_Contact_Manager"></a>

### <a name="the-contact-manager-solution"></a>Řešení správce kontaktů

Řešení Contact Manager je navrženo tak, aby umožňovalo registraci přihlášených uživatelů, kteří přidávají a upravují kontaktní informace prostřednictvím webového rozhraní. Řešení Správce kontaktů se skládá ze čtyř individuálních projektů:

![](enterprise-web-deployment-scenario-overview/_static/image2.png)

- **ContactManager. Mvc**. Toto je projekt webové aplikace ASP.NET MVC3, který představuje vstupní bod pro řešení. Nabízí některé základní funkce webové aplikace, jako je například poskytování možnosti vytvářet a zobrazovat podrobnosti kontaktu. Aplikace spoléhá na službu Windows Communication Foundation (WCF) ke správě kontaktů a databázi služby ASP.NET Application Services pro správu ověřování a autorizace.
- **ContactManager. Database**. Toto je projekt databáze sady Visual Studio 2010. Projekt definuje schéma pro databázi, která obsahuje kontaktní údaje.
- **ContactManager. Service**. Toto je projekt webové služby WCF. WCF zpřístupňuje koncový bod, který volajícím umožňuje provádět operace vytvoření, načtení, aktualizace a odstranění (CRUD) v databázi Správce kontaktů. Služba spoléhá na databázi Správce kontaktů a sestavení ContactManager. Common. dll.
- **ContactManager. Common**. Toto je projekt knihovny tříd. Služba WCF spoléhá na typy definované v tomto sestavení.

Kompletní přezkoumání řešení a jeho požadavků na nasazení najdete v prvním kurzu v této sérii, [nasazení webu v podniku](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).

<a id="_Deployment_Tasks"></a>

## <a name="deployment-tasks"></a>Úlohy nasazení

Nasazení aplikací do různých prostředí ve velké organizaci zahrnuje několik různých úloh. Toto jsou klíčové úlohy, které kurzy pokrývají:

![](enterprise-web-deployment-scenario-overview/_static/image3.png)

Tady je seznam všech kroků v procesu nasazení z perspektivy uživatelů popsaných dříve v tomto dokumentu:

1. Všichni členové týmu si prostudují řešení Contact Manager v aplikaci Visual Studio 2010 k určení klíčových požadavků a problémů při nasazení.
2. Matný Hink může nasadit řešení Contact Manageru přímo z pracovní stanice pro vývojáře do testovacího prostředí pro vývojáře, aby se prováděl počáteční test logiky nasazení.
3. Mat Hink přidá aplikaci do správy zdrojového kódu v TFS.
4. Rob Walters vytvoří v týmovém sestavení různé definice sestavení pro řešení Správce kontaktů. Jedna definice sestavení používá CI k nasazení řešení do testovacího prostředí pro vývojáře vždy, když uživatel vyhledá nový kód. Další definice sestavení umožňuje uživatelům aktivovat nasazení do přípravného prostředí podle potřeby.
5. Pokaždé, když uživatel kontroluje nový kód, týmový Build automaticky sestaví komponenty řešení, spustí testy jednotek a nasadí řešení do testovacího prostředí pro vývojáře, pokud bylo sestavení úspěšné a testy jednotek proběhnou úspěšně.
6. Když uživatel aktivuje nasazení do přípravného prostředí, řešení je zabaleno a nasazeno v jednom kroku procesu. Tento proces také vygeneruje balíček pro ruční nasazení do provozního prostředí.
7. Lisa Andrews nasadí aplikaci do provozního prostředí, a to ručním importem webového balíčku vytvořeného v kroku 6.

### <a name="key-deployment-issues"></a>Problémy s nasazením klíčů

Řešení Contact Manager a společnost Fabrikam, Inc. zvýrazní různé běžné problémy a problémy, se kterými se můžete setkat při nasazení komplexních řešení na podnikové úrovni. Příklad:

- Musíte být schopni nasadit projekty do více prostředí, jako jsou vývojové nebo testovací prostředí, pracovní platformy a provozní servery. Řešení musí být nasazené s jiným nastavením konfigurace pro každé prostředí.
- V rámci jednoho kroku nebo procesu automatického sestavení a nasazení je třeba nasadit více závislých projektů současně.
- Musíte být schopni nasazovat nasazení z automatizovaného procesu. Například chcete použít proces CI k nasazení webových aplikací do přípravného prostředí, když je nový kód vrácen se změnami.
- Musíte být schopni řídit proces nasazení a nastavit proměnné pro nasazení mimo sadu Visual Studio, protože vývojáři pravděpodobně nemají správné nastavení konfigurace nebo potřebná pověření pro každé cílové prostředí.
- Je nutné nasadit databázové projekty založené na schématu a zachovat existující data v následných nasazeních.
- Databáze členství je nutné nasadit na základě ad hoc bez nutnosti nasazovat data uživatelského účtu. Je také možné, že budete muset aktualizovat schéma nasazených databází členství, aniž byste ztratili stávající data uživatelského účtu.
- Pokud nasazujete obsah do různých cílových prostředí, je potřeba vyloučit určité soubory nebo složky.

Kromě toho se Správa nasazení aktualizuje, když jsou aktualizace časté a přírůstkové vyvolává některé další problémy. Příklad:

- Testy jednotek spustíte pokaždé, když vývojář zkontroluje nový kód. Řešení budete chtít nasadit pouze v případě, že kód projde testy jednotek.
- Když nasadíte webovou aplikaci do pracovního nebo produkčního prostředí, chcete uživatele přesměrovat do souboru *offline. htm aplikace\_* po dobu trvání procesu nasazení.
- Chcete protokolovat činnosti nasazení. Proces nasazení by měl odeslat e-mailová oznámení o úspěšných nebo neúspěšných nasazeních určeným příjemcům.
- Pokud automatické nasazení neproběhne úspěšně, proces nasazení by měl zopakovat aktuální nasazení nebo nasadit předchozí webový balíček.

> [!div class="step-by-step"]
> [Předchozí](deploying-web-applications-in-enterprise-scenarios.md)
> [Další](application-lifecycle-management-from-development-to-production.md)

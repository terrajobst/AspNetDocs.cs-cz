---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
title: Výběr správného přístupu k nasazení webu | Microsoft Docs
author: jrjlee
description: Když pracujete s nástrojem Internetová informační služba (IIS) web pro nasazení webu (Nasazení webu) 2,0 nebo novějším, existují tři hlavní přístupy, které můžete použít k získání...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 787a53fd-9901-4a11-9d58-61e0509cda45
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 13f784dd8e6404806104d56b026b3c41ca178892
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78548480"
---
# <a name="choosing-the-right-approach-to-web-deployment"></a>Výběr správného přístupu k nasazení webu

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Když pracujete s nástrojem Internetová informační služba (IIS) web pro nasazení webu (Nasazení webu) 2,0 nebo novějším, existují tři hlavní přístupy, které můžete použít k získání zabalené webové aplikace na webový server. Máte tyto možnosti:
> 
> - Nasaďte aplikaci ze vzdáleného umístění tak, že na cílovém serveru zacílíte na *službu Web Deployment Agent* (také označovanou jako "vzdálený agent").
> - Nasaďte aplikaci ze vzdáleného umístění pomocí Nasazení webu na vyžádání (označuje se také jako "dočasný agent").
> - Nasaďte aplikaci ze vzdáleného umístění tím, že zacílíte na *obslužnou rutinu nasazení webu služby IIS* na cílovém serveru.
> - Nasaďte aplikaci ručním zkopírováním webového balíčku do cílového serveru a jeho importem prostřednictvím Správce služby IIS.
> 
> Způsob konfigurace cílových webových serverů bude záviset na tom, který přístup k nasazení chcete použít. Toto téma vám pomůže určit, který přístup k nasazení je pro vás nejvhodnější.

V této tabulce jsou uvedeny hlavní výhody a nevýhody jednotlivých přístupů k nasazení spolu s scénáři, které většinou vyhovují jednotlivým přístupům.

| Přístup | Výhody | Nevýhody | Typické scénáře |
| --- | --- | --- | --- |
| Vzdálený agent | Nastavení je snadné. Je vhodný pro běžné aktualizace webových aplikací a obsahu. | Uživatel musí být na cílovém serveru správcem. uživatel nemůže zadat alternativní přihlašovací údaje. | Vývojová prostředí. Testovací prostředí. |
| Dočasný Agent | V cílovém počítači není nutné instalovat Nasazení webu. K automatickému použití se používá nejnovější verze Nasazení webu. | Uživatel musí být na cílovém serveru správcem. uživatel nemůže zadat alternativní přihlašovací údaje. | Vývojová prostředí. Testovací prostředí. |
| Obslužná rutina Nasazení webu | Uživatelé, kteří nejsou správci, můžou obsah nasadit. Je vhodný pro běžné aktualizace webových aplikací a obsahu. | Nastavení je mnohem složitější. | Přípravná prostředí. Intranetová produkční prostředí. Hostovaná prostředí. |
| Offline nasazení | Nastavení je velmi snadné. Je vhodný pro izolovaná prostředí. | Správce serveru musí vždy ručně zkopírovat a importovat webový balíček. | Internetová produkční prostředí. Izolovaná síťová prostředí. |

## <a name="using-the-remote-agent"></a>Používání vzdáleného agenta

Když instalujete Nasazení webu s použitím výchozího nastavení na cílovém serveru, služba Web Deployment Agent ("vzdálený agent") se automaticky nainstaluje a spustí. Vzdálený agent ve výchozím nastavení zveřejňuje koncový bod HTTP na této adrese:

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample1.cmd)]

> [!NOTE]
> [*Server*] můžete nahradit názvem počítače vašeho webového serveru, IP adresou vašeho webového serveru nebo názvem hostitele, který se překládá na váš webový server.

Správci serveru mohou nasadit webové balíčky ze vzdáleného umístění, jako je vývojářský počítač nebo server sestavení, zadáním této adresy koncového bodu. Předpokládejme například, že mat Hink ve společnosti Fabrikam, Inc. sestavil projekt webové aplikace ContactManager. Mvc na svém vývojářském počítači. Proces sestavení vygeneruje webový balíček společně se souborem *. deploy. cmd* , který obsahuje nasazení webu příkazy potřebné k instalaci balíčku. Pokud je podkladem správce serveru na serveru TESTWEB1, může webovou aplikaci nasadit na testovací webový server spuštěním tohoto příkazu na svém počítači pro vývojáře:

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample2.cmd)]

Ve skutečnosti může spustitelný soubor Nasazení webu odvodit adresu koncového bodu vzdáleného agenta, pokud zadáte název počítače, takže v podkladu je třeba zadat pouze tento příkaz:

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample3.cmd)]

> [!NOTE]
> Další informace o Nasazení webu syntaxe příkazového řádku a souborech *. deploy. cmd* naleznete v tématu [How to: install a Deployment Package by using a Deploy. cmd File](https://msdn.microsoft.com/library/ff356104.aspx).

Vzdálený agent nabízí přímý způsob, jak nasadit obsah ze vzdáleného umístění a tento přístup může fungovat dobře při jednom nebo automatizovaném nasazení. Uživatel, který spouští příkaz pro nasazení, ale musí být také správcem domény nebo členem místní skupiny Administrators na cílovém serveru. Kromě toho vzdálený agent nepodporuje základní ověřování, takže nemůžete předat alternativní přihlašovací údaje na příkazovém řádku.

Vzdálený agent poskytuje užitečný přístup k nasazení ve scénářích vývoje nebo testování, kde pro vývojáře není neobvyklé mít plnou kontrolu nad testovacím serverem a aplikace se obvykle znovu sestavují a nasazují. používáte. Tento přístup je však obvykle méně přijatelný pro pracovní nebo produkční prostředí.

Úplný příklad scénáře, který používá přístup ke vzdálenému agentovi, najdete v tématu [scénář: konfigurace testovacího prostředí pro nasazení webu](scenario-configuring-a-test-environment-for-web-deployment.md).

## <a name="using-the-temp-agent"></a>Použití dočasného agenta

Přístup k dočasným agentům k nasazení je podobný přístupu ke vzdálenému agentovi. Na rozdíl od přístupu ke vzdálenému agentu ale nemusíte na cílovém webovém serveru Nasazení webu instalovat. Při nasazení Nasazení webu nainstaluje na cílovém serveru dočasnou verzi služby Agent pro nasazení webu a použije se k nasazení vašeho obsahu do služby IIS. Až se nasazení dokončí, odeberou se všechny dočasné soubory.

Pokud chcete použít nastavení dočasná poskytovatel agenta, přidejte do příkazu nasazení příznak **/g** :

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample4.cmd)]

> [!NOTE]
> Dočasného agenta nelze použít, pokud je v cílovém počítači nainstalována služba Agent nasazení webu, a to i v případě, že služba není spuštěna.

Výhodou tohoto přístupu je, že nemusíte spravovat instalace Nasazení webu na cílových serverech. Navíc nemusíte zajišťovat, aby na zdrojovém a cílovém počítači běžela stejná verze Nasazení webu. Tento přístup ale utrpí ze stejných omezení zabezpečení jako vzdálený přístup k agentům, konkrétně proto, že musíte být místním správcem cílového serveru, abyste mohli nasadit obsah, a podporuje se jenom ověřování NTLM. Přístup k dočasnému agentovi také vyžaduje mnohem více počátečních konfigurací cílového prostředí.

Další informace o použití dočasného agenta najdete v tématu [Postup: instalace balíčku pro nasazení pomocí souboru Deploy. cmd](https://msdn.microsoft.com/library/ff356104.aspx) a [nasazení webu na vyžádání](https://technet.microsoft.com/library/ee517345(WS.10).aspx).

## <a name="using-the-web-deploy-handler"></a>Použití obslužné rutiny Nasazení webu

Pro IIS 7 a vyšší Nasazení webu nabízí alternativní přístup k nasazení prostřednictvím obslužné rutiny Nasazení webu služby IIS. Obslužná rutina Nasazení webu úzce integrována se službou IIS Web Management Service (WMSvc), která je navržena tak, aby uživatelům umožnila správu webů IIS ze vzdálených umístění.

Vzdálený agent ve výchozím nastavení zveřejňuje koncový bod HTTP na této adrese:

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample5.cmd)]

> [!NOTE]
> [*Server*] můžete nahradit názvem počítače vašeho webového serveru, IP adresou vašeho webového serveru nebo názvem hostitele, který se překládá na váš webový server.

Velkou výhodou Nasazení webu obslužné rutiny přes vzdáleného agenta a dočasného agenta je, aby bylo možné nakonfigurovat službu IIS tak, aby uživatelé bez oprávnění správce mohli nasazovat aplikace a obsah na konkrétní weby služby IIS. Obslužná rutina Nasazení webu také podporuje základní ověřování, takže v příkazech Nasazení webu můžete zadat alternativní přihlašovací údaje jako parametry. Hlavní nevýhodou je, že obslužná rutina Nasazení webu je zpočátku mnohem složitější, aby se nastavila a nakonfigurovala.

V případě uživatelů bez oprávnění správce umožní služba webové správy (WMSvc) uživateli připojit se ke službě IIS pomocí připojení na úrovni webu místo připojení na úrovni serveru. Pro přístup k určité lokalitě můžete do adresy koncového bodu zahrnout řetězec dotazu specifický pro lokalitu:

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample6.cmd)]

Předpokládejme například, že proces sestavení je konfigurován pro automatické nasazení webové aplikace do přípravného prostředí po každém úspěšném sestavení. Pokud jste použili vzdálený přístup k agentům, je nutné, aby proces sestavení identifikoval správce na cílových serverech. V opačném případě použití obslužné rutiny nasazení webu můžete udělit uživateli&#x2014;bez oprávnění správce**FABRIKAM\stagingdeployer** v tomto případě&#x2014;oprávnění pouze pro konkrétní web služby IIS a proces sestavení může poskytnout tyto přihlašovací údaje k nasazení webového balíčku.

[!code-console[Main](choosing-the-right-approach-to-web-deployment/samples/sample7.cmd)]

> [!NOTE]
> Další informace o Nasazení webu operací a syntaxi příkazového řádku najdete v tématu [nasazení webu příkazového řádku reference](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx). Další informace o použití souboru *. deploy. cmd* naleznete v tématu [How to: install a Deployment Package by using a Deploy. cmd File](https://msdn.microsoft.com/library/ff356104.aspx).

Obslužná rutina Nasazení webu poskytuje užitečný přístup k nasazení v pracovních prostředích, hostovaných prostředích a intranetových produkčních prostředích, kde je k dispozici vzdálený přístup k serveru, ale přihlašovací údaje správce.

Ucelený příklad scénáře, který používá přístup k obslužné rutině Nasazení webu, najdete v tématu [scénář: Konfigurace přípravného prostředí pro nasazení webu](scenario-configuring-a-staging-environment-for-web-deployment.md).

## <a name="using-offline-deployment"></a>Použití offline nasazení

V některých případech není možné nebo praktické nasadit aplikace a obsah na web IIS ze vzdáleného umístění. Například zdrojový a cílový počítač může být v izolovaných sítích nebo síťových segmentech nebo zásada brány firewall nemusí povolit vzdálený přístup.

Ve scénářích, které mají, můžete dál používat možnosti balení a publikování Nasazení webu; nemůžete je jenom používat ze vzdáleného umístění. Místo toho musí správce cílového serveru zkopírovat webový balíček na server a importovat ho pomocí Správce služby IIS.

![](choosing-the-right-approach-to-web-deployment/_static/image1.png)

Přístup k offline nasazení je obvykle užitečný v produkčním prostředí s přístupem k Internetu, kde servery v hraniční síti můžou mít omezené možnosti připojení k počítačům v interní síti.

Ucelený příklad scénáře, který využívá přístup k offline nasazení, najdete v tématu [scénář: Konfigurace provozního prostředí pro nasazení webu](scenario-configuring-a-production-environment-for-web-deployment.md).

## <a name="further-reading"></a>Další čtení

Další informace o Nasazení webu operací a syntaxi příkazového řádku najdete v tématu [nasazení webu příkazového řádku reference](https://technet.microsoft.com/library/dd568991(v=ws.10).aspx). Další informace o použití souboru *. deploy. cmd* naleznete v tématu [How to: install a Deployment Package by using a Deploy. cmd File](https://msdn.microsoft.com/library/ff356104.aspx).

Obecnější informace o různých způsobech, kterými můžete nasadit webové balíčky ze vzdáleného počítače, najdete v tématu [použití nasazení webu vzdáleně](https://technet.microsoft.com/library/ee461175(WS.10).aspx). Další informace o používání Nasazení webu na vyžádání najdete v článku [nasazení webu na vyžádání](https://technet.microsoft.com/library/ee517345(WS.10).aspx).

> [!div class="step-by-step"]
> [Předchozí](configuring-server-environments-for-web-deployment.md)
> [Další](scenario-configuring-a-test-environment-for-web-deployment.md)

---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
title: Konfigurace oprávnění pro nasazení týmového sestavení | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak nakonfigurovat oprávnění, aby mohl server sestavení nasadit obsah na webové servery a databázové servery jako součást automatizovaného b...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 2488a91e-b0a8-465a-b874-3233f724b56b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-permissions-for-team-build-deployment
msc.type: authoredcontent
ms.openlocfilehash: 5699f72af6b8d7f18d1a2c631dfdedd63c66e1e6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638423"
---
# <a name="configuring-permissions-for-team-build-deployment"></a>Konfigurace oprávnění pro nasazení týmového sestavení

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak nakonfigurovat oprávnění, aby mohl server sestavení nasadit obsah na webové servery a databázové servery jako součást procesu automatizovaného sestavení.

Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého [řešení](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.

Metoda nasazení na srdce těchto kurzů je založena na způsobu rozdělení souborů projektu popsaných v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md), ve kterém je proces sestavení řízen dvěma soubory&#x2014;projektu jeden, který obsahuje pokyny pro sestavení, které platí pro každé cílové prostředí, a jedno obsahující nastavení sestavení a nasazení specifické pro konkrétní prostředí. V době sestavení je soubor projektu specifický pro prostředí sloučen do souboru projektu prostředí – nezávislá a vytvoří kompletní sadu instrukcí pro sestavení.

## <a name="task-overview"></a>Přehled úlohy

Při instalaci služby Team Foundation Server (TFS) 2010 Build Service zadáte identitu, se kterou chcete službu spustit. Ve výchozím nastavení je to účet síťové služby. Případně můžete službu sestavení nakonfigurovat tak, aby běžela pomocí doménového účtu.

Všechny úlohy nasazení, které vyžadují ověřování systému Windows a které plánujete automatizovat pomocí sestavení týmu, se spustí pomocí identity sestavovací služby. V takovém případě je potřeba udělit identitě sestavovací služby veškerá požadovaná oprávnění na webových serverech a na vašich databázových serverech.

> [!NOTE]
> Účet síťové služby používá účet počítače k ověřování pro jiné počítače. Účty počítačů mají podobu * [název domény]\[název počítače] * **$** &#x2014;například **FABRIKAM\TFSBUILD $** . V takovém případě, pokud je vaše sestavovací služba spuštěna pomocí identity síťové služby, měli byste udělit všechna požadovaná oprávnění k identitě účtu počítače pro server sestavení.

## <a name="configuring-web-server-permissions"></a>Konfigurace oprávnění webového serveru

Jak je popsáno v tématu [Volba správného přístupu k nasazení webu](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md), existují dva hlavní přístupy, které můžete použít, pokud chcete nasadit webové balíčky na vzdálený webový server:

- Nasaďte aplikaci ze vzdáleného umístění tak, že na cílovém serveru zacílíte na *službu Web Deployment Agent* (také označovanou jako vzdálený Agent).
- Nasaďte aplikaci ze vzdáleného umístění tím, že na cílovém serveru zacílíte*obslužnou rutinu nasazení webu Internetová informační služba (IIS)* .

Vzdálený agent má v tomto případě dvě klíčová omezení:

- Vzdálený Agent podporuje pouze ověřování NTLM. Jinými slovy, nasazení musí používat identitu&#x2014;sestavovací služby. nemůžete zosobnit jiný účet.
- Chcete-li použít vzdáleného agenta, musí být účet, který provádí nasazení, správcem cílového serveru.

Tato dvě omezení společně přistupují ke vzdálenému agentovi při automatizovaném nasazení týmového sestavení. Chcete-li použít tento přístup, je nutné, aby byl účet služby sestavení správcem na všech cílových webových serverech.

Naproti tomu Nasazení webu přístup k obslužné rutině nabízí různé výhody:

- Obslužná rutina Nasazení webu podporuje základní ověřování přes protokol HTTPS, které umožňuje předat přihlašovací údaje alternativního účtu k nástroji pro nasazení webu služby IIS (Nasazení webu).
- Cílové webové servery můžete nakonfigurovat tak, aby umožňovaly uživatelům bez oprávnění správce nasadit obsah na konkrétní weby IIS pomocí obslužné rutiny Nasazení webu.

V důsledku toho je vhodné při automatizaci nasazení webového balíčku z týmového sestavení přesně cílit na obslužnou rutinu Nasazení webu. Toto je doporučený postup:

1. Vytvořte doménový účet s nízkou úrovní oprávnění, který bude použit pro nasazení.
2. Nakonfigurujte obslužnou rutinu Nasazení webu a udělte účtu požadovaná oprávnění k nasazení obsahu na konkrétní web IIS, jak je popsáno v tématu [Konfigurace webového serveru pro nasazení webu publikování (nasazení webu obslužné rutiny)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).
3. K provedení tohoto nasazení můžete vyvolat Nasazení webu a cílit na obslužnou rutinu Nasazení webu pomocí základního ověřování a zadáním přihlašovacích údajů účtu domény, který jste vytvořili.

V ukázkovém řešení [Contact Manageru](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) zadáte typ ověřování (Basic nebo NTLM), přihlašovací údaje nasazení webu a adresu koncového bodu (vzdálený agent nebo nasazení webu obslužné rutiny) v souboru projektu specifického pro prostředí. Tyto hodnoty se používají k formulování a spuštění Nasazení webu příkazu při spuštění souboru projektu. Další informace najdete v tématu [nasazení webových balíčků](../web-deployment-in-the-enterprise/deploying-web-packages.md).

Další informace o konfiguraci obslužné rutiny Nasazení webu, včetně postupu konfigurace oprávnění, najdete v tématu [Konfigurace webového serveru pro nasazení webu publikování (nasazení webu obslužné rutiny)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md). Další informace o konfiguraci vzdáleného agenta najdete v tématu [Konfigurace webového serveru pro nasazení webu publikování (vzdálený Agent)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md).

## <a name="configuring-database-server-permissions"></a>Konfigurace oprávnění databázového serveru

Pokud chcete nasadit databázi do SQL Server, musíte:

- Vytvořte přihlašovací údaje pro účet nasazení v instanci SQL Server.
- Udělte přihlašovacímu jménu oprávnění **dbcreator** pro instanci SQL Server.
- Po počátečním nasazení přidejte přihlašovací údaje do role **vlastníka\_DB** v cílové databázi. To je nutné kvůli dalším nasazením, přičemž místo vytvoření nové databáze měníte stávající databázi.

Můžete provést ověření u SQL Server instance pomocí ověřování NTLM nebo ověřování SQL Server:

- Pokud používáte ověřování NTLM, je nutné udělit oprávnění popsaná výše k účtu sestavovací služby.
- Pokud používáte ověřování SQL Server, musíte udělit oprávnění popsaná výše k účtu SQL Server. V připojovacím řetězci, který použijete k nasazení databáze, musíte také zadat uživatelské jméno a heslo SQL Server.

Podrobné informace o tom, jak nakonfigurovat oprávnění pro nasazení databáze, najdete v tématu [Konfigurace databázového serveru pro nasazení webu publikování](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).

## <a name="conclusion"></a>Závěr

V tuto chvíli byste měli pochopit požadovaná oprávnění, společně s možnostmi ověřování, které jsou otevřené pro vás, při automatizaci nasazení webové aplikace a databáze z týmového sestavení. Měli byste taky mít přístup k potřebným oprávněním pro webové servery služby IIS a SQL Server databázových serverů.

## <a name="further-reading"></a>Další čtení

Další informace o konfiguraci prostředí Windows serveru pro podporu vzdáleného nasazení najdete v tématu [Konfigurace serverových prostředí pro nasazení webu](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).

> [!div class="step-by-step"]
> [Předchozí](deploying-a-specific-build.md)

---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
title: Řešení Správce kontaktů | Microsoft Docs
author: jrjlee
description: Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého řešení&#x2014;správce kontaktů představuje aplikaci na úrovni podniku s reálným Leve...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 4d8c8d19-055b-4b70-9ee1-f748f0db3a01
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/the-contact-manager-solution
msc.type: authoredcontent
ms.openlocfilehash: 12ed7827f7392e559e04121386f7cd045de8462b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586266"
---
# <a name="the-contact-manager-solution"></a>Řešení správce kontaktů

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Tato [série kurzů](web-deployment-in-the-enterprise.md) používá ukázkové řešení&#x2014;, pomocí kterého řešení&#x2014;správce kontaktů představuje podnikovou aplikaci s realistickou úrovní složitosti. Toto téma představuje řešení Správce kontaktů, popisuje klíčové součásti řešení a identifikuje výzvy k nasazení tohoto druhu aplikace na různé cílové platformy v podnikovém prostředí.
> 
> Při práci s tématy v těchto kurzech můžete použít řešení Správce kontaktů jako referenční implementaci, která ukazuje, jak můžete ve scénářích podnikového nasazení splnit konkrétní problémy. V dalším tématu, [nastavování řešení Správce kontaktů](setting-up-the-contact-manager-solution.md), popisuje, jak stáhnout a spustit řešení na pracovní stanici pro vývojáře.

## <a name="solution-overview"></a>Přehled řešení

Řešení Správce kontaktů se skládá ze čtyř individuálních projektů:

![](the-contact-manager-solution/_static/image1.png)

- **ContactManager. Mvc**. Toto je projekt webové aplikace ASP.NET MVC 3, který představuje vstupní bod pro řešení. Nabízí některé základní funkce webové aplikace, jako je například poskytování možnosti vytvářet a zobrazovat podrobnosti kontaktu. Aplikace spoléhá na službu Windows Communication Foundation (WCF) ke správě kontaktů a databázi služby ASP.NET Application Services pro správu ověřování a autorizace.
- **ContactManager. Database**. Toto je projekt databáze sady Visual Studio. Projekt definuje schéma pro databázi, která obsahuje kontaktní údaje.
- **ContactManager. Service**. Toto je projekt webové služby WCF. Služba WCF zpřístupňuje koncový bod, který volajícím umožňuje provádět operace vytvoření, načtení, aktualizace a odstranění (CRUD) v databázi **ContactManager** . Služba spoléhá na databázi **ContactManager** a na sestavení **ContactManager. Common. dll** .
- **ContactManager. Common**. Toto je projekt knihovny tříd. Služba WCF spoléhá na typy definované v tomto sestavení.

Řešení zahrnuje také složku řešení s názvem Publish. Obsahuje různé vlastní soubory projektu a soubory příkazů, které ukazují, jak lze řídit a manipulovat s procesem sestavení a nasazení. Tyto informace jsou podrobněji popsány dále v tomto kurzu.

Na koncepční úrovni se součásti řešení vejdou dohromady takto:

![](the-contact-manager-solution/_static/image2.png)

> [!NOTE]
> I když webová aplikace ASP.NET MVC 3 používá poskytovatele členství ASP.NET, všechny stránky v rámci webové aplikace povolují anonymní přístup. To je jasně nerealistické nastavení. Toto řešení je ale nastavené tak, aby bylo snazší ho nasadit a otestovat bez konfigurace uživatelských účtů a rolí.

## <a name="deployment-challenges"></a>Problémy s nasazením

Řešení Správce kontaktů znázorňuje několik problémů s nasazením, které jsou společné pro mnoho scénářů nasazení podniku:

- Řešení se skládá z více závislých projektů. Tyto projekty je nutné nasadit současně.
- Připojovací řetězce a koncové body služby je potřeba aktualizovat pro každé prostředí a v mnoha případech tyto informace nebudou pro vývojáře dostupné.
- Když nasadíte databázi **ContactManager** do přípravného a produkčního prostředí, je potřeba zachovat stávající data v následných nasazeních.
- Když nasadíte databázi služby ASP.NET Application Services, je potřeba nasadit některá konfigurační data, ale vynechat všechna data uživatelského účtu.
- Projekty obsahují některé soubory a složky, které by neměly být nasazeny. Tyto soubory a složky je potřeba z procesu nasazení vyloučit.
- Řešení musí podporovat automatizované nasazení ze serveru sestavení Team Foundation Server (TFS).

## <a name="conclusion"></a>Závěr

V tomto tématu najdete základní informace o řešení Contact Manageru a zjistili jsme některé z hlavních problémů při nasazení, které jsou společné pro mnoho scénářů nasazení v podniku. Zbývající témata v tomto kurzu popisují některé postupy, které můžete použít ke splnění těchto problémů.

V dalším tématu, [nastavování řešení Správce kontaktů](setting-up-the-contact-manager-solution.md), popisuje, jak stáhnout a spustit řešení na pracovní stanici pro vývojáře.

> [!div class="step-by-step"]
> [Předchozí](web-deployment-in-the-enterprise.md)
> [Další](setting-up-the-contact-manager-solution.md)

---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments
title: Nasazení databází členství v podnikových prostředích | Microsoft Docs
author: jrjlee
description: Toto téma vysvětluje klíčové doporučení a problémy, které je potřeba překonat při zřizování databází ASP.NET Application Services (častěji...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 3cf765df-d311-4f68-a295-c9685ceea830
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments
msc.type: authoredcontent
ms.openlocfilehash: 50f49af502b75aa5ad52756a76a5e7340aca53f7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526003"
---
# <a name="deploying-membership-databases-to-enterprise-environments"></a>Nasazení databází členství do podnikových prostředí

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma vysvětluje klíčové doporučení a problémy, které budete muset překonat při zřizování databází ASP.NET Application Services (častěji označované jako databáze členství) v testovacích, pracovních nebo produkčních prostředích. Popisuje také přístupy, které můžete použít ke splnění těchto výzev.

Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého [řešení](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.

Metoda nasazení na srdce těchto kurzů je založena na způsobu rozdělení souborů projektu popsaných v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md), ve kterém je proces sestavení řízen dvěma soubory&#x2014;projektu jeden, který obsahuje pokyny pro sestavení, které platí pro každé cílové prostředí, a jedno obsahující nastavení sestavení a nasazení specifické pro konkrétní prostředí. V době sestavení je soubor projektu specifický pro prostředí sloučen do souboru projektu prostředí – nezávislá a vytvoří kompletní sadu instrukcí pro sestavení.

## <a name="what-are-the-issues-when-you-deploy-a-membership-database"></a>Jaké jsou problémy při nasazení databáze členství?

Ve většině případů, když navrhujete strategii nasazení pro databázi, je první věc, kterou je potřeba zvážit, ta data, která chcete nasadit. Ve vývojovém nebo testovacím prostředí můžete chtít nasadit data uživatelského účtu, abyste usnadnili rychlé a snadné testování. V pracovním nebo produkčním prostředí je velmi pravděpodobné, že byste chtěli nasadit data uživatelského účtu.

Databáze členství ASP.NET bohužel zavádí některé konkrétní výzvy, které by toto rozhodnutí bylo mnohem složitější:

- Nasazení pouze schématu ponechá databázi členství v nefunkčním stavu. Důvodem je to, že databáze členství zahrnuje některá konfigurační data (v tabulce **aspnet\_SchemaVersions** ), kterou databáze vyžaduje, aby fungovala. Pokud například provádíte nasazení databáze členství pouze ve schématu, aby bylo možné vyloučit data uživatelského účtu, budete muset spustit skript po nasazení, který přidá základní konfigurační data.
- V závislosti na tom, jak je vaše databáze členství nakonfigurovaná, může zprostředkovatel členství použít klíč počítače k šifrování hesel a jejich uložení v databázi. V takovém případě se všechna data uživatelského účtu, která nasazujete s databází, stanou na cílovém serveru nepoužitelná. Z tohoto důvodu není nasazení dat uživatelských účtů podporovaným scénářem.

## <a name="choosing-a-membership-database-strategy"></a>Výběr strategie databáze členství

Tyto pokyny použijte, když zvolíte, jak zřídit databázi členství v prostředí podnikového serveru:

- Bez ohledu na to, co je to možné, nesaďte databáze členství. Místo toho vytvořte databázi členství ručně na cílovém databázovém serveru. Pokud jste nepřizpůsobili schéma databáze členství, můžete jednoduše vytvořit nový v umístění v umístění pomocí [nástroje ASP.NET SQL Server Registration Tool (aspnet\_regsql. exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx).
- Pokud nemáte žádnou možnost, ale chcete nasadit databázi&#x2014;členství, například pokud jste provedli rozsáhlé úpravy schématu&#x2014;databáze, měli byste provést nasazení databáze členství pouze schématu, vyloučit data uživatelského účtu a pak spustit skript po nasazení, který přidá požadovaná konfigurační data. Obecné pokyny k těmto postupům najdete v tématu [Postupy: nasazení databáze členství ASP.NET bez zahrnutí uživatelských účtů](https://msdn.microsoft.com/library/ff361972(v=vs.100).aspx).

Je důležité si uvědomit, že *schéma vaší databáze členství je pravděpodobně poměrně statické*. I v případě, že jste přizpůsobili databázi členství, je pravděpodobné, že bude nutné pravidelně&#x2014;aktualizovat schéma, které se nemění se stejnou frekvencí jako kód ve webové aplikaci nebo databázovém projektu. V takovém případě není nutné zahrnout databázi členství do procesů automatizovaného nebo jednoduchého nasazení.

## <a name="using-vsdbcmd-to-update-a-membership-database-schema"></a>Použití VSDBCMD k aktualizaci schématu databáze členství

Pokud upravíte strukturu databáze členství po prvním nasazení, nebudete chtít k opětovnému nasazení databáze používat nástroj pro nasazení webu Internetová informační služba (IIS) (Nasazení webu). Funkce nasazení databáze v Nasazení webu nezahrnuje možnost vytvářet rozdílové aktualizace cílové databáze&#x2014;, nasazení webu musí databázi vyřadit a znovu vytvořit. To znamená, že ztratíte všechna existující data uživatelského účtu, což je obvykle nežádoucí v pracovních nebo produkčních prostředích.

Alternativou je použití nástroje VSDBCMD k aktualizaci schématu cílové databáze. VSDBCMD obsahuje dvě důležité možnosti. Nejprve může importovat schéma existující databáze do souboru. dbschema. Za druhé může nasadit soubor. dbschema do existující databáze jako rozdílovou aktualizaci, což znamená, že provede pouze změny, které vyžadují, aby byla cílová databáze aktuální, a neztratíte žádná data.

K aktualizaci schématu databáze členství můžete použít tyto kroky vysoké úrovně:

1. Pomocí akce **importu** VSDBCMD vygenerujte soubor. dbschema pro vaši zdrojovou databázi členství. Tento postup je popsaný v tématu [Postupy: Import schématu z příkazového řádku](https://msdn.microsoft.com/library/dd172135.aspx).
2. K nasazení souboru. dbschema do cílové databáze členství použijte akci **nasazení** VSDBCMD. Tento postup je popsaný v tématu [Reference k příkazovému řádku pro VSDBCMD. EXE (nasazení a import schématu)](https://msdn.microsoft.com/library/dd193283.aspx).

## <a name="conclusion"></a>Závěr

Toto téma popisuje některé problémy, se kterými se můžete setkat, když potřebujete zřídit ASP.NET databáze členství v různých cílových prostředích. Konkrétně vysvětluje, proč nasazení pouze schématu ponechá databázi členství v nefunkčním stavu a proč není podporována implementace dat uživatelského účtu. V tématu najdete také pokyny k zřizování, nasazování a aktualizaci databází členství v různých scénářích.

## <a name="further-reading"></a>Další čtení

Další pokyny a příklady použití VSDBCMD najdete v tématu [Reference k příkazovému řádku pro VSDBCMD. EXE (nasazení a import schématu)](https://msdn.microsoft.com/library/dd193283.aspx) a [Postupy: Import schématu z příkazového řádku](https://msdn.microsoft.com/library/dd172135.aspx). Další informace o použití ASPNET\_regsql. exe k vytvoření databází členství najdete v tématu [nástroj ASP.NET pro registraci SQL Server (aspnet\_regsql. exe)](https://msdn.microsoft.com/library/ms229862(v=vs.100).aspx). Obecnější pokyny k nasazení databází členství najdete v tématu [How to: Deploy a ASP.NET Membership Database bez zahrnutí uživatelských účtů](https://msdn.microsoft.com/library/ff361972(v=vs.100).aspx).

> [!div class="step-by-step"]
> [Předchozí](deploying-database-role-memberships-to-test-environments.md)
> [Další](excluding-files-and-folders-from-deployment.md)

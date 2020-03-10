---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
title: Konfigurace serveru sestavení TFS pro nasazení webu | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak připravit server sestavení Team Foundation Server (TFS) pro sestavení a nasazení vašich řešení pomocí sestavení týmu a internetového Informat...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f8400241-4f4b-4bbd-9994-54fb64909e6e
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: b3aaf7234706d149a3c784347528923f662c3511
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78631094"
---
# <a name="configuring-a-tfs-build-server-for-web-deployment"></a>Konfigurace serveru TFS Build pro nasazení webu

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak připravit server sestavení Team Foundation Server (TFS) pro sestavení a nasazení vašich řešení pomocí týmového sestavení a nástroje pro nasazení webu služby Internetová informační služba (Nasazení webu).

Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého [řešení](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.

Metoda nasazení na srdce těchto kurzů je založena na způsobu rozdělení souborů projektu popsaných v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md), ve kterém je proces sestavení řízen dvěma soubory&#x2014;projektu jeden, který obsahuje pokyny pro sestavení, které platí pro každé cílové prostředí, a jedno obsahující nastavení sestavení a nasazení specifické pro konkrétní prostředí. V době sestavení je soubor projektu specifický pro prostředí sloučen do souboru projektu prostředí – nezávislá a vytvoří kompletní sadu instrukcí pro sestavení.

## <a name="task-overview"></a>Přehled úlohy

K přípravě serveru sestavení pro sestavení a nasazení vašich řešení budete potřebovat:

- Nainstalujte a nakonfigurujte sestavovací službu TFS.
- Nainstalujte Visual Studio 2010.
- Nainstalujte všechny produkty nebo komponenty, které jsou nutné k sestavení vašeho řešení, například verze .NET Framework nebo ASP.NET MVC.
- Nainstalujte Nasazení webu 2,0 nebo novější.

V tomto tématu se dozvíte, jak provádět tyto postupy, nebo ukazují na další prostředky, kde existují. V úlohách a návodech v tomto tématu se předpokládá, že:

- Začínáte s čistým sestavením serveru, na kterém běží Windows Server 2008 R2 Service Pack 1.
- Server je připojený k doméně se statickou IP adresou.
- Nainstalovali jste aplikační vrstvu TFS na samostatný server, jak je popsáno v tématu [Přehled podnikového nasazení webu: scénář](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md).

### <a name="who-performs-these-procedures"></a>Kdo provádí tyto postupy?

Ve většině případů bude správce TFS zodpovědný za konfiguraci serverů sestavení. V některých případech může tým pro vývojáře převzít vlastnictví konkrétních serverů sestavení.

## <a name="install-and-configure-the-tfs-build-service"></a>Instalace a konfigurace sestavovací služby TFS

Při konfiguraci serveru sestavení je prvním úkolem, jak nainstalovat a nakonfigurovat službu TFS Build Service. V rámci tohoto procesu budete potřebovat:

- Nainstalujte sestavovací službu TFS a nakonfigurujte účet služby. Všechny úlohy sestavení, včetně nasazení, se spustí pomocí identity účtu sestavovací služby.
- Vytvořte *kontrolér sestavení* a jednoho nebo více *agentů sestavení*. Každý kontrolér sestavení spravuje sadu agentů sestavení. Při zařazování sestavení do fronty přiřadí kontrolér sestavení úlohu sestavení k dostupnému agentu sestavení. Každá kolekce týmových projektů v TFS je namapována na jeden kontrolér sestavení.
- Konfigurace ukládací složky pro výstupy sestavení. Toto je síťová sdílená složka. Všechny výstupy sestavení, jako jsou balíčky pro nasazení webu, se odesílají do ukládací složky.

Kapitola [Správa Team Foundation Build](https://msdn.microsoft.com/library/ms252495.aspx) na webu MSDN obsahuje všechny prostředky, které potřebujete k provedení těchto úloh:

- Koncepční přehled sestavení Team Foundation, včetně sestavovací služby, kontrolérů sestavení a agentů sestavení, naleznete v tématu [Principy systému sestavení Team Foundation](https://msdn.microsoft.com/library/dd793166.aspx).
- Informace o instalaci a konfiguraci sestavovací služby naleznete v tématu [Configure a Build Machine](https://msdn.microsoft.com/library/ms181712.aspx).
- Informace o vytváření kontrolérů sestavení najdete v tématu [Vytvoření a práce s řadičem sestavení](https://msdn.microsoft.com/library/ee330987.aspx).
- Informace o vytváření agentů sestavení najdete v tématu [Vytvoření a práce s agenty sestavení](https://msdn.microsoft.com/library/bb399135.aspx).
- Informace o vytváření a konfiguraci ukládacích složek najdete v tématu [Nastavení odkládacích složek](https://msdn.microsoft.com/library/bb778394.aspx).

## <a name="install-required-products-and-components"></a>Nainstalovat požadované produkty a součásti

Chcete-li serveru sestavení povolit sestavení vašich řešení, je nutné nainstalovat jakékoli produkty, komponenty nebo sestavení, které vaše řešení vyžaduje. Před instalací jakékoli komponenty webové platformy byste měli nainstalovat Visual Studio 2010 (libovolná verze) na server sestavení. Tím se zajistí, aby služba sestavení měla k dispozici cílové soubory služby Core Microsoft Build Engine (MSBuild) a cílové soubory kanálu pro publikování na webu (WPP). Instalační program sady Visual Studio by měl také nainstalovat Nasazení webu, které budete potřebovat, pokud plánujete nasadit webové balíčky jako součást procesu sestavení.

Nejlepším způsobem, jak nainstalovat společné součásti webové platformy, je použití [instalačního programu webové platformy](https://go.microsoft.com/?linkid=9805118). Tím zajistíte, že instalujete nejnovější verzi každého produktu, a také automaticky zjistíte a nainstalujete všechny požadované součásti pro každý produkt. V případě řešení [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) byste měli k instalaci těchto produktů a součástí použít instalační program webové platformy:

- **.NET Framework 4,0**. To je nutné ke spuštění aplikací, které byly vytvořeny v této verzi .NET Framework.
- **Nástroj pro nasazení webu 2,1 nebo novější**. Tím se na váš server nainstaluje Nasazení webu (a jeho základní spustitelný soubor MSDeploy. exe). V rámci tohoto procesu nainstaluje a spustí službu Web Deployment Agent. Tato služba umožňuje nasadit webové balíčky ze vzdáleného počítače.
- **ASP.NET MVC 3**. Tím se nainstaluje sestavení, která potřebujete ke spouštění aplikací ASP.NET MVC 3.

**Instalace požadovaných produktů a součástí**

1. Nainstalujte Visual Studio 2010. Po zobrazení výzvy k výběru funkcí k instalaci byste měli zahrnout:

    1. Všechny programovací jazyky, které potřebujete zkompilovat.
    2. Visual Web Developer. Tím se zajistí, že cíle WPP budou přidány do serveru sestavení.

        ![](configuring-a-tfs-build-server-for-web-deployment/_static/image1.png)
2. Po dokončení instalace sady Visual Studio 2010 Stáhněte a nainstalujte [sadu Visual studio 2010 Service Pack 1](https://go.microsoft.com/?linkid=9805133) (Pokud ještě není součástí instalačního média).

    > [!NOTE]
    > Sada Visual Studio 2010 Service Pack 1 řeší chybu, která může nástroji MSBuild zabránit ve vyhledání spustitelného souboru MSDeploy.
3. Stáhněte a spusťte [instalační program webové platformy](https://go.microsoft.com/?linkid=9805118).
4. V horní části okna **Instalace webové platformy 3,0** klikněte na **produkty**.
5. Na levé straně okna klikněte v navigačním podokně na možnost **architektury**.
6. Pokud .NET Framework ještě není nainstalovaná, na řádku **Microsoft .NET Framework 4** klikněte na **Přidat**.

    > [!NOTE]
    > Je možné, že jste už nainstalovali .NET Framework 4,0 prostřednictvím web Windows Update. Pokud je produkt nebo součást již nainstalována, instalační program webové platformy tuto skutečnost indikuje tak, že nahrazuje tlačítko **Přidat** s textem, který je **nainstalován**.

    ![](configuring-a-tfs-build-server-for-web-deployment/_static/image2.png)
7. V řádku **ASP.NET MVC 3 (Visual Studio 2010)** klikněte na **Přidat**.
8. V navigačním podokně klikněte na možnost **Server**.
9. V řádku **Nástroje pro nasazení webu 2,1** klikněte na **Přidat**.
10. Klikněte na **Nainstalovat**. Instalační program webové platformy zobrazí seznam produktů&#x2014;spolu s případnými přidruženými závislostmi&#x2014;, které se mají nainstalovat, a zobrazí výzvu k přijetí těchto licenčních podmínek.
11. Přečtěte si licenční podmínky a pokud souhlasíte s podmínkami **, klikněte na Souhlasím.**
12. Po dokončení instalace klikněte na **Dokončit**a potom zavřete okno **instalace webové platformy 3,0** .

> [!NOTE]
> Pokud proces nasazení zahrnuje použití nástrojů, jako je VSDBCMD. exe nebo SQLCMD. exe, musíte zajistit, aby byly tyto nástroje nainstalovány na serveru sestavení. VSDBCMD. exe je nástroj sady Visual Studio, který je obvykle přidán na server při instalaci serveru Team Foundation Build. SQLCMD. exe je SQL Server nástroj. Samostatnou verzi nástroje SQLCMD. exe si můžete stáhnout ze stránky [Microsoft SQL Server 2008 R2 Feature Pack](https://go.microsoft.com/?linkid=9805134) .

## <a name="conclusion"></a>Závěr

V tomto okamžiku je server sestavení připravený začít sestavovat a nasazovat projekty webových aplikací. V dalším tématu [Vytvoření definice sestavení, která podporuje nasazení](creating-a-build-definition-that-supports-deployment.md), popisuje, jak vytvořit a nakonfigurovat definici sestavení, která určuje, kdy a jak mají být vaše projekty sestaveny a nasazeny.

## <a name="further-reading"></a>Další čtení

Obecnější pokyny pro práci s týmovým sestavením naleznete v tématu [Správa Team Foundation Build](https://msdn.microsoft.com/library/ms252495.aspx).

> [!div class="step-by-step"]
> [Předchozí](adding-content-to-source-control.md)
> [Další](creating-a-build-definition-that-supports-deployment.md)

---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
title: Vyloučení souborů a složek z nasazení | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak můžete vyloučit soubory a složky z balíčku pro nasazení webu při vytváření a zabalení projektu webové aplikace.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f4cc2d40-6a78-429b-b06f-07d000d4caad
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment
msc.type: authoredcontent
ms.openlocfilehash: a262ce43d7199fb1015d54d0b7c213857c360946
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544973"
---
# <a name="excluding-files-and-folders-from-deployment"></a>Vyloučení souborů a složek z nasazení

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak můžete vyloučit soubory a složky z balíčku pro nasazení webu při vytváření a zabalení projektu webové aplikace.

Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého [řešení](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.

Metoda nasazení na srdce těchto kurzů je založena na způsobu rozdělení souborů projektu popsaných v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md), ve kterém je proces sestavení řízen dvěma soubory&#x2014;projektu jeden, který obsahuje pokyny pro sestavení, které platí pro každé cílové prostředí, a jedno obsahující nastavení sestavení a nasazení specifické pro konkrétní prostředí. V době sestavení je soubor projektu specifický pro prostředí sloučen do souboru projektu prostředí – nezávislá a vytvoří kompletní sadu instrukcí pro sestavení.

## <a name="overview"></a>Přehled

Při sestavování projektu webové aplikace v aplikaci Visual Studio 2010 vám kanál publikování na webu (WPP) umožňuje tento proces sestavení roztáhnout do balíčku zkompilované webové aplikace do nasazeného webového balíčku. Pak můžete použít Nasazení webu Nástroj pro nasazení webu Internetová informační služba (IIS) k nasazení tohoto webového balíčku na vzdálený webový server služby IIS nebo ručně importovat webový balíček pomocí Správce služby IIS. Tento proces vytváření balíčků je vysvětlen v tématu [sestavování a balení projektů webových aplikací](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).

Jak tedy můžete řídit, co bude součástí vašeho webového balíčku? Nastavení projektu v aplikaci Visual Studio, prostřednictvím podkladového souboru projektu, poskytují dostatečné řízení pro mnoho scénářů. V některých případech však můžete chtít přizpůsobit obsah webového balíčku konkrétním cílovým prostředím. Například můžete chtít zahrnout složku pro soubory protokolu, když nasadíte aplikaci do testovacího prostředí, ale vyloučíte složku při nasazení aplikace do pracovního nebo produkčního prostředí. V tomto tématu se dozvíte, jak to udělat.

## <a name="what-gets-included-by-default"></a>Co je ve výchozím nastavení zahrnuté?

Při konfiguraci vlastností projektu webové aplikace v aplikaci Visual Studio se v seznamu **položky k nasazení** na webové stránce **Balení/publikování** dá určit, co chcete zahrnout do balíčku pro nasazení webu. Ve výchozím nastavení je tato hodnota nastavena na **pouze soubory potřebné ke spuštění této aplikace**.

![](excluding-files-and-folders-from-deployment/_static/image1.png)

Když zvolíte **pouze soubory potřebné ke spuštění této aplikace**, WPP se pokusí určit, které soubory mají být přidány do webového balíčku. To zahrnuje:

- Všechny výstupy sestavení pro projekt.
- Všechny soubory označené pomocí akce sestavení **obsahu**.

> [!NOTE]
> Logika, která určuje, které soubory se mají zahrnout, je obsažená v tomto souboru:   
> *%PROGRAMFILES%\MSBuild\Microsoft\VisualStudio\v10.0\Web\ Microsoft. Web. Publishing. OnlyFilesToRunTheApp. targets*

## <a name="excluding-specific-files-and-folders"></a>Vyloučení konkrétních souborů a složek

V některých případech budete chtít podrobnější kontrolu nad tím, které soubory a složky budou nasazeny. Pokud víte, které soubory chcete vyloučit před časem, a vyloučení platí pro všechna cílová prostředí, můžete jednoduše nastavit **akci sestavení** každého souboru na **none**.

**Vyloučení určitých souborů z nasazení**

1. V okně **Průzkumník řešení** klikněte pravým tlačítkem na soubor a pak klikněte na **vlastnosti**.
2. V okně **vlastnosti** vyberte na řádku **Akce sestavení** možnost **žádný**.

Tento přístup ale není vždycky pohodlný. Například můžete chtít změnit, které soubory a složky jsou zahrnuty v závislosti na cílovém prostředí a mimo aplikaci Visual Studio. Například v ukázkovém řešení Správce kontaktů si prohlédněte obsah projektu ContactManager. Mvc:

![](excluding-files-and-folders-from-deployment/_static/image2.png)

- Interní složka obsahuje některé skripty SQL, které vývojář používá k vytváření, vyřazení a naplnění místních databází pro účely vývoje. Žádná z těchto složek by se neměla nasadit do pracovního nebo produkčního prostředí.
- Složka skripty obsahuje několik souborů JavaScriptu. Mnoho těchto souborů je součástí čistě pro podporu ladění nebo poskytování IntelliSense v aplikaci Visual Studio. Některé z těchto souborů by se neměly nasazovat do pracovních nebo produkčních prostředí. Můžete je ale chtít nasadit do testovacího prostředí pro vývojáře, abyste usnadnili řešení potíží.

I když byste mohli manipulovat se soubory projektu pro vyloučení konkrétních souborů a složek, existuje jednodušší způsob. Služba WPP zahrnuje mechanismus pro vyloučení souborů a složek sestavením seznamů položek s názvem **ExcludeFromPackageFolders** a **ExcludeFromPackageFiles**. Tento mechanismus můžete roztáhnout přidáním vlastních položek do těchto seznamů. K tomu je potřeba provést tyto kroky vysoké úrovně:

1. Vytvořte vlastní soubor projektu nazvaný *[název projektu]. WPP. targets* ve stejné složce jako soubor projektu.

    > [!NOTE]
    > Soubor *. WPP. targets* musí být ve stejné složce jako soubor&#x2014;projektu webové aplikace, například *ContactManager. Mvc. csproj*&#x2014;, nikoli ve stejné složce jako jakékoli vlastní soubory projektu, které slouží k řízení procesu sestavení a nasazení.
2. V souboru *. WPP. targets* přidejte prvek **Item** .
3. V elementu **Item** přidejte položky **ExcludeFromPackageFolders** a **ExcludeFromPackageFiles** , které vyloučí konkrétní soubory a složky podle potřeby.

Toto je základní struktura tohoto souboru *. WPP. targets* :

[!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample1.xml)]

Všimněte si, že každá položka obsahuje element metadat položky s názvem **FromTarget**. Toto je volitelná hodnota, která nemá vliv na proces sestavení; slouží pouze k označení, proč byly vynechány konkrétní soubory nebo složky, pokud někdo kontroluje protokoly sestavení.

## <a name="excluding-files-and-folders-from-a-web-package"></a>Vyloučení souborů a složek z webového balíčku

Následující postup ukazuje, jak přidat soubor *. WPP. targets* do projektu webové aplikace a jak použít soubor k vyloučení určitých souborů a složek z webového balíčku při sestavování projektu.

**Vyloučení souborů a složek z balíčku pro nasazení webu**

1. Otevřete řešení v aplikaci Visual Studio 2010.
2. V okně **Průzkumník řešení** klikněte pravým tlačítkem myši na uzel projektu webové aplikace (například **ContactManager. Mvc**), přejděte na **Přidat**a klikněte na **Nová položka**.
3. V dialogovém okně **Přidat novou položku** vyberte šablonu **souboru XML** .
4. Do pole **název** zadejte *[název projektu] * * *. WPP. targets** (například **ContactManager. Mvc. WPP. targets**) a pak klikněte na **Přidat**.

    ![](excluding-files-and-folders-from-deployment/_static/image3.png)

    > [!NOTE]
    > Pokud přidáte novou položku do kořenového uzlu projektu, je soubor vytvořen ve stejné složce jako soubor projektu. To můžete ověřit tak, že otevřete složku v Průzkumníku Windows.
5. Do souboru přidejte prvek **projektu** a prvek skupiny **položek** :

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample2.xml)]
6. Chcete-li vyloučit složky z webového balíčku, přidejte element **ExcludeFromPackageFolders** do elementu **Item** :

   1. V atributu **include** zadejte středníkem oddělený seznam složek, které chcete vyloučit.
   2. V elementu metadat **FromTarget** zadejte smysluplnou hodnotu, která určuje, proč se složky vylučují, jako název souboru *. WPP. targets* .

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample3.xml)]
7. Chcete-li vyloučit soubory z webového balíčku, přidejte element **ExcludeFromPackageFiles** do elementu **Item** :

   1. V atributu **include** zadejte středníkem oddělený seznam souborů, které chcete vyloučit.
   2. V elementu metadat **FromTarget** zadejte smysluplnou hodnotu, která určuje, proč jsou soubory vyloučeny, jako název souboru *. WPP. targets* .

      [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample4.xml)]
8. Soubor *[název projektu]. WPP. targets* by teď měl vypadat takto:

    [!code-xml[Main](excluding-files-and-folders-from-deployment/samples/sample5.xml)]
9. Uložte a zavřete soubor *[název projektu]. WPP. targets* .

Při příštím sestavení a zabalení projektu webové aplikace bude modul WPP automaticky detekovat soubor *. WPP. targets* . Všechny zadané soubory a složky nebudou součástí webového balíčku.

## <a name="conclusion"></a>Závěr

Toto téma popisuje, jak vyloučit konkrétní soubory a složky při vytváření webového balíčku vytvořením vlastního souboru *. WPP. targets* ve stejné složce jako soubor projektu webové aplikace.

## <a name="further-reading"></a>Další čtení

Další informace o použití vlastních souborů projektu Microsoft Build Engine (MSBuild) k řízení procesu nasazení naleznete v tématu [porozumění souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md) a [porozumění procesu sestavení](../web-deployment-in-the-enterprise/understanding-the-build-process.md). Další informace o procesu balení a nasazení najdete v tématu [sestavování a balení projektů webových aplikací](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md), [Konfigurace parametrů pro nasazení webového balíčku](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)a [nasazení webových balíčků](../web-deployment-in-the-enterprise/deploying-web-packages.md).

> [!div class="step-by-step"]
> [Předchozí](deploying-membership-databases-to-enterprise-environments.md)
> [Další](taking-web-applications-offline-with-web-deploy.md)

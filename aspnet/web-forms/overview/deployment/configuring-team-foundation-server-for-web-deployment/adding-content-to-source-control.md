---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
title: Přidávání obsahu do správy zdrojových kódů | Microsoft Docs
author: jrjlee
description: Toto téma vysvětluje, jak přidat obsah do správy zdrojového kódu v Team Foundation Server (TFS) 2010. Popisuje, jak přidat řešení a projekty do týmového projektu...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 86c14aab-c2dd-4f73-b40c-c6d52fa44950
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control
msc.type: authoredcontent
ms.openlocfilehash: 16073dd2fb0ea1cc4ddbc94c843181933dc174c1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634461"
---
# <a name="adding-content-to-source-control"></a>Přidání obsahu do správy zdrojového kódu

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma vysvětluje, jak přidat obsah do správy zdrojového kódu v Team Foundation Server (TFS) 2010. Popisuje, jak přidat řešení a projekty do týmového projektu v TFS a vysvětluje, jak přidat externí závislosti, jako jsou architektury nebo sestavení, do správy zdrojového kódu.

Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého [řešení](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.

## <a name="task-overview"></a>Přehled úlohy

Ve většině případů by měl být každý člen vývojářského týmu schopný přidávat obsah do správy zdrojového kódu. Chcete-li přidat řešení do správy zdrojového kódu v TFS, je nutné provést tyto kroky vysoké úrovně:

- Připojte se k týmovému projektu.
- Namapujte strukturu složek týmového projektu na serveru na strukturu složek na místním počítači.
- Přidejte řešení a jeho obsah do správy zdrojových kódů.
- Přidejte všechny externí závislosti do správy zdrojového kódu.

V tomto tématu se dozvíte, jak provádět tyto postupy.

V úlohách a návodech v tomto tématu se předpokládá, že jste již vytvořili nový týmový projekt TFS pro správu obsahu. Další informace o vytvoření nového týmového projektu naleznete v tématu [vytvoření týmového projektu v serveru TFS](creating-a-team-project-in-tfs.md).

### <a name="who-performs-these-procedures"></a>Kdo provádí tyto postupy?

Ve většině případů by měl být každý člen vývojářského týmu schopný přidávat a upravovat obsah v rámci konkrétních týmových projektů.

## <a name="connect-to-a-team-project-and-create-a-folder-mapping"></a>Připojit se k týmovému projektu a vytvořit mapování složky

Před přidáním jakéhokoli obsahu do správy zdrojového kódu se musíte připojit k týmovému projektu a vytvořit mapování mezi strukturou složek na serveru a systémem souborů na místním počítači.

**Připojení k týmovému projektu a mapování místní cesty**

1. Na pracovní stanici pro vývojáře otevřete Visual Studio 2010.
2. V aplikaci Visual Studio v nabídce **tým** klikněte na **připojit k Team Foundation Server**.

    > [!NOTE]
    > Pokud jste již nakonfigurovali připojení k serveru TFS, můžete vynechat kroky 3-6.
3. V dialogovém okně **připojení k týmovému projektu** klikněte na možnost **servery**.
4. V dialogovém okně **Přidat/odebrat Team Foundation Server** klikněte na **Přidat**.
5. V dialogovém okně **přidat Team Foundation Server** zadejte podrobnosti instance TFS a pak klikněte na tlačítko **OK**.

    ![](adding-content-to-source-control/_static/image1.png)
6. V dialogovém okně **Přidat/odebrat Team Foundation Server** klikněte na **Zavřít**.
7. V dialogovém okně **připojit k týmovému projektu** vyberte instanci TFS, ke které se chcete připojit, vyberte kolekci týmového projektu, vyberte týmový projekt, do kterého chcete přidat, a potom klikněte na tlačítko **připojit**.

    ![](adding-content-to-source-control/_static/image2.png)
8. V okně **Team Explorer** rozbalte svůj týmový projekt a potom poklikejte na **Správa zdrojového kódu**.

    ![](adding-content-to-source-control/_static/image3.png)
9. Na kartě **Průzkumník správy zdrojových souborů** klikněte na **Nenamapováno**.

    ![](adding-content-to-source-control/_static/image4.png)
10. V dialogovém okně **Mapa** v poli **místní složka** vyhledejte (nebo vytvořte) místní složku, která bude sloužit jako kořenová složka pro týmový projekt, a pak klikněte na tlačítko **Mapa**.

    ![](adding-content-to-source-control/_static/image5.png)
11. Až budete vyzváni ke stažení zdrojových souborů, klikněte na **Ano**.

    ![](adding-content-to-source-control/_static/image6.png)

V tomto okamžiku jste namapovali složku na straně serveru pro týmový projekt do místní složky na pracovní stanici pro vývojáře. Stáhli jste také veškerý existující obsah z týmového projektu do vaší místní struktury složek. Nyní můžete začít přidávat vlastní obsah do správy zdrojového kódu.

## <a name="add-projects-and-solutions-to-source-control"></a>Přidat projekty a řešení do správy zdrojového kódu

Chcete-li přidat projekty a řešení do správy zdrojového kódu, je nutné je nejprve přesunout do mapované složky pro týmový projekt na místním počítači. Potom můžete obsah vrátit se změnami a synchronizovat vaše dodatky se serverem.

**Přidání projektů do správy zdrojových kódů**

1. Na pracovní stanici pro vývojáře přesuňte své projekty a řešení do vhodného umístění v rámci struktury mapované složky pro týmový projekt.

    > [!NOTE]
    > Mnoho organizací bude mít upřednostňovaný přístup k tomu, jak by měly být projekty a řešení uspořádány ve správě zdrojového kódu. Pokyny k strukturování složek naleznete v tématu [How to: Structure Your Source Control Folders in Team Foundation Server](https://msdn.microsoft.com/library/bb668992.aspx).
2. Otevřete řešení v aplikaci Visual Studio 2010.
3. V okně **Průzkumník řešení** klikněte pravým tlačítkem na řešení a potom klikněte na **Přidat řešení do správy zdrojového kódu**.

    ![](adding-content-to-source-control/_static/image7.png)

    > [!NOTE]
    > V některých případech, v závislosti na tom, jak vaše organizace chce strukturovat obsah v TFS, možná budete muset přidat projekty do správy zdrojového kódu jednotlivě a poskytnout tak přesnější kontrolu nad tím, jak je zdrojový kód uspořádán.
4. Ověřte, zda se na kartě **Průzkumník správy zdrojových souborů** zobrazuje obsah, který jste přidali v rámci struktury serverové složky pro týmový projekt.

    ![](adding-content-to-source-control/_static/image8.png)

    > [!NOTE]
    > Karta **Průzkumník správy zdrojových souborů** zobrazuje obsah bez dalšího dotazování, protože jste své řešení přidali do mapované složky v místním systému souborů. Pokud bylo vaše řešení v nemapovaném umístění, zobrazí se výzva k zadání umístění složky v TFS i v místním systému souborů.
5. Na kartě **Průzkumník správy zdrojových souborů** v podokně **složky** klikněte pravým tlačítkem myši na týmový projekt (například **ContactManager**) a potom klikněte na možnost **vrátit se změnami do seznamu probíhající změny**.
6. V dialogovém okně **vrátit se změnami – zdrojové soubory** zadejte komentář a potom klikněte na možnost **vrátit se**změnami.

    ![](adding-content-to-source-control/_static/image9.png)

V tomto okamžiku jste přidali řešení do správy zdrojového kódu v TFS.

## <a name="add-external-dependencies-to-source-control"></a>Přidat externí závislosti do správy zdrojového kódu

Když přidáte projekt nebo řešení do správy zdrojového kódu, budou přidány také všechny soubory a složky v rámci projektu nebo řešení. V mnoha případech se ale projekty a řešení také spoléhají na externí závislosti, jako jsou místní sestavení, aby fungovaly správně. Je nutné přidat takové prostředky do správy zdrojových kódů, aby mohl týmový Build i ostatní členové týmu vývojáře sestavit kód úspěšně.

Například struktura složky pro ukázkové řešení Contact Manager obsahuje složku s názvem Packages. Obsahuje sestavení a různé podpůrné prostředky pro ADO.NET Entity Framework 4,1. Složka Packages není součástí řešení Správce kontaktů, ale řešení se bez něj nebude sestavovat úspěšně. Chcete-li povolit týmové sestavení pro sestavení řešení, je nutné přidat složku balíčky do správy zdrojového kódu.

> [!NOTE]
> Zahrnutí složky balíčků je typické, co se stane, když do svého řešení přidáte Entity Framework nebo podobné prostředky pomocí rozšíření NuGet pro Visual Studio 2010.

**Přidání jiného než projektového obsahu do správy zdrojů**

1. Ujistěte se, že položky, které chcete přidat (například složka balíčky), jsou v příslušném umístění v rámci mapované složky v místním systému souborů.
2. V aplikaci Visual Studio 2010 v okně **Team Explorer** rozbalte svůj týmový projekt a dvakrát klikněte na položku **Správa zdrojového kódu**.

    ![](adding-content-to-source-control/_static/image10.png)
3. Na kartě **Průzkumník správy zdrojových souborů** v podokně **složky** vyberte složku obsahující položku nebo položky, které chcete přidat.
4. Klikněte na tlačítko **Přidat položky do složky** .

    ![](adding-content-to-source-control/_static/image11.png)
5. V dialogovém okně **Přidat do správy zdrojového kódu** vyberte složku nebo položky, které chcete přidat, a poté klikněte na tlačítko **Další**.

    ![](adding-content-to-source-control/_static/image12.png)
6. Na kartě **vyloučené položky** vyberte všechny požadované položky, které byly automaticky vyloučeny (například sestavení), a potom klikněte na položku **Zahrnout položky (y)** .

    ![](adding-content-to-source-control/_static/image13.png)
7. Na kartě **položky, které chcete přidat** ověřte, zda jsou uvedeny všechny soubory, které chcete zahrnout, a poté klikněte na tlačítko **Dokončit**.

    ![](adding-content-to-source-control/_static/image14.png)
8. V okně **Průzkumník správy zdrojových souborů** klikněte na tlačítko **vrátit se změnami** .

    ![](adding-content-to-source-control/_static/image15.png)
9. V dialogovém okně **vrátit se změnami – zdrojové soubory** zadejte komentář a potom klikněte na možnost **vrátit se**změnami.

V tuto chvíli jste přidali externí závislosti pro vaše řešení do správy zdrojového kódu.

## <a name="conclusion"></a>Závěr

Toto téma popisuje, jak se připojit k týmovému projektu, mapovat strukturu složek a přidat obsah do správy zdrojového kódu. Další informace o tom, jak pracovat s položkami v rámci správy zdrojového kódu, naleznete v tématu [using a Control Version](https://msdn.microsoft.com/library/ms181368.aspx).

V dalším tématu [Konfigurace serveru TFS Build pro nasazení webu](configuring-a-tfs-build-server-for-web-deployment.md), popisuje, jak připravit server TFS Team Build pro sestavení a nasazení vašeho řešení.

## <a name="further-reading"></a>Další čtení

Další informace o práci se správou zdrojového kódu v TFS najdete v tématu [použití správy verzí](https://msdn.microsoft.com/library/ms181368.aspx).

> [!div class="step-by-step"]
> [Předchozí](creating-a-team-project-in-tfs.md)
> [Další](configuring-a-tfs-build-server-for-web-deployment.md)

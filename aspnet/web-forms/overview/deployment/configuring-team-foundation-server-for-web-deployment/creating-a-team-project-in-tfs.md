---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
title: Vytvoření týmového projektu v TFS | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak vytvořit nový týmový projekt v Team Foundation Server (TFS) 2010.
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b28d3e2d-0bb4-4e29-a780-af810b964722
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs
msc.type: authoredcontent
ms.openlocfilehash: d12e0636ce3b6239d125305db4354278f9f24960
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639655"
---
# <a name="creating-a-team-project-in-tfs"></a>Vytváření týmových projektů v TFS

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak vytvořit nový týmový projekt v Team Foundation Server (TFS) 2010.

Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého [řešení](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.

## <a name="task-overview"></a>Přehled úlohy

Chcete-li zřídit a použít nový týmový projekt na serveru TFS, je nutné provést tyto kroky vysoké úrovně:

- Udělte oprávnění uživateli, který vytvoří nový týmový projekt.
- Vytvořte týmový projekt.
- Udělte oprávnění členům týmu, kteří budou pracovat na projektu.
- Vrátit se změnami obsah.

V tomto tématu se dozvíte, jak provádět tyto postupy, a identifikuje uživatele a role úloh, které jsou pravděpodobně zodpovědné za jednotlivé postupy. Uvědomte si, že v závislosti na struktuře vaší organizace může být každý z těchto úkolů zodpovědností jiné osoby.

V úlohách a návodech v tomto tématu se předpokládá, že jste nainstalovali a nakonfigurovali TFS a že jste jako součást procesu konfigurace vytvořili kolekci týmového projektu. Další informace o těchto předpokladech a obecnější informace o tomto scénáři najdete v tématu [Konfigurace serveru TFS Build pro nasazení webu](configuring-a-tfs-build-server-for-web-deployment.md).

## <a name="grant-permissions-to-the-team-project-creator"></a>Udělení oprávnění tvůrci týmového projektu

Pro vytvoření nového týmového projektu budete potřebovat tato oprávnění:

- Musíte mít oprávnění **vytvořit nové projekty** v aplikační vrstvě TFS. Toto oprávnění obvykle udělujete přidáním uživatelů do skupiny TFS **Správci kolekce projektů** . Toto oprávnění zahrnuje i globální skupina **Správci Team Foundation** .
- Musíte mít oprávnění k vytváření nových týmových webů v rámci kolekce webů služby SharePoint, která odpovídá kolekci TFS Team Project Collection. Toto oprávnění obvykle udělujete tak, že přidáte uživatele do skupiny služby SharePoint s právy **Úplné řízení** v kolekci webů služby SharePoint.
- Pokud používáte funkce SQL Server Reporting Services, musíte být členem role **Správce obsahu Team Foundation** ve službě Reporting Services.

### <a name="who-performs-these-procedures"></a>Kdo provádí tyto postupy?

Obvykle tyto postupy provádí osoba nebo skupina, která spravuje nasazení TFS.

Vzhledem k tomu, že se jedná o vysoce privilegovanou sadu oprávnění, jsou nové týmové projekty obvykle vytvářeny malou podmnožinou uživatelů s zodpovědností za správu nasazení serveru TFS. Vývojářům většinou nebudou udělena oprávnění potřebná k vytváření nových týmových projektů.

### <a name="grant-permissions-in-tfs"></a>Udělení oprávnění v TFS

Chcete-li uživateli povolit vytváření nových týmových projektů, je prvním úkolem vysoké úrovně přidání uživatele do skupiny **Správci kolekcí projektů** pro kolekci týmového projektu.

**Přidání uživatele do skupiny Správci kolekcí projektů**

1. Na serveru TFS v nabídce **Start** přejděte na **všechny programy**, klikněte na **Microsoft Team Foundation Server 2010**a potom klikněte na **Konzola pro správu serveru Team Foundation**.
2. Ve stromovém zobrazení rozbalte položku **aplikační vrstva**a potom klikněte na položku **kolekce týmových projektů**.

    ![](creating-a-team-project-in-tfs/_static/image1.png)
3. V podokně **kolekce týmových projektů** vyberte kolekci týmového projektu, kterou chcete spravovat.

    ![](creating-a-team-project-in-tfs/_static/image2.png)
4. Na kartě **Obecné** klikněte na **členství ve skupině**.

    ![](creating-a-team-project-in-tfs/_static/image3.png)
5. V dialogovém okně **globální skupiny** vyberte skupinu **Správci kolekce projektů** a potom klikněte na tlačítko **vlastnosti**.
6. V dialogovém okně **Vlastnosti skupiny Team Foundation Server** vyberte **uživatele nebo skupinu systému Windows**a potom klikněte na tlačítko **Přidat**.

    ![](creating-a-team-project-in-tfs/_static/image4.png)
7. V dialogovém okně **Vybrat uživatele, počítače nebo skupiny** zadejte uživatelské jméno uživatele, kterého chcete umožnit vytváření nových týmových projektů, klikněte na tlačítko **kontrolovat názvy**a pak klikněte na tlačítko **OK**.

    ![](creating-a-team-project-in-tfs/_static/image5.png)
8. V dialogovém okně **Vlastnosti skupiny Team Foundation Server** klikněte na tlačítko **OK**.
9. V dialogovém okně **globální skupiny** klikněte na **Zavřít**.

### <a name="grant-permissions-in-sharepoint-services"></a>Udělení oprávnění ve službě SharePoint Services

Dále musíte uživateli udělit oprávnění k vytváření nových týmových webů v kolekci webů služby SharePoint, která odpovídá vaší kolekci týmových projektů TFS.

**Udělení oprávnění k úplnému řízení pro kolekci webů služby SharePoint**

1. V Team Foundation Server Administration Console na stránce **kolekce týmových projektů** vyberte kolekci týmového projektu, kterou chcete spravovat.
2. Na kartě **sharepointový web** si poznamenejte hodnotu **aktuální výchozí umístění lokality** adresa URL.

    ![](creating-a-team-project-in-tfs/_static/image6.png)
3. Spusťte aplikaci Internet Explorer a pak použijte adresu URL, kterou jste si poznamenali v kroku 2.

    > [!NOTE]
    > Pokud nejste přihlášení k Windows jako uživatel, který kolekci týmových projektů vytvořil, budete se muset přihlásit k SharePointu jako tento uživatel, aby bylo možné pokračovat.
4. V nabídce **Akce webu** klikněte na položku **Nastavení webu**.

    ![](creating-a-team-project-in-tfs/_static/image7.png)
5. Na stránce **Nastavení webu** v části **Uživatelé a oprávnění**klikněte na **Uživatelé a skupiny**.
6. V levém navigačním panelu klikněte na **skupiny**.

    ![](creating-a-team-project-in-tfs/_static/image8.png)
7. Na stránce **lidé a skupiny: všechny skupiny** klikněte na **nastavit skupiny pro tento web**.

    ![](creating-a-team-project-in-tfs/_static/image9.png)

   > [!NOTE]
   > Může se zobrazit chyba <strong>HTTP 404 nenalezena</strong> z důvodu chyby kódování http s dvojitou přesností. Pokud k tomu dojde, nahraďte adresu URL tímto:   
   > `[site_collection_URL]/_layouts/permsetup.aspx` například:  
   > `http://tfs/sites/Fabrikam%20Web%20Projects/_layouts/permsetup.aspx` 
8. Na stránce **nastavit skupiny pro tuto lokalitu** přidejte uživatele, který bude vytvářet týmové projekty, do skupiny **vlastníci** a pak klikněte na tlačítko **OK**.

    ![](creating-a-team-project-in-tfs/_static/image10.png)

Další informace o tom, jak povolit uživatelům vytvářet nové týmové projekty v rámci kolekce týmového projektu, naleznete v tématu [Nastavení oprávnění správce pro kolekce týmových projektů](https://msdn.microsoft.com/library/dd547204.aspx).

## <a name="create-a-new-team-project-and-add-users"></a>Vytvoření nového týmového projektu a přidání uživatelů

Jakmile máte potřebná oprávnění, můžete použít okno **Team Explorer** v aplikaci Visual Studio 2010 k vytvoření nového týmového projektu. Tento přístup poskytuje průvodce, který shromažďuje všechny požadované informace a provádí nezbytné úlohy v TFS, SharePointu a SQL Server Reporting Services. Také budete muset udělit oprávnění k novému týmovému projektu členům vývojářského týmu, aby jim umožnili přidávat a upravovat obsah.

### <a name="who-performs-these-procedures"></a>Kdo provádí tyto postupy?

Tyto postupy obvykle provádí správce TFS nebo vedoucí vývojářského týmu.

### <a name="create-a-new-team-project"></a>Vytvořit nový týmový projekt

Další postup popisuje, jak vytvořit nový týmový projekt v TFS 2010.

**Vytvoření nového týmového projektu**

1. V nabídce **Start** přejděte na **všechny programy**, klikněte na **Microsoft Visual Studio 2010**, klikněte pravým tlačítkem na **Microsoft Visual Studio 2010**a pak klikněte na **Spustit jako správce**.

    > [!NOTE]
    > Pokud Visual Studio 2010 nespouštíte jako správce, Průvodce novým týmovým projektem se v posledním kroku nezdařil.
2. Pokud se zobrazí dialogové okno **řízení uživatelských účtů** , klikněte na tlačítko **Ano**.
3. V aplikaci Visual Studio v nabídce **tým** klikněte na **připojit k Team Foundation Server**.

    > [!NOTE]
    > Pokud jste již nakonfigurovali připojení k serveru TFS, můžete vynechat kroky 4-7.
4. V dialogovém okně **připojení k týmovému projektu** klikněte na možnost **servery**.
5. V dialogovém okně **Přidat/odebrat Team Foundation Server** klikněte na **Přidat**.
6. V dialogovém okně **přidat Team Foundation Server** zadejte podrobnosti instance TFS a pak klikněte na tlačítko **OK**.

    ![](creating-a-team-project-in-tfs/_static/image11.png)
7. V dialogovém okně **Přidat/odebrat Team Foundation Server** klikněte na **Zavřít**.
8. V dialogovém okně **připojit k týmovému projektu** vyberte instanci TFS, ke které se chcete připojit, vyberte kolekci týmového projektu, do které chcete přidat, a poté klikněte na tlačítko **připojit**.

    ![](creating-a-team-project-in-tfs/_static/image12.png)
9. V okně **Team Explorer** klikněte pravým tlačítkem na kolekci týmového projektu a pak klikněte na **nový týmový projekt**.

    ![](creating-a-team-project-in-tfs/_static/image13.png)
10. V dialogovém okně **nový týmový projekt** zadejte název a popis týmového projektu a poté klikněte na tlačítko **Další**.

    > [!NOTE]
    > Pokud váš týmový projekt obsahuje mezery, můžete se setkat s některými problémy při použití nástroje Internetová informační služba (IIS) web pro nasazení webu (Nasazení webu) k nasazení balíčků z výstupní cesty. Mezery v cestě můžou mít za následek mnohem obtížnější spuštění Nasazení webuch příkazů.

    ![](creating-a-team-project-in-tfs/_static/image14.png)
11. Na stránce **Vyberte šablonu procesu** vyberte šablonu procesu, kterou chcete použít ke správě procesu vývoje, a poté klikněte na tlačítko **Další**.

    > [!NOTE]
    > Další informace o šablonách procesů pro TFS naleznete v tématu [Process Templates and Tools](https://msdn.microsoft.com/vstudio/aa718795).
12. Na stránce **nastavení týmového webu** ponechte výchozí nastavení beze změny a potom klikněte na tlačítko **Další**.
13. Toto nastavení vytvoří nebo identifikuje týmový web služby SharePoint, který je spojen s týmovým projektem TFS. Váš vývojový tým může pomocí tohoto webu spravovat dokumentaci, zúčastnit se diskuzních vláken, vytvářet stránky wikiwebu a provádět různé další úkoly, které nesouvisí s kódem. Další informace najdete v tématu [interakce mezi produkty SharePoint a Team Foundation Server](https://msdn.microsoft.com/library/ms253177.aspx).
14. Na stránce **zadat nastavení správy zdrojů** ponechte výchozí nastavení beze změny a potom klikněte na tlačítko **Další**.
15. Toto nastavení identifikuje nebo vytvoří umístění v hierarchii složek TFS, které bude sloužit jako kořenová složka pro váš obsah.
16. Na stránce **Potvrdit nastavení týmového projektu** klikněte na **Dokončit**.
17. Po úspěšném vytvoření nového týmového projektu klikněte na stránce **vytvořený týmový projekt** na **Zavřít**.

### <a name="add-users-to-a-team-project"></a>Přidání uživatelů do týmového projektu

Teď, když jste vytvořili nový týmový projekt, můžete uživatelům udělit oprávnění k tomu, aby mohli začít přidávat a spolupracovat na obsahu.

**Přidání uživatelů do týmového projektu**

1. V aplikaci Visual Studio 2010 v okně **Team Explorer** klikněte pravým tlačítkem myši na týmový projekt, přejděte na položku **nastavení týmového projektu**a pak klikněte na položku **členství ve skupině**.

    ![](creating-a-team-project-in-tfs/_static/image15.png)
2. Chcete-li uživateli povolit přidávání, úpravy a odebírání kódu pod správou zdrojových kódů, je nutné jej přidat do skupiny **přispěvatelé** .
3. V dialogovém okně **skupiny projektu** vyberte skupinu **přispěvatelé** a potom klikněte na tlačítko **vlastnosti**.

    ![](creating-a-team-project-in-tfs/_static/image16.png)
4. V dialogovém okně **Vlastnosti skupiny Team Foundation Server** vyberte **uživatele nebo skupinu systému Windows**a potom klikněte na tlačítko **Přidat**.

    ![](creating-a-team-project-in-tfs/_static/image17.png)
5. V dialogovém okně **Vybrat uživatele, počítače nebo skupiny** zadejte uživatelské jméno uživatele, kterého chcete přidat do týmového projektu, klikněte na tlačítko **kontrolovat jména**a potom klikněte na tlačítko **OK**.

    ![](creating-a-team-project-in-tfs/_static/image18.png)
6. V dialogovém okně **Vlastnosti skupiny Team Foundation Server** klikněte na tlačítko **OK**.
7. V dialogovém okně **skupiny projektu** klikněte na tlačítko **Zavřít**.

## <a name="conclusion"></a>Závěr

V tuto chvíli je váš nový týmový projekt připravený k použití a váš vývojový tým může začít přidávat obsah a spolupracovat na procesu vývoje.

V dalším tématu [Přidání obsahu do správy zdrojových kódů](adding-content-to-source-control.md)popisuje, jak přidat obsah do správy zdrojových kódů.

## <a name="further-reading"></a>Další čtení

Širší pokyny týkající se vytváření týmových projektů v TFS naleznete v tématu [Create a Team Project](https://msdn.microsoft.com/library/ms181477(v=VS.100).aspx). Další informace o tom, jak povolit uživatelům vytvářet nové týmové projekty v rámci kolekce týmového projektu, naleznete v tématu [Nastavení oprávnění správce pro kolekce týmových projektů](https://msdn.microsoft.com/library/dd547204.aspx). Další informace o přidávání uživatelů do týmových projektů naleznete v tématu [Přidání uživatelů do týmových projektů](https://msdn.microsoft.com/library/bb558971.aspx).

> [!div class="step-by-step"]
> [Předchozí](configuring-team-foundation-server-for-web-deployment.md)
> [Další](adding-content-to-source-control.md)

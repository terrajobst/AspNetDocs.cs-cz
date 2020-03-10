---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
title: Nasazení konkrétního sestavení | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak nasadit webové balíčky a databázové skripty z konkrétního předchozího sestavení do nového cíle, jako je například pracovní nebo produkční plochy...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c979535f-48a3-4ec4-a633-a77889b86ddb
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
msc.type: authoredcontent
ms.openlocfilehash: 6bede6b36c24ade928ab052e14daec1e017bd0b2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639669"
---
# <a name="deploying-a-specific-build"></a>Nasazení konkrétního sestavení

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak nasadit webové balíčky a databázové skripty z konkrétního předchozího sestavení do nového cíle, jako je pracovní nebo produkční prostředí.

Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého [řešení](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.

Metoda nasazení na srdce těchto kurzů je založena na způsobu rozdělení souboru projektu popsaného v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md), ve kterém je proces sestavení a nasazení řízen dvěma soubory&#x2014;projektu, které obsahují pokyny pro sestavení, které platí pro každé cílové prostředí, a jedno obsahující nastavení sestavení a nasazení specifické pro konkrétní prostředí. V době sestavení je soubor projektu specifický pro prostředí sloučen do souboru projektu prostředí – nezávislá a vytvoří kompletní sadu instrukcí pro sestavení.

## <a name="task-overview"></a>Přehled úlohy

Do této chvíle se témata v tomto kurzu zaměřují na postupy vytváření, balení a nasazování webových aplikací a databází v rámci jednoho kroku nebo automatizovaného procesu. V některých běžných scénářích ale budete chtít vybrat prostředky, které nasazujete ze seznamu sestavení v ukládací složce. Jinými slovy, poslední sestavení nemusí být sestavení, které chcete nasadit.

Vezměte v úvahu scénář průběžné integrace (CI), který je popsaný v předchozím tématu, a vytvořte [definici sestavení, která podporuje nasazení](creating-a-build-definition-that-supports-deployment.md). Vytvořili jste definici sestavení v Team Foundation Server (TFS) 2010. Pokaždé, když vývojář kontroluje kód na TFS, týmový Build sestaví váš kód, vytvoří webové balíčky a databázové skripty jako součást procesu sestavení, spustí všechny testy jednotek a nasadí vaše prostředky do testovacího prostředí. V závislosti na zásadách uchovávání informací, které jste nakonfigurovali při vytváření definice sestavení, TFS zachovává určitý počet předchozích sestavení.

![](deploying-a-specific-build/_static/image1.png)

Nyní předpokládejme, že jste provedli ověřování a ověřovací testování proti jednomu z těchto sestavení v testovacím prostředí a jste připraveni nasadit aplikaci do přípravného prostředí. Mezitím si vývojáři mohli vrátit nový kód. Nechcete znovu sestavovat řešení a nasazovat ho do přípravného prostředí a nechcete nasadit poslední sestavení do přípravného prostředí. Místo toho chcete nasadit konkrétní sestavení, které jste ověřili a ověřili na testovacích serverech.

K tomu je nutné sdělit Microsoft Build Engine (MSBuild), kde najít webové balíčky a databázové skripty, které vygeneroval konkrétní sestavení.

## <a name="overriding-the-outputroot-property"></a>Přepsání vlastnosti OutputRoot

V [ukázkovém řešení](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)soubor *Publish. proj* deklaruje vlastnost s názvem **OutputRoot**. Jak název navrhuje, jedná se o kořenovou složku, která obsahuje všechno, co proces sestavení generuje. V souboru *Publish. proj* vidíte, že vlastnost **OutputRoot** odkazuje na kořenové umístění pro všechny prostředky nasazení.

> [!NOTE]
> **OutputRoot** je běžně používaný název vlastnosti. Soubory C# projektu Visual a Visual Basic také deklaruje tuto vlastnost pro uložení kořenového umístění pro všechny výstupy sestavení.

[!code-xml[Main](deploying-a-specific-build/samples/sample1.xml)]

Pokud chcete, aby soubor projektu nasadil webové balíčky a databázové skripty z jiného umístění&#x2014;, jako jsou výstupy předchozího sestavení&#x2014;TFS, stačí přepsat vlastnost **OutputRoot** . Měli byste nastavit hodnotu vlastnosti na příslušnou složku sestavení v Team Build serveru. Pokud jste spustili nástroj MSBuild z příkazového řádku, můžete zadat hodnotu parametru **OutputRoot** jako argument příkazového řádku:

[!code-console[Main](deploying-a-specific-build/samples/sample2.cmd)]

V praxi byste ale chtěli také přeskočit cíl&#x2014; **sestavení** , ale pokud neplánujete použít výstupy sestavení, nebudete moct sestavovat vaše řešení. To lze provést zadáním cíle, které chcete spustit z příkazového řádku:

[!code-console[Main](deploying-a-specific-build/samples/sample3.cmd)]

Ve většině případů však budete chtít sestavit logiku nasazení do definice sestavení TFS. To umožňuje uživatelům s touto **frontou** vytvářet oprávnění k aktivaci nasazení z jakékoli instalace sady Visual Studio s připojením k serveru TFS.

## <a name="creating-a-build-definition-to-deploy-specific-builds"></a>Vytvoření definice sestavení pro nasazení konkrétních sestavení

Další postup popisuje, jak vytvořit definici sestavení, která umožňuje uživatelům aktivovat nasazení do přípravného prostředí jediným příkazem.

V takovém případě nechcete, aby definice sestavení skutečně sestavila&#x2014;vše, co chcete, aby byla logika nasazení spuštěna ve vlastním souboru projektu. Soubor *Publish. proj* obsahuje podmíněnou logiku, která přeskočí cíl **sestavení** , pokud soubor běží v týmovém sestavení. Provede to vyhodnocením předdefinované vlastnosti **BuildingInTeamBuild** , která je automaticky nastavena na **hodnotu true** , pokud spustíte soubor projektu v týmovém sestavení. V důsledku toho můžete přeskočit proces sestavení a jednoduše spustit soubor projektu pro nasazení stávajícího sestavení.

**Vytvoření definice sestavení pro ruční spuštění nasazení**

1. V aplikaci Visual Studio 2010 v okně **Team Explorer** rozbalte uzel týmového projektu, klikněte pravým tlačítkem na položku **sestavení**a poté klikněte na možnost **Nová definice sestavení**.

    ![](deploying-a-specific-build/_static/image2.png)
2. Na kartě **Obecné** zadejte název definice sestavení (například **DeployToStaging**) a volitelný popis.
3. Na kartě **aktivační událost** vyberte **ručně – vrácení se změnami neaktivují nové sestavení**.
4. Na kartě **výchozí hodnoty sestavení** v poli **Kopírovat výstup sestavení do následující ukládací složky** zadejte cestu UNC (Universal Naming Convention) k odkládací složce (například **\\TFSBUILD\Drops**).

    ![](deploying-a-specific-build/_static/image3.png)
5. Na kartě **proces** v rozevíracím seznamu **soubor procesu sestavení** ponechte vybranou možnost **šabloně DefaultTemplate. XAML** . Toto je jedna z výchozích šablon procesu sestavení, které se přidají do všech nových týmových projektů.
6. V tabulce **parametrů procesu sestavení** klikněte na řádek **položky k sestavení** a potom klikněte na tlačítko se **třemi tečkami** .

    ![](deploying-a-specific-build/_static/image4.png)
7. V dialogovém okně **položky k sestavení** klikněte na tlačítko **Přidat**.
8. V rozevíracím seznamu **položky typu** vyberte možnost **soubory projektu MSBuild**.
9. Přejděte do umístění vlastního souboru projektu, pomocí kterého budete řídit proces nasazení, vyberte soubor a klikněte na tlačítko **OK**.

    ![](deploying-a-specific-build/_static/image5.png)
10. V dialogovém okně **položky k sestavení** klikněte na tlačítko **OK**.
11. V tabulce **parametrů procesu sestavení** rozbalte oddíl **Upřesnit** .
12. V řádku **argumenty MSBuild** zadejte umístění souboru projektu specifického pro prostředí a přidejte zástupný symbol pro umístění složky sestavení:

    [!code-console[Main](deploying-a-specific-build/samples/sample4.cmd)]

    ![](deploying-a-specific-build/_static/image6.png)

    > [!NOTE]
    > Je nutné přepsat hodnotu **OutputRoot** pokaždé, když sestavení zařadíte do fronty. Tento postup je popsaný v dalším postupu.
13. Klikněte na **Uložit**.

Při aktivaci sestavení je třeba aktualizovat vlastnost **OutputRoot** , aby odkazovala na sestavení, které chcete nasadit.

**Nasazení konkrétního sestavení z definice sestavení**

1. V okně **Team Explorer** klikněte pravým tlačítkem myši na definici sestavení a potom klikněte na příkaz **zařadit nové sestavení do fronty**.

    ![](deploying-a-specific-build/_static/image7.png)
2. V dialogovém okně **sestavení fronty** na kartě **parametry** rozbalte část **Upřesnit** .
3. V řádku **argumenty MSBuild** nahraďte hodnotu vlastnosti **OutputRoot** umístěním složky sestavení. Příklad:

    [!code-console[Main](deploying-a-specific-build/samples/sample5.cmd)]

    ![](deploying-a-specific-build/_static/image8.png)

    > [!NOTE]
    > Nezapomeňte na konec cesty do složky sestavení zahrnout koncové lomítko.
4. Klikněte na **fronta**.

Při zařazení sestavení do fronty bude soubor projektu nasazovat databázové skripty a webové balíčky ze ukládací složky sestavení, kterou jste zadali ve vlastnosti **OutputRoot** .

## <a name="conclusion"></a>Závěr

Toto téma popisuje, jak publikovat prostředky nasazení, jako jsou webové balíčky a databázové skripty, z konkrétního předchozího sestavení s použitím modelu nasazení rozděleného souboru projektu. Vysvětluje, jak přepsat vlastnost **OutputRoot** a jak začlenit logiku nasazení do definice sestavení TFS.

## <a name="further-reading"></a>Další čtení

Další informace o vytváření definic sestavení naleznete v tématu [Vytvoření základní definice sestavení](https://msdn.microsoft.com/library/ms181716.aspx) a [Definování procesu sestavení](https://msdn.microsoft.com/library/ms181715.aspx). Další informace o sestaveních služby Řízení front najdete v tématu [zařazení sestavení do fronty](https://msdn.microsoft.com/library/ms181722.aspx).

> [!div class="step-by-step"]
> [Předchozí](creating-a-build-definition-that-supports-deployment.md)
> [Další](configuring-permissions-for-team-build-deployment.md)

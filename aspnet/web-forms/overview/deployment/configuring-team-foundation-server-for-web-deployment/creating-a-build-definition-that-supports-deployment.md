---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
title: Vytvoření definice sestavení, která podporuje nasazení | Microsoft Docs
author: jrjlee
description: Chcete-li provést jakýkoli druh sestavení v Team Foundation Server (TFS) 2010, je nutné vytvořit definici sestavení v rámci týmového projektu. Toto téma des...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: fe47a018-f6d0-4979-80e7-5b1fa75a5865
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
msc.type: authoredcontent
ms.openlocfilehash: e11c91a824446572aaf0b3bc6954b9b8ffb4eaff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78603997"
---
# <a name="creating-a-build-definition-that-supports-deployment"></a>Vytvoření definice nasazení, která podporuje nasazení

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Chcete-li provést jakýkoli druh sestavení v Team Foundation Server (TFS) 2010, je nutné vytvořit definici sestavení v rámci týmového projektu. Toto téma popisuje, jak vytvořit novou definici sestavení v sadě TFS a jak řídit nasazení webu v rámci procesu sestavení v týmovém sestavení.

Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého [řešení](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.

Metoda nasazení na srdce těchto kurzů je založena na způsobu rozdělení souboru projektu popsaného v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md), ve kterém je proces sestavení a nasazení řízen dvěma soubory&#x2014;projektu, které obsahují pokyny pro sestavení, které platí pro každé cílové prostředí, a jedno obsahující nastavení sestavení a nasazení specifické pro konkrétní prostředí. V době sestavení je soubor projektu specifický pro prostředí sloučen do souboru projektu prostředí – nezávislá a vytvoří kompletní sadu instrukcí pro sestavení.

## <a name="task-overview"></a>Přehled úlohy

Definice sestavení je mechanismus, který určuje, jak a kdy dochází k sestavení pro týmové projekty v TFS. Každá definice sestavení Určuje:

- Věci, které chcete sestavit, například soubory řešení aplikace Visual Studio nebo vlastní soubory projektu Microsoft Build Engine (MSBuild).
- Kritéria, která určují, kdy by mělo dojít k sestavení, jako jsou ruční triggery, kontinuální integrace (CI) nebo ověřované vrácení se změnami.
- Umístění, do kterého má tým sestavení odeslat výstupy sestavení, včetně artefaktů nasazení, jako jsou webové balíčky a databázové skripty.
- Doba, po kterou mají být všechna sestavení uchována.
- Různé další parametry procesu sestavení.

> [!NOTE]
> Další informace o definicích sestavení naleznete v tématu [Definice procesu sestavení](https://msdn.microsoft.com/library/ms181715.aspx).

V tomto tématu se dozvíte, jak vytvořit definici sestavení, která používá CI, aby se spustilo sestavení při kontrole nového obsahu vývojářem. Pokud je sestavení úspěšné, služba sestavení spustí vlastní soubor projektu pro nasazení řešení do testovacího prostředí.

Při aktivaci sestavení je nutné provést tyto akce:

- Nejdřív by mělo sestavení týmu sestavit řešení. V rámci tohoto procesu vytvoří týmový Build kanál pro publikování webu (WPP), který vygeneruje balíčky pro nasazení webu pro každý projekt webové aplikace v řešení. V týmovém sestavení se také spustí všechny testy jednotek spojené s řešením.
- Pokud se sestavení řešení nepovede, týmový Build by neměl provádět žádnou další akci. Selhání testu jednotek by mělo být považováno za selhání sestavení.
- Pokud se sestavení řešení zdaří, týmový Build by měl spustit vlastní soubor projektu, který řídí nasazení řešení. V rámci tohoto procesu týmový Build vyvolá Nasazení webu Nástroj pro nasazení webu Internetová informační služba (IIS), který nainstaluje zabalené webové aplikace na cílové webové servery a vyvolá nástroj VSDBCMD. exe pro spuštění vytváření databáze. skripty na cílových databázových serverech.

To znázorňuje proces:

![](creating-a-build-definition-that-supports-deployment/_static/image1.png)

Ukázkové řešení [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) obsahuje vlastní soubor projektu MSBuild, *publikování. proj*, který můžete spustit z nástroje MSBuild nebo sestavení týmu. Jak je popsáno v tématu [Principy procesu sestavení](../web-deployment-in-the-enterprise/understanding-the-build-process.md), tento soubor projektu definuje logiku, která nasazuje vaše webové balíčky a databáze do cílového prostředí. Soubor obsahuje logiku, která vynechá proces sestavení a balení, pokud je spuštěn v rámci týmového sestavení, takže je potřeba spustit pouze úlohy nasazení. Důvodem je, že při automatizaci nasazení tímto způsobem obvykle budete chtít zajistit, aby se řešení úspěšně sestavilo a před zahájením procesu nasazení předá všechny testy jednotek.

V další části se dozvíte, jak implementovat tento proces vytvořením nové definice sestavení.

> [!NOTE]
> Tento postup&#x2014;, ve kterém jeden automatizovaný proces sestavuje, testuje a nasazuje řešení&#x2014;, je pravděpodobně nejvíce vhodný pro nasazení do testovacích prostředí. V případě pracovních a produkčních prostředí je mnohem více pravděpodobnější, že budete chtít nasadit obsah z předchozího sestavení, které jste již ověřili a ověřili v testovacím prostředí. Tento přístup je popsaný v dalším tématu [nasazení konkrétního sestavení](deploying-a-specific-build.md).

### <a name="who-performs-this-procedure"></a>Kdo tento postup provádí?

Tento postup obvykle provádí správce TFS. V některých případech může vedoucí týmu vývojářů převzít zodpovědnost za kolekci týmového projektu v TFS. Chcete-li vytvořit novou definici sestavení, musíte být členem skupiny **Správci sestavení kolekcí projektů** pro kolekci týmových projektů, která obsahuje vaše řešení.

## <a name="create-a-build-definition-for-ci-and-deployment"></a>Vytvoření definice sestavení pro CI a nasazení

Další postup popisuje, jak vytvořit definici sestavení, která spouští triggery CI. Pokud je sestavení úspěšné, řešení je nasazeno pomocí logiky ve vlastním souboru projektu MSBuild.

**Vytvoření definice sestavení pro CI a nasazení**

1. V aplikaci Visual Studio 2010 v okně **Team Explorer** rozbalte uzel týmového projektu, klikněte pravým tlačítkem na položku **sestavení**a poté klikněte na možnost **Nová definice sestavení**.

    ![](creating-a-build-definition-that-supports-deployment/_static/image2.png)
2. Na kartě **Obecné** zadejte název definice sestavení (například **DeployToTest**) a volitelný popis.
3. Na kartě **aktivační událost** vyberte kritéria, u kterých chcete aktivovat nové sestavení. Například pokud chcete sestavit řešení a nasadit do testovacího prostředí pokaždé, když vývojář zkontroluje nový kód, vyberte možnost **průběžná integrace**.
4. Na kartě **výchozí hodnoty sestavení** v poli **Kopírovat výstup sestavení do následující ukládací složky** zadejte cestu UNC (Universal Naming Convention) k odkládací složce (například **\\TFSBUILD\Drops**).

    ![](creating-a-build-definition-that-supports-deployment/_static/image3.png)

    > [!NOTE]
    > Toto odkládací umístění uchovává několik sestavení v závislosti na nakonfigurovaných zásadách uchovávání informací. Když chcete publikovat artefakty nasazení z konkrétního sestavení do pracovního nebo produkčního prostředí, najdete je tam.
5. Na kartě **proces** v rozevíracím seznamu **soubor procesu sestavení** ponechte vybranou možnost **šabloně DefaultTemplate. XAML** . Toto je jedna z výchozích šablon procesu sestavení, které se přidají do všech nových týmových projektů.
6. V tabulce **parametrů procesu sestavení** klikněte na řádek **položky k sestavení** a potom klikněte na tlačítko se **třemi tečkami** .

    ![](creating-a-build-definition-that-supports-deployment/_static/image4.png)
7. V dialogovém okně **položky k sestavení** klikněte na tlačítko **Přidat**.
8. Přejděte do umístění souboru řešení a klikněte na tlačítko **OK**.

    ![](creating-a-build-definition-that-supports-deployment/_static/image5.png)
9. V dialogovém okně **položky k sestavení** klikněte na tlačítko **Přidat**.
10. V rozevíracím seznamu **položky typu** vyberte možnost **soubory projektu MSBuild**.
11. Přejděte do umístění vlastního souboru projektu, pomocí kterého budete řídit proces nasazení, vyberte soubor a klikněte na tlačítko **OK**.

    ![](creating-a-build-definition-that-supports-deployment/_static/image6.png)
12. V dialogovém okně **položky k sestavení** by nyní mělo být zobrazeno dvě položky. Klikněte na tlačítko **OK**.

    ![](creating-a-build-definition-that-supports-deployment/_static/image7.png)
13. Na kartě **proces** v tabulce **Parametry procesu sestavení** rozbalte část **Upřesnit** .
14. V řádku **argumenty MSBuild** přidejte všechny argumenty příkazového řádku MSBuild, které musí *jedna* z položek sestavit. Ve scénáři řešení Contact Manager jsou vyžadovány tyto argumenty:

    [!code-console[Main](creating-a-build-definition-that-supports-deployment/samples/sample1.cmd)]

    ![](creating-a-build-definition-that-supports-deployment/_static/image8.png)
15. V tomto příkladu:

    1. Při sestavování řešení Contact Manageru se vyžadují argumenty balíčku **DeployOnBuild = true** a **DeployTarget =** . Nástroj MSBuild vydává pokyn k vytváření balíčků pro nasazení webu po sestavení každého projektu webové aplikace, jak je popsáno v tématu [sestavování a balení projektů webových aplikací](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).
    2. Při vytváření souboru *Publish. proj* je vyžadován argument **TargetEnvPropsFile** . Tato vlastnost označuje umístění konfiguračního souboru specifického pro prostředí, jak je popsáno v tématu [Principy procesu sestavení](../web-deployment-in-the-enterprise/understanding-the-build-process.md).
16. Na kartě **zásady uchovávání informací** nakonfigurujte, kolik sestavení každého typu chcete zachovat podle potřeby.
17. Klikněte na **Uložit**.

## <a name="queue-a-build"></a>Zařazení sestavení do fronty

V tomto okamžiku jste vytvořili alespoň jednu novou definici sestavení. Proces sestavení, který jste definovali, se nyní spustí podle triggerů, které jste zadali v definici sestavení.

Pokud jste nakonfigurovali definici sestavení tak, aby používala CI, můžete otestovat definici sestavení dvěma způsoby:

- Vrátit se změnami obsah do týmového projektu, který spustí automatické sestavení.
- Zařadí sestavení do fronty ručně.

**Ruční zařazení sestavení do fronty**

1. V okně **Team Explorer** klikněte pravým tlačítkem myši na definici sestavení a potom klikněte na příkaz **zařadit nové sestavení do fronty**.

    ![](creating-a-build-definition-that-supports-deployment/_static/image9.png)
2. V dialogovém okně **sestavení fronty** zkontrolujte vlastnosti sestavení a pak klikněte na **fronta**.

    ![](creating-a-build-definition-that-supports-deployment/_static/image10.png)

Chcete-li zkontrolovat průběh a výsledek sestavení&#x2014;bez ohledu na to, zda byly aktivovány ručně nebo automaticky&#x2014;dvakrát klikněte na definici sestavení v okně **Team Explorer** . Tím se otevře karta **Průzkumník sestavení** .

![](creating-a-build-definition-that-supports-deployment/_static/image11.png)

Z tohoto místa můžete řešit problémy s neúspěšnými sestaveními. Pokud dvakrát kliknete na jednotlivé sestavení, můžete zobrazit souhrnné informace a kliknout na podrobné soubory protokolu.

![](creating-a-build-definition-that-supports-deployment/_static/image12.png)

Tyto informace můžete použít k řešení neúspěšných sestavení a vyřešení všech problémů předtím, než se pokusíte o další sestavení.

> [!NOTE]
> Sestavení, která spouštějí logiku nasazení, budou pravděpodobně neúspěšná, dokud neudělíte serveru sestavení žádná oprávnění požadovaná v cílovém prostředí. Další informace najdete v tématu [Konfigurace oprávnění pro nasazení týmového sestavení](configuring-permissions-for-team-build-deployment.md).

## <a name="monitor-the-build-process"></a>Monitorování procesu sestavení

TFS nabízí širokou škálu funkcí, které vám pomůžou monitorovat proces sestavení. TFS například může poslat e-mail nebo zobrazit výstrahy v oznamovací oblasti hlavního panelu po dokončení sestavení. Další informace naleznete v tématu [Run and monitor Builds](https://msdn.microsoft.com/library/ms181721.aspx).

## <a name="conclusion"></a>Závěr

Toto téma popisuje, jak vytvořit definici sestavení v sadě TFS. Definice sestavení je nakonfigurována pro CI, takže proces sestavení se spustí pokaždé, když vývojář vrátí obsah do týmového projektu. Definice sestavení spustí vlastní soubor projektu MSBuild pro nasazení webových balíčků a databázových skriptů do cílového serverového prostředí.

Aby bylo automatizované nasazení v rámci procesu sestavení úspěšné, je nutné udělit příslušné oprávnění k účtu sestavovací služby na cílových webových serverech a cílovém databázovém serveru. Poslední téma v tomto kurzu, [Konfigurace oprávnění pro nasazení týmového sestavení](configuring-permissions-for-team-build-deployment.md), popisuje, jak identifikovat a nakonfigurovat oprávnění požadovaná pro automatizované nasazení ze serveru sestavení týmu.

## <a name="further-reading"></a>Další čtení

Další informace o vytváření definic sestavení naleznete v tématu [Vytvoření základní definice sestavení](https://msdn.microsoft.com/library/ms181716.aspx) a [Definování procesu sestavení](https://msdn.microsoft.com/library/ms181715.aspx). Další informace o sestaveních služby Řízení front najdete v tématu [zařazení sestavení do fronty](https://msdn.microsoft.com/library/ms181722.aspx).

> [!div class="step-by-step"]
> [Předchozí](configuring-a-tfs-build-server-for-web-deployment.md)
> [Další](deploying-a-specific-build.md)

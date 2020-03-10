---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
title: Sestavování a balení projektů webových aplikací | Microsoft Docs
author: jrjlee
description: Pokud chcete nasadit projekt webové aplikace do prostředí vzdáleného serveru, prvním úkolem je sestavit projekt a vygenerovat sadu Web Deployment Pack...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 94e92f80-a7e3-4d18-9375-ff8be5d666ac
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/building-and-packaging-web-application-projects
msc.type: authoredcontent
ms.openlocfilehash: 1d0ee0264ce6461d7b0159f1a44de4de31e2d079
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78573918"
---
# <a name="building-and-packaging-web-application-projects"></a>Sestavení a balení projektů webových aplikací

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Pokud chcete nasadit projekt webové aplikace do prostředí vzdáleného serveru, je prvním úkolem sestavení projektu a vygenerování balíčku pro nasazení webu. Toto téma popisuje, jak proces sestavení funguje pro projekty webových aplikací. Konkrétně vysvětluje:
> 
> - Způsob, jakým kanál publikování na webu (WPP) rozšiřuje proces sestavení tak, aby zahrnoval funkce nasazení.
> - Způsob, jakým nástroj Internetová informační služba (IIS) web pro nasazení webu (Nasazení webu) změní webovou aplikaci na balíček pro nasazení.
> - Jak proces sestavení a balení funguje a jaké soubory jsou vytvořeny.

V aplikaci Visual Studio 2010 proces sestavení a nasazení pro projekty webové aplikace podporuje WPP. WPP poskytuje sadu Microsoft Build Engine (MSBuild) cílů, které zvyšují funkčnost nástroje MSBuild a umožňují integraci s Nasazení webu. V sadě Visual Studio můžete zobrazit tyto rozšířené funkce na stránkách vlastností projektu webové aplikace. **Webová stránka balení a publikování** spolu se stránkou **Package/Publish SQL** umožňuje nakonfigurovat, jak je projekt webové aplikace zabalen pro nasazení, když je proces sestavení dokončen.

![](building-and-packaging-web-application-projects/_static/image1.png)

## <a name="how-does-the-wpp-work"></a>Jak funguje WPP?

Pokud se podíváte na soubor projektu pro C#projekt webové aplikace na bázi, vidíte, že importuje dva soubory. targets.

[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample1.xml)]

První příkaz **Import** je společný pro všechny vizuální C# projekty. Tento soubor, *Microsoft. CSharp. targets*obsahuje cíle a úkoly, které jsou specifické pro C#vizuál. Například úloha C# kompilátoru (**CSC**) je vyvolána zde. Soubor *Microsoft. CSharp. targets* v systému zase importuje soubor *Microsoft. Common. targets* . Tato definice definuje cíle, které jsou společné pro všechny projekty, jako je **sestavení**, opětovné **sestavení**, **spuštění**, **kompilace**a **Vyčištění**. Druhý příkaz **Import** je specifický pro projekty webových aplikací. Soubor *Microsoft. WebApplication. targets* v systému zase importuje soubor *Microsoft. Web. Publishing. targets* . Soubor *Microsoft. Web. Publishing. targets* *je* v podstatě WPP. Definuje cíle, jako jsou **balíčky** a **MSDeployPublish**, které vyvolávají nasazení webu k dokončení různých úloh nasazení.

Abyste pochopili, jak se tyto další cíle používají, otevřete v ukázkovém řešení Contact Manageru soubor *Publish. proj* a podívejte se na cíl **BuildProjects** .

[!code-xml[Main](building-and-packaging-web-application-projects/samples/sample2.xml)]

Tento cíl používá úlohu **MSBuild** k sestavení různých projektů. Všimněte si vlastností **DeployOnBuild** a **DeployTarget** :

- Vlastnost **DeployOnBuild = true** v podstatě znamená, že chcete po úspěšném dokončení sestavení provést další cíl.
- Vlastnost **DeployTarget** Určuje název cíle, který chcete spustit, pokud je vlastnost **DeployOnBuild** rovna hodnotě **true**. V tomto případě určíte, že má nástroj MSBuild po sestavení projektu spustit cíl **balíčku** .

Cíl **balíčku** je definován v souboru *Microsoft. Web. Publishing. targets* . V podstatě tento cíl převezme výstup sestavení projektu webové aplikace a převede ho do balíčku pro nasazení webu, který lze publikovat na webový server služby IIS.

> [!NOTE]
> Chcete-li zobrazit soubor projektu (například <em>ContactManager. Mvc. csproj</em>) v aplikaci Visual Studio 2010, musíte nejprve uvolnit projekt z řešení. V okně <strong>Průzkumník řešení</strong> klikněte pravým tlačítkem myši na uzel projektu a potom klikněte na položku <strong>Uvolnit projekt</strong>. Znovu klikněte pravým tlačítkem na uzel projektu a pak klikněte na <strong>Upravit</strong><em>[soubor projektu]</em>). Soubor projektu se otevře v nezpracovaném formuláři XML. Až budete hotovi, nezapomeňte znovu načíst projekt.  
> Další informace o cílech, úkolech <strong>a příkazech</strong> nástroje MSBuild naleznete v tématu [porozumění souboru projektu](understanding-the-project-file.md). Podrobné seznámení se soubory projektu a WPP naleznete v části [uvnitř Microsoft Build Engine: použití nástroje MSBuild a Team Foundation Build](http://amzn.com/0735645248) podle Sayed Ibrahim Hashimi a William Bartholomew, ISBN: 978-0-7356-4524-0.

## <a name="what-is-a-web-deployment-package"></a>Co je balíček pro nasazení webu?

Při sestavování a nasazování projektu webové aplikace buď pomocí sady Visual Studio 2010 nebo přímo pomocí nástroje MSBuild, je konečný výsledek obvykle balíček pro *nasazení webu*. Balíček pro nasazení webu je soubor. zip. Obsahuje vše, co služba IIS a Nasazení webu potřebuje k opětovnému vytvoření webové aplikace, včetně:

- Kompilovaný výstup vaší webové aplikace, včetně obsahu, souborů prostředků, konfiguračních souborů, zdrojů JavaScriptu a kaskádových šablon stylů (CSS) atd.
- Sestavení pro projekt webové aplikace a pro všechny odkazované projekty v rámci vašeho řešení.
- Skripty SQL pro generování všech databází, které nasazujete pomocí webové aplikace.

Po vygenerování balíčku pro nasazení webu ho můžete publikovat na webový server služby IIS různými způsoby. Můžete ji například vzdáleně nasadit tak, že zacílíte na Nasazení webu službu vzdáleného agenta nebo obslužnou rutinu Nasazení webu na cílovém webovém serveru, nebo můžete pomocí Správce služby IIS ručně importovat balíček na cílovém webovém serveru. Další informace o těchto přístupů k nasazení najdete v tématu [Volba správného přístupu k nasazení webu](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md).

## <a name="how-does-the-build-process-work"></a>Jak proces sestavení funguje?

To ukazuje, co se stane při sestavení a zabalení projektu webové aplikace:

![](building-and-packaging-web-application-projects/_static/image2.png)

Při sestavování projektu webové aplikace proces sestavení vygeneruje soubor s názvem *[název projektu]. SourceManifest. XML*. Spolu se souborem projektu a výstupem sestavení to *. Soubor SourceManifest. XML* oznamuje nasazení webu, co je potřeba zahrnout do balíčku pro nasazení webu. Pomocí těchto vstupů Nasazení webu vygeneruje balíček pro nasazení webu s názvem *[název projektu]. zip*.

Společně s balíčkem nasazení webu generuje proces sestavení dva soubory, které vám mohou pomáhat s použitím balíčku:

- Soubor *. deploy. cmd* obsahuje sadu parametrizovaných příkazů nasazení webu (msdeploy. exe), které publikují balíček pro nasazení webu na vzdáleném webovém serveru služby IIS. Spuštění souboru *. deploy. cmd* s příslušnými parametry obvykle poskytuje rychlejší a jednodušší alternativu k ručnímu vytváření příkazů MSDeploy. exe.
- Soubor *SetParameters. XML* poskytuje sadu hodnot parametrů pro příkaz msdeploy. exe. Tyto hodnoty zahrnují vlastnosti, jako je název webové aplikace služby IIS, do které chcete balíček nasadit, hodnoty všech koncových bodů služby a připojovacích řetězců, které jsou definovány v souboru *Web. config* , a všechny hodnoty vlastností nasazení, které jsou definovány na stránkách vlastností projektu.

Soubor *SetParameters. XML* je klíč pro správu procesu nasazení. Tento soubor je vygenerován dynamicky podle obsahu vašeho projektu webové aplikace. Například pokud přidáte připojovací řetězec do souboru *Web. config* , proces sestavení automaticky rozpozná připojovací řetězec, zruší odpovídající nasazení a vytvoří záznam v souboru *SetParameters. XML* , který umožňuje změnit připojovací řetězec v rámci procesu nasazení. V dalším tématu [Konfigurace parametrů pro nasazení webového balíčku](configuring-parameters-for-web-package-deployment.md), vysvětluje roli tohoto souboru podrobněji a popisuje různé způsoby, jak ho můžete upravovat během sestavování a nasazování.

> [!NOTE]
> V aplikaci Visual Studio 2010 nepodporuje WPP předkompilování stránek ve webové aplikaci před sbalením. Další verze sady Visual Studio a WPP budou zahrnovat možnost předkompilování webové aplikace jako možnosti balení.

## <a name="conclusion"></a>Závěr

Toto téma poskytuje přehled procesu sestavení a balení pro projekty webových aplikací v aplikaci Visual Studio 2010. Popisuje, jak vám WPP umožňuje vyvolat Nasazení webu příkazy z MSBuild a vysvětluje, jak proces sestavení a balení funguje.

Po vytvoření balíčku pro nasazení webu je dalším krokem jeho nasazení. Další informace najdete v tématu [Konfigurace parametrů pro nasazení webového balíčku](configuring-parameters-for-web-package-deployment.md) a [nasazení webových balíčků](deploying-web-packages.md).

## <a name="further-reading"></a>Další čtení

Další témata v tomto kurzu, [Konfigurace parametrů pro nasazení webového balíčku](configuring-parameters-for-web-package-deployment.md) a [nasazení webových balíčků](deploying-web-packages.md), poskytují pokyny k používání webového balíčku, který jste vytvořili. Konečný kurz v této sérii, [Pokročilé nasazení podnikového webu](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md), poskytuje pokyny k přizpůsobení a řešení potíží s procesem balení.

Podrobné seznámení se soubory projektu a WPP naleznete v části [uvnitř Microsoft Build Engine: použití nástroje MSBuild a Team Foundation Build](http://amzn.com/0735645248) podle Sayed Ibrahim Hashimi a William Bartholomew, ISBN: 978-0-7356-4524-0.

> [!div class="step-by-step"]
> [Předchozí](understanding-the-build-process.md)
> [Další](configuring-parameters-for-web-package-deployment.md)

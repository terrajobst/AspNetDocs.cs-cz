---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery
title: Průběžná integrace a průběžné doručování (vytváření skutečných cloudových aplikací s Azure) | Microsoft Docs
author: MikeWasson
description: Vytváření reálných cloudových aplikací pomocí Azure je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které mohou...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: eaece9f5-f80c-428b-b771-5db66d275b7d
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery
msc.type: authoredcontent
ms.openlocfilehash: cf3c65ef95528173eed3fb08984035b2512861c4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617836"
---
# <a name="continuous-integration-and-continuous-delivery-building-real-world-cloud-apps-with-azure"></a>Průběžná integrace a průběžné doručování (vytváření skutečných cloudových aplikací s Azure)

[Jan Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Dykstra](https://github.com/tdykstra)

[Stažení opravy projektu IT](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stažení elektronické knihy](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **Vytváření reálných cloudových aplikací pomocí Azure** je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které vám pomůžou úspěšně vyvíjet webové aplikace pro Cloud. Informace o elektronické příručce najdete v [první kapitole](introduction.md).

První dva doporučené vzory vývojového procesu byly [automatizovat vše](automate-everything.md) a [správu zdrojového kódu](source-control.md)a třetí model procesu je kombinuje. Průběžná integrace (CI) znamená, že když vývojář zkontroluje kód do zdrojového úložiště, automaticky se spustí sestavení. Průběžné doručování (CD) provede tento krok dál: po úspěšném sestavení a automatizované testy jednotek se aplikace automaticky nasadí do prostředí, kde můžete provádět podrobnější testování.

Cloud vám umožní minimalizovat náklady na údržbu testovacího prostředí, protože platíte jenom za prostředky prostředí za předpokladu, že je používáte. Váš proces CD může nastavit testovací prostředí, když ho potřebujete, a po dokončení testování můžete prostředí využít.

## <a name="continuous-integration-and-continuous-delivery-workflow"></a>Pracovní postup průběžné integrace a průběžného doručování

Obecně doporučujeme průběžné doručování do prostředí pro vývoj a přípravu. Většina týmů, dokonce i v Microsoftu, vyžaduje pro produkční nasazení ruční kontrolu a proces schvalování. V případě nasazení v produkčním prostředí byste se měli ujistit, že k němu dojde, když jsou hlavní lidé na vývojovém týmu k dispozici pro podporu nebo v obdobích s nízkým provozem. Nemáte ale nic, co vám nebrání zcela automatizovat vývojová a testovací prostředí, aby se všichni vývojáři mohli vrátit ke změnám a aby bylo pro testování přijetí nastaveno prostředí.

Následující diagram ze [vzorů a postupů Microsoftu o průběžném doručování](https://aka.ms/ReleasePipeline) ilustruje typický pracovní postup. Kliknutím na obrázek zobrazíte jeho plnou velikost v původním kontextu.

[pracovní postup průběžného doručování ![](continuous-integration-and-continuous-delivery/_static/image1.png)](https://msdn.microsoft.com/library/dn449955.aspx)

## <a name="how-the-cloud-enables-cost-effective-ci-and-cd"></a>Jak Cloud umožňuje nákladově efektivní CI a CD

Automatizace těchto procesů v Azure je snadná. Vzhledem k tomu, že používáte vše v cloudu, nemusíte kupovat ani spravovat servery pro vaše sestavení nebo testovací prostředí. A nemusíte čekat, než bude server dostupný pro vaše testování. U každého sestavení, které uděláte, můžete v Azure aktivovat testovací prostředí pomocí skriptu Automation, spustit testy přijetí nebo podrobnější testy, a až budete hotovi, stačí, když jste to udělali. A pokud tento server spouštíte jenom na 2 hodiny nebo 8 hodin nebo den, bude se vám za to, že je třeba platit jenom za čas, kdy je počítač skutečně spuštěný, platit minimální. Například prostředí potřebné pro opravu IT aplikace v podstatě stojí za 1 cent za hodinu, pokud přejdete na jednu úroveň výš než úroveň Free. Pokud jste v průběhu měsíce spustili prostředí jenom za hodinu, vaše testovací prostředí by mohlo být levnější než Latte zakoupené na Starbucks.

## <a name="azure-devops-services"></a>Azure DevOps Services 

Azure DevOps Services poskytuje řadu funkcí, které vám pomůžou s vývojem aplikací z plánování nasazení.

- Podporuje správu zdrojového kódu Git (Distributed) i TFVC (centralizovaný).
- Nabízí elastickou sestavovací službu, což znamená, že dynamicky vytvoří sestavovací servery, když jsou potřeba, a po dokončení je vybere. Můžete automaticky aktivovat sestavení, když někdo kontroluje změny ve zdrojovém kódu a vy nemusíte přidělit a zaplatit za vaše vlastní servery sestavení, které jsou nečinné většinou času. Sestavovací služba je zdarma, dokud nepřekračujete určitý počet sestavení. Pokud očekáváte, že budete provádět velké množství sestavení, můžete platit trochu navíc pro rezervované servery sestavení.
- Podporuje průběžné doručování do Azure.
- Podporuje automatizované zátěžové testování. Zátěžové testování je pro cloudovou aplikaci kritické, ale často je opomíjené, dokud není příliš pozdě. Zátěžové testování simuluje těžké používání aplikace tisíci uživatelů, což vám umožní najít kritická místa a zvýšit propustnost – před uvolněním aplikace do produkčního prostředí.
- Podporuje spolupráci v rámci týmové místnosti, která usnadňuje komunikaci v reálném čase a spolupráci pro malé agilní týmy.
- Podporuje agilní řízení projektů.

Další informace o funkcích průběžné integrace a doručování Azure DevOps Services najdete v [dokumentaci ke službě Azure DevOps](/azure/devops/index).

Pokud hledáte správu projektů, týmovou spolupráci a řešení správy zdrojového kódu, podívejte se Azure DevOps Services. Zaregistrujte se na [Azure DevOps Services](https://dev.azure.com/).

## <a name="summary"></a>Souhrn

První tři vzory vývoje v cloudu byly o tom, jak implementovat recyklovatelné, spolehlivé a předvídatelné vývojové procesy s malým časem. V [další kapitole](web-development-best-practices.md) začneme pohlížet na struktury architektury a kódování.

## <a name="resources"></a>Zdroje

Další informace najdete v tématu [nasazení webové aplikace v Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-deploy/).

Viz také následující zdroje informací:

- [Vytvoření kanálu pro vydání s Team Foundation Server 2012](https://aka.ms/ReleasePipeline). Elektronická kniha, praktická cvičení a ukázka kódu podle vzorů a postupů Microsoftu, nabízí podrobný Úvod k průběžnému doručování. Pokrývá použití Visual Studio Lab Management a sady Visual Studio Release Management.
- [DevOps nástroje a pokyny pro Alm](https://aka.ms/vsarsolutions/). ALM skupiny zavedly doprovodné řešení Sample DevOps Workbench a praktické pokyny ve spolupráci se vzorci &amp; postupy, který *vytváří kanál vydání s tfs 2012*, jako skvělý způsob, jak začít s vytvářením konceptů DevOps &amp; Release Management pro TFS 2012 a zahájit pneumatiky. Návod ukazuje, jak jednou vytvořit a nasadit do více prostředí.
- [Testování pro nepřetržité doručování pomocí sady Visual Studio 2012](https://msdn.microsoft.com/library/jj159345.aspx). Elektronická kniha podle vzorů a postupů od Microsoftu vysvětluje, jak integrovat automatizované testování s průběžným doručováním.
- [WindowsAzureDeploymentTracker](https://github.com/RyanTBerry/WindowsAzureDeploymentTracker). Zdrojový kód pro nástroj, který má zachytit sestavení z TFS (na základě popisku), sestavit ho, zabalit ho a dovolit někomu v roli DevOps nakonfigurovat konkrétní aspekty IT a vložit ho do Azure. Nástroj sleduje proces nasazení, aby bylo možné operace vrátit zpět do dříve nasazené verze. Nástroj nemá žádné externí závislosti a může pracovat samostatně pomocí rozhraní API TFS a sady Azure SDK.
- [Průběžné doručování: spolehlivé softwarové verze prostřednictvím automatizace sestavení, testování a nasazení](https://www.amazon.com/Continuous-Delivery-Deployment-Automation-Addison-Wesley/dp/0321601912/ref=sr_1_1?s=books&amp;ie=UTF8&amp;qid=1377126361). Book by jez Humble.
- [Návrh verze IT! a nasazení softwaru připraveného pro produkční](https://www.amazon.com/Release-It-Production-Ready-Pragmatic-Programmers/dp/0978739213)prostředí. Kniha podle Michal T. Nygard.

> [!div class="step-by-step"]
> [Předchozí](source-control.md)
> [Další](web-development-best-practices.md)

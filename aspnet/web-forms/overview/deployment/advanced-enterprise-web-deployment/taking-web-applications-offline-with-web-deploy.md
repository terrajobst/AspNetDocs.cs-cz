---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/taking-web-applications-offline-with-web-deploy
title: Přepnutí webových aplikací do režimu offline pomocí Nasazení webu | Microsoft Docs
author: jrjlee
description: Toto téma popisuje, jak převést webovou aplikaci do režimu offline po dobu trvání automatizovaného nasazení pomocí webové depl služby Internetová informační služba (IIS)...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 3e9f6e7d-8967-4586-94d5-d3a122f12529
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/taking-web-applications-offline-with-web-deploy
msc.type: authoredcontent
ms.openlocfilehash: ba60664a0c3daa0650cd7e7cfc4ab9da08df3440
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526066"
---
# <a name="taking-web-applications-offline-with-web-deploy"></a>Převedení webových aplikací offline nástrojem pro nasazení webu

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma popisuje, jak převést webovou aplikaci do režimu offline po dobu trvání automatizovaného nasazení pomocí nástroje pro nasazení webu služby Internetová informační služba (IIS) (Nasazení webu). Uživatelé, kteří přešli do webové aplikace, budou přesměrováni do *aplikace\_offline souboru. htm* až do dokončení nasazení.

Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého [řešení](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.

Metoda nasazení na srdce těchto kurzů je založena na způsobu rozdělení souborů projektu popsaných v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md), ve kterém je proces sestavení řízen dvěma soubory&#x2014;projektu jeden, který obsahuje pokyny pro sestavení, které platí pro každé cílové prostředí, a jedno obsahující nastavení sestavení a nasazení specifické pro konkrétní prostředí. V době sestavení je soubor projektu specifický pro prostředí sloučen do souboru projektu prostředí – nezávislá a vytvoří kompletní sadu instrukcí pro sestavení.

## <a name="task-overview"></a>Přehled úlohy

V mnoha scénářích budete chtít při provádění změn v souvisejících součástech, jako jsou databáze nebo webové služby, převést webovou aplikaci do offline režimu. Ve službě IIS a ASP.NET to můžete dosáhnout umístěním souboru s názvem *App\_offline. htm* do kořenové složky webu služby IIS nebo webové aplikace. *Aplikace\_offline souboru. htm* je standardní soubor HTML a obvykle obsahuje jednoduchou zprávu, která dává uživateli, že lokalita je dočasně nedostupná z důvodu údržby. I když *aplikace\_offline souboru. htm* existuje v kořenové složce webu, služba IIS automaticky přesměruje všechny požadavky na daný soubor. Až dokončíte aktualizace, odeberte *aplikaci\_offline souboru. htm* a web bude pokračovat v obsluze požadavků obvyklým způsobem.

Když použijete Nasazení webu k provádění automatizovaných nebo jednoduchých nasazení do cílového prostředí, možná budete chtít přidat a odebrat *aplikaci\_offline souboru. htm* do procesu nasazení. K tomu je potřeba provést tyto úlohy vysoké úrovně:

- V souboru projektu Microsoft Build Engine (MSBuild), který používáte k řízení procesu nasazení, vytvořte cíl nástroje MSBuild, který zkopíruje *aplikaci\_offline soubor. htm* na cílový server před zahájením všech úloh nasazení.
- Přidejte další cíl nástroje MSBuild, který odebere *aplikaci\_offline souboru. htm* z cílového serveru po dokončení všech úloh nasazení.
- V projektu webové aplikace vytvořte soubor *. WPP. targets* , který zajistí, že je do balíčku pro nasazení přidána *aplikace\_offline soubor. htm* při vyvolání nasazení webu.

V tomto tématu se dozvíte, jak provádět tyto postupy. V úlohách a návodech v tomto tématu se předpokládá, že jste již vytvořili řešení, které obsahuje alespoň jeden projekt webové aplikace a že k řízení procesu nasazení použijete vlastní soubor projektu, jak je popsáno v tématu [nasazení webu v podniku](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md). Alternativně můžete použít ukázkové řešení [Contact Manageru](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) a postupovat podle příkladů v tématu.

## <a name="adding-an-app_offline-file-to-a-web-application-project"></a>Přidání aplikace\_offline souboru do projektu webové aplikace

První úkol, který je třeba dokončit, je přidání *aplikace\_offline* souboru do projektu webové aplikace:

- Chcete-li zabránit tomu, aby soubor v konfliktu s procesem vývoje (nechcete, aby byla vaše aplikace trvale offline), měli byste ji zavolat na jinou hodnotu než *aplikace\_offline. htm*. Souborovou aplikaci můžete například pojmenovat *\_offline-Template. htm*.
- Chcete-li zabránit nasazení souboru tak, jak je, měli byste nastavit akci sestavení na **žádné**.

**Přidání aplikace\_offline souboru do projektu webové aplikace**

1. Otevřete řešení v aplikaci Visual Studio 2010.
2. V okně **Průzkumník řešení** klikněte pravým tlačítkem myši na projekt webové aplikace, přejděte na **Přidat**a klikněte na **Nová položka**.
3. V dialogovém okně **Přidat novou položku** vyberte možnost **Stránka HTML**.
4. Do pole **název** zadejte **App\_offline-Template. htm**a pak klikněte na **Přidat**.

    ![](taking-web-applications-offline-with-web-deploy/_static/image1.png)
5. Přidejte jednoduchý kód HTML, který informuje uživatele o tom, že aplikace není k dispozici, a pak soubor uložte. Nezahrnujte žádné značky na straně serveru (například všechny značky, které jsou s předponou "ASP:"). 

    ![](taking-web-applications-offline-with-web-deploy/_static/image2.png)
6. V okně **Průzkumník řešení** klikněte pravým tlačítkem myši na nový soubor a potom klikněte na příkaz **vlastnosti**.
7. V okně **vlastnosti** vyberte na řádku **Akce sestavení** možnost **žádný**.

    ![](taking-web-applications-offline-with-web-deploy/_static/image3.png)

## <a name="deploying-and-deleting-an-app_offline-file"></a>Nasazení a odstranění aplikace\_offline souboru

Dalším krokem je úprava logiky nasazení a zkopírování souboru na cílový server na začátku procesu nasazení a jeho odebrání na konci.

> [!NOTE]
> Další postup předpokládá, že používáte vlastní soubor projektu MSBuild k řízení procesu nasazení, jak je popsáno v tématu [Principy souboru projektu](../web-deployment-in-the-enterprise/understanding-the-project-file.md). Pokud nasazujete přímo ze sady Visual Studio, budete muset použít jiný přístup. Sayed Ibrahim Hashimi popisuje jeden takový postup, [jak během publikování převést vaši webovou aplikaci do offline režimu](http://sedodream.com/2012/01/08/HowToTakeYourWebAppOfflineDuringPublishing.aspx).

Chcete-li nasadit *aplikaci\_offline* souboru na cílový web služby IIS, je nutné vyvolat soubor MSDeploy. exe pomocí [zprostředkovatele nasazení webu **contentPath** ](https://technet.microsoft.com/library/dd569034(WS.10).aspx). Zprostředkovatel **contentPath** podporuje cesty k fyzickým adresářům i webové aplikace IIS nebo cesty k aplikacím, což usnadňuje volbu synchronizace souborů mezi složkou projektu sady Visual Studio a webovou aplikací služby IIS. Chcete-li nasadit soubor, váš příkaz MSDeploy by měl vypadat takto:

[!code-console[Main](taking-web-applications-offline-with-web-deploy/samples/sample1.cmd)]

Chcete-li odebrat soubor z cílové lokality na konci procesu nasazení, příkaz MSDeploy by měl vypadat takto:

[!code-console[Main](taking-web-applications-offline-with-web-deploy/samples/sample2.cmd)]

Chcete-li tyto příkazy automatizovat jako součást procesu sestavení a nasazení, je třeba je integrovat do vlastního souboru projektu MSBuild. Další postup popisuje, jak to provést.

**Nasazení a odstranění aplikace\_offline souboru**

1. V aplikaci Visual Studio 2010 otevřete soubor projektu MSBuild, který řídí proces nasazení. V ukázkovém řešení [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) se jedná o soubor *Publish. proj* .
2. V kořenovém elementu **projektu** vytvořte nový prvek **Property** pro ukládání proměnných *aplikace\_offline* nasazení:

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample3.xml)]
3. Vlastnost **SourceRoot** je definována jinde v souboru *Publish. proj* . Označuje umístění kořenové složky pro zdrojový obsah vzhledem k aktuální cestě&#x2014;jinými slovy vzhledem k umístění souboru *Publish. proj* .
4. Zprostředkovatel služby **contentPath** nebude akceptovat relativní cesty k souborům, takže před jeho nasazením musíte získat absolutní cestu ke zdrojovému souboru. K tomu můžete použít úlohu [ConvertToAbsolutePath –](https://msdn.microsoft.com/library/bb882668.aspx) .
5. Přidejte nový **cílový** element s názvem **GetAppOfflineAbsolutePath**. V rámci tohoto cíle použijte úlohu **ConvertToAbsolutePath –** k získání absolutní cesty k *aplikaci\_offline souboru šablony* do složky projektu.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample4.xml)]
6. Tento cíl vezme relativní cestu k *aplikaci\_offline souboru šablony* ve složce projektu a uloží ji do nové vlastnosti jako absolutní cestu k souboru. Atribut **BeforeTargets** určuje, že chcete, aby se tento cíl spustil před cílem **DeployAppOffline** , který vytvoříte v dalším kroku.
7. Přidejte nový cíl s názvem **DeployAppOffline**. V rámci tohoto cíle volejte příkaz MSDeploy. exe, který nasadí vaši *aplikaci\_offline* souboru na cílový webový server.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample5.xml)]
8. V tomto příkladu je vlastnost **ContactManagerIisPath** definovaná jinde v souboru projektu. Toto je jednoduše cesta k aplikaci služby IIS ve formátu *[název webu IIS]/[název aplikace]* . Zahrnutí podmínky v cíli umožňuje uživatelům přepínání *aplikace\_offline* nasazení, a to změnou hodnoty vlastnosti nebo zadáním parametru příkazového řádku.
9. Přidejte nový cíl s názvem **DeleteAppOffline**. V rámci tohoto cíle volejte příkaz MSDeploy. exe, který odebere vaši *aplikaci\_offline* souboru z cílového webového serveru.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample6.xml)]
10. Konečným úkolem je vyvolat tyto nové cíle v příslušných bodech během provádění souboru projektu. Můžete to udělat různými způsoby. Například v souboru *Publish. proj* vlastnost **FullPublishDependsOn** určuje seznam cílů, které musí být spuštěny v pořadí, kdy je vyvolán výchozí cíl **FullPublish** .
11. Upravte soubor projektu MSBuild tak, aby vyvolal cíle **DeployAppOffline** a **DeleteAppOffline** ve vhodných bodech v procesu publikování.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample7.xml)]

Když spustíte vlastní soubor projektu MSBuild, *aplikace\_offline* soubor se nasadí na server hned po úspěšném sestavení. Po dokončení všech úloh nasazení se pak odstraní ze serveru.

## <a name="adding-an-app_offline-file-to-deployment-packages"></a>Přidání aplikace\_offline souboru do balíčků pro nasazení

V závislosti na tom, jak nakonfigurujete nasazení, se&#x2014;&#x2014;může při nasazení webového balíčku do cíle automaticky odstranit veškerý existující obsah v cílové webové aplikaci IIS, jako je například *aplikace\_offline. htm* . Aby bylo zajištěno, že *aplikace\_offline souboru. htm* zůstane v platnosti po dobu trvání nasazení, je třeba zahrnout soubor do samotného balíčku pro nasazení webu společně s nasazením souboru přímo na začátku procesu nasazení.

- Pokud jste postupovali s předchozími úkoly v tomto tématu, přihlásili jste se do projektu webové aplikace *\_v režimu offline. htm aplikace* v jiném názvu souboru (používáme *App\_offline-Template. htm*) a nastavíte akci sestavení na **žádná**. Tyto změny jsou nezbytné, aby se zabránilo souboru v konfliktu s vývojem a laděním. V důsledku toho je nutné přizpůsobit proces balení, aby bylo zajištěno, že *aplikace\_offline souboru. htm* je součástí balíčku pro nasazení webu.

Kanál pro publikování na webu (WPP) používá seznam položek s názvem **FilesForPackagingFromProject** k vytvoření seznamu souborů, které by měly být zahrnuty do balíčku pro nasazení webu. Obsah svých webových balíčků můžete přizpůsobit přidáním vlastních položek do tohoto seznamu. K tomu je potřeba provést tyto kroky vysoké úrovně:

1. Vytvořte vlastní soubor projektu nazvaný *[název projektu]. WPP. targets* ve stejné složce jako soubor projektu.

    > [!NOTE]
    > Soubor *. WPP. targets* musí být ve stejné složce jako soubor&#x2014;projektu webové aplikace, například *ContactManager. Mvc. csproj*&#x2014;, nikoli ve stejné složce jako jakékoli vlastní soubory projektu, které slouží k řízení procesu sestavení a nasazení.
2. V souboru *. WPP. targets* vytvořte nový cíl nástroje MSBuild, který se spustí *před* cílem **CopyAllFilesToSingleFolderForPackage** . Toto je cíl WPP, který vytváří seznam věcí, které se mají zahrnout do balíčku.
3. V novém cíli vytvořte element **Item** .
4. V prvku skupiny **položek** přidejte položku **FilesForPackagingFromProject** a určete *aplikaci\_offline. htm* .

Soubor *. WPP. targets* by měl vypadat takto:

[!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample8.xml)]

Toto jsou klíčové body poznámky v tomto příkladu:

- Atribut **BeforeTargets** vloží tento cíl do WPP tím, že určí, že by měl být proveden těsně před cílem **CopyAllFilesToSingleFolderForPackage** .
- Položka **FilesForPackagingFromProject** používá hodnotu metadat **DestinationRelativePath** k přejmenování souboru z *aplikace\_offline-template. htm* na *aplikaci\_offline. htm* při přidání do seznamu.

Následující postup ukazuje, jak přidat tento soubor *. WPP. targets* do projektu webové aplikace.

**Přidání souboru. WPP. targets do balíčku pro nasazení webu**

1. Otevřete řešení v aplikaci Visual Studio 2010.
2. V okně **Průzkumník řešení** klikněte pravým tlačítkem myši na uzel projektu webové aplikace (například **ContactManager. Mvc**), přejděte na **Přidat**a klikněte na **Nová položka**.
3. V dialogovém okně **Přidat novou položku** vyberte šablonu **souboru XML** .
4. Do pole **název** zadejte *[název projektu] * * *. WPP. targets** (například **ContactManager. Mvc. WPP. targets**) a pak klikněte na **Přidat**.

    ![](taking-web-applications-offline-with-web-deploy/_static/image4.png)

    > [!NOTE]
    > Pokud přidáte novou položku do kořenového uzlu projektu, je soubor vytvořen ve stejné složce jako soubor projektu. To můžete ověřit tak, že otevřete složku v Průzkumníku Windows.
5. Do souboru přidejte kód MSBuild popsaný výše.

    [!code-xml[Main](taking-web-applications-offline-with-web-deploy/samples/sample9.xml)]
6. Uložte a zavřete soubor *[název projektu]. WPP. targets* .

Při příštím sestavení a zabalení projektu webové aplikace bude modul WPP automaticky detekovat soubor *. WPP. targets* . Soubor *app\_offline-Template. htm* bude součástí výsledného balíčku pro nasazení webu jako *aplikace\_offline. htm*.

> [!NOTE]
> Pokud se nasazení nezdaří, *aplikace\_offline souboru. htm* zůstane na svém místě a vaše aplikace zůstane offline. To je obvykle požadované chování. Pokud chcete aplikaci převést zpět do režimu online, můžete *aplikaci odstranit\_offline souboru. htm* z webového serveru. Případně, pokud opravíte nějaké chyby a spustíte úspěšné nasazení, bude odebrána *aplikace\_offline souboru. htm* .

## <a name="conclusion"></a>Závěr

Toto téma popisuje, jak převést webovou aplikaci do režimu offline po dobu trvání nasazení, publikováním *aplikace\_souboru offline. htm* na cílovém serveru na začátku procesu nasazení a jeho odebráním na konci. Popisuje také způsob zahrnutí *aplikace\_offline souboru. htm* do balíčku pro nasazení webu.

## <a name="further-reading"></a>Další čtení

Další informace o procesu balení a nasazení najdete v tématu [sestavování a balení projektů webových aplikací](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md), [Konfigurace parametrů pro nasazení webového balíčku](../web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment.md)a [nasazení webových balíčků](../web-deployment-in-the-enterprise/deploying-web-packages.md).

Pokud publikujete své webové aplikace přímo ze sady Visual Studio a nepoužijete vlastní přístup k souboru projektu MSBuild popsaný v těchto kurzech, budete muset při publikování převést aplikaci do offline režimu. přihlášení.

> [!div class="step-by-step"]
> [Předchozí](excluding-files-and-folders-from-deployment.md)
> [Další](running-windows-powershell-scripts-from-msbuild-project-files.md)

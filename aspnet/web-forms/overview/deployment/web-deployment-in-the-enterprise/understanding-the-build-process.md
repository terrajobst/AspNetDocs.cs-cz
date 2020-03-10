---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
title: Princip procesu sestavení | Microsoft Docs
author: jrjlee
description: Toto téma poskytuje návod pro proces sestavení a nasazení na podnikové úrovni. Přístup popsaný v tomto tématu používá vlastní Microsoft Build Engin...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 5b982451-547b-4a2f-a5dc-79bc64d84d40
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
msc.type: authoredcontent
ms.openlocfilehash: 802d93f7ca987d018967275bae68b8c56d883a25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641139"
---
# <a name="understanding-the-build-process"></a>Vysvětlení procesu sestavení

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Toto téma poskytuje návod pro proces sestavení a nasazení na podnikové úrovni. Přístup popsaný v tomto tématu používá vlastní soubory projektu Microsoft Build Engine (MSBuild) k zajištění jemně odstupňované kontroly nad všemi aspekty procesu. V rámci souborů projektu se vlastní cíle MSBuild používají ke spouštění nástrojů pro nasazení, jako je nástroj pro nasazení webu Internetová informační služba (IIS) a nástroj pro nasazení databáze VSDBCMD. exe.
> 
> > [!NOTE]
> > Předchozí téma [porozumění souboru projektu](understanding-the-project-file.md), popisuje klíčové komponenty souboru projektu MSBuild a zavádí koncept rozdělených souborů projektu pro podporu nasazení do více cílových prostředí. Pokud jste ještě tyto koncepty nepoužívali, měli byste před zahájením práce s tímto tématem zkontrolovat [porozumění souboru projektu](understanding-the-project-file.md) .

Toto téma je součástí série kurzů založených na požadavcích podnikového nasazení fiktivní společnosti s názvem Fabrikam, Inc. Tato série kurzů používá ukázkové řešení&#x2014;, pomocí kterého [řešení](the-contact-manager-solution.md)&#x2014;správce kontaktů představuje webovou aplikaci s realistickou úrovní složitosti, včetně aplikace ASP.NET MVC 3, služby Windows Communication Foundation (WCF) a databázového projektu.

Metoda nasazení na srdce těchto kurzů je založena na způsobu rozdělení souborů projektu popsaných v tématu [Principy souboru projektu](understanding-the-project-file.md), ve kterém je proces sestavení řízen dvěma soubory&#x2014;projektu jeden, který obsahuje pokyny pro sestavení, které platí pro každé cílové prostředí, a jedno obsahující nastavení sestavení a nasazení specifické pro konkrétní prostředí. V době sestavení je soubor projektu specifický pro prostředí sloučen do souboru projektu prostředí – nezávislá a vytvoří kompletní sadu instrukcí pro sestavení.

## <a name="build-and-deployment-overview"></a>Přehled Build and Deployment

V [řešení Správce kontaktů](the-contact-manager-solution.md)tři soubory řídí proces sestavení a nasazení:

- *Soubor univerzálního projektu* (*Publish. proj*). Obsahuje pokyny pro sestavení a nasazení, které se mezi cílovými prostředími nemění.
- *Soubor projektu specifický pro prostředí* (*ENV-dev. proj*). Obsahuje nastavení sestavení a nasazení, která jsou specifická pro konkrétní cílové prostředí. Například můžete použít soubor *ENV-dev. proj* k poskytnutí nastavení pro vývojové nebo testovací prostředí a vytvoření alternativního souboru s názvem *ENV-Stage. proj* k poskytnutí nastavení pro přípravný prostředí.
- *Soubor příkazů* (*Publish-dev. cmd*). Obsahuje příkaz MSBuild. exe, který určuje, které soubory projektu chcete spustit. Můžete vytvořit soubor příkazů pro každé cílové prostředí, kde každý soubor obsahuje příkaz MSBuild. exe, který určuje jiný soubor projektu specifický pro prostředí. To umožňuje vývojáři nasadit do různých prostředí jednoduše tak, že spustí příslušný soubor příkazů.

V ukázkovém řešení najdete tyto tři soubory ve složce řešení publikování.

![](understanding-the-build-process/_static/image1.png)

Předtím, než se podíváte na tyto soubory podrobněji, se podívejme na to, jak celkový proces sestavení funguje při použití tohoto přístupu. Na vysoké úrovni proces sestavení a nasazení vypadá takto:

![](understanding-the-build-process/_static/image2.png)

První věc, ke které dojde, je, že dva&#x2014;soubory projektu, které obsahují obecné pokyny pro sestavení a nasazení a které obsahují nastavení&#x2014;specifické pro prostředí, jsou sloučeny do jediného souboru projektu. Nástroj MSBuild potom funguje podle pokynů v souboru projektu. Vytvoří každý z projektů v řešení pomocí souboru projektu pro každý projekt. Pak volá jiné nástroje, například Nasazení webu (MSDeploy. exe) a nástroj VSDBCMD k nasazení webového obsahu a databází do cílového prostředí.

Od začátku do konce se proces sestavení a nasazení provádí tyto úlohy:

1. Odstraní obsah výstupního adresáře při přípravě na nové sestavení.
2. Vytváří každý projekt v řešení:

    1. Pro webové projekty&#x2014;v tomto případě webová aplikace ASP.NET MVC a webová služba&#x2014;WCF vytvoří proces sestavení balíček pro nasazení webu pro každý projekt.
    2. Pro databázové projekty vytvoří proces sestavení manifest nasazení (soubor. DeployManifest) pro každý projekt.
3. Používá nástroj VSDBCMD. exe k nasazení jednotlivých databázových projektů v řešení pomocí různých vlastností ze souborů&#x2014;projektu cílový připojovací řetězec a název&#x2014;databáze společně se souborem. DeployManifest.
4. Používá nástroj MSDeploy. exe k nasazení každého webového projektu v řešení pomocí různých vlastností ze souborů projektu pro řízení procesu nasazení.

Pomocí ukázkového řešení můžete tento proces sledovat podrobněji.

> [!NOTE]
> Pokyny k přizpůsobení souborů projektu specifických pro prostředí pro vlastní serverová prostředí najdete v tématu [Konfigurace vlastností nasazení pro cílové prostředí](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).

## <a name="invoking-the-build-and-deployment-process"></a>Vyvolává se proces Build and Deployment.

Pro nasazení řešení Contact Manageru do testovacího prostředí Vývojář spustí vývojář soubor příkazů *Publish-dev. cmd* . Tím se vyvolá MSBuild. exe, zadáním příkazu *Publish. proj* jako souboru projektu pro provedení a *env. proj* jako hodnoty parametru.

[!code-console[Main](understanding-the-build-process/samples/sample1.cmd)]

> [!NOTE]
> Přepínač **/FL** (krátký pro **/FileLogger**) zapíše výstup sestavení do souboru s názvem *MSBuild. log* v aktuálním adresáři. Další informace naleznete v tématu [Reference k příkazovému řádku MSBuild](https://msdn.microsoft.com/library/ms164311.aspx).

V tomto okamžiku spustí nástroj MSBuild spuštěný, načte soubor *Publish. proj* a spustí zpracování pokynů v něm. První instrukce instruuje nástroj MSBuild, aby naimportoval soubor projektu, který určuje parametr **TargetEnvPropsFile** .

[!code-xml[Main](understanding-the-build-process/samples/sample2.xml)]

Parametr **TargetEnvPropsFile** určuje soubor *ENV-dev. proj* , takže nástroj MSBuild sloučí obsah souboru *ENV-dev. proj* do souboru *Publish. proj* .

Další prvky, které nástroj MSBuild nalezne ve sloučeném souboru projektu, jsou skupiny vlastností. Vlastnosti jsou zpracovávány v pořadí, ve kterém jsou uvedeny v souboru. Nástroj MSBuild vytvoří dvojici klíč-hodnota pro každou vlastnost a zajistí splnění všech zadaných podmínek. Vlastnosti definované později v souboru přepíšou všechny vlastnosti se stejným názvem definovaným dříve v souboru. Zvažte například vlastnosti **OutputRoot** .

[!code-xml[Main](understanding-the-build-process/samples/sample3.xml)]

Když nástroj MSBuild zpracuje první element **OutputRoot** , neposkytne se podobný parametr s podobným názvem, nastaví hodnotu vlastnosti **OutputRoot** na **.. \Publish\Out**. Když dojde k druhému prvku **OutputRoot** , pokud je podmínka vyhodnocena jako **true**, přepíše hodnotu vlastnosti **OutputRoot** hodnotou parametru **OutDir** .

Další prvek, který MSBuild narazí, je jediná skupina položek obsahující položku s názvem **ProjectsToBuild**.

[!code-xml[Main](understanding-the-build-process/samples/sample4.xml)]

Nástroj MSBuild zpracovává tuto instrukci vytvořením seznamu položek s názvem **ProjectsToBuild**. V tomto případě obsahuje seznam položek jednu hodnotu&#x2014;cesta a název souboru řešení.

V tomto okamžiku jsou zbývající prvky cíli. Cíle jsou zpracovávány jinak než z vlastností&#x2014;a položek v podstatě, cíle nejsou zpracovávány, pokud nejsou explicitně zadány uživatelem nebo vyvolány jinou konstrukcí v rámci souboru projektu. Odvolat, že otevírací značka **projektu** obsahuje atribut **DefaultTargets –** .

[!code-xml[Main](understanding-the-build-process/samples/sample5.xml)]

Nástroj MSBuild dá pokyn k vyvolání cíle **FullPublish** , nejsou-li při vyvolání nástroje MSBuild. exe určeny cíle. Cíl **FullPublish** neobsahuje žádné úlohy. místo toho určuje pouze seznam závislostí.

[!code-xml[Main](understanding-the-build-process/samples/sample6.xml)]

Tato závislost oznamuje nástroji MSBuild, že má spustit cíl **FullPublish** , musí vyvolat tento seznam cílů v zadaném pořadí:

1. Musí vyvolat **čistý** cíl.
2. Musí vyvolat cíl **BuildProjects** .
3. Musí vyvolat cíl **GatherPackagesForPublishing** .
4. Musí vyvolat cíl **PublishDbPackages** .
5. Musí vyvolat cíl **PublishWebPackages** .

### <a name="the-clean-target"></a>Cíl vyčištění

**Čistý** cíl v podstatě odstraní výstupní adresář a veškerý jeho obsah jako přípravu pro nové sestavení.

[!code-xml[Main](understanding-the-build-process/samples/sample7.xml)]

Všimněte si, že cíl zahrnuje prvek **Item** . Při definování vlastností nebo položek v rámci **cílového** prvku vytváříte *dynamické* vlastnosti a položky. Jinými slovy, vlastnosti nebo položky nejsou zpracovány, dokud není proveden cíl. Výstupní adresář možná neexistuje nebo obsahuje žádné soubory, dokud proces sestavení nezačne, takže nemůžete sestavit **\_FilesToDelete** seznamu jako statickou položku; musíte počkat, až bude prováděno provádění. V takovém případě sestavíte seznam jako dynamickou položku v rámci cíle.

> [!NOTE]
> V takovém případě, protože **čistý** cíl je první spuštění, není nutné používat dynamickou skupinu položek. V tomto typu scénáře je však vhodné použít dynamické vlastnosti a položky, protože v určitém okamžiku můžete chtít provést cíle v jiném pořadí.  
> Měli byste se také zaměřit, aby nedošlo k deklarování položek, které nikdy nebudou použity. Pokud máte položky, které bude používat jenom konkrétní cíl, zvažte jejich umístění uvnitř cíle, aby se odstranila veškerá nepotřebná režie na proces sestavení.

Mimo jiné dynamické položky je **čistý** cíl poměrně jednoduchý a využívá předdefinované **zprávy**, **odstraňování**a **RemoveDir –** úkoly:

1. Odeslat zprávu do protokolovacího nástroje.
2. Sestavte seznam souborů, které chcete odstranit.
3. Odstraňte soubory.
4. Odeberte výstupní adresář.

### <a name="the-buildprojects-target"></a>Cíl BuildProjects

Cíl **BuildProjects** v podstatě sestaví všechny projekty v ukázkovém řešení.

[!code-xml[Main](understanding-the-build-process/samples/sample8.xml)]

Tento cíl byl podrobněji popsán v předchozím tématu, [porozumění souboru projektu](understanding-the-project-file.md)pro ilustraci, jakým způsobem jsou úkoly a cíle odkazovat na vlastnosti a položky. V tuto chvíli vás zajímá hlavně úlohu **MSBuild** . Tuto úlohu můžete použít k sestavení více projektů. Úloha nevytváří novou instanci nástroje MSBuild. exe; používá aktuální spuštěnou instanci pro sestavení jednotlivých projektů. Klíčové body zájmu v tomto příkladu jsou vlastnosti nasazení:

- Vlastnost **DeployOnBuild** instruuje nástroj MSBuild, aby po dokončení sestavení každého projektu spouštěla jakékoli pokyny k nasazení v nastavení projektu.
- Vlastnost **DeployTarget** identifikuje cíl, který chcete vyvolat po sestavení projektu. V tomto případě cílový **balíček** sestaví výstup projektu do nasazeného webového balíčku.

> [!NOTE]
> Cíl **balíčku** vyvolá kanál publikování na webu (WPP), který poskytuje integraci mezi msbuildem a nasazení webu. Pokud se chcete podívat na předdefinované cíle, které poskytuje WPP, zkontrolujte soubor *Microsoft. Web. Publishing. targets* ve složce% ProgramFiles (x86)% \ MSBuild\Microsoft\VisualStudio\v10.0\Web.

### <a name="the-gatherpackagesforpublishing-target"></a>Cíl GatherPackagesForPublishing

Pokud zkoumáte cíl **GatherPackagesForPublishing** , všimnete si, že ve skutečnosti neobsahují žádné úkoly. Místo toho obsahuje jednu skupinu položek, která definuje tři dynamické položky.

[!code-xml[Main](understanding-the-build-process/samples/sample9.xml)]

Tyto položky odkazují na balíčky pro nasazení, které byly vytvořeny při spuštění cíle **BuildProjects** . Tyto položky nelze definovat staticky v souboru projektu, protože soubory, na které položky odkazují, neexistují, dokud není proveden cíl **BuildProjects** . Místo toho musí být položky definovány dynamicky v rámci cíle, který není vyvolán až po provedení cíle **BuildProjects** .

Tyto položky se v tomto cíli&#x2014;nepoužívají. Tento cíl jednoduše sestaví položky a Metadata přidružená k jednotlivým hodnotám položek. Po zpracování těchto prvků bude položka **PublishPackages** obsahovat dvě hodnoty, cestu k souboru *ContactManager. Mvc. deploy. cmd* a cestu k souboru *ContactManager. Service. deploy. cmd* . Nasazení webu vytvoří tyto soubory jako součást webového balíčku pro každý projekt a jedná se o soubory, které je nutné vyvolat na cílovém serveru, aby bylo možné balíčky nasadit. Otevřete-li jeden z těchto souborů, bude v podstatě zobrazen příkaz MSDeploy. exe s různými hodnotami parametrů specifických pro sestavení.

Položka **DbPublishPackages** bude obsahovat jednu hodnotu, cestu k souboru *ContactManager. Database. DeployManifest* .

> [!NOTE]
> Soubor. DeployManifest je generován při vytváření databázového projektu a používá stejné schéma jako soubor projektu MSBuild. Obsahuje všechny informace potřebné k nasazení databáze včetně umístění schématu databáze (. dbschema) a podrobností všech skriptů před nasazením a po nasazení. Další informace najdete v tématu [přehled Build and Deployment databáze](https://msdn.microsoft.com/library/aa833165.aspx).

Dozvíte se víc o tom, jak se vytvářejí a používají balíčky pro nasazení a manifesty nasazení databáze při [sestavování a zabalení projektů webových aplikací](building-and-packaging-web-application-projects.md) a [nasazení databázových projektů](deploying-database-projects.md).

### <a name="the-publishdbpackages-target"></a>Cíl PublishDbPackages

Krátce řečeno, cíl **PublishDbPackages** VYVOLÁ nástroj VSDBCMD pro nasazení databáze **ContactManager** do cílového prostředí. Konfigurace nasazení databáze zahrnuje spoustu rozhodnutí a drobné odlišnosti a další informace o tomto postupu najdete v části [nasazení databázových projektů](deploying-database-projects.md) a [přizpůsobení nasazení databáze pro více prostředí](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md). V tomto tématu se zaměříme na to, jak tento cíl skutečně funguje.

Nejprve si všimněte, že počáteční značka obsahuje atribut **výstupy** .

[!code-xml[Main](understanding-the-build-process/samples/sample10.xml)]

Toto je příklad *cílového dávkování*. V souborech projektu MSBuild je dávkování metodou pro iteraci kolekce. Hodnota atributu Outputs ( **výstups** **) "% (DbPublishPackages. identity)"** odkazuje na vlastnost metadata **identity** seznamu položek **DbPublishPackages** . Tento zápis **výstupy =% * * * (ITEMLIST. ItemMetaDataName)* je přeložen jako:

- Rozdělte položky v **DbPublishPackages** na dávky položek, které obsahují stejnou hodnotu metadat **identity** .
- Spustí cíl na dávce.

> [!NOTE]
> **Identita** je jedna z [vestavěných hodnot metadat](https://msdn.microsoft.com/library/ms164313.aspx) , která je přiřazena ke každé položce při vytváření. Odkazuje na hodnotu atributu **include** v prvku&#x2014; **Item** jinými slovy, cestu a název souboru položky.

V takovém případě, protože by nikdy neměla existovat více než jedna položka se stejnou cestou a názvem souboru, budeme v podstatě pracovat se velikostmi dávek. Cíl se spustí jednou pro každý databázový balíček.

Podobný zápis můžete zobrazit ve vlastnosti **\_cmd** , která vytvoří příkaz VSDBCMD s příslušnými přepínači.

[!code-xml[Main](understanding-the-build-process/samples/sample11.xml)]

V tomto případě: **% (DbPublishPackages. DatabaseConnectionString)** , **% (DbPublishPackages. TargetDatabase)** a **% (DbPublishPackages. FullPath)** odkazuje na hodnoty metadat kolekce položek **DbPublishPackages** . Vlastnost **\_cmd** je používána úlohou **exec** , která vyvolá příkaz.

[!code-xml[Main](understanding-the-build-process/samples/sample12.xml)]

V důsledku tohoto zápisu úloha **exec** vytvoří dávky na základě jedinečných kombinací hodnot metadat **DatabaseConnectionString**, **TargetDatabase**a **FullPath** a úloha se spustí jednou pro každou dávku. Toto je příklad *dávkového zpracování úloh*. Vzhledem k tomu, že dávkování na úrovni cíle již dělí kolekci položek na dávky s jednou položkou, úloha **exec** se spustí jednou a pouze jednou pro každou iteraci cíle. Jinými slovy Tato úloha vyvolá nástroj VSDBCMD jednou pro každý balíček databáze v řešení.

> [!NOTE]
> Další informace o cíli a dávkování úloh najdete v tématech [dávkování](https://msdn.microsoft.com/library/ms171473.aspx)nástroje MSBuild, [metadata položky v cílové dávce](https://msdn.microsoft.com/library/ms228229.aspx)a [Metadata položek v dávkování úloh](https://msdn.microsoft.com/library/ms171474.aspx).

### <a name="the-publishwebpackages-target"></a>Cíl PublishWebPackages

Od tohoto okamžiku jste vyvolali cíl **BuildProjects** , který generuje balíček pro nasazení webu pro každý projekt v ukázkovém řešení. Každý balíček je přiložen k souboru *Deploy. cmd* , který obsahuje příkazy MSDeploy. exe vyžadované k nasazení balíčku do cílového prostředí a soubor *SetParameters. XML* , který určuje nezbytné podrobnosti o cílovém prostředí. Vyvolali jste také cíl **GatherPackagesForPublishing** , který generuje kolekci položek obsahující soubory *Deploy. cmd* , které vás zajímají. Cíl **PublishWebPackages** v podstatě provádí tyto funkce:

- Zpracovává soubor *SetParameters. XML* pro každý balíček, aby obsahoval správné podrobnosti pro cílové prostředí pomocí úlohy **XmlPoke –** .
- Vyvolá soubor *Deploy. cmd* pro každý balíček pomocí příslušných přepínačů.

Podobně jako v cíli **PublishDbPackages** používá cíl **PublishWebPackages** cílové dávkování, aby se zajistilo, že se cíl spustí jednou pro každý webový balíček.

[!code-xml[Main](understanding-the-build-process/samples/sample13.xml)]

V rámci cíle se ke spuštění souboru *Deploy. cmd* pro každý webový balíček používá úloha **exec** .

[!code-xml[Main](understanding-the-build-process/samples/sample14.xml)]

Další informace o konfiguraci nasazení webových balíčků naleznete v tématu [sestavování a balení projektů webových aplikací](building-and-packaging-web-application-projects.md).

## <a name="conclusion"></a>Závěr

Toto téma poskytuje návod, jak použít rozdělené soubory projektu k řízení procesu sestavení a nasazení od začátku do konce pro ukázkové řešení Contact Manageru. Použití tohoto přístupu vám umožní spouštět složitá nasazení na podnikové úrovni v jednom kroku s možností opakování pouhým spuštěním souboru příkazů specifických pro konkrétní prostředí.

## <a name="further-reading"></a>Další čtení

Podrobné seznámení se soubory projektu a WPP naleznete v části [uvnitř Microsoft Build Engine: použití nástroje MSBuild a Team Foundation Build](http://amzn.com/0735645248) podle Sayed Ibrahim Hashimi a William Bartholomew, ISBN: 978-0-7356-4524-0.

> [!div class="step-by-step"]
> [Předchozí](understanding-the-project-file.md)
> [Další](building-and-packaging-web-application-projects.md)

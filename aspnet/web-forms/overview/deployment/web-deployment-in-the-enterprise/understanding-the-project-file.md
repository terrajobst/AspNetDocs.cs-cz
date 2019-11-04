---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
title: Porozumění souboru projektu | Microsoft Docs
author: jrjlee
description: Soubory projektu Microsoft Build Engine (MSBuild) leží na srdce procesu sestavení a nasazení. Toto téma začíná koncepčním přehledem nástroje MSBuild...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 07978d9d-341c-4524-bcba-62976f390f77
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-project-file
msc.type: authoredcontent
ms.openlocfilehash: 419fe51aaf65bddcc2c50380f099f842a8d9439c
ms.sourcegitcommit: 84b1681d4e6253e30468c8df8a09fe03beea9309
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/02/2019
ms.locfileid: "73445699"
---
# <a name="understanding-the-project-file"></a>Porozumění souboru projektu

od [Jason Novák](https://github.com/jrjlee)

[Stáhnout PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> Soubory projektu Microsoft Build Engine (MSBuild) leží na srdce procesu sestavení a nasazení. Toto téma začíná koncepčním přehledem nástroje MSBuild a souboru projektu. Popisuje klíčové komponenty, které se budou nacházet při práci se soubory projektu, a funguje jako příklad, jak můžete použít soubory projektu k nasazení reálných aplikací.
> 
> Co se naučíte:
> 
> - Jak nástroj MSBuild používá soubory projektu MSBuild k sestavení projektů.
> - Jak se MSBuild integruje s technologiemi nasazení, jako je třeba nástroj pro nasazení webu Internetová informační služba (IIS) (Nasazení webu).
> - Jak pochopit klíčové součásti souboru projektu.
> - Jak lze použít soubory projektu k sestavení a nasazení komplexních aplikací.

## <a name="msbuild-and-the-project-file"></a>MSBuild a soubor projektu

Při vytváření a sestavování řešení v aplikaci Visual Studio používá Visual Studio nástroj MSBuild k sestavení každého projektu ve vašem řešení. Každý projekt sady Visual Studio obsahuje soubor projektu MSBuild s příponou souboru, který odráží typ projektu&#x2014;, například C# projekt (. csproj), projekt Visual Basic.NET (. vbproj) nebo databázový projekt (. dbproj). Aby bylo možné sestavit projekt, MSBuild musí zpracovat soubor projektu přidružený k projektu. Soubor projektu je dokument XML, který obsahuje všechny informace a pokyny, které nástroj MSBuild potřebuje k sestavení projektu, jako je například obsah, který se má zahrnout, požadavky na platformu, informace o verzi, nastavení webového serveru nebo databázového serveru a úlohy, které je třeba provést.

Soubory projektu MSBuild jsou založené na [schématu XML MSBuild](/visualstudio/msbuild/msbuild-project-file-schema-reference)a v důsledku toho je proces sestavení zcela otevřený a transparentní. Kromě toho není nutné instalovat sadu Visual Studio, aby bylo možné použít modul&#x2014;MSBuild. spustitelný soubor MSBuild. exe je součástí .NET Framework a lze jej spustit z příkazového řádku. Jako vývojář můžete vytvořit vlastní soubory projektu MSBuild pomocí schématu XML pro MSBuild, aby bylo možné nasazovat sofistikovanou a jemně odstupňovanou kontrolu nad tím, jak jsou vaše projekty sestaveny a nasazeny. Tyto vlastní soubory projektu fungují přesně stejným způsobem jako soubory projektu, které aplikace Visual Studio generuje automaticky.

> [!NOTE]
> Můžete také použít soubory projektu MSBuild se službou Team Build Service v Team Foundation Server (TFS). Můžete například použít soubory projektu ve scénářích průběžné integrace (CI) k automatizaci nasazení do testovacího prostředí, když je nový kód vrácen se změnami. Další informace najdete v tématu [konfigurace Team Foundation Server pro automatizované nasazení webu](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md).

### <a name="project-file-naming-conventions"></a>Zásady vytváření názvů souborů projektu

Když vytváříte vlastní soubory projektu, můžete použít jakoukoli příponu souboru, kterou chcete. Pokud ale chcete, aby vaše řešení bylo snazší pochopit, měli byste použít tyto běžné konvence:

- Použijte rozšíření. proj při vytváření souboru projektu, který vytváří projekty.
- Použijte rozšíření. targets při vytváření opakovaně použitelného souboru projektu pro import do jiných souborů projektu. Soubory s příponou. targets obvykle sestavují sám sebe, jednoduše obsahují pokyny, které lze importovat do souborů. proj.

### <a name="integration-with-deployment-technologies"></a>Integrace s technologiemi nasazení

Pokud jste pracovali s projekty webové aplikace v aplikaci Visual Studio 2010, jako jsou webové aplikace ASP.NET a webové aplikace ASP.NET MVC, budete si vědomi, že tyto projekty obsahují integrovanou podporu pro balení a nasazení webové aplikace do cílového prostředí. Stránky **vlastností** pro tyto projekty zahrnují **Balení/publikování webu** a **Balení/publikování SQL** karet, které můžete použít ke konfiguraci způsobu, jakým jsou komponenty vaší aplikace zabaleny a nasazeny. Tím se zobrazí karta **Balení/publikování webu** :

![](understanding-the-project-file/_static/image1.png)

Základní technologie za těmito možnostmi je známá jako kanál publikování na webu (WPP). Rozhraní WPP v podstatě přináší Nástroj MSBuild a [nasazení webu](https://go.microsoft.com/?linkid=9805122) dohromady, aby poskytovala kompletní proces sestavení, balíčku a nasazení pro vaše webové aplikace.

Dobrá zpráva vám umožní využít integrační body, které poskytuje WPP při vytváření vlastních souborů projektu pro webové projekty. Do souboru projektu můžete zahrnout pokyny pro nasazení, které vám umožňují sestavovat projekty, vytvářet balíčky pro nasazení webu a instalovat tyto balíčky na vzdálených serverech prostřednictvím jediného souboru projektu a jediného volání MSBuild. Můžete také volat jakékoli jiné spustitelné soubory jako součást procesu sestavení. Například můžete spustit nástroj příkazového řádku VSDBCMD. exe, který nasadí databázi ze souboru schématu. V průběhu tohoto tématu se dozvíte, jak můžete využít tyto možnosti pro splnění požadavků vašich scénářů podnikového nasazení.

> [!NOTE]
> Další informace o tom, jak funguje proces nasazení webové aplikace, najdete v tématu [Přehled nasazení projektu webové aplikace ASP.NET](https://msdn.microsoft.com/library/dd394698.aspx).

## <a name="the-anatomy-of-a-project-file"></a>Anatomie souboru projektu

Předtím, než se podíváte na proces sestavení podrobněji, se vám postará o seznámení se základní strukturou souboru projektu MSBuild. V této části najdete přehled častých prvků, které se zobrazí při kontrole, úpravách nebo vytváření souboru projektu. Konkrétně se naučíte:

- Jak používat *vlastnosti* pro správu proměnných pro proces sestavení.
- Jak použít *položky* k identifikaci vstupů do procesu sestavení, jako jsou soubory kódu.
- Jak používat *cíle* a *úkoly* k poskytnutí instrukcí pro provádění nástroje MSBuild pomocí *vlastností* a *položek* definovaných jinde v souboru projektu.

Zobrazuje vztah mezi klíčovými elementy v souboru projektu MSBuild:

![](understanding-the-project-file/_static/image2.png)

### <a name="the-project-element"></a>Prvek projektu

Prvek [projektu](https://msdn.microsoft.com/library/bcxfsh87.aspx) je kořenovým prvkem každého souboru projektu. Kromě určení schématu XML pro soubor projektu může prvek **projektu** obsahovat atributy pro určení vstupních bodů pro proces sestavení. Například v [ukázkovém řešení Contact Manager](the-contact-manager-solution.md)určuje soubor *Publish. proj* , že sestavení má začít voláním cíle s názvem **FullPublish**.

[!code-xml[Main](understanding-the-project-file/samples/sample1.xml)]

### <a name="properties-and-conditions"></a>Vlastnosti a podmínky

Soubor projektu obvykle potřebuje poskytnout spoustu různých informací, aby bylo možné úspěšně sestavit a nasadit vaše projekty. Tyto informace mohou zahrnovat názvy serverů, připojovací řetězce, přihlašovací údaje, konfigurace sestavení, cesty ke zdrojovým a cílovým souborům a jakékoli další informace, které chcete zahrnout do přizpůsobení podpory. V souboru projektu musí být vlastnosti definovány v rámci elementu [Property](https://msdn.microsoft.com/library/t4w159bs.aspx) . Vlastnosti nástroje MSBuild se skládají z párů klíč-hodnota. V rámci elementu **Property** element název elementu definuje klíč vlastnosti a obsah elementu definuje hodnotu vlastnosti. Můžete například definovat vlastnosti s názvem **servername** a **ConnectionString** k uložení názvu statického serveru a připojovacího řetězce.

[!code-xml[Main](understanding-the-project-file/samples/sample2.xml)]

Chcete-li načíst hodnotu vlastnosti, použijte formát *$ (propertyName)* . Pokud například chcete načíst hodnotu vlastnosti **servername** , zadejte:

[!code-powershell[Main](understanding-the-project-file/samples/sample3.ps1)]

> [!NOTE]
> V tomto tématu se zobrazí příklady a kdy použít hodnoty vlastností dále.

Vložení informací jako statických vlastností v souboru projektu není vždy ideálním přístupem ke správě procesu sestavení. V mnoha scénářích budete chtít získat informace z jiných zdrojů nebo uživateli poskytnout informace z příkazového řádku. Nástroj MSBuild umožňuje zadat jakoukoli hodnotu vlastnosti jako parametr příkazového řádku. Například uživatel může zadat hodnotu **servername** , když spustí soubor MSBuild. exe z příkazového řádku.

[!code-console[Main](understanding-the-project-file/samples/sample4.cmd)]

> [!NOTE]
> Další informace o argumentech a přepínačích, které lze použít s nástrojem MSBuild. exe, naleznete v tématu [Reference k příkazovému řádku MSBuild](https://msdn.microsoft.com/library/ms164311.aspx).

Můžete použít stejnou syntaxi vlastnosti pro získání hodnot proměnných prostředí a integrovaných vlastností projektu. Pro vás jsou definovány spousty běžně používaných vlastností a můžete je použít v souborech projektu včetně příslušného názvu parametru. &#x2014;Chcete-li například načíst aktuální platformu projektu, například **x86** nebo **AnyCpu**&#x2014;, můžete do souboru projektu zahrnout odkaz na vlastnost **$ (Platform)** . Další informace naleznete v tématu [makra pro příkazy a vlastnosti sestavení](https://msdn.microsoft.com/library/c02as0cs.aspx), [běžné vlastnosti projektu MSBuild](https://msdn.microsoft.com/library/bb629394.aspx)a [vyhrazené vlastnosti](https://msdn.microsoft.com/library/ms164309.aspx).

Vlastnosti se často používají ve spojení s *podmínkami*. Většina elementů MSBuild podporuje atribut **Condition** , který umožňuje zadat kritéria, na základě kterých má MSBuild prvek vyhodnotit. Zvažte například tuto definici vlastnosti:

[!code-xml[Main](understanding-the-project-file/samples/sample5.xml)]

Když nástroj MSBuild zpracuje tuto definici vlastnosti, nejprve zkontroluje, zda je k dispozici hodnota vlastnosti **$ (OutputRoot)** . Pokud je hodnota vlastnosti prázdná&#x2014;, uživateli se pro tuto vlastnost&#x2014;nezadala hodnota, podmínka se vyhodnotí jako **true** a hodnota vlastnosti je nastavená na **... \Publish\Out**. Pokud uživatel zadal hodnotu pro tuto vlastnost, podmínka se vyhodnotí jako **false** a hodnota statické vlastnosti se nepoužije.

Další informace o různých způsobech, jak můžete zadat podmínky, najdete v tématu [podmínky nástroje MSBuild](https://msdn.microsoft.com/library/7szfhaft.aspx).

### <a name="items-and-item-groups"></a>Položky a skupiny položek

Jednou z důležitých rolí souboru projektu je definování vstupů pro proces sestavení. Obvykle tyto vstupy jsou soubory&#x2014;kódu, konfigurační soubory, soubory příkazů a všechny další soubory, které potřebujete pro zpracování nebo kopírování v rámci procesu sestavení. Ve schématu projektu MSBuild jsou tyto vstupy reprezentovány prvky [Item](https://msdn.microsoft.com/library/ms164283.aspx) . V souboru projektu musí být položky definovány v rámci elementu [Item](https://msdn.microsoft.com/library/646dk05y.aspx) . Stejně jako prvky **vlastností** můžete pojmenovat prvek **položky** , například. Je však nutné zadat atribut **include** k identifikaci souboru nebo zástupného znaku, který položka představuje.

[!code-xml[Main](understanding-the-project-file/samples/sample6.xml)]

Zadáním více prvků **položky** se stejným názvem efektivně vytvoříte pojmenovaný seznam prostředků. Dobrým způsobem, jak to zobrazit v akci, je prohlédnout si jeden ze souborů projektu, které Visual Studio vytvoří. Například soubor *ContactManager. Mvc. csproj* v ukázkovém řešení obsahuje mnoho skupin položek, z nichž každý má několik identicky pojmenovaných prvků **Item** .

[!code-xml[Main](understanding-the-project-file/samples/sample7.xml)]

Tímto způsobem soubor projektu instruuje nástroj MSBuild, aby vytvořil seznam souborů, které je potřeba zpracovat stejným způsobem&#x2014;jako **odkaz** obsahuje sestavení, která musí být na místě pro úspěšné sestavení. seznam **kompilací** obsahuje kód. soubory, které je třeba zkompilovat, a seznam **obsahu** obsahuje prostředky, které je nutné zkopírovat beze změny. Podíváme se na to, jak proces sestavení odkazuje a používá tyto položky dále v tomto tématu.

Prvky položky mohou také zahrnovat podřízené elementy [ItemMetadata –](https://msdn.microsoft.com/library/ms164284.aspx) . Jsou to uživatelsky definované páry klíč-hodnota a v podstatě představují vlastnosti, které jsou specifické pro danou položku. Například velké množství prvků položky **kompilace** v souboru projektu zahrnuje podřízené elementy **DependentUpon** .

[!code-xml[Main](understanding-the-project-file/samples/sample8.xml)]

> [!NOTE]
> Kromě metadat položek vytvořených uživatelem jsou všechny položky při vytváření přiřazeny k různým běžným metadatům. Další informace najdete v tématu [známá metadata položek](https://msdn.microsoft.com/library/ms164313.aspx).

Můžete vytvořit prvky **Item** v rámci elementu **projektu** na kořenové úrovni nebo v rámci specifických **cílových** elementů. **Prvky pole** také podporují atributy **podmínky** , které umožňují přizpůsobit vstupy procesu sestavení podle podmínek, jako je například konfigurace projektu nebo platforma.

### <a name="targets-and-tasks"></a>Cíle a úkoly

Ve schématu MSBuild element [Task](https://msdn.microsoft.com/library/77f2hx1s.aspx) představuje individuální instrukci sestavení (nebo úkol). Nástroj MSBuild obsahuje velké množství předdefinovaných úloh. Příklad:

- Úloha **kopírování** kopíruje soubory do nového umístění.
- Úloha **CSC** vyvolá kompilátor vizuálu C# .
- Úloha **Vbc** vyvolá kompilátor Visual Basic.
- Úloha **exec** spustí zadaný program.
- Úloha **zprávy** zapíše zprávu do protokolovacího nástroje.

> [!NOTE]
> Úplné podrobnosti o úkolech, které jsou k dispozici v poli, naleznete v tématu [Reference k úloze MSBuild](https://msdn.microsoft.com/library/7z253716.aspx). Další informace o úlohách, včetně toho, jak vytvořit vlastní úkoly, najdete v tématu [úlohy nástroje MSBuild](https://msdn.microsoft.com/library/ms171466.aspx).

Úkoly musí být vždy obsaženy v rámci [cílových](https://msdn.microsoft.com/library/t50z2hka.aspx) elementů. **Cílový** element je sada jednoho nebo více úloh, které jsou spouštěny sekvenčně a soubor projektu může obsahovat více cílů. Pokud chcete spustit úlohu nebo sadu úkolů, vyvoláte cíl, který je obsahuje. Předpokládejme například, že máte jednoduchý soubor projektu, který zaznamená zprávu.

[!code-xml[Main](understanding-the-project-file/samples/sample9.xml)]

Cíl můžete vyvolat z příkazového řádku pomocí přepínače **/t** pro určení cíle.

[!code-console[Main](understanding-the-project-file/samples/sample10.cmd)]

Alternativně můžete přidat atribut **DefaultTargets –** do prvku **projektu** , chcete-li určit cíle, které chcete vyvolat.

[!code-xml[Main](understanding-the-project-file/samples/sample11.xml)]

V takovém případě nemusíte zadávat cíl z příkazového řádku. Můžete jednoduše zadat soubor projektu a nástroj MSBuild vyvolá cíl **FullPublish** za vás.

[!code-console[Main](understanding-the-project-file/samples/sample12.cmd)]

Atributy **podmínky** můžou zahrnovat i cíle i úkoly. V takovém případě můžete zvolit, že chcete vynechat všechny cíle nebo jednotlivé úkoly, pokud jsou splněny určité podmínky.

Obecně řečeno, když vytváříte užitečné úlohy a cíle, budete muset odkazovat na vlastnosti a položky, které jste definovali jinde v souboru projektu:

- Chcete-li použít hodnotu vlastnosti, zadejte **$ (***PropertyName***)** , kde *PropertyName* je název elementu **vlastnosti** nebo název parametru.
- Chcete-li použít položku, zadejte **@ (***Item***)** , kde *Item* je název elementu **Item** .

> [!NOTE]
> Pamatujte, že pokud vytvoříte více položek se stejným názvem, vytváříte seznam. Naopak pokud vytvoříte více vlastností se stejným názvem, přepíše hodnota poslední vlastnosti, kterou poskytnete, všechny předchozí vlastnosti se stejným názvem&#x2014;. vlastnost může obsahovat pouze jednu hodnotu.

Například v souboru *Publish. proj* v ukázkovém řešení si prohlédněte cíl **BuildProjects** .

[!code-xml[Main](understanding-the-project-file/samples/sample13.xml)]

V této ukázce můžete sledovat tyto klíčové body:

- Pokud je zadán parametr **BuildingInTeamBuild** a má hodnotu **true**, nebude provedena žádná z úloh v tomto cíli.
- Cíl obsahuje jednu instanci úlohy [MSBuild](https://msdn.microsoft.com/library/z7f65y0d.aspx) . Tato úloha umožňuje sestavit další projekty MSBuild.
- Položka **ProjectsToBuild** je předána úkolu. Tato položka může představovat seznam souborů projektu nebo řešení, které jsou definovány elementy **ProjectsToBuild** Item v rámci skupiny položek. V tomto případě položka **ProjectsToBuild** odkazuje na jeden soubor řešení.

    [!code-xml[Main](understanding-the-project-file/samples/sample14.xml)]
- Hodnoty vlastností předané do úlohy **MSBuild** obsahují parametry s názvem **OutputRoot** a **Konfigurace**. Ty jsou nastaveny na hodnoty parametrů, pokud jsou k dispozici, nebo hodnoty statických vlastností, pokud nejsou.

    [!code-xml[Main](understanding-the-project-file/samples/sample15.xml)]

Můžete také zjistit, že úloha **MSBuild** vyvolá cíl s názvem **Build**. Toto je jeden z několika předdefinovaných cílů, které se běžně používají v souborech projektu sady Visual Studio a jsou k dispozici ve vlastních souborech projektu, jako je **sestavení**, **Vyčištění**, **opětovné sestavení**a **publikování**. Přečtěte si další informace o použití cílů a úloh pro řízení procesu sestavení a o tom, co je potřeba pro úlohu **MSBuild** zejména v tomto tématu.

> [!NOTE]
> Další informace o cílech naleznete v tématu [cíle nástroje MSBuild](https://msdn.microsoft.com/library/ms171462.aspx).

## <a name="splitting-project-files-to-support-multiple-environments"></a>Rozdělování souborů projektu pro podporu více prostředí

Předpokládejme, že chcete být schopni nasadit řešení do více prostředí, jako jsou testovací servery, pracovní platformy a produkční prostředí. Konfigurace se může podstatně lišit mezi těmito prostředími&#x2014;, a to nejen z hlediska názvů serverů, připojovacích řetězců atd., ale také potenciálně z hlediska přihlašovacích údajů, nastavení zabezpečení a spousty dalších faktorů. Pokud to potřebujete udělat pravidelně, není ve skutečnosti vhodné upravovat více vlastností v souboru projektu pokaždé, když přepínáte cílové prostředí. Ani to není ideální řešení pro vyžadování nekonečné seznamu hodnot vlastností, které mají být poskytnuty procesu sestavení.

Naštěstí existuje alternativa. Nástroj MSBuild umožňuje rozdělit konfiguraci sestavení napříč více soubory projektu. Chcete-li zjistit, jak to funguje, v ukázkovém řešení si všimněte, že existují dva vlastní soubory projektu:

- *Publish. proj*, který obsahuje vlastnosti, položky a cíle, které jsou společné pro všechna prostředí.
- *ENV-dev. proj*obsahující vlastnosti, které jsou specifické pro vývojářské prostředí.

Nyní si všimněte, že soubor *Publish. proj* obsahuje prvek [Import](https://msdn.microsoft.com/library/92x05xfs.aspx) , který je bezprostředně pod otevírací značkou **projektu** .

[!code-xml[Main](understanding-the-project-file/samples/sample16.xml)]

Element **Import** slouží k importu obsahu jiného souboru projektu MSBuild do aktuálního souboru projektu MSBuild. V tomto případě parametr **TargetEnvPropsFile** poskytuje název souboru projektu, který chcete importovat. Můžete zadat hodnotu pro tento parametr při spuštění nástroje MSBuild.

[!code-console[Main](understanding-the-project-file/samples/sample17.cmd)]

Tím se efektivně sloučí obsah těchto dvou souborů do jediného souboru projektu. Pomocí tohoto přístupu můžete vytvořit jeden soubor projektu obsahující konfiguraci univerzálního sestavení a více doplňkových souborů projektu obsahující vlastnosti specifické pro prostředí. V důsledku toho stačí spustit příkaz s jinou hodnotou parametru, který umožňuje nasazení řešení do jiného prostředí.

![](understanding-the-project-file/_static/image3.png)

Rozdělení souborů projektu tímto způsobem je dobrý postup. Umožňuje vývojářům nasazovat do více prostředí spuštěním jediného příkazu, přičemž se vyhnete duplikování vlastností univerzálního sestavení napříč více soubory projektu.

> [!NOTE]
> Pokyny k přizpůsobení souborů projektu specifických pro prostředí pro vlastní serverová prostředí najdete v tématu [Konfigurace vlastností nasazení pro cílové prostředí](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).

## <a name="conclusion"></a>Závěr

Toto téma poskytuje obecné informace o souborech projektu MSBuild a vysvětluje, jak můžete vytvořit vlastní soubory projektu pro řízení procesu sestavení. Představil také koncept rozdělení souborů projektu na pokyny pro univerzální sestavení a vlastnosti sestavení specifické pro prostředí, které usnadňují sestavování a nasazování projektů do více cílů.

V dalším tématu [Principy procesu sestavení](understanding-the-build-process.md)poskytujeme další informace o tom, jak můžete použít soubory projektu k řízení sestavení a nasazení, a Projděte si nasazení řešení s realistickým stupněm složitosti.

## <a name="further-reading"></a>Další čtení

Podrobné seznámení se soubory projektu a WPP naleznete v části [uvnitř Microsoft Build Engine: použití nástroje MSBuild a Team Foundation Build](http://amzn.com/0735645248) podle Sayed Ibrahim Hashimi a William Bartholomew, ISBN: 978-0-7356-4524-0.

> [!div class="step-by-step"]
> [Předchozí](setting-up-the-contact-manager-solution.md)
> [Další](understanding-the-build-process.md)

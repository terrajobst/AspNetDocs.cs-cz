---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
title: 'Nasazení webové aplikace v ASP.NET s SQL Server Compact pomocí sady Visual Studio nebo Visual Web Developer: řešení potíží (12 z 12) | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 3fc23eed-921d-4d46-a610-a2d156e4bd03
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
msc.type: authoredcontent
ms.openlocfilehash: db8f58e3679e6dea865dadb6f64916032dd9f38c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74639865"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-troubleshooting-12-of-12"></a>Nasazení webové aplikace SQL Server Compact v ASP.NET s využitím sady Visual Studio nebo Visual Web Developer: řešení potíží (12 z 12)

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) projekt webové aplikace ASP.NET, který obsahuje databázi SQL Server Compact pomocí sady Visual Studio 2012 RC nebo Visual Studio Express 2012 RC pro web. Můžete také použít Visual Studio 2010, pokud nainstalujete aktualizaci publikování na webu. Úvod k řadě najdete v [prvním kurzu v řadě](deployment-to-a-hosting-provider-introduction-1-of-12.md).
> 
> Kurz, který ukazuje funkce nasazení představené po vydání RC sady Visual Studio 2012, ukazuje, jak nasadit jiné edice SQL Server než SQL Server Compact a ukazuje, jak nasadit na weby Windows Azure najdete v tématu [nasazení webu ASP.NET pomocí sady Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).

Tato stránka popisuje některé běžné problémy, které mohou nastat při nasazení webové aplikace ASP.NET pomocí sady Visual Studio. Jeden nebo více možných příčin a odpovídajících řešení jsou pro každý z nich k dispozici.

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a>Chyba serveru v '/' aplikace – aktuální vlastní nastavení chyb brání ve vzdáleném zobrazení podrobností o chybě

### <a name="scenario"></a>Scénář

Po nasazení lokality na vzdáleného hostitele obdržíte chybovou zprávu, která označuje nastavení customErrors v souboru Web. config, ale neindikuje, co je skutečná příčina chyby:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample1.cmd)]

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Ve výchozím nastavení ASP.NET zobrazuje podrobné informace o chybách pouze v případě, že je webová aplikace spuštěna v místním počítači. Obecně není vhodné zobrazovat podrobné informace o chybách, pokud je webová aplikace veřejně dostupná přes Internet, protože hackeři můžou pomocí těchto informací najít ohrožení zabezpečení v aplikaci. Pokud však nasazujete lokalitu nebo aktualizace lokality, někdy se něco pokazilo a potřebujete získat zprávu o skutečné chybové zprávě.

Chcete-li aplikaci povolit, aby při spuštění na vzdáleném hostiteli zobrazila podrobné chybové zprávy, upravte soubor Web. config a nastavte režim `customErrors` vypnutý, znovu nasaďte aplikaci a spusťte aplikaci znovu:

1. Pokud má soubor Web. config aplikace `customErrors` element v elementu `system.web`, změňte atribut `mode` na off. V opačném případě přidejte `customErrors` element v elementu `system.web` s atributem `mode` nastaveným na "off", jak je znázorněno v následujícím příkladu:

    [!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample2.xml?highlight=3)]
2. Nasaďte aplikaci.
3. Spusťte aplikaci a opakujte vše, co jste předtím způsobili, že došlo k chybě. Nyní vidíte, co je skutečná chybová zpráva.
4. Po vyřešení chyby obnovte původní nastavení `customErrors` a znovu nasaďte aplikaci.

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a>Přístup je odepřen na webové stránce, která používá SQL Server Compact

### <a name="scenario"></a>Scénář

Když nasadíte lokalitu, která používá SQL Server Compact, a spustíte stránku v nasazeném webu, která přistupuje k databázi, zobrazí se tato chybová zpráva:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Účet síťové služby na serveru musí být schopný číst komprimaci nativních binárních souborů služby SQL, které jsou ve složce *bin\amd64* nebo *bin\x86* , ale nemá oprávnění ke čtení těchto složek. Nastavte oprávnění ke čtení pro síťovou službu ve složce *bin* a ujistěte se, že jste rozšířili oprávnění na podsložky.

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a>Konfigurační soubor nelze přečíst z důvodu nedostatečných oprávnění.

### <a name="scenario"></a>Scénář

Když kliknete na tlačítko publikovat v aplikaci Visual Studio a nasadíte aplikaci do služby IIS na místním počítači, publikování se nezdařila a v okně **výstup** se zobrazí chybová zpráva podobná této:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample4.cmd)]

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Chcete-li použít publikování jedním kliknutím na službu IIS na místním počítači, je nutné spustit aplikaci Visual Studio s oprávněními správce. Zavřete Visual Studio a restartujte ho s oprávněními správce.

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a>Nepovedlo se připojit k cílovému počítači... Pomocí zadaného procesu

### <a name="scenario"></a>Scénář

Když kliknete na tlačítko publikovat v aplikaci Visual Studio pro nasazení aplikace, publikování se nezdařilo a okno **výstup** zobrazuje chybovou zprávu podobnou této:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample5.cmd)]

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Proxy server přerušuje komunikaci s cílovým serverem. V Ovládacích panelech systému Windows nebo v aplikaci Internet Explorer vyberte možnost **Možnosti Internetu** a vyberte kartu **připojení** . V dialogovém okně **Vlastnosti Internetu** klikněte na **Nastavení místní sítě**. V dialogovém okně **Nastavení místní sítě (LAN)** zrušte zaškrtnutí políčka **automaticky zjišťovat nastavení** . Pak znovu klikněte na tlačítko publikovat.

Pokud potíže potrvají, obraťte se na správce systému a zjistěte, co se dá udělat s nastavením proxy serveru nebo brány firewall. K tomuto problému dochází, protože Nasazení webu používá nestandardní port pro nasazení služby webové správy (8172); pro další připojení Nasazení webu používá port 80. Pokud nasazujete pro poskytovatele hostingu třetí strany, obvykle používáte službu webové správy.

## <a name="default-net-40-application-pool-does-not-exist"></a>Výchozí fond aplikací .NET 4,0 neexistuje.

### <a name="scenario"></a>Scénář

Když nasadíte aplikaci, která vyžaduje .NET Framework 4, zobrazí se tato chybová zpráva:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample6.cmd)]

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Ve službě IIS není nainstalován ASP.NET 4. Pokud je server, na který nasazujete, váš vývojový počítač a je na něm nainstalovaná aplikace Visual Studio 2010, v počítači je nainstalovaná služba ASP.NET 4, ale možná není nainstalovaná ve službě IIS. Na serveru, na který nasazujete, otevřete příkazový řádek se zvýšenými oprávněními a nainstalujte ASP.NET 4 do služby IIS spuštěním následujících příkazů:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample7.cmd)]

Je také možné, že bude nutné ručně nastavit .NET Framework verzi výchozího fondu aplikací. Další informace najdete v kurzu [nasazení do služby IIS jako testovací prostředí](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) .

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a>Formát inicializačního řetězce nevyhovuje specifikaci počínaje indexem 0.

### <a name="scenario"></a>Scénář

Po nasazení aplikace pomocí publikování jedním kliknutím spustíte stránku, která přistupuje k databázi, a zobrazí se tato chybová zpráva:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample8.cmd)]

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Otevřete soubor *Web. config* v nasazené lokalitě a zkontrolujte, zda jsou hodnoty připojovacího řetězce začínat `$(ReplaceableToken_`, jako v následujícím příkladu:

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample9.xml)]

Pokud připojovací řetězce vypadají jako v tomto příkladu, upravte soubor projektu a přidejte následující vlastnost do prvku `PropertyGroup`, který je pro všechny konfigurace sestavení:

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample10.xml)]

Pak aplikaci znovu nasaďte.

## <a name="http-500-internal-server-error"></a>Chyba interního serveru HTTP 500

### <a name="scenario"></a>Scénář

Při spuštění nasazené lokality se zobrazí následující chybová zpráva bez konkrétních informací, které označují příčinu chyby:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample11.cmd)]

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

K dispozici je mnoho příčin 500 chyb, ale příčinou může být to, že pokud budete postupovat podle těchto kurzů, je třeba vložit element XML na nesprávné místo v jednom z transformačních souborů XML. Tato chyba se například zobrazí, pokud vložíte transformaci, která vloží prvek `<location>` v části `<system.web>` namísto přímo pod `<configuration>`. Řešením v takovém případě je opravit transformační soubor XML a znovu nasadit.

## <a name="http-50021-internal-server-error"></a>Chyba interního serveru HTTP 500,21

### <a name="scenario"></a>Scénář

Když spustíte nasazenou lokalitu, zobrazí se následující chybová zpráva:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample12.cmd)]

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Lokalita, kterou jste nasadili, ASP.NET 4, ale ASP.NET 4 není zaregistrovaná ve službě IIS na serveru. Na serveru otevřete příkazový řádek se zvýšenými oprávněními a zaregistrujte ASP.NET 4 spuštěním následujících příkazů:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample13.cmd)]

Je také možné, že bude nutné ručně nastavit .NET Framework verzi výchozího fondu aplikací. Další informace najdete v kurzu [nasazení do služby IIS jako testovací prostředí](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md) .

## <a name="login-failed-opening-sql-server-express-database-in-app_data"></a>Přihlášení selhalo při otevírání databáze SQL Server Express v\_data aplikace.

### <a name="scenario"></a>Scénář

Aktualizovali jste připojovací řetězec souboru *Web. config* tak, aby odkazoval na databázi SQL Server Express jako soubor *. mdf* ve složce *aplikace\_data* a při prvním spuštění aplikace se zobrazí následující chybová zpráva:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample14.cmd)]

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Název souboru *. mdf* se nemůže shodovat s názvem žádné SQL Server Express databáze, která v počítači existovala dříve, i když jste odstranili soubor *. mdf* dříve existující databáze. Změňte název souboru *. mdf* na název, který se nikdy nepoužil jako název databáze, a změňte soubor *Web. config* tak, aby používal nový název. Alternativně můžete pomocí [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) odstranit dříve existující databáze SQL Server Express.

## <a name="model-compatibility-cannot-be-checked"></a>Nejde zkontrolovat kompatibilitu modelů.

### <a name="scenario"></a>Scénář

Aktualizovali jste připojovací řetězec souboru *Web. config* tak, aby odkazoval na novou SQL Server Express databázi a při prvním spuštění aplikace se zobrazí následující chybová zpráva:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample15.cmd)]

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Pokud se název databáze, který jste umístili do souboru Web. config, předtím používal v počítači, může databáze již existovat s některými tabulkami. Vyberte nový název, který nebyl dříve použit na vašem počítači, a změňte soubor *Web. config* tak, aby odkazoval na použití tohoto nového názvu databáze. Alternativně můžete pomocí [nástroje SQL Server Express](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990) nebo [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) odstranit stávající databázi.

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a>Chyba SQL, když se skript pokusí vytvořit uživatele nebo role

### <a name="scenario"></a>Scénář

Používáte nasazení databáze nakonfigurované na kartě **balíček/publikovat SQL** , skripty SQL, které se spouštějí během nasazení, zahrnují příkazy CREATE USER nebo Create role a spuštění skriptu se v případě provedení těchto příkazů nezdařilo. Může se zobrazit podrobnější zpráva, například následující:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample16.cmd)]

Pokud k této chybě dojde, pokud jste nakonfigurovali nasazení databáze v průvodci **publikováním webu** , nikoli na kartě **Package/Publish SQL** , vytvořte vlákno ve fóru [Konfigurace a nasazení](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) a řešení se přidá do této stránky pro odstraňování potíží.

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Uživatelský účet, který používáte k provádění nasazení, nemá oprávnění k vytváření uživatelů nebo rolí. Například hostující společnost může přiřadit role `db_datareader`, `db_datawriter`a `db_ddladmin` k uživatelskému účtu, který pro vás nastaví. Ty jsou dostačující pro vytváření většiny databázových objektů, ale ne pro vytváření uživatelů nebo rolí. Jedním ze způsobů, jak se vyhnout chybě, je vyloučení uživatelů a rolí z nasazení databáze. To lze provést úpravou prvku `PreSource` pro automaticky generovaný skript databáze, aby obsahoval následující atributy:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample17.cmd)]

Informace o tom, jak upravit prvek `PreSource` v souboru projektu, naleznete v tématu [How to: Edit nastavení nasazení v souboru projektu](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx). Pokud se uživatelé nebo role ve vaší vývojové databázi musí nacházet v cílové databázi, požádejte o pomoc svého poskytovatele hostingu.

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a>Chyba časového limitu SQL Server při spouštění vlastních skriptů během nasazení

### <a name="scenario"></a>Scénář

Zadali jste vlastní skripty SQL, které se spustí během nasazení, a když je Nasazení webu spustí, vyprší časový limit.

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Spuštění více skriptů, které mají různé režimy transakce, může způsobit chyby s časovým limitem. Ve výchozím nastavení se automaticky generované skripty spouštějí v transakci, ale vlastní skripty ne. Pokud na kartě **Package/PUBLISH SQL** vyberete možnost získat **data nebo schéma z existující databáze** a přidáte vlastní skript SQL, je nutné změnit nastavení transakce na některých skriptech, aby všechny skripty používaly stejné nastavení transakce. Další informace najdete v tématu [Postup: nasazení databáze pomocí projektu webové aplikace](https://msdn.microsoft.com/library/dd465343.aspx).

Pokud jste nakonfigurovali nastavení transakce tak, aby vše bylo stejné, ale stále se tato chyba zobrazila, možná alternativní řešení je spouštět samostatně. V mřížce **databázové skripty** na kartě **Package/Publish** SQL zrušte zaškrtnutí políčka **Zahrnout** pro skript, který způsobí chybu časového limitu, a pak projekt publikujte. Pak se vraťte do mřížky **databázové skripty** , zaškrtněte políčko **Zahrnout** do tohoto skriptu a zrušte zaškrtnutí políček **Zahrnout** pro ostatní skripty. Pak projekt znovu publikujte. Tentokrát při publikování se spustí pouze vybraný vlastní skript.

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a>Data datového proudu manifestu webového serveru ještě nejsou k dispozici.

### <a name="scenario"></a>Scénář

Při instalaci balíčku pomocí souboru *Deploy. cmd* s možností `t` (test) se zobrazí následující chybová zpráva:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample18.cmd)]

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Chybová zpráva znamená, že příkaz nemůže vytvořit testovací sestavu. Příkaz se ale může spustit, pokud použijete možnost `y` (vlastní instalace). Zpráva indikuje pouze, že došlo k potížím s spuštěním příkazu v režimu testu.

## <a name="this-application-requires-managedruntimeversion-v40"></a>Tato aplikace vyžaduje ManagedRuntimeVersion v 4.0.

### <a name="scenario"></a>Scénář

Při pokusu o nasazení se zobrazí následující chybová zpráva:

 Chyba: streamovaná data typu ' sitemanifest/dbFullSql [@path= ' C:\TEMP\AdventureWorksGrant.sql ']/sqlScript ' ještě nejsou k dispozici. Fond aplikací, který se pokoušíte použít, má vlastnost ' managedRuntimeVersion ' nastavenou na hodnotu ' v 2.0 '. Tato aplikace vyžaduje: v 4.0. 

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Ve službě IIS není nainstalován ASP.NET 4. Pokud je server, na který nasazujete, váš vývojový počítač a je na něm nainstalovaná aplikace Visual Studio 2010, v počítači je nainstalovaná služba ASP.NET 4, ale možná není nainstalovaná ve službě IIS. Na serveru, na který nasazujete, otevřete příkazový řádek se zvýšenými oprávněními a nainstalujte ASP.NET 4 do služby IIS spuštěním následujících příkazů:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample19.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a>Microsoft. Web. Deployment. DeploymentProviderOptions se nedá přetypovat.

### <a name="scenario"></a>Scénář

Při nasazení balíčku se zobrazí následující chybová zpráva:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample20.cmd)]

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Pokoušíte se o nasazení ze Správce služby IIS pomocí uživatelského rozhraní Nasazení webu 1,1 na server s nainstalovanou Nasazení webu 2,0. Pokud pomocí nástroje pro vzdálenou správu služby IIS nasazujete Import balíčku, při navázání připojení zaškrtněte dialogové okno **nové funkce k dispozici** . (Toto dialogové okno může být zobrazeno pouze jednou při prvním navázání připojení. Pokud chcete vymazat připojení a začít znovu, zavřete Správce služby IIS a znovu ho spusťte zadáním `inetmgr /reset` na příkazovém řádku.) Pokud je jedna z uvedených funkcí **nasazení webu uživatelské rozhraní**a má číslo verze nižší než 8, server, na který nasazujete, může mít nainstalovanou Nasazení webu verze 1,1 a 2,0. Pokud chcete nasadit z klienta, který má nainstalovaný 2,0, musí mít server nainstalovanou jenom Nasazení webu 2,0. Pokud chcete tento problém vyřešit, budete muset kontaktovat svého poskytovatele hostingu.

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a>Nelze načíst nativní součásti SQL Server Compact

### <a name="scenario"></a>Scénář

Když spustíte nasazenou lokalitu, zobrazí se následující chybová zpráva:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample21.cmd)]

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Nasazený web nemá podsložky *amd64* a *x86* s nativními sestaveními ve složce *bin* aplikace. V počítači, který má nainstalované SQL Server Compact, jsou nativní sestavení umístěná ve *složce C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*. Nejlepším způsobem, jak získat správné soubory do správných složek v projektu sady Visual Studio, je instalace balíčku NuGet SqlServerCompact. Instalace balíčku přidá skript po sestavení ke zkopírování nativních sestavení do *amd64* a *x86*. Aby je bylo možné nasadit, je však nutné je ručně zahrnout do projektu. Další informace najdete v kurzu [nasazení SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) .

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a>Po nasazení Code First aplikace Entity Framework se chyba cesta není platná.

### <a name="scenario"></a>Scénář

Nasadíte aplikaci, která používá Migrace Entity Framework Code First, a systém DBMS, jako je například SQL Server Compact, který ukládá svou databázi do souboru ve složce aplikace\_data. Po vašem prvním nasazení máte Migrace Code First nakonfigurovanou k vytvoření databáze. Při spuštění aplikace se zobrazí chybová zpráva podobná následujícímu příkladu:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample22.cmd)]

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Code First se pokouší vytvořit databázi, ale složka\_data App neexistuje. Buď nemáte žádné soubory ve složce *\_dat* , když jste nasadili, nebo jste na kartě **Balení/publikování webu** okna **vlastností projektu** vybrali možnost **vyloučit\_data aplikace** . Proces nasazení nevytvoří složku na serveru, pokud ve složce nejsou žádné soubory, které se mají zkopírovat na server. Pokud jste již v lokalitě nastavili databázi, proces nasazení je odstraní a *aplikace\_data* samotné složky, pokud jste v profilu publikování vybrali možnost **odebrat další soubory v cílovém umístění** . Pokud chcete tento problém vyřešit, vložte do složky *App\_data* zástupný soubor, jako je soubor. txt, a ujistěte se, že jste vybrali možnost **vyloučit\_data aplikace** a znovu nasadit. 

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a>Objekt COM, který je oddělený od jeho podkladového RCW, nelze použít.

### <a name="scenario"></a>Scénář

Úspěšně jste pomocí publikování jedním kliknutím nasadili aplikaci a pak jste tuto chybu začali používat:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample23.cmd)]

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Pro vyřešení této chyby je obvykle potřeba zavřít a restartovat aplikaci Visual Studio.

## <a name="deployment-fails-because-user-credentials-used-for-publishing-dont-have-setacl-authority"></a>Nasazení se nepovedlo, protože přihlašovací údaje použité k publikování nemají setACL autoritu.

### <a name="scenario"></a>Scénář

Publikování se nepovede s chybou, která indikuje, že nemáte oprávnění k nastavení oprávnění ke složkám (uživatelský účet, který používáte, nemá autoritu setACL).

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Ve výchozím nastavení sada Visual Studio nastaví oprávnění ke čtení pro kořenovou složku webu a oprávnění k zápisu do složky\_dat aplikace. Pokud víte, že výchozí oprávnění pro složky webu jsou správná a není nutné je nastavit, toto chování zakážete přidáním **&lt;cíle IncludeSetACLProviderOn&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** do souboru profilu publikování (aby to ovlivnilo jeden profil) nebo do souboru WPP. TARGETS (aby ovlivnil všechny profily). Informace o tom, jak tyto soubory upravit, najdete v tématu [Postupy: Úprava nastavení nasazení v souborech profilu (. pubxml)](https://msdn.microsoft.com/library/ff398069.aspx). 

## <a name="access-denied-errors-when-the-application-tries-to-write-to-an-application-folder"></a>Když se aplikace pokusí zapisovat do složky aplikace, dojde k chybám odepření přístupu.

### <a name="scenario"></a>Scénář

Chyby aplikace, když se pokusí vytvořit nebo upravit soubor v jedné ze složek aplikace, protože nemá pro tuto složku oprávnění pro zápis.

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Ve výchozím nastavení sada Visual Studio nastaví oprávnění ke čtení pro kořenovou složku webu a oprávnění k zápisu do složky\_dat aplikace. Pokud vaše aplikace potřebuje přístup pro zápis do podsložky, můžete nastavit oprávnění pro tuto složku, jak je znázorněno v části [Nastavení oprávnění složky](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md) a [nasazení do kurzů produkčního prostředí](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) . Pokud vaše aplikace potřebuje oprávnění k zápisu do kořenové složky lokality, je třeba zabránit tomu, aby v kořenové složce nastavila přístup jen pro čtení, a to tak, že do souboru profilu publikování přidáte **&lt;umístění IncludeSetACLProviderOn&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** (pro ovlivnění jednoho profilu) nebo do souboru WPP. TARGETS (aby to ovlivnilo všechny profily). Informace o tom, jak tyto soubory upravit, najdete v tématu [Postupy: Úprava nastavení nasazení v souborech profilu (. pubxml)](https://msdn.microsoft.com/library/ff398069.aspx). <a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a>Chyba konfigurace – atribut targetFramework odkazuje na verzi, která je novější než nainstalovaná verze .NET Framework

### <a name="scenario"></a>Scénář

Úspěšně jste publikovali webový projekt, který se zaměřuje na ASP.NET 4,5, ale při spuštění aplikace (s režimem `customErrors` nastaveným na off v souboru Web. config) se zobrazí následující chyba:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample24.cmd)]

Zdrojové chybové pole chybové stránky zvýrazní následující řádek ze souboru Web. config, protože by došlo k chybě:

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample25.cmd)]

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Server nepodporuje ASP.NET 4,5. Obraťte se na poskytovatele hostingu a zjistěte, kdy a kde je možné přidat podporu pro ASP.NET 4,5. Pokud upgrade serveru není možnost, je nutné nasadit webový projekt, který cílí na ASP.NET 4 nebo starší místo. Pokud nasadíte webový projekt ASP.NET 4 nebo starší do stejného místa, zaškrtněte políčko **odebrat další soubory v cílovém umístění** na kartě **Nastavení** průvodce **Publikovat web** . Pokud nevyberete možnost **odebrat další soubory v cílovém umístění**, budete mít i nadále k dispozici stránku Chyba konfigurace.

Okna **vlastností** projektu obsahují rozevírací seznam cílové rozhraní, ale tento problém nemůžete vyřešit pouhou změnou tohoto problému z **.NET Framework 4,5** na **.NET Framework 4**. Pokud změníte cílovou architekturu na dřívější verzi rozhraní, projekt bude mít stále odkazy na sestavení verze novějšího rozhraní a nebude spuštěn. Je nutné ručně změnit tyto odkazy nebo vytvořit nový projekt, který se zaměřuje na .NET Framework 4 nebo starší. Další informace najdete v tématu [.NET Framework cílení na weby](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx).

> [!div class="step-by-step"]
> [Předchozí](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)

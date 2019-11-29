---
uid: web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting
title: 'Nasazení webu ASP.NET pomocí sady Visual Studio: řešení potíží | Microsoft Docs'
author: tdykstra
description: V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která bude Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí usin...
ms.author: riande
ms.date: 06/01/2015
ms.assetid: c0090595-ab3b-4b9b-9e16-7a1891e8cb2f
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: b42476fca18b04f4557a216ee205cfd9220023e8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74623576"
---
# <a name="aspnet-web-deployment-using-visual-studio-troubleshooting"></a>Nasazení webu ASP.NET pomocí sady Visual Studio: řešení potíží

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout počáteční projekt](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> V této sérii kurzů se dozvíte, jak nasadit (publikovat) webovou aplikaci ASP.NET, která umožňuje Azure App Service Web Apps nebo poskytovateli hostingu třetí strany, pomocí sady Visual Studio 2012 nebo Visual Studio 2010. Informace o řadě najdete v [prvním kurzu v řadě](introduction.md).

Tato stránka popisuje některé běžné problémy, které mohou nastat při nasazení webové aplikace ASP.NET pomocí sady Visual Studio. Jeden nebo více možných příčin a odpovídajících řešení jsou pro každý z nich k dispozici.

Uvedené scénáře platí pro poskytovatele hostingu Azure i od jiných výrobců. Další informace o řešení potíží s webovými aplikacemi v Azure App Service najdete v následujících zdrojích informací:

- [Řešení potíží s webovou aplikací v Azure App Service pomocí sady Visual Studio](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-troubleshoot-visual-studio/)
- [Monitorování Web Apps v Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-monitor//)
- [Oznamujeme vydání verze Windows Azure SDK 2,0 pro .NET](http://https://weblogs.asp.net/scottgu/announcing-the-release-of-windows-azure-sdk-2-0-for-net) (blog pro ScottGu), kde se dozvíte, jak získat diagnostické protokoly v sadě Visual Studio.

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a>Chyba serveru v '/' aplikace – aktuální vlastní nastavení chyb brání ve vzdáleném zobrazení podrobností o chybě

### <a name="scenario"></a>Scénář

Po nasazení lokality na vzdáleného hostitele obdržíte chybovou zprávu, která označuje nastavení customErrors v souboru Web. config, ale neindikuje, co je skutečná příčina chyby:

[!code-xml[Main](troubleshooting/samples/sample1.xml)]

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Ve výchozím nastavení ASP.NET zobrazuje podrobné informace o chybách pouze v případě, že je webová aplikace spuštěna v místním počítači. Obecně není vhodné zobrazovat podrobné informace o chybách, pokud je webová aplikace veřejně dostupná přes Internet, protože hackeři můžou pomocí těchto informací najít ohrožení zabezpečení v aplikaci. Pokud však nasazujete lokalitu nebo aktualizace lokality, někdy se něco pokazilo a potřebujete získat zprávu o skutečné chybové zprávě.

Chcete-li aplikaci povolit, aby při spuštění na vzdáleném hostiteli zobrazovala podrobné chybové zprávy, upravte soubor Web. config tak, aby byl režim customErrors vypnutý, znovu nasaďte aplikaci a spusťte aplikaci znovu:

1. Pokud má soubor Web. config aplikace v prvku System. Web prvek customErrors, změňte atribut Mode na hodnotu OFF. V opačném případě přidejte prvek customErrors do prvku System. Web s atributem mode nastaveným na "off", jak je znázorněno v následujícím příkladu: 

    [!code-xml[Main](troubleshooting/samples/sample2.xml)]
2. Nasaďte aplikaci.
3. Spusťte aplikaci a opakujte vše, co jste předtím způsobili, že došlo k chybě. Nyní vidíte, co je skutečná chybová zpráva.
4. Po vyřešení chyby obnovte původní nastavení customErrors a aplikaci znovu nasaďte.

## <a name="cannot-createshadow-copy-contosouniversity-when-that-file-already-exists"></a>Nelze vytvořit nebo stínovou kopii ' ContosoUniversity ', pokud tento soubor již existuje.

### <a name="scenario"></a>Scénář

Při pokusu o spuštění projektu v aplikaci Visual Studio se zobrazí chybová stránka se zprávou jako v následujícím příkladu:

Chyba serveru v aplikaci/ Nelze vytvořit nebo stínovou kopii ' ContosoUniversity ', pokud tento soubor již existuje.

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Počkejte minutu a aktualizujte prohlížeč, nebo znovu zkompilujte web a zkuste ho spustit znovu.

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a>Přístup je odepřen na webové stránce, která používá SQL Server Compact

### <a name="scenario"></a>Scénář

Když nasadíte lokalitu, která používá SQL Server Compact, a spustíte stránku v nasazeném webu, která přistupuje k databázi, zobrazí se tato chybová zpráva:

Přístup byl zamítnut. (Výjimka z HRESULT: 0x80070005 (E\_ACCESSDENIED))

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Účet síťové služby na serveru musí být schopný číst komprimaci nativních binárních souborů služby SQL, které jsou ve složce *bin\amd64* nebo *bin\x86* , ale nemá oprávnění ke čtení těchto složek. Nastavte oprávnění ke čtení pro síťovou službu ve složce *bin* a ujistěte se, že jste rozšířili oprávnění na podsložky.

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a>Konfigurační soubor nelze přečíst z důvodu nedostatečných oprávnění.

### <a name="scenario"></a>Scénář

Když kliknete na tlačítko publikovat v aplikaci Visual Studio a nasadíte aplikaci do služby IIS na místním počítači, publikování se nezdařila a v okně **výstup** se zobrazí chybová zpráva podobná této:

Při čtení konfiguračního souboru služby IIS ' počítač/přesměrování ' došlo k chybě. Identita, která provádí tuto operaci, byla... Chyba: konfigurační soubor nelze přečíst z důvodu nedostatečných oprávnění.

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Chcete-li použít publikování jedním kliknutím na službu IIS na místním počítači, je nutné spustit aplikaci Visual Studio s oprávněními správce. Zavřete Visual Studio a restartujte ho s oprávněními správce.

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a>Nepovedlo se připojit k cílovému počítači... Pomocí zadaného procesu

### <a name="scenario"></a>Scénář

Když kliknete na tlačítko publikovat v aplikaci Visual Studio pro nasazení aplikace, publikování se nezdařilo a okno **výstup** zobrazuje chybovou zprávu podobnou této:

[!code-console[Main](troubleshooting/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Proxy server přerušuje komunikaci s cílovým serverem. V Ovládacích panelech systému Windows nebo v aplikaci Internet Explorer vyberte možnost **Možnosti Internetu** a vyberte kartu **připojení** . V dialogovém okně **Vlastnosti Internetu** klikněte na **Nastavení místní sítě**. V dialogovém okně **Nastavení místní sítě (LAN)** zrušte zaškrtnutí políčka **automaticky zjišťovat nastavení** . Pak znovu klikněte na tlačítko publikovat.

Pokud potíže potrvají, obraťte se na správce systému a zjistěte, co se dá udělat s nastavením proxy serveru nebo brány firewall. K tomuto problému dochází, protože Nasazení webu používá nestandardní port pro nasazení služby webové správy (8172); pro další připojení Nasazení webu používá port 80. Pokud nasazujete pro poskytovatele hostingu třetí strany, obvykle používáte službu webové správy.

## <a name="default-net-40-application-pool-does-not-exist"></a>Výchozí fond aplikací .NET 4,0 neexistuje.

### <a name="scenario"></a>Scénář

Když nasadíte aplikaci, která vyžaduje .NET Framework 4, zobrazí se tato chybová zpráva:

Výchozí fond aplikací .NET 4,0 neexistuje nebo aplikaci nelze přidat. Ověřte prosím, že na tomto počítači je nainstalovaná ASP.NET 4,0.

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Ve službě IIS není nainstalován ASP.NET 4. Pokud je server, na který nasazujete, váš vývojový počítač a je na něm nainstalovaná aplikace Visual Studio 2010, v počítači je nainstalovaná služba ASP.NET 4, ale možná není nainstalovaná ve službě IIS. Na serveru, na který nasazujete, otevřete příkazový řádek se zvýšenými oprávněními a nainstalujte ASP.NET 4 do služby IIS spuštěním následujících příkazů:

[!code-console[Main](troubleshooting/samples/sample4.cmd)]

Je také možné, že bude nutné ručně nastavit .NET Framework verzi výchozího fondu aplikací. Další informace najdete v kurzu nasazení do služby IIS jako kurz testovacího prostředí v této sérii.

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a>Formát inicializačního řetězce nevyhovuje specifikaci počínaje indexem 0.

### <a name="scenario"></a>Scénář

Po nasazení aplikace pomocí publikování jedním kliknutím spustíte stránku, která přistupuje k databázi, a zobrazí se tato chybová zpráva:

Formát inicializačního řetězce nevyhovuje specifikaci počínaje indexem 0.

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Otevřete soubor *Web. config* v nasazené lokalitě a zkontrolujte, zda jsou hodnoty připojovacího řetězce začínat `$(ReplaceableToken_`, jako v následujícím příkladu:

[!code-xml[Main](troubleshooting/samples/sample5.xml)]

Pokud připojovací řetězce vypadají jako v tomto příkladu, upravte soubor projektu a přidejte následující vlastnost do prvku skupiny vlastností, který je pro všechny konfigurace sestavení:

[!code-xml[Main](troubleshooting/samples/sample6.xml)]

Pak aplikaci znovu nasaďte.

## <a name="http-500-internal-server-error"></a>Chyba interního serveru HTTP 500

### <a name="scenario"></a>Scénář

Při spuštění nasazené lokality se zobrazí následující chybová zpráva bez konkrétních informací, které označují příčinu chyby:

Chyba protokolu HTTP 500 – došlo k vnitřní chybě serveru.

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

K dispozici je mnoho příčin 500 chyb, ale jedna z možných příčin je, že v případě, že budete postupovat podle těchto kurzů, vložíte element XML na nesprávné místo v jednom z transformačních souborů Web. config. Tato chyba se například zobrazí, pokud vložíte transformaci, která vloží &lt;umístění&gt; elementu v &lt;System. Web&gt; místo přímo v části &lt;konfigurace&gt;. Pomocí funkce Web. config Transform Preview můžete ověřit, že transformace fungují tak, jak mají. Řešení Pokud najdete transformaci, která byla nesprávně kódována, je třeba opravit transformační soubor a znovu nasadit. Pokud chyba není zjevná, zkuste transformovat a znovu nasadit, abyste zjistili, která z nich způsobuje chybu 500.

## <a name="http-50021-internal-server-error"></a>Chyba interního serveru HTTP 500,21

### <a name="scenario"></a>Scénář

Když spustíte nasazenou lokalitu, zobrazí se následující chybová zpráva:

Chyba protokolu HTTP 500,21 – došlo k vnitřní chybě serveru. Obslužná rutina "PageHandlerFactory-Integrated" má v seznamu modulů špatný modul "ManagedPipelineHandler".

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Lokalita, kterou jste nasadili, ASP.NET 4, ale ASP.NET 4 není zaregistrovaná ve službě IIS na serveru. Na serveru otevřete příkazový řádek se zvýšenými oprávněními a zaregistrujte ASP.NET 4 spuštěním následujících příkazů:

[!code-console[Main](troubleshooting/samples/sample7.cmd)]

Je také možné, že bude nutné ručně nastavit .NET Framework verzi výchozího fondu aplikací. Další informace najdete v kurzu nasazení do služby IIS jako kurz testovacího prostředí v této sérii.

## <a name="login-failed-opening-sql-server-express-database-in-app_data"></a>Přihlášení selhalo při otevírání databáze SQL Server Express v\_data aplikace.

### <a name="scenario"></a>Scénář

Aktualizovali jste připojovací řetězec souboru *Web. config* tak, aby odkazoval na databázi SQL Server Express jako soubor *. mdf* ve složce *aplikace\_data* a při prvním spuštění aplikace se zobrazí následující chybová zpráva:

System. data. SqlClient. SqlException: Nelze otevřít databázi DatabaseName požadovanou pro přihlášení. Přihlášení se nezdařilo.

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Název souboru *. mdf* se nemůže shodovat s názvem žádné SQL Server Express databáze, která v počítači existovala dříve, i když jste odstranili soubor *. mdf* dříve existující databáze. Změňte název souboru *. mdf* na název, který se nikdy nepoužil jako název databáze, a změňte soubor *Web. config* tak, aby používal nový název. Alternativně můžete pomocí [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) odstranit dříve existující databáze SQL Server Express.

## <a name="model-compatibility-cannot-be-checked"></a>Nejde zkontrolovat kompatibilitu modelů.

### <a name="scenario"></a>Scénář

Aktualizovali jste připojovací řetězec souboru *Web. config* tak, aby odkazoval na novou SQL Server Express databázi a při prvním spuštění aplikace se zobrazí následující chybová zpráva:

Kompatibilita modelů nejde zkontrolovat, protože databáze neobsahuje metadata modelu. Zajistěte, aby se IncludeMetadataConvention přidal do konvencí DbModelBuilder.

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Pokud se název databáze, který jste umístili do souboru Web. config, předtím používal v počítači, může databáze již existovat s některými tabulkami. Vyberte nový název, který nebyl dříve použit na vašem počítači, a změňte soubor *Web. config* tak, aby odkazoval na použití tohoto nového názvu databáze. Alternativně můžete pomocí [nástroje SQL Server Express](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990) nebo [SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593) odstranit stávající databázi.

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a>Chyba SQL, když se skript pokusí vytvořit uživatele nebo role

### <a name="scenario"></a>Scénář

Používáte nasazení databáze nakonfigurované na kartě **balíček/publikovat SQL** , skripty SQL, které se spouštějí během nasazení, zahrnují příkazy CREATE USER nebo Create role a spuštění skriptu se v případě provedení těchto příkazů nezdařilo. Může se zobrazit podrobnější zpráva, například následující:

[!code-console[Main](troubleshooting/samples/sample8.cmd)]

Pokud k této chybě dojde, pokud jste nakonfigurovali nasazení databáze v průvodci **publikováním webu** , nikoli na kartě **Package/Publish SQL** , vytvořte vlákno ve fóru [Konfigurace a nasazení](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment) a řešení se přidá do této stránky pro odstraňování potíží.

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Uživatelský účet, který používáte k provádění nasazení, nemá oprávnění k vytváření uživatelů nebo rolí. Například hostující společnost může k uživatelskému účtu, který nastaví za vás, přiřazovat role\_DataReader, DB\_datawrite a DB\_DB. Ty jsou dostačující pro vytváření většiny databázových objektů, ale ne pro vytváření uživatelů nebo rolí. Jedním ze způsobů, jak se vyhnout chybě, je vyloučení uživatelů a rolí z nasazení databáze. To lze provést úpravou elementu předsource pro automaticky generovaný skript databáze tak, aby obsahoval následující atributy:

[!code-console[Main](troubleshooting/samples/sample9.cmd)]

Informace o tom, jak upravit prvek předsource v souboru projektu, naleznete v tématu [How to: Edit nastavení nasazení v souboru projektu](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx). Pokud se uživatelé nebo role ve vaší vývojové databázi musí nacházet v cílové databázi, požádejte o pomoc svého poskytovatele hostingu.

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a>Chyba časového limitu SQL Server při spouštění vlastních skriptů během nasazení

### <a name="scenario"></a>Scénář

Zadali jste vlastní skripty SQL, které se spustí během nasazení, a když je Nasazení webu spustí, vyprší časový limit.

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Spuštění více skriptů, které mají různé režimy transakce, může způsobit chyby s časovým limitem. Ve výchozím nastavení se automaticky generované skripty spouštějí v transakci, ale vlastní skripty ne. Pokud na kartě **Package/PUBLISH SQL** vyberete možnost získat **data nebo schéma z existující databáze** a přidáte vlastní skript SQL, je nutné změnit nastavení transakce na některých skriptech, aby všechny skripty používaly stejné nastavení transakce. Další informace najdete v tématu [Postup: nasazení databáze pomocí projektu webové aplikace](https://msdn.microsoft.com/library/dd465343.aspx).

Pokud jste nakonfigurovali nastavení transakce tak, aby vše bylo stejné, ale stále se tato chyba zobrazila, možná alternativní řešení je spouštět samostatně. V mřížce **databázové skripty** na kartě **Package/Publish** SQL zrušte zaškrtnutí políčka **Zahrnout** pro skript, který způsobí chybu časového limitu, a pak projekt publikujte. Pak se vraťte do mřížky **databázové skripty** , zaškrtněte políčko **Zahrnout** do tohoto skriptu a zrušte zaškrtnutí políček **Zahrnout** pro ostatní skripty. Pak projekt znovu publikujte. Tentokrát při publikování se spustí pouze vybraný vlastní skript.

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a>Data datového proudu manifestu webového serveru ještě nejsou k dispozici.

### <a name="scenario"></a>Scénář

Při instalaci balíčku pomocí souboru *Deploy. cmd* s možností t (test) se zobrazí následující chybová zpráva:

Chyba: streamovaná data typu ' sitemanifest/dbFullSql [@path= ' C:\TEMP\AdventureWorksGrant.sql ']/sqlScript ' ještě nejsou k dispozici.

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Chybová zpráva znamená, že příkaz nemůže vytvořit testovací sestavu. Příkaz se ale může spustit, pokud použijete možnost y (vlastní instalace). Zpráva indikuje pouze, že došlo k potížím s spuštěním příkazu v režimu testu.

## <a name="this-application-requires-managedruntimeversion-v40"></a>Tato aplikace vyžaduje ManagedRuntimeVersion v 4.0.

### <a name="scenario"></a>Scénář

Při pokusu o nasazení se zobrazí následující chybová zpráva:

Fond aplikací, který se pokoušíte použít, má vlastnost ' managedRuntimeVersion ' nastavenou na hodnotu ' v 2.0 '. Tato aplikace vyžaduje: v 4.0.

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Ve službě IIS není nainstalován ASP.NET 4. Pokud je server, na který nasazujete, váš vývojový počítač a je na něm nainstalovaná aplikace Visual Studio 2010, v počítači je nainstalovaná služba ASP.NET 4, ale možná není nainstalovaná ve službě IIS. Na serveru, na který nasazujete, otevřete příkazový řádek se zvýšenými oprávněními a nainstalujte ASP.NET 4 do služby IIS spuštěním následujících příkazů:

[!code-console[Main](troubleshooting/samples/sample10.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a>Microsoft. Web. Deployment. DeploymentProviderOptions se nedá přetypovat.

### <a name="scenario"></a>Scénář

Při nasazení balíčku se zobrazí následující chybová zpráva:

Nelze přetypovat objekt typu Microsoft. Web. Deployment. DeploymentProviderOptions na Microsoft. Web. Deployment. DeploymentProviderOptions.

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Pokoušíte se o nasazení ze Správce služby IIS pomocí uživatelského rozhraní Nasazení webu 1,1 na server s nainstalovanou Nasazení webu 2,0. Pokud pomocí nástroje pro vzdálenou správu služby IIS nasazujete Import balíčku, při navázání připojení zaškrtněte dialogové okno **nové funkce k dispozici** . (Toto dialogové okno může být zobrazeno pouze jednou při prvním navázání připojení. Pokud chcete vymazat připojení a začít znovu, zavřete Správce služby IIS a znovu ho spusťte zadáním příkazu inetmgr/reset po vyčištění do příkazového řádku.) Pokud je jedna z uvedených funkcí **nasazení webu uživatelské rozhraní**a má číslo verze nižší než 8, server, na který nasazujete, může mít nainstalovanou Nasazení webu verze 1,1 a 2,0. Pokud chcete nasadit z klienta, který má nainstalovaný 2,0, musí mít server nainstalovanou jenom Nasazení webu 2,0. Pokud chcete tento problém vyřešit, budete muset kontaktovat svého poskytovatele hostingu.

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a>Nelze načíst nativní součásti SQL Server Compact

### <a name="scenario"></a>Scénář

Když spustíte nasazenou lokalitu, zobrazí se následující chybová zpráva:

Nelze načíst nativní součásti SQL Server Compact odpovídající poskytovateli ADO.NET verze 8482. Nainstalujte správnou verzi SQL Server Compact. Další podrobnosti najdete v článku 974247 znalostní báze Knowledge Base.

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Nasazený web nemá podsložky *amd64* a *x86* s nativními sestaveními ve složce *bin* aplikace. V počítači, který má nainstalované SQL Server Compact, jsou nativní sestavení umístěná ve *složce C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*. Nejlepším způsobem, jak získat správné soubory do správných složek v projektu sady Visual Studio, je instalace balíčku NuGet SqlServerCompact. Instalace balíčku přidá skript po sestavení ke zkopírování nativních sestavení do *amd64* a *x86*. Aby je bylo možné nasadit, je však nutné je ručně zahrnout do projektu. Další informace najdete v kurzu [nasazení SQL Server Compact](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md) .

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a>Po nasazení Code First aplikace Entity Framework se chyba cesta není platná.

### <a name="scenario"></a>Scénář

Nasadíte aplikaci, která používá Migrace Entity Framework Code First, a systém DBMS, jako je například SQL Server Compact, který ukládá svou databázi do souboru ve složce aplikace\_data. Po vašem prvním nasazení máte Migrace Code First nakonfigurovanou k vytvoření databáze. Při spuštění aplikace se zobrazí chybová zpráva podobná následujícímu příkladu:

Cesta není platná. Ověřte adresář pro databázi. [Path = c:\inetpub\wwwroot\App\_Data\DatabaseName.sdf]

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Code First se pokouší vytvořit databázi, ale složka\_data App neexistuje. Buď nemáte žádné soubory ve složce *\_dat* , když jste nasadili, nebo jste na kartě **balení nebo publikování na webu** projektu okno Vlastnosti vybrali možnost **vyloučit\_data aplikací** . Proces nasazení nevytvoří složku na serveru, pokud ve složce nejsou žádné soubory, které se mají zkopírovat na server. Pokud jste již v lokalitě nastavili databázi, proces nasazení je odstraní a *aplikace\_data* samotné složky, pokud jste v profilu publikování vybrali možnost **odebrat další soubory v cílovém umístění** . Pokud chcete tento problém vyřešit, vložte do složky *App\_data* zástupný soubor, jako je soubor. txt, a ujistěte se, že jste vybrali možnost **vyloučit\_data aplikace** a znovu nasadit.

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a>Objekt COM, který je oddělený od jeho podkladového RCW, nelze použít.

### <a name="scenario"></a>Scénář

Úspěšně jste pomocí publikování jedním kliknutím nasadili aplikaci a pak jste tuto chybu začali používat:

Úloha nasazení webu se nezdařila. (Nepovedlo se dokončit požadavek na adresu URL vzdáleného agenta<https://serverurl.com/msdeploy.axd?site=sitename>.)  
 Nepovedlo se dokončit požadavek na adresu URL vzdáleného agenta<https://url/msdeploy.axd?site=sitename>.  
Požadavek byl přerušen: požadavek byl zrušen.  
Objekt modelu COM, který byl oddělen od jeho podkladové RCW, nelze použít.

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

Ve výchozím nastavení sada Visual Studio nastaví oprávnění ke čtení pro kořenovou složku webu a oprávnění k zápisu do složky\_dat aplikace. Pokud vaše aplikace potřebuje přístup pro zápis do podsložky, můžete nastavit oprávnění pro tuto složku, jak je uvedeno v části nastavení oprávnění složky a nasazení do kurzů produkčního prostředí v této sérii. Pokud vaše aplikace potřebuje oprávnění k zápisu do kořenové složky lokality, je třeba zabránit tomu, aby v kořenové složce nastavila přístup jen pro čtení, a to tak, že do souboru profilu publikování přidáte **&lt;umístění IncludeSetACLProviderOn&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** (pro ovlivnění jednoho profilu) nebo do souboru WPP. TARGETS (aby to ovlivnilo všechny profily). Informace o tom, jak tyto soubory upravit, najdete v tématu [Postupy: Úprava nastavení nasazení v souborech profilu (. pubxml)](https://msdn.microsoft.com/library/ff398069.aspx).

<a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a>Chyba konfigurace – atribut targetFramework odkazuje na verzi, která je novější než nainstalovaná verze .NET Framework

### <a name="scenario"></a>Scénář

Úspěšně jste publikovali webový projekt, který se zaměřuje na ASP.NET 4,5, ale při spuštění aplikace (s režimem customErrors nastaveným na "off" v souboru Web. config) se zobrazí následující chyba:

Atribut targetFramework v prvku &lt;Compilation&gt; elementu souboru Web. config se používá pouze k cílení na verzi 4,0 a novějších .NET Framework (například '&lt;Compilation targetFramework = "4.0"&gt;"). Atribut targetFramework aktuálně odkazuje na verzi, která je novější než nainstalovaná verze .NET Framework. Zadejte platnou cílovou verzi .NET Framework nebo nainstalujte požadovanou verzi .NET Framework.

Zdrojové chybové pole chybové stránky zvýrazní následující řádek ze souboru Web. config, protože by došlo k chybě:

&lt;kompilace targetFramework = "4.5"/&gt;

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Server nepodporuje ASP.NET 4,5. Obraťte se na poskytovatele hostingu a zjistěte, kdy a kde je možné přidat podporu pro ASP.NET 4,5. Pokud upgrade serveru není možnost, je nutné nasadit webový projekt, který cílí na ASP.NET 4 nebo starší místo.

Pokud nasadíte webový projekt ASP.NET 4 nebo starší do stejného místa, zaškrtněte políčko **odebrat další soubory v cílovém umístění** na kartě **Nastavení** průvodce **Publikovat web** . Pokud nevyberete možnost **odebrat další soubory v cílovém umístění**, budete mít i nadále k dispozici stránku Chyba konfigurace.

Okna **vlastností** projektu obsahují rozevírací seznam cílové rozhraní, ale tento problém nemůžete vyřešit pouhou změnou tohoto problému z **.NET Framework 4,5** na **.NET Framework 4**. Pokud změníte cílovou architekturu na dřívější verzi rozhraní, projekt bude mít stále odkazy na sestavení verze novějšího rozhraní a nebude spuštěn. Je nutné ručně změnit tyto odkazy nebo vytvořit nový projekt, který se zaměřuje na .NET Framework 4 nebo starší. Další informace najdete v tématu [.NET Framework cílení na weby](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx).

## <a name="medium-trust-errors"></a>Chyby střední důvěryhodnosti

### <a name="scenario"></a>Scénář

Když spustíte aplikaci v produkčním prostředí, dojde k chybě související se středním vztahem důvěryhodnosti.

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

Mnoho poskytovatelů hostingu třetích stran spouští váš web ve středním vztahu důvěryhodnosti, což znamená, že některé věci neumožňují. Například kód aplikace nemůže získat přístup k registru systému Windows a nemůže číst nebo zapisovat soubory, které se nacházejí mimo hierarchii složek vaší aplikace. Ve výchozím nastavení je vaše aplikace spuštěná v *úplném vztahu důvěryhodnosti* na místním počítači, což znamená, že aplikace může být schopná provádět věci, které se při nasazení do produkčního prostředí nezdařily.

Aplikaci můžete nakonfigurovat tak, aby běžela v rámci střední důvěryhodnosti v místním prostředí služby IIS, aby mohla řešit potíže. Provedete to tak, že otevřete soubor *Web. config* aplikace a přidáte element **Trust** do prvku **System. Web** , jak je znázorněno v tomto příkladu.

[!code-xml[Main](troubleshooting/samples/sample11.xml)]

Aplikace se teď v IIS spustí ve středním vztahu důvěryhodnosti i na místním počítači.

Tento postup neprovádějte, pokud nasazujete na Azure App Service, protože Azure nevyžaduje střední důvěryhodnost. V době, kdy je tento kurz napsán v únoru, 2012, použití této metody k tomu, aby vaše aplikace běžela ve středním vztahu důvěryhodnosti, způsobí chybu v Azure.

Pokud používáte Migrace Entity Framework Code First a nasazujete pro poskytovatele hostingu, který spouští vaši aplikaci ve středním vztahu důvěryhodnosti, ujistěte se, že máte nainstalovanou verzi 5,0 nebo novější. V Entity Framework verze 4,3 vyžaduje migrace úplný vztah důvěryhodnosti, aby bylo možné aktualizovat schéma databáze.

## <a name="http-40417-not-found-error"></a>Chyba HTTP 404,17 se nenašla.

### <a name="scenario"></a>Scénář

Když na vývojovém počítači ve službě IIS spustíte nasazenou lokalitu, zobrazí se následující chybová zpráva s oznámením, že server nemůže zpracovat default. aspx:

Chyba protokolu HTTP 404,17 – nenalezeno

Požadovaný obsah vypadá jako skript a nebude obsluhován obslužnou rutinou statického souboru.

### <a name="possible-cause-and-solution"></a>Možná příčina a řešení

V počítači nemusí být nainstalována ASP.NET 4,5. Podívejte se na postup v tématu nasazení do služby IIS jako kurz testovacího prostředí v této sérii, který vysvětluje, jak nainstalovat ASP.NET 4,5.

> [!div class="step-by-step"]
> [Předchozí](deploying-extra-files.md)

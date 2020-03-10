---
uid: web-pages/readme/overview
title: Soubor Readme WebMatrix | Microsoft Docs
author: rick-anderson
description: Soubor Readme pro ASP.NET verze WebMatrix a Web Pages (Razor) 1,0
ms.author: riande
ms.date: 01/06/2011
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: fac53e935860a90d8f2aa96699d56d66ade3a40f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563467"
---
# <a name="webmatrix-readme"></a>WebMatrix – soubor Readme

13. ledna 2011

## <a name="contents"></a>Obsah

> [!NOTE]
> Tento soubor Readme se týká verze 1,0 WebMatrixu.

- [Přehled](#Overview)
- [Instalace](#Installation_Notes)
- [Jak publikovat aplikace](#InstructionsForPublishingApplications)
- [Změny a problémy](#ChangesAndIssues)

    - [Instalace WebMatrix 1,0](#Known_Issues_Installation)
    - [Webové stránky ASP.NET](#Known_Issues_ASPNET)
    - [WebMatrixu](#Known_Issues_WebMatrix)
    - [IIS Express](#Known_Issues_IISExpress)
    - [SQL Server Compact](#Known_Issues_SQLServerCompact)
    - [Instalace aplikací](#Known_Issues_Installing_Applications)
    - [Publikování aplikací](#Known_Issues_Publishing_Applications)
- [Další informace](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a>Přehled

> Microsoft WebMatrix 1,0 je bezplatný sada pro vývoj webů, která se instaluje během několika minut. Integruje webový server s databázovými a programovacími rozhraními k vytvoření jediného integrovaného prostředí. Pomocí WebMatrixu můžete zjednodušit způsob, jakým kód, otestujete a publikujete vlastní web ASP.NET nebo PHP, nebo můžete pomocí WebMatrixu začít nový web pomocí oblíbených open source aplikací, jako je DotNetNuke, Umbraco, WordPress nebo Joomla. WebMatrix používá stejný výkonný prostředí webového serveru, databázového stroje a rozhraní, které spustí vaši webovou stránku na internetu, což usnadňuje přechod z vývoje do produkčního prostředí a hladkého a bezproblémového.

<a id="Installation_Notes"></a>

## <a name="installation"></a>Instalace

> Pokud chcete nainstalovat WebMatrix 1,0, musíte nejdřív nainstalovat [Instalace webové platformy Microsoft 3,0](https://go.microsoft.com/fwlink/?LinkID=194638). Po nainstalování instalačního programu webové platformy ho můžete použít k instalaci WebMatrixu.
> 
> Pokud máte při instalaci problémy, přečtěte si téma [řešení potíží s instalace webové platformy Microsoft](https://go.microsoft.com/fwlink/?LinkId=196212).

<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a>Jak publikovat aplikace

> Přečtěte si podrobné [pokyny pro publikování aplikací](https://go.microsoft.com/fwlink/?LinkID=196149) .

<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a>Změny a problémy

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a>Problémy s instalací WebMatrix 1,0

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a>Problém: WebMatrix 1,0 je dostupný jenom na platformách, které podporují Microsoft .NET Framework 4.

> Pro WebMatrix se vyžaduje .NET Framework verze 4. V některých případech se instalační program WebMatrix 1,0 pokusí nainstalovat na platformu, která není součástí podporované konfigurační sady. Konkrétně Windows Vista bez aktualizace SP1 vám umožní zahájit instalaci WebMatrixu, ale komponenta .NET Framework 4 selže a zablokuje instalaci.
> 
> **Alternativní řešení**  
> Nainstalujte na podporovanou platformu, která zahrnuje:
> 
> - Windows 7
> - Windows Server 2008
> - Windows Server 2008 R2
> - Windows Vista SP1 nebo novější
> - Windows XP SP3
> - Windows Server 2003 SP2

#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>Problém: nejde nainstalovat WebMatrix 1,0, pokud je nainstalovaná Microsoft Visual Studio 2008 bez Microsoft Visual Studio 2008 SP1.

> **Alternativní řešení**  
> Nainstalujte [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) z webu Microsoft Download Center.

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a>Problém: některá sestavení pro SQL Server Compact 4,0 nejsou v globální mezipaměti sestavení (GAC) nainstalovaná.

> Spravovaná sestavení pro SQL Server Compact 4,0 nejsou vložena do globální mezipaměti sestavení (GAC) při instalaci SQL Server Compact 4,0 na počítači 64 a počítač má nainstalovaný pouze klientský profil .NET Framework 3,5 SP1. Spravovaná sestavení, která nejsou nainstalovaná v globální mezipaměti sestavení (GAC), jsou:
> 
> - *System. data. SqlServerCe. dll* (poskytovatel ADO.NET)
> - *System. data. SqlServerCe. entity. dll* (ADO.NET Entity Framework)
> 
> **Alternativní řešení**  
> Odinstalujte SQL Server Compact 4,0. Úplnou verzi .NET Framework 3,5 SP1 si stáhněte a nainstalujte z následujícího umístění:  
>   
> [Microsoft .NET Framework 3,5 Service Pack 1 (úplný balíček)](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> Pak přeinstalujte SQL Server Compact 4,0.

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a>Problém: SQL Server Compact nejde odinstalovat pomocí příkazového řádku.

> Odinstalace SQL Server Compact pomocí možností příkazového řádku nefunguje v této verzi.
> 
> **Alternativní řešení**  
> Pomocí *programů a funkcí* v Ovládacích panelech systému Windows odinstalujte Microsoft SQL Server Compact 4,0.

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a>ASP.NET Web Pages

Tato část dokumentu popisuje nové funkce, změny a známé problémy s verzí 1,0 webových stránek ASP.NET s využitím syntaxe Razor.

- [Nové funkce](#NewFeatures)
- [Provedeny](#Changes)
- [Problémy](#Issues)

#### <a id="NewFeatures"></a>Nové funkce

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a>Novinka: Přidání nastavení konfigurace za účelem zakázání správce balíčků

> Nový klíč `asp:AdminManagerEnabled` je k dispozici pro `<appSettings>` prvek v souboru *Web. config* , který umožňuje zcela zakázat Správce balíčků. Výchozí hodnota pro tento prvek je true, to znamená, že pokud není obsažena v souboru *Web. config* , je povolen správce balíčků. Chcete-li zakázat Správce balíčků, přidejte následující element do souboru *Web. config* v kořenovém adresáři webu:
> 
> [!code-xml[Main](overview/samples/sample1.xml)]

#### <a id="Changes"></a>Provedeny

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a>Změna: klíč webpages: AdminFolderVirtualPath se přejmenoval na ASP: AdminFolderVirtualPath.

> Klíč `webPages:AdminFolderVirtualPath`, který lze přidat do souboru *Web. config* pro určení umístění správce balíčků, byl přejmenován na použití `asp:`ho oboru názvů namísto oboru názvů `webPages`. Pokud jste tento prvek použili, je nutné jej přejmenovat v konfiguračním souboru.

#### <a id="Issues"></a> Známé problémy

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a>Problém: hesla pro uživatele členství již nejsou rozpoznána.

> Algoritmus pro vytváření a ukládání hesel členství (přihlášení) byl změněn tak, aby byl bezpečnější. V důsledku toho nebudou rozpoznána hesla uložená pro členy (uživatelé) vytvořená ve verzích beta verze ASP.NET Razor. 
> 
> **Alternativní řešení** Pokud lokalita ještě není vložená do produkčního prostředí, odeberte z databáze členství záznamy uživatelů. Pokud je databáze živá, programově znovu vygenerujte stávající hesla v databázi členství.

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>Problém: neočekávané chování při použití vlastní uživatelské tabulky pro členství

> Chcete-li inicializovat poskytovatele členství pro web ASP.NET Razor, zavoláte metodu `WebSecurity.InitializeDatabaseConnection`. (Ve webové matici úvodní šablona webu obsahuje volání této metody v souboru *\_AppStart. cshtml* .) Pokud je parametr `autoCreateTables` této metody nastaven na hodnotu true (ve výchozím nastavení je nastaven na hodnotu true v šabloně počátečního webu) a pokud je do metody (druhý parametr) předána nerozpoznaný název tabulky, metoda nevyvolá chybu. Místo toho se tabulka automaticky vytvoří.
> 
> To může být problém, pokud máte v úmyslu použít pro členství vlastní uživatelskou tabulku, ale předat do metody `WebSecurity.InitializeDatabaseConnection` špatný název tabulky. Vzhledem k tomu, že metoda není ve výchozím nastavení vyvolána, pokud zadaná tabulka neexistuje a protože místo toho vytvoří novou tabulku, aplikace může vypadat, že bude fungovat. Nicméně kód aplikace, který závisí na vlastní uživatelské tabulce (a u polí v ní), může nakonec selhat s neočekávanými chybami.
> 
> **Alternativní řešení**  
> Ujistěte se, že název předaný v metodě `InitializeDatabaseConnection` odpovídá tabulce profilů uživatele v databázi členství, nebo se ujistěte, že parametr `autoCreateTables` je nastaven na hodnotu false.

#### <a name="issue-error-message-the-admin-module-requires-access-to-app_data"></a>Problém: chybová zpráva "modul Správce vyžaduje přístup k ~/App\_data"

> V některých případech se při pokusu o vytvoření uživatelů nebo jiné práci se systémem členství v ASP.NET může způsobit, že se na stránce zobrazí chyba *, že modul Správce vyžaduje přístup k ~/App\_data*. K tomu dochází, pokud účet, na kterém je spuštěná služba IIS nebo IIS Express, nemá oprávnění k vytvoření a zápisu do složky *\_dat aplikace* v kořenovém adresáři webu. 
> 
> **Alternativní řešení** Ručně vytvořte složku *dat\_aplikace* pro web. Pak se ujistěte, že účet systému Windows, pod kterým běží aplikace (obvykle síťová služba), má oprávnění ke čtení a zápisu pro kořenové složky aplikace a pro podsložky, jako jsou například data aplikace\_. Podrobnější informace jsou k dispozici v článku znalostní báze [problémy s SQL Server Expressmi vytvářením uživatelských instancí a projektů webových aplikací ASP.NET](https://support.microsoft.com/kb/2002980).

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>Problém: nepovedlo se vygenerovat uživatelskou instanci SQL Server, chyba.

> Pokud webová aplikace WebMatrix používá SQL Server Express a je v systému Windows 7 nebo Windows Server 2008 R2 spuštěna služba IIS 7,5, může se zobrazit chyba, která indikuje, že SQL Server během běhu nemůže načíst cestu k místní aplikaci uživatele.
> 
> **Alternativní řešení** Ujistěte se, že účet systému Windows, pod kterým je aplikace spuštěna (obvykle síťová služba), má oprávnění ke čtení a zápisu pro kořenové složky aplikace a pro podsložky, jako jsou například *data aplikace\_* . Podrobnější informace jsou k dispozici v článku znalostní báze [problémy s SQL Server Expressmi vytvářením uživatelských instancí a projektů webových aplikací ASP.NET](https://support.microsoft.com/kb/2002980).

#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a>Problém: soubory, které obsahují prostředky správce balíčků nebo hesla správce balíčků, jsou v rámci služby IIS 6,0 a starší.

> Pokud nasadíte aplikaci ASP.NET Web Pages (Razor), která byla sestavena pomocí verze RC2, a pokud aplikace obsahuje soubor *Password. txt* nebo *packagesources. txt* v oblasti */App\_data/správce*, služba IIS 6,0 bude v případě potřeby využívat soubor a potenciálně vystaví hesla pro vaši instanci správce balíčků. 
> 
> **Alternativní řešení** Přejmenujte soubor *Password. txt* nebo *packagesources. txt* na *Password. config* nebo *packagesources. config*. Ve výchozím nastavení služba IIS 6,0 neposkytuje soubory, které mají příponu *. config* . (Ve službě IIS 7 se nezpracovávají žádné soubory ve složce *App\_data* , takže je nemusíte soubory přejmenovávat.)

#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a>Problém: odinstalování balíčků nainstalovaných pomocí beta 3 verze neodstraní zcela součásti balíčku.

> Pokud jste balíček nainstalovali pomocí Správce balíčků ve verzi beta 3 a pak se pokusíte ho odinstalovat pomocí aktuální verze, balíček není zcela odinstalován. Pomocí tlačítka **odinstalovat** správce balíčků se odstraní některé komponenty, ale ponechá kód knihovny balíčku a neaktualizuje soubor *Package. config* .
> 
> **Alternativní řešení**   
> Proveďte tyto kroky:  
> 1. Odstraňte složku *aplikace\_Data\packages* . Tím se odstraní všechny balíčky.   
> 2. Odstraňte soubor *Packages. config* v kořenovém adresáři webu.

#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a>Problém: v aplikaci Visual Studio vyvolání webového správce balíčků převede aplikaci do offline režimu.

> Pokud pracujete v aplikaci Visual Studio (nikoli WebMatrix) a ke spuštění Správce balíčků použijete funkci *\_admin* , Visual Studio převede aplikaci do offline režimu a odešle *aplikaci\_offline. htm* do kořenového adresáře webu, což narušuje možnosti použití Správce balíčků.
> 
> [!NOTE]
> I když byste při použití webového rozhraní Správce balíčků nejčastěji viděli toto chování, dojde k stejnému chování, když přidáte, odeberete nebo upravíte jakékoli soubory ve složce *App\_data* .
> 
> **Alternativní řešení**   
> Chcete-li pracovat s balíčky v aplikaci Visual Studio, použijte místo webového správce balíčků rozšíření NuGet. Informace najdete v [dokumentaci k NuGet](https://docs.microsoft.com/nuget/). Pokud pracujete s jinými soubory ve složce *App\_data* , zvažte, jestli soubory jsou jinde, abyste se tomuto problému vyhnuli. Pokud to není praktické, odstraňte *aplikaci\_offline souboru. htm* ručně nebo počkejte, až se web automaticky vrátí do online režimu (ve výchozím nastavení po 30 sekundách).

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>Problém: Visual Studio IntelliSense a šablony projektů dostupné jenom ve ASP.NET MVC verze 3

> Při instalaci webových stránek ASP.NET se také neinstalují nástroje pro Visual Studio, jako jsou IntelliSense a šablony projektů pro aplikace ASP.NET Web Pages.
> 
> **Alternativní řešení** Chcete-li používat IntelliSense a šablony projektů pro aplikace ASP.NET Web Pages v aplikaci Visual Studio, nainstalujte ASP.NET MVC 3 RC buď prostřednictvím instalačního programu webové platformy, nebo pomocí [samostatného instalačního programu](https://go.microsoft.com/fwlink/?LinkID=191797).

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>Problém: čtení informačních kanálů nebo jiných externích dat prostřednictvím proxy server

> Pokud je server, na kterém je spuštěná lokalita, za proxy server, může být nutné nakonfigurovat informace o proxy serveru v souboru *Web. config* , aby bylo možné číst informace, které pocházejí z mimo vaši lokalitu. Pokud například použijete pomocníka `ReCaptcha`, pomáhající osoba komunikuje se službou reCAPTCHA, ale může být blokována proxy server. Podobně kanály, které se používají v ASP.NET webové stránky, jako je informační kanál používaný správcem balíčků, můžou vyžadovat konfiguraci proxy serveru.
> 
> Pokud dochází k potížím při práci s externí službou nebo při práci s kanálem balíčku, vložte následující prvky do kořenového souboru *Web. config* vaší aplikace:
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> Další informace o konfiguraci proxy server najdete v tématu [&lt;proxy&gt; elementu (nastavení sítě)](https://msdn.microsoft.com/library/sa91de1e.aspx) na webu MSDN.

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>Problém: Odinstalace .NET Framework verze 4: zakáže webové stránky ASP.NET se syntaxí Razor.

> Pokud odinstalujete .NET Framework verze 4 a pak ji znovu nainstalujete, ASP.NET webové stránky s syntaxe Razor jsou zakázané. Stránky s příponou *. cshtml* neběží správně. Webové stránky ASP.NET registrují sestavení v kořenovém souboru *Web. config* počítače a odebrání .NET Framework Tento soubor odebere. Opětovná instalace .NET Framework nainstaluje novou verzi konfiguračního souboru, ale nepřidá odkaz pro sestavení webových stránek ASP.NET.
> 
> **Alternativní řešení** Po přeinstalaci .NET Framework přeinstalujte webové stránky ASP.NET pomocí syntaxe Razor. Tím se do souboru *Web. config* přidá následující element v kořenovém adresáři počítače, který je obvykle v následujícím umístění:  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a>Problém: adresy URL bez přípony nenaleznou soubory. cshtml/. vbhtml ve službě IIS 7 nebo IIS 7,5

> V případě služby IIS 7 nebo IIS 7,5 nebudou žádosti s adresou URL, jako jsou následující, schopné najít stránky s příponou *. cshtml* nebo *. vbhtml* :  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> K tomuto problému dochází, protože přepis adres URL není ve výchozím nastavení povolený pro IIS 7 nebo IIS 7,5. Ve scénáři likeliest se problém nezobrazuje při místním testování pomocí IIS Express, ale při nasazování webu na hostující web dojde k jeho práci.
> 
> **Alternativní řešení**
> 
> - Pokud máte kontrolu nad počítačem serveru, na serverovém počítači nainstalujte aktualizaci popsanou v [aktualizaci, která umožňuje určitým obslužným rutinám služby iis 7,0 nebo iis 7,5 zpracovávat požadavky, jejichž adresy URL nekončí tečkou](https://support.microsoft.com/kb/980368).
> - Pokud nemáte kontrolu nad počítačem serveru (například nasazujete na hostující Web), přidejte následující do souboru *Web. config* webu: 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>Problém: nasazení aplikace do počítače, ve kterém není nainstalovaná SQL Server Compact

> Aplikace, které zahrnují SQL Server Compact databáze, mohou běžet v počítači, kde není nainstalován SQL Server Compact. Microsoft WebMatrix 1,0 automaticky zkopíruje tyto binární soubory a provede příslušné transformace souboru *Web. config* .
> 
> **Alternativní řešení** Pokud potřebujete tyto soubory zkopírovat a provést změny v souboru *Web. config* ručně, postupujte následovně:
> 
> 1. Zkopírujte sestavení databázového stroje do složky *bin* (a podsložek) aplikace v cílovém počítači:  
> 
>    - Kopírování *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll*   
>      **do** *\Bin*
>    - Kopírování *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* **do** *\Bin\x86*
>    - Kopírování *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* * **do** *\Bin\amd64*
> 
> 2. V kořenové složce webu vytvořte nebo otevřete soubor *Web. config* . (Ve WebMatrixu 1,0 je tento typ souboru k dispozici, pokud kliknete na tlačítko **vše** v dialogovém okně **zvolit typ souboru** .)
> 3. Přidejte následující prvek jako podřízený prvek prvku `<configuration>` (není uvnitř elementu `<system.web>`):
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>Problém: pomocníka databáze a WebGrid nefungují v nestředním vztahu důvěryhodnosti v Visual Basic

> Pokud používáte Visual Basic (vytváření souborů *. vbhtml* ), `Database` a `WebGrid` pomocníka nebudou fungovat, pokud je aplikace nastavená tak, aby používala střední důvěryhodnost.
> 
> **Alternativní řešení**  
> Pokud používáte sadu Visual Studio 2010, můžete tento problém vyřešit instalací verze Service Pack 1. Dokud nebude k dispozici konečná verze nástroje SP1, můžete stáhnout beta verzi nástroje SP1 ze stránky [Microsoft Visual Studio 2010 s aktualizací Service Pack 1 beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) na webu Microsoft Download Center.   
>   
> Pokud to není praktické nebo pokud nepoužíváte sadu Visual Studio 2010, můžete aplikaci dočasně nastavit tak, aby používala úplný vztah důvěryhodnosti.

#### <a name="issue-applicationpart-resources-are-externally-accessible"></a>Problém: prostředky "ApplicationPart" jsou externě přístupné

> Pokud sestavení obsahuje objekty, které jsou odvozeny z třídy `ApplicationPart`, jsou prostředky tohoto sestavení zpřístupněny třídou `ResourceRouteHandler`. Podívejte se například na následující adresu URL:  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> Tento požadavek stáhne všechny řetězce prostředků v sestavení *System. Web. webpages. Administration. dll* . Stáhnou se všechny integrované prostředky (dokonce i ty, které nejsou určené k obsluhování jako statický obsah). Pokud vložené prostředky obsahují citlivé informace, může to představovat bezpečnostní riziko. 
> 
> **Alternativní řešení**   
> Pokud vytvoříte objekt **ApplicationPart** , ujistěte se, že vložené prostředky přidružené k danému sestavení **ApplicationPart** objektu neobsahují citlivé informace.

<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a>WebMatrix

> [!NOTE]
> Informace o problémech s instalací pro WebMatrix najdete v části [potíže s instalací WebMatrix](#Known_Issues_Installation) výše v tomto dokumentu.

Tato část dokumentu popisuje známé problémy pro vývojové prostředí WebMatrix.

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a>Problém: změny uživatelského jména nebo hesla databázového připojovacího řetězce v souboru Web. config se neprojeví v pracovním prostoru databáze.

> **Alternativní řešení**  
> 
> 1. V souboru *Web. config* změňte název databáze v připojovacím řetězci (například přidat "1").
> 2. Uložte soubor *Web. config* .
> 3. Klikněte na **databáze** a aktualizujte.
> 4. Změňte název databáze v připojovacím řetězci v souboru *Web. config* zpět na původní název databáze.
> 5. Uložte soubor *Web. config* .
> 6. Klikněte na **databáze** a aktualizujte.

#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a>Problém: složky vytvořené pomocí WebMatrixu se nedají odstranit.

> Pokud je WebMatrix spuštěný pomocí zvýšených oprávnění (to znamená, že jste spustili WebMatrix pomocí možnosti **Spustit jako správce** ve Windows), složky, které jsou vytvořené pomocí WebMatrixu, se nedají odstranit pomocí Průzkumníka Windows.
> 
> **Alternativní řešení**  
> Spusťte Průzkumníka Windows pomocí zvýšených oprávnění. Postupujte následovně:  
> 
> 1. V systému Windows klikněte na tlačítko **Start**.
> 2. Zadejte "Průzkumník Windows" a klikněte pravým tlačítkem myši na položku **Průzkumník Windows**.
> 3. Klikněte na **Spustit jako správce**. Pak můžete složky odstranit.

#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a>Problém: WebMatrix 1,0 není schopen provádět určité úlohy, které vyžadují zvýšení úrovně oprávnění.

> WebMatrix 1,0 není schopen provádět určité úlohy, které vyžadují zvýšení oprávnění, jako je například instalace dalších součástí v následujících situacích:
> 
> - V systému Windows Vista nebo Windows 7 jste přihlášeni pomocí účtu, který nemá oprávnění správce a nástroj řízení uživatelských účtů (UAC) je zakázán.
> - Používáte Microsoft Windows XP nebo Microsoft Windows Server 2003.
> 
> **Alternativní řešení**  
> Většina úloh v WebMatrixu 1,0 nevyžaduje oprávnění správce. V případě, že to uděláte, můžete tuto operaci provést jako správce nebo postupovat podle následujících kroků:
> 
> - V systému Windows Vista nebo Windows 7 povolte nástroj řízení uživatelských účtů.
> - V systému Windows XP přidejte uživatele do skupiny zabezpečení Správci.

#### <a name="issue-site-from-web-gallery-is-disabled"></a>Problém: lokalita z webové galerie je zakázaná.

> Možnost **web z Galerie webu** je zakázána, pokud není nainstalována instalace webové platformy 3,0.
> 
> **Alternativní řešení**  
> Nainstalujte [Instalace webové platformy Microsoft 3,0](https://go.microsoft.com/fwlink/?LinkID=194638).

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a>Problém: Google Chrome není k dispozici jako možnost spuštění.

> Google Chrome se v seznamu **Spustit** na kartě **Domů** nezobrazí.
> 
> **Alternativní řešení**  
> Některé verze Google Chrome se neregistrují správně s funkcí výchozí programy v systému Windows. Jako alternativní řešení spusťte Google Chrome, klikněte na nabídku *přizpůsobit a řídit Google Chrome* , klikněte na *Možnosti*a potom klikněte na *nastavit Google Chrome výchozí prohlížeč*.

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a>Problém: dialogové okno cizí klíč nepovoluje zadávání primárního klíče.

> Dialogové okno **cizí klíč** vám neumožňuje zadat název primárního klíče z tabulky primárního klíče.
> 
> **Alternativní řešení**  
> To je úmyslné. Nemusíte zadávat název primárního klíče z tabulky primárního klíče.

#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a>Problém: IntelliSense není k dispozici ve WebMatrixu pro C#syntaxe Razor, nebo Visual Basic

> Technologie IntelliSense je podporována v WebMatrixu pro HTML a CSS. Není ale k dispozici pro jiné jazyky. 
> 
> **Alternativní řešení**   
> Žádné.

#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a>Problém: technologie IntelliSense pro HTML a CSS navrhuje prvky, které nejsou kontextově vhodné

> Technologie IntelliSense pro značky ve WebMatrixu podporuje HTML pomocí [přechodného schématu XHTML 1,0](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) a šablon stylů CSS pomocí [schématu CSS 2,1](http://www.w3.org/TR/CSS2/). Vzhledem k tomu, že je technologie IntelliSense založena na těchto specifických schématech, mohou být doporučeny určité značky, atributy nebo vlastnosti, které nejsou vhodné pro aktuální definici stránky nebo stylu. V případě HTML může také vést k neočekávaným návrhům v obsahu, který může být interpretován jako nesprávně vytvořený kód XHTML (například když nejsou značky uzavřeny). Tento problém může být více patrné, pokud je kurzor uvnitř nekompletní značky; v takovém případě může IntelliSense navrhovat nové úvodní značky nebo nabízet jiné nesprávné návrhy. 
> 
> **Alternativní řešení**   
> V případě jazyka HTML se ujistěte, že pracujete v rámci dobře formátované a kompletní stránky XHTML. Pro šablony stylů CSS neexistuje žádné alternativní řešení.

#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a>Problém: při psaní není vyvolána technologie IntelliSense

> V důsledku toho nemusí být technologie IntelliSense vyvolána, protože v editoru je zadán kód HTML nebo šablona stylů CSS. Konkrétně k tomu může dojít, když je kurzor přímo vedle jiného prvku nebo na konci souboru. 
> 
> **Alternativní řešení**   
> Zajistěte, aby kolem místa vložení bylo prázdné místo, a že kurzor není na konci souboru. IntelliSense můžete také vyvolat ručně stisknutím kombinace kláves CTRL + MEZERNÍK.

#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a>Problém: pro zakázání IntelliSense není k dispozici žádné uživatelské rozhraní.

> WebMatrix 1,0 neposkytuje žádné uživatelské rozhraní ani gesto pro zakázání technologie IntelliSense. 
> 
> **Alternativní řešení**   
> Spusťte WebMatrix pomocí následujícího příkazu, který obsahuje přepínač zakazující technologii IntelliSense:  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`

<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a>IIS Express

IIS Express má vlastní soubor Readme, který je k dispozici na následující adrese URL:

[https://go.microsoft.com/fwlink/?LinkID=207675&amp; clcid = 0x405](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a>SQL Server Compact

SQL Server Compact má vlastní soubor Readme, který je k dispozici na následující adrese URL:

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

Informace o problémech, které zahrnují instalaci SQL Server Compact jako součást webové matrice, najdete v části [potíže při instalaci WebMatrix](#Known_Issues_Installation) výše v tomto dokumentu.

### <a id="Known_Issues_Installing_Applications"></a>Instalace aplikací

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>Problém: instalace aplikace může trvat dlouhou dobu, pokud se složka Dokumenty uživatele přesměruje na sdílenou síťovou složku.

> **Alternativní řešení**  
> Žádné. Instalace aplikace může nějakou dobu trvat, ale nainstaluje se správně.

### <a id="Known_Issues_Publishing_Applications"></a>Publikování aplikací

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a>Problém: při publikování SQL Compact Database nejde získat povinná oprávnění.

> WebMatrix plně nepodporuje nasazení podpůrných binárních souborů pro SQL Server Compact na server, na kterém běží .NET Framework verze 3,5 s konfigurací středně důvěryhodného vztahu důvěryhodnosti.
> 
> **Alternativní řešení**  
> Upřednostňovaným řešením je instalace .NET Framework 4 na server. Případně proveďte následující:
> 
> 1. Do části `SecurityClasses` v souboru *Web\_MediumTrust. config* přidejte následující prvky:
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. Vytvořte novou sadu oprávnění v souboru *Web\_MediumTrust. config* s následujícími požadovanými oprávněními:
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. Použijte sadu oprávnění na SQL Server Compact tím, že do souboru *Web\_MediumTrust. config* vložíte následující prvky:
> 
>     [!code-html[Main](overview/samples/sample8.html)]

#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a>Problém: galerie a webové aplikace PhpBB po publikování zobrazují chybu služba není k dispozici.

> V některých případech publikování aplikace způsobí chybu "služba není k dispozici".
> 
> **Alternativní řešení**  
> Ve WebMatrixu přidejte zpětné lomítko (\) na konec názvu serveru v okně **Nastavení publikování** a pak aplikaci znovu publikujte.

#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a>Problém: rozložení webu Moodle a odkazy se po publikování přeruší.

> Po publikování aplikace Moodle aplikace nefunguje správně.
> 
> **Alternativní řešení**  
> Ve WebMatrixu přidejte lomítko (/) na konec pole **název webu** v okně **Nastavení publikování** a pak znovu publikujte aplikaci.

#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a>Problém: publikování nopCommerce se nezdařilo s chybou databáze

> Publikování nopCommerce se nepovede a ohlásí chybu v databázi, jako je "vložení do tabulky protokolu NOP\_se nezdařilo."
> 
> **Alternativní řešení**  
> 
> 1. V nabídce WebMatrix klikněte na **Spustit** , aby se NopCommerce spouštěla místně.
> 2. Přihlaste se na stránku Správa.
> 3. Klikněte na nabídku **systém** .
> 4. Klikněte na možnost **protokol** .
> 5. Klikněte na tlačítko **Vymazat protokol**.
> 6. Publikujte nopCommerce znovu.

#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a>Problém: SilverStripe CMS zobrazí při stažení publikované lokality chybu FCGI PHP protokolu HTTP 500.

> **Alternativní řešení**  
> Po kliknutí na **Stáhnout publikovaný web**vynechejte `silverstripe-cache/manifest_main` v **publikování Preview**. Tento soubor se používá pro účely ukládání do mezipaměti a je specifický pro každý počítač.

#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a>Problém: při stahování publikované lokality se u podtextu zobrazí zpráva "Chyba serveru v aplikaci/".

> **Alternativní řešení**  
> Otevřete soubor *Web. config* webu a v připojovacím řetězci databáze nahraďte ID a heslo uživatele pomocí přihlašovacích údajů správce SQL Server (přihlašovací údaje SA).
> 
> Případně můžete pomocí těchto kroků udělit uživatelskému účtu, ke kterému jste přihlášeni, oprávnění `db_owner`:
> 
> 1. Nainstalujte SQL Server Management Studio pomocí instalačního programu webové platformy.
> 2. Připojte se k místní instanci SQL Server Express (ve výchozím nastavení `.\SQLEXPRESS`).
> 3. Klikněte na **databáze** &gt; *[LocalSubtextDatabase]* &gt; **zabezpečení** &gt; **uživatele** &gt; *[localSubtextUser*] (výchozí nastavení je `subtextuser`], klikněte pravým tlačítkem myši a klikněte na **vlastnosti**.
> 4. V části členství v roli vyberte **db\_vlastník** .

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a>Problém: po publikování nemusí lokalita fungovat, pokud se v poli Cílová adresa URL nepoužívá předpona http://nebo https://.

> Pokud v dialogovém okně **Nastavení publikování** nezačíná cílová adresa URL `http://` nebo `https://`, web po nasazení nemusí fungovat.
> 
> **Alternativní řešení**  
> Ujistěte se, že před publikováním webu se v dialogovém okně **Nastavení publikování** spustí cílová adresa URL s `http://` nebo `https://`.

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a>Problém: publikování databáze MySQL se nepovede kvůli chybě: publikování databáze se nepovedlo. K tomu může dojít, pokud Vzdálená databáze nemůže skript spustit. "

> K této chybě může dojít z několika důvodů. Jedním z důvodů, proč se tato chyba zobrazuje, je, že databázový skript obsahuje znak jednoduché uvozovky (') a výchozí znaková sada databáze MySQL není UTF-8.
> 
> **Alternativní řešení**  
> Nastavte výchozí znakovou sadu pro vzdálenou databázi MySQL na UTF-8.

#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a>Problém: některé odkazy nejsou v DotNetNuke viditelné po publikování nebo stahování webu.

> Pokud publikujete nebo stáhnete web DotNetNuke, možná budete muset vymazat mezipaměť a získat tak nové odkazy, které se zobrazí na webu.
> 
> **Alternativní řešení**
> 
> 1. Přihlaste se jako hostitel.
> 2. Přejděte do nabídky hostitel a vyberte **Nastavení hostitele**.
> 3. Přejděte dolů a v části **Upřesnit nastavení**rozbalte položku **Nastavení výkonu**.
> 4. Klikněte na odkaz **Vymazat mezipaměť** pro stránky.
> 5. Přejít do dolní části stránky a restartovat aplikaci.

#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a>Problém: některé odkazy v AtomSite se po stažení publikované lokality poruší.

> **Alternativní řešení**  
> V souboru *Service. config* , *Users. config* a všechny soubory *. XML* nahraďte řetězec adresy URL (například `http://myhost.com/atomsite`) místním souborem (například `http://localhost:1239`).

#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a>Problém: aplikace založené na MySQL, jako je WordPress, se nepodařilo publikovat a nahlásit chybu databáze.

> Ve výchozím nastavení WebMatrix nainstaluje MySQL se znakovou sadou UTF-8. Pokud si MySQL nainstalujete sami a znaková sada není UTF-8 (například je Latin1), může proces publikování pro databáze selhat.
> 
> **Alternativní řešení**
> 
> 1. Změňte znakovou sadu pro MySQL na UTF-8. (Podrobnosti najdete v tématu [znaková sada serveru a kolace](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) na webu MySQL.)
> 2. Přeinstalujte aplikaci.
> 3. Znovu publikujte aplikaci.

#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a>Problém: u aplikací, které mají instalaci prostřednictvím prohlížeče, se nezdařila možnost stáhnout publikovaný web.

> Některé aplikace (například Kentico CMS) vyžadují jejich spuštění v prohlížeči, aby bylo možné provést instalaci po instalaci, jako je například vytvoření databáze. Pokud publikujete aplikaci, například bez dokončení instalace na základě prohlížeče, pokus o stažení stejné lokality ze vzdáleného serveru se nezdaří.
> 
> **Alternativní řešení**  
> Před publikováním webu dokončete instalační program na základě prohlížeče.

#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a>Problém: "stažení publikovaného webu" se nezdařila s chybou databáze pro DotNetNuke a Kooboo CMS

> Pokud se pokusíte stáhnout aplikaci ze serveru a máte přihlašovací údaje správce v připojovacím řetězci databáze v dialogovém okně **publikování nastavení** , může se v protokolu publikování zobrazit následující chyba:
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> **Alternativní řešení**  
> Pokud je to praktické, publikujte lokalitu (nebo ji publikujte) pomocí přihlašovacích údajů bez oprávnění správce pro databázi.

<a id="More_Info"></a>

## <a name="for-more-information"></a>Další informace

Další informace o WebMatrixu 1,0 najdete na následujících webech:

- [IIS.net](http://iis.net/)
- [ASP.NET](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

© 2011 Microsoft Corporation. Všechna práva vyhrazena. [Podmínek použití](https://msdn.microsoft.cos/cc300389.aspx).

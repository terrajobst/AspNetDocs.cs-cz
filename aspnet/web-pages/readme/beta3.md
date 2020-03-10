---
uid: web-pages/readme/beta3
title: Readme (Web Matrix) a ASP.NET Web Pages (Razor) beta 3 pro vydání verze | Microsoft Docs
author: rick-anderson
description: Soubor Readme o nástroji WebMatrix a webových stránkách ASP.NET (Razor) verze Beta 3
ms.author: riande
ms.date: 01/10/2011
ms.assetid: ffa3d5c9-91e5-4da3-b409-560b0c7fbbf0
msc.legacyurl: /web-pages/readme/beta3
msc.type: content
ms.openlocfilehash: dc1d9237c04a7fcdbf4db6ccc8c36d255f6de003
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628896"
---
# <a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a>Soubor Readme o nástroji WebMatrix a webových stránkách ASP.NET (Razor) verze Beta 3

> Soubor Readme o nástroji WebMatrix a webových stránkách ASP.NET (Razor) verze Beta 3

9\. listopadu 2010

## <a name="contents"></a>Obsah

- [Přehled](#Overview)
- [Instalace](#Installation_Notes)
- [Nové funkce, změny a známé problémy ve verzi beta 3](#Known_Issues)

    - [Problémy s instalací WebMatrixu](#Known_Issues_Installation)
    - [Webové stránky ASP.NET](#Known_Issues_ASPNET)
    - [SQL Server Compact](#Known_Issues_SQL_Server_Compact)
    - [Instalace aplikací](#Known_Issues_Installing_Applications)
    - [Publikování aplikací](#Known_Issues_Publishing_Applications)
    - [Další problémy](#Known_Issues_Other_Issues)
- [Další informace](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a>Přehled

> Microsoft WebMatrix beta je bezplatný sada pro vývoj na webu, která se instaluje během několika minut. Integruje webový server s databázovými a programovacími rozhraními k vytvoření jediného integrovaného prostředí. Pomocí WebMatrixu beta můžete zjednodušit způsob, jakým kód, otestujete a publikujete vlastní web ASP.NET nebo PHP, nebo můžete pomocí WebMatrixu beta začít nový web pomocí oblíbených open source aplikací, jako je DotNetNuke, Umbraco, WordPress nebo Joomla. WebMatrix beta používá stejné výkonné prostředí webového serveru, databázového stroje a rozhraní, které spustí vaši webovou stránku na internetu, což usnadňuje přechod od vývoje k produkčnímu a bezproblémovému fungování.

<a id="Installation_Notes"></a>

## <a name="installation"></a>Instalace

> K instalaci WebMatrixu beta 3 použijete [Instalace webové platformy Microsoft 3,0](https://go.microsoft.com/fwlink/?LinkID=194638). Po instalaci instalačního programu webové platformy ho můžete použít k instalaci WebMatrixu beta 3.
> 
> Pokud máte při instalaci problémy, přečtěte si téma [řešení potíží s instalace webové platformy Microsoft](https://go.microsoft.com/fwlink/?LinkId=196212).

<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a>Pokyny k publikování aplikací

> Přečtěte si podrobné [pokyny pro publikování aplikací](https://go.microsoft.com/fwlink/?LinkID=196149) .

<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a>Nové funkce, změny, problémy s andKnown

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a>Instalace WebMatrix beta 3

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a>Problém: WebMatrix beta 3 je dostupný jenom na platformách, které podporují Microsoft .NET Framework 4.

> Pro WebMatrix beta se vyžaduje .NET Framework verze 4. V některých případech se instalační program WebMatrix beta pokusí nainstalovat na platformu, která není součástí podporované konfigurační sady. Konkrétně Windows Vista bez aktualizace SP1 vám umožní zahájit instalaci WebMatrixu beta, ale komponenta .NET Framework 4 selže a zablokuje instalaci.
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

#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a>Problém: nejde nainstalovat WebMatrix beta 3, pokud je nainstalovaná Microsoft Visual Studio 2008 bez Microsoft Visual Studio 2008 SP1.

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

Tato část dokumentu popisuje nové funkce, změny a známé problémy ve verzi beta 3 webových stránek ASP.NET s syntaxe Razor.

- [Nové funkce](#NewFeatures)
- [Provedeny](#Changes)
- [Problémy](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a>Nové funkce ve verzi beta 3 pro webové stránky ASP.NET se syntaxí Razor

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a>Novinka: metoda "HTML. Raw" vykresluje nekódovaný kód

> Nová metoda `Html.Raw` umožňuje vykreslení značky HTML jako značky namísto vykreslování kódovaného výstupu. (Ve výchozím nastavení ASP.NET Razor kóduje řetězce před jejich vykreslením.) Syntaxe je:
> 
> `Html.Raw(value)`
> 
> Následující příklad ukazuje, jak použít `Html.Raw`:
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]

<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a>Změny ve verzi beta 3 pro webové stránky ASP.NET se syntaxí Razor

#### <a name="change-hrefattribute-method-removed"></a>Změna: metoda "HrefAttribute" byla odebrána.

> Metoda `HrefAttribute` třídy `WebPage` byla odebrána. Tato pomoc se použila ke kódování nebezpečných znaků v adresách URL. Již není vyžadován, protože ASP.NET Razor automaticky kóduje řetězce. (K vykreslování nekódovaných řetězců použijte novou metodu `Html.Raw`.)

#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a>Změna: syntaxe deklarativních pomocníků "@helper" se změnila

> Ve verzi beta 3 ASP.NET mění způsob, jakým analyzuje pomocníky vytvořené pomocí syntaxe `@helper`. V podstatě se syntaxe `@helper` nyní analyzuje jako blok kódu namísto jako blok značek, které mohou obsahovat kód. Proto kód uvnitř pomocné rutiny nemusí být uzavřen do `@{ }`ch bloků. V opačném případě se značky uvnitř pomocné rutiny musí explicitně zahrnout do prvků HTML nebo do značek ASP.NET Razor `<text></text>`.
> 
> Například následující syntaxe `@helper` funguje ve verzi beta 3:
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> Ve verzi beta 3 se tato pomocná Nápověda musí změnit tak, aby vypadala jako v následujícím příkladu:
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> Všimněte si, že `@{ }` znaky kolem počátečního kódu v pomocné rutině již nejsou používány. Důvodem je to, že obsah pomocníků je ve výchozím nastavení považován za blok kódu. Pomocné rutiny vykresluje kód, který začíná otevírací `<a>`ovou značkou. Pokud musí pomoc vykreslovat prostý text nebo značky, které neobsahují uzavírací značku (například `<meta>` značky), musí být obsah, který se má vykreslit, v `<text></text>` značek.

#### <a name="change-webpagecontexthttpcontext-removed"></a>Změna: WebPageContext. HttpContext se odstranilo.

> Vlastnost `WebPageContext.HttpContext` byla odebrána. Místo toho použijte `HttpContext.Current`. (Vlastnost `WebPageContext.HttpContext` jednoduše zabalené.)

#### <a name="change-facebook-helper-moved-to-new-package"></a>Změna: Pomocník pro Facebook se přesunul do nového balíčku.

> Pomocná rutina `Facebook` byla přesunuta do knihovny *Facebook. Helper* , která obsahuje nápovědu `Facebook` a další funkce. Tuto knihovnu musíte nainstalovat jako samostatný balíček, jak je popsáno v tématu "instalace pomocníků se správcem balíčků" v kurzu [Začínáme se stránkami ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202889).

#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a>Změna: typy členství, rolí a zabezpečení se přesunou do nového sestavení.

> Následující typy byly přesunuty do sestavení `WebMatrix.WebData`:
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`

#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a>Change: třída "TagBuilder" přesunutá na sestavení System. Web. webpages. dll

> Třída `TagBuilde` r byla přesunuta do sestavení System. Web. webpages. dll. Dřív to bylo v sestavení, které bylo součástí ASP.NET MVC. Tato změna znamená, že nemusíte instalovat ASP.NET MVC, aby bylo možné použít třídu `TagBuilder`.
> 
> Nicméně třída je stále v oboru názvů `System.Web.Mvc`. Aby bylo možné použít třídu `TagBuilder` (například ve vlastním Pomocníkovi ASP.NET Razor), musíte odkazovat na obor názvů (například přidáním `@using System.Web.Mvc` do kódu).

#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a>Změna: syntaxe ověření žádosti se změnila; Odstranila se třída "ověření".

> Chcete-li zakázat ověřování pro jednotlivá pole nebo sadu polí ve verzi beta 3, můžete zavolat metodu `Validation.Exclude` a předat název nebo názvy polí, které mají být vyloučeny z ověřování. V rámci verze beta 3 je k dispozici nová syntaxe pro obejít ověření. Byla odstraněna metoda `Validation` použitá v beta verzi 3.
> 
> > [!NOTE]
> > Pokud nezakážete ověření žádosti, pokud se uživatelé pokusí odeslat kód HTML (například pomocí editoru formátovaného textu na stránce), bude webová stránka hlásit chybu, jako *je potenciálně nebezpečná žádost. z klienta byla zjištěna hodnota formuláře* a vstup uživatele není přijat. Pokud zakážete ověření žádosti, musíte ručně zkontrolovat vstup uživatele, abyste se ujistili, že neobsahují potenciálně nebezpečné značky nebo skripty, a to jako v případě [knihovny Microsoft Anti-průřezing Scripting Library v 4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651).
> 
> 
> Chcete-li zakázat automatické ověřování žádostí, zavolejte metodu `Request.Unvalidated`, předejte jí název pole nebo jiný objekt post, pro který chcete obejít ověření žádosti. Tuto metodu můžete použít k obejít ověřování pro jakékoli položky v `Form`, `QueryString`, `Cookies`a `ServerVariables` kolekcích. Následující příklady ukazují, jak používat metodu `Unvalidated`:
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]

<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a>Známé problémy pro webové stránky ASP.NET se syntaxí Razor

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a>Problém: neočekávané chování při použití vlastní uživatelské tabulky pro členství

> Chcete-li inicializovat poskytovatele členství pro web ASP.NET Razor, zavoláte metodu `WebSecurity.InitializeDatabaseConnection`. (Ve webové matici úvodní šablona webu obsahuje volání této metody v souboru *\_AppStart. cshtml* .) Pokud je parametr `autoCreateTables` této metody nastaven na hodnotu true (ve výchozím nastavení je nastaven na hodnotu true v šabloně počátečního webu) a pokud je do metody (druhý parametr) předána nerozpoznaný název tabulky, metoda nevyvolá chybu. Místo toho se tabulka automaticky vytvoří.
> 
> To může být problém, pokud máte v úmyslu použít pro členství vlastní uživatelskou tabulku, ale předat do metody `WebSecurity.InitializeDatabaseConnection` špatný název tabulky. Vzhledem k tomu, že metoda není ve výchozím nastavení vyvolána, pokud zadaná tabulka neexistuje a protože místo toho vytvoří novou tabulku, aplikace může vypadat, že bude fungovat. Nicméně kód aplikace, který závisí na vlastní uživatelské tabulce (a u polí v ní), může nakonec selhat s neočekávanými chybami.
> 
> **Alternativní řešení**  
> Ujistěte se, že název předaný v metodě `InitializeDatabaseConnection` odpovídá tabulce profilů uživatele v databázi členství, nebo se ujistěte, že parametr `autoCreateTables` je nastaven na hodnotu false.

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a>Problém: nepovedlo se vygenerovat uživatelskou instanci SQL Server, chyba.

> Pokud webová aplikace WebMatrix používá SQL Server Express a je v systému Windows 7 nebo Windows Server 2008 R2 spuštěna služba IIS 7,5, může se zobrazit chyba, která indikuje, že SQL Server během běhu nemůže načíst cestu k místní aplikaci uživatele.
> 
> **Alternativní řešení** Ujistěte se, že účet systému Windows, pod kterým je aplikace spuštěna (obvykle síťová služba), má oprávnění ke čtení a zápisu pro kořenové složky aplikace a pro podsložky, jako jsou například *data aplikace\_* . Podrobnější informace jsou k dispozici v článku znalostní báze [problémy s SQL Server Expressmi vytvářením uživatelských instancí a projektů webových aplikací ASP.NET](https://support.microsoft.com/kb/2002980).

#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a>Problém: v aplikaci Visual Studio se obory názvů pro vlastní sestavení (DLL) neimportují automaticky

> Použijete-li vlastní sestavení v projektu v aplikaci Visual Studio, obory názvů deklarované v těchto sestaveních nejsou automaticky importovány v době návrhu. V důsledku toho se odkazy na vlastní typy nemusí rozpoznat v době návrhu a jsou označeny jako nerozpoznané v sadě Visual Studio (pomocí "vlnovek"). K tomuto problému dochází pouze v době návrhu v aplikaci Visual Studio; aplikace sama funguje správně.
> 
> **Alternativní řešení**  
> Zahrňte příkaz `using` (`imports` v Visual Basic), který odkazuje na entity, které nejsou v době návrhu rozpoznány.

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a>Problém: Visual Studio IntelliSense a šablony projektů dostupné jenom ve ASP.NET MVC verze 3

> Při instalaci webových stránek ASP.NET se také neinstalují nástroje pro Visual Studio, jako jsou IntelliSense a šablony projektů pro aplikace ASP.NET Web Pages.
> 
> **Alternativní řešení** Chcete-li používat IntelliSense a šablony projektů pro aplikace ASP.NET Web Pages v aplikaci Visual Studio, nainstalujte ASP.NET MVC 3 RC buď prostřednictvím instalačního programu webové platformy, nebo pomocí [samostatného instalačního programu](https://go.microsoft.com/fwlink/?LinkID=191797).

#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a>Problém: nepovedlo se najít&gt; třídu&lt;Helper, chyba.

> Po upgradu na verzi beta 3 se může zobrazit chyba, že pomocná třída (například třída `Facebook`) nebyla nalezena. Od verze beta 2 a pokračování ve verzi beta 3 se pomocníki přesunuli na balíčky, které musíte explicitně nainstalovat. Existující weby nejsou upgradovány, aby zahrnovaly tyto balíčky. To zahrnuje weby ve složkách *\My Documents\IISExpress* nebo *\Dokumenty Documents\My Web Sites* . Konkrétně se zobrazí tato chyba, pokud použijete výchozí web na *stránce moje weby* (WEB1), který obsahuje odkaz na pomocnou nápovědu `Twitter`.
> 
> **Alternativní řešení**  
> Zakomentujte volání libovolných pomocníků v lokalitě, spusťte stránku *\_admin* a nainstalujte balíček nebo balíčky, které obsahují pomocníky, které chcete použít. Po instalaci balíčku můžete odkomentovat řádky, které odkazují na pomocníka.

#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a>Problém: nasazení sestavení beta 3 ASP.NET Razor do složky bin nemusí fungovat na hostitelských webech

> Pokud nasadíte web ASP.NET Web Pages na hostující web a pokud nasadíte sestavení ASP.NET Razor beta 3 do složky *bin* webu, může docházet k chybám, včetně následujících:
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> K tomu může dojít, pokud poskytovatel hostingu nainstaloval sestavení ASP.NET Web Pages beta 1 do globální mezipaměti aplikace serveru (GAC). Sestavení v mezipaměti GAC mají přednost před sestaveními nainstalovanými místně ve složce *bin* .
> 
> **Alternativní řešení** Obraťte se na svého poskytovatele hostingu a ověřte, že chyby, které vidíte, jsou způsobeny konfliktem mezi verzemi sestavení a vaší verze poskytovatele. Pokud ano, požádejte poskytovatele hostingu, aby aktualizoval sestavení v mezipaměti GAC serveru.

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a>Problém: čtení informačních kanálů nebo jiných externích dat prostřednictvím proxy server

> Pokud je server, na kterém je spuštěná lokalita, za proxy server, může být nutné nakonfigurovat informace o proxy serveru v souboru *Web. config* , aby bylo možné číst informace, které pocházejí z mimo vaši lokalitu. Pokud například použijete pomocníka `ReCaptcha`, pomáhající osoba komunikuje se službou reCAPTCHA, ale může být blokována proxy server. Podobně kanály, které se používají v ASP.NET webové stránky, jako je informační kanál používaný správcem balíčků, můžou vyžadovat konfiguraci proxy serveru.
> 
> Pokud dochází k potížím při práci s externí službou nebo při práci s kanálem balíčku, vložte následující prvky do kořenového souboru *Web. config* vaší aplikace:
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> Další informace o konfiguraci proxy server najdete v tématu [&lt;proxy&gt; elementu (nastavení sítě)](https://msdn.microsoft.com/library/sa91de1e.aspx) na webu MSDN.

#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a>Problém: Chyba "Microsoft. Web. Infrastructure. dll" nelze načíst "

> Pokud jste dříve nainstalovali verzi beta 1 webových stránek ASP.NET pomocí nástroje syntaxe Razor a potom nainstalujete verzi beta 3, všechna příslušná sestavení jsou nainstalována v globální mezipaměti sestavení (GAC), s výjimkou *Microsoft. Web. Infrastructure. dll*. V takovém případě se při spuštění ASP.NET Razor Pages zobrazí chyba, která indikuje, že se nepovedlo načíst *Microsoft. Web. Infrastructure. dll* .
> 
> K tomuto problému dochází, pokud jste načetli verzi beta 3 na čistý počítač.
> 
> **Alternativní řešení**  
> V Ovládacích panelech odinstalujte webové stránky ASP.NET. Pak přeinstalujte verzi beta 3.

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a>Problém: Odinstalace .NET Framework verze 4: zakáže webové stránky ASP.NET se syntaxí Razor.

> Pokud odinstalujete .NET Framework verze 4 a pak ji znovu nainstalujete, ASP.NET webové stránky s syntaxe Razor jsou zakázané. Stránky s příponou *. cshtml* neběží správně. Webové stránky ASP.NET registrují sestavení v kořenovém souboru *Web. config* počítače a odebrání .NET Framework Tento soubor odebere. Opětovná instalace .NET Framework nainstaluje novou verzi konfiguračního souboru, ale nepřidá odkaz pro sestavení webových stránek ASP.NET.
> 
> **Alternativní řešení** Po přeinstalaci .NET Framework přeinstalujte webové stránky ASP.NET pomocí syntaxe Razor. Tím se do souboru *Web. config* přidá následující element v kořenovém adresáři počítače, který je obvykle v následujícím umístění:  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> 
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]

#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a>Problém: aplikace dřív nasazené se ASP.NET sestaveními ve složce Bin se objeví chyby.

> Během nasazování kopíruje kopie sestavení webových stránek ASP.NET (například *Microsoft. webpages. dll*) do složky *bin* webu na serveru. (K této situaci mohlo dojít automaticky během nasazování nebo proto, že vývojář explicitně zkopíroval sestavení.) Pokud je však nainstalována verze beta 3, dojde k chybám, například chybám, které nebyly nalezeny pro určité typy. K tomu dochází, protože počet typů webových stránek ASP.NET byl přesunut do různých oborů názvů pro verzi beta 3.
> 
> **Alternativní řešení**   
> Vymažte složku *bin* nasazené aplikace, zkopírujte nová sestavení do složky (nebo aplikaci znovu nasaďte) a pak aplikaci spusťte znovu.

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
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]

#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a>Problém: použití projektu webové aplikace nebo ASP.NET MVC a ASP.NET webových stránek ve stejné aplikaci

> Pokud jste používali webové stránky v ASP.NET v projektu webové aplikace nebo v aplikaci ASP.NET MVC, může se zobrazit chyba, kterou *WebPageHttpApplication* nelze najít.
> 
> **Alternativní řešení**  
> Pokud se zobrazí tato chyba, změňte základní třídu, ze které je aplikace odvozena. V souboru *Global. asax* změňte následující řádek:
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> K tomuto:
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> To v důsledku toho obrátí změnu, která byla představena pro ASP.NET webové stránky verze beta 1 s syntaxe Razor.

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a>Problém: nasazení aplikace do počítače, ve kterém není nainstalovaná SQL Server Compact

> Aplikace, které zahrnují SQL Server Compact databáze, mohou běžet v počítači, kde není nainstalován SQL Server Compact. Microsoft WebMatrix beta 3 automaticky zkopíruje tyto binární soubory a provede příslušné transformace souboru *Web. config* .
> 
> **Alternativní řešení** Pokud potřebujete tyto soubory zkopírovat a provést změny v souboru *Web. config* ručně, postupujte následovně:
> 
> 1. Zkopírujte sestavení databázového stroje do složky *bin* (a podsložek) aplikace v cílovém počítači: 
> 
>     - Kopírování *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.data.SqlServerCe.dll* **do** *\Bin*
>     - Kopírování *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* * **do** *\Bin\x86*
>     - Kopírování *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* * **do** *\Bin\amd64*
> 2. V kořenové složce webu vytvořte nebo otevřete soubor *Web. config* . (Ve WebMatrixu beta 3 je tento typ souboru k dispozici, pokud kliknete na tlačítko **vše** v dialogovém okně **zvolit typ souboru** .)
> 3. Přidejte následující prvek jako podřízený prvek **&lt;konfigurace&gt;** (není uvnitř elementu **&lt;system. Web&gt;** ):
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a>Problém: pomocníka databáze a WebGrid nefungují v nestředním vztahu důvěryhodnosti v Visual Basic

> Pokud používáte Visual Basic (vytváření souborů *. vbhtml* ), `Database` a `WebGrid` pomocníka nebudou fungovat, pokud je aplikace nastavená tak, aby používala střední důvěryhodnost.
> 
> **Alternativní řešení**  
> Dočasně nastavte aplikaci tak, aby používala úplný vztah důvěryhodnosti.

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a>SQL Server Compact

#### <a name="issue-encrypt-property-is-not-recognized"></a>Problém: vlastnost Encrypt není rozpoznaná.

> SQL Server Compact 4,0 nerozpozná vlastnost `Encrypt` třídy `SqlCeConnection`. Tuto vlastnost byste neměli používat k šifrování souborů databáze. Vlastnost `Encrypt` se v SQL Server Compact 3,5 verze nepoužívá a byla zachována pouze z důvodu zpětné kompatibility. 
> 
> **Alternativní řešení**  
> Pomocí vlastnosti `Encryption Mode` třídy `SqlCeConnection` Zašifrujte soubory databáze SQL Server Compact 4,0. Následující příklad ukazuje, jak vytvořit šifrované databáze SQL Server Compact 4,0 pomocí vlastnosti `Encryption Mode`:
> 
> [!code-csharp[Main](beta3/samples/sample11.cs)]
> 
> [!code-vb[Main](beta3/samples/sample12.vb)]
> 
> Chcete-li změnit režim šifrování existující databáze SQL Server Compact 4,0, postupujte následovně:
> 
> [!code-csharp[Main](beta3/samples/sample13.cs)]
> 
> [!code-vb[Main](beta3/samples/sample14.vb)]
> 
> K šifrování nešifrované databáze SQL Server Compact 4,0 postupujte takto:
> 
> [!code-csharp[Main](beta3/samples/sample15.cs)]
> 
> [!code-vb[Main](beta3/samples/sample16.vb)]

#### <a name="issue-microsoft-visual-c-2008-runtime-libraries-are-required"></a>Problém: vyžadují se C++ knihovny modulu runtime Microsoft Visual 2008.

> Nativní knihovny DLL SQL Server Compact 4,0 potřebují knihovny runtime Microsoft Visual C++ 2008 (x86, IA64 a x64) s aktualizací Service Pack 1.
> 
> **Alternativní řešení**  
> Nainstalujte .NET Framework 3,5 SP1. Tím se také nainstaluje knihovny C++ Runtime Visual 2008 runtime SP1. Knihovny si můžete stáhnout z následujícího umístění:   
>   
> [Microsoft Visual C++ 2008 Service Pack 1 Redistributable Package aktualizace zabezpečení knihovny ATL](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> Všimněte si, že při instalaci .NET Framework 2,0, 3,0 nebo 4 *se neinstalují* knihovny C++ runtime Visual 2008 SP1.

#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a>Problém: Pokud je SQL Server Compact nainstalován před instalací nástroje .NET Framework na počítači, není v souboru .NET Framework Machine. config registrován jeho neutrální název poskytovatele.

> SQL Server Compact lze nainstalovat do počítače, který nemá .NET Framework nainstalován, protože SQL Server Compact vyžaduje rozhraní .NET Framework. Pokud před instalací SQL Server Compact není nainstalovaná žádná .NET Framework verze 3,5 ani 4, instalační program SQL Server Compact neregistruje v souboru *Machine. config* jeho nevariantní poskytovatele. Žádná aplikace, která spoléhá na položku SQL Server Compact v souboru *Machine. config* , se nezdaří. Položka registrace neutrálního názvu v *souboru Machine. config* vypadá jako v následujícím příkladu:
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> **Alternativní řešení**  
> Odinstalujte SQL Server Compact 4,0 CTP1. Z následujícího umístění si stáhněte a nainstalujte plné verze .NET Framework:
> 
> [Microsoft .NET Framework 3,5 Service Pack 1 (úplný balíček)](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [Verze Microsoft .NET Framework 4,0 (úplný balíček)](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> Pak přeinstalujte [SQL Server Compact 4,0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en).

<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a>Instalace aplikací

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a>Problém: instalace aplikace může trvat dlouhou dobu, pokud se složka Dokumenty uživatele přesměruje na sdílenou síťovou složku.

> **Alternativní řešení**  
> Žádné. Instalace aplikace může nějakou dobu trvat, ale nainstaluje se správně.

<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a>Publikování aplikací

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

<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a>Další problémy

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a>Problém: v sestavách pro Group by nefunguje hledání nebo filtr: typ problému

> Pokud spustíte sestavu pro lokalitu, zadáte text do pole *filtrovat podle adresy URL* a kliknete na tlačítko *Hledat*, nic se nestane. Důvodem je to, že tento ovládací prvek není funkční, pokud je stav *Seskupit podle* sestavy nastaven na *typ vystavení*, což je výchozí hodnota.
> 
> **Alternativní řešení** Na kartě *Seskupit podle* na pásu karet klikněte na možnost *Adresa URL* a seskupte položky podle jejich zdrojové adresy URL. Textové pole a tlačítko pro filtrování položek je funkční v tomto stavu.

#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a>Problém: aplikace WCF selhaly při spuštění s IIS Express

> Při procházení aplikace WCF dojde k chybě podobné následujícímu:
> 
> *Nelze načíst soubor nebo sestavení Microsoft. Web. Administration, Version = 7.0.0.0, Culture = neutral, PublicKeyToken = 31bf3856ad364e35 nebo jedna z jejích závislostí. Systém nemůže najít zadaný soubor.*
> 
> K tomu dochází, protože IIS Express beta verze standardně nepodporuje WCF.
> 
> **Alternativní řešení** Použijte jedno z následujících řešení (alternativní řešení #2 vyžaduje Microsoft Windows Vista nebo novější):
> 
> 
> 1. Zkopírujte sestavení *Microsoft. Web. dll* a *Microsoft. Web. Administration. dll* z umístění instalace WebMatrix do adresáře *bin* aplikace WCF. Ve výchozím nastavení je WebMatrix nainstalovaný v podsložce *WebMatrixu Microsoftu* ve složce *Program Files (Program Files* ) systému.
> 2. V systému Microsoft Windows Vista nebo novějším vytvořte symlink do sestavení v adresáři *bin* pomocí následujících příkazů. (Tento přístup má výhodu, že nevytváří kopii sestavení.)
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. Nainstalujte dvě sestavení v globální mezipaměti sestavení (GAC). Na příkazovém řádku se zvýšenými oprávněními spusťte následující příkazy:
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]

#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a>Problém: WebMatrix beta 3 není schopen provádět určité úlohy, které vyžadují zvýšení úrovně oprávnění.

> WebMatrix beta 3 není schopen provádět určité úlohy, které vyžadují zvýšení oprávnění, jako je například instalace dalších součástí v následujících situacích:
> 
> - V systému Windows Vista nebo Windows 7 jste přihlášeni pomocí účtu, který nemá oprávnění správce a nástroj řízení uživatelských účtů (UAC) je zakázán.
> - Používáte Microsoft Windows XP nebo Microsoft Windows Server 2003.
> 
> **Alternativní řešení**  
> Většina úkolů v WebMatrixu beta 3 nevyžaduje oprávnění správce. V případě, že to uděláte, můžete tuto operaci provést jako správce nebo postupovat podle následujících kroků:
> 
> - V systému Windows Vista nebo Windows 7 povolte nástroj řízení uživatelských účtů.
> - V systému Windows XP přidejte uživatele do skupiny zabezpečení Správci.

#### <a name="issue-site-from-web-gallery-is-disabled"></a>Problém: lokalita z webové galerie je zakázaná.

> Možnost **web z Galerie webu** je zakázána, pokud není nainstalována instalace webové platformy 3,0.
> 
> **Alternativní řešení**  
> Nainstalujte [Instalace webové platformy Microsoft 3,0](https://go.microsoft.com/fwlink/?LinkID=194638).

#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a>Problém: v systému Windows Server 2003 se IIS Express nespouštějí pro uživatele bez oprávnění správce.

> Pokud na Windows serveru 2003 spustíte stránku nebo spustíte IIS Express, IIS Express se nespustí. U webových stránek se zobrazí chyba, která indikuje, že aplikace byla spuštěna uživatelem bez oprávnění správce.
> 
> **Alternativní řešení**  
> Spusťte WebMatrix beta 3 jako uživatel s právy pro správu. Další podrobnosti najdete v následujícím článku znalostní báze:  
>   
> [Aplikace, kterou spouští uživatel bez oprávnění správce, nemůže naslouchat přenosu HTTP počítače, na kterém je aplikace spuštěná v systému Windows Vista, Windows Server 2003 nebo Windows XP.](https://support.microsoft.com/kb/939786)

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

#### <a name="issue-the-relationships-button-is-disabled"></a>Problém: tlačítko relace je zakázané.

> Tlačítko **relace** na kartě **tabulka** v pracovním prostoru **databáze** je pro databáze SQL Server Compact zakázané.
> 
> **Alternativní řešení**  
> Žádné. SQL Server Compact nepodporuje relace mezi tabulkami.

#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a>Problém: parametrizované dotazy SQL vyvolávají výjimky

> Pokud v SQL Server Compact 4,0 neurčíte datový typ, například `SqlDbType` nebo `DbType` pro parametry v parametrizovaných dotazech, je vyvolána výjimka při spuštění dotazu.
> 
> **Alternativní řešení**  
> Explicitně nastavte datový typ pro parametry, jako je `SqlDbType` nebo `DbType`. To je důležité v případě datových typů objektů BLOB (`image` a `ntext`). Použijte kód podobný následujícímu:
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
> 
> [!code-vb[Main](beta3/samples/sample21.vb)]

<a id="More_Info"></a>

## <a name="for-more-information"></a>Další informace

Další informace o WebMatrixu beta 3 najdete na následujících webech:

- [IIS.net](http://iis.net/)
- [ASP.NET](https://asp.net/webmatrix)
- [Microsoft.com/web](https://www.microsoft.com/web)

---

© 2010 Microsoft Corporation. Všechna práva vyhrazena. [Podmínek použití](https://msdn.microsoft.cos/cc300389.aspx).

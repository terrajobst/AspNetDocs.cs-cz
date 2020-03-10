---
uid: whitepapers/aspnet4/breaking-changes
title: ASP.NET 4 průlomové změny | Microsoft Docs
author: rick-anderson
description: Tento dokument popisuje změny, které byly provedeny pro verzi .NET Framework verze 4, která může potenciálně ovlivnit aplikace, které byly vytvořeny pomocí...
ms.author: riande
ms.date: 02/10/2010
ms.assetid: d601c540-f86b-4feb-890c-20c806b3da6c
msc.legacyurl: /whitepapers/aspnet4/breaking-changes
msc.type: content
ms.openlocfilehash: 8ccad3b40a723c92a3164de082e1f94577141008
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78546247"
---
# <a name="aspnet-4-breaking-changes"></a>ASP.NET 4 – nejnovější změny

> Tento dokument popisuje změny, které byly provedeny pro verzi .NET Framework verze 4, které mohou mít potenciálně vliv na aplikace vytvořené pomocí dřívějších verzí, včetně verzí ASP.NET 4 beta 1 a beta 2.
> 
> [Stáhnout tento dokument White Paper](https://download.microsoft.com/download/7/1/A/71A105A9-89D6-4201-9CC5-AD6A3B7E2F22/ASP_NET_4_Breaking_Changes.pdf)

<a id="0.1__Toc256768952"></a><a id="0.1__Toc256770056"></a>

## <a name="contents"></a>Obsah

[Nastavení ControlRenderingCompatibilityVersion v souboru Web. config](#0.1__Toc256770141 "_Toc256770141")  
[ClientIDMode změny](#0.1__Toc256770142 "_Toc256770142")  
[HtmlEncode a UrlEncode teď zakódují jednoduché uvozovky.](#0.1__Toc256770143 "_Toc256770143")  
[ASP.NET stránka (. aspx) je přísnější](#0.1__Toc256770144 "_Toc256770144")  
[Aktualizované soubory definice prohlížeče](#0.1__Toc256770145 "_Toc256770145")  
[Soubor System. Web. Mobile. dll byl odebrán z kořenového konfiguračního souboru webu](#0.1__Toc256770146 "_Toc256770146")  
[Ověření žádosti ASP.NET](#0.1__Toc256770147 "_Toc256770147")  
[Výchozí algoritmus hash je teď HMACSHA256](#0.1__Toc256770148 "_Toc256770148")  
[Chyby konfigurace související s novou kořenovou konfigurací ASP.NET 4](#0.1__Toc256770149 "_Toc256770149")  
[ASP.NET 4 podřízené aplikace se nespustí, když jsou v aplikacích ASP.NET 2,0 nebo ASP.NET 3,5.](#0.1__Toc256770150 "_Toc256770150")  
[Weby ASP.NET 4 se nedaří spustit na počítačích, na kterých je nainstalována služba SharePoint.](#0.1__Toc256770151 "_Toc256770151")  
[Vlastnost HttpRequest. FilePath už neobsahuje PathInfo hodnoty.](#0.1__Toc256770152 "_Toc256770152")  
[Aplikace ASP.NET 2,0 můžou generovat chyby HttpException –, které odkazují na eurl. axd.](#0.1__Toc256770153 "_Toc256770153")  
[Obslužné rutiny událostí nemusí být vyvolány ve výchozím dokumentu v integrovaném režimu služby IIS 7 nebo IIS 7,5.](#0.1__Toc256770154 "_Toc256770154")  
[Změny implementace ASP.NET Code Access Security (CAS)](#0.1__Toc256770155 "_Toc256770155")  
[MembershipUser a další typy v oboru názvů System. Web. Security byly přesunuty.](#0.1__Toc256770156 "_Toc256770156")  
[Změny v ukládání výstupu do mezipaměti se liší \* hlavičce protokolu HTTP](#0.1__Toc256770157 "_Toc256770157")  
[Typy System. Web. Security pro Passport jsou zastaralé.](#0.1__Toc256770158 "_Toc256770158")  
[Vlastnost MenuItem. PopOutImageUrl nemůže vykreslit image v ASP.NET 4.](#0.1__Toc256770159 "_Toc256770159")  
[Nabídka. StaticPopOutImageUrl a menu. DynamicPopOutImageUrl se nepodaří vykreslit obrázky, když cesty obsahují zpětná lomítka.](#0.1__Toc256770160 "_Toc256770160")  
[Právní omezení](#0.1__Toc256770161 "_Toc256770161")

<a id="0.1__ControlRenderingCompatibilityVersio"></a><a id="0.1__Toc245724853"></a><a id="0.1__Toc255587630"></a><a id="0.1__Toc256770141"></a>

## <a name="controlrenderingcompatibilityversion-setting-in-the-webconfig-file"></a>Nastavení ControlRenderingCompatibilityVersion v souboru Web. config

Ovládací prvky ASP.NET byly upraveny ve verzi .NET Framework 4, aby bylo možné zadat přesnější způsob, jak vykreslovat značky. V předchozích verzích .NET Framework některé ovládací prvky vygenerovaly značky, které jste nemuseli zakázat. Ve výchozím nastavení se ASP.NET 4 tento typ značky již negeneruje.

Pokud používáte Visual Studio 2010 k upgradu aplikace z ASP.NET 2,0 nebo ASP.NET 3,5, nástroj automaticky přidá nastavení do souboru `Web.config`, který zachovává starší vykreslování. Pokud však provedete upgrade aplikace tím, že změníte fond aplikací ve službě IIS tak, aby byl cílen na .NET Framework 4, ASP.NET ve výchozím nastavení použije nový režim vykreslování. Chcete-li zakázat nový režim vykreslování, přidejte do souboru `Web.config` následující nastavení:

[!code-xml[Main](breaking-changes/samples/sample1.xml)]

Hlavní vykreslování změny, které přináší nové chování, jsou následující:

- Ovládací prvky **Image** a **obrázkové** již nevykreslují atribut `border="0"`.
- Třída **BaseValidator** a ověřovací ovládací prvky, které jsou z něho odvozené, již ve výchozím nastavení nevykresluje červený text.
- Ovládací prvek **HtmlForm** nevykresluje atribut **Name** .
- Ovládací prvek **tabulka** již nevykresluje atribut `border="0"`.
- Ovládací prvky, které nejsou navrženy pro vstup uživatele (například ovládací prvek **popisek** ) již nevykreslují atribut `disabled="disabled"`, pokud je vlastnost **Enabled** nastavena na **hodnotu false** (nebo pokud dědí toto nastavení z ovládacího prvku kontejneru).

<a id="0.1__Toc245724854"></a><a id="0.1__Toc255587631"></a><a id="0.1__Toc256770142"></a>

## <a name="clientidmode-changes"></a>ClientIDMode změny

Nastavení **ClientIDMode** v ASP.NET 4 umožňuje určit, jak ASP.NET generuje atribut **ID** pro prvky jazyka HTML. V předchozích verzích ASP.NET byl výchozí chování ekvivalentní s nastavením **AutoID** **ClientIDMode**. Výchozí nastavení je však nyní **předvídatelné**.

Použijete-li sadu Visual Studio 2010 k upgradu aplikace z ASP.NET 2,0 nebo ASP.NET 3,5, nástroj automaticky přidá do souboru `Web.config` nastavení, které zachovává chování předchozích verzí .NET Framework. Pokud však provedete upgrade aplikace tím, že změníte fond aplikací ve službě IIS tak, aby byl cílen na .NET Framework 4, ASP.NET ve výchozím nastavení použije nový režim. Chcete-li zakázat nový režim ID klienta, přidejte do souboru `Web.config` následující nastavení:

[!code-xml[Main](breaking-changes/samples/sample2.xml)]

<a id="0.1__Toc245724855"></a><a id="0.1__Toc255587632"></a><a id="0.1__Toc256770143"></a>

## <a name="htmlencode-and-urlencode-now-encode-single-quotation-marks"></a>HtmlEncode a UrlEncode teď zakódují jednoduché uvozovky.

V ASP.NET 4 byly aktualizovány metody **HtmlEncode** a **UrlEncode** tříd **HttpUtility** a **HttpServerUtility** , aby se zakódovat znak jednoduché uvozovky (') následujícím způsobem:

- Metoda **HtmlEncode** kóduje instance jednoduché uvozovky jako.
- Metoda **UrlEncode** kóduje instance jednoduché uvozovky jako %27.

<a id="0.1__Toc255587633"></a><a id="0.1__Toc256770144"></a><a id="0.1__Toc245724856"></a>

## <a name="aspnet-page-aspx-parser-is-stricter"></a>ASP.NET stránka (. aspx) je přísnější

Analyzátor stránky pro ASP.NET stránky (soubory`.aspx`) a uživatelské ovládací prvky (soubory`.ascx`) jsou v ASP.NET 4 přísnější a zamítnou více instancí neplatných značek. Například následující dva fragmenty by úspěšně analyzovaly v dřívějších verzích ASP.NET, ale nyní budou generovat chyby analyzátoru v ASP.NET 4.

[!code-aspx[Main](breaking-changes/samples/sample3.aspx)]

Všimněte si, že na konci značky **HiddenField** je neplatný středník.

[!code-aspx[Main](breaking-changes/samples/sample4.aspx)]

Všimněte si neuzavřeného atributu **style** , který se spouští do atributu **CssClass** .

<a id="0.1__Toc255587634"></a><a id="0.1__Toc256770145"></a>

## <a name="browser-definition-files-updated"></a>Aktualizované soubory definice prohlížeče

Soubory definic prohlížeče byly aktualizovány tak, aby obsahovaly informace o nových a aktualizovaných prohlížečích a zařízeních. Odebraly se starší prohlížeče a zařízení, jako je například Netscape Navigator, a přidaly se novější prohlížeče a zařízení, jako je Google Chrome a Apple iPhone.

Pokud vaše aplikace obsahuje vlastní definice prohlížečů, které dědí z jedné z odebraných definic prohlížeče, zobrazí se chyba. Pokud například složka `App_Browsers` obsahuje definici prohlížeče, která dědí z definice prohlížeče IE2, zobrazí se následující chybová zpráva konfigurace:

- Nebyl nalezen element prohlížeče nebo brány s ID ' IE2 '.

> [!NOTE]
> Objekt **HttpBrowserCapabilities** (který je vystavený vlastností **Request. browser** stránky) je řízen soubory definic prohlížeče. Proto se informace vrácené přístupem k vlastnosti tohoto objektu v ASP.NET 4 mohou lišit od informací vrácených v dřívější verzi ASP.NET.

Původní soubory definice prohlížeče se můžete vrátit tak, že zkopírujete soubory definice prohlížeče z následující složky:

[!code-console[Main](breaking-changes/samples/sample5.cmd)]

Zkopírujte soubory do odpovídající složky `\CONFIG\Browsers` ASP.NET 4. Po zkopírování souborů spusťte nástroj příkazového řádku ASPNET\_regbrowsers. exe.

<a id="0.1__Toc255587635"></a><a id="0.1__Toc256770146"></a>

## <a name="systemwebmobiledll-removed-from-root-web-configuration-file"></a>Soubor System. Web. Mobile. dll byl odebrán z kořenového konfiguračního souboru webu

V předchozích verzích nástroje ASP.NET byl odkaz na sestavení System. Web. Mobile. dll zahrnut do kořenového `Web.config` souboru v části **sestavení** v části. Aby bylo možné zvýšit výkon, byl odebrán odkaz na toto sestavení.

Sestavení System. Web. Mobile. dll je součástí ASP.NET 4, ale je zastaralé. Chcete-li použít typy ze sestavení System. Web. Mobile. dll, přidejte odkaz na toto sestavení buď do kořenového `Web.config` souboru, nebo do souboru `Web.config` aplikace. Například pokud chcete použít některý z (nepoužívané) ASP.NET mobilní ovládací prvky, musíte do souboru `Web.config` přidat odkaz na sestavení System. Web. Mobile. dll.

<a id="0.1__Toc245724857"></a><a id="0.1__Toc255587636"></a><a id="0.1__Toc256770147"></a>

## <a name="aspnet-request-validation"></a>Ověření žádosti ASP.NET

Funkce ověření žádosti v ASP.NET poskytuje určitou úroveň výchozí ochrany proti útokům prostřednictvím skriptování mezi weby (XSS). V předchozích verzích ASP.NET byl standardně povolen ověřovací požadavek. Nicméně se aplikuje jenom na stránky ASP.NET (`.aspx` soubory a jejich soubory třídy) a jenom v případě, že byly tyto stránky spuštěné.

V ASP.NET 4 je ve výchozím nastavení povolená žádost o ověření pro všechny požadavky, protože je povolená před fází **beginRequest** požadavku HTTP. V důsledku toho se ověření žádosti vztahuje na požadavky pro všechny ASP.NET prostředky, nikoli jenom na žádosti stránky ASPX. To zahrnuje požadavky, jako jsou volání webové služby a vlastní obslužné rutiny HTTP. Ověření žádosti je také aktivní, když vlastní moduly HTTP čtou obsah požadavku HTTP.

V důsledku toho se teď můžou vyskytnout chyby ověřování u požadavků, u kterých se dřív neaktivovaly chyby. Chcete-li se vrátit k chování funkce ověření žádosti ASP.NET 2,0, přidejte do souboru `Web.config` následující nastavení:

[!code-xml[Main](breaking-changes/samples/sample6.xml)]

Nicméně doporučujeme analyzovat všechny chyby ověření žádosti, abyste zjistili, zda existující obslužné rutiny, moduly nebo jiné vlastní kódy mají přístup potenciálně nebezpečné vstupy HTTP, které by mohly být vektory útoku XSS.

<a id="0.1__Toc245724858"></a><a id="0.1__Toc255587637"></a><a id="0.1__Toc256770148"></a>

## <a name="default-hashing-algorithm-is-now-hmacsha256"></a>Výchozí algoritmus hash je teď HMACSHA256

ASP.NET používá šifrovací algoritmy i algoritmy hash k zabezpečení dat, jako jsou soubory cookie ověřování pomocí formulářů a stav zobrazení. Ve výchozím nastavení teď ASP.NET 4 používá algoritmus HMACSHA256 pro operace hash na souborech cookie a stavu zobrazení. Starší verze ASP.NET používaly starší algoritmus HMACSHA1.

Vaše aplikace můžou být ovlivněné, pokud spustíte smíšené prostředí ASP.NET 2.0/ASP. NET 4, kde data, jako jsou soubory cookie ověřování formulářů, musí fungovat ve verzích across.NET Framework. Pokud chcete webovou aplikaci ASP.NET 4 nakonfigurovat tak, aby používala starší algoritmus HMACSHA1, přidejte do souboru `Web.config` následující nastavení:

[!code-xml[Main](breaking-changes/samples/sample7.xml)]

<a id="0.1__Toc245724859"></a><a id="0.1__Toc255587638"></a><a id="0.1__Toc256770149"></a>

## <a name="configuration-errors-related-to-new-aspnet-4-root-configuration"></a>Chyby konfigurace související s novou kořenovou konfigurací ASP.NET 4

Konfigurační soubory root (`machine.config` soubor a kořenový `Web.config` soubor) pro .NET Framework 4 (a tedy ASP.NET 4) byly aktualizovány tak, aby obsahovaly většinu často se konfiguračních informací, které v ASP.NET 3,5 byly nalezeny v `Web.config` souborech aplikace. Vzhledem ke složitosti spravovaných systémů konfigurace služby IIS 7 a IIS 7,5, které spouštějí aplikace ASP.NET 3,5 v ASP.NET 4 a v části IIS 7 a služba IIS 7,5 můžou způsobit chyby konfigurace ASP.NET nebo IIS.

Doporučujeme, abyste upgradovali aplikace ASP.NET 3,5 na ASP.NET 4 pomocí nástrojů pro upgrade projektu v aplikaci Visual Studio 2010, pokud je to praktické. Visual Studio 2010 automaticky upraví soubor `Web.config` aplikace ASP.NET 3,5 tak, aby obsahoval příslušná nastavení pro ASP.NET 4.

Je však podporován scénář ke spouštění aplikací ASP.NET 3,5 pomocí .NET Framework 4 bez nutnosti rekompilace. V takovém případě může být nutné ručně upravit soubor `Web.config` aplikace před spuštěním aplikace v .NET Framework 4 a v části IIS 7 nebo IIS 7,5.

Následující dvě části popisují změny, které mohou být nutné pro různé kombinace softwaru.

**Windows Vista SP1 nebo Windows Server 2008 SP1, kde nejsou nainstalované žádné opravy hotfix KB958854 ani SP2.** V této konfiguraci systém konfigurace služby IIS 7 nesprávně sloučí spravovanou konfiguraci aplikace tím, že porovná soubor `Web.config` 2,0 na úrovni aplikace s `machine.config`mi soubory. Z tohoto důvodu musí mít soubory `Web.config` na úrovni aplikace z .NET Framework 3,5 nebo novější definici konfiguračního oddílu **System. Web. Extensions** (element), aby nedošlo k selhání ověření služby IIS 7.

Ručně upravily `Web.config` položky souboru na úrovni aplikace, které se přesně neshodují s původními definicemi často používaného konfiguračního oddílu, které byly představeny se sadou Visual Studio 2008, způsobí chyby konfigurace ASP.NET. (Výchozí položky konfigurace, které jsou generovány v aplikaci Visual Studio 2008 fungují správně.) Běžným problémem je, že ručně upravené `Web.config` soubory ponechají konfigurační atributy **AllowDefinition** a **RequirePermission** , které se nacházejí v různých definicích konfiguračního oddílu. Tím dojde k neshodě mezi zkráceným oddílem konfigurace v souborech `Web.config` na úrovni aplikace a úplnou definicí v souboru `machine.config` ASP.NET 4. Výsledkem je, že v době spuštění vyvolá konfigurační systém ASP.NET 4 chybu konfigurace.

**Windows Vista SP2, Windows Server 2008 SP2, Windows 7, Windows Server 2008 R2 a taky Windows Vista SP1 a Windows Server 2008 SP1, kde je nainstalovaná oprava hotfix KB958854**

V tomto scénáři systém nativní konfigurace služby IIS 7 a IIS 7,5 vrátí chybu konfigurace, protože provádí porovnání textu u atributu **typu** , který je definován pro obslužnou rutinu spravovaného konfiguračního oddílu. Vzhledem k tomu, že všechny soubory `Web.config` generované v rámci sady Visual Studio 2008 a Visual Studio 2008 SP1 mají v řetězci typu pro systém hodnotu "3,5". obslužné rutiny konfiguračního oddílu **Web. Extensions** (a související) a protože soubor ASP.NET 4 `machine.config` má v atributu **Type** pro stejné obslužné rutiny konfiguračního oddílu "4,0", aplikace, které jsou generovány v rámci sady Visual Studio 2008 nebo Visual Studio 2008 SP1 vždy selžou ověření konfigurace v iis 7 a IIS 7,5.

<a id="0.1__Toc251910248"></a>

### <a name="resolving-these-issues"></a>Řešení těchto problémů

Alternativním řešením pro první scénář je aktualizovat soubor `Web.config` na úrovni aplikace zahrnutím často používaného konfiguračního textu ze souboru `Web.config`, který byl vygenerován automaticky pomocí sady Visual Studio 2008.

Alternativním řešením pro první scénář je instalace aktualizace Service Pack 2 pro Vista nebo Windows Server 2008 do vašeho počítače nebo instalace opravy hotfix KB958854 ([https://support.microsoft.com/kb/958854](https://support.microsoft.com/kb/958854)), která opravuje nesprávné chování při sloučení konfiguračního systému služby IIS. Po provedení některé z těchto akcí však aplikace pravděpodobně dojde k chybě konfigurace z důvodu problému popsaného pro druhý scénář.

Alternativním řešením pro druhý scénář je odstranit nebo komentovat všechny definice konfiguračního oddílu **System. Web. Extensions** a definice skupin oddílů konfigurace z `Web.config` souboru na úrovni aplikace. Tyto definice jsou obvykle na začátku souboru `Web.config` na úrovni aplikace a lze je identifikovat pomocí elementu **configSections** a jeho podřízených elementů.

V obou scénářích se doporučuje také ručně odstranit oddíl **System. CodeDom** , přestože to není vyžadováno.

<a id="0.1__Toc252995490"></a><a id="0.1__Toc255587639"></a><a id="0.1__Toc256770150"></a><a id="0.1__Toc245724860"></a>

## <a name="aspnet-4-child-applications-fail-to-start-when-under-aspnet-20-or-aspnet-35-applications"></a>ASP.NET 4 podřízené aplikace se nespustí, když jsou v aplikacích ASP.NET 2,0 nebo ASP.NET 3,5.

ASP.NET 4 aplikace, které jsou nakonfigurované jako podřízené položky aplikací, které používají starší verze ASP.NET, se nemusí podařit spustit kvůli chybám konfigurace nebo kompilace. Následující příklad ukazuje adresářovou strukturu pro ovlivněnou aplikaci.

`/parentwebapp` (nakonfigurováno pro použití ASP.NET 2,0 nebo ASP.NET 3,5)  
`/childwebapp` (nakonfigurováno pro použití ASP.NET 4)

Aplikace ve složce `childwebapp` se nepodaří spustit ve službě IIS 7 nebo IIS 7,5 a ohlásí chybu konfigurace. Text chyby bude obsahovat zprávu podobnou následující:

- `The requested page cannot be accessed because the related configuration data for the page is invalid.`

- `The configuration section 'configSections' cannot be read because it is missing a section declaration.`

V případě služby IIS 6 se aplikace ve složce `childwebapp` také nespustí, ale ohlásí jinou chybu. Text chyby může například nastavovat následující:

- `The value for the 'compilerVersion' attribute in the provider options must be 'v4.0' or later if you are compiling for version 4.0 or later of the .NET Framework. To compile this Web application for version 3.5 or earlier of the .NET Framework, remove the 'targetFramework' attribute from the element of the Web.config file`

K těmto scénářům dochází, protože informace o konfiguraci z nadřazené aplikace ve složce `parentwebapp` jsou součástí hierarchie informací o konfiguraci, které určují poslední Sloučená nastavení konfigurace používaná podřízenou webovou aplikací ve složce `childwebapp`. V závislosti na tom, jestli je webová aplikace ASP.NET 4 spuštěná ve službě IIS 7 (nebo IIS 7,5) nebo ve službě IIS 6, vrátí buď konfigurační systém služby IIS, nebo kompilační systém ASP.NET 4 chybu.

Kroky, které je nutné provést při řešení tohoto problému a získání podřízené aplikace ASP.NET 4, závisí na tom, zda je aplikace ASP.NET 4 spuštěna ve službě IIS 6 nebo ve službě IIS 7 (nebo IIS 7,5).

### <a name="step-1-iis-7-or-iis-75-only"></a>Krok 1 (jenom IIS 7 nebo IIS 7,5)

Tento krok je nutný jenom v operačních systémech, na kterých běží IIS 7 nebo IIS 7,5, mezi které patří Windows Vista, Windows Server 2008, Windows 7 a Windows Server 2008 R2.

Přesuňte definici **configSections** do souboru `Web.config` nadřazené aplikace (aplikace, která spouští ASP.NET 2,0 nebo ASP.NET 3,5) do kořenového souboru `Web.config` pro the.NET Framework 2,0. Systém nativní konfigurace služby IIS 7 a IIS 7,5 kontroluje prvek **configSections** při sloučení hierarchie konfiguračních souborů. Přesunutí definice **configSections** z `Web.config` souboru nadřazené webové aplikace do kořenového `Web.config` souboru efektivně skrývá prvek z procesu sloučení konfigurace, ke kterému dochází pro podřízenou aplikaci ASP.NET 4.

V 32ovém operačním systému nebo u 32 fondů aplikací se v kořenovém `Web.config` souboru pro ASP.NET 2,0 a ASP.NET 3,5 obvykle nachází v následující složce:

`C:\Windows\Microsoft.NET\Framework\v2.0.50727\CONFIG`

V 64ovém operačním systému nebo u 64 fondů aplikací se v kořenovém `Web.config` souboru pro ASP.NET 2,0 a ASP.NET 3,5 obvykle nachází v následující složce:

`C:\Windows\Microsoft.NET\Framework64\v2.0.50727\CONFIG`

Pokud na počítači s podporou 64 běží jak 32, tak i 64 webové aplikace, je potřeba přesunout element **configSections** do kořenových `Web.config` souborů pro systémy s 32 a 64.

Při vložení prvku **configSections** do kořenového `Web.config` souboru, vložte oddíl hned za element **Konfigurace** . Následující příklad ukazuje, co by horní část kořenového souboru `Web.config` měla vypadat po dokončení přesunutí prvků.

> [!NOTE]
> V následujícím příkladu byly řádky zabaleny pro čitelnost.

[!code-xml[Main](breaking-changes/samples/sample8.xml)]

### <a name="step-2-all-versions-of-iis"></a>Krok 2 (všechny verze služby IIS)

Tento krok je povinný, pokud je podřízená webová aplikace ASP.NET 4 spuštěná ve službě IIS 6 nebo ve službě IIS 7 (nebo IIS 7,5).

V souboru `Web.config` nadřazené webové aplikace, která používá ASP.NET 2 nebo ASP.NET 3,5, přidejte značku **umístění** , která explicitně určuje (pro konfigurační systémy služby IIS i ASP.NET), že položky konfigurace platí pouze pro nadřazenou webovou aplikaci. Následující příklad ukazuje syntaxi elementu **Location** , který se má přidat:

[!code-xml[Main](breaking-changes/samples/sample9.xml)]

Následující příklad ukazuje, jak se značka **Location** používá k zabalení všech konfiguračních oddílů začínajících oddílem **appSettings** a konče v oddílu **System. webServer** .

[!code-xml[Main](breaking-changes/samples/sample10.xml)]

Po dokončení kroků 1 a 2 se podřízené webové aplikace ASP.NET 4 spustí bez chyb.

<a id="0.1__Toc252995491"></a><a id="0.1__Toc255587640"></a><a id="0.1__Toc256770151"></a>

## <a name="aspnet-4-web-sites-fail-to-start-on-computers-where-sharepoint-is-installed"></a>Weby ASP.NET 4 se nedaří spustit na počítačích, na kterých je nainstalována služba SharePoint.

Webové servery, na kterých je spuštěný SharePoint, mají `Web.config` soubor, který je nasazený v kořenovém adresáři webu SharePoint (například `c:\inetpub\wwwroot\web.config` pro výchozí web). V tomto souboru `Web.config` SharePoint nastaví vlastní úroveň částečného vztahu důvěryhodnosti s názvem WSS\_Minimal.

Pokud se pokusíte spustit web ASP.NET 4, který je nasazen jako podřízený tento typ webu služby SharePoint, zobrazí se následující chyba:

`Could not find permission set named 'ASP.NET'.`

K této chybě dochází, protože infrastruktura ASP.NET 4 Code Access Security (CAS) hledá sadu oprávnění s názvem ASP.NET. Nicméně konfigurační soubor částečné důvěryhodnosti, na který odkazuje WSS\_minimální, neobsahuje žádné sady oprávnění s tímto názvem.

V současné době není k dispozici verze SharePointu, která je kompatibilní s ASP.NET. V důsledku toho byste se neměli pokoušet spustit web ASP.NET 4 jako podřízenou lokalitu pod weby služby SharePoint.

<a id="0.1__Toc255587641"></a><a id="0.1__Toc256770152"></a>

## <a name="the-httprequestfilepath-property-no-longer-includes-pathinfo-values"></a>Vlastnost HttpRequest. FilePath už neobsahuje PathInfo hodnoty.

Předchozí verze ASP.NET zahrnovaly hodnotu **PathInfo** v hodnotě vrácené z různých vlastností souvisejících s cestou k souboru, včetně **HttpRequest. FilePath**, **HttpRequest. AppRelativeCurrentExecutionFilePath**a **HttpRequest. CurrentExecutionFilePath**. ASP.NET 4 již nezahrnuje hodnotu **PathInfo** v vrácených hodnotách z těchto vlastností. Místo toho jsou informace **PathInfo** k dispozici v **HttpRequest. PathInfo**. Představte si například následující fragment adresy URL:

`/testapp/Action.mvc/SomeAction`

V dřívějších verzích ASP.NET mají vlastnosti **HttpRequest** následující hodnoty:

**HttpRequest. FilePath**: `/testapp/Action.mvc/SomeAction`

**HttpRequest. PathInfo**: (prázdné)

Ve ASP.NET 4 vlastnosti **HttpRequest** jsou místo toho tyto hodnoty:

**HttpRequest. FilePath**: `/testapp/Action.mvc`

**HttpRequest. PathInfo**: `SomeAction`

<a id="0.1__Toc252995493"></a><a id="0.1__Toc255587642"></a><a id="0.1__Toc256770153"></a><a id="0.1__Toc245724861"></a>

## <a name="aspnet-20-applications-might-generate-httpexception-errors-that-reference-eurlaxd"></a>Aplikace ASP.NET 2,0 můžou generovat chyby HttpException –, které odkazují na eurl. axd.

Po povolení ASP.NET 4 ve službě IIS 6 mohou aplikace ASP.NET 2,0, které běží na službě IIS 6 (v systému Windows Server 2003 nebo Windows Server 2003 R2), způsobit chyby, jako například následující:

`System.Web.HttpException: Path '/[yourApplicationRoot]/eurl.axd/[Value]' was not found.`

K této chybě dochází, protože když ASP.NET zjistí, že je web nakonfigurovaný tak, aby používal ASP.NET 4, nativní komponenta ASP.NET 4 předá rozšiřující URL spravované části ASP.NET pro další zpracování. Pokud jsou ale virtuální adresáře, které jsou pod webem ASP.NET 4, nakonfigurované tak, aby používaly ASP.NET 2,0, zpracování adresy URL bez přípony tímto způsobem vede k upravené adrese URL, která obsahuje řetězec "eurl. axd". Tato upravená adresa URL se pak pošle do aplikace ASP.NET 2,0. ASP.NET 2,0 nemůže rozpoznat formát "eurl. axd". Proto se ASP.NET 2,0 pokusí najít soubor s názvem `eurl.axd` a spustit ho. Vzhledem k tomu, že žádný takový soubor neexistuje, požadavek se nezdařil s výjimkou **HttpException –** .

Tento problém můžete obejít pomocí jedné z následujících možností.

### <a name="option-1"></a>možnost 1

Pokud se ASP.NET 4 nevyžaduje k tomu, aby mohl web běžet, přemapujte lokalitu na místo toho použití ASP.NET 2,0.

### <a name="option-2"></a>Možnost 2

Pokud je pro spuštění webu vyžadován ASP.NET 4, přesuňte všechny podřízené virtuální adresáře ASP.NET 2,0 na jiný web, který je namapován na ASP.NET 2,0.

### <a name="option-3"></a>Možnost 3

Pokud není praktické přemapování webu na ASP.NET 2,0 nebo změnu umístění virtuálního adresáře, explicitně zakažte zpracování adresy URL bez přípony v ASP.NET 4. Použijte následující postup:

1. V registru Windows otevřete následující uzel:

`HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\ASP.NET\4.0.30319.0`

1. Vytvořte novou hodnotu **DWORD** s názvem **EnableExtensionlessUrls**.
2. Nastavte **EnableExtensionlessUrls** na hodnotu 0. Tím se zakáže chování adresy URL s příponou.
3. Uložte hodnotu registru a zavřete Editor registru.
4. Spusťte nástroj příkazového řádku **iisreset** , který způsobí, že služba IIS přečte novou hodnotu registru.

> [!NOTE]
> Nastavení **EnableExtensionlessUrls** na hodnotu 1 povolí chování nerozšiřujících adres URL. Toto je výchozí nastavení, pokud není zadána žádná hodnota.

<a id="0.1__Toc252995494"></a><a id="0.1__Toc255587643"></a><a id="0.1__Toc256770154"></a><a id="0.1__Toc245724862"></a>

## <a name="event-handlers-might-not-be-not-raised-in-a-default-document-in-iis-7-or-iis-75-integrated-mode"></a>Obslužné rutiny událostí nemusí být vyvolány ve výchozím dokumentu v integrovaném režimu služby IIS 7 nebo IIS 7,5.

ASP.NET 4 zahrnuje úpravy, které mění způsob, jakým se překládá atribut **Action** elementu HTML **Form** , když se přeloží adresa URL bez přípony na výchozí dokument. Příkladem adresy URL bez přípony, která se překládá na výchozí dokument, by byla [http://contoso.com/](http://contoso.com/)a výsledkem je žádost o [http://contoso.com/Default.aspx](http://contoso.com/Default.aspx).

ASP.NET 4 teď vykresluje hodnotu atributu **Action** elementu **formuláře** HTML jako prázdný řetězec, když se požadavek provede na rozšiřující adresu URL, na kterou je namapovaný výchozí dokument. Například v dřívějších verzích ASP.NET by požadavek na [http://contoso.com](http://contoso.com) způsobil požadavek na `Default.aspx`. V tomto dokumentu bude počáteční značka **formuláře** vykreslena jako v následujícím příkladu:

`<form action="Default.aspx" />`

V ASP.NET 4 se žádost o [http://contoso.com](http://contoso.com) také vede k žádosti o `Default.aspx`. ASP.NET nyní ale vykresluje značku **formuláře** HTML pro otevření jako v následujícím příkladu:

`<form action="" />`

Tento rozdíl ve způsobu vykreslování atributu **Action** může způsobit drobné změny ve způsobu, jakým je příspěvek formuláře ZPRACOVÁVÁN službou IIS a ASP.NET. Když je atribut **Action** prázdným řetězcem, vytvoří objekt IIS **DefaultDocumentModule** podřízenou žádost o `Default.aspx`. V rámci většiny podmínek je tato podřízená žádost transparentní pro kód aplikace a stránka `Default.aspx` pracuje normálně.

Potenciální interakce mezi spravovaným kódem a integrovaným režimem služby IIS 7 nebo IIS 7,5 může ale způsobit, že spravované stránky. aspx v rámci podřízeného požadavku přestanou fungovat správně. Pokud dojde k následujícím podmínkám, podřízené žádosti na `Default.aspx` dokument způsobí chybu nebo neočekávané chování:

1. Do prohlížeče se pošle stránka. aspx s atributem **Akce** prvku **formuláře** nastaveným na hodnotu.
2. Formulář je odeslán zpět do ASP.NET.
3. Spravovaný modul HTTP čte část těla entity. Například modul čte **požadavek. Form** nebo **Request. Paras**. To způsobí, že tělo entity požadavku POST bude načteno do spravované paměti. V důsledku toho již není tělo entity k dispozici pro žádné moduly nativního kódu, které jsou spuštěny v integrovaném režimu služby IIS 7 nebo IIS 7,5.
4. Objekt služby IIS **DefaultDocumentModule** nakonec spustí a vytvoří podřízený požadavek na dokument `Default.aspx`. Vzhledem k tomu, že tělo entity již bylo přečteno částí spravovaného kódu, není k dispozici žádný obsah entity k odeslání podřízené žádosti.
5. Když je kanál HTTP spuštěn pro podřízený požadavek, obslužná rutina pro `.aspx` soubory se spustí během fáze spuštění rutiny.
6. Vzhledem k tomu, že není k dispozici žádné tělo entity, neexistují žádné proměnné formuláře a žádný stav zobrazení, a proto nejsou k dispozici žádné informace pro obslužnou rutinu stránky. aspx, aby bylo možné určit, jakou událost (pokud existuje) by měla být vyvolána. V důsledku toho žádná z obslužných rutin události postback pro stránku ovlivnila. aspx nebude spuštěna.

Toto chování můžete obejít následujícími způsoby:

- Identifikujte modul HTTP, který v rámci požadavků na dokumenty přistupuje k hlavnímu textu entity žádosti, a určete, jestli se dá nakonfigurovat tak, aby se spouštěl jenom pro spravované požadavky. V integrovaném režimu pro IIS 7 i IIS 7,5 se moduly HTTP dají označit tak, aby se spouštěly jenom pro spravované požadavky, a to tak, že do položky **System. webServer/** modules daného modulu přidáte následující atribut:

- `precondition="managedHandler"`

- Toto nastavení zakáže modul pro požadavky, které služba IIS 7 a IIS 7,5 určí jako nespravované požadavky. U výchozích požadavků dokumentu je prvním požadavkem adresa URL bez přípony. Proto služba IIS nespustí žádné spravované moduly, které jsou označeny podmínkou spravované obslužné rutiny během procesu prvotního zpracování žádosti. V důsledku toho spravované moduly neúmyslně přečtou tělo entity, takže obsah entity je stále k dispozici a je předán spolu s podřízeným požadavkem a výchozím dokumentem.

- Pokud se problematické moduly HTTP musí spustit pro všechny požadavky (u statických souborů, u nerozšiřujících adres URL, které se překládají na objekt **DefaultDocumentModule** , pro spravované žádosti atd.), upravte ovlivněné stránky ASPX explicitním nastavením vlastnosti **Action** objektu **System. Web. UI. HtmlControls. HtmlForm** stránky na neprázdný řetězec. Například pokud je výchozí dokument `Default.aspx`, upravte kód stránky tak, aby explicitně nastavil vlastnost **Action** ovládacího prvku **HtmlForm** na Default. aspx.

<a id="0.1__Toc255587644"></a><a id="0.1__Toc256770155"></a>

## <a name="changes-to-the-aspnet-code-access-security-cas-implementation"></a>Změny implementace ASP.NET Code Access Security (CAS)

ASP.NET 2,0 a rozšířením funkce ASP.NET, které byly přidány v 3,5, použijte model CAS (.NET Framework 1,1 a 2,0 Code Access Security). Implementace certifikačních autorit v ASP.NET 4 se ale podstatně převedla. V důsledku toho mohou ASP.NET aplikace s částečným vztahem důvěryhodnosti, které spoléhají na důvěryhodný kód spuštěný v globální mezipaměti sestavení (GAC), selhat s různými výjimkami zabezpečení. Aplikace s částečným vztahem důvěryhodnosti, které spoléhají na rozsáhlé změny v zásadách CAS počítače, můžou selhat i při výjimkách zabezpečení.

Můžete vrátit částečně důvěryhodné aplikace ASP.NET 4 k chování ASP.NET 1,1 a 2,0 pomocí nového atributu **LegacyCasModel** v elementu konfigurace **vztahu důvěryhodnosti** , jak je znázorněno v následujícím příkladu:

`<trust level= "Medium" legacyCasModel="true" />`

Když se vrátíte na starší verzi modelu CAS, jsou povolené následující staré chování CAS:

- Je dodržena zásada CAS počítače.
- V jedné doméně aplikace je povoleno více různých sad oprávnění.
- Explicitní kontrolní výrazy oprávnění nejsou požadovány pro sestavení v globální mezipaměti sestavení (GAC), která jsou vyvolána, pokud je v zásobníku pouze ASP.NET nebo jiný kód .NET Framework.

Jeden scénář nelze vrátit v .NET Framework 4: aplikace s částečným vztahem důvěryhodnosti nemůžou již volat určitá rozhraní API v System. Web. dll a System. Web. Extensions. dll. V předchozích verzích .NET Framework bylo možné, že newebové aplikace s částečným vztahem důvěryhodnosti mají explicitně udělená oprávnění **AspNetHostingPermission** . Tyto aplikace mohou potom použít **System. Web. HttpUtility**, typy v oborech názvů **System. Web. ClientServices.\*** a typy související s členstvím, rolemi a profily. Volání těchto typů z newebových aplikací s částečnou důvěryhodností již není podporováno v .NET Framework 4.

> [!NOTE]
> Funkce **HtmlEncode** a **HtmlDecode** třídy **System. Web. HttpUtility** byla přesunuta do nové třídy .NET Framework 4 **System .NET. WebUtility** . Pokud se jednalo o jedinou funkci ASP.NET, která byla použita, upravte kód aplikace tak, aby místo toho používal novou třídu **WebUtility** .

Níže je uveden přehled vysoké úrovně změn výchozí implementace CAS v ASP.NET 4:

- Domény aplikace ASP.NET jsou nyní homogenní aplikační domény. V doméně aplikace jsou k dispozici pouze sady udělení s částečnou důvěryhodností a plnou důvěryhodností.
- ASP.NET sady udělení částečně důvěryhodného vztahu důvěryhodnosti jsou nezávislé na zásadách CAS na úrovni organizace, na úrovni počítače nebo na úrovni uživatele.
- ASP.NET sestavení, která byla dodávána v 3,5 a 3,5 SP1, byla převedena tak, aby používala model transparentnosti .NET Framework 4.
- Použití atributu ASP.NET **AspNetHostingPermission** se podstatně snížilo. Většina instancí tohoto atributu se odebrala z veřejných rozhraní ASP.NET API.
- Dynamicky kompilovaná sestavení vytvořená poskytovateli sestavení ASP.NET byla aktualizována tak, aby explicitně označila sestavení jako transparentní.
- Všechna sestavení ASP.NET jsou nyní označena takovým způsobem, že atribut APTCA je dodržen pouze v prostředích pro hostování webů. Částečně důvěryhodná newebová hostující prostředí, jako je ClickOnce, nebude možné volat do sestavení ASP.NET.

Další informace o novém modelu zabezpečení přístupu kódu ASP.NET 4 najdete v tématu [použití zabezpečení přístupu kódu v aplikacích ASP.NET](https://msdn.microsoft.com/library/dd984947%28VS.100%29.aspx) na webu MSDN.

<a id="0.1__Toc256770156"></a><a id="0.1__Toc245724863"></a><a id="0.1__Toc252995496"></a><a id="0.1__Toc255587645"></a><a id="0.1__Toc245724864"></a>

## <a name="membershipuser-and-other-types-in-the-systemwebsecurity-namespace-have-been-moved"></a>MembershipUser a další typy v oboru názvů System. Web. Security byly přesunuty.

Některé typy používané ve členství ASP.NET byly přesunuty z `System.Web.dll` do nového sestavení System. Web. ApplicationServices. dll. Typy byly přesunuty za účelem vyřešení závislostí architektonického vrstvení mezi typy v klientovi a v rozšířených .NET Framework SKU.

Projekty webů nemají v důsledku přesunutí těchto typů problémy, protože System. Web. ApplicationServices. dll byl přidán do seznamu odkazovaných sestavení, která jsou používána ve výchozím nastavení systémem kompilace ASP.NET. Pokud upgradujete projekt webu, který byl vytvořen pomocí dřívější verze ASP.NET na ASP.NET 4 otevřením v aplikaci Visual Studio 2010, projekt se zkompiluje bez chyb.

Podobně pokud upgradujete projekt webové aplikace, který byl vytvořen v dřívější verzi ASP.NET na ASP.NET 4 tím, že ho otevřete v aplikaci Visual Studio 2010, proces upgradu přidá do projektu odkaz na System. Web. ApplicationServices. dll. Proto budou aktualizované projekty webové aplikace také zkompilovány bez chyb.

Zkompilované (binární) soubory, které byly vytvořeny pomocí dřívějších verzí ASP.NET, budou také spuštěny bez chyb na ASP.NET 4, i když byly typy členství přesunuty do jiného sestavení. Informace o přesměrování typu byly přidány do verze ASP.NET 4 `System.Web.dll`, která automaticky směruje odkazy za běhu pro tyto typy do nového umístění pro typy.

Knihovny tříd, které používají konkrétní typy členství a které byly upgradovány z dřívějších verzí ASP.NET, však nebudou zkompilovány při použití v projektu ASP.NET 4. Například projekt knihovny tříd může selhat při kompilaci a nahlásit chybu, například následující:

- `The type 'System.Web.Security.MembershipUser' is defined in an assembly that is not referenced. You must add a reference to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`

- `The type name 'MembershipUser' could not be found. This type has been forwarded to assembly 'System.Web.ApplicationServices, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'. Consider adding a reference to that assembly.`

Tento problém můžete obejít tak, že do projektu knihovny tříd přidáte odkaz na System. Web. ApplicationServices. dll.

V následujícím seznamu jsou uvedeny typy *System. Web. Security* , které byly přesunuty z `System.Web.dll` do System. Web. ApplicationServices. dll:

- *System. Web. Security. MembershipCreateStatus*
- *System. Web. Security. Membership. CreateUserException*
- *System. Web. Security. MembershipPasswordException –*
- *System. Web. Security. MembershipPasswordFormat*
- *System. Web. Security. MembershipProvider*
- *System. Web. Security. MembershipProviderCollection*
- *System. Web. Security. MembershipUser*
- *System. Web. Security. MembershipUserCollection*
- *System. Web. Security. MembershipValidatePasswordEventHandler*
- *System. Web. Security. ValidatePasswordEventArgs*
- *System. Web. Security. poskytovatel RoleProvider*
- <a id="0.1_a"></a>*System. Web. Configuration. MembershipPasswordCompatibilityMode*

<a id="0.1__Toc256770157"></a>

## <a name="output-caching-changes-to-vary--http-header"></a>Změny v ukládání výstupu do mezipaměti se liší \* hlavičce protokolu HTTP

V ASP.NET 1,0 vyvolala chyba stránky v mezipaměti zadané `Location="ServerAndClient"` jako výstup – nastavení mezipaměti, které vygeneruje `Vary:*` hlavičku HTTP v odpovědi. To mělo vliv na to, že klientské prohlížeče nebudou stránku ukládat místně do mezipaměti.

V ASP.NET 1,1 byla přidána metoda **System. Web. HttpCachePolicy. SetOmitVaryStar** , která může být volána pro potlačení hlavičky `Vary:*`. Tato metoda byla vybrána, protože změna vygenerované hlavičky HTTP byla považována za potenciálně zásadní změnu v čase. Vývojáři však zaznamenali chování v ASP.NET a zprávy o chybách naznačují, že vývojáři nemají informace o existujícím chování **SetOmitVaryStar** .

V ASP.NET 4 bylo učiněno rozhodnutí k vyřešení problému root. Hlavička protokolu HTTP `Vary:*` již není generována z odpovědí, které určují následující direktivu:

`<%@OutputCache Location="ServerAndClient" %>`

V důsledku toho už **SetOmitVaryStar** není potřeba, aby bylo možné potlačit hlavičku `Vary:*`.

V aplikacích, které určují `Location="ServerAndClient"` v direktivě **@ OutputCache** na stránce, se nyní zobrazí chování odvozené od názvu hodnoty atributu **Location** – to znamená, že stránky budou v prohlížeči ukládat do mezipaměti, aniž by bylo nutné volat metodu **SetOmitVaryStar** .

Pokud stránky v aplikaci musí vygenerovat `Vary:*`, zavolejte metodu **AppendHeader** , jak je uvedeno v následujícím příkladu:

`HttpResponse.AppendHeader("Vary","*");`

Případně můžete změnit hodnotu atributu **umístění** výstupního ukládání do mezipaměti na "Server".

<a id="0.1__Toc255587646"></a><a id="0.1__Toc256770158"></a>

## <a name="systemwebsecurity-types-for-passport-are-obsolete"></a>Typy System. Web. Security pro Passport jsou zastaralé.

Podpora služby Passport integrovaná do ASP.NET 2,0 byla zastaralá a během několika let Nepodporovaná kvůli změnám ve službě Passport (teď LiveID). Výsledkem je, že pět typů souvisejících se službou Passport v **System. Web. Security** je nyní označeno atributem **ObsoleteAttribute** .

<a id="0.1__The_MenuItem.PopOutImageUrl_Propert"></a><a id="0.1__Toc256770159"></a>

## <a name="the-menuitempopoutimageurl-property-fails-to-render-an-image-in-aspnet-4"></a>Vlastnost MenuItem. PopOutImageUrl nemůže vykreslit image v ASP.NET 4.

V ASP.NET 3,5 vlastnost *MenuItem. PopOutImageUrl* umožňuje zadat adresu URL obrázku, který se zobrazí v položce nabídky, aby označoval, že položka nabídky má dynamickou podnabídku. Následující příklad ukazuje, jak zadat tuto vlastnost v označení v ASP.NET 3,5.

[!code-aspx[Main](breaking-changes/samples/sample11.aspx)]

V důsledku změny návrhu v ASP.NET 4 se nevykresluje žádný výstup pro *PopOutImageUrl* , pokud je vlastnost nastavena pro třídu *MenuItem* . Místo toho je nutné zadat adresu URL obrázku přímo v ovládacím prvku *nabídky* buď pomocí vlastnosti *StaticPopOutImageUrl* nebo vlastnosti *DynamicPopOutImageUrl* . Když pracujete se statickou nabídkou, vlastnost *menu. StaticPopOutImageUrl* Určuje adresu URL obrázku, který se zobrazí, aby označoval, že položka statické nabídky má podnabídku, jak je znázorněno v následujícím příkladu:

[!code-aspx[Main](breaking-changes/samples/sample12.aspx)]

Pokud pracujete s dynamickou nabídkou, použijte vlastnost *menu. DynamicPopOutImageUrl* k určení adresy URL pro obrázek, který označuje, že dynamická položka nabídky obsahuje podnabídku. Následující příklad je podobný předchozímu, ale ukazuje, jak nastavit vlastnost *DynamicPopOutImageUrl* pro dynamickou nabídku.

[!code-aspx[Main](breaking-changes/samples/sample13.aspx)]

Pokud vlastnost *menu. DynamicPopOutImageUrl* není nastavená a vlastnost *menu. DynamicEnableDefaultPopOutImage* je nastavená na *false*, nezobrazí se žádný obrázek. Podobně pokud vlastnost *StaticPopOutImageUrl* není nastavená a vlastnost *StaticEnableDefaultPopOutImage* je nastavená na *false*, nezobrazí se žádný obrázek.

Při nastavování cest pro tyto vlastnosti použijte lomítko (/) místo zpětného lomítka (\). Další informace najdete v tématu [nabídka. StaticPopOutImageUrl a nabídka. DynamicPopOutImageUrl se nepodaří vykreslit obrázky, když cesty obsahují zpětná lomítka](#0.1__Menu.StaticPopOutImageUrl_and_Menu. "_Menu. StaticPopOutImageUrl_and_Menu.") jinde v tomto dokumentu.

<a id="0.1__Menu.StaticPopOutImageUrl_and_Menu."></a><a id="0.1__Toc256770160"></a>

## <a name="menustaticpopoutimageurl-and-menudynamicpopoutimageurl-fail-to-render-images-when-paths-contain-backslashes"></a>Nabídka. StaticPopOutImageUrl a menu. DynamicPopOutImageUrl se nepodaří vykreslit obrázky, když cesty obsahují zpětná lomítka.

V ASP.NET 4 se obrázky, které zadáte, pomocí *nabídky. StaticPopOutImageUrl* a *menu. DynamicPopOutImageUrl* nebudou vykreslovat, pokud cesta obsahuje nepoužité body (\). Jedná se o změnu z dřívějších verzí ASP.NET.

Následující příklad značky ovládacího prvku *nabídky* ukazuje vlastnost *StaticPopOutImageUrl* nastavenou pomocí cesty, která obsahuje zpětné lomítko. V ASP.NET 4 se obrázek zadaný ve vlastnosti nevykresluje.

[!code-aspx[Main](breaking-changes/samples/sample14.aspx)]

Chcete-li tento problém vyřešit, změňte hodnoty cest, které jsou zadány ve vlastnostech *StaticPopOutImageUrl* a *DynamicPopOutImageUrl* , a použijte lomítka (/). Tato změna se zobrazuje v následujícím příkladu:

[!code-aspx[Main](breaking-changes/samples/sample15.aspx)]

Počítejte s tím, že aplikace, které byly migrovány z dřívějších verzí ASP.NET na ASP.NET 4, mohou být ovlivněny také, protože došlo ke změně vlastnosti *MenuItem. PopOutImageUrl* . Další informace naleznete v tématu [vlastnost MenuItem. PopOutImageUrl neumožňuje vykreslit obrázek v ASP.NET 4](#0.1__The_MenuItem.PopOutImageUrl_Propert "_The_MenuItem. PopOutImageUrl_Propert") jinde v tomto dokumentu.

<a id="0.1__Toc224729061"></a><a id="0.1__Toc255587647"></a><a id="0.1__Toc256770161"></a>

## <a name="disclaimer"></a>Právní omezení

Toto je předběžný dokument a může být podstatně měněn před konečným komerčním vydáním softwaru popsaného v tomto dokumentu.

Informace obsažené v tomto dokumentu představují aktuální pohled společnosti Microsoft Corporation na problémy, které jsou popsány k datu publikování. Vzhledem k tomu, že Microsoft musí reagovat na měnící se podmínky na trhu, neměl by být interpretován jako závazek společnosti Microsoft a společnost Microsoft nemůže zaručit přesnost všech informací, které jsou uvedeny po datu publikování.

Tento dokument White Paper slouží pouze k informativním účelům. SPOLEČNOST MICROSOFT NEPOSKYTUJE ŽÁDNÉ ZÁRUKY, AŤ UŽ VÝSLOVNĚ UVEDENÉ, PŘEDPOKLÁDANÉ NEBO STATUTÁRNÍ, JAKO INFORMACE V TOMTO DOKUMENTU.

Dodržování všech platných zákonů o autorských právech je zodpovědností uživatele. Bez omezení práv v rámci autorského práva nesmí být žádná část tohoto dokumentu reprodukována, ukládána do systému pro načítání nebo převedena v jakémkoli tvaru nebo jakýmkoli prostředkem (elektronickými, mechanicky, fotokopírováním, záznamem nebo jiným) nebo pro jakékoli účely. bez výslovného písemného svolení společnosti Microsoft Corporation.

Společnost Microsoft může mít patenty, patentové aplikace, ochranné známky, autorská práva nebo jiná práva duševního vlastnictví, která zahrnují předmět v tomto dokumentu. S výjimkou výslovně uvedených v písemné licenční smlouvě od společnosti Microsoft vám poskytnutí tohoto dokumentu neposkytuje žádnou licenci na tyto patenty, ochranné známky, autorská práva ani jiné duševní vlastnictví.

Pokud není uvedeno jinak, jsou ukázkové společnosti, organizace, produkty, názvy domén, e-mailové adresy, loga, osoby, místa a události uvedené v ukázkách smyšlené a bez jakýchkoli souvislostí se skutečnou společností, organizací, produktem, názvem domény, e-mailem. adresa, logo, osoba, místo nebo událost jsou zamýšlené nebo by se měly odvodit.

© 2010 Microsoft Corporation. Všechna práva vyhrazena.

Microsoft a Windows jsou buď registrované ochranné známky, nebo ochranné známky společnosti Microsoft Corporation v USA a dalších zemích.

Názvy skutečných společností a produktů uvedených v tomto dokumentu můžou být ochranné známky jejich příslušných vlastníků.

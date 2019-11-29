---
uid: whitepapers/mvc3-release-notes
title: ASP.NET MVC 3 | Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 10/06/2010
ms.assetid: f44c166e-7e91-48a0-a6f8-d9285f3594e5
msc.legacyurl: /whitepapers/mvc3-release-notes
msc.type: content
ms.openlocfilehash: 504202068f5db4f8614bba02e8066ffecfd15b48
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74619241"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

- [Přehled](#overview)
- [Poznámky k instalaci](#installation-notes)
- [Požadavky na software](#software-requirements)
- [Dokumentace](#documentation)
- [Pracovníky](#support)
- [Upgrade projektu ASP.NET MVC 2 na ASP.NET aktualizace nástrojů MVC 3](#upgrading)
- [Aktualizace nástrojů ASP.NET MVC 3 (12. dubna 2011)](#tu-changes)

    - [Dialogové okno Přidat řadič teď může používat řadiče pro generování uživatelského rozhraní se zobrazeními a kódem přístupu k datům.](#tu-AddControllerDialog)
    - [Vylepšení dialogového okna Nový projekt ASP.NET MVC 3](#tu-ImprovementsNewDialogBox)
    - [Šablony projektů teď zahrnují modernizr 1,7](#tu-Modernizr)
    - [Šablony projektů zahrnují aktualizované verze jQuery, uživatelského rozhraní jQuery a ověření jQuery.](#tu-UpdatedJQuery)
    - [Šablony projektů teď zahrnují ADO.NET Entity Framework 4,1 jako předinstalovaný balíček NuGet.](#tu-EF)
    - [Šablony projektů zahrnují knihovny JavaScriptu jako předem nainstalované balíčky NuGet](#tu-JavaScriptLibsNuget)
    - [Známé problémy](#tu-KI)
- [ASP.NET MVC 3 RTM (13. ledna 2011)](#MVC3RTM)

    - [Změna: aktualizace verze uživatelského rozhraní jQuery na 1.8.7](#RTM-1)
    - [Změnit: výchozí ModelMetadataProvider se změnil na DataAnnotationsModelMetadataProvider.](#RTM-2)
    - [Opraveno: vkládání části výrazu Razor, který obsahuje prázdné výsledky v opačném případě.](#RTM-3)
    - [Opraveno: přejmenování souboru Razor, který je otevřen v editoru, zakáže barevné zvýrazňování syntaxe a IntelliSense.](#RTM-4)
    - [Známé problémy](#RTM-KI)
    - [Průlomové změny](#RTM-BC)
- [ASP.NET MVC 3 Release Candidate 2 (10. prosince 2010)](#_Toc2)

    - [Šablony projektů se změnily tak, aby zahrnovaly jQuery 1.4.4, jQuery Validation 1,7 a jQuery UI 1.8.6 y UI 1.8.6](#_Toc2_1)
    - [Přidala se třída "AdditionalMetadataAttribute".](#_Toc2_2)
    - [Vylepšené generování uživatelského rozhraní zobrazení](#_Toc2_3)
    - [Přidaná metoda HTML. Raw](#_Toc2_3)
    - [Vlastnost Controller. ViewModel se přejmenovala na hodnotu ViewBag.](#_Toc2_4)
    - [Třída "ControllerSessionStateAttribute" se přejmenovala na "SessionStateAttribute".](#_Toc2_5)
    - [Byla přejmenována vlastnost "pole" RemoteAttribute na hodnotu "AdditionalFields".](#_Toc2_6)
    - [Přejmenování "SkipRequestValidationAttribute" na "AllowHtmlAttribute"](#_Toc2_7)
    - [Změnila se metoda "HTML. ValidationMessage", která zobrazí první užitečnou chybovou zprávu.](#_Toc2_8)
    - [Opravená deklarace @model, aby se do dokumentu nepřidalo prázdné místo](#_Toc2_9)
    - [Přidání vlastnosti "přípony" do zobrazení modulů pro podporu názvů souborů specifických pro určitý modul](#_Toc2_10)
    - [Oprava "LabelFor" pomocníka pro vygenerování správné hodnoty pro atribut "for"](#_Toc2_11)
    - [Opravená metoda "RenderAction", která má mít přednost explicitním hodnotám při vytváření vazby modelu](#_Toc2_12)
    - [Průlomové změny](#_Toc2_BC)
    - [Známé problémy](#_Toc2_KI)
- [ASP.NET MVC 3 Release Candidate (listopad 9, 2010)](#TOC_ASP_NET_3_RC)

    - [Nové funkce v ASP.NET MVC 3 RC](#_Toc276711785)
    - [Správce balíčků NuGet](#_Toc276711786)
    - [Vylepšené dialogové okno Nový projekt](#_Toc276711787)
    - [Řadiče s nerelačními relacemi](#_Toc276711788)
    - [Nové atributy ověřování](#_Toc276711789)
    - [Nová přetížení pro metody "LabelFor" a "LabelForModel"](#_Toc276711790)
    - [Ukládání výstupu podřízené akce do mezipaměti](#_Toc276711791)
    - [Vylepšení dialogového okna Přidat zobrazení](#_Toc276711792)
    - [Podrobné ověření požadavku](#_Toc276711793)
    - [Průlomové změny](#_Toc276711794)
    - [Známé problémy](#_Toc276711795)
- [Formátu. Poznámky k verzi MVC 3 beta (říjen 6, 2010)](#TOC_ASP_NET_3_Beta)

    - [Nové funkce v ASP.NET MVC 3 beta](#0.1__Toc274034215)
    - [Správce balíčků NuPack](#0.1__Toc274034216)
    - [Vylepšený dialog Nový projekt](#0.1__Toc274034217)
    - [Zjednodušený způsob, jak zadat modely silného typu v zobrazeních Razor](#0.1__Toc274034218)
    - [Podpora pro nové pomocné metody webových stránek ASP.NET](#0.1__Toc274034219)
    - [Podpora vkládání dalších závislostí](#0.1__Toc274034220)
    - [Nová podpora pro nenápad AJAX na bázi jQuery](#0.1__Toc274034221)
    - [Nová podpora pro nenápadné ověřování jQuery](#0.1__Toc274034222)
    - [Nové příznaky pro aplikaci pro ověřování klienta a nenáročnému JavaScriptu](#0.1__Toc274034223)
    - [Nová podpora kódu, který se spouští před spuštěním zobrazení](#0.1__Toc274034224)
    - [Nová podpora pro syntaxi VBHTML Razor](#0.1__Toc274034225)
    - [Přesnější řízení nad ValidateInputAttribute](#0.1__Toc274034226)
    - [Pomáhat pomocníkům při převodu podtržítek na spojovníky názvů atributů HTML zadaných pomocí anonymních objektů](#0.1__Toc274034227)
    - [Opravy chyb](#0.1__Toc274034228)
    - [Průlomové změny](#0.1__Toc274034229)
    - [Známé problémy](#0.1__Toc274034230)
- [Právní omezení](#0.1__Toc274034231)

<a id="overview"></a>
## <a name="overview"></a>Přehled

Tento dokument popisuje vydání ASP.NET MVC 3 RTM pro Visual Studio 2010. ASP.NET MVC je rozhraní pro vývoj webových aplikací, které používají vzor MVC (Model-View-Controller). Instalační program ASP.NET MVC 3 obsahuje následující komponenty:

- ASP.NET MVC 3 – součásti modulu runtime
- ASP.NET MVC 3 – nástroje sady Visual Studio 2010
- ASP.NET běhové komponenty webových stránek
- Webové stránky ASP.NET – nástroje sady Visual Studio 2010
- Microsoft Package Manager pro .NET (NuGet)
- Aktualizace pro Visual Studio 2010, která umožňuje podporu syntaxe Razor. (Podrobnosti najdete v článku 2483190 znalostní báze.)

Úplnou sadu poznámek k verzi pro každou předběžnou verzi ASP.NET MVC 3 najdete na webu ASP.NET na následující adrese URL:

https://www.asp.net/learn/whitepapers/mvc3-release-notes

<a id="installation-notes"></a>
## <a name="installation-notes"></a>Poznámky k instalaci

Pokud chcete nainstalovat ASP.NET MVC 3 RTM pomocí instalačního programu webové platformy (Web PI), navštivte následující stránku:

[https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3](https://www.microsoft.com/web/gallery/install.aspx?appid=MVC3)

Případně si můžete stáhnout instalační program pro ASP.NET MVC 3 RTM pro Visual Studio 2010 na následující stránce:

https://go.microsoft.com/fwlink/?LinkID=208140

ASP.NET MVC 3 se dá nainstalovat a může běžet souběžně s ASP.NET MVC 2.

<a id="software-requirements"></a>
## <a name="software-requirements"></a>Požadavky na software

Komponenty run-time ASP.NET MVC 3 vyžadují následující software:

- .NET Framework verze 4 

    ASP.NET MVC 3 Tools sady Visual Studio 2010 vyžadují následující software:
- Visual Studio 2010 nebo Visual Web Developer 2010 Express.

<a id="documentation"></a>
## <a name="documentation"></a>Dokumentace

Dokumentace k ASP.NET MVC je k dispozici na webu MSDN na následující adrese URL:

[https://go.microsoft.com/fwlink/?LinkId=205717](https://go.microsoft.com/fwlink/?LinkId=205717)

Kurzy a další informace o ASP.NET MVC jsou k dispozici na stránce MVC webu ASP.NET na následující adrese URL:

[https://www.asp.net/mvc/](../mvc/index.md)

<a id="support"></a>
## <a name="support"></a>Podpora

Toto je plně podporovaná verze. Informace o získání technické podpory najdete na [webu Podpora Microsoftu](https://support.microsoft.com/).

Také si můžete zdarma vydávat otázky týkající se této verze do fóra ASP.NET MVC, kde členové komunity ASP.NET mají často schopnost zajistit neformální podporu:

[https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)

<a id="upgrading"></a>
## <a name="upgrading-an-aspnet-mvc-2-project-to-aspnet-mvc-3-tools-update"></a>Upgrade projektu ASP.NET MVC 2 na ASP.NET aktualizace nástrojů MVC 3

ASP.NET MVC 3 se dá nainstalovat souběžně s ASP.NET MVC 2 na stejném počítači, což vám umožní pružně vybrat, kdy se má upgradovat aplikace ASP.NET MVC 2 na ASP.NET MVC 3.

Chcete-li ručně upgradovat existující aplikaci ASP.NET MVC 2 na verzi 3, postupujte následovně:

1. Vytvořte na svém počítači nový prázdný projekt ASP.NET MVC 3. Tento projekt bude obsahovat některé soubory, které jsou nutné pro upgrade.
2. Zkopírujte následující soubory z projektu ASP.NET MVC 3 do odpovídajícího umístění projektu ASP.NET MVC 2. Budete muset aktualizovat všechny odkazy na knihovnu jQuery na účet pro nový název souboru (jQuery 1.5.1. js): 

    - /Views/Web.config
    - /packages.config
    - /Scripts/\*. js
    - /Content/Themes/\*.\*
3. Zkopírujte složku *balíčky* do kořene prázdného řešení projektu ASP.NET MVC 3 do kořenového adresáře vašeho řešení, které je v adresáři, kde je umístěn soubor. sln řešení.
4. Pokud projekt ASP.NET MVC 2 obsahuje nějaké oblasti, zkopírujte soubor/Views/Web.config do složky *zobrazení* každé oblasti.
5. V souboru Web. config v projektu ASP.NET MVC 2, globální hledání a nahrazení verze ASP.NET MVC. Vyhledejte tyto informace: 

    [!code-console[Main](mvc3-release-notes/samples/sample1.cmd)]

    Nahraďte ji následujícím:

    [!code-console[Main](mvc3-release-notes/samples/sample2.cmd)]
6. V Průzkumník řešení odstraňte odkaz na *System. Web. Mvc* (který odkazuje na knihovnu DLL z verze 2) a pak přidejte odkaz na *System. Web. Mvc* (v 3.0.0.0).
7. Přidejte odkaz na System. Web. webpages. dll a System. Web. helps. dll. Tato sestavení jsou umístěna v následujících složkách: 

    - % ProgramFiles% \ Microsoft ASP. NET\ASP.NET MVC 3 \ Assemblies
    - % ProgramFiles% \ Microsoft ASP. NET\ASP.NET Web Pages\v1.0\Assemblies
8. V Průzkumník řešení klikněte pravým tlačítkem myši na název projektu a vyberte Uvolnit projekt. Pak znovu klikněte pravým tlačítkem na název projektu a vyberte upravit *ProjectName*. csproj.
9. Vyhledejte element *ProjectTypeGuids* a nahraďte {F85E285D-A4E0-4152-9332-AB1D724D3325} řetězcem {E53F8FEA-EAE0-44A6-8774-FFD645390401}.
10. Uložte změny, klikněte pravým tlačítkem na projekt a pak vyberte znovu načíst projekt.
11. V kořenovém souboru Web. config aplikace přidejte následující nastavení do oddílu *Assemblies (sestavení* ). 

    [!code-xml[Main](mvc3-release-notes/samples/sample3.xml)]
12. Pokud projekt odkazuje na všechny knihovny třetích stran, které jsou kompilovány pomocí ASP.NET MVC 2, přidejte následující zvýrazněný element *bindingRedirect* do souboru Web. config v kořenovém adresáři aplikace v části *Konfigurace* : 

    [!code-xml[Main](mvc3-release-notes/samples/sample4.xml)]

<a id="tu-changes"></a>
## <a name="changes-in-aspnet-mvc-3-tools-update"></a>Změny v nástroji ASP.NET MVC 3 – aktualizace

Tato část popisuje změny provedené ve vydání aktualizace nástrojů ASP.NET MVC 3 od verze ASP.NET MVC 3 RTM.

<a id="tu-AddControllerDialog"></a>
### <a name="add-controller-dialog-box-can-now-scaffold-controllers-with-views-and-data-access-code"></a>Dialogové okno Přidat řadič teď může používat řadiče pro generování uživatelského rozhraní se zobrazeními a kódem přístupu k datům.

Generování uživatelského rozhraní je způsob, jak rychle vygenerovat kontroler a zobrazení pro vaši aplikaci. Po vygenerování kódu ho můžete upravit, aby splňoval požadavky vašeho projektu.

Chcete-li otevřít dialogové okno *Přidat řadič* v ASP.NET MVC 3, klikněte pravým tlačítkem myši na složku *controllers* v *Průzkumník řešení*, klikněte na možnost *Přidat*a poté klikněte na možnost *kontroler*. Dialogové okno bylo vylepšeno a nabízí další možnosti generování uživatelského rozhraní.

![](mvc3-release-notes/_static/image1.png)

Ve výchozím nastavení jsou k dispozici tři šablony generování uživatelského rozhraní.

#### <a name="empty-controller"></a>Prázdný kontroler

Tato šablona vygeneruje prázdný soubor kontroleru. Tato šablona je ekvivalentem nezaškrtnutí *možnosti Přidat akce pro vytváření, úpravy, podrobnosti a odstraňování scénářů* v předchozích verzích ASP.NET MVC. Pokud zvolíte tuto možnost, nebudou k dispozici žádné další možnosti.

#### <a name="controller-with-empty-readwrite-actions"></a>Kontroler s prázdnými akcemi čtení/zápisu

Tato šablona vygeneruje soubor kontroleru, který obsahuje všechny požadované metody akce, ale žádné implementační kódy v metodách. Tato šablona je ekvivalentní ke kontrole *Přidání akcí pro scénáře vytváření, úprav, podrobností a odstraňování* v předchozích verzích služby ASP.NET MVC. Pokud zvolíte tuto možnost, nebudou k dispozici žádné další možnosti.

#### <a name="controller-with-readwrite-actions-and-views-using-entity-framework"></a>Kontroler s akcemi a zobrazeními čtení/zápisu pomocí Entity Framework

Tato šablona vám umožní rychle vytvořit uživatelské rozhraní pro zadávání dat. Generuje kód, který zpracovává řadu běžných požadavků a scénářů, například následující:

- *Přístup k datům*. Generovaný kód čte a zapisuje entity v databázi. Funguje s Entity Framework Code First přístup, pokud zvolíte existující třídu kontextu dat nebo pokud necháte šablonu generovat novou třídu *DbContext* . Funguje také s Entity Framework Database First nebo Model First přístupu, pokud zvolíte existující třídu *ObjectContext* .
- *Ověřování*. Vygenerovaný kód používá vazby modelu ASP.NET MVC a metadata, aby bylo možné vygenerovat formuláře podle pravidel deklarovaných ve vaší třídě modelu. To zahrnuje Vestavěná ověřovací pravidla, například *povinné* a *StringLength* atributy a vlastní ověřovací pravidla.
- *Relace 1: n*. Pokud definujete relace cizího klíče typu 1: n mezi třídami modelu, vygenerovaný kód vytvoří rozevírací seznamy pro výběr souvisejících entit. Můžete například definovat následující třídy modelu následující Entity Framework Code First konvence: 

    [!code-csharp[Main](mvc3-release-notes/samples/sample5.cs)]

    Po vytvoření uživatelského rozhraní řadiče pro třídu *produktu* budou jeho zobrazení uživatelům umožňovat výběr objektu *kategorie* pro každou instanci *produktu* .

    Tato šablona umožňuje další možnosti v dialogovém okně *Přidat řadič* . Pro *třídu modelu*můžete zvolit libovolnou třídu modelu ve vašem řešení, která určuje typ dat, která budou uživatelé moci vytvořit nebo upravit:
- Pokud chcete použít Entity Framework Code First, můžete zvolit libovolnou třídu modelu.
- Pokud používáte Entity Framework Database First nebo Entity Framework Model First, nezapomeňte zvolit třídu entity definovanou v koncepčním modelu.

Pro *třídu kontextu dat*můžete provést následující volby:

- Pokud chcete použít Code First a nemají žádnou existující třídu kontextu dat, vyberte * * nový datový kontext * *. Třída kontextu dat se pak vygeneruje za vás.
- Pokud chcete použít Code First a mít existující třídu kontextu dat, vyberte ji zde. Bude aktualizován tak, aby zachoval třídu modelu, kterou jste vybrali.
- Pokud používáte Database First nebo Model First, vyberte třídu kontext objektu zde.

Pro zobrazení vyberte modul zobrazení, který chcete použít, nebo vyberte možnost žádné, pokud nechcete používat žádná zobrazení.

Můžete vybrat Upřesnit Optionsto a zadat další možnosti pro vygenerovaná zobrazení. Můžete například zvolit rozložení nebo stránku předlohy, která se má použít.

<a id="tu-ImprovementsNewDialogBox"></a>
### <a name="improvements-to-the-aspnet-mvc-3-new-project-dialog-box"></a>Vylepšení dialogového okna Nový projekt ASP.NET MVC 3

Dialogové okno, které použijete k vytvoření nových projektů ASP.NET MVC 3, zahrnuje několik vylepšení, jak je uvedeno níže.

![](mvc3-release-notes/_static/image2.png)

#### <a name="new-intranet-project-template"></a>Nová šablona "intranetový projekt"

Seznam šablon projektů obsahuje novou šablonu pro intranetovou aplikaci. Tato šablona obsahuje nastavení pro vytváření webových aplikací pomocí ověřování systému Windows namísto ověřování pomocí formulářů. Vzhledem k tomu, že intranetová aplikace vyžaduje některá nastavení služby IIS, která nelze zapouzdřit v šabloně projektu, šablona obsahuje soubor Readme s pokyny, jak vytvořit šablonu projektu ve službě IIS. Dokumentace k nové šabloně intranetové aplikace je k dispozici na webu MSDN na následující adrese URL:

[https://msdn.microsoft.com/library/gg703322(VS.98).aspx](https://msdn.microsoft.com/library/gg703322(VS.98).aspx)

#### <a name="project-templates-are-now-html5-enabled"></a>Šablony projektu jsou teď povolené HTML5.

Dialogové okno Nový projekt nyní obsahuje možnost Přidat funkce specifické pro HTML5 do šablon projektů. Výběr možnosti způsobí vygenerování zobrazení, která obsahují nové prvky HTML5 `<header>`, `<footer>`a `<navigation>`.

Všimněte si, že starší verze prohlížečů nepodporují značky specifické pro HTML5. Pro řešení tohoto omezení obsahují šablony projektů HTML5 odkaz na knihovnu modernizr. (Další informace najdete v další části.)

<a id="tu-Modernizr"></a>
### <a name="project-templates-now-include-modernizr-17"></a>Šablony projektů teď zahrnují modernizr 1,7

Modernizr je knihovna JavaScriptu, která umožňuje podporu šablon stylů CSS 3 a HTML5 v prohlížečích, které tyto funkce ještě nepodporují. Tato knihovna je zahrnutá jako předem nainstalovaný balíček NuGet v šablonách pro projekty ASP.NET MVC 3. Další informace o modernizr najdete v tématu [http://www.modernizr.com/](http://www.modernizr.com/).

<a id="tu-UpdatedJQuery"></a>
### <a name="project-templates-include-updated-versions-of-jquery-jquery-ui-and-jquery-validation"></a>Šablony projektů zahrnují aktualizované verze jQuery, uživatelského rozhraní jQuery a ověření jQuery.

Šablony projektu nyní obsahují následující verze skriptů jQuery:

- jQuery 1.5.1
- Ověření jQuery 1,8
- 1\.8.11 uživatelského rozhraní jQuery

Tyto knihovny jsou zahrnuté jako předem nainstalované balíčky NuGet.

<a id="tu-EF"></a>
### <a name="project-templates-now-include-adonet-entity-framework-41-as-a-pre-installed-nuget-package"></a>Šablony projektů teď zahrnují ADO.NET Entity Framework 4,1 jako předinstalovaný balíček NuGet.

ADO.NET Entity Framework 4,1 obsahuje funkci Code First. Code First je nový model vývoje pro ADO.NET Entity Framework, který poskytuje alternativu k existujícím vzorům Database First a Model First.

Code First se zaměřuje na definování modelu pomocí tříd POCO ("obyčejné staré objekty CLR") napsané v Visual Basic nebo C#. Tyto třídy je pak možné namapovat na existující databázi nebo použít ke generování schématu databáze. Další konfiguraci můžete zadat pomocí atributů *Dataanotace* nebo pomocí rozhraní API Fluent.

Dokumentace k používání služby Code Firstwith ASP.NET MVC je k dispozici na webu ASP.NET na následujících adresách URL:

[https://www.asp.net/mvc/tutorials/getting-started-with-mvc3-part1-cs](../mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [https://www.asp.net/entity-framework/tutorials/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application](../mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)

<a id="tu-JavaScriptLibsNuget"></a>
### <a name="project-templates-include-javascript-libraries-as-pre-installed-nuget-packages"></a>Šablony projektů zahrnují knihovny JavaScriptu jako předem nainstalované balíčky NuGet

Když vytvoříte nový projekt ASP.NET MVC 3, projekt bude obsahovat dříve zmíněné soubory JavaScriptu (například knihovnu modernizr) jejich instalací pomocí NuGet místo přímého přidávání skriptů do složky skripty v šabloně projektu. obsah. To umožňuje použít NuGet k aktualizaci skriptů na nejnovější verzi při vydání nových verzí skriptů.

Například vzhledem k četnosti nových verzí jQuery je verze jQuery, která je obsažena v šabloně projektu, v určitém okamžiku neaktuální. Vzhledem k tomu, že jQuery je součástí nainstalovaného balíčku NuGet, budete upozorněni v dialogovém okně NuGet, pokud jsou k dispozici novější verze jQuery.

Vzhledem k tomu, že jQuery obsahuje číslo verze v názvu souboru, aktualizace jQuery na nejnovější verzi také vyžaduje aktualizaci značky `<script>`, která odkazuje na soubor jQuery na použití nového názvu souboru. Ostatní zahrnuté knihovny skriptů neobsahují číslo verze v názvu skriptu, takže je můžete snáze aktualizovat na nejnovější verze.

<a id="tu-KI"></a>
## <a name="known-issues"></a>Známé problémy

- V některých případech může instalace selhat s chybovou zprávou "instalace se nezdařila s kódem chyby (0x80070643)". Informace o tom, jak tento problém obejít, najdete v [článku 2531566 znalostní báze](https://support.microsoft.com/kb/2531566).
- Generování uživatelského rozhraní pro přidání kontroleru neposkytuje entity pro generování uživatelského rozhraní, které využívají podporu dědičnosti entit v rámci Entity Framework. Například vzhledem k tomu, že pro třídu základní *osoby* , která je zděděna třídou *studenta* , vytvoří generátor třídy *student* generovaný kód, který není zkompilován.
- Vytvoření nového projektu ASP.NET MVC 3 ve složce řešení způsobí chybu *NullReferenceException* . Alternativním řešením je vytvořit projekt ASP.NET MVC 3 v kořenovém adresáři řešení a pak ho přesunout do složky řešení.
- IntelliSense pro syntaxe Razor nefunguje, když je nainstalováno reostřejšíer. Pokud máte k dispozici reostřejšíer a chcete využít podporu technologie IntelliSense pro Razor v ASP.NET MVC 3, přečtěte si článek o tom, jak se mají v blogu hadi Hariri vykonat [a](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) v současné době využít možnosti jejich použití dohromady.
- Během instalace se v dialogovém okně přijetí smlouvy EULA zobrazí licenční podmínky v okně, které je menší než určené.
- Při úpravách zobrazení Razor (. cshtml nebo. *soubor vbhtml* ), zobrazení. ASP.NET MVC 3 nezahrnuje žádné fragmenty kódu pro zobrazení Razor.. aspxselecting fragment kódu pro ASP.NET MVC zobrazí fragmenty kódu pro
- Pokud nainstalujete ASP.NET MVC 3 pro Visual Web Developer Express na počítač, na kterém není nainstalovaná aplikace Visual Studio, a později nainstalujete Visual Studio, musíte znovu nainstalovat ASP.NET MVC 3. Visual Studio a Visual Web Developer Express sdílí komponenty, které jsou upgradovány instalačním programem ASP.NET MVC 3. Stejný problém se týká, pokud nainstalujete ASP.NET MVC 3 pro Visual Studio na počítači, který nemá Visual Web Developer Express, a pak později nainstalujete Visual Web Developer Express.

<a id="MVC3RTM"></a>
## <a name="changes-in-aspnet-mvc-3-rtm"></a>Změny v ASP.NET MVC 3 RTM

Tato část popisuje změny a opravy chyb provedené ve verzi ASP.NET MVC 3 RTM od verze RC2.

<a id="RTM-1"></a>
### <a name="change-updated-the-version-of-jquery-ui-to-187"></a>Změna: aktualizace verze uživatelského rozhraní jQuery na 1.8.7

Šablony projektů ASP.NET MVC pro sadu Visual Studio byly aktualizovány tak, aby obsahovaly nejnovější verzi knihovny uživatelského rozhraní jQuery. Šablony také obsahují minimální sadu souborů prostředků, které jsou vyžadovány uživatelským rozhraním jQuery, například přidružené soubory CSS a obrázky.

<a id="RTM-2"></a>
### <a name="change-changed-the-default-modelmetadataprovider-back-to-dataannotationsmodelmetadataprovider"></a>Změnit: výchozí ModelMetadataProvider se změnil na DataAnnotationsModelMetadataProvider.

Verze RC2 ASP.NET MVC 3 představila *CachedDataAnnotationsMetadataProvider* třídu, která poskytuje ukládání do mezipaměti nad stávající třídou *DataAnnotationsModelMetadataProvider* jako zlepšení výkonu. Nicméně některé chyby byly nahlášeny s touto implementací, takže změna byla vrácena a přesunuta do projektu Future MVC, který je k dispozici v [ASP.NET Webstacku](https://github.com/aspnet/AspNetWebStack).

<a id="RTM-3"></a>
### <a name="fixed-pasting-part-of-a-razor-expression-that-contains-whitespace-results-in-it-being-reversed"></a>Opraveno: vkládání části výrazu Razor, který obsahuje prázdné výsledky v opačném případě.

V předběžných verzích ASP.NET MVC 3 při vložení části výrazu Razor, který obsahuje prázdný znak do souboru Razor, je výsledný výraz obrácený. Zvažte například následující blok kódu Razor:

[!code-cshtml[Main](mvc3-release-notes/samples/sample6.cshtml)]

Pokud v první metodě vyberete text "první param" a vložíte ho jako argument do druhé metody, výsledek je následující:

[!code-cshtml[Main](mvc3-release-notes/samples/sample7.cshtml)]

Správným chováním je, že operace vložení by měla mít za následek následující:

[!code-cshtml[Main](mvc3-release-notes/samples/sample8.cshtml)]

Tento problém byl opraven ve verzi RTM, takže při operaci vložení se výraz správně zachovává.

<a id="RTM-4"></a>
### <a name="fixed-renaming-a-razor-file-that-is-opened-in-the-editor-disables-syntax-colorization-and-intellisense"></a>Opraveno: přejmenování souboru Razor, který je otevřen v editoru, zakáže barevné zvýrazňování syntaxe a IntelliSense.

Přejmenování souboru Razor pomocí Průzkumník řešení, když je soubor otevřen v okně editoru, způsobí, že zvýrazňování syntaxe a IntelliSense přestanou fungovat pro tento soubor. Tato funkce byla opravena, takže zvýrazňování a IntelliSense jsou po přejmenování udržovány.

<a id="RTM-KI"></a>
## <a name="known-issues"></a>Známé problémy

- Pokud zavřete Visual Studio 2010 SP1 Beta, zatímco je otevřená konzola správce balíčků NuGet, dojde k chybě sady Visual Studio a pokusí se o restartování. Tato akce bude opravena ve verzi RTM sady Visual Studio 2010 SP1.
- Instalační program ASP.NET MVC 3 umožňuje nainstalovat pouze počáteční verzi Správce balíčků NuGet. Po instalaci počáteční verze je možné NuGet nainstalovat a aktualizovat pomocí Správce rozšíření sady Visual Studio. Pokud už máte nainstalovaný NuGet, Projděte si galerii rozšíření sady Visual Studio a aktualizujte na nejnovější verzi NuGetu.
- Vytvoření nového projektu ASP.NET MVC 3 ve složce řešení způsobí chybu *NullReferenceException* . Alternativním řešením je vytvořit projekt ASP.NET MVC 3 v kořenovém adresáři řešení a pak ho přesunout do složky řešení.
- Dokončení instalačního programu může trvat mnohem déle než předchozí verze ASP.NET MVC. Důvodem je to, že aktualizuje součásti sady Visual Studio 2010.
- IntelliSense pro syntaxe Razor nefunguje, když je nainstalováno reostřejšíer. Pokud máte k dispozici reostřejšíer a chcete využít podporu technologie IntelliSense pro Razor v ASP.NET MVC 3, přečtěte si článek o tom, jak se mají v blogu hadi Hariri vykonat [a](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) v současné době využít možnosti jejich použití dohromady.
- Zobrazení CCSHTML a VBHTML vytvořená ve verzi beta sady ASP.NET MVC 3 nemají správnou sadu akcí sestavení s výsledkem, že tyto typy zobrazení jsou při publikování projektu vynechány. Hodnota akce sestavení pro tyto soubory by měla být nastavena na "content". ASP.NET MVC 3 RTM opravuje tento problém pro nové soubory, ale neopraví nastavení existujících souborů pro projekt vytvořený pomocí předprodejních verzí.
- ![](mvc3-release-notes/_static/image3.png)
- Během instalace se v dialogovém okně přijetí smlouvy EULA zobrazí licenční podmínky v okně, které je menší než určené.
- Při úpravách zobrazení Razor (soubor. cshtml) nebude k dispozici položka nabídky přejít na řadič v aplikaci Visual Studio a neexistují žádné fragmenty kódu.
- Pokud nainstalujete ASP.NET MVC 3 pro Visual Web Developer Express na počítač, na kterém není nainstalovaná aplikace Visual Studio, a později nainstalujete Visual Studio, musíte znovu nainstalovat ASP.NET MVC 3. Visual Studio a Visual Web Developer Express sdílí komponenty, které jsou upgradovány instalačním programem ASP.NET MVC 3. Stejný problém se týká, pokud nainstalujete ASP.NET MVC 3 pro Visual Studio na počítači, který nemá Visual Web Developer Express, a pak později nainstalujete Visual Web Developer Express.

<a id="RTM-BC"></a>
## <a name="breaking-changes"></a>Nejnovější změny

- V předchozích verzích ASP.NET MVC jsou filtry akcí vytvářeny na žádost s výjimkou případů v několika případech. Tímto chováním nebylo nikdy zaručené chování, ale pouze podrobností o implementaci a kontraktu pro filtry bylo považovat za bezstavové. V ASP.NET MVC 3 jsou filtry ukládány do mezipaměti mnohem agresivní. Proto všechny vlastní filtry akcí, které mají nesprávně uložený stav instance, můžou být poškozené.
- Pořadí spouštění pro filtry výjimek se změnilo pro filtry výjimek, které mají stejnou hodnotu *Order* . V ASP.NET MVC 2 a starších verzích filtry výjimek na kontroleru, které mají stejnou hodnotu *objednávky* jako u metody Action, se spustí před filtry výjimek v metodě Action. Obvykle se jedná o případ, kdy jsou filtry výjimek aplikovány bez zadané hodnoty *pořadí* . V ASP.NET MVC 3 bylo toto pořadí obráceno, aby se nejdříve nastavila většina specifická obslužná rutina výjimky. V případě, že je vlastnost *Order* explicitně určena jako v dřívějších verzích, jsou filtry spouštěny v zadaném pořadí.
- Do základní třídy *VirtualPathProviderViewEngine* byla přidána nová vlastnost s názvem *přípona* . Když ASP.NET vyhledává zobrazení podle cesty (ne podle názvu), jsou zvážena pouze zobrazení s příponou souboru obsaženou v seznamu určeném touto novou vlastností. Toto je zásadní změna v aplikacích, kde je zaregistrován vlastní poskytovatel sestavení, aby bylo možné povolit vlastní příponu souboru pro zobrazení webového formuláře a kde poskytovatel odkazuje na tato zobrazení pomocí úplné cesty namísto názvu. Alternativním řešením je změnit hodnotu vlastnosti *přípony* souborů tak, aby zahrnovala vlastní příponu souboru.
- Vlastní tovární implementace kontroleru, které přímo implementují rozhraní *IControllerFactory* , musí poskytovat implementaci nové metody *GetControllerSessionBehavior* , která se přidala do rozhraní v této verzi. Obecně se doporučuje toto rozhraní neimplementovat přímo a místo toho odvozovat třídu z *DefaultControllerFactory*.

<a id="_Toc2"></a>
## <a name="changes-in-aspnet-mvc-3-rc2"></a>Změny v ASP.NET MVC 3 RC2

Tato část popisuje změny (nové funkce a opravy chyb) provedené ve verzi ASP.NET MVC 3 RC2 od verze RC.

<a id="_Toc2_1"></a>
### <a name="project-templates-changed-to-include-jquery-144-jquery-validation-17-and-jquery-ui-186"></a>Šablony projektu se změnily tak, aby zahrnovaly jQuery 1.4.4, jQuery Validation 1,7 a jQuery UI 1.8.6.

Šablony projektů pro ASP.NET MVC 3 nyní obsahují nejnovější verze uživatelského rozhraní jQuery, jQuery ověřování a jQuery. uživatelské rozhraní jQuery je nové přidání do šablon projektů a poskytuje užitečné pomůcky uživatelského rozhraní. Další informace o uživatelském rozhraní jQuery najdete na jeho domovské stránce: [http://jqueryui.com/](http://jqueryui.com/).

<a id="_Toc2_2"></a>
### <a name="added-additionalmetadataattribute-class"></a>Přidala se třída "AdditionalMetadataAttribute".

Třídu *AdditionalMetadataAttribute* můžete použít k naplnění slovníku *ModelMetadata. AdditionalValues* pro vlastnost modelu.

Předpokládejme například, že model zobrazení obsahuje vlastnosti, které by měly být zobrazeny pouze pro správce. Tento model lze opatřit pomocí nového atributu pomocí AdminOnly jako klíč a true jako hodnotu, jak je uvedeno v následujícím příkladu:

[!code-csharp[Main](mvc3-release-notes/samples/sample9.cs)]

Tato metadata jsou zpřístupněna všem zobrazením nebo šablonám editoru při vykreslování modelu zobrazení produktu. K interpretaci informací o metadatech slouží vývojář aplikace.

<a id="_Toc2_3"></a>
### <a name="improved-view-scaffolding"></a>Vylepšené generování uživatelského rozhraní zobrazení

Šablony T4 použité pro zobrazení generování uživatelského rozhraní nyní generují volání pomocných metod šablon, jako je například *EditorFor* , namísto pomocných rutin, jako je například *TextBoxFor*. Tato změna vylepšuje podporu metadat v modelu ve formě atributů anotace dat, když dialogové okno Přidat zobrazení vygeneruje zobrazení.

Přidání zobrazení generování uživatelského rozhraní obsahuje také vylepšené zjišťování a využití informací o primárním klíči v modelu na základě konvence. Například dialogové okno Přidat zobrazení používá tyto informace k tomu, aby se zajistilo, že hodnota primárního klíče není vytvořená jako upravitelná pole formuláře.

Výchozí šablony pro úpravy a vytváření obsahují odkazy na skripty jQuery potřebné pro ověření klienta.

<a id="_Toc2_4"></a>
### <a name="added-htmlraw-method"></a>Přidaná metoda HTML. Raw

Ve výchozím nastavení používá modul pro zobrazení Razor Standard HTML všechny hodnoty. Například následující fragment kódu kóduje kód HTML uvnitř proměnné pozdravu tak, aby byl zobrazen na stránce jako `<strong>Hello World!</strong>`.

[!code-cshtml[Main](mvc3-release-notes/samples/sample10.cshtml)]

Nová metoda *HTML. Raw* poskytuje jednoduchý způsob zobrazení nekódovaného kódu HTML v případě, že je známý obsah v bezpečí. Následující příklad zobrazuje stejný řetězec, ale řetězec je vykreslen jako značka:

[!code-cshtml[Main](mvc3-release-notes/samples/sample11.cshtml)]

<a id="_Toc2_5"></a>
### <a name="renamed-controllerviewmodel-property-and-the-view-property-to-viewbag"></a>Vlastnost Controller. ViewModel se přejmenovala na hodnotu ViewBag.

Dříve vlastnost *ViewModel* *řadiče* odpovídala vlastnosti *zobrazení* . Obě tyto vlastnosti poskytují způsob, jak přistupovat k hodnotám objektu *ViewDataDictionary* pomocí syntaxe pro přístup k dynamické vlastnosti. Obě vlastnosti byly přejmenovány tak, aby byly stejné, aby se předešlo nejasnostem a bylo tak lépe konzistentní.

<a id="_Toc2_6"></a>
### <a name="renamed-controllersessionstateattribute-class-to-sessionstateattribute"></a>Třída "ControllerSessionStateAttribute" se přejmenovala na "SessionStateAttribute".

Třída *ControllerSessionStateAttribute* byla představena ve verzi RC sady ASP.NET MVC 3. Vlastnost byla přejmenována na stručnější.

<a id="_Toc2_7"></a>
### <a name="renamed-remoteattribute-fields-property-to-additionalfields"></a>Byla přejmenována vlastnost "pole" RemoteAttribute na hodnotu "AdditionalFields".

Vlastnost *polí* třídy *RemoteAttribute* způsobila nějaký nejasnost mezi uživateli. Přejmenováním této vlastnosti na *AdditionalFields* objasní svůj záměr.

<a id="_Toc2_8"></a>
### <a name="renamed-skiprequestvalidationattribute-to-allowhtmlattribute"></a>Přejmenování "SkipRequestValidationAttribute" na "AllowHtmlAttribute"

Atribut *SkipRequestValidationAttribute* se přejmenoval na *AllowHtmlAttribute* , aby lépe představoval zamýšlené použití.

<a id="_Toc2_9"></a>
### <a name="changed-htmlvalidationmessage-method-to-display-the-first-useful-error-message"></a>Změnila se metoda "HTML. ValidationMessage", která zobrazí první užitečnou chybovou zprávu.

Metoda *HTML. ValidationMessage* byla opravena tak, aby zobrazovala první užitečnou chybovou zprávu namísto pouhého zobrazení první chyby.

Při vytváření vazby modelu může být slovník *ModelState* vyplněný z více zdrojů s chybovými zprávami o vlastnosti, včetně z modelu samotného (Pokud implementuje *IValidatableObject*), z atributů ověřování použitých pro vlastnost a z výjimek vyvolaných během přistupování k vlastnosti.

Když metoda *HTML. ValidationMessage* zobrazí ověřovací zprávu, přeskočí položky stavu modelu, které obsahují výjimku, protože nejsou obvykle určeny pro koncového uživatele. Místo toho metoda vyhledá první ověřovací zprávu, která není přidružena k výjimce, a zobrazí tuto zprávu. Pokud se taková zpráva nenajde, použije se výchozí obecná chybová zpráva, která je přidružená k první výjimce.

<a id="_Toc2_10"></a>
### <a name="fixed-model-declaration-to-not-add-whitespace-to-the-document"></a>Opravená deklarace @model, aby se do dokumentu nepřidalo prázdné místo

V dřívějších verzích `@model` deklarace v horní části zobrazení přidala prázdný řádek do vykresleného výstupu HTML. To bylo opraveno, aby deklarace nevedla prázdné znaky.

<a id="_Toc2_11"></a>
### <a name="added-fileextensions-property-to-view-engines-to-support-engine-specific-file-names"></a>Přidání vlastnosti "přípony" do zobrazení modulů pro podporu názvů souborů specifických pro určitý modul

Modul zobrazení může vracet zobrazení pomocí explicitní cesty zobrazení, jak je uvedeno v následujícím příkladu:

[!code-csharp[Main](mvc3-release-notes/samples/sample12.cs)]

První modul zobrazení se vždy pokusí vykreslit zobrazení. Ve výchozím nastavení je modul zobrazení webových formulářů prvním modulem zobrazení. vzhledem k tomu, že modul Web Forms nemůže vykreslit zobrazení Razor, dojde k chybě. Zobrazit moduly teď mají vlastnost *přípony* souborů, která se používá k určení, které přípony souborů podporují. Tato vlastnost je zaškrtnuta v případě, že ASP.NET určuje, zda zobrazovací modul může vykreslit soubor. Toto je zásadní změna a další podrobnosti jsou uvedeny v části [průlomované změny](#_Toc2_BC) v tomto dokumentu.

<a id="_Toc2_12"></a>
### <a name="fixed-labelfor-helper-to-emit-the-correct-value-for-the-for-attribute"></a>Oprava "LabelFor" pomocníka pro vygenerování správné hodnoty pro atribut "for"

Byla opravena chyba, kde Metoda *LabelFor* vygenerovala *pro* atribut, který se shoduje s atributem *názvu* *vstupního* elementu namísto jeho ID. Podle konsorcia W3C by atribut *for* měl odpovídat ID *vstupního* elementu.

<a id="_Toc2_13"></a>
### <a name="fixed-renderaction-method-to-give-explicit-values-precedence-during-model-binding"></a>Opravená metoda "RenderAction", která má mít přednost explicitním hodnotám při vytváření vazby modelu

V dřívějších verzích byly explicitní hodnoty, které byly předány metodě *RenderAction* , ignorovány ve prospěch aktuálních hodnot formuláře během vazby modelu uvnitř podřízené akce. Oprava zajistí, že při vytváření vazby modelu budou mít explicitní hodnoty přednost.

<a id="_Toc2_BC"></a>
## <a name="breaking-changes"></a>Nejnovější změny

- V předchozích verzích ASP.NET MVC byly pro každý požadavek vytvořeny filtry akcí s výjimkou v několika případech. Tímto chováním nebylo nikdy zaručené chování, ale pouze podrobností o implementaci a kontraktu pro filtry bylo považovat za bezstavové. V ASP.NET MVC 3 jsou filtry ukládány do mezipaměti mnohem agresivní. Proto všechny vlastní filtry akcí, které mají nesprávně uložený stav instance, můžou být poškozené.
- Pořadí spouštění pro filtry výjimek se změnilo pro filtry výjimek, které mají stejnou hodnotu *Order* . V ASP.NET MVC 2 a starších byly filtry výjimek na kontroleru, které mají stejnou hodnotu *Order* jako u metody Action, byly provedeny před filtry výjimek v metodě Action. Obvykle se jedná o případ, kdy byly filtry výjimek aplikovány bez zadané hodnoty *pořadí* . V ASP.NET MVC 3 bylo toto pořadí obráceno, aby se nejdříve nastavila většina specifická obslužná rutina výjimky. V případě, že je vlastnost *Order* explicitně určena jako v dřívějších verzích, jsou filtry spouštěny v zadaném pořadí.
- Do základní třídy *VirtualPathProviderViewEngine* byla přidána nová vlastnost s názvem *přípona* . Když ASP.NET vyhledává zobrazení podle cesty (ne podle názvu), jsou zvážena pouze zobrazení s příponou souboru obsaženou v seznamu určeném touto novou vlastností. Toto je zásadní změna v aplikacích, kde je zaregistrován vlastní poskytovatel sestavení, aby bylo možné povolit vlastní příponu souboru pro zobrazení webového formuláře a kde poskytovatel odkazuje na tato zobrazení pomocí úplné cesty namísto názvu. Alternativním řešením je změnit hodnotu vlastnosti *přípony* souborů tak, aby zahrnovala vlastní příponu souboru.
- Vlastní tovární implementace kontroleru, které přímo implementují rozhraní *IControllerFactory* , musí poskytovat implementaci nové metody *GetControllerSessionBehavior* , která se přidala do rozhraní v této verzi. Obecně se doporučuje toto rozhraní neimplementovat přímo a místo toho odvozovat třídu z *DefaultControllerFactory*.

<a id="_Toc2_KI"></a>
## <a name="known-issues"></a>Známé problémy

- Instalační program ASP.NET MVC 3 umožňuje nainstalovat pouze počáteční verzi Správce balíčků NuGet. Po instalaci počáteční verze je možné NuGet nainstalovat a aktualizovat pomocí Správce rozšíření sady Visual Studio. Pokud už máte nainstalovaný NuGet, Projděte si galerii rozšíření sady Visual Studio a aktualizujte na nejnovější verzi NuGetu.
- Vytvoření nového projektu ASP.NET MVC 3 ve složce řešení způsobí chybu *NullReferenceException* . Alternativním řešením je vytvořit projekt ASP.NET MVC 3 v kořenovém adresáři řešení a pak ho přesunout do složky řešení.
- Dokončení instalačního programu může trvat mnohem déle než předchozí verze ASP.NET MVC. Důvodem je to, že aktualizuje součásti sady Visual Studio 2010.
- IntelliSense pro syntaxe Razor nefunguje, když je nainstalováno reostřejšíer. Pokud máte k dispozici reostřejšíer a chcete využít podporu technologie IntelliSense Razor v ASP.NET MVC 3 RC2, přečtěte si článek o tom, jak se budou tyto možnosti používat v dnešní době [, na blogu](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) hadi Hariri.
- Zobrazení CSHTML a VBHTML vytvořená ve verzi beta sady ASP.NET MVC 3 nemají správnou sadu akcí sestavení s výsledkem, že tyto typy zobrazení jsou při publikování projektu vynechány. Hodnota *Akce sestavení* pro tyto soubory by měla být nastavena na obsah. ASP.NET MVC 3 RC2 opravuje tento problém pro nové soubory, ale neopraví nastavení existujících souborů pro projekt vytvořený pomocí beta verze.![](mvc3-release-notes/_static/image4.png)
- Během instalace se v dialogovém okně přijetí smlouvy EULA zobrazí licenční podmínky v okně, které je menší než určené.
- Při úpravách zobrazení Razor (soubor. cshtml) nebude k dispozici položka nabídky přejít na řadič v aplikaci Visual Studio a neexistují žádné fragmenty kódu.
- Pokud nainstalujete ASP.NET MVC 3 pro Visual Web Developer Express na počítač, na kterém není nainstalovaná aplikace Visual Studio, a později nainstalujete Visual Studio, musíte znovu nainstalovat ASP.NET MVC 3. Visual Studio a Visual Web Developer Express sdílí komponenty, které jsou upgradovány instalačním programem ASP.NET MVC 3. Stejný problém se týká, pokud nainstalujete ASP.NET MVC 3 pro Visual Studio na počítači, který nemá Visual Web Developer Express, a pak později nainstalujete Visual Web Developer Express.
- Instalace ASP.NET MVC 3 RC 2 neaktualizuje NuGet, pokud ji už máte nainstalovanou. Pokud chcete upgradovat NuGet, navštivte Správce rozšíření sady Visual Studio a měl by se zobrazit jako dostupná aktualizace. Z této služby můžete upgradovat NuGet na nejnovější verzi.

<a id="TOC_ASP_NET_3_RC"></a>
## <a name="aspnet-mvc-3-release-candidate"></a>ASP.NET MVC 3 Release Candidate

ASP.NET MVC Release Candidate byl vydán 9. listopadu 2010.

<a id="_Toc276711785"></a>
## <a name="new-features-in-aspnet-mvc-3-rc"></a>Nové funkce v ASP.NET MVC 3 RC

Tato část popisuje funkce, které byly představeny ve verzi ASP.NET MVC 3 RC, od verze beta.

<a id="_Toc276711786"></a>
### <a name="nuget-package-manager"></a>Správce balíčků NuGet

ASP.NET MVC 3 zahrnuje Správce balíčků NuGet (dříve označovaný jako NuPack), což je integrovaný nástroj pro správu balíčků pro přidávání knihoven a nástrojů do projektů sady Visual Studio. Tento nástroj automatizuje kroky, které vývojáři dnes využívají, aby získaly knihovnu do zdrojového stromu.

S NuGet můžete pracovat jako s nástrojem příkazového řádku, jako s integrovaným oknem konzoly v sadě Visual Studio 2010, v místní nabídce sady Visual Studio a jako sadou rutin PowerShellu.

Další informace o NuGet najdete v [dokumentaci k NuGet](https://docs.microsoft.com/nuget/).

<a id="_Toc276711787"></a>
### <a name="improved-new-project-dialog-box"></a>Vylepšené dialogové okno Nový projekt

Při vytváření nového projektu teď dialogové okno Nový projekt umožňuje určit modul zobrazení i typ projektu ASP.NET MVC.

![](mvc3-release-notes/_static/image5.png)

Tato verze obsahuje podporu pro úpravu seznamu šablon a modulů zobrazení uvedených v dialogovém okně.

Výchozí šablony jsou následující:

Obsahovat. Obsahuje minimální sadu souborů pro projekt ASP.NET MVC, včetně výchozí adresářové struktury pro projekty ASP.NET MVC, souboru site. CSS, který obsahuje výchozí styly ASP.NET MVC a adresář skriptů, který obsahuje výchozí soubory JavaScriptu.

Internetovou aplikaci. Obsahuje ukázkové funkce, které demonstrují, jak použít poskytovatele členství s ASP.NET MVC.

Seznam šablon projektu, které se zobrazí v dialogovém okně, je určen v registru systému Windows.

<a id="_Toc276711788"></a>
### <a name="sessionless-controllers"></a>Řadiče s nerelačními relacemi

Nový *ControllerSessionStateAttribute* nabízí větší kontrolu nad chováním stavu relace pro řadiče tím, že zadáte hodnotu výčtu [System. Web. SessionState. SessionStateBehavior](https://msdn.microsoft.com/library/system.web.sessionstate.sessionstatebehavior.aspx) .

Následující příklad ukazuje, jak vypnout stav relace pro všechny požadavky na kontroler.

[!code-csharp[Main](mvc3-release-notes/samples/sample13.cs)]

Následující příklad ukazuje, jak nastavit stav relace jen pro čtení pro všechny požadavky na kontroler.

[!code-csharp[Main](mvc3-release-notes/samples/sample14.cs)]

<a id="_Toc276711789"></a>
### <a name="new-validation-attributes"></a>Nové atributy ověřování

#### <a name="compareattribute"></a>CompareAttribute

Nový atribut ověřování *CompareAttribute* vám umožňuje porovnat hodnoty dvou různých vlastností modelu. V následujícím příkladu musí vlastnost *ComparePassword* odpovídat poli *heslo* , aby byla platná.

[!code-csharp[Main](mvc3-release-notes/samples/sample15.cs)]

#### <a name="remoteattribute"></a>RemoteAttribute

Nový atribut ověření *RemoteAttribute* využívá vzdálený validátor modulu plug-in jQuery pro ověření, který umožňuje ověřování na straně klienta volat metodu na serveru, který provádí skutečnou logiku ověřování.

V následujícím příkladu má vlastnost *username* použit parametr *RemoteAttribute* . Při úpravách této vlastnosti v zobrazení pro úpravy bude ověření klienta volat akci s názvem *UserNameAvailable* ve třídě *UsersController* , aby toto pole bylo možné ověřit.

[!code-csharp[Main](mvc3-release-notes/samples/sample16.cs)]

Následující příklad ukazuje odpovídající kontroler.

[!code-csharp[Main](mvc3-release-notes/samples/sample17.cs)]

Ve výchozím nastavení je název vlastnosti, na kterou je atribut použit, odesílán do metody Action jako parametr řetězce dotazu.

<a id="_Toc276711790"></a>
### <a name="new-overloads-for-labelfor-and-labelformodel-methods"></a>Nová přetížení pro metody "LabelFor" a "LabelForModel"

Pro metody *LabelFor* a *LabelForModel* se přidala nová přetížení, která umožňují zadat text popisku. Následující příklad ukazuje, jak použít tato přetížení.

[!code-cshtml[Main](mvc3-release-notes/samples/sample18.cshtml)]

<a id="_Toc276711791"></a>
### <a name="child-action-output-caching"></a>Ukládání výstupu podřízené akce do mezipaměti

*OutputCacheAttribute* podporuje ukládání výstupu do mezipaměti podřízených akcí, které jsou volány pomocí pomocných metod *HTML. RenderAction* nebo *HTML. Action* . Následující příklad ukazuje zobrazení, které volá jinou akci.

[!code-cshtml[Main](mvc3-release-notes/samples/sample19.cshtml)]

Akce *GETDATE* je opatřena poznámkou s *OutputCacheAttribute*:

[!code-csharp[Main](mvc3-release-notes/samples/sample20.cs)]

Po spuštění tohoto kódu je výsledek volání HTML. Action ("GETDATE") uložen do mezipaměti po dobu 100 sekund.

<a id="_Toc276711792"></a>
### <a name="add-view-dialog-box-improvements"></a>Vylepšení dialogového okna Přidat zobrazení

Když přidáte zobrazení silného typu, dialogové okno Přidat zobrazení teď vyfiltruje víc nepoužitelných typů než v předchozích verzích, jako je třeba mnoho základních .NET Framework typů. Seznam je nyní seřazen podle názvu třídy, a ne podle plně kvalifikovaného názvu typu, což usnadňuje hledání typů. Například název typu je nyní zobrazen jako v následujícím příkladu:

ClassName (obor názvů)

V dřívějších verzích se tato zpráva zobrazila jako následující:

Namespace. ClassName

<a id="_Toc276711793"></a>
### <a name="granular-request-validation"></a>Podrobné ověření požadavku

Vlastnost *Exclude* třídy *ValidateInputAttribute* již neexistuje. Místo toho, aby bylo ověření žádosti přeskočeno pro konkrétní vlastnosti modelu během vytváření vazby modelu, použijte nový *SkipRequestValidationAttribute*.

Předpokládejme například, že se pro úpravu blogového příspěvku používá metoda akce:

[!code-csharp[Main](mvc3-release-notes/samples/sample21.cs)]

Následující příklad ukazuje model zobrazení pro Blogový příspěvek.

[!code-csharp[Main](mvc3-release-notes/samples/sample22.cs)]

Když uživatel odešle kód pro vlastnost Description, vazba modelu selže z důvodu ověření žádosti. Chcete-li zakázat ověření žádosti během vazby modelu pro popis blogového příspěvku, použijte *SkipRequpestValidationAttribute* na vlastnost, jak je znázorněno v následujícím příkladu:.

[!code-csharp[Main](mvc3-release-notes/samples/sample23.cs)]

Případně pro vypnutí žádosti o ověření pro každou vlastnost modelu použijte *ValidateInputAttribute* s hodnotou *false* na metodu akce:

[!code-csharp[Main](mvc3-release-notes/samples/sample24.cs)]

<a id="_Toc276711794"></a>
## <a name="breaking-changes"></a>Nejnovější změny

- Pořadí spouštění pro filtry výjimek se změnilo pro filtry výjimek, které mají stejnou hodnotu *Order* . V ASP.NET MVC 2 a starších byly filtry výjimek na řadiči, které měly stejné *pořadí* jako u metody Action, provedeny před filtry výjimek v metodě Action. Obvykle se jedná o případ, kdy byly filtry výjimek aplikovány bez zadané hodnoty *pořadí* . V ASP.NET MVC 3 bylo toto pořadí obráceno, aby se nejdříve nastavila většina specifická obslužná rutina výjimky. V případě, že je vlastnost *Order* explicitně určena jako v dřívějších verzích, jsou filtry spouštěny v zadaném pořadí.
- Do základní třídy *VirtualPathProviderViewEngine* se přidala nová vlastnost s názvem *přípona* . Při vyhledávání zobrazení podle cesty (a nikoli podle názvu) se považuje jenom zobrazení s příponou souboru obsažená v seznamu určeném touto novou vlastností. Toto je zásadní změna pro uživatele, kteří registrují vlastního poskytovatele sestavení, aby povolili vlastní příponu souboru pro zobrazení webového formuláře a odkazovala na tato zobrazení pomocí úplné cesty místo názvu. Alternativním řešením je změnit hodnotu vlastnosti *přípony* souborů tak, aby zahrnovala vlastní příponu souboru.

<a id="_Toc276711795"></a>
## <a name="known-issues"></a>Známé problémy

- Instalační program může trvat mnohem déle než předchozí verze ASP.NET MVC, protože aktualizuje součásti sady Visual Studio 2010.
- Přidání generování uživatelského rozhraní zobrazení při výběru vlastností astrongly typů zobrazení typu, které jsou jen pro zápis. Tyto by se měly vždycky ignorovat pomocí generování uživatelského rozhraní. Dialog Přidat zobrazení také při generování zobrazení upravit nebo vytvořit vytvoří vlastnosti jen pro čtení. Vlastnosti jen pro čtení by měly být pro zobrazení zobrazení a seznamu pouze vygenerované jako generátory.
- Ladění nefunguje, když je nainstalovaná ASP.NET MVC 3 společně s asynchronní CTP. ASP.NET MVC 3 nelze nainstalovat souběžně s asynchronní CTP. Odinstalujte asynchronní CTP za účelem opravy ladění. Další podrobnosti najdete v [tomto blogovém příspěvku](http://drew-prog.blogspot.com/2010/11/how-to-uninstall-microsoft-aspnet-mvc-3.html) o odinstalaci všech částí ASP.NET MVC 3 RC.
- Technologie IntelliSense pro Razor nefunguje, když je nainstalováno reostřejšíer. Pokud máte reostřejšíer nainstalovaný a chcete využít podporu technologie IntelliSense Razor v ASP.NET MVC 3 RC, přečtěte si [Tento Blogový příspěvek](https://blogs.jetbrains.com/dotnet/2010/11/razor-intellisense-and-resharper/) z JetBrains, který pojednává o způsobech jejich používání společně.
- Zobrazení CSHTML a VBHTML vytvořená pomocí beta verze ASP.NET MVC 3 nemají správnou akci sestavení, která je vynechává z publikování. *Akce sestavení* pro tyto soubory by měla být nastavená na "obsah". ASP.NET MVC 3 RC opravuje tento problém pro nové soubory, ale neopraví nastavení existujících souborů pro projekt vytvořený pomocí beta verze.
- Instalační program může trvat mnohem déle než předchozí verze ASP.NET MVC, protože aktualizuje součásti sady Visual Studio 2010.
- Přidání generování uživatelského rozhraní pro zobrazení při výběru možnosti upravit pouze generátory zobrazení silného typu. Podobně jsou vlastnosti jen pro zápis vygenerované pro zobrazení "zobrazení".
- Během instalace se v dialogovém okně přijetí smlouvy EULA zobrazí licenční podmínky v okně, které je menší než určené.
- Při instalaci sady Visual Studio Async CTP dojde ke konfliktu s verzí Razor, která je součástí instalace nástrojů ASP.NET MVC 3. Ujistěte se, že se nepokoušíte nainstalovat Visual Studio Async CTP a verzi Razor do stejného počítače.
- Při úpravách zobrazení Razor (soubor. cshtml) nebude k dispozici položka nabídky přejít na řadič v aplikaci Visual Studio a neexistují žádné fragmenty kódu.

<a id="TOC_ASP_NET_3_Beta"></a>
## <a name="aspnet-mvc-3-beta"></a>ASP.NET MVC 3 beta

ASP.NET MVC 3 beta byla vydána 6. října 2010. Následující poznámky jsou specifické pro beta verzi a vztahují se na všechny aktualizace nebo změny, na které odkazuje část ASP.NET MVC 3 Release Candidate výše.

## <a id="0.1__Toc274034215"></a>New Featuresin ASP.NET MVC 3 beta

<a id="0.1__Default_validation_system"></a>Tato část popisuje funkce, které byly představeny ve verzi ASP.NET MVC 3 beta.

### <a id="0.1__Toc274034216"></a>Správce balíčků NuGet

ASP.NET MVC 3 zahrnuje Správce balíčků NuGet, což je integrovaný nástroj pro správu balíčků pro přidávání knihoven a nástrojů do projektů sady Visual Studio. Ve většině případů automatizuje kroky, které vývojáři dnes využívají, aby získaly knihovnu do zdrojového stromu.

S NuGet můžete pracovat jako s nástrojem příkazového řádku, jako s integrovaným oknem konzoly v sadě Visual Studio 2010, v místní nabídce sady Visual Studio a jako sadou rutin PowerShellu.

Další informace o NuGet najdete v [dokumentaci k NuGet](https://docs.microsoft.com/nuget/).

### <a id="0.1__Toc274034217"></a>Vylepšený dialog Nový projekt

Při vytváření nového projektu teď dialogové okno Nový projekt umožňuje určit modul zobrazení i typ projektu ASP.NET MVC.

![](mvc3-release-notes/_static/image6.png)

V této verzi není zahrnutá podpora pro úpravu seznamu šablon a zobrazení modulů, které jsou uvedené v tomto dialogu.

Výchozí šablony jsou následující:

Obsahovat. Obsahuje minimální sadu souborů pro projekt ASP.NET MVC, včetně výchozí adresářové struktury pro projekty ASP.NET MVC, malého souboru. CSS, který obsahuje výchozí styly ASP.NET MVC, a adresáře skriptů, které obsahují výchozí soubory JavaScriptu.

Internetovou aplikaci. Obsahuje ukázkové funkce, které demonstrují, jak používat poskytovatele členství v rámci ASP.NET MVC.

### <a id="0.1__Toc274034218"></a>Zjednodušený způsob, jak zadat modely silného typu v zobrazeních Razor

Způsob určení typu modelu pro zobrazení se silnými typy Razor byl zjednodušen pomocí nové direktivy @model pro zobrazení CSHTML a direktivy @ModelType pro zobrazení VBHTML. V dřívějších verzích ASP.NET MVC byste zadali model silného typu pro zobrazení Razor tímto způsobem:

[!code-cshtml[Main](mvc3-release-notes/samples/sample25.cshtml)]

V této verzi můžete použít následující syntaxi:

[!code-cshtml[Main](mvc3-release-notes/samples/sample26.cshtml)]

### <a id="0.1__Toc274034219"></a>Podpora pro nové pomocné metody webových stránek ASP.NET

Technologie New ASP.NET Web Pages zahrnuje sadu pomocných metod, které jsou užitečné pro přidání běžně používaných funkcí do zobrazení a řadičů. ASP.NET MVC 3 podporuje používání těchto pomocných metod v rámci řadičů a zobrazení (tam, kde je to vhodné). Tyto metody jsou obsaženy v sestavení System. Web. Helpers. Následující tabulka uvádí několik pomocných metod ASP.NET webových stránek.

| **Podpůrn** | **Popis** |
| --- | --- |
| Graf | Vykreslí graf v rámci zobrazení. Obsahuje metody, jako je například Chart. ToWebImage, Chart. Save a Chart. Write. |
| SGC | Používá algoritmy hash k vytváření správně nasolených a zatřiďovacích hesel. |
| WebGrid | Vykreslí kolekci objektů (obvykle data z databáze) jako mřížku. Podporuje stránkování a řazení. |
| Webimage | Vykreslí obrázek. |
| Webová pošta | Pošle e-mailovou zprávu. |

Stručné téma s přehledem obsahuje seznam pomocníků a základní syntaxe je k dispozici jako součást dokumentace ASP.NET syntaxe Razor na následující adrese URL:

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-api-reference](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)

### <a id="0.1__Toc274034220"></a>Podpora vkládání dalších závislostí

V rámci verze Preview 1 pro ASP.NET MVC 3 je v aktuální verzi zahrnutá podpora pro dvě nové služby a čtyři existující služby a vylepšená podpora pro řešení závislosti a běžný lokátor služby.

#### <a name="new-icontrolleractivator-interface-for-fine-grained-controller-instantiation"></a>Nové rozhraní IControllerActivator pro vytvoření podrobného vytváření instancí kontroleru

Nové rozhraní IControllerActivator poskytuje podrobnější kontrolu nad tím, jak se vytváří instance řadičů přes vkládání závislostí. Následující příklad ukazuje rozhraní:

[!code-csharp[Main](mvc3-release-notes/samples/sample27.cs)]

Naproti tomu roli objektu pro vytváření kontroléru. Továrna kontroleru je implementací rozhraní IControllerFactory, které zodpovídá jak při hledání typu kontroleru, tak při vytváření instancí instance daného typu kontroleru.

Aktivátory kontroleru jsou zodpovědné jenom za vytvoření instance typu kontroleru. Neprovádějí vyhledávání typu řadiče. Po nalezení správného typu kontroleru by se továrny kontrolérů měly delegovat na instanci IControllerActivator, aby zpracovávala vlastní instanci řadiče.

Třída DefaultControllerFactory má nový konstruktor, který přijímá instanci IControllerFactory. To umožňuje použít vkládání závislostí pro správu tohoto aspektu vytváření kontroléru, aniž by bylo nutné přepsat výchozí chování při vyhledávání typu řadiče.

#### <a name="iservicelocator-interface-replaced-with-idependencyresolver"></a>Rozhraní IServiceLocator nahrazené IDependencyResolver

V závislosti na názorech komunity nahradila verze ASP.NET MVC 3 beta použití rozhraní IServiceLocator s rozhraním slimmed IDependencyResolver, které je specifické pro potřeby ASP.NET MVC. Následující příklad ukazuje nové rozhraní:

[!code-csharp[Main](mvc3-release-notes/samples/sample28.cs)]

V rámci této změny byla třída ServiceLocator nahrazena také třídou DependencyResolver. Registrace překladače závislostí se podobá starší verzi ASP.NET MVC:

[!code-csharp[Main](mvc3-release-notes/samples/sample29.cs)]

Implementace tohoto rozhraní by měla jednoduše delegovat na podkladový kontejner injektáže závislosti a poskytnout tak registrovanou službu pro požadovaný typ.

Pokud nejsou k dispozici žádné registrované služby požadovaného typu, ASP.NET MVC očekává, že implementace tohoto rozhraní vrátí hodnotu null ze služby GetService a vrátí prázdnou kolekci ze služeb GetService.

Nová třída DependencyResolver umožňuje registrovat třídy, které implementují nové rozhraní IDependencyResolver nebo rozhraní IServiceLocator (Common Service Locator Interface). Další informace o běžných lokátorech služby najdete v tématu [CommonServiceLocator na GitHubu](https://github.com/unitycontainer/commonservicelocator).

<a id="0.1__Breaking_Changes"></a>

#### <a name="new-iviewactivator-interface-for-fine-grained-view-page-instantiation"></a>Nové rozhraní IViewActivator pro detailní vytváření instancí stránky zobrazení

Nové rozhraní IViewPageActivator poskytuje podrobnější kontrolu nad tím, jak jsou stránky zobrazení vytvořeny pomocí injektáže závislostí. To platí pro instance WebFormView i pro instance RazorView. Následující příklad ukazuje nové rozhraní:

[!code-csharp[Main](mvc3-release-notes/samples/sample30.cs)]

Tyto třídy nyní přijímají argument konstruktoru IViewPageActivator, který umožňuje použití injektáže závislosti k řízení, jak jsou vytvořeny instance ViewPage, ViewUserControl a WebViewPage.

#### <a name="new-dependency-resolver-support-for-existing-services"></a>Nová podpora překladače závislostí pro existující služby

Nová verze zahrnuje podporu překladu závislostí pro následující služby:

- Poskytovatelé ověřování modelu. Třídy, které implementují ModelValidatorProvider, můžou být zaregistrované v překladači závislostí a systém je bude používat k podpoře ověřování na straně klienta a serveru.
- Poskytovatel metadat modelu Jedna třída, která implementuje ModelMetadataProvider, může být registrována v překladači závislostí a systém ji bude používat k poskytování metadat pro šablonování a ověřovací systémy.
- Zprostředkovatelé hodnot. Třídy, které implementují ValueProviderFactory, mohou být registrovány v překladači závislostí a systém je bude používat k vytvoření zprostředkovatelů hodnot, které jsou spotřebovány řadičem a během vazby modelu.
- Pořadače modelů. Třídy, které implementují IModelBinderProvider, mohou být registrovány v překladači závislostí a systém je bude používat k vytváření pořadačů modelů, které jsou spotřebovány systémem vazby modelu.

### <a id="0.1__Toc274034221"></a>Nová podpora pro nenápad AJAX na bázi jQuery

ASP.NET MVC obsahuje pomocné metody AJAX, například následující:

- AJAX. ActionLink
- AJAX. RouteLink
- AJAX. BeginForm
- AJAX. BeginRouteForm

Tyto metody používají JavaScript k vyvolání metody akce na serveru místo použití úplného zpětného volání. Tato funkce se aktualizovala tak, aby využívala nenápadný způsob. Namísto rušivého vygenerování vložených klientských skriptů tyto pomocné metody oddělují chování od značky tím, že generují atributy HTML5 pomocí předpony *data-AJAX* . Chování se pak aplikuje na značky odkazem na příslušné soubory JavaScriptu. Ujistěte se, že jsou odkazovány následující soubory jazyka JavaScript:

- jQuery 1.4.1. js
- jQuery. unnápad. Ajax. js

Tato funkce je ve výchozím nastavení povolená v souboru Web. config v ASP.NET MVC 3 nové šablony projektu, ale ve výchozím nastavení je pro existující projekty zakázané. Další informace najdete v tématu [přidané příznaky pro aplikaci pro ověřování klientů a](#0.1_AddedApplicationWideFlagsForClientValida) nenáročného JavaScriptu na později v tomto dokumentu.

### <a id="0.1__Toc274034222"></a>Nová podpora pro nenápadné ověřování jQuery

Ve výchozím nastavení používá ASP.NET MVC 3 beta nezpůsobující ověřování jQuery, aby bylo možné provádět ověřování na straně klienta. Pokud chcete povolit nenápadné ověřování klientů, udělejte v zobrazení volání jako v následujícím seznamu:

[!code-csharp[Main](mvc3-release-notes/samples/sample31.cs)]

To vyžaduje, aby vlastnost ViewContext. UnobtrusiveJavaScriptEnabled byla nastavena na hodnotu true, což lze provést provedením následujících volání:

[!code-csharp[Main](mvc3-release-notes/samples/sample32.cs)]

Také se ujistěte, že jsou odkazovány následující soubory jazyka JavaScript.

- jQuery 1.4.1. js
- jQuery. Validate. js
- jQuery. Validate. nenáročná. js

Tato funkce je ve výchozím nastavení povolená v souboru Web. config v ASP.NET MVC 3 nové šablony projektu, ale ve výchozím nastavení je pro existující projekty zakázané. Další informace najdete v tématu [nové příznaky pro ověřování klientů v úrovni aplikace a](#0.1_AddedApplicationWideFlagsForClientValida) nenáročného JavaScriptu v tomto dokumentu.

<a id="0.1__Toc274034223"></a>

### <a id="0.1_AddedApplicationWideFlagsForClientValida"></a>Nové příznaky pro aplikaci pro ověřování klienta a nenáročnému JavaScriptu

Můžete povolit nebo zakázat ověřování klienta a nenápadit globálně JavaScript pomocí statických členů třídy HtmlHelper, jak je uvedeno v následujícím příkladu:

[!code-csharp[Main](mvc3-release-notes/samples/sample33.cs)]

Výchozí šablony projektu umožňují ve výchozím nastavení nenápadný JavaScript. Tyto funkce můžete povolit nebo zakázat v kořenovém souboru Web. config aplikace pomocí následujících nastavení:

[!code-xml[Main](mvc3-release-notes/samples/sample34.xml)]

Vzhledem k tomu, že tyto funkce můžete ve výchozím nastavení povolit, byly do třídy HtmlHelper zavedena nová přetížení, která umožňují přepsat výchozí nastavení, jak je znázorněno v následujících příkladech:

[!code-csharp[Main](mvc3-release-notes/samples/sample35.cs)]

Z důvodu zpětné kompatibility jsou obě tyto funkce ve výchozím nastavení zakázané.

### <a id="0.1__Toc274034224"></a>Nová podpora kódu, který se spouští před spuštěním zobrazení

Nyní můžete umístit soubor s názvem \_viewstart. cshtml (nebo \_viewstart. vbhtml) do adresáře views a přidat do něj kód, který bude sdílen mezi více zobrazeními v tomto adresáři a jeho podadresáři. Například můžete vložit následující kód do stránky \_viewstart. cshtml ve složce ~/Views:

[!code-cshtml[Main](mvc3-release-notes/samples/sample36.cshtml)]

Tím nastavíte stránku rozložení pro každé zobrazení ve složce zobrazení a všechny její podsložky rekurzivně. Při vykreslování zobrazení se kód v souboru \_viewstart. cshtml spustí před spuštěním kódu zobrazení. Kód \_viewstart. cshtml se vztahuje na všechna zobrazení v této složce.

Ve výchozím nastavení se kód v souboru \_viewstart. cshtml vztahuje také na zobrazení v jakékoli podsložce. Jednotlivé podsložky však mohou mít vlastní verzi souboru \_viewstart. cshtml; v takovém případě má přednost místní verze. Chcete-li například spustit kód, který je společný pro všechna zobrazení pro HomeController, \_vložte soubor viewstart. cshtml do složky ~/Views/Home.

### <a id="0.1__Toc274034225"></a>Nová podpora pro syntaxi VBHTML Razor

Předchozí ASP.NET MVC Preview zahrnuje podporu pro zobrazení pomocí syntaxe Razor založené na C#. V těchto zobrazeních se používá Přípona souboru. cshtml. V rámci průběžné práce na podporu Razor zavádí ASP.NET MVC 3 beta podporu syntaxe Razor v Visual Basic, která používá příponu souboru. vbhtml.

Úvod k použití syntaxe Visual Basic na stránkách VBHTML najdete v kurzu na následující adrese URL:

[https://www.asp.net/webmatrix/tutorials/asp-net-web-pages-visual-basic](../web-pages/overview/getting-started/introducing-razor-syntax-vb.md)

### <a id="0.1__Toc274034226"></a>Přesnější řízení nad ValidateInputAttribute

ASP.NET MVC má vždycky zahrnutou třídu ValidateInputAttribute, která volá základní infrastrukturu ověřování žádostí ASP.NET, aby se zajistilo, že příchozí požadavek neobsahuje potenciálně škodlivý vstup. Ve výchozím nastavení je povoleno ověřování vstupu. Ověření žádosti je možné zakázat pomocí atributu ValidateInputAttribute, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](mvc3-release-notes/samples/sample37.cs)]

Mnoho webových aplikací však má jednotlivá pole formuláře, která musí umožňovat jazyk HTML, zatímco zbývající pole by neměla. Třída ValidateInputAttribute nyní umožňuje zadat seznam polí, která by neměla být obsažena v žádosti o ověření.

Pokud například vyvíjíte modul blogu, možná budete chtít v poli tělo a souhrnu použít označení. Tato pole mohou být reprezentovány dvěma vstupními prvky, každý s atributem názvu odpovídajícím názvu vlastnosti ("tělo" a "summary"). Chcete-li zakázat ověření žádosti pouze pro tato pole, zadejte názvy (oddělené čárkami) ve vlastnosti Exclude třídy metodě ValidateInput, jak je uvedeno v následujícím příkladu:

[!code-csharp[Main](mvc3-release-notes/samples/sample38.cs)]

### <a id="0.1__Toc274034227"></a>Pomáhat pomocníkům při převodu podtržítek na spojovníky názvů atributů HTML zadaných pomocí anonymních objektů

Pomocné metody umožňují zadat páry název-hodnota atributu pomocí anonymního objektu, jak je uvedeno v následujícím příkladu:

[!code-csharp[Main](mvc3-release-notes/samples/sample39.cs)]

Tento přístup neumožňuje používat spojovníky v názvu atributu, protože spojovník nelze použít pro název vlastnosti v ASP.NET. Pomlčky jsou však důležité pro vlastní atributy HTML5; HTML5 například používá předponu "data-".

Ve stejnou dobu nelze podtržítka použít pro názvy atributů ve formátu HTML, ale jsou platné v rámci názvů vlastností. Proto pokud zadáte atributy pomocí anonymního objektu a pokud názvy atributů obsahují podtržítko,, pomocné metody převedou podtržítka na spojovníky. Například následující syntaxe pomocníka používá podtržítko:

[!code-csharp[Main](mvc3-release-notes/samples/sample40.cs)]

Předchozí příklad vykresluje následující kód při spuštění pomocníka:

[!code-html[Main](mvc3-release-notes/samples/sample41.html)]

## <a id="0.1__Toc274034228"></a>Opravy chyb

Výchozí šablona objektu pro pomocníky šablony EditorFor a DisplayFor teď podporuje řazení určené ve vlastnosti DisplayAttribute. Order. (V předchozích verzích se nastavení Order nepoužilo.)

Ověřování klienta teď podporuje ověřování přepsaných vlastností, u kterých se aplikují atributy ověřování.

Služba JsonValueProviderFactory je nyní registrována ve výchozím nastavení.

## <a id="0.1__Toc274034229"></a>Průlomové změny

Pořadí spouštění pro filtry výjimek se změnilo pro filtry výjimek, které mají stejnou hodnotu Order. V ASP.NET MVC 2 a starších verzích filtry výjimek na kontroleru se stejným pořadím jako u metody Action byly provedeny před filtry výjimek v metodě Action. Obvykle se jedná o případ, kdy byly filtry výjimek aplikovány bez zadané hodnoty pořadí. V ASP.NET MVC 3 bylo toto pořadí obráceno, aby se nejdříve nastavila většina specifická obslužná rutina výjimky. V případě, že je vlastnost Order explicitně určena jako v dřívějších verzích, jsou filtry spouštěny v zadaném pořadí.

## <a id="0.1__Toc274034230"></a>Známé problémy

Během instalace se v dialogovém okně přijetí smlouvy EULA zobrazí licenční podmínky v okně, které je menší než určené.

Zobrazení Razor nemají podporu technologie IntelliSense ani zvýrazňování syntaxe. Očekává se, že podpora pro syntaxe Razor v aplikaci Visual Studio bude zahrnutá jako součást novější verze.

Při úpravách zobrazení Razor (soubor cshtml) <a id="0.1__Toc224729061"></a> <a id="0.1__Toc238051347"></a> nebude k dispozici položka nabídky přejít na řadič v aplikaci Visual Studio a neexistují žádné fragmenty kódu.

Při použití syntaxe @model pro určení silně typovaného zobrazení CSHTML nejsou rozpoznány jazykové zkratky pro typy. Například @model int nebude fungovat, ale @model Int32 bude fungovat. Alternativním řešením pro tuto chybu je použití skutečného názvu typu při zadání typu modelu.

Při použití syntaxe @model k určení silně typovaného zobrazení CSHTML (nebo @ModelType určení zobrazení typu VBHTML se silným typem) nejsou podporované typy s možnou hodnotou null a deklarace polí. Například @model int? není podporováno. Použijte místo toho `@model Nullable<Int32>`. Syntaxe @model řetězec [] není také podporována; místo toho použijte `@model IList<string>`.

Při upgradu projektu ASP.NET MVC 2 na ASP.NET MVC 3 nezapomeňte přidat následující do oddílu appSettings souboru Web. config:

[!code-xml[Main](mvc3-release-notes/samples/sample42.xml)]

Došlo k známému problému, který způsobí, že ověřování pomocí formulářů vždy přesměruje neověřené uživatele na ~/Account/Login a ignoruje nastavení ověřování pomocí formulářů použité v souboru Web. config. Alternativním řešením je přidat následující nastavení aplikace.

[!code-xml[Main](mvc3-release-notes/samples/sample43.xml)]

## <a id="0.1__Toc274034231"></a>Právní omezení

© 2011 Microsoft Corporation. Všechna práva vyhrazena. Tento dokument se poskytuje "tak, jak je". Informace a názory vyjádřené v tomto dokumentu, včetně adres URL a dalších odkazů na internetové weby, se mohou bez předchozího oznámení změnit. Berete na sebe rizika spojená s jeho používáním.

Tento dokument vám neposkytuje žádná zákonná práva k žádnému duševnímu vlastnictví v jakémkoli produktu společnosti Microsoft. Tento dokument můžete kopírovat a používat pro vaše interní referenční účely.

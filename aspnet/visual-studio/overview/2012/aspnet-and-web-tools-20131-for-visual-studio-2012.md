---
uid: visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
title: Poznámky k verzi pro ASP.NET and Web Tools 2013,1 pro Visual Studio 2012 | Microsoft Docs
author: microsoft
description: Tento dokument popisuje vydání ASP.NET and Web Tools 2013,1 pro sadu Visual Studio 2012.
ms.author: riande
ms.date: 11/13/2013
ms.assetid: ca26e5bb-630e-41d2-8512-2a9386c431cb
msc.legacyurl: /visual-studio/overview/2012/aspnet-and-web-tools-20131-for-visual-studio-2012
msc.type: authoredcontent
ms.openlocfilehash: 260af1018064d60d80cbb1002001f28c4daffffd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578440"
---
# <a name="release-notes-for-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Poznámky k verzi pro ASP.NET a webové nástroje 2013.1 pro Visual Studio 2012

od [Microsoftu](https://github.com/microsoft)

> Tento dokument popisuje vydání ASP.NET and Web Tools 2013,1 pro sadu Visual Studio 2012.

## <a name="contents"></a>Obsah

- [Poznámky k instalaci](#install)
- [Požadavky na software](#requirements)
- Nové funkce v ASP.NET and Web Tools 2013,1 pro Visual Studio 2012

    - [Bootstrap](#bootstrap)
    - [Šablony](#templates)

        - [Šablona MVC 5 pro ASP.NET](#mvc5template)
        - [Šablona webového rozhraní API 2 pro ASP.NET](#apitemplate)
        - [Šablony položek](#itemtemplate)
    - [Entity Framework 6](#ef6)
    - [ASP.NET generování uživatelského rozhraní](#scaffold)
    - [Editor Razor](#razor)
    - [NuGet 2.7](#nuget)
- Známé problémy a zásadní změny

    - [ASP.NET generování uživatelského rozhraní](#issuescaffolding)

        - [Rozhraní API pro MVC a webové rozhraní API – chyba při nenalezení protokolu HTTP 404](#404issue)
        - [Visual Studio Express 2012 pro web přestane fungovat po přidání vygenerované položky](#expressissue)
    - [ASP.NET Razor 3](#issuerazor)

        - [Zobrazení souboru CSHTML s procházením nebo F5 způsobuje chybu serveru](#browseissue)
        - [Přepsání adresy URL a tilda (~)](#rewriteissue)
    - [Šablony](#templateissue)

<a id="install"></a>
## <a name="installation-notes"></a>Poznámky k instalaci

[Nainstalovat](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WebNode11Pack.appids) ASP.NET and Web Tools 2013,1 pro Visual Studio 2012.

<a id="requirements"></a>
## <a name="software-requirements"></a>Požadavky na software

Pro web musíte mít buď Visual Studio 2012, nebo Visual Studio Express 2012.

## <a name="new-features-in-aspnet-and-web-tools-20131-for-visual-studio-2012"></a>Nové funkce v ASP.NET and Web Tools 2013,1 pro Visual Studio 2012

<a id="bootstrap"></a>
### <a name="bootstrap"></a>Spouštěcí rutina

Při generování uživatelského rozhraní a zobrazení řadiče MVC 5 označení pro zobrazení používá [bootstrap](http://getbootstrap.com/).

<a id="templates"></a>
### <a name="templates"></a>Šablony

<a id="mvc5template"></a>
#### <a name="aspnet-mvc-5-template"></a>Šablona MVC 5 pro ASP.NET

Přidali jsme novou šablonu MVC 5. Odkazuje na nejnovější balíčky NuGet sady MVC 5 a pomocí generování uživatelského rozhraní můžete přidat řadiče a zobrazení.

<a id="apitemplate"></a>
#### <a name="aspnet-web-api-2-template"></a>Šablona webového rozhraní API 2 pro ASP.NET

Přidali jsme novou šablonu webového rozhraní API 2. Odkazuje na nejnovější balíčky rozhraní Web API 2 NuGet a pomocí generování uživatelského rozhraní můžete přidat řadiče a zobrazení.

<a id="itemtemplate"></a>
#### <a name="item-templates"></a>Šablony položek

Přidali jsme nové šablony položek pro zobrazení MVC 5, webové stránky (Razor 3) a ovladače webového rozhraní API 2. Při přidávání nových položek nainstalují do projektu související balíčky NuGet.

<a id="ef6"></a>
### <a name="entity-framework-6"></a>Entity Framework 6

Při generování uživatelského rozhraní MVC nebo kontroleru webového rozhraní API pomocí Entity Framework používáme rozhraní .NET Framework 6. Další informace o Entity Framework najdete v tématu [Historie verzí Entity Framework](https://msdn.com/data/jj574253).

Můžete si také stáhnout a nainstalovat nástroje Entity Framework 6 pro Visual Studio 2012. Viz část [Get Entity Framework](https://msdn.com/data/ee712906#tooling).

<a id="scaffold"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET generování uživatelského rozhraní

Generování uživatelského rozhraní ASP.NET je rozhraní pro generování kódu pro webové aplikace v ASP.NET. Umožňuje snadno přidat do projektu často používaný kód, který komunikuje s datovým modelem.

V předchozích verzích sady Visual Studio bylo generování uživatelského rozhraní omezeno na ASP.NET projekty MVC. V této aktualizaci teď můžete použít generování uživatelského rozhraní pro libovolný projekt ASP.NET, včetně webových formulářů. Tato aktualizace nepodporuje generování stránek pro projekt webových formulářů, ale můžete stále používat generování uživatelského rozhraní s webovými formuláři přidáním závislostí MVC do projektu. Do budoucí aktualizace se přidají podpora pro generování stránek webových formulářů.

Při použití generování uživatelského rozhraní zajišťujeme, aby byly v projektu nainstalované všechny požadované závislosti. Například pokud začnete s projektem ASP.NET Web Forms a potom použijete generování uživatelského rozhraní pro přidání kontroleru webového rozhraní API, požadované balíčky NuGet a odkazy se automaticky přidají do projektu.

Chcete-li přidat generování uživatelského rozhraní MVC do projektu webových formulářů, přidejte **novou vygenerované položky** a v dialogovém okně vyberte **závislosti MVC 5** . K dispozici jsou dvě možnosti pro generování uživatelského rozhraní MVC; Minimální a plná. Pokud vyberete minimální, do projektu se přidají jenom balíčky NuGet a odkazy pro ASP.NET MVC. Pokud vyberete možnost úplná, budou přidány minimální závislosti a také požadované soubory obsahu pro projekt MVC.

Podpora pro generování generovaných asynchronních řadičů používá nové asynchronní funkce z Entity Framework 6.

Další informace a kurzy najdete v tématu [Přehled generování uživatelského rozhraní ASP.NET](../2013/aspnet-scaffolding-overview.md). Tyto kurzy ukazují generování uživatelského rozhraní s Visual Studio 2013, ale platí také pro ASP.NET and Web Tools 2013,1 pro Visual Studio 2012.

<a id="razor"></a>
### <a name="razor-editor"></a>Editor Razor

V této aktualizaci Visual Studio 2012 teď podporuje nástroje a úpravy Razor 3.

<a id="nuget"></a>
### <a name="nuget-27"></a>NuGet 2.7

NuGet 2,7 obsahuje bohatou sadu nových funkcí, které jsou podrobně popsány v [poznámkách k verzi nuget 2,7](http://docs.nuget.org/docs/release-notes/nuget-2.7).

Tato verze NuGet neumožňuje uživatelům explicitně dovolit NuGet obnovovat chybějící balíčky. Při instalaci NuGet 2,7 budou uživatelé implicitně souhlasit s automatickým obnovením chybějících balíčků. Uživatelé se můžou výslovně odhlásit z obnovení balíčků prostřednictvím nastavení NuGet v aplikaci Visual Studio. Tato změna zjednodušuje způsob, jakým funguje obnovení balíčku.

## <a name="known-issues-and-breaking-changes"></a>Známé problémy a zásadní změny

<a id="issuescaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET generování uživatelského rozhraní

<a id="404issue"></a>
#### <a name="mvc-and-web-api-scaffolding---http-404-not-found-error"></a>Rozhraní API pro MVC a webové rozhraní API – chyba při nenalezení protokolu HTTP 404

Pokud narazíte na chybu při přidávání vygenerované položky do projektu, je možné, že váš projekt zůstane v nekonzistentním stavu. Některé změny generované generováním uživatelského rozhraní se vrátí zpátky, ale jiné změny, třeba nainstalované balíčky NuGet, se nebudou vracet zpátky. Pokud se změny konfigurace směrování vrátí zpět, uživatelům se při přechodu na vygenerované položky zobrazí chyba HTTP 404.

Pokud chcete tuto chybu pro MVC opravit, přidejte novou vygenerované položky a vyberte závislosti MVC 5 (minimální nebo plné). Tento proces přidá všechny požadované změny do projektu.

Oprava této chyby pro webové rozhraní API:

1. Do projektu přidejte následující třídu WebApiConfig.

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample1.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample2.vb)]
2. Nakonfigurujte WebApiConfig. Register v aplikaci\_metodu Start v Global. asax následujícím způsobem:

    [!code-csharp[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample3.cs)]

    [!code-vb[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample4.vb)]

<a id="expressissue"></a>
#### <a name="visual-studio-express-2012-for-web-stops-working-after-adding-a-scaffolded-item"></a>Visual Studio Express 2012 pro web přestane fungovat po přidání vygenerované položky

Pokud Visual Studio Express 2012 pro web přestane fungovat po přidání vygenerované položky s Entity Framework (například kontroler webového rozhraní API 2 s akcemi pomocí Entity Framework), je možné, že se Visual Studio Express nepodařilo načíst nativní bitovou kopii sestavení. závisí na System. Web. Extensions.

Chcete-li tento problém vyřešit, nakonfigurujte Visual Studio Express pro práci s imagí jazyka MSIL typu System. Web. Extensions:

1. Otevřete příkazový řádek v režimu správce.
2. Přejít na%ProgramFiles%\Microsoft Visual Studio 11.0 \ Common7\IDE nebo% ProgramFiles (x86)% \ Microsoft Visual Studio 11.0 \ Common7\IDE (pro 64 bitových oken).
3. V textovém editoru otevřete soubor VWDExpress. exe. config.
4. Přidejte následující řádek pod &lt;konfigurační&gt;/&lt;modulu runtime&gt;:  

    [!code-xml[Main](aspnet-and-web-tools-20131-for-visual-studio-2012/samples/sample5.xml)]
5. Restartujte Visual Studio Express 2012 pro web.

<a id="issuerazor"></a>
### <a name="aspnet-razor-3"></a>ASP.NET Razor 3

<a id="browseissue"></a>
#### <a name="viewing-cshtml-file-with-browse-with-or-f5-causes-a-server-error"></a>Zobrazení souboru CSHTML s procházením nebo F5 způsobuje chybu serveru

Když vytvoříte projekt MVC 5 v aplikaci Visual Studio 2012 (nebo otevřete v aplikaci Visual Studio 2012 projekt MVC 5, který byl vytvořen v Visual Studio 2013), a pokusíte se zobrazit soubor cshtml pomocí příkazu procházet s nebo F5, zobrazí se chyba oznamující, že **Chyba serveru v aplikaci/** . Server se pokusí přejít na `http://localhost:XXXX/Views/../XXXX.cshtml`

Chcete-li tento problém vyřešit, změňte nastavení **Akce spuštění** v projektu na **konkrétní stránku**. Pro stránku nemusíte zadávat hodnotu.

![](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image1.png)

Po provedení této změny vyberete F5 přejít na kořen vaší aplikace (`http://localhost:XXXX`). Toto chování není stejné jako chování pro projekty MVC 5 v Visual Studio 2013, kde **aktuální nastavení stránky** spouští otevřenou stránku.

<a id="rewriteissue"></a>
#### <a name="url-rewrite-and-tilde"></a>Přepsání adresy URL a tilda (~)

Po upgradu na ASP.NET Razor 3 nebo ASP.NET MVC 5 již nemusí zápis tildy (~) fungovat správně, pokud používáte přepisy URL. Přepsání adresy URL má vliv na znak tilda (~) v prvcích HTML, jako je například &lt;A/&gt;, &lt;SCRIPT/&gt;, &lt;LINK/&gt;, a v důsledku toho není tilda nadále namapována do kořenového adresáře.

Například pokud přepíšete požadavky pro **ASP.NET/Content** do **ASP.NET**, atribut href v &lt;a href = "~/content/"/&gt; překládá na **/Content/Content/** namísto **/** . Chcete-li tuto změnu potlačit, můžete nastavit **WasUrlRewritten kontext služby IIS\_** na hodnotu false na každé webové stránce nebo v **aplikaci\_beginRequest** v souboru Global. asax.

<a id="templateissue"></a>
### <a name="templates"></a>Šablony

Když vytváříte projekty ASP.NET MVC pomocí sady Visual Studio 2012 v systému Windows 8.1 nebo Windows Server 2012 R2, Visual Studio zobrazí chybovou zprávu s informací o tom, že se nezdařila konfigurace webu [URL] pro ASP.NET 4,5.

![Chyba konfigurace](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image2.png)

Tato chyba se zobrazí, protože Visual Studio 2012 nepovoluje funkci ASP.NET 4,5, když je nainstalovaná v těchto verzích Windows. Pokud chcete povolit ASP.NET 4,5, postupujte podle kroků popsaných v tématu [Zapnutí nebo vypnutí funkcí systému Windows](https://windows.microsoft.com/windows-8/turn-windows-features-on-off).

![Zapnutí nebo vypnutí funkcí Windows](aspnet-and-web-tools-20131-for-visual-studio-2012/_static/image3.png)

Alternativně můžete povolit ASP.NET 4,5 prostřednictvím příkazového řádku.

1. Otevřete příkazový řádek v režimu správce.
2. Spusťte následující příkaz, který povolí ASP.NET 4,5.  
    `dism /Online /Enable-Feature /FeatureName:NetFx4Extended-ASPNET45 /Quiet /NoRestart`

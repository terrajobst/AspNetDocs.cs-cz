---
uid: visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
title: ASP.NET and Web Tools 2013,2 pro Visual Studio 2013 poznámky k verzi | Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 03/06/2014
ms.assetid: 7ef5f73c-ca60-43c1-bdb2-702800347e7e
msc.legacyurl: /visual-studio/overview/2013/aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes
msc.type: authoredcontent
ms.openlocfilehash: 22d4d4afd6963f23d6cfef1745a859c20b69d599
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623191"
---
# <a name="aspnet-and-web-tools-20132--for-visual-studio-2013-release-notes"></a>ASP.NET a webové nástroje 2013.2 pro Visual Studio 2013 – poznámky k verzi

od [Microsoftu](https://github.com/microsoft)

## <a name="installation-notes"></a>Poznámky k instalaci

ASP.NET and Web Tools pro sadu Visual Studio 2013,2 jsou součástí hlavního instalačního programu a je možné je stáhnout jako součást [Visual Studio 2013 Update 2](https://go.microsoft.com/fwlink/?LinkId=390521).

## <a name="documentation"></a>Dokumentace

Kurzy a další informace o ASP.NET and Web Tools pro Visual Studio 2013,2 jsou k dispozici na webu [ASP.NET](https://www.asp.net/).

## <a name="software-requirements"></a>Požadavky na software

ASP.NET and Web Tools pro Visual Studio 2013,2 vyžaduje Visual Studio 2013.

## <a name="new-features-in-aspnet-and-web-tools-for-visual-studio-20132"></a>Nové funkce v ASP.NET and Web Tools pro Visual Studio 2013,2

V následujících částech jsou popsány funkce, které byly představeny v této verzi.

- [Jedna šablona projektu ASP.NET](#oneaspnet)
- [Při spouštění webových aplikací v IIS Express podporovat protokol SSL](#ssl)
- [Vylepšení webového editoru sady Visual Studio](#vswebeditor)
- [Browser Link](#browserlink)
- [Podpora pro Azure App Service Web Apps v aplikaci Visual Studio](#waws)
- [Vytvoření vzdálených prostředků Azure při vytváření nového webového projektu](#AzureResources)
- [Vylepšení publikování na webu](#webpublish)
- [ASP.NET generování uživatelského rozhraní](#scaffolding)
- [NuGet 2.8.1](#nuget)
- [Webové formuláře ASP.NET](#webforms)
- [ASP.NET MVC 5.1.2](#mvc)
- [ASP.NET webového rozhraní API 2.1.2](#webapi)
- [ASP.NET webové stránky 3.1.2](#webpages)
- [Entity Framework 6,1](#ef)
- [ASP.NET Identity 2.0.0](#identity)
- [Komponenty Microsoft OWIN](#owin)
- [2.0.2 signálu ASP.NET](#signalr)

<a id="oneaspnet"></a>
### <a name="one-aspnet-project-templates"></a>Jedna šablona projektu ASP.NET

- Aktualizace šablon projektů ASP.NET pro podporu potvrzení účtu a resetování hesla.
- Aktualizujte šablonu webového rozhraní API ASP.NET tak, aby podporovala ověřování pomocí místních účtů organizace.
- Šablona ASP.NET SPA teď obsahuje ověřování založené na zobrazeních MVC a na straně serveru. Šablona má kontroler WebAPI, ke kterému mají oprávnění pouze ověření uživatelé.

<a id="ssl"></a>
### <a name="support-ssl-when-launching-web-applications-on-iis-express"></a>Při spouštění webových aplikací v IIS Express podporovat protokol SSL

Abychom odstranili upozornění zabezpečení při procházení a ladění HTTPS na místním hostiteli, Přidali jsme dialog, který umožní aplikaci Internet Explorer a Chrome důvěřovat certifikátu IIS Express podepsaného svým držitelem.

Například vlastnost webového projektu může být nastavena na používání protokolu SSL. Kliknutím na F4 zobrazte dialogové okno Vlastnosti. Změňte možnost **SSL povoleno** na hodnotu true. Zkopírujte adresu URL protokolu SSL.

![Vlastnost s povoleným protokolem SSL](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image1.png)

Nastavte kartu webová stránka vlastností webového projektu tak, aby používala adresu URL založenou na protokolu HTTPS (adresa URL SSL bude `https://localhost:44300/`a, pokud jste předtím nevytvořili weby SSL.)

![Nastavit adresu URL projektu (HTTPS)](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image2.png)

Stiskněte klávesy CTRL+F5 a spusťte aplikaci. Postupujte podle pokynů pro důvěřování certifikátu podepsanému svým držitelem, který IIS Express vygeneroval.

![Upozornění SSL](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image3.png)

Přečtěte si dialogové okno **Upozornění zabezpečení** a pak klikněte na tlačítko **Ano** , pokud chcete nainstalovat certifikát reprezentující localhost.

![Bezpečnostní upozornění](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image4.png)

Tato lokalita se zobrazí v IE nebo Chrome bez upozornění certifikátu v prohlížeči.

![Stránka HTTPS bez upozornění](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image5.png)

Firefox používá vlastní úložiště certifikátů, takže zobrazí upozornění.

<a id="vswebeditor"></a>
### <a name="visual-studio-web-editor-enhancements"></a>Vylepšení webového editoru sady Visual Studio

- **Nová položka a Editor projektu JSON**: do sady Visual Studio jsme přidali položku a Editor projektu JSON. Aktuální funkce editoru JSON zahrnují zabarvení, ověřování syntaxe, dokončování složených závorek, nastavení možností nástrojů a další.

    ![JSON Editor](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image6.png)

    IntelliSense teď podporuje [schéma JSON](http://json-schema.org/) verze v3 a v4. K dispozici je pole se seznamem schématu, ve kterém můžete zvolit existující schémata, upravit cestu k místnímu schématu nebo jednoduše přetažením souboru JSON projektu na něj získat relativní cestu.

    ![JSON IntelliSense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image7.png)    ![Editor schémat JSON](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image8.png)
- **Nový editor Sass (scss)** : Přidali jsme méně ve VS2013 RTM a teď máme položku a Editor projektu Sass. Funkce editoru Sass jsou srovnatelné s editorem LESS a zahrnují zabarvení, proměnné a objekty Mixin IntelliSense, komentář/odložení, rychlé informace, formátování, ověřování syntaxe, sestavování, příkazu goto definition, výběr barvy, nastavení možností nástroje atd.

    ![Přidat novou položku: SCSS styly](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image9.png)    ![Editor šablon stylů](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image10.png)
- **Nový výběr adresy URL v dokumentech HTML, Razor, CSS, LESS a Sass:** VS 2013 dodána bez výběru adresy URL mimo stránky webových formulářů. Nový výběr adresy URL pro editory HTML, Razor, CSS, LESS a Sass je bezplatná dialogová okna pro výběr Fluent, které rozumí... a filtruje seznam souborů vhodně pro značky a odkazy img.

    ![Výběr adresy URL pro značku obrázku](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image11.png)    ![Výběr adresy URL pro zobrazení](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image12.png)    ![Výběr adresy URL pro šablony stylů CSS](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image13.png)
- **Aktualizace editoru LESS přidáním dalších funkcí**
- **Vyseknutí upgradu IntelliSense**: Přidali jsme nestandardní syntaxi vykrojení pro vs IntelliSense, "Ko-vs-šéfredaktor viewModel:" syntax. Dá se použít k vytvoření vazby na více modelů zobrazení na stránce pomocí komentářů ve formuláři:

    ![Vyseknutí IntelliSense](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image14.png)

    Přidali jsme také podporu pro vnořené ViewModel IntelliSense, takže můžete přejít na hluboce vnořené objekty na ViewModel.

    `<div data-bind="text: foo.bar.baz.etc" />`

    Zobrazená technologie IntelliSense je úplná technologie IntelliSense objektu JavaScriptu.

    ![IntelliSense znázorňující plný JavaScriptový objekt](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image15.png)
- **Nový výběr adresy URL v dokumentech HTML, Razor, CSS, LESS a Sass**: vs 2013 dodána bez výběru adresy URL mimo stránky webových formulářů. Nový výběr adresy URL pro editory HTML, Razor, CSS, LESS a Sass je bezplatná dialogová okna pro výběr Fluent, které rozumí... a filtruje seznam souborů vhodně pro značky a odkazy img.

    ![Výběr adresy URL pro značku obrázku](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image16.png)    ![Výběr adresy URL pro zobrazení](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image17.png)    ![Výběr adresy URL pro šablony stylů CSS](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image18.png)

<a id="browserlink"></a>
### <a name="browser-link"></a>Odkaz prohlížeče

- Odkaz na prohlížeč teď podporuje připojení HTTPS a zobrazí seznam, který je v řídicím panelu s dalšími připojeními, pokud je certifikát důvěryhodný pro prohlížeč.
- Statické mapování zdrojového kódu HTML
- Podpora SPA pro mapování dat
- Automaticky aktualizovat data mapování

<a id="waws"></a>
### <a name="support-for-azure-app-service-web-apps-in-visual-studio"></a>Podpora pro Azure App Service Web Apps v aplikaci Visual Studio

- **Podpora přihlášení Azure.**
- **Vzdálené ladění a vzdálené zobrazení pro webové aplikace**: teď podporujeme [vzdálené ladění pro webové aplikace v Azure App Service](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio) a vzdálené zobrazení souborů obsahu webové aplikace v Průzkumníku serveru.

<a id="AzureResources"></a>
### <a name="create-remote-azure-resources-when-creating-a-new-web-project"></a>Vytvoření vzdálených prostředků Azure při vytváření nového webového projektu

Do dialogového okna Nová webová aplikace jsme přidali zaškrtávací políčko pro [Vytvoření vzdálených prostředků](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet) v Azure. Výběrem této možnosti budete moci integrovat možnosti vytváření nové webové aplikace, nastavení webu pro publikování Azure pro testování a vytvoření profilu publikování v několika jednoduchých krocích.

![Nový projekt s prostředky Azure](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image19.png)![Publikování do Azure](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image20.png)

<a id="webpublish"></a>
### <a name="web-publish-enhancements"></a>Vylepšení publikování na webu

- Vylepšete uživatelské prostředí pro publikování.

<a id="scaffolding"></a>
### <a name="aspnet-scaffolding"></a>ASP.NET generování uživatelského rozhraní

- **Podpora výčtu:** Pokud model používá výčty, pak generátor MVC vygeneruje rozevírací seznam pro výčet. To používá pomocníka enum v MVC.
- **Podpora Bootstrap**: aktualizace šablon EditorFor v generování uživatelského rozhraní MVC, aby používaly třídy Bootstrap.
- **Podpora balíčků**: služby MVC a rozhraní Web API budou přidávat balíčky 5,1 pro MVC a webové rozhraní API.

Následující snímky obrazovky ukazují modely generování uživatelského rozhraní.

- Kód modelu:

     ![Kód modelu](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image21.png)
- Zkompilujte kód modelu, klikněte pravým tlačítkem myši a vyberte **Přidat**, **Nová vygenerovaná položka**.

     ![Přidat novou vygenerované položky](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image22.png)
- Vyberte **MVC5 Controller se zobrazeními, a to pomocí Entity Framework**:

     ![Přidat nový kontroler MVC5 se zobrazeními](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image23.png)
- **Přidat kontroler** pomocí modelu:

    ![](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image24.png)
- Zkontrolujte generovaný kód, například views/WeekdayModels/Edit. cshtml obsahuje `@Html.EnumDropDownListFor`: ![zobrazení obsahující](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image25.png) EnumDropDownListFor
- Spuštěním stránky zobrazíte vygenerované pole se seznamem, Všimněte si, že pokud hodnota může být null, lze pro pole se seznamem zvolit prázdný řetězec. Například na stránce **vytvořit** se zobrazí následující:

    ![Pole se seznamem umožňující prázdný řetězec](aspnet-and-web-tools-20132-preview-for-visual-studio-2013-release-notes/_static/image26.png)

<a id="nuget"></a>
### <a name="nuget-281"></a>NuGet 2.8.1

NuGet 2.8.1 RTM bude vydány v dubnu 2014. Tady jsou nejdůležitějšími body z poznámky k verzi, ale další informace o těchto změnách najdete v [úplném poznámkách k verzi](http://docs.nuget.org/docs/release-notes/nuget-2.8) .

- **Cílové aplikace Windows Phone 8,1**: NuGet 2.8.1 nyní podporuje cílení na Windows Phone 8,1 aplikace pomocí monikerů cílového rozhraní WINDOWSPHONEAPP, WPA, WINDOWSPHONEAPP81 a WPA81.

- **Řešení oprav pro závislosti**: při vyhodnocování závislostí balíčku NuGet implementovala strategii pro výběr nejnižší hlavní verze balíčku, která splňuje závislosti na balíčku. Na rozdíl od hlavní a dílčí verze však verze opravy vždy přeložila na nejvyšší verzi. I když bylo chování záměrně úmyslné, vytvořilo se nedostatečné determinismem pro instalaci balíčků se závislostmi.
- **DependencyVersion přepínač**: i když NuGet 2,8 mění *výchozí* chování pro řešení závislostí, přidá taky přesnější kontrolu nad procesem překladu závislostí prostřednictvím přepínače-DependencyVersion v konzole správce balíčků. Přepínač umožňuje překládat závislosti na nejnižší možnou verzi (výchozí chování), nejvyšší možnou verzi nebo nejvyšší dílčí nebo opravnou verzi. Tento přepínač funguje jenom pro rutinu Install-Package v příkazu PowerShellu.
- **DependencyVersion atribut**: kromě přepínače-DependencyVersion popsaného výše, NuGet taky povolil možnost nastavit nový atribut v souboru NuGet. config, který definuje výchozí hodnotu, pokud není přepínač-DependencyVersion zadaný při vyvolání Install-Package. Tuto hodnotu bude také respektován dialog správce balíčků NuGet pro všechny operace instalace balíčku. Chcete-li nastavit tuto hodnotu, přidejte do souboru NuGet. config atribut níže:

    `<config> <add key="dependencyversion" value="Highest" /> </config>`
- **Náhled operací NuGet s-whatIf**: některé balíčky NuGet můžou mít hloubkové grafy závislosti a jako takové můžou být užitečné při instalaci, odinstalaci nebo aktualizaci, abyste nejdřív viděli, co se stane. NuGet 2,8 přidá standardní PowerShell – co když se přepne na příkazy Install-Package, Uninstall-Package a Update-Package, aby se povolilo vizualizace celého uzavření balíčků, na které se příkaz použije.
- **Balíček downgrade**: není neobvyklé instalovat předprodejní verzi balíčku, aby bylo možné prozkoumat nové funkce a pak se rozhodnout vrátit zpět k poslední stabilní verzi. Před NuGet 2,8 se jednalo o proces odinstalace předprodejního balíčku a jeho závislostí a následná instalace starší verze. S NuGet 2,8 se ale balíček Update-Package vrátí zpátky celý uzávěr balíčku (například strom závislosti balíčku) na předchozí verzi.
- **Závislosti vývoje**: mnoho různých typů schopností lze doručovat jako balíčky NuGet – včetně nástrojů, které se používají pro optimalizaci procesu vývoje. Tyto komponenty, i když můžou být instrumentované při vývoji nového balíčku, by se při pozdějším publikování neměly považovat za závislost nového balíčku. NuGet 2,8 umožňuje balíčku identifikovat sám sebe v souboru. nuspec jako developmentDependency. Po nainstalování budou tato metadata také přidána do souboru Packages. config projektu, do kterého byl balíček nainstalován. Když se tento soubor Packages. config později analyzuje pro závislosti NuGet během balíčku NuGet. exe, vyloučí tyto závislosti označené jako závislosti na vývoji.
- **Jednotlivé soubory Packages. config pro různé platformy**: při vývoji aplikací pro více cílových platforem je běžné mít pro každé z těchto prostředí sestavení různé soubory projektu. Také je běžné využívat různé balíčky NuGet v různých souborech projektu, protože balíčky mají různé úrovně podpory pro různé platformy. NuGet 2,8 poskytuje vylepšenou podporu pro tento scénář vytvořením různých souborů Package. config pro různé soubory projektu specifické pro platformu.
- Přechod **na místní mezipaměť**: i když se balíčky NuGet typicky využívají ze vzdálené galerie, jako je například [galerie NuGet](http://www.nuget.org) pomocí síťového připojení, existuje mnoho scénářů, ve kterých klient není připojen. Bez připojení k síti klient NuGet nemohl úspěšně nainstalovat balíčky, i když už tyto balíčky na počítači klienta v místní mezipaměti NuGet. NuGet 2,8 přidá do konzoly Správce balíčků automatickou zálohu mezipaměti.

    Funkce Fallback mezipaměti nevyžaduje žádné konkrétní argumenty příkazu. Kromě toho záložní záloha v tuto chvíli funguje jenom v konzole správce balíčků – v dialogovém okně Správce balíčků to chování momentálně nefunguje.
- **Opravy chyb**: jedna z podstatných opravených chyb byla zlepšení výkonu v příkazu Update-Package-REINSTALL.

    Kromě těchto funkcí a výše zmíněné opravy výkonu obsahuje tato verze NuGet také mnoho dalších oprav chyb. V této verzi byly vyřešeny 181 celkové problémy. Úplný seznam pracovních položek opravených v NuGet 2,8 najdete v [přehledu problémů NuGet](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all) pro tuto verzi.

<a id="webforms"></a>
### <a name="aspnet-web-forms"></a>ASP.NET – webové formuláře

- Šablony webových formulářů nyní ukazují, jak provést potvrzení účtu a resetování hesla pro ASP.NET Identity.
- Řízení zdrojů dat entit a dynamické Zprostředkovatel dat pro Entity Framework 6. Další podrobnosti najdete na následujícím blogu MSDN: [poskytovatel dynamických dat a ovládací prvek EntityDataSource pro Entity Framework 6](https://blogs.msdn.com/b/webdev/archive/2014/01/30/announcing-preview-of-dynamic-data-provider-and-entitydatasource-control-for-entity-framework-6.aspx).

<a id="mvc"></a>
### <a name="aspnet-mvc-512"></a>ASP.NET MVC 5.1.2

- [Vylepšení směrování atributů](../../../mvc/overview/releases/mvc51-release-notes.md#AttributeRouting)
- [Podpora zavedení šablon editoru](../../../mvc/overview/releases/mvc51-release-notes.md#Bootstrap)
- [Podpora výčtu v zobrazeních](../../../mvc/overview/releases/mvc51-release-notes.md#Enum)
- [Nenáročná podpora atributů MinLength/MaxLength](../../../mvc/overview/releases/mvc51-release-notes.md#Unobtrusive)
- [Podpora kontextu this v nenápadu AJAX](../../../mvc/overview/releases/mvc51-release-notes.md#thisContext)
- Různé [opravy chyb](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=MVC&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webapi"></a>
### <a name="aspnet-web-api-212"></a>ASP.NET webového rozhraní API 2.1.2

- [Zpracování globálních chyb](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#global-error)
- [Vylepšení směrování atributů](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#attribute-routing)
- [Vylepšení stránky pro stránku s usnadněním](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#help-page)
- [Podpora IgnoreRoute](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#ignoreroute)
- [BSON – formátovací modul typu média](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#bson)
- [Lepší podpora pro asynchronní filtry](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#async-filters)
- [Analýza dotazů pro knihovnu formátování klienta](../../../web-api/overview/releases/whats-new-in-aspnet-web-api-21.md#query-parsing)
- Různé [opravy chyb](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20API%7cWeb%20API%20OData&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="webpages"></a>
### <a name="aspnet-web-pages-312"></a>ASP.NET webové stránky 3.1.2

- Různé [opravy chyb](https://aspnetwebstack.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=v5.1%20Preview%7cv5.1%20RTM&assignedTo=All&component=Web%20Pages/Razor&sortField=AssignedTo&sortDirection=Ascending&page=0&reasonClosed=Fixed)

<a id="ef"></a>
### <a name="entity-framework-61"></a>Entity Framework 6,1

Entity Framework byla aktualizována na verzi 6,1 pro modul runtime a nástroje. Entity Framework (EF) 6,1 je dílčí aktualizace pro Entity Framework 6 a obsahuje řadu oprav chyb a nové funkce. Podrobné informace o EF 6.1, včetně odkazů na dokumentaci pro nové funkce, najdete v tématu [Entity Framework Historie verzí](https://msdn.microsoft.com/data/jj574253). Mezi nové funkce v této verzi patří:

- **Konsolidace nástrojů** nabízí jednotný způsob, jak vytvořit nový model EF. Tato funkce rozšiřuje Průvodce model EDM (Entity Data Model) ADO.NET, aby podporoval vytváření Code Firstch modelů, včetně zpětné analýzy z existující databáze. Tyto funkce byly dříve dostupné v kvalitě beta verze nástroje EF Power Tools.
- **Zpracování chyb potvrzení transakce** poskytuje nové rozhraní [System. data. entity. Infrastructure. CommitFailureHandler](https://msdn.microsoft.com/library/system.data.entity.infrastructure.commitfailurehandler(v=vs.113).aspx) , které využívá nově zavedenou schopnost zachytit operace transakce. **CommitFailureHandler** umožňuje automatické obnovení při selhání připojení a zároveň potvrzení transakce.
- **IndexAttribute** umožňuje zadat indexy umístěním atributu vlastnosti (nebo vlastností) ve vašem modelu Code First. Code First pak vytvoří odpovídající index v databázi.
- **Rozhraní API pro veřejné mapování** poskytuje přístup k informacím EF, které se týkají způsobu mapování vlastností a typů na sloupce a tabulky v databázi. V dřívějších verzích bylo toto rozhraní API interní.
- **Možnost konfigurovat zachycení prostřednictvím souboru app/web. config**(umožnění přidání zachycení bez opětovné kompilace aplikace).
- **DatabaseLogger** je nový zachytávací, který usnadňuje protokolování všech operací databáze do souboru. V kombinaci s předchozí funkcí vám to umožňuje snadno přepnout na protokolování operací databáze pro nasazenou aplikaci, aniž by bylo nutné znovu kompilovat.
- Bylo vylepšeno **zjišťování změn modelů migrace** , aby bylo možné zajistit přesnější a migrační migrace. výkon procesu zjišťování změn byl také výrazně vylepšen.
- **Vylepšení výkonu** , včetně méně databázových operací během inicializace, optimalizace pro porovnání rovnosti null v dotazech LINQ, rychlejší generování zobrazení (vytváření modelů) ve více scénářích a efektivnější materializace sledovaných entit s více přidruženími.

<a id="identity"></a>
### <a name="aspnet-identity-200"></a>ASP.NET Identity 2.0.0

- **Dvojúrovňové ověřování**: ASP.NET identity teď podporuje dvojúrovňové ověřování. Dvojúrovňové ověřování zajišťuje další vrstvu zabezpečení uživatelských účtů v případě ohrožení zabezpečení hesla. K dispozici je také ochrana proti útokům hrubou silou pomocí obou kódů faktoru.
- **Uzamčení účtu:** Poskytuje způsob, jak uživatele uzamknout, pokud uživatel zadá své heslo nebo kódy dvou faktorů nesprávně. Je možné nakonfigurovat počet neplatných pokusů a časový interval pro uživatele uzamčený. Vývojář může volitelně vypnout uzamknutí účtu u určitých uživatelských účtů, aby museli.
- **Potvrzení účtu:** ASP.NET Identity systém teď podporuje potvrzení účtu. Toto je poměrně běžný scénář ve většině webů, kde se při registraci nového účtu na webu vyžaduje, abyste před provedením jakékoli akce na webu potvrdili, že jste si vyžádali e-mail. Potvrzení e-mailu je užitečné, protože brání v vytváření falešných účtů. To je velmi užitečné, pokud používáte e-mail jako metodu komunikace s uživateli vašeho webu, jako jsou například weby fóra, bankovní, elektronického obchodování nebo sociální weby.
- **Resetování hesla:** Resetování hesla je funkce, ve které může uživatel resetovat hesla, pokud si zapomněli heslo.
- **Bezpečnostní razítko (odhlásit všude):** Podporuje způsob, jak znovu vygenerovat token zabezpečení pro uživatele v případech, kdy uživatel změní heslo nebo jakékoli jiné informace související se zabezpečením, jako je například odebrání přidruženého přihlášení (například Facebook, Google, účet Microsoft atd.). To je potřeba, aby se zajistilo zrušení platnosti všech tokenů generovaných se starým heslem. Pokud změníte heslo uživatele v ukázkovém projektu, pro uživatele se vygeneruje nový token a všechny předchozí tokeny se zruší. Tato funkce poskytuje další vrstvu zabezpečení vaší aplikace, protože když změníte heslo, budete se odhlásit z libovolného místa (všech ostatních prohlížečů), ke kterým jste se přihlásili do této aplikace.
- **Nastavit typ primárního klíče pro uživatele a role**: v ASP.NET identity 1,0 se jako primární klíč pro uživatele tabulky a role používaly řetězce. To znamená, že pokud byl systém ASP.NET Identity trval v SQL Server pomocí Entity Framework, používali jsme nvarchar. V rámci této výchozí implementace Stack Overflow a na základě příchozí zpětné vazby bylo k dispozici celá řada diskuzí. Poskytujeme zavěšení rozšiřitelnosti, kde můžete určit, co by mělo být primární klíč tabulky uživatelů a rolí. Tento zavěšení rozšíření je zvlášť užitečné, pokud migrujete aplikaci a aplikace ukládá identifikátory UserIds nebo čísla.
- **Podpora rozhraní IQueryable pro uživatele a role**: Přidání podpory pro IQueryable na UsersStore a RolesStore můžete snadno získat seznam uživatelů a rolí.
- **Podpora operace odstranění prostřednictvím UserManager**
- **Indexování na uživatelské jméno**: v ASP.NET identity Entity Framework implementaci jsme do tohoto uživatelského jména přidali jedinečný index pomocí nového IndexAttributeu v EF 6.1.0. Tím se zajistí, že uživatelská jména jsou vždycky jedinečná a nedošlo ke konfliktu časování, ve kterém by bylo možné ukončit duplicitní uživatelská jména.
- **Vylepšené validátory hesla:** Validátor hesla, který byl dodán v ASP.NET Identity 1,0, byl poměrně základním validátorem hesla, který vyhodnotil jenom minimální délku. Existuje nové validátor hesla, který vám poskytne větší kontrolu nad složitostí hesla. Počítejte s tím, že i když zapnete všechna nastavení v tomto hesle, doporučujeme vám, abyste pro uživatelské účty povolili dvojúrovňové ověřování.
- **Middleware IdentityFactory/CreatePerOwinContext**:

    - **Správce uživatelů**: implementaci továrny můžete použít k získání instance UserManager z kontextu Owin. Tento model se podobá tomu, co používáme pro získání správce AuthenticationManager z kontextu OWIN pro přihlášení a odhlášení. Toto je doporučený způsob získání instance UserManager na žádost pro aplikaci.
    - **DbContextFactory**: ASP.NET Identity používá Entity Framework pro zachování systému Identity v SQL Server. K tomu má systém identit odkaz na ApplicationDbContext. Middleware DbContextFactory vrací instanci ApplicationDbContext na žádost, kterou můžete použít ve vaší aplikaci.
- **Balíček NuGet pro ASP.NET identity Samples**: balíček NuGet Samples může usnadnit instalaci a spuštění ukázek pro ASP.NET identity a postupovat podle osvědčených postupů. Toto je ukázková aplikace ASP.NET MVC. Před nasazením tohoto kódu v produkčním prostředí prosím upravte kód tak, aby odpovídal vaší aplikaci. Ukázková aplikace by měla být nainstalovaná v prázdné aplikaci ASP.NET. Další informace o balíčku najdete v tomto blogovém příspěvku: [oznamujeme RTM ASP.NET identity 2.0.0](https://blogs.msdn.com/b/webdev/archive/2014/03/20/test-announcing-rtm-of-asp-net-identity-2-0-0.aspx)

<a id="owin"></a>
### <a name="microsoft-owin-components"></a>Komponenty Microsoft OWIN

V této verzi se opravily spousta chyb. Podrobnější informace najdete v [poznámkách k verzi pro verzi 2.1.0](https://katanaproject.codeplex.com/releases/view/113281) .

<a id="signalr"></a>
### <a name="aspnet-signalr-202"></a>2\.0.2 signálu ASP.NET

V této verzi se opravily spousta chyb. Podrobnější informace najdete v [poznámkách k verzi pro verzi 2.0.2](https://github.com/SignalR/SignalR/releases/tag/2.0.2) .

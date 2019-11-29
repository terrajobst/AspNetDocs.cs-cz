---
uid: mvc/mvc3
title: ASP.NET MVC 3
author: rick-anderson
description: (zahrnuje aktualizace nástrojů z dubna 2011) ASP.NET MVC 3 je architektura pro vytváření škálovatelných webových aplikací založených na standardech pomocí dobře zavedeného vzoru návrhu...
ms.author: riande
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 421a06c89d4dbcb05d4080033813cc6558b7c698
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74586753"
---
# <a name="aspnet-mvc-3"></a>ASP.NET MVC 3

> *(zahrnuje aktualizace nástrojů z dubna 2011)*
> 
> ASP.NET MVC 3 je architektura pro vytváření škálovatelných webových aplikací založených na standardech pomocí dobře zavedených vzorů návrhu a síly ASP.NET a .NET Framework.
> 
> Instaluje se vedle sebe s ASP.NET MVC 2, takže ji můžete začít používat ještě dnes!
> 
> Stáhněte si [instalační program sem](https://go.microsoft.com/fwlink/?LinkID=208140)

## <a name="top-features"></a>Hlavní funkce

- Integrovaný systém generování uživatelského rozhraní rozšiřitelný přes NuGet
- Šablony projektů s podporou formátu HTML 5
- Přehledná zobrazení včetně nového modulu zobrazení Razor
- Výkonné háky se vkládáním závislostí a globálními filtry akcí
- Bohatá podpora JavaScriptu s nenápadem jazyka JavaScript, ověřování jQuery a vazeb JSON
- *Přečtěte si seznam úplných funkcí [níže](#overview) .*

## <a name="top-links"></a>Hlavní odkazy

Co je nového v ASP.NET MVC 3

- Filip Haack: [vydaná ASP.NET MVC 3](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)
- Scott Hanselman: [ASP.NET MvC3, WebMatrix, NuGet, IIS Express a ovocné vydání – Webová verze od Microsoftu v kontextu](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)
- Scott Guthrie: [oznamuje vydání sady ASP.NET MVC 3, IIS Express, SQL CE 4, web farme Framework, sadu, WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)
- [Poznámky k verzi pro ASP.NET MVC 3](../whitepapers/mvc3-release-notes.md)

Instalace a pomáhat

- Instalace ASP.NET MVC 3 pomocí [instalačního programu webové platformy (doporučeno)](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)
- Instalace ASP.NET MVC 3 pomocí [spustitelného souboru instalačního programu](https://go.microsoft.com/fwlink/?LinkID=208140)
- Instalace [ASP.NET MVC 3 pro Visual Studio 11 Developer Preview](https://go.microsoft.com/fwlink/?LinkID=208140)
- Přečtěte si [kurz Úvod do ASP.NET MVC 3](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)
- Získat nápovědu a diskutovat ASP.NET MVC 3 ve [fórech](https://forums.asp.net/1146.aspx)

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a>ASP.NET MVC 3 – Přehled

ASP.NET MVC 3 staví na ASP.NET MVC 1 a 2 a přidává skvělé funkce, které zjednodušují váš kód a umožňují hlubší rozšiřitelnost. V tomto tématu najdete přehled mnoha nových funkcí, které jsou součástí této verze, a jsou uspořádány do následujících částí:

- [Rozšiřitelné generování uživatelského rozhraní s integrací MvcScaffold](#BM_MvcScaffolding)
- [Šablony projektů s podporou formátu HTML 5](#BM_HTML5)
- [Modul zobrazení Razor](#BM_TheRazorViewEngine)
- [Podpora pro více modulů zobrazení](#BM_Support_for_Multiple_View_Engines)
- [Vylepšení kontroléru](#BM_Controller_Improvements)
- [JavaScript a AJAX](#BM_JavaScript_and_Ajax_Improvements)
- [Vylepšení ověřování modelu](#BM_Model_Validation_Improvements)
- [Vylepšení vkládání závislostí](#BM_Dependency_Injection_Improvements)
- [Další nové funkce](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a>Rozšiřitelné generování uživatelského rozhraní s integrací MvcScaffold

Nový systém vytváření uživatelského rozhraní usnadňuje výběr a zahájení používání produktu, pokud jste zcela nové rozhraní a automatizaci běžných úloh vývoje, pokud máte zkušenosti a už víte, co děláte.

To je podporováno novým balíčkem pro *generování uživatelského rozhraní* NuGet s názvem **MvcScaffolding**. Pojem "generování uživatelského rozhraní používá mnoho softwarových technologií, což znamená" rychlé generování základního přehledu o softwaru, který pak můžete upravit a přizpůsobit. " Balíček pro generování uživatelského rozhraní, který vytváříme pro ASP.NET MVC, je výrazně přínosný v několika scénářích:

- **Pokud se naučíte ASP.NET MVC poprvé**, protože vám poskytne rychlý způsob, jak získat nějaký užitečný, funkční kód, který pak můžete upravit a přizpůsobit podle svých potřeb. Ušetří vám trauma, že se díváte na prázdnou stránku a nemá žádný nápad na to, kde začít!
- **Pokud znáte ASP.NET MVC dobře a teď prozkoumáte novou technologii doplňku** , jako je například objektově-relační Mapovač, modul zobrazení, knihovnu testování atd., protože Tvůrce této technologie také mohl vytvořit pro něj balíček pro generování uživatelského rozhraní.
- **Pokud vaše práce zahrnuje opakované vytváření podobných tříd nebo souborů nějakého řazení**, protože můžete vytvořit vlastní generátory výstupu výstupních přípravek, skripty pro nasazení nebo cokoli jiného, co potřebujete. Všichni členové týmu mohou používat i vlastní lešení.

Mezi další funkce v MvcScaffolding patří:

- Podpora projektů C# a projektů VB
- Podpora pro zobrazovací moduly Razor a ASPX
- Podporuje generování uživatelského rozhraní do oblastí MVC ASP.NET a použití vlastních rozložení/hlavních zobrazení.
- Výstup můžete snadno přizpůsobit úpravou šablon T4.
- Pomocí vlastní logiky PowerShellu a vlastních šablon T4 můžete přidat zcela nové uživatelské rozhraní. Tyto (a všechny vlastní parametry, které jste jim dali), se automaticky zobrazí v seznamu pro doplňování na kartě konzoly.
- Balíčky NuGet, které obsahují další generátory, můžete získat pro různé technologie (například pro LINQ to SQL nyní existuje zkušební verze jednoho) a vzájemně je kombinovat a porovnávat s nimi.

Aktualizace nástrojů ASP.NET MVC 3 obsahuje skvělou podporu sady Visual Studio pro tento systém generování uživatelského rozhraní, jako je například:

- Dialog Přidat řadič teď podporuje úplné automatické generování uživatelského rozhraní pro vytváření, čtení, aktualizaci a odstraňování akcí kontroleru a odpovídajících zobrazení. Ve výchozím nastavení tato rozhraní pro přístup k datům pomocí kódu EF Code First.
- Dialog Přidat řadič podporuje *rozšiřitelné generování uživatelského rozhraní* prostřednictvím balíčků NuGet, jako je *MvcScaffolding*. To umožňuje zapojení do vlastního uživatelského rozhraní do dialogového okna, které vám umožní vytvářet pro ostatní technologie pro přístup k datům, jako je NHibernate nebo i JET, ODBCDirect v případě, že jste to zaznamenali.

Další informace o generování uživatelského rozhraní v ASP.NET MVC 3 najdete v následujících zdrojích informací:

- Steveský seriál Sanderson, včetně: 

    1. [Úvod: generování uživatelského rozhraní projektu MVC 3 v ASP.NET pomocí balíčku MvcScaffolding](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [Standardní použití: typické případy použití a možnosti](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [Relace 1: n](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [Akce generování uživatelského rozhraní a testy jednotek](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [Přepsání šablon T4](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [Tento příspěvek: vytváření vlastních lešení](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- Příspěvek Scott Hanselman ze své relace PDC 2010 [Vytvoření blogu s pojmenovaným balíčkem webové](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx) aplikace
- [Poznámky k verzi MVC 3](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a>Šablony projektů HTML 5

Dialogové okno Nový projekt obsahuje zaškrtávací políčko Povolit verze HTML 5 šablon projektů. Tyto šablony využívají modernizr 1,7 k zajištění podpory kompatibility HTML 5 a CSS 3 v prohlížečích nižší úrovně.

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a>Modul zobrazení Razor

ASP.NET MVC 3 přináší nový zobrazovací modul s názvem Razor, který nabízí následující výhody:

- Syntaxe Razor je čistý a stručný a vyžaduje minimální počet klávesových úhozů.
- Razor se snadno učí, protože je založena na stávajících jazycích, jako C# je a Visual Basic.
- Visual Studio zahrnuje technologii IntelliSense a barvu kódu pro syntaxe Razor.
- Zobrazení Razor lze testovat jednotkou bez nutnosti spustit aplikaci nebo spustit webový server.

Mezi nové funkce Razor patří následující:

- `@model` syntaxe pro určení typu, který se předává do zobrazení.
- syntaxe komentáře `@* *@`.
- Možnost zadat výchozí hodnoty (například `layoutpage`) jednou pro celou lokalitu.
- Metoda `Html.Raw` pro zobrazení textu bez kódování HTML
- Podpora pro sdílení kódu mezi více zobrazeními ( *\_souborů viewstart. cshtml* nebo *\_viewstart. vbhtml* ).

Razor obsahuje také nové pomocníky HTML, například následující:

- `Chart`. Vykreslí graf a nabídne stejné funkce jako ovládací prvek grafu v ASP.NET 4.
- `WebGrid`. Vykreslí datovou mřížku a doplní funkce stránkování a řazení.
- `Crypto`. Používá algoritmy hash k vytváření správně nasolených a zatřiďovacích hesel.
- `WebImage`. Vykreslí obrázek.
- `WebMail`. Pošle e-mailovou zprávu.

Další informace o Razor najdete v následujících zdrojích informací:

- [Příspěvek na blogu Scottu Guthrie, představení Razor](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [Blogový příspěvek Scott Guthrie, který zavádí klíčové slovo @model](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [Příspěvek na blogu pro Scott Guthrie představení Razor Layouts](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [Stručný přehled rozhraní API Razor](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [Poznámky k verzi MVC 3](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a>Podpora pro více modulů zobrazení

Dialogové okno **Přidat zobrazení** v ASP.NET MVC 3 vám umožňuje vybrat modul zobrazení, se kterým chcete pracovat, a dialogové okno **Nový projekt** vám umožní určit výchozí modul zobrazení pro projekt. Můžete zvolit modul webové formuláře zobrazení (ASPX), Razor nebo open source zobrazení, jako je [Spark](http://sparkviewengine.com/), [NHaml](https://code.google.com/p/nhaml/)nebo [NDjango](http://ndjango.org/).

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a>Vylepšení kontroléru

### <a name="global-action-filters"></a>Filtry globálních akcí

Někdy je vhodné provést logiku buď před spuštěním metody akce, nebo po spuštění metody akce. Pro podporu tohoto ASP.NET MVC 2 poskytla filtry akcí. Filtry akcí jsou vlastní atributy, které poskytují deklarativní způsob pro přidání chování před akcí a po akci na konkrétní metody akce kontroleru. V některých případech však můžete chtít určit chování před akcemi nebo po akci, které se vztahuje na všechny metody akcí. MVC 3 vám umožňuje zadat globální filtry jejich přidáním do kolekce `GlobalFilters`. Další informace o globálních filtrech akcí najdete v následujících zdrojích informací:

- [Blog Scottu Guthrie na MVC 3 Preview](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- [Filtrování v ASP.NET MVC](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)

### <a name="new-viewbag-property"></a>Nová vlastnost "ViewBag"

Řadiče MVC 2 podporují vlastnost `ViewData`, která umožňuje předat data do šablony zobrazení pomocí rozhraní API slovníku s pozdní vazbou. V MVC 3 můžete k dosažení stejného účelu použít také poněkud jednodušší syntaxi s vlastností `ViewBag`. Například namísto psaní `ViewData["Message"]="text"`můžete napsat `ViewBag.Message="text"`. Nemusíte definovat žádné třídy silného typu pro použití vlastnosti `ViewBag`. Vzhledem k tomu, že se jedná o dynamickou vlastnost, můžete místo toho získat nebo nastavit vlastnosti a dynamicky je vyřešit v době běhu. Interně se `ViewBag` vlastnosti ukládají jako páry název/hodnota ve slovníku `ViewData`. (Poznámka: ve většině předběžných verzí sady MVC 3 byla vlastnost `ViewBag` pojmenována jako vlastnost `ViewModel`.)

### <a name="new-actionresult-types"></a>Nové typy "ActionResult"

Následující typy `ActionResult` a odpovídající pomocné metody jsou v MVC 3 nové nebo rozšířené:

- [HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx). Vrátí klientovi stavový kód HTTP 404.
- [RedirectResult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx). Vrátí dočasné přesměrování (Stavový kód HTTP 302) nebo trvalé přesměrování (Stavový kód HTTP 301) v závislosti na logickém parametru. Ve spojení s touto změnou má třída [Controller](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx) nyní tři metody pro provádění trvalých přesměrování: `RedirectPermanent`, `RedirectToRoutePermanent`a `RedirectToActionPermanent`. Tyto metody vracejí instanci `RedirectResult` s vlastností `Permanent` nastavenou na `true`.
- [HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx). Vrátí stavový kód HTTP zadaný uživatelem.

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a>Vylepšení jazyka JavaScript a AJAX

Ve výchozím nastavení se pomocníkům AJAX a ověřování v MVC 3 používají nenápadný přístup k JavaScriptu. Nenápadní JavaScript zabraňuje vložení vloženého JavaScriptu do HTML. Díky tomu je váš kód HTML menší a méně zbytečný a zjednoduší se tak vyměňované nebo přizpůsobení knihoven JavaScriptu. Ověřovací pomocníky v MVC 3 používají ve výchozím nastavení také modul plug-in `jQueryValidate`. Pokud chcete chování MVC 2, můžete zakázat nenápadný JavaScript pomocí nastavení souboru *Web. config* . Další informace o vylepšeních JavaScriptu a AJAX najdete v následujících zdrojích informací:

- [Základní Úvod k nenápadu JavaScriptu na webu Wikipedii](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [Brad Wilson nenápadový příspěvek JavaScriptu](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [Brad Wilson zveřejní příspěvek na ověřování JavaScriptu.](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- [Vytvoření aplikace MVC 3 se syntaxí Razor a nenápadem JavaScriptu](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md) (kurz na webu ASP.NET)
- [Poznámky k verzi MVC 3](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a>Ověřování na straně klienta je ve výchozím nastavení povoleno.

V dřívějších verzích MVC je nutné explicitně volat `Html.EnableClientValidation` metodu ze zobrazení, aby bylo možné povolit ověřování na straně klienta. V MVC 3 to již není nutné, protože ověřování na straně klienta je ve výchozím nastavení povoleno. (Toto můžete zakázat pomocí nastavení v souboru *Web. config* .)

Aby ověřování na straně klienta fungovalo, stále musíte odkazovat na příslušné knihovny pro ověřování jQuery a jQuery ve vaší lokalitě. Tyto knihovny můžete hostovat na svém vlastním serveru nebo je odkazovat ze sítě Content Delivery Network (CDN), jako je sítě CDN od Microsoftu nebo Google.

### <a name="remote-validator"></a>Vzdálený validátor

ASP.NET MVC 3 podporuje novou třídu [RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx) , která umožňuje využít podporu vzdáleného validátoru pro ověření jQuery v modulu plug-in. To umožňuje knihovně ověřování na straně klienta automaticky volat vlastní metodu, která je definována na serveru, aby bylo možné provést ověřovací logiku, která může být provedena pouze na straně serveru.

V následujícím příkladu atribut `Remote` určuje, že ověřování klienta volá akci nazvanou `UserNameAvailable` ve třídě `UsersController`, aby bylo možné ověřit pole `UserName`.

[!code-csharp[Main](mvc3/samples/sample1.cs)]

Následující příklad ukazuje odpovídající kontroler.

[!code-csharp[Main](mvc3/samples/sample2.cs)]

Další informace o použití atributu `Remote` naleznete v tématu [How to: Implement Remote ověřování in ASP.NET MVC](https://msdn.microsoft.com/library/gg508808(VS.98).aspx) v knihovně MSDN.

### <a name="json-binding-support"></a>Podpora vazeb JSON

ASP.NET MVC 3 obsahuje integrovanou podporu vazeb JSON, která umožňuje metodám akcí přijímat data s kódováním JSON a model – svázat je s parametry Action-Method. Tato funkce je užitečná ve scénářích, které zahrnují šablony klientů a datové vazby. (Šablony klientů umožňují formátovat a zobrazovat jednu datovou položku nebo sadu datových položek pomocí šablon, které se spouštějí na klientovi.) MVC 3 vám umožňuje snadno propojit šablony klientů s metodami akce na serveru, který odesílá a přijímá data JSON. Další informace o podpoře vazeb JSON najdete v části **vylepšení pro JavaScript a AJAX** v [příspěvku na blogu pro Scott GUTHRIE ve verzi MVC 3](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx).

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a>Vylepšení ověřování modelu

### <a name="dataannotations-metadata-attributes"></a>Atributy metadat "DataAnnotations"

ASP.NET MVC 3 podporuje `DataAnnotations` atributy metadat, jako je například `DisplayAttribute`.

### <a name="validationattribute-class"></a>Třída "ValidationAttribute"

`ValidationAttribute` třída byla vylepšena v .NET Framework 4 pro podporu nového přetížení `IsValid`, která poskytuje další informace o aktuálním kontextu ověřování, jako je například ověřování objektu. To umožňuje bohatší scénáře, kde můžete ověřit aktuální hodnotu na základě jiné vlastnosti modelu. Například nový atribut `CompareAttribute` umožňuje porovnat hodnoty dvou vlastností modelu. V následujícím příkladu musí vlastnost `ComparePassword` odpovídat poli `Password`, aby byla platná.

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a>Ověřovací rozhraní

Rozhraní [IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx) umožňuje provádět ověřování na úrovni modelu a umožňuje poskytovat chybové zprávy ověřování, které jsou specifické pro stav celkového modelu, nebo mezi dvěma vlastnostmi v rámci modelu. MVC 3 nyní načítá chyby z rozhraní `IValidatableObject` při vytváření vazby modelu a automaticky označí nebo zvýrazňuje ovlivněná pole v rámci zobrazení pomocí vestavěných pomocníků formulářů HTML.

Rozhraní [IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx) umožňuje ASP.NET MVC zjišťovat v době běhu, zda má validátor podporu pro ověření klienta. Toto rozhraní bylo navrženo tak, aby bylo možné je integrovat s celou řadou ověřovacích architektur.

Další informace o ověřovacích rozhraních naleznete v části **vylepšení ověřování modelů** v [příspěvku na blogu pro Scott GUTHRIE ve verzi MVC 3](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx). (Upozorňujeme však, že odkaz na "IValidateObject" v blogu by měl být "IValidatableObject".)

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a>Vylepšení vkládání závislostí

ASP.NET MVC 3 poskytuje lepší podporu pro použití injektáže závislosti (DI) a pro integraci s vkládáním závislostí nebo kontejnery inverze Control (IOC). Byla přidána podpora pro DI v následujících oblastech:

- Řadiče (registrace a vkládání továrnování kontrolérů, vložení řadičů).
- Zobrazení (registrování a vkládání modulů zobrazení, vkládání závislostí do stránek zobrazení).
- Filtry akcí (hledání a vložení filtrů).
- Pořadače modelů (registrace a vkládání).
- Poskytovatelé ověřování modelu (registrace a vkládání).
- Poskytovatelé metadat modelů (registrace a vkládání).
- Zprostředkovatelé hodnot (registrace a vkládání).

MVC 3 podporuje [společnou knihovnu lokátorů služeb](https://github.com/unitycontainer/commonservicelocator) a jakýkoliv kontejner di, který podporuje `IServiceLocator` rozhraní této knihovny. Podporuje také nové rozhraní `IDependencyResolver`, které usnadňuje integraci DI Frameworku.

Další informace o DI v MVC 3 najdete v následujících zdrojích informací:

- [Řada příspěvků na blogu brada Wilson na místě služby](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [Poznámky k verzi MVC 3](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a>Další nové funkce

### <a name="nuget-integration"></a>Integrace NuGet

ASP.NET MVC 3 automaticky instaluje a povoluje NuGet v rámci své instalace. NuGet je bezplatný Open Source správce balíčků usnadňující hledání, instalaci a používání knihoven a nástrojů .NET v projektech. Funguje se všemi typy projektů aplikace Visual Studio (včetně webových formulářů ASP.NET a ASP.NET MVC).

NuGet umožňuje vývojářům, kteří udržují open source projekty (například projekty, jako je MOQ, NHibernate, Ninject, StructureMap, NUnit, Windsor, RhinoMocks a knihovny elmah), zabalit své knihovny a zaregistrovat je v online galerii. Pro vývojáře v rozhraní .NET je pak snadné použít jednu z těchto knihoven k vyhledání balíčku a jeho instalaci v projektech, na kterých pracují.

V případě aktualizace nástrojů ASP.NET 3 obsahují šablony projektů knihovny JavaScriptu s předem nainstalovanými balíčky NuGet, takže je lze aktualizovat prostřednictvím NuGet. Entity Framework Code First jsou také předem nainstalovány jako balíček NuGet.

Další informace o NuGet najdete v [dokumentaci k NuGet](https://docs.microsoft.com/nuget/).

### <a name="partial-page-output-caching"></a>Ukládání výstupu do mezipaměti částečné stránky

ASP.NET MVC podporuje ukládání výstupu do mezipaměti pro odpovědi na celé stránky od verze 1. MVC 3 také podporuje ukládání výstupů na částečných stránkách, což umožňuje snadno ukládat oblasti nebo fragmenty odpovědi. Další informace o ukládání do mezipaměti najdete v části **ukládání do mezipaměti částečného výstupu stránky** [v příspěvku na blogu GUTHRIE na webu MVC 3 Release Candidate](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) a v části **ukládání výstupu do mezipaměti podřízené akce** v [poznámkách k verzi MVC 3](../whitepapers/mvc3-release-notes.md).

### <a name="granular-control-over-request-validation"></a>Detailní kontrola nad žádostí o ověření

ASP.NET MVC obsahuje integrované ověřování žádostí, které automaticky pomáhá chránit před útoky XSS a HTML injektáže. Někdy však budete chtít explicitně zakázat ověření žádosti, například pokud chcete uživatelům umožnit publikování obsahu HTML (například v položkách blogu nebo obsahu CMS). Nyní můžete přidat atribut [AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx) do modelů nebo zobrazit modely a zakázat ověřování žádostí na základě jednotlivých vlastností při vytváření vazby modelu. Další informace o ověření žádosti najdete v následujících zdrojích informací:

- Část " **nenápadný JavaScript a ověření** " v [příspěvku na blogu GUTHRIE na portálu MVC 3 Release Candidate](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx).
- [Poznámky k verzi MVC 3](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a>Dialogové okno rozšiřitelný nový projekt

V ASP.NET MVC 3 můžete přidat šablony projektů, Zobrazit moduly a projekty pro testování částí do dialogového okna **Nový projekt** .

### <a name="template-scaffolding-improvements"></a>Vylepšení generování šablon

ASP.NET MVC 3 – šablony pro generování uživatelského rozhraní poskytují lepší úlohu pro identifikaci vlastností primárního klíče v modelech a jejich zpracování odpovídajícím způsobem, než v dřívějších verzích MVC. (Například šablony generování uživatelského rozhraní se nyní ujistěte, že primární klíč není vytvořen jako pole formuláře s možností úprav.)

Ve výchozím nastavení se pomocí rutiny pro vytváření a úpravy teď místo pomocníka `Html.TextBoxFor` používá pomocná rutina `Html.EditorFor`. Tato funkce vylepšuje podporu metadat v modelu ve formě atributů anotace dat, když dialogové okno **Přidat zobrazení** vygeneruje zobrazení.

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a>Nová přetížení pro "HTML. LabelFor" a "HTML. LabelForModel"

Byla přidána nová přetížení metod pro `LabelFor` a pomocné metody `LabelForModel`. Nová přetížení umožňují zadat nebo přepsat text popisku.

### <a name="sessionless-controller-support"></a>Podpora řadiče s nerelačními relacemi

V ASP.NET MVC 3 můžete určit, zda chcete, aby třída Controller používala stav relace, a pokud ano, zda má být stav relace určen jen pro čtení/zápis nebo jen pro čtení. Další informace o podpoře řadičů bez relací najdete v [poznámkách k verzi MVC 3](../whitepapers/mvc3-release-notes.md).

### <a name="new-additionalmetadataattribute-class"></a>Nová třída "AdditionalMetadataAttribute"

Atribut [AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx) můžete použít k naplnění `ModelMetadata.AdditionalValues` slovníku pro vlastnost modelu. Například pokud má model zobrazení vlastnost, která by měla být zobrazena pouze pro správce, můžete tuto vlastnost opatřit poznámkami, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](mvc3/samples/sample4.cs)]

Tato metadata jsou zpřístupněna všem zobrazením nebo šablonám editoru při vykreslování modelu zobrazení produktu. Informace o metadatech můžete interpretovat.

### <a name="accountcontroller-improvements"></a>Vylepšení AccountController

AccountController v šabloně internetového projektu byl výrazně vylepšen.

### <a name="new-intranet-project-template"></a>Nová šablona intranetového projektu

K dispozici je nová šablona intranetového projektu, která umožňuje ověřování systému Windows a odebírá AccountController.

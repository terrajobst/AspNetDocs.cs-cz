---
uid: whitepapers/mvc4-release-notes
title: ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: Tento dokument popisuje vydání ASP.NET MVC 4.
ms.author: riande
ms.date: 09/09/2011
ms.assetid: f014524f-25c0-4094-b8e1-886d99536f00
msc.legacyurl: /whitepapers/mvc4-release-notes
msc.type: content
ms.openlocfilehash: b57480bd0274fbb76c600dfb0dd09037bdcbf1e7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563425"
---
# <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

> Tento dokument popisuje vydání ASP.NET MVC 4.

- [Poznámky k instalaci](#_Toc303253802)
- [Dokumentace](#_Toc303253803)
- [Podpora](#_Toc303253804)
- [Požadavky na software](#_Toc303253805)
- [Nové funkce v ASP.NET MVC 4](#_Toc303253807)

    - [Webové rozhraní API v ASP.NET](#_Toc317096197)
    - [Vylepšení výchozích šablon projektů](#_Toc303253808)
    - [Šablona mobilního projektu](#_Toc303253809)
    - [Režimy zobrazení](#_Toc303253810)
    - [jQuery Mobile, přepínač zobrazení a přepsání prohlížeče](#_Toc303253811)
    - [Podpora úloh pro asynchronní řadiče](#_Toc303253813)
    - [Sada Azure SDK](#_Toc303253814)
    - [Migrace databáze](#_Toc303253818)
    - [Prázdná šablona projektu](#_Toc303253819)
    - [Přidat kontroler do libovolné složky projektu](#_Toc303253820)
    - [Vytváření sady a minifikace](#_Toc303253821)
    - [Povolení přihlášení z Facebooku a dalších webů pomocí OAuth a OpenID](#_Toc303253822)
- [Upgrade projektu ASP.NET MVC 3 na ASP.NET MVC 4](#_Toc303253806)
- [Změny z ASP.NET MVC 4 Release Candidate](#_Toc303253817)
- [Známé problémy a zásadní změny](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a>Poznámky k instalaci

ASP.NET MVC 4 pro Visual Studio 2010 se dá nainstalovat z [domovské stránky ASP.NET MVC 4](../mvc/mvc4.md) pomocí instalačního programu webové platformy.

Před instalací ASP.NET MVC 4 doporučujeme odinstalovat všechny dříve nainstalované verze Preview ASP.NET MVC 4. ASP.NET MVC 4 beta a Release Candidate můžete upgradovat na ASP.NET MVC 4 bez odinstalace.

Tato verze není kompatibilní s žádnými verzemi Preview .NET Framework 4,5. Před instalací ASP.NET MVC 4 musíte samostatně upgradovat všechny nainstalované verze Preview .NET Framework 4,5 na konečnou verzi.

ASP.NET MVC 4 se dá nainstalovat a spustit souběžně s ASP.NET MVC 3.

<a id="_Toc303253803"></a>
## <a name="documentation"></a>Dokumentace

Dokumentace k ASP.NET MVC je k dispozici na webu MSDN na následující adrese URL:

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

Kurzy a další informace o ASP.NET MVC jsou k dispozici na stránce MVC 4 na webu ASP.NET ([https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)).

<a id="_Toc303253804"></a>
## <a name="support"></a>Podpora

ASP.NET MVC 4 je plně podporovaná. Pokud máte dotazy týkající se práce s tímto vydáním, můžete je také zveřejnit na fórum ASP.NET MVC ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)), kde členové komunity ASP.NET často mohou zajistit neoficiální podporu.

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a>Požadavky na software

Komponenty ASP.NET MVC 4 pro Visual Studio vyžadují PowerShell 2,0 a Visual Studio 2010 s aktualizací Service Pack 1 nebo Visual Web Developer Express 2010 s aktualizací Service Pack 1.

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4"></a>Nové funkce v ASP.NET MVC 4

Tato část popisuje funkce, které byly představeny ve verzi ASP.NET MVC 4.

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a>Webové rozhraní API ASP.NET

ASP.NET MVC 4 zahrnuje webové rozhraní API ASP.NET, novou architekturu pro vytváření služeb HTTP, které mohou oslovit širokou škálu klientů včetně prohlížečů a mobilních zařízení. Webové rozhraní API ASP.NET je také ideální platformou pro vytváření služeb RESTful.

Webové rozhraní API pro ASP.NET zahrnuje podporu pro následující funkce:

- **Moderní programovací model http:** Přímý přístup a manipulace s požadavky HTTP a odpověďmi ve webových rozhraních API pomocí nového a silně typovaného objektového modelu HTTP. Stejný programovací model a kanál HTTP jsou symetricky k dispozici na klientovi prostřednictvím nového typu *HttpClient* .
- **Úplná podpora pro trasy:** Webové rozhraní API pro ASP.NET podporuje úplnou sadu možností směrování ASP.NET, včetně parametrů a omezení trasy. Kromě toho používejte jednoduché konvence k mapování akcí na metody HTTP.
- **Vyjednávání obsahu:** Klient a server můžou společně spolupracovat, aby určily správný formát dat vrácených z webového rozhraní API. Webové rozhraní API pro ASP.NET poskytuje výchozí podporu formátů kódovaných v jazyce XML, JSON a formátu URL a můžete tuto podporu rozšíření přidat vlastní formátovací moduly nebo dokonce nahradit výchozí strategii vyjednávání obsahu.
- **Vazba modelů a ověřování:** Pořadače modelů poskytují snadný způsob, jak extrahovat data z různých částí požadavku HTTP a převádět tyto části do objektů .NET, které může používat akce webového rozhraní API. Ověřování se provádí taky u parametrů akce na základě datových poznámek.
- **Filtry:** Webové rozhraní API ASP.NET podporuje filtry, včetně známých filtrů, jako je například atribut *[autorizovat]* . Můžete vytvářet a připojovat vlastní filtry pro akce, autorizaci a zpracování výjimek.
- **Složení dotazu:** Použijte atribut filtru *[Queryable]* u akce, která vrací *IQueryable* , aby bylo možné podporovat dotazování webového rozhraní API prostřednictvím konvencí dotazů OData.
- **Vylepšená testování:** Namísto nastavení podrobností HTTP ve statických objektech kontextu akce webového rozhraní API fungují s instancemi *zprávy HttpRequestMessage* a *HttpResponseMessage*. Vytvořte projekt testů jednotek společně s vaším projektem webového rozhraní API, abyste mohli rychle začít psát testy jednotek pro vaše funkce webového rozhraní API.
- **Konfigurace založená na kódu:** Konfigurace webového rozhraní API ASP.NET se provádí výhradně prostřednictvím kódu, takže se soubory Config nechají vyčistit. Pro konfiguraci bodů rozšiřitelnosti použijte poskytnutý vzor lokátoru služby.
- **Vylepšená podpora pro kontejnery inverze správy (IOC):** Webové rozhraní API pro ASP.NET poskytuje skvělou podporu pro kontejnery IoC prostřednictvím vylepšené abstrakce překladače závislostí.
- **Samoobslužný hostitel:** Webová rozhraní API je možné kromě služby IIS hostovat i ve vašem vlastním procesu a přitom pořád využívat úplný výkon tras a dalších funkcí webového rozhraní API.
- **Vytvoření vlastní stránky pro stránku s dalšími stránkami a testování:** Nyní můžete snadno vytvořit vlastní nápovědu a zkušební stránky pro vaše webová rozhraní API pomocí nové služby *IApiExplorer* a získat tak úplný popis prostředí API vaší webové aplikace.
- **Monitorování a diagnostika:** Webové rozhraní API pro ASP.NET teď poskytuje infrastrukturu pro sledování světlé váhy, která usnadňuje integraci s existujícími řešeními protokolování, jako je System. Diagnostics, ETW a rozhraní pro protokolování třetích stran. Trasování můžete povolit tím, že poskytnete implementaci *ITraceWriter* a přidáte ji do konfigurace webového rozhraní API.
- **Vytváření odkazů:** Pomocí webového rozhraní API ASP.NET *UrlHelper* vygenerujte odkazy na související prostředky ve stejné aplikaci.
- **Šablona projektu webového rozhraní API:** Vyberte nový projekt webového rozhraní API. Průvodce projektem MVC 4 vám umožní rychle začít pracovat s webovým rozhraním API ASP.NET.
- **Generování uživatelského rozhraní:** Pomocí dialogového okna **Přidat řadič** můžete rychle vytvořit generátor webových rozhraní API na základě entity Frameworkho typu modelu založeného na.

Další podrobnosti o webovém rozhraní API ASP.NET najdete na [https://www.asp.net/web-api](../web-api/index.md).

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a>Vylepšení výchozích šablon projektů

Šablona, která se používá k vytvoření nových projektů ASP.NET MVC 4, se aktualizovala tak, aby vytvořila moderní web s častým hledáním:

![](mvc4-release-notes/_static/image1.png)

Kromě toho, že je v nové šabloně k dispozici vylepšení kosmetických prostředků, lepší funkce. Tato šablona využívá techniku označovanou jako adaptivní vykreslování, aby vypadala dobře v desktopových prohlížečích i v mobilních prohlížečích bez jakýchkoli úprav.

![](mvc4-release-notes/_static/image2.png)

Chcete-li zobrazit adaptivní vykreslování v akci, můžete použít mobilní emulátor nebo stačí zkusit změnit velikost okna prohlížeče plochy na menší. Dojde-li k zobrazení okna prohlížeče dostatečně malého, změní se rozložení stránky.

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a>Šablona mobilního projektu

Pokud spouštíte nový projekt a chcete vytvořit web speciálně pro mobilní prohlížeče a tablety, můžete použít šablonu projektu nové mobilní aplikace. To je založené na jQuery Mobile, open source knihovně pro sestavování tónově optimalizovaného uživatelského rozhraní:

![](mvc4-release-notes/_static/image3.png)

Tato šablona obsahuje stejnou strukturu aplikace jako šablona internetové aplikace (a kód kontroleru je prakticky identický), ale je ve stylu jQuery Mobile, aby vypadala dobře a pracovala na dotykové mobilní zařízeních. Další informace o způsobu strukturování a stylu mobilního uživatelského rozhraní naleznete na [webu jQuery Mobile Project](http://jquerymobile.com/).

Pokud již máte web orientovaný na plochu, do kterého chcete přidat zobrazení optimalizovaná pro mobilní zařízení, nebo pokud chcete vytvořit jednu lokalitu, která bude pro stolní a mobilní prohlížeče používat jiná zobrazení s různými styly, můžete použít novou funkci zobrazení režimů. (Další informace najdete v další části.)

<a id="_Toc303253810"></a>
### <a name="display-modes"></a>Režimy zobrazení

Funkce nové režimy zobrazení umožňuje aplikaci vybrat zobrazení v závislosti na prohlížeči, který požadavek odeslal. Pokud například prohlížeč stolních počítačů požaduje domovskou stránku, může aplikace použít šablonu Views\Home\Index.cshtml. Pokud mobilní prohlížeč požaduje domovskou stránku, může aplikace vrátit šablonu Views\Home\Index.mobile.cshtml.

Rozložení a částečné typy lze také přepsat pro konkrétní typy prohlížečů. Příklad:

- Pokud vaše složka Views\Shared obsahuje rozvržení \_layout. cshtml a \_layout. Mobile. cshtml, ve výchozím nastavení bude aplikace používat \_layout. Mobile. cshtml během požadavků z mobilních prohlížečů a \_layout. cshtml během ostatních požadavků.
- Pokud složka obsahuje \_MyPartial. cshtml a \_MyPartial. Mobile. cshtml, instrukce @Html.Partial("\_MyPartial") bude vykreslovat \_MyPartial. Mobile. cshtml během požadavků z mobilních prohlížečů a \_MyPartial. cshtml během ostatních požadavků.

Pokud chcete vytvořit konkrétnější zobrazení, rozložení nebo částečná zobrazení pro jiná zařízení, můžete zaregistrovat novou instanci *DefaultDisplayMode* a určit, který název se má vyhledat, když požadavek splní určité podmínky. Do souboru Global. asax můžete například přidat následující *\_* kód, který zaregistruje řetězec "iPhone" jako režim zobrazení, který se použije, když prohlížeč Apple iPhone vytvoří požadavek:

[!code-csharp[Main](mvc4-release-notes/samples/sample1.cs)]

Po spuštění tohoto kódu, když se v prohlížeči Apple iPhone vytvoří žádost, bude vaše aplikace používat Views\Shared\\_Layout. iPhone. cshtml rozložení (pokud existuje). Další informace o režimu zobrazení naleznete v tématu [ASP.NET MVC 4 Mobile Features](../mvc/overview/older-versions/aspnet-mvc-4-mobile-features.md). Aplikace používající DisplayModeProvider by měly nainstalovat [pevný balíček NuGet DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) . [Aktualizace ASP.NET Update 2012](https://go.microsoft.com/fwlink/?LinkID=271322) obsahuje pevný balíček NuGet [DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) v nových šablonách projektů. Podrobnosti o opravě najdete v tématu [ASP.NET pro mobilní ukládání do mezipaměti služby MVC 4 opravené chyby](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) .

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-and-mobile-features"></a>Funkce a mobilní zařízení jQuery

Informace o vytváření mobilních aplikací pomocí ASP.NET MVC 4 pomocí jQuery Mobile najdete v kurzu ASP.NET – [mobilní funkce MVC 4](../mvc/overview/older-versions/aspnet-mvc-4-mobile-features.md).

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a>Podpora úloh pro asynchronní řadiče

Nyní můžete napsat asynchronní metody akcí jako jediné metody, které vracejí objekt typu *Task* nebo *task&lt;ActionResult&gt;* .

 Další informace najdete v tématu [Použití asynchronních metod v ASP.NET MVC 4](../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a>Azure SDK

ASP.NET MVC 4 podporuje 1,6 a novější verze sady Windows Azure SDK.

<a id="_Toc303253818"></a>
### <a name="database-migrations"></a>Migrace databáze

Projekty MVC 4 ASP.NET nyní zahrnují Entity Framework 5. Jednou z skvělých funkcí v Entity Framework 5 je podpora pro migrace databáze. Tato funkce umožňuje snadno vyvíjet schéma databáze pomocí migrace zaměřené na kód při zachování dat v databázi. Další informace o migraci databáze najdete v tématu [Přidání nového pole do modelu a tabulky filmů](../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table.md) v [kurzu Úvod do ASP.NET MVC 4](../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md).

<a id="_Toc303253819"></a>
### <a name="empty-project-template"></a>Prázdná šablona projektu

Prázdná šablona projektu MVC je teď skutečně prázdná, takže můžete začít z zcela čistého SLAT. Předchozí verze prázdné šablony projektu byla přejmenována na Basic.

<a id="_Toc303253820"></a>
### <a name="add-controller-to-any-project-folder"></a>Přidat kontroler do libovolné složky projektu

Nyní můžete kliknout pravým tlačítkem a vybrat **Přidat kontroler** z libovolné složky v projektu MVC. Díky tomu máte větší flexibilitu při organizování vašich řadičů, a to včetně udržování řadičů MVC a webových rozhraní API v samostatných složkách.

<a id="_Toc303253821"></a>
### <a name="bundling-and-minification"></a>Sdružování a minifikace

Rozhraní sdružování a minifikace vám umožňuje snížit počet požadavků HTTP, které webová stránka potřebuje k tomu, aby bylo možné provést kombinování jednotlivých souborů do jediného souboru seskupeného pro skripty a šablony stylů CSS. Pak může snížit celkovou velikost těchto požadavků tím, že minifikace obsah sady. Minifikace může zahrnovat aktivity, jako je odstranění prázdných znaků, pro zkrácení názvů proměnných, dokonce i sbalení selektorů CSS na základě jejich sémantiky. Sady jsou deklarovány a nakonfigurovány v kódu a jsou snadno odkazovány v zobrazeních prostřednictvím pomocných metod, které mohou generovat buď jediné propojení na sadu, nebo při ladění více odkazů na jednotlivé obsahy sady. Další informace najdete v tématu [sdružování a minifikace](../mvc/overview/performance/bundling-and-minification.md).

<a id="_Toc303253822"></a>
### <a name="enabling-logins-from-facebook-and-other-sites-using-oauth-and-openid"></a>Povolení přihlášení z Facebooku a dalších webů pomocí OAuth a OpenID

Výchozí šablony v ASP.NET MVC 4 šablona internetových projektů teď zahrnují podporu přihlášení OAuth a OpenID pomocí knihovny DotNetOpenAuth. Informace o konfiguraci poskytovatele OAuth nebo OpenID najdete v tématu [Podpora protokolu OAuth/OpenID pro webové formuláře, MVC a webové stránky](https://blogs.msdn.com/b/webdev/archive/2012/08/15/oauth-openid-support-for-webforms-mvc-and-webpages.aspx) a dokumentaci k [funkcím OAuth a OpenID ve webových stránkách ASP.NET](../web-pages/overview/releases/top-features-in-web-pages-2.md#oauthsetup).

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a>Upgrade projektu ASP.NET MVC 3 na ASP.NET MVC 4

ASP.NET MVC 4 se dá nainstalovat souběžně s ASP.NET MVC 3 ve stejném počítači, což vám umožní pružně vybrat, kdy se má upgradovat aplikace ASP.NET MVC 3 na ASP.NET MVC 4.

Nejjednodušší způsob, jak upgradovat, je vytvoření nového projektu ASP.NET MVC 4 a zkopírování všech zobrazení, řadičů, kódu a souborů obsahu z existujícího projektu MVC 3 do nového projektu a následné aktualizace odkazů na sestavení v novém projektu tak, aby odpovídaly žádné šabloně mimo MVC v cluded assembiles, kterou používáte. Pokud jste provedli změny v souboru Web. config v projektu MVC 3, musíte tyto změny také sloučit do souboru Web. config v projektu MVC 4.

Pokud chcete ručně upgradovat existující aplikaci ASP.NET MVC 3 na verzi 4, udělejte toto:

1. V všech souborech Web. config v projektu (v kořenu projektu existuje jedna z nich, jedna ve složce views a jedna ve složce zobrazení pro každou oblast v projektu), nahraďte všechny výskyty následujícího textu (Poznámka: System. Web. webpages, Version = 1.0.0.0 nebyl nalezen v projekty vytvořené pomocí sady Visual Studio 2012): 

    [!code-console[Main](mvc4-release-notes/samples/sample2.cmd)]

    s následujícím odpovídajícím textem:

    [!code-console[Main](mvc4-release-notes/samples/sample3.cmd)]
2. V kořenovém souboru Web. config aktualizujte element *webpages: Version* na "2.0.0.0" a přidejte nový klíč *PreserveLoginUrl* , který má hodnotu "true": 

    [!code-xml[Main](mvc4-release-notes/samples/sample4.xml)]
3. V Průzkumník řešení klikněte pravým tlačítkem na odkazy a vyberte Spravovat balíčky NuGet. V levém podokně vyberte **Online\NuGet oficiální zdroj balíčku**a pak aktualizujte následující:

    - ASP.NET MVC 4
    - (Volitelné) jQuery, ověřování jQuery a uživatelské rozhraní jQuery
    - Volitelné Entity Framework
    - (Optonal) Modernizr
4. V Průzkumník řešení klikněte pravým tlačítkem myši na název projektu a pak vyberte Uvolnit projekt. Pak znovu klikněte pravým tlačítkem na název a vyberte upravit *ProjectName*. csproj.
5. Vyhledejte element *ProjectTypeGuids* a nahraďte {E53F8FEA-EAE0-44A6-8774-FFD645390401} řetězcem {E3E379DF-F4C6-4180-9B81-6769533ABE47}.
6. Uložte změny, zavřete soubor projektu (. csproj), který jste upravovali, klikněte pravým tlačítkem myši na projekt a pak vyberte znovu načíst projekt.
7. Pokud projekt odkazuje na jakékoli knihovny třetích stran, které jsou kompilovány pomocí předchozích verzí ASP.NET MVC, otevřete kořenový soubor Web. config a přidejte následující tři prvky *bindingRedirect* do oddílu *Konfigurace* : 

    [!code-xml[Main](mvc4-release-notes/samples/sample5.xml)]

<a id="_Toc303253817"></a>
## <a name="changes-from-aspnet-mvc-4-release-candidate"></a>Změny z ASP.NET MVC 4 Release Candidate

Poznámky k verzi pro ASP.NET MVC 4 Release Candidate najdete tady:

Hlavní změny z ASP.NET MVC 4 Release Candidate v této verzi jsou shrnuté níže:

- **Podle konfigurace řadiče:** Řadiče webového rozhraní API ASP.NET se dají přidružit pomocí vlastního atributu, který implementuje *IControllerConfiguration* pro nastavení vlastních formátovacích funkcí, selektor akcí a vazeb parametrů. *HttpControllerConfigurationAttribute* se odebral.
- **Obslužné rutiny zpráv na trase:** Nyní můžete zadat koncovou obslužnou rutinu zprávy v řetězci požadavku pro danou trasu. Díky tomu může podpora pro jízdní prostředí používat směrování k odeslání do jejich vlastních koncových bodů (mimo*IHttpController*).
- **Oznámení o průběhu:** *ProgressMessageHandler* vygeneruje oznámení o průběhu obou odesílaných entit požadavků a stahovaných entit odpovědí. Pomocí této obslužné rutiny je možné sledovat, jak daleko odesíláte text žádosti nebo stáhnout tělo odpovědi.
- **Nabízený obsah:** Třída *PushStreamContent* umožňuje scénářům, kdy datový producent chce zapisovat přímo do žádosti nebo odpovědi (buď synchronně nebo asynchronně) pomocí datového proudu. Když je *PushStreamContent* připravený přijímat data, která volá delegát akce s výstupním datovým proudem. Vývojář pak může zapsat do datového proudu tak dlouho, jak je potřeba, a po dokončení zápisu tento datový proud zavřít. *PushStreamContent* detekuje ukončení datového proudu a dokončuje základní asynchronní *úlohu* pro vypsání obsahu.
- **Vytváření odpovědí na chyby:** Typ *HttpError* použijte k trvalému vyjádření informací o chybě z, jako jsou chyby ověřování a výjimky, a přitom stále dodržuje *IncludeErrorDetailPolicy*. Nové metody rozšíření *CreateErrorResponse* můžete použít k snadnému vytváření odpovědí na chyby s *HttpError* jako obsahem. Obsah *HttpError* je vyjednáno plněný obsah.
- **MediaRangeMapping odebrané:** Rozsahy typů médií teď zpracovává výchozí Negociační obsahu.
- **Výchozí vazba parametrů pro parametry jednoduchého typu je nyní [FromUri]:** V předchozích verzích webového rozhraní API ASP.NET bylo výchozí vazba parametrů pro parametry jednoduchého typu použité pro vazbu modelu. Výchozí vazba parametru pro parametry jednoduchého typu je nyní *[FromUri]* .
- **Výběr akce respektuje požadované parametry:** Výběr akce ve webovém rozhraní API ASP.NET nyní vybere akci pouze v případě, že jsou k dispozici všechny požadované parametry, které pocházejí z identifikátoru URI. Parametr může být zadán jako nepovinný zadáním výchozí hodnoty pro argument v signatuře metody Action.
- **Přizpůsobení vazeb parametrů http:** Použijte *ParameterBindingAttribute* k přizpůsobení vazby parametru pro konkrétní parametr akce nebo použijte *ParameterBindingRules* na *HttpConfiguration* k přizpůsobení vazeb parametrů v podstatě.
- **Vylepšení MediaTypeFormatter:** Formátovací moduly teď mají přístup k úplné instanci *HttpContent* .
- **Výběr zásad ukládání do vyrovnávací paměti hostitele:** Implementací a konfigurací služby *IHostBufferPolicySelector* ve webovém rozhraní API ASP.NET umožníte hostitelům určit zásadu pro použití ukládání do vyrovnávací paměti.
- **Přístup k klientským certifikátům nezávislá způsobem hostitele:** Použijte metodu rozšíření *GetClientCertificate* k získání poskytnutého klientského certifikátu ze zprávy požadavku.
- **Rozšiřitelnost vyjednávání obsahu:** Přizpůsobte vyjednávání obsahu odvozením z *DefaultContentNegotiator* a přepsáním veškerého aspektu vyjednávání obsahu, které byste chtěli.
- **Podpora pro vracení 406 nepřijatelných odpovědí:** V ASP.NET webovém rozhraní API teď můžete 406 vracet nepřijatelné odpovědi, pokud se nenalezne vhodný formátovací modul vytvořením *DefaultContentNegotiator* s parametrem *excludeMatchOnTypeOnly* nastaveným na *hodnotu true*.
- **Číst data formuláře jako kolekce NameValueCollection nebo JToken:** Data formuláře můžete číst v řetězci dotazu identifikátoru URI nebo v textu požadavku jako *kolekce NameValueCollection* pomocí metod rozšíření *ParseQueryString* a *ReadAsFormDataAsync* v uvedeném pořadí. Podobně můžete číst data formuláře v řetězci dotazu identifikátoru URI nebo v textu požadavku jako *JToken* pomocí metod rozšíření *TryReadQueryAsJson* a *ReadAsAsync*&lt;t&gt; v uvedeném pořadí.
- **Vylepšení s více částmi:** Nyní je možné napsat *MultipartStreamProvider* , který je zcela přizpůsobený typu dat MIME, které může číst, a prezentovat výsledek optimálním způsobem pro uživatele. Krok po zpracování můžete také připojit na *MultipartStreamProvider* , který umožňuje, aby implementace provedená podle toho, jak se bude účtovat, v částech těla MIME. Například implementace *MultipartFormDataStreamProvider* přečte části dat formuláře HTML a přidá je do *kolekce NameValueCollection* , aby bylo možné je snadno získat od volajícího.
- **Vylepšení vytváření odkazů:** *UrlHelper* už nezávisí na *HttpControllerContext*. Teď můžete přistupovat k *UrlHelper* z libovolného kontextu, ve kterém je *zprávy HttpRequestMessage* k dispozici.
- **Změna pořadí provádění obslužné rutiny zpráv:** Obslužné rutiny zpráv se teď spouštějí v pořadí, v jakém jsou nakonfigurované místo v opačném pořadí.
- **Pomocný modul pro zapojení obslužných rutin zpráv:** Nový *HttpClientFactory* , který může napravit *DelegatingHandlers* a vytvořit *HttpClient* s požadovaným kanálem připraveným k přechodu. Poskytuje také funkce pro zapojení do alternativních vnitřních obslužných rutin (výchozí hodnota je *HttpClientHandler*) a také při použití *HttpMessageInvoker* nebo jiné *DelegatingHandler* namísto *HttpClient* jako top-původce.
- **Podpora sítě CDN ve webové optimalizaci ASP.NET:** ASP.NET Web Optimization teď nabízí podporu alternativních cest CDN, které vám umožní zadat pro každý z nich další adresu URL, která odkazuje na stejný prostředek v síti pro doručování obsahu. Podpora sítě CDN umožňuje, aby váš skript a styly byly geograficky blíže k koncovým spotřebitelům webových aplikací. Pokud síť CDN není k dispozici, měla by provozní aplikace implementovat zálohu. Otestujte záložní.
- **Trasy a konfigurace ASP.NET webového rozhraní API byly přesunuty do *WebApiConfig. Register* static Method, který může být resused v testovacím kódu.** Dříve byly v *RouteConfig. RegisterRoutes* přidány trasy webového rozhraní API ASP.NET společně se standardními trasami MVC. Výchozí trasy a konfigurace webového rozhraní API ASP.NET jsou teď zpracovávány samostatnou metodou *WebApiConfig. Register* pro usnadnění testování.

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a>Známé problémy a zásadní změny

- **Verze RC a RTM ASP.NET MVC 4 nesprávně vrátila zobrazení desktopových počítačů v mezipaměti, pokud by se měla vrátit mobilní zobrazení.**

    - Podrobnosti o opravě najdete v tématu věnovaném [chybě ukládání do mezipaměti pro mobilní služby ASP.NET MVC 4](https://blogs.msdn.com/b/rickandy/archive/2012/09/17/asp-net-mvc-4-mobile-caching-bug-fixed.aspx) . Opravu lze nainstalovat z pevného balíčku NuGet [DisplayModes](http://nuget.org/packages/Microsoft.AspNet.Mvc.FixedDisplayModes) .
- **Přerušující se změny v modulu zobrazení Razor**. Následující typy byly odebrány z typu *System. Web. Mvc. Razor*: 

    - *ModelSpan*
    - *MvcVBRazorCodeGenerator*
    - *MvcCSharpRazorCodeGenerator*
    - *MvcVBRazorCodeParser*

  Odebraly se také následující metody: 

    - *MvcCSharpRazorCodeParser. ParseInheritsStatement (System. Web. Razor. Parser. CodeBlockInfo)*
    - *MvcWebPageRazorHost. DecorateCodeGenerator (System. Web. Razor. Generator. RazorCodeGenerator)*
    - *MvcVBRazorCodeParser. ParseInheritsStatement (System. Web. Razor. Parser. CodeBlockInfo)*
- **Pokud je WebMatrix. WebData. dll součástí adresáře/bin aplikací ASP.NET MVC 4, převezme adresu URL pro ověřování pomocí formulářů.** Přidání sestavení WebMatrix. WebData. dll do vaší aplikace (například výběrem možnosti "webové stránky ASP.NET se syntaxí Razor" při použití dialogového okna Přidat nasaditelné závislosti) dojde k přepsání přesměrování přihlášení ověřování na/account/Logon, nikoli/Account/Login podle očekávání výchozího řadiče účtů ASP.NET MVC. Chcete-li zabránit tomuto chování a použít zadanou adresu URL již v části ověřování souboru Web. config, můžete přidat appSetting s názvem PreserveLoginUrl a nastavit jej na hodnotu true: 

    [!code-xml[Main](mvc4-release-notes/samples/sample6.xml)]
- **Správce balíčků NuGet se nedokáže nainstalovat při pokusu o instalaci ASP.NET MVC 4 pro souběžnou instalaci sady Visual Studio 2010 a Visual Web Developer 2010.** Chcete-li spustit sadu Visual Studio 2010 a Visual Web Developer 2010 vedle sebe s ASP.NET MVC 4, je nutné nainstalovat ASP.NET MVC 4 poté, co byly obě verze sady Visual Studio již nainstalovány.
- **Odinstalace ASP.NET MVC 4 se nezdařila, pokud byly požadavky již odinstalovány.** Chcete-li vyčistit odinstalaci ASP.NET MVC 4You, je nutné před odinstalací sady Visual Studio odinstalovat ASP.NET MVC 4.
- **Instalace ASP.NET MVC 4 přerušuje aplikace ASP.NET MVC 3 RTM.** Aplikace ASP.NET MVC 3, které byly vytvořeny ve verzi RTM (nejsou ve verzi [ASP.NET MVC 3 Tools Update](https://www.microsoft.com/download/details.aspx?id=1491) ), vyžadují následující změny, aby fungovaly souběžně s ASP.NET MVC 4. Při sestavování projektu bez provedení těchto aktualizací dojde k chybám kompilace. 

    **Požadované aktualizace**

  1. V kořenovém souboru Web. config přidejte nový *&lt;appSettings&gt;* záznam s klíčovými *webovými stránkami: verze* a hodnota *1.0.0.0*. 

      [!code-xml[Main](mvc4-release-notes/samples/sample7.xml)]
  2. V Průzkumník řešení klikněte pravým tlačítkem myši na název projektu a pak vyberte Uvolnit projekt. Pak znovu klikněte pravým tlačítkem na název a vyberte upravit *ProjectName*. csproj.
  3. Vyhledejte následující odkazy na sestavení: 

      [!code-xml[Main](mvc4-release-notes/samples/sample8.xml)]

      Nahraďte je následujícími kroky:

      [!code-xml[Main](mvc4-release-notes/samples/sample9.xml)]
  4. Uložte změny, zavřete soubor projektu (. csproj), který jste upravovali, a potom klikněte pravým tlačítkem myši na projekt a vyberte možnost znovu načíst.

- **Změna projektu ASP.NET MVC 4 na cílovou 4,0 z 4,5 neaktualizuje odkaz na sestavení EntityFramework:** Pokud změníte projekt ASP.NET MVC 4 na cílovou verzi 4,0 po určený 4,5, odkaz na sestavení EntityFramework bude stále ukazovat na verzi 4,5. Pokud chcete tento problém vyřešit, odinstalujte a znovu nainstalujte balíček NuGet EntityFramework.
- **403 zakázané při spuštění aplikace ASP.NET MVC 4 v Azure po změně na cílovou 4,0 z 4,5:** Pokud změníte projekt ASP.NET MVC 4 na cílovou 4,0 po určený 4,5 a pak ho nasadíte do Azure, může se za běhu zobrazit Chyba 403 zakázáno. K řešení tohoto problému přidejte do souboru Web. config následující: `<modules runAllManagedModulesForAllRequests="true" />`
- **Při psaní\' v řetězcovém literálu v souboru Razor dojde k chybě sady Visual Studio 2012.** Chcete-li tento problém obejít, zadejte nejprve koncovou uvozovku řetězcového literálu.
- <strong>Když přejdete na &quot;účet/spravovat&quot; v šabloně Internet dojde k chybě za běhu pro jazyky CHS, rev a CHT.</strong> Pokud chcete problém vyřešit, upravte stránku tak, aby se <em>od@User.Identity.Namea</em> tak, že se umístí jako jediný obsah v rámci značky <em>&lt;Strong&gt;</em> .
- **Poskytovatelé Google a LinkedInu se na webech Azure nepodporují.** Při nasazování na weby Azure použijte alternativní zprostředkovatele ověřování.
- **Při použití UriPathExtensionMapping se službou IIS 8 Express nebo IIS se při pokusu o použití rozšíření zobrazí 404 nenalezené chyby.** Obslužná rutina statického souboru bude v konfliktu s požadavky na webová rozhraní API, která používají *UriPathExtensionMappings*. Pokud chcete tento problém obejít, nastavte *runAllManagedModulesForAllRequests = true* v souboru Web. config.
- **Metoda Controller. Execute již není volána.** Všechny řadiče MVC jsou nyní vždy spouštěny asynchronně.

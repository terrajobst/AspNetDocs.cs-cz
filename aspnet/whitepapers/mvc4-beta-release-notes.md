---
uid: whitepapers/mvc4-beta-release-notes
title: ASP.NET MVC 4 | Microsoft Docs
author: rick-anderson
description: Tento dokument popisuje vydání ASP.NET MVC 4 beta pro Visual Studio 2010.
ms.author: riande
ms.date: 09/09/2011
ms.assetid: 666407bb-81de-4319-89ba-0302c382a208
msc.legacyurl: /whitepapers/mvc4-beta-release-notes
msc.type: content
ms.openlocfilehash: 17800dfe091bbb7afb25f7f41e3bd885b882edb0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78523301"
---
# <a name="aspnet-mvc-4"></a>ASP.NET MVC 4

> Tento dokument popisuje vydání ASP.NET MVC 4 beta pro Visual Studio 2010.
> 
> > [!NOTE]
> > Nejedná se o nejaktuálnější verzi. Poznámky k verzi ASP.NET MVC 4 RC jsou k dispozici [zde](mvc4-release-notes.md).

- [Poznámky k instalaci](#_Toc303253802)
- [Dokumentace](#_Toc303253803)
- [Podpora](#_Toc303253804)
- [Požadavky na software](#_Toc303253805)
- [Upgrade projektu ASP.NET MVC 3 na ASP.NET MVC 4](#_Toc303253806)
- [Nové funkce v ASP.NET MVC 4 beta](#_Toc303253807)

    - [Webové rozhraní API v ASP.NET](#_Toc317096197)
    - [ASP.NET aplikace s jednou stránkou](#_Toc317096198)
    - [Vylepšení výchozích šablon projektů](#_Toc303253808)
    - [Šablona mobilního projektu](#_Toc303253809)
    - [Režimy zobrazení](#_Toc303253810)
    - [jQuery Mobile, přepínač zobrazení a přepsání prohlížeče](#_Toc303253811)
    - [Recepty pro generování kódu v aplikaci Visual Studio](#_Toc303253812)
    - [Podpora úloh pro asynchronní řadiče](#_Toc303253813)
    - [Sada Azure SDK](#_Toc303253814)
    - [Známé problémy a zásadní změny](#_Toc303253815)

<a id="_Toc303253802"></a>
## <a name="installation-notes"></a>Poznámky k instalaci

ASP.NET MVC 4 beta pro Visual Studio 2010 se dá nainstalovat z [domovské stránky ASP.NET MVC 4](../mvc/mvc4.md) pomocí instalačního programu webové platformy.

Před instalací ASP.NET MVC 4 beta musíte odinstalovat všechny dříve nainstalované verze Preview ASP.NET MVC 4.

Tato verze není kompatibilní s .NET Framework 4,5 Developer Preview. Před instalací sady ASP.NET MVC 4 beta je třeba odinstalovat .NET 4,5 Developer Preview.

ASP.NET MVC 4 se dá nainstalovat a může běžet souběžně s ASP.NET MVC 3.

<a id="_Toc303253803"></a>
## <a name="documentation"></a>Dokumentace

Dokumentace k ASP.NET MVC je k dispozici na webu MSDN na následující adrese URL:

[https://go.microsoft.com/fwlink/?LinkID=243043](https://go.microsoft.com/fwlink/?LinkID=243043)

Kurzy a další informace o ASP.NET MVC jsou k dispozici na stránce MVC 4 na webu ASP.NET ([https://www.asp.net/mvc/mvc4](../mvc/mvc4.md)).

<a id="_Toc303253804"></a>
## <a name="support"></a>Podpora

Toto je verze Preview a není oficiálně podporovaná. Pokud máte dotazy týkající se práce s touto verzí, pošlete je na fórum ASP.NET MVC ([https://forums.asp.net/1146.aspx](https://forums.asp.net/1146.aspx)), kde členové komunity ASP.NET často mohou zajistit neformální podporu.

<a id="_Toc303253805"></a>
## <a name="software-requirements"></a>Požadavky na software

Komponenty ASP.NET MVC 4 pro Visual Studio vyžadují PowerShell 2,0 a Visual Studio 2010 s aktualizací Service Pack 1 nebo Visual Web Developer Express 2010 s aktualizací Service Pack 1.

<a id="_Toc303253806"></a>
## <a name="upgrading-an-aspnet-mvc-3-project-to-aspnet-mvc-4"></a>Upgrade projektu ASP.NET MVC 3 na ASP.NET MVC 4

ASP.NET MVC 4 se dá nainstalovat souběžně s ASP.NET MVC 3 ve stejném počítači, což vám umožní pružně vybrat, kdy se má upgradovat aplikace ASP.NET MVC 3 na ASP.NET MVC 4.

Nejjednodušší způsob, jak upgradovat, je vytvoření nového projektu ASP.NET MVC 4 a zkopírování všech zobrazení, řadičů, kódu a souborů obsahu z existujícího projektu MVC 3 do nového projektu a následné aktualizace odkazů na sestavení v novém projektu tak, aby odpovídaly původnímu projektu. Pokud jste provedli změny v souboru Web. config v projektu MVC 3, musíte tyto změny také sloučit do souboru Web. config v projektu MVC 4.

Pokud chcete ručně upgradovat existující aplikaci ASP.NET MVC 3 na verzi 4, udělejte toto:

1. V všech souborech Web. config v projektu (v kořenu projektu existuje jedna z nich, jedna ve složce views a jedna ve složce zobrazení pro každou oblast v projektu) nahraďte všechny výskyty následujícího textu:

    [!code-console[Main](mvc4-beta-release-notes/samples/sample1.cmd)]

    s následujícím odpovídajícím textem:

    [!code-console[Main](mvc4-beta-release-notes/samples/sample2.cmd)]
2. V kořenovém souboru Web. config aktualizujte element *webpages: Version* na "2.0.0.0" a přidejte nový klíč *PreserveLoginUrl* , který má hodnotu "true":

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample3.xml)]
3. V Průzkumník řešení odstraňte odkaz na *System. Web. Mvc* (který odkazuje na knihovnu DLL verze 3). Pak přidejte odkaz na *System. Web. Mvc* (v 4.0.0.0). Konkrétně proveďte následující změny pro aktualizaci odkazů na sestavení. Podrobnosti najdete tady:

    1. V Průzkumník řešení odstraňte odkazy na následující sestavení: 

        - *System. Web. Mvc*(v 3.0.0.0)
        - *System. Web. webpages*(v 1.0.0.0)
        - *System. Web. Razor*(v 1.0.0.0)
        - *System. Web. webpages. Deployment*(v 1.0.0.0)
        - *System. Web. webpages. Razor*(v 1.0.0.0)
    2. Přidejte odkazy na následující sestavení: 

        - *System. Web. Mvc*(v 4.0.0.0)
        - *System. Web. webpages*(v 2.0.0.0)
        - *System. Web. Razor*(v 2.0.0.0)
        - *System. Web. webpages. Deployment*(v 2.0.0.0)
        - *System. Web. webpages. Razor*(v 2.0.0.0)
4. V Průzkumník řešení klikněte pravým tlačítkem myši na název projektu a pak vyberte Uvolnit projekt. Pak znovu klikněte pravým tlačítkem na název a vyberte upravit *ProjectName*. csproj.
5. Vyhledejte element *ProjectTypeGuids* a nahraďte {E53F8FEA-EAE0-44A6-8774-FFD645390401} řetězcem {E3E379DF-F4C6-4180-9B81-6769533ABE47}.
6. Uložte změny, zavřete soubor projektu (. csproj), který jste upravovali, klikněte pravým tlačítkem myši na projekt a pak vyberte znovu načíst projekt.
7. Pokud projekt odkazuje na jakékoli knihovny třetích stran, které jsou kompilovány pomocí předchozích verzí ASP.NET MVC, otevřete kořenový soubor Web. config a přidejte následující tři prvky *bindingRedirect* do oddílu *Konfigurace* : 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample4.xml)]

<a id="_Toc303253807"></a>
## <a name="new-features-in-aspnet-mvc-4-beta"></a>Nové funkce v ASP.NET MVC 4 beta

Tato část popisuje funkce, které byly představeny ve verzi ASP.NET MVC 4 beta.

<a id="_Toc317096197"></a>
### <a name="aspnet-web-api"></a>Webové rozhraní API ASP.NET

ASP.NET MVC 4 nyní zahrnuje webové rozhraní API ASP.NET, novou architekturu pro vytváření služeb HTTP, které mohou oslovit širokou škálu klientů včetně prohlížečů a mobilních zařízení. Webové rozhraní API ASP.NET je také ideální platformou pro vytváření služeb RESTful.

Webové rozhraní API pro ASP.NET zahrnuje podporu pro následující funkce:

- **Moderní programovací model http:** Přímý přístup a manipulace s požadavky HTTP a odpověďmi ve webových rozhraních API pomocí nového a silně typovaného objektového modelu HTTP. Stejný programovací model a kanál HTTP jsou symetricky k dispozici na klientovi prostřednictvím nového typu HttpClient.
- **Plná podpora pro trasy**: webová rozhraní API teď podporují úplnou sadu možností směrování, které jsou vždycky součástí webového zásobníku, včetně parametrů a omezení trasy. Kromě toho mapování na akce má úplnou podporu pro konvence, takže už nemusíte používat atributy, jako je například [HttpPost], na vaše třídy a metody.
- **Vyjednávání obsahu**: klient a server můžou spolupracovat na tom, aby určily správný formát dat vrácených z rozhraní API. Poskytujeme výchozí podporu pro formáty kódování XML, JSON a forma formátu URL a můžete tuto podporu rozšíření přidat pomocí vlastních formátovacích modulů nebo dokonce nahradit výchozí strategii vyjednávání obsahu.
- **Vazba modelů a ověřování:** Pořadače modelů poskytují snadný způsob, jak extrahovat data z různých částí požadavku HTTP a převádět tyto části do objektů .NET, které může používat akce webového rozhraní API.
- **Filtry:** Webová rozhraní API teď podporují filtry, včetně známých filtrů, jako je například atribut [autorizovat]. Můžete vytvářet a připojovat vlastní filtry pro akce, autorizaci a zpracování výjimek.
- **Složení dotazu:** Tím, že jednoduše vrátí IQueryable&lt;T&gt;, vaše webové rozhraní API bude podporovat dotazování prostřednictvím konvencí adresy URL OData.
- **Vylepšená testování podrobností http:** Místo nastavení podrobností HTTP ve statických objektech kontextu můžou akce webového rozhraní API pracovat s instancemi zprávy HttpRequestMessage a HttpResponseMessage. Obecné verze těchto objektů také existují, aby bylo možné pracovat s vlastními typy společně s typy HTTP.
- **Vylepšení inverze ovládacího prvku (IOC) prostřednictvím DependencyResolver:** Webové rozhraní API teď používá ke zjištění instancí mnoha různých zařízení vzor lokátoru služby implementovaný překladačem závislostí MVC.
- **Konfigurace založená na kódu:** Konfigurace webového rozhraní API se provádí výhradně prostřednictvím kódu, takže se soubory Config nechají vyčistit.
- **Samoobslužný hostitel:** Webová rozhraní API je možné kromě služby IIS hostovat i ve vašem vlastním procesu a přitom pořád využívat úplný výkon tras a dalších funkcí webového rozhraní API.

Další podrobnosti o webovém rozhraní API ASP.NET najdete na [https://www.asp.net/web-api](../web-api/index.md).

<a id="_Toc317096198"></a>
### <a name="aspnet-single-page-application"></a>ASP.NET aplikace s jednou stránkou

ASP.NET MVC 4 teď obsahuje předběžnou verzi Preview prostředí pro vytváření jednoduchých aplikací s výraznými interakcemi na straně klienta pomocí rozhraní JavaScript a webových rozhraní API. Tato podpora zahrnuje:

- Sada knihoven JavaScriptu pro rozsáhlejší místní interakce s daty uloženými v mezipaměti
- Další součásti webového rozhraní API pro pracovní jednotku a podporu DAL
- Šablona projektu MVC s generováním uživatelského rozhraní, která umožňuje rychle začít

Pokud chcete získat další informace o podpoře jednostránkové aplikace v ASP.NET MVC 4, navštivte prosím [https://www.asp.net/single-page-application](../single-page-application/index.md).

<a id="_Toc303253808"></a>
### <a name="enhancements-to-default-project-templates"></a>Vylepšení výchozích šablon projektů

Šablona, která se používá k vytvoření nových projektů ASP.NET MVC 4, se aktualizovala tak, aby vytvořila moderní web s častým hledáním:

![](mvc4-beta-release-notes/_static/image1.png)

Kromě toho, že je v nové šabloně k dispozici vylepšení kosmetických prostředků, lepší funkce. Tato šablona využívá techniku označovanou jako adaptivní vykreslování, aby vypadala dobře v desktopových prohlížečích i v mobilních prohlížečích bez jakýchkoli úprav.

![](mvc4-beta-release-notes/_static/image2.png)

Chcete-li zobrazit adaptivní vykreslování v akci, můžete použít mobilní emulátor nebo stačí zkusit změnit velikost okna prohlížeče plochy na menší. Dojde-li k zobrazení okna prohlížeče dostatečně malého, změní se rozložení stránky.

Dalším vylepšením výchozí šablony projektu je použití JavaScriptu k poskytnutí bohatšího uživatelského rozhraní. Odkazy na přihlášení a registraci, které jsou používány v šabloně, jsou příklady použití dialogového okna uživatelského rozhraní jQuery k zobrazení stránky s bohatou přihlašovací obrazovkou:

![](mvc4-beta-release-notes/_static/image3.png)

<a id="_Toc303253809"></a>
### <a name="mobile-project-template"></a>Šablona mobilního projektu

Pokud spouštíte nový projekt a chcete vytvořit web speciálně pro mobilní prohlížeče a tablety, můžete použít šablonu projektu nové mobilní aplikace. To je založené na jQuery Mobile, open source knihovně pro sestavování tónově optimalizovaného uživatelského rozhraní:

![](mvc4-beta-release-notes/_static/image4.png)

Tato šablona obsahuje stejnou strukturu aplikace jako šablona internetové aplikace (a kód kontroleru je prakticky identický), ale je ve stylu jQuery Mobile, aby vypadala dobře a pracovala na dotykové mobilní zařízeních. Další informace o způsobu strukturování a stylu mobilního uživatelského rozhraní naleznete na [webu jQuery Mobile Project](http://jquerymobile.com/).

Pokud již máte web orientovaný na plochu, do kterého chcete přidat zobrazení optimalizovaná pro mobilní zařízení, nebo pokud chcete vytvořit jednu lokalitu, která bude pro stolní a mobilní prohlížeče používat jiná zobrazení s různými styly, můžete použít novou funkci zobrazení režimů. (Další informace najdete v další části.)

<a id="_Toc303253810"></a>
### <a name="display-modes"></a>Režimy zobrazení

Funkce nové režimy zobrazení umožňuje aplikaci vybrat zobrazení v závislosti na prohlížeči, který požadavek odeslal. Pokud například prohlížeč stolních počítačů požaduje domovskou stránku, může aplikace použít šablonu Views\Home\Index.cshtml. Pokud mobilní prohlížeč požaduje domovskou stránku, může aplikace vrátit šablonu Views\Home\Index.mobile.cshtml.

Rozložení a částečné typy lze také přepsat pro konkrétní typy prohlížečů. Příklad:

- Pokud vaše složka Views\Shared obsahuje rozvržení \_layout. cshtml a \_layout. Mobile. cshtml, ve výchozím nastavení bude aplikace používat \_layout. Mobile. cshtml během požadavků z mobilních prohlížečů a \_layout. cshtml během ostatních požadavků.
- Pokud složka obsahuje \_MyPartial. cshtml a \_MyPartial. Mobile. cshtml, instrukce @Html.Partial("\_MyPartial") bude vykreslovat \_MyPartial. Mobile. cshtml během požadavků z mobilních prohlížečů a \_MyPartial. cshtml během ostatních požadavků.

Pokud chcete vytvořit konkrétnější zobrazení, rozložení nebo částečná zobrazení pro jiná zařízení, můžete zaregistrovat novou instanci *DefaultDisplayMode* a určit, který název se má vyhledat, když požadavek splní určité podmínky. Do souboru Global. asax můžete například přidat následující *\_* kód, který zaregistruje řetězec "iPhone" jako režim zobrazení, který se použije, když prohlížeč Apple iPhone vytvoří požadavek:

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample5.cs)]

Po spuštění tohoto kódu, když se v prohlížeči Apple iPhone vytvoří žádost, bude vaše aplikace používat Views\Shared\\_Layout. iPhone. cshtml rozložení (pokud existuje).

<a id="_Toc303253811"></a>
### <a name="jquery-mobile-the-view-switcher-and-browser-overriding"></a>jQuery Mobile, přepínač zobrazení a přepsání prohlížeče

jQuery Mobile je open source knihovna pro sestavení webového uživatelského rozhraní optimalizovaného pro dotykové ovládání. Pokud chcete použít jQuery Mobile s aplikací ASP.NET MVC 4, můžete si stáhnout a nainstalovat balíček NuGet, který vám pomůže začít. Pokud ho chcete nainstalovat z konzoly Správce balíčků sady Visual Studio, zadejte následující příkaz:

[!code-powershell[Main](mvc4-beta-release-notes/samples/sample6.ps1)]

Tím se nainstaluje jQuery Mobile a některé pomocné soubory, včetně následujících:

- Zobrazení/Shared/\_layout. Mobile. cshtml, což je rozložení založené na mobilním systému jQuery.
- Komponenta s přepínačem zobrazení, která se skládá z částečného zobrazení zobrazení/Shared/\_ViewSwitcher. cshtml a řadiče ViewSwitcherController.cs.

Po instalaci balíčku spusťte aplikaci v mobilním prohlížeči (nebo s ekvivalentními oprávněními, jako je doplněk pro [přepínač uživatelského agenta](http://chrispederick.com/work/user-agent-switcher/) prohlížeče Firefox). Uvidíte, že stránky vypadají velmi jinak, protože aplikace jQuery Mobile zpracovává rozložení a styl. Abyste to mohli využít, můžete postupovat takto:

- Vytvořte přepsání pro mobilní zařízení, jak je popsáno v části [režimy zobrazení](#_Toc303253810) výše (například vytvořit Views\Home\Index.Mobile.cshtml pro přepsání Views\Home\Index.cshtml pro mobilní prohlížeče).
- Další informace o tom, jak do mobilních zobrazení přidat prvky uživatelského rozhraní optimalizované pro dotykové ovládání, najdete v dokumentaci k nástroji [jQuery](http://jquerymobile.com/) .

Konvence pro mobilní optimalizované webové stránky je přidat odkaz, jehož text je například desktopové zobrazení nebo režim celého webu, který umožňuje uživatelům přepnout na desktopovou verzi stránky. Balíček jQuery. Mobile. MVC obsahuje ukázkovou komponentu pro přepínání zobrazení pro tento účel. Používá se ve výchozím Views\Shared\\_Layout. Mobile. cshtml a vypadá to, že se stránka vykresluje:

![](mvc4-beta-release-notes/_static/image5.png)

Pokud návštěvník klikne na odkaz, přepne na desktopovou verzi stejné stránky.

Vzhledem k tomu, že vaše rozložení na ploše nebude ve výchozím nastavení zahrnovat přepínač zobrazení, Návštěvníci nebudou mít možnost získat přístup do mobilního režimu. Pokud to chcete povolit, přidejte následující odkaz *\_ViewSwitcher* do rozložení plochy, a to těsně uvnitř *&lt;těla&gt;* elementu:

[!code-cshtml[Main](mvc4-beta-release-notes/samples/sample7.cshtml)]

Přepínač zobrazení používá novou funkci nazvanou přepisování prohlížeče. Tato funkce umožňuje, aby vaše aplikace považovala požadavky, jako kdyby dostala z jiného prohlížeče (uživatelského agenta), než je ten, ze kterého jsou ve skutečnosti. V následující tabulce je uveden seznam metod, které potlačuje prohlížeč poskytuje.

| `HttpContext.SetOverriddenBrowser(userAgentString)` | Přepíše hodnotu skutečného uživatelského agenta žádosti pomocí zadaného uživatelského agenta. |
| --- | --- |
| `HttpContext.GetOverriddenUserAgent()` | Vrátí hodnotu přepsání uživatelského agenta požadavku nebo skutečný řetězec uživatelského agenta, pokud nebylo zadáno žádné přepsání. |
| `HttpContext.GetOverriddenBrowser()` | Vrátí instanci *HttpBrowserCapabilitiesBase* , která odpovídá uživatelskému agentovi, který je aktuálně nastaven pro požadavek (skutečnost nebo přepsání). Tuto hodnotu můžete použít k získání vlastností, jako je například *IsMobileDevice*. |
| `HttpContext.ClearOverriddenBrowser()` | Odebere každého přepsaného uživatelského agenta pro aktuální žádost. |

Přepsání prohlížeče je základní funkcí ASP.NET MVC 4 a je k dispozici i v případě, že balíček jQuery. Mobile. MVC nenainstalujete. Má však vliv pouze na zobrazení, rozložení a výběr částečně, a to nijak neovlivní žádnou jinou funkci ASP.NET, která závisí na objektu *Request. browser* .

Ve výchozím nastavení se přepsání User-Agent ukládá pomocí souboru cookie. Chcete-li uložit přepsání jinde (například v databázi), můžete nahradit výchozího zprostředkovatele (*BrowserOverrideStores. Current*). Dokumentace k tomuto poskytovateli bude k dispozici pro pozdější vydání služby ASP.NET MVC.

<a id="_Toc303253812"></a>
### <a name="recipes-for-code-generation-in-visual-studio"></a>Recepty pro generování kódu v aplikaci Visual Studio

Nová funkce recepty umožňuje aplikaci Visual Studio generovat kód specifický pro řešení na základě balíčků, které můžete nainstalovat pomocí NuGet. Rozhraní recepty usnadňuje vývojářům psát moduly plug-in pro generování kódu, které můžete použít také k nahrazení vestavěných generátorů kódu pro přidat oblast, přidat kontroler a přidat zobrazení. Vzhledem k tomu, že recepty jsou nasazeny jako balíčky NuGet, mohou být snadno zkontrolovány do správy zdrojového kódu a sdíleny se všemi vývojáři na projektu automaticky. Jsou také k dispozici na základě jednotlivých řešení.

<a id="_Toc303253813"></a>
### <a name="task-support-for-asynchronous-controllers"></a>Podpora úloh pro asynchronní řadiče

Nyní můžete napsat asynchronní metody akcí jako jediné metody, které vracejí objekt typu *Task* nebo *task&lt;ActionResult&gt;* .

Například pokud používáte Visual C# 5 (nebo použití [asynchronní CTP](https://msdn.microsoft.com/vstudio/async.aspx)), můžete vytvořit asynchronní metodu akce, která bude vypadat následovně:

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample8.cs)]

V metodě předchozí akce se volání *newsService. GetHeadlinesAsync* a *sportsService. GetScoresAsync* nazývají asynchronně a neblokují vlákno z fondu vláken.

Asynchronní metody akcí, které vracejí instance *úloh* , mohou také podporovat časové limity. Chcete-li provést metodu akce zrušit, přidejte do signatury metody Action parametr typu *CancellationToken* . Následující příklad ukazuje metodu asynchronní akce, která má časový limit 2500 milisekund a zobrazuje zobrazení *časového* limitu klientovi, pokud dojde k vypršení časového limitu.

[!code-csharp[Main](mvc4-beta-release-notes/samples/sample9.cs)]

<a id="_Toc303253814"></a>
### <a name="azure-sdk"></a>Azure SDK

ASP.NET MVC 4 beta podporuje vydání sady Windows Azure SDK ze září 2011 1,5.

<a id="_Toc303253815"></a>
## <a name="known-issues-and-breaking-changes"></a>Známé problémy a zásadní změny

- **Po instalaci ASP.NET MVC 4 beta se Editor CSHTML/VBHTML v sadě Visual Studio 2010 s aktualizací Service Pack 1 CSHTML/VBHTML může po zadání fragmentu nebo JavaScriptu do souborů cshtml nebo VBHTML pozastavit po dlouhou dobu.** K tomu dochází pouze v aplikacích ASP.NET MVC 4, které byly vytvořeny a nebyly dosud kompilovány.

    Alternativním řešením je zkompilovat projekt a získat sestavení ve složce bin. Poznámka: Pokud vyčistíte projekt, který odebere sestavení ze složky bin, problém s editorem se vrátí.

    Tato akce bude opravena v příští verzi.
- **C#Šablony projektů pro Visual Studio 11 Beta obsahují v Global.asax.cs nesprávný připojovací řetězec.** Výchozí připojení zadané v metodě spustit\_aplikace pro projekty vytvořené v aplikaci Visual Studio 11 Beta obsahují připojovací řetězec LocalDB, který obsahuje zpětné lomítko (\) znak). Výsledkem je chyba připojení při pokusu o přístup k Entity Framework DbContext, která generuje SqlException.

    Chcete-li tento problém vyřešit, vydejte znak zpětného lomítka v aplikaci\_Start metody Global.asax.cs, aby vypadal takto:

    [!code-csharp[Main](mvc4-beta-release-notes/samples/sample10.cs)]
- **ASP.NET aplikace MVC 4, které cílí na .NET 4,5, vyvolají FileLoadException při pokusu o přístup k sestavení System. NET. http. dll při spuštění pod .NET 4,0.** Aplikace ASP.NET MVC 4 vytvořené v rámci .NET 4,5 obsahují přesměrování vazby, které má za následek FileLoadException, které státy nemohly načíst soubor nebo sestavení System .NET. http nebo jedna z jeho závislostí. Při spuštění aplikace v systému s nainstalovanou platformou .NET 4,0. Chcete-li tento problém vyřešit, odeberte následující přesměrování vazby ze souboru Web. config:

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample11.xml)]

    Element vazby sestavení v upraveném souboru Web. config by měl vypadat takto:

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample12.xml)]
- <strong>Šablona položky přidat kontroler v projektech Visual Basic generuje nesprávný obor názvů při vyvolání</strong><strong>zevnitř oblasti.</strong> Když přidáte kontroler do oblasti v projektu ASP.NET MVC, který používá Visual Basic, Šablona položky vloží do kontroleru nesprávný obor názvů. Výsledkem je chyba "soubor nebyl nalezen" při přechodu na jakoukoli akci v kontroleru.  
  
  Vygenerovaný obor názvů vynechá vše po kořenovém oboru názvů. Například vygenerovaný obor názvů je *RootNamespace* , ale měl by být *RootNamespace. areas. areas. Controllers* .
- **Přerušující se změny v modulu zobrazení Razor.** V rámci přepsání analyzátoru Razor byly z *System. Web. Mvc. Razor*odebrány následující typy: 

    - *ModelSpan*
    - *MvcVBRazorCodeGenerator*
    - *MvcCSharpRazorCodeGenerator*
    - *MvcVBRazorCodeParser*

  Odebraly se také následující metody: 

    - *MvcCSharpRazorCodeParser. ParseInheritsStatement (System. Web. Razor. Parser. CodeBlockInfo)*
    - *MvcWebPageRazorHost. DecorateCodeGenerator (System. Web. Razor. Generator. RazorCodeGenerator)*
    - *MvcVBRazorCodeParser. ParseInheritsStatement (System. Web. Razor. Parser. CodeBlockInfo)*
- **Pokud je WebMatrix. WebData. dll součástí adresáře/bin aplikací ASP.NET MVC 4, převezme adresu URL pro ověřování pomocí formulářů.** Přidání sestavení WebMatrix. WebData. dll do vaší aplikace (například výběrem možnosti "webové stránky ASP.NET se syntaxí Razor" při použití dialogového okna Přidat nasaditelné závislosti) dojde k přepsání přesměrování přihlášení ověřování na/account/Logon, nikoli/Account/Login podle očekávání výchozího řadiče účtů ASP.NET MVC. Chcete-li zabránit tomuto chování a použít zadanou adresu URL již v části ověřování souboru Web. config, můžete přidat appSetting s názvem PreserveLoginUrl a nastavit jej na hodnotu true: 

    [!code-xml[Main](mvc4-beta-release-notes/samples/sample13.xml)]
- **Správce balíčků NuGet se nedokáže nainstalovat při pokusu o instalaci ASP.NET MVC 4 pro souběžnou instalaci sady Visual Studio 2010 a Visual Web Developer 2010.** Chcete-li spustit sadu Visual Studio 2010 a Visual Web Developer 2010 vedle sebe s ASP.NET MVC 4, je nutné nainstalovat ASP.NET MVC 4 poté, co byly obě verze sady Visual Studio již nainstalovány.
- **Odinstalace ASP.NET MVC 4 se nezdařila, pokud byly požadavky již odinstalovány.** Chcete-li vyčistit odinstalaci ASP.NET MVC 4You, je nutné před odinstalací sady Visual Studio odinstalovat ASP.NET MVC 4.
- **Když spustíte výchozí projekt webového rozhraní API, zobrazí se pokyny, které uživatele nesprávně nasměrují, aby mohli přidávat trasy pomocí metody RegisterApis, která neexistuje.** Trasy by měly být přidány v metodě RegisterRoutes pomocí směrovací tabulky ASP.NET.
- **Instalace ASP.NET MVC 4 beta přerušuje aplikace ASP.NET MVC 3 RTM.** Aplikace ASP.NET MVC 3, které byly vytvořeny ve verzi RTM (nejsou ve verzi ASP.NET MVC 3 Tools Update), vyžadují následující změny, aby bylo možné pracovat vedle sebe s ASP.NET MVC 4 beta. Při sestavování projektu bez provedení těchto aktualizací dojde k chybám kompilace. 

    **Požadované aktualizace**

  1. V kořenovém souboru Web. config přidejte nový *&lt;appSettings&gt;* záznam s klíčovými *webovými stránkami: verze* a hodnota *1.0.0.0*.

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample14.xml)]
  2. V Průzkumník řešení klikněte pravým tlačítkem myši na název projektu a pak vyberte Uvolnit projekt. Pak znovu klikněte pravým tlačítkem na název a vyberte upravit *ProjectName*. csproj.
  3. Vyhledejte následující odkazy na sestavení: 

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample15.xml)]

      Nahraďte je následujícími kroky:

      [!code-xml[Main](mvc4-beta-release-notes/samples/sample16.xml)]
  4. Uložte změny, zavřete soubor projektu (. csproj), který jste upravovali, a potom klikněte pravým tlačítkem myši na projekt a vyberte možnost znovu načíst.

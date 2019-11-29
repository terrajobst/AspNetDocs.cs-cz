---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax
title: Principy částečných aktualizací stránek pomocí ASP.NET AJAX | Microsoft Docs
author: scottcate
description: Nejužitečnější funkce rozšíření AJAX ASP.NET je možnost provádět částečné nebo přírůstkové aktualizace stránky bez úplného zpětného odeslání na t...
ms.author: riande
ms.date: 03/28/2008
ms.assetid: 54d9df99-1161-4899-b4e8-2679c85915e7
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-partial-page-updates-with-asp-net-ajax
msc.type: authoredcontent
ms.openlocfilehash: 4b87cb8f58dbd7f27b16bcb0d488ff361770d4fe
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74622990"
---
# <a name="understanding-partial-page-updates-with-aspnet-ajax"></a>Principy částečných aktualizací stránek technologií ASP.NET AJAX

[Scott Cate](https://github.com/scottcate)

[Stáhnout PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial01_Partial_Page_Updates_cs.pdf)

> Nejužitečnější funkce rozšíření AJAX ASP.NET je možnost provádět částečné nebo přírůstkové aktualizace stránky bez nutnosti úplného postbacku na server, aniž by došlo ke změně kódu a minimálním změnám kódu. Výhody jsou rozsáhlé – stav vašich multimédií (například Adobe Flash nebo Windows Media) se nezměnil, snižuje náklady na šířku pásma a u klienta se neobjeví blikání, které je obvykle spojené s postbackem.

## <a name="introduction"></a>Úvod

Technologie Microsoftu pro ASP.NET přináší objektově orientovaný a řízený programovací model a podílí se na nich s výhodami zkompilovaného kódu. Nicméně jeho model zpracování na straně serveru má několik nevýhod, které přináší technologie:

- Aktualizace stránky vyžadují zpáteční cestu k serveru, který vyžaduje obnovení stránky.
- Výměna zpráv neuchovává žádné efekty vygenerované JavaScriptem nebo jinými technologiemi na straně klienta (například Adobe Flash).
- Při postbacku nepodporují automatické obnovení pozice posouvání prohlížeče jiné než Microsoft Internet Explorer. A dokonce i v Internet Exploreru se při aktualizaci stránky stále bliká.
- Zpětná volání mohou zahrnovat velkou šířku pásma, protože pole \_\_formuláře VIEWSTATE může růst, zejména při práci s ovládacími prvky, jako je ovládací prvek GridView nebo Repeater.
- Neexistuje žádný jednotný model pro přístup k webovým službám prostřednictvím JavaScriptu nebo jiné technologie na straně klienta.

Zadejte rozšíření AJAX Microsoftu pro ASP.NET. AJAX, který **představuje synchronní** **J** avaScript **A** ND **X** ml, je integrovaná architektura pro poskytování přírůstkových aktualizací stránky prostřednictvím JavaScriptu pro různé platformy, skládající se z kódu na straně serveru, který tvoří rozhraní Microsoft AJAX Framework, a komponenty skriptu nazvané Microsoft AJAX Script Library. Rozšíření ASP.NET AJAX také poskytují podporu pro více platforem pro přístup k webovým službám ASP.NET prostřednictvím JavaScriptu.

Tento dokument White Paper prověřuje funkci částečné aktualizace stránky rozšíření AJAX ASP.NET, která zahrnuje komponentu ScriptManager, ovládací prvek UpdatePanel a ovládací prvek UpdateProgress, a bere v úvahu scénáře, ve kterých by měly být nebo neměly být využívá.

Tento dokument White Paper vychází z verze beta 2 sady Visual Studio 2008 a .NET Framework 3,5, která integruje rozšíření ASP.NET AJAX do knihovny základních tříd (kde byla dříve součástí doplňku pro ASP.NET 2,0). Tento dokument White Paper také předpokládá, že používáte Visual Studio 2008 a ne Visual Web Developer Express Edition; Některé odkazované šablony projektu nemusí být k dispozici uživatelům aplikace Visual Web Developer Express.

## <a name="partial-page-updates"></a>Částečné aktualizace stránky

Nejužitečnější funkce rozšíření AJAX ASP.NET je možnost provádět částečné nebo přírůstkové aktualizace stránky bez nutnosti úplného postbacku na server, aniž by došlo ke změně kódu a minimálním změnám kódu. Výhody jsou rozsáhlé – stav vašich multimédií (například Adobe Flash nebo Windows Media) se nezměnil, snižuje náklady na šířku pásma a u klienta se neobjeví blikání, které je obvykle spojené s postbackem.

Možnost integrace částečného vykreslování stránky je integrována do ASP.NET s minimálními změnami v projektu.

## <a name="walkthrough-integrating-partial-rendering-into-an-existing-project"></a>Návod: integrace částečného vykreslování do existujícího projektu

1. V Microsoft Visual Studio 2008 vytvořte nový projekt webu ASP.NET tak, že kliknete na <em>soubor</em> <em>-&gt; nový</em> <em>-&gt; web</em> a vyberete web ASP.NET z dialogového okna. Můžete si ho pojmenovat bez ohledu na to, co chcete, a můžete ho nainstalovat buď do systému souborů, nebo do Internetová informační služba (IIS).
2. Zobrazí se prázdná výchozí stránka se základní značkou ASP.NET (formulář na straně serveru a direktiva `@Page`). Přetáhněte popisek s názvem `Label1` a tlačítko s názvem `Button1` na stránku v rámci prvku formuláře. Můžete nastavit jejich vlastnosti textu tak, aby cokoli, co chcete.
3. V zobrazení Návrh dvakrát klikněte `Button1` pro vygenerování obslužné rutiny události kódu na pozadí. V rámci této obslužné rutiny události nastavte `Label1.Text` pro kliknutí na tlačítko! .

**Výpis 1: označení pro default. aspx před povolením částečného vykreslování**

[!code-aspx[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample1.aspx)]

**Výpis 2: CodeBehind (oříznuto) v default.aspx.cs**

[!code-csharp[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample2.cs)]

1. Stisknutím klávesy F5 spusťte svůj web. Visual Studio vás vyzve k přidání souboru Web. config pro povolení ladění. Udělejte to. Po kliknutí na tlačítko si všimněte, že se stránka aktualizuje a změní text v popisku a při překreslení stránky se zobrazí krátká blikání.
2. Po zavření okna prohlížeče se vraťte do sady Visual Studio a na stránku značek. V sadě nástrojů sady Visual Studio přejděte dolů a najděte kartu Rozšíření AJAX. (Pokud tuto kartu nemáte, protože používáte starší verzi rozšíření AJAX nebo Atlas, přečtěte si návod k registraci položek sady nástrojů rozšíření AJAX později v tomto dokumentu White Paper nebo nainstalujte aktuální verzi pomocí Instalační služba systému Windows ke stažení. z webu).

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image2.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image1.png)

([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-partial-page-updates-with-asp-net-ajax/_static/image3.png))

1. <em>Známý problém:</em> Pokud sadu Visual Studio 2008 nainstalujete do počítače, na kterém již je nainstalována sada Visual Studio 2005 s rozšířeními ASP.NET 2,0 AJAX, bude Visual Studio 2008 importovat položky sady nástrojů rozšíření AJAX. To, jestli se jedná o tento případ, můžete zjistit tak, že prozkoumáte popisy těchto komponent. měli byste vyslovit verzi 3.5.0.0. Pokud říká verze 2.0.0.0, pak jste importovali staré položky sady nástrojů a bude nutné je ručně importovat pomocí dialogového okna zvolit položky sady nástrojů v sadě Visual Studio. Pomocí návrháře nebude možné přidat ovládací prvky verze 2.

2. Před začátkem `<asp:Label>` značky vytvořte řádek prázdných znaků a dvakrát klikněte na ovládací prvek UpdatePanel v sadě nástrojů. Všimněte si, že v horní části stránky je obsažena nová direktiva `@Register`, která označuje, že ovládací prvky v oboru názvů System. Web. UI by měly být importovány pomocí předpony `asp:`.
3. Přetáhněte uzavírací `</asp:UpdatePanel>` tag po konci elementu Button, aby byl element ve správném formátu s zabalené ovládací prvky Label a Button.
4. Po otevření značky `<asp:UpdatePanel>` začněte otevírat novou značku. Všimněte si, že IntelliSense zobrazí výzvu se dvěma možnostmi. V takovém případě vytvořte značku `<ContentTemplate>`. Nezapomeňte tuto značku kolem popisku a tlačítka zabalit tak, aby byl kód ve správném formátu.

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image5.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image4.png)

([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-partial-page-updates-with-asp-net-ajax/_static/image6.png))

1. Kdekoli v rámci prvku `<form>` přidejte ovládací prvek ScriptManager Poklikáním na položku `ScriptManager` v sadě nástrojů.
2. Upravte značku `<asp:ScriptManager>` tak, aby obsahovala atribut `EnablePartialRendering= true`.

**Výpis 3: označení pro default. aspx s povoleným částečným vykreslováním**

[!code-aspx[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample3.aspx)]

1. Otevřete soubor Web. config. Všimněte si, že Visual Studio automaticky přidalo odkaz na kompilaci do System. Web. Extensions. dll.

1. Novinky ve Visual Studiu 2008: soubor Web. config, který je součástí šablon projektů webu ASP.NET, automaticky zahrnuje všechny nezbytné odkazy na rozšíření ASP.NET AJAX a obsahuje oddíly informací o konfiguraci, které mohou být zrušením komentáře umožníte další funkce. Po instalaci rozšíření ASP.NET 2,0 AJAX byly sady Visual Studio 2005 podobné šablony. V aplikaci Visual Studio 2008 jsou však rozšíření AJAX ve výchozím nastavení zaregistrována (to znamená, že jsou ve výchozím nastavení odkazována, ale lze je odebrat jako odkazy).

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image8.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image7.png)

([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-partial-page-updates-with-asp-net-ajax/_static/image9.png))

1. Stisknutím klávesy F5 spusťte svůj web. Všimněte si, jak se změnily žádné změny zdrojového kódu pro podporu částečného vykreslování značek.

Po spuštění webu by se mělo zobrazit, že je nyní povoleno částečné vykreslování, protože po kliknutí na tlačítko nebude blikat, ani nedojde k žádné změně v umístění posunutí stránky (Tento příklad neukazuje na). Pokud jste se po kliknutí na tlačítko podívái na vykreslený zdroj stránky, potvrďte, že ve skutečnosti nedošlo k chybě, původní text popisku je stále součástí zdrojového kódu a popisek se změnil prostřednictvím JavaScriptu.

Visual Studio 2008 se nedodává s předem definovanou šablonou pro web s podporou AJAX ASP.NET. Nicméně tato šablona byla k dispozici v sadě Visual Studio 2005, pokud byla nainstalována rozšíření AJAX sady Visual Studio 2005 a ASP.NET 2,0. V důsledku toho bude pravděpodobně konfigurace webu a počínaje šablonou webu s podporou jazyka AJAX ještě snazší, protože šablona by měla obsahovat plně nakonfigurovaný soubor Web. config (podpora všech rozšíření ASP.NET AJAX, včetně přístupu k webovým službám). a serializace JSON – JavaScript Object Notation) a ve výchozím nastavení zahrnuje UpdatePanel a ContentTemplate v rámci hlavní stránky webových formulářů. Povolení částečného vykreslování s touto výchozí stránkou je jednoduché jako přechází krok 10 tohoto návodu a přehození ovládacích prvků na stránku.

## <a name="the-scriptmanager-control"></a>Ovládací prvek ScriptManager

## <a name="scriptmanager-control-reference"></a>Odkaz na ovládací prvek ScriptManager

Vlastnosti s povolenou značkou:

| **Název vlastnosti** | **Textový** | **Popis** |
| --- | --- | --- |
| AllowCustomErrors – přesměrování | Logick | Určuje, jestli se má použít oddíl vlastní chyby souboru Web. config ke zpracování chyb. |
| AsyncPostBackError – zpráva | String | Získá nebo nastaví chybovou zprávu odeslanou klientovi, pokud je vyvolána chyba. |
| AsyncPostBack – časový limit | Int32 | Získá nebo nastaví výchozí dobu, po kterou by měl klient čekat na dokončení asynchronního požadavku. |
| EnableScript – globalizace | Logick | Získá nebo nastaví, zda je povoleno globalizace skriptů. |
| EnableScript – lokalizace | Logick | Získává nebo nastavuje, jestli je povolená lokalizace skriptů. |
| ScriptLoadTimeout | Int32 | Určuje počet sekund povolených pro načtení skriptů do klienta. |
| ScriptMode | Enum (auto, Debug, Release, dědění) | Získá nebo nastaví, jestli se mají vykreslovat verze pro vydání skriptů. |
| scriptPath | String | Získá nebo nastaví kořenovou cestu k umístění souborů skriptu, které se mají odeslat klientovi. |

Vlastnosti pouze kódu:

| **Název vlastnosti** | **Textový** | **Popis** |
| --- | --- | --- |
| AuthenticationService | AuthenticationService – nadřízený | Získá podrobnosti o proxy ověřovací službě ASP.NET, která se pošle klientovi. |
| IsDebuggingEnabled | Logick | Získá, zda je povoleno ladění skriptů a kódu. |
| IsInAsyncPostback | Logick | Získá, zda je stránka aktuálně v asynchronním požadavku POST. |
| Objektem ProfileService | Správce ProfileService | Načte podrobnosti o proxy službě profilace ASP.NET, která se pošle klientovi. |
| Skripty | Kolekce&lt;odkaz na skript&gt; | Získá kolekci odkazů skriptu, které budou odeslány klientovi. |
| Služby | Služba&lt;kolekce – referenční informace&gt; | Získá kolekci odkazů proxy webových služeb, které budou odeslány klientovi. |
| SupportsPartialRendering | Logick | Získá, zda aktuální klient podporuje částečné vykreslování. Pokud tato vlastnost vrátí **hodnotu false**, pak všechny požadavky na stránky budou standardním zpětným voláním. |

Metody veřejného kódu:

| **Název metody** | **Textový** | **Popis** |
| --- | --- | --- |
| SetFocus (řetězec) | Šekem | Nastaví fokus klienta na určitý ovládací prvek, když se žádost dokončí. |

Následníky kódu:

| **Inteligentní** | **Popis** |
| --- | --- |
| &lt;AuthenticationService&gt; | Poskytuje podrobnosti o proxy službě ASP.NET Authentication Service. |
| &lt;ProfileService&gt; | Poskytuje podrobnosti o proxy serveru ke službě profilace ASP.NET. |
| Skripty &lt;&gt; | Poskytuje další odkazy na skripty. |
| &lt;ASP: ScriptReference&gt; | Označuje konkrétní odkaz na skript. |
| &lt;Service&gt; | Poskytuje další odkazy na webové služby, které budou mít generované třídy proxy. |
| &lt;ASP: ServiceReference&gt; | Označuje konkrétní odkaz na webovou službu. |

Ovládací prvek ScriptManager je základní jádro pro rozšíření ASP.NET AJAX. Poskytuje přístup ke knihovně skriptů (včetně rozsáhlého systému typů skriptů na straně klienta), podporuje částečné vykreslování a poskytuje rozsáhlou podporu pro další služby ASP.NET (například ověřování a profilování, ale také další webové služby). Ovládací prvek ScriptManager také poskytuje podporu globalizace a lokalizace pro klientské skripty.

## <a name="providing-alternative-and-supplemental-scripts"></a>Poskytování alternativních a doplňkových skriptů

I když rozšíření Microsoft ASP.NET 2,0 AJAX zahrnuje celý kód skriptu v edicích pro ladění i vydání jako prostředky vložené v odkazovaných sestaveních, vývojáři jsou zdarma pro přesměrování ovládacího prvku ScriptManager do přizpůsobených souborů skriptu a také k registraci další nezbytné skripty.

Chcete-li přepsat výchozí vazbu pro obvykle zahrnuté skripty (například ty, které podporují obor názvů Sys. WebForms a customing System), můžete se zaregistrovat pro událost `ResolveScriptReference` třídy ScriptManager. Při volání této metody má obslužná rutina události možnost změnit cestu k souboru skriptu. Správce skriptů pak pošle klientovi jinou nebo přizpůsobenou kopii skriptů.

Kromě toho mohou být odkazy na skripty (reprezentované `ScriptReference` třídou) zahrnuty programově nebo prostřednictvím značek. Provedete to tak, že programově upravíte `ScriptManager.Scripts` kolekci, nebo zahrňte `<asp:ScriptReference>` značky pod značku `<Scripts>`, která je podřízenou položkou první úrovně ovládacího prvku ScriptManager.

## <a name="custom-error-handling-for-updatepanels"></a>Vlastní zpracování chyb pro UpdatePanel

I když jsou aktualizace zpracovávány triggery určenými ovládacími prvky UpdatePanel, podpora pro zpracování chyb a vlastní chybové zprávy je zpracována instancí ovládacího prvku ScriptManager stránky. K tomu je potřeba vystavit událost, `AsyncPostBackError`, na stránku, která pak může poskytovat vlastní logiku zpracování výjimek.

Zavoláním události AsyncPostBackError můžete zadat vlastnost `AsyncPostBackErrorMessage`, která pak způsobí, že se po dokončení zpětného volání vyvolá okno s výstrahami.

Místo použití výchozího upozornění je možné také přizpůsobit na straně klienta. Například můžete chtít zobrazit přizpůsobený `<div>` prvek namísto výchozího modálního dialogového okna prohlížeče. V takovém případě můžete chybu zpracovat v klientském skriptu:

**Výpis 5: skript na straně klienta pro zobrazení vlastních chyb**

[!code-html[Main](understanding-partial-page-updates-with-asp-net-ajax/samples/sample4.html)]

Úplně jednoduše, výše uvedený skript zaregistruje zpětné volání s běhovým modulem AJAX na straně klienta pro po dokončení asynchronního požadavku. Pak zkontroluje, jestli se nahlásila chyba, a pokud ano, zpracuje podrobnosti a nakonec určí modul runtime, že chyba byla zpracována ve vlastním skriptu.

## <a name="globalization-and-localization-support"></a>Podpora globalizace a lokalizace

Ovládací prvek ScriptManager poskytuje rozsáhlou podporu pro lokalizaci řetězců skriptu a komponent uživatelského rozhraní. Toto téma je ale mimo rámec tohoto dokumentu White Paper. Další informace naleznete v dokumentu White Paper, podpora globalizace v rozšířeních ASP.NET AJAX.

## <a name="the-updatepanel-control"></a>Ovládací prvek UpdatePanel

## <a name="updatepanel-control-reference"></a>Odkaz na ovládací prvek UpdatePanel

Vlastnosti s povolenou značkou:

| **Název vlastnosti** | **Textový** | **Popis** |
| --- | --- | --- |
| Vlastnost ChildrenAsTriggers | bool | Určuje, zda podřízené ovládací prvky automaticky vyvolávají aktualizaci při zpětném odeslání. |
| RenderMode | Enum (Block, inline) | Určuje způsob, jakým se bude obsah vizuálně prezentovat. |
| Li UpdateMode nastavena | Enum (vždy, podmíněný) | Určuje, zda je prvek UpdatePanel vždy aktualizován během částečného vykreslení nebo zda je aktualizován pouze v případě, že je dosaženo triggeru. |

Vlastnosti pouze kódu:

| **Název vlastnosti** | **Textový** | **Popis** |
| --- | --- | --- |
| IsInPartialRendering | bool | Získá, zda objekt UpdatePanel podporuje částečné vykreslení pro aktuální požadavek. |
| ContentTemplate | Platnou ITemplate | Získá šablonu značek pro žádost o aktualizaci. |
| ContentTemplateContainer | Control | Získá programovou šablonu pro žádost o aktualizaci. |
| Aktivační procedury | UpdatePanel – Trigger triggeru | Získá seznam aktivačních událostí přidružených k aktuálnímu prvku UpdatePanel. |

Metody veřejného kódu:

| **Název metody** | **Textový** | **Popis** |
| --- | --- | --- |
| Update () | Šekem | Aktualizuje zadaný objekt UpdatePanel programově. Umožňuje serveru požadavek na aktivaci částečného vykreslování v jiném neaktivovaném prvku UpdatePanel. |

Následníky kódu:

| **Inteligentní** | **Popis** |
| --- | --- |
| &lt;ContentTemplate&gt; | Určuje kód, který má být použit k vykreslení výsledku částečného vykreslení. Podřízený objekt &lt;ASP:&gt;UpdatePanel |
| &lt;Triggery&gt; | Určuje kolekci ovládacích prvků *n* přidružených k aktualizaci tohoto prvku UpdatePanel. Podřízený objekt &lt;ASP:&gt;UpdatePanel |
| &lt;ASP: AsyncPostBackTrigger&gt; | Určuje aktivační událost, která vyvolá vykreslení částečné stránky pro daný prvek UpdatePanel. To může nebo nemusí být ovládací prvek jako následník objektu UpdatePanel. Členit na název události. Podřízený objekt &lt;triggery&gt;. |
| &lt;ASP: PostBackTrigger&gt; | Určuje ovládací prvek, který způsobí, že se celá stránka aktualizuje. To může nebo nemusí být ovládací prvek jako následník objektu UpdatePanel. Členit na objekt. Podřízený objekt &lt;triggery&gt;. |

Ovládací prvek `UpdatePanel` je ovládací prvek, který odděluje obsah na straně serveru, který se bude účastnit částečného vykreslování rozšíření AJAX. Neexistuje žádné omezení počtu ovládacích prvků UpdatePanel, které mohou být na stránce, a mohou být vnořeny. Každý prvek UpdatePanel je izolovaný, takže každý může pracovat nezávisle (můžete mít spuštěné dva prvky UpdatePanel současně a vykreslovat různé části stránky, nezávisle na postbacku stránky).

Ovládací prvek UpdatePanel primárně pracuje s triggery ovládacího prvku – ve výchozím nastavení jakýkoli ovládací prvek obsažený v `ContentTemplate` ovládacího prvku UpdatePanel, který vytváří postback, je zaregistrován jako Trigger ovládacího prvku UpdatePanel. To znamená, že UpdatePanel může pracovat s výchozími ovládacími prvky svázanými s daty (například GridView), s uživatelskými ovládacími prvky a mohou být naprogramovány do skriptu.

Ve výchozím nastavení, když je aktivováno částečné vykreslování stránky, budou všechny ovládací prvky UpdatePanel na stránce aktualizovány bez ohledu na to, zda ovládací prvky UpdatePanel definují triggery pro takovou akci. Například pokud jeden prvek UpdatePanel definuje ovládací prvek tlačítko a na něj je kliknuto, všechny ovládací prvky UpdatePanel na této stránce budou ve výchozím nastavení aktualizovány. Důvodem je, že ve výchozím nastavení je vlastnost `UpdateMode` ovládacího prvku UpdatePanel nastavena na hodnotu `Always`. Alternativně můžete nastavit vlastnost li UpdateMode nastavena na `Conditional`, což znamená, že se ovládací prvek UpdatePanel aktualizuje pouze v případě, že je dosaženo konkrétní triggeru.

## <a name="custom-control-notes"></a>Poznámky k vlastním ovládacím prvkům

UpdatePanel lze přidat do libovolného uživatelského ovládacího prvku nebo vlastního ovládacího prvku; Nicméně stránka, na které jsou zahrnuty tyto ovládací prvky, musí také obsahovat ovládací prvek ScriptManager s vlastností EnablePartialRendering nastavenou na **hodnotu true**.

Jedním ze způsobů, kterými se můžete při použití vlastních ovládacích prvků webu pořídit, je přepsat chráněnou metodu `CreateChildControls()` `CompositeControl` třídy. Díky tomu můžete vložit UpdatePanel mezi podřízenými prvky ovládacího prvku a vnějším světem, pokud určíte, že stránka podporuje částečné vykreslování; v opačném případě můžete podřízené ovládací prvky jednoduše navrstvit do kontejneru `Control` instance.

## <a name="updatepanel-considerations"></a>Předpoklady pro UpdatePanel

Objekt UpdatePanel funguje jako něco z černého pole a zabalí zpětná volání ASP.NET v rámci kontextu JavaScript XMLHttpRequest. Existují však významné důležité požadavky na výkon, a to s ohledem na chování a rychlost. Chcete-li pochopit, jak bude UpdatePanel fungovat, abyste se mohli lépe rozhodnout, kdy je jeho použití vhodné, měli byste prostudovat AJAX Exchange. V následujícím příkladu je použit existující web a aplikace Mozilla Firefox s rozšířením Firebug (Firebug zachytí data XMLHttpRequest).

Vezměte v úvahu formulář, který kromě jiného má pole PSČ, které má vyplnit pole město a stát ve formuláři nebo ovládacím prvku. Tento formulář nakonec shromažďuje informace o členství, včetně jména, adresy a kontaktní informace uživatele. V závislosti na požadavcích konkrétního projektu je potřeba vzít v úvahu spoustu důvodů návrhu.

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image11.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image10.png)

([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-partial-page-updates-with-asp-net-ajax/_static/image12.png))

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image14.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image13.png)

([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-partial-page-updates-with-asp-net-ajax/_static/image15.png))

V původní iteraci této aplikace byl ovládací prvek sestaven, který zahrnoval celé údaje o registraci uživatelů, včetně PSČ, města a státu. Celý ovládací prvek byl zabalen do prvku UpdatePanel a vyřazen do webového formuláře. Po zadání PSČ uživatelem aplikace UpdatePanel detekuje událost (odpovídající událost TextChanged v back-endu, buď zadáním triggerů, nebo pomocí vlastnosti vlastnost ChildrenAsTriggers nastavenou na hodnotu true). AJAX účtuje všechna pole v rámci prvku UpdatePanel zachycená FireBug (viz diagram na pravé straně).

Vzhledem k tomu, že snímek obrazovky indikuje, hodnoty z každého ovládacího prvku v rámci prvku UpdatePanel jsou dodány (v tomto případě jsou všechny prázdné) a také pole ViewState. Všechna ta, která je přes 9kb dat, se odešlou, když ve skutečnosti stačí jenom pět bajtů dat potřebných k provedení tohoto konkrétního požadavku. Odpověď je ještě více bloated: celkově se 57kb pošle klientovi, stačí aktualizovat textové pole a rozevírací pole.

Může být také důležité, abyste viděli, jak ASP.NET AJAX aktualizuje prezentaci. Část odpovědi žádosti o aktualizaci ovládacího prvku UpdatePanel se zobrazuje na levé straně v konzole Firebug. je to speciálně formulovaná řetězec oddělený pomocí kanálu, který je rozdělen skriptem klienta a poté znovu sestaven na stránce. Konkrétně ASP.NET AJAX nastaví vlastnost *InnerHtml* elementu HTML v klientovi, který reprezentuje váš prvek UpdatePanel. Když prohlížeč znovu vygeneruje model DOM, dojde v závislosti na množství informací, které je třeba zpracovat, k mírnému zpoždění.

Opětovné generování modelu DOM aktivuje několik dalších problémů:

[![](understanding-partial-page-updates-with-asp-net-ajax/_static/image17.png)](understanding-partial-page-updates-with-asp-net-ajax/_static/image16.png)

([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-partial-page-updates-with-asp-net-ajax/_static/image18.png))

- Pokud je fokus elementu HTML v rámci objektu UpdatePanel, ztratí se fokus. Pro uživatele, kteří stiskli klávesu TAB k ukončení poštovního směrovacího čísla, by tedy bylo k dispozici textové pole City (jeho další cíl). Jakmile však prvek UpdatePanel aktualizuje zobrazení, formulář již nemá fokus a stisknutí klávesy TAB začne zvýrazňovat prvky fokusu (například odkazy).
- Pokud je použit libovolný typ vlastního skriptu na straně klienta, který přistupuje k prvkům modelu DOM, odkazy zachované pomocí funkce mohou být po částečném zpětném odeslání nefunkční.

UpdatePanel nejsou určeny k zachycení všech řešení. Místo toho poskytují rychlé řešení pro určité situace, včetně vytváření prototypů, malých aktualizací ovládacích prvků a poskytování známého rozhraní pro ASP.NET vývojářů, kteří mohou být obeznámeni s modelem objektu .NET, ale menším způsobem s modelem DOM. V závislosti na scénáři aplikace může docházet k vyššímu výkonu.

- Zvažte použití PageMethods a JSON (JavaScript Object Notation) umožňuje vývojářům vyvolat statické metody na stránce, jako kdyby bylo volání webové služby vyvoláno. Vzhledem k tomu, že metody jsou statické, není nutné žádný stav; volající skriptu dodá parametry a výsledek je vrácen asynchronně.
- Zvažte použití webové služby a formátu JSON, pokud je třeba jeden ovládací prvek použít na několika místech v rámci aplikace. To znovu vyžaduje velmi málo zvláštní práci a pracuje asynchronně.

Zahrnutí funkcí přes webové služby nebo metody stránky obsahuje také nevýhody. První a nejpřednější vývojáři v ASP.NET obvykle většinou vytvářejí malé komponenty funkcí do uživatelských ovládacích prvků (soubory. ascx). Do těchto souborů nelze hostovat metody stránky. musí být hostovány v rámci skutečné třídy stránky ASPX. Webové služby, podobně, musí být hostované v rámci třídy. asmx. V závislosti na aplikaci může tato architektura porušovat jednu zásadu zodpovědnosti, protože funkce pro jednu komponentu je teď rozložená mezi dvě nebo víc fyzických komponent, které můžou mít jenom minimální nebo žádné soudržné vazby.

Nakonec, pokud aplikace vyžaduje, aby se UpdatePanel používaly, měly by vám pomoci při řešení potíží a údržbě v následujících pokynech.

- **Vnořovat UpdatePanels co nejmenší, nejen v jednotkách, ale i napříč jednotkami kódu.** Například mít UpdatePanel na stránce, která zabalí ovládací prvek, zatímco tento ovládací prvek také obsahuje UpdatePanel, který obsahuje jiný ovládací prvek, který obsahuje UpdatePanel, je vnoření mezi jednotkami. To pomáhá udržet jasné, které prvky by se měly aktualizovat, a zabraňuje neočekávaným aktualizacím podřízených prvků UpdatePanel.
- **Ponechte vlastnost *vlastnost ChildrenAsTriggers* nastavenou na hodnotu false a explicitně nastavte aktivované události.** Použití kolekce `<Triggers>` je mnohem jasný způsob, jak zpracovávat události a může zabránit neočekávanému chování, pomoci s úlohami údržby a vynucením vývojářů, aby se pro událost přinutili.
- **K dosažení funkčnosti použijte nejmenší možnou jednotku.** Jak je uvedeno v diskuzi za službu PSČ, zabalíte jenom minimální dobu na server, celkový počet zpracovaných položek a nároky na výměnu klientského serveru, což zlepšuje výkon.

## <a name="the-updateprogress-control"></a>Ovládací prvek UpdateProgress

## <a name="updateprogress-control-reference"></a>Odkaz na ovládací prvek UpdateProgress

Vlastnosti s povolenou značkou:

| **Název vlastnosti** | **Textový** | **Popis** |
| --- | --- | --- |
| AssociatedUpdate-PanelID | String | Určuje ID prvku UpdatePanel, na kterém by měl tento prvek UpdateProgress nahlásit. |
| Hodnotou DisplayAfter | Hmot | Určuje časový limit v milisekundách, než se tento ovládací prvek zobrazí po zahájení asynchronního požadavku. |
| DynamicLayout | bool | Určuje, zda je průběh vykreslen dynamicky. |

Následníky kódu:

| **Inteligentní** | **Popis** |
| --- | --- |
| &lt;objekt ProgressTemplate&gt; | Obsahuje sadu šablon ovládacího prvku pro obsah, který bude zobrazen s tímto ovládacím prvkem. |

Ovládací prvek UpdateProgress vám poskytne přehled o tom, jak zajistit, aby vaše uživatelé měli zájem o přenos na server. To může uživatelům pomoct vědět, že děláte něco, i když nemusí být zřejmé, zejména proto, že většina uživatelů se používá k aktualizaci stránky a zobrazení zvýraznění stavového řádku.

V podobě poznámky se ovládací prvky UpdateProgress mohou objevit kdekoli v hierarchii stránky. V případech, kdy je částečný postback inicializován z podřízeného prvku UpdatePanel (kde je objekt UpdatePanel vnořen v rámci jiného prvku UpdatePanel), postbacky, které spouštějí podřízenou třídu UpdatePanel, způsobí zobrazení šablon UpdateProgress pro podřízenou položku. UpdatePanel i nadřazený UpdatePanel. Pokud je však aktivační událost přímým podřízeným prvku nadřazeného prvku UpdatePanel, zobrazí se pouze šablony UpdateProgress přidružené k nadřazenému objektu.

## <a name="summary"></a>Přehled

Microsoft ASP.NET rozšíření AJAX jsou sofistikované produkty navržené tak, aby vám pomohla při snadnějším zpřístupnění webového obsahu a poskytování bohatšího uživatelského prostředí pro vaše webové aplikace. V rámci rozšíření ASP.NET AJAX jsou částečně viditelné ovládací prvky vykreslování stránky, včetně ovládacího prvku ScriptManager, UpdatePanel a ovládacích prvků UpdateProgress, některé z nejužitečnějších komponent sady Toolkit.

Komponenta ScriptManager integruje zřizování klientského JavaScriptu pro rozšíření a umožňuje různým serverovým a klientským součástem spolupracovat s minimálními investicemi na vývoj.

Ovládací prvek UpdatePanel je zjevné pole Magic-Markup v rámci objektu UpdatePanel může mít CodeBehind na straně serveru a neaktivuje aktualizaci stránky. Ovládací prvky UpdatePanel mohou být vnořené a mohou být závislé na ovládacích prvcích v jiných prvcích UpdatePanel. Ve výchozím nastavení ovládací prvky UpdatePanel zpracovávají jakékoli postbacky vyvolané jejich následnými ovládacími prvky, i když tuto funkci lze jemně vyladit, a to deklarativně nebo programově.

Při použití ovládacího prvku UpdatePanel by měli vývojáři vědět o dopadu na výkon, který by mohl potenciálně nastat. K potenciálním alternativám patří webové služby a metody stránky, i když návrh aplikace by měl být zvážen.

Ovládací prvek UpdateProgress umožňuje uživateli, aby věděli, že se Neignoruje, a že požadavek na pozadí bude pokračovat, zatímco stránka není v opačném případě bez jakýchkoli požadavků na reakci na vstup uživatele. Zahrnuje také možnost přerušit částečné vykreslování výsledků.

Tyto nástroje společně pomáhají vytvořit bohatou a bezproblémovou činnost pro uživatele a snížit tak pracovní postup tak, aby na serveru méně zjevné.

## <a name="bio"></a>Dostupnost

Scott Cate spolupracuje s webovými technologiemi Microsoftu od 1997 a je prezidentem myKB.com ([www.myKB.com](http://www.myKB.com)), kde se specializuje při psaní aplikací založených na ASP.NET zaměřené na softwarová řešení ve znalostní bázi Knowledge Base. Scott se dá kontaktovat e-mailem na [scott.cate@myKB.com](mailto:scott.cate@myKB.com) nebo jeho blogu na [ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [Next](understanding-asp-net-ajax-updatepanel-triggers.md)

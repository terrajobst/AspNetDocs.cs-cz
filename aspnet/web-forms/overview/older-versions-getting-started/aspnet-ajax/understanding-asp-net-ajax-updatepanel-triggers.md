---
uid: web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-updatepanel-triggers
title: Porozumění aktivačním událostem ASP.NET AJAX prvku | Microsoft Docs
author: scottcate
description: Při práci v editoru značek v aplikaci Visual Studio si můžete všimnout (z IntelliSense), že existují dva podřízené prvky ovládacího prvku UpdatePanel. Jedna z Wh...
ms.author: riande
ms.date: 03/12/2008
ms.assetid: faab8503-2984-48a9-8a40-7728461abc50
msc.legacyurl: /web-forms/overview/older-versions-getting-started/aspnet-ajax/understanding-asp-net-ajax-updatepanel-triggers
msc.type: authoredcontent
ms.openlocfilehash: b1cc869f373d4f8283b4d92af74707c3f11fef61
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78547451"
---
# <a name="understanding-aspnet-ajax-updatepanel-triggers"></a>Principy aktivačních událostí UpdatePanel technologie ASP.NET AJAX

[Scott Cate](https://github.com/scottcate)

[Stáhnout PDF](https://download.microsoft.com/download/C/1/9/C19A3451-1D14-477C-B703-54EF22E197EE/AJAX_tutorial02_Triggers_cs.pdf)

> Při práci v editoru značek v aplikaci Visual Studio si můžete všimnout (z IntelliSense), že existují dva podřízené prvky ovládacího prvku UpdatePanel. Jedním z nich je prvek Triggers, který určuje ovládací prvky na stránce (nebo uživatelský ovládací prvek, pokud používáte), které aktivují částečné vykreslení ovládacího prvku UpdatePanel, ve kterém je element umístěn.

## <a name="introduction"></a>Úvod

Technologie Microsoftu pro ASP.NET přináší objektově orientovaný a řízený programovací model a podílí se na nich s výhodami zkompilovaného kódu. Model zpracování na straně serveru má však několik nevýhod, které je součástí technologie, mnohé z nich lze řešit novými funkcemi obsaženými v rozšířeních Microsoft ASP.NET 3,5 AJAX. Tato rozšíření umožňují mnoho nových bohatých funkcí klienta, včetně částečného vykreslování stránek bez nutnosti úplné aktualizace stránky, možnosti přístupu k webovým službám prostřednictvím klientského skriptu (včetně rozhraní API pro profilaci ASP.NET) a rozsáhlého rozhraní API na straně klienta. Navrženo pro zrcadlení mnoha řídicích schémat, které jsou vidět v ASP.NET sadě ovládacích prvků na straně serveru.

Tento dokument White Paper prověřuje funkce triggerů XML rozhraní ASP.NET AJAX `UpdatePanel` komponenty. Triggery XML poskytují podrobnou kontrolu nad komponentami, které mohou způsobit částečné vykreslení pro konkrétní ovládací prvky UpdatePanel.

Tento dokument White Paper vychází z verze beta 2 .NET Framework 3,5 a Visual Studio 2008. Rozšíření ASP.NET AJAX, dříve jako sestavení, která cílí na ASP.NET 2,0, jsou nyní integrována do knihovny základních tříd .NET Framework. Tento dokument White Paper také předpokládá, že budete pracovat se sadou Visual Studio 2008, nikoli s nástrojem Visual Web Developer Express a bude poskytovat návody v závislosti na uživatelském rozhraní sady Visual Studio (i když budou výpisy kódu plně kompatibilní bez ohledu na vývojové prostředí).

## <a name="triggers"></a>*Triggery*

Aktivační události pro daný prvek UpdatePanel ve výchozím nastavení automaticky obsahují všechny podřízené ovládací prvky, které vyvolávají zpětné volání, včetně (například) ovládací prvky TextBox, které mají svou `AutoPostBack` vlastnost nastavenou na **hodnotu true**. Triggery ale mohou být také zahrnuty deklarativně pomocí značek; To se provádí v sekci `<triggers>` deklarace ovládacího prvku UpdatePanel. I když k aktivačním událostem lze získat přístup prostřednictvím vlastnosti kolekce `Triggers`, doporučuje se registrovat jakékoli částečné triggery vykreslení v době běhu (například pokud ovládací prvek není k dispozici v době návrhu) pomocí metody `RegisterAsyncPostBackControl(Control)` objektu ScriptManager pro vaši stránku v rámci události `Page_Load`. Mějte na paměti, že stránky jsou bezstavové, a proto byste tyto ovládací prvky měli znovu zaregistrovat při každém jejich vytvoření.

Automatické zahrnutí podřízených triggerů může být také zakázáno (takže podřízené ovládací prvky, které vytvářejí postbacky, nejsou automaticky spouštěny pomocí částečného vykreslení) nastavením vlastnosti `ChildrenAsTriggers` na **hodnotu false (NEPRAVDA**). To umožňuje největší flexibilitu při přiřazování, které konkrétní ovládací prvky mohou vyvolat vykreslování stránky, a je doporučeno, aby vývojář mohl na událost reagovat, nikoli v případě, že bude zpracovávat události, které mohou nastat.

Všimněte si, že když jsou ovládací prvky UpdatePanel vnořené, pokud je li UpdateMode nastavena nastaveno na **podmíněný**, pokud je podřízený prvek UpdatePanel aktivován, ale nadřazený objekt není, bude obnoven pouze podřízený prvek UpdatePanel. Pokud je však nadřazený prvek UpdatePanel aktualizován, pak bude podřízený prvek UpdatePanel také aktualizován.

## <a name="the-lttriggersgt-element"></a>*&lt;Trigger&gt; elementu*

Při práci v editoru značek v aplikaci Visual Studio si můžete všimnout (z IntelliSense), že existují dva podřízené prvky `UpdatePanel`ho ovládacího prvku. Nejčastěji používaný prvek je `<ContentTemplate>` prvek, který v podstatě zapouzdřuje obsah, který bude uložen na panelu aktualizace (obsah, pro který povolujeme částečné vykreslování). Druhý prvek je prvek `<Triggers>`, který určuje ovládací prvky na stránce (nebo uživatelský ovládací prvek, pokud používáte), které aktivují částečné vykreslení ovládacího prvku UpdatePanel, ve kterém &lt;Trigger&gt; elementu.

Element `<Triggers>` může obsahovat libovolný počet všech dvou podřízených uzlů: `<asp:AsyncPostBackTrigger>` a `<asp:PostBackTrigger>`. Oba přijmou dva atributy, `ControlID` a `EventName`a mohou určit kterýkoli ovládací prvek v rámci aktuální jednotky zapouzdření (například pokud se ovládací prvek UpdatePanel nachází v ovládacím prvku webového uživatele, neměli byste se pokoušet o odkaz na ovládací prvek na stránce, na které se uživatelský ovládací prvek nachází).

Element `<asp:AsyncPostBackTrigger>` je zvláště užitečný v tom, že může cílit na jakoukoli událost z ovládacího prvku, který existuje jako podřízený *objekt ovládacího prvku UpdatePanel v* jednotce zapouzdření, nikoli pouze ovládací prvek UpdatePanel, pod kterým je tato aktivační událost podřízená. Proto může být proveden jakýkoli ovládací prvek pro aktivaci částečné aktualizace stránky.

Podobně element `<asp:PostBackTrigger>` lze použít k aktivaci částečného vykreslování stránky, ale ten, který vyžaduje úplnou zpáteční cestu k serveru. Tento element Trigger lze také použít k vynucení zobrazení celé stránky, pokud by ovládací prvek jinak spouštěl částečnou vykreslování stránky (například, když ovládací prvek `Button` existuje v prvku `<ContentTemplate>` ovládacího prvku UpdatePanel). Znovu element PostBackTrigger může určit jakýkoli ovládací prvek, který je podřízeným ovládacím prvkem ovládacího prvku UpdatePanel v aktuální jednotce zapouzdření.

## <a name="lttriggersgt-element-reference"></a>*&gt; odkaz na element &lt;triggery*

*Následníky kódu:*

| **Tag** | **Popis** |
| --- | --- |
| &lt;ASP: AsyncPostBackTrigger&gt; | Určuje ovládací prvek a událost, které způsobí částečnou aktualizaci stránky ovládacího prvku UpdatePanel, který obsahuje tento odkaz triggeru. |
| &lt;ASP: PostBackTrigger&gt; | Určuje ovládací prvek a událost, které způsobí, že dojde k úplné aktualizaci stránky (úplná aktualizace stránky). Tato značka se dá použít k vynucení plné aktualizace, když ovládací prvek jinak aktivuje částečné vykreslování. |

## <a name="walkthrough-cross-updatepanel-triggers"></a>*Návod: triggery mezi různými UpdatePanel*

1. Vytvořte novou stránku ASP.NET s nastaveným objektem ScriptManager pro povolení částečného vykreslování. Přidat do této stránky dva prvky UpdatePanel – v prvním případě přidejte ovládací prvek popisek (Label1) a dva ovládací prvky tlačítka (Button1 a Button2). Button1 by měl vyslovit kliknout pro aktualizaci obou a Button2 by se mělo jednat o to, že tuto možnost můžete aktualizovat nebo něco na těchto řádcích. V druhém prvku UpdatePanel, zahrňte pouze ovládací prvek popisek (Label2), ale nastavte jeho vlastnost ForeColor na jinou hodnotu než výchozí, abyste ho rozlišili.
2. Nastavte vlastnost li UpdateMode nastavena obou značek UpdatePanel na **podmíněný**.

**Výpis 1: označení pro default. aspx:** 

[!code-aspx[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample1.aspx)]

1. V obslužné rutině události Click pro Button1 nastavte Label1. text a Label2. text na něco závislého na čase (například DateTime. Now. ToLongTimeString ()). Pro obslužnou rutinu události Click pro Button2 nastavte pouze Label1. text na hodnotu závislou na čase.

**Výpis 2: CodeBehind (oříznuto) v default.aspx.cs:** 

[!code-csharp[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample2.cs)]

1. Stisknutím klávesy F5 Sestavte a spusťte projekt. Všimněte si, že když kliknete na aktualizovat oba panely, oba popisky změní text; Když však kliknete na tlačítko Aktualizovat tento panel, pouze aktualizace Label1.

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image2.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image1.png)

([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-updatepanel-triggers/_static/image3.png))

## <a name="under-the-hood"></a>*Pod kapotou*

S využitím příkladu, který jsme právě nastavili, můžeme pohlížet na to, co ASP.NET AJAX dělá a jak funguje naše více panelů UpdatePanel. Abychom to mohli udělat, budeme pracovat s generovaným zdrojem HTML stránky a také s použitím rozšíření Mozilla Firefox s názvem FireBug – s ním můžeme snadno kontrolovat zpětná volání AJAX. Také použijeme Nástroj pro odrážející rozhraní .NET Lutz roeder. Oba tyto nástroje jsou volně dostupné online a dají se najít pomocí hledání v Internetu.

Zkoumání zdrojového kódu stránky ukazuje téměř nic z obyčejného. ovládací prvky UpdatePanel jsou vykresleny jako kontejnery `<div>` a je možné zobrazit prostředek skriptu, který je součástí `<asp:ScriptManager>`. K dispozici jsou také některé nové volání jazyka PageRequestManager specifická pro AJAX, která jsou interní pro knihovnu klientských skriptů AJAX. Nakonec uvidíme dva kontejnery UpdatePanel – jeden s vykreslenými `<input>` tlačítky s těmito dvěma ovládacími prvky `<asp:Label>` vykreslenými jako kontejnery `<span>`. (Pokud zkontrolujete stromovou strukturu modelu DOM v FireBug, všimnete si, že popisky jsou ztlumené, aby označovaly, že nevytvářejí viditelný obsah).

Klikněte na tlačítko Aktualizovat tento panel a Všimněte si, že se hlavní UpdatePanel bude aktualizovat s aktuálním časem serveru. V FireBug klikněte na kartu konzola, abyste mohli žádost kontrolovat. Nejprve prověřte parametry žádosti POST:

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image5.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image4.png)

([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-updatepanel-triggers/_static/image6.png))

Všimněte si, že ovládací prvek UpdatePanel indikuje kód AJAX na straně serveru, který přesně vyvolal řídicí strom pomocí parametru ScriptManager1: `Button1` ovládacího prvku `UpdatePanel1`. Nyní klikněte na tlačítko Aktualizovat oba panely. Pak se podíváme na odpověď, v řetězci se zobrazí řada proměnných, které jsou odděleny kanálem. Konkrétně se zobrazí nejvyšší prvek UpdatePanel, `UpdatePanel1`, má celý kód HTML odeslaný do prohlížeče. Knihovna klientského skriptu AJAX nahrazuje původní obsah HTML pomocí nového obsahu prostřednictvím vlastnosti `.innerHTML`, a proto Server odesílá změněný obsah ze serveru jako kód HTML.

Nyní klikněte na tlačítko Aktualizovat oba panely a prověřte výsledky ze serveru. Výsledky jsou velmi podobné – oba UpdatePanel dostávají ze serveru nový kód HTML. Stejně jako u předchozího zpětného volání je odeslán další stav stránky.

Jak vidíte, protože není k provedení zpětného vyhledávání v AJAX k dispozici žádný speciální kód, knihovna skriptů klienta AJAX dokáže zachytit postbacky formuláře bez jakéhokoli dalšího kódu. Serverové ovládací prvky automaticky využívají JavaScript, takže se automaticky neodesílají formuláře – ASP.NET automaticky vloží kód pro ověřování a stav formuláře, a to především pomocí automatického zahrnutí prostředků skriptu, třídy PostBackOptions a třídy ClientScriptManager.

Například zvažte ovládací prvek CheckBox; Prověřte třídu zpětného překladu v rozhraní .NET reflektor. Chcete-li to provést, zajistěte, aby bylo sestavení System. Web otevřeno, a přejděte na třídu `System.Web.UI.WebControls.CheckBox` a otevřete metodu `RenderInputTag`. Vyhledejte podmíněný objekt, který kontroluje vlastnost `AutoPostBack`:

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image8.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image7.png)

([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-updatepanel-triggers/_static/image9.png))

Je-li na ovládacím prvku `CheckBox` povoleno automatické zpětné odeslání (prostřednictvím vlastnosti reASP.NET), výsledná `<input>` značka je proto vykreslena pomocí skriptu pro zpracování událostí ve svém atributu `onclick`. Zachycení formuláře odesláním umožňuje, aby bylo ASP.NET AJAX vloženo na stránku nerušivé, což pomáhá zabránit jakýmkoli případným změnám, které by mohly nastat při použití pravděpodobně nepřesné náhrady řetězce. Kromě toho umožňuje *jakémukoli* vlastnímu ovládacímu prvku ASP.NET využít sílu ASP.NET AJAX bez jakéhokoli dalšího kódu pro podporu jeho použití v kontejneru UpdatePanel.

Funkce `<triggers>` odpovídají hodnotám inicializovaným v volání PageRequestManager pro \_updateControls (Všimněte si, že knihovna skriptů klienta ASP.NET AJAX používá konvenci, že metody, události a názvy polí začínající podtržítkem jsou označeny jako interní a nejsou určeny pro použití vně samotné knihovny). Díky tomu můžeme sledovat, které ovládací prvky jsou určeny k tomu, aby způsobily zpětná volání AJAX.

Řekněme například, že na stránku přidáte dva další ovládací prvky, které ponechají jeden ovládací prvek mimo prvky UpdatePanel a opouštíte ho v rámci prvku UpdatePanel. Přidáme ovládací prvek CheckBox v horním prvku UpdatePanel a vyřaďte objekt DropDownList s řadou barev definovaných v seznamu. Toto je nový kód:

**Výpis 3: nový kód**

[!code-aspx[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample3.aspx)]

A tady je nový kód na pozadí:

**Výpis 4: CodeBehind**

[!code-csharp[Main](understanding-asp-net-ajax-updatepanel-triggers/samples/sample4.cs)]

Nápadem na této stránce je, že rozevírací seznam vybere jednu ze tří barev k zobrazení druhého popisku, zda zaškrtávací políčko určuje, zda je tučné a zda popisky zobrazují datum i čas. Zaškrtávací políčko by nemělo způsobit aktualizaci AJAX, ale rozevírací seznam by měl, i když není v ovládacím prvku UpdatePanel.

[![](understanding-asp-net-ajax-updatepanel-triggers/_static/image11.png)](understanding-asp-net-ajax-updatepanel-triggers/_static/image10.png)

([Kliknutím zobrazíte obrázek v plné velikosti.](understanding-asp-net-ajax-updatepanel-triggers/_static/image12.png))

Jak je znázorněno na obrázku výše, bylo kliknutí na tlačítko poslední na pravé tlačítko Aktualizovat tento panel, což aktualizovalo horní čas nezávisle na nejnižším čase. Datum bylo také přepnuto mezi kliknutím, protože datum je viditelné v dolním popisku. Nakonec je barva dolního popisku: aktualizovala se z poslední doby, než je text popisku, který ukazuje, že je stav ovládacího prvku důležitý, a uživatelé očekávají, že budou zachovány prostřednictvím zpětného volání AJAX. Čas se *ale*neaktualizoval. Čas byl automaticky znovu vyplněný po trvalosti pole \_\_VIEWSTATE stránky, která je interpretována modulem runtime ASP.NET při opětovném vykreslování ovládacího prvku na serveru. Kód serveru ASP.NET AJAX nerozpozná, v jakých metodách se mění stav ovládacích prvků. jednoduše se znovu naplní ze stavu zobrazení a pak spustí události, které jsou vhodné.

Mělo by být navázáno, ale čas, který byl inicializován během události\_načítání stránky, byl čas správně zvýšen. V důsledku toho by vývojáři měli být přistupují opatrněi, že se během příslušných obslužných rutin událostí spouští příslušný kód, a vyhněte se použití stránky\_načíst, když bude obslužná rutina události ovládacího prvku vhodná.

## <a name="summary"></a>Souhrn

Ovládací prvek UpdatePanel rozšíření ASP.NET AJAX je univerzální a může využít řadu metod pro identifikaci řídicích událostí, které by měly způsobit aktualizaci. Podporuje automatické aktualizace svými podřízenými ovládacími prvky, ale může také reagovat na události řízení jinde na stránce.

Chcete-li snížit potenciál pro zatížení serveru, je doporučeno, aby vlastnost `ChildrenAsTriggers` ovládacího prvku UpdatePanel byla nastavena na hodnotu `false`a aby byly události místo zahrnuty ve výchozím nastavení. To také brání jakýmkoli nepotřebným událostem v tom, že způsobují potenciálně nežádoucí účinky, včetně ověření a změny vstupních polí. Tyto typy chyb může být obtížné izolovat, protože se stránka aktualizuje transparentně na uživatele a příčina může být proto okamžitě zřejmá.

Prozkoumáním vnitřních pracovních segmentů modelu zachycení formuláře ASP.NET AJAX jsme dokázali určit, že používá rozhraní, které už poskytuje ASP.NET. V takovém případě zachovává maximální kompatibilitu s ovládacími prvky navrženými pomocí stejné architektury a intrudes na všech dalších JavaScriptu napsaných pro stránku.

## <a name="bio"></a>Bio

Rob Paveza je zkušeným vývojářem aplikací .NET na Terralever ([www.Terralever.com](http://www.terralever.com)), což je přední interaktivní podnik pro prodej v Tempe, AZ. Dá se získat na [robpaveza@gmail.com](mailto:robpaveza@gmail.com)a jeho blog se nachází na [http://geekswithblogs.net/robp/](http://geekswithblogs.net/robp/).

Scott Cate spolupracuje s webovými technologiemi Microsoftu od 1997 a je prezidentem myKB.com ([www.myKB.com](http://www.myKB.com)), kde se specializuje při psaní aplikací založených na ASP.NET zaměřené na softwarová řešení ve znalostní bázi Knowledge Base. Scott se dá kontaktovat e-mailem na [scott.cate@myKB.com](mailto:scott.cate@myKB.com) nebo jeho blogu na [ScottCate.com](http://ScottCate.com)

> [!div class="step-by-step"]
> [Předchozí](understanding-partial-page-updates-with-asp-net-ajax.md)
> [Další](understanding-asp-net-ajax-authentication-and-profile-application-services.md)

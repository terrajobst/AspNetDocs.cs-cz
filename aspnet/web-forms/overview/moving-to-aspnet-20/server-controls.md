---
uid: web-forms/overview/moving-to-aspnet-20/server-controls
title: Serverové ovládací prvky | Microsoft Docs
author: microsoft
description: ASP.NET 2,0 vylepšuje serverové ovládací prvky mnoha způsoby. V tomto modulu se podíváme na některé změny architektury, jak ASP.NET 2,0 a Visual Studio 200...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 43f6ac47-76fc-4cf7-8e9f-c18ce673dfd8
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/server-controls
msc.type: authoredcontent
ms.openlocfilehash: c02a633013f061c09141d4f98871848c011a799e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641440"
---
# <a name="server-controls"></a>Serverové ovládací prvky

od [Microsoftu](https://github.com/microsoft)

> ASP.NET 2,0 vylepšuje serverové ovládací prvky mnoha způsoby. V tomto modulu se podíváme na některé změny architektury, jak ASP.NET 2,0 a Visual Studio 2005 se řídí serverovými ovládacími prvky.

ASP.NET 2,0 vylepšuje serverové ovládací prvky mnoha způsoby. V tomto modulu se podíváme na některé změny architektury, jak ASP.NET 2,0 a Visual Studio 2005 se řídí serverovými ovládacími prvky.

## <a name="view-state"></a>Stav zobrazení

Primární Změna stavu zobrazení v ASP.NET 2,0 je výrazné snížení velikosti. Zvažte stránku s ovládacím prvkem kalendáře. Tady je stav zobrazení v ASP.NET 1,1.

[!code-css[Main](server-controls/samples/sample1.css)]

Nyní je stav zobrazení na stejné stránce v ASP.NET 2,0.

[!code-css[Main](server-controls/samples/sample2.css)]

To je poměrně významná změna. vzhledem k tomu, že se stav zobrazení přenese zpátky a zpátky přes vodič, může tato změna dát vývojářům výrazný nárůst výkonu. Snížení velikosti stavu zobrazení je z velké části vzhledem k tomu, že je interně zpracováváme. Pamatujte, že stav zobrazení je řetězec kódovaný v kódování Base64. Abychom lépe pochopili změnu stavu zobrazení v ASP.NET 2,0, Podívejme se na dekódování hodnot z výše uvedených příkladů.

Tady je dekódovat stav zobrazení 1,1:

[!code-css[Main](server-controls/samples/sample3.css)]

To může vypadat jako nesrozumitelné, ale tady je nějaký vzor. V ASP.NET 1. x jsme použili jednoduché znaky k identifikaci datových typů a hodnot s oddělovači pomocí &lt;&gt; znaků. Znak "t" v ukázce stavu zobrazení výše představuje S trojicí. S trojicí obsahuje dvojici ArrayLists ("l" představuje objekt ArrayList.) Jedna z těchto ArrayLists obsahuje Int32 ("i") s hodnotou 1 a druhá obsahuje další S trojicí. S trojicí obsahuje dvojici ArrayLists atd. Je důležité si pamatovat, že používáme Triplets, které obsahují páry, identifikujeme datové typy prostřednictvím písmen a používáme &lt; a &gt; znaky jako oddělovače.

V ASP.NET 2,0 vypadá dekódování stavu zobrazení trochu odlišně.

[!code-powershell[Main](server-controls/samples/sample4.ps1)]

Měli byste si všimnout výrazné změny v zobrazení stavu Dekódovatelné zobrazení. Tato změna má několik architektur architektury. Stav zobrazení v ASP.NET 1. x používá LosFormatter k serializaci dat. V 2,0 používáme novou třídu třídě ObjectStateFormatter. Tato třída byla navržena specificky pro pomoc při serializaci a deserializaci stavu zobrazení a stavu řízení. (Stav ovládacího prvku bude popsaný v další části.) Existuje mnoho výhod, kterými se mění metoda, pomocí které se provádí serializace a deserializace. Jedním z nejvýraznějších je fakt, že na rozdíl od LosFormatter, který používá modul TextWriter, třídě ObjectStateFormatter používá BinaryWriter. To umožňuje ASP.NET 2,0 uložit stav zobrazení řady bajtů namísto řetězců. Proveďte například celé číslo. V ASP.NET 1,1 je celé číslo, které je vyžadováno 4 bajty stavu zobrazení. V ASP.NET 2,0, které stejné celé číslo vyžaduje jenom 1 bajt. Bylo provedeno jiné vylepšení, které snižuje množství uloženého stavu zobrazení. Hodnoty DateTime jsou například nyní uloženy pomocí TickCount namísto řetězce.

Vzhledem k tomu, že všechny, které dostatečně nedostly, se na skutečnost, že jeden z největších uživatelů stavu zobrazení v 1. x, jednalo o ovládací prvky DataGrid a podobné. Hlavní nevýhodou ovládacích prvků, jako je například objekt DataGrid, kde je umístěn stav zobrazení, je, že často obsahuje velké množství opakujících se informací. V ASP.NET 1. x byly tyto opakující se informace jednoduše uloženy nad a znovu, což vedlo k bloated stavu zobrazení. V ASP.NET 2,0 používáme novou třídu IndexedString k ukládání těchto dat. Pokud se řetězec opakuje, stačí pouze uložit token pro IndexedString a index v běžící tabulce objektů IndexedString.

## <a name="control-state"></a>Stav ovládacího prvku

Jedním z hlavních rukojetí, které vývojáři mají se stavem zobrazení, byla velikost, kterou přidala do datové části HTTP. Jak už jsme uvedli, jedním z největších uživatelů stavu zobrazení je ovládací prvek DataGrid. Aby nedocházelo k obrovským hodnotám stavu zobrazení generovanému pomocí DataGrid, mnoho vývojářů jednoduše zakázal stav zobrazení pro tento ovládací prvek. Toto řešení bohužel nebylo vždy dobré. Stav zobrazení v ASP.NET 1. x obsahuje nejen data potřebná pro správné fungování ovládacího prvku. Obsahuje také informace týkající se stavu uživatelského rozhraní ovládacího prvku. To znamená, že pokud chcete povolit stránkování na DataGrid, musíte povolit stav zobrazení i v případě, že nepotřebujete všechny informace uživatelského rozhraní, které stav zobrazení obsahuje. Jedná se o scénář všech nebo žádného.

V ASP.NET 2,0 se stav ovládacího prvku vyřeší tím, že problém je úhledný prostřednictvím zavedení stavu ovládacího prvku. Stav ovládacího prvku obsahuje data, která jsou nezbytně nutná pro správné fungování ovládacího prvku. Na rozdíl od stavu zobrazení nemůže být stav ovládacího prvku zakázán. Proto je důležité, aby data uložená ve stavu řízení byla pečlivě kontrolována.

> [!NOTE]
> Stav ovládacího prvku je uložen společně se stavem zobrazení v poli \_\_VIEWSTATE skrytý formulář.

Toto video je názorný postup stavu zobrazení a stavu řízení.

![](server-controls/_static/image1.png)

[Otevření videa na celé obrazovce](server-controls/_static/state1.wmv)

Aby mohl serverový ovládací prvek číst a zapisovat do stavu ovládacího prvku, je nutné provést tři kroky.

## <a name="step-1-call-the-registerrequirescontrolstate-method"></a>Krok 1: volání metody RegisterRequiresControlState

Metoda RegisterRequiresControlState informuje ASP.NET, že ovládací prvek musí zachovat stav ovládacího prvku. Přebírá jeden argument typu Control, který je registrovaným ovládacím prvkem.

Je důležité si uvědomit, že registrace netrvala z požadavku na vyžádání. Proto tato metoda musí být volána u všech požadavků, pokud ovládací prvek bude uchovávat stav ovládacího prvku. Doporučuje se, aby se metoda volala v OnInit.

[!code-csharp[Main](server-controls/samples/sample5.cs)]

## <a name="step-2-override-savecontrolstate"></a>Krok 2: přepsání SaveControlState

Metoda SaveControlState ukládá změny stavu ovládacího prvku pro ovládací prvek od posledního odeslání zpět. Vrátí objekt představující stav ovládacího prvku.

## <a name="step-3-override-loadcontrolstate"></a>Krok 3: přepsání LoadControlState

Metoda LoadControlState načte uložený stav do ovládacího prvku. Metoda přijímá jeden argument typu Object, který obsahuje uložený stav ovládacího prvku.

## <a name="full-xhtml-compliance"></a>Úplné dodržování předpisů v XHTML

Každý webový vývojář ví o významu standardů ve webových aplikacích. Aby bylo možné spravovat vývojové prostředí založené na standardech, ASP.NET 2,0 je plně kompatibilní s NORMou XHTML. Proto se všechny značky vykreslí podle standardů XHTML v prohlížečích podporujících formát HTML 4,0 nebo vyšší.

Definice DOCTYPE v ASP.NET 1,1 byla následující:

[!code-html[Main](server-controls/samples/sample6.html)]

Výchozí definice DOCTYPE v ASP.NET 2,0 je následující:

[!code-html[Main](server-controls/samples/sample7.html)]

Zvolíte-li možnost, můžete změnit výchozí kompatibilitu XHTML prostřednictvím uzlu xhtmlConformance v konfiguračním souboru. Například následující uzel v souboru Web. config změní dodržování předpisů NORMou XHTML 1,0 Strict:

[!code-xml[Main](server-controls/samples/sample8.xml)]

Pokud zvolíte, můžete také nakonfigurovat ASP.NET tak, aby používal starší konfiguraci použitou v ASP.NET 1. x, a to následujícím způsobem:

[!code-xml[Main](server-controls/samples/sample9.xml)]

## <a name="adaptive-rendering-using-adapters"></a>Adaptivní vykreslování pomocí adaptérů

V ASP.NET 1. x obsahuje konfigurační soubor&gt; oddíl &lt;browserCaps, který vyplnil objekt HttpBrowserCapabilities. Tento objekt umožňuje vývojářům určit, které zařízení vytváří konkrétní požadavek, a správně vykreslit kód. V ASP.NET 2,0 model se vylepšil a teď používá novou třídu ControlAdapter. Třída ControlAdapter Přepisuje události v životním cyklu ovládacího prvku a řídí vykreslování ovládacích prvků na základě možností uživatelského agenta. Možnosti konkrétního uživatelského agenta jsou definovány souborem definice prohlížeče (soubor s příponou souboru. browser) uloženým v c:\Windows\Microsoft.NET\Framework\v2.0.\*\*\*\*složce \Config\browsers.

> [!NOTE]
> Třída ControlAdapter je abstraktní třída.

Podobně jako v části &lt;browserCaps&gt; v 1. x definiční soubor prohlížeče používá regulární výraz k analýze řetězce uživatelského agenta, aby bylo možné identifikovat žádající prohlížeč. Definuje konkrétní možnosti pro tohoto uživatelského agenta. ControlAdapter vykreslí ovládací prvek prostřednictvím metody Render. Proto pokud přepíšete metodu vykreslení, neměli byste volat vykreslování na základní třídě. V takovém případě může dojít k vykreslování dvakrát, jednou pro adaptér a pro samotný ovládací prvek.

## <a name="developing-a-custom-adapter"></a>Vývoj vlastního adaptéru

Pomocí dědění z ControlAdapter můžete vyvíjet vlastní adaptér. Kromě toho můžete zdědit z abstraktní třídy PageAdapter v případech, kdy je pro stránku vyžadován adaptér. Mapování ovládacích prvků na vlastní adaptér je provedeno prostřednictvím elementu &lt;controlAdapters&gt; v definičním souboru prohlížeče. Například následující kód XML z definičního souboru prohlížeče mapuje ovládací prvek nabídky na třídu MenuAdapter:

[!code-html[Main](server-controls/samples/sample10.html)]

Pomocí tohoto modelu je vývojářům ovládacího prvku velmi snadné cílit na konkrétní zařízení nebo prohlížeč. Je také poměrně jednoduché, aby měl vývojář úplnou kontrolu nad tím, jak stránky vykreslují na každé zařízení.

## <a name="per-device-rendering"></a>Vykreslování podle zařízení

Vlastnosti ovládacího prvku serveru v ASP.NET 2,0 lze zadat pomocí předpony specifické pro prohlížeč. Například kód níže změní text popisku v závislosti na tom, které zařízení slouží k procházení stránky.

[!code-aspx[Main](server-controls/samples/sample11.aspx)]

Pokud je stránka obsahující tento popisek procházena z aplikace Internet Explorer, zobrazí se v popisku text "probíhá procházení z Internet Exploreru". Když se stránka prochází z prohlížeče Firefox, zobrazí se v tomto popisku text "prochází z prohlížeče Firefox". Když se stránka prochází z libovolného jiného zařízení, zobrazí se zpráva, že procházíte z neznámého zařízení. Libovolnou vlastnost lze zadat pomocí této speciální syntaxe.

## <a name="setting-focus"></a>Nastavení fokusu

Vývojáři ASP.NET 1. x často žádají o nastavení počátečního zaměření na konkrétní ovládací prvek. Například na přihlašovací stránce je užitečné mít pole ID uživatele při prvním načtení stránky fokus získat fokus. V ASP.NET 1. x se tento postup vyžaduje pro zápis některých skriptů na straně klienta. I když je takový skript triviální úlohou, již není nutné v ASP.NET 2,0 s metodou SetFocus. Metoda SetFocus přijímá jeden argument určující ovládací prvek, který by měl získat fokus. Tento argument může být buď ID klienta ovládacího prvku jako řetězec, nebo název ovládacího prvku serveru jako objekt ovládacího prvku. Například chcete-li nastavit počáteční fokus na ovládací prvek TextBox s názvem txtUserID při prvním načtení stránky, přidejte následující kód pro\_načtení stránky:

[!code-csharp[Main](server-controls/samples/sample12.cs)]

--nebo

[!code-csharp[Main](server-controls/samples/sample13.cs)]

ASP.NET 2,0 používá obslužnou rutinu WebResource. axd (popsanou dříve) k vykreslení funkce na straně klienta, která nastavuje fokus. Název funkce na straně klienta je WebForm\_automatický fokus, jak je znázorněno zde:

[!code-html[Main](server-controls/samples/sample14.html)]

Alternativně můžete použít metodu fokusu pro ovládací prvek pro nastavení prvotního výběru na tento ovládací prvek. Metoda Focus je odvozena z třídy ovládacího prvku a je k dispozici pro všechny ovládací prvky ASP.NET 2,0. Je také možné nastavit fokus na konkrétní ovládací prvek, když dojde k chybě ověřování. Který bude popsaný v pozdějším modulu.

## <a name="new-server-controls-in-aspnet-20"></a>Nové serverové ovládací prvky v ASP.NET 2,0

Níže jsou uvedené nové serverové ovládací prvky v ASP.NET 2,0. Další podrobnosti o některých z nich najdete v pozdějších modulech.

## <a name="imagemap-control"></a>Ovládací prvek ImageMap

Ovládací prvek ImageMap umožňuje přidat hotspoty do obrázku, který může iniciovat zpětné odeslání nebo přejít na adresu URL. K dispozici jsou tři typy aktivních bodů; CircleHotSpot, RectangleHotSpot a PolygonHotSpot. Hotspoty se přidávají prostřednictvím editoru kolekce v sadě Visual Studio nebo programově v kódu. Pro kreslení hotspotů na obrázku není k dispozici žádné uživatelské rozhraní. Souřadnice a velikost nebo poloměr aktivního bodu musí být zadány deklarativně. V Návrháři není také vizuální reprezentace hotspotu. Pokud je hotspot nakonfigurovaný tak, aby přešel na adresu URL, adresa URL se zadá přes vlastnost NavigateUrl hotspotu. V případě back-hotspotu zpětného odeslání umožňuje vlastnost PostBackValue předat řetězec v příspěvku zpět, který lze načíst v kódu na straně serveru.

![Editor kolekce HotSpotů v sadě Visual Studio](server-controls/_static/image1.jpg)

**Obrázek 1**: Editor kolekce hotspotů v sadě Visual Studio

## <a name="bulletedlist-control"></a>Ovládací prvek BulletedList

Ovládací prvek BulletedList je seznam s odrážkami, který může být snadno vázaný na data. Seznam lze seřadit (číslovaný) nebo Neseřazený prostřednictvím vlastnosti BulletStyle. Každá položka v seznamu je reprezentována objektem ListItem.

![Ovládací prvek BulletedList v aplikaci Visual Studio](server-controls/_static/image1.gif)

**Obrázek 2**: ovládací prvek BulletedList v aplikaci Visual Studio

## <a name="hiddenfield-control"></a>Ovládací prvek HiddenField

Ovládací prvek HiddenField přidá skryté pole formuláře na stránku, což je hodnota, která je k dispozici v kódu na straně serveru. Obvykle se očekává, že hodnota skrytého pole formuláře zůstane beze změny mezi zpětnými odesláními. Uživatel se zlými úmysly však může změnit hodnotu před odesláním zpět. Pokud k tomu dojde, ovládací prvek HiddenField vyvolá událost ValueChanged. Pokud máte citlivé informace v ovládacím prvku HiddenField a chcete zajistit, že zůstane beze změny, měli byste zpracovat událost ValueChanged ve vašem kódu.

## <a name="fileupload-control"></a>Ovládací prvek nahrání souborů

Ovládací prvek nahrání souborů v ASP.NET 2,0 umožňuje nahrávat soubory na webový server prostřednictvím stránky ASP.NET. Tento ovládací prvek je poměrně podobný třídě ASP.NET 1. x HtmlInputFile s několika výjimkami. V ASP.NET 1. x se doporučuje, aby vlastnost PostedFile byla kontrolována na hodnotu null, aby bylo možné zjistit, zda byl soubor dobrý. Ovládací prvek nahrání do ASP.NET 2,0 přidává novou vlastnost HasFile, kterou můžete použít pro stejný účel a je to trochu efektivnější.

Vlastnost PostedFile je stále k dispozici pro přístup k objektu HttpPostedFile, ale některé funkce HttpPostedFile jsou nyní k dispozici vnitřně s ovládacím prvkem pro nahrání souborů. Například pro uložení nahraného souboru v ASP.NET 1. x zavoláte metodu SaveAs na objektu HttpPostedFile. Pomocí ovládacího prvku nahrání souborů v ASP.NET 2,0 byste volali metodu SaveAs na samotném ovládacím prvku pro nahrání souborů.

Další významná změna v chování 2,0 (a pravděpodobně nejvýznamnější změna) znamená, že již není nutné načíst celý nahraný soubor do paměti před jeho uložením. V souboru 1. x se všechny nahrané soubory uloží do paměti před zápisem na disk. Tato architektura zabraňuje nahrávání velkých souborů.

V ASP.NET 2,0 atribut requestLengthDiskThreshold prvku httpRuntime umožňuje nakonfigurovat, kolik kilobajtů je uchováváno ve vyrovnávací paměti v paměti před zápisem na disk.

**Důležité**: dokumentace MSDN (a dokumentace jinde) určuje, že tato hodnota je v bajtech (ne v kilobajtech) a že výchozí hodnota je 256. Hodnota je ve skutečnosti zadána v kilobajtech a výchozí hodnota je 80. Když zadáte výchozí hodnotu 80K, zajistíme, že vyrovnávací paměť nekončí na haldě velkých objektů.

## <a name="wizard-control"></a>Ovládací prvek Průvodce

Je poměrně běžné, že se ASP.NET vývojáři působit potíže a snaží se shromažďovat informace v řadě "stránky" pomocí panelů nebo přenášet ze stránky na stránku. Častěji než ne, Endeavor je frustrující jeden a časově náročné. Nový ovládací prvek Průvodce vyřeší problémy tím, že umožňuje lineární a nelineární kroky v rozhraní průvodce, se kterým uživatelé znají. Ovládací prvek Průvodce prezentuje vstupní formuláře v řadě kroků. Každý krok je konkrétní typ určený vlastností vlastnost StepType ovládacího prvku. K dispozici jsou následující typy kroků:

| **Typ kroku** | **Vysvětlení** |
| --- | --- |
| Autom. | Průvodce automaticky určí typ kroku na základě jeho pozice v rámci hierarchie kroku. |
| Start | První krok, který se často používá k zobrazení úvodního příkazu. |
| Krok | Běžný krok. |
| Dokončit | Poslední krok, který se obvykle používá k zobrazení tlačítka k dokončení průvodce. |
| Complete | Uvede zprávu oznamující úspěch nebo neúspěch. |

> [!NOTE]
> Ovládací prvek Průvodce sleduje svůj stav pomocí stavu ovládacího prvku ASP.NET. Proto může být vlastnost EnableViewState nastavena na hodnotu false bez jakýchkoli škod.

Toto video je návodem k ovládacímu prvku průvodce.

![](server-controls/_static/image2.png)

[Otevření videa na celé obrazovce](server-controls/_static/wizard1.wmv)

## <a name="localize-control"></a>Lokalizovat ovládací prvek

Ovládací prvek Localize je podobný ovládacímu prvku literálu. Nicméně ovládací prvek lokalizace má vlastnost **režimu** , která určuje, jakým způsobem je vykreslen kód, který je přidán do něj. Vlastnost Mode podporuje následující hodnoty:

| **Mode** | **Vysvětlení** |
| --- | --- |
| Transformace | Označení se transformuje podle protokolu prohlížeče, který požadavek odeslal. |
| Předávací | Značka je vykreslena tak, jak je. |
| Kódování | Kód, který je přidán do ovládacího prvku, je kódován pomocí HtmlEncode. |

## <a name="multiview-and-view-controls"></a>Ovládací prvky MultiView a View

Ovládací prvek MultiView funguje jako kontejner pro ovládací prvky zobrazení a ovládací prvek zobrazení slouží jako kontejner (podobně jako ovládací prvek panelu) pro jiné ovládací prvky. Každé zobrazení v ovládacím prvku MultiView je reprezentované jediným ovládacím prvkem zobrazení. První ovládací prvek zobrazení v prvku MultiView je zobrazení 0, druhý je zobrazení 1 atd. Zobrazení lze přepnout zadáním vlastnost ActiveViewIndex ovládacího prvku MultiView.

## <a name="substitution-control"></a>Ovládací prvek Substitution

Náhradní ovládací prvek se používá ve spojení s ukládáním do mezipaměti ASP.NET. V případech, kdy chcete využít výhod ukládání do mezipaměti, ale máte části stránky, které je třeba aktualizovat na každém požadavku (jinými slovy, části stránky, které jsou vyjmuty z ukládání do mezipaměti), přináší náhradní součást skvělé řešení. Ovládací prvek ve skutečnosti nevykresluje žádný výstup. Místo toho je svázán s metodou v kódu na straně serveru. Po vyžádání stránky je volána metoda a vrácený kód je vykreslen namísto ovládacího prvku Substitution.

Metoda, na kterou je ovládací prvek substituce svázán, je určena prostřednictvím vlastnosti **methodName** . Tato metoda musí splňovat následující kritéria:

- Musí se jednat o statickou metodu (Shared v jazyce VB).
- Přijímá jeden parametr typu HttpContext.
- Vrátí řetězec představující značku, která by měla nahradit ovládací prvek na stránce.

Ovládací prvek Substitution není schopen měnit žádný jiný ovládací prvek na stránce, ale má přístup k aktuálnímu objektu HttpContext prostřednictvím jeho parametru.

## <a name="gridview-control"></a>Ovládací prvek GridView

Ovládací prvek GridView je náhradou ovládacího prvku DataGrid. Tento ovládací prvek se podrobněji pokryje v pozdějším modulu.

## <a name="detailsview-control"></a>DetailsView – ovládací prvek

Ovládací prvek DetailsView umožňuje zobrazit jeden záznam ze zdroje dat a upravit nebo odstranit. Podrobněji se popisuje v pozdějším modulu.

## <a name="formview-control"></a>FormView – ovládací prvek

Ovládací prvek FormView slouží k zobrazení jednoho záznamu z datového zdroje ve konfigurovatelným rozhraní. Podrobněji se popisuje v pozdějším modulu.

## <a name="accessdatasource-control"></a>Ovládací prvek AccessDataSource

Ovládací prvek AccessDataSource se používá pro data navázání databáze Access. Podrobněji se popisuje v pozdějším modulu.

## <a name="objectdatasource-control"></a>Ovládací prvek ObjectDataSource

Ovládací prvek ObjectDataSource slouží k podpoře architektury se třemi úrovněmi, aby ovládací prvky mohly být vázány na data pro byznys objekt střední vrstvy na rozdíl od dvojrozměrného modelu, kde jsou ovládací prvky svázány přímo se zdrojem dat. V pozdějším modulu se podrobněji prodiskutuje.

## <a name="xmldatasource-control"></a>XmlDataSource Control

Ovládací prvek XmlDataSource se používá k vytvoření vazby dat na zdroj dat XML. Podrobněji se popisuje v pozdějším modulu.

## <a name="sitemapdatasource-control"></a>Ovládací prvek SiteMapDataSource

Ovládací prvek SiteMapDataSource poskytuje datovou vazbu pro ovládací prvky navigace na webu v závislosti na mapě webu. V pozdějším modulu se podrobněji prodiskutuje.

## <a name="sitemappath-control"></a>Ovládací prvek SiteMapPath

Ovládací prvek SiteMapPath zobrazí řadu navigačních odkazů, které se běžně označují jako cesty. Podrobněji se popisuje v pozdějším modulu.

## <a name="menu-control"></a>Ovládací prvek nabídky

Ovládací prvek nabídky zobrazí dynamické nabídky využívající technologii DHTML. Podrobněji se popisuje v pozdějším modulu.

## <a name="treeview-control"></a>TreeView – ovládací prvek

Ovládací prvek TreeView slouží k zobrazení hierarchického stromového zobrazení dat. Podrobněji se popisuje v pozdějším modulu.

## <a name="login-control"></a>Řízení přihlášení

Ovládací prvek Login poskytuje mechanismus pro přihlášení k webu. Podrobněji se popisuje v pozdějším modulu.

## <a name="loginview-control"></a>Ovládací prvek LoginView

Ovládací prvek LoginView umožňuje zobrazení různých šablon v závislosti na stavu přihlášení uživatele. Podrobněji se popisuje v pozdějším modulu.

## <a name="passwordrecovery-control"></a>Ovládací prvek PasswordRecovery

Ovládací prvek PasswordRecovery slouží k načítání zapomenutých hesel uživateli aplikace ASP.NET. Podrobněji se popisuje v pozdějším modulu.

## <a name="loginstatus"></a>Ovládací stavu přihlášení

Ovládací prvek ovládací stavu přihlášení zobrazí stav přihlášení uživatele. Podrobněji se popisuje v pozdějším modulu.

## <a name="loginname"></a>loginName

Ovládací prvek LoginName zobrazuje uživatelské jméno po přihlášení k aplikaci ASP.NET. Podrobněji se popisuje v pozdějším modulu.

## <a name="createuserwizard"></a>CreateUserWizard

Ovládacím CreateUserWizard je konfigurovatelný průvodce, který dává uživatelům možnost vytvořit si účet členství v ASP.NET pro použití v aplikaci ASP.NET. Podrobněji se popisuje v pozdějším modulu.

## <a name="changepassword"></a>Metodu ChangePassword

Ovládací prvek ChangePassword umožňuje uživatelům změnit heslo pro aplikaci ASP.NET. Podrobněji se popisuje v pozdějším modulu.

## <a name="various-webparts"></a>Různé webové části

ASP.NET 2,0 se dodává s různými Webové části. Tyto informace se budou pokrýt v pozdějším modulu.

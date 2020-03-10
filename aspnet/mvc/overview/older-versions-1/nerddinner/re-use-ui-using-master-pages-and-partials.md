---
uid: mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
title: Opětovné použití uživatelského rozhraní pomocí stránek předlohy a částečně | Microsoft Docs
author: microsoft
description: 'Krok 7: Prohlédněte si způsoby, jak můžeme použít "suchý princip" v našich šablonách zobrazení, aby se odstranila duplicita kódu, a to pomocí šablon částečného zobrazení a stránek předlohy.'
ms.author: riande
ms.date: 07/27/2010
ms.assetid: d4243a4a-e91c-4116-9ae0-5c08e5285677
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/re-use-ui-using-master-pages-and-partials
msc.type: authoredcontent
ms.openlocfilehash: 0b17cb6ac14b7f187bf1f175097a37907689d46e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580330"
---
# <a name="re-use-ui-using-master-pages-and-partials"></a>Opakované použití uživatelského rozhraní pomocí stránek předloh a částečných zobrazení

od [Microsoftu](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 7 bezplatného [kurzu aplikace "NerdDinner"](introducing-the-nerddinner-tutorial.md) , který vás provede procesem vytvoření malé, ale dokončené webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 7: Prohlédněte si způsoby, jak můžeme použít "suchý princip" v našich šablonách zobrazení k odstranění duplicity kódu pomocí šablon částečného zobrazení a stránek předlohy.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme vám postupovat podle [Začínáme s kurzy pro](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [hudební úložiště](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) MVC 3 nebo MVC.

## <a name="nerddinner-step-7-partials-and-master-pages"></a>NerdDinner krok 7: částečné a hlavní stránky

Jedna z návrhů filozofiemi ASP.NET MVC se vztahuje na princip "neopakuje se sami" (obvykle se označuje jako "SUCHá"). SUCHÝ návrh pomáhá eliminovat duplicity kódu a logiky, což výrazně usnadňuje sestavování a snazší správu aplikací.

V některých našich scénářích NerdDinner jsme už viděli vydaný suchý princip. Několik příkladů: naše logika ověřování je implementovaná v rámci naší modelové vrstvy, která umožňuje vyhovět v rámci scénářů úprav a vytváření v našem řadiči. znovu použijeme šablonu zobrazení "NotFound" v rámci metod Edit, Details a DELETE Action. používáme vzor pojmenovávání konvence se šablonami zobrazení, což eliminuje nutnost explicitního zadání názvu při volání pomocné metody View (); a znovu používáme třídu DinnerFormViewModel pro scénáře úprav a vytváření akcí.

Teď se podíváme na způsoby, jak můžeme použít "suchý princip" v našich šablonách zobrazení, aby bylo možné duplikaci kódu také eliminovat.

### <a name="re-visiting-our-edit-and-create-view-templates"></a>Opětovné návštěvy šablon zobrazení pro úpravy a vytváření

V současné době používáme dvě různé šablony zobrazení – Edit. aspx a Create. aspx – k zobrazení našeho uživatelského rozhraní formuláře večeře. Rychlé vizuální porovnání se vysvětlují, jak jsou podobné. V následujícím seznamu vypadá formulář pro vytváření vypadat takto:

![](re-use-ui-using-master-pages-and-partials/_static/image1.png)

A vypadá to, že náš formulář "Upravit" vypadá takto:

![](re-use-ui-using-master-pages-and-partials/_static/image2.png)

Nejedná se o rozdíl v tom, že existuje? Kromě textu nadpisu a záhlaví jsou ovládací prvky rozložení a vstup formuláře identické.

Pokud otevřete šablony zobrazení "Edit. aspx" a "vytvořit. aspx", zjistíme, že obsahují identické rozložení formuláře a vstupní kód pro řízení vstupu. Tato duplicita znamená, že je potřeba udělat změny dvakrát, kdykoli zavedeme nebo změníte novou vlastnost večeře – což není dobré.

### <a name="using-partial-view-templates"></a>Použití šablon částečného zobrazení

ASP.NET MVC podporuje možnost definovat "částečné zobrazení" šablony, které lze použít k zapouzdření logiky vykreslování zobrazení pro dílčí část stránky. "Částečné" představují užitečný způsob, jak definovat logiku vykreslování zobrazení jednou a pak ji znovu použít na více místech v rámci aplikace.

Abychom vám pomohli "vyschnout" náš upravit. aspx a vytvořit šablonu zobrazení. aspx, můžeme vytvořit částečnou šablonu zobrazení s názvem "DinnerForm. ascx", která zapouzdřuje rozložení formuláře a vstupní prvky společné do obou. To provedete tak, že kliknete pravým tlačítkem na náš adresář/Views/Dinners a vyberete příkaz nabídky přidat&gt;zobrazení:

![](re-use-ui-using-master-pages-and-partials/_static/image3.png)

Tím se zobrazí dialogové okno Přidat zobrazení. Podíváme se na nové zobrazení, které chceme vytvořit "DinnerForm", v dialogovém okně vyberte zaškrtávací políčko vytvořit částečné zobrazení a uveďte, že mu předáte DinnerFormViewModel třídu:

![](re-use-ui-using-master-pages-and-partials/_static/image4.png)

Po kliknutí na tlačítko Přidat vytvoří Visual Studio novou šablonu zobrazení "DinnerForm. ascx" pro nás v adresáři "\Views\Dinners".

Do naší nové šablony částečného zobrazení "DinnerForm. ascx" si pak můžeme zkopírovat nebo vložit duplicitní kód pro rozložení a zadání duplicitního formuláře z naší šablony zobrazení Edit. aspx/Create. aspx:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample1.aspx)]

Pak můžeme aktualizovat šablony zobrazení pro úpravy a vytváření, aby se volala částečná šablona DinnerForm a vyloučila se duplikace formuláře. To lze provést voláním HTML. RenderPartial ("DinnerForm") v našich šablonách zobrazení:

##### <a name="createaspx"></a>Create.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample2.aspx)]

##### <a name="editaspx"></a>Edit.aspx

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample3.aspx)]

Můžete explicitně kvalifikovat cestu částečné šablony, kterou chcete při volání HTML. RenderPartial (například: ~ zobrazení/večeře/DinnerForm. ascx). V našem kódu výše ale využíváme výhod vzoru pojmenování založeného na konvenci v rámci ASP.NET MVC a jako název částečného vykreslování pouze zadáte "DinnerForm". Když to uděláte, ASP.NET MVC bude nejdřív vypadat v adresáři zobrazení založeném na konvencích (pro DinnersController by to bylo/Views/Dinners). Pokud nenalezne částečnou šablonu, bude ji v adresáři/Views/Shared Hledat.

Pokud je volána metoda HTML. RenderPartial () s pouze názvem částečného zobrazení, ASP.NET MVC bude předána do částečného zobrazení stejného modelu a objekty ViewData slovníku používané šablonou volajícího zobrazení. Alternativně existují přetížené verze jazyka HTML. RenderPartial (), které umožňují předat alternativní objekt modelu nebo slovník ViewData pro použití částečného zobrazení. To je užitečné ve scénářích, kdy chcete pouze předat podmnožinu celého modelu/ViewModel.

| **Vedlejší téma: Proč &lt;%%&gt; místo &lt;% =%&gt;?** |
| --- |
| Jednou z drobných věcí, které jste si poznamenali u výše uvedeného kódu, je, že používáme &lt;%%&gt; bloku namísto &lt;% =%&gt; bloku při volání HTML. RenderPartial (). &lt;% =%&gt; bloky v ASP.NET označují, že vývojář chce vykreslit zadanou hodnotu (například: &lt;% = "Hello"%&gt; by vygeneroval "Hello"). &lt;%%&gt; Blocks místo toho naznačují, že vývojář chce spustit kód a že všechny vykreslené výstupy v nich musí být provedeny explicitně (například: &lt;% Response. Write ("Hello")%&gt;. Důvodem, že používáme &lt;%%&gt; bloku s nášm kódem HTML. RenderPartial, je, že metoda HTML. RenderPartial () nevrátí řetězec a místo toho použije výstup tohoto obsahu přímo do výstupního datového proudu šablony zobrazení volání. Provede to z důvodů efektivity výkonu a tím se vyhne nutnosti vytvořit objekt (potenciálně velmi rozsáhlý) dočasného objektu řetězce. Tím se snižuje využití paměti a zlepšuje se celková propustnost aplikací. Jednou z běžných chyb při použití HTML. RenderPartial () je zapomenout na konec volání přidat středník, pokud se nachází v rámci bloku&gt; &lt;%%. Například tento kód způsobí chybu kompilátoru: &lt;% HTML. RenderPartial ("DinnerForm")%&gt; místo toho musíte napsat: &lt;% HTML. RenderPartial ("DinnerForm"); %&gt; k tomu, protože bloky &lt;%%&gt; jsou samostatně obsahující příkazy kódu a při použití C# příkazů Code je nutné ukončit středníkem. |

### <a name="using-partial-view-templates-to-clarify-code"></a>Použití částečných šablon zobrazení k objasnění kódu

Vytvořili jsme šablonu částečného zobrazení "DinnerForm", aby se zabránilo duplikování logiky vykreslování zobrazení na více místech. Toto je nejběžnější důvod k vytvoření šablon částečného zobrazení.

Někdy je stále vhodné vytvářet částečná zobrazení i v případě, že jsou volána pouze na jednom místě. Velmi složité šablony zobrazení mohou být často mnohem snazší, pokud jsou extrahovány logiky pro vykreslení zobrazení a rozděleny do jedné nebo více dobře pojmenovaných částečných šablon.

Podívejte se například na následující fragment kódu ze souboru Web. Master v našem projektu (který brzy prohlížíme). Kód je relativně přímo předáván, protože logiku pro zobrazení odkazu na přihlášení nebo odhlášení v pravém horním rohu obrazovky je zapouzdřena v části "LogOnUserControl" (částečně):

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample4.aspx)]

Kdykoli zjistíte, že se snažíte pochopit kód HTML/kódu v rámci šablony zobrazení a, zvažte, zda by nebyl jasný, pokud byl některý z nich extrahován a refaktoroval do dobře pojmenovaných částečných zobrazení.

### <a name="master-pages"></a>Stránky předlohy

Kromě podpory částečných zobrazení podporuje ASP.NET MVC také možnost vytvářet šablony "Master Page", které lze použít k definování společného rozložení a HTML nejvyšší úrovně webu. Ovládací prvky zástupných symbolů obsahu je pak možné přidat na stránku předlohy k identifikaci nahraditelných oblastí, které mohou být přepsány nebo "vyplněny" zobrazeními. To poskytuje velmi účinný (a suchý) způsob, jak použít společné rozložení v rámci aplikace.

Ve výchozím nastavení mají nové projekty ASP.NET MVC automaticky přidaných předloh stránky. Tato stránka předlohy má název Web. Master a je umístěná ve složce \Views\Shared\:

![](re-use-ui-using-master-pages-and-partials/_static/image5.png)

Výchozí soubor Web. Master vypadá následovně. Definuje vnější HTML webu spolu s nabídkou pro navigaci v horní části. Obsahuje dva prvky nahraditelných zástupných symbolů obsahu – jeden pro název a druhý, kde by měl být primární obsah stránky nahrazen:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample5.aspx)]

Všechny šablony zobrazení, které jsme vytvořili pro naši aplikaci NerdDinner ("list", "Details", "Edit", "Create", "NotFound" atd.), byly založené na této šabloně site. Master. To je indikováno pomocí atributu "MasterPageFile", který byl přidán ve výchozím nastavení, do horní &lt;direktivy% @ Page%&gt;, když jsme vytvořili naše zobrazení pomocí dialogového okna Přidat zobrazení:

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample6.aspx)]

To znamená, že můžeme změnit obsah webu. Master a tyto změny se použijí automaticky a použijí se, když vygenerujeme kteroukoli z našich šablon zobrazení.

Pojďme aktualizovat oddíl záhlaví Web. Master tak, aby bylo záhlaví naší aplikace "NerdDinner" místo "Moje aplikace MVC". Pojďme také aktualizovat naši navigační nabídku tak, aby první karta byla "najít večeři" (zpracována metodou HomeController indexu () akce) a přidat novou kartu s názvem "host a večeře" (zpracováno metodou akce Create () DinnersController):

[!code-aspx[Main](re-use-ui-using-master-pages-and-partials/samples/sample7.aspx)]

Když ukládáme soubor Web. Master a aktualizujeme náš prohlížeč, uvidíme, že se změny v hlavičce zobrazí ve všech zobrazeních v rámci naší aplikace. Příklad:

![](re-use-ui-using-master-pages-and-partials/_static/image6.png)

A s adresou URL */Dinners/Edit/[ID]* :

![](re-use-ui-using-master-pages-and-partials/_static/image7.png)

### <a name="next-step"></a>Další krok

Částečné a hlavní stránky poskytují velmi flexibilní možnosti, které umožňují vyčistit zobrazení. Zjistíte, že vám pomohou vyhnout se duplicitám zobrazení obsahu a kódu a usnadnit čtení a údržbu šablon zobrazení.

Teď se podíváme na scénář výpisu, který jsme vytvořili dříve, a povolili jsme podporu škálovatelného stránkování.

> [!div class="step-by-step"]
> [Předchozí](use-viewdata-and-implement-viewmodel-classes.md)
> [Další](implement-efficient-data-paging.md)

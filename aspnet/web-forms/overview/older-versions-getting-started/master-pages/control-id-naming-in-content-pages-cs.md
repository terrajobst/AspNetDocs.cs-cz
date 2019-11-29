---
uid: web-forms/overview/older-versions-getting-started/master-pages/control-id-naming-in-content-pages-cs
title: Pojmenovávání ID ovládacích prvků naC#stránkách obsahu () | Microsoft Docs
author: rick-anderson
description: Ukazuje, jak ovládací prvky ContentPlaceHolder slouží jako názvový kontejner, a proto programově pracují s ovládacím prvkem (prostřednictvím FindControl)...
ms.author: riande
ms.date: 06/10/2008
ms.assetid: 1c7d0916-0988-4b4f-9a03-935e4b5af6af
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/control-id-naming-in-content-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: e849e5860dc988e112cc3a65d976c16ecdf77416
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74624382"
---
# <a name="control-id-naming-in-content-pages-c"></a>Pojmenovávání ID ovládacích prvků na stránkách obsahu (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_05_CS.zip) nebo [stažení PDF](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_05_CS.pdf)

> Ukazuje, jak ovládací prvky ContentPlaceHolder slouží jako názvový kontejner, a proto programově pracují s ovládacím prvkem (prostřednictvím FindControl). Podívá se na tento problém a alternativní řešení. Také popisuje, jak programově přistupovat k výsledné hodnotě ClientID.

## <a name="introduction"></a>Úvod

Všechny ovládací prvky ASP.NET serveru obsahují vlastnost `ID`, která jednoznačně identifikuje ovládací prvek a je prostředkem, pomocí kterého je ovládací prvek programově použit v třídě kódu na pozadí. Podobně prvky v dokumentu HTML mohou zahrnovat atribut `id`, který jednoznačně identifikuje prvek; Tyto hodnoty `id` jsou často používány v skriptu na straně klienta pro programové odkazy na konkrétní prvek jazyka HTML. V důsledku toho můžete předpokládat, že když je serverový ovládací prvek ASP.NET vykreslen do HTML, je použita jeho `ID` hodnota jako hodnota `id` vykresleného prvku HTML. To nemusí nutně znamenat případ, protože v určitých případech může být jeden ovládací prvek s jednou `ID` hodnotou ve vykresleném kódu vícekrát. Zvažte ovládací prvek GridView, který obsahuje TemplateField s ovládacím prvkem web popisku s `ID` hodnotou NázevVýrobku. Když je prvek GridView svázán s jeho zdrojem dat za běhu, je tento popisek opakován jednou pro každý řádek prvku GridView. Každý vykreslený popisek potřebuje jedinečnou `id` hodnotu.

Pro zpracování takových scénářů ASP.NET umožňuje, aby byly některé ovládací prvky označeny jako názvové kontejnery. Názvový kontejner slouží jako nový obor názvů `ID`. Všechny serverové ovládací prvky, které se zobrazují v rámci názvového kontejneru, mají svou vygenerovanou `id` hodnotu předponou `ID` ovládacího prvku názvového kontejneru. Například třídy `GridView` a `GridViewRow` jsou názvové kontejnery. V důsledku toho je ovládacímu prvku popisek, který je definován v prvku GridView TemplateField s `ID` NázevVýrobku, předána vykreslená `id` hodnota `GridViewID_GridViewRowID_ProductName`. Vzhledem k tomu, že *GridViewRowID* je pro každý řádek prvku GridView jedinečný, výsledné `id` hodnoty jsou jedinečné.

> [!NOTE]
> [Rozhraní`INamingContainer`](https://msdn.microsoft.com/library/system.web.ui.inamingcontainer.aspx) slouží k označení toho, že konkrétní serverový ovládací prvek ASP.NET by měl fungovat jako názvový kontejner. Rozhraní `INamingContainer` nevypíše žádné metody, které musí serverový ovládací prvek implementovat; místo toho se používá jako značka. Při generování vykresleného kódu, pokud ovládací prvek implementuje toto rozhraní, modul ASP.NET automaticky přihlásí svoji `ID` hodnotu na hodnoty atributu vykreslované `id`. Tento postup se podrobněji popisuje v kroku 2.

Pojmenování kontejnerů nemění pouze hodnotu atributu vygenerované `id`, ale také ovlivňuje způsob, jakým lze ovládací prvek programově odkazovat z třídy kódu na pozadí stránky ASP.NET. Metoda `FindControl("controlID")` se běžně používá pro programové odkazování webového ovládacího prvku. `FindControl` ale neprojde pomocí názvových kontejnerů. V důsledku toho nemůžete přímo použít metodu `Page.FindControl` pro referenční ovládací prvky v prvku GridView nebo jiném názvovém kontejneru.

Jak je možné mít surmised, stránky předloh a prvky ContentPlaceHolder jsou implementovány jako názvové kontejnery. V tomto kurzu prověříme, jak hlavní stránky ovlivňují prvky HTML `id` hodnoty a způsoby, jak programově odkazovat webové ovládací prvky v rámci stránky obsahu pomocí `FindControl`.

## <a name="step-1-adding-a-new-aspnet-page"></a>Krok 1: Přidání nové stránky ASP.NET

Abychom předvedli koncepty popsané v tomto kurzu, přidáme na náš web novou ASP.NET stránku. Vytvořte novou stránku obsahu s názvem `IDIssues.aspx` v kořenové složce, navázate ji na `Site.master` stránku předlohy.

![Přidejte stránku obsahu IDIssues. aspx do kořenové složky](control-id-naming-in-content-pages-cs/_static/image1.png)

**Obrázek 01**: Přidání stránky obsahu `IDIssues.aspx` do kořenové složky

Visual Studio automaticky vytvoří ovládací prvek obsahu pro každou ze čtyř prvků ContentPlaceHolder stránky předlohy. Jak je uvedeno v kurzu [*vícenásobné prvky ContentPlaceHolder a výchozí obsah*](multiple-contentplaceholders-and-default-content-cs.md) , pokud se ovládací prvek obsahu nezobrazuje, místo toho se vygeneruje výchozí obsah prvku ContentPlaceHolder stránky předlohy. Vzhledem k tomu, že `QuickLoginUI` a `LeftColumnContent` prvky ContentPlaceHolder obsahují vhodný výchozí kód pro tuto stránku, přejděte dopředu a odstraňte jejich odpovídající ovládací prvky obsahu z `IDIssues.aspx`. V tomto okamžiku by deklarativní označení stránky obsahu mělo vypadat takto:

[!code-aspx[Main](control-id-naming-in-content-pages-cs/samples/sample1.aspx)]

V kurzu [*zadání nadpisu, meta značek a dalších hlaviček HTML v kurzu hlavní stránky*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) jsme vytvořili vlastní třídu základní stránky (`BasePage`), která automaticky nakonfiguruje nadpis stránky, pokud není explicitně nastavený. Aby stránka `IDIssues.aspx` mohla tuto funkci využívat, třída kódu na pozadí stránky musí být odvozena od `BasePage` třídy (namísto `System.Web.UI.Page`). Upravte definici třídy kódu na pozadí tak, aby vypadala takto:

[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample2.cs)]

Nakonec aktualizujte soubor `Web.sitemap` tak, aby obsahoval položku pro tuto novou lekci. Přidejte prvek `<siteMapNode>` a nastavte jeho atributy `title` a `url` na hodnotu "problémy s pojmenování ID" a `~/IDIssues.aspx`v uvedeném pořadí. Po tom, co se přidávají změny `Web.sitemap` souboru, by měly vypadat podobně jako v následujícím příkladu:

[!code-xml[Main](control-id-naming-in-content-pages-cs/samples/sample3.xml)]

Jak ukazuje obrázek 2, nová položka mapy webu v `Web.sitemap` se okamžitě projeví v části lekce v levém sloupci.

![Oddíl lekce teď obsahuje odkaz na &quot;problémy s pojmenování ID ovládacího prvku&quot;](control-id-naming-in-content-pages-cs/_static/image2.png)

**Obrázek 02**: část lekce teď obsahuje odkaz na "problémy s pojmenování ID ovládacího prvku".

## <a name="step-2-examining-the-renderedidchanges"></a>Krok 2: prozkoumání vygenerovaných`ID`změn

Abychom lépe pochopili změny, které modul ASP.NET provede pro vygenerované `id` hodnoty serverových ovládacích prvků, přidáme na stránku `IDIssues.aspx` několik webových ovládacích prvků a potom se zobrazí vykreslené značky odeslané do prohlížeče. Konkrétně zadejte text "Zadejte prosím svůj věk", a potom klikněte na ovládací prvek TextBox (Web Control). Dále dolů na stránce přidejte webový ovládací prvek tlačítko a webový ovládací prvek popisek. Nastavte vlastnosti `ID` a `Columns` textového pole na `Age` a 3 v uvedeném pořadí. Nastavte vlastnosti `Text` a `ID` tlačítka na Odeslat a `SubmitButton`. Vymažte vlastnost `Text` popisku a nastavte její `ID` na `Results`.

V tomto okamžiku by deklarativní označení ovládacího prvku obsahu mělo vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](control-id-naming-in-content-pages-cs/samples/sample4.aspx)]

Obrázek 3 ukazuje stránku při zobrazení pomocí návrháře aplikace Visual Studio.

[![stránka obsahuje tři webové ovládací prvky: textové pole, tlačítko a popisek](control-id-naming-in-content-pages-cs/_static/image4.png)](control-id-naming-in-content-pages-cs/_static/image3.png)

**Obrázek 03**: stránka obsahuje tři webové ovládací prvky: textové pole, tlačítko a popisek ([kliknutím zobrazíte obrázek v plné velikosti](control-id-naming-in-content-pages-cs/_static/image5.png)).

Přejděte na stránku v prohlížeči a zobrazte zdroj HTML. Jak ukazuje následující kód, `id` hodnoty prvků HTML pro ovládací prvky TextBox, Button a Label jsou kombinací hodnot `ID` ovládacích prvků Web a `ID` hodnot názvových kontejnerů na stránce.

[!code-html[Main](control-id-naming-in-content-pages-cs/samples/sample5.html)]

Jak bylo popsáno dříve v tomto kurzu, jak hlavní stránka a její prvky ContentPlaceHolder slouží jako názvové kontejnery. V důsledku toho oba přispívají vykreslené `ID` hodnoty jejich vnořených ovládacích prvků. Převezměte `id` atribut TextBox, například: `ctl00_MainContent_Age`. Odvolání, že hodnota `ID` ovládacího prvku TextBox byla `Age`. Tato hodnota je předponou hodnoty `ID` ovládacího prvku ContentPlaceHolder, `MainContent`. Kromě toho je tato hodnota předpona `ID` hodnotou stránky předlohy `ctl00`. Čistý efekt je hodnota atributu `id` skládající se z `ID` hodnot stránky předlohy, ovládacího prvku ContentPlaceHolder a samotného textového pole.

Obrázek 4 znázorňuje toto chování. Chcete-li určit vykreslený `id` `Age` textového pole, začněte hodnotou `ID` ovládacího prvku TextBox, `Age`. Dále budete pracovat v hierarchii ovládacích prvků. V každém názvovém kontejneru (u těchto uzlů s broskvovou barvou) použijte předponu aktuálního vykresleného `id` pomocí `id`názvového kontejneru.

![Generované atributy ID jsou založené na hodnotách ID názvových kontejnerů.](control-id-naming-in-content-pages-cs/_static/image6.png)

**Obrázek 04**: vygenerované `id` atributy jsou založené na `ID` hodnotách názvových kontejnerů.

> [!NOTE]
> Jak jsme probrali, `ctl00` část vykresleného `id` atributu představuje hodnotu `ID` stránky předlohy, ale možná budete zajímat, jak tato `ID`ovaná hodnota byla. Nezadali jsme ho nikde na našem hlavním serveru nebo na stránce obsahu. Většina serverových ovládacích prvků na stránce ASP.NET se přidávají explicitně prostřednictvím deklarativního označení stránky. Ovládací prvek `MainContent` ContentPlaceHolder byl explicitně zadán v označení `Site.master`; `Age` textového pole bylo definováno `IDIssues.aspx`značku. Hodnoty `ID` pro tyto typy ovládacích prvků můžeme zadat pomocí okno Vlastnosti nebo z deklarativní syntaxe. Jiné ovládací prvky, například samotné hlavní stránky, nejsou definovány v deklarativní značce. V důsledku toho musí být jejich `ID` hodnoty automaticky vygenerovány pro nás. Modul ASP.NET nastaví za běhu hodnoty `ID` pro tyto ovládací prvky, jejichž ID nejsou explicitně nastavena. Používá vzor pojmenování `ctlXX`, kde *XX* je sekvenční zvýšení celočíselné hodnoty.

Vzhledem k tomu, že hlavní stránka slouží jako názvový kontejner, webové ovládací prvky definované na stránce předlohy také změnily hodnoty vygenerované `id` atributu. Například popisek `DisplayDate`, který jsme přidali na stránku předlohy v kurzu [*vytváření rozložení v rámci webu pomocí stránek*](creating-a-site-wide-layout-using-master-pages-cs.md) , má následující vykreslený kód:

[!code-html[Main](control-id-naming-in-content-pages-cs/samples/sample6.html)]

Všimněte si, že atribut `id` obsahuje hodnotu `ID` (`ctl00`) hlavní stránky a hodnotu `ID` webového ovládacího prvku popisek (`DateDisplay`).

## <a name="step-3-programmatically-referencing-web-controls-viafindcontrol"></a>Krok 3: programové odkazy na webové ovládací prvky prostřednictvím`FindControl`

Každý ovládací prvek serveru ASP.NET zahrnuje metodu `FindControl("controlID")`, která vyhledává následníky ovládacího prvku ovládacího prvku s názvem *controlID*. Pokud se takový ovládací prvek najde, vrátí se. Pokud se nenajde žádný vyhovující ovládací prvek, `FindControl` vrátí `null`.

`FindControl` je užitečná ve scénářích, kdy potřebujete mít přístup k ovládacímu prvku, ale nemáte k němu přímý odkaz. Při práci s datovými webovými ovládacími prvky, jako je například GridView, jsou ovládací prvky v rámci polí prvku GridView definovány jednou v deklarativní syntaxi, ale za běhu je vytvořena instance ovládacího prvku pro každý řádek prvku GridView. V důsledku toho existují ovládací prvky vygenerované za běhu, ale není k dispozici přímý odkaz z třídy kódu na pozadí. V důsledku toho je potřeba použít `FindControl` k programové práci s konkrétním ovládacím prvkem v rámci polí prvku GridView. (Další informace o použití `FindControl` pro přístup k ovládacím prvkům v rámci šablon webového ovládacího prvku data web naleznete v tématu [vlastní formátování na základě dat](../../data-access/custom-formatting/custom-formatting-based-upon-data-cs.md).) K tomuto stejnému scénáři dochází, když dynamicky přidáváte webové ovládací prvky do webového formuláře, téma popsané v tématu [vytváření dynamických uživatelských rozhraní pro zadávání dat](https://msdn.microsoft.com/library/aa479330.aspx).

Pro ilustraci použití metody `FindControl` pro hledání ovládacích prvků v rámci stránky obsahu vytvořte obslužnou rutinu události pro událost `Click` `SubmitButton`. V obslužné rutině události přidejte následující kód, který programově odkazuje na `Age` TextBox a `Results` popisek pomocí metody `FindControl` a poté zobrazí zprávu v `Results` na základě vstupu uživatele.

> [!NOTE]
> Samozřejmě nemusíme používat `FindControl` pro odkazování na ovládací prvky popisek a TextBox pro tento příklad. Můžeme na ně odkazovat přímo prostřednictvím hodnot `ID` vlastností. Používám `FindControl` k ilustraci toho, co se stane při použití `FindControl` ze stránky obsahu.

[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample7.cs)]

I když syntaxe použitá pro volání metody `FindControl` se mírně liší v prvních dvou řádcích `SubmitButton_Click`, jsou sémanticky ekvivalentní. Zajistěte, aby všechny ovládací prvky ASP.NET serveru zahrnovaly metodu `FindControl`. To zahrnuje třídu `Page`, ze které musí být odvozeny všechny třídy ASP.NET kódu na pozadí. Proto volání `FindControl("controlID")` je ekvivalentní volání `Page.FindControl("controlID")`, za předpokladu, že jste přepsali `FindControl` metodu ve třídě kódu na pozadí nebo ve vlastní základní třídě.

Po zadání tohoto kódu navštivte stránku `IDIssues.aspx` v prohlížeči, zadejte svůj věk a klikněte na tlačítko Odeslat. Po kliknutí na tlačítko Odeslat se `NullReferenceException` vyvolá (viz obrázek 5).

[Vyvolá se ![NullReferenceException.](control-id-naming-in-content-pages-cs/_static/image8.png)](control-id-naming-in-content-pages-cs/_static/image7.png)

**Obrázek 05**: je vyvolána `NullReferenceException` A ([kliknutím zobrazíte obrázek v plné velikosti](control-id-naming-in-content-pages-cs/_static/image9.png)).

Pokud nastavíte zarážku v obslužné rutině události `SubmitButton_Click`, uvidíte, že obě volání `FindControl` vrací hodnotu `null`. `NullReferenceException` je vyvolána, když se pokusíte o přístup k vlastnosti `Text` textového pole `Age`.

Problém je, že `Control.FindControl` pouze v podřízených objektech *hledání,* které jsou *ve stejném názvovém kontejneru*. Vzhledem k tomu, že stránka předlohy představuje nový kontejner pro pojmenování, volání `Page.FindControl("controlID")` nikdy permeates `ctl00`objektu hlavní stránky. (Pokud chcete zobrazit hierarchii ovládacích prvků, která zobrazuje objekt `Page` jako nadřazený objekt hlavní stránky `ctl00`, přečtěte si část zpět na obrázek 4.) Proto popisek `Results` a textové pole `Age` nebyly nalezeny a `ResultsLabel` a `AgeTextBox` jsou přiřazeny hodnoty `null`.

K této výzvě existují dvě alternativní řešení: můžeme přejít k podrobnostem, jednomu názvovému kontejneru v jednom okamžiku, na příslušný ovládací prvek. nebo můžeme vytvořit vlastní metodu `FindControl`, kterou permeates názvové kontejnery. Pojďme se podívat na každou z těchto možností.

### <a name="drilling-into-the-appropriate-naming-container"></a>Přechod do příslušného názvového kontejneru

Chcete-li použít `FindControl` pro odkazování na `Results` popisek nebo textové pole `Age`, musíme volat `FindControl` z nadřazeného ovládacího prvku ve stejném názvovém kontejneru. Jak ukazuje obrázek 4, ovládací prvek `MainContent` ContentPlaceHolder je jediným nadřazeným prvkem `Results` nebo `Age`, který se nachází v rámci stejného názvového kontejneru. Jinými slovy, volání metody `FindControl` z ovládacího prvku `MainContent`, jak je znázorněno v následujícím fragmentu kódu, správně vrátí odkaz na ovládací prvky `Results` nebo `Age`.

[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample8.cs)]

Nemůžeme ale pracovat s `MainContent` prvky ContentPlaceHolder ze třídy kódu na pozadí stránky obsahu pomocí výše uvedené syntaxe, protože prvek ContentPlaceHolder je definován na stránce předlohy. Místo toho je třeba použít `FindControl` k získání odkazu na `MainContent`. Nahraďte kód v obslužné rutině `SubmitButton_Click` události následujícími úpravami:

[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample9.cs)]

Pokud navštívíte stránku v prohlížeči, zadejte svůj věk a klikněte na tlačítko Odeslat, `NullReferenceException` je vyvolána. Pokud nastavíte zarážku v obslužné rutině události `SubmitButton_Click`, uvidíte, že k této výjimce dojde při pokusu o volání metody `FindControl` `MainContent` objektu. Objekt `MainContent` je `null`, protože metoda `FindControl` nemůže najít objekt s názvem "MainContent". Základní důvod je stejný jako u `Results` popisku a `Age` ovládacích prvků TextBox: `FindControl` spustí hledání z horní části hierarchie ovládacího prvku a proniká kontejnery pojmenování, ale `MainContent` ContentPlaceHolder je v rámci stránky předlohy, což je názvový kontejner.

Předtím, než můžeme použít `FindControl` k získání odkazu na `MainContent`, budeme nejdřív potřebovat odkaz na ovládací prvek stránky předlohy. Jakmile máme odkaz na hlavní stránku, můžeme získat odkaz na `MainContent` ContentPlaceHolder přes `FindControl` a odtud odkazuje na `Results` popisek a `Age` TextBox (znovu pomocí `FindControl`). Jak ale získáme odkaz na stránku předlohy? Kontrolou atributů `id` ve vykreslených značkách je zřejmé, že hodnota `ID` stránky předlohy `ctl00`. Proto můžeme použít `Page.FindControl("ctl00")` k získání odkazu na hlavní stránku a potom pomocí tohoto objektu získat odkaz na `MainContent`a tak dále. Následující fragment kódu znázorňuje tuto logiku:

[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample10.cs)]

I když tento kód bude určitě fungovat, předpokládá se, že automaticky vygenerovaný `ID` hlavní stránky bude vždycky `ctl00`. Není nikdy vhodné vytvářet předpoklady pro automaticky generované hodnoty.

Naštěstí je odkaz na stránku předlohy přístupný prostřednictvím vlastnosti `Master` `Page` třídy. Proto místo toho, aby bylo možné použít `FindControl("ctl00")` k získání odkazu na stránku předlohy, aby bylo možné získat přístup k `MainContent` ContentPlaceHolder, můžeme místo toho použít `Page.Master.FindControl("MainContent")`. Aktualizujte obslužnou rutinu události `SubmitButton_Click` pomocí následujícího kódu:

[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample11.cs)]

Tentokrát navštívíte stránku pomocí prohlížeče, zadáte svůj věk a kliknutím na tlačítko Odeslat zobrazíte zprávu v popisku `Results`, jak je očekáváno.

[![se stáří uživatele zobrazuje v popisku.](control-id-naming-in-content-pages-cs/_static/image11.png)](control-id-naming-in-content-pages-cs/_static/image10.png)

**Obrázek 06**: v popisku se zobrazí věk uživatele ([kliknutím zobrazíte obrázek v plné velikosti](control-id-naming-in-content-pages-cs/_static/image12.png)).

### <a name="recursively-searching-through-naming-containers"></a>Rekurzivní hledání pomocí názvových kontejnerů

Důvod, proč předchozí příklad kódu odkazoval na `MainContent` ovládací prvek ContentPlaceHolder ze stránky předlohy a následně ovládací prvky `Results` popisek a `Age` TextBox z `MainContent`, je, že metoda `Control.FindControl` vyhledává pouze v rámci názvového kontejneru *ovládacího prvku*. `FindControl` zůstat v rámci názvového kontejneru, má smysl ve většině scénářů, protože dva ovládací prvky ve dvou různých názvových kontejnerech mohou mít stejné `ID` hodnoty. Vezměte v úvahu případ prvku GridView, který definuje webový ovládací prvek popisku s názvem `ProductName` v rámci jednoho z jeho TemplateFields. Když jsou data svázána s prvku GridView za běhu, je pro každý řádek prvku GridView vytvořen `ProductName` popisek. Pokud `FindControl` prohledali všechny názvové kontejnery a volali `Page.FindControl("ProductName")`, která instance Label by měla `FindControl` vracet? Popisek `ProductName` v prvním řádku GridView? Ten v posledním řádku?

Proto *je ve*většině případů vhodné, `Control.FindControl` aby se ve většině případů ve většině případů vyhledala pouze názvový kontejner pro Existují však i jiné případy, jako je například jedna z nich, kde máme jedinečný `ID` ve všech názvových kontejnerech a chcete se vyhnout tomu, aby pečlivě odkazy na každý kontejner pro pojmenování v hierarchii ovládacích prvků pro přístup k ovládacímu prvku. `FindControl` variantě, která rekurzivně prohledává všechny názvové kontejnery, má smysl. .NET Framework bohužel tuto metodu neobsahuje.

Dobrá zpráva je, že můžeme vytvořit vlastní `FindControl` metodu, která rekurzivně vyhledá všechny názvové kontejnery. Ve skutečnosti se můžeme pomocí *rozšiřujících metod* zasměrovat na metodu `FindControlRecursive` `Control` třídy, aby mohla doprovázet svou stávající `FindControl` metodu.

> [!NOTE]
> Metody rozšíření jsou novou funkcí C# 3,0 a Visual Basic 9, což jsou jazyky dodávané s .NET Framework verzí 3,5 a sadou Visual Studio 2008. Krátké metody rozšíření umožňují vývojářům vytvořit novou metodu pro existující typ třídy prostřednictvím speciální syntaxe. Další informace o této užitečné funkci naleznete v článku můj článek a [rozšíření funkce základního typu pomocí rozšiřujících metod](http://aspnet.4guysfromrolla.com/articles/120507-1.aspx).

Chcete-li vytvořit metodu rozšíření, přidejte nový soubor do složky `App_Code` s názvem `PageExtensionMethods.cs`. Přidejte metodu rozšíření s názvem `FindControlRecursive`, která přebírá jako vstupní `string` parametr s názvem `controlID`. Aby metody rozšíření správně fungovaly, je nezbytné, aby třída samotné a její metody rozšíření byly označeny `static`. Kromě toho všechny metody rozšíření musí přijmout jako první parametr objekt typu, na který se metoda rozšíření vztahuje, a tento vstupní parametr musí předcházet klíčovým slovem `this`.

Přidejte následující kód do souboru třídy `PageExtensionMethods.cs` pro definování této třídy a metody rozšíření `FindControlRecursive`:

[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample12.cs)]

S tímto kódem se vrátíte na třídu kódu na pozadí `IDIssues.aspx` stránky a odkomentujte aktuální `FindControl` volání metody. Nahraďte je voláními `Page.FindControlRecursive("controlID")`. Co je na rozšiřujících metodách náročné, je, že se zobrazují přímo v rozevíracích seznamech technologie IntelliSense. Jak ukazuje obrázek 7, když zadáte Page a potom stiskněte perioda, je `FindControlRecursive` metoda obsažena v rozevíracím seznamu technologie IntelliSense spolu s jinými metodami `Control` třídy.

[v rozevíracích seznamech technologie IntelliSense jsou zahrnuté rozšiřující metody ![.](control-id-naming-in-content-pages-cs/_static/image14.png)](control-id-naming-in-content-pages-cs/_static/image13.png)

**Obrázek 07**: rozšiřující metody jsou obsaženy v rozevíracích seznamech technologie IntelliSense ([kliknutím zobrazíte obrázek v plné velikosti](control-id-naming-in-content-pages-cs/_static/image15.png)).

Do obslužné rutiny události `SubmitButton_Click` zadejte následující kód a potom ho otestujte na stránce, zadáním věku a kliknutím na tlačítko Odeslat. Jak je znázorněno na obrázku 6, výsledný výstup bude zpráva "jste si stáří let stará!"

[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample13.cs)]

> [!NOTE]
> Vzhledem k C# tomu, že rozšiřující metody jsou v 3,0 a Visual Basic 9 nové, pokud používáte Visual Studio 2005, nemůžete použít rozšiřující metody. Místo toho budete muset implementovat metodu `FindControlRecursive` do pomocné třídy. [Rick Strahl](http://www.west-wind.com/WebLog/default.aspx) obsahuje takový příklad v blogovém příspěvku, [ASP.NET Maser stránky a `FindControl`](http://www.west-wind.com/WebLog/posts/5127.aspx).

## <a name="step-4-using-the-correctidattribute-value-in-client-side-script"></a>Krok 4: použití správné hodnoty atributu`id`v skriptu na straně klienta

Jak je uvedeno v tomto kurzu, je často atribut pro `id` vykreslení webového ovládacího prvku, který se používá v skriptu na straně klienta pro programové odkazování na konkrétní prvek HTML. Například následující JavaScript odkazuje na prvek HTML podle jeho `id` a poté zobrazí jeho hodnotu v modálním okně se zprávou:

[!code-csharp[Main](control-id-naming-in-content-pages-cs/samples/sample14.cs)]

Odvolání na stránkách ASP.NET, které neobsahují kontejner pro pojmenování, je atribut vykreslené `id` elementu HTML totožný s hodnotou vlastnosti `ID` webového ovládacího prvku. Z tohoto důvodu se nachází na kód `id` hodnoty atributu do kódu JavaScriptu. To znamená, že pokud víte, že chcete přistupovat k webovému ovládacímu prvku TextBox `Age` pomocí skriptu na straně klienta, udělejte to prostřednictvím volání `document.getElementById("Age")`.

Problém s tímto přístupem je, že při použití stránek předloh (nebo jiné názvové ovládací prvky kontejneru) není vykreslený `id` HTML synonymum s vlastností `ID` webového ovládacího prvku. Vaše první sklon může být navštívená stránka prostřednictvím prohlížeče a zobrazit zdroj, aby bylo možné určit skutečný atribut `id`. Jakmile znáte vygenerovanou `id` hodnotu, můžete ji vložit do volání `getElementById` pro přístup k elementu HTML, ke kterému potřebujete pracovat prostřednictvím skriptu na straně klienta. Tento přístup je méně, než je ideální, protože určité změny v hierarchii ovládacího prvku stránky nebo změny `ID` vlastností ovládacích prvků pro pojmenování změní výsledný `id` atribut, čímž dojde k porušení kódu JavaScriptu.

Dobrá zpráva je, že hodnota atributu `id`, která je vykreslena, je přístupná v kódu na straně serveru prostřednictvím [vlastnosti`ClientID`](https://msdn.microsoft.com/library/system.web.ui.control.clientid.aspx)webového ovládacího prvku. Tuto vlastnost byste měli použít k určení hodnoty atributu `id` používaného v skriptu na straně klienta. Například pro přidání funkce JavaScriptu na stránku, která při volání zobrazí hodnotu `Age` TextBox v modálním okně zprávy, přidejte následující kód do obslužné rutiny události `Page_Load`:

[!code-javascript[Main](control-id-naming-in-content-pages-cs/samples/sample15.js)]

Výše uvedený kód vloží hodnotu vlastnosti ClientID `Age`ového pole do volání JavaScriptu pro `getElementById`. Pokud navštívíte tuto stránku v prohlížeči a zobrazíte zdroj HTML, najdete následující kód JavaScriptu:

[!code-html[Main](control-id-naming-in-content-pages-cs/samples/sample16.html)]

Všimněte si, jak se ve volání `getElementById`zobrazí správná hodnota atributu `id` `ctl00_MainContent_Age`. Vzhledem k tomu, že se tato hodnota počítá za běhu, funguje bez ohledu na pozdější změny v hierarchii ovládacích prvků stránky.

> [!NOTE]
> Tento příklad JavaScriptu pouze ukazuje, jak přidat funkci JavaScriptu, která správně odkazuje na element HTML vykreslený ovládacím prvkem serveru. Chcete-li použít tuto funkci, musíte vytvořit další JavaScript pro volání funkce při načtení dokumentu nebo v případě, že se některá konkrétní akce uživatele zobrazí. Další informace o těchto a souvisejících tématech najdete v článku [práce se skriptem na straně klienta](https://msdn.microsoft.com/library/aa479302.aspx).

## <a name="summary"></a>Přehled

Některé ovládací prvky ASP.NET serveru fungují jako názvové kontejnery, což ovlivňuje vygenerované `id` hodnoty atributu jejich podřízených ovládacích prvků a také rozsah ovládacích prvků canvassed metodou `FindControl`. S ohledem na stránky předlohy, samotná hlavní stránka a její ovládací prvky ContentPlaceHolder mají pojmenování kontejnerů. V důsledku toho musíme na stránce obsahu pomocí `FindControl`naprogramovat trochu více práce, které programově odkazují na ovládací prvky. V tomto kurzu jsme prozkoumali dva postupy: přechod do ovládacího prvku ContentPlaceHolder a volání jeho `FindControl` metody; a hromadnou implementaci `FindControl`, která rekurzivně prohledává všechny názvové kontejnery.

Kromě potíží na straně serveru zavedených názvové kontejnery, které se týkají odkazů na webové ovládací prvky, jsou také problémy na straně klienta. V případě absence názvových kontejnerů je hodnota vlastnosti `ID` webového ovládacího prvku a vykreslená `id` hodnota atributu jedna. Ale s přidáním názvového kontejneru, vykreslený `id` atribut zahrnuje jak hodnoty `ID` webového ovládacího prvku, tak i názvový kontejner (y) v původ hierarchie ovládacích prvků. Tyto aspekty pojmenování jsou neproblémové, pokud používáte vlastnost `ClientID` webového ovládacího prvku k určení hodnoty atributu vygenerované `id` ve skriptu na straně klienta.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [ASP.NET hlavní stránky a `FindControl`](http://www.west-wind.com/WebLog/posts/5127.aspx)
- [Vytváření uživatelských rozhraní pro zadávání dynamických dat](https://msdn.microsoft.com/library/aa479330.aspx)
- [Rozšíření funkce základního typu pomocí rozšiřujících metod](http://aspnet.4guysfromrolla.com/articles/120507-1.aspx)
- [Postupy: odkazování na obsah hlavní stránky ASP.NET](https://msdn.microsoft.com/library/xxwa0ff0.aspx)
- [Mater stránky: tipy, triky a depeše](http://www.odetocode.com/articles/450.aspx)
- [Práce s skriptem na straně klienta](https://msdn.microsoft.com/library/aa479302.aspx)

### <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 3,5 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Scott se dá kontaktovat [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Zack Novotný a Barnerjee. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com).

> [!div class="step-by-step"]
> [Předchozí](urls-in-master-pages-cs.md)
> [Další](interacting-with-the-master-page-from-the-content-page-cs.md)

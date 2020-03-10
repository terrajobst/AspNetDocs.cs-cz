---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
title: Představení webových stránek ASP.NET – vytvoření konzistentního rozložení | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se dozvíte, jak pomocí rozložení vytvořit konzistentní vzhled stránek na webu, který používá webové stránky ASP.NET. Předpokládá se, že jste dokončili...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: c85ec591-f8d7-4882-b763-de6ab9f3df7a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
msc.type: authoredcontent
ms.openlocfilehash: 678eb7089e95e3d221d6b2d82034a62aefa75757
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526689"
---
# <a name="introducing-aspnet-web-pages---creating-a-consistent-layout"></a>Představení webových stránek ASP.NET – vytvoření konzistentního rozložení

tím, že [FitzMacken](https://github.com/tfitzmac)

> V tomto kurzu se dozvíte, jak pomocí *rozložení* vytvořit konzistentní vzhled stránek na webu, který používá webové stránky ASP.NET. Předpokládá, že jste dokončili řadu [odstraněním dat databáze na webových stránkách ASP.NET](https://go.microsoft.com/fwlink/?LinkId=251584).
> 
> Naučíte se:
> 
> - Stránka rozložení.
> - Jak kombinovat stránky rozložení s dynamickým obsahem.
> - Jak předat hodnoty na stránku rozložení.

## <a name="about-layouts"></a>O rozloženích

Všechny stránky, které jste doposud vytvořili, mají kompletní, samostatné stránky. Všechny patří do stejné lokality, ale nemají žádné společné prvky ani standardní vzhled.

Většina lokalit má konzistentní vzhled a rozložení. Například pokud přejdete na web [Microsoft.com/web](https://www.microsoft.com/web/) a vyhledáte, uvidíte, že stránky všechny odpovídají celkovému rozložení a vizuálnímu motivu:

![Stránka Microsoft.com/web webu zobrazující rozložení záhlaví, navigační oblasti, oblasti obsahu a zápatí](layouts/_static/image1.png)

*Neefektivní* způsob, jak vytvořit toto rozložení, by bylo definovat záhlaví, navigační panel a zápatí samostatně na každé stránce. Pokaždé, když budete chtít stejný kód duplikovat. Pokud jste chtěli něco změnit (například aktualizovat zápatí), budete muset každou stránku změnit samostatně.

To je místo, kde jsou *stránky rozložení* součástí. Na webových stránkách ASP.NET můžete definovat stránku rozložení, která poskytuje celkový kontejner pro stránky na webu. Stránka rozložení může například obsahovat záhlaví, navigační oblast a zápatí. Stránka rozložení obsahuje zástupný symbol, kde se přechází hlavní obsah.

Pak můžete definovat jednotlivé stránky obsahu, které obsahují značky a kód pouze pro tuto stránku. Stránky obsahu nemusí být kompletní stránky HTML. nemusejí mít ani `<body>` element. Mají také řádek kódu, který oznamuje ASP.NET, na které stránce rozložení chcete zobrazit obsah. Tady je obrázek, který ukazuje, jak tento vztah funguje:

![Koncepční diagram, který zobrazuje dvě stránky obsahu a stránku rozložení, na které se vejdou](layouts/_static/image2.png)

Tato interakce je snadno srozumitelná, když ji vidíte v akci. V tomto kurzu změníte stránky filmů na použití rozložení.

## <a name="adding-a-layout-page"></a>Přidání stránky rozložení

Začnete vytvořením stránky rozložení, která definuje typické rozložení stránky pomocí záhlaví, zápatí a oblasti pro hlavní obsah. Na webu WebPagesMovies přidejte stránku CSHTML s názvem *\_layout. cshtml*.

Úvodní znak podtržítka (`_`) je významný. Pokud název stránky začíná podtržítkem, ASP.NET nebude přímo odesílat tuto stránku do prohlížeče. Tato konvence vám umožní definovat stránky, které jsou pro vaši lokalitu nutné, ale uživatelé by nemuseli žádat o přímý přístup.

Obsah stránky nahraďte následujícím:

[!code-html[Main](layouts/samples/sample1.html)]

Jak vidíte, tento kód je pouze HTML, který používá `<div>` prvky pro definování tří částí na stránce a další `<div>` elementu pro uložení tří částí. Zápatí obsahuje bitovou kopii kódu Razor: `@DateTime.Now.Year`, který vykreslí aktuální rok v tomto umístění stránky.

Všimněte si, že existuje odkaz na šablonu stylů s názvem *video. CSS*. Šablona stylů je místo, kde budou definovány podrobnosti fyzického rozložení prvků. Vytvoříte to za chvíli.

Jedinou neobvyklou funkcí na této stránce *\_layout. cshtml* je `@Render.Body()` čára. To je zástupný symbol, kde bude obsah přecházet, když je toto rozložení sloučeno s jinou stránkou.

## <a name="adding-a-css-file"></a>Přidání souboru. CSS

Upřednostňovaným způsobem, jak definovat skutečné uspořádání (to znamená, vzhled) prvků na stránce, je použití pravidel kaskádových šablon stylů (CSS). Proto vytvoříte soubor *. CSS* , který obsahuje pravidla pro nové rozložení.

V části WebMatrix vyberte kořen webu. Pak na kartě **soubory** na pásu karet klikněte na šipku pod tlačítkem **Nový** a pak klikněte na **Nová složka**.

![Možnost Nová složka v části nový na pásu karet.](layouts/_static/image3.png)

Pojmenujte nové *styly*složek.

![Pojmenování nové složky ' Styles '](layouts/_static/image4.png)

Uvnitř nové složky *stylů* vytvořte soubor s názvem *filmovés. CSS*.

![Vytváření nového souboru filmů. CSS](layouts/_static/image5.png)

Nahraďte obsah nového souboru *. CSS* následujícím způsobem:

[!code-css[Main](layouts/samples/sample2.css)]

V těchto pravidlech šablon stylů CSS nebudeme počítat s výjimkou dvou věcí. Jedním z nich je, že kromě nastavení písem a velikostí používají pravidla absolutní umístění k určení umístění záhlaví, zápatí a oblasti hlavního obsahu. Pokud se chystáte umístění v šablonách stylů CSS, můžete si přečíst kurz pro [umístění šablon stylů CSS](http://www.w3schools.com/css/css_positioning.asp) na webu w3schools.

Druhá Poznámka je, že v dolní části jsme zkopírovali pravidla stylů, která byla původně definována v souboru *Movies. cshtml* . Tato pravidla se použila v [úvodu k zobrazení dat pomocí ASP.NET na webové stránky](https://go.microsoft.com/fwlink/?LinkId=251580) , aby pomocné rutiny `WebGrid` vykreslily značky, které přidaly do tabulky pruhy. (Pokud budete používat soubor *. CSS* pro definice stylu, můžete také zadat pravidla stylu pro celou lokalitu v tomto umístění.)

## <a name="updating-the-movies-file-to-use-the-layout"></a>Aktualizace souboru filmů pro použití rozložení

Nyní můžete aktualizovat existující soubory na webu, aby používaly nové rozložení. Otevřete soubor *Movies. cshtml* . V horní části, jako první řádek kódu, přidejte následující:

[!code-csharp[Main](layouts/samples/sample3.cs)]

Stránka teď začíná tímto způsobem:

[!code-cshtml[Main](layouts/samples/sample4.cshtml?highlight=2)]

Tento jeden řádek kódu oznamuje ASP.NET, že když se stránka *videa* spustí, měla by se sloučit se souborem *\_layout. cshtml* .

Vzhledem k tomu, že soubor *Movies. cshtml* nyní používá stránku rozložení, můžete odebrat značku ze stránky *filmy. cshtml* , která je pořízena souborem *\_layout. cshtml* . `<!DOCTYPE>`, `<html>`a `<body>` otevírání a zavírání značek. Odbrat celý `<head>` prvek a jeho obsah, který obsahuje pravidla stylu pro mřížku, protože tato pravidla teď máte v souboru *. CSS* . I když jste na něm, změňte existující `<h1>` element na `<h2>` element; na stránce rozložení již existuje prvek `<h1>`. Změňte `<h2>` text na "vypsat filmy".

Obvykle byste nemuseli tyto změny na stránce obsahu provádět. Když zahájíte stránku s rozložením, vytvoříte stránky obsahu bez všech těchto prvků, které mají začít. V takovém případě však převádíte samostatnou stránku na jednu, která používá rozložení, takže existuje bit vyčištění.

Až budete hotovi, stránka *filmy. cshtml* bude vypadat následovně:

[!code-cshtml[Main](layouts/samples/sample5.cshtml)]

### <a name="testing-the-layout"></a>Testování rozložení

Nyní vidíte, jak vypadá rozložení. Ve WebMatrixu klikněte pravým tlačítkem na stránku *filmy. cshtml* a vyberte **Spustit v prohlížeči**. Když prohlížeč stránku zobrazí, vypadá to jako tato stránka:

![Stránka filmy vykreslená pomocí rozložení](layouts/_static/image6.png)

ASP.NET sloučil obsah stránky video. cshtml na stránku *\_layout. cshtml* , kde je `RenderBody` metoda. A samozřejmě stránku *\_layout. cshtml* odkazuje na soubor *. CSS* , který definuje vzhled stránky.

## <a name="updating-the-addmovie-page-to-use-the-layout"></a>Aktualizace stránky AddMovie pro použití rozložení

Výhodou pro výhody rozvržení je, že je můžete použít pro všechny stránky na webu. Otevřete stránku *AddMovie. cshtml* .

Můžete si uvědomit, že na stránce *AddMovie. cshtml* byla původně některá pravidla šablon stylů CSS, aby bylo možné definovat vzhled chybových zpráv ověřování. Vzhledem k tomu, že máte soubor *. CSS* pro váš web nyní, můžete tato pravidla přesunout do souboru *. CSS* . Odeberte je ze souboru *AddMovie. cshtml* a přidejte je do dolní části souboru *Movies. CSS* . Přesouváte následující pravidla:

[!code-css[Main](layouts/samples/sample6.css)]

Nyní proveďte stejné řazení změn v *AddMovie. cshtml* , které jste provedli pro *filmy. cshtml* – přidejte `Layout="~/_Layout.cshtml;` a odeberte kód HTML, který je nyní cizí. Změňte `<h1>` element na `<h2>`. Až budete hotovi, stránka bude vypadat jako v tomto příkladu:

[!code-cshtml[Main](layouts/samples/sample7.cshtml)]

Spusťte stránku. Nyní vypadá jako na tomto obrázku:

![Stránka Přidat filmy vykreslená pomocí rozložení](layouts/_static/image7.png)

Chcete provést podobné změny na stránkách v lokalitě – *EditMovie. cshtml* a *DeleteMovie. cshtml*. Než však provedete, můžete provést další změnu rozložení, které je trochu flexibilnější.

## <a name="passing-title-information-to-the-layout-page"></a>Předávání informací o názvu na stránku rozložení

Stránka *\_layout. cshtml* , kterou jste vytvořili, má `<title>` element, který je nastaven na "moji filmový web". Většina prohlížečů zobrazuje obsah tohoto prvku jako text na kartě:

![Element &lt;title&gt; stránky zobrazený na kartě prohlížeče](layouts/_static/image8.png)

Tyto informace o názvu jsou obecné. Řekněme, že chcete, aby byl text nadpisu pro aktuální stránku konkrétnější. (Text nadpisu se používá také vyhledávacími weby k určení toho, co stránka se chystá.) Můžete předat informace ze stránky obsahu, jako je například *filmy. cshtml* nebo *AddMovie. cshtml* , na stránku rozložení a pak tyto informace použít k přizpůsobení toho, co stránka rozložení vykreslí.

Otevřete znovu stránku *filmy. cshtml* . V kódu nahoře přidejte následující řádek:

[!code-csharp[Main](layouts/samples/sample8.cs)]

Objekt `Page` je k dispozici na všech stránkách *. cshtml* a je pro tento účel, totiž pro sdílení informací mezi stránkou a jejím rozložením.

Otevřete stránku *\_layout. cshtml* . Změňte element `<title>` tak, aby vypadal jako tento kód:

[!code-html[Main](layouts/samples/sample9.html)]

Tento kód vykresluje bez ohledu na to, zda je vlastnost `Page.Title` v daném umístění stránky.

Spusťte stránku *filmy. cshtml* . Tentokrát karta prohlížeč zobrazuje, co jste předali jako hodnotu `Page.Title`:

![Karta prohlížeče zobrazující nadpis, který se vytvořil dynamicky](layouts/_static/image9.png)

Pokud chcete, zobrazte zdroj stránky v prohlížeči. Můžete vidět, že `<title>` element je vykreslen jako `<title>List Movies</title>`.

> [!TIP] 
> 
> **Objekt Page**
> 
> Užitečnou funkcí `Page` je, že se jedná o dynamický objekt – vlastnost `Title` není pevným ani rezervovaným názvem. Pro hodnotu objektu `Page` můžete použít *libovolný* název. Například můžete snadno předat název pomocí vlastnosti s názvem `Page.CurrentName` nebo `Page.MyPage`. Jediným omezením je, že název musí dodržovat běžná pravidla pro to, které vlastnosti mohou být pojmenovány. (Například název nesmí obsahovat mezeru.)
> 
> Můžete předat libovolný počet hodnot pomocí objektu `Page`. Pokud jste chtěli předat informace o videu na stránku rozložení, mohli byste předat hodnoty pomocí typu `Page.MovieTitle` a `Page.Genre` a `Page.MovieYear`. (Nebo jiné názvy, které jste vymysleli k ukládání informací.) Jediným požadavkem, který je pravděpodobně zřejmý – je, že je nutné použít stejné názvy na stránce obsahu a na stránce rozložení.
> 
> Informace, které předáte pomocí objektu `Page`, nejsou omezeny pouze na text, který se má zobrazit na stránce rozložení. Můžete předat hodnotu stránce rozložení a potom kód na stránce rozložení může použít hodnotu k rozhodnutí, zda se má zobrazit sekce stránky, co soubor *. CSS* , který má být použit, a tak dále. Hodnoty, které předáte do objektu `Page`, jsou stejně jako jakékoli jiné hodnoty, které používáte v kódu. Je pouze to, že hodnoty pocházejí ze stránky obsahu a jsou předány na stránku rozložení.

Otevřete stránku *AddMovie. cshtml* a přidejte řádek na začátek kódu, který poskytuje název stránky *AddMovie. cshtml* :

[!code-csharp[Main](layouts/samples/sample10.cs)]

Spusťte stránku *AddMovie. cshtml* . Tady vidíte nový název:

![Karta prohlížeče zobrazující, že se název přidat filmy vytvořil dynamicky](layouts/_static/image10.png)

## <a name="updating-the-remaining-pages-to-use-the-layout"></a>Aktualizace zbývajících stránek na používání rozložení

Nyní můžete zbývající stránky na webu dokončit tak, aby používaly nové rozložení. Otevřete *EditMovie. cshtml* a *DeleteMovie. cshtml* a udělejte v nich stejné změny.

Přidejte řádek kódu, který odkazuje na stránku rozložení:

[!code-csharp[Main](layouts/samples/sample11.cs)]

Přidejte řádek pro nastavení názvu stránky:

[!code-csharp[Main](layouts/samples/sample12.cs)]

nebo:

[!code-csharp[Main](layouts/samples/sample13.cs)]

Odebrat všechny nadbytečné značky HTML – v podstatě ponechte pouze bity, které jsou uvnitř elementu `<body>` (plus blok kódu v horní části).

Změňte `<h1>` element tak, aby byl `<h2>` element.

Jakmile provedete tyto změny, otestujte je a ujistěte se, že se zobrazují správně a že je název správný.

## <a name="parting-thoughts-about-layout-pages"></a>Rozmístění nápadů na stránky rozložení

V tomto kurzu jste vytvořili stránku *\_layout. cshtml* a pomocí metody `RenderBody` sloučíte obsah z jiné stránky. To je základní model pro použití rozložení na webových stránkách.

Stránky rozložení mají další funkce, které tady nepokrýváme. Můžete například vnořovat stránky rozložení – jedna stránka rozložení může odkazovat na další. Vnořená rozložení můžou být užitečná, když pracujete s podčástmi lokality, která vyžaduje různá rozložení. Můžete také použít další metody (například `RenderSection`), chcete-li nastavit pojmenované oddíly na stránce rozložení.

Kombinace stránek rozložení a souborů *. CSS* je výkonné. Jak vidíte v další sérii kurzů, můžete v WebMatrixu vytvořit web na základě *šablony*, která vám poskytne web s předem sestavenými funkcemi. Šablony usnadňují použití stránek rozložení a šablon stylů CSS k vytváření webů, které vypadají skvěle a mají funkce jako nabídky. Tady je snímek obrazovky domovské stránky z webu založeného na šabloně, který zobrazuje funkce, které používají stránky rozložení a šablony stylů CSS:

![Rozložení vytvořené šablonou webu WebMatrix zobrazující záhlaví, navigační oblast, oblast obsahu, volitelný oddíl a přihlašovací odkazy](layouts/_static/image11.png)

## <a name="complete-listing-for-movie-page-updated-to-use-a-layout-page"></a>Úplný výpis stránky videa (aktualizovaný pro použití stránky rozložení)

[!code-cshtml[Main](layouts/samples/sample14.cshtml)]

## <a name="complete-page-listing-for-add-movie-page-updated-for-layout"></a>Dokončení výpisu stránky pro stránku přidat film (Aktualizováno pro rozložení)

[!code-cshtml[Main](layouts/samples/sample15.cshtml)]

## <a name="complete-page-listing-for-delete-movie-page-updated-for-layout"></a>Dokončení výpisu stránky pro stránku odstranit film (Aktualizováno pro rozložení)

[!code-cshtml[Main](layouts/samples/sample16.cshtml)]

## <a name="complete-page-listing-for-edit-movie-page-updated-for-layout"></a>Úplný výpis stránky pro stránku Upravit film (Aktualizováno pro rozložení)

[!code-cshtml[Main](layouts/samples/sample17.cshtml)]

## <a name="coming-up-next"></a>Připravujeme další

V dalším kurzu se dozvíte, jak publikovat web na Internet tak, aby ho všichni mohli vidět.

## <a name="additional-resources"></a>Další prostředky

- [Vytvoření konzistentního vzhledu](https://go.microsoft.com/fwlink/?LinkID=202891) – článek, který poskytuje další podrobnosti o práci s rozloženími. Popisuje také, jak předat hodnotu stránce rozložení, která zobrazuje nebo skrývá část obsahu.
- [Vnořené stránky rozložení se syntaxí Razor](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) – Jan slané Blogy příklad, jak vnořit stránky rozložení. (Zahrnuje stažení stránek.)

> [!div class="step-by-step"]
> [Předchozí](deleting-data.md)
> [Další](publishing.md)

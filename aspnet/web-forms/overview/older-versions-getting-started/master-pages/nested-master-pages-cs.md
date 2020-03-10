---
uid: web-forms/overview/older-versions-getting-started/master-pages/nested-master-pages-cs
title: Vnořené stránky předlohy (C#) | Microsoft Docs
author: rick-anderson
description: Ukazuje, jak vnořit jednu hlavní stránku do jiné.
ms.author: riande
ms.date: 07/28/2008
ms.assetid: 32b7fb6e-d74b-4048-91f8-70631b2523ee
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/nested-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 67093266567a97cd22b353115616484fd9ef155e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574380"
---
# <a name="nested-master-pages-c"></a>Vložené hlavní stránky (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_10_CS.zip) nebo [stažení PDF](https://download.microsoft.com/download/d/6/6/d66ad554-afdd-409e-a5c3-201b774fbb31/ASPNET_MasterPages_Tutorial_10_CS.pdf)

> Ukazuje, jak vnořit jednu hlavní stránku do jiné.

## <a name="introduction"></a>Úvod

V průběhu posledních devět kurzů jsme viděli, jak implementovat rozložení pro celé pracoviště pomocí stránek předlohy. Ve kostce stránky předlohy nám umožňují vývojářům stránek definovat společné značky na stránce předlohy spolu s konkrétními oblastmi, které je možné přizpůsobit na základě stránky obsahu stránky po obsahu. Ovládací prvky ContentPlaceHolder na stránce předlohy označují přizpůsobitelné oblasti. přizpůsobené značky pro ovládací prvky ContentPlaceHolder jsou definovány na stránce obsahu prostřednictvím ovládacích prvků obsahu.

Techniky hlavní stránky, které jsme prozkoumali, jsou proto Skvělé, pokud máte v celé lokalitě použito jedno rozložení. Mnoho velkých webů ale má rozložení lokality, které je přizpůsobené v různých oddílech. Představte si například aplikaci zdravotní péče, kterou používá ústavní pracovníci, ke správě informací o pacientech, aktivit a fakturaci. V této aplikaci můžou být tři typy webových stránek:

- Personální stránky pro konkrétní členy, kde zaměstnanci můžou aktualizovat dostupnost, zobrazit plány nebo si vyžádat dobu trvání dovolené.
- Stránky specifické pro pacienty, kde pedagogické členové zobrazují nebo upravují informace pro konkrétního pacienta.
- Stránky specifické pro fakturaci, kde účetníci kontrolují aktuální stavy deklarací identity a finanční sestavy.

Každá stránka může sdílet společné rozložení, jako je například nabídka v horní části, a řada často používaných odkazů podél dolního okraje. Ale stránky pro zaměstnance, pacienty a fakturaci budou muset přizpůsobit toto obecné rozložení. Například všechny stránky specifické pro zaměstnance by měly obsahovat kalendář a seznam úkolů, které zobrazují aktuálně přihlášený účet dostupnosti a denní plán. Některé stránky specifické pro pacient musí zobrazovat jméno, adresu a informace o pojištění pro pacienta, jejichž informace se upravují.

Taková přizpůsobená rozložení je možné vytvořit pomocí *vnořených stránek předlohy*. K implementaci výše uvedeného scénáře doporučujeme začít vytvořením hlavní stránky, která definovala rozložení v rámci lokality, obsah nabídky a zápatí s prvky ContentPlaceHolders definující přizpůsobitelné oblasti. Vytvoříme tři vnořené stránky předlohy, jednu pro každý typ webové stránky. Každá vnořená hlavní stránka by definovala obsah mezi typem stránek obsahu, které používají stránku předlohy. Jinými slovy vnořená hlavní stránka pro stránky obsahu specifické pro pacienty by obsahovala značky a programovou logiku pro zobrazení informací o upravovaném pacienta. Když vytváříte novou stránku specifickou pro pacienty, navážeme ji na tuto vnořenou stránku předlohy.

Tento kurz se spustí zvýrazněním výhod vnořených stránek předlohy. Pak ukazuje, jak vytvořit a používat vnořené stránky předlohy.

> [!NOTE]
> Vnořené stránky předlohy byly možné od verze 2,0 .NET Framework. Visual Studio 2005 ale nezahrnuje podporu pro vnořené stránky předloh v době návrhu. Dobrá zpráva je, že Visual Studio 2008 nabízí bohatě funkční prostředí pro vnořené stránky předlohy. Pokud vás zajímá použití vnořených stránek předlohy, ale stále používáte Visual Studio 2005, podívejte se na záznam blogu [Scott Guthrie](https://weblogs.asp.net/scottgu/), [tipy pro vnořené stránky předlohy v době návrhu vs 2005](https://weblogs.asp.net/scottgu/archive/2005/11/11/430382.aspx).

## <a name="the-benefits-of-nested-master-pages"></a>Výhody vnořených stránek předlohy

Mnoho webů má předaný návrh lokality a také přizpůsobené návrhy, které jsou specifické pro určité typy stránek. Například v naší ukázkové webové aplikaci jsme vytvořili oddíl základní Administration (stránky ve složce `~/Admin`). V současné době webové stránky ve složce `~/Admin` používají stejnou stránku předlohy jako tyto stránky, které nejsou v oddílu Správa (konkrétně `Site.master` nebo `Alternate.master`v závislosti na výběru uživatele).

> [!NOTE]
> Prozatím předstírat, že náš web má jenom jednu stránku předlohy, `Site.master`. Budeme řešit použití vnořených stránek předlohy se dvěma (nebo více) stránkami předlohy počínaje "používáním vnořené stránky předlohy pro část pro správu" dále v tomto kurzu.

Představte si, že jsme byli požádáni o přizpůsobení rozložení stránek pro správu, aby obsahovalo Další informace nebo odkazy, které by jinak nebyly na jiných stránkách v lokalitě. Tento požadavek můžete implementovat čtyřmi způsoby:

1. Ručně přidejte informace specifické pro správu a odkazy na všechny stránky obsahu ve složce `~/Admin`.
2. Aktualizujte stránku předlohy `Site.master` tak, aby obsahovala informace specifické pro oddíl Správa a odkazy, a potom přidejte kód na stránku předlohy, kde tyto oddíly zobrazíte nebo skryjete na základě toho, jestli se jedna ze stránek pro správu právě navštíví.
3. Vytvořte novou stránku předlohy specifickou pro oddíl Správa a zkopírujte z `Site.master`značky, přidejte informace a odkazy specifické pro oddíl Správa a pak aktualizujte stránky obsahu ve `~/Admin` složce tak, aby používala tuto novou stránku předlohy.
4. Vytvořte vnořenou stránku předlohy, která se váže na `Site.master` a zda stránky obsahu ve `~/Admin` složce používají tuto novou vnořenou stránku předlohy. Tato vnořená hlavní stránka by obsahovala jenom další informace a odkazy, které jsou specifické pro stránky pro správu, a nemusí opakovat označení, které už je definované v `Site.master`.

První možnost je nejméně palatable. Celým bodem stránek předlohy je opuštění a ruční kopírování a vkládání běžných značek na nové stránky ASP.NET. Druhá možnost je přijatelná, ale aplikace je méně udržovatelná, protože hromadně udržuje hlavní stránky se značkami, které se zobrazují pouze občas, a vyžaduje, aby vývojáři, kteří upravují stránku předlohy, mohli tento kód obejít a museli si pamatovat, když, v případě, že je skrytá, zobrazí se přesně určité značky. Tento přístup by byl méně Tenable jako přizpůsobení z více a více typů webových stránek, které je nutné přizpůsobit na této jediné stránce předlohy.

Třetí možnost odstraní zbytečné a složitosti problémy, které jsou Surface druhé možnosti. Možnost tři hlavní nevýhoda však znamená, že pro nás vyžaduje zkopírování a vložení společného rozložení z `Site.master` do nové hlavní stránky pro správu, která je specifická pro oddíl. Pokud se později rozhodnete změnit rozložení v rámci lokality, je nutné si pamatovat na jeho změnu na dvou místech.

Čtvrtá možnost vnořené stránky předlohy vám poskytne nejlepší z druhé a třetí možnosti. Informace o rozložení v rámci lokality jsou uchovávány v jednom souboru – hlavní stránka nejvyšší úrovně – zatímco obsah specifický pro konkrétní oblasti je rozdělen do různých souborů.

Tento kurz začíná zobrazením vytváření a používání jednoduché vnořené stránky předlohy. Vytvoříme značku nové hlavní stránky nejvyšší úrovně, dvě vnořené stránky předlohy a dvě stránky obsahu. Počínaje "používáním vnořené stránky předlohy pro část pro správu" se podíváme na aktualizaci stávající architektury hlavní stránky, aby zahrnovala použití vnořených stránek předlohy. Konkrétně vytvoříme vnořenou hlavní stránku a použijeme ji k zahrnutí dalšího vlastního obsahu pro stránky obsahu do složky `~/Admin`.

## <a name="step-1-creating-a-simple-top-level-master-page"></a>Krok 1: Vytvoření jednoduché hlavní stránky nejvyšší úrovně

Vytvoření vnořené hlavní stránky na základě jedné z existujících stránek předlohy a následná aktualizace stávající stránky obsahu, aby používala tuto novou vnořenou stránku předlohy namísto hlavní stránky nejvyšší úrovně, má za následek určitou složitost, protože stávající stránky obsahu již očekávají určité Ovládací prvky ContentPlaceHolder definované v hlavní stránce nejvyšší úrovně. Proto vnořená hlavní stránka musí obsahovat také stejné ovládací prvky ContentPlaceHolder se stejnými názvy. Kromě toho má naše konkrétní ukázková aplikace dvě stránky předlohy (`Site.master` a `Alternate.master`), které se dynamicky přiřazují na stránku obsahu založené na uživatelských preferencích, které další přidávají k této složitosti. V tomto kurzu se podíváme na aktualizaci existující aplikace, aby používala vnořené stránky předlohy, ale nejprve se zaměříme na jednoduchý vnořený příklad stránek na konci.

Vytvořte novou složku s názvem `NestedMasterPages` a přidejte do ní nový soubor hlavní stránky s názvem `Simple.master`. (Viz obrázek 1 pro snímek obrazovky Průzkumník řešení po přidání této složky a souboru.) Přetáhněte `AlternateStyles.css` soubor předlohy se styly z Průzkumník řešení na Návrhář. Tím přidáte `<link>` element do souboru šablony stylů v elementu `<head>`, po kterém by značky `<head>` elementu hlavní stránky měly vypadat takto:

[!code-aspx[Main](nested-master-pages-cs/samples/sample1.aspx)]

Dále do webového formuláře `Simple.master`přidejte následující značky:

[!code-aspx[Main](nested-master-pages-cs/samples/sample2.aspx)]

Tento kód zobrazí odkaz s názvem "vnořené stránky předlohy (jednoduché)" v horní části stránky s velkým bílým písmem na pozadí námořnická modrá. Níže je `MainContent` ContentPlaceHolder. Obrázek 1 ukazuje stránku předlohy `Simple.master`, když je načtena v návrháři aplikace Visual Studio.

[![vnořená hlavní stránka definuje obsah specifický pro stránky v oddílu Správa.](nested-master-pages-cs/_static/image2.png)](nested-master-pages-cs/_static/image1.png)

**Obrázek 01**: vnořená hlavní stránka definuje obsah specifický pro stránky v části Správa ([kliknutím zobrazíte obrázek v plné velikosti).](nested-master-pages-cs/_static/image3.png)

## <a name="step-2-creating-a-simple-nested-master-page"></a>Krok 2: Vytvoření jednoduché vnořené stránky předlohy

`Simple.master` obsahuje dva ovládací prvky ContentPlaceHolder: `MainContent` ContentPlaceHolder, které jsme přidali v rámci webového formuláře společně s `head` ContentPlaceHolder v elementu `<head>`. Pokud bychom vytvořili stránku obsahu a navážeme ji na `Simple.master` stránka obsahu by měla dva ovládací prvky obsahu odkazující na tyto dva prvky ContentPlaceHolder. Podobně pokud vytvoříme vnořenou hlavní stránku a navážeme ji na `Simple.master` pak bude mít vnořená hlavní stránka dva ovládací prvky obsahu.

Pojďme do složky `NestedMasterPages` s názvem `SimpleNested.master`přidat novou vnořenou stránku předlohy. Klikněte pravým tlačítkem na složku `NestedMasterPages` a vyberte možnost Přidat novou položku. Tím se zobrazí dialogové okno Přidat novou položku zobrazenou na obrázku 2. Vyberte typ šablony stránky předlohy a zadejte název nové stránky předlohy. Chcete-li označit, že nová stránka předlohy by měla být vnořenou stránkou předlohy, zaškrtněte políčko vybrat hlavní stránku.

Potom klikněte na tlačítko Přidat. Tím se zobrazí stejné dialogové okno vybrat hlavní stránku, které vidíte při vázání stránky obsahu na stránku předlohy (viz obrázek 3). Ve složce `NestedMasterPages` vyberte stránku předlohy `Simple.master` a klikněte na OK.

> [!NOTE]
> Pokud jste web ASP.NET vytvořili pomocí modelu projektu webové aplikace namísto modelu projektu webu, nezobrazí se v dialogovém okně Přidat novou položku na obrázku 2 zaškrtávací políčko vybrat hlavní stránku. Chcete-li vytvořit vnořenou stránku předlohy při použití modelu projektu webové aplikace, musíte zvolit vnořenou šablonu hlavní stránky (místo šablony stránky předlohy). Po výběru šablony vnořené stránky předlohy a kliknutí na tlačítko Přidat se zobrazí stejné dialogové okno vybrat hlavní stránku zobrazené na obrázku 3.

[![zaškrtnutím políčka &quot;vybrat vzorovou stránku&quot; přidáte vnořenou stránku předlohy.](nested-master-pages-cs/_static/image5.png)](nested-master-pages-cs/_static/image4.png)

**Obrázek 02**: Zaškrtnutím políčka vybrat vzorovou stránku přidáte vnořenou stránku předlohy ([kliknutím zobrazíte obrázek v plné velikosti).](nested-master-pages-cs/_static/image6.png)

[![vytvořit vazby na vnořenou stránku předlohy na jednoduchou hlavní stránku hlavního serveru.](nested-master-pages-cs/_static/image8.png)](nested-master-pages-cs/_static/image7.png)

**Obrázek 03**: Svázání vnořené stránky předlohy s `Simple.master` stránkou předlohy ([kliknutím zobrazíte obrázek v plné velikosti](nested-master-pages-cs/_static/image9.png))

Deklarativní označení vnořené stránky předlohy zobrazené níže obsahuje dva ovládací prvky obsahu odkazující na dva ovládací prvky ContentPlaceHolder stránky hlavní úrovně.

[!code-aspx[Main](nested-master-pages-cs/samples/sample3.aspx)]

S výjimkou direktivy `<%@ Master %>` je počáteční deklarativní značkovací kód vnořené stránky stejný jako kód, který je původně generován při vázání stránky obsahu na stejnou hlavní stránku nejvyšší úrovně. Podobně jako direktiva `<%@ Page %>` stránky obsahu zahrnuje direktiva `<%@ Master %>`, která obsahuje atribut `MasterPageFile`, který určuje nadřazenou stránku předlohy nadřazené stránky. Hlavní rozdíl mezi vnořenou stránkou předlohy a stránkou obsahu vázanými na stejnou hlavní stránku nejvyšší úrovně je, že vnořená hlavní stránka může obsahovat ovládací prvky ContentPlaceHolder. Ovládací prvky ContentPlaceHolder vložené hlavní stránky definují oblasti, ve kterých mohou stránky obsahu přizpůsobit značky.

Umožňuje aktualizovat tuto vnořenou stránku předlohy tak, aby zobrazila text "Hello" z SimpleNested! v ovládacím prvku Content, který odpovídá ovládacímu prvku `MainContent` ContentPlaceHolder.

[!code-aspx[Main](nested-master-pages-cs/samples/sample4.aspx)]

Po tomto přidání uložte vnořenou stránku předlohy a přidejte novou stránku obsahu do složky `NestedMasterPages` s názvem `Default.aspx`a vytvořte její vazby na `SimpleNested.master` hlavní stránku. Při přidávání této stránky můžete být překvapeni, abyste viděli, že neobsahuje žádné ovládací prvky obsahu (viz obrázek 4). Stránka obsahu má přístup pouze k ovládacím prvkům s *nadřazenými* prvky hlavní stránky. `SimpleNested.master` neobsahuje žádné ovládací prvky ContentPlaceHolder; Proto všechny stránky obsahu svázané s touto stránkou předlohy nemohou obsahovat žádné ovládací prvky obsahu.

[![nová stránka obsahu neobsahuje žádné ovládací prvky obsahu.](nested-master-pages-cs/_static/image11.png)](nested-master-pages-cs/_static/image10.png)

**Obrázek 04**: stránka nový obsah neobsahuje žádné ovládací prvky obsahu ([kliknutím zobrazíte obrázek v plné velikosti).](nested-master-pages-cs/_static/image12.png)

Co musíme udělat, je aktualizovat vnořenou hlavní stránku (`SimpleNested.master`) tak, aby zahrnovala ovládací prvky ContentPlaceHolder. Obvykle budete chtít, aby vnořené stránky předlohy zahrnovaly prvek ContentPlaceHolder pro každý prvek ContentPlaceHolder definovaný jeho nadřazenou stránkou předlohy, čímž bylo umožněno, aby jeho podřízená stránka předlohy nebo stránka obsahu pracovala s libovolným prvkem ContentPlaceHolder stránky hlavní stránky. ovládací prvky.

Aktualizujte `SimpleNested.master` stránku předlohy tak, aby obsahovala prvek ContentPlaceHolder ve svých dvou ovládacích prvcích obsahu. Udělte ovládací prvky ContentPlaceHolder stejný název jako ovládací prvek ContentPlaceHolder, na který se vztahuje ovládací prvek Content. To znamená přidání ovládacího prvku ContentPlaceHolder s názvem `MainContent` k ovládacímu prvku obsahu v `SimpleNested.master`, který odkazuje na `MainContent` ContentPlaceHolder v `Simple.master`. Proveďte stejnou věc v ovládacím prvku obsahu, která odkazuje na `head` ContentPlaceHolder.

> [!NOTE]
> I když doporučujeme pojmenovat ovládací prvky ContentPlaceHolder ve vnořené stránce předlohy stejně jako prvky ContentPlaceHolder na stránce předlohy nejvyšší úrovně, toto pojmenovávání se nevyžaduje. Můžete dát ovládacím prvkům ContentPlaceHolder na své vnořené stránce předlohy libovolný název, který chcete. Je však snazší si uvědomit, jaké prvky ContentPlaceHolder odpovídají v jaké oblasti stránky, pokud má hlavní stránka nejvyšší úrovně a vnořené stránky předlohy stejné názvy.

Po provedení těchto přidání by deklarativní označení stránky hlavní stránky `SimpleNested.master` mělo vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](nested-master-pages-cs/samples/sample5.aspx)]

Odstraňte `Default.aspx` stránku obsahu, kterou jsme právě vytvořili, a pak ji znovu přidejte a navážeme ji na `SimpleNested.master` stránku předlohy. Tentokrát aplikace Visual Studio přidá do `Default.aspx`dva ovládací prvky obsahu odkazující na prvky ContentPlaceHolders nyní definované v `SimpleNested.master` (viz obrázek 6). Přidejte text "Hello" z default. aspx! " v ovládacím prvku Content, na který se odkazuje `MainContent`.

Na obrázku 5 jsou uvedené tři entity – `Simple.master`, `SimpleNested.master`a `Default.aspx` – a jak se vzájemně vztahují. Jak znázorňuje diagram, vnořená hlavní stránka implementuje ovládací prvky obsahu pro své nadřazené prvky ContentPlaceHolder. Pokud tyto oblasti potřebují být dostupné pro stránku obsahu, vnořená hlavní stránka musí přidat své vlastní prvky ContentPlaceHolder do ovládacích prvků obsahu.

[![rozložení stránky obsahu v zobrazení stránky nejvyšší úrovně a vnořených hlavních stránek](nested-master-pages-cs/_static/image14.png)](nested-master-pages-cs/_static/image13.png)

**Obrázek 05**: stránky nejvyšší úrovně a vnořené hlavní stránky určují rozložení stránky obsahu ([kliknutím zobrazíte obrázek v plné velikosti).](nested-master-pages-cs/_static/image15.png)

Toto chování ilustruje, jak se stránka obsahu nebo stránka předlohy společnost Cognizant jenom na svou nadřazenou stránku předlohy. Toto chování je také uvedeno v návrháři aplikace Visual Studio. Obrázek 6 ukazuje návrháře `Default.aspx`. Návrhář sice jasně ukazuje, které oblasti jsou editovatelné na stránce obsahu a které části nejsou. neumožňuje určit, které neupravitelné oblasti jsou z vnořené stránky předlohy a jaké oblasti se nacházejí na hlavní stránce nejvyšší úrovně.

[![stránka obsahu teď obsahuje ovládací prvky obsahu pro vnořené prvky ContentPlaceHolder stránky předlohy.](nested-master-pages-cs/_static/image17.png)](nested-master-pages-cs/_static/image16.png)

**Obrázek 6**: stránka obsahu teď obsahuje ovládací prvky obsahu pro vnořené prvky ContentPlaceHolder stránky předlohy ([kliknutím zobrazíte obrázek v plné velikosti).](nested-master-pages-cs/_static/image18.png)

## <a name="step-3-adding-a-second-simple-nested-master-page"></a>Krok 3: Přidání druhé jednoduché vnořené stránky předlohy

Výhoda vnořených stránek předlohy je zřejmější, pokud existuje více vnořených stránek předlohy. Pro ilustraci této výhody vytvořte další vnořenou stránku předlohy ve složce `NestedMasterPages`. Pojmenujte tuto novou vnořenou stránku předlohy `SimpleNestedAlternate.master` a navažte ji na `Simple.master` stránku předlohy. Přidejte ovládací prvky ContentPlaceHolder do dvou ovládacích prvků obsahu vnořené stránky předlohy, jako jsme to provedli v kroku 2. Přidejte také text "Hello" z SimpleNestedAlternate! v ovládacím prvku Content, který odpovídá `MainContent` ContentPlaceHolder stránky hlavní stránky nejvyšší úrovně. Po provedení těchto změn by deklarativní označení nové vnořené stránky předlohy měla vypadat nějak takto:

[!code-aspx[Main](nested-master-pages-cs/samples/sample6.aspx)]

Vytvořte stránku obsahu s názvem `Alternate.aspx` ve složce `NestedMasterPages` a navažte ji na `SimpleNestedAlternate.master` vnořenou hlavní stránkou. Přidejte text "Hello" z alternativního! " v ovládacím prvku Content, který odpovídá `MainContent`. Obrázek 7 zobrazuje `Alternate.aspx` při prohlížení pomocí návrháře sady Visual Studio.

[![alternativní přípona. aspx je svázána s hlavní stránkou SimpleNestedAlternate. Master.](nested-master-pages-cs/_static/image20.png)](nested-master-pages-cs/_static/image19.png)

**Obrázek 07**: `Alternate.aspx` je svázána se stránkou předlohy `SimpleNestedAlternate.master` ([kliknutím zobrazíte obrázek v plné velikosti).](nested-master-pages-cs/_static/image21.png)

Porovnejte návrháře na obrázku 7 s návrhářem na obrázku 6. Obě stránky obsahu sdílejí stejné rozložení definované na hlavní stránce nejvyšší úrovně (`Simple.master`), konkrétně v tématu kurz "vnořené stránky předlohy (jednoduché)". Ve svých nadřazených stránkách předlohy ale zároveň má stejný obsah definovaný jako text "Hello" z SimpleNested! " na obrázku 6 a "Hello" z SimpleNestedAlternate! " na obrázku 7. Tyto rozdíly jsou v tomto případě triviální, ale můžete tento příklad zvětšit tak, aby zahrnoval smysluplnější rozdíly. Například stránka `SimpleNested.master` může obsahovat nabídku s možnostmi specifickými pro její stránky obsahu, zatímco `SimpleNestedAlternate.master` mohou mít informace, které se vztahují na stránky obsahu, které se na ni vážou.

Nyní si představte, že jsme potřebovali udělat změnu rozložení lokality. Představte si například, že jsme chtěli přidat seznam běžných odkazů na všechny stránky obsahu. K tomu je potřeba aktualizovat hlavní stránku nejvyšší úrovně `Simple.master`. Všechny změny, které se okamžitě projeví ve vnořených stránkách předlohy a na základě přípon, jejich stránek obsahu.

K demonstraci snadného, které můžeme změnit rozložení lokality, otevřete stránku předloha `Simple.master` a přidejte následující značku mezi `topContent` a prvky `mainContent` `<div>`:

[!code-aspx[Main](nested-master-pages-cs/samples/sample7.aspx)]

Tím přidáte dvě odkazy na horní stranu každé stránky, která se váže k `Simple.master`, `SimpleNested.master`nebo `SimpleNestedAlternate.master`. Tyto změny platí pro všechny vnořené stránky předlohy a jejich stránky obsahu okamžitě. Obrázek 8 zobrazuje `Alternate.aspx` při prohlížení v prohlížeči. Všimněte si přidání odkazů v horní části stránky (ve srovnání s obrázkem 7).

[![změněné na hlavní stránku nejvyšší úrovně se okamžitě projeví ve vnořených stránkách předlohy a jejich stránkách obsahu.](nested-master-pages-cs/_static/image23.png)](nested-master-pages-cs/_static/image22.png)

**Obrázek 08**: Změna na hlavní stránku nejvyšší úrovně se okamžitě projeví ve svých vnořených stránkách předlohy a jejich stránkách obsahu ([kliknutím zobrazíte obrázek v plné velikosti).](nested-master-pages-cs/_static/image24.png)

## <a name="using-a-nested-master-page-for-the-administration-section"></a>Použití vnořené stránky předlohy pro oddíl Administration

V tuto chvíli jsme si prohlédli výhody vnořených hlavních stránek a viděli, jak je vytvořit a používat v aplikaci ASP.NET. Příklady v krocích 1, 2 a 3 však zahrnovaly vytvoření nové hlavní stránky nejvyšší úrovně, nové vnořené stránky předlohy a nové stránky obsahu. Jak přidat novou vnořenou stránku předlohy na web se stávajícími stránkami předloh a obsahu nejvyšší úrovně?

Integrace vnořené stránky předlohy do existující webové stránky a její přidružení k existujícím stránkám obsahu vyžaduje trochu větší úsilí než od začátku. Kroky 4, 5, 6 a 7 Prozkoumejte tyto problémy, jako jsme nastavili naši ukázkovou aplikaci tak, aby zahrnovala novou vnořenou stránku předlohy s názvem `AdminNested.master`, která obsahuje pokyny pro správce a které používají stránky ASP.NET ve `~/Admin` složce.

Integrace vnořené stránky předlohy do naší ukázkové aplikace zavádí následující mezní hodnoty:

- Stávající stránky obsahu ve složce `~/Admin` mají určitá očekávání ze své hlavní stránky. Pro Start očekávají, že jsou k dispozici určité ovládací prvky ContentPlaceHolder. Kromě toho stránky `~/Admin/AddProduct.aspx` a `~/Admin/Products.aspx` volají metodu public `RefreshRecentProductsGrid` hlavní stránky, nastavit její vlastnost `GridMessageText` nebo mít pro událost `PricesDoubled` obslužnou rutinu události. V důsledku toho musí vnořená stránka předlohy poskytovat stejné prvky ContentPlaceHolder a veřejné členy.
- V předchozím kurzu jsme rozšířili třídu `BasePage`, aby dynamicky nastavila vlastnost `MasterPageFile` objektu `Page` na základě proměnné relace. Jak podporujeme dynamické stránky předloh při použití vnořených stránek předlohy?

Tyto dvě problémy se budou nacházet při sestavování vnořené hlavní stránky a jejich použití z našich stávajících stránek obsahu. Prozkoumáme a surmountme tyto problémy, jak nastanou.

## <a name="step-4-creating-the-nested-master-page"></a>Krok 4: vytvoření vnořené stránky předlohy

Naším prvním úkolem je vytvořit vnořenou stránku předlohy, kterou budou používat stránky v části Správa. Jak jsme viděli v kroku 2, při přidávání nové vnořené stránky předlohy je potřeba zadat nadřazenou stránku nadřazené hlavní stránky. Máme ale dvě hlavní stránky nejvyšší úrovně: `Site.master` a `Alternate.master`. Odvoláme, že jsme vytvořili `Alternate.master` v předchozím kurzu a napsali jste kód ve třídě `BasePage`, která nastaví vlastnost `MasterPageFile` objektu stránky za běhu na buď `Site.master`, nebo `Alternate.master` v závislosti na hodnotě proměnné relace `MyMasterPage`.

Jak nakonfigurujeme naši vnořenou stránku předlohy tak, aby používala příslušnou hlavní stránku nejvyšší úrovně? Máme dvě možnosti:

- Vytvořte dvě vnořené stránky předlohy, `AdminNestedSite.master` a `AdminNestedAlternate.master`a vytvořte jejich vazby na hlavní stránky nejvyšší úrovně `Site.master` a `Alternate.master`v uvedeném pořadí. V `BasePage`pak nastavíme `MasterPageFile` objektu `Page` na příslušnou vnořenou stránku předlohy.
- Vytvoří jednu vnořenou hlavní stránku a bude mít stránky obsahu používat tuto konkrétní stránku předlohy. Za běhu musíme za běhu nastavit vlastnost `MasterPageFile` vnořené hlavní stránky na příslušnou hlavní stránku nejvyšší úrovně. (Jak jste teď možná nahlásili, stránky předlohy mají také vlastnost `MasterPageFile`.)

Pojďme použít druhou možnost. Vytvořte jeden vnořený soubor hlavní stránky ve složce `~/Admin` s názvem `AdminNested.master`. Vzhledem k tomu, že obě `Site.master` i `Alternate.master` mají stejnou sadu ovládacích prvků ContentPlaceHolder, nezáleží na tom, jakou stránku předlohy svážete s tím, i když doporučujeme, abyste ji navázali `Site.master` za účelem konzistence.

[![přidat vnořenou stránku předlohy do složky ~/admin.](nested-master-pages-cs/_static/image26.png)](nested-master-pages-cs/_static/image25.png)

**Obrázek 09**: přidejte do složky `~/Admin` vnořenou stránku předlohy. ([Kliknutím zobrazíte obrázek v plné velikosti.](nested-master-pages-cs/_static/image27.png))

Vzhledem k tomu, že vnořená hlavní stránka je svázána se stránkou předlohy se čtyřmi ovládacími prvky ContentPlaceHolder, Visual Studio přidá čtyři ovládací prvky obsahu do počáteční značky vnořeného souboru hlavní stránky. Podobně jako u kroků 2 a 3 přidejte ovládací prvek ContentPlaceHolder do každého ovládacího prvku Content, který má stejný název jako ovládací prvek ContentPlaceHolder hlavní stránky nejvyšší úrovně. Do ovládacího prvku Content, který odpovídá `MainContent` ContentPlaceHolder, přidejte také následující kód:

[!code-html[Main](nested-master-pages-cs/samples/sample8.html)]

Dále Definujte třídu `instructions` CSS v souborech `Styles.css` a `AlternateStyles.css` šablon stylů CSS. Následující pravidla šablony stylů CSS způsobí zobrazení prvků jazyka HTML s `instructions`ou třídou, která má být zobrazena se světle žlutou barvou pozadí a černým, plným ohraničením:

[!code-css[Main](nested-master-pages-cs/samples/sample9.css)]

Vzhledem k tomu, že tento kód byl přidán na vnořenou stránku předlohy, bude se zobrazovat pouze na stránkách, které používají tuto vnořenou stránku předlohy (konkrétně stránky v části Správa).

Po provedení těchto přidání na vnořenou hlavní stránku by jeho deklarativní označení mělo vypadat podobně jako následující:

[!code-aspx[Main](nested-master-pages-cs/samples/sample10.aspx)]

Všimněte si, že každý ovládací prvek obsahu má ovládací prvek ContentPlaceHolder a že vlastnosti ContentPlaceHolder Controls `ID` jsou přiřazeny stejné hodnoty jako odpovídající ovládací prvky ContentPlaceHolder na stránce předlohy nejvyšší úrovně. Kromě toho se značky specifické pro oddíl Správa zobrazí v `MainContent` ContentPlaceHolder.

Obrázek 10 ukazuje `AdminNested.master` vnořenou stránku předlohy při zobrazení prostřednictvím návrháře aplikace Visual Studio. Pokyny najdete ve žlutém poli v horní části ovládacího prvku obsahu `MainContent`.

[![vnořená hlavní stránka rozšiřuje hlavní stránku nejvyšší úrovně tak, aby obsahovala pokyny pro správce.](nested-master-pages-cs/_static/image29.png)](nested-master-pages-cs/_static/image28.png)

**Obrázek 10**: vnořená stránka předlohy rozšiřuje hlavní stránku nejvyšší úrovně, která obsahuje pokyny pro správce. ([Kliknutím zobrazíte obrázek v plné velikosti.](nested-master-pages-cs/_static/image30.png))

## <a name="step-5-updating-the-existing-content-pages-to-use-the-new-nested-master-page"></a>Krok 5: aktualizace stávajících stránek obsahu tak, aby používaly novou vnořenou stránku předlohy

Kdykoli přidáme novou stránku obsahu do oddílu pro správu, musíme ji navazovat na `AdminNested.master` hlavní stránku, kterou jsme právě vytvořili. Ale co o stávajících stránkách obsahu? V současné době jsou všechny stránky obsahu v lokalitě odvozeny od třídy `BasePage`, která programově nastavuje stránku předlohy stránky obsahu za běhu. Nejedná se o chování, které chceme pro stránky obsahu v části Správa. Místo toho chceme, aby tyto stránky obsahu vždy používaly stránku `AdminNested.master`. Bude odpovědností na vnořenou stránku předlohy pro výběr obsahu stránky obsahu nejvyšší úrovně za běhu.

Nejlepším způsobem, jak dosáhnout tohoto požadovaného chování, je vytvořit novou vlastní třídu základní stránky s názvem `AdminBasePage`, která rozšiřuje třídu `BasePage`. `AdminBasePage` pak může přepsat `SetMasterPageFile` a nastavit `MasterPageFile` objektu `Page` na pevně zakódované hodnoty "~/Admin/AdminNested.master". Tímto způsobem budou všechny stránky, které jsou odvozeny od `AdminBasePage`, používat `AdminNested.master`, zatímco každá stránka, která je odvozena z `BasePage`, bude mít vlastnost `MasterPageFile` nastavenou dynamicky na hodnotu "~/site.Master" nebo "~/Alternate.Master" na základě hodnoty proměnné relace `MyMasterPage`.

Začněte přidáním nového souboru třídy do složky `App_Code` s názvem `AdminBasePage.cs`. Nastavte `AdminBasePage` `BasePage` a pak přepište metodu `SetMasterPageFile`. V této metodě přiřaďte `MasterPageFile` hodnotu ~/Admin/AdminNested.master. Po provedení těchto změn by soubor vaší třídy měl vypadat nějak takto:

[!code-csharp[Main](nested-master-pages-cs/samples/sample11.cs)]

Teď je potřeba mít existující stránky obsahu v oddílu pro správu, ale musí být odvozené z `AdminBasePage` místo `BasePage`. Pro každou stránku obsahu ve složce `~/Admin` přejděte na soubor třídy kódu na pozadí a proveďte tuto změnu. Například v `~/Admin/Default.aspx` byste změnili deklaraci třídy kódu na pozadí z:

[!code-csharp[Main](nested-master-pages-cs/samples/sample12.cs)]

Komu:

[!code-csharp[Main](nested-master-pages-cs/samples/sample13.cs)]

Obrázek 11 znázorňuje, jak je hlavní stránka nejvyšší úrovně (`Site.master` nebo `Alternate.master`), vnořená hlavní stránka (`AdminNested.master`) a stránky obsahu oddílu správy vzájemně propojeny.

[![vnořená hlavní stránka definuje obsah specifický pro stránky v oddílu Správa.](nested-master-pages-cs/_static/image32.png)](nested-master-pages-cs/_static/image31.png)

**Obrázek 11**: vnořená hlavní stránka definuje obsah specifický pro stránky v části Správa ([kliknutím zobrazíte obrázek v plné velikosti).](nested-master-pages-cs/_static/image33.png)

## <a name="step-6-mirroring-the-master-pages-public-methods-and-properties"></a>Krok 6: zrcadlení veřejných metod a vlastností hlavní stránky

Odvolání, že stránky `~/Admin/AddProduct.aspx` a `~/Admin/Products.aspx` komunikují programově s hlavní stránkou: `~/Admin/AddProduct.aspx` volá metodu public `RefreshRecentProductsGrid` hlavní stránky a nastaví její vlastnost `GridMessageText`; `~/Admin/Products.aspx` má pro událost `PricesDoubled` obslužnou rutinu události. V předchozím kurzu jsme vytvořili abstraktní třídu `BaseMasterPage`, která definovala tyto veřejné členy.

Stránky `~/Admin/AddProduct.aspx` a `~/Admin/Products.aspx` předpokládají, že jejich hlavní stránka je odvozena z třídy `BaseMasterPage`. Stránka `AdminNested.master` však v současné době rozšiřuje třídu `System.Web.UI.MasterPage`. V důsledku toho je při návštěvě `~/Admin/Products.aspx` vyvolána `InvalidCastException` zpráva: "" nelze přetypovat objekt typu ' ASP. admin\_adminnested\_Master ' na typ ' BaseMasterPage '.

Aby bylo možné tuto chybu opravit, potřebujeme, aby třída `AdminNested.master` kódu na pozadí rozšířila `BaseMasterPage`. Aktualizovat deklaraci třídy u vnořené stránky s kódem na pozadí z:

[!code-csharp[Main](nested-master-pages-cs/samples/sample14.cs)]

Komu:

[!code-csharp[Main](nested-master-pages-cs/samples/sample15.cs)]

Ještě to neudělalo. Vzhledem k tomu, že třída `BaseMasterPage` je abstraktní, musíme přepsat členy `abstract`, `RefreshRecentProductsGrid` a `GridMessageText`. Tyto členy jsou používány hlavními stránkami nejvyšší úrovně k aktualizaci jejich uživatelských rozhraní. (Ve skutečnosti tyto metody používají pouze hlavní stránku `Site.master`, i když hlavní stránky nejvyšší úrovně implementují tyto metody, protože obě rozšiřuje `BaseMasterPage`.)

I když musíme tyto členy implementovat v `AdminNested.master`, je nutné, aby všechny tyto implementace byly jednoduše volány stejným členem na hlavní stránce nejvyšší úrovně používané vnořenou stránkou předlohy. Například když stránka obsahu v oddílu pro správu volá metodu `RefreshRecentProductsGrid` vnořené hlavní stránky, je nutné, aby všechny vnořené hlavní stránky navolaly `RefreshRecentProductsGrid` metodu `Site.master` nebo `Alternate.master`.

Chcete-li to dosáhnout, Začněte přidáním následující direktivy `@MasterType` do horní části `AdminNested.master`:

[!code-aspx[Main](nested-master-pages-cs/samples/sample16.aspx)]

Odvolání, že direktiva `@MasterType` přidá vlastnost silného typu do třídy kódu na pozadí s názvem `Master`. Pak přepište `RefreshRecentProductsGrid` a `GridMessageText` členů a jednoduše delegovat volání odpovídající metodě `Master`:

[!code-csharp[Main](nested-master-pages-cs/samples/sample17.cs)]

S tímto kódem byste měli být schopni navštívit a používat stránky obsahu v části Správa. Obrázek 12 zobrazuje stránku `~/Admin/Products.aspx` při prohlížení v prohlížeči. Jak vidíte, stránka obsahuje dialogové okno pokyny pro správu, které je definováno na vnořené stránce předlohy.

[![stránky obsahu v části Správa zahrnuje pokyny v horní části každé stránky.](nested-master-pages-cs/_static/image35.png)](nested-master-pages-cs/_static/image34.png)

**Obrázek 12**: stránky obsahu v části Správa obsahují pokyny v horní části každé stránky ([kliknutím zobrazíte obrázek v plné velikosti).](nested-master-pages-cs/_static/image36.png)

## <a name="step-7-using-the-appropriate-top-level-master-page-at-runtime"></a>Krok 7: použití příslušné hlavní stránky nejvyšší úrovně za běhu

I když jsou všechny stránky obsahu v části Správa plně funkční, všichni používají stejnou hlavní stránku nejvyšší úrovně a ignorují stránku předlohy vybranou uživatelem na `ChooseMasterPage.aspx`. Důvodem tohoto chování je skutečnost, že vnořená stránka předlohy má svou `MasterPageFile` vlastnost staticky nastavenou na `Site.master` ve své `<%@ Master %>` direktivě.

Chcete-li použít hlavní stránku nejvyšší úrovně vybranou koncovým uživatelem, musíme nastavit vlastnost `MasterPageFile` `AdminNested.master`na hodnotu v proměnné relace `MyMasterPage`. Vzhledem k tomu, že jsme nastavili `MasterPageFile` vlastnosti stránek obsahu v `BasePage`, možná si myslíte, že by se vlastnost `MasterPageFile` vnořené stránky předlohy nastavila v `BaseMasterPage` nebo ve třídě kódu na pozadí `AdminNested.master`. To ale nebude fungovat, protože potřebujeme nastavit vlastnost `MasterPageFile` na konci předinicializační fáze. Nejdřívější čas, který můžeme programově rozvolat do životního cyklu stránky ze stránky předlohy, je fáze init (která nastane po fázi předinicializace).

Proto je potřeba nastavit vlastnost `MasterPageFile` vnořené hlavní stránky ze stránek obsahu. Jediné stránky obsahu, které používají `AdminNested.master` hlavní stránku, jsou odvozeny z `AdminBasePage`. Proto můžeme tuto logiku vložit do tohoto umístění. V kroku 5 jsme overrode metodu `SetMasterPageFile` a nastavením vlastnosti `MasterPageFile` objektu `Page` na ~/Admin/AdminNested.master. Aktualizujte `SetMasterPageFile` a nastavte také vlastnost `MasterPageFile` stránky předlohy na výsledek uložený v relaci:

[!code-csharp[Main](nested-master-pages-cs/samples/sample18.cs)]

Metoda `GetMasterPageFileFromSession`, kterou jsme přidali do `BasePage` třídy v předchozím kurzu, vrátí odpovídající cestu k souboru hlavní stránky na základě hodnoty proměnné relace.

Při této změně se výběr hlavní stránky uživatele přenese do oddílu Správa. Obrázek 13 znázorňuje stejnou stránku jako obrázek 12, ale poté, co uživatel změnil výběr své hlavní stránky na `Alternate.master`.

[![stránka vnořené správy používá hlavní stránku nejvyšší úrovně vybranou uživatelem.](nested-master-pages-cs/_static/image38.png)](nested-master-pages-cs/_static/image37.png)

**Obrázek 13**: stránka vnořené správy používá hlavní stránku nejvyšší úrovně vybranou uživatelem ([kliknutím zobrazíte obrázek v plné velikosti).](nested-master-pages-cs/_static/image39.png)

## <a name="summary"></a>Souhrn

Vzhledem k tomu, jak můžou stránky obsahu navazovat vazby na stránku předlohy, je možné vytvořit vnořené stránky předlohy s vazbou podřízené stránky předlohy na nadřazenou stránku předlohy. Podřízená stránka předlohy může definovat ovládací prvky obsahu pro každé z jejích nadřazených elementů ContentPlaceHolder; pak může do těchto ovládacích prvků obsahu přidat vlastní ovládací prvky ContentPlaceHolder (stejně jako jiné značky). Vnořené stránky předlohy jsou poměrně užitečné ve velkých webových aplikacích, kde všechny stránky sdílí vzhled a atmosféru, ale některé oddíly lokality vyžadují jedinečné vlastní nastavení.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Vnořené stránky předloh ASP.NET](https://msdn.microsoft.com/library/x2b3ktt7.aspx)
- [Tipy pro vnořené stránky předloh a dobu návrhu VS 2005](https://weblogs.asp.net/scottgu/archive/2005/11/11/430382.aspx)
- [A podpora vnořené stránky předlohy VS 2008](https://weblogs.asp.net/scottgu/archive/2007/07/09/vs-2008-nested-master-page-support.aspx)

### <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 3,5 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672329972/4guysfromrollaco). Scott se dá kontaktovat [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](specifying-the-master-page-programmatically-cs.md)
> [Další](creating-a-site-wide-layout-using-master-pages-vb.md)

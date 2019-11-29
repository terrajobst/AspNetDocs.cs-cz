---
uid: web-forms/overview/older-versions-getting-started/master-pages/creating-a-site-wide-layout-using-master-pages-cs
title: Vytvoření rozložení v rámci webu pomocí stránek předlohy (C#) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se zobrazí základy hlavní stránky. To znamená, co jsou stránky předlohy, jak vytvoří hlavní stránku, co je to držitelé obsahu, jak provede jeden dobropis...
ms.author: riande
ms.date: 05/21/2008
ms.assetid: 78f8d194-03b9-44a5-8255-90e7cd1c2ee1
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/creating-a-site-wide-layout-using-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 1a5e85c443a2a3642ec185ab1897c43cdb2ab1f7
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74619516"
---
# <a name="creating-a-site-wide-layout-using-master-pages-c"></a>Vytvoření rozložení platného pro celý web pomocí stránek předlohy (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_01_CS.zip) nebo [stažení PDF](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_01_CS.pdf)

> V tomto kurzu se zobrazí základy hlavní stránky. To, co jsou stránky předlohy, jak vytvoří hlavní stránku, co jsou držitele obsahu, jak vytvoří stránku ASP.NET, která používá hlavní stránku, jak probíhá změna hlavní stránky, jak se automaticky projeví na svých přidružených stránkách obsahu a tak dále.

## <a name="introduction"></a>Úvod

Jeden atribut dobře navrženého webu je konzistentní rozložení stránky na úrovni webu. Vezměte si například web www.asp.net. V době psaní tohoto zápisu má každá stránka stejný obsah v horní a dolní části stránky. Jak ukazuje obrázek 1, v horní horní části každé stránky se zobrazuje šedý pruh se seznamem komunit Microsoftu. Pod tím je logo lokality, seznam jazyků, do kterých byl web přeložen, a základní oddíly: domů, začínáme, informace, soubory ke stažení a tak dále. Stejně tak dolní část stránky obsahuje informace o reklamě v www.asp.net, prohlášení o autorských právech a odkaz na prohlášení o zásadách ochrany osobních údajů.

[![web www.asp.net využívá konzistentní vzhled a chování napříč všemi stránkami.](creating-a-site-wide-layout-using-master-pages-cs/_static/image2.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image1.png)

<strong>Obrázek 01</strong>: web www.ASP.NET využívá konzistentní vzhled a chování napříč všemi stránkami ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-site-wide-layout-using-master-pages-cs/_static/image3.png)).

Dalším atributem dobře navržené lokality je jednoduchost, se kterým se dá změnit vzhled webu. Obrázek 1 zobrazuje domovskou stránku www.asp.net od března 2008, ale mezi teď a publikací tohoto kurzu se možná změnil vzhled a chování. Možná se položky nabídky podél horní části rozšíří, aby zahrnovaly nový oddíl pro rozhraní MVC. Nebo je možné, že se odsadí nový návrh s různými barvami, písmy a rozložením, představili. Použití takových změn u celého webu by mělo být rychlý a jednoduchý proces, který nevyžaduje úpravu tisíců webových stránek, které tvoří Web.

Vytváření šablony stránky na úrovni webu v ASP.NET je možné prostřednictvím použití *stránek předlohy*. Ve kostce je hlavní stránkou speciální typ stránky ASP.NET, která definuje kód, který je společný pro všechny *stránky obsahu* , i oblasti, které jsou přizpůsobitelné na základě stránky obsahu stránky po obsahu. (Stránka obsahu je stránka ASP.NET, která je svázána s hlavní stránkou.) Pokaždé, když se změní rozložení nebo formátování hlavní stránky, okamžitě se aktualizují všechny jeho výstup stránky obsahu, což usnadňuje aktualizaci a nasazení jednoho souboru (konkrétně stránky předlohy).

Toto je první kurz v sérii kurzů, které se probírají pomocí stránek předlohy. V průběhu této série kurzů jsme:

- Kontrola vytváření stránek předloh a jejich přidružených stránek obsahu
- Prodiskutujte celou řadu tipů, triky a depeší,
- Identifikujte společnou stránku nástrah a Prozkoumejte alternativní řešení.
- Podívejte se, jak získat přístup k hlavní stránce ze stránky obsahu a naopak,
- Naučte se, jak určit stránku předlohy stránky obsahu za běhu a
- Další témata upřesňujících stránek předlohy.

Tyto kurzy jsou stručné a poskytují podrobné pokyny s mnoha snímky obrazovky, které vás provedou procesem vizuálně. Každý kurz je k dispozici v C# a Visual Basic verzích a zahrnuje stažení kompletního používaného kódu.

Tento kurz konference začíná zobrazením základů stránky předlohy. Probereme, jak fungují stránky předlohy, podívejte se na téma Vytvoření stránky předlohy a přidružených obsahu pomocí nástroje Visual Web Developer a podívejte se, jak se změny na hlavní stránce projeví okamžitě na stránkách obsahu. Pojďme začít!

## <a name="understanding-how-master-pages-work"></a>Princip fungování stránek předlohy

Vytváření webu s konzistentním rozložením stránky v celém webu vyžaduje, aby každá webová stránka kromě vlastního obsahu generovala i společné formátovací značky. Například zatímco každý kurz nebo příspěvek fóra na www.asp.net má svůj vlastní jedinečný obsah, každá z těchto stránek také vykreslí řadu běžných `<div>` prvků, které zobrazují odkazy na nejvyšší úrovni: domů, začínáme, informace a tak dále.

Existují různé techniky pro vytváření webových stránek s konzistentním pohledem a chováním. Naive přístupem je jednoduše zkopírovat a vložit společné označení rozložení na všechny webové stránky, ale tento přístup má řadu downsides. U startů se při každém vytvoření nové stránky musíte pamatovat na zkopírování a vložení sdíleného obsahu na stránku. Tyto operace kopírování a vkládání jsou zralé kvůli chybě, protože můžete omylem zkopírovat pouze podmnožinu sdílených značek na novou stránku. A pokud ho chcete vypnout, tento přístup nahrazuje stávající vzhled v rámci nejrůznějších webů, protože každá jediná stránka v lokalitě musí být upravena, aby bylo možné nový vzhled a chování použít.

Před ASP.NET verze 2,0 vývojáři stránky často umístili společné značky v [uživatelských ovládacích prvcích](https://msdn.microsoft.com/library/y6wb1a0e.aspx) a pak přidali tyto uživatelské ovládací prvky na každou stránku a všechny stránky. Tento přístup vyžaduje, aby si vývojář stránky ručně přidal uživatelské ovládací prvky na všechny nové stránky, ale povolily se pro snazší úpravy v rámci lokality, protože když aktualizujete společné značky, stačí, když aktualizujete Common Markup pouze uživatelské ovládací prvky, které je třeba upravit. Ale Visual Studio .NET 2002 a 2003 – verze sady Visual Studio použité k vytváření ASP.NETch aplikací s 1. x – vykreslené uživatelské ovládací prvky v zobrazení Návrh jako šedá pole. V důsledku toho nezpůsobí vývojáři stránek použití tohoto přístupu prostředí WYSIWYG v době návrhu.

Nedostatky použití uživatelských ovládacích prvků byly řešeny v ASP.NET verze 2,0 a Visual Studio 2005 pomocí úvodních *stránek předlohy*. Stránka předlohy je speciální typ stránky ASP.NET, která definuje značky v rámci lokality i *oblasti* , kde přidružené *stránky obsahu* definují vlastní značky. Jak uvidíme v kroku 1, tyto oblasti jsou definovány ovládacími prvky ContentPlaceHolder. Ovládací prvek ContentPlaceHolder jednoduše označuje pozici v hierarchii ovládacích prvků hlavní stránky, kde může být vlastní obsah vložen pomocí stránky obsahu.

> [!NOTE]
> Základní koncepty a funkce hlavních stránek se od verze 2,0 ASP.NET nezměnily. Visual Studio 2008 však nabízí podporu pro vnořené stránky předloh, což je funkce, která v aplikaci Visual Studio 2005 chyběla. V budoucím kurzu se podíváme na použití vnořených stránek předlohy.

Obrázek 2 ukazuje, jak může vypadat hlavní stránka www.asp.net. Všimněte si, že stránka předlohy definuje společné rozložení na úrovni webu – značky v horním, dolním a pravé straně každé stránky a také ovládací prvek ContentPlaceHolder v prostřední levé straně, kde se nachází jedinečný obsah pro každou jednotlivou webovou stránku.

![Stránka předlohy definuje rozložení na úrovni webu a oblasti, které lze upravovat na stránce obsahu – podle obsahu.](creating-a-site-wide-layout-using-master-pages-cs/_static/image4.png)

**Obrázek 02**: Stránka předlohy definuje rozložení na úrovni webu a oblasti, které lze upravovat na stránce obsahu – podle obsahu stránky.

Po definování hlavní stránky může být vazba na nové stránky ASP.NET pomocí zaškrtnutí políčka. Tyto stránky ASP.NET – označované jako stránky obsahu – obsahují ovládací prvek obsahu pro každé ovládací prvky ContentPlaceHolder na stránce předlohy. Když se stránka obsahu navštíví prostřednictvím prohlížeče, modul ASP.NET vytvoří hierarchii ovládacích prvků hlavní stránky a vloží hierarchii ovládacích prvků stránky obsahu na příslušné místo. Tato kombinovaná hierarchie ovládacích prvků se vykreslí a výsledný HTML se vrátí do prohlížeče koncového uživatele. V důsledku toho stránka obsahu vygeneruje společné značky definované v jeho hlavní stránce mimo ovládací prvky ContentPlaceHolder a označení stránky definované v rámci svých vlastních ovládacích prvků obsahu. Tento koncept znázorňuje obrázek 3.

[![se značky požadované stránky zatavené na stránku předlohy](creating-a-site-wide-layout-using-master-pages-cs/_static/image6.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image5.png)

**Obrázek 03**: vyžádané označení stránky je pokryto na stránce předlohy ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-site-wide-layout-using-master-pages-cs/_static/image7.png)

Teď, když jsme probrali, jak fungují stránky předloh, se podívejme na vytváření předloh a přidružených stránek obsahu pomocí nástroje Visual Web Developer.

> [!NOTE]
> Aby bylo možné oslovit nejširší možnou cílovou skupinu, web ASP.NET, který sestavíme v této sérii kurzů, se vytvoří pomocí ASP.NET 3,5 s bezplatnou verzí sady Visual Studio 2008 společnosti Microsoft, která je v sadě Visual Studio, [Visual Web Developer 2008](https://www.microsoft.com/express/vwd/). Pokud jste ještě neupgradovali na ASP.NET 3,5, nedělejte si starosti – koncepty popsané v těchto kurzech fungují stejně dobře i s ASP.NET 2,0 a sadou Visual Studio 2005. Některé ukázkové aplikace ale můžou používat nové funkce .NET Framework verze 3,5; Při použití specifických funkcí 3,5 jsem si všimněte, že je popsán postup implementace podobných funkcí ve verzi 2,0. Mějte na paměti, že ukázkové aplikace, které jsou k dispozici ke stažení z každého kurzu, cílí na .NET Framework verze 3,5, což vede k `Web.config` souboru, který obsahuje prvky konfigurace specifické pro 3,5 a odkazy na obory názvů specifické pro 3,5 v příkazech `using` v třídách kódu na pozadí stránek ASP.NET. Dlouhý příběh – Pokud jste ještě na svém počítači nainstalovali .NET 3,5, nebude webová aplikace ke stažení fungovat, aniž byste nejdřív odebrali značku 3,5 určenou z `Web.config`. Další informace o tomto tématu najdete v článku o [deprotínající se `Web.config` souboru verze 3.5 pro ASP.NET](http://www.4guysfromrolla.com/articles/121207-1.aspx) . Také budete muset odebrat `using` příkazy, které odkazují na obory názvů specifické pro 3,5.

## <a name="step-1-creating-a-master-page"></a>Krok 1: vytvoření hlavní stránky

Než budeme moct prozkoumat vytváření a používání stránek hlavní a obsah, musíme nejdřív potřebovat web ASP.NET. Začněte vytvořením nového webu ASP.NET založeného na systému souborů. Chcete-li to provést, spusťte Visual Web Developer a pak přejděte do nabídky soubor a zvolte možnost Nový web a zobrazí se dialogové okno Nový web (viz obrázek 4). Vyberte šablonu webu ASP.NET, nastavte rozevírací seznam umístění na systém souborů, vyberte složku, kam chcete umístit web, a nastavte jazyk na C#. Tím se vytvoří nový web s `Default.aspx` stránkou ASP.NET, `App_Data` složkou a souborem `Web.config`.

> [!NOTE]
> Visual Studio podporuje dva režimy řízení projektů: projekty webu a projekty webových aplikací. Webové projekty neobsahují soubor projektu, zatímco projekty webové aplikace napodobují architekturu projektu v aplikaci Visual Studio .NET 2002/2003 – obsahují soubor projektu a zkompiluje zdrojový kód projektu do jednoho sestavení, které je umístěno ve složce `/bin`. Visual Studio 2005 zpočátku podporuje jenom webové projekty, i když se [model projektu webové aplikace](https://msdn.microsoft.com/library/aa730880(vs.80).aspx) znovu představil s aktualizací Service Pack 1. Visual Studio 2008 nabízí jak modely projektu. Edice Visual Web Developer 2005 a 2008 však podporují pouze projekty webu. Používám model projektu webu pro moje ukázky v této sérii kurzů. Pokud používáte jinou edici než Express a chcete místo toho použít model projektu webové aplikace, můžete to udělat, ale mějte na paměti, že mezi tím, co vidíte na obrazovce, a kroky, které je třeba vzít v úvahu, se může stát, že se zobrazují a instructioé snímky obrazovky. NS dodané v těchto kurzech.

[![vytvoření nového webu založeného na systému souborů](creating-a-site-wide-layout-using-master-pages-cs/_static/image9.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image8.png)

**Obrázek 04**: vytvoření nového webu založeného na systému souborů ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-site-wide-layout-using-master-pages-cs/_static/image10.png))

V dalším kroku přidejte do kořenového adresáře stránku předlohy kliknutím pravým tlačítkem myši na název projektu, zvolením možnosti Přidat novou položku a výběrem šablony stránky předlohy. Všimněte si, že stránky předlohy končí rozšířením `.master`. Pojmenujte tuto novou stránku předlohy `Site.master` a klikněte na Přidat.

[![přidat hlavní stránku s názvem site. Master na web](creating-a-site-wide-layout-using-master-pages-cs/_static/image12.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image11.png)

**Obrázek 05**: přidejte do webu stránku předlohy s názvem `Site.master` ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-site-wide-layout-using-master-pages-cs/_static/image13.png)

Přidání nového souboru hlavní stránky pomocí nástroje Visual Web Developer vytvoří hlavní stránku s následujícím deklarativním označením:

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample1.aspx)]

První řádek v deklarativní značce označení je [direktiva`@Master`](https://msdn.microsoft.com/library/ms228176.aspx). Direktiva `@Master` je podobná [direktivě`@Page`](https://msdn.microsoft.com/library/ydy4x04a.aspx) , která se zobrazuje na stránkách ASP.NET. Definuje jazyk na straně serveru (C#) a informace o umístění a dědičnosti třídy kódu na pozadí hlavní stránky.

`DOCTYPE` a deklarativní označení stránky se zobrazí pod direktivou `@Master`. Stránka obsahuje statický kód HTML spolu se čtyřmi serverovými ovládacími prvky:

- **Webový formulář (`<form runat="server">`)** – protože všechny stránky ASP.NET mají typicky webový formulář – a protože stránka předlohy může obsahovat webové ovládací prvky, které se musí objevit v rámci webového formuláře – nezapomeňte přidat webový formulář na stránku předlohy (místo přidání webového formuláře na každou stránku obsahu).
- **Ovládací prvek ContentPlaceHolder s názvem `ContentPlaceHolder1`** – tento ovládací prvek ContentPlaceHolder se zobrazí v rámci webového formuláře a slouží jako oblast pro uživatelské rozhraní stránky obsahu.
- **`<head>` element na straně serveru** – `<head>` prvek má atribut `runat="server"`, který ho zpřístupní prostřednictvím kódu na straně serveru. `<head>` prvek je implementován tímto způsobem, aby bylo možné přidat nebo upravit název stránky a jiné značky `<head>`. Například nastavení vlastnosti `Title` stránky ASP.NET mění prvek `<title>` vykreslený ovládacím prvkem `<head>` Server.
- **Ovládací prvek ContentPlaceHolder nazvaný `head`** – tento ovládací prvek ContentPlaceHolder se zobrazí v ovládacím prvku `<head>` Server a lze jej použít k deklarativnímu přidání obsahu do `<head>` elementu.

Tato výchozí hlavní stránka je deklarativní označení slouží jako výchozí bod pro návrh vlastních stránek předlohy. Můžete upravovat kód HTML nebo přidat další webové ovládací prvky nebo prvky ContentPlaceHoldery na stránku předlohy.

> [!NOTE]
> Při návrhu stránky předlohy se ujistěte, že stránka předlohy obsahuje webový formulář a že v tomto webovém formuláři se zobrazí alespoň jeden ovládací prvek ContentPlaceHolder.

### <a name="creating-a-simple-site-layout"></a>Vytvoření jednoduchého rozložení webu

Nyní rozbalíme výchozí deklarativní označení `Site.master`k vytvoření rozložení lokality, kde všechny stránky sdílí: společné záhlaví; levý sloupec s navigací, novinkami a dalším obsahem na úrovni webu; a zápatí, které zobrazuje ikonu "používá se Microsoft ASP.NET". Obrázek 6 znázorňuje konečný výsledek stránky předlohy, když se jedna z jeho stránek obsahu zobrazí v prohlížeči. Oblast červeného kruhu na obrázku 6 je specifická pro navštívenou stránku (`Default.aspx`); druhý obsah je definován na stránce předlohy, a proto je konzistentní napříč všemi stránkami obsahu.

[![stránka předlohy definuje označení pro horní, levou a dolní část.](creating-a-site-wide-layout-using-master-pages-cs/_static/image15.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image14.png)

**Obrázek 6**: Stránka předlohy definuje označení pro horní, levou a dolní část ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-site-wide-layout-using-master-pages-cs/_static/image16.png)).

Chcete-li dosáhnout rozložení lokality na obrázku 6, začněte aktualizací stránky předlohy `Site.master` tak, aby obsahovala následující deklarativní označení:

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample2.aspx)]

Rozložení stránky předlohy je definováno pomocí řady `<div>` prvků jazyka HTML. `topContent` `<div>` obsahuje značku, která se zobrazí v horní části každé stránky, zatímco `mainContent`, `leftContent`a `footerContent` `<div>` s slouží k zobrazení obsahu stránky, levého sloupce a ikony "napájeno z Microsoft ASP.NET" v uvedeném pořadí. Kromě přidání těchto prvků `<div>` také přejmenováni vlastnost `ID` primárního ovládacího prvku ContentPlaceHolder z `ContentPlaceHolder1` na `MainContent`.

Pravidla formátování a rozložení pro tyto položky roztříděné `<div>` prvky jsou v souboru [CSS (Cascading StyleSheet)](http://en.wikipedia.org/wiki/Cascading_Style_Sheets) `Styles.css`, který je zadán prostřednictvím elementu &lt;odkaz&gt; prvku na &lt;Head&gt; elementu stránky předlohy. Tato různá pravidla definují vzhled a chování každého prvku `<div>` uvedeného výše. Například prvek `topContent` `<div>`, který zobrazuje text "kurzy stránek předlohy" a odkaz na jeho pravidla formátování určená v `Styles.css` následujícím způsobem:

[!code-css[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample3.css)]

Pokud jste na svém počítači, budete si muset stáhnout doprovodný kód tohoto kurzu a přidat soubor `Styles.css` do projektu. Podobně také budete muset vytvořit složku s názvem images a zkopírovat ikonu "používá se Microsoft ASP.NET" ze staženého ukázkového webu do vašeho projektu.

> [!NOTE]
> Diskuze o formátování šablon stylů CSS a webových stránek překračuje rámec tohoto článku. Další informace o šablonách stylů CSS najdete v [kurzech šablon stylů CSS](http://www.w3schools.com/css/default.asp) na adrese [w3schools.com](http://www.w3schools.com/). Můžu také povzbudit, abyste si stáhli doprovodný kód tohoto kurzu a nahráli s nastaveními CSS v `Styles.css`, abyste viděli účinky různých pravidel formátování.

### <a name="creating-a-master-page-using-an-existing-design-template"></a>Vytvoření hlavní stránky pomocí existující šablony návrhu

V průběhu let jsem sestavil řadu webových aplikací ASP.NET pro malé až střední společnosti. Někteří moji klienti mají existující rozložení lokality, které chtěli použít; jiní uživatelé mají příslušného návrháře grafiky. Několik svěřených mě pro návrh rozložení webu. Jak je znázorněno na obrázku 6, úkoly programátora pro návrh rozložení webu se obvykle považují za to, že váš účet bude mít otevřený – srdce chirurgie, zatímco váš lékař vaše daně provádí.

Naštěstí je k dispozici několik webů, které nabízejí bezplatné šablony návrhu HTML – Google vrátilo více než 6 000 000 výsledků pro hledaný termín "bezplatné šablony webu". Jedna z oblíbených položek je [OpenDesigns.org](http://opendesigns.org/). Jakmile najdete šablonu webu, kterou chcete, přidejte soubory CSS a obrázky do projektu webu a integrujte HTML šablony do své stránky předlohy.

> [!NOTE]
> Microsoft taky nabízí řadu [bezplatných šablon ASP.NET design Kit](https://msdn.microsoft.com/asp.net/aa336613.aspx) , které se integrují do dialogového okna Nový web v sadě Visual Studio.

## <a name="step-2-creating-associated-content-pages"></a>Krok 2: vytvoření přidružených stránek obsahu

Po vytvoření stránky předlohy jsme připraveni začít vytvářet ASP.NET stránky, které jsou svázané se stránkou předlohy. Tyto stránky se označují jako *stránky obsahu*.

Pojďme přidat novou ASP.NET stránku do projektu a vytvořit její vazby na stránku předlohy `Site.master`. V Průzkumník řešení klikněte pravým tlačítkem myši na název projektu a vyberte možnost Přidat novou položku. Vyberte šablonu webového formuláře, zadejte název `About.aspx`a potom zaškrtněte políčko "vybrat hlavní stránku", jak je znázorněno na obrázku 7. Tím se zobrazí dialogové okno Výběr stránky předlohy (viz obrázek 8), ze kterého můžete zvolit předlohovou stránku, kterou chcete použít.

> [!NOTE]
> Pokud jste web ASP.NET vytvořili pomocí modelu projektu webové aplikace namísto modelu projektu webu, nezobrazí se v dialogovém okně Přidat novou položku zobrazená na obrázku 7 zaškrtávací políčko vybrat hlavní stránku. Chcete-li vytvořit stránku obsahu při použití modelu projektu webové aplikace, musíte zvolit šablonu formuláře webového obsahu místo šablony webového formuláře. Po výběru šablony formuláře webového obsahu a kliknutí na tlačítko Přidat se zobrazí dialogové okno Výběr stránky předlohy zobrazené na obrázku 8.

[![přidání nové stránky obsahu](creating-a-site-wide-layout-using-master-pages-cs/_static/image18.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image17.png)

**Obrázek 07**: Přidání nové stránky obsahu ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-site-wide-layout-using-master-pages-cs/_static/image19.png))

[![vybrat hlavní stránku site. Master.](creating-a-site-wide-layout-using-master-pages-cs/_static/image21.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image20.png)

**Obrázek 08**: Výběr stránky předlohy `Site.master` ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-site-wide-layout-using-master-pages-cs/_static/image22.png))

Jak ukazuje následující deklarativní kód, nová stránka obsahu obsahuje direktivu `@Page`, která odkazuje zpět na svou hlavní stránku a ovládací prvek obsahu pro každé ovládací prvky ContentPlaceHolder stránky předlohy.

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample4.aspx)]

> [!NOTE]
> V části "Vytvoření jednoduchého rozložení lokality" v kroku 1 byl přejmenován `ContentPlaceHolder1` na `MainContent`. Pokud jste nezměnili přejmenování tohoto `ID` ovládacího prvku ContentPlaceHolder stejným způsobem, deklarativní označení stránky obsahu se mírně liší od označení uvedeného výše. To znamená, že druhý `ContentPlaceHolderID` ovládacího prvku obsahu bude odrážet `ID` odpovídajícího ovládacího prvku ContentPlaceHolder na stránce předlohy.

Při vykreslování stránky obsahu musí modul ASP.NET pořídit ovládací prvky obsahu stránky ovládacími prvky ContentPlaceHolder stránky předlohy. Modul ASP.NET určuje stránku předlohy stránky obsahu z atributu `MasterPageFile` direktivy `@Page`. Jak je uvedeno výše, je tato stránka obsahu svázána s `~/Site.master`.

Vzhledem k tomu, že stránka předlohy obsahuje dva ovládací prvky ContentPlaceHolder-`head` a `MainContent`-vizuální webový vývojář vygeneroval dva ovládací prvky obsahu. Každý ovládací prvek obsahu odkazuje na konkrétní prvek ContentPlaceHolder prostřednictvím jeho vlastnosti `ContentPlaceHolderID`.

Kde stránky předlohy vychází z předchozích technik šablon na úrovni webu, je jejich podpora v době návrhu. Obrázek 9 ukazuje stránku `About.aspx` obsahu při zobrazení pomocí zobrazení Návrh aplikace Visual Web Developer. Všimněte si, že když je obsah stránky předlohy viditelný, je zobrazen šedě a nelze jej upravit. Ovládací prvky obsahu odpovídající prvkům ContentPlaceHolder stránky předlohy jsou však editovatelné. A stejně jako u jakékoli jiné stránky ASP.NET můžete vytvořit rozhraní stránky obsahu přidáním webových ovládacích prvků prostřednictvím zobrazení zdroje nebo návrh.

[![zobrazení návrhu stránky obsahu se zobrazí obsah pro stránku a stránku předlohy pro konkrétní stránku.](creating-a-site-wide-layout-using-master-pages-cs/_static/image24.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image23.png)

**Obrázek 09**: návrhové zobrazení stránky obsahu zobrazuje obsah stránky a stránky předlohy ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-site-wide-layout-using-master-pages-cs/_static/image25.png)).

### <a name="adding-markup-and-web-controls-to-the-content-page"></a>Přidání značek a webových ovládacích prvků na stránku obsahu

Chvíli vytvořte nějaký obsah pro stránku `About.aspx`. Jak vidíte na obrázku 10, zadali jsme nadpis "o autorovi" a několik odstavců textu, ale můžete také volně přidávat webové ovládací prvky. Po vytvoření tohoto rozhraní navštivte stránku `About.aspx` v prohlížeči.

[![stránku About. aspx najdete v prohlížeči.](creating-a-site-wide-layout-using-master-pages-cs/_static/image27.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image26.png)

**Obrázek 10**: navštivte stránku `About.aspx` v prohlížeči ([kliknutím zobrazíte obrázek v plné velikosti](creating-a-site-wide-layout-using-master-pages-cs/_static/image28.png)).

Je důležité pochopit, že požadovaná stránka obsahu a její přidružená stránka předlohy jsou pojistá a vykreslená na webovém serveru jako celek. V prohlížeči koncového uživatele se pak pošle výsledný pojistka HTML. Pokud to chcete ověřit, zobrazte HTML přijatý prohlížečem tak, že v nabídce zobrazení kliknete na možnost zdroj. Všimněte si, že neexistují žádné rámce ani žádné jiné specializované postupy pro zobrazení dvou různých webových stránek v jednom okně.

### <a name="binding-a-master-page-to-an-existing-aspnet-page"></a>Navázání stránky předlohy na existující stránku ASP.NET

Jak jsme viděli v tomto kroku, přidání nové stránky obsahu do webové aplikace ASP.NET je tak jednoduché, protože kontroluje zaškrtnutí políčka "vybrat hlavní stránku" a výběr stránky předlohy. Bohužel převod stávající stránky ASP.NET na hlavní stránku není tak snadné.

K navázání stránky předlohy na existující stránku ASP.NET je třeba provést následující kroky:

1. Přidejte atribut `MasterPageFile` k direktivě `@Page` stránky ASP.NET, na kterou odkazuje na příslušnou stránku předlohy.
2. Přidejte ovládací prvky obsahu pro každý prvek ContentPlaceHolder na stránce předlohy.
3. Selektivně vyjměte a vložte existující obsah stránky ASP.NET do odpovídajících ovládacích prvků obsahu. Jsem tady říká "selektivní", protože stránka ASP.NET pravděpodobně obsahuje kód, který je již vyjádřený stránkou předlohy, jako je například `DOCTYPE`, `<html>` prvek a webový formulář.

Podrobné pokyny k tomuto procesu spolu se snímky obrazovky najdete v kurzu [Guthrie](https://weblogs.asp.net/scottgu/) [používání stránek předlohy a navigace na webu](http://webproject.scottgu.com/CSharp/MasterPages/MasterPages.aspx) . Podrobné informace o tomto postupu najdete v části aktualizace `Default.aspx` a `DataSample.aspx` použití stránky předlohy.

Vzhledem k tomu, že je mnohem snazší vytvořit nové stránky obsahu, než je převod existujících ASP.NET stránek na stránky obsahu, doporučujeme, abyste při každém vytvoření nového webu ASP.NET přidali do lokality hlavní stránku. Vytvoří vazby všech nových ASP.NET stránek na tuto stránku předlohy. Nedělejte si starosti, pokud je počáteční hlavní stránka velmi jednoduchá nebo prostá. stránku předlohy můžete aktualizovat později.

> [!NOTE]
> Při vytváření nové aplikace ASP.NET `Default.aspx` přidá Visual Web Developer stránku, která není svázána s hlavní stránkou. Pokud chcete procvičit převod stávající stránky ASP.NET na stránku obsahu, pokračujte a udělejte to pomocí `Default.aspx`. Alternativně můžete odstranit `Default.aspx` a pak je znovu přidat, ale tentokrát kontrolujete zaškrtnutí políčka "vybrat hlavní stránku".

## <a name="step-3-updating-the-master-pages-markup"></a>Krok 3: aktualizace značek stránky předlohy

Jednou z hlavních výhod stránek předloh je, že k definování celkového rozložení pro celou řadu stránek na webu můžete použít jednu hlavní stránku. Proto aktualizace vzhledu lokality a chování vyžaduje aktualizaci jednoho souboru – hlavní stránka.

Pro ilustraci tohoto chování aktualizujeme naši hlavní stránku tak, aby obsahovala aktuální datum v horní části levého sloupce. Přidejte popisek s názvem `DateDisplay` do `<div>``leftContent`.

[!code-aspx[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample5.aspx)]

Dále vytvořte obslužnou rutinu události `Page_Load` pro stránku předlohy a přidejte následující kód:

[!code-csharp[Main](creating-a-site-wide-layout-using-master-pages-cs/samples/sample6.cs)]

Výše uvedený kód nastaví vlastnost `Text` popisku na aktuální datum a čas zformátovaný jako den v týdnu, název měsíce a den se dvěma číslicemi (viz obrázek 11). Pomocí této změny znovu navštivte jednu z vašich stránek obsahu. Jak ukazuje obrázek 11, výsledné označení je okamžitě aktualizováno, aby zahrnovalo změnu na stránku předlohy.

[Při zobrazení stránky obsahu se projeví ![změny na stránce předlohy.](creating-a-site-wide-layout-using-master-pages-cs/_static/image30.png)](creating-a-site-wide-layout-using-master-pages-cs/_static/image29.png)

**Obrázek 11**: při zobrazení stránky obsahu se projeví změny na stránce předlohy ([kliknutím zobrazíte obrázek v plné velikosti).](creating-a-site-wide-layout-using-master-pages-cs/_static/image31.png)

> [!NOTE]
> Jak ukazuje tento příklad, stránky předlohy mohou obsahovat webové ovládací prvky na straně serveru, kód a obslužné rutiny událostí.

## <a name="summary"></a>Přehled

Stránky předlohy umožňují vývojářům ASP.NET navrhovat konzistentní rozložení v rámci webu, které je snadno aktualizovatelné. Vytváření stránek předloh a jejich přidružených stránek obsahu je jednoduché jako vytváření standardních ASP.NET stránek, protože Visual Web Developer nabízí bohatou podporu při návrhu.

Příklad stránky předlohy, kterou jsme vytvořili v tomto kurzu, obsahoval dva ovládací prvky ContentPlaceHolder, `head` a `MainContent`. Do naší stránky obsahu jsme ale uvedli jenom označení pro `MainContent` ovládací prvek ContentPlaceHolder. V dalším kurzu se podíváme na použití více ovládacích prvků obsahu na stránce obsahu. Také se naučíte, jak definovat výchozí značky pro ovládací prvky obsahu v rámci stránky předlohy, a jak přepínat mezi použitím výchozího kódu definovaného na stránce předlohy a poskytováním vlastního kódu ze stránky obsahu.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [ASP.NET pro návrháře: Bezplatné šablony návrhu a pokyny k vytváření webů ASP.NET pomocí webových standardů](https://msdn.microsoft.com/asp.net/aa336602.aspx)
- [ASP.NET hlavní stránky – přehled](https://msdn.microsoft.com/library/wtxbf3hh.aspx)
- [Pokyny pro kaskádové šablony stylů (CSS)](http://www.w3schools.com/css/default.asp)
- [Dynamické nastavení názvu stránky](http://aspnet.4guysfromrolla.com/articles/051006-1.aspx)
- [Stránky předlohy v ASP.NET](http://www.odetocode.com/articles/419.aspx)
- [Kurzy rychlý Start stránek předloh](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/masterpages/default.aspx)

### <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 3,5 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Scott se dá kontaktovat [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky

Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com).

> [!div class="step-by-step"]
> [Next](multiple-contentplaceholders-and-default-content-cs.md)

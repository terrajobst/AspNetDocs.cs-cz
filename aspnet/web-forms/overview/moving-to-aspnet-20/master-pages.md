---
uid: web-forms/overview/moving-to-aspnet-20/master-pages
title: Stránky předlohy | Microsoft Docs
author: microsoft
description: Jedna z klíčových součástí úspěšného webu je konzistentní vzhled a chování. V ASP.NET 1. x vývojáři používali uživatelské ovládací prvky pro replikaci běžné stránky elem...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 9c0cce4d-efd9-4c14-b0e8-a1a140abb3f4
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/master-pages
msc.type: authoredcontent
ms.openlocfilehash: 36f2caf7c2c9bcafd22c8f6681c1d6b19fe5078a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78567331"
---
# <a name="master-pages"></a>Stránky předlohy

od [Microsoftu](https://github.com/microsoft)

> Jedna z klíčových součástí úspěšného webu je konzistentní vzhled a chování. V ASP.NET 1. x vývojáři používali uživatelské ovládací prvky pro replikaci běžných prvků stránky napříč webovou aplikací. I když je to určitě funkční, používá uživatelské ovládací prvky nějaké nevýhody. Například změna pozice uživatelského ovládacího prvku vyžaduje změnu na více stránkách v rámci lokality. Uživatelské ovládací prvky nejsou vykreslovány v zobrazení Návrh po vložení na stránku.

Jedna z klíčových součástí úspěšného webu je konzistentní vzhled a chování. V ASP.NET 1. x vývojáři používali uživatelské ovládací prvky pro replikaci běžných prvků stránky napříč webovou aplikací. I když je to určitě funkční, používá uživatelské ovládací prvky nějaké nevýhody. Například změna pozice uživatelského ovládacího prvku vyžaduje změnu na více stránkách v rámci lokality. Uživatelské ovládací prvky nejsou vykreslovány v zobrazení Návrh po vložení na stránku.

ASP.NET 2,0 zavádí stránky předlohy jako způsob zachování konzistentního vzhledu a chování, jak budete brzy vidět, stránky předlohy představují významné vylepšení nad metodou uživatelského ovládacího prvku.

## <a name="why-master-pages"></a>Proč stránky předlohy?

Možná vás zajímá, proč byly stránky předlohy potřeba v ASP.NET 2,0. Po všech webech již vývojáři webů používají uživatelské ovládací prvky v ASP.NET 1. x ke sdílení oblastí obsahu mezi stránkami. Existuje několik důvodů, proč jsou uživatelské ovládací prvky řešením pro vytváření společného rozložení méně než optimální.

Uživatelské ovládací prvky ve skutečnosti nedefinují rozložení stránky. Místo toho definují rozložení a funkčnost pro část stránky. Rozdíl mezi těmito dvěma je důležitý, protože usnadňuje správu řešení uživatelského ovládacího prvku mnohem obtížnější. Například pokud chcete změnit pozici uživatelského ovládacího prvku na stránce, musíte upravit aktuální stránku, na které se uživatelský ovládací prvek zobrazuje. To je dobré, pokud máte jenom pár stránek, ale ve velkých lokalitách se rychle stávají Nightmare správy webů!

Další nevýhodou použití uživatelských ovládacích prvků pro definování společného rozložení je kořenová architektura ASP.NET sama o sobě. Pokud je některý veřejný člen uživatelského ovládacího prvku změněn, je nutné znovu kompilovat všechny stránky, které používají uživatelský ovládací prvek. ASP.NET pak znovu vytvoří JIT stránky při prvním použití. Jednou z nich vznikne neškálovatelná architektura a problém správy lokality pro větší weby.

Oba tyto problémy (a mnoho dalších) jsou řešeny stránkami předlohy v ASP.NET 2,0.

## <a name="how-master-pages-work"></a>Jak fungují stránky předlohy

Stránka předlohy je podobná šabloně pro jiné stránky. Prvky stránky, které by měly být sdíleny mezi ostatními stránkami (tj. nabídky, ohraničení atd.), jsou přidány do stránky předlohy. Když jsou do webu přidány nové stránky, můžete je přidružit k hlavní stránce. Stránka, která je přidružena k hlavní stránce, se nazývá **stránka obsahu**. Ve výchozím nastavení se stránka obsahu převezme na základě vzhledu stránky předlohy. Při vytváření stránky předlohy ale můžete definovat části stránky, které může stránka obsahu nahradit vlastním obsahem. Tyto části jsou definované pomocí nového ovládacího prvku zavedeného v ASP.NET 2,0; ovládací prvek **ContentPlaceHolder**

Stránka předlohy může obsahovat libovolný počet ovládacích prvků ContentPlaceHolder (nebo žádný vůbec). Na stránce obsah se zobrazí obsah z ovládacích prvků ContentPlaceHolder v ovládacích prvcích **obsahu** , další nový ovládací prvek v ASP.NET 2,0. Ve výchozím nastavení jsou ovládací prvky obsahu stránky obsahu prázdné, takže můžete poskytovat vlastní obsah. Pokud chcete použít obsah ze stránky předlohy v rámci ovládacích prvků obsahu, můžete tak učinit, protože se později zobrazí v tomto modulu. Ovládací prvek obsahu je namapován na ovládací prvek ContentPlaceHolder prostřednictvím atributu ContentPlaceHolderID ovládacího prvku Content. Následující kód mapuje ovládací prvek obsahu na ovládací prvek ContentPlaceHolder s názvem mainBody na stránce předlohy.

[!code-aspx[Main](master-pages/samples/sample1.aspx)]

> [!NOTE]
> Často uslyšíte, že uživatelé popisují stránky předlohy jako základní třídu pro jiné stránky. Které ve skutečnosti nejsou pravdivé. Vztah mezi stránkami předloh a stránkami obsahu není jedním z dědičnosti.

**Obrázek 1** ukazuje stránku předlohy a přidruženou stránku obsahu, jak se zobrazují v aplikaci Visual Studio 2005. Ovládací prvek ContentPlaceHolder lze zobrazit na stránce předlohy a odpovídající ovládací prvek obsahu na stránce obsah. Všimněte si, že obsah stránek předlohy, který je mimo prvek ContentPlaceHolder, je viditelný, ale šedý na stránce obsahu. Stránka obsahu může supplanted jenom obsah uvnitř ovládacího prvku ContentPlaceHolder. Veškerý další obsah, který pochází ze stránky předlohy, je neměnný.

![Stránka předlohy a její přidružená stránka obsahu](master-pages/_static/image1.jpg)

**Obrázek 1**: Stránka předlohy a její přidružená stránka obsahu

## <a name="creating-a-master-page"></a>Vytvoření stránky předlohy

Vytvoření nové stránky předlohy:

1. Otevřete Visual Studio 2005 a vytvořte nový web.
2. Klikněte na soubor, nový, soubor.
3. V dialogovém okně Přidat novou položku vyberte hlavní soubor, jak je znázorněno na **obrázku 2**.
4. Klikněte na Přidat.

![Vytvoření nové stránky předlohy](master-pages/_static/image2.jpg)

**Obrázek 2**: vytvoření nové stránky předlohy

Všimněte si, že Přípona souboru hlavní stránky je *. Master*. Jedná se o jeden ze způsobů, které se hlavní stránka od obyčejné stránky liší. Druhým hlavním rozdílem je to, že místo direktivy @Page obsahuje stránka předloha direktivu @Master. Přepněte do zobrazení zdroje pro stránku předlohy, kterou jste právě vytvořili, a Prohlédněte si kód.

Ve výchozím nastavení bude mít nová stránka předlohy jeden ovládací prvek ContentPlaceHolder. Ve většině případů je vhodnější vytvořit nejprve běžné prvky stránky a pak vkládat ovládací prvky ContentPlaceHolder, kde je požadován vlastní obsah. V těchto případech budou vývojáři chtít odstranit výchozí ovládací prvek ContentPlaceHolder a vkládat nové při vývoji stránky. Ovládací prvky ContentPlaceHolder nelze měnit bez ohledu na to, že se zobrazí úchyty pro změnu velikosti. Ovládací prvky ContentPlaceHolder velikost jsou automaticky založeny na obsahu, který obsahuje jedinou výjimku; Umístíte-li ovládací prvek ContentPlaceHolder do bloku elementu, jako je například buňka tabulky, bude velikost podle velikosti elementu.

## <a name="lab-1-working-with-master-pages"></a>Testovací prostředí 1 pracuje se stránkami předlohy

V tomto testovacím prostředí vytvoříte novou stránku předlohy a definujete tři ovládací prvky ContentPlaceHolder. Pak vytvoříte novou stránku obsahu a nahradíte obsah alespoň jedním ovládacím prvkům ContentPlaceHolder.

1. Vytvořte hlavní stránku a vložte ovládací prvky ContentPlaceHolder. 

    1. Vytvořte novou stránku předlohy, jak je popsáno výše.
    2. Odstraní výchozí ovládací prvek ContentPlaceHolder.
    3. Vyberte ovládací prvek ContentPlaceHolder tím, že kliknete na horní ohraničení ovládacího prvku a pak ho odstraníte stisknutím klávesy DEL na klávesnici.
    4. Vložte novou tabulku pomocí šablony *záhlaví a strany* , jak je znázorněno na obrázku 3. Změňte šířku a výšku na 90%, aby byla celá tabulka viditelná v návrháři.

![](master-pages/_static/image3.jpg)

**Obrázek 3**

1. Umístěte kurzor do každé buňky tabulky a nastavte vlastnost *VAlign* na *Top*.
2. V sadě nástrojů vložte ovládací prvek ContentPlaceHolder do horní buňky tabulky (buňka záhlaví).
3. Když vložíte tento ovládací prvek ContentPlaceHolder, Všimněte si, že výška řádku bude trvat téměř celou stránku, jak je znázorněno na obrázku 4. V tomto okamžiku se na to netýkají.

![Prázdné místo je ve stejné buňce jako ContentPlaceHolder](master-pages/_static/image1.gif)

**Obrázek 4**: prázdné místo je ve stejné buňce jako prvek ContentPlaceHolder

1. Umístěte ovládací prvek ContentPlaceHolder do ostatních dvou buněk. Po vložení dalších ovládacích prvků ContentPlaceHolder by měla být velikost buněk tabulky tak, jak byste očekávali. Stránka by teď měla vypadat jako stránka zobrazená na **obrázku 5**.

![Hlavní seznam se všemi ovládacími prvky ContentPlaceHolder. Všimněte si, že výška buňky pro buňku záhlaví je teď.](master-pages/_static/image2.gif)

**Obrázek 5**: hlavní seznam se všemi ovládacími prvky ContentPlaceHolder. Všimněte si, že výška buňky pro buňku záhlaví je teď.

1. Zadejte nějaký text podle vlastního výběru do každého ze tří ovládacích prvků ContentPlaceHolder.
2. Uložte stránku předlohy jako Exercise1. Master.
3. Vytvořte nový webový formulář a přidružte jej k hlavní stránce Exercise1. Master.
4. V aplikaci Visual Studio 2005 vyberte soubor, nový, soubor.
5. V dialogovém okně Přidat novou položku vyberte **webový formulář** .
6. Ujistěte se, že je zaškrtnuto políčko vybrat hlavní stránku, jak je znázorněno na obrázku 6.

![Přidání nové stránky obsahu](master-pages/_static/image3.gif)

**Obrázek 6**: Přidání nové stránky obsahu

1. Klikněte na Přidat.
2. V dialogovém okně vybrat hlavní stránku vyberte Exercise1. Master, jak je znázorněno na obrázku 7.
3. Kliknutím na tlačítko OK přidejte novou stránku obsahu.

Stránka nový obsah se zobrazí v aplikaci Visual Studio s jedním ovládacím prvkem obsahu pro každý ovládací prvek ContentPlaceHolder na stránce předlohy. Ve výchozím nastavení jsou ovládací prvky obsahu prázdné, takže můžete přidat vlastní obsah. Pokud byste chtěli, aby používali obsah z ovládacího prvku ContentPlaceHolder na stránce předlohy, stačí kliknout na symbol inteligentní značky (malá černá šipka v pravém horním rohu ovládacího prvku) a zvolit možnost *výchozí pro hlavní obsah* z inteligentní značky, jak je znázorněno na **obrázku 8**. Když to uděláte, položka nabídky se změní a *vytvoří vlastní obsah*. Kliknutím na něj v tomto okamžiku odeberete obsah ze stránky předlohy, který vám umožní definovat vlastní obsah pro konkrétní ovládací prvek obsahu.

![Nastavení ovládacího prvku obsahu jako výchozího obsahu stránek předlohy](master-pages/_static/image4.gif)

**Obrázek 7**: nastavení ovládacího prvku obsahu jako výchozího jako obsahu stránek předlohy

## <a name="connecting-master-page-and-content-pages"></a>Připojení stránky předlohy a stránek obsahu

Přidružení mezi stránkou předlohy a stránkou obsahu lze nakonfigurovat jedním ze čtyř různých způsobů:

- Atribut <strong>MasterPageFile</strong> direktivy @Page
- Nastavení vlastnosti **Page. MasterPageFile** v kódu
- **&lt;stránky&gt;** elementu v konfiguračním souboru aplikace (Web. config v kořenové složce aplikace)
- **&lt;stránky&gt;** elementu v konfiguračním souboru podsložek (Web. config v podsložce)

## <a name="masterpagefile-attribute"></a>MasterPageFile – atribut

Atribut MasterPageFile usnadňuje použití stránky předlohy na konkrétní ASP.NET stránku. Je to také metoda, která se používá k použití stránky předlohy při zaškrtnutí políčka **Vybrat hlavní stránku** jako v cvičení 1.

## <a name="setting-pagemasterpagefile-in-code"></a>Nastavení stránky. MasterPageFile v kódu

Nastavením vlastnosti MasterPageFile v kódu můžete pro svůj obsah použít určitou stránku předlohy za běhu. To je užitečné v případech, kdy možná budete muset použít určitou hlavní stránku na základě role uživatelů nebo jiných kritérií. Vlastnost MasterPageFile musí být nastavena v metodě předinit. Pokud je nastavena po předinicializaci metody, bude vyvolána událost InvalidOperationException. Stránka, na které je nastavena tato vlastnost, musí mít také ovládací prvek obsahu jako ovládací prvek nejvyšší úrovně stránky. V opačném případě bude při nastavení vlastnosti MasterPageFile vyvolána výjimka HttpException –.

## <a name="using-the-ltpagesgt-element"></a>Použití &lt;stránek&gt; elementu

Stránku předlohy pro stránky můžete nakonfigurovat nastavením atributu masterPageFile na stránkách &lt;&gt; elementu souboru Web. config. Při použití této metody mějte na paměti, že soubory Web. config nižší ve struktuře aplikace mohou toto nastavení přepsat. Toto nastavení se přepíše u všech atributů MasterPageFile nastavených v direktivě @Page. Použití &lt;stránky&gt; elementu usnadňuje vytvoření *Hlavní* hlavní stránky, která může být v případě potřeby přepsána v určitých složkách nebo souborech.

## <a name="properties-in-master-pages"></a>Vlastnosti na stránkách předlohy

Stránka předlohy může vystavovat vlastnosti pouhým nastavením těchto vlastností jako veřejných v rámci stránky předlohy. Například následující kód definuje vlastnost s názvem SomeProperty:

[!code-csharp[Main](master-pages/samples/sample2.cs)]

Chcete-li získat přístup k vlastnosti SomeProperty ze stránky obsahu, bude nutné použít vlastnost Master, například:

[!code-csharp[Main](master-pages/samples/sample3.cs)]

## <a name="nesting-master-pages"></a>Vnořování stránek předlohy

Stránky předlohy představují dokonalé řešení, které zajišťuje běžný vzhled a chování napříč velkou webovou aplikací. Nejedná se ale o společné rozhraní, aby některé části velké lokality sdílely společné rozhraní, zatímco jiné části sdílejí jiné rozhraní. Aby bylo možné tuto potřebu vyřešit, je k většímu řešení více stránek předlohy. To však stále neřeší skutečnost, že velké aplikace mohou mít určité komponenty (například nabídku), které jsou sdíleny mezi všemi stránkami a dalšími komponentami, které jsou sdíleny pouze mezi některými oddíly webu. V takovém případě vnořené stránky předlohy doplňují nutnost v textu. Jak jste viděli, normální stránka předlohy se skládá ze stránky předlohy a obsahu stránky. V situaci vnořené stránky předlohy jsou k dispozici dvě stránky předlohy. nadřazený hlavní server a podřízená hlavní položka. Podřízená stránka předlohy je také stránkou obsahu a její hlavní stránkou je nadřazená hlavní stránka.

Zde je kód typické stránky předlohy:

[!code-aspx[Main](master-pages/samples/sample4.aspx)]

Ve vnořeném hlavním scénáři by to byl nadřazený hlavní server. Jiná stránka předlohy by tuto stránku používala jako svou hlavní stránku a tento kód by vypadal takto:

[!code-aspx[Main](master-pages/samples/sample5.aspx)]

Všimněte si, že v tomto scénáři je podřízená předloha také stránkou obsahu nadřazeného hlavního serveru. Veškerý obsah podřízeného hlavního serveru se zobrazí uvnitř ovládacího prvku obsahu, který získá obsah z ovládacího prvku ContentPlaceHolder.

> [!NOTE]
> Podpora návrháře není pro vnořené stránky předlohy k dispozici. Při vývoji pomocí vnořených hlavních serverů bude nutné použít zobrazení zdroje.

Toto video ukazuje návod pro použití vnořených stránek předlohy.

![](master-pages/_static/image1.png)

[Otevření videa na celé obrazovce](master-pages/_static/nested1.wmv)

![Výběr stránky předlohy](master-pages/_static/image4.jpg)

**Obrázek 8**: Výběr stránky předlohy

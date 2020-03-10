---
uid: web-pages/overview/data/7-displaying-data-in-a-chart
title: Zobrazení dat v grafu pomocí ASP.NET webových stránek (Razor) | Microsoft Docs
author: microsoft
description: Tato kapitola vysvětluje, jak zobrazit data v grafu. V předchozích kapitolách jste zjistili, jak data zobrazit ručně a v mřížce. Tato kapitola vysvětluje...
ms.author: riande
ms.date: 05/22/2012
ms.assetid: f889fd46-4dac-4ecb-83d8-60e64c22036e
msc.legacyurl: /web-pages/overview/data/7-displaying-data-in-a-chart
msc.type: authoredcontent
ms.openlocfilehash: 6dad67d4e3d38d57a761c567d937d714a3184ea9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627489"
---
# <a name="displaying-data-in-a-chart-with-aspnet-web-pages-razor"></a>Zobrazení dat v grafu s ASP.NET webovými stránkami (Razor)

od [Microsoftu](https://github.com/microsoft)

> Tento článek vysvětluje, jak pomocí grafu zobrazit data na webu ASP.NET Web Pages (Razor) pomocí pomocné rutiny `Chart`.
> 
> **Co se naučíte**:
> 
> - Jak zobrazit data v grafu.
> - Jak styl grafů pomocí integrovaných motivů.
> - Jak uložit grafy a jak je ukládat do mezipaměti pro lepší výkon.
> 
> Jedná se o funkce ASP.NET programování, které jsou představené v článku:
> 
> - Pomocná rutina `Chart`
> 
> > [!NOTE]
> > Informace v tomto článku se vztahují na ASP.NET webové stránky 1,0 a webové stránky 2.

<a id="The_Chart_Helper"></a>
## <a name="the-chart-helper"></a>Pomocník pro grafy

Pokud chcete zobrazit data v grafické podobě, můžete použít pomocníka `Chart`. Pomocná rutina `Chart` může vykreslit obrázek zobrazující data v nejrůznějších typech grafů. Podporuje mnoho možností formátování a označování. Pomocník pro `Chart` může vykreslovat více než 30 typů grafů, včetně všech typů grafů, které můžete znát z aplikace Microsoft Excel nebo jiných nástrojů &#8212; plošných grafů, pruhových grafů, sloupcových grafů, spojnicových grafů a výsečových grafů, společně s dalšími specializovanými grafy, jako jsou burzovní grafy.

| **Plošný graf** ![Popis: obrázek typu plošného grafu](7-displaying-data-in-a-chart/_static/image1.jpg) | **Pruhový graf** ![Popis: obrázek typu pruhového grafu](7-displaying-data-in-a-chart/_static/image2.jpg) |
| --- | --- |
| **Sloupcový graf** ![Popis: obrázek typu sloupcového grafu](7-displaying-data-in-a-chart/_static/image3.jpg) | **Spojnicový graf** ![Popis: obrázek typu spojnicového grafu](7-displaying-data-in-a-chart/_static/image4.jpg) |
| **Výsečový graf** ![Popis: obrázek typu výsečového grafu](7-displaying-data-in-a-chart/_static/image5.jpg) | **Burzovní graf** ![Popis: Obrázek burzovního typu grafu](7-displaying-data-in-a-chart/_static/image6.jpg) |

### <a name="chart-elements"></a>Prvky grafu

Grafy zobrazují data a další prvky, jako jsou legendy, osy, řady a tak dále. Následující obrázek znázorňuje mnoho prvků grafu, které lze přizpůsobit při použití pomocné rutiny `Chart`. V tomto článku se dozvíte, jak nastavit některé (ne všechny) těchto elementů.

![Popis: Obrázek znázorňující prvky grafu](7-displaying-data-in-a-chart/_static/image7.jpg)

<a id="Creating_a_Chart"></a>
## <a name="creating-a-chart-from-data"></a>Vytvoření grafu z dat

Data zobrazená v grafu mohou být z pole, z výsledků vrácených z databáze nebo z dat, která jsou v souboru XML.

### <a name="using-an-array"></a>Použití pole

Jak je vysvětleno v [úvodu k ASP.NET programování webových stránek pomocí syntaxe Razor](https://go.microsoft.com/fwlink/?LinkId=202890), pole umožňuje uložit kolekci podobných položek do jedné proměnné. Pole lze použít k zahrnutí dat, která chcete zahrnout do grafu.

Tento postup ukazuje, jak můžete vytvořit graf z dat v polích pomocí výchozího typu grafu. Také ukazuje, jak zobrazit graf v rámci stránky.

1. Vytvořte nový soubor s názvem *ChartArrayBasic. cshtml*.
2. Existující obsah nahraďte následujícím: 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample1.cshtml)]

    Kód nejprve vytvoří nový graf a nastaví jeho šířku a výšku. Název grafu určíte pomocí metody `AddTitle`. Chcete-li přidat data, použijte metodu `AddSeries`. V tomto příkladu použijte parametr `name`, `xValue` a parametry `yValues` metody `AddSeries`. Parametr `name` je zobrazený v legendě grafu. Parametr `xValue` obsahuje pole dat, která se zobrazují podél vodorovné osy grafu. Parametr `yValues` obsahuje pole dat, která se používají k vykreslení svislých bodů grafu.

    Metoda `Write` skutečně vykresluje graf. V takovém případě, protože jste nezadali typ grafu, vykreslí pomoc `Chart` výchozí graf, což je sloupcový graf.
3. Spusťte stránku v prohlížeči. Prohlížeč zobrazí graf. 

    ![](7-displaying-data-in-a-chart/_static/image8.jpg)

### <a name="using-a-database-query-for-chart-data"></a>Použití databázového dotazu pro data grafu

Pokud jsou informace, které chcete grafem, v databázi, můžete spustit databázový dotaz a potom pomocí dat z výsledků vytvořit graf. Tento postup vám ukáže, jak číst a zobrazovat data z databáze vytvořená v článku [Úvod k práci s databází v lokalitách webových stránek ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202893).

1. Přidejte *aplikaci\_data* do kořenového adresáře webu, pokud složka ještě neexistuje.
2. Do složky *Data\_aplikace* přidejte soubor databáze s názvem *SmallBakery. sdf* , který je popsán v tématu [Úvod k práci s databází na webech webových stránek ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202893).
3. Vytvořte nový soubor s názvem *ChartDataQuery. cshtml*.
4. Existující obsah nahraďte následujícím:   

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample2.cshtml)]

    Kód nejprve otevře databázi SmallBakery a přiřadí ji k proměnné s názvem `db`. Tato proměnná představuje objekt `Database`, který lze použít ke čtení a zápisu do databáze. V dalším kroku kód spustí dotaz SQL, který získá název a cenu každého produktu. Kód vytvoří nový graf a předá databázový dotaz do něj voláním metody `DataBindTable` grafu. Tato metoda přijímá dva parametry: parametr `dataSource` je pro data z dotazu a parametr `xField` umožňuje nastavit, který datový sloupec se použije pro osu x grafu.

    Jako alternativu k použití metody `DataBindTable` můžete použít metodu `AddSeries` pomocné rutiny `Chart`. Metoda `AddSeries` umožňuje nastavit parametr `xValue` a `yValues`. Například namísto použití metody `DataBindTable` jako v tomto příkladu:

    [!code-css[Main](7-displaying-data-in-a-chart/samples/sample3.css)]

    Metodu `AddSeries` můžete použít takto:

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample4.html)]

    Oba vykreslují stejné výsledky. Metoda `AddSeries` je pružnější, protože můžete zadat typ grafu a data více explicitně, ale metodu `DataBindTable` je snazší použít, pokud nepotřebujete větší flexibilitu.
5. Spusťte stránku v prohlížeči. 

    ![](7-displaying-data-in-a-chart/_static/image9.jpg)

### <a name="using-xml-data"></a>Použití dat XML

Třetí možností pro vytváření grafů je použití souboru XML jako dat grafu. To vyžaduje, aby soubor XML měl také soubor schématu (soubor *. xsd* ), který popisuje strukturu XML. Tento postup ukazuje, jak číst data ze souboru XML.

1. Ve složce *App\_data* vytvořte nový soubor XML s názvem *data. XML*.
2. Existující XML nahraďte následujícím kódem XML o zaměstnancích v fiktivní společnosti. 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample5.xml)]
3. Ve složce *App\_data* vytvořte nový soubor XML s názvem *data. xsd*. (Všimněte si, že tento čas je rozšířením *. xsd*.)
4. Existující XML nahraďte následujícím kódem: 

    [!code-xml[Main](7-displaying-data-in-a-chart/samples/sample6.xml)]
5. V kořenovém adresáři webu vytvořte nový soubor s názvem *ChartDataXML. cshtml*.
6. Existující obsah nahraďte následujícím: 

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample7.cshtml)]

    Kód nejprve vytvoří objekt `DataSet`. Tento objekt se používá ke správě dat načtených ze souboru XML a jejich uspořádání podle informací v souboru schématu. (Všimněte si, že začátek kódu obsahuje příkaz `using SystemData`. To je nutné, aby bylo možné pracovat s objektem `DataSet`. Další informace najdete v části [&quot;použití příkazů&quot; a plně kvalifikovaných názvů](#SB_UsingStatements) dále v tomto článku.)

    Dále kód vytvoří objekt `DataView` na základě datové sady. Zobrazení dat poskytuje objekt, ke &#8212; kterému se může graf navazovat, číst a vykreslovat. Graf se váže k datům pomocí metody `AddSeries`, jak jste se viděli dříve při vytváření grafu dat pole, s výjimkou toho, že parametry `xValue` a `yValues` jsou nastaveny na `DataView` objekt.

    Tento příklad také ukazuje, jak zadat konkrétní typ grafu. Při přidání dat do metody `AddSeries` je parametr `chartType` také nastaven na zobrazení výsečového grafu.
7. Spusťte stránku v prohlížeči. 

    ![](7-displaying-data-in-a-chart/_static/image10.jpg)

> [!TIP]
> 
> <a id="SB_UsingStatements"></a>
> ### <a name="using-statements-and-fully-qualified-names"></a>Příkazy using a plně kvalifikované názvy
> 
> .NET Framework, na kterých ASP.NET webové stránky s syntaxe Razor, se skládá z mnoha tisíc součástí (třídy). Aby bylo možné je spravovat pro práci se všemi těmito třídami, jsou uspořádány do *oborů názvů*, které jsou podobně jako knihovny. Například obor názvů `System.Web` obsahuje třídy, které podporují komunikaci mezi serverem a prohlížečem, `System.Xml` obor názvů obsahuje třídy, které se používají k vytváření a čtení souborů XML a obor názvů `System.Data` obsahuje třídy, které umožňují pracovat s daty.
> 
> Aby bylo možné přistupovat k určité třídě v .NET Framework, kód musí znát nejen název třídy, ale také obor názvů, ve kterém je třída. Například pro použití pomocné rutiny `Chart` musí kód najít třídu `System.Web.Helpers.Chart`, která kombinuje obor názvů (`System.Web.Helpers`) s názvem třídy (`Chart`). Je známo, že *plně kvalifikovaný* název &#8212; třídy je úplný, jednoznačné umístění v rámci obrovského .NET Framework. V kódu by to vypadalo takto:
> 
> `var myChart = new System.Web.Helpers.Chart(width: 600, height: 400) // etc.`
> 
> Nicméně je nenáročný (a náchylná k chybám) pro použití těchto dlouhých plně kvalifikovaných názvů pokaždé, když chcete odkazovat na třídu nebo pomocnou nápovědu. Proto pro snazší použití názvů tříd můžete *importovat* obory názvů, které vás zajímají, což je obvykle pouze několik z mnoha oborů názvů v .NET Framework. Pokud jste naimportovali obor názvů, můžete místo plně kvalifikovaného názvu (`System.Web.Helpers.Chart`) použít pouze název třídy (`Chart`). Když váš kód běží a nalezne název třídy, může zobrazit pouze obory názvů, které jste importovali, a najít tuto třídu.
> 
> Použijete-li ASP.NET webové stránky s syntaxe Razor k vytváření webových stránek, obvykle vždy používáte stejnou sadu tříd, včetně `WebPage` třídy, různých pomocníků atd. Pokud chcete ušetřit práci při importu relevantních oborů názvů při každém vytvoření webu, ASP.NET je nakonfigurován tak, aby automaticky importoval sadu základních oborů názvů pro každý web. To je důvod, proč jste se nemuseli zabývat obory názvů nebo importovat do této chvíle. všechny třídy, se kterými jste pracovali, jsou v oborech názvů, které jsou už pro vás naimportovány.
> 
> Někdy však potřebujete pracovat se třídou, která není v oboru názvů, který je automaticky importován za vás. V takovém případě můžete buď použít plně kvalifikovaný název třídy, nebo můžete ručně importovat obor názvů, který obsahuje třídu. Chcete-li importovat obor názvů, použijte příkaz `using` (`import` v Visual Basic), jak jste viděli v příkladu dříve v tomto článku.
> 
> Například třída `DataSet` je v oboru názvů `System.Data`. Obor názvů `System.Data` není automaticky dostupný pro ASP.NETé stránky Razor. Proto pokud chcete pracovat s `DataSet` třídou pomocí jejího plně kvalifikovaného názvu, můžete použít kód podobný tomuto:
> 
> `var dataSet = new System.Data.DataSet();`
> 
> Pokud je nutné použít třídu `DataSet` opakovaně, můžete takový obor názvů naimportovat a pak použít pouze název třídy v kódu:
> 
> [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample8.cshtml)]
> 
> Můžete přidat `using` příkazy pro všechny jiné obory názvů .NET Framework, na které chcete odkazovat. Nicméně jak je uvedeno, nebudete je muset provádět často, protože většina tříd, se kterými budete pracovat, je v oborech názvů, které jsou importovány automaticky pomocí ASP.NET pro použití na stránkách *. cshtml* a *. vbhtml* .

<a id="Displaying_Charts"></a>
## <a name="displaying-charts-inside-a-web-page"></a>Zobrazení grafů v rámci webové stránky

V příkladech, které jste si viděli, vytvoříte graf a pak se graf vykresluje přímo do prohlížeče jako grafika. V mnoha případech však chcete graf zobrazit jako součást stránky, nikoli jenom samostatně v prohlížeči. K tomu je potřeba proces se dvěma kroky. Prvním krokem je vytvoření stránky, která graf generuje, protože jste už viděli.

Druhým krokem je zobrazit výsledný obrázek na jiné stránce. Chcete-li zobrazit obrázek, použijte prvek `<img>` HTML, stejným způsobem jako při zobrazení libovolného obrázku. Namísto odkazování na soubor *. jpg* nebo *. png* však element `<img>` odkazuje na soubor *. cshtml* obsahující pomocnou nápovědu `Chart`, která vytváří graf. Při spuštění zobrazované stránky `<img>` element získá výstup pomocné rutiny `Chart` a vykreslí graf.

![](7-displaying-data-in-a-chart/_static/image11.jpg)

1. Vytvořte soubor s názvem *ShowChart. cshtml*.
2. Existující obsah nahraďte následujícím: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample9.html)]

    Kód používá element `<img>` k zobrazení grafu, který jste vytvořili dříve v souboru *ChartArrayBasic. cshtml* .
3. Spusťte webovou stránku v prohlížeči. V souboru *ShowChart. cshtml* se zobrazí obrázek grafu na základě kódu obsaženého v souboru *ChartArrayBasic. cshtml* .

<a id="Styling_a_Chart"></a>
## <a name="styling-a-chart"></a>Stylování grafu

Pomocná rutina `Chart` podporuje velký počet možností, které umožňují přizpůsobit vzhled grafu. Můžete nastavit barvy, písma, ohraničení a tak dále. Snadný způsob, jak přizpůsobit vzhled grafu, je použít *motiv*. Motivy jsou soubory informací, které určují, jaká se mají u vykreslovaného grafu použít písma, barvy, popisky, palety, hranice a efekty. (Všimněte si, že styl grafu neoznačuje typ grafu.)

V následující tabulce jsou uvedeny předdefinované motivy.

| Použit | Popis |
| --- | --- |
| `Vanilla` | Zobrazí červené sloupce na bílém pozadí. |
| `Blue` | Zobrazí modré sloupce na pozadí s modrým přechodem. |
| `Green` | Zobrazí modré sloupce na zeleném přechodu na pozadí. |
| `Yellow` | Zobrazí oranžové sloupce na žlutém pozadí přechodu. |
| `Vanilla3D` | Zobrazí 3D červené sloupce na bílém pozadí. |

Můžete určit motiv, který se použije při vytváření nového grafu.

1. Vytvořte nový soubor s názvem *ChartStyleGreen. cshtml*.
2. Stávající obsah stránky nahraďte následujícím způsobem:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample10.cshtml)]

    Tento kód je stejný jako předchozí příklad, který používá databázi pro data, ale přidává parametr `theme` při vytváření objektu `Chart`. V následujícím příkladu je zobrazen změněný kód:

    [!code-csharp[Main](7-displaying-data-in-a-chart/samples/sample11.cs)]
3. Spusťte stránku v prohlížeči. Zobrazí se stejná data jako předtím, ale v grafu se vyhledá více: 

    ![](7-displaying-data-in-a-chart/_static/image12.jpg)

<a id="Saving_a_Chart"></a>
## <a name="saving-a-chart"></a>Uložení grafu

Použijete-li pomocníka `Chart` jako v tomto článku, který jste doposud viděli v tomto článku, pomocník znovu vytvoří graf od nuly při každém jeho vyvolání. V případě potřeby také kód pro graf znovu dotazuje databázi nebo znovu přečte soubor XML, aby získal data. V některých případech to může být složitá operace, například pokud je databáze, kterou se dotazuje, Velká, nebo pokud soubor XML obsahuje velké množství dat. I v případě, že graf nezahrnuje velké množství dat, proces dynamického vytváření imagí přebírá prostředky serveru a pokud hodně lidí požaduje stránku nebo stránky, které graf zobrazují, může to mít vliv na výkon vašeho webu.

Abychom vám pomohli snížit potenciální dopad na vytvoření grafu, můžete si ho vytvořit, když ho poprvé budete potřebovat, a pak ho uložit. Pokud je nutné graf znovu vygenerovat, můžete pouze načíst uloženou verzi a vykreslit ji.

Graf můžete uložit následujícími způsoby:

- Uloží graf do mezipaměti v paměti počítače (na serveru).
- Uložte graf jako soubor obrázku.
- Uložte graf jako soubor XML. Tato možnost umožňuje upravit graf před tím, než ho uložíte.

### <a name="caching-a-chart"></a>Ukládání grafu do mezipaměti

Po vytvoření grafu je můžete uložit do mezipaměti. Ukládání do mezipaměti v grafu znamená, že není nutné ho znovu vytvořit, pokud je potřeba ho znovu zobrazit. Při ukládání grafu do mezipaměti mu udělíte klíč, který musí být pro tento graf jedinečný.

Pokud na serveru dojde k nedostatku paměti, může dojít k odebrání grafů uložených do mezipaměti. Mezipaměť se navíc vymaže, pokud se vaše aplikace z nějakého důvodu restartuje. Standardní způsob, jak pracovat s grafem uloženým v mezipaměti, je proto vždy nejprve kontrolovat, zda je v mezipaměti k dispozici, a v případě potřeby ho vytvořit nebo znovu vytvořit.

1. V kořenovém adresáři webu vytvořte soubor s názvem *ShowCachedChart. cshtml*.
2. Existující obsah nahraďte následujícím: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample12.html)]

    Značka `<img>` obsahuje atribut `src`, který odkazuje na soubor *ChartSaveToCache. cshtml* a předá na stránku klíč jako řetězec dotazu. Klíč obsahuje hodnotu &quot;myChartKey&quot;. Soubor *ChartSaveToCache. cshtml* obsahuje pomocnou nápovědu `Chart`, která vytváří graf. Tuto stránku vytvoříte za chvíli.

    Na konci stránky je odkaz na stránku s názvem *ClearCache. cshtml*. To je stránka, kterou vytvoříte také za chvíli. Budete potřebovat *ClearCache. cshtml* pouze pro testování ukládání do mezipaměti v tomto příkladu – není to odkaz nebo stránka, kterou byste normálně zahrnuli při práci s grafy uloženými v mezipaměti.
3. V kořenovém adresáři webu vytvořte nový soubor s názvem *ChartSaveToCache. cshtml*.
4. Existující obsah nahraďte následujícím:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample13.cshtml)]

    Kód nejprve kontroluje, zda cokoli bylo předáno jako hodnota klíče v řetězci dotazu. V takovém případě se kód pokusí přečíst graf z mezipaměti voláním metody `GetFromCache` a předáním klíče. Pokud dojde k tomu, že v mezipaměti nejsou žádné žádné položky (k tomu dojde při prvním vyžádání grafu), kód vytvoří graf obvyklým způsobem. Po dokončení grafu kód ho uloží do mezipaměti voláním `SaveToCache`. Tato metoda vyžaduje klíč (aby se graf mohl požadovat později) a množství času, po který se má graf Uložit do mezipaměti. (Přesný čas, po který byste měli ukládat do mezipaměti, bude záviset na tom, jak často si myslíte, že se data, která představuje Metoda `SaveToCache` také vyžaduje parametr &#8212; `slidingExpiration`, pokud je nastaven na hodnotu true, čítač časového limitu se resetuje pokaždé, když je graf k dispozici. V takovém případě to znamená, že položka mezipaměti grafu vyprší 2 minuty od posledního otevření uživatele. (Alternativa k klouzavému vypršení platnosti je absolutní doba vypršení platnosti, což znamená, že položka mezipaměti vyprší přesně 2 minuty poté, co byla vložena do mezipaměti, bez ohledu na to, jak často k ní došlo.)

    Nakonec kód používá metodu `WriteFromCache` k načtení a vykreslení grafu z mezipaměti. Všimněte si, že tato metoda je mimo blok `if`, který kontroluje mezipaměť, protože získá graf z mezipaměti, zda byl graf v době, kdy byl vytvořen, nebo musel být vygenerován a uložen v mezipaměti.

    Všimněte si, že v tomto příkladu metoda `AddTitle` obsahuje časové razítko. (Přidá aktuální datum a čas &#8212; `DateTime.Now` &#8212; k názvu.)
5. Vytvořte novou stránku s názvem *ClearCache. cshtml* a nahraďte její obsah následujícím obsahem:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample14.cshtml)]

    Tato stránka používá pomocníka `WebCache` k odebrání grafu, který je uložen v mezipaměti v *ChartSaveToCache. cshtml*. Jak bylo uvedeno dříve, obvykle nemusíte mít stránku podobnou této. Vytváříte ho tady jenom pro snazší testování ukládání do mezipaměti.
6. Spusťte webovou stránku *ShowCachedChart. cshtml* v prohlížeči. Stránka zobrazuje obrázek grafu na základě kódu obsaženého v souboru *ChartSaveToCache. cshtml* . Poznamenejte si, co časové razítko říká v nadpisu grafu. 

    ![Popis: obrázek základního grafu s časovým razítkem v nadpisu grafu](7-displaying-data-in-a-chart/_static/image13.jpg)
7. Zavřete prohlížeč.
8. Znovu spusťte *ShowCachedChart. cshtml* . Všimněte si, že časové razítko je stejné jako předtím, což znamená, že graf nebyl znovu vygenerován, ale byl načten z mezipaměti.
9. V *ShowCachedChart. cshtml*klikněte na odkaz **Vymazat mezipaměť** . Tím přejdete do *ClearCache. cshtml*, který hlásí, že byla mezipaměť vymazána.
10. Klikněte na odkaz **vrátit se k ShowCachedChart. cshtml** nebo znovu spusťte *ShowCachedChart. cshtml* z WebMatrixu. Všimněte si, že se časové razítko změnilo, protože byla mezipaměť vymazána. Proto kód musel znovu vygenerovat graf a vrátit jej zpět do mezipaměti.

### <a name="saving-a-chart-as-an-image-file"></a>Uložení grafu jako souboru obrázku

Graf můžete také uložit jako soubor obrázku (například jako soubor s *příponou. jpg* ) na serveru aplikace. Pak můžete použít soubor bitové kopie tak, jak byste měli nějaký obrázek. Výhodou je, že soubor je uložený místo uložení do dočasné mezipaměti. Novou image grafu můžete uložit v různou dobu (například každou hodinu) a potom zachovat trvalý záznam změn, ke kterým dojde v průběhu času. Všimněte si, že musíte mít jistotu, že vaše webová aplikace má oprávnění k uložení souboru do složky na serveru, kam chcete umístit soubor obrázku.

1. V kořenovém adresáři webu vytvořte složku s názvem *\_ChartFiles* , pokud ještě neexistuje.
2. V kořenovém adresáři webu vytvořte nový soubor s názvem *ChartSave. cshtml*.
3. Existující obsah nahraďte následujícím:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample15.cshtml)]

    Kód nejprve zkontroluje, zda existuje soubor *. jpg* voláním metody `File.Exists`. Pokud soubor neexistuje, kód vytvoří nový `Chart` z pole. Tentokrát kód volá metodu `Save` a předá parametr `path` a určí cestu k souboru a název souboru, kam se má graf uložit. V těle stránky `<img>` element používá cestu k ukázání na soubor *. jpg* k zobrazení.
4. Spusťte soubor *ChartSave. cshtml* .
5. Vrátí se do WebMatrixu. Všimněte si, že soubor obrázku s názvem *chart01. jpg* byl uložen do složky *\_ChartFiles* .

### <a name="saving-a-chart-as-an-xml-file"></a>Uložení grafu jako souboru XML

Nakonec můžete graf uložit jako soubor XML na serveru. Výhodou použití této metody pro ukládání grafu do mezipaměti nebo uložení grafu do souboru je, že před zobrazením grafu v případě, že jste chtěli, můžete XML upravit. Vaše aplikace musí mít oprávnění ke čtení a zápisu pro složku na serveru, kam chcete uložit soubor obrázku.

1. V kořenovém adresáři webu vytvořte nový soubor s názvem *ChartSaveXml. cshtml*.
2. Existující obsah nahraďte následujícím:

    [!code-cshtml[Main](7-displaying-data-in-a-chart/samples/sample16.cshtml)]

    Tento kód je podobný kódu, který jste viděli dříve pro uložení grafu v mezipaměti s tím rozdílem, že používá soubor XML. Kód nejprve zkontroluje, zda existuje soubor XML voláním metody `File.Exists`. Pokud soubor existuje, kód vytvoří nový objekt `Chart` a předá název souboru jako parametr `themePath`. Tím se vytvoří graf na základě libovolného prvku v souboru XML. Pokud soubor XML ještě neexistuje, kód vytvoří graf jako normální a pak zavolá `SaveXml` k uložení. Graf je vykreslen pomocí metody `Write`, jak jste viděli před.

    Stejně jako u stránky, která ukázala ukládání do mezipaměti, obsahuje tento kód časové razítko v nadpisu grafu.
3. Vytvořte novou stránku s názvem *ChartDisplayXMLChart. cshtml* a přidejte do ní následující kód: 

    [!code-html[Main](7-displaying-data-in-a-chart/samples/sample17.html)]
4. Spusťte stránku *ChartDisplayXMLChart. cshtml* . Zobrazí se graf. Poznamenejte si časové razítko v nadpisu grafu.
5. Zavřete prohlížeč.
6. Ve WebMatrixu klikněte pravým tlačítkem na složku *\_ChartFiles* , klikněte na **aktualizovat**a pak otevřete složku. Soubor *XMLChart. XML* v této složce vytvořila pomocná rutina `Chart`. 

    ![Popis: složka _ChartFiles zobrazující soubor XMLChart. XML vytvořený pomocníkem grafu.](7-displaying-data-in-a-chart/_static/image14.jpg)
7. Spusťte znovu stránku *ChartDisplayXMLChart. cshtml* . Graf zobrazuje stejné časové razítko jako při prvním spuštění stránky. To je proto, že se graf generuje z formátu XML, který jste předtím uložili.
8. Ve WebMatrixu otevřete složku *\_ChartFiles* a odstraňte soubor *XMLChart. XML* .
9. Spusťte stránku *ChartDisplayXMLChart. cshtml* ještě jednou. Tentokrát je časové razítko aktualizováno, protože pomoc `Chart` musela znovu vytvořit soubor XML. Pokud chcete, vyhledejte složku *\_ChartFiles* a Všimněte si, že se soubor XML vrátí zpět.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Další prostředky

- [Úvod k práci s databází v ASP.NET webech webových stránek](https://go.microsoft.com/fwlink/?LinkId=202893)
- [Použití ukládání do mezipaměti na webech webových stránek ASP.NET ke zvýšení výkonu](https://go.microsoft.com/fwlink/?LinkId=202903)
- [Třída grafu](https://msdn.microsoft.com/library/system.web.helpers.chart(v=vs.99)) (Referenční dokumentace rozhraní API webových stránek ASP.NET na webu MSDN)

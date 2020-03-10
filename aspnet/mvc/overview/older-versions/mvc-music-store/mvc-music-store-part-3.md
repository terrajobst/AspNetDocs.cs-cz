---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: '3\. část: zobrazení a ViewModels | Microsoft Docs'
author: jongalloway
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 3 pokrývá zobrazení a ViewModels.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 3fcfc816cde22c697a78bab2c9ea7ace1bf68501
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559806"
---
# <a name="part-3-views-and-viewmodels"></a>3\. část: Zobrazení a modely ViewModel

o [Jan Galloway](https://github.com/jongalloway)

> Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio pro vývoj webů.  
>   
> Úložiště hudby MVC je zjednodušená ukázka implementace úložiště, která prodává hudební alba online a implementuje základní funkce pro správu webů, přihlašování uživatelů a nákupních košíků.  
>   
> V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 3 pokrývá zobrazení a ViewModels.

Zatím jsme právě vraceli řetězce z akcí kontroleru. To je dobrý způsob, jak získat představu o tom, jak ovladače fungují, ale není to, jak byste chtěli sestavit skutečnou webovou aplikaci. Budeme chtít lepší způsob, jak vygenerovat kód HTML zpátky do prohlížečů, které navštíví náš web – One, kde můžeme použít soubory šablon k jednoduššímu přizpůsobení odeslání obsahu HTML. To je přesně to, co dělají zobrazení.

## <a name="adding-a-view-template"></a>Přidání šablony zobrazení

Chcete-li použít šablonu zobrazení, změníme metodu indexu HomeController tak, aby vracela ActionResult a vrátila zobrazení (), jako je například:

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

Výše uvedená změna znamená, že místo vrácení řetězce je třeba použít zobrazení k vygenerování výsledku zpět.

Nyní do našeho projektu přidáme příslušnou šablonu zobrazení. K tomu umístíme textový kurzor v rámci metody akce indexu, potom klikněte pravým tlačítkem a vyberte Přidat zobrazení. Tím zobrazíte dialogové okno Přidat zobrazení:

![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)

Dialog Přidat zobrazení umožňuje rychle a snadno generovat soubory šablon zobrazení. Dialog Přidat zobrazení se ve výchozím nastavení předem vyplní názvem šablony zobrazení, která se má vytvořit, aby odpovídala metodě akce, která ji bude používat. Vzhledem k tomu, že jsme použili kontextovou nabídku přidat zobrazení v rámci metody akce index () našeho HomeController, zobrazí se v dialogovém okně Přidat zobrazení "index", protože ve výchozím nastavení se předběžně vyplní název zobrazení. Nepotřebujeme změnit žádnou z možností v tomto dialogu, takže klikněte na tlačítko Přidat.

Po kliknutí na tlačítko Přidat vytvoří Visual Web Developer novou index. cshtml šablona zobrazení pro nás v adresáři \Views\Home a vytvoří složku, pokud ještě neexistuje.

![](mvc-music-store-part-3/_static/image2.png)

Název a umístění složky souboru index. cshtml jsou důležité a následují výchozí zásady vytváření názvů pro ASP.NET MVC. Název adresáře \Views\Home odpovídá kontroleru, který má název HomeController. Název šablony zobrazení, index, odpovídá metodě akce kontroleru, které zobrazení zobrazí.

ASP.NET MVC nám umožňuje vyhnout se nutnosti explicitně zadat název nebo umístění šablony zobrazení, když používáme toto zásady vytváření názvů k vrácení zobrazení. Ve výchozím nastavení bude při psaní kódu, jako je například v rámci našeho HomeController, vykreslena šablona zobrazení \Views\Home\Index.cshtml:

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

Visual Web Developer vytvořil a otevřel šablonu zobrazení index. cshtml po kliknutí na tlačítko Přidat v dialogovém okně Přidat zobrazení. Obsah indexu. cshtml je uveden níže.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

Toto zobrazení používá syntaxe Razor, což je stručnější než modul zobrazení webových formulářů používaný ve webových formulářích ASP.NET a předchozích verzích ASP.NET MVC. Modul zobrazení webových formulářů je stále k dispozici v ASP.NET MVC 3, ale mnoho vývojářů zjistí, že zobrazovací modul Razor přesně odpovídá vývoji ASP.NET MVC.

První tři řádky nastaví nadpis stránky pomocí ViewBag. title. Podíváme se, jak tento postup ještě brzy funguje, ale nejdřív aktualizujte text záhlaví textu a zobrazí se stránka. Aktualizujte &lt;H2&gt; tag, který říká "Toto je Domovská stránka", jak je znázorněno níže.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

Spuštění aplikace ukazuje, že náš nový text je viditelný na domovské stránce.

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a>Použití rozložení pro běžné prvky webu

Většina webů má obsah, který je sdílen mezi mnoha stránkami: navigace, zápatí, obrázky s logem, odkazy na šablony stylů atd. Modul zobrazení Razor usnadňuje správu pomocí stránky s názvem \_layout. cshtml, která se pro nás vytvořila automaticky ve složce/Views/Shared.

![](mvc-music-store-part-3/_static/image4.png)

Dvojím kliknutím na tuto složku zobrazíte obsah, který vidíte níže.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

Obsah z našich individuálních zobrazení se zobrazí příkazem @RenderBody() a veškerý společný obsah, který chceme zobrazit mimo rozhraní, lze přidat do \_layout. cshtml Markup. Chceme, aby vaše hudební úložiště MVC mělo společné záhlaví s odkazy na naši domovskou stránku a oblast úložiště na všech stránkách v lokalitě, takže přidáme tuto šablonu přímo nad tento příkaz @RenderBody().

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a>Aktualizace šablony stylů

Prázdná šablona projektu obsahuje velmi zjednodušený soubor CSS, který obsahuje pouze styly používané k zobrazení ověřovacích zpráv. Náš Návrhář nabízí několik dalších šablon stylů CSS a obrázků, které definují vzhled a chování pro náš web, takže je teď přidáme.

Aktualizovaný soubor a obrázky CSS jsou obsaženy v adresáři obsahu souboru MvcMusicStore-Assets. zip, který je k dispozici na stránce [MVC – hudba-Store](https://github.com/evilDave/MVC-Music-Store). Oba z nich vybereme v Průzkumníkovi Windows a vyřadíte je do složky obsahu našeho řešení ve Visual Web Developer, jak je znázorněno níže:

![](mvc-music-store-part-3/_static/image5.png)

Zobrazí se výzva k potvrzení, jestli chcete přepsat existující soubor Web. CSS. Klikněte na tlačítkoAno.

![](mvc-music-store-part-3/_static/image6.png)

Složka obsah vaší aplikace se teď zobrazí takto:

![](mvc-music-store-part-3/_static/image7.png)

Nyní spusťte aplikaci a sledujte, jak se naše změny hledají na domovské stránce.

![](mvc-music-store-part-3/_static/image8.png)

- Pojďme se podívat na to, co se změnilo: metoda akce indexu HomeController se našla a zobrazila se šablona \Views\Home\Index.cshtmlView, i když náš kód se nazývá "návratové zobrazení ()", protože naše šablona zobrazení následovala standardní konvence vytváření názvů.
- Na domovské stránce se zobrazuje jednoduchá uvítací zpráva, která je definována v rámci šablony zobrazení \Views\Home\Index.cshtml.
- Domovská stránka používá naši šablonu \_layout. cshtml, takže úvodní zpráva je obsažena v rozložení HTML webu Standard.

## <a name="using-a-model-to-pass-information-to-our-view"></a>Předání informací do našeho zobrazení pomocí modelu

Šablona zobrazení, která jenom zobrazuje pevně zakódované HTML, nebude vytvářet velice zajímavé webové stránky. Abychom mohli vytvořit dynamický web, místo toho budeme chtít předat informace z našich akcí kontroleru do našich šablon zobrazení.

Ve vzoru kontroleru zobrazení modelu se pojem model vztahuje na objekty, které představují data v aplikaci. Objekty modelu se často shodují s tabulkami v databázi, ale nemusí být.

Metody akcí kontroleru, které vracejí ActionResult, mohou předat objekt modelu do zobrazení. Díky tomu může kontroler vyčistit všechny informace potřebné k vygenerování odpovědi a pak tyto informace předat do šablony zobrazení, která se použije k vygenerování příslušné odpovědi HTML. To je nejjednodušší pochopit tím, že se zobrazí v akci, takže se můžeme začít.

Nejprve vytvoříme některé třídy modelu, které reprezentují žánry a alba v rámci našeho obchodu. Pojďme začít vytvořením třídy žánru. Klikněte pravým tlačítkem na složku modely v rámci projektu, vyberte možnost "Přidat třídu" a pojmenujte soubor "Genre.cs".

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

Pak přidejte vlastnost názvu veřejné řetězce do třídy, která byla vytvořena:

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

*Poznámka: v případě, že se zajímá, znamená C#to, že zápis {get; set;} používá automaticky implementované funkce vlastností. Díky tomu máme výhody vlastnosti bez nutnosti deklarovat pole pro zálohování.*

Potom postupujte podle stejných kroků a vytvořte třídu alba (s názvem Album.cs), která má název a vlastnost Žánr:

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

Nyní můžeme upravit StoreController pro použití zobrazení, která zobrazují dynamické informace z našeho modelu. If – pro demonstrační účely: máme moje alba na základě ID žádosti. Tyto informace můžeme zobrazit jako v následujícím zobrazení.

![](mvc-music-store-part-3/_static/image10.png)

Začneme tak, že změníte akci úložiště Details, aby se zobrazily informace o jednom albu. Přidejte do horní části třídy **StoreControllers** příkaz "using", který bude zahrnovat obor názvů MvcMusicStore. Models, takže nemusíme psát MvcMusicStore. Models. album pokaždé, když chceme použít třídu alba. Oddíl "using" této třídy by se teď měl zobrazit jako níže.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

V dalším kroku aktualizujeme akci kontroleru podrobností tak, aby vracela ActionResult místo řetězce, stejně jako u metody indexu HomeController.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

Nyní můžeme upravit logiku, aby vracela objekt alba do zobrazení. Později v tomto kurzu načteme data z databáze, ale hned teď k zahájení práce použijeme "fiktivní data".

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

*Poznámka: Pokud si nejste obeznámeni C#s, můžete předpokládat, že použití var znamená, že je naše proměnná alba pozdní vazbá. To není správné – C# kompilátor používá odvození typu na základě toho, co přiřadíme proměnné k určení toho, že album je typu album a kompilování lokální proměnné alba jako typ alba, takže získáme kontrolu v době kompilace a podporu editoru kódu Visual Studio.*

Teď vytvoříme šablonu zobrazení, která pomocí našeho alba vygeneruje odpověď HTML. Než budeme udělat, musíme sestavit projekt, aby dialog Přidat zobrazení věděl o naší nově vytvořené třídě alba. Projekt můžete sestavit tak, že vyberete položku nabídky Ladit ⇨ Build MvcMusicStore (pro další kredity, můžete k sestavení projektu použít zástupce CTRL + SHIFT-B).

![](mvc-music-store-part-3/_static/image11.png)

Teď, když jsme si nastavili naše podpůrné třídy, jsme připraveni sestavit naši šablonu zobrazení. Klikněte pravým tlačítkem v rámci metody Details a vyberte Přidat zobrazení... z místní nabídky.

![](mvc-music-store-part-3/_static/image12.png)

Vytvoříme novou šablonu zobrazení, jako jsme předtím pracovali s HomeController. Protože ho vytváříme z StoreController, ve výchozím nastavení se vygeneruje v souboru \Views\Store\Index.cshtml.

Na rozdíl od dřív, vrátíme zaškrtávací políčko vytvořit zobrazení se silným typem. Potom v rámci příkazu "View data-Class" downlist vybereme naši třídu "album". Tím se zobrazí dialogové okno Přidat zobrazení, ve kterém můžete vytvořit šablonu zobrazení, která očekává, že se objekt alba předává k použití.

![](mvc-music-store-part-3/_static/image13.png)

Po kliknutí na tlačítko Přidat se vytvoří šablona zobrazení \Views\Store\Details.cshtml, která obsahuje následující kód.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

Všimněte si prvního řádku, který označuje, že toto zobrazení je silně typované pro naši třídu alba. Modul zobrazení Razor chápe, že byl předán objekt alba, takže můžeme snadno získat přístup k vlastnostem modelu a dokonce i využít výhod technologie IntelliSense v editoru aplikace Visual Web Developer.

Aktualizujte &lt;H2&gt; tag, aby se zobrazila vlastnost title alba úpravou této čáry, která se zobrazí takto.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

Všimněte si, že technologie IntelliSense je aktivována při zadání tečky po klíčovém slově @Model a zobrazení vlastností a metod, které třída alba podporuje.

Pojďme teď náš projekt znovu spustit a přejít na adresu URL/Store/Details/5. Zobrazí se podrobnosti o albu, jak je znázorněno níže.

![](mvc-music-store-part-3/_static/image14.png)

Teď povedeme k podobným aktualizacím pro metodu akce procházení pro Store. Aktualizujte metodu tak, aby vrátila ActionResult, a upravte logiku metody tak, aby vytvořila nový objekt žánru a vrátil ho do zobrazení.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

Klikněte pravým tlačítkem myši do metody Browse a vyberte Přidat zobrazení... v kontextové nabídce přidejte zobrazení, které je silného typu, a přidejte silný typ ke třídě Žánr.

![](mvc-music-store-part-3/_static/image15.png)

Aktualizujte &lt;H2&gt; elementu v kódu zobrazení (v/Views/Store/Browse.cshtml), aby se zobrazily informace o žánru.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

Teď náš projekt znovu spusťte a přejděte k/Store/Browse? Žánr = adresa URL disdisce. Zobrazí se stránka pro procházení, jak je uvedeno níže.

![](mvc-music-store-part-3/_static/image16.png)

Nakonec provedeme trochu složitější aktualizace metody a zobrazení akce **indexu úložiště** , abyste zobrazili seznam všech žánrů v našem obchodě. Provedeme to pomocí seznamu žánrů jako našeho objektu modelu, nikoli jenom jediného žánru.

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

Klikněte pravým tlačítkem myši na metodu akce indexu úložiště a vyberte možnost přidat zobrazení jako dříve, jako třídu modelu vyberte Žánr a stiskněte tlačítko Přidat.

![](mvc-music-store-part-3/_static/image17.png)

Nejdříve změníme deklaraci @model tak, aby označovala, že zobrazení očekává několik objektů žánrů, nikoli jenom jeden. Změňte první řádek/Store/Index.cshtml ke čtení následujícím způsobem:

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

To oznamuje modulu zobrazení Razor, že bude fungovat s objektem modelu, který může obsahovat několik žánrů objektů. Používáme&lt;žánru IEnumerable&gt; spíše než seznam&lt;Žánr&gt;, protože je obecnější, což nám umožňuje změnit typ modelu později na libovolný typ objektu, který podporuje rozhraní IEnumerable.

V dalším kroku procházíme objekty žánru v modelu, jak je uvedeno v následujícím kódu zobrazení dokončeno.

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

Všimněte si, že máme plnou podporu technologie IntelliSense, když tento kód zadáte, takže když zadáte "@Model." Uvidíme všechny metody a vlastnosti podporované rozhraním IEnumerable typu Žánr.

![](mvc-music-store-part-3/_static/image18.png)

V rámci naší smyčky "foreach" si Visual Web Developer ví, že každá položka je typu Žánr, takže jsme viděli IntelliSense pro každý typ žánru.

![](mvc-music-store-part-3/_static/image19.png)

Dále funkce generování uživatelského rozhraní zkontrolovala objekt žánru a určila, že každá z nich bude mít vlastnost Name, takže projde a zapíše je. Také generuje odkazy pro úpravy, podrobnosti a odstranění na každou jednotlivou položku. Budeme s tím využívat i v našich manažerech Storu, ale teď rádi máme místo toho jednoduchý seznam.

Když aplikaci spustíme a přejdeme na/Store, uvidíme, že se zobrazuje počet i seznam žánrů.

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a>Přidávání odkazů mezi stránkami

Naše adresa URL/Store, ve které jsou uvedené žánry, jsou v současné době uvedeny názvy žánrů jednoduše jako prostý text. Pojďme to změnit, takže místo prostého textu máme názvy žánrů odkaz na příslušnou adresu URL/Store/Browse, takže když kliknete na hudební žánr, jako je "disco", přejdete na adresu URL/Store/Browse? Žánr = disco. Naši šablonu zobrazení \Views\Store\Index.cshtml bychom mohli aktualizovat tak, aby vyhledala tyto odkazy pomocí následujícího **kódu:**

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

To funguje, ale může vést k problémům později, protože spoléhá na pevně zakódované řetězec. Například pokud jsme chtěli řadič přejmenovat, musíme vyhledat odkazy, které je potřeba aktualizovat.

Alternativním přístupem, který můžeme použít, je využít pomocnou metodu HTML. ASP.NET MVC obsahuje pomocné metody HTML, které jsou k dispozici z našeho kódu šablony zobrazení k provádění celé řady běžných úloh stejně jako to. Pomocná metoda HTML. ActionLink () je obzvláště užitečná a usnadňuje tak vytváření &lt;HTML a&gt; odkazů a postará se o obtěžující podrobnosti, jako je například zajištění správné kódování adres URL cest.

HTML. ActionLink () má několik různých přetížení, které umožňují zadat co nejvíce informací, kolik potřebujete pro vaše odkazy. V nejjednodušším případě zadáte pouze text odkazu a metodu Action, na kterou přejdete, když na klienta kliknete na hypertextový odkaz. Například můžeme na stránce s podrobnostmi úložiště propojit metodu "/Store/" index () s textem odkazu a přejít do indexu úložiště pomocí následujícího volání:

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

*Poznámka: v tomto případě jsme nemuseli zadat název kontroleru, protože jsme právě provedli odkaz na jinou akci v rámci stejného kontroleru, který vykresluje aktuální zobrazení.*

Naše odkazy na stránku pro procházení budou muset předat parametr, takže použijeme další přetížení metody HTML. ActionLink, která přijímá tři parametry:

- 1. Text odkazu, ve kterém se zobrazí název žánru
- 2. Název akce kontroleru (Procházet)
- 3. Hodnoty parametrů směrování, zadání názvu (žánr) a hodnoty (název žánru)

Pokud to všechno dohromady, napíšeme tyto odkazy na zobrazení indexu úložiště:

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

Když teď znovu spustíte náš projekt a získáte přístup k adrese URL/Store/, zobrazí se seznam žánrů. Každý Žánr je hypertextový odkaz – když se na něj klikne, pošle nám na náš/Store/Browse? Žánr = *[Žánr]* adresa URL.

![](mvc-music-store-part-3/_static/image3.jpg)

HTML pro seznam žánru vypadá takto:

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]

> [!div class="step-by-step"]
> [Předchozí](mvc-music-store-part-2.md)
> [Další](mvc-music-store-part-4.md)

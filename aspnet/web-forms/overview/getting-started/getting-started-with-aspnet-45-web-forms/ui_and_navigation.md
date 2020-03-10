---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/ui_and_navigation
title: Uživatelské rozhraní a navigace | Microsoft Docs
author: Erikre
description: V této sérii kurzů se seznámíte se základy vytváření aplikací webových formulářů ASP.NET pomocí ASP.NET 4,5 a Microsoft Visual Studio Express 2013 pro My...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 5c76891d-e515-4885-b576-76bd2c494efe
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/ui_and_navigation
msc.type: authoredcontent
ms.openlocfilehash: ac1dcaf1ba911fdcaeb3845c6836ec771733d93e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78643554"
---
# <a name="ui-and-navigation"></a>Uživatelské rozhraní a navigace

od [Erik Reitan](https://github.com/Erikre)

[Stáhnout vzorový projekt Wingtip Toys (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) nebo [Stáhnout elektronickou knihu (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> V této sérii kurzů se naučíte základy vytváření webových formulářů ASP.NET pomocí ASP.NET 4,5 a Microsoft Visual Studio Express 2013 pro web. K dispozici je Visual Studio 2013 [projekt se C# zdrojovým kódem](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) , který se doprovází v této sérii kurzů.

V tomto kurzu upravíte uživatelské rozhraní výchozí webové aplikace tak, aby podporovalo funkce aplikace Wingtip Toys Store typu přední. Přidáte také jednoduchou navigaci a datovou vazbu. Tento kurz sestaví na předchozím kurzu Vytvoření vrstvy přístupu k datům a je součástí série kurzů Wingtip Toys.

## <a name="what-youll-learn"></a>Naučíte se:

- Postup změny uživatelského rozhraní pro podporu funkcí aplikace Wingtip Toys Store front.
- Jak nakonfigurovat element HTML5 pro zahrnutí navigace na stránce
- Jak vytvořit ovládací prvek řízený daty pro přechod na konkrétní data produktu.
- Jak zobrazit data z databáze vytvořené pomocí Entity Framework Code First

Webové formuláře ASP.NET umožňují vytvářet dynamický obsah pro webovou aplikaci. Každá webová stránka ASP.NET je vytvořena způsobem podobným webové stránce ve statickém formátu HTML (stránka, která nezahrnuje zpracování na základě serveru), ale ASP.NET webová stránka obsahuje navíc prvky, které ASP.NET rozpozná a zpracuje při spuštění stránky kód HTML.

Se statickou stránkou HTML (soubor *. htm* nebo *. html* ) Server splní požadavek `Web` tím, že ho přečte a pošle ho do prohlížeče. Naproti tomu, když někdo požaduje webovou stránku ASP.NET (soubor *. aspx* ), stránka se spustí jako program na webovém serveru. Když je stránka spuštěna, může provádět libovolný úkol, který vyžaduje váš web, včetně výpočtu hodnot, čtení nebo zápisu informací o databázi nebo volání jiných programů. Jako výstup stránky dynamicky vytvoří značky (například prvky v HTML) a pošle Tento dynamický výstup do prohlížeče.

## <a name="modifying-the-ui"></a>Změna uživatelského rozhraní

V této sérii kurzů budete pokračovat úpravou stránky *Default. aspx* . Změníte uživatelské rozhraní, které je již vytvořeno pomocí výchozí šablony použité k vytvoření aplikace. Typ úprav, které provedete, je typický při vytváření libovolné aplikace webového formuláře. Provedete to tak, že změníte název, nahradíte nějaký obsah a odeberete nepotřebný výchozí obsah.

1. Otevřete nebo přejděte na stránku *Default. aspx* .
2. Pokud se stránka zobrazí v **návrhovém** zobrazení, přepněte do zobrazení **zdroje** .
3. V horní části stránky v direktivě `@Page` změňte atribut `Title` na "Vítejte", jak je znázorněno na žlutém obrázku níže. 

    [!code-aspx[Main](ui_and_navigation/samples/sample1.aspx?highlight=1)]
4. Také na stránce *Default. aspx* nahraďte veškerý výchozí obsah obsažený ve značce `<asp:Content>` tak, aby se označení zobrazovalo jako níže. 

    [!code-aspx[Main](ui_and_navigation/samples/sample2.aspx)]
5. Uložte stránku *Default. aspx* výběrem možnosti **Uložit soubor default. aspx** z nabídky **soubor** .

   Výsledná stránka *Default. aspx* se zobrazí takto: 

[!code-aspx[Main](ui_and_navigation/samples/sample3.aspx)]

V příkladu jste nastavili atribut `Title` direktivy `@Page`. Když se v prohlížeči zobrazí kód HTML, `<%: Page.Title %>` kód serveru, který se přeloží na obsah obsažený v atributu `Title`.

Stránka příklad obsahuje základní prvky, které tvoří webovou stránku ASP.NET. Stránka obsahuje statický text, který může být na stránce HTML, spolu s prvky, které jsou specifické pro ASP.NET. Obsah obsažený ve stránce *Default. aspx* bude integrován s obsahem stránky předlohy, který bude vysvětlen dále v tomto kurzu.

### <a name="page-directive"></a>@Page direktiva

Webové formuláře ASP.NET obvykle obsahují direktivy, které umožňují zadat vlastnosti stránky a informace o konfiguraci stránky. Direktivy jsou používány ASP.NET jako pokyny pro zpracování stránky, ale nejsou vykresleny jako součást kódu, který je odeslán do prohlížeče.

Nejběžněji použitou direktivou je direktiva `@Page`, která umožňuje určit mnoho možností konfigurace pro stránku, včetně následujících:

1. Programovací jazyk serveru pro kód na stránce, například C#.
2. Určuje, zda je stránka stránkou s kódem serveru přímo na stránce, která se nazývá stránka s jedním souborem nebo zda se jedná o stránku s kódem v samostatném souboru třídy, který se nazývá stránka s kódem na pozadí.
3. Určuje, zda má stránka přidruženou stránku předlohy, a měla by proto být považována za stránku obsahu.
4. Možnosti ladění a trasování.

Pokud do stránky nezahrnete direktivu `@Page`, nebo pokud direktiva neobsahuje konkrétní nastavení, bude nastavení děděno z konfiguračního souboru *Web. config* nebo z konfiguračního souboru *Machine. config* . Soubor *Machine. config* poskytuje další nastavení konfigurace pro všechny aplikace spuštěné v počítači.

> [!NOTE] 
> 
> Soubor *Machine. config* také poskytuje podrobné informace o všech možných nastaveních konfigurace.

### <a name="web-server-controls"></a>Ovládací prvky webového serveru

Ve většině aplikací webových formulářů ASP.NET přidáte ovládací prvky, které uživateli umožňují pracovat se stránkou, jako jsou tlačítka, textová pole, seznamy a tak dále. Tyto ovládací prvky webového serveru jsou podobné tlačítkům HTML a vstupním elementům. Jsou však zpracovávány na serveru, což umožňuje použít serverový kód k nastavení jejich vlastností. Tyto ovládací prvky také vyvolávají události, které lze zpracovat v kódu serveru.

Serverové ovládací prvky používají speciální syntaxi, kterou ASP.NET rozpoznává při spuštění stránky. Název značky pro ovládací prvky serveru ASP.NET začíná předponou `asp:`. To umožňuje ASP.NET rozpoznávat a zpracovávat tyto serverové ovládací prvky. Pokud ovládací prvek není součástí .NET Framework, může být tato předpona odlišná. Kromě předpony `asp:` zahrnuje i ovládací prvky serveru ASP.NET také atribut `runat="server"` a `ID`, které lze použít pro odkazování ovládacího prvku v kódu serveru.

Při spuštění stránky ASP.NET identifikuje ovládací prvky serveru a spustí kód, který je spojen s těmito ovládacími prvky. Mnoho ovládacích prvků vykresluje kód HTML nebo jiný kód na stránku, když je zobrazen v prohlížeči.

### <a name="server-code"></a>Serverový kód

Většina webových formulářů ASP.NET zahrnuje kód, který běží na serveru při zpracování stránky. Jak je uvedeno výše, kód serveru lze použít k provedení celé řady věcí, jako je například přidání dat do ovládacího prvku ListView. ASP.NET podporuje mnoho jazyků pro spuštění na serveru, včetně C#Visual Basic, J# a dalších.

ASP.NET podporuje dva modely pro psaní kódu serveru pro webovou stránku. V modelu jediného souboru je kód stránky v prvku skriptu, kde otevírací značka obsahuje atribut `runat="server"`. Alternativně můžete vytvořit kód pro stránku v samostatném souboru třídy, který je označován jako model kódu na pozadí. V takovém případě webové formuláře ASP.NET většinou neobsahuje serverový kód. Místo toho direktiva `@Page` obsahuje informace, které propojí stránku *aspx* s přidruženým souborem kódu na pozadí.

Atribut `CodeBehind` obsažený v direktivě `@Page` Určuje název samostatného souboru třídy a atribut `Inherits` Určuje název třídy v souboru kódu na pozadí, který odpovídá stránce.

### <a name="updating-the-master-page"></a>Aktualizace stránky předlohy

Ve webových formulářích ASP.NET vám stránky předloh umožňují vytvořit konzistentní rozložení stránek ve vaší aplikaci. Jedna hlavní stránka definuje vzhled a chování a standardní chování, které chcete mít u všech stránek (nebo skupiny stránek) ve vaší aplikaci. Pak můžete vytvořit jednotlivé stránky obsahu obsahující obsah, který chcete zobrazit, jak je vysvětleno výše. Když si uživatel vyžádá stránky obsahu, ASP.NET je sloučí se stránkou předlohy, aby vytvořil výstup, který kombinuje rozložení stránky předlohy s obsahem ze stránky obsahu.

Nový web potřebuje jedno logo, které se má zobrazit na každé stránce. Chcete-li přidat toto logo, můžete upravit kód HTML na stránce předlohy.

1. V **Průzkumník řešení**vyhledejte a otevřete stránku **Web. Master** .
2. Pokud je stránka v zobrazení **Návrh** , přepněte do zobrazení **zdroje** .
3. Aktualizace stránky předlohy **úpravou nebo přidáním** zvýrazněné značky žlutě: 

    [!code-aspx[Main](ui_and_navigation/samples/sample4.aspx?highlight=9,49,76-81,87)]

Tento HTML zobrazí obrázek s názvem *logo. jpg* ze složky *Image* webové aplikace, kterou přidáte později. Pokud se v prohlížeči zobrazí stránka, která používá stránku předlohy, bude zobrazeno logo. Pokud uživatel klikne na logo, uživatel přejde zpět na stránku *Default. aspx* . Značka ukotvení HTML `<a>` zabalí ovládací prvek serveru imagí a umožňuje, aby byl obrázek zahrnutý jako součást odkazu. Atribut `href` pro značku kotvy Určuje kořenový adresář "`~/`" webu jako umístění odkazu. Ve výchozím nastavení se stránka *Default. aspx* zobrazuje, když uživatel přejde do kořenového adresáře webu. **Image** `<asp:Image>` serverový ovládací prvek obsahuje vlastnosti, jako je například `BorderStyle`, které se při zobrazení v prohlížeči VYKRESLUJÍ jako HTML.

### <a name="master-pages"></a>Stránky předlohy

Hlavní stránka je soubor ASP.NET s příponou. Master (například *site. Master*) s předdefinovaným rozložením, které může zahrnovat statický text, prvky HTML a serverové ovládací prvky. Hlavní stránka je identifikována speciální direktivou `@Master`, která nahrazuje direktivu `@Page`, která se používá pro obyčejné stránky *aspx* .

Kromě direktivy `@Master` obsahuje stránka předlohy také všechny prvky HTML nejvyšší úrovně stránky, jako je například `html`, `head`a `form`. Například na stránce předlohy, kterou jste přidali výše, použijete `table` HTML pro rozložení, `img` prvek pro logo společnosti, statický text a serverové ovládací prvky pro zpracování společného členství pro vaši lokalitu. V rámci stránky předlohy můžete použít libovolný kód HTML a všechny ASP.NET prvky.

Kromě statického textu a ovládacích prvků, které se zobrazí na všech stránkách, obsahuje stránka předlohy také jeden nebo více ovládacích prvků **ContentPlaceHolder** . Tyto zástupné ovládací prvky definují oblasti, kde se zobrazí nahraditelný obsah. Nahraditelný obsah je naopak definovaný na stránkách obsahu, jako je například *Default. aspx*, pomocí ovládacího prvku **Content** Server.

#### <a name="adding-image-files"></a>Přidávání souborů obrázků

Obrázek loga, který je odkazován výše, spolu se všemi obrázky produktu, je nutné přidat do webové aplikace, aby bylo možné je zobrazit při zobrazení projektu v prohlížeči.

#### <a name="download-from-msdn-samples-site"></a>Stáhnout z webu ukázek MSDN:

[Začínáme s webovými formuláři ASP.NET 4,5 a Visual Studio 2013-Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) (C#)

Ke stažení patří prostředky ve složce *WingtipToys-assets* , které se používají k vytvoření ukázkové aplikace.

1. Pokud jste to ještě neudělali, Stáhněte si komprimované ukázkové soubory pomocí odkazu výše na webu MSDN Samples.
2. Po stažení otevřete soubor. zip a zkopírujte obsah do místní složky na vašem počítači.
3. Vyhledejte a otevřete složku *WingtipToys-assets* .
4. Přetahováním můžete zkopírovat složku *katalogu* z místní složky do kořenového adresáře projektu webové aplikace v **Průzkumník řešení** sady Visual Studio. 

    ![Uživatelské rozhraní a soubory pro navigaci – kopírování](ui_and_navigation/_static/image1.png)
5. V dalším kroku vytvořte novou složku s názvem *Image* kliknutím pravým tlačítkem na projekt **WingtipToys** v **Průzkumník řešení** a výběrem **Přidat** -&gt; **novou složku**.
6. Zkopírujte soubor *logo. jpg* ze složky *WingtipToys-assets* v **Průzkumníkovi souborů** do složky *Image* projektu webové aplikace v **Průzkumník řešení** sady Visual Studio.
7. Klikněte na možnost **Zobrazit všechny soubory** v horní části **Průzkumník řešení** a aktualizujte seznam souborů, Pokud nevidíte nové soubory.  
  
    **Průzkumník řešení** nyní zobrazuje aktualizované soubory projektu. 

    ![Uživatelské rozhraní a navigace – Průzkumník řešení](ui_and_navigation/_static/image2.png)

### <a name="adding-pages"></a>Přidávání stránek

Před přidáním navigace do webové aplikace nejprve přidáte dvě nové stránky, na které budete přecházet. Později v této sérii kurzů zobrazíte informace o produktech a produktech na těchto nových stránkách.

1. V **Průzkumník řešení**klikněte pravým tlačítkem myši na **WingtipToys**, klikněte na **Přidat**a pak klikněte na **Nová položka**.   
 Zobrazí se dialogové okno **Přidat novou položku** .
2. Na levé straně vyberte skupinu **Visual C#**  -&gt; **Web** Templates. Pak v prostředním seznamu vyberte možnost **webový formulář s hlavní stránkou** a pojmenujte ji *ProductList. aspx*. 

    ![Uživatelské rozhraní a navigace – dialogové okno Přidat novou položku](ui_and_navigation/_static/image3.png)
3. Vyberte **site. Master** a připojte stránku předlohy k nově vytvořené stránce *aspx* . 

    ![Uživatelské rozhraní a navigace – výběr stránky předlohy](ui_and_navigation/_static/image4.png)
4. Pomocí následujících stejných kroků přidejte další stránku s názvem *ProductDetails. aspx* .

### <a name="updating-bootstrap"></a>Probíhá aktualizace Bootstrap.

Šablony projektu Visual Studio 2013 používají [bootstrap](http://getbootstrap.com/), rozložení a rozhraní pro vytváření na Twitteru. Bootstrap používá CSS3 k tomu, aby poskytovala reagující návrh, což znamená, že rozložení se můžou dynamicky přizpůsobovat různým velikostem oken prohlížeče. Můžete také použít funkci zaváděcí rutiny Bootstrap, která umožňuje snadno změnit vzhled a chování aplikace. Ve výchozím nastavení Šablona webové aplikace ASP.NET v Visual Studio 2013 zahrnuje Bootstrap jako balíček NuGet.

V tomto kurzu změníte vzhled a chování aplikace Wingtip Toys tím, že nahradíte spouštěcí soubory CSS.

1. V **Průzkumník řešení**otevřete složku *obsahu* .
2. Klikněte pravým tlačítkem na soubor *bootstrap. CSS* a přejmenujte ho na *bootstrap-Original. CSS*.
3. Přejmenujte *bootstrap. min. CSS* na *bootstrap-Original. min. CSS*.
4. V **Průzkumník řešení**klikněte pravým tlačítkem myši na složku *obsahu* a vyberte možnost **Otevřít složku v Průzkumníku souborů**.  
   Zobrazí se Průzkumník souborů. Do tohoto umístění uložíte stažené soubory ve spouštěcí šabloně CSS.
5. V prohlížeči přejdete na [https://bootswatch.com/3/](https://bootswatch.com/3/).
6. Posuňte okno prohlížeče, dokud se nezobrazí motiv Cerulean. 

    ![Uživatelské rozhraní a navigace – motiv Cerulean](ui_and_navigation/_static/image5.png)
7. Stáhněte soubor *bootstrap. CSS* a soubor *bootstrap. min. CSS* do složky *obsahu* . Použijte cestu ke složce obsahu, která se zobrazí v okně **Průzkumníka souborů** , které jste předtím otevřeli.
8. V **aplikaci Visual Studio** v horní části **Průzkumník řešení**vyberte možnost **Zobrazit všechny soubory** , chcete-li zobrazit nové soubory ve složce obsahu. 

    ![Uživatelské rozhraní a navigace – Průzkumník řešení](ui_and_navigation/_static/image6.png)

   Ve složce **obsahu** se zobrazí dva nové soubory CSS, ale Všimněte si, že ikona vedle názvu souboru je šedá. To znamená, že soubor ještě nebyl do projektu přidán.
9. Klikněte pravým tlačítkem na soubory *bootstrap. CSS* a *bootstrap. min. CSS* a vyberte možnost **zahrnout do projektu**.   
   Při spuštění aplikace Wingtip Toys dále v tomto kurzu se zobrazí nové uživatelské rozhraní.

> [!NOTE] 
> 
> Šablona webové aplikace ASP.NET používá soubor *. config* v kořenovém adresáři projektu pro uložení cesty spouštěcích souborů CSS.

### <a name="modifying-the-default-navigation"></a>Úprava výchozí navigace

Výchozí navigaci pro každou stránku aplikace lze upravit změnou neuspořádaného prvku seznamu navigace, který je na stránce *site. Master* .

1. V **Průzkumník řešení**vyhledejte a otevřete stránku *Web. Master* .
2. Přidejte další navigační odkaz zvýrazněný žlutě do seznamu, který se zobrazuje níže:   

    [!code-html[Main](ui_and_navigation/samples/sample5.html?highlight=5)]

Jak vidíte ve výše uvedeném jazyce HTML, upravili jste všechny položky řádku `<li>` obsahující značku kotv `<a>` s atributem Link `href`. Každý `href` odkazuje na stránku ve webové aplikaci. Pokud uživatel klikne na jeden z těchto odkazů (například **Products**), v prohlížeči přejde na stránku, která je obsažena v `href` (například **ProductList. aspx**). Aplikaci spustíte na konci tohoto kurzu.

> [!NOTE] 
> 
> Znak tildy (`~`) slouží k určení, že cesta `href` začíná v kořenu projektu.

### <a name="adding-a-data-control-to-display-navigation-data"></a>Přidání ovládacího prvku data pro zobrazení navigačních dat

V dalším kroku přidáte ovládací prvek pro zobrazení všech kategorií z databáze. Každá kategorie bude fungovat jako odkaz na stránku *ProductList. aspx* . Když uživatel klikne na odkaz kategorie v prohlížeči, přejde na stránku Products a zobrazí pouze produkty přidružené k vybrané kategorii.

Použijete ovládací prvek **ListView** k zobrazení všech kategorií obsažených v databázi. Přidání ovládacího prvku **ListView** na stránku předlohy:

1. Na stránce *site. Master* přidejte následující zvýrazněný `<div>` prvek **za** element `<div>` obsahující `id="TitleContent"`, který jste přidali dříve:  

    [!code-aspx[Main](ui_and_navigation/samples/sample6.aspx?highlight=7-21)]

V tomto kódu se zobrazí všechny kategorie z databáze. Ovládací prvek **ListView** zobrazí název každé kategorie jako text odkazu a obsahuje odkaz na stránku *ProductList. aspx* s hodnotou dotazovacího řetězce, která obsahuje `ID` kategorie. Nastavením vlastnosti `ItemType` v ovládacím prvku **ListView** je výraz datové vazby `Item` dostupný v rámci uzlu `ItemTemplate` a ovládací prvek se bude silně nacházet. Můžete vybrat Podrobnosti objektu `Item` pomocí technologie IntelliSense, například zadání `CategoryName`. Tento kód je obsažen uvnitř kontejneru `<%#: %>`, který označuje výraz datové vazby. Přidáním (:) na konec předpony `<%#` je výsledkem výrazu datové vazby kódování HTML. V případě, že je výsledkem kódování HTML, je vaše aplikace lépe chráněná proti útokům prostřednictvím injektáže XSS (mezi weby) a útoky prostřednictvím injektáže HTML.

> [!NOTE] 
> 
> **Tip**
> 
> Když přidáte kód zadáním během vývoje, můžete si být jisti, že je nalezen platný člen objektu, protože datové ovládací prvky silného typu zobrazují dostupné členy založené na technologii IntelliSense. Technologie IntelliSense nabízí při psaní kódu vhodné možnosti kódu, jako jsou vlastnosti, metody a objekty.

V dalším kroku implementujete metodu `GetCategories` pro načtení dat.

### <a name="linking-the-data-control-to-the-database"></a>Propojení ovládacího prvku dat s databází

Předtím, než budete moci zobrazit data v ovládacím prvku dat, je třeba propojit ovládací prvek data s databází. Chcete-li vytvořit odkaz, můžete upravit kód za souborem *site.Master.cs* .

1. V **Průzkumník řešení**klikněte pravým tlačítkem na stránku *Web. Master* a pak klikněte na **Zobrazit kód**. Soubor *site.Master.cs* se otevře v editoru.
2. Poblíž začátku souboru *site.Master.cs* přidejte dva další obory názvů tak, aby všechny zahrnuté obory názvů vypadaly takto:  

    [!code-csharp[Main](ui_and_navigation/samples/sample7.cs?highlight=8-9)]
3. Přidejte zvýrazněnou `GetCategories` metodu za obslužnou rutinu události `Page_Load` následujícím způsobem:  

    [!code-csharp[Main](ui_and_navigation/samples/sample8.cs?highlight=6-11)]

Výše uvedený kód se spustí, když se v prohlížeči načte jakákoli stránka, která používá stránku předlohy. Ovládací prvek `ListView` (nazvaný "categoryList"), který jste přidali dříve v tomto kurzu, používá k výběru dat vazbu modelu. V označení ovládacího prvku `ListView` nastavte vlastnost `SelectMethod` ovládacího prvku na metodu `GetCategories` uvedenou výše. Ovládací prvek `ListView` volá během životního cyklu stránky příslušnou metodu `GetCategories` a automaticky vytvoří vazby vrácených dat. V dalším kurzu se dozvíte víc o vazbách dat.

### <a name="running-the-application-and-creating-the-database"></a>Spuštění aplikace a vytvoření databáze

Dříve v této sérii kurzů jste vytvořili třídu inicializátoru (s názvem "ProductDatabaseInitializer") a tuto třídu zadali v souboru *Global.asax.cs* . Entity Framework vygeneruje databázi při prvním spuštění aplikace, protože metoda `Application_Start` obsažená v souboru *Global.asax.cs* bude volat třídu inicializátoru. Třída inicializátoru použije třídy modelu (`Category` a `Product`), které jste přidali dříve v této sérii kurzů, k vytvoření databáze.

1. V **Průzkumník řešení**klikněte pravým tlačítkem na stránku *Default. aspx* a vyberte **nastavit jako úvodní stránku**.
2. V aplikaci Visual Studio stiskněte klávesu **F5**.   
 Nastavení všeho v průběhu tohoto prvního spuštění bude trvat trochu dlouho.   
    ![uživatelského rozhraní a navigace – okna prohlížeče](ui_and_navigation/_static/image7.png)  
 Když aplikaci spustíte, aplikace se zkompiluje a databáze s názvem *wingtiptoys. mdf* se vytvoří ve složce *App\_data* . V prohlížeči se zobrazí nabídka navigace v kategorii. Tato nabídka byla vygenerována načtením kategorií z databáze. V dalším kurzu budete implementovat navigaci.
3. Zavřete prohlížeč a zastavte běžící aplikaci.

### <a name="reviewing-the-database"></a>Kontrola databáze

Otevřete soubor *Web. config* a podívejte se do části připojovací řetězec. Můžete vidět, že hodnota `AttachDbFilename` v připojovacím řetězci odkazuje na `DataDirectory` pro projekt webové aplikace. Hodnota `|DataDirectory|` je rezervovaná hodnota, která představuje *datovou složku\_aplikace* v projektu. V této složce se nachází databáze vytvořená z vašich tříd entit.

[!code-xml[Main](ui_and_navigation/samples/sample9.xml)]

> [!NOTE] 
> 
> Pokud složka *\_data* není viditelná nebo pokud je složka prázdná, vyberte ikonu **aktualizovat** a potom v horní části okna **Průzkumník řešení** ikona **Zobrazit všechny soubory** . Aby se zobrazily všechny dostupné ikony, může být potřeba zvětšit šířku **Průzkumník řešení** oken.

Nyní můžete zkontrolovat data obsažená v souboru databáze *wingtiptoys. mdf* pomocí okna **Průzkumník serveru** .

1. Rozbalte složku *Data\_aplikace* . Pokud není složka *aplikace\_data* viditelná, přečtěte si poznámku výše.
2. Pokud není soubor databáze *wingtiptoys. mdf* viditelný, vyberte ikonu **aktualizace** a potom v horní části okna **Průzkumník řešení** ikona **Zobrazit všechny soubory** .
3. Klikněte pravým tlačítkem myši na soubor databáze *wingtiptoys. mdf* a vyberte **otevřít**.  
    Zobrazí se **Průzkumník serveru** . 

    ![Uživatelské rozhraní a navigace – Průzkumník serveru](ui_and_navigation/_static/image8.png)
4. Rozbalte složku *tabulky* .
5. Klikněte pravým tlačítkem myši na tabulku **Products**a vyberte možnost **Zobrazit data tabulky**.  
 Zobrazí se tabulka **Products (produkty** ). 

    ![UI a navigace – tabulka produktů](ui_and_navigation/_static/image9.png)
6. Toto zobrazení vám umožní zobrazit a upravit data v tabulce **produkty** ručně.
7. Zavřete okno Tabulka **produktů** .
8. V **Průzkumník serveru**klikněte znovu pravým tlačítkem myši na tabulku **Products** a vyberte možnost **Otevřít definici tabulky**.  
 Zobrazí se návrh dat pro tabulku **Products** . 

    ![Uživatelské rozhraní a navigace – návrh produktů](ui_and_navigation/_static/image10.png)
9. Na kartě **T-SQL** se zobrazí příkaz SQL DDL, který se použil k vytvoření tabulky. Můžete také použít uživatelské rozhraní na kartě **Návrh** k úpravě schématu.
10. V **Průzkumník serveru**klikněte pravým tlačítkem na **WingtipToys** Database a vyberte **Zavřít připojení**.   
 Odpojením databáze od sady Visual Studio bude schéma databáze možné upravit později v této sérii kurzů.
11. Vraťte se na **Průzkumník řešení**tak, že v dolní části okna **Průzkumník serveru** vyberete kartu **Průzkumník řešení** .

## <a name="summary"></a>Souhrn

V tomto kurzu série jste přidali některé základní uživatelské rozhraní, grafiky, stránky a navigaci. Kromě toho jste spustili webovou aplikaci, která vytvořila databázi z datových tříd, které jste přidali v předchozím kurzu. Obsah tabulky *Products* si také můžete zobrazit přímo v databázi. V dalším kurzu zobrazíte datové položky a podrobnosti z databáze.

## <a name="additional-resources"></a>Další prostředky

[Úvod do programování webových stránek ASP.NET](https://msdn.microsoft.com/library/ms178125.aspx)   
  [Přehled ovládacích prvků webového serveru ASP.NET](https://msdn.microsoft.com/library/zsyt68f1.aspx)  
[Kurz šablon stylů CSS](http://www.w3schools.com/css/default.asp)

> [!div class="step-by-step"]
> [Předchozí](create_the_data_access_layer.md)
> [Další](display_data_items_and_details.md)

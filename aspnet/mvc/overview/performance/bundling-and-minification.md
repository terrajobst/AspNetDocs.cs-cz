---
uid: mvc/overview/performance/bundling-and-minification
title: Sdružování a minifikace | Microsoft Docs
author: Rick-Anderson
description: Sdružování a minifikace jsou dva postupy, které můžete použít v ASP.NET 4,5 ke zlepšení doby načítání požadavků. Sdružování a minifikace vylepšuje dobu načítání prostřednictvím reducin...
ms.author: riande
ms.date: 08/23/2012
ms.assetid: 5894dc13-5d45-4dad-8096-136499120f1d
msc.legacyurl: /mvc/overview/performance/bundling-and-minification
msc.type: authoredcontent
ms.openlocfilehash: 61bfe5dbac04b57e1461183b66ead2f01fe0734c
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457762"
---
# <a name="bundling-and-minification"></a>Sdružování a minifikace

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> Sdružování a minifikace jsou dva postupy, které můžete použít v ASP.NET 4,5 ke zlepšení doby načítání požadavků. Sdružování a minifikace vylepšuje dobu načítání tím, že snižuje počet požadavků na server a snižuje velikost požadovaných prostředků (například CSS a JavaScript).

Většina aktuálních hlavních prohlížečů omezuje počet [souběžných připojení](http://www.browserscope.org/?category=network) na každý název hostitele na šest. To znamená, že až se šest požadavků zpracovává, v prohlížeči se zařadí další požadavky na prostředky na hostitele. Na následujícím obrázku se na kartách sítě IE F12 Developer Tools zobrazuje časování prostředků vyžadovaných zobrazením ukázkové aplikace.

![B/M](bundling-and-minification/_static/image1.png)

Šedé pruhy zobrazují čas, který prohlížeč vyřadí do fronty čekáním na šest limitů připojení. Žlutým pruhem je požadavek na první bajt, tedy čas potřebný k odeslání požadavku a přijetí první odpovědi ze serveru. Modré pruhy znázorňují čas potřebný k přijetí dat odpovědi ze serveru. Poklikáním na prostředek můžete získat podrobné informace o časování. Například následující obrázek ukazuje podrobnosti časování pro načtení souboru */Scripts/MyScripts/JavaScript6.js* .

![](bundling-and-minification/_static/image2.png)

Předchozí obrázek znázorňuje **počáteční** událost, která udává čas, kdy se požadavek zařadil do fronty, protože prohlížeč omezuje počet současných připojení. V takovém případě se žádost zařadila do fronty po 46 milisekund čekání na dokončení jiné žádosti.

## <a name="bundling"></a>Sdružování

Sdružování je nová funkce v ASP.NET 4,5, která usnadňuje kombinování nebo rozčlenění více souborů do jednoho souboru. Můžete vytvářet šablony stylů CSS, JavaScript a další sady. Méně souborů znamená méně požadavků HTTP a může zlepšit výkon při prvním načtení stránky.

Následující obrázek znázorňuje stejné zobrazení časování zobrazení o aplikaci, které se zobrazilo dříve, ale tentokrát s povoleným sdružováním a minifikace.

![](bundling-and-minification/_static/image3.png)

## <a name="minification"></a>Minifikace

Minifikace provádí různé optimalizace kódu pro skripty nebo šablony stylů CSS, jako je například odebrání nepotřebných prázdných znaků a komentářů a zkrácení názvů proměnných na jeden znak. Vezměte v úvahu následující funkce JavaScriptu.

[!code-javascript[Main](bundling-and-minification/samples/sample1.js)]

Po minifikace je funkce snížena na následující:

[!code-javascript[Main](bundling-and-minification/samples/sample2.js)]

Kromě odebrání komentářů a nepotřebných prázdných znaků byly následující parametry a názvy proměnných přejmenovány (zkráceny) následujícím způsobem:

| **Původně** | **Jmenovanou** |
| --- | --- |
| imageTagAndImageID | n |
| imageContext | t |
| imageElement | i |

## <a name="impact-of-bundling-and-minification"></a>Dopad sdružování a minifikace

V následující tabulce je uvedeno několik důležitých rozdílů mezi seznamem všech prostředků jednotlivě a pomocí sdružování a minifikace (B/M) v ukázkovém programu.

|  | **Použití B/M** | **Bez B/M** | **Mění** |
| --- | --- | --- | --- |
| **Požadavky na soubory** | 9 | 34 | 256% |
| **Odesláno KB** | 3.26 | 11.92 | 266% |
| **Přijato KB** | 388.51 | 530 | 36 % |
| **Čas načtení** | 510 MS | 780 MS | 53% |

Odeslané bajty měly výrazné snížení se sdružováním, protože prohlížeče jsou poměrně podrobné s použitím hlaviček protokolu HTTP, které se vztahují na požadavky. Snížení počtu přijatých bajtů není tak velké, protože největší soubory (*skripty\\jQuery-UI-1.8.11. min. js* a *skripty\\jQuery 1.7.1. min. js*) již minifikovaného. Poznámka: časování ukázkového programu používalo nástroj [Fiddler](http://www.fiddler2.com/fiddler2/) k simulaci pomalé sítě. (V nabídce **pravidla** Fiddler vyberte možnost **výkon** a nastavte **simulaci rychlosti modemu**.)

## <a name="debugging-bundled-and-minified-javascript"></a>Ladění a minifikovaného JavaScriptu pro balíčky

Je snadné ladit JavaScript ve vývojovém prostředí (kde je [element Compilation](https://msdn.microsoft.com/library/s10awwz0.aspx) v souboru *Web. config* nastaven na `debug="true"`), protože soubory JavaScriptu nejsou v balíčku nebo minifikovaného. Můžete také ladit sestavení pro vydání, kde jsou soubory JavaScriptu seskupené a minifikovaného. Pomocí vývojářských nástrojů IE F12 můžete ladit funkci JavaScriptu, která je součástí minifikovaného sady, pomocí následujícího postupu:

1. Vyberte kartu **skript** a potom vyberte tlačítko **Spustit ladění** .
2. Vyberte sadu prostředků obsahující funkci JavaScriptu, kterou chcete ladit, pomocí tlačítka assety.  
    ![](bundling-and-minification/_static/image4.png)
3. Minifikovaného JavaScript naformátujte tak, že vyberete **tlačítko konfigurace** ![](bundling-and-minification/_static/image5.png)a pak vyberete **formát JavaScript**.
4. Ve vstupním poli **vyhledávacího skriptu** vyberte název funkce, kterou chcete ladit. Na následujícím obrázku byl do vstupního pole **vyhledávacího skriptu** zadán **AddAltToImg** .  
    ![](bundling-and-minification/_static/image6.png)

Další informace o ladění pomocí vývojářských nástrojů F12 najdete v článku na webu MSDN, který [používá vývojářské nástroje F12 k ladění chyb JavaScriptu](https://msdn.microsoft.com/library/ie/gg699336(v=vs.85).aspx).

## <a name="controlling-bundling-and-minification"></a>Řízení sdružování a minifikace

Sdružování a minifikace jsou povoleny nebo zakázány nastavením hodnoty atributu Debug v [elementu compilation](https://msdn.microsoft.com/library/s10awwz0.aspx) v souboru *Web. config* . V následujícím kódu XML je `debug` nastavené na hodnotu true, takže sdružování a minifikace jsou zakázané.

[!code-xml[Main](bundling-and-minification/samples/sample3.xml?highlight=2)]

Pokud chcete povolit sdružování a minifikace, nastavte hodnotu `debug` na false (NEPRAVDA). Nastavení *Web. config* můžete přepsat vlastností `EnableOptimizations` třídy `BundleTable`. Následující kód umožňuje sdružování a minifikace a Přepisuje jakékoli nastavení v souboru *Web. config* .

[!code-csharp[Main](bundling-and-minification/samples/sample4.cs?highlight=7)]

> [!NOTE]
> Pokud `EnableOptimizations` není `true` nebo atribut debug v [prvku Compilation](https://msdn.microsoft.com/library/s10awwz0.aspx) v souboru *Web. config* je nastaven na `false`, soubory nebudou seskupeny ani minifikovaného. Kromě toho se nepoužijí soubory. min, přičemž budou vybrány úplné verze ladění. `EnableOptimizations` Přepisuje atribut debug v [elementu compilation](https://msdn.microsoft.com/library/s10awwz0.aspx) v souboru *Web. config.*

## <a name="using-bundling-and-minification-with-aspnet-web-forms-and-web-pages"></a>Použití sdružování a minifikace s webovými formuláři ASP.NET a webovými stránkami

- Informace o webových stránkách naleznete v položce blogu [Přidání webové optimalizace na web webové stránky](https://docs.microsoft.com/archive/blogs/rickandy/adding-web-optimization-to-a-web-pages-site).
- Webové formuláře najdete v tématu [Přidání zařazení a minifikace do webových formulářů](https://docs.microsoft.com/archive/blogs/rickandy/adding-bundling-and-minification-to-web-forms)na blogu.

## <a name="using-bundling-and-minification-with-aspnet-mvc"></a>Použití sdružování a minifikace s ASP.NET MVC

V této části vytvoříme projekt ASP.NET MVC, který bude kontrolovat sdružování a minifikace. Nejprve vytvořte nový internetový projekt ASP.NET MVC s názvem **MvcBM** , aniž by došlo ke změně výchozího nastavení.

Otevřete *aplikaci\\\_spusťte soubor\\BundleConfig.cs* a Projděte si `RegisterBundles` metodu, která se používá k vytváření, registraci a konfiguraci sad. Následující kód ukazuje část metody `RegisterBundles`.

[!code-csharp[Main](bundling-and-minification/samples/sample5.cs)]

Předchozí kód vytvoří novou sadu JavaScriptu s názvem *~/Bundles/jQuery* , která obsahuje všechny příslušné (tj. Debug nebo minifikovaného, ale ne. *vsdoc*) soubory ve složce *Scripts* , které odpovídají řetězci zástupné karty "~/Scripts/jQuery-{Version}.js". Pro ASP.NET MVC 4 to znamená s konfigurací ladění, soubor *jQuery 1.7.1. js* se přidá do sady prostředků. V konfiguraci vydané verze se přidá *jQuery 1.7.1. min. js* . Rozhraní sdružování se skládá z několika běžných konvencí, jako například:

- Výběr souboru ". min" pro vydání, pokud existují *FileX. min. js* a *FileX. js* .
- Výběr verze, která není ". min" pro ladění.
- Ignorují se soubory "-vsdoc" (například *jQuery 1.7.1-vsdoc. js*), které jsou používány pouze pomocí technologie IntelliSense.

`{version}` zástupné znaky, které jsou uvedené výše, slouží k automatickému vytvoření sady jQuery s příslušnou verzí jQuery ve složce *Scripts* . V tomto příkladu použití zástupné karty přináší následující výhody:

- Umožňuje použít NuGet pro aktualizaci na novější verzi jQuery beze změny předcházejícího kódu služby sdružování nebo odkazů jQuery na stránkách zobrazení.
- Automaticky vybere úplnou verzi pro konfigurace ladění a verzi ". min" pro sestavení vydaných verzí.

## <a name="using-a-cdn"></a>Používání sítě CDN

 Následující kód nahrazuje místní sadu jQuery pomocí sady CDN jQuery.

[!code-csharp[Main](bundling-and-minification/samples/sample6.cs)]

Ve výše uvedeném kódu bude z CDN v režimu vydání požadován příkaz jQuery a ladicí verze jQuery bude v režimu ladění načtena místně. Při používání sítě CDN byste měli mít záložní mechanismus pro případ, že žádost CDN není úspěšná. Následující fragment kódu z konce souboru rozložení zobrazuje skript přidaný do požadavku jQuery, aby síť CDN nebyla úspěšná.

[!code-cshtml[Main](bundling-and-minification/samples/sample7.cshtml?highlight=5-13)]

## <a name="creating-a-bundle"></a>Vytvoření sady prostředků

Třída [sady prostředků](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx) `Include` metoda přebírá pole řetězců, kde každý řetězec je virtuální cesta k prostředku. Následující kód z metody `RegisterBundles` v *App\\\_Start\\BundleConfig.cs* ukazuje, jakým způsobem se do sady přidaly různé soubory:

[!code-csharp[Main](bundling-and-minification/samples/sample8.cs)]

K přidání všech souborů v adresáři (a volitelně všech podadresářích), které odpovídají vzoru hledání, je k dispozici `IncludeDirectory` třídy [sady prostředků](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx) . `IncludeDirectory` rozhraní API třídy [sady prostředků](https://msdn.microsoft.com/library/system.web.optimization.bundle(v=VS.110).aspx) se zobrazuje níže:

[!code-csharp[Main](bundling-and-minification/samples/sample9.cs)]

Na sady jsou odkazovány v zobrazeních pomocí metody Render (`Styles.Render` pro CSS a `Scripts.Render` pro JavaScript). Následující kód z *zobrazení\\sdílené\\\_layout. cshtml* ukazuje, jak výchozí ASP.NET zobrazení internetového projektu odkazuje na sady CSS a JavaScript.

[!code-cshtml[Main](bundling-and-minification/samples/sample10.cshtml?highlight=5-6,11)]

Všimněte si, že metody vykreslování přebírají pole řetězců, takže můžete přidat více sad v jednom řádku kódu. Obecně budete chtít použít metody vykreslení, které vytvoří nezbytný kód HTML pro odkaz na prostředek. Můžete použít metodu `Url` pro vygenerování adresy URL assetu bez označení potřebného k odkazování na prostředek. Předpokládejme, že jste chtěli použít nový [asynchronní](http://www.whatwg.org/specs/web-apps/current-work/#attr-script-async) atribut HTML5. Následující kód ukazuje, jak odkazovat na modernizr pomocí metody `Url`.

[!code-cshtml[Main](bundling-and-minification/samples/sample11.cshtml?highlight=11)]

## <a name="using-the--wildcard-character-to-select-files"></a>Použití zástupného znaku "\*" pro výběr souborů

Virtuální cesta zadaná v metodě `Include` a ve vzorci hledání v metodě `IncludeDirectory` může přijmout jeden zástupný znak "\*" jako předponu nebo příponu do posledního segmentu cesty. V řetězci hledání se nerozlišují malá a velká písmena. Metoda `IncludeDirectory` má možnost Hledat podadresáře.

Vezměte v úvahu projekt s následujícími soubory JavaScriptu:

- *Skripty\\Common\\AddAltToImg. js*
- *Skripty\\Common\\ToggleDiv. js*
- *Skripty\\Common\\ToggleImg. js*
- *Skripty\\Common\\sub1\\ToggleLinks. js*

![DIR imag](bundling-and-minification/_static/image7.png)

Následující tabulka ukazuje soubory přidané do sady prostředků pomocí zástupného znaku, jak je znázorněno níže:

| **Volání** | **Přidané soubory nebo vyvolání výjimky** |
| --- | --- |
| Include ("~/Scripts/Common/\*. js") | *AddAltToImg. js*, *ToggleDiv. js*, *ToggleImg. js* |
| Include ("~/Scripts/Common/T\*. js") | Neplatná výjimka vzoru. Zástupný znak je povolen pouze pro předponu nebo příponu. |
| Include ("~/Scripts/Common/\*og.\*") | Neplatná výjimka vzoru. Je povolen pouze jeden zástupný znak. |
| Include ("~/Scripts/Common/T\*") | *ToggleDiv. js*, *ToggleImg. js* |
| Include ("~/Scripts/Common/\*") | Neplatná výjimka vzoru. Čistý zástupný segment není platný. |
| IncludeDirectory ("~/Scripts/Common"; "T\*") | *ToggleDiv. js*, *ToggleImg. js* |
| IncludeDirectory ("~/Scripts/Common"; "T\*"; true) | *ToggleDiv. js*, *ToggleImg. js*, *ToggleLinks. js* |

Explicitní přidání každého souboru do sady se obvykle upřednostňuje pro načítání souborů se zástupnými znaky z následujících důvodů:

- Přidávání skriptů podle zástupných znaků, aby je bylo možné načíst v abecedním pořadí, což obvykle není to, co chcete. Soubory CSS a JavaScript často musí být přidány do konkrétní (neabecední) objednávky. Toto riziko můžete zmírnit přidáním vlastní implementace [IBundleOrderer](https://msdn.microsoft.com/library/system.web.optimization.ibundleorderer(VS.110).aspx) , ale explicitní přidání každého souboru je méně náchylné k chybám. Například můžete do složky v budoucnu přidat nové prostředky, které mohou vyžadovat úpravu [IBundleOrderer](https://msdn.microsoft.com/library/system.web.optimization.ibundleorderer(VS.110).aspx) implementace.
- Zobrazení konkrétních souborů přidaných do adresáře pomocí zástupných znaků můžete zahrnout do všech zobrazení odkazujících na daný svazek. Pokud je do sady prostředků přidán konkrétní skript, může se v jiných zobrazeních, která odkazují na daný svazek, zobrazit chyba JavaScriptu.
- Soubory CSS, které importují jiné soubory, mají za následek dvojí načtení importovaných souborů. Například následující kód vytvoří sadu prostředků s největším počtem souborů CSS motivu uživatelského rozhraní jQuery, které jsou načteny dvakrát. 

    [!code-csharp[Main](bundling-and-minification/samples/sample12.cs)]

  Selektor zástupných znaků "\*. css" přiřadí všechny soubory CSS ve složce, včetně *obsahu\\themes\\base\\jQuery. UI. All. CSS* . Soubor *jQuery. UI. All. CSS* importuje další soubory CSS.

## <a name="bundle-caching"></a>Ukládání sady prostředků do mezipaměti

Sady svazků nastavují hlavičku Expires protokolu HTTP jeden rok od okamžiku vytvoření sady. Pokud přejdete na dříve zobrazenou stránku, Fiddler ukazuje, že IE nevytváří podmíněný požadavek na sadu, tedy neexistují žádné požadavky HTTP GET z IE na sady a žádné odpovědi HTTP 304 ze serveru. Můžete vynutit, aby aplikace IE nastala podmíněný požadavek pro jednotlivé sady pomocí klávesy F5 (výsledkem je odpověď HTTP 304 pro jednotlivé sady). Úplnou aktualizaci můžete vynutit pomocí ^ F5 (výsledkem bude odpověď HTTP 200 pro jednotlivé sady.)

Na následujícím obrázku je vidět karta **ukládání do mezipaměti** v podokně odpověď Fiddler:

![Obrázek ukládání do mezipaměti Fiddler](bundling-and-minification/_static/image8.png)

Požadavek   
`http://localhost/MvcBM_time/bundles/AllMyScripts?v=r0sLDicvP58AIXN_mc3QdyVvVj5euZNzdsa2N1PKvb81`  
 je pro sadu prostředků **AllMyScripts** a obsahuje dvojici řetězců dotazu **v = R0sLDicvP58AIXN\\\_mc3QdyVvVj5euZNzdsa2N1PKvb81**. Řetězec dotazu **v** má token hodnoty, který je jedinečný identifikátor používaný pro ukládání do mezipaměti. Pokud se svazek nemění, aplikace ASP.NET požádá o sadu prostředků **AllMyScripts** pomocí tohoto tokenu. Pokud se kterýkoli soubor ve svazku změní, rozhraní optimalizace ASP.NET vygeneruje nový token, který zaručuje, že požadavky prohlížeče na tento svazek získají nejnovější sadu.

Pokud spustíte vývojářské nástroje IE9 F12 a přejdete na dříve načtenou stránku, IE nesprávně zobrazuje podmíněné požadavky GET na jednotlivé sady a server, který vrací HTTP 304. Můžete si přečíst, proč má IE9 problémy s určením, jestli se podmíněný požadavek provedl v položce blogu [pomocí sítě CDN a vyprší za účelem vylepšení výkonu webu](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx).

## <a name="less-coffeescript-scss-sass-bundling"></a>LESS, CoffeeScript, SCSS, Sass sdružování.

Rozhraní sdružování a minifikace poskytuje mechanismus pro zpracování zprostředkujících jazyků, jako je [scss](http://sass-lang.com/), [Sass](http://sass-lang.com/), [menší](http://www.dotlesscss.org/) nebo [Coffeescript](http://coffeescript.org/), a použití transformací, jako je minifikace, do výsledné sady. Například pro přidání souborů [. less](http://www.dotlesscss.org/) do projektu MVC 4:

1. Vytvořte složku pro méně obsahu. Následující příklad používá složku *Content\\MyLess* .
2. Přidejte do projektu [necelou](http://www.dotlesscss.org/) plochu **balíčku NuGet** .  
    ![instalace nech NuGet](bundling-and-minification/_static/image9.png)
3. Přidejte třídu, která implementuje rozhraní [IBundleTransform](https://msdn.microsoft.com/library/system.web.optimization.ibundletransform(VS.110).aspx) . Pro transformaci. less přidejte do projektu následující kód.

    [!code-csharp[Main](bundling-and-minification/samples/sample13.cs)]
4. Pomocí `LessTransform` a transformace [CssMinify](https://msdn.microsoft.com/library/system.web.optimization.cssminify(VS.110).aspx) vytvořte sadu méně souborů. Do metody `RegisterBundles` v souboru *App\\_Start\\souboru BundleConfig.cs* přidejte následující kód.

    [!code-csharp[Main](bundling-and-minification/samples/sample14.cs)]
5. Přidejte následující kód do všech zobrazení, která odkazují na méně sady.

    [!code-cshtml[Main](bundling-and-minification/samples/sample15.cshtml)]

## <a name="bundle-considerations"></a>Požadavky sady prostředků

Dobrým postupem při vytváření svazků je zahrnutí "sady" jako předpony do názvu sady prostředků. Tím se zabrání možnému [konfliktu směrování](https://forums.asp.net/post/5012037.aspx).

Po aktualizaci jednoho souboru v sadě se pro parametr řetězce dotazu sady prostředků vygeneruje nový token a při příštím požadavku na stránku obsahující sadu se musí stáhnout úplná sada prostředků. V tradičním označení, kde je každý Asset uveden samostatně, bude stažen pouze změněný soubor. Prostředky, které se často mění, nemusí být vhodnými kandidáty pro sdružování.

Seřízení a minifikace primárně zlepšují dobu načtení první stránky. Po vyžádání webové stránky prohlížeč ukládá do mezipaměti prostředky (JavaScript, CSS a image), takže sdružování a minifikace nebude poskytovat žádné zvýšení výkonu při požadavku na stejnou stránku nebo stránky na stejném webu, který požaduje stejné prostředky. Pokud ve svých prostředcích nenastavíte hlavičku Expires správně a nepoužijete sdružování a minifikace, heuristika aktuálnosti prohlížečů označí prostředky jako zastaralé po několika dnech a prohlížeč bude pro každý Asset vyžadovat požadavek na ověření. V tomto případě sdružování a minifikace poskytují zvýšení výkonu po žádosti o první stránku. Podrobnosti najdete v blogu [použití sítě CDN a vyprší pro zlepšení výkonu](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx)webu.

Omezení prohlížeče šesti současných připojení na každý název hostitele je možné zmírnit pomocí sítě [CDN](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx). Vzhledem k tomu, že CDN bude mít jiný název hostitele než váš hostující web, požadavky na prostředky z CDN se nebudou počítat s omezením šesti současných připojení k vašemu hostitelskému prostředí. CDN může také poskytovat společné ukládání balíčků do mezipaměti a výhody ukládání do mezipaměti.

Balíčky by měly být rozdělené podle stránek, které je potřebují. Například výchozí šablona ASP.NET MVC pro internetovou aplikaci vytvoří sadu prostředků jQuery oddělenou od jQuery. Vzhledem k tomu, že výchozí zobrazení nejsou k dispozici a neúčtují hodnoty, neobsahují sadu ověření.

Obor názvů `System.Web.Optimization` je implementován v *knihovně System. Web. Optimization. dll*. Využívá knihovnu webodmašťování (*webodmašťování. dll*) pro funkce minifikace, které zase používá *Antlr3. Runtime. dll*.

*Používám Twitter k vytváření rychlých příspěvků a sdílení odkazů. Moje obslužná rutina Twitteru je*: [@RickAndMSFT](http://twitter.com/RickAndMSFT)

## <a name="additional-resources"></a>Další materiály a zdroje informací

- Video:[sdružování a optimalizace](https://channel9.msdn.com/Events/aspConf/aspConf/Bundling-and-Optimizing) podle [Howard Dierking](https://twitter.com/#!/howard_dierking)
- [Přidání webové optimalizace do webu webových stránek](https://blogs.msdn.com/b/rickandy/archive/2012/08/15/adding-web-optimization-to-a-web-pages-site.aspx).
- [Přidání sdružování a minifikace do webových formulářů](https://blogs.msdn.com/b/rickandy/archive/2012/08/14/adding-bundling-and-minification-to-web-forms.aspx).
- [Dopad na výkon sdružování a minifikace na procházení webu pomocí aplikace](https://blogs.msdn.com/b/henrikn/archive/2012/06/17/performance-implications-of-bundling-and-minification-on-http.aspx) [petr F Nielsen](http://en.wikipedia.org/wiki/Henrik_Frystyk_Nielsen) [@frystyk](https://twitter.com/frystyk)
- [Použití sítě CDN a vyprší za účelem vylepšení výkonu](https://blogs.msdn.com/b/rickandy/archive/2011/05/21/using-cdns-to-improve-web-site-performance.aspx) webu Rick Anderson [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT)
- [Minimalizovat čas RTT (doba odezvy)](https://developers.google.com/speed/docs/best-practices/rtt)

## <a name="contributors"></a>Spoluautoři

- Hao Kung
- [Howard Dierking](https://twitter.com/#!/howard_dierking)
- Diana LaRose

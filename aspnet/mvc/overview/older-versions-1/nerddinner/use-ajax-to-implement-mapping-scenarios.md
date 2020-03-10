---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
title: Použití jazyka AJAX k implementaci scénářů mapování | Microsoft Docs
author: microsoft
description: Krok 11 ukazuje, jak integrovat podporu mapování AJAX do naší aplikace NerdDinner, která umožňuje uživatelům vytvářet, upravovat nebo zobrazovat večeři, aby viděli l...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: f731990a-0a81-4d62-81df-87d676cdedd6
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-implement-mapping-scenarios
msc.type: authoredcontent
ms.openlocfilehash: 7fc90f978b9f9eca511feca70a3c0d02ec69b940
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78580113"
---
# <a name="use-ajax-to-implement-mapping-scenarios"></a>Použití jazyka AJAX k implementaci scénářů mapování

od [Microsoftu](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 11 bezplatného [kurzu aplikace "NerdDinner"](introducing-the-nerddinner-tutorial.md) , který vás provede procesem vytvoření malé, ale dokončené webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 11 ukazuje, jak integrovat podporu mapování AJAX do naší aplikace v NerdDinner, která umožňuje uživatelům vytvářet, upravovat nebo zobrazovat večeře, aby viděli umístění večeře.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme vám postupovat podle [Začínáme s kurzy pro](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [hudební úložiště](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) MVC 3 nebo MVC.

## <a name="nerddinner-step-11-integrating-an-ajax-map"></a>NerdDinner krok 11: integrace mapy AJAX

Nyní budeme naši aplikaci trochu vizuálně zajímavější integrací podpory mapování AJAX. Tím umožníte uživatelům, kteří vytvářejí, upravují nebo zobrazují večeři, zobrazit umístění večeře.

### <a name="creating-a-map-partial-view"></a>Vytvoření částečného zobrazení mapy

V rámci naší aplikace budeme používat funkce mapování na několika místech. Abychom zachovali náš kód v SUŠINě, zapouzdřuje se společná funkce mapy v rámci jedné částečné šablony, kterou můžeme znovu použít napříč různými akcemi a zobrazeními řadiče. Pojmenujte Toto částečné zobrazení "map. ascx" a vytvořte ho v adresáři \Views\Dinners.

Mapu. ascx můžeme vytvořit částečně tak, že kliknete pravým tlačítkem na adresář \Views\Dinners a vyberete příkaz nabídky pro zobrazení pro přidání&gt;. Pojmenuje zobrazení "map. ascx", zkontrolujeme ho jako částečné zobrazení a oznámíme, že předáváme silně typované třídy modelu "večeře".

![](use-ajax-to-implement-mapping-scenarios/_static/image1.png)

Po kliknutí na tlačítko Přidat se vytvoří částečná šablona. Pak aktualizujeme soubor map. ascx tak, aby měl následující obsah:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample1.aspx)]

První skript &lt;&gt; odkazuje na knihovnu mapování Microsoft Virtual Earth 6,2. Druhý skript &lt;&gt; odkazuje na soubor map. js, který bude brzy vytvořen, který bude zapouzdřit naši společnou logiku mapování JavaScriptu. &lt;div ID = "theMap"&gt; prvek je kontejner HTML, který bude virtuální země používat k hostování mapy.

Pak budeme mít vložený &lt;skript&gt; skriptu, který obsahuje dvě funkce JavaScriptu specifické pro toto zobrazení. První funkce používá jQuery k vedení funkce, která se spustí, když je stránka připravena ke spuštění skriptu na straně klienta. Volá pomocnou funkci LoadMap (), kterou definujeme v rámci souboru skriptu map. js pro načtení mapového ovládacího prvku Virtual Earth. Druhá funkce je obslužná rutina události zpětného volání, která přidá kód PIN k mapě, která identifikuje umístění.

Všimněte si, jak používám &lt;na straně serveru% =%&gt; bloku v bloku skriptu na straně klienta, aby se vložila Zeměpisná šířka a zeměpisná délka večeře, kterou chceme namapovat do JavaScriptu. To je užitečnou technikou pro výstup dynamických hodnot, které mohou být používány skriptem na straně klienta (bez nutnosti samostatného volání AJAX zpět na server pro načtení hodnot, což zrychluje). &lt;% =%&gt;ch bloků bude provedeno při vykreslování zobrazení na serveru, takže výstup HTML bude pouze končit vloženými hodnotami JavaScriptu (například: var Latitude = 47,64312;).

### <a name="creating-a-mapjs-utility-library"></a>Vytvoření knihovny nástrojů map. js

Teď vytvoříme soubor map. js, který můžeme použít k zapouzdření funkcí JavaScriptu pro naši mapu (a implementaci výše uvedených metod LoadMap a LoadPin). To můžeme provést tak, že kliknete pravým tlačítkem na adresář \Scripts v našem projektu a pak vyberete příkaz nabídky přidat&gt;novou položku, vyberete položku JScript a pojmenujte ji "map. js".

Níže je kód JavaScriptu, který přidáme do souboru map. js, který bude komunikovat s virtuálním Earth, aby se zobrazila naše mapa a přidala se k nim pro naši večeři jejich kódy PIN:

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample2.js)]

### <a name="integrating-the-map-with-create-and-edit-forms"></a>Integrace mapy s formuláři pro vytváření a úpravy

Nyní budeme integrovat podporu map s našimi stávajícími scénáři vytvoření a úpravy. Dobrá zpráva je, že to je poměrně snadné – to znamená, že nám nepotřebujeme změnit žádný kód našeho kontroleru. Vzhledem k tomu, že naše zobrazení pro vytváření a úpravy sdílejí společné zobrazení "DinnerForm" a implementují uživatelské rozhraní formuláře večeře, můžeme mapu přidat na jednom místě a použít k tomu naše scénáře vytvoření a úprav.

Vše, co musíme udělat, je otevřít částečné zobrazení \Views\Dinners\DinnerForm.ascx a aktualizovat ho tak, aby obsahovalo naši novou část mapy. Níže vidíte, že aktualizovaný DinnerForm bude vypadat po přidání mapy (Poznámka: prvky formuláře HTML jsou vynechány ve fragmentu kódu níže pro zkrácení):

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample3.aspx)]

Výše uvedená DinnerForm přebírá objekt typu "DinnerFormViewModel" jako typ modelu (protože potřebuje buď objekt večeře, tak i SelectList pro naplnění ovládacího prvku DropDownList v zemích). Částečná mapa pouze potřebuje objekt typu "večeře" jako typ modelu, a takže když vykreslíme částečnou mapu, předáváme jí pouze dílčí vlastnost DinnerFormViewModel:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample4.aspx)]

Funkce jazyka JavaScript, kterou jsme přidali do částečného použití jQuery, k připojení události "rozostření" do textového pole "adresa" jazyka HTML. Pravděpodobně jste si vyzkoušeli události "fokus", které se aktivují, když uživatel klikne na textové pole nebo na jeho kartu. Opak je událost "rozostření", která se aktivuje, když uživatel ukončí textové pole. Výše uvedená obslužná rutina události vymaže hodnoty textového pole Zeměpisná šířka a zeměpisná délka, pokud k tomu dojde, a pak vykreslí nové umístění adresy na naší mapě. Obslužná rutina události zpětného volání, kterou jsme definovali v souboru map. js, pak aktualizuje textová pole Zeměpisná délka a zeměpisná šířka na našem formuláři pomocí hodnot vrácených funkcí Virtual Earth na základě adresy, kterou jsme přiřadili.

A když teď znovu spustíte naši aplikaci a kliknete na kartu "hostitel večeře", zobrazí se výchozí mapa zobrazená společně s našemi standardními prvky formuláře večeře:

![](use-ajax-to-implement-mapping-scenarios/_static/image2.png)

Když zadáte adresu a potom tabulátor, mapa se dynamicky aktualizuje pro zobrazení umístění a naše obslužná rutina události naplní textová pole Zeměpisná šířka/zeměpisná místa s hodnotami umístění:

![](use-ajax-to-implement-mapping-scenarios/_static/image3.png)

Pokud ukládáme novou večeři a pak ji znovu otevřete pro úpravy, zjistíme, že při načtení stránky se zobrazí umístění mapy:

![](use-ajax-to-implement-mapping-scenarios/_static/image4.png)

Pokaždé, když se změní pole adresa, aktualizuje se souřadnice mapy a zeměpisná šířka a délka.

Teď, když Mapa zobrazuje umístění na večeři, můžeme také změnit pole formuláře Zeměpisná šířka a zeměpisná délka, ze kterých jsou viditelná textová pole, aby byly skryté prvky (protože mapa je automaticky aktualizuje při každé zadání adresy). Provedete to tak, že pro použití pomocné metody HTML. Hidden () přepneme na použití pomocníka HTML HTML. TextBox ():

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample5.aspx)]

A teď jsou naše formuláře trochu uživatelsky přívětivější a nepoužívejte neupravenou zeměpisnou šířku a délku (ale pořád je uložíte s každou večeři v databázi):

![](use-ajax-to-implement-mapping-scenarios/_static/image5.png)

### <a name="integrating-the-map-with-the-details-view"></a>Integrace mapy se zobrazením podrobností

Teď, když máme mapu integrovanou s našimi scénáři vytvoření a úprav, můžeme ji také integrovat s našimi scénáři. Stačí, abyste volali &lt;% HTML. RenderPartial ("map"); %&gt; v zobrazení podrobností.

Níže je uveden zdrojový kód pro zobrazení kompletních podrobností (s integrací mapy) vypadá takto:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample6.aspx)]

A když uživatel přejde na adresu URL/Dinners/Details/[ID], uvidí podrobnosti o večeři, umístění večeře na mapě (dokončete s PIN kódem, který při najetí myší nad zobrazí název večeře a jeho adresa) a odkaz AJAX na pro něj:

![](use-ajax-to-implement-mapping-scenarios/_static/image6.png)

### <a name="implementing-location-search-in-our-database-and-repository"></a>Implementace vyhledávání umístění v naší databázi a úložišti

Abychom dokončili naši implementaci AJAX, přidáváme mapu na domovskou stránku aplikace, která umožňuje uživatelům graficky vyhledávat večeře.

![](use-ajax-to-implement-mapping-scenarios/_static/image7.png)

Zahájíme implementaci podpory v rámci naší databáze a vrstvy úložiště dat, abychom mohli efektivně provádět hledání na základě protokolu RADIUS založeného na poloze pro večeři. K implementaci tohoto postupu můžeme použít nové [geoprostorové funkce sql 2008](https://www.microsoft.com/sqlserver/2008/en/us/spatial-data.aspx) nebo můžete použít přístup k funkcím SQL, které Gary Dryden popisuje v článku: [http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx](http://www.codeproject.com/KB/cs/distancebetweenlocations.aspx) a Rob Conery blogged o použití s LINQ to SQL tady: [http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/](http://blog.wekeroad.com/2007/08/30/linq-and-geocoding/)

Chcete-li implementovat tuto techniku, otevřete v sadě Visual Studio "Průzkumník serveru", vyberte databázi NerdDinner a potom klikněte pravým tlačítkem myši na poduzel functions a zvolte možnost vytvořit novou "skalární funkci":

![](use-ajax-to-implement-mapping-scenarios/_static/image8.png)

Pak vložíte do následující funkce DistanceBetween:

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample7.sql)]

Pak vytvoříme novou funkci vracející tabulku v SQL Server, kterou zavoláme "NearestDinners":

![](use-ajax-to-implement-mapping-scenarios/_static/image9.png)

Tato funkce tabulky "NearestDinners" používá pomocnou funkci DistanceBetween k vrácení všech večeři v rámci 100 mil od zeměpisné šířky a délky, kterou poskytujeme:

[!code-sql[Main](use-ajax-to-implement-mapping-scenarios/samples/sample8.sql)]

Pro volání této funkce nejprve otevřete návrháře LINQ to SQL dvojitým kliknutím na soubor NerdDinner. dbml v adresáři \Models:

![](use-ajax-to-implement-mapping-scenarios/_static/image10.png)

Pak přetáhneme funkce NearestDinners a DistanceBetween do návrháře LINQ to SQL, který způsobí, že budou přidány jako metody na naší LINQ to SQL třídy NerdDinnerDataContext:

![](use-ajax-to-implement-mapping-scenarios/_static/image11.png)

Pak můžeme vystavit metodu dotazu "FindByLocation" na naší třídě DinnerRepository, která používá funkci NearestDinner k vrácení nadcházejících večeři, které jsou v 100 mílích zadaného umístění:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample9.cs)]

### <a name="implementing-a-json-based-ajax-search-action-method"></a>Implementace metody akce vyhledávání AJAX založené na JSON

Nyní implementujeme metodu akce kontroleru, která využívá novou metodu úložiště FindByLocation (), která vrátí zpět seznam dat o večeři, který lze použít k naplnění mapy. Tuto metodu akce budeme mít zpátky zpátky data ve formátu JSON (JavaScript Object Notation), aby bylo možné snadno manipulovat pomocí JavaScriptu na klientovi.

Pokud to chcete provést, vytvoříme novou třídu "SearchController" tak, že kliknete pravým tlačítkem na adresář \Controllers a kliknete na příkaz nabídky přidat&gt;Controller. Následně implementujeme metodu akce "SearchByLocation" v rámci nové třídy SearchController, například níže:

[!code-csharp[Main](use-ajax-to-implement-mapping-scenarios/samples/sample10.cs)]

Metoda akce SearchByLocation SearchController interně volá metodu FindByLocation na DinnerRepository, aby získala seznam přilehlých večeři. Místo toho, aby se objekty večeře vracely přímo klientovi, ale místo toho vrátí JsonDinner objekty. Třída JsonDinner zpřístupňuje podmnožinu vlastností večeře (například: z bezpečnostních důvodů nezveřejňuje jména osob, které mají na večeři odpověď). Obsahuje taky vlastnost RSVPCount, která neexistuje na večeři – a která se dynamicky počítá pomocí počítání počtu objektů RSVP přidružených k určité večeři.

Pak použijeme pomocnou metodu JSON () na základní třídě kontroleru a vrátí sekvenci večeře pomocí formátu drátového formátu založeného na formátu JSON. JSON je standardní textový formát pro reprezentace jednoduchých datových struktur. Níže je uveden příklad, jak seznam ve formátu JSON se dvěma JsonDinner objekty vypadá, když se vrátí z naší metody akce:

[!code-json[Main](use-ajax-to-implement-mapping-scenarios/samples/sample11.json)]

### <a name="calling-the-json-based-ajax-method-using-jquery"></a>Volání metody AJAX založené na formátu JSON pomocí jQuery

Nyní jsme připraveni aktualizovat domovskou stránku aplikace NerdDinner, aby používala metodu SearchByLocation akce SearchController. Provedete to tak, že otevřete šablonu zobrazení/Views/Home/Index.aspx a aktualizujeme ji tak, aby měla textové pole, tlačítko hledání, naši mapu a &lt;&gt; elementu div s názvem dinnerList:

[!code-aspx[Main](use-ajax-to-implement-mapping-scenarios/samples/sample12.aspx)]

Na stránku pak můžeme přidat dvě funkce JavaScriptu:

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample13.html)]

První funkce JavaScriptu načte mapu při prvním načtení stránky. Druhá funkce JavaScriptu nahlasuje obslužnou rutinu události v JavaScriptu kliknutím na tlačítko Hledat. Když je stisknuto tlačítko, volá funkci JavaScriptu FindDinnersGivenLocation (), kterou přidáme do našeho souboru map. js:

[!code-javascript[Main](use-ajax-to-implement-mapping-scenarios/samples/sample14.js)]

Tato funkce FindDinnersGivenLocation () volá mapu. Find () na ovládacím prvku Virtual Earth ho zaprostřední na zadané místo. Když se služba Virtual Earth map vrátí, mapa. Metoda Find () vyvolá metodu zpětného volání callbackUpdateMapDinners, kterou jsme předali jako konečný argument.

Metoda callbackUpdateMapDinners () je místo, kde je skutečná práce dokončena. Pomocí pomocné metody jQuery $. post () zavolá AJAX do metody akce SearchByLocation () naší SearchController () a předá jí zeměpisnou šířku a délku nově zarovnaného vycentrovat mapy. Definuje vloženou funkci, která bude volána po dokončení pomocné metody $. post () a výsledky večeře ve formátu JSON vrácené z metody akce SearchByLocation () budou předány pomocí proměnné s názvem "večeře". Pak provede foreach nad každou vrácenou večeři a pomocí zeměpisné šířky a délky a dalších vlastností přidá nový PIN kód na mapě. Přidá taky položku večeře do seznamu v kódu HTML večeře napravo od mapy. Potom vytvoří pro připínáček i seznam HTML událost najetí myší, aby se zobrazily podrobnosti o večeři, když na ně uživatel najede myší:

[!code-html[Main](use-ajax-to-implement-mapping-scenarios/samples/sample15.html)]

A teď když aplikaci spustíme a navštívíme domovskou stránku, zobrazí se mapa. Když zadáte název města, na které bude mapa zobrazovat nadcházející večeři v blízkosti této:

![](use-ajax-to-implement-mapping-scenarios/_static/image12.png)

Po najetí myší na večeři se zobrazí podrobnosti.

Kliknutím na název večeře buď v bublině, nebo na pravé straně v seznamu HTML přejdete na večeři – což můžeme volitelně použít pro zasílání zpráv protokol RSVP:

![](use-ajax-to-implement-mapping-scenarios/_static/image13.png)

### <a name="next-step"></a>Další krok

Nyní jsme implementovali všechny funkce aplikace naší aplikace NerdDinner. Teď se podíváme na to, jak můžeme povolit automatizované testování částí.

> [!div class="step-by-step"]
> [Předchozí](use-ajax-to-deliver-dynamic-updates.md)
> [Další](enable-automated-unit-testing.md)

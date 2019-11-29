---
uid: web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-vb
title: Zobrazení binárních dat ve webových ovládacích prvcích dat (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se podíváme na možnosti, jak prezentovat binární data na webové stránce, včetně zobrazení souboru obrázku a zřízení odkazu ke stažení f...
ms.author: riande
ms.date: 03/27/2007
ms.assetid: 9201656a-e1c2-4020-824b-18fb632d2925
msc.legacyurl: /web-forms/overview/data-access/working-with-binary-files/displaying-binary-data-in-the-data-web-controls-vb
msc.type: authoredcontent
ms.openlocfilehash: 27c901af092aa990f557750dc5d2c42ba2644c02
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640702"
---
# <a name="displaying-binary-data-in-the-data-web-controls-vb"></a>Zobrazení binárních dat ve webových ovládacích prvcích dat (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stáhnout ukázkovou aplikaci](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_55_VB.exe) nebo [Stáhnout PDF](displaying-binary-data-in-the-data-web-controls-vb/_static/datatutorial55vb1.pdf)

> V tomto kurzu se podíváme na možnosti, jak prezentovat binární data na webové stránce, včetně zobrazení souboru obrázku a zřízení odkazu ke stažení pro soubor PDF.

## <a name="introduction"></a>Úvod

V předchozím kurzu jsme prozkoumali dva postupy pro přiřazení binárních dat k základnímu datovému modelu aplikace a pomocí ovládacího prvku pro nahrání souborů nahrajte soubory z prohlížeče do systému souborů webového serveru s. Ještě jsme viděli, jak přidružit nahraná binární data k datovému modelu. To znamená, že po nahrání a uložení souboru do systému souborů musí být cesta k souboru uložena v příslušném záznamu databáze. Pokud jsou data ukládána přímo v databázi, pak nahraná binární data nemusí být uložena do systému souborů, ale musí být vložena do databáze.

Předtím, než se podíváme na přiřazení dat k datovému modelu, si ale nejdřív podíváme, jak zadat binární data pro koncového uživatele. Prezentace textových dat je dostatečně jednoduchá, ale jak mají být prezentována binární data? Záleží samozřejmě na typu binárních dat. V případě imagí nejspíš chceme zobrazit obrázek. v případě souborů PDF, dokumentů aplikace Microsoft Word, souborů ZIP a dalších typů binárních dat je pravděpodobně vhodnější poskytnout odkaz ke stažení.

V tomto kurzu se podíváme na to, jak prezentovat binární data spolu s přidruženými textovými daty pomocí datových ovládacích prvků web, jako jsou GridView a DetailsView. V dalším kurzu provedeme naši pozornost přidružení nahraného souboru k databázi.

## <a name="step-1-providingbrochurepathvalues"></a>Krok 1: poskytování hodnot`BrochurePath`

Sloupec `Picture` v tabulce `Categories` již obsahuje binární data pro různé image kategorií. Konkrétně sloupec `Picture` pro každý záznam obsahuje binární obsah rastrového obrázku s nízkou kvalitou, 16 barev. Každý obrázek kategorie má 172 pixelů na šířku a 120 pixelů na výšku a spotřebovává zhruba 11 KB. Čím více, binární obsah ve sloupci `Picture` obsahuje hlavičku [OLE](http://en.wikipedia.org/wiki/Object_Linking_and_Embedding) 78 bajtů, která musí být před zobrazením obrázku odstraněna. Tyto informace hlavičky jsou k dispozici, protože databáze Northwind má své kořeny v aplikaci Microsoft Access. V aplikaci Access se binární data ukládají pomocí datového typu objektu OLE, který se v této hlavičce rozsměruje. Prozatím se dozvíte, jak oddělit hlavičky z těchto kvalitních imagí, aby se zobrazil obrázek. V budoucím kurzu sestavíme rozhraní pro aktualizaci sloupce kategorie s `Picture` a nahradíte tyto bitmapové obrázky, které používají záhlaví OLE, s ekvivalentními obrázky JPG bez zbytečných hlaviček OLE.

V předchozím kurzu jsme viděli, jak používat ovládací prvek pro nahrání souborů. Proto můžete pokračovat a přidat soubory brožur do systému souborů webového serveru s. V takovém případě ale neaktualizuje sloupec `BrochurePath` v tabulce `Categories`. V dalším kurzu se dozvíte, jak toho dosáhnout, ale pro teď potřebujeme ručně zadat hodnoty pro tento sloupec.

V tomto kurzu pro stažení najdete sedm souborů brožury PDF ve složce `~/Brochures`, jednu pro každou z kategorií s výjimkou rybích plodů. Záměrně jsem při přidávání brožury o mořském plodu, který ilustruje způsob zpracování scénářů, ve kterých nejsou ke všem záznamům přidružená binární data. Chcete-li aktualizovat `Categories`ovou tabulku pomocí těchto hodnot, klikněte pravým tlačítkem myši na uzel `Categories` z Průzkumník serveru a vyberte možnost zobrazit data tabulky. Pak zadejte virtuální cesty k souborům brožur pro každou kategorii, která obsahuje leták, jak ukazuje obrázek 1. Vzhledem k tomu, že pro kategorii rybího moře není k dispozici žádná brožura, ponechte hodnotu `BrochurePath` sloupce s jako `NULL`.

[![ručně zadat hodnoty pro sloupec Categories Table s BrochurePath](displaying-binary-data-in-the-data-web-controls-vb/_static/image1.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image1.png)

**Obrázek 1**: ručně zadejte hodnoty pro sloupec `Categories` `BrochurePath` tabulky ([kliknutím zobrazíte obrázek v plné velikosti).](displaying-binary-data-in-the-data-web-controls-vb/_static/image2.png)

## <a name="step-2-providing-a-download-link-for-the-brochures-in-a-gridview"></a>Krok 2: poskytnutí odkazu ke stažení pro brožury v prvku GridView

S `BrochurePath` hodnotami zadanými pro tabulku `Categories` jsme znovu připraveni vytvořit prvek GridView, který obsahuje seznam jednotlivých kategorií spolu s odkazem na stažení kategorie s brožurou. V kroku 4 rozšíříme tento prvek GridView a zobrazí se také obrázek kategorie s.

Začněte přetažením prvku GridView z panelu nástrojů do návrháře stránky `DisplayOrDownloadData.aspx` ve složce `BinaryData`. Nastavte `ID` prvku GridView s `Categories` a pomocí inteligentní značky GridView s vyberte, že se má vytvořit vazba k novému zdroji dat. Konkrétně ho navažte na prvek ObjectDataSource s názvem `CategoriesDataSource`, který načte data pomocí metody `CategoriesBLL` Object s `GetCategories()`.

[![vytvořit nový prvek ObjectDataSource s názvem CategoriesDataSource](displaying-binary-data-in-the-data-web-controls-vb/_static/image2.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image3.png)

**Obrázek 2**: vytvoření nového prvku ObjectDataSource s názvem `CategoriesDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](displaying-binary-data-in-the-data-web-controls-vb/_static/image4.png))

[![nakonfigurovat prvek ObjectDataSource tak, aby používal třídu CategoriesBLL](displaying-binary-data-in-the-data-web-controls-vb/_static/image3.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image5.png)

**Obrázek 3**: Konfigurace prvku ObjectDataSource, aby používal třídu `CategoriesBLL` ([kliknutím zobrazíte obrázek v plné velikosti](displaying-binary-data-in-the-data-web-controls-vb/_static/image6.png))

[![načíst seznam kategorií pomocí metody GetCategories ()](displaying-binary-data-in-the-data-web-controls-vb/_static/image4.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image7.png)

**Obrázek 4**: načtení seznamu kategorií pomocí metody `GetCategories()` ([kliknutím zobrazíte obrázek v plné velikosti](displaying-binary-data-in-the-data-web-controls-vb/_static/image8.png))

Po dokončení Průvodce konfigurací zdroje dat bude Visual Studio automaticky přidávat vlastnost BoundField do `Categories` GridView pro `CategoryID`, `CategoryName`, `Description`, `NumberOfProducts`a `BrochurePath` `DataColumn` s. Pokračujte a odeberte `NumberOfProducts` vlastnost BoundField, protože dotaz `GetCategories()` metody s nenačítá tyto informace. Odeberte taky `CategoryID` vlastnost BoundField a přejmenujte `CategoryName` a `BrochurePath` vlastnosti `HeaderText` na kategorie a brožury. Po provedení těchto změn by deklarativní značky GridView a ObjectDataSource s měly vypadat takto:

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample1.aspx)]

Zobrazit tuto stránku v prohlížeči (viz obrázek 5). V seznamu se zobrazí každá z těchto osmi kategorií. Sedm kategorií s hodnotami `BrochurePath` má `BrochurePath` hodnotu zobrazenou v příslušném vlastnost BoundField. Ryby, u kterých je `NULL` hodnotou `BrochurePath`, se zobrazí prázdná buňka.

[![je uvedena každá kategorie s názvem, popisem a hodnotou BrochurePath.](displaying-binary-data-in-the-data-web-controls-vb/_static/image5.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image9.png)

**Obrázek 5**: v seznamu jsou uvedeny všechny kategorie s názvem, popis a `BrochurePath` ([kliknutím zobrazíte obrázek v plné velikosti](displaying-binary-data-in-the-data-web-controls-vb/_static/image10.png)).

Místo zobrazení textu `BrochurePath`ho sloupce chceme vytvořit odkaz na leták. K tomu je potřeba odebrat `BrochurePath` vlastnost BoundField a nahradit ho HyperLinkField. Nastavte novou vlastnost HyperLinkField s `HeaderText` na hodnotu leták, její vlastnost `Text` na hodnotu zobrazit brožuru a její vlastnost `DataNavigateUrlFields` na `BrochurePath`.

![Přidat HyperLinkField pro BrochurePath](displaying-binary-data-in-the-data-web-controls-vb/_static/image6.gif)

**Obrázek 6**: Přidání HyperLinkField pro `BrochurePath`

Tím se přidá sloupec odkazů do prvku GridView, jak ukazuje obrázek 7. Kliknutím na odkaz zobrazení brožury se PDF buď zobrazí přímo v prohlížeči, nebo vyzve uživatele ke stažení souboru v závislosti na tom, jestli je nainstalovaná čtečka PDF a nastavení prohlížeče s.

[![můžete zobrazit brožuru kategorie s kliknutím na odkaz Zobrazit brožuru.](displaying-binary-data-in-the-data-web-controls-vb/_static/image7.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image11.png)

**Obrázek 7**: Brožura kategorie s se dá zobrazit kliknutím na odkaz Zobrazit brožuru ([kliknutím zobrazíte obrázek v plné velikosti](displaying-binary-data-in-the-data-web-controls-vb/_static/image12.png)).

[Zobrazuje se ![kategorie s brožurou PDF.](displaying-binary-data-in-the-data-web-controls-vb/_static/image8.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image13.png)

**Obrázek 8**: zobrazení kategorie s brožurou PDF ([kliknutím zobrazíte obrázek v plné velikosti](displaying-binary-data-in-the-data-web-controls-vb/_static/image14.png))

## <a name="hiding-the-view-brochure-text-for-categories-without-a-brochure"></a>Skrytí textu v brožuře zobrazení pro kategorie bez brožury

Jak ukazuje obrázek 7, `BrochurePath` HyperLinkField zobrazí hodnotu vlastnosti `Text` (zobrazení brožury) pro všechny záznamy bez ohledu na to, zda existuje hodnota, která není`NULL` pro `BrochurePath`. Pokud je samozřejmě `BrochurePath` `NULL`, odkaz se zobrazí pouze jako text, jako je například případ s kategorií rybích plodů (odkaz zpět na obrázek 7). Místo zobrazení textu v podobě brožury může být vhodné, aby tyto kategorie bez `BrochurePath` hodnoty zobrazovaly nějaký alternativní text, například není dostupná žádná brožura.

Aby bylo možné toto chování poskytnout, musíme použít TemplateField, jehož obsah je generován prostřednictvím volání metody stránky, která generuje příslušný výstup na základě `BrochurePath` hodnoty. Nejdříve jsme tuto techniku formátování prozkoumali zpět v kurzu [použití templatefields v ovládacím prvku GridView](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) .

Přepněte HyperLinkField na TemplateField tím, že vyberete `BrochurePath` HyperLinkField a pak kliknete na tlačítko převést toto pole na odkaz TemplateField v dialogovém okně Upravit sloupce.

![Převést HyperLinkField na TemplateField](displaying-binary-data-in-the-data-web-controls-vb/_static/image9.gif)

**Obrázek 9**: převod HyperLinkField na TemplateField

Tím se vytvoří TemplateField s `ItemTemplate`, která obsahuje webový ovládací prvek hypertextového odkazu, jehož vlastnost `NavigateUrl` je svázána s hodnotou `BrochurePath`. Nahraďte tento kód voláním metody `GenerateBrochureLink`a předejte hodnotu `BrochurePath`:

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample2.aspx)]

Dále vytvořte metodu `Protected` ve třídě ASP.NET stránky s kódem na pozadí s názvem `GenerateBrochureLink`, která vrací `String` a přijímá `Object` jako vstupní parametr.

[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample3.vb)]

Tato metoda určuje, zda je hodnota předaného `Object` databáze `NULL` a pokud ano, vrátí zprávu oznamující, že v kategorii chybí brožura. V opačném případě, pokud je `BrochurePath` hodnota, zobrazí se v hypertextovém odkazu. Všimněte si, že pokud je hodnota `BrochurePath` přítomna, je předána [metodě`ResolveUrl(url)`](https://msdn.microsoft.com/library/system.web.ui.control.resolveurl.aspx). Tato metoda vyřeší předanou *adresu URL*a nahradí `~` znak odpovídající virtuální cestou. Například pokud je aplikace rootem na `/Tutorial55`, `ResolveUrl("~/Brochures/Meats.pdf")` vrátí `/Tutorial55/Brochures/Meat.pdf`.

Obrázek 10 ukazuje stránku po použití těchto změn. Všimněte si, že pole `BrochurePath` kategorie v mořských plodech nyní zobrazuje text bez dostupné brožury.

[![text není k dispozici žádná brožura pro tyto kategorie bez brožury.](displaying-binary-data-in-the-data-web-controls-vb/_static/image10.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image15.png)

**Obrázek 10**: text žádná brožura není k dispozici pro tyto kategorie bez brožury ([kliknutím zobrazíte obrázek v plné velikosti).](displaying-binary-data-in-the-data-web-controls-vb/_static/image16.png)

## <a name="step-3-adding-a-web-page-to-display-a-category-s-picture"></a>Krok 3: Přidání webové stránky pro zobrazení obrázku kategorie s

Když uživatel navštíví stránku ASP.NET, obdrží stránku ASP.NET stránky s kódem HTML. Přijatý kód HTML je pouze text a neobsahuje žádná binární data. Všechna další binární data, jako jsou obrázky, zvukové soubory, aplikace Macromedia Flash, vložená Media Player videa Windows a tak dále, existují jako samostatné prostředky na webovém serveru. KÓD HTML obsahuje odkazy na tyto soubory, ale nezahrnuje skutečný obsah souborů.

Například v jazyce HTML je `<img>` element použit pro odkazování na obrázek, s atributem `src` odkazujícím na soubor obrázku, například:

[!code-html[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample4.html)]

Když prohlížeč tento kód HTML obdrží, provede další požadavek na webový server, který načte binární obsah souboru obrázku, který se pak zobrazí v prohlížeči. Stejný koncept platí pro všechna binární data. V kroku 2 se brožura neodeslala do prohlížeče jako součást značky HTML stránky. Namísto toho vykreslené hypertextové odkazy HTML, které po kliknutí vyvolaly, způsobila, že prohlížeč požaduje přímo dokument PDF.

Chcete-li zobrazit nebo dovolit uživatelům stahovat binární data, která jsou uložena v databázi, musíme vytvořit samostatnou webovou stránku, která vrací data. Pro naši aplikaci je k dispozici pouze jedno binární datové pole, které je přímo v databázi Uloženo v kategorii s obrázkem. Proto potřebujeme stránku, která při volání vrátí data obrázku konkrétní kategorie.

Přidejte novou stránku ASP.NET do složky `BinaryData` s názvem `DisplayCategoryPicture.aspx`. Když to uděláte, ponechejte políčko vybrat hlavní stránku nezaškrtnuté. Tato stránka očekává `CategoryID` hodnotu v řetězci QueryString a vrátí binární data pro daný sloupec kategorie s `Picture`. Vzhledem k tomu, že tato stránka vrací binární data a nic jiného, nepotřebuje žádný kód v oddílu HTML. Proto klikněte v levém dolním rohu na kartu zdroj a odeberte všechny značky stránky s výjimkou direktivy `<%@ Page %>`. To znamená, že deklarativní označení `DisplayCategoryPicture.aspx` s by se měla skládat z jednoho řádku:

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample5.aspx)]

Pokud se v direktivě `<%@ Page %>` zobrazí atribut `MasterPageFile`, odeberte ho.

Do třídy s kódem na pozadí přidejte následující kód do obslužné rutiny události `Page_Load`:

[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample6.vb)]

Tento kód začíná čtením v `CategoryID` hodnota QueryString do proměnné s názvem `categoryID`. V dalším kroku se data obrázku načítají prostřednictvím volání metody `CategoriesBLL` třídy s `GetCategoryWithBinaryDataByCategoryID(categoryID)`. Tato data se vrátí klientovi pomocí metody `Response.BinaryWrite(data)`, ale před tím, než se zavolá, se musí odstranit záhlaví `Picture` sloupce s hodnotou OLE. K tomu je potřeba vytvořit pole `Byte` s názvem `strippedImageData`, která budou obsahovat přesně 78 znaků, než je ve sloupci `Picture`. [Metoda`Array.Copy`](https://msdn.microsoft.com/library/z50k9bft.aspx) slouží ke zkopírování dat z `category.Picture` počínaje pozicí 78 až do `strippedImageData`.

Vlastnost `Response.ContentType` Určuje [typ MIME](http://en.wikipedia.org/wiki/MIME) vraceného obsahu, aby prohlížeč věděl, jak ho vykreslit. Vzhledem k tomu, že sloupec `Categories` `Picture` tabulky je rastrový obrázek, tady se používá typ MIME rastrového obrázku (obrázek/bmp). Vynecháte-li typ MIME, bude většina prohlížečů stále zobrazovat obrázek správně, protože může odvodit typ na základě obsahu binárních dat souboru obrázku. Nicméně je obezřetné zahrnout typ MIME, pokud je to možné. Úplný seznam [typů médií MIME](http://www.iana.org/assignments/media-types/)najdete na [webu Internet Assigned Numbers Authority](http://www.iana.org/) .

Po vytvoření této stránky můžete zobrazit konkrétní obrázek kategorie s `DisplayCategoryPicture.aspx?CategoryID=categoryID`. Obrázek 11 znázorňuje obrázek kategorie nápoje, který se dá zobrazit z `DisplayCategoryPicture.aspx?CategoryID=1`.

[![se zobrazuje obrázek kategorie nápoje](displaying-binary-data-in-the-data-web-controls-vb/_static/image11.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image17.png)

**Obrázek 11**: zobrazuje se obrázek kategorie nápoje ([kliknutím zobrazíte obrázek v plné velikosti).](displaying-binary-data-in-the-data-web-controls-vb/_static/image18.png)

Pokud při návštěvě `DisplayCategoryPicture.aspx?CategoryID=categoryID`dojde k výjimce, která čtení nedokáže přetypovat objekt typu System. DBNull na typ System. Byte [], existují dvě věci, které mohou být příčinou. Nejdříve `Picture` sloupec `Categories` tabulek s povoluje hodnoty `NULL`. `DisplayCategoryPicture.aspx` stránka však předpokládá, že existuje hodnota, která není`NULL`. Vlastnost `Picture` `CategoriesDataTable` nelze použít přímo, pokud má hodnotu `NULL`. Pokud chcete povolit `NULL` hodnoty pro sloupec `Picture`, přejete si, že chcete zahrnout následující podmínku:

[!code-vb[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample7.vb)]

Výše uvedený kód předpokládá, že existuje nějaký soubor obrázku s názvem `NoPictureAvailable.gif` ve složce `Images`, kterou chcete zobrazit pro tyto kategorie bez obrázku.

Tato výjimka by mohla být také způsobena tím, že se příkaz `CategoriesTableAdapter` s `GetCategoryWithBinaryDataByCategoryID` metodě s `SELECT` vrátí zpět na hlavní seznam sloupců dotazů, ke kterému může dojít, pokud používáte příkazy SQL ad hoc a vy znovu spustíte Průvodce pro hlavní dotaz TableAdapter s. Zkontrolujte, zda `GetCategoryWithBinaryDataByCategoryID` metoda s `SELECT` příkaz stále obsahuje sloupec `Picture`.

> [!NOTE]
> Pokaždé, když se `DisplayCategoryPicture.aspx` navštíví, k databázi se dostanete a vrátí se zadané údaje o obrázcích pro kategorie s. Pokud se obrázek kategorie s nezměnil, protože ho uživatel naposledy zobrazil, je to však nevyužité úsilí. Naštěstí protokol HTTP umožňuje *podmíněné načtení*. Klient, který vydává požadavek HTTP, odesílá společně [`If-Modified-Since` HLAVIČCE http](http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html) , která poskytuje datum a čas posledního načtení tohoto prostředku z webového serveru od klienta. Pokud se obsah od tohoto zadaného data nezměnil, může webový server reagovat s [nezměněným stavovým kódem (304)](http://www.w3.org/Protocols/rfc2616/rfc2616-sec10.html) a neposílá zpět požadovaný obsah prostředku. V krátké době tato technika zbavuje webový server, že potřebuje odeslat obsah pro prostředek, pokud se nezměnil od chvíle, kdy se klient naposledy připojil.

K implementaci tohoto chování ale vyžaduje přidání `PictureLastModified`ho sloupce do tabulky `Categories` k zachycení při poslední aktualizaci sloupce `Picture` a také kódu pro kontrolu `If-Modified-Since` hlavičky. Další informace o hlavičkách `If-Modified-Since` a pracovním postupu podmíněného načtení najdete v tématu [http podmíněný přístup pro hackery RSS](http://fishbowl.pastiche.org/2002/10/21/http_conditional_get_for_rss_hackers) a [hlubší pohled na provádění požadavků HTTP na stránce ASP.NET](http://aspnet.4guysfromrolla.com/articles/122204-1.aspx).

## <a name="step-4-displaying-the-category-pictures-in-a-gridview"></a>Krok 4: zobrazení obrázků kategorií v prvku GridView

Teď, když máme webovou stránku pro zobrazení konkrétní kategorie s obrázkem, můžeme ji zobrazit pomocí [webového ovládacího prvku obrázek](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/standard/image.aspx) nebo `<img>` HTML elementu, který odkazuje na `DisplayCategoryPicture.aspx?CategoryID=categoryID`. Obrázky, jejichž adresa URL je určena daty databáze, mohou být zobrazeny v prvku GridView nebo DetailsView pomocí ImageField. ImageField obsahuje vlastnosti `DataImageUrlField` a `DataImageUrlFormatString`, které fungují jako `DataNavigateUrlFields` HyperLinkField s a vlastnosti `DataNavigateUrlFormatString`.

Nechejte rozšířit `Categories` GridView v `DisplayOrDownloadData.aspx` přidáním ImageField, aby se zobrazily jednotlivé obrázky kategorií. Jednoduše přidejte ImageField a nastavte jeho `DataImageUrlField` a vlastnosti `DataImageUrlFormatString` na `CategoryID` a `DisplayCategoryPicture.aspx?CategoryID={0}`v uvedeném pořadí. Tím se vytvoří sloupec GridView, který vykreslí `<img>` element, jehož `src` odkazuje na atribut `DisplayCategoryPicture.aspx?CategoryID={0}`, kde {0} je nahrazeno hodnotou `CategoryID` řádku GridView.

![Přidat ImageField do prvku GridView.](displaying-binary-data-in-the-data-web-controls-vb/_static/image12.gif)

**Obrázek 12**: Přidání prvku ImageField do prvku GridView.

Po přidání ImageField by vaše deklarativní syntaxe GridViewu měla vypadat jako soothe po:

[!code-aspx[Main](displaying-binary-data-in-the-data-web-controls-vb/samples/sample8.aspx)]

Chvíli počkejte, než tuto stránku zobrazíte v prohlížeči. Všimněte si, jak každý záznam nyní obsahuje obrázek pro kategorii.

[![je pro každý řádek zobrazený obrázek kategorie s](displaying-binary-data-in-the-data-web-controls-vb/_static/image13.gif)](displaying-binary-data-in-the-data-web-controls-vb/_static/image19.png)

**Obrázek 13**: kategorie s – obrázek se zobrazí pro každý řádek ([kliknutím zobrazíte obrázek v plné velikosti](displaying-binary-data-in-the-data-web-controls-vb/_static/image20.png)).

## <a name="summary"></a>Přehled

V tomto kurzu jsme prozkoumali, jak prezentovat binární data. Způsob, jakým jsou data uvedena, závisí na typu dat. Pro soubory brožur PDF jsme uživatelům nabídli odkaz na zobrazení brožury, který po kliknutí přivedl uživatele přímo k souboru PDF. V případě obrázku kategorie s jsme nejprve vytvořili stránku, která načte a vrátí binární data z databáze a pak tuto stránku použila k zobrazení všech kategorií s v prvku GridView.

Teď, když jsme si vyhledali, jak zobrazit binární data, jsme přezkoumali, jak provést vkládání, aktualizace a odstraňování dat v databázi s binárními daty. V dalším kurzu se podíváme na to, jak přidružit nahraný soubor k odpovídajícímu záznamu databáze. V tomto kurzu se dozvíte, jak aktualizovat existující binární data a jak odstranit binární data při odebrání přidruženého záznamu.

Šťastné programování!

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucích k tomuto kurzu byli Teresa Murphy a Dave Gardner. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](uploading-files-vb.md)
> [Další](including-a-file-upload-option-when-adding-a-new-record-vb.md)

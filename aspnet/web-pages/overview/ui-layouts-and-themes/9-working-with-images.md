---
uid: web-pages/overview/ui-layouts-and-themes/9-working-with-images
title: Práce s obrázky na webu ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: V této kapitole se dozvíte, jak přidat, zobrazit a manipulovat s obrázky (změnit velikost, překlopit a přidat meze) na vašem webu.
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 778c4e58-4372-4d25-bab9-aec4a8d8e38d
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/9-working-with-images
msc.type: authoredcontent
ms.openlocfilehash: 53514b3c314fc182a43c82974ffcfa8158a636a1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78631857"
---
# <a name="working-with-images-in-an-aspnet-web-pages-razor-site"></a>Práce s obrázky na webu ASP.NET Web Pages (Razor)

tím, že [FitzMacken](https://github.com/tfitzmac)

> V tomto článku se dozvíte, jak přidat, zobrazit a manipulovat s obrázky (Změna velikosti, překlopení a přidání vodoznaků) na webu ASP.NET Web Pages (Razor).
> 
> Naučíte se:
> 
> - Jak dynamicky přidat obrázek na stránku
> - Jak umožnit uživatelům odeslat obrázek.
> - Jak změnit velikost obrázku
> - Jak překlopit nebo otočit obrázek
> - Postup přidání vodoznaku do obrázku
> - Použití obrázku jako meze.
> 
> Jedná se o funkce ASP.NET programování, které jsou představené v článku:
> 
> - Pomocná rutina `WebImage`
> - Objekt `Path`, který poskytuje metody, které umožňují pracovat s cestami a názvy souborů.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 2
> - WebMatrix 2
>   
> 
> V tomto kurzu se používá také WebMatrix 3.

<a id="Adding_an_Image"></a>
## <a name="adding-an-image-to-a-web-page-dynamically"></a>Dynamické přidání obrázku na webovou stránku

Při vývoji webu můžete přidat obrázky na svůj web a na jednotlivé stránky. Můžete také umožnit uživatelům odeslat obrázky, které mohou být užitečné pro úlohy, jako je například umožnění Přidání fotografie profilu.

Pokud je obrázek již na vašem webu k dispozici a chcete jej pouze zobrazit na stránce, použijte prvek HTML `<img>` takto:

[!code-html[Main](9-working-with-images/samples/sample1.html)]

Někdy je ale potřeba, abyste mohli obrázky dynamicky &#8212; zobrazovat, ale nevíte, jaký obrázek chcete zobrazit, dokud stránka neběží.

Postup v této části ukazuje, jak zobrazit obrázek průběžně, kde uživatelé určují název souboru obrázku ze seznamu názvů obrázků. Vyberou název obrázku z rozevíracího seznamu a při odeslání stránky se zobrazí obrázek, který vybrali.

![obrazu](9-working-with-images/_static/image1.jpg "ch9images-1. jpg")

1. V WebMatrixu vytvořte nový web.
2. Přidejte novou stránku s názvem *DynamicImage. cshtml*.
3. V kořenové složce webu přidejte novou složku a pojmenujte ji jako *Image*.
4. Přidejte čtyři obrázky do složky *images* , kterou jste právě vytvořili. (Všechny užitečné obrázky budou, ale měly by se vejít na stránku.) Přejmenujte obrázky *Photo1. jpg*, *Photo2. jpg*, *Photo3. jpg*a *Photo4. jpg*. (V tomto postupu nebudete používat *Photo4. jpg* , ale budete ho používat později v článku.)
5. Ověřte, že čtyři bitové kopie nejsou označeny jako jen pro čtení.
6. Stávající obsah stránky nahraďte následujícím způsobem:

    [!code-cshtml[Main](9-working-with-images/samples/sample2.cshtml)]

    Tělo stránky obsahuje rozevírací seznam (`<select>` element), který má název `photoChoice`. Seznam má tři možnosti a atribut `value` každé možnosti seznamu má název jedné z imagí, které vložíte do složky *images* . V podstatě vám seznam umožní uživateli vybrat popisný název, například &quot;fotografii 1&quot;, a po odeslání stránky předává název souboru *. jpg* .

    V kódu můžete získat výběr uživatele (jinými slovy, název souboru obrázku) ze seznamu, a to čtením `Request["photoChoice"]`. Nejprve se zobrazí, zda existuje výběr. Pokud je k dispozici, vytvoříte cestu k obrázku, který se skládá z názvu složky pro obrázky a názvu souboru obrázku uživatele. (Pokud jste se pokusili vytvořit cestu, ale nedošlo k žádnému `Request["photoChoice"]`, zobrazí se chyba.) Výsledkem je relativní cesta, například:

    *obrázky/Photo1. jpg*

    Cesta je uložena v proměnné s názvem `imagePath`, kterou budete později potřebovat na stránce.

    V těle je také `<img>` element, který se používá k zobrazení obrázku, který uživatel vybral. Atribut `src` není nastaven na název souboru nebo na adresu URL, třeba v případě, že byste chtěli zobrazit statický prvek. Místo toho je nastavená na `@imagePath`, což znamená, že získá hodnotu z cesty, kterou jste nastavili v kódu.

    Při prvním spuštění stránky, ale není k dispozici žádný obrázek k zobrazení, protože uživatel nic nevybrali. To obvykle znamená, že atribut `src` by byl prázdný a obrázek by se zobrazil jako červený &quot;x&quot; (nebo bez ohledu na to, jestli se v prohlížeči nenajde obrázek). Chcete-li tomu zabránit, vložte prvek `<img>` do bloku `if`, který testuje, zda obsahuje `imagePath` proměnná, která obsahuje nějaké informace. Pokud uživatel provedl výběr, `imagePath` obsahuje cestu. Pokud uživatel nezvolil obrázek, nebo pokud se jedná o první zobrazení stránky, `<img>` element není ani vykreslen.
7. Uložte soubor a spusťte stránku v prohlížeči. (Před spuštěním se ujistěte, že je stránka vybraná v pracovním prostoru **soubory** .)
8. V rozevíracím seznamu vyberte obrázek a klikněte na **ukázkový obrázek**. Ujistěte se, že se zobrazují různé obrázky pro různé volby.

<a id="Uploading_an_Image"></a>
## <a name="uploading-an-image"></a>Nahrání obrázku

Předchozí příklad ukazuje, jak dynamicky zobrazit obrázek, ale pracoval pouze s obrázky, které již byly na vašem webu. Tento postup ukazuje, jak umožnit uživatelům odeslat obrázek, který se pak zobrazí na stránce. V ASP.NET můžete pomocí pomocné rutiny `WebImage` manipulovat s imagemi, které obsahují metody, které umožňují vytvářet, manipulovat a ukládat obrázky. Pomocná rutina `WebImage` podporuje všechny běžné typy souborů webové image, včetně *. jpg*, *. png*a *. bmp*. V celém článku budete používat obrázky *. jpg* , ale můžete použít libovolný z těchto typů obrázků.

![obrazu](9-working-with-images/_static/image2.jpg "ch9images-2. jpg")

1. Přidejte novou stránku a pojmenujte ji *UploadImage. cshtml*.
2. Stávající obsah stránky nahraďte následujícím způsobem: 

    [!code-cshtml[Main](9-working-with-images/samples/sample3.cshtml)]

    Tělo textu má element `<input type="file">`, který umožňuje uživatelům vybrat soubor, který se má nahrát. Když kliknete na **Odeslat**, soubor, který se vybere, se odešle spolu s formulářem.

    K získání nahraného obrázku použijte pomocníka `WebImage`, který obsahuje nejrůznější užitečné metody pro práci s obrázky. Konkrétně se používá `WebImage.GetImageFromRequest` k získání nahraného obrázku (pokud existuje) a jeho uložení do proměnné s názvem `photo`.

    Spousta práce v tomto příkladu zahrnuje získání a nastavení názvů souborů a cest. Problém je, že chcete získat název (a pouze název) image, kterou uživatel nahrál, a pak vytvořit novou cestu, do které budete image ukládat. Vzhledem k tomu, že uživatelé mohou nahrát více obrázků se stejným názvem, použijete pro vytváření jedinečných názvů bitovou kopii dalšího kódu a zajistěte, aby uživatelé nepřepsali existující obrázky.

    Pokud byl obrázek odeslán (test `if (photo != null)`), získá se název obrázku z vlastnosti `FileName` obrázku. Když uživatel obrázek nahraje, `FileName` obsahuje původní název uživatele, který zahrnuje cestu z počítače uživatele. Může to vypadat takto:

    *C:\Users\Joe\Pictures\SamplePhoto1.jpg*

    Nechcete všechny tyto informace o cestě, ale &#8212; chcete mít jenom skutečný název souboru (*SamplePhoto1. jpg*). Pomocí metody `Path.GetFileName` můžete prokládat pouze soubor z cesty, například takto:

    [!code-csharp[Main](9-working-with-images/samples/sample4.cs)]

    Pak můžete vytvořit nový jedinečný název souboru přidáním identifikátoru GUID k původnímu názvu. (Další informace o identifikátorech GUID najdete v tématu [o guidch](#SB_AboutGUIDs) dále v tomto článku.) Pak vytvoříte úplnou cestu, kterou můžete použít k uložení obrázku. Cesta pro uložení se skládá z nového názvu souboru, složky (imagí) a aktuálního umístění webu.

    > [!NOTE]
    > Aby váš kód ukládal soubory do složky *imagí* , aplikace potřebuje oprávnění ke čtení i zápisu pro tuto složku. Ve vývojovém počítači to není obvykle problém. Když ale publikujete web na webový server poskytovatele hostingu, možná budete muset tato oprávnění výslovně nastavit. Pokud spustíte tento kód na serveru poskytovatele hostingu a získáte chyby, obraťte se na poskytovatele hostingu a zjistěte, jak tato oprávnění nastavit.

    Nakonec předáte cestu pro uložení do metody `Save` pomocné rutiny `WebImage`. Tím se nahraný obrázek uloží pod jeho nový název. Metoda Save vypadá takto: `photo.Save(@"~\" + imagePath)`. Úplná cesta je připojena k `@"~\"`, což je aktuální umístění webu. (Informace o operátoru `~` naleznete v tématu [Úvod do webového programování ASP.NET pomocí syntaxe Razor](https://go.microsoft.com/fwlink/?LinkId=202890#ID_WorkingWithFileAndFolderPaths).)

    Jak je uvedeno v předchozím příkladu, tělo stránky obsahuje prvek `<img>` pro zobrazení obrázku. Pokud byla nastavena `imagePath`, je prvek `<img>` vykreslen a jeho atribut `src` je nastaven na hodnotu `imagePath`.
3. Spusťte stránku v prohlížeči.
4. Nahrajte obrázek a ujistěte se, že je zobrazený na stránce.
5. V lokalitě otevřete složku *images* . Vidíte, že byl přidán nový soubor, jehož název souboru vypadá nějak takto:: 

    *45ea4527-7ddd-4965-b9ca-c6444982b342\_MyPhoto. png*

    Toto je obrázek, který jste nahráli pomocí identifikátoru GUID s předponou názvu. (Vlastní soubor bude mít jiný identifikátor GUID a pravděpodobně se jmenuje něco jiného než *Myphoto. png*.)

> [!TIP] 
> 
> <a id="SB_AboutGUIDs"></a>
> ### <a name="about-guids"></a>O identifikátorech GUID
> 
> Identifikátor GUID (globálně jedinečné ID) je identifikátor, který se obvykle vykresluje v následujícím formátu: `936DA01F-9ABD-4d9d-80C7-02AF85C822A8`. Čísla a písmena (od A-F) se liší pro každý identifikátor GUID, ale všechny mají stejný postup jako při používání skupin 8-4-4-4-12 znaků. (Technicky, identifikátor GUID je 16 bajtů nebo 128bitové číslo.) Pokud potřebujete identifikátor GUID, můžete zavolat specializovaný kód, který pro vás vygeneruje identifikátor GUID. V rámci identifikátorů GUID je to, že mezi mimořádnou velikostí čísla (3,4 x 10<sup>38</sup>) a algoritmem pro jeho vygenerování je výsledný počet prakticky zaručený jako jeden z druhů. Identifikátory GUID jsou proto dobrým způsobem, jak vygenerovat názvy věcí, pokud musíte zaručit, že nebudete používat stejný název dvakrát. Nevýhodou je samozřejmě, že identifikátory GUID nejsou obzvláště uživatelsky přívětivé, takže mají být použity, pokud se název používá pouze v kódu.

<a id="Resizing_an_Image"></a>
## <a name="resizing-an-image"></a>Změna velikosti obrázku

Pokud web akceptuje obrázky od uživatele, možná budete chtít změnit velikost obrázků, než je zobrazíte nebo uložíte. Pro tuto akci můžete znovu použít pomocníka `WebImage`.

Tento postup ukazuje, jak změnit velikost nahraného obrázku pro vytvoření miniatury a pak uložit miniaturu a původní obrázek na webu. Miniaturu můžete zobrazit na stránce a použít hypertextový odkaz pro přesměrování uživatelů na obrázek v plné velikosti.

![obrazu](9-working-with-images/_static/image3.jpg "ch9images-3. jpg")

1. Přidejte novou stránku s názvem *Thumbnail. cshtml*.
2. Ve složce *images* vytvořte podsložku s názvem *palec*.
3. Stávající obsah stránky nahraďte následujícím způsobem: 

    [!code-cshtml[Main](9-working-with-images/samples/sample5.cshtml)]

    Tento kód je podobný kódu z předchozího příkladu. Rozdílem je, že tento kód uloží obrázek dvakrát, jednou za normálních podmínek, a jednou po vytvoření miniatury bitové kopie. Napřed dostanete nahraný obrázek a uložte ho do složky *images* . Pak vytvoříte novou cestu k obrázku miniatury. Chcete-li vytvořit miniaturu, zavoláte `Resize` metodu `WebImage` pomoc k vytvoření obrázku 60-pixel podle 60-pixel. Tento příklad ukazuje, jak zachováte poměr stran a jak můžete zabránit zvětšování obrázku (pro případ, že by nová velikost znamenala větší velikost obrázku). Obrázek se změněnou velikostí se pak uloží v podsložce s *miniaturami* .

    Na konci značky použijete stejný `<img>` element s atributem Dynamic `src`, který jste si poznamenali v předchozích příkladech, k podmíněnému zobrazení obrázku. V tomto případě zobrazíte miniaturu. Pomocí elementu `<a>` také můžete vytvořit hypertextový odkaz na velkou verzi obrázku. Stejně jako u atributu `src` `<img>` elementu, je automaticky nastaven atribut `href` prvku `<a>` dynamicky na cokoli, co je v `imagePath`. Chcete-li se ujistit, že cesta může fungovat jako adresa URL, předáte `imagePath` do metody `Html.AttributeEncode`, která převede rezervované znaky v cestě na znaky, které jsou v adrese URL v pořádku.
4. Spusťte stránku v prohlížeči.
5. Nahrajte fotografii a ověřte, jestli je zobrazená miniatura.
6. Kliknutím na miniaturu zobrazíte obrázek v plné velikosti.
7. V *obrazech* a *obrázcích/palec*si všimněte, že byly přidány nové soubory.

<a id="Rotating_and_Flipping"></a>
## <a name="rotating-and-flipping-an-image"></a>Otočení a překlopení obrázku

Pomocná rutina `WebImage` také umožňuje překlopit a otočit obrázky. Tento postup ukazuje, jak získat obrázek ze serveru, jak překlopit obrázek (svisle), uložit ho a pak zobrazit převrácenou image na stránce. V tomto příkladu jste právě používali soubor, který už máte na serveru (*Photo2. jpg*). V reálné aplikaci byste pravděpodobně přeměnili obrázek, jehož název se dynamicky načte, stejně jako v předchozích příkladech.

![obrazu](9-working-with-images/_static/image4.jpg "ch9images-4. jpg")

1. Přidejte novou stránku s názvem *FlipImage. cshtml*.
2. Stávající obsah stránky nahraďte následujícím způsobem: 

    [!code-cshtml[Main](9-working-with-images/samples/sample6.cshtml)]

    Kód používá pomocníka `WebImage` k získání obrázku ze serveru. Cestu k bitové kopii vytvoříte pomocí stejné techniky, jakou jste použili v předchozích příkladech pro ukládání imagí, a předáte tuto cestu při vytváření image pomocí `WebImage`:

    [!code-javascript[Main](9-working-with-images/samples/sample7.js)]

    Pokud se najde obrázek, vytvoří se nová cesta a název souboru, podobně jako v předchozích příkladech. Chcete-li překlopit obrázek, zavoláte metodu `FlipVertical` a pak obrázek znovu uložíte.

    Obrázek se znovu zobrazí na stránce pomocí elementu `<img>` s atributem `src` nastaveným na `imagePath`.
3. Spusťte stránku v prohlížeči. Zobrazuje se obrázek pro *Photo2. jpg* .
4. Aktualizujte stránku, nebo požádejte stránku znovu, aby se zobrazila znovu pravá strana.

Pro otočení obrázku použijte stejný kód s tím rozdílem, že místo volání `FlipVertical` nebo `FlipHorizontal`zavoláte `RotateLeft` nebo `RotateRight`.

<a id="Adding_a_Watermark"></a>
## <a name="adding-a-watermark-to-an-image"></a>Přidání vodoznaku do obrázku

Když na svůj web přidáte obrázky, možná budete chtít přidat vodoznak do obrázku před jeho uložením nebo zobrazením na stránce. Lidé často používají vodoznaky k přidání informací o autorských právech do obrázku nebo pro inzerci svého obchodního jména.

![obrazu](9-working-with-images/_static/image5.jpg "ch9images-5. jpg")

1. Přidejte novou stránku s názvem *vodotisk. cshtml*.
2. Stávající obsah stránky nahraďte následujícím způsobem: 

    [!code-cshtml[Main](9-working-with-images/samples/sample8.cshtml)]

    Tento kód je podobný kódu na stránce *FlipImage. cshtml* ze starší verze (Přestože tato doba používá soubor *Photo3. jpg* ). Chcete-li přidat meze, zavoláte metodu `AddTextWatermark` pomocné rutiny `WebImage` před uložením obrázku. V volání `AddTextWatermark`předáte text &quot;můj vodoznak&quot;, nastavíte barvu písma na žlutou a nastavíte rodinu písma na Arial. (I když zde není zobrazená, Pomocník pro `WebImage` také umožňuje určit krytí, rodinu písem a velikost písma a umístění textu meze.) Když uložíte obrázek, nesmí být jen pro čtení.

    Jak jste viděli dříve, obrázek se zobrazí na stránce pomocí elementu `<img>` s atributem src nastaveným na `@imagePath`.
3. Spusťte stránku v prohlížeči. V pravém dolním rohu obrázku si všimněte textu "můj vodoznak".

<a id="Using_an_Image_as_a_Watermark"></a>
## <a name="using-an-image-as-a-watermark"></a>Použití obrázku jako meze

Místo používání textu pro vodoznak můžete použít jiný obrázek. Lidé někdy používají jako vodoznak obrázky, jako je logo společnosti, nebo používají obrázek vodoznaku místo textu pro informace o autorských právech.

![obrazu](9-working-with-images/_static/image6.jpg "ch9images-6. jpg")

1. Přidejte novou stránku s názvem *ImageWatermark. cshtml*.
2. Přidejte obrázek do složky *images* , kterou můžete použít jako logo a přejmenovat image *MyCompanyLogo. jpg*. Tento obrázek by měl být obrázek, který se zobrazí jasně, když je nastaven na 80 pixelů a velký objem 20 pixelů.
3. Stávající obsah stránky nahraďte následujícím způsobem: 

    [!code-cshtml[Main](9-working-with-images/samples/sample9.cshtml)]

    Jedná se o další variaci kódu z předchozích příkladů. V tomto případě zavoláte `AddImageWatermark` pro přidání obrázku meze do cílové Image (*Photo3. jpg*) před uložením obrázku. Při volání `AddImageWatermark`nastavíte šířku na 80 pixelů a výšku na 20 pixelů. Obrázek *MyCompanyLogo. jpg* je vodorovně zarovnán do středu a svisle zarovnané v dolní části cílové image. Neprůhlednost je nastavena na 100% a odsazení je nastaveno na 10 pixelů. Pokud je obrázek meze větší než cílový obrázek, nic se nestane. Pokud je obrázek meze větší než cílový obrázek a nastavíte odsazení obrázku na hodnotu nula, vodoznak se ignoruje.

    Stejně jako předtím zobrazíte obrázek pomocí elementu `<img>` a dynamického atributu `src`.
4. Spusťte stránku v prohlížeči. Všimněte si, že obrázek vodoznaku se zobrazí v dolní části hlavní bitové kopie.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Další prostředky

[Práce se soubory na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202896)

[Úvod do programování webových stránek ASP.NET pomocí syntaxe Razor](https://go.microsoft.com/fwlink/?LinkID=251587)

---
uid: web-pages/overview/getting-started/introducing-razor-syntax-vb
title: Seznámení s ASP.NET webovým programováním pomocí syntaxe Razor (Visual Basic) | Microsoft Docs
author: Rick-Anderson
description: Tento dodatek vám poskytne přehled o programování s ASP.NET webovými stránkami v Visual Basic pomocí syntaxe Razor.
ms.author: riande
ms.date: 02/07/2014
ms.assetid: 5da59646-e973-41cd-88a9-c6b2c0594027
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-vb
msc.type: authoredcontent
ms.openlocfilehash: 2be57655b8c9b76b94e1d9a7ae5fbee27545a0a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526591"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a>Úvod do webového programování v ASP.NET pomocí syntaxe Razor (Visual Basic)

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek vám poskytne přehled o programování s ASP.NET webovými stránkami pomocí syntaxe Razor a Visual Basic. ASP.NET je technologie Microsoftu pro spouštění dynamických webových stránek na webových serverech.
> 
> **Co se naučíte**:
> 
> - Nejčastějších 8 programovacích tipů pro Začínáme s programováním webových stránek ASP.NET pomocí syntaxe Razor.
> - Základní koncepty programování, které budete potřebovat.
> - Jaký kód serveru ASP.NET a syntaxe Razor se týkají.
>   
> 
> ## <a name="software-versions"></a>Verze softwaru
> 
> 
> - Webové stránky ASP.NET (Razor) 3
>   
> 
> Tento kurz funguje také s ASP.NET webovými stránkami 2.

Většina příkladů použití webových stránek ASP.NET s využitím C#syntaxe Razor. Ale syntaxe Razor také podporuje Visual Basic. Chcete-li programovat webovou stránku ASP.NET v Visual Basic, vytvořte webovou stránku s příponou názvu souboru *. vbhtml* a pak přidejte Visual Basic kód. Tento článek vám poskytne přehled o práci s Visual Basicm jazykem a syntaxí pro vytváření webových stránek ASP.NET.

> [!NOTE]
> Výchozí šablony webu pro WebMatrix společnosti Microsoft (**pekařes**, **Fotogalerie a** **úvodní web**atd.) jsou k dispozici v C# a Visual Basic verzích. Šablony Visual Basic můžete nainstalovat jako balíčky NuGet. Šablony webu jsou nainstalovány v kořenové složce vaší lokality ve složce s názvem *šablony společnosti Microsoft*.

## <a name="the-top-8-programming-tips"></a>Prvních 8 tipů pro programování

Tato část obsahuje několik tipů, které bezpodmínečně potřebujete znát při psaní kódu ASP.NET serveru pomocí syntaxe Razor.

### <a name="1-you-add-code-to-a-page-using-the--character"></a>1. na stránku přidáte kód pomocí znaku @.

`@` znak spouští vložené výrazy, bloky s jedním příkazem a bloky s více příkazy:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

Výsledek zobrazený v prohlížeči:

![Razor-Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> **Kódování HTML**
> 
> Pokud zobrazíte obsah na stránce pomocí `@`ho znaku, jako v předchozích příkladech, ASP.NET kód HTML zakóduje výstup. Tím se nahradí vyhrazené znaky HTML (například `<` a `>` a `&`) kódy, které umožňují zobrazení znaků jako znaků na webové stránce namísto interpretace jako značek nebo entit jazyka HTML. Bez kódování HTML se výstup z kódu serveru nemusí zobrazit správně a může vystavit stránku pro rizika zabezpečení.
> 
> Pokud je vaším cílem výstup kódu HTML, který vykresluje značky jako kód (například `<p></p>` pro odstavec nebo `<em></em>` k zdůraznění textu), přečtěte si část [kombinování textu, značky a kódu v blocích kódu](#BM_CombiningTextMarkupAndCode) dále v tomto článku.
> 
> Další informace o kódování HTML najdete v tématu [práce s formuláři HTML v lokalitách webových stránek ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202892).

### <a name="2-you-enclose-code-blocks-with-codeend-code"></a>2. uzavíráte bloky kódu s kódem... Koncový kód

Blok kódu obsahuje jeden nebo více příkazů kódu a je uzavřen s klíčovými slovy `Code` a `End Code`. Ihned po znaku &#8212; `@` vložte klíčové slovo Open `Code`, mezi kterými nemůžete vložit mezeru.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

Výsledek zobrazený v prohlížeči:

![Razor-Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a>3. uvnitř bloku se každý příkaz kódu ukončí s koncem řádku.

V Visual Basic blok kódu, každý příkaz končí koncem řádku. (Později v článku uvidíte způsob, jak v případě potřeby zabalit příkaz dlouhého kódu do několika řádků.)

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a>4. proměnné použijete k uložení hodnot.

Hodnoty můžete ukládat do *proměnné*, včetně řetězců, čísel a dat atd. Novou proměnnou vytvoříte pomocí klíčového slova `Dim`. Hodnoty proměnných můžete vkládat přímo na stránce pomocí `@`.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

Výsledek zobrazený v prohlížeči:

![Razor-Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a>5. Uzavřete řetězcové hodnoty literálu do dvojitých uvozovek.

*Řetězec* je posloupnost znaků, které jsou považovány za text. Pokud chcete zadat řetězec, uzavřete ho do dvojitých uvozovek:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

Chcete-li vložit dvojité uvozovky v rámci řetězcové hodnoty, vložte dva znaky dvojité uvozovky. Pokud chcete, aby se znak dvojité uvozovky objevily jednou ve výstupu stránky, zadejte ho jako `""` v řetězci v uvozovkách a pokud chcete, aby se zobrazilo dvakrát, zadejte ho jako `""""` v řetězci v uvozovkách.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

Výsledek zobrazený v prohlížeči:

![Razor-Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a>6. Visual Basic kód nerozlišuje velká a malá písmena

Jazyk Visual Basic nerozlišuje velká a malá písmena. Klíčová slova pro programování (například `Dim`, `If`a `True`) a názvy proměnných (jako `myString`nebo `subTotal`) mohou být zapsány v každém případě.

Následující řádky kódu přiřadí hodnotu proměnné `lastname` s použitím malých písmen a pak mají výstup hodnoty proměnné na stránku pomocí velkého jména.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

Výsledek zobrazený v prohlížeči:

![vb-syntax-5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a>7. mnoho z vašich kódování zahrnuje práci s objekty

Objekt představuje věc, kterou můžete programovat se &#8212; stránkou, textovým polem, souborem, obrázkem, webovým požadavkem, e-mailovou zprávou, záznamem zákazníka (řádkem databáze) atd. Objekty mají vlastnosti, které popisují jejich &#8212; charakteristiky, objekt textového pole má vlastnost `Text`, objekt žádosti má vlastnost `Url`, e-mailová zpráva má vlastnost `From` a objekt Customer má vlastnost `FirstName`. Objekty mají také metody, které jsou &quot;slovesy&quot; mohou provádět. Mezi příklady patří `Save` metoda objektu souboru, metoda `Rotate` objektu obrázku a metoda `Send` objektu e-mailu.

Často budete pracovat s objektem `Request`, který vám poskytne informace, jako jsou hodnoty polí formuláře na stránce (textová pole atd.), jaký typ prohlížeče požadavek odeslal, adresu URL stránky, identitu uživatele atd. Tento příklad ukazuje, jak získat přístup k vlastnostem objektu `Request` a jak volat metodu `MapPath` objektu `Request`, který poskytuje absolutní cestu stránky na serveru:

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

Výsledek zobrazený v prohlížeči:

![Razor-Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a>8. můžete napsat kód, který provede rozhodnutí.

Klíčovou funkcí dynamických webových stránek je, že můžete určit, co dělat na základě podmínek. Nejběžnější způsob, jak to provést, je pomocí příkazu `If` (a volitelného příkazu `Else`).

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

Příkaz `If IsPost` je zkrácený způsob psaní `If IsPost = True`. Spolu s `If`mi příkazy existují různé způsoby, jak testovat podmínky, opakovat bloky kódu a tak dále, které jsou popsány dále v tomto článku.

Výsledek zobrazený v prohlížeči (po kliknutí na **Odeslat**):

![Razor-Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> **Metody GET a POST HTTP a vlastnost-post**
> 
> Protokol použitý pro webové stránky (HTTP) podporuje velmi omezený počet metod (&quot;&quot;ch operací), které se používají k provádění požadavků na server. Dva nejběžnější jsou GET, které slouží ke čtení stránky a k odeslání příspěvku, který slouží k odeslání stránky. Obecně platí, že uživatel poprvé požaduje stránku, stránka se požaduje pomocí GET. Pokud uživatel vyplní formulář a klikne na tlačítko **Odeslat**, prohlížeč ODEŠLE požadavek post na server.
> 
> Ve webovém programování je často užitečné zjistit, jestli se stránka požaduje jako GET nebo jako příspěvek, abyste věděli, jak stránku zpracovat. Na webových stránkách ASP.NET můžete pomocí vlastnosti `IsPost` zjistit, jestli je požadavek GET nebo POST. Pokud je žádost příspěvek, vlastnost `IsPost` vrátí hodnotu true a můžete provádět akce, jako je například čtení hodnot textových polí na formuláři. V mnoha příkladech se dozvíte, jak stránku zpracovat odlišně v závislosti na hodnotě `IsPost`.

## <a name="a-simple-code-example"></a>Příklad jednoduchého kódu

Tento postup ukazuje, jak vytvořit stránku, která znázorňuje základní programovací techniky. V tomto příkladu vytvoříte stránku, která umožní uživatelům zadat dvě čísla, pak je přidá a zobrazí výsledek.

1. V editoru vytvořte nový soubor a pojmenujte ho *AddNumbers. vbhtml*.
2. Zkopírujte následující kód a označení na stránku a nahraďte cokoli již na stránce.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    Tady je několik věcí, které můžete poznamenat:

    - `@` znak spustí první blok kódu na stránce a předá `totalMessage` proměnnou vloženou poblíž dolů.
    - Blok v horní části stránky je uzavřený v `Code...End Code`.
    - Proměnné `total`, `num1`, `num2`a `totalMessage` ukládají několik čísel a řetězce.
    - Literální řetězcová hodnota přiřazená k proměnné `totalMessage` je v dvojitých uvozovkách.
    - Vzhledem k tomu, že Visual Basic kód nerozlišuje velká a malá písmena, je-li proměnná `totalMessage` použita v dolní části stránky, musí její název odpovídat pouze pravopisu deklarace proměnné v horní části stránky. Záleží na velikosti písmen.
    - Výraz `num1.AsInt()` + `num2.AsInt()` ukazuje, jak pracovat s objekty a metodami. Metoda `AsInt` u každé proměnné převede řetězec zadaný uživatelem na celé číslo (celé číslo), které lze přidat.
    - Značka `<form>` obsahuje atribut `method="post"`. To určuje, že když uživatel klikne na **Přidat**, stránka se pošle na server pomocí metody HTTP POST. Po odeslání stránky se kód `If IsPost` vyhodnotí jako true a spustí se podmíněný kód a zobrazí se výsledek přidání čísel.
3. Uložte stránku a spusťte ji v prohlížeči. (Před spuštěním se ujistěte, že je stránka vybraná v pracovním prostoru **soubory** .) Zadejte dvě celá čísla a potom klikněte na tlačítko **Přidat** .

    ![Razor-Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a>Visual Basic jazyk a syntax

Dříve jste viděli základní příklad, jak vytvořit webovou stránku ASP.NET a jak můžete přidat serverový kód do kódu HTML. Tady se naučíte základy použití Visual Basic k zápisu kódu serveru ASP.NET pomocí syntaxe Razor &#8212; , která jsou pravidla pro programování jazyků.

Pokud máte zkušenosti s programováním (zejména pokud jste použili C, C++, C#, Visual Basic nebo JavaScript), je většina věcí, kterou si přečtete, dobře známá. Pravděpodobně budete potřebovat seznámení pouze s tím, jak je kód WebMatrix přidán do značek v souborech *. vbhtml* .

### <a id="BM_CombiningTextMarkupAndCode"></a>Kombinování textu, značek a kódu v blocích kódu

V blocích serverového kódu často budete chtít výstup textu a značky na stránku. Pokud blok kódu serveru obsahuje text, který není kód a místo toho by měl být vykreslen tak, jak je, ASP.NET musí být schopni tento text odlišit od kódu. To lze provést několika způsoby.

- Uzavřete text do elementu bloku HTML, jako je `<p></p>` nebo `<em></em>`:

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    Element HTML může obsahovat text, další prvky HTML a výrazy kódu serveru. Když ASP.NET uvidí otevření značky HTML (například `<p>`), vykreslí vše prvek a jeho obsah tak, jak je, do prohlížeče (a přeloží výrazy kódu serveru).

- Použijte operátor `@:` nebo prvek `<text>`. `@:` vytvoří výstup jednoho řádku obsahu obsahujícího prostý text nebo nespárované značky HTML. element `<text>` obklopuje více řádků do výstupu. Tyto možnosti jsou užitečné, pokud nechcete vykreslit prvek HTML jako součást výstupu.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    Následující příklad opakuje předchozí příklad, ale používá jednu dvojici `<text>` značek k uzavření textu, který se má vykreslit.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    V následujícím příkladu jsou značky `<text>` a `</text>` uzavřeny tři řádky, všechny, které obsahují neuzavřený text a nespárované značky HTML (`<br />`), spolu s kódem serveru a odpovídajícími značkami HTML. Znovu můžete také předcházet každý řádek jednotlivě pomocí operátoru `@:`; Jak funguje.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > Při výstupu textu, jak je znázorněno v &#8212; této části pomocí elementu jazyka HTML, operátoru `@:` nebo elementu &#8212; `<text>` ASP.NET nekóduje výstup do kódu HTML. (Jak bylo uvedeno dříve, ASP.NET zakóduje výstup výrazů serverového kódu a bloků serverového kódu, které jsou před `@`, s výjimkou zvláštních případů uvedených v této části.)

### <a name="whitespace"></a>Typy

Nadbytečné mezery v příkazu (a mimo řetězcový literál) neovlivňují příkaz:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a>Rozdělení dlouhých příkazů na více řádků

Příkaz dlouhého kódu můžete rozdělit na více řádků pomocí znaku podtržítka `_` (který se v Visual Basic označuje jako *znak pokračování*) po každém řádku kódu. Chcete-li rozdělit příkaz na další řádek, na konci řádku přidejte mezeru a pak znak pokračování. Pokračujte v prohlášení na dalším řádku. Příkazy lze zabalit do tolika řádků, kolik potřebujete ke zlepšení čitelnosti. Následující příkazy jsou stejné:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

Nemůžete však obtékat čáru uprostřed řetězcového literálu. Následující příklad nefunguje:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

Pro kombinování dlouhého řetězce, který se zalomí na více řádků, jako je výše uvedený kód, byste museli použít *operátor zřetězení* (`&`), který se zobrazí později v tomto článku.

### <a name="code-comments"></a>Komentáře ke kódu

Komentáře umožňují psát si poznámky pro sebe nebo jiné. Komentáře syntaxe Razor jsou s předponou `@*` a končí `*@`.

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

V rámci bloků kódu můžete použít komentáře syntaxe Razor, nebo můžete použít obyčejného znaku Visual Basic komentáře, což je jedna uvozovka (`'`) s předponou na každý řádek.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a>Proměnné

Proměnná je pojmenovaný objekt, který slouží k ukládání dat. Proměnné můžete pojmenovat cokoli, ale název musí začínat znakem abecedy a nesmí obsahovat mezery ani vyhrazené znaky. V Visual Basic, jak jste viděli dříve, Velká a malá písmena v názvu proměnné nezáleží na velikosti písmen.

### <a name="variables-and-data-types"></a>Proměnné a datové typy

Proměnná může mít určitý datový typ, který označuje, jaký druh dat je uložený v proměnné. Můžete mít řetězcové proměnné, které ukládají řetězcové hodnoty (například &quot;Hello World&quot;), celočíselné proměnné, které ukládají hodnoty s celými čísly (například 3 nebo 79), a proměnné data uchovávající hodnoty data v různých formátech (například 4/12/2012 nebo březen 2009). A existuje mnoho dalších typů dat, které můžete použít.

Nemusíte ale zadávat typ pro proměnnou. Ve většině případů ASP.NET může zjistit typ podle toho, jak se data v proměnné používají. (Někdy musíte zadat typ; uvidíte příklady, kde je to pravda.)

Chcete-li deklarovat proměnnou bez určení typu, použijte `Dim` plus název proměnné (např. `Dim myVar`). Chcete-li deklarovat proměnnou s typem, použijte `Dim` plus název proměnné následovaný `As` a pak název typu (například `Dim myVar As String`).

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

Následující příklad ukazuje některé vložené výrazy, které používají proměnné na webové stránce.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

Výsledek zobrazený v prohlížeči:

![Razor-Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a>Převod a testování datových typů

I když ASP.NET může obvykle určit datový typ automaticky, někdy to nemůže. Proto může být nutné pomáhat s ASP.NETm při provádění explicitního převodu. I v případě, že není nutné převést typy, někdy je vhodné otestovat a zjistit, se kterými typem dat pracujete.

Nejběžnějším případem je, že je nutné převést řetězec na jiný typ, jako je například na celé číslo nebo datum. Následující příklad ukazuje typický případ, kdy je nutné převést řetězec na číslo.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

Jako pravidlo se vstup uživatele dostane jako řetězce. I když se uživateli zobrazí výzva k zadání čísla, a to i v případě, že zadali číslici, když se odešle vstup uživatele a přečtete ho v kódu, data jsou ve formátu řetězce. Proto je nutné převést řetězec na číslo. Pokud se v příkladu pokusíte provést aritmetické operace s hodnotami bez jejich převádění, dojde k následující chybě, protože ASP.NET nemůže přidat dva řetězce:

`Cannot implicitly convert type 'string' to 'int'.`

Chcete-li převést hodnoty na celá čísla, zavolejte metodu `AsInt`. Pokud je převod úspěšný, můžete čísla přidat.

V následující tabulce jsou uvedeny některé běžné metody převodu a testování pro proměnné.

:::row:::
    :::column:::
        <strong>Metoda</strong>
    :::column-end:::
    :::column:::
        <strong>Popis</strong>
    :::column-end:::
    :::column:::
        <strong>Příklad</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
        Převede řetězec reprezentující celé číslo (například &quot;593&quot;) na celé číslo.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample23.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsBool(), IsBool()`
    :::column-end:::
    :::column:::
        Převede řetězec jako &quot;true&quot; nebo &quot;false&quot; na typ Boolean.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample24.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsFloat(), IsFloat()`
    :::column-end:::
    :::column:::
        Převede řetězec, který má hodnotu typu Decimal, například &quot;1,3&quot; nebo &quot;7,439&quot; na číslo s plovoucí desetinnou čárkou.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample25.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDecimal(), IsDecimal()`
    :::column-end:::
    :::column:::
        Převede řetězec, který má hodnotu typu Decimal, například &quot;1,3&quot; nebo &quot;7,439&quot; na desetinné číslo. (V ASP.NET je desetinné číslo přesnější než číslo s plovoucí desetinnou čárkou.)
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample26.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsDateTime(), IsDateTime()`
    :::column-end:::
    :::column:::
        Převede řetězec, který představuje hodnotu data a času na ASP.NET typ `DateTime`.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample27.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `ToString()`
    :::column-end:::
    :::column:::
        Převede jakýkoli jiný datový typ na řetězec.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a>Operátory

Operátor je klíčové slovo nebo znak, který oznamuje ASP.NET, jaký druh příkazu má být proveden ve výrazu. Visual Basic podporuje mnoho operátorů, ale k zahájení vývoje webových stránek ASP.NET potřebujete jenom několik málo. Následující tabulka shrnuje nejběžnější operátory.

:::row:::
    :::column:::
        <strong>Podnikatel</strong>
    :::column-end:::
    :::column:::
        <strong>Popis</strong>
    :::column-end:::
    :::column:::
        <strong>Příklady</strong>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+ - * /`
    :::column-end:::
    :::column:::
        Matematické operátory používané v numerických výrazech.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample29.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
        Přiřazení a rovnost. V závislosti na kontextu přiřadí hodnotu na pravé straně příkazu objektu na levé straně nebo ověří hodnoty rovnosti.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample30.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `<>`
    :::column-end:::
    :::column:::
        Nerovnost. Vrátí `True`, pokud se hodnoty neshodují.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample31.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
        Menší než, větší než, menší nebo rovno, a větší nebo rovno.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample32.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&`
    :::column-end:::
    :::column:::
        Zřetězení, které se používá k spojování řetězců.
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample33.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+= -=`
    :::column-end:::
    :::column:::
        Operátory přírůstku a snížení, které přidají a odečtou 1 (v uvedeném pořadí) z proměnné.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample34.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `.`
    :::column-end:::
    :::column:::
        Tečka. Slouží k rozlišení objektů a jejich vlastností a metod.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample35.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
        Závorky. Slouží k seskupení výrazů, k předání parametrů metodám a k přístupu ke členům polí a kolekcí.
    :::column-end:::
    :::column:::
        [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample36.vbhtml)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `Not`
    :::column-end:::
    :::column:::
        Mění. Obrátí hodnotu true na false a naopak. Obvykle se používá jako zkrácený způsob testování pro `False` (tj. není-li `True`).
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample37.vb)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AndAlso OrElse`
    :::column-end:::
    :::column:::
        Logický operátor AND a OR, který se používá k propojení podmínek.
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]
    :::column-end:::
:::row-end:::

## <a name="working-with-file-and-folder-paths-in-code"></a>Práce s cestami k souborům a složkám v kódu

V kódu často budete pracovat s cestami k souborům a složkám. Tady je příklad fyzické struktury složek pro web, jak se může zobrazit na vašem vývojovém počítači:

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

Tady jsou některé důležité informace o adresách URL a cestách:

- Adresa URL začíná buď s názvem domény (`http://www.example.com`), nebo s názvem serveru (`http://localhost`, `http://mycomputer`).
- Adresa URL odpovídá fyzické cestě na hostitelském počítači. `http://myserver` například může odpovídat složce *C:\websites\mywebsite* na serveru.
- Virtuální cesta je zkrácený pro reprezentaci cest v kódu bez nutnosti zadat úplnou cestu. Obsahuje část adresy URL, která následuje za názvem domény nebo serveru. Pokud používáte virtuální cesty, můžete svůj kód přesunout do jiné domény nebo serveru, aniž byste museli cesty aktualizovat.

Tady je příklad, který vám pomůže pochopit rozdíly:

| Úplná adresa URL | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| Název serveru | *mycompanyserver* |
| Virtuální cesta | */humanresources/CompanyPolicy.htm* |
| Fyzická cesta | *C:\mywebsites\humanresources\CompanyPolicy.htm* |

Virtuální kořenový adresář je/, stejně jako kořenový adresář vaší jednotky C:. (Cesty k virtuálním složkám vždycky používají lomítka.) Virtuální cesta ke složce nemusí mít stejný název jako fyzická složka; může to být alias. (Na provozních serverech se virtuální cesta zřídka shoduje s přesnou fyzickou cestou.)

Když pracujete se soubory a složkami v kódu, někdy potřebujete odkazovat na fyzickou cestu a někdy na virtuální cestu v závislosti na objektech, se kterými pracujete. ASP.NET poskytuje tyto nástroje pro práci s cestami k souborům a složkám v kódu: metoda `Server.MapPath` a operátor `~` a metoda `Href`.

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a>Převod virtuálních na fyzické cesty: Metoda Server. MapPath

Metoda `Server.MapPath` Převede virtuální cestu (například */Default.cshtml*) na absolutní fyzickou cestu (například *C:\WebSites\MyWebSiteFolder\default.cshtml*). Tuto metodu použijete kdykoli, když potřebujete úplnou fyzickou cestu. Typickým příkladem je, že načítáte nebo píšete textový soubor nebo soubor obrázku na webovém serveru.

Obvykle neznáte absolutní fyzickou cestu k webu na serveru hostujícího webu, takže tato metoda může převést cestu, kterou znáte – virtuální cestu – k odpovídající cestě na serveru za vás. Do metody předáte virtuální cestu k souboru nebo složce a vrátíte fyzickou cestu:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a>Odkazování na virtuální kořenový adresář: operátor ~ a metoda href

V souboru *. cshtml* nebo *. vbhtml* můžete odkazovat na virtuální kořenovou cestu pomocí operátoru `~`. To je velmi užitečné, protože můžete přesouvat stránky v lokalitě a jakékoli odkazy, které obsahují na jiné stránky, nebudou přerušeny. K dispozici je také užitečné v případě, že jste web někdy přesunuli do jiného umístění. Zde je několik příkladů:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

Pokud je web `http://myserver/myapp`, v takovém případě bude ASP.NET považovat tyto cesty při spuštění stránky:

- `myImagesFolder`: `http://myserver/myapp/images`
- `myStyleSheet`: `http://myserver/myapp/styles/Stylesheet.css`

(Tyto cesty ve skutečnosti neuvidíte jako hodnoty proměnné, ale ASP.NET je bude považovat za to, co byly.)

Operátor `~` lze použít jak v kódu serveru (jak je uvedeno výše), tak v označení, například takto:

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

V kódu se používá operátor `~` k vytváření cest k prostředkům, jako jsou soubory obrázků, jiné webové stránky a soubory CSS. Po spuštění stránky ASP.NET vyhledá stránku (kód i kód) a přeloží všechny `~` odkazy na příslušnou cestu.

## <a name="conditional-logic-and-loops"></a>Podmíněná logika a smyčky

Kód serveru ASP.NET vám umožňuje provádět úlohy na základě podmínek a napsat kód, který opakuje příkazy, a to tak, že se kód spouštějí smyčkou, a to podle určitého počtu.

### <a name="testing-conditions"></a>Podmínky testování

Chcete-li otestovat jednoduchou podmínku, použijte příkaz `If...Then`, který vrací `True` nebo `False` na základě testu, který zadáte:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

Klíčové slovo `If` spustí blok. Skutečný test (podmínka) následuje za klíčovým slovem `If` a vrátí hodnotu true nebo false. Příkaz `If` končí na `Then`. Příkazy, které se spustí, pokud je test pravdivý, je uzavřený `If` a `End If`. Příkaz `If` může zahrnovat blok `Else`, který určuje příkazy, které se mají spustit, pokud je podmínka nepravdivá:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

Pokud příkaz `If` spustí blok kódu, nemusíte používat normální příkazy `Code...End Code` k zahrnutí bloků. Do bloku můžete přidat pouze `@` a bude fungovat. Tento přístup funguje s `If` a dalšími Visual Basic programovací klíčová slova, která následují bloky kódu, včetně `For`, `For Each`, `Do While`atd.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

Pomocí jednoho nebo více `ElseIf`ch bloků můžete přidat více podmínek:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

V tomto příkladu, pokud není první podmínka v `If`ovém bloku pravdivá, je zaškrtnuta podmínka `ElseIf`. Pokud je tato podmínka splněna, jsou provedeny příkazy v bloku `ElseIf`. Pokud není splněna žádná z podmínek, jsou provedeny příkazy v bloku `Else`. Můžete přidat libovolný počet bloků `ElseIf` a potom zavřít s `Else` bloku jako &quot;vše ostatní&quot; podmínka.

K otestování velkého počtu podmínek použijte `Select Case` blok:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

Testovaná hodnota je v závorkách (v příkladu proměnné weekday). Každý jednotlivý test používá příkaz `Case`, který obsahuje hodnotu. Je-li hodnota příkazu `Case` shodná s testovací hodnotou, je proveden kód v tomto bloku `Case`.

Výsledek posledního dvou podmíněných bloků zobrazených v prohlížeči:

![Razor – Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a>Kód smyčky

Často je třeba spouštět stejné příkazy opakovaně. Provedete to pomocí smyčky. Například často spustíte stejné příkazy pro každou položku v kolekci dat. Pokud víte přesně, kolikrát chcete cyklovat, můžete použít smyčku `For`. Tento druh smyčky je zvláště užitečný pro inventarizaci a počítání:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

Smyčka začíná klíčovým slovem `For` následovanými třemi prvky:

- Ihned po příkazu `For` deklarujete proměnnou čítače (nemusíte používat `Dim`) a pak určíte rozsah, jako v `i = 10 to 20`. To znamená, že proměnná `i` začne počítat 10 a pokračovat, dokud nedosáhne 20 (včetně).
- Mezi příkazy `For` a `Next` je obsah bloku. To může obsahovat jeden nebo více příkazů kódu, které se spouštějí s každou smyčkou.
- Příkaz `Next i` ukončí smyčku. Zvýší hodnotu čítače a spustí další iteraci smyčky.

Řádek kódu mezi `For` a `Next` řádky obsahuje kód, který se spustí pro každou iteraci smyčky. Kód vytvoří nový odstavec (`<p>` element) pokaždé a přidá řádek do výstupu a zobrazí hodnotu i (čítač). Když spustíte tuto stránku, v příkladu se vytvoří 11 řádků, ve kterých se zobrazí výstup, a text na každém řádku, který označuje číslo položky.

![Razor-Img11](introducing-razor-syntax-vb/_static/image11.jpg)

Pokud pracujete s kolekcí nebo polem, často používáte smyčku `For Each`. Kolekce je skupina podobných objektů a smyčka `For Each` umožňuje provádět úlohy na každé položce v kolekci. Tento typ smyčky je vhodný pro kolekce, protože na rozdíl od `For` smyčky nemusíte zvyšovat čítač nebo nastavit limit. Místo toho kód smyčky `For Each` jednoduše projde přes kolekci, dokud není dokončena.

Tento příklad vrátí položky v kolekci `Request.ServerVariables` (které obsahují informace o vašem webovém serveru). Používá smyčku `For Each` k zobrazení názvu každé položky vytvořením nového prvku `<li>` v seznamu s odrážkami HTML.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

Za klíčovým slovem `For Each` následuje proměnná, která představuje jednu položku v kolekci (v příkladu `myItem`) následovanou klíčovým slovem `In` následovaný kolekcí, kterou chcete procyklovat. V těle `For Each` smyčky můžete k aktuální položce přistupovat pomocí proměnné, kterou jste předtím deklarovali.

![Razor-Img12](introducing-razor-syntax-vb/_static/image12.jpg)

Chcete-li vytvořit obecnější smyčku pro účely, použijte příkaz `Do While`:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

Tato smyčka začíná klíčovým slovem `Do While` následovaným podmínkou, následovanou blokem, který se má opakovat. Smyčky typicky přidávají (přidávají do) nebo snižují (odečtou z) proměnnou nebo objekt, který se používá pro počítání. V příkladu operátor `+=` přidá 1 k hodnotě proměnné pokaždé, když se smyčka spustí. (Chcete-li snížit proměnnou ve smyčce, která počítá dolů, použijte operátor snížení `-=`.)

## <a name="objects-and-collections"></a>Objekty a kolekce

Skoro všechno na webu ASP.NET je objekt, včetně samotné webové stránky. Tato část popisuje některé důležité objekty, se kterými se často pracujete ve vašem kódu.

### <a name="page-objects"></a>Objekty stránky

Nejzákladnější objekt v ASP.NET je stránka. K vlastnostem objektu stránky můžete přistupovat přímo bez jakéhokoli opravňujícího objektu. Následující kód Získá cestu k souboru stránky pomocí objektu `Request` stránky:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

Pomocí vlastností objektu `Page` můžete získat velké množství informací, například:

- `Request`. Jak už jste viděli, jedná se o kolekci informací o aktuální žádosti, včetně typu prohlížeče, který požadavek odeslal, adresu URL stránky, identitu uživatele atd.
- `Response`. Toto je kolekce informací o odpovědi (stránky), která se odešle do prohlížeče, když je kód serveru spuštěný. Tuto vlastnost můžete například použít k zápisu informací do odpovědi.

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a>Objekty kolekce (pole a slovníky)

Kolekce je skupina objektů stejného typu, například kolekce `Customer` objektů z databáze. ASP.NET obsahuje mnoho předdefinovaných kolekcí, jako je kolekce `Request.Files`.

Často budete pracovat s daty v kolekcích. Dva společné typy kolekcí jsou *pole* a *slovník*. Pole je užitečné, pokud chcete uložit kolekci podobných položek, ale nechcete vytvořit samostatnou proměnnou pro uchování každé položky:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

Pomocí polí deklarujete konkrétní datový typ, například `String`, `Integer`nebo `DateTime`. Chcete-li označit, že proměnná může obsahovat pole, přidejte do názvu proměnné v deklaraci (například `Dim myVar() As String`) závorky. K položkám v poli můžete přistupovat pomocí jejich pozice (indexu) nebo pomocí příkazu `For Each`. Indexy polí jsou počítány od &#8212; nuly, tj. první položka je na pozici 0, druhá položka je na pozici 1 atd.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

Počet položek v poli můžete určit získáním jeho vlastnosti `Length`. Chcete-li získat pozici konkrétní položky v poli (tj. pro hledání v poli), použijte metodu `Array.IndexOf`. Můžete také provést akce, jako je vrácení obsahu pole (`Array.Reverse` metody) nebo řazení obsahu (metoda `Array.Sort`).

Výstup kódu řetězcového pole zobrazeného v prohlížeči:

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

Slovník je kolekce párů klíč/hodnota, kde zadáte klíč (nebo název) pro nastavení nebo načtení příslušné hodnoty:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

Chcete-li vytvořit slovník, použijte klíčové slovo `New` pro indikaci, že vytváříte nový objekt `Dictionary`. K proměnné můžete přiřadit slovník pomocí klíčového slova `Dim`. Datové typy položek ve slovníku označíte pomocí závorek (`( )`). Na konci deklarace je nutné přidat další dvojici závorek, protože se jedná o metodu, která vytvoří nový slovník.

Chcete-li přidat položky do slovníku, můžete zavolat metodu `Add` proměnné Dictionary (`myScores` v tomto případě) a poté zadat klíč a hodnotu. Alternativně můžete pomocí závorek označit klíč a provést jednoduché přiřazení, jako v následujícím příkladu:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

Pokud chcete získat hodnotu ze slovníku, zadáte klíč v závorkách:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a>Volání metod s parametry

Jak jste viděli výše v tomto článku, objekty, které program mají, mají metody. Například `Database` objekt může mít metodu `Database.Connect`. Mnoho metod má také jeden nebo více parametrů. *Parametr* je hodnota, kterou předáte metodě, aby mohla metoda dokončit její úlohu. Podívejte se například na deklaraci metody `Request.MapPath`, která přijímá tři parametry:

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

Tato metoda vrátí fyzickou cestu na serveru, který odpovídá zadané virtuální cestě. Tři parametry pro metodu jsou `virtualPath`, `baseVirtualDir`a `allowCrossAppMapping`. (Všimněte si, že v deklaraci jsou parametry uvedeny s datovými typy dat, která budou přijímat.) Při volání této metody je nutné dodat hodnoty pro všechny tři parametry.

Pokud používáte Visual Basic s syntaxe Razor, máte dvě možnosti pro předávání parametrů metodě: *poziční parametry* nebo *pojmenované parametry*. Chcete-li volat metodu pomocí pozičních parametrů, předáte parametry v přesném pořadí, které je zadáno v deklaraci metody. (Toto pořadí byste obvykle znali v dokumentaci k metodě.) Je nutné postupovat podle pořadí a v případě potřeby nemůžete přeskočit &#8212; žádný z parametrů, předáte prázdný řetězec (`""`) nebo hodnotu null pro poziční parametr, pro který nemáte hodnotu.

Následující příklad předpokládá, že máte ve svém webu složku s názvem *skripty* . Kód volá metodu `Request.MapPath` a předá hodnoty pro tři parametry ve správném pořadí. Pak zobrazí výslednou mapovanou cestu.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

Pokud existuje mnoho parametrů pro metodu, můžete zachovat čisticí kód a čitelnější pomocí pojmenovaných parametrů. Chcete-li volat metodu pomocí pojmenovaných parametrů, zadejte název parametru následovaný `:=` a potom zadejte hodnotu. Výhodou pojmenovaných parametrů je, že je můžete přidat v libovolném požadovaném pořadí. (Nevýhodou je, že volání metody není jako kompaktní.)

Následující příklad volá stejnou metodu jako výše, ale používá pojmenované parametry k poskytnutí těchto hodnot:

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

Jak vidíte, parametry jsou předány v jiném pořadí. Pokud však spustíte předchozí příklad a tento příklad vrátí stejnou hodnotu.

## <a name="handling-errors"></a>Zpracování chyb

### <a name="try-catch-statements"></a>Příkazy try-catch

Často budete mít ve svém kódu příkazy, které mohou selhat z důvodů mimo váš ovládací prvek. Příklad:

- Pokud se váš kód pokusí otevřít, vytvořit, číst nebo zapsat soubor, může dojít k nejrůznějším chybám. Soubor, který chcete, možná neexistuje, může být uzamčen, kód pravděpodobně nemá oprávnění atd.
- Podobně platí, že pokud se váš kód pokusí aktualizovat záznamy v databázi, může dojít k problémům s oprávněními, připojení k databázi může být vyřazeno, data, která mají být uložena, mohou být neplatná atd.

V programovacích podmínkách se tyto situace nazývají *výjimky*. Pokud váš kód narazí na výjimku, vygeneruje (vyvolá) chybovou zprávu, která je nejlepší pro uživatele.

![Razor-Img14](introducing-razor-syntax-vb/_static/image14.jpg)

V situacích, kdy se váš kód může setkat s výjimkami, a aby se předešlo chybovým zprávám tohoto typu, můžete použít příkazy `Try/Catch`. V příkazu `Try` spustíte kód, který kontrolujete. V jednom nebo více příkazech `Catch` můžete vyhledat konkrétní chyby (konkrétní typy výjimek), ke kterým mohlo dojít. Můžete zahrnout tolik příkazů `Catch`, kolik potřebujete pro hledání chyb, které očekáváte.

> [!NOTE]
> Doporučujeme, abyste se vyhnuli použití metody `Response.Redirect` v příkazech `Try/Catch`, protože to může způsobit výjimku na stránce.

Následující příklad ukazuje stránku, která vytvoří textový soubor pro první požadavek a pak zobrazí tlačítko, které uživateli otevře soubor. Příklad záměrně používá špatný název souboru, takže bude způsobovat výjimku. Kód zahrnuje `Catch` příkazy pro dvě možné výjimky: `FileNotFoundException`, ke kterým dojde, pokud je název souboru špatný a `DirectoryNotFoundException`, ke kterému dochází, pokud ASP.NET nemůže dokonce najít složku. (Můžete zrušit komentář k příkazu v příkladu, abyste viděli, jak se spustí, když vše funguje správně.)

Pokud váš kód nezpracovává výjimku, zobrazila se chybová stránka, například snímek předchozí obrazovky. Nicméně část `Try/Catch` pomáhá zabránit uživateli v zobrazování těchto typů chyb.

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a>Další prostředky

### <a name="reference-documentation"></a>Referenční dokumentace

- [ASP.NET](https://msdn.microsoft.com/library/ee532866.aspx)
- [Visual Basic jazyk](https://msdn.microsoft.com/library/2x7h1hfk.aspx)

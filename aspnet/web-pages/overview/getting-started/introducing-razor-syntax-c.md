---
uid: web-pages/overview/getting-started/introducing-razor-syntax-c
title: Seznámení s ASP.NET webovým programováním pomocíC#syntaxe Razor () | Microsoft Docs
author: Rick-Anderson
description: Tato kapitola vám poskytne přehled o programování s ASP.NET webovými stránkami pomocí syntaxe Razor. ASP.NET je technologie Microsoftu pro spouštění dynamického webového PA...
ms.author: riande
ms.date: 02/07/2014
ms.assetid: aa67d304-583b-4bf8-a231-195656cfb587
msc.legacyurl: /web-pages/overview/getting-started/introducing-razor-syntax-c
msc.type: authoredcontent
ms.openlocfilehash: c2f420bb7c2f7d2e31654c20fb9ec7497a30a9f7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641573"
---
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a>Úvod do webového programování v ASP.NET pomocí syntaxe Razor (C#)

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek vám poskytne přehled o programování s ASP.NET webovými stránkami pomocí syntaxe Razor. ASP.NET je technologie Microsoftu pro spouštění dynamických webových stránek na webových serverech. Tento článek se C# zaměřuje na používání programovacího jazyka.
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

## <a name="the-top-8-programming-tips"></a>Prvních 8 tipů pro programování

Tato část obsahuje několik tipů, které bezpodmínečně potřebujete znát při psaní kódu ASP.NET serveru pomocí syntaxe Razor.

> [!NOTE]
> Syntaxe Razor vychází z C# programovacího jazyka a je to jazyk, který se nejčastěji používá s ASP.NET webovými stránkami. Syntaxe Razor ale taky podporuje Visual Basic jazyk a všechno, co vidíte, můžete také udělat v Visual Basic. Podrobnosti najdete v dodatku [Visual Basic jazyk a syntaxi](https://go.microsoft.com/fwlink/?LinkId=202908).

Další informace o většině těchto programovacích postupů najdete dále v článku.

### <a name="1-you-add-code-to-a-page-using-the--character"></a>1. na stránku přidáte kód pomocí znaku @.

Znak `@` spouští vložené výrazy, bloky s jedním příkazem a bloky s více příkazy:

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

Tyto příkazy vypadají jako při spuštění stránky v prohlížeči:

![Razor-Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> **Kódování HTML**
> 
> Pokud zobrazíte obsah na stránce pomocí `@`ho znaku, jako v předchozích příkladech, ASP.NET kód HTML zakóduje výstup. Tím se nahradí vyhrazené znaky HTML (například `<` a `>` a `&`) kódy, které umožňují zobrazení znaků jako znaků na webové stránce namísto interpretace jako značek nebo entit jazyka HTML. Bez kódování HTML se výstup z kódu serveru nemusí zobrazit správně a může vystavit stránku pro rizika zabezpečení.
> 
> Pokud je vaším cílem výstup kódu HTML, který vykresluje značky jako kód (například `<p></p>` pro odstavec nebo `<em></em>` k zdůraznění textu), přečtěte si část [kombinování textu, značky a kódu v blocích kódu](#BM_CombiningTextMarkupAndCode) dále v tomto článku.
> 
> Můžete si přečíst další informace o kódování HTML při [práci s formuláři](https://go.microsoft.com/fwlink/?LinkId=202892).

### <a name="2-you-enclose-code-blocks-in-braces"></a>2. můžete bloky kódu uzavřít do složených závorek.

*Blok kódu* obsahuje jeden nebo více příkazů kódu a je uzavřen ve složených závorkách.

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

Výsledek zobrazený v prohlížeči:

![Razor-Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a>3. uvnitř bloku se každý příkaz kódu ukončí středníkem.

Uvnitř bloku kódu musí každý úplný příkaz kódu končit středníkem. Vložené výrazy nekončí středníkem.

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a>4. proměnné použijete k uložení hodnot.

Hodnoty můžete ukládat do *proměnné*, včetně řetězců, čísel a dat atd. Novou proměnnou vytvoříte pomocí klíčového slova `var`. Hodnoty proměnných můžete vkládat přímo na stránce pomocí `@`.

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

Výsledek zobrazený v prohlížeči:

![Razor-Img3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a>5. Uzavřete řetězcové hodnoty literálu do dvojitých uvozovek.

*Řetězec* je posloupnost znaků, které jsou považovány za text. Pokud chcete zadat řetězec, uzavřete ho do dvojitých uvozovek:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

Pokud řetězec, který chcete zobrazit, obsahuje znak zpětného lomítka (`\`) nebo dvojité uvozovky (`"`), použijte *doslovné řetězcový literál* , který je předponou operátoru `@`. (V C#, znak \ má zvláštní význam, pokud nepoužijete doslovné řetězcový literál.)

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

Chcete-li vložit dvojité uvozovky, použijte doslovné řetězcový literál a uvozovky opakujte:

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

Tady je výsledek použití obou z těchto příkladů na stránce:

![Razor-Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> Všimněte si, že znak `@` slouží k označení doslovnéch řetězcových literálů C# v a k označení kódu na stránkách ASP.NET.

### <a name="6-code-is-case-sensitive"></a>6. kód rozlišuje velká a malá písmena.

V C#, klíčová slova (například `var`, `true`a `if`) a názvy proměnných rozlišují malá a velká písmena. Následující řádky kódu vytvoří dvě různé proměnné `lastName` a `LastName.`

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

Pokud deklarujete proměnnou jako `var lastName = "Smith";` a pokusíte se na ni odkazovat na tuto proměnnou jako `@LastName`, místo `"Smith"`se zobrazí hodnota `"Jones"`.

> [!NOTE]
> V Visual Basic klíčová slova a proměnné *nerozlišují velká a malá písmena.*

### <a name="7-much-of-your-coding-involves-objects"></a>7. mnoho z vašich kódování zahrnuje objekty

*Objekt* představuje věc, kterou můžete programovat se &#8212; stránkou, textovým polem, souborem, obrázkem, webovým požadavkem, e-mailovou zprávou, záznamem zákazníka (řádkem databáze) atd. Objekty mají vlastnosti, které popisují jejich charakteristiky a které můžete číst nebo měnit &#8212; objekt textového pole, má vlastnost `Text` (mimo jiné), objekt požadavku má vlastnost `Url`, e-mailová zpráva má vlastnost `From` a objekt Customer má vlastnost `FirstName`. Objekty mají také metody, které jsou &quot;slovesy&quot; mohou provádět. Mezi příklady patří `Save` metoda objektu souboru, metoda `Rotate` objektu obrázku a metoda `Send` objektu e-mailu.

Často budete pracovat s objektem `Request`, který vám poskytne informace, jako jsou hodnoty textových polí (pole formuláře) na stránce, jaký typ prohlížeče odeslal požadavek, adresu URL stránky, identitu uživatele atd. Následující příklad ukazuje, jak získat přístup k vlastnostem objektu `Request` a jak zavolat metodu `MapPath` objektu `Request`, který poskytuje absolutní cestu stránky na serveru:

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

Výsledek zobrazený v prohlížeči:

![Razor-Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a>8. můžete napsat kód, který provede rozhodnutí.

Klíčovou funkcí dynamických webových stránek je, že můžete určit, co dělat na základě podmínek. Nejběžnější způsob, jak to provést, je pomocí příkazu `if` (a volitelného příkazu `else`).

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

Příkaz `if(IsPost)` je zkrácený způsob psaní `if(IsPost == true)`. Spolu s `if`mi příkazy existují různé způsoby, jak testovat podmínky, opakovat bloky kódu a tak dále, které jsou popsány dále v tomto článku.

Výsledek zobrazený v prohlížeči (po kliknutí na **Odeslat**):

![Razor-Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a>Metody GET a POST HTTP a vlastnost-post
> 
> Protokol použitý pro webové stránky (HTTP) podporuje velmi omezený počet metod (operací), které se používají k provádění požadavků na server. Dva nejběžnější jsou GET, které slouží ke čtení stránky a k odeslání příspěvku, který slouží k odeslání stránky. Obecně platí, že uživatel poprvé požaduje stránku, stránka se požaduje pomocí GET. Pokud uživatel vyplní formulář a klikne na tlačítko Odeslat, prohlížeč odešle požadavek POST na server.
> 
> Ve webovém programování je často užitečné zjistit, jestli se stránka požaduje jako GET nebo jako příspěvek, abyste věděli, jak stránku zpracovat. Na webových stránkách ASP.NET můžete pomocí vlastnosti `IsPost` zjistit, jestli je požadavek GET nebo POST. Pokud je žádost příspěvek, vlastnost `IsPost` vrátí hodnotu true a můžete provádět akce, jako je například čtení hodnot textových polí na formuláři. V mnoha příkladech se dozvíte, jak stránku zpracovat odlišně v závislosti na hodnotě `IsPost`.

## <a name="a-simple-code-example"></a>Příklad jednoduchého kódu

Tento postup ukazuje, jak vytvořit stránku, která znázorňuje základní programovací techniky. V tomto příkladu vytvoříte stránku, která umožní uživatelům zadat dvě čísla, pak je přidá a zobrazí výsledek.

1. V editoru vytvořte nový soubor a pojmenujte jej *AddNumbers. cshtml*.
2. Zkopírujte následující kód a označení na stránku a nahraďte cokoli již na stránce.  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    Tady je několik věcí, které můžete poznamenat:

    - `@` znak spustí první blok kódu na stránce a předá `totalMessage` proměnnou, která je vložena poblíž dolní části stránky.
    - Blok v horní části stránky je uzavřený ve složených závorkách.
    - V bloku v horní části všechny řádky končí středníkem.
    - Proměnné `total`, `num1`, `num2`a `totalMessage` ukládají několik čísel a řetězce.
    - Literální řetězcová hodnota přiřazená k proměnné `totalMessage` je v dvojitých uvozovkách.
    - Vzhledem k tomu, že kód rozlišuje velká a malá písmena, je-li proměnná `totalMessage` použita v dolní části stránky, její název musí přesně odpovídat proměnné v horní části.
    - Výraz `num1.AsInt() + num2.AsInt()` ukazuje, jak pracovat s objekty a metodami. Metoda `AsInt` u každé proměnné převede řetězec zadaný uživatelem na číslo (celé číslo), takže můžete na něm provádět aritmetické operace.
    - Značka `<form>` obsahuje atribut `method="post"`. To určuje, že když uživatel klikne na **Přidat**, stránka se pošle na server pomocí metody HTTP POST. Po odeslání stránky se `if(IsPost)` test vyhodnotí jako true a spustí se podmíněný kód a zobrazí se výsledek přidání čísel.
3. Uložte stránku a spusťte ji v prohlížeči. (Před spuštěním se ujistěte, že je stránka vybraná v pracovním prostoru **soubory** .) Zadejte dvě celá čísla a potom klikněte na tlačítko **Přidat** . 

    ![Razor-Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a>Základní koncepty programování

Tento článek vám poskytne přehled o ASP.NET webovém programování. Nejedná se o vyčerpávající přezkoumání, a to pouze rychlou prohlídku prostřednictvím konceptů programování, které použijete nejčastěji. I když to bude mít skoro všechno, co budete potřebovat k zahájení práce s ASP.NET webovými stránkami.

Ale první, což je málo technického pozadí.

### <a name="the-razor-syntax-server-code-and-aspnet"></a>Syntaxe Razor, kód serveru a ASP.NET

Syntaxe Razor je jednoduchá programovací syntaxe pro vkládání kódu založeného na serveru na webové stránce. Na webové stránce, která používá syntaxe Razor, existují dva druhy obsahu: obsah klienta a kód serveru. Obsah klienta je ta, kterou jste použili pro webové stránky: značky HTML (elementy), informace o stylu, jako je například CSS, možná některý klientský skript, například JavaScript, a prostý text.

Syntaxe Razor umožňuje přidat serverový kód do tohoto obsahu klienta. Pokud je na stránce kód serveru, server nejprve spustí tento kód, než pošle stránku do prohlížeče. Po spuštění na serveru může kód provádět úlohy, které mohou být mnohem složitější pomocí samotného klientského obsahu, jako je například přístup k databázím založeným na serveru. Nejdůležitější je, že serverový kód může dynamicky vytvářet obsah &#8212; klienta, který může generovat kód HTML nebo jiný obsah za běhu a pak ho odeslat prohlížeči spolu se všemi statickými HTML, které stránka může obsahovat. V perspektivě prohlížeče se obsah klienta generovaný kódem serveru neliší od jiného obsahu klienta. Jak už jste viděli, kód serveru, který je potřeba, je poměrně jednoduchý.

ASP.NET webové stránky, které zahrnují syntaxe Razor mají speciální příponu souboru ( *. cshtml* nebo *. vbhtml*). Server rozpoznává tato rozšíření, spouští kód označený syntaxe Razor a poté odesílá stránku do prohlížeče.

### <a name="where-does-aspnet-fit-in"></a>Kde se ASP.NET vejde?

Syntaxe Razor vychází z technologie od Microsoftu s názvem ASP.NET, která je zase založená na .NET Framework Microsoft. The.NET Framework je Big, komplexní programovací rozhraní Microsoftu pro vývoj prakticky jakéhokoli typu počítačové aplikace. ASP.NET je součástí .NET Framework, který je speciálně navržený pro vytváření webových aplikací. Vývojáři používali ASP.NET k vytvoření mnoha největších a nejvyšších webů provozu na světě. (Kdykoli se zobrazí přípona názvu souboru *. aspx* jako součást adresy URL v lokalitě, budete si vědomi, že se web napsal pomocí ASP.NET.)

Syntaxe Razor poskytuje veškerou sílu ASP.NET, ale s využitím zjednodušené syntaxe, která se snadno naučíte, pokud jste odborníkem na začátečníky a máte vyšší produktivitu. I když se tato syntaxe snadno používá, její rodinný vztah k ASP.NET a .NET Framework znamená, že když se vaše weby stanou sofistikovanější, máte sílu větší architektury, kterou máte k dispozici.

![Razor-Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> **Třídy a instance**
> 
> ASP.NET Server Code používá objekty, které jsou vytvořeny na nápad třídy. Třída je definicí nebo šablonou pro objekt. Například aplikace může obsahovat třídu `Customer` definující vlastnosti a metody, které vyžaduje objekt zákazníka.
> 
> Když aplikace potřebuje pracovat se skutečnými informacemi o zákaznících, vytvoří instanci ( *nebo vytvoří instanci) objektu*zákazníka. Každý jednotlivý zákazník je samostatnou instancí třídy `Customer`. Každá instance podporuje stejné vlastnosti a metody, ale hodnoty vlastností každé instance jsou obvykle rozdílné, protože každý objekt zákazníka je jedinečný. V jednom objektu zákazníka může být vlastnost `LastName` "Smith"; v jiném objektu zákazníka by vlastnost `LastName` mohla být "Novotný".
> 
> Podobně je každá jednotlivá webová stránka na vašem webu `Page` objekt, který je instancí třídy `Page`. Tlačítko na stránce je objekt `Button`, který je instancí třídy `Button` a tak dále. Každá instance má své vlastní charakteristiky, ale všechny jsou založeny na tom, co je zadáno v definici třídy objektu.

## <a name="basic-syntax"></a>Základní syntaxe

Dříve jste viděli základní příklad, jak vytvořit stránku webových stránek ASP.NET a jak můžete přidat serverový kód do kódu HTML. Tady se naučíte základy psaní kódu serveru ASP.NET pomocí syntaxe Razor &#8212; , což jsou pravidla programování.

Pokud máte zkušenosti s programováním (zejména pokud jste použili C, C++, C#, Visual Basic nebo JavaScript), je většina věcí, kterou si přečtete, dobře známá. Pravděpodobně budete potřebovat seznámení pouze s tím, jak je serverový kód přidán do značek v souborech *. cshtml* .

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a>Kombinování textu, značek a kódu v blocích kódu

V blocích serverového kódu často chcete na stránku výstup textu nebo značky (nebo obojí). Pokud blok kódu serveru obsahuje text, který není kód a místo toho by měl být vykreslen tak, jak je, ASP.NET musí být schopni tento text odlišit od kódu. To lze provést několika způsoby.

- Vložte text do prvku HTML, jako je `<p></p>` nebo `<em></em>`:   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    Element HTML může obsahovat text, další prvky HTML a výrazy kódu serveru. Když ASP.NET uvidí otevření značky HTML (například `<p>`), vykreslí vše včetně prvku a jeho obsahu tak, jak je do prohlížeče, a překládá výrazy kódu serveru při jejich přechodu.
- Použijte operátor `@:` nebo prvek `<text>`. `@:` vytvoří výstup jednoho řádku obsahu obsahujícího prostý text nebo nespárované značky HTML. element `<text>` obklopuje více řádků do výstupu. Tyto možnosti jsou užitečné, pokud nechcete vykreslit prvek HTML jako součást výstupu.  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    Pokud chcete výstupovat více řádků textu nebo nespárované značky HTML, můžete před každý řádek zadat `@:`, nebo můžete uzavřít řádek do `<text>` elementu. Podobně jako operátor `@:`, jsou`<text>` značky používány ASP.NET k identifikaci textového obsahu a nejsou nikdy vykresleny ve výstupu stránky.

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    První příklad opakuje předchozí příklad, ale používá jednu dvojici `<text>` značek k uzavření textu, který se má vykreslit. V druhém příkladu jsou značky `<text>` a `</text>` uzavřeny tři řádky, všechny, které obsahují neuzavřený text a nespárované značky HTML (`<br />`), spolu s kódem serveru a odpovídajícími značkami HTML. Znovu můžete také předcházet každý řádek jednotlivě pomocí operátoru `@:`; Jak funguje.

    > [!NOTE]
    > Při výstupu textu, jak je znázorněno v &#8212; této části pomocí elementu jazyka HTML, operátoru `@:` nebo elementu &#8212; `<text>` ASP.NET nekóduje výstup do kódu HTML. (Jak bylo uvedeno dříve, ASP.NET zakóduje výstup výrazů serverového kódu a bloků serverového kódu, které jsou před `@`, s výjimkou zvláštních případů uvedených v této části.)

### <a name="whitespace"></a>Typy

Nadbytečné mezery v příkazu (a mimo řetězcový literál) neovlivňují příkaz:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

Zalomení řádku v příkazu nemá žádný vliv na příkaz a lze zabalit příkazy pro čitelnost. Následující příkazy jsou stejné:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

Nemůžete však obtékat čáru uprostřed řetězcového literálu. Následující příklad nefunguje:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

Pro kombinování dlouhého řetězce, který se zalomí na více řádků, jako je výše uvedený kód, existují dvě možnosti. Můžete použít operátor zřetězení (`+`), který uvidíte dále v tomto článku. Můžete také použít `@` znak k vytvoření doslovného řetězcového literálu, jak jste viděli výše v tomto článku. Můžete přerušit doslovné řetězce literálů napříč řádky:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a>Komentáře kódu (a označení)

Komentáře umožňují psát si poznámky pro sebe nebo jiné. Také vám umožňují zakázat (*komentovat*) oddíl kódu nebo značky, které nechcete spustit, ale chcete na stránce uchovávat čas.

Existuje odlišná syntaxe komentářů pro kód Razor a kód HTML. Stejně jako u všech kódů Razor jsou na serveru zpracovávány komentáře Razor (a poté odstraněny) před odesláním stránky do prohlížeče. Proto syntaxe komentářů Razor umožňuje vkládat komentáře do kódu (nebo dokonce do značky), které vidíte při úpravách souboru, ale uživatelé nevidí, i ve zdroji stránky.

V případě komentářů ASP.NET Razor zahájíte komentář pomocí `@*` a ukončíte ho `*@`. Komentář může být na jednom řádku nebo několika řádcích:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

Zde je komentář v rámci bloku kódu:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

Zde je stejný blok kódu, který má řádek s komentářem kódu, aby se nespouštěl:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

V bloku kódu jako alternativu k použití syntaxe komentářů Razor můžete použít syntaxi komentářů programovacího jazyka, který používáte, například C#:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

V C#jednom řádku předchází `//` znaků a víceřádkové komentáře začínají `/*` a končí `*/`. (Stejně jako u komentářů Razor C# nejsou komentáře vykreslovány do prohlížeče.)

V případě značky, jak budete pravděpodobně znát, můžete vytvořit komentář HTML:

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

Komentáře HTML začínají `<!--`mi znaky a končí `-->`. K obklopení nejenom textu můžete použít komentáře ve formátu HTML, ale také všechny značky HTML, které můžete chtít na stránce zachovat, ale nechcete je vykreslit. V tomto komentáři HTML se skryje celý obsah značek a text, který obsahují:

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

Na rozdíl od komentářů Razor *jsou* komentáře HTML vykresleny na stránku a uživatel je uvidí pomocí zobrazení zdroje stránky.

Syntaxe Razor má omezení pro vnořené bloky C#. Další informace najdete v [pojmenovaných C# proměnných a vnořených blocích generuje porušený kód](http://aspnetwebstack.codeplex.com/workitem/1914) .

## <a name="variables"></a>Proměnné

Proměnná je pojmenovaný objekt, který slouží k ukládání dat. Proměnné můžete pojmenovat cokoli, ale název musí začínat znakem abecedy a nesmí obsahovat mezery ani vyhrazené znaky.

### <a name="variables-and-data-types"></a>Proměnné a datové typy

Proměnná může mít určitý datový typ, který označuje, jaký druh dat je uložený v proměnné. Můžete mít řetězcové proměnné, které ukládají řetězcové hodnoty (například &quot;Hello World&quot;), celočíselné proměnné, které ukládají hodnoty s celými čísly (například 3 nebo 79), a proměnné data uchovávající hodnoty data v různých formátech (například 4/12/2012 nebo březen 2009). A existuje mnoho dalších typů dat, které můžete použít.

Obecně ale nemusíte zadávat typ pro proměnnou. Ve většině času ASP.NET dokáže zjistit typ podle toho, jak se data v proměnné používají. (Někdy musíte zadat typ; uvidíte příklady, kde je to pravda.)

Deklarujete proměnnou pomocí klíčového slova `var` (Pokud nechcete zadat typ) nebo pomocí názvu typu:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

Následující příklad ukazuje několik typických použití proměnných na webové stránce:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

Pokud na stránce zkombinujete předchozí příklady, zobrazí se v prohlížeči:

![Razor-Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a>Převod a testování datových typů

I když ASP.NET může obvykle určit datový typ automaticky, někdy to nemůže. Proto může být nutné pomáhat s ASP.NETm při provádění explicitního převodu. I v případě, že není nutné převést typy, někdy je vhodné otestovat a zjistit, se kterými typem dat pracujete.

Nejběžnějším případem je, že je nutné převést řetězec na jiný typ, jako je například na celé číslo nebo datum. Následující příklad ukazuje typický případ, kdy je nutné převést řetězec na číslo.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

Jako pravidlo se vstup uživatele dostane jako řetězce. I když jste si vyzkoušeli, že uživatel zadal číslo, a to i v případě, že zadali číslici, když se odešle vstup uživatele a přečtete ho v kódu, data jsou ve formátu řetězce. Proto je nutné převést řetězec na číslo. Pokud se v příkladu pokusíte provést aritmetické operace s hodnotami bez jejich převádění, dojde k následující chybě, protože ASP.NET nemůže přidat dva řetězce:

*Typ String nejde implicitně převést na int.*

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
    Převede řetězec představující celé číslo (například "593") na celé číslo.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample28.cs)]
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
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample29.cs)]
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
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample30.cs)]
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
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample31.cs)]
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
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample32.cs)]
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
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a>Operátory

Operátor je klíčové slovo nebo znak, který oznamuje ASP.NET, jaký druh příkazu má být proveden ve výrazu. C# Jazyk (a syntaxe Razor, který je na něm založen), podporuje mnoho operátorů, ale stačí, abyste pomohli jenom rozpoznat pár, abyste mohli začít. Následující tabulka shrnuje nejběžnější operátory.

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
        `+` `-` `*` `/`
    :::column-end:::
    :::column:::
    Matematické operátory používané v numerických výrazech.
    :::column-end:::
    :::column:::
        [!code-css[Main](introducing-razor-syntax-c/samples/sample34.css)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `=`
    :::column-end:::
    :::column:::
    Přiřazení. Přiřadí hodnotu na pravé straně příkazu k objektu na levé straně.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample35.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `==`
    :::column-end:::
    :::column:::
    Porovnávání. Vrátí `true`, pokud jsou hodnoty stejné. (Všimněte si rozdílu mezi operátorem `=` a operátorem `==`.)
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample36.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!=`
    :::column-end:::
    :::column:::
    Nerovnost. Vrátí `true`, pokud se hodnoty neshodují.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample37.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `< > <= >=`
    :::column-end:::
    :::column:::
    Menší než, větší než, menší než nebo rovno, a větší než nebo rovno.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample38.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+`
    :::column-end:::
    :::column:::
    Zřetězení, které se používá k spojování řetězců. ASP.NET ví rozdíl mezi tímto operátorem a operátorem sčítání na základě datového typu výrazu.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+=` `-=`
    :::column-end:::
    :::column:::
    Operátory přírůstku a snížení, které přidají a odečtou 1 (v uvedeném pořadí) z proměnné.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample40.cs)]
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
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample41.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `()`
    :::column-end:::
    :::column:::
    Závorky. Slouží k seskupení výrazů a předání parametrů metodám.
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample42.js)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `[]`
    :::column-end:::
    :::column:::
    Hranat. Používá se pro přístup k hodnotám v polích nebo kolekcích.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample43.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `!`
    :::column-end:::
    :::column:::
    Mění. Obrátí `true` hodnotu na `false` a naopak. Obvykle se používá jako zkrácený způsob testování pro `false` (tj. není-li `true`).
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `&&` `||`
    :::column-end:::
    :::column:::
    Logický operátor AND a OR, který se používá k propojení podmínek.
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]
    :::column-end:::
:::row-end:::

<a id="ID_WorkingWithFileAndFolderPaths"></a>
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

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a>Odkazování na virtuální kořenový adresář: operátor ~ a metoda href

V souboru *. cshtml* nebo *. vbhtml* můžete odkazovat na virtuální kořenovou cestu pomocí operátoru `~`. To je velmi užitečné, protože můžete přesouvat stránky v lokalitě a jakékoli odkazy, které obsahují na jiné stránky, nebudou přerušeny. K dispozici je také užitečné v případě, že jste web někdy přesunuli do jiného umístění. Zde je několik příkladů:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

Pokud je web `http://myserver/myapp`, v takovém případě bude ASP.NET považovat tyto cesty při spuštění stránky:

- `myImagesFolder`: `http://myserver/myapp/images`
- `myStyleSheet`: `http://myserver/myapp/styles/Stylesheet.css`

(Tyto cesty ve skutečnosti neuvidíte jako hodnoty proměnné, ale ASP.NET je bude považovat za to, co byly.)

Operátor `~` lze použít jak v kódu serveru (jak je uvedeno výše), tak v označení, například takto:

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

V kódu se používá operátor `~` k vytváření cest k prostředkům, jako jsou soubory obrázků, jiné webové stránky a soubory CSS. Po spuštění stránky ASP.NET vyhledá stránku (kód i kód) a přeloží všechny `~` odkazy na příslušnou cestu.

## <a name="conditional-logic-and-loops"></a>Podmíněná logika a smyčky

Kód serveru ASP.NET vám umožňuje provádět úlohy na základě podmínek a napsat kód, který opakuje příkazy, a to podle určitého počtu, kolikrát (tj. kód spouštějící smyčku).

### <a name="testing-conditions"></a>Podmínky testování

Chcete-li otestovat jednoduchou podmínku, použijte příkaz `if`, který vrací hodnotu true nebo false na základě testu, který zadáte:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

Klíčové slovo `if` spustí blok. Skutečný test (podmínka) je v závorkách a vrátí hodnotu true nebo false. Příkazy, které se spustí, pokud je test true, jsou uzavřeny ve složených závorkách. Příkaz `if` může zahrnovat blok `else`, který určuje příkazy, které se mají spustit, pokud je podmínka nepravdivá:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

Pomocí `else if`ového bloku můžete přidat víc podmínek:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

V tomto příkladu, pokud není první podmínka v bloku If nastavena na hodnotu true, je zaškrtnuta podmínka `else if`. Pokud je tato podmínka splněna, jsou provedeny příkazy v bloku `else if`. Pokud není splněna žádná z podmínek, jsou provedeny příkazy v bloku `else`. Můžete přidat libovolný počet else if Blocks a pak zavřít s `else` blok jako &quot;vše jiného&quot; podmínka.

K otestování velkého počtu podmínek použijte `switch` blok:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

Hodnota, která se má testovat, je v závorkách (v příkladu `weekday` proměnné). Každý jednotlivý test používá příkaz `case`, který končí dvojtečkou (:). Je-li hodnota příkazu `case` shodná s testovací hodnotou, je proveden kód v tomto bloku případu. Všechny příkazy Case zavřete příkazem `break`. (Pokud zapomenete zahrnout do každého bloku `case`, kód z dalšího příkazu `case` se spustí také.) `switch` blok často obsahuje `default` příkaz jako poslední případ pro &quot;vše ostatní&quot; možnost, která se spustí, pokud žádný z ostatních případů neplatí.

Výsledek posledního dvou podmíněných bloků zobrazených v prohlížeči:

![Razor – Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a>Kód smyčky

Často je třeba spouštět stejné příkazy opakovaně. Provedete to pomocí smyčky. Například často spustíte stejné příkazy pro každou položku v kolekci dat. Pokud víte přesně, kolikrát chcete cyklovat, můžete použít smyčku `for`. Tento druh smyčky je zvláště užitečný pro inventarizaci a počítání:

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

Smyčka začíná klíčovým slovem `for`, po kterém následují tři příkazy v závorkách, přičemž každý z nich končí středníkem.

- V závorkách první příkaz (`var i=10;`) vytvoří čítač a inicializuje jej na hodnotu 10. Nemusíte pojmenovat `i` &#8212; čítače. můžete použít libovolnou proměnnou. Po spuštění smyčky `for` se čítač automaticky zvýší.
- Druhý příkaz (`i < 21;`) nastaví podmínku pro jak daleko chcete počítat. V takovém případě chcete, aby bylo možné přejít maximálně o 20 (to znamená, že bude pokračovat i v případě, že je čítač menší než 21).
- Třetí příkaz (`i++`) používá operátor přírůstek, který jednoduše určuje, že čítač by měl mít 1 přidaný čítač při každém spuštění smyčky.

Uvnitř složených závorek je kód, který se spustí pro každou iteraci smyčky. Kód vytvoří nový odstavec (`<p>` element) pokaždé a přidá řádek do výstupu a zobrazí hodnotu `i` (čítač). Když spustíte tuto stránku, v příkladu se vytvoří 11 řádků, ve kterých se zobrazí výstup, a text na každém řádku, který označuje číslo položky.

![Razor-Img11](introducing-razor-syntax-c/_static/image11.jpg)

Pokud pracujete s kolekcí nebo polem, často používáte smyčku `foreach`. Kolekce je skupina podobných objektů a smyčka `foreach` umožňuje provádět úlohy na každé položce v kolekci. Tento typ smyčky je vhodný pro kolekce, protože na rozdíl od `for` smyčky nemusíte zvyšovat čítač nebo nastavit limit. Místo toho kód smyčky `foreach` jednoduše projde přes kolekci, dokud není dokončena.

Například následující kód vrátí položky v kolekci `Request.ServerVariables`, což je objekt, který obsahuje informace o vašem webovém serveru. Používá smyčku `foreac` h k zobrazení názvu každé položky vytvořením nového prvku `<li>` v seznamu s odrážkami HTML.

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

Za klíčovým slovem `foreach` následuje závorky, kde deklarujete proměnnou reprezentující jednu položku v kolekci (v příkladu `var item`) následovaný klíčovým slovem `in` následovaným kolekcí, kterou chcete procyklovat. V těle `foreach` smyčky můžete k aktuální položce přistupovat pomocí proměnné, kterou jste předtím deklarovali.

![Razor-Img12](introducing-razor-syntax-c/_static/image12.jpg)

Chcete-li vytvořit obecnější smyčku pro účely, použijte příkaz `while`:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

Smyčka `while` začíná klíčovým slovem `while` následovanými závorkami, kde určíte, jak dlouho bude smyčka pokračovat (zde, pokud je `countNum` menší než 50), pak se blok opakuje. Smyčky typicky přidávají (přidávají do) nebo snižují (odečtou z) proměnnou nebo objekt, který se používá pro počítání. V příkladu operátor `+=` přidá 1 pro `countNum` pokaždé, když se smyčka spustí. (Chcete-li snížit proměnnou ve smyčce, která počítá dolů, použijte operátor snížení `-=`).

## <a name="objects-and-collections"></a>Objekty a kolekce

Skoro všechno na webu ASP.NET je objekt, včetně samotné webové stránky. Tato část popisuje některé důležité objekty, se kterými se často pracujete ve vašem kódu.

### <a name="page-objects"></a>Objekty stránky

Nejzákladnější objekt v ASP.NET je stránka. K vlastnostem objektu stránky můžete přistupovat přímo bez jakéhokoli opravňujícího objektu. Následující kód Získá cestu k souboru stránky pomocí objektu `Request` stránky:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

Chcete-li zrušit zaškrtnutí, že odkazujete na vlastnosti a metody v objektu aktuální stránky, můžete volitelně použít klíčové slovo `this` pro reprezentaci objektu Page v kódu. Zde je předchozí příklad kódu s `this` přidat k reprezentaci stránky:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

Pomocí vlastností objektu `Page` můžete získat velké množství informací, například:

- `Request`. Jak už jste viděli, jedná se o kolekci informací o aktuální žádosti, včetně typu prohlížeče, který požadavek odeslal, adresu URL stránky, identitu uživatele atd.
- `Response`. Toto je kolekce informací o odpovědi (stránky), která se odešle do prohlížeče, když je kód serveru spuštěný. Tuto vlastnost můžete například použít k zápisu informací do odpovědi. 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a>Objekty kolekce (pole a slovníky)

*Kolekce* je skupina objektů stejného typu, například kolekce `Customer` objektů z databáze. ASP.NET obsahuje mnoho předdefinovaných kolekcí, jako je kolekce `Request.Files`.

Často budete pracovat s daty v kolekcích. Dva společné typy kolekcí jsou *pole* a *slovník*. Pole je užitečné, pokud chcete uložit kolekci podobných položek, ale nechcete vytvořit samostatnou proměnnou pro uchování každé položky:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

Pomocí polí deklarujete konkrétní datový typ, například `string`, `int`nebo `DateTime`. Chcete-li označit, že proměnná může obsahovat pole, přidejte do deklarace hranaté závorky (například `string[]` nebo `int[]`). K položkám v poli můžete přistupovat pomocí jejich pozice (indexu) nebo pomocí příkazu `foreach`. Indexy polí jsou počítány od &#8212; nuly, tj. první položka je na pozici 0, druhá položka je na pozici 1 atd.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

Počet položek v poli můžete určit získáním jeho vlastnosti `Length`. Chcete-li získat pozici konkrétní položky v poli (pro hledání v poli), použijte metodu `Array.IndexOf`. Můžete také provést akce, jako je vrácení obsahu pole (`Array.Reverse` metody) nebo řazení obsahu (metoda `Array.Sort`).

Výstup kódu řetězcového pole zobrazeného v prohlížeči:

![Razor-Img13](introducing-razor-syntax-c/_static/image13.jpg)

Slovník je kolekce párů klíč/hodnota, kde zadáte klíč (nebo název) pro nastavení nebo načtení příslušné hodnoty:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

Chcete-li vytvořit slovník, použijte klíčové slovo `new` pro indikaci, že vytváříte nový objekt Dictionary. K proměnné můžete přiřadit slovník pomocí klíčového slova `var`. Datové typy položek ve slovníku označíte pomocí lomených závorek (`< >`). Na konci deklarace je nutné přidat dvojici závorek, protože se jedná o metodu, která vytvoří nový slovník.

Chcete-li přidat položky do slovníku, můžete zavolat metodu `Add` proměnné Dictionary (`myScores` v tomto případě) a poté zadat klíč a hodnotu. Alternativně můžete pomocí hranatých závorek označit klíč a provést jednoduché přiřazení, jako v následujícím příkladu:

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

Pokud chcete získat hodnotu ze slovníku, zadáte klíč v závorkách:

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a>Volání metod s parametry

Jak si přečtete výše v tomto článku, objekty, se kterými program pracuje, můžou mít metody. Například `Database` objekt může mít metodu `Database.Connect`. Mnoho metod má také jeden nebo více parametrů. *Parametr* je hodnota, kterou předáte metodě, aby mohla metoda dokončit její úlohu. Podívejte se například na deklaraci metody `Request.MapPath`, která přijímá tři parametry:

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

(Řádek byl zabalen, aby byl čitelnější. Mějte na paměti, že můžete umístit konce řádků téměř na jakékoli místo kromě řetězců, které jsou uzavřeny v uvozovkách.)

Tato metoda vrátí fyzickou cestu na serveru, který odpovídá zadané virtuální cestě. Tři parametry pro metodu jsou `virtualPath`, `baseVirtualDir`a `allowCrossAppMapping`. (Všimněte si, že v deklaraci jsou parametry uvedeny s datovými typy dat, která budou přijímat.) Při volání této metody je nutné dodat hodnoty pro všechny tři parametry.

Syntaxe Razor poskytuje dvě možnosti pro předávání parametrů metodě: *poziční parametry* a *pojmenované parametry*. Chcete-li volat metodu pomocí pozičních parametrů, předáte parametry v přesném pořadí, které je zadáno v deklaraci metody. (Toto pořadí byste obvykle znali v dokumentaci k metodě.) Je nutné postupovat podle pořadí a v případě potřeby nemůžete přeskočit &#8212; žádný z parametrů, předáte prázdný řetězec (`""`) nebo `null` pozičního parametru, pro který nemáte hodnotu.

Následující příklad předpokládá, že máte ve svém webu složku s názvem *skripty* . Kód volá metodu `Request.MapPath` a předá hodnoty pro tři parametry ve správném pořadí. Pak zobrazí výslednou mapovanou cestu.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

Pokud má metoda mnoho parametrů, můžete si kód lépe přečíst pomocí pojmenovaných parametrů. Chcete-li volat metodu pomocí pojmenovaných parametrů, zadejte název parametru následovaný dvojtečkou (:) a pak hodnotu. Výhodou pojmenovaných parametrů je, že je můžete předat v libovolném požadovaném pořadí. (Nevýhodou je, že volání metody není jako kompaktní.)

Následující příklad volá stejnou metodu jako výše, ale používá pojmenované parametry k poskytnutí těchto hodnot:

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

Jak vidíte, parametry jsou předány v jiném pořadí. Pokud však spustíte předchozí příklad a tento příklad vrátí stejnou hodnotu.

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a>Zpracování chyb

### <a name="try-catch-statements"></a>Příkazy try-catch

Často budete mít ve svém kódu příkazy, které mohou selhat z důvodů mimo váš ovládací prvek. Příklad:

- Pokud se váš kód pokusí vytvořit soubor nebo k němu získat přístup, může dojít k nejrůznějším chybám. Soubor, který chcete, možná neexistuje, může být uzamčen, kód pravděpodobně nemá oprávnění atd.
- Podobně platí, že pokud se váš kód pokusí aktualizovat záznamy v databázi, může dojít k problémům s oprávněními, připojení k databázi může být vyřazeno, data, která mají být uložena, mohou být neplatná atd.

V programovacích podmínkách se tyto situace nazývají *výjimky*. Pokud váš kód narazí na výjimku, vygeneruje (vyvolá) chybovou zprávu, která je na nejvyšší úrovni uživatelům obtěžující:

![Razor-Img14](introducing-razor-syntax-c/_static/image14.jpg)

V situacích, kdy se váš kód může setkat s výjimkami, a aby se předešlo chybovým zprávám tohoto typu, můžete použít příkazy `try/catch`. V příkazu `try` spustíte kód, který kontrolujete. V jednom nebo více příkazech `catch` můžete vyhledat konkrétní chyby (konkrétní typy výjimek), ke kterým mohlo dojít. Můžete zahrnout tolik příkazů `catch`, kolik potřebujete pro hledání chyb, které očekáváte.

> [!NOTE]
> Doporučujeme, abyste se vyhnuli použití metody `Response.Redirect` v příkazech `try/catch`, protože to může způsobit výjimku na stránce.

Následující příklad ukazuje stránku, která vytvoří textový soubor pro první požadavek a pak zobrazí tlačítko, které uživateli otevře soubor. Příklad záměrně používá špatný název souboru, takže bude způsobovat výjimku. Kód zahrnuje `catch` příkazy pro dvě možné výjimky: `FileNotFoundException`, ke kterým dojde, pokud je název souboru špatný a `DirectoryNotFoundException`, ke kterému dochází, pokud ASP.NET nemůže dokonce najít složku. (Můžete zrušit komentář k příkazu v příkladu, abyste viděli, jak se spustí, když vše funguje správně.)

Pokud váš kód nezpracovává výjimku, zobrazila se chybová stránka, například snímek předchozí obrazovky. Nicméně část `try/catch` pomáhá zabránit uživateli v zobrazování těchto typů chyb.

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a>Další prostředky

**Programování pomocí Visual Basic**

[Příloha: Visual Basic jazyk a syntax](https://go.microsoft.com/fwlink/?LinkId=202908)

**Referenční dokumentace**

[ASP.NET](https://msdn.microsoft.com/library/ee532866.aspx)

[C#Language](https://msdn.microsoft.com/library/kx37x362.aspx)

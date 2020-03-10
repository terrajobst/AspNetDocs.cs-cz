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
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-visual-basic"></a><span data-ttu-id="b397c-103">Úvod do webového programování v ASP.NET pomocí syntaxe Razor (Visual Basic)</span><span class="sxs-lookup"><span data-stu-id="b397c-103">Introduction to ASP.NET Web Programming Using the Razor Syntax (Visual Basic)</span></span>

<span data-ttu-id="b397c-104">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="b397c-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="b397c-105">Tento článek vám poskytne přehled o programování s ASP.NET webovými stránkami pomocí syntaxe Razor a Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="b397c-105">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax and Visual Basic.</span></span> <span data-ttu-id="b397c-106">ASP.NET je technologie Microsoftu pro spouštění dynamických webových stránek na webových serverech.</span><span class="sxs-lookup"><span data-stu-id="b397c-106">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span>
> 
> <span data-ttu-id="b397c-107">**Co se naučíte**:</span><span class="sxs-lookup"><span data-stu-id="b397c-107">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="b397c-108">Nejčastějších 8 programovacích tipů pro Začínáme s programováním webových stránek ASP.NET pomocí syntaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="b397c-108">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="b397c-109">Základní koncepty programování, které budete potřebovat.</span><span class="sxs-lookup"><span data-stu-id="b397c-109">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="b397c-110">Jaký kód serveru ASP.NET a syntaxe Razor se týkají.</span><span class="sxs-lookup"><span data-stu-id="b397c-110">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="b397c-111">Verze softwaru</span><span class="sxs-lookup"><span data-stu-id="b397c-111">Software versions</span></span>
> 
> 
> - <span data-ttu-id="b397c-112">Webové stránky ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="b397c-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="b397c-113">Tento kurz funguje také s ASP.NET webovými stránkami 2.</span><span class="sxs-lookup"><span data-stu-id="b397c-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="b397c-114">Většina příkladů použití webových stránek ASP.NET s využitím C#syntaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="b397c-114">Most examples of using ASP.NET Web Pages with Razor syntax use C#.</span></span> <span data-ttu-id="b397c-115">Ale syntaxe Razor také podporuje Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="b397c-115">But the Razor syntax also supports Visual Basic.</span></span> <span data-ttu-id="b397c-116">Chcete-li programovat webovou stránku ASP.NET v Visual Basic, vytvořte webovou stránku s příponou názvu souboru *. vbhtml* a pak přidejte Visual Basic kód.</span><span class="sxs-lookup"><span data-stu-id="b397c-116">To program an ASP.NET web page in Visual Basic, you create a web page with a *.vbhtml* filename extension, and then add Visual Basic code.</span></span> <span data-ttu-id="b397c-117">Tento článek vám poskytne přehled o práci s Visual Basicm jazykem a syntaxí pro vytváření webových stránek ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="b397c-117">This article gives you an overview of working with the Visual Basic language and syntax to create ASP.NET Webpages.</span></span>

> [!NOTE]
> <span data-ttu-id="b397c-118">Výchozí šablony webu pro WebMatrix společnosti Microsoft (**pekařes**, **Fotogalerie a** **úvodní web**atd.) jsou k dispozici v C# a Visual Basic verzích.</span><span class="sxs-lookup"><span data-stu-id="b397c-118">The default website templates for Microsoft WebMatrix (**Bakery**, **Photo Gallery**, and **Starter Site**, etc.) are available in C# and Visual Basic versions.</span></span> <span data-ttu-id="b397c-119">Šablony Visual Basic můžete nainstalovat jako balíčky NuGet.</span><span class="sxs-lookup"><span data-stu-id="b397c-119">You can install the Visual Basic templates by as NuGet packages.</span></span> <span data-ttu-id="b397c-120">Šablony webu jsou nainstalovány v kořenové složce vaší lokality ve složce s názvem *šablony společnosti Microsoft*.</span><span class="sxs-lookup"><span data-stu-id="b397c-120">Website templates are installed in the root folder of your site in a folder named *Microsoft Templates*.</span></span>

## <a name="the-top-8-programming-tips"></a><span data-ttu-id="b397c-121">Prvních 8 tipů pro programování</span><span class="sxs-lookup"><span data-stu-id="b397c-121">The Top 8 Programming Tips</span></span>

<span data-ttu-id="b397c-122">Tato část obsahuje několik tipů, které bezpodmínečně potřebujete znát při psaní kódu ASP.NET serveru pomocí syntaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="b397c-122">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="b397c-123">1. na stránku přidáte kód pomocí znaku @.</span><span class="sxs-lookup"><span data-stu-id="b397c-123">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="b397c-124">`@` znak spouští vložené výrazy, bloky s jedním příkazem a bloky s více příkazy:</span><span class="sxs-lookup"><span data-stu-id="b397c-124">The `@` character starts inline expressions, single-statement blocks, and multi-statement blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample1.vbhtml)]

<span data-ttu-id="b397c-125">Výsledek zobrazený v prohlížeči:</span><span class="sxs-lookup"><span data-stu-id="b397c-125">The result displayed in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-vb/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="b397c-127">**Kódování HTML**</span><span class="sxs-lookup"><span data-stu-id="b397c-127">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="b397c-128">Pokud zobrazíte obsah na stránce pomocí `@`ho znaku, jako v předchozích příkladech, ASP.NET kód HTML zakóduje výstup.</span><span class="sxs-lookup"><span data-stu-id="b397c-128">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="b397c-129">Tím se nahradí vyhrazené znaky HTML (například `<` a `>` a `&`) kódy, které umožňují zobrazení znaků jako znaků na webové stránce namísto interpretace jako značek nebo entit jazyka HTML.</span><span class="sxs-lookup"><span data-stu-id="b397c-129">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="b397c-130">Bez kódování HTML se výstup z kódu serveru nemusí zobrazit správně a může vystavit stránku pro rizika zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="b397c-130">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="b397c-131">Pokud je vaším cílem výstup kódu HTML, který vykresluje značky jako kód (například `<p></p>` pro odstavec nebo `<em></em>` k zdůraznění textu), přečtěte si část [kombinování textu, značky a kódu v blocích kódu](#BM_CombiningTextMarkupAndCode) dále v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="b397c-131">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="b397c-132">Další informace o kódování HTML najdete v tématu [práce s formuláři HTML v lokalitách webových stránek ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202892).</span><span class="sxs-lookup"><span data-stu-id="b397c-132">You can read more about HTML encoding in [Working with HTML Forms in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>

### <a name="2-you-enclose-code-blocks-with-codeend-code"></a><span data-ttu-id="b397c-133">2. uzavíráte bloky kódu s kódem... Koncový kód</span><span class="sxs-lookup"><span data-stu-id="b397c-133">2. You enclose code blocks with Code...End Code</span></span>

<span data-ttu-id="b397c-134">Blok kódu obsahuje jeden nebo více příkazů kódu a je uzavřen s klíčovými slovy `Code` a `End Code`.</span><span class="sxs-lookup"><span data-stu-id="b397c-134">A code block includes one or more code statements and is enclosed with the keywords `Code` and `End Code`.</span></span> <span data-ttu-id="b397c-135">Ihned po znaku &#8212; `@` vložte klíčové slovo Open `Code`, mezi kterými nemůžete vložit mezeru.</span><span class="sxs-lookup"><span data-stu-id="b397c-135">Place the opening `Code` keyword immediately after the `@` character &#8212; there can't be whitespace between them.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample2.vbhtml)]

<span data-ttu-id="b397c-136">Výsledek zobrazený v prohlížeči:</span><span class="sxs-lookup"><span data-stu-id="b397c-136">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-vb/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-line-break"></a><span data-ttu-id="b397c-138">3. uvnitř bloku se každý příkaz kódu ukončí s koncem řádku.</span><span class="sxs-lookup"><span data-stu-id="b397c-138">3. Inside a block, you end each code statement with a line break</span></span>

<span data-ttu-id="b397c-139">V Visual Basic blok kódu, každý příkaz končí koncem řádku.</span><span class="sxs-lookup"><span data-stu-id="b397c-139">In a Visual Basic code block, each statement ends with a line break.</span></span> <span data-ttu-id="b397c-140">(Později v článku uvidíte způsob, jak v případě potřeby zabalit příkaz dlouhého kódu do několika řádků.)</span><span class="sxs-lookup"><span data-stu-id="b397c-140">(Later in the article you'll see a way to wrap a long code statement into multiple lines if needed.)</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample3.vbhtml)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="b397c-141">4. proměnné použijete k uložení hodnot.</span><span class="sxs-lookup"><span data-stu-id="b397c-141">4. You use variables to store values</span></span>

<span data-ttu-id="b397c-142">Hodnoty můžete ukládat do *proměnné*, včetně řetězců, čísel a dat atd. Novou proměnnou vytvoříte pomocí klíčového slova `Dim`.</span><span class="sxs-lookup"><span data-stu-id="b397c-142">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `Dim` keyword.</span></span> <span data-ttu-id="b397c-143">Hodnoty proměnných můžete vkládat přímo na stránce pomocí `@`.</span><span class="sxs-lookup"><span data-stu-id="b397c-143">You can insert variable values directly in a page using `@`.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample4.vbhtml)]

<span data-ttu-id="b397c-144">Výsledek zobrazený v prohlížeči:</span><span class="sxs-lookup"><span data-stu-id="b397c-144">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-vb/_static/image3.jpg)

### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="b397c-146">5. Uzavřete řetězcové hodnoty literálu do dvojitých uvozovek.</span><span class="sxs-lookup"><span data-stu-id="b397c-146">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="b397c-147">*Řetězec* je posloupnost znaků, které jsou považovány za text.</span><span class="sxs-lookup"><span data-stu-id="b397c-147">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="b397c-148">Pokud chcete zadat řetězec, uzavřete ho do dvojitých uvozovek:</span><span class="sxs-lookup"><span data-stu-id="b397c-148">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample5.vbhtml)]

<span data-ttu-id="b397c-149">Chcete-li vložit dvojité uvozovky v rámci řetězcové hodnoty, vložte dva znaky dvojité uvozovky.</span><span class="sxs-lookup"><span data-stu-id="b397c-149">To embed double quotation marks within a string value, insert two double quotation mark characters.</span></span> <span data-ttu-id="b397c-150">Pokud chcete, aby se znak dvojité uvozovky objevily jednou ve výstupu stránky, zadejte ho jako `""` v řetězci v uvozovkách a pokud chcete, aby se zobrazilo dvakrát, zadejte ho jako `""""` v řetězci v uvozovkách.</span><span class="sxs-lookup"><span data-stu-id="b397c-150">If you want the double quotation character to appear once in the page output, enter it as `""` within the quoted string, and if you want it to appear twice, enter it as `""""` within the quoted string.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample6.vbhtml)]

<span data-ttu-id="b397c-151">Výsledek zobrazený v prohlížeči:</span><span class="sxs-lookup"><span data-stu-id="b397c-151">The result displayed in a browser:</span></span>

![Razor-Img4](introducing-razor-syntax-vb/_static/image4.jpg)

### <a name="6-visual-basic-code-is-not-case-sensitive"></a><span data-ttu-id="b397c-153">6. Visual Basic kód nerozlišuje velká a malá písmena</span><span class="sxs-lookup"><span data-stu-id="b397c-153">6. Visual Basic code is not case sensitive</span></span>

<span data-ttu-id="b397c-154">Jazyk Visual Basic nerozlišuje velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="b397c-154">The Visual Basic language is not case sensitive.</span></span> <span data-ttu-id="b397c-155">Klíčová slova pro programování (například `Dim`, `If`a `True`) a názvy proměnných (jako `myString`nebo `subTotal`) mohou být zapsány v každém případě.</span><span class="sxs-lookup"><span data-stu-id="b397c-155">Programming keywords (like `Dim`, `If`, and `True`) and variable names (like `myString`, or `subTotal`) can be written in any case.</span></span>

<span data-ttu-id="b397c-156">Následující řádky kódu přiřadí hodnotu proměnné `lastname` s použitím malých písmen a pak mají výstup hodnoty proměnné na stránku pomocí velkého jména.</span><span class="sxs-lookup"><span data-stu-id="b397c-156">The following lines of code assign a value to the variable `lastname` using a lowercase name, and then output the variable value to the page using an uppercase name.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample7.vbhtml)]

<span data-ttu-id="b397c-157">Výsledek zobrazený v prohlížeči:</span><span class="sxs-lookup"><span data-stu-id="b397c-157">The result displayed in a browser:</span></span>

![vb-syntax-5](introducing-razor-syntax-vb/_static/image5.jpg)

### <a name="7-much-of-your-coding-involves-working-with-objects"></a><span data-ttu-id="b397c-159">7. mnoho z vašich kódování zahrnuje práci s objekty</span><span class="sxs-lookup"><span data-stu-id="b397c-159">7. Much of your coding involves working with objects</span></span>

<span data-ttu-id="b397c-160">Objekt představuje věc, kterou můžete programovat se &#8212; stránkou, textovým polem, souborem, obrázkem, webovým požadavkem, e-mailovou zprávou, záznamem zákazníka (řádkem databáze) atd. Objekty mají vlastnosti, které popisují jejich &#8212; charakteristiky, objekt textového pole má vlastnost `Text`, objekt žádosti má vlastnost `Url`, e-mailová zpráva má vlastnost `From` a objekt Customer má vlastnost `FirstName`.</span><span class="sxs-lookup"><span data-stu-id="b397c-160">An object represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics &#8212; a text box object has a `Text` property, a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="b397c-161">Objekty mají také metody, které jsou &quot;slovesy&quot; mohou provádět.</span><span class="sxs-lookup"><span data-stu-id="b397c-161">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="b397c-162">Mezi příklady patří `Save` metoda objektu souboru, metoda `Rotate` objektu obrázku a metoda `Send` objektu e-mailu.</span><span class="sxs-lookup"><span data-stu-id="b397c-162">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="b397c-163">Často budete pracovat s objektem `Request`, který vám poskytne informace, jako jsou hodnoty polí formuláře na stránce (textová pole atd.), jaký typ prohlížeče požadavek odeslal, adresu URL stránky, identitu uživatele atd. Tento příklad ukazuje, jak získat přístup k vlastnostem objektu `Request` a jak volat metodu `MapPath` objektu `Request`, který poskytuje absolutní cestu stránky na serveru:</span><span class="sxs-lookup"><span data-stu-id="b397c-163">You'll often work with the `Request` object, which gives you information like the values of form fields on the page (text boxes, etc.), what type of browser made the request, the URL of the page, the user identity, etc. This example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample8.html)]

<span data-ttu-id="b397c-164">Výsledek zobrazený v prohlížeči:</span><span class="sxs-lookup"><span data-stu-id="b397c-164">The result displayed in a browser:</span></span>

![Razor-Img5](introducing-razor-syntax-vb/_static/image6.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="b397c-166">8. můžete napsat kód, který provede rozhodnutí.</span><span class="sxs-lookup"><span data-stu-id="b397c-166">8. You can write code that makes decisions</span></span>

<span data-ttu-id="b397c-167">Klíčovou funkcí dynamických webových stránek je, že můžete určit, co dělat na základě podmínek.</span><span class="sxs-lookup"><span data-stu-id="b397c-167">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="b397c-168">Nejběžnější způsob, jak to provést, je pomocí příkazu `If` (a volitelného příkazu `Else`).</span><span class="sxs-lookup"><span data-stu-id="b397c-168">The most common way to do this is with the `If` statement (and optional `Else` statement).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample9.vbhtml)]

<span data-ttu-id="b397c-169">Příkaz `If IsPost` je zkrácený způsob psaní `If IsPost = True`.</span><span class="sxs-lookup"><span data-stu-id="b397c-169">The statement `If IsPost` is a shorthand way of writing `If IsPost = True`.</span></span> <span data-ttu-id="b397c-170">Spolu s `If`mi příkazy existují různé způsoby, jak testovat podmínky, opakovat bloky kódu a tak dále, které jsou popsány dále v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="b397c-170">Along with `If` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="b397c-171">Výsledek zobrazený v prohlížeči (po kliknutí na **Odeslat**):</span><span class="sxs-lookup"><span data-stu-id="b397c-171">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor-Img6](introducing-razor-syntax-vb/_static/image7.jpg)

> [!TIP] 
> 
> <span data-ttu-id="b397c-173">**Metody GET a POST HTTP a vlastnost-post**</span><span class="sxs-lookup"><span data-stu-id="b397c-173">**HTTP GET and POST Methods and the IsPost Property**</span></span>
> 
> <span data-ttu-id="b397c-174">Protokol použitý pro webové stránky (HTTP) podporuje velmi omezený počet metod (&quot;&quot;ch operací), které se používají k provádění požadavků na server.</span><span class="sxs-lookup"><span data-stu-id="b397c-174">The protocol used for web pages (HTTP) supports a very limited number of methods (&quot;verbs&quot;) that are used to make requests to the server.</span></span> <span data-ttu-id="b397c-175">Dva nejběžnější jsou GET, které slouží ke čtení stránky a k odeslání příspěvku, který slouží k odeslání stránky.</span><span class="sxs-lookup"><span data-stu-id="b397c-175">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="b397c-176">Obecně platí, že uživatel poprvé požaduje stránku, stránka se požaduje pomocí GET.</span><span class="sxs-lookup"><span data-stu-id="b397c-176">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="b397c-177">Pokud uživatel vyplní formulář a klikne na tlačítko **Odeslat**, prohlížeč ODEŠLE požadavek post na server.</span><span class="sxs-lookup"><span data-stu-id="b397c-177">If the user fills in a form and then clicks **Submit**, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="b397c-178">Ve webovém programování je často užitečné zjistit, jestli se stránka požaduje jako GET nebo jako příspěvek, abyste věděli, jak stránku zpracovat.</span><span class="sxs-lookup"><span data-stu-id="b397c-178">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="b397c-179">Na webových stránkách ASP.NET můžete pomocí vlastnosti `IsPost` zjistit, jestli je požadavek GET nebo POST.</span><span class="sxs-lookup"><span data-stu-id="b397c-179">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="b397c-180">Pokud je žádost příspěvek, vlastnost `IsPost` vrátí hodnotu true a můžete provádět akce, jako je například čtení hodnot textových polí na formuláři.</span><span class="sxs-lookup"><span data-stu-id="b397c-180">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="b397c-181">V mnoha příkladech se dozvíte, jak stránku zpracovat odlišně v závislosti na hodnotě `IsPost`.</span><span class="sxs-lookup"><span data-stu-id="b397c-181">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>

## <a name="a-simple-code-example"></a><span data-ttu-id="b397c-182">Příklad jednoduchého kódu</span><span class="sxs-lookup"><span data-stu-id="b397c-182">A Simple Code Example</span></span>

<span data-ttu-id="b397c-183">Tento postup ukazuje, jak vytvořit stránku, která znázorňuje základní programovací techniky.</span><span class="sxs-lookup"><span data-stu-id="b397c-183">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="b397c-184">V tomto příkladu vytvoříte stránku, která umožní uživatelům zadat dvě čísla, pak je přidá a zobrazí výsledek.</span><span class="sxs-lookup"><span data-stu-id="b397c-184">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="b397c-185">V editoru vytvořte nový soubor a pojmenujte ho *AddNumbers. vbhtml*.</span><span class="sxs-lookup"><span data-stu-id="b397c-185">In your editor, create a new file and name it *AddNumbers.vbhtml*.</span></span>
2. <span data-ttu-id="b397c-186">Zkopírujte následující kód a označení na stránku a nahraďte cokoli již na stránce.</span><span class="sxs-lookup"><span data-stu-id="b397c-186">Copy the following code and markup into the page, replacing anything already in the page.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample10.vbhtml)]

    <span data-ttu-id="b397c-187">Tady je několik věcí, které můžete poznamenat:</span><span class="sxs-lookup"><span data-stu-id="b397c-187">Here are some things for you to note:</span></span>

    - <span data-ttu-id="b397c-188">`@` znak spustí první blok kódu na stránce a předá `totalMessage` proměnnou vloženou poblíž dolů.</span><span class="sxs-lookup"><span data-stu-id="b397c-188">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable embedded near the bottom.</span></span>
    - <span data-ttu-id="b397c-189">Blok v horní části stránky je uzavřený v `Code...End Code`.</span><span class="sxs-lookup"><span data-stu-id="b397c-189">The block at the top of the page is enclosed in `Code...End Code`.</span></span>
    - <span data-ttu-id="b397c-190">Proměnné `total`, `num1`, `num2`a `totalMessage` ukládají několik čísel a řetězce.</span><span class="sxs-lookup"><span data-stu-id="b397c-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="b397c-191">Literální řetězcová hodnota přiřazená k proměnné `totalMessage` je v dvojitých uvozovkách.</span><span class="sxs-lookup"><span data-stu-id="b397c-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="b397c-192">Vzhledem k tomu, že Visual Basic kód nerozlišuje velká a malá písmena, je-li proměnná `totalMessage` použita v dolní části stránky, musí její název odpovídat pouze pravopisu deklarace proměnné v horní části stránky.</span><span class="sxs-lookup"><span data-stu-id="b397c-192">Because Visual Basic code is not case sensitive, when the `totalMessage` variable is used near the bottom of the page, its name only needs to match the spelling of the variable declaration at the top of the page.</span></span> <span data-ttu-id="b397c-193">Záleží na velikosti písmen.</span><span class="sxs-lookup"><span data-stu-id="b397c-193">The casing doesn't matter.</span></span>
    - <span data-ttu-id="b397c-194">Výraz `num1.AsInt()` + `num2.AsInt()` ukazuje, jak pracovat s objekty a metodami.</span><span class="sxs-lookup"><span data-stu-id="b397c-194">The expression `num1.AsInt()` + `num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="b397c-195">Metoda `AsInt` u každé proměnné převede řetězec zadaný uživatelem na celé číslo (celé číslo), které lze přidat.</span><span class="sxs-lookup"><span data-stu-id="b397c-195">The `AsInt` method on each variable converts the string entered by a user to a whole number (an integer) that can be added.</span></span>
    - <span data-ttu-id="b397c-196">Značka `<form>` obsahuje atribut `method="post"`.</span><span class="sxs-lookup"><span data-stu-id="b397c-196">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="b397c-197">To určuje, že když uživatel klikne na **Přidat**, stránka se pošle na server pomocí metody HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="b397c-197">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="b397c-198">Po odeslání stránky se kód `If IsPost` vyhodnotí jako true a spustí se podmíněný kód a zobrazí se výsledek přidání čísel.</span><span class="sxs-lookup"><span data-stu-id="b397c-198">When the page is submitted, the code `If IsPost` evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="b397c-199">Uložte stránku a spusťte ji v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="b397c-199">Save the page and run it in a browser.</span></span> <span data-ttu-id="b397c-200">(Před spuštěním se ujistěte, že je stránka vybraná v pracovním prostoru **soubory** .) Zadejte dvě celá čísla a potom klikněte na tlačítko **Přidat** .</span><span class="sxs-lookup"><span data-stu-id="b397c-200">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span>

    ![Razor-Img7](introducing-razor-syntax-vb/_static/image8.jpg)

## <a name="visual-basic-language-and-syntax"></a><span data-ttu-id="b397c-202">Visual Basic jazyk a syntax</span><span class="sxs-lookup"><span data-stu-id="b397c-202">Visual Basic Language and Syntax</span></span>

<span data-ttu-id="b397c-203">Dříve jste viděli základní příklad, jak vytvořit webovou stránku ASP.NET a jak můžete přidat serverový kód do kódu HTML.</span><span class="sxs-lookup"><span data-stu-id="b397c-203">Earlier you saw a basic example of how to create an ASP.NET web page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="b397c-204">Tady se naučíte základy použití Visual Basic k zápisu kódu serveru ASP.NET pomocí syntaxe Razor &#8212; , která jsou pravidla pro programování jazyků.</span><span class="sxs-lookup"><span data-stu-id="b397c-204">Here you'll learn the basics of using Visual Basic to write ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="b397c-205">Pokud máte zkušenosti s programováním (zejména pokud jste použili C, C++, C#, Visual Basic nebo JavaScript), je většina věcí, kterou si přečtete, dobře známá.</span><span class="sxs-lookup"><span data-stu-id="b397c-205">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="b397c-206">Pravděpodobně budete potřebovat seznámení pouze s tím, jak je kód WebMatrix přidán do značek v souborech *. vbhtml* .</span><span class="sxs-lookup"><span data-stu-id="b397c-206">You'll probably need to familiarize yourself only with how WebMatrix code is added to markup in *.vbhtml* files.</span></span>

### <a id="BM_CombiningTextMarkupAndCode"></a><span data-ttu-id="b397c-207">Kombinování textu, značek a kódu v blocích kódu</span><span class="sxs-lookup"><span data-stu-id="b397c-207">Combining text, markup, and code in code blocks</span></span>

<span data-ttu-id="b397c-208">V blocích serverového kódu často budete chtít výstup textu a značky na stránku.</span><span class="sxs-lookup"><span data-stu-id="b397c-208">In server code blocks, you'll often want to output text and markup to the page.</span></span> <span data-ttu-id="b397c-209">Pokud blok kódu serveru obsahuje text, který není kód a místo toho by měl být vykreslen tak, jak je, ASP.NET musí být schopni tento text odlišit od kódu.</span><span class="sxs-lookup"><span data-stu-id="b397c-209">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="b397c-210">To lze provést několika způsoby.</span><span class="sxs-lookup"><span data-stu-id="b397c-210">There are several ways to do this.</span></span>

- <span data-ttu-id="b397c-211">Uzavřete text do elementu bloku HTML, jako je `<p></p>` nebo `<em></em>`:</span><span class="sxs-lookup"><span data-stu-id="b397c-211">Enclose the text in an HTML block element like `<p></p>` or `<em></em>`:</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample11.vbhtml)]

    <span data-ttu-id="b397c-212">Element HTML může obsahovat text, další prvky HTML a výrazy kódu serveru.</span><span class="sxs-lookup"><span data-stu-id="b397c-212">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="b397c-213">Když ASP.NET uvidí otevření značky HTML (například `<p>`), vykreslí vše prvek a jeho obsah tak, jak je, do prohlížeče (a přeloží výrazy kódu serveru).</span><span class="sxs-lookup"><span data-stu-id="b397c-213">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything the element and its content as is to the browser (and resolves the server-code expressions).</span></span>

- <span data-ttu-id="b397c-214">Použijte operátor `@:` nebo prvek `<text>`.</span><span class="sxs-lookup"><span data-stu-id="b397c-214">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="b397c-215">`@:` vytvoří výstup jednoho řádku obsahu obsahujícího prostý text nebo nespárované značky HTML. element `<text>` obklopuje více řádků do výstupu.</span><span class="sxs-lookup"><span data-stu-id="b397c-215">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="b397c-216">Tyto možnosti jsou užitečné, pokud nechcete vykreslit prvek HTML jako součást výstupu.</span><span class="sxs-lookup"><span data-stu-id="b397c-216">These options are useful when you don't want to render an HTML element as part of the output.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample12.vbhtml)]

    <span data-ttu-id="b397c-217">Následující příklad opakuje předchozí příklad, ale používá jednu dvojici `<text>` značek k uzavření textu, který se má vykreslit.</span><span class="sxs-lookup"><span data-stu-id="b397c-217">The following example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample13.vbhtml)]

    <span data-ttu-id="b397c-218">V následujícím příkladu jsou značky `<text>` a `</text>` uzavřeny tři řádky, všechny, které obsahují neuzavřený text a nespárované značky HTML (`<br />`), spolu s kódem serveru a odpovídajícími značkami HTML.</span><span class="sxs-lookup"><span data-stu-id="b397c-218">In the following example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="b397c-219">Znovu můžete také předcházet každý řádek jednotlivě pomocí operátoru `@:`; Jak funguje.</span><span class="sxs-lookup"><span data-stu-id="b397c-219">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample14.vbhtml)]

    > [!NOTE]
    > <span data-ttu-id="b397c-220">Při výstupu textu, jak je znázorněno v &#8212; této části pomocí elementu jazyka HTML, operátoru `@:` nebo elementu &#8212; `<text>` ASP.NET nekóduje výstup do kódu HTML.</span><span class="sxs-lookup"><span data-stu-id="b397c-220">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="b397c-221">(Jak bylo uvedeno dříve, ASP.NET zakóduje výstup výrazů serverového kódu a bloků serverového kódu, které jsou před `@`, s výjimkou zvláštních případů uvedených v této části.)</span><span class="sxs-lookup"><span data-stu-id="b397c-221">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="b397c-222">Typy</span><span class="sxs-lookup"><span data-stu-id="b397c-222">Whitespace</span></span>

<span data-ttu-id="b397c-223">Nadbytečné mezery v příkazu (a mimo řetězcový literál) neovlivňují příkaz:</span><span class="sxs-lookup"><span data-stu-id="b397c-223">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample15.vbhtml)]

### <a name="breaking-long-statements-into-multiple-lines"></a><span data-ttu-id="b397c-224">Rozdělení dlouhých příkazů na více řádků</span><span class="sxs-lookup"><span data-stu-id="b397c-224">Breaking long statements into multiple lines</span></span>

<span data-ttu-id="b397c-225">Příkaz dlouhého kódu můžete rozdělit na více řádků pomocí znaku podtržítka `_` (který se v Visual Basic označuje jako *znak pokračování*) po každém řádku kódu.</span><span class="sxs-lookup"><span data-stu-id="b397c-225">You can break a long code statement into multiple lines by using the underscore character `_` (which in Visual Basic is called the *continuation character*) after each line of code.</span></span> <span data-ttu-id="b397c-226">Chcete-li rozdělit příkaz na další řádek, na konci řádku přidejte mezeru a pak znak pokračování.</span><span class="sxs-lookup"><span data-stu-id="b397c-226">To break a statement onto the next line, at the end of the line add a space and then the continuation character.</span></span> <span data-ttu-id="b397c-227">Pokračujte v prohlášení na dalším řádku.</span><span class="sxs-lookup"><span data-stu-id="b397c-227">Continue the statement on the next line.</span></span> <span data-ttu-id="b397c-228">Příkazy lze zabalit do tolika řádků, kolik potřebujete ke zlepšení čitelnosti.</span><span class="sxs-lookup"><span data-stu-id="b397c-228">You can wrap statements onto as many lines as you need to improve readability.</span></span> <span data-ttu-id="b397c-229">Následující příkazy jsou stejné:</span><span class="sxs-lookup"><span data-stu-id="b397c-229">The following statements are the same:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample16.vbhtml)]

<span data-ttu-id="b397c-230">Nemůžete však obtékat čáru uprostřed řetězcového literálu.</span><span class="sxs-lookup"><span data-stu-id="b397c-230">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="b397c-231">Následující příklad nefunguje:</span><span class="sxs-lookup"><span data-stu-id="b397c-231">The following example doesn't work:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample17.vbhtml)]

<span data-ttu-id="b397c-232">Pro kombinování dlouhého řetězce, který se zalomí na více řádků, jako je výše uvedený kód, byste museli použít *operátor zřetězení* (`&`), který se zobrazí později v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="b397c-232">To combine a long string that wraps to multiple lines like the above code, you would need to use the *concatenation operator* (`&`), which you'll see later in this article.</span></span>

### <a name="code-comments"></a><span data-ttu-id="b397c-233">Komentáře ke kódu</span><span class="sxs-lookup"><span data-stu-id="b397c-233">Code comments</span></span>

<span data-ttu-id="b397c-234">Komentáře umožňují psát si poznámky pro sebe nebo jiné.</span><span class="sxs-lookup"><span data-stu-id="b397c-234">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="b397c-235">Komentáře syntaxe Razor jsou s předponou `@*` a končí `*@`.</span><span class="sxs-lookup"><span data-stu-id="b397c-235">Razor syntax comments are prefixed with `@*` and end with `*@`.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-vb/samples/sample18.cshtml)]

<span data-ttu-id="b397c-236">V rámci bloků kódu můžete použít komentáře syntaxe Razor, nebo můžete použít obyčejného znaku Visual Basic komentáře, což je jedna uvozovka (`'`) s předponou na každý řádek.</span><span class="sxs-lookup"><span data-stu-id="b397c-236">Within code blocks you can use the Razor syntax comments, or you can use ordinary Visual Basic comment character, which is a single quote (`'`) prefixed to each line.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample19.vbhtml)]

## <a name="variables"></a><span data-ttu-id="b397c-237">Proměnné</span><span class="sxs-lookup"><span data-stu-id="b397c-237">Variables</span></span>

<span data-ttu-id="b397c-238">Proměnná je pojmenovaný objekt, který slouží k ukládání dat.</span><span class="sxs-lookup"><span data-stu-id="b397c-238">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="b397c-239">Proměnné můžete pojmenovat cokoli, ale název musí začínat znakem abecedy a nesmí obsahovat mezery ani vyhrazené znaky.</span><span class="sxs-lookup"><span data-stu-id="b397c-239">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span> <span data-ttu-id="b397c-240">V Visual Basic, jak jste viděli dříve, Velká a malá písmena v názvu proměnné nezáleží na velikosti písmen.</span><span class="sxs-lookup"><span data-stu-id="b397c-240">In Visual Basic, as you saw earlier, the case of the letters in a variable name doesn't matter.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="b397c-241">Proměnné a datové typy</span><span class="sxs-lookup"><span data-stu-id="b397c-241">Variables and data types</span></span>

<span data-ttu-id="b397c-242">Proměnná může mít určitý datový typ, který označuje, jaký druh dat je uložený v proměnné.</span><span class="sxs-lookup"><span data-stu-id="b397c-242">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="b397c-243">Můžete mít řetězcové proměnné, které ukládají řetězcové hodnoty (například &quot;Hello World&quot;), celočíselné proměnné, které ukládají hodnoty s celými čísly (například 3 nebo 79), a proměnné data uchovávající hodnoty data v různých formátech (například 4/12/2012 nebo březen 2009).</span><span class="sxs-lookup"><span data-stu-id="b397c-243">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="b397c-244">A existuje mnoho dalších typů dat, které můžete použít.</span><span class="sxs-lookup"><span data-stu-id="b397c-244">And there are many other data types you can use.</span></span>

<span data-ttu-id="b397c-245">Nemusíte ale zadávat typ pro proměnnou.</span><span class="sxs-lookup"><span data-stu-id="b397c-245">However, you don't have to specify a type for a variable.</span></span> <span data-ttu-id="b397c-246">Ve většině případů ASP.NET může zjistit typ podle toho, jak se data v proměnné používají.</span><span class="sxs-lookup"><span data-stu-id="b397c-246">In most cases ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="b397c-247">(Někdy musíte zadat typ; uvidíte příklady, kde je to pravda.)</span><span class="sxs-lookup"><span data-stu-id="b397c-247">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="b397c-248">Chcete-li deklarovat proměnnou bez určení typu, použijte `Dim` plus název proměnné (např. `Dim myVar`).</span><span class="sxs-lookup"><span data-stu-id="b397c-248">To declare a variable without specifying a type, use `Dim` plus the variable name (for instance, `Dim myVar`).</span></span> <span data-ttu-id="b397c-249">Chcete-li deklarovat proměnnou s typem, použijte `Dim` plus název proměnné následovaný `As` a pak název typu (například `Dim myVar As String`).</span><span class="sxs-lookup"><span data-stu-id="b397c-249">To declare a variable with a type, use `Dim` plus the variable name, followed by `As` and then the type name (for instance, `Dim myVar As String`).</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample20.vbhtml)]

<span data-ttu-id="b397c-250">Následující příklad ukazuje některé vložené výrazy, které používají proměnné na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="b397c-250">The following example shows some inline expressions that use the variables in a web page.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample21.vbhtml)]

<span data-ttu-id="b397c-251">Výsledek zobrazený v prohlížeči:</span><span class="sxs-lookup"><span data-stu-id="b397c-251">The result displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-vb/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="b397c-253">Převod a testování datových typů</span><span class="sxs-lookup"><span data-stu-id="b397c-253">Converting and testing data types</span></span>

<span data-ttu-id="b397c-254">I když ASP.NET může obvykle určit datový typ automaticky, někdy to nemůže.</span><span class="sxs-lookup"><span data-stu-id="b397c-254">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="b397c-255">Proto může být nutné pomáhat s ASP.NETm při provádění explicitního převodu.</span><span class="sxs-lookup"><span data-stu-id="b397c-255">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="b397c-256">I v případě, že není nutné převést typy, někdy je vhodné otestovat a zjistit, se kterými typem dat pracujete.</span><span class="sxs-lookup"><span data-stu-id="b397c-256">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="b397c-257">Nejběžnějším případem je, že je nutné převést řetězec na jiný typ, jako je například na celé číslo nebo datum.</span><span class="sxs-lookup"><span data-stu-id="b397c-257">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="b397c-258">Následující příklad ukazuje typický případ, kdy je nutné převést řetězec na číslo.</span><span class="sxs-lookup"><span data-stu-id="b397c-258">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample22.vbhtml)]

<span data-ttu-id="b397c-259">Jako pravidlo se vstup uživatele dostane jako řetězce.</span><span class="sxs-lookup"><span data-stu-id="b397c-259">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="b397c-260">I když se uživateli zobrazí výzva k zadání čísla, a to i v případě, že zadali číslici, když se odešle vstup uživatele a přečtete ho v kódu, data jsou ve formátu řetězce.</span><span class="sxs-lookup"><span data-stu-id="b397c-260">Even if you've prompted the user to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="b397c-261">Proto je nutné převést řetězec na číslo.</span><span class="sxs-lookup"><span data-stu-id="b397c-261">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="b397c-262">Pokud se v příkladu pokusíte provést aritmetické operace s hodnotami bez jejich převádění, dojde k následující chybě, protože ASP.NET nemůže přidat dva řetězce:</span><span class="sxs-lookup"><span data-stu-id="b397c-262">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

`Cannot implicitly convert type 'string' to 'int'.`

<span data-ttu-id="b397c-263">Chcete-li převést hodnoty na celá čísla, zavolejte metodu `AsInt`.</span><span class="sxs-lookup"><span data-stu-id="b397c-263">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="b397c-264">Pokud je převod úspěšný, můžete čísla přidat.</span><span class="sxs-lookup"><span data-stu-id="b397c-264">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="b397c-265">V následující tabulce jsou uvedeny některé běžné metody převodu a testování pro proměnné.</span><span class="sxs-lookup"><span data-stu-id="b397c-265">The following table lists some common conversion and test methods for variables.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="b397c-266"><strong>Metoda</strong></span><span class="sxs-lookup"><span data-stu-id="b397c-266"><strong>Method</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="b397c-267"><strong>Popis</strong></span><span class="sxs-lookup"><span data-stu-id="b397c-267"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="b397c-268"><strong>Příklad</strong></span><span class="sxs-lookup"><span data-stu-id="b397c-268"><strong>Example</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
        <span data-ttu-id="b397c-269">Převede řetězec reprezentující celé číslo (například &quot;593&quot;) na celé číslo.</span><span class="sxs-lookup"><span data-stu-id="b397c-269">Converts a string that represents a whole number (like &quot;593&quot;) to an integer.</span></span>
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
        <span data-ttu-id="b397c-270">Převede řetězec jako &quot;true&quot; nebo &quot;false&quot; na typ Boolean.</span><span class="sxs-lookup"><span data-stu-id="b397c-270">Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
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
        <span data-ttu-id="b397c-271">Převede řetězec, který má hodnotu typu Decimal, například &quot;1,3&quot; nebo &quot;7,439&quot; na číslo s plovoucí desetinnou čárkou.</span><span class="sxs-lookup"><span data-stu-id="b397c-271">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
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
        <span data-ttu-id="b397c-272">Převede řetězec, který má hodnotu typu Decimal, například &quot;1,3&quot; nebo &quot;7,439&quot; na desetinné číslo.</span><span class="sxs-lookup"><span data-stu-id="b397c-272">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="b397c-273">(V ASP.NET je desetinné číslo přesnější než číslo s plovoucí desetinnou čárkou.)</span><span class="sxs-lookup"><span data-stu-id="b397c-273">(In ASP.NET, a decimal number is more precise than a floating-point number.)</span></span>
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
        <span data-ttu-id="b397c-274">Převede řetězec, který představuje hodnotu data a času na ASP.NET typ `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="b397c-274">Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
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
        <span data-ttu-id="b397c-275">Převede jakýkoli jiný datový typ na řetězec.</span><span class="sxs-lookup"><span data-stu-id="b397c-275">Converts any other data type to a string.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample28.vb)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a><span data-ttu-id="b397c-276">Operátory</span><span class="sxs-lookup"><span data-stu-id="b397c-276">Operators</span></span>

<span data-ttu-id="b397c-277">Operátor je klíčové slovo nebo znak, který oznamuje ASP.NET, jaký druh příkazu má být proveden ve výrazu.</span><span class="sxs-lookup"><span data-stu-id="b397c-277">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="b397c-278">Visual Basic podporuje mnoho operátorů, ale k zahájení vývoje webových stránek ASP.NET potřebujete jenom několik málo.</span><span class="sxs-lookup"><span data-stu-id="b397c-278">Visual Basic supports many operators, but you only need to recognize a few to get started developing ASP.NET web pages.</span></span> <span data-ttu-id="b397c-279">Následující tabulka shrnuje nejběžnější operátory.</span><span class="sxs-lookup"><span data-stu-id="b397c-279">The following table summarizes the most common operators.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="b397c-280"><strong>Podnikatel</strong></span><span class="sxs-lookup"><span data-stu-id="b397c-280"><strong>Operator</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="b397c-281"><strong>Popis</strong></span><span class="sxs-lookup"><span data-stu-id="b397c-281"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
        <span data-ttu-id="b397c-282"><strong>Příklady</strong></span><span class="sxs-lookup"><span data-stu-id="b397c-282"><strong>Examples</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `+ - * /`
    :::column-end:::
    :::column:::
        <span data-ttu-id="b397c-283">Matematické operátory používané v numerických výrazech.</span><span class="sxs-lookup"><span data-stu-id="b397c-283">Math operators used in numerical expressions.</span></span>
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
        <span data-ttu-id="b397c-284">Přiřazení a rovnost.</span><span class="sxs-lookup"><span data-stu-id="b397c-284">Assignment and equality.</span></span> <span data-ttu-id="b397c-285">V závislosti na kontextu přiřadí hodnotu na pravé straně příkazu objektu na levé straně nebo ověří hodnoty rovnosti.</span><span class="sxs-lookup"><span data-stu-id="b397c-285">Depending on context, either assigns the value on the right side of a statement to the object on the left side, or checks the values for equality.</span></span>
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
        <span data-ttu-id="b397c-286">Nerovnost.</span><span class="sxs-lookup"><span data-stu-id="b397c-286">Inequality.</span></span> <span data-ttu-id="b397c-287">Vrátí `True`, pokud se hodnoty neshodují.</span><span class="sxs-lookup"><span data-stu-id="b397c-287">Returns `True` if the values are not equal.</span></span>
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
        <span data-ttu-id="b397c-288">Menší než, větší než, menší nebo rovno, a větší nebo rovno.</span><span class="sxs-lookup"><span data-stu-id="b397c-288">Less than, greater than, less than or equal, and greater than or equal.</span></span>
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
        <span data-ttu-id="b397c-289">Zřetězení, které se používá k spojování řetězců.</span><span class="sxs-lookup"><span data-stu-id="b397c-289">Concatenation, which is used to join strings.</span></span>
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
        <span data-ttu-id="b397c-290">Operátory přírůstku a snížení, které přidají a odečtou 1 (v uvedeném pořadí) z proměnné.</span><span class="sxs-lookup"><span data-stu-id="b397c-290">The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
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
        <span data-ttu-id="b397c-291">Tečka.</span><span class="sxs-lookup"><span data-stu-id="b397c-291">Dot.</span></span> <span data-ttu-id="b397c-292">Slouží k rozlišení objektů a jejich vlastností a metod.</span><span class="sxs-lookup"><span data-stu-id="b397c-292">Used to distinguish objects and their properties and methods.</span></span>
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
        <span data-ttu-id="b397c-293">Závorky.</span><span class="sxs-lookup"><span data-stu-id="b397c-293">Parentheses.</span></span> <span data-ttu-id="b397c-294">Slouží k seskupení výrazů, k předání parametrů metodám a k přístupu ke členům polí a kolekcí.</span><span class="sxs-lookup"><span data-stu-id="b397c-294">Used to group expressions, to pass parameters to methods, and to access members of arrays and collections.</span></span>
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
        <span data-ttu-id="b397c-295">Mění.</span><span class="sxs-lookup"><span data-stu-id="b397c-295">Not.</span></span> <span data-ttu-id="b397c-296">Obrátí hodnotu true na false a naopak.</span><span class="sxs-lookup"><span data-stu-id="b397c-296">Reverses a true value to false and vice versa.</span></span> <span data-ttu-id="b397c-297">Obvykle se používá jako zkrácený způsob testování pro `False` (tj. není-li `True`).</span><span class="sxs-lookup"><span data-stu-id="b397c-297">Typically used as a shorthand way to test for `False` (that is, for not `True`).</span></span>
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
        <span data-ttu-id="b397c-298">Logický operátor AND a OR, který se používá k propojení podmínek.</span><span class="sxs-lookup"><span data-stu-id="b397c-298">Logical AND and OR, which are used to link conditions together.</span></span>
    :::column-end:::
    :::column:::
        [!code-vb[Main](introducing-razor-syntax-vb/samples/sample38.vb)]
    :::column-end:::
:::row-end:::

## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="b397c-299">Práce s cestami k souborům a složkám v kódu</span><span class="sxs-lookup"><span data-stu-id="b397c-299">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="b397c-300">V kódu často budete pracovat s cestami k souborům a složkám.</span><span class="sxs-lookup"><span data-stu-id="b397c-300">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="b397c-301">Tady je příklad fyzické struktury složek pro web, jak se může zobrazit na vašem vývojovém počítači:</span><span class="sxs-lookup"><span data-stu-id="b397c-301">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="b397c-302">Tady jsou některé důležité informace o adresách URL a cestách:</span><span class="sxs-lookup"><span data-stu-id="b397c-302">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="b397c-303">Adresa URL začíná buď s názvem domény (`http://www.example.com`), nebo s názvem serveru (`http://localhost`, `http://mycomputer`).</span><span class="sxs-lookup"><span data-stu-id="b397c-303">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="b397c-304">Adresa URL odpovídá fyzické cestě na hostitelském počítači.</span><span class="sxs-lookup"><span data-stu-id="b397c-304">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="b397c-305">`http://myserver` například může odpovídat složce *C:\websites\mywebsite* na serveru.</span><span class="sxs-lookup"><span data-stu-id="b397c-305">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="b397c-306">Virtuální cesta je zkrácený pro reprezentaci cest v kódu bez nutnosti zadat úplnou cestu.</span><span class="sxs-lookup"><span data-stu-id="b397c-306">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="b397c-307">Obsahuje část adresy URL, která následuje za názvem domény nebo serveru.</span><span class="sxs-lookup"><span data-stu-id="b397c-307">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="b397c-308">Pokud používáte virtuální cesty, můžete svůj kód přesunout do jiné domény nebo serveru, aniž byste museli cesty aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="b397c-308">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="b397c-309">Tady je příklad, který vám pomůže pochopit rozdíly:</span><span class="sxs-lookup"><span data-stu-id="b397c-309">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="b397c-310">Úplná adresa URL</span><span class="sxs-lookup"><span data-stu-id="b397c-310">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="b397c-311">Název serveru</span><span class="sxs-lookup"><span data-stu-id="b397c-311">Server name</span></span> | <span data-ttu-id="b397c-312">*mycompanyserver*</span><span class="sxs-lookup"><span data-stu-id="b397c-312">*mycompanyserver*</span></span> |
| <span data-ttu-id="b397c-313">Virtuální cesta</span><span class="sxs-lookup"><span data-stu-id="b397c-313">Virtual path</span></span> | <span data-ttu-id="b397c-314">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="b397c-314">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="b397c-315">Fyzická cesta</span><span class="sxs-lookup"><span data-stu-id="b397c-315">Physical path</span></span> | <span data-ttu-id="b397c-316">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="b397c-316">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="b397c-317">Virtuální kořenový adresář je/, stejně jako kořenový adresář vaší jednotky C:.</span><span class="sxs-lookup"><span data-stu-id="b397c-317">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="b397c-318">(Cesty k virtuálním složkám vždycky používají lomítka.) Virtuální cesta ke složce nemusí mít stejný název jako fyzická složka; může to být alias.</span><span class="sxs-lookup"><span data-stu-id="b397c-318">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="b397c-319">(Na provozních serverech se virtuální cesta zřídka shoduje s přesnou fyzickou cestou.)</span><span class="sxs-lookup"><span data-stu-id="b397c-319">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="b397c-320">Když pracujete se soubory a složkami v kódu, někdy potřebujete odkazovat na fyzickou cestu a někdy na virtuální cestu v závislosti na objektech, se kterými pracujete.</span><span class="sxs-lookup"><span data-stu-id="b397c-320">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="b397c-321">ASP.NET poskytuje tyto nástroje pro práci s cestami k souborům a složkám v kódu: metoda `Server.MapPath` a operátor `~` a metoda `Href`.</span><span class="sxs-lookup"><span data-stu-id="b397c-321">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="b397c-322">Převod virtuálních na fyzické cesty: Metoda Server. MapPath</span><span class="sxs-lookup"><span data-stu-id="b397c-322">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="b397c-323">Metoda `Server.MapPath` Převede virtuální cestu (například */Default.cshtml*) na absolutní fyzickou cestu (například *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="b397c-323">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="b397c-324">Tuto metodu použijete kdykoli, když potřebujete úplnou fyzickou cestu.</span><span class="sxs-lookup"><span data-stu-id="b397c-324">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="b397c-325">Typickým příkladem je, že načítáte nebo píšete textový soubor nebo soubor obrázku na webovém serveru.</span><span class="sxs-lookup"><span data-stu-id="b397c-325">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="b397c-326">Obvykle neznáte absolutní fyzickou cestu k webu na serveru hostujícího webu, takže tato metoda může převést cestu, kterou znáte – virtuální cestu – k odpovídající cestě na serveru za vás.</span><span class="sxs-lookup"><span data-stu-id="b397c-326">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="b397c-327">Do metody předáte virtuální cestu k souboru nebo složce a vrátíte fyzickou cestu:</span><span class="sxs-lookup"><span data-stu-id="b397c-327">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample39.vbhtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="b397c-328">Odkazování na virtuální kořenový adresář: operátor ~ a metoda href</span><span class="sxs-lookup"><span data-stu-id="b397c-328">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="b397c-329">V souboru *. cshtml* nebo *. vbhtml* můžete odkazovat na virtuální kořenovou cestu pomocí operátoru `~`.</span><span class="sxs-lookup"><span data-stu-id="b397c-329">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="b397c-330">To je velmi užitečné, protože můžete přesouvat stránky v lokalitě a jakékoli odkazy, které obsahují na jiné stránky, nebudou přerušeny.</span><span class="sxs-lookup"><span data-stu-id="b397c-330">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="b397c-331">K dispozici je také užitečné v případě, že jste web někdy přesunuli do jiného umístění.</span><span class="sxs-lookup"><span data-stu-id="b397c-331">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="b397c-332">Zde je několik příkladů:</span><span class="sxs-lookup"><span data-stu-id="b397c-332">Here are some examples:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample40.vbhtml)]

<span data-ttu-id="b397c-333">Pokud je web `http://myserver/myapp`, v takovém případě bude ASP.NET považovat tyto cesty při spuštění stránky:</span><span class="sxs-lookup"><span data-stu-id="b397c-333">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="b397c-334">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="b397c-334">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="b397c-335">`myStyleSheet`: `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="b397c-335">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="b397c-336">(Tyto cesty ve skutečnosti neuvidíte jako hodnoty proměnné, ale ASP.NET je bude považovat za to, co byly.)</span><span class="sxs-lookup"><span data-stu-id="b397c-336">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="b397c-337">Operátor `~` lze použít jak v kódu serveru (jak je uvedeno výše), tak v označení, například takto:</span><span class="sxs-lookup"><span data-stu-id="b397c-337">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-vb/samples/sample41.html)]

<span data-ttu-id="b397c-338">V kódu se používá operátor `~` k vytváření cest k prostředkům, jako jsou soubory obrázků, jiné webové stránky a soubory CSS.</span><span class="sxs-lookup"><span data-stu-id="b397c-338">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="b397c-339">Po spuštění stránky ASP.NET vyhledá stránku (kód i kód) a přeloží všechny `~` odkazy na příslušnou cestu.</span><span class="sxs-lookup"><span data-stu-id="b397c-339">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="b397c-340">Podmíněná logika a smyčky</span><span class="sxs-lookup"><span data-stu-id="b397c-340">Conditional Logic and Loops</span></span>

<span data-ttu-id="b397c-341">Kód serveru ASP.NET vám umožňuje provádět úlohy na základě podmínek a napsat kód, který opakuje příkazy, a to tak, že se kód spouštějí smyčkou, a to podle určitého počtu.</span><span class="sxs-lookup"><span data-stu-id="b397c-341">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="b397c-342">Podmínky testování</span><span class="sxs-lookup"><span data-stu-id="b397c-342">Testing conditions</span></span>

<span data-ttu-id="b397c-343">Chcete-li otestovat jednoduchou podmínku, použijte příkaz `If...Then`, který vrací `True` nebo `False` na základě testu, který zadáte:</span><span class="sxs-lookup"><span data-stu-id="b397c-343">To test a simple condition you use the `If...Then` statement, which returns `True` or `False` based on a test you specify:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample42.vbhtml)]

<span data-ttu-id="b397c-344">Klíčové slovo `If` spustí blok.</span><span class="sxs-lookup"><span data-stu-id="b397c-344">The `If` keyword starts a block.</span></span> <span data-ttu-id="b397c-345">Skutečný test (podmínka) následuje za klíčovým slovem `If` a vrátí hodnotu true nebo false.</span><span class="sxs-lookup"><span data-stu-id="b397c-345">The actual test (condition) follows the `If` keyword and returns true or false.</span></span> <span data-ttu-id="b397c-346">Příkaz `If` končí na `Then`.</span><span class="sxs-lookup"><span data-stu-id="b397c-346">The `If` statement ends with `Then`.</span></span> <span data-ttu-id="b397c-347">Příkazy, které se spustí, pokud je test pravdivý, je uzavřený `If` a `End If`.</span><span class="sxs-lookup"><span data-stu-id="b397c-347">The statements that will run if the test is true are enclosed by `If` and `End If`.</span></span> <span data-ttu-id="b397c-348">Příkaz `If` může zahrnovat blok `Else`, který určuje příkazy, které se mají spustit, pokud je podmínka nepravdivá:</span><span class="sxs-lookup"><span data-stu-id="b397c-348">An `If` statement can include an `Else` block that specifies statements to run if the condition is false:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample43.vbhtml)]

<span data-ttu-id="b397c-349">Pokud příkaz `If` spustí blok kódu, nemusíte používat normální příkazy `Code...End Code` k zahrnutí bloků.</span><span class="sxs-lookup"><span data-stu-id="b397c-349">If an `If` statement starts a code block, you don't have to use the normal `Code...End Code` statements to include the blocks.</span></span> <span data-ttu-id="b397c-350">Do bloku můžete přidat pouze `@` a bude fungovat.</span><span class="sxs-lookup"><span data-stu-id="b397c-350">You can just add `@` to the block, and it will work.</span></span> <span data-ttu-id="b397c-351">Tento přístup funguje s `If` a dalšími Visual Basic programovací klíčová slova, která následují bloky kódu, včetně `For`, `For Each`, `Do While`atd.</span><span class="sxs-lookup"><span data-stu-id="b397c-351">This approach works with `If` as well as other Visual Basic programming keywords that are followed by code blocks, including `For`, `For Each`, `Do While`, etc.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample44.vbhtml)]

<span data-ttu-id="b397c-352">Pomocí jednoho nebo více `ElseIf`ch bloků můžete přidat více podmínek:</span><span class="sxs-lookup"><span data-stu-id="b397c-352">You can add multiple conditions using one or more `ElseIf` blocks:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample45.vbhtml)]

<span data-ttu-id="b397c-353">V tomto příkladu, pokud není první podmínka v `If`ovém bloku pravdivá, je zaškrtnuta podmínka `ElseIf`.</span><span class="sxs-lookup"><span data-stu-id="b397c-353">In this example, if the first condition in the `If` block is not true, the `ElseIf` condition is checked.</span></span> <span data-ttu-id="b397c-354">Pokud je tato podmínka splněna, jsou provedeny příkazy v bloku `ElseIf`.</span><span class="sxs-lookup"><span data-stu-id="b397c-354">If that condition is met, the statements in the `ElseIf` block are executed.</span></span> <span data-ttu-id="b397c-355">Pokud není splněna žádná z podmínek, jsou provedeny příkazy v bloku `Else`.</span><span class="sxs-lookup"><span data-stu-id="b397c-355">If none of the conditions are met, the statements in the `Else` block are executed.</span></span> <span data-ttu-id="b397c-356">Můžete přidat libovolný počet bloků `ElseIf` a potom zavřít s `Else` bloku jako &quot;vše ostatní&quot; podmínka.</span><span class="sxs-lookup"><span data-stu-id="b397c-356">You can add any number of `ElseIf` blocks, and then close with an `Else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="b397c-357">K otestování velkého počtu podmínek použijte `Select Case` blok:</span><span class="sxs-lookup"><span data-stu-id="b397c-357">To test a large number of conditions, use a `Select Case` block:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample46.vbhtml)]

<span data-ttu-id="b397c-358">Testovaná hodnota je v závorkách (v příkladu proměnné weekday).</span><span class="sxs-lookup"><span data-stu-id="b397c-358">The value to test is in parentheses (in the example, the weekday variable).</span></span> <span data-ttu-id="b397c-359">Každý jednotlivý test používá příkaz `Case`, který obsahuje hodnotu.</span><span class="sxs-lookup"><span data-stu-id="b397c-359">Each individual test uses a `Case` statement that lists a value.</span></span> <span data-ttu-id="b397c-360">Je-li hodnota příkazu `Case` shodná s testovací hodnotou, je proveden kód v tomto bloku `Case`.</span><span class="sxs-lookup"><span data-stu-id="b397c-360">If the value of a `Case` statement matches the test value, the code in that `Case` block is executed.</span></span>

<span data-ttu-id="b397c-361">Výsledek posledního dvou podmíněných bloků zobrazených v prohlížeči:</span><span class="sxs-lookup"><span data-stu-id="b397c-361">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor – Img10](introducing-razor-syntax-vb/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="b397c-363">Kód smyčky</span><span class="sxs-lookup"><span data-stu-id="b397c-363">Looping code</span></span>

<span data-ttu-id="b397c-364">Často je třeba spouštět stejné příkazy opakovaně.</span><span class="sxs-lookup"><span data-stu-id="b397c-364">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="b397c-365">Provedete to pomocí smyčky.</span><span class="sxs-lookup"><span data-stu-id="b397c-365">You do this by looping.</span></span> <span data-ttu-id="b397c-366">Například často spustíte stejné příkazy pro každou položku v kolekci dat.</span><span class="sxs-lookup"><span data-stu-id="b397c-366">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="b397c-367">Pokud víte přesně, kolikrát chcete cyklovat, můžete použít smyčku `For`.</span><span class="sxs-lookup"><span data-stu-id="b397c-367">If you know exactly how many times you want to loop, you can use a `For` loop.</span></span> <span data-ttu-id="b397c-368">Tento druh smyčky je zvláště užitečný pro inventarizaci a počítání:</span><span class="sxs-lookup"><span data-stu-id="b397c-368">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample47.vbhtml)]

<span data-ttu-id="b397c-369">Smyčka začíná klíčovým slovem `For` následovanými třemi prvky:</span><span class="sxs-lookup"><span data-stu-id="b397c-369">The loop begins with the `For` keyword, followed by three elements:</span></span>

- <span data-ttu-id="b397c-370">Ihned po příkazu `For` deklarujete proměnnou čítače (nemusíte používat `Dim`) a pak určíte rozsah, jako v `i = 10 to 20`.</span><span class="sxs-lookup"><span data-stu-id="b397c-370">Immediately after the `For` statement, you declare a counter variable (you don't have to use `Dim`) and then indicate the range, as in `i = 10 to 20`.</span></span> <span data-ttu-id="b397c-371">To znamená, že proměnná `i` začne počítat 10 a pokračovat, dokud nedosáhne 20 (včetně).</span><span class="sxs-lookup"><span data-stu-id="b397c-371">This means the variable `i` will start counting at 10 and continue until it reaches 20 (inclusive).</span></span>
- <span data-ttu-id="b397c-372">Mezi příkazy `For` a `Next` je obsah bloku.</span><span class="sxs-lookup"><span data-stu-id="b397c-372">Between the `For` and `Next` statements is the content of the block.</span></span> <span data-ttu-id="b397c-373">To může obsahovat jeden nebo více příkazů kódu, které se spouštějí s každou smyčkou.</span><span class="sxs-lookup"><span data-stu-id="b397c-373">This can contain one or more code statements that execute with each loop.</span></span>
- <span data-ttu-id="b397c-374">Příkaz `Next i` ukončí smyčku.</span><span class="sxs-lookup"><span data-stu-id="b397c-374">The `Next i` statement ends the loop.</span></span> <span data-ttu-id="b397c-375">Zvýší hodnotu čítače a spustí další iteraci smyčky.</span><span class="sxs-lookup"><span data-stu-id="b397c-375">It increments the counter and starts the next iteration of the loop.</span></span>

<span data-ttu-id="b397c-376">Řádek kódu mezi `For` a `Next` řádky obsahuje kód, který se spustí pro každou iteraci smyčky.</span><span class="sxs-lookup"><span data-stu-id="b397c-376">The line of code between the `For` and `Next` lines contains the code that runs for each iteration of the loop.</span></span> <span data-ttu-id="b397c-377">Kód vytvoří nový odstavec (`<p>` element) pokaždé a přidá řádek do výstupu a zobrazí hodnotu i (čítač).</span><span class="sxs-lookup"><span data-stu-id="b397c-377">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of i (the counter).</span></span> <span data-ttu-id="b397c-378">Když spustíte tuto stránku, v příkladu se vytvoří 11 řádků, ve kterých se zobrazí výstup, a text na každém řádku, který označuje číslo položky.</span><span class="sxs-lookup"><span data-stu-id="b397c-378">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-vb/_static/image11.jpg)

<span data-ttu-id="b397c-380">Pokud pracujete s kolekcí nebo polem, často používáte smyčku `For Each`.</span><span class="sxs-lookup"><span data-stu-id="b397c-380">If you're working with a collection or array, you often use a `For Each` loop.</span></span> <span data-ttu-id="b397c-381">Kolekce je skupina podobných objektů a smyčka `For Each` umožňuje provádět úlohy na každé položce v kolekci.</span><span class="sxs-lookup"><span data-stu-id="b397c-381">A collection is a group of similar objects, and the `For Each` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="b397c-382">Tento typ smyčky je vhodný pro kolekce, protože na rozdíl od `For` smyčky nemusíte zvyšovat čítač nebo nastavit limit.</span><span class="sxs-lookup"><span data-stu-id="b397c-382">This type of loop is convenient for collections, because unlike a `For` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="b397c-383">Místo toho kód smyčky `For Each` jednoduše projde přes kolekci, dokud není dokončena.</span><span class="sxs-lookup"><span data-stu-id="b397c-383">Instead, the `For Each` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="b397c-384">Tento příklad vrátí položky v kolekci `Request.ServerVariables` (které obsahují informace o vašem webovém serveru).</span><span class="sxs-lookup"><span data-stu-id="b397c-384">This example returns the items in the `Request.ServerVariables` collection (which contains information about your web server).</span></span> <span data-ttu-id="b397c-385">Používá smyčku `For Each` k zobrazení názvu každé položky vytvořením nového prvku `<li>` v seznamu s odrážkami HTML.</span><span class="sxs-lookup"><span data-stu-id="b397c-385">It uses a `For Each` loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample48.vbhtml)]

<span data-ttu-id="b397c-386">Za klíčovým slovem `For Each` následuje proměnná, která představuje jednu položku v kolekci (v příkladu `myItem`) následovanou klíčovým slovem `In` následovaný kolekcí, kterou chcete procyklovat.</span><span class="sxs-lookup"><span data-stu-id="b397c-386">The `For Each` keyword is followed by a variable that represents a single item in the collection (in the example, `myItem`), followed by the `In` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="b397c-387">V těle `For Each` smyčky můžete k aktuální položce přistupovat pomocí proměnné, kterou jste předtím deklarovali.</span><span class="sxs-lookup"><span data-stu-id="b397c-387">In the body of the `For Each` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-vb/_static/image12.jpg)

<span data-ttu-id="b397c-389">Chcete-li vytvořit obecnější smyčku pro účely, použijte příkaz `Do While`:</span><span class="sxs-lookup"><span data-stu-id="b397c-389">To create a more general-purpose loop, use the `Do While` statement:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample49.vbhtml)]

<span data-ttu-id="b397c-390">Tato smyčka začíná klíčovým slovem `Do While` následovaným podmínkou, následovanou blokem, který se má opakovat.</span><span class="sxs-lookup"><span data-stu-id="b397c-390">This loop begins with the `Do While` keyword, followed by a condition, followed by the block to repeat.</span></span> <span data-ttu-id="b397c-391">Smyčky typicky přidávají (přidávají do) nebo snižují (odečtou z) proměnnou nebo objekt, který se používá pro počítání.</span><span class="sxs-lookup"><span data-stu-id="b397c-391">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="b397c-392">V příkladu operátor `+=` přidá 1 k hodnotě proměnné pokaždé, když se smyčka spustí.</span><span class="sxs-lookup"><span data-stu-id="b397c-392">In the example, the `+=` operator adds 1 to the value of a variable each time the loop runs.</span></span> <span data-ttu-id="b397c-393">(Chcete-li snížit proměnnou ve smyčce, která počítá dolů, použijte operátor snížení `-=`.)</span><span class="sxs-lookup"><span data-stu-id="b397c-393">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`.)</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="b397c-394">Objekty a kolekce</span><span class="sxs-lookup"><span data-stu-id="b397c-394">Objects and Collections</span></span>

<span data-ttu-id="b397c-395">Skoro všechno na webu ASP.NET je objekt, včetně samotné webové stránky.</span><span class="sxs-lookup"><span data-stu-id="b397c-395">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="b397c-396">Tato část popisuje některé důležité objekty, se kterými se často pracujete ve vašem kódu.</span><span class="sxs-lookup"><span data-stu-id="b397c-396">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="b397c-397">Objekty stránky</span><span class="sxs-lookup"><span data-stu-id="b397c-397">Page objects</span></span>

<span data-ttu-id="b397c-398">Nejzákladnější objekt v ASP.NET je stránka.</span><span class="sxs-lookup"><span data-stu-id="b397c-398">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="b397c-399">K vlastnostem objektu stránky můžete přistupovat přímo bez jakéhokoli opravňujícího objektu.</span><span class="sxs-lookup"><span data-stu-id="b397c-399">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="b397c-400">Následující kód Získá cestu k souboru stránky pomocí objektu `Request` stránky:</span><span class="sxs-lookup"><span data-stu-id="b397c-400">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample50.vbhtml)]

<span data-ttu-id="b397c-401">Pomocí vlastností objektu `Page` můžete získat velké množství informací, například:</span><span class="sxs-lookup"><span data-stu-id="b397c-401">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="b397c-402">`Request`.</span><span class="sxs-lookup"><span data-stu-id="b397c-402">`Request`.</span></span> <span data-ttu-id="b397c-403">Jak už jste viděli, jedná se o kolekci informací o aktuální žádosti, včetně typu prohlížeče, který požadavek odeslal, adresu URL stránky, identitu uživatele atd.</span><span class="sxs-lookup"><span data-stu-id="b397c-403">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="b397c-404">`Response`.</span><span class="sxs-lookup"><span data-stu-id="b397c-404">`Response`.</span></span> <span data-ttu-id="b397c-405">Toto je kolekce informací o odpovědi (stránky), která se odešle do prohlížeče, když je kód serveru spuštěný.</span><span class="sxs-lookup"><span data-stu-id="b397c-405">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="b397c-406">Tuto vlastnost můžete například použít k zápisu informací do odpovědi.</span><span class="sxs-lookup"><span data-stu-id="b397c-406">For example, you can use this property to write information into the response.</span></span>

    [!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample51.vbhtml)]

### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="b397c-407">Objekty kolekce (pole a slovníky)</span><span class="sxs-lookup"><span data-stu-id="b397c-407">Collection objects (arrays and dictionaries)</span></span>

<span data-ttu-id="b397c-408">Kolekce je skupina objektů stejného typu, například kolekce `Customer` objektů z databáze.</span><span class="sxs-lookup"><span data-stu-id="b397c-408">A collection is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="b397c-409">ASP.NET obsahuje mnoho předdefinovaných kolekcí, jako je kolekce `Request.Files`.</span><span class="sxs-lookup"><span data-stu-id="b397c-409">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="b397c-410">Často budete pracovat s daty v kolekcích.</span><span class="sxs-lookup"><span data-stu-id="b397c-410">You'll often work with data in collections.</span></span> <span data-ttu-id="b397c-411">Dva společné typy kolekcí jsou *pole* a *slovník*.</span><span class="sxs-lookup"><span data-stu-id="b397c-411">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="b397c-412">Pole je užitečné, pokud chcete uložit kolekci podobných položek, ale nechcete vytvořit samostatnou proměnnou pro uchování každé položky:</span><span class="sxs-lookup"><span data-stu-id="b397c-412">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample52.vbhtml)]

<span data-ttu-id="b397c-413">Pomocí polí deklarujete konkrétní datový typ, například `String`, `Integer`nebo `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="b397c-413">With arrays, you declare a specific data type, such as `String`, `Integer`, or `DateTime`.</span></span> <span data-ttu-id="b397c-414">Chcete-li označit, že proměnná může obsahovat pole, přidejte do názvu proměnné v deklaraci (například `Dim myVar() As String`) závorky.</span><span class="sxs-lookup"><span data-stu-id="b397c-414">To indicate that the variable can contain an array, you add parentheses to the variable name in the declaration (such as `Dim myVar() As String`).</span></span> <span data-ttu-id="b397c-415">K položkám v poli můžete přistupovat pomocí jejich pozice (indexu) nebo pomocí příkazu `For Each`.</span><span class="sxs-lookup"><span data-stu-id="b397c-415">You can access items in an array using their position (index) or by using the `For Each` statement.</span></span> <span data-ttu-id="b397c-416">Indexy polí jsou počítány od &#8212; nuly, tj. první položka je na pozici 0, druhá položka je na pozici 1 atd.</span><span class="sxs-lookup"><span data-stu-id="b397c-416">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample53.vbhtml)]

<span data-ttu-id="b397c-417">Počet položek v poli můžete určit získáním jeho vlastnosti `Length`.</span><span class="sxs-lookup"><span data-stu-id="b397c-417">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="b397c-418">Chcete-li získat pozici konkrétní položky v poli (tj. pro hledání v poli), použijte metodu `Array.IndexOf`.</span><span class="sxs-lookup"><span data-stu-id="b397c-418">To get the position of a specific item in the array (that is, to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="b397c-419">Můžete také provést akce, jako je vrácení obsahu pole (`Array.Reverse` metody) nebo řazení obsahu (metoda `Array.Sort`).</span><span class="sxs-lookup"><span data-stu-id="b397c-419">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="b397c-420">Výstup kódu řetězcového pole zobrazeného v prohlížeči:</span><span class="sxs-lookup"><span data-stu-id="b397c-420">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-vb/_static/image13.jpg)

<span data-ttu-id="b397c-422">Slovník je kolekce párů klíč/hodnota, kde zadáte klíč (nebo název) pro nastavení nebo načtení příslušné hodnoty:</span><span class="sxs-lookup"><span data-stu-id="b397c-422">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample54.vbhtml)]

<span data-ttu-id="b397c-423">Chcete-li vytvořit slovník, použijte klíčové slovo `New` pro indikaci, že vytváříte nový objekt `Dictionary`.</span><span class="sxs-lookup"><span data-stu-id="b397c-423">To create a dictionary, you use the `New` keyword to indicate that you're creating a new `Dictionary` object.</span></span> <span data-ttu-id="b397c-424">K proměnné můžete přiřadit slovník pomocí klíčového slova `Dim`.</span><span class="sxs-lookup"><span data-stu-id="b397c-424">You can assign a dictionary to a variable using the `Dim` keyword.</span></span> <span data-ttu-id="b397c-425">Datové typy položek ve slovníku označíte pomocí závorek (`( )`).</span><span class="sxs-lookup"><span data-stu-id="b397c-425">You indicate the data types of the items in the dictionary using parentheses ( `( )` ).</span></span> <span data-ttu-id="b397c-426">Na konci deklarace je nutné přidat další dvojici závorek, protože se jedná o metodu, která vytvoří nový slovník.</span><span class="sxs-lookup"><span data-stu-id="b397c-426">At the end of the declaration, you must add another pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="b397c-427">Chcete-li přidat položky do slovníku, můžete zavolat metodu `Add` proměnné Dictionary (`myScores` v tomto případě) a poté zadat klíč a hodnotu.</span><span class="sxs-lookup"><span data-stu-id="b397c-427">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="b397c-428">Alternativně můžete pomocí závorek označit klíč a provést jednoduché přiřazení, jako v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="b397c-428">Alternatively, you can use parentheses to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample55.vbhtml)]

<span data-ttu-id="b397c-429">Pokud chcete získat hodnotu ze slovníku, zadáte klíč v závorkách:</span><span class="sxs-lookup"><span data-stu-id="b397c-429">To get a value from the dictionary, you specify the key in parentheses:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample56.vbhtml)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="b397c-430">Volání metod s parametry</span><span class="sxs-lookup"><span data-stu-id="b397c-430">Calling Methods with Parameters</span></span>

<span data-ttu-id="b397c-431">Jak jste viděli výše v tomto článku, objekty, které program mají, mají metody.</span><span class="sxs-lookup"><span data-stu-id="b397c-431">As you saw earlier in this article, the objects that you program with have methods.</span></span> <span data-ttu-id="b397c-432">Například `Database` objekt může mít metodu `Database.Connect`.</span><span class="sxs-lookup"><span data-stu-id="b397c-432">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="b397c-433">Mnoho metod má také jeden nebo více parametrů.</span><span class="sxs-lookup"><span data-stu-id="b397c-433">Many methods also have one or more parameters.</span></span> <span data-ttu-id="b397c-434">*Parametr* je hodnota, kterou předáte metodě, aby mohla metoda dokončit její úlohu.</span><span class="sxs-lookup"><span data-stu-id="b397c-434">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="b397c-435">Podívejte se například na deklaraci metody `Request.MapPath`, která přijímá tři parametry:</span><span class="sxs-lookup"><span data-stu-id="b397c-435">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-vb[Main](introducing-razor-syntax-vb/samples/sample57.vb)]

<span data-ttu-id="b397c-436">Tato metoda vrátí fyzickou cestu na serveru, který odpovídá zadané virtuální cestě.</span><span class="sxs-lookup"><span data-stu-id="b397c-436">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="b397c-437">Tři parametry pro metodu jsou `virtualPath`, `baseVirtualDir`a `allowCrossAppMapping`.</span><span class="sxs-lookup"><span data-stu-id="b397c-437">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="b397c-438">(Všimněte si, že v deklaraci jsou parametry uvedeny s datovými typy dat, která budou přijímat.) Při volání této metody je nutné dodat hodnoty pro všechny tři parametry.</span><span class="sxs-lookup"><span data-stu-id="b397c-438">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="b397c-439">Pokud používáte Visual Basic s syntaxe Razor, máte dvě možnosti pro předávání parametrů metodě: *poziční parametry* nebo *pojmenované parametry*.</span><span class="sxs-lookup"><span data-stu-id="b397c-439">When you're using Visual Basic with the Razor syntax, you have two options for passing parameters to a method: *positional parameters* or *named parameters*.</span></span> <span data-ttu-id="b397c-440">Chcete-li volat metodu pomocí pozičních parametrů, předáte parametry v přesném pořadí, které je zadáno v deklaraci metody.</span><span class="sxs-lookup"><span data-stu-id="b397c-440">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="b397c-441">(Toto pořadí byste obvykle znali v dokumentaci k metodě.) Je nutné postupovat podle pořadí a v případě potřeby nemůžete přeskočit &#8212; žádný z parametrů, předáte prázdný řetězec (`""`) nebo hodnotu null pro poziční parametr, pro který nemáte hodnotu.</span><span class="sxs-lookup"><span data-stu-id="b397c-441">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or null for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="b397c-442">Následující příklad předpokládá, že máte ve svém webu složku s názvem *skripty* .</span><span class="sxs-lookup"><span data-stu-id="b397c-442">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="b397c-443">Kód volá metodu `Request.MapPath` a předá hodnoty pro tři parametry ve správném pořadí.</span><span class="sxs-lookup"><span data-stu-id="b397c-443">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="b397c-444">Pak zobrazí výslednou mapovanou cestu.</span><span class="sxs-lookup"><span data-stu-id="b397c-444">It then displays the resulting mapped path.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample58.vbhtml)]

<span data-ttu-id="b397c-445">Pokud existuje mnoho parametrů pro metodu, můžete zachovat čisticí kód a čitelnější pomocí pojmenovaných parametrů.</span><span class="sxs-lookup"><span data-stu-id="b397c-445">When there are many parameters for a method, you can keep your code cleaner and more readable by using named parameters.</span></span> <span data-ttu-id="b397c-446">Chcete-li volat metodu pomocí pojmenovaných parametrů, zadejte název parametru následovaný `:=` a potom zadejte hodnotu.</span><span class="sxs-lookup"><span data-stu-id="b397c-446">To call a method using named parameters, specify the parameter name followed by `:=` and then provide the value.</span></span> <span data-ttu-id="b397c-447">Výhodou pojmenovaných parametrů je, že je můžete přidat v libovolném požadovaném pořadí.</span><span class="sxs-lookup"><span data-stu-id="b397c-447">An advantage of named parameters is that you can add them in any order you want.</span></span> <span data-ttu-id="b397c-448">(Nevýhodou je, že volání metody není jako kompaktní.)</span><span class="sxs-lookup"><span data-stu-id="b397c-448">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="b397c-449">Následující příklad volá stejnou metodu jako výše, ale používá pojmenované parametry k poskytnutí těchto hodnot:</span><span class="sxs-lookup"><span data-stu-id="b397c-449">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample59.vbhtml)]

<span data-ttu-id="b397c-450">Jak vidíte, parametry jsou předány v jiném pořadí.</span><span class="sxs-lookup"><span data-stu-id="b397c-450">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="b397c-451">Pokud však spustíte předchozí příklad a tento příklad vrátí stejnou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="b397c-451">However, if you run the previous example and this example, they'll return the same value.</span></span>

## <a name="handling-errors"></a><span data-ttu-id="b397c-452">Zpracování chyb</span><span class="sxs-lookup"><span data-stu-id="b397c-452">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="b397c-453">Příkazy try-catch</span><span class="sxs-lookup"><span data-stu-id="b397c-453">Try-Catch statements</span></span>

<span data-ttu-id="b397c-454">Často budete mít ve svém kódu příkazy, které mohou selhat z důvodů mimo váš ovládací prvek.</span><span class="sxs-lookup"><span data-stu-id="b397c-454">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="b397c-455">Příklad:</span><span class="sxs-lookup"><span data-stu-id="b397c-455">For example:</span></span>

- <span data-ttu-id="b397c-456">Pokud se váš kód pokusí otevřít, vytvořit, číst nebo zapsat soubor, může dojít k nejrůznějším chybám.</span><span class="sxs-lookup"><span data-stu-id="b397c-456">If your code tries to open, create, read, or write a file, all sorts of errors might occur.</span></span> <span data-ttu-id="b397c-457">Soubor, který chcete, možná neexistuje, může být uzamčen, kód pravděpodobně nemá oprávnění atd.</span><span class="sxs-lookup"><span data-stu-id="b397c-457">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="b397c-458">Podobně platí, že pokud se váš kód pokusí aktualizovat záznamy v databázi, může dojít k problémům s oprávněními, připojení k databázi může být vyřazeno, data, která mají být uložena, mohou být neplatná atd.</span><span class="sxs-lookup"><span data-stu-id="b397c-458">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="b397c-459">V programovacích podmínkách se tyto situace nazývají *výjimky*.</span><span class="sxs-lookup"><span data-stu-id="b397c-459">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="b397c-460">Pokud váš kód narazí na výjimku, vygeneruje (vyvolá) chybovou zprávu, která je nejlepší pro uživatele.</span><span class="sxs-lookup"><span data-stu-id="b397c-460">If your code encounters an exception, it generates (throws) an error message that is, at best, annoying to users.</span></span>

![Razor-Img14](introducing-razor-syntax-vb/_static/image14.jpg)

<span data-ttu-id="b397c-462">V situacích, kdy se váš kód může setkat s výjimkami, a aby se předešlo chybovým zprávám tohoto typu, můžete použít příkazy `Try/Catch`.</span><span class="sxs-lookup"><span data-stu-id="b397c-462">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `Try/Catch` statements.</span></span> <span data-ttu-id="b397c-463">V příkazu `Try` spustíte kód, který kontrolujete.</span><span class="sxs-lookup"><span data-stu-id="b397c-463">In the `Try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="b397c-464">V jednom nebo více příkazech `Catch` můžete vyhledat konkrétní chyby (konkrétní typy výjimek), ke kterým mohlo dojít.</span><span class="sxs-lookup"><span data-stu-id="b397c-464">In one or more `Catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="b397c-465">Můžete zahrnout tolik příkazů `Catch`, kolik potřebujete pro hledání chyb, které očekáváte.</span><span class="sxs-lookup"><span data-stu-id="b397c-465">You can include as many `Catch` statements as you need to look for errors that you're anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="b397c-466">Doporučujeme, abyste se vyhnuli použití metody `Response.Redirect` v příkazech `Try/Catch`, protože to může způsobit výjimku na stránce.</span><span class="sxs-lookup"><span data-stu-id="b397c-466">We recommend that you avoid using the `Response.Redirect` method in `Try/Catch` statements, because it can cause an exception in your page.</span></span>

<span data-ttu-id="b397c-467">Následující příklad ukazuje stránku, která vytvoří textový soubor pro první požadavek a pak zobrazí tlačítko, které uživateli otevře soubor.</span><span class="sxs-lookup"><span data-stu-id="b397c-467">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="b397c-468">Příklad záměrně používá špatný název souboru, takže bude způsobovat výjimku.</span><span class="sxs-lookup"><span data-stu-id="b397c-468">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="b397c-469">Kód zahrnuje `Catch` příkazy pro dvě možné výjimky: `FileNotFoundException`, ke kterým dojde, pokud je název souboru špatný a `DirectoryNotFoundException`, ke kterému dochází, pokud ASP.NET nemůže dokonce najít složku.</span><span class="sxs-lookup"><span data-stu-id="b397c-469">The code includes `Catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="b397c-470">(Můžete zrušit komentář k příkazu v příkladu, abyste viděli, jak se spustí, když vše funguje správně.)</span><span class="sxs-lookup"><span data-stu-id="b397c-470">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="b397c-471">Pokud váš kód nezpracovává výjimku, zobrazila se chybová stránka, například snímek předchozí obrazovky.</span><span class="sxs-lookup"><span data-stu-id="b397c-471">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="b397c-472">Nicméně část `Try/Catch` pomáhá zabránit uživateli v zobrazování těchto typů chyb.</span><span class="sxs-lookup"><span data-stu-id="b397c-472">However, the `Try/Catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-vbhtml[Main](introducing-razor-syntax-vb/samples/sample60.vbhtml)]

## <a name="additional-resources"></a><span data-ttu-id="b397c-473">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="b397c-473">Additional Resources</span></span>

### <a name="reference-documentation"></a><span data-ttu-id="b397c-474">Referenční dokumentace</span><span class="sxs-lookup"><span data-stu-id="b397c-474">Reference Documentation</span></span>

- [<span data-ttu-id="b397c-475">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="b397c-475">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)
- [<span data-ttu-id="b397c-476">Visual Basic jazyk</span><span class="sxs-lookup"><span data-stu-id="b397c-476">Visual Basic Language</span></span>](https://msdn.microsoft.com/library/2x7h1hfk.aspx)

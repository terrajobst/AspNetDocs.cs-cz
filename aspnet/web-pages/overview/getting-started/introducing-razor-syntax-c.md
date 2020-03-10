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
# <a name="introduction-to-aspnet-web-programming-using-the-razor-syntax-c"></a><span data-ttu-id="92f39-104">Úvod do webového programování v ASP.NET pomocí syntaxe Razor (C#)</span><span class="sxs-lookup"><span data-stu-id="92f39-104">Introduction to ASP.NET Web Programming Using the Razor Syntax (C#)</span></span>

<span data-ttu-id="92f39-105">tím, že [FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="92f39-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="92f39-106">Tento článek vám poskytne přehled o programování s ASP.NET webovými stránkami pomocí syntaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="92f39-106">This article gives you an overview of programming with ASP.NET Web Pages using the Razor syntax.</span></span> <span data-ttu-id="92f39-107">ASP.NET je technologie Microsoftu pro spouštění dynamických webových stránek na webových serverech.</span><span class="sxs-lookup"><span data-stu-id="92f39-107">ASP.NET is Microsoft's technology for running dynamic web pages on web servers.</span></span> <span data-ttu-id="92f39-108">Tento článek se C# zaměřuje na používání programovacího jazyka.</span><span class="sxs-lookup"><span data-stu-id="92f39-108">This articles focuses on using the C# programming language.</span></span>
> 
> <span data-ttu-id="92f39-109">**Co se naučíte**:</span><span class="sxs-lookup"><span data-stu-id="92f39-109">**What you'll learn**:</span></span>
> 
> - <span data-ttu-id="92f39-110">Nejčastějších 8 programovacích tipů pro Začínáme s programováním webových stránek ASP.NET pomocí syntaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="92f39-110">The top 8 programming tips for getting started with programming ASP.NET Web Pages using Razor syntax.</span></span>
> - <span data-ttu-id="92f39-111">Základní koncepty programování, které budete potřebovat.</span><span class="sxs-lookup"><span data-stu-id="92f39-111">Basic programming concepts you'll need.</span></span>
> - <span data-ttu-id="92f39-112">Jaký kód serveru ASP.NET a syntaxe Razor se týkají.</span><span class="sxs-lookup"><span data-stu-id="92f39-112">What ASP.NET server code and the Razor syntax is all about.</span></span>
>   
> 
> ## <a name="software-versions"></a><span data-ttu-id="92f39-113">Verze softwaru</span><span class="sxs-lookup"><span data-stu-id="92f39-113">Software versions</span></span>
> 
> 
> - <span data-ttu-id="92f39-114">Webové stránky ASP.NET (Razor) 3</span><span class="sxs-lookup"><span data-stu-id="92f39-114">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="92f39-115">Tento kurz funguje také s ASP.NET webovými stránkami 2.</span><span class="sxs-lookup"><span data-stu-id="92f39-115">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="the-top-8-programming-tips"></a><span data-ttu-id="92f39-116">Prvních 8 tipů pro programování</span><span class="sxs-lookup"><span data-stu-id="92f39-116">The Top 8 Programming Tips</span></span>

<span data-ttu-id="92f39-117">Tato část obsahuje několik tipů, které bezpodmínečně potřebujete znát při psaní kódu ASP.NET serveru pomocí syntaxe Razor.</span><span class="sxs-lookup"><span data-stu-id="92f39-117">This section lists a few tips that you absolutely need to know as you start writing ASP.NET server code using the Razor syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="92f39-118">Syntaxe Razor vychází z C# programovacího jazyka a je to jazyk, který se nejčastěji používá s ASP.NET webovými stránkami.</span><span class="sxs-lookup"><span data-stu-id="92f39-118">The Razor syntax is based on the C# programming language, and that's the language that's used most often with ASP.NET Web Pages.</span></span> <span data-ttu-id="92f39-119">Syntaxe Razor ale taky podporuje Visual Basic jazyk a všechno, co vidíte, můžete také udělat v Visual Basic.</span><span class="sxs-lookup"><span data-stu-id="92f39-119">However, the Razor syntax also supports the Visual Basic language, and everything you see you can also do in Visual Basic.</span></span> <span data-ttu-id="92f39-120">Podrobnosti najdete v dodatku [Visual Basic jazyk a syntaxi](https://go.microsoft.com/fwlink/?LinkId=202908).</span><span class="sxs-lookup"><span data-stu-id="92f39-120">For details, see the appendix [Visual Basic Language and Syntax](https://go.microsoft.com/fwlink/?LinkId=202908).</span></span>

<span data-ttu-id="92f39-121">Další informace o většině těchto programovacích postupů najdete dále v článku.</span><span class="sxs-lookup"><span data-stu-id="92f39-121">You can find more details about most of these programming techniques later in the article.</span></span>

### <a name="1-you-add-code-to-a-page-using-the--character"></a><span data-ttu-id="92f39-122">1. na stránku přidáte kód pomocí znaku @.</span><span class="sxs-lookup"><span data-stu-id="92f39-122">1. You add code to a page using the @ character</span></span>

<span data-ttu-id="92f39-123">Znak `@` spouští vložené výrazy, bloky s jedním příkazem a bloky s více příkazy:</span><span class="sxs-lookup"><span data-stu-id="92f39-123">The `@` character starts inline expressions, single statement blocks, and multi-statement blocks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample1.html)]

<span data-ttu-id="92f39-124">Tyto příkazy vypadají jako při spuštění stránky v prohlížeči:</span><span class="sxs-lookup"><span data-stu-id="92f39-124">This is what these statements look like when the page runs in a browser:</span></span>

![Razor-Img1](introducing-razor-syntax-c/_static/image1.jpg)

> [!TIP] 
> 
> <span data-ttu-id="92f39-126">**Kódování HTML**</span><span class="sxs-lookup"><span data-stu-id="92f39-126">**HTML Encoding**</span></span>
> 
> <span data-ttu-id="92f39-127">Pokud zobrazíte obsah na stránce pomocí `@`ho znaku, jako v předchozích příkladech, ASP.NET kód HTML zakóduje výstup.</span><span class="sxs-lookup"><span data-stu-id="92f39-127">When you display content in a page using the `@` character, as in the preceding examples, ASP.NET HTML-encodes the output.</span></span> <span data-ttu-id="92f39-128">Tím se nahradí vyhrazené znaky HTML (například `<` a `>` a `&`) kódy, které umožňují zobrazení znaků jako znaků na webové stránce namísto interpretace jako značek nebo entit jazyka HTML.</span><span class="sxs-lookup"><span data-stu-id="92f39-128">This replaces reserved HTML characters (such as `<` and `>` and `&`) with codes that enable the characters to be displayed as characters in a web page instead of being interpreted as HTML tags or entities.</span></span> <span data-ttu-id="92f39-129">Bez kódování HTML se výstup z kódu serveru nemusí zobrazit správně a může vystavit stránku pro rizika zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="92f39-129">Without HTML encoding, the output from your server code might not display correctly, and could expose a page to security risks.</span></span>
> 
> <span data-ttu-id="92f39-130">Pokud je vaším cílem výstup kódu HTML, který vykresluje značky jako kód (například `<p></p>` pro odstavec nebo `<em></em>` k zdůraznění textu), přečtěte si část [kombinování textu, značky a kódu v blocích kódu](#BM_CombiningTextMarkupAndCode) dále v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="92f39-130">If your goal is to output HTML markup that renders tags as markup (for example `<p></p>` for a paragraph or `<em></em>` to emphasize text), see the section [Combining Text, Markup, and Code in Code Blocks](#BM_CombiningTextMarkupAndCode) later in this article.</span></span>
> 
> <span data-ttu-id="92f39-131">Můžete si přečíst další informace o kódování HTML při [práci s formuláři](https://go.microsoft.com/fwlink/?LinkId=202892).</span><span class="sxs-lookup"><span data-stu-id="92f39-131">You can read more about HTML encoding in [Working with Forms](https://go.microsoft.com/fwlink/?LinkId=202892).</span></span>

### <a name="2-you-enclose-code-blocks-in-braces"></a><span data-ttu-id="92f39-132">2. můžete bloky kódu uzavřít do složených závorek.</span><span class="sxs-lookup"><span data-stu-id="92f39-132">2. You enclose code blocks in braces</span></span>

<span data-ttu-id="92f39-133">*Blok kódu* obsahuje jeden nebo více příkazů kódu a je uzavřen ve složených závorkách.</span><span class="sxs-lookup"><span data-stu-id="92f39-133">A *code block* includes one or more code statements and is enclosed in braces.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample2.html)]

<span data-ttu-id="92f39-134">Výsledek zobrazený v prohlížeči:</span><span class="sxs-lookup"><span data-stu-id="92f39-134">The result displayed in a browser:</span></span>

![Razor-Img2](introducing-razor-syntax-c/_static/image2.jpg)

### <a name="3-inside-a-block-you-end-each-code-statement-with-a-semicolon"></a><span data-ttu-id="92f39-136">3. uvnitř bloku se každý příkaz kódu ukončí středníkem.</span><span class="sxs-lookup"><span data-stu-id="92f39-136">3. Inside a block, you end each code statement with a semicolon</span></span>

<span data-ttu-id="92f39-137">Uvnitř bloku kódu musí každý úplný příkaz kódu končit středníkem.</span><span class="sxs-lookup"><span data-stu-id="92f39-137">Inside a code block, each complete code statement must end with a semicolon.</span></span> <span data-ttu-id="92f39-138">Vložené výrazy nekončí středníkem.</span><span class="sxs-lookup"><span data-stu-id="92f39-138">Inline expressions don't end with a semicolon.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample3.html)]

### <a name="4-you-use-variables-to-store-values"></a><span data-ttu-id="92f39-139">4. proměnné použijete k uložení hodnot.</span><span class="sxs-lookup"><span data-stu-id="92f39-139">4. You use variables to store values</span></span>

<span data-ttu-id="92f39-140">Hodnoty můžete ukládat do *proměnné*, včetně řetězců, čísel a dat atd. Novou proměnnou vytvoříte pomocí klíčového slova `var`.</span><span class="sxs-lookup"><span data-stu-id="92f39-140">You can store values in a *variable*, including strings, numbers, and dates, etc. You create a new variable using the `var` keyword.</span></span> <span data-ttu-id="92f39-141">Hodnoty proměnných můžete vkládat přímo na stránce pomocí `@`.</span><span class="sxs-lookup"><span data-stu-id="92f39-141">You can insert variable values directly in a page using `@`.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample4.html)]

<span data-ttu-id="92f39-142">Výsledek zobrazený v prohlížeči:</span><span class="sxs-lookup"><span data-stu-id="92f39-142">The result displayed in a browser:</span></span>

![Razor-Img3](introducing-razor-syntax-c/_static/image3.jpg)

<a id="ID_StringLiterals"></a>
### <a name="5-you-enclose-literal-string-values-in-double-quotation-marks"></a><span data-ttu-id="92f39-144">5. Uzavřete řetězcové hodnoty literálu do dvojitých uvozovek.</span><span class="sxs-lookup"><span data-stu-id="92f39-144">5. You enclose literal string values in double quotation marks</span></span>

<span data-ttu-id="92f39-145">*Řetězec* je posloupnost znaků, které jsou považovány za text.</span><span class="sxs-lookup"><span data-stu-id="92f39-145">A *string* is a sequence of characters that are treated as text.</span></span> <span data-ttu-id="92f39-146">Pokud chcete zadat řetězec, uzavřete ho do dvojitých uvozovek:</span><span class="sxs-lookup"><span data-stu-id="92f39-146">To specify a string, you enclose it in double quotation marks:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample5.cshtml)]

<span data-ttu-id="92f39-147">Pokud řetězec, který chcete zobrazit, obsahuje znak zpětného lomítka (`\`) nebo dvojité uvozovky (`"`), použijte *doslovné řetězcový literál* , který je předponou operátoru `@`.</span><span class="sxs-lookup"><span data-stu-id="92f39-147">If the string that you want to display contains a backslash character ( `\` ) or double quotation marks ( `"` ), use a *verbatim string literal* that's prefixed with the `@` operator.</span></span> <span data-ttu-id="92f39-148">(V C#, znak \ má zvláštní význam, pokud nepoužijete doslovné řetězcový literál.)</span><span class="sxs-lookup"><span data-stu-id="92f39-148">(In C#, the \ character has special meaning unless you use a verbatim string literal.)</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample6.html)]

<span data-ttu-id="92f39-149">Chcete-li vložit dvojité uvozovky, použijte doslovné řetězcový literál a uvozovky opakujte:</span><span class="sxs-lookup"><span data-stu-id="92f39-149">To embed double quotation marks, use a verbatim string literal and repeat the quotation marks:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample7.html)]

<span data-ttu-id="92f39-150">Tady je výsledek použití obou z těchto příkladů na stránce:</span><span class="sxs-lookup"><span data-stu-id="92f39-150">Here's the result of using both of these examples in a page:</span></span>

![Razor-Img4](introducing-razor-syntax-c/_static/image4.jpg)

> [!NOTE]
> <span data-ttu-id="92f39-152">Všimněte si, že znak `@` slouží k označení doslovnéch řetězcových literálů C# v a k označení kódu na stránkách ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="92f39-152">Notice that the `@` character is used both to mark verbatim string literals in C# and to mark code in ASP.NET pages.</span></span>

### <a name="6-code-is-case-sensitive"></a><span data-ttu-id="92f39-153">6. kód rozlišuje velká a malá písmena.</span><span class="sxs-lookup"><span data-stu-id="92f39-153">6. Code is case sensitive</span></span>

<span data-ttu-id="92f39-154">V C#, klíčová slova (například `var`, `true`a `if`) a názvy proměnných rozlišují malá a velká písmena.</span><span class="sxs-lookup"><span data-stu-id="92f39-154">In C#, keywords (like `var`, `true`, and `if`) and variable names are case sensitive.</span></span> <span data-ttu-id="92f39-155">Následující řádky kódu vytvoří dvě různé proměnné `lastName` a `LastName.`</span><span class="sxs-lookup"><span data-stu-id="92f39-155">The following lines of code create two different variables, `lastName` and `LastName.`</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample8.cshtml)]

<span data-ttu-id="92f39-156">Pokud deklarujete proměnnou jako `var lastName = "Smith";` a pokusíte se na ni odkazovat na tuto proměnnou jako `@LastName`, místo `"Smith"`se zobrazí hodnota `"Jones"`.</span><span class="sxs-lookup"><span data-stu-id="92f39-156">If you declare a variable as `var lastName = "Smith";` and try to reference that variable in your page as `@LastName`, you would get the value `"Jones"` instead of `"Smith"`.</span></span>

> [!NOTE]
> <span data-ttu-id="92f39-157">V Visual Basic klíčová slova a proměnné *nerozlišují velká a malá písmena.*</span><span class="sxs-lookup"><span data-stu-id="92f39-157">In Visual Basic, keywords and variables are *not* case sensitive.</span></span>

### <a name="7-much-of-your-coding-involves-objects"></a><span data-ttu-id="92f39-158">7. mnoho z vašich kódování zahrnuje objekty</span><span class="sxs-lookup"><span data-stu-id="92f39-158">7. Much of your coding involves objects</span></span>

<span data-ttu-id="92f39-159">*Objekt* představuje věc, kterou můžete programovat se &#8212; stránkou, textovým polem, souborem, obrázkem, webovým požadavkem, e-mailovou zprávou, záznamem zákazníka (řádkem databáze) atd. Objekty mají vlastnosti, které popisují jejich charakteristiky a které můžete číst nebo měnit &#8212; objekt textového pole, má vlastnost `Text` (mimo jiné), objekt požadavku má vlastnost `Url`, e-mailová zpráva má vlastnost `From` a objekt Customer má vlastnost `FirstName`.</span><span class="sxs-lookup"><span data-stu-id="92f39-159">An *object* represents a thing that you can program with &#8212; a page, a text box, a file, an image, a web request, an email message, a customer record (database row), etc. Objects have properties that describe their characteristics and that you can read or change &#8212; a text box object has a `Text` property (among others), a request object has a `Url` property, an email message has a `From` property, and a customer object has a `FirstName` property.</span></span> <span data-ttu-id="92f39-160">Objekty mají také metody, které jsou &quot;slovesy&quot; mohou provádět.</span><span class="sxs-lookup"><span data-stu-id="92f39-160">Objects also have methods that are the &quot;verbs&quot; they can perform.</span></span> <span data-ttu-id="92f39-161">Mezi příklady patří `Save` metoda objektu souboru, metoda `Rotate` objektu obrázku a metoda `Send` objektu e-mailu.</span><span class="sxs-lookup"><span data-stu-id="92f39-161">Examples include a file object's `Save` method, an image object's `Rotate` method, and an email object's `Send` method.</span></span>

<span data-ttu-id="92f39-162">Často budete pracovat s objektem `Request`, který vám poskytne informace, jako jsou hodnoty textových polí (pole formuláře) na stránce, jaký typ prohlížeče odeslal požadavek, adresu URL stránky, identitu uživatele atd. Následující příklad ukazuje, jak získat přístup k vlastnostem objektu `Request` a jak zavolat metodu `MapPath` objektu `Request`, který poskytuje absolutní cestu stránky na serveru:</span><span class="sxs-lookup"><span data-stu-id="92f39-162">You'll often work with the `Request` object, which gives you information like the values of text boxes (form fields) on the page, what type of browser made the request, the URL of the page, the user identity, etc. The following example shows how to access properties of the `Request` object and how to call the `MapPath` method of the `Request` object, which gives you the absolute path of the page on the server:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample9.html)]

<span data-ttu-id="92f39-163">Výsledek zobrazený v prohlížeči:</span><span class="sxs-lookup"><span data-stu-id="92f39-163">The result displayed in a browser:</span></span>

![Razor-Img5](introducing-razor-syntax-c/_static/image5.jpg)

### <a name="8-you-can-write-code-that-makes-decisions"></a><span data-ttu-id="92f39-165">8. můžete napsat kód, který provede rozhodnutí.</span><span class="sxs-lookup"><span data-stu-id="92f39-165">8. You can write code that makes decisions</span></span>

<span data-ttu-id="92f39-166">Klíčovou funkcí dynamických webových stránek je, že můžete určit, co dělat na základě podmínek.</span><span class="sxs-lookup"><span data-stu-id="92f39-166">A key feature of dynamic web pages is that you can determine what to do based on conditions.</span></span> <span data-ttu-id="92f39-167">Nejběžnější způsob, jak to provést, je pomocí příkazu `if` (a volitelného příkazu `else`).</span><span class="sxs-lookup"><span data-stu-id="92f39-167">The most common way to do this is with the `if` statement (and optional `else` statement).</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample10.cshtml)]

<span data-ttu-id="92f39-168">Příkaz `if(IsPost)` je zkrácený způsob psaní `if(IsPost == true)`.</span><span class="sxs-lookup"><span data-stu-id="92f39-168">The statement `if(IsPost)` is a shorthand way of writing `if(IsPost == true)`.</span></span> <span data-ttu-id="92f39-169">Spolu s `if`mi příkazy existují různé způsoby, jak testovat podmínky, opakovat bloky kódu a tak dále, které jsou popsány dále v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="92f39-169">Along with `if` statements, there are a variety of ways to test conditions, repeat blocks of code, and so on, which are described later in this article.</span></span>

<span data-ttu-id="92f39-170">Výsledek zobrazený v prohlížeči (po kliknutí na **Odeslat**):</span><span class="sxs-lookup"><span data-stu-id="92f39-170">The result displayed in a browser (after clicking **Submit**):</span></span>

![Razor-Img6](introducing-razor-syntax-c/_static/image6.jpg)

> [!TIP] 
> 
> <a id="SB_HttpGetPost"></a>
> ### <a name="http-get-and-post-methods-and-the-ispost-property"></a><span data-ttu-id="92f39-172">Metody GET a POST HTTP a vlastnost-post</span><span class="sxs-lookup"><span data-stu-id="92f39-172">HTTP GET and POST Methods and the IsPost Property</span></span>
> 
> <span data-ttu-id="92f39-173">Protokol použitý pro webové stránky (HTTP) podporuje velmi omezený počet metod (operací), které se používají k provádění požadavků na server.</span><span class="sxs-lookup"><span data-stu-id="92f39-173">The protocol used for web pages (HTTP) supports a very limited number of methods (verbs) that are used to make requests to the server.</span></span> <span data-ttu-id="92f39-174">Dva nejběžnější jsou GET, které slouží ke čtení stránky a k odeslání příspěvku, který slouží k odeslání stránky.</span><span class="sxs-lookup"><span data-stu-id="92f39-174">The two most common ones are GET, which is used to read a page, and POST, which is used to submit a page.</span></span> <span data-ttu-id="92f39-175">Obecně platí, že uživatel poprvé požaduje stránku, stránka se požaduje pomocí GET.</span><span class="sxs-lookup"><span data-stu-id="92f39-175">In general, the first time a user requests a page, the page is requested using GET.</span></span> <span data-ttu-id="92f39-176">Pokud uživatel vyplní formulář a klikne na tlačítko Odeslat, prohlížeč odešle požadavek POST na server.</span><span class="sxs-lookup"><span data-stu-id="92f39-176">If the user fills in a form and then clicks a submit button, the browser makes a POST request to the server.</span></span>
> 
> <span data-ttu-id="92f39-177">Ve webovém programování je často užitečné zjistit, jestli se stránka požaduje jako GET nebo jako příspěvek, abyste věděli, jak stránku zpracovat.</span><span class="sxs-lookup"><span data-stu-id="92f39-177">In web programming, it's often useful to know whether a page is being requested as a GET or as a POST so that you know how to process the page.</span></span> <span data-ttu-id="92f39-178">Na webových stránkách ASP.NET můžete pomocí vlastnosti `IsPost` zjistit, jestli je požadavek GET nebo POST.</span><span class="sxs-lookup"><span data-stu-id="92f39-178">In ASP.NET Web Pages, you can use the `IsPost` property to see whether a request is a GET or a POST.</span></span> <span data-ttu-id="92f39-179">Pokud je žádost příspěvek, vlastnost `IsPost` vrátí hodnotu true a můžete provádět akce, jako je například čtení hodnot textových polí na formuláři.</span><span class="sxs-lookup"><span data-stu-id="92f39-179">If the request is a POST, the `IsPost` property will return true, and you can do things like read the values of text boxes on a form.</span></span> <span data-ttu-id="92f39-180">V mnoha příkladech se dozvíte, jak stránku zpracovat odlišně v závislosti na hodnotě `IsPost`.</span><span class="sxs-lookup"><span data-stu-id="92f39-180">Many examples you'll see show you how to process the page differently depending on the value of `IsPost`.</span></span>

## <a name="a-simple-code-example"></a><span data-ttu-id="92f39-181">Příklad jednoduchého kódu</span><span class="sxs-lookup"><span data-stu-id="92f39-181">A Simple Code Example</span></span>

<span data-ttu-id="92f39-182">Tento postup ukazuje, jak vytvořit stránku, která znázorňuje základní programovací techniky.</span><span class="sxs-lookup"><span data-stu-id="92f39-182">This procedure shows you how to create a page that illustrates basic programming techniques.</span></span> <span data-ttu-id="92f39-183">V tomto příkladu vytvoříte stránku, která umožní uživatelům zadat dvě čísla, pak je přidá a zobrazí výsledek.</span><span class="sxs-lookup"><span data-stu-id="92f39-183">In the example, you create a page that lets users enter two numbers, then it adds them and displays the result.</span></span>

1. <span data-ttu-id="92f39-184">V editoru vytvořte nový soubor a pojmenujte jej *AddNumbers. cshtml*.</span><span class="sxs-lookup"><span data-stu-id="92f39-184">In your editor, create a new file and name it *AddNumbers.cshtml*.</span></span>
2. <span data-ttu-id="92f39-185">Zkopírujte následující kód a označení na stránku a nahraďte cokoli již na stránce.</span><span class="sxs-lookup"><span data-stu-id="92f39-185">Copy the following code and markup into the page, replacing anything already in the page.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample11.cshtml)]

    <span data-ttu-id="92f39-186">Tady je několik věcí, které můžete poznamenat:</span><span class="sxs-lookup"><span data-stu-id="92f39-186">Here are some things for you to note:</span></span>

    - <span data-ttu-id="92f39-187">`@` znak spustí první blok kódu na stránce a předá `totalMessage` proměnnou, která je vložena poblíž dolní části stránky.</span><span class="sxs-lookup"><span data-stu-id="92f39-187">The `@` character starts the first block of code in the page, and it precedes the `totalMessage` variable that's embedded near the bottom of the page.</span></span>
    - <span data-ttu-id="92f39-188">Blok v horní části stránky je uzavřený ve složených závorkách.</span><span class="sxs-lookup"><span data-stu-id="92f39-188">The block at the top of the page is enclosed in braces.</span></span>
    - <span data-ttu-id="92f39-189">V bloku v horní části všechny řádky končí středníkem.</span><span class="sxs-lookup"><span data-stu-id="92f39-189">In the block at the top, all lines end with a semicolon.</span></span>
    - <span data-ttu-id="92f39-190">Proměnné `total`, `num1`, `num2`a `totalMessage` ukládají několik čísel a řetězce.</span><span class="sxs-lookup"><span data-stu-id="92f39-190">The variables `total`, `num1`, `num2`, and `totalMessage` store several numbers and a string.</span></span>
    - <span data-ttu-id="92f39-191">Literální řetězcová hodnota přiřazená k proměnné `totalMessage` je v dvojitých uvozovkách.</span><span class="sxs-lookup"><span data-stu-id="92f39-191">The literal string value assigned to the `totalMessage` variable is in double quotation marks.</span></span>
    - <span data-ttu-id="92f39-192">Vzhledem k tomu, že kód rozlišuje velká a malá písmena, je-li proměnná `totalMessage` použita v dolní části stránky, její název musí přesně odpovídat proměnné v horní části.</span><span class="sxs-lookup"><span data-stu-id="92f39-192">Because the code is case-sensitive, when the `totalMessage` variable is used near the bottom of the page, its name must match the variable at the top exactly.</span></span>
    - <span data-ttu-id="92f39-193">Výraz `num1.AsInt() + num2.AsInt()` ukazuje, jak pracovat s objekty a metodami.</span><span class="sxs-lookup"><span data-stu-id="92f39-193">The expression `num1.AsInt() + num2.AsInt()` shows how to work with objects and methods.</span></span> <span data-ttu-id="92f39-194">Metoda `AsInt` u každé proměnné převede řetězec zadaný uživatelem na číslo (celé číslo), takže můžete na něm provádět aritmetické operace.</span><span class="sxs-lookup"><span data-stu-id="92f39-194">The `AsInt` method on each variable converts the string entered by a user to a number (an integer) so that you can perform arithmetic on it.</span></span>
    - <span data-ttu-id="92f39-195">Značka `<form>` obsahuje atribut `method="post"`.</span><span class="sxs-lookup"><span data-stu-id="92f39-195">The `<form>` tag includes a `method="post"` attribute.</span></span> <span data-ttu-id="92f39-196">To určuje, že když uživatel klikne na **Přidat**, stránka se pošle na server pomocí metody HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="92f39-196">This specifies that when the user clicks **Add**, the page will be sent to the server using the HTTP POST method.</span></span> <span data-ttu-id="92f39-197">Po odeslání stránky se `if(IsPost)` test vyhodnotí jako true a spustí se podmíněný kód a zobrazí se výsledek přidání čísel.</span><span class="sxs-lookup"><span data-stu-id="92f39-197">When the page is submitted, the `if(IsPost)` test evaluates to true and the conditional code runs, displaying the result of adding the numbers.</span></span>
3. <span data-ttu-id="92f39-198">Uložte stránku a spusťte ji v prohlížeči.</span><span class="sxs-lookup"><span data-stu-id="92f39-198">Save the page and run it in a browser.</span></span> <span data-ttu-id="92f39-199">(Před spuštěním se ujistěte, že je stránka vybraná v pracovním prostoru **soubory** .) Zadejte dvě celá čísla a potom klikněte na tlačítko **Přidat** .</span><span class="sxs-lookup"><span data-stu-id="92f39-199">(Make sure the page is selected in the **Files** workspace before you run it.) Enter two whole numbers and then click the **Add** button.</span></span> 

    ![Razor-Img7](introducing-razor-syntax-c/_static/image7.jpg)

## <a name="basic-programming-concepts"></a><span data-ttu-id="92f39-201">Základní koncepty programování</span><span class="sxs-lookup"><span data-stu-id="92f39-201">Basic Programming Concepts</span></span>

<span data-ttu-id="92f39-202">Tento článek vám poskytne přehled o ASP.NET webovém programování.</span><span class="sxs-lookup"><span data-stu-id="92f39-202">This article provides you with an overview of ASP.NET web programming.</span></span> <span data-ttu-id="92f39-203">Nejedná se o vyčerpávající přezkoumání, a to pouze rychlou prohlídku prostřednictvím konceptů programování, které použijete nejčastěji.</span><span class="sxs-lookup"><span data-stu-id="92f39-203">It isn't an exhaustive examination, just a quick tour through the programming concepts you'll use most often.</span></span> <span data-ttu-id="92f39-204">I když to bude mít skoro všechno, co budete potřebovat k zahájení práce s ASP.NET webovými stránkami.</span><span class="sxs-lookup"><span data-stu-id="92f39-204">Even so, it covers almost everything you'll need to get started with ASP.NET Web Pages.</span></span>

<span data-ttu-id="92f39-205">Ale první, což je málo technického pozadí.</span><span class="sxs-lookup"><span data-stu-id="92f39-205">But first, a little technical background.</span></span>

### <a name="the-razor-syntax-server-code-and-aspnet"></a><span data-ttu-id="92f39-206">Syntaxe Razor, kód serveru a ASP.NET</span><span class="sxs-lookup"><span data-stu-id="92f39-206">The Razor Syntax, Server Code, and ASP.NET</span></span>

<span data-ttu-id="92f39-207">Syntaxe Razor je jednoduchá programovací syntaxe pro vkládání kódu založeného na serveru na webové stránce.</span><span class="sxs-lookup"><span data-stu-id="92f39-207">Razor syntax is a simple programming syntax for embedding server-based code in a web page.</span></span> <span data-ttu-id="92f39-208">Na webové stránce, která používá syntaxe Razor, existují dva druhy obsahu: obsah klienta a kód serveru.</span><span class="sxs-lookup"><span data-stu-id="92f39-208">In a web page that uses the Razor syntax, there are two kinds of content: client content and server code.</span></span> <span data-ttu-id="92f39-209">Obsah klienta je ta, kterou jste použili pro webové stránky: značky HTML (elementy), informace o stylu, jako je například CSS, možná některý klientský skript, například JavaScript, a prostý text.</span><span class="sxs-lookup"><span data-stu-id="92f39-209">Client content is the stuff you're used to in web pages: HTML markup (elements), style information such as CSS, maybe some client script such as JavaScript, and plain text.</span></span>

<span data-ttu-id="92f39-210">Syntaxe Razor umožňuje přidat serverový kód do tohoto obsahu klienta.</span><span class="sxs-lookup"><span data-stu-id="92f39-210">Razor syntax lets you add server code to this client content.</span></span> <span data-ttu-id="92f39-211">Pokud je na stránce kód serveru, server nejprve spustí tento kód, než pošle stránku do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="92f39-211">If there's server code in the page, the server runs that code first, before it sends the page to the browser.</span></span> <span data-ttu-id="92f39-212">Po spuštění na serveru může kód provádět úlohy, které mohou být mnohem složitější pomocí samotného klientského obsahu, jako je například přístup k databázím založeným na serveru.</span><span class="sxs-lookup"><span data-stu-id="92f39-212">By running on the server, the code can perform tasks that can be a lot more complex to do using client content alone, like accessing server-based databases.</span></span> <span data-ttu-id="92f39-213">Nejdůležitější je, že serverový kód může dynamicky vytvářet obsah &#8212; klienta, který může generovat kód HTML nebo jiný obsah za běhu a pak ho odeslat prohlížeči spolu se všemi statickými HTML, které stránka může obsahovat.</span><span class="sxs-lookup"><span data-stu-id="92f39-213">Most importantly, server code can dynamically create client content &#8212; it can generate HTML markup or other content on the fly and then send it to the browser along with any static HTML that the page might contain.</span></span> <span data-ttu-id="92f39-214">V perspektivě prohlížeče se obsah klienta generovaný kódem serveru neliší od jiného obsahu klienta.</span><span class="sxs-lookup"><span data-stu-id="92f39-214">From the browser's perspective, client content that's generated by your server code is no different than any other client content.</span></span> <span data-ttu-id="92f39-215">Jak už jste viděli, kód serveru, který je potřeba, je poměrně jednoduchý.</span><span class="sxs-lookup"><span data-stu-id="92f39-215">As you've already seen, the server code that's required is quite simple.</span></span>

<span data-ttu-id="92f39-216">ASP.NET webové stránky, které zahrnují syntaxe Razor mají speciální příponu souboru ( *. cshtml* nebo *. vbhtml*).</span><span class="sxs-lookup"><span data-stu-id="92f39-216">ASP.NET web pages that include the Razor syntax have a special file extension (*.cshtml* or *.vbhtml*).</span></span> <span data-ttu-id="92f39-217">Server rozpoznává tato rozšíření, spouští kód označený syntaxe Razor a poté odesílá stránku do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="92f39-217">The server recognizes these extensions, runs the code that's marked with Razor syntax, and then sends the page to the browser.</span></span>

### <a name="where-does-aspnet-fit-in"></a><span data-ttu-id="92f39-218">Kde se ASP.NET vejde?</span><span class="sxs-lookup"><span data-stu-id="92f39-218">Where does ASP.NET fit in?</span></span>

<span data-ttu-id="92f39-219">Syntaxe Razor vychází z technologie od Microsoftu s názvem ASP.NET, která je zase založená na .NET Framework Microsoft.</span><span class="sxs-lookup"><span data-stu-id="92f39-219">Razor syntax is based on a technology from Microsoft called ASP.NET, which in turn is based on the Microsoft .NET Framework.</span></span> <span data-ttu-id="92f39-220">The.NET Framework je Big, komplexní programovací rozhraní Microsoftu pro vývoj prakticky jakéhokoli typu počítačové aplikace.</span><span class="sxs-lookup"><span data-stu-id="92f39-220">The.NET Framework is a big, comprehensive programming framework from Microsoft for developing virtually any type of computer application.</span></span> <span data-ttu-id="92f39-221">ASP.NET je součástí .NET Framework, který je speciálně navržený pro vytváření webových aplikací.</span><span class="sxs-lookup"><span data-stu-id="92f39-221">ASP.NET is the part of the .NET Framework that's specifically designed for creating web applications.</span></span> <span data-ttu-id="92f39-222">Vývojáři používali ASP.NET k vytvoření mnoha největších a nejvyšších webů provozu na světě.</span><span class="sxs-lookup"><span data-stu-id="92f39-222">Developers have used ASP.NET to create many of the largest and highest-traffic websites in the world.</span></span> <span data-ttu-id="92f39-223">(Kdykoli se zobrazí přípona názvu souboru *. aspx* jako součást adresy URL v lokalitě, budete si vědomi, že se web napsal pomocí ASP.NET.)</span><span class="sxs-lookup"><span data-stu-id="92f39-223">(Any time you see the file-name extension *.aspx* as part of the URL in a site, you'll know that the site was written using ASP.NET.)</span></span>

<span data-ttu-id="92f39-224">Syntaxe Razor poskytuje veškerou sílu ASP.NET, ale s využitím zjednodušené syntaxe, která se snadno naučíte, pokud jste odborníkem na začátečníky a máte vyšší produktivitu.</span><span class="sxs-lookup"><span data-stu-id="92f39-224">The Razor syntax gives you all the power of ASP.NET, but using a simplified syntax that's easier to learn if you're a beginner and that makes you more productive if you're an expert.</span></span> <span data-ttu-id="92f39-225">I když se tato syntaxe snadno používá, její rodinný vztah k ASP.NET a .NET Framework znamená, že když se vaše weby stanou sofistikovanější, máte sílu větší architektury, kterou máte k dispozici.</span><span class="sxs-lookup"><span data-stu-id="92f39-225">Even though this syntax is simple to use, its family relationship to ASP.NET and the .NET Framework means that as your websites become more sophisticated, you have the power of the larger frameworks available to you.</span></span>

![Razor-Img8](introducing-razor-syntax-c/_static/image8.jpg)

> [!TIP] 
> 
> <span data-ttu-id="92f39-227">**Třídy a instance**</span><span class="sxs-lookup"><span data-stu-id="92f39-227">**Classes and Instances**</span></span>
> 
> <span data-ttu-id="92f39-228">ASP.NET Server Code používá objekty, které jsou vytvořeny na nápad třídy.</span><span class="sxs-lookup"><span data-stu-id="92f39-228">ASP.NET server code uses objects, which are in turn built on the idea of classes.</span></span> <span data-ttu-id="92f39-229">Třída je definicí nebo šablonou pro objekt.</span><span class="sxs-lookup"><span data-stu-id="92f39-229">The class is the definition or template for an object.</span></span> <span data-ttu-id="92f39-230">Například aplikace může obsahovat třídu `Customer` definující vlastnosti a metody, které vyžaduje objekt zákazníka.</span><span class="sxs-lookup"><span data-stu-id="92f39-230">For example, an application might contain a `Customer` class that defines the properties and methods that any customer object needs.</span></span>
> 
> <span data-ttu-id="92f39-231">Když aplikace potřebuje pracovat se skutečnými informacemi o zákaznících, vytvoří instanci ( *nebo vytvoří instanci) objektu*zákazníka.</span><span class="sxs-lookup"><span data-stu-id="92f39-231">When the application needs to work with actual customer information, it creates an instance of (or *instantiates*) a customer object.</span></span> <span data-ttu-id="92f39-232">Každý jednotlivý zákazník je samostatnou instancí třídy `Customer`.</span><span class="sxs-lookup"><span data-stu-id="92f39-232">Each individual customer is a separate instance of the `Customer` class.</span></span> <span data-ttu-id="92f39-233">Každá instance podporuje stejné vlastnosti a metody, ale hodnoty vlastností každé instance jsou obvykle rozdílné, protože každý objekt zákazníka je jedinečný.</span><span class="sxs-lookup"><span data-stu-id="92f39-233">Every instance supports the same properties and methods, but the property values for each instance are typically different, because each customer object is unique.</span></span> <span data-ttu-id="92f39-234">V jednom objektu zákazníka může být vlastnost `LastName` "Smith"; v jiném objektu zákazníka by vlastnost `LastName` mohla být "Novotný".</span><span class="sxs-lookup"><span data-stu-id="92f39-234">In one customer object, the `LastName` property might be "Smith"; in another customer object, the `LastName` property might be "Jones."</span></span>
> 
> <span data-ttu-id="92f39-235">Podobně je každá jednotlivá webová stránka na vašem webu `Page` objekt, který je instancí třídy `Page`.</span><span class="sxs-lookup"><span data-stu-id="92f39-235">Similarly, any individual web page in your site is a `Page` object that's an instance of the `Page` class.</span></span> <span data-ttu-id="92f39-236">Tlačítko na stránce je objekt `Button`, který je instancí třídy `Button` a tak dále.</span><span class="sxs-lookup"><span data-stu-id="92f39-236">A button on the page is a `Button` object that is an instance of the `Button` class, and so on.</span></span> <span data-ttu-id="92f39-237">Každá instance má své vlastní charakteristiky, ale všechny jsou založeny na tom, co je zadáno v definici třídy objektu.</span><span class="sxs-lookup"><span data-stu-id="92f39-237">Each instance has its own characteristics, but they all are based on what's specified in the object's class definition.</span></span>

## <a name="basic-syntax"></a><span data-ttu-id="92f39-238">Základní syntaxe</span><span class="sxs-lookup"><span data-stu-id="92f39-238">Basic Syntax</span></span>

<span data-ttu-id="92f39-239">Dříve jste viděli základní příklad, jak vytvořit stránku webových stránek ASP.NET a jak můžete přidat serverový kód do kódu HTML.</span><span class="sxs-lookup"><span data-stu-id="92f39-239">Earlier you saw a basic example of how to create an ASP.NET Web Pages page, and how you can add server code to HTML markup.</span></span> <span data-ttu-id="92f39-240">Tady se naučíte základy psaní kódu serveru ASP.NET pomocí syntaxe Razor &#8212; , což jsou pravidla programování.</span><span class="sxs-lookup"><span data-stu-id="92f39-240">Here you'll learn the basics of writing ASP.NET server code using the Razor syntax &#8212; that is, the programming language rules.</span></span>

<span data-ttu-id="92f39-241">Pokud máte zkušenosti s programováním (zejména pokud jste použili C, C++, C#, Visual Basic nebo JavaScript), je většina věcí, kterou si přečtete, dobře známá.</span><span class="sxs-lookup"><span data-stu-id="92f39-241">If you're experienced with programming (especially if you've used C, C++, C#, Visual Basic, or JavaScript), much of what you read here will be familiar.</span></span> <span data-ttu-id="92f39-242">Pravděpodobně budete potřebovat seznámení pouze s tím, jak je serverový kód přidán do značek v souborech *. cshtml* .</span><span class="sxs-lookup"><span data-stu-id="92f39-242">You'll probably need to familiarize yourself only with how server code is added to markup in *.cshtml* files.</span></span>

<a id="BM_CombiningTextMarkupAndCode"></a>
### <a name="combining-text-markup-and-code-in-code-blocks"></a><span data-ttu-id="92f39-243">Kombinování textu, značek a kódu v blocích kódu</span><span class="sxs-lookup"><span data-stu-id="92f39-243">Combining Text, Markup, and Code in Code Blocks</span></span>

<span data-ttu-id="92f39-244">V blocích serverového kódu často chcete na stránku výstup textu nebo značky (nebo obojí).</span><span class="sxs-lookup"><span data-stu-id="92f39-244">In server code blocks, you often want to output text or markup (or both) to the page.</span></span> <span data-ttu-id="92f39-245">Pokud blok kódu serveru obsahuje text, který není kód a místo toho by měl být vykreslen tak, jak je, ASP.NET musí být schopni tento text odlišit od kódu.</span><span class="sxs-lookup"><span data-stu-id="92f39-245">If a server code block contains text that's not code and that instead should be rendered as is, ASP.NET needs to be able to distinguish that text from code.</span></span> <span data-ttu-id="92f39-246">To lze provést několika způsoby.</span><span class="sxs-lookup"><span data-stu-id="92f39-246">There are several ways to do this.</span></span>

- <span data-ttu-id="92f39-247">Vložte text do prvku HTML, jako je `<p></p>` nebo `<em></em>`:</span><span class="sxs-lookup"><span data-stu-id="92f39-247">Enclose the text in an HTML element like `<p></p>` or `<em></em>`:</span></span>   

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample12.cshtml)]

    <span data-ttu-id="92f39-248">Element HTML může obsahovat text, další prvky HTML a výrazy kódu serveru.</span><span class="sxs-lookup"><span data-stu-id="92f39-248">The HTML element can include text, additional HTML elements, and server-code expressions.</span></span> <span data-ttu-id="92f39-249">Když ASP.NET uvidí otevření značky HTML (například `<p>`), vykreslí vše včetně prvku a jeho obsahu tak, jak je do prohlížeče, a překládá výrazy kódu serveru při jejich přechodu.</span><span class="sxs-lookup"><span data-stu-id="92f39-249">When ASP.NET sees the opening HTML tag (for example, `<p>`), it renders everything including the element and its content as is to the browser, resolving server-code expressions as it goes.</span></span>
- <span data-ttu-id="92f39-250">Použijte operátor `@:` nebo prvek `<text>`.</span><span class="sxs-lookup"><span data-stu-id="92f39-250">Use the `@:` operator or the `<text>` element.</span></span> <span data-ttu-id="92f39-251">`@:` vytvoří výstup jednoho řádku obsahu obsahujícího prostý text nebo nespárované značky HTML. element `<text>` obklopuje více řádků do výstupu.</span><span class="sxs-lookup"><span data-stu-id="92f39-251">The `@:` outputs a single line of content containing plain text or unmatched HTML tags; the `<text>` element encloses multiple lines to output.</span></span> <span data-ttu-id="92f39-252">Tyto možnosti jsou užitečné, pokud nechcete vykreslit prvek HTML jako součást výstupu.</span><span class="sxs-lookup"><span data-stu-id="92f39-252">These options are useful when you don't want to render an HTML element as part of the output.</span></span>  

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample13.cshtml)]

    <span data-ttu-id="92f39-253">Pokud chcete výstupovat více řádků textu nebo nespárované značky HTML, můžete před každý řádek zadat `@:`, nebo můžete uzavřít řádek do `<text>` elementu.</span><span class="sxs-lookup"><span data-stu-id="92f39-253">If you want to output multiple lines of text or unmatched HTML tags, you can precede each line with `@:`, or you can enclose the line in a `<text>` element.</span></span> <span data-ttu-id="92f39-254">Podobně jako operátor `@:`, jsou`<text>` značky používány ASP.NET k identifikaci textového obsahu a nejsou nikdy vykresleny ve výstupu stránky.</span><span class="sxs-lookup"><span data-stu-id="92f39-254">Like the `@:` operator,`<text>` tags are used by ASP.NET to identify text content and are never rendered in the page output.</span></span>

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample14.cshtml)]

    <span data-ttu-id="92f39-255">První příklad opakuje předchozí příklad, ale používá jednu dvojici `<text>` značek k uzavření textu, který se má vykreslit.</span><span class="sxs-lookup"><span data-stu-id="92f39-255">The first example repeats the previous example but uses a single pair of `<text>` tags to enclose the text to render.</span></span> <span data-ttu-id="92f39-256">V druhém příkladu jsou značky `<text>` a `</text>` uzavřeny tři řádky, všechny, které obsahují neuzavřený text a nespárované značky HTML (`<br />`), spolu s kódem serveru a odpovídajícími značkami HTML.</span><span class="sxs-lookup"><span data-stu-id="92f39-256">In the second example, the `<text>` and `</text>` tags enclose three lines, all of which have some uncontained text and unmatched HTML tags (`<br />`), along with server code and matched HTML tags.</span></span> <span data-ttu-id="92f39-257">Znovu můžete také předcházet každý řádek jednotlivě pomocí operátoru `@:`; Jak funguje.</span><span class="sxs-lookup"><span data-stu-id="92f39-257">Again, you could also precede each line individually with the `@:` operator; either way works.</span></span>

    > [!NOTE]
    > <span data-ttu-id="92f39-258">Při výstupu textu, jak je znázorněno v &#8212; této části pomocí elementu jazyka HTML, operátoru `@:` nebo elementu &#8212; `<text>` ASP.NET nekóduje výstup do kódu HTML.</span><span class="sxs-lookup"><span data-stu-id="92f39-258">When you output text as shown in this section &#8212; using an HTML element, the `@:` operator, or the `<text>` element &#8212; ASP.NET doesn't HTML-encode the output.</span></span> <span data-ttu-id="92f39-259">(Jak bylo uvedeno dříve, ASP.NET zakóduje výstup výrazů serverového kódu a bloků serverového kódu, které jsou před `@`, s výjimkou zvláštních případů uvedených v této části.)</span><span class="sxs-lookup"><span data-stu-id="92f39-259">(As noted earlier, ASP.NET does encode the output of server code expressions and server code blocks that are preceded by `@`, except in the special cases noted in this section.)</span></span>

### <a name="whitespace"></a><span data-ttu-id="92f39-260">Typy</span><span class="sxs-lookup"><span data-stu-id="92f39-260">Whitespace</span></span>

<span data-ttu-id="92f39-261">Nadbytečné mezery v příkazu (a mimo řetězcový literál) neovlivňují příkaz:</span><span class="sxs-lookup"><span data-stu-id="92f39-261">Extra spaces in a statement (and outside of a string literal) don't affect the statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample15.cshtml)]

<span data-ttu-id="92f39-262">Zalomení řádku v příkazu nemá žádný vliv na příkaz a lze zabalit příkazy pro čitelnost.</span><span class="sxs-lookup"><span data-stu-id="92f39-262">A line break in a statement has no effect on the statement, and you can wrap statements for readability.</span></span> <span data-ttu-id="92f39-263">Následující příkazy jsou stejné:</span><span class="sxs-lookup"><span data-stu-id="92f39-263">The following statements are the same:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample16.cshtml)]

<span data-ttu-id="92f39-264">Nemůžete však obtékat čáru uprostřed řetězcového literálu.</span><span class="sxs-lookup"><span data-stu-id="92f39-264">However, you can't wrap a line in the middle of a string literal.</span></span> <span data-ttu-id="92f39-265">Následující příklad nefunguje:</span><span class="sxs-lookup"><span data-stu-id="92f39-265">The following example doesn't work:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample17.cshtml)]

<span data-ttu-id="92f39-266">Pro kombinování dlouhého řetězce, který se zalomí na více řádků, jako je výše uvedený kód, existují dvě možnosti.</span><span class="sxs-lookup"><span data-stu-id="92f39-266">To combine a long string that wraps to multiple lines like the above code, there are two options.</span></span> <span data-ttu-id="92f39-267">Můžete použít operátor zřetězení (`+`), který uvidíte dále v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="92f39-267">You can use the concatenation operator (`+`), which you'll see later in this article.</span></span> <span data-ttu-id="92f39-268">Můžete také použít `@` znak k vytvoření doslovného řetězcového literálu, jak jste viděli výše v tomto článku.</span><span class="sxs-lookup"><span data-stu-id="92f39-268">You can also use the `@` character to create a verbatim string literal, as you saw earlier in this article.</span></span> <span data-ttu-id="92f39-269">Můžete přerušit doslovné řetězce literálů napříč řádky:</span><span class="sxs-lookup"><span data-stu-id="92f39-269">You can break verbatim string literals across lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample18.cshtml)]

### <a name="code-and-markup-comments"></a><span data-ttu-id="92f39-270">Komentáře kódu (a označení)</span><span class="sxs-lookup"><span data-stu-id="92f39-270">Code (and Markup) Comments</span></span>

<span data-ttu-id="92f39-271">Komentáře umožňují psát si poznámky pro sebe nebo jiné.</span><span class="sxs-lookup"><span data-stu-id="92f39-271">Comments let you leave notes for yourself or others.</span></span> <span data-ttu-id="92f39-272">Také vám umožňují zakázat (*komentovat*) oddíl kódu nebo značky, které nechcete spustit, ale chcete na stránce uchovávat čas.</span><span class="sxs-lookup"><span data-stu-id="92f39-272">They also allow you to disable (*comment out*) a section of code or markup that you don't want to run but want to keep in your page for the time being.</span></span>

<span data-ttu-id="92f39-273">Existuje odlišná syntaxe komentářů pro kód Razor a kód HTML.</span><span class="sxs-lookup"><span data-stu-id="92f39-273">There's different commenting syntax for Razor code and for HTML markup.</span></span> <span data-ttu-id="92f39-274">Stejně jako u všech kódů Razor jsou na serveru zpracovávány komentáře Razor (a poté odstraněny) před odesláním stránky do prohlížeče.</span><span class="sxs-lookup"><span data-stu-id="92f39-274">As with all Razor code, Razor comments are processed (and then removed) on the server before the page is sent to the browser.</span></span> <span data-ttu-id="92f39-275">Proto syntaxe komentářů Razor umožňuje vkládat komentáře do kódu (nebo dokonce do značky), které vidíte při úpravách souboru, ale uživatelé nevidí, i ve zdroji stránky.</span><span class="sxs-lookup"><span data-stu-id="92f39-275">Therefore, the Razor commenting syntax lets you put comments into the code (or even into the markup) that you can see when you edit the file, but that users don't see, even in the page source.</span></span>

<span data-ttu-id="92f39-276">V případě komentářů ASP.NET Razor zahájíte komentář pomocí `@*` a ukončíte ho `*@`.</span><span class="sxs-lookup"><span data-stu-id="92f39-276">For ASP.NET Razor comments, you start the comment with `@*` and end it with `*@`.</span></span> <span data-ttu-id="92f39-277">Komentář může být na jednom řádku nebo několika řádcích:</span><span class="sxs-lookup"><span data-stu-id="92f39-277">The comment can be on one line or multiple lines:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample19.cshtml)]

<span data-ttu-id="92f39-278">Zde je komentář v rámci bloku kódu:</span><span class="sxs-lookup"><span data-stu-id="92f39-278">Here is a comment within a code block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample20.cshtml)]

<span data-ttu-id="92f39-279">Zde je stejný blok kódu, který má řádek s komentářem kódu, aby se nespouštěl:</span><span class="sxs-lookup"><span data-stu-id="92f39-279">Here is the same block of code, with the line of code commented out so that it won't run:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample21.cshtml)]

<span data-ttu-id="92f39-280">V bloku kódu jako alternativu k použití syntaxe komentářů Razor můžete použít syntaxi komentářů programovacího jazyka, který používáte, například C#:</span><span class="sxs-lookup"><span data-stu-id="92f39-280">Inside a code block, as an alternative to using Razor comment syntax, you can use the commenting syntax of the programming language you're using, such as C#:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample22.cshtml)]

<span data-ttu-id="92f39-281">V C#jednom řádku předchází `//` znaků a víceřádkové komentáře začínají `/*` a končí `*/`.</span><span class="sxs-lookup"><span data-stu-id="92f39-281">In C#, single-line comments are preceded by the `//` characters, and multi-line comments begin with `/*` and end with `*/`.</span></span> <span data-ttu-id="92f39-282">(Stejně jako u komentářů Razor C# nejsou komentáře vykreslovány do prohlížeče.)</span><span class="sxs-lookup"><span data-stu-id="92f39-282">(As with Razor comments, C# comments are not rendered to the browser.)</span></span>

<span data-ttu-id="92f39-283">V případě značky, jak budete pravděpodobně znát, můžete vytvořit komentář HTML:</span><span class="sxs-lookup"><span data-stu-id="92f39-283">For markup, as you probably know, you can create an HTML comment:</span></span>

[!code-xml[Main](introducing-razor-syntax-c/samples/sample23.xml)]

<span data-ttu-id="92f39-284">Komentáře HTML začínají `<!--`mi znaky a končí `-->`.</span><span class="sxs-lookup"><span data-stu-id="92f39-284">HTML comments start with `<!--` characters and end with `-->`.</span></span> <span data-ttu-id="92f39-285">K obklopení nejenom textu můžete použít komentáře ve formátu HTML, ale také všechny značky HTML, které můžete chtít na stránce zachovat, ale nechcete je vykreslit.</span><span class="sxs-lookup"><span data-stu-id="92f39-285">You can use HTML comments to surround not only text, but also any HTML markup that you may want to keep in the page but don't want to render.</span></span> <span data-ttu-id="92f39-286">V tomto komentáři HTML se skryje celý obsah značek a text, který obsahují:</span><span class="sxs-lookup"><span data-stu-id="92f39-286">This HTML comment will hide the entire content of the tags and the text they contain:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample24.html)]

<span data-ttu-id="92f39-287">Na rozdíl od komentářů Razor *jsou* komentáře HTML vykresleny na stránku a uživatel je uvidí pomocí zobrazení zdroje stránky.</span><span class="sxs-lookup"><span data-stu-id="92f39-287">Unlike Razor comments, HTML comments *are* rendered to the page and the user can see them by viewing the page source.</span></span>

<span data-ttu-id="92f39-288">Syntaxe Razor má omezení pro vnořené bloky C#.</span><span class="sxs-lookup"><span data-stu-id="92f39-288">Razor has limitations on nested blocks of C#.</span></span> <span data-ttu-id="92f39-289">Další informace najdete v [pojmenovaných C# proměnných a vnořených blocích generuje porušený kód](http://aspnetwebstack.codeplex.com/workitem/1914) .</span><span class="sxs-lookup"><span data-stu-id="92f39-289">For more information see [Named C# Variables and Nested Blocks Generate Broken Code](http://aspnetwebstack.codeplex.com/workitem/1914)</span></span>

## <a name="variables"></a><span data-ttu-id="92f39-290">Proměnné</span><span class="sxs-lookup"><span data-stu-id="92f39-290">Variables</span></span>

<span data-ttu-id="92f39-291">Proměnná je pojmenovaný objekt, který slouží k ukládání dat.</span><span class="sxs-lookup"><span data-stu-id="92f39-291">A variable is a named object that you use to store data.</span></span> <span data-ttu-id="92f39-292">Proměnné můžete pojmenovat cokoli, ale název musí začínat znakem abecedy a nesmí obsahovat mezery ani vyhrazené znaky.</span><span class="sxs-lookup"><span data-stu-id="92f39-292">You can name variables anything, but the name must begin with an alphabetic character and it cannot contain whitespace or reserved characters.</span></span>

### <a name="variables-and-data-types"></a><span data-ttu-id="92f39-293">Proměnné a datové typy</span><span class="sxs-lookup"><span data-stu-id="92f39-293">Variables and Data Types</span></span>

<span data-ttu-id="92f39-294">Proměnná může mít určitý datový typ, který označuje, jaký druh dat je uložený v proměnné.</span><span class="sxs-lookup"><span data-stu-id="92f39-294">A variable can have a specific data type, which indicates what kind of data is stored in the variable.</span></span> <span data-ttu-id="92f39-295">Můžete mít řetězcové proměnné, které ukládají řetězcové hodnoty (například &quot;Hello World&quot;), celočíselné proměnné, které ukládají hodnoty s celými čísly (například 3 nebo 79), a proměnné data uchovávající hodnoty data v různých formátech (například 4/12/2012 nebo březen 2009).</span><span class="sxs-lookup"><span data-stu-id="92f39-295">You can have string variables that store string values (like &quot;Hello world&quot;), integer variables that store whole-number values (like 3 or 79), and date variables that store date values in a variety of formats (like 4/12/2012 or March 2009).</span></span> <span data-ttu-id="92f39-296">A existuje mnoho dalších typů dat, které můžete použít.</span><span class="sxs-lookup"><span data-stu-id="92f39-296">And there are many other data types you can use.</span></span>

<span data-ttu-id="92f39-297">Obecně ale nemusíte zadávat typ pro proměnnou.</span><span class="sxs-lookup"><span data-stu-id="92f39-297">However, you generally don't have to specify a type for a variable.</span></span> <span data-ttu-id="92f39-298">Ve většině času ASP.NET dokáže zjistit typ podle toho, jak se data v proměnné používají.</span><span class="sxs-lookup"><span data-stu-id="92f39-298">Most of the time, ASP.NET can figure out the type based on how the data in the variable is being used.</span></span> <span data-ttu-id="92f39-299">(Někdy musíte zadat typ; uvidíte příklady, kde je to pravda.)</span><span class="sxs-lookup"><span data-stu-id="92f39-299">(Occasionally you must specify a type; you'll see examples where this is true.)</span></span>

<span data-ttu-id="92f39-300">Deklarujete proměnnou pomocí klíčového slova `var` (Pokud nechcete zadat typ) nebo pomocí názvu typu:</span><span class="sxs-lookup"><span data-stu-id="92f39-300">You declare a variable using the `var` keyword (if you don't want to specify a type) or by using the name of the type:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample25.cshtml)]

<span data-ttu-id="92f39-301">Následující příklad ukazuje několik typických použití proměnných na webové stránce:</span><span class="sxs-lookup"><span data-stu-id="92f39-301">The following example shows some typical uses of variables in a web page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample26.cshtml)]

<span data-ttu-id="92f39-302">Pokud na stránce zkombinujete předchozí příklady, zobrazí se v prohlížeči:</span><span class="sxs-lookup"><span data-stu-id="92f39-302">If you combine the previous examples in a page, you see this displayed in a browser:</span></span>

![Razor-Img9](introducing-razor-syntax-c/_static/image9.jpg)

### <a name="converting-and-testing-data-types"></a><span data-ttu-id="92f39-304">Převod a testování datových typů</span><span class="sxs-lookup"><span data-stu-id="92f39-304">Converting and Testing Data Types</span></span>

<span data-ttu-id="92f39-305">I když ASP.NET může obvykle určit datový typ automaticky, někdy to nemůže.</span><span class="sxs-lookup"><span data-stu-id="92f39-305">Although ASP.NET can usually determine a data type automatically, sometimes it can't.</span></span> <span data-ttu-id="92f39-306">Proto může být nutné pomáhat s ASP.NETm při provádění explicitního převodu.</span><span class="sxs-lookup"><span data-stu-id="92f39-306">Therefore, you might need to help ASP.NET out by performing an explicit conversion.</span></span> <span data-ttu-id="92f39-307">I v případě, že není nutné převést typy, někdy je vhodné otestovat a zjistit, se kterými typem dat pracujete.</span><span class="sxs-lookup"><span data-stu-id="92f39-307">Even if you don't have to convert types, sometimes it's helpful to test to see what type of data you might be working with.</span></span>

<span data-ttu-id="92f39-308">Nejběžnějším případem je, že je nutné převést řetězec na jiný typ, jako je například na celé číslo nebo datum.</span><span class="sxs-lookup"><span data-stu-id="92f39-308">The most common case is that you have to convert a string to another type, such as to an integer or date.</span></span> <span data-ttu-id="92f39-309">Následující příklad ukazuje typický případ, kdy je nutné převést řetězec na číslo.</span><span class="sxs-lookup"><span data-stu-id="92f39-309">The following example shows a typical case where you must convert a string to a number.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample27.cshtml)]

<span data-ttu-id="92f39-310">Jako pravidlo se vstup uživatele dostane jako řetězce.</span><span class="sxs-lookup"><span data-stu-id="92f39-310">As a rule, user input comes to you as strings.</span></span> <span data-ttu-id="92f39-311">I když jste si vyzkoušeli, že uživatel zadal číslo, a to i v případě, že zadali číslici, když se odešle vstup uživatele a přečtete ho v kódu, data jsou ve formátu řetězce.</span><span class="sxs-lookup"><span data-stu-id="92f39-311">Even if you've prompted users to enter a number, and even if they've entered a digit, when user input is submitted and you read it in code, the data is in string format.</span></span> <span data-ttu-id="92f39-312">Proto je nutné převést řetězec na číslo.</span><span class="sxs-lookup"><span data-stu-id="92f39-312">Therefore, you must convert the string to a number.</span></span> <span data-ttu-id="92f39-313">Pokud se v příkladu pokusíte provést aritmetické operace s hodnotami bez jejich převádění, dojde k následující chybě, protože ASP.NET nemůže přidat dva řetězce:</span><span class="sxs-lookup"><span data-stu-id="92f39-313">In the example, if you try to perform arithmetic on the values without converting them, the following error results, because ASP.NET cannot add two strings:</span></span>

<span data-ttu-id="92f39-314">*Typ String nejde implicitně převést na int.*</span><span class="sxs-lookup"><span data-stu-id="92f39-314">*Cannot implicitly convert type 'string' to 'int'.*</span></span>

<span data-ttu-id="92f39-315">Chcete-li převést hodnoty na celá čísla, zavolejte metodu `AsInt`.</span><span class="sxs-lookup"><span data-stu-id="92f39-315">To convert the values to integers, you call the `AsInt` method.</span></span> <span data-ttu-id="92f39-316">Pokud je převod úspěšný, můžete čísla přidat.</span><span class="sxs-lookup"><span data-stu-id="92f39-316">If the conversion is successful, you can then add the numbers.</span></span>

<span data-ttu-id="92f39-317">V následující tabulce jsou uvedeny některé běžné metody převodu a testování pro proměnné.</span><span class="sxs-lookup"><span data-stu-id="92f39-317">The following table lists some common conversion and test methods for variables.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="92f39-318"><strong>Metoda</strong></span><span class="sxs-lookup"><span data-stu-id="92f39-318"><strong>Method</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="92f39-319"><strong>Popis</strong></span><span class="sxs-lookup"><span data-stu-id="92f39-319"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="92f39-320"><strong>Příklad</strong></span><span class="sxs-lookup"><span data-stu-id="92f39-320"><strong>Example</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        `AsInt(), IsInt()`
    :::column-end:::
    :::column:::
    <span data-ttu-id="92f39-321">Převede řetězec představující celé číslo (například "593") na celé číslo.</span><span class="sxs-lookup"><span data-stu-id="92f39-321">Converts a string that represents a whole number (like "593") to an integer.</span></span>
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
    <span data-ttu-id="92f39-322">Převede řetězec jako &quot;true&quot; nebo &quot;false&quot; na typ Boolean.</span><span class="sxs-lookup"><span data-stu-id="92f39-322">Converts a string like &quot;true&quot; or &quot;false&quot; to a Boolean type.</span></span>
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
    <span data-ttu-id="92f39-323">Převede řetězec, který má hodnotu typu Decimal, například &quot;1,3&quot; nebo &quot;7,439&quot; na číslo s plovoucí desetinnou čárkou.</span><span class="sxs-lookup"><span data-stu-id="92f39-323">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a floating-point number.</span></span>
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
    <span data-ttu-id="92f39-324">Převede řetězec, který má hodnotu typu Decimal, například &quot;1,3&quot; nebo &quot;7,439&quot; na desetinné číslo.</span><span class="sxs-lookup"><span data-stu-id="92f39-324">Converts a string that has a decimal value like &quot;1.3&quot; or &quot;7.439&quot; to a decimal number.</span></span> <span data-ttu-id="92f39-325">(V ASP.NET je desetinné číslo přesnější než číslo s plovoucí desetinnou čárkou.)</span><span class="sxs-lookup"><span data-stu-id="92f39-325">(In ASP.NET, a decimal number is more precise than a floating-point number.)</span></span>
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
    <span data-ttu-id="92f39-326">Převede řetězec, který představuje hodnotu data a času na ASP.NET typ `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="92f39-326">Converts a string that represents a date and time value to the ASP.NET `DateTime` type.</span></span>
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
    <span data-ttu-id="92f39-327">Převede jakýkoli jiný datový typ na řetězec.</span><span class="sxs-lookup"><span data-stu-id="92f39-327">Converts any other data type to a string.</span></span>
    :::column-end:::
    :::column:::
        [!code-javascript[Main](introducing-razor-syntax-c/samples/sample33.js)]
    :::column-end:::
:::row-end:::

## <a name="operators"></a><span data-ttu-id="92f39-328">Operátory</span><span class="sxs-lookup"><span data-stu-id="92f39-328">Operators</span></span>

<span data-ttu-id="92f39-329">Operátor je klíčové slovo nebo znak, který oznamuje ASP.NET, jaký druh příkazu má být proveden ve výrazu.</span><span class="sxs-lookup"><span data-stu-id="92f39-329">An operator is a keyword or character that tells ASP.NET what kind of command to perform in an expression.</span></span> <span data-ttu-id="92f39-330">C# Jazyk (a syntaxe Razor, který je na něm založen), podporuje mnoho operátorů, ale stačí, abyste pomohli jenom rozpoznat pár, abyste mohli začít.</span><span class="sxs-lookup"><span data-stu-id="92f39-330">The C# language (and the Razor syntax that's based on it) supports many operators, but you only need to recognize a few to get started.</span></span> <span data-ttu-id="92f39-331">Následující tabulka shrnuje nejběžnější operátory.</span><span class="sxs-lookup"><span data-stu-id="92f39-331">The following table summarizes the most common operators.</span></span>

:::row:::
    :::column:::
    <span data-ttu-id="92f39-332"><strong>Podnikatel</strong></span><span class="sxs-lookup"><span data-stu-id="92f39-332"><strong>Operator</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="92f39-333"><strong>Popis</strong></span><span class="sxs-lookup"><span data-stu-id="92f39-333"><strong>Description</strong></span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="92f39-334"><strong>Příklady</strong></span><span class="sxs-lookup"><span data-stu-id="92f39-334"><strong>Examples</strong></span></span>
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="92f39-335">`+` `-` `*` `/`</span><span class="sxs-lookup"><span data-stu-id="92f39-335">`+` `-` `*` `/`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="92f39-336">Matematické operátory používané v numerických výrazech.</span><span class="sxs-lookup"><span data-stu-id="92f39-336">Math operators used in numerical expressions.</span></span>
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
    <span data-ttu-id="92f39-337">Přiřazení.</span><span class="sxs-lookup"><span data-stu-id="92f39-337">Assignment.</span></span> <span data-ttu-id="92f39-338">Přiřadí hodnotu na pravé straně příkazu k objektu na levé straně.</span><span class="sxs-lookup"><span data-stu-id="92f39-338">Assigns the value on the right side of a statement to the object on the left side.</span></span>
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
    <span data-ttu-id="92f39-339">Porovnávání.</span><span class="sxs-lookup"><span data-stu-id="92f39-339">Equality.</span></span> <span data-ttu-id="92f39-340">Vrátí `true`, pokud jsou hodnoty stejné.</span><span class="sxs-lookup"><span data-stu-id="92f39-340">Returns `true` if the values are equal.</span></span> <span data-ttu-id="92f39-341">(Všimněte si rozdílu mezi operátorem `=` a operátorem `==`.)</span><span class="sxs-lookup"><span data-stu-id="92f39-341">(Notice the distinction between the `=` operator and the `==` operator.)</span></span>
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
    <span data-ttu-id="92f39-342">Nerovnost.</span><span class="sxs-lookup"><span data-stu-id="92f39-342">Inequality.</span></span> <span data-ttu-id="92f39-343">Vrátí `true`, pokud se hodnoty neshodují.</span><span class="sxs-lookup"><span data-stu-id="92f39-343">Returns `true` if the values are not equal.</span></span>
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
    <span data-ttu-id="92f39-344">Menší než, větší než, menší než nebo rovno, a větší než nebo rovno.</span><span class="sxs-lookup"><span data-stu-id="92f39-344">Less-than, greater-than, less-than-or-equal, and greater-than-or-equal.</span></span>
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
    <span data-ttu-id="92f39-345">Zřetězení, které se používá k spojování řetězců.</span><span class="sxs-lookup"><span data-stu-id="92f39-345">Concatenation, which is used to join strings.</span></span> <span data-ttu-id="92f39-346">ASP.NET ví rozdíl mezi tímto operátorem a operátorem sčítání na základě datového typu výrazu.</span><span class="sxs-lookup"><span data-stu-id="92f39-346">ASP.NET knows the difference between this operator and the addition operator based on the data type of the expression.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample39.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="92f39-347">`+=` `-=`</span><span class="sxs-lookup"><span data-stu-id="92f39-347">`+=` `-=`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="92f39-348">Operátory přírůstku a snížení, které přidají a odečtou 1 (v uvedeném pořadí) z proměnné.</span><span class="sxs-lookup"><span data-stu-id="92f39-348">The increment and decrement operators, which add and subtract 1 (respectively) from a variable.</span></span>
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
    <span data-ttu-id="92f39-349">Tečka.</span><span class="sxs-lookup"><span data-stu-id="92f39-349">Dot.</span></span> <span data-ttu-id="92f39-350">Slouží k rozlišení objektů a jejich vlastností a metod.</span><span class="sxs-lookup"><span data-stu-id="92f39-350">Used to distinguish objects and their properties and methods.</span></span>
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
    <span data-ttu-id="92f39-351">Závorky.</span><span class="sxs-lookup"><span data-stu-id="92f39-351">Parentheses.</span></span> <span data-ttu-id="92f39-352">Slouží k seskupení výrazů a předání parametrů metodám.</span><span class="sxs-lookup"><span data-stu-id="92f39-352">Used to group expressions and to pass parameters to methods.</span></span>
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
    <span data-ttu-id="92f39-353">Hranat.</span><span class="sxs-lookup"><span data-stu-id="92f39-353">Brackets.</span></span> <span data-ttu-id="92f39-354">Používá se pro přístup k hodnotám v polích nebo kolekcích.</span><span class="sxs-lookup"><span data-stu-id="92f39-354">Used for accessing values in arrays or collections.</span></span>
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
    <span data-ttu-id="92f39-355">Mění.</span><span class="sxs-lookup"><span data-stu-id="92f39-355">Not.</span></span> <span data-ttu-id="92f39-356">Obrátí `true` hodnotu na `false` a naopak.</span><span class="sxs-lookup"><span data-stu-id="92f39-356">Reverses a `true` value to `false` and vice versa.</span></span> <span data-ttu-id="92f39-357">Obvykle se používá jako zkrácený způsob testování pro `false` (tj. není-li `true`).</span><span class="sxs-lookup"><span data-stu-id="92f39-357">Typically used as a shorthand way to test for `false` (that is, for not `true`).</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample44.cs)]
    :::column-end:::
:::row-end:::

---

:::row:::
    :::column:::
        <span data-ttu-id="92f39-358">`&&` `||`</span><span class="sxs-lookup"><span data-stu-id="92f39-358">`&&` `||`</span></span>
    :::column-end:::
    :::column:::
    <span data-ttu-id="92f39-359">Logický operátor AND a OR, který se používá k propojení podmínek.</span><span class="sxs-lookup"><span data-stu-id="92f39-359">Logical AND and OR, which are used to link conditions together.</span></span>
    :::column-end:::
    :::column:::
        [!code-csharp[Main](introducing-razor-syntax-c/samples/sample45.cs)]
    :::column-end:::
:::row-end:::

<a id="ID_WorkingWithFileAndFolderPaths"></a>
## <a name="working-with-file-and-folder-paths-in-code"></a><span data-ttu-id="92f39-360">Práce s cestami k souborům a složkám v kódu</span><span class="sxs-lookup"><span data-stu-id="92f39-360">Working with File and Folder Paths in Code</span></span>

<span data-ttu-id="92f39-361">V kódu často budete pracovat s cestami k souborům a složkám.</span><span class="sxs-lookup"><span data-stu-id="92f39-361">You'll often work with file and folder paths in your code.</span></span> <span data-ttu-id="92f39-362">Tady je příklad fyzické struktury složek pro web, jak se může zobrazit na vašem vývojovém počítači:</span><span class="sxs-lookup"><span data-stu-id="92f39-362">Here is an example of physical folder structure for a website as it might appear on your development computer:</span></span>

`C:\WebSites\MyWebSite default.cshtml datafile.txt \images Logo.jpg \styles Styles.css`

<span data-ttu-id="92f39-363">Tady jsou některé důležité informace o adresách URL a cestách:</span><span class="sxs-lookup"><span data-stu-id="92f39-363">Here are some essential details about URLs and paths:</span></span>

- <span data-ttu-id="92f39-364">Adresa URL začíná buď s názvem domény (`http://www.example.com`), nebo s názvem serveru (`http://localhost`, `http://mycomputer`).</span><span class="sxs-lookup"><span data-stu-id="92f39-364">A URL begins with either a domain name (`http://www.example.com`) or a server name (`http://localhost`, `http://mycomputer`).</span></span>
- <span data-ttu-id="92f39-365">Adresa URL odpovídá fyzické cestě na hostitelském počítači.</span><span class="sxs-lookup"><span data-stu-id="92f39-365">A URL corresponds to a physical path on a host computer.</span></span> <span data-ttu-id="92f39-366">`http://myserver` například může odpovídat složce *C:\websites\mywebsite* na serveru.</span><span class="sxs-lookup"><span data-stu-id="92f39-366">For example, `http://myserver` might correspond to the folder *C:\websites\mywebsite* on the server.</span></span>
- <span data-ttu-id="92f39-367">Virtuální cesta je zkrácený pro reprezentaci cest v kódu bez nutnosti zadat úplnou cestu.</span><span class="sxs-lookup"><span data-stu-id="92f39-367">A virtual path is shorthand to represent paths in code without having to specify the full path.</span></span> <span data-ttu-id="92f39-368">Obsahuje část adresy URL, která následuje za názvem domény nebo serveru.</span><span class="sxs-lookup"><span data-stu-id="92f39-368">It includes the portion of a URL that follows the domain or server name.</span></span> <span data-ttu-id="92f39-369">Pokud používáte virtuální cesty, můžete svůj kód přesunout do jiné domény nebo serveru, aniž byste museli cesty aktualizovat.</span><span class="sxs-lookup"><span data-stu-id="92f39-369">When you use virtual paths, you can move your code to a different domain or server without having to update the paths.</span></span>

<span data-ttu-id="92f39-370">Tady je příklad, který vám pomůže pochopit rozdíly:</span><span class="sxs-lookup"><span data-stu-id="92f39-370">Here's an example to help you understand the differences:</span></span>

| <span data-ttu-id="92f39-371">Úplná adresa URL</span><span class="sxs-lookup"><span data-stu-id="92f39-371">Complete URL</span></span> | `http://mycompanyserver/humanresources/CompanyPolicy.htm` |
| --- | --- |
| <span data-ttu-id="92f39-372">Název serveru</span><span class="sxs-lookup"><span data-stu-id="92f39-372">Server name</span></span> | <span data-ttu-id="92f39-373">*mycompanyserver*</span><span class="sxs-lookup"><span data-stu-id="92f39-373">*mycompanyserver*</span></span> |
| <span data-ttu-id="92f39-374">Virtuální cesta</span><span class="sxs-lookup"><span data-stu-id="92f39-374">Virtual path</span></span> | <span data-ttu-id="92f39-375">*/humanresources/CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="92f39-375">*/humanresources/CompanyPolicy.htm*</span></span> |
| <span data-ttu-id="92f39-376">Fyzická cesta</span><span class="sxs-lookup"><span data-stu-id="92f39-376">Physical path</span></span> | <span data-ttu-id="92f39-377">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span><span class="sxs-lookup"><span data-stu-id="92f39-377">*C:\mywebsites\humanresources\CompanyPolicy.htm*</span></span> |

<span data-ttu-id="92f39-378">Virtuální kořenový adresář je/, stejně jako kořenový adresář vaší jednotky C:.</span><span class="sxs-lookup"><span data-stu-id="92f39-378">The virtual root is /, just like the root of your C: drive is \.</span></span> <span data-ttu-id="92f39-379">(Cesty k virtuálním složkám vždycky používají lomítka.) Virtuální cesta ke složce nemusí mít stejný název jako fyzická složka; může to být alias.</span><span class="sxs-lookup"><span data-stu-id="92f39-379">(Virtual folder paths always use forward slashes.) The virtual path of a folder doesn't have to have the same name as the physical folder; it can be an alias.</span></span> <span data-ttu-id="92f39-380">(Na provozních serverech se virtuální cesta zřídka shoduje s přesnou fyzickou cestou.)</span><span class="sxs-lookup"><span data-stu-id="92f39-380">(On production servers, the virtual path rarely matches an exact physical path.)</span></span>

<span data-ttu-id="92f39-381">Když pracujete se soubory a složkami v kódu, někdy potřebujete odkazovat na fyzickou cestu a někdy na virtuální cestu v závislosti na objektech, se kterými pracujete.</span><span class="sxs-lookup"><span data-stu-id="92f39-381">When you work with files and folders in code, sometimes you need to reference the physical path and sometimes a virtual path, depending on what objects you're working with.</span></span> <span data-ttu-id="92f39-382">ASP.NET poskytuje tyto nástroje pro práci s cestami k souborům a složkám v kódu: metoda `Server.MapPath` a operátor `~` a metoda `Href`.</span><span class="sxs-lookup"><span data-stu-id="92f39-382">ASP.NET gives you these tools for working with file and folder paths in code: the `Server.MapPath` method, and the `~` operator and `Href` method.</span></span>

### <a name="converting-virtual-to-physical-paths-the-servermappath-method"></a><span data-ttu-id="92f39-383">Převod virtuálních na fyzické cesty: Metoda Server. MapPath</span><span class="sxs-lookup"><span data-stu-id="92f39-383">Converting virtual to physical paths: the Server.MapPath method</span></span>

<span data-ttu-id="92f39-384">Metoda `Server.MapPath` Převede virtuální cestu (například */Default.cshtml*) na absolutní fyzickou cestu (například *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span><span class="sxs-lookup"><span data-stu-id="92f39-384">The `Server.MapPath` method converts a virtual path (like */default.cshtml*) to an absolute physical path (like *C:\WebSites\MyWebSiteFolder\default.cshtml*).</span></span> <span data-ttu-id="92f39-385">Tuto metodu použijete kdykoli, když potřebujete úplnou fyzickou cestu.</span><span class="sxs-lookup"><span data-stu-id="92f39-385">You use this method any time you need a complete physical path.</span></span> <span data-ttu-id="92f39-386">Typickým příkladem je, že načítáte nebo píšete textový soubor nebo soubor obrázku na webovém serveru.</span><span class="sxs-lookup"><span data-stu-id="92f39-386">A typical example is when you're reading or writing a text file or image file on the web server.</span></span>

<span data-ttu-id="92f39-387">Obvykle neznáte absolutní fyzickou cestu k webu na serveru hostujícího webu, takže tato metoda může převést cestu, kterou znáte – virtuální cestu – k odpovídající cestě na serveru za vás.</span><span class="sxs-lookup"><span data-stu-id="92f39-387">You typically don't know the absolute physical path of your site on a hosting site's server, so this method can convert the path you do know — the virtual path — to the corresponding path on the server for you.</span></span> <span data-ttu-id="92f39-388">Do metody předáte virtuální cestu k souboru nebo složce a vrátíte fyzickou cestu:</span><span class="sxs-lookup"><span data-stu-id="92f39-388">You pass the virtual path to a file or folder to the method, and it returns the physical path:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample46.cshtml)]

### <a name="referencing-the-virtual-root-the--operator-and-href-method"></a><span data-ttu-id="92f39-389">Odkazování na virtuální kořenový adresář: operátor ~ a metoda href</span><span class="sxs-lookup"><span data-stu-id="92f39-389">Referencing the virtual root: the ~ operator and Href method</span></span>

<span data-ttu-id="92f39-390">V souboru *. cshtml* nebo *. vbhtml* můžete odkazovat na virtuální kořenovou cestu pomocí operátoru `~`.</span><span class="sxs-lookup"><span data-stu-id="92f39-390">In a *.cshtml* or *.vbhtml* file, you can reference the virtual root path using the `~` operator.</span></span> <span data-ttu-id="92f39-391">To je velmi užitečné, protože můžete přesouvat stránky v lokalitě a jakékoli odkazy, které obsahují na jiné stránky, nebudou přerušeny.</span><span class="sxs-lookup"><span data-stu-id="92f39-391">This is very handy because you can move pages around in a site, and any links they contain to other pages won't be broken.</span></span> <span data-ttu-id="92f39-392">K dispozici je také užitečné v případě, že jste web někdy přesunuli do jiného umístění.</span><span class="sxs-lookup"><span data-stu-id="92f39-392">It's also handy in case you ever move your website to a different location.</span></span> <span data-ttu-id="92f39-393">Zde je několik příkladů:</span><span class="sxs-lookup"><span data-stu-id="92f39-393">Here are some examples:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample47.cshtml)]

<span data-ttu-id="92f39-394">Pokud je web `http://myserver/myapp`, v takovém případě bude ASP.NET považovat tyto cesty při spuštění stránky:</span><span class="sxs-lookup"><span data-stu-id="92f39-394">If the website is `http://myserver/myapp`, here's how ASP.NET will treat these paths when the page runs:</span></span>

- <span data-ttu-id="92f39-395">`myImagesFolder`: `http://myserver/myapp/images`</span><span class="sxs-lookup"><span data-stu-id="92f39-395">`myImagesFolder`: `http://myserver/myapp/images`</span></span>
- <span data-ttu-id="92f39-396">`myStyleSheet`: `http://myserver/myapp/styles/Stylesheet.css`</span><span class="sxs-lookup"><span data-stu-id="92f39-396">`myStyleSheet` : `http://myserver/myapp/styles/Stylesheet.css`</span></span>

<span data-ttu-id="92f39-397">(Tyto cesty ve skutečnosti neuvidíte jako hodnoty proměnné, ale ASP.NET je bude považovat za to, co byly.)</span><span class="sxs-lookup"><span data-stu-id="92f39-397">(You won't actually see these paths as the values of the variable, but ASP.NET will treat the paths as if that's what they were.)</span></span>

<span data-ttu-id="92f39-398">Operátor `~` lze použít jak v kódu serveru (jak je uvedeno výše), tak v označení, například takto:</span><span class="sxs-lookup"><span data-stu-id="92f39-398">You can use the `~` operator both in server code (as above) and in markup, like this:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample48.html)]

<span data-ttu-id="92f39-399">V kódu se používá operátor `~` k vytváření cest k prostředkům, jako jsou soubory obrázků, jiné webové stránky a soubory CSS.</span><span class="sxs-lookup"><span data-stu-id="92f39-399">In markup, you use the `~` operator to create paths to resources like image files, other web pages, and CSS files.</span></span> <span data-ttu-id="92f39-400">Po spuštění stránky ASP.NET vyhledá stránku (kód i kód) a přeloží všechny `~` odkazy na příslušnou cestu.</span><span class="sxs-lookup"><span data-stu-id="92f39-400">When the page runs, ASP.NET looks through the page (both code and markup) and resolves all the `~` references to the appropriate path.</span></span>

## <a name="conditional-logic-and-loops"></a><span data-ttu-id="92f39-401">Podmíněná logika a smyčky</span><span class="sxs-lookup"><span data-stu-id="92f39-401">Conditional Logic and Loops</span></span>

<span data-ttu-id="92f39-402">Kód serveru ASP.NET vám umožňuje provádět úlohy na základě podmínek a napsat kód, který opakuje příkazy, a to podle určitého počtu, kolikrát (tj. kód spouštějící smyčku).</span><span class="sxs-lookup"><span data-stu-id="92f39-402">ASP.NET server code lets you perform tasks based on conditions and write code that repeats statements a specific number of times (that is, code that runs a loop).</span></span>

### <a name="testing-conditions"></a><span data-ttu-id="92f39-403">Podmínky testování</span><span class="sxs-lookup"><span data-stu-id="92f39-403">Testing Conditions</span></span>

<span data-ttu-id="92f39-404">Chcete-li otestovat jednoduchou podmínku, použijte příkaz `if`, který vrací hodnotu true nebo false na základě testu, který zadáte:</span><span class="sxs-lookup"><span data-stu-id="92f39-404">To test a simple condition you use the `if` statement, which returns true or false based on a test you specify:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample49.cshtml)]

<span data-ttu-id="92f39-405">Klíčové slovo `if` spustí blok.</span><span class="sxs-lookup"><span data-stu-id="92f39-405">The `if` keyword starts a block.</span></span> <span data-ttu-id="92f39-406">Skutečný test (podmínka) je v závorkách a vrátí hodnotu true nebo false.</span><span class="sxs-lookup"><span data-stu-id="92f39-406">The actual test (condition) is in parentheses and returns true or false.</span></span> <span data-ttu-id="92f39-407">Příkazy, které se spustí, pokud je test true, jsou uzavřeny ve složených závorkách.</span><span class="sxs-lookup"><span data-stu-id="92f39-407">The statements that run if the test is true are enclosed in braces.</span></span> <span data-ttu-id="92f39-408">Příkaz `if` může zahrnovat blok `else`, který určuje příkazy, které se mají spustit, pokud je podmínka nepravdivá:</span><span class="sxs-lookup"><span data-stu-id="92f39-408">An `if` statement can include an `else` block that specifies statements to run if the condition is false:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample50.cshtml)]

<span data-ttu-id="92f39-409">Pomocí `else if`ového bloku můžete přidat víc podmínek:</span><span class="sxs-lookup"><span data-stu-id="92f39-409">You can add multiple conditions using an `else if` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample51.cshtml)]

<span data-ttu-id="92f39-410">V tomto příkladu, pokud není první podmínka v bloku If nastavena na hodnotu true, je zaškrtnuta podmínka `else if`.</span><span class="sxs-lookup"><span data-stu-id="92f39-410">In this example, if the first condition in the if block is not true, the `else if` condition is checked.</span></span> <span data-ttu-id="92f39-411">Pokud je tato podmínka splněna, jsou provedeny příkazy v bloku `else if`.</span><span class="sxs-lookup"><span data-stu-id="92f39-411">If that condition is met, the statements in the `else if` block are executed.</span></span> <span data-ttu-id="92f39-412">Pokud není splněna žádná z podmínek, jsou provedeny příkazy v bloku `else`.</span><span class="sxs-lookup"><span data-stu-id="92f39-412">If none of the conditions are met, the statements in the `else` block are executed.</span></span> <span data-ttu-id="92f39-413">Můžete přidat libovolný počet else if Blocks a pak zavřít s `else` blok jako &quot;vše jiného&quot; podmínka.</span><span class="sxs-lookup"><span data-stu-id="92f39-413">You can add any number of else if blocks, and then close with an `else` block as the &quot;everything else&quot; condition.</span></span>

<span data-ttu-id="92f39-414">K otestování velkého počtu podmínek použijte `switch` blok:</span><span class="sxs-lookup"><span data-stu-id="92f39-414">To test a large number of conditions, use a `switch` block:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample52.cshtml)]

<span data-ttu-id="92f39-415">Hodnota, která se má testovat, je v závorkách (v příkladu `weekday` proměnné).</span><span class="sxs-lookup"><span data-stu-id="92f39-415">The value to test is in parentheses (in the example, the `weekday` variable).</span></span> <span data-ttu-id="92f39-416">Každý jednotlivý test používá příkaz `case`, který končí dvojtečkou (:).</span><span class="sxs-lookup"><span data-stu-id="92f39-416">Each individual test uses a `case` statement that ends with a colon (:).</span></span> <span data-ttu-id="92f39-417">Je-li hodnota příkazu `case` shodná s testovací hodnotou, je proveden kód v tomto bloku případu.</span><span class="sxs-lookup"><span data-stu-id="92f39-417">If the value of a `case` statement matches the test value, the code in that case block is executed.</span></span> <span data-ttu-id="92f39-418">Všechny příkazy Case zavřete příkazem `break`.</span><span class="sxs-lookup"><span data-stu-id="92f39-418">You close each case statement with a `break` statement.</span></span> <span data-ttu-id="92f39-419">(Pokud zapomenete zahrnout do každého bloku `case`, kód z dalšího příkazu `case` se spustí také.) `switch` blok často obsahuje `default` příkaz jako poslední případ pro &quot;vše ostatní&quot; možnost, která se spustí, pokud žádný z ostatních případů neplatí.</span><span class="sxs-lookup"><span data-stu-id="92f39-419">(If you forget to include break in each `case` block, the code from the next `case` statement will run also.) A `switch` block often has a `default` statement as the last case for an &quot;everything else&quot; option that runs if none of the other cases are true.</span></span>

<span data-ttu-id="92f39-420">Výsledek posledního dvou podmíněných bloků zobrazených v prohlížeči:</span><span class="sxs-lookup"><span data-stu-id="92f39-420">The result of the last two conditional blocks displayed in a browser:</span></span>

![Razor – Img10](introducing-razor-syntax-c/_static/image10.jpg)

### <a name="looping-code"></a><span data-ttu-id="92f39-422">Kód smyčky</span><span class="sxs-lookup"><span data-stu-id="92f39-422">Looping Code</span></span>

<span data-ttu-id="92f39-423">Často je třeba spouštět stejné příkazy opakovaně.</span><span class="sxs-lookup"><span data-stu-id="92f39-423">You often need to run the same statements repeatedly.</span></span> <span data-ttu-id="92f39-424">Provedete to pomocí smyčky.</span><span class="sxs-lookup"><span data-stu-id="92f39-424">You do this by looping.</span></span> <span data-ttu-id="92f39-425">Například často spustíte stejné příkazy pro každou položku v kolekci dat.</span><span class="sxs-lookup"><span data-stu-id="92f39-425">For example, you often run the same statements for each item in a collection of data.</span></span> <span data-ttu-id="92f39-426">Pokud víte přesně, kolikrát chcete cyklovat, můžete použít smyčku `for`.</span><span class="sxs-lookup"><span data-stu-id="92f39-426">If you know exactly how many times you want to loop, you can use a `for` loop.</span></span> <span data-ttu-id="92f39-427">Tento druh smyčky je zvláště užitečný pro inventarizaci a počítání:</span><span class="sxs-lookup"><span data-stu-id="92f39-427">This kind of loop is especially useful for counting up or counting down:</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample53.html)]

<span data-ttu-id="92f39-428">Smyčka začíná klíčovým slovem `for`, po kterém následují tři příkazy v závorkách, přičemž každý z nich končí středníkem.</span><span class="sxs-lookup"><span data-stu-id="92f39-428">The loop begins with the `for` keyword, followed by three statements in parentheses, each terminated with a semicolon.</span></span>

- <span data-ttu-id="92f39-429">V závorkách první příkaz (`var i=10;`) vytvoří čítač a inicializuje jej na hodnotu 10.</span><span class="sxs-lookup"><span data-stu-id="92f39-429">Inside the parentheses, the first statement (`var i=10;`) creates a counter and initializes it to 10.</span></span> <span data-ttu-id="92f39-430">Nemusíte pojmenovat `i` &#8212; čítače. můžete použít libovolnou proměnnou.</span><span class="sxs-lookup"><span data-stu-id="92f39-430">You don't have to name the counter `i` &#8212; you can use any variable.</span></span> <span data-ttu-id="92f39-431">Po spuštění smyčky `for` se čítač automaticky zvýší.</span><span class="sxs-lookup"><span data-stu-id="92f39-431">When the `for` loop runs, the counter is automatically incremented.</span></span>
- <span data-ttu-id="92f39-432">Druhý příkaz (`i < 21;`) nastaví podmínku pro jak daleko chcete počítat.</span><span class="sxs-lookup"><span data-stu-id="92f39-432">The second statement (`i < 21;`) sets the condition for how far you want to count.</span></span> <span data-ttu-id="92f39-433">V takovém případě chcete, aby bylo možné přejít maximálně o 20 (to znamená, že bude pokračovat i v případě, že je čítač menší než 21).</span><span class="sxs-lookup"><span data-stu-id="92f39-433">In this case, you want it to go to a maximum of 20 (that is, keep going while the counter is less than 21).</span></span>
- <span data-ttu-id="92f39-434">Třetí příkaz (`i++`) používá operátor přírůstek, který jednoduše určuje, že čítač by měl mít 1 přidaný čítač při každém spuštění smyčky.</span><span class="sxs-lookup"><span data-stu-id="92f39-434">The third statement (`i++` ) uses an increment operator, which simply specifies that the counter should have 1 added to it each time the loop runs.</span></span>

<span data-ttu-id="92f39-435">Uvnitř složených závorek je kód, který se spustí pro každou iteraci smyčky.</span><span class="sxs-lookup"><span data-stu-id="92f39-435">Inside the braces is the code that will run for each iteration of the loop.</span></span> <span data-ttu-id="92f39-436">Kód vytvoří nový odstavec (`<p>` element) pokaždé a přidá řádek do výstupu a zobrazí hodnotu `i` (čítač).</span><span class="sxs-lookup"><span data-stu-id="92f39-436">The markup creates a new paragraph (`<p>` element) each time and adds a line to the output, displaying the value of `i` (the counter).</span></span> <span data-ttu-id="92f39-437">Když spustíte tuto stránku, v příkladu se vytvoří 11 řádků, ve kterých se zobrazí výstup, a text na každém řádku, který označuje číslo položky.</span><span class="sxs-lookup"><span data-stu-id="92f39-437">When you run this page, the example creates 11 lines displaying the output, with the text in each line indicating the item number.</span></span>

![Razor-Img11](introducing-razor-syntax-c/_static/image11.jpg)

<span data-ttu-id="92f39-439">Pokud pracujete s kolekcí nebo polem, často používáte smyčku `foreach`.</span><span class="sxs-lookup"><span data-stu-id="92f39-439">If you're working with a collection or array, you often use a `foreach` loop.</span></span> <span data-ttu-id="92f39-440">Kolekce je skupina podobných objektů a smyčka `foreach` umožňuje provádět úlohy na každé položce v kolekci.</span><span class="sxs-lookup"><span data-stu-id="92f39-440">A collection is a group of similar objects, and the `foreach` loop lets you carry out a task on each item in the collection.</span></span> <span data-ttu-id="92f39-441">Tento typ smyčky je vhodný pro kolekce, protože na rozdíl od `for` smyčky nemusíte zvyšovat čítač nebo nastavit limit.</span><span class="sxs-lookup"><span data-stu-id="92f39-441">This type of loop is convenient for collections, because unlike a `for` loop, you don't have to increment the counter or set a limit.</span></span> <span data-ttu-id="92f39-442">Místo toho kód smyčky `foreach` jednoduše projde přes kolekci, dokud není dokončena.</span><span class="sxs-lookup"><span data-stu-id="92f39-442">Instead, the `foreach` loop code simply proceeds through the collection until it's finished.</span></span>

<span data-ttu-id="92f39-443">Například následující kód vrátí položky v kolekci `Request.ServerVariables`, což je objekt, který obsahuje informace o vašem webovém serveru.</span><span class="sxs-lookup"><span data-stu-id="92f39-443">For example, the following code returns the items in the `Request.ServerVariables` collection, which is an object that contains information about your web server.</span></span> <span data-ttu-id="92f39-444">Používá smyčku `foreac` h k zobrazení názvu každé položky vytvořením nového prvku `<li>` v seznamu s odrážkami HTML.</span><span class="sxs-lookup"><span data-stu-id="92f39-444">It uses a `foreac` h loop to display the name of each item by creating a new `<li>` element in an HTML bulleted list.</span></span>

[!code-html[Main](introducing-razor-syntax-c/samples/sample54.html)]

<span data-ttu-id="92f39-445">Za klíčovým slovem `foreach` následuje závorky, kde deklarujete proměnnou reprezentující jednu položku v kolekci (v příkladu `var item`) následovaný klíčovým slovem `in` následovaným kolekcí, kterou chcete procyklovat.</span><span class="sxs-lookup"><span data-stu-id="92f39-445">The `foreach` keyword is followed by parentheses where you declare a variable that represents a single item in the collection (in the example, `var item`), followed by the `in` keyword, followed by the collection you want to loop through.</span></span> <span data-ttu-id="92f39-446">V těle `foreach` smyčky můžete k aktuální položce přistupovat pomocí proměnné, kterou jste předtím deklarovali.</span><span class="sxs-lookup"><span data-stu-id="92f39-446">In the body of the `foreach` loop, you can access the current item using the variable that you declared earlier.</span></span>

![Razor-Img12](introducing-razor-syntax-c/_static/image12.jpg)

<span data-ttu-id="92f39-448">Chcete-li vytvořit obecnější smyčku pro účely, použijte příkaz `while`:</span><span class="sxs-lookup"><span data-stu-id="92f39-448">To create a more general-purpose loop, use the `while` statement:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample55.cshtml)]

<span data-ttu-id="92f39-449">Smyčka `while` začíná klíčovým slovem `while` následovanými závorkami, kde určíte, jak dlouho bude smyčka pokračovat (zde, pokud je `countNum` menší než 50), pak se blok opakuje.</span><span class="sxs-lookup"><span data-stu-id="92f39-449">A `while` loop begins with the `while` keyword, followed by parentheses where you specify how long the loop continues (here, for as long as `countNum` is less than 50), then the block to repeat.</span></span> <span data-ttu-id="92f39-450">Smyčky typicky přidávají (přidávají do) nebo snižují (odečtou z) proměnnou nebo objekt, který se používá pro počítání.</span><span class="sxs-lookup"><span data-stu-id="92f39-450">Loops typically increment (add to) or decrement (subtract from) a variable or object used for counting.</span></span> <span data-ttu-id="92f39-451">V příkladu operátor `+=` přidá 1 pro `countNum` pokaždé, když se smyčka spustí.</span><span class="sxs-lookup"><span data-stu-id="92f39-451">In the example, the `+=` operator adds 1 to `countNum` each time the loop runs.</span></span> <span data-ttu-id="92f39-452">(Chcete-li snížit proměnnou ve smyčce, která počítá dolů, použijte operátor snížení `-=`).</span><span class="sxs-lookup"><span data-stu-id="92f39-452">(To decrement a variable in a loop that counts down, you would use the decrement operator `-=`).</span></span>

## <a name="objects-and-collections"></a><span data-ttu-id="92f39-453">Objekty a kolekce</span><span class="sxs-lookup"><span data-stu-id="92f39-453">Objects and Collections</span></span>

<span data-ttu-id="92f39-454">Skoro všechno na webu ASP.NET je objekt, včetně samotné webové stránky.</span><span class="sxs-lookup"><span data-stu-id="92f39-454">Nearly everything in an ASP.NET website is an object, including the web page itself.</span></span> <span data-ttu-id="92f39-455">Tato část popisuje některé důležité objekty, se kterými se často pracujete ve vašem kódu.</span><span class="sxs-lookup"><span data-stu-id="92f39-455">This section discusses some important objects you'll work with frequently in your code.</span></span>

### <a name="page-objects"></a><span data-ttu-id="92f39-456">Objekty stránky</span><span class="sxs-lookup"><span data-stu-id="92f39-456">Page Objects</span></span>

<span data-ttu-id="92f39-457">Nejzákladnější objekt v ASP.NET je stránka.</span><span class="sxs-lookup"><span data-stu-id="92f39-457">The most basic object in ASP.NET is the page.</span></span> <span data-ttu-id="92f39-458">K vlastnostem objektu stránky můžete přistupovat přímo bez jakéhokoli opravňujícího objektu.</span><span class="sxs-lookup"><span data-stu-id="92f39-458">You can access properties of the page object directly without any qualifying object.</span></span> <span data-ttu-id="92f39-459">Následující kód Získá cestu k souboru stránky pomocí objektu `Request` stránky:</span><span class="sxs-lookup"><span data-stu-id="92f39-459">The following code gets the page's file path, using the `Request` object of the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample56.cshtml)]

<span data-ttu-id="92f39-460">Chcete-li zrušit zaškrtnutí, že odkazujete na vlastnosti a metody v objektu aktuální stránky, můžete volitelně použít klíčové slovo `this` pro reprezentaci objektu Page v kódu.</span><span class="sxs-lookup"><span data-stu-id="92f39-460">To make it clear that you're referencing properties and methods on the current page object, you can optionally use the keyword `this` to represent the page object in your code.</span></span> <span data-ttu-id="92f39-461">Zde je předchozí příklad kódu s `this` přidat k reprezentaci stránky:</span><span class="sxs-lookup"><span data-stu-id="92f39-461">Here is the previous code example, with `this` added to represent the page:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample57.cshtml)]

<span data-ttu-id="92f39-462">Pomocí vlastností objektu `Page` můžete získat velké množství informací, například:</span><span class="sxs-lookup"><span data-stu-id="92f39-462">You can use properties of the `Page` object to get a lot of information, such as:</span></span>

- <span data-ttu-id="92f39-463">`Request`.</span><span class="sxs-lookup"><span data-stu-id="92f39-463">`Request`.</span></span> <span data-ttu-id="92f39-464">Jak už jste viděli, jedná se o kolekci informací o aktuální žádosti, včetně typu prohlížeče, který požadavek odeslal, adresu URL stránky, identitu uživatele atd.</span><span class="sxs-lookup"><span data-stu-id="92f39-464">As you've already seen, this is a collection of information about the current request, including what type of browser made the request, the URL of the page, the user identity, etc.</span></span>
- <span data-ttu-id="92f39-465">`Response`.</span><span class="sxs-lookup"><span data-stu-id="92f39-465">`Response`.</span></span> <span data-ttu-id="92f39-466">Toto je kolekce informací o odpovědi (stránky), která se odešle do prohlížeče, když je kód serveru spuštěný.</span><span class="sxs-lookup"><span data-stu-id="92f39-466">This is a collection of information about the response (page) that will be sent to the browser when the server code has finished running.</span></span> <span data-ttu-id="92f39-467">Tuto vlastnost můžete například použít k zápisu informací do odpovědi.</span><span class="sxs-lookup"><span data-stu-id="92f39-467">For example, you can use this property to write information into the response.</span></span> 

    [!code-cshtml[Main](introducing-razor-syntax-c/samples/sample58.cshtml)]

<a id="ID_CollectionsAndObjects"></a>
### <a name="collection-objects-arrays-and-dictionaries"></a><span data-ttu-id="92f39-468">Objekty kolekce (pole a slovníky)</span><span class="sxs-lookup"><span data-stu-id="92f39-468">Collection Objects (Arrays and Dictionaries)</span></span>

<span data-ttu-id="92f39-469">*Kolekce* je skupina objektů stejného typu, například kolekce `Customer` objektů z databáze.</span><span class="sxs-lookup"><span data-stu-id="92f39-469">A *collection* is a group of objects of the same type, such as a collection of `Customer` objects from a database.</span></span> <span data-ttu-id="92f39-470">ASP.NET obsahuje mnoho předdefinovaných kolekcí, jako je kolekce `Request.Files`.</span><span class="sxs-lookup"><span data-stu-id="92f39-470">ASP.NET contains many built-in collections, like the `Request.Files` collection.</span></span>

<span data-ttu-id="92f39-471">Často budete pracovat s daty v kolekcích.</span><span class="sxs-lookup"><span data-stu-id="92f39-471">You'll often work with data in collections.</span></span> <span data-ttu-id="92f39-472">Dva společné typy kolekcí jsou *pole* a *slovník*.</span><span class="sxs-lookup"><span data-stu-id="92f39-472">Two common collection types are the *array* and the *dictionary*.</span></span> <span data-ttu-id="92f39-473">Pole je užitečné, pokud chcete uložit kolekci podobných položek, ale nechcete vytvořit samostatnou proměnnou pro uchování každé položky:</span><span class="sxs-lookup"><span data-stu-id="92f39-473">An array is useful when you want to store a collection of similar items but don't want to create a separate variable to hold each item:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample59.cshtml)]

<span data-ttu-id="92f39-474">Pomocí polí deklarujete konkrétní datový typ, například `string`, `int`nebo `DateTime`.</span><span class="sxs-lookup"><span data-stu-id="92f39-474">With arrays, you declare a specific data type, such as `string`, `int`, or `DateTime`.</span></span> <span data-ttu-id="92f39-475">Chcete-li označit, že proměnná může obsahovat pole, přidejte do deklarace hranaté závorky (například `string[]` nebo `int[]`).</span><span class="sxs-lookup"><span data-stu-id="92f39-475">To indicate that the variable can contain an array, you add brackets to the declaration (such as `string[]` or `int[]`).</span></span> <span data-ttu-id="92f39-476">K položkám v poli můžete přistupovat pomocí jejich pozice (indexu) nebo pomocí příkazu `foreach`.</span><span class="sxs-lookup"><span data-stu-id="92f39-476">You can access items in an array using their position (index) or by using the `foreach` statement.</span></span> <span data-ttu-id="92f39-477">Indexy polí jsou počítány od &#8212; nuly, tj. první položka je na pozici 0, druhá položka je na pozici 1 atd.</span><span class="sxs-lookup"><span data-stu-id="92f39-477">Array indexes are zero-based &#8212; that is, the first item is at position 0, the second item is at position 1, and so on.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample60.cshtml)]

<span data-ttu-id="92f39-478">Počet položek v poli můžete určit získáním jeho vlastnosti `Length`.</span><span class="sxs-lookup"><span data-stu-id="92f39-478">You can determine the number of items in an array by getting its `Length` property.</span></span> <span data-ttu-id="92f39-479">Chcete-li získat pozici konkrétní položky v poli (pro hledání v poli), použijte metodu `Array.IndexOf`.</span><span class="sxs-lookup"><span data-stu-id="92f39-479">To get the position of a specific item in the array (to search the array), use the `Array.IndexOf` method.</span></span> <span data-ttu-id="92f39-480">Můžete také provést akce, jako je vrácení obsahu pole (`Array.Reverse` metody) nebo řazení obsahu (metoda `Array.Sort`).</span><span class="sxs-lookup"><span data-stu-id="92f39-480">You can also do things like reverse the contents of an array (the `Array.Reverse` method) or sort the contents (the `Array.Sort` method).</span></span>

<span data-ttu-id="92f39-481">Výstup kódu řetězcového pole zobrazeného v prohlížeči:</span><span class="sxs-lookup"><span data-stu-id="92f39-481">The output of the string array code displayed in a browser:</span></span>

![Razor-Img13](introducing-razor-syntax-c/_static/image13.jpg)

<span data-ttu-id="92f39-483">Slovník je kolekce párů klíč/hodnota, kde zadáte klíč (nebo název) pro nastavení nebo načtení příslušné hodnoty:</span><span class="sxs-lookup"><span data-stu-id="92f39-483">A dictionary is a collection of key/value pairs, where you provide the key (or name) to set or retrieve the corresponding value:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample61.cshtml)]

<span data-ttu-id="92f39-484">Chcete-li vytvořit slovník, použijte klíčové slovo `new` pro indikaci, že vytváříte nový objekt Dictionary.</span><span class="sxs-lookup"><span data-stu-id="92f39-484">To create a dictionary, you use the `new` keyword to indicate that you're creating a new dictionary object.</span></span> <span data-ttu-id="92f39-485">K proměnné můžete přiřadit slovník pomocí klíčového slova `var`.</span><span class="sxs-lookup"><span data-stu-id="92f39-485">You can assign a dictionary to a variable using the `var` keyword.</span></span> <span data-ttu-id="92f39-486">Datové typy položek ve slovníku označíte pomocí lomených závorek (`< >`).</span><span class="sxs-lookup"><span data-stu-id="92f39-486">You indicate the data types of the items in the dictionary using angle brackets ( `< >` ).</span></span> <span data-ttu-id="92f39-487">Na konci deklarace je nutné přidat dvojici závorek, protože se jedná o metodu, která vytvoří nový slovník.</span><span class="sxs-lookup"><span data-stu-id="92f39-487">At the end of the declaration, you must add a pair of parentheses, because this is actually a method that creates a new dictionary.</span></span>

<span data-ttu-id="92f39-488">Chcete-li přidat položky do slovníku, můžete zavolat metodu `Add` proměnné Dictionary (`myScores` v tomto případě) a poté zadat klíč a hodnotu.</span><span class="sxs-lookup"><span data-stu-id="92f39-488">To add items to the dictionary, you can call the `Add` method of the dictionary variable (`myScores` in this case), and then specify a key and a value.</span></span> <span data-ttu-id="92f39-489">Alternativně můžete pomocí hranatých závorek označit klíč a provést jednoduché přiřazení, jako v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="92f39-489">Alternatively, you can use square brackets to indicate the key and do a simple assignment, as in the following example:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample62.cs)]

<span data-ttu-id="92f39-490">Pokud chcete získat hodnotu ze slovníku, zadáte klíč v závorkách:</span><span class="sxs-lookup"><span data-stu-id="92f39-490">To get a value from the dictionary, you specify the key in brackets:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample63.cs)]

## <a name="calling-methods-with-parameters"></a><span data-ttu-id="92f39-491">Volání metod s parametry</span><span class="sxs-lookup"><span data-stu-id="92f39-491">Calling Methods with Parameters</span></span>

<span data-ttu-id="92f39-492">Jak si přečtete výše v tomto článku, objekty, se kterými program pracuje, můžou mít metody.</span><span class="sxs-lookup"><span data-stu-id="92f39-492">As you read earlier in this article, the objects that you program with can have methods.</span></span> <span data-ttu-id="92f39-493">Například `Database` objekt může mít metodu `Database.Connect`.</span><span class="sxs-lookup"><span data-stu-id="92f39-493">For example, a `Database` object might have a `Database.Connect` method.</span></span> <span data-ttu-id="92f39-494">Mnoho metod má také jeden nebo více parametrů.</span><span class="sxs-lookup"><span data-stu-id="92f39-494">Many methods also have one or more parameters.</span></span> <span data-ttu-id="92f39-495">*Parametr* je hodnota, kterou předáte metodě, aby mohla metoda dokončit její úlohu.</span><span class="sxs-lookup"><span data-stu-id="92f39-495">A *parameter* is a value that you pass to a method to enable the method to complete its task.</span></span> <span data-ttu-id="92f39-496">Podívejte se například na deklaraci metody `Request.MapPath`, která přijímá tři parametry:</span><span class="sxs-lookup"><span data-stu-id="92f39-496">For example, look at a declaration for the `Request.MapPath` method, which takes three parameters:</span></span>

[!code-csharp[Main](introducing-razor-syntax-c/samples/sample64.cs)]

<span data-ttu-id="92f39-497">(Řádek byl zabalen, aby byl čitelnější.</span><span class="sxs-lookup"><span data-stu-id="92f39-497">(The line has been wrapped to make it more readable.</span></span> <span data-ttu-id="92f39-498">Mějte na paměti, že můžete umístit konce řádků téměř na jakékoli místo kromě řetězců, které jsou uzavřeny v uvozovkách.)</span><span class="sxs-lookup"><span data-stu-id="92f39-498">Remember that you can put line breaks almost any place except inside strings that are enclosed in quotation marks.)</span></span>

<span data-ttu-id="92f39-499">Tato metoda vrátí fyzickou cestu na serveru, který odpovídá zadané virtuální cestě.</span><span class="sxs-lookup"><span data-stu-id="92f39-499">This method returns the physical path on the server that corresponds to a specified virtual path.</span></span> <span data-ttu-id="92f39-500">Tři parametry pro metodu jsou `virtualPath`, `baseVirtualDir`a `allowCrossAppMapping`.</span><span class="sxs-lookup"><span data-stu-id="92f39-500">The three parameters for the method are `virtualPath`, `baseVirtualDir`, and `allowCrossAppMapping`.</span></span> <span data-ttu-id="92f39-501">(Všimněte si, že v deklaraci jsou parametry uvedeny s datovými typy dat, která budou přijímat.) Při volání této metody je nutné dodat hodnoty pro všechny tři parametry.</span><span class="sxs-lookup"><span data-stu-id="92f39-501">(Notice that in the declaration, the parameters are listed with the data types of the data that they'll accept.) When you call this method, you must supply values for all three parameters.</span></span>

<span data-ttu-id="92f39-502">Syntaxe Razor poskytuje dvě možnosti pro předávání parametrů metodě: *poziční parametry* a *pojmenované parametry*.</span><span class="sxs-lookup"><span data-stu-id="92f39-502">The Razor syntax gives you two options for passing parameters to a method: *positional parameters* and *named parameters*.</span></span> <span data-ttu-id="92f39-503">Chcete-li volat metodu pomocí pozičních parametrů, předáte parametry v přesném pořadí, které je zadáno v deklaraci metody.</span><span class="sxs-lookup"><span data-stu-id="92f39-503">To call a method using positional parameters, you pass the parameters in a strict order that's specified in the method declaration.</span></span> <span data-ttu-id="92f39-504">(Toto pořadí byste obvykle znali v dokumentaci k metodě.) Je nutné postupovat podle pořadí a v případě potřeby nemůžete přeskočit &#8212; žádný z parametrů, předáte prázdný řetězec (`""`) nebo `null` pozičního parametru, pro který nemáte hodnotu.</span><span class="sxs-lookup"><span data-stu-id="92f39-504">(You would typically know this order by reading documentation for the method.) You must follow the order, and you can't skip any of the parameters &#8212; if necessary, you pass an empty string (`""`) or `null` for a positional parameter that you don't have a value for.</span></span>

<span data-ttu-id="92f39-505">Následující příklad předpokládá, že máte ve svém webu složku s názvem *skripty* .</span><span class="sxs-lookup"><span data-stu-id="92f39-505">The following example assumes you have a folder named *scripts* on your website.</span></span> <span data-ttu-id="92f39-506">Kód volá metodu `Request.MapPath` a předá hodnoty pro tři parametry ve správném pořadí.</span><span class="sxs-lookup"><span data-stu-id="92f39-506">The code calls the `Request.MapPath` method and passes values for the three parameters in the correct order.</span></span> <span data-ttu-id="92f39-507">Pak zobrazí výslednou mapovanou cestu.</span><span class="sxs-lookup"><span data-stu-id="92f39-507">It then displays the resulting mapped path.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample65.cshtml)]

<span data-ttu-id="92f39-508">Pokud má metoda mnoho parametrů, můžete si kód lépe přečíst pomocí pojmenovaných parametrů.</span><span class="sxs-lookup"><span data-stu-id="92f39-508">When a method has many parameters, you can keep your code more readable by using named parameters.</span></span> <span data-ttu-id="92f39-509">Chcete-li volat metodu pomocí pojmenovaných parametrů, zadejte název parametru následovaný dvojtečkou (:) a pak hodnotu.</span><span class="sxs-lookup"><span data-stu-id="92f39-509">To call a method using named parameters, you specify the parameter name followed by a colon (:), and then the value.</span></span> <span data-ttu-id="92f39-510">Výhodou pojmenovaných parametrů je, že je můžete předat v libovolném požadovaném pořadí.</span><span class="sxs-lookup"><span data-stu-id="92f39-510">The advantage of named parameters is that you can pass them in any order you want.</span></span> <span data-ttu-id="92f39-511">(Nevýhodou je, že volání metody není jako kompaktní.)</span><span class="sxs-lookup"><span data-stu-id="92f39-511">(A disadvantage is that the method call is not as compact.)</span></span>

<span data-ttu-id="92f39-512">Následující příklad volá stejnou metodu jako výše, ale používá pojmenované parametry k poskytnutí těchto hodnot:</span><span class="sxs-lookup"><span data-stu-id="92f39-512">The following example calls the same method as above, but uses named parameters to supply the values:</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample66.cshtml)]

<span data-ttu-id="92f39-513">Jak vidíte, parametry jsou předány v jiném pořadí.</span><span class="sxs-lookup"><span data-stu-id="92f39-513">As you can see, the parameters are passed in a different order.</span></span> <span data-ttu-id="92f39-514">Pokud však spustíte předchozí příklad a tento příklad vrátí stejnou hodnotu.</span><span class="sxs-lookup"><span data-stu-id="92f39-514">However, if you run the previous example and this example, they'll return the same value.</span></span>

<a id="ID_HandlingErrors"></a>
## <a name="handling-errors"></a><span data-ttu-id="92f39-515">Zpracování chyb</span><span class="sxs-lookup"><span data-stu-id="92f39-515">Handling Errors</span></span>

### <a name="try-catch-statements"></a><span data-ttu-id="92f39-516">Příkazy try-catch</span><span class="sxs-lookup"><span data-stu-id="92f39-516">Try-Catch Statements</span></span>

<span data-ttu-id="92f39-517">Často budete mít ve svém kódu příkazy, které mohou selhat z důvodů mimo váš ovládací prvek.</span><span class="sxs-lookup"><span data-stu-id="92f39-517">You'll often have statements in your code that might fail for reasons outside your control.</span></span> <span data-ttu-id="92f39-518">Příklad:</span><span class="sxs-lookup"><span data-stu-id="92f39-518">For example:</span></span>

- <span data-ttu-id="92f39-519">Pokud se váš kód pokusí vytvořit soubor nebo k němu získat přístup, může dojít k nejrůznějším chybám.</span><span class="sxs-lookup"><span data-stu-id="92f39-519">If your code tries to create or access a file, all sorts of errors might occur.</span></span> <span data-ttu-id="92f39-520">Soubor, který chcete, možná neexistuje, může být uzamčen, kód pravděpodobně nemá oprávnění atd.</span><span class="sxs-lookup"><span data-stu-id="92f39-520">The file you want might not exist, it might be locked, the code might not have permissions, and so on.</span></span>
- <span data-ttu-id="92f39-521">Podobně platí, že pokud se váš kód pokusí aktualizovat záznamy v databázi, může dojít k problémům s oprávněními, připojení k databázi může být vyřazeno, data, která mají být uložena, mohou být neplatná atd.</span><span class="sxs-lookup"><span data-stu-id="92f39-521">Similarly, if your code tries to update records in a database, there can be permissions issues, the connection to the database might be dropped, the data to save might be invalid, and so on.</span></span>

<span data-ttu-id="92f39-522">V programovacích podmínkách se tyto situace nazývají *výjimky*.</span><span class="sxs-lookup"><span data-stu-id="92f39-522">In programming terms, these situations are called *exceptions*.</span></span> <span data-ttu-id="92f39-523">Pokud váš kód narazí na výjimku, vygeneruje (vyvolá) chybovou zprávu, která je na nejvyšší úrovni uživatelům obtěžující:</span><span class="sxs-lookup"><span data-stu-id="92f39-523">If your code encounters an exception, it generates (throws) an error message that's, at best, annoying to users:</span></span>

![Razor-Img14](introducing-razor-syntax-c/_static/image14.jpg)

<span data-ttu-id="92f39-525">V situacích, kdy se váš kód může setkat s výjimkami, a aby se předešlo chybovým zprávám tohoto typu, můžete použít příkazy `try/catch`.</span><span class="sxs-lookup"><span data-stu-id="92f39-525">In situations where your code might encounter exceptions, and in order to avoid error messages of this type, you can use `try/catch` statements.</span></span> <span data-ttu-id="92f39-526">V příkazu `try` spustíte kód, který kontrolujete.</span><span class="sxs-lookup"><span data-stu-id="92f39-526">In the `try` statement, you run the code that you're checking.</span></span> <span data-ttu-id="92f39-527">V jednom nebo více příkazech `catch` můžete vyhledat konkrétní chyby (konkrétní typy výjimek), ke kterým mohlo dojít.</span><span class="sxs-lookup"><span data-stu-id="92f39-527">In one or more `catch` statements, you can look for specific errors (specific types of exceptions) that might have occurred.</span></span> <span data-ttu-id="92f39-528">Můžete zahrnout tolik příkazů `catch`, kolik potřebujete pro hledání chyb, které očekáváte.</span><span class="sxs-lookup"><span data-stu-id="92f39-528">You can include as many `catch` statements as you need to look for errors that you are anticipating.</span></span>

> [!NOTE]
> <span data-ttu-id="92f39-529">Doporučujeme, abyste se vyhnuli použití metody `Response.Redirect` v příkazech `try/catch`, protože to může způsobit výjimku na stránce.</span><span class="sxs-lookup"><span data-stu-id="92f39-529">We recommend that you avoid using the `Response.Redirect` method in `try/catch` statements, because it can cause an exception in your page.</span></span>

<span data-ttu-id="92f39-530">Následující příklad ukazuje stránku, která vytvoří textový soubor pro první požadavek a pak zobrazí tlačítko, které uživateli otevře soubor.</span><span class="sxs-lookup"><span data-stu-id="92f39-530">The following example shows a page that creates a text file on the first request and then displays a button that lets the user open the file.</span></span> <span data-ttu-id="92f39-531">Příklad záměrně používá špatný název souboru, takže bude způsobovat výjimku.</span><span class="sxs-lookup"><span data-stu-id="92f39-531">The example deliberately uses a bad file name so that it will cause an exception.</span></span> <span data-ttu-id="92f39-532">Kód zahrnuje `catch` příkazy pro dvě možné výjimky: `FileNotFoundException`, ke kterým dojde, pokud je název souboru špatný a `DirectoryNotFoundException`, ke kterému dochází, pokud ASP.NET nemůže dokonce najít složku.</span><span class="sxs-lookup"><span data-stu-id="92f39-532">The code includes `catch` statements for two possible exceptions: `FileNotFoundException`, which occurs if the file name is bad, and `DirectoryNotFoundException`, which occurs if ASP.NET can't even find the folder.</span></span> <span data-ttu-id="92f39-533">(Můžete zrušit komentář k příkazu v příkladu, abyste viděli, jak se spustí, když vše funguje správně.)</span><span class="sxs-lookup"><span data-stu-id="92f39-533">(You can uncomment a statement in the example in order to see how it runs when everything works properly.)</span></span>

<span data-ttu-id="92f39-534">Pokud váš kód nezpracovává výjimku, zobrazila se chybová stránka, například snímek předchozí obrazovky.</span><span class="sxs-lookup"><span data-stu-id="92f39-534">If your code didn't handle the exception, you would see an error page like the previous screen shot.</span></span> <span data-ttu-id="92f39-535">Nicméně část `try/catch` pomáhá zabránit uživateli v zobrazování těchto typů chyb.</span><span class="sxs-lookup"><span data-stu-id="92f39-535">However, the `try/catch` section helps prevent the user from seeing these types of errors.</span></span>

[!code-cshtml[Main](introducing-razor-syntax-c/samples/sample67.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="92f39-536">Další prostředky</span><span class="sxs-lookup"><span data-stu-id="92f39-536">Additional Resources</span></span>

<span data-ttu-id="92f39-537">**Programování pomocí Visual Basic**</span><span class="sxs-lookup"><span data-stu-id="92f39-537">**Programming with Visual Basic**</span></span>

[<span data-ttu-id="92f39-538">Příloha: Visual Basic jazyk a syntax</span><span class="sxs-lookup"><span data-stu-id="92f39-538">Appendix: Visual Basic Language and Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkId=202908)

<span data-ttu-id="92f39-539">**Referenční dokumentace**</span><span class="sxs-lookup"><span data-stu-id="92f39-539">**Reference Documentation**</span></span>

[<span data-ttu-id="92f39-540">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="92f39-540">ASP.NET</span></span>](https://msdn.microsoft.com/library/ee532866.aspx)

[<span data-ttu-id="92f39-541">C#Language</span><span class="sxs-lookup"><span data-stu-id="92f39-541">C# Language</span></span>](https://msdn.microsoft.com/library/kx37x362.aspx)

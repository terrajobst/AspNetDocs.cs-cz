---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
title: Přidání ověření do modelu | Microsoft Docs
author: shanselman
description: Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC. Vytvořte jednoduchou webovou aplikaci, která čte a zapisuje z databáze.
ms.author: riande
ms.date: 08/14/2010
ms.assetid: aa7b3e8e-e23d-49f1-b160-f99a7f2982bd
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part7
msc.type: authoredcontent
ms.openlocfilehash: 9403be574324c34edf93bef1e0e4fd7ba68a3a9d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543643"
---
# <a name="adding-validation-to-the-model"></a><span data-ttu-id="eb3a7-104">Přidání ověření do modelu</span><span class="sxs-lookup"><span data-stu-id="eb3a7-104">Adding Validation to the Model</span></span>

<span data-ttu-id="eb3a7-105">[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="eb3a7-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="eb3a7-106">Toto je úvodní kurz pro začátečníky, který představuje základy ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="eb3a7-107">Vytvoříte jednoduchou webovou aplikaci, která čte a zapisuje z databáze.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="eb3a7-108">Navštivte [centrum učení služby ASP.NET MVC](../../../index.md) , kde najdete další kurzy a ukázky pro ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="eb3a7-109">V této části budeme implementovat podporu nutnou k povolení ověřování vstupu v rámci naší aplikace.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-109">In this section we are going to implement the support necessary to enable input validation within our application.</span></span> <span data-ttu-id="eb3a7-110">Zajistíme, aby byl obsah databáze vždycky správný, a při pokusu o zadání užitečných chybových zpráv, které se pokoušejí, a zadání filmových dat, která nejsou platná.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-110">We'll ensure that our database content is always correct, and provide helpful error messages to end users when they try and enter Movie data which is not valid.</span></span> <span data-ttu-id="eb3a7-111">Začneme přidáním malé logiky ověřování do třídy video.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-111">We'll begin by adding a little validation logic to the Movie class.</span></span>

<span data-ttu-id="eb3a7-112">Klikněte pravým tlačítkem na složku modelu a vyberte Přidat třídu.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-112">Right click on the Model folder and select Add Class.</span></span> <span data-ttu-id="eb3a7-113">Pojmenujte film vaší třídy.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-113">Name your class Movie.</span></span>

<span data-ttu-id="eb3a7-114">Po předchozím vytvoření modelu entity filmu rozhraní IDE vytvořilo třídu filmu.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-114">When we created the Movie Entity Model earlier, the IDE created a Movie class.</span></span> <span data-ttu-id="eb3a7-115">Ve skutečnosti může být součástí třídy video v jednom souboru a částečně v jiném.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-115">In fact, part of the Movie class can be in one file and part in another.</span></span> <span data-ttu-id="eb3a7-116">Toto se nazývá částečná třída.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-116">This is called a Partial Class.</span></span> <span data-ttu-id="eb3a7-117">Chystáme se třídu Movie rozšiřuje z jiného souboru.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-117">We're going to extend the Movie class from another file.</span></span>

<span data-ttu-id="eb3a7-118">Vytvoříme částečnou třídu filmu, která odkazuje na "přítel Class" s některými atributy, které budou poskytovat pomocný parametr ověřování systému.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-118">We'll create a partial movie class that points to a "buddy class" with some attributes that will give validation hints to the system.</span></span> <span data-ttu-id="eb3a7-119">Název a cenu budeme označovat jako povinnou a také si Navedeme, že cena bude v určitém rozsahu.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-119">We'll mark the Title and Price as Required, and also insist that the Price be within a certain range.</span></span> <span data-ttu-id="eb3a7-120">Klikněte pravým tlačítkem na složku modely a vyberte Přidat třídu.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-120">Right click the Models folder and select Add Class.</span></span> <span data-ttu-id="eb3a7-121">Pojmenujte film na třídu a klikněte na tlačítko OK.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-121">Name your class Movie and Click the OK button.</span></span> <span data-ttu-id="eb3a7-122">Tady je, jak má naše částečná třída filmu vypadat.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-122">Here's what our partial Movie class looks like.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part7/samples/sample1.cs)]

<span data-ttu-id="eb3a7-123">Spusťte aplikaci znovu a zkuste zadat film s cenou vyšší než 100.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-123">Re-Run your application and try to enter a movie with a price over 100.</span></span> <span data-ttu-id="eb3a7-124">Po odeslání formuláře se zobrazí chybová zpráva.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-124">You'll get an error after you've submitted the form.</span></span> <span data-ttu-id="eb3a7-125">Tato chyba se zachycuje na straně serveru a nastane po publikování formuláře.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-125">The error is caught on the server side and occurs after the Form is POSTed.</span></span> <span data-ttu-id="eb3a7-126">Všimněte si, jak byly integrované pomocníky HTML v ASP.NET MVC dostatečně inteligentní pro zobrazení chybové zprávy a udržování hodnot pro nás v rámci elementů TextBox:</span><span class="sxs-lookup"><span data-stu-id="eb3a7-126">Notice how ASP.NET MVC's built-in HTML helpers were smart enough to display the error message and maintain the values for us within the textbox elements:</span></span>

<span data-ttu-id="eb3a7-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="eb3a7-127">[![CreateMovieWithValidation](getting-started-with-mvc-part7/_static/image2.png)](getting-started-with-mvc-part7/_static/image1.png)</span></span>

<span data-ttu-id="eb3a7-128">To funguje skvěle, ale v případě, že se na straně klienta může informovat uživatel hned po straně klienta.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-128">This works great, but it'd be nice if we could tell the user on the client-side, immediately, before the server gets involved.</span></span>

<span data-ttu-id="eb3a7-129">Pojďme povolit ověřování na straně klienta pomocí JavaScriptu.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-129">Let's enable some client-side validation with JavaScript.</span></span>

## <a name="adding-client-side-validation"></a><span data-ttu-id="eb3a7-130">Přidání ověřování na straně klienta</span><span class="sxs-lookup"><span data-stu-id="eb3a7-130">Adding Client-Side Validation</span></span>

<span data-ttu-id="eb3a7-131">Vzhledem k tomu, že naše třída filmu již obsahuje některé atributy ověřování, stačí do naší šablony zobrazení Create. aspx přidat několik souborů JavaScriptu a přidat řádek kódu, který povolí ověřování na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-131">Since our Movie class already has some validation attributes, we'll just need to add a few JavaScript files to our Create.aspx View template and add a line of code to enable client-side validation to take place.</span></span>

<span data-ttu-id="eb3a7-132">V souboru vwd se podívejte na naše zobrazení/složku videa a otevřete vytvořit. aspx.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-132">From within VWD go our Views/Movie folder and open up Create.aspx.</span></span>

<span data-ttu-id="eb3a7-133">Otevřete složku skripty v Průzkumník řešení a přetáhněte následující tři skripty do značky &lt;Head&gt;.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-133">Open up the Scripts folder in the Solution Explorer and drag the following three scripts to within the &lt;head&gt; tag.</span></span>

- <span data-ttu-id="eb3a7-134">MicrosoftAjax.js</span><span class="sxs-lookup"><span data-stu-id="eb3a7-134">MicrosoftAjax.js</span></span>
- <span data-ttu-id="eb3a7-135">MicrosoftMvcValidation.js</span><span class="sxs-lookup"><span data-stu-id="eb3a7-135">MicrosoftMvcValidation.js</span></span>

<span data-ttu-id="eb3a7-136">Chcete, aby se tyto soubory skriptu zobrazovaly v tomto pořadí.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-136">You want these script files to appear in this order.</span></span>

[!code-html[Main](getting-started-with-mvc-part7/samples/sample2.html)]

<span data-ttu-id="eb3a7-137">Přidejte také tento jediný řádek nad HTML. BeginForm:</span><span class="sxs-lookup"><span data-stu-id="eb3a7-137">Also, add this single line above the Html.BeginForm:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part7/samples/sample3.aspx)]

<span data-ttu-id="eb3a7-138">Zde je kód zobrazený v rámci integrovaného vývojového prostředí (IDE).</span><span class="sxs-lookup"><span data-stu-id="eb3a7-138">Here's the code shown within the IDE.</span></span>

<span data-ttu-id="eb3a7-139">[Filmy ![– Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="eb3a7-139">[![Movies - Microsoft Visual Web Developer 2010 Express (10)](getting-started-with-mvc-part7/_static/image4.png)](getting-started-with-mvc-part7/_static/image3.png)</span></span>

<span data-ttu-id="eb3a7-140">Spusťte aplikaci a znovu navštivte/Movies/Create a klikněte na vytvořit bez zadání jakýchkoli dat.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-140">Run your application and visit /Movies/Create again, and click Create without entering any data.</span></span> <span data-ttu-id="eb3a7-141">Chybové zprávy se zobrazí okamžitě bez blikání stránky, které přiřadíme k posílání dat zpět na server.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-141">The error messages appear immediately without the page flash that we associate with sending data all the way back to the server.</span></span> <span data-ttu-id="eb3a7-142">Důvodem je to, že ASP.NET MVC nyní ověřuje vstup na straně klienta (pomocí JavaScriptu) i na serveru.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-142">This is because ASP.NET MVC is now validating the input on both the client (using JavaScript) and on the server.</span></span>

<span data-ttu-id="eb3a7-143">[![vytvoření – Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="eb3a7-143">[![Create - Windows Internet Explorer](getting-started-with-mvc-part7/_static/image6.png)](getting-started-with-mvc-part7/_static/image5.png)</span></span>

<span data-ttu-id="eb3a7-144">To je dobré.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-144">This is looking good!</span></span> <span data-ttu-id="eb3a7-145">Nyní přidáme do databáze jeden další sloupec.</span><span class="sxs-lookup"><span data-stu-id="eb3a7-145">Let's now add one additional column to the database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="eb3a7-146">[Předchozí](getting-started-with-mvc-part6.md)
> [Další](getting-started-with-mvc-part8.md)</span><span class="sxs-lookup"><span data-stu-id="eb3a7-146">[Previous](getting-started-with-mvc-part6.md)
[Next](getting-started-with-mvc-part8.md)</span></span>

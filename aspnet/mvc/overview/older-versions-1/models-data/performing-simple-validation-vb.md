---
uid: mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
title: Provedení jednoduchého ověření (VB) | Dokumentace Microsoftu
author: StephenWalther
description: Zjistěte, jak provést ověření v aplikaci ASP.NET MVC. V tomto kurzu se zavádí Stephen Walther vám stav modelu a pomocná rutina pro ověření HTML...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: df6cf4b7-0bb3-4c4e-b17a-bd78a759a6bc
msc.legacyurl: /mvc/overview/older-versions-1/models-data/performing-simple-validation-vb
msc.type: authoredcontent
ms.openlocfilehash: 1d0bd6917bab61b17d1cafcf0cd9eb1983275dc8
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/01/2019
ms.locfileid: "57075955"
---
<a name="performing-simple-validation-vb"></a><span data-ttu-id="551a1-104">Provedení jednoduchého ověření (VB)</span><span class="sxs-lookup"><span data-stu-id="551a1-104">Performing Simple Validation (VB)</span></span>
====================
<span data-ttu-id="551a1-105">podle [Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="551a1-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="551a1-106">Zjistěte, jak provést ověření v aplikaci ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="551a1-106">Learn how to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="551a1-107">V tomto kurzu se zavádí Stephen Walther vám stav modelu a pomocných rutin HTML ověření.</span><span class="sxs-lookup"><span data-stu-id="551a1-107">In this tutorial, Stephen Walther introduces you to model state and the validation HTML helpers.</span></span>


<span data-ttu-id="551a1-108">Cílem tohoto kurzu je vysvětlují, jak můžete provést ověření v rámci aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="551a1-108">The goal of this tutorial is to explain how you can perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="551a1-109">Například se dozvíte, jak zabránit odeslání formuláře, který neobsahuje hodnotu pro požadované pole.</span><span class="sxs-lookup"><span data-stu-id="551a1-109">For example, you learn how to prevent someone from submitting a form that does not contain a value for a required field.</span></span> <span data-ttu-id="551a1-110">Zjistíte, jak používat stav modelu a pomocných rutin HTML ověření.</span><span class="sxs-lookup"><span data-stu-id="551a1-110">You learn how to use model state and the validation HTML helpers.</span></span>

## <a name="understanding-model-state"></a><span data-ttu-id="551a1-111">Porozumění stavu modelu</span><span class="sxs-lookup"><span data-stu-id="551a1-111">Understanding Model State</span></span>

<span data-ttu-id="551a1-112">Používáte stav modelu - nebo přesněji, slovník stavu modelu – pro reprezentaci chyby ověření.</span><span class="sxs-lookup"><span data-stu-id="551a1-112">You use model state - or more accurately, the model state dictionary - to represent validation errors.</span></span> <span data-ttu-id="551a1-113">Například akce Create() ve výpisu 1 ověří vlastnosti třídy produktu před přidáním třídy produktu do databáze.</span><span class="sxs-lookup"><span data-stu-id="551a1-113">For example, the Create() action in Listing 1 validates the properties of a Product class before adding the Product class to a database.</span></span>


<span data-ttu-id="551a1-114">Můžu mi doporučujeme přidat logiku ověřování nebo databáze do kontroleru.</span><span class="sxs-lookup"><span data-stu-id="551a1-114">I'm not recommending that you add your validation or database logic to a controller.</span></span> <span data-ttu-id="551a1-115">Kontroler může obsahovat pouze logiku související řízení toku aplikace.</span><span class="sxs-lookup"><span data-stu-id="551a1-115">A controller should contain only logic related to application flow control.</span></span> <span data-ttu-id="551a1-116">Zástupce pro zjednodušení jsme se rozhodli.</span><span class="sxs-lookup"><span data-stu-id="551a1-116">We are taking a shortcut to keep things simple.</span></span>


<span data-ttu-id="551a1-117">**Výpis 1 - Controllers\ProductController.vb**</span><span class="sxs-lookup"><span data-stu-id="551a1-117">**Listing 1 - Controllers\ProductController.vb**</span></span>

[!code-vb[Main](performing-simple-validation-vb/samples/sample1.vb)]

<span data-ttu-id="551a1-118">V informacích 1 se ověří název, popis a UnitsInStock vlastnosti třídy produktu.</span><span class="sxs-lookup"><span data-stu-id="551a1-118">In Listing 1, the Name, Description, and UnitsInStock properties of the Product class are validated.</span></span> <span data-ttu-id="551a1-119">Pokud selže některý z těchto vlastností ověřovací test chybu se přidá do slovníku stavů modelu (reprezentovaný identifikátorem ModelState vlastnost třídy Controller).</span><span class="sxs-lookup"><span data-stu-id="551a1-119">If any of these properties fail a validation test then an error is added to the model state dictionary (represented by the ModelState property of the Controller class).</span></span>

<span data-ttu-id="551a1-120">Pokud nejsou žádné chyby v modelu stavu ModelState.IsValid vlastnost vrátí hodnotu false.</span><span class="sxs-lookup"><span data-stu-id="551a1-120">If there are any errors in model state then the ModelState.IsValid property returns false.</span></span> <span data-ttu-id="551a1-121">V takovém případě se zobrazí znovu formuláře HTML pro vytvoření nového produktu.</span><span class="sxs-lookup"><span data-stu-id="551a1-121">In that case, the HTML form for creating a new product is redisplayed.</span></span> <span data-ttu-id="551a1-122">Jinak pokud nejsou žádné chyby ověření, se přidá nového produktu do databáze.</span><span class="sxs-lookup"><span data-stu-id="551a1-122">Otherwise, if there are no validation errors, the new Product is added to the database.</span></span>

## <a name="using-the-validation-helpers"></a><span data-ttu-id="551a1-123">Použití pomocných rutin ověření</span><span class="sxs-lookup"><span data-stu-id="551a1-123">Using the Validation Helpers</span></span>

<span data-ttu-id="551a1-124">Architektura ASP.NET MVC zahrnuje dvě pomocné rutiny ověření: pomocné rutiny Html.ValidationMessage() a Html.ValidationSummary() pomocné rutiny.</span><span class="sxs-lookup"><span data-stu-id="551a1-124">The ASP.NET MVC framework includes two validation helpers: the Html.ValidationMessage() helper and the Html.ValidationSummary() helper.</span></span> <span data-ttu-id="551a1-125">Pomocí těchto dvou pomocných rutin v zobrazení zobrazují chybové zprávy ověření.</span><span class="sxs-lookup"><span data-stu-id="551a1-125">You use these two helpers in a view to display validation error messages.</span></span>

<span data-ttu-id="551a1-126">Pomocné rutiny Html.ValidationMessage() a Html.ValidationSummary() se používají ve vytvoření a úprava zobrazení, která jsou automaticky generovány generování uživatelského rozhraní ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="551a1-126">The Html.ValidationMessage() and Html.ValidationSummary() helpers are used in the Create and Edit views that are generated automatically by the ASP.NET MVC scaffolding.</span></span> <span data-ttu-id="551a1-127">Postupujte podle těchto kroků vygenerujete vytvořit zobrazení:</span><span class="sxs-lookup"><span data-stu-id="551a1-127">Follow these steps to generate the Create view:</span></span>

1. <span data-ttu-id="551a1-128">Klikněte pravým tlačítkem na Create() akce v kontroleru produktu a vyberte možnost nabídky **přidat zobrazení** (viz obrázek 1).</span><span class="sxs-lookup"><span data-stu-id="551a1-128">Right-click the Create() action in the Product controller and select the menu option **Add View** (see Figure 1).</span></span>
2. <span data-ttu-id="551a1-129">V **přidat zobrazení** dialogového okna, zaškrtněte políčko s popiskem **vytvoření zobrazení se silnými typy** (viz obrázek 2).</span><span class="sxs-lookup"><span data-stu-id="551a1-129">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view** (see Figure 2).</span></span>
3. <span data-ttu-id="551a1-130">Z **zobrazení dat třídy** rozevíracího seznamu vyberte třídu produktu.</span><span class="sxs-lookup"><span data-stu-id="551a1-130">From the **View data class** dropdown list, select the Product class.</span></span>
4. <span data-ttu-id="551a1-131">Z **zobrazit obsah** rozevíracího seznamu vyberte možnost vytvořit.</span><span class="sxs-lookup"><span data-stu-id="551a1-131">From the **View content** dropdown list, select Create.</span></span>
5. <span data-ttu-id="551a1-132">Klikněte na tlačítko **Přidat**.</span><span class="sxs-lookup"><span data-stu-id="551a1-132">Click the **Add** button.</span></span>


<span data-ttu-id="551a1-133">Ujistěte se, že vytváříte aplikaci před přidáním zobrazení.</span><span class="sxs-lookup"><span data-stu-id="551a1-133">Make sure that you build your application before adding a view.</span></span> <span data-ttu-id="551a1-134">V opačném případě nebude zobrazovat seznam tříd **zobrazení dat třídy** rozevíracího seznamu.</span><span class="sxs-lookup"><span data-stu-id="551a1-134">Otherwise, the list of classes won't appear in the **View data class** dropdown list.</span></span>


<span data-ttu-id="551a1-135">[![Dialogové okno Nový projekt](performing-simple-validation-vb/_static/image1.jpg)](performing-simple-validation-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="551a1-135">[![The New Project dialog box](performing-simple-validation-vb/_static/image1.jpg)](performing-simple-validation-vb/_static/image1.png)</span></span>

<span data-ttu-id="551a1-136">**Obrázek 01**: Přidání zobrazení ([kliknutím ji zobrazíte obrázek v plné velikosti](performing-simple-validation-vb/_static/image2.png))</span><span class="sxs-lookup"><span data-stu-id="551a1-136">**Figure 01**: Adding a view([Click to view full-size image](performing-simple-validation-vb/_static/image2.png))</span></span>


<span data-ttu-id="551a1-137">[![Dialogové okno Nový projekt](performing-simple-validation-vb/_static/image2.jpg)](performing-simple-validation-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="551a1-137">[![The New Project dialog box](performing-simple-validation-vb/_static/image2.jpg)](performing-simple-validation-vb/_static/image3.png)</span></span>

<span data-ttu-id="551a1-138">**Obrázek 02**: Vytvoření zobrazení se silnými typy ([kliknutím ji zobrazíte obrázek v plné velikosti](performing-simple-validation-vb/_static/image4.png))</span><span class="sxs-lookup"><span data-stu-id="551a1-138">**Figure 02**: Creating a strongly-typed view ([Click to view full-size image](performing-simple-validation-vb/_static/image4.png))</span></span>


<span data-ttu-id="551a1-139">Po dokončení těchto kroků, získáte v informacích 2 zobrazení pro vytváření.</span><span class="sxs-lookup"><span data-stu-id="551a1-139">After you complete these steps, you get the Create view in Listing 2.</span></span>

<span data-ttu-id="551a1-140">**Listing 2 - Views\Product\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="551a1-140">**Listing 2 - Views\Product\Create.aspx**</span></span>

[!code-aspx[Main](performing-simple-validation-vb/samples/sample2.aspx)]

<span data-ttu-id="551a1-141">V informacích 2 nazývá Html.ValidationSummary() pomocné rutiny okamžitě nad formuláře HTML.</span><span class="sxs-lookup"><span data-stu-id="551a1-141">In Listing 2, the Html.ValidationSummary() helper is called immediately above the HTML form.</span></span> <span data-ttu-id="551a1-142">Tato pomocná slouží k zobrazení seznam chybových zpráv ověření.</span><span class="sxs-lookup"><span data-stu-id="551a1-142">This helper is used to display a list of validation error messages.</span></span> <span data-ttu-id="551a1-143">Pomocná rutina Html.ValidationSummary() vykreslí chyby v seznamu s odrážkami.</span><span class="sxs-lookup"><span data-stu-id="551a1-143">The Html.ValidationSummary() helper renders the errors in a bulleted list.</span></span>

<span data-ttu-id="551a1-144">Pomocná rutina Html.ValidationMessage() se nazývá vedle každého pole formuláře HTML.</span><span class="sxs-lookup"><span data-stu-id="551a1-144">The Html.ValidationMessage() helper is called next to each of the HTML form fields.</span></span> <span data-ttu-id="551a1-145">Tato pomocná slouží k zobrazení chybové zprávy přímo vedle pole formuláře.</span><span class="sxs-lookup"><span data-stu-id="551a1-145">This helper is used to display an error message right next to a form field.</span></span> <span data-ttu-id="551a1-146">V případě výpis 2 zobrazí pomocná Html.ValidationMessage() hvězdičky, když dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="551a1-146">In the case of Listing 2, the Html.ValidationMessage() helper displays an asterisk when there is an error.</span></span>

<span data-ttu-id="551a1-147">Na stránce na obrázku 3 znázorňuje chybové zprávy, který je vykreslen metodou ověřování pomocné rutiny, když se odešle formulář, chybějící pole a neplatné hodnoty.</span><span class="sxs-lookup"><span data-stu-id="551a1-147">The page in Figure 3 illustrates the error messages rendered by the validation helpers when the form is submitted with missing fields and invalid values.</span></span>


<span data-ttu-id="551a1-148">[![Dialogové okno Nový projekt](performing-simple-validation-vb/_static/image3.jpg)](performing-simple-validation-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="551a1-148">[![The New Project dialog box](performing-simple-validation-vb/_static/image3.jpg)](performing-simple-validation-vb/_static/image5.png)</span></span>

<span data-ttu-id="551a1-149">**Obrázek 03**: Zobrazení pro vytváření odeslanou s problémy ([kliknutím ji zobrazíte obrázek v plné velikosti](performing-simple-validation-vb/_static/image6.png))</span><span class="sxs-lookup"><span data-stu-id="551a1-149">**Figure 03**: The Create view submitted with problems ([Click to view full-size image](performing-simple-validation-vb/_static/image6.png))</span></span>


<span data-ttu-id="551a1-150">Všimněte si, že vzhled HTML vstupní pole se nezmění, i když dojde k chybě ověřování.</span><span class="sxs-lookup"><span data-stu-id="551a1-150">Notice that the appearance of the HTML input fields are also modified when there is a validation error.</span></span> <span data-ttu-id="551a1-151">Pomocné rutiny vykreslení Html.TextBox() *třídy = "Chyba vstupu ověřování"* atribut, když dojde k chybě ověřování přidružený k vlastnosti vykreslen metodou Html.TextBox() helper.</span><span class="sxs-lookup"><span data-stu-id="551a1-151">The Html.TextBox() helper renders a *class="input-validation-error"* attribute when there is a validation error associated with the property rendered by the Html.TextBox() helper.</span></span>

<span data-ttu-id="551a1-152">Existují tři CSS třídy List stylu používat k ovládání výskyt chyb ověřování:</span><span class="sxs-lookup"><span data-stu-id="551a1-152">There are three cascading style sheet classes used to control the appearance of validation errors:</span></span>

- <span data-ttu-id="551a1-153">vstup-– Chyba ověřování – použít &lt;vstupní&gt; vykreslen metodou Html.TextBox() helper značky.</span><span class="sxs-lookup"><span data-stu-id="551a1-153">input-validation-error - Applied to the &lt;input&gt; tag rendered by Html.TextBox() helper.</span></span>
- <span data-ttu-id="551a1-154">pole – – Chyba ověřování – použít &lt;span&gt; vykreslen metodou Html.ValidationMessage() helper značky.</span><span class="sxs-lookup"><span data-stu-id="551a1-154">field-validation-error - Applied to the &lt;span&gt; tag rendered by the Html.ValidationMessage() helper.</span></span>
- <span data-ttu-id="551a1-155">summary – chyby ověřování - použít &lt;ul&gt; vykreslen metodou Html.ValidationSumamry() helper značky.</span><span class="sxs-lookup"><span data-stu-id="551a1-155">validation-summary-errors - Applied to the &lt;ul&gt; tag rendered by the Html.ValidationSumamry() helper.</span></span>

<span data-ttu-id="551a1-156">Můžete upravit tyto šablony třídy List stylu a proto upravit vzhled chyby ověření tak, že upravíte soubor Site.css umístěný ve složce obsahu.</span><span class="sxs-lookup"><span data-stu-id="551a1-156">You can modify these cascading style sheet classes, and therefore modify the appearance of the validation errors, by modifying the Site.css file located in the Content folder.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="551a1-157">Třída HtmlHelper obsahuje statické vlastnosti jen pro čtení pro načítání názvů ověřování související s CSS třídy.</span><span class="sxs-lookup"><span data-stu-id="551a1-157">The HtmlHelper class includes read-only static properties for retrieving the names of the validation related CSS classes.</span></span> <span data-ttu-id="551a1-158">Tyto statické vlastnosti jsou pojmenovány ValidationInputCssClassName ValidationFieldCssClassName a ValidationSummaryCssClassName.</span><span class="sxs-lookup"><span data-stu-id="551a1-158">These static properties are named ValidationInputCssClassName, ValidationFieldCssClassName, and ValidationSummaryCssClassName.</span></span>


## <a name="prebinding-validation-and-postbinding-validation"></a><span data-ttu-id="551a1-159">Prebinding ověřování a ověřování Postbinding</span><span class="sxs-lookup"><span data-stu-id="551a1-159">Prebinding Validation and Postbinding Validation</span></span>

<span data-ttu-id="551a1-160">Pokud odeslání formuláře HTML pro vytváření produktu, a zadáte neplatnou hodnotu pro pole price a žádná hodnota pro pole UnitsInStock, získáte ověřovacích zpráv, který zobrazí obrázek 4.</span><span class="sxs-lookup"><span data-stu-id="551a1-160">If you submit the HTML form for creating a Product, and you enter an invalid value for the price field and no value for the UnitsInStock field, then you'll get the validation messages displayed in Figure 4.</span></span> <span data-ttu-id="551a1-161">Odkud pocházejí tyto chybových zpráv ověření ze?</span><span class="sxs-lookup"><span data-stu-id="551a1-161">Where do these validation error messages come from?</span></span>


<span data-ttu-id="551a1-162">[![Dialogové okno Nový projekt](performing-simple-validation-vb/_static/image4.jpg)](performing-simple-validation-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="551a1-162">[![The New Project dialog box](performing-simple-validation-vb/_static/image4.jpg)](performing-simple-validation-vb/_static/image7.png)</span></span>

<span data-ttu-id="551a1-163">**Obrázek 04**: Prebinding chyby ověření ([kliknutím ji zobrazíte obrázek v plné velikosti](performing-simple-validation-vb/_static/image8.png))</span><span class="sxs-lookup"><span data-stu-id="551a1-163">**Figure 04**: Prebinding Validation Errors([Click to view full-size image](performing-simple-validation-vb/_static/image8.png))</span></span>


<span data-ttu-id="551a1-164">Existují ve skutečnosti dva typy chybových zpráv ověření – těch, které generuje předtím, než pole formuláře HTML, které jsou vázány na třídu a jsou generovány po polí formuláře, které jsou vázány na třídu.</span><span class="sxs-lookup"><span data-stu-id="551a1-164">There are actually two types of validation error messages - those generated before the HTML form fields are bound to a class and those generated after the form fields are bound to the class.</span></span> <span data-ttu-id="551a1-165">Jinými slovy, existují prebinding chyby ověření a postbinding chyby ověření.</span><span class="sxs-lookup"><span data-stu-id="551a1-165">In other words, there are prebinding validation errors and postbinding validation errors.</span></span>

<span data-ttu-id="551a1-166">Akce Create() vystavené kontroler produktu v informacích 1 přijímá instanci třídy produktu.</span><span class="sxs-lookup"><span data-stu-id="551a1-166">The Create() action exposed by the Product controller in Listing 1 accepts an instance of the Product class.</span></span> <span data-ttu-id="551a1-167">Podpis metody Create vypadá takto:</span><span class="sxs-lookup"><span data-stu-id="551a1-167">The signature of the Create method looks like this:</span></span>

[!code-vb[Main](performing-simple-validation-vb/samples/sample3.vb)]

<span data-ttu-id="551a1-168">Hodnoty polí formuláře HTML z formuláře vytvořit jsou vázány na třídu productToCreate se nazývá vazač modelu.</span><span class="sxs-lookup"><span data-stu-id="551a1-168">The values of the HTML form fields from the Create form are bound to the productToCreate class by something called a model binder.</span></span> <span data-ttu-id="551a1-169">Výchozí vazač modelu přidá chybovou zprávu do stavu modelu automaticky při pole formuláře nemůže vytvořit vazbu na vlastnost formuláře.</span><span class="sxs-lookup"><span data-stu-id="551a1-169">The default model binder adds an error message to model state automatically when it cannot bind a form field to a form property.</span></span>

<span data-ttu-id="551a1-170">Výchozí vazač modelu nelze vytvořit vazbu řetězec "apple" Price vlastnosti třídy produktu.</span><span class="sxs-lookup"><span data-stu-id="551a1-170">The default model binder cannot bind the string "apple" to the Price property of the Product class.</span></span> <span data-ttu-id="551a1-171">Vlastnost typu desetinného čísla nelze přiřadit řetězec.</span><span class="sxs-lookup"><span data-stu-id="551a1-171">You can't assign a string to a decimal property.</span></span> <span data-ttu-id="551a1-172">Proto přidá vazač modelu chybu do stavu modelu.</span><span class="sxs-lookup"><span data-stu-id="551a1-172">Therefore, the model binder adds an error to model state.</span></span>

<span data-ttu-id="551a1-173">Výchozí vazač modelu také nelze přiřadit hodnotu Nothing vlastnost, která nepřijímá hodnotu Nothing.</span><span class="sxs-lookup"><span data-stu-id="551a1-173">The default model binder also cannot assign the value Nothing to a property that does not accept the value Nothing.</span></span> <span data-ttu-id="551a1-174">Zejména vazače modelu nelze přiřadit hodnotu Nothing UnitsInStock vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="551a1-174">In particular, the model binder cannot assign the value Nothing to the UnitsInStock property.</span></span> <span data-ttu-id="551a1-175">Vazač modelu zase vrací a přidá chybovou zprávu do stavu modelu.</span><span class="sxs-lookup"><span data-stu-id="551a1-175">Once again, the model binder gives up and adds an error message to model state.</span></span>

<span data-ttu-id="551a1-176">Pokud chcete přizpůsobit vzhled tyto prebinding chybové zprávy je potřeba vytvořit prostředek řetězce pro tyto zprávy.</span><span class="sxs-lookup"><span data-stu-id="551a1-176">If you want to customize the appearance of these prebinding error messages then you need to create resource strings for these messages.</span></span>

## <a name="summary"></a><span data-ttu-id="551a1-177">Souhrn</span><span class="sxs-lookup"><span data-stu-id="551a1-177">Summary</span></span>

<span data-ttu-id="551a1-178">Cílem tohoto kurzu bylo popisují základní mechanismy ověřování v rozhraní ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="551a1-178">The goal of this tutorial was to describe the basic mechanics of validation in the ASP.NET MVC framework.</span></span> <span data-ttu-id="551a1-179">Jste zjistili, jak používat stav modelu a pomocných rutin HTML ověření.</span><span class="sxs-lookup"><span data-stu-id="551a1-179">You learned how to use model state and the validation HTML helpers.</span></span> <span data-ttu-id="551a1-180">Také jsme probírali rozdíl mezi prebinding a postbinding ověření.</span><span class="sxs-lookup"><span data-stu-id="551a1-180">We also discussed the distinction between prebinding and postbinding validation.</span></span> <span data-ttu-id="551a1-181">V dalších kurzech používání probereme různé strategie pro přesun kód pro ověření vašeho řadiče a do vaší třídy modelu.</span><span class="sxs-lookup"><span data-stu-id="551a1-181">In other tutorials, we'll discuss various strategies for moving your validation code out of your controllers and into your model classes.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="551a1-182">[Předchozí](displaying-a-table-of-database-data-vb.md)
> [další](validating-with-the-idataerrorinfo-interface-vb.md)</span><span class="sxs-lookup"><span data-stu-id="551a1-182">[Previous](displaying-a-table-of-database-data-vb.md)
[Next](validating-with-the-idataerrorinfo-interface-vb.md)</span></span>
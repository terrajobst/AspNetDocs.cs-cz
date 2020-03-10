---
uid: mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
title: Ověřování pomocí validátorů datových poznámek (C#) | Microsoft Docs
author: microsoft
description: Využijte výhod modelu datových poznámek, abyste mohli provádět ověřování v rámci aplikace ASP.NET MVC. Naučte se používat různé typy validátoru...
ms.author: riande
ms.date: 05/29/2009
ms.assetid: 7ca8013e-9dfc-4e33-8336-cdccfd5f9414
msc.legacyurl: /mvc/overview/older-versions-1/models-data/validation-with-the-data-annotation-validators-cs
msc.type: authoredcontent
ms.openlocfilehash: e154384c08adf0c14920afff85e983a67b41707c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542131"
---
# <a name="validation-with-the-data-annotation-validators-c"></a><span data-ttu-id="052ef-104">Ověřování validátory datových poznámek (C#)</span><span class="sxs-lookup"><span data-stu-id="052ef-104">Validation with the Data Annotation Validators (C#)</span></span>

<span data-ttu-id="052ef-105">od [Microsoftu](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="052ef-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="052ef-106">Využijte výhod modelu datových poznámek, abyste mohli provádět ověřování v rámci aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="052ef-106">Take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="052ef-107">Naučte se používat různé typy atributů validátoru a pracovat s nimi v Microsoft Entity Framework.</span><span class="sxs-lookup"><span data-stu-id="052ef-107">Learn how to use the different types of validator attributes and work with them in the Microsoft Entity Framework.</span></span>

<span data-ttu-id="052ef-108">V tomto kurzu se naučíte, jak pomocí validátorů datových poznámek provádět ověřování v aplikaci ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="052ef-108">In this tutorial, you learn how to use the Data Annotation validators to perform validation in an ASP.NET MVC application.</span></span> <span data-ttu-id="052ef-109">Výhodou použití validátorů datových poznámek je, že vám umožňují provádět ověřování jednoduše přidáním jednoho nebo více atributů, jako je například povinný nebo StringLength atribut – na vlastnost třídy.</span><span class="sxs-lookup"><span data-stu-id="052ef-109">The advantage of using the Data Annotation validators is that they enable you to perform validation simply by adding one or more attributes – such as the Required or StringLength attribute – to a class property.</span></span>

<span data-ttu-id="052ef-110">Předtím, než budete moci použít validátory datových poznámek, je nutné stáhnout pořadač modelů datových poznámek.</span><span class="sxs-lookup"><span data-stu-id="052ef-110">Before you can use the Data Annotation validators, you must download the Data Annotations Model Binder.</span></span> <span data-ttu-id="052ef-111">Ukázku pořadače datových poznámek si můžete stáhnout z webu CodePlex kliknutím [sem](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span><span class="sxs-lookup"><span data-stu-id="052ef-111">You can download the Data Annotations Model Binder Sample from the CodePlex website by clicking [here](http://aspnet.codeplex.com/Release/ProjectReleases.aspx?ReleaseId=24471).</span></span>

<span data-ttu-id="052ef-112">Je důležité si uvědomit, že pořadač pro datové poznámky není oficiální součástí rozhraní Microsoft ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="052ef-112">It is important to understand that the Data Annotations Model Binder is not an official part of the Microsoft ASP.NET MVC framework.</span></span> <span data-ttu-id="052ef-113">I když je pořadač modelů datových poznámek vytvořený týmem Microsoft ASP.NET MVC, Microsoft nenabízí oficiální podporu produktu pro model datových poznámek s popisem a použitý v tomto kurzu.</span><span class="sxs-lookup"><span data-stu-id="052ef-113">Although the Data Annotations Model Binder was created by the Microsoft ASP.NET MVC team, Microsoft does not offer official product support for the Data Annotations Model Binder described and used in this tutorial.</span></span>

## <a name="using-the-data-annotation-model-binder"></a><span data-ttu-id="052ef-114">Použití pořadače modelů datových poznámek</span><span class="sxs-lookup"><span data-stu-id="052ef-114">Using the Data Annotation Model Binder</span></span>

<span data-ttu-id="052ef-115">Aby bylo možné použít Bindery modelu datových poznámek v aplikaci ASP.NET MVC, musíte nejprve přidat odkaz na sestavení Microsoft. Web. Mvc. DataAnnotations. dll a sestavení System. ComponentModel. DataAnnotations. dll.</span><span class="sxs-lookup"><span data-stu-id="052ef-115">In order to use the Data Annotations Model Binder in an ASP.NET MVC application, you first need to add a reference to the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly.</span></span> <span data-ttu-id="052ef-116">Vyberte projekt možnosti nabídky **, přidat odkaz**.</span><span class="sxs-lookup"><span data-stu-id="052ef-116">Select the menu option **Project, Add Reference**.</span></span> <span data-ttu-id="052ef-117">Potom klikněte na kartu **Procházet** a přejděte do umístění, kam jste stáhli (a odeberou) ukázku pořadače datových poznámek (viz **Obrázek 1**).</span><span class="sxs-lookup"><span data-stu-id="052ef-117">Next click the **Browse** tab and browse to the location where you downloaded (and unzipped) the Data Annotations Model Binder sample (see **Figure 1**).</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image2.png)](validation-with-the-data-annotation-validators-cs/_static/image1.png)

<span data-ttu-id="052ef-118">**Obrázek 1**: Přidání odkazu na pořadač modelů datových poznámek ([kliknutím zobrazíte obrázek v plné velikosti](validation-with-the-data-annotation-validators-cs/_static/image3.png))</span><span class="sxs-lookup"><span data-stu-id="052ef-118">**Figure 1**: Adding a reference to the Data Annotations Model Binder ([Click to view full-size image](validation-with-the-data-annotation-validators-cs/_static/image3.png))</span></span>

<span data-ttu-id="052ef-119">Vyberte sestavení Microsoft. Web. Mvc. DataAnnotations. dll a System. ComponentModel. DataAnnotations. dll a klikněte na tlačítko **OK** .</span><span class="sxs-lookup"><span data-stu-id="052ef-119">Select both the Microsoft.Web.Mvc.DataAnnotations.dll assembly and the System.ComponentModel.DataAnnotations.dll assembly and click the **OK** button.</span></span>

<span data-ttu-id="052ef-120">Sestavení System. ComponentModel. DataAnnotations. dll, které je součástí .NET Framework Service Pack 1, nelze použít u pořadače modelů datových poznámek.</span><span class="sxs-lookup"><span data-stu-id="052ef-120">You cannot use the System.ComponentModel.DataAnnotations.dll assembly included with .NET Framework Service Pack 1 with the Data Annotations Model Binder.</span></span> <span data-ttu-id="052ef-121">Je nutné použít verzi sestavení System. ComponentModel. DataAnnotations. dll zahrnuté v ukázce stažení modelu datových poznámek.</span><span class="sxs-lookup"><span data-stu-id="052ef-121">You must use the version of the System.ComponentModel.DataAnnotations.dll assembly included with the Data Annotations Model Binder Sample download.</span></span>

<span data-ttu-id="052ef-122">Nakonec je nutné zaregistrovat pořadač modelu DataAnnotations v souboru Global. asax.</span><span class="sxs-lookup"><span data-stu-id="052ef-122">Finally, you need to register the DataAnnotations Model Binder in the Global.asax file.</span></span> <span data-ttu-id="052ef-123">Přidejte následující řádek kódu do obslužné rutiny události aplikace\_Start (), aby metoda Application\_Start () vypadala takto:</span><span class="sxs-lookup"><span data-stu-id="052ef-123">Add the following line of code to the Application\_Start() event handler so that the Application\_Start() method looks like this:</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample1.cs)]

<span data-ttu-id="052ef-124">Tento řádek kódu registruje ataAnnotationsModelBinder jako výchozí modelový pořadač pro celou aplikaci ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="052ef-124">This line of code registers the ataAnnotationsModelBinder as the default model binder for the entire ASP.NET MVC application.</span></span>

## <a name="using-the-data-annotation-validator-attributes"></a><span data-ttu-id="052ef-125">Používání atributů validátoru datových poznámek</span><span class="sxs-lookup"><span data-stu-id="052ef-125">Using the Data Annotation Validator Attributes</span></span>

<span data-ttu-id="052ef-126">Při použití pořadače datových poznámek pomocí atributů validátoru provedete ověření.</span><span class="sxs-lookup"><span data-stu-id="052ef-126">When you use the Data Annotations Model Binder, you use validator attributes to perform validation.</span></span> <span data-ttu-id="052ef-127">Obor názvů System. ComponentModel. DataAnnotations obsahuje následující atributy validátoru:</span><span class="sxs-lookup"><span data-stu-id="052ef-127">The System.ComponentModel.DataAnnotations namespace includes the following validator attributes:</span></span>

- <span data-ttu-id="052ef-128">Rozsah – umožňuje ověřit, zda hodnota vlastnosti spadá mezi zadaný rozsah hodnot.</span><span class="sxs-lookup"><span data-stu-id="052ef-128">Range – Enables you to validate whether the value of a property falls between a specified range of values.</span></span>
- <span data-ttu-id="052ef-129">RegularExpression – umožňuje ověřit, zda hodnota vlastnosti odpovídá zadanému vzoru regulárního výrazu.</span><span class="sxs-lookup"><span data-stu-id="052ef-129">RegularExpression – Enables you to validate whether the value of a property matches a specified regular expression pattern.</span></span>
- <span data-ttu-id="052ef-130">Požadováno – umožňuje označit vlastnost jako povinnou.</span><span class="sxs-lookup"><span data-stu-id="052ef-130">Required – Enables you to mark a property as required.</span></span>
- <span data-ttu-id="052ef-131">StringLength – umožňuje zadat maximální délku řetězcové vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="052ef-131">StringLength – Enables you to specify a maximum length for a string property.</span></span>
- <span data-ttu-id="052ef-132">Ověření – základní třída pro všechny atributy validátoru.</span><span class="sxs-lookup"><span data-stu-id="052ef-132">Validation – The base class for all validator attributes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="052ef-133">Pokud vaše požadavky na ověření nejsou splněné pomocí žádného ze standardních validátorů, budete mít vždy možnost vytvořit vlastní atribut validátoru děděním nového atributu validátoru z atributu základní ověření.</span><span class="sxs-lookup"><span data-stu-id="052ef-133">If your validation needs are not satisfied by any of the standard validators then you always have the option of creating a custom validator attribute by inheriting a new validator attribute from the base Validation attribute.</span></span>

<span data-ttu-id="052ef-134">Třída Product v **seznamu 1** ukazuje, jak používat tyto atributy validátoru.</span><span class="sxs-lookup"><span data-stu-id="052ef-134">The Product class in **Listing 1** illustrates how to use these validator attributes.</span></span> <span data-ttu-id="052ef-135">Vlastnosti název, popis a JednotkováCena jsou označeny jako povinné.</span><span class="sxs-lookup"><span data-stu-id="052ef-135">The Name, Description, and UnitPrice properties are marked as required.</span></span> <span data-ttu-id="052ef-136">Vlastnost Name musí mít délku řetězce, který je kratší než 10 znaků.</span><span class="sxs-lookup"><span data-stu-id="052ef-136">The Name property must have a string length that is less than 10 characters.</span></span> <span data-ttu-id="052ef-137">Nakonec musí vlastnost UnitPrice odpovídat vzoru regulárního výrazu, který představuje částku měny.</span><span class="sxs-lookup"><span data-stu-id="052ef-137">Finally, the UnitPrice property must match a regular expression pattern that represents a currency amount.</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample2.cs)]

<span data-ttu-id="052ef-138">**Výpis 1**: Models\Product.cs</span><span class="sxs-lookup"><span data-stu-id="052ef-138">**Listing 1**: Models\Product.cs</span></span>

<span data-ttu-id="052ef-139">Třída Product ukazuje, jak použít jeden další atribut: atribut DisplayName.</span><span class="sxs-lookup"><span data-stu-id="052ef-139">The Product class illustrates how to use one additional attribute: the DisplayName attribute.</span></span> <span data-ttu-id="052ef-140">Atribut DisplayName umožňuje upravit název vlastnosti, když je vlastnost zobrazena v chybové zprávě.</span><span class="sxs-lookup"><span data-stu-id="052ef-140">The DisplayName attribute enables you to modify the name of the property when the property is displayed in an error message.</span></span> <span data-ttu-id="052ef-141">Místo zobrazení chybové zprávy "povinné pole UnitPrice" můžete zobrazit chybovou zprávu "pole Cena je povinné".</span><span class="sxs-lookup"><span data-stu-id="052ef-141">Instead of displaying the error message "The UnitPrice field is required" you can display the error message "The Price field is required".</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="052ef-142">Pokud chcete úplně přizpůsobit chybovou zprávu zobrazované validátorem, můžete k vlastnosti ErrorMessage validátoru přiřadit vlastní chybovou zprávu, například: `<Required(ErrorMessage:="This field needs a value!")>`</span><span class="sxs-lookup"><span data-stu-id="052ef-142">If you want to completely customize the error message displayed by a validator then you can assign a custom error message to the validator's ErrorMessage property like this: `<Required(ErrorMessage:="This field needs a value!")>`</span></span>

<span data-ttu-id="052ef-143">Můžete použít třídu Product v **seznamu 1** s akcí kontroleru vytvořit () v **seznamu 2**.</span><span class="sxs-lookup"><span data-stu-id="052ef-143">You can use the Product class in **Listing 1** with the Create() controller action in **Listing 2**.</span></span> <span data-ttu-id="052ef-144">Tato akce kontroleru znovu zobrazí zobrazení pro vytváření, pokud stav modelu obsahuje nějaké chyby.</span><span class="sxs-lookup"><span data-stu-id="052ef-144">This controller action redisplays the Create view when model state contains any errors.</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample3.cs)]

<span data-ttu-id="052ef-145">**Výpis 2**: Controllers\ProductController.vb</span><span class="sxs-lookup"><span data-stu-id="052ef-145">**Listing 2**: Controllers\ProductController.vb</span></span>

<span data-ttu-id="052ef-146">Nakonec můžete vytvořit zobrazení v **seznamu 3** kliknutím pravým tlačítkem myši na akci vytvořit () a výběrem možnosti nabídky **Přidat zobrazení**.</span><span class="sxs-lookup"><span data-stu-id="052ef-146">Finally, you can create the view in **Listing 3** by right-clicking the Create() action and selecting the menu option **Add View**.</span></span> <span data-ttu-id="052ef-147">Vytvořte zobrazení silného typu s třídou Product jako třídu modelu.</span><span class="sxs-lookup"><span data-stu-id="052ef-147">Create a strongly-typed view with the Product class as the model class.</span></span> <span data-ttu-id="052ef-148">V rozevíracím seznamu zobrazit obsah vyberte **vytvořit** (viz **Obrázek 2**).</span><span class="sxs-lookup"><span data-stu-id="052ef-148">Select **Create** from the view content dropdown list (see **Figure 2**).</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image5.png)](validation-with-the-data-annotation-validators-cs/_static/image4.png)

<span data-ttu-id="052ef-149">**Obrázek 2**: Přidání zobrazení pro vytvoření</span><span class="sxs-lookup"><span data-stu-id="052ef-149">**Figure 2**: Adding the Create View</span></span>

[!code-aspx[Main](validation-with-the-data-annotation-validators-cs/samples/sample4.aspx)]

<span data-ttu-id="052ef-150">**Výpis 3**: Views\Product\Create.aspx</span><span class="sxs-lookup"><span data-stu-id="052ef-150">**Listing 3**: Views\Product\Create.aspx</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="052ef-151">Odeberte pole ID z formuláře vytvořit generovaného pomocí možnosti nabídky **Přidat zobrazení** .</span><span class="sxs-lookup"><span data-stu-id="052ef-151">Remove the Id field from the Create form generated by the **Add View** menu option.</span></span> <span data-ttu-id="052ef-152">Vzhledem k tomu, že pole ID odpovídá sloupci identity, nechcete uživatelům povolit zadání hodnoty do tohoto pole.</span><span class="sxs-lookup"><span data-stu-id="052ef-152">Because the Id field corresponds to an Identity column, you don't want to allow users to enter a value for this field.</span></span>

<span data-ttu-id="052ef-153">Pokud odešlete formulář pro vytvoření produktu a nezadáte hodnoty pro požadovaná pole, zobrazí se chybové zprávy ověření na **obrázku 3** .</span><span class="sxs-lookup"><span data-stu-id="052ef-153">If you submit the form for creating a Product and you do not enter values for the required fields, then the validation error messages in **Figure 3** are displayed.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image7.png)](validation-with-the-data-annotation-validators-cs/_static/image6.png)

<span data-ttu-id="052ef-154">**Obrázek 3**: Chybí povinná pole</span><span class="sxs-lookup"><span data-stu-id="052ef-154">**Figure 3**: Missing required fields</span></span>

<span data-ttu-id="052ef-155">Pokud zadáte neplatnou hodnotu měny, zobrazí se chybová zpráva na **obrázku 4** .</span><span class="sxs-lookup"><span data-stu-id="052ef-155">If you enter an invalid currency amount, then the error message in **Figure 4** is displayed.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image9.png)](validation-with-the-data-annotation-validators-cs/_static/image8.png)

<span data-ttu-id="052ef-156">**Obrázek 4**: Neplatná částka měny</span><span class="sxs-lookup"><span data-stu-id="052ef-156">**Figure 4**: Invalid currency amount</span></span>

## <a name="using-data-annotation-validators-with-the-entity-framework"></a><span data-ttu-id="052ef-157">Použití validátorů datových poznámek pomocí Entity Framework</span><span class="sxs-lookup"><span data-stu-id="052ef-157">Using Data Annotation Validators with the Entity Framework</span></span>

<span data-ttu-id="052ef-158">Pokud používáte Microsoft Entity Framework k vygenerování tříd datového modelu, nemůžete použít atributy validátoru přímo na vaše třídy.</span><span class="sxs-lookup"><span data-stu-id="052ef-158">If you are using the Microsoft Entity Framework to generate your data model classes then you cannot apply the validator attributes directly to your classes.</span></span> <span data-ttu-id="052ef-159">Vzhledem k tomu, že Entity Framework Designer generuje třídy modelu, všechny změny, které provedete v třídách modelu, budou při příštím provedení změn v Návrháři přepsány.</span><span class="sxs-lookup"><span data-stu-id="052ef-159">Because the Entity Framework Designer generates the model classes, any changes you make to the model classes will be overwritten the next time you make any changes in the Designer.</span></span>

<span data-ttu-id="052ef-160">Chcete-li použít validátory s třídami generovanými Entity Framework pak je třeba vytvořit metaznačky datových tříd.</span><span class="sxs-lookup"><span data-stu-id="052ef-160">If you want to use the validators with the classes generated by the Entity Framework then you need to create meta data classes.</span></span> <span data-ttu-id="052ef-161">Validátory lze použít pro třídu meta data namísto použití validátorů na skutečnou třídu.</span><span class="sxs-lookup"><span data-stu-id="052ef-161">You apply the validators to the meta data class instead of applying the validators to the actual class.</span></span>

<span data-ttu-id="052ef-162">Představte si například, že jste vytvořili třídu filmů pomocí Entity Framework (viz **Obrázek 5**).</span><span class="sxs-lookup"><span data-stu-id="052ef-162">For example, imagine that you have created a Movie class using the Entity Framework (see **Figure 5**).</span></span> <span data-ttu-id="052ef-163">Představte si, že chcete, aby název filmu a vlastnosti režiséra byly povinné.</span><span class="sxs-lookup"><span data-stu-id="052ef-163">Imagine, furthermore, that you want to make the Movie Title and Director properties required properties.</span></span> <span data-ttu-id="052ef-164">V takovém případě můžete vytvořit částečnou třídu a třídu meta data v **seznamu 4**.</span><span class="sxs-lookup"><span data-stu-id="052ef-164">In that case, you can create the partial class and meta data class in **Listing 4**.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image11.png)](validation-with-the-data-annotation-validators-cs/_static/image10.png)

<span data-ttu-id="052ef-165">**Obrázek 5**: třída filmu vygenerovaná Entity Framework</span><span class="sxs-lookup"><span data-stu-id="052ef-165">**Figure 5**: Movie class generated by Entity Framework</span></span>

[!code-csharp[Main](validation-with-the-data-annotation-validators-cs/samples/sample5.cs)]

<span data-ttu-id="052ef-166">**Výpis 4**: Models\Movie.cs</span><span class="sxs-lookup"><span data-stu-id="052ef-166">**Listing 4**: Models\Movie.cs</span></span>

<span data-ttu-id="052ef-167">Soubor v **seznamu 4** obsahuje dvě třídy s názvem video a MovieMetaData.</span><span class="sxs-lookup"><span data-stu-id="052ef-167">The file in **Listing 4** contains two classes named Movie and MovieMetaData.</span></span> <span data-ttu-id="052ef-168">Třída Movie je částečnou třídou.</span><span class="sxs-lookup"><span data-stu-id="052ef-168">The Movie class is a partial class.</span></span> <span data-ttu-id="052ef-169">Odpovídá částečné třídě generované Entity Framework, která je obsažena v souboru datamode. Designer. vb.</span><span class="sxs-lookup"><span data-stu-id="052ef-169">It corresponds to the partial class generated by the Entity Framework that is contained in the DataModel.Designer.vb file.</span></span>

<span data-ttu-id="052ef-170">V současné době rozhraní .NET Framework nepodporuje částečné vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="052ef-170">Currently, the .NET framework does not support partial properties.</span></span> <span data-ttu-id="052ef-171">Proto neexistuje způsob, jak použít atributy validátoru na vlastnosti třídy filmu definované v souboru datamode. Designer. vb použitím atributů validátoru na vlastnosti třídy filmu definované v souboru v **seznamu 4**.</span><span class="sxs-lookup"><span data-stu-id="052ef-171">Therefore, there is no way to apply the validator attributes to the properties of the Movie class defined in the DataModel.Designer.vb file by applying the validator attributes to the properties of the Movie class defined in the file in **Listing 4**.</span></span>

<span data-ttu-id="052ef-172">Všimněte si, že částečná třída videa je upravena atributem MetadataType, který odkazuje na třídu MovieMetaData.</span><span class="sxs-lookup"><span data-stu-id="052ef-172">Notice that the Movie partial class is decorated with a MetadataType attribute that points at the MovieMetaData class.</span></span> <span data-ttu-id="052ef-173">Třída MovieMetaData obsahuje vlastnosti proxy serveru pro vlastnosti třídy video.</span><span class="sxs-lookup"><span data-stu-id="052ef-173">The MovieMetaData class contains proxy properties for the properties of the Movie class.</span></span>

<span data-ttu-id="052ef-174">Atributy validátoru jsou aplikovány na vlastnosti třídy MovieMetaData.</span><span class="sxs-lookup"><span data-stu-id="052ef-174">The validator attributes are applied to the properties of the MovieMetaData class.</span></span> <span data-ttu-id="052ef-175">Vlastnosti název, ředitel a DateReleased jsou všechny označené jako požadované vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="052ef-175">The Title, Director, and DateReleased properties are all marked as required properties.</span></span> <span data-ttu-id="052ef-176">Vlastnosti režiséra musí být přiřazen řetězec, který obsahuje méně než 5 znaků.</span><span class="sxs-lookup"><span data-stu-id="052ef-176">The Director property must be assigned a string that contains less than 5 characters.</span></span> <span data-ttu-id="052ef-177">Nakonec se atribut DisplayName aplikuje na vlastnost DateReleased, aby se zobrazila chybová zpráva, například pole Datum uvolnění je povinné.</span><span class="sxs-lookup"><span data-stu-id="052ef-177">Finally, the DisplayName attribute is applied to the DateReleased property to display an error message like "The Date Released field is required."</span></span> <span data-ttu-id="052ef-178">místo chyby "pole DateReleased je povinné."</span><span class="sxs-lookup"><span data-stu-id="052ef-178">instead of the error "The DateReleased field is required."</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="052ef-179">Všimněte si, že vlastnosti proxy v třídě MovieMetaData nemusejí představovat stejné typy jako odpovídající vlastnosti ve třídě Movie.</span><span class="sxs-lookup"><span data-stu-id="052ef-179">Notice that the proxy properties in the MovieMetaData class do not need to represent the same types as the corresponding properties in the Movie class.</span></span> <span data-ttu-id="052ef-180">Například vlastnost Director je vlastnost řetězce ve třídě Movie a vlastnost objektu ve třídě MovieMetaData.</span><span class="sxs-lookup"><span data-stu-id="052ef-180">For example, the Director property is a string property in the Movie class and an object property in the MovieMetaData class.</span></span>

<span data-ttu-id="052ef-181">Stránka na **obrázku 6** znázorňuje chybové zprávy vrácené při zadání neplatných hodnot vlastností videa.</span><span class="sxs-lookup"><span data-stu-id="052ef-181">The page in **Figure 6** illustrates the error messages returned when you enter invalid values for the Movie properties.</span></span>

[![](validation-with-the-data-annotation-validators-cs/_static/image13.png)](validation-with-the-data-annotation-validators-cs/_static/image12.png)

<span data-ttu-id="052ef-182">**Obrázek 6**: použití validátorů s entity frameworkem ([kliknutím zobrazíte obrázek v plné velikosti](validation-with-the-data-annotation-validators-cs/_static/image14.png))</span><span class="sxs-lookup"><span data-stu-id="052ef-182">**Figure 6**: Using validators with the Entity Framework ([Click to view full-size image](validation-with-the-data-annotation-validators-cs/_static/image14.png))</span></span>

## <a name="summary"></a><span data-ttu-id="052ef-183">Souhrn</span><span class="sxs-lookup"><span data-stu-id="052ef-183">Summary</span></span>

<span data-ttu-id="052ef-184">V tomto kurzu jste zjistili, jak můžete pomocí pořadače modelu datové poznámky využít k ověřování v rámci aplikace ASP.NET MVC.</span><span class="sxs-lookup"><span data-stu-id="052ef-184">In this tutorial, you learned how to take advantage of the Data Annotation Model Binder to perform validation within an ASP.NET MVC application.</span></span> <span data-ttu-id="052ef-185">Zjistili jste, jak používat různé typy atributů validátoru, jako jsou povinné a StringLength atributy.</span><span class="sxs-lookup"><span data-stu-id="052ef-185">You learned how to use the different types of validator attributes such as the Required and StringLength attributes.</span></span> <span data-ttu-id="052ef-186">Zjistili jste také, jak tyto atributy použít při práci s Entity Frameworkem Microsoft.</span><span class="sxs-lookup"><span data-stu-id="052ef-186">You also learned how to use these attributes when working with the Microsoft Entity Framework.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="052ef-187">[Předchozí](validating-with-a-service-layer-cs.md)
> [Další](creating-model-classes-with-the-entity-framework-vb.md)</span><span class="sxs-lookup"><span data-stu-id="052ef-187">[Previous](validating-with-a-service-layer-cs.md)
[Next](creating-model-classes-with-the-entity-framework-vb.md)</span></span>

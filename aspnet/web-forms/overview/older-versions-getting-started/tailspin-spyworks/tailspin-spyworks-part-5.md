---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
title: 'Část 5: obchodní logika | Microsoft Docs'
author: JoeStagner
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 5 přidává některé obchodní logiky.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: eaef475a-ca91-47ea-a4a7-d074005ed80c
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-5
msc.type: authoredcontent
ms.openlocfilehash: c60eece9223c47304786d7b0d0ca4b11ac0572e9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78630303"
---
# <a name="part-5-business-logic"></a><span data-ttu-id="e3bdf-104">5\. část: Obchodní logika</span><span class="sxs-lookup"><span data-stu-id="e3bdf-104">Part 5: Business Logic</span></span>

<span data-ttu-id="e3bdf-105">[Jana Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="e3bdf-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="e3bdf-106">Tailspin Spyworks ukazuje, jak neobyčejně jednoduché je vytvářet výkonné a škálovatelné aplikace pro platformu .NET.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="e3bdf-107">Ukazuje, jak používat Skvělé nové funkce v ASP.NET 4 k vytvoření online obchodu, včetně nákupu, rezervace a správy.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="e3bdf-108">V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="e3bdf-109">Část 5 přidává některé obchodní logiky.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-109">Part 5 adds some business logic.</span></span>

## <a id="_Toc260221671"></a><span data-ttu-id="e3bdf-110">Přidání některé obchodní logiky</span><span class="sxs-lookup"><span data-stu-id="e3bdf-110">Adding Some Business Logic</span></span>

<span data-ttu-id="e3bdf-111">Chceme, aby naše možnosti nákupu byly dostupné vždycky, když někdo navštíví náš web.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-111">We want our shopping experience to be available whenever someone visits our web site.</span></span> <span data-ttu-id="e3bdf-112">Návštěvníci budou moci procházet a přidávat položky do nákupního košíku i v případě, že nejsou registrováni nebo přihlášeni.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-112">Visitors will be able to browse and add items to the shopping cart even if they are not registered or logged in.</span></span> <span data-ttu-id="e3bdf-113">Až budou připravené k registraci, budou mít možnost ověřit a pokud ještě nejsou členy, budou moci vytvořit účet.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-113">When they are ready to check out they will be given the option to authenticate and if they are not yet members they will be able to create an account.</span></span>

<span data-ttu-id="e3bdf-114">To znamená, že bude nutné implementovat logiku pro převod nákupního košíku z anonymního na stav "registrovaný uživatel".</span><span class="sxs-lookup"><span data-stu-id="e3bdf-114">This means that we will need to implement the logic to convert the shopping cart from an anonymous state to a "Registered User" state.</span></span>

<span data-ttu-id="e3bdf-115">Pojďme vytvořit adresář s názvem "Classes", potom klikněte pravým tlačítkem myši na složku a vytvořte nový soubor "Class" s názvem MyShoppingCart.cs</span><span class="sxs-lookup"><span data-stu-id="e3bdf-115">Let's create a directory named "Classes" then Right-Click on the folder and create a new "Class" file named MyShoppingCart.cs</span></span>

![](tailspin-spyworks-part-5/_static/image1.jpg)

![](tailspin-spyworks-part-5/_static/image1.png)

<span data-ttu-id="e3bdf-116">Jak už jsme uvedli, rozšíříme třídu, která implementuje stránku MyShoppingCart. aspx, a my to provedeme pomocí. ČISTOU výkonnou konstrukci "částečné třídy".</span><span class="sxs-lookup"><span data-stu-id="e3bdf-116">As previously mentioned we will be extending the class that implements the MyShoppingCart.aspx page and we will do this using .NET's powerful "Partial Class" construct.</span></span>

<span data-ttu-id="e3bdf-117">Vygenerované volání pro náš soubor MyShoppingCart.aspx.cf vypadá takto.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-117">The generated call for our MyShoppingCart.aspx.cf file looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample1.cs)]

<span data-ttu-id="e3bdf-118">Všimněte si použití klíčového slova Partial.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-118">Note the use of the "partial" keyword.</span></span>

<span data-ttu-id="e3bdf-119">Soubor třídy, který jsme právě vygenerovali, vypadá takto.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-119">The class file that we just generated looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample2.cs)]

<span data-ttu-id="e3bdf-120">Naše implementace sloučíme přidáním klíčového slova Partial do tohoto souboru.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-120">We will merge our implementations by adding the partial keyword to this file as well.</span></span>

<span data-ttu-id="e3bdf-121">Náš nový soubor třídy teď vypadá takto.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-121">Our new class file now looks like this.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample3.cs)]

<span data-ttu-id="e3bdf-122">První metoda, kterou přidáme do naší třídy, je metoda AddItem.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-122">The first method that we will add to our class is the "AddItem" method.</span></span> <span data-ttu-id="e3bdf-123">Toto je metoda, která bude nakonec volána, když uživatel klikne na odkazy přidat do kresby na stránce seznam produktů a podrobnosti o produktu.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-123">This is the method that will ultimately be called when the user clicks on the "Add to Art" links on the Product List and Product Details pages.</span></span>

<span data-ttu-id="e3bdf-124">V horní části stránky přidejte následující příkazy using.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-124">Append the following to the using statements at the top of the page.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample4.cs)]

<span data-ttu-id="e3bdf-125">A přidejte tuto metodu do třídy MyShoppingCart.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-125">And add this method to the MyShoppingCart class.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample5.cs)]

<span data-ttu-id="e3bdf-126">Používáme LINQ to Entities k zobrazení, zda je položka na košíku již.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-126">We are using LINQ to Entities to see if the item is already in the cart.</span></span> <span data-ttu-id="e3bdf-127">Pokud ano, aktualizujeme množství objednávky položky, jinak vytvoříme novou položku pro vybranou položku.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-127">If so, we update the order quantity of the item, otherwise we create a new entry for the selected item</span></span>

<span data-ttu-id="e3bdf-128">Aby bylo možné zavolat tuto metodu, implementujeme stránku AddToCart. aspx, která nejenom třídí tuto metodu, ale po přidání této položky se pak zobrazí aktuální nákupy a = košík.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-128">In order to call this method we will implement an AddToCart.aspx page that not only class this method but then displayed the current shopping a=cart after the item has been added.</span></span>

<span data-ttu-id="e3bdf-129">V Průzkumníku řešení klikněte pravým tlačítkem myši na název řešení a přidejte a přidejte novou stránku s názvem AddToCart. aspx, jak jsme to udělali dříve.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-129">Right-Click on the solution name in the solution explorer and add and new page named AddToCart.aspx as we have done previously.</span></span>

<span data-ttu-id="e3bdf-130">I když jsme tuto stránku mohli použít k zobrazení dočasných výsledků, jako jsou problémy s nízkými zásobami atd. v naší implementaci se stránka ve skutečnosti nevykresluje, ale místo toho se zavolá do logiky Add a Redirect.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-130">While we could use this page to display interim results like low stock issues, etc, in our implementation, the page will not actually render, but rather call the "Add" logic and redirect.</span></span>

<span data-ttu-id="e3bdf-131">K tomuto účelu přidáme následující kód do události\_načíst stránku.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-131">To accomplish this we'll add the following code to the Page\_Load event.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample6.cs)]

<span data-ttu-id="e3bdf-132">Všimněte si, že produkt načítáme k přidání do nákupního košíku z parametru QueryString a voláním metody AddItem naší třídy.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-132">Note that we are retrieving the product to add to the shopping cart from a QueryString parameter and calling the AddItem method of our class.</span></span>

<span data-ttu-id="e3bdf-133">Za předpokladu, že se nevyskytnou žádné chyby, řízení se předává na stránku SHoppingCart. aspx, kterou budeme plně implementovat.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-133">Assuming no errors are encountered control is passed to the SHoppingCart.aspx page which we will fully implement next.</span></span> <span data-ttu-id="e3bdf-134">Pokud by měla být chyba, vyvolali výjimku.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-134">If there should be an error we throw an exception.</span></span>

<span data-ttu-id="e3bdf-135">V současné době jsme ještě neimplementovali globální obslužnou rutinu chyb, takže by tato výjimka nebyla ošetřená naší aplikací, ale tuto chvíli nasadíme.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-135">Currently we have not yet implemented a global error handler so this exception would go unhandled by our application but we will remedy this shortly.</span></span>

<span data-ttu-id="e3bdf-136">Všimněte si také použití příkazu Debug. selžou () (k dispozici prostřednictvím `using System.Diagnostics;)`</span><span class="sxs-lookup"><span data-stu-id="e3bdf-136">Note also the use of the statement Debug.Fail() (available via `using System.Diagnostics;)`</span></span>

<span data-ttu-id="e3bdf-137">Je aplikace spuštěna v ladicím programu, tato metoda zobrazí podrobný dialog s informacemi o stavu aplikace spolu s chybovou zprávou, kterou zadáte.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-137">Is the application is running inside the debugger, this method will display a detailed dialog with information about the applications state along with the error message that we specify.</span></span>

<span data-ttu-id="e3bdf-138">Při spuštění v produkčním prostředí se příkaz Debug. selžou () ignoruje.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-138">When running in production the Debug.Fail() statement is ignored.</span></span>

<span data-ttu-id="e3bdf-139">Všimněte si, že kód nad voláním metody v názvech tříd nákupního košíku "GetShoppingCartId".</span><span class="sxs-lookup"><span data-stu-id="e3bdf-139">You will note in the code above a call to a method in our shopping cart class names "GetShoppingCartId".</span></span>

<span data-ttu-id="e3bdf-140">Přidejte kód pro implementaci metody následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-140">Add the code to implement the method as follows.</span></span>

<span data-ttu-id="e3bdf-141">Všimněte si, že jsme také přidali tlačítka aktualizace a rezervace a popisek, kde můžeme zobrazit kartu "celkem".</span><span class="sxs-lookup"><span data-stu-id="e3bdf-141">Note that we've also added update and checkout buttons and a label where we can display the cart "total".</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample7.cs)]

<span data-ttu-id="e3bdf-142">Nyní můžeme přidat položky do nákupního košíku, ale neimplementovali jsme logiku pro zobrazení košíku po přidání produktu.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-142">We can now add items to our shopping cart but we have not implemented the logic to display the cart after a product has been added.</span></span>

<span data-ttu-id="e3bdf-143">Proto na stránce MyShoppingCart. aspx přidáte ovládací prvek EntityDataSource a ovládací prvek GridVire následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-143">So, in the MyShoppingCart.aspx page we'll add an EntityDataSource control and a GridVire control as follows.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample8.aspx)]

<span data-ttu-id="e3bdf-144">Zavolejte formulář v návrháři, abyste mohli dvakrát kliknout na tlačítko Aktualizovat košík a generovat obslužnou rutinu události Click, která je zadána v deklaraci v označení.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-144">Call up the form in the designer so that you can double click on the Update Cart button and generate the click event handler that is specified in the declaration in the markup.</span></span>

<span data-ttu-id="e3bdf-145">Podrobnosti budeme implementovat později, ale to nám umožní sestavit a spustit naši aplikaci bez chyb.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-145">We'll implement the details later but doing this will let us build and run our application without errors.</span></span>

<span data-ttu-id="e3bdf-146">Když aplikaci spustíte a přidáte ji do nákupního košíku, zobrazí se tato položka.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-146">When you run the application and add an item to the shopping cart you will see this.</span></span>

![](tailspin-spyworks-part-5/_static/image2.jpg)

<span data-ttu-id="e3bdf-147">Všimněte si, že jsme se odchýlit od výchozího zobrazení mřížky implementací tří vlastních sloupců.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-147">Note that we have deviated from the "default" grid display by implementing three custom columns.</span></span>

<span data-ttu-id="e3bdf-148">První je editovatelné pole "vázané" množství:</span><span class="sxs-lookup"><span data-stu-id="e3bdf-148">The first is an Editable, "Bound" field for the Quantity:</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample9.aspx)]

<span data-ttu-id="e3bdf-149">Další je "počítaný" sloupec, který zobrazuje celkovou položku řádku (náklady za položku, kolikrát se množství má seřadit):</span><span class="sxs-lookup"><span data-stu-id="e3bdf-149">The next is a "calculated" column that displays the line item total (the item cost times the quantity to be ordered):</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample10.aspx)]

<span data-ttu-id="e3bdf-150">Nakonec máme vlastní sloupec, který obsahuje ovládací prvek CheckBox, který bude uživatel používat k označení toho, že by měla být položka z nákupního grafu odebrána.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-150">Lastly we have a custom column that contains a CheckBox control that the user will use to indicate that the item should be removed from the shopping chart.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-5/samples/sample11.aspx)]

![](tailspin-spyworks-part-5/_static/image3.jpg)

<span data-ttu-id="e3bdf-151">Jak vidíte, řádek celková objednávka je prázdný, takže přidáváme logiku pro výpočet celkového počtu objednávek.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-151">As you can see, the Order Total line is empty so let's add some logic to calculate the Order Total.</span></span>

<span data-ttu-id="e3bdf-152">Nejdříve implementujeme metodu gettotal pro naši třídu MyShoppingCart.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-152">We'll first implement a "GetTotal" method to our MyShoppingCart Class.</span></span>

<span data-ttu-id="e3bdf-153">Do souboru MyShoppingCart.cs přidejte následující kód.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-153">In the MyShoppingCart.cs file add the following code.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample12.cs)]

<span data-ttu-id="e3bdf-154">Potom na stránce\_načíst obslužnou rutinu události můžeme zavolat naši metodu gettotal.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-154">Then in the Page\_Load event handler we'll can call our GetTotal method.</span></span> <span data-ttu-id="e3bdf-155">SOUČASNĚ přidáme test, abyste zjistili, jestli je nákupní košík prázdný, a pokud je zobrazený, upravte zobrazení podle potřeby.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-155">At the same time we'll add a test to see if the shopping cart is empty and adjust the display accordingly if it is.</span></span>

<span data-ttu-id="e3bdf-156">Když se teď nákupní košík vyprázdní, získáme toto:</span><span class="sxs-lookup"><span data-stu-id="e3bdf-156">Now if the shopping cart is empty we get this:</span></span>

![](tailspin-spyworks-part-5/_static/image4.jpg)

<span data-ttu-id="e3bdf-157">A pokud ne, uvidíme celkový počet.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-157">And if not, we see our total.</span></span>

![](tailspin-spyworks-part-5/_static/image5.jpg)

<span data-ttu-id="e3bdf-158">Tato stránka ale ještě není dokončená.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-158">However, this page is not yet complete.</span></span>

<span data-ttu-id="e3bdf-159">K přepočítání nákupního košíku budeme potřebovat další logiku odebráním položek označených k odebrání a určením nových hodnot množství, které mohl uživatel v mřížce změnit.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-159">We will need additional logic to recalculate the shopping cart by removing items marked for removal and by determining new quantity values as some may have been changed in the grid by the user.</span></span>

<span data-ttu-id="e3bdf-160">Umožňuje přidat metodu "RemoveItem" do naší třídy nákupního košíku v MyShoppingCart.cs pro zpracování případu, když uživatel označí položku k odebrání.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-160">Lets add a "RemoveItem" method to our shopping cart class in MyShoppingCart.cs to handle the case when a user marks an item for removal.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample13.cs)]

<span data-ttu-id="e3bdf-161">Nyní můžeme pracovat jako způsob, jak zpracovat situaci, když uživatel jednoduše změní kvalitu, která má být seřazena v prvku GridView.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-161">Now let's ad a method to handle the circumstance when a user simply changes the quality to be ordered in the GridView.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample14.cs)]

<span data-ttu-id="e3bdf-162">Se základními funkcemi odebrání a aktualizace můžeme implementovat logiku, která ve skutečnosti aktualizuje nákupní košík v databázi.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-162">With the basic Remove and Update features in place we can implement the logic that actually updates the shopping cart in the database.</span></span> <span data-ttu-id="e3bdf-163">(V MyShoppingCart.cs)</span><span class="sxs-lookup"><span data-stu-id="e3bdf-163">(In MyShoppingCart.cs)</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample15.cs)]

<span data-ttu-id="e3bdf-164">Všimněte si, že tato metoda očekává dva parametry.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-164">You'll note that this method expects two parameters.</span></span> <span data-ttu-id="e3bdf-165">Jednou z nich je ID nákupního košíku a druhý je pole objektů uživatelsky definovaného typu.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-165">One is the shopping cart Id and the other is an array of objects of user defined type.</span></span>

<span data-ttu-id="e3bdf-166">Proto pro minimalizaci závislostí naší logiky o specifických uživatelských rozhraních jsme definovali datovou strukturu, kterou můžeme použít k předání položek nákupního košíku do našeho kódu bez toho, aby byla metoda, která potřebuje přímý přístup k ovládacímu prvku GridView.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-166">So as to minimize the dependency of our logic on user interface specifics, we've defined a data structure that we can use to pass the shopping cart items to our code without our method needing to directly access the GridView control.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample16.cs)]

<span data-ttu-id="e3bdf-167">V našem souboru MyShoppingCart.aspx.cs můžeme použít tuto strukturu v našem tlačítku aktualizace klikněte níže na obslužnou rutinu události.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-167">In our MyShoppingCart.aspx.cs file we can use this structure in our Update Button Click Event handler as follows.</span></span> <span data-ttu-id="e3bdf-168">Všimněte si, že kromě aktualizace košíku aktualizujeme také celkové množství košíku.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-168">Note that in addition to updating the cart we will update the cart total as well.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample17.cs)]

<span data-ttu-id="e3bdf-169">Všimněte si, že konkrétního zájmu tohoto řádku kódu:</span><span class="sxs-lookup"><span data-stu-id="e3bdf-169">Note with particular interest this line of code:</span></span>

[!code-javascript[Main](tailspin-spyworks-part-5/samples/sample18.js)]

<span data-ttu-id="e3bdf-170">GetValues () je speciální pomocná funkce, která bude implementována v MyShoppingCart.aspx.cs následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-170">GetValues() is a special helper function that we will implement in MyShoppingCart.aspx.cs as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-5/samples/sample19.cs)]

<span data-ttu-id="e3bdf-171">To poskytuje čistě způsob, jak získat přístup k hodnotám vázaných prvků v našem ovládacím prvku GridView.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-171">This provides a clean way to access the values of the bound elements in our GridView control.</span></span> <span data-ttu-id="e3bdf-172">Vzhledem k tomu, že je ovládací prvek CheckBox odebrat položku nevázaný, k němu přistupujeme prostřednictvím metody FindControl ().</span><span class="sxs-lookup"><span data-stu-id="e3bdf-172">Since our "Remove Item" CheckBox Control is not bound we'll access it via the FindControl() method.</span></span>

<span data-ttu-id="e3bdf-173">V této fázi vývoje projektu se připravujeme k implementaci procesu registrace.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-173">At this stage in your project's development we are getting ready to implement the checkout process.</span></span>

<span data-ttu-id="e3bdf-174">Než to uděláte, využijte Visual Studio k vygenerování databáze členství a přidání uživatele do úložiště členství.</span><span class="sxs-lookup"><span data-stu-id="e3bdf-174">Before doing so let's use Visual Studio to generate the membership database and add a user to the membership repository.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e3bdf-175">[Předchozí](tailspin-spyworks-part-4.md)
> [Další](tailspin-spyworks-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="e3bdf-175">[Previous](tailspin-spyworks-part-4.md)
[Next](tailspin-spyworks-part-6.md)</span></span>

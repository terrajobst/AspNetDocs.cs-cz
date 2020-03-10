---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
title: '8\. část: finální stránky, zpracování výjimek a závěr | Microsoft Docs'
author: JoeStagner
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 8 přidá stránku kontaktů, o stránku a výjimku...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5aeadf8f-39f3-4f07-a78f-1c310c64fb23
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-8
msc.type: authoredcontent
ms.openlocfilehash: 707dc9d87ae324a7897c971a451e40bc54c96cb3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586882"
---
# <a name="part-8-final-pages-exception-handling-and-conclusion"></a><span data-ttu-id="f52ba-104">8\. část: Závěrečné stránky, zpracování výjimek a závěr</span><span class="sxs-lookup"><span data-stu-id="f52ba-104">Part 8: Final Pages, Exception Handling, and Conclusion</span></span>

<span data-ttu-id="f52ba-105">[Jana Stagner](https://github.com/JoeStagner)</span><span class="sxs-lookup"><span data-stu-id="f52ba-105">by [Joe Stagner](https://github.com/JoeStagner)</span></span>

> <span data-ttu-id="f52ba-106">Tailspin Spyworks ukazuje, jak neobyčejně jednoduché je vytvářet výkonné a škálovatelné aplikace pro platformu .NET.</span><span class="sxs-lookup"><span data-stu-id="f52ba-106">Tailspin Spyworks demonstrates how extraordinarily simple it is to create powerful, scalable applications for the .NET platform.</span></span> <span data-ttu-id="f52ba-107">Ukazuje, jak používat Skvělé nové funkce v ASP.NET 4 k vytvoření online obchodu, včetně nákupu, rezervace a správy.</span><span class="sxs-lookup"><span data-stu-id="f52ba-107">It shows off how to use the great new features in ASP.NET 4 to build an online store, including shopping, checkout, and administration.</span></span>
> 
> <span data-ttu-id="f52ba-108">V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks.</span><span class="sxs-lookup"><span data-stu-id="f52ba-108">This tutorial series details all of the steps taken to build the Tailspin Spyworks sample application.</span></span> <span data-ttu-id="f52ba-109">Část 8 přidá stránku kontaktů, informace o stránce a zpracování výjimek.</span><span class="sxs-lookup"><span data-stu-id="f52ba-109">Part 8 adds a contact page, about page, and exception handling.</span></span> <span data-ttu-id="f52ba-110">Toto je závěr řady.</span><span class="sxs-lookup"><span data-stu-id="f52ba-110">This is the conclusion of the series.</span></span>

## <a id="_Toc260221680"></a><span data-ttu-id="f52ba-111">Stránka kontaktu (posílání e-mailů z ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="f52ba-111">Contact Page (Sending email from ASP.NET)</span></span>

<span data-ttu-id="f52ba-112">Vytvořit novou stránku s názvem ContactUs. aspx</span><span class="sxs-lookup"><span data-stu-id="f52ba-112">Create a new page named ContactUs.aspx</span></span>

<span data-ttu-id="f52ba-113">Pomocí návrháře vytvořte následující formulář, který bere zvláštní poznámku, aby zahrnoval ToolkitScriptManager a ovládací prvek editoru z AjaxControlToolkit.</span><span class="sxs-lookup"><span data-stu-id="f52ba-113">Using the designer, create the following form taking special note to include the ToolkitScriptManager and the Editor control from the AjaxControlToolkit.</span></span> <span data-ttu-id="f52ba-114">.</span><span class="sxs-lookup"><span data-stu-id="f52ba-114">.</span></span>

![](tailspin-spyworks-part-8/_static/image1.jpg)

<span data-ttu-id="f52ba-115">Dvojím kliknutím na tlačítko Odeslat vygenerujete obslužnou rutinu události Click v souboru kódu na pozadí a implementujete metodu, která odešle kontaktní údaje jako e-mail.</span><span class="sxs-lookup"><span data-stu-id="f52ba-115">Double click on the "Submit" button to generate a click event handler in the code behind file and implement a method to send the contact information as an email.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

<span data-ttu-id="f52ba-116">Tento kód vyžaduje, aby soubor Web. config obsahoval položku v konfiguračním oddílu, která určuje server SMTP, který má být použit pro odesílání e-mailů.</span><span class="sxs-lookup"><span data-stu-id="f52ba-116">This code requires that your web.config file contain an entry in the configuration section that specifies the SMTP server to use for sending mail.</span></span>

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a><span data-ttu-id="f52ba-117">O stránce</span><span class="sxs-lookup"><span data-stu-id="f52ba-117">About Page</span></span>

<span data-ttu-id="f52ba-118">Vytvořte stránku s názvem AboutUs. aspx a přidejte libovolný obsah, který chcete.</span><span class="sxs-lookup"><span data-stu-id="f52ba-118">Create a page named AboutUs.aspx and add whatever content you like.</span></span>

## <a id="_Toc260221682"></a><span data-ttu-id="f52ba-119">Globální obslužná rutina výjimky</span><span class="sxs-lookup"><span data-stu-id="f52ba-119">Global Exception Handler</span></span>

<span data-ttu-id="f52ba-120">Nakonec v rámci aplikace jsme vyvolali výjimky a existují nepředvídatelné okolnosti, které studené i neošetřené výjimky způsobují v naší webové aplikaci.</span><span class="sxs-lookup"><span data-stu-id="f52ba-120">Lastly, throughout the application we have thrown exceptions and there are unforeseen circumstances that cold also cause unhandled exceptions in our web application.</span></span>

<span data-ttu-id="f52ba-121">Nikdy nechcete, aby se Neošetřená výjimka zobrazovala návštěvníkovi webu.</span><span class="sxs-lookup"><span data-stu-id="f52ba-121">We never want an unhandled exception to be displayed to a web site visitor.</span></span>

![](tailspin-spyworks-part-8/_static/image2.jpg)

<span data-ttu-id="f52ba-122">Kromě toho, že se neošetřené výjimky ještěrů uživateli může také jednat o problém se zabezpečením.</span><span class="sxs-lookup"><span data-stu-id="f52ba-122">Apart from being a terrible user experience unhandled exceptions can also be a security problem.</span></span>

<span data-ttu-id="f52ba-123">Chcete-li tento problém vyřešit, implementujeme globální obslužnou rutinu výjimky.</span><span class="sxs-lookup"><span data-stu-id="f52ba-123">To solve this problem we will implement a global exception handler.</span></span>

<span data-ttu-id="f52ba-124">Provedete to tak, že otevřete soubor Global. asax a poznamenejte si následující předem generovanou obslužnou rutinu události.</span><span class="sxs-lookup"><span data-stu-id="f52ba-124">To do this, open the Global.asax file and note the following pre-generated event handler.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

<span data-ttu-id="f52ba-125">Přidejte kód pro implementaci\_obslužná rutina chyby aplikace následujícím způsobem.</span><span class="sxs-lookup"><span data-stu-id="f52ba-125">Add code to implement the Application\_Error handler as follows.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

<span data-ttu-id="f52ba-126">Pak přidejte do řešení stránku s názvem Error. aspx a přidejte tento fragment kódu.</span><span class="sxs-lookup"><span data-stu-id="f52ba-126">Then add a page named Error.aspx to the solution and add this markup snippet.</span></span>

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

<span data-ttu-id="f52ba-127">Nyní na stránce obslužná rutina události\_načtení extrahuje chybové zprávy z objektu Request.</span><span class="sxs-lookup"><span data-stu-id="f52ba-127">Now in the Page\_Load event handler extract the error messages from the Request Object.</span></span>

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a><span data-ttu-id="f52ba-128">Závěr</span><span class="sxs-lookup"><span data-stu-id="f52ba-128">Conclusion</span></span>

<span data-ttu-id="f52ba-129">Zjistili jsme, že ASP.NET WebForms usnadňuje vytváření sofistikovaných webů s přístupem k databázi, členstvím, AJAX atd.</span><span class="sxs-lookup"><span data-stu-id="f52ba-129">We've seen that ASP.NET WebForms makes it easy to create a sophisticated website with database access, membership, AJAX, etc.</span></span> <span data-ttu-id="f52ba-130">poměrně rychle.</span><span class="sxs-lookup"><span data-stu-id="f52ba-130">pretty quickly.</span></span>

<span data-ttu-id="f52ba-131">Snad v tomto kurzu jste získali nástroje, které potřebujete k zahájení vytváření vlastních aplikací ASP.NET WebForms.</span><span class="sxs-lookup"><span data-stu-id="f52ba-131">Hopefully this tutorial has given you the tools you need to get started building your own ASP.NET WebForms applications!</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f52ba-132">Předchozí</span><span class="sxs-lookup"><span data-stu-id="f52ba-132">Previous</span></span>](tailspin-spyworks-part-7.md)

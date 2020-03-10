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
# <a name="part-8-final-pages-exception-handling-and-conclusion"></a>8\. část: Závěrečné stránky, zpracování výjimek a závěr

[Jana Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks ukazuje, jak neobyčejně jednoduché je vytvářet výkonné a škálovatelné aplikace pro platformu .NET. Ukazuje, jak používat Skvělé nové funkce v ASP.NET 4 k vytvoření online obchodu, včetně nákupu, rezervace a správy.
> 
> V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 8 přidá stránku kontaktů, informace o stránce a zpracování výjimek. Toto je závěr řady.

## <a id="_Toc260221680"></a>Stránka kontaktu (posílání e-mailů z ASP.NET)

Vytvořit novou stránku s názvem ContactUs. aspx

Pomocí návrháře vytvořte následující formulář, který bere zvláštní poznámku, aby zahrnoval ToolkitScriptManager a ovládací prvek editoru z AjaxControlToolkit. .

![](tailspin-spyworks-part-8/_static/image1.jpg)

Dvojím kliknutím na tlačítko Odeslat vygenerujete obslužnou rutinu události Click v souboru kódu na pozadí a implementujete metodu, která odešle kontaktní údaje jako e-mail.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample1.cs)]

Tento kód vyžaduje, aby soubor Web. config obsahoval položku v konfiguračním oddílu, která určuje server SMTP, který má být použit pro odesílání e-mailů.

[!code-xml[Main](tailspin-spyworks-part-8/samples/sample2.xml)]

## <a id="_Toc260221681"></a>O stránce

Vytvořte stránku s názvem AboutUs. aspx a přidejte libovolný obsah, který chcete.

## <a id="_Toc260221682"></a>Globální obslužná rutina výjimky

Nakonec v rámci aplikace jsme vyvolali výjimky a existují nepředvídatelné okolnosti, které studené i neošetřené výjimky způsobují v naší webové aplikaci.

Nikdy nechcete, aby se Neošetřená výjimka zobrazovala návštěvníkovi webu.

![](tailspin-spyworks-part-8/_static/image2.jpg)

Kromě toho, že se neošetřené výjimky ještěrů uživateli může také jednat o problém se zabezpečením.

Chcete-li tento problém vyřešit, implementujeme globální obslužnou rutinu výjimky.

Provedete to tak, že otevřete soubor Global. asax a poznamenejte si následující předem generovanou obslužnou rutinu události.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample3.cs)]

Přidejte kód pro implementaci\_obslužná rutina chyby aplikace následujícím způsobem.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample4.cs)]

Pak přidejte do řešení stránku s názvem Error. aspx a přidejte tento fragment kódu.

[!code-aspx[Main](tailspin-spyworks-part-8/samples/sample5.aspx)]

Nyní na stránce obslužná rutina události\_načtení extrahuje chybové zprávy z objektu Request.

[!code-csharp[Main](tailspin-spyworks-part-8/samples/sample6.cs)]

## <a id="_Toc260221683"></a>Závěr

Zjistili jsme, že ASP.NET WebForms usnadňuje vytváření sofistikovaných webů s přístupem k databázi, členstvím, AJAX atd. poměrně rychle.

Snad v tomto kurzu jste získali nástroje, které potřebujete k zahájení vytváření vlastních aplikací ASP.NET WebForms.

> [!div class="step-by-step"]
> [Předchozí](tailspin-spyworks-part-7.md)

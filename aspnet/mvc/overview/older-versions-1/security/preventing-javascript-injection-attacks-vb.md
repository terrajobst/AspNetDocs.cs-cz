---
uid: mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
title: Zabránění útokům prostřednictvím injektáže JavaScriptu (VB) | Microsoft Docs
author: StephenWalther
description: Zabraňte útokům prostřednictvím injektáže JavaScriptu a útokům na skriptování mezi weby. V tomto kurzu Stephen Walther vysvětluje, jak můžete snadno de...
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 9274a72e-34dd-4dae-8452-ed733ae71377
msc.legacyurl: /mvc/overview/older-versions-1/security/preventing-javascript-injection-attacks-vb
msc.type: authoredcontent
ms.openlocfilehash: dfe09085f26c62c566649bc6f570aa25367a0f07
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74594736"
---
# <a name="preventing-javascript-injection-attacks-vb"></a>Prevence útoků založených na injektáži JavaScriptu (VB)

od [Stephen Walther](https://github.com/StephenWalther)

[Stáhnout PDF](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_06_VB.pdf)

> Zabraňte útokům prostřednictvím injektáže JavaScriptu a útokům na skriptování mezi weby. V tomto kurzu Stephen Walther vysvětluje, jak můžete tyto typy útoků snadno přesazovat pomocí kódování HTML vašeho obsahu.

Cílem tohoto kurzu je vysvětlit, jak můžete zabránit útokům prostřednictvím injektáže JavaScriptu v aplikacích ASP.NET MVC. Tento kurz popisuje dva přístupy k obraně webu proti útoku prostřednictvím injektáže JavaScriptu. Naučíte se, jak zabránit útokům prostřednictvím injektáže JavaScriptu pomocí kódování zobrazených dat. Naučíte se také, jak zabránit útokům prostřednictvím injektáže JavaScriptu při kódování dat, která přijímáte.

## <a name="what-is-a-javascript-injection-attack"></a>Co je útok injektáže JavaScriptu?

Pokaždé, když přijmete vstup uživatele a znovu zobrazíte uživatelský vstup, otevřete web pro útoky prostřednictvím injektáže JavaScriptu. Pojďme se podívat na konkrétní aplikaci, která je otevřená pro útoky prostřednictvím injektáže JavaScriptu.

Představte si, že jste vytvořili web zpětné vazby od zákazníka (viz obrázek 1). Zákazníci si můžou web navštívit a zadat svůj názor na své zkušenosti s používáním vašich produktů. Když zákazník odešle zpětnou vazbu, zpětná vazba se znovu zobrazí na stránce zpětná vazba.

[![web Feedback pro zákazníky](preventing-javascript-injection-attacks-vb/_static/image2.png)](preventing-javascript-injection-attacks-vb/_static/image1.png)

**Obrázek 01**: web zpětné vazby od zákazníků ([kliknutím zobrazíte obrázek v plné velikosti](preventing-javascript-injection-attacks-vb/_static/image3.png))

Web zpětné vazby od zákazníka používá `controller` v seznamu 1. Tato `controller` obsahuje dvě akce s názvem `Index()` a `Create()`.

**Výpis 1 – `HomeController.vb`**

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample1.vb)]

Metoda `Index()` zobrazí `Index` zobrazení. Tato metoda předá všechna předchozí zpětnou vazbu od zákazníků k zobrazení `Index` načtením zpětné vazby z databáze (pomocí dotazu LINQ to SQL).

Metoda `Create()` vytvoří novou položku zpětné vazby a přidá ji do databáze. Zpráva, kterou zákazník zadá do formuláře, je předána metodě `Create()` v parametru zprávy. Vytvoří se položka zpětné vazby a tato zpráva se přiřadí vlastnosti `Message` položky zpětné vazby. Položka zpětné vazby je odeslána do databáze pomocí volání metody `DataContext.SubmitChanges()`. Nakonec se návštěvník přesměruje zpátky na `Index` zobrazení, kde se zobrazuje veškerá zpětná vazba.

Zobrazení `Index` je obsaženo v seznamu 2.

**Výpis 2 – `Index.aspx`**

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample2.aspx)]

Zobrazení `Index` obsahuje dva oddíly. Horní část obsahuje vlastní formulář zpětné vazby zákazníků. Dolní část obsahuje pro.. Každé smyčka, která prochází všemi předchozími položkami zpětné vazby od zákazníků a zobrazuje vlastnosti EntryDate a Message pro každou položku zpětné vazby.

Web zpětné vazby od zákazníka je jednoduchý Web. Web je bohužel otevřený pro útoky prostřednictvím injektáže JavaScriptu.

Představte si, že do formuláře zpětné vazby zákazníka zadáte následující text:

[!code-html[Main](preventing-javascript-injection-attacks-vb/samples/sample3.html)]

Tento text představuje skript JavaScriptu, který zobrazí okno upozorňující na zprávu. Jakmile někdo tento skript odešle do formuláře zpětné vazby, zpráva <em>Boo!</em> zobrazí se vždy, když kdokoli navštíví web zpětné vazby od zákazníka v budoucnosti (viz obrázek 2).

[![vkládání JavaScriptu](preventing-javascript-injection-attacks-vb/_static/image5.png)](preventing-javascript-injection-attacks-vb/_static/image4.png)

**Obrázek 02**: vkládání JavaScriptu ([kliknutím zobrazíte obrázek v plné velikosti](preventing-javascript-injection-attacks-vb/_static/image6.png))

Nyní může být vaše počáteční odpověď na útoky prostřednictvím injektáže JavaScriptu apathy. Možná si myslíte, že útoky prostřednictvím injektáže JavaScriptu jsou jednoduše typu útoku na odstranění *obličeje* . Možná si myslíte, že nikdo nemůže dělat cokoli, co Evil, tím, že potvrdil útok prostřednictvím injektáže JavaScriptu.

Hacker ale může provádět nějaké skutečně evilé věci vložením JavaScriptu do webu. Můžete použít útok prostřednictvím injektáže JavaScriptu k provádění útoku skriptování mezi weby (XSS). Při útoku na skriptování mezi weby ukrástte důvěrné informace o uživateli a odešlete informace na jiný web.

Hacker může například pomocí útoku na vložení JavaScriptu ukrást hodnoty souborů cookie prohlížeče od jiných uživatelů. Pokud se citlivé informace, jako jsou hesla, čísla kreditních karet nebo čísla sociálního pojištění, ukládají do souborů cookie prohlížeče, pak hacker může k odcizení těchto informací použít útok prostřednictvím injektáže JavaScriptu. Nebo, pokud uživatel zadá citlivé informace v poli formuláře obsaženém na stránce, která byla ohrožena útokem prostřednictvím JavaScriptu, může počítačový podvodník použít vložený JavaScript k přemístění dat formuláře a odeslat ho na jiný web.

*Děsili se prosím*. Využijte útoky prostřednictvím injektáže JavaScriptu a ochraňte důvěrné informace uživatele. V následujících dvou částech probereme dvě techniky, pomocí kterých můžete chránit aplikace ASP.NET MVC před útoky prostřednictvím injektáže JavaScriptu.

## <a name="approach-1-html-encode-in-the-view"></a>Přístup #1: kódování HTML v zobrazení

Jedním z jednoduchých způsobů, jak zabránit útokům prostřednictvím injektáže JavaScriptu, je kódování HTML, které zakóduje data zadaná uživateli webu při zobrazení dat v zobrazení. Tento postup obsahuje aktualizované zobrazení `Index` v seznamu 3.

**Výpis 3 – `Index.aspx` (kódovaný v HTML)**

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample4.aspx)]

Všimněte si, že hodnota `feedback.Message` je kódována HTML před zobrazením hodnoty s následujícím kódem:

[!code-aspx[Main](preventing-javascript-injection-attacks-vb/samples/sample5.aspx)]

Co to znamená pro kódování řetězce ve formátu HTML? Při kódování řetězce ve formátu HTML jsou nebezpečné znaky, jako například `<` a `>` nahrazeny odkazy na entity HTML, jako je například `&lt;` a `&gt;`. Takže pokud je řetězec `<script>alert("Boo!")</script>` kódovaný v jazyce HTML, bude převeden na `&lt;script&gt;alert(&quot;Boo!&quot;)&lt;/script&gt;`. Kódovaný řetězec již není spouštěn jako JavaScriptový skript, který je interpretován prohlížečem. Místo toho se stránka s neškodou zobrazí na obrázku 3.

[![napadený JavaScriptový útok](preventing-javascript-injection-attacks-vb/_static/image8.png)](preventing-javascript-injection-attacks-vb/_static/image7.png)

**Obrázek 03**: napadený JavaScriptový útok ([kliknutím zobrazíte obrázek v plné velikosti](preventing-javascript-injection-attacks-vb/_static/image9.png))

Všimněte si, že v zobrazení `Index` v seznamu 3 je zakódována pouze hodnota `feedback.Message`. Hodnota `feedback.EntryDate` není kódovaná. Stačí pouze kódovat data zadaná uživatelem. Vzhledem k tomu, že hodnota EntryDate byla v kontroleru vygenerována, nemusíte tuto hodnotu kódovat HTML.

## <a name="approach-2-html-encode-in-the-controller"></a>Přístup #2: kódování HTML v kontroleru

Namísto dat kódování HTML při zobrazení dat v zobrazení můžete data kódovat přímo před odesláním dat do databáze. Tento druhý přístup se vezme v případě `controller` v seznamu 4.

**Výpis 4 – `HomeController.cs` (kódovaný v HTML)**

[!code-vb[Main](preventing-javascript-injection-attacks-vb/samples/sample6.vb)]

Všimněte si, že hodnota zprávy je kódována HTML před odesláním hodnoty do databáze v rámci akce `Create()`. Když je zpráva v zobrazení znovu zobrazená, zpráva je zakódovaná HTML a veškerý JavaScript vložený ve zprávě se neprovede.

Obvykle byste měli upřednostňovat první přístup popsaný v tomto kurzu přes tento druhý přístup. Problém s tímto druhým přístupem je, že ve vaší databázi skončí data kódovaná pomocí HTML. Jinými slovy, data databáze jsou změněných s Funny znaky.

Proč je to chybné? Pokud někdy potřebujete zobrazit databázová data v jiné než webové stránce, budete mít problémy. Například již nelze snadno zobrazit data v aplikaci model Windows Forms.

## <a name="summary"></a>Přehled

Účelem tohoto kurzu bylo scarei potenciálního útoku na injektáže JavaScriptu. Tento kurz popisuje dva způsoby, jak chránit vaše aplikace ASP.NET MVC proti útokům prostřednictvím injektáže JavaScriptu: buď můžete HTML zakódovat data odeslaná v zobrazení, nebo můžete HTML kódovat data odeslaná uživatelem v řadiči.

> [!div class="step-by-step"]
> [Předchozí](authenticating-users-with-windows-authentication-vb.md)

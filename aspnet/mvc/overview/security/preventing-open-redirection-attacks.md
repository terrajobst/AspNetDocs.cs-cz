---
uid: mvc/overview/security/preventing-open-redirection-attacks
title: Zabránění útokům na otevřenéC#přesměrování () | Microsoft Docs
author: jongalloway
description: V tomto kurzu se dozvíte, jak můžete zabránit útokům na otevřené přesměrování v aplikacích ASP.NET MVC. Tento kurz se zabývá provedenými změnami...
ms.author: riande
ms.date: 02/27/2014
ms.assetid: 69fb02e0-f5b7-4c35-878c-fa87164fc785
msc.legacyurl: /mvc/overview/security/preventing-open-redirection-attacks
msc.type: authoredcontent
ms.openlocfilehash: cfa635d4fd14d031993c5b452325cbe334f82dc2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538169"
---
# <a name="preventing-open-redirection-attacks-c"></a>Prevence útoků založených na otevřeném přesměrování (C#)

o [Jan Galloway](https://github.com/jongalloway)

> V tomto kurzu se dozvíte, jak můžete zabránit útokům na otevřené přesměrování v aplikacích ASP.NET MVC. Tento kurz popisuje změny provedené v AccountController v ASP.NET MVC 3 a ukazuje, jak můžete tyto změny použít ve stávajících aplikacích ASP.NET MVC 1,0 a 2.

## <a name="what-is-an-open-redirection-attack"></a>Co je otevřený útok na přesměrování?

Každá webová aplikace, která přesměrovává na adresu URL zadanou prostřednictvím žádosti, jako je například dotaz nebo data formuláře, může být úmyslně poškozena a přesměruje uživatele na externí, škodlivou adresu URL. Tato manipulace se nazývá útok typu otevřené přesměrování.

Vždy, když vaše logika aplikace přesměrovává na zadanou adresu URL, je nutné ověřit, že adresa URL pro přesměrování nebyla úmyslně poškozena. Přihlášení, které se používá ve výchozím AccountController pro ASP.NET MVC 1,0 a ASP.NET MVC 2, je zranitelné kvůli útokům na otevřené přesměrování. Naštěstí je snadné aktualizovat existující aplikace, aby používaly opravy z ASP.NET MVC 3 Preview.

Abychom porozuměli ohrožení zabezpečení, Podívejme se na to, jak přesměrování přihlášení funguje ve výchozím projektu webové aplikace ASP.NET MVC 2. V této aplikaci se pokusit o návštěvu akce kontroleru, která má atribut [autorizační], přesměruje neautorizované uživatele na zobrazení/Account/LogOn. Toto přesměrování na/Account/LogOn bude obsahovat parametr returnUrl QueryString, aby se uživatel mohl vrátit na původně požadovanou adresu URL po úspěšném přihlášení.

Na následujícím snímku obrazovky vidíte, že při pokusu o přístup k zobrazení/Account/ChangePassword, když není přihlášen, se v důsledku přesměrování na/Account/LogOn? ReturnUrl =% 2fAccount% 2fChangePassword% 2f.

[![](preventing-open-redirection-attacks/_static/image2.png)](preventing-open-redirection-attacks/_static/image1.png)

**Obrázek 01**: přihlašovací stránka s otevřeným přesměrováním

Vzhledem k tomu, že parametr ReturnUrl QueryString není ověřený, útočník ho může upravit a vložit do parametru adresu URL, aby mohl spustit útok typu otevřené přesměrování. Abychom to ukázali, můžeme parametr ReturnUrl změnit na [http://bing.com](http://bing.com), takže výsledná přihlašovací adresa URL bude/Account/LogOn? ReturnUrl =<http://www.bing.com/>. Po úspěšném přihlášení k lokalitě budeme přesměrováni na [http://bing.com](http://bing.com). Vzhledem k tomu, že toto přesměrování není ověřeno, může místo toho odkazovat na škodlivý web, který se pokusí uživatele přimět.

### <a name="a-more-complex-open-redirection-attack"></a>Složitější útok na otevřené přesměrování

Útoky na otevřené přesměrování jsou obzvláště nebezpečné, protože útočník ví, že se snažíme přihlásit ke konkrétnímu webu, což nám způsobuje hrozbu [útoku phishing](https://www.microsoft.com/protect/fraud/phishing/symptoms.aspx). Útočník by například mohl odeslat škodlivé e-maily uživatelům webu při pokusu o zaznamenání hesla. Pojďme se podívat, jak to bude fungovat na webu NerdDinner. (Upozorňujeme, že Live NerdDinner web byl aktualizován tak, aby chránil proti útokům s otevřeným přesměrováním.)

Nejdřív útočník pošle odkaz na přihlašovací stránku na NerdDinner, která obsahuje přesměrování na jejich falešný stránku:

[http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn](http://nerddinner.com/Account/LogOn?returnUrl=http://nerddiner.com/Account/LogOn)

Všimněte si, že návratová adresa URL odkazuje na nerddiner.com, ve kterém chybí "n" ze slova večeře. V tomto příkladu je to doména, kterou útočník ovládá. Po přístupu k výše uvedenému odkazu se dostanete na legitimní přihlašovací stránku NerdDinner.com.

[![](preventing-open-redirection-attacks/_static/image4.png)](preventing-open-redirection-attacks/_static/image3.png)

**Obrázek 02**: přihlašovací stránka NerdDinner s otevřeným přesměrováním

Když se správně přihlásíme, akce přihlášení ASP.NET MVC AccountController přesměruje na adresu URL zadanou v parametru returnUrl QueryString. V tomto případě je to adresa URL, kterou útočník zadal, což je [http://nerddiner.com/Account/LogOn](http://nerddiner.com/Account/LogOn). Pokud se nejedná o extrémně sledované, je velmi pravděpodobný, ale nemůžeme si to všimnout, zejména proto, že útočník má pozor, abyste se ujistili, že jeho neoprávněná stránka vypadá přesně stejně jako stránka legitimního přihlášení. Tato přihlašovací stránka obsahuje chybovou zprávu s požadavkem na opětovné přihlášení. Clumsy nás, musíme nezadat heslo.

[![](preventing-open-redirection-attacks/_static/image6.png)](preventing-open-redirection-attacks/_static/image5.png)

**Obrázek 03**: obrazovka přihlašovacího jména k Padělánému NerdDinner

Když znovu zadáte naše uživatelské jméno a heslo, přihlašovací stránka uloží tyto informace a pošle nám k legitimnímu webu NerdDinner.com. V tuto chvíli web NerdDinner.com již ověřil vaše jméno, takže přihlašovací stránka může přesměrovat přímo na tuto stránku. Konečným výsledkem je, že útočník má naše uživatelské jméno a heslo, ale nejsme si vědomi, že k nim jsme dostali.

## <a name="looking-at-the-vulnerable-code-in-the-accountcontroller-logon-action"></a>Podívejte se na ohrožený kód v akci přihlášení k AccountController

Kód pro akci přihlášení v aplikaci ASP.NET MVC 2 je uveden níže. Všimněte si, že po úspěšném přihlášení kontroler vrátí přesměrování na returnUrl. Můžete vidět, že se neprovádí žádné ověřování proti parametru returnUrl.

**Výpis 1 – akce přihlášení k ASP.NET MVC 2 v `AccountController.cs`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample1.cs)]

Teď se podíváme na změny akce přihlášení ASP.NET MVC 3. Tento kód byl změněn tak, aby ověřil parametr returnUrl voláním nové metody v pomocné třídě System. Web. Mvc. URL s názvem `IsLocalUrl()`.

**Výpis 2 – akce přihlášení ASP.NET MVC 3 v `AccountController.cs`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample2.cs)]

Tato změna se změnila tak, aby se ověřil parametr návratové adresy URL voláním nové metody v pomocné třídě System. Web. Mvc. URL, `IsLocalUrl()`.

## <a name="protecting-your-aspnet-mvc-10-and-mvc-2-applications"></a>Ochrana aplikací ASP.NET MVC 1,0 a MVC 2

Můžete využít změny ASP.NET MVC 3 v našich stávajících aplikacích ASP.NET MVC 1,0 a 2 tak, že přidáte pomocnou metodu IsLocalUrl () a aktualizujete akci přihlášení a ověříte parametr returnUrl.

Metoda UrlHelper IsLocalUrl () ve skutečnosti stačí pouze volat do metody v System. Web. webpages, protože toto ověřování je také používáno aplikacemi ASP.NET Web Pages.

**Výpis 3 – metoda IsLocalUrl () z ASP.NET MVC 3 UrlHelper `class`**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample3.cs)]

Metoda IsUrlLocalToHost obsahuje skutečnou logiku ověřování, jak je uvedeno v seznamu 4.

**Výpis 4 – IsUrlLocalToHost () metody z třídy System. Web. webpages RequestExtensions**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample4.cs)]

V naší aplikaci ASP.NET MVC 1,0 nebo 2 přidáme do AccountController metodu IsLocalUrl (), ale doporučujeme ji přidat do samostatné pomocné třídy, pokud je to možné. Provedeme dvě malé změny ve verzi ASP.NET MVC 3 IsLocalUrl () tak, aby fungovaly v rámci AccountController. Nejprve ho z veřejné metody změní na soukromou metodu, protože veřejné metody v řadičích jsou přístupné jako akce kontroleru. Za druhé změníme hovor, který zkontroluje hostitele adresy URL s hostitelem aplikace. Toto volání dělá použití místního pole Třída requestContext ve třídě UrlHelper. Místo použití tohoto. Třída requestContext. HttpContext. Request. URL. Host, použijeme to. Request. URL. Host. Následující kód ukazuje upravenou metodu IsLocalUrl () pro použití s třídou Controller v aplikacích ASP.NET MVC 1,0 a 2.

**Výpis 5 – IsLocalUrl () metody, která je upravena pro použití s třídou kontroleru MVC**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample5.cs)]

Teď, když je na místě metoda IsLocalUrl (), můžeme ji zavolat z naší akce přihlášení k ověření parametru returnUrl, jak je znázorněno v následujícím kódu.

**Výpis 6 – aktualizovaná metoda přihlašování, která ověřuje parametr returnUrl**

[!code-csharp[Main](preventing-open-redirection-attacks/samples/sample6.cs)]

Nyní můžeme otestovat útok na otevřené přesměrování tím, že se pokusíte přihlásit pomocí externí návratové adresy URL. Pojďme použít/Account/LogOn? ReturnUrl = znovu<http://www.bing.com/>.

[![](preventing-open-redirection-attacks/_static/image8.png)](preventing-open-redirection-attacks/_static/image7.png)

**Obrázek 04**: testování aktualizované akce přihlášení

Po úspěšném přihlášení se přesměruje na akci řadiče pro Home/index, nikoli na externí adresu URL.

[![](preventing-open-redirection-attacks/_static/image10.png)](preventing-open-redirection-attacks/_static/image9.png)

**Obrázek 05**: útok otevřeného přesměrování byl nepřipraven

## <a name="summary"></a>Souhrn

V případě, že jsou adresy URL přesměrování předány jako parametry v adrese URL aplikace, může dojít k útokům na otevřené přesměrování. Šablona ASP.NET MVC 3 obsahuje kód pro ochranu před útoky na otevřené přesměrování. Tento kód můžete přidat s určitou úpravou pro ASP.NET MVC 1,0 a 2 aplikace. Pokud chcete chránit před útoky typu Open, pokud se přihlašujete do aplikací ASP.NET 1,0 a 2, přidejte metodu IsLocalUrl () a v akci přihlášení ověřte parametr returnUrl.

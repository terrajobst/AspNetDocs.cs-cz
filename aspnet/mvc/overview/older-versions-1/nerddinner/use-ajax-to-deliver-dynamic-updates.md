---
uid: mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
title: Použití jazyka AJAX k doručování dynamických aktualizací | Microsoft Docs
author: microsoft
description: Krok 10 implementuje podporu pro přihlášené uživatele, aby ODPOVĚDĚLi na svůj zájem o účast na večeři s využitím přístupu založeného na AJAX, který je integrovaný v podrobnostech na večeři...
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 18700815-8e6c-4489-91af-7ea9dab6529e
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-ajax-to-deliver-dynamic-updates
msc.type: authoredcontent
ms.openlocfilehash: 3edc02fec546609505b5e085440fa684abe7acd0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600847"
---
# <a name="use-ajax-to-deliver-dynamic-updates"></a>Použití jazyka AJAX k dynamickým aktualizacím

od [Microsoftu](https://github.com/microsoft)

[Stáhnout PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> Toto je krok 10 bezplatného [kurzu aplikace "NerdDinner"](introducing-the-nerddinner-tutorial.md) , který vás provede procesem vytvoření malé, ale dokončené webové aplikace pomocí ASP.NET MVC 1.
> 
> Krok 10 implementuje podporu pro přihlášené uživatele, aby ODPOVĚDĚLi na svůj zájem o účast na večeři s využitím přístupu založeného na AJAX, který je integrovaný na stránce s podrobnostmi o večeři.
> 
> Pokud používáte ASP.NET MVC 3, doporučujeme vám postupovat podle [Začínáme s kurzy pro](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) [hudební úložiště](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) MVC 3 nebo MVC.

## <a name="nerddinner-step-10-ajax-enabling-rsvps-accepts"></a>NerdDinner krok 10: AJAX povolující protokoly RSVP

Pojďme teď pro přihlášené uživatele implementovat podporu, která zaznamená svůj zájem o účast na večeři. Povolíme to s využitím přístupu založeného na AJAX, který je integrovaný na stránce s podrobnostmi o večeři.

### <a name="indicating-whether-the-user-is-rsvpd"></a>Označuje, zda uživatel používá protokol RSVP.

Uživatelé můžou navštívit adresu URL */Dinners/Details/[ID*] a zobrazit podrobnosti o konkrétní večeři:

![](use-ajax-to-deliver-dynamic-updates/_static/image1.png)

Metoda akce Details () je implementována takto:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample1.cs)]

Náš první krok pro implementaci podpory protokolu RSVP bude přidat pomocnou metodu "IsUserRegistered (uživatelské jméno)" do našeho objektu večeře (v rámci předchozí třídy Dinner.cs, kterou jsme vytvořili dříve). Tato pomocná metoda vrátí hodnotu true nebo false v závislosti na tom, zda uživatel aktuálně hlásí odpověď pro večeři:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample2.cs)]

Potom můžeme do naší šablony zobrazení Details. aspx přidat následující kód, který zobrazí příslušnou zprávu s oznámením, že je uživatel zaregistrován nebo není pro událost:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample3.html)]

A teď když uživatel navštíví večeři, na který se zaregistruje, zobrazí se tato zpráva:

![](use-ajax-to-deliver-dynamic-updates/_static/image2.png)

A když navštívíte večeři, že nejsou zaregistrovaní, uvidí následující zprávu:

![](use-ajax-to-deliver-dynamic-updates/_static/image3.png)

### <a name="implementing-the-register-action-method"></a>Implementace metody akce registru

Pojďme teď přidat funkce potřebné k tomu, aby uživatelé mohli na stránce s podrobnostmi povolit zasílání zpráv na večeři.

Pokud to chcete provést, vytvoříme novou třídu "RSVPController" tak, že kliknete pravým tlačítkem na adresář \Controllers a kliknete na příkaz nabídky přidat&gt;Controller.

Implementujeme metodu "Register" v rámci nové třídy RSVPController, která jako argument převezme ID pro večeři, načte příslušný objekt večeře, zkontroluje, jestli je přihlášený uživatel aktuálně v seznamu uživatelů, kteří si ho zaregistrovali, a pokud nepřidá objekt RSVP pro ně:

[!code-csharp[Main](use-ajax-to-deliver-dynamic-updates/samples/sample4.cs)]

Všimněte si, jak vracíme jednoduchý řetězec jako výstup metody Action. Tuto zprávu jsme mohli vložit do šablony zobrazení – ale vzhledem k tomu, že je to malé, budeme jenom používat pomocnou metodu Content () pro základní třídu kontroleru a vrátíte zprávu s řetězcem, jako je výše.

### <a name="calling-the-rsvpforevent-action-method-using-ajax"></a>Volání metody akce RSVPForEvent pomocí jazyka AJAX

Použijeme AJAX k vyvolání metody akce registrace z našeho zobrazení podrobností. Implementace je poměrně jednoduchá. Nejprve přidáme dva odkazy knihovny skriptu:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample5.html)]

První knihovna odkazuje na základní knihovnu skriptů ASP.NET AJAX na straně klienta. Tento soubor má přibližně 24k velikost (komprimovaná) a obsahuje základní funkce AJAX na straně klienta. Druhá knihovna obsahuje funkce nástrojů, které se integrují s vestavěnými podpůrnými metodami AJAX v ASP.NET MVC (které budeme brzy používat).

Pak můžeme aktualizovat kód šablony zobrazení, který jsme přidali dříve, takže místo výstupu "Nejste pro tuto událost zaregistrováni", ale vygenerujeme odkaz, který po vložení vyvolá volání AJAX, které vyvolá naši metodu RSVPForEvent akce na našem řadiči protokolu RSVP. a zaprotokoluje uživatele:

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample6.aspx)]

Použitá pomocná metoda AJAX. ActionLink () je vestavěná do ASP.NET MVC a je podobná jako pomocná metoda HTML. ActionLink () s tím rozdílem, že místo provedení standardní navigace vytvoří odkaz AJAX na metodu Action při kliknutí na odkaz. Nad tím voláme metodu akce Register v řadiči "RSVP" a předáte DinnerID jako parametr "ID". Konečný parametr AjaxOptions, který předáváme, znamená, že chceme převzít obsah vrácený z metody Action a aktualizovat element HTML &lt;div&gt; na stránce, jejíž ID je "rsvpmsg".

A teď když uživatel přejde na večeři, ke kterému ještě nejsou zaregistrované, uvidí pro něj odkaz na protokol RSVP:

![](use-ajax-to-deliver-dynamic-updates/_static/image4.png)

Pokud kliknete na odkaz "protokol RSVP pro tuto událost", provedou volání metody Register na řadiči protokolu RSVP volání AJAX a když se dokončí, zobrazí se aktualizovaná zpráva podobná následující:

![](use-ajax-to-deliver-dynamic-updates/_static/image5.png)

Šířka pásma sítě a provoz v rámci tohoto volání AJAX jsou skutečně odlehčené. Když uživatel klikne na odkaz protokol RSVP pro tuto událost, pošle se malý požadavek na síť HTTP POST na adresu URL */Dinners/Register/1* , která vypadá takto:

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample7.cmd)]

A odpověď z naší metody akce registrace je jednoduše:

[!code-console[Main](use-ajax-to-deliver-dynamic-updates/samples/sample8.cmd)]

Toto zjednodušené volání je rychlé a bude fungovat i přes pomalou síť.

### <a name="adding-a-jquery-animation"></a>Přidání animace jQuery

Funkce AJAX, které jsme implementovali, funguje dobře a rychle. Někdy k tomu může dojít, když si uživatel nemusí všimnout, že odkaz na protokol RSVP byl nahrazen novým textem. Pokud chcete, aby byl výsledek trochu jasnější, můžeme přidat jednoduchou animaci, která upozorní na zprávu aktualizace.

Výchozí šablona projektu ASP.NET MVC zahrnuje jQuery – vynikající (a velmi oblíbenou) knihovnu JavaScript open source, která je také podporována společností Microsoft. jQuery poskytuje řadu funkcí, včetně skvělé knihovny pro výběr a efekty HTML modelu HTML.

Pokud chcete použít jQuery, nejdřív na něj přidáte odkaz na skript. Vzhledem k tomu, že budeme používat jQuery v rámci celé řady míst v rámci našeho webu, přidáme odkaz na skript do souboru hlavní stránky site. Master, aby ho všechny stránky mohli používat.

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample9.html)]

*Tip: Ujistěte se, že máte nainstalovanou opravu hotfix technologie JavaScript IntelliSense pro VS 2008 SP1, která umožňuje bohatší podporu technologie IntelliSense pro soubory JavaScriptu (včetně jQuery). Můžete si ho stáhnout z: http://tinyurl.com/vs2008javascripthotfix*

Kód napsaný pomocí JQuery často používá globální metodu "$ ()" jazyka JavaScript, která načítá jeden nebo více elementů jazyka HTML pomocí selektoru šablon stylů CSS. Například *$ ("#rsvpmsg")* vybere libovolný prvek HTML s ID rsvpmsg, zatímco *$ (". něco")* by vybralo všechny prvky s názvem "text" třídy CSS. Můžete také zapisovat pokročilejší dotazy, jako je "návrat všech zkontrolovaných přepínačů" pomocí dotazu na selektor, jako je: *$ ("vstup [@type= Radio] [@checked]")* .

Po vybrání prvků můžete volat metody, které mají být vyvolány, jako jejich skrývání: *$ ("#rsvpmsg"). Hide ();*

Pro náš scénář protokolu RSVP definujeme jednoduchou funkci JavaScriptu s názvem "AnimateRSVPMessage", která vybere&gt; &lt;div a animuje velikost jejího textového obsahu. Následující kód začíná textem malý a pak způsobí, že se zvýší v časovém rozmezí 400 milisekund:

[!code-html[Main](use-ajax-to-deliver-dynamic-updates/samples/sample10.html)]

Tuto funkci JavaScriptu pak můžeme natočit po úspěšném dokončení volání AJAX tím, že předáte svůj název do pomocné metody AJAX. ActionLink () (přes vlastnost události AjaxOptions "úspěch"):

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample11.aspx)]

A teď, když se klikne na odkaz "RSVP pro tuto událost" a naše volání jazyka AJAX se úspěšně dokončí, bude zpráva o obsahu, která se pošle zpátky, animovat a bude růst velká:

![](use-ajax-to-deliver-dynamic-updates/_static/image6.png)

Kromě poskytování události "úspěch" objekt AjaxOptions zpřístupňuje události při zahájení, selhání a dokončení, které lze zpracovat (spolu s celou řadou dalších vlastností a užitečnými možnostmi).

### <a name="cleanup---refactor-out-a-rsvp-partial-view"></a>Vyčištění – Refaktorovat částečné zobrazení protokolu RSVP

Naše šablona zobrazení podrobností začíná mít za chvilku, což znamená, že se bude porozumět trochu obtížnější. Pro zlepšení čitelnosti kódu se dokončí vytvořením částečného zobrazení – RSVPStatus. ascx – které zapouzdřuje všechny kódy zobrazení protokolu RSVP pro naši stránku podrobností.

To můžeme udělat tak, že kliknete pravým tlačítkem na složku \Views\Dinners a pak zvolíte příkaz nabídky zobrazení pro přidání&gt;. Podíváme se, že bude mít objekt večeře jako svůj ViewModel silně typovaného typu. Pak můžeme obsah protokolu RSVP zkopírovat a vložit z našeho zobrazení Details. aspx.

Až to uděláte, vytvoříme také další částečné zobrazení – EditAndDeleteLinks. ascx – zapouzdřuje náš kód zobrazení odkazu pro úpravy a odstranění. Také ponecháme objekt večeře jako svůj ViewModel silně typovaného typu a zkopírujete nebo vložíte logiku upravit a odstranit z našich zobrazení Details. aspx.

Šablona zobrazení podrobností teď může do dolní části Přidat dvě volání metody HTML. RenderPartial ():

[!code-aspx[Main](use-ajax-to-deliver-dynamic-updates/samples/sample12.aspx)]

To způsobuje, že by měl čistič kódu číst a udržovat.

### <a name="next-step"></a>Další krok

Teď se podíváme na to, jak můžeme ještě dál používat AJAX a přidat do naší aplikace podporu interaktivního mapování.

> [!div class="step-by-step"]
> [Předchozí](secure-applications-using-authentication-and-authorization.md)
> [Další](use-ajax-to-implement-mapping-scenarios.md)

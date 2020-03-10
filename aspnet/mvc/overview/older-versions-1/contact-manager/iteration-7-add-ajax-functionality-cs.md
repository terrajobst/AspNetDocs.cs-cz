---
uid: mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-cs
title: 'Iterace #7 – přidání funkcí AJAXC#() | Microsoft Docs'
author: microsoft
description: V sedmé iteraci vylepšit rychlost reakce a výkon naší aplikace přidáním podpory pro AJAX.
ms.author: riande
ms.date: 02/20/2009
ms.assetid: f1b0809e-8909-444e-b6bb-a5cd1dea3f72
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-7-add-ajax-functionality-cs
msc.type: authoredcontent
ms.openlocfilehash: 7c8eb3d3688674dd2c220b4bd1b5982f2610d0eb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544175"
---
# <a name="iteration-7--add-ajax-functionality-c"></a>Iterace #7 – přidání funkcí AJAXC#()

od [Microsoftu](https://github.com/microsoft)

[Stáhnout kód](iteration-7-add-ajax-functionality-cs/_static/contactmanager_7_cs1.zip)

> V sedmé iteraci vylepšit rychlost reakce a výkon naší aplikace přidáním podpory pro AJAX.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>Sestavování aplikace pro správu kontaktů ASP.NETC#MVC ()

V této sérii kurzů sestavíme celou aplikaci pro správu kontaktů od začátku do konce. Aplikace Správce kontaktů umožňuje ukládat kontaktní údaje – jména, telefonní čísla a e-mailové adresy – seznam lidí.

Aplikaci sestavíme přes několik iterací. U každé iterace doporučujeme aplikaci postupně vylepšit. Cílem tohoto vícenásobného přístupu k iteraci je umožnit pochopení příčiny každé změny.

- Iterace #1 – Vytvoření aplikace V první iteraci vytvoříme nejjednodušším způsobem správce kontaktů. Přidáváme podporu základních databázových operací: vytváření, čtení, aktualizace a odstraňování (CRUD).

- Iterace #2 – nastaví vzhled aplikace jako příjemné. V této iteraci Vylepšete vzhled aplikace úpravou výchozí stránky předlohy zobrazení ASP.NET MVC a šablony kaskádových stylů.

- Iterace #3 – Přidání ověření formuláře. Třetí iterace přidá základní ověřování formuláře. Uživatelům bráníme v odesílání formuláře bez nutnosti vyplnit požadovaná pole formuláře. Ověřujeme taky e-mailové adresy a telefonní čísla.

- Iterace #4 – zajistěte, aby byla aplikace volně spojená. V této čtvrté iteraci využijeme několik vzorů návrhu softwaru, které usnadňují údržbu a úpravy aplikace Správce kontaktů. Například refaktorujte naši aplikaci, aby používala vzor úložiště a vzor vkládání závislostí.

- Iterace #5 – vytvoření testů jednotek. V páté iteraci aplikace usnadňuje údržbu a úpravy přidáním jednotkových testů. Pro naše řadiče a logiku ověřování jsme nastavili třídy datového modelu a testy jednotek.

- Iterace #6 – použití vývoje řízeného testem. V této šesté iteraci přidáme do naší aplikace nové funkce, a to tak, že nejprve zapíšeme testy jednotek a napíšeme kód na testy jednotek. V této iteraci přidáváme skupiny kontaktů.

- Iterace #7 – přidání funkce AJAX V sedmé iteraci vylepšit rychlost reakce a výkon naší aplikace přidáním podpory pro AJAX.

## <a name="this-iteration"></a>Tato iterace

V této iteraci aplikace Správce kontaktů refaktorujte naši aplikaci, aby používala AJAX. Díky využití AJAX je naše aplikace rychlejší reagovat. Pokud musíme na stránce aktualizovat jenom určitou oblast, můžeme se vyhnout vykreslování celé stránky.

Naše zobrazení indexu budeme Refaktorovat, aby při každém výběru nové skupiny kontaktů nemuseli znovu zobrazovat celou stránku. Místo toho, když někdo klikne na skupinu kontaktů, jednoduše aktualizujeme seznam kontaktů a ponecháme zbytek stránky beze změny.

Změníme také způsob, jakým funguje odkaz pro odstranění. Místo zobrazení samostatné potvrzovací stránky zobrazíme dialogové okno pro potvrzení JavaScriptu. Pokud potvrdíte, že chcete odstranit kontakt, je provedena operace odstranění protokolu HTTP na serveru pro odstranění záznamu kontaktu z databáze.

Kromě toho budeme využívat funkci jQuery k přidání animačních efektů do našeho zobrazení indexu. Animace se zobrazí, když se nový seznam kontaktů načítá ze serveru.

Nakonec využijeme podporu rozhraní ASP.NET AJAX pro správu historie prohlížeče. Body historie se vytvoří vždy, když provedeme volání AJAX a aktualizujeme seznam kontaktů. Tímto způsobem budou fungovat tlačítka v prohlížeči zpět a dopředu.

## <a name="why-use-ajax"></a>Proč používat AJAX?

Použití jazyka AJAX má mnoho výhod. Nejprve přidání funkce AJAX do aplikace má za následek lepší uživatelské prostředí. V normální webové aplikaci musí být celá stránka odeslána zpět na server každý a pokaždé, když uživatel provede akci. Vždy, když provedete akci, prohlížeč se zamkne a uživatel musí počkat, až se načte celá stránka a znovu se zobrazí.

To je nepřijatelné prostředí v případě desktopové aplikace. V případě webové aplikace se ale tradičně nejedná o špatné uživatelské prostředí, protože jsme nevěděli, že bychom mohli dělat lepší možnosti. Mysleli jsme, že se jednalo o omezení webových aplikací v případě, že se jednalo o omezení naší imaginationsy.

V aplikaci AJAX nemusíte mít k činnost koncového uživatele, aby bylo možné aktualizovat stránku. Místo toho můžete na pozadí provést asynchronní požadavek na aktualizaci stránky. Nenutí uživatele počkat, dokud se část stránky aktualizuje.

Díky využití technologie AJAX můžete také zvýšit výkon aplikace. Zvažte, jak aplikace Správce kontaktů funguje hned teď bez funkce AJAX. Po kliknutí na skupinu kontaktů je nutné znovu zobrazit celé zobrazení indexu. Seznam kontaktů a seznamu skupin kontaktů musí být načten z databázového serveru. Všechna tato data musí být předána napříč vodiči z webového serveru do webového prohlížeče.

Po přidání funkce AJAX do naší aplikace se však můžeme vyhnout zobrazení celé stránky, když uživatel klikne na skupinu kontaktů. Už nemusíte přesáhnout skupiny kontaktů z databáze. Nepotřebujeme také nasdílet celé zobrazení indexu po celém vedení. Díky využití technologie AJAX snižujeme množství práce, které náš databázový server musí provést, a snižujeme množství síťových přenosů vyžadovaných aplikací.

## <a name="don-t-be-afraid-of-ajax"></a>Nebojte AJAX

Někteří vývojáři vyhnuli používání AJAX, protože se obávat i v prohlížečích nižší úrovně. Chtějí zajistit, aby jejich webové aplikace i nadále fungovaly, když k nim přistupoval prohlížeč, který nepodporuje JavaScript. Vzhledem k tomu, že AJAX závisí na JavaScriptu, někteří vývojáři nepoužívají AJAX.

Nicméně pokud máte pozor, jak implementovat AJAX, můžete vytvářet aplikace, které fungují v prohlížečích pro nejvyšší úroveň i na nižší úrovni. Naše aplikace Správce kontaktů bude fungovat s prohlížeči, které podporují JavaScript a prohlížeče, které ne.

Pokud používáte aplikaci Správce kontaktů s prohlížečem, který podporuje JavaScript, budete mít lepší uživatelské prostředí. Když například kliknete na skupinu kontaktů, bude aktualizována pouze oblast stránky, která zobrazuje kontakty.

Pokud na druhé straně používáte aplikaci Správce kontaktů s prohlížečem, který nepodporuje JavaScript (nebo který má JavaScript zakázaný), budete mít trochu méně žádoucí uživatelské prostředí. Když například kliknete na skupinu kontaktů, je nutné publikovat celé zobrazení indexu zpět do prohlížeče, aby se zobrazil seznam kontaktů.

## <a name="adding-the-required-javascript-files"></a>Přidávání požadovaných souborů JavaScriptu

K přidání funkcí AJAX do naší aplikace bude nutné použít tři soubory JavaScriptu. Všechny tři tyto soubory jsou zahrnuté ve složce Scripts v nové aplikaci ASP.NET MVC.

Pokud máte v úmyslu používat AJAX na více stránkách aplikace, je vhodné zahrnout požadované soubory JavaScriptu do stránky předlohy zobrazení aplikace. Soubory JavaScriptu tak budou automaticky zahrnuty do všech stránek aplikace.

Do značky &lt;Head&gt; na stránce zobrazení předlohy přidejte následující JavaScript:

[!code-html[Main](iteration-7-add-ajax-functionality-cs/samples/sample1.html)]

## <a name="refactoring-the-index-view-to-use-ajax"></a>Refaktoring pro zobrazení indexu pro použití jazyka AJAX

Nechte začít úpravou našeho zobrazení indexu tak, aby se kliknutím na skupinu kontaktů aktualizace zobrazovala pouze v oblasti zobrazení, která zobrazuje kontakty. Červené pole na obrázku 1 obsahuje oblast, kterou chceme aktualizovat.

[![aktualizace jenom kontaktů](iteration-7-add-ajax-functionality-cs/_static/image1.jpg)](iteration-7-add-ajax-functionality-cs/_static/image1.png)

**Obrázek 01**: aktualizace pouze kontaktů ([kliknutím zobrazíte obrázek v plné velikosti](iteration-7-add-ajax-functionality-cs/_static/image2.png))

Prvním krokem je oddělení části zobrazení, kterou chceme asynchronně aktualizovat, na samostatnou částečnou (zobrazení uživatelského ovládacího prvku). Část zobrazení index, která zobrazuje tabulku kontaktů, byla přesunuta do části v seznamu 1.

**Výpis 1 – Views\Contact\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample2.aspx)]

Všimněte si, že částečná v seznamu 1 má jiný model než zobrazení indexu. Atribut *Inherits* ve &lt;direktivě% @ Page%&gt; určuje, že částečné dědění ze skupiny ViewUserControl&lt;&gt; třídy.

Aktualizované zobrazení indexu je obsaženo v seznamu 2.

**Výpis 2 – Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample3.aspx)]

Existují dvě věci, které byste si měli všimnout o aktualizovaném zobrazení v seznamu 2. Nejprve si všimněte, že veškerý obsah přesunutý na částečný je nahrazen voláním HTML. RenderPartial (). Metoda HTML. RenderPartial () je volána, když je nejprve požadováno zobrazení indexu, aby se zobrazila počáteční sada kontaktů.

Za druhé si všimněte, že kód HTML. ActionLink (), který se používá k zobrazení skupin kontaktů, byl nahrazen výrazem AJAX. ActionLink (). Technologie AJAX. ActionLink () je volána s následujícími parametry:

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample4.aspx)]

První parametr představuje text, který má být zobrazen pro odkaz, druhý parametr představuje hodnoty trasy a třetí parametr představuje možnosti AJAX. V tomto případě používáme možnost UpdateTargetId AJAX, která odkazuje na značku&gt; HTML &lt;div, kterou chceme aktualizovat po dokončení požadavku AJAX. Chceme aktualizovat značku&gt; &lt;div novým seznamem kontaktů.

Aktualizovaná metoda index () kontroleru kontaktů je obsažena v seznamu 3.

**Výpis 3-Controllers\ContactController.cs (metoda index)**

[!code-csharp[Main](iteration-7-add-ajax-functionality-cs/samples/sample5.cs)]

Podmínka aktualizovaného indexu () podmíněně vrátí jednu ze dvou věcí. Pokud je akce index () vyvolána požadavkem jazyka AJAX, kontroler vrátí částečný. V opačném případě akce index () vrátí celé zobrazení.

Všimněte si, že akce index () nepotřebuje při vyvolání požadavku AJAX vracet tolik dat. V kontextu normálního požadavku vrátí akce index seznam všech skupin kontaktů a vybrané skupiny kontaktů. V kontextu požadavku AJAX vrátí akce index () pouze vybranou skupinu. AJAX znamená na databázovém serveru méně práce.

Naše změněné zobrazení indexu funguje v případě prohlížečů pro nejvyšší úroveň i pro klienty nižší úrovně. Pokud kliknete na skupinu kontaktů a váš prohlížeč podporuje jazyk JavaScript, bude aktualizována pouze oblast zobrazení, která obsahuje seznam kontaktů. Pokud na druhé straně váš prohlížeč nepodporuje JavaScript, pak se aktualizuje celé zobrazení.

Naše aktualizované zobrazení indexu obsahuje jeden problém. Po kliknutí na skupinu kontaktů není zvýrazněna vybraná skupina. Vzhledem k tomu, že seznam skupin je zobrazen mimo oblast, která je aktualizována během požadavku AJAX, není zvýrazněna pravá skupina. Tento problém vyřešíme v další části.

## <a name="adding-jquery-animation-effects"></a>Přidávání efektů animace jQuery

Když kliknete na odkaz na webové stránce, normálně můžete pomocí indikátoru průběhu prohlížeče zjistit, jestli prohlížeč aktivně načítá aktualizovaný obsah. Při provádění požadavku AJAX na druhé straně indikátor průběhu prohlížeče nezobrazuje žádný průběh. To může uživatelům proměnit nerv. Jak poznáte, jestli je prohlížeč zmrazený?

Existuje několik způsobů, jak můžete určit, že při provádění požadavku AJAX je prováděna práce. Jedním z přístupů je zobrazení jednoduché animace. Můžete například rozmizet oblast při zahájení a zmizení požadavku AJAX v oblasti po dokončení žádosti.

K vytvoření efektů animace použijeme knihovnu jQuery, která je součástí Microsoft ASP.NET rozhraní MVC. Aktualizované zobrazení indexu je obsaženo v seznamu 4.

**Výpis 4 – Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample6.aspx)]

Všimněte si, že aktualizované zobrazení indexu obsahuje tři nové funkce JavaScriptu. První dvě funkce používají jQuery ke zmizení a zmizení v seznamu kontaktů po kliknutí na novou skupinu kontaktů. Třetí funkce zobrazí chybovou zprávu, když požadavek AJAX způsobí chybu (například časový limit sítě).

První funkce také postará o zvýraznění vybrané skupiny. Atribut class = Selected je přidán do nadřazeného elementu (element LI), na který se odkazuje element. Příkaz jQuery usnadňuje výběr správného prvku a přidání třídy CSS.

Tyto skripty jsou svázány s odkazy skupin s použitím parametru AJAX. ActionLink () AjaxOptions. Aktualizované volání metody AJAX. ActionLink () vypadá takto:

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample7.aspx)]

## <a name="adding-browser-history-support"></a>Přidání podpory pro historii prohlížeče

Když kliknete na odkaz pro aktualizaci stránky, aktualizuje se historie vašeho prohlížeče. Tímto způsobem můžete kliknutím na tlačítko zpět v prohlížeči přejít zpátky v čase do předchozího stavu stránky. Pokud například kliknete na skupinu kontaktů přátelé a pak na skupinu obchodních kontaktů, můžete kliknout na tlačítko zpět v prohlížeči a přejít zpět na stav stránky při výběru skupiny kontaktů přátelé.

Provádění požadavku AJAX bohužel neaktualizuje historii prohlížeče automaticky. Pokud kliknete na skupinu kontaktů a seznam porovnávacích kontaktů se načte s požadavkem AJAX, nebude se aktualizovat historie prohlížeče. Po výběru nové skupiny kontaktů nelze přejít zpět na skupinu kontaktů pomocí tlačítka zpět v prohlížeči.

Pokud chcete, aby uživatelé mohli používat tlačítko zpět v prohlížeči po provedení požadavků AJAX, musíte provést trochu více práce. Je potřeba využít výhod funkce správy historie prohlížeče postavených v rozhraní ASP.NET AJAX.

ASP.NET v prohlížeči AJAX v historii, je třeba provést tři věci:

1. Povolte historii prohlížeče nastavením vlastnosti enableBrowserHistory na hodnotu true.
2. Uloží body historie při změně stavu zobrazení voláním metody addHistoryPoint ().
3. Rekonstruovat stav zobrazení při vyvolání události navigate.

Aktualizované zobrazení indexu je obsaženo v seznamu 5.

**Výpis 5 – Views\Contact\Index.aspx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample8.aspx)]

V výpisu 5 je ve funkci pageInit () povolena historie prohlížeče. Funkce pageInit () se používá také k nastavení obslužné rutiny události navigate. Událost Navigate je vyvolána vždy, když tlačítko vpřed nebo zpět v prohlížeči způsobí změnu stavu stránky.

Metoda beginContactList () je volána, když kliknete na skupinu kontaktů. Tato metoda vytvoří nový bod historie voláním metody addHistoryPoint (). Do historie se přidá ID kliknutí na skupinu kontaktů.

ID skupiny se načte z atributu expand na odkaz skupiny kontaktů. Odkaz je vykreslen s následujícím voláním jazyka AJAX. ActionLink ().

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample9.aspx)]

Poslední parametr předaný metodě AJAX. ActionLink () přidá atribut Expanded na odkaz (malý počet pro kompatibilitu s NORMou XHTML).

Když uživatel narazí na tlačítko zpět nebo vpřed v prohlížeči, událost Navigate se vyvolá a zavolá se metoda Navigate (). Tato metoda aktualizuje kontakty zobrazené na stránce tak, aby odpovídaly stavu stránky, který odpovídá bodu historie prohlížeče předanému metodě Navigate.

## <a name="performing-ajax-deletes"></a>Provádění odstraňování AJAX

Pokud chcete odstranit kontakt v současné době, musíte kliknout na odkaz odstranit a pak kliknout na tlačítko Odstranit zobrazené na stránce pro potvrzení odstranění (viz obrázek 2). Zdá se, že hodně požadavků na stránky pro něco jednoduchého, jako je odstranění záznamu databáze.

[![stránce pro potvrzení odstranění](iteration-7-add-ajax-functionality-cs/_static/image2.jpg)](iteration-7-add-ajax-functionality-cs/_static/image3.png)

**Obrázek 02**: Stránka pro potvrzení odstranění ([kliknutím zobrazíte obrázek v plné velikosti](iteration-7-add-ajax-functionality-cs/_static/image4.png))

Nachází na to, že se stránka pro potvrzení odstranění přeskočit a odstraní kontakt přímo ze zobrazení indexu. Měli byste se tomuto pokušení vyhnout, protože tento přístup otevře vaši aplikaci pro bezpečnostní otvory. Obecně platí, že nebudete chtít provést operaci HTTP GET při vyvolání akce, která mění stav webové aplikace. Při odstraňování je potřeba provést HTTP POST nebo ještě lepší, ale i operaci odstranění protokolu HTTP.

Odkaz Delete je obsažený v ContactList částečně. Aktualizovaná verze ContactList částečně je obsažena v seznamu 6.

**Výpis 6 – Views\Contact\ContactList.ascx**

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample10.aspx)]

Odkaz Delete je vykreslen s následujícím voláním metody AJAX. ImageActionLink ():

[!code-aspx[Main](iteration-7-add-ajax-functionality-cs/samples/sample11.aspx)]

> [!NOTE] 
> 
> AJAX. ImageActionLink () není standardní součástí architektury ASP.NET MVC. AJAX. ImageActionLink () je vlastní pomocná metoda, která je součástí projektu správce kontaktů.

Parametr AjaxOptions má dvě vlastnosti. Nejprve se vlastnost potvrdit používá k zobrazení dialogového okna pro potvrzení JavaScriptu. Za druhé se k provedení operace odstranění protokolu HTTP používá vlastnost HttpMethod.

Výpis 7 obsahuje novou akci AjaxDelete (), která byla přidána do kontroleru kontaktů.

**Výpis 7 – Controllers\ContactController.cs (AjaxDelete)**

[!code-csharp[Main](iteration-7-add-ajax-functionality-cs/samples/sample12.cs)]

Akce AjaxDelete () je upravena pomocí atributu AcceptVerbs. Tento atribut brání vyvolání akce s výjimkou jakékoli jiné operace HTTP, než je operace HTTP DELETE. Konkrétně nemůžete tuto akci vyvolat pomocí protokolu HTTP GET.

Po odstranění záznamu databáze je třeba zobrazit aktualizovaný seznam kontaktů, které neobsahují odstraněný záznam. Metoda AjaxDelete () vrátí částečný ContactList a aktualizovaný seznam kontaktů.

## <a name="summary"></a>Souhrn

V této iteraci jsme do naší aplikace Správce kontaktů přidali funkce AJAX. Pomocí AJAX jsme vylepšili rychlost odezvy a výkon naší aplikace.

Nejdříve jsme převedli zobrazení indexu tak, aby se kliknutím na skupinu kontaktů neaktualizovalo celé zobrazení. Místo toho se kliknutím na skupinu kontaktů aktualizuje jenom seznam kontaktů.

V dalším kroku jsme pro zmizení a zmizení v seznamu kontaktů používali efekty animace jQuery. Přidání animace do aplikace AJAX lze použít k tomu, aby uživatelům aplikace poskytovala ekvivalent indikátoru průběhu prohlížeče.

Přidali jsme také podporu historie prohlížeče do naší aplikace AJAX. Povolili jsme uživatelům kliknout na tlačítka zpět a přeposlání v prohlížeči, abyste změnili stav zobrazení indexu.

Nakonec jsme vytvořili odkaz Delete, který podporuje operace odstranění protokolu HTTP. Při provádění odstraňování v AJAX umožňují uživatelům odstraňovat záznamy databáze, aniž by museli vyžadovat, aby si uživatel vyžádal další stránku pro potvrzení odstranění.

> [!div class="step-by-step"]
> [Předchozí](iteration-6-use-test-driven-development-cs.md)
> [Další](iteration-1-create-the-application-vb.md)

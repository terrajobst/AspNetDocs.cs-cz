---
uid: mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
title: 'Iterace #3 – Přidání ověření formulářeC#() | Microsoft Docs'
author: microsoft
description: Třetí iterace přidá základní ověřování formuláře. Uživatelům bráníme v odesílání formuláře bez nutnosti vyplnit požadovaná pole formuláře. Ověřujeme také emai...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 51a0d175-913b-43d8-95e3-840fb96ad1a9
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-3-add-form-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: af2e86e820f60f0a3d8e3db8f78eba67ef63579a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544469"
---
# <a name="iteration-3--add-form-validation-c"></a>Iterace #3 – Přidání ověření formulářeC#()

od [Microsoftu](https://github.com/microsoft)

[Stáhnout kód](iteration-3-add-form-validation-cs/_static/contactmanager_3_cs1.zip)

> Třetí iterace přidá základní ověřování formuláře. Uživatelům bráníme v odesílání formuláře bez nutnosti vyplnit požadovaná pole formuláře. Ověřujeme taky e-mailové adresy a telefonní čísla.

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

V této druhé iteraci aplikace Správce kontaktů přidáme základní ověřování formuláře. Uživatelům bráníme v odesílání kontaktu bez nutnosti zadávat hodnoty pro požadovaná pole formuláře. Také Ověřujeme telefonní čísla a e-mailové adresy (viz obrázek 1).

[![dialogového okna Nový projekt](iteration-3-add-form-validation-cs/_static/image1.jpg)](iteration-3-add-form-validation-cs/_static/image1.png)

**Obrázek 01**: formulář s ověřením ([kliknutím zobrazíte obrázek v plné velikosti](iteration-3-add-form-validation-cs/_static/image2.png))

V této iteraci přidáme logiku ověřování přímo k akcím kontroleru. Obecně to není doporučený způsob, jak přidat ověřování do aplikace ASP.NET MVC. Lepším přístupem je umístit logiku ověřování aplikace v samostatné [vrstvě služby](http://martinfowler.com/eaaCatalog/serviceLayer.html). V další iteraci refaktorujte aplikaci Správce kontaktů, aby se aplikace udržovala lépe.

V této iteraci, aby bylo možné něco jednoduchého, zapíšeme ručně kód pro ověření. Namísto psaní ověřovacího kódu dodržovali můžeme využít rozhraní ověřování. Například můžete použít blok aplikace Microsoft Enterprise Library Validation (VAB) k implementaci logiky ověření pro aplikaci ASP.NET MVC. Další informace o bloku aplikace ověřování najdete v těchto tématech:

[*http://msdn.microsoft.com/library/dd203099.aspx*](https://msdn.microsoft.com/library/dd203099.aspx)

## <a name="adding-validation-to-the-create-view"></a>Přidání ověření do zobrazení pro vytvoření

Nechte začít tím, že do zobrazení pro vytváření přidáte logiku ověřování. Naštěstí, protože jsme vygenerovali zobrazení pro vytvoření pomocí sady Visual Studio, zobrazení vytvořit již obsahuje veškerou nezbytnou logiku uživatelského rozhraní pro zobrazení ověřovacích zpráv. Zobrazení vytvořit je obsaženo v seznamu 1.

**Výpis 1 – \Views\Contact\Create.aspx**

[!code-aspx[Main](iteration-3-add-form-validation-cs/samples/sample1.aspx)]

Všimněte si volání pomocné metody HTML. ovládací souhrnu ověření (), která se zobrazuje hned nad formulářem HTML. Pokud dojde k chybovým zprávám ověřování, pak tato metoda zobrazí ověřovací zprávy v seznamu s odrážkami.

Všimněte si, kromě toho, volání HTML. ValidationMessage (), která se zobrazí vedle každého pole formuláře. Pomocník ValidationMessage () zobrazí konkrétní chybovou zprávu ověření. V případě výpisu 1 se zobrazí hvězdička, pokud dojde k chybě ověření.

Nakonec pomocník HTML. TextBox () automaticky vykreslí třídu kaskádového stylu šablony, pokud dojde k chybě ověřování přidružené k vlastnosti zobrazené v pomocné rutině. Pomocník HTML. TextBox () vykreslí třídu s názvem **Input-Validation-Error**.

Při vytváření nové aplikace ASP.NET MVC se šablona stylů s názvem Web. CSS vytvoří automaticky ve složce obsahu. Tato šablona stylů obsahuje následující definice tříd šablon stylů CSS souvisejících s vzhledem chybových zpráv ověřování:

[!code-css[Main](iteration-3-add-form-validation-cs/samples/sample2.css)]

Třída pole-ověření – chyba se používá k vytvoření stylu výstupu vygenerovaného pomocníkem HTML. ValidationMessage (). Třída Input-Validation-Error se používá k vytvoření stylu textového pole (vstupu) vykresleného pomocníkem HTML. TextBox (). Třída ověření-Summary-Errors slouží k vytvoření stylu neuspořádaného seznamu vykresleného pomocníkem HTML. ovládací souhrnu ověření ().

> [!NOTE] 
> 
> Můžete upravit třídy šablon stylů popsané v této části, chcete-li přizpůsobit vzhled chybových zpráv ověřování.

## <a name="adding-validation-logic-to-the-create-action"></a>Přidání logiky ověřování do akce vytvořit

V současné době se zobrazení vytvořit nezobrazí chybové zprávy ověřování, protože jsme nenapsali logiku pro vygenerování všech zpráv. Aby bylo možné zobrazit chybové zprávy ověřování, je nutné přidat chybové zprávy do ModelState.

> [!NOTE] 
> 
> Metoda UpdateModel () přidává do ModelState automaticky chybové zprávy, když při přiřazování hodnoty pole formuláře k vlastnosti dojde k chybě. Například pokud se pokusíte přiřadit řetězec "Apple" k vlastnosti DatumNarození, která přijímá hodnoty DateTime, metoda UpdateModel () přidá chybu ModelState.

Upravená metoda Create () v seznamu 2 obsahuje novou část, která ověřuje vlastnosti třídy kontaktů před tím, než se nový kontakt vloží do databáze.

**Výpis 2-Controllers\ContactController.cs (vytvoření s ověřením)**

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample3.cs)]

Oddíl Validate vynutil čtyři odlišná ověřovací pravidla:

- Vlastnost FirstName musí mít délku větší než nula (a nemůže se skládat pouze z mezer).
- Vlastnost LastName musí mít délku větší než nula (a nesmí se skládat pouze z mezer).
- Pokud má vlastnost Phone hodnotu (má délku větší než 0), musí vlastnost Phone odpovídat regulárnímu výrazu.
- Pokud má vlastnost email hodnotu (má délku větší než 0), musí vlastnost email odpovídat regulárnímu výrazu.

Pokud dojde k porušení ověřovacího pravidla, do ModelState se přidá chybová zpráva s metodou AddModelError (). Když do ModelState přidáte zprávu, zadáte název vlastnosti a text chybové zprávy ověřování. Tato chybová zpráva se zobrazí v zobrazení pomocí pomocných metod HTML. ovládací souhrnu ověření () a HTML. ValidationMessage ().

Po spuštění ověřovacích pravidel je zaškrtnuta vlastnost IsValid třídy ModelState. Vlastnost IsValid vrátí hodnotu false, pokud byly do ModelState přidány jakékoli chybové zprávy ověřování. Pokud se ověření nepovede, formulář pro vytvoření se znovu zobrazí s chybovými zprávami.

> [!NOTE] 
> 
> Mám regulární výrazy pro ověření telefonního čísla a e-mailové adresy z úložiště regulárních výrazů na [ *http://regexlib.com* ](http://regexlib.com)

## <a name="adding-validation-logic-to-the-edit-action"></a>Přidání logiky ověřování do akce upravit

Akce upravit () aktualizuje kontakt. Akce Edit () musí provést přesně stejné ověření jako akce Create (). Místo duplikace stejného ověřovacího kódu by měl být kontroler kontaktů Refaktorovat, aby akce Create () a Edit () volaly stejnou metodu ověřování.

Upravená třída správce kontaktů je obsažena v seznamu 3. Tato třída má novou metodu ValidateContact (), která je volána v rámci akcí Create () a Edit ().

**Výpis 3 – Controllers\ContactController.cs**

[!code-csharp[Main](iteration-3-add-form-validation-cs/samples/sample4.cs)]

## <a name="summary"></a>Souhrn

V této iteraci jsme přidali základní ověřování formuláře do naší aplikace Správce kontaktů. Naše logika ověřování brání uživatelům v odesílání nového kontaktu nebo úpravě existujícího kontaktu bez zadání hodnot pro vlastnosti FirstName a LastName. Kromě toho musí uživatelé zadávat platná telefonní čísla a e-mailové adresy.

V této iteraci jsme do naší aplikace Správce kontaktů přidali logiku ověřování nejjednodušším způsobem. Kombinování logiky ověřování do naší logiky kontroleru ale v dlouhodobém období vytvoří problémy. Naše aplikace bude obtížnější se udržovat a upravit v průběhu času.

V další iteraci budeme Refaktorovat naši logiku ověřování a logiku přístupu k databázi z našich řadičů. Pomůžeme vám využít několik principů návrhu softwaru, které nám umožní vytvořit více volně vázaných a udržovatelných aplikací.

> [!div class="step-by-step"]
> [Předchozí](iteration-2-make-the-application-look-nice-cs.md)
> [Další](iteration-4-make-the-application-loosely-coupled-cs.md)

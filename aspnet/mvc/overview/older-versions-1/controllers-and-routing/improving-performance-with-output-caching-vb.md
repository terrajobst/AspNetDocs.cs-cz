---
uid: mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
title: Zvýšení výkonu ukládání výstupu do mezipaměti (VB) | Microsoft Docs
author: microsoft
description: V tomto kurzu zjistíte, jak můžete významně zlepšit výkon webových aplikací ASP.NET MVC, a využít tak ukládání výstupu do mezipaměti. ...
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 0e7b4d85-2c46-4eaf-b6a8-6cd566a67334
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/improving-performance-with-output-caching-vb
msc.type: authoredcontent
ms.openlocfilehash: b713b56e149f196794b3223ba88e3b41bf3e34c4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601246"
---
# <a name="improving-performance-with-output-caching-vb"></a>Zlepšení výkonu ukládáním výstupů do mezipaměti (VB)

od [Microsoftu](https://github.com/microsoft)

> V tomto kurzu zjistíte, jak můžete významně zlepšit výkon webových aplikací ASP.NET MVC, a využít tak ukládání výstupu do mezipaměti. Naučíte se, jak uložit výsledek vrácený z akce kontroleru, aby se stejný obsah nemusel vytvořit, a to pokaždé, když nový uživatel vyvolá akci.

Cílem tohoto kurzu je vysvětlit, jak můžete významně zlepšit výkon aplikace ASP.NET MVC, a využít tak výhod výstupní mezipaměti. Výstupní mezipaměť umožňuje ukládat do mezipaměti obsah vrácený akcí kontroleru. Tímto způsobem není nutné vygenerovat stejný obsah a pokaždé, když je vyvolána stejná akce kontroleru.

Představte si například, že vaše aplikace ASP.NET MVC zobrazuje seznam záznamů databáze v zobrazení s názvem index. Obvykle každý a pokaždé, když uživatel vyvolá akci kontroleru, která vrací zobrazení indexu, musí být sada záznamů databáze načtena z databáze spuštěním databázového dotazu.

Pokud na druhé straně využijete výstupní mezipaměť, můžete se vyhnout provádění databázového dotazu pokaždé, když kterýkoli uživatel vyvolá stejnou akci kontroleru. Zobrazení se dá načíst z mezipaměti, místo aby se znovu vygenerovala z akce kontroleru. Ukládání do mezipaměti umožňuje zabránit tomu, aby na serveru prováděl redundantní práci.

#### <a name="enabling-output-caching"></a>Povolení ukládání výstupu do mezipaměti

Ukládání výstupu do mezipaměti povolíte tak, že přidáte atribut &lt;OutputCache&gt; buď na akci samostatného kontroleru, nebo na celou třídu kontroleru. Například kontroler v výpisu 1 zveřejňuje akci s názvem index (). Výstup akce index () je uložen do mezipaměti po dobu 10 sekund.

**Výpis 1 – Controllers\HomeController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample1.vb)]

Ve verzích beta verze ASP.NET MVC nefunguje ukládání výstupu do mezipaměti pro adresu URL, jako je [http://www.MySite.com/](http://www.mysite.com/). Místo toho je nutné zadat adresu URL, například [http://www.MySite.com/Home/Index](http://www.mysite.com/Home/Index).

V výpisu 1 se výstup akce index () ukládá do mezipaměti po dobu 10 sekund. Pokud dáváte přednost, můžete zadat mnohem delší dobu trvání mezipaměti. Například pokud chcete, aby se výstup akce kontroleru do mezipaměti najednal na jeden den, můžete zadat dobu trvání mezipaměti 86400 sekund (60 sekund \* 60 minut \* 24 hodin).

Není zaručeno, že obsah bude uložen do mezipaměti po dobu, kterou zadáte. Když dojde k nízkému množství paměťových prostředků, mezipaměť začne automaticky vyřazovat obsah.

Domovský řadič v seznamu 1 vrátí zobrazení indexu v seznamu 2. Neexistují žádné zvláštní informace o tomto zobrazení. Zobrazení index jednoduše zobrazí aktuální čas (viz obrázek 1).

**Výpis 2 – Views\Home\Index.aspx**

[!code-aspx[Main](improving-performance-with-output-caching-vb/samples/sample2.aspx)]

**Obrázek 1 – zobrazení indexu v mezipaměti**

![clip_image002](improving-performance-with-output-caching-vb/_static/image1.jpg)

Pokud akci index () zavoláte několikrát tak, že zadáte adresu URL/Home/Index do panelu Adresa v prohlížeči a znovu kliknete na tlačítko Aktualizovat/načíst znovu, čas zobrazený v zobrazení indexu se nemění na 10 sekund. Zobrazí se stejná doba, protože zobrazení je uloženo v mezipaměti.

Je důležité si uvědomit, že stejné zobrazení je uloženo v mezipaměti pro všechny uživatele, kteří navštíví vaši aplikaci. Kdokoli, kdo vyvolá akci index (), obdrží stejnou verzi zobrazení indexu v mezipaměti. To znamená, že množství práce, které webový server musí provést pro obsluhu zobrazení indexu, se výrazně zkrátí.

Zobrazení v seznamu 2 se bude provádět něco jednoduchého. Zobrazení pouze zobrazí aktuální čas. Mohli byste ale stejně snadno ukládat do mezipaměti zobrazení, které zobrazuje sadu záznamů databáze. V takovém případě nemusí být sada záznamů databáze načtena z databáze a pokaždé, když je vyvolána akce kontroleru, která zobrazení vrací. Ukládání do mezipaměti může snížit množství práce, které musí webový server i databázový server provést.

V zobrazení MVC Nepoužívejte stránku &lt;direktivy% @ OutputCache%&gt;. Tato direktiva je vyhodnocena z webového formuláře World a neměla by se používat v aplikaci ASP.NET MVC. 

#### <a name="where-content-is-cached"></a>Umístění obsahu do mezipaměti

Ve výchozím nastavení platí, že při použití atributu &lt;OutputCache&gt; je obsah uložen do mezipaměti ve třech umístěních: webový server, všechny proxy servery a webový prohlížeč. Úpravou vlastnosti umístění&gt; atributu &lt;OutputCache se dá řídit přesně tam, kde je obsah uložený v mezipaměti.

Vlastnost Location můžete nastavit na jednu z následujících hodnot:

> · Jakýmikoli
> 
> · Služba
> 
> · Proudu
> 
> · Server
> 
> · NTato
> 
> · ServerAndClient

Ve výchozím nastavení má vlastnost Location hodnotu any. Existují však situace, kdy je vhodné ukládat do mezipaměti pouze v prohlížeči nebo pouze na serveru. Pokud například ukládáte do mezipaměti informace, které jsou pro každého uživatele individuální, pak byste neměli ukládat informace na server do mezipaměti. Pokud pro různé uživatele zobrazujete různé informace, měli byste tyto informace ukládat do mezipaměti jenom v klientovi.

Například kontroler v seznamu 3 zveřejňuje akci s názvem GetName (), která vrací aktuální uživatelské jméno. Pokud se konektor připojí k webu a vyvolá akci GetName (), pak akce vrátí řetězec "Hi-zdířka". Pokud se následně Jill do webu a vyvolá akci GetName (), zobrazí se také řetězec "Hi kolík". Řetězec je uložen v mezipaměti na webovém serveru pro všechny uživatele po počátečním vyvolání akce kontroleru.

**Výpis 3 – Controllers\BadUserController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample3.vb)]

Nejpravděpodobnější příčinou je, že kontroler v seznamu 3 nefunguje tak, jak chcete. Nechcete zobrazit zprávu "Hi-Link" na Jill.

Nikdy byste neměli ukládat do mezipaměti individuální obsah v mezipaměti serveru. Můžete ale chtít ukládat do mezipaměti přizpůsobený obsah v mezipaměti prohlížeče, aby se zlepšil výkon. Pokud ukládáte obsah do mezipaměti v prohlížeči a uživatel spustí stejnou akci kontroleru několikrát, může být obsah načten z mezipaměti prohlížeče namísto serveru.

Upravený kontroler v seznamu 4 ukládá do mezipaměti výstup akce GetName (). Obsah je však uložen v mezipaměti pouze v prohlížeči, nikoli na serveru. Tímto způsobem, když více uživatelů vyvolá metodu GetName (), každá osoba získá své vlastní uživatelské jméno a ne uživatelské jméno jiné osoby.

**Výpis 4 – Controllers\UserController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample4.vb)]

Všimněte si, že atribut &lt;OutputCache&gt; v seznamu 4 obsahuje vlastnost Location nastavenou na hodnotu OutputCacheLocation. Client. Atribut &lt;OutputCache&gt; také obsahuje vlastnost úložiště. Vlastnost neukládejte se používá k informování proxy serverů a prohlížečů, že by neměly ukládat trvalou kopii obsahu v mezipaměti.

#### <a name="varying-the-output-cache"></a>Proměnlivá výstupní mezipaměť

V některých situacích možná budete chtít, aby různé verze stejného obsahu v mezipaměti byly. Představte si například, že vytváříte stránku hlavní/podrobnosti. Stránka předlohy zobrazuje seznam názvů filmů. Po kliknutí na název získáte podrobnosti o vybraném videu.

Pokud ukládáte stránku podrobností do mezipaměti, zobrazí se v podrobnostech pro stejný film bez ohledu na to, na který film kliknete. První film vybraný prvním uživatelem se zobrazí všem budoucím uživatelům.

Tento problém můžete vyřešit tím, že využijete vlastnost VaryByParam atributu &lt;OutputCache&gt;. Tato vlastnost umožňuje vytvořit různé verze velmi stejného obsahu v mezipaměti, když parametr formuláře nebo parametr řetězce dotazu se liší.

Například kontroler v seznamu 5 zpřístupňuje dvě akce pojmenované hlavní () a podrobnosti (). Akce Master () vrátí seznam názvů filmů a akce podrobnosti () vrátí podrobnosti vybraného filmu.

**Výpis 5 – Controllers\MoviesController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample5.vb)]

Akce Master () obsahuje vlastnost VaryByParam s hodnotou "none". Při vyvolání akce Master () se vrátí stejná verze zobrazení hlavního v mezipaměti. Parametry formuláře nebo parametry řetězce dotazu jsou ignorovány (viz obrázek 2).

**Obrázek 2 – zobrazení/Movies/Master**

![clip_image004](improving-performance-with-output-caching-vb/_static/image2.jpg)

**Obrázek 3 – zobrazení/Movies/Details**

![clip_image006](improving-performance-with-output-caching-vb/_static/image3.jpg)

Akce podrobnosti () obsahuje vlastnost VaryByParam s hodnotou ID. Při předání různých hodnot parametru ID do akce kontroleru se generují různé verze v mezipaměti zobrazení podrobností.

Je důležité pochopit, že použití vlastnosti VaryByParam má za následek větší mezipaměť a ne méně. Pro každou jinou verzi parametru ID je vytvořena odlišná verze zobrazení v mezipaměti.

Vlastnost VaryByParam můžete nastavit na následující hodnoty:

> \* = vytvořit jinou verzi uloženou v mezipaměti vždy, když se liší parametr řetězce formuláře nebo dotazu.
> 
> None = nikdy nevytvářet jiné verze v mezipaměti
> 
> Střední seznam parametrů = vytvořit jiné verze v mezipaměti vždy, když se v seznamu změní kterýkoli parametr řetězce formuláře nebo řetězce dotazu

#### <a name="creating-a-cache-profile"></a>Vytváření profilu mezipaměti

Jako alternativu ke konfiguraci vlastností výstupní mezipaměti úpravou vlastností atributu &lt;OutputCache&gt; můžete vytvořit profil mezipaměti v souboru webové konfigurace (Web. config). Vytvoření profilu mezipaměti v konfiguračním souboru webu nabízí několik důležitých výhod.

Nejprve pomocí konfigurace ukládání výstupu do mezipaměti v konfiguračním souboru webu můžete řídit, jak akce řadiče ukládají obsah do mezipaměti v jednom centrálním umístění. Můžete vytvořit jeden profil mezipaměti a použít profil pro několik řadičů nebo akcí kontroleru.

Za druhé můžete upravit konfigurační soubor webu bez nutnosti opětovné kompilace aplikace. Pokud potřebujete zakázat ukládání do mezipaměti pro aplikaci, která již byla nasazena do produkčního prostředí, můžete jednoduše upravit profily mezipaměti definované v konfiguračním souboru webu. Všechny změny konfiguračního souboru webu budou zjišťovány automaticky a aplikovány.

Například část &lt;ukládání do mezipaměti&gt; webové konfigurace v seznamu 6 definuje profil mezipaměti s názvem Cache1Hour. Oddíl &lt;Caching&gt; se musí nacházet v části &lt;System. Web&gt; konfiguračního souboru webu.

**Výpis 6 – ukládání části do mezipaměti pro web. config**

[!code-xml[Main](improving-performance-with-output-caching-vb/samples/sample6.xml)]

Kontroler v seznamu 7 ukazuje, jak můžete použít profil Cache1Hour pro akci kontroleru s atributem &lt;OutputCache&gt;.

**Výpis 7 – Controllers\ProfileController.vb**

[!code-vb[Main](improving-performance-with-output-caching-vb/samples/sample7.vb)]

Pokud vyvoláte akci index () vystavenou kontrolérem v seznamu 7, bude se stejná doba vracet po dobu 1 hodiny.

#### <a name="summary"></a>Souhrn

Ukládání výstupu do mezipaměti poskytuje velmi snadný způsob, jak významně zlepšit výkon aplikací ASP.NET MVC. V tomto kurzu jste zjistili, jak pomocí atributu &lt;OutputCache&gt; ukládat výstup akcí kontroleru do mezipaměti. Zjistili jste také, jak upravit vlastnosti atributu &lt;OutputCache&gt;, jako jsou například vlastnosti Duration a VaryByParam, abyste mohli změnit způsob ukládání obsahu do mezipaměti. Nakonec jste zjistili, jak definovat profily mezipaměti v konfiguračním souboru webu.

> [!div class="step-by-step"]
> [Předchozí](understanding-action-filters-vb.md)
> [Další](adding-dynamic-content-to-a-cached-page-vb.md)

---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
title: 'Část 8: nákupní košík s aktualizacemi AJAX | Microsoft Docs'
author: jongalloway
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 8 pokrývá nákupní košík s aktualizacemi AJAX.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 26b2f55e-ed42-4277-89b0-c941eb754145
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-8
msc.type: authoredcontent
ms.openlocfilehash: 89897ad41b217764cbd17317d4bf5d6a5c5d488f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539254"
---
# <a name="part-8-shopping-cart-with-ajax-updates"></a>8\. část: Nákupní košík s aktualizacemi Ajax

o [Jan Galloway](https://github.com/jongalloway)

> Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio pro vývoj webů.  
>   
> Úložiště hudby MVC je zjednodušená ukázka implementace úložiště, která prodává hudební alba online a implementuje základní funkce pro správu webů, přihlašování uživatelů a nákupních košíků.  
>   
> V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 8 pokrývá nákupní košík s aktualizacemi AJAX.

Uživatelům umožníme umístit alba do svého košíku bez registrace, ale budou se muset zaregistrovat jako hosté, aby se dokončila rezervace. Proces nákupu a rezervace se rozdělí na dva řadiče: kontroler ShoppingCart, který umožňuje anonymně přidávat položky na košík a kontroler rezervace, který zpracovává proces rezervace. V této části začneme s nákupním košíkem a pak sestavíme proces registrace v následující části.

## <a name="adding-the-cart-order-and-orderdetail-model-classes"></a>Přidání tříd modelu košíku, objednávky a OrderDetail

Na základě nákupních košíků a procesů rezervace se budou využívat některé nové třídy. Klikněte pravým tlačítkem na složku modely a přidejte třídu košíku (Cart.cs) s následujícím kódem.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample1.cs)]

Tato třída je poměrně podobná ostatním, co jsme doposud používali, s výjimkou atributu [key] pro vlastnost RecordId. Položky z košíku budou mít identifikátor řetězce s názvem CartID, který umožní anonymní nákupy, ale tabulka obsahuje primární klíč s názvem RecordId. Podle konvence Entity Framework jako první očekává, že primární klíč pro tabulku s názvem košík bude buď CartId, nebo ID, ale můžeme ho snadno přepsat prostřednictvím poznámek nebo kódu, pokud chceme. Toto je příklad toho, jak můžeme použít jednoduché konvence v Entity Framework kódu jako první, když se na nás líbí, ale neomezujeme je, když ne.

Dále přidejte třídu Order (Order.cs) s následujícím kódem.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample2.cs)]

Tato třída sleduje informace o souhrnu a doručení pro objednávku. **Ještě nebude zkompilován**, protože má vlastnost navigace OrderDetails, která závisí na třídě, kterou jsme ještě nevytvořili. Pojďme to teď opravit přidáním třídy s názvem OrderDetail.cs a přidáním následujícího kódu.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample3.cs)]

Provedeme jednu poslední aktualizaci třídy MusicStoreEntities, aby zahrnovala DbSets, které zveřejňují tyto nové třídy modelu, včetně Negenerickými&lt;interpretu&gt;. Aktualizovaná třída MusicStoreEntities se zobrazuje níže.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample4.cs)]

## <a name="managing-the-shopping-cart-business-logic"></a>Správa obchodní logiky nákupního košíku

V dalším kroku vytvoříme třídu ShoppingCart ve složce modely. Model ShoppingCart zpracovává přístup k datům v tabulce košíku. Kromě toho zpracuje obchodní logiku pro přidání a odebrání položek z nákupního košíku.

Vzhledem k tomu, že nechcete vyžadovat, aby se uživatelé k účtu přihlásili pouze za účelem přidání položek do nákupního košíku, přiřadíme uživatelům dočasný jedinečný identifikátor (pomocí identifikátoru GUID nebo globálně jedinečného identifikátoru) při přístupu k nákupnímu košíku. Toto ID uložíme pomocí třídy ASP.NET session.

*Poznámka: relace ASP.NET je vhodným místem pro ukládání informací specifických pro uživatele, jejichž platnost vyprší po opuštění lokality. I když by zneužití stavu relace mohlo mít dopad na výkon na větších lokalitách, používá naše světlo dobře funkční pro demonstrační účely.*

Třída ShoppingCart zpřístupňuje následující metody:

**AddToCart** převezme album jako parametr a přidá ho do košíku uživatele. Vzhledem k tomu, že tabulka košíku sleduje množství pro každé album, obsahuje logiku pro vytvoření nového řádku, pokud je to potřeba, nebo jenom zvýšit množství, pokud už si uživatel objednal jednu kopii alba.

**RemoveFromCart** převezme ID alba a odebere ho z košíku uživatele. Pokud má uživatel ve svém košíku jenom jednu kopii alba, řádek se odebere.

**EmptyCart** odebere všechny položky z nákupního košíku uživatele.

**GetCartItems** načte seznam CartItems pro zobrazení nebo zpracování.

**GetCount** načte celkový počet alb, které má uživatel v rámci svého nákupního košíku.

**Gettotal** vypočítá celkové náklady na všechny položky v košíku.

**CreateOrder** převede nákupní košík na objednávku během fáze rezervace.

**Getkošík** je statická metoda, která umožňuje našim řadičům získat objekt košíku. Používá metodu **GetCartId** ke zpracování čtení CartId z uživatelské relace. Metoda GetCartId vyžaduje HttpContextBase, aby mohla číst CartId uživatele z uživatelské relace.

Tady je kompletní **Třída ShoppingCart**:

[!code-csharp[Main](mvc-music-store-part-8/samples/sample5.cs)]

## <a name="viewmodels"></a>ViewModels

Náš řadič nákupního košíku bude muset sdělit některé komplexní informace, které se nemapují čistě na naše objekty modelu. Nechceme upravovat naše modely, abychom mohli přizpůsobit naše zobrazení; Třídy modelu by měly představovat naši doménu, nikoli uživatelské rozhraní. Jedním z řešení by bylo předat informace do našich zobrazení pomocí třídy ViewBag, stejně jako v informacích rozevíracího seznamu Správce úložiště, ale předáním velkého množství informací prostřednictvím ViewBag je obtížné spravovat.

K tomuto řešení slouží vzor *ViewModel* . Při použití tohoto modelu vytvoříme třídy silného typu, které jsou optimalizované pro naše konkrétní scénáře zobrazení a které zveřejňují vlastnosti pro dynamické hodnoty/obsah, které jsou potřebné pro naše šablony zobrazení. Naše třídy kontroleru pak mohou naplnit a předávat tyto třídy optimalizované pro zobrazení do naší šablony zobrazení, která se má použít. To umožňuje v šablonách zobrazení používat technologii IntelliSense pro ověřování, kontrolu doby kompilace a editory.

Vytvoříme dva modely zobrazení pro použití v našem řadiči nákupního košíku: ShoppingCartViewModel bude obsahovat obsah nákupního košíku uživatele a ShoppingCartRemoveViewModel se použije k zobrazení informací o potvrzení, když uživatel nějakou dobu odstraní. z jejich košíku.

Pojďme vytvořit novou složku ViewModels v kořenovém adresáři našeho projektu, abychom zachovali věci uspořádané. Klikněte pravým tlačítkem na projekt, vyberte přidat/nová složka.

![](mvc-music-store-part-8/_static/image1.jpg)

Pojmenujte složku ViewModels.

![](mvc-music-store-part-8/_static/image1.png)

Dále přidejte třídu ShoppingCartViewModel do složky ViewModels. Má dvě vlastnosti: seznam položek košíku a Desítková hodnota pro uchování celkové ceny pro všechny položky v košíku.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample6.cs)]

Nyní přidejte ShoppingCartRemoveViewModel do složky ViewModels s následujícími čtyřmi vlastnostmi.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample7.cs)]

## <a name="the-shopping-cart-controller"></a>Řadič nákupního košíku

Řadič nákupního košíku má tři hlavní účely: Přidání položek do košíku, odebrání položek z košíku a zobrazení položek na vozíku. Využije tři třídy, které jsme právě vytvořili: ShoppingCartViewModel, ShoppingCartRemoveViewModel a ShoppingCart. Stejně jako v případě StoreController a StoreManagerController přidáme pole pro uložení instance MusicStoreEntities.

Přidejte do projektu nový řadič nákupního košíku pomocí prázdné šablony kontroleru.

![](mvc-music-store-part-8/_static/image2.png)

Tady je kompletní kontroler ShoppingCart. Akce index a přidat řadič by měly vypadat velmi dobře. Akce kontroleru odebrat a CartSummary zpracovávají dva zvláštní případy, které probereme v následující části.

[!code-csharp[Main](mvc-music-store-part-8/samples/sample8.cs)]

## <a name="ajax-updates-with-jquery"></a>Aktualizace AJAX pomocí jQuery

Dál vytvoříme stránku indexu nákupního košíku, která se silně zapíše do ShoppingCartViewModel a použije šablonu zobrazení seznamu pomocí stejné metody jako předtím.

![](mvc-music-store-part-8/_static/image3.png)

Ale namísto použití HTML. ActionLink k odebrání položek z košíku použijeme jQuery pro všechny odkazy v tomto zobrazení, které mají třídu HTML RemoveLink, na událost Click. Namísto publikování formuláře tato obslužná rutina události Click provede zpětné volání AJAX na naši akci RemoveFromCart Controller. RemoveFromCart vrátí serializovaný výsledek JSON, který naše zpětné volání jQuery analyzuje a provede čtyři rychlé aktualizace stránky pomocí jQuery:

- 1. Odebere odstraněné album ze seznamu.
- 2. Aktualizuje počet košíků v hlavičce.
- 3. Zobrazí zprávu aktualizace pro uživatele.
- 4. Aktualizuje celkovou cenu za košík.

Vzhledem k tomu, že je scénář odebrání zpracováván pomocí zpětného volání AJAX v rámci zobrazení indexu, nepotřebujeme další pohled na RemoveFromCart akci. Zde je kompletní kód pro zobrazení/ShoppingCart/Index:

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample9.cshtml)]

Aby bylo možné tento test provést, musíme do nákupního košíku přidat položky. Naše zobrazení **podrobností o Storu** aktualizujeme tak, aby obsahovalo tlačítko Přidat do košíku. V tom, že jsme v něm, můžeme přidat další informace o albu, které jsme přidali od poslední aktualizace tohoto zobrazení: Žánr, Interpret, cena a obrázek alba. Aktualizovaný kód zobrazení podrobností úložiště se zobrazí, jak je znázorněno níže.

[!code-cshtml[Main](mvc-music-store-part-8/samples/sample10.cshtml)]

Nyní můžeme kliknout na obchod a testovat přidávání a odebírání alb z a do nákupního košíku. Spusťte aplikaci a přejděte do indexu úložiště.

![](mvc-music-store-part-8/_static/image4.png)

Potom kliknutím na Žánr zobrazíte seznam alb.

![](mvc-music-store-part-8/_static/image5.png)

Po kliknutí na název alba se teď zobrazí naše aktualizované zobrazení podrobností o albu, včetně tlačítka Přidat do košíku.

![](mvc-music-store-part-8/_static/image6.png)

Kliknutím na tlačítko Přidat do košíku se zobrazí zobrazení indexu nákupního košíku v seznamu souhrnu nákupního košíku.

![](mvc-music-store-part-8/_static/image7.png)

Po načtení nákupního košíku můžete kliknutím na odkaz odebrat z košíku Zobrazit aktualizaci AJAX do nákupního košíku.

![](mvc-music-store-part-8/_static/image8.png)

Sestavili jsme pracovní nákupní košík, který umožňuje neregistrovaným uživatelům přidávat položky do košíku. V následující části jim umožníme registrovat a dokončit proces registrace.

> [!div class="step-by-step"]
> [Předchozí](mvc-music-store-part-7.md)
> [Další](mvc-music-store-part-9.md)

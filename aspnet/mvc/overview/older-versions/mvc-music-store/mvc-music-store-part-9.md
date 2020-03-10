---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
title: 'Část 9: registrace a rezervace | Microsoft Docs'
author: jongalloway
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 9 pokrývá registraci a rezervaci.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: d65c5c2b-a039-463f-ad29-25cf9fb7a1ba
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-9
msc.type: authoredcontent
ms.openlocfilehash: 040bc0ccef889fb9a7c3d9b5ce88c75b7b754248
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559533"
---
# <a name="part-9-registration-and-checkout"></a>9\. část: Registrace a pokladna

o [Jan Galloway](https://github.com/jongalloway)

> Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio pro vývoj webů.  
>   
> Úložiště hudby MVC je zjednodušená ukázka implementace úložiště, která prodává hudební alba online a implementuje základní funkce pro správu webů, přihlašování uživatelů a nákupních košíků.  
>   
> V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 9 pokrývá registraci a rezervaci.

V této části vytvoříme CheckoutController, ve kterém se budou shromažďovat informace o adrese a platbách nakupujících. Před rezervací budeme vyžadovat, aby se uživatelé zaregistrovali na našem webu, takže tento kontroler bude vyžadovat autorizaci.

Uživatelé přejdou k procesu rezervace z jeho nákupního košíku kliknutím na tlačítko "rezervovat".

![](mvc-music-store-part-9/_static/image1.jpg)

Pokud uživatel není přihlášený, zobrazí se jim výzva k zadání.

![](mvc-music-store-part-9/_static/image1.png)

Po úspěšném přihlášení se zobrazí uživatel zobrazení adresa a platby.

![](mvc-music-store-part-9/_static/image2.png)

Po vyplnění formuláře a odeslání objednávky se zobrazí obrazovka potvrzení objednávky.

![](mvc-music-store-part-9/_static/image3.png)

Při pokusu o zobrazení neexistující objednávky nebo objednávky, která nepatří do, se zobrazí zobrazení chyb.

![](mvc-music-store-part-9/_static/image4.png)

## <a name="migrating-the-shopping-cart"></a>Migruje se nákupní košík.

I když je nákupní proces anonymní, když uživatel klikne na tlačítko rezervovat, bude se muset zaregistrovat a přihlásit. Uživatelé budou očekávat, že si zachováme informace o nákupních košíkech mezi návštěvami, takže při dokončení registrace nebo přihlášení bude potřeba přidružit informace nákupního košíku k uživateli.

To je vlastně velmi jednoduché, protože naše třída ShoppingCart již má metodu, která bude přidružit všechny položky v aktuálním vozíku k uživatelskému jménu. Tuto metodu budeme muset volat, až uživatel dokončí registraci nebo přihlášení.

Otevřete třídu **AccountController** , kterou jsme přidali, když jsme nastavili členství a autorizaci. Přidejte příkaz using odkazující na MvcMusicStore. Models a pak přidejte následující metodu MigrateShoppingCart:

[!code-csharp[Main](mvc-music-store-part-9/samples/sample1.cs)]

V dalším kroku změňte akci po ověření přihlašovacího příspěvku tak, aby se MigrateShoppingCart volala po ověření uživatele, jak je znázorněno níže:

[!code-csharp[Main](mvc-music-store-part-9/samples/sample2.cs)]

Proveďte stejnou změnu akce registrovat po, ihned po úspěšném vytvoření uživatelského účtu:

[!code-csharp[Main](mvc-music-store-part-9/samples/sample3.cs)]

To je teď – anonymní nákupní košík se po úspěšné registraci nebo přihlášení automaticky přenese na uživatelský účet.

## <a name="creating-the-checkoutcontroller"></a>Vytváření CheckoutController

Klikněte pravým tlačítkem na složku Controllers a přidejte do projektu s názvem CheckoutController nový kontroler pomocí prázdné šablony kontroleru.

![](mvc-music-store-part-9/_static/image5.png)

Nejdřív přidejte atribut autorizovat nad deklaraci třídy kontroleru, aby se před rezervací vyžadovaly, aby se uživatelé zaregistrovali:

[!code-csharp[Main](mvc-music-store-part-9/samples/sample4.cs)]

*Poznámka: Tato změna se podobá StoreManagerController, ale v takovém případě atribut autorizovat vyžaduje, aby uživatel byl v roli správce. V kontroleru rezervací vyžadujeme, aby byl uživatel přihlášený, ale nevyžadoval, aby byli správci.*

V zájmu jednoduchosti se v tomto kurzu nebudeme zabývat informacemi o platbách. Místo toho umožňujíme uživatelům rezervovat kód propagačního kódu. Tento kód propagačního kódu budeme uchovávat pomocí konstanty s názvem PromoCode.

Jak je uvedeno v StoreController, deklarujeme pole pro uložení instance třídy MusicStoreEntities s názvem storeDB. Aby bylo možné používat třídu MusicStoreEntities, je nutné přidat příkaz using pro obor názvů MvcMusicStore. Models. V horní části našeho kontroleru registrace se zobrazí níže.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample5.cs)]

CheckoutController bude mít následující akce kontroleru:

**AddressAndPayment (Get Method)** zobrazí formulář, který uživateli umožní zadat jejich informace.

**AddressAndPayment (post metoda)** ověří zadání a zpracuje objednávku.

Po úspěšném dokončení procesu registrace se zobrazí **dokončeno** . Toto zobrazení bude obsahovat číslo objednávky uživatele jako potvrzení.

Nejprve přejmenujte akci řadiče indexu (která byla generována při vytvoření kontroleru) do AddressAndPayment. Tato akce kontroleru jenom zobrazí formulář pro registraci, takže nevyžaduje žádné informace o modelu.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample6.cs)]

Metoda AddressAndPayment POST se bude řídit stejným vzorem, který jsme použili v StoreManagerController: bude se pokusit přijmout odeslání formuláře a dokončit objednávku a formulář bude znovu zobrazen, pokud selže.

Po ověření, že vstup na formuláři splňuje naše požadavky na ověření pro objednávku, zkontrolujeme přímo hodnotu formuláře PromoCode. Za předpokladu, že všechno je správné, uložíme aktualizované informace s objednávkou, poznáte objekt ShoppingCart, aby se dokončil proces pořadí, a přesměruje na akci dokončení.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample7.cs)]

Po úspěšném dokončení procesu registrace budou uživatelé přesměrováni na dokončení akce kontroleru. Tato akce provede jednoduchou kontrolu za účelem ověření, že objednávka skutečně patří přihlášenému uživateli před zobrazením čísla objednávky jako potvrzení.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample8.cs)]

*Poznámka: ve složce/Views/Shared se při zahájení projektu automaticky vytvořilo zobrazení chyby pro nás.*

Úplný kód CheckoutController je následující:

[!code-csharp[Main](mvc-music-store-part-9/samples/sample9.cs)]

## <a name="adding-the-addressandpayment-view"></a>Přidání zobrazení AddressAndPayment

Nyní vytvoříme zobrazení AddressAndPayment. Klikněte pravým tlačítkem myši na jednu z akcí AddressAndPayment Controller a přidejte zobrazení s názvem AddressAndPayment, které je silně typované jako objednávka a používá úpravu šablony, jak je znázorněno níže.

![](mvc-music-store-part-9/_static/image6.png)

Toto zobrazení využívá dva techniky, které jsme prohlédli při sestavování zobrazení StoreManagerEdit:

- K zobrazení polí formuláře pro model objednávky použijeme HTML. EditorForModel ().
- Použijeme pravidla ověřování s použitím třídy Order s atributy ověřování.

Začneme aktualizací kódu formuláře tak, aby používal HTML. EditorForModel () následovaný dalším textovým polem pro propagační kód. Úplný kód pro zobrazení AddressAndPayment je uveden níže.

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample10.cshtml)]

## <a name="defining-validation-rules-for-the-order"></a>Definování ověřovacích pravidel pro objednávku

Teď, když je naše zobrazení nastavené, nastavíme pro model objednávky pravidla ověřování, která jsme předtím používali pro model alba. Klikněte pravým tlačítkem na složku modely a přidejte třídu s názvem Order. Kromě ověřovacích atributů, které jsme pro album používali dřív, použijeme k ověření e-mailové adresy uživatele regulární výraz.

[!code-csharp[Main](mvc-music-store-part-9/samples/sample11.cs)]

Při pokusu o odeslání formuláře s chybějícími nebo neplatnými informacemi se nyní zobrazí chybová zpráva s použitím ověřování na straně klienta.

![](mvc-music-store-part-9/_static/image7.png)

V pořádku jsme dokončili většinu pevné práce pro proces registrace; jenom pár lichá a končí na dokončení. Musíme přidat dvě jednoduchá zobrazení a musíme se postarat o předání informací o košíku během procesu přihlášení.

## <a name="adding-the-checkout-complete-view"></a>Přidání zobrazení dokončené rezervace

Zobrazení dokončené rezervace je poměrně jednoduché, protože stačí zobrazit ID objednávky. Klikněte pravým tlačítkem na akci dokončit kontroler a přidejte zobrazení s názvem dokončeno, které je silně typované jako celé číslo.

![](mvc-music-store-part-9/_static/image8.png)

Nyní aktualizujeme kód zobrazení, aby se zobrazilo ID objednávky, jak je znázorněno níže.

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample12.cshtml)]

## <a name="updating-the-error-view"></a>Aktualizace zobrazení chyb

Výchozí šablona obsahuje zobrazení chyb ve složce sdílené zobrazení, aby ji bylo možné znovu použít jinde v lokalitě. Toto zobrazení chyb obsahuje velmi jednoduchou chybu a nepoužívá rozložení webu, takže ji aktualizujeme.

Vzhledem k tomu, že se jedná o obecnou chybovou stránku, je obsah velmi jednoduchý. Pokud chce uživatel opakovat akci, bude obsahovat zprávu a odkaz pro přechod na předchozí stránku v historii.

[!code-cshtml[Main](mvc-music-store-part-9/samples/sample13.cshtml)]

> [!div class="step-by-step"]
> [Předchozí](mvc-music-store-part-8.md)
> [Další](mvc-music-store-part-10.md)

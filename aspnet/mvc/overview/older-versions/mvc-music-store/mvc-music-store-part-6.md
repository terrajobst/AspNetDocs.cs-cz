---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
title: '6\. část: použití datových poznámek pro ověření modelu | Microsoft Docs'
author: jongalloway
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 6 pokrývá použití datových poznámek pro model V...
ms.author: riande
ms.date: 04/21/2011
ms.assetid: b3193d33-2d0b-4d98-9712-58bd897c62ec
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-6
msc.type: authoredcontent
ms.openlocfilehash: bc031dd5be61cc6707c522f85f6af77a420c8b31
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539275"
---
# <a name="part-6-using-data-annotations-for-model-validation"></a>6\. část: Používání datových poznámek k ověření modelu

o [Jan Galloway](https://github.com/jongalloway)

> Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio pro vývoj webů.  
>   
> Úložiště hudby MVC je zjednodušená ukázka implementace úložiště, která prodává hudební alba online a implementuje základní funkce pro správu webů, přihlašování uživatelů a nákupních košíků.  
>   
> V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 6 pokrývá použití datových poznámek pro ověřování modelu.

Máme velký problém s našimi formuláři pro vytváření a úpravy: neprovádí žádné ověření. Můžeme dělat věci, jako je třeba ponechat povinná pole prázdná, nebo zadat písmena v poli Price a první chyba, kterou uvidíme z databáze.

Do naší aplikace můžeme snadno přidat ověřování tím, že do našich tříd modelů přidáte datové poznámky. Poznámky k datům nám umožňují popsat pravidla, která chceme použít pro vlastnosti modelu, a ASP.NET MVC se postará o vynucování a zobrazování vhodných zpráv pro naše uživatele.

## <a name="adding-validation-to-our-album-forms"></a>Přidání ověřování do našich formulářů alba

Použijeme následující atributy poznámky k datům:

- **Required** – označuje, že vlastnost je povinné pole.
- **DisplayName** – definuje text, který chceme použít pro pole formuláře a ověřovací zprávy.
- **StringLength** – definuje maximální délku pole řetězce.
- **Rozsah** – poskytuje maximální a minimální hodnotu pro číselné pole.
- **BIND** – vypíše pole, která se mají vyloučit nebo zahrnout, když jsou parametry vazby nebo hodnoty formulářů na vlastnosti modelu.
- **ScaffoldColumn** – umožňuje skrývání polí z formulářů editoru.

*Poznámka: Další informace o ověřování modelu pomocí atributů datových poznámek najdete v dokumentaci MSDN na adrese* [`https://go.microsoft.com/fwlink/?LinkId=159063`](https://go.microsoft.com/fwlink/?LinkId=159063)

Otevřete třídu alba a přidejte následující příkazy *using* do horní části.

[!code-csharp[Main](mvc-music-store-part-6/samples/sample1.cs)]

Dále aktualizujte vlastnosti tak, aby se přidaly atributy zobrazení a ověření, jak je vidět níže.

[!code-csharp[Main](mvc-music-store-part-6/samples/sample2.cs)]

I když tam máme, změnili jsme také Žánr a umělec na virtuální vlastnosti. To umožňuje Entity Framework opožděně načítat je podle potřeby.

[!code-csharp[Main](mvc-music-store-part-6/samples/sample3.cs)]

Po přidání těchto atributů do našeho modelu alba si naše obrazovka pro vytvoření a úpravu hned spustí ověřování polí a použití zobrazovaných názvů, které jsme zvolili (např. adresa URL alba alba místo AlbumArtUrl). Spusťte aplikaci a přejděte do/StoreManager/Create.

![](mvc-music-store-part-6/_static/image1.png)

Dále porušíme některá pravidla ověřování. Zadejte cenu 0 a nechejte název prázdný. Po kliknutí na tlačítko vytvořit se zobrazí formulář s chybovými zprávami ověřování, které zobrazují, která pole nesplňovala vámi definovaná pravidla ověřování.

![](mvc-music-store-part-6/_static/image2.png)

## <a name="testing-the-client-side-validation"></a>Testování ověřování na straně klienta

Ověřování na straně serveru je velmi důležité z hlediska aplikace, protože uživatelé mohou obejít ověřování na straně klienta. Formuláře webové stránky, které implementují pouze ověřování na straně serveru, však projeví tři významné problémy.

1. Uživatel musí počkat na publikování formuláře, jeho ověření na serveru a odeslání odpovědi do prohlížeče.
2. Uživatel nezíská okamžitou zpětnou vazbu, když opraví pole tak, aby nyní prošl pravidla ověřování.
3. Nepotřebujeme k provádění logiky ověřování místo využití prohlížeče uživatele prostředky serveru.

Naštěstí šablony uživatelského rozhraní ASP.NET MVC 3 obsahují integrované ověřování na straně klienta, které nevyžadují žádnou další práci.

Zadáním jednoho písmena v poli název splníte požadavky na ověření, takže se ověřovací zpráva okamžitě odebere.

![](mvc-music-store-part-6/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](mvc-music-store-part-5.md)
> [Další](mvc-music-store-part-7.md)

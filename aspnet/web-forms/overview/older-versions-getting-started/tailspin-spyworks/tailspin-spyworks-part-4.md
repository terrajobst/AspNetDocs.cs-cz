---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
title: '4\. část: seznam produktů | Microsoft Docs'
author: JoeStagner
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 4 pokrývá výpis produktů pomocí ovládacího prvku GridView...
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 4fab47d5-a6ec-4fdc-91f0-651a093a24b9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-4
msc.type: authoredcontent
ms.openlocfilehash: 7af1b8afa2ecc8df9846f2edd2091b26b93a811c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78566981"
---
# <a name="part-4-listing-products"></a>4\. část: Seznam produktů

[Jana Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks ukazuje, jak neobyčejně jednoduché je vytvářet výkonné a škálovatelné aplikace pro platformu .NET. Ukazuje, jak používat Skvělé nové funkce v ASP.NET 4 k vytvoření online obchodu, včetně nákupu, rezervace a správy.
> 
> V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 4 pokrývá výpis produktů pomocí ovládacího prvku GridView.

## <a id="_Toc260221670"></a>Výpis produktů pomocí ovládacího prvku GridView

Pojďme začít s implementací naší stránky ProductsList. aspx tím, že kliknete pravým tlačítkem na naše řešení a vyberete Přidat a nová položka.

![](tailspin-spyworks-part-4/_static/image1.jpg)

Vyberte možnost webový formulář pomocí stránky předlohy a zadejte název stránky ProductsList. aspx.

Klikněte na tlačítko Přidat.

![](tailspin-spyworks-part-4/_static/image2.jpg)

Dále zvolte složku "Styles" (styly), kde jsme umístili stránku Web. Master a vyberte ji v okně "obsah složky".

![](tailspin-spyworks-part-4/_static/image3.jpg)

Stránku vytvoříte kliknutím na OK.

Naše databáze je naplněná daty produktu, jak vidíte níže.

![](tailspin-spyworks-part-4/_static/image4.jpg)

Po vytvoření naší stránky znovu použijeme zdroj dat entity pro přístup k datům produktu, ale v této instanci musíme vybrat entity produktů a musíme omezit vrácené položky jenom na ty, které jsou pro vybranou kategorii vracené.

Abychom to mohli udělat, řekne EntityDataSource, aby automaticky vygeneroval klauzuli WHERE, a my určíme WhereParameter.

Odvoláte to, když jsme vytvořili položky nabídky v naší "nabídce kategorie produktu", dynamicky jsme vytvořili propojení přidáním KódKategorie do řetězce dotazu pro každé propojení. Zdroj dat entity sdělíme, aby se odvodil parametr WHERE z tohoto parametru QueryString.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample1.aspx)]

Dále nakonfigurujeme ovládací prvek ListView pro zobrazení seznamu produktů. Pro vytvoření optimálního prostředí pro nákupy zkomprimujeme několik stručných funkcí do každého jednotlivého produktu zobrazeného v našem ListVew.

- Název produktu bude odkaz na detailní zobrazení produktu.
- Zobrazí se cena za produkt.
- Zobrazí se obrázek produktu a dynamicky se vybere obrázek z adresáře imagí katalogu v naší aplikaci.
- Budeme zahrnovat odkaz na okamžité přidání konkrétního produktu do nákupního košíku.

Zde je značka pro naši instanci ovládacího prvku ListView.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample2.aspx)]

Dynamicky vytváříme několik odkazů na každý zobrazený produkt.

Před testováním vlastní nové stránky taky musíme vytvořit adresářovou strukturu pro Image katalogu produktů následujícím způsobem.

![](tailspin-spyworks-part-4/_static/image1.png)

Jakmile budou k dispozici naše image produktů, můžeme otestovat stránku seznam produktů.

![](tailspin-spyworks-part-4/_static/image5.jpg)

Na domovské stránce webu klikněte na jeden z odkazů seznamu kategorií.

![](tailspin-spyworks-part-4/_static/image6.jpg)

Nyní musíme implementovat stránku ProductDetails. aspx a funkci AddToCart.

Pomocí&gt;souboru New vytvořte stránku s názvem ProductDetails. aspx pomocí stránky předlohy webu, kterou jste předtím používali.

Znovu použijeme ovládací prvek EntityDataSource pro přístup k určitému záznamu produktu v databázi a my použijeme ovládací prvek ASP.NET FormView k zobrazení dat produktu následujícím způsobem.

[!code-aspx[Main](tailspin-spyworks-part-4/samples/sample3.aspx)]

Nedělejte si starosti, pokud formátování vypadá za bitovou Funny. Výše uvedený kód ponechá místo v rozložení zobrazení pro několik funkcí, které budeme implementovat později.

Nákupní košík bude v naší aplikaci představovat složitější logiku. Chcete-li začít, použijte&gt;soubor New k vytvoření stránky s názvem MyShoppingCart. aspx.

Všimněte si, že nepoužíváme název ShoppingCart. aspx.

Naše databáze obsahuje tabulku s názvem "ShoppingCart". Když jsme vygenerovali model EDM (Entity Data Model) pro každou tabulku v databázi se vytvořila třída. Proto model EDM (Entity Data Model) vygeneroval třídu entity s názvem "ShoppingCart". Mohli jsme model upravit, abychom mohli použít tento název pro implementaci nákupních košíků nebo ho pro naše potřeby využít, ale místo toho je možné jednoduše vybrat název, který se tomuto konfliktu vyhne.

Také je potřeba poznamenat, že vytvoříme jednoduchý nákupní košík a vložíte logiku nákupního košíku se zobrazením nákupního košíku. Můžeme se také rozhodnout implementovat si nákupní košík v zcela oddělené obchodní vrstvě.

> [!div class="step-by-step"]
> [Předchozí](tailspin-spyworks-part-3.md)
> [Další](tailspin-spyworks-part-5.md)

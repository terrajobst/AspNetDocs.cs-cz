---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
title: 'Část 3: nabídka rozložení a kategorie | Microsoft Docs'
author: JoeStagner
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 3 pokrývá přidání rozložení a nabídky kategorie.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 94ea1a70-a9bc-4241-8f36-08366d64bab9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-3
msc.type: authoredcontent
ms.openlocfilehash: a223b97fd362ecf73ecde431e141021c1dcc6a6d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639116"
---
# <a name="part-3-layout-and-category-menu"></a>3\. část: Nabídka Rozložení a Kategorie

[Jana Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks ukazuje, jak neobyčejně jednoduché je vytvářet výkonné a škálovatelné aplikace pro platformu .NET. Ukazuje, jak používat Skvělé nové funkce v ASP.NET 4 k vytvoření online obchodu, včetně nákupu, rezervace a správy.
> 
> V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 3 pokrývá přidání rozložení a nabídky kategorie.

## <a id="_Toc260221669"></a>Přidání některých rozložení a nabídky kategorie

Na naší stránce předlohy webu přidáte div pro sloupec vlevo, který bude obsahovat nabídku kategorie produktu.

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample1.aspx)]

Všimněte si, že požadované zarovnání a další formátování poskytne Třída CSS, kterou jsme přidali do našeho souboru Style. CSS.

[!code-css[Main](tailspin-spyworks-part-3/samples/sample2.css)]

Nabídka Produktová kategorie se vytvoří dynamicky za běhu a provede dotazování databáze Commerce na existující kategorie produktů a vytvoření položek nabídky a odpovídajících odkazů.

K tomuto účelu použijeme dvě stránky ASP. NETTO výkonné ovládací prvky pro data. Ovládací prvek zdroje dat entity a ovládací prvek ListView.

![](tailspin-spyworks-part-3/_static/image1.jpg)

Pojďme přepnout na zobrazení Návrh a pomocí pomocníků nakonfigurovat naše ovládací prvky.

![](tailspin-spyworks-part-3/_static/image2.jpg)

Nastavíme vlastnost ID EntityDataSource na možnost EDS\_kategorii\_a kliknete na Konfigurovat zdroj dat.

![](tailspin-spyworks-part-3/_static/image3.jpg)

Vyberte připojení CommerceEntities, které jste vytvořili pro nás, když jsme vytvořili model zdroje dat entity pro naši obchodní databázi a kliknete na další.

![](tailspin-spyworks-part-3/_static/image4.jpg)

Vyberte název sady entit "kategorie" a ponechte ostatní možnosti jako výchozí. Klikněte na tlačítko Dokončit.

Nyní nastavíme vlastnost ID instance ovládacího prvku ListView, kterou jsme umístili na naši stránku, na ListView\_ProductsMenu a aktivujete její pomoc.

![](tailspin-spyworks-part-3/_static/image5.jpg)

I když bychom mohli použít možnosti ovládacího prvku k formátování zobrazení a formátování datových položek, vytváření naší nabídky bude vyžadovat pouze jednoduché označení, takže budeme kód zadávat v zobrazení zdroje.

[!code-aspx[Main](tailspin-spyworks-part-3/samples/sample3.aspx)]

Poznamenejte si prosím příkaz Eval: &lt;% # Eval ("CategoryName")%&gt;

Syntaxe ASP.NET &lt;% #%&gt; je zjednodušená konvence, která řídí modulu runtime, aby běžela bez ohledu na to, zda je obsažena v rámci výstupu, a výstupem výsledků "na řádku".

Vyhodnocení příkazu ("CategoryName") dává pokyn, aby pro aktuální položku v vázané kolekci datových položek načetla hodnotu názvů položek modelu entity "CategoryName". Toto je Stručná syntaxe pro velmi výkonnou funkci.

Umožňuje aplikaci spustit nyní.

![](tailspin-spyworks-part-3/_static/image6.jpg)

Všimněte si, že se teď zobrazuje naše nabídka kategorie produktů, a když najedete myší na jednu z položek nabídky kategorie, můžeme odkazy na položky nabídky odkazovat na stránku, kterou jsme ještě vytvořili s názvem ProductsList. aspx a že jsme vytvořili argument dynamického řetězce dotazu, který obsahuje  ID kategorie

> [!div class="step-by-step"]
> [Předchozí](tailspin-spyworks-part-2.md)
> [Další](tailspin-spyworks-part-4.md)

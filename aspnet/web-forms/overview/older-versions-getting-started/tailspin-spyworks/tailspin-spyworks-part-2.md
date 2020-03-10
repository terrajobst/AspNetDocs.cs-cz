---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: 'Část 2: Vrstva přístupu k datům | Microsoft Docs'
author: JoeStagner
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 2 pokrývá přidání vrstvy přístupu k datům.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 342d2c54dfba5d052570e890f85dcf9739f9884f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78573246"
---
# <a name="part-2-data-access-layer"></a>2\. část: Vrstva přístupu k datům

[Jana Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks ukazuje, jak neobyčejně jednoduché je vytvářet výkonné a škálovatelné aplikace pro platformu .NET. Ukazuje, jak používat Skvělé nové funkce v ASP.NET 4 k vytvoření online obchodu, včetně nákupu, rezervace a správy.
> 
> V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace Tailspin Spyworks. Část 2 pokrývá přidání vrstvy přístupu k datům.

## <a id="_Toc260221668"></a>Přidání vrstvy přístupu k datům

Naše aplikace elektronického obchodování bude záviset na dvou databázích.

Pro informace o zákaznících budeme používat standardní databázi členství v ASP.NET. Pro náš nákupní košík a katalog produktů implementujeme databázi SQL Express následujícím způsobem.

![](tailspin-spyworks-part-2/_static/image1.jpg)

Když jste vytvořili databázi (obchod. mdf) v aplikační složce\_aplikace, můžeme pokračovat v vytváření naší vrstvy přístupu k datům pomocí Entity Framework .NET.

Vytvoříme složku s názvem "přístup k datům\_" a na tuto složku kliknete pravým tlačítkem a vyberete Přidat novou položku.

V položce "nainstalované šablony" a potom vyberte "ADO.NET model EDM (Entity Data Model)" zadejte EDM\_Commerce. edmx jako název a klikněte na tlačítko Přidat.

![](tailspin-spyworks-part-2/_static/image2.jpg)

Vyberte možnost generovat z databáze.

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

Uložte a sestavte.

Teď jsme připraveni přidat naši první funkci – nabídku kategorie produktu.

> [!div class="step-by-step"]
> [Předchozí](tailspin-spyworks-part-1.md)
> [Další](tailspin-spyworks-part-3.md)

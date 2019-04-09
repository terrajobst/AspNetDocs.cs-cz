---
uid: web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
title: 'Část 2: Vrstva přístupu k datům | Dokumentace Microsoftu'
author: JoeStagner
description: V této sérii kurzů podrobně popisuje všechny kroky k vytvoření ukázkové aplikace Tailspin Spyworks. 2. část se věnuje přidání vrstvy přístupu k datům.
ms.author: riande
ms.date: 07/21/2010
ms.assetid: 5a9d5429-d70b-411c-8474-f42cf7ef8a2b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-2
msc.type: authoredcontent
ms.openlocfilehash: 3fbc6fe4d94534a038a81532b3cd8ca30ddf9b11
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2019
ms.locfileid: "59378383"
---
# <a name="part-2-data-access-layer"></a>Část 2: Vrstva přístupu k datům

podle [Joe Stagner](https://github.com/JoeStagner)

> Tailspin Spyworks ukazuje, jak mimořádně jednoduché je vytvářet výkonné a škálovatelné aplikace pro platformu .NET. Zobrazuje vypnout použití skvělých nových funkcí v technologii ASP.NET 4 k sestavení nebo online úložiště, včetně nákupu, Pokladna a správu.
> 
> V této sérii kurzů podrobně popisuje všechny kroky k vytvoření ukázkové aplikace Tailspin Spyworks. 2. část se věnuje přidání vrstvy přístupu k datům.


## <a id="_Toc260221668"></a>  Přidání vrstvy přístupu k datům

Naši aplikaci elektronického obchodování, bude záviset na dvě databáze.

Informace o zákaznících použijeme standardní databáze členství technologie ASP.NET. Pro náš katalog nákupního košíku a produktu jsme budete následujícím způsobem implementace databáze SQL Express.

![](tailspin-spyworks-part-2/_static/image1.jpg)

Databáze (Commerce.mdf) máte vytvořený v aplikaci aplikace\_složka dat je možné přejít k vytvoření naší vrstvy přístupu k datům pomocí Entity Frameworku .NET.

Vytvoříme složku s názvem "Data\_přístup" a je v této složce klikněte pravým tlačítkem myši a vyberte "Přidat novou položku".

"Nainstalované šablony" položky a pak vyberte "ADO.NET Entity Data Model" Zadejte EDM\_Commerce.edmx jako název a klikněte na tlačítko "Přidat".

![](tailspin-spyworks-part-2/_static/image2.jpg)

Zvolte možnost "Generovat z databáze".

![](tailspin-spyworks-part-2/_static/image1.png)

![](tailspin-spyworks-part-2/_static/image2.png)

![](tailspin-spyworks-part-2/_static/image3.png)

![](tailspin-spyworks-part-2/_static/image3.jpg)

Uložit a sestavit.

Nyní jsme připraveni pro přidání naši první funkci – nabídky kategorie produktu.

> [!div class="step-by-step"]
> [Předchozí](tailspin-spyworks-part-1.md)
> [další](tailspin-spyworks-part-3.md)

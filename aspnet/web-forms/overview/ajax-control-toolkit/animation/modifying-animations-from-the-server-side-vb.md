---
uid: web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
title: Úprava animací ze strany serveru (VB) | Microsoft Docs
author: wenz
description: Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Animace také mohou...
ms.author: riande
ms.date: 06/02/2008
ms.assetid: addcf4aa-340a-460b-9c64-506424a1f725
msc.legacyurl: /web-forms/overview/ajax-control-toolkit/animation/modifying-animations-from-the-server-side-vb
msc.type: authoredcontent
ms.openlocfilehash: ebc311d1a931ad611d9556799c94440d41a9cf49
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78597998"
---
# <a name="modifying-animations-from-the-server-side-vb"></a>Změna animací ze strany serveru (VB)

od [Christian Wenz](https://github.com/wenz)

[Stažení kódu](https://download.microsoft.com/download/f/9/a/f9a26acd-8df4-4484-8a18-199e4598f411/Animation9.vb.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/7/1/6718d452-ff89-4d3f-a90e-c74ec2d636a3/animation9VB.pdf)

> Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Animace se taky můžou změnit na straně serveru.

## <a name="overview"></a>Přehled

Ovládací prvek animace v ovládacím prvku ASP.NET AJAX Control Toolkit není pouze ovládací prvek, ale celá rozhraní pro přidání animací do ovládacího prvku. Animace se taky můžou změnit na straně serveru.

## <a name="steps"></a>Kroky

Nejprve do stránky zahrňte `ScriptManager`. pak je načtena knihovna ASP.NET AJAX, která umožňuje používat sadu nástrojů Control Toolkit:

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample1.aspx)]

Animace se použije na panel textu, který vypadá takto:

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample2.aspx)]

V přidružené třídě CSS pro panel definujte Skvělé barvy pozadí a také nastavte pevnou šířku panelu:

[!code-css[Main](modifying-animations-from-the-server-side-vb/samples/sample3.css)]

Zbytek kódu se spouští na straně serveru a nepoužívá značky; místo toho používá kód k vytvoření `AnimationExtender`ho ovládacího prvku:

[!code-aspx[Main](modifying-animations-from-the-server-side-vb/samples/sample4.aspx)]

Sada Control Toolkit ale v současné době neposkytuje přístup rozhraní API k vytváření jednotlivých animací. Je však možné nastavit vlastnost animací `AnimationExtender`na řetězec obsahující značku XML použitou při deklarativním přiřazení animací. Chcete-li vytvořit XML, které nesmí obsahovat prvek `<Animations>` můžete použít podporu XML .NET Framework nebo, jak je uvedeno v následujícím kódu, pouze zadat řetězec:

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample5.vb)]

Nakonec přidejte ovládací prvek `AnimationExtender` do aktuální stránky v rámci `<form runat="server">` elementu a ujistěte se, že je animace zahrnutá a spuštěná:

[!code-vb[Main](modifying-animations-from-the-server-side-vb/samples/sample6.vb)]

[![je animace vytvořena pomocí kódu/VB na straně C#serveru](modifying-animations-from-the-server-side-vb/_static/image2.png)](modifying-animations-from-the-server-side-vb/_static/image1.png)

Animace je vytvořena pomocí/vb kódu na straně C#serveru ([kliknutím zobrazíte obrázek v plné velikosti).](modifying-animations-from-the-server-side-vb/_static/image3.png)

> [!div class="step-by-step"]
> [Předchozí](triggering-an-animation-in-another-control-vb.md)
> [Další](executing-animations-using-client-side-code-vb.md)

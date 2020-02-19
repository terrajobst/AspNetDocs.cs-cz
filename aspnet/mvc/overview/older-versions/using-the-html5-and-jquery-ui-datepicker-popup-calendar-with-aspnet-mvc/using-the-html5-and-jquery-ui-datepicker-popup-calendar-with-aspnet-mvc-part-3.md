---
uid: mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
title: Použití místního kalendáře DatePicker HTML5 a jQuery UI s ASP.NET MVC – část 3 | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy práce s šablonami editoru, šablonami zobrazení a místním datepickerm ovládacího prvku jQuery uživatelského rozhraní v ASP.NET MV...
ms.author: riande
ms.date: 08/29/2011
ms.assetid: 8f5f91ae-12d7-4cf3-ac09-4bb53d07ee60
msc.legacyurl: /mvc/overview/older-versions/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc/using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3
msc.type: authoredcontent
ms.openlocfilehash: b3249397e54e64538c4dc78e5fe8b94656e8962b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457892"
---
# <a name="using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc---part-3"></a>Použití místního kalendáře DatePicker HTML5 a jQuery UI s ASP.NET MVC – část 3

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> V tomto kurzu se seznámíte se základy práce s šablonami editoru, šablonami zobrazení a místním datepickerm ovládacího prvku jQuery uživatelského rozhraní ve webové aplikaci ASP.NET MVC.

## <a name="working-with-complex-types"></a>Práce se složitými typy

V této části vytvoříte třídu adres a naučíte se, jak vytvořit šablonu pro její zobrazení.

Ve složce *modely* vytvořte nový soubor třídy s názvem *Person.cs* , kam umístíte dva typy: třídu `Person` a třídu `Address`. Třída `Person` bude obsahovat vlastnost, která je zadána jako `Address`. Typ `Address` je komplexní typ, což znamená, že se nejedná o jeden z předdefinovaných typů jako `int`, `string`nebo `double`. Místo toho má několik vlastností. Kód pro nové třídy vypadá takto:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample1.cs)]

V kontroleru `Movie` přidejte následující akci `PersonDetail` k zobrazení instance osoby:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample2.cs)]

Pak přidejte následující kód do kontroleru `Movie` k naplnění modelu `Person` pomocí některých ukázkových dat:

[!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample3.cs)]

Otevřete soubor *Views\Movies\PersonDetail.cshtml* a přidejte následující kód pro zobrazení `PersonDetail`.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample4.cshtml)]

Stisknutím kombinace kláves CTRL + F5 spusťte aplikaci a přejděte na *video/PersonDetail*.

Zobrazení `PersonDetail` neobsahuje komplexní typ `Address`, jak vidíte na tomto snímku obrazovky. (Není zobrazena žádná adresa.)

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image1.png)

Data modelu `Address` nejsou zobrazena, protože se jedná o komplexní typ. Chcete-li zobrazit informace o adrese, otevřete znovu soubor *Views\Movies\PersonDetail.cshtml* a přidejte následující kód.

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample5.cshtml)]

Úplný kód pro zobrazení `PersonDetail` nyní vypadá takto:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample6.cshtml)]

Spusťte aplikaci znovu a zobrazte `PersonDetail` zobrazení. Zobrazí se nyní informace o adrese:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image2.png)

### <a name="creating-a-template-for-a-complex-type"></a>Vytvoření šablony pro komplexní typ

V této části vytvoříte šablonu, která bude použita k vykreslení `Address` komplexního typu. Když vytvoříte šablonu pro typ `Address`, ASP.NET MVC ji může automaticky použít k formátování modelu adresy kdekoli v aplikaci. To poskytuje způsob, jak řídit vykreslování `Address`ho typu z jediného místa v aplikaci.

Ve složce *Views\Shared\DisplayTemplates* vytvořte s názvem **adresa**částečného zobrazení se silným typem:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image3.png)

Klikněte na **Přidat**a pak otevřete nový soubor *Views\Shared\DisplayTemplates\Address.cshtml* . Nové zobrazení obsahuje následující generovaný kód:

[!code-cshtml[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample7.cshtml)]

Spusťte aplikaci a zobrazte `PersonDetail` zobrazení. Tentokrát `Address` šablona, kterou jste právě vytvořili, slouží k zobrazení `Address` komplexního typu, takže zobrazení vypadá takto:

![](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/_static/image4.png)

### <a name="summary-ways-to-specify-the-model-display-format-and-template"></a>Shrnutí: způsoby určení formátu a šablony zobrazení modelu

Viděli jste, že můžete zadat formát nebo šablonu pro vlastnost modelu pomocí následujících přístupů:

- Použití atributu `DisplayFormat` na vlastnost v modelu. Například následující kód způsobí, že se datum zobrazí bez času:

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample8.cs)]
- Použití atributu [DataType](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.datatype.aspx) na vlastnost v modelu a určení datového typu. Například následující kód způsobí, že se datum zobrazí bez času.

    [!code-csharp[Main](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-3/samples/sample9.cs)]

    Pokud aplikace obsahuje šablonu *Date. cshtml* ve složce *Views\Shared\DisplayTemplates* nebo ve složce *Views\Movies\DisplayTemplates* , bude tato šablona použita k vykreslení vlastnosti `DateTime`. Jinak integrovaný systém ASP.NET šablonování zobrazí vlastnost jako datum.
- Vytvoření šablony zobrazení ve složce *Views\Shared\DisplayTemplates* nebo ve složce *Views\Movies\DisplayTemplates* , jejíž název se shoduje s datovým typem, který chcete formátovat. Například jste viděli, že *Views\Shared\DisplayTemplates\DateTime.cshtml* byl použit k vykreslení vlastností `DateTime` v modelu, bez přidání atributu do modelu a bez přidání kódu do zobrazení.
- Pomocí atributu [UIHint](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.uihintattribute.uihint.aspx) v modelu zadejte šablonu pro zobrazení vlastnosti modelu.
- Explicitně přidejte název šablony zobrazení do volání [HTML. DisplayFor](https://msdn.microsoft.com/library/ee407420.aspx) v zobrazení.

Přístup, který použijete, závisí na tom, co musíte udělat ve své aplikaci. Ke smíchání těchto přístupů není Neběžné, abyste získali přesně takový druh formátování, které potřebujete.

V další části převedete ozubené kolečky a přejdete z přizpůsobení způsobu, jakým se zobrazí data pro přizpůsobení způsobu jejich zadávání. DatePicker jQuery se připojíte k zobrazením pro úpravy v aplikaci, aby bylo možné zadat data uhlazený způsobem.

> [!div class="step-by-step"]
> [Předchozí](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-2.md)
> [Další](using-the-html5-and-jquery-ui-datepicker-popup-calendar-with-aspnet-mvc-part-4.md)

---
uid: mvc/overview/older-versions-1/models-data/performing-simple-validation-cs
title: Provádění jednoduchého ověřováníC#() | Microsoft Docs
author: StephenWalther
description: Naučte se provádět ověřování v aplikaci ASP.NET MVC. V tomto kurzu vás Stephen Walther seznámí se stavem modelu a pomocníkem pro ověřování HTML...
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 21383c9d-6aea-4bad-a99b-b5f2c9d6503f
msc.legacyurl: /mvc/overview/older-versions-1/models-data/performing-simple-validation-cs
msc.type: authoredcontent
ms.openlocfilehash: e33f522af74efe97b5a245e956bc0b918ea769af
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78542992"
---
# <a name="performing-simple-validation-c"></a>Provedení jednoduchého ověření (C#)

od [Stephen Walther](https://github.com/StephenWalther)

> Naučte se provádět ověřování v aplikaci ASP.NET MVC. V tomto kurzu vám Stephen Walther zavádí stav modelu a pomocníky HTML pro ověřování.

Cílem tohoto kurzu je vysvětlit, jak můžete provádět ověřování v rámci aplikace ASP.NET MVC. Naučíte se například, jak zabránit někomu v odesílání formuláře, který neobsahuje hodnotu pro požadované pole. Naučíte se používat stav modelu a ověřovací pomocníky HTML pro ověřování.

## <a name="understanding-model-state"></a>Princip stavu modelu

Použijete model stavu nebo přesněji, slovník stavu modelu – k vyjádření chyb ověřování. Například akce vytvořit () v seznamu 1 ověřuje vlastnosti třídy produktu před přidáním třídy produktu do databáze.

Nedoporučujeme, abyste přidali ověřování nebo databázovou logiku do kontroleru. Kontroler by měl obsahovat jenom logiku související s řízením toku aplikace. Připravujeme zástupce, abychom mohli něco zjednodušit.

**Výpis 1 – Controllers\ProductController.cs**

[!code-csharp[Main](performing-simple-validation-cs/samples/sample1.cs)]

V seznamu 1 jsou ověřovány vlastnosti název, popis a JednotkyNaSkladě třídy produktu. Pokud některá z těchto vlastností selže ověřovací test, je přidána chyba do slovníku stavu modelu (reprezentovaného vlastností ModelState třídy Controller).

Pokud dojde k chybám ve stavu modelu, vlastnost ModelState. IsValid vrátí hodnotu false. V takovém případě se zobrazí formulář HTML pro vytvoření nového produktu. V opačném případě, pokud nedochází k chybám ověření, je nový produkt přidán do databáze.

## <a name="using-the-validation-helpers"></a>Použití pomocníků ověřování

Rozhraní ASP.NET MVC obsahuje dvě pomocné rutiny ověřování: Pomocník HTML. ValidationMessage () a nápovědu HTML. ovládací souhrnu ověření (). Tyto dva pomocníky slouží v zobrazení k zobrazení chybových zpráv ověřování.

V zobrazeních pro vytváření a úpravy, která jsou generována automaticky pomocí generování uživatelského rozhraní ASP.NET MVC, se používají pomocníky HTML. ValidationMessage () a HTML. ovládací souhrnu ověření (). Pomocí těchto kroků vygenerujte zobrazení vytvořit:

1. Klikněte pravým tlačítkem na akci vytvořit () v řadiči produktu a vyberte možnost nabídky **Přidat zobrazení** (viz obrázek 1).
2. V dialogovém okně **Přidat zobrazení** zaškrtněte políčko **vytvořit zobrazení silného typu** (viz obrázek 2).
3. V rozevíracím seznamu **Třída zobrazení dat** vyberte třídu produktu.
4. V rozevíracím seznamu **Zobrazit obsah** vyberte vytvořit.
5. Klikněte na tlačítko **Přidat**.

Před přidáním zobrazení nezapomeňte sestavit aplikaci. V opačném případě se seznam tříd nezobrazí v rozevíracím seznamu **Zobrazit data třídy** .

[![dialogového okna Nový projekt](performing-simple-validation-cs/_static/image1.jpg)](performing-simple-validation-cs/_static/image1.png)

**Obrázek 01**: Přidání zobrazení ([kliknutím zobrazíte obrázek v plné velikosti](performing-simple-validation-cs/_static/image2.png))

[![dialogového okna Nový projekt](performing-simple-validation-cs/_static/image2.jpg)](performing-simple-validation-cs/_static/image3.png)

**Obrázek 02**: Vytvoření zobrazení silného typu ([kliknutím zobrazíte obrázek v plné velikosti](performing-simple-validation-cs/_static/image4.png))

Po dokončení těchto kroků získáte zobrazení vytvořit v seznamu 2.

**Výpis 2 – Views\Product\Create.aspx**

[!code-aspx[Main](performing-simple-validation-cs/samples/sample2.aspx)]

V seznamu 2 se volá HTML. ovládací souhrnu ověření () hned nad formulářem HTML. Tato pomocná Nápověda slouží k zobrazení seznamu chybových zpráv ověřování. Pomocník HTML. ovládací souhrnu ověření () vykreslí chyby v seznamu s odrážkami.

Pomocný objekt HTML. ValidationMessage () se volá vedle každého pole formuláře HTML. Tato pomocná zpráva se používá k zobrazení chybové zprávy přímo vedle pole formuláře. V případě výpisu 2 zobrazí pomocník HTML. ValidationMessage () hvězdičku, pokud dojde k chybě.

Stránka na obrázku 3 znázorňuje chybové zprávy, které jsou generovány pomocníky ověřování při odeslání formuláře s chybějícími poli a neplatnými hodnotami.

[![dialogového okna Nový projekt](performing-simple-validation-cs/_static/image3.jpg)](performing-simple-validation-cs/_static/image5.png)

**Obrázek 03**: zobrazení pro vytváření odeslané s problémy ([kliknutím zobrazíte obrázek v plné velikosti](performing-simple-validation-cs/_static/image6.png))

Všimněte si, že při chybě ověřování se také změní vzhled vstupních polí ve formátu HTML. Pomocník HTML. TextBox () vykreslí atribut *Class = "Input-Validation-Error"* , pokud dojde k chybě ověřování přidružené k vlastnosti vykreslené pomocníkem HTML. TextBox ().

Existují tři šablony kaskádových šablon stylů, které slouží k řízení vzhledu chyb ověřování:

- vstup-ověření – Chyba – aplikuje se na &lt;Input&gt; značka vykreslená pomocníkem HTML. TextBox ().
- ověření pole – chyba – byla použita na &lt;rozpětí&gt; značka vykreslená pomocníkem HTML. ValidationMessage ().
- ověření-Shrnutí – chyby – používá se pro &lt;značku ul&gt; vykreslené pomocníkem HTML. ovládací souhrnu ověření ().

Tyto třídy kaskádových šablon stylů můžete upravit, a proto upravit vzhled chyb ověřování úpravou souboru site. CSS umístěného ve složce obsahu.

> [!NOTE] 
> 
> Třída HtmlHelper zahrnuje statické vlastnosti jen pro čtení pro načtení názvů tříd CSS souvisejících s ověřením. Tyto statické vlastnosti mají název ValidationInputCssClassName, ValidationFieldCssClassName a ValidationSummaryCssClassName.

## <a name="prebinding-validation-and-postbinding-validation"></a>Ověření předzávazného ověřování a Postbinding

Pokud odešlete formulář HTML pro vytvoření produktu a zadáte neplatnou hodnotu pro pole Price a žádnou hodnotu pro pole JednotkyNaSkladě, zobrazí se ověřovací zprávy na obrázku 4. Kde se tyto chybové zprávy ověřování podávají?

[![dialogového okna Nový projekt](performing-simple-validation-cs/_static/image4.jpg)](performing-simple-validation-cs/_static/image7.png)

**Obrázek 04**: Chyby ověření předvazeb ([kliknutím zobrazíte obrázek v plné velikosti](performing-simple-validation-cs/_static/image8.png))

Existují dva typy chybových zpráv ověřování – jsou vygenerovány před tím, než jsou pole formuláře HTML svázána s třídou a jsou vygenerovány poté, co jsou pole formuláře svázána s třídou. Jinými slovy, došlo k předvázání chyb ověřování a postbinding chyby ověřování.

Akce Create () vystavená produktovým adaptérem v seznamu 1 přijímá instanci třídy produktu. Signatura metody Create vypadá takto:

[!code-csharp[Main](performing-simple-validation-cs/samples/sample3.cs)]

Hodnoty polí formuláře HTML z formuláře pro vytvoření jsou svázány s třídou productToCreate podle typu pořadače modelů. Výchozí pořadač modelů přidá chybovou zprávu do stavu modelu automaticky, když nemůže navazovat pole formuláře na vlastnost formuláře.

Výchozí model pořadače nemůže navazovat řetězec "Apple" na vlastnost Price třídy produktu. Nemůžete přiřadit řetězec k vlastnosti Decimal. Proto pořadač modelů přidá chybu do stavu modelu.

Výchozí modelový pořadač také nemůže přiřadit hodnotu null vlastnosti, která nepřijímá hodnoty null. Například pořadač modelů nemůže k vlastnosti UnitsInStock přiřadit hodnotu null. Znovu vytvoří pořadač modelů a přidá chybovou zprávu do stavu modelu.

Pokud chcete přizpůsobit vzhled těchto chybových zpráv, musíte pro tyto zprávy vytvořit řetězce prostředků.

## <a name="summary"></a>Souhrn

Cílem tohoto kurzu bylo popsat základní mechanismy ověřování v rozhraní ASP.NET MVC. Zjistili jste, jak používat stav modelu a ověřovací pomocníky HTML pro ověřování. Probrali jsme také rozdíl mezi předvázanými a postbinding ověřováním. V dalších kurzech se podíváme na různé strategie pro přesun ověřovacího kódu z vašich řadičů a do vašich tříd modelu.

> [!div class="step-by-step"]
> [Předchozí](displaying-a-table-of-database-data-cs.md)
> [Další](validating-with-the-idataerrorinfo-interface-cs.md)

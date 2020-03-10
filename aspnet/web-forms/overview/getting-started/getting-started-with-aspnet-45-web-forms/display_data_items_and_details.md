---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
title: Zobrazit datové položky a podrobnosti | Microsoft Docs
author: Erikre
description: V této sérii kurzů se seznámíte se základy vytváření aplikací webových formulářů ASP.NET pomocí ASP.NET 4,7 a Microsoft Visual Studio 2017
ms.author: riande
ms.date: 1/04/2019
ms.assetid: 64a491a8-0ed6-4c2f-9c1c-412962eb6006
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/display_data_items_and_details
msc.type: authoredcontent
ms.openlocfilehash: 130c9ffd29df612dac5bb954830a2eb9b738aaf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641111"
---
# <a name="display-data-items-and-details"></a>Zobrazení datových položek a podrobností

od [Erik Reitan](https://github.com/Erikre)

> V této sérii kurzů se naučíte, jak vytvářet aplikace webových formulářů v ASP.NET pomocí ASP.NET 4,7 a Microsoft Visual Studio 2017.

V tomto kurzu se dozvíte, jak zobrazit položky dat a podrobnosti o datových položkách pomocí webových formulářů ASP.NET a Entity Framework Code First. Tento kurz sestaví na předchozím kurzu "uživatelské rozhraní a navigace" jako součást série kurzů Wingtip Toys. Po dokončení tohoto kurzu uvidíte produkty na stránce *ProductsList. aspx* a v podrobnostech o produktu na stránce *ProductDetails. aspx* .

## <a name="youll-learn-how-to"></a>Dozvíte se, jak provést tyto akce:

- Přidání ovládacího prvku data pro zobrazení produktů z databáze
- Propojit ovládací prvek dat s vybranými daty
- Přidání ovládacího prvku data pro zobrazení podrobností o produktu z databáze
- Načte hodnotu z řetězce dotazu a pomocí této hodnoty omezí data načítaná z databáze.

### <a name="features-introduced-in-this-tutorial"></a>Funkce, které jsou představené v tomto kurzu:

- Vazby modelu
- Zprostředkovatelé hodnot

## <a name="add-a-data-control"></a>Přidání ovládacího prvku data

K vytvoření vazby dat na serverový ovládací prvek můžete použít několik různých možností. Mezi nejběžnější patří:

* Přidání ovládacího prvku zdroje dat
* Ruční přidání kódu
* Použití vazby modelu

### <a name="use-a-data-source-control-to-bind-data"></a>Použití ovládacího prvku zdroje dat pro svázání dat

Přidání ovládacího prvku zdroje dat umožňuje propojit ovládací prvek zdroje dat s ovládacím prvkem, který zobrazuje data. Pomocí tohoto přístupu můžete deklarativně namísto programově propojit serverové ovládací prvky se zdroji dat.

### <a name="code-by-hand-to-bind-data"></a>Kódování dat pomocí ručního vytvoření vazby dat

Kódování podle rukou zahrnuje:

1. Čtení hodnoty
2. Kontroluje se, jestli je null.
3. Převod na odpovídající typ
4. Kontrola úspěšnosti převodu
5. Použití hodnoty v dotazu 

Tento přístup vám umožní mít plnou kontrolu nad logikou přístupu k datům.

### <a name="use-model-binding-to-bind-data"></a>Použití vazby modelu pro svázání dat

Vazba modelu umožňuje vytvořit vazbu výsledků s mnohem menším kódem a poskytuje možnost opakovaného použití funkcí v celé aplikaci. Zjednodušuje práci s logikou přístupu k datům, a přitom stále poskytuje bohatou datovou vazbu na datovou strukturu.

## <a name="display-products"></a>Zobrazit produkty

V tomto kurzu použijete vazbu modelu pro svázání dat. Chcete-li nakonfigurovat ovládací prvek data na použití vazby modelu pro výběr dat, nastavte vlastnost `SelectMethod` ovládacího prvku na název metody v kódu stránky. Ovládací prvek data volá metodu v příslušnou dobu životního cyklu stránky a automaticky vytvoří vazby vrácených dat. Není nutné explicitně volat metodu `DataBind`.

1. V **Průzkumník řešení**otevřete *ProductList. aspx*.
2. Nahraďte existující kód tímto kódem:   

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample1.aspx)]

Tento kód používá ovládací prvek **ListView** s názvem `productList` k zobrazení produktů.

[!code-aspx-csharp[Main](display_data_items_and_details/samples/sample2.aspx)]

Pomocí šablon a stylů definujete způsob, jakým ovládací prvek **ListView** zobrazuje data. Je vhodný pro data v jakékoli opakující se struktuře. I když tento příklad **ListView** jednoduše zobrazuje data databáze, můžete také bez kódu povolit uživatelům upravovat, vkládat a odstraňovat data a řadit a stránkovat data.

Nastavením vlastnosti `ItemType` v ovládacím prvku **ListView** je k dispozici výraz datové vazby `Item` a ovládací prvek se zapíše do silného typu. Jak je uvedeno v předchozím kurzu, můžete vybrat Podrobnosti objektu položky pomocí technologie IntelliSense, například zadání `ProductName`:

![Zobrazení datových položek a podrobností – IntelliSense](display_data_items_and_details/_static/image1.png)

K určení `SelectMethod` hodnoty používáte také vazbu modelu. Tato hodnota (`GetProducts`) odpovídá metodě, kterou přidáte do kódu za účelem zobrazení produktů v dalším kroku.

### <a name="add-code-to-display-products"></a>Přidat kód pro zobrazení produktů

V tomto kroku přidáte kód k naplnění ovládacího prvku **ListView** daty produktu z databáze. Kód podporuje zobrazování všech produktů a jednotlivých kategorií produktů.

1. V **Průzkumník řešení**klikněte pravým tlačítkem na *ProductList. aspx* a pak vyberte **Zobrazit kód**.
2. Nahraďte existující kód v souboru *ProductList.aspx.cs* tímto způsobem:   

    [!code-csharp[Main](display_data_items_and_details/samples/sample3.cs)]

Tento kód ukazuje metodu `GetProducts`, kterou ovládací prvek **ListView** `ItemType` vlastností na stránce *ProductList. aspx* . Chcete-li omezit výsledky na určitou kategorii databáze, kód nastaví `categoryId` hodnotu z hodnoty řetězce dotazu předané na stránku *ProductList. aspx* , když je stránka *ProductList. aspx* přesměrována na. Třída `QueryStringAttribute` v oboru názvů `System.Web.ModelBinding` slouží k načtení hodnoty proměnné řetězce dotazu `id`. Tím se dá pokyn k vytvoření vazby modelu k pokusu o vazbu hodnoty z řetězce dotazu k parametru `categoryId` v době běhu.

Pokud je do stránky předána platná kategorie jako řetězec dotazu, výsledky dotazu jsou omezeny na tyto produkty v databázi, které odpovídají hodnotě `categoryId`. Pokud je například adresa URL stránky *ProductsList. aspx* následující:

[!code-console[Main](display_data_items_and_details/samples/sample4.cmd)]

Na stránce se zobrazí pouze produkty, u kterých se `categoryId` rovná `1`.

Pokud je zavolána stránka *ProductList. aspx* , jsou zobrazeny všechny produkty, pokud není zadán řetězec dotazu.

Zdroje hodnot těchto metod jsou označovány jako *Zprostředkovatelé hodnot* (například *QueryString*) a atributy parametrů, které určují, který zprostředkovatel hodnot použít se označuje jako *atributy zprostředkovatele hodnoty* (například `id`). ASP.NET zahrnuje zprostředkovatele hodnot a odpovídající atributy pro všechny typické zdroje vstupu uživatele v aplikaci webových formulářů, jako je řetězec dotazu, soubory cookie, hodnoty formulářů, ovládací prvky, stav zobrazení, stav relace a vlastnosti profilu. Můžete také napsat vlastní zprostředkovatele hodnot.

### <a name="run-the-application"></a>Spuštění aplikace

Spusťte aplikaci nyní, chcete-li zobrazit všechny produkty nebo produkty kategorie.

1. Spusťte aplikaci stisknutím klávesy **F5** v aplikaci Visual Studio.  
   Prohlížeč otevře a zobrazí stránku *Default. aspx* .

2. V navigační nabídce kategorie produktů vyberte **automobily** .  
   Zobrazí se stránka *ProductList. aspx* zobrazující pouze produkty kategorie **automobilů** . Později v tomto kurzu zobrazíte podrobnosti o produktu.  

    ![Zobrazení datových položek a podrobností – automobily](display_data_items_and_details/_static/image2.png)

3. V navigační nabídce v horní části vyberte **produkty** .  
   Znovu se zobrazí stránka *ProductList. aspx* , tentokrát ale zobrazí celý seznam produktů.   

    ![Zobrazení datových položek a podrobností – produkty](display_data_items_and_details/_static/image3.png)

4. Zavřete prohlížeč a vraťte se do sady Visual Studio.

### <a name="add-a-data-control-to-display-product-details"></a>Přidání ovládacího prvku data pro zobrazení podrobností o produktu

V dalším kroku upravíte značky na stránce *ProductDetails. aspx* , kterou jste přidali v předchozím kurzu, abyste zobrazili konkrétní informace o produktu.

1. V **Průzkumník řešení**otevřete *ProductDetails. aspx*.

2. Nahraďte existující kód tímto kódem:

    [!code-aspx-csharp[Main](display_data_items_and_details/samples/sample5.aspx)] 

    Tento kód používá ovládací prvek **FormView** k zobrazení konkrétních podrobností o produktu. Tento kód používá metody, jako jsou metody použité k zobrazení dat na stránce *ProductList. aspx* . Ovládací prvek **FormView** slouží k zobrazení jednoho záznamu v čase ze zdroje dat. Při použití ovládacího prvku **FormView** vytvoříte šablony pro zobrazení a úpravy hodnot vázaných na data. Tyto šablony obsahují ovládací prvky, výrazy vazby a formátování, které definují vzhled a funkce formuláře.

Připojení předchozí značky k databázi vyžaduje další kód.

1. V **Průzkumník řešení**klikněte pravým tlačítkem na *ProductDetails. aspx* a pak klikněte na **Zobrazit kód**.  
   Zobrazí se soubor *ProductDetails.aspx.cs* .

2. Nahraďte existující kód tímto kódem:   

    [!code-csharp[Main](display_data_items_and_details/samples/sample6.cs)]

Tento kód kontroluje hodnotu řetězce dotazu "`productID`". Pokud se najde platná hodnota řetězce dotazu, zobrazí se shodný produkt. Pokud se řetězec dotazu nenajde nebo jeho hodnota není platná, nezobrazí se žádný produkt.

### <a name="run-the-application"></a>Spuštění aplikace

Nyní můžete spustit aplikaci, abyste viděli jednotlivé produkty zobrazené na základě ID produktu.

1. Spusťte aplikaci stisknutím klávesy **F5** v aplikaci Visual Studio.  
   Prohlížeč otevře a zobrazí stránku *Default. aspx* .

2. V nabídce navigace v kategorii vyberte **lodě** .  
   Zobrazí se stránka *ProductList. aspx* .

3. Vyberte **papírový člun** ze seznamu produktů.
   Zobrazí se stránka *ProductDetails. aspx* .

    ![Zobrazení datových položek a podrobností – produkty](display_data_items_and_details/_static/image4.png)
    
4. Zavřete prohlížeč.

## <a name="additional-resources"></a>Další zdroje

[Načítání a zobrazování dat s vazbami modelů a webovými formuláři](../../presenting-and-managing-data/model-binding/retrieving-data.md)

## <a name="next-steps"></a>Další kroky

V tomto kurzu jste přidali značky a kód pro zobrazení produktů a podrobností o produktu. Seznámili jste se s datovými ovládacími prvky silného typu, vazbou modelů a poskytovateli hodnot. V dalším kurzu přidáte nákupní košík do ukázkové aplikace Wingtip Toys. 

> [!div class="step-by-step"]
> [Předchozí](ui_and_navigation.md)
> [Další](shopping-cart.md)

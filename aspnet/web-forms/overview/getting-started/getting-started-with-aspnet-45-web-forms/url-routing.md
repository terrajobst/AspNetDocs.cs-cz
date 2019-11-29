---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
title: Směrování adres URL | Microsoft Docs
author: Erikre
description: V této sérii kurzů se seznámíte se základy vytváření aplikací webových formulářů ASP.NET pomocí ASP.NET 4,5 a Microsoft Visual Studio Express 2013 pro My...
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 4f4bf092-c400-471f-a876-78fda0417890
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
msc.type: authoredcontent
ms.openlocfilehash: 66b727b69ca4f9a3d35b67f492f9a554146e09ef
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74590712"
---
# <a name="url-routing"></a>Směrování adresy URL

od [Erik Reitan](https://github.com/Erikre)

[Stáhnout vzorový projekt Wingtip Toys (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) nebo [Stáhnout elektronickou knihu (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)

> V této sérii kurzů se naučíte základy vytváření webových formulářů ASP.NET pomocí ASP.NET 4,5 a Microsoft Visual Studio Express 2013 pro web. K dispozici je Visual Studio 2013 [projekt se C# zdrojovým kódem](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) , který se doprovází v této sérii kurzů.

V tomto kurzu upravíte ukázkovou aplikaci Wingtip Toys, která bude podporovat směrování adres URL. Směrování umožňuje, aby webová aplikace používala adresy URL, které jsou uživatelsky přívětivější a lépe zapamatovatelné a lépe podporované vyhledávacími moduly. Tento kurz sestaví z předchozího kurzu "členství a správy" a je součástí série kurzů Wingtip Toys.

## <a name="what-youll-learn"></a>Co se naučíte:

- Jak registrovat trasy pro aplikaci webových formulářů ASP.NET
- Postup přidání tras na webovou stránku.
- Jak vybrat data z databáze pro podporu tras.

## <a name="aspnet-routing-overview"></a>ASP.NET směrování – přehled

Směrování adres URL umožňuje nakonfigurovat aplikaci, aby přijímala adresy URL požadavků, které nejsou namapované na fyzické soubory. Adresa URL požadavku je jednoduše adresa URL, kterou uživatel zadá do prohlížeče, aby našli stránku na vašem webu. Směrování můžete použít k definování adres URL, které jsou sémanticky smysluplné pro uživatele a které můžou pomáhat s optimalizací vyhledávání na modulech (SEO).

Ve výchozím nastavení zahrnuje šablona webových formulářů [ASP.NET popisné adresy URL](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/). Většina základních pracovních postupů se implementuje pomocí *popisných adres URL*. V tomto kurzu ale přidáte přizpůsobené možnosti směrování.

Před přizpůsobením směrování adres URL může ukázková aplikace Wingtip Toys odkazovat na produkt pomocí následující adresy URL:

`https://localhost:44300/ProductDetails.aspx?productID=2`

Pomocí přizpůsobení směrování adres URL se ukázková aplikace Wingtip Toys připojí ke stejnému produktu pomocí snazší čtení adresy URL:

`https://localhost:44300/Product/Convertible%20Car`

### <a name="routes"></a>Tras

Trasa je vzor URL, který je namapován na obslužnou rutinu. Obslužná rutina může být fyzický soubor, jako je například soubor. aspx v aplikaci webových formulářů. Obslužná rutina může být také třída, která zpracovává požadavek. Chcete-li definovat trasu, vytvořte instanci třídy směrování zadáním vzoru adresy URL, obslužné rutiny a volitelně názvu trasy.

Přidáte trasu do aplikace přidáním objektu `Route` do vlastnosti static `Routes` třídy `RouteTable`. Vlastnost Routes je objekt `RouteCollection`, který ukládá všechny trasy pro aplikaci.

### <a name="url-patterns"></a>Vzory adres URL

Vzor adresy URL může obsahovat literálové hodnoty a zástupné symboly proměnných (označované jako parametry adresy URL). Literály a zástupné symboly jsou umístěny v segmentech adresy URL, které jsou odděleny znakem lomítka (`/`).

Když se vytvoří požadavek na webovou aplikaci, adresa URL se analyzuje na segmenty a zástupné symboly a hodnoty proměnných jsou k dispozici pro obslužnou rutinu žádosti. Tento proces je podobný způsobu, jakým jsou data v řetězci dotazu analyzována a předána obslužné rutině žádosti. V obou případech jsou informace o proměnných zahrnuty v adrese URL a předány obslužné rutině ve formě párů klíč-hodnota. Pro řetězce dotazu jsou klíče i hodnoty v adrese URL. Pro trasy jsou klíče zástupné názvy definované ve vzoru adresy URL a v adrese URL jsou pouze hodnoty.

Ve vzoru adresy URL definujete zástupné symboly jejich uzavřením do složených závorek (`{` a `}`). V segmentu lze definovat více než jeden zástupný symbol, ale zástupné symboly musí být odděleny hodnotou literálu. Například `{language}-{country}/{action}` je platným modelem trasy. `{language}{country}/{action}` však není platným vzorem, protože mezi zástupnými symboly není hodnota literálu nebo oddělovač. Směrování proto nemůže určit, kde se má oddělit hodnota pro zástupný symbol jazyka od hodnoty pro zástupný text země.

### <a name="mapping-and-registering-routes"></a>Mapování a registrace tras

Než budete moci přidat trasy na stránky ukázkové aplikace Wingtip Toys, je nutné při spuštění aplikace zaregistrovat trasy. Chcete-li zaregistrovat trasy, upravte obslužnou rutinu události `Application_Start`.

1. V **Průzkumník řešení**sady Visual Studio vyhledejte a otevřete soubor *Global.asax.cs* .
2. Kód zvýrazněný žlutě přidejte do souboru *Global.asax.cs* následujícím způsobem:   

    [!code-csharp[Main](url-routing/samples/sample1.cs?highlight=30-31,34-46)]

Po spuštění ukázkové aplikace Wingtip Toys zavolá obslužnou rutinu události `Application_Start`. Na konci této obslužné rutiny události je volána metoda `RegisterCustomRoutes`. Metoda `RegisterCustomRoutes` přidává každou trasu voláním metody `MapPageRoute` objektu `RouteCollection`. Trasy se definují pomocí názvu trasy, adresy URL trasy a fyzické adresy URL.

První parametr ("`ProductsByCategoryRoute`") je název trasy. Používá se k volání trasy, pokud je potřeba. Druhý parametr ("`Category/{categoryName}`") definuje přívětivou nahrazující adresu URL, která může být dynamická na základě kódu. Tuto trasu použijete při naplňování ovládacího prvku dat pomocí odkazů, které jsou generovány na základě dat. Trasa se zobrazí takto:

[!code-csharp[Main](url-routing/samples/sample2.cs)]

Druhý parametr trasy obsahuje dynamickou hodnotu určenou složenými závorkami (`{ }`). V tomto případě je `categoryName` proměnná, která bude sloužit k určení správné cesty směrování.

> [!NOTE] 
> 
> **Optional**
> 
> Je možné, že je snazší spravovat kód přesunutím metody `RegisterCustomRoutes` do samostatné třídy. Ve složce *Logic* Vytvořte samostatnou třídu `RouteActions`. Přesuňte výše uvedenou metodu `RegisterCustomRoutes` ze souboru *Global.asax.cs* do nové třídy `RoutesActions`. Použijte třídu `RoleActions` a metodu `createAdmin` jako příklad, jak volat metodu `RegisterCustomRoutes` ze souboru *Global.asax.cs* .

Můžete také zaznamenat `RegisterRoutes` volání metody pomocí objektu `RouteConfig` na začátku `Application_Start` obslužné rutiny události. Toto volání provede implementaci výchozího směrování. Byla vložena jako výchozí kód při vytváření aplikace pomocí šablony webových formulářů sady Visual Studio.

## <a name="retrieving-and-using-route-data"></a>Načítání a používání dat směrování

Jak je uvedeno výše, trasy lze definovat. Kód, který jste přidali do obslužné rutiny události `Application_Start` v souboru *Global.asax.cs* , načte definovatelné trasy.

### <a name="setting-routes"></a>Nastavení tras

Trasy vyžadují, abyste přidali další kód. V tomto kurzu použijete vazbu modelu k načtení objektu `RouteValueDictionary`, který se používá při generování tras pomocí dat z ovládacího prvku data. Objekt `RouteValueDictionary` bude obsahovat seznam názvů produktů, které patří do konkrétní kategorie produktů. Pro každý produkt se vytvoří odkaz na základě dat a tras.

#### <a name="enable-routes-for-categories-and-products"></a>Povolit trasy pro kategorie a produkty

V dalším kroku aktualizujete aplikaci tak, aby používala `ProductsByCategoryRoute` k určení správné trasy, která se má zahrnout pro jednotlivé odkazy na kategorie produktů. Také aktualizujete stránku *ProductList. aspx* tak, aby obsahovala směrovaný odkaz na každý produkt. Odkazy se zobrazí, protože byly před změnou, ale odkazy teď budou používat směrování adres URL.

1. V **Průzkumník řešení**otevřete stránku *Web. Master* , pokud ještě není otevřená.
2. Aktualizujte ovládací prvek **ListView** s názvem "`categoryList`" se změnami zvýrazněnými žlutě, takže se kód zobrazí takto:   

    [!code-aspx[Main](url-routing/samples/sample3.aspx?highlight=7-9)]
3. V **Průzkumník řešení**otevřete stránku *ProductList. aspx* .
4. Aktualizujte `ItemTemplate` element stránky *ProductList. aspx* s aktualizacemi zvýrazněnými žlutě, takže se kód zobrazí takto:   

    [!code-aspx[Main](url-routing/samples/sample4.aspx?highlight=6-9,14-16)]
5. Otevřete kód na pozadí *ProductList.aspx.cs* a přidejte následující obor názvů zvýrazněný žlutě:  

    [!code-csharp[Main](url-routing/samples/sample5.cs?highlight=9)]
6. Metodu `GetProducts` kódu na pozadí (*ProductList.aspx.cs*) nahraďte následujícím kódem:   

    [!code-csharp[Main](url-routing/samples/sample6.cs)]

#### <a name="add-code-for-product-details"></a>Přidat kód pro podrobnosti o produktu

Nyní aktualizujte kód na pozadí (*ProductDetails.aspx.cs*) pro stránku *ProductDetails. aspx* , aby používala data směrování. Všimněte si, že nová metoda `GetProduct` přijímá také hodnotu řetězce dotazu pro případ, kde má uživatel odkaz, který používá starší nesměrované, nesměrované adresy URL.

1. Metodu `GetProduct` kódu na pozadí (*ProductDetails.aspx.cs*) nahraďte následujícím kódem:   

    [!code-csharp[Main](url-routing/samples/sample7.cs)]

## <a name="running-the-application"></a>Spuštění aplikace

Nyní můžete spustit aplikaci a zobrazit aktualizované trasy.

1. Stisknutím klávesy **F5** spusťte ukázkovou aplikaci Wingtip Toys.  
 Prohlížeč otevře a zobrazí stránku *Default. aspx* .
2. V horní části stránky klikněte na odkaz **produkty** .  
 Všechny produkty se zobrazí na stránce *ProductList. aspx* . Pro prohlížeč se zobrazí následující adresa URL (s použitím vašeho čísla portu):  
    `https://localhost:44300/ProductList`
3. V dalším kroku klikněte na odkaz kategorie **automobilů** v horní části stránky.  
 Na stránce *ProductList. aspx* se zobrazí pouze automobily. Pro prohlížeč se zobrazí následující adresa URL (s použitím vašeho čísla portu):  
    `https://localhost:44300/Category/Cars`
4. Kliknutím na odkaz, který obsahuje název první auta uvedené na stránce ("**převoditelná auto**") se zobrazí podrobnosti o produktu.  
 Pro prohlížeč se zobrazí následující adresa URL (s použitím vašeho čísla portu):  
    `https://localhost:44300/Product/Convertible%20Car`
5. V dalším kroku zadejte následující nesměrované adresy URL (pomocí čísla portu) do prohlížeče:  
    `https://localhost:44300/ProductDetails.aspx?productID=2`  
 Kód stále rozpoznává adresu URL, která obsahuje řetězec dotazu, pro případ, kdy má uživatel odkaz na záložku.

## <a name="summary"></a>Přehled

V tomto kurzu jste přidali trasy pro kategorie a produkty. Zjistili jste, jak lze směrovat trasy k datovým ovládacím prvkům, které používají vazbu modelu. V dalším kurzu budete implementovat globální zpracování chyb.

## <a name="additional-resources"></a>Další materiály a zdroje informací

[Popisné adresy URL ASP.NET](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)  
[Nasazení zabezpečené aplikace webových formulářů ASP.NET pomocí členství, protokolu OAuth a SQL Database pro Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[Microsoft Azure – bezplatná zkušební verze](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> [Předchozí](membership-and-administration.md)
> [Další](aspnet-error-handling.md)

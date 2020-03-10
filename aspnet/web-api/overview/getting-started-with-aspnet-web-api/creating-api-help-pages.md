---
uid: web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
title: Vytváření stránek s nápovědu pro ASP.NET Web API – ASP.NET 4. x
author: MikeWasson
description: Tento kurz s kódem ukazuje, jak vytvořit stránky s nápovědu pro ASP.NET webové rozhraní API v ASP.NET 4. x.
ms.author: riande
ms.date: 04/01/2013
ms.custom: seoapril2019
ms.assetid: 0150e67b-c50d-4613-83ea-7b4ef8cacc5a
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/creating-api-help-pages
msc.type: authoredcontent
ms.openlocfilehash: 8308dab8bd66aa8f5a3c5fb4133fc7a3df78f671
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556873"
---
# <a name="creating-help-pages-for-aspnet-web-api"></a>Vytváření stránek s nápovědu pro webové rozhraní API ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

Tento kurz s kódem ukazuje, jak vytvořit stránky s nápovědu pro ASP.NET webové rozhraní API v ASP.NET 4. x.

Při vytváření webového rozhraní API je často užitečné vytvořit stránku s přehledem, aby ostatní vývojáři věděli, jak vaše rozhraní API volat. Můžete vytvořit veškerou dokumentaci ručně, ale je lepší ji vygenerovat co nejvíce. Pro usnadnění tohoto úkolu poskytuje webové rozhraní API ASP.NET knihovnu pro automatické generování stránek s podporou v době běhu.

![](creating-api-help-pages/_static/image1.png)

## <a name="creating-api-help-pages"></a>Vytváření stránek s nápovědě k rozhraní API

Nainstalujte [aktualizaci ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=282650). Tato aktualizace integruje stránky s nápovědě do šablony projektu webového rozhraní API.

Dále vytvořte nový projekt ASP.NET MVC 4 a vyberte šablonu projektu webového rozhraní API. Šablona projektu vytvoří ukázkový kontroler rozhraní API s názvem `ValuesController`. Šablona také vytvoří stránky s nápovědě k rozhraní API. Všechny soubory kódu pro stránku s nápovědu jsou umístěny do složky oblasti projektu.

![](creating-api-help-pages/_static/image2.png)

Po spuštění aplikace obsahuje Domovská stránka odkaz na stránku s informacemi o rozhraní API. Z domovské stránky je relativní cesta/help.

![](creating-api-help-pages/_static/image3.png)

Tento odkaz vás přesune na stránku souhrnu rozhraní API.

![](creating-api-help-pages/_static/image4.png)

Zobrazení MVC pro tuto stránku je definováno v oblasti/HelpPage/zobrazení/help/index. cshtml. Tuto stránku můžete upravit a upravit tak rozložení, Úvod, nadpis, styly a tak dále.

Hlavní část stránky je tabulka rozhraní API seskupená podle kontroleru. Položky tabulky jsou generovány dynamicky pomocí rozhraní **IApiExplorer** . (Další informace o tomto rozhraní se dozvíte později.) Pokud přidáte nový kontroler rozhraní API, tabulka se automaticky aktualizuje v době běhu.

Sloupec "rozhraní API" obsahuje seznam metod HTTP a relativního identifikátoru URI. Sloupec Description (popis) obsahuje dokumentaci pro každé rozhraní API. Zpočátku je dokumentace pouze zástupný text. V další části si ukážeme, jak přidat dokumentaci z komentářů XML.

Každé rozhraní API má odkaz na stránku s podrobnějšími informacemi, včetně příkladů požadavků a těl odpovědí.

![](creating-api-help-pages/_static/image5.png)

## <a name="adding-help-pages-to-an-existing-project"></a>Přidání stránek s nápovědě do existujícího projektu

Stránky s přehledem můžete přidat do existujícího projektu webového rozhraní API pomocí Správce balíčků NuGet. Tato možnost je užitečná, když začínáte s jinou šablonou projektu než s šablonou Web API.

V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**. V okně [konzoly Správce balíčků](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) zadejte jeden z následujících příkazů:

Pro **C#** aplikaci: `Install-Package Microsoft.AspNet.WebApi.HelpPage`

Pro **Visual Basic** aplikaci: `Install-Package Microsoft.AspNet.WebApi.HelpPage.VB`

Existují dva balíčky, jeden pro C# a jeden pro Visual Basic. Ujistěte se, že použijete ten, který odpovídá vašemu projektu.

Tento příkaz nainstaluje potřebná sestavení a přidá zobrazení MVC pro stránky s nápovědu (umístěné ve složce oblasti/HelpPage). Musíte ručně přidat odkaz na stránku s usnadněním. Identifikátor URI je/help. Chcete-li vytvořit odkaz v zobrazení Razor, přidejte následující:

[!code-cshtml[Main](creating-api-help-pages/samples/sample1.cshtml)]

Také nezapomeňte zaregistrovat oblasti. V souboru Global. asax přidejte následující kód do **aplikace\_Start** , pokud tam ještě není:

[!code-csharp[Main](creating-api-help-pages/samples/sample2.cs?highlight=4)]

## <a name="adding-api-documentation"></a>Přidání dokumentace k rozhraní API

Ve výchozím nastavení mají stránky pro nápovědu zástupné řetězce pro dokumentaci. Pomocí dokumentačních [komentářů XML](https://msdn.microsoft.com/library/b2s063f7.aspx) můžete vytvořit dokumentaci. Pokud chcete tuto funkci povolit, otevřete soubor oblasti souborů/HelpPage/App\_spusťte/HelpPageConfig. cs a odkomentujte následující řádek:

[!code-csharp[Main](creating-api-help-pages/samples/sample3.cs)]

Teď povolte dokumentaci XML. V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a vyberte **vlastnosti**. Vyberte stránku **sestavení** .

![](creating-api-help-pages/_static/image6.png)

V části **výstup**ověřte **soubor dokumentace XML**. Do pole pro úpravy zadejte "App\_data/XmlDocument. XML".

![](creating-api-help-pages/_static/image7.png)

V dalším kroku otevřete kód pro `ValuesController` kontroler rozhraní API, který je definovaný v/Controllers/ValuesController.cs. Přidejte do metod kontroleru nějaké dokumentační komentáře. Příklad:

[!code-csharp[Main](creating-api-help-pages/samples/sample4.cs)]

> [!NOTE]
> Tip: Pokud umístíte blikající kurzor na řádek nad metodu a zadáte tři lomítka, Visual Studio automaticky vloží prvky XML. Pak můžete vyplnit prázdné hodnoty.

Nyní Sestavte a spusťte aplikaci znovu a přejděte na stránku s nápovědě. V tabulce rozhraní API by se měly zobrazit řetězce dokumentace.

![](creating-api-help-pages/_static/image8.png)

Stránka Help čte řetězce ze souboru XML v době běhu. (Při nasazení aplikace nezapomeňte nasadit soubor XML.)

## <a name="under-the-hood"></a>Pod kapotou

Stránky s usnadněním jsou postaveny nad třídou **ApiExplorer** , která je součástí rozhraní Web API Framework. Třída **ApiExplorer** poskytuje nezpracovaný materiál pro vytvoření stránky s nápovědu. Pro každé rozhraní API obsahuje **ApiExplorer** **ApiDescription** , který popisuje rozhraní API. Pro tento účel je "rozhraní API" definováno jako kombinace metody HTTP a relativního identifikátoru URI. Tady jsou například některá odlišná rozhraní API:

- ZÍSKAT/api/Products
- ZÍSKAT/api/Products/{id}
- PŘÍSPĚVEK/api/Products

Pokud akce kontroleru podporuje více metod HTTP, **ApiExplorer** považuje každou metodu za odlišné rozhraní API.

Chcete-li skrýt rozhraní API z **ApiExplorer**, přidejte do akce atribut **ApiExplorerSettings** a nastavte *IgnoreApi* na hodnotu true.

[!code-csharp[Main](creating-api-help-pages/samples/sample5.cs)]

Tento atribut můžete také přidat do kontroleru pro vyloučení celého kontroleru.

Třída ApiExplorer získává řetězce dokumentace z rozhraní **IDocumentationProvider** . Jak bylo uvedeno dříve, knihovna stránky pro usnadnění poskytuje **IDocumentationProvider** , který získává dokumentaci z dokumentů XML dokumentace. Kód je umístěný v/Areas/HelpPage/XmlDocumentationProvider.cs. Dokumentaci z jiného zdroje můžete získat tak, že napíšete vlastní **IDocumentationProvider**. Pro jeho vedení volejte metodu rozšíření **SetDocumentationProvider** definovanou v **HelpPageConfigurationExtensions**

**ApiExplorer** automaticky volá rozhraní **IDocumentationProvider** , aby získala dokumentační řetězce pro každé rozhraní API. Ukládá je do vlastnosti **dokumentace** objektů **ApiDescription** a **ApiParameterDescription** .

## <a name="next-steps"></a>Další kroky

Nejste omezeni na stránky s technickou pomocí, které jsou zde uvedeny. **ApiExplorer** se ve skutečnosti neomezí na vytváření stránek s nápovědě. Yao Huang – vypsalo jsme některé skvělé blogové příspěvky, které vám pomohou se zamyslet ze svého boxu:

- [Přidání jednoduchého testovacího klienta na stránku ASP.NET webové rozhraní API](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/02/adding-a-simple-test-client-to-asp-net-web-api-help-page.aspx)
- [Stránka podpory webového rozhraní API pro ASP.NET funguje na samoobslužných službách](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/20/making-asp-net-web-api-help-page-work-on-self-hosted-services.aspx)
- [Generování stránky s nápovědu (nebo klienta) v době návrhu pro webové rozhraní API ASP.NET](https://blogs.msdn.com/b/yaohuang1/archive/2013/01/20/design-time-generation-of-help-page-or-proxy-for-asp-net-web-api.aspx)
- [Pokročilá přizpůsobení stránky s technickou nastavením](https://blogs.msdn.com/b/yaohuang1/archive/2012/12/10/asp-net-web-api-help-page-part-3-advanced-help-page-customizations.aspx)

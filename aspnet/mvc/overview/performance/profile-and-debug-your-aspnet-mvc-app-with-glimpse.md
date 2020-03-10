---
uid: mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
title: Profilování a ladění aplikace ASP.NET MVC pomocí nakoukněte | Microsoft Docs
author: Rick-Anderson
description: Nakoukněte je prosperující a rostoucí rodina Open Source balíčků NuGet, které poskytují podrobné informace o výkonu, ladění a diagnostických informacích pro ASP.NET a...
ms.author: riande
ms.date: 03/26/2015
ms.assetid: c205805f-efdd-4fa7-9616-f26eab180611
msc.legacyurl: /mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
msc.type: authoredcontent
ms.openlocfilehash: d3689147a3bc3aa1f4180c377d2483a94bdd95a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538533"
---
# <a name="profile-and-debug-your-aspnet-mvc-app-with-glimpse"></a>Profil aplikace ASP.NET MVC a její ladění pomocí balíčku Glimpse

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> Nakoukněte je prosperující a rostoucí rodina Open Source balíčků NuGet, které poskytují podrobné informace o výkonu, ladění a diagnostikě pro aplikace ASP.NET. Je triviální pro instalaci, odlehčenou, extrémně rychlou a zobrazení klíčových metrik výkonu v dolní části každé stránky. Umožňuje přejít k podrobnostem aplikace v případě, že potřebujete zjistit, co se na serveru chystá. Nakoukněte poskytuje spoustu užitečných informací, které doporučujeme využít v rámci vašeho vývojového cyklu, včetně vašeho testovacího prostředí Azure. Zatímco [Fiddler](http://www.telerik.com/fiddler) a [vývojové nástroje F-12](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx) poskytují zobrazení na straně klienta, nakoukněte poskytuje podrobné zobrazení ze serveru. Tento kurz se zaměřuje na použití balíčků nakoukněte ASP.NET MVC a EF, ale k dispozici je spousta dalších balíčků. Kde je to možné, připojte se k odpovídajícím [nakouknětem dokumentům](http://getglimpse.com/Docs/) , které můžu udržovat. Nakoukněte je open source projekt, takže můžete přispívat ke zdrojovému kódu a dokumentům.

- [Instalace nakoukněte](#ig)
- [Povolit nakoukněte pro localhost](#eg)
- [Karta Časová osa](#Time)
- [Vazby modelu](#mb)
- [Tras](#route)
- [Používání nakoukněte v Azure](#da)
- [Další zdroje](#addRes)

<a id="ig"></a>
## <a name="installing-glimpse"></a>Instalace nakoukněte

Nakoukněte můžete nainstalovat z konzoly Správce balíčků NuGet nebo z konzoly **Správa balíčků NuGet** . V této ukázce nainstalujete balíčky Mvc5 a EF6:

![instalace nakoukněte z NuGet DLG](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image1.png)

Hledání *nakoukněte. EF*

![Nakoukněte. EF z instalačního dialogu NuGet](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image2.png)

Když vyberete **nainstalované balíčky**, uvidíte, že jsou nainstalované závislé moduly nakoukněte:

![Instalované balíčky nakoukněte z DLg](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image3.png)

Následující příkazy instalují moduly nakoukněte MVC5 a EF6 z konzoly Správce balíčků:

[!code-console[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample1.cmd)]

<a id="eg"></a>
## <a name="enable-glimpse-for-localhost"></a>Povolit nakoukněte pro localhost

Přejděte na http://localhost:&lt;p. #&gt;/Glimpse.axd a klikněte na tlačítko <strong>zapnout nakoukněte</strong> .

![Stránka AXD nakoukněte](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image4.png)

Pokud máte zobrazený panel Oblíbené položky, můžete přetáhnout nakoukněte tlačítka a přidat je jako Bookmarklets:

![IE s nakoukněte Bookmarklets](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image5.png)

Teď můžete aplikaci Procházet a v dolní části stránky se zobrazí **zobrazení hlavice** (HUD).

![Stránka správce kontaktů s HUD](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image6.png)

[Stránka NAKOUKNĚTE HUD](http://getglimpse.com/Docs/Heads-up-Display) detailuje informace o časování zobrazené výše. Nenáročné údaje o výkonu, které HUD zobrazí, vám může upozorňovat na problém okamžitě – předtím, než se dostanete ke zkušebnímu cyklu. Kliknutím na &quot;g&quot; v pravém dolním rohu se zobrazí panel nakoukněte:

![Panel nakoukněte](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image7.png)

Na obrázku výše je vybrána [karta spuštění](http://getglimpse.com/Docs/Execution-Tab) , která zobrazuje časové údaje o akcích a filtrech v kanálu. V průběhu fáze 6 kanálu se můžete podívat na svůj [časovač filtru stop watch](http://www.nuget.org/packages/StopWatch/) . I když je časově náročný časovač schopen poskytnout užitečná data o profilech a časováních, nezjistí veškerý čas strávený při autorizaci a vygenerování zobrazení. Můžete si přečíst informace o mém časovači v [profilu a čas, kdy vaše aplikace ASP.NET MVC vše navede do Azure](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx). Stránka [karty](http://getglimpse.com/Docs/Tabs) obsahuje odkazy na podrobné informace o jednotlivých kartách.

<a id="Time"></a>
## <a name="the-timeline-tab"></a>Karta Časová osa

Změnil (a) jsem si nezpracovaný [kurz Dykstra EF 6/MVC 5](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) s následující změnou kódu na řadič instruktorů:

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample2.cs?highlight=1,20-31)]

Výše uvedený kód umožňuje mně předat řetězec dotazu (`eager`) k řízení Eager nebo explicitního načítání dat. Na následujícím obrázku je použit explicitní načítání a na stránce časování se zobrazí všechny zápisy, které jsou načteny v metodě `Index` Action:

![explicitní načítání](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image8.png)

V následujícím kódu je zadán Eager a každý zápis je načten po volání zobrazení `Index`:

![Eager je zadaný.](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image9.png)

Když najedete myší na časový segment, získáte podrobné informace o časování:

![Pokud chcete zobrazit podrobné časování, najeďte myší.](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image10.png)

<a id="mb"></a>
## <a name="model-binding"></a>Vazba modelu

[Karta vazba modelu](http://getglimpse.com/Docs/Model-Binding-Tab) poskytuje spoustu informací, které vám pomohou pochopit, jak jsou proměnné formuláře svázané a proč některé nejsou vázané na to, co by očekávalo. Následující obrázek ukazuje **?** ikona, na kterou můžete kliknout a získat tak stránku s nápovědu nakoukněte pro tuto funkci.

![zobrazení vazby modelu nakoukněte](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image11.png)

<a id="route"></a>
## <a name="routes"></a>Trasy

 Karta trasy nakoukněte vám může přispět k ladění a pochopení směrování. Na následujícím obrázku je vybraná trasa k produktu (a zobrazuje se v nakoukněte konvenci zeleně). Zobrazuje se taky ![vybraný název produktu](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) omezení tras, oblasti a datové tokeny. Další informace najdete v tématu [nakoukněte trasy](http://getglimpse.com/Docs/Routes-Tab) a [směrování atributů v ASP.NET MVC 5](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) . 

<a id="da"></a>
## <a name="using-glimpse-on-azure"></a>Používání nakoukněte v Azure

Výchozí zásady zabezpečení nakoukněte povolují, aby se data nakoukněte zobrazovala jenom z místního hostitele. Tuto zásadu zabezpečení můžete změnit, abyste mohli tato data zobrazit na vzdáleném serveru (například v Azure Web App). V případě testovacích prostředí v Azure přidejte zvýrazněné označení do dolní části souboru *Web. config* a povolte nakoukněte:

[!code-xml[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample3.xml?highlight=2-6)]

Tato změna samostatně umožňuje všem uživatelům zobrazit data nakoukněte ve vzdálené lokalitě. Zvažte přidání značky výše k publikačnímu profilu, takže se nasadí jenom použité, když použijete tento profil publikování (například Azure test Profile). K omezení dat nakoukněte přidáme roli `canViewGlimpseData` a povolíte uživatelům v této roli jenom zobrazení dat nakoukněte.

Odstraňte komentáře ze souboru *GlimpseSecurityPolicy.cs* a změňte volání [IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) z `Administrator` na roli `canViewGlimpseData`:

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample4.cs?highlight=6)]

> [!WARNING]
> Zabezpečení: rozsáhlá data, která poskytuje nakoukněte, by mohla vystavit zabezpečení vaší aplikace. Společnost Microsoft neprovedla audit zabezpečení nakoukněte pro použití v aplikacích v produkci.

Informace o přidávání rolí najdete v kurzu [nasazení webové aplikace ASP.NET MVC 5 pomocí členství, protokolu OAuth a SQL Database do kurzu Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) .

<a id="addRes"></a>
## <a name="additional-resources"></a>Další prostředky

- [Nasazení zabezpečené aplikace ASP.NET MVC 5 s členstvím, protokolem OAuth a SQL Database do Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)
- [Konfigurace nakoukněte](http://getglimpse.com/Docs/Configuration) – Stránka s dokumentem týkající se konfigurace karet, zásad modulu runtime, protokolování a dalších.

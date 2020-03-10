---
uid: aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
title: Začínáme s OWIN a Katana | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 09/27/2013
ms.assetid: 6dae249f-5ac6-4f6e-bc49-13bcd5a54a70
msc.legacyurl: /aspnet/overview/owin-and-katana/getting-started-with-owin-and-katana
msc.type: authoredcontent
ms.openlocfilehash: 4dfd7b8ebb2bb48d7ef800fd522b79a7b4a045c2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584670"
---
# <a name="getting-started-with-owin-and-katana"></a>Začínáme se specifikací OWIN a sadou Katana

o [Jan Wasson](https://github.com/MikeWasson)

[Open Web Interface for .NET (Owin)](http://owin.org/) definuje abstrakci mezi webovými servery .NET a webovými aplikacemi. Díky oddělení webového serveru od aplikace OWIN usnadňuje vytváření middlewaru pro vývoj webů .NET. OWIN také usnadňuje portování webových aplikací jiným hostitelům&#8212;, jako je například samoobslužné hostování ve službě systému Windows nebo v jiném procesu.

OWIN je specifikace ve vlastnictví komunity, nikoli implementace. Projekt Katana je sada open source OWIN komponent vyvinutých společností Microsoft. Obecný přehled obou OWIN a Katana najdete v tématu [Přehled projektu Katana](an-overview-of-project-katana.md). V tomto článku přejdete přímo do kódu, abyste mohli začít.

V tomto kurzu se používá [Visual Studio 2013 Release Candidate](https://go.microsoft.com/fwlink/?LinkId=306566), ale můžete také použít Visual Studio 2012. V aplikaci Visual Studio 2012 se liší několik kroků, které jsou uvedeny níže.

## <a name="host-owin-in-iis"></a>OWIN hostitele ve službě IIS

V této části budeme hostovat OWIN ve službě IIS. Tato možnost nabízí flexibilitu a možnosti vytváření kanálu OWIN spolu s vyspělou sadou funkcí IIS. Pomocí této možnosti se aplikace OWIN spustí v kanálu žádosti ASP.NET.

Nejprve vytvořte nový projekt webové aplikace ASP.NET. (V aplikaci Visual Studio 2012 použijte prázdný typ projektu webové aplikace ASP.NET.)

![](getting-started-with-owin-and-katana/_static/image1.png)

V dialogovém okně **Nový projekt ASP.NET** vyberte **prázdnou** šablonu.

![](getting-started-with-owin-and-katana/_static/image2.png)

### <a name="add-nuget-packages"></a>Přidání balíčků NuGet

Dále přidejte požadované balíčky NuGet. V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**. V okně konzoly Správce balíčků zadejte následující příkaz:

`install-package Microsoft.Owin.Host.SystemWeb –Pre`

![](getting-started-with-owin-and-katana/_static/image3.png)

### <a name="add-a-startup-class"></a>Přidat třídu po spuštění

Dále přidejte třídu pro spuštění OWIN. V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a vyberte možnost **Přidat**a pak vyberte možnost **Nová položka**. V dialogovém okně **Přidat novou položku** vyberte **Owin třídy po spuštění**. Další informace o konfiguraci třídy po spuštění naleznete v tématu [Owin Startup Class Detection](owin-startup-class-detection.md).

![](getting-started-with-owin-and-katana/_static/image4.png)

Do metody `Startup1.Configuration` přidejte následující kód:

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample1.cs?highlight=3)]

Tento kód přidá do kanálu OWIN jednoduchý objekt middleware, který je implementován jako funkce, která přijímá instanci **Microsoft. Owin. IOwinContext** . Když server přijme požadavek HTTP, kanál OWIN vyvolá middleware. Middleware nastaví typ obsahu pro odpověď a zapíše text odpovědi.

> [!NOTE]
> Šablona třídy po spuštění OWIN je k dispozici v Visual Studio 2013. Pokud používáte Visual Studio 2012, stačí přidat novou prázdnou třídu s názvem `Startup1`a vložit do následujícího kódu:

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample2.cs)]

### <a name="run-the-application"></a>Spuštění aplikace

Stisknutím klávesy F5 spusťte ladění. Visual Studio otevře okno prohlížeče, ve kterém se `http://localhost:*port*/`. Stránka by měla vypadat takto:

![](getting-started-with-owin-and-katana/_static/image5.png)

## <a name="self-host-owin-in-a-console-application"></a>OWIN samostatného hostitele v konzolové aplikaci

Tuto aplikaci je snadné převést z hostování služby IIS na samoobslužné hostování ve vlastním procesu. Při hostování služby IIS funguje služba IIS jako server HTTP i proces, který hostuje službu. V případě samoobslužného hostování aplikace vytvoří proces a jako server HTTP používá třídu **HttpListener** .

V aplikaci Visual Studio vytvořte novou konzolovou aplikaci. V okně konzoly Správce balíčků zadejte následující příkaz:

`Install-Package Microsoft.Owin.SelfHost -Pre`

Přidejte třídu `Startup1` z části 1 tohoto kurzu do projektu. Tuto třídu nemusíte měnit.

Implementujte metodu `Main` aplikace následujícím způsobem.

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample3.cs)]

Když spustíte konzolovou aplikaci, server začne naslouchat `http://localhost:9000`. Pokud ve webovém prohlížeči přejdete na tuto adresu, zobrazí se stránka "Hello World".

![](getting-started-with-owin-and-katana/_static/image6.png)

## <a name="add-owin-diagnostics"></a>Přidat diagnostiku OWIN

Balíček Microsoft. Owin. Diagnostics obsahuje middleware, který zachycuje neošetřené výjimky a zobrazuje stránku HTML s podrobnostmi o chybě. Tato stránka funguje podobně jako na chybové stránce ASP.NET, která se někdy označuje jako "[žlutá obrazovka smrti](http://en.wikipedia.org/wiki/Yellow_Screen_of_Death#Yellow)" (YSOD). Podobně jako u YSOD je chybová stránka Katana užitečná při vývoji, ale je dobrým zvykem ji zakázat v provozním režimu.

Chcete-li nainstalovat balíček diagnostiky do projektu, zadejte následující příkaz v okně konzoly Správce balíčků:

`install-package Microsoft.Owin.Diagnostics –Pre`

Změňte kód v metodě `Startup1.Configuration` následujícím způsobem:

[!code-csharp[Main](getting-started-with-owin-and-katana/samples/sample4.cs?highlight=4,9-12)]

Nyní použijte kombinaci kláves CTRL + F5 ke spuštění aplikace bez ladění, aby se Visual Studio při výjimce nepřerušilo. Aplikace se chová stejně jako předtím, dokud nepřejdete na `http://localhost/fail`, kde aplikace vyvolá výjimku. Middleware chybové stránky bude zachytit výjimku a zobrazit stránku HTML s informacemi o chybě. Kliknutím na karty můžete zobrazit zásobník, řetězec dotazu, soubory cookie, hlavičku požadavku a proměnné prostředí OWIN.

![](getting-started-with-owin-and-katana/_static/image7.png)

## <a name="next-steps"></a>Další kroky

- [Rozpoznání spouštěcí třídy OWIN](owin-startup-class-detection.md)
- [Použití OWIN k samoobslužnému hostování ASP.NET webového rozhraní API](../../../web-api/overview/hosting-aspnet-web-api/use-owin-to-self-host-web-api.md)
- [Použití OWIN k samočinnému hostování signálu](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)

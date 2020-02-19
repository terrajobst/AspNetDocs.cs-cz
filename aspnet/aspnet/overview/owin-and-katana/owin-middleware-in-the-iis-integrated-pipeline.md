---
uid: aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
title: Middleware OWIN v integrovaném kanálu IIS | Microsoft Docs
author: Praburaj
description: Tento článek ukazuje, jak spustit OWIN middlewar Components (OMCs) v integrovaném kanálu služby IIS a jak nastavit událost kanálu, na které OMC běží. Měli byste...
ms.author: riande
ms.date: 11/07/2013
ms.assetid: d031c021-33c2-45a5-bf9f-98f8fa78c2ab
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-middleware-in-the-iis-integrated-pipeline
msc.type: authoredcontent
ms.openlocfilehash: 7d157fb6bd9e2ae9b55af41ef06c1eb5e6310ce1
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456709"
---
# <a name="owin-middleware-in-the-iis-integrated-pipeline"></a>Middleware OWIN v integrovaném kanálu IIS

[Praburaj Thiagarajan](https://github.com/Praburaj), [Rick Anderson](https://twitter.com/RickAndMSFT)

> Tento článek ukazuje, jak spustit OWIN middlewar Components (OMCs) v integrovaném kanálu služby IIS a jak nastavit událost kanálu, na které OMC běží. Před čtením tohoto kurzu byste si měli projít přehled o [detekci spouštěcí třídy](owin-startup-class-detection.md) [projektu Katana](an-overview-of-project-katana.md) a Owin. Tento kurz napsal Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), Chris Rossův, Praburaj Thiagarajan a Howard Dierking ( [@howard\_Dierking](https://twitter.com/howard_dierking) ).

I když jsou součásti [Owin](an-overview-of-project-katana.md) middleware (OMCs) primárně určené ke spuštění v kanálu Server-nezávislá, je možné spustit OMC i v integrovaném kanálu služby IIS (**klasický režim není podporován)** . OMC se dá použít v integrovaném kanálu IIS tak, že do konzoly Správce balíčků nainstalujete následující balíček (PMC):

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample1.cmd)]

To znamená, že všechny aplikační architektury, i ty, které ještě nemůžou běžet mimo IIS a System. Web, můžou využívat stávající součásti middlewaru OWIN. 

> [!NOTE]
> Všechny balíčky `Microsoft.Owin.Security.*` se dodávají s novým systémem identit v Visual Studio 2013 (například soubory cookie, účet Microsoft, Google, Facebook, Twitter, [nosný token](http://self-issued.info/docs/draft-ietf-oauth-v2-bearer.html), OAuth, autorizační Server, JWT, Azure Active Directory a Active Directory Federation Services), jsou vytvořené jako OMCs a dají se použít ve scénářích hostovaných v místním prostředí i v rámci služby IIS.

## <a name="how-owin-middleware-executes-in-the-iis-integrated-pipeline"></a>Jak OWIN middleware provádí v integrovaném kanálu IIS

V případě konzolových aplikací OWIN se kanál aplikace sestavený pomocí [Konfigurace spuštění](owin-startup-class-detection.md) nastavuje podle pořadí, ve kterém se komponenty přidávají pomocí metody `IAppBuilder.Use`. To znamená, že kanál OWIN v modulu runtime [Katana](an-overview-of-project-katana.md) zpracuje OMCs v pořadí, v jakém byly zaregistrovány pomocí `IAppBuilder.Use`. V kanálu integrovaném se službou IIS se kanál žádostí [skládá z](https://msdn.microsoft.com/library/ms178468(v=vs.85).aspx) odebíraného předdefinované sady událostí kanálu, jako je například [beginRequest](https://msdn.microsoft.com/library/system.web.httpapplication.beginrequest.aspx), [AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx), [AuthorizeRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authorizerequest.aspx)atd.

Pokud jsme porovnali OMC s modulem [HttpModule](https://msdn.microsoft.com/library/zec9k340(v=vs.85).aspx) v ASP.NET World, musí být OMC zaregistrovaný do správné předem definované události kanálu. Například `MyModule` HttpModule se vyvolá, když se do fáze [AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx) v kanálu dostane požadavek:

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample2.cs?highlight=10)]

Aby se OMC účastnila stejného řazení na základě událostí, zkontroluje kód modulu runtime [Katana](an-overview-of-project-katana.md) prostřednictvím [konfigurace spouštění](owin-startup-class-detection.md) a přihlásí každou součást middlewaru do integrované události kanálu. Například následující OMC a registrační kód vám umožní zobrazit výchozí registraci události pro middlewarové komponenty. (Podrobnější pokyny k vytvoření třídy pro spuštění OWIN najdete v tématu [detekce spouštěcí třídy Owin](owin-startup-class-detection.md).)

1. Vytvořte prázdný projekt webové aplikace a pojmenujte ho **owin2**.
2. V konzole správce balíčků (PMC) spusťte následující příkaz: 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample3.cmd)]
3. Přidejte `OWIN Startup Class` a pojmenujte ji `Startup`. Nahraďte generovaný kód následujícím (změny jsou zvýrazněny):  

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample4.cs?highlight=5-7,15-36)]
4. Stiskněte klávesu F5 a spusťte aplikaci.

Konfigurace po spuštění nastaví kanál se třemi součástmi middlewaru, první dva zobrazují diagnostické informace a poslední z nich odpovídá na události (a také zobrazení diagnostických informací). Metoda `PrintCurrentIntegratedPipelineStage` zobrazuje integrovanou událost kanálu, kterou tento middleware vyvolal a zprávu. Ve výstupním okně se zobrazí následující okna:

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample5.cmd)]

Modul runtime Katana namapovaný každou ze součástí middleware OWIN na [PreExecuteRequestHandler](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx) ve výchozím nastavení, což odpovídá [PreRequestHandlerExecute](https://msdn.microsoft.com/library/system.web.httpapplication.prerequesthandlerexecute.aspx)události kanálu služby IIS.

## <a name="stage-markers"></a>Značky fáze

Můžete označit OMCs ke spuštění ve specifických fázích kanálu pomocí metody rozšíření `IAppBuilder UseStageMarker()`. Pokud chcete v určité fázi spustit sadu middlewarových součástí, vložte značku fáze hned po nastavení poslední komponenty během registrace. Existují pravidla, ve kterých fáze kanálu můžete spustit middleware a které komponenty objednávky musí být spuštěny (pravidla jsou vysvětlena dále v kurzu). Do kódu `Configuration` přidejte `UseStageMarker` metoda, jak je znázorněno níže:

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample6.cs?highlight=13,19)]

Volání `app.UseStageMarker(PipelineStage.Authenticate)` nakonfiguruje všechny dříve registrované komponenty middlewaru (v tomto případě naše dvě diagnostické komponenty), které se spustí ve fázi ověřování kanálu. Poslední součást middleware (která zobrazuje diagnostiku a reaguje na požadavky) se spustí ve fázi `ResolveCache` (událost [ResolveRequestCache](https://msdn.microsoft.com/library/system.web.httpapplication.resolverequestcache.aspx) ).

Stiskněte klávesu F5 a spusťte aplikaci. V okně výstup se zobrazí následující:

[!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample7.cmd)]

## <a name="stage-marker-rules"></a>Pravidla značek fáze

Owin middlewarové komponenty (OMC) je možné nakonfigurovat tak, aby běžely v následujících událostech fáze OWIN kanálu:

[!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample8.cs)]

1. Ve výchozím nastavení se OMCs spustí při poslední události (`PreHandlerExecute`). Proto náš první ukázkový kód zobrazuje "PreExecuteRequestHandler".
2. Pomocí metody `app.UseStageMarker` můžete zaregistrovat OMC, který se má spustit dříve, v libovolné fázi kanálu OWIN, který je uvedený ve výčtu `PipelineStage`.
3. OWIN kanál a kanál služby IIS jsou seřazené, proto musí být volání `app.UseStageMarker` v daném pořadí. Nemůžete nastavit obslužnou rutinu události na událost, která předchází poslední události zaregistrovanou do do `app.UseStageMarker`. Například *po* volání:

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample9.cmd)]

   volání `app.UseStageMarker` předávání `Authenticate` nebo `PostAuthenticate` nebudou dodržena a nebude vyvolána žádná výjimka. OMCs se spouští v poslední fázi, která je ve výchozím nastavení `PreHandlerExecute`. Značky fáze se používají, aby je bylo možné spustit dříve. Pokud zadáte značky fáze mimo pořadí, Zaokrouhleme na předchozí značku. Jinými slovy, přidání značky fáze říká "spustit ne později než fáze X". OMC se spustí na první značce fáze, kterou jste přidali za ně v kanálu OWIN.
4. Nejstarší fáze volání `app.UseStageMarker` WINS. Pokud například přepnete pořadí `app.UseStageMarker` volání z předchozího příkladu:

    [!code-csharp[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample10.cs?highlight=13,19)]

   Zobrazí se okno výstup: 

    [!code-console[Main](owin-middleware-in-the-iis-integrated-pipeline/samples/sample11.cmd)]

   OMCs se spustí ve fázi `AuthenticateRequest`, protože poslední OMC zaregistrovaný v události `Authenticate` a událost `Authenticate` předchází všem ostatním událostem.

---
uid: aspnet/overview/owin-and-katana/owin-startup-class-detection
title: Detekce spouštěcí třídy OWIN | Microsoft Docs
author: Praburaj
description: V tomto kurzu se dozvíte, jak nakonfigurovat, kterou spouštěcí třídu OWIN je načtená. Další informace o OWIN najdete v tématu Přehled projektu Katana. Tento kurz byl...
ms.author: riande
ms.date: 01/28/2019
ms.assetid: 08257f55-36f4-4e39-9c88-2a5602838c79
msc.legacyurl: /aspnet/overview/owin-and-katana/owin-startup-class-detection
msc.type: authoredcontent
ms.openlocfilehash: e1670c32049ec33dd4d1941a091a429d3929c452
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617045"
---
# <a name="owin-startup-class-detection"></a>Rozpoznání spouštěcí třídy OWIN

> V tomto kurzu se dozvíte, jak nakonfigurovat, kterou spouštěcí třídu OWIN je načtená. Další informace o OWIN najdete v tématu [Přehled projektu Katana](an-overview-of-project-katana.md). Tento kurz napsal Rick Anderson ( [@RickAndMSFT](https://twitter.com/#!/RickAndMSFT) ), Praburaj Thiagarajan a Howard Dierking ( [@howard\_Dierking](https://twitter.com/howard_dierking) ).
>
> ## <a name="prerequisites"></a>Předpoklady
>
> [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)

## <a name="owin-startup-class-detection"></a>Rozpoznání spouštěcí třídy OWIN

 Každá aplikace OWIN má spouštěcí třídu, kde zadáte komponenty pro kanál aplikace. Existují různé způsoby, jak můžete připojit třídu spuštění s modulem runtime v závislosti na zvoleném modelu hostování (OwinHost, IIS a IIS-Express). Spouštěcí třída uvedená v tomto kurzu se dá použít v každé hostující aplikaci. Pomocí jednoho z těchto přístupů připojíte spouštěcí třídu k hostujícímu modulu runtime:

1. **Konvence pojmenování**: Katana vyhledá třídu s názvem `Startup` v oboru názvů, která odpovídá názvu sestavení nebo globálnímu oboru názvů.
2. **OwinStartup atribut**: Jedná se o přístup většiny vývojářů, kteří budou muset zadat třídu pro spuštění. Následující atribut nastaví spouštěcí třídu na třídu `TestStartup` v oboru názvů `StartupDemo`.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample1.cs)]

   Atribut `OwinStartup` Přepisuje konvence pojmenování. Můžete také zadat popisný název s tímto atributem, ale použití popisného názvu vyžaduje, abyste také používali `appSetting` prvek v konfiguračním souboru.
3. **Element appSetting v konfiguračním souboru**: element `appSetting` přepisuje atribut `OwinStartup` a konvence pojmenování. Můžete mít více spouštěcích tříd (každý pomocí atributu `OwinStartup`) a nakonfigurovat, která spouštěcí třída bude načtena do konfiguračního souboru pomocí kódu, který je podobný následujícímu:

    [!code-xml[Main](owin-startup-class-detection/samples/sample2.xml)]

   Následující klíč, který explicitně specifikuje spouštěcí třídu a sestavení lze také použít:

    [!code-xml[Main](owin-startup-class-detection/samples/sample3.xml)]

   Následující kód XML v konfiguračním souboru Určuje popisný název spouštěcí třídy `ProductionConfiguration`.

    [!code-xml[Main](owin-startup-class-detection/samples/sample4.xml)]

   Výše uvedený kód musí být použit s následujícím atributem `OwinStartup`, který určuje popisný název a způsobuje, že se třída `ProductionStartup2` spustí.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample5.cs?highlight=1,16)]
4. Chcete-li zakázat zjišťování spouštění OWIN, přidejte `appSetting owin:AutomaticAppStartup` s hodnotou `"false"` v souboru Web. config.

    [!code-xml[Main](owin-startup-class-detection/samples/sample6.xml)]

## <a name="create-an-aspnet-web-app-using-owin-startup"></a>Vytvoření webové aplikace v ASP.NET pomocí spuštění OWIN

1. Vytvořte prázdnou webovou aplikaci v Asp.Net a pojmenujte ji **StartupDemo**. – Nainstalujte `Microsoft.Owin.Host.SystemWeb` pomocí Správce balíčků NuGet. V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak klikněte na **Konzola správce balíčků**. Zadejte následující příkaz:

    [!code-powershell[Main](owin-startup-class-detection/samples/sample7.ps1)]
2. Přidejte třídu pro spuštění OWIN. V aplikaci Visual Studio 2017 klikněte pravým tlačítkem myši na projekt a vyberte možnost **Přidat třídu**.-v dialogovém okně **Přidat novou položku** zadejte do vyhledávacího pole *OWIN* a změňte název na Startup.cs a pak vyberte **Přidat**.

     ![](owin-startup-class-detection/_static/image1.png)

   Až příště budete chtít přidat *třídu pro spuštění Owin*, bude dostupná z nabídky **Přidat** .

     ![](owin-startup-class-detection/_static/image2.png)

   Případně můžete kliknout pravým tlačítkem myši na projekt a vybrat možnost **Přidat**, vybrat **položku Nová položka**a vybrat třídu pro **spuštění Owin**.

     ![](owin-startup-class-detection/_static/image3.png)

- Vygenerovaný kód nahraďte v souboru *Startup.cs* následujícím způsobem:

    [!code-csharp[Main](owin-startup-class-detection/samples/sample8.cs?highlight=5,7,15-28,31-34)]

  Výraz lambda `app.Use` slouží k registraci zadané komponenty middlewaru do kanálu OWIN. V tomto případě nastavujeme protokolování příchozích požadavků před reakcí na příchozí požadavek. Parametr `next` je delegát ( [Func](https://msdn.microsoft.com/library/bb534960(v=vs.100).aspx) &lt; [Task](https://msdn.microsoft.com/library/dd321424(v=vs.100).aspx) &gt;) k další komponentě v kanálu. Výraz lambda `app.Run` zapojování kanálu na příchozí požadavky a poskytuje mechanismus odezvy.
     > [!NOTE]
     > V kódu výše jsme zavedli komentář k atributu `OwinStartup` a budeme se spoléhat na konvenci spuštění třídy s názvem `Startup`.-Stisknutím klávesy ***F5*** spusťte aplikaci. Stiskněte několikrát aktualizovat.

    ![](owin-startup-class-detection/_static/image4.png) Poznámka: číslo zobrazené na obrázcích v tomto kurzu se neshoduje s číslem, které vidíte. Řetězec milisekund se používá k zobrazení nové odpovědi při aktualizaci stránky.
  Trasovací informace můžete zobrazit v okně **výstup** .

    ![](owin-startup-class-detection/_static/image5.png)

## <a name="add-more-startup-classes"></a>Přidat další třídy po spuštění

V této části přidáme další spouštěcí třídu. Do své aplikace můžete přidat více tříd OWIN Startup. Můžete například chtít vytvořit třídy po spuštění pro vývoj, testování a produkci.

1. Vytvořte novou třídu OWIN Startup a pojmenujte ji `ProductionStartup`.
2. Vygenerovaný kód nahraďte následujícím kódem:

    [!code-csharp[Main](owin-startup-class-detection/samples/sample9.cs?highlight=14-18)]
3. Aplikaci spustíte stisknutím klávesy Control F5. Atribut `OwinStartup` určuje, že se spouští spouštěcí třída výroby.

    ![](owin-startup-class-detection/_static/image6.png)
4. Vytvořte další třídu OWIN Startup a pojmenujte ji `TestStartup`.
5. Vygenerovaný kód nahraďte následujícím kódem:

    [!code-csharp[Main](owin-startup-class-detection/samples/sample10.cs?highlight=6,14-18)]

   Přetížení atributu `OwinStartup` výše určuje `TestingConfiguration` jako *popisný* název třídy po spuštění.
6. Otevřete soubor *Web. config* a přidejte spouštěcí klíč aplikace Owin, který určuje popisný název třídy po spuštění:

    [!code-xml[Main](owin-startup-class-detection/samples/sample11.xml?highlight=3-5)]
7. Aplikaci spustíte stisknutím klávesy Control F5. Prvek nastavení aplikace má stejný předchůdce a je spuštěna konfigurace testu.

    ![](owin-startup-class-detection/_static/image7.png)
8. Odeberte *popisný* název z atributu `OwinStartup` ve třídě `TestStartup`.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample12.cs)]
9. Nahraďte spouštěcí klíč aplikace OWIN v souboru *Web. config* následujícím způsobem:

    [!code-xml[Main](owin-startup-class-detection/samples/sample13.xml)]
10. Vrátit atribut `OwinStartup` v každé třídě na kód výchozího atributu generovaný aplikací Visual Studio:

    [!code-csharp[Main](owin-startup-class-detection/samples/sample14.cs)]

    Každý z následujících spouštěcích klíčů aplikace OWIN způsobí spuštění produkční třídy.

    [!code-xml[Main](owin-startup-class-detection/samples/sample15.xml)]

    Poslední spouštěcí klíč určuje metodu konfigurace spuštění. Následující spouštěcí klíč aplikace OWIN umožňuje změnit název třídy konfigurace na `MyConfiguration`.

    [!code-xml[Main](owin-startup-class-detection/samples/sample16.xml)]

## <a name="using-owinhostexe"></a>Použití Owinhost. exe

1. Soubor Web. config nahraďte následujícím kódem:

    [!code-xml[Main](owin-startup-class-detection/samples/sample17.xml?highlight=3-6)]

   Poslední klíč služby WINS, takže v tomto případě je `TestStartup` zadán.
2. Nainstalujte Owinhost z PMC:

    [!code-console[Main](owin-startup-class-detection/samples/sample18.cmd)]
3. Přejděte do složky aplikace (do složky obsahující soubor *Web. config* ) a do příkazového řádku zadejte:

    [!code-console[Main](owin-startup-class-detection/samples/sample19.cmd)]

   Zobrazí se okno příkazového řádku:

    [!code-console[Main](owin-startup-class-detection/samples/sample20.cmd)]
4. Spusťte prohlížeč s `http://localhost:5000/`URL.

    ![](owin-startup-class-detection/_static/image8.png)

   OwinHost respektují konvence při spuštění uvedené výše.
5. V příkazovém okně ukončete OwinHost stisknutím klávesy ENTER.
6. Ve třídě `ProductionStartup` přidejte následující atribut OwinStartup, který určuje popisný název *ProductionConfiguration*.

    [!code-csharp[Main](owin-startup-class-detection/samples/sample21.cs)]
7. Do příkazového řádku zadejte:

    [!code-console[Main](owin-startup-class-detection/samples/sample22.cmd)]

   Je načtena produkční spouštěcí třída.
    ![](owin-startup-class-detection/_static/image9.png)

   Naše aplikace má více tříd po spuštění a v tomto příkladu jsme odvodili, která spouštěcí třída se načte až do doby běhu.
8. Otestujte následující možnosti spuštění modulu runtime:

    [!code-console[Main](owin-startup-class-detection/samples/sample23.cmd)]

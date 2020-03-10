---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
title: Vytvoření klientské aplikace OData v4 (C#) | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 47202362-3808-4add-9a69-c9d1f91d5e4e
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/create-an-odata-v4-client-app
msc.type: authoredcontent
ms.openlocfilehash: a0016cf2cc7bffe6268664395ccb38e140090310
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556292"
---
# <a name="create-an-odata-v4-client-app-c"></a>Vytvoření klientské aplikace OData v4 (C#)

o [Jan Wasson](https://github.com/MikeWasson)

V předchozím kurzu jste vytvořili základní službu OData, která podporuje operace CRUD. Nyní vytvoříme klienta pro službu.

Spusťte novou instanci sady Visual Studio a vytvořte nový projekt konzolové aplikace. V dialogovém okně **Nový projekt** vyberte možnost **nainstalované** &gt; **šablony** &gt; **Visual C#**  &gt; **plocha Windows**a vyberte šablonu **Konzolová aplikace** . Pojmenujte projekt &quot;ProductsApp&quot;.

![](create-an-odata-v4-client-app/_static/image1.png)

> [!NOTE]
> Konzolovou aplikaci můžete také přidat do stejného řešení sady Visual Studio, které obsahuje službu OData.

## <a name="install-the-odata-client-code-generator"></a>Instalace generátoru kódu klienta OData

V nabídce **nástroje** vyberte **rozšíření a aktualizace**. Vyberte **Online** &gt; **galerii sady Visual Studio**. Do vyhledávacího pole vyhledejte &quot;&quot;generátoru kódu klienta OData. Kliknutím na **Stáhnout** nainstalujte VSIX. Může se zobrazit výzva k restartování sady Visual Studio.

[![](create-an-odata-v4-client-app/_static/image3.png)](create-an-odata-v4-client-app/_static/image2.png)

## <a name="run-the-odata-service-locally"></a>Místní spuštění služby OData

Spusťte projekt ProductService ze sady Visual Studio. Ve výchozím nastavení Visual Studio spustí prohlížeč do kořenového adresáře aplikace. Poznamenejte si identifikátor URI; budete ho potřebovat v dalším kroku. Ponechte aplikaci spuštěnou.

![](create-an-odata-v4-client-app/_static/image4.png)

> [!NOTE]
> Pokud oba projekty umístíte do stejného řešení, nezapomeňte spustit projekt ProductService bez ladění. V dalším kroku budete muset zajistit, aby služba běžela při úpravě projektu konzolové aplikace.

## <a name="generate-the-service-proxy"></a>Vygenerovat proxy služby

Proxy služby je třída rozhraní .NET, která definuje metody pro přístup ke službě OData. Proxy překládá volání metod na požadavky HTTP. Třídu proxy vytvoříte spuštěním [šablony T4](https://msdn.microsoft.com/library/bb126445.aspx).

Klikněte pravým tlačítkem na projekt. Vyberte **přidat** &gt; **novou položku**.

![](create-an-odata-v4-client-app/_static/image5.png)

V dialogovém okně **Přidat novou položku** vyberte položku **vizuální C# položky** &gt; **kód** &gt; **OData Client**. Pojmenujte šablonu &quot;ProductClient.tt&quot;. Klikněte na **Přidat** a potom na upozornění zabezpečení.

[![](create-an-odata-v4-client-app/_static/image7.png)](create-an-odata-v4-client-app/_static/image6.png)

V tomto okamžiku se zobrazí chyba, kterou můžete ignorovat. Visual Studio automaticky spustí šablonu, ale šablona potřebuje nejdřív některá nastavení konfigurace.

[![](create-an-odata-v4-client-app/_static/image9.png)](create-an-odata-v4-client-app/_static/image8.png)

Otevřete soubor ProductClient. OData. config. V elementu `Parameter` vložte identifikátor URI z projektu ProductService (předchozí krok). Příklad:

[!code-xml[Main](create-an-odata-v4-client-app/samples/sample1.xml)]

[![](create-an-odata-v4-client-app/_static/image11.png)](create-an-odata-v4-client-app/_static/image10.png)

Znovu spusťte šablonu. V Průzkumník řešení klikněte pravým tlačítkem na soubor ProductClient.tt a vyberte **Spustit vlastní nástroj**.

Šablona vytvoří soubor kódu s názvem ProductClient.cs, který definuje proxy server. Při vývoji aplikace můžete při změně koncového bodu OData znovu spustit šablonu a aktualizovat proxy.

![](create-an-odata-v4-client-app/_static/image12.png)

## <a name="use-the-service-proxy-to-call-the-odata-service"></a>Použití proxy služby pro volání služby OData

Otevřete soubor Program.cs a nahraďte často používaný kód následujícím kódem.

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample2.cs)]

Nahraďte hodnotu *SERVICEURI* identifikátorem URI služby ze starší verze.

[!code-csharp[Main](create-an-odata-v4-client-app/samples/sample3.cs)]

Při spuštění aplikace by měla být výstupem následující:

[!code-console[Main](create-an-odata-v4-client-app/samples/sample4.cmd)]

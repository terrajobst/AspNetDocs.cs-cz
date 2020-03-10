---
uid: web-api/overview/older-versions/self-host-a-web-api
title: Samoobslužné hostování ASP.NET webového rozhraní API 1C#()-ASP.NET 4. x
author: MikeWasson
description: Kurz s kódem ukazuje, jak hostovat webové rozhraní API v konzolové aplikaci.
ms.author: riande
ms.date: 01/26/2012
ms.custom: seoapril2019
ms.assetid: be5ab1e2-4140-4275-ac59-ca82a1bac0c1
msc.legacyurl: /web-api/overview/older-versions/self-host-a-web-api
msc.type: authoredcontent
ms.openlocfilehash: bae1737ba5b16bc67fa0ed0474ff04df0add1b3a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525086"
---
# <a name="self-host-aspnet-web-api-1-c"></a>Samoobslužné hostování ASP.NET webového rozhraní API 1C#()

o [Jan Wasson](https://github.com/MikeWasson)

> V tomto kurzu se dozvíte, jak hostovat webové rozhraní API v konzolové aplikaci. Webové rozhraní API ASP.NET nevyžaduje službu IIS. Webové rozhraní API můžete sami hostovat ve svém vlastním hostitelském procesu. 
> 
> **Nové aplikace by měly používat OWIN k samoobslužnému hostování webového rozhraní API.** Viz [použití Owin k samoobslužnému hostování ASP.NET webového rozhraní API 2](../hosting-aspnet-web-api/use-owin-to-self-host-web-api.md).
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové rozhraní API 1
> - Visual Studio 2012

## <a name="create-the-console-application-project"></a>Vytvoření projektu konzolové aplikace

Spusťte Visual Studio a na **úvodní** stránce vyberte **Nový projekt** . Nebo v nabídce **soubor** vyberte **Nový** a pak **projekt**.

V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte uzel  **C# vizuál** . V **části C#vizuál** vyberte **Windows**. V seznamu šablon projektu vyberte možnost **Konzolová aplikace**. Pojmenujte projekt &quot;SelfHost&quot; a klikněte na tlačítko **OK**.

![](self-host-a-web-api/_static/image1.png)

## <a name="set-the-target-framework-visual-studio-2010"></a>Nastavení cílové architektury (Visual Studio 2010)

Pokud používáte Visual Studio 2010, změňte cílovou architekturu na .NET Framework 4,0. (Ve výchozím nastavení se šablona projektu zaměřuje na [Profil klienta rozhraní .NET Framework](https://msdn.microsoft.com/library/cc656912.aspx#features_not_included_in_the_net_framework_client_profile).)

V Průzkumník řešení klikněte pravým tlačítkem myši na projekt a vyberte **vlastnosti**. V rozevíracím seznamu **cílové rozhraní** Změňte cílovou architekturu na .NET Framework 4,0. Po zobrazení výzvy k použití změny klikněte na **Ano**.

![](self-host-a-web-api/_static/image2.png)

## <a name="install-nuget-package-manager"></a>Nainstalovat správce balíčků NuGet

Správce balíčků NuGet je nejjednodušší způsob, jak přidat sestavení webového rozhraní API do projektu non-ASP.NET.

Chcete-li zjistit, zda je nainstalován Správce balíčků NuGet, klikněte na nabídku **nástroje** v aplikaci Visual Studio. Pokud se zobrazí položka nabídky s názvem **Správce balíčků NuGet**, měli byste mít správce balíčků NuGet.

Instalace správce balíčků NuGet:

1. Spusťte Visual Studio.
2. V nabídce **nástroje** vyberte **rozšíření a aktualizace**.
3. V dialogovém okně **rozšíření a aktualizace** vyberte **online**.
4. Pokud nevidíte "Správce balíčků NuGet", do vyhledávacího pole zadejte "Správce balíčků NuGet".
5. Vyberte správce balíčků NuGet a klikněte na **Stáhnout**.
6. Po dokončení stahování se zobrazí výzva k instalaci.
7. Po dokončení instalace se může zobrazit výzva k restartování sady Visual Studio.

![](self-host-a-web-api/_static/image3.png)

## <a name="add-the-web-api-nuget-package"></a>Přidat balíček NuGet webového rozhraní API

Po instalaci správce balíčků NuGet přidejte do svého projektu balíček samoobslužného hostování webového rozhraní API.

1. V nabídce **nástroje** vyberte **Správce balíčků NuGet**. *Poznámka*: Pokud tuto položku nabídky nevidíte, ujistěte se, že je správce balíčků NuGet nainstalovaný správně.
2. Vyberte **Spravovat balíčky NuGet pro řešení** .
3. V dialogovém okně **Spravovat balíčky zrnko** vyberte možnost **online**.
4. Do vyhledávacího pole zadejte &quot;Microsoft. AspNet. WebApi. SelfHost&quot;.
5. Vyberte samostatný hostitel webového rozhraní API ASP.NET a klikněte na **nainstalovat**.
6. Po instalaci balíčku zavřete dialog kliknutím na **Zavřít** .

> [!NOTE]
> Nezapomeňte nainstalovat balíček s názvem Microsoft. AspNet. WebApi. SelfHost, nikoli AspNetWebApi. SelfHost.

![](self-host-a-web-api/_static/image4.png)

## <a name="create-the-model-and-controller"></a>Vytvoření modelu a kontroleru

V tomto kurzu se jako [Začínáme](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) kurz používá stejný model a třídy kontroleru.

Přidejte veřejnou třídu s názvem `Product`.

[!code-csharp[Main](self-host-a-web-api/samples/sample1.cs)]

Přidejte veřejnou třídu s názvem `ProductsController`. Tato třída je odvozena od třídy **System. Web. http. ApiController**.

[!code-csharp[Main](self-host-a-web-api/samples/sample2.cs)]

Další informace o kódu v tomto kontroleru najdete v kurzu [Začínáme](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md) . Tento kontroler definuje tři akce GET:

| URI | Popis |
| --- | --- |
| /api/products | Získá seznam všech produktů. |
| *ID* /API/Products/ | Získá produkt podle ID. |
| /API/Products/? kategorie =*kategorie* | Získá seznam produktů podle kategorií. |

## <a name="host-the-web-api"></a>Hostování webového rozhraní API

Otevřete soubor Program.cs a přidejte následující příkazy using:

[!code-csharp[Main](self-host-a-web-api/samples/sample3.cs)]

Do třídy **program** přidejte následující kód.

[!code-csharp[Main](self-host-a-web-api/samples/sample4.cs)]

## <a name="optional-add-an-http-url-namespace-reservation"></a>Volitelné Přidání rezervace oboru názvů URL protokolu HTTP

Tato aplikace naslouchá `http://localhost:8080/`. Ve výchozím nastavení vyžaduje naslouchání na konkrétní adrese HTTP oprávnění správce. Při spuštění tohoto kurzu se vám proto může zobrazit tato chyba: "protokol HTTP nemohl zaregistrovat adresu URL http://+:8080/" Existují dva způsoby, jak se vyhnout této chybě:

- Spusťte aplikaci Visual Studio se zvýšenými oprávněními správce nebo
- Pomocí nástroje Netsh. exe udělte vašemu účtu oprávnění k rezervaci adresy URL.

Chcete-li použít nástroj Netsh. exe, otevřete příkazový řádek s oprávněními správce a zadejte následující příkaz: následující příkaz:

[!code-console[Main](self-host-a-web-api/samples/sample5.cmd)]

kde *machine\username* je váš uživatelský účet.

Po skončení samoobslužného hostování nezapomeňte rezervaci odstranit:

[!code-console[Main](self-host-a-web-api/samples/sample6.cmd)]

## <a name="call-the-web-api-from-a-client-application-c"></a>Volání webového rozhraní API z klientské aplikace (C#)

Pojďme napsat jednoduchou konzolovou aplikaci, která volá webové rozhraní API.

Přidejte do řešení nový projekt konzolové aplikace:

- V Průzkumník řešení klikněte pravým tlačítkem na řešení a vyberte **Přidat nový projekt**.
- Vytvořte novou konzolovou aplikaci s názvem &quot;ClientApp&quot;.

![](self-host-a-web-api/_static/image5.png)

Pomocí Správce balíčků NuGet přidejte balíček základních knihoven webových rozhraní API ASP.NET:

- V nabídce Nástroje vyberte **Správce balíčků NuGet**.
- Vyberte **Spravovat balíčky NuGet pro řešení** .
- V dialogovém okně **Spravovat balíčky NuGet** vyberte **online**.
- Do vyhledávacího pole zadejte &quot;Microsoft. AspNet. WebApi. Client&quot;.
- Vyberte balíček klientské knihovny Microsoft ASP.NET webového rozhraní API a klikněte na **nainstalovat**.

Přidejte odkaz v ClientApp do projektu SelfHost:

- V Průzkumník řešení klikněte pravým tlačítkem myši na projekt ClientApp.
- Vyberte **Přidat odkaz**.
- V dialogovém okně **Správce odkazů** v části **řešení**vyberte **projekty**.
- Vyberte projekt SelfHost.
- Klikněte na tlačítko **OK**.

![](self-host-a-web-api/_static/image6.png)

Otevřete soubor Client/program. cs. Přidejte následující příkaz **using** :

[!code-csharp[Main](self-host-a-web-api/samples/sample7.cs)]

Přidejte statickou instanci **HttpClient** :

[!code-csharp[Main](self-host-a-web-api/samples/sample8.cs)]

Přidejte následující metody k vypsání seznamu všechny produkty, vypíše produkt podle ID a vypíše produkty podle kategorie.

[!code-csharp[Main](self-host-a-web-api/samples/sample9.cs)]

Každá z těchto metod se shoduje se stejným vzorem:

1. Voláním **HttpClient. GetAsync** odešlete požadavek GET na příslušný identifikátor URI.
2. Zavolejte **HttpResponseMessage. EnsureSuccessStatusCode**. Tato metoda vyvolá výjimku, pokud je stavem odpovědi HTTP kód chyby.
3. Pro rekonstrukci typu CLR z odpovědi HTTP zavolejte **ReadAsAsync&lt;t&gt;** . Tato metoda je rozšiřující metoda definovaná v **System .NET. http. HttpContentExtensions**.

Metody **GetAsync** a **ReadAsAsync** jsou asynchronní. Vrací objekty **úkolu** , které představují asynchronní operaci. Získání vlastnosti **výsledku** zablokuje vlákno, dokud se operace nedokončí.

Další informace o použití HttpClient, včetně toho, jak provést neblokující volání, najdete v tématu [volání webového rozhraní API z klienta .NET](../advanced/calling-a-web-api-from-a-net-client.md).

Před voláním těchto metod nastavte vlastnost BaseAddress v instanci HttpClient na hodnotu "`http://localhost:8080`". Příklad:

[!code-csharp[Main](self-host-a-web-api/samples/sample10.cs)]

To by mělo mít následující výstup. (Nezapomeňte nejdřív spustit aplikaci SelfHost.)

[!code-console[Main](self-host-a-web-api/samples/sample11.cmd)]

![](self-host-a-web-api/_static/image7.png)

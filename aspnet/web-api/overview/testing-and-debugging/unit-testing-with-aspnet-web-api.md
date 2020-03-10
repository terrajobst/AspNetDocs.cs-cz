---
uid: web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
title: Testování částí ASP.NET webového rozhraní API 2 | Microsoft Docs
author: Rick-Anderson
description: Tyto doprovodné materiály a aplikace ukazují, jak vytvořit jednoduché testy částí pro aplikaci webového rozhraní API 2. Tento kurz ukazuje, jak zahrnout proj test jednotek...
ms.author: riande
ms.date: 06/05/2014
ms.assetid: bf20f78d-ff91-48be-abd1-88e23dcc70ba
msc.legacyurl: /web-api/overview/testing-and-debugging/unit-testing-with-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: f2d60b977475e048a3a74aabff4adc768ee22baf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554969"
---
# <a name="unit-testing-aspnet-web-api-2"></a>Testování částí ASP.NET webového rozhraní API 2

tím, že [FitzMacken](https://github.com/tfitzmac)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> Tyto doprovodné materiály a aplikace ukazují, jak vytvořit jednoduché testy částí pro aplikaci webového rozhraní API 2. V tomto kurzu se dozvíte, jak zahrnout projekt testování částí do řešení a zapsat testovací metody, které kontrolují vrácené hodnoty z metody kontroleru.
>
> V tomto kurzu se předpokládá, že jste obeznámeni se základními koncepty webového rozhraní API ASP.NET. Úvodní kurz najdete v tématu [Začínáme s webovým rozhraním API 2 pro ASP.NET](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).
>
> Testování částí v tomto tématu se úmyslně omezí na jednoduché scénáře dat. V případě testování částí pokročilejších scénářů dat naleznete informace v tématu napodobování [Entity Framework při testování jednotek webového rozhraní API 2 ASP.NET](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).
>
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
> - Webové rozhraní API 2

## <a name="in-this-topic"></a>V tomto tématu

Toto téma obsahuje následující oddíly:

- [Požadavky](#prereqs)
- [Stáhnout kód](#download)
- [Vytvořit aplikaci s projektem testování částí](#appwithunittest)
    - [Přidat projekt testu jednotek při vytváření aplikace](#whencreate)
    - [Přidat projekt testu jednotek do existující aplikace](#addtoexisting)
- [Nastavení aplikace webového rozhraní API 2](#setupproject)
- [Nainstalovat balíčky NuGet do projektu testů](#testpackages)
- [Vytváření testů](#tests)
- [Spustit testy](#runtests)

<a id="prereqs"></a>
## <a name="prerequisites"></a>Předpoklady

[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Komunita, edice Professional nebo Enterprise

<a id="download"></a>
## <a name="download-code"></a>Stažení kódu

Stáhněte [dokončený projekt](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11). Projekt ke stažení obsahuje kód jednotkového testu pro toto téma a pro napodobení [Entity Framework při testování částí webového rozhraní API ASP.NET](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md) .

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a>Vytvořit aplikaci s projektem testování částí

Můžete buď vytvořit projekt testování částí při vytváření aplikace, nebo přidat projekt testování částí do existující aplikace. Tento kurz ukazuje obě metody pro vytvoření projektu testování částí. Pokud chcete postupovat podle tohoto kurzu, můžete použít libovolný přístup.

<a id="whencreate"></a>
### <a name="add-unit-test-project-when-creating-the-application"></a>Přidat projekt testu jednotek při vytváření aplikace

Vytvořte novou webovou aplikaci v ASP.NET s názvem **StoreApp**.

![vytvořit projekt](unit-testing-with-aspnet-web-api/_static/image1.png)

V okně Nová okna projektu ASP.NET vyberte **prázdnou** šablonu a přidejte složky a základní odkazy pro webové rozhraní API. Vyberte možnost **Přidat testy jednotek** . Projekt testu jednotek je automaticky pojmenován **StoreApp. Tests**. Tento název můžete zachovat.

![vytvořit projekt testu jednotek](unit-testing-with-aspnet-web-api/_static/image2.png)

Po vytvoření aplikace se zobrazí, že obsahuje dva projekty.

![dva projekty](unit-testing-with-aspnet-web-api/_static/image3.png)

<a id="addtoexisting"></a>
### <a name="add-unit-test-project-to-an-existing-application"></a>Přidat projekt testu jednotek do existující aplikace

Pokud jste při vytváření aplikace nevytvořili projekt testu jednotek, můžete ho kdykoli přidat. Předpokládejme například, že již máte aplikaci s názvem StoreApp a chcete přidat jednotkové testy. Chcete-li přidat projekt testování částí, klikněte pravým tlačítkem na řešení a vyberte možnost **Přidat** a **Nový projekt**.

![Přidat nový projekt do řešení](unit-testing-with-aspnet-web-api/_static/image4.png)

V levém podokně vyberte **test** a pro typ projektu vyberte **projekt testování částí** . Pojmenujte projekt **StoreApp. Tests**.

![Přidat projekt testu jednotek](unit-testing-with-aspnet-web-api/_static/image5.png)

Ve vašem řešení se zobrazí projekt testování částí.

V projektu testování jednotky přidejte odkaz na projekt do původního projektu.

<a id="setupproject"></a>
## <a name="set-up-the-web-api-2-application"></a>Nastavení aplikace webového rozhraní API 2

V projektu StoreApp přidejte soubor třídy do složky **modely** s názvem **Product.cs**. Obsah souboru nahraďte následujícím kódem.

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample1.cs)]

Sestavte řešení.

Klikněte pravým tlačítkem na složku řadiče a vyberte **Přidat** a **Nová vygenerovaná položka**. Vyberte **kontroler webového rozhraní API 2 – prázdné**.

![Přidat nový kontroler](unit-testing-with-aspnet-web-api/_static/image6.png)

Nastavte název kontroleru na **SimpleProductController**a klikněte na **Přidat**.

![zadat kontroler](unit-testing-with-aspnet-web-api/_static/image7.png)

Nahraďte existující kód následujícím kódem. Pro zjednodušení tohoto příkladu jsou data uložena v seznamu, nikoli v databázi. Seznam definovaný v této třídě představuje produkční data. Všimněte si, že kontroler zahrnuje konstruktor, který přebírá jako parametr seznam objektů produktu. Tento konstruktor umožňuje předat testovací data při testování jednotky. Kontroler také obsahuje dvě **asynchronní** metody pro ilustraci asynchronních metod testování částí. Tyto asynchronní metody byly implementovány voláním **Task. FromResult** pro minimalizaci nadbytečného kódu, ale obvykle by metody zahrnovaly operace náročné na prostředky.

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample2.cs)]

Metoda getproduct vrátí instanci rozhraní **IHttpActionResult** . IHttpActionResult je jednou z nových funkcí webového rozhraní API 2 a zjednodušuje vývoj testů jednotek. Třídy, které implementují rozhraní IHttpActionResult, se nacházejí v oboru názvů [System. Web. http. Results](https://msdn.microsoft.com/library/system.web.http.results.aspx) . Tyto třídy reprezentují možné odezvy z požadavku akce a odpovídají stavovým kódům HTTP.

Sestavte řešení.

Nyní jste připraveni k nastavení testovacího projektu.

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a>Nainstalovat balíčky NuGet do projektu testů

Použijete-li prázdnou šablonu k vytvoření aplikace, projekt testu jednotek (StoreApp. Tests) neobsahuje žádné nainstalované balíčky NuGet. Jiné šablony, jako je například šablona webového rozhraní API, obsahují některé balíčky NuGet v projektu testování částí. Pro tento kurz musíte do testovacího projektu zahrnout balíček Microsoft ASP.NET Web API 2 Core.

Klikněte pravým tlačítkem na projekt StoreApp. Tests a vyberte možnost **Spravovat balíčky NuGet**. Chcete-li přidat balíčky do projektu, je nutné vybrat projekt StoreApp. Tests.

![spravovat balíčky](unit-testing-with-aspnet-web-api/_static/image8.png)

Najděte a nainstalujte balíček Microsoft ASP.NET webového rozhraní API 2 Core.

![nainstalovat balíček webového rozhraní API Core](unit-testing-with-aspnet-web-api/_static/image9.png)

Zavřete okno Spravovat balíčky NuGet.

<a id="tests"></a>
## <a name="create-tests"></a>Vytváření testů

Ve výchozím nastavení obsahuje projekt testů prázdný testovací soubor s názvem UnitTest1.cs. Tento soubor zobrazuje atributy, které použijete k vytvoření testovacích metod. Pro testování částí můžete použít tento soubor nebo vytvořit vlastní soubor.

![UnitTest1](unit-testing-with-aspnet-web-api/_static/image10.png)

Pro tento kurz vytvoříte vlastní testovací třídu. Soubor UnitTest1.cs můžete odstranit. Přidejte třídu s názvem **TestSimpleProductController.cs**a nahraďte kód následujícím kódem.

[!code-csharp[Main](unit-testing-with-aspnet-web-api/samples/sample3.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a>Spouštění testů

Nyní jste připraveni spustit testy. Všechny metody, které jsou označeny atributem **TestMethod** , budou testovány. Z položky nabídky **test** spusťte testy.

![Provádění testů](unit-testing-with-aspnet-web-api/_static/image11.png)

Otevřete okno **Průzkumník testů** a Všimněte si výsledků testů.

![výsledky testu](unit-testing-with-aspnet-web-api/_static/image12.png)

## <a name="summary"></a>Souhrn

Dokončili jste tento kurz. Data v tomto kurzu se záměrně zjednodušila a zaměřuje se na podmínky testování částí. V případě testování částí pokročilejších scénářů dat naleznete informace v tématu napodobování [Entity Framework při testování jednotek webového rozhraní API 2 ASP.NET](mocking-entity-framework-when-unit-testing-aspnet-web-api-2.md).

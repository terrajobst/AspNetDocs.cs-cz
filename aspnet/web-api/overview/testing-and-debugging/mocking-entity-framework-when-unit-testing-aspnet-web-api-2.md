---
uid: web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
title: Napodobení Entity Framework při testování částí ASP.NET webového rozhraní API 2 | Microsoft Docs
author: Rick-Anderson
description: Tyto doprovodné materiály a aplikace ukazují, jak vytvořit testy částí pro aplikaci webového rozhraní API 2, která používá Entity Framework. Ukazuje, jak změnit...
ms.author: riande
ms.date: 12/13/2013
ms.assetid: cd844025-ccad-41ce-8694-595f1022a49f
msc.legacyurl: /web-api/overview/testing-and-debugging/mocking-entity-framework-when-unit-testing-aspnet-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 258450107ee7443c4efd43a3b8e4851249745227
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555088"
---
# <a name="mocking-entity-framework-when-unit-testing-aspnet-web-api-2"></a>Napodobování Entity Framework při testování jednotek webového rozhraní API 2 ASP.NET

tím, že [FitzMacken](https://github.com/tfitzmac)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11)

> Tyto doprovodné materiály a aplikace ukazují, jak vytvořit testy částí pro aplikaci webového rozhraní API 2, která používá Entity Framework. Ukazuje, jak upravit vygenerovaný řadič, aby bylo možné předat objekt kontextu pro testování a jak vytvořit objekty testu, které pracují s Entity Framework.
>
> Úvod do testování částí s webovým rozhraním API v ASP.NET najdete v tématu [testování částí s webovým rozhraním API 2 pro ASP.NET](unit-testing-with-aspnet-web-api.md).
>
> V tomto kurzu se předpokládá, že jste obeznámeni se základními koncepty webového rozhraní API ASP.NET. Úvodní kurz najdete v tématu [Začínáme s webovým rozhraním API 2 pro ASP.NET](../getting-started-with-aspnet-web-api/tutorial-your-first-web-api.md).
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
- [Vytvoření třídy modelu](#modelclass)
- [Přidání kontroleru](#controller)
- [Přidat vkládání závislostí](#dependency)
- [Nainstalovat balíčky NuGet do projektu testů](#testpackages)
- [Vytvořit kontext testu](#testcontext)
- [Vytváření testů](#tests)
- [Spustit testy](#runtests)

Pokud jste již dokončili kroky při [testování částí s webovým rozhraním API 2 pro ASP.NET](unit-testing-with-aspnet-web-api.md), můžete přejít k části [Přidání kontroleru](#controller).

<a id="prereqs"></a>
## <a name="prerequisites"></a>Předpoklady

Visual Studio 2017 Community, Professional nebo Enterprise Edition

<a id="download"></a>
## <a name="download-code"></a>Stažení kódu

Stáhněte [dokončený projekt](https://code.msdn.microsoft.com/Unit-Testing-with-ASPNET-1374bc11). Projekt ke stažení obsahuje kód jednotkového testu pro toto téma a téma [testování částí ASP.NET webového rozhraní API 2](unit-testing-with-aspnet-web-api.md) .

<a id="appwithunittest"></a>
## <a name="create-application-with-unit-test-project"></a>Vytvořit aplikaci s projektem testování částí

Můžete buď vytvořit projekt testování částí při vytváření aplikace, nebo přidat projekt testování částí do existující aplikace. V tomto kurzu se dozvíte, jak vytvořit projekt testování částí při vytváření aplikace.

Vytvořte novou webovou aplikaci v ASP.NET s názvem **StoreApp**.

V okně Nová okna projektu ASP.NET vyberte **prázdnou** šablonu a přidejte složky a základní odkazy pro webové rozhraní API. Vyberte možnost **Přidat testy jednotek** . Projekt testu jednotek je automaticky pojmenován **StoreApp. Tests**. Tento název můžete zachovat.

![vytvořit projekt testu jednotek](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image1.png)

Po vytvoření aplikace uvidíte, že obsahuje dva projekty – **StoreApp** a **StoreApp. Tests**.

<a id="modelclass"></a>
## <a name="create-the-model-class"></a>Vytvoření třídy modelu

V projektu StoreApp přidejte soubor třídy do složky **modely** s názvem **Product.cs**. Obsah souboru nahraďte následujícím kódem.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample1.cs)]

Sestavte řešení.

<a id="controller"></a>
## <a name="add-the-controller"></a>Přidání kontroleru

Klikněte pravým tlačítkem na složku řadiče a vyberte **Přidat** a **Nová vygenerovaná položka**. Pomocí Entity Framework vyberte kontroler webového rozhraní API 2 s akcemi.

![Přidat nový kontroler](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image2.png)

Nastavte následující hodnoty:

- Název kontroleru: **ProductController**
- Třída modelu: **produkt**
- Třída kontextu dat: [vybrat **nový kontext dat** , který vyplní hodnoty zobrazené níže]

![zadat kontroler](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image3.png)

Kliknutím na **Přidat** vytvořte kontroler s automaticky generovaným kódem. Kód obsahuje metody pro vytváření, načítání, aktualizaci a odstraňování instancí třídy produktu. Následující kód ukazuje metodu pro přidání produktu. Všimněte si, že metoda vrací instanci třídy **IHttpActionResult**.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample2.cs)]

IHttpActionResult je jednou z nových funkcí webového rozhraní API 2 a zjednodušuje vývoj testů jednotek.

V další části budete přizpůsobovat generovaný kód pro usnadnění předávání testovacích objektů do kontroleru.

<a id="dependency"></a>
## <a name="add-dependency-injection"></a>Přidat vkládání závislostí

V současné době je třída ProductController pevně kódovaná pro použití instance třídy StoreAppContext. K úpravě aplikace a odstranění této pevně zakódované závislosti použijete vzor nazvaný injektáže závislosti. Přerušením této závislosti můžete předat objekt objektu k testování.

Klikněte pravým tlačítkem na složku **modely** a přidejte nové rozhraní s názvem **IStoreAppContext**.

Nahraďte kód následujícím kódem.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample3.cs)]

Otevřete soubor StoreAppContext.cs a udělejte následující zvýrazněné změny. Důležité změny, které se mají poznamenat:

- Třída StoreAppContext implementuje rozhraní IStoreAppContext.
- Metoda MarkAsModified je implementovaná.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample4.cs?highlight=6,14-17)]

Otevřete soubor ProductController.cs. Změňte existující kód tak, aby odpovídal zvýrazněnému kódu. Tyto změny ruší závislost na StoreAppContext a povolují ostatním třídám předat jiný objekt pro třídu kontextu. Tato změna vám umožní předat kontext testu během testování částí.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample5.cs?highlight=4,7-12)]

V ProductController je potřeba udělat ještě jednu změnu. V metodě **PutProduct** nahraďte řádek, který nastaví stav entity na hodnotu změněno, voláním metody MarkAsModified.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample6.cs?highlight=14-15)]

Sestavte řešení.

Nyní jste připraveni k nastavení testovacího projektu.

<a id="testpackages"></a>
## <a name="install-nuget-packages-in-test-project"></a>Nainstalovat balíčky NuGet do projektu testů

Použijete-li prázdnou šablonu k vytvoření aplikace, projekt testu jednotek (StoreApp. Tests) neobsahuje žádné nainstalované balíčky NuGet. Jiné šablony, jako je například šablona webového rozhraní API, obsahují některé balíčky NuGet v projektu testování částí. Pro tento kurz musíte zahrnout balíček Entity Framework a balíček Microsoft ASP.NET Web API 2 Core do projektu testů.

Klikněte pravým tlačítkem na projekt StoreApp. Tests a vyberte možnost **Spravovat balíčky NuGet**. Chcete-li přidat balíčky do projektu, je nutné vybrat projekt StoreApp. Tests.

![spravovat balíčky](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image4.png)

V online balíčcích vyhledejte a nainstalujte balíček EntityFramework (verze 6,0 nebo novější). Pokud se zdá, že balíček EntityFramework je již nainstalován, jste pravděpodobně vybrali projekt StoreApp namísto projektu StoreApp. Tests.

![Přidat Entity Framework](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image5.png)

Najděte a nainstalujte balíček Microsoft ASP.NET webového rozhraní API 2 Core.

![nainstalovat balíček webového rozhraní API Core](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image6.png)

Zavřete okno Spravovat balíčky NuGet.

<a id="testcontext"></a>
## <a name="create-test-context"></a>Vytvořit kontext testu

Do testovacího projektu přidejte třídu s názvem **TestDbSet** . Tato třída slouží jako základní třída pro sadu testovacích dat. Nahraďte kód následujícím kódem.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample7.cs)]

Přidejte třídu s názvem **TestProductDbSet** do testovacího projektu, který obsahuje následující kód.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample8.cs)]

Přidejte třídu s názvem **TestStoreAppContext** a nahraďte existující kód následujícím kódem.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample9.cs)]

<a id="tests"></a>
## <a name="create-tests"></a>Vytváření testů

Ve výchozím nastavení obsahuje projekt testů prázdný testovací soubor s názvem **UnitTest1.cs**. Tento soubor zobrazuje atributy, které použijete k vytvoření testovacích metod. Pro tento kurz můžete tento soubor odstranit, protože budete přidávat novou testovací třídu.

Do testovacího projektu přidejte třídu s názvem **TestProductController** . Nahraďte kód následujícím kódem.

[!code-csharp[Main](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/samples/sample10.cs)]

<a id="runtests"></a>
## <a name="run-tests"></a>Spouštění testů

Nyní jste připraveni spustit testy. Všechny metody, které jsou označeny atributem **TestMethod** , budou testovány. Z položky nabídky **test** spusťte testy.

![Provádění testů](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image7.png)

Otevřete okno **Průzkumník testů** a Všimněte si výsledků testů.

![výsledky testu](mocking-entity-framework-when-unit-testing-aspnet-web-api-2/_static/image8.png)

---
uid: web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
title: Volání webového rozhraní API z aplikace Windows Phone 8 (C#)-ASP.NET 4. x
author: rmcmurray
description: 'Kurz s kódem: Vytvoření aplikace webového rozhraní API v ASP.NET v ASP.NET 4. x, která poskytuje katalog knih pro aplikaci Windows Phone 8.'
ms.author: riande
ms.date: 10/09/2013
ms.custom: seoapril2019
ms.assetid: b9775f41-352a-4f82-baa6-23e95b342e20
msc.legacyurl: /web-api/overview/mobile-clients/calling-web-api-from-a-windows-phone-8-application
msc.type: authoredcontent
ms.openlocfilehash: c5da14a6856f551343b6fb14f0aedc659e792f6b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78614735"
---
# <a name="calling-web-api-from-a-windows-phone-8-application-c"></a>Volání webového rozhraní API z aplikace pro Windows Phone 8 (C#)

od [Robert blog](https://github.com/rmcmurray)

V tomto kurzu se naučíte, jak vytvořit úplný kompletní scénář skládající se z aplikace ASP.NET Web API, která poskytuje katalog knih pro aplikaci Windows Phone 8.

### <a name="overview"></a>Přehled

Služby RESTful, jako je ASP.NET webové rozhraní API, zjednodušují vytváření aplikací založených na protokolu HTTP pro vývojáře abstrakcí architektury pro aplikace na straně serveru a na straně klienta. Namísto vytváření proprietárního protokolu založeného na soketu pro komunikaci, vývojáři webového rozhraní API jednoduše potřebují publikovat požadavky HTTP pro svou aplikaci (například: GET, POST, PUT, DELETE) a klientské aplikace jenom potřebují spotřebovat. metody HTTP, které jsou nezbytné pro jejich aplikaci.

V tomto uceleném kurzu se naučíte, jak pomocí webového rozhraní API vytvořit následující projekty:

- V [první části tohoto kurzu](#STEP1)vytvoříte aplikaci webového rozhraní API ASP.NET, která bude podporovat všechny operace vytvoření, čtení, aktualizace a odstranění (CRUD) pro správu katalogu knih. Tato aplikace použije [ukázkový soubor XML (Books. XML)](https://msdn.microsoft.com/library/windows/desktop/ms762271.aspx) z MSDN.
- V [druhé části tohoto kurzu](#STEP2)vytvoříte interaktivní aplikaci Windows Phone 8, která načte data z vaší aplikace webového rozhraní API.

#### <a name="prerequisites"></a>Předpoklady

- Visual Studio 2013 s nainstalovanou sadou Windows Phone 8 SDK
- Windows 8 nebo novější v 64 systému s nainstalovanou technologií Hyper-V
- Seznam dalších požadavků najdete v části *požadavky na systém* na stránce pro stažení [sady Windows Phone SDK 8,0](https://www.microsoft.com/download/details.aspx?id=35471) .

> [!NOTE]
> Pokud budete testovat připojení mezi webovým rozhraním API a Windows Phone 8 projektů v místním systému, budete muset postupovat podle pokynů v článku *[připojení emulátoru Windows Phone 8 k webovým aplikacím API v místním počítači](https://go.microsoft.com/fwlink/?LinkId=324014)* a nastavení testovacího prostředí.

<a id="STEP1"></a>
### <a name="step-1-creating-the-web-api-bookstore-project"></a>Krok 1: vytvoření projektu Bookstore webového rozhraní API

Prvním krokem tohoto uceleného kurzu je vytvoření projektu webového rozhraní API, který podporuje všechny operace CRUD. Všimněte si, že do tohoto řešení přidáte projekt Windows Phone aplikace v [kroku 2](#STEP2) tohoto kurzu.

1. Otevřete **Visual Studio 2013**.
2. Klikněte na **soubor**, **Nový**a pak na **projekt**.
3. Po zobrazení dialogového okna **Nový projekt** rozbalte položku **nainstalováno**, potom **šablony**, **C#vizuál**a pak možnost **Web**.

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image2.png)](calling-web-api-from-a-windows-phone-8-application/_static/image1.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                Rozbalte kliknutím na obrázek.                                                                |

4. Zvýrazněte **ASP.NET webová aplikace**, jako název projektu zadejte **Bookstore** a pak klikněte na **OK**.
5. Po zobrazení dialogového okna **Nový projekt ASP.NET** vyberte šablonu **webové rozhraní API** a pak klikněte na **OK**.

   | [![](calling-web-api-from-a-windows-phone-8-application/_static/image4.png)](calling-web-api-from-a-windows-phone-8-application/_static/image3.png) |
   |-----------------------------------------------------------------------------------------------------------------------------------------------------|
   |                                                                Rozbalte kliknutím na obrázek.                                                                |

6. Po otevření projektu webového rozhraní API odeberte z projektu ukázkový kontroler:

    1. Rozbalte složku **Controllers** v Průzkumníkovi řešení.
    2. Klikněte pravým tlačítkem na soubor **ValuesController.cs** a pak klikněte na **Odstranit**.
    3. Po zobrazení výzvy k potvrzení odstranění klikněte na **OK** .
7. Přidejte datový soubor XML do projektu webového rozhraní API; Tento soubor obsahuje obsah katalogu Bookstore:

   1. V Průzkumníku řešení klikněte pravým tlačítkem na složku **aplikace\_data** a pak klikněte na **Přidat**a pak klikněte na **Nová položka**.
   2. Jakmile se zobrazí dialogové okno **Přidat novou položku** , zvýrazněte šablonu **souboru XML** .
   3. Pojmenujte soubor **Books. XML**a potom klikněte na **Přidat**.
   4. Po otevření souboru **Books. XML** nahraďte kód v souboru souborem XML z ukázkových **knih. XML** na webu MSDN: 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample1.xml)]
   5. Uložte a zavřete soubor XML.

8. Přidejte model Bookstore do projektu webového rozhraní API; Tento model obsahuje logiku vytváření, čtení, aktualizace a odstranění (CRUD) pro aplikaci Bookstore:

   1. V Průzkumníku řešení klikněte pravým tlačítkem na složku **modely** , potom klikněte na **Přidat**a potom klikněte na **Třída**.
   2. Když se zobrazí dialogové okno **Přidat novou položku** , pojmenujte soubor třídy **BookDetails.cs**a pak klikněte na **Přidat**.
   3. Po otevření souboru **BookDetails.cs** nahraďte kód v souboru následujícím kódem: 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample2.cs)]
   4. Uložte a zavřete soubor **BookDetails.cs** .

9. Přidejte kontroler Bookstore do projektu webového rozhraní API:

   1. V Průzkumníku řešení klikněte pravým tlačítkem na složku **řadiče** a pak klikněte na **Přidat**a potom na **kontroler**.
   2. Po zobrazení dialogového okna **Přidat generování uživatelského rozhraní** zvýrazněte možnost **KONTROLER webového rozhraní API 2 – prázdné**a pak klikněte na tlačítko **Přidat**.
   3. Po zobrazení dialogového okna **Přidat řadič** pojmenujte kontrolér **BooksController**a pak klikněte na **Přidat**.
   4. Po otevření souboru **BooksController.cs** nahraďte kód v souboru následujícím kódem: 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample3.cs)]
   5. Uložte a zavřete soubor **BooksController.cs** .

10. Sestavte aplikaci webového rozhraní API, aby kontrolovala chyby.

<a id="STEP2"></a>
### <a name="step-2-adding-the-windows-phone-8-bookstore-catalog-project"></a>Krok 2: Přidání projektu katalogu Bookstore pro Windows Phone 8

Dalším krokem tohoto kompletního scénáře je vytvoření aplikace katalogu pro Windows Phone 8. Tato aplikace bude používat šablonu *aplikace Windows Phone Data Bound* pro výchozí uživatelské rozhraní a bude používat aplikaci webového rozhraní API, kterou jste vytvořili v [kroku 1](#STEP1) tohoto kurzu jako zdroj dat.

1. V Průzkumníku řešení klikněte pravým tlačítkem na řešení **Bookstore** a pak klikněte na **Přidat**a **Nový projekt**.
2. Po zobrazení dialogového okna **Nový projekt** rozbalte položku **nainstalováno**, **C#vizuál**a poté **Windows Phone**.
3. Zvýrazněte **Windows Phone aplikace datové vazby**, jako název zadejte **BookCatalog** a pak klikněte na **OK**.
4. Přidejte do projektu **BookCatalog** balíček NuGet JSON.NET:

    1. V Průzkumníku řešení klikněte pravým tlačítkem na **odkazy** pro projekt **BookCatalog** a pak klikněte na **Spravovat balíčky NuGet**.
    2. Po zobrazení dialogového okna **Spravovat balíčky NuGet** rozbalte oddíl **Online** a zvýrazněte **NuGet.org**.
    3. Do vyhledávacího pole zadejte **JSON.NET** a klikněte na ikonu hledání.
    4. Ve výsledcích hledání zvýrazněte **JSON.NET** a pak klikněte na **nainstalovat**.
    5. Po dokončení instalace klikněte na **Zavřít**.
5. Přidejte model **BookDetails** do projektu **BookCatalog** ; obsahuje obecný model třídy Bookstore:

   1. V Průzkumníku řešení klikněte pravým tlačítkem na projekt **BookCatalog** , pak klikněte na **Přidat**a potom na **Nová složka**.
   2. Pojmenujte nové **modely**složek.
   3. V Průzkumníku řešení klikněte pravým tlačítkem na složku **modely** , potom klikněte na **Přidat**a potom klikněte na **Třída**.
   4. Když se zobrazí dialogové okno **Přidat novou položku** , pojmenujte soubor třídy **BookDetails.cs**a pak klikněte na **Přidat**.
   5. Po otevření souboru **BookDetails.cs** nahraďte kód v souboru následujícím kódem: 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample4.cs)]
   6. Uložte a zavřete soubor **BookDetails.cs** .

6. Aktualizujte třídu **MainViewModel.cs** tak, aby zahrnovala funkce pro komunikaci s aplikací webového rozhraní API pro Bookstore:

   1. Rozbalte složku **ViewModels** v Průzkumníku řešení a dvakrát klikněte na soubor **MainViewModel.cs** .
   2. Po otevření souboru **MainViewModel.cs** nahraďte kód v souboru následujícím kódem: Všimněte si, že budete muset aktualizovat hodnotu `apiUrl` konstanty se skutečnou adresou URL webového rozhraní API: 

       [!code-csharp[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample5.cs)]
   3. Uložte a zavřete soubor **MainViewModel.cs** .

7. Chcete-li přizpůsobit název aplikace, aktualizujte soubor **MainPage. XAML** :

   1. Dvakrát klikněte na soubor **MainPage. XAML** v Průzkumníkovi řešení.
   2. Po otevření souboru **MainPage. XAML** vyhledejte následující řádky kódu: 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample6.xml)]
   3. Nahraďte tyto řádky následujícím způsobem: 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample7.xml)]
   4. Uložte a zavřete soubor **MainPage. XAML** .

8. Chcete-li upravit zobrazené položky, aktualizujte soubor **DetailsPage. XAML** :

   1. Dvakrát klikněte na soubor **DetailsPage. XAML** v Průzkumníkovi řešení.
   2. Po otevření souboru **DetailsPage. XAML** vyhledejte následující řádky kódu: 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample8.xml)]
   3. Nahraďte tyto řádky následujícím způsobem: 

       [!code-xml[Main](calling-web-api-from-a-windows-phone-8-application/samples/sample9.xml)]
   4. Uložte a zavřete soubor **DetailsPage. XAML** .

9. Sestavte aplikaci Windows Phone pro kontrolu chyb.

### <a name="step-3-testing-the-end-to-end-solution"></a>Krok 3: testování kompletního řešení

Jak je uvedeno v části *požadavky* v tomto kurzu, když testujete připojení mezi WEBOVÝm rozhraním api a Windows Phone 8 projektů v místním systému, budete muset postupovat podle pokynů v článku *[připojení emulátoru Windows Phone 8 k webovým aplikacím API v místním počítači](https://go.microsoft.com/fwlink/?LinkId=324014)* , abyste mohli nastavit testovací prostředí.

Po nakonfigurování testovacího prostředí budete muset nastavit aplikaci Windows Phone jako spouštěný projekt. Provedete to tak, že v Průzkumníku řešení zvýrazníte aplikaci **BookCatalog** a pak kliknete na **nastavit jako spouštěný projekt**:

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image6.png)](calling-web-api-from-a-windows-phone-8-application/_static/image5.png) |
| --- |
| Rozbalte kliknutím na obrázek. |

Když stisknete klávesu F5, Visual Studio spustí emulátor Windows Phone, který zobrazí &quot;při načítání dat aplikace z webového rozhraní API počkat&quot; zprávu:

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image8.png)](calling-web-api-from-a-windows-phone-8-application/_static/image7.png) |
| --- |
| Rozbalte kliknutím na obrázek. |

Pokud je všechno úspěšné, měli byste vidět zobrazený katalog:

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image10.png)](calling-web-api-from-a-windows-phone-8-application/_static/image9.png) |
| --- |
| Rozbalte kliknutím na obrázek. |

Pokud klepnete na název knihy, aplikace zobrazí popis knihy:

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image12.png)](calling-web-api-from-a-windows-phone-8-application/_static/image11.png) |
| --- |
| Rozbalte kliknutím na obrázek. |

Pokud aplikace nemůže komunikovat s webovým rozhraním API, zobrazí se chybová zpráva:

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image14.png)](calling-web-api-from-a-windows-phone-8-application/_static/image13.png) |
| --- |
| Rozbalte kliknutím na obrázek. |

Pokud klepnete na chybovou zprávu, zobrazí se další podrobnosti o této chybě:

| [![](calling-web-api-from-a-windows-phone-8-application/_static/image16.png)](calling-web-api-from-a-windows-phone-8-application/_static/image15.png) |
|-------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                                                 Rozbalte kliknutím na obrázek.                                                                 |

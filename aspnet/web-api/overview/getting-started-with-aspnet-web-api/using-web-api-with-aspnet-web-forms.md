---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: Použití webového rozhraní API s ASP.NET webovými formuláři – ASP.NET 4. x
author: MikeWasson
description: Kurz s kódem krok za krokem k přidání webového rozhraní API do aplikace ASP.NET Forms pro ASP.NET 4. x
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556775"
---
# <a name="using-web-api-with-aspnet-web-forms"></a>Použití rozhraní Web API s webovými formuláři ASP.NET

o [Jan Wasson](https://github.com/MikeWasson)

Tento kurz vás provede jednotlivými kroky přidání webového rozhraní API do tradiční aplikace webových formulářů ASP.NET v ASP.NET 4. x. 

## <a name="overview"></a>Přehled

I když je webové rozhraní API ASP.NET zabalené s ASP.NET MVC, je snadné přidat webové rozhraní API do tradiční aplikace webové formuláře ASP.NET.

Chcete-li použít webové rozhraní API v aplikaci webových formulářů, existují dva hlavní kroky:

- Přidejte kontroler webového rozhraní API, který je odvozený od třídy **ApiController** .
- Přidejte směrovací tabulku do **aplikace\_spustit** metodu.

## <a name="create-a-web-forms-project"></a>Vytvoření projektu webových formulářů

Spusťte Visual Studio a na **úvodní** stránce vyberte **Nový projekt** . Nebo v nabídce **soubor** vyberte **Nový** a pak **projekt**.

V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte uzel  **C# vizuál** . V **části C#vizuál** vyberte **Web**. V seznamu šablon projektu vyberte **ASP.NET aplikace webových formulářů**. Zadejte název projektu a klikněte na tlačítko **OK**.

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a>Vytvoření modelu a kontroleru

V tomto kurzu se jako [Začínáme](tutorial-your-first-web-api.md) kurz používá stejný model a třídy kontroleru.

Nejprve přidejte třídu modelu. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt a vyberte **Přidat třídu**. Pojmenujte produkt třídy a přidejte následující implementaci:

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

V dalším kroku přidejte do projektu kontroler webového rozhraní API. *kontroler* je objekt, který zpracovává požadavky HTTP na webové rozhraní API.

V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt. Vyberte možnost **Přidat novou položku**.

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

V části **Nainstalované šablony**rozbalte **položku C# vizuál** a vyberte možnost **Web**. Pak ze seznamu šablon vyberte **Třída kontroleru webového rozhraní API**. Pojmenujte kontroler "ProductsController" a klikněte na **Přidat**.

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

Průvodce **přidáním nové položky** vytvoří soubor s názvem ProductsController.cs. Odstraňte metody, které průvodce zahrnul, a přidejte následující metody:

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

Další informace o kódu v tomto kontroleru najdete v kurzu [Začínáme](tutorial-your-first-web-api.md) .

## <a name="add-routing-information"></a>Přidat informace o směrování

Dále přidáte trasu identifikátoru URI, aby byly identifikátory URI formuláře &quot;/API/Products/&quot; směrovány do kontroleru.

V **Průzkumník řešení**dvakrát klikněte na Global. asax a otevřete soubor kódu na pozadí Global.asax.cs. Přidejte následující příkaz **using** .

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

Poté do aplikace přidejte následující kód **\_počáteční** metoda:

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

Další informace o směrovacích tabulkách najdete v tématu [směrování ve webovém rozhraní API ASP.NET](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).

## <a name="add-client-side-ajax"></a>Add Client-Side AJAX

To je všechno, co potřebujete k vytvoření webového rozhraní API, ke kterému mají přístup klienti. Nyní přidáme stránku HTML, která používá jQuery k volání rozhraní API.

Ujistěte se, že vaše stránka předlohy (například *site. Master*) obsahuje `ContentPlaceHolder` `ID="HeadContent"`:

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

Otevřete soubor default. aspx. Nahraďte často používaný text v části hlavní obsah, jak je znázorněno níže:

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

Dále do oddílu `HeaderContent` přidejte odkaz na zdrojový soubor jQuery:

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

Poznámka: odkaz na skript lze snadno přidat přetažením z **Průzkumník řešení** do okna Editor kódu.

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

Pod značkou skriptu jQuery přidejte následující blok skriptu:

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

Když se dokument načte, vytvoří tento skript požadavek AJAX, aby &quot;API/Products&quot;. Požadavek vrátí seznam produktů ve formátu JSON. Skript přidá informace o produktu do tabulky HTML.

Při spuštění aplikace by měla vypadat takto:

![](using-web-api-with-aspnet-web-forms/_static/image5.png)

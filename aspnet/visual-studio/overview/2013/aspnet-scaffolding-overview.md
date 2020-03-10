---
uid: visual-studio/overview/2013/aspnet-scaffolding-overview
title: ASP.NET generování uživatelského rozhraní v Visual Studio 2013 | Microsoft Docs
author: Rick-Anderson
description: ASP.NET generování uživatelského rozhraní je nová funkce, která je součástí Visual Studio 2013.
ms.author: riande
ms.date: 04/09/2014
ms.assetid: a41ec9d4-8287-4f31-9e2a-460e7b7f04be
msc.legacyurl: /visual-studio/overview/2013/aspnet-scaffolding-overview
msc.type: authoredcontent
ms.openlocfilehash: cf4669b769cee28475e2dd6a6ddf07ea1434d04d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557979"
---
# <a name="aspnet-scaffolding-in-visual-studio-2013"></a>Vygenerování uživatelského rozhraní ASP.NET v sadě Visual Studio 2013

tím, že [FitzMacken](https://github.com/tfitzmac)

> ASP.NET generování uživatelského rozhraní je nová funkce, která je součástí Visual Studio 2013.

## <a name="overview"></a>Přehled

Generování uživatelského rozhraní ASP.NET je rozhraní pro generování kódu pro webové aplikace v ASP.NET. Visual Studio 2013 obsahuje předem instalované generátory kódu pro MVC a projekty webového rozhraní API. Pokud chcete rychle přidat kód, který komunikuje s datovými modely, přidejte do projektu generování uživatelského rozhraní. Použití generování uživatelského rozhraní může zkrátit dobu vývoje standardních datových operací v projektu.

Ve výchozím nastavení Visual Studio 2013 nepodporuje generování kódu pro projekt webových formulářů, ale můžete použít generování uživatelského rozhraní s webovými formuláři, a to buď přidáním závislosti MVC do projektu, nebo instalací rozšíření. Oba přístupy jsou uvedené níže.

Visual Studio 2013 Update 2 (aktuálně RC) poskytuje možnost rozšiřování ASP.NET generování uživatelského rozhraní tak, aby splňovalo požadavky vašeho scénáře. Pomocí této funkce můžete vytvořit vlastní šablonu generování uživatelského rozhraní a přidat ji do dialogového okna Přidat nové generování uživatelského rozhraní. V rámci vlastní šablony určíte kód, který se generuje při přidávání vygenerované položky. Další informace najdete v tématu [Vytvoření vlastního lešení pro Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).

## <a name="prerequisites"></a>Předpoklady

Chcete-li použít generování uživatelského rozhraní ASP.NET, musíte mít:

- Microsoft Visual Studio 2013
- Web Vývojářské nástroje (součást výchozí instalace Visual Studio 2013)
- ASP.NET webová rozhraní a nástroje 2013 (součást výchozí instalace Visual Studio 2013)

## <a name="add-a-scaffolded-item-to-mvc-or-web-api"></a>Přidání vygenerované položky do MVC nebo webového rozhraní API

Chcete-li přidat generování uživatelského rozhraní, klikněte pravým tlačítkem myši buď na projekt, nebo na složku v rámci projektu, a vyberte možnost **Přidat** – **Nová vygenerovaná položka**, jak je znázorněno na následujícím obrázku.

![Přidat položku uživatelského rozhraní](aspnet-scaffolding-overview/_static/image1.png)

V okně **Přidat generování uživatelského rozhraní** vyberte typ uživatelského rozhraní, které chcete přidat.

![Vybrat typ uživatelského rozhraní](aspnet-scaffolding-overview/_static/image2.png)

Okno **Přidat kontrolér** nabízí možnost vybrat možnosti pro vygenerování kontroleru, včetně toho, jestli chcete použít nové asynchronní funkce z Entity Framework 6.

![Přidat kontroler](aspnet-scaffolding-overview/_static/image3.png)

Pro váš scénář jsou vytvořeny relevantní třídy a stránky. Například následující obrázek ukazuje kontroler MVC a zobrazení, které byly vytvořeny pomocí generování uživatelského rozhraní pro třídu modelu s názvem filmy.

![Vytvořené soubory](aspnet-scaffolding-overview/_static/image4.png)

## <a name="add-a-scaffolded-item-to-web-forms"></a>Přidání vygenerované položky do webových formulářů

Chcete-li přidat generování uživatelského rozhraní, které generuje kód webových formulářů, je nutné buď nainstalovat rozšíření do sady Visual Studio, nebo přidat závislosti MVC. Oba přístupy jsou uvedené níže, ale stačí udělat jenom jeden z těchto přístupů.

### <a name="web-forms-scaffolding-extension"></a>Rozšíření pro generování uživatelského rozhraní webových formulářů

Můžete nainstalovat rozšíření sady Visual Studio, které vám umožní používat generování uživatelského rozhraní s projektem webových formulářů. V aplikaci Visual Studio vyberte **nástroje** a pak **rozšíření a aktualizace**. Z tohoto dialogového okna vyhledejte galerii sady Visual Studio pro **vygenerování uživatelského rozhraní webových formulářů**.

![instalace generování uživatelského rozhraní webových formulářů](aspnet-scaffolding-overview/_static/image5.png)

Další informace najdete v tématu [generování uživatelského rozhraní webových formulářů](https://go.microsoft.com/fwlink/p/?LinkId=396478).

### <a name="mvc-dependencies"></a>Závislosti MVC

Chcete-li přidat závislosti MVC, vyberte **přidat** - **Nová vygenerovaná položka**. V okně Přidat generování uživatelského rozhraní vyberte **závislosti MVC**, jak je znázorněno níže.

![přidat závislosti MVC](aspnet-scaffolding-overview/_static/image6.png)

K dispozici jsou dvě možnosti pro generování uživatelského rozhraní MVC; Minimální a plná. Pokud vyberete minimální, do projektu se přidají jenom balíčky NuGet a odkazy pro ASP.NET MVC. Pokud vyberete možnost úplná, budou přidány minimální závislosti a také požadované soubory obsahu pro projekt MVC. Chcete-li snadno používat generování uživatelského rozhraní, vyberte možnost úplné závislosti.

![Výběr úplných závislostí](aspnet-scaffolding-overview/_static/image7.png)

Po přidání závislostí se zobrazí soubor **Readme. txt** . Pečlivě postupujte podle pokynů v tomto souboru a ujistěte se, že váš projekt funguje správně.

Po dokončení kroků v souboru Readme. txt můžete přidat novou vygenerované položky, jak je znázorněno v předchozí části o MVC a webovém rozhraní API. Automaticky vygenerovaná zobrazení a kontroler budou správně fungovat v rámci projektu.

## <a name="tutorials"></a>Kurzy

Chcete-li vytvořit přizpůsobený generátor, přečtěte si téma [Vytvoření vlastního lešení pro Visual Studio](https://go.microsoft.com/fwlink/p/?LinkId=395029).

Chcete-li přizpůsobit vygenerované soubory, přečtěte si téma [jak přizpůsobit vygenerované soubory z dialogového okna nové vygenerované položky](https://blogs.msdn.com/b/webdev/archive/2013/12/26/how-to-customize-the-generated-files-from-the-new-scaffolded-item-dialog.aspx).

Příklad použití generování uživatelského rozhraní s **Database Firstm vývojem**naleznete v tématu [EF Database First with ASP.NET MVC](../../../mvc/overview/getting-started/database-first-development/setting-up-database.md).

Příklad použití generování uživatelského rozhraní v projektu **MVC** najdete v tématu [Začínáme s ASP.NET MVC 5](../../../mvc/overview/getting-started/introduction/getting-started.md).

Příklad použití generování uživatelského rozhraní v projektu **webového rozhraní API** najdete v tématu [Vytvoření REST API s směrováním atributů ve webovém rozhraní API 2](../../../web-api/overview/web-api-routing-and-actions/create-a-rest-api-with-attribute-routing.md).

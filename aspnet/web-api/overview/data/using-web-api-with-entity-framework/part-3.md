---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: Použití Migrace Code First k osazení databáze | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: 257bd06848adb949330856cc71eeb3d685e9d036
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557454"
---
# <a name="use-code-first-migrations-to-seed-the-database"></a>Použití Migrace Code First k osazení databáze

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://github.com/MikeWasson/BookService)

V této části použijete [migrace Code First](https://msdn.microsoft.com/data/jj591621) v EF k osazení databáze s testovacími daty.

V nabídce **nástroje** vyberte **Správce balíčků NuGet**a pak vyberte **Konzola správce balíčků**. V okně konzoly Správce balíčků zadejte následující příkaz:

[!code-console[Main](part-3/samples/sample1.cmd)]

Tento příkaz přidá do projektu složku s názvem migrace a ve složce Migraces vytvoří soubor kódu s názvem Configuration.cs.

![](part-3/_static/image1.png)

Otevřete soubor Configuration.cs. Přidejte následující příkaz **using** .

[!code-csharp[Main](part-3/samples/sample2.cs)]

Poté do metody **Configuration. Seed** přidejte následující kód:

[!code-csharp[Main](part-3/samples/sample3.cs)]

V okně konzoly Správce balíčků zadejte následující příkazy:

[!code-console[Main](part-3/samples/sample4.cmd)]

První příkaz vygeneruje kód, který vytvoří databázi, a druhý příkaz spustí tento kód. Databáze je vytvořena lokálně pomocí [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx).

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a>Prozkoumat rozhraní API (volitelné)

Stisknutím klávesy F5 spusťte aplikaci v režimu ladění. Visual Studio spustí IIS Express a spustí vaši webovou aplikaci. Visual Studio potom spustí prohlížeč a otevře domovskou stránku aplikace.

Když Visual Studio spustí webový projekt, přiřadí číslo portu. Na následujícím obrázku je číslo portu 50524. Při spuštění aplikace se zobrazí jiné číslo portu.

![](part-3/_static/image3.png)

Domovská stránka se implementuje pomocí ASP.NET MVC. V horní části stránky je odkaz, který říká "rozhraní API". Tento odkaz vám umožní automaticky vygenerovanou stránku s nápovědu pro webové rozhraní API. (Pokud se chcete dozvědět, jak se tato stránka této stránky vygenerovala, a jak na stránku přidat vlastní dokumentaci, přečtěte si téma [Vytvoření stránek s nápovědu pro webové rozhraní API ASP.NET](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) Kliknutím na odkazy na stránku v nápovědě zobrazíte podrobnosti o rozhraní API, včetně formátu požadavků a odpovědí.

![](part-3/_static/image4.png)

Rozhraní API povoluje operace CRUD v databázi. Následující shrnuje rozhraní API.

| Autoři |  |
| --- | -- |
| GET api/authors | Získá všechny autory. |
| GET api/authors/{id} | Získejte autora podle ID. |
| POST /api/authors | Vytvořit nového autora |
| PUT /api/authors/{id} | Aktualizace existujícího autora |
| DELETE /api/authors/{id} | Odstraní autora. |

| Knihy |  |
| --- | -- |
| GET /api/books | Získejte všechny knihy. |
| GET /api/books/{id} | Získat knihu podle ID |
| POST /api/books | Vytvořte novou knihu. |
| PUT /api/books/{id} | Aktualizuje existující knihu. |
| DELETE /api/books/{id} | Odstraní knihu. |

## <a name="view-the-database-optional"></a>Zobrazit databázi (volitelné)

Při spuštění příkazu Update-Database se v EF vytvořila databáze a volala se metoda `Seed`. Když aplikaci spouštíte místně, EF používá [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx). Databázi můžete zobrazit v aplikaci Visual Studio. V nabídce **Zobrazení** vyberte **Průzkumník objektů systému SQL Server**.

![](part-3/_static/image5.png)

V dialogovém okně **připojit k serveru** zadejte do pole **název serveru** text "(LocalDB) \v11.0". U možnosti **ověřování** ponechte možnost ověřování systému Windows. Klikněte na **Připojit**.

![](part-3/_static/image6.png)

Visual Studio se připojí k LocalDB a zobrazí vaše existující databáze v okně Průzkumník objektů systému SQL Server. Uzly můžete rozbalit a zobrazit tak tabulky, které jsme vytvořili v EF.

![](part-3/_static/image7.png)

Data zobrazíte tak, že kliknete pravým tlačítkem na tabulku a vyberete **Zobrazit data**.

![](part-3/_static/image8.png)

Následující snímek obrazovky ukazuje výsledky pro tabulku Books. Všimněte si, že EF naplnilo databázi daty počáteční hodnoty a tabulka obsahuje cizí klíč do tabulky autoři.

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> [Předchozí](part-2.md)
> [Další](part-4.md)

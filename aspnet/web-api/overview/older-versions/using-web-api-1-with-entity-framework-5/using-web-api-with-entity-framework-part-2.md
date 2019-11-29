---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
title: 'Část 2: vytvoření doménových modelů | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: fe3ef85f-bdc6-4e10-9768-25aa565c01d0
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
msc.type: authoredcontent
ms.openlocfilehash: 7c5ed1bdb4b390c94907b14e208231f16ad42d96
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600357"
---
# <a name="part-2-creating-the-domain-models"></a>Část 2: vytvoření doménových modelů

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-models"></a>Přidat modely

Existují tři způsoby přístupu k Entity Framework:

- Databáze – první: začnete s databází a Entity Framework generuje kód.
- Model – první: začnete s vizuálním modelem a Entity Framework generuje databázi i kód.
- First Code: Začněte s kódem a Entity Framework vygeneruje databázi.

Používáme přístup k prvnímu kódu, takže začneme definováním našich objektů domény jako POCOs (objekty CLR ve starém Old). V případě přístupu k prvnímu kódu objekty domény nepotřebují žádný další kód pro podporu databázové vrstvy, jako jsou transakce nebo trvalost. (Konkrétně není nutné dědit od třídy [objektů EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) .) K řízení způsobu, jakým Entity Framework vytváří schéma databáze, můžete i nadále používat datové poznámky.

Vzhledem k tomu, že POCOs neobsahují žádné další vlastnosti, které popisují [stav databáze](https://msdn.microsoft.com/library/system.data.entitystate.aspx), mohou být snadno serializovány do formátu JSON nebo XML. To ale znamená, že byste měli vždy zveřejnit vaše Entity Framework modely přímo na klienty, jak uvidíme později v tomto kurzu.

Vytvoříme následující POCOs:

- Produkt
- Za
- OrderDetail

Chcete-li vytvořit každou třídu, klikněte pravým tlačítkem myši na složku modely v Průzkumník řešení. V místní nabídce vyberte **Přidat** a pak vyberte **Třída.**

![](using-web-api-with-entity-framework-part-2/_static/image1.png)

Přidejte třídu `Product` s následující implementací:

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample1.cs)]

Podle konvence Entity Framework používá vlastnost `Id` jako primární klíč a mapuje ji na sloupec identity v tabulce databáze. Když vytvoříte novou instanci `Product`, nenastavíte hodnotu pro `Id`, protože databáze generuje hodnotu.

Atribut **ScaffoldColumn** určuje, že ASP.NET MVC přeskočí vlastnost `Id` při generování formuláře editoru. **Požadovaný** atribut se používá k ověření modelu. Určuje, že vlastnost `Name` musí být neprázdný řetězec.

Přidejte třídu `Order`:

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample2.cs)]

Přidejte třídu `OrderDetail`:

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample3.cs)]

## <a name="foreign-key-relations"></a>Vztahy cizího klíče

Jedna objednávka obsahuje mnoho podrobností objednávky a jednotlivé podrobnosti objednávky se vztahují na jeden produkt. Pro reprezentaci těchto vztahů třída `OrderDetail` definuje vlastnosti pojmenované `OrderId` a `ProductId`. Entity Framework odvodí, že tyto vlastnosti reprezentují cizí klíče, a přidá do databáze omezení pro cizí klíč.

![](using-web-api-with-entity-framework-part-2/_static/image2.png)

Třídy `Order` a `OrderDetail` také zahrnují "navigační" vlastnosti, které obsahují odkazy na související objekty. V pořadí podle vlastností navigace můžete přejít na produkty v pořadí.

Zkompilujte projekt nyní. Entity Framework používá reflexi ke zjištění vlastností modelů, takže vyžaduje zkompilované sestavení pro vytvoření schématu databáze.

## <a name="configure-the-media-type-formatters"></a>Konfigurace formátovacích modulů typu média

[Formátovací modul typu Media](../../formats-and-model-binding/media-formatters.md) je objekt, který serializace data při zápisu textu odpovědi HTTP do webového rozhraní API. Vestavěné formátovací moduly podporují výstup JSON a XML. Ve výchozím nastavení oba tyto formátovací moduly serializovat všechny objekty podle hodnoty.

Při serializaci hodnotou se vytvoří problém, pokud graf objektu obsahuje cyklické odkazy. To je přesně případ u tříd `Order` a `OrderDetail`, protože každá z nich obsahuje odkaz na druhou. Formátování bude následovat po odkazech, psaní každého objektu podle hodnoty a jít v kruzích. Proto musíme změnit výchozí chování.

V Průzkumník řešení rozbalte složku App\_Start Folder a otevřete soubor s názvem WebApiConfig.cs. Do `WebApiConfig` třídy přidejte následující kód:

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample4.cs?highlight=11)]

Tento kód nastaví formátovací modul JSON tak, aby zachoval odkazy na objekty, a odstraní formátovací modul XML z kanálu zcela. (Formátovací modul XML můžete nastavit tak, aby zachoval odkazy na objekty, ale je to trochu víc práce a pro tuto aplikaci potřebujeme JSON. Další informace naleznete v tématu [zpracování cyklických odkazů na objekty](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).)

> [!div class="step-by-step"]
> [Předchozí](using-web-api-with-entity-framework-part-1.md)
> [Další](using-web-api-with-entity-framework-part-3.md)

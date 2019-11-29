---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
title: 'Část 6: vytváření řadičů produktu a objednávek | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 91ee29ee-0689-40ee-914a-e7dd733b6622
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
msc.type: authoredcontent
ms.openlocfilehash: e0bf88e3477acbde910cde956042449bc86ce79a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600026"
---
# <a name="part-6-creating-product-and-order-controllers"></a>Část 6: vytváření řadičů produktu a objednávek

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a>Přidat kontroler produktů

Kontroler správců je pro uživatele, kteří mají oprávnění správce. Zákazníci můžou na druhé straně zobrazovat produkty, ale nemůžou je vytvořit, aktualizovat ani odstranit.

Přístup k metodám post, PUT a DELETE můžeme snadno omezit, zatímco metody Get jsou otevřené. Podívejte se ale na data vrácená produktem:

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

Vlastnost `ActualCost` by se neměla zobrazovat zákazníkům. Řešením je definování *objektu pro přenos dat* (DTO), který obsahuje podmnožinu vlastností, které by měly být viditelné pro zákazníky. Pro `ProductDTO` instancí budeme používat technologii LINQ to Project `Product` Instances.

Do složky modely přidejte třídu s názvem `ProductDTO`.

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

Nyní přidejte kontroler. V Průzkumník řešení klikněte pravým tlačítkem myši na složku Controllers. Vyberte **Přidat**a pak vybrat **kontroler**. V dialogovém okně **Přidat řadič** pojmenujte kontrolér &quot;ProductsController&quot;. V části **Šablona**vyberte **prázdný kontroler rozhraní API**.

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

Nahraďte vše ve zdrojovém souboru následujícím kódem:

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

Kontroler stále používá `OrdersContext` k dotazování databáze. Místo toho, aby se přímo vracely `Product` Instances, voláme `MapProducts`, aby je provedla na `ProductDTO` instancí:

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

Metoda `MapProducts` vrací rozhraní **IQueryable**, takže můžeme výsledek sestavit s ostatními parametry dotazu. Můžete to vidět v metodě `GetProduct`, která do dotazu přidá klauzuli **WHERE** :

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a>Přidat řadič objednávek

Dále přidejte kontroler, který umožňuje uživatelům vytvářet a zobrazovat objednávky.

Začneme s jiným DTO. V Průzkumník řešení klikněte pravým tlačítkem na složku modely a přidejte třídu s názvem `OrderDTO` použijte následující implementaci:

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

Nyní přidejte kontroler. V Průzkumník řešení klikněte pravým tlačítkem myši na složku Controllers. Vyberte **Přidat**a pak vybrat **kontroler**. V dialogovém okně **Přidat řadič** nastavte následující možnosti:

- V části **název kontroleru**zadejte "OrdersController".
- V části **Šablona**vyberte možnost kontroler API s akcemi čtení/zápisu pomocí Entity Framework.
- V části **třída modelu**vyberte &quot;Order (ProductStore. Models)&quot;.
- V části **Třída kontextu dat**vyberte &quot;OrdersContext (ProductStore. Models)&quot;.

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

Klikněte na tlačítko **Přidat**. Tím se přidá soubor s názvem OrdersController.cs. Dál je potřeba upravit výchozí implementaci kontroleru.

Nejprve odstraňte metody `PutOrder` a `DeleteOrder`. V této ukázce zákazníci nemůžou upravovat ani odstraňovat existující objednávky. V reálné aplikaci budete potřebovat spoustu back-endové logiky, která tyto případy zpracovává. (Například bylo objednávka již expedována?)

Změňte metodu `GetOrders` tak, aby vracela pouze objednávky, které patří uživateli:

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

Změňte metodu `GetOrder` následujícím způsobem:

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

Zde jsou změny, které jsme provedli v metodě:

- Návratová hodnota je instance `OrderDTO` namísto `Order`.
- Při dotazování databáze pro objednávku používáme metodu [DbQuery. include](https://msdn.microsoft.com/library/gg696395) k načtení souvisejících entit `OrderDetail` a `Product`.
- Výsledek se sloučí s využitím projekce.

Odpověď HTTP bude obsahovat pole produktů s množstvím:

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

Tento formát je snazší, aby klienti využili oproti původnímu grafu objektů, který obsahuje vnořené entity (pořadí, podrobnosti a produkty).

Poslední metoda, kterou je třeba zvážit `PostOrder`. V tuto chvíli Tato metoda používá instanci `Order`. Ale zvažte, co se stane, když klient pošle text požadavku takto:

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

Toto je dobře strukturované pořadí a Entity Framework je Happily vložit do databáze. Obsahuje však produktovou entitu, která nebyla dříve k dispozici. Klient právě vytvořil v naší databázi nový produkt! V případě, že se jim zobrazí objednávka Koala, bude to u oddělení pro plnění objednávek neočekávaně. Morální je, buďte pozorně opatrní na data, která přijmete v žádosti POST nebo PUT.

Chcete-li se tomuto problému vyhnout, změňte metodu `PostOrder` tak, aby převzala instanci `OrderDTO`. `Order`vytvořte pomocí `OrderDTO`.

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

Všimněte si, že používáme vlastnosti `ProductID` a `Quantity` a ignorujeme všechny hodnoty, které klient poslal pro název produktu nebo cenu. Pokud ID produktu není platné, porušuje se omezení cizího klíče v databázi a vložení se nezdaří, jak by mělo.

Toto je kompletní `PostOrder` metoda:

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

Nakonec přidejte do kontroleru atribut **autorizace** :

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

V současné době můžou objednávky vytvářet nebo zobrazovat jenom registrovaní uživatelé.

> [!div class="step-by-step"]
> [Předchozí](using-web-api-with-entity-framework-part-5.md)
> [Další](using-web-api-with-entity-framework-part-7.md)

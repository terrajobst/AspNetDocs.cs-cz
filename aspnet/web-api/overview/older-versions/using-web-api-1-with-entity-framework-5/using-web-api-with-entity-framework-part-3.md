---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
title: 'Část 3: vytvoření kontroleru správce | Microsoft Docs'
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 6b9ae3c4-0274-4170-a1bb-9df9c546b2a9
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
msc.type: authoredcontent
ms.openlocfilehash: f39be7a84e85db93487d246e9f8cb59c401fe5ce
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600033"
---
# <a name="part-3-creating-an-admin-controller"></a>3\. část: vytvoření kontroleru správce

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-controller"></a>Přidat kontroler správce

V této části přidáme kontroler webového rozhraní API, který podporuje operace CRUD (vytváření, čtení, aktualizace a odstraňování) na produktech. Kontroler použije Entity Framework ke komunikaci s databázovou vrstvou. Pouze správci budou moci použít tento kontroler. Zákazníci budou k produktům přistupovat přes jiný kontroler.

V Průzkumník řešení klikněte pravým tlačítkem myši na složku Controllers. Vyberte **Přidat** a potom **kontroler**.

![](using-web-api-with-entity-framework-part-3/_static/image1.png)

V dialogovém okně **Přidat řadič zadejte** název kontroleru `AdminController`. V části **Šablona**vyberte &quot;Controller rozhraní API s akcemi čtení/zápisu pomocí Entity Framework&quot;. V části **třída modelu**vyberte produkt (ProductStore. Models). V části **datový kontext**vyberte&lt;nový kontext dat&gt;.

![](using-web-api-with-entity-framework-part-3/_static/image2.png)

> [!NOTE]
> Pokud rozevírací seznam **třídy modelu** nezobrazuje žádné třídy modelu, ujistěte se, že jste projekt kompilováni. Entity Framework používá reflexi, takže potřebuje zkompilované sestavení.

Vybráním možnosti&lt;nový kontext dat&gt;se otevře dialogové okno **nový kontext** dat. Pojmenujte `ProductStore.Models.OrdersContext`datový kontext.

![](using-web-api-with-entity-framework-part-3/_static/image3.png)

Kliknutím na tlačítko **OK** zavřete dialogové okno **nový kontext dat** . V dialogovém okně **Přidat řadič** klikněte na **Přidat**.

Tady je postup přidaný do projektu:

- Třída s názvem `OrdersContext`, která je odvozena z **DbContext**. Tato třída poskytuje připevňování mezi modely POCO a databází.
- Kontroler webového rozhraní API s názvem `AdminController`. Tento kontroler podporuje operace CRUD pro instance `Product`. Používá třídu `OrdersContext` ke komunikaci s Entity Framework.
- Nový připojovací řetězec databáze v souboru Web. config.

![](using-web-api-with-entity-framework-part-3/_static/image4.png)

Otevřete soubor OrdersContext.cs. Všimněte si, že konstruktor určuje název připojovacího řetězce databáze. Tento název odkazuje na připojovací řetězec, který byl přidán do souboru Web. config.

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample1.cs)]

Do `OrdersContext` třídy přidejte následující vlastnosti:

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample2.cs)]

**Negenerickými** představuje sadu entit, na které se dá dotazovat. Zde je kompletní seznam pro třídu `OrdersContext`:

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample3.cs)]

Třída `AdminController` definuje pět metod, které implementují základní funkce CRUD. Každá metoda odpovídá identifikátoru URI, který může klient vyvolat:

| Metoda kontroleru | Popis | URI | HTTP – metoda |
| --- | --- | --- | --- |
| GetProducts | Načte všechny produkty. | rozhraní API/produkty | GET |
| Getproduct | Vyhledá produkt podle ID. | API/Products/*ID* | GET |
| PutProduct | Aktualizuje produkt. | API/Products/*ID* | PŘEVÉST |
| PostProduct | Vytvoří nový produkt. | rozhraní API/produkty | POST |
| DeleteProduct | Odstraní produkt. | API/Products/*ID* | DELETE |

Každá metoda volá do `OrdersContext` dotazování databáze. Metody, které mění kolekci (PUT, POST a DELETE) volání `db.SaveChanges`, aby zachovaly změny v databázi. Řadiče se vytvoří na žádost HTTP a pak se vyřadí, takže je nutné zachovat změny před tím, než se metoda vrátí.

## <a name="add-a-database-initializer"></a>Přidat inicializátor databáze

Entity Framework má skvělé funkce, která umožňuje naplnit databázi při spuštění a automaticky znovu vytvořit databázi vždy, když se změní modely. Tato funkce je užitečná při vývoji, protože máte vždy nějaká testovací data, a to i v případě, že změníte modely.

V Průzkumník řešení klikněte pravým tlačítkem na složku modely a vytvořte novou třídu s názvem `OrdersContextInitializer`. Vložit do následující implementace:

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample4.cs)]

Díky dědění z třídy **DropCreateDatabaseIfModelChanges** oznamujeme Entity Framework k vyřazení databáze pokaždé, když upravíte třídy modelu. Když Entity Framework vytvoří (nebo znovu vytvoří) databázi, zavolá metodu **počáteční** hodnoty k naplnění tabulek. Metoda **počáteční** hodnoty používáme k přidání některých ukázkových produktů plus Příklad objednávky.

Tato funkce je ideální pro testování, ale nepoužívejte třídu **DropCreateDatabaseIfModelChanges** v produkčním prostředí, protože byste mohli přijít o data, pokud někdo změní třídu modelu.

Dále otevřete Global. asax a přidejte následující kód do **aplikace\_spustit** metodu:

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample5.cs)]

## <a name="send-a-request-to-the-controller"></a>Odeslat žádost do kontroleru

V tuto chvíli jsme nenapsali žádný kód klienta, ale můžete vyvolat webové rozhraní API pomocí webového prohlížeče nebo ladicího nástroje HTTP, jako je [Fiddler](http://www.fiddler2.com/fiddler2/). V aplikaci Visual Studio stiskněte klávesu F5 pro spuštění ladění. Webový prohlížeč se otevře pro `http://localhost:*portnum*/`, kde *portnum* je nějaké číslo portu.

Odešle požadavek HTTP na`http://localhost:*portnum*/api/admin`. První požadavek může být pomalý, protože Entity Framework musí vytvořit a naplnit databázi. Odpověď by měla vypadat nějak takto:

[!code-console[Main](using-web-api-with-entity-framework-part-3/samples/sample6.cmd)]

> [!div class="step-by-step"]
> [Předchozí](using-web-api-with-entity-framework-part-2.md)
> [Další](using-web-api-with-entity-framework-part-4.md)

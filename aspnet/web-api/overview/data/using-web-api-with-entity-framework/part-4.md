---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-4
title: Zpracování vztahů entit | Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: d2f5710c-23c7-40a5-9cd9-5d0516570cba
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-4
msc.type: authoredcontent
ms.openlocfilehash: be4948e5443a5eb4e1824c63dd0c445a7ee1928e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557461"
---
# <a name="handling-entity-relations"></a>Ošetření relací prvků

o [Jan Wasson](https://github.com/MikeWasson)

[Stáhnout dokončený projekt](https://github.com/MikeWasson/BookService)

Tato část popisuje některé podrobnosti o tom, jak EF načte související entity, a jak zpracovat cyklické navigační vlastnosti ve třídách modelu. (Tato část poskytuje znalosti na pozadí a není nutná k dokončení tohoto kurzu. Pokud dáváte přednost, přejděte k [části 5.](part-5.md).)

## <a name="eager-loading-versus-lazy-loading"></a>Načítání Eager versus opožděné načítání

Při použití EF s relační databází je důležité pochopit, jak EF načítají související data.

Je také užitečné zobrazit dotazy SQL, které EF vygeneruje. Chcete-li trasovat SQL, přidejte do konstruktoru `BookServiceContext` následující řádek kódu:

[!code-csharp[Main](part-4/samples/sample1.cs)]

Pokud odešlete požadavek GET na/API/Books, vrátí se JSON podobný následujícímu:

[!code-console[Main](part-4/samples/sample2.cmd)]

Můžete vidět, že vlastnost Author má hodnotu null, i když kniha obsahuje platný AuthorId. To je proto, že EF nenačítá související entity autora. Protokol trasování pro dotaz SQL potvrzuje toto:

[!code-console[Main](part-4/samples/sample3.sql)]

Příkaz SELECT přijímá z tabulky Books a neodkazuje na tabulku autorů.

Pro referenci je zde metoda třídy `BooksController`, která vrací seznam knih.

[!code-csharp[Main](part-4/samples/sample4.cs)]

Pojďme se podívat, jak bychom mohli jako součást dat JSON vracet autora. Existují tři způsoby, jak načíst související data v Entity Framework: načítání Eager, opožděné načítání a explicitní načítání. Existují kompromisy s každou technikou, takže je důležité pochopit, jak fungují.

### <a name="eager-loading"></a>Eager načítání

Při *načítání Eager*načítá EF související entity jako součást počátečního databázového dotazu. K provedení Eager načítání použijte metodu rozšíření **System. data. entity. include** .

[!code-csharp[Main](part-4/samples/sample5.cs)]

Tato informace oznamuje EF, aby obsahovala data autora v dotazu. Pokud tuto změnu uděláte a spustíte aplikaci, data JSON teď vypadá takto:

[!code-console[Main](part-4/samples/sample6.cmd)]

Protokol trasování ukazuje, že EF provedl spojení s knihou a vytvářením tabulek.

[!code-console[Main](part-4/samples/sample7.cmd)]

### <a name="lazy-loading"></a>Opožděné načítání

Při opožděném načítání EF automaticky načte související entitu v případě, že je vlastnost navigace pro tuto entitu zpětně odkazovaná. Chcete-li povolit opožděné načítání, nastavte vlastnost navigace jako virtuální. Například ve třídě Book:

[!code-csharp[Main](part-4/samples/sample8.cs?highlight=6)]

Nyní zvažte následující kód:

[!code-csharp[Main](part-4/samples/sample9.cs)]

Když je povoleno opožděné načítání, přístup k vlastnosti `Author` v `books[0]` způsobí, že EF bude dotazovat databázi pro autora.

Opožděné načítání vyžaduje více databázových cest, protože EF odesílá dotaz pokaždé, když načte související entitu. Obecně platí, že pro objekty, které jste serializováni, chcete zakázat opožděné načítání. Serializátor musí číst všechny vlastnosti modelu, které aktivují načítání souvisejících entit. Například zde jsou dotazy SQL v případě, kdy EF serializace seznam knih s povoleným opožděným načtením. Můžete vidět, že EF vytvoří tři samostatné dotazy pro tři autory.

[!code-console[Main](part-4/samples/sample10.sql)]

Existují i časy, kdy možná budete chtít použít opožděné načítání. Eager načítání může způsobit, že EF generuje velmi složité spojení. Nebo možná budete potřebovat související entity pro malou podmnožinu dat a opožděné načítání by bylo efektivnější.

Jedním ze způsobů, jak zabránit problémům s serializací, je serializace objektů přenosu dat (DTO) místo objektů entit. Tento postup budu zobrazovat později v článku.

### <a name="explicit-loading"></a>Explicitní načítání

Explicitní načítání je podobné opožděnému načítání s tím rozdílem, že explicitně získáte související data v kódu; k tomu nedochází automaticky při přístupu k navigační vlastnosti. Explicitní načítání nabízí větší kontrolu nad tím, kdy načíst související data, ale vyžaduje další kód. Další informace o explicitním načítání najdete v tématu [načítání souvisejících entit](https://msdn.microsoft.com/data/jj574232#explicit).

## <a name="navigation-properties-and-circular-references"></a>Navigační vlastnosti a cyklické odkazy

Když jsme definovali knihu a tvorbu modelů, definovali jsme navigační vlastnost pro třídu `Book` pro relaci typu kniha – autor, ale v druhém směru jsme nedefinovali vlastnost navigace.

Co se stane, když přidáte odpovídající navigační vlastnost do třídy `Author`?

[!code-csharp[Main](part-4/samples/sample11.cs?highlight=7)]

To bohužel při serializaci modelů vytvoří problém. Pokud načtete související data, vytvoří se kruhový graf objektů.

![](part-4/_static/image1.png)

Pokud se formátovací modul JSON nebo XML pokusí o serializaci grafu, vyvolá výjimku. Tyto dva formátovací moduly vyvolávají odlišnou zprávu o výjimce. Tady je příklad pro formátovací modul JSON:

[!code-console[Main](part-4/samples/sample12.cmd)]

Tady je formátovací modul XML:

[!code-xml[Main](part-4/samples/sample13.xml)]

Jedním z řešení je použití DTO, který je popsán v následující části. Alternativně můžete nakonfigurovat formátovací moduly JSON a XML pro zpracování cyklů grafu. Další informace najdete v tématu [zpracování cyklických odkazů na objekty](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).

Pro tento kurz nepotřebujete `Author.Book` navigační vlastnost, takže ji můžete opustit.

> [!div class="step-by-step"]
> [Předchozí](part-3.md)
> [Další](part-5.md)

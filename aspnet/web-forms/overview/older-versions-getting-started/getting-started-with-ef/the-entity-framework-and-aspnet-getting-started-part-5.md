---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
title: Začínáme s Entity Framework 4,0 Database First a webovými formuláři ASP.NET 4 – část 5 | Microsoft Docs
author: tdykstra
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak pomocí Entity Framework vytvořit aplikace webových formulářů ASP.NET. Ukázková aplikace je...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: 24ad4379-3fb2-44dc-ba59-85fe0ffcb2ae
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-5
msc.type: authoredcontent
ms.openlocfilehash: 75328e67abb4295b619cac5423a9eb970942fff7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78527998"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-5"></a>Začínáme s Entity Framework 4,0 Database First a webovými formuláři ASP.NET 4 – část 5

tím, že [Dykstra](https://github.com/tdykstra)

> Ukázková webová aplikace společnosti Contoso University ukazuje, jak pomocí Entity Framework 4,0 a sady Visual Studio 2010 vytvářet aplikace webových formulářů ASP.NET. Informace o řadě kurzů najdete v [prvním kurzu v řadě](the-entity-framework-and-aspnet-getting-started-part-1.md) .

## <a name="working-with-related-data-continued"></a>Práce se souvisejícími daty – pokračování

V předchozím kurzu jste začali používat ovládací prvek `EntityDataSource` pro práci se souvisejícími daty. Zobrazili jste více úrovní hierarchie a upravili data ve vlastnostech navigace. V tomto kurzu budete dál pracovat se souvisejícími daty přidáním a odstraněním relací a přidáním nové entity, která má relaci k existující entitě.

Vytvoříte stránku, která přidá kurzy přiřazené k oddělením. Tato oddělení už existují a při vytváření nového kurzu zároveň navážete vztah mezi ním a stávajícím oddělením.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image1.png)

Vytvoříte také stránku, která pracuje s relací m:n, a to přiřazením instruktora k kurzu (přidáním vztahu mezi dvěma entitami, které vyberete) nebo odebráním instruktora z kurzu (odebráním relace mezi dvěma entitami, které jste Vyberte). V databázi se při přidání vztahu mezi instruktorem a kurzem přidá nový řádek, který se přidá do tabulky přidružení `CourseInstructor`. odebrání relace zahrnuje odstranění řádku z tabulky přidružení `CourseInstructor`. Nicméně to provedete v Entity Framework nastavením vlastností navigace, aniž by bylo třeba explicitně odkazovat na tabulku `CourseInstructor`.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image3.png)

## <a name="adding-an-entity-with-a-relationship-to-an-existing-entity"></a>Přidání entity s relací s existující entitou

Vytvořte novou webovou stránku s názvem *CoursesAdd. aspx* , která používá hlavní stránku *Web. Master* , a přidejte následující kód do ovládacího prvku `Content` s názvem `Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample1.aspx)]

Tento kód vytvoří ovládací prvek `EntityDataSource`, který vybere kurzy, který umožňuje vkládání a určuje obslužnou rutinu pro událost `Inserting`. Obslužnou rutinu použijete k aktualizaci `Department` navigační vlastnosti při vytvoření nové entity `Course`.

Značka také vytvoří ovládací prvek `DetailsView`, který se má použít pro přidání nových entit `Course`. Označení používá vázaná pole pro `Course` vlastnosti entity. Je nutné zadat hodnotu `CourseID`, protože se nejedná o pole vygenerované systémem. Místo toho je číslo kurzu, které se musí zadat ručně při vytvoření kurzu.

Použijete pole šablony pro `Department` navigační vlastnost, protože vlastnosti navigace nelze použít s ovládacími prvky `BoundField`. Pole Šablona poskytuje rozevírací seznam pro výběr oddělení. Rozevírací seznam je vázán na `Departments` sadu entit pomocí `Eval` místo `Bind`, protože nelze přímo svázat navigační vlastnosti, aby je bylo možné aktualizovat. Zadáte obslužnou rutinu pro událost `Init` ovládacího prvku `DropDownList`, abyste mohli uložit odkaz na ovládací prvek pro použití kódem, který aktualizuje `DepartmentID` cizí klíč.

V *CoursesAdd.aspx.cs* hned po deklaraci částečné třídy přidejte pole třídy, které bude obsahovat odkaz na ovládací prvek `DepartmentsDropDownList`:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample2.cs)]

Přidejte obslužnou rutinu pro událost `Init` ovládacího prvku `DepartmentsDropDownList`, abyste mohli uložit odkaz na ovládací prvek. To vám umožní získat hodnotu, kterou uživatel zadal, a použít ho k aktualizaci `DepartmentID` hodnoty `Course` entity.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample3.cs)]

Přidejte obslužnou rutinu pro událost `Inserting` ovládacího prvku `DetailsView`:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample4.cs)]

Když uživatel klikne na `Insert`, vyvolá se událost `Inserting` před vložením nového záznamu. Kód v obslužné rutině získá `DepartmentID` z ovládacího prvku `DropDownList` a použije ho k nastavení hodnoty, která bude použita pro vlastnost `DepartmentID` entity `Course`.

Entity Framework se postará o přidání tohoto kurzu do navigační vlastnosti `Courses` přidružené entity `Department`. Přidá také oddělení do navigační vlastnosti `Department` entity `Course`.

Spusťte stránku.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-5/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image5.png)

Zadejte ID, název, počet kreditů a vyberte oddělení a pak klikněte na **Vložit**.

Spusťte stránku *courses. aspx* a vyberte stejné oddělení, abyste viděli nový kurz.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-5/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image7.png)

## <a name="working-with-many-to-many-relationships"></a>Práce s relacemi M:n

Vztah mezi `Courses` sadou entit a sadou entit `People` je relace m:n. `Course` entita obsahuje navigační vlastnost s názvem `People`, která může obsahovat nula, jednu nebo více souvisejících entit `Person` entit (představujících instruktory přiřazené k učení tohoto kurzu). A `Person` entita má vlastnost navigace nazvanou `Courses`, která může obsahovat nula, jednu nebo více souvisejících entit `Course` entit (představujících kurzy, které instruktor má přiřazený k výuce). Jeden instruktor může naučit několik kurzů a jeden kurz může být výukou více instruktorů. V této části návodu přidáte a odeberete relace mezi `Person` a `Course` entitou aktualizací vlastností navigace souvisejících entit.

Vytvořte novou webovou stránku s názvem *InstructorsCourses. aspx* , která používá hlavní stránku *Web. Master* , a přidejte následující kód do ovládacího prvku `Content` s názvem `Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample5.aspx)]

Tento kód vytvoří ovládací prvek `EntityDataSource`, který načte název a `PersonID` `Person` entit pro instruktory. Ovládací prvek `DropDrownList` je svázán s ovládacím prvkem `EntityDataSource`. Ovládací prvek `DropDownList` určuje obslužnou rutinu pro událost `DataBound`. Pomocí této obslužné rutiny provedete vázání dvou rozevíracích seznamů, které zobrazují kurzy.

Značka také vytvoří následující skupinu ovládacích prvků, které se použijí pro přiřazení kurzu k vybranému instruktorovi:

- `DropDownList` ovládací prvek pro výběr kurzu, který se má přiřadit Tento ovládací prvek se naplní kurzy, které aktuálně nejsou přiřazené k vybranému instruktorovi.
- `Button` ovládací prvek pro zahájení přiřazení.
- `Label` ovládací prvek pro zobrazení chybové zprávy v případě, že přiřazení se nezdařilo.

Nakonec značka vytvoří také skupinu ovládacích prvků, které se použijí pro odebrání kurzu od vybraného instruktora.

V *InstructorsCourses.aspx.cs*přidejte příkaz using:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample6.cs)]

Přidejte metodu pro vyplňování dvou rozevíracích seznamů, které zobrazují kurzy:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample7.cs)]

Tento kód získá všechny kurzy ze sady entit `Courses` a získá kurzy z navigační vlastnosti `Courses` entity `Person` pro vybraného instruktora. Pak určuje, které kurzy jsou přiřazeny k tomuto instruktorovi a odpovídajícím způsobem naplní rozevírací seznamy.

Přidejte obslužnou rutinu pro událost `Click` `Assign`ho tlačítka:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample8.cs)]

Tento kód získá `Person` entitu pro vybraného instruktora, získá `Course` entitu pro vybraný kurz a přidá vybraný kurz do navigační vlastnosti `Courses` entity `Person` instruktoru. Poté uloží změny do databáze a znovu naplní rozevírací seznamy, takže výsledky lze zobrazit okamžitě.

Přidejte obslužnou rutinu pro událost `Click` `Remove`ho tlačítka:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample9.cs)]

Tento kód získá `Person` entitu pro vybraného instruktora, získá `Course` entitu pro vybraný kurz a odebere vybraný kurz z `Courses` navigační vlastnosti entity `Person`. Poté uloží změny do databáze a znovu naplní rozevírací seznamy, takže výsledky lze zobrazit okamžitě.

Přidejte kód do metody `Page_Load`, která zajistí, že chybové zprávy nejsou viditelné, pokud není k dispozici žádná chyba, a přidejte obslužné rutiny pro události `DataBound` a `SelectedIndexChanged` v rozevíracím seznamu instruktory k naplnění rozevíracích seznamů kurzů:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-5/samples/sample10.cs)]

Spusťte stránku.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-5/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-5/_static/image9.png)

Vyberte instruktora. V rozevíracím seznamu <strong>přiřadit kurz</strong> se zobrazí kurzy, které instruktor neučí, a v rozevíracím seznamu <strong>Odebrat kurz</strong> se zobrazí kurzy, ke kterým je instruktor již přiřazen. V části <strong>přiřadit kurz</strong> vyberte kurz a pak klikněte na <strong>přiřadit</strong>. Kurz se přesune do rozevíracího seznamu <strong>Odebrat kurz</strong> . V části <strong>Odebrat kurz</strong> vyberte kurz a klikněte na <strong>Odebrat</strong><em>.</em> Kurz se přesune do rozevíracího seznamu <strong>přiřadit kurz</strong> .

Už jste viděli několik dalších způsobů, jak pracovat se souvisejícími daty. V následujícím kurzu se dozvíte, jak pomocí dědičnosti v datovém modelu zlepšit udržovatelnost aplikace.

> [!div class="step-by-step"]
> [Předchozí](the-entity-framework-and-aspnet-getting-started-part-4.md)
> [Další](the-entity-framework-and-aspnet-getting-started-part-6.md)

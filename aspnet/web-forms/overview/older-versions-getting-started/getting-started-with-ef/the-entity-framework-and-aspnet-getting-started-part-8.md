---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
title: Začínáme s Entity Framework 4,0 Database First a webovými formuláři ASP.NET 4 – část 8 | Microsoft Docs
author: tdykstra
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak pomocí Entity Framework vytvořit aplikace webových formulářů ASP.NET. Ukázková aplikace je...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: aaadd9bb-5508-448c-ad57-5497dff90e13
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-8
msc.type: authoredcontent
ms.openlocfilehash: ff6a808dd501df8056c0fb0784a8e42e094d5db7
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78585909"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-8"></a>Začínáme s Entity Framework 4,0 Database First a webovými formuláři ASP.NET 4 – část 8

tím, že [Dykstra](https://github.com/tdykstra)

> Ukázková webová aplikace společnosti Contoso University ukazuje, jak pomocí Entity Framework 4,0 a sady Visual Studio 2010 vytvářet aplikace webových formulářů ASP.NET. Informace o řadě kurzů najdete v [prvním kurzu v řadě](the-entity-framework-and-aspnet-getting-started-part-1.md) .

## <a name="using-dynamic-data-functionality-to-format-and-validate-data"></a>Formátování a ověření dat pomocí funkce dynamických dat

V předchozím kurzu jste implementovali uložené procedury. V tomto kurzu se dozvíte, jak může funkce dynamických dat poskytovat následující výhody:

- Pole jsou automaticky formátována pro zobrazení na základě jejich datového typu.
- Pole se automaticky ověřují na základě jejich datového typu.
- Do datového modelu můžete přidat metadata pro přizpůsobení formátování a chování ověřování. Když to uděláte, můžete přidat pravidla formátování a ověřování na jednom místě a automaticky se použije všude, kde máte přístup k polím pomocí dynamických ovládacích prvků dat.

Chcete-li zjistit, jak to funguje, změňte ovládací prvky, které slouží k zobrazení a úpravě polí na stávající stránce *students. aspx* , a přidejte metadata formátování a ověření do polí název a datum pro `Student` typ entity.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-8/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image1.png)

## <a name="using-dynamicfield-and-dynamiccontrol-controls"></a>Používání ovládacích prvků DynamicField a objektu DynamicControl

Otevřete stránku *students. aspx* a v ovládacím prvku `StudentsGridView` nahraďte **název** a **Datum registrace** `TemplateField` prvky následujícím kódem:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample1.aspx)]

Tento kód používá ovládací prvky `DynamicControl` místo `TextBox` a ovládací prvky `Label` v poli Šablona názvu studenta a pro datum zápisu používá ovládací prvek `DynamicField`. Nejsou zadány žádné formátovací řetězce.

Přidejte ovládací prvek `ValidationSummary` za ovládací prvek `StudentsGridView`.

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample2.aspx)]

V ovládacím prvku `SearchGridView` nahraďte značky pro sloupce **název** a **Datum zápisu** stejně jako v ovládacím prvku `StudentsGridView`, s výjimkou vynechat prvek `EditItemTemplate`. Prvek `Columns` ovládacího prvku `SearchGridView` nyní obsahuje následující kód:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample3.aspx)]

Otevřete *students.aspx.cs* a přidejte následující příkaz `using`:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample4.cs)]

Přidejte obslužnou rutinu pro událost `Init` stránky:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample5.cs)]

Tento kód určuje, že dynamická data budou poskytovat formátování a ověřování v těchto ovládacích prvcích vázaných na data pro pole `Student` entitu. Pokud se zobrazí chybová zpráva podobná následujícímu příkladu při spuštění stránky, obvykle znamená, že jste zapomněli volat metodu `EnableDynamicData` v `Page_Init`:

`Could not determine a MetaTable. A MetaTable could not be determined for the data source 'StudentsEntityDataSource' and one could not be inferred from the request URL.`

Spusťte stránku.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-8/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image3.png)

Ve sloupci **Datum zápisu** se zobrazí čas společně s datem, protože typ vlastnosti je `DateTime`. Později to opravíte.

Prozatím si všimněte, že dynamická data automaticky poskytují základní ověření dat. Klikněte například na **Upravit**, zrušte zaškrtnutí políčka datum, klikněte na **aktualizovat**a uvidíte, že dynamická data automaticky vytvoří toto povinné pole, protože v datovém modelu se nepovoluje hodnota null. Stránka zobrazuje hvězdičku za polem a chybovou zprávu v ovládacím prvku `ValidationSummary`:

[![Image05](the-entity-framework-and-aspnet-getting-started-part-8/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image5.png)

Můžete vynechat ovládací prvek `ValidationSummary`, protože můžete také umístit ukazatel myši na hvězdičku, aby se zobrazila chybová zpráva:

[![Image06](the-entity-framework-and-aspnet-getting-started-part-8/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image7.png)

Dynamická data také ověří, že data zadaná v poli **Datum registrace** jsou platné datum:

[![Image04](the-entity-framework-and-aspnet-getting-started-part-8/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image9.png)

Jak vidíte, jedná se o obecnou chybovou zprávu. V další části se dozvíte, jak přizpůsobit zprávy a také pravidla pro ověřování a formátování.

## <a name="adding-metadata-to-the-data-model"></a>Přidání metadat do datového modelu

Obvykle chcete přizpůsobit funkce poskytované dynamickými daty. Můžete například změnit způsob zobrazení dat a obsah chybových zpráv. Pravidla pro ověřování dat se obvykle přizpůsobují tak, aby poskytovala více funkcí, než jaká dynamická data poskytuje automaticky na základě datových typů. K tomu je třeba vytvořit dílčí třídy, které odpovídají typům entit.

V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt **ContosoUniversity** , vyberte možnost **Přidat odkaz**a přidejte odkaz na `System.ComponentModel.DataAnnotations`.

[![Image11](the-entity-framework-and-aspnet-getting-started-part-8/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image11.png)

Ve složce *dal* vytvořte nový soubor třídy, pojmenujte ho *student.cs*a v něm nahraďte kód šablony následujícím kódem.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-8/samples/sample6.cs)]

Tento kód vytvoří pro entitu `Student` částečnou třídu. Atribut `MetadataType` aplikovaný na tuto částečnou třídu identifikuje třídu, kterou používáte k určení metadat. Třída metadat může mít libovolný název, ale použití názvu entity plus "metadata" je běžný postup.

Atributy použité pro vlastnosti třídy metadata určují formátování, ověřování, pravidla a chybové zprávy. Zde uvedené atributy budou mít následující výsledky:

- `EnrollmentDate` se zobrazí jako datum (bez času).
- Obě pole název musí mít délku 25 nebo méně znaků a je k dispozici vlastní chybová zpráva.
- Obě pole jména jsou povinná a vlastní chybová zpráva je k dispozici.

Spusťte znovu stránku *students. aspx* a uvidíte, že se data nyní zobrazují bez časů:

[![Image08](the-entity-framework-and-aspnet-getting-started-part-8/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image13.png)

Upravte řádek a pokuste se vymazat hodnoty v polích název. Hvězdičky indikující chyby pole se zobrazí hned po opuštění pole, než kliknete na tlačítko **aktualizovat**. Po kliknutí na možnost **aktualizovat**se na stránce zobrazí text chybové zprávy, kterou jste zadali.

[![Image10](the-entity-framework-and-aspnet-getting-started-part-8/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image15.png)

Zkuste zadat názvy, které jsou delší než 25 znaků, klikněte na **aktualizovat**a na stránce se zobrazí text chybové zprávy, kterou jste zadali.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-8/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-8/_static/image17.png)

Teď, když jste nastavili tato pravidla formátování a ověřování v metadatech datového modelu, pravidla se automaticky použijí na všech stránkách, které zobrazují nebo povolují změny těchto polí, pokud použijete ovládací prvky `DynamicControl` nebo `DynamicField`. Tím se sníží množství redundantního kódu, který musíte napsat, což usnadňuje programování a testování, a zajišťuje, aby formátování a ověřování dat bylo konzistentní v celé aplikaci.

## <a name="more-information"></a>Další informace

Tím se tato série kurzů dokončí Začínáme Entity Framework. Další materiály, které vám pomůžou naučit se používat Entity Framework, najdete [v prvním kurzu v další Entity Framework řadě kurzů](../continuing-with-ef/using-the-entity-framework-and-the-objectdatasource-control-part-1-getting-started.md) nebo na následujících webech:

- [Nejčastější dotazy k Entity Framework](http://www.ef-faq.org/introduction.html)
- [Blog týmu Entity Framework](https://blogs.msdn.com/b/adonet/)
- [Entity Framework v knihovně MSDN](https://msdn.microsoft.com/library/bb399572.aspx)
- [Entity Framework v centru pro vývojáře dat MSDN](https://msdn.microsoft.com/data/ef.aspx)
- [Přehled ovládacího prvku webového serveru EntityDataSource v knihovně MSDN](https://msdn.microsoft.com/library/cc488502.aspx)
- [Odkaz na rozhraní API ovládacího prvku EntityDataSource v knihovně MSDN](https://msdn.microsoft.com/library/system.web.ui.webcontrols.entitydatasource.aspx)
- [Entity Framework fóra na webu MSDN](https://social.msdn.microsoft.com/forums/adodotnetentityframework/)
- [Blog Julie Lerman](http://thedatafarm.com/blog/)

> [!div class="step-by-step"]
> [Předchozí](the-entity-framework-and-aspnet-getting-started-part-7.md)

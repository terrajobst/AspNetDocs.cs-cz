---
uid: web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
title: Začínáme s Entity Framework 4,0 Database First a webovými formuláři ASP.NET 4 – část 4 | Microsoft Docs
author: tdykstra
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak pomocí Entity Framework vytvořit aplikace webových formulářů ASP.NET. Ukázková aplikace je...
ms.author: riande
ms.date: 12/03/2010
ms.assetid: ceb9e60f-957c-4d25-9331-cc527de96a33
msc.legacyurl: /web-forms/overview/older-versions-getting-started/getting-started-with-ef/the-entity-framework-and-aspnet-getting-started-part-4
msc.type: authoredcontent
ms.openlocfilehash: eb75a76038466bf30738387ed4739687de1df944
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78638164"
---
# <a name="getting-started-with-entity-framework-40-database-first-and-aspnet-4-web-forms---part-4"></a>Začínáme s Entity Framework 4,0 Database First a webovými formuláři ASP.NET 4 – část 4

tím, že [Dykstra](https://github.com/tdykstra)

> Ukázková webová aplikace společnosti Contoso University ukazuje, jak pomocí Entity Framework 4,0 a sady Visual Studio 2010 vytvářet aplikace webových formulářů ASP.NET. Informace o řadě kurzů najdete v [prvním kurzu v řadě](the-entity-framework-and-aspnet-getting-started-part-1.md) .

## <a name="working-with-related-data"></a>Práce se souvisejícími daty

V předchozím kurzu jste použili ovládací prvek `EntityDataSource` k filtrování, řazení a seskupování dat. V tomto kurzu zobrazíte a aktualizujete související data.

Vytvoříte stránku instruktory, která zobrazuje seznam instruktorů. Když vyberete instruktora, zobrazí se seznam kurzů, které tento instruktor výukoval. Když vyberete kurz, zobrazí se podrobnosti o kurzu a seznam studentů zaregistrovaných v tomto kurzu. Můžete upravit název instruktora, datum přijetí a přiřazení kanceláře. Přiřazení kanceláře je samostatná sada entit, ke které přistupujete prostřednictvím navigační vlastnosti.

Můžete propojit hlavní data s podrobnostmi o datech v kódu nebo v kódu. V této části kurzu použijete obě metody.

[![Image01](the-entity-framework-and-aspnet-getting-started-part-4/_static/image2.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image1.png)

## <a name="displaying-and-updating-related-entities-in-a-gridview-control"></a>Zobrazení a aktualizace souvisejících entit v ovládacím prvku GridView

Vytvořte novou webovou stránku s názvem *instruktors. aspx* , která používá hlavní stránku *Web. Master* , a přidejte následující kód do ovládacího prvku `Content` s názvem `Content2`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample1.aspx)]

Tento kód vytvoří ovládací prvek `EntityDataSource`, který vybere instruktory a povolí aktualizace. Element `div` konfiguruje značku pro vykreslení vlevo, takže můžete přidat sloupec hned později.

Mezi značkami `EntityDataSource` a uzavírací `</div>`ovou značkou přidejte následující kód, který vytvoří ovládací prvek `GridView` a ovládací prvek `Label`, který budete používat pro chybové zprávy:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample2.aspx)]

Tento ovládací prvek `GridView` umožňuje výběr řádků, zvýrazní vybraný řádek barevnou šedou barvou pozadí a určí obslužné rutiny (které vytvoříte později) pro události `SelectedIndexChanged` a `Updating`. Určuje také `PersonID` pro vlastnost `DataKeyNames`, takže hodnota klíče vybraného řádku může být předána jinému ovládacímu prvku, který později přidáte.

Poslední sloupec obsahuje přiřazení kanceláře instruktora, které je uloženo v navigační vlastnosti entity `Person`, protože pochází z přidružené entity. Všimněte si, že prvek `EditItemTemplate` určuje `Eval` namísto `Bind`, protože ovládací prvek `GridView` nemůže přímo navazovat vazby na navigační vlastnosti, aby je bylo možné aktualizovat. V kódu aktualizujete přiřazení Office. Chcete-li to provést, budete potřebovat odkaz na ovládací prvek `TextBox` a získáte ho a uložíte v události `Init` ovládacího prvku `TextBox`.

Následujícím ovládacím prvkem `GridView` je `Label` ovládací prvek, který se používá pro chybové zprávy. Vlastnost `Visible` ovládacího prvku je `false`a stav zobrazení je vypnutý, takže popisek se zobrazí pouze v případě, že kód je viditelný v reakci na chybu.

Otevřete soubor *Instructors.aspx.cs* a přidejte následující příkaz `using`:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample3.cs)]

Přidejte pole soukromé třídy hned po deklaraci názvu částečné třídy, aby obsahovalo odkaz na textové pole přiřazení sady Office.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample4.cs)]

Přidejte zástupnou proceduru pro obslužnou rutinu události `SelectedIndexChanged`, kterou přidáte pro pozdější kód. Přidejte také obslužnou rutinu pro `Init` událost `TextBox` ovládacího prvku přiřazení sady Office, abyste mohli uložit odkaz na ovládací prvek `TextBox`. Tento odkaz použijete k získání hodnoty zadané uživatelem za účelem aktualizace entity přidružené k navigační vlastnosti.

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample5.cs)]

Pomocí události `Updating` ovládacího prvku `GridView` můžete aktualizovat vlastnost `Location` přidružené entity `OfficeAssignment`. Přidejte následující obslužnou rutinu pro událost `Updating`:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample6.cs)]

Tento kód se spustí, když uživatel klikne na **aktualizovat** na řádku `GridView`. Kód používá LINQ to Entities k načtení `OfficeAssignment` entity, která je přidružena k aktuální `Person` entitě pomocí `PersonID` vybraného řádku z argumentu události.

Kód pak provede jednu z následujících akcí v závislosti na hodnotě v ovládacím prvku `InstructorOfficeTextBox`:

- Pokud textové pole má hodnotu a neexistuje žádná `OfficeAssignment` entita, která by se měla aktualizovat, vytvoří se.
- Pokud textové pole má hodnotu a existuje `OfficeAssignment` entita, aktualizuje hodnotu vlastnosti `Location`.
- Pokud je textové pole prázdné a existuje-`OfficeAssignment` entita, odstraní entitu.

Potom změny uloží do databáze. Pokud dojde k výjimce, zobrazí se chybová zpráva.

Spusťte stránku.

[![Image02](the-entity-framework-and-aspnet-getting-started-part-4/_static/image4.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image3.png)

Klikněte na tlačítko **Upravit** a všechna pole změnit na textová pole.

[![Image03](the-entity-framework-and-aspnet-getting-started-part-4/_static/image6.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image5.png)

Změňte některou z těchto hodnot včetně **přiřazení Office**. Klikněte na **aktualizovat** a zobrazí se změny v seznamu.

## <a name="displaying-related-entities-in-a-separate-control"></a>Zobrazení souvisejících entit v samostatném ovládacím prvku

Každý instruktor může vytvořit výuku jednoho nebo více kurzů, takže přidáte ovládací prvek `EntityDataSource` a ovládací prvek `GridView` k vypsání kurzů přidružených k určitému instruktorovi, který je vybrán v ovládacím prvku `GridView` instruktory. Chcete-li vytvořit záhlaví a ovládací prvek `EntityDataSource` pro entity kurzů, přidejte následující kód mezi chybovou zprávu `Label` ovládací prvek a uzavírací `</div>` Značka:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample7.aspx)]

Parametr `Where` obsahuje hodnotu `PersonID` instruktora, jejíž řádek je vybrán v ovládacím prvku `InstructorsGridView`. Vlastnost `Where` obsahuje příkaz pro dílčí výběr, který získá všechny přidružené `Person` entity z vlastnosti navigace `People` `Course` entity a vybere entitu `Course`, pokud jedna z přidružených entit `Person` obsahuje vybranou `PersonID` hodnotu.

Chcete-li vytvořit ovládací prvek `GridView`. Přidejte následující značku hned za ovládací prvek `CoursesEntityDataSource` (před uzavírací značku `</div>`):

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample8.aspx)]

Vzhledem k tomu, že se nezobrazí žádné kurzy, pokud není vybrán žádný instruktor, je zahrnut `EmptyDataTemplate` element.

Spusťte stránku.

[![Image04](the-entity-framework-and-aspnet-getting-started-part-4/_static/image8.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image7.png)

Vyberte instruktora s přiřazeným jedním nebo více kurzy a v seznamu se zobrazí kurz nebo kurzy. (Poznámka: Přestože schéma databáze umožňuje více kurzů, v datech testu dodaných s databází nemá žádný instruktor více než jeden kurz. Do databáze můžete přidat kurzy, a to pomocí okna **Průzkumník serveru** nebo stránky *CoursesAdd. aspx* , kterou přidáte v pozdějším kurzu.)

[![Image05](the-entity-framework-and-aspnet-getting-started-part-4/_static/image10.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image9.png)

Ovládací prvek `CoursesGridView` zobrazuje pouze několik polí kurzu. Chcete-li zobrazit všechny podrobnosti o kurzu, použijte ovládací prvek `DetailsView` pro kurz, který uživatel vybere. V *instruktors. aspx*přidejte následující značky za uzavírací značku `</div>` (Nezapomeňte umístit toto označení **za** uzavírací značku div, nikoli před ní):

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample9.aspx)]

Tento kód vytvoří ovládací prvek `EntityDataSource`, který je svázán se sadou entit `Courses`. Vlastnost `Where` vybere kurz pomocí `CourseID` hodnoty vybraného řádku v ovládacím prvku kurzy `GridView`. Značka určuje obslužnou rutinu pro událost `Selected`, kterou použijete později pro zobrazení studijních známek, což je další nižší úroveň v hierarchii.

V *Instructors.aspx.cs*vytvořte následující zástupnou proceduru pro metodu `CourseDetailsEntityDataSource_Selected`. (Tento zástupný kód vyplníte později v tomto kurzu. zatím ho budete potřebovat, aby se stránka zkompiluje a spustí.)

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample10.cs)]

Spusťte stránku.

[![Image06](the-entity-framework-and-aspnet-getting-started-part-4/_static/image12.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image11.png)

Zpočátku neexistují žádné podrobnosti o kurzu, protože není vybraný žádný kurz. Vyberte instruktora s přiřazeným kurzem a potom vyberte kurz, ve kterém se zobrazí podrobnosti.

[![Image07](the-entity-framework-and-aspnet-getting-started-part-4/_static/image14.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image13.png)

## <a name="using-the-entitydatasource-selected-event-to-display-related-data"></a>Zobrazení souvisejících dat pomocí události "vybrané" v EntityDataSource

Nakonec chcete zobrazit všechny zaregistrované studenty a jejich třídy pro vybraný kurz. K tomu budete používat událost `Selected` ovládacího prvku `EntityDataSource` vázaného na `DetailsView`kurzu.

V *instruktors. aspx*přidejte následující značku za ovládací prvek `DetailsView`:

[!code-aspx[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample11.aspx)]

Tento kód vytvoří ovládací prvek `ListView`, který zobrazí seznam studentů a jejich třídy pro vybraný kurz. Není zadán žádný zdroj dat, protože ovládací prvek bude svázán v kódu. Element `EmptyDataTemplate` obsahuje zprávu, která se zobrazí, když není vybraný žádný kurz – v takovém případě se žádné studenty nemůžou zobrazit. Element `LayoutTemplate` vytvoří tabulku HTML pro zobrazení seznamu a `ItemTemplate` Určuje sloupce, které se mají zobrazit. ID studenta a stupeň studenta jsou z entity `StudentGrade` a jméno studenta pochází z `Person` entity, kterou Entity Framework zpřístupňuje v `Person` navigační vlastnosti entity `StudentGrade`.

V *Instructors.aspx.cs*nahraďte metodu podložit-out `CourseDetailsEntityDataSource_Selected` následujícím kódem:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample12.cs)]

Argument události pro tuto událost poskytuje vybraná data ve formě kolekce, která bude obsahovat nula položek, pokud není nic vybráno, nebo jednu položku, je-li vybrána entita `Course`. Pokud je vybrána entita `Course`, kód používá metodu `First` k převedení kolekce na jeden objekt. Poté získá `StudentGrade` entit z navigační vlastnosti, převede je na kolekci a naváže ovládací prvek `GradesListView` na kolekci.

To je dostačující pro zobrazení stupňů, ale chcete se ujistit, že se při prvním zobrazení stránky zobrazí zpráva v prázdné šabloně a když není vybraný kurz. Uděláte to tak, že vytvoříte následující metodu, kterou budete volat ze dvou míst:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample13.cs)]

Zavolejte tuto novou metodu z metody `Page_Load` k zobrazení prázdné datové šablony při prvním zobrazení stránky. A zavolejte ji z metody `InstructorsGridView_SelectedIndexChanged`, protože tato událost je vyvolána, když je vybrán instruktor, což znamená, že nové kurzy jsou načteny do kurzů `GridView` řízení a ještě není vybráno žádné. Toto jsou dvě volání:

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample14.cs)]

[!code-csharp[Main](the-entity-framework-and-aspnet-getting-started-part-4/samples/sample15.cs)]

Spusťte stránku.

[![Image08](the-entity-framework-and-aspnet-getting-started-part-4/_static/image16.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image15.png)

Vyberte instruktora s přiřazeným kurzem a potom vyberte kurz.

[![Image09](the-entity-framework-and-aspnet-getting-started-part-4/_static/image18.png)](the-entity-framework-and-aspnet-getting-started-part-4/_static/image17.png)

Teď jste viděli několik způsobů, jak pracovat se souvisejícími daty. V následujícím kurzu se dozvíte, jak přidat relace mezi stávajícími entitami, jak odebrat relace a jak přidat novou entitu, která má relaci s existující entitou.

> [!div class="step-by-step"]
> [Předchozí](the-entity-framework-and-aspnet-getting-started-part-3.md)
> [Další](the-entity-framework-and-aspnet-getting-started-part-5.md)

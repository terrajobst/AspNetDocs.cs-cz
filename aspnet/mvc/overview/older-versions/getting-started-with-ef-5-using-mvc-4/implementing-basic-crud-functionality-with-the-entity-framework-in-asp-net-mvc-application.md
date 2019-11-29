---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
title: Implementace základní funkce CRUD pomocí Entity Framework v aplikaci ASP.NET MVC (2 z 10) | Microsoft Docs
author: tdykstra
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: f7bace3f-b85a-47ff-b5fe-49e81441cdf9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: eba146d2975e0dcf243facf7c205c4acfe40b6f6
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595332"
---
# <a name="implementing-basic-crud-functionality-with-the-entity-framework-in-aspnet-mvc-application-2-of-10"></a>Implementace základní funkce CRUD pomocí Entity Framework v aplikaci ASP.NET MVC (2 z 10)

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio 2012. Informace o řadě kurzů najdete v [prvním kurzu v řadě](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Řadu kurzů můžete spustit na začátku nebo [si stáhnout počáteční projekt pro tuto kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a začít zde.
> 
> > [!NOTE] 
> > 
> > Pokud narazíte na problém, který nemůžete vyřešit, [Stáhněte si dokončenou kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a pokuste se problém reprodukován. Řešení problému můžete obecně najít porovnáním kódu s dokončeným kódem. Některé běžné chyby a jejich řešení najdete v tématu [chyby a alternativní řešení.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

V předchozím kurzu jste vytvořili aplikaci MVC, která ukládá a zobrazuje data pomocí Entity Framework a SQL Server LocalDB. V tomto kurzu zkontrolujete a upravíte kód CRUD (vytvořit, číst, aktualizovat, odstranit), který pro vás automaticky vytvoří generování uživatelského rozhraní MVC v řadičích a zobrazeních.

> [!NOTE]
> Je běžný postup implementace vzoru úložiště, aby bylo možné vytvořit vrstvu abstrakce mezi řadičem a vrstvou přístupu k datům. Pro zjednodušení těchto výukových kurzů nebudete implementovat úložiště do pozdějšího kurzu v této řadě.

V tomto kurzu vytvoříte následující webové stránky:

![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image1.png)

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image2.png)

![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image3.png)

![Student_delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image4.png)

## <a name="creating-a-details-page"></a>Vytvoření stránky s podrobnostmi

Vygenerovaný kód pro studenty `Index` stránku opustil vlastnost `Enrollments`, protože tato vlastnost obsahuje kolekci. Na stránce `Details` zobrazíte obsah kolekce v tabulce HTML.

 V *Controllers\StudentController.cs*metoda Action pro zobrazení `Details` používá metodu `Find` k načtení jedné entity `Student`. 

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample1.cs)]

 Hodnota klíče je předána metodě jako parametr `id` a přichází z dat směrování v hypertextovém odkazu **Podrobnosti** na stránce indexu. 

1. Otevřete *Views\Student\Details.cshtml*. Každé pole se zobrazí pomocí pomocné rutiny `DisplayFor`, jak je znázorněno v následujícím příkladu: 

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample2.cshtml)]
2. Po poli `EnrollmentDate` a bezprostředně před uzavírací značkou `fieldset` přidejte kód pro zobrazení seznamu registrací, jak je znázorněno v následujícím příkladu:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample3.cshtml?highlight=4-22)]

    Tento kód projde entitami v navigační vlastnosti `Enrollments`. Pro každou entitu `Enrollment` ve vlastnosti se zobrazí titul kurzu a stupeň. Titul kurzu se načte z `Course` entity, která je uložená v `Course` navigační vlastnosti entity `Enrollments`. Všechna tato data jsou načtena z databáze automaticky v případě potřeby. (Jinými slovy, zde se používá opožděné načítání. Neurčili jste *načítání Eager* pro navigační vlastnost `Courses`, takže při prvním pokusu o přístup k této vlastnosti se do databáze pošle dotaz, aby se data načetla. Další informace o opožděném načítání a Eager načítání najdete v kurzu pro [čtení souvisejících dat](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) dále v této sérii.)
3. Spusťte stránku tak, že vyberete kartu **Students** a kliknete na odkaz **Podrobnosti** pro Alexander Carson. Zobrazí se seznam kurzů a stupňů pro vybraného studenta:

    ![Student_Details_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image5.png)

## <a name="updating-the-create-page"></a>Aktualizace stránky pro vytvoření

1. V *Controllers\StudentController.cs*nahraďte metodu `HttpPost``Create` akce následujícím kódem pro přidání bloku `try-catch` a [atributu BIND](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) do vygenerované metody: 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample4.cs?highlight=4,7-8,14-20)]

    Tento kód přidá entitu `Student` vytvořenou pomocí pořadače modelu ASP.NET MVC do sady entit `Students` a následně uloží změny do databáze. (*Modelový pořadač* odkazuje na funkci ASP.NET MVC, která usnadňuje práci s daty odesílanými formulářem. modelový pořadač převede hodnoty vystavených formulářů na typy CLR a předá je metodě Action v parametrech. V tomto případě vytvoří pořadač modelů `Student` entitu pro použití hodnot vlastností z kolekce `Form`.)

    Atribut `ValidateAntiForgeryToken` pomáhá zabránit útokům proti [padělání požadavků mezi weby](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) .

<a id="overpost"></a>

    > [!WARNING]
    > Security - The `Bind` attribute is added to protect against *over-posting*. For example, suppose the `Student` entity includes a `Secret` property that you don't want this web page to update.
    > 
    > [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample5.cs?highlight=7)]
    > 
    > Even if you don't have a `Secret` field on the web page, a hacker could use a tool such as [fiddler](http://fiddler2.com/home), or write some JavaScript, to post a `Secret` form value. Without the [Bind](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx) attribute limiting the fields that the model binder uses when it creates a `Student` instance*,* the model binder would pick up that `Secret` form value and use it to update the `Student` entity instance. Then whatever value the hacker specified for the `Secret` form field would be updated in your database. The following image shows the fiddler tool adding the `Secret` field (with the value "OverPost") to the posted form values.
    > 
    > ![](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image6.png)  
    > 
    > The value "OverPost" would then be successfully added to the `Secret` property of the inserted row, although you never intended that the web page be able to update that property.
    > 
    > It's a security best practice to use the `Include` parameter with the `Bind` attribute to *whitelist* fields. It's also possible to use the `Exclude` parameter to *blacklist* fields you want to exclude. The reason `Include` is more secure is that when you add a new property to the entity, the new field is not automatically protected by an `Exclude` list.
    > 
    > Another alternative approach, and one preferred by many, is to use only view models with model binding. The view model contains only the properties you want to bind. Once the MVC model binder has finished, you copy the view model properties to the entity instance.

    Other than the `Bind` attribute, the `try-catch` block is the only change you've made to the scaffolded code. If an exception that derives from [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) is caught while the changes are being saved, a generic error message is displayed. [DataException](https://msdn.microsoft.com/library/system.data.dataexception.aspx) exceptions are sometimes caused by something external to the application rather than a programming error, so the user is advised to try again. Although not implemented in this sample, a production quality application would log the exception (and non-null inner exceptions ) with a logging mechanism such as [ELMAH](https://code.google.com/p/elmah/).

    The code in *Views\Student\Create.cshtml* is similar to what you saw in *Details.cshtml*, except that `EditorFor` and `ValidationMessageFor` helpers are used for each field instead of `DisplayFor`. The following example shows the relevant code:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample6.cshtml)]

    *Create.cshtml* also includes `@Html.AntiForgeryToken()`, which works with the `ValidateAntiForgeryToken` attribute in the controller to help prevent [cross-site request forgery](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) attacks.

    No changes are required in *Create.cshtml*.
2. Spusťte stránku tak, že vyberete kartu **Students** a kliknete na **vytvořit novou**.

    ![Student_Create_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image7.png)

    Ve výchozím nastavení funguje ověřování dat. Zadejte názvy a neplatné datum a kliknutím na **vytvořit** se zobrazí chybová zpráva.

    ![Students_Create_page_error_message](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image8.png)

    Následující zvýrazněný kód ukazuje kontrolu ověřování modelu.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample7.cs?highlight=5)]

    Změňte datum na platnou hodnotu, například 9/1/2005, a kliknutím na tlačítko **vytvořit** zobrazíte nového studenta na stránce **Rejstřík** .

    ![Students_Index_page_with_new_student](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image9.png)

## <a name="updating-the-edit-post-page"></a>Aktualizace stránky pro úpravu příspěvku

V *Controllers\StudentController.cs*metoda `HttpGet` `Edit` (ta bez atributu `HttpPost`) používá metodu `Find` k načtení vybrané entity `Student`, jak jste viděli v metodě `Details`. Tuto metodu nemusíte měnit.

Pokud však chcete přidat blok `try-catch` a [atribut BIND](https://msdn.microsoft.com/library/system.web.mvc.bindattribute(v=vs.108).aspx), nahraďte metodu `HttpPost` `Edit` akci následujícím kódem:

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample8.cs)]

Tento kód se podobá tomu, co jste viděli v metodě `HttpPost` `Create`. Nicméně místo přidání entity vytvořené pomocí pořadače modelu do sady entit tento kód nastaví příznak u entity indikující, že byla změněna. Když je volána metoda [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) , [upravený](https://msdn.microsoft.com/library/system.data.entitystate.aspx) příznak způsobí, že Entity Framework vytvoří příkazy SQL pro aktualizaci řádku databáze. Všechny sloupce řádku databáze budou aktualizovány, včetně těch, které uživatel nezměnil, a konflikty souběžnosti jsou ignorovány. (Naučíte se, jak zpracovávat souběžnost v pozdějším kurzu v této sérii.)

### <a name="entity-states-and-the-attach-and-savechanges-methods"></a>Stavy entit a metody Attach a SaveChanges

Kontext databáze uchovává informace o tom, zda jsou entity v paměti synchronizovány s odpovídajícími řádky v databázi, a tyto informace určují, co se stane při volání metody `SaveChanges`. Když například předáte novou entitu metodě [Add](https://msdn.microsoft.com/library/system.data.entity.dbset.add(v=vs.103).aspx) , stav této entity je nastaven na `Added`. Poté při volání metody [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) vyvolá kontext databáze příkaz SQL `INSERT`.

Entita může být v jednom z[následujících stavů](https://msdn.microsoft.com/library/system.data.entitystate.aspx):

- `Added`. Entita zatím v databázi neexistuje. Metoda `SaveChanges` musí vystavovat příkaz `INSERT`.
- `Unchanged`. Pomocí metody `SaveChanges` není nic nutné s touto entitou dělat. Při čtení entity z databáze se entita spouští s tímto stavem.
- `Modified`. Některé nebo všechny hodnoty vlastností entity byly změněny. Metoda `SaveChanges` musí vystavovat příkaz `UPDATE`.
- `Deleted`. Entita byla označena pro odstranění. Metoda `SaveChanges` musí vystavovat příkaz `DELETE`.
- `Detached`. Entita není sledována kontextem databáze.

V aplikaci klasické pracovní plochy se obvykle automaticky nastaví změny stavu. V typu aplikace na ploše si přečtete entitu a provedete změny jejích hodnot vlastností. Tím dojde k automatické změně stavu entity na `Modified`. Poté při volání `SaveChanges`Entity Framework vygeneruje příkaz jazyka SQL `UPDATE`, který aktualizuje pouze skutečné vlastnosti, které jste změnili.

Odpojená povaha webových aplikací nepovoluje tuto souvislou sekvenci. [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) , který čte entitu, je uvolněna po vykreslení stránky. Když je volána metoda `HttpPost` `Edit` akce, je vytvořena nová žádost a máte novou instanci [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx), takže je nutné ručně nastavit stav entity na `Modified.` pak při volání `SaveChanges`Entity Framework aktualizuje všechny sloupce řádku databáze, protože kontext nemá žádný způsob, jak zjistit, které vlastnosti jste změnili.

Pokud chcete, aby příkaz SQL `Update` aktualizoval pouze pole, která uživatel skutečně změnil, můžete původní hodnoty Uložit nějakým způsobem (například skrytá pole), aby byly k dispozici při volání metody `Edit` `HttpPost`. Pak můžete vytvořit entitu `Student` s použitím původních hodnot, zavolat metodu `Attach` s touto původní verzí entity, aktualizovat hodnoty entity na nové hodnoty a potom volat `SaveChanges.` pro další informace najdete v tématu [stavy entit a metody SaveChanges](https://msdn.microsoft.com/data/jj592676) a [místní data](https://msdn.microsoft.com/data/jj592872) v centru pro vývojáře dat MSDN.

Kód v *Views\Student\Edit.cshtml* je podobný tomu, co jste viděli v části *vytvoření. cshtml*a nejsou vyžadovány žádné změny.

Spusťte stránku tak, že vyberete kartu **Students** a potom kliknete na hypertextový odkaz **Upravit** .

![Student_Edit_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image10.png)

Změňte některá data a klikněte na **Uložit**. Změněná data se zobrazí na stránce index.

![Students_Index_page_after_edit](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a>Aktualizace stránky pro odstranění

V *Controllers\StudentController.cs*kód šablony pro metodu `HttpGet` `Delete` používá metodu `Find` k načtení vybrané entity `Student`, jak jste viděli v `Details` a `Edit` metod. K implementaci vlastní chybové zprávy, když volání `SaveChanges` dojde k chybě, přidáte k této metodě a příslušnému zobrazení některé funkce.

Jak jste viděli pro operace aktualizace a vytváření, vyžadují operace odstranění dvě metody akcí. Metoda, která je volána jako odpověď na požadavek GET, zobrazí zobrazení, které uživateli umožňuje schválit nebo zrušit operaci odstranění. Pokud ho uživatel schválí, vytvoří se požadavek POST. Pokud k tomu dojde, je volána metoda `HttpPost` `Delete` a pak tato metoda skutečně provede operaci DELETE.

Do metody `Delete` `HttpPost` přidáte blok `try-catch`, který bude zpracovávat chyby, ke kterým může dojít při aktualizaci databáze. Pokud dojde k chybě, metoda `HttpPost` `Delete` volá metodu `HttpGet` `Delete` a předá jí parametr, který indikuje, že došlo k chybě. Metoda `HttpGet Delete` pak znovu zobrazí potvrzovací stránku spolu s chybovou zprávou, takže uživatel může příležitost zrušit nebo zkusit znovu.

1. Nahraďte metodu `HttpGet` `Delete` akci následujícím kódem, který spravuje zasílání zpráv o chybách: 

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample9.cs)]

    Tento kód přijímá [volitelný](https://msdn.microsoft.com/library/dd264739.aspx) logický parametr, který označuje, zda bylo voláno po neúspěšném uložení změn. Tento parametr je `false`, pokud je metoda `Delete` `HttpGet` volána bez předchozí chyby. Pokud je volána metodou `HttpPost` `Delete` v reakci na chybu aktualizace databáze, je parametr `true` a do zobrazení se předává chybová zpráva.
2. Nahraďte metodu `HttpPost` `Delete` Action (s názvem `DeleteConfirmed`) následujícím kódem, který provede skutečnou operaci odstranění a zachytí všechny chyby aktualizace databáze.

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample10.cs)]

     Tento kód načte vybranou entitu a pak zavolá metodu [Remove](https://msdn.microsoft.com/library/system.data.entity.dbset.remove(v=vs.103).aspx) pro nastavení stavu entity na `Deleted`. Při volání `SaveChanges` se vygeneruje příkaz SQL `DELETE`. Změnili jste také název metody akce z `DeleteConfirmed` na `Delete`. Generovaný kód s názvem `HttpPost` `Delete` metody `DeleteConfirmed` pro udělení jedinečného podpisu `HttpPost` metodě. (CLR vyžaduje, aby byly přetížené metody pro různé parametry metody.) Teď, když jsou podpisy jedinečné, můžete s úmluvou MVC pracovat a používat stejný název pro `HttpPost` a `HttpGet` odstranit metody.

     Pokud zlepšení výkonu v aplikaci s vysokým objemem je prioritou, můžete se vyhnout zbytečným dotazům SQL k načtení řádku nahrazením řádků kódu, které volají `Find` a `Remove` metody s následujícím kódem, jak je znázorněno žlutým zvýrazněním:

     [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample11.cs)]

     Tento kód vytvoří instanci entity `Student` pouze pomocí hodnoty primárního klíče a poté nastaví stav entity na hodnotu `Deleted`. To je vše, co Entity Framework potřebuje, aby se entita odstranila.

     Jak je uvedeno, metoda `HttpGet` `Delete` data neodstraňují. Provádění operace odstranění v reakci na požadavek GET (nebo pro tuto skutečnost, provádění operací úprav, operace vytvoření nebo jakékoli jiné operace, která mění data) vytvoří bezpečnostní riziko. Další informace najdete v tématu [ASP.NET #46 Tip – nepoužívejte odstranění odkazů, protože vytvářejí bezpečnostní otvory](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx) na blogu Stephen Walther.
3. V *Views\Student\Delete.cshtml*přidejte chybovou zprávu mezi nadpisem `h2` a záhlavím `h3`, jak je znázorněno v následujícím příkladu:

     [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample12.cshtml?highlight=2)]

     Spusťte stránku tak, že vyberete kartu **Students** a kliknete na **Odstranit** hypertextový odkaz:

     ![Student_Delete_page](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image12.png)
4. Klikněte na **Odstranit**. Stránka index se zobrazí bez odstraněného studenta. (Příklad kódu pro zpracování chyb v akci v kurzu [zpracování souběžného zpracování](../../getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) v této sérii najdete v tématu.)

## <a name="ensuring-that-database-connections-are-not-left-open"></a>Zajištění, že připojení databáze nejsou otevřená vlevo

Aby se zajistilo, že se připojení k databázi řádně zavřou, a prostředky, které jsou uvolněny, mělo by se jí zobrazit, že instance kontextu je vyřazená. To je důvod, proč generovaný kód poskytuje metodu [Dispose](https://msdn.microsoft.com/library/system.idisposable.dispose(v=vs.110).aspx) na konci `StudentController` třídy v *StudentController.cs*, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample13.cs)]

Základní `Controller` třída již implementuje rozhraní `IDisposable`, takže tento kód jednoduše přidá přepsání do metody `Dispose(bool)` k explicitnímu uvolnění instance kontextu.

## <a name="summary"></a>Přehled

Nyní máte úplnou sadu stránek, které provádějí jednoduché operace CRUD `Student` entit. Pomocí pomocníků MVC můžete vygenerovat prvky uživatelského rozhraní pro datová pole. Další informace o pomocníkech MVC najdete v tématu [vykreslování formuláře pomocí pomocníků HTML](https://msdn.microsoft.com/library/dd410596(v=VS.98).aspx) (stránka je pro MVC 3, ale je stále relevantní pro MVC 4).

V dalším kurzu rozšíříte funkci stránky index přidáním řazení a stránkování.

Odkazy na další prostředky Entity Framework najdete v [mapě obsahu pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

> [!div class="step-by-step"]
> [Předchozí](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)
> [Další](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)

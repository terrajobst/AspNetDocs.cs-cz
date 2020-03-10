---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
title: 'Kurz: implementace funkce CRUD pomocí Entity Framework v ASP.NET MVC | Microsoft Docs'
description: Přečtěte si a přizpůsobte kód pro vytváření, čtení, aktualizaci, odstranění (CRUD), který automaticky vytvoří generování uživatelského rozhraní MVC v řadičích a zobrazeních.
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: a2f70ba4-83d1-4002-9255-24732726c4f2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9ed388543dd54d209ff2a0b92df4f7659962582c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583158"
---
# <a name="tutorial-implement-crud-functionality-with-the-entity-framework-in-aspnet-mvc"></a>Kurz: implementace funkce CRUD pomocí Entity Framework v ASP.NET MVC

V [předchozím kurzu](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)jste vytvořili aplikaci MVC, která ukládá a zobrazuje data pomocí Entity Framework (EF) 6 a SQL Server LocalDB. V tomto kurzu prohlížíte a přizpůsobíte kód pro vytváření, čtení, aktualizaci, odstranění (CRUD), který pro vás automaticky vytvoří generování uživatelského rozhraní MVC v řadičích a zobrazeních.

> [!NOTE]
> Je běžný postup implementace vzoru úložiště, aby bylo možné vytvořit vrstvu abstrakce mezi řadičem a vrstvou přístupu k datům. Aby byly tyto kurzy jednoduché a zaměřené na výuku, jak použít vlastní EF 6, nepoužívají úložiště. Informace o tom, jak implementovat úložiště, najdete v tématu [Mapa obsahu ASP.NET Data Access](../../../../whitepapers/aspnet-data-access-content-map.md).

Tady jsou příklady webových stránek, které vytvoříte:

![Snímek obrazovky se stránkou s podrobnostmi studenta.](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image1.png)

![Snímek obrazovky se stránkou pro vytvoření studenta](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image2.png)

![Snímek obrazovky se stránkou pro odstranění studenta](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image3.png)

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Vytvořit stránku podrobností
> * Aktualizace stránky pro vytvoření
> * Aktualizace metody HttpPost Edit
> * Aktualizovat stránku Delete
> * Zavřít databázová připojení
> * Zpracování transakcí

## <a name="prerequisites"></a>Předpoklady

* [Vytvoření datového modelu Entity Framework](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)

## <a name="create-a-details-page"></a>Vytvořit stránku podrobností

Vygenerovaný kód pro studenty `Index` stránku opustil vlastnost `Enrollments`, protože tato vlastnost obsahuje kolekci. Na stránce `Details` zobrazíte obsah kolekce v tabulce HTML.

V *Controllers\StudentController.cs*metoda Action pro zobrazení `Details` používá metodu [find](https://msdn.microsoft.com/library/gg696418(v=VS.103).aspx) k načtení jedné `Student` entity.

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample1.cs)]

Hodnota klíče je předána metodě jako parametr `id` a přichází z *dat směrování* v hypertextovém odkazu **Podrobnosti** na stránce indexu.

### <a name="tip-route-data"></a>Tip: **směrování dat**

Data směrování jsou data, která modelový pořadač nalezl v segmentu URL zadaném ve směrovací tabulce. Výchozí trasa například určuje `controller`, `action`a `id` segmenty:

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample2.cs?highlight=3)]

V následující adrese URL se výchozí mapy tras `Instructor` jako `controller``Index` jako `action` a 1 jako `id`. Jedná se o hodnoty dat tras.

`http://localhost:1230/Instructor/Index/1?courseID=2021`

`?courseID=2021` je hodnota řetězce dotazu. Pořadač modelů bude fungovat i v případě, že předáte `id` jako hodnotu řetězce dotazu:

`http://localhost:1230/Instructor/Index?id=1&CourseID=2021`

Adresy URL jsou vytvořeny `ActionLink` příkazy v zobrazení Razor. V následujícím kódu se parametr `id` shoduje s výchozí trasou, takže `id` přidána do dat trasy.

[!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample3.cshtml)]

V následujícím kódu `courseID` neodpovídá parametru ve výchozí trase, takže se přidá jako řetězec dotazu.

[!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample4.cshtml)]

### <a name="to-create-the-details-page"></a>Vytvoření stránky podrobností

1. Otevřete *Views\Student\Details.cshtml*.

   Každé pole se zobrazí pomocí pomocné rutiny `DisplayFor`, jak je znázorněno v následujícím příkladu:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample5.cshtml)]

2. Po `EnrollmentDate` pole a bezprostředně před uzavírací značku `</dl>` přidejte zvýrazněný kód pro zobrazení seznamu registrací, jak je znázorněno v následujícím příkladu:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample6.cshtml?highlight=8-29)]

    Pokud je odsazení kódu po vložení kódu nesprávné, stiskněte **ctrl**+**k**, **stisknutím klávesy CTRL+** **D** ho naformátujte.

    Tento kód projde entitami v navigační vlastnosti `Enrollments`. Pro každou entitu `Enrollment` ve vlastnosti se zobrazí titul kurzu a stupeň. Titul kurzu se načte z `Course` entity, která je uložená v `Course` navigační vlastnosti entity `Enrollments`. Všechna tato data jsou načtena z databáze automaticky v případě potřeby. Jinými slovy, používáte opožděné načítání zde. Neurčili jste *Eager načítání* pro vlastnost navigace `Courses`, takže se registrace nenačítala ve stejném dotazu, který se dodanými studenty. Místo toho se při prvním pokusu o přístup k vlastnosti navigace `Enrollments` do databáze pošle nový dotaz, aby se data načetla. Další informace o opožděném načítání a Eager načítání najdete v kurzu pro [čtení souvisejících dat](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md) dále v této sérii.

3. Otevřete stránku podrobností spuštěním programu (**Ctrl**+**F5**), výběrem karty **Students** a kliknutím na odkaz **Podrobnosti** pro Alexander Carson. (Pokud po otevření souboru *Details. cshtml* stisknete klávesu **CTRL**+**F5** , zobrazí se chyba HTTP 400. Je to proto, že se Visual Studio pokusí spustit stránku podrobností, ale nedostalo se na odkaz, který určuje, kdo má zobrazit. Pokud k tomu dojde, z adresy URL odeberte "student/Details" a zkuste to znovu, nebo zavřete prohlížeč, klikněte pravým tlačítkem na projekt a pak klikněte na **zobrazit** > **zobrazení v prohlížeči**.)

    Zobrazí se seznam kurzů a stupňů pro vybraného studenta.

4. Zavřete prohlížeč.

## <a name="update-the-create-page"></a>Aktualizace stránky pro vytvoření

1. V *Controllers\StudentController.cs*nahraďte metodu <xref:System.Web.Mvc.HttpPostAttribute> `Create` akci následujícím kódem. Tento kód přidá blok `try-catch` a odebere `ID` z atributu <xref:System.Web.Mvc.BindAttribute> pro vygenerované metody:

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample7.cs?highlight=3,5-6,13-18)]

    Tento kód přidá entitu `Student` vytvořenou pomocí pořadače modelu ASP.NET MVC do sady entit `Students` a následně uloží změny do databáze. *Pořadač modelů* odkazuje na funkci ASP.NET MVC, která usnadňuje práci s daty odesílanými formulářem. pořadač modelů převede hodnoty odeslaných formulářů na typy CLR a předá je metodě Action v parametrech. V takovém případě pořadač modelů vytvoří instanci entity `Student` pro použití hodnot vlastností z kolekce `Form`.

    Odebrali jste `ID` z atributu BIND, protože `ID` je hodnota primárního klíče, kterou SQL Server nastaví automaticky při vložení řádku. Vstup od uživatele nenastavuje hodnotu `ID`.

    <a id="overpost"></a>

    ### <a name="security-warning---the-validateantiforgerytoken-attribute-helps-prevent-cross-site-request-forgery-attacks-it-requires-a-corresponding-htmlantiforgerytoken-statement-in-the-view-which-youll-see-later"></a>Upozornění zabezpečení – atribut `ValidateAntiForgeryToken` pomáhá zabránit útokům proti [padělání požadavků mezi weby](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) . V zobrazení vyžaduje odpovídající příkaz `Html.AntiForgeryToken()`, který se zobrazí později.

    Atribut `Bind` je jedním ze způsobů, jak chránit před *převzetím* služeb při selhání ve scénářích vytváření. Předpokládejme například, že entita `Student` zahrnuje vlastnost `Secret`, kterou nechcete, aby tato webová stránka nastavila.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample8.cs?highlight=7)]

    I když na webové stránce nemáte pole `Secret`, hacker by mohl k odeslání `Secret` hodnoty formuláře použít nějaký nástroj, jako je [Fiddler](http://fiddler2.com/home)nebo napsat nějaký JavaScript. Bez atributu <xref:System.Web.Mvc.BindAttribute> omezující pole, která model Binder používá při vytváření instance `Student`<em>,</em> vytvoří pořadač modelu tuto hodnotu `Secret` formuláře a použije ji k vytvoření instance entity `Student`. Pak se v databázi aktualizuje počítačový podvodník zadaný pro pole `Secret` formuláře. Následující obrázek ukazuje nástroj Fiddler, který přidá pole `Secret` (s hodnotou "Repost") do publikovaných hodnot formuláře.

    ![](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/_static/image5.png)

    Hodnota "" přeúčtování "by se pak úspěšně přidala do vlastnosti `Secret` vloženého řádku, i když jste tak ještě neučinili, že webová stránka bude moct tuto vlastnost nastavit.

    Je nejvhodnější použít parametr `Include` s atributem `Bind` na seznam *povolených* polí. Je také možné použít parametr `Exclude` pro *zakázaná* pole, která chcete vyloučit. Důvodem `Include` je bezpečnější je to, že když přidáte novou vlastnost k entitě, nové pole se automaticky nechrání pomocí seznamu `Exclude`.

    Je možné zabránit tomu, aby v úpravách scénářů byla přepsána nejprve z databáze a následným voláním `TryUpdateModel`a předáním seznamu explicitně povolených vlastností. To je metoda použitá v těchto kurzech.

    Alternativní způsob, jak zabránit předávání, které upřednostňuje mnoho vývojářů, je použít modely zobrazení spíše než třídy entit s vazbou modelu. Do modelu zobrazení zahrňte pouze vlastnosti, které chcete aktualizovat. Po dokončení pořadače modelu MVC zkopírujte vlastnosti zobrazení modelu do instance entity, volitelně pomocí nástroje, jako je například [automapper](http://automapper.org/). Použijte DB. Zadáním v instanci entity nastavte její stav na nezměněno a pak nastavte vlastnost ("PropertyName"). U každé vlastnosti entity, která je obsažena v modelu zobrazení, se změní na true. Tato metoda funguje ve scénářích úpravy a vytváření.

    Kromě atributu `Bind` je `try-catch` blok jedinou změnou, kterou jste provedli v kódu generování. Pokud je při ukládání změn zachycena výjimka odvozená od <xref:System.Data.DataException>, zobrazí se obecná chybová zpráva. výjimky <xref:System.Data.DataException> jsou někdy způsobeny něčím externím pro aplikaci, nikoli při programování, takže se uživateli doporučuje akci opakovat. I když v této ukázce není implementované, aplikace produkční kvality by tuto výjimku zaznamenala. Další informace najdete v části **Log for Insight** v tématu [monitorování a telemetrie (vytváření skutečných cloudových aplikací s Azure)](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log).

    Kód v *Views\Student\Create.cshtml* je podobný tomu, co jste viděli v *Details. cshtml*, s tím rozdílem, že `EditorFor` a `ValidationMessageFor` pomocníka se používají pro každé pole místo `DisplayFor`. Zde je příslušný kód:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample9.cshtml)]

    Příkaz *Create. cshtml* zahrnuje také `@Html.AntiForgeryToken()`, který spolupracuje s atributem `ValidateAntiForgeryToken` v kontroleru, aby se zabránilo útokům na [falšování mezi weby](../../security/xsrfcsrf-prevention-in-aspnet-mvc-and-web-pages.md) .

    V *Create. cshtml*nejsou vyžadovány žádné změny.

2. Spusťte tuto stránku spuštěním programu, výběrem karty **Students** a kliknutím na **vytvořit novou**.

3. Zadejte názvy a neplatné datum a kliknutím na **vytvořit** se zobrazí chybová zpráva.

    Toto je ověřování na straně serveru, které se ve výchozím nastavení zobrazí. V pozdějším kurzu uvidíte, jak přidat atributy, které generují kód pro ověřování na straně klienta. Následující zvýrazněný kód ukazuje kontrolu ověřování modelu v metodě **Create** .

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample10.cs?highlight=1)]

4. Změňte datum na platnou hodnotu a kliknutím na tlačítko **vytvořit** zobrazíte nového studenta na stránce **Rejstřík** .

5. Zavřete prohlížeč.

## <a name="update-httppost-edit-method"></a>Update HttpPost Edit – metoda

1. Metodu <xref:System.Web.Mvc.HttpPostAttribute> `Edit` akci nahraďte následujícím kódem:

   [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample11.cs)]

   > [!NOTE]
   > V `HttpGet Edit` *Controllers\StudentController.cs*metoda (ta bez atributu `HttpPost`) používá metodu `Find` k načtení vybrané entity `Student`, jak jste viděli v metodě `Details`. Tuto metodu nemusíte měnit.

   Tyto změny implementují osvědčené postupy zabezpečení, které zabrání [přestavování](#overpost), generování atributu `Bind` a přidání entity vytvořené pomocí pořadače modelu do sady entit s upraveným příznakem. Tento kód již není doporučen, protože atribut `Bind` vymaže všechna dříve existující data v polích, která nejsou uvedena v parametru `Include`. V budoucnu se generátor kontroleru MVC aktualizuje, aby negeneroval atributy `Bind` pro metody úprav.

   Nový kód přečte existující entitu a volá <xref:System.Web.Mvc.Controller.TryUpdateModel%2A> pro aktualizaci polí ze vstupu uživatele v publikovaných datech formuláře. Automatické sledování změn Entity Framework v entitě nastaví příznak [EntityState. Modified](<xref:System.Data.EntityState.Modified>) . Když je volána metoda [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) , příznak <xref:System.Data.EntityState.Modified> způsobí, že Entity Framework vytvoří příkazy SQL pro aktualizaci řádku databáze. [Konflikty souběžnosti](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md) jsou ignorovány a všechny sloupce řádku databáze jsou aktualizovány, včetně těch, které uživatel nezměnil. (V dalším kurzu se dozvíte, jak zvládnout konflikty souběžnosti a pokud chcete v databázi aktualizovat pouze jednotlivá pole, můžete nastavit entitu na [EntityState. Unchanged](<xref:System.Data.EntityState.Unchanged>) a nastavte jednotlivá pole na [EntityState. Modified](<xref:System.Data.EntityState.Modified>).)

   Chcete-li zabránit předávání, pole, která chcete aktualizovat pomocí stránky pro úpravy, jsou na seznamu povolená v parametrech `TryUpdateModel`. V současné době nejsou k dispozici žádná doplňková pole, která chráníte, ale seznam polí, ke kterým má pořadač modelů navazovat vazby, zajišťuje, že pokud přidáte pole do datového modelu v budoucnosti, budou automaticky chráněny, dokud je nepřidáte sem.

   V důsledku těchto změn je signatura metody HttpPost Edit shodná s metodou Edit HttpGet; Proto jste přejmenovali metodu EditPost.

   > [!TIP]
   >
   > **Stavy entit a metody Attach a SaveChanges**
   >
   > Kontext databáze uchovává informace o tom, zda jsou entity v paměti synchronizovány s odpovídajícími řádky v databázi, a tyto informace určují, co se stane při volání metody `SaveChanges`. Když například předáte novou entitu metodě [Add](https://msdn.microsoft.com/library/system.data.entity.dbset.add(v=vs.103).aspx) , stav této entity je nastaven na `Added`. Poté při volání metody [SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx) vyvolá kontext databáze příkaz SQL `INSERT`.
   >
   > Entita může být v jednom z následujících [stavů](xref:System.Data.EntityState):
   >
   > - `Added`. Entita zatím v databázi neexistuje. Metoda `SaveChanges` musí vystavovat příkaz `INSERT`.
   > - `Unchanged`. Pomocí metody `SaveChanges` není nic nutné s touto entitou dělat. Při čtení entity z databáze se entita spouští s tímto stavem.
   > - `Modified`. Některé nebo všechny hodnoty vlastností entity byly změněny. Metoda `SaveChanges` musí vystavovat příkaz `UPDATE`.
   > - `Deleted`. Entita byla označena pro odstranění. Metoda `SaveChanges` musí vystavovat příkaz `DELETE`.
   > - `Detached`. Entita není sledována kontextem databáze.
   >
   > V aplikaci klasické pracovní plochy se obvykle automaticky nastaví změny stavu. V typu aplikace na ploše si přečtete entitu a provedete změny jejích hodnot vlastností. Tím dojde k automatické změně stavu entity na `Modified`. Poté při volání `SaveChanges`Entity Framework vygeneruje příkaz jazyka SQL `UPDATE`, který aktualizuje pouze skutečné vlastnosti, které jste změnili.
   >
   > Odpojená povaha webových aplikací nepovoluje tuto souvislou sekvenci. [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx) , který čte entitu, je uvolněna po vykreslení stránky. Když je volána metoda `HttpPost` `Edit` akce, je vytvořena nová žádost a máte novou instanci [DbContext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx), takže je nutné ručně nastavit stav entity na `Modified.` pak při volání `SaveChanges`Entity Framework aktualizuje všechny sloupce řádku databáze, protože kontext nemá žádný způsob, jak zjistit, které vlastnosti jste změnili.
   >
   > Pokud chcete, aby příkaz SQL `Update` aktualizoval pouze pole, která uživatel skutečně změnil, můžete původní hodnoty Uložit nějakým způsobem (například skrytá pole), aby byly k dispozici při volání metody `Edit` `HttpPost`. Pak můžete vytvořit entitu `Student` s použitím původních hodnot, zavolat metodu `Attach` s touto původní verzí entity, aktualizovat hodnoty entity na nové hodnoty a potom volat `SaveChanges.` pro další informace, viz [stavy entit a metody SaveChanges](/ef/ef6/saving/change-tracking/entity-state) a [místní data](/ef/ef6/querying/local-data).

   Kód HTML a Razor v *Views\Student\Edit.cshtml* je podobný tomu, co jste viděli v souboru *Create. cshtml*a nejsou vyžadovány žádné změny.

2. Spusťte tuto stránku spuštěním programu, výběrem karty **Students** a kliknutím na hypertextový odkaz pro **Úpravy** .

3. Změňte některá data a klikněte na **Uložit**. Změněná data se zobrazí na stránce index.

4. Zavřete prohlížeč.

## <a name="update-the-delete-page"></a>Aktualizovat stránku Delete

V *Controllers\StudentController.cs*kód šablony pro metodu <xref:System.Web.Mvc.HttpGetAttribute> `Delete` používá metodu `Find` k načtení vybrané entity `Student`, jak jste viděli v `Details` a `Edit` metod. K implementaci vlastní chybové zprávy, když volání `SaveChanges` dojde k chybě, přidáte k této metodě a příslušnému zobrazení některé funkce.

Jak jste viděli pro operace aktualizace a vytváření, vyžadují operace odstranění dvě metody akcí. Metoda, která je volána jako odpověď na požadavek GET, zobrazí zobrazení, které uživateli umožňuje schválit nebo zrušit operaci odstranění. Pokud ho uživatel schválí, vytvoří se požadavek POST. Pokud k tomu dojde, je volána metoda `HttpPost` `Delete` a pak tato metoda skutečně provede operaci DELETE.

Do metody `Delete` <xref:System.Web.Mvc.HttpPostAttribute> přidáte blok `try-catch`, který bude zpracovávat chyby, ke kterým může dojít při aktualizaci databáze. Pokud dojde k chybě, metoda <xref:System.Web.Mvc.HttpPostAttribute> `Delete` volá metodu <xref:System.Web.Mvc.HttpGetAttribute> `Delete` a předá jí parametr, který indikuje, že došlo k chybě. Metoda <xref:System.Web.Mvc.HttpGetAttribute> `Delete` pak znovu zobrazí potvrzovací stránku spolu s chybovou zprávou, takže uživatel může příležitost zrušit nebo zkusit znovu.

1. Nahraďte metodu <xref:System.Web.Mvc.HttpGetAttribute> `Delete` akci následujícím kódem, který spravuje zasílání zpráv o chybách:

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample12.cs?highlight=1,7-10)]

    Tento kód akceptuje [volitelný parametr](https://msdn.microsoft.com/library/dd264739.aspx) , který označuje, zda byla metoda volána po neúspěšném uložení změn. Tento parametr je `false`, pokud je metoda `Delete` `HttpGet` volána bez předchozí chyby. Pokud je volána metodou `HttpPost` `Delete` v reakci na chybu aktualizace databáze, je parametr `true` a do zobrazení se předává chybová zpráva.

2. Nahraďte metodu <xref:System.Web.Mvc.HttpPostAttribute> `Delete` Action (s názvem `DeleteConfirmed`) následujícím kódem, který provede skutečnou operaci odstranění a zachytí všechny chyby aktualizace databáze.

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample13.cs)]

    Tento kód načte vybranou entitu a pak zavolá metodu [Remove](https://msdn.microsoft.com/library/system.data.entity.dbset.remove(v=vs.103).aspx) pro nastavení stavu entity na `Deleted`. Při volání `SaveChanges` se vygeneruje příkaz SQL `DELETE`. Změnili jste také název metody akce z `DeleteConfirmed` na `Delete`. Generovaný kód s názvem `HttpPost` `Delete` metody `DeleteConfirmed` pro udělení jedinečného podpisu `HttpPost` metodě. (CLR vyžaduje, aby byly přetížené metody pro různé parametry metody.) Teď, když jsou podpisy jedinečné, můžete s úmluvou MVC pracovat a používat stejný název pro `HttpPost` a `HttpGet` odstranit metody.

    Pokud zlepšení výkonu v aplikaci s vysokým objemem je prioritou, můžete se vyhnout zbytečným dotazům SQL k načtení řádku nahrazením řádků kódu, které volají `Find` a `Remove` metody s následujícím kódem:

    [!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample14.cs)]

    Tento kód vytvoří instanci entity `Student` pouze pomocí hodnoty primárního klíče a poté nastaví stav entity na hodnotu `Deleted`. To je vše, co Entity Framework potřebuje, aby se entita odstranila.

    Jak je uvedeno, metoda `HttpGet` `Delete` data neodstraňují. Provádění operace odstranění v reakci na požadavek GET (nebo pro tuto skutečnost, provádění operací úprav, operace vytvoření nebo jakékoli jiné operace, která mění data) vytvoří bezpečnostní riziko. Další informace najdete v tématu [ASP.NET #46 Tip – nepoužívejte odstranění odkazů, protože vytvářejí bezpečnostní otvory](http://stephenwalther.com/blog/archive/2009/01/21/asp.net-mvc-tip-46-ndash-donrsquot-use-delete-links-because.aspx) na blogu Stephen Walther.

3. V *Views\Student\Delete.cshtml*přidejte chybovou zprávu mezi nadpisem `h2` a záhlavím `h3`, jak je znázorněno v následujícím příkladu:

    [!code-cshtml[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample15.cshtml?highlight=2)]

4. Spusťte tuto stránku spuštěním programu, výběrem karty **Students** a kliknutím na **Odstranit** hypertextový odkaz.

5. Na stránce vyberte možnost **Odstranit** . **opravdu chcete tuto zprávu odstranit?**

    Stránka index se zobrazí bez odstraněného studenta. (Příklad kódu pro zpracování chyb v akci v [kurzu souběžnosti](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)najdete v tématu.)

## <a name="close-database-connections"></a>Zavřít databázová připojení

Chcete-li zavřít databázová připojení a uvolnit prostředky, které jsou k dispozici co nejdříve, vyřazení instance kontextu, jakmile s ní budete hotovi. To je důvod, proč generovaný kód poskytuje metodu [Dispose](https://msdn.microsoft.com/library/system.idisposable.dispose(v=vs.110).aspx) na konci `StudentController` třídy v *StudentController.cs*, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application/samples/sample16.cs)]

Základní `Controller` třída již implementuje rozhraní `IDisposable`, takže tento kód jednoduše přidá přepsání do metody `Dispose(bool)` k explicitnímu uvolnění instance kontextu.

## <a name="handle-transactions"></a>Zpracování transakcí

Ve výchozím nastavení Entity Framework implicitně implementuje transakce. Ve scénářích, kdy provedete změny více řádků nebo tabulek a potom zavoláte `SaveChanges`, Entity Framework automaticky zajistí, že všechny změny byly úspěšné nebo všechny selžou. Pokud se nějaké změny provedly a pak dojde k chybě, změny se automaticky vrátí zpět. V případech, kdy potřebujete větší kontrolu&mdash;například, pokud chcete zahrnout operace provedené mimo Entity Framework v transakci&mdash;naleznete v tématu [práce s transakcemi](/ef/ef6/saving/transactions).

## <a name="get-the-code"></a>Získání kódu

[Stáhnout dokončený projekt](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Další zdroje

Nyní máte úplnou sadu stránek, které provádějí jednoduché operace CRUD `Student` entit. Pomocí pomocníků MVC můžete vygenerovat prvky uživatelského rozhraní pro datová pole. Další informace o pomocníkech MVC najdete v tématu [vykreslování formuláře pomocí pomocníků HTML](/previous-versions/aspnet/dd410596(v=vs.98)) (článek je pro MVC 3, ale je stále relevantní pro MVC 5).

Odkazy na další prostředky EF 6 najdete v [prostředcích, které jsou doporučeny pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

## <a name="next-steps"></a>Další kroky

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Stránka s podrobnostmi se vytvořila.
> * Aktualizace stránky pro vytvoření
> * Aktualizovala se metoda HttpPost Edit.
> * Aktualizace stránky odstranění
> * Uzavřená databázová připojení
> * Zpracované transakce

Přejděte k dalšímu článku a Naučte se, jak do projektu přidat řazení, filtrování a stránkování.
> [!div class="nextstepaction"]
> [Řazení, filtrování a stránkování](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)

---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
title: Zpracování souběžnosti s Entity Framework v aplikaci ASP.NET MVC (7 z 10) | Microsoft Docs
author: tdykstra
description: Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio...
ms.author: riande
ms.date: 07/30/2013
ms.assetid: b83f47c4-8521-4d0a-8644-e8f77e39733e
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 9800a313879477f36a730e6a70c79bc06d403ae3
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/07/2020
ms.locfileid: "77074946"
---
# <a name="handling-concurrency-with-the-entity-framework-in-an-aspnet-mvc-application-7-of-10"></a>Zpracování souběžnosti s Entity Framework v aplikaci ASP.NET MVC (7 z 10)

tím, že [Dykstra](https://github.com/tdykstra)

[Stáhnout dokončený projekt](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Ukázková webová aplikace společnosti Contoso University ukazuje, jak vytvářet aplikace ASP.NET MVC 4 pomocí Code First Entity Framework 5 a Visual Studio 2012. Informace o řadě kurzů najdete v [prvním kurzu v řadě](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md). Řadu kurzů můžete spustit na začátku nebo [si stáhnout počáteční projekt pro tuto kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a začít zde.
> 
> > [!NOTE] 
> > 
> > Pokud narazíte na problém, který nemůžete vyřešit, [Stáhněte si dokončenou kapitolu](building-the-ef5-mvc4-chapter-downloads.md) a pokuste se problém reprodukován. Řešení problému můžete obecně najít porovnáním kódu s dokončeným kódem. Některé běžné chyby a jejich řešení najdete v tématu [chyby a alternativní řešení.](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)

V předchozích dvou kurzech jste pracovali se souvisejícími daty. V tomto kurzu se dozvíte, jak zvládnout souběžnost. Vytvoříte webové stránky, které budou fungovat s entitou `Department`, a stránky, které upravují a odstraňují `Department` entity, budou zpracovávat chyby souběžnosti. Následující ilustrace znázorňují rejstřík a odstraňování stránek, včetně některých zpráv zobrazených v případě konfliktu souběžnosti.

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

## <a name="concurrency-conflicts"></a>Konflikty souběžnosti

Ke konfliktu souběžnosti dojde, když jeden uživatel zobrazuje data entity, aby je mohl upravit, a poté jiný uživatel aktualizuje data stejné entity před zápisem prvního uživatele do databáze. Pokud nepovolíte detekci takových konfliktů, si aktualizace databáze poslední přepíše změny provedené ostatními uživateli. V mnoha aplikacích je toto riziko přijatelné: v případě, že existuje několik uživatelů nebo málo aktualizací, nebo pokud jsou nějaké změny přepsány, náklady na programování pro souběžnost můžou převážit výhody. V takovém případě nemusíte konfigurovat aplikaci pro zpracování konfliktů souběžnosti.

### <a name="pessimistic-concurrency-locking"></a>Pesimistická souběžnost (uzamykání)

Pokud vaše aplikace potřebuje zabránit náhodné ztrátě dat ve scénářích souběžnosti, stačí jeden způsob, jak to provést, pomocí zámků databáze. Tato metoda se nazývá *pesimistická souběžnost*. Například před čtením řádku z databáze si vyžádáte zámek jen pro čtení nebo pro přístup k aktualizacím. Pokud zamknete řádek pro přístup k aktualizacím, žádní jiní uživatelé nemůžou Uzamknout řádek buď pro čtení, nebo pro přístup k aktualizacím, protože by získali kopii dat, která se v procesu mění. Pokud zamknete řádek pro přístup jen pro čtení, můžou ho jiní uživatelé taky uzamknout pro přístup jen pro čtení, ale ne pro aktualizace.

Správa zámků má nevýhody. Může být komplexní pro program. Vyžaduje významné prostředky správy databáze a může způsobit problémy s výkonem, protože se zvyšuje počet uživatelů aplikace (to znamená, že se nedokáže správně škálovat). Z těchto důvodů ne všechny systémy správy databáze podporují pesimistickou souběžnost. Entity Framework pro něj neposkytuje žádnou integrovanou podporu a v tomto kurzu se vám nezobrazí, jak ho implementovat.

### <a name="optimistic-concurrency"></a>Optimistická metoda souběžného zpracování

Alternativou k pesimistické souběžnosti je *Optimistická souběžnost*. Optimistická souběžnost znamená, že může dojít ke konfliktům souběžnosti a v případě, že je funguje správně. Například Jan spustí stránku pro úpravy oddělení, změní částku **rozpočtu** pro anglické oddělení z $350 000,00 na $0,00.

![Changing_English_dept_budget_to_100000](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

Až Jan klikne na **Uložit**, spustí Jana stejnou stránku a změní pole **počáteční datum** z 9/1/2007 na 8/8/2013.

![Changing_English_dept_start_date_to_1999](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

Jan klikne na **Uložit** jako první a uvidí jeho změnu, když se prohlížeč vrátí na stránku indexu, a potom Jana klikne na **Uložit**. Co bude dál se určuje podle způsobu zpracování konfliktů souběžnosti. Mezi tyto možnosti patří:

- Můžete sledovat, kterou vlastnost uživatel změnil, a aktualizovat pouze odpovídající sloupce v databázi. V ukázkovém scénáři by se neztratila žádná data, protože dva uživatelé aktualizovali různé vlastnosti. Když někdo příště prochází v anglickém oddělení, uvidí změny Jan i Jana – počáteční datum 8/8/2013 a rozpočet s nulovými dolary.

    Tato metoda aktualizace může snížit počet konfliktů, které by mohly mít za následek ztrátu dat, ale nemůže se vyhnout ztrátě dat, pokud se ve stejné vlastnosti entity provedou konkurenční změny. To, zda Entity Framework funguje tímto způsobem závisí na způsobu implementace kódu aktualizace. V rámci webové aplikace to často není praktické, protože může vyžadovat, abyste zachovali velké množství stavu, aby bylo možné sledovat všechny původní hodnoty vlastností pro entitu a také nové hodnoty. Udržování velkých objemů stavu může ovlivnit výkon aplikace, protože buď vyžaduje prostředky serveru, nebo musí být součástí samotné webové stránky (například ve skrytých polích).
- Můžete nechat změnu přepsat Jan. Když někdo příště prochází v anglickém oddělení, uvidí 8/8/2013 a obnovenou hodnotu $350 000,00. To se označuje jako *klient WINS* nebo *Poslední ve scénáři WINS* . (Hodnoty klienta mají přednost před tím, co je v úložišti dat.) Jak je uvedeno v části Úvod do této části, pokud neuděláte žádné kódování pro zpracování souběžnosti, k tomu dojde automaticky.
- Můžete zabránit tomu, aby se změna v databázi nástroje Jana aktualizovala. Obvykle by se zobrazila chybová zpráva, zobrazila se její aktuální stav dat a umožní jí, aby znovu použila změny, pokud je stále chce udělat. To se označuje jako scénář *služby WINS pro Store* . (Hodnoty úložiště dat mají přednost před hodnotami odeslanými klientem.) V tomto kurzu implementujete scénář služby WINS pro Store. Tato metoda zajistí, že nedojde k přepsání žádné změny bez upozornění uživatele na to, co se děje.

### <a name="detecting-concurrency-conflicts"></a>Zjišťování konfliktů souběžnosti

Konflikty můžete vyřešit zpracováním výjimek [OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx) , které Entity Framework vyvolá. Chcete-li zjistit, kdy vyvolat tyto výjimky, Entity Framework musí být schopna detekovat konflikty. Proto je nutné správně nakonfigurovat databázi a datový model. Mezi možnosti pro povolení detekce konfliktů patří následující:

- V tabulce databáze zahrňte sloupec sledování, který se dá použít k určení, kdy došlo ke změně řádku. Pak můžete nakonfigurovat Entity Framework pro zahrnutí tohoto sloupce do klauzule `Where` příkazů SQL `Update` nebo `Delete`.

    Datový typ sloupce sledování je obvykle [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx). Hodnota [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) je sekvenční číslo, které se zvýší pokaždé, když se řádek aktualizuje. V příkazu `Update` nebo `Delete` zahrnuje klauzule `Where` původní hodnotu sloupce sledování (původní verze řádku). Pokud byl aktualizovaný řádek změněn jiným uživatelem, hodnota ve sloupci `rowversion` se liší od původní hodnoty, takže příkaz `Update` nebo `Delete` nemůže najít řádek, který se má aktualizovat z důvodu klauzule `Where`. Pokud Entity Framework zjistí, že nebyly aktualizovány žádné řádky pomocí příkazu `Update` nebo `Delete` (tj. Pokud je počet ovlivněných řádků nula), interpretuje to jako konflikt souběžnosti.
- Nakonfigurujte Entity Framework tak, aby zahrnoval původní hodnoty všech sloupců v tabulce v klauzuli `Where` příkazů `Update` a `Delete`.

    Stejně jako v první možnosti, pokud se cokoli na řádku od prvního načtení řádku změnilo, klauzule `Where` nevrátí řádek, který se má aktualizovat, což Entity Framework interpretuje jako konflikt souběžnosti. U databázových tabulek, které mají mnoho sloupců, může tento přístup mít za následek velmi velké `Where` klauzule a může vyžadovat, abyste zachovali velké objemy stavů. Jak bylo uvedeno dříve, údržba velkých objemů stavu může ovlivnit výkon aplikace, protože vyžaduje prostředky serveru nebo musí být součástí samotné webové stránky. Proto se tento přístup obecně nedoporučuje a nejedná se o metodu používanou v tomto kurzu.

    Pokud chcete tento přístup implementovat do souběžnosti, je nutné označit všechny vlastnosti neprimárního klíče v entitě, pro kterou chcete sledovat souběžnost, přidáním atributu [ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx) do nich. Tato změna umožňuje Entity Framework zahrnout všechny sloupce v klauzuli SQL `WHERE` příkazů `UPDATE`.

Ve zbývající části tohoto kurzu přidáte vlastnost sledování [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) k entitě `Department`, vytvoříte kontroler a zobrazení a otestujete, zda vše funguje správně.

## <a name="add-an-optimistic-concurrency-property-to-the-department-entity"></a>Přidat vlastnost optimistického souběžnosti k entitě oddělení

Do *Models\Department.cs*přidejte vlastnost sledování s názvem `RowVersion`:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=18-19)]

Atribut [timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) určuje, že tento sloupec bude obsažen v klauzuli `Where` `Update` a `Delete` příkazy odeslané do databáze. Atribut se nazývá [časové razítko](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) , protože předchozí verze SQL Server používaly datový typ [časové razítko](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx) SQL předtím, než ho nahradí SQL [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) . Typ .NET pro `rowversion` je bajtové pole. Pokud dáváte přednost použití rozhraní Fluent API, můžete použít metodu [IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx) k určení vlastnosti sledování, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

Podívejte se na problém GitHubu [nahradit IsConcurrencyToken podle IsRowVersion](https://github.com/aspnet/AspNetDocs/issues/302).

Přidáním vlastnosti, kterou jste změnili databázový model, takže je nutné provést další migraci. V konzole správce balíčků (PMC) zadejte následující příkazy:

[!code-console[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cmd)]

## <a name="create-a-department-controller"></a>Vytvoření řadiče oddělení

Vytvořte řadič `Department` a zobrazení stejným způsobem jako ostatní řadiče pomocí následujících nastavení:

![Add_Controller_dialog_box_for_Department_controller](https://asp.net/media/2578041/Windows-Live-Writer_Handling-C.NET-MVC-Application-7-of-10h1_AFDC_Add_Controller_dialog_box_for_Department_controller_d1d9c788-f970-4d6a-9f5a-1eddc84330b7.png)

Do *Controllers\DepartmentController.cs*přidejte příkaz `using`:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

Změňte "LastName" na "FullName" všude v tomto souboru (čtyři výskyty), aby rozevírací seznamy správce oddělení budou obsahovat úplný název instruktora, nikoli jenom příjmení.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=1)]

Existující kód pro metodu `HttpPost` `Edit` nahraďte následujícím kódem:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

Zobrazení uloží původní hodnotu `RowVersion` ve skrytém poli. Když pořadač modelů vytvoří instanci `department`, bude mít tento objekt původní hodnotu vlastnosti `RowVersion` a nové hodnoty pro ostatní vlastnosti, jak zadal uživatel na stránce pro úpravy. Pak když Entity Framework vytvoří příkaz SQL `UPDATE`, bude tento příkaz obsahovat klauzuli `WHERE`, která hledá řádek, který má původní `RowVersion` hodnotu.

Pokud nejsou ovlivněny žádné řádky pomocí příkazu `UPDATE` (žádné řádky nemají původní `RowVersion` hodnotu), Entity Framework vyvolá výjimku `DbUpdateConcurrencyException` a kód v bloku `catch` získá ovlivněnou entitu `Department` z objektu Exception. Tato entita načte obě hodnoty z databáze a nové hodnoty zadané uživatelem:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

Dále kód přidá vlastní chybovou zprávu pro každý sloupec, který má hodnoty databáze jiné než uživatel zadaný na stránce pro úpravy:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

Delší chybová zpráva vysvětluje, co se stalo, a co dělat.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

Nakonec kód nastaví `RowVersion` hodnotu objektu `Department` na novou hodnotu načtenou z databáze. Tato nová hodnota `RowVersion` se uloží do skrytého pole, když se znovu zobrazí stránka pro úpravy, a když uživatel příště klikne na **Uložit**, zachytí se jenom chyby souběžnosti, ke kterým dochází, protože se znovu zobrazí stránka pro úpravy.

V *Views\Department\Edit.cshtml*přidejte skryté pole pro uložení hodnoty vlastnosti `RowVersion` hned za skryté pole pro vlastnost `DepartmentID`:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cshtml?highlight=17)]

V *Views\Department\Index.cshtml*nahraďte existující kód následujícím kódem pro přesunutí odkazů na řádky doleva a změňte nadpis stránky a záhlaví sloupců tak, aby se zobrazily `FullName` místo `LastName` ve sloupci **správce** :

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cshtml)]

## <a name="testing-optimistic-concurrency-handling"></a>Testování optimistického zpracování souběžnosti

Spusťte web a klikněte na **oddělení**:

![Department_Index_page_before_edits](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

Klikněte pravým **tlačítkem myši na hypertextový** odkaz pro Kim Abercrombie a vyberte **otevřít na nové kartě** a potom klikněte na odkaz **Upravit** pro Kim Abercrombie. Tato dvě okna zobrazují stejné informace.

![Department_Edit_page_before_changes](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

Změňte pole v prvním okně prohlížeče a klikněte na **Uložit**.

![Department_Edit_page_1_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

Prohlížeč zobrazí stránku indexu se změněnou hodnotou.

![Departments_Index_page_after_first_budget_edit](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

Změňte jakékoli pole v druhém okně prohlížeče a klikněte na **Uložit**.

![Department_Edit_page_2_after_change](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

V druhém okně prohlížeče klikněte na **Uložit** . Zobrazí se chybová zpráva:

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

Znovu klikněte na **Uložit** . Hodnota, kterou jste zadali ve druhém prohlížeči, se uloží spolu s původní hodnotou dat, která se mění v prvním prohlížeči. Po zobrazení stránky index se zobrazí uložené hodnoty.

![Department_Index_page_with_change_from_second_browser](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)

## <a name="updating-the-delete-page"></a>Aktualizace stránky pro odstranění

Pro stránku odstranění Entity Framework detekuje konflikty souběžnosti způsobené někým jiným upravováním oddělení podobným způsobem. Pokud metoda `HttpGet` `Delete` zobrazí zobrazení potvrzení, obsahuje zobrazení původní hodnotu `RowVersion` ve skrytém poli. Tato hodnota je pak k dispozici pro metodu `HttpPost` `Delete`, která je volána, když uživatel potvrdí odstranění. Když Entity Framework vytvoří příkaz SQL `DELETE`, zahrnuje klauzuli `WHERE` s původní `RowVersion`ou hodnotou. Pokud tento příkaz má vliv na nulové řádky (což znamená, že řádek byl změněn po zobrazení stránky pro potvrzení odstranění), je vyvolána výjimka souběžnosti a metoda `HttpGet Delete` je volána s příznakem chyby nastaveným na `true`, aby bylo možné znovu zobrazit potvrzovací stránku s chybovou zprávou. Je také možné, že došlo ke ovlivnění nulových řádků, protože řádek odstranil jiný uživatel, takže v takovém případě se zobrazí jiná chybová zpráva.

V *DepartmentController.cs*nahraďte metodu `HttpGet` `Delete` následujícím kódem:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cs)]

Metoda přijímá volitelný parametr, který označuje, zda se stránka po chybě souběžného zpracování znovu zobrazuje. Pokud je tento příznak `true`, pošle se do zobrazení chybová zpráva s použitím vlastnosti `ViewBag`.

Nahraďte kód v metodě `HttpPost` `Delete` (s názvem `DeleteConfirmed`) následujícím kódem:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

V právě vygenerovaném kódu jste tuto metodu přijali pouze s ID záznamu:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

Změnili jste tento parametr na instanci entity `Department`, kterou vytvořila pořadač modelů. Díky tomu získáte přístup k hodnotě vlastnosti `RowVersion` kromě klíče záznamu.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

Změnili jste také název metody akce z `DeleteConfirmed` na `Delete`. Generovaný kód s názvem `HttpPost` `Delete` metody `DeleteConfirmed` pro udělení jedinečného podpisu `HttpPost` metodě. (CLR vyžaduje, aby byly přetížené metody pro různé parametry metody.) Teď, když jsou podpisy jedinečné, můžete s úmluvou MVC pracovat a používat stejný název pro `HttpPost` a `HttpGet` odstranit metody.

Pokud je zachycena chyba souběžnosti, kód znovu zobrazí stránku pro potvrzení odstranění a poskytne příznak označující, že by měla zobrazit chybovou zprávu o souběžnosti.

V *Views\Department\Delete.cshtml*nahraďte generovaný kód následujícím kódem, který provede některé změny formátování, a přidá pole chybové zprávy. Změny jsou zvýrazněné.

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml?highlight=9,37,40,45-46)]

Tento kód přidá chybovou zprávu mezi `h2` a záhlaví `h3`:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

V poli `Administrator` nahrazuje `LastName` `FullName`:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

Nakonec přidá skrytá pole pro `DepartmentID` a vlastnosti `RowVersion` po příkazu `Html.BeginForm`:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

Spusťte stránku rejstřík oddělení. Klikněte pravým tlačítkem myši na hypertextový odkaz **Odstranit** pro anglické oddělení a vyberte **otevřít v novém okně** a potom v prvním okně klikněte na hypertextový odkaz **Upravit** pro anglické oddělení.

V prvním okně změňte jednu z hodnot a klikněte na **Uložit** :

![Department_Edit_page_after_change_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

Stránka index potvrzuje změnu.

![Departments_Index_page_after_budget_edit_before_delete](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)

V druhém okně klikněte na **Odstranit**.

![Department_Delete_confirmation_page_before_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)

Zobrazí se chybová zpráva o souběžnosti a hodnoty oddělení se aktualizují s tím, co je aktuálně v databázi.

![Department_Delete_confirmation_page_with_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

Pokud znovu kliknete na tlačítko **Odstranit** , budete přesměrováni na stránku index, která ukazuje, že oddělení bylo odstraněno.

## <a name="summary"></a>Souhrn

Tím se dokončí Úvod ke zpracování konfliktů souběžnosti. Informace o dalších způsobech zpracování různých scénářů souběžnosti naleznete v tématu [optimistické vzorce souběžnosti](https://blogs.msdn.com/b/adonet/archive/2011/02/03/using-dbcontext-in-ef-feature-ctp5-part-9-optimistic-concurrency-patterns.aspx) a [práce s hodnotami vlastností](https://blogs.msdn.com/b/adonet/archive/2011/01/30/using-dbcontext-in-ef-feature-ctp5-part-5-working-with-property-values.aspx) na blogu týmu Entity Framework. V dalším kurzu se dozvíte, jak implementovat dědičnost tabulek na hierarchii pro `Instructor` a `Student` entity.

Odkazy na další prostředky Entity Framework najdete v [mapě obsahu pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

> [!div class="step-by-step"]
> [Předchozí](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)
> [Další](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)

---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Kurz: zpracování souběžnosti s EF v aplikaci ASP.NET MVC 5'
description: V tomto kurzu se dozvíte, jak používat optimistickou souběžnost ke zpracování konfliktů, když více uživatelů aktualizuje stejnou entitu ve stejnou dobu.
author: tdykstra
ms.author: riande
ms.topic: tutorial
ms.date: 01/15/2019
ms.assetid: be0c098a-1fb2-457e-b815-ddca601afc65
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 43c5fdff5601c9bff32300d3460de0079a498d28
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616107"
---
# <a name="tutorial-handle-concurrency-with-ef-in-an-aspnet-mvc-5-app"></a>Kurz: zpracování souběžnosti s EF v aplikaci ASP.NET MVC 5

V předchozích kurzech jste zjistili, jak aktualizovat data. V tomto kurzu se dozvíte, jak používat optimistickou souběžnost ke zpracování konfliktů, když více uživatelů aktualizuje stejnou entitu ve stejnou dobu. Webové stránky, které pracují s entitou `Department`, změníte tak, aby zpracovaly chyby souběžnosti. Následující ilustrace znázorňují stránky upravit a odstranit, včetně některých zpráv zobrazených v případě, že dojde ke konfliktu souběžnosti.

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Další informace o konfliktech souběžnosti
> * Přidat optimistickou souběžnost
> * Upravit kontroler oddělení
> * Zpracování souběžnosti testů
> * Aktualizovat stránku Delete

## <a name="prerequisites"></a>Předpoklady

* [Async a uložené procedury](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="concurrency-conflicts"></a>Konflikty souběžnosti

Ke konfliktu souběžnosti dojde, když jeden uživatel zobrazuje data entity, aby je mohl upravit, a poté jiný uživatel aktualizuje data stejné entity před zápisem prvního uživatele do databáze. Pokud nepovolíte detekci takových konfliktů, si aktualizace databáze poslední přepíše změny provedené ostatními uživateli. V mnoha aplikacích je toto riziko přijatelné: v případě, že existuje několik uživatelů nebo málo aktualizací, nebo pokud jsou nějaké změny přepsány, náklady na programování pro souběžnost můžou převážit výhody. V takovém případě nemusíte konfigurovat aplikaci pro zpracování konfliktů souběžnosti.

### <a name="pessimistic-concurrency-locking"></a>Pesimistická souběžnost (uzamykání)

Pokud vaše aplikace potřebuje zabránit náhodné ztrátě dat ve scénářích souběžnosti, stačí jeden způsob, jak to provést, pomocí zámků databáze. Tato metoda se nazývá *pesimistická souběžnost*. Například před čtením řádku z databáze si vyžádáte zámek jen pro čtení nebo pro přístup k aktualizacím. Pokud zamknete řádek pro přístup k aktualizacím, žádní jiní uživatelé nemůžou Uzamknout řádek buď pro čtení, nebo pro přístup k aktualizacím, protože by získali kopii dat, která se v procesu mění. Pokud zamknete řádek pro přístup jen pro čtení, můžou ho jiní uživatelé taky uzamknout pro přístup jen pro čtení, ale ne pro aktualizace.

Správa zámků má nevýhody. Může být komplexní pro program. Vyžaduje významné prostředky správy databáze a může způsobit problémy s výkonem, protože se zvyšuje počet uživatelů aplikace. Z těchto důvodů ne všechny systémy správy databáze podporují pesimistickou souběžnost. Entity Framework pro něj neposkytuje žádnou integrovanou podporu a v tomto kurzu se vám nezobrazí, jak ho implementovat.

### <a name="optimistic-concurrency"></a>Optimistická metoda souběžného zpracování

Alternativou k pesimistické souběžnosti je *Optimistická souběžnost*. Optimistická souběžnost znamená, že může dojít ke konfliktům souběžnosti a v případě, že je funguje správně. Například Jan spustí stránku pro úpravy oddělení, změní částku **rozpočtu** pro anglické oddělení z $350 000,00 na $0,00.

Až Jan klikne na **Uložit**, spustí Jana stejnou stránku a změní pole **počáteční datum** z 9/1/2007 na 8/8/2013.

Jan klikne na **Uložit** jako první a uvidí jeho změnu, když se prohlížeč vrátí na stránku indexu, a potom Jana klikne na **Uložit**. Co bude dál se určuje podle způsobu zpracování konfliktů souběžnosti. Mezi tyto možnosti patří:

- Můžete sledovat, kterou vlastnost uživatel změnil, a aktualizovat pouze odpovídající sloupce v databázi. V ukázkovém scénáři by se neztratila žádná data, protože dva uživatelé aktualizovali různé vlastnosti. Když někdo příště prochází v anglickém oddělení, uvidí změny Jan i Jana – počáteční datum 8/8/2013 a rozpočet s nulovými dolary.

    Tato metoda aktualizace může snížit počet konfliktů, které by mohly mít za následek ztrátu dat, ale nemůže se vyhnout ztrátě dat, pokud se ve stejné vlastnosti entity provedou konkurenční změny. To, zda Entity Framework funguje tímto způsobem závisí na způsobu implementace kódu aktualizace. V rámci webové aplikace to často není praktické, protože může vyžadovat, abyste zachovali velké množství stavu, aby bylo možné sledovat všechny původní hodnoty vlastností pro entitu a také nové hodnoty. Udržování velkých objemů stavu může ovlivnit výkon aplikace, protože buď vyžaduje prostředky serveru, nebo musí být součástí samotné webové stránky (například v skrytých polích) nebo v souboru cookie.
- Můžete nechat změnu přepsat Jan. Když někdo příště prochází v anglickém oddělení, uvidí 8/8/2013 a obnovenou hodnotu $350 000,00. To se označuje jako *klient WINS* nebo *Poslední ve scénáři WINS* . (Všechny hodnoty z klienta mají přednost před tím, co je v úložišti dat.) Jak je uvedeno v části Úvod do této části, pokud neuděláte žádné kódování pro zpracování souběžnosti, k tomu dojde automaticky.
- Můžete zabránit tomu, aby se změna v databázi nástroje Jana aktualizovala. Obvykle by se zobrazila chybová zpráva, zobrazila se její aktuální stav dat a umožní jí, aby znovu použila změny, pokud je stále chce udělat. To se označuje jako scénář *služby WINS pro Store* . (Hodnoty úložiště dat mají přednost před hodnotami odeslanými klientem.) V tomto kurzu implementujete scénář služby WINS pro Store. Tato metoda zajistí, že nedojde k přepsání žádné změny bez upozornění uživatele na to, co se děje.

### <a name="detecting-concurrency-conflicts"></a>Zjišťování konfliktů souběžnosti

Konflikty můžete vyřešit zpracováním výjimek [OptimisticConcurrencyException](https://msdn.microsoft.com/library/system.data.optimisticconcurrencyexception.aspx) , které Entity Framework vyvolá. Chcete-li zjistit, kdy vyvolat tyto výjimky, Entity Framework musí být schopna detekovat konflikty. Proto je nutné správně nakonfigurovat databázi a datový model. Mezi možnosti pro povolení detekce konfliktů patří následující:

- V tabulce databáze zahrňte sloupec sledování, který se dá použít k určení, kdy došlo ke změně řádku. Pak můžete nakonfigurovat Entity Framework pro zahrnutí tohoto sloupce do klauzule `Where` příkazů SQL `Update` nebo `Delete`.

    Datový typ sloupce sledování je obvykle [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx). Hodnota [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) je sekvenční číslo, které se zvýší pokaždé, když se řádek aktualizuje. V příkazu `Update` nebo `Delete` zahrnuje klauzule `Where` původní hodnotu sloupce sledování (původní verze řádku). Pokud byl aktualizovaný řádek změněn jiným uživatelem, hodnota ve sloupci `rowversion` se liší od původní hodnoty, takže příkaz `Update` nebo `Delete` nemůže najít řádek, který se má aktualizovat z důvodu klauzule `Where`. Pokud Entity Framework zjistí, že nebyly aktualizovány žádné řádky pomocí příkazu `Update` nebo `Delete` (tj. Pokud je počet ovlivněných řádků nula), interpretuje to jako konflikt souběžnosti.
- Nakonfigurujte Entity Framework tak, aby zahrnoval původní hodnoty všech sloupců v tabulce v klauzuli `Where` příkazů `Update` a `Delete`.

    Stejně jako v první možnosti, pokud se cokoli na řádku od prvního načtení řádku změnilo, klauzule `Where` nevrátí řádek, který se má aktualizovat, což Entity Framework interpretuje jako konflikt souběžnosti. U databázových tabulek, které mají mnoho sloupců, může tento přístup mít za následek velmi velké `Where` klauzule a může vyžadovat, abyste zachovali velké objemy stavů. Jak bylo uvedeno dříve, údržba velkých objemů stavu může ovlivnit výkon aplikace. Proto se tento přístup obecně nedoporučuje a nejedná se o metodu používanou v tomto kurzu.

    Pokud chcete tento přístup implementovat do souběžnosti, je nutné označit všechny vlastnosti neprimárního klíče v entitě, pro kterou chcete sledovat souběžnost, přidáním atributu [ConcurrencyCheck](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.concurrencycheckattribute.aspx) do nich. Tato změna umožňuje Entity Framework zahrnout všechny sloupce v klauzuli SQL `WHERE` příkazů `UPDATE`.

Ve zbývající části tohoto kurzu přidáte vlastnost sledování [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) k entitě `Department`, vytvoříte kontroler a zobrazení a otestujete, zda vše funguje správně.

## <a name="add-optimistic-concurrency"></a>Přidat optimistickou souběžnost

Do *Models\Department.cs*přidejte vlastnost sledování s názvem `RowVersion`:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=20-22)]

Atribut [timestamp](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) určuje, že tento sloupec bude obsažen v klauzuli `Where` `Update` a `Delete` příkazy odeslané do databáze. Atribut se nazývá [časové razítko](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.timestampattribute.aspx) , protože předchozí verze SQL Server používaly datový typ [časové razítko](https://msdn.microsoft.com/library/ms182776(v=SQL.90).aspx) SQL předtím, než ho nahradí SQL [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) . Typ .NET pro [rowversion](https://msdn.microsoft.com/library/ms182776(v=sql.110).aspx) je bajtové pole.

Pokud dáváte přednost použití rozhraní Fluent API, můžete použít metodu [IsConcurrencyToken](https://msdn.microsoft.com/library/gg679501(v=VS.103).aspx) k určení vlastnosti sledování, jak je znázorněno v následujícím příkladu:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

Přidáním vlastnosti, kterou jste změnili databázový model, takže je nutné provést další migraci. V konzole správce balíčků (PMC) zadejte následující příkazy:

[!code-console[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cmd)]

## <a name="modify-department-controller"></a>Upravit kontroler oddělení

Do *Controllers\DepartmentController.cs*přidejte příkaz `using`:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

V souboru *DepartmentController.cs* změňte všechny čtyři výskyty "LastName" na "FullName", aby rozevírací seznamy správce oddělení obsahovaly celé jméno instruktora, nikoli jenom příjmení.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs?highlight=1)]

Existující kód pro metodu `HttpPost` `Edit` nahraďte následujícím kódem:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

Pokud metoda `FindAsync` vrátí hodnotu null, oddělení bylo odstraněno jiným uživatelem. Zobrazený kód používá hodnoty odeslaného formuláře k vytvoření entity oddělení, aby bylo možné upravit stránku úprav, aby se mohla znovu zobrazit chybová zpráva. Jako alternativu nebudete muset entitu oddělení znovu vytvořit, pokud se zobrazí pouze chybová zpráva bez zobrazení polí oddělení.

Zobrazení ukládá původní hodnotu `RowVersion` ve skrytém poli a metoda ji přijímá v parametru `rowVersion`. Před voláním `SaveChanges`je nutné do kolekce `OriginalValues` pro entitu vložit původní hodnotu vlastnosti `RowVersion`. Pak když Entity Framework vytvoří příkaz SQL `UPDATE`, bude tento příkaz obsahovat klauzuli `WHERE`, která hledá řádek, který má původní `RowVersion` hodnotu.

Pokud nejsou ovlivněny žádné řádky pomocí příkazu `UPDATE` (žádné řádky nemají původní `RowVersion` hodnotu), Entity Framework vyvolá výjimku `DbUpdateConcurrencyException` a kód v bloku `catch` získá ovlivněnou entitu `Department` z objektu Exception.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

Tento objekt má nové hodnoty zadané uživatelem v jeho vlastnosti `Entity` a můžete načíst hodnoty načtené z databáze voláním metody `GetDatabaseValues`.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

Metoda `GetDatabaseValues` vrátí hodnotu null, pokud někdo odstranil řádek z databáze. v opačném případě je nutné přetypování vráceného objektu na třídu `Department`, aby bylo možné získat přístup k vlastnostem `Department`. (Vzhledem k tomu, že jste již kontrolovali odstranění, `databaseEntry` by byl null pouze v případě, že se oddělení odstranilo po `FindAsync` provedení a před provedením `SaveChanges`.)

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

Dále kód přidá vlastní chybovou zprávu pro každý sloupec, který má hodnoty databáze jiné než uživatel zadaný na stránce pro úpravy:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

Delší chybová zpráva vysvětluje, co se stalo, a co dělat.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

Nakonec kód nastaví `RowVersion` hodnotu objektu `Department` na novou hodnotu načtenou z databáze. Tato nová hodnota `RowVersion` se uloží do skrytého pole, když se znovu zobrazí stránka pro úpravy, a když uživatel příště klikne na **Uložit**, zachytí se jenom chyby souběžnosti, ke kterým dochází, protože se znovu zobrazí stránka pro úpravy.

V *Views\Department\Edit.cshtml*přidejte skryté pole pro uložení hodnoty vlastnosti `RowVersion` hned za skryté pole pro vlastnost `DepartmentID`:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=18)]

## <a name="test-concurrency-handling"></a>Zpracování souběžnosti testů

Spusťte web a klikněte na **oddělení**.

Klikněte pravým tlačítkem myši **na hypertextový** odkaz pro jazykové oddělení a vyberte **otevřít na nové kartě** a pak klikněte na hypertextový odkaz pro **Úpravy** v anglickém oddělení. Tyto dvě karty zobrazují stejné informace.

Změňte pole na první kartě prohlížeče a klikněte na **Uložit**.

Prohlížeč zobrazí stránku indexu se změněnou hodnotou.

Změňte pole na druhé kartě prohlížeče a klikněte na **Uložit**. Zobrazí se chybová zpráva:

![Department_Edit_page_2_after_clicking_Save](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

Znovu klikněte na **Uložit** . Hodnota, kterou jste zadali na druhé záložce prohlížeče, se uloží spolu s původní hodnotou dat, která jste změnili v prvním prohlížeči. Po zobrazení stránky index se zobrazí uložené hodnoty.

## <a name="update-the-delete-page"></a>Aktualizovat stránku Delete

Pro stránku odstranění Entity Framework detekuje konflikty souběžnosti způsobené někým jiným upravováním oddělení podobným způsobem. Pokud metoda `HttpGet` `Delete` zobrazí zobrazení potvrzení, obsahuje zobrazení původní hodnotu `RowVersion` ve skrytém poli. Tato hodnota je pak k dispozici pro metodu `HttpPost` `Delete`, která je volána, když uživatel potvrdí odstranění. Když Entity Framework vytvoří příkaz SQL `DELETE`, zahrnuje klauzuli `WHERE` s původní `RowVersion`ou hodnotou. Pokud tento příkaz má vliv na nulové řádky (což znamená, že řádek byl změněn po zobrazení stránky pro potvrzení odstranění), je vyvolána výjimka souběžnosti a metoda `HttpGet Delete` je volána s příznakem chyby nastaveným na `true`, aby bylo možné znovu zobrazit potvrzovací stránku s chybovou zprávou. Je také možné, že došlo ke ovlivnění nulových řádků, protože řádek odstranil jiný uživatel, takže v takovém případě se zobrazí jiná chybová zpráva.

V *DepartmentController.cs*nahraďte metodu `HttpGet` `Delete` následujícím kódem:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cs)]

Metoda přijímá volitelný parametr, který označuje, zda se stránka po chybě souběžného zpracování znovu zobrazuje. Pokud je tento příznak `true`, pošle se do zobrazení chybová zpráva s použitím vlastnosti `ViewBag`.

Nahraďte kód v metodě `HttpPost` `Delete` (s názvem `DeleteConfirmed`) následujícím kódem:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cs)]

V právě vygenerovaném kódu jste tuto metodu přijali pouze s ID záznamu:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cs)]

Změnili jste tento parametr na instanci entity `Department`, kterou vytvořila pořadač modelů. Díky tomu získáte přístup k hodnotě vlastnosti `RowVersion` kromě klíče záznamu.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cs)]

Změnili jste také název metody akce z `DeleteConfirmed` na `Delete`. Generovaný kód s názvem `HttpPost` `Delete` metody `DeleteConfirmed` pro udělení jedinečného podpisu `HttpPost` metodě. (CLR vyžaduje, aby byly přetížené metody pro různé parametry metody.) Teď, když jsou podpisy jedinečné, můžete s úmluvou MVC pracovat a používat stejný název pro `HttpPost` a `HttpGet` odstranit metody.

Pokud je zachycena chyba souběžnosti, kód znovu zobrazí stránku pro potvrzení odstranění a poskytne příznak označující, že by měla zobrazit chybovou zprávu o souběžnosti.

V *Views\Department\Delete.cshtml*nahraďte generovaný kód následujícím kódem, který přidá pole chybové zprávy a skrytá pole pro vlastnosti DepartmentID a rowversion. Změny jsou zvýrazněné.

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml?highlight=9-10,21,52-54)]

Tento kód přidá chybovou zprávu mezi `h2` a záhlaví `h3`:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cshtml)]

V poli `Administrator` nahrazuje `LastName` `FullName`:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cshtml)]

Nakonec přidá skrytá pole pro `DepartmentID` a vlastnosti `RowVersion` po příkazu `Html.BeginForm`:

[!code-cshtml[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cshtml)]

Spusťte stránku rejstřík oddělení. Klikněte pravým tlačítkem myši na hypertextový odkaz **Odstranit** pro anglické oddělení a vyberte **otevřít na nové kartě** a pak na první kartě klikněte na odkaz **Upravit** pro anglické oddělení.

V prvním okně změňte jednu z hodnot a klikněte na **Uložit**.

Stránka index potvrzuje změnu.

Na druhé kartě klikněte na **Odstranit**.

Zobrazí se chybová zpráva o souběžnosti a hodnoty oddělení se aktualizují s tím, co je aktuálně v databázi.

![Department_Delete_confirmation_page_with_concurrency_error](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)

Pokud znovu kliknete na tlačítko **Odstranit** , budete přesměrováni na stránku index, která ukazuje, že oddělení bylo odstraněno.

## <a name="get-the-code"></a>Získání kódu

[Stáhnout dokončený projekt](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Další zdroje

Odkazy na další prostředky Entity Framework najdete v [prostředcích, které jsou doporučeny pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

Informace o jiných způsobech zpracování různých scénářů souběžnosti naleznete v tématu [optimistické vzorce souběžnosti](https://msdn.microsoft.com/data/jj592904) a [práce s hodnotami vlastností](https://msdn.microsoft.com/data/jj592677) na webu MSDN. V dalším kurzu se dozvíte, jak implementovat dědičnost tabulek na hierarchii pro `Instructor` a `Student` entity.

## <a name="next-steps"></a>Další kroky

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Dozvědělo se o konfliktech souběžnosti
> * Přidání optimistického řízení souběžnosti
> * Změněný kontroler oddělení
> * Testované zpracování souběžnosti
> * Aktualizace stránky odstranění

V dalším článku se dozvíte, jak implementovat dědičnost v datovém modelu.
> [!div class="nextstepaction"]
> [Implementace dědičnosti v datovém modelu](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)

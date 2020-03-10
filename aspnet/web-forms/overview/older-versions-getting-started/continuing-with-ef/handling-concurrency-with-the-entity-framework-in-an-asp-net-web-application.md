---
uid: web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
title: Zpracování souběžnosti s Entity Framework 4,0 ve webové aplikaci ASP.NET 4 | Microsoft Docs
author: tdykstra
description: Tato řada kurzů se sestavuje na webové aplikaci Contoso University, která je vytvořená Začínáme pomocí řady kurzů Entity Framework 4,0. I...
ms.author: riande
ms.date: 01/26/2011
ms.assetid: a5aa22a6-fb7f-4f41-9c7f-addda151940b
msc.legacyurl: /web-forms/overview/older-versions-getting-started/continuing-with-ef/handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application
msc.type: authoredcontent
ms.openlocfilehash: 3df5f7d9c8fb22e1ea34fe16560bdb9a1309bb56
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78632585"
---
# <a name="handling-concurrency-with-the-entity-framework-40-in-an-aspnet-4-web-application"></a>Zpracování souběžnosti s Entity Framework 4,0 ve webové aplikaci ASP.NET 4

tím, že [Dykstra](https://github.com/tdykstra)

> Tato řada kurzů se sestavuje na webové aplikaci Contoso University, která je vytvořená [Začínáme pomocí řady kurzů Entity Framework 4,0](https://asp.net/entity-framework/tutorials#Getting%20Started) . Pokud jste nedokončili předchozí kurzy, jako výchozí bod tohoto kurzu si můžete aplikaci, kterou jste vytvořili, [Stáhnout](https://code.msdn.microsoft.com/ASPNET-Web-Forms-97f8ee9a) . Můžete si také [Stáhnout aplikaci](https://code.msdn.microsoft.com/ASPNET-Web-Forms-6c7197aa) , která je vytvořená úplnou řadou kurzů. Pokud máte dotazy k kurzům, můžete je publikovat na [fórum ASP.NET Entity Framework](https://forums.asp.net/1227.aspx).

V předchozím kurzu jste zjistili, jak řadit a filtrovat data pomocí ovládacího prvku `ObjectDataSource` a Entity Framework. V tomto kurzu se dozvíte o možnostech zpracování souběžnosti ve webové aplikaci v ASP.NET, která používá Entity Framework. Vytvoří se nová webová stránka, která je vyhrazená pro aktualizaci přiřazení instruktor kanceláře. Budete zpracovávat problémy souběžnosti na této stránce a na stránce oddělení, kterou jste vytvořili dříve.

[![Image06](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image2.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image1.png)

[![Image01](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image4.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image3.png)

## <a name="concurrency-conflicts"></a>Konflikty souběžnosti

Ke konfliktu souběžnosti dojde, když jeden uživatel upraví záznam a jiný uživatel upraví stejný záznam předtím, než se do databáze zapíše Změna prvního uživatele. Pokud nenastavíte Entity Framework k detekci takových konfliktů, při aktualizaci databáze poslední přepíše změny provedené ostatními uživateli. V mnoha aplikacích je toto riziko přijatelné a vy nemusíte konfigurovat aplikaci tak, aby zpracovávala možné konflikty souběžnosti. (Pokud je k dispozici málo uživatelů nebo málo aktualizací, nebo pokud není důležité, pokud jsou nějaké změny přepsány, náklady na programování pro souběžnost můžou převážit výhody.) Pokud se nemusíte starat o konflikty souběžnosti, můžete tento kurz přeskočit; zbývající dva kurzy v řadě nejsou závislé na nic, co v tomto případě sestavíte.

### <a name="pessimistic-concurrency-locking"></a>Pesimistická souběžnost (uzamykání)

Pokud vaše aplikace potřebuje zabránit náhodné ztrátě dat ve scénářích souběžnosti, stačí jeden způsob, jak to provést, pomocí zámků databáze. Tato metoda se nazývá *pesimistická souběžnost*. Například před čtením řádku z databáze si vyžádáte zámek jen pro čtení nebo pro přístup k aktualizacím. Pokud zamknete řádek pro přístup k aktualizacím, žádní jiní uživatelé nemůžou Uzamknout řádek buď pro čtení, nebo pro přístup k aktualizacím, protože by získali kopii dat, která se v procesu mění. Pokud zamknete řádek pro přístup jen pro čtení, můžou ho jiní uživatelé taky uzamknout pro přístup jen pro čtení, ale ne pro aktualizace.

Správa zámků má některé nevýhody. Může být komplexní pro program. Vyžaduje významné prostředky správy databáze a může způsobit problémy s výkonem, protože se zvyšuje počet uživatelů aplikace (to znamená, že se nedokáže správně škálovat). Z těchto důvodů ne všechny systémy správy databáze podporují pesimistickou souběžnost. Entity Framework pro něj neposkytuje žádnou integrovanou podporu a v tomto kurzu se vám nezobrazí, jak ho implementovat.

### <a name="optimistic-concurrency"></a>Optimistická metoda souběžného zpracování

Alternativou k pesimistické souběžnosti je *Optimistická souběžnost*. Optimistická souběžnost znamená, že může dojít ke konfliktům souběžnosti a v případě, že je funguje správně. Například Jan spustí stránku *oddělení. aspx* , klikne na odkaz **Upravit** pro oddělení historie a sníží částku **rozpočtu** z $1 000 000,00 na $125 000,00. (Jan spravuje konkurenční oddělení a chce zdarma uvolnit peníze pro vlastní oddělení.)

[![Image07](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image6.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image5.png)

Když Jan klikne na **aktualizovat**, spustí Jana stejnou stránku, klikne na odkaz **Upravit** pro oddělení historie a pak změní pole **počáteční datum** z 1/10/2011 na 1/1/1999. (Jana spravuje oddělení historie a chce dát mu větší služební věk.)

[![Image08](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image8.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image7.png)

Jan klikne na **aktualizovat** jako první a pak Jana klikne na **aktualizovat**. V prohlížeči Jana se nyní zobrazí hodnota **rozpočtu** jako $1 000 000,00, ale to není správné, protože se změnila hodnota od jan do $125 000,00.

V tomto scénáři můžete použít následující akce:

- Můžete sledovat, kterou vlastnost uživatel změnil, a aktualizovat pouze odpovídající sloupce v databázi. V ukázkovém scénáři by se neztratila žádná data, protože dva uživatelé aktualizovali různé vlastnosti. Když někdo příště prochází oddělení historie, uvidí 1/1/1999 a $125 000,00. 

    Toto je výchozí chování Entity Framework a může podstatně snížit počet konfliktů, které by mohly vést ke ztrátě dat. Toto chování však nebrání ztrátě dat, pokud jsou v rámci stejné vlastnosti entity provedeny konkurenční změny. Kromě toho toto chování není vždy možné; Když namapujete uložené procedury na typ entity, aktualizují se všechny vlastnosti entity, když se v databázi provedou jakékoli změny entity.
- Můžete nechat změnu přepsat Jan. Jakmile Jana klikne na **aktualizovat**, částka **rozpočtu** se vrátí do $1 000 000,00. To se označuje jako *klient WINS* nebo *Poslední ve scénáři WINS* . (Hodnoty klienta mají přednost před tím, co je v úložišti dat.)
- Můžete zabránit tomu, aby se změna v databázi nástroje Jana aktualizovala. Obvykle byste zobrazili chybovou zprávu, zobrazila její aktuální stav dat a umožní jí znovu zadat změny, pokud je stále chce udělat. Proces můžete dále automatizovat uložením jeho vstupu a tím, že ho budete moct znovu použít, aniž byste ho museli znovu zadávat. To se označuje jako scénář *služby WINS pro Store* . (Hodnoty úložiště dat přednost hodnoty odeslány klientem.)

### <a name="detecting-concurrency-conflicts"></a>Zjišťování konfliktů souběžnosti

V Entity Framework můžete vyřešit konflikty zpracováním `OptimisticConcurrencyException` výjimek, které Entity Framework vyvolá. Chcete-li zjistit, kdy vyvolat tyto výjimky, Entity Framework musí být schopna detekovat konflikty. Proto je nutné správně nakonfigurovat databázi a datový model. Mezi možnosti pro povolení detekce konfliktů patří následující:

- V databázi zahrňte sloupec tabulky, který se dá použít k určení, kdy došlo ke změně řádku. Pak můžete nakonfigurovat Entity Framework pro zahrnutí tohoto sloupce do klauzule `Where` příkazů SQL `Update` nebo `Delete`.

    To je účel sloupce `Timestamp` v tabulce `OfficeAssignment`.

    [![Image09](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image10.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image9.png)

    Datový typ sloupce `Timestamp` se také označuje jako `Timestamp`. Sloupec ale ve skutečnosti neobsahuje hodnotu data nebo času. Místo toho je hodnota sekvenční číslo, které se zvýší pokaždé, když se řádek aktualizuje. V příkazu `Update` nebo `Delete` zahrnuje klauzule `Where` původní `Timestamp` hodnotu. Pokud byl aktualizovaný řádek změněn jiným uživatelem, hodnota v `Timestamp` se liší od původní hodnoty, takže klauzule `Where` nevrátí žádný řádek, který se má aktualizovat. Pokud Entity Framework zjistí, že aktuální `Update` nebo `Delete` příkaz neaktualizoval žádné řádky (tj. Pokud je počet ovlivněných řádků nula), interpretuje to jako konflikt souběžnosti.
- Nakonfigurujte Entity Framework tak, aby zahrnoval původní hodnoty všech sloupců v tabulce v klauzuli `Where` příkazů `Update` a `Delete`.

    Stejně jako v první možnosti, pokud se cokoli na řádku od prvního načtení řádku změnilo, klauzule `Where` nevrátí řádek, který se má aktualizovat, což Entity Framework interpretuje jako konflikt souběžnosti. Tato metoda je platná jako při použití pole `Timestamp`, ale může být neefektivní. U databázových tabulek, které mají mnoho sloupců, může být výsledkem velmi velkých `Where` klauzulí a ve webové aplikaci může vyžadovat, abyste zachovali velké množství stavu. Udržování velkých objemů stavu může ovlivnit výkon aplikace, protože buď vyžaduje prostředky serveru (například stav relace), nebo musí být součástí samotné webové stránky (například stav zobrazení).

V tomto kurzu přidáte zpracování chyb pro konflikty optimistického souběžnosti pro entitu, která nemá vlastnost sledování (`Department` entitu), a pro entitu, která má vlastnost sledování (`OfficeAssignment` entita).

## <a name="handling-optimistic-concurrency-without-a-tracking-property"></a>Zpracovává se Optimistická souběžnost bez vlastnosti sledování.

K implementaci optimistického řízení souběžnosti pro entitu `Department`, která nemá vlastnost sledování (`Timestamp`), dokončíte následující úlohy:

- Změňte datový model tak, aby povoloval sledování souběžnosti pro `Department` entit.
- Ve třídě `SchoolRepository` zpracujte výjimky souběžnosti v metodě `SaveChanges`.
- Na stránce *oddělení. aspx* můžete zpracovat výjimky souběžnosti tím, že se uživateli zobrazí zpráva s upozorněním, že se provedené změny nezdařily. Uživatel pak může zobrazit aktuální hodnoty a opakovat změny, pokud jsou stále potřeba.

### <a name="enabling-concurrency-tracking-in-the-data-model"></a>Povolení sledování souběžnosti v datovém modelu

V sadě Visual Studio otevřete webovou aplikaci Contoso University, se kterou jste pracovali v předchozím kurzu této série.

Otevřete *SchoolModel. edmx*a v návrháři datového modelu klikněte pravým tlačítkem na vlastnost `Name` v entitě `Department` a pak klikněte na **vlastnosti**. V okně **vlastnosti** změňte vlastnost `ConcurrencyMode` na hodnotu `Fixed`.

[![Image16](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image12.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image11.png)

Totéž udělejte u ostatních skalárních vlastností, které nejsou primárním klíčem (`Budget`, `StartDate`a `Administrator`.) (To nejde udělat pro navigační vlastnosti.) To určuje, že pokaždé, když Entity Framework generuje příkaz jazyka SQL `Update` nebo `Delete`, který aktualizuje entitu `Department` v databázi, musí být v klauzuli `Where` zahrnuté tyto sloupce (s původními hodnotami). Pokud není nalezen žádný řádek při spuštění příkazu `Update` nebo `Delete`, Entity Framework vyvolá výjimku optimistického zpracování.

Uložte a zavřete datový model.

### <a name="handling-concurrency-exceptions-in-the-dal"></a>Zpracování výjimek souběžnosti v DAL

Otevřete *SchoolRepository.cs* a přidejte následující příkaz `using` pro obor názvů `System.Data`:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample1.cs)]

Přidejte následující novou `SaveChanges` metodu, která zpracovává optimistické výjimky souběžnosti:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample2.cs)]

Pokud při volání této metody dojde k chybě souběžnosti, hodnoty vlastností entity v paměti jsou nahrazeny hodnotami, které jsou aktuálně v databázi. Výjimka souběžnosti je znovu vyvolána, aby ji webová stránka mohla zpracovat.

V metodách `DeleteDepartment` a `UpdateDepartment` nahraďte existující volání `context.SaveChanges()` voláním `SaveChanges()`, aby bylo možné vyvolat novou metodu.

### <a name="handling-concurrency-exceptions-in-the-presentation-layer"></a>Zpracování výjimek souběžnosti v prezentační vrstvě

Otevřete panel *oddělení. aspx* a přidejte `OnDeleted="DepartmentsObjectDataSource_Deleted"` atribut pro ovládací prvek `DepartmentsObjectDataSource`. Otevírací značka ovládacího prvku bude nyní vypadat podobně jako v následujícím příkladu.

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample3.aspx)]

V ovládacím prvku `DepartmentsGridView` zadejte všechny sloupce tabulky v atributu `DataKeyNames`, jak je znázorněno v následujícím příkladu. Všimněte si, že se tím vytvoří velmi rozsáhlá pole stavu zobrazení, což je jeden z důvodů, proč použití sledovacího pole obvykle představuje preferovaný způsob, jak sledovat konflikty souběžnosti.

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample4.aspx)]

Otevřete *departments.aspx.cs* a přidejte následující příkaz `using` pro obor názvů `System.Data`:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample5.cs)]

Přidejte následující novou metodu, kterou budete volat z `Updated` a obslužné rutiny události `Deleted` ovládacího prvku zdroje dat pro zpracování výjimek souběžnosti:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample6.cs)]

Tento kód kontroluje typ výjimky, a pokud se jedná o výjimku souběžnosti, kód dynamicky vytvoří ovládací prvek `CustomValidator`, který zase zobrazí zprávu v ovládacím prvku `ValidationSummary`.

Zavolejte novou metodu z obslužné rutiny události `Updated`, kterou jste přidali dříve. Kromě toho vytvořte novou `Deleted` obslužnou rutinu události, která volá stejnou metodu (ale neprovede žádnou jinou):

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample7.cs)]

### <a name="testing-optimistic-concurrency-in-the-departments-page"></a>Testování optimistické souběžnosti na stránce oddělení

Spusťte stránku *oddělení. aspx* .

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image14.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image13.png)

V řádku klikněte na **Upravit** a změňte hodnotu ve sloupci **rozpočet** . (Nezapomeňte, že můžete upravovat jenom záznamy, které jste pro tento kurz vytvořili, protože existující záznamy `School` databáze obsahují neplatná data. Záznam pro ekonomické oddělení je bezpečný pro experimentování s.)

[![Image18](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image16.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image15.png)

Otevřete nové okno prohlížeče a znovu spusťte stránku (zkopírujte adresu URL z pole adresa prvního okna prohlížeče do druhého okna prohlížeče).

[![Image17](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image18.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image17.png)

Klikněte na **Upravit** ve stejném řádku, který jste upravovali dříve, a změňte hodnotu **rozpočtu** na jinou.

[![Image19](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image20.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image19.png)

V druhém okně prohlížeče klikněte na **aktualizovat**. Částka **rozpočtu** se úspěšně změnila na tuto novou hodnotu.

[![Image20](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image22.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image21.png)

V prvním okně prohlížeče klikněte na **aktualizovat**. Aktualizace se nezdařila. Částka **rozpočtu** se znovu zobrazí pomocí hodnoty, kterou jste nastavili v druhém okně prohlížeče, a zobrazí se chybová zpráva.

[![Image21](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image24.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image23.png)

## <a name="handling-optimistic-concurrency-using-a-tracking-property"></a>Zpracování optimistického řízení souběžnosti pomocí vlastnosti sledování

Chcete-li zpracovat optimistickou souběžnost pro entitu, která má vlastnost sledování, proveďte následující úlohy:

- Přidejte uložené procedury do datového modelu pro správu `OfficeAssignment` entit. (Vlastnosti sledování a uložené procedury nemusejí být používány dohromady. jsou zde pouze seskupeny na ilustraci.)
- Přidejte metody CRUD do DAL a knihoven BLL pro `OfficeAssignment` entit, včetně kódu pro zpracování optimistických výjimek souběžnosti v DAL.
- Vytvoří webovou stránku přiřazení Office.
- Otestujte optimistickou souběžnost na nové webové stránce.

### <a name="adding-officeassignment-stored-procedures-to-the-data-model"></a>Přidání uložených procedur OfficeAssignment do datového modelu

Otevřete soubor *SchoolModel. edmx* v Návrháři modelů, klikněte pravým tlačítkem myši na návrhovou plochu a klikněte na příkaz **aktualizovat model z databáze**. Na kartě **Přidat** dialogového okna **zvolit objekty databáze** rozbalte **uložené procedury** a vyberte tři `OfficeAssignment` uložené procedury (viz následující snímek obrazovky) a pak klikněte na **Dokončit**. (Tyto uložené procedury byly již v databázi v době, kdy jste je stáhli nebo vytvořili pomocí skriptu.)

[![Image02](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image26.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image25.png)

Klikněte pravým tlačítkem na entitu `OfficeAssignment` a vyberte **mapování uložených procedur**.

[![Image03](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image28.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image27.png)

Nastavte funkce **INSERT**, **Update**a **Delete** tak, aby používaly odpovídající uložené procedury. Pro parametr `OrigTimestamp` funkce `Update` nastavte **vlastnost** na hodnotu `Timestamp` a vyberte možnost **použít původní hodnotu** .

[![Image04](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image30.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image29.png)

Když Entity Framework volá uloženou proceduru `UpdateOfficeAssignment`, předáte původní hodnotu sloupce `Timestamp` v parametru `OrigTimestamp`. Uložená procedura používá tento parametr v klauzuli `Where`:

[!code-sql[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample8.sql)]

Uložená procedura také vybere novou hodnotu sloupce `Timestamp` po aktualizaci tak, aby Entity Framework mohl ponechat entitu `OfficeAssignment`, která je v paměti, synchronizována s odpovídajícím řádkem databáze.

(Všimněte si, že úložná procedura pro odstranění přiřazení kanceláře neobsahuje parametr `OrigTimestamp`. Z tohoto důvodu Entity Framework nemůže před odstraněním ověřit, zda je entita beze změny.)

Uložte a zavřete datový model.

### <a name="adding-officeassignment-methods-to-the-dal"></a>Přidání metod OfficeAssignment do DAL

Otevřete *ISchoolRepository.cs* a přidejte následující metody CRUD pro sadu entit `OfficeAssignment`:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample9.cs)]

Do *SchoolRepository.cs*přidejte následující nové metody. V metodě `UpdateOfficeAssignment` zavoláte místní metodu `SaveChanges` namísto `context.SaveChanges`.

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample10.cs)]

V projektu testu otevřete *MockSchoolRepository.cs* a přidejte do něj následující kolekce `OfficeAssignment` a metody CRUD. (Maketa úložiště musí implementovat rozhraní úložiště, jinak se řešení nezkompiluje.)

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample11.cs)]

### <a name="adding-officeassignment-methods-to-the-bll"></a>Přidání metod OfficeAssignment do knihoven BLL

V hlavním projektu otevřete *SchoolBL.cs* a přidejte následující metody CRUD pro `OfficeAssignment` sadu entit:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample12.cs)]

## <a name="creating-an-officeassignments-web-page"></a>Vytvoření webové stránky OfficeAssignments

Vytvořte novou webovou stránku, která používá hlavní stránku *Web. Master* a pojmenujte ji *OfficeAssignments. aspx*. Přidejte následující značku do ovládacího prvku `Content` s názvem `Content2`:

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample13.aspx)]

Všimněte si, že v atributu `DataKeyNames` značka určuje vlastnost `Timestamp` a také klíč záznamu (`InstructorID`). Určení vlastností v atributu `DataKeyNames` způsobí, že ovládací prvek je uloží do stavu ovládacího prvku (což je podobně jako stav zobrazení), takže původní hodnoty jsou k dispozici během zpracování zpětného volání.

Pokud jste hodnotu `Timestamp` neuložili, Entity Framework by ji neobsahovala pro klauzuli `Where` příkazu SQL `Update`. V důsledku toho by se nenašly žádné aktualizace. V důsledku toho Entity Framework vyvolat výjimku optimistické souběžnosti pokaždé, když se aktualizuje entita `OfficeAssignment`.

Otevřete *OfficeAssignments.aspx.cs* a přidejte následující příkaz `using` pro vrstvu přístupu k datům:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample14.cs)]

Přidejte následující metodu `Page_Init`, která umožňuje funkci dynamického data. Přidejte také následující obslužnou rutinu pro událost `Updated` ovládacího prvku `ObjectDataSource`, aby bylo možné zjistit chyby souběžnosti:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample15.cs)]

### <a name="testing-optimistic-concurrency-in-the-officeassignments-page"></a>Testování optimistické souběžnosti na stránce OfficeAssignments

Spusťte stránku *OfficeAssignments. aspx* .

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image32.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image31.png)

V řádku klikněte na **Upravit** a změňte hodnotu ve sloupci **umístění** .

[![Image11](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image34.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image33.png)

Otevřete nové okno prohlížeče a znovu spusťte stránku (zkopírujte adresu URL z prvního okna prohlížeče do druhého okna prohlížeče).

[![Image10](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image36.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image35.png)

Klikněte na **Upravit** ve stejném řádku, který jste upravovali dříve, a změňte hodnotu **umístění** na jinou.

[![Image12](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image38.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image37.png)

V druhém okně prohlížeče klikněte na **aktualizovat**.

[![Image13](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image40.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image39.png)

Přepněte do prvního okna prohlížeče a klikněte na **aktualizovat**.

[![Image15](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image42.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image41.png)

Zobrazí se chybová zpráva a hodnota **umístění** byla aktualizována, aby se zobrazila hodnota, na kterou jste změnili v druhém okně prohlížeče.

## <a name="handling-concurrency-with-the-entitydatasource-control"></a>Zpracování souběžnosti s ovládacím prvkem EntityDataSource

Ovládací prvek `EntityDataSource` obsahuje vestavěnou logiku, která rozpoznává nastavení souběžnosti v datovém modelu a zpracovává odpovídající operace aktualizace a odstranění. Stejně jako u všech výjimek je však nutné zpracovat výjimky `OptimisticConcurrencyException` sami, aby bylo možné zadat uživatelsky přívětivou chybovou zprávu.

Dále nakonfigurujete stránku *kurzy. aspx* (která používá ovládací prvek `EntityDataSource`) k povolení operací aktualizace a odstranění a k zobrazení chybové zprávy, pokud dojde ke konfliktu souběžnosti. Entita `Course` nemá sloupec sledování souběžnosti, takže budete používat stejnou metodu, kterou jste provedli s entitou `Department`: Sledujte hodnoty všech neklíčových vlastností.

Otevřete soubor *SchoolModel. edmx* . Pro neklíčové vlastnosti entity `Course` (`Title`, `Credits`a `DepartmentID`) nastavte vlastnost **režim souběžnosti** na `Fixed`. Pak datový model uložte a zavřete.

Otevřete stránku *kurzy. aspx* a proveďte následující změny:

- V ovládacím prvku `CoursesEntityDataSource` přidejte atributy `EnableUpdate="true"` a `EnableDelete="true"`. Otevírací značka pro tento ovládací prvek teď vypadá podobně jako v následujícím příkladu:

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample16.aspx)]
- V ovládacím prvku `CoursesGridView` změňte hodnotu atributu `DataKeyNames` na `"CourseID,Title,Credits,DepartmentID"`. Pak přidejte `CommandField` element do prvku `Columns`, který zobrazuje tlačítka **Upravit** a **Odstranit** (`<asp:CommandField ShowEditButton="True" ShowDeleteButton="True" />`). Ovládací prvek `GridView` se teď podobá následujícímu příkladu:

    [!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample17.aspx)]

Spusťte stránku a na stránce oddělení vytvořte situaci, ve které došlo ke konfliktu. Spusťte stránku ve dvou oknech prohlížeče, v každém okně klikněte na **Upravit** na stejném řádku a udělejte v každém z nich jinou změnu. V jednom okně klikněte na **aktualizovat** a potom v druhém okně klikněte na **aktualizovat** . Když kliknete na **aktualizovat** podruhé, zobrazí se chybová stránka, která bude mít za následek neošetřenou výjimku souběžnosti.

[![Image22](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image44.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image43.png)

Tato chyba se zpracovává způsobem velmi podobným způsobu, jakým jste ji zpracovali pro ovládací prvek `ObjectDataSource`. Otevřete stránku *kurzy. aspx* a v ovládacím prvku `CoursesEntityDataSource` určete obslužné rutiny pro události `Deleted` a `Updated`. Otevírací značka ovládacího prvku teď vypadá podobně jako v následujícím příkladu:

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample18.aspx)]

Před ovládacím prvkem `CoursesGridView` přidejte následující ovládací prvek `ValidationSummary`:

[!code-aspx[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample19.aspx)]

V *courses.aspx.cs*přidejte příkaz `using` pro `System.Data` oboru názvů, přidejte metodu, která kontroluje výjimky souběžnosti, a přidejte obslužné rutiny pro `Updated` a `Deleted` obslužné rutiny ovládacího prvku `EntityDataSource`. Kód bude vypadat jako následující:

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample20.cs)]

[!code-csharp[Main](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/samples/sample21.cs)]

Jediný rozdíl mezi tímto kódem a to, co jste použili pro ovládací prvek `ObjectDataSource` je, že v tomto případě je výjimka souběžnosti ve vlastnosti `Exception` objektu argumenty události, nikoli v této vlastnosti `InnerException` této výjimky.

Spusťte stránku a vytvořte konflikt souběžnosti znovu. Tentokrát se zobrazí chybová zpráva:

[![Image23](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image46.png)](handling-concurrency-with-the-entity-framework-in-an-asp-net-web-application/_static/image45.png)

Tím se dokončí Úvod ke zpracování konfliktů souběžnosti. V dalším kurzu se dozvíte, jak zvýšit výkon webové aplikace, která používá Entity Framework.

> [!div class="step-by-step"]
> [Předchozí](using-the-entity-framework-and-the-objectdatasource-control-part-3-sorting-and-filtering.md)
> [Další](maximizing-performance-with-the-entity-framework-in-an-asp-net-web-application.md)

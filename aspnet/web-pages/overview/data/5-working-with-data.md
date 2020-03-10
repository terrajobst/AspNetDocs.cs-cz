---
uid: web-pages/overview/data/5-working-with-data
title: Úvod k práci s databází na webech ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Tato kapitola popisuje, jak získat přístup k datům z databáze a jak ji zobrazit pomocí webových stránek ASP.NET.
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 673d502f-2c16-4a6f-bb63-dbfd9a77ef47
msc.legacyurl: /web-pages/overview/data/5-working-with-data
msc.type: authoredcontent
ms.openlocfilehash: 45e988d037465e59ad352bb9444af2c69fd3cd70
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586532"
---
# <a name="introduction-to-working-with-a-database-in-aspnet-web-pages-razor-sites"></a>Úvod k práci s databází na webech ASP.NET Web Pages (Razor)

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek popisuje, jak pomocí nástrojů Microsoft WebMatrix vytvořit databázi na webu ASP.NET Web Pages (Razor) a jak vytvářet stránky, které vám umožní zobrazovat, přidávat, upravovat a odstraňovat data.
> 
> **Co se naučíte:** 
> 
> - Jak vytvořit databázi.
> - Jak se připojit k databázi.
> - Jak zobrazit data na webové stránce.
> - Jak vkládat, aktualizovat a odstraňovat záznamy databáze.
> 
> Tyto funkce jsou představené v článku:
> 
> - Práce s databází edice Microsoft SQL Server Compact.
> - Práce s dotazy SQL.
> - Třída `Database`.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 2
> - WebMatrix 2
>   
> 
> V tomto kurzu se používá také WebMatrix 3. Můžete použít webové stránky ASP.NET 3 a Visual Studio 2013 (nebo Visual Studio Express 2013 pro web); uživatelské rozhraní se ale bude lišit.

## <a name="introduction-to-databases"></a>Seznámení s databázemi

Představte si typický adresář. Pro každou položku v adresáři (tj. pro jednotlivé osoby) máte několik informací, jako je křestní jméno, příjmení, adresa, e-mailová adresa a telefonní číslo.

Typický způsob, jak obrázková data vypadat jako tabulka s řádky a sloupci. V rámci databázových podmínek se každý řádek často označuje jako záznam. Každý sloupec (někdy označovaný jako pole) obsahuje hodnotu pro každý typ dat: jméno, příjmení a tak dále.

| **ID** | **FirstName** | **Polím** | **Adresáře** | **E-mail** | **Hovor** |
| --- | --- | --- | --- | --- | --- |
| 1 | Jan | Abrus | 210 100th St SE Orcas WA 98031 | jim@contoso.com | 555 0100 |
| 2 | Terry | Adams | 1234 Main St. Praha WA – 99011 | terry@cohowinery.com | 555 0101 |

U většiny tabulek databáze musí mít tabulka sloupec, který obsahuje jedinečný identifikátor, jako je číslo zákazníka, číslo účtu atd. To se označuje jako *primární klíč*tabulky a používá se k identifikaci každého řádku v tabulce. V tomto příkladu je sloupec ID primárním klíčem pro adresář.

Díky tomuto základnímu porozumění databázím jste připraveni zjistit, jak vytvořit jednoduchou databázi a provádět operace, jako je přidání, úpravy a odstranění dat.

> [!TIP] 
> 
> **Relační databáze**
> 
> Data můžete ukládat mnoha různými způsoby, včetně textových souborů a tabulek. U většiny podnikových použití se ale data ukládají do relační databáze.
> 
> Tento článek se nevejde do databází velmi hluboko. Může se ale stát, že si ho budete potřebovat trochu porozumět. V relační databázi jsou informace logicky rozděleny do samostatných tabulek. Například databáze pro školu může obsahovat samostatné tabulky pro studenty a pro nabídky tříd. Databázový software (například SQL Server) podporuje výkonné příkazy, které umožňují dynamicky navazovat relace mezi tabulkami. Relační databázi můžete například použít k vytvoření logického vztahu mezi studenty a třídami, aby bylo možné vytvořit plán. Ukládání dat v samostatných tabulkách zkracuje složitost struktury tabulky a snižuje nutnost uchovávat redundantní data v tabulkách.

## <a name="creating-a-database"></a>Vytvoření databáze

Tento postup popisuje, jak vytvořit databázi s názvem SmallBakery pomocí nástroje pro návrh databáze SQL Server Compact, který je součástí WebMatrixu. I když můžete vytvořit databázi pomocí kódu, je obvyklejší vytvořit databázi a tabulky databáze pomocí nástroje pro návrh, jako je WebMatrix.

1. Spusťte WebMatrix a na stránce rychlé zprovoznění klikněte na možnost **lokalita ze šablony**.
2. Vyberte možnost **prázdný web**a do pole **název webu** zadejte "SmallBakery" a klikněte na tlačítko **OK**. Web se vytvoří a zobrazí ve WebMatrixu.
3. V levém podokně klikněte na pracovní prostor **databáze** .
4. Na pásu karet klikněte na možnost **Nová databáze**. Vytvoří se prázdná databáze se stejným názvem, jako má vaše lokalita.
5. V levém podokně rozbalte uzel **SmallBakery. sdf** a klikněte na možnost **tabulky**.
6. Na pásu karet klikněte na možnost **Nová tabulka**. WebMatrix otevře Návrháře tabulky.

    ![obrazu](5-working-with-data/_static/image1.jpg)
7. Klikněte do sloupce **název** a zadejte &quot;ID&quot;.
8. Ve sloupci **datový typ** vyberte **int**.
9. Nastavit **je primární klíč?** a **identifikovat?** možnosti **Ano**.

    Jak název navrhuje, **má primární klíč** databázi, která bude představovat primární klíč tabulky. **Označuje identitu** databázi, aby automaticky vytvořila identifikační číslo pro každý nový záznam a přiřadila mu další pořadové číslo (od 1).
10. Klikněte na další řádek. Editor spustí novou definici sloupce.
11. Jako hodnotu název zadejte &quot;název&quot;.
12. V poli **datový typ**vyberte &quot;nvarchar&quot; a nastavte délku na 50. *Var* část `nvarchar` oznamuje databázi, že data pro tento sloupec budou řetězcem, jehož velikost se může lišit od záznamu k záznamu. (Předpona *n* představuje *národní*, což znamená, že pole může obsahovat znaková data, která představují jakýkoli abecední &#8212; nebo systém zápisu, který je, že pole obsahuje data ve formátu Unicode.)
13. Nastavte možnost **povoluje hodnoty null** na **ne**. Tím se vyhodnotí, že sloupec *název* nebude ponechán prázdný.
14. Pomocí stejného postupu vytvořte sloupec s názvem *Description*. Nastavte **datový typ** na "nvarchar" a 50 na délku a nastavte hodnotu **povoleno null** na false.
15. Vytvořte sloupec s názvem *Price*. Nastavte **datový typ na peníze** a nastavte možnost **povoluje hodnoty null** na hodnotu NEPRAVDA.
16. Do pole v horní části pojmenujte tabulku &quot;&quot;produktu.

    Až budete hotovi, definice bude vypadat takto:

    ![obrazu](5-working-with-data/_static/image2.png)
17. Tabulku uložte stisknutím kombinace kláves CTRL + S.

## <a name="adding-data-to-the-database"></a>Přidání dat do databáze

Teď můžete do své databáze přidat ukázková data, která budete používat později v článku.

1. V levém podokně rozbalte uzel **SmallBakery. sdf** a klikněte na možnost **tabulky**.
2. Klikněte pravým tlačítkem na tabulku produktů a pak klikněte na **data**.
3. V podokně úprav zadejte následující záznamy:

    | **Název** | **Popis** | **Cenové** |
    | --- | --- | --- |
    | Chléb | Vloženými čerstvě každý den. | 2.99 |
    | Strawberry Shortcake | Provedená organická Jahoda z naší zahrady. | 9.99 |
    | Výseč Apple | Druhý jenom k výsečovému diagramu vašeho MOM. | 12.99 |
    | Výsečový Pecan | Pokud jste jako pecans, je to pro vás. | 10.99 |
    | Výseč citronu | S nejlepšími citrony, které jsou na světě. | 11.99 |
    | Dortíky | Vaše děti a dítě se vám budou líbit. | 7.99 |

    Nezapomeňte, že pro sloupec *ID* nemusíte nic zadávat. Když jste vytvořili sloupec *ID* , nastavíte jeho vlastnost **identity** na hodnotu true, což způsobí, že se automaticky vyplní.

    Až skončíte s zadáváním dat, Návrhář tabulky bude vypadat takto:

    ![obrazu](5-working-with-data/_static/image3.jpg)
4. Zavřete kartu obsahující data databáze.

## <a name="displaying-data-from-a-database"></a>Zobrazení dat z databáze

Jakmile získáte databázi s daty, můžete zobrazit data na webové stránce ASP.NET. Pokud chcete vybrat řádky tabulky, které se mají zobrazit, použijte příkaz SQL, který je příkaz, který předáte do databáze.

1. V levém podokně klikněte na pracovní prostor **soubory** .
2. V kořenovém adresáři webu vytvořte novou stránku CSHTML s názvem *ListProducts. cshtml*.
3. Existující značku nahraďte následujícím kódem:

    [!code-cshtml[Main](5-working-with-data/samples/sample1.cshtml)]

    V prvním bloku kódu otevřete soubor *SmallBakery. sdf* (databáze), který jste vytvořili dříve. Metoda `Database.Open` předpokládá, že soubor *. sdf* je ve složce *\_data aplikace* vašeho webu. (Všimněte si, že ve skutečnosti nemusíte zadávat příponu &#8212; *. sdf* , pokud tak učiníte, nebude metoda `Open` fungovat.)

    > [!NOTE]
    > Složka *App\_data* je speciální složkou v ASP.NET, která se používá k ukládání datových souborů. Další informace najdete v části [připojení k databázi](#SB_ConnectingToADatabase) dále v tomto článku.

    Pak vytvoříte žádost o dotazování databáze pomocí následujícího příkazu SQL `Select`:

    [!code-sql[Main](5-working-with-data/samples/sample2.sql)]

    V příkazu `Product` identifikuje tabulku pro dotaz. Znak `*` určuje, že dotaz by měl vracet všechny sloupce z tabulky. (Můžete také vypsat sloupce jednotlivě a oddělit je čárkami, pokud jste chtěli zobrazit pouze některé sloupce.) Klauzule `Order By` určuje, jak mají být data v tomto &#8212; případě seřazena podle sloupce *název* . To znamená, že data jsou seřazená podle abecedy na základě hodnoty sloupce *název* pro každý řádek.

    V těle stránky kód vytvoří tabulku HTML, která bude použita k zobrazení dat. Uvnitř prvku `<tbody>` použijete smyčku `foreach` k samostatnému získání každého řádku dat, který je vrácen dotazem. Pro každý řádek dat vytvoříte řádek tabulky HTML (`<tr>` element). Pak vytvoříte buňky tabulky HTML (`<td>` elementy) pro každý sloupec. Pokaždé, když projdete smyčku, je další dostupný řádek z databáze v proměnné `row` (nastavíte tuto hodnotu v příkazu `foreach`). Chcete-li získat z řádku jednotlivý sloupec, můžete použít `row.Name` nebo `row.Description` nebo jakýkoli název sloupce, který chcete.
4. Spusťte stránku v prohlížeči. (Před spuštěním se ujistěte, že je stránka vybraná v pracovním prostoru **soubory** .) Na stránce se zobrazí seznam podobný následujícímu:

    ![obrazu](5-working-with-data/_static/image4.jpg)

> [!TIP] 
> 
> **Jazyk SQL (Structured Query Language) (SQL)**
> 
> SQL je jazyk, který se používá ve většině relačních databází pro správu dat v databázi. Obsahuje příkazy, které umožňují načíst data a aktualizovat je a umožňují vytvářet, upravovat a spravovat databázové tabulky. SQL se liší od programovacího jazyka (jako je ten, který používáte ve WebMatrixu), protože v jazyce SQL je to, že databázi říkáte, co potřebujete, a je to úloha databáze, která ukazuje, jak získat data nebo provést úlohu. Tady jsou příklady některých příkazů SQL a jejich možnosti:
> 
> `SELECT Id, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> Načte sloupce *ID*, *název*a *ceny* ze záznamů v tabulce *produktů* , pokud je hodnota *Price* větší než 10, a výsledky vrátí v abecedním pořadí podle hodnot sloupce *název* . Tento příkaz vrátí sadu výsledků dotazu obsahující záznamy, které splňují kritéria, nebo prázdnou sadu, pokud žádné záznamy neodpovídají.
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ("Croissant", "A flaky delight", 1.99)`
> 
> Tím se do tabulky *produkt* vloží nový záznam, ve sloupci *název* se &quot;croissant&quot;, sloupec *Description* , který &quot;&quot;světla, a cenu na 1,99.
> 
> `DELETE FROM Product WHERE ExpirationDate < "01/01/2008"`
> 
> Tento příkaz odstraní záznamy v tabulce *produktů* , jejichž sloupec Datum vypršení platnosti je starší než 1. ledna 2008. (To předpokládá, že tabulka *produktu* má takový sloupec kurzu.) Datum je zadáno ve formátu MM/DD/RRRR, ale mělo by být zadáno ve formátu používaném pro vaše národní prostředí.
> 
> Příkazy `Insert Into` a `Delete` nevrací sady výsledků dotazu. Místo toho vrátí číslo, které oznamuje, kolik záznamů bylo ovlivněno příkazem.
> 
> Pro některé z těchto operací (jako je vkládání a odstraňování záznamů) musí mít proces, který vyžaduje operaci, příslušná oprávnění v databázi. To je důvod, proč v produkčních databázích, které často potřebujete při připojování k databázi zadávat uživatelské jméno a heslo.
> 
> Existují spousty příkazů SQL, ale všechny mají stejný vzor jako to. Pomocí příkazů SQL můžete vytvořit tabulky databáze, spočítat počet záznamů v tabulce, vypočítat ceny a provádět spoustu dalších operací.

## <a name="inserting-data-in-a-database"></a>Vkládání dat do databáze

V této části se dozvíte, jak vytvořit stránku, která uživatelům umožňuje přidat nový produkt do tabulky databáze *produktu* . Po vložení nového záznamu produktu se na stránce zobrazí aktualizovaná tabulka pomocí stránky *ListProducts. cshtml* , kterou jste vytvořili v předchozí části.

Stránka obsahuje ověření, aby se zajistilo, že data, která uživatel zadá, jsou pro databázi platná. Například kód na stránce zajistí, že byla zadána hodnota pro všechny požadované sloupce.

1. Na webu vytvořte nový soubor CSHTML s názvem *InsertProducts. cshtml*.
2. Existující značku nahraďte následujícím kódem:

    [!code-cshtml[Main](5-working-with-data/samples/sample3.cshtml)]

    Tělo stránky obsahuje formulář HTML se třemi textovými poli, která umožní uživatelům zadat název, popis a cenu. Když uživatel klikne na tlačítko **Vložit** , otevře se kód v horní části stránky s připojením k databázi *SmallBakery. sdf* . Potom získáte hodnoty, které uživatel odeslal pomocí objektu `Request` a přiřadit tyto hodnoty lokálním proměnným.

    Chcete-li ověřit, zda uživatel zadal hodnotu pro každý požadovaný sloupec, zaregistrujte každý `<input>` prvek, který chcete ověřit:

    [!code-csharp[Main](5-working-with-data/samples/sample4.cs)]

    Pomocník `Validation` kontroluje, zda existuje hodnota v každém z polí, která jste zaregistrovali. Můžete otestovat, jestli všechna pole prošla ověřením, a to tak, že zkontrolujete `Validation.IsValid()`, které obvykle provedete předtím, než budete zpracovávat informace, které dostanete od uživatele:

    [!code-csharp[Main](5-working-with-data/samples/sample5.cs)]

    (Operátor `&&` znamená a – tento test je, *Pokud se jedná o odeslání formuláře a všechna pole prošla ověřením*.)

    Pokud jsou všechny sloupce ověřené (žádné byly prázdné), můžete pokračovat a vytvořit příkaz SQL, který vloží data a pak ji spustit, jak je uvedeno dále:

    [!code-csharp[Main](5-working-with-data/samples/sample6.cs)]

    Pro hodnoty, které mají být vloženy, zahrnete zástupné symboly parametrů (`@0`, `@1`, `@2`).

    > [!NOTE]
    > Z důvodu zabezpečení je vždy nutné předat hodnoty příkazu SQL pomocí parametrů, jak vidíte v předchozím příkladu. To vám dává možnost ověřit data uživatele a pomáhá chránit před pokusy o odeslání škodlivých příkazů do vaší databáze (někdy označované jako útoky prostřednictvím injektáže SQL).

    Chcete-li spustit dotaz, použijte tento příkaz a předejte mu proměnné obsahující hodnoty, které mají být nahrazeny zástupnými symboly:

    [!code-csharp[Main](5-working-with-data/samples/sample7.cs)]

    Po provedení příkazu `Insert Into` odešlete uživateli stránku se seznamem produktů, které používají tento řádek:

    [!code-javascript[Main](5-working-with-data/samples/sample8.js)]

    Pokud ověření nebylo úspěšné, přeskočíte vložení. Místo toho máte na stránce pomocníka, kde můžete zobrazit nahromaděné chybové zprávy (pokud existují):

    [!code-cshtml[Main](5-working-with-data/samples/sample9.cshtml)]

    Všimněte si, že blok stylu v kódu obsahuje definici třídy CSS s názvem `.validation-summary-errors`. Toto je název třídy šablony stylů CSS, která se používá ve výchozím nastavení pro element `<div>`, který obsahuje chyby ověřování. V tomto případě Třída CSS určuje, že chyby souhrnu ověření jsou zobrazeny červeně a tučně, ale můžete definovat třídu `.validation-summary-errors` pro zobrazení libovolného formátování, které chcete.

### <a name="testing-the-insert-page"></a>Testování stránky pro vložení

1. Zobrazit stránku v prohlížeči. Na stránce se zobrazí formulář podobný tomu, který je zobrazený na následujícím obrázku.

    ![obrazu](5-working-with-data/_static/image5.jpg)
2. Zadejte hodnoty pro všechny sloupce, ale ujistěte se, že sloupec *Price* ponecháte prázdný.
3. Klikněte na tlačítko **Vložit**. Na stránce se zobrazí chybová zpráva, jak je znázorněno na následujícím obrázku. (Žádný nový záznam není vytvořen.)

    ![obrazu](5-working-with-data/_static/image6.jpg)
4. Vyplňte formulář úplně a pak klikněte na **Vložit**. Tentokrát se zobrazí stránka *ListProducts. cshtml* a zobrazí se nový záznam.

## <a name="updating-data-in-a-database"></a>Aktualizace dat v databázi

Po zadání dat do tabulky může být nutné ji aktualizovat. Tento postup vám ukáže, jak vytvořit dvě stránky, které jsou podobné těm, které jste vytvořili pro předchozí vložení dat. Na první stránce se zobrazí produkty, které uživatelům umožní vybrat jednu ke změně. Druhá stránka umožňuje uživatelům provádět úpravy a ukládat je.

> [!NOTE] 
> 
> **Důležité** informace Na produkčním webu je obvykle možné omezit, kdo může provádět změny dat. Informace o tom, jak nastavit členství a způsoby, jak autorizovat uživatele k provádění úloh na webu, najdete v tématu věnovaném [Přidání zabezpečení a členství na web webových stránek ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202904).

1. Na webu vytvořte nový soubor CSHTML s názvem *EditProducts. cshtml*.
2. Nahraďte existující kód v souboru následujícím kódem:

    [!code-cshtml[Main](5-working-with-data/samples/sample10.cshtml)]

    Jediným rozdílem mezi touto stránkou a stránkou *ListProducts. cshtml* z předchozích verzí je, že tabulka HTML na této stránce obsahuje sloupec navíc, který zobrazuje odkaz pro **Úpravy** . Po kliknutí na tento odkaz přejdete na stránku *UpdateProducts. cshtml* (kterou vytvoříte dále), kde můžete vybraný záznam upravit.

    Podívejte se na kód, který vytvoří odkaz pro **Úpravy** :

    [!code-cshtml[Main](5-working-with-data/samples/sample11.cshtml)]

    Tím se vytvoří element HTML `<a>`, jehož atribut `href` je nastaven dynamicky. Atribut `href` Určuje stránku, která se zobrazí, když uživatel klikne na odkaz. Také předává `Id` hodnotu aktuálního řádku na odkaz. Po spuštění stránky může zdroj stránky obsahovat odkazy, jako jsou tyto:

    [!code-html[Main](5-working-with-data/samples/sample12.html)]

    Všimněte si, že atribut `href` je nastaven na hodnotu `UpdateProducts/n`, kde *n* je číslo produktu. Když uživatel klikne na jeden z těchto odkazů, Výsledná adresa URL bude vypadat přibližně takto:

    `http://localhost:18816/UpdateProducts/6`

    Jinými slovy, číslo produktu, které se má upravit, se předává v adrese URL.
3. Zobrazit stránku v prohlížeči. Stránka zobrazuje data v následujícím formátu:

    ![obrazu](5-working-with-data/_static/image7.jpg)

    V dalším kroku vytvoříte stránku, která umožní uživatelům data skutečně aktualizovat. Stránka aktualizace obsahuje ověření pro ověření dat, která uživatel zadal. Například kód na stránce zajistí, že byla zadána hodnota pro všechny požadované sloupce.
4. Na webu vytvořte nový soubor CSHTML s názvem *UpdateProducts. cshtml*.
5. Nahraďte existující kód v souboru následujícím kódem.

    [!code-cshtml[Main](5-working-with-data/samples/sample13.cshtml)]

    Tělo stránky obsahuje formulář HTML, ve kterém je zobrazený produkt a kde ho můžou uživatelé upravovat. Chcete-li získat produkt, který chcete zobrazit, použijte tento příkaz SQL:

    [!code-sql[Main](5-working-with-data/samples/sample14.sql)]

    Tím se vybere produkt, jehož ID odpovídá hodnotě předané v parametru `@0`. (Vzhledem k tomu, že *ID* je primární klíč, a proto musí být jedinečný, může být vždy vybrán pouze jeden záznam produktu.) Chcete-li získat hodnotu ID, která bude předána tomuto příkazu `Select`, můžete načíst hodnotu, která je předána stránce jako součást adresy URL, pomocí následující syntaxe:

    [!code-csharp[Main](5-working-with-data/samples/sample15.cs)]

    Chcete-li skutečně načíst záznam produktu, použijte metodu `QuerySingle`, která vrátí pouze jeden záznam:

    [!code-csharp[Main](5-working-with-data/samples/sample16.cs)]

    Jeden řádek se vrátí do proměnné `row`. Data můžete získat z každého sloupce a přiřadit je k místním proměnným, jako je:

    [!code-csharp[Main](5-working-with-data/samples/sample17.cs)]

    Ve značkách pro formulář se tyto hodnoty zobrazují automaticky v jednotlivých textových polích pomocí vloženého kódu, jako je následující:

    [!code-html[Main](5-working-with-data/samples/sample18.html)]

    Tato část kódu zobrazuje záznam produktu, který se má aktualizovat. Po zobrazení záznamu může uživatel upravovat jednotlivé sloupce.

    Když uživatel formulář odešle kliknutím na tlačítko **aktualizovat** , spustí se kód v bloku `if(IsPost)`. Tím se získá hodnoty uživatele z objektu `Request`, uloží hodnoty do proměnných a ověří, že každý sloupec byl vyplněn. Pokud ověření projde, kód vytvoří následující příkaz SQL Update:

    [!code-sql[Main](5-working-with-data/samples/sample19.sql)]

    V příkazu SQL `Update` zadáte každý sloupec, který se má aktualizovat, a hodnotu, na kterou se má nastavit. V tomto kódu jsou hodnoty zadány pomocí zástupných symbolů parametrů `@0`, `@1`, `@2`a tak dále. (Jak bylo uvedeno dříve, z důvodu zabezpečení byste měli vždy předat hodnoty příkazu SQL pomocí parametrů.)

    Při volání metody `db.Execute` předáte proměnné, které obsahují hodnoty v pořadí, které odpovídá parametrům v příkazu SQL:

    [!code-csharp[Main](5-working-with-data/samples/sample20.cs)]

    Po provedení příkazu `Update` zavoláte následující metodu, aby se uživatel přesměroval zpátky na stránku pro úpravy:

    [!code-cshtml[Main](5-working-with-data/samples/sample21.cshtml)]

    Efekt je, že uživatel uvidí aktualizovaný výpis dat v databázi a může upravit jiný produkt.
6. Uložte stránku.
7. Spusťte stránku *EditProducts. cshtml* (ne stránku aktualizace) a pak klikněte na **Upravit** a vyberte produkt, který chcete upravit. Zobrazí se stránka *UpdateProducts. cshtml* , která zobrazuje vybraný záznam.

    ![obrazu](5-working-with-data/_static/image8.jpg)
8. Proveďte změnu a klikněte na **aktualizovat**. Seznam produktů se znovu zobrazuje s aktualizovanými daty.

## <a name="deleting-data-in-a-database"></a>Odstraňování dat v databázi

V této části se dozvíte, jak umožnit uživatelům odstranit produkt z tabulky databáze *produktu* . Příklad se skládá ze dvou stránek. Na první stránce Uživatelé vyberou záznam, který chcete odstranit. Záznam, který se má odstranit, se pak zobrazí na druhé stránce, která jim umožní potvrdit, že chce záznam odstranit.

> [!NOTE] 
> 
> **Důležité** informace Na produkčním webu je obvykle možné omezit, kdo může provádět změny dat. Informace o tom, jak nastavit členství a způsoby, jak autorizovat uživatele k provádění úloh na webu, najdete v tématu věnovaném [Přidání zabezpečení a členství na web webových stránek ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202904).

1. Na webu vytvořte nový soubor CSHTML s názvem *ListProductsForDelete. cshtml*.
2. Existující značku nahraďte následujícím kódem:

    [!code-cshtml[Main](5-working-with-data/samples/sample22.cshtml)]

    Tato stránka se podobá stránce *EditProducts. cshtml* ze starší verze. Namísto zobrazení odkazu pro **Úpravy** každého produktu se ale zobrazí odkaz **Odstranit** . Odkaz **Delete** je vytvořen pomocí následujícího vloženého kódu v kódu:

    [!code-cshtml[Main](5-working-with-data/samples/sample23.cshtml)]

    Tím se vytvoří adresa URL, která vypadá takto: když uživatel klikne na odkaz:

    `http://<server>/DeleteProduct/4`

    Adresa URL volá stránku s názvem *DeleteProduct. cshtml* (kterou vytvoříte dále) a předá jí ID produktu, který chcete odstranit (zde 4).
3. Uložte soubor, ale nechte ho otevřený.
4. Vytvořte další soubor CHTML s názvem *DeleteProduct. cshtml*. Existující obsah nahraďte následujícím:

    [!code-cshtml[Main](5-working-with-data/samples/sample24.cshtml)]

    Tuto stránku volá *ListProductsForDelete. cshtml* a umožňuje uživatelům potvrdit, že chtějí odstranit produkt. Pokud chcete vypsat produkt, který se má odstranit, získáte ID produktu, který se má odstranit z adresy URL, a to pomocí následujícího kódu:

    [!code-csharp[Main](5-working-with-data/samples/sample25.cs)]

    Stránka pak vyzve uživatele, aby kliknutím na tlačítko skutečně odstranil záznam. Toto je důležité bezpečnostní opatření: když na webu provedete citlivé operace, jako je aktualizace nebo odstranění dat, měly by se tyto operace vždy provádět pomocí operace POST, nikoli operace GET. Pokud je vaše lokalita nastavená tak, aby operace odstranění mohla probíhat pomocí operace GET, může kdokoli předat adresu URL, jako je `http://<server>/DeleteProduct/4`, a z databáze odstranit cokoli, co chtějí. Přidáním potvrzení a kódováním stránky, aby bylo možné provést odstranění pouze pomocí příspěvku, přidáte míru zabezpečení na web.

    Skutečná operace odstranění se provádí pomocí následujícího kódu, který nejprve potvrdí, že se jedná o operaci post a že ID není prázdné:

    [!code-csharp[Main](5-working-with-data/samples/sample26.cs)]

    Kód spustí příkaz SQL, který odstraní zadaný záznam a pak přesměruje uživatele zpět na stránku výpisu.
5. Spusťte *ListProductsForDelete. cshtml* v prohlížeči.

    ![obrazu](5-working-with-data/_static/image9.jpg)
6. Klikněte na odkaz **Odstranit** pro jeden z produktů. Zobrazí se stránka *DeleteProduct. cshtml* , která potvrdí, že chcete záznam odstranit.
7. Klikněte na tlačítko **Odstranit** . Záznam produktu je odstraněn a stránka je aktualizována aktualizovaným seznamem produktů.

> [!TIP]
> 
> <a id="SB_ConnectingToADatabase"></a>
> ### <a name="connecting-to-a-database"></a>Připojení k databázi
> 
> K databázi se můžete připojit dvěma způsoby. Nejprve je třeba použít metodu `Database.Open` a zadat název souboru databáze (menší přípona *. sdf* ):
> 
> `var db = Database.Open("SmallBakery");`
> 
> Metoda `Open` předpokládá, že. soubor *SDF* se nachází ve složce *dat\_App* webu. Tato složka je určená speciálně pro uchovávání dat. Například má příslušná oprávnění, aby mohl web číst a zapisovat data a jako bezpečnostní opatření nepovoluje WebMatrix přístup k souborům z této složky.
> 
> Druhým způsobem je použití připojovacího řetězce. Připojovací řetězec obsahuje informace o tom, jak se připojit k databázi. To může zahrnovat cestu k souboru nebo může obsahovat název SQL Server databáze na místním nebo vzdáleném serveru spolu s uživatelským jménem a heslem pro připojení k tomuto serveru. (Pokud zachováte data v centrálně spravované verzi SQL Server, jako je například na webu poskytovatele hostingu, vždy pomocí připojovacího řetězce určete informace o připojení databáze.)
> 
> Ve WebMatrixu se připojovací řetězce obvykle ukládají do souboru XML s názvem *Web. config*. Jak název napovídá, můžete použít soubor *Web. config* v kořenovém adresáři webu k uložení informací o konfiguraci lokality včetně všech připojovacích řetězců, které může váš web vyžadovat. Příklad připojovacího řetězce v souboru *Web. config* může vypadat takto:
> 
> [!code-xml[Main](5-working-with-data/samples/sample27.xml)]
> 
> V tomto příkladu připojovací řetězec odkazuje na databázi v instanci SQL Server, která běží na serveru někam (na rozdíl od místního souboru *. sdf* ). Museli byste nahradit vhodné názvy `myServer` a `myDatabase`a zadat SQL Server přihlašovací hodnoty pro `username` a `password`. (Uživatelské jméno a heslo nejsou nutně stejné jako vaše přihlašovací údaje systému Windows nebo jako hodnoty, které vám poskytovatel hostingu udělil pro přihlášení ke svým serverům. Požádejte správce o přesné hodnoty, které potřebujete.)
> 
> Metoda `Database.Open` je flexibilní, protože umožňuje předat buď název souboru databáze *. sdf* , nebo název připojovacího řetězce, který je uložený v souboru *Web. config* . Následující příklad ukazuje, jak se připojit k databázi pomocí připojovacího řetězce, který je znázorněn v předchozím příkladu:
> 
> [!code-cshtml[Main](5-working-with-data/samples/sample28.cshtml)]
> 
> Jak je uvedeno, metoda `Database.Open` umožňuje předat buď název databáze, nebo připojovací řetězec a určí, která se má použít. To je velmi užitečné při nasazení (publikování) webu. Při vývoji a testování webu můžete použít soubor *. sdf* ve složce *App\_data* . Pak když přesunete lokalitu na provozní server, můžete použít připojovací řetězec v souboru *Web. config* , který má stejný název jako soubor *. sdf* , ale který odkazuje na databázi &#8212; poskytovatele hostingu bez nutnosti změny kódu.
> 
> Nakonec, pokud chcete pracovat přímo s připojovacím řetězcem, můžete zavolat metodu `Database.OpenConnectionString` a předat jí skutečný připojovací řetězec místo pouze název jednoho v souboru *Web. config* . To může být užitečné v situacích, kdy z nějakého důvodu nemáte přístup k připojovacímu řetězci (nebo k hodnotám, jako je název souboru *. sdf* ), dokud nebude stránka spuštěna. Ve většině scénářů ale můžete použít `Database.Open`, jak je popsáno v tomto článku.

## <a name="additional-resources"></a>Další prostředky

- [SQL Server Compact](https://www.microsoft.com/sqlserver/2008/en/us/compact.aspx)
- [Připojení k databázi SQL Server nebo MySQL ve WebMatrixu](https://go.microsoft.com/fwlink/?LinkId=208661)
- [Ověřování uživatelských vstupů na webech s webovými stránkami ASP.NET](https://go.microsoft.com/fwlink/?LinkId=253002)

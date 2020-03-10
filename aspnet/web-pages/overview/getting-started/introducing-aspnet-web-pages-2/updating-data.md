---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
title: Představení ASP.NET webových stránek – aktualizace dat databáze | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se dozvíte, jak aktualizovat (změnit) existující položku databáze při použití webových stránek ASP.NET (Razor). Předpokládá se, že jste dokončili řadu th...
ms.author: riande
ms.date: 01/02/2018
ms.assetid: ac86ec9c-6b69-485b-b9e0-8b9127b13e6b
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
msc.type: authoredcontent
ms.openlocfilehash: 8f8bcfb7d9d2416a2699776cadbdaae8e12415ba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574226"
---
# <a name="introducing-aspnet-web-pages---updating-database-data"></a>Představení ASP.NET webových stránek – aktualizace databázových dat

tím, že [FitzMacken](https://github.com/tfitzmac)

> V tomto kurzu se dozvíte, jak aktualizovat (změnit) existující položku databáze při použití webových stránek ASP.NET (Razor). Předpokládá, že jste dokončili řadu prostřednictvím [zadávání dat pomocí formulářů pomocí webových stránek ASP.NET](entering-data.md).
> 
> Naučíte se:
> 
> - Jak vybrat jednotlivý záznam v pomocné rutině `WebGrid`.
> - Jak číst jeden záznam z databáze.
> - Jak přednačíst formulář s hodnotami z databázového záznamu.
> - Jak aktualizovat existující záznam v databázi.
> - Jak ukládat informace na stránce bez jejich zobrazení
> - Jak pomocí skrytého pole ukládat informace.
>   
> 
> Popsané funkce a technologie:
> 
> - Pomocná rutina `WebGrid`
> - Příkaz SQL `Update`.
> - Metoda `Database.Execute`.
> - Skrytá pole (`<input type="hidden">`).

## <a name="what-youll-build"></a>Co sestavíte

V předchozím kurzu jste zjistili, jak přidat záznam do databáze. Tady se dozvíte, jak zobrazit záznam pro úpravy. Na stránce *filmy* aktualizujte pomocníka `WebGrid` tak, aby se zobrazil odkaz pro **Úpravy** vedle každého filmu:

![Zobrazení webgridu, včetně odkazu upravit pro každý film](updating-data/_static/image1.png)

Když kliknete na odkaz **Upravit** , přejdete na jinou stránku, kde jsou informace o filmu již ve formuláři:

![Upravit stránku videa zobrazující film, který se má upravit](updating-data/_static/image2.png)

Můžete změnit libovolnou z těchto hodnot. Po odeslání změn kód na stránce aktualizuje databázi a přejde zpět na seznam videí.

Tato část procesu funguje téměř přesně stejně jako stránka *AddMovie. cshtml* , kterou jste vytvořili v předchozím kurzu, takže mnohé z těchto kurzů budou známé.

Existuje několik způsobů, jak můžete implementovat způsob, jak upravit jednotlivý film. Vybraný přístup byl zvolen, protože je snadné ho implementovat a snadno pochopit.

## <a name="adding-an-edit-link-to-the-movie-listing"></a>Přidání odkazu pro úpravy do seznamu filmů

Začněte tím, že aktualizujete stránku *filmy* , aby každý seznam filmů obsahoval i odkaz pro **Úpravy** .

Otevřete soubor *Movies. cshtml* .

V těle stránky změňte kód `WebGrid` přidáním sloupce. Zde je upravený kód:

[!code-html[Main](updating-data/samples/sample1.html?highlight=6)]

Nový sloupec je tento:

[!code-html[Main](updating-data/samples/sample2.html)]

V bodě tohoto sloupce je zobrazen odkaz (`<a>` element), jehož text říká "Edit". I když je po spuštění stránky potřeba vytvořit odkaz, který vypadá takto: `id` hodnota pro každý film se liší:

[!code-css[Main](updating-data/samples/sample3.css)]

Tento odkaz vyvolá stránku s názvem *EditMovie*a předá řetězec dotazu `?id=7` této stránce.

Syntaxe nového sloupce může vypadat jako složitý, ale je to pouze proto, že se skládá z několika prvků. Každý jednotlivý prvek je jednoduchý. Pokud se zaměříte na pouze `<a>` element, uvidíte tento kód:

[!code-html[Main](updating-data/samples/sample4.html)]

Další informace o tom, jak mřížka funguje: Mřížka zobrazuje řádky, jednu pro každý záznam databáze a zobrazuje sloupce pro každé pole v záznamu databáze. Při sekonstrukci každého řádku mřížky objekt `item` obsahuje záznam databáze (položku) pro tento řádek. Toto uspořádání poskytuje způsob, jak v kódu získat data pro daný řádek. To je to, co vidíte tady: výraz `item.ID` získává hodnotu ID aktuální položky databáze. Můžete získat libovolný z hodnot databáze (název, Žánr nebo rok) stejným způsobem jako při použití `item.Title`, `item.Genre`nebo `item.Year`.

Výraz `"~/EditMovie?id=@item.ID` kombinuje pevně zakódovaný součást cílové adresy URL (`~/EditMovie?id=`) s tímto dynamicky odvozeným ID. (V předchozím kurzu jste viděli operátor `~`, jedná se o operátor ASP.NET, který představuje aktuální kořenový adresář webu.)

Výsledkem je, že tato část kódu ve sloupci jednoduše vytvoří jako následující kód v době běhu něco podobného jako v následujícím kódu:

[!code-xml[Main](updating-data/samples/sample5.xml)]

Přirozeně platí, že skutečná hodnota `id` bude pro každý řádek odlišná.

## <a name="creating-a-custom-display-for-a-grid-column"></a>Vytvoření vlastního zobrazení pro sloupec mřížky

Nyní zpět do sloupce Grid. Tři sloupce, které jste původně použili v mřížce, zobrazují jenom datové hodnoty (název, Žánr a rok). Toto zobrazení jste určili předáním názvu sloupce databáze &mdash; například `grid.Column("Title")`.

Tento nový sloupec odkaz pro **Úpravy** se liší. Místo zadání názvu sloupce předáváte `format` parametr. Tento parametr umožňuje definovat značku, kterou `WebGrid` pomocnou nápovědu vykreslí spolu s hodnotou `item` pro zobrazení dat sloupce jako tučné nebo zelené nebo v jakémkoli požadovaném formátu. Pokud byste například chtěli, aby se nadpis zobrazoval tučně, mohli byste vytvořit sloupec podobný tomuto příkladu:

[!code-html[Main](updating-data/samples/sample6.html)]

(Různé `@` znaky, které vidíte ve vlastnosti `format` označuje přechod mezi značkami a hodnotou kódu.)

Jakmile budete vědět o vlastnosti `format`, je snazší pochopit, jak je nový sloupec odkaz pro **Úpravy** vložen dohromady:

[!code-html[Main](updating-data/samples/sample7.html)]

Sloupec se skládá *pouze* ze značky, který vykresluje odkaz, a navíc některé informace (ID), které jsou extrahovány z záznamu databáze pro řádek.

> [!TIP]
> 
> **Pojmenované parametry a poziční parametry pro metodu**
> 
> V mnoha případech, kdy jste volali metodu a předali do ní parametry, jste jednoduše zadali hodnoty parametrů oddělené čárkami. Tady je několik příkladů:
> 
> `db.Execute(insertCommand, title, genre, year)`
> 
> `Validation.RequireField("title", "You must enter a title")`
> 
> Neuváděli jsme problém, když jste si tento kód poprvé viděli, ale v každém případě předáváte parametry metodám v určitém pořadí &mdash; konkrétně, pořadí, ve kterém jsou parametry definované v této metodě. V případě `db.Execute` a `Validation.RequireFields`se při spuštění stránky zobrazí chybová zpráva, když se stránka spustí, nebo alespoň některých neobvyklých výsledků. Jasně je nutné znát pořadí předání parametrů v. (Ve WebMatrix vám IntelliSense může pořídit, jak zjistit název, typ a pořadí parametrů.)
> 
> Jako alternativu k předávání hodnot v pořadí můžete použít *pojmenované parametry*. (Předání parametrů v pořadí se říká použití *pozičních parametrů*.) U pojmenovaných parametrů explicitně zahrnete název parametru při předání jeho hodnoty. Pojmenované parametry už v těchto kurzech využijete několikrát. Příklad:
> 
> [!code-csharp[Main](updating-data/samples/sample8.cs)]
> 
> a
> 
> [!code-css[Main](updating-data/samples/sample9.css)]
> 
> Pojmenované parametry jsou užitečné v několika situacích, zejména v případě, že metoda přijímá mnoho parametrů. Jedním z nich je, že chcete předat jenom jeden nebo dva parametry, ale hodnoty, které chcete předat, nejsou mezi prvními pozicemi v seznamu parametrů. Další situací je, že chcete, aby byl váš kód čitelnější předáním parametrů v pořadí, které vám dává smysl.
> 
> Aby bylo možné použít pojmenované parametry, je třeba znát názvy parametrů. WebMatrix IntelliSense může *Zobrazit* názvy, ale nemůže je aktuálně vyplnit za vás.

## <a name="creating-the-edit-page"></a>Vytvoření stránky pro úpravy

Nyní můžete vytvořit stránku *EditMovie* . Když uživatel klikne na odkaz pro **Úpravy** , ukončí se na této stránce.

Vytvořte stránku s názvem *EditMovie. cshtml* a nahraďte obsah souboru následujícím kódem:

[!code-cshtml[Main](updating-data/samples/sample10.cshtml)]

Tato značka a kód se podobá tomu, co máte na stránce *AddMovie* . V textu tlačítka Odeslat je malý rozdíl. Stejně jako u stránky *AddMovie* existuje `Html.ValidationSummary` volání, které zobrazí chyby ověřování, pokud existují. Tentokrát opouštíme volání `Validation.Message`, protože se zobrazí chyby v souhrnu ověření. Jak je uvedeno v předchozím kurzu, můžete použít souhrn ověření a jednotlivé chybové zprávy v různých kombinacích.

Znovu si všimněte, že atribut `method` elementu `<form>` je nastaven na `post`. Stejně jako u stránky *AddMovie. cshtml* provede tato stránka změny v databázi. Proto by tento formulář měl provádět operaci `POST`. (Další informace o rozdílu mezi operacemi `GET` a `POST` najdete v tématu o [bezpečnosti operací GET, post a http](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety) v kurzu o formulářích HTML.)

Jak jste viděli v předchozím kurzu, atributy `value` textových polí se nastavují pomocí kódu Razor, aby je bylo možné předem načíst. Tentokrát ale používáte proměnné jako `title` a `genre` pro tuto úlohu místo `Request.Form["title"]`:

`<input type="text" name="title" value="@title" />`

Stejně jako v tomto kódu bude tento kód předem načítat hodnoty textového pole s hodnotami filmu. Zobrazí se čas, proč je užitečné místo použití objektu `Request` použít proměnné.

Na této stránce je také `<input type="hidden">` element. Tento element ukládá ID filmu bez toho, aby byl viditelný na stránce. ID je zpočátku předáno na stránku pomocí hodnoty řetězce dotazu (`?id=7` nebo podobný v adrese URL). Vložením hodnoty ID do skrytého pole se můžete ujistit, že je k dispozici při odeslání formuláře, a to i v případě, že již nemáte přístup k původní adrese URL, ve které byla stránka vyvolána.

Na rozdíl od stránky *AddMovie* má kód stránky *EditMovie* dvě odlišné funkce. První funkce je, že když se stránka zobrazí poprvé (a *pouze* potom), kód získá ID filmu z řetězce dotazu. Kód pak pomocí ID přečte příslušný film z databáze a zobrazí ho (přednačtení) v textových polích.

Druhá funkce je, že když uživatel klikne na tlačítko **Odeslat změny** , kód musí číst hodnoty textových polí a ověřit je. Kód také musí aktualizovat položku databáze o nové hodnoty. Tato technika je podobná přidání záznamu, jak jste viděli v *AddMovie*.

## <a name="adding-code-to-read-a-single-movie"></a>Přidání kódu pro čtení jednoho filmu

Chcete-li provést první funkci, přidejte tento kód do horní části stránky:

[!code-cshtml[Main](updating-data/samples/sample11.cshtml)]

Většina tohoto kódu je uvnitř bloku, který začíná `if(!IsPost)`. Operátor `!` znamená "NOT", takže výraz znamená, že se nejedná o *příspěvek po odeslání*, což je nepřímý způsob, jak vyjádřit, *zda je tato žádost poprvé, kdy byla tato stránka spuštěna*. Jak bylo uvedeno dříve, tento kód by měl běžet *pouze* při prvním spuštění stránky. Pokud jste kód nezahrnuli do `if(!IsPost)`, bude spuštěn při každém vyvolání stránky, ať už poprvé, nebo v reakci na kliknutí na tlačítko.

Všimněte si, že kód obsahuje `else` blokovat tento čas. Jak jsme uvedli, že jsme zavedli `if` bloky, někdy budete chtít spustit alternativní kód, pokud podmínka, kterou testujete, není pravdivá. To je v tomto případě. Pokud podmínka projde (to znamená, že pokud je ID předané na stránku ok), přečtěte si řádek z databáze. Nicméně pokud podmínka není splněna, je spuštěn blok `else` a kód nastaví chybovou zprávu.

## <a name="validating-a-value-passed-to-the-page"></a>Ověření hodnoty předané stránce

Kód používá `Request.QueryString["id"]` k získání ID, které je předáno stránce. Kód zajišťuje, aby byla hodnota pro ID skutečně předána. Pokud nebyla předána žádná hodnota, kód nastaví chybu ověřování.

Tento kód ukazuje jiný způsob, jak ověřit informace. V předchozím kurzu jste pracovali s pomocníkem `Validation`. Zaregistrovali jste pole k ověření a ASP.NET automaticky prošly ověřováním a zobrazenými chybami pomocí `Html.ValidationMessage` a `Html.ValidationSummary`. V takovém případě ale neověřujete vstup uživatele. Místo toho ověřujete hodnotu, která byla předána stránce jinde. Pomocná rutina `Validation` to neudělá za vás.

Proto si tuto hodnotu zkontrolujete sami tak, že ji otestujete pomocí `if(!Request.QueryString["ID"].IsEmpty()`). Pokud dojde k potížím, můžete zobrazit chybu pomocí `Html.ValidationSummary`, stejně jako u pomocné rutiny `Validation`. Chcete-li to provést, zavolejte `Validation.AddFormError` a předejte jí zprávu k zobrazení. `Validation.AddFormError` je vestavěná metoda, která umožňuje definovat vlastní zprávy, které se propojují se systémem ověřování, který jste už obeznámeni s nástrojem. (Později v tomto kurzu budeme mluvit o tom, jak tento proces ověřování udělat trochu robustnější.)

Po ujištění, že je pro film k dispozici ID, přečte tento kód databázi a vyhledá pouze jednu položku databáze. (Pravděpodobně jste si všimli obecný vzor pro databázové operace: Otevřete databázi, definujte příkaz SQL a spusťte příkaz.) Tentokrát příkaz SQL `Select` zahrnuje `WHERE ID = @0`. Vzhledem k tomu, že ID je jedinečné, může být vrácen pouze jeden záznam.

Dotaz je proveden pomocí `db.QuerySingle` (není `db.Query`, jak jste použili pro záznam filmu) a kód vloží výsledek do proměnné `row`. Název `row` je libovolný. proměnné můžete pojmenovat libovolným způsobem. Proměnné inicializované v horní části se pak vyplní podrobnostmi o videu, aby se tyto hodnoty mohly zobrazit v textových polích.

## <a name="testing-the-edit-page-so-far"></a>Testování stránky pro úpravy (zatím daleko)

Pokud chcete stránku otestovat, spusťte nyní stránku *filmy* a klikněte na odkaz **Upravit** vedle libovolného videa. Zobrazí se stránka *EditMovie* s podrobnostmi, které jste vyplnili pro vybraný film:

![Upravit stránku videa zobrazující film, který se má upravit](updating-data/_static/image3.png)

Všimněte si, že adresa URL stránky obsahuje něco jako `?id=10` (nebo nějaké jiné číslo). Proto jste se seznámili s tím, že na stránce *videa* funguje **Úpravy** , že vaše stránka čte ID z řetězce dotazu a že databázový dotaz, který získá jeden záznam filmu, funguje.

Můžete změnit informace o videu, ale po kliknutí na tlačítko **Odeslat změny**nedojde k žádné akci.

## <a name="adding-code-to-update-the-movie-with-the-users-changes"></a>Přidání kódu pro aktualizaci videa se změnami uživatele

V souboru *EditMovie. cshtml* pro implementaci druhé funkce (uložení změn) přidejte následující kód těsně do uzavírací závorky bloku `@`. (Pokud si nejste jistí přesně, kam kód vložit, můžete si prohlédnout [kompletní výpis kódu na stránce Upravit film](#Complete_Page_Listing_for_EditMovie) , která se zobrazí na konci tohoto kurzu.)

[!code-csharp[Main](updating-data/samples/sample12.cs)]

Tento kód je opět podobný kódu v *AddMovie*. Kód je v bloku `if(IsPost)`, protože tento kód je spuštěn pouze v případě, že uživatel klikne na tlačítko **Odeslat změny** &mdash; to, kdy (a pouze když) byl formulář publikován. V tomto případě nepoužíváte test jako `if(IsPost && Validation.IsValid())`– to znamená, že nezkombinujete oba testy pomocí a. Na této stránce nejprve určíte, zda se jedná o odeslání formuláře (`if(IsPost)`), a poté zaregistrujte pole pro ověření. Potom můžete testovat výsledky ověření (`if(Validation.IsValid()`). Tok je trochu jiný než na stránce *AddMovie. cshtml* , ale účinek je stejný.

Hodnoty textových polí získáte pomocí `Request.Form["title"]` a podobného kódu pro ostatní prvky `<input>`. Všimněte si, že tentokrát kód získá ID filmu z skrytého pole (`<input type="hidden">`). Při prvním spuštění stránky kód získal z řetězce dotazu ID. Hodnotu z skrytého pole získáte, abyste se ujistili, že získáváte ID původně zobrazeného videa pro případ, že řetězec dotazu byl od té doby nějakým způsobem změněn.

Skutečně je důležité rozdíl mezi kódem *AddMovie* a tímto kódem je, že v tomto kódu je místo příkazu `Insert Into` použit příkaz SQL `Update`. Následující příklad ukazuje syntaxi příkazu SQL `Update`:

`UPDATE table SET col1="value", col2="value", col3="value" ... WHERE ID = value`

Můžete určit libovolné sloupce v libovolném pořadí a nemusíte nutně aktualizovat každý sloupec během operace `Update`. (Samotné ID nemůžete aktualizovat, protože to by v platnosti mělo Uložit záznam jako nový záznam a to není u operace `Update` povolené.)

> [!NOTE] 
> 
> **Důležité** informace Klauzule `Where` s ID je velmi důležitá, protože to je způsob, jakým databáze ví, který záznam databáze chcete aktualizovat. Pokud jste opustili klauzuli `Where`, databáze by aktualizovala *všechny* záznamy v databázi. Ve většině případů se jedná o havárie.

V kódu jsou hodnoty, které se mají aktualizovat, předány příkazu SQL pomocí zástupných symbolů. Pokud chcete opakovat, co jsme řekli: z bezpečnostních důvodů používejte k předávání hodnot do příkazu SQL *jenom* zástupné symboly.

Poté, co kód používá `db.Execute` ke spuštění příkazu `Update`, přesměruje zpět na stránku výpisu, kde můžete zobrazit změny.

> [!TIP] 
> 
> **Různé příkazy SQL, různé metody**
> 
> Možná jste si všimli, že ke spouštění různých příkazů SQL používáte trochu odlišné metody. Chcete-li spustit dotaz `Select`, který potenciálně vrátí více záznamů, použijte metodu `Query`. Pokud chcete spustit `Select` dotaz, který znáte, vrátí jenom jednu položku databáze, použijte metodu `QuerySingle`. Chcete-li spustit příkazy, které provedou změny, ale nevracejí položky databáze, použijte metodu `Execute`.
> 
> Musíte mít různé metody, protože každá z nich vrací různé výsledky, protože jste viděli rozdíl mezi `Query` a `QuerySingle`. (Metoda `Execute` ve skutečnosti vrací hodnotu také &mdash;, konkrétně počet řádků databáze, které byly ovlivněny příkazem &mdash;, ale zatím jste je dosud nemuseli ignorovat.)
> 
> Samozřejmě může metoda `Query` vracet pouze jeden řádek databáze. ASP.NET však vždy zpracovává výsledky metody `Query` jako kolekci. I v případě, že metoda vrátí pouze jeden řádek, je nutné z kolekce extrahovat jeden řádek. Proto v situacích, kdy *víte* , že se dostanete jenom na jeden řádek, je to pro použití `QuerySingle`trochu pohodlnější.
> 
> K dispozici je několik dalších metod, které provádějí konkrétní typy databázových operací. Seznam metod databáze najdete v [rychlé referenční příručce k rozhraní API webových stránek ASP.NET](../../api-reference/asp-net-web-pages-api-reference.md#Data).

## <a name="making-validation-for-the-id-more-robust"></a>Provádí se ověřování pro robustnější ID.

Při prvním spuštění stránky získáte ID filmu z řetězce dotazu, abyste se mohli dostat k tomuto videu z databáze. Provedli jste si, že skutečně existovala hodnota pro vyhledání, kterou jste provedli pomocí tohoto kódu:

[!code-csharp[Main](updating-data/samples/sample13.cs)]

Tento kód jste použili k tomu, abyste se ujistili, že pokud se uživatel dostane na stránku *EditMovies* bez předchozího výběru videa na stránce *filmy* , stránka by zobrazila uživatelsky přívětivou chybovou zprávu. (V opačném případě se uživatelům zobrazí chyba, která by ji pravděpodobně Zaměňujte.)

Toto ověřování však není velmi robustní. Tato stránka se může vyvolávat taky s těmito chybami:

- ID není číslo. Například stránku lze vyvolat pomocí adresy URL, jako je `http://localhost:nnnnn/EditMovie?id=abc`.
- ID je číslo, ale odkazuje na film, který neexistuje (například `http://localhost:nnnnn/EditMovie?id=100934`).

Pokud se zajímá zobrazí chyby, které jsou výsledkem těchto adres URL, spusťte stránku *filmy* . Vyberte film, který chcete upravit, a pak změňte adresu URL stránky *EditMovie* na adresu URL, která obsahuje abecední ID nebo ID neexistujícího filmu.

Co byste měli dělat? První oprava je zajistit, aby nejenom bylo předáno ID do stránky, ale toto ID je celé číslo. Změňte kód pro `!IsPost` testu tak, aby vypadal jako v tomto příkladu:

[!code-csharp[Main](updating-data/samples/sample14.cs)]

Přidali jste do testu `IsEmpty` druhou podmínku, která je propojená s `&&` (logická a):

[!code-csharp[Main](updating-data/samples/sample15.cs)]

Můžete si pamatovat od kurzu [Úvod k programování webových stránek ASP.NET](../introducing-razor-syntax-c.md) , které metody jako `AsBool` `AsInt` převod řetězce znaků na jiný datový typ. Metoda `IsInt` (a další, jako je `IsBool` a `IsDateTime`), jsou podobné. Testuje však pouze to, zda *lze* řetězec převést, aniž by bylo nutné převod skutečně provést. Takže v podstatě říkáte, že *hodnota řetězce dotazu může být převedena na celé číslo...* .

Dalším možným problémem je hledání filmu, který neexistuje. Kód pro získání filmu vypadá jako tento kód:

[!code-csharp[Main](updating-data/samples/sample16.cs)]

Pokud předáte `movieId` hodnotu metodě `QuerySingle`, která neodpovídá skutečnému filmu, nebude nic vráceno a příkazy, které následují (například `title=row.Title`), mají za následek chyby.

Teď je k dispozici Snadná oprava. Pokud metoda `db.QuerySingle` nevrátí žádné výsledky, bude mít proměnná `row` hodnotu null. Proto můžete před pokusem o získání hodnot z něj ověřit, zda je proměnná `row` null. Následující kód přidá `if` blok kolem příkazů, které získávají hodnoty z objektu `row`:

[!code-csharp[Main](updating-data/samples/sample17.cs)]

U těchto dvou dalších ověřovacích ověřovacích testů se stránka bude více vykazovat jako odrážka. Úplný kód pro `!IsPost`ovou větev teď vypadá jako v tomto příkladu:

[!code-csharp[Main](updating-data/samples/sample18.cs)]

Jednou z nich si ukážeme, že tento úkol je vhodný pro `else` blok. Pokud testy neprojde, `else` blokuje nastavování chybových zpráv.

## <a name="adding-a-link-to-return-to-the-movies-page"></a>Přidání odkazu, který se má vrátit na stránku filmů

Poslední a užitečnou podrobností je přidat odkaz zpátky na stránku *filmy* . V běžném toku událostí se uživatelé spustí na stránce *filmy* a klikněte na odkaz **Upravit** . Tím se přidají na stránku *EditMovie* , kde můžou upravovat film a kliknout na tlačítko. Poté, co kód zpracuje změnu, přesměruje zpět na stránku *filmy* .

Naopak

- Uživatel se může rozhodnout neměnit cokoli.
- Uživatel se mohl na tuto stránku setkat, aniž byste na stránce *filmy* nejdřív klikli na odkaz pro **Úpravy** .

V obou případech chcete, aby se mohli snadno vrátit do hlavního výpisu. Jedná se o snadnou opravu &mdash; přidejte následující značku hned za uzavírací značku `</form>` v kódu:

[!code-html[Main](updating-data/samples/sample19.html)]

Tento kód používá stejnou syntaxi pro `<a>` element, který jste viděli jinde. Adresa URL zahrnuje `~` "kořen webu".

## <a name="testing-the-movie-update-process"></a>Testování procesu aktualizace filmů

Nyní můžete provést test. Spusťte stránku *filmy* a klikněte na **Upravit** vedle videa. Když se zobrazí stránka *EditMovie* , proveďte změny ve videu a klikněte na **Odeslat změny**. Když se zobrazí seznam filmů, ujistěte se, že jsou zobrazené vaše změny.

Pokud chcete zajistit, aby ověřování fungovalo, klikněte na **Upravit** pro jiný film. Až se dostanete na stránku *EditMovie* , zrušte zaškrtnutí pole **Žánr** (nebo pole **year** nebo obojí) a zkuste odeslat změny. Zobrazí se chyba, protože byste očekávali:

![Stránka upravit film ukazující chyby ověřování](updating-data/_static/image4.png)

Kliknutím na odkaz **Přejít na seznam filmů** zrušte změny a vraťte se na stránku *filmy* .

## <a name="coming-up-next"></a>Připravujeme další

V dalším kurzu uvidíte, jak odstranit záznam videa.

## <a name="complete-listing-for-movie-page-updated-with-edit-links"></a>Úplný výpis stránky videa (aktualizovaný pomocí odkazů pro úpravy)

[!code-cshtml[Main](updating-data/samples/sample20.cshtml)]

<a id="Complete_Page_Listing_for_EditMovie"></a>
## <a name="complete-page-listing-for-edit-movie-page"></a>Dokončení výpisu stránky pro stránku Upravit film

[!code-cshtml[Main](updating-data/samples/sample21.cshtml)]

## <a name="additional-resources"></a>Další prostředky

- [Seznámení s ASP.NET webovým programováním pomocí syntaxe Razor](../../getting-started/introducing-razor-syntax-c.md)
- [Příkaz SQL Update](http://www.w3schools.com/sql/sql_update.asp) na webu w3schools

> [!div class="step-by-step"]
> [Předchozí](entering-data.md)
> [Další](deleting-data.md)

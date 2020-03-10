---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
title: Představení webových stránek ASP.NET – zadávání dat databáze pomocí formulářů | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se dozvíte, jak vytvořit vstupní formulář a pak zadat data, která dostanete z formuláře do tabulky databáze při použití webových stránek ASP.NET (...
ms.author: riande
ms.date: 05/28/2015
ms.assetid: d37c93fc-25fd-4e94-8671-0d437beef206
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
msc.type: authoredcontent
ms.openlocfilehash: b9354a7b97a7df9020a681f709e16a92650cfcf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624535"
---
# <a name="introducing-aspnet-web-pages---entering-database-data-by-using-forms"></a>Představení webových stránek ASP.NET – zadávání dat databáze pomocí formulářů

tím, že [FitzMacken](https://github.com/tfitzmac)

> V tomto kurzu se dozvíte, jak vytvořit vstupní formulář a pak zadat data, která dostanete z formuláře do tabulky databáze při použití webových stránek ASP.NET (Razor). Předpokládá, že jste dokončili řadu prostřednictvím [základních formulářů HTML v ASP.NET webových stránkách](https://go.microsoft.com/fwlink/?LinkId=251581).
> 
> Naučíte se:
> 
> - Další informace o tom, jak zpracovávat formuláře zadávání.
> - Jak přidat (vložit) data do databáze.
> - Jak zajistit, aby uživatelé zadali požadovanou hodnotu ve formuláři (ověření vstupu uživatele).
> - Jak zobrazit chyby ověřování.
> - Jak přejít na jinou stránku z aktuální stránky.
>   
> 
> Popsané funkce a technologie:
> 
> - Metoda `Database.Execute`.
> - Příkaz SQL `Insert Into`
> - Pomocná rutina `Validation`
> - Metoda `Response.Redirect`.

## <a name="what-youll-build"></a>Co sestavíte

V předchozím kurzu, který ukázal, jak vytvořit databázi, jste zadali data databáze tak, že upravíte databázi přímo v WebMatrixu a pracujete v pracovním prostoru **databáze** . Ve většině aplikací to není praktický způsob, jak vložit data do databáze, i když. Takže v tomto kurzu vytvoříte webové rozhraní, které vám umožní nebo kdokoli zadá data a uloží je do databáze.

Vytvoříte stránku, kde můžete zadat nové filmy. Stránka bude obsahovat formulář, který obsahuje pole (textová pole), kde můžete zadat název, Žánr a rok videa. Stránka bude vypadat jako na této stránce:

![Stránka Přidat film v prohlížeči](entering-data/_static/image1.png)

Textová pole budou prvky HTML `<input>`, které budou vypadat jako tento kód:

`<input type="text" name="genre" value="" />`

## <a name="creating-the-basic-entry-form"></a>Vytvoření základního formuláře položky

Vytvořte stránku s názvem *AddMovie. cshtml*.

Nahraďte obsah souboru následujícím kódem. Přepsat vše; v krátké době přidáte blok kódu.

[!code-cshtml[Main](entering-data/samples/sample1.cshtml)]

Tento příklad ukazuje typický kód HTML pro vytvoření formuláře. Používá prvky `<input>` pro textová pole a pro tlačítko Odeslat. Titulky pro textová pole jsou vytvořeny pomocí standardních `<label>` prvků. Prvky `<fieldset>` a `<legend>` vloží do formuláře Skvělé pole.

Všimněte si, že na této stránce `<form>` element používá `post` jako hodnotu atributu `method`. V předchozím kurzu jste vytvořili formulář, který používal metodu `get`. To bylo správné, protože ačkoliv formulář odeslal hodnoty na server, požadavek provedl žádné změny. Všechna data byla načtena různými způsoby. Na této stránce ale *provedete* změny – Chystáte se přidat nové záznamy databáze. Proto by tato forma měla používat metodu `post`. (Další informace o rozdílu mezi operacemi `GET` a `POST` najdete v předchozím kurzu na postranním panelu pro[získání, odeslání a zabezpečení operací HTTP](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety) .)

Všimněte si, že každé textové pole má element `name` (`title`, `genre`, `year`). Jak jste viděli v předchozím kurzu, tyto názvy jsou důležité, protože musíte mít tyto názvy, abyste mohli později získat vstup uživatele. Můžete použít libovolný název. Je užitečné použít smysluplné názvy, které vám pomůžou zapamatovat si, se kterými daty pracujete.

Atribut `value` každého prvku `<input>` obsahuje bitovou kopii kódu Razor (například `Request.Form["title"]`). Zjistili jste ve verzi tohoto štychu v předchozím kurzu, abyste zachovali hodnotu zadanou do textového pole (pokud existuje) po odeslání formuláře.

## <a name="getting-the-form-values"></a>Získání hodnot formuláře

Dále přidáte kód, který zpracovává formulář. V osnově provedete následující akce:

1. Ověřte, zda je stránka publikována (odeslána). Chcete, aby se váš kód spouštěl pouze v případě, že uživatel klikl na tlačítko, nikoli při prvním spuštění stránky.
2. Načte hodnoty, které uživatel zadal do textových polí. V takovém případě, protože formulář používá příkaz `POST`, získáte hodnoty formuláře z kolekce `Request.Form`.
3. Vložte hodnoty jako nový záznam do tabulky databáze *filmů* .

V horní části souboru přidejte následující kód:

[!code-cshtml[Main](entering-data/samples/sample2.cshtml)]

První pár řádků vytvoří proměnné (`title`, `genre`a `year`), aby se hodnoty z textových polí vešly. Řádková `if(IsPost)` zajistí, že proměnné jsou nastaveny *pouze* v případě, že uživatel klikne na tlačítko **přidat video** – to znamená, když byl formulář publikován.

Jak jste viděli v předchozím kurzu, získáte hodnotu textového pole pomocí výrazu, jako je `Request.Form["name"]`, kde *název* je název `<input>` elementu.

Názvy proměnných (`title`, `genre`a `year`) jsou libovolné. Podobně jako názvy, které přiřadíte `<input>` prvků, můžete je zavolat libovolným způsobem. (Názvy proměnných nemusejí odpovídat atributům názvu `<input>` prvků ve formuláři.) Ale stejně jako u elementů `<input>` je vhodné použít názvy proměnných, které odráží data, která obsahují. Když píšete kód, konzistentní názvy usnadňují zapamatování, se kterými daty pracujete.

## <a name="adding-data-to-the-database"></a>Přidání dat do databáze

V bloku kódu, který jste právě přidali, těsně *uvnitř* uzavírací složené závorky (`}`) bloku `if` (ne pouze uvnitř bloku kódu) přidejte následující kód:

[!code-csharp[Main](entering-data/samples/sample3.cs)]

Tento příklad je podobný kódu, který jste použili v předchozím kurzu pro načtení a zobrazení dat. Řádek, který začíná `db =` otevře databázi, například dřív, a další řádek definuje příkaz SQL znovu, jak jste viděli předtím. Tentokrát ale definuje příkaz SQL `Insert Into`. Následující příklad ukazuje obecnou syntaxi příkazu `Insert Into`:

`INSERT INTO table (column1, column2, column3, ...) VALUES (value1, value2, value3, ...)`

Jinými slovy, zadáte tabulku, do které se má vložit, a pak uveďte sloupce, které se mají vložit do, a potom vypište hodnoty, které chcete vložit. (Jak je uvedeno dříve, SQL nerozlišuje velká a malá písmena, ale někteří lidé mají na velká písmena, aby usnadnili čtení příkazu.)

Sloupce, které vkládáte do, jsou již uvedeny v příkazu – `(Title, Genre, Year)`. Zajímavá část je způsob, jak získat hodnoty z textových polí do `VALUES` části příkazu. Místo skutečných hodnot vidíte `@0`, `@1`a `@2`, což jsou zástupné symboly kurzů. Při spuštění příkazu (na řádku `db.Execute`) předáte hodnoty, které jste získali z textových polí.

**Významná!** Mějte na paměti, že jediným způsobem, jak byste měli v příkazu SQL zahrnout data zadaná online uživatelem, je použít zástupné symboly, jak vidíte tady (`VALUES(@0, @1, @2)`). Pokud do příkazu SQL zřetězete vstup uživatele, otevřete sami sebe s útokem na injektáže SQL, jak je vysvětleno v tématu [základy formulářů na webových stránkách ASP.NET](https://go.microsoft.com/fwlink/?LinkId=251581) (předchozí kurz).

V rámci `if` bloku přidejte následující řádek za `db.Execute` řádek:

[!code-css[Main](entering-data/samples/sample4.css)]

Po vložení nového videa do databáze se tento řádek přeskočí (přesměrovává) na stránku *filmy* , abyste viděli film, který jste právě zadali. Operátor `~` znamená "kořen webu". (Operátor `~` funguje pouze na stránkách ASP.NET, ne v HTML všeobecně.)

Úplný blok kódu vypadá jako v tomto příkladu:

[!code-cshtml[Main](entering-data/samples/sample5.cshtml)]

## <a name="testing-the-insert-command-so-far"></a>Testování příkazu INSERT (zatím daleko)

Ještě nejste hotovi, ale teď je vhodná doba k otestování.

Ve stromovém zobrazení souborů ve WebMatrixu klikněte pravým tlačítkem na stránku *AddMovie. cshtml* a pak klikněte na **Spustit v prohlížeči**.

![Stránka Přidat film v prohlížeči](entering-data/_static/image2.png)

(Pokud skončíte s jinou stránkou v prohlížeči, ujistěte se, že adresa URL je `http://localhost:nnnnn/AddMovie`), kde *nnnnn* je číslo portu, které používáte.)

Zobrazila se chybová stránka? Pokud ano, přečtěte si je pečlivě a ujistěte se, že kód přesně vypadá, co byl uveden výše.

Zadejte film do formuláře &mdash; například, použijte "občanský Kane", "drama" a "1941". (Nebo cokoli.) Pak klikněte na **Přidat film**.

Pokud vše proběhne správně, budete přesměrováni na stránku *filmy* . Ujistěte se, že je uvedený nový film.

![Stránka filmy zobrazující nově přidaný film](entering-data/_static/image3.png)

## <a name="validating-user-input"></a>Ověřování vstupu uživatele

Vraťte se na stránku *AddMovie* nebo ji znovu spusťte. Zadejte jiný film, ale tentokrát zadejte jenom nadpis &mdash; například, do pole deště zadejte "singin'". Pak klikněte na **Přidat film**.

Budete přesměrováni na stránku *filmy* znovu. Nový film můžete najít, ale neúplný.

![Stránka filmy s informacemi o novém videu, u kterých chybí některé hodnoty](entering-data/_static/image4.png)

Při vytváření tabulky *filmů* jste výslovně uvedli, že žádná pole by mohla mít hodnotu null. Tady máte vstupní formulář pro nové filmy a zanecháváte si pole prázdné. To je chyba.

V tomto případě databáze ve skutečnosti nevyvolává (nebo *vyvolává*) chybu. Nezadali jste Žánr nebo rok, takže kód na stránce *AddMovie* tyto hodnoty považuje za vyvolané *prázdné řetězce*. Když jste spustili příkaz SQL `Insert Into`, pole žánru a roku neobsahovala v nich užitečná data, ale nemají hodnotu null.

Zjevně nechcete uživatelům umožnit zadávat do databáze informace o polovičním vyprázdnění filmů. Řešením je ověřit vstup uživatele. Ve výchozím nastavení se ověří, že uživatel zadal hodnotu pro všechna pole (to znamená, že žádná z nich neobsahuje prázdný řetězec).

> [!TIP]
> 
> **Null a prázdné řetězce**
> 
> V programování existuje rozdíl mezi různými pojmy "žádná hodnota". Obecně je hodnota *null* , pokud nebyla nikdy nastavena nebo inicializována jakýmkoli způsobem. Naproti tomu proměnná, která očekává znaková data (řetězce), může být nastavena na *prázdný řetězec*. V takovém případě hodnota není null; je pouze explicitně nastaveno na řetězec znaků, jejichž délka je nula. Tyto dva příkazy znázorňují rozdíl:
> 
> [!code-csharp[Main](entering-data/samples/sample6.cs)]
> 
> Je to poněkud složitější než to, ale důležité je, že `null` představuje řazení neurčitého stavu.
> 
> Nyní je důležité pochopit přesně, pokud je hodnota null, a když je pouze prázdný řetězec. V kódu stránky *AddMovie* získáte hodnoty textových polí pomocí `Request.Form["title"]` a tak dále. Při prvním spuštění stránky (před kliknutím na tlačítko) je hodnota `Request.Form["title"]` null. Ale při odeslání formuláře `Request.Form["title"]` Získá hodnotu `title` textového pole. Není zřejmé, ale prázdné textové pole není null. obsahuje pouze prázdný řetězec. Takže když se kód spustí jako odpověď na kliknutí na tlačítko, `Request.Form["title"]` obsahuje prázdný řetězec.
> 
> Proč je tento rozdíl důležitý? Při vytváření tabulky *filmů* jste výslovně uvedli, že žádná pole by mohla mít hodnotu null. Ale tady máte vstupní formulář pro nové filmy a necháte pole prázdná. Měli byste očekávat, že databáze bude stěžovatelem při pokusu o uložení nových filmů, které neobsahovaly hodnoty pro žánr nebo rok. Ale to je &mdash;, i když necháte tato textová pole prázdná, hodnoty nemůžou být null. Jedná se o prázdné řetězce. V důsledku toho můžete uložit nové filmy do databáze s prázdnými sloupci &mdash;, ale ne null! &mdash; hodnoty. Proto je nutné se ujistit, že uživatelé neodesílají prázdný řetězec, který můžete provést ověřením vstupu uživatele.

### <a name="the-validation-helper"></a>Pomocník pro ověřování

Webové stránky ASP.NET obsahují nápovědu &mdash; `Validation` pomocníka &mdash;, pomocí kterých se můžete ujistit, že uživatelé zadávají data vyhovující vašim požadavkům. Pomocník pro `Validation` je jedním z pomocných rutin, které jsou integrované pro ASP.NET webových stránek, takže je nemusíte instalovat jako balíček pomocí NuGet, jak jste nainstalovali pomocníka Gravatar v předchozím kurzu.

Chcete-li ověřit vstup uživatele, proveďte následující akce:

- Pomocí kódu určete, že chcete v textových polích na stránce vyžadovat hodnoty.
- Vložte do kódu test, aby byly informace o videu přidány do databáze pouze v případě, že vše ověřuje správně.
- Přidejte kód do značky pro zobrazení chybových zpráv.

V bloku kódu na stránce *AddMovie* vpravo nahoře před deklaracemi proměnné přidejte následující kód:

[!code-csharp[Main](entering-data/samples/sample7.cs)]

Zavoláte `Validation.RequireField` jednou pro každé pole (`<input>` element), kde chcete vyžadovat zadání. Můžete také přidat vlastní chybovou zprávu pro každé volání, jako tady vidíte. (Tyto zprávy jsme rozlišili tak, aby ukázaly, že zde můžete nic dělat.)

Pokud dojde k potížím, chcete zabránit vložení nových informací o videu do databáze. V bloku `if(IsPost)` použijte `&&` (Logical AND) k přidání další podmínky, která testuje `Validation.IsValid()`. Až skončíte, celý `if(IsPost)` blok vypadá jako tento kód:

[!code-csharp[Main](entering-data/samples/sample8.cs)]

Pokud dojde k chybě ověřování u libovolného pole, které jste zaregistrovali pomocí pomocné rutiny `Validation`, vrátí metoda `Validation.IsValid` hodnotu false. A v takovém případě žádný kód v tomto bloku nebude spuštěn, takže do databáze nebudou vloženy žádné neplatné záznamy filmů. A samozřejmě nejste přesměrováni na stránku *filmy* .

Kompletní blok kódu, včetně ověřovacího kódu, teď vypadá jako v tomto příkladu:

[!code-cshtml[Main](entering-data/samples/sample9.cshtml?highlight=10)]

## <a name="displaying-validation-errors"></a>Zobrazení chyb ověřování

Posledním krokem je zobrazení všech chybových zpráv. Můžete zobrazit jednotlivé zprávy pro každou chybu ověřování, nebo můžete zobrazit souhrn nebo obojí. V tomto kurzu provedete obojí, abyste viděli, jak funguje.

Vedle každého prvku `<input>`, který ověřujete, zavolejte metodu `Html.ValidationMessage` a předejte jí název `<input>`ho prvku, který ověřujete. Metodu `Html.ValidationMessage` vložíte přímo tam, kde chcete, aby se zobrazila chybová zpráva. Při spuštění stránky vykreslí metoda `Html.ValidationMessage` `<span>` elementu, kde se zobrazí chyba ověřování. (Pokud není k dispozici žádná chyba, element `<span>` je vykreslen, ale v něm není žádný text.)

Změňte značku na stránce tak, aby obsahovala metodu `Html.ValidationMessage` pro každý ze tří `<input>` prvků na stránce, jako v tomto příkladu:

[!code-cshtml[Main](entering-data/samples/sample10.cshtml?highlight=3,8,13)]

Chcete-li zjistit, jak souhrn funguje, přidejte také následující značku a kód hned za `<h1>Add a Movie</h1>` element na stránce:

[!code-cshtml[Main](entering-data/samples/sample11.cshtml)]

Ve výchozím nastavení metoda `Html.ValidationSummary` zobrazuje všechny zprávy o ověřování v seznamu (`<ul>` element, který je uvnitř elementu `<div>`). Stejně jako u metody `Html.ValidationMessage` se kód pro Shrnutí ověření vždy vykreslí; Pokud nejsou žádné chyby, nejsou vykresleny žádné položky seznamu.

Souhrn může být alternativní způsob, jak zobrazit ověřovací zprávy místo pomocí metody `Html.ValidationMessage` k zobrazení každé chyby specifické pro každé pole. Můžete také použít souhrn i podrobnosti. Nebo můžete použít metodu `Html.ValidationSummary` k zobrazení obecné chyby a potom použít jednotlivá volání `Html.ValidationMessage` k zobrazení podrobností.

Stránka dokončení teď vypadá jako v tomto příkladu:

[!code-cshtml[Main](entering-data/samples/sample12.cshtml)]

A to je vše. Nyní můžete stránku otestovat přidáním videa, ale ponechání jednoho nebo více polí. Když to uděláte, zobrazí se následující chybová zpráva:

![Přidat stránku videa zobrazující chybové zprávy ověřování](entering-data/_static/image5.png)

## <a name="styling-the-validation-error-messages"></a>Určení stylu chybových zpráv ověřování

Vidíte, že se zobrazují chybové zprávy, ale ve skutečnosti se neukládají velmi dobře. K dispozici je jednoduchý způsob, jak tyto chybové zprávy naformátovat, ale.

Chcete-li naformátovat jednotlivé chybové zprávy, které jsou zobrazeny `Html.ValidationMessage`, vytvořte třídu stylu CSS s názvem `field-validation-error`. Chcete-li definovat hledání souhrnu ověření, vytvořte třídu stylu CSS s názvem `validation-summary-errors`.

Chcete-li zjistit, jak tento postup funguje, přidejte prvek `<style>` do části `<head>` stránky. Pak definujte třídy stylů s názvem `field-validation-error` a `validation-summary-errors`, které obsahují následující pravidla:

[!code-cshtml[Main](entering-data/samples/sample13.cshtml?highlight=4-17)]

Normálně byste pravděpodobně umístili informace o stylu do samostatného souboru *. CSS* , ale pro zjednodušení můžete je umístit na stránku. (Později v tomto kurzu nastavíte pravidla šablony stylů CSS do samostatného souboru *. CSS* .)

Pokud dojde k chybě ověřování, metoda `Html.ValidationMessage` vykreslí `<span>` prvek, který obsahuje `class="field-validation-error"`. Přidáním definice stylu pro tuto třídu můžete nakonfigurovat, jak bude zpráva vypadat. Pokud dojde k chybám, metoda `ValidationSummary` podobně dynamicky vykresluje `class="validation-summary-errors"`atributu.

Spusťte znovu stránku a záměrně ponechte několik polí. Chyby jsou nyní mnohem patrné. (Ve skutečnosti se overdone, ale to je jenom k tomu, abyste viděli, co můžete dělat.)

![Přidat stránku videa ukazující chyby ověřování, které byly ve stylu](entering-data/_static/image6.png)

## <a name="adding-a-link-to-the-movies-page"></a>Přidání odkazu na stránku filmů

Prvním krokem je to, aby bylo možné se dostat na stránku *AddMovie* z původního seznamu filmů.

Otevřete stránku *filmy* znovu. Po uzavírací značce `</div>`, která následuje po `WebGrid` pomocné rutiny, přidejte následující kód:

[!code-cshtml[Main](entering-data/samples/sample14.cshtml)]

Jak jste viděli dřív, ASP.NET interpretuje operátor `~` jako kořen webu. Nemusíte používat operátor `~`; můžete použít `<a href="./AddMovie">Add a movie</a>` značek nebo nějaký jiný způsob, jak definovat cestu, kterou jazyk HTML rozumí. Ale operátor `~` je dobrým obecným přístupem při vytváření odkazů na stránky Razor, protože je web flexibilnější – Pokud přesunete aktuální stránku do podsložky, bude odkaz pořád přejít na stránku *AddMovie* . (Nezapomeňte, že operátor `~` funguje pouze na stránkách *. cshtml* . ASP.NET je srozumitelná, ale nejedná se o standardní HTML.)

Až skončíte, spusťte stránku *filmy* . Bude vypadat jako na této stránce:

![Stránka filmy s odkazem na stránku přidat filmy](entering-data/_static/image7.png)

Klikněte na odkaz **Přidat film** , abyste se ujistili, že přejde na stránku *AddMovie* .

## <a name="coming-up-next"></a>Připravujeme další

V dalším kurzu se dozvíte, jak umožnit uživatelům upravovat data, která už jsou v databázi.

## <a name="complete-listing-for-addmovie-page"></a>Úplný výpis pro stránku AddMovie

[!code-cshtml[Main](entering-data/samples/sample15.cshtml)]

## <a name="additional-resources"></a>Další prostředky

- [Seznámení s ASP.NET webovým programováním pomocí syntaxe Razor](https://go.microsoft.com/fwlink/?LinkID=202890)
- [Příkaz SQL INSERT INTO](http://www.w3schools.com/sql/sql_insert.asp) na webu w3schools
- [Ověřování vstupu uživatele na webech webových stránek ASP.NET](https://go.microsoft.com/fwlink/?LinkId=253002). Další informace o práci s pomocníkem `Validation`.

> [!div class="step-by-step"]
> [Předchozí](form-basics.md)
> [Další](updating-data.md)

---
uid: single-page-application/overview/introduction/knockoutjs-template
title: 'Jedna stránka aplikace: KnockoutJS šablona | Microsoft Docs'
author: MikeWasson
description: Vyseknutí šablony
ms.author: riande
ms.date: 01/30/2013
ms.assetid: f9c07af0-4b20-4b08-af8f-47fc3df169a2
msc.legacyurl: /single-page-application/overview/introduction/knockoutjs-template
msc.type: authoredcontent
ms.openlocfilehash: 3a551db1caa9636eb7f2e04c287d3ef371263584
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578692"
---
# <a name="single-page-application-knockoutjs-template"></a>Jednostránková aplikace: šablona KnockoutJS

o [Jan Wasson](https://github.com/MikeWasson)

> Vyseknutí šablony MVC je součástí ASP.NET and Web Tools 2012,2
> 
> [Stáhnout ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=282650)

Aktualizace ASP.NET and Web Tools 2012,2 obsahuje šablonu s jednou stránkou aplikace (SPA) pro ASP.NET MVC 4. Tato šablona je navržená tak, aby vám mohla rychle začít vytvářet interaktivní webové aplikace na straně klienta.

Jednostránkové aplikace (SPA) je obecný termín pro webovou aplikaci, která načte jednu stránku HTML a pak dynamicky aktualizuje stránku místo načtení nových stránek. Po počátečním načtení stránky mluví zabezpečené připojení k serveru přes požadavky AJAX.

![](knockoutjs-template/_static/image1.png)

AJAX není nic nového, ale dnes existuje rozhraní JavaScript, které usnadňuje sestavování a údržbu rozsáhlých propracovaných aplikací s SPA. Také HTML 5 a CSS3 usnadňují vytváření bohatých uživatelská rozhraní.

Aby bylo možné začít, šablona SPA vytvoří ukázku aplikace "seznam úkolů". V tomto kurzu budeme pořizovat Průvodce šablonou. Nejdřív se podíváme na samotnou aplikaci seznamu úkolů a potom zkontrolujte, jaké části technologie budou fungovat.

## <a name="create-a-new-spa-template-project"></a>Vytvoření nového projektu šablony pro SPA

Požadavky:

- Visual Studio 2012 nebo Visual Studio Express 2012 pro web
- Aktualizace ASP.NET Web Tools 2012,2 Update. Aktualizaci můžete nainstalovat [tady](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=ASPDOTNETandWebTools2012_2).

Spusťte Visual Studio a na úvodní stránce vyberte **Nový projekt** . Nebo v nabídce **soubor** vyberte **Nový** a pak **projekt**.

V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte uzel  **C# vizuál** . V **části C#vizuál** vyberte **Web**. V seznamu šablon projektu vyberte **ASP.NET webová aplikace MVC 4**. Pojmenujte projekt a klikněte na tlačítko **OK**.

![](knockoutjs-template/_static/image2.png)

V průvodci **vytvořením nového projektu** vyberte možnost **aplikace s jednoduchou stránkou**.

![](knockoutjs-template/_static/image3.png)

Stisknutím klávesy F5 aplikaci sestavíte a spustíte. Při prvním spuštění aplikace se zobrazí přihlašovací obrazovka.

![](knockoutjs-template/_static/image4.png)

Klikněte na odkaz &quot;zaregistrovat&quot; a vytvořte nového uživatele.

![](knockoutjs-template/_static/image5.png)

Po přihlášení aplikace vytvoří výchozí seznam úkolů se dvěma položkami. Kliknutím na Přidat seznam TODO můžete přidat nový seznam.

![](knockoutjs-template/_static/image6.png)

Přejmenujte seznam, přidejte položky do seznamu a zrušte zaškrtnutí. Můžete také odstranit položky nebo odstranit celý seznam. Změny se automaticky uchovávají v databázi na serveru (ve skutečnosti se v tomto okamžiku LocalDB, protože spouštíte aplikaci místně).

![](knockoutjs-template/_static/image7.png)

## <a name="architecture-of-the-spa-template"></a>Architektura šablony SPA

Tento diagram znázorňuje hlavní stavební kameny pro aplikaci.

![](knockoutjs-template/_static/image8.png)

ASP.NET MVC na straně serveru slouží jako HTML a také zpracovává ověřování na základě formulářů.

Webové rozhraní API ASP.NET zpracovává všechny požadavky, které se týkají ToDoLists a ToDoItems, včetně získání, vytvoření, aktualizace a odstranění. Klient vyměňuje data s webovým rozhraním API ve formátu JSON.

Entity Framework (EF) je vrstva O/RM. Mezi objektem orientovaným světem ASP.NET a podkladovou databází je vypravuje. Databáze používá LocalDB, ale můžete ji změnit v souboru Web. config. Obvykle byste používali LocalDB pro místní vývoj a pak na server nasadili SQL Database na serveru pomocí migrace kódu EF First.

Na straně klienta zpracovává knihovna vyseknutí. js aktualizace stránky od požadavků AJAX. Vyseknutí používá datovou vazbu k synchronizaci stránky s nejnovějšími daty. Tímto způsobem nemusíte psát žádný kód, který projde daty JSON a aktualizuje DOM. Místo toho vložíte do kódu HTML deklarativní atributy, které oznamují, jak prezentovat data.

Velkou výhodou této architektury je, že odděluje prezentační vrstvu od aplikační logiky. Můžete vytvořit část webového rozhraní API, aniž byste věděli, jak bude vaše webová stránka vypadat. Na straně klienta vytvoříte "model zobrazení", který bude představovat tato data, a model zobrazení používá vykrojení k vytvoření vazby na kód HTML. To vám umožní snadno změnit kód HTML beze změny modelu zobrazení. (Později se podíváme na trochu vyseknutí.)

## <a name="models"></a>Modely

V projektu sady Visual Studio obsahuje složka modely modely, které se používají na straně serveru. (Existují i modely na straně klienta; budeme se k nim dostat.)

![](knockoutjs-template/_static/image9.png)

**TodoItem, TodoList**

Jedná se o databázové modely pro Entity Framework Code First. Všimněte si, že tyto modely mají vlastnosti, které ukazují na sebe navzájem. `ToDoList` obsahuje kolekci ToDoItems a každý `ToDoItem` má odkaz zpátky na svůj nadřazený ToDoList. Tyto vlastnosti se nazývají navigační vlastnosti a představují vztah 1: n a seznam úkolů a jejich položky úkolů.

Třída `ToDoItem` také používá atribut **[klíč ForeignKey]** k určení toho, že `ToDoListId` je cizí klíč do tabulky `ToDoList`. To oznamuje EF, aby do databáze přidalo omezení cizího klíče.

[!code-csharp[Main](knockoutjs-template/samples/sample1.cs)]

**TodoItemDto, TodoListDto**

Tyto třídy definují data, která budou odeslána klientovi. "DTO" představuje "objekt přenosu dat". DTO definuje, jak budou entity serializovány do formátu JSON. Obecně je k dispozici několik důvodů použití DTO:

- Chcete-li řídit, které vlastnosti jsou serializovány. DTO může obsahovat podmnožinu vlastností z doménového modelu. Můžete to udělat z důvodů zabezpečení (pro skrytí citlivých dat) nebo jednoduše ke snížení množství dat, která odesíláte.
- Chcete-li změnit tvar dat, například pro sloučení složitější datové struktury.
- Aby se zajistila jakákoli obchodní logika z DTO (oddělení obav).
- Pokud vaše doménové modely nelze z nějakého důvodu serializovat. Například cyklické odkazy mohou způsobit problémy při serializaci objektu. Existují způsoby, jak tento problém zpracovat ve webovém rozhraní API (viz [zpracování cyklických odkazů na objekty](../../../web-api/overview/formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)); ale použití DTO jednoduše zabrání problému zcela.

V šabloně SPA obsahuje DTO stejná data jako doménové modely. Jsou však stále užitečné, protože zabraňují cyklickým odkazům z navigačních vlastností a ukazují obecný vzor DTO.

**AccountModels.cs**

Tento soubor obsahuje modely pro členství v lokalitě. Třída `UserProfile` definuje schéma pro profily uživatelů v databázi členství. (V tomto případě jsou jediným údajem ID uživatele a uživatelské jméno.) Jiné třídy modelu v tomto souboru slouží k vytvoření registračních formulářů uživatelů a přihlášení.

## <a name="entity-framework"></a>Entity Framework

Šablona SPA používá Code First EF. Při vývoji Code First nadefinujete modely nejprve v kódu a pak EF používá model k vytvoření databáze. EF můžete použít také pro existující databázi ([Database First](https://msdn.microsoft.com/data/jj206878.aspx)).

Třída `TodoItemContext` ve složce modely je odvozena od **DbContext**. Tato třída poskytuje "připevnit" mezi modely a EF. `TodoItemContext` obsahuje kolekci `ToDoItem` a kolekci `TodoList`. K dotazování databáze stačí napsat dotaz LINQ na tyto kolekce. Tady je příklad, jak můžete vybrat všechny seznamy úkolů pro uživatele "Alice":

[!code-csharp[Main](knockoutjs-template/samples/sample2.cs)]

Můžete také přidat nové položky do kolekce, aktualizovat položky nebo odstranit položky z kolekce a zachovat změny v databázi.

## <a name="aspnet-web-api-controllers"></a>Řadiče webového rozhraní API ASP.NET

Ve webovém rozhraní API ASP.NET jsou řadiče objekty, které zpracovávají požadavky HTTP. Jak už bylo zmíněno, šablona SPA používá webové rozhraní API k povolení operací CRUD pro instance `ToDoList` a `ToDoItem`. Řadiče se nacházejí ve složce Controllers v řešení.

![](knockoutjs-template/_static/image10.png)

- `TodoController`: zpracovává požadavky HTTP na položky úkolů.
- `TodoListController`: zpracovává požadavky HTTP pro seznamy úkolů.

Tyto názvy jsou významné, protože webové rozhraní API odpovídá cestě identifikátoru URI k názvu kontroleru. (Informace o tom, jak webové rozhraní API směruje požadavky HTTP na řadiče, najdete v tématu [směrování ve webovém rozhraní api ASP.NET](../../../web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api.md).)

Pojďme se podívat na třídu `ToDoListController`. Obsahuje jeden datový člen:

[!code-csharp[Main](knockoutjs-template/samples/sample3.cs)]

`TodoItemContext` slouží ke komunikaci s EF, jak je popsáno výše. Metody na kontroleru implementují operace CRUD. Webové rozhraní API mapuje požadavky HTTP z klienta na metody kontroleru následujícím způsobem:

| Požadavek HTTP | Metoda kontroleru | Popis |
| --- | --- | --- |
| ZÍSKAT /api/todo | `GetTodoLists` | Získá kolekci seznamů úkolů. |
| ZÍSKAT*ID* /API/todo/ | `GetTodoList` | Získá seznam úkolů podle ID. |
| VLOŽIT*ID* /API/todo/ | `PutTodoList` | Aktualizuje seznam úkolů. |
| Publikovat/api/todo | `PostTodoList` | Vytvoří nový seznam úkolů. |
| Odstranit*ID* /API/todo/ | `DeleteTodoList` | Odstraní seznam TODO. |

Všimněte si, že identifikátory URI pro některé operace obsahují zástupné symboly pro hodnotu ID. Chcete-li například odstranit seznam na základě ID 42, je identifikátor URI `/api/todo/42`.

Další informace o používání webového rozhraní API pro operace CRUD najdete v tématu [Vytvoření webového rozhraní API, které podporuje operace CRUD](../../../web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations.md). Kód pro tento kontroler je poměrně jednoduchý. Tady je několik zajímavých bodů:

- Metoda `GetTodoLists` používá dotaz LINQ k filtrování výsledků podle ID přihlášeného uživatele. Tímto způsobem uživatel uvidí jenom data, která mu patří. Všimněte si také, že příkaz SELECT slouží k převodu instancí `ToDoList` na instance `TodoListDto`.
- Metody PUT a POST kontrolují stav modelu před úpravou databáze. Pokud je **ModelState. IsValid** false, tyto metody vrátí HTTP 400, chybný požadavek. Přečtěte si další informace o ověřování modelu ve webovém rozhraní API při [ověřování modelu](../../../web-api/overview/formats-and-model-binding/model-validation-in-aspnet-web-api.md).
- Třída Controller je také upravena atributem **[autorizovat]** . Tento atribut kontroluje, jestli je požadavek HTTP ověřený. Pokud žádost není ověřena, klient obdrží HTTP 401, Neautorizováno. Přečtěte si další informace o ověřování při [ověřování a autorizaci ve webovém rozhraní API ASP.NET](../../../web-api/overview/security/authentication-and-authorization-in-aspnet-web-api.md).

Třída `TodoController` je velmi podobná `TodoListController`. Největší rozdíl spočívá v tom, že nedefinuje žádné metody GET, protože klient obdrží položky úkolů spolu s každým seznamem úkolů.

## <a name="mvc-controllers-and-views"></a>Řadiče a zobrazení MVC

Řadiče MVC jsou také umístěny ve složce Controllers v řešení. `HomeController` vykreslí hlavní HTML pro aplikaci. Zobrazení pro domovský kontroler je definováno v zobrazeních/Home/index. cshtml. V zobrazení domů se v závislosti na tom, jestli je uživatel přihlášený, vykreslí jiný obsah:

[!code-cshtml[Main](knockoutjs-template/samples/sample4.cshtml)]

Když jsou uživatelé přihlášení, uvidí hlavní uživatelské rozhraní. V opačném případě se zobrazí panel přihlášení. Všimněte si, že toto podmíněné vykreslování se stane na straně serveru. Nikdy nedoporučujeme skrývat citlivý obsah na straně&#8212;klienta cokoli, co pošlete v odpovědi HTTP, je viditelné někomu, kdo sleduje nezpracované zprávy HTTP.

## <a name="client-side-javascript-and-knockoutjs"></a>JavaScript na straně klienta a vyseknutí. js

Nyní se z aplikace na straně serveru zapíná na klienta. Šablona SPA používá kombinaci jQuery a vykrojení. js k vytvoření hladkého interaktivního uživatelského rozhraní. Vykrojení. js je knihovna JavaScriptu, která usnadňuje svázání HTML s daty. Metoda vykrojení. js používá vzor nazvaný "Model-View-ViewModel".

- Model je doménová data (seznam úkolů a položky ToDo).
- Zobrazení je dokument HTML.
- Model zobrazení je JavaScriptový objekt, který uchovává data modelu. Model zobrazení je abstrakcí kódu uživatelského rozhraní. Neobsahuje žádné znalosti reprezentace HTML. Místo toho představuje abstraktní funkce zobrazení, jako je například seznam položek ToDo.

Zobrazení je vázáno na data na model zobrazení. Aktualizace zobrazení – model se automaticky projeví v zobrazení. Vazby fungují i v druhém směru. Události v modelu DOM (například kliknutí) jsou vázány na data pro funkce v modelu zobrazení, které spouštějí volání jazyka AJAX.

Šablona zabezpečeného hesla uspořádá JavaScript na straně klienta do tří vrstev:

- todo. DataContext. js: odesílá požadavky AJAX.
- todo. model. js: definuje modely.
- todo. ViewModel. js: definuje model zobrazení.

![](knockoutjs-template/_static/image11.png)

Tyto soubory skriptu se nacházejí ve složce Scripts/App v řešení.

![](knockoutjs-template/_static/image12.png)

**todo. DataContext** zpracovává všechna volání AJAX do řadičů webového rozhraní API. (Volání AJAX pro přihlášení jsou definována jinde, v ajaxlogin. js.)

**todo. model. js** definuje modely na straně klienta (prohlížeč) pro seznamy úkolů. Existují dvě třídy modelů: todoItem a todoList.

Mnohé z vlastností v třídách modelu jsou typu "Ko. pozorovatelný". Observables je způsob, jakým má vyseknutí svůj Magic. Z [dokumentace vyseknutí](http://knockoutjs.com/documentation/introduction.html): pozorovatelný je objekt JavaScriptu, který může upozornit předplatitele na změny. Když je hodnota pozorovatelných změn, vyseknutí aktualizuje všechny prvky HTML, které jsou vázány na tyto observables. Například todoItem má observables pro název a vlastnosti vlastnosti:

[!code-javascript[Main](knockoutjs-template/samples/sample5.js)]

Můžete se také přihlásit k odběru pozorovatele v kódu. Například třída todoItem se přihlašuje ke změnám ve vlastnostech "dokončí" a "title":

[!code-javascript[Main](knockoutjs-template/samples/sample6.js)]

**Zobrazit model**

Model zobrazení je definován v todo. ViewModel. js. Model zobrazení je centrální bod, ve kterém aplikace váže prvky stránky HTML k datům domény. V šabloně protokolu SPA obsahuje model zobrazení pozorovatelný pole todoLists. Následující kód v modelu zobrazení oznamuje vykrojení použití vazby:

[!code-javascript[Main](knockoutjs-template/samples/sample7.js)]

## <a name="html-and-data-binding"></a>HTML a datové vazby

Hlavní HTML pro stránku je definováno v zobrazeních/Home/index. cshtml. Vzhledem k tomu, že používáme datovou vazbu, je kód HTML pouze šablonou pro to, co se skutečně vykresluje. Vykrojení používá *deklarativní* vazby. Prvky stránky můžete navazovat na data přidáním atributu "data-bind" do elementu. Tady je jednoduchý příklad, který je pořízený z dokumentace vyseknutí:

[!code-html[Main](knockoutjs-template/samples/sample8.html)]

V tomto příkladu vyseknutí aktualizuje obsah **&lt;rozpětí&gt;** elementu s hodnotou `myItems.count()`. Pokaždé, když se tato hodnota změní, vyseknutí aktualizuje dokument.

Vykrojení poskytuje řadu různých typů vazeb. Tady jsou některé z vazeb použitých v šabloně SPA:

- **foreach**: umožňuje iterovat smyčku a použít stejný kód pro každou položku v seznamu. Slouží k vykreslení seznamů úkolů a položek úkolů. V rámci **foreach**jsou vazby aplikovány na prvky seznamu.
- **Visible**: používá se pro přepínání viditelnosti. Skryje značky, když je kolekce prázdná, nebo se zobrazí chybová zpráva.
- **Value**: slouží k naplnění hodnot formuláře.
- **klikněte na**: váže událost Click k funkci v modelu zobrazení.

## <a name="anti-csrf-protection"></a>Ochrana proti CSRF

Padělání žádostí mezi weby (CSRF) je útok, kdy škodlivý web pošle požadavek na ohrožený web, ve kterém je aktuálně přihlášený uživatel. Aby se zabránilo útokům CSRF, používá ASP.NET MVC *tokeny proti padělání*, označované také jako ověřovací tokeny žádostí. Nápad je, že server vloží náhodně vygenerovaný token do webové stránky. Když klient odešle data na server, musí tuto hodnotu zahrnout do zprávy požadavku.

Tokeny ochrany proti padělání fungují, protože škodlivá stránka nemůže číst tokeny uživatele z důvodu zásad stejného původu. (Zásady se stejným zdrojem brání tomu, aby se dokumenty hostované na dvou různých webech lišily k obsahu.)

ASP.NET MVC nabízí integrovanou podporu pro tokeny proti padělání prostřednictvím třídy ochrany proti [padělání](https://msdn.microsoft.com/library/system.web.helpers.antiforgery.aspx) a atributu [[ValidateAntiForgeryToken]](https://msdn.microsoft.com/library/system.web.mvc.validateantiforgerytokenattribute.aspx) . V současné době tato funkce není integrována do webového rozhraní API. Šablona SPA ale obsahuje vlastní implementaci webového rozhraní API. Tento kód je definován ve třídě `ValidateHttpAntiForgeryTokenAttribute`, která je umístěna ve složce filtry řešení. Další informace o službě anti-CSRF ve webovém rozhraní API najdete v tématu [prevence útoků prostřednictvím CSRF (pro falšování požadavků mezi lokalitami)](../../../web-api/overview/security/preventing-cross-site-request-forgery-csrf-attacks.md).

## <a name="conclusion"></a>Závěr

Šablona zabezpečeného hesla je navržená tak, aby vám mohla rychle začít psát moderní interaktivní webové aplikace. Používá knihovnu vykrojení. js k oddělení prezentace (značky HTML) z logiky dat a aplikací. Ale vykrojení není jedinou knihovnou JavaScriptu, kterou můžete použít k vytvoření zabezpečeného hesla. Pokud chcete prozkoumat některé další možnosti, podívejte se na [šablony pro Spa vytvořené komunitou](../templates/index.md).

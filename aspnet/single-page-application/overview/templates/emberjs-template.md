---
uid: single-page-application/overview/templates/emberjs-template
title: Šablona EmberJS | Microsoft Docs
author: xqiu
description: Šablona EmberJS
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 04d5f142-5f62-494a-b5ea-4f3d068d34cb
msc.legacyurl: /single-page-application/overview/templates/emberjs-template
msc.type: authoredcontent
ms.openlocfilehash: 1aefa46dd0841b1b06675409cc8a09f9a218d7ac
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578503"
---
# <a name="emberjs-template"></a>Šablona EmberJS

od [Xinyang Qiu](https://github.com/xqiu)

> Šablona EmberJS MVC je zapsána Nathan Totten, Thiago Santos a Xinyang Qiu.
> 
> [Stažení šablony EmberJS MVC](https://go.microsoft.com/fwlink/?LinkId=282647)

Šablona EmberJS SPA je navržená tak, aby vám mohla rychle začít vytvářet interaktivní webové aplikace na straně klienta pomocí EmberJS.

Jednostránkové aplikace (SPA) je obecný termín pro webovou aplikaci, která načte jednu stránku HTML a pak dynamicky aktualizuje stránku místo načtení nových stránek. Po počátečním načtení stránky mluví zabezpečené připojení k serveru přes požadavky AJAX.

![](emberjs-template/_static/image1.png)

AJAX není nic nového, ale dnes existuje rozhraní JavaScript, které usnadňuje sestavování a údržbu rozsáhlých propracovaných aplikací s SPA. Také HTML 5 a CSS3 usnadňují vytváření bohatých uživatelská rozhraní.

Šablona EmberJS SPA používá knihovnu JavaScript [života](http://emberjs.com/) ke zpracování aktualizací stránky od požadavků AJAX. Života. js používá datovou vazbu k synchronizaci stránky s nejnovějšími daty. Tímto způsobem nemusíte psát žádný kód, který projde daty JSON a aktualizuje DOM. Místo toho umístíte deklarativní atributy do kódu HTML, které sděluje života. js, jak prezentovat data.

Na straně serveru je šablona EmberJS skoro shodná se [šablonou KNOCKOUTJS Spa](../introduction/knockoutjs-template.md). Používá ASP.NET MVC k poskytování dokumentů HTML a webové rozhraní API ASP.NET pro zpracování požadavků AJAX od klienta. Další informace o těchto aspektech šablony najdete v dokumentaci k [šabloně KnockoutJS](../introduction/knockoutjs-template.md) . Toto téma se zaměřuje na rozdíly mezi šablonou vyseknutí a šablonou EmberJS.

## <a name="create-an-emberjs-spa-template-project"></a>Vytvoření projektu šablony EmberJS SPA

Stáhněte a nainstalujte šablonu kliknutím na tlačítko Stáhnout výše. Možná budete muset restartovat Visual Studio.

V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte uzel  **C# vizuál** . V **části C#vizuál** vyberte **Web**. V seznamu šablon projektu vyberte **ASP.NET webová aplikace MVC 4**. Pojmenujte projekt a klikněte na tlačítko **OK**.

![](emberjs-template/_static/image2.png)

V průvodci **vytvořením nového projektu** vyberte **projekt života. js Spa**.

![](emberjs-template/_static/image4.png)

## <a name="emberjs-spa-template-overview"></a>Přehled šablony EmberJS SPA

Šablona EmberJS používá kombinaci jQuery, života. js, handlebars. js k vytvoření hladkého interaktivního uživatelského rozhraní.

Života. js je knihovna JavaScriptu, která používá model MVC na straně klienta.

- *Šablona*napsaná v jazyce handlebars šablonování popisuje uživatelské rozhraní aplikace. V režimu vydání se [kompilátor handlebars](https://github.com/Myslik/csharp-ember-handlebars) používá k vytvoření balíčku a zkompilování šablony handlebars.
- *Model* ukládá data aplikace, která získá ze serveru (seznamy úkolů a položky ToDo).
- *Kontrolér* ukládá stav aplikace. Řadiče často prezentují data modelu do odpovídajících šablon.
- *Zobrazení* překládá primitivní události z aplikace a předá je řadiči.
- *Směrovač* spravuje stav aplikace a udržuje synchronizaci adres URL a šablon.

Kromě toho je možné pomocí knihovny dat života synchronizovat objekty JSON (získané ze serveru prostřednictvím rozhraní RESTful API) a modely klientů.

Šablona EmberJS SPA uspořádá skripty do osmi vrstev:

- WebApi\_Adapter. js, WebApi\_serializátor. js: rozšiřuje knihovnu dat života pro práci s webovým rozhraním API ASP.NET.
- Skripty/pomocníky. js: definuje nové Handlebarsy pomocníka pro života.
- Skripty/App. js: Vytvoří aplikaci a nakonfiguruje adaptér a serializátor.
- Skripty/aplikace/modely/\*. js: definuje modely.
- Skripty/aplikace/zobrazení/\*. js: definuje zobrazení.
- Skripty/aplikace/řadiče/\*. js: definuje řadiče.
- Skripty, aplikace/trasy, skripty/aplikace/směrovač. js: definuje trasy.
- Templates/\*. hr: definuje šablony handlebars.

Pojďme se podívat na některé z těchto skriptů podrobněji.

## <a name="models"></a>Modely

Modely jsou definovány ve složce Scripts/app/modely. Existují dva soubory modelů: todoItem. js a todoList. js.

**todo. model. js** definuje modely na straně klienta (prohlížeč) pro seznamy úkolů. Existují dvě třídy modelů: todoItem a todoList. V života jsou modely podtřídy DS. Vzorový. Model může mít vlastnosti s atributy:

[!code-javascript[Main](emberjs-template/samples/sample1.js)]

Modely můžou definovat relace s jinými modely:

[!code-css[Main](emberjs-template/samples/sample2.css)]

Modely mohou mít vypočítané vlastnosti, které se vážou na jiné vlastnosti:

[!code-javascript[Main](emberjs-template/samples/sample3.js)]

Modely mohou mít funkce pozorovatele, které jsou vyvolány při změně pozorované vlastnosti:

[!code-javascript[Main](emberjs-template/samples/sample4.js)]

## <a name="views"></a>Zobrazení

Zobrazení jsou definována ve složce Scripts/app/views. Zobrazení překládá události z uživatelského rozhraní aplikace. Obslužná rutina události může volat zpět do funkcí kontroleru nebo jednoduše volat kontext dat přímo.

Například následující kód je ze zobrazení/TodoItemEditView. js. Definuje zpracování událostí pro vstupní textové pole.

[!code-javascript[Main](emberjs-template/samples/sample5.js)]

## <a name="controller"></a>Kontrolér

Řadiče se definují ve složce Scripts/App/Controllers. Chcete-li reprezentovat jeden model, rozšíří `Ember.ObjectController`:

[!code-javascript[Main](emberjs-template/samples/sample6.js)]

Kontroler může také představovat kolekci modelů rozšířením `Ember.ArrayController`. Například TodoListController představuje pole objektů `todoList`. Kontroler seřadí podle ID todoList v sestupném pořadí:

[!code-javascript[Main](emberjs-template/samples/sample7.js)]

Kontroler definuje funkci s názvem `addTodoList`, která vytvoří novou todoList a přidá ji do pole. Chcete-li zjistit, jakým způsobem bude tato funkce volána, otevřete soubor šablony s názvem todoListTemplate. html ve složce šablony. Následující kód šablony váže tlačítko k funkci `addTodoList`:

[!code-html[Main](emberjs-template/samples/sample8.html)]

Kontroler obsahuje také vlastnost `error`, která obsahuje chybovou zprávu. Zde je kód šablony pro zobrazení chybové zprávy (také v souboru todoListTemplate. html):

[!code-html[Main](emberjs-template/samples/sample9.html)]

## <a name="routes"></a>Trasy

Směrovač. js definuje trasy a výchozí šablonu pro zobrazení, nastavení stavu aplikace a odpovídá adresám URL na trasy:

[!code-javascript[Main](emberjs-template/samples/sample10.js)]

TodoListRoute. js načte data pro TodoListRoute přepsáním funkce setupController:

[!code-javascript[Main](emberjs-template/samples/sample11.js)]

Života používá konvence pojmenování, které odpovídají adresám URL, názvům tras, řadičům a šablonám. Další informace najdete v tématu [http://emberjs.com/guides/routing/defining-your-routes/](http://emberjs.com/guides/routing/defining-your-routes/) v dokumentaci k EmberJS.

## <a name="templates"></a>Šablony

Složka šablony obsahuje čtyři šablony:

- Application. hr: výchozí šablona, která je vykreslena při spuštění aplikace.
- o. hr: Šablona pro trasu "/About".
- index. hr: Šablona pro kořenovou trasu "/".
- todoList. hr: Šablona pro trasu "/todo".
- \_panel. hr: Šablona definuje navigační nabídku.

Šablona aplikace funguje jako stránka předlohy. Obsahuje záhlaví, zápatí a "{{vývod}}" pro vložení dalších šablon v závislosti na trase. Další informace o šablonách aplikací v života naleznete v tématu [http://guides.emberjs.com/v1.10.0/templates/the-application-template//](http://guides.emberjs.com/v1.10.0/templates/the-application-template/).

Šablona "/todoList" obsahuje dva výrazy smyčky. Vnější smyčka je `{{#each controller}}`a uvnitř smyčky je `{{#each todos}}`. Následující kód ukazuje integrované zobrazení `Ember.Checkbox`, přizpůsobený `App.TodoItemEditView`a odkaz s akcí `deleteTodo`.

[!code-html[Main](emberjs-template/samples/sample12.html)]

Třída `HtmlHelperExtensions` definovaná v Controllers/HtmlHelperExtensions. cs definuje pomocnou funkci pro ukládání souborů šablony do mezipaměti a vložení šablon, když je **ladění** v souboru Web. config nastaveno na **hodnotu true** . Tato funkce se volá ze souboru zobrazení ASP.NET MVC definovaného v zobrazeních/domů/App. cshtml:

[!code-cshtml[Main](emberjs-template/samples/sample13.cshtml)]

Volána bez argumentů, funkce vykreslí všechny soubory šablon ve složce Templates. Můžete také zadat podsložku nebo konkrétní soubor šablony.

Je-li v souboru Web. config **hodnota** **Debug** , aplikace obsahuje položku sady prostředků "~/Bundles/templates". Tato položka sady je přidána v BundleConfig.cs pomocí knihovny kompilátoru handlebars:

[!code-csharp[Main](emberjs-template/samples/sample14.cs)]

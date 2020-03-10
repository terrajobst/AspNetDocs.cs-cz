---
uid: single-page-application/overview/templates/backbonejs-template
title: Šablona páteře | Microsoft Docs
author: madskristensen
description: Šablona hesla pro páteřní šablonu. js
ms.author: riande
ms.date: 04/04/2013
ms.assetid: 00aca413-f067-4108-9bd1-cf21e64a2646
msc.legacyurl: /single-page-application/overview/templates/backbonejs-template
msc.type: authoredcontent
ms.openlocfilehash: 7297db7d5b35a53b40f9d9162960e529a167bd12
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558224"
---
# <a name="backbone-template"></a>Šablona Backbone

od [Madse Kristensena](https://github.com/madskristensen)

> Šablona páteřního hesla byla zapsaná pomocí Kazi Manzur Rashid
> 
> [Stažení šablony páteřní soubor. js SPA](https://go.microsoft.com/fwlink/?LinkId=293631)

Šablona s páteřním heslem. js je navržená tak, aby vám mohla rychle začít vytvářet interaktivní webové aplikace na straně klienta pomocí [páteřního. js.](http://backbonejs.org/)

Šablona poskytuje počáteční kostru pro vývoj aplikace v páteřním formátu. js v ASP.NET MVC. Mimo pole poskytuje základní funkce pro přihlášení uživatelů, včetně registrace uživatelů, přihlášení, resetování hesla a potvrzení uživatele se základními e-mailovými šablonami.

Požadavky:

- [Aktualizace ASP.NET and Web Tools 2012,2](https://go.microsoft.com/fwlink/?LinkId=282650)

## <a name="create-a-backbone-template-project"></a>Vytvoření projektu s páteřní šablonou

Stáhněte a nainstalujte šablonu kliknutím na tlačítko Stáhnout výše. Šablona je zabalená jako soubor rozšíření sady Visual Studio (VSIX). Možná budete muset restartovat Visual Studio.

V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte uzel  **C# vizuál** . V **části C#vizuál** vyberte **Web**. V seznamu šablon projektu vyberte **ASP.NET webová aplikace MVC 4**. Pojmenujte projekt a klikněte na tlačítko **OK**.

![](backbonejs-template/_static/image1.png)

V průvodci **vytvořením nového projektu** vyberte projekt páteřní. js Spa.

![](backbonejs-template/_static/image2.png)

Stisknutím kombinace kláves CTRL + F5 sestavíte a spustíte aplikaci bez ladění, nebo stiskněte klávesu F5 ke spuštění s laděním.

![](backbonejs-template/_static/image3.png)

Kliknutím na můj účet se zobrazí přihlašovací stránka:

![](backbonejs-template/_static/image4.png)

## <a name="walkthrough-client-code"></a>Návod: klientský kód

Pojďme začít na straně klienta. Skripty klientské aplikace jsou umístěné ve složce ~/Scripts/Application. Aplikace je zapsána v [TypeScript](http://www.typescriptlang.org/) (soubory. TS), které jsou zkompilovány do jazyka JavaScript (soubory. js).

**Aplikace**

`Application` je definována v Application. TS. Tento objekt Inicializuje aplikaci a funguje jako kořenový obor názvů. Udržuje informace o konfiguraci a stavu, které jsou sdíleny napříč aplikací, například zda je uživatel přihlášený.

Metoda `application.start` vytváří modální zobrazení a připojuje obslužné rutiny událostí pro události na úrovni aplikace, jako je například přihlášení uživatele. V dalším kroku vytvoří výchozí směrovač a zkontroluje, jestli je zadaná adresa URL na straně klienta. V takovém případě přesměruje na výchozí adresu URL (#!/).

**Události**

Při vývoji volně vázaných komponent jsou vždy důležité události. Aplikace často provádějí více operací v reakci na akci uživatele. Páteřní síť poskytuje integrované události s komponentami, jako je model, kolekce a zobrazení. Namísto vytváření vzájemných závislostí mezi těmito součástmi používá šablona "" pub/sub "model: objekt `events` definovaný v události. TS funguje jako centrum událostí pro publikování a přihlášení k odběru událostí aplikace. Objekt `events` je typu singleton. Následující kód ukazuje, jak se přihlásit k odběru události a poté aktivovat událost:

[!code-csharp[Main](backbonejs-template/samples/sample1.cs)]

**Směrovací**

V páteřním. js směrovač poskytuje metody pro směrování stránek na straně klienta a jejich propojení s akcemi a událostmi. Šablona definuje jeden směrovač ve směrovači. TS. Směrovač vytvoří zobrazení activable a udržuje stav při přepínání zobrazení. (Zobrazení Activable jsou popsaná v následující části.) Zpočátku má projekt dvě zástupné zobrazení, domovskou stránku a o produktu. Má také zobrazení NotFound, které se zobrazí, pokud trasa není známá.

**Zobrazení**

Zobrazení jsou definována v ~/scripts/Application/views. Existují dva druhy zobrazení, activable zobrazení a modální zobrazení dialogových oken. Zobrazení Activable je vyvoláno směrovačem. Když se zobrazí zobrazení activable, všechna ostatní zobrazení activable se stanou neaktivní. Chcete-li vytvořit zobrazení activable, rozšíříte zobrazení pomocí objektu `Activable`:

[!code-javascript[Main](backbonejs-template/samples/sample2.js)]

Rozšíření pomocí `Activable` přidá do zobrazení dvě nové metody `activate` a `deactivate`. Směrovač volá tyto metody pro aktivaci a deaktivaci zobrazení.

Modální zobrazení jsou implementována jako modální dialogová okna pro spuštění z [Twitteru](https://twitter.github.com/bootstrap/) . Zobrazení `Membership` a `Profile` jsou modální zobrazení. Zobrazení modelu mohou být vyvolána všemi událostmi aplikace. Například v zobrazení `Navigation` kliknutím na odkaz Můj účet zobrazíte `Membership` zobrazení nebo zobrazení `Profile`, podle toho, jestli je uživatel přihlášený. `Navigation` připojí obslužné rutiny události Click k jakýmkoli podřízeným elementům, které mají atribut `data-command`. Zde je kód HTML:

[!code-html[Main](backbonejs-template/samples/sample3.html)]

Zde je kód v navigaci. TS, aby se události připojily:

[!code-csharp[Main](backbonejs-template/samples/sample4.cs)]

**Vzor**

Modely jsou definované v ~/scripts/Application/Models. Všechny modely mají tři základní věci: výchozí atributy, ověřovací pravidla a koncový bod na straně serveru. Tady je typický příklad:

[!code-javascript[Main](backbonejs-template/samples/sample5.js)]

**Moduly plug-in**

Složka ~/Scripts/Application/lib obsahuje několik užitečných modulů plug-in jQuery. Soubor Form. TS definuje modul plug-in pro práci s daty formuláře. Často potřebujete serializovat nebo deserializovat data formuláře a zobrazit všechny chyby ověřování modelu. Modul plug-in formuláře. TS obsahuje metody, jako jsou `serializeFields`, `deserializeFields`a `showFieldErrors`. Následující příklad ukazuje, jak serializovat formulář do modelu.

[!code-javascript[Main](backbonejs-template/samples/sample6.js)]

Modul plug-in flashbar. TS poskytuje uživatelům různé druhy zpráv zpětné vazby. Metody jsou `$.showSuccessbar`, `$.showErrorbar` a `$.showInfobar`. Na pozadí používá upozornění zaváděcího nástroje Twitter k zobrazení úhledných animovaných zpráv.

Modul plug-in potvrdit. TS nahrazuje dialogové okno pro potvrzení prohlížeče, i když se rozhraní API trochu liší:

[!code-javascript[Main](backbonejs-template/samples/sample7.js)]

## <a name="walkthrough-server-code"></a>Návod: serverový kód

Teď se podíváme na stranu serveru.

**Kontrolery**

V aplikaci s jedinou stránkou přehrává Server v uživatelském rozhraní pouze malou roli. Server obvykle vykreslí počáteční stránku a potom odesílá a přijímá data JSON.

Šablona má dva řadiče MVC: `HomeController` vykreslí úvodní stránku a `SupportsController` slouží k potvrzení nových uživatelských účtů a resetování hesel. Všechny ostatní řadiče v šabloně jsou ASP.NET webovými řadiči rozhraní API, které odesílají a přijímají data JSON. Ve výchozím nastavení používají řadiče novou třídu `WebSecurity` k provádění úloh souvisejících s uživatelem. Mají však také volitelné konstruktory, které umožňují předat delegáty pro tyto úlohy. To usnadňuje testování a umožňuje nahradit `WebSecurity` jiným způsobem pomocí kontejneru IoC. Zde naleznete příklad:

[!code-csharp[Main](backbonejs-template/samples/sample8.cs)]

## <a name="views"></a>Zobrazení

Zobrazení jsou navržena jako modulární: každá část stránky má vlastní vyhrazené zobrazení. V aplikaci s jednou stránkou je běžné zahrnout zobrazení, která nemají odpovídající kontroler. Zobrazení můžete zahrnout voláním `@Html.Partial('myView')`, ale to je zdlouhavé. Aby to bylo snazší, Šablona definuje pomocnou metodu `IncludeClientViews`, která vykresluje všechna zobrazení v zadané složce:

[!code-cshtml[Main](backbonejs-template/samples/sample9.cshtml)]

Pokud není zadán název složky, výchozí název složky je "ClientViews". Pokud vaše zobrazení klienta používá také částečná zobrazení, pojmenujte částečné zobrazení pomocí znaku podtržítka (například `_SignUp`). Metoda `IncludeClientViews` vyloučí všechna zobrazení, jejichž název začíná podtržítkem. Chcete-li zahrnout částečné zobrazení v zobrazení klienta, zavolejte `Html.ClientView('SignUp')` místo `Html.Partial('_SignUp')`.

**Odesílání e-mailů**

K odeslání e-mailu šablona používá [poštovní směrovací číslo](http://aboutcode.net/postal). Poštovní směrovací číslo je však abstraktní ze zbytku kódu s rozhraním `IMailer`, takže jej lze snadno nahradit jinou implementací. Šablony e-mailu se nacházejí ve složce views/Emails. E-mailová adresa odesílatele je zadána v souboru Web. config v `sender.email` klíč oddílu **appSettings** . Kromě toho, když `debug="true"` v souboru Web. config, aplikace nevyžaduje při urychlení vývoje e-mailové potvrzení uživatele.

## <a name="github"></a>GitHub

Můžete také najít šablonu páteřní. js SPA na [GitHubu](https://github.com/kazimanzurrashid/AspNetMvcBackboneJsSpa).

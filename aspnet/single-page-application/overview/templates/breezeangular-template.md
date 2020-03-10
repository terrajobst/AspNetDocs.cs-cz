---
uid: single-page-application/overview/templates/breezeangular-template
title: Breeze/úhlová šablona | Microsoft Docs
author: madskristensen
description: Šablona aplikace Breeze/úhlová jedna stránka
ms.author: riande
ms.date: 03/08/2013
ms.assetid: db31e909-563a-4516-aadd-62aa210ac7e4
msc.legacyurl: /single-page-application/overview/templates/breezeangular-template
msc.type: authoredcontent
ms.openlocfilehash: 3e4e63d385a56d51d3d08696782b43d6228f6201
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578538"
---
# <a name="breezeangular-template"></a>Šablona Breeze/Angular

od [Madse Kristensena](https://github.com/madskristensen)

> Breeze nebo úhlová šablona MVC byla zapsána od společnosti "3. Bell"
> 
> [Stažení šablony Breeze/úhlové MVC](https://go.microsoft.com/fwlink/?LinkId=286437)

[AngularJS](http://angularjs.org) je open source knihovna z Google pro vytváření aplikací s jednou stránkou (jednostránkové). Nabízí datové vazby, vkládání závislostí a správu obrazovky. Zkombinujte se s [BreezeJS](http://www.breezejs.com/?utm_source=ms-spa), jinou otevřenou zdrojovou knihovnou pro modelování dat a správu dat a máte základní komponenty pro skvělou aplikaci klienta HTML/JavaScript.

Šablona Breeze/úhlového hesla je variací [šablony KNOCKOUTJS Spa](../introduction/knockoutjs-template.md) , která je součástí aktualizace ASP.NET and Web Tools 2012,2. Pokud máte Visual Studio, budete mít k dispozici příklad ZABEZPEČENÉho a spuštěného prostředí za méně než 60 sekund.

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningTodoPage.png)

Kromě toho aplikace vypadá velmi podobně jako šablona KnockoutJS SPA. Ale v digestoři je to poměrně jiné. Šablona KnockoutJS používá vykrojení pro datovou vazbu a nezpracovaná AJAX pro přístup k datům. Šablona Breeze/úhlů používá pro datovou vazbu a Breeze pro přístup k datům úhlů. Tyto knihovny umožňují další možnosti, včetně navigace na stránce a historie.

Tady je stránka o aplikaci:

![](http://www.breezejs.com/sites/all/images/spa-template/NgRunningAboutPage.png)

Tato stránka zobrazuje běžící protokol událostí během aktuální uživatelské relace, včetně:

- Přenosu. Poznamenejte si vytvoření kontroleru TODO na #2 a #7.
- Vzdálené dotazy (#3) a dotazy na místní mezipaměť (#7).
- Ukládají se nové entity (#5, #6) a upravené (#4).
- Změny ověřené na klientovi (#9), aby mohl uživatel opravit chyby před potvrzením změn v databázi.

V této šabloně je ještě více prozkoumat, včetně těchto:

- Dynamické načítání šablon zobrazení HTML
- Vlastní datová vazba prostřednictvím úhlových direktiv "
- Modularita a vstřikování závislostí.
- Filtry dotazů, řazení, stránkování, projekce a zahrnutí souvisejících entit.
- Sdílení dat napříč více obrazovkami.
- Uložení více změn v rámci jedné transakce.
- Ověřovací pravidla, která byla automaticky šířena ze serveru do klienta jazyka JavaScript.

Pusťme se do toho.

## <a name="create-a-breezeangular-template-project"></a>Vytvoření projektu šablony Breeze/úhlů

Stáhněte a nainstalujte šablonu kliknutím na tlačítko Stáhnout výše. Šablona je zabalená jako soubor rozšíření sady Visual Studio (VSIX). Možná budete muset restartovat Visual Studio.

V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte uzel  **C# vizuál** . V **části C#vizuál** vyberte **Web**. V seznamu šablon projektu vyberte **ASP.NET webová aplikace MVC 4**. Pojmenujte projekt a klikněte na tlačítko **OK**.

V průvodci **vytvořením nového projektu** vyberte **Breeze úhlové Spa**.

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeNgSpaTemplate.png)

Stisknutím kombinace kláves CTRL + F5 sestavíte a spustíte aplikaci bez ladění, nebo stiskněte klávesu F5 ke spuštění s laděním.

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrLogin.png)

Při prvním spuštění aplikace se zobrazí přihlašovací obrazovka. Klikněte na odkaz Zaregistrovat se a nová stránka se zobrazí v zobrazení, kde můžete zadat uživatelské jméno a heslo. (Stránky pro přihlášení a registraci jsou sestavené pomocí ASP.NET MVC.) Po odeslání registračního formuláře vygeneruje Server TodoList se dvěma položkami pro váš účet. Pak je prezentuje na žluté poznámce.

![](http://www.breezejs.com/sites/all/images/spa-template/TodoList.png)

Teď jste v rámci zabezpečeného hesla. Vše, co vidíte a budete pracovat, když pracujete s todo, se vykresluje a spravuje na klientovi pomocí vyseknutí a Breeze. Prozkoumat aplikaci jako uživatel... ale s očima vývojáře. Pomocí vývojářských nástrojů v prohlížeči Zachyťte síťový provoz. (V Internet Exploreru: stiskněte klávesu F12, vyberte kartu **síť** a klikněte na **Spustit zachytávání**.) Nyní vyzkoušejte následující:

- Přidejte novou položku todo.
- Klikněte na popisek a upravte název položky ToDo.
- Zaškrtnutím políčka označíte, že položka se dokončila. Všimněte si, že je textové pole zakázáno, takže nadpis již není možné upravovat.
- Klikněte na x vpravo od popisku. Položka zmizí a z databáze se odstraní.
- Vyberte jinou položku a vymažte její název. Zobrazí se chyba ověření, že název je povinný. Po krátké pauze se předchozí nadpis obnoví.
- Zadejte absurdně dlouhý nadpis. Obdržíte jinou chybu ověřování, že název je příliš dlouhý.
- Klikněte na tlačítko Přidat seznam todo. Nalevo od předchozího seznamu se zobrazí nový seznam.
- Začněte s názvem TodoList, který aktivuje jeho požadovaná a délková ověření.
- Kliknutím do textového pole název vymažete chybovou zprávu.
- Kliknutím na x v kruhu v pravém horním rohu odstraňte TodoList a jeho todo.
- Kliknutím na odkaz "o" v pravém horním rohu zobrazíte protokol těchto aktivit.

Logika ověřování se provádí pomocí Breeze na straně klienta. Atributy ověřování v třídách model serveru jsou šířeny do klienta a provedeny automaticky před tím, než klient kontaktuje server.

Zkontrolujte síťový provoz. Všimněte si, že na server nebyla žádná volání, když Breeze zjistil chybu. Každá platná změna způsobila požadavek POST na "/api/Todo/SaveChanges". Breeze zařadí změny a pošle je společně jako jeden požadavek do `SaveChanges` metody řadiče webového rozhraní API. To se liší od šablony KnockoutJS SPA, která vytváří požadavky na vložení, odeslání a odstranění každé položky jednotlivě.

Všimněte si také, že při přepínání mezi TodoList a o stránkách nedochází k žádnému síťovému provozu. Důvodem je to, že dotaz byl omezený na místní mezipaměť Breeze.

## <a name="peek-inside"></a>Náhled dovnitř

Tato aplikace má stranu klienta a na straně serveru. Zásobník na straně klienta se skládá z malého formátu HTML a kombinace modulů JavaScript aplikace (ve složce App) a JavaScriptových knihoven třetích stran (ve složce Scripts).

![](http://www.breezejs.com/sites/all/images/spa-template/NgClientArchitecture2.png)

Architektura uživatelského rozhraní odděluje widgety HTML zobrazení z kódu doprovodné prezentace v řadičích. Úhlový systém vázání dat koordinuje zobrazení a řadiče tak, aby každý z nich mohl dělat svou úlohu, aniž by Intimate znalosti druhé.

Kontroler požádá kontext dat o získání a uložení entit modelu. Kontext dat deleguje většinu práce na Breeze, která vytváří objekty modelu sledování samy sebe z výsledků dotazu JSON.

Zásobník na straně serveru se skládá z určitého kódu pro vývojáře a tří principů knihoven .NET: webové rozhraní API, Entity Framework a Breeze.NET:

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

Základní architektura je stejná jako šablona KnockoutJS SPA. Implementace je však mnohem jednodušší: DTO byly odstraněny a většina z Entity Framework podrobností byla delegována na Breeze.NET.

## <a name="next-steps"></a>Další kroky

Doporučujeme, abyste prozkoumali kód a provedli [rozsáhlou diskuzi](http://www.breezejs.com/ng-spa-template?utm_source=ms-spa) o zásobníku klienta i serveru na webu Breeze.

Můžete se pokusit přehrát dotaz Breeze na straně klienta; Přidejte některé filtry a seřadí je. Můžete přidat další vlastnosti modelu a další entity, které vám pomůžou dosáhnout lepšího vývoje pro komplexní vývoj SPA. Když jste si jisti návrhem, můžete funkce TODO odtrhnout a nahradit je vlastními.

Šťastné kódování!

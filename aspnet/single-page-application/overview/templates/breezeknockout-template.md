---
uid: single-page-application/overview/templates/breezeknockout-template
title: Šablona Breeze/vykrojení | Microsoft Docs
author: madskristensen
description: Šablona jedné stránky aplikace Breeze/vykrojení
ms.author: riande
ms.date: 01/30/2013
ms.assetid: 3bd94827-3c59-448f-abc3-36e6df4858db
msc.legacyurl: /single-page-application/overview/templates/breezeknockout-template
msc.type: authoredcontent
ms.openlocfilehash: 5bb9ee8f758a25afa6baf3ccbaf7d5864754c7df
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558189"
---
# <a name="breezeknockout-template"></a>Šablona Breeze/Knockout

od [Madse Kristensena](https://github.com/madskristensen)

> Šablona MVC Breeze/vyseknutí byla zapsána od společnosti "3. Bell"
> 
> [Stáhnout šablonu MVC Breeze/vyseknutí](https://go.microsoft.com/fwlink/?LinkId=282649)

Seznámili jste se s "jednoduchou stránkovou aplikací" (SPA) a přemýšleli, co je. I když se o něm můžete přečtením, měli byste k tomu mít přednost. Ale kdo má čas ke stažení ukázky? Pokud máte aplikaci Visual Studio, budete mít k dispozici příklad ZABEZPEČENÉho a spuštěného prostředí za méně než 60 sekund s šablonou aplikace ASP.NET MVC 4 "Breeze/vykrojení jedné stránky".

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

## <a name="what-is-the-breezeknockout-spa-template"></a>Jaká je šablona hesla Breeze/vykrojení?

Většina šablon projektů generuje kostru aplikace. Do těchto kostí se vloží svalovina přidáním kódu a nakonec doručovat funkční aplikaci. Šablona hesla Breeze/vykrojení se liší. Vygeneruje ukázkovou aplikaci, kterou si můžete prostudovat. Ukazuje návrh aplikace SPA a mnoho technik pro sestavování SPA.

Šablona Breeze/vykrojení je variací [šablony KNOCKOUTJS Spa](../introduction/knockoutjs-template.md) , která je součástí aktualizace ASP.NET and Web Tools 2012,2. Šablona Breeze SPA vygeneruje aplikaci se stejným uživatelským prostředím, ale má odlišnou implementaci pomocí Breeze pro správu dat.

Šablona KnockoutJS SPA vytváří žádosti o služby s nezpracovaným jQuery AJAX, který je vhodný pro jednoduchou aplikaci. Ale propracovanější aplikace mají přísnější požadavky na správu dat. Například většina aplikací:

- Dotazování a opětovné dotazování serveru během uživatelské relace rozšířené.
- Přidejte filtry dotazu, řazení a stránkování.
- Sdílejte stejná data napříč více obrazovkami.
- Nashromáždí změny v mnoha objektech a pak je uložte jako jednu transakci.
- Ověří změny u klienta, aby mohl uživatel opravit chyby před potvrzením změn v databázi.

Knihovna BreezeJS tyto rutinní zpracuje za vás a uvolní vám tak vývoj logiky aplikace a uživatelského prostředí, které záleží nejvíc.

[**Breeze**](http://www.breezejs.com/?utm_source=ms-spa) je open source knihovna pro vytváření bohatých datových aplikací v jazycích JavaScript a HTML, což jsou typy aplikací, které byly historicky doručovány jako samostatné desktopové aplikace.

Šablona Breeze/vykrojení vám pomůže s tím, že se jedná o první zásadní krok k robustnější infrastruktuře správy dat. Vytvoří ukázkovou aplikaci todo, která je umístěná v rámci stejné šablony KnockoutJS SPA. V rámci uvnitř nahrazuje datovou vrstvu AJAX pomocí Breeze, takže můžete porovnat dva přístupy vedle sebe. Samozřejmě se zlomeko, že se dotkne potenciálu aplikace Breeze. Uvidíte ale, jak Breeze funguje a jak malý je nutný k provedení tohoto přechodu.

Pusťme se do toho.

## <a name="create-a-breezeknockout-template-project"></a>Vytvořit projekt šablony Breeze/vykrojení

Stáhněte a nainstalujte šablonu kliknutím na tlačítko Stáhnout výše. Šablona je zabalená jako soubor rozšíření sady Visual Studio (VSIX). Možná budete muset restartovat Visual Studio.

V podokně **šablony** vyberte **Nainstalované šablony** a rozbalte uzel  **C# vizuál** . V **části C#vizuál** vyberte **Web**. V seznamu šablon projektu vyberte **ASP.NET webová aplikace MVC 4**. Pojmenujte projekt a klikněte na tlačítko **OK**.

V průvodci **vytvořením nového projektu** vyberte **Breeze vykrojení Spa**.

![](http://www.breezejs.com/sites/all/images/spa-template/SelectBreezeKOSpaTemplate.png)

Stisknutím kombinace kláves CTRL + F5 sestavíte a spustíte aplikaci bez ladění, nebo stiskněte klávesu F5 ke spuštění s laděním.

![](http://www.breezejs.com/sites/all/images/spa-template/ZephyrRunning.png)

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

Logika ověřování se provádí pomocí Breeze na straně klienta. Atributy ověřování v třídách model serveru jsou šířeny do klienta a provedeny automaticky před tím, než klient kontaktuje server.

Zkontrolujte síťový provoz. Všimněte si, že na server nebyla žádná volání, když Breeze zjistil chybu. Každá platná změna způsobila požadavek POST na "/api/Todo/SaveChanges". Breeze zařadí změny a pošle je společně jako jeden požadavek do `SaveChanges` metody řadiče webového rozhraní API. To se liší od šablony KnockoutJS SPA, která vytváří požadavky na vložení, odeslání a odstranění každé položky jednotlivě.

## <a name="peek-inside"></a>Náhled dovnitř

Tato aplikace má stranu klienta a na straně serveru. Zásobník na straně klienta se skládá z malého formátu HTML a kombinace modulů JavaScript aplikace (ve složce App) a JavaScriptových knihoven třetích stran (ve složce Scripts).

![](http://www.breezejs.com/sites/all/images/spa-template/ClientArchitecture.png)

Pokud jste prozkoumali šablonu KnockoutJS SPA, měla by to vypadat velmi dobře. Zaměřte se na modré čtverečky. Architektura uživatelského rozhraní je model-View-ViewModel (MVVM), ve kterém jsou widgety HTML v zobrazení čistě oddělené od kódu doprovodné prezentace v modelu zobrazení. Systém vázání dat (v tomto případě vykrojení v tomto případě) koordinuje zobrazení a model zobrazení, aby každý z nich mohl dělat svou úlohu, aniž by Intimate znalosti druhého.

Model zapouzdřuje data todo. Entity v modelu jsou konstruovány pomocí Breeze s nečinnými vlastnostmi, takže mohou být vázány přímo na widgety v zobrazení. Model zobrazení požádá kontext dat o získání a uložení entit modelu. Kontext dat deleguje většinu práce na Breeze.

Zásobník na straně serveru se skládá z určitého kódu pro vývojáře a tří principů knihoven .NET: webové rozhraní API, Entity Framework a Breeze.NET:

![](http://www.breezejs.com/sites/all/images/spa-template/ServerArchitecture.png)

Základní architektura je stejná jako šablona KnockoutJS SPA. Implementace je však mnohem jednodušší: DTO byly odstraněny a většina z Entity Framework podrobností byla delegována na Breeze.NET.

## <a name="next-steps"></a>Další kroky

Doporučujeme, abyste prozkoumali kód a provedli [rozsáhlou diskuzi](http://www.breezejs.com/spa-template?utm_source=ms-spa) o zásobníku klienta i serveru na webu Breeze.

Můžete se pokusit přehrát dotaz Breeze na straně klienta; Přidejte některé filtry a seřadí je. Můžete přidat další vlastnosti modelu a další entity, které vám pomůžou dosáhnout lepšího vývoje pro komplexní vývoj SPA. Když jste si jisti návrhem, můžete funkce TODO odtrhnout a nahradit je vlastními.

Brzy budete připraveni na další velký krok: přidání obrazovek na straně klienta a navigace mezi nimi. Tuto šablonu SPA ponecháte za tím, že zapnete podrobnější sadu protokolů SPA, jako je třeba [Jan Papa Hot navrhování ručníků](https://github.com/johnpapa/HotTowel#readme "Horká navrhování ručníků"), který přidá Durandal do kombinace Breeze a vykrojení.

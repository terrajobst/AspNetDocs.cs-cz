---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: 'Část 5: úpravy formulářů a šablonování | Microsoft Docs'
author: jongalloway
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 5 pokrývá úpravy formulářů a šablonování.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: 20b99cbe57b5dfa623205838a5929733a6c2d70d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559547"
---
# <a name="part-5-edit-forms-and-templating"></a>5\. část: Editační formuláře a šablonování textu

o [Jan Galloway](https://github.com/jongalloway)

> Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio pro vývoj webů.  
>   
> Úložiště hudby MVC je zjednodušená ukázka implementace úložiště, která prodává hudební alba online a implementuje základní funkce pro správu webů, přihlašování uživatelů a nákupních košíků.
> 
> V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 5 pokrývá úpravy formulářů a šablonování.

V poslední kapitole jsme načetli data z naší databáze a zobrazili jsme ji. V této kapitole také povolíme úpravy dat.

## <a name="creating-the-storemanagercontroller"></a>Vytváření StoreManagerController

Začneme vytvořením nového kontroleru s názvem **StoreManagerController**. Pro tento kontroler využijeme funkce pro generování uživatelského rozhraní, které jsou k dispozici v aktualizaci nástrojů ASP.NET MVC 3. V dialogovém okně Přidat řadič nastavte možnosti, jak je znázorněno níže.

![](mvc-music-store-part-5/_static/image1.png)

Když kliknete na tlačítko Přidat, uvidíte, že mechanismus generování uživatelského rozhraní ASP.NET MVC 3 má pro vás dobrý objem práce:

- Vytvoří nový StoreManagerController s místní proměnnou Entity Framework.
- Přidá složku StoreManager do složky zobrazení projektu.
- Přidá vytvořit. cshtml, DELETE. cshtml, details. cshtml, Edit. cshtml a index. cshtml, silně typované na třídu alba.

![](mvc-music-store-part-5/_static/image2.png)

Nová třída kontroleru StoreManager zahrnuje operace CRUD (vytvořit, číst, aktualizovat, odstranit), které znají, jak pracovat s třídou modelu alba a použít náš Entity Framework kontext pro přístup k databázi.

## <a name="modifying-a-scaffolded-view"></a>Úprava vygenerovaného zobrazení

Je důležité si uvědomit, že i když byl tento kód vygenerován pro nás, jedná se o standardní ASP.NET kód MVC, stejně jako v průběhu tohoto kurzu. Je vhodné vám ušetřit čas při psaní často používaného kódu kontroleru a vytváření zobrazení se silnými typy, ale toto není druh generovaného kódu, který jste mohli vidět s nepříjemné upozorněními v komentářích k tomu, jak nesmí změnit. znakovou. Toto je váš kód a očekává se, že ho změníte.

Pojďme tedy začít rychle upravovat v zobrazení indexu StoreManager (/Views/StoreManager/Index.cshtml). V tomto zobrazení se zobrazí tabulka, která obsahuje seznam alb v našem úložišti s odkazy upravit/podrobnosti/odstranit a obsahuje veřejné vlastnosti alba. Odebereme pole AlbumArtUrl, protože toto zobrazení není velice užitečné. V části &lt;tabulky&gt; kódu zobrazení odeberte &lt;&gt; a &lt;&gt; TD, jak ukazují zvýrazněné řádky níže:

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

Upravený kód zobrazení se zobrazí takto:

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a>První pohled na správce úložiště

Nyní spusťte aplikaci a přejděte do/StoreManager/. Tím se zobrazí index Správce úložiště, který jsme právě změnili, a zobrazí se seznam alb ve Storu s odkazy na úpravy, podrobnosti a odstranění.

![](mvc-music-store-part-5/_static/image3.png)

Kliknutím na odkaz Upravit se zobrazí formulář pro úpravy s poli pro album, včetně rozevíracích seznamů žánru a umělce.

![](mvc-music-store-part-5/_static/image4.png)

V dolní části klikněte na odkaz zpět na seznam a pak klikněte na odkaz podrobnosti pro album. Zobrazí se podrobné informace o jednotlivých albech.

![](mvc-music-store-part-5/_static/image5.png)

Znovu klikněte na odkaz zpět na seznam a pak klikněte na odkaz odstranit. Tím se zobrazí potvrzovací dialogové okno s podrobnostmi o albu a s dotazem, jestli jsme si jisti, že ji chceme odstranit.

![](mvc-music-store-part-5/_static/image6.png)

Kliknutí na tlačítko Odstranit v dolní části odstraní album a vrátíte se na stránku index, kde se zobrazí odstraněné album.

Neudělali jsme se správcem úložiště, ale máme pracovní kontroler a kód zobrazení pro zahájení operací CRUD.

## <a name="looking-at-the-store-manager-controller-code"></a>Podívejte se na kód kontroleru Správce úložiště.

Kontroler Správce úložiště obsahuje dobrý objem kódu. Podívejme se na to shora dolů. Kontroler zahrnuje některé standardní obory názvů pro kontroler MVC a také odkaz na obor názvů našich modelů. Kontroler má soukromou instanci MusicStoreEntities, kterou používají všechny akce kontroleru pro přístup k datům.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a>Akce indexu a podrobností Správce úložiště

Zobrazení index načte seznam alb, včetně informací o žánru a informacích o jednotlivých albech, jak jsme se předtím viděli při práci na metodě procházení Store. Zobrazení index je po odkazech na propojené objekty, aby mohl zobrazit název a jméno žánru každého alba, aby byl kontroler efektivní a dotazován na tyto informace v původní žádosti.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

Akce kontroleru řadiče StoreManager funguje úplně stejně jako akce s podrobnostmi řadiče úložiště, které jsme napsali jako předchozí dotaz na album podle ID pomocí metody Find () a pak ji vrátíte do zobrazení.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a>Metody akce vytvoření

Metody akce vytvoření se trochu liší od těch, které jsme doposud viděli, protože zpracovávají vstup z formuláře. Když uživatel poprvé navštíví/StoreManager/Create/, zobrazí se prázdná forma. Tato stránka HTML bude obsahovat prvek &lt;Form&gt;, který obsahuje ovládací prvky DropDown a TextBox Input, kde mohou zadat podrobnosti o albu.

Jakmile uživatel vyplní hodnoty ve formuláři alba, může kliknutím na tlačítko Uložit odeslat tyto změny zpět do naší aplikace, aby se uložily v rámci databáze. Když uživatel stiskne tlačítko Uložit, &lt;formulář&gt; provede odeslání do adresy URL/StoreManager/Create/a odešle &lt;formuláře&gt; hodnoty jako součást příspěvku HTTP.

ASP.NET MVC nám umožňuje snadno rozdělit logiku těchto dvou scénářů volání adresy URL tím, že nám umožní implementovat dvě samostatné metody "vytvoření" v rámci naší třídy StoreManagerController – jednu pro zpracování počátečního protokolu HTTP-GET na adresu URL/StoreManager/Create/a druhý pro zpracování HTTP-POST u odeslaných změn.

### <a name="passing-information-to-a-view-using-viewbag"></a>Předávání informací do zobrazení pomocí ViewBag

Používali jsme ViewBag dříve v tomto kurzu, ale nemluviliy se o nich hodně. ViewBag nám umožňuje předat informace do zobrazení bez použití objektu modelu silného typu. V takovém případě musí akce upravit HTTP-získat Controller předat seznam žánrů a umělců do formuláře k naplnění rozevíracích seznamů a nejjednodušší způsob, jak to udělat, aby byly vráceny jako ViewBag položky.

ViewBag je dynamický objekt, což znamená, že můžete zadat ViewBag. foo nebo ViewBag. YourNameHere, aniž by bylo nutné psát kód pro definování těchto vlastností. V tomto případě kód kontroleru používá ViewBag. GenreId a ViewBag. ArtistId, aby hodnoty rozevíracího seznamu odeslané ve formuláři byly GenreId a ArtistId, což jsou vlastnosti alba, které budou nastaveny.

Tyto hodnoty rozevíracích seznamů jsou vráceny do formuláře pomocí objektu SelectList, který je sestaven pouze pro tento účel. To se provádí pomocí kódu takto:

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

Jak vidíte z kódu metody akce, jsou použity tři parametry pro vytvoření tohoto objektu:

- Seznam položek, které budou zobrazeny v rozevíracím seznamu. Všimněte si, že to není pouze řetězec – předáváme seznam žánrů.
- Dalším parametrem, který je předán do SelectList, je vybraná hodnota. Tímto způsobem SelectList ví, jak předem vybrat položku v seznamu. To bude snazší pochopit, kdy se podíváme na formulář pro úpravy, který je poměrně podobný.
- Konečný parametr je vlastnost, která má být zobrazena. V tomto případě to znamená, že vlastnost Genre.Name se zobrazí uživateli.

V takovém případě je akce HTTP-GET Create poměrně jednoduchá – do ViewBag se přidají dvě SelectLists a do formuláře se nepředává žádný objekt modelu (protože ještě nebyl vytvořen).

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a>Pomocník HTML pro zobrazení rozevíracích seznamu v zobrazení pro vytváření

Vzhledem k tomu, že jsme mluvilii, jak jsou hodnoty rozevíracího seznamu předávány zobrazení, se podívejme na zobrazení a podívejte se, jak se tyto hodnoty zobrazují. V kódu zobrazení (/Views/StoreManager/Create.cshtml) se zobrazí následující volání pro zobrazení rozevírací nabídky Žánr.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

To se označuje jako pomocník HTML – metoda nástroje, která provádí běžné úkoly zobrazení. Pomocníky HTML jsou velmi užitečné při zachování stručného a čitelného kódu zobrazení. Pomocná rutina HTML. DropDownList je poskytována ASP.NET MVC, ale jakmile se později ukážeme, že je možné vytvořit vlastní pomůcky pro kód zobrazení, budeme v naší aplikaci znovu používat.

Volání HTML. DropDownList stačí pouze 2 věci – kde získat seznam k zobrazení a jaká hodnota (pokud existuje) by měla být předem vybraná. První parametr, GenreId, instruuje DropDownList, aby hledal hodnotu s názvem GenreId v modelu nebo v ViewBag. Druhý parametr se používá k označení hodnoty, která se má zobrazit v rozevíracím seznamu původně vybrané. Vzhledem k tomu, že se jedná o formulář pro vytvoření, není k dispozici žádná hodnota, která se má Předvybrat a zadat řetězec. je předána hodnota Empty

### <a name="handling-the-posted-form-values"></a>Zpracování hodnot publikovaných formulářů

Jak jsme probrali dřív, ke každému formuláři jsou přidruženy dvě metody akcí. První zpracuje požadavek HTTP-GET a zobrazí formulář. Druhý zpracovává požadavek HTTP-POST, který obsahuje odeslané hodnoty formuláře. Všimněte si, že akce kontroleru má atribut [HttpPost], který oznamuje ASP.NET MVC, že by měl reagovat pouze na požadavky HTTP-POST.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

Tato akce má čtyři zodpovědnosti:

- 1. Přečtěte si hodnoty formuláře.
- 2. Kontrola, zda hodnoty formuláře přecházejí do libovolných ověřovacích pravidel
- 3. Pokud je odeslání formuláře platné, uložte data a zobrazte aktualizovaný seznam.
- 4. Pokud odeslání formuláře není platné, zobrazí se znovu formulář s chybami ověřování.

#### <a name="reading-form-values-with-model-binding"></a>Čtení hodnot formuláře s vazbou modelu

Akce kontroleru zpracovává odeslání formuláře, které zahrnuje hodnoty pro GenreId a ArtistId (z rozevíracího seznamu) a hodnoty TextBox pro title, Price a AlbumArtUrl. I když je možné přímo získat přístup k hodnotám formuláře, lepším řešením je použití možností vazby modelu integrovaných do ASP.NET MVC. Když akce kontroleru převezme typ modelu jako parametr, ASP.NET MVC se pokusí naplnit objekt daného typu pomocí vstupů formuláře (stejně jako hodnoty Route a QueryString). To dělá tak, že vyhledá hodnoty, jejichž názvy odpovídají vlastnostem objektu modelu, například při nastavení hodnoty GenreId nového objektu alba, vyhledá vstup s názvem GenreId. Při vytváření zobrazení pomocí standardních metod v ASP.NET MVC budou formuláře vždy vykresleny pomocí názvů vlastností jako názvy vstupních polí, takže názvy polí budou přesně odpovídat.

#### <a name="validating-the-model"></a>Ověřování modelu

Model je ověřen pomocí jednoduchého volání ModelState. IsValid. Zatím jsme nepřidali žádná ověřovací pravidla do naší třídy alba. provedeme to tak, že v tuto chvíli Tato kontrola nebude mnohem dělat. Důležité je, aby se tato kontrola ModelStat. IsValid přizpůsobila ověřovacím pravidlům, která jsme umístili do našeho modelu, takže budoucí změny pravidel ověřování nebudou pro kód akce kontroleru vyžadovat žádné aktualizace.

#### <a name="saving-the-submitted-values"></a>Uložení odeslaných hodnot

Pokud odesláním formuláře projde ověřování, je čas uložit hodnoty do databáze. U Entity Framework, který pouze vyžaduje přidání modelu do kolekce alba a volání metody SaveChanges.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

Entity Framework generuje vhodné příkazy SQL pro zachování hodnoty. Po uložení dat přesměrujeme zpátky na seznam alb, abychom mohli zobrazit naši aktualizaci. To se provádí vrácením RedirectToAction s názvem akce kontroleru, kterou chceme zobrazit. V tomto případě je to metoda indexu.

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a>Zobrazení neplatných odeslání formulářů s chybami ověřování

V případě neplatného vstupu formuláře jsou hodnoty rozevíracího seznamu přidány do ViewBag (jako v případě HTTP-GET) a hodnoty vázaného modelu jsou předány zpět do zobrazení pro zobrazení. Chyby ověřování se automaticky zobrazí pomocí @Html.ValidationMessageFor pomocníka HTML.

#### <a name="testing-the-create-form"></a>Testování formuláře pro vytvoření

Pokud chcete tento test vyzkoušet, spusťte aplikaci a přejděte k/StoreManager/Create/– zobrazí se prázdný formulář, který vrátila metoda StoreController Create HTTP-GET.

Vyplňte některé hodnoty a kliknutím na tlačítko vytvořit formulář odešlete.

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a>Zpracování úprav

Pár akcí úprav (HTTP-GET a HTTP-POST) se velmi podobá metodám pro vytváření akcí, které jsme právě prohlédli na. Vzhledem k tomu, že scénář úprav zahrnuje práci s existujícím albumm, metoda upravit HTTP-GET načte album na základě parametru ID, která byla předána prostřednictvím trasy. Tento kód pro načtení alba podle AlbumId je stejný jako v případě, že jste předtím prohlédli v akci kontroleru podrobností. Stejně jako u metody Create/HTTP-GET jsou hodnoty rozevíracího seznamu vraceny prostřednictvím ViewBag. To umožňuje vrátit album jako náš objekt modelu do zobrazení (které je silně typované pro třídu alba) a současně předat další data (např. seznam žánrů) prostřednictvím ViewBag.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

Akce upravit HTTP-POST je velmi podobná akci vytvoření HTTP-POST. Jediným rozdílem je, že místo přidání nového alba do databáze. Kolekce alb: aktuální instance alba vyhledáváme pomocí DB. Záznam (album) a nastavení jeho stavu na hodnotu změněno. Tato zpráva oznamuje Entity Framework, že upravujeme existující album na rozdíl od vytvoření nového alba.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

Tuto akci můžeme otestovat spuštěním aplikace a přechodem na/StoreManger/a následným kliknutím na odkaz upravit pro album.

![](mvc-music-store-part-5/_static/image9.png)

Tím se zobrazí formulář pro úpravy zobrazený metodou upravit HTTP-GET. Vyplňte některé hodnoty a klikněte na tlačítko Uložit.

![](mvc-music-store-part-5/_static/image10.png)

Tato funkce odešle formulář, uloží hodnoty a vrátí nás do seznamu alb, kde je zobrazeno, že byly hodnoty aktualizovány.

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a>Odstraňování zpracování

Odstranění probíhá stejným vzorem jako operace Upravit a vytvořit, a to pomocí jedné akce kontroleru pro zobrazení potvrzovacího formuláře a další akce kontroleru pro zpracování odesílání formuláře.

Akce řadiče HTTP-GET Delete je přesně stejná jako u předchozí akce kontroleru podrobností Správce úložiště.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

Pomocí šablony pro odstranění obsahu zobrazení zobrazíme formulář, který je silně zadaný pro typ alba.

![](mvc-music-store-part-5/_static/image12.png)

Šablona pro odstranění zobrazuje všechna pole pro model, ale můžeme ho zjednodušit poměrně k tétomu bitu. Změňte kód zobrazení v/Views/StoreManager/Delete.cshtml na následující.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

Tím se zobrazí zjednodušené potvrzení o odstranění.

![](mvc-music-store-part-5/_static/image13.png)

Kliknutím na tlačítko Odstranit dojde k odeslání formuláře zpět na server, který provede akci DeleteConfirmed.

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

Náš postup pro odstranění ovladače HTTP-POST provede tyto akce:

- 1. Načte album podle ID.
- 2. Odstraní album a uloží změny.
- 3. Přesměruje na index, který ukazuje, že se album odebralo ze seznamu.

Pokud to chcete otestovat, spusťte aplikaci a přejděte do/StoreManager. Vyberte album ze seznamu a klikněte na odkaz odstranit.

![](mvc-music-store-part-5/_static/image14.png)

Zobrazí se vám obrazovka pro potvrzení odstranění.

![](mvc-music-store-part-5/_static/image15.png)

Kliknutím na tlačítko Odstranit odeberete album a vrátíte se na stránku index Správce úložiště, kde se zobrazí, že se album odstranilo.

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a>Zkrácení textu pomocí vlastní pomůcky HTML

Máme jeden možný problém s naší stránkou indexu správce obchodů. Vlastnosti názvu našeho alba a jméno umělce můžou být dostatečně dlouhé, aby mohly vyvolat formátování tabulky. Vytvoříme vlastní nápovědu HTML, která nám umožní snadno zkrátit tyto a další vlastnosti v našich zobrazeních.

![](mvc-music-store-part-5/_static/image17.png)

Syntaxe @helper Razor má poměrně snadné vytváření vlastních pomocných funkcí pro použití ve vašich zobrazeních. Otevřete zobrazení/Views/StoreManager/Index.cshtml a přidejte následující kód přímo za @model řádek.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

Tato pomocná metoda přebírá řetězec a povoluje maximální délku. Pokud je zadaný text kratší než zadaná délka, pomocník ho zapíše tak, jak je. Pokud je delší, zkrátí text a vykreslí "...". pro zbytek.

Teď můžeme použít naši podpůrnou pomoc, aby se zajistilo, že vlastnosti názvu alba i jméno interpreta jsou kratší než 25 znaků. Úplný kód zobrazení pomocí našeho nového pomocníka pro zkracování se zobrazí níže.

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

Když teď procházíme adresu URL/StoreManager/, budou se alba a tituly uchovávat pod maximálními délkami.

![](mvc-music-store-part-5/_static/image18.png)

Poznámka: v tomto příkladu se zobrazuje jednoduchý případ vytváření a používání pomocníka v jednom zobrazení. Další informace o vytváření pomocníků, které můžete použít v celém webu, najdete v příspěvku na blogu: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)

> [!div class="step-by-step"]
> [Předchozí](mvc-music-store-part-4.md)
> [Další](mvc-music-store-part-6.md)

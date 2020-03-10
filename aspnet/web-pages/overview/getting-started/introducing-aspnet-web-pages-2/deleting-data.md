---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
title: Představení webových stránek ASP.NET-odstraňování dat databáze | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se dozvíte, jak odstranit jednotlivou položku databáze. Předpokládá, že jste dokončili řadu prostřednictvím aktualizace databázových dat v ASP.NET Web PA...
ms.author: riande
ms.date: 01/02/2018
ms.assetid: 75b5c1cf-84bd-434f-8a86-85c568eb5b09
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
msc.type: authoredcontent
ms.openlocfilehash: c8620fc1abc61d514bdc039c66f7a84e67e89abe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78629036"
---
# <a name="introducing-aspnet-web-pages---deleting-database-data"></a>Představení webových stránek ASP.NET – odstranění databázových dat

tím, že [FitzMacken](https://github.com/tfitzmac)

> V tomto kurzu se dozvíte, jak odstranit jednotlivou položku databáze. Předpokládá, že jste dokončili řadu prostřednictvím [aktualizace databázových dat ve webových stránkách ASP.NET](updating-data.md).
> 
> Naučíte se:
> 
> - Jak vybrat jednotlivý záznam ze seznamu záznamů.
> - Jak odstranit jeden záznam z databáze.
> - Jak kontrolovat, zda bylo na formuláři kliknuto konkrétní tlačítko.
>   
> 
> Popsané funkce a technologie:
> 
> - Pomocná rutina `WebGrid`
> - Příkaz SQL `Delete`.
> - Metoda `Database.Execute` pro spuštění příkazu SQL `Delete`

## <a name="what-youll-build"></a>Co sestavíte

V předchozím kurzu jste zjistili, jak aktualizovat existující záznam databáze. Tento kurz je podobný, s tím rozdílem, že místo aktualizace záznamu ho odstraníte. Procesy jsou mnohem stejné, s výjimkou toho, že odstranění je jednodušší, takže tento kurz bude krátký.

Na stránce *filmy* aktualizujte pomocníka `WebGrid` tak, aby se zobrazil odkaz pro **odstranění** vedle každého filmu, který se doprovází pomocí odkazu pro **Úpravy** , který jste přidali dříve.

![Stránka filmy znázorňující odkaz pro odstranění každého filmu](deleting-data/_static/image1.png)

Stejně jako u úprav můžete po kliknutí na odkaz **Odstranit** přejít na jinou stránku, kde jsou informace o filmu již ve formě:

![Odstranit stránku videa se zobrazeným filmem](deleting-data/_static/image2.png)

Potom můžete kliknutím na toto tlačítko trvale odstranit záznam.

## <a name="adding-a-delete-link-to-the-movie-listing"></a>Přidání odkazu pro odstranění na seznam filmů

Začnete přidáním odkazu pro **odstranění** do pomocné rutiny `WebGrid`. Tento odkaz je podobný odkazu pro **Úpravy** , který jste přidali v předchozím kurzu.

Otevřete soubor *Movies. cshtml* .

Změňte `WebGrid` označení v těle stránky přidáním sloupce. Zde je upravený kód:

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

Nový sloupec je tento:

[!code-html[Main](deleting-data/samples/sample2.html)]

Způsob, jakým je mřížka nakonfigurována, je sloupec pro **Úpravy** v mřížce umístěn nejvíce vlevo a sloupec pro **odstranění** je umístěn nejvíce vpravo. (Pro případ, že jste si nevšimli, je teď za `Year` sloupce čárka.) Neexistují žádné speciální informace o tom, kde tyto sloupce odkazů přecházejí, a můžete je tak snadno umístit vedle sebe. V takovém případě jsou oddělené, aby byly těžší v kombinaci.

![Stránka filmy s odkazy upravit a podrobnosti označují, že nejsou vedle sebe navzájem.](deleting-data/_static/image3.png)

Nový sloupec zobrazuje odkaz (`<a>` element), jehož text říká "Delete". Cíl odkazu (jeho `href` atribut) je kód, který se nakonec překládá na něco podobného jako tato adresa URL, přičemž `id` hodnota se u každého filmu liší:

[!code-css[Main](deleting-data/samples/sample3.css)]

Tento odkaz vyvolá stránku s názvem *DeleteMovie* a předá jí ID vybraného filmu.

Tento kurz nepřejde do podrobností o tom, jak je tento odkaz vytvořený, protože je skoro totožný s odkazem na **Úpravy** z předchozího kurzu ([aktualizace dat databáze na webových stránkách ASP.NET](updating-data.md)).

## <a name="creating-the-delete-page"></a>Vytvoření stránky pro odstranění

Nyní můžete vytvořit stránku, která bude cílem pro odkaz **Delete** v mřížce.

> [!NOTE] 
> 
> **Důležité** informace Technika prvního výběru záznamu, který se má odstranit, a následného použití samostatné stránky a tlačítka k potvrzení, že proces je mimořádně důležitý pro zabezpečení. Jak jste si přečetli v předchozích kurzech, je nutné, aby *jakýkoli* druh změny webu byl *vždy* proveden pomocí &mdash; formuláře, který používá operaci http post. Pokud jste provedli změnu webu pouhým kliknutím na odkaz (tj. pomocí operace GET), můžou lidé na vašem webu provádět jednoduché požadavky a odstraňovat vaše data. I prohledávací modul, který indexuje web, může omylem odstranit data pouze pomocí následujících odkazů.
> 
> Když vaše aplikace umožňuje uživatelům změnit záznam, je nutné k tomu připrezentovat záznam uživateli pro úpravy. Ale můžete se rozhodnout, že tento krok vynecháte pro odstranění záznamu. Tento krok přeskočte, ale. (Je také užitečné, když uživatelé uvidí záznam a potvrdí, že odstraňují záznam, který zamýšlel.)
> 
> V další sadě kurzů se dozvíte, jak přidat funkce přihlášení, aby se uživatel musel před odstraněním záznamu přihlásit.

Vytvořte stránku s názvem *DeleteMovie. cshtml* a nahraďte obsah souboru následujícím kódem:

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

Tento kód je podobný jako *EditMovie* stránky s tím rozdílem, že místo použití textových polí (`<input type="text">`) obsahuje značka `<span>` prvky. Tady není nic, co byste mohli upravit. Vše, co musíte udělat, je zobrazit podrobnosti o videu, aby se uživatelé mohli ujistit, že odstraňují správný film.

Značka již obsahuje odkaz, který uživateli umožňuje vracet se na stránku se seznamem filmů.

Stejně jako na stránce *EditMovie* je ID vybraného filmu uloženo ve skrytém poli. (Předává se na stránku na prvním místě jako hodnota řetězce dotazu.) `Html.ValidationSummary` volání, které zobrazí chyby ověřování. V takovém případě může dojít k chybě, že se na stránku předalo žádné ID filmu nebo že ID filmu není platné. K této situaci může dojít, pokud někdo spustil tuto stránku bez předchozího výběru videa na stránce *filmy* .

Popisek tlačítka je **Odstranit film**a jeho atribut Name je nastaven na `buttonDelete`. Atribut `name` bude použit v kódu k identifikaci tlačítka, které odeslalo formulář.

Budete muset napsat kód na 1) Přečtěte si podrobnosti o videu při prvním zobrazení stránky a 2) opravdu odstranit film, když uživatel klikne na tlačítko.

## <a name="adding-code-to-read-a-single-movie"></a>Přidání kódu pro čtení jednoho filmu

V horní části stránky *DeleteMovie. cshtml* přidejte následující blok kódu:

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

Tento kód je stejný jako odpovídající kód na stránce *EditMovie* . Získá ID filmu z řetězce dotazu a pomocí ID přečte záznam z databáze. Kód obsahuje ověřovací test (`IsInt()` a `row != null`), aby bylo zajištěno, že ID filmu, které je předáno na stránku, je platné.

Mějte na paměti, že tento kód by měl být spuštěn pouze při prvním spuštění stránky. Pokud uživatel klikne na tlačítko **Odstranit film** , nechcete znovu načíst záznam videa z databáze. Proto kód pro čtení filmu je uvnitř testu, který říká `if(!IsPost)` &mdash;, který je, *Pokud požadavek není operace post (odeslání formuláře)* .

## <a name="adding-code-to-delete-the-selected-movie"></a>Přidání kódu pro odstranění vybraného filmu

Chcete-li odstranit film, když uživatel klikne na tlačítko, přidejte následující kód těsně do uzavírací závorky bloku `@`:

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

Tento kód je podobný kódu pro aktualizaci existujícího záznamu, ale jednodušší. Kód v podstatě spustí příkaz SQL `Delete`.

 Stejně jako na stránce *EditMovie* je kód v bloku `if(IsPost)`. Tentokrát je stav `if()` trochu složitější: 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

Existují dvě podmínky. První je, že se stránka posílá, protože jste viděli před &mdash; `if(IsPost)`.

Druhá podmínka je `!Request["buttonDelete"].IsEmpty()`, což znamená, že žádost obsahuje objekt s názvem `buttonDelete`. V případě potřeby se jedná o nepřímý způsob testování, který tlačítko odeslalo formulář. Pokud formulář obsahuje více tlačítek pro odeslání, zobrazí se v žádosti pouze název tlačítka, které bylo kliknuto. Proto logicky, pokud se název určitého tlačítka objeví v žádosti &mdash; nebo jak je uvedeno v kódu, pokud toto tlačítko není prázdné &mdash;, které je tlačítko, které formulář odeslalo.

Operátor `&&` znamená "a" (Logical a). Proto je celá podmínka `if`...

*Tento požadavek je post (nejedná se o první požadavek).*  
  
 AND  
  
Tlačítko `buttonDelete`*bylo tlačítko, které odeslalo formulář.*

Tento formulář (ve skutečnosti tuto stránku) obsahuje jenom jedno tlačítko, takže další test pro `buttonDelete` není technicky nutný. Pořád se chystáte provést operaci, která bude trvale odebírat data. Proto chcete mít jistotu, že provádíte operaci pouze v případě, že ji uživatel výslovně požadoval. Předpokládejme například, že později jste tuto stránku rozšířili a přidali do ní další tlačítka. Dokonce i kód, který odstraní film, bude spuštěn pouze v případě, že bylo kliknuto na tlačítko `buttonDelete`.

Stejně jako na stránce *EditMovie* získáte ID z skrytého pole a pak spustíte příkaz SQL. Syntaxe příkazu `Delete` je:

`DELETE FROM table WHERE ID = value`

Je důležité zahrnout klauzuli `WHERE` a ID. Pokud ponecháte klauzuli WHERE, *odstraní se všechny záznamy v tabulce*. Jak jste viděli, předáte hodnotu ID příkazu SQL pomocí zástupného symbolu.

## <a name="testing-the-movie-delete-process"></a>Testování procesu odstranění filmu

Nyní můžete provést test. Spusťte stránku *filmy* a klikněte na tlačítko **Odstranit** vedle videa. Po zobrazení stránky *DeleteMovie* klikněte na **Odstranit film**.

![Stránka odstranit film s zvýrazněným tlačítkem odstranit video](deleting-data/_static/image4.png)

Když kliknete na tlačítko, kód odstraní filmy a vrátí se do seznamu filmů. Můžete vyhledat odstraněný film a potvrdit, že je odstraněný.

## <a name="coming-up-next"></a>Připravujeme další

V dalším kurzu se dozvíte, jak dát všem stránkám na vašem webu běžný vzhled a rozložení.

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a>Úplný výpis stránky videa (aktualizovaný s odkazy Delete)

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a>Úplný výpis pro stránku DeleteMovie

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a>Další prostředky

- [Seznámení s ASP.NET webovým programováním pomocí syntaxe Razor](../introducing-razor-syntax-c.md)
- [Příkaz SQL Delete](http://www.w3schools.com/sql/sql_delete.asp) na webu w3schools

> [!div class="step-by-step"]
> [Předchozí](updating-data.md)
> [Další](layouts.md)

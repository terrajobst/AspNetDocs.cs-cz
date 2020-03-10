---
uid: web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
title: Vytvoření konzistentního rozložení v lokalitách ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Aby bylo vytváření webových stránek pro svůj web efektivnější, můžete vytvořit opakovaně použitelné bloky obsahu (například záhlaví a zápatí) pro váš web a Vy c...
ms.author: riande
ms.date: 03/10/2014
ms.assetid: d7bd001b-6db2-4422-9b78-f3d08b743b00
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
msc.type: authoredcontent
ms.openlocfilehash: 3f63ce68ae4c13970ac0df196167ace0b22b592c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627447"
---
# <a name="creating-a-consistent-layout-in-aspnet-web-pages-razor-sites"></a>Vytvoření konzistentního rozložení na webech ASP.NET Web Pages (Razor)

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek vysvětluje, jak můžete použít stránky rozložení na webu ASP.NET Web Pages (Razor) k vytvoření opakovaně použitelných bloků obsahu (například hlaviček a zápatí) a vytvořit konzistentní vzhled pro všechny stránky v lokalitě.
> 
> **Co se naučíte:** 
> 
> - Vytvoření opakovaně použitelných bloků obsahu, jako jsou záhlaví a zápatí.
> - Jak vytvořit konzistentní vzhled pro všechny stránky v lokalitě pomocí rozložení.
> - Jak předat data v době běhu do stránky rozložení.
> 
> Jedná se o funkce ASP.NET, které jsou představené v článku:
> 
> - Bloky obsahu, což jsou soubory, které obsahují obsah ve formátu HTML, který má být vložen na více stránek.
> - Stránky rozložení, což jsou stránky, které obsahují obsah ve formátu HTML, který může být sdílen stránkami na webu.
> - Metody `RenderPage`, `RenderBody`a `RenderSection`, které oznamují ASP.NET, kde vložit prvky stránky.
> - Slovník `PageData`, který umožňuje sdílet data mezi bloky obsahu a stránkami rozložení.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 3
>   
> 
> Tento kurz funguje také s ASP.NET webovými stránkami 2.

## <a name="about-layout-pages"></a>O stránkách rozložení

Mnoho webů má obsah, který se zobrazuje na každé stránce, jako je záhlaví a zápatí, nebo pole, které oznamuje uživatelům, že se přihlásili. ASP.NET umožňuje vytvořit samostatný soubor s blokem obsahu, který může obsahovat text, kód a kód, stejně jako běžná webová stránka. Pak můžete vložit blok obsahu na jiné stránky na webu, kde chcete informace zobrazit. Tímto způsobem nemusíte kopírovat a vkládat stejný obsah na každou stránku. Vytváření společného obsahu, podobně jako to, usnadňuje aktualizaci webu. Pokud potřebujete změnit obsah, můžete jenom aktualizovat jeden soubor a změny se pak projeví všude, kde je obsah vložený.

Následující obrázek znázorňuje fungování bloků obsahu. Když prohlížeč požaduje stránku z webového serveru, ASP.NET vloží bloky obsahu v místě, kde je na hlavní stránce volána metoda `RenderPage`. Stránka dokončeno (sloučeno) se pak pošle do prohlížeče.

![Koncepční diagram znázorňující, jak metoda RenderPage vloží odkazovanou stránku na aktuální stránku.](3-creating-a-consistent-look/_static/image1.jpg)

V tomto postupu vytvoříte stránku, která odkazuje na dva bloky obsahu (záhlaví a zápatí) umístěné v samostatných souborech. Stejné bloky obsahu můžete použít na libovolné stránce webu. Až budete hotovi, dostanete stránku podobné této:

![Snímek obrazovky, který ukazuje stránku v prohlížeči, která je výsledkem spuštění stránky, která obsahuje volání metody RenderPage.](3-creating-a-consistent-look/_static/image2.png)

1. V kořenové složce vašeho webu vytvořte soubor s názvem *index. cshtml*.
2. Existující značku nahraďte následujícím kódem:

    [!code-html[Main](3-creating-a-consistent-look/samples/sample1.html)]
3. V kořenové složce vytvořte složku s názvem *Shared*.

    > [!NOTE]
    > Běžným postupem je ukládání souborů, které jsou sdíleny mezi webovými stránkami ve složce s názvem *Shared*.
4. Ve *sdílené* složce vytvořte soubor s názvem *\_Header. cshtml*.
5. Existující obsah nahraďte následujícím:

    [!code-html[Main](3-creating-a-consistent-look/samples/sample2.html)]

    Všimněte si, že název souboru je *\_Header. cshtml*s podtržítkem (\_) jako předponou. ASP.NET nepošle stránku do prohlížeče, pokud jeho název začíná podtržítkem. To brání lidem v žádosti (neúmyslně nebo jinak) tyto stránky přímo. Je vhodné použít podtržítko pro názvy stránek, které mají v nich bloky obsahu, protože nechcete, aby uživatelé mohli vyžádat tyto stránky &#8212; výhradně pro vložení na jiné stránky.
6. Ve *sdílené* složce vytvořte soubor s názvem *\_footer. cshtml* a nahraďte ho následujícím obsahem:

    [!code-html[Main](3-creating-a-consistent-look/samples/sample3.html)]
7. Na stránce *index. cshtml* přidejte dvě volání metody `RenderPage`, jak je znázorněno zde:

    [!code-html[Main](3-creating-a-consistent-look/samples/sample4.html)]

    To ukazuje, jak vložit blok obsahu do webové stránky. Zavoláte metodu `RenderPage` a předá jí název souboru, jehož obsah chcete v tomto okamžiku vložit. Sem vkládáte obsah *\_hlaviček. cshtml* a *\_footer. cshtml* do souboru *index. cshtml* .
8. Spusťte stránku *index. cshtml* v prohlížeči. (Ve WebMatrixu v pracovním prostoru **soubory** klikněte pravým tlačítkem na soubor a vyberte **Spustit v prohlížeči**.)
9. V prohlížeči zobrazte zdroj stránky. (Například v Internet Exploreru klikněte pravým tlačítkem na stránku a pak klikněte na **Zobrazit zdroj**.)

    To vám umožní zobrazit kód webové stránky, který se odešle do prohlížeče, který kombinuje značky stránky indexu s bloky obsahu. Následující příklad ukazuje zdroj stránky, který je vykreslen pro *index. cshtml*. Volání `RenderPage`, která jste vložili do souboru *index. cshtml* , byla nahrazena skutečným obsahem souborů hlaviček a zápatí.

    [!code-html[Main](3-creating-a-consistent-look/samples/sample5.html)]

## <a name="creating-a-consistent-look-using-layout-pages"></a>Vytvoření konzistentního vzhledu pomocí stránek rozložení

Zatím jste viděli, že na více stránkách je snadné zahrnout stejný obsah. Strukturovaným přístupem k vytvoření konzistentního vzhledu webu je použití stránek rozložení. Stránka rozložení definuje strukturu webové stránky, ale neobsahuje žádný skutečný obsah. Po vytvoření stránky rozložení můžete vytvořit webové stránky, které obsah obsahují, a pak je propojit se stránkou rozložení. Po zobrazení těchto stránek budou tyto stránky formátovány podle stránky rozložení. (V tomto smyslu stránka rozložení funguje jako typ šablony pro obsah, který je definovaný na jiných stránkách.)

Stránka rozložení je stejně jako libovolná stránka HTML s tím rozdílem, že obsahuje volání metody `RenderBody`. Pozice metody `RenderBody` na stránce rozložení určuje, kam budou zahrnuty informace ze stránky obsahu.

Následující diagram znázorňuje, jak se stránky obsahu a stránky rozložení kombinují za běhu, aby se vytvořila hotová webová stránka. Prohlížeč vyžádá stránku obsahu. Stránka obsahu obsahuje kód, který určuje stránku rozložení, která se má použít pro strukturu stránky. Na stránce rozložení je obsah vložen do místa, kde je volána metoda `RenderBody`. Bloky obsahu lze také vložit do stránky rozložení voláním metody `RenderPage`, způsobu, jaký jste provedli v předchozí části. Až se webová stránka dokončí, pošle se do prohlížeče.

![Snímek obrazovky, který ukazuje stránku v prohlížeči, která je výsledkem spuštění stránky, která obsahuje volání metody RenderBody.](3-creating-a-consistent-look/_static/image3.jpg)

Následující postup ukazuje, jak vytvořit stránku rozložení a propojit na ni stránky obsahu.

1. Ve *sdílené* složce vašeho webu vytvořte soubor s názvem *\_Layout1. cshtml*.
2. Existující obsah nahraďte následujícím:

    [!code-html[Main](3-creating-a-consistent-look/samples/sample6.html)]

    Pomocí metody `RenderPage` na stránce rozložení lze vkládat bloky obsahu. Stránka rozložení může obsahovat pouze jedno volání metody `RenderBody`.
3. Ve *sdílené* složce vytvořte soubor s názvem *\_Header2. cshtml* a nahraďte veškerý existující obsah následujícím:

    [!code-html[Main](3-creating-a-consistent-look/samples/sample7.html)]
4. V kořenové složce vytvořte novou složku a pojmenujte ji *styly*.
5. Ve složce *Styles (styly* ) vytvořte soubor s názvem *Web. CSS* a přidejte následující definice stylu:

    [!code-css[Main](3-creating-a-consistent-look/samples/sample8.css)]

    Tyto definice stylu slouží pouze k zobrazení, jak lze použít šablony stylů se stránkami rozložení. Pokud chcete, můžete pro tyto prvky definovat vlastní styly.
6. V kořenové složce vytvořte soubor s názvem *Content1. cshtml* a nahraďte veškerý existující obsah následujícím:

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample9.cshtml)]

    Toto je stránka, která bude používat stránku rozložení. Blok kódu v horní části stránky indikuje, kterou stránku rozložení použít k formátování tohoto obsahu.
7. Spusťte *Content1. cshtml* v prohlížeči. Vykreslená stránka používá formát a předlohu stylů definované v *\_Layout1. cshtml* a text (Content) definovaný v *Content1. cshtml*.

    ![obrazu](3-creating-a-consistent-look/_static/image4.png)

    Můžete opakovat krok 6 a vytvořit další stránky obsahu, které pak můžou sdílet stejnou stránku rozložení.

    > [!NOTE]
    > Můžete nastavit web tak, aby bylo možné automaticky použít stejnou stránku rozložení pro všechny stránky obsahu ve složce. Podrobnosti najdete v tématu [přizpůsobení chování pro webové stránky ASP.NET napříč lokalitami](https://go.microsoft.com/fwlink/?LinkId=202906).

## <a name="designing-layout-pages-that-have-multiple-content-sections"></a>Návrh stránek rozložení, které mají více oddílů obsahu

Stránka obsahu může obsahovat více oddílů, což je užitečné, pokud chcete použít rozložení, která mají více oblastí s nahraditelným obsahem. Na stránce obsah dáte každému oddílu jedinečný název. (Výchozí oddíl zůstane nepojmenovaný.) Na stránce rozložení přidejte `RenderBody` metodu, která určuje, kde se má zobrazit oddíl bez názvu (výchozí). Pak přidáte samostatné metody `RenderSection`, aby bylo možné vykreslit pojmenované oddíly jednotlivě.

Následující diagram ukazuje, jak ASP.NET zpracovává obsah, který je rozdělen do více částí. Každý pojmenovaný oddíl je obsažen v bloku oddílu na stránce obsahu. (Nazývají se `Header` a `List` v příkladu.) Rozhraní vloží oddíl obsahu do stránky rozložení v místě, kde je volána metoda `RenderSection`. Nejmenovaný (výchozí) oddíl je vložen do místa, kde je volána metoda `RenderBody`, jak jste viděli dříve.

![Koncepční diagram znázorňující, jak metoda RenderSection vkládá odkazy na oddíly do aktuální stránky.](3-creating-a-consistent-look/_static/image5.jpg)

Tento postup ukazuje, jak vytvořit stránku obsahu s více oddíly obsahu a jak ji vykreslit pomocí stránky rozložení, která podporuje více oddílů obsahu.

1. Ve *sdílené* složce vytvořte soubor s názvem *\_Layout2. cshtml*.
2. Existující obsah nahraďte následujícím:

    [!code-html[Main](3-creating-a-consistent-look/samples/sample10.html)]

    Pomocí metody `RenderSection` můžete vykreslit oddíly záhlaví i seznamu.
3. V kořenové složce vytvořte soubor s názvem *Content2. cshtml* a nahraďte veškerý existující obsah následujícím:

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample11.cshtml)]

    Tato stránka obsahu obsahuje blok kódu v horní části stránky. Každý pojmenovaný oddíl je obsažen v bloku oddílu. Zbývající část stránky obsahuje oddíl výchozí (nepojmenovaný) obsah.
4. Spusťte *Content2. cshtml* v prohlížeči.

    ![Snímek obrazovky, který ukazuje stránku v prohlížeči, která je výsledkem spuštění stránky, která obsahuje volání metody RenderSection.](3-creating-a-consistent-look/_static/image6.png)

## <a name="making-content-sections-optional"></a>Nastavení oddílů obsahu jako volitelné

Obvykle oddíly, které vytvoříte na stránce obsahu, musí odpovídat oddílům, které jsou definovány na stránce rozložení. Pokud dojde k některé z následujících akcí, můžete získat chyby:

- Stránka Obsah obsahuje oddíl, který nemá žádný odpovídající oddíl na stránce rozložení.
- Stránka rozložení obsahuje oddíl, pro který není k dispozici žádný obsah.
- Stránka rozložení obsahuje volání metod, která se pokusí vykreslit stejnou část více než jednou.

Toto chování pojmenovaného oddílu však můžete přepsat deklarováním oddílu, který bude volitelný na stránce rozložení. To umožňuje definovat více stránek obsahu, které mohou sdílet stránku rozložení, ale mohou nebo nemusí mít obsah pro konkrétní oddíl.

1. Otevřete *Content2. cshtml* a odeberte následující část:

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample12.cshtml)]
2. Uložte stránku a spusťte ji v prohlížeči. Zobrazí se chybová zpráva, protože stránka obsahu neposkytuje obsah pro oddíl definovaný na stránce rozložení, konkrétně v oddílu záhlaví.

    ![Snímek obrazovky zobrazující chybu, ke které dojde, pokud spouštíte stránku, která volá metodu RenderSection, ale není k dispozici odpovídající oddíl.](3-creating-a-consistent-look/_static/image7.png)
3. Ve *sdílené* složce otevřete stránku *\_Layout2. cshtml* a nahraďte tento řádek:

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample13.js)]

    s následujícím kódem:

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample14.js)]

    Jako alternativu můžete nahradit předchozí řádek kódu následujícím blokem kódu, který vytváří stejné výsledky:

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample15.cshtml)]
4. Znovu spusťte stránku *Content2. cshtml* v prohlížeči. (Pokud pořád tuto stránku otevřete v prohlížeči, můžete ji jenom aktualizovat.) Tentokrát se stránka zobrazuje bez chyby, i když nemá hlavičku.

## <a name="passing-data-to-layout-pages"></a>Předávání dat na stránky rozložení

Můžete mít data definovaná na stránce obsahu, na kterou musíte odkazovat na stránce rozložení. Pokud ano, musíte předat data ze stránky obsahu na stránku rozložení. Například můžete chtít zobrazit stav přihlášení uživatele nebo můžete chtít zobrazit nebo skrýt oblasti obsahu založené na vstupu uživatele.

Chcete-li předat data ze stránky obsahu na stránku rozložení, můžete vložit hodnoty do vlastnosti `PageData` stránky obsahu. Vlastnost `PageData` je kolekce párů název/hodnota, které obsahují data, která chcete předat mezi stránkami. Na stránce rozložení můžete následně číst hodnoty z vlastnosti `PageData`.

Tady je jiný diagram. Tento příklad ukazuje, jak může ASP.NET pomocí vlastnosti `PageData` předávat hodnoty ze stránky obsahu na stránku rozložení. Když ASP.NET začne sestavovat webovou stránku, vytvoří kolekci `PageData`. Na stránce obsah napíšete kód pro vložení dat do kolekce `PageData`. K hodnotám v kolekci `PageData` lze také přistupovat jinými oddíly na stránce obsahu nebo dalšími bloky obsahu.

![Koncepční diagram znázorňující, jak může stránka obsahu naplnit slovník PageData a předat tyto informace na stránku rozložení.](3-creating-a-consistent-look/_static/image8.jpg)

Následující postup ukazuje, jak předat data ze stránky obsahu na stránku rozložení. Po spuštění stránky se zobrazí tlačítko, které uživateli umožňuje skrýt nebo zobrazit seznam definovaný na stránce rozložení. Když uživatel klikne na tlačítko, nastaví hodnotu true nebo false (logická hodnota) ve vlastnosti `PageData`. Stránka rozložení načte tuto hodnotu a pokud je false, seznam skryje. Hodnota se také používá na stránce obsah k určení, zda se má zobrazit tlačítko **Skrýt seznam** nebo **Zobrazit seznam** .

![obrazu](3-creating-a-consistent-look/_static/image9.jpg)

1. V kořenové složce vytvořte soubor s názvem *Content3. cshtml* a nahraďte veškerý existující obsah následujícím:

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample16.cshtml)]

    Kód ukládá dvě části dat do vlastnosti &#8212; `PageData` název webové stránky a hodnotu true nebo false pro určení, zda se má zobrazit seznam.

    Všimněte si, že ASP.NET umožňuje vložit kód HTML do stránky podmíněně pomocí bloku kódu. Například blok `if/else` v těle stránky určuje, který formulář se má zobrazit v závislosti na tom, zda je `PageData["ShowList"]` nastaven na hodnotu true.
2. Ve *sdílené* složce vytvořte soubor s názvem *\_Layout3. cshtml* a nahraďte veškerý existující obsah následujícím:

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample17.cshtml)]

    Stránka rozložení obsahuje výraz v prvku `<title>`, který získá hodnotu názvu z vlastnosti `PageData`. K určení, zda se má zobrazit blok obsahu seznamu, používá také `ShowList` hodnotu vlastnosti `PageData`.
3. Ve *sdílené* složce vytvořte soubor s názvem *\_list. cshtml* a nahraďte veškerý existující obsah následujícím:

    [!code-html[Main](3-creating-a-consistent-look/samples/sample18.html)]
4. Spusťte stránku *Content3. cshtml* v prohlížeči. Stránka se zobrazí se seznamem zobrazeným na levé straně stránky a tlačítkem **Skrýt seznam** v dolní části.

    ![Snímek obrazovky zobrazující stránku obsahující seznam a tlačítko s textem skrýt seznam](3-creating-a-consistent-look/_static/image10.png)
5. Klikněte na **Skrýt seznam**. Seznam zmizí a tlačítko se změní na **zobrazení seznamu**.

    ![Snímek obrazovky se stránkou, která nezahrnuje seznam a tlačítko s textem Zobrazit seznam.](3-creating-a-consistent-look/_static/image11.png)
6. Klikněte na tlačítko **Zobrazit seznam** a seznam se zobrazí znovu.

## <a name="additional-resources"></a>Další prostředky

[Přizpůsobení chování na úrovni webu pro webové stránky v ASP.NET](https://go.microsoft.com/fwlink/?LinkId=202906)

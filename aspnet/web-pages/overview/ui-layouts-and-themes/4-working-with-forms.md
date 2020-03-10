---
uid: web-pages/overview/ui-layouts-and-themes/4-working-with-forms
title: Práce s formuláři HTML na webech ASP.NET Web Pages (Razor) | Microsoft Docs
author: Rick-Anderson
description: Formulář je oddíl dokumentu HTML, kam vložíte ovládací prvky pro zadání uživatele, jako jsou textová pole, zaškrtávací políčka, přepínače a rozevírací seznamy. Používáte formuláře Wh...
ms.author: riande
ms.date: 02/10/2014
ms.assetid: f3f4b8c8-e8f6-4474-ad94-69228a6c01ee
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/4-working-with-forms
msc.type: authoredcontent
ms.openlocfilehash: c7d4802063c8610a246afe67bd15eea429f7304a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639704"
---
# <a name="working-with-html-forms-in-aspnet-web-pages-razor-sites"></a>Práce s formuláři HTML na webech ASP.NET Web Pages (Razor)

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek popisuje, jak zpracovat formulář HTML (s textovými poli a tlačítky) při práci na webu ASP.NET Web Pages (Razor).
> 
> **Co se naučíte:** 
> 
> - Vytvoření formuláře HTML.
> - Čtení vstupu uživatele z formuláře.
> - Ověření vstupu uživatele
> - Obnovení hodnot formuláře po odeslání stránky.
> 
> Toto jsou koncepty programování ASP.NET představené v článku:
> 
> - Objekt `Request`
> - Ověřování vstupu.
> - Kódování HTML.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 3
>   
> 
> Tento kurz funguje také s ASP.NET webovými stránkami 2.

## <a name="creating-a-simple-html-form"></a>Vytvoření jednoduchého HTML formuláře

1. Vytvoří nový web.
2. V kořenové složce vytvořte webovou stránku s názvem *Form. cshtml* a zadejte následující kód:

    [!code-html[Main](4-working-with-forms/samples/sample1.html)]
3. Spusťte stránku v prohlížeči. (Ve WebMatrixu v pracovním prostoru **soubory** klikněte pravým tlačítkem na soubor a vyberte **Spustit v prohlížeči**.) Zobrazí se jednoduchý formulář se třemi vstupními poli a tlačítkem **Odeslat** .

    ![Snímek obrazovky formuláře se třemi textovými poli](4-working-with-forms/_static/image1.png)

    Pokud v tomto okamžiku kliknete na tlačítko **Odeslat** , nedojde k žádné akci. Aby formulář mohl být užitečný, musíte přidat nějaký kód, který se spustí na serveru.

## <a name="reading-user-input-from-the-form"></a>Čtení vstupu uživatele z formuláře

Chcete-li zpracovat formulář, přidejte kód, který přečte hodnoty odeslaných polí a provede s nimi něco. Tento postup ukazuje, jak číst pole a zobrazit vstup uživatele na stránce. (V produkční aplikaci obecně provedete zajímavější věci s uživatelským vstupem. Provedete to v článku o práci s databázemi.)

1. V horní části souboru *. cshtml formuláře* zadejte následující kód:

    [!code-cshtml[Main](4-working-with-forms/samples/sample2.cshtml)]

    Když uživatel poprvé vyžádá stránku, zobrazí se pouze prázdný formulář. Uživatel (který bude) vyplní formulář a klikne na **Odeslat**. Tím se vstup uživatele odešle (odešle) na server. Ve výchozím nastavení požadavek přejde na stejnou stránku (konkrétně na *Form. cshtml*).

    Když stránku odešlete tímto časem, hodnoty, které jste zadali, se zobrazí hned nad formulářem:

    ![Snímek obrazovky zobrazující hodnoty, které jste zadali na stránce.](4-working-with-forms/_static/image2.png)

    Podívejte se na kód stránky. Nejprve pomocí metody `IsPost` určíte, zda je stránka publikována &#8212; , tedy zda uživatel klikl na tlačítko **Odeslat** . Pokud se jedná o příspěvek, `IsPost` vrátí hodnotu true. Toto je standardní způsob na webových stránkách ASP.NET, abyste zjistili, jestli pracujete s počátečním požadavkem (požadavek GET) nebo zpětným voláním (požadavek POST). (Další informace o příkazu GET a POST najdete na bočním panelu "HTTP GET a POST a" Property "v tématu [Úvod k ASP.NET programování webových stránek pomocí syntaxe Razor](https://go.microsoft.com/fwlink/?LinkId=202890#SB_HttpGetPost).)

    Dále získáte hodnoty, které uživatel vyplnil z objektu `Request.Form` a vložíte je do proměnných pro pozdější použití. Objekt `Request.Form` obsahuje všechny hodnoty, které byly odeslány se stránkou, z nichž každá je identifikována klíčem. Klíč je ekvivalentem atributu `name` pole formuláře, které chcete číst. Chcete-li například číst pole `companyname` (textové pole), použijte `Request.Form["companyname"]`.

    Hodnoty formuláře jsou uloženy v objektu `Request.Form` jako řetězce. Proto pokud je nutné pracovat s hodnotou jako číslo nebo datum nebo nějaký jiný typ, je nutné jej převést z řetězce na tento typ. V příkladu je metoda `AsInt` `Request.Form` použita k převodu hodnoty pole zaměstnanci (které obsahuje počet zaměstnanců) na celé číslo.
2. Otevřete stránku v prohlížeči, vyplňte pole formuláře a klikněte na **Odeslat**. Na stránce se zobrazí hodnoty, které jste zadali.

> [!TIP] 
> 
> <a id="SB_HTMLEncoding"></a>
> ### <a name="html-encoding-for-appearance-and-security"></a>Kódování HTML pro vzhled a zabezpečení
> 
> HTML má speciální použití pro znaky, jako `<`, `>`a `&`. Pokud se tyto speciální znaky zobrazí tam, kde nejsou očekávány, mohou ruin vzhled a funkce webové stránky. Například prohlížeč interpretuje `<` znak (Pokud není následován mezerou) jako začátek elementu HTML, jako je například `<b>` nebo `<input ...>`. Pokud prohlížeč nerozpozná prvek, jednoduše zahodí řetězec, který začíná na `<`, dokud nedosáhne něco, co znovu rozpoznává. Zjevně to může způsobit, že se na stránce divné vykreslování.
> 
> Kódování HTML nahrazuje tyto vyhrazené znaky kódem, který prohlížeče interpretuje jako správný symbol. Například znak `<` je nahrazen `&lt;` a znak `>` je nahrazen `&gt;`. Prohlížeč vykreslí tyto náhradní řetězce jako znaky, které chcete zobrazit.
> 
> Je vhodné použít kódování HTML při každém zobrazení řetězců (vstupů), které jste dostali od uživatele. Pokud to neuděláte, uživatel se může pokusit najít webovou stránku, aby spouštěl škodlivý skript nebo něco jiného, co neohrožuje zabezpečení vašeho webu, nebo to není, co máte v úmyslu. (To je obzvláště důležité, Pokud převezmete uživatelský vstup, uložte ho někde došlo a pak ho později &#8212; zobrazit jako komentář blogu, kontrolu uživatele nebo něco podobného.)
> 
> Aby se zabránilo těmto problémům, webové stránky ASP.NET automaticky zakóduje veškerý textový obsah, který je výstupem z kódu. Například při zobrazení obsahu proměnné nebo výrazu pomocí kódu, jako je například `@MyVar`, ASP.NET webové stránky automaticky zakóduje výstup.

## <a name="validating-user-input"></a>Ověřování vstupu uživatele

Uživatelé provedou chyby. Požádáte je, aby vyplnili pole a zapomněli se k němu, nebo požádáte, aby zadali počet zaměstnanců, a místo toho zadá název. Chcete-li zajistit, aby byl formulář před jeho zpracováním vyplněn správně, ověřte vstup uživatele.

Tento postup ukazuje, jak ověřit všechna tři pole formuláře, abyste se ujistili, že uživatel je nenechal prázdný. Také zkontrolujete, jestli je hodnota počtu zaměstnanců číslo. Pokud dojde k chybám, zobrazí se chybová zpráva s informacemi o tom, jaké hodnoty neprošly ověřením.

1. V souboru *Form. cshtml* nahraďte první blok kódu následujícím kódem: 

    [!code-cshtml[Main](4-working-with-forms/samples/sample3.cshtml)]

    K ověření vstupu uživatele použijete pomoc `Validation`. Požadovaná pole zaregistrujete voláním `Validation.RequireField`. Další typy ověřování zaregistrujete voláním `Validation.Add` a zadáním pole, které se má ověřit, a typu ověření, které má být provedeno.

    Po spuštění stránky ASP.NET provede všechna ověření za vás. Výsledky můžete kontrolovat voláním `Validation.IsValid`, což vrátí hodnotu true, pokud se jakékoli pole nezdařilo, a NEPRAVDA. Obvykle zavoláte `Validation.IsValid` před provedením jakéhokoli zpracování na vstupu uživatele.
2. Aktualizujte `<body>` element přidáním tří volání metody `Html.ValidationMessage`, například takto:

    [!code-cshtml[Main](4-working-with-forms/samples/sample4.cshtml?highlight=8,13,18)]

    Chcete-li zobrazit chybové zprávy ověřování, můžete zavolat HTML.`ValidationMessage` a předejte jí název pole, pro které chcete zprávu.
3. Spusťte stránku. Pole ponechte prázdné a klikněte na **Odeslat**. Zobrazí se chybové zprávy.

    ![Snímek obrazovky zobrazující chybové zprávy zobrazené v případě, že uživatelský vstup neprojde ověřením](4-working-with-forms/_static/image3.jpg)
4. Přidejte řetězec (například "ABC") do pole **počet zaměstnanců** a klikněte na **Odeslat** znovu. Tentokrát se zobrazí chyba, která indikuje, že řetězec není ve správném formátu, jmenovitě jako celé číslo.

    ![Snímek obrazovky zobrazující chybové zprávy, které se zobrazí, pokud uživatelé zadají do pole zaměstnanci řetězec.](4-working-with-forms/_static/image4.jpg)

Webové stránky ASP.NET poskytují více možností pro ověřování vstupu uživatele, včetně možnosti automaticky provádět ověřování pomocí skriptu klienta, aby uživatelé získali okamžitou zpětnou vazbu v prohlížeči. Další informace najdete v části [Další materiály](#Additional_Resources) níže.

## <a name="restoring-form-values-after-postbacks"></a>Obnovení hodnot formuláře po Postbackech

Když jste otestovali stránku v předchozí části, možná jste si všimli, že pokud jste provedli chybu ověření, všechno, co jste zadali (ne jen neplatná data), bylo pryč a museli jste znovu zadat hodnoty pro všechna pole. To ukazuje důležitý bod: Když odešlete stránku, zpracujete ji a pak ji znovu vykreslíte, stránka se znovu vytvoří od začátku. Jak jste viděli, znamená to, že všechny hodnoty, které byly na stránce při odeslání, jsou ztraceny.

Můžete to ale snadno opravit. Máte přístup k hodnotám, které byly odeslány (v objektu `Request.Form`, takže je možné tyto hodnoty vyplnit do polí formuláře při vykreslování stránky.

1. V souboru *Form. cshtml* nahraďte `value` atributy `<input>` prvků pomocí atributu `value`.: 

    [!code-cshtml[Main](4-working-with-forms/samples/sample5.cshtml?highlight=13,19,25)]

    Atribut `value` prvků `<input>` byl nastaven na dynamické čtení hodnoty pole z objektu `Request.Form`. Při prvním vyžádání stránky jsou všechny hodnoty v objektu `Request.Form` prázdné. To je v pořádku, protože tento formulář je prázdný.
2. Otevřete stránku v prohlížeči, vyplňte pole formuláře nebo je nechte prázdné a klikněte na **Odeslat**. Zobrazí se stránka, která zobrazuje odeslané hodnoty.

    ![forms-5](4-working-with-forms/_static/image5.jpg)

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Další prostředky

- [1 001 způsoby získání vstupu od webových uživatelů](https://msdn.microsoft.com/library/ms971057.aspx)
- [Používání formulářů a zpracování vstupu uživatele](https://msdn.microsoft.com/library/ms525182(VS.90).aspx)
- [Ověřování uživatelských vstupů na webech s webovými stránkami ASP.NET](https://go.microsoft.com/fwlink/?LinkId=253002)
- [Použití automatického dokončování ve formulářích HTML](https://msdn.microsoft.com/library/ms533032(VS.85).aspx)

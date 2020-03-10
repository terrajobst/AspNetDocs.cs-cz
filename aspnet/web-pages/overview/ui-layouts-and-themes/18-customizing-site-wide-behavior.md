---
uid: web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
title: Přizpůsobení chování webu pro weby ASP.NET webových stránek (Razor) na úrovni serveru | Microsoft Docs
author: Rick-Anderson
description: Tato kapitola vysvětluje, jak provést nastavení pro celý web nebo celou složku, a ne jenom stránku.
ms.author: riande
ms.date: 02/17/2014
ms.assetid: e158bed7-226f-4275-b02e-7553bd58c669
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/18-customizing-site-wide-behavior
msc.type: authoredcontent
ms.openlocfilehash: f05e05f725d9209bce283ce18659ae5efe4de2ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634622"
---
# <a name="customizing-site-wide-behavior-for-aspnet-web-pages-razor-sites"></a>Přizpůsobení chování na úrovni webu pro weby ASP.NET Web Pages (Razor)

tím, že [FitzMacken](https://github.com/tfitzmac)

> Tento článek vysvětluje, jak provést nastavení na straně webu pro stránky na webu ASP.NET Web Pages (Razor).
> 
> Naučíte se:
> 
> - Jak spustit kód, který umožňuje nastavit hodnoty (globální hodnoty nebo nastavení pomocníka) pro všechny stránky v lokalitě.
> - Jak spustit kód, který umožňuje nastavit hodnoty pro všechny stránky ve složce.
> - Jak spustit kód před a po načtení stránky.
> - Odeslání chyb do centrální chybové stránky.
> - Postup přidání ověřování na všechny stránky ve složce.
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a>Verze softwaru použité v tomto kurzu
> 
> 
> - Webové stránky ASP.NET (Razor) 2
> - WebMatrix 3
> - Knihovna webových pomocníků ASP.NET (balíček NuGet)
>   
> 
> Tento kurz taky funguje s ASP.NET webovými stránkami 3 a Visual Studio 2013 (nebo Visual Studio Express 2013 pro web) s tím rozdílem, že nemůžete použít knihovnu webových pomocníků ASP.NET.

<a id="Adding_Website_Startup_Code"></a>
## <a name="adding-website-startup-code-for-aspnet-web-pages"></a>Přidání spouštěcího kódu webu pro webové stránky ASP.NET

Pro většinu kódu, který píšete na webových stránkách ASP.NET, může jednotlivé stránky obsahovat veškerý kód, který je pro tuto stránku vyžadován. Například pokud stránka pošle e-mailovou zprávu, je možné umístit veškerý kód pro tuto operaci na jednu stránku. To může zahrnovat kód pro inicializaci nastavení pro odesílání e-mailů (tj. pro server SMTP) a pro odesílání e-mailových zpráv.

V některých případech však můžete chtít spustit kód před spuštěním libovolné stránky v lokalitě. To je užitečné pro nastavení hodnot, které lze použít kdekoli v lokalitě (označované jako *globální hodnoty*). Některé pomocníky například vyžadují, abyste zadali hodnoty jako nastavení e-mailu nebo klíče účtu. Může být užitečné, pokud chcete tato nastavení zachovat v globálních hodnotách.

To můžete provést vytvořením stránky s názvem *\_AppStart. cshtml* v kořenovém adresáři webu. Pokud tato stránka existuje, spustí se při prvním vyžádání libovolné stránky v webu. Proto je dobrým místem pro spuštění kódu pro nastavení globálních hodnot. (Vzhledem k tomu, že *\_AppStart. cshtml* má předponu podtržítka, ASP.NET neposílá stránku do prohlížeče, i když si ji uživatelé vyžádají přímo.)

Následující diagram znázorňuje, jak stránka *\_AppStart. cshtml* funguje. Pokud se pro stránku objeví požadavek, a pokud se jedná o první požadavek na jakoukoli stránku v lokalitě, ASP.NET nejdřív zkontroluje\_, jestli existuje stránka *AppStart. cshtml* . V takovém případě se spustí veškerý kód na stránce *\_AppStart. cshtml* a následně se spustí požadovaná stránka.

![obrazu](18-customizing-site-wide-behavior/_static/image1.jpg)

## <a name="setting-global-values-for-your-website"></a>Nastavení globálních hodnot pro váš web

1. V kořenové složce webu WebMatrix vytvořte soubor s názvem *\_AppStart. cshtml*. Soubor musí být v kořenu webu.
2. Existující obsah nahraďte následujícím: 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample1.cshtml)]

    Tento kód ukládá hodnotu do slovníku `AppState`, který je automaticky dostupný pro všechny stránky v lokalitě. Všimněte si, že soubor *\_AppStart. cshtml* neobsahuje žádné značky. Stránka spustí kód a pak přesměruje na stránku, která byla původně vyžádána.

    > [!NOTE]
    > Buďte opatrní při vložení kódu do souboru *\_AppStart. cshtml* . Pokud dojde k jakýmkoli chybám v kódu v souboru *\_AppStart. cshtml* , web se nespustí.
3. V kořenové složce vytvořte novou stránku s názvem *APPNAME. cshtml*.
4. Nahraďte výchozí kód a kód následujícím kódem: 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample2.html)]

    Tento kód extrahuje hodnotu z objektu `AppState`, který jste nastavili na stránce *\_AppStart. cshtml* .
5. Spusťte stránku *APPNAME. cshtml* v prohlížeči. (Před spuštěním se ujistěte, že je stránka vybraná v pracovním prostoru **soubory** .) Na stránce se zobrazí globální hodnota. 

    ![obrazu](18-customizing-site-wide-behavior/_static/image2.jpg)

<a id="Setting_Values_For_Helpers"></a>
## <a name="setting-values-for-helpers"></a>Nastavení hodnot pro pomocníky

Dobrým použitím souboru *\_AppStart. cshtml* je nastavit hodnoty pro pomocníky, které používáte ve vaší lokalitě a které musí být inicializovány. Typické příklady jsou nastavení e-mailu pro pomocníka `WebMail` a soukromé a veřejné klíče pro pomocnou pomoc `ReCaptcha`. V takových případech můžete hodnoty nastavit jednou v *\_AppStart. cshtml* a potom jsou již nastaveny pro všechny stránky ve vaší lokalitě.

Tento postup vám ukáže, jak globálně nastavit `WebMail` nastavení. (Další informace o použití pomocníka `WebMail` najdete v tématu [Přidání e-mailu na web webových stránek ASP.NET](../getting-started/11-adding-email-to-your-web-site.md).)

1. Přidejte knihovnu webových pomocníků ASP.NET na web, jak je popsáno v [tématu Instalace pomocníků na webu ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=252372), pokud jste ho ještě nepřidali.
2. Pokud ještě nemáte soubor *\_AppStart. cshtml* , v kořenové složce webu vytvořte soubor s názvem *\_AppStart. cshtml*.
3. Do souboru *\_AppStart. cshtml* přidejte následující nastavení `WebMail`: 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample3.cshtml?highlight=2-7)]

    Upravte následující nastavení související s e-maily v kódu:

   - Nastavte `your-SMTP-host` na název serveru SMTP, ke kterému máte přístup.
   - Nastavte `your-user-name-here` na uživatelské jméno pro svůj účet serveru SMTP.
   - Nastavte `your-account-password` na heslo pro svůj účet serveru SMTP.
   - Nastavte `your-email-address-here` na vlastní e-mailovou adresu. Toto je e-mailová adresa, ze které se zpráva odesílá. (Někteří poskytovatelé e-mailu neumožňují zadat jinou adresu `From` a vaše uživatelské jméno bude používat jako `From`ová adresa.)

     Další informace o nastavení SMTP najdete v tématu [Konfigurace nastavení e-mailu](https://go.microsoft.com/fwlink/?LinkID=202899#configuring_email_settings) v článku [odesílání e-mailů z webu ASP.NET Web Pages (Razor)](https://go.microsoft.com/fwlink/?LinkID=202899) a [problémů s odesíláním e-mailů](https://go.microsoft.com/fwlink/?LinkId=253001#email) v [příručce pro řešení potíží s webovými stránkami ASP.NET](https://go.microsoft.com/fwlink/?LinkId=253001).
4. Uložte soubor *\_AppStart. cshtml* a zavřete ho.
5. V kořenové složce webu vytvořte novou stránku s názvem *TestEmail. cshtml*.
6. Existující obsah nahraďte následujícím: 

     [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample4.cshtml)]
7. Spusťte stránku *TestEmail. cshtml* v prohlížeči.
8. Vyplňte pole, abyste si sami poslali e-mailovou zprávu, a pak klikněte na **Odeslat**.
9. Zkontrolujte e-mail a ujistěte se, že jste se seznámili s touto zprávou.

Důležitou součástí tohoto příkladu je to, že nastavení, které obvykle neměníte – jako je název serveru SMTP a e-mailových přihlašovacích údajů, se nastavují v souboru *\_AppStart. cshtml* . Tímto způsobem je nemusíte znovu nastavovat na každé stránce, kam odesíláte e-mail. (I když Pokud z nějakého důvodu potřebujete tato nastavení změnit, můžete je nastavit individuálně na stránce.) Na stránce nastavte pouze hodnoty, které se obvykle mění pokaždé, například příjemce a tělo e-mailové zprávy.

<a id="Running_Code_Before_and_After"></a>
## <a name="running-code-before-and-after-files-in-a-folder"></a>Spuštění kódu před a za soubory ve složce

Stejně jako můžete použít *\_AppStart. cshtml* k zápisu kódu před stránky v lokalitě, můžete napsat kód, který se spustí před (a po) libovolné stránce v konkrétní složce. To je užitečné pro věci, jako je nastavení stejné stránky rozložení pro všechny stránky ve složce, nebo pro kontrolu, jestli je uživatel přihlášený před spuštěním stránky ve složce.

Pro stránky v určitých složkách můžete vytvořit kód v souboru s názvem *\_PageStart. cshtml*. Následující diagram znázorňuje, jak stránka *\_PageStart. cshtml* funguje. Když požadavek přichází na stránku, ASP.NET nejdřív zkontroluje stránku *\_AppStart. cshtml* a spustí ji. Pak ASP.NET ověří, zda je na stránce *\_PageStart. cshtml* , a pokud ano, spustí se. Potom spustí požadovanou stránku.

Na stránce *\_PageStart. cshtml* můžete určit, kde se má během zpracování požadovat spuštění požadované stránky, a to včetně metody `RunPage`. To vám umožní spustit kód, než se spustí požadovaná stránka, a potom po ní znovu. Pokud nezahrnete `RunPage`, spustí se veškerý kód v *\_PageStart. cshtml* a pak se požadovaná stránka automaticky spustí.

![obrazu](18-customizing-site-wide-behavior/_static/image3.jpg)

ASP.NET umožňuje vytvořit hierarchii souborů *. cshtml\_PageStart* . Můžete vložit *\_PageStart. cshtml* do kořenové složky lokality a do jakékoli podsložky. Po vyžádání stránky se spustí soubor *\_PageStart. cshtml* na nejvyšší úrovni (nejbližší k kořenovému adresáři webu), za nímž následuje *\_PageStart. cshtml* v další podčásti, a tak dále strukturu podsložky, dokud požadavek nedosáhne složky, která obsahuje požadovanou stránku. Po spuštění všech relevantních souborů *\_PageStart. cshtml* se spustí požadovaná stránka.

Například můžete mít následující kombinaci *\_PageStart. cshtml* Files a *Default. cshtml* File:

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample5.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample6.cshtml)]

[!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample7.cshtml)]

Při spuštění */myFolder/default.cshtml*se zobrazí následující:

[!code-console[Main](18-customizing-site-wide-behavior/samples/sample8.cmd)]

## <a name="running-initialization-code-for-all-pages-in-a-folder"></a>Spuštění inicializačního kódu pro všechny stránky ve složce

Vhodným použitím *\_PageStart. cshtml* je inicializovat stejnou stránku rozložení pro všechny soubory v jedné složce.

1. V kořenové složce vytvořte novou složku s názvem *InitPages*.
2. Ve složce *InitPages* na vašem webu vytvořte soubor s názvem *\_PageStart. cshtml* a nahraďte výchozí kód a kód následujícím kódem: 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample9.cshtml)]
3. V kořenovém adresáři webu vytvořte složku s názvem *Shared*.
4. Ve *sdílené* složce vytvořte soubor s názvem *\_Layout1. cshtml* a nahraďte výchozí kód a kód následujícím kódem: 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample10.cshtml)]
5. Ve složce *InitPages* vytvořte soubor s názvem *Content1. cshtml* a nahraďte stávající obsah následujícím: 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample11.html)]
6. Ve složce *InitPages* vytvořte jiný soubor s názvem *Content2. cshtml* a nahraďte výchozí kód následujícím kódem: 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample12.html)]
7. Spusťte *Content1. cshtml* v prohlížeči. 

    ![obrazu](18-customizing-site-wide-behavior/_static/image4.jpg)

    Když se spustí stránka *Content1. cshtml* , sada *\_PageStart. cshtml* nastaví `Layout` a také nastaví `PageData["MyBackground"]` na barvu. V *Content1. cshtml*se aplikuje rozložení a barva.
8. Zobrazí *Content2. cshtml* v prohlížeči. 

    Rozložení je stejné, protože obě stránky používají stejnou stránku rozložení a barvu, jak jsou inicializovány v *\_PageStart. cshtml*.

## <a name="using-_pagestartcshtml-to-handle-errors"></a>Použití \_PageStart. cshtml ke zpracování chyb

Dalším vhodným způsobem *\_souboru PageStart. cshtml* je vytvořit způsob, jak zpracovat chyby programování (výjimky), které mohou nastat na libovolné stránce s *příponou. cshtml* ve složce. Tento příklad ukazuje jeden ze způsobů, jak to provést.

1. V kořenové složce vytvořte složku s názvem *InitCatch*.
2. Ve složce *InitCatch* na vašem webu vytvořte soubor s názvem *\_PageStart. cshtml* a nahraďte existující značky a kód následujícím kódem: 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample13.cshtml)]

    V tomto kódu se pokusíte spustit požadovanou stránku explicitně voláním metody `RunPage` uvnitř bloku `try`. Pokud dojde k jakýmkoli chybám při programování na požadované stránce, spustí se kód uvnitř `catch` bloku. V tomto případě kód přesměruje na stránku (*Error. cshtml*) a předá název souboru, u kterého došlo k chybě v rámci adresy URL. (Stránku vytvoříte za chvíli.)
3. Ve složce *InitCatch* vašeho webu vytvořte soubor s názvem *Exception. cshtml* a nahraďte existující značky a kód následujícím kódem: 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample14.cshtml)]

    Pro účely tohoto příkladu, co děláte na této stránce, se při pokusu o otevření databázového souboru, který neexistuje, záměrně vytvoří chyba.
4. V kořenové složce vytvořte soubor s názvem *Error. cshtml* a nahraďte stávající značky a kód následujícím kódem: 

    [!code-html[Main](18-customizing-site-wide-behavior/samples/sample15.html)]

    Na této stránce výraz `@Request["source"]` Získá hodnotu z adresy URL a zobrazí ji.
5. Na panelu nástrojů klikněte na **Uložit**.
6. V prohlížeči spusťte *Exception. cshtml* . 

    ![obrazu](18-customizing-site-wide-behavior/_static/image5.jpg)

    Vzhledem k tomu, že dojde k chybě ve *výjimce. cshtml*, stránka *\_PageStart. cshtml* přesměruje na soubor *Error. cshtml* , který zobrazí zprávu.

    Další informace o výjimkách naleznete v tématu [Úvod do programování webových stránek ASP.NET pomocí syntaxe Razor](https://go.microsoft.com/fwlink/?LinkID=251587).

<a id="Using__PageStart.cshtml_to_Restrict_Folder_Access"></a>
## <a name="using-_pagestartcshtml-to-restrict-folder-access"></a>Omezení přístupu ke složkám pomocí \_PageStart. cshtml

Můžete také použít soubor *\_PageStart. cshtml* k omezení přístupu ke všem souborům ve složce.

1. V části WebMatrix vytvořte nový web pomocí možnosti **šablony z webu** .
2. Z dostupných šablon vyberte **Start site**.
3. V kořenové složce vytvořte složku s názvem *AuthenticatedContent*.
4. Ve složce *AuthenticatedContent* vytvořte soubor s názvem *\_PageStart. cshtml* a nahraďte existující značky a kód následujícím kódem: 

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample16.cshtml)]

    Kód začíná tím, že zabrání ukládání všech souborů v této složce do mezipaměti. (To je vyžadováno pro scénáře, jako jsou veřejné počítače, kde nechcete, aby byl jeden uživatel v mezipaměti k dispozici pro dalšího uživatele.) Dále kód určí, zda se uživatel přihlásil k webu předtím, než může zobrazit libovolnou stránku ve složce. Pokud uživatel není přihlášený, přesměruje kód na přihlašovací stránku. Přihlašovací stránka může uživatele vrátit na stránku, která byla původně vyžádána v případě, že zahrnete hodnotu řetězce dotazu s názvem `ReturnUrl`.
5. Vytvořte novou stránku ve složce *AuthenticatedContent* s názvem *Page. cshtml*.
6. Nahraďte výchozí kód následujícím kódem:  

    [!code-cshtml[Main](18-customizing-site-wide-behavior/samples/sample17.cshtml)]
7. V prohlížeči spusťte *stránku. cshtml* . Kód vás přesměruje na přihlašovací stránku. Před přihlášením se musíte zaregistrovat. Po registraci a přihlášení můžete přejít na stránku a zobrazit její obsah.

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a>Další prostředky

[Úvod do programování webových stránek ASP.NET pomocí syntaxe Razor](https://go.microsoft.com/fwlink/?LinkID=251587)

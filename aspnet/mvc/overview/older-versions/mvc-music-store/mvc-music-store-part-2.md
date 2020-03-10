---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: 'Část 2: řadiče | Microsoft Docs'
author: jongalloway
description: V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 2 pokrývá řadiče.
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: 9dc2226f4951d4bed122df37d35bbb94730a00ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559876"
---
# <a name="part-2-controllers"></a>2\. část: Kontrolery

o [Jan Galloway](https://github.com/jongalloway)

> Hudební úložiště MVC je výuková aplikace, která zavádí a vysvětluje krok za krokem, jak používat ASP.NET MVC a Visual Studio pro vývoj webů.  
>   
> Úložiště hudby MVC je zjednodušená ukázka implementace úložiště, která prodává hudební alba online a implementuje základní funkce pro správu webů, přihlašování uživatelů a nákupních košíků.  
>   
> V této sérii kurzů se podrobně povedou všechny kroky, které se provedly při vytváření ukázkové aplikace úložiště ASP.NET MVC pro hudební úložiště. Část 2 pokrývá řadiče.

V případě tradičních webových architektur jsou příchozí adresy URL obvykle mapovány na soubory na disku. Příklad: požadavek na adresu URL, například "/Products.aspx" nebo "/Products.php", může být zpracován souborem "Products. aspx" nebo "Products. php".

Webové architektury MVC mapují adresy URL na kód serveru trochu jiným způsobem. Namísto mapování příchozích adres URL na soubory místo toho namapujte adresy URL na metody třídy. Tyto třídy se nazývají "řadiče" a zodpovídají za zpracování příchozích požadavků HTTP, zpracování vstupu uživatele, načítání a ukládání dat a určení odpovědi, která se pošle zpátky klientovi (zobrazení HTML, stažení souboru, přesměrování na jiný). Adresa URL atd.).

## <a name="adding-a-homecontroller"></a>Přidání HomeController

Budeme začínat aplikaci pro hudební úložiště MVC přidáním třídy Controller, která bude zpracovávat adresy URL na domovské stránce našeho webu. Budeme dodržovat výchozí konvence pojmenování ASP.NET MVC a volat IT HomeController.

Klikněte pravým tlačítkem na složku Controllers v rámci Průzkumník řešení a vyberte Přidat a pak na Controller... systému

![](mvc-music-store-part-2/_static/image1.jpg)

Tím se zobrazí dialogové okno Přidat kontroler. Pojmenujte kontroler "HomeController" a stiskněte tlačítko Přidat.

![](mvc-music-store-part-2/_static/image1.png)

Tím se vytvoří nový soubor HomeController.cs s následujícím kódem:

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

Chcete-li začít co nejjednodušší, nahraďte metodu indexu jednoduchou metodou, která pouze vrátí řetězec. Provedeme dvě změny:

- Změna metody pro vrácení řetězce místo ActionResult
- Změnou příkazu return vraťte text Hello z domova.

Metoda by teď měla vypadat takto:

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a>Spuštění aplikace

Teď web spusťte. Můžeme spustit náš webový server a vyzkoušet web pomocí některého z následujících postupů:

- Vyberte položku nabídky ladění ⇨ spustit ladění.
- Klikněte na tlačítko se zelenou šipkou na panelu nástrojů ![](mvc-music-store-part-2/_static/image2.jpg)
- Použijte klávesovou zkratku F5.

Pomocí kteréhokoli z výše uvedených kroků se zkompiluje náš projekt a následně se spustí vývojový server ASP.NET, který je integrován do aplikace Visual Web Developer. V dolním rohu obrazovky se zobrazí oznámení o tom, že se spustil vývojový server ASP.NET a zobrazí se číslo portu, pod kterým je spuštěný.

![](mvc-music-store-part-2/_static/image2.png)

Visual Web Developer pak automaticky otevře okno prohlížeče, jehož adresa URL odkazuje na náš webový server. Umožní vám to rychle vyzkoušet naši webovou aplikaci:

![](mvc-music-store-part-2/_static/image3.png)

Dobře, to bylo poměrně rychlé – vytvořili jsme nový web, Přidali jsme tři linky a v prohlížeči máme text. Nerakety vědy, ale je to na začátku.

*Poznámka: Visual Web Developer zahrnuje vývojový server ASP.NET, který bude web spouštět na náhodném bezplatném čísle "port". Na snímku obrazovky výše je web spuštěný v `http://localhost:26641/`, takže používá port 26641. Vaše číslo portu se bude lišit. Když budeme v tomto kurzu pohovořit o adrese URL jako/Store/Browse, bude jít po čísle portu. Za předpokladu, že se číslo portu 26641, procházení na/Store/Browse znamená procházení na `http://localhost:26641/Store/Browse`.*

## <a name="adding-a-storecontroller"></a>Přidání StoreController

Přidali jsme jednoduchý HomeController, který implementuje domovskou stránku našeho webu. Teď přidáme další kontroler, který použijeme k implementaci funkce procházení našeho obchodu s hudbou. Náš kontroler úložiště bude podporovat tři scénáře:

- Stránka se seznamem hudebních žánrů v našem hudebním obchodě
- Stránka pro procházení, na které jsou uvedena všechna hudební alba v konkrétním žánru
- Stránka s podrobnostmi, která zobrazuje informace o konkrétním hudebním albu

Začneme přidáním nové třídy StoreController. Pokud jste to ještě neudělali, ukončete aplikaci tak, že zavřete prohlížeč nebo vyberete položku nabídky Ladit ⇨ zastavit ladění.

Nyní přidejte nové StoreController. Stejně jako u HomeController to provedeme tak, že kliknete pravým tlačítkem na složku Controllers v rámci Průzkumník řešení a vyberete položku nabídky přidat řadič&gt;Controller.

![](mvc-music-store-part-2/_static/image4.png)

Náš nový StoreController už obsahuje metodu "index". Pomocí této metody "index" implementujeme naši stránku se seznamem, kde jsou uvedeny všechny žánry v našem obchodě s hudbou. Přidáme také dvě další metody, které implementují dva další scénáře, které chceme StoreController zpracovat: Procházet a podrobnosti.

Tyto metody (index, procházení a podrobnosti) v rámci našeho kontroleru se nazývají "akce kontroleru" a protože jste už viděli metodu akce HomeController. index (), jejich úkolem je reagovat na požadavky na adresu URL a (obecně řečeno) zjistit, který obsah má se poslat zpátky v prohlížeči nebo uživateli, který adresu URL vyvolal.

Spustíme naši implementaci StoreController změnou metody theIndex () pro vrácení řetězce "Hello z Store. index ()" a my přidáme podobné metody pro Browse () a Details ():

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

Spusťte projekt znovu a procházejte následující adresy URL:

- /Store
- /Store/Browse
- /Store/Details

Přístup k těmto adresám URL vyvolá metody akcí v rámci našeho kontroleru a návratové odezvy řetězce:

![](mvc-music-store-part-2/_static/image5.png)

To je skvělé, ale jedná se o pouze konstantní řetězce. Pojďme je udělat dynamicky, aby z adresy URL převzali informace a zobrazili je ve výstupu stránky.

Nejdříve změníme metodu akce procházení, aby se z adresy URL načetla hodnota QueryString. To můžeme udělat přidáním parametru "Žánr" do naší metody akce. Když to provedeme, ASP.NET MVC při vyvolání automaticky předáte všechny parametry dotazu nebo formuláře odeslání s názvem "Žánr".

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

*Poznámka: pro úpravu vstupu uživatele používáme metodu Utility HttpUtility. HtmlEncode. To brání uživatelům v vkládání JavaScriptu do našeho zobrazení s odkazem jako/Store/Browse? Žánr =&lt;okno skriptu&gt;Window. Location = 'http://hackersite.com'&lt;/Script&gt;.*

Teď procházíme na/Store/Browse? Žánr = disco

![](mvc-music-store-part-2/_static/image6.png)

Pojďme dále změnit akci podrobností pro čtení a zobrazení vstupního parametru s názvem ID. Na rozdíl od předchozí metody nevložíme hodnotu ID jako parametr QueryString. Místo toho ho vložíme přímo do samotné adresy URL. Příklad:/Store/Details/5.

ASP.NET MVC nám umožňuje snadno to dělat bez nutnosti konfigurovat cokoli. Výchozí konvence směrování ASP.NET MVC je zacházet s segmentem adresy URL za názvem metody akce jako s parametrem s názvem "ID". Pokud vaše metoda Action má parametr s názvem ID, pak ASP.NET MVC automaticky předává segment adresy URL jako parametr.

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

Spusťte aplikaci a přejděte do/Store/Details/5:

![](mvc-music-store-part-2/_static/image7.png)

Pojďme si rekapitulace, co jsme doposud provedli:

- V aplikaci Visual Web Developer jsme vytvořili nový projekt ASP.NET MVC.
- Probrali jsme základní strukturu složek aplikace ASP.NET MVC.
- Zjistili jsme, jak náš web spustit pomocí vývojového serveru ASP.NET
- Vytvořili jsme dvě třídy kontroleru: HomeController a StoreController.
- Do našich řadičů jsme přidali metody akcí, které reagují na žádosti URL a vracejí text do prohlížeče.

> [!div class="step-by-step"]
> [Předchozí](mvc-music-store-part-1.md)
> [Další](mvc-music-store-part-3.md)

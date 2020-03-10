---
uid: web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-cs
title: Adresy URL na stránkách předlohyC#() | Microsoft Docs
author: rick-anderson
description: Řeší způsob, jakým se mohou adresy URL na stránce předlohy přerušit, protože soubor hlavní stránky je v jiném relativním adresáři než stránka obsahu. Vyhledává se při přenesení...
ms.author: riande
ms.date: 06/10/2008
ms.assetid: 48b58a18-5ea4-468c-b326-f35331b3e1e9
msc.legacyurl: /web-forms/overview/older-versions-getting-started/master-pages/urls-in-master-pages-cs
msc.type: authoredcontent
ms.openlocfilehash: 2551a5361256234883bb37e46e794037284445a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78585846"
---
# <a name="urls-in-master-pages-c"></a>Adresy URL stránek předloh (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/e/e/f/eef369f5-743a-4a52-908f-b6532c4ce0a4/ASPNET_MasterPages_Tutorial_04_CS.zip) nebo [stažení PDF](https://download.microsoft.com/download/8/f/6/8f6349e4-6554-405a-bcd7-9b094ba5089a/ASPNET_MasterPages_Tutorial_04_CS.pdf)

> Řeší způsob, jakým se mohou adresy URL na stránce předlohy přerušit, protože soubor hlavní stránky je v jiném relativním adresáři než stránka obsahu. Podívá se na adresy URL prostřednictvím ~ v deklarativní syntaxi a pomocí kódu programu ResolveUrl a ResolveClientUrl. (Podívejte se také na

## <a name="introduction"></a>Úvod

Ve všech příkladech, které jsme doposud viděli, se hlavní stránka a stránky obsahu nacházely ve stejné složce (kořenová složka webu). Neexistuje proto žádný důvod, proč se hlavní a stránky obsahu musí nacházet ve stejné složce. Můžete vytvářet stránky obsahu v podsložkách. Podobně můžete vytvořit složku `~/MasterPages/`, do které umístíte stránky předlohy vaší lokality.

Jedním z možných problémů s umístěním hlavní stránky a stránkami obsahu v různých složkách jsou poškozené adresy URL. Pokud stránka předlohy obsahuje relativní adresy URL v hypertextových odkazech, obrázcích nebo jiných prvcích, odkaz nebude platný pro stránky obsahu, které se nacházejí v jiné složce. V tomto kurzu se podíváme na zdroj těchto potíží i na alternativní řešení.

## <a name="the-problem-with-relative-urls"></a>Problém s relativními adresami URL

Adresa URL na webové stránce je označována jako *relativní adresa URL* , pokud umístění prostředku, na který odkazuje, je relativní vzhledem k umístění webové stránky ve struktuře složek webu. Všechny adresy URL, které nezačínají předním lomítkem (`/`) nebo protokol (například `http://`), jsou relativní vzhledem k tomu, že prohlížeč je vyhodnocený v závislosti na umístění webové stránky, která obsahuje adresu URL.

Náš web má například složku `~/Images/` s jedním souborem obrázku, `PoweredByASPNET.gif`. Soubor stránky předlohy `Site.master` obsahuje `<img>` prvek v `footerContent` oblasti s následujícím kódem:

[!code-html[Main](urls-in-master-pages-cs/samples/sample1.html)]

Hodnota atributu `src` v prvku `<img>` je relativní adresa URL, protože nezačíná `/` ani `http://`. V krátkém případě hodnota atributu `src` instruuje prohlížeč, aby hledal v podsložce `Images` pro soubor s názvem `PoweredByASPNET.gif`.

Při návštěvě stránky obsahu se výše uvedený kód pošle přímo do prohlížeče. Chvíli počkejte, než se navštíví `About.aspx` a zobrazte zdroj HTML odeslaný do prohlížeče. Zjistíte, že do prohlížeče byl odeslán přesně stejný kód na stránce předlohy.

[!code-html[Main](urls-in-master-pages-cs/samples/sample2.html)]

Pokud je stránka obsahu v kořenové složce (jak je `About.aspx`), vše funguje podle očekávání, protože složka `Images` relativní ke kořenové složce. Pokud se ale stránka obsahu nachází v jiné složce než stránka předlohy, budou se tyto věci dělit. K tomu je potřeba vytvořit podsložku s názvem `Admin`. Dále přidejte stránku obsahu s názvem `Default.aspx` do složky `Admin` a ujistěte se, že novou stránku navážete na `Site.master` hlavní stránku.

> [!NOTE]
> V kurzu [*zadání názvu, meta značek a dalších záhlaví HTML v kurzu hlavní stránky*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) jsme vytvořili vlastní třídu základní stránky s názvem `BasePage`, která automaticky nastaví název stránky obsahu (pokud nebyl explicitně přiřazený). Nezapomeňte, že nově vytvořená třída kódu na pozadí je odvozená od `BasePage`, aby mohla využívat tuto funkci.

Po vytvoření této stránky obsahu by váš Průzkumník řešení měl vypadat podobně jako obrázek 1.

![Do projektu se přidala nová složka a stránka ASP.NET.](urls-in-master-pages-cs/_static/image1.png)

**Obrázek 01**: do projektu se přidala nová složka a stránka ASP.NET.

Dále aktualizujte soubor `Web.sitemap` tak, aby zahrnoval novou položku `<siteMapNode>` pro tuto lekci. Následující kód XML ukazuje kompletní kód `Web.sitemap`, který nyní obsahuje přidání třetího `<siteMapNode>` elementu.

[!code-xml[Main](urls-in-master-pages-cs/samples/sample3.xml)]

Nově vytvořená `Default.aspx` stránka by měla obsahovat čtyři ovládací prvky obsahu odpovídající čtyřm ovládacím prvkům ContentPlaceHolders v `Site.master`. Přidejte nějaký text k ovládacímu prvku obsahu odkazujícímu na `MainContent` ContentPlaceHolder a potom navštivte stránku pomocí prohlížeče. Jak ukazuje obrázek 2, prohlížeč nemůže najít soubor bitové kopie `PoweredByASPNET.gif`. Co se sem zaměří?

Stránka `~/Admin/Default.aspx` obsahu je pro `footerContent` oblast odeslána stejným HTML jako stránka `About.aspx`:

[!code-html[Main](urls-in-master-pages-cs/samples/sample4.html)]

Vzhledem k tomu, že atribut `src` elementu `<img>` je relativní adresa URL, prohlížeč se pokusí vyhledat složku `Images` relativní vzhledem k umístění složky webové stránky. Jinými slovy, prohlížeč hledá soubor bitové kopie `Admin/Images/PoweredByASPNET.gif`.

[![soubor obrázku PoweredByASPNET. gif nejde najít.](urls-in-master-pages-cs/_static/image3.png)](urls-in-master-pages-cs/_static/image2.png)

**Obrázek 02**: Nepodařilo se najít soubor bitové kopie `PoweredByASPNET.gif` ([kliknutím zobrazíte obrázek v plné velikosti](urls-in-master-pages-cs/_static/image4.png)).

### <a name="replacing-relative-urls-with-absolute-urls"></a>Nahrazení relativních adres URL absolutními adresami URL

Opakem relativní adresy URL je *absolutní adresa URL*, která začíná lomítkem (`/`) nebo protokolem jako `http://`. Vzhledem k tomu, že absolutní adresa URL určuje umístění prostředku ze známého pevného bodu, je stejná absolutní adresa URL platná na libovolné webové stránce, bez ohledu na umístění webové stránky ve struktuře složek webu.

Pro nápravu poškozeného obrázku, který je znázorněn na obrázku 2, je nutné aktualizovat atribut `src` elementu `<img>` tak, aby místo relativního typu použil absolutní adresu URL. Chcete-li určit správnou absolutní adresu URL, navštivte jednu z webových stránek na webu a zkontrolujte adresní řádek. Jak ukazuje adresní řádek na obrázku 2, plně kvalifikovaná cesta k webové aplikaci je `http://localhost:3908/ASPNET_MasterPages_Tutorial_04_CS/`. Proto můžeme aktualizovat atribut `src` elementu `<img>` na jednu z následujících dvou absolutních adres URL:

- `/ASPNET_MasterPages_Tutorial_04_CS/Images/PoweredByASPNET.gif`
- `http://localhost:3908/ASPNET_MasterPages_Tutorial_04_CS/Images/PoweredByASPNET.gif`

Chvíli počkejte, než se aktualizuje atribut `<img>` elementu `src` na absolutní adresu URL pomocí jedné z výše uvedených formulářů a pak na stránce `~/Admin/Default.aspx` prostřednictvím prohlížeče. Tentokrát prohlížeč správně najde a zobrazí soubor obrázku `PoweredByASPNET.gif` (viz obrázek 3).

[![se teď zobrazí obrázek PoweredByASPNET. gif.](urls-in-master-pages-cs/_static/image6.png)](urls-in-master-pages-cs/_static/image5.png)

**Obrázek 03**: zobrazí se nyní `PoweredByASPNET.gif` obrázek ([kliknutím zobrazíte obrázek v plné velikosti](urls-in-master-pages-cs/_static/image7.png)).

I když pevné kódování na absolutní adrese URL funguje, pevně Couples svůj kód HTML na server a umístění složky webu, které se může změnit. Použití absolutní adresy URL formuláře `http://localhost:3908/...` je poměrně křehký, protože číslo portu předcházející `localhost` je vybráno automaticky pokaždé, když se spustí vývojový webový server sady Visual Studio. Podobně platí, že část `http://localhost` je platná pouze při testování místně. Po nasazení kódu na provozní server se základ adresy URL změní na něco jiného, jako `http://www.yourserver.com`. Absolutní adresa URL ve formuláři `/ASPNET_MasterPages_Tutorial_04_CS/...` také trpí stejným brittleness, protože často tato cesta k této aplikaci se mezi vývojovými a provozními servery liší.

Dobrá zpráva je, že ASP.NET nabízí metodu pro generování platné relativní adresy URL za běhu.

## <a name="usingandresolveclienturl"></a>Používání`~`a`ResolveClientUrl`

Místo pevného kódu absolutní adresa URL umožňuje vývojářům stránky použít vlnovku (`~`) k označení kořenového adresáře webové aplikace. Například dříve v tomto kurzu jsem v textu použili notaci `~/Admin/Default.aspx`, který odkazuje na stránku `Default.aspx` ve složce `Admin`. `~` označuje, že složka `Admin` je podsložkou kořenového adresáře webové aplikace.

[Metoda`ResolveClientUrl`](https://msdn.microsoft.com/library/system.web.ui.control.resolveclienturl.aspx) třídy `Control` přebírá adresu URL a upravuje ji na relativní adresu URL, která je vhodná pro webovou stránku, na které se ovládací prvek nachází. Například volání `ResolveClientUrl("~/Images/PoweredByASPNET.gif")` z `About.aspx` vrátí `Images/PoweredByASPNET.gif`. Voláním z `~/Admin/Default.aspx`však vrátí `../Images/PoweredByASPNET.gif`.

> [!NOTE]
> Vzhledem k tomu, že všechny ovládací prvky serveru ASP.NET jsou odvozeny od třídy `Control`, všechny serverové ovládací prvky mají přístup k metodě `ResolveClientUrl`. I třída `Page` je odvozena od `Control` třídy, což znamená, že tuto metodu lze použít přímo ze tříd kódu na pozadí ASP.NET stránek.

### <a name="usingin-the-declarative-markup"></a>Použití`~`v deklarativní značce

Některé webové ovládací prvky ASP.NET obsahují vlastnosti související s adresou URL: ovládací prvek hypertextový odkaz má vlastnost `NavigateUrl`; ovládací prvek obrázek má vlastnost `ImageUrl`; a tak dále. Při vykreslení tyto ovládací prvky předají hodnoty vlastností související s adresou URL do `ResolveClientUrl`. V důsledku toho, pokud tyto vlastnosti obsahují `~` k určení kořenového adresáře webové aplikace, adresa URL bude změněna na platnou relativní adresu URL.

Mějte na paměti, že `~` transformují pouze ovládací prvky serveru ASP.NET ve vlastnostech souvisejících s adresou URL. Pokud se `~` objeví ve statickém kódu HTML, jako je například `<img src="~/Images/PoweredByASPNET.gif" />`, modul ASP.NET odesílá `~` do prohlížeče spolu se zbytkem obsahu HTML. Prohlížeč předpokládá, že `~` je součástí adresy URL. Například pokud prohlížeč obdrží značku, `<img src="~/Images/PoweredByASPNET.gif" />` předpokládá, že existuje podsložka s názvem `~` s podsložkou `Images` obsahující soubor bitové kopie `PoweredByASPNET.gif`.

Chcete-li opravit označení obrázku v `Site.master`, nahraďte existující prvek `<img>` webovým ovládacím prvkem ASP.NET Image. Nastavte `ID` webového ovládacího prvku obrázek na `PoweredByImage`, jeho vlastnost `ImageUrl` na `~/Images/PoweredByASPNET.gif`a jeho vlastnost `AlternateText` na "Power by ASP.NET!".

[!code-aspx[Main](urls-in-master-pages-cs/samples/sample5.aspx)]

Po provedení této změny na stránce předlohy znovu přejděte na stránku `~/Admin/Default.aspx`. Tentokrát se `PoweredByASPNET.gif` obrázkový soubor na stránce zobrazuje (viz obrázek 3). Při vykreslení webového ovládacího prvku obrázek používá metodu `ResolveClientUrl` k překladu hodnoty vlastnosti `ImageUrl`. V `~/Admin/Default.aspx` `ImageUrl` převede na odpovídající relativní adresu URL, jak ukazuje následující fragment kódu HTML:

[!code-html[Main](urls-in-master-pages-cs/samples/sample6.html)]

> [!NOTE]
> Kromě toho, že se používá ve vlastnostech webového ovládacího prvku založeném na adrese URL, lze `~` použít také při volání metod `Response.Redirect` a `Server.MapPath`, a to mimo jiné. Kromě toho může být metoda `ResolveClientUrl` vyvolána přímo z deklarativní značky ASP.NET nebo hlavní stránky, pokud je to potřeba; viz položka blogu [Fritz](https://www.pluralsight.com/blogs/fritz/), která [používá `ResolveClientUrl` v kódu](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx).

## <a name="fixing-the-master-pages-remaining-relative-urls"></a>Oprava zbývajících relativních adres URL stránky předlohy

Kromě prvku `<img>` v `footerContent`, kterou jsme právě opravili, stránka předlohy obsahuje ještě jednu relativní adresu URL, která vyžaduje naši pozornost. Oblast `topContent` obsahuje odkazy "kurzy stránek předlohy", které odkazují na `Default.aspx`.

[!code-html[Main](urls-in-master-pages-cs/samples/sample7.html)]

Vzhledem k tomu, že je tato adresa URL relativní, odešle uživatel stránku `Default.aspx` ve složce stránky obsahu, na které se Návštěvníci nacházejí. Chcete-li, aby tento odkaz vždy odkazoval na `Default.aspx` v kořenové složce, musíme nahradit prvek `<a>` webovým ovládacím prvkem hypertextový odkaz, aby bylo možné použít zápis `~`.

Odeberte kód prvku `<a>` a přidejte ovládací prvek hypertextový odkaz na místo. Nastavte `ID` hypertextového odkazu na `lnkHome`, jeho vlastnost `NavigateUrl` na `~/Default.aspx`a vlastnost `Text` na "kurzy stránek předlohy".

[!code-aspx[Main](urls-in-master-pages-cs/samples/sample8.aspx)]

A to je vše! V tomto okamžiku jsou všechny adresy URL na naší hlavní stránce správně založené na tom, kde jsou vykresleny pomocí stránky obsahu bez ohledu na to, ve kterých složkách se stránka předlohy a stránka obsahu nacházejí.

### <a name="automatic-url-resolution-in-theheadsection"></a>Automatické rozlišení adresy URL v části`<head>`

V kurzu [*vytváření rozložení na úrovni webu pomocí stránek*](creating-a-site-wide-layout-using-master-pages-cs.md) jsme do `Styles.css` souboru v `<head>` oblasti přidali `<link>`:

[!code-aspx[Main](urls-in-master-pages-cs/samples/sample9.aspx)]

I když je atribut `href` elementu `<link>` relativní, je automaticky převeden na odpovídající cestu za běhu. Jak jsme probrali v kurzu [*zadání nadpisu, meta značek a dalších hlaviček HTML v kurzu hlavní stránky*](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md) , je `<head>` oblast ve skutečnosti ovládací prvek na straně serveru, který umožňuje upravovat obsah svých vnitřních ovládacích prvků při jejich vykreslování.

Pokud to chcete ověřit, přejděte na stránku `~/Admin/Default.aspx` a zobrazte zdroj HTML odeslaný do prohlížeče. Jak ukazuje následující fragment kódu, `href` atribut `<link>` elementu byl automaticky upraven na odpovídající relativní adresu URL `../Styles.css`.

[!code-html[Main](urls-in-master-pages-cs/samples/sample10.html)]

## <a name="summary"></a>Souhrn

Stránky předlohy velmi často obsahují odkazy, obrázky a další externí prostředky, které je třeba zadat pomocí adresy URL. Vzhledem k tomu, že stránka předloh a stránky obsahu nemusí existovat ve stejné složce, je důležité se zdržet používání relativních adres URL. I když je možné použít pevně kódované absolutní adresy URL, tak, aby se tak těsně Couples absolutní adresa URL webové aplikace. Pokud se absolutní adresa URL mění – stejně jako při přesunu nebo nasazení webové aplikace, nezapomeňte se vrátit zpět a aktualizovat absolutní adresy URL.

Ideálním přístupem je použití vlnovku (`~`) k označení kořene aplikace. ASP.NET webové ovládací prvky, které obsahují vlastnosti související s adresou URL, mapují `~` do kořenového adresáře aplikace za běhu. Interně webové ovládací prvky používají metodu `ResolveClientUrl` třídy `Control` k vygenerování platného relativního URL. Tato metoda je veřejná a dostupná z každého serverového ovládacího prvku (včetně třídy `Page`), takže ji můžete použít programově z vašich tříd kódu na pozadí, pokud je to potřeba.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Stránky předlohy v ASP.NET](http://www.odetocode.com/Articles/419.aspx)
- [Adresa URL pro přenesení na hlavní stránku](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/masterpages/default.aspx#urls)
- [Použití `ResolveClientUrl` ve značkách](https://www.pluralsight.com/blogs/fritz/archive/2006/02/06/18596.aspx)

### <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 3,5 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Scott se dá kontaktovat [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky

Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com).

> [!div class="step-by-step"]
> [Předchozí](specifying-the-title-meta-tags-and-other-html-headers-in-the-master-page-cs.md)
> [Další](control-id-naming-in-content-pages-cs.md)

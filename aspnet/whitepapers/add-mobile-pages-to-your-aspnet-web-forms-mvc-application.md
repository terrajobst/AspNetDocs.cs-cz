---
uid: whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application
title: 'Postupy: Přidání mobilních stránek do webových formulářů ASP.NET/aplikace MVC | Microsoft Docs'
author: rick-anderson
description: Tento postup popisuje různé způsoby, jak vydávat stránky optimalizované pro mobilní zařízení z webových formulářů ASP.NET/aplikace MVC a navrhuje architekturu a...
ms.author: riande
ms.date: 01/20/2011
ms.assetid: 3124f28e-cc32-418a-afe3-519fa56f4c36
msc.legacyurl: /whitepapers/add-mobile-pages-to-your-aspnet-web-forms-mvc-application
msc.type: content
ms.openlocfilehash: 63c555358d06a9506bb5c8c993800c3307108192
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78572735"
---
# <a name="how-to-add-mobile-pages-to-your-aspnet-web-forms--mvc-application"></a>Postup: Přidání mobilních stránek do webových formulářů ASP.NET/aplikace MVC

> **Platí pro**
> 
> - Webové formuláře ASP.NET verze 4,0
> - ASP.NET MVC verze 3,0
> 
> **Souhrn**
> 
> Tento postup popisuje různé způsoby, jak vydávat stránky optimalizované pro mobilní zařízení z webových formulářů ASP.NET/aplikace MVC, a navrhuje problémy architektury a návrhu, které je potřeba vzít v úvahu při zaměření na širokou škálu zařízení. Tento dokument také vysvětluje, proč jsou ASP.NET mobilní ovládací prvky z ASP.NET 2,0 až 3,5 a popisuje některé moderní alternativy.

## <a name="contents"></a>Obsah

- Přehled
- Možnosti architektury
- Detekce prohlížečů a zařízení
- Jak mohou aplikace webových formulářů ASP.NET prezentovat stránky pro mobilní zařízení
- Jak aplikace ASP.NET MVC můžou prezentovat stránky pro mobilní zařízení
- Další zdroje

Ukázky kódu ke stažení, které demonstrují tyto techniky White paper pro ASP.NET webové formuláře i MVC, najdete v tématu [Mobile Apps & weby pomocí ASP.NET](https://docs.microsoft.com/aspnet/mobile/overview).

## <a name="overview"></a>Přehled

Mobilní zařízení – smartphony, telefony s funkcemi a tablety – pro přístup k webu můžete dál rozrůstat v oblíbenosti. Pro mnoho webových vývojářů a web orientovaných společností to znamená, že je stále důležitější zajistit pro návštěvníky používání těchto zařízení skvělý zážitek z procházení.

### <a name="how-earlier-versions-of-aspnet-supported-mobile-browsers"></a>Jak dřívější verze ASP.NET podporují mobilní prohlížeče

ASP.NET verze 2,0 až 3,5 zahrnovaly *ASP.NET mobilní ovládací prvky*: sadu serverových ovládacích prvků pro mobilní zařízení v sestavení *System. Web. Mobile. dll* a v oboru názvů *System. Web. UI. MobileControls* . Sestavení je stále součástí ASP.NET 4, ale je zastaralé. Vývojářům se doporučuje migrovat na více moderních přístupů, jako jsou ty popsané v tomto dokumentu.

Důvodem, proč jsou ASP.NET mobilní ovládací prvky označeny jako zastaralé, je, že jejich návrh se orientuje na mobilní telefony, které byly běžné přibližně 2005 a starší. Ovládací prvky jsou hlavně navržené pro vykreslení WML nebo cHTML značek (místo obyčejného HTML) pro prohlížeče WAP tohoto období. Ale WAP, WML a cHTML už nejsou relevantní pro většinu projektů, protože HTML se teď stal jazykem všudypřítomný Markup Language pro mobilní a desktopové prohlížeče.

### <a name="the-challenges-of-supporting-mobile-devices-today"></a>Výzvy k podpoře mobilních zařízení ještě dnes

I když v mobilních prohlížečích teď skoro podporuje HTML, pořád se při vytváření skvělého prostředí pro procházení mobilních zařízení projeví i mnoho výzev:

- ***Velikost obrazovky*** – mobilní zařízení se výrazně liší ve formě a jejich obrazovky jsou často mnohem menší než stolní monitory. Proto možná budete muset pro ně navrhovat zcela různá rozložení stránek.
- ***Metody zadávání*** – některá zařízení mají klávesnice, některé mají tablety, jiné používají dotykové ovládání. Možná budete muset zvážit několik navigačních mechanismů a metod zadávání dat.
- ***Dodržování standardů*** – mnoho mobilních prohlížečů nepodporuje nejnovější standardy HTML, CSS a JavaScript.
- ***Šířka pásma*** – mobilní data v síti se liší v neobvyklém provozu a někteří koncoví uživatelé jsou tarify, které účtují až megabajtů.

Není k dispozici žádné řešení s jedním velikostí. vaše aplikace bude muset vypadat a chovat se odlišně v závislosti na zařízení, které k němu přistupuje. V závislosti na tom, jakou úroveň mobilní podpory požadujete, může to být větší výzva pro webové vývojáře, než je plocha "konflikty prohlížeče".

Vývojáři, kteří se přistupují k podpoře mobilních prohlížečů poprvé, často považují za důležité, aby podporovali nejnovější a nejpropracovanější smartphony (např. Windows Phone 7, iPhone nebo Android), třeba kvůli tomu, že vývojáři často vlastní takové signalizac. Avšak levnější telefony jsou stále extrémně populární a jejich vlastníci je používají k procházení webu – zejména v zemích, ve kterých je snazší mobilní telefony získat, než širokopásmové připojení. Vaše firma bude muset rozhodnout, jaké množství zařízení bude podporovat, a to zvážením jeho pravděpodobných zákazníků. Pokud vytváříte online brožuru pro luxus Health Spa, můžete učinit obchodní rozhodnutí jenom pro účely cílení na pokročilé smartphony, zatímco Pokud vytváříte systém rezervace lístků pro kino, pravděpodobně budete potřebovat účet pro návštěvníky s méně výkonnými funkcemi. telefonu.

## <a name="architectural-options"></a>Možnosti architektury

Než se dostanete ke konkrétním technickým podrobnostem o webových formulářích ASP.NET nebo MVC, pamatujte, že vývojáři webu mají všeobecně tři hlavní možné možnosti pro podporu mobilních prohlížečů:

1. ***Nedělat nic –*** Můžete jednoduše vytvořit standardní webovou aplikaci orientovanou na plochu, která se spoléhá na mobilní prohlížeče a vykreslit je přijatelné. 

    - **Advantage**: Jedná se o možnost nejlevnější k implementaci a údržbě – žádná další práce
    - **Nevýhody**: poskytuje nejhorší prostředí pro koncové uživatele: 

        - Nejnovější smartphony můžou váš kód HTML vykreslovat stejně jako desktopový prohlížeč, ale uživatelé budou pořád nuceně přiblížit a posouvat vodorovně a svisle a využívat obsah na malé obrazovce. To je mnohem z optimálního.
        - Starší zařízení a telefony funkcí se nemusí podařit vykreslit vaše značky uspokojivým způsobem.
        - I na nejnovějších zařízeních tabletu (jejichž obrazovky můžou být stejně velká jako obrazovky přenosné počítače), platí různá pravidla interakce. Dotykové ovládání funguje nejlépe s většími tlačítky a vazbami, které jsou dále roztaženy, a neexistuje žádný způsob, jak ukazatel myši nakládat na rozevírací nabídku.
2. ***Řešení problému na klientovi* –** pečlivé používání šablon stylů CSS a [progresivního vylepšení](http://en.wikipedia.org/wiki/Progressive_enhancement) vám umožní vytvořit značky, styly a skripty, které se přizpůsobí libovolnému prohlížeči. Například pomocí [multimediálních dotazů šablon stylů CSS 3](http://www.w3.org/TR/2010/CR-css3-mediaqueries-20100727/)můžete vytvořit rozložení s více sloupci, které změní na jedno rozložení sloupce na zařízeních, jejichž obrazovky jsou užší než zvolená prahová hodnota. 

    - **Advantage**: optimalizuje vykreslování pro konkrétní zařízení, které se používá, a to i pro neznámá budoucí zařízení podle toho, jaké charakteristiky obrazovky a vstupu mají.
    - **Výhoda**: snadno můžete sdílet logiku na straně serveru napříč všemi typy zařízení – minimální duplicita kódu nebo úsilí.
    - **Nevýhody**: mobilní zařízení se liší od stolních zařízení, ve kterých můžete chtít, aby se vaše mobilní stránky zcela lišily od stránek na ploše, které zobrazují různé informace. Tyto variace můžou být neefektivní nebo neumožňují dosáhnout robustních pouze prostřednictvím šablon stylů CSS, zejména s ohledem na to, jak nekonzistentně starší zařízení interpretují pravidla stylů CSS. To platí zejména pro atributy CSS 3.
    - **Nevýhody**: poskytuje žádnou podporu pro různé logiky na straně serveru a pracovní postupy pro různá zařízení. Nemůžete například implementovat zjednodušený pracovní postup rezervace nákupního košíku pro mobilní uživatele prostřednictvím šablon stylů CSS samostatně.
    - **Nevýhody**: neefektivní využití šířky pásma. Je možné, že budete muset přenést značky a styly, které se vztahují na všechna možná zařízení, a to i v případě, že cílové zařízení použije jenom podmnožinu těchto informací.
3. ***Řešení problému na serveru* –** Pokud váš server ví, k čemu má zařízení přístup, nebo alespoň jeho vlastnosti, jako je například velikost obrazovky a vstupní metoda a zda se jedná o mobilní zařízení – může spustit jinou logiku a výstup jiné kódování HTML. 

    - **Výhody:** Maximální flexibilita. Neexistuje žádné omezení na to, kolik je možné měnit logiku na straně serveru pro mobilní zařízení, nebo optimalizovat vaše značky pro požadované rozložení pro konkrétní zařízení.
    - **Výhody:** Efektivní využití šířky pásma. Je nutné přenést pouze informace o značkách a stylech, které budou cílové zařízení používat.
    - **Nevýhody:** Někdy vynutí opakování úsilí nebo kódu (např. vytváření podobných a mírně odlišných kopií webových formulářů nebo zobrazení MVC). Pokud je to možné, provedete si běžnou logiku na podkladovou vrstvu nebo službu, ale stále i některé části kódu uživatelského rozhraní nebo značky mohou být duplikovány a poté udržovány paralelně.
    - **Nevýhody:** Detekce zařízení není triviální. Vyžaduje seznam nebo databázi známých typů zařízení a jejich charakteristiky (které nemusí vždy být zcela v aktuálním stavu) a nemají zaručené přesné párování všech příchozích požadavků. Tento dokument popisuje některé možnosti a jejich nástrah později.

Pro dosažení nejlepších výsledků většina vývojářů potřebuje kombinovat možnosti (2) a (3). Drobné stylistické rozdíly jsou na straně klienta nejlépe přizpůsobené pomocí šablon stylů CSS nebo dokonce i JavaScriptu, zatímco hlavní rozdíly v datech, pracovních postupech nebo značkách jsou v kódu na straně serveru nejefektivnější.

### <a name="this-paper-focuses-on-server-side-techniques"></a>Tento dokument se zaměřuje na techniky na straně serveru.

Vzhledem k tomu, že webové formuláře ASP.NET a MVC jsou hlavně technologiemi na straně serveru, tento dokument White Paper se soustředí na techniky na straně serveru, které vám umožní vydávat různé značky a logiku pro mobilní prohlížeče. Samozřejmě to můžete také kombinovat s jakoukoli technikou na straně klienta (například dotazy na média CSS 3, progresivní navýšení JavaScript), ale to je více věcí pro návrh webu než ASP.NET vývoj.

## <a name="browser-and-device-detection"></a>Detekce prohlížečů a zařízení

Klíčové předpoklady pro všechny techniky na straně serveru pro podporu mobilních zařízení spočívá v tom, jaké zařízení vaše návštěvník používá. Ve skutečnosti je ještě lepší, než když znáte výrobce a model číslo tohoto zařízení, aby znal *charakteristiky* zařízení. Mezi vlastnosti může patřit:

- Je mobilní zařízení?
- Input – metoda (myš/klávesnice, dotykové ovládání, klávesnice, pákový ovladač,...)
- Velikost obrazovky (fyzicky a v pixelech)
- Podporovaná média a formáty dat
- Atd.

Je lepší učinit rozhodnutí na základě charakteristik, než je číslo modelu, protože pak budete lépe vybaveni pro zpracování budoucích zařízení.

### <a name="using-aspnets-built-in-browser-detection-support"></a>Pomocí ASP. Podpora detekce integrovaného prohlížeče sítě

Webové formuláře ASP.NET a vývojáři MVC můžou okamžitě zjistit důležité charakteristiky v navštíveném prohlížeči, a to zkontrolováním vlastností objektu *Request. browser* . Podívejte se například na

- Request.Browser.IsMobileDevice
- Request.Browser.MobileDeviceManufacturer, Request.Browser.MobileDeviceModel
- Request. browser. ScreenPixelsWidth
- Request.Browser.SupportsXmlHttp
- ...a mnoho dalších

Platforma ASP.NET se na pozadí shoduje s hlavičkou příchozích *uživatelských agentů* (UA) http proti regulárním výrazům v sadě souborů XML s definicí prohlížeče. Ve výchozím nastavení platforma obsahuje definice pro řadu běžných mobilních zařízení a můžete přidat vlastní soubory definice prohlížeče pro jiné, které chcete rozpoznat. Další podrobnosti najdete v tématu [ovládací prvky webového serveru MSDN page ASP.NET a možnosti prohlížeče](https://msdn.microsoft.com/library/x3k2ssx2.aspx).

### <a name="using-the-wurfl-device-database-via-51degreesmobi-foundation"></a>Používání databáze zařízení WURFL prostřednictvím 51Degrees.mobi Foundation

ASP. Podpora vyhledávání v integrovaném prohlížeči sítě pro spoustu aplikací bude stačit, existují dva hlavní případy, kdy nemusí být k dispozici:

- ***Chcete rozpoznat nejnovější zařízení***(bez ručního vytváření definičních souborů prohlížeče). Upozorňujeme, že soubory definic prohlížeče .NET 4 nejsou dostatečně nedávné pro rozpoznávání Windows Phone 7, telefonů s Androidem, Operau mobilní prohlížeče nebo Apple iPady.
- ***Potřebujete podrobnější informace o možnostech zařízení***. Možná budete potřebovat vědět o metodě vstupu zařízení (např. dotykové ovládání) nebo o tom, jaké formáty zvuku prohlížeč podporuje. Tyto informace nejsou k dispozici v standardních definičních souborech prohlížeče.

[Projekt WURFL ( *Wireless Universal Resource File* )](http://wurfl.sourceforge.net/) udržuje mnohem aktuálnější a podrobné informace o mobilních zařízeních, která se v současnosti používají.

Skvělé novinky pro vývojáře na platformě .NET jsou v prostředí ASP. Funkce detekce prohlížeče sítě je rozšiřitelná, takže je možné ji rozšířit, aby se tyto problémy vyřešily. Do projektu můžete například přidat Open Source knihovnu [*51Degrees.mobi Foundation*](https://github.com/51Degrees/dotNET-Device-Detection) . Je to ASP.NET IHttpModule nebo poskytovatel schopností prohlížeče (použitelné pro webové formuláře i aplikace MVC), které přímo čtou WURFL data a zavěsí je do ASP. Mechanizmus detekce vestavěného prohlížeče sítě. Po instalaci modulu *Request. browser* bude náhle obsahovat přesnější a podrobné informace: správně rozpozná mnoho dříve zmíněných zařízení a zobrazí seznam jejich schopností (včetně dalších funkcí, jako je například metoda Input). Další podrobnosti najdete v dokumentaci k projektu.

## <a name="how-web-forms-applications-can-present-mobile-specific-pages"></a>Jak můžou aplikace webových formulářů prezentovat stránky pro mobilní zařízení

Ve výchozím nastavení tady vidíte, jak se na běžných mobilních zařízeních zobrazují nové aplikace webových formulářů:

![](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/_static/image1.png)

Zřejmé, že rozložení vypadá velmi jako mobilní – Tato stránka byla navržena pro velké a orientované monitorování, nikoli pro obrazovku orientovaný na výšku. Co k tomu můžete?

Jak je popsáno výše v tomto dokumentu, existuje mnoho způsobů, jak přizpůsobit stránky pro mobilní zařízení. Některé techniky jsou založené na serveru, jiné spouštějí v klientovi.

### <a name="creating-a-mobile-specific-master-page"></a>Vytvoření hlavní stránky specifické pro mobilní zařízení

V závislosti na vašich požadavcích může být možné použít stejné webové formuláře pro všechny návštěvníky, ale mají dvě samostatné stránky předlohy: jeden pro návštěvníky stolních počítačů, druhý pro mobilní návštěvníky. Tím získáte flexibilitu při změně šablony stylů CSS nebo značek HTML nejvyšší úrovně na možnost mobilní zařízení, aniž byste museli duplikovat libovolnou logiku stránky.

To je snadné. Například můžete přidat obslužnou rutinu před inicializací, jako je například následující, do webového formuláře:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample1.cs)]

Nyní vytvořte hlavní stránku s názvem Mobile. Master ve složce nejvyšší úrovně aplikace a použije se při zjištění mobilního zařízení. Vaše mobilní Předloha může v případě potřeby odkazovat na šablonu stylů CSS specifickou pro mobilní zařízení. Pro návštěvníky plochy se pořád zobrazuje vaše výchozí stránka předlohy, ne mobilní zařízení.

### <a name="creating-independent-mobile-specific-web-forms"></a>Vytváření nezávislých webových formulářů specifických pro mobilní zařízení

Pro zajištění maximální flexibility můžete jít mnohem víc, než jenom samostatné stránky předloh pro různé typy zařízení. Můžete implementovat dvě *zcela oddělené sady webových formulářů* – jednu sadu pro desktopové prohlížeče, jinou sadu pro mobilní zařízení. To funguje nejlépe, pokud chcete pro mobilní návštěvníky prezentovat velmi jiné informace nebo pracovní postupy. Zbývající část této části popisuje tento přístup podrobněji.

Za předpokladu, že už máte aplikaci webových formulářů navrženou pro stolní počítače, nejjednodušší způsob, jak pokračovat, je vytvořit podsložku s názvem "mobilní" v rámci projektu a vytvořit mobilní stránky tam. Můžete sestavit celou podřízenou lokalitu s vlastními stránkami předlohy, šablonami stylů a stránkami, a to pomocí všech stejných technik, které byste použili pro jakoukoli jinou aplikaci webového formuláře. Nemusíte nutně vytvořit mobilní ekvivalent pro *každou* stránku na desktopové stránce. Můžete si vybrat, jakou podmnožinu funkcí dává mobilní Návštěvníci smysl.

Vaše mobilní stránky mohou sdílet běžné statické prostředky (například obrázky, JavaScript nebo soubory CSS) s běžnými stránkami, pokud chcete. Vzhledem k tomu, že vaše "mobilní" složka nebude označena jako samostatná aplikace, *Pokud je* hostována ve službě IIS (pouze jednoduché Podsložky webových formulářů), bude také sdílet stejnou konfiguraci, data relace a další infrastrukturu jako stránky plochy.

> [!NOTE]
> Vzhledem k tomu, že tento přístup obvykle zahrnuje některé duplicity kódu (mobilní stránky budou nejspíš sdílet některé podobnosti se stránkami na ploše), je důležité vyhodnotit všechny běžné obchodní logiky nebo datové kódy pro přístup do sdílené základní vrstvy nebo služby. Jinak budete muset při vytváření a údržbě aplikace zdvojnásobit úsilí.

#### <a name="redirecting-mobile-visitors-to-your-mobile-pages"></a>Přesměrování mobilních návštěvníků na mobilní stránky

Je často vhodné přesměrovat mobilní návštěvníky na mobilní stránky jenom na *první* žádost ve své relaci procházení (a ne na každý požadavek ve své relaci), protože:

- Mobilním návštěvníkům pak můžete snadno umožnit přístup k vašim stránkám plochy, pokud si chtějí – Stačí umístit odkaz na stránku předlohy, která se odkazuje na desktopovou verzi. Návštěvník nebude přesměrován zpět na mobilní stránku, protože již není prvním požadavkem ve své relaci.
- Zabraňuje riziku v narušování požadavků na všechny dynamické prostředky sdílené mezi desktopovou a mobilní částí vaší lokality (například pokud máte společný webový formulář, který se zobrazuje na ploše a mobilní části vaší lokality v prvku IFRAME nebo v určitých obslužných rutinách AJAX).

K tomu můžete svou logiku přesměrování umístit v **relaci\_spustit** metodu. Do souboru Global.asax.cs přidejte například následující metodu:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample2.cs)]

#### <a name="configuring-forms-authentication-to-respect-your-mobile-pages"></a>Konfigurace ověřování formulářů pro respektování mobilních stránek

Všimněte si, že ověřování prostřednictvím formulářů provádí určité předpoklady, kde může přesměrovat návštěvníky během a po procesu ověřování:

- Pokud uživatel potřebuje být ověřený, ověřování pomocí formulářů je přesměruje na stránku pro přihlášení k ploše bez ohledu na to, jestli se jedná o stolní nebo mobilní uživatele (protože má jenom koncept *jedné* přihlašovací adresy URL). Za předpokladu, že chcete nastavit styl mobilní přihlašovací stránky odlišně, je potřeba vylepšit přihlašovací stránku plochy, aby přesměrovala mobilní uživatele na samostatnou mobilní přihlašovací stránku. Do kódu přihlašovací stránky na **ploše** můžete například přidat následující kód na pozadí: 

    [!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample3.cs)]
- Až se uživatel úspěšně přihlásí, ověřování pomocí formulářů je ve výchozím nastavení přesměruje na domovskou stránku plochy (protože má jenom koncept *jedné* výchozí stránky). Musíte vylepšit mobilní přihlašovací stránku tak, aby se přesměrovala na mobilní domovskou stránku po úspěšném přihlášení. Přidejte například následující kód na **mobilní** přihlašovací stránku kód na pozadí: 

    [!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample4.cs)]
  
  Tento kód předpokládá, že vaše stránka obsahuje ovládací prvek přihlašovacího serveru s názvem LoginUser, jako v výchozí šabloně projektu.

### <a name="working-with-output-caching"></a>Práce s ukládáním výstupu do mezipaměti

Pokud používáte ukládání výstupu do mezipaměti, mějte na paměti, že ve výchozím nastavení je možné, aby uživatel klasické pracovní plochy navštívil určitou adresu URL (což způsobilo uložení výstupu do mezipaměti) a potom mobilní uživatel, který obdrží výstup na ploše uložený v mezipaměti. Toto upozornění se týká toho, zda právě měníte hlavní stránku podle typu zařízení nebo když implementujete úplně samostatné webové formuláře na typ zařízení.

Chcete-li se tomuto problému vyhnout, můžete ASP.NET změnit položku mezipaměti podle toho, zda návštěvník používá mobilní zařízení. Přidejte parametr hodnota VaryByCustom do deklarace OutputCache vaší stránky následujícím způsobem:

[!code-aspx[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample5.aspx)]

Dále definujte *isMobileDevice* jako parametr vlastní mezipaměti přidáním následujícího přepsání metody do souboru Global.asax.cs:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample6.cs)]

Tím zajistíte, aby mobilní Návštěvníci na stránce nedostali výstup, který jste předtím umístili do mezipaměti návštěvníkem plochy.

### <a name="a-working-example"></a>Pracovní příklad

Chcete-li zobrazit tyto techniky v akci, Stáhněte si [Tento dokument White Paper Samples Code](https://docs.microsoft.com/aspnet/mobile/overview). Ukázková aplikace webových formulářů automaticky přesměruje mobilní uživatele na skupinu stránek specifických pro mobilní zařízení v podsložce s názvem mobilní. Značky a styly těchto stránek jsou lépe optimalizované pro mobilní prohlížeče, jak vidíte na následujících snímcích obrazovky:

![](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/_static/image2.png)

Další tipy k optimalizaci značek a šablon stylů CSS pro mobilní prohlížeče najdete v části "styly mobilních stránek pro mobilní prohlížeče" dále v tomto dokumentu.

## <a name="how-aspnet-mvc-applications-can-present-mobile-specific-pages"></a>Jak aplikace ASP.NET MVC můžou prezentovat stránky pro mobilní zařízení

Vzhledem k tomu, že vzorek Model-View-Controller odděluje aplikační logiku (v řadičích) z prezentační logiky (v zobrazeních), můžete vybrat některý z následujících přístupů ke zpracování mobilní podpory v kódu na straně serveru:

1. ***používat stejné řadiče a zobrazení pro stolní i mobilní prohlížeče, ale v závislosti na typu zařízení vykreslí zobrazení v různých rozloženích Razor.** Tato možnost funguje nejlépe, pokud zobrazujete stejná data na všech zařízeních, ale jednoduše chcete dodat jiné šablony stylů CSS nebo změnit několik prvků HTML na nejvyšší úrovni pro mobilní zařízení.
2. ***Používejte stejné řadiče pro stolní i mobilní prohlížeče, ale vykreslete různá zobrazení v závislosti na typu zařízení***. Tato možnost funguje nejlépe, pokud zobrazujete zhruba stejná data a zadáváte stejné pracovní postupy pro koncové uživatele, ale chcete vykreslit velmi různé značky HTML tak, aby vyhovovaly používanému zařízení.
3. ***vytvářet samostatné oblasti pro stolní a mobilní prohlížeče, které implementují nezávislé řadiče a zobrazení pro každou *.** Tato možnost funguje nejlépe, pokud zobrazujete velmi různé obrazovky, které obsahují různé informace a vedoucí uživatele k různým pracovním postupům optimalizovaným pro jejich typ zařízení. Může to znamenat, že došlo k nějakému opakování kódu, ale můžete ho minimalizovat tak, že se běžně vyřadí do příslušné vrstvy nebo služby.

Pokud chcete vzít **první** možnost a měnit pouze rozložení Razor na typ zařízení, je velmi snadné. Pouze upravte soubor \_ViewStart. cshtml následujícím způsobem:

[!code-cshtml[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample7.cshtml)]

Nyní můžete vytvořit rozložení specifické pro mobilní zařízení s názvem \_LayoutMobile. cshtml s strukturou stránky a pravidly CSS optimalizovanými pro mobilní zařízení.

Pokud chcete využít **druhou** možnost, vykreslit v závislosti na typu zařízení návštěvníka úplně různá zobrazení, přečtěte si [Blogový příspěvek Scott Hanselman](http://www.hanselman.com/blog/ABetterASPNETMVCMobileDeviceCapabilitiesViewEngine.aspx).

Zbytek tohoto dokumentu se zaměřuje na **třetí** možnost – vytváří samostatné řadiče *a* zobrazení pro mobilní zařízení – takže můžete přesně řídit, jakou sadu funkcí jsou pro mobilní návštěvníky nabízené.

### <a name="setting-up-a-mobile-area-within-your-aspnet-mvc-application"></a>Nastavení mobilní oblasti v rámci aplikace ASP.NET MVC

Do existující aplikace ASP.NET MVC můžete v normálním způsobu přidat oblast s názvem "mobilní", a to normálním způsobem: klikněte pravým tlačítkem myši na název projektu v Průzkumník řešení a pak zvolte Přidat oblast. Pak můžete přidat řadiče a zobrazení jako v libovolné jiné oblasti aplikace ASP.NET MVC. Například přidejte do mobilní oblasti nový kontroler s názvem HomeController, který bude fungovat jako Domovská stránka pro mobilní návštěvníky.

### <a name="ensuring-the-url-mobile-reaches-the-mobile-homepage"></a>Zajištění, aby adresa URL/Mobilea dosáhla domovské stránky mobilní

Pokud chcete, aby se adresa URL/Mobilea k akci indexu v HomeController uvnitř mobilní oblasti, budete muset v konfiguraci směrování udělat dvě malé změny. Nejprve aktualizujte třídu MobileAreaRegistration tak, aby HomeController je výchozím řadičem v mobilní oblasti, jak je znázorněno v následujícím kódu:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample8.cs)]

To znamená, že mobilní Domovská stránka se teď bude nacházet na/Mobile místo/Mobile/Home, protože "Home" je teď implicitně výchozím názvem kontroleru pro mobilní stránky.

Dále si všimněte, že přidání druhého HomeController do aplikace (tj. mobilní zařízení, kromě stávající plochy), budete mít na hlavní domovské stránce přerušenou svou normální plochu. Dojde k selhání s chybou "bylo*nalezeno více typů, které odpovídají řadiči s názvem" Home "* ". Pokud chcete tento problém vyřešit, aktualizujte konfiguraci směrování na nejvyšší úrovni (v Global.asax.cs), abyste určili, že by měl mít vaše desktopová HomeController přednost při nejednoznačnosti:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample9.cs)]

Teď dojde k chybě a adresa URL http:\/\/*yoursite*/se dostane na domovskou stránku na ploše a http:\/\/*yoursite*/Mobile/se dostanete k mobilní domovské stránce.

### <a name="redirecting-mobile-visitors-to-your-mobile-area"></a>Přesměrování mobilních návštěvníků do mobilní oblasti

ASP.NET MVC obsahuje mnoho různých bodů rozšiřitelnosti, takže je možné vložit logiku přesměrování mnoha různými způsoby. Jednou z možností je vytvořit atribut filtru [RedirectMobileDevicesToMobileArea], který provede přesměrování v případě splnění následujících podmínek:

1. Je to první požadavek v relaci uživatele (tj. Session. IsNewSession Equals true).
2. Požadavek přichází z mobilního prohlížeče (tj. Request. browser. IsMobileDevice se rovná true).
3. Uživatel již nepožaduje prostředek v mobilní oblasti (tj. část *cesty* adresy URL nezačíná na/Mobile).

Ukázka ke stažení, která je součástí tohoto dokumentu White Paper, zahrnuje implementaci této logiky. Implementuje se jako autorizační filtr, který je odvozený od AuthorizeAttribute, což znamená, že může správně fungovat i v případě, že používáte ukládání výstupu do mezipaměti (jinak, pokud návštěvník pro stolní počítače poprvé přistupuje k určité adrese URL, výstup na ploše může být uložený v mezipaměti a pak bude obsluhován Další mobilní Návštěvníci).

Vzhledem k tomu, že se jedná o filtr, můžete zvolit, že se má použít pro konkrétní řadiče a akce, např.

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample10.cs)]

… nebo ho můžete použít pro všechny řadiče a akce jako *globální filtr* MVC 3 v souboru Global.asax.cs:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample11.cs)]

Ukázka ke stažení také ukazuje, jak lze vytvořit podtřídy tohoto atributu, který přesměruje na konkrétní umístění v mobilní oblasti. To znamená, že můžete například:

- Zaregistrujte globální filtr, jak vidíte výše, který ve výchozím nastavení odesílá mobilním návštěvníkům mobilním stránkám mobilní aplikace.
- Použijte také speciální filtr [RedirectMobileDevicesToMobileProductPage] pro akci "Zobrazit produkt", která přijímají mobilní návštěvníky k mobilní verzi jakékoli stránky produktu, kterou požadoval.
- Použít také další speciální podtřídy filtru na konkrétní akce, přesměrování mobilních návštěvníků na ekvivalentní mobilní stránku

### <a name="configuring-forms-authentication-to-respect-your-mobile-pages"></a>Konfigurace ověřování formulářů pro respektování mobilních stránek

Pokud používáte ověřování pomocí formulářů, měli byste si uvědomit, že když se uživatel musí přihlásit, automaticky přesměruje uživatele na jednu konkrétní adresu URL pro přihlášení, která je ve výchozím nastavení **/account/LogOn**. To znamená, že mobilní uživatelé mohou být přesměrováni na akci přihlášení na plochu.

Pokud se chcete tomuto problému vyhnout, přidejte do své pracovní plochy logiku pro "přihlášení", aby se mobilní uživatelé znovu přesměroval na mobilní akci "přihlášení". Pokud používáte výchozí šablonu aplikace ASP.NET MVC, aktualizujte akci přihlášení AccountController následujícím způsobem:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample12.cs)]

… a potom implementujte vhodný mobilní akci "přihlášení" na řadiči s názvem AccountController v mobilní oblasti.

### <a name="working-with-output-caching"></a>Práce s ukládáním výstupu do mezipaměti

Pokud používáte filtr [OutputCache], musíte vynutit, aby se položka mezipaměti lišila podle typu zařízení. Napište například:

[!code-javascript[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample13.js)]

Pak do souboru Global.asax.cs přidejte následující metodu:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample14.cs)]

Tím zajistíte, aby mobilní Návštěvníci na stránce nedostali výstup, který jste předtím umístili do mezipaměti návštěvníkem plochy.

### <a name="a-working-example"></a>Pracovní příklad

Chcete-li zobrazit tyto techniky v akci, Stáhněte si [Tento dokument s ukázkami, které jsou k disknize](https://docs.microsoft.com/aspnet/mobile/overview). Ukázka zahrnuje aplikaci ASP.NET MVC 3 (Release Candidate) rozšířenou na podporu mobilních zařízení pomocí výše popsaných metod.

## <a name="further-guidance-and-suggestions"></a>Další doprovodné materiály a návrhy

Následující diskuze platí pro webové formuláře i vývojáře MVC, kteří používají techniky popsané v tomto dokumentu.

### <a name="enhancing-your-redirection-logic-using-51degreesmobi-foundation"></a>Vylepšení logiky přesměrování pomocí 51Degrees.mobi Foundation

Logika přesměrování zobrazená v tomto dokumentu může být pro vaši aplikaci dokonale dostačující, ale nebude fungovat, pokud potřebujete zakázat relace nebo mobilní prohlížeče, které soubory cookie odmítnou (nemůžou mít relace), protože nedokáže zjistit, jestli je daný požadavek první z nich od tohoto návštěvníka.

Už jste zjistili, jak může Open Source 51Degrees.mobi Foundation zlepšit přesnost ASP. Detekce prohlížeče sítě. Má také integrovanou možnost přesměrovat mobilní návštěvníky na konkrétní umístění konfigurovaná v souboru Web. config. Je možné pracovat bez závislosti na ASP.NETch relacích (a tedy souborů cookie) tím, že ukládá dočasný protokol hashů hlaviček protokolu HTTP návštěvníků a IP adres, takže ví, zda je nebo není každý požadavek prvním z daného Vistor.

Následující prvek přidaný do oddílu fiftyOne v souboru Web. config přesměruje první požadavek ze zjištěného mobilního zařízení na stránku ~/Mobile/Default.aspx. Všechny požadavky na stránky v mobilní *složce nebudou* přesměrovány bez ohledu na typ zařízení. Pokud je mobilní zařízení neaktivní po dobu 20 minut nebo více zařízení, bude zapomenuté a následné požadavky budou pro účely přesměrování považovány za nové.

[!code-xml[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample15.xml)]

Další podrobnosti najdete v [dokumentaci k 51Degrees.mobi Foundation](https://github.com/51Degrees/dotNET-Device-Detection).

> [!NOTE]
> Funkci přesměrování 51Degrees.mobi Foundation *můžete* použít pro aplikace ASP.NET MVC, ale budete muset definovat konfiguraci přesměrování z adres URL s běžnými adresami URL, nikoli z podmínek směrování nebo vložením filtrů MVC na akce. Důvodem je to, že (v době psaní) 51Degrees.mobi Foundation nerozpoznává filtry nebo směrování.

### <a name="disabling-transcoders-and-proxy-servers"></a>Zakázání TriCaster a proxy serverů

Operátoři mobilní sítě mají v přístupu k mobilnímu Internetu dva široké cíle:

1. Poskytněte co nejvíce relevantní obsah
2. Maximalizujte počet zákazníků, kteří můžou sdílet omezené síťové šířky sítě.

Vzhledem k tomu, že většina webových stránek byla navržena pro velké obrazovky velikosti stolních počítačů a rychlé širokopásmové připojení s pevnou čárou, mnoho operátorů používá *TriCaster* nebo *proxy servery* , které dynamicky mění webový obsah. Mohou upravit kód HTML nebo šablonu stylů CSS tak, aby odpovídaly menším obrazovkám (zejména u "telefonů s funkcemi", které neobsahovaly výpočetní výkon pro zpracování složitých rozložení), a mohou znovu komprimovat vaše image (významně snížit jejich kvalitu), aby se zvýšila rychlost doručování stránek.

Ale pokud jste se naučili vytvořit mobilní optimalizovanou verzi vašeho webu, nebudete pravděpodobně chtít, aby operátor sítě s ním jakkoli narušil. Následující řádek můžete přidat na stránku\_načíst událost do libovolného webového formuláře ASP.NET:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample16.cs)]

Nebo pro řadič MVC ASP.NET můžete přidat následující přepsání metody tak, aby platilo pro všechny akce na tomto kontroleru:

[!code-csharp[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample17.cs)]

Výsledná zpráva HTTP informuje TriCaster a proxy s podporou standardu W3C, aby neměnily obsah. Samozřejmě není nijak zaručeno, že budou operátoři mobilní sítě respektovat tuto zprávu.

### <a name="styling-mobile-pages-for-mobile-browsers"></a>Stylování mobilních stránek pro mobilní prohlížeče

Je nad rámec tohoto dokumentu, který popisuje skvělé informace o tom, jaké druhy kódu HTML fungují správně nebo které techniky návrhu webu maximalizují použitelnost na konkrétních zařízeních. K nalezení dostatečně jednoduchého rozložení optimalizovaného pro obrazovku na mobilní úrovni nepoužívejte nespolehlivé triky umístění HTML nebo CSS. Jedinou důležitou technikou je, že je však *zobrazení značky meta*.

Některé moderní mobilní prohlížeče, ve snaze zobrazit webové stránky, které jsou určené pro stolní monitory, vykreslí stránku na virtuálním plátně, která se také označuje jako "zobrazení" (například virtuální zobrazení je 980 pixelů na iPhonu a 850 pixelů v systému Opera Mobile ve výchozím nastavení) a potom umožňuje škálovat výsledek dolů tak, aby se vešel na fyzické pixely obrazovky. Uživatel si pak může toto zobrazení zvětšit a posunout. Tato výhoda má tu výhodu, že umožňuje prohlížeči zobrazit stránku v jejím zamýšleném rozložení, ale má také nevýhodu, že vynucuje přiblížení a posouvání, což pro uživatele nevyhovuje. Pokud navrhujete mobilní zařízení, je lepší navrhovat pro užší obrazovku, takže není potřeba žádné přiblížení ani horizontální posouvání.

Způsob, jak sdělit mobilnímu prohlížeči, jak velký má být zobrazení prostřednictvím nestandardního *zobrazení* značky meta. Pokud například do sekce HEAD stránky přidáte následující:,

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample18.html)]

… pak se podpora prohlížečů smartphone rozloží na stránku na virtuálním plátně na šířku 480 pixelů. To znamená, že pokud vaše prvky HTML definují své šířky v procentech, budou se tyto procentní hodnoty interpretovat s ohledem na tuto šířku 480 pixelů, nikoli na výchozí šířku zobrazení. V důsledku toho je pravděpodobnost, že se uživatel bude muset přiblížit do horizontálního měřítka a výrazně zlepšit možnosti procházení mobilních zařízení.

Pokud chcete, aby se šířka zobrazení shodovala s fyzickými obrazovými body zařízení, můžete zadat následující:

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample19.html)]

Aby to fungovalo správně, je nutné explicitně vynutit, aby prvky převyšuje tuto šířku (např. pomocí atributu *Width* nebo vlastnosti CSS), jinak bude mít prohlížeč nuceně používat větší zobrazení bez ohledu na to, co je potřeba. Viz také: [Další podrobnosti o nestandardním tagu zobrazení](https://developer.apple.com/library/safari/#documentation/AppleApplications/Reference/SafariHTMLRef/Articles/MetaTags.html).

Většina moderních telefonů Smartphone podporuje *duální orientaci*: můžou se uchovávat v režimu na výšku nebo na šířku. Proto je důležité nevytvářet předpoklady o šířce obrazovky v pixelech. Ani Nepředpokládáme, že je šířka obrazovky pevná, protože uživatel může změnit orientaci zařízení, když jsou na vaší stránce.

Starší zařízení se systémem Windows Mobile a BlackBerry mohou také v záhlaví stránky přijmout následující značky meta, aby byly informace o tom, že jsou optimalizovány pro mobilní zařízení, a proto by neměly být transformovány.

[!code-html[Main](add-mobile-pages-to-your-aspnet-web-forms-mvc-application/samples/sample20.html)]

## <a name="additional-resources"></a>Další prostředky

Seznam emulátorů a simulátorů mobilních zařízení, které můžete použít k otestování webové aplikace Mobile ASP.NET, najdete na stránce [simulace oblíbených mobilních zařízení pro účely testování](../mobile/device-simulators.md).

## <a name="credits"></a>Kredity

- Primární autor: Steven Sanderson
- Revidující/další zapisovače obsahu: James Rosewell, Mikael Söderström, Scott Hanselman, Scott Hunterem

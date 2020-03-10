---
uid: web-forms/overview/older-versions-security/introduction/forms-authentication-configuration-and-advanced-topics-vb
title: Konfigurace ověřování formulářů a Pokročilá témata (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu prověříme různá nastavení ověřování pomocí formulářů a zjistíte, jak je upravovat pomocí elementu Forms. To má za následek detailní...
ms.author: riande
ms.date: 01/14/2008
ms.assetid: 829d2f56-5c48-445b-b826-3418a450c788
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/forms-authentication-configuration-and-advanced-topics-vb
msc.type: authoredcontent
ms.openlocfilehash: 4d77816a489a4fa16cd70ec4214cd2f8ee563029
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637989"
---
# <a name="forms-authentication-configuration-and-advanced-topics-vb"></a>Konfigurace ověřování pomocí formuláře a pokročilá témata (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/ASPNET_Security_Tutorial_03_VB.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial03_AuthAdvanced_vb.pdf)

> V tomto kurzu prověříme různá nastavení ověřování pomocí formulářů a zjistíte, jak je upravovat pomocí elementu Forms. To bude mít podrobnější přehled o přizpůsobení hodnoty časového limitu ověřovacího lístku formulářů pomocí přihlašovací stránky s vlastní adresou URL (třeba Login. aspx místo Login. aspx) a ověřovacími lístky pro formuláře bez souborů cookie.

## <a name="introduction"></a>Úvod

V [předchozím kurzu](an-overview-of-forms-authentication-vb.md) jsme se prohlédli v krocích nezbytných pro implementaci ověřování pomocí formulářů v aplikaci ASP.NET, od zadání nastavení konfigurace v souboru Web. config pro vytvoření přihlašovací stránky pro zobrazení jiného obsahu pro ověřené a anonymní uživatele. Odvoláme, že jsme nakonfigurovali web na používání ověřování pomocí formulářů, nastavením atributu Mode&gt; elementu &lt;Authentication na formuláře. Element &lt;Authentication&gt; může volitelně zahrnovat &lt;Forms&gt; podřízený element, pomocí kterého je možné určit sortiment nastavení ověřování pomocí formulářů.

V tomto kurzu prověříme různá nastavení ověřování pomocí formulářů a zjistíte, jak je upravovat pomocí&gt; elementu &lt;Forms. To bude mít podrobnější přehled o přizpůsobení hodnoty časového limitu ověřovacího lístku formulářů pomocí přihlašovací stránky s vlastní adresou URL (třeba Login. aspx místo Login. aspx) a ověřovacími lístky pro formuláře bez souborů cookie. Podíváme se také na strukturu lístku pro ověřování pomocí formulářů a Prohlédněte si preventivní opatření ASP.NET, která zajistí, aby data lístku byla zabezpečená před kontrolou a manipulací. Nakonec se podíváme na to, jak ukládat dodatečná uživatelská data v ověřovacím lístku pro formuláře a jak tato data vytvořit prostřednictvím vlastního objektu zabezpečení.

## <a name="step-1-examining-the-ltformsgt-configuration-settings"></a>Krok 1: Kontrola nastavení konfigurace&gt; &lt;Forms

Systém ověřování pomocí formulářů v ASP.NET nabízí řadu nastavení konfigurace, která je možné přizpůsobit na základě aplikace. To zahrnuje nastavení jako: životnost lístku pro ověřování formulářů; Jaký je způsob, jakým se tato ochrana používá pro lístek; za jakých podmínek se používají ověřovací lístky bez souborů cookie; Cesta k přihlašovací stránce a další informace. Chcete-li upravit výchozí hodnoty, přidejte [&lt;forms&gt; element](https://msdn.microsoft.com/library/1d3t3c61.aspx) jako podřízený [prvek&lt;ověřování&gt;](https://msdn.microsoft.com/library/532aee0e.aspx)a určete tak hodnoty vlastností, které chcete přizpůsobit jako atributy XML, například takto:

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample1.xml)]

Tabulka 1 shrnuje vlastnosti, které lze přizpůsobit pomocí&gt; elementu &lt;Forms. Vzhledem k tomu, že web. config je soubor XML, názvy atributů v levém sloupci rozlišují velká a malá písmena.

| <strong>Atribut</strong> |                                                                                                                                                                                                                                     <strong>Popis</strong>                                                                                                                                                                                                                                      |
|----------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         formulář         |                                                                                                                Tento atribut určuje, za jakých podmínek je ověřovací lístek uložený v souboru cookie, který je vložený v adrese URL. Povolené hodnoty jsou: UseCookies; UseUri; Automatické rozpoznávání a UseDeviceProfile (výchozí). Krok 2 toto nastavení prověřuje podrobněji.                                                                                                                |
|         defaultUrl         |                                                                                                                                                         Určuje adresu URL, na kterou se uživatelé přesměrují po přihlášení ze stránky pro přihlášení, pokud v řetězci dotazu není zadaná žádná hodnota RedirectUrl. Výchozí hodnota je Default. aspx.                                                                                                                                                         |
|           domain           | Při použití ověřovacích lístků založených na souborech cookie toto nastavení určuje hodnotu domény cookie s. Výchozí hodnota je prázdný řetězec, který způsobí, že prohlížeč použije doménu, ze které byla vydána (například www.yourdomain.com). V takovém <strong>případě se soubory</strong> cookie neodesílají při vytváření požadavků na subdomény, jako je admin.yourdomain.com. Pokud chcete, aby byl soubor cookie předán všem poddoménám, je třeba přizpůsobit atribut domény jeho nastavení na yourdomain.com. |
|  enableCrossAppRedirects   |                                                                                                                                                                   Logická hodnota označující, zda jsou ověření uživatelé zapamatování při přesměrování na adresy URL v jiných webových aplikacích na stejném serveru. Výchozí hodnotou je hodnota false.                                                                                                                                                                   |
|          loginUrl          |                                                                                                                                                                                                                      Adresa URL přihlašovací stránky Výchozí hodnota je Login. aspx.                                                                                                                                                                                                                      |
|            jméno            |                                                                                                                                                                                                   Pokud používáte ověřovací lístky založené na souborech cookie, název souboru cookie. Výchozí hodnota je. ASPXAUTH.                                                                                                                                                                                                   |
|            path            |                                                                             Při použití ověřovacích lístků založených na souborech cookie toto nastavení určuje atribut cesty cookie s. Atribut path umožňuje vývojářům omezit rozsah souboru cookie na konkrétní hierarchii adresářů. Výchozí hodnota je/, která informuje prohlížeč o odeslání souboru cookie ověřovacího lístku do jakékoli žádosti provedené v doméně.                                                                              |
|         ochrana         |                                                                                                                                            Určuje, jaké techniky se používají k ochraně lístku pro ověřování pomocí formulářů. Povolené hodnoty jsou: All (výchozí); Šifr NTato a ověření. Tato nastavení jsou podrobněji popsaná v kroku 3.                                                                                                                                            |
|         Vlastnost requireSSL         |                                                                                                                                                                                Logická hodnota určující, zda je pro přenos ověřovacího souboru cookie vyžadováno připojení SSL. Výchozí hodnota je false.                                                                                                                                                                                |
|     Parametr slidingExpiration      |                                                                                                 Logická hodnota, která označuje, zda se má resetovat časový limit ověřovacího souboru cookie s pokaždé, když uživatel navštíví web během jedné relace. Výchozí hodnotou je hodnota true. Zásady časového limitu ověřovacího lístku jsou podrobněji popsány v části určení hodnoty časového limitu lístku s.                                                                                                 |
|          timeout           |                                                                                                                               Určuje dobu v minutách, po jejímž uplynutí vyprší platnost souboru cookie ověřovacího lístku. Výchozí hodnota je 30. Zásady časového limitu ověřovacího lístku jsou podrobněji popsány v části určení hodnoty časového limitu lístku s.                                                                                                                               |

**Tabulka 1**: shrnutí atributů &lt;ových formulářů&gt; prvků

V ASP.NET 2,0 a novějších jsou výchozí hodnoty ověřování založené na formulářích pevně zakódované ve třídě FormsAuthenticationConfiguration v .NET Framework. V souboru Web. config musí být všechny úpravy aplikovány na jednotlivé aplikace. To se liší od ASP.NET 1. x, kde byly uloženy výchozí hodnoty ověřování pomocí formulářů v souboru Machine. config (a je proto možné je upravit prostřednictvím editace Machine. config). V tématu ASP.NET 1. x je vhodné uvést, že počet nastavení systému ověřování pomocí formulářů má jiné výchozí hodnoty v ASP.NET 2,0 a vyšší než v ASP.NET 1. x. Pokud migrujete aplikaci z prostředí ASP.NET 1. x, je důležité znát tyto rozdíly. Seznam rozdílů najdete [v technické dokumentaci k elementu &lt;forms&gt;](https://msdn.microsoft.com/library/1d3t3c61.aspx) .

> [!NOTE]
> Několik nastavení ověřování, jako je například časový limit, doména a cesta, určují podrobnosti pro výsledný soubor cookie lístku ověřování formulářů. Pokud chcete získat další informace o souborech cookie, jak fungují a jejich různé vlastnosti, přečtěte si [Tento kurz](http://www.quirksmode.org/js/cookies.html).

### <a name="specifying-the-tickets-timeout-value"></a>Zadání hodnoty časového limitu lístku

Lístek ověřování pomocí formulářů je token, který představuje identitu. U lístků ověřování na základě souborů cookie je tento token uložený ve formě souboru cookie a odeslán na webový server na každém požadavku. Držitel tokenu, v podstatě, deklaruje, jsem *uživatelským jménem*, jsem už přihlášený a používá se k tomu, aby bylo možné pamatovat identitu uživatele v rámci návštěv stránky.

Lístek ověřování pomocí formulářů obsahuje jenom identitu uživatele, ale obsahuje taky informace, které vám pomůžou zajistit integritu a zabezpečení tokenu. I když nechcete, aby nekalé uživatel schopný vytvořit padělaný token, nebo nějakým způsobem upravit nevhodný token.

Jednou z těchto informací, které jsou součástí lístku, je *vypršení platnosti*, což je datum a čas, kdy lístek již není platný. Pokaždé, když FormsAuthenticationModule zkontroluje ověřovací lístek, zajistí, že platnost lístku ještě neuplynula. Pokud k tomu dojde, ignoruje lístek a identifikuje uživatele jako anonymního. Toto zabezpečení pomáhá chránit před útoky přes opakované přehrání. Bez vypršení platnosti, pokud se hacker mohl dostat do platného ověřovacího lístku uživatele, třeba získáním fyzického přístupu ke svému počítači a jeho kořenem prostřednictvím svých souborů cookie – může poslat požadavek na server pomocí tohoto autentizačního lístku pro ověření a získat položku. I když vypršení platnosti nebrání tomuto scénáři, omezí okno, během kterého může být takový útok úspěšný.

> [!NOTE]
> Krok 3 podrobně popisuje další techniky používané systémem pro ověřování pomocí formulářů k ochraně ověřovacího lístku.

Když vytváříte ověřovací lístek, systém ověřování pomocí formulářů po konzultaci s nastavením časového limitu určí jeho platnost. Jak je uvedeno v tabulce 1, nastavení časového limitu je standardně nastavené na 30 minut, což znamená, že když se vytvoří lístek pro ověřování pomocí formulářů, nastaví se datum a čas 30 minut v budoucnosti.

Vypršení platnosti definuje absolutní čas v budoucnosti, kdy vyprší platnost lístku pro ověřování na formuláři. Vývojáři ale obvykle chtějí implementovat klouzavé vypršení platnosti, což se resetuje pokaždé, když uživatel přenavštíví Web. Toto chování je určeno nastavením parametr slidingExpiration. Pokud je nastavená hodnota true (výchozí), pokaždé, když FormsAuthenticationModule ověřuje uživatele, aktualizuje vypršení platnosti lístku. Pokud je hodnota nastavena na false, platnost konce platnosti nebude u každého požadavku aktualizována, což způsobí, že lístku vyprší přesně časový limit v minutách po prvním vytvoření lístku.

> [!NOTE]
> Vypršení platnosti uložené v ověřovacím lístku je absolutní hodnota data a času, například 2. srpna 2008 11:34 AM. Datum a čas jsou navíc relativní vzhledem k místnímu času webového serveru. Toto rozhodnutí o návrhu může mít zajímavé vedlejší účinky v oblasti letního času (DST), což znamená, že se hodiny v USA přesunuly před jednu hodinu (za předpokladu, že je webový server hostovaný v národním prostředí, kde se pozoruje letní čas). Zvažte, co se stane pro web ASP.NET s vypršenou platností 30 minut v době, kdy začíná letní čas (což je 2:00 dop.). Představte si, že se návštěvník přihlásí k webu dne 11. března 2008 v 1:55. Tím se vygeneruje lístek ověřování pomocí formulářů, jehož platnost vyprší 11. března 2008 v 2:25 (30 minut v budoucnosti). Po 2:00 se však hodiny přeskočí na 3:00 z důvodu letního času. Když uživatel načte novou stránku šest minut po přihlášení (v 3:01.), FormsAuthenticationModule Poznámkový odkaz, že lístek vypršel, a přesměruje uživatele na přihlašovací stránku. Podrobnější diskuzi o tomto a jiném časovém limitu ověřovacího lístku oddities, jakož i alternativním řešením, najdete v části řešení Stefan Schackow *Professional ASP.NET 2,0 zabezpečení, členství a správy rolí* (ISBN: 978-0-7645-9698-8).

Obrázek 1 znázorňuje pracovní postup, pokud je parametr slidingExpiration nastaven na hodnotu false a časový limit je nastavený na 30. Všimněte si, že ověřovací lístek generovaný při přihlášení obsahuje datum vypršení platnosti a tato hodnota není aktualizována při dalších požadavcích. Pokud FormsAuthenticationModule zjistí, že platnost lístku vypršela, zahodí ho a považuje požadavek za anonymní.

[![grafické znázornění vypršení platnosti lístku pro ověřování pomocí formulářů, pokud je parametr slidingExpiration false](forms-authentication-configuration-and-advanced-topics-vb/_static/image2.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image1.png)

**Obrázek 01**: grafická reprezentace lístku ověřování pomocí formulářů, pokud je parametr slidingExpiration false ([kliknutím zobrazíte obrázek v plné velikosti](forms-authentication-configuration-and-advanced-topics-vb/_static/image3.png)).

Obrázek 2 ukazuje pracovní postup, pokud je parametr slidingExpiration nastaven na hodnotu true a časový limit je nastavený na 30. Po přijetí ověřené žádosti (s lístkem bez vypršení platnosti) se její vypršení platnosti aktualizuje na časový limit v řádu minut v budoucnosti.

[![grafické znázornění lístku pro ověřování pomocí formulářů, pokud je hodnota parametr slidingExpiration pravdivá.](forms-authentication-configuration-and-advanced-topics-vb/_static/image5.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image4.png)

**Obrázek 02**: grafická reprezentace lístku pro ověřování pomocí formulářů, když má parametr slidingExpiration hodnotu true ([kliknutím zobrazíte obrázek v plné velikosti](forms-authentication-configuration-and-advanced-topics-vb/_static/image6.png)).

Když použijete lístky ověřování na základě souborů cookie (výchozí nastavení), bude tato diskuze trochu větší, protože soubory cookie můžou mít také zadané své vlastní vypršení platnosti. Vypršení platnosti souboru cookie (nebo jeho nedostatku) instruuje prohlížeč, kdy by měl být soubor cookie zničen. Pokud soubor cookie nemá vypršení platnosti, je zničen při vypnutí prohlížeče. Pokud dojde k vypršení platnosti, soubor cookie zůstane uložený v počítači uživatele až do doby, kdy uplyne datum a čas zadaný v vypršení platnosti. Když prohlížeč zničí soubor cookie, už se neposílá webovému serveru. Proto je zničení souboru cookie obdobně přihlášeno uživateli z lokality.

> [!NOTE]
> Uživatel samozřejmě může proaktivně odebrat všechny soubory cookie uložené v jejich počítači. V aplikaci Internet Explorer 7 přejděte na nástroje, možnosti a klikněte na tlačítko Odstranit v části Historie procházení. Odtud klikněte na tlačítko Odstranit soubory cookie.

Systém ověřování pomocí formulářů vytvoří soubory cookie založené na relacích nebo vypršení platnosti v závislosti na hodnotě předané do parametru *persistCookie* . Odvolat, že metody GetAuthCookie, SetAuthCookie a RedirectFromLoginPage třídy FormsAuthentication přebírají dva vstupní parametry: *username* a *persistCookie*. Přihlašovací stránka, kterou jsme vytvořili v předchozím kurzu, obsahuje zaškrtávací políčko pro zapamatování, které určuje, jestli se vytvořil trvalý soubor cookie. Trvalé soubory cookie jsou založeny na vypršení platnosti; soubory cookie, které nejsou trvalé, jsou založené na relacích.

Koncepty s časovým limitem a parametr slidingExpiration jsou již popsány u souborů cookie relace i vypršení platnosti. Ve vykonání je pouze jeden malý rozdíl: při použití souborů cookie založených na vypršení platnosti s slidingTimeout nastavenou na hodnotu true je platnost souboru cookie aktualizována pouze v případě, že uplynula více než polovina zadaného času.

Pojďme aktualizovat zásady časového limitu ověřovacích lístků pro náš web tak, aby lístky s časovým limitem po jedné hodině (60 minut) používaly klouzavé vypršení. Chcete-li tuto změnu změnit, aktualizujte soubor Web. config a přidejte &lt;Forms&gt; elementu do &lt;ověřování&gt; elementu pomocí následujícího kódu:

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample2.xml)]

### <a name="using-an-login-page-url-other-than-loginaspx"></a>Použití jiné adresy URL přihlašovací stránky než Login. aspx

Vzhledem k tomu, že FormsAuthenticationModule automaticky přesměruje neautorizované uživatele na přihlašovací stránku, musí znát adresu URL přihlašovací stránky. Tato adresa URL je určena atributem loginUrl ve&gt; elementu &lt;Forms a má výchozí hodnotu Login. aspx. Pokud předáváte přes existující web, možná už máte přihlašovací stránku s jinou adresou URL, která už je záložkou a indexována vyhledávacími moduly. Místo přejmenování stávající přihlašovací stránky na přihlašovací. aspx a průlomové odkazy a záložky uživatelů můžete místo toho upravit atribut loginUrl tak, aby odkazoval na přihlašovací stránku.

Například pokud se vaše přihlašovací stránka jmenovala Login. aspx a byla umístěna v adresáři uživatelé, můžete nastavení konfigurace loginUrl nasměrovat na ~/Users/SignIn.aspx, například:

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample3.xml)]

Vzhledem k tomu, že naše aktuální aplikace již má přihlašovací stránku s názvem Login. aspx, není nutné zadávat vlastní hodnotu v prvku &lt;Forms&gt; elementu.

## <a name="step-2-using-cookieless-forms-authentication-tickets"></a>Krok 2: použití lístků pro ověřování pomocí formulářů bez souborů cookie

Ve výchozím nastavení systém ověřování pomocí formulářů určuje, zda se mají ukládat ověřovací lístky do kolekce souborů cookie, nebo je vložit do adresy URL na základě uživatelského agenta, který navštívil web. Všechny běžné desktopové prohlížeče, jako jsou Internet Explorer, Firefox, Opera a Safari, podporují soubory cookie, ale ne všechna mobilní zařízení.

Zásady souborů cookie používané systémem pro ověřování pomocí formulářů závisí na nastavení souborů cookie v&gt; elementu &lt;Forms, ke kterému se dá přiřadit jedna ze čtyř hodnot:

- UseCookies – určuje, zda budou vždy použity ověřovací lístky založené na souborech cookie.
- UseUri – označuje, že se nikdy nepoužijí ověřovací lístky založené na souborech cookie.
- Automaticky rozpoznat – Pokud profil zařízení nepodporuje soubory cookie, nepoužijí se ověřovací lístky založené na souborech cookie. Pokud profil zařízení podporuje soubory cookie, používá se k určení, jestli jsou soubory cookie povolené, mechanizmus zjišťování.
- UseDeviceProfile – výchozí; používá lístky ověřování založené na souborech cookie pouze v případě, že profil zařízení podporuje soubory cookie. Nepoužívá se žádný mechanismus zjišťování.

Nastavení automatického rozpoznávání a UseDeviceProfile se spoléhá na *profil zařízení* při zjištění, jestli se má použít ověřovací lístky založené na souborech cookie nebo bez souborů cookie. ASP.NET udržuje databázi různých zařízení a jejich schopností, jako je třeba to, jestli podporují soubory cookie, jakou verzi JavaScriptu podporují a tak dále. Pokaždé, když zařízení požádá o webovou stránku z webového serveru, pošle se spolu s hlavičkou http *uživatelského agenta* , které identifikuje typ zařízení. ASP.NET automaticky odpovídá zadanému řetězci User-Agent s odpovídajícím profilem zadaným ve své databázi.

> [!NOTE]
> Tato databáze možností zařízení je uložena v řadě souborů XML, které vyhovují [schématu definičního souboru prohlížeče](https://msdn.microsoft.com/library/ms228122.aspx). Výchozí soubory profilu zařízení se nacházejí v%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG\Browsers. Do složky aplikace\_prohlížeče aplikace můžete také přidat vlastní soubory. Další informace naleznete v tématu [How to: Detekce typů prohlížeče na webových stránkách ASP.NET](https://msdn.microsoft.com/library/3yekbd5b.aspx).

Vzhledem k tomu, že výchozí nastavení je UseDeviceProfile, použijí se lístky pro ověřování pomocí formulářů bez souborů cookie, když se web navštíví zařízením, u kterého profil hlásí, že nepodporuje soubory cookie.

### <a name="encoding-the-authentication-ticket-in-the-url"></a>Kódování ověřovacího lístku v adrese URL

Soubory cookie jsou přirozené médium pro zahrnutí informací z prohlížeče do jednotlivých požadavků na konkrétní web, což má za následek to, proč výchozí nastavení ověřování pomocí formulářů používá soubory cookie, pokud je hostující zařízení podporuje. Pokud se soubory cookie nepodporují, musí se použít alternativní způsob předání ověřovacího lístku z klienta na server. Běžným řešením použitým v prostředí bez souborů cookie je zakódovat data souborů cookie v adrese URL.

Nejlepším způsobem, jak zjistit, jak můžou být tyto informace vložené v rámci adresy URL, je vynutit, aby lokalita používala ověřovací lístky bez souborů cookie. To je možné dosáhnout nastavením konfigurace nastavení souborů cookie na UseUri:

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample4.xml)]

Až tuto změnu provedete, navštivte web prostřednictvím prohlížeče. Při návštěvě anonymního uživatele budou adresy URL vypadat stejně jako dříve. Když například navštívíte stránku Default. aspx, na panelu Adresa v prohlížeči se zobrazí následující adresa URL:

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/default.aspx`

Po přihlášení se ale ověřovací lístek formulářů vloží do adresy URL. Když například navštívíte přihlašovací stránku a přihlásíte se jako Sam, vrátí se na stránku Default. aspx, ale adresa URL tohoto času:

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/(F(jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2))/default.aspx`

Lístek ověřování formulářů byl vložen v rámci adresy URL. Řetězec (F (jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2) představuje informace ověřovacího lístku s šestnáctkovým zakódovaným řetězcem, který je obvykle uložen v souboru cookie.

Aby lístky pro ověřování bez souborů cookie fungovaly, musí systém zakódovat všechny adresy URL na stránce, aby zahrnovali data ověřovacího lístku. v opačném případě se ověřovací lístek ztratí, když uživatel klikne na odkaz. Naštěstí, tato logika vkládání se provádí automaticky. Chcete-li tuto funkci předvést, otevřete stránku Default. aspx a přidejte ovládací prvek hypertextový odkaz, nastavte jeho text a vlastnosti NavigateUrl na test Link a SomePage. aspx v uvedeném pořadí. Nezáleží na tom, že v našem projektu není stránka s názvem SomePage. aspx.

Uložte změny do souboru Default. aspx a pak na něj přejděte v prohlížeči. Přihlaste se k webu, aby byl lístek ověřování formulářů vložen do adresy URL. Pak z default. aspx klikněte na odkaz test odkazu. Co se stalo? Pokud žádná stránka s názvem SomePage. aspx neexistuje, došlo k chybě 404, ale to není důležité. Místo toho se zaměřte na adresní řádek v prohlížeči. Všimněte si, že obsahuje lístek ověřování formulářů v adrese URL.

`http://localhost:2448/ASPNET\_Security\_Tutorial\_03\_CS/(F(jaIOIDTJxIr12xYS-VVgkqKCVAuIoW30Bu0diWi6flQC-FyMaLXJfow\_Vd9GZkB2Cv-rfezq0gKadKX0YPZCkA2))/SomePage.aspx`

Adresa URL SomePage. aspx v odkazu se automaticky převedla na adresu URL, která obsahuje ověřovací lístek – nemuseli jsme psát Lick kódu. Ověřovací lístek formuláře bude automaticky vložen do adresy URL pro všechny hypertextové odkazy, které nezačínají na http://nebo/. Nezáleží na tom, zda se hypertextový odkaz objeví ve volání metody Response. Redirect, v ovládacím prvku hypertextový odkaz nebo v ukotveném prvku HTML (tj. &lt;a href = "..."&gt;...&lt;/a&gt;). Dokud se adresa URL nelíbí http://www.someserver.com/SomePage.aspx nebo/SomePage.aspx, bude pro nás vložen lístek pro ověřování na formuláři.

> [!NOTE]
> Lístky ověřování pomocí formulářů bez souborů cookie dodržují stejné zásady časového limitu jako lístky ověřování založené na souborech cookie. Ověřovací lístky bez souborů cookie jsou ale náchylnější k útokům, protože ověřovací lístek je vložený přímo v adrese URL. Představte si uživatele, který navštíví web, přihlásí se a pak vloží adresu URL do e-mailu kolegovi. Pokud kolega na tento odkaz klikne ještě před dosažením vypršení platnosti, přihlásí se jako uživatel, který e-mail odeslal.

## <a name="step-3-securing-the-authentication-ticket"></a>Krok 3: zabezpečení ověřovacího lístku

Lístek ověřování pomocí formulářů se přenáší prostřednictvím kabelu buď v souboru cookie, nebo přímo vložený v rámci adresy URL. Kromě informací o identitě může lístek ověřování také zahrnovat uživatelská data (jak uvidíme v kroku 4). V důsledku toho je důležité, aby data lístku byla šifrována z Prying oči a (ještě důležitější), aby systém ověřování pomocí formulářů mohl zaručit, že lístek nebyl zfalšován.

Aby bylo zajištěno soukromí dat lístku, může systém ověřování formulářů šifrovat data lístku. Nepodaří-li se zašifrovat data lístků, odesílají potenciálně citlivé informace prostřednictvím tohoto drátu v prostém textu.

Aby bylo zaručeno pravost lístku, systém ověřování pomocí formulářů musí lístek *ověřit* . Ověření je zákonem, který zajišťuje, že konkrétní část dat nebyla upravena a že je zajištěna prostřednictvím *[ověřovacího kódu zprávy (Mac)](http://en.wikipedia.org/wiki/Message_authentication_code)* . V kostce je počítač MAC malými informacemi, které určují data, která je třeba ověřit (v tomto případě lístku). Pokud jsou data reprezentovaná počítačem MAC upravená, pak MAC a data se neshodují. Kromě toho je výpočetní výkon pro hackery vyměněn jak k úpravě dat, tak k vytvoření vlastního počítače MAC, aby odpovídal změněným datům.

Při vytváření (nebo úpravách) lístku vytvoří systém ověřování pomocí formulářů počítač MAC a připojí ho k datům lístku. Po doručení následné žádosti systém ověřováním formulářů porovná údaje v počítačích MAC a lístků a ověří pravost dat lístku. Obrázek 3 znázorňuje tento pracovní postup graficky.

[![se pravost lístku zajišťuje prostřednictvím MAC](forms-authentication-configuration-and-advanced-topics-vb/_static/image8.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image7.png)

**Obrázek 03**: pravost lístku se zajišťuje prostřednictvím Mac ([kliknutím zobrazíte obrázek v plné velikosti).](forms-authentication-configuration-and-advanced-topics-vb/_static/image9.png)

Jaké míry zabezpečení jsou aplikovány na ověřovací lístek, závisí na nastavení ochrany v prvku &lt;Forms&gt; elementu. Nastavení ochrany může být přiřazeno jedné z následujících tří hodnot:

- Vše – lístek je šifrovaný i digitálně podepsaný (výchozí).
- Používá se šifrování jen pro šifrování – negeneruje se žádná adresa MAC.
- Žádné – lístek není šifrovaný ani digitálně podepsaný.
- Ověření – je vygenerována adresa MAC, ale data lístku jsou odesílána přes drát v prostém textu.

Microsoft důrazně doporučuje použít nastavení vše.

### <a name="setting-the-validation-and-decryption-keys"></a>Nastavení ověřovacích a dešifrovacích klíčů

Algoritmy šifrování a hash používané systémem pro ověřování pomocí formulářů k šifrování a ověření ověřovacího lístku jsou přizpůsobitelné pomocí [elementu&lt;machineKey&gt;](https://msdn.microsoft.com/library/w8h3skw9.aspx) v souboru Web. config. Tabulka 2 obsahuje popis atributů prvku &lt;machineKey&gt; a jejich možné hodnoty.

| **Atribut** | **Popis** |
| --- | --- |
| dešifrování | Určuje algoritmus používaný k šifrování. Tento atribut může mít jednu z následujících čtyř hodnot:-auto-výchozí; Určuje algoritmus na základě délky atributu decryptionKey. -AES – používá algoritmus [Standard AES (Advanced Encryption Standard) (AES)](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) . -DES – používá algoritmus [des (Data Encryption Standard)](http://en.wikipedia.org/wiki/Data_Encryption_Standard) , je tento algoritmus považován za výpočetně slabý a neměl by se používat. -3DES – používá algoritmus [Triple DES](http://en.wikipedia.org/wiki/Triple_DES) , který pracuje třikrát po trojnásobné použití algoritmu DES. |
| decryptionKey | Tajný klíč používaný šifrovacím algoritmem Tato hodnota musí být šestnáctkovým řetězcem příslušné délky (na základě hodnoty v dešifrování), vygenerovat nebo buď pomocí hodnoty připojené k, IsolateApps. Přidáním IsolateApps dáte pokyn ASP.NET k použití jedinečné hodnoty pro každou aplikaci. Výchozí hodnota je AutoGenerate, IsolateApps. |
| ověření | Označuje algoritmus použitý k ověření. Tento atribut může mít jednu z následujících čtyř hodnot:-AES-používá algoritmus standard AES (Advanced Encryption Standard) (AES). -MD5 – používá algoritmus [MD5 (Message-Digest 5)](http://en.wikipedia.org/wiki/MD5) . -SHA1 – používá algoritmus [SHA1](http://en.wikipedia.org/wiki/Sha1) (výchozí). -3DES-používá algoritmus Triple DES. |
| validationKey | Tajný klíč používaný algoritmem ověřování. Tato hodnota musí být šestnáctkový řetězec odpovídající délky (na základě hodnoty v ověřování), vygenerovat nebo buď pomocí hodnoty připojené k, IsolateApps. Přidáním IsolateApps dáte pokyn ASP.NET k použití jedinečné hodnoty pro každou aplikaci. Výchozí hodnota je AutoGenerate, IsolateApps. |

**Tabulka 2**: atributy elementu &lt;machineKey&gt;

Důkladná diskuze o těchto možnostech šifrování a ověřování a o specialistech a nevýhody různých algoritmů jsou nad rámec tohoto kurzu. Podrobný pohled na tyto problémy, včetně pokynů k používání šifrovacích a ověřovacích algoritmů, jaké délky klíčů použít a jakým způsobem nejlépe vygenerujete tyto klíče, najdete v článku *profesionální ASP.NET 2,0 zabezpečení, členství a Správa rolí*.

Ve výchozím nastavení se klíče používané pro šifrování a ověřování generují automaticky pro každou aplikaci a tyto klíče se ukládají v rámci místního úřadu zabezpečení (LSA). V krátkém případě je ve výchozím nastavení zaručeno použití jedinečných klíčů na webovém serveru a na jednotlivých webových serverech. V důsledku toho toto výchozí chování nebude fungovat v následujících dvou scénářích:

- **Webové farmy** – ve scénáři [webové farmy](http://en.wikipedia.org/wiki/Web_farm) je jediná webová aplikace hostovaná na více webových serverech pro účely škálovatelnosti a redundance. Všechny příchozí požadavky jsou odesílány na server ve farmě, což znamená, že po celou dobu životnosti uživatelské relace se mohou pro zpracování svých různých požadavků použít různé servery. V důsledku toho musí každý server používat stejné šifrovací a ověřovací klíče, aby byl lístek ověřování pomocí formulářů vytvořený, zašifrovaný a ověřený na jednom serveru možné dešifrovat a ověřit na jiném serveru ve farmě.
- **Sdílení lístků mezi aplikacemi** – jeden webový server může hostovat několik aplikací ASP.NET. Pokud potřebujete, aby tyto různé aplikace sdílely jeden lístek ověřování pomocí formulářů, je nezbytné, aby se jejich šifrovací a ověřovací klíče shodovaly.

Když pracujete v nastavení webové farmy nebo sdílíte ověřovací lístky napříč aplikacemi na stejném serveru, budete muset v ovlivněných aplikacích nakonfigurovat prvek &lt;machineKey&gt;, aby se hodnoty decryptionKey a validationKey shodovaly.

I když žádné z výše uvedených scénářů neplatí pro naši ukázkovou aplikaci, můžeme pořád zadat explicitní hodnoty decryptionKey a validationKey a definovat algoritmy, které se mají použít. Přidejte do souboru Web. config nastavení &lt;machineKey&gt;:

[!code-xml[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample5.xml)]

Další informace najdete v tématu [Postup: Konfigurace MachineKey v ASP.NET 2,0](https://msdn.microsoft.com/library/ms998288.aspx).

> [!NOTE]
> Hodnoty decryptionKey a validationKey byly získány z webové stránky [Steve Gibsons](http://www.grc.com/stevegibson.htm) [Perfect hesly](https://www.grc.com/passwords.htm), která generuje 64 náhodné hexadecimální znaky na každé návštěvě stránky. Chcete-li snížit pravděpodobnost, že tyto klíče přizpůsobují své možnosti v produkčních aplikacích, doporučujeme nahradit výše uvedené klíče náhodným generováním na stránce dokonalých hesel.

## <a name="step-4-storing-additional-user-data-in-the-ticket"></a>Krok 4: uložení dalších uživatelských dat do lístku

Mnoho webových aplikací zobrazuje informace o zobrazení stránky v aktuálně přihlášeném uživateli nebo jejich základu. Například webová stránka může zobrazit jméno uživatele a datum posledního přihlášení v horním rohu každé stránky. Lístek ověřování pomocí formulářů uchovává uživatelské jméno aktuálně přihlášeného uživatele, ale pokud potřebujete nějaké další informace, musí stránka přejít do úložiště uživatele – obvykle databáze – pro vyhledávání informací, které nejsou uložené v ověřovacím lístku.

S malým počtem kódů můžeme do lístku pro ověřování pomocí formulářů ukládat Další informace o uživateli. Taková data lze vyjádřit prostřednictvím [vlastnosti UserData](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.userdata.aspx)v rámci [třídy FormsAuthenticationTicket](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.aspx). Toto je užitečné místo pro vložení malého množství informací o uživateli, který je často potřeba. Hodnota zadaná ve vlastnosti UserData je obsažena v rámci souboru cookie ověřovacího lístku a, podobně jako ostatní pole lístků, je zašifrováno a ověřeno na základě konfigurace systému ověřování pomocí formulářů. Ve výchozím nastavení je pro UserData prázdný řetězec.

Aby bylo možné ukládat data uživatelů do ověřovacího lístku, musíme na přihlašovací stránce napsat část kódu, která bude připravovat informace specifické pro uživatele a uložit je do lístku. Vzhledem k tomu, že UserData je vlastnost typu řetězec, data, která jsou v něm uložena, musí být správně serializována jako řetězec. Představte si například, že naše úložiště uživatelů zahrnovalo datum narození a jméno svého zaměstnavatele a že jsme chtěli tyto dvě hodnoty vlastností Uložit do ověřovacího lístku. Tyto hodnoty jsme mohli serializovat na řetězec zřetězením data uživatele o narození řetězce s svislým kanálem (|) následovaným názvem zaměstnavatele. Pro uživatele narozené 15. srpna 1974, který spolupracuje s Northwind Traders, přiřadíme tuto vlastnost UserData jako řetězec: 1974-08-15 | Northwind Traders.

Kdykoliv potřebujeme přístup k datům uloženým v lístku, můžeme to udělat tak, že převedeme FormsAuthenticationTicket a deserializaci aktuálního požadavku na vlastnost UserData. V případě příkladu data narození a jméno zaměstnavatele by byl řetězec UserData rozdělen do dvou podřetězců na základě oddělovače (|).

[v ověřovacím lístku mohou být uloženy ![Další informace o uživateli.](forms-authentication-configuration-and-advanced-topics-vb/_static/image11.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image10.png)

**Obrázek 04**: Další informace o uživateli mohou být uloženy v ověřovacím lístku ([kliknutím zobrazíte obrázek v plné velikosti).](forms-authentication-configuration-and-advanced-topics-vb/_static/image12.png)

### <a name="writing-information-to-userdata"></a>Zápis informací do UserData

Bohužel přidání informací specifických pro uživatele do lístku pro ověřování pomocí formulářů není tak jasné, jako by bylo možné očekávat. Vlastnost UserData třídy FormsAuthenticationTicket je pouze pro čtení a lze ji zadat pouze prostřednictvím konstruktoru třídy FormsAuthenticationTicket. Když zadáte vlastnost UserData v konstruktoru, musíme taky zadat další hodnoty lístku: uživatelské jméno, datum problému, vypršení platnosti atd. Když jsme vytvořili přihlašovací stránku v předchozím kurzu, měla by být pro nás zpracována třídou FormsAuthentication. Při přidávání UserData do FormsAuthenticationTicket budeme muset napsat kód, který bude replikovat většinu funkcí již poskytovaných třídou FormsAuthentication.

Podíváme se na potřebný kód pro práci s UserData, a to tak, že aktualizujete stránku Login. aspx a zaznamenáte si další informace o uživateli k ověřovacímu lístku. Předstírat, že naše uživatelské úložiště obsahuje informace o společnosti, pro kterou uživatel pracuje, a o jejich názvu a o tom, že chceme tyto informace zachytit v ověřovacím lístku. Aktualizujte obslužnou rutinu události LoginButton kliknutí na stránku Login. aspx, aby kód vypadal jako následující:

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample6.vb)]

Pojďme krokovat tento kód po jednotlivých řádcích. Metoda začíná definováním čtyř polí řetězců: uživatelé, hesla, companyName a titleAtCompany. Tato pole obsahují uživatelská jména, hesla, názvy společností a názvy uživatelských účtů v systému, z nichž jsou tři: Scott, Jisun a Sam. V reálné aplikaci se tyto hodnoty dotazují z úložiště uživatele, ale nejsou pevně zakódované ve zdrojovém kódu stránky.

V předchozím kurzu, pokud jsou zadané přihlašovací údaje platné, jsme jednoduše volali FormsAuthentication. RedirectFromLoginPage (UserName. text, RememberMe. Checked), který provedl následující kroky:

1. Vytvoření lístku pro ověřování formulářů
2. Lístek se zapsal do příslušného úložiště. Pro lístky ověřování založené na souborech cookie se používá kolekce souborů cookie v prohlížeči. v případě ověřovacích lístků bez souborů cookie jsou data lístků serializovaná na adresu URL.
3. Přesměrováno uživatele na příslušnou stránku

Tyto kroky se replikují do výše uvedeného kódu. Za prvé, řetězec, který nakonec ukládáme do vlastnosti UserData, se vytvoří tak, že se zkombinuje název společnosti a název, přičemž tyto dvě hodnoty se znakem svislé čáry (|).

Dim userDataString As String = String.Concat(companyName(i), "|", titleAtCompany(i))

Dále je vyvolána metoda FormsAuthentication. GetAuthCookie, která vytvoří ověřovací lístek, zašifruje ho a ověří ho v závislosti na nastavení konfigurace a umístí ho do objektu HttpCookie.

Dim authCookie as HttpCookie = FormsAuthentication. GetAuthCookie (UserName. text, RememberMe. Checked)

Aby bylo možné pracovat s FormAuthenticationTicket vloženým v souboru cookie, musíme volat [metodu dešifrování](https://msdn.microsoft.com/library/system.web.security.formsauthentication.decrypt.aspx)třídy FormAuthentication, která předává hodnotu souboru cookie.

Dim lístek as FormsAuthenticationTicket = FormsAuthentication. dešifruje (authCookie. Value)

Pak vytvoříme *novou* instanci FormsAuthenticationTicket založenou na stávajících hodnotách FormsAuthenticationTicket. Tento nový lístek ale obsahuje informace specifické pro uživatele (userDataString).

Dim newTicket As FormsAuthenticationTicket = New FormsAuthenticationTicket(ticket.Version, ticket.Name, ticket.IssueDate, ticket.Expiration, ticket.IsPersistent, userDataString)

Pak zašifrujeme (a ověříme) novou instanci FormsAuthenticationTicket voláním [metody Encrypt](https://msdn.microsoft.com/library/system.web.security.formsauthentication.encrypt.aspx)a tato šifrovaná (a ověřená) data vložte zpátky do authCookie.

authCookie.Value = FormsAuthentication.Encrypt(newTicket)

Nakonec se authCookie přidá do kolekce Response. cookies a metoda GetRedirectUrl se zavolá k určení vhodné stránky pro odeslání uživatele.

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample7.vb)]

Veškerý tento kód je nutný, protože vlastnost UserData je jen pro čtení a třída FormsAuthentication neposkytuje žádné metody pro zadání informací o uživatelských geografických metodách ve svých GetAuthCookie, SetAuthCookie nebo RedirectFromLoginPage.

> [!NOTE]
> Kód, který jsme právě prozkoumali, ukládá do ověřovacího lístku založeného na souborech cookie informace specifické pro uživatele. Třídy zodpovědné za serializaci ověřovacího lístku Forms na adresu URL jsou interní pro .NET Framework. Dlouhý příběh je krátký. data uživatelů nemůžete ukládat do lístku pro ověřování pomocí formulářů bez souborů cookie.

### <a name="accessing-the-userdata-information"></a>Přístup k informacím o UserData

V tomto okamžiku se název a název společnosti každého uživatele uloží do vlastnosti UserData ověřovacího lístku formuláře, když se přihlásí. K těmto informacím můžete získat přístup z ověřovacího lístku na libovolné stránce, aniž byste museli ukládat uživatele do úložiště. Abychom se vypracovali, jak se tyto informace dají načíst z vlastnosti UserData, můžeme aktualizovat default. aspx, aby jeho uvítací zpráva obsahovala nejen jméno uživatele, ale i společnost, pro kterou pracují, a jejich název.

V současné době obsahuje default. aspx panel AuthenticatedMessagePanel s ovládacím prvkem popisek s názvem WelcomeBackMessage. Tento panel se zobrazuje jenom pro ověřené uživatele. Aktualizujte kód na stránce Default. aspx\_obslužnou rutinu události Load, aby vypadala takto:

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample8.vb)]

Pokud je Request. WelcomeBackMessage nastaven na hodnotu true, vlastnost text na začátku je nejprve nastavena na Vítejte zpět, *uživatelské jméno*. Pak je vlastnost User. identity převedena na objekt FormsIdentity, aby bylo možné získat přístup k základnímu FormsAuthenticationTicket. Jakmile budeme mít FormsAuthenticationTicket, deserializovatme vlastnost UserData na název společnosti a název. To je provedeno rozdělením řetězce na znak kanálu. Název a název společnosti se pak zobrazí v popisku WelcomeBackMessage.

Obrázek 5 znázorňuje snímek obrazovky s tímto zobrazením v akci. Když se přihlásíte jako Scott, zobrazí se uvítací zpráva s oznámením, která obsahuje společnost a název Scott.

[Zobrazuje se ![název společnosti a názvu aktuálně přihlášeného uživatele.](forms-authentication-configuration-and-advanced-topics-vb/_static/image14.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image13.png)

**Obrázek 05**: zobrazí se aktuálně přihlášená společnost a název uživatele ([kliknutím zobrazíte obrázek v plné velikosti](forms-authentication-configuration-and-advanced-topics-vb/_static/image15.png)).

> [!NOTE]
> Vlastnost UserData ověřovacího lístku slouží jako mezipaměť pro úložiště uživatele. Stejně jako jakákoli mezipaměť, je nutné ji aktualizovat při změně podkladových dat. Pokud například existuje webová stránka, ze které mohou uživatelé aktualizovat svůj profil, musí být pole uložená v mezipaměti ve vlastnosti UserData aktualizována, aby odrážela změny provedené uživatelem.

## <a name="step-5-using-a-custom-principal"></a>Krok 5: použití vlastního objektu zabezpečení

U každého příchozího požadavku se FormsAuthenticationModule pokusí ověřit uživatele. Pokud je k dispozici ověřovací lístek bez vypršení platnosti, FormsAuthenticationModule přiřadí vlastnost HttpContext. User k novému objektu GenericPrincipal. Tento objekt GenericPrincipal má identitu typu FormsIdentity, která obsahuje odkaz na lístek ověřování pomocí formulářů. Třída GenericPrincipal obsahuje minimální funkčnost, kterou vyžaduje třída, která implementuje IPrincipal – má pouze vlastnost identity a metodu IsInRole.

Objekt zabezpečení má dvě povinnosti: k určení rolí, do kterých uživatel patří, a k poskytnutí informací o identitě. K tomu je možné využít metodu IsInRole (*roleName*) a vlastnost identity rozhraní IPrincipal (v uvedeném pořadí). Třída GenericPrincipal umožňuje určit pole řetězců názvů rolí prostřednictvím jeho konstruktoru; jeho Metoda IsInRole (*roleName*) pouze kontroluje, zda předaná v *roleName* existuje v poli řetězců. Když FormsAuthenticationModule vytvoří GenericPrincipal, předá do konstruktoru GenericPrincipal v prázdném poli řetězce. V důsledku toho všechna volání IsInRole budou vždycky vracet hodnotu false.

Třída GenericPrincipal splňuje potřeby většiny scénářů ověřování založených na formulářích, kde se role nepoužívají. V případech, kdy výchozí zpracování role není dostatečné nebo když potřebujete k uživateli přidružit vlastní objekt IIdentity, můžete v pracovním postupu ověřování vytvořit vlastní objekt IPrincipal a přiřadit ho k vlastnosti HttpContext. User.

> [!NOTE]
> Jak uvidíme v budoucích kurzech, a to v případě ASP. Rozhraní .NET Framework Roles je povoleno, vytvoří vlastní objekt zabezpečení typu [Tento RolePrincipal](https://msdn.microsoft.com/library/system.web.security.roleprincipal.aspx) a přepíše objekt GenericPrincipal, který se vytvořil pro ověřování pomocí formulářů. Provede to pro přizpůsobení metody IsInRole objektu zabezpečení rozhraní rozhraní API architektury rolí.

Vzhledem k tomu, že jsme se ještě dodržovali s rolemi, jediným důvodem, proč by bylo vytvoření vlastního objektu zabezpečení v tomto situaci, bylo přidružit k objektu zabezpečení vlastní objekt IIdentity. V kroku 4 jsme se podívali na ukládání dalších informací o uživatelích do vlastnosti UserData ověřovacího lístku, zejména podle názvu společnosti a jejich názvu. Informace o UserData jsou ale přístupné jenom prostřednictvím ověřovacího lístku a pak jako serializovaného řetězce, což znamená, že kdykoli chceme zobrazit informace o uživateli uložené v lístku, potřebujeme analyzovat vlastnost UserData.

Prostředí pro vývojáře můžeme vylepšit vytvořením třídy, která implementuje IIdentity a obsahuje vlastnosti CompanyName a title. Díky tomu může vývojář získat přístup k názvu a názvu společnosti aktuálně přihlášeného uživatele přímo prostřednictvím vlastností CompanyName a title, aniž by bylo nutné znát způsob, jak analyzovat vlastnost UserData.

### <a name="creating-the-custom-identity-and-principal-classes"></a>Vytvoření vlastní třídy identity a objektů zabezpečení

Pro tento kurz vytvoříme vlastní objekty zabezpečení a identity ve složce App\_Code. Začněte tím, že do svého projektu přidáte aplikaci\_kódu, kliknete pravým tlačítkem myši na název projektu v Průzkumník řešení, vyberete možnost Přidat složku ASP.NET a zvolíte\_kód aplikace. Složka\_kódu aplikace je speciální složka ASP.NET, která obsahuje soubory třídy specifické pro web.

> [!NOTE]
> Složka\_kódu aplikace by měla být použita pouze při správě projektu prostřednictvím modelu projektu webu. Pokud používáte [model projektu webové aplikace](https://msdn.microsoft.com/asp.net/Aa336618.aspx), vytvořte standardní složku a přidejte do ní třídy. Můžete například přidat novou složku s názvem Classes a umístit svůj kód do tohoto umístění.

Dále přidejte dva nové soubory třídy do složky\_kódu aplikace, jednu s názvem CustomIdentity. vb a jednu s názvem CustomPrincipal. vb.

[![do projektu přidejte třídy CustomIdentity a CustomPrincipal.](forms-authentication-configuration-and-advanced-topics-vb/_static/image17.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image16.png)

**Obrázek 06**: přidejte do projektu třídy CustomIdentity a CustomPrincipal ([kliknutím zobrazíte obrázek v plné velikosti](forms-authentication-configuration-and-advanced-topics-vb/_static/image18.png)).

Třída CustomIdentity zodpovídá za implementaci rozhraní IIdentity, které definuje vlastnosti AuthenticationType, Authenticated a Name. Kromě požadovaných vlastností vás zajímá vystavení základního autentizačního lístku s formuláři a také vlastností pro název a název společnosti uživatele. Do třídy CustomIdentity zadejte následující kód.

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample9.vb)]

Všimněte si, že třída obsahuje členskou proměnnou FormsAuthenticationTicket (\_lístek) a že informace o lístku musí být dodány prostřednictvím konstruktoru. Tato data lístku se používají při vracení názvu identity. vlastnost UserData je analyzována tak, aby vracela hodnoty vlastností CompanyName a title.

Dále vytvořte třídu CustomPrincipal. Vzhledem k tomu, že s rolemi v tomto situaci nejsou obavy, konstruktor třídy CustomPrincipal přijímá pouze objekt CustomIdentity; jeho Metoda IsInRole vždy vrátí hodnotu false.

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample10.vb)]

### <a name="assigning-a-customprincipal-object-to-the-incoming-requests-security-context"></a>Přiřazení objektu CustomPrincipal k kontextu zabezpečení příchozího požadavku

Nyní máme třídu, která rozšiřuje výchozí specifikaci IIdentity, aby zahrnovala vlastnosti CompanyName a title, a také vlastní třídu zabezpečení, která používá vlastní identitu. Jsme připraveni přejít do kanálu ASP.NET a přiřazovat vlastní objekt zabezpečení do kontextu zabezpečení příchozího požadavku.

Kanál ASP.NET přijímá příchozí požadavek a zpracovává ho pomocí několika kroků. V každém kroku se vyvolá konkrétní událost, která vývojářům umožní klepnout do kanálu ASP.NET a upravit požadavek v určitých fázích životního cyklu. FormsAuthenticationModule například počká, až ASP.NET vyvolá [událost AuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx). v takovém případě zkontroluje příchozí požadavek na ověřovací lístek. Pokud se najde ověřovací lístek, vytvoří se objekt GenericPrincipal a přiřadí se k vlastnosti HttpContext. User.

Po události AuthenticateRequest kanál ASP.NET vyvolá [událost PostAuthenticateRequest](https://msdn.microsoft.com/library/system.web.httpapplication.postauthenticaterequest.aspx), což je místo, kde můžeme nahradit objekt GenericPrincipal vytvořený FormsAuthenticationModule s instancí našeho objektu CustomPrincipal. Obrázek 7 znázorňuje tento pracovní postup.

[![GenericPrincipal nahrazuje CustomPrincipal v události PostAuthenticationRequest](forms-authentication-configuration-and-advanced-topics-vb/_static/image20.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image19.png)

**Obrázek 07**: GenericPrincipal se nahrazuje CustomPrincipal v události PostAuthenticationRequest ([kliknutím zobrazíte obrázek v plné velikosti](forms-authentication-configuration-and-advanced-topics-vb/_static/image21.png)).

Aby bylo možné spustit kód v reakci na událost kanálu ASP.NET, můžeme buď vytvořit příslušnou obslužnou rutinu události v Global. asax, nebo vytvořit vlastní modul HTTP. V tomto kurzu vytvoříme obslužnou rutinu události v Global. asax. Začněte tím, že do svého webu přidáte Global. asax. Klikněte pravým tlačítkem myši na název projektu v Průzkumník řešení a přidejte položku typu globální třída aplikace s názvem Global. asax.

[![přidat soubor Global. asax na web](forms-authentication-configuration-and-advanced-topics-vb/_static/image23.png)](forms-authentication-configuration-and-advanced-topics-vb/_static/image22.png)

**Obrázek 08**: Přidání souboru Global. asax na web ([kliknutím zobrazíte obrázek v plné velikosti](forms-authentication-configuration-and-advanced-topics-vb/_static/image24.png))

Výchozí šablona Global. asax obsahuje obslužné rutiny událostí pro určitý počet událostí kanálu ASP.NET, včetně události Start, end a [Error](https://msdn.microsoft.com/library/system.web.httpapplication.error.aspx), mimo jiné. Nebojte se odebrat tyto obslužné rutiny událostí, protože je pro tuto aplikaci nepotřebujeme. Událost, které vás zajímá, je PostAuthenticateRequest. Aktualizujte soubor Global. asax tak, aby jeho značky vypadaly podobně jako v následujícím příkladu:

[!code-aspx[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample11.aspx)]

Metoda aplikace\_OnPostAuthenticateRequest se spustí pokaždé, když modul runtime ASP.NET vyvolá událost PostAuthenticateRequest, která se stane jednou u každé příchozí žádosti stránky. Obslužná rutina události se spustí tak, že zkontroluje, jestli je uživatel ověřený a ověřený přes ověřování pomocí formulářů. Pokud ano, vytvoří se nový objekt CustomIdentity a v jeho konstruktoru se předala ověřovací lístek aktuální žádosti. Za tímto je vytvořen objekt CustomPrincipal a byl v jeho konstruktoru předán právě vytvořený objekt CustomIdentity. Nakonec je kontext zabezpečení aktuální žádosti přiřazen k nově vytvořenému objektu CustomPrincipal.

Všimněte si, že poslední krok a přidružení objektu CustomPrincipal k kontextu zabezpečení žádosti – přiřadí objekt zabezpečení dvěma vlastnostem: HttpContext. User a Thread. CurrentPrincipal. Tato dvě přiřazení jsou nezbytná z důvodu způsobu zpracování kontextů zabezpečení v ASP.NET. .NET Framework přidruží kontext zabezpečení ke každému běžícímu vláknu; Tyto informace jsou k dispozici jako objekt IPrincipal prostřednictvím [vlastnosti CurrentPrincipal](https://msdn.microsoft.com/library/system.threading.thread.currentcontext.aspx) [objektu vlákna](https://msdn.microsoft.com/library/system.threading.thread.aspx). To je matoucí, že ASP.NET má vlastní informace o kontextu zabezpečení (HttpContext. User).

V některých případech je při určování kontextu zabezpečení prověřena vlastnost Thread. CurrentPrincipal. v jiných scénářích se používá HttpContext. User. Například existují funkce zabezpečení v rozhraní .NET, které vývojářům umožňují deklarativní určení toho, jakým způsobem mohou uživatelé nebo role vytvářet instance třídy nebo volat konkrétní metody (viz [Přidání autorizačních pravidel do obchodních a datových vrstev pomocí PrincipalPermissionAttributes](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)). Pod rámec těchto vazeb tyto deklarativní techniky určují kontext zabezpečení prostřednictvím vlastnosti Thread. CurrentPrincipal.

V jiných scénářích je použita vlastnost HttpContext. User. Například v předchozím kurzu jsme tuto vlastnost použili k zobrazení aktuálně přihlášeného uživatelského jména uživatele. Jasně je nutné, aby se informace o kontextu zabezpečení ve vlastnostech vlákna. CurrentPrincipal a HttpContext. User shodovaly.

Modul runtime ASP.NET automaticky synchronizuje Tyto hodnoty vlastností pro nás. Tato synchronizace se však vyskytne po události AuthenticateRequest, ale *před* událostí PostAuthenticateRequest. V důsledku toho, aby při přidávání vlastního objektu zabezpečení v události PostAuthenticateRequest bylo nutné, aby bylo jisté, že ručně přiřadí vlákna. CurrentPrincipal nebo else Thread. CurrentPrincipal a HttpContext. uživatel nebude synchronizován. Podrobnější diskusi k tomuto problému najdete v tématu [kontext. User vs. Thread. CurrentPrincipal](http://leastprivilege.com/2005/11/23/context-user-vs-thread-currentprincipal/) .

### <a name="accessing-the-companyname-and-title-properties"></a>Přístup k vlastnostem CompanyName a názvu

Pokaždé, když požadavek dorazí a odešle do modulu ASP.NET, aktivuje se obslužná rutina události aplikace\_OnPostAuthenticateRequest v Global. asax. Pokud byl požadavek úspěšně ověřen serverem FormsAuthenticationModule, obslužná rutina události vytvoří nový objekt CustomPrincipal s objektem CustomIdentity na základě lístku pro ověřování pomocí formulářů. Díky této logice je přístup k informacím o aktuálně přihlášeném uživatelskému jménu a názvu společnosti neuvěřitelně přímočarý.

Vraťte se na stránku\_načíst obslužnou rutinu události ve formátu default. aspx, kde v kroku 4 jste napsali kód pro načtení lístku ověřování formuláře a k analýze vlastnosti UserData, aby se zobrazil název a název společnosti uživatele. U aktuálně používaných objektů CustomPrincipal a CustomIdentity není nutné analyzovat hodnoty z vlastnosti UserData lístku. Místo toho jednoduše Získejte odkaz na objekt CustomIdentity a použijte jeho vlastnosti CompanyName a title:

[!code-vb[Main](forms-authentication-configuration-and-advanced-topics-vb/samples/sample12.vb)]

## <a name="summary"></a>Souhrn

V tomto kurzu jsme prozkoumali, jak přizpůsobit nastavení systému ověřování pomocí formulářů pomocí souboru Web. config. Prohlédli jsme se na tom, jak se zpracovává vypršení platnosti ověřovacího lístku a jak se používají ochranná a ověřovací ochrana k ochraně lístku před kontrolou a úpravou. Nakonec jsme probrali použití vlastnosti UserData v ověřovacím lístku pro ukládání dalších informací o uživateli do samotného lístku a použití vlastních objektů zabezpečení a identity k zveřejnění těchto informací v lépe přívětivém způsobu vývojářů.

V tomto kurzu se uzavírá naše zkoumání ověřování formulářů v ASP.NET. Další kurz spustí naši cestu do prostředí členství.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Rozhmyz ověřování formulářů](http://aspnet.4guysfromrolla.com/articles/072005-1.aspx)
- [Vysvětlení: ověřování prostřednictvím formulářů v ASP.NET 2,0](https://msdn.microsoft.com/library/aa480476.aspx)
- [Postupy: ochrana ověřování pomocí formulářů v ASP.NET 2,0](https://msdn.microsoft.com/library/ms998310.aspx)
- [Professional ASP.NET 2,0 zabezpečení, členství a Správa rolí](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html) (ISBN: 978-0-7645-9698-8)
- [Zabezpečení ovládacích prvků přihlášení](https://msdn.microsoft.com/library/ms178346.aspx)
- [&gt; element ověřování &lt;](https://msdn.microsoft.com/library/532aee0e.aspx)
- [&gt; prvek &lt;Forms pro &lt;ověřování&gt;](https://msdn.microsoft.com/library/1d3t3c61.aspx)
- [Element &lt;machineKey&gt;](https://msdn.microsoft.com/library/w8h3skw9.aspx)
- [Princip lístku a souboru cookie pro ověřování formulářů](https://support.microsoft.com/kb/910443)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>Výukové video o tématech obsažených v tomto kurzu

- [Postup změny vlastností ověřování formulářů](../../../videos/authentication/how-to-change-the-forms-authentication-properties.md)
- [Jak nastavit a používat ověřování bez souborů cookie v aplikaci ASP.NET](../../../videos/authentication/how-to-setup-and-use-cookie-less-authentication-in-an-aspnet-application.md)
- [Přemístění formulářů ASP pro přihlášení](../../../videos/authentication/asp-forms-login-relocation.md)
- [Konfigurace vlastního klíče přihlašovacích formulářů](../../../videos/authentication/forms-login-custom-key-configuration.md)
- [Přidání vlastních dat do metody ověřování](../../../videos/authentication/add-custom-data-to-the-authentication-method.md)
- [Použití vlastních hlavních objektů](../../../videos/authentication/use-custom-principal-objects.md)

### <a name="about-the-author"></a>O autorovi

Scott Mitchell, autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je *[Sams naučit se ASP.NET 2,0 za 24 hodin](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* . Scott se dá kontaktovat [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Alicja Maziarz. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com).

> [!div class="step-by-step"]
> [Předchozí](an-overview-of-forms-authentication-vb.md)

---
uid: web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs
title: Přehled ověřování prostřednictvím formulářů (C#) | Microsoft Docs
author: rick-anderson
description: Vytváření vlastních tras
ms.author: riande
ms.date: 01/14/2008
ms.assetid: de2d65b9-aadc-42ba-abe1-4e87e66521a0
msc.legacyurl: /web-forms/overview/older-versions-security/introduction/an-overview-of-forms-authentication-cs
msc.type: authoredcontent
ms.openlocfilehash: 009c3f84e00d648ede4a15e530ceac2d23e01eec
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74620456"
---
# <a name="an-overview-of-forms-authentication-c"></a>Přehled ověřování prostřednictvím formulářů (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/ASPNET_Security_Tutorial_02_CS.zip) nebo [stažení PDF](https://download.microsoft.com/download/2/F/7/2F705A34-F9DE-4112-BBDE-60098089645E/aspnet_tutorial02_FormsAuth_cs.pdf)

> V tomto kurzu se od pouhého diskuze k implementaci změní. Konkrétně se podíváme na implementaci ověřování formulářů. Webová aplikace, kterou začneme sestavovat v tomto kurzu, bude i nadále postavená v dalších kurzech, protože se přesunuje z jednoduchých ověřování pomocí formulářů na členství a role.
> 
> Další informace o tomto tématu najdete v tomto videu: [Použití ověřování Basic Forms v ASP.NET](../../../videos/authentication/using-basic-forms-authentication-in-aspnet.md).

## <a name="introduction"></a>Úvod

V [předchozím kurzu](security-basics-and-asp-net-support-cs.md) jsme probrali různé možnosti ověřování, autorizace a uživatelského účtu, které poskytuje ASP.NET. V tomto kurzu se od pouhého diskuze k implementaci změní. Konkrétně se podíváme na implementaci ověřování formulářů. Webová aplikace, kterou začneme sestavovat v tomto kurzu, bude i nadále postavená v dalších kurzech, protože se přesunuje z jednoduchých ověřování pomocí formulářů na členství a role.

Tento kurz začíná podrobnějším pohledem na pracovní postup ověřování pomocí formulářů, které jsme provedli v předchozím kurzu. V tomto případě vytvoříme web ASP.NET, který vám umožní vydemo koncepty ověřování pomocí formulářů. Dále nakonfigurujeme lokalitu, aby používala ověřování pomocí formulářů, vytvořili jednoduchou přihlašovací stránku a zjistili, jak určit, jestli je uživatel ověřený, a pokud ano, uživatelské jméno, se kterým se přihlásilo.

Porozumění pracovnímu postupu ověřování pomocí formulářů, jeho povolení ve webové aplikaci a vytváření přihlašovacích a odhlašovacích stránek jsou všechny důležité kroky při vytváření ASP.NET aplikace, která podporuje uživatelské účty a ověřuje uživatele prostřednictvím webové stránky. Z tohoto důvodu jsou k dispozici tyto kurzy – a protože již máte zkušenosti s konfigurací ověřování pomocí formulářů v minulých projektech, doporučujeme, abyste tento kurz nastavili v plném rozsahu.

## <a name="understanding-the-forms-authentication-workflow"></a>Princip pracovního postupu ověřování formulářů

Když modul runtime ASP.NET zpracuje požadavek na prostředek ASP.NET, například stránku ASP.NET nebo webovou službu ASP.NET, požadavek během svého životního cyklu vyvolá několik událostí. Na začátku a na konci žádosti byly vyvolány události, které se vyvolaly při ověřování a autorizaci žádosti, událost vyvolaná v případě neošetřené výjimky a tak dále. Chcete-li zobrazit úplný seznam událostí, přečtěte si [události objektu HttpApplication](https://msdn.microsoft.com/library/system.web.httpapplication_events.aspx).

*Moduly HTTP* jsou spravované třídy, jejichž kód je spuštěn v reakci na konkrétní událost v životním cyklu žádosti. ASP.NET se dodává s několika moduly HTTP, které provádějí zásadní úlohy na pozadí. Dva předdefinované moduly HTTP, které jsou obzvláště relevantní pro naši diskuzi:

- **[`FormsAuthenticationModule`](https://msdn.microsoft.com/library/system.web.security.formsauthenticationmodule.aspx)** – ověřuje uživatele pomocí kontrolního lístku pro formuláře, který je obvykle zahrnutý v kolekci souborů cookie uživatele. Pokud neexistují žádné ověřovací lístky formulářů, uživatel je anonymní.
- **[`UrlAuthorizationModule`](https://msdn.microsoft.com/library/system.web.security.urlauthorizationmodule.aspx)** – určuje, jestli má aktuální uživatel autorizaci pro přístup k požadované adrese URL. Tento modul určí autoritu tím, že se pojednáním s autorizačními pravidly zadanými v konfiguračních souborech aplikace. ASP.NET také zahrnuje [`FileAuthorizationModule`](https://msdn.microsoft.com/library/system.web.security.fileauthorizationmodule.aspx) , který určuje autoritu v rámci konzultací s požadovanými seznamy řízení přístupu (ACL) souborů.

`FormsAuthenticationModule` se pokusí ověřit uživatele před spuštěním `UrlAuthorizationModule` (a `FileAuthorizationModule`). Pokud uživatel, který vytváří požadavek, nemá oprávnění k přístupu k požadovanému prostředku, modul autorizace žádost ukončí a vrátí [neautorizovaný stav HTTP 401](http://www.checkupdown.com/status/E401.html) . Ve scénářích ověřování systému Windows se do prohlížeče vrátí stav HTTP 401. Tento stavový kód způsobí, že v prohlížeči se uživateli zobrazí výzva k zadání přihlašovacích údajů prostřednictvím modálního dialogového okna. Při ověřování pomocí formulářů se ale stav neautorizovaného protokolu HTTP 401 nikdy neposílá do prohlížeče, protože FormsAuthenticationModule zjistí tento stav a změní ho tak, aby místo toho přesměroval uživatele na přihlašovací stránku (přes stav [přesměrování HTTP 302](http://www.checkupdown.com/status/E302.html) ).

Zodpovědnost na přihlašovací stránce slouží k určení, jestli jsou přihlašovací údaje uživatele platné, a pokud ano, vytvoří lístek pro ověřování pomocí formulářů a přesměruje uživatele zpátky na stránku, na kterou se pokoušel navštívit. Ověřovací lístek je součástí dalších požadavků na stránky na webu, které `FormsAuthenticationModule` používá k identifikaci uživatele.

![Pracovní postup ověřování formulářů](an-overview-of-forms-authentication-cs/_static/image1.png)

**Obrázek 1**: Pracovní postup ověřování formulářů

### <a name="remembering-the-authentication-ticket-across-page-visits"></a>Zapamatování ověřovacího lístku v rámci stránkových návštěv

Po přihlášení musí být lístek ověřování formulářů odeslán zpět na webový server na každý požadavek, aby uživatel zůstal přihlášený při procházení webu. To se obvykle provádí umístěním ověřovacího lístku do kolekce souborů cookie uživatele. [Soubory cookie](http://en.wikipedia.org/wiki/HTTP_cookie) jsou malé textové soubory, které se nacházejí v počítači uživatele a jsou přenášeny do hlaviček protokolu HTTP na každém požadavku na web, který soubor cookie vytvořil. Proto po vytvoření lístku pro ověřování pomocí formulářů a jeho uložení do souborů cookie prohlížeče Každá následná návštěva tohoto webu odešle ověřovací lístek spolu s požadavkem, čímž uživatele identifikuje.

Jedním z aspektů souborů cookie je vypršení platnosti, což je datum a čas, kdy prohlížeč zahodí soubor cookie. Když vyprší platnost souboru cookie pro ověřování formulářů, uživatel už nemůže být ověřený a stane se z něj anonymní. Když se uživatel navštíví z veřejného terminálu, je pravděpodobné, že budou chtít, aby ověřovací lístek vypršel při zavření prohlížeče. Při návštěvě z domova ale stejný uživatel může chtít, aby byl ověřovací lístek zapamatovatný v prohlížeči, aby se nemusel znovu přihlašovat při každé návštěvě webu. Toto rozhodnutí často provádí uživatel ve formě zaškrtávacího políčka "zapamatovat mě" na přihlašovací stránce. V kroku 3 se podíváme na to, jak na přihlašovací stránce implementovat zaškrtávací políčko zapamatovatelné. V následujícím kurzu se podrobně řeší nastavení časového limitu ověřovacího lístku.

> [!NOTE]
> Je možné, že uživatelský agent použitý k přihlášení k webu nemusí podporovat soubory cookie. V takovém případě může ASP.NET použít lístky pro ověřování pomocí formulářů cookie. V tomto režimu je ověřovací lístek zakódovaný do adresy URL. Podíváme se, když se použijí ověřovací lístky cookie a jak se vytvářejí a spravují v dalším kurzu.

### <a name="the-scope-of-forms-authentication"></a>Rozsah ověřování formulářů

`FormsAuthenticationModule` je spravovaný kód, který je součástí modulu runtime ASP.NET. Před verzí 7 webového serveru [Internetová informační služba](https://www.iis.net/) od Microsoftu existovala odlišná bariéra mezi KANÁLEM HTTP služby IIS a kanálem běhového prostředí ASP.NET. V krátkém případě se v IIS 6 a starších verzích `FormsAuthenticationModule` spouští jenom v případě, že je žádost delegovaná z IIS na modul runtime ASP.NET. Ve výchozím nastavení služba IIS zpracovává samotný statický obsah, jako jsou stránky HTML a soubory CSS a obrázky – a při požadavku na stránku s příponou. aspx,. asmx nebo. ashx jenom vypnul požadavky na modul runtime ASP.NET.

Služba IIS 7 ale umožňuje integrované kanály IIS a ASP.NET. S několika konfiguračními nastaveními můžete nastavit IIS 7, aby se FormsAuthenticationModule pro *všechny* požadavky. Kromě toho se službou IIS 7 můžete definovat autorizační pravidla URL pro soubory libovolného typu. Další informace najdete v tématu [změny mezi VERZEMI IIS6 a IIS7 Security](https://www.iis.net/learn/get-started/whats-new-in-iis-7/changes-in-security-between-iis-60-and-iis-7-and-above), [zabezpečení webové platformy](https://www.iis.net/learn/get-started/whats-new-in-iis-7/iis7-and-above-security-improvements)a [principem ověřování adres URL v IIS7](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/URL-Authorization/Understanding-IIS7-URL-Authorization).

Velký příběh ve verzích starších než IIS 7 můžete k ochraně prostředků zpracovávaných modulem runtime ASP.NET použít jenom ověřování pomocí formulářů. Podobně platí, že autorizační pravidla URL se aplikují jenom na prostředky zpracovávané modulem runtime ASP.NET. Ale u služby IIS 7 je možné integrovat FormsAuthenticationModule a UrlAuthorizationModule do kanálu HTTP služby IIS, což rozšiřuje tuto funkci na všechny požadavky.

## <a name="step-1-creating-an-aspnet-website-for-this-tutorial-series"></a>Krok 1: Vytvoření webu v ASP.NET pro tuto řadu kurzů

Aby bylo možné oslovit nejširší možnou cílovou skupinu, bude web ASP.NET sestaven v celé řadě a bude vytvořen s bezplatnou verzí sady Visual Studio 2008, [Visual Web Developer 2008](https://www.microsoft.com/express/vwd/)společnosti Microsoft. V databázi [edice Microsoft SQL Server 2005 Express](https://msdn.microsoft.com/sql/Aa336346.aspx) budeme implementovat úložiště `SqlMembershipProvider` uživatele. Pokud používáte sadu Visual Studio 2005 nebo jinou edici sady Visual Studio 2008 nebo SQL Server, nedělejte si starosti – tyto kroky budou téměř totožné a jakékoli netriviální rozdíly budou nahlášeny.

> [!NOTE]
> Ukázková webová aplikace použitá v každém kurzu je k dispozici jako soubor ke stažení. Tuto aplikaci ke stažení jsme vytvořili pomocí aplikace Visual Web Developer 2008 cílené pro .NET Framework verze 3,5. Vzhledem k tomu, že je aplikace cílena na rozhraní .NET 3,5, soubor Web. config obsahuje další konfigurační prvky specifické pro 3,5. Dlouhý příběh – Pokud jste ještě v počítači nainstalovali .NET 3,5, nebude webová aplikace ke stažení fungovat, aniž byste nejdřív odebrali značku 3,5 ze souboru Web. config.

Než budeme moct nakonfigurovat ověřování prostřednictvím formulářů, musíme nejdřív potřebovat web ASP.NET. Začněte vytvořením nového webu ASP.NET založeného na systému souborů. Chcete-li to provést, spusťte Visual Web Developer a pak přejděte do nabídky soubor a zvolte možnost Nový web a zobrazí se dialogové okno Nový web. Vyberte šablonu webu ASP.NET, nastavte rozevírací seznam umístění na systém souborů, vyberte složku, kam chcete umístit web, a nastavte jazyk na C#. Tím se vytvoří nový web s výchozí stránkou. aspx ASP.NET, datovou složkou aplikace\_a souborem Web. config.

> [!NOTE]
> Visual Studio podporuje dva režimy řízení projektů: Projekty webu a projekty webových aplikací. Webové projekty neobsahují soubor projektu, zatímco projekty webové aplikace napodobují architekturu projektu v aplikaci Visual Studio .NET 2002/2003 – obsahují soubor projektu a zkompiluje zdrojový kód projektu do jednoho sestavení, které je umístěno ve složce/bin. Visual Studio 2005 zpočátku podporuje jenom webové projekty, i když se model projektu webové aplikace znovu představil s aktualizací Service Pack 1. Visual Studio 2008 nabízí jak modely projektu. Edice Visual Web Developer 2005 a 2008 však podporují pouze projekty webu. Použijem model projektu webu. Pokud používáte jinou edici než Express a chcete místo toho použít [model projektu webové aplikace](https://msdn.microsoft.com/library/aa730880%28vs.80%29.aspx) , můžete to udělat, ale mějte na paměti, že mezi tím, co vidíte na obrazovce, a kroky, které je nutné vzít v těchto kurzech, může dojít k nějakým rozporům.

[![vytvoření nového webu založeného na systému souborů](an-overview-of-forms-authentication-cs/_static/image3.png)](an-overview-of-forms-authentication-cs/_static/image2.png)

**Obrázek 2**: Vytvoření nového webu založeného na systému souborů ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-cs/_static/image4.png))

### <a name="adding-a-master-page"></a>Přidání stránky předlohy

Dále do kořenového adresáře s názvem site. Master přidejte novou hlavní stránku. [Stránky předlohy](https://msdn.microsoft.com/library/wtxbf3hh.aspx) umožňují vývojáři stránky definovat šablonu pro lokalitu, která může být použita na ASP.NET stránky. Hlavní výhodou hlavních stránek je, že celkový vzhled webu může být definován v jednom umístění, což usnadňuje aktualizaci a vylepšení rozložení webu.

[![přidat hlavní stránku s názvem site. Master na web](an-overview-of-forms-authentication-cs/_static/image6.png)](an-overview-of-forms-authentication-cs/_static/image5.png)

**Obrázek 3**: Přidejte hlavní stránku s názvem site. Master na web ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-cs/_static/image7.png)).

Na stránce předlohy definujte rozložení stránky na úrovni webu. Můžete použít zobrazení Návrh a přidat libovolné rozložení nebo webové ovládací prvky, které potřebujete, nebo můžete ručně přidat značky v zobrazení zdroje. Rozčleněním rozložení stránky předlohy je napodobované rozložení používané v *[rámci práce s daty v řadě kurzů ASP.NET 2,0](../../data-access/index.md)* (viz obrázek 4). Stránka předlohy používá [kaskádové šablony stylů](http://www.w3schools.com/css/default.asp) pro umisťování a styly s nastaveními CSS definovanými v souboru Style. CSS (který je zahrnutý v tomto kurzu ke stažení). I když nemůžete říct od značky níže, jsou definována pravidla šablony stylů CSS tak, aby byl obsah navigace &lt;div&gt;je naprosto umístěný tak, aby se zobrazil vlevo a měla pevnou šířku 200 pixelů.

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample1.aspx)]

Stránka předlohy definuje rozložení statické stránky i oblasti, které lze upravit pomocí stránek ASP.NET, které používají stránku předlohy. Tyto upravitelné oblasti obsahu jsou označeny ovládacím prvkem `ContentPlaceHolder`, který se může zobrazit v obsahu &lt;div&gt;. Naše stránka předlohy obsahuje jeden `ContentPlaceHolder` (MainContent), ale stránka předlohy může mít několik prvků ContentPlaceHolder.

Pomocí značky uvedeného výše se přepíná na zobrazení Návrh zobrazuje rozložení stránky předlohy. Všechny stránky ASP.NET, které používají tuto stránku předlohy, budou mít jednotné rozložení s možností zadat značku `MainContent` oblasti.

[![stránku předlohy při prohlížení v návrhovém zobrazení](an-overview-of-forms-authentication-cs/_static/image9.png)](an-overview-of-forms-authentication-cs/_static/image8.png)

**Obrázek 4**: Stránka předlohy zobrazená v návrhovém zobrazení ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-cs/_static/image10.png))

### <a name="creating-content-pages"></a>Vytváření stránek obsahu

V tomto okamžiku máme stránku Default. aspx na našem webu, ale nepoužíváme tu stránku předlohy, kterou jsme právě vytvořili. I když je možné manipulovat s deklarativním označením webové stránky, aby používala stránku předlohy, pokud stránka ještě neobsahuje žádný obsah, je snazší ji jednoduše odstranit a znovu přidat do projektu a zadat hlavní stránku, která se má použít. Proto začněte odstraněním default. aspx z projektu.

Potom klikněte pravým tlačítkem myši na název projektu v Průzkumník řešení a vyberte možnost Přidat nový webový formulář s názvem default. aspx. Tentokrát zaškrtněte políčko "vybrat hlavní stránku" a ze seznamu zvolte stránku předloha lokality. Master.

[![přidat novou stránku Default. aspx, která umožňuje výběr stránky předlohy](an-overview-of-forms-authentication-cs/_static/image12.png)](an-overview-of-forms-authentication-cs/_static/image11.png)

**Obrázek 5**: Přidejte novou stránku Default. aspx, kterou zvolíte pro výběr stránky předlohy ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-forms-authentication-cs/_static/image13.png)

![Použití stránky předlohy Web. Master](an-overview-of-forms-authentication-cs/_static/image14.png)

**Obrázek 6**: Použití stránky předlohy Web. Master

> [!NOTE]
> Pokud používáte model projektu webové aplikace, dialogové okno Přidat novou položku nezahrnuje zaškrtávací políčko vybrat hlavní stránku. Místo toho je nutné přidat položku typu formulář webového obsahu. Po výběru možnosti formulář webového obsahu a kliknutí na tlačítko Přidat se v aplikaci Visual Studio zobrazí stejné dialogové okno pro výběr předlohy zobrazené na obrázku 6.

Nové deklarativní označení stránky default. aspx zahrnuje pouze direktivu @Page určující cestu k souboru hlavní stránky a ovládací prvek obsahu pro MainContent ContentPlaceHolder stránky předlohy.

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample2.aspx)]

Prozatím ponechejte default. aspx prázdnou. Později v tomto kurzu se vrátíme k přidání obsahu.

> [!NOTE]
> Naše stránka předlohy obsahuje oddíl nabídky nebo nějaké jiné navigační rozhraní. V budoucím kurzu vytvoříme takové rozhraní.

## <a name="step-2-enabling-forms-authentication"></a>Krok 2: Povolení ověřování formulářů

Při vytvoření webu ASP.NET je dalším úkolem povolit ověřování pomocí formulářů. Konfigurace ověřování aplikace je určena prostřednictvím [elementu`<authentication>`](https://msdn.microsoft.com/library/532aee0e.aspx) v souboru Web. config. Element `<authentication>` obsahuje jeden atribut s názvem Mode, který určuje model ověřování používaný aplikací. Tento atribut může mít jednu z následujících čtyř hodnot:

- **Windows** – jak je popsáno v předchozím kurzu, když aplikace používá ověřování systému Windows, je to zodpovědnost webového serveru za účelem ověření návštěvníka a obvykle se provádí prostřednictvím základního ověřování systému Windows, Digest nebo integrovaného ověřování systému Windows.
- **Formuláře**– uživatelé se ověřují prostřednictvím formuláře na webové stránce.
- **Passport**– uživatelé se ověřují pomocí sítě služby Passport společnosti Microsoft.
- **Žádné**– nepoužívá se žádný ověřovací model; Všichni návštěvníci jsou anonymní.

Ve výchozím nastavení používají aplikace ASP.NET ověřování systému Windows. Chcete-li změnit typ ověřování na ověřování typu Forms, je nutné upravit atribut mode elementu `<authentication>` na Forms.

Pokud projekt ještě neobsahuje soubor Web. config, přidejte jej nyní kliknutím pravým tlačítkem myši na název projektu v Průzkumník řešení, zvolíte příkaz Přidat novou položku a poté přidáte konfigurační soubor webu.

[![Pokud projekt ještě neobsahuje Web. config, přidejte ho teď](an-overview-of-forms-authentication-cs/_static/image16.png)](an-overview-of-forms-authentication-cs/_static/image15.png)

**Obrázek 7**: Pokud projekt ještě neobsahuje Web. config, přidejte ho hned ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-forms-authentication-cs/_static/image17.png)

Dále vyhledejte prvek `<authentication>` a aktualizujte ho, aby bylo možné používat ověřování pomocí formulářů. Po této změně by kód souboru Web. config měl vypadat nějak takto:

[!code-xml[Main](an-overview-of-forms-authentication-cs/samples/sample3.xml)]

> [!NOTE]
> Vzhledem k tomu, že web. config je soubor XML, je důležité velká a malá písmena. Ujistěte se, že jste nastavili atribut Mode na Forms s velkým písmenem "F". Pokud používáte jiná velká a malá písmena, například "Forms", obdržíte chybu konfigurace při návštěvě webu prostřednictvím prohlížeče.

Element `<authentication>` může volitelně zahrnovat `<forms>` podřízený prvek, který obsahuje nastavení specifická pro ověřování pomocí formulářů. Teď používáme jenom výchozí nastavení ověřování pomocí formulářů. V dalším kurzu budeme prozkoumat `<forms>` podřízený element podrobněji.

## <a name="step-3-building-the-login-page"></a>Krok 3: Sestavení přihlašovací stránky

Aby bylo možné podporovat ověřování pomocí formulářů, náš web potřebuje přihlašovací stránku. Jak je popsáno v části princip pracovního postupu pro ověřování pomocí formulářů, `FormsAuthenticationModule` automaticky přesměruje uživatele na přihlašovací stránku, pokud se pokusí získat přístup ke stránce, které nemají oprávnění k zobrazení. K dispozici jsou také ASP.NET webové ovládací prvky, které zobrazí odkaz na přihlašovací stránku pro anonymní uživatele. Tím begs otázku "Jaká je adresa URL přihlašovací stránky?"

Ve výchozím nastavení systém ověřování pomocí formulářů očekává, že přihlašovací stránka bude pojmenována Login. aspx a umístí se do kořenového adresáře webové aplikace. Pokud chcete použít jinou adresu URL přihlašovací stránky, můžete to udělat tak, že ji zadáte v souboru Web. config. V dalším kurzu se dozvíte, jak to udělat.

Přihlašovací stránka má tři zodpovědnosti:

1. Zadejte rozhraní, které návštěvníkovi umožňuje zadat své přihlašovací údaje.
2. Určete, jestli jsou odeslaná pověření platná.
3. Přihlaste se k uživateli vytvořením lístku pro ověřování pomocí formulářů.

### <a name="creating-the-login-pages-user-interface"></a>Vytvoření uživatelského rozhraní přihlašovací stránky

Pojďme začít s prvním úkolem. Přidejte novou stránku ASP.NET do kořenového adresáře lokality s názvem Login. aspx a přidružte ji k hlavní stránce site. Master.

[![přidat novou stránku ASP.NET s názvem Login. aspx](an-overview-of-forms-authentication-cs/_static/image19.png)](an-overview-of-forms-authentication-cs/_static/image18.png)

**Obrázek 8**: Přidejte novou stránku ASP.NET s názvem Login. aspx ([kliknutím zobrazíte obrázek v plné velikosti](an-overview-of-forms-authentication-cs/_static/image20.png)).

Typické rozhraní přihlašovací stránky se skládá ze dvou textových polí – jednu pro jméno uživatele, jednu pro heslo – a tlačítko pro odeslání formuláře. Websites často obsahují zaškrtávací políčko "zapamatovatelné", které pokud je zaškrtnuto, uchovává výsledný ověřovací lístek v rámci restartování prohlížeče.

Přidejte dvě textová pole do souboru Login. aspx a nastavte jejich `ID` vlastnosti na uživatelské jméno a heslo (v uvedeném pořadí). Nastavte také vlastnost `TextMode` hesla na heslo. Dále přidejte ovládací prvek CheckBox, nastavením jeho `ID` vlastností na RememberMe a jeho vlastnost `Text` na "zapamatování". Za tímto účelem přidejte tlačítko s názvem LoginButton, jehož vlastnost `Text` je nastavena na "login". A nakonec přidejte ovládací prvek web Label a nastavte jeho vlastnost `ID` na InvalidCredentialsMessage, jeho vlastnost `Text` na "uživatelské jméno nebo heslo je neplatné. Zkuste to prosím znovu. ", jeho vlastnost `ForeColor` na červenou a vlastnost `Visible` na false.

V tuto chvíli by vaše obrazovka měla vypadat podobně jako snímek obrazovky na obrázku 9 a deklarativní syntaxe stránky by měla vypadat takto:

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample4.aspx)]

[![přihlašovací stránka obsahuje dvě textová pole, zaškrtávací políčko, tlačítko a popisek.](an-overview-of-forms-authentication-cs/_static/image22.png)](an-overview-of-forms-authentication-cs/_static/image21.png)

**Obrázek 9**: Přihlašovací stránka obsahuje dvě textová pole, zaškrtávací políčko, tlačítko a popisek ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-forms-authentication-cs/_static/image23.png)

Nakonec vytvořte obslužnou rutinu události pro událost kliknutí LoginButton. V Návrháři stačí dvakrát kliknout na ovládací prvek tlačítko a vytvořit tuto obslužnou rutinu události.

### <a name="determining-if-the-supplied-credentials-are-valid"></a>Určení, zda jsou zadaná pověření platná

Nyní je nutné implementovat úlohu 2 v obslužné rutině události kliknutí na tlačítko – určete, zda jsou zadaná pověření platná. Aby to bylo možné, musí být úložiště uživatele, které obsahuje všechna pověření uživatelů, aby bylo možné určit, jestli zadané přihlašovací údaje odpovídají všem známým přihlašovacím údajům.

Před ASP.NET 2,0 byly vývojáři odpovědni za implementaci jejich vlastních uživatelských úložišť a psaní kódu pro ověření zadaných přihlašovacích údajů proti obchodu. Většina vývojářů implementuje úložiště uživatele v databázi a vytvoří tabulku s názvem uživatelé se sloupci, jako je uživatelské jméno, heslo, E-mail, LastLoginDate a tak dále. Tato tabulka bude mít jeden záznam na uživatelský účet. Ověření přihlašovacích údajů zadaných uživatelem by vyžadovalo dotazování databáze na odpovídající uživatelské jméno a pak zajisti, že heslo v databázi odpovídá zadanému heslu.

S ASP.NET 2,0 by měli vývojáři použít jednoho poskytovatele členství pro správu úložiště uživatelů. V této sérii kurzů budeme používat SqlMembershipProvider, který používá databázi SQL Server pro úložiště uživatele. Při použití SqlMembershipProvider musíme implementovat konkrétní schéma databáze, které zahrnuje tabulky, zobrazení a uložené procedury očekávané zprostředkovatelem. Podíváme se, jak toto schéma implementovat v rámci ***vytváření schématu členství v SQL Server*** kurzu. Se zprostředkovatelem členství na místě je ověření přihlašovacích údajů uživatele jednoduché jako volání [metody ValidateUser (*username*, *Password*)](https://msdn.microsoft.com/library/system.web.security.membership.validateuser.aspx) [třídy členství](https://msdn.microsoft.com/library/system.web.security.membership.aspx), která vrací logickou hodnotu označující, zda je kombinace *uživatelského jména* a *hesla* k displatnosti. Prohlížíme si, že ještě jsme neimplementovali úložiště uživatelů SqlMembershipProvider, ale v tuto chvíli nemůžeme použít metodu ValidateUser třídy členství.

Místo toho, abyste si vybrali vlastní tabulku databáze vlastní uživatelé (která by byla zastaralá, jakmile jsme implementovali SqlMembershipProvider), pojďme místo toho zadat platné přihlašovací údaje v rámci samotné přihlašovací stránky. Do obslužné rutiny události kliknutí na LoginButton přidejte následující kód:

[!code-csharp[Main](an-overview-of-forms-authentication-cs/samples/sample5.cs)]

Jak vidíte, existují tři platné uživatelské účty – Scott, Jisun a Sam – a všechny tři mají stejné heslo ("heslo"). Kód zachází pomocí polí uživatelé a hesla, kde se shodují platné uživatelské jméno a heslo. Pokud jsou uživatelské jméno i heslo platné, musíme uživatele přihlašovat a pak je přesměrovat na příslušnou stránku. Pokud pověření nejsou platná, zobrazí se popisek InvalidCredentialsMessage.

Když uživatel zadá platné přihlašovací údaje, uvedli jsme, že jsou pak přesměrováni na příslušnou stránku. Jakou stránku i to je vhodné? Odvolá se, když uživatel navštíví stránku, které nemají oprávnění k zobrazení, FormsAuthenticationModule je automaticky přesměruje na přihlašovací stránku. V takovém případě zahrnuje požadovanou adresu URL v řetězci QueryString prostřednictvím parametru ReturnUrl. To znamená, že pokud se uživatel pokusil navštívit ProtectedPage. aspx a že k tomu nebyli oprávněni, FormsAuthenticationModule je přesměruje na:

Login.aspx?ReturnUrl=ProtectedPage.aspx

Po úspěšném přihlášení by uživatel měl být přesměrován zpět na ProtectedPage. aspx. Případně můžou uživatelé navštívit přihlašovací stránku na vlastní Volition. V takovém případě se po přihlášení uživatele musí odeslat na stránku Default. aspx kořenové složky.

### <a name="logging-in-the-user"></a>Přihlášení uživatele

Za předpokladu, že zadané přihlašovací údaje jsou platné, musíme vytvořit lístek ověřování pomocí formulářů, a tím přihlašovat uživatele k webu. [Třída FormsAuthentication](https://msdn.microsoft.com/library/system.web.security.formsauthentication.aspx) v [oboru názvů System. Web. Security](https://msdn.microsoft.com/library/system.web.security.aspx) poskytuje metody pro přihlašování a odhlašování uživatelů prostřednictvím systému ověřování pomocí formulářů. I když existuje několik metod ve třídě FormsAuthentication, zajímá Vás tři tyto situaci:

- [GetAuthCookie (*username*, *persistCookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.getauthcookie.aspx) – vytvoří lístek pro ověřování pomocí formulářů pro zadané jméno *uživatele*. Dále tato metoda vytvoří a vrátí objekt HttpCookie, který obsahuje obsah ověřovacího lístku. Pokud má *persistCookie* hodnotu true, vytvoří se trvalý soubor cookie.
- [SetAuthCookie (*username*; *persistCookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.setauthcookie.aspx) – zavolá metodu GetAuthCookie (*username*, *persistCookie*), která vygeneruje soubor cookie pro ověřování formulářů. Tato metoda pak přidá soubor cookie vrácený GetAuthCookie do kolekce cookies (předpokládá se, že se používá ověřování pomocí formulářů založených na souborech cookie). jinak tato metoda volá interní třídu, která zpracovává logiku lístku bez souborů cookie).
- [RedirectFromLoginPage (*username*; *persistCookie*)](https://msdn.microsoft.com/library/system.web.security.formsauthentication.redirectfromloginpage.aspx) – Tato metoda volá SetAuthCookie (*username*, *persistCookie*) a pak přesměruje uživatele na příslušnou stránku.

GetAuthCookie je užitečné v případě, že před zápisem souboru cookie do kolekce souborů cookie potřebujete změnit ověřovací lístek. SetAuthCookie je užitečné, pokud chcete vytvořit ověřovací lístek pro formuláře a přidat ho do kolekce souborů cookie, ale nechcete uživatele přesměrovat na příslušnou stránku. Možná byste je chtěli ponechat na přihlašovací stránce nebo je odeslat na jinou stránku.

Vzhledem k tomu, že chceme uživatele přihlašovat a přesměrovat je na příslušnou stránku, použijte RedirectFromLoginPage. Aktualizujte obslužnou rutinu události kliknutí na LoginButton a nahraďte dva řádky TODO s komentářem následujícím řádkem kódu:

FormsAuthentication.RedirectFromLoginPage(UserName.Text, RememberMe.Checked);

Při vytváření lístku pro ověřování pomocí formulářů použijeme vlastnost text uživatelského jména pro parametr *username* lístku Forms pro ověřování a zaškrtnuté políčko RememberMe pro parametr *persistCookie* .

Přihlašovací stránku otestujete tak, že ji navštívíte v prohlížeči. Začněte zadáním neplatných přihlašovacích údajů, jako je například uživatelské jméno "ne" a heslo "nesprávného". Po kliknutí na tlačítko pro přihlášení dojde k postbacku a zobrazí se popisek InvalidCredentialsMessage.

[![popisek InvalidCredentialsMessage se zobrazí při zadání neplatných přihlašovacích údajů.](an-overview-of-forms-authentication-cs/_static/image25.png)](an-overview-of-forms-authentication-cs/_static/image24.png)

**Obrázek 10**: Popisek InvalidCredentialsMessage se zobrazí při zadání neplatných přihlašovacích údajů ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-forms-authentication-cs/_static/image26.png)

Potom zadejte platné přihlašovací údaje a klikněte na tlačítko pro přihlášení. Tentokrát dojde k tomu, že se vytvoří lístek pro ověřování pomocí formulářů a automaticky se přesměruje zpátky na Default. aspx. V tuto chvíli jste se přihlásili k webu, přestože neexistují žádná vizuální upozornění k tomu, abyste označili, že jste právě přihlášení. V kroku 4 se dozvíte, jak programově určit, jestli je uživatel přihlášený, a jak identifikovat uživatele, který stránku navštívil.

Krok 5 prověřuje techniky pro protokolování uživatele z webu.

### <a name="securing-the-login-page"></a>Zabezpečení přihlašovací stránky

Když uživatel zadá své přihlašovací údaje a odešle formulář přihlašovací stránky, přihlašovací údaje – včetně jejího hesla – budou přenášeny přes Internet na webový server v *prostém textu*. To znamená, že uživatelské jméno a heslo může sledovat jakýkoli počítačový podvodník, který bude sledovat síťový provoz. Aby k tomu nedocházelo, je nezbytné šifrovat síťový provoz pomocí [protokolu SSL (Secure Socket Layer)](http://en.wikipedia.org/wiki/Secure_Sockets_Layer). Tím se zajistí, že přihlašovací údaje (stejně jako kód HTML celé stránky) budou šifrovány od okamžiku, kdy prohlížeč opustí, dokud je webový server neobdrží.

Pokud váš web neobsahuje citlivé informace, budete na přihlašovací stránce potřebovat jenom SSL a na dalších stránkách, kde by se heslo uživatele jinak poslalo přes drát v prostém textu. Nemusíte se starat o zabezpečení lístku pro ověřování pomocí formulářů, protože ve výchozím nastavení je šifrovaný i digitálně podepsaný (aby se zabránilo manipulaci). Podrobnější diskuzi o zabezpečení lístku ověřování pomocí formulářů najdete v následujícím kurzu.

> [!NOTE]
> Mnohé finanční a lékařské weby jsou nakonfigurovány na používání protokolu SSL na *všech* stránkách přístupných pro ověřené uživatele. Pokud vytváříte takový web, můžete nakonfigurovat systém ověřování pomocí formulářů, aby se ověřovací lístek pro formuláře přenesl jenom přes zabezpečené připojení. V dalším kurzu se podíváme na různé možnosti konfigurace ověřování formulářů, *[konfiguraci ověřování formulářů a Pokročilá témata](forms-authentication-configuration-and-advanced-topics-cs.md)* .

## <a name="step-4-detecting-authenticated-visitors-and-determining-their-identity"></a>Krok 4: Zjišťování ověřených návštěvníků a určení jejich identity

V tuto chvíli jsme povolili ověřování pomocí formulářů a vytvořili přihlašovací stránku základní, ale ještě jsme prozkoumali, jak můžeme určit, jestli je uživatel ověřený nebo anonymní. V některých scénářích můžeme zobrazit různá data nebo informace v závislosti na tom, jestli se stránka zobrazuje na stránce ověřeného nebo anonymního uživatele. Kromě toho často potřebuje znát identitu ověřeného uživatele.

Pojďme rozrozšiřovat stávající stránku Default. aspx a tyto techniky ilustrovat. V části default. aspx přidejte dva ovládací prvky panelu, jednu s názvem AuthenticatedMessagePanel a další s názvem AnonymousMessagePanel. Do prvního panelu přidejte ovládací prvek popisek s názvem WelcomeBackMessage. Na druhém panelu přidejte ovládací prvek hypertextový odkaz, nastavte jeho vlastnost text na "přihlásit se" a jeho vlastnost NavigateUrl na ~/Login.aspx. V tomto okamžiku by deklarativní označení pro default. aspx mělo vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample6.aspx)]

Jak už jste to vyodhadli teď, tady je postup, jak zobrazit AuthenticatedMessagePanel jenom pro ověřené návštěvníky a jenom AnonymousMessagePanel pro anonymní návštěvníky. Abychom to dosáhli, je potřeba nastavit tyto viditelné vlastnosti panelů v závislosti na tom, jestli je uživatel přihlášený nebo ne.

[Vlastnost Request. neověřovaného](https://msdn.microsoft.com/library/system.web.httprequest.isauthenticated.aspx) vrátí logickou hodnotu, která označuje, zda byla žádost ověřena. Do stránky\_načíst kód obslužné rutiny události zadejte následující kód:

[!code-csharp[Main](an-overview-of-forms-authentication-cs/samples/sample7.cs)]

S tímto kódem přejděte na stránku Default. aspx přes prohlížeč. Za předpokladu, že jste se ještě přihlásili, se zobrazí odkaz na přihlašovací stránku (viz obrázek 11). Klikněte na tento odkaz a přihlaste se k webu. Jak jsme viděli v kroku 3, po zadání přihlašovacích údajů se vrátíte na Default. aspx, ale tentokrát na stránce se zobrazí zpráva "Vítejte zpátky!". zpráva (viz obrázek 12).

![Při anonymním navštívení se zobrazí odkaz Přihlásit se.](an-overview-of-forms-authentication-cs/_static/image27.png)

**Obrázek 11**: Při anonymním navštívení se zobrazí odkaz Přihlásit se.

![Ověření uživatelé se zobrazí](an-overview-of-forms-authentication-cs/_static/image28.png)

**Obrázek 12**: Ověřeným uživatelům se zobrazí zpráva "Vítejte zpátky!". Message

Identitu aktuálně přihlášeného uživatele můžeme určit prostřednictvím [Vlastnosti uživatele](https://msdn.microsoft.com/library/system.web.httpcontext.user.aspx) [HttpContext objektu](https://msdn.microsoft.com/library/system.web.httpcontext.aspx). Objekt HttpContext reprezentuje informace o aktuálním požadavku a je domovkou pro takové běžné ASP.NET objekty jako odpověď, požadavek a relace mimo jiné. Vlastnost User představuje kontext zabezpečení aktuální žádosti HTTP a implementuje [rozhraní IPrincipal](https://msdn.microsoft.com/library/system.security.principal.iprincipal.aspx).

Vlastnost User je nastavena vlastností FormsAuthenticationModule. Konkrétně Pokud FormsAuthenticationModule nalezne v příchozím požadavku lístek ověřování pomocí formulářů, vytvoří nový objekt GenericPrincipal a přiřadí ho k vlastnosti User.

Objekty zabezpečení (například GenericPrincipal) poskytují informace o identitě uživatele a rolích, ke kterým patří. Rozhraní IPrincipal definuje dva členy:

- [IsInRole (*roleName*)](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole.aspx) – metoda, která vrací logickou hodnotu udávající, zda objekt zabezpečení patří do zadané role.
- [Identity](https://msdn.microsoft.com/library/system.security.principal.iprincipal.identity.aspx) – vlastnost, která vrací objekt, který implementuje [rozhraní IIdentity](https://msdn.microsoft.com/library/system.security.principal.iidentity.aspx). Rozhraní IIdentity definuje tři vlastnosti: [AuthenticationType](https://msdn.microsoft.com/library/system.security.principal.iidentity.authenticationtype.aspx), [Neověřeno](https://msdn.microsoft.com/library/system.security.principal.iidentity.isauthenticated.aspx)a [název](https://msdn.microsoft.com/library/system.security.principal.iidentity.name.aspx).

Název aktuálního návštěvníka můžeme určit pomocí následujícího kódu:

String currentUsersName = User.Identity.Name;

Při použití ověřování pomocí formulářů se vytvoří [objekt FormsIdentity](https://msdn.microsoft.com/library/system.web.security.formsidentity.aspx) pro vlastnost identity GenericPrincipal. Třída FormsIdentity vždy vrátí řetězec "Forms" pro jeho vlastnost AuthenticationType a hodnotu true pro jeho vlastnost Authenticated. Vlastnost Name vrací uživatelské jméno zadané při vytváření ověřovacího lístku formulářů. Kromě těchto tří vlastností FormsIdentity zahrnuje přístup k základnímu ověřovacímu lístku prostřednictvím jeho [vlastnosti lístku](https://msdn.microsoft.com/library/system.web.security.formsidentity.ticket.aspx). Vlastnost lístku vrací objekt typu [FormsAuthenticationTicket](https://msdn.microsoft.com/library/system.web.security.formsauthenticationticket.aspx), který má vlastnosti, jako je například vypršení platnosti, trvalá, IssueDate, název a tak dále.

Důležitým bodem, který je třeba vzít tady, je, že parametr *username* zadaný v FormsAuthentication. GetAuthCookie (*username*, *PersistCookie*), FormsAuthentication. SetAuthCookie (*username*, *persistCookie*) a FormsAuthentication. RedirectFromLoginPage (*username*, *persistCookie*) je stejná hodnota vrácená User.identity.Name. Ověřovací lístek vytvořený těmito metodami je navíc k dispozici přetypování User. identity na objekt FormsIdentity a následným přístupem k vlastnosti lístku:

[!code-csharp[Main](an-overview-of-forms-authentication-cs/samples/sample8.cs)]

Pojďme na Default. aspx poskytnout přizpůsobenější zprávu. Aktualizujte obslužnou rutinu události stránky\_načíst, aby vlastnost text popisku WelcomeBackMessage přiřadila řetězec "Vítejte zpět, *username*!".

WelcomeBackMessage. text = "Vítejte zpět," + User.Identity.Name + "!";

Obrázek 13 znázorňuje účinek této úpravy (když se přihlašujete jako uživatel Scott).

![Uvítací zpráva obsahuje jméno aktuálně přihlášeného uživatele.](an-overview-of-forms-authentication-cs/_static/image29.png)

**Obrázek 13**: Uvítací zpráva obsahuje jméno aktuálně přihlášeného uživatele.

### <a name="using-the-loginview-and-loginname-controls"></a>Použití ovládacích prvků LoginView a LoginName

Běžným požadavkem je zobrazení jiného obsahu pro ověřené a anonymní uživatele. Takže se zobrazuje jméno aktuálně přihlášeného uživatele. Z tohoto důvodu zahrnuje ASP.NET dva webové ovládací prvky, které poskytují stejné funkce jako na obrázku 13, ale bez nutnosti napsat jediný řádek kódu.

[Ovládací prvek LoginView](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginview.aspx) je webový ovládací prvek založený na šabloně, který usnadňuje zobrazení různých dat ověřeným a anonymním uživatelům. LoginView obsahuje dvě předdefinované šablony:

- AnonymousTemplate – libovolný kód přidaný do této šablony se zobrazí pouze anonymním návštěvníkům.
- LoggedInTemplate – kód této šablony je zobrazen pouze ověřeným uživatelům.

Pojďme přidat ovládací prvek LoginView na stránku předlohy našeho webu site. Master. Namísto přidání pouze ovládacího prvku LoginView přidáváme jak nový ovládací prvek ContentPlaceHolder, tak ovládací prvek LoginView v rámci tohoto nového prvku ContentPlaceHolder. Odůvodnění tohoto rozhodnutí se brzy ukáže.

> [!NOTE]
> Kromě AnonymousTemplate a LoggedInTemplate může ovládací prvek LoginView zahrnovat šablony pro konkrétní role. Šablony specifické pro role zobrazují pouze označení uživatelům patřícím do zadané role. V budoucím kurzu prověříme funkce založené na rolích ovládacího prvku LoginView.

Začněte přidáním prvku ContentPlaceHolder s názvem LoginContent do stránky předlohy v navigačním &lt;elementu div&gt;. Můžete jednoduše přetáhnout ovládací prvek ContentPlaceHolder z panelu nástrojů do zobrazení zdroje a umístit výslednou značku přímo nad "TODO: Nabídka se zobrazí tady... textové.

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample9.aspx)]

Dále přidejte ovládací prvek LoginView do prvku LoginContent ContentPlaceHolder. Obsah umístěný do ovládacích prvků ContentPlaceHolder stránky předlohy se považuje za *výchozí obsah* prvku ContentPlaceHolder. To znamená, že stránky ASP.NET, které používají tuto stránku předlohy, mohou pro každý prvek ContentPlaceHolder zadat vlastní obsah nebo použít výchozí obsah stránky předlohy.

Prvek LoginView a jiné ovládací prvky související s přihlášením jsou umístěny na kartě Login (přihlášení) panelu nástrojů.

![Ovládací prvek LoginView v sadě nástrojů](an-overview-of-forms-authentication-cs/_static/image30.png)

**Obrázek 14**: Ovládací prvek LoginView v sadě nástrojů

Dále přidejte dva &lt;br/&gt; prvky ihned za ovládací prvek LoginView, ale ještě v prvku ContentPlaceHolder. V tuto chvíli by značky &lt;div&gt; elementu měly vypadat takto:

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample10.aspx)]

Šablony prvku LoginView lze definovat z návrháře nebo deklarativní značky. V návrháři aplikace Visual Studio rozbalte inteligentní značku LoginView, která obsahuje seznam nakonfigurovaných šablon v rozevíracím seznamu. Do AnonymousTemplate zadejte text "Hello, cizí". Dále přidejte ovládací prvek hypertextový odkaz a nastavte jeho text a vlastnosti NavigateUrl na "přihlásit se" a "~/login.aspx" v uvedeném pořadí.

Po nakonfigurování AnonymousTemplate přepněte na LoggedInTemplate a zadejte text "Vítejte zpátky". Pak přetáhněte ovládací prvek LoginName ze sady nástrojů na LoggedInTemplate a umístěte ho hned za text "Vítejte zpátky". [Ovládací prvek LoginName](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginname.aspx), jak má název, zobrazuje název aktuálně přihlášeného uživatele. Interně, ovládací prvek LoginName jednoduše vytvoří výstup vlastnosti User.Identity.Name.

Po provedení těchto dodatků do šablon ovládacího prvku LoginView by značky měly vypadat podobně jako následující:

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample11.aspx)]

S tímto přidáním na stránku hlavního serveru. Master se na každé stránce na našem webu zobrazí jiná zpráva v závislosti na tom, jestli je uživatel ověřený. Obrázek 15 ukazuje stránku Default. aspx při návštěvě prohlížeče uživatelem Jisun. Zpráva "Vítejte zpět, Jisun" se opakuje dvakrát: jednou v navigační oblasti hlavní stránky na levé straně (prostřednictvím ovládacího prvku LoginView, který jsme právě přidali), a jednou v oblasti obsahu default. aspx (přes ovládací prvky panelů a programová logika).

![Ovládací prvek LoginView zobrazuje](an-overview-of-forms-authentication-cs/_static/image31.png)

**Obrázek 15**: Ovládací prvek LoginView zobrazí "Vítejte zpět, Jisuno".

Vzhledem k tomu, že jsme přidali LoginView do stránky předlohy, může se objevit na každé stránce na našem webu. Mohou však být webové stránky, kde nechci zobrazit tuto zprávu. Takovou stránkou je přihlašovací stránka, protože odkaz na přihlašovací stránku se tam vykoná. Vzhledem k tomu, že jsme ovládací prvek LoginView umístili do prvku ContentPlaceHolder na stránce předlohy, můžeme tento výchozí kód přepsat na naší stránce obsahu. Otevřete Login. aspx a pokračujte v návrháři. Vzhledem k tomu, že jsme nedefinovali explicitně ovládací prvek obsahu v Login. aspx pro LoginContent ContentPlaceHolder na stránce předlohy, přihlašovací stránka zobrazí pro tento prvek ContentPlaceHolder výchozí označení stránky předlohy. Můžete to vidět prostřednictvím návrháře – LoginContent ContentPlaceHolder zobrazuje výchozí kód (ovládací prvek LoginView).

[![přihlašovací stránka zobrazuje výchozí obsah pro LoginContent ContentPlaceHolder stránky předlohy.](an-overview-of-forms-authentication-cs/_static/image33.png)](an-overview-of-forms-authentication-cs/_static/image32.png)

**Obrázek 16**: Přihlašovací stránka zobrazuje výchozí obsah pro LoginContent ContentPlaceHolder stránky předlohy ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-forms-authentication-cs/_static/image34.png)

Chcete-li přepsat výchozí označení pro LoginContent ContentPlaceHolder, jednoduše klikněte pravým tlačítkem myši na oblast v návrháři a v místní nabídce vyberte možnost vytvořit vlastní obsah. (Při použití sady Visual Studio 2008 obsahuje ovládací prvek ContentPlaceHolder inteligentní značku, která, pokud je vybrána, nabízí stejnou možnost.) Tím se do značek stránky přidá nový ovládací prvek obsahu, který nám umožní definovat vlastní obsah pro tuto stránku. Sem můžete přidat vlastní zprávu, jako je například "Přihlaste se...", ale nechte tuto položku prázdnou.

> [!NOTE]
> V aplikaci Visual Studio 2005 vytvoření vlastního obsahu vytvoří na stránce ASP.NET prázdný ovládací prvek obsahu. V aplikaci Visual Studio 2008 však vytváření vlastního obsahu kopíruje výchozí obsah stránky předlohy do nově vytvořeného ovládacího prvku obsahu. Pokud používáte Visual Studio 2008, potom po vytvoření nového ovládacího prvku obsahu nezapomeňte vymazat obsah zkopírovaný ze stránky předlohy.

Obrázek 17: po provedení této změny se v prohlížeči zobrazí stránka Login. aspx. Všimněte si, že při návštěvě default. aspx není v levé navigační &lt;zpráva "Hello, cizí" ani "Vítejte zpátky", *uživatelské jméno*.&gt;.

[![přihlašovací stránka skryje výchozí značku LoginContent ContentPlaceHolder.](an-overview-of-forms-authentication-cs/_static/image36.png)](an-overview-of-forms-authentication-cs/_static/image35.png)

**Obrázek 17**: Přihlašovací stránka skryje výchozí značku LoginContent ContentPlaceHolder ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-forms-authentication-cs/_static/image37.png)

## <a name="step-5-logging-out"></a>Krok 5: Odhlášení

V kroku 3 jsme se vyhledali na stránce vytvoření přihlašovací stránky pro přihlášení uživatele k webu, ale ještě jsme viděli, jak se uživatele odhlásili. Kromě metod pro protokolování uživatele v nástroji třída FormsAuthentication poskytuje také [metodu pro odhlášení](https://msdn.microsoft.com/library/system.web.security.formsauthentication.signout.aspx). Metoda odhlašování jednoduše zničí lístek ověřování formulářů, čímž uživatele odhlásí mimo lokalitu.

Odkaz na odhlášení je taková společná funkce, kterou ASP.NET obsahuje ovládací prvek specificky navržený pro odhlášení uživatele. [Ovládací prvek ovládací stavu přihlášení](https://msdn.microsoft.com/library/system.web.ui.webcontrols.loginstatus.aspx) zobrazí přihlašovací údaje LinkButton nebo "logout" LinkButton v závislosti na stavu ověřování uživatele. "Přihlašovací" LinkButton se vykreslí pro anonymní uživatele, zatímco "odhlašovací" odkaz se zobrazí ověřeným uživatelům. Text pro "login" a "odhlašovací" adresu je možné nakonfigurovat prostřednictvím vlastností LoginText a LogoutTextu ovládací stavu přihlášení.

Kliknutím na "přihlašování" přizpůsobíte postback, ze kterého je na přihlašovací stránce vystaveno přesměrování. Kliknutím na "odhlašovací" odkaz způsobí, že ovládací prvek ovládací stavu přihlášení vyvolá metodu FormsAuthentication. schvalování a pak přesměruje uživatele na stránku. Stránka odhlášeného uživatele se přesměruje na záviset na vlastnosti LogoutAction, která se dá přiřadit jedné ze tří následujících hodnot:

- Aktualizovat – výchozí nastavení; přesměruje uživatele na stránku, na kterou právě navštívili. Pokud stránka, na které jste právě navštívili, nepovoluje anonymní uživatele, bude FormsAuthenticationModule automaticky přesměrovat uživatele na přihlašovací stránku.

Je možné, že budete zajímá, proč se zde přesměrování provádí. Pokud uživatel chce zůstat na stejné stránce, proč nutnost explicitního přesměrování? Důvodem je, že když se klikne na odkaz "odhlásit", uživatel má stále lístek ověřování formulářů ve svých kolekcích souborů cookie. V důsledku toho je požadavek na postback ověřený požadavek. Ovládací prvek ovládací stavu přihlášení volá metodu odhlašování, ale k tomu dojde poté, co FormsAuthenticationModule uživatele ověřuje. Explicitní přesměrování proto způsobí, že prohlížeč tuto stránku znovu vyžádá. V době, kdy prohlížeč znovu požádá o stránku, byl odebrán lístek ověřování pomocí formulářů, a proto je příchozí požadavek anonymní.

- Přesměrování – uživatel je přesměrován na adresu URL určenou vlastností LogoutPageUrl ovládací stavu přihlášení.
- RedirectToLoginPage – uživatel je přesměrován na přihlašovací stránku.

Pojďme do stránky předlohy přidat ovládací prvek ovládací stavu přihlášení a nakonfigurovat ho tak, aby používal možnost přesměrování k odeslání uživatele na stránku, která zobrazuje zprávu potvrzující, že byla odhlášena. Začněte vytvořením stránky v kořenovém adresáři s názvem logout. aspx. Nezapomeňte tuto stránku přidružit k webu. Hlavní stránka předlohy. Dále zadejte zprávu do značky stránky vysvětlující uživateli, že se odhlásili.

Potom se vraťte na stránku předlohy site. Master a přidejte ovládací prvek ovládací stavu přihlášení pod prvek LoginView v LoginContent ContentPlaceHolder. Nastavte vlastnost LogoutAction ovládacího prvku ovládací stavu přihlášení na redirect a jeho vlastnost LogoutPageUrl na ~/logout.aspx.

[!code-aspx[Main](an-overview-of-forms-authentication-cs/samples/sample12.aspx)]

Vzhledem k tomu, že ovládací stavu přihlášení je mimo ovládací prvek LoginView, bude zobrazen pro anonymní i ověřené uživatele, ale to je v pořádku, protože ovládací stavu přihlášení správně zobrazuje "přihlašovací" nebo "odhlašovací" LinkButton. Při přidání ovládacího prvku ovládací stavu přihlášení je hypertextový odkaz "přihlásit" v AnonymousTemplate nadbytečný, takže ho odeberte.

Obrázek 18: při návštěvě Jisun se zobrazí default. aspx. Všimněte si, že v levém sloupci se zobrazí zpráva "Vítejte zpět, Jisun" spolu s odkazem pro odhlášení. Kliknutím na položku Odhlásit odkaz dojde k odeslání zpětného volání, odhlásí Jisun ze systému a poté přesměruje na odhlašovací. aspx. Jak ukazuje obrázek 19, v době, kdy se Jisun dostane k odhlášení. aspx, se již odhlásil a je proto anonymní. Proto v levém sloupci se zobrazí text "Vítejte, cizí" a odkaz na přihlašovací stránku.

[![default. aspx zobrazí](an-overview-of-forms-authentication-cs/_static/image39.png)](an-overview-of-forms-authentication-cs/_static/image38.png)

**Obrázek 18**: Default. aspx zobrazuje "Vítejte zpátky, Jisun" spolu s "odhlašovacím" odkazem ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-forms-authentication-cs/_static/image40.png)

[![se odhlašovací. aspx zobrazuje](an-overview-of-forms-authentication-cs/_static/image42.png)](an-overview-of-forms-authentication-cs/_static/image41.png)

**Obrázek 19**: Odhlašovací. aspx zobrazuje "Vítejte, cizí" spolu s "přihlašovacím" odkazem ([kliknutím zobrazíte obrázek v plné velikosti).](an-overview-of-forms-authentication-cs/_static/image43.png)

> [!NOTE]
> Doporučujeme, abyste si na stránce odhlašovací. aspx přizpůsobili, abyste skryli LoginContent ContentPlaceHolder (jako jsme to v kroku 4 pro Login. aspx). Důvodem je, že "přihlašovací" LinkButton vykreslený ovládacím prvkem ovládací stavu přihlášení (ten, který je pod "Hello, cizí") pošle uživateli přihlašovací stránku, která předá aktuální adresu URL v parametru QueryString ReturnUrl. Krátce, pokud uživatel, který se odhlásil, klikne na odkaz "přihlašování k ovládací stavu přihlášení" a pak se přihlásí, bude přesměrován zpět na logout. aspx, což by mohlo snadno Zaměňujte uživatele.

## <a name="summary"></a>Souhrn

V tomto kurzu jsme začali s přezkoumáním pracovního postupu ověřování pomocí formulářů a pak v aplikaci ASP.NET implementovat ověřování pomocí formulářů. Ověřování pomocí formulářů používá FormsAuthenticationModule, která má dvě zodpovědnosti: identifikace uživatelů na základě lístku pro ověřování pomocí formulářů a přesměrování neautorizovaných uživatelů na přihlašovací stránku.

Třída FormsAuthentication .NET Framework zahrnuje metody pro vytváření, kontrolu a odebírání lístků pro ověřování formulářů. Vlastnost Request. neověřovaného objektu a uživatele poskytuje další programovou podporu pro určení, zda je požadavek ověřený, a informace o identitě uživatele. K dispozici jsou také webové ovládací prvky LoginView, ovládací stavu přihlášení a LoginName, které vývojářům poskytují rychlý a bezplatný kód pro provádění mnoha běžných úloh souvisejících s přihlášením. Tyto a další webové ovládací prvky související s přihlašovacími údaji prověříme podrobněji v budoucích kurzech.

V tomto kurzu jsme získali přehled možností ověřování pomocí formulářů. Nepovedlo se prozkoumat možnosti konfigurace, podívejte se, jak lístky pro ověřování formulářů cookie fungují, nebo prozkoumat, jak ASP.NET chrání obsah ověřovacího lístku pro formuláře. V [dalším kurzu](forms-authentication-configuration-and-advanced-topics-cs.md)budeme diskutovat o těchto tématech a dalších.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Změny mezi službami IIS6 a IIS7 Security](https://www.iis.net/articles/view.aspx/IIS7/Managing-IIS7/Configuring-Security/Changes-between-IIS6-and-IIS7-Security)
- [Přihlašovací ovládací prvky ASP.NET](https://msdn.microsoft.com/library/d51ttbhx.aspx)
- [Professional ASP.NET 2,0 zabezpečení, členství a Správa rolí](http://www.wrox.com/WileyCDA/WroxTitle/productCd-0764596985.html) (ISBN: 978-0-7645-9698-8)
- [Element `<authentication>`](https://msdn.microsoft.com/library/532aee0e.aspx)
- [Element `<forms>` pro `<authentication>`](https://msdn.microsoft.com/library/1d3t3c61.aspx)

### <a name="video-training-on-topics-contained-in-this-tutorial"></a>Výukové video o tématech obsažených v tomto kurzu

- [Použití ověřování založeného na základních formulářích v ASP.NET](../../../videos/authentication/using-basic-forms-authentication-in-aspnet.md)

## <a name="about-the-author"></a>O autorovi

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml), autor 7 ASP/ASP. NET Books a zakladatel of [4GuysFromRolla.com](http://www.4guysfromrolla.com), pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je [*Sams naučit se ASP.NET 2,0 za 24 hodin*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco). Dá se získat na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com) nebo prostřednictvím svého blogu, který najdete na adrese [http://ScottOnWriting.NET](http://ScottOnWriting.NET).

## <a name="special-thanks-to"></a>Zvláštní díky...

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Vedoucí recenzent pro tento kurz byl tento kurz zkontrolován řadou užitečných revidujících. Kontroloři vedoucí pro tento kurz zahrnují Alicja Maziarz, John Suru a Teresa Murphy. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com.](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](security-basics-and-asp-net-support-cs.md)
> [Další](forms-authentication-configuration-and-advanced-topics-cs.md)

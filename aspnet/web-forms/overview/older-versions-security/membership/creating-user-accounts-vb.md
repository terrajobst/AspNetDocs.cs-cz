---
uid: web-forms/overview/older-versions-security/membership/creating-user-accounts-vb
title: Vytváření uživatelských účtů (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se podíváme na použití rozhraní členství (přes SqlMembershipProvider) k vytvoření nových uživatelských účtů. Uvidíme, jak vytvořit nové...
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 9ef3e893-bebe-4b13-9fe5-8b71720dd85e
msc.legacyurl: /web-forms/overview/older-versions-security/membership/creating-user-accounts-vb
msc.type: authoredcontent
ms.openlocfilehash: 01be198c329f372ddcd529ad8a369f2d3426a9fc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586819"
---
# <a name="creating-user-accounts-vb"></a>Vytváření uživatelských účtů (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_05_VB.zip) nebo [stažení PDF](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial05_CreatingUsers_vb.pdf)

> V tomto kurzu se podíváme na použití rozhraní členství (přes SqlMembershipProvider) k vytvoření nových uživatelských účtů. Uvidíme, jak vytvořit nové uživatele programově a prostřednictvím ASP. Zabudovaný ovládacím CreateUserWizard ovládací prvek sítě.

## <a name="introduction"></a>Úvod

<a id="_msoanchor_1"> </a>V [předchozím kurzu](creating-the-membership-schema-in-sql-server-vb.md) jsme nainstalovali schéma služby Application Services do databáze, která přidala tabulky, zobrazení a uložené procedury vyžadované `SqlMembershipProvider` a `SqlRoleProvider`. Tím se vytvoří infrastruktura, kterou budeme potřebovat pro zbývající kurzy v této sérii. V tomto kurzu se podíváme na použití rozhraní členství (prostřednictvím `SqlMembershipProvider`) k vytvoření nových uživatelských účtů. Uvidíme, jak vytvořit nové uživatele programově a prostřednictvím ASP. Zabudovaný ovládacím CreateUserWizard ovládací prvek sítě.

Kromě toho, jak se naučíte vytvářet nové uživatelské účty, budeme také muset aktualizovat ukázkový web, který jsme vytvořili poprvé v  *<a id="_msoanchor_2">[ ](../introduction/an-overview-of-forms-authentication-vb.md)</a>kurzu Přehled ověřování prostřednictvím formulářů* , a pak ho rozšířit v kurzu  *<a id="_msoanchor_3">[ ](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md)</a>konfigurace ověřování formulářů a Pokročilá témata* . Naše Ukázková webová aplikace má přihlašovací stránku, která ověřuje přihlašovací údaje uživatelů proti pevně zakódované dvojici uživatelského jména a hesla. Kromě toho `Global.asax` obsahuje kód, který vytváří vlastní `IPrincipal` a objekty `IIdentity` pro ověřené uživatele. Aktualizujeme přihlašovací stránku, aby ověřovala přihlašovací údaje uživatelů vůči rozhraní členství a odebrala vlastní objekt zabezpečení a logiku identity.

Pojďme začít!

## <a name="the-forms-authentication-and-membership-checklist"></a>Ověřování formulářů a kontrolní seznam členství

Než začneme s rozhraním pro členství začít pracovat, Podívejme se, abychom si prohlédli důležité kroky, které jsme provedli pro dosažení tohoto bodu. Při použití architektury členství v `SqlMembershipProvider` ve scénáři ověřování založeném na formulářích, je nutné provést následující kroky před implementací funkce členství ve webové aplikaci:

1. **Povolte ověřování pomocí formulářů.** Jak jsme probrali v  *<a id="_msoanchor_4">[ ](../introduction/an-overview-of-forms-authentication-vb.md)</a>přehledu ověřování pomocí formulářů*, ověřování pomocí formulářů je povolené úpravou `Web.config` a nastavením atributu `mode` elementu `<authentication>` na `Forms`. Když je povoleno ověřování pomocí formulářů, je každý příchozí požadavek prověřen pro *lístek ověřování pomocí formulářů*, který Pokud je přítomen, identifikuje žadatele.
2. **Přidejte schéma služby Application Services do příslušné databáze.** Při použití `SqlMembershipProvider` potřebujeme nainstalovat schéma služby Application Services do databáze. Toto schéma je obvykle přidáno do stejné databáze, která obsahuje datový model aplikace. *Vytvoření schématu členství v SQL Server kurzu, které jste prohlédli pomocí nástroje `aspnet_regsql.exe` k tomuto účelu. <a id="_msoanchor_5">[ ](creating-the-membership-schema-in-sql-server-vb.md)</a>*
3. **Upravte nastavení webové aplikace tak, aby odkazovalo na databázi z kroku 2.** *Vytvoření schématu členství v SQL Server* kurzu ukázalo dva způsoby, jak nakonfigurovat webovou aplikaci tak, aby `SqlMembershipProvider` používala databázi vybranou v kroku 2: úpravou `LocalSqlServer` název připojovacího řetězce; nebo přidáním nového registrovaného poskytovatele do seznamu zprostředkovatelů rozhraní pro členství a přizpůsobením tohoto nového poskytovatele pro použití databáze z kroku 2.

Při sestavování webové aplikace, která používá ověřování pomocí `SqlMembershipProvider` a formulářů, je nutné provést tyto tři kroky předtím, než použijete třídu `Membership` nebo webové ovládací prvky přihlášení ASP.NET. Vzhledem k tomu, že jsme už provedli tyto kroky v předchozích kurzech, jsme připraveni začít používat rámec členství.

## <a name="step-1-adding-new-aspnet-pages"></a>Krok 1: přidání nových stránek ASP.NET

V tomto kurzu a dalších třech prozkoumáme různé funkce a možnosti související s členstvím. K implementaci témat prověřených v rámci těchto kurzů budeme potřebovat řadu ASP.NET stránek. Pojďme vytvořit tyto stránky a potom soubor mapy webu `(Web.sitemap)`.

Začněte vytvořením nové složky v projektu s názvem `Membership`. Dále přidejte pět nových ASP.NET stránek do složky `Membership` a propojíte jednotlivé stránky pomocí `Site.master` stránky předlohy. Pojmenujte stránky:

- `CreatingUserAccounts.aspx`
- `UserBasedAuthorization.aspx`
- `EnhancedCreateUserWizard.aspx`
- `AdditionalUserInfo.aspx`
- `Guestbook.aspx`

V tomto okamžiku by Průzkumník řešení projektu vypadala podobně jako snímek obrazovky, který ukazuje obrázek 1.

[do složky členství bylo přidáno ![pět nových stránek.](creating-user-accounts-vb/_static/image2.png)](creating-user-accounts-vb/_static/image1.png)

**Obrázek 1**: do složky `Membership` bylo přidáno pět nových stránek ([kliknutím zobrazíte obrázek v plné velikosti).](creating-user-accounts-vb/_static/image3.png)

Každá stránka by měla v tomto okamžiku obsahovat dva ovládací prvky obsahu, jednu pro každý prvek prvků hlavní stránky: `MainContent` a `LoginContent`.

[!code-aspx[Main](creating-user-accounts-vb/samples/sample1.aspx)]

Odvolat, že výchozí kód `LoginContent` ContentPlaceHolder zobrazuje odkaz na přihlášení nebo odhlášení od webu v závislosti na tom, jestli je uživatel ověřený. Přítomnost ovládacího prvku `Content2` obsahu však přepisuje výchozí značku stránky předlohy. Jak jsme probrali v  *<a id="_msoanchor_6">[ ](../introduction/an-overview-of-forms-authentication-vb.md)</a>kurzu Přehled ověřování* založeného na formulářích, to je užitečné na stránkách, kde nechcete zobrazovat možnosti související s přihlášením v levém sloupci.

Pro tyto pět stran ale chceme pro `LoginContent` ContentPlaceHolder zobrazit výchozí označení stránky předlohy. Proto odeberte deklarativní označení pro ovládací prvek obsahu `Content2`. Po tom by každý z pěti značek stránky měl obsahovat pouze jeden ovládací prvek obsahu.

## <a name="step-2-creating-the-site-map"></a>Krok 2: vytvoření mapy webu

Všechny kromě triviálních webů potřebují implementovat nějaký formulář pro navigační uživatelské rozhraní. Navigační uživatelské rozhraní může být jednoduchý seznam odkazů na různé části webu. Alternativně mohou být tyto odkazy uspořádány do nabídek nebo zobrazení stromové struktury. Jako vývojáři stránky tvoří navigační uživatelské rozhraní pouze polovinu tohoto článku. Pro definování logických struktur webu potřebujeme taky nějaký způsob, který lze udržovat udržovatelně a aktualizovatelný způsobem. Když se přidají nové stránky nebo odeberou stávající stránky, chceme mít schopnost aktualizovat jeden zdroj – mapu webu a tyto změny se projeví v navigačním uživatelském rozhraní lokality.

Tyto dvě úlohy – definice mapy lokality a implementace navigačního uživatelského rozhraní založeného na mapě webu – lze snadno dosáhnout díky rozhraní mapy webu a webovým ovládacím prvkům navigace přidaným v ASP.NET verze 2,0. Rozhraní mapy webu umožňuje vývojářům definovat mapu webu a následně k nim přistupovat prostřednictvím programového rozhraní API ( [`SiteMap` třídy](https://msdn.microsoft.com/library/system.web.sitemap.aspx)). Vestavěné navigační webové ovládací prvky obsahují [ovládací prvek nabídky](https://msdn.microsoft.com/library/bz09dy46.aspx), [ovládací prvek TreeView](https://msdn.microsoft.com/library/3eafky27.aspx)a [ovládací prvek SiteMapPath](https://msdn.microsoft.com/library/3eafky27.aspx).

Podobně jako v případě členství a rolí jsou rozhraní mapy webu sestavena základem [modelem poskytovatele](http://aspnet.4guysfromrolla.com/articles/101905-1.aspx). Úkolem třídy poskytovatele mapy webu je vygenerovat strukturu v paměti, kterou používá `SiteMap` třídy z trvalého úložiště dat, jako je například soubor XML nebo databázová tabulka. .NET Framework se dodává s výchozím poskytovatelem mapy webu, který čte data mapy webu ze souboru XML ([`XmlSiteMapProvider`](https://msdn.microsoft.com/library/system.web.xmlsitemapprovider.aspx)) a toto je zprostředkovatel, který v tomto kurzu použijeme. U některých alternativních implementací poskytovatele mapy webu najdete další části věnované čtení na konci tohoto kurzu.

Výchozí zprostředkovatel mapy webu očekává v kořenovém adresáři správně formátovaný soubor XML s názvem `Web.sitemap`. Vzhledem k tomu, že používáme tohoto výchozího zprostředkovatele, musíme tento soubor přidat a definovat strukturu mapy webu v příslušném formátu XML. Chcete-li přidat soubor, klikněte pravým tlačítkem myši na název projektu v Průzkumník řešení a vyberte možnost Přidat novou položku. Z dialogového okna se můžete rozhodnout přidat soubor typu mapa webu s názvem `Web.sitemap`.

[![přidat soubor s názvem Web. sitemap do kořenového adresáře projektu](creating-user-accounts-vb/_static/image5.png)](creating-user-accounts-vb/_static/image4.png)

**Obrázek 2**: přidejte soubor s názvem `Web.sitemap` do kořenového adresáře projektu ([kliknutím zobrazíte obrázek v plné velikosti).](creating-user-accounts-vb/_static/image6.png)

Soubor mapování webu XML definuje strukturu webu jako hierarchii. Tento hierarchický vztah je modelován v souboru XML pomocí původ prvků `<siteMapNode>`. `Web.sitemap` musí začínat `<siteMap>` nadřazeným uzlem, který má přesně jednu `<siteMapNode>` podřízenou položku. Tento element `<siteMapNode>` nejvyšší úrovně představuje kořen hierarchie a může mít libovolný počet podřízených uzlů. Každý prvek `<siteMapNode>` musí zahrnovat atribut `title` a může volitelně zahrnovat atributy `url` a `description`, a to mimo jiné. Každý neprázdný `url` atribut musí být jedinečný.

Do souboru `Web.sitemap` zadejte následující kód XML:

[!code-xml[Main](creating-user-accounts-vb/samples/sample2.xml)]

Výše uvedené označení mapy webu definuje hierarchii zobrazenou na obrázku 3.

[![mapa webu představuje hierarchickou navigační strukturu.](creating-user-accounts-vb/_static/image8.png)](creating-user-accounts-vb/_static/image7.png)

**Obrázek 3**: Mapa webu představuje hierarchickou navigační strukturu ([kliknutím zobrazíte obrázek v plné velikosti).](creating-user-accounts-vb/_static/image9.png)

## <a name="step-3-updating-the-master-page-to-include-a-navigational-user-interface"></a>Krok 3: aktualizace stránky předlohy tak, aby zahrnovala navigační uživatelské rozhraní

ASP.NET zahrnuje řadu webových ovládacích prvků souvisejících s navigací pro návrh uživatelského rozhraní. Mezi ně patří nabídka, TreeView a ovládací prvky SiteMapPath. Ovládací prvky menu a TreeView vykreslují strukturu mapy webu v nabídce nebo stromu, v uvedeném pořadí, zatímco SiteMapPath zobrazí popis cesty, který ukazuje navštívený aktuální uzel i jeho předchůdce. Data mapy webu mohou být svázána s jinými datovými ovládacími prvky dat pomocí ovládacího prvku SiteMapDataSource a lze k němu přistupovat programově prostřednictvím třídy `SiteMap`.

Vzhledem k tomu, že důkladná diskuze nad rámec architektury mapy webu a navigační ovládací prvky přesahují rozsah této série kurzů, nemusíte místo útraty vytvořit vlastní navigační rozhraní pro navigaci, které se používá v *[rámci práce s daty v řadě kurzů ASP.NET 2,0](../../data-access/index.md)* , která používá ovládací prvek Repeater k zobrazení seznamu odkazů s odrážkami, jak je znázorněno na obrázku 4.

### <a name="adding-a-two-level-list-of-links-in-the-left-column"></a>Přidání seznamu odkazů ze dvou úrovní do levého sloupce

Chcete-li vytvořit toto rozhraní, přidejte následující deklarativní označení do levého sloupce `Site.master` hlavní stránky, kde text TODO: nabídka bude pokračovat... v současné době se nachází.

[!code-aspx[Main](creating-user-accounts-vb/samples/sample3.aspx)]

Výše uvedený kód váže ovládací prvek Repeater s názvem `menu` k prvku SiteMapDataSource, který vrací hierarchii mapy webu definovanou v `Web.sitemap`. Vzhledem k tomu, že [vlastnost`ShowStartingNode`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sitemapdatasource.showstartingnode.aspx) ovládacího prvku SiteMapDataSource je nastavená na hodnotu false, začne vracet hierarchii mapy lokality počínaje podřízenými uzly domovského uzlu. Repeater zobrazí každý z těchto uzlů (v současné době pouze členství) v elementu `<li>`. Další vnitřní opakovač pak zobrazí podřízené objekty aktuálního uzlu ve vnořeném neuspořádaném seznamu.

Obrázek 4 znázorňuje Vykreslený výstup výše uvedeného kódu se strukturou mapy webu, kterou jsme vytvořili v kroku 2. Repeater vykresluje Vanilla neuspořádaný seznam značek. pro rozložení aesthetically-přitažlivé jsou odpovědni pravidla šablony kaskádových stylů definovaná v `Styles.css`. Podrobnější popis toho, jak výše uvedený kód funguje, najdete v kurzu [hlavní stránky a navigace na webu](https://asp.net/learn/data-access/tutorial-03-vb.aspx) .

[![se navigační uživatelské rozhraní vykresluje pomocí vnořených neuspořádaných seznamů.](creating-user-accounts-vb/_static/image11.png)](creating-user-accounts-vb/_static/image10.png)

**Obrázek 4**: navigační uživatelské rozhraní se vykresluje pomocí vnořených neuspořádaných seznamů ([kliknutím zobrazíte obrázek v plné velikosti).](creating-user-accounts-vb/_static/image12.png)

### <a name="adding-breadcrumb-navigation"></a>Přidávání navigace s popisem cesty

Kromě seznamu odkazů v levém sloupci máme také každou stránku, kde se zobrazí [Popis cesty](http://en.wikipedia.org/wiki/Breadcrumb_%28navigation%29). Navigace s popisem cesty je navigační prvek uživatelského rozhraní, který rychle zobrazuje uživatele na aktuální pozici v rámci hierarchie lokality. Ovládací prvek SiteMapPath používá rozhraní mapy webu k určení umístění aktuální stránky v mapě webu a následně zobrazí popis cesty na základě těchto informací.

Konkrétně přidejte `<span>` element do záhlaví `<div>` prvku hlavní stránky a nastavte nový atribut `class` elementu `<span>` na popis cesty. (Třída `Styles.css` obsahuje pravidlo pro třídu s popisem cesty.) Dále do tohoto nového prvku `<span>` přidejte SiteMapPath.

[!code-aspx[Main](creating-user-accounts-vb/samples/sample4.aspx)]

Obrázek 5 ukazuje výstup SiteMapPath při návštěvě `~/Membership/CreatingUserAccounts.aspx`.

[![zobrazení navigace zobrazuje aktuální stránku a její předchůdce v mapě webu](creating-user-accounts-vb/_static/image14.png)](creating-user-accounts-vb/_static/image13.png)

**Obrázek 5**: navigace s popisem cesty zobrazuje aktuální stránku a její předchůdce v mapě webu ([kliknutím zobrazíte obrázek v plné velikosti).](creating-user-accounts-vb/_static/image15.png)

## <a name="step-4-removing-the-custom-principal-and-identity-logic"></a>Krok 4: Odebrání vlastního objektu zabezpečení a logiky identity

V kurzu *Konfigurace ověřování a Pokročilá témata jsme zjistili, jak přidružit k ověřenému uživateli vlastní objekty zabezpečení a identity. <a id="_msoanchor_7">[ ](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md)</a>* Provedli jsme to vytvořením obslužné rutiny události v `Global.asax` pro událost `PostAuthenticateRequest` aplikace, která se aktivuje po ověření uživatele `FormsAuthenticationModule`. V této obslužné rutině události nahradili `GenericPrincipal` a objekty `FormsIdentity` přidané `FormsAuthenticationModule` s objekty `CustomPrincipal` a `CustomIdentity`, které jsme vytvořili v tomto kurzu.

Zatímco vlastní objekty zabezpečení a identity jsou užitečné v některých scénářích, ve většině případů jsou objekty `GenericPrincipal` a `FormsIdentity` dostatečné. V důsledku toho se domníváme, že by bylo vhodné se vrátit k výchozímu chování. Tuto změnu udělejte buď odebráním nebo zadáním komentáře obslužné rutiny události `PostAuthenticateRequest`, nebo odstraněním `Global.asax` souboru zcela.

> [!NOTE]
> Po odhlášení nebo odebrání kódu v `Global.asax`budete muset odkomentovat kód v `Default.aspx's` třídy kódu na pozadí, která přetypování `User.Identity` vlastnost na instanci `CustomIdentity`.

## <a name="step-5-programmatically-creating-a-new-user"></a>Krok 5: Programové vytvoření nového uživatele

Chcete-li vytvořit nový uživatelský účet prostřednictvím rozhraní členství, použijte [metodu`CreateUser`](https://msdn.microsoft.com/library/system.web.security.membership.createuser.aspx)třídy `Membership`. Tato metoda má vstupní parametry pro uživatelské jméno, heslo a další pole související s uživatelem. Při vyvolání IT deleguje vytvoření nového uživatelského účtu nakonfigurovanému zprostředkovateli členství a vrátí [objekt`MembershipUser`](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx) reprezentující právě vytvořený uživatelský účet.

Metoda `CreateUser` má čtyři přetížení, přičemž každý z nich přijímá jiný počet vstupních parametrů:

- [`CreateUser(username, password)`](https://msdn.microsoft.com/library/d8t4h2es.aspx)
- [`CreateUser(username, password, email)`](https://msdn.microsoft.com/library/t8yy6w3h.aspx)
- [`CreateUser(username, password, email, passwordQuestion, passwordAnswer, isApproved, MembershipCreateStatus)`](https://msdn.microsoft.com/library/82xx2e62.aspx)
- [`CreateUser(username, password, email, passwordQuestion, passwordAnswer, isApproved, providerUserKey, MembershipCreateStatus)`](https://msdn.microsoft.com/library/ms152012.aspx)

Tato čtyři přetížení se liší od množství shromažďovaných informací. První přetížení například vyžaduje pouze uživatelské jméno a heslo pro nový uživatelský účet, zatímco druhý z nich také vyžaduje e-mailovou adresu uživatele.

Tato přetížení existují, protože informace potřebné k vytvoření nového uživatelského účtu závisí na nastavení konfigurace poskytovatele členství. V kurzu  *<a id="_msoanchor_8">[ ](creating-the-membership-schema-in-sql-server-vb.md)</a>vytváření schématu členství v SQL Server* jsme prozkoumali určení nastavení konfigurace zprostředkovatele členství v `Web.config`. Tabulka 2 obsahuje úplný seznam nastavení konfigurace.

Toto nastavení konfigurace zprostředkovatele členství, které ovlivňuje `CreateUser` přetížení, je možné použít jako `requiresQuestionAndAnswer` nastavení. Pokud je `requiresQuestionAndAnswer` nastavená na `true` (výchozí nastavení), pak při vytváření nového uživatelského účtu musíte zadat bezpečnostní otázku a odpověď. Tyto informace se později použijí, pokud uživatel potřebuje resetovat nebo změnit heslo. Konkrétně v takovém případě se zobrazí bezpečnostní otázka a musí zadat správnou odpověď, aby bylo možné resetovat nebo změnit heslo. V důsledku toho, pokud je `requiresQuestionAndAnswer` nastavena na `true` pak volání jednoho z prvních dvou `CreateUser` přetížení má za následek výjimku, protože bezpečnostní otázka a odpověď chybí. Vzhledem k tomu, že je naše aplikace momentálně nakonfigurovaná tak, aby vyžadovala bezpečnostní otázku a odpověď, budeme při vytváření uživatelského kódu programově potřebovat jedno z těchto dvou přetížení.

K ilustraci pomocí `CreateUser` metody vytvoříme uživatelské rozhraní, ve kterém se uživateli zobrazí výzva k zadání jména, hesla, e-mailu a odpovědi na předem definovanou bezpečnostní otázku. Ve složce `Membership` otevřete stránku `CreatingUserAccounts.aspx` a přidejte do ovládacího prvku obsahu následující webové ovládací prvky:

- Textové pole s názvem `Username`
- Textové pole s názvem `Password`, jehož vlastnost `TextMode` je nastavena na `Password`
- Textové pole s názvem `Email`
- Popisek s názvem `SecurityQuestion` s jeho vlastností `Text` se vymazal.
- Textové pole s názvem `SecurityAnswer`
- Tlačítko s názvem `CreateAccountButton`, jehož vlastnost `Text` je nastavena na vytvoření uživatelského účtu
- Ovládací prvek popisek s názvem `CreateAccountResults` s jeho vlastností `Text` vymazal.

V tuto chvíli by vaše obrazovka měla vypadat podobně jako snímek obrazovky, který je znázorněn na obrázku 6.

[![přidat různé webové ovládací prvky na stránku CreatingUserAccounts. aspx](creating-user-accounts-vb/_static/image17.png)](creating-user-accounts-vb/_static/image16.png)

**Obrázek 6**: přidejte do `CreatingUserAccounts.aspx Page` různé webové ovládací prvky ([kliknutím zobrazíte obrázek v plné velikosti](creating-user-accounts-vb/_static/image18.png)).

Popisek `SecurityQuestion` a textové pole `SecurityAnswer` mají za cíl zobrazit předem definovanou bezpečnostní otázku a shromažďovat odpověď uživatele. Všimněte si, že bezpečnostní otázka a odpověď jsou uloženy na základě uživatele, takže je možné umožnit každému uživateli definovat vlastní bezpečnostní otázku. V tomto příkladu se ale rozhodli použít univerzální bezpečnostní otázku, konkrétně: co je vaše oblíbená barva?

Chcete-li implementovat tuto předem definovanou bezpečnostní otázku, přidejte konstantu do třídy kódu na pozadí stránky s názvem `passwordQuestion`a přiřaďte jí bezpečnostní otázku. Potom v obslužné rutině události `Page_Load` přiřaďte tuto konstantu k vlastnosti `Text` popisku `SecurityQuestion`:

[!code-vb[Main](creating-user-accounts-vb/samples/sample5.vb)]

Dále vytvořte obslužnou rutinu události pro událost `Click` `CreateAccountButton'` s a přidejte následující kód:

[!code-vb[Main](creating-user-accounts-vb/samples/sample6.vb)]

Obslužná rutina události `Click` začíná definováním proměnné pojmenované `createStatus` typu [`MembershipCreateStatus`](https://msdn.microsoft.com/library/system.web.security.membershipcreatestatus.aspx). `MembershipCreateStatus` je výčet, který označuje stav operace `CreateUser`. Například pokud je uživatelský účet úspěšně vytvořen, bude výsledná `MembershipCreateStatus` instance nastavena na hodnotu `Success;` na druhé straně, pokud operace selže, protože již existuje uživatel se stejným uživatelským jménem, bude nastaven na hodnotu `DuplicateUserName`. V `CreateUser` přetížení potřebujeme předat instanci `MembershipCreateStatus` do metody. Tento parametr je nastaven na odpovídající hodnotu v rámci metody `CreateUser` a můžeme zjistit jeho hodnotu po volání metody, abyste zjistili, zda byl uživatelský účet úspěšně vytvořen.

Po volání `CreateUser`, který se předává do `createStatus`, se pro výstup příslušné zprávy v závislosti na hodnotě přiřazené k `createStatus`používá příkaz `Select Case`. Obrázky 7 ukazují výstup nově úspěšně vytvořeného uživatele. Na obrázcích 8 a 9 se zobrazí výstup, když se uživatelský účet nevytvoří. Na obrázku 8 návštěvník zadal heslo s pěti písmeny, které nesplňuje požadavky na sílu hesla napsané v nastavení konfigurace poskytovatele členství. Na obrázku 9 se návštěvník pokouší vytvořit uživatelský účet s existujícím uživatelským jménem (ten vytvořený na obrázku 7).

[![se úspěšně vytvořil nový uživatelský účet.](creating-user-accounts-vb/_static/image20.png)](creating-user-accounts-vb/_static/image19.png)

**Obrázek 7**: byl úspěšně vytvořen nový uživatelský účet ([kliknutím zobrazíte obrázek v plné velikosti](creating-user-accounts-vb/_static/image21.png)).

[![uživatelský účet není vytvořen, protože zadané heslo je příliš slabé.](creating-user-accounts-vb/_static/image23.png)](creating-user-accounts-vb/_static/image22.png)

**Obrázek 8**: uživatelský účet není vytvořen, protože zadané heslo je příliš slabé ([kliknutím zobrazíte obrázek v plné velikosti).](creating-user-accounts-vb/_static/image24.png)

[![uživatelský účet není vytvořen, protože uživatelské jméno je již používáno.](creating-user-accounts-vb/_static/image26.png)](creating-user-accounts-vb/_static/image25.png)

**Obrázek 9**: uživatelský účet není vytvořen, protože uživatelské jméno je již používáno ([kliknutím zobrazíte obrázek v plné velikosti).](creating-user-accounts-vb/_static/image27.png)

> [!NOTE]
> Může se zajímat, jak určit úspěch nebo neúspěch při použití jednoho z prvních dvou přetížení metod `CreateUser`, ani z toho, který má parametr typu `MembershipCreateStatus`. Tyto první dvě přetížení vyvolávají [výjimku`MembershipCreateUserException`](https://msdn.microsoft.com/library/system.web.security.membershipcreateuserexception.aspx) v tváři selhání, která zahrnuje [vlastnost`StatusCode`](https://msdn.microsoft.com/library/system.web.security.membershipcreateuserexception.statuscode.aspx) typu `MembershipCreateStatus`.

Po vytvoření několika uživatelských účtů ověřte, že byly vytvořeny účty pomocí výpisu obsahu `aspnet_Users` a `aspnet_Membership` tabulek v databázi `SecurityTutorials.mdf`. Jak ukazuje obrázek 10, Přidali jsme dva uživatele prostřednictvím stránky `CreatingUserAccounts.aspx`: tito a Bruce.

[![v úložišti uživatelů členství jsou dva uživatelé: tito a Bruce](creating-user-accounts-vb/_static/image29.png)](creating-user-accounts-vb/_static/image28.png)

**Obrázek 10**: v úložišti uživatelů členství jsou dva uživatelé: tito a Bruce ([kliknutím zobrazíte obrázek v plné velikosti](creating-user-accounts-vb/_static/image30.png)).

I když úložiště uživatele členství teď obsahuje informace o účtu Bruce a tito, zatím jsme implementovali funkce, které umožní přihlašovat se k webu Bruce nebo tito. V současné době `Login.aspx` ověřuje přihlašovací údaje uživatele proti pevně zakódované sadě párů uživatelských jmen a hesel – *neověřuje zadané* přihlašovací údaje pro rozhraní členství. Nyní se zobrazí nové uživatelské účty v `aspnet_Users` a `aspnet_Membership` tabulky budou stačit. V dalším kurzu  *<a id="_msoanchor_9">[ ](validating-user-credentials-against-the-membership-user-store-vb.md)</a>ověříte přihlašovací údaje uživatele proti uživatelskému úložišti členství*, aktualizujeme přihlašovací stránku, aby se ověřilo v úložišti členství.

> [!NOTE]
> Pokud nevidíte žádné uživatele v databázi `SecurityTutorials.mdf`, může to být tím, že vaše webová aplikace používá výchozího poskytovatele členství, `AspNetSqlMembershipProvider`, který jako své uživatelské úložiště používá databázi `ASPNETDB.mdf`. Chcete-li zjistit, zda se jedná o problém, klikněte na tlačítko Aktualizovat v Průzkumník řešení. Pokud byla do složky `App_Data` přidána databáze s názvem `ASPNETDB.mdf`, jedná se o problém. Vraťte se ke kroku 4  *<a id="_msoanchor_10">[ ](creating-the-membership-schema-in-sql-server-vb.md)</a>v tématu vytvoření schématu členství v SQL Server* kurzu, kde najdete pokyny, jak správně nakonfigurovat poskytovatele členství.

Ve většině scénářů vytváření uživatelských účtů se návštěvník zobrazuje s nějakým rozhraním, které umožňuje zadat své uživatelské jméno, heslo, e-mail a další důležité informace. tím se vytvoří nový účet. V tomto kroku jsme se prohlédli vytvořením takového rozhraní a pak viděli, jak pomocí metody `Membership.CreateUser` programově přidat nový uživatelský účet na základě vstupů uživatele. Náš kód ale právě vytvořil nový uživatelský účet. Neprováděly se žádné následné akce, třeba přihlášení uživatele k webu v rámci právě vytvořeného uživatelského účtu nebo odeslání e-mailu s potvrzením uživateli. Tyto další kroky by vyžadovaly další kód v obslužné rutině události `Click` tlačítka.

ASP.NET se dodává s ovládacím prvkem ovládacím CreateUserWizard, který je navržený tak, aby zpracovával proces vytváření uživatelských účtů, vygenerování uživatelského rozhraní pro vytváření nových uživatelských účtů, vytvoření účtu v rámci členství v architektuře a provádění post-Account. úlohy vytváření, jako je například odeslání potvrzovacího e-mailu a přihlášení právě vytvořeného uživatele do lokality. Použití ovládacího prvku ovládacím CreateUserWizard je jednoduché jako přetahování ovládacího prvku ovládacím CreateUserWizard ze sady nástrojů na stránku a nastavení několika vlastností. Ve většině případů nemusíte psát jediný řádek kódu. Tento ovládací prvek Nifty si podrobněji prozkoumáme v kroku 6.

Pokud jsou nové uživatelské účty vytvořeny pouze pomocí typické webové stránky pro vytvoření účtu, je pravděpodobné, že někdy budete muset napsat kód, který používá metodu `CreateUser`, protože ovládací prvek ovládacím CreateUserWizard pravděpodobně bude vyhovovat vašim potřebám. Nicméně metoda `CreateUser` je užitečná ve scénářích, kdy potřebujete vysoce přizpůsobené uživatelské prostředí pro vytváření účtů nebo když potřebujete programově vytvořit nové uživatelské účty pomocí alternativního rozhraní. Můžete mít například stránku, která umožňuje uživateli odeslat soubor XML, který obsahuje informace o uživateli z jiné aplikace. Stránka může analyzovat obsah nahraného souboru XML a vytvořit nový účet pro každého uživatele reprezentovaného v XML voláním metody `CreateUser`.

## <a name="step-6-creating-a-new-user-with-the-createuserwizard-control"></a>Krok 6: vytvoření nového uživatele pomocí ovládacího prvku ovládacím CreateUserWizard

ASP.NET se dodává s řadou přihlašovacích webových ovládacích prvků. Tyto ovládací prvky pomáhají v mnoha běžných scénářích souvisejících s uživatelským účtem a přihlašovacími údaji. [Ovládací prvek ovládacím CreateUserWizard](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/createuserwizard.aspx) je jedním z těchto ovládacích prvků, který je navržen pro zobrazení uživatelského rozhraní pro přidání nového uživatelského účtu do architektury členství.

Stejně jako mnoho dalších webových ovládacích prvků souvisejících s přihlášením, lze ovládacím CreateUserWizard použít bez nutnosti psát jediný řádek kódu. Intuitivní poskytuje uživatelské rozhraní na základě nastavení konfigurace poskytovatele členství a interně volá metodu `CreateUser` `Membership` třídy poté, co uživatel zadá potřebné informace a klikne na tlačítko vytvořit uživatele. Ovládací prvek ovládacím CreateUserWizard je velice přizpůsobitelný. V různých fázích procesu vytváření účtů je hostitel událostí, které se aktivují. V případě potřeby můžeme vytvářet obslužné rutiny událostí pro vložení vlastní logiky do pracovního postupu vytváření účtů. Kromě toho je vzhled ovládacím CreateUserWizard velmi flexibilní. Existuje mnoho vlastností, které definují vzhled výchozího rozhraní. v případě potřeby lze ovládací prvek převést na šablonu nebo můžete přidat další kroky k registraci uživatele.

Pojďme se podívat na použití výchozího rozhraní a chování ovládacího prvku ovládacím CreateUserWizard. Podíváme se na to, jak přizpůsobit vzhled prostřednictvím vlastností a událostí ovládacího prvku.

### <a name="examining-the-createuserwizards-default-interface-and-behavior"></a>Prověřování výchozího rozhraní a chování ovládacím CreateUserWizard

Vraťte se na stránku `CreatingUserAccounts.aspx` ve složce `Membership`, přepněte do režimu návrhu nebo rozdělení a pak přidejte ovládací prvek ovládacím CreateUserWizard do horní části stránky. Ovládací prvek ovládacím CreateUserWizard je uložen v části ovládací prvky přihlášení sady nástrojů. Po přidání ovládacího prvku nastavte jeho vlastnost `ID` na hodnotu `RegisterUser`. Vzhledem k zobrazení snímku obrazovky na obrázku 11 ovládacím CreateUserWizard vykreslí rozhraní s textovým polem pro uživatelské jméno, heslo, e-mailovou adresu a otázku a odpověď zabezpečení nového uživatele.

[![ovládacího prvku ovládacím CreateUserWizard vykreslí obecné uživatelské rozhraní pro vytvoření.](creating-user-accounts-vb/_static/image32.png)](creating-user-accounts-vb/_static/image31.png)

**Obrázek 11**: ovládací prvek ovládacím CreateUserWizard vykreslí obecné vytvoření uživatelského rozhraní ([kliknutím zobrazíte obrázek v plné velikosti).](creating-user-accounts-vb/_static/image33.png)

Pojďme chvíli porovnávat výchozí uživatelské rozhraní generované ovládacím prvkem ovládacím CreateUserWizard s rozhraním, které jsme vytvořili v kroku 5. Pro Starter umožňuje ovládacímu prvku ovládacím CreateUserWizard návštěvník zadat bezpečnostní otázku a odpověď, zatímco naše ručně vytvořené rozhraní používalo předem definovanou bezpečnostní otázku. Rozhraní ovládacího prvku ovládacím CreateUserWizard obsahuje také ověřovací ovládací prvky, zatímco jsme ještě v našem rozhraních pole formuláře implementovali ověřování. A rozhraní ovládacího prvku ovládacím CreateUserWizard obsahuje textové pole pro potvrzení hesla (spolu s CompareValidator, aby se zajistilo, že text zadaný v poli heslo a porovnání hesla je stejný).

Zajímavou je, že ovládací prvek ovládacím CreateUserWizard při vykreslování svého uživatelského rozhraní konzultuje nastavení konfigurace poskytovatele členství. Například pokud je `requiresQuestionAndAnswer` nastavena na hodnotu true, budou se zobrazovat pouze textová pole otázka zabezpečení a odpověď. Podobně ovládacím CreateUserWizard automaticky přidá ovládací prvek RegularExpressionValidator, aby se zajistilo splnění požadavků na sílu hesla, a nastaví jeho `ErrorMessage` a `ValidationExpression` vlastností na základě nastavení konfigurace `minRequiredPasswordLength`, `minRequiredNonalphanumericCharacters`a `passwordStrengthRegularExpression`.

Ovládací prvek ovládacím CreateUserWizard, jak má název, je odvozen od [ovládacího prvku Průvodce](https://msdn.microsoft.com/library/s2etd1ek.aspx). Ovládací prvky průvodce jsou navržené tak, aby poskytovaly rozhraní pro provádění úloh s více kroky. Ovládací prvek Průvodce může mít libovolný počet `WizardSteps`, z nichž každá představuje šablonu, která definuje HTML a webové ovládací prvky pro daný krok. V ovládacím prvku průvodce se zpočátku zobrazí první `WizardStep`společně s ovládacími prvky navigace, které uživateli umožňují pokračovat z jednoho kroku na další, nebo pro návrat k předchozím krokům.

Jak ukazuje deklarativní označení na obrázku 11, výchozí rozhraní ovládacího prvku ovládacím CreateUserWizard zahrnuje dva `WizardStep` s:

- [`CreateUserWizardStep`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizardstep.aspx) ? vykreslí rozhraní ke shromáždění informací pro vytvoření nového uživatelského účtu. Toto je krok znázorněný na obrázku 11.
- [`CompleteWizardStep`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.completewizardstep.aspx) ? vykreslí zprávu oznamující, že byl účet úspěšně vytvořen.

Vzhled a chování ovládacím CreateUserWizard můžete upravit tak, že některý z těchto kroků převedete na šablony nebo přidáte vlastní `WizardStep` s. Podíváme se na přidání `WizardStep` do registračního rozhraní v kurzu *ukládání dalších informací o uživateli* .

Pojďme se podívat na ovládací prvek ovládacím CreateUserWizard v akci. Navštivte stránku `CreatingUserAccounts.aspx` v prohlížeči. Začněte zadáním některých neplatných hodnot do rozhraní ovládacím CreateUserWizard. Zkuste zadat heslo, které nevyhovuje požadavkům na sílu hesla, nebo textové pole s uživatelským jménem nechte prázdné. V ovládacím CreateUserWizard se zobrazí příslušná chybová zpráva. Obrázek 12 ukazuje výstup při pokusu o vytvoření uživatele s nedostatečným silným heslem.

[![ovládacím CreateUserWizard automaticky vloží ovládací prvky ověřování.](creating-user-accounts-vb/_static/image35.png)](creating-user-accounts-vb/_static/image34.png)

**Obrázek 12**: ovládacím CreateUserWizard automaticky vloží ovládací prvky ověřování ([kliknutím zobrazíte obrázek v plné velikosti](creating-user-accounts-vb/_static/image36.png)).

V dalším kroku zadejte do ovládacím CreateUserWizard příslušné hodnoty a klikněte na tlačítko vytvořit uživatele. Za předpokladu, že jsou povinná pole Zadaná a síla hesla postačuje, vytvoří ovládacím CreateUserWizard nový uživatelský účet prostřednictvím architektury členství a pak zobrazí rozhraní `CompleteWizardStep`(viz obrázek 13). Na pozadí ovládacím CreateUserWizard volá metodu `Membership.CreateUser` stejným způsobem jako v kroku 5.

[![byl úspěšně vytvořen nový uživatelský účet.](creating-user-accounts-vb/_static/image38.png)](creating-user-accounts-vb/_static/image37.png)

**Obrázek 13**: byl vytvořen nový uživatelský účet ([kliknutím zobrazíte obrázek v plné velikosti](creating-user-accounts-vb/_static/image39.png)).

> [!NOTE]
> Jak ukazuje obrázek 13, rozhraní `CompleteWizardStep`obsahuje tlačítko pro pokračování. V tomto okamžiku, kdy na ni klikneme pouze k provedení postbacku, ale návštěvník na stejné stránce zůstane. V části Přizpůsobení vzhledu a chování ovládacím CreateUserWizard pomocí jeho části se podíváme na to, jak toto tlačítko umožňuje odeslat návštěvníka na `Default.aspx` (nebo na jinou stránku).

Po vytvoření nového uživatelského účtu se vraťte do sady Visual Studio a Projděte si tabulky `aspnet_Users` a `aspnet_Membership`, jako jsme na obrázku 10, abyste ověřili, že byl účet úspěšně vytvořen.

### <a name="customizing-the-createuserwizards-behavior-and-appearance-through-its-properties"></a>Přizpůsobení chování a vzhledu ovládacím CreateUserWizard prostřednictvím vlastností

Ovládacím CreateUserWizard je možné přizpůsobit různými způsoby, prostřednictvím vlastností, `WizardStep` s a obslužnými rutinami událostí. V této části se podíváme na to, jak přizpůsobit vzhled ovládacího prvku prostřednictvím jeho vlastností. v další části se podíváme na rozšíření chování ovládacího prvku prostřednictvím obslužných rutin událostí.

Prakticky všechen text zobrazený ve výchozím uživatelském rozhraní ovládacího prvku ovládacím CreateUserWizard se dá přizpůsobit pomocí jeho spoustu vlastností. Například uživatelské jméno, heslo, potvrzení hesla, E-mail, otázka zabezpečení a popisky odpovědí zabezpečení zobrazené nalevo od textových polí lze přizpůsobit pomocí [`UserNameLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.usernamelabeltext.aspx), [`PasswordLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.passwordlabeltext.aspx), [`ConfirmPasswordLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.confirmpasswordlabeltext.aspx), [`EmailLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.emaillabeltext.aspx), [`QuestionLabelText`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.questionlabeltext.aspx)a [`AnswerLabelText`ch](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.answerlabeltext.aspx) vlastností v uvedeném pořadí. Podobně existují vlastnosti pro určení textu pro tlačítka pro vytvoření uživatele a pokračování v `CreateUserWizardStep` a `CompleteWizardStep`, a také v případě, že jsou tato tlačítka vykreslena jako tlačítka, LinkButtons nebo ImageButtons.

Barvy, ohraničení, písma a další vizuální prvky lze konfigurovat prostřednictvím hostitele vlastností stylu. Vlastní ovládací prvek ovládacím CreateUserWizard má společné vlastnosti stylu webového ovládacího prvku – `BackColor`, `BorderStyle`, `CssClass`, `Font`a tak dále, a existuje mnoho vlastností stylu pro definování vzhledu pro konkrétní oddíly rozhraní ovládacím CreateUserWizard. [Vlastnost`TextBoxStyle`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.textboxstyle.aspx)například definuje styly pro textová pole v `CreateUserWizardStep`, zatímco [vlastnost`TitleTextStyle`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.titletextstyle.aspx) definuje styl nadpisu (Zaregistrujte si nový účet).

Kromě vlastností souvisejících s vzhledy existuje mnoho vlastností, které mají vliv na chování ovládacího prvku ovládacím CreateUserWizard. [Vlastnost`DisplayCancelButton`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.wizard.displaycancelbutton.aspx), pokud je nastavena na hodnotu true, zobrazuje tlačítko Storno vedle tlačítka pro vytvoření uživatele (výchozí hodnota je false). Pokud zobrazíte tlačítko zrušit, nezapomeňte také nastavit [vlastnost`CancelDestinationPageUrl`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx), která určuje stránku, na kterou se uživatel pošle po kliknutí na zrušit. Jak je uvedeno v předchozí části, tlačítko pokračovat v rozhraní `CompleteWizardStep`způsobí postback, ale návštěvníka zůstane na stejné stránce. Chcete-li poslat návštěvníka na jinou stránku po kliknutí na tlačítko pokračovat, stačí zadat adresu URL ve [vlastnosti`ContinueDestinationPageUrl`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx).

Pojďme aktualizovat ovládací prvek `RegisterUser` ovládacím CreateUserWizard a zobrazit tak tlačítko Storno a odeslat návštěvníka do `Default.aspx` při kliknutí na tlačítka pro zrušení nebo pokračování. Chcete-li to dosáhnout, nastavte vlastnost `DisplayCancelButton` na hodnotu true a vlastnosti `CancelDestinationPageUrl` a `ContinueDestinationPageUrl` na ~/Default.aspx. Obrázek 14 zobrazuje aktualizovaný ovládacím CreateUserWizard při prohlížení v prohlížeči.

[![vlastnost CreateUserWizardStep obsahuje tlačítko Storno.](creating-user-accounts-vb/_static/image41.png)](creating-user-accounts-vb/_static/image40.png)

**Obrázek 14**: `CreateUserWizardStep` obsahuje tlačítko Storno ([kliknutím zobrazíte obrázek v plné velikosti](creating-user-accounts-vb/_static/image42.png)).

Když návštěvník zadá uživatelské jméno, heslo, e-mailovou adresu a bezpečnostní otázku a odpověď a klikne na vytvořit uživatele, vytvoří se nový uživatelský účet a návštěvník se přihlásí jako nově vytvořený uživatel. Za předpokladu, že osoba, která navštíví stránku, vytváří nový účet pro sebe sama, bude to zřejmě požadovaným chováním. Můžete ale chtít správcům dovolit přidávat nové uživatelské účty. V takovém případě se vytvoří uživatelský účet, ale správce zůstane přihlášený jako správce (a ne jako nově vytvořený účet). Toto chování lze upravit pomocí [vlastnosti Boolean`LoginCreatedUser`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.logincreateduser.aspx).

Uživatelské účty v rámci systému členství obsahují příznak schválené; neschválení uživatelé se nemohou přihlásit k webu. Ve výchozím nastavení je nově vytvořený účet označený jako schválený a umožňuje uživateli, aby se k webu přihlásil hned. Je ale možné, že budou nové uživatelské účty označené jako neschválené. Možná budete chtít, aby správce ručně schválil nové uživatele předtím, než se může přihlásit. nebo možná budete chtít ověřit, jestli je e-mailová adresa zadaná v zápisu platná, než uživatel povolí přihlášení. Bez ohledu na to, že je to možné, můžete mít nově vytvořený uživatelský účet označený jako Neschválený nastavením [vlastnosti`DisableCreatedUser`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.disablecreateduser.aspx) ovládacího prvku ovládacím CreateUserWizard na hodnotu true (výchozí hodnota je false).

K dalším vlastnostem souvisejícím s chováním patří `AutoGeneratePassword` a `MailDefinition`. Je-li [vlastnost`AutoGeneratePassword`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.autogeneratepassword.aspx) nastavena na hodnotu true, v `CreateUserWizardStep` se nezobrazují pole heslo a potvrzení hesla; místo toho je automaticky vygenerováno heslo nově vytvořeného uživatele pomocí [metody`GeneratePassword`](https://msdn.microsoft.com/library/system.web.security.membership.generatepassword.aspx)`Membership` třídy. Metoda `GeneratePassword` sestaví heslo zadané délky a s dostatečným počtem nealfanumerických znaků pro splnění nakonfigurovaných požadavků na sílu hesla.

[Vlastnost`MailDefinition`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.maildefinition.aspx) je užitečná, pokud chcete odeslat e-mail na e-mailovou adresu zadanou během procesu vytváření účtu. Vlastnost `MailDefinition` zahrnuje řadu podvlastností pro definování informací o vytvořené e-mailové zprávě. Mezi tyto podvlastnosti patří možnosti jako `Subject`, `Priority`, `IsBodyHtml`, `From`, `CC`a `BodyFileName`. [Vlastnost`BodyFileName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.maildefinition.bodyfilename.aspx) odkazuje na text nebo soubor HTML, který obsahuje tělo e-mailové zprávy. Tělo podporuje dvě předem definované zástupné symboly: `<%UserName%>` a `<%Password%>`. Tyto zástupné symboly, pokud jsou k dispozici v souboru `BodyFileName`, budou nahrazeny jménem a heslem právě vytvořeného uživatele.

> [!NOTE]
> Vlastnost `MailDefinition` ovládacího prvku obsahuje pouze podrobnosti o e-mailové zprávě, která je odeslána při vytvoření nového účtu. `CreateUserWizard` Neobsahuje žádné podrobnosti o tom, jak je e-mailová zpráva odeslána (tj. zda se používá server SMTP nebo odesílající poštovní schránka, všechny informace o ověřování atd.). Tyto podrobnosti nízké úrovně musí být definovány v části `<system.net>` v `Web.config`. Další informace o těchto nastaveních konfigurace a o posílání e-mailů ze ASP.NET 2,0 najdete v tématu [Nejčastější dotazy na adrese SystemNetMail.com](http://www.systemnetmail.com/) a v článku o [posílání e-mailů v ASP.NET 2,0](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx).

### <a name="extending-the-createuserwizards-behavior-using-event-handlers"></a>Rozšíření chování ovládacím CreateUserWizard pomocí obslužných rutin událostí

Ovládací prvek ovládacím CreateUserWizard vyvolává během svého pracovního postupu několik událostí. Například když návštěvník zadá své uživatelské jméno, heslo a další relevantní informace a klikne na tlačítko vytvořit uživatele, ovládací prvek ovládacím CreateUserWizard vyvolá [událost`CreatingUser`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.creatinguser.aspx). Pokud během procesu vytváření dojde k problému, je vyvolána [událost`CreateUserError`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createusererror.aspx) ; Pokud je však uživatel úspěšně vytvořen, je vyvolána [událost`CreatedUser`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx) . K dispozici jsou další události ovládacího prvku ovládacím CreateUserWizard, které jsou vyvolány, ale jedná se o tři nejvíc německých.

V některých scénářích můžeme chtít klepnout do pracovního postupu ovládacím CreateUserWizard, který můžeme udělat vytvořením obslužné rutiny události pro příslušnou událost. Pro ilustraci si Vylepšete `RegisterUser` ovládací prvek ovládacím CreateUserWizard, aby zahrnoval nějaké vlastní ověření uživatelského jména a hesla. Konkrétně Vylepšete naše ovládacím CreateUserWizard, aby uživatelská jména neobsahovala mezery na začátku nebo na konci a uživatelské jméno se nemůže objevit kdekoli v hesle. V krátkém případě chceme uživatelům zabránit v vytváření uživatelského jména, jako je "Scott", nebo mít kombinaci uživatelského jména a hesla jako Scott a Scott. 1234.

K tomuto účelu vytvoříme obslužnou rutinu události pro událost `CreatingUser`, která provede dodatečné ověřovací kontroly. Pokud nejsou zadaná data platná, musíme proces vytváření zrušit. Pro zobrazení zprávy s vysvětlením, že uživatelské jméno nebo heslo je neplatné, musíme také na stránku přidat webový ovládací prvek popisek. Začněte přidáním ovládacího prvku popisek pod ovládacím prvkem ovládacím CreateUserWizard, nastavením jeho vlastnosti `ID` na `InvalidUserNameOrPasswordMessage` a jeho vlastnost `ForeColor` na `Red`. Vymažte vlastnost `Text` a nastavte její `EnableViewState` a `Visible` vlastnosti na false.

[!code-aspx[Main](creating-user-accounts-vb/samples/sample7.aspx)]

Dále vytvořte obslužnou rutinu události pro událost `CreatingUser` ovládacího prvku ovládacím CreateUserWizard. Chcete-li vytvořit obslužnou rutinu události, vyberte ovládací prvek v návrháři a pak přejít na okno Vlastnosti. Odtud klikněte na ikonu blesku a potom dvakrát klikněte na příslušnou událost a vytvořte obslužnou rutinu události.

Do obslužné rutiny události `CreatingUser` přidejte následující kód:

[!code-vb[Main](creating-user-accounts-vb/samples/sample8.vb)]

Všimněte si, že uživatelské jméno a heslo zadané do ovládacího prvku ovládacím CreateUserWizard jsou k dispozici prostřednictvím vlastností [`UserName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.username.aspx) a [`Password`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.password.aspx)v uvedeném pořadí. Tyto vlastnosti používáme ve výše uvedené obslužné rutině události k určení, jestli zadané uživatelské jméno obsahuje mezery na začátku nebo na konci a zda se uživatelské jméno nachází v hesle. Pokud je splněna jedna z těchto podmínek, zobrazí se chybová zpráva v popisku `InvalidUserNameOrPasswordMessage` a vlastnost `e.Cancel` obslužné rutiny události je nastavena na `True`. Pokud je `e.Cancel` nastavená na `True`, ovládacím CreateUserWizard krátkodobé okruhy svého pracovního postupu, což efektivně zruší proces vytváření uživatelských účtů.

Obrázek 15 znázorňuje snímek obrazovky `CreatingUserAccounts.aspx`, když uživatel zadá uživatelské jméno s úvodními mezerami.

[![uživatelská jména s počátečními nebo koncovými mezerami nejsou povolené.](creating-user-accounts-vb/_static/image44.png)](creating-user-accounts-vb/_static/image43.png)

**Obrázek 15**: uživatelská jména s úvodními nebo koncovými mezerami nejsou povolena ([kliknutím zobrazíte obrázek v plné velikosti).](creating-user-accounts-vb/_static/image45.png)

> [!NOTE]
> V kurzu  *<a id="_msoanchor_11">[ ](storing-additional-user-information-vb.md)</a>ukládání dalších informací o uživatelích* se zobrazí příklad použití události `CreatedUser` ovládacího prvku ovládacím CreateUserWizard.

## <a name="summary"></a>Souhrn

Metoda `CreateUser` třídy `Membership` vytvoří nový uživatelský účet v rámci rozhraní členství. Provede tak delegováním volání nakonfigurovanému zprostředkovateli členství. V případě `SqlMembershipProvider`přidá metoda `CreateUser` záznam do tabulek databáze `aspnet_Users` a `aspnet_Membership`.

Zatímco nové uživatelské účty je možné vytvářet programově (jak jsme viděli v kroku 5), je rychlejší a jednodušší přístup k použití ovládacího prvku ovládacím CreateUserWizard. Tento ovládací prvek vykreslí uživatelské rozhraní s více kroky pro shromažďování uživatelských informací a vytvoření nového uživatele v rámci systému členství. Pod sebou tento ovládací prvek používá stejnou metodu `Membership.CreateUser`, jak je vyhodnoceno v kroku 5, ale ovládací prvek vytvoří uživatelské rozhraní, ovládací prvky ověřování a reaguje na chyby při vytváření uživatelského účtu, aniž by musel psát Lick kódu.

V tuto chvíli máme funkci pro vytváření nových uživatelských účtů. Přihlašovací stránka se ale pořád ověřuje na základě pevně zakódovaných přihlašovacích údajů, které jsme zadali zpátky v druhém kurzu. <a id="_msoanchor_12"> </a>V [dalším kurzu](validating-user-credentials-against-the-membership-user-store-vb.md) aktualizujeme `Login.aspx`, aby se ověřilo zadání přihlašovacích údajů uživatele k rozhraní členství.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [`CreateUser` technickou dokumentaci](https://msdn.microsoft.com/library/system.web.security.membershipprovider.createuser.aspx)
- [Přehled ovládacího prvku ovládacím CreateUserWizard](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/login/createuserwizard.aspx)
- [Vytvoření poskytovatele mapy webu založeného na systému souborů](http://aspnet.4guysfromrolla.com/articles/020106-1.aspx)
- [Vytvoření podrobného uživatelského rozhraní pomocí ovládacího prvku Průvodce ASP.NET 2,0](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)
- [Prověřování navigace na webu ASP.NET 2.0](http://aspnet.4guysfromrolla.com/articles/111605-1.aspx)
- [Stránky předlohy a navigace na webu](https://asp.net/learn/data-access/tutorial-03-vb.aspx)
- [Poskytovatel mapy webu SQL, na který jste čekali](https://msdn.microsoft.com/msdnmag/issues/06/02/WickedCode/default.aspx)

### <a name="about-the-author"></a>O autorovi

Scott Mitchell, autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je *[Sams naučit se ASP.NET 2,0 za 24 hodin](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* . Scott se dá kontaktovat [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Teresa Murphy. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4guysfromrolla.com).

> [!div class="step-by-step"]
> [Předchozí](creating-the-membership-schema-in-sql-server-vb.md)
> [Další](validating-user-credentials-against-the-membership-user-store-vb.md)

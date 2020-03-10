---
uid: web-forms/overview/older-versions-security/roles/role-based-authorization-vb
title: Autorizace na základě rolí (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu se naučíte, jak Framework role přidruží role uživatele k jeho kontextu zabezpečení. Pak prověřuje, jak použít adresu URL založenou na rolích...
ms.author: riande
ms.date: 03/24/2008
ms.assetid: 83b4f5a4-4f5a-4380-ba33-f0b5c5ac6a75
msc.legacyurl: /web-forms/overview/older-versions-security/roles/role-based-authorization-vb
msc.type: authoredcontent
ms.openlocfilehash: feb3e5eb992284033853e67bfab3872243cefe39
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78573155"
---
# <a name="role-based-authorization-vb"></a>Ověřování založené na rolích (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/VB.11.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial11_RoleAuth_vb.pdf)

> V tomto kurzu se naučíte, jak Framework role přidruží role uživatele k jeho kontextu zabezpečení. Pak prověřuje, jak použít autorizační pravidla adresy URL na základě rolí. V tomto případě se podíváme na použití deklarativních a programových prostředků pro změnu zobrazených dat a funkcí nabízených stránkou ASP.NET.

## <a name="introduction"></a>Úvod

<a id="_msoanchor_1"> </a>V kurzu [*ověřování na základě uživatele*](../membership/user-based-authorization-vb.md) jsme zjistili, jak použít autorizaci URL k určení toho, co můžou uživatelé navštívit na konkrétní sadu stránek. V `Web.config`jenom trochu značek, můžeme dát pokyn ASP.NET, aby bylo možné navštívit stránku jenom ověřeným uživatelům. Nebo bychom mohli určit, že je povolený jenom uživatel tito a Bob, nebo jestli se povolili všichni ověření uživatelé s výjimkou Sam.

Kromě autorizace adresy URL jsme také vyhledali deklarativní a programové techniky pro řízení zobrazených dat a funkce nabízené stránkou na základě navštíveného uživatele. Konkrétně jsme vytvořili stránku, která uvádí obsah aktuálního adresáře. Kdokoli může navštívit tuto stránku, ale jenom ověření uživatelé můžou zobrazit obsah souborů a jenom tito může soubory odstranit.

Použití autorizačních pravidel pro uživatele podle uživatelů se může rozšířit do účetní Nightmare. Udržovatelnější přístup je použití autorizace na základě rolí. Dobrá zpráva je, že nástroje s naší likvidací pro použití autorizačních pravidel fungují stejně dobře i s rolemi tak, jak jsou k dispozici pro uživatelské účty. Autorizační pravidla URL můžou místo uživatelů určovat role. Ovládací prvek LoginView, který vykresluje různý výstup pro ověřené a anonymní uživatele, se dá nakonfigurovat tak, aby zobrazoval jiný obsah na základě rolí přihlášeného uživatele. A rozhraní API rolí obsahuje metody pro určení rolí přihlášeného uživatele.

V tomto kurzu se naučíte, jak Framework role přidruží role uživatele k jeho kontextu zabezpečení. Pak prověřuje, jak použít autorizační pravidla adresy URL na základě rolí. V tomto případě se podíváme na použití deklarativních a programových prostředků pro změnu zobrazených dat a funkcí nabízených stránkou ASP.NET. Pojďme začít!

## <a name="understanding-how-roles-are-associated-with-a-users-security-context"></a>Princip přidružení rolí k kontextu zabezpečení uživatele

Pokaždé, když požadavek vstoupí do kanálu ASP.NET, je přidružen k kontextu zabezpečení, který obsahuje informace identifikující žadatele. Při použití ověřování pomocí formulářů se jako token identity používá ověřovací lístek. Jak jsme probrali <a id="_msoanchor_2"> </a>v [*přehledu ověřování formulářů*](../introduction/an-overview-of-forms-authentication-vb.md) a <a id="_msoanchor_3"> </a> [*konfiguraci ověřování formulářů a pokročilých tématech*](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md) , `FormsAuthenticationModule` zodpovídá za určení totožnosti žadatele, kterou provede během [`AuthenticateRequest` události](https://msdn.microsoft.com/library/system.web.httpapplication.authenticaterequest.aspx).

Pokud je nalezen platný lístek ověřovacího lístku bez vypršení platnosti, `FormsAuthenticationModule` ho dekóduje, aby zjistil identitu žadatele. Vytvoří nový objekt `GenericPrincipal` a přiřadí ho k objektu `HttpContext.User`. Účelem objektu zabezpečení, jako je například `GenericPrincipal`, je identifikovat jméno ověřeného uživatele a jaké role patří do. Tento účel je zjevné faktem, že všechny objekty zabezpečení mají vlastnost `Identity` a metodu `IsInRole(roleName)`. `FormsAuthenticationModule`však nemá zájem o zaznamenávání informací o rolích a objekt `GenericPrincipal`, který vytváří, neurčuje žádné role.

Pokud je povolená architektura rolí, [`RoleManagerModule`](https://msdn.microsoft.com/library/system.web.security.rolemanagermodule.aspx) modul HTTP v části po `FormsAuthenticationModule` a identifikuje role ověřeného uživatele během [události`PostAuthenticateRequest`](https://msdn.microsoft.com/library/system.web.httpapplication.postauthenticaterequest.aspx), která se aktivuje po `AuthenticateRequest` události. Pokud je požadavek od ověřeného uživatele, `RoleManagerModule` přepíše objekt `GenericPrincipal` vytvořený `FormsAuthenticationModule` a nahradí jej [objektem`RolePrincipal`](https://msdn.microsoft.com/library/system.web.security.roleprincipal.aspx). Třída `RolePrincipal` používá rozhraní API rolí k určení rolí, do kterých uživatel patří.

Obrázek 1 znázorňuje pracovní postup kanálu ASP.NET při použití ověřování pomocí formulářů a architektury rolí. Nejprve se `FormsAuthenticationModule` spustí, identifikuje uživatele prostřednictvím ověřovacího lístku a vytvoří nový objekt `GenericPrincipal`. Dále `RoleManagerModule` kroky v a přepíší objekt `GenericPrincipal` s objektem `RolePrincipal`.

Pokud web navštíví anonymní uživatel, `FormsAuthenticationModule` ani `RoleManagerModule` nevytvoří objekt zabezpečení.

[![události kanálu ASP.NET pro ověřeného uživatele při použití ověřování pomocí formulářů a architektury rolí](role-based-authorization-vb/_static/image2.png)](role-based-authorization-vb/_static/image1.png)

**Obrázek 1**: ASP.NET kanálu události pro ověřeného uživatele při použití ověřování pomocí formulářů a architektury rolí ([kliknutím zobrazíte obrázek v plné velikosti](role-based-authorization-vb/_static/image3.png))

### <a name="caching-role-information-in-a-cookie"></a>Ukládání informací o rolích do mezipaměti v souboru cookie

Metoda `IsInRole(roleName)` objektu `RolePrincipal` volá `Roles`.`GetRolesForUser` pro získání rolí pro uživatele, aby bylo možné určit, zda je uživatel členem *roleName*. Při použití `SqlRoleProvider`je výsledkem dotaz na databázi úložiště rolí. Při použití autorizačních pravidel URL založené na rolích se metoda `IsInRole` `RolePrincipal`volá na každý požadavek na stránku, která je chráněná autorizačními pravidly URL založené na rolích. Místo toho, aby při každém požadavku vyhledána informace role v databázi, zahrnuje `Roles` Framework možnost ukládat do mezipaměti role uživatele v souboru cookie.

Pokud je architektura rolí nakonfigurovaná tak, aby do mezipaměti přestavila role uživatelů v souboru cookie, `RoleManagerModule` vytvoří soubor cookie během [`EndRequest` události](https://msdn.microsoft.com/library/system.web.httpapplication.endrequest.aspx)kanálu ASP.NET. Tento soubor cookie se používá v dalších žádostech v `PostAuthenticateRequest`, což je při vytvoření objektu `RolePrincipal`. Pokud je soubor cookie platný a nevypršela jeho platnost, data v souboru cookie budou analyzována a použita k naplnění rolí uživatele. tím se `RolePrincipal` tak, že se nemusíte zavolat do `Roles` třídy za účelem určení rolí uživatele. Obrázek 2 znázorňuje tento pracovní postup.

[![informací o roli uživatele může být uložen v souboru cookie za účelem zvýšení výkonu.](role-based-authorization-vb/_static/image5.png)](role-based-authorization-vb/_static/image4.png)

**Obrázek 2**: informace o roli uživatele mohou být uloženy v souboru cookie za účelem zvýšení výkonu ([kliknutím zobrazíte obrázek v plné velikosti).](role-based-authorization-vb/_static/image6.png)

Ve výchozím nastavení je mechanismus souborů cookie mezipaměti rolí zakázaný. Dá se povolit prostřednictvím `<roleManager>`; označení konfigurace v `Web.config`. Provedli jsme použití [prvku`<roleManager>`](https://msdn.microsoft.com/library/ms164660.aspx) k určení zprostředkovatelů rolí <a id="_msoanchor_4"> </a>v kurzu [*vytváření a Správa rolí*](creating-and-managing-roles-vb.md) , takže byste už měli mít tento prvek v souboru `Web.config` vaší aplikace. Nastavení souborů cookie pro mezipaměť rolí je zadáno jako atributy `<roleManager>`; a jsou shrnuty v tabulce 1.

> [!NOTE]
> Nastavení konfigurace uvedená v tabulce 1 určují vlastnosti výsledného souboru cookie mezipaměti rolí. Pokud chcete získat další informace o souborech cookie, jak fungují a jejich různé vlastnosti, přečtěte si [Tento kurz](http://www.quirksmode.org/js/cookies.html).

| <strong>Vlastnost</strong> |                                                                                                                                                                                                                                                                                                                                                         <strong>Popis</strong>                                                                                                                                                                                                                                                                                                                                                          |
|---------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   `cacheRolesInCookie`    |                                                                                                                                                                                                                                                                                                                              Logická hodnota, která označuje, zda je použito ukládání souborů cookie do mezipaměti. Výchozí hodnota je `false`.                                                                                                                                                                                                                                                                                                                              |
|       `cookieName`        |                                                                                                                                                                                                                                                                                                                                     Název souboru cookie mezipaměti role. Výchozí hodnota je ". ASPXROLES".                                                                                                                                                                                                                                                                                                                                     |
|       `cookiePath`        |                                                                                                                                                                                                                                Cesta k souboru cookie s názvem rolí Atribut path umožňuje vývojářům omezit rozsah souboru cookie na konkrétní hierarchii adresářů. Výchozí hodnota je "/", která informuje prohlížeč o odeslání souboru cookie ověřovacího lístku do jakékoli žádosti provedené v doméně.                                                                                                                                                                                                                                 |
|    `cookieProtection`     |                                                                                                                                                               Určuje, jaké techniky se používají k ochraně souborů cookie mezipaměti rolí. Povolené hodnoty jsou: `All` (výchozí); `Encryption`; `None`; a `Validation`. Další informace o těchto úrovních ochrany najdete <a id="_anchor_5"> </a>v kroku 3 v kurzu [*Konfigurace ověřování formulářů a Pokročilá témata*](../introduction/forms-authentication-configuration-and-advanced-topics-vb.md) .                                                                                                                                                                |
|    `cookieRequireSSL`     |                                                                                                                                                                                                                                                                                                   Logická hodnota určující, zda je pro přenos ověřovacího souboru cookie vyžadováno připojení SSL. Výchozí hodnota je `false`.                                                                                                                                                                                                                                                                                                   |
| `cookieSlidingExpiration` |                                                                                                                                                                                                                                                  Logická hodnota, která označuje, zda se má resetovat časový limit souboru cookie pokaždé, když uživatel navštíví web během jedné relace. Výchozí hodnota je `false`. Tato hodnota je relevantní pouze v případě, že je `createPersistentCookie` nastaveno na `true`.                                                                                                                                                                                                                                                  |
|      `cookieTimeout`      |                                                                                                                                                                                                                                                                         Určuje dobu v minutách, po jejímž uplynutí vyprší platnost souboru cookie ověřovacího lístku. Výchozí hodnota je `30`. Tato hodnota je relevantní pouze v případě, že je `createPersistentCookie` nastaveno na `true`.                                                                                                                                                                                                                                                                         |
| `createPersistentCookie`  |                                                                                                                                                                   Logická hodnota určující, zda je soubor cookie mezipaměti role souborem cookie relace nebo trvalým souborem cookie. Pokud `false` (výchozí), použije se soubor cookie relace, který se odstraní při zavření prohlížeče. Pokud `true`, použije se trvalý soubor cookie. vyprší `cookieTimeout` počet minut po jeho vytvoření nebo po předchozí návštěvě v závislosti na hodnotě `cookieSlidingExpiration`.                                                                                                                                                                    |
|         `domain`          |                                                                                                                                                 Určuje hodnotu domény souboru cookie. Výchozí hodnota je prázdný řetězec, který způsobí, že prohlížeč použije doménu, ze které byla vydána (například www.yourdomain.com). V takovém <strong>případě se soubory</strong> cookie neodesílají při vytváření požadavků na subdomény, jako je admin.yourdomain.com. Pokud chcete, aby byl soubor cookie předán všem poddoménám, které potřebujete k přizpůsobení atributu `domain`, nastavte jej na hodnotu "yourdomain.com".                                                                                                                                                 |
|    `maxCachedResults`     | Určuje maximální počet názvů rolí, které jsou uloženy v mezipaměti v souboru cookie. Výchozí hodnota je 25. `RoleManagerModule` nevytvoří soubor cookie pro uživatele, kteří patří do více než `maxCachedResults` rolí. V důsledku toho metoda `IsInRole` objektu `RolePrincipal` použije třídu `Roles` k určení rolí uživatele. Důvod `maxCachedResults` existuje, protože mnoho uživatelských agentů nepovoluje soubory cookie větší než 4 096 bajtů. Proto je tento limit určen ke snížení pravděpodobnosti překročení tohoto omezení velikosti. Pokud máte extrémně dlouhé názvy rolí, možná budete chtít zvážit zadání menší hodnoty `maxCachedResults`. contrariwise, pokud máte extrémně krátké názvy rolí, můžete tuto hodnotu pravděpodobně zvýšit. |

**Tabulka 1**: možnosti konfigurace souborů cookie mezipaměti rolí

Pojďme nakonfigurovat naši aplikaci tak, aby používala soubory cookie mezipaměti netrvalé role. K tomu je potřeba aktualizovat element `<roleManager>` v `Web.config` tak, aby zahrnoval následující atributy týkající se souborů cookie:

[!code-xml[Main](role-based-authorization-vb/samples/sample1.xml)]

Aktualizoval (a) `<roleManager>`; element přidáním tří atributů: `cacheRolesInCookie`, `createPersistentCookie`a `cookieProtection`. Když nastavíte `cacheRolesInCookie` na `true`, `RoleManagerModule` teď automaticky ukládat do mezipaměti role uživatele v souboru cookie, a nemusíte přitom vyhledávat informace o rolích uživatele u jednotlivých požadavků. Explicitně jsem nastavil `createPersistentCookie` a `cookieProtection` atributy na `false` a `All`, v uvedeném pořadí. Technicky, nemuseli byste pro tyto atributy zadat hodnoty, protože jsem je právě přiřadil jejich výchozím hodnotám, ale teď je umístili, aby se explicitně vymazalo, že nepoužívám trvalé soubory cookie a že soubor cookie je šifrovaný i ověřený.

A je to! V tomto případě bude rámec rolí ukládat do mezipaměti role uživatelů v souborech cookie. Pokud prohlížeč uživatele nepodporuje soubory cookie, nebo pokud jsou jeho soubory cookie odstraněny nebo ztraceny, nejedná se o velké obchodování – objekt `RolePrincipal` jednoduše použije třídu `Roles` v případě, že není k dispozici žádný soubor cookie (nebo neplatný nebo neplatnost).

> [!NOTE]
> Vzory &amp; postupů společnosti Microsoft nedoporučují použití souborů cookie trvalé mezipaměti rolí. Vzhledem k tomu, že držení souboru cookie mezipaměti rolí je dostatečné pro prokázání členství v roli, pokud hacker může nějakým způsobem získat přístup k souboru cookie platného uživatele, může tento uživatel zosobnit. Pravděpodobnost tohoto chování se zvyšuje, pokud je soubor cookie uložený v prohlížeči uživatele. Další informace o tomto doporučení zabezpečení a dalších potížích se zabezpečením najdete v [seznamu otázek zabezpečení pro ASP.NET 2,0](https://msdn.microsoft.com/library/ms998375.aspx).

## <a name="step-1-defining-role-based-url-authorization-rules"></a>Krok 1: definování autorizačních pravidel URL na základě rolí

Jak je popsáno v <a id="_msoanchor_6"> </a>kurzu [*ověřování na základě uživatele*](../membership/user-based-authorization-vb.md) , ověřování adres URL nabízí způsob, jak omezit přístup k sadě stránek na základě rolí uživatelů nebo rolí. Autorizační pravidla adresy URL jsou napsána v `Web.config` pomocí [elementu`<authorization>`](https://msdn.microsoft.com/library/8d82143t.aspx) s `<allow>` a podřízenými prvky `<deny>`. Kromě autorizačních pravidel souvisejících s uživatelem, které jsou popsány v předchozích kurzech, mohou jednotlivé `<allow>` a `<deny>` podřízeného prvku zahrnovat také:

- Konkrétní role
- Seznam rolí oddělených čárkami

Například autorizační pravidla URL udělují přístup těmto uživatelům v rolích správci a vedoucí, ale mají přístup ke všem ostatním:

[!code-xml[Main](role-based-authorization-vb/samples/sample2.xml)]

Element `<allow>` ve výše uvedeném kódu uvádí, že role správců a vedoucích jsou povoleny. `<deny>`; element instruuje, že *Všichni* uživatelé mají odepřený přístup.

Pojďme nakonfigurovat naši aplikaci tak, aby `ManageRoles.aspx`, `UsersAndRoles.aspx`a `CreateUserWizardWithRoles.aspx` stránky byly dostupné jenom pro tyto uživatele v roli Administrators, zatímco `RoleBasedAuthorization.aspx` stránka zůstane dostupná pro všechny návštěvníky.

Chcete-li to provést, Začněte přidáním souboru `Web.config` do složky `Roles`.

[![přidat soubor Web. config do adresáře role](role-based-authorization-vb/_static/image8.png)](role-based-authorization-vb/_static/image7.png)

**Obrázek 3**: přidání souboru `Web.config` do adresáře `Roles` ([kliknutím zobrazíte obrázek v plné velikosti](role-based-authorization-vb/_static/image9.png))

Dále přidejte následující kód konfigurace pro `Web.config`:

[!code-xml[Main](role-based-authorization-vb/samples/sample3.xml)]

Element `<authorization>` v části `<system.web>` označuje, že k prostředkům ASP.NET v adresáři `Roles` mají přístup pouze uživatelé v roli Administrators. Element `<location>` definuje alternativní sadu autorizačních pravidel URL pro stránku `RoleBasedAuthorization.aspx` a umožňuje všem uživatelům navštívit stránku.

Po uložení změn do `Web.config`se přihlaste jako uživatel, který není v roli správců, a pak zkuste navštívit jednu z chráněných stránek. `UrlAuthorizationModule` zjistí, že nemáte oprávnění k návštěvě požadovaného prostředku; v důsledku toho `FormsAuthenticationModule` vás přesměruje na přihlašovací stránku. Přihlašovací stránka vás pak přesměruje na stránku `UnauthorizedAccess.aspx` (viz obrázek 4). Toto konečné přesměrování ze stránky pro přihlášení k `UnauthorizedAccess.aspx` dojde z důvodu kódu, který jsme přidali na přihlašovací stránku v kroku 2 <a id="_msoanchor_7"> </a>kurzu [*ověřování na základě uživatele*](../membership/user-based-authorization-vb.md) . Konkrétně přihlašovací stránka automaticky přesměruje všechny ověřené uživatele na `UnauthorizedAccess.aspx`, pokud řetězec QueryString obsahuje parametr `ReturnUrl`, protože tento parametr označuje, že se uživatel dostal na přihlašovací stránku po pokusu o zobrazení stránky, kterou nemá oprávnění k zobrazení.

[Jenom ![můžou chráněné stránky zobrazit jenom uživatelé v roli správců.](role-based-authorization-vb/_static/image11.png)](role-based-authorization-vb/_static/image10.png)

**Obrázek 4**: chráněné stránky můžou zobrazit jenom uživatelé v roli správců ([kliknutím zobrazíte obrázek v plné velikosti](role-based-authorization-vb/_static/image12.png)).

Odhlaste se a pak se přihlaste jako uživatel, který se nachází v roli správců. Nyní byste měli být schopni zobrazit tři chráněné stránky.

[![tito může navštívit stránku UsersAndRoles. aspx, protože je v roli správců.](role-based-authorization-vb/_static/image14.png)](role-based-authorization-vb/_static/image13.png)

**Obrázek 5**: tito může navštívit stránku `UsersAndRoles.aspx`, protože je v roli správců ([kliknutím zobrazíte obrázek v plné velikosti).](role-based-authorization-vb/_static/image15.png)

> [!NOTE]
> Při určování autorizačních pravidel URL – pro role nebo uživatele – je důležité mít na paměti, že pravidla se analyzují postupně shora dolů. Jakmile je nalezena shoda, uživateli je udělen nebo odepřen přístup v závislosti na tom, zda byla shoda nalezena v prvku `<allow>` nebo `<deny>`. **Pokud není nalezena žádná shoda, uživateli je udělen přístup.** Proto pokud chcete omezit přístup k jednomu nebo více uživatelským účtům, je nutné použít `<deny>` prvek jako poslední prvek v konfiguraci autorizace adresy URL. **Pokud vaše autorizační pravidla URL neobsahují** element`<deny>` **, udělí se přístup všichni uživatelé.** Důkladnější diskuzi o tom, jak se pravidla autorizace adresy URL analyzují, najdete v části o tom, jak `UrlAuthorizationModule` používá autorizační pravidla pro udělení nebo zamítnutí přístupu v <a id="_msoanchor_8"> </a>kurzu [*ověřování na základě uživatele*](../membership/user-based-authorization-vb.md) .

## <a name="step-2-limiting-functionality-based-on-the-currently-logged-in-users-roles"></a>Krok 2: omezení funkčnosti na základě rolí aktuálně přihlášeného uživatele

Autorizace adres URL usnadňuje zadání hrubých autorizačních pravidel, která určují, jaké identity jsou povolené a které jsou odepřené zobrazení konkrétní stránky (nebo všech stránek ve složce a jejích podsložkách). V některých případech ale můžeme chtít, aby všichni uživatelé navštívili stránku, ale omezili funkčnost této stránky na základě rolí návštěvníků daného uživatele. To může vést k tomu, že se data budou zobrazovat nebo skrývat na základě role uživatele nebo nabízí další funkce uživatelům, kteří patří do určité role.

Tato jemně zrnitá autorizační pravidla založená na rolích je možné implementovat deklarativně nebo programově (nebo prostřednictvím některé kombinace dvou). V další části se dozvíte, jak implementovat deklarativní ověřování zrnitosti prostřednictvím ovládacího prvku LoginView. Podle toho budeme zkoumat programové techniky. Než se budeme moct podívat na použití jemných autorizačních pravidel, nejdřív musíme vytvořit stránku, jejíž funkce závisí na roli uživatele, na které se uživatel navštíví.

Pojďme vytvořit stránku, která zobrazí seznam všech uživatelských účtů v systému v prvku GridView. Prvek GridView bude obsahovat uživatelské jméno, e-mailovou adresu, datum posledního přihlášení a komentáře k uživateli. Kromě zobrazování informací o jednotlivých uživatelích bude prvek GridView obsahovat možnosti úprav a odstranění. Zpočátku tuto stránku vytvoříme s funkcemi Upravit a odstranit dostupnými pro všechny uživatele. V částech "použití ovládacího prvku LoginView" a "programové omezení funkčnosti" se dozvíte, jak povolit nebo zakázat tyto funkce na základě role navštíveného uživatele.

> [!NOTE]
> ASP.NET stránka pro sestavení používá ovládací prvek GridView k zobrazení uživatelských účtů. Vzhledem k tomu, že se řada kurzů zaměřuje na ověřování prostřednictvím formulářů, autorizaci, uživatelské účty a role, Nechci strávit příliš mnoho času, který by probral vnitřní práci ovládacího prvku GridView. I když tento kurz obsahuje konkrétní podrobné pokyny pro nastavení této stránky, neuvádí podrobnosti o tom, proč byly určité volby provedeny, nebo jaké konkrétní vlastnosti mají na Vykreslený výstup. Pro důkladné přezkoumání ovládacího prvku GridView se podívejte na *[práci s daty v řadě kurzů ASP.NET 2,0](../../data-access/index.md)* .

Začněte tím, že otevřete stránku `RoleBasedAuthorization.aspx` ve složce `Roles`. Přetáhněte prvek GridView ze stránky do návrháře a nastavte jeho `ID` na `UserGrid`. V okamžiku budeme psát kód, který bude volat `Membership`.`GetAllUsers` Metoda a váže výsledný objekt `MembershipUserCollection` k prvku GridView. `MembershipUserCollection` obsahuje objekt `MembershipUser` pro každý uživatelský účet v systému. objekty `MembershipUser` mají vlastnosti jako `UserName`,`Email`,`LastLoginDate` a tak dále.

Předtím, než napíšeme kód, který sváže uživatelské účty s mřížkou, nejdřív nadefinujeme pole prvku GridView. V inteligentní značce prvku GridView klikněte na odkaz Upravit sloupce a otevřete dialogové okno pole (viz obrázek 6). Z tohoto místa zrušte zaškrtnutí políčka automaticky generovat pole v levém dolním rohu. Vzhledem k tomu, že chceme, aby tento prvek GridView zahrnoval možnosti úprav a odstranění, přidejte CommandField a nastavte jeho `ShowEditButton` a vlastnosti `ShowDeleteButton` na hodnotu true. V dalším kroku přidejte čtyři pole pro zobrazení `UserName`, `Email`, `LastLoginDate`a `Comment`ch vlastností. Použijte vlastnost BoundField pro dvě vlastnosti jen pro čtení (`UserName` a `LastLoginDate`) a TemplateFields pro dvě upravitelná pole (`Email` a `Comment`).

Má první vlastnost BoundField zobrazovat vlastnost `UserName`; nastavte jeho `HeaderText` a vlastnosti `DataField` na "UserName". Toto pole nebude možné upravovat, proto nastavte jeho vlastnost `ReadOnly` na hodnotu true. Nakonfigurujte `LastLoginDate` vlastnost BoundField nastavením `HeaderText` na "Poslední přihlášení" a jeho `DataField` na "LastLoginDate". Pojďme naformátovat výstup tohoto vlastnost boundfieldu, aby se zobrazilo pouze datum (místo data a času). Pokud to chcete provést, nastavte vlastnost `HtmlEncode` vlastnost BoundField na hodnotu false a vlastnost `DataFormatString` na hodnotu "{0:d}". Nastavte také vlastnost `ReadOnly` na hodnotu true.

Nastavte vlastnosti `HeaderText` obou vlastností TemplateField na "E-mail" a "comment".

[![polí prvku GridView lze konfigurovat pomocí dialogového okna pole.](role-based-authorization-vb/_static/image17.png)](role-based-authorization-vb/_static/image16.png)

**Obrázek 6**: pole prvku GridView lze konfigurovat pomocí dialogového okna pole ([kliknutím zobrazíte obrázek v plné velikosti).](role-based-authorization-vb/_static/image18.png)

Teď je potřeba definovat `ItemTemplate` a `EditItemTemplate` pole "E-mail" a "comment". Přidejte webový ovládací prvek popisek do každého `ItemTemplates` a navažte své `Text` vlastnosti na `Email` a `Comment` vlastnosti v uvedeném pořadí.

Pro TemplateField "E-mail" přidejte do svého `EditItemTemplate` textové pole s názvem `Email` a vytvořte vazbu jeho vlastnosti `Text` s vlastností `Email` pomocí obousměrné datové vazby. Přidejte do `EditItemTemplate` RequiredFieldValidator a RegularExpressionValidator, abyste zajistili, že návštěvník upravující vlastnost email zadal platnou e-mailovou adresu. Pro TemplateField ' comment ' přidejte do `EditItemTemplate`víceřádkové textové pole s názvem `Comment`. Nastavte vlastnosti `Columns` a `Rows` textového pole na 40 a 4 v uvedeném pořadí a potom vytvořte vazbu jeho vlastnosti `Text` na vlastnost `Comment` pomocí obousměrné datové vazby.

Po konfiguraci těchto vlastností TemplateField by jejich deklarativní označení mělo vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](role-based-authorization-vb/samples/sample4.aspx)]

Když upravujete nebo odstraňujete uživatelský účet, bude potřeba, abyste věděli, že hodnota vlastnosti `UserName` tohoto uživatele. Nastavte vlastnost `DataKeyNames` prvku GridView na "UserName", aby byly tyto informace k dispozici prostřednictvím kolekce `DataKeys` prvku GridView.

Nakonec na stránku přidejte ovládací prvek ovládací souhrnu ověření a nastavte jeho vlastnost `ShowMessageBox` na hodnotu true a vlastnost `ShowSummary` na hodnotu false. Pomocí těchto nastavení ovládací souhrnu ověření zobrazí výstrahu na straně klienta, pokud se uživatel pokusí upravit uživatelský účet s chybějící nebo neplatnou e-mailovou adresou.

[!code-aspx[Main](role-based-authorization-vb/samples/sample5.aspx)]

Nyní jsme dokončili deklarativní označení této stránky. Naším dalším úkolem je vytvořit datovou sadu uživatelských účtů k prvku GridView. Přidejte metodu s názvem `BindUserGrid` do třídy kódu na pozadí `RoleBasedAuthorization.aspx` stránky, která váže `MembershipUserCollection` vrácených `Membership.GetAllUsers` do prvku `UserGrid` GridView. Voláním této metody z obslužné rutiny události `Page_Load` na první stránce.

[!code-vb[Main](role-based-authorization-vb/samples/sample6.vb)]

Pokud je tento kód na místě, navštivte stránku pomocí prohlížeče. Jak ukazuje obrázek 7, měla by se zobrazit informace o zobrazení prvku GridView o každém uživatelském účtu v systému.

[![UserGrid GridView zobrazí informace o jednotlivých uživatelích v systému.](role-based-authorization-vb/_static/image20.png)](role-based-authorization-vb/_static/image19.png)

**Obrázek 7**: `UserGrid` GridView zobrazí informace o jednotlivých uživatelích v systému ([kliknutím zobrazíte obrázek v plné velikosti).](role-based-authorization-vb/_static/image21.png)

> [!NOTE]
> `UserGrid` GridView zobrazí všechny uživatele v nestránkovaném rozhraní. Toto rozhraní jednoduché mřížky není vhodné pro scénáře, ve kterých je několik desítek uživatelů. Jednou z možností je nakonfigurovat prvek GridView tak, aby umožňoval stránkování. Metoda `Membership.GetAllUsers` má dvě přetížení: jednu, která nepřijímá žádné vstupní parametry, vrátí všechny uživatele a jeden z nich, který přebírá celočíselné hodnoty pro index stránky a velikost stránky, a vrátí pouze zadanou podmnožinu uživatelů. Druhé přetížení lze použít k efektivnějšímu stránkování uživatelů, protože vrací pouze přesné podmnožiny uživatelských účtů, nikoli *všechny* . Máte-li tisíce uživatelských účtů, je vhodné zvážit rozhraní založené na filtrech, které zobrazuje pouze uživatele, jejichž uživatelské jméno začíná zvoleným znakem, například. [Metoda`Membership.FindUsersByName`](https://msdn.microsoft.com/library/system.web.security.membership.findusersbyname.aspx) je ideální pro sestavování uživatelského rozhraní založeného na filtrech. V budoucím kurzu se podíváme na sestavení takového rozhraní.

Ovládací prvek GridView nabízí vestavěnou úpravu a odstranění podpory, pokud je ovládací prvek svázán s správně nakonfigurovaným ovládacím prvkem zdroje dat, jako je SqlDataSource nebo ObjectDataSource. `UserGrid` prvek GridView má však svá data programově svázaná; Proto je nutné napsat kód, který provede tyto dvě úlohy. Konkrétně je potřeba vytvořit obslužné rutiny událostí pro `RowEditing`, `RowCancelingEdit`, `RowUpdating`a `RowDeleting` události, které se aktivují, když návštěvník klikne na tlačítka pro úpravy, zrušení, aktualizaci nebo odstranění prvku GridView.

Začněte vytvořením obslužných rutin událostí pro `RowEditing`, `RowCancelingEdit`a `RowUpdating` událostí prvku GridView a přidejte následující kód:

[!code-vb[Main](role-based-authorization-vb/samples/sample7.vb)]

Obslužné rutiny událostí `RowEditing` a `RowCancelingEdit` jednoduše nastaví vlastnost `EditIndex` prvku GridView a pak znovu naváže seznam uživatelských účtů k mřížce. Zajímavé věci se objeví v obslužné rutině události `RowUpdating`. Tato obslužná rutina události se spustí tím, že zajistí, aby data byla platná, a potom se z kolekce `DataKeys` při`UserName`a hodnota upravovaného uživatelského účtu. Do těchto dvou polí TemplateField `EditItemTemplate` a jsou pak programově odkazována textová pole `Email` a `Comment`. Jejich `Text` vlastnosti obsahují upravenou e-mailovou adresu a komentář.

Aby bylo možné aktualizovat uživatelský účet prostřednictvím rozhraní API pro členství, musíme nejdřív získat informace o uživateli, které provedeme prostřednictvím volání `Membership.GetUser(userName)`. Vrácených vlastností `Email` objektu `MembershipUser` a `Comment` je pak Aktualizováno hodnotami zadanými do dvou textových polí z rozhraní pro úpravy. Nakonec jsou tyto úpravy uloženy s voláním [`Membership.UpdateUser`](https://msdn.microsoft.com/library/system.web.security.membership.updateuser.aspx). Obslužná rutina události `RowUpdating` se dokončí vrácením prvku GridView do jeho rozhraní před úpravou.

Dále vytvořte obslužnou rutinu události `RowDeleting` RowDeleting a přidejte následující kód:

[!code-vb[Main](role-based-authorization-vb/samples/sample8.vb)]

Výše uvedená obslužná rutina události začíná přebírání `UserName` hodnoty z kolekce `DataKeys` prvku GridView; Tato hodnota `UserName` se pak předává do [metody`DeleteUser`](https://msdn.microsoft.com/library/system.web.security.membership.deleteuser.aspx)třídy členství. Metoda `DeleteUser` odstraní uživatelský účet ze systému, včetně souvisejících dat členství (například to, k jakým rolím tento uživatel patří). Po odstranění uživatele je `EditIndex` mřížky nastavená na hodnotu-1 (pro případ, že uživatel klikl na tlačítko Odstranit, zatímco jiný řádek byl v režimu úprav) a zavolá se metoda `BindUserGrid`.

> [!NOTE]
> Tlačítko Odstranit nevyžaduje před odstraněním uživatelského účtu žádné potvrzení od uživatele. Doporučujeme přidat nějakou formu potvrzení uživatele, abyste se zmenšení pravděpodobnosti, že se účet omylem odstranil. Jedním z nejjednodušších způsobů, jak potvrdit akci, je použít dialogové okno pro potvrzení na straně klienta. Další informace o tomto postupu najdete v tématu [Přidání potvrzení na straně klienta při odstraňování](https://asp.net/learn/data-access/tutorial-42-vb.aspx).

Ověřte, zda tato stránka funguje podle očekávání. Měli byste být schopni upravit e-mailovou adresu a komentář libovolného uživatele a také odstranit jakýkoli uživatelský účet. Vzhledem k tomu, že stránka `RoleBasedAuthorization.aspx` je přístupná všem uživatelům, může na této stránce přejít i na anonymní návštěvníky – na této stránce a na Upravit a odstranit uživatelské účty! Pojďme aktualizovat tuto stránku tak, aby mohli upravovat e-mailové adresy a komentáře uživatele jenom uživatelé v rolích vedoucí a Administrators a jenom správci můžou odstranit uživatelský účet.

Oddíl "použití ovládacího prvku LoginView" vyhledá použití ovládacího prvku LoginView k zobrazení pokynů specifických pro roli uživatele. Pokud uživatel na této stránce navštíví roli správce, zobrazí se vám pokyny k úpravám a odstraňování uživatelů. Pokud uživatel v roli Nadřízenýe dosáhne této stránky, zobrazí se vám pokyny k úpravám uživatelů. A pokud je návštěvník anonymní nebo není v roli správce nebo správce, zobrazí se zpráva s vysvětlením, že nemůžou upravovat ani odstraňovat informace o uživatelském účtu. V části programově se omezuje Funkčnostme psaní kódu, který programově zobrazuje nebo skrývá tlačítka pro úpravy a odstranění na základě role uživatele.

### <a name="using-the-loginview-control"></a>Použití ovládacího prvku LoginView

Jak jsme viděli v minulých kurzech, ovládací prvek LoginView je užitečný pro zobrazení různých rozhraní pro ověřené a anonymní uživatele, ale ovládací prvek LoginView lze použít také k zobrazení různých značek na základě rolí uživatele. Pojďme použít ovládací prvek LoginView k zobrazení různých pokynů na základě role navštíveného uživatele.

Začněte přidáním prvku LoginView nad `UserGrid` prvku GridView. Jak bylo popsáno dříve, ovládací prvek LoginView má dva předdefinované šablony: `AnonymousTemplate` a `LoggedInTemplate`. Do obou těchto šablon zadejte stručnou zprávu, která uživatele informuje o tom, že nemůžou upravovat ani odstraňovat informace o uživateli.

[!code-aspx[Main](role-based-authorization-vb/samples/sample9.aspx)]

Kromě `AnonymousTemplate` a `LoggedInTemplate`může ovládací prvek LoginView zahrnovat *kolekci RoleGroups*, což jsou šablony pro konkrétní role. Každá role role obsahuje jednu vlastnost `Roles`, která určuje, pro jaké role se role vztahuje. Vlastnost `Roles` lze nastavit na jedinou roli (například "Administrators") nebo na seznam rolí oddělených čárkou (například Administrators, Vedoucís).

Pokud chcete spravovat kolekci RoleGroups, klikněte na odkaz upravit kolekci RoleGroups z inteligentní značky ovládacího prvku a zobrazte tak editor kolekce rolí. Přidejte dvě nové kolekci RoleGroups. Nastavte vlastnost `Roles` první skupiny rolí na "Administrators" a druhou na "nadřízený".

[![spravovat šablony specifické pro role LoginView prostřednictvím editoru kolekce rolí](role-based-authorization-vb/_static/image23.png)](role-based-authorization-vb/_static/image22.png)

**Obrázek 8**: Správa šablon specifických pro role LoginView pomocí editoru kolekce rolí ([kliknutím zobrazíte obrázek v plné velikosti](role-based-authorization-vb/_static/image24.png))

Kliknutím na tlačítko OK zavřete Editor kolekce rolí. Tím se aktualizuje deklarativní označení prvku LoginView tak, aby zahrnovala `<RoleGroups>` oddíl s `<asp:RoleGroup>` podřízeným elementem pro každou skupinu rolí definovanou v editoru kolekce rolí. Kromě toho rozevírací seznam "zobrazení" v inteligentní značce LoginView – který zpočátku uvádí pouze `AnonymousTemplate` a `LoggedInTemplate` – nyní obsahuje také přidané kolekci rolegroupsy.

Upravte kolekci RoleGroups tak, aby se uživatelům v roli Vedoucíi zobrazili pokyny k úpravám uživatelských účtů, zatímco uživatelé v roli správců jsou uvedeni pokyny k úpravám a odstraňování. Po provedení těchto změn by deklarativní označení vaší LoginView mělo vypadat podobně jako následující.

[!code-aspx[Main](role-based-authorization-vb/samples/sample10.aspx)]

Po provedení těchto změn stránku uložte a pak ji přejděte přes prohlížeč. Nejdřív stránku navštívíte jako anonymní uživatel. Měla by se zobrazit zpráva "Nejste přihlášeni k systému. Proto nemůžete upravovat ani odstraňovat informace o uživateli. " Pak se přihlaste jako ověřený uživatel, ale ten, který se nenachází v roli správce ani správce. Tentokrát by se měla zobrazit zpráva "Nejste členem rolí správce nebo správců. Proto nemůžete upravovat ani odstraňovat informace o uživateli. "

Potom se přihlaste jako uživatel, který je členem role vedoucí. Tentokrát by se měla zobrazit zpráva vedoucí ke konkrétní roli (viz obrázek 9). A pokud se přihlásíte jako uživatel v roli správců, měla by se zobrazit zpráva specifická pro roli správců (viz obrázek 10).

[![Bruce se zobrazuje zpráva vedoucí ke konkrétní roli.](role-based-authorization-vb/_static/image26.png)](role-based-authorization-vb/_static/image25.png)

**Obrázek 9**: Bruce je zobrazená zpráva vedoucí ke konkrétní roli ([kliknutím zobrazíte obrázek v plné velikosti).](role-based-authorization-vb/_static/image27.png)

[![tito se zobrazí zpráva specifická pro roli správce](role-based-authorization-vb/_static/image29.png)](role-based-authorization-vb/_static/image28.png)

**Obrázek 10**: Tito se zobrazuje zpráva správců specifická pro roli ([kliknutím zobrazíte obrázek v plné velikosti).](role-based-authorization-vb/_static/image30.png)

V případě, že se snímky obrazovky na obrázcích 9 a 10 zobrazují, vykreslují pouze jednu šablonu, i když je použito více šablon. Bruce a tito jsou přihlášeni jako uživatelé, ale ovládací prvky LoginView vykreslují pouze stejnou roli role a nikoli `LoggedInTemplate`. Kromě toho tito patří do rolí správců i vedoucích, ale ovládací prvek LoginView vykresluje šablonu správců specifickou pro role namísto vedoucích jedna.

Obrázek 11 znázorňuje pracovní postup, který používá ovládací prvek LoginView k určení, která šablona se má vykreslit. Všimněte si, že pokud je zadána více než jedna zadaná role, šablona LoginView vykreslí *první* roli, která odpovídá. Jinými slovy, pokud máme jako první skupinu rolí a správce jako druhou, pak když tito navštíví tuto stránku, uvidí zprávu vedoucí.

[![pracovní postup ovládacího prvku LoginView pro určení, která šablona se má vykreslit](role-based-authorization-vb/_static/image32.png)](role-based-authorization-vb/_static/image31.png)

**Obrázek 11**: pracovní postup ovládacího prvku LoginView pro určení, která šablona se má vykreslit ([kliknutím zobrazíte obrázek v plné velikosti](role-based-authorization-vb/_static/image33.png))

### <a name="programmatically-limiting-functionality"></a>Programově omezené funkce

I když ovládací prvek LoginView zobrazuje různé pokyny v závislosti na roli uživatele, který navštíví stránku, tlačítka pro úpravy a zrušení zůstávají viditelná pro všechny. Pro anonymní návštěvníky a uživatele, kteří nejsou v roli vedoucí ani správce, je potřeba programově skrýt tlačítka pro úpravy a odstranění. Musíme skrýt tlačítko Odstranit pro všechny uživatele, kteří nejsou správci. Aby bylo možné tento postup provést, napíšeme bitovou kopii kódu, který programově odkazuje na CommandField úpravy a odstranění LinkButtons, a v případě potřeby nastaví vlastnosti `Visible` na `False`.

Nejjednodušší způsob, jak programově odkazovat ovládací prvky ve CommandField, je nejprve převést na šablonu. To lze provést tak, že kliknete na odkaz Upravit sloupce z inteligentní značky GridView, vyberete CommandField ze seznamu aktuálních polí a kliknete na odkaz převést toto pole na TemplateField. Tím se CommandField převede na TemplateField pomocí `ItemTemplate` a `EditItemTemplate`. `ItemTemplate` obsahuje LinkButtony Edit a DELETE, zatímco `EditItemTemplate` v rámci aktualizace a zrušení LinkButtons.

[![převést CommandField na TemplateField](role-based-authorization-vb/_static/image35.png)](role-based-authorization-vb/_static/image34.png)

**Obrázek 12**: Převeďte CommandField na TemplateField ([kliknutím zobrazíte obrázek v plné velikosti).](role-based-authorization-vb/_static/image36.png)

Aktualizujte položky LinkButtons Edit a DELETE v `ItemTemplate`a nastavte jejich vlastnosti `ID` na hodnoty `EditButton` a `DeleteButton`v uvedeném pořadí.

[!code-aspx[Main](role-based-authorization-vb/samples/sample11.aspx)]

Vždy, když jsou data svázána s prvku GridView, prvek GridView vytvoří výčet záznamů v jeho vlastnosti `DataSource` a vygeneruje odpovídající objekt `GridViewRow`. Při vytvoření každého objektu `GridViewRow` je vyvolána událost `RowCreated`. Aby bylo možné skrýt tlačítka pro úpravy a odstranění pro neoprávněné uživatele, musíme pro tuto událost vytvořit obslužnou rutinu události a programově odkazovat na vložené a odstranit LinkButtons, přičemž se odpovídajícím způsobem nastavují vlastnosti `Visible`.

Vytvořte obslužnou rutinu události `RowCreated` událost a přidejte následující kód:

[!code-vb[Main](role-based-authorization-vb/samples/sample12.vb)]

Mějte na paměti, že `RowCreated` událost je aktivována pro *všechny* řádky GridView, včetně záhlaví, zápatí, rozhraní pageru a tak dále. Chcete-li se s datovým řádkem, který není v režimu úprav (protože řádek v režimu úprav má místo úpravy a odstranění), odkazovat pouze na odkazy na úpravy a odstranění. Tuto kontrolu zpracovává příkaz `If`.

Pokud se chystáme s datovým řádkem, který není v režimu úprav, odkaz na úpravy a odstranění LinkButtons je odkazován a jejich `Visible` vlastnosti jsou nastaveny na základě logických hodnot vrácených metodou `IsInRole(roleName)` objektu `User`. Objekt `User` odkazuje na objekt zabezpečení vytvořený `RoleManagerModule`; v důsledku toho `IsInRole(roleName)` metoda používá rozhraní API rolí k určení, zda aktuální návštěvník patří do *roleName*.

> [!NOTE]
> Mohli bychom použít třídu role přímo a nahradit volání `User.IsInRole(roleName)` voláním [metody`Roles.IsUserInRole(roleName)`](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx). Rozhodli jste se v tomto příkladu použít metodu `IsInRole(roleName)` objektu zabezpečení, protože je efektivnější než použití rozhraní API rolí přímo. Dříve v tomto kurzu jsme nakonfigurovali správce rolí tak, aby v souboru cookie do mezipaměti aktualizoval role uživatelů. Tato data souborů cookie uložené v mezipaměti se využívají jenom při volání metody `IsInRole(roleName)` objektu zabezpečení. Přímá volání rozhraní API rolí vždy zahrnují cestu k úložišti rolí. I když se role v souboru cookie neukládají do mezipaměti, volání metody `IsInRole(roleName)` objektu zabezpečení je obvykle efektivnější, protože při prvním volání během žádosti ukládá výsledky do mezipaměti. Rozhraní API rolí na druhé straně neprovádí žádné ukládání do mezipaměti. Vzhledem k tomu, že se událost `RowCreated` spustí jednou pro každý řádek v prvku GridView, používá `User.IsInRole(roleName)` pouze jednu cestu k úložišti rolí, zatímco `Roles.IsUserInRole(roleName)` vyžaduje *n* cest, kde *n* je počet uživatelských účtů zobrazených v mřížce.

Vlastnost `Visible` tlačítka pro úpravy je nastavená na `True`, pokud uživatel, který navštíví tuto stránku, je v roli správci nebo Vedoucíi. v opačném případě je nastavená na `False`. Vlastnost `Visible` tlačítka odstranit je nastavená na `True` jenom v případě, že se uživatel nachází v roli Administrators.

Otestuje tuto stránku pomocí prohlížeče. Pokud stránku navštívíte jako anonymní návštěvník nebo jako uživatel, který není správcem ani správcem, je CommandField prázdná. pořád existuje, ale jako tenké Sliver bez tlačítek upravit nebo odstranit.

> [!NOTE]
> Je možné CommandField zcela skrýt, když se stránka navštíví bez oprávnění správce a bez správce. Tuto funkci mám jako cvičení pro čtenáře.

[![tlačítka pro úpravy a odstranění jsou skrytá pro nesprávce a bez správců.](role-based-authorization-vb/_static/image38.png)](role-based-authorization-vb/_static/image37.png)

**Obrázek 13**: tlačítka pro úpravy a odstranění jsou skrytá pro nesprávce a jiné ([kliknutím zobrazíte obrázek v plné velikosti](role-based-authorization-vb/_static/image39.png)).

Pokud uživatel, který patří do role správce (ale ne do role správců), uvidí jenom tlačítko Upravit.

[![, když je pro správce k dispozici tlačítko Upravit, je tlačítko Odstranit skryté.](role-based-authorization-vb/_static/image41.png)](role-based-authorization-vb/_static/image40.png)

**Obrázek 14**: zatímco tlačítko Upravit je dostupné pro správce, tlačítko Odstranit je skryté ([kliknutím zobrazíte obrázek v plné velikosti).](role-based-authorization-vb/_static/image42.png)

A pokud se správce navštíví, má přístup k tlačítkům upravit a odstranit.

[![tlačítek upravit a odstranit jsou dostupná jenom pro správce.](role-based-authorization-vb/_static/image44.png)](role-based-authorization-vb/_static/image43.png)

**Obrázek 15**: tlačítka pro úpravy a odstranění jsou k dispozici pouze správcům ([kliknutím zobrazíte obrázek v plné velikosti](role-based-authorization-vb/_static/image45.png)).

## <a name="step-3-applying-role-based-authorization-rules-to-classes-and-methods"></a>Krok 3: použití autorizačních pravidel na základě rolí na třídy a metody

V kroku 2 jsme omezili možnosti úprav pro uživatele v rolích vedoucích a správců a možnosti odstraňování jenom správcům. To bylo provedeno skrytím přidružených prvků uživatelského rozhraní pro neoprávněné uživatele prostřednictvím programových technik. Taková opatření nezaručují, že neoprávněný uživatel nebude moci provést privilegovanou akci. Může se jednat o prvky uživatelského rozhraní, které se přidají později, nebo které jsme zapomněli skrýt pro neoprávněné uživatele. Nebo počítačový podvodník může zjistit nějaký jiný způsob, jak ASP.NET stránku spustit požadovanou metodu.

Snadný způsob, jak zajistit, že konkrétnímu kusu funkcí nemůžete mít přístup neoprávněným uživatelem, je vytřídit tuto třídu nebo metodu pomocí [atributu`PrincipalPermission`](https://msdn.microsoft.com/library/system.security.permissions.principalpermissionattribute.aspx). Pokud modul runtime .NET používá třídu nebo provede některou z jeho metod, zkontroluje, zda má aktuální kontext zabezpečení oprávnění. Atribut `PrincipalPermission` poskytuje mechanismus, pomocí kterého můžeme definovat tato pravidla.

V <a id="_msoanchor_9"> </a>kurzu [*ověřování na základě uživatele*](../membership/user-based-authorization-vb.md) jsme se podívali na použití atributu `PrincipalPermission` zpátky. Konkrétně jsme viděli, jak vyplňujeme obslužnou rutinu události `SelectedIndexChanged` a `RowDeleting` prvku GridView tak, aby mohly být provedeny pouze ověřenými uživateli a tito v uvedeném pořadí. Atribut `PrincipalPermission` funguje stejně i s rolemi.

Pojďme pomocí atributu `PrincipalPermission` v prvku GridView `RowUpdating` a `RowDeleting` obslužné rutiny událostí, aby se zakázalo provádění neautorizovaných uživatelů. Vše, co je potřeba udělat, je přidat odpovídající atribut základem jednotlivé definice funkce:

[!code-vb[Main](role-based-authorization-vb/samples/sample13.vb)]

Atribut pro `RowUpdating` obslužná rutina události Určuje, že pouze uživatelé v rolích správců nebo vedoucích mohou spustit obslužnou rutinu události, kde atribut v obslužné rutině události `RowDeleting` omezuje provádění na uživatele v roli správců.

> [!NOTE]
> Atribut `PrincipalPermission` je reprezentován jako třída v oboru názvů `System.Security.Permissions`. Nezapomeňte přidat příkaz `Imports System.Security.Permissions` v horní části souboru třídy kódu na pozadí pro import tohoto oboru názvů.

V případě, že se nesprávce pokusí spustit obslužnou rutinu `RowDeleting` události nebo pokud se nespustí správce nebo se pokusí spustit obslužnou rutinu události `RowUpdating`, modul runtime .NET vyvolá `SecurityException`.

[![je-li kontext zabezpečení autorizován pro spuštění metody, je vyvolána výjimka SecurityException](role-based-authorization-vb/_static/image47.png)](role-based-authorization-vb/_static/image46.png)

**Obrázek 16**: Pokud kontext zabezpečení není autorizován k provedení metody, je vyvolána `SecurityException` ([kliknutím zobrazíte obrázek v plné velikosti).](role-based-authorization-vb/_static/image48.png)

Kromě stránek ASP.NET má řada aplikací také architekturu, která zahrnuje různé vrstvy, například obchodní logiku a vrstvy přístupu k datům. Tyto vrstvy jsou obvykle implementovány jako knihovny tříd a třídy nabídky a metody pro provádění obchodní logiky a funkcionality související s daty. Atribut `PrincipalPermission` je užitečný pro použití autorizačních pravidel pro tyto vrstvy.

Další informace o použití atributu `PrincipalPermission` k definování autorizačních pravidel pro třídy a metody najdete v záznamu blogu [Scott Guthrie](https://weblogs.asp.net/scottgu/) [Přidání autorizačních pravidel do obchodních a datových vrstev pomocí `PrincipalPermissionAttributes`](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx).

## <a name="summary"></a>Souhrn

V tomto kurzu jsme se podívali na to, jak na základě rolí uživatele zadat hrubou a přesnou autorizační pravidla zrn. Formátu. Funkce NET URL Authorization umožňuje vývojářům stránky určit, které identity mají povolený nebo odepřený přístup k jakým stránkám. Jak jsme viděli v <a id="_msoanchor_10"> </a>kurzu [*ověřování na základě uživatele*](../membership/user-based-authorization-vb.md) , autorizační pravidla URL se dají použít na základě uživatele. Můžou se taky použít na základě rolí rolí, jak jsme viděli v kroku 1 tohoto kurzu.

Pravidla autorizace jemně zrnitosti se můžou použít deklarativně nebo programově. V kroku 2 jsme se vyhledali pomocí funkce kolekci RoleGroups ovládacího prvku LoginView k vykreslení různých výstupů na základě rolí navštíveného uživatele. Prohlédli jsme také způsoby, jak programově zjistit, jestli uživatel patří do konkrétní role a jak se odpovídajícím způsobem upravit funkce stránky.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Přidání autorizačních pravidel do obchodních a datových vrstev pomocí `PrincipalPermissionAttributes`](https://weblogs.asp.net/scottgu/archive/2006/10/04/Tip_2F00_Trick_3A00_-Adding-Authorization-Rules-to-Business-and-Data-Layers-using-PrincipalPermissionAttributes.aspx)
- [Prověřování členství, rolí a profilů v ASP.NET 2.0: práce s rolemi](http://aspnet.4guysfromrolla.com/articles/121405-1.aspx)
- [Seznam otázek zabezpečení pro ASP.NET 2,0](https://msdn.microsoft.com/library/ms998375.aspx)
- [Technická dokumentace pro `<roleManager>` element](https://msdn.microsoft.com/library/ms164660.aspx)

### <a name="about-the-author"></a>O autorovi

Scott Mitchell, autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je *[Sams naučit se ASP.NET 2,0 za 24 hodin](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* . Scott se dá kontaktovat [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky...

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Recenzenti pro tento kurz zahrnují například Banerjee a Teresa Murphy. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](assigning-roles-to-users-vb.md)

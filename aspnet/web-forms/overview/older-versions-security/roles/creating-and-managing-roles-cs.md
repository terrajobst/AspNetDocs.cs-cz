---
uid: web-forms/overview/older-versions-security/roles/creating-and-managing-roles-cs
title: Vytváření a Správa rolí (C#) | Microsoft Docs
author: rick-anderson
description: Tento kurz prověřuje kroky nezbytné pro konfiguraci architektury rolí. Podle toho sestavíme webové stránky pro vytváření a odstraňování rolí.
ms.author: riande
ms.date: 03/24/2008
ms.assetid: 113f10b3-a19a-471b-8ff6-db3c79ce8a91
msc.legacyurl: /web-forms/overview/older-versions-security/roles/creating-and-managing-roles-cs
msc.type: authoredcontent
ms.openlocfilehash: a7883d0b05f2fa5a3fdac887f8c8b39d70418fb3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640243"
---
# <a name="creating-and-managing-roles-c"></a>Vytváření a správa rolí (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/CS.09.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial09_CreatingRoles_cs.pdf)

> Tento kurz prověřuje kroky nezbytné pro konfiguraci architektury rolí. Podle toho sestavíme webové stránky pro vytváření a odstraňování rolí.

## <a name="introduction"></a>Úvod

<a id="_msoanchor_1"> </a>V kurzu [*ověřování na základě uživatele*](../membership/user-based-authorization-cs.md) jsme se vyhledali pomocí oprávnění URL k omezení určitých uživatelů ze sady stránek a průzkumu deklarativních a programových techniků pro úpravu funkcí ASP.NET stránky na základě navštíveného uživatele. Udělování oprávnění pro přístup k stránkám nebo funkcím na základě uživatele se ale může stát nightmareem údržby ve scénářích, kdy je k dispozici mnoho uživatelských účtů nebo když se uživatelská oprávnění často mění. Pokaždé, když uživatel získá nebo ztratí autorizaci k provedení konkrétního úkolu, musí aktualizovat příslušná autorizační pravidla URL, deklarativní značení a kód.

Obvykle pomáhá klasifikovat uživatele do skupin nebo *rolí* a potom použít oprávnění pro role na základě rolí. Většina webových aplikací má například určitou sadu stránek nebo úloh, které jsou vyhrazeny pouze pro administrativní uživatele. Pomocí technik získaných v kurzu *ověřování na základě uživatele* přidáme vhodná AUTORIZAČNÍ pravidla URL, deklarativní značky a kód, které umožní zadaným uživatelským účtům provádět úlohy správy. Pokud ale byl přidán nový správce nebo pokud se stávající správce musel odvolat oprávnění pro správu, museli byste vracet a aktualizovat konfigurační soubory a webové stránky. Role však můžeme vytvořit roli správců a přiřadit tyto důvěryhodné uživatele k roli správců. V dalším kroku přidáme vhodná autorizační pravidla URL, deklarativní značky a kód, aby role správců mohla provádět různé úlohy správy. Díky této infrastruktuře je přidání nových správců k lokalitě nástroje nebo odebrání stávajících správců jednoduché, jako třeba zahrnutí nebo odebrání uživatele z role správců. Není nutná žádná konfigurace, deklarativní označení nebo změny kódu.

ASP.NET nabízí architekturu rolí pro definování rolí a jejich přidružení k uživatelským účtům. S architekturou role můžeme vytvořit a odstranit role, přidat uživatele do role nebo je z ní odebrat, zjistit skupinu uživatelů, kteří patří do určité role, a určit, jestli uživatel patří do určité role. Po nakonfigurování architektury rolí můžeme prostřednictvím autorizačních pravidel URL omezit přístup k stránkám rolí podle rolí a na základě rolí aktuálně přihlášeného uživatele můžete zobrazit nebo skrýt Další informace nebo funkce na stránce.

Tento kurz prověřuje kroky nezbytné pro konfiguraci architektury rolí. Podle toho sestavíme webové stránky pro vytváření a odstraňování rolí. <a id="_msoanchor_2"> </a>V kurzu [*přiřazování rolí uživatelům*](assigning-roles-to-users-cs.md) se podíváme na postup přidání a odebrání uživatelů z rolí. A v <a id="_msoanchor_3"> </a>kurzu [*ověřování založeného na rolích*](role-based-authorization-cs.md) se dozvíte, jak omezit přístup k stránkám rolí podle rolí a jak upravit funkce stránky v závislosti na roli navštíveného uživatele. Pojďme začít!

## <a name="step-1-adding-new-aspnet-pages"></a>Krok 1: přidání nových stránek ASP.NET

V tomto kurzu a dalších dvou budeme zkoumat různé funkce a možnosti související se rolemi. K implementaci témat prověřených v rámci těchto kurzů budeme potřebovat řadu ASP.NET stránek. Pojďme vytvořit tyto stránky a aktualizovat mapu webu.

Začněte vytvořením nové složky v projektu s názvem `Roles`. Dále přidejte čtyři nové stránky ASP.NET do složky `Roles` a propojíte jednotlivé stránky pomocí `Site.master` stránky předlohy. Pojmenujte stránky:

- `ManageRoles.aspx`
- `UsersAndRoles.aspx`
- `CreateUserWizardWithRoles.aspx`
- `RoleBasedAuthorization.aspx`

V tomto okamžiku by Průzkumník řešení projektu vypadala podobně jako snímek obrazovky, který ukazuje obrázek 1.

[do složky role byly přidány ![čtyři nové stránky.](creating-and-managing-roles-cs/_static/image2.png)](creating-and-managing-roles-cs/_static/image1.png)

**Obrázek 1**: do složky `Roles` bylo přidáno čtyři nové stránky ([kliknutím zobrazíte obrázek v plné velikosti).](creating-and-managing-roles-cs/_static/image3.png)

Každá stránka by měla v tomto okamžiku obsahovat dva ovládací prvky obsahu, jednu pro každý prvek prvků hlavní stránky: `MainContent` a `LoginContent`.

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample1.aspx)]

Odvolat, že výchozí kód `LoginContent` ContentPlaceHolder zobrazuje odkaz na přihlášení nebo odhlášení od webu v závislosti na tom, jestli je uživatel ověřený. Přítomnost ovládacího prvku `Content2` obsahu na stránce ASP.NET však přepisuje výchozí značku stránky předlohy. Jak jsme popsali v <a id="_msoanchor_4"> </a>kurzu [*Přehled ověřování*](../introduction/an-overview-of-forms-authentication-cs.md) založeného na formulářích, přepsání výchozích značek je užitečné na stránkách, kde nechcete zobrazovat možnosti související s přihlášením v levém sloupci.

Pro tyto čtyři stránky ale chceme pro `LoginContent` ContentPlaceHolder zobrazit výchozí označení stránky předlohy. Proto odeberte deklarativní označení pro ovládací prvek obsahu `Content2`. Po tom by každý ze čtyř značek stránky měl obsahovat pouze jeden ovládací prvek obsahu.

Nakonec aktualizujeme mapu webu (`Web.sitemap`), aby zahrnovala tyto nové webové stránky. Po `<siteMapNode>`, kterou jsme přidali pro kurzy členství, přidejte následující kód XML.

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample2.xml)]

Po aktualizaci mapy webu navštivte web prostřednictvím prohlížeče. Jak ukazuje obrázek 2, navigace na levé straně teď obsahuje položky pro kurzy rolí.

[do složky role byly přidány ![čtyři nové stránky.](creating-and-managing-roles-cs/_static/image5.png)](creating-and-managing-roles-cs/_static/image4.png)

**Obrázek 2**: do složky `Roles` bylo přidáno čtyři nové stránky ([kliknutím zobrazíte obrázek v plné velikosti).](creating-and-managing-roles-cs/_static/image6.png)

## <a name="step-2-specifying-and-configuring-the-roles-framework-provider"></a>Krok 2: určení a konfigurace poskytovatele rozhraní rolí

Podobně jako rozhraní členství, rozhraní role je sestaveno základem modelem poskytovatele. Jak je popsáno v <a id="_msoanchor_5"> </a>kurzu [*Základy zabezpečení a ASP.net support*](../introduction/security-basics-and-asp-net-support-cs.md) , .NET Framework lodí se třemi vestavěnými poskytovateli rolí: [`AuthorizationStoreRoleProvider`](https://msdn.microsoft.com/library/system.web.security.authorizationstoreroleprovider.aspx), [`WindowsTokenRoleProvider`](https://msdn.microsoft.com/library/system.web.security.windowstokenroleprovider.aspx)a [`SqlRoleProvider`](https://msdn.microsoft.com/library/system.web.security.sqlroleprovider.aspx). Tato řada kurzů se zaměřuje na `SqlRoleProvider`, která jako úložiště role používá databázi Microsoft SQL Server.

Pod pokrývá rámec rolí a `SqlRoleProvider` fungují stejně jako rozhraní členství a `SqlMembershipProvider`. .NET Framework obsahuje třídu `Roles`, která slouží jako rozhraní API pro architekturu role. Třída `Roles` obsahuje statické metody jako `CreateRole`, `DeleteRole`, `GetAllRoles`, `AddUserToRole`, `IsUserInRole`a tak dále. Když je vyvolána jedna z těchto metod, třída `Roles` deleguje volání nakonfigurovaného zprostředkovatele. `SqlRoleProvider` v reakci pracuje s tabulkami, které jsou specifické pro role (`aspnet_Roles` a `aspnet_UsersInRoles`).

Aby bylo možné používat poskytovatele `SqlRoleProvider` v naší aplikaci, musíme určit, kterou databázi použít jako úložiště. `SqlRoleProvider` očekává, že úložiště rolí má určité databázové tabulky, zobrazení a uložené procedury. Tyto požadované objekty databáze je možné přidat pomocí [nástroje`aspnet_regsql.exe`](https://msdn.microsoft.com/library/ms229862.aspx). V tuto chvíli již máme databázi se schématem, které je nezbytné pro `SqlRoleProvider`. Zpět v <a id="_msoanchor_6"> </a> [*vytváření schématu členství v SQL Server*](../membership/creating-the-membership-schema-in-sql-server-cs.md) kurzu jsme vytvořili databázi s názvem `SecurityTutorials.mdf` a použili jste `aspnet_regsql.exe` k přidání aplikačních služeb, které obsahují databázové objekty vyžadované `SqlRoleProvider`. Proto musíme pouze sdělit rozhraní role, aby bylo možné povolit podporu rolí a používat `SqlRoleProvider` s databází `SecurityTutorials.mdf` jako úložiště rolí.

Rozhraní role se konfiguruje prostřednictvím &lt;`roleManager`&gt; elementu v souboru `Web.config` aplikace. Ve výchozím nastavení je podpora rolí zakázaná. Chcete-li jej povolit, je nutné nastavit atribut `enabled` [&lt;`roleManager`&gt;](https://msdn.microsoft.com/library/ms164660.aspx) elementu na `true`, například:

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample3.xml)]

Ve výchozím nastavení mají všechny webové aplikace poskytovatele rolí s názvem `AspNetSqlRoleProvider` typu `SqlRoleProvider`. Tento výchozí zprostředkovatel je zaregistrován v `machine.config` (nachází se v `%WINDIR%\Microsoft.Net\Framework\v2.0.50727\CONFIG`):

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample4.xml)]

Atribut `connectionStringName` zprostředkovatele určuje používané úložiště rolí. Poskytovatel `AspNetSqlRoleProvider` nastaví tento atribut na hodnotu `LocalSqlServer`, která je také definována v `machine.config` a body ve výchozím nastavení, do databáze SQL Server 2005 Express Edition ve složce `App_Data` s názvem `aspnet.mdf`.

V důsledku toho, pokud jednoduše povolíme architekturu rolí bez zadání informací o poskytovateli v souboru `Web.config` aplikace, aplikace používá výchozí registrovaného poskytovatele rolí `AspNetSqlRoleProvider`. Pokud databáze `~/App_Data/aspnet.mdf` neexistuje, modul runtime ASP.NET ho automaticky vytvoří a přidá schéma služby Application Services. Nechci ale používat databázi `aspnet.mdf`; místo toho chceme použít databázi `SecurityTutorials.mdf`, kterou jsme již vytvořili, a přidat schéma služby Application Services do nástroje. Tuto úpravu lze provést jedním ze dvou způsobů:

- <strong>Zadejte hodnotu pro</strong> <strong>název připojovacího řetězce`LocalSqlServer`v</strong> <strong>`Web.config`</strong> <strong>.</strong> Přepsáním hodnoty názvu připojovacího řetězce `LocalSqlServer` v `Web.config`můžeme použít výchozí registrovaný zprostředkovatel rolí (`AspNetSqlRoleProvider`) a správně pracovat s databází `SecurityTutorials.mdf`. Další informace o této technice najdete v příspěvku na blogu [Scott Guthrie](https://weblogs.asp.net/scottgu/), [konfigurace ASP.NET 2,0 Aplikační služby pro použití SQL Server 2000 nebo SQL Server 2005](https://weblogs.asp.net/scottgu/archive/2005/08/25/423703.aspx).
- <strong>Přidejte nového registrovaného poskytovatele typu</strong> <strong>`SqlRoleProvider`</strong> <strong>a nakonfigurujte jeho</strong> nastavení<strong>`connectionStringName`</strong> <strong>tak, aby odkazovalo</strong> na databázi<strong>`SecurityTutorials.mdf`</strong> <strong>.</strong> Toto je doporučený postup, který se používá v <a id="_msoanchor_7"> </a>rámci [*vytváření schématu členství v SQL Server*](../membership/creating-the-membership-schema-in-sql-server-cs.md) kurzu a jedná se o přístup, který v tomto kurzu použijeme i vy.

Do souboru `Web.config` přidejte následující označení konfigurace rolí. Tento kód zaregistruje nového poskytovatele s názvem `SecurityTutorialsSqlRoleProvider`.

[!code-xml[Main](creating-and-managing-roles-cs/samples/sample5.xml)]

Výše uvedený kód definuje `SecurityTutorialsSqlRoleProvider` jako výchozího zprostředkovatele (prostřednictvím `defaultProvider` atributu v elementu `<roleManager>`). Nastaví také nastavení `applicationName` `SecurityTutorialsSqlRoleProvider`na `SecurityTutorials`, což je stejné nastavení `applicationName` používané poskytovatelem členství (`SecurityTutorialsSqlMembershipProvider`). I když zde není zobrazen, [element`<add>`](https://msdn.microsoft.com/library/ms164662.aspx) pro `SqlRoleProvider` může také obsahovat atribut `commandTimeout` k určení doby trvání časového limitu databáze (v sekundách). Výchozí hodnota je 30.

S tímto kódem konfigurace jsme připraveni začít s používáním funkcí role v rámci naší aplikace.

> [!NOTE]
> Výše uvedené konfigurační značky ilustrují použití atributů `enabled` a `defaultProvider` elementu &lt;`roleManager`&gt;. Existuje mnoho dalších atributů, které mají vliv na způsob, jakým role Framework přiřazuje informace o roli pro uživatele na základě uživatele. Tato nastavení prověříme v <a id="_msoanchor_8"> </a>kurzu [*ověřování na základě rolí*](role-based-authorization-cs.md) .

## <a name="step-3-examining-the-roles-api"></a>Krok 3: prozkoumání rozhraní API rolí

Funkce rozhraní role je vystavena prostřednictvím [třídy`Roles`](https://msdn.microsoft.com/library/system.web.security.roles.aspx), která obsahuje třináct statických metod pro provádění operací založených na rolích. Když se podíváme na vytváření a odstraňování rolí v krocích 4 a 6, použijeme metody [`CreateRole`](https://msdn.microsoft.com/library/system.web.security.roles.createrole.aspx) a [`DeleteRole`](https://msdn.microsoft.com/library/system.web.security.roles.deleterole.aspx) , které přidají nebo odeberou roli ze systému.

Chcete-li získat seznam všech rolí v systému, použijte [metodu`GetAllRoles`](https://msdn.microsoft.com/library/system.web.security.roles.getallroles.aspx) (viz krok 5). [Metoda`RoleExists`](https://msdn.microsoft.com/library/system.web.security.roles.roleexists.aspx) vrací logickou hodnotu, která označuje, zda zadaná role existuje.

V dalším kurzu podíváme se, jak přidružit uživatele k rolím. Metody [`AddUserToRole`](https://msdn.microsoft.com/library/system.web.security.roles.addusertorole.aspx), [`AddUserToRoles`](https://msdn.microsoft.com/library/system.web.security.roles.addusertoroles.aspx), [`AddUsersToRole`](https://msdn.microsoft.com/library/system.web.security.roles.adduserstorole.aspx)a [`AddUsersToRoles`](https://msdn.microsoft.com/library/system.web.security.roles.adduserstoroles.aspx) třídy `Roles` do jedné nebo více rolí přidávají jednoho nebo více uživatelů. Chcete-li odebrat uživatele z rolí, použijte metody [`RemoveUserFromRole`](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromrole.aspx), [`RemoveUserFromRoles`](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromroles.aspx), [`RemoveUsersFromRole`](https://msdn.microsoft.com/library/system.web.security.roles.removeusersfromrole.aspx)nebo [`RemoveUsersFromRoles`](https://msdn.microsoft.com/library/system.web.security.roles.removeusersfromroles.aspx) .

<a id="_msoanchor_9"> </a>V kurzu [*ověřování na základě role*](role-based-authorization-cs.md) podíváme se na způsoby, jak programově zobrazit nebo skrýt funkce na základě role aktuálně přihlášeného uživatele. K tomu můžeme použít metody [`FindUsersInRole`](https://msdn.microsoft.com/library/system.web.security.roles.findusersinrole.aspx), [`GetRolesForUser`](https://msdn.microsoft.com/library/system.web.security.roles.getrolesforuser.aspx), [`GetUsersInRole`](https://msdn.microsoft.com/library/system.web.security.roles.getusersinrole.aspx)nebo [`IsUserInRole`](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx) třídy `Role`.

> [!NOTE]
> Mějte na paměti, že pokud je vyvolána jedna z těchto metod, třída `Roles` deleguje volání nakonfigurovaného zprostředkovatele. V našem případě to znamená, že se volání odesílá do `SqlRoleProvider`. `SqlRoleProvider` pak provede příslušnou databázovou operaci na základě vyvolané metody. Například kód `Roles.CreateRole("Administrators")` vede `SqlRoleProvider` provádění uložené procedury `aspnet_Roles_CreateRole`, která vloží nový záznam do tabulky `aspnet_Roles` s názvem Administrators.

Zbývající část tohoto kurzu se zabývá používáním metod `CreateRole`, `GetAllRoles`a `DeleteRole` třídy `Roles` ke správě rolí v systému.

## <a name="step-4-creating-new-roles"></a>Krok 4: vytvoření nových rolí

Role nabízí způsob, jak libovolně seskupovat uživatele a nejčastěji toto seskupení slouží k pohodlnější způsobu použití autorizačních pravidel. Pokud ale chcete použít role jako autorizační mechanismus, nejdřív je potřeba definovat, jaké role v aplikaci existují. ASP.NET bohužel neobsahuje ovládací prvek CreateRoleWizard. Aby bylo možné přidat nové role, musíme vytvořit vhodné uživatelské rozhraní a vyvolat rozhraní API pro role dodržovali. Dobrá zpráva je, že to je velmi snadné.

> [!NOTE]
> I když není k dispozici žádný webový ovládací prvek CreateRoleWizard, je k dispozici [Nástroj pro správu webu ASP.NET](https://msdn.microsoft.com/library/ms228053.aspx), což je místní aplikace ASP.NET navržená tak, aby pomohla při zobrazení a správě konfigurace vaší webové aplikace. Nejedná se však o velký ventilátor nástroje pro správu webu ASP.NET ze dvou důvodů. Nejprve se jedná o bitovou laděnou a činnost koncového uživatele opouští hodně. Za druhé je nástroj pro správu webu ASP.NET navržený tak, aby fungoval pouze místně. to znamená, že budete muset vytvořit vlastní webové stránky správy rolí, pokud potřebujete vzdáleně spravovat role na živém webu. Z těchto dvou důvodů se v tomto kurzu a dalším se zaměřujete na vytváření nezbytných nástrojů pro správu rolí na webové stránce, a nemusíte se spoléhat na nástroj pro správu webu ASP.NET.

Otevřete stránku `ManageRoles.aspx` ve složce `Roles` a přidejte do stránky ovládací prvek webové tlačítko a tlačítko. Nastavte vlastnost `ID` ovládacího prvku TextBox na `RoleName` a vlastnosti `ID` a `Text` tlačítka na `CreateRoleButton` a vytvořit roli v uvedeném pořadí. V tomto okamžiku by deklarativní označení stránky mělo vypadat podobně jako následující:

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample6.aspx)]

Dále dvakrát klikněte na ovládací prvek tlačítko `CreateRoleButton` v návrháři a vytvořte obslužnou rutinu události `Click` a přidejte následující kód:

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample7.cs)]

Výše uvedený kód začíná přiřazením názvu oříznuté role zadaného v `RoleName` TextBox do proměnné `newRoleName`. Dále je volána metoda `RoleExists` třídy `Roles` k určení, zda role `newRoleName` již v systému existuje. Pokud role neexistuje, je vytvořena prostřednictvím volání metody `CreateRole`. Pokud je metodě `CreateRole` předán název role, která již v systému existuje, je vyvolána výjimka `ProviderException`. Proto kód nejprve kontroluje, aby se zajistilo, že role v systému ještě neexistuje, než zavoláte `CreateRole`. Obslužná rutina události `Click` končí tím, že se vymaže vlastnost `Text` textového pole `RoleName`.

> [!NOTE]
> Možná vás zajímá, co se stane, když uživatel do textového pole `RoleName` nezadáte žádnou hodnotu. Pokud je hodnota předaná do metody `CreateRole` `null` nebo prázdný řetězec, je vyvolána výjimka. Podobně platí, že pokud název role obsahuje čárku, je vyvolána výjimka. V důsledku toho by měla stránka obsahovat ovládací prvky ověřování, aby uživatel zadal roli a neobsahoval žádné čárky. Jako cvičení pro čtenáře mám odejít.

Pojďme vytvořit roli s názvem Administrators. Navštivte stránku `ManageRoles.aspx` v prohlížeči, do textového pole zadejte Administrators (viz obrázek 3) a pak klikněte na tlačítko vytvořit roli.

[![vytvoření role správců](creating-and-managing-roles-cs/_static/image8.png)](creating-and-managing-roles-cs/_static/image7.png)

**Obrázek 3**: vytvoření role správců ([kliknutím zobrazíte obrázek v plné velikosti](creating-and-managing-roles-cs/_static/image9.png))

Co se stane? Dojde k postbacku, ale není k dispozici žádný vizuální hromádka, že do systému byla role skutečně přidána. Tuto stránku v kroku 5 aktualizujeme, aby zahrnovala vizuální zpětnou vazbu. Teď ale můžete ověřit, že se role vytvořila, a to tak, že do databáze `SecurityTutorials.mdf`ete a zobrazíte data z tabulky `aspnet_Roles`. Jak ukazuje obrázek 4, tabulka `aspnet_Roles` obsahuje záznam pro role správce, které jste právě přidali.

[![tabulce aspnet_Roles má řádek pro správce](creating-and-managing-roles-cs/_static/image11.png)](creating-and-managing-roles-cs/_static/image10.png)

**Obrázek 4**: tabulka `aspnet_Roles` obsahuje řádek pro správce ([kliknutím zobrazíte obrázek v plné velikosti](creating-and-managing-roles-cs/_static/image12.png)).

## <a name="step-5-displaying-the-roles-in-the-system"></a>Krok 5: Zobrazení rolí v systému

Pojďme rozšířit stránku `ManageRoles.aspx`, aby obsahovala seznam aktuálních rolí v systému. K tomuto účelu přidejte ovládací prvek GridView na stránku a nastavte jeho vlastnost `ID` na hodnotu `RoleList`. Dále přidejte metodu do třídy kódu na pozadí stránky s názvem `DisplayRolesInGrid` pomocí následujícího kódu:

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample8.cs)]

Metoda `GetAllRoles` třídy `Roles` vrátí všechny role v systému jako pole řetězců. Toto pole řetězce je pak svázáno s prvku GridView. Aby bylo možné vytvořit vazby seznamu rolí k prvku GridView při prvním načtení stránky, je nutné volat metodu `DisplayRolesInGrid` z obslužné rutiny události `Page_Load` stránky. Následující kód volá tuto metodu při prvním navštívení stránky, ale ne při následném postbacku.

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample9.cs)]

Pokud je tento kód na místě, navštivte stránku pomocí prohlížeče. Jak ukazuje obrázek 5, měla by se zobrazit mřížka s jedním sloupcem označeným položkou. Mřížka obsahuje řádek pro roli správců, kterou jsme přidali v kroku 4.

[![se v prvku GridView zobrazují role v jednom sloupci.](creating-and-managing-roles-cs/_static/image14.png)](creating-and-managing-roles-cs/_static/image13.png)

**Obrázek 5**: prvek GridView zobrazí role v jednom sloupci ([kliknutím zobrazíte obrázek v plné velikosti).](creating-and-managing-roles-cs/_static/image15.png)

Prvek GridView zobrazí jedinou sloupec označený jako položka, protože vlastnost `AutoGenerateColumns` prvku GridView je nastavena na hodnotu true (výchozí), což způsobí, že prvek GridView automaticky vytvoří sloupec pro každou vlastnost v jeho `DataSource`. Pole má jedinou vlastnost, která představuje prvky v poli, tedy jeden sloupec v prvku GridView.

Při zobrazování dat pomocí prvku GridView, raději místo toho, aby byly implicitně generovány v prvku GridView, byly explicitně definovány moje sloupce. Explicitním definováním sloupců je mnohem snazší data formátovat, měnit jejich uspořádání a provádět další běžné úlohy. Proto aktualizujeme deklarativní označení prvku GridView tak, aby jeho sloupce byly explicitně definovány.

Začněte nastavením vlastnosti `AutoGenerateColumns` prvku GridView na hodnotu false. Potom do mřížky přidejte TemplateField, nastavte jeho vlastnost `HeaderText` na role a nakonfigurujte jeho `ItemTemplate` tak, aby zobrazovalo obsah pole. Chcete-li to dosáhnout, přidejte webový ovládací prvek popisek s názvem `RoleNameLabel` do `ItemTemplate` a navažte jeho vlastnost `Text` na `Container.DataItem`.

Tyto vlastnosti a obsah `ItemTemplate`lze nastavit deklarativně nebo prostřednictvím dialogového okna pole prvku GridView a upravit rozhraní šablon. Chcete-li získat přístup k dialogovému oknu pole, klikněte na odkaz Upravit sloupce v inteligentní značce prvku GridView. Poté zrušte zaškrtnutí políčka automaticky generovat pole, chcete-li nastavit vlastnost `AutoGenerateColumns` na hodnotu false a přidat pole TemplateField do prvku GridView, nastavením jeho vlastnosti `HeaderText` na role. Chcete-li definovat obsah `ItemTemplate`, vyberte možnost Upravit šablony z inteligentní značky prvku GridView. Přetáhněte ovládací prvek web Label na `ItemTemplate`, nastavte jeho vlastnost `ID` na `RoleNameLabel`a nakonfigurujte jeho nastavení s datovou vazbou tak, aby byla vlastnost `Text` svázaná s `Container.DataItem`.

Bez ohledu na to, jaký přístup používáte, by výsledný deklarativní kód prvku GridView měl po dokončení vypadat podobně jako následující.

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample10.aspx)]

> [!NOTE]
> Obsah pole se zobrazí pomocí `<%# Container.DataItem %>`syntaxe datové vazby. Podrobný popis, proč se tato syntaxe používá při zobrazení obsahu pole vázaného na prvek GridView, je nad rámec tohoto kurzu. Další informace o této problematice naleznete v tématu [vazba skalárního pole na datově datovou webovou ovládací prvek](http://aspnet.4guysfromrolla.com/articles/082504-1.aspx).

V současné době je `RoleList` prvek GridView svázán pouze se seznamem rolí při prvním navštívení stránky. Při přidání nové role musíme aktualizovat mřížku. Chcete-li to provést, aktualizujte obslužnou rutinu události `Click` tlačítka `CreateRoleButton` tak, aby při vytvoření nové role zavolala metodu `DisplayRolesInGrid`.

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample11.cs)]

Když teď uživatel přidá novou roli, `RoleList` prvek GridView zobrazí právě přidanou roli při postbacku a poskytne vizuální zpětnou vazbu, kterou se role úspěšně vytvořila. To provedete tak, že navštívíte stránku `ManageRoles.aspx` v prohlížeči a přidáte roli s názvem Nadřízenýes. Po kliknutí na tlačítko vytvořit roli se postback následovat a mřížka se aktualizuje tak, aby zahrnovala správce i nové role, vedoucí.

[![se přidala role Nadřízenýs.](creating-and-managing-roles-cs/_static/image17.png)](creating-and-managing-roles-cs/_static/image16.png)

**Obrázek 6**: přidala se role Nadřízený ([kliknutím zobrazíte obrázek v plné velikosti](creating-and-managing-roles-cs/_static/image18.png)).

## <a name="step-6-deleting-roles"></a>Krok 6: odstranění rolí

V tomto okamžiku může uživatel vytvořit novou roli a zobrazit všechny stávající role ze stránky `ManageRoles.aspx`. Umožňuje uživatelům také odstranit role. Metoda `Roles.DeleteRole` má dvě přetížení:

- [`DeleteRole(roleName)`](https://msdn.microsoft.com/library/ek4sywc0.aspx) – odstraní roli *roleName*. Pokud role obsahuje jednoho nebo více členů, je vyvolána výjimka.
- [`DeleteRole(roleName, throwOnPopulatedRole)`](https://msdn.microsoft.com/library/38h6wf59.aspx) – odstraní roli *roleName*. Pokud je `true`*throwOnPopulateRole* , pak je vyvolána výjimka, pokud role obsahuje jednoho nebo více členů. Pokud je `false`*throwOnPopulateRole* , odstraní se role bez ohledu na to, zda obsahuje nějaké členy. Interně `DeleteRole(roleName)` metoda volá `DeleteRole(roleName, true)`.

Metoda `DeleteRole` také vyvolá výjimku, pokud je *roleName* `null` nebo prázdný řetězec nebo pokud *roleName* obsahuje čárku. Pokud v systému *roleName* neexistuje, `DeleteRole` selžou bez vyvolání výjimky.

Pojďme rozšířit ovládací prvek GridView v `ManageRoles.aspx` tak, aby zahrnoval tlačítko pro odstranění, které po kliknutí odstraní vybranou roli. Začněte přidáním tlačítka odstranit do prvku GridView tak, že se vrátíte do dialogového okna pole a přidáte tlačítko Odstranit, které se nachází pod možností CommandField. Vytvořte tlačítko Odstranit ve sloupci úplně vlevo a nastavte jeho vlastnost `DeleteText` na Odstranit roli.

[![přidat tlačítko Odstranit do prvku GridView RoleList](creating-and-managing-roles-cs/_static/image20.png)](creating-and-managing-roles-cs/_static/image19.png)

**Obrázek 7**: Přidání tlačítka pro odstranění do `RoleList` GridView ([kliknutím zobrazíte obrázek v plné velikosti](creating-and-managing-roles-cs/_static/image21.png))

Po přidání tlačítka odstranit by deklarativní označení prvku GridView mělo vypadat podobně jako následující:

[!code-aspx[Main](creating-and-managing-roles-cs/samples/sample12.aspx)]

Dále vytvořte obslužnou rutinu události pro událost `RowDeleting` prvku GridView. Toto je událost, která je vyvolána při zpětném volání při kliknutí na tlačítko Odstranit roli. Přidejte následující kód do obslužné rutiny události.

[!code-csharp[Main](creating-and-managing-roles-cs/samples/sample13.cs)]

Kód začíná programově odkazující na `RoleNameLabel` webový ovládací prvek v řádku, na kterém bylo tlačítko pro odstranění role kliknuto. Následně se vyvolá metoda `Roles.DeleteRole`, která předává `Text` `RoleNameLabel` a `false`, čímž odstraňuje roli bez ohledu na to, jestli jsou k této roli přidruženi všichni uživatelé. Nakonec se `RoleList` prvek GridView aktualizuje tak, aby se v mřížce již nezobrazovala role pouhého odstranění.

> [!NOTE]
> Tlačítko Odstranit roli nevyžaduje před odstraněním role žádné potvrzení od uživatele. Jedním z nejjednodušších způsobů, jak potvrdit akci, je použít dialogové okno pro potvrzení na straně klienta. Další informace o tomto postupu najdete v tématu [Přidání potvrzení na straně klienta při odstraňování](https://asp.net/learn/data-access/tutorial-42-cs.aspx).

## <a name="summary"></a>Souhrn

Mnoho webových aplikací má určitá autorizační pravidla nebo funkce na úrovni stránky, které jsou k dispozici pouze pro určité třídy uživatelů. Může se například jednat o sadu webových stránek, ke kterým mají přístup jenom správci. Místo definování těchto autorizačních pravidel pro uživatele, často je lépe užitečné definovat pravidla na základě role. To znamená, že nemusíte explicitně povolit uživatelům Scott a Jisun přístup k webovým stránkám pro správu, což je efektivnější přístup k tomu, aby měli členové role správců přístup k těmto stránkám a pak mohli poznamenat Scott a Jisun jako uživatelé patřící do Role Administrators.

Role architektury usnadňuje vytváření a správu rolí. V tomto kurzu jsme prozkoumali, jak nakonfigurovat architekturu rolí, aby používala `SqlRoleProvider`, která jako úložiště role používá databázi Microsoft SQL Server. Vytvořili jsme také webovou stránku, která obsahuje seznam existujících rolí v systému a umožňuje vytvořit nové role a odstranit stávající. V dalších kurzech se dozvíte, jak přiřadit uživatele k rolím a jak použít autorizaci založenou na rolích.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Zkoumání členství, rolí a profilů v ASP.NET 2.0](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [Postupy: použití Správce rolí v ASP.NET 2,0](https://msdn.microsoft.com/library/ms998314.aspx)
- [Poskytovatelé rolí](https://msdn.microsoft.com/library/aa478950.aspx)
- [Postup při zavedení vlastního nástroje pro správu webu](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)
- [Technická dokumentace pro `<roleManager>` element](https://msdn.microsoft.com/library/ms164660.aspx)
- [Používání rozhraní API pro členství a správce rolí](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/security/membership.aspx)

### <a name="about-the-author"></a>O autorovi

Scott Mitchell, autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je *[Sams naučit se ASP.NET 2,0 za 24 hodin](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* . Scott se dá kontaktovat [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontroloři vedoucí pro tento kurz zahrnují Alicja Maziarz, jako jsou Banerjee a Teresa Murphy. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Next](assigning-roles-to-users-cs.md)

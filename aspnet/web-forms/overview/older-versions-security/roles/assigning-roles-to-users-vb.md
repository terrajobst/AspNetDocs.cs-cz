---
uid: web-forms/overview/older-versions-security/roles/assigning-roles-to-users-vb
title: Přiřazování rolí uživatelům (VB) | Microsoft Docs
author: rick-anderson
description: V tomto kurzu sestavíme dvě ASP.NET stránky, které vám pomůžou se správou toho, co uživatelé patří do rolí. První stránka bude obsahovat možnosti, které vám umožní zjistit, co...
ms.author: riande
ms.date: 03/24/2008
ms.assetid: fd208ee9-69cc-4467-9783-b4e039bdd1d3
msc.legacyurl: /web-forms/overview/older-versions-security/roles/assigning-roles-to-users-vb
msc.type: authoredcontent
ms.openlocfilehash: b53df4494eb0faef7c5e4547c2bf95e5fb071298
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74577861"
---
# <a name="assigning-roles-to-users-vb"></a>Přiřazení rolí uživatelům (VB)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/VB.10.zip) nebo [stažení PDF](https://download.microsoft.com/download/6/0/3/6032582f-360d-4739-b935-38721fdb86ea/aspnet_tutorial10_AssigningRoles_vb.pdf)

> V tomto kurzu sestavíme dvě ASP.NET stránky, které vám pomůžou se správou toho, co uživatelé patří do rolí. Na první stránce se budou zobrazovat informace o tom, co uživatelé patří k dané roli, k jakým rolím patří určitý uživatel a možnost přiřadit nebo odebrat konkrétního uživatele z konkrétní role. Na druhé stránce rozsadíme ovládací prvek ovládacím CreateUserWizard tak, aby obsahoval krok pro určení rolí, do kterých patří nově vytvořený uživatel. To je užitečné ve scénářích, kdy správce může vytvořit nové uživatelské účty.

## <a name="introduction"></a>Úvod

V <a id="_msoanchor_1"> </a> [předchozím kurzu](creating-and-managing-roles-vb.md) byly zkontrolovány architektury rolí a `SqlRoleProvider`; zjistili jsme, jak použít třídu `Roles` k vytváření, načítání a odstraňování rolí. Kromě vytváření a odstraňování rolí musíme být schopni přiřadit nebo odebrat uživatele z role. ASP.NET bohužel nedodává žádné webové ovládací prvky pro správu toho, co uživatelé patří do rolí. Místo toho je nutné vytvořit vlastní ASP.NET stránky pro správu těchto přidružení. Dobrá zpráva je, že přidávání a odebírání uživatelů do rolí je poměrně snadné. Třída `Roles` obsahuje řadu metod pro přidání jednoho nebo více uživatelů k jedné nebo více rolím.

V tomto kurzu sestavíme dvě ASP.NET stránky, které vám pomůžou se správou toho, co uživatelé patří do rolí. Na první stránce se budou zobrazovat informace o tom, co uživatelé patří k dané roli, k jakým rolím patří určitý uživatel a možnost přiřadit nebo odebrat konkrétního uživatele z konkrétní role. Na druhé stránce rozsadíme ovládací prvek ovládacím CreateUserWizard tak, aby obsahoval krok pro určení rolí, do kterých patří nově vytvořený uživatel. To je užitečné ve scénářích, kdy správce může vytvořit nové uživatelské účty.

Pojďme začít!

## <a name="listing-what-users-belong-to-what-roles"></a>Výpis toho, co uživatelé patří k rolím

Prvním pořadím podnikání pro účely tohoto kurzu je vytvoření webové stránky, ze které lze přiřadit uživatele k rolím. Předtím, než se budeme věnovat dodržovali s přiřazením uživatelů k rolím, se nejprve zaměřujeme na to, jak určit, co uživatelé patří k rolím. Existují dva způsoby, jak zobrazit tyto informace: "podle role" nebo "podle uživatele". Mohli bychom návštěvníkům dovolit vybrat roli a pak jim zobrazit všechny uživatele, kteří patří do této role (zobrazení "podle role"), nebo se může vyzvat návštěvníka k výběru uživatele a pak jim zobrazit role přiřazené tomuto uživateli (zobrazení "podle uživatele").

Zobrazení "podle rolí" je užitečné v případech, kdy návštěvník chce znát skupinu uživatelů, kteří patří do určité role; zobrazení "podle uživatele" je ideální, když návštěvník potřebuje znát role určitého uživatele. Máme naši stránku, jak na to role, tak i na základě uživatelského rozhraní.

Začneme tím, že se vytvoří rozhraní "podle uživatele". Toto rozhraní se bude skládat z rozevíracího seznamu a seznamu zaškrtávacích políček. Rozevírací seznam se naplní sadou uživatelů v systému. zaškrtávací políčka budou vytvářet výčet rolí. Výběrem uživatele v rozevíracím seznamu se budou tyto role, ke kterým uživatel patří, kontrolovat. Osoba, která navštíví stránku, pak může zaškrtnout nebo zrušit zaškrtnutí políček a přidat nebo odebrat vybraného uživatele z odpovídajících rolí.

> [!NOTE]
> Použití rozevíracího seznamu pro výpis uživatelských účtů není ideální volbou pro weby, kde můžou existovat stovky uživatelských účtů. Rozevírací seznam je navržený tak, aby uživateli umožnil vybrat jednu položku z relativně krátkého seznamu možností. Rychle se nepraktický, jak se rozroste počet položek seznamu. Pokud vytváříte web, který bude mít potenciálně velký počet uživatelských účtů, můžete zvážit použití alternativního uživatelského rozhraní, například stránkového prvku GridView nebo filtrovacího rozhraní, které seznam vyzve návštěvníka k výběru písmena a pak pouze Zobrazuje uživatele, jejichž uživatelské jméno začíná zvoleným písmenem.

## <a name="step-1-building-the-by-user-user-interface"></a>Krok 1: vytvoření uživatelského rozhraní "podle uživatele"

Otevřete stránku `UsersAndRoles.aspx`. V horní části stránky přidejte webový ovládací prvek popisek s názvem `ActionStatus` a vymažte jeho vlastnost `Text`. Tento popisek použijeme k poskytnutí zpětné vazby k provedeným akcím, zobrazování zpráv, jako je například "uživatel tito byl přidán do role správců" nebo "uživatel Jisun byl odebrán z role Vedoucís". Aby se tyto zprávy daly vyřídit, nastavte vlastnost `CssClass` popisku na "důležité".

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample1.aspx)]

Dále přidejte následující definici třídy CSS do `Styles.css` šablony stylů:

[!code-css[Main](assigning-roles-to-users-vb/samples/sample2.css)]

Tato definice CSS dává pokyn prohlížeči k zobrazení popisku s použitím velkého červeného písma. Obrázek 1 ukazuje tento efekt prostřednictvím návrháře sady Visual Studio.

[![vlastnost CssClass popisku má za následek velké červené písmo.](assigning-roles-to-users-vb/_static/image2.png)](assigning-roles-to-users-vb/_static/image1.png)

**Obrázek 1**: vlastnost `CssClass` popisku má za následek velké červené písmo ([kliknutím zobrazíte obrázek v plné velikosti).](assigning-roles-to-users-vb/_static/image3.png)

V dalším kroku přidejte na stránku objekt DropDownList, nastavte jeho vlastnost `ID` na `UserList`a nastavte jeho vlastnost `AutoPostBack` na hodnotu true. Tuto sadu DropDownList použijeme k vypsání všech uživatelů v systému. Tato DropDownList bude svázána s kolekcí objektů MembershipUser. Vzhledem k tomu, že chceme, aby vlastnost DropDownList zobrazovala vlastnost UserName objektu MembershipUser (a použila ji jako hodnotu položky seznamu), nastavte vlastnosti ovládacího prvku DropDownList `DataTextField` a `DataValueField` na "UserName".

Pod ovládacím prvkem DropDownList přidejte Repeater s názvem `UsersRoleList`. Tento Repeater zobrazí seznam všech rolí v systému jako řadu zaškrtávacích políček. Pomocí následujících deklarativních značek definujte `ItemTemplate` opakovače:

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample3.aspx)]

Kód `ItemTemplate` obsahuje ovládací prvek webového ovládacího prvku CheckBox s názvem `RoleCheckBox`. Vlastnost `AutoPostBack` zaškrtávacího políčka je nastavena na hodnotu true a vlastnost `Text` je svázána s `Container.DataItem`. Důvodem je, že syntaxe datové vazby je jednoduše `Container.DataItem` je, že rozhraní Framework vrátí seznam názvů rolí jako pole řetězců a toto pole řetězců, které budeme svázat s Repeat. Podrobný popis, proč se tato syntaxe používá k zobrazení obsahu pole vázaného k datovému ovládacímu prvku webového ovládacího prvku, je nad rámec tohoto kurzu. Další informace o této problematice naleznete v tématu [vazba skalárního pole na datově datovou webovou ovládací prvek](http://aspnet.4guysfromrolla.com/articles/082504-1.aspx).

V tomto okamžiku by deklarativní označení "podle uživatele" mělo vypadat podobně jako následující:

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample4.aspx)]

Nyní jsme připraveni zapsat kód pro svázání sady uživatelských účtů s ovládacím prvkem DropDownList a sadou rolí pro Repeater. Do třídy kódu na pozadí stránky přidejte metodu s názvem `BindUsersToUserList` a jinou pojmenovanou `BindRolesList`pomocí následujícího kódu:

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample5.vb)]

Metoda `BindUsersToUserList` načte všechny uživatelské účty v systému prostřednictvím [metody`Membership.GetAllUsers`](https://msdn.microsoft.com/library/dy8swhya.aspx). Tím se vrátí [objekt`MembershipUserCollection`](https://msdn.microsoft.com/library/system.web.security.membershipusercollection.aspx), což je kolekce [instancí`MembershipUser`](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx). Tato kolekce je pak svázána s `UserList` DropDownList. Instance `MembershipUser`, které strukturu kolekci obsahují různé vlastnosti, například `UserName`, `Email`, `CreationDate`a `IsOnline`. Aby vlastnost DropDownList mohla zobrazit hodnotu vlastnosti `UserName`, zajistěte, aby byly vlastnosti `DataTextField` a `DataValueField` `UserList` DropDownList nastavené na UserName.

> [!NOTE]
> Metoda `Membership.GetAllUsers` má dvě přetížení: jednu, která nepřijímá žádné vstupní parametry, vrátí všechny uživatele a jednu, která má celočíselné hodnoty pro index stránky a velikost stránky, a vrátí pouze zadanou podmnožinu uživatelů. V případě, že je v prvku uživatelského rozhraní stránkovaného prvku zobrazeno velké množství uživatelských účtů, lze druhé přetížení použít k efektivnějšímu stránkování uživatelů, protože vrátí pouze přesné podmnožiny uživatelských účtů, nikoli všechny.

Metoda `BindRolesToList` začíná voláním [metody`GetAllRoles`](https://msdn.microsoft.com/library/system.web.security.roles.getallroles.aspx)`Roles` třídy, která vrací pole řetězců obsahující role v systému. Toto pole řetězců je pak svázáno s argumentem Repeater.

Nakonec musíme při prvním načtení stránky zavolat tyto dvě metody. Do obslužné rutiny události `Page_Load` přidejte následující kód:

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample6.vb)]

V případě tohoto kódu si chvíli počkejte, než se stránka navštíví přes prohlížeč. vaše obrazovka by měla vypadat podobně jako na obrázku 2. V rozevíracím seznamu se naplní všechny uživatelské účty a pod ní se zobrazí Každá role jako zaškrtávací políčko. Vzhledem k tomu, že jsme nastavili `AutoPostBack` vlastnosti ovládacího prvku DropDownList a zaškrtávací políčka na hodnotu true, změna vybraného uživatele nebo zaškrtnutí nebo zrušení kontroly role způsobí postback. Neprovádí se ale žádná akce, protože ještě máme psát kód pro zpracování těchto akcí. Tyto úlohy budeme řešit v následujících dvou částech.

[![stránce se zobrazí uživatelé a role.](assigning-roles-to-users-vb/_static/image5.png)](assigning-roles-to-users-vb/_static/image4.png)

**Obrázek 2**: stránka zobrazuje uživatele a role ([kliknutím zobrazíte obrázek v plné velikosti).](assigning-roles-to-users-vb/_static/image6.png)

### <a name="checking-the-roles-the-selected-user-belongs-to"></a>Kontrola rolí, do kterých vybraný uživatel patří

Při prvním načtení stránky nebo pokaždé, když návštěvník vybere nového uživatele v rozevíracím seznamu, musíme aktualizovat zaškrtávací políčka `UsersRoleList`tak, aby se dané zaškrtávací políčko role kontrolovalo pouze v případě, že vybraný uživatel patří do této role. K tomu je potřeba vytvořit metodu s názvem `CheckRolesForSelectedUser` s následujícím kódem:

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample7.vb)]

Výše uvedený kód začíná určením, kdo má vybraný uživatel. Pak pomocí [metody`GetRolesForUser(userName)`](https://msdn.microsoft.com/library/system.web.security.roles.getrolesforuser.aspx) třídy role vrátí sadu rolí zadaného uživatele jako pole řetězců. V dalším kroku jsou vyhodnoceny položky Repeater a na `RoleCheckBox` je programově odkazováno zaškrtávací políčko pro každou položku. Zaškrtávací políčko je zaškrtnuto pouze v případě, že je role, ke které odpovídá, obsažena v poli `selectedUsersRoles` řetězců.

> [!NOTE]
> Pokud používáte ASP.NET verze 2,0, nebude zkompilována syntaxe `Linq.Enumerable.Contains(Of String)(...)`. Metoda `Contains(Of String)` je součástí [knihovny LINQ](http://en.wikipedia.org/wiki/Language_Integrated_Query), která je v ASP.NET 3,5 novinkou. Pokud stále používáte verzi ASP.NET 2,0, použijte místo toho [metodu`Array.IndexOf(Of String)`](https://msdn.microsoft.com/library/eha9t187.aspx) .

Metoda `CheckRolesForSelectedUser` musí být volána ve dvou případech: při prvním načtení stránky a pokaždé, když se změní vybraný index `UserList` DropDownList. Proto volejte tuto metodu z obslužné rutiny události `Page_Load` (po volání `BindUsersToUserList` a `BindRolesToList`). Také vytvořte obslužnou rutinu události pro událost `SelectedIndexChanged` ovládacího prvku DropDownList a zavolejte tuto metodu odtud.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample8.vb)]

S tímto kódem můžete stránku otestovat přes prohlížeč. Vzhledem k tomu, že na stránce `UsersAndRoles.aspx` aktuálně chybí možnost přiřadit uživatele k rolím, žádní uživatelé nemají role. Vytvoříme rozhraní pro přiřazení uživatelů k rolím v okamžiku, takže můžete vzít slovo, že tento kód funguje, a ověřit, že je to později, nebo můžete ručně přidat uživatele k rolím tak, že do tabulky `aspnet_UsersInRoles` vložíte záznamy, abyste mohli tuto funkci nyní otestovat.

### <a name="assigning-and-removing-users-from-roles"></a>Přiřazení a odebrání uživatelů z rolí

Když návštěvník zkontroluje nebo vrátí zaškrtávací políčko v `UsersRoleList` Repeater, musíme přidat nebo odebrat vybraného uživatele z odpovídající role. Vlastnost `AutoPostBack` CheckBox je aktuálně nastavená na hodnotu true, což způsobí, že se v případě, že je zaškrtnuto nebo není zaškrtnuté zaškrtávací políčko v rámci tohoto opakovače. V krátkém případě musíme pro událost `CheckChanged` CheckBox vytvořit obslužnou rutinu události. Vzhledem k tomu, že je zaškrtávací políčko v ovládacím prvku Repeater, musíme přidat ruční vložení obslužné rutiny události. Začněte přidáním obslužné rutiny události do třídy kódu na pozadí jako metody `Protected`, například takto:

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample9.vb)]

Za chvíli se vrátíme k zápisu kódu pro tuto obslužnou rutinu události. Nejdřív ale Pojďme dokončit práci s zpracováním událostí. Z zaškrtávacího políčka `ItemTemplate`v rámci tohoto opakovače přidejte `OnCheckedChanged="RoleCheckBox_CheckChanged"`. Tato syntaxe spoludrátuje obslužnou rutinu události `RoleCheckBox_CheckChanged` `RoleCheckBox`události `CheckedChanged`.

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample10.aspx)]

Náš konečný úkol je dokončit obslužnou rutinu události `RoleCheckBox_CheckChanged`. Musíme začít odkazem na ovládací prvek CheckBox, který událost vyvolal, protože tato instance CheckBox oznamuje, jaká role byla zaškrtnutoa nebo nezkontrolována prostřednictvím jejího `Text` a `Checked` vlastností. Pomocí těchto informací spolu s uživatelským jménem vybraného uživatele přidáme nebo odeberete uživatele z role prostřednictvím metody [`AddUserToRole`](https://msdn.microsoft.com/library/system.web.security.roles.addusertorole.aspx) nebo [`RemoveUserFromRole`](https://msdn.microsoft.com/library/system.web.security.roles.removeuserfromrole.aspx)třídy `Roles`.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample11.vb)]

Výše uvedený kód začíná programově odkazující na zaškrtávací políčko, které vyvolalo událost, která je k dispozici prostřednictvím vstupního parametru `sender`. Pokud je zaškrtnuté políčko, vybraný uživatel se přidá do zadané role, jinak se z role odeberou. V obou případech `ActionStatus` popisek zobrazí zprávu, která shrnuje právě prováděnou akci.

Vyzkoušejte si chvilku, abyste tuto stránku otestovali přes prohlížeč. Vyberte tito uživatele a pak přidejte tito do rolí Administrators a Administrators.

[k rolím správců a vedoucích se přidala ![tito.](assigning-roles-to-users-vb/_static/image8.png)](assigning-roles-to-users-vb/_static/image7.png)

**Obrázek 3**: tito bylo přidáno do rolí Správci a vedoucí ([kliknutím zobrazíte obrázek v plné velikosti).](assigning-roles-to-users-vb/_static/image9.png)

V dalším kroku vyberte v rozevíracím seznamu možnost uživatel Bruce. Je k dispozici postback a zaškrtávací políčka pro opakování jsou aktualizována prostřednictvím `CheckRolesForSelectedUser`. Vzhledem k tomu, že Bruce ještě nepatří do žádné role, nejsou tato dvě zaškrtávací políčka zaškrtnutá. V dalším kroku přidejte Bruce do role Nadřízenýs.

[do role Nadřízený byl přidán ![Bruce](assigning-roles-to-users-vb/_static/image11.png)](assigning-roles-to-users-vb/_static/image10.png)

**Obrázek 4**: Bruce bylo přidáno do role Nadřízený ([kliknutím zobrazíte obrázek v plné velikosti](assigning-roles-to-users-vb/_static/image12.png)).

Chcete-li dále ověřit funkčnost metody `CheckRolesForSelectedUser`, vyberte uživatele, který není tito nebo Bruce. Všimněte si, že zaškrtávací políčka jsou automaticky nezaškrtnutá a zjišťují, že nepatří do žádné role. Vraťte se na tito. Měla by být zaškrtnutá políčka správci i vedoucí.

## <a name="step-2-building-the-by-roles-user-interface"></a>Krok 2: sestavování uživatelského rozhraní "podle rolí"

V tuto chvíli jsme dokončili rozhraní "podle uživatelů" a připraveni začít řešit rozhraní "podle rolí". Rozhraní "podle rolí" vyzve uživatele k výběru role z rozevíracího seznamu a poté zobrazí skupinu uživatelů, kteří patří do této role v prvku GridView.

Přidejte do `UsersAndRoles.aspx page`další ovládací prvek DropDownList. Umístěte ho pod ovládací prvek Repeater, pojmenujte ho `RoleList`a nastavte jeho vlastnost `AutoPostBack` na hodnotu true. Pod tím přidejte prvek GridView a pojmenujte jej `RolesUserList`. Tento prvek GridView zobrazí seznam uživatelů, kteří patří do vybrané role. Nastavte vlastnost `AutoGenerateColumns` prvku GridView na hodnotu false, do kolekce `Columns` mřížky přidejte TemplateField a nastavte její vlastnost `HeaderText` na "uživatelé". Definujte `ItemTemplate` TemplateField, aby se zobrazila hodnota výrazu DataBinding `Container.DataItem` ve vlastnosti `Text` popisku s názvem `UserNameLabel`.

Po přidání a konfiguraci prvku GridView by deklarativní označení "podle role" mělo vypadat podobně jako následující:

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample12.aspx)]

Musíme `RoleList` DropDownList naplnit sadou rolí v systému. Chcete-li toho dosáhnout, aktualizujte metodu `BindRolesToList` tak, že je svázáno pole řetězců vrácené metodou `Roles.GetAllRoles` do `RolesList` DropDownList (a také `UsersRoleList` Repeater).

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample13.vb)]

Poslední dva řádky v metodě `BindRolesToList` byly přidány pro svázání sady rolí k ovládacímu prvku `RoleList` DropDownList. Obrázek 5 zobrazuje konečný výsledek při zobrazení v prohlížeči – rozevírací seznam vyplněný rolemi systému.

[![rolí se zobrazují v RoleList DropDownList](assigning-roles-to-users-vb/_static/image14.png)](assigning-roles-to-users-vb/_static/image13.png)

**Obrázek 5**: role se zobrazují v `RoleList` DropDownList ([kliknutím zobrazíte obrázek v plné velikosti).](assigning-roles-to-users-vb/_static/image15.png)

### <a name="displaying-the-users-that-belong-to-the-selected-role"></a>Zobrazují se uživatelé, kteří patří do vybrané role.

Při prvním načtení stránky nebo při výběru nové role z `RoleList` DropDownList musíme zobrazit seznam uživatelů, kteří patří do této role v prvku GridView. Pomocí následujícího kódu vytvořte metodu s názvem `DisplayUsersBelongingToRole`:

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample14.vb)]

Tato metoda začíná získáním vybrané role z `RoleList` DropDownList. Poté pomocí [metody`Roles.GetUsersInRole(roleName)`](https://msdn.microsoft.com/library/system.web.security.roles.getusersinrole.aspx) načte pole řetězců uživatelských jmen uživatelů, kteří patří do této role. Toto pole je pak svázáno s `RolesUserList` GridView.

Tato metoda musí být volána za dvou okolností: při počátečním načtení stránky a při změně vybrané role v `RoleList` DropDownList. Proto aktualizujte obslužnou rutinu události `Page_Load` tak, aby se tato metoda vyvolala po volání `CheckRolesForSelectedUser`. Dále vytvořte obslužnou rutinu události pro událost `SelectedIndexChanged` `RoleList`a zavolejte tuto metodu i tam.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample15.vb)]

Když je tento kód na místě, `RolesUserList` GridView by měl zobrazit uživatele, kteří patří do vybrané role. Jak ukazuje obrázek 6, role správce se skládá ze dvou členů: Bruce a tito.

[![v prvku GridView zobrazí seznam uživatelů, kteří patří do vybrané role.](assigning-roles-to-users-vb/_static/image17.png)](assigning-roles-to-users-vb/_static/image16.png)

**Obrázek 6**: v ovládacím prvku GridView zobrazí seznam uživatelů, kteří patří do vybrané role ([kliknutím zobrazíte obrázek v plné velikosti).](assigning-roles-to-users-vb/_static/image18.png)

### <a name="removing-users-from-the-selected-role"></a>Odebírají se uživatelé z vybrané role.

Pojďme rozšířit `RolesUserList` GridView tak, aby obsahovala sloupec tlačítek Remove (odebrat). Kliknutím na tlačítko odebrat pro určitého uživatele je z této role odeberete.

Začněte přidáním pole tlačítko pro odstranění do prvku GridView. Zajistěte, aby se toto pole zobrazovalo jako levé a aby se změnila jeho vlastnost `DeleteText`a z "odstranit" (výchozí) na "Remove".

[![přidat](assigning-roles-to-users-vb/_static/image20.png)](assigning-roles-to-users-vb/_static/image19.png)

**Obrázek 7**: Přidání tlačítka "odebrat" do prvku GridView ([kliknutím zobrazíte obrázek v plné velikosti](assigning-roles-to-users-vb/_static/image21.png))

Po kliknutí na tlačítko "odebrat" v důsledku postbacku dojde k vyvolání události `RowDeleting` ovládacího prvku GridView. Pro tuto událost musíme vytvořit obslužnou rutinu události a napsat kód, který odebere uživatele z vybrané role. Vytvořte obslužnou rutinu události a přidejte následující kód:

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample16.vb)]

Kód začíná určením zvoleného názvu role. Potom programově odkazuje na ovládací prvek `UserNameLabel` z řádku, u kterého bylo tlačítko "odebrat" kliknuto, aby bylo možné určit uživatelské jméno uživatele, který má být odebrán. Uživatel je pak odebrán z role prostřednictvím volání metody `Roles.RemoveUserFromRole`. `RolesUserList` prvek GridView se pak aktualizuje a zobrazí se zpráva prostřednictvím ovládacího prvku popisek `ActionStatus`.

> [!NOTE]
> Tlačítko Odebrat nevyžaduje před odebráním uživatele z této role žádné potvrzení od uživatele. Beru na schůzku, abyste přidali určitou úroveň potvrzení uživatele. Jedním z nejjednodušších způsobů, jak potvrdit akci, je použít dialogové okno pro potvrzení na straně klienta. Další informace o tomto postupu najdete v tématu [Přidání potvrzení na straně klienta při odstraňování](https://asp.net/learn/data-access/tutorial-42-vb.aspx).

Obrázek 8 ukazuje stránku po odebrání uživatele tito ze skupiny vedoucích.

[![Alas, tito už není správce.](assigning-roles-to-users-vb/_static/image23.png)](assigning-roles-to-users-vb/_static/image22.png)

**Obrázek 8**: Alas, tito již není správce ([kliknutím zobrazíte obrázek v plné velikosti](assigning-roles-to-users-vb/_static/image24.png)).

### <a name="adding-new-users-to-the-selected-role"></a>Přidávání nových uživatelů do vybrané role

Společně s odebráním uživatelů z vybrané role by měl být návštěvník této stránky také schopný přidat uživatele do vybrané role. Nejlepší rozhraní pro přidání uživatele k vybrané roli závisí na počtu uživatelských účtů, které očekáváte. Pokud bude váš web obsahovat jenom pár desítek uživatelských účtů nebo méně, můžete tady použít DropDownList. Pokud se může jednat o tisíce uživatelských účtů, měli byste zahrnout uživatelské rozhraní, které návštěvníkovi umožní stránkovat prostřednictvím účtů, vyhledat konkrétní účet nebo filtrovat uživatelské účty jiným způsobem.

Pro tuto stránku můžeme použít velmi jednoduché rozhraní, které funguje bez ohledu na počet uživatelských účtů v systému. Konkrétně použijeme textové pole, které vyzve návštěvníka k zadání uživatelského jména uživatele, který chce přidat do vybrané role. Pokud už žádný uživatel s tímto názvem neexistuje nebo pokud je uživatel členem této role, zobrazí se ve `ActionStatus` popisku zpráva. Pokud ale uživatel existuje a není členem této role, přidáme je do role a aktualizujeme mřížku.

Přidejte textové pole a tlačítko pod prvek GridView. Nastavte `ID` textového pole na `UserNameToAddToRole` a nastavte vlastnosti `ID` a `Text` vlastností na `AddUserToRoleButton` a přidat uživatele do role (v uvedeném pořadí).

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample17.aspx)]

Dále vytvořte obslužnou rutinu události `Click` pro `AddUserToRoleButton` a přidejte následující kód:

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample18.vb)]

Většina kódu v obslužné rutině události `Click` provádí různé kontroly ověřování. Zajišťuje, že návštěvník zadal uživatelské jméno v `UserNameToAddToRole`m textovém poli, že uživatel existuje v systému a že ještě nepatří do vybrané role. Pokud některá z těchto kontrol neproběhne úspěšně, zobrazí se v `ActionStatus` příslušná zpráva a obslužná rutina události se ukončí. Pokud všechny kontroly projde, uživatel se do role přidá prostřednictvím metody `Roles.AddUserToRole`. Za tímto účelem je vlastnost `Text` textového pole vymazána, prvek GridView se aktualizuje a `ActionStatus` popisek zobrazí zprávu oznamující, že zadaný uživatel byl úspěšně přidán do vybrané role.

> [!NOTE]
> Pro zajištění, že zadaný uživatel ještě nepatří do vybrané role, používáme [metodu`Roles.IsUserInRole(userName, roleName)`](https://msdn.microsoft.com/library/system.web.security.roles.isuserinrole.aspx), která vrací logickou hodnotu, která označuje, jestli je *uživatelské jméno* členem *roleName*. Tuto metodu použijeme znovu v <a id="_msoanchor_2"> </a> [dalším kurzu](role-based-authorization-vb.md) , když se podíváme na autorizaci založenou na rolích.

Navštivte stránku pomocí prohlížeče a vyberte roli vedoucí z `RoleList` DropDownList. Zkuste zadat neplatné uživatelské jméno – zobrazí se zpráva s vysvětlením, že uživatel v systému neexistuje.

[![nemůžete do role přidat neexistujícího uživatele](assigning-roles-to-users-vb/_static/image26.png)](assigning-roles-to-users-vb/_static/image25.png)

**Obrázek 9**: do role nemůžete přidat neexistujícího uživatele ([kliknutím zobrazíte obrázek v plné velikosti](assigning-roles-to-users-vb/_static/image27.png)).

Teď zkuste přidat platného uživatele. Pokračujte a znovu přidejte tito do role vedoucí.

[![tito je znovu vedoucí!](assigning-roles-to-users-vb/_static/image29.png)](assigning-roles-to-users-vb/_static/image28.png)

**Obrázek 10**: tito je potom znovu vedoucí!  ([Kliknutím zobrazíte obrázek v plné velikosti.](assigning-roles-to-users-vb/_static/image30.png))

## <a name="step-3-cross-updating-the-by-user-and-by-role-interfaces"></a>Krok 3: Křížová aktualizace rozhraní "podle uživatele" a "podle role"

Stránka `UsersAndRoles.aspx` nabízí dvě odlišná rozhraní pro správu uživatelů a rolí. V současné době tato dvě rozhraní pracují nezávisle na sobě, takže je možné, že se změny provedené v jednom rozhraní neprojeví okamžitě. Představte si například, že návštěvník na stránku vybere roli Nadřízenýs z `RoleList` DropDownList, která jako své členy vypíše seznam Bruce a tito. V dalším kroku návštěvník vybere tito z `UserList` DropDownList, který kontroluje zaškrtnutí políček správci a vedoucí v `UsersRoleList`m OPAKOVAČI. Pokud návštěvník pak zrušit kontrolu role správce od tohoto opakovače, tito se odebere z role Nadřízený, ale tato úprava se neprojeví v rozhraní "by role". Prvek GridView bude stále zobrazovat tito jako člen role Nadřízenýs.

Chcete-li tento problém vyřešit, je nutné aktualizovat prvek GridView vždy, když je role zaškrtnuta nebo není zkontrolována z `UsersRoleList`ho opakovače. Podobně je potřeba aktualizovat Repeater vždy, když se uživatel odebere nebo přidá do role z rozhraní "podle role".

Opakovač v rozhraní "by uživatel" se aktualizuje voláním metody `CheckRolesForSelectedUser`. Rozhraní "by role" lze upravit v obslužné rutině události `RowDeleting` prvku GridView `RolesUserList` a obslužné rutiny události `Click` tlačítka `AddUserToRoleButton`. Proto je nutné volat metodu `CheckRolesForSelectedUser` od každé z těchto metod.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample19.vb)]

Podobně se ovládací prvek GridView v rozhraní "by role" aktualizuje voláním metody `DisplayUsersBelongingToRole` a rozhraní "podle uživatele" je změněno prostřednictvím obslužné rutiny události `RoleCheckBox_CheckChanged`. Proto je nutné volat metodu `DisplayUsersBelongingToRole` z této obslužné rutiny události.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample20.vb)]

U těchto vedlejších změn kódu jsou nyní správně vzájemně aktualizovány rozhraní "podle uživatele" a "podle rolí". Pokud to chcete ověřit, přejděte na stránku pomocí prohlížeče a vyberte tito a vedoucí z `UserList` a `RoleList` DropDownLists (v uvedeném pořadí). Všimněte si, že když zrušíte kontrolu role dohlížitelé pro tito z opakovače v rozhraní "by uživatel", tito se automaticky odebere z prvku GridView v rozhraní "by role". Přidání tito zpět do role dohlížitelé z rozhraní "by role" automaticky znovu kontroluje zaškrtnutí políčka vedoucí v rozhraní "podle uživatele".

## <a name="step-4-customizing-the-createuserwizard-to-include-a-specify-roles-step"></a>Krok 4: přizpůsobení ovládacím CreateUserWizard tak, aby zahrnovalo krok "zadání rolí"

<a id="_msoanchor_3"> </a>V kurzu [*vytváření uživatelských účtů*](../membership/creating-user-accounts-vb.md) jsme zjistili, jak pomocí webového ovládacího prvku ovládacím CreateUserWizard poskytnout rozhraní pro vytvoření nového uživatelského účtu. Ovládací prvek ovládacím CreateUserWizard lze použít jedním ze dvou způsobů:

- Jako prostředek pro návštěvníky vytvořit vlastní uživatelský účet na webu a
- Jako prostředek pro správce vytváření nových účtů

V prvním případu použití návštěvník dostane na web a vyplní ovládacím CreateUserWizard a zadá své informace, aby se mohl zaregistrovat na webu. Ve druhém případě správce vytvoří nový účet pro jinou osobu.

Když je účet vytvořen správcem nějaké jiné osoby, může být užitečné, aby správce mohl určit, k jakým rolím nový uživatelský účet patří. <a id="_msoanchor_4"> </a>V kurzu [ *ukládání* *dalších informací o uživatelích* ](../membership/storing-additional-user-information-vb.md) jsme viděli, jak přizpůsobit ovládacím CreateUserWizard přidáním dalších `WizardSteps`. Pojďme se podívat na to, jak do ovládacím CreateUserWizard přidat další krok, abyste mohli zadat role nového uživatele.

Otevřete stránku `CreateUserWizardWithRoles.aspx` a přidejte ovládací prvek ovládacím CreateUserWizard s názvem `RegisterUserWithRoles`. Nastavte vlastnost `ContinueDestinationPageUrl` ovládacího prvku na ~/Default.aspx. Vzhledem k tomu, že tady je, že správce bude používat tento ovládací prvek ovládacím CreateUserWizard k vytváření nových uživatelských účtů, nastavte vlastnost `LoginCreatedUser` ovládacího prvku na hodnotu false. Tato vlastnost `LoginCreatedUser` určuje, zda je návštěvník automaticky přihlášen jako právě vytvořený uživatel a má výchozí hodnotu true. Nastavíme ji na false, protože když správce vytvoří nový účet, chceme ho nechat přihlášený jako sám.

V dalším kroku vyberte Přidat nebo odebrat `WizardSteps`... možnost z inteligentní značky ovládacím CreateUserWizard a přidejte novou `WizardStep`a nastavte její `ID` na `SpecifyRolesStep`. Přesuňte `SpecifyRolesStep WizardStep` tak, aby se nastavila po kroku registrace nového účtu, ale před krokem dokončení. Nastavte vlastnost `Title` `WizardStep`na zadat role, vlastnost `StepType` na `Step`a vlastnost `AllowReturn` na hodnotu false.

[![přidat](assigning-roles-to-users-vb/_static/image32.png)](assigning-roles-to-users-vb/_static/image31.png)

**Obrázek 11**: přidejte `WizardStep` "zadat role" do ovládacím CreateUserWizard ([kliknutím zobrazíte obrázek v plné velikosti).](assigning-roles-to-users-vb/_static/image33.png)

Po této změně by deklarativní označení ovládacím CreateUserWizard mělo vypadat takto:

[!code-aspx[Main](assigning-roles-to-users-vb/samples/sample21.aspx)]

V `WizardStep`zadejte role, přidejte CheckBoxList s názvem `RoleList.` Tato funkce CheckBoxList zobrazí seznam dostupných rolí a umožní osobě navštěvovat tuto stránku, aby zkontrolovala, k jakým rolím patří nově vytvořený uživatel.

Jsme opustili dvě úlohy kódování: Nejdřív je potřeba naplnit `RoleList` CheckBoxList pomocí rolí v systému. za druhé, musíme přidat vytvořeného uživatele k vybraným rolím, když se uživatel přesune z kroku "zadat role" do kroku "dokončeno". V obslužné rutině události `Page_Load` můžeme provést první úlohu. Následující kód programově odkazuje na zaškrtávací políčko `RoleList` na první návštěvě stránky a vytvoří z něj role v systému.

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample22.vb)]

Výše uvedený kód by měl vypadat dobře. <a id="_msoanchor_5"> </a>V kurzu [ *ukládání* *dalších informací o uživateli* ](../membership/storing-additional-user-information-vb.md) jsme použili dva příkazy `FindControl` pro odkazování na webový ovládací prvek z vlastního `WizardStep`. A kód, který váže role k CheckBoxList, byl získán z výše v tomto kurzu.

Aby bylo možné provést druhý programovací úkol, musíme po dokončení kroku "zadání rolí" informovat. Odvolání, že ovládacím CreateUserWizard má událost `ActiveStepChanged`, která se aktivuje při každém přechodu návštěvníka z jednoho kroku na druhý. Tady můžeme určit, jestli uživatel dosáhl kroku "dokončení"; Pokud ano, musíme přidat uživatele k vybraným rolím.

Vytvořte obslužnou rutinu události pro událost `ActiveStepChanged` a přidejte následující kód:

[!code-vb[Main](assigning-roles-to-users-vb/samples/sample23.vb)]

Pokud uživatel právě dosáhl kroku "dokončeno", obslužná rutina události zobrazí výčet položek `RoleList` CheckBoxList a právě vytvořeného uživatele je přiřazeno k vybraným rolím.

Navštivte tuto stránku v prohlížeči. Prvním krokem v ovládacím CreateUserWizard je standardní krok zaregistrovat se k novému účtu, který vyzývá k zadání uživatelského jména, hesla, e-mailu a dalších klíčových informací nového uživatele. Zadejte informace pro vytvoření nového uživatele s názvem Wanda.

[![vytvořit nového uživatele s názvem Wanda](assigning-roles-to-users-vb/_static/image35.png)](assigning-roles-to-users-vb/_static/image34.png)

**Obrázek 12**: vytvoření nového uživatele s názvem Wanda ([kliknutím zobrazíte obrázek v plné velikosti](assigning-roles-to-users-vb/_static/image36.png))

Klikněte na tlačítko vytvořit uživatele. Ovládacím CreateUserWizard interně volá metodu `Membership.CreateUser`, vytváří nový uživatelský účet a následně postupuje k dalšímu kroku, "zadání rolí". Tady jsou uvedené systémové role. Zaškrtněte políčko vedoucí a klikněte na další.

[![Wanda členství v roli správce](assigning-roles-to-users-vb/_static/image38.png)](assigning-roles-to-users-vb/_static/image37.png)

**Obrázek 13**: vytvoření Wanda člena role Nadřízený ([kliknutím zobrazíte obrázek v plné velikosti](assigning-roles-to-users-vb/_static/image39.png))

Kliknutím na tlačítko Další dojde k postbacku a aktualizace `ActiveStep` na "dokončený" krok. V obslužné rutině události `ActiveStepChanged` je nedávno vytvořený uživatelský účet přiřazen k roli Nadřízenýs. Pokud to chcete ověřit, vraťte se na stránku `UsersAndRoles.aspx` a vyberte Správce z `RoleList` DropDownList. Jak ukazuje obrázek 14, dohlížitelé se teď skládají ze tří uživatelů: Bruce, tito a Wanda.

[Všechny správce ![Bruce, tito a Wanda](assigning-roles-to-users-vb/_static/image41.png)](assigning-roles-to-users-vb/_static/image40.png)

**Obrázek 14**: Bruce, tito a Wanda jsou všichni vedoucí ([kliknutím zobrazíte obrázek v plné velikosti](assigning-roles-to-users-vb/_static/image42.png)).

## <a name="summary"></a>Přehled

Rozhraní role nabízí metody pro načítání informací o rolích a metodách konkrétního uživatele k určení toho, co uživatelé patří do zadané role. Kromě toho existuje několik způsobů, jak přidat a odebrat jednoho nebo více uživatelů k jedné nebo více rolím. V tomto kurzu se zaměřujeme jenom na dvě z těchto metod: `AddUserToRole` a `RemoveUserFromRole`. Existují další varianty navržené pro přidání více uživatelů k jedné roli a přiřazení více rolí jednomu uživateli.

Tento kurz také obsahuje přehled o rozšíření ovládacího prvku ovládacím CreateUserWizard, který obsahuje `WizardStep` k určení rolí nově vytvořeného uživatele. Tento krok může správcům přispět k zjednodušení procesu vytváření uživatelských účtů pro nové uživatele.

V tuto chvíli jsme viděli, jak vytvořit a odstranit role a jak přidávat a odebírat uživatele z rolí. Ale zatím jsme se vyhledali při použití autorizace na základě rolí. <a id="_msoanchor_6"> </a>V [následujícím kurzu](role-based-authorization-vb.md) se podíváme na definování autorizačních pravidel URL pro role na základě rolí a také omezení funkcí na úrovni stránek na základě rolí aktuálně přihlášeného uživatele.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Přehled nástroje pro správu webu ASP.NET](https://msdn.microsoft.com/library/ms228053.aspx)
- [Prozkoumává se ASP. Členství v síti, role a profil](http://aspnet.4guysfromrolla.com/articles/120705-1.aspx)
- [Postup při zavedení vlastního nástroje pro správu webu](http://aspnet.4guysfromrolla.com/articles/052307-1.aspx)

### <a name="about-the-author"></a>O autorovi

Scott Mitchell, autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je *[Sams naučit se ASP.NET 2,0 za 24 hodin](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* . Scott se dá kontaktovat [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky...

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Kontrolor pro tento kurz byl Teresa Murphy. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [Předchozí](creating-and-managing-roles-vb.md)
> [Další](role-based-authorization-vb.md)

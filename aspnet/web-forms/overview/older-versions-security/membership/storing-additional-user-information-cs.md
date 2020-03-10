---
uid: web-forms/overview/older-versions-security/membership/storing-additional-user-information-cs
title: Ukládají se další informace oC#uživateli () | Microsoft Docs
author: rick-anderson
description: V tomto kurzu odpovíme na tuto otázku vytvořením velmi základní aplikace v knize webkniha. V takovém případě se podíváme na různé možnosti modelu...
ms.author: riande
ms.date: 01/18/2008
ms.assetid: 1642132a-1ca5-4872-983f-ab59fc8865d3
msc.legacyurl: /web-forms/overview/older-versions-security/membership/storing-additional-user-information-cs
msc.type: authoredcontent
ms.openlocfilehash: 24b96e86bc93e03d2639b73e35ed1fd1271bac5a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634867"
---
# <a name="storing-additional-user-information-c"></a>Ukládání dalších informací o uživatelích (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/ASPNET_Security_Tutorial_08_CS.zip) nebo [stažení PDF](https://download.microsoft.com/download/3/f/5/3f5a8605-c526-4b34-b3fd-a34167117633/aspnet_tutorial08_ExtraUserInfo_cs.pdf)

> V tomto kurzu odpovíme na tuto otázku vytvořením velmi základní aplikace v knize webkniha. V takovém případě se podíváme na různé možnosti pro modelování informací o uživatelích v databázi a potom se dozvíte, jak tyto údaje přidružit k uživatelským účtům vytvořeným pomocí architektury členství.

## <a name="introduction"></a>Úvod

Formátu. Rámec členství netto nabízí flexibilní rozhraní pro správu uživatelů. Rozhraní API pro členství zahrnuje metody pro ověřování přihlašovacích údajů, načítání informací o aktuálně přihlášeném uživateli, vytváření nového uživatelského účtu a odstranění uživatelského účtu mimo jiné. Každý uživatelský účet v rozhraní členství obsahuje jenom vlastnosti potřebné k ověřování přihlašovacích údajů a provádění základních úloh souvisejících s uživatelským účtem. Toto je legitimace metodami a vlastnostmi [třídy`MembershipUser`](https://msdn.microsoft.com/library/system.web.security.membershipuser.aspx), která modeluje uživatelský účet v rozhraní členství. Tato třída má vlastnosti, jako [`UserName`](https://msdn.microsoft.com/library/system.web.security.membershipuser.username.aspx), [`Email`](https://msdn.microsoft.com/library/system.web.security.membershipuser.email.aspx)a [`IsLockedOut`](https://msdn.microsoft.com/library/system.web.security.membershipuser.islockedout.aspx), a metody jako [`GetPassword`](https://msdn.microsoft.com/library/system.web.security.membershipuser.getpassword.aspx) a [`UnlockUser`](https://msdn.microsoft.com/library/system.web.security.membershipuser.unlockuser.aspx).

Často, aplikace musí ukládat Další informace o uživateli, které nejsou zahrnuty v rámci členství v rozhraní. Maloobchodní prodejce může například potřebovat umožnit každému uživateli ukládat své dodací a fakturační adresy, platební údaje, předvolby pro doručování a kontaktní telefonní číslo. Kromě toho je každá objednávka v systému přidružena k určitému uživatelskému účtu.

Třída `MembershipUser` nezahrnuje vlastnosti, jako je `PhoneNumber` nebo `DeliveryPreferences` nebo `PastOrders`. Jak sleduji informace o uživateli, které aplikace potřebuje, a je třeba ji integrovat s rozhraním členství? V tomto kurzu odpovíme na tuto otázku vytvořením velmi základní aplikace v knize webkniha. V takovém případě se podíváme na různé možnosti pro modelování informací o uživatelích v databázi a potom se dozvíte, jak tyto údaje přidružit k uživatelským účtům vytvořeným pomocí architektury členství. Pojďme začít!

## <a name="step-1-creating-the-guestbook-applications-data-model"></a>Krok 1: vytvoření datového modelu aplikace pro knihu návštěv

Existují různé techniky, které je možné využít k zaznamenání informací o uživatelích do databáze a jejich přidružení k uživatelským účtům vytvořeným v rámci rozhraní členství. Abychom tyto techniky předvedli, musíme rozšířit výuku webové aplikace tak, aby zachytával data související s uživatelem. (V současné době datový model aplikace obsahuje pouze tabulky aplikačních služeb, které vyžaduje `SqlMembershipProvider`.)

Pojďme vytvořit velmi jednoduchou aplikaci v knize pro knihu, kde může ověřený uživatel opustit komentář. Kromě ukládání komentářů na kniha návštěv Umožníme každému uživateli ukládat jeho domovskou města, domovskou stránku a podpis. V případě potřeby se Domovská stránka, Domovská stránka a podpis uživatele zobrazí na každé zprávě, kterou opustí kniha návštěv.

### <a name="adding-theguestbookcommentstable"></a>Přidání tabulky`GuestbookComments`

Abychom mohli zachytit komentáře knihy návštěv, musíme vytvořit databázovou tabulku s názvem `GuestbookComments`, která obsahuje sloupce jako `CommentId`, `Subject`, `Body`a `CommentDate`. Také je nutné, aby každý záznam v tabulce `GuestbookComments` odkazoval na uživatele, který komentář opustil.

Chcete-li přidat tuto tabulku do naší databáze, přejděte do Průzkumníka databáze v aplikaci Visual Studio a přejděte k podrobnostem o `SecurityTutorials` databázi. Klikněte pravým tlačítkem na složku tabulky a vyberte možnost Přidat novou tabulku. Tím se zobrazí rozhraní, které nám umožňuje definovat sloupce pro novou tabulku.

[![přidat novou tabulku do databáze SecurityTutorials](storing-additional-user-information-cs/_static/image2.png)](storing-additional-user-information-cs/_static/image1.png)

**Obrázek 1**: Přidání nové tabulky do databáze `SecurityTutorials` ([kliknutím zobrazíte obrázek v plné velikosti](storing-additional-user-information-cs/_static/image3.png))

Dále definujte sloupce `GuestbookComments`. Začněte přidáním sloupce s názvem `CommentId` typu `uniqueidentifier`. V tomto sloupci se jednoznačně identifikují jednotlivé komentáře v knize webkniha, takže zakažte `NULL` s a označte ji jako primární klíč tabulky. Místo zadání hodnoty `CommentId` pole u každého `INSERT`můžeme určit, že se má pro toto `INSERT` pole automaticky vygenerovat nová hodnota `uniqueidentifier`, která nastaví výchozí hodnotu sloupce na `NEWID()`. Po přidání prvního pole, jeho označení jako primárního klíče a nastavení jeho výchozí hodnoty by měla obrazovka vypadat podobně jako snímek obrazovky, který je znázorněný na obrázku 2.

[![přidat primární sloupec s názvem CommentId](storing-additional-user-information-cs/_static/image5.png)](storing-additional-user-information-cs/_static/image4.png)

**Obrázek 2**: přidejte primární sloupec s názvem `CommentId` ([kliknutím zobrazíte obrázek v plné velikosti](storing-additional-user-information-cs/_static/image6.png)).

Dále přidejte sloupec s názvem `Subject` typu `nvarchar(50)` a sloupec s názvem `Body` typu `nvarchar(MAX)`, v obou sloupcích zakážete `NULL` s. Po přidání sloupce s názvem `CommentDate` typu `datetime`. Zakažte `NULL` s a nastavte výchozí hodnotu `CommentDate` sloupce na `getdate()`.

To vše zůstává, pokud chcete přidat sloupec, který přidruží uživatelský účet ke každému komentáři knihy. Jednou z možností je přidání sloupce s názvem `UserName` typu `nvarchar(256)`. To je vhodná volba při použití poskytovatele členství jiného než `SqlMembershipProvider`. Ale při použití `SqlMembershipProvider`, jak je v této sérii kurzů, sloupec `UserName` v tabulce `aspnet_Users` není zaručený jako jedinečný. Primární klíč `aspnet_Users` tabulky je `UserId` a je typu `uniqueidentifier`. Proto tabulka `GuestbookComments` potřebuje sloupec s názvem `UserId` typu `uniqueidentifier` (nepovoluje hodnoty `NULL`). Pokračujte a přidejte tento sloupec.

> [!NOTE]
> Jak je popsáno v tématu [*vytváření schématu členství v SQL Server*](creating-the-membership-schema-in-sql-server-cs.md) kurzu, je rozhraní členství navrženo tak, aby umožňovalo více webových aplikací s různými uživatelskými účty sdílet stejné úložiště uživatelů. Provádí rozdělení uživatelských účtů do různých aplikací. I když je každé uživatelské jméno zaručené jako jedinečné v rámci aplikace, může být stejné uživatelské jméno použito v různých aplikacích, které používají stejné uživatelské úložiště. V tabulce `aspnet_Users` v polích `UserName` a `ApplicationId` existuje omezení složené `UNIQUE`, ale ne jednu v poli `UserName`. V důsledku toho může tabulka ASPNET\_Users obsahovat dva (nebo více) záznamy se stejnou `UserName` hodnotou. V poli `UserId` tabulky `aspnet_Users` však existuje omezení `UNIQUE` (protože se jedná o primární klíč). Omezení `UNIQUE` je důležité, protože bez něj nemůžeme navázat omezení cizího klíče mezi tabulkami `GuestbookComments` a `aspnet_Users`.

Po přidání sloupce `UserId` tabulku uložte kliknutím na ikonu Uložit na panelu nástrojů. Pojmenujte novou `GuestbookComments`tabulky.

Máme poslední problém s účastí s `GuestbookComments` tabulkou: Musíme vytvořit [omezení cizího klíče](https://msdn.microsoft.com/library/ms175464.aspx) mezi sloupci `GuestbookComments.UserId` a sloupcem `aspnet_Users.UserId`. Chcete-li to dosáhnout, klikněte na ikonu vztahu na panelu nástrojů a spusťte dialogové okno relace cizího klíče. (Případně můžete toto dialogové okno spustit tak, že přejdete do nabídky Návrháře tabulky a zvolíte možnost relace.)

Klikněte na tlačítko Přidat v levém dolním rohu dialogového okna relace cizího klíče. Tím se přidá nové omezení cizího klíče, i když stále potřebujeme definovat tabulky, které se účastní vztahu.

[![pomocí dialogového okna relace cizího klíče spravovat omezení cizího klíče tabulky](storing-additional-user-information-cs/_static/image8.png)](storing-additional-user-information-cs/_static/image7.png)

**Obrázek 3**: pomocí dialogového okna relace cizího klíče můžete spravovat omezení cizího klíče tabulky ([kliknutím zobrazíte obrázek v plné velikosti).](storing-additional-user-information-cs/_static/image9.png)

V dalším kroku klikněte na ikonu elipsy v řádku specifikace tabulky a sloupců vpravo. Tím se spustí dialogové okno tabulky a sloupce, ve kterém můžeme zadat primární klíč tabulka a sloupec a sloupec cizího klíče z tabulky `GuestbookComments`. Konkrétně vyberte `aspnet_Users` a `UserId` jako tabulku a sloupec primárního klíče a `UserId` z tabulky `GuestbookComments` jako sloupec cizího klíče (viz obrázek 4). Po definování tabulek a sloupců primárního a cizího klíče klikněte na tlačítko OK, čímž se vrátíte do dialogového okna relace cizího klíče.

[![stanovit omezení cizího klíče mezi tabulkami aspnet_Users a GuesbookComments](storing-additional-user-information-cs/_static/image11.png)](storing-additional-user-information-cs/_static/image10.png)

**Obrázek 4**: stanovení omezení cizího klíče mezi tabulkami `aspnet_Users` a `GuesbookComments` ([kliknutím zobrazíte obrázek v plné velikosti](storing-additional-user-information-cs/_static/image12.png))

V tomto okamžiku bylo vytvořeno omezení cizího klíče. Přítomnost tohoto omezení zajišťuje [relační integritu](http://en.wikipedia.org/wiki/Referential_integrity) mezi dvěma tabulkami tím, že garantuje, že nikdy nebudete položkou knihy typu kniha, která odkazuje na neexistující uživatelský účet. Ve výchozím nastavení omezení cizího klíče zakáže nadřazený záznam, který se má odstranit, pokud existují odpovídající podřízené záznamy. To znamená, že pokud uživatel vytvoří jeden nebo více komentářů v knize webkniha a pokusí se tento uživatelský účet odstranit, odstranění se nepovede, pokud se nejprve neodstraní komentáře knihy návštěv.

Omezení cizího klíče lze nakonfigurovat tak, aby při odstranění nadřazeného záznamu automaticky odstranila přidružené podřízené záznamy. Jinými slovy můžeme nastavit toto omezení cizího klíče tak, aby se položky knihy návštěv uživatele automaticky odstranily, když se odstraní jeho uživatelský účet. To provedete tak, že rozbalíte část "vložení a aktualizace specifikací" a nastavíte vlastnost "Odstranit pravidlo" na hodnotu Cascade.

[![nakonfigurovat omezení cizího klíče pro kaskádová odstranění](storing-additional-user-information-cs/_static/image14.png)](storing-additional-user-information-cs/_static/image13.png)

**Obrázek 5**: Konfigurace omezení cizího klíče pro kaskádová odstranění ([kliknutím zobrazíte obrázek v plné velikosti](storing-additional-user-information-cs/_static/image15.png))

Chcete-li uložit omezení cizího klíče, klikněte na tlačítko Zavřít, čímž ukončíte relace cizího klíče. Pak klikněte na ikonu Uložit na panelu nástrojů a uložte tabulku a tuto relaci.

### <a name="storing-the-users-home-town-homepage-and-signature"></a>Ukládání domovské města, domovské stránky a podpisu uživatele

Tabulka `GuestbookComments` ukazuje, jak ukládat informace, které sdílí relaci 1:1 s uživatelskými účty. Vzhledem k tomu, že každý uživatelský účet může mít libovolný počet přidružených komentářů, je tento vztah modelován vytvořením tabulky, která bude obsahovat sadu komentářů, která obsahuje sloupec, který odkazuje na konkrétního uživatele na jednotlivé komentáře. Při použití `SqlMembershipProvider`je tento odkaz nejlépe vytvořen vytvořením sloupce s názvem `UserId` typu `uniqueidentifier` a omezením cizího klíče mezi tímto sloupcem a `aspnet_Users.UserId`.

Teď je potřeba přidružit tři sloupce každému uživatelskému účtu, aby se uložila Domovská města, Domovská stránka a podpis uživatele, který se zobrazí v jeho komentářích knihy. Existuje mnoho různých způsobů, jak to provést:

- <strong>Přidejte nové sloupce do</strong> tabulek<strong>`aspnet_Users`</strong> <strong>nebo</strong> <strong>`aspnet_Membership`</strong> <strong>.</strong> Tento přístup nedoporučujeme, protože mění schéma používané `SqlMembershipProvider`. Toto rozhodnutí se může vrátit k Haunt, že jste na cestách. Například co když budoucí verze ASP.NET používá jiné schéma `SqlMembershipProvider`. Společnost Microsoft může zahrnovat Nástroj pro migraci dat ASP.NET 2,0 `SqlMembershipProvider` do nového schématu, ale pokud jste změnili schéma ASP.NET 2,0 `SqlMembershipProvider`, takové konverzi nemusí být možné.

- **Použijte ASP. Rozhraní Profile sítě, které definuje vlastnost profilu domovské města, domovské stránky a podpisu.** ASP.NET zahrnuje profilový rámec, který je určen k ukládání dalších dat specifických pro uživatele. Podobně jako rozhraní pro členství je profil architektury sestaven základem modelem poskytovatele. .NET Framework se dodává s `SqlProfileProvider` sthat ukládá data profilu do databáze SQL Server. Ve skutečnosti má naše databáze již tabulku, kterou používá `SqlProfileProvider` (`aspnet_Profile`), jak byla přidána, když jsme přidali aplikační služby zpátky v <a id="_msoanchor_2"> </a>kurzu [*vytváření schématu členství v SQL Server*](creating-the-membership-schema-in-sql-server-cs.md) .   
  Hlavní výhodou architektury Profile je, že vývojářům umožňuje definovat vlastnosti profilu v `Web.config` – není nutné zapisovat kód pro serializaci dat profilu do a ze základního úložiště dat. V krátkém případě je neuvěřitelně snadné definovat sadu vlastností profilu a pracovat s nimi v kódu. Systém profilů však opouští hodně, který je potřeba, když se dostane do správy verzí, takže pokud máte aplikaci, kde očekáváte, že nové vlastnosti specifické pro uživatele chcete přidat později, nebo existující, které mají být odebrány nebo změněny, pak rozhraní Profile nemusí být  nejlepší možnost. Kromě toho `SqlProfileProvider` ukládá vlastnosti profilu vysoce denormalizovaný způsob, takže je možné spustit dotazy přímo proti datům profilu (například kolik uživatelů má bydliště v New York).   
  Další informace o rozhraní Profile najdete v části "Další informace" na konci tohoto kurzu.

- <strong>Přidejte tyto tři sloupce do nové tabulky v databázi a vytvořte relaci 1:1 mezi touto tabulkou a</strong> <strong>`aspnet_Users`</strong> <strong>.</strong> Tento přístup zahrnuje trochu větší práci než s profilovou architekturou, ale nabízí maximální flexibilitu při modelování dalších vlastností uživatele v databázi. Toto je možnost, kterou použijeme v tomto kurzu.

Vytvoříme novou tabulku s názvem `UserProfiles` pro uložení domovské města, domovské stránky a podpisu pro každého uživatele. Klikněte pravým tlačítkem na složku Tables (tabulky) v okně Průzkumník databáze a vyberte možnost vytvořit novou tabulku. Název prvního sloupce `UserId` a nastavte jeho typ na `uniqueidentifier`. Zakáže `NULL` hodnoty a označí sloupec jako primární klíč. Dále přidejte sloupce s názvem: `HomeTown` typu `nvarchar(50)`; `HomepageUrl` typu `nvarchar(100)`; a podpis typu `nvarchar(500)`. Každý z těchto tří sloupců může přijmout `NULL`ou hodnotu.

[![vytvoření tabulky UserProfiles](storing-additional-user-information-cs/_static/image17.png)](storing-additional-user-information-cs/_static/image16.png)

**Obrázek 6**: vytvoření tabulky `UserProfiles` ([kliknutím zobrazíte obrázek v plné velikosti](storing-additional-user-information-cs/_static/image18.png))

Uložte tabulku a pojmenujte ji `UserProfiles`. Nakonec vytvořte omezení cizího klíče mezi `UserId` poli `UserProfiles` tabulky a polem `aspnet_Users.UserId`. Vzhledem k tomu, že jsme použili omezení cizího klíče mezi tabulkami `GuestbookComments` a `aspnet_Users`, tato omezení se kaskádově odstraní. Vzhledem k tomu, že pole `UserId` v `UserProfiles` je primární klíč, zajistí to, aby v tabulce `UserProfiles` pro každý uživatelský účet nebude více než jeden záznam. Tento typ relace se označuje jako 1:1.

Teď, když máme datový model vytvořený, jsme připravení ho použít. V krocích 2 a 3 se podíváme na to, jak aktuálně přihlášený uživatel může zobrazit a upravit informace o domovské městě, domovské stránce a podpisu. V kroku 4 vytvoříme rozhraní pro ověřené uživatele, na které se budou posílat nové komentáře do knihy návštěv a zobrazovat stávající.

## <a name="step-2-displaying-the-users-home-town-homepage-and-signature"></a>Krok 2: zobrazení domovské města, domovské stránky a podpisu uživatele

Existuje řada způsobů, jak umožňuje aktuálně přihlášenému uživateli zobrazit a upravit informace o domovské městě, domovské stránce a podpisu. Mohli jsme ručně vytvořit uživatelské rozhraní s ovládacími prvky TextBox a Label nebo můžeme použít jeden z webových ovládacích prvků dat, jako je ovládací prvek DetailsView. Chcete-li provést `SELECT` databáze a `UPDATE` příkazy můžeme zapsat ADO.NET kód do třídy kódu na pozadí naší stránky nebo nebo případně použít deklarativní přístup se třídou SqlDataSource. V ideálním případě by naše aplikace obsahovala vrstvenou architekturu, kterou můžeme buď vyvolat programově z třídy kódu na pozadí stránky, nebo deklarativně prostřednictvím ovládacího prvku ObjectDataSource.

Vzhledem k tomu, že se řada kurzů zaměřuje na ověřování pomocí formulářů, autorizaci, uživatelské účty a role, nebudete mít důkladnou diskuzi o těchto různých možnostech přístupu k datům nebo proč se Vrstvená architektura upřednostňuje při přímém provádění příkazů SQL. ze stránky ASP.NET. Projdeme pomocí ovládacího prvku DetailsView a SqlDataSource – nejrychlejší a nejjednodušší možnost – ale v konceptech, které jsou popsány, je možné použít pro alternativní webové ovládací prvky a logiku přístupu k datům. Další informace o práci s daty v ASP.NET najdete v tématu věnovaném *[práci s daty v](../../data-access/index.md)* řadě kurzů pro ASP.NET 2,0.

Otevřete stránku `AdditionalUserInfo.aspx` ve složce `Membership` a přidejte na ni ovládací prvek DetailsView, nastavte jeho vlastnost `ID` na `UserProfile` a vymažte jeho `Width` a `Height` vlastnosti. Rozbalte inteligentní značku ovládacího prvku DetailsView a vyberte možnost svázání s novým ovládacím prvkem zdroje dat. Spustí se Průvodce konfigurací zdroje dat (viz obrázek 7). V prvním kroku se zobrazí výzva k zadání typu zdroje dat. Vzhledem k tomu, že se připojujete přímo k databázi `SecurityTutorials`, vyberte ikonu databáze a zadejte `ID` jako `UserProfileDataSource`.

[![přidat nový ovládací prvek SqlDataSource s názvem UserProfileDataSource](storing-additional-user-information-cs/_static/image20.png)](storing-additional-user-information-cs/_static/image19.png)

**Obrázek 7**: přidejte nový ovládací prvek SqlDataSource s názvem `UserProfileDataSource` ([kliknutím zobrazíte obrázek v plné velikosti](storing-additional-user-information-cs/_static/image21.png)).

Na další obrazovce se zobrazí výzva, aby se databáze používala. V `Web.config` pro databázi `SecurityTutorials` už jsme definovali připojovací řetězec. Tento název připojovacího řetězce – `SecurityTutorialsConnectionString` – by měl být v rozevíracím seznamu. Vyberte tuto možnost a klikněte na další.

[![v rozevíracím seznamu zvolit SecurityTutorialsConnectionString](storing-additional-user-information-cs/_static/image23.png)](storing-additional-user-information-cs/_static/image22.png)

**Obrázek 8**: v rozevíracím seznamu vyberte možnost `SecurityTutorialsConnectionString` ([kliknutím zobrazíte obrázek v plné velikosti](storing-additional-user-information-cs/_static/image24.png)).

Na další obrazovce se zobrazí výzva k zadání tabulky a sloupců, které se mají dotazovat. V rozevíracím seznamu vyberte tabulku `UserProfiles` a ověřte všechny sloupce.

[![vrátit všechny sloupce z tabulky UserProfiles](storing-additional-user-information-cs/_static/image26.png)](storing-additional-user-information-cs/_static/image25.png)

**Obrázek 9**: Převeďte zpátky všechny sloupce z `UserProfiles` tabulky ([kliknutím zobrazíte obrázek v plné velikosti).](storing-additional-user-information-cs/_static/image27.png)

Aktuální dotaz na obrázku 9 vrátí *všechny* záznamy v `UserProfiles`, ale zajímá se jenom na záznam aktuálně přihlášeného uživatele. Chcete-li přidat klauzuli `WHERE`, klikněte na tlačítko `WHERE` a zobrazte dialogové okno Přidat `WHERE` klauzuli (viz obrázek 10). Tady můžete vybrat sloupec, který se má filtrovat, operátor a zdroj parametru filtru. Vyberte `UserId` jako sloupec a "=" jako operátor.

Bohužel není k dispozici žádný vestavěný zdroj parametrů, který by měl vracet `UserId` hodnotu aktuálně přihlášeného uživatele. Tuto hodnotu bude nutné připravujeme programově. Proto nastavte rozevírací seznam zdroj na hodnotu žádné, klikněte na tlačítko Přidat a přidejte parametr a pak klikněte na tlačítko OK.

[![přidat parametr filtru do sloupce UserId](storing-additional-user-information-cs/_static/image29.png)](storing-additional-user-information-cs/_static/image28.png)

**Obrázek 10**: přidejte parametr filtru do sloupce `UserId` ([kliknutím zobrazíte obrázek v plné velikosti).](storing-additional-user-information-cs/_static/image30.png)

Po kliknutí na tlačítko OK se vrátíte na obrazovku zobrazenou na obrázku 9. Tentokrát ale dotaz SQL v dolní části obrazovky by měl obsahovat klauzuli `WHERE`. Kliknutím na tlačítko Další přejdete na obrazovku test Query. Tady můžete spustit dotaz a zobrazit výsledky. Kliknutím na Dokončit dokončete průvodce.

Po dokončení Průvodce konfigurací zdroje dat vytvoří Visual Studio ovládací prvek SqlDataSource na základě nastavení určeného v průvodci. Kromě toho ručně přidá BoundFields do ovládacího prvku DetailsView pro každý sloupec vrácený `SelectCommand`SqlDataSource. V ovládacím prvku DetailsView není nutné zobrazovat `UserId` pole, protože tento uživatel nemusí znát tuto hodnotu. Toto pole můžete odebrat přímo z deklarativního kódu ovládacího prvku DetailsView nebo kliknutím na odkaz upravit pole z jeho inteligentní značky.

V tomto okamžiku by deklarativní označení stránky mělo vypadat podobně jako v následujícím příkladu:

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample1.aspx)]

Musíme programově nastavit parametr `UserId` ovládacího prvku SqlDataSource na aktuálně přihlášeného uživatele `UserId` předtím, než se data vyberou. To lze provést vytvořením obslužné rutiny události pro událost `Selecting` SqlDataSource a přidáním následujícího kódu:

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample2.cs)]

Výše uvedený kód začíná získáním odkazu na aktuálně přihlášeného uživatele voláním metody `GetUser` `Membership` třídy. Tím se vrátí objekt `MembershipUser`, jehož vlastnost `ProviderUserKey` obsahuje `UserId`. Hodnota `UserId` se pak přiřadí k parametru `@UserId` SqlDataSource.

> [!NOTE]
> Metoda `Membership.GetUser()` vrací informace o aktuálně přihlášeném uživateli. Pokud se stránka navštíví anonymní uživatel, vrátí se hodnota `null`. V takovém případě to bude mít za následek `NullReferenceException` v následujícím řádku kódu při pokusu o čtení vlastnosti `ProviderUserKey`. Samozřejmě se nemusíte starat o `Membership.GetUser()` vrácení `null` hodnoty na stránce `AdditionalUserInfo.aspx`, protože jsme v předchozím kurzu nakonfigurovali autorizaci adres URL, aby k prostředkům ASP.NET v této složce byla přístupná jenom ověření uživatelé. Pokud potřebujete získat přístup k informacím o aktuálně přihlášeném uživateli na stránce, kde je povolen anonymní přístup, ujistěte se, že je před odkazování na jeho vlastnosti vrácen objekt bez`null MembershipUser` z metody `GetUser()`.

Pokud navštívíte stránku `AdditionalUserInfo.aspx` v prohlížeči, zobrazí se prázdná stránka, protože jsme ještě do tabulky `UserProfiles` přidali všechny řádky. V kroku 6 se podíváme na postup přizpůsobení ovládacího prvku ovládacím CreateUserWizard, který automaticky přidá nový řádek do tabulky `UserProfiles`, když se vytvoří nový uživatelský účet. Teď ale budete muset ručně vytvořit záznam v tabulce.

Přejděte do Průzkumníka databáze v aplikaci Visual Studio a rozbalte složku tabulky. Klikněte pravým tlačítkem na tabulku `aspnet_Users` a vyberte možnost zobrazit data tabulky. zobrazí se záznamy v tabulce. proveďte stejnou věc pro `UserProfiles` tabulku. Obrázek 11 zobrazuje tyto výsledky, pokud jsou rozloženy svisle. V mojí databázi se aktuálně `aspnet_Users` záznamy pro Bruce, Fred a tito, ale v tabulce `UserProfiles` nejsou žádné záznamy.

[![obsah tabulek aspnet_Users a UserProfile se zobrazí](storing-additional-user-information-cs/_static/image32.png)](storing-additional-user-information-cs/_static/image31.png)

**Obrázek 11**: zobrazí se obsah tabulek `aspnet_Users` a `UserProfiles` ([kliknutím zobrazíte obrázek v plné velikosti).](storing-additional-user-information-cs/_static/image33.png)

Do tabulky `UserProfiles` přidejte nový záznam ručním zadáním hodnot pro pole `HomeTown`, `HomepageUrl`a `Signature`. Nejjednodušší způsob, jak získat platnou hodnotu `UserId` v novém `UserProfiles`m záznamu, je vybrat pole `UserId` z konkrétního uživatelského účtu v tabulce `aspnet_Users` a pak ho zkopírovat a vložit do pole `UserId` v `UserProfiles`. Obrázek 12 zobrazuje tabulku `UserProfiles` po přidání nového záznamu pro Bruce.

[![záznam se přidal do profilů uživatelů pro Bruce.](storing-additional-user-information-cs/_static/image35.png)](storing-additional-user-information-cs/_static/image34.png)

**Obrázek 12**: Přidání záznamu do `UserProfiles` pro Bruce ([kliknutím zobrazíte obrázek v plné velikosti](storing-additional-user-information-cs/_static/image36.png))

Vraťte se na stránku `AdditionalUserInfo.aspx`, která se přihlásila jako Bruce. Jak ukazuje obrázek 13, zobrazí se nastavení Bruce.

[![se aktuálně hostující uživatel zobrazuje jeho nastavení.](storing-additional-user-information-cs/_static/image38.png)](storing-additional-user-information-cs/_static/image37.png)

**Obrázek 13**: aktuálně navštívený uživatel zobrazuje jeho nastavení ([kliknutím zobrazíte obrázek v plné velikosti).](storing-additional-user-information-cs/_static/image39.png)

> [!NOTE]
> Pokračujte a ručně přidejte záznamy v tabulce `UserProfiles` pro každého uživatele, který je členem skupiny. V kroku 6 se podíváme na postup přizpůsobení ovládacího prvku ovládacím CreateUserWizard, který automaticky přidá nový řádek do tabulky `UserProfiles`, když se vytvoří nový uživatelský účet.

## <a name="step-3-allowing-the-user-to-edit-his-home-town-homepage-and-signature"></a>Krok 3: povolení úprav domovské města, domovské stránky a podpisu uživatelem

V tomto okamžiku si aktuálně přihlášený uživatel může zobrazit jeho domovskou města, domovskou stránku a nastavení podpisu, ale nemůže je ještě upravovat. Pojďme aktualizovat ovládací prvek DetailsView tak, aby bylo možné upravovat data.

První věc, kterou je potřeba udělat, je přidání `UpdateCommand` pro SqlDataSource, určení příkazu `UPDATE`, který se má provést, a jeho odpovídajících parametrů. Vyberte SqlDataSource a z okno Vlastnosti klikněte na tři tečky vedle vlastnosti UpdateQuery a zobrazte tak dialogové okno Editor příkazů a parametrů. Do textového pole zadejte následující příkaz `UPDATE`:

[!code-sql[Main](storing-additional-user-information-cs/samples/sample3.sql)]

Potom klikněte na tlačítko Aktualizovat parametry, čímž se vytvoří parametr v kolekci `UpdateParameters` ovládacího prvku SqlDataSource pro každý z parametrů v příkazu `UPDATE`. Ponechte zdroj všech parametrů nastaven na None a kliknutím na tlačítko OK dialogové okno dokončete.

[![zadat událost UpdateCommand a UpdateParameters objektu SqlDataSource](storing-additional-user-information-cs/_static/image41.png)](storing-additional-user-information-cs/_static/image40.png)

**Obrázek 14**: určení `UpdateCommand` a `UpdateParameters` ve třídě SqlDataSource ([kliknutím zobrazíte obrázek v plné velikosti](storing-additional-user-information-cs/_static/image42.png))

V důsledku přídavků ovládacího prvku SqlDataSource může ovládací prvek DetailsView nyní podporovat úpravy. Z inteligentní značky DetailsView zaškrtněte políčko Povolit úpravy. Tím přidáte CommandField do kolekce `Fields` ovládacího prvku s vlastností `ShowEditButton` nastavenou na hodnotu true. Tím se vykreslí tlačítko pro úpravy, když je ovládací prvek DetailsView zobrazen v režimu jen pro čtení a tlačítka aktualizovat a zrušit při zobrazení v režimu úprav. Místo toho, aby uživatel musel kliknout na upravit, můžeme mít k dispozici vykreslování prvku DetailsView ve stavu "vždycky upravovat" nastavením [vlastnosti`DefaultMode`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.detailsview.defaultmode.aspx) ovládacího prvku DetailsView na hodnotu `Edit`.

S těmito změnami by deklarativní označení ovládacího prvku DetailsView mělo vypadat podobně jako následující:

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample4.aspx)]

Všimněte si přidání CommandField a vlastnosti `DefaultMode`.

Pokračujte a otestujte tuto stránku prostřednictvím prohlížeče. Při návštěvě uživatele, který má odpovídající záznam v `UserProfiles`, se nastavení uživatele zobrazí ve upravitelném rozhraní.

[![ovládacího prvku DetailsView vykreslí upravitelné rozhraní.](storing-additional-user-information-cs/_static/image44.png)](storing-additional-user-information-cs/_static/image43.png)

**Obrázek 15**: ovládací prvek DetailsView vykresluje upravitelné rozhraní ([kliknutím zobrazíte obrázek v plné velikosti](storing-additional-user-information-cs/_static/image45.png)).

Zkuste změnit hodnoty a klikněte na tlačítko Aktualizovat. Vypadá to, že se nic nestane. Existuje postback a hodnoty jsou uloženy do databáze, ale není k dispozici žádný vizuální názor na to, že došlo k uložení.

Chcete-li tento problém napravit, vraťte se do sady Visual Studio a přidejte ovládací prvek Popisek nad ovládací prvek DetailsView. Nastavte jeho `ID` na `SettingsUpdatedMessage`, vlastnost `Text` na "nastavení bylo aktualizováno" a jeho `Visible` a `EnableViewState` vlastnosti `false`.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample5.aspx)]

Je potřeba zobrazit popisek `SettingsUpdatedMessage` pokaždé, když se prvek DetailsView aktualizuje. K tomuto účelu vytvořte obslužnou rutinu události pro událost `ItemUpdated` ovládacího prvku DetailsView a přidejte následující kód:

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample6.cs)]

Vraťte se na stránku `AdditionalUserInfo.aspx` v prohlížeči a aktualizujte data. Tentokrát se zobrazí užitečná zpráva o stavu.

[Při aktualizaci nastavení se zobrazí ![krátká zpráva.](storing-additional-user-information-cs/_static/image47.png)](storing-additional-user-information-cs/_static/image46.png)

**Obrázek 16**: při aktualizaci nastavení se zobrazí krátká zpráva ([kliknutím zobrazíte obrázek v plné velikosti](storing-additional-user-information-cs/_static/image48.png)).

> [!NOTE]
> Rozhraní pro úpravy ovládacího prvku DetailsView opouští hodně, které je potřeba. Používá textová pole se standardní velikostí, ale pole Signature by pravděpodobně mělo být víceřádkové textové pole. RegularExpressionValidator by měla být použita k zajištění, že adresa URL domovské stránky, pokud je zadána, začíná na "http://" nebo "https://". Kromě toho, vzhledem k tomu, že ovládací prvek DetailsView má svou vlastnost `DefaultMode` nastavenou na `Edit`, tlačítko zrušit neprovede žádnou akci. Měla by být odebrána nebo, pokud se klikne na tlačítko, přesměruje uživatele na jinou stránku (například `~/Default.aspx`). Tato vylepšení zanecháváme jako cvičení pro čtenáře.

### <a name="adding-a-link-to-theadditionaluserinfoaspxpage-in-the-master-page"></a>Přidání odkazu na stránku`AdditionalUserInfo.aspx`na stránce předlohy

V současné době web neposkytuje žádné odkazy na `AdditionalUserInfo.aspx` stránku. Jediným způsobem, jak ho dosáhnout, je zadat adresu URL stránky přímo do panelu Adresa v prohlížeči. Pojďme na stránku předlohy `Site.master` přidat odkaz na tuto stránku.

Odvolání, že stránka předlohy obsahuje web ovládacího prvku LoginView ve svém `LoginContent` ContentPlaceHolder, který zobrazuje jiný kód pro ověřené a anonymní návštěvníky. Aktualizuje `LoggedInTemplate` ovládacího prvku LoginView tak, aby zahrnoval odkaz na stránku `AdditionalUserInfo.aspx`. Po provedení těchto změn by deklarativní označení ovládacího prvku LoginView mělo vypadat podobně jako následující:

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample7.aspx)]

Všimněte si, že přidání ovládacího prvku hypertextový odkaz `lnkUpdateSettings` do `LoggedInTemplate`. Pomocí tohoto odkazu můžou ověření uživatelé rychle přejít na stránku a zobrazit a upravit jejich domovskou města, domovskou stránku a nastavení podpisu.

## <a name="step-4-adding-new-guestbook-comments"></a>Krok 4: přidání nových komentářů k knize návštěv

Stránka `Guestbook.aspx` je místo, kde mohou uživatelé zobrazit knihu pro vkládání a nechat si komentovat. Začněte vytvořením rozhraní pro přidání nových komentářů do knihy návštěv.

Otevřete stránku `Guestbook.aspx` v aplikaci Visual Studio a sestavte uživatelské rozhraní sestávající ze dvou ovládacích prvků TextBox, jednu pro předmět nového komentáře a jeden pro jeho tělo. Nastavte vlastnost `ID` prvního textového ovládacího prvku na hodnotu `Subject` a jeho vlastnost `Columns` na 40; nastavte druhý `ID` na `Body`, jeho `TextMode` na `MultiLine`a vlastnosti `Width` a `Rows` na hodnotu "95%" a 8 v uvedeném pořadí. Chcete-li dokončit uživatelské rozhraní, přidejte webový ovládací prvek tlačítko s názvem `PostCommentButton` a nastavte jeho vlastnost `Text` na "zveřejnit váš komentář".

Vzhledem k tomu, že každý komentář k knize webkniha vyžaduje předmět a tělo, přidejte do každého textového pole RequiredFieldValidator. Nastavte vlastnost `ValidationGroup` těchto ovládacích prvků na "EnterComment"; Podobně nastavte vlastnost `ValidationGroup` ovládacího prvku `PostCommentButton` na hodnotu "EnterComment". Další informace o ASP. Ovládací prvky ověřování netto, Prohlédněte si [ověřování formuláře v ASP.NET](http://www.4guysfromrolla.com/webtech/090200-1.shtml), ve [kterém se neprotínají ovládací prvky ověřování v ASP.NET 2,0](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx), a v [kurzu ověřování serveru kontrolujeme](http://www.w3schools.com/aspnet/aspnet_refvalidationcontrols.asp) [W3Schools](http://www.w3schools.com/).

Po vytvoření uživatelského rozhraní by deklarativní označení stránky mělo vypadat přibližně takto:

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample8.aspx)]

V případě, že je uživatelské rozhraní dokončeno, náš další úkol slouží k vložení nového záznamu do tabulky `GuestbookComments` při kliknutí na `PostCommentButton`. To lze provést několika způsoby: kód ADO.NET můžeme zapsat do obslužné rutiny události `Click` tlačítka; na stránku můžeme přidat ovládací prvek SqlDataSource, nakonfigurovat jeho `InsertCommand`a potom volat jeho `Insert` metodu z obslužné rutiny události `Click`; nebo můžeme vytvořit střední vrstvu, která byla zodpovědná za vkládání nových komentářů do knihy návštěv, a vyvolat tuto funkci z obslužné rutiny `Click` události. Vzhledem k tomu, že jsme se podívali na použití SqlDataSource v kroku 3, pojďme použít kód ADO.NET.

> [!NOTE]
> Třídy ADO.NET používané pro programový přístup k datům z databáze Microsoft SQL Server se nacházejí v oboru názvů `System.Data.SqlClient`. Tento obor názvů možná budete muset importovat do třídy kódu na pozadí vaší stránky (tj. `using System.Data.SqlClient;`).

Vytvořte obslužnou rutinu události pro událost `Click` `PostCommentButton`a přidejte následující kód:

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample9.cs)]

Obslužná rutina události `Click` se spustí kontrolou, jestli jsou data dodaná uživatelem platná. Pokud ne, před vložením záznamu se ukončí obslužná rutina události. Za předpokladu, že dodaná data jsou platná, je načtena hodnota `UserId` aktuálně přihlášeného uživatele a uložena v `currentUserId` místní proměnné. Tato hodnota je potřebná, protože při vkládání záznamu do `GuestbookComments`je nutné zadat `UserId`ou hodnotu.

V tomto případě je připojovací řetězec pro databázi `SecurityTutorials` načten z `Web.config` a je zadán příkaz `INSERT` SQL. Pak se vytvoří a otevře objekt `SqlConnection`. Dále je vytvořen objekt `SqlCommand` a jsou přiřazeny hodnoty parametrů použitých v dotazu `INSERT`. Pak se provede příkaz `INSERT` a připojení se zavřelo. Na konci obslužné rutiny události jsou `Subject` a `Body` TextBoxs `Text` vlastnosti vymazané, aby se hodnoty uživatele nezachovaly v rámci zpětného odeslání.

Pokračujte a otestujte tuto stránku v prohlížeči. Vzhledem k tomu, že tato stránka je v `Membership` složce, není přístupná pro anonymní návštěvníky. Proto se musíte nejdřív přihlásit (Pokud jste to ještě neučinili). Zadejte hodnotu do pole `Subject` a `Body` textová pole a klikněte na tlačítko `PostCommentButton`. Tím dojde k přidání nového záznamu do `GuestbookComments`. Při zpětném volání se předmět a text, který jste zadali, vymaže z textových polí.

Po kliknutí na tlačítko `PostCommentButton` neexistuje žádná vizuální zpětná vazba, kterou komentář přidal do knihy návštěv. Tuto stránku pořád potřebujeme aktualizovat, aby se zobrazily existující komentáře knihy, které provedeme v kroku 5. Jakmile to dovedeme, zobrazí se v seznamu komentářů jenom přidaný komentář, který poskytuje odpovídající vizuální zpětnou vazbu. Prozkoumáním obsahu `GuestbookComments` tabulky teď potvrďte, že se Váš komentář k knize návštěv uložil.

Obrázek 17 zobrazuje obsah `GuestbookComments` tabulky po tom, co byly dva komentáře ponechány.

[![můžete zobrazit komentáře knihy návštěv v tabulce GuestbookComments](storing-additional-user-information-cs/_static/image50.png)](storing-additional-user-information-cs/_static/image49.png)

**Obrázek 17**: komentáře knihy návštěv můžete zobrazit v tabulce `GuestbookComments` ([kliknutím zobrazíte obrázek v plné velikosti).](storing-additional-user-information-cs/_static/image51.png)

> [!NOTE]
> Pokud se uživatel pokusí vložit komentář knihy pro zápis, který obsahuje potenciálně nebezpečné označení, jako je například HTML – ASP.NET, vyvolá `HttpRequestValidationException`. Chcete-li získat další informace o této výjimce, proč je vyvolána a jak povolit uživatelům odesílat potenciálně nebezpečné hodnoty, přečtěte si dokument [White Paper s ověřením žádosti](../../../../whitepapers/request-validation.md).

## <a name="step-5-listing-the-existing-guestbook-comments"></a>Krok 5: výpis stávajících komentářů knihy návštěv

Kromě předchodu komentářů by uživatel, který navštívil stránku `Guestbook.aspx`, měl také schopnost zobrazit existující komentáře v rámci knihy. K tomuto účelu přidejte ovládací prvek ListView s názvem `CommentList` do dolní části stránky.

> [!NOTE]
> Ovládací prvek ListView je pro ASP.NET verze 3,5 nový. Je navržena tak, aby zobrazovala seznam položek v rámci velmi přizpůsobitelného a flexibilního rozložení, stále nabízí integrované úpravy, vkládání, odstraňování, stránkování a řazení funkcí jako GridView. Pokud používáte ASP.NET 2,0, bude místo toho nutné použít ovládací prvek DataList nebo Repeater. Další informace o použití ListView najdete v tématu o blogu [Guthrie](https://weblogs.asp.net/scottgu/), [na ovládacím prvku ASP: ListView](https://weblogs.asp.net/scottgu/archive/2007/08/10/the-asp-listview-control-part-1-building-a-product-listing-page-with-clean-css-ui.aspx)a v článku o [zobrazení dat pomocí ovládacího prvku ListView](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx).

Otevřete inteligentní značku ListView a v rozevíracím seznamu zvolit zdroj dat navažte ovládací prvek k novému zdroji dat. Jak jsme viděli v kroku 2, spustí se Průvodce konfigurací zdroje dat. Vyberte ikonu databáze, pojmenujte výsledné `CommentsDataSource`SqlDataSource a klikněte na OK. Potom v rozevíracím seznamu vyberte připojovací řetězec `SecurityTutorialsConnectionString` a klikněte na další.

V tomto okamžiku v kroku 2 jsme určili data k dotazování tak, že v rozevíracím seznamu vybereme tabulku `UserProfiles` a vyberete sloupce, které se mají vrátit (vrátí se zpět na obrázek 9). Tentokrát ale chceme vytvořit příkaz SQL, který vrátí nejen záznamy z `GuestbookComments`, ale také domovské město, domovskou stránku, signaturu a uživatelské jméno pro komentář. Proto vyberte přepínač "zadat vlastní příkaz SQL nebo uloženou proceduru" a klikněte na tlačítko Další.

Tím se zobrazí obrazovka "definovat vlastní příkazy nebo uložené procedury". Kliknutím na tlačítko Tvůrce dotazů graf sestavíte. Tvůrce dotazů začne tím, že se nám zobrazí dotaz na zadání tabulek, ze kterých chceme dotazovat. Vyberte tabulky `GuestbookComments`, `UserProfiles`a `aspnet_Users` a klikněte na tlačítko OK. Tato akce přidá všechny tři tabulky na návrhovou plochu. Vzhledem k tomu, že existují omezení cizího klíče mezi tabulkami `GuestbookComments`, `UserProfiles`a `aspnet_Users`, Tvůrce dotazů tyto tabulky automaticky `JOIN` s.

Vše, co zbývá, je určit sloupce, které se mají vrátit. V `GuestbookComments` tabulce vyberte sloupce `Subject`, `Body`a `CommentDate`; Vrátí sloupce `HomeTown`, `HomepageUrl`a `Signature` z tabulky `UserProfiles`; a vrátí `UserName` z `aspnet_Users`. Přidejte také "`ORDER BY CommentDate DESC`" na konec `SELECT` dotazu, aby poslední příspěvky byly vráceny jako první. Po provedení těchto výběrů by rozhraní Tvůrce dotazů mělo vypadat podobně jako snímek obrazovky na obrázku 18.

[![vytvořený dotaz spojí tabulky GuestbookComments, UserProfile a aspnet_Users.](storing-additional-user-information-cs/_static/image53.png)](storing-additional-user-information-cs/_static/image52.png)

**Obrázek 18**: vytvořený dotaz `JOIN` s tabulkami `GuestbookComments`, `UserProfiles`a `aspnet_Users` ([kliknutím zobrazíte obrázek v plné velikosti).](storing-additional-user-information-cs/_static/image54.png)

Kliknutím na tlačítko OK zavřete okno Tvůrce dotazů a vraťte se na obrazovku "definovat vlastní příkazy nebo uložené procedury". Kliknutím na tlačítko Další přejdete na obrazovku test Query, kde můžete zobrazit výsledky dotazu kliknutím na tlačítko Test dotazu. Až budete připraveni, dokončete Průvodce konfigurací zdroje dat kliknutím na Dokončit.

Po dokončení Průvodce konfigurací zdroje dat v kroku 2 byla aktualizace přidruženého ovládacího prvku DetailsView `Fields` aktualizována tak, aby zahrnovala vlastnost BoundField pro každý sloupec vrácený `SelectCommand`. Vlastnost ListView však zůstává beze změny; pořád musíme definovat rozložení. Rozložení objektu ListView lze vytvořit ručně prostřednictvím jeho deklarativního označení nebo z možnosti konfigurovat ListView v jeho inteligentní značce. Obvykle dávají přednost definici značky ručně, ale použijte jakoukoli metodu, která je pro vás nejpřirozenější.

Při použití následujících `LayoutTemplate`, `ItemTemplate`a `ItemSeparatorTemplate` pro ovládací prvek ListView:

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample10.aspx)]

`LayoutTemplate` definuje označení vygenerované ovládacím prvkem, zatímco `ItemTemplate` vykreslí každou položku vrácenou funkcí SqlDataSource. Výsledný kód `ItemTemplate`je umístěn v ovládacím prvku `itemPlaceholder` `LayoutTemplate`. Kromě `itemPlaceholder`obsahuje `LayoutTemplate` ovládací prvek DataPager, který omezí zobrazení ListView na stránku a zobrazí na stránce pouze 10 komentářů knihy návštěv (výchozí) a vykresluje stránkovací rozhraní.

Můj `ItemTemplate` zobrazuje každý předmět komentáře knihy návštěv v `<h4>` elementu s textem, který se nachází pod předmětem předmětu. Všimněte si, že syntaxe použitá pro zobrazení těla přebírá data vrácená příkazem `Eval("Body")` DataBinding, převede ji na řetězec a nahradí zalomení řádků pomocí `<br />` elementu. Tento převod je nutný k zobrazení konců řádků zadaných při odeslání komentáře, protože HTML ignoruje prázdné znaky. Podpis uživatele se pod textem zobrazuje kurzívou, za nímž následuje hlavní město uživatele, odkaz na jeho domovskou stránku, datum a čas podání komentáře a uživatelské jméno osoby, která tento komentář opustila.

Chvíli si zobrazte stránku v prohlížeči. V kroku 5 se tady zobrazí komentáře, které jste přidali do knihy návštěv.

[![kniha návštěv. aspx nyní zobrazuje komentáře knihy pro knihu návštěv.](storing-additional-user-information-cs/_static/image56.png)](storing-additional-user-information-cs/_static/image55.png)

**Obrázek 19**: `Guestbook.aspx` nyní zobrazuje komentáře knihy návštěv ([kliknutím zobrazíte obrázek v plné velikosti](storing-additional-user-information-cs/_static/image57.png))

Zkuste přidat nový komentář do knihy návštěv. Po kliknutí na tlačítko `PostCommentButton` se stránka publikuje zpátky a do databáze se přidá komentář, ale ovládací prvek ListView se neaktualizuje, aby se zobrazil nový komentář. To může opravit buď:

- Aktualizace obslužné rutiny události `Click` `PostCommentButton`ho tlačítka tak, aby po vložení nového komentáře do databáze volala metodu `DataBind()` ovládacího prvku ListView
- Nastavení vlastnosti `EnableViewState` ovládacího prvku ListView na hodnotu `false`. Tento přístup funguje, protože zakázáním stavu zobrazení ovládacího prvku musí znovu navazovat vazby na podkladová data při každém postbacku.

Tento kurz ukazuje na webu kurz ke stažení z tohoto kurzu. Vlastnost `EnableViewState` ovládacího prvku ListView `false` a kód potřebný k programovému navázání vazby dat k objektu ListView je k dispozici v obslužné rutině události `Click`, ale je označen jako komentář.

> [!NOTE]
> V současné době stránka `AdditionalUserInfo.aspx` umožňuje uživateli zobrazit a upravit nastavení domovské města, domovské stránky a podpisu. Může být vhodné aktualizovat `AdditionalUserInfo.aspx`, aby se zobrazily komentáře knihy návštěv přihlášeného uživatele. To znamená, že kromě přezkoumání a úprav svých informací může uživatel navštívit stránku `AdditionalUserInfo.aspx`, kde zjistí, jaké komentáře v knize návštěv udělaly v minulosti. Ponechám se to jako cvičení pro zúčastněný čtenář.

## <a name="step-6-customizing-the-createuserwizard-control-to-include-an-interface-for-the-home-town-homepage-and-signature"></a>Krok 6: přizpůsobení ovládacího prvku ovládacím CreateUserWizard tak, aby zahrnoval rozhraní pro domovskou města, domovskou stránku a podpis

`SELECT` dotaz použitý stránkou `Guestbook.aspx` používá `INNER JOIN` k kombinování souvisejících záznamů mezi tabulkami `GuestbookComments`, `UserProfiles`a `aspnet_Users`. Pokud uživatel, který nemá žádný záznam v `UserProfiles`, vytvoří komentář k knize webkniha, komentář se nezobrazí v zobrazení ListView, protože `INNER JOIN` vrací `GuestbookComments` záznamy pouze v případě, že jsou v `UserProfiles` a `aspnet_Users`odpovídající záznamy. A jak jsme viděli v kroku 3, pokud uživatel nemá záznam ve `UserProfiles` nemůže zobrazit nebo upravit jeho nastavení na stránce `AdditionalUserInfo.aspx`.

V důsledku našich rozhodnutí o návrhu nemusíte říct, že každý uživatelský účet v systému členství má odpovídající záznam v `UserProfiles` tabulce. Co chceme, aby se přidaný záznam přidal do `UserProfiles` pokaždé, když se v ovládacím CreateUserWizard vytvoří nový uživatelský účet členství.

Jak je popsáno v kurzu [*vytváření uživatelských účtů*](creating-user-accounts-cs.md) , poté, co je vytvořen nový uživatelský účet členství, vyvolá ovládací prvek ovládacím createuserwizard [událost`CreatedUser`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx). Pro tuto událost můžeme vytvořit obslužnou rutinu události, získat ID uživatele pro právě vytvořeného uživatele a potom do tabulky `UserProfiles` vložit záznam s výchozími hodnotami pro sloupce `HomeTown`, `HomepageUrl`a `Signature`. A co víc, je možné vyzvat uživatele k zadání těchto hodnot přizpůsobením rozhraní ovládacího prvku ovládacím CreateUserWizard, aby zahrnoval další textová pole.

Nejprve se podíváme na postup přidání nového řádku do tabulky `UserProfiles` v obslužné rutině události `CreatedUser` s výchozími hodnotami. V tomto článku se dozvíte, jak přizpůsobit uživatelské rozhraní ovládacího prvku ovládacím CreateUserWizard, aby zahrnovala další pole formuláře pro shromáždění domovské města, domovské stránky a podpisu nového uživatele.

### <a name="adding-a-default-row-touserprofiles"></a>Přidání výchozího řádku do`UserProfiles`

V kurzu [*vytváření uživatelských účtů*](creating-user-accounts-cs.md) jsme na stránku `CreatingUserAccounts.aspx` ve složce `Membership` přidali ovládací prvek ovládacím CreateUserWizard. Aby měl ovládací prvek ovládacím CreateUserWizard přidat záznam `UserProfiles` tabulky při vytváření uživatelského účtu, musíme aktualizovat funkce ovládacího prvku ovládacím CreateUserWizard. Místo toho, aby se tyto změny na stránce `CreatingUserAccounts.aspx`, místo toho přidejte na stránku `EnhancedCreateUserWizard.aspx` nový ovládací prvek ovládacím CreateUserWizard a proveďte úpravy pro tento kurz.

Otevřete stránku `EnhancedCreateUserWizard.aspx` v sadě Visual Studio a přetáhněte ovládací prvek ovládacím CreateUserWizard z panelu nástrojů na stránku. Nastavte vlastnost `ID` ovládacího prvku ovládacím CreateUserWizard na hodnotu `NewUserWizard`. Jak jsme probrali <a id="_msoanchor_5"> </a>v kurzu [*vytváření uživatelských účtů*](creating-user-accounts-cs.md) , výchozí uživatelské rozhraní ovládacím CreateUserWizard vyzve návštěvníka k zadání potřebných informací. Po zadání těchto informací ovládací prvek interně vytvoří nový uživatelský účet v rozhraní členství, a to vše bez nutnosti napsat jediný řádek kódu.

Ovládací prvek ovládacím CreateUserWizard vyvolává během svého pracovního postupu několik událostí. Jakmile návštěvník zadá informace o požadavku a odešle formulář, zpočátku ovládací prvek ovládacím CreateUserWizard aktivuje jeho [událost`CreatingUser`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.creatinguser.aspx). Pokud během procesu vytváření dojde k problému, je vyvolána [událost`CreateUserError`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createusererror.aspx) ; Pokud je však uživatel úspěšně vytvořen, je vyvolána [událost`CreatedUser`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.createduser.aspx) . <a id="_msoanchor_6"> </a>V kurzu [*vytváření uživatelských účtů*](creating-user-accounts-cs.md) jsme pro událost `CreatingUser` vytvořili obslužnou rutinu události, která zajistí, že zadané uživatelské jméno neobsahuje žádné mezery na začátku nebo na konci a že se uživatelské jméno neobjevilo kdekoli v hesle.

Aby bylo možné přidat řádek v tabulce `UserProfiles` pro právě vytvořeného uživatele, musíme pro událost `CreatedUser` vytvořit obslužnou rutinu události. V době, kdy se událost `CreatedUser` vyvolala, byl uživatelský účet již vytvořen v rámci rozhraní pro členství a umožňuje nám načíst hodnotu UserId účtu.

Vytvořte obslužnou rutinu události pro událost `CreatedUser` `NewUserWizard`a přidejte následující kód:

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample11.cs)]

Výše uvedený kód se načte načtením ID uživatele, který je právě přidaným uživatelským účtem. K tomu je potřeba pomocí metody `Membership.GetUser(username)` vracet informace o konkrétním uživateli a pak pomocí vlastnosti `ProviderUserKey` načíst své ID uživatele. Uživatelské jméno zadané uživatelem v ovládacím prvku ovládacím CreateUserWizard je k dispozici prostřednictvím [vlastnosti`UserName`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.username.aspx).

Dále je připojovací řetězec načten z `Web.config` a je zadán příkaz `INSERT`. Jsou vytvořeny instance potřebných objektů ADO.NET a příkaz byl proveden. Kód přiřadí instanci [`DBNull`](https://msdn.microsoft.com/library/system.dbnull.aspx) do parametrů `@HomeTown`, `@HomepageUrl`a `@Signature`, což má za následek vložení hodnot `NULL` databáze pro pole `HomeTown`, `HomepageUrl`a `Signature`.

Navštivte stránku `EnhancedCreateUserWizard.aspx` v prohlížeči a vytvořte nový uživatelský účet. Až to uděláte, vraťte se do sady Visual Studio a Projděte si obsah `aspnet_Users` a `UserProfiles` tabulek (jako jsme to dělali na obrázku 12). Měl by se zobrazit nový uživatelský účet v `aspnet_Users` a odpovídající `UserProfiles` řádek (s `NULL`mi hodnotami pro `HomeTown`, `HomepageUrl`a `Signature`).

[![přidání nového uživatelského účtu a záznamu UserProfile](storing-additional-user-information-cs/_static/image59.png)](storing-additional-user-information-cs/_static/image58.png)

**Obrázek 20**: Přidal se nový uživatelský účet a záznam `UserProfiles` ([kliknutím zobrazíte obrázek v plné velikosti).](storing-additional-user-information-cs/_static/image60.png)

Poté, co návštěvník zadal nové informace o účtu a kliknul na tlačítko vytvořit uživatele, je vytvořen uživatelský účet a do tabulky `UserProfiles` přidán řádek. Ovládacím CreateUserWizard pak zobrazí jeho `CompleteWizardStep`, který zobrazí zprávu o úspěchu a tlačítko pokračovat. Kliknutí na tlačítko pokračovat způsobí postback, ale není provedena žádná akce. uživatel zablokoval na stránce `EnhancedCreateUserWizard.aspx`.

Můžeme zadat adresu URL, na kterou se uživateli pošle, když se klikne na tlačítko pokračovat prostřednictvím [vlastnosti`ContinueDestinationPageUrl`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.continuedestinationpageurl.aspx)ovládacího prvku ovládacím CreateUserWizard. Vlastnost `ContinueDestinationPageUrl` nastavte na ~/Membership/AdditionalUserInfo.aspx. Tím se nový uživatel bude `AdditionalUserInfo.aspx`, kde může zobrazit a aktualizovat jeho nastavení.

### <a name="customizing-the-createuserwizards-interface-to-prompt-for-the-new-users-home-town-homepage-and-signature"></a>Přizpůsobení rozhraní ovládacím CreateUserWizard, aby se zobrazila výzva k zadání domovské města, domovské stránky a podpisu nového uživatele

Výchozí rozhraní ovládacího prvku ovládacím CreateUserWizard je dostačující pro scénáře vytváření jednoduchých účtů, kde se shromažďují jenom informace o hlavním uživatelském účtu, jako je uživatelské jméno, heslo a e-mail. Ale co kdybyste chtěli požádat návštěvníka o zadání domovské města, domovské stránky a podpisu při vytváření svého účtu? Je možné přizpůsobit rozhraní ovládacího prvku ovládacím CreateUserWizard a shromažďovat další informace při registraci. Tyto informace mohou být použity v obslužné rutině události `CreatedUser` pro vložení dalších záznamů do podkladové databáze.

Ovládací prvek ovládacím CreateUserWizard rozšiřuje ovládací prvek Průvodce ASP.NET, což je ovládací prvek, který umožňuje vývojářům stránky definovat řadu seřazených `WizardSteps`. Ovládací prvek Průvodce vykresluje aktivní krok a poskytuje navigační rozhraní, které návštěvníkovi umožňuje procházet tyto kroky. Ovládací prvek Průvodce je ideální pro rozdělení dlouhého úkolu na několik krátkých kroků. Další informace o ovládacím prvku Průvodce najdete v tématu [vytvoření podrobného uživatelského rozhraní pomocí ovládacího prvku průvodce ASP.NET 2,0](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx).

Výchozí označení ovládacího prvku ovládacím CreateUserWizard definuje dvě `WizardSteps`: `CreateUserWizardStep` a `CompleteWizardStep`.

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample12.aspx)]

První `WizardStep`, `CreateUserWizardStep`, vykreslí rozhraní, které vyzve k zadání uživatelského jména, hesla, e-mailu a tak dále. Jakmile návštěvník doplní tyto informace a klikne na možnost "vytvořit uživatele", zobrazí se `CompleteWizardStep`, která zobrazuje zprávu o úspěchu a tlačítko pokračovat.

Chcete-li přizpůsobit rozhraní ovládacího prvku ovládacím CreateUserWizard tak, aby zahrnovalo další pole formuláře, můžeme:

- <strong>Vytvořte jeden nebo více nových</strong> <strong>`WizardStep`</strong> <strong>s, aby obsahovaly další prvky uživatelského rozhraní</strong>. Chcete-li přidat novou `WizardStep` do ovládacím CreateUserWizard, klikněte na odkaz Přidat nebo odebrat `WizardSteps`z inteligentní značky a spusťte Editor kolekce `WizardStep`. Odtud můžete přidat, odebrat nebo změnit pořadí kroků v průvodci. Toto je přístup, který budeme používat pro tento kurz.

- <strong>Převést</strong> <strong>`CreateUserWizardStep`</strong> <strong>na upravitelnou</strong> <strong>`WizardStep`</strong> <strong>.</strong> Tím se `CreateUserWizardStep` nahradí ekvivalentní `WizardStep`, jehož značka definuje uživatelské rozhraní odpovídající `CreateUserWizardStep`. Převodem `CreateUserWizardStep` do `WizardStep` můžeme přemístit ovládací prvky nebo přidat další prvky uživatelského rozhraní do tohoto kroku. Chcete-li převést `CreateUserWizardStep` nebo `CompleteWizardStep` na upravitelnou `WizardStep`, klikněte na odkaz "přizpůsobit krok vytvoření uživatele" nebo "přizpůsobit úplný krok" z inteligentní značky ovládacího prvku.

- **Použijte několik kombinací výše uvedených dvou možností.**

Je důležité mít na paměti, že při kliknutí na tlačítko vytvořit uživatele z jeho `CreateUserWizardStep`spustí ovládací prvek ovládacím CreateUserWizard svůj proces vytváření uživatelského účtu. Nezáleží na tom, jestli existují další `WizardStep` s po `CreateUserWizardStep` nebo ne.

Když přidáte vlastní `WizardStep` k ovládacímu prvku ovládacím CreateUserWizard ke shromáždění dalšího vstupu uživatele, můžete vlastní `WizardStep` umístit před nebo po `CreateUserWizardStep`. Pokud se nachází před `CreateUserWizardStep` pak bude pro obslužnou rutinu události `CreatedUser` k dispozici další uživatelský vstup shromážděný z vlastního `WizardStep`. Pokud však vlastní `WizardStep` přijde po `CreateUserWizardStep` potom podle času, kdy se vlastní `WizardStep` zobrazí, nový uživatelský účet už je vytvořený a událost `CreatedUser` už se aktivovala.

Obrázek 21 ukazuje pracovní postup, když přidaný `WizardStep` předchází `CreateUserWizardStep`. Vzhledem k tomu, že dodatečné informace o uživateli byly shromážděny časem `CreatedUser` události, je nutné provést aktualizaci `CreatedUser` obslužné rutiny událostí pro načtení těchto vstupů a použít je pro hodnoty parametrů příkazu `INSERT` (místo `DBNull.Value`).

[![pracovní postup ovládacím CreateUserWizard, když další prvek WizardStep předchází vlastnost CreateUserWizardStep](storing-additional-user-information-cs/_static/image62.png)](storing-additional-user-information-cs/_static/image61.png)

**Obrázek 21**: ovládacím CreateUserWizard pracovní postup, když předchází `CreateUserWizardStep` `WizardStep` ([kliknutím zobrazíte obrázek v plné velikosti](storing-additional-user-information-cs/_static/image63.png))

Pokud je vlastní `WizardStep` umístěn *po* `CreateUserWizardStep`, je však proces vytvoření uživatelského účtu proveden předtím, než uživatel měl možnost zadat jeho domovskou města, domovskou stránku nebo podpis. V takovém případě musí být tyto další informace po vytvoření uživatelského účtu vloženy do databáze, jak je znázorněno na obrázku 22.

[![pracovní postup ovládacím CreateUserWizard, když se další prvek WizardStep nachází po hodnotě CreateUserWizardStep](storing-additional-user-information-cs/_static/image65.png)](storing-additional-user-information-cs/_static/image64.png)

**Obrázek 22**: pracovní postup ovládacím CreateUserWizard, když se za `CreateUserWizardStep` dostane další `WizardStep` ([kliknutím zobrazíte obrázek v plné velikosti](storing-additional-user-information-cs/_static/image66.png))

Pracovní postup uvedený na obrázku 22 čeká na vložení záznamu do `UserProfiles` tabulky až do dokončení kroku 2. Pokud návštěvník ukončí svůj prohlížeč po kroku 1, bude však dosaženo stavu, ve kterém byl vytvořen uživatelský účet, ale do `UserProfiles`nebyl přidán žádný záznam. Jedním alternativním řešením je mít záznam s `NULL` nebo výchozími hodnotami, které jsou vložené do `UserProfiles` v obslužné rutině události `CreatedUser` (která se aktivuje po kroku 1), a po dokončení kroku 2 Tento záznam aktualizovat. Tím se zajistí, že se pro uživatelský účet přidá záznam `UserProfiles`, i když uživatel ukončí proces registrace v rámci.

V tomto kurzu vytvoříme nový `WizardStep`, ke kterému dochází po `CreateUserWizardStep`, ale před `CompleteWizardStep`. Pojďme nejdřív načíst prvek WizardStep na místě a nakonfigurovat a potom se podíváme na kód.

Z inteligentní značky ovládacího prvku ovládacím CreateUserWizard vyberte možnost Přidat nebo odebrat `WizardStep` s, která zobrazí dialogové okno Editor kolekce `WizardStep`. Přidejte novou `WizardStep`, nastavte její `ID` na `UserSettings`, její `Title` na nastavení a `StepType` na `Step`. Pak ji umístěte do umístění po `CreateUserWizardStep` ("Zaregistrujte se k novému účtu") a před `CompleteWizardStep` ("dokončeno"), jak je znázorněno na obrázku 23.

[![přidání nového prvku WizardStep k ovládacímu prvku ovládacím CreateUserWizard](storing-additional-user-information-cs/_static/image68.png)](storing-additional-user-information-cs/_static/image67.png)

**Obrázek 23**: přidání nového `WizardStep` k ovládacímu prvku ovládacím CreateUserWizard ([kliknutím zobrazíte obrázek v plné velikosti](storing-additional-user-information-cs/_static/image69.png))

Kliknutím na tlačítko OK zavřete dialogové okno Editor kolekce `WizardStep`. Nový `WizardStep` je legitimace prostřednictvím aktualizovaného deklarativního kódu ovládacího prvku ovládacím CreateUserWizard:

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample13.aspx)]

Všimněte si nového prvku `<asp:WizardStep>`. Je potřeba přidat uživatelské rozhraní pro shromáždění domovské města, domovské stránky a podpisu nového uživatele. Tento obsah můžete zadat v deklarativní syntaxi nebo prostřednictvím návrháře. Chcete-li použít návrháře, vyberte v rozevíracím seznamu v inteligentní značce krok "nastavení" a zobrazte tak krok v návrháři.

> [!NOTE]
> Výběr kroku prostřednictvím rozevíracího seznamu inteligentních značek aktualizuje [vlastnost`ActiveStepIndex`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.createuserwizard.activestepindex.aspx)ovládacího prvku ovládacím CreateUserWizard, která určuje index počátečního kroku. Proto pokud použijete tento rozevírací seznam pro úpravu kroku nastavení v návrháři, nezapomeňte ho nastavit zpátky na možnost zaregistrovat se k novému účtu, aby se tento krok zobrazil, když uživatelé poprvé navštíví stránku `EnhancedCreateUserWizard.aspx`.

Vytvořte uživatelské rozhraní v rámci kroku "nastavení", které obsahuje tři ovládací prvky TextBox s názvem `HomeTown`, `HomepageUrl`a `Signature`. Po sestavení tohoto rozhraní by deklarativní označení ovládacím CreateUserWizard mělo vypadat podobně jako následující:

[!code-aspx[Main](storing-additional-user-information-cs/samples/sample14.aspx)]

Pokračujte a navštivte tuto stránku v prohlížeči a vytvořte nový uživatelský účet, který určí hodnoty pro domovskou města, domovskou stránku a podpis. Po dokončení `CreateUserWizardStep` se uživatelský účet vytvoří v rámci architektury členství a spustí se `CreatedUser` obslužná rutina události, která přidá nový řádek do `UserProfiles`, ale s `NULL`ovou hodnotou databáze `HomeTown`, `HomepageUrl`a `Signature`. Hodnoty zadané pro domovskou města, domovskou stránku a podpis se nikdy nepoužijí. Čistým výsledkem je nový uživatelský účet s `UserProfiles` záznamem, jehož pole `HomeTown`, `HomepageUrl`a `Signature` je ještě nutné zadat.

Musíme spustit kód za krokem "nastavení", který převezme hodnoty domovské města, honepage a signatury zadané uživatelem a aktualizuje příslušný záznam `UserProfiles`. Pokaždé, když uživatel přejde mezi kroky v ovládacím prvku průvodce, aktivuje se [událost`ActiveStepChanged`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.wizard.activestepchanged.aspx) průvodce. Pro tuto událost můžeme vytvořit obslužnou rutinu události a aktualizovat tabulku `UserProfiles`, když se krok vaše nastavení dokončil.

Přidejte obslužnou rutinu události pro událost `ActiveStepChanged` ovládacím CreateUserWizard a přidejte následující kód:

[!code-csharp[Main](storing-additional-user-information-cs/samples/sample15.cs)]

Výše uvedený kód začíná určením, zda jsme právě dosáhli kroku "dokončení". Vzhledem k tomu, že krok dokončení nastane hned za krokem "nastavení", pak když návštěvník dostane krok "dokončeno", který znamená, že právě dokončil krok "nastavení".

V takovém případě potřebujeme programově odkazovat na ovládací prvky TextBox v rámci `UserSettings WizardStep`. K tomu je potřeba použít metodu `FindControl` pro programové odkazování na `UserSettings WizardStep`a pak znovu odkazovat na textová pole z `WizardStep`. Po odkazování na textová pole jsme připraveni spustit příkaz `UPDATE`. Příkaz `UPDATE` má stejný počet parametrů jako příkaz `INSERT` v obslužné rutině události `CreatedUser`, ale zde používáme hodnoty domovské města, domovské stránky a podpisu poskytnuté uživatelem.

Pomocí této obslužné rutiny události můžete navštívit stránku `EnhancedCreateUserWizard.aspx` v prohlížeči a vytvořit nový uživatelský účet, který určí hodnoty domovské města, domovské stránky a podpisu. Po vytvoření nového účtu byste měli být přesměrováni na stránku `AdditionalUserInfo.aspx`, kde se zobrazují informace domovské města, domovské stránky a podpisu.

> [!NOTE]
> Náš web má v současné době dvě stránky, ze kterých může návštěvník vytvořit nový účet: `CreatingUserAccounts.aspx` a `EnhancedCreateUserWizard.aspx`. Stránka Mapa webu a přihlašovací stránka webu odkazuje na stránku `CreatingUserAccounts.aspx`, ale stránka `CreatingUserAccounts.aspx` nevyzve uživatele k zadání domovské města, domovské stránky a informací o podpisu a nepřidá odpovídající řádek do `UserProfiles`. Proto buď aktualizujte `CreatingUserAccounts.aspx` stránku tak, že nabídne tuto funkci, nebo aktualizujte stránku mapa a přihlašovací stránka, aby odkazovala `EnhancedCreateUserWizard.aspx` namísto `CreatingUserAccounts.aspx`. Pokud zvolíte druhou možnost, nezapomeňte aktualizovat soubor `Web.config` `Membership` složky tak, aby umožňoval anonymním uživatelům přístup na stránku `EnhancedCreateUserWizard.aspx`.

## <a name="summary"></a>Souhrn

V tomto kurzu jsme se prohlédli na postupy modelování dat, která se týkají uživatelských účtů v rámci rozhraní členství. Konkrétně jsme se podívali na modelování entit, které sdílí relaci 1:1 s uživatelskými účty a data, která sdílí relaci 1:1. Kromě toho jsme viděli, jak se tyto související informace můžou zobrazovat, vkládat a aktualizovat s některými příklady použití ovládacího prvku SqlDataSource a dalších uživatelů pomocí kódu ADO.NET.

V tomto kurzu se dokončí náš pohled na uživatelské účty. Počínaje dalším kurzem zapnete naši pozornost s rolemi. V dalších několika kurzech se podíváme na rámec rolí, informace o tom, jak vytvořit nové role, jak přiřadit role uživatelům, jak určit, k jakým rolím uživatel patří, a jak použít autorizaci založenou na rolích.

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Přístup k datům v ASP.NET 2,0 a jejich aktualizace](http://aspnet.4guysfromrolla.com/articles/011106-1.aspx)
- [Ovládací prvek Průvodce ASP.NET 2,0](https://weblogs.asp.net/scottgu/archive/2006/02/21/438732.aspx)
- [Vytvoření podrobného uživatelského rozhraní pomocí ovládacího prvku Průvodce ASP.NET 2,0](http://aspnet.4guysfromrolla.com/articles/061406-1.aspx)
- [Vytváření vlastních parametrů ovládacího prvku DataSource](http://aspnet.4guysfromrolla.com/articles/110106-1.aspx)
- [Přizpůsobení ovládacího prvku ovládacím CreateUserWizard](http://aspnet.4guysfromrolla.com/articles/070506-1.aspx)
- [Rychlé starty ovládacího prvku DetailsView](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/data/detailsview.aspx)
- [Zobrazení dat pomocí ovládacího prvku ListView](http://aspnet.4guysfromrolla.com/articles/122607-1.aspx)
- [RozASP.NET ovládacích prvků ověřování v 2,0](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)
- [Úpravy vkládání a odstraňování dat](../../data-access/editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)
- [Ověřování formuláře v ASP.NET](http://www.4guysfromrolla.com/webtech/090200-1.shtml)
- [Shromažďování uživatelských informací o registraci uživatele](https://weblogs.asp.net/scottgu/archive/2006/07/05/Tip_2F00_Trick_3A00_-Gathering-Custom-User-Registration-Information.aspx)
- [Profily v ASP.NET 2,0](http://www.odetocode.com/Articles/440.aspx)
- [Ovládací prvek ASP: ListView](https://weblogs.asp.net/scottgu/archive/2007/08/10/the-asp-listview-control-part-1-building-a-product-listing-page-with-clean-css-ui.aspx)
- [Rychlé zprovoznění profilů uživatelů](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/profile/default.aspx)

### <a name="about-the-author"></a>O autorovi

Scott Mitchell, autor několika stránek ASP/ASP. NET Books a zakladatel of 4GuysFromRolla.com, pracoval s webovými technologiemi Microsoftu od 1998. Scott funguje jako nezávislý konzultant, Trainer a zapisovač. Nejnovější kniha je *[Sams naučit se ASP.NET 2,0 za 24 hodin](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)* . Scott se dá kontaktovat [mitchell@4guysfromrolla.com](mailto:mitchell@4guysfromrolla.com) nebo prostřednictvím svého blogu na [http://ScottOnWriting.NET](http://scottonwriting.net/).

### <a name="special-thanks-to"></a>Zvláštní díky...

Tato řada kurzů byla přezkoumána mnoha užitečnými kontrolory. Uvažujete o přezkoumání mých nadcházejících článků na webu MSDN? Pokud ano, vyřaďte mi řádek na [mitchell@4GuysFromRolla.com](mailto:mitchell@4GuysFromRolla.com).

> [!div class="step-by-step"]
> [Předchozí](user-based-authorization-cs.md)
> [Další](creating-the-membership-schema-in-sql-server-vb.md)

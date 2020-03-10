---
uid: web-forms/overview/moving-to-aspnet-20/caching
title: Ukládání do mezipaměti | Microsoft Docs
author: microsoft
description: Porozumění ukládání do mezipaměti je důležité pro dobře prováděnou aplikaci ASP.NET. ASP.NET 1. x nabízí tři různé možnosti ukládání do mezipaměti; ukládání výstupu do mezipaměti,...
ms.author: riande
ms.date: 02/20/2005
ms.assetid: 2bb109d2-e299-46ea-9054-fa0263b59165
msc.legacyurl: /web-forms/overview/moving-to-aspnet-20/caching
msc.type: authoredcontent
ms.openlocfilehash: 4f0b021ca6ca151544dd9fb0587ed9e0cf14ff65
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78575934"
---
# <a name="caching"></a>Ukládání do mezipaměti

od [Microsoftu](https://github.com/microsoft)

> Porozumění ukládání do mezipaměti je důležité pro dobře prováděnou aplikaci ASP.NET. ASP.NET 1. x nabízí tři různé možnosti ukládání do mezipaměti; ukládání výstupu do mezipaměti, ukládání fragmentů do mezipaměti a rozhraní API mezipaměti.

Porozumění ukládání do mezipaměti je důležité pro dobře prováděnou aplikaci ASP.NET. ASP.NET 1. x nabízí tři různé možnosti ukládání do mezipaměti; ukládání výstupu do mezipaměti, ukládání fragmentů do mezipaměti a rozhraní API mezipaměti. ASP.NET 2,0 nabízí všechny tři tyto metody, ale přidává několik významných dalších funkcí. Existuje několik nových závislostí mezipaměti a vývojáři teď mají možnost vytvářet i vlastní závislosti v mezipaměti. Konfigurace ukládání do mezipaměti byla v ASP.NET 2,0 značně vylepšena.

## <a name="new-features"></a>Nové funkce

## <a name="cache-profiles"></a>Profily mezipaměti

Profily mezipaměti umožňují vývojářům definovat konkrétní nastavení mezipaměti, která pak můžete použít na jednotlivé stránky. Pokud máte například některé stránky, jejichž platnost má vypršet z mezipaměti po 12 hodinách, můžete snadno vytvořit profil mezipaměti, který lze na tyto stránky použít. Chcete-li přidat nový profil mezipaměti, použijte část &lt;outputCacheSettings&gt; v konfiguračním souboru. Níže je například konfigurace profilu mezipaměti s názvem *Twoday* , která konfiguruje dobu trvání mezipaměti 12 hodin.

[!code-xml[Main](caching/samples/sample1.xml)]

Chcete-li tento profil mezipaměti použít na konkrétní stránku, použijte atribut CacheProfile direktivy @ OutputCache, jak je znázorněno níže:

[!code-aspx[Main](caching/samples/sample2.aspx)]

## <a name="custom-cache-dependencies"></a>Vlastní závislosti mezipaměti

ASP.NET 1. x Developers provedli pro vlastní závislosti mezipaměti. V ASP.NET 1. x byla třída CacheDependency zapečetěná, což vývojářům zabránilo odvozovat z nich své vlastní třídy. V ASP.NET 2,0 se toto omezení odebere a vývojáři můžou zdarma vyvíjet vlastní závislosti v mezipaměti. Třída CacheDependency umožňuje vytvoření vlastní závislosti mezipaměti na základě souborů, adresářů nebo klíčů mezipaměti.

Například následující kód vytvoří novou závislost vlastní mezipaměti založenou na souboru s názvem věci. XML v kořenovém adresáři webové aplikace:

[!code-csharp[Main](caching/samples/sample3.cs)]

V tomto scénáři platí, že při změně souboru. XML se položka v mezipaměti zruší.

Je také možné vytvořit vlastní závislost mezipaměti pomocí klíčů mezipaměti. Při použití této metody odebrání klíče mezipaměti zruší platnost dat uložených v mezipaměti. Ilustruje to následující příklad:

[!code-csharp[Main](caching/samples/sample4.cs)]

Chcete-li neověřit položku, která byla vložena výše, jednoduše odeberte položku, která byla vložena do mezipaměti, aby fungovala jako klíč mezipaměti.

[!code-csharp[Main](caching/samples/sample5.cs)]

Všimněte si, že klíč položky, která funguje jako klíč mezipaměti, musí být stejný jako hodnota přidaná do pole klíčů mezipaměti.

## <a name="polling-based-sql-cache-dependenciesalso-called-table-based-dependencies"></a>Dotazy na závislosti mezipaměti SQL založené na dotazech (označované taky jako závislosti založené na tabulkách)

SQL Server 7 a 2000 použijte model založený na cyklickém dotazování pro závislosti mezipaměti SQL. Model založený na dotazech používá aktivační událost na databázové tabulce, která se aktivuje při změně dat v tabulce. Tato aktivační událost aktualizuje pole **changeId** v tabulce oznámení, které ASP.NET pravidelně kontroluje. Pokud bylo pole **changeId** aktualizováno, ASP.NET ví, že se data změnila, a zruší platnost dat uložených v mezipaměti.

> [!NOTE]
> SQL Server 2005 může také používat model založený na cyklickém dotazování, ale vzhledem k tomu, že model založený na dotazech není nejúčinnějším modelem, doporučuje se použít model založený na dotazech (popsaný později) s SQL Server 2005.

Aby závislost mezipaměti SQL používala model založený na dotazech, aby fungovala správně, musí mít tabulky povolená oznámení. To lze provést programově pomocí třídy SqlCacheDependencyAdmin nebo pomocí nástroje ASPNET\_regsql. exe.

Následující příkazový řádek registruje tabulku Products v databázi Northwind nacházející se v instanci služby SQL Server s názvem *dBASE* pro funkci závislosti mezipaměti SQL.

[!code-console[Main](caching/samples/sample6.cmd)]

Následuje vysvětlení přepínačů příkazového řádku použitých ve výše uvedeném příkazu:

| **Přepínač příkazového řádku** | **Účel** |
| --- | --- |
| -S *Server* | Určuje název serveru. |
| – Ed | Určuje, že by měla být databáze povolena pro funkci závislosti mezipaměti SQL. |
| -d *\_název databáze* | Určuje název databáze, který má být povolen pro závislost mezipaměti SQL. |
| -E | Určuje, že ASPNET\_regsql by měl při připojování k databázi používat ověřování systému Windows. |
| – et | Určuje, že povolujeme databázovou tabulku pro funkci závislosti mezipaměti SQL. |
| -t *\_název tabulky* | Určuje název tabulky databáze, která má být povolena pro funkci závislosti mezipaměti SQL. |

> [!NOTE]
> Pro ASPNET\_regsql. exe jsou k dispozici další přepínače. Úplný seznam zobrazíte spuštěním ASPNET\_regsql. exe-? z příkazového řádku.

Když se spustí tento příkaz, provedou se následující změny databáze SQL Server:

- Přidala se tabulka **AspNet\_SqlCacheTablesForChangeNotification** . Tato tabulka obsahuje jeden řádek pro každou tabulku v databázi, pro kterou byla povolena závislost mezipaměti SQL.
- V databázi se vytvoří následující uložené procedury:

| AspNet\_SqlCachePollingStoredProcedure | Zadá dotaz na tabulku AspNet\_SqlCacheTablesForChangeNotification a vrátí všechny tabulky, které mají povolenou funkci závislosti mezipaměti SQL, a hodnotu changeId pro každou tabulku. Tato uložená procedura slouží k tomu, aby zjistila, jestli se data změnila. |
| --- | --- |
| AspNet\_SqlCacheQueryRegisteredTablesStoredProcedure | Vrátí všechny tabulky povolené pro závislost mezipaměti SQL pomocí dotazu na tabulku AspNet\_SqlCacheTablesForChangeNotification a vrátí všechny tabulky povolené pro závislost mezipaměti SQL. |
| AspNet\_SqlCacheRegisterTableStoredProcedure | Zaregistruje tabulku pro funkci závislosti mezipaměti SQL přidáním potřebné položky do tabulky oznámení a přidá aktivační událost. |
| AspNet\_SqlCacheUnRegisterTableStoredProcedure | Zruší registraci tabulky pro závislost mezipaměti SQL odebráním položky v tabulce oznámení a odebere Trigger. |
| AspNet\_SqlCacheUpdateChangeIdStoredProcedure | Aktualizuje tabulku oznámení zvýšením changeId u změněné tabulky. ASP.NET používá tuto hodnotu k určení, jestli se data změnila. Jak je uvedeno níže, tato uložená procedura se spustí triggerem vytvořeným při povolení tabulky. |

- Pro tabulku se vytvoří aktivační událost SQL Server s názvem  **_Table\_Name_\_AspNet\_SqlCacheNotification\_** . Tato aktivační událost spustí SqlCacheUpdateChangeIdStoredProcedure AspNet\_, když se v tabulce provede vložení, aktualizace nebo odstranění.
- Do databáze se přidala role SQL Server s názvem **aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess** .

Role **aspnet\_ChangeNotification\_ReceiveNotificationsOnlyAccess** SQL Server má pro ASPNET\_SQLCACHEPOLLINGSTOREDPROCEDURE oprávnění Exec. Aby model cyklického dotazování fungoval správně, je nutné přidat účet procesu do role ASPNET\_ChangeNotification\_ReceiveNotificationsOnlyAccess. Nástroj ASPNET\_regsql. exe to pro vás neudělá.

### <a name="configuring-polling-based-sql-cache-dependencies"></a>Konfigurace závislostí mezipaměti SQL na základě cyklického dotazování

Pro konfiguraci závislostí mezipaměti SQL založeného na dotazech je potřeba několik kroků. Prvním krokem je povolení databáze a tabulky, jak je popsáno výše. Po dokončení tohoto kroku je zbývající konfigurace následující:

- Konfigurace konfiguračního souboru ASP.NET.
- Konfigurace podtřídy SqlCacheDependency

### <a name="configuring-the-aspnet-configuration-file"></a>Konfigurace konfiguračního souboru ASP.NET

Kromě přidání připojovacího řetězce, jak je popsáno v předchozím modulu, je nutné také nakonfigurovat&gt; elementu &lt;cache pomocí elementu &lt;sqlCacheDependency&gt; element, jak je znázorněno níže:

[!code-xml[Main](caching/samples/sample7.xml)]

Tato konfigurace povoluje závislost mezipaměti SQL v databázi *pubs* . Všimněte si, že atribut pollTime v &lt;sqlCacheDependency&gt; elementu je standardně 60000 milisekund nebo 1 minuta. (Tato hodnota nemůže být menší než 500 milisekund.) V tomto příkladu &lt;přidání&gt; elementu přidá novou databázi a přepíše pollTime a nastaví ji na 9000000 milisekund.

#### <a name="configuring-the-sqlcachedependency"></a>Konfigurace podtřídy SqlCacheDependency

Dalším krokem je konfigurace SqlCacheDependency. Nejjednodušší způsob, jak toho dosáhnout, je zadat hodnotu pro atribut SqlDependency v direktivě @ cache, jak je znázorněno níže:

[!code-aspx[Main](caching/samples/sample8.aspx)]

V direktivě @ OutputCache je závislost mezipaměti SQL nakonfigurovaná pro tabulku *autoři* v databázi *pubs* . Více závislostí lze nakonfigurovat oddělením středníkem, např.:

[!code-aspx[Main](caching/samples/sample9.aspx)]

Další metodou konfigurace SqlCacheDependency je tak, že to uděláte programově. Následující kód vytvoří novou závislost mezipaměti SQL v tabulce *autoři* v databázi *pubs* .

[!code-csharp[Main](caching/samples/sample10.cs)]

Jednou z výhod programu pro definování závislosti mezipaměti SQL je, že můžete zpracovat jakékoli výjimky, ke kterým může dojít. Pokud se například pokusíte definovat závislost mezipaměti SQL pro databázi, u které není povoleno oznámení, bude vyvolána výjimka **DatabaseNotEnabledForNotificationException –** . V takovém případě se můžete pokusit o povolení databáze pro oznámení voláním metody **SqlCacheDependencyAdmin. EnableNotifications** a předáním názvu databáze.

Podobně platí, že pokud se pokusíte definovat závislost mezipaměti SQL pro tabulku, u které není povoleno oznámení, bude vyvolána výjimka **TableNotEnabledForNotificationException –** . Pak můžete zavolat metodu **SqlCacheDependencyAdmin. EnableTableForNotifications** a předat jí název databáze a název tabulky.

Následující ukázka kódu ukazuje, jak správně nakonfigurovat zpracování výjimek při konfiguraci závislosti mezipaměti SQL.

[!code-csharp[Main](caching/samples/sample11.cs)]

Další informace: [https://msdn.microsoft.com/library/t9x04ed2.aspx](https://msdn.microsoft.com/library/t9x04ed2.aspx)

## <a name="query-based-sql-cache-dependencies-sql-server-2005-only"></a>Závislosti mezipaměti SQL založené na dotazech (jenom SQL Server 2005)

Pokud používáte SQL Server 2005 pro závislost mezipaměti SQL, model založený na dotazech není nutný. Při použití s SQL Server 2005 funguje závislost mezipaměti SQL přímo prostřednictvím připojení SQL k instanci SQL Server (není nutná žádná další konfigurace) pomocí oznámení dotazů SQL Server 2005.

Nejjednodušší způsob, jak povolit oznámení na základě dotazů, je provést deklarativní postup nastavením atributu **SqlCacheDependency** objektu zdroje dat na hodnotu **CommandNotification** a nastavením atributu **EnableCaching** na **hodnotu true**. Při použití této metody není vyžadován žádný kód. Pokud se změní výsledek příkazu provedeného proti zdroji dat, zruší platnost dat v mezipaměti.

Následující příklad konfiguruje ovládací prvek zdroje dat pro závislost mezipaměti SQL:

[!code-aspx[Main](caching/samples/sample12.aspx)]

V tomto případě, pokud dotaz zadaný v vlastnosti **SelectCommand** vrací jiný výsledek než původně, výsledky, které jsou uloženy v mezipaměti, jsou neověřeny.

Můžete také určit, že všechny zdroje dat budou povolené pro závislosti mezipaměti SQL, a to nastavením atributu **SqlDependency** direktivy **@ OutputCache** na hodnotu **CommandNotification**. Následující příklad znázorňuje tuto.

[!code-aspx[Main](caching/samples/sample13.aspx)]

> [!NOTE]
> Další informace o oznámeních dotazů v SQL Server 2005 naleznete na webu SQL Server Books Online.

Další metodou konfigurace závislosti mezipaměti SQL založeného na dotazech je to provést programově pomocí třídy SqlCacheDependency. Následující ukázka kódu ukazuje, jak to lze provést.

[!code-csharp[Main](caching/samples/sample14.cs)]

Další informace: [https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp](https://msdn.microsoft.com/library/default.asp?url=/library/enus/dnvs05/html/querynotification.asp)

## <a name="post-cache-substitution"></a>Náhrada po mezipaměti

Ukládání stránky do mezipaměti může významně zvýšit výkon webové aplikace. V některých případech ale potřebujete, aby se většina stránky ukládala do mezipaměti a některé fragmenty stránky byly dynamické. Například pokud vytvoříte stránku novinových scénářů, které jsou kompletně statické pro nastavené časové období, můžete nastavit ukládání celé stránky do mezipaměti. Pokud jste chtěli zahrnout rotační hlavičku reklamy, která se změnila na všech žádostech stránky, je nutné, aby část stránky obsahující reklamu byla dynamická. Aby bylo možné stránku ukládat do mezipaměti, ale dynamicky dosadit obsah, můžete použít substituci ASP.NET po mezipaměti. Při nahrazení po mezipaměti je celá stránka výstupní v mezipaměti s konkrétními částmi označenými jako vyloučené z ukládání do mezipaměti. V příkladu proužkové reklamy vám ovládací prvek AdRotator umožňuje využít výhod substituce po mezipaměti, aby se pro každého uživatele a při každé aktualizaci stránky vytvořila dynamická inzerce.

Existují tři způsoby implementace náhrady po mezipaměti:

- Deklarativně pomocí ovládacího prvku pro nahrazování.
- Programově pomocí rozhraní API pro nahrazování ovládacích prvků.
- Implicitně pomocí ovládacího prvku AdRotator.

### <a name="substitution-control"></a>Ovládací prvek Substitution

Ovládací prvek ASP.NET Substitution určuje oddíl stránky v mezipaměti, která je vytvořena dynamicky, nikoli v mezipaměti. Náhradní ovládací prvek umístíte na místo na stránce, kde se má zobrazit dynamický obsah. V době běhu volá ovládací prvek Substitution metodu, kterou určíte pomocí vlastnosti MethodName. Metoda musí vracet řetězec, který pak nahradí obsah ovládacího prvku pro nahrazování. Metoda musí být statická metoda na ovládacím prvku obsahujícím stránku nebo UserControl. Použití ovládacího prvku Substitution způsobí změnu mezipaměti na straně klienta na možnost ukládání do mezipaměti serveru, takže se stránka nebude ukládat do mezipaměti v klientovi. Tím se zajistí, že budoucí požadavky na stránku volají metodu znovu, aby se vygeneroval dynamický obsah.

### <a name="substitution-api"></a>Náhradní rozhraní API

Chcete-li vytvořit dynamický obsah stránky v mezipaměti programově, můžete zavolat metodu [WriteSubstitution](https://msdn.microsoft.com/library/system.web.httpresponse.writesubstitution.aspx) v kódu stránky a předat jí název metody jako parametr. Metoda, která zpracovává vytváření dynamického obsahu, přijímá jeden parametr [HttpContext](https://msdn.microsoft.com/library/system.web.httpcontext.aspx) a vrací řetězec. Vrácený řetězec je obsah, který bude nahrazen v daném umístění. Výhodou volání metody WriteSubstitution namísto použití ovládacího prvku pro nahrazování je deklarativní, že můžete zavolat metodu libovolného objektu místo volání statické metody stránky nebo objektu UserControl.

Volání metody WriteSubstitution způsobí, že se mezipaměť na straně klienta změní na možnost ukládání do mezipaměti serveru, takže se stránka nebude ukládat do mezipaměti klienta. Tím se zajistí, že budoucí požadavky na stránku volají metodu znovu, aby se vygeneroval dynamický obsah.

### <a name="adrotator-control"></a>Ovládací prvek AdRotator

Serverový ovládací prvek AdRotator implementuje podporu pro nahrazení po mezipaměti interně. Pokud umístíte ovládací prvek AdRotator na svou stránku, vykreslí se jedinečné reklamy na každém požadavku bez ohledu na to, zda je nadřazená stránka uložena do mezipaměti. V důsledku toho je stránka, která obsahuje ovládací prvek AdRotator, pouze uložená v mezipaměti na straně serveru.

## <a name="controlcachepolicy-class"></a>ControlCachePolicy – třída

Třída ControlCachePolicy umožňuje programové řízení pro ukládání fragmentů do mezipaměti pomocí uživatelských ovládacích prvků. ASP.NET vloží uživatelské ovládací prvky do instance [BasePartialCachingControl](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.aspx) . Třída BasePartialCachingControl představuje uživatelský ovládací prvek, který má povoleno ukládání výstupu do mezipaměti.

Při přístupu k vlastnosti [BasePartialCachingControl. Vlastnost CachePolicy](https://msdn.microsoft.com/library/system.web.ui.basepartialcachingcontrol.cachepolicy.aspx) ovládacího prvku [PartialCachingControl](https://msdn.microsoft.com/library/system.web.ui.partialcachingcontrol.aspx) budete vždy obdržet platný objekt ControlCachePolicy. Pokud však přistupujete k vlastnosti [UserControl. Vlastnost CachePolicy](https://msdn.microsoft.com/library/system.web.ui.usercontrol.cachepolicy.aspx) ovládacího prvku [UserControl](https://msdn.microsoft.com/library/system.web.ui.usercontrol.aspx) , obdržíte platný objekt ControlCachePolicy pouze v případě, že uživatelský ovládací prvek je již zabalen ovládacím prvkem BasePartialCachingControl. Pokud není zabalen, objekt ControlCachePolicy vrácený vlastností vyvolá výjimku při pokusu o manipulaci, protože nemá přidružené BasePartialCachingControl. Pokud chcete zjistit, jestli instance UserControl podporuje ukládání do mezipaměti bez generování výjimek, prozkoumejte vlastnost [SupportsCaching](https://msdn.microsoft.com/library/system.web.ui.controlcachepolicy.supportscaching.aspx) .

Použití třídy ControlCachePolicy je jedním z několika způsobů, jak lze povolit ukládání výstupu do mezipaměti. Následující seznam popisuje metody, které můžete použít k povolení ukládání výstupu do mezipaměti:

- Použijte direktivu [@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx) k povolení ukládání výstupu do mezipaměti v deklarativních scénářích.
- Použijte atribut [PartialCachingAttribute](https://msdn.microsoft.com/library/system.web.ui.partialcachingattribute.aspx) , chcete-li povolit ukládání do mezipaměti pro uživatelský ovládací prvek v souboru kódu na pozadí.
- Použijte třídu ControlCachePolicy k určení nastavení mezipaměti v programových scénářích, ve kterých pracujete s instancemi BasePartialCachingControl, které byly povoleny do mezipaměti pomocí jedné z předchozích metod a dynamicky načteny pomocí metody [System. Web. UI. třída TemplateControl. LoadControl](https://msdn.microsoft.com/library/system.web.ui.templatecontrol.loadcontrol.aspx) .

Instance ControlCachePolicy může být úspěšně manipulována pouze mezi fázemi init a PreRender životního cyklu ovládacího prvku. Pokud upravíte objekt ControlCachePolicy po fázi PreRender, ASP.NET vyvolá výjimku, protože jakékoli změny provedené po vygenerování ovládacího prvku nemohou skutečně ovlivnit nastavení mezipaměti (ovládací prvek je uložen v mezipaměti během fáze vykreslování). Nakonec instance uživatelského ovládacího prvku (a proto jeho objekt ControlCachePolicy) je k dispozici pouze pro programovou manipulaci, když je ve skutečnosti vykreslena.

## <a name="changes-to-caching-configuration---the-ltcachinggt-element"></a>Změny v konfiguraci ukládání do mezipaměti – &lt;&gt; elementu pro ukládání do mezipaměti

Konfigurace ukládání do mezipaměti v ASP.NET 2,0 je několik změn. Element &lt;Caching&gt; je v ASP.NET 2,0 novinkou a umožňuje ukládat do mezipaměti změny konfigurace v konfiguračním souboru. K dispozici jsou následující atributy.

| **Element** | **Popis** |
| --- | --- |
| **uchovávat** | Volitelný element. Definuje globální nastavení mezipaměti aplikace. |
| **outputCache** | Volitelný element. Určuje nastavení výstupní mezipaměti pro aplikaci na úrovni aplikace. |
| **outputCacheSettings** | Volitelný element. Určuje nastavení výstupní mezipaměti, která lze použít na stránky v aplikaci. |
| **Třídy** | Volitelný element. Konfiguruje závislosti mezipaměti SQL pro aplikaci ASP.NET. |

### <a name="the-ltcachegt-element"></a>&gt; elementu &lt;cache

V&gt; elementu &lt;cache jsou k dispozici následující atributy:

| **Atribut** | **Popis** |
| --- | --- |
| **disableMemoryCollection** | Volitelný atribut **typu Boolean** . Získává nebo nastavuje hodnotu, která indikuje, jestli je zakázaná kolekce paměti mezipaměti, která nastane, když je počítač v paměti tlakem. |
| **disableExpiration** | Volitelný atribut **typu Boolean** . Získává nebo nastavuje hodnotu, která indikuje, jestli je zakázané vypršení platnosti mezipaměti. Pokud je tato možnost zakázaná, položky uložené v mezipaměti nekončí vypršení platnosti a nedochází k čištění dat na pozadí s neplatnými položkami mezipaměti. |
| **privateBytesLimit** | Nepovinný atribut **Int64** Získá nebo nastaví hodnotu, která indikuje maximální velikost privátních bajtů aplikace před tím, než začne vyprázdnit položky s vypršenou platností a pokus o uvolnění paměti. Tento limit zahrnuje jak paměť využívaná v mezipaměti, tak i normální režii paměti spuštěné aplikace. Nastavení nula znamená, že ASP.NET bude používat vlastní heuristické metody pro určení, kdy se má spustit uvolnění paměti. |
| **percentagePhysicalMemoryUsedLimit** | Volitelný atribut **Int32** Získává nebo nastavuje hodnotu, která indikuje maximální procento fyzické paměti počítače, kterou může aplikace spotřebovat před tím, než začne docházet k vyprázdnění položek s vypršenou platností a pokus o uvolnění paměti zahrnuje i paměť využívané mezipamětí. jako normální využití paměti běžící aplikace. Nastavení nula znamená, že ASP.NET bude používat vlastní heuristické metody pro určení, kdy se má spustit uvolnění paměti. |
| **privateBytesPollTime** | Volitelný atribut **TimeSpan** . Získá nebo nastaví hodnotu označující časový interval mezi dotazem na využití paměti privátních bajtů aplikace. |

### <a name="the-ltoutputcachegt-element"></a>Element &lt;outputCache&gt;

Pro &lt;outputCache&gt; element jsou k dispozici následující atributy.

|       <strong>Atribut</strong>        |                                                                                                                                                                                                                                                       <strong>Popis</strong>                                                                                                                                                                                                                                                       |
|-----------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   <strong>enableOutputCache</strong>    |                                                                                                                                                          Volitelný atribut <strong>typu Boolean</strong> . Povolí nebo zakáže výstupní mezipaměť stránky. Pokud je tato možnost zakázána, žádné stránky nejsou ukládány do mezipaměti bez ohledu na programové nebo deklarativní nastavení. Výchozí hodnota je <strong>true</strong>.                                                                                                                                                           |
|  <strong>enableFragmentCache</strong>   |                                                Volitelný atribut <strong>typu Boolean</strong> . Povolí nebo zakáže mezipaměť fragmentů aplikace. Pokud je tato část zakázaná, neukládají se do mezipaměti žádné stránky bez ohledu na direktivu [@ OutputCache](https://msdn.microsoft.com/library/hdxfb6cy.aspx) nebo použitém profilu mezipaměti. Zahrnuje hlavičku Cache-Control, která označuje, že nadřazené proxy servery i klienti prohlížeče by se neměli pokoušet ukládat výstup stránky do mezipaměti. Výchozí hodnota je <strong>false</strong>.                                                 |
| <strong>sendCacheControlHeader</strong> |                                                                                                                                                      Volitelný atribut <strong>typu Boolean</strong> . Získává nebo nastavuje hodnotu, která označuje, jestli se ve výchozím nastavení odesílá do modulu výstupní mezipaměti <strong>privátní hlavička Cache-Control: Private</strong> . Výchozí hodnota je <strong>false</strong>.                                                                                                                                                      |
|      <strong>omitVaryStar</strong>      | Volitelný atribut <strong>typu Boolean</strong> . Povolí nebo zakáže odeslání<strong>http v odpovědi \</strong ><em>hlavičce. S výchozím nastavením false</em>se <strong>pro stránky v mezipaměti pošle hlavička "* Vary: \*". Při odeslání hlavičky Vary umožňuje ukládání různých verzí do mezipaměti na základě toho, co je uvedeno v hlavičce Vary. Například <em>: User-Agents</em> uloží různé verze stránky na základě uživatelského agenta, který požadavek vystavil. Výchozí hodnota je * * false</strong>. |

### <a name="the-ltoutputcachesettingsgt-element"></a>Element &lt;outputCacheSettings&gt;

&lt;element&gt; outputCacheSettings umožňuje vytváření profilů mezipaměti, jak je popsáno výše. Jediným podřízeným elementem prvku &lt;outputCacheSettings&gt; je prvek&gt; &lt;outputCacheProfiles pro konfiguraci profilů mezipaměti.

### <a name="the-ltsqlcachedependencygt-element"></a>Element &lt;sqlCacheDependency&gt;

Následující atributy jsou k dispozici pro &lt;&gt; elementu sqlCacheDependency.

| **Atribut** | **Popis** |
| --- | --- |
| **umožněn** | Požadovaný atribut **typu Boolean** . Indikuje, jestli se pro ně nedotazují změny. |
| **pollTime** | Volitelný atribut **Int32** Nastaví frekvenci, se kterou se podtřídy SqlCacheDependency dotazují na změny v tabulce databáze. Tato hodnota odpovídá počtu milisekund mezi po sobě jdoucí cyklické dotazování. Nedá se nastavit na míň než 500 milisekund. Výchozí hodnota je 1 minuta. |

### <a name="more-information"></a>Další informace

K dispozici jsou některé další informace, o kterých byste měli vědět o konfiguraci mezipaměti.

- Pokud není nastaven limit Nesdílených bajtů pracovních procesů, mezipaměť bude používat jedno z následujících omezení: 

    - x86 GB: 800MB nebo 60% fyzické paměti RAM, podle toho, co je méně
    - x86 povolenou: 1800MB nebo 60% fyzické paměti RAM, podle toho, co je míň
    - x64:1 terabajt nebo 60% fyzické paměti RAM, podle toho, co je míň
- Pokud jsou nastavené limity velikosti privátních bajtů pracovních procesů a &lt;mezipaměti privateBytesLimit/&gt;, mezipaměť bude používat minimálně tyto dvě.
- Stejně jako v 1. x jsme vynechal položky mezipaměti a zavolali GC. Shromažďovat ze dvou důvodů: 

    - Blíží se limit Nesdílených bajtů.
    - Dostupná paměť je blízko nebo méně než 10%.
- Nastavením &lt;mezipaměti percentagePhysicalMemoryUseLimit/&gt; na 100 můžete efektivně zakázat funkci trim a mezipaměť pro stav s nedostatkem volné paměti.
- Na rozdíl od 1. x 2,0 pozastaví ořezávání a shromáždí volání, pokud poslední GC. Collect nesnižoval soukromé bajty nebo velikost spravovaných hald o více než 1% limitu paměti (mezipaměti).

## <a name="lab1-custom-cache-dependencies"></a>Lab1: vlastní závislosti mezipaměti

1. Vytvoří nový web.
2. Přidejte nový soubor XML s názvem cache. XML a uložte jej do kořenového adresáře webové aplikace.
3. Přidejte následující kód na stránku\_metoda Load v kódu na pozadí default. aspx: 

    [!code-csharp[Main](caching/samples/sample15.cs)]
4. Do horní části default. aspx v zobrazení zdroj přidejte následující: 

    [!code-aspx[Main](caching/samples/sample16.aspx)]
5. Přejděte na Default. aspx. Co tento čas říká?
6. Aktualizujte prohlížeč. Co tento čas říká?
7. Otevřete cache. XML a přidejte následující kód: 

    [!code-xml[Main](caching/samples/sample17.xml)]
8. Uložte cache. XML.
9. Aktualizujte si prohlížeč. Co tento čas říká?
10. Vysvětlete, proč se čas aktualizoval místo zobrazení hodnot dříve uložených v mezipaměti:

## <a name="lab-2-using-polling-based-cache-dependencies"></a>Testovací prostředí 2: použití závislostí mezipaměti založeného na dotazech

Toto testovací prostředí používá projekt, který jste vytvořili v předchozím modulu, který umožňuje upravovat data v databázi Northwind prostřednictvím ovládacího prvku GridView a DetailsView.

1. Otevřete projekt v aplikaci Visual Studio 2005.
2. Pro povolení databáze a tabulky Products spusťte nástroj ASPNET\_regsql s databází Northwind. Použijte následující příkaz z příkazového řádku sady Visual Studio: 

    [!code-console[Main](caching/samples/sample18.cmd)]
3. Do souboru Web. config přidejte následující: 

    [!code-xml[Main](caching/samples/sample19.xml)]
4. Přidejte nový webformu s názvem showData. aspx.
5. Přidejte následující direktivu @ OutputCache na stránku showData. aspx: 

    [!code-aspx[Main](caching/samples/sample20.aspx)]
6. Na stránku\_načtení showData. aspx přidejte následující kód: 

    [!code-html[Main](caching/samples/sample21.html)]
7. Přidejte nový ovládací prvek SqlDataSource do showData. aspx a nakonfigurujte ho tak, aby používal připojení k databázi Northwind. Klikněte na Další.
8. Zaškrtněte políčka NázevVýrobku a ProductID a klikněte na další.
9. Klikněte na tlačítko Dokončit.
10. Přidejte nový prvek GridView na stránku showData. aspx.
11. Z rozevíracího seznamu vyberte možnost SqlDataSource1.
12. Uložte a přejděte na showData. aspx. Poznamenejte si čas zobrazený v čase.

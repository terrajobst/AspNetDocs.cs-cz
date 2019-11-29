---
uid: web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs
title: Protokolování podrobností o chybách pomocí monitorování stavu ASP.NETC#() | Microsoft Docs
author: rick-anderson
description: Systém sledování stavu společnosti Microsoft poskytuje snadný a přizpůsobitelný způsob, jak protokolovat různé webové události, včetně neošetřených výjimek. Tento kurz projde p...
ms.author: riande
ms.date: 06/09/2009
ms.assetid: b1abb452-642a-4ff3-8504-37b85590ff79
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deploying-web-site-projects/logging-error-details-with-asp-net-health-monitoring-cs
msc.type: authoredcontent
ms.openlocfilehash: e52ed94f78d053701771690fce432d5a1d465b62
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74637277"
---
# <a name="logging-error-details-with-aspnet-health-monitoring-c"></a>Protokolování podrobností o chybách pomocí monitorování stavu v ASP.NET (C#)

[Scott Mitchell](https://twitter.com/ScottOnWriting)

[Stažení kódu](https://download.microsoft.com/download/1/0/C/10CC829F-A808-4302-97D3-59989B8F9C01/ASPNET_Hosting_Tutorial_13_CS.zip) nebo [stažení PDF](https://download.microsoft.com/download/5/C/5/5C57DB8C-5DEA-4B3A-92CA-4405544D313B/aspnet_tutorial13_HealthMonitoring_cs.pdf)

> Systém sledování stavu společnosti Microsoft poskytuje snadný a přizpůsobitelný způsob, jak protokolovat různé webové události, včetně neošetřených výjimek. Tento kurz vás provede nastavením systému monitorování stavu, aby protokoloval neošetřené výjimky do databáze a upozornil vývojářům prostřednictvím e-mailové zprávy.

## <a name="introduction"></a>Úvod

Protokolování je užitečný nástroj pro monitorování stavu nasazené aplikace a diagnostikování všech problémů, které mohou nastat. Je obzvláště důležité protokolovat chyby, ke kterým dochází v nasazené aplikaci, aby bylo možné je odstranit. Událost `Error` je vyvolána pokaždé, když dojde k neošetřené výjimce v aplikaci ASP.NET; [předchozí kurz](processing-unhandled-exceptions-cs.md) ukázal, jak upozorněte vývojáře na chybu a protokolovat své podrobnosti vytvořením obslužné rutiny události pro událost `Error`. Nicméně vytvoření obslužné rutiny události `Error` k zaznamenání podrobností o chybě a informování o tom, že vývojář bude zbytečný, protože tuto úlohu může provádět ASP. *Systém monitorování stavu*sítě.

Systém sledování stavu byl představený v ASP.NET 2,0 a je navržený tak, aby monitoroval stav nasazené aplikace ASP.NET protokolováním událostí, ke kterým dojde během doby platnosti aplikace nebo žádosti. Události zaznamenané systémem sledování stavu se nazývají *události monitorování stavu* nebo *webové události*a zahrnují:

- Události životního cyklu aplikace, například při spuštění nebo zastavení aplikace
- Události zabezpečení, včetně neúspěšných pokusů o přihlášení a nezdařených žádostí o ověření adresy URL
- Chyby aplikace, včetně neošetřených výjimek, zobrazování výjimek při analýze stavu, žádosti o ověření a chyby kompilace, a to mimo jiné typy chyb.

Když se aktivuje událost monitorování stavu, může se přihlásit k libovolnému počtu zadaných *zdrojů protokolu*. Systém monitorování stavu je dodáván se zdroji protokolů, které protokolují webové události do databáze Microsoft SQL Server, do protokolu událostí systému Windows nebo prostřednictvím e-mailové zprávy, mimo jiné. Můžete také vytvořit vlastní zdroje protokolů.

V `Web.config`se definují události v systémových protokolech monitorování stavu společně s použitými zdroji protokolů. Pomocí několika řádků kódu konfigurace můžete použít sledování stavu k protokolování všech neošetřených výjimek do databáze a k informování o výjimce prostřednictvím e-mailu.

## <a name="exploring-the-health-monitoring-systems-configuration"></a>Zkoumání konfigurace systému sledování stavu

Chování systému monitorování stavu je definováno pomocí informací o konfiguraci, které jsou umístěny v [prvku`<healthMonitoring>`](https://msdn.microsoft.com/library/2fwh2ss9.aspx) v `Web.config`. Tento oddíl konfigurace definuje mimo jiné následující tři důležité informace:

1. Události monitorování stavu, které jsou při vyvolání, by měly být protokolovány,
2. Zdroje protokolů a
3. Způsob, jakým se každá událost monitorování stavu definovaná v (1) mapuje na zdroje protokolu definované v (2).

Tyto informace jsou zadány pomocí tří elementů konfigurace podřízených: [`<eventMappings>`](https://msdn.microsoft.com/library/yc5yk01w.aspx), [`<providers>`](https://msdn.microsoft.com/library/zaa41kz1.aspx)a [`<rules>`](https://msdn.microsoft.com/library/fe5wyxa0.aspx)v uvedeném pořadí.

Výchozí informace o konfiguraci systému monitorování stavu najdete v souboru `Web.config` v `%WINDIR%\Microsoft.NET\Framework\version\CONFIG` složce. Tyto výchozí konfigurační informace s některými odebranými kódy pro zkrácení jsou uvedené níže:

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample1.xml)]

Události monitorování stavu, které jsou předmětem zájmu, jsou definovány v prvku `<eventMappings>`, který poskytuje lidský popisný název třídy událostí monitorování stavu. Ve výše uvedeném kódu `<eventMappings>` prvek přiřadí "všechny chyby" uživatelsky přívětivým názvům události monitorování stavu typu `WebBaseErrorEvent` a název "audity selhání" pro události monitorování stavu typu `WebFailureAuditEvent`.

Element `<providers>` definuje zdroje protokolů a poskytuje jim uživatelsky přívětivý název a uvádí všechny informace o konfiguraci specifické pro zdroj protokolu. První prvek `<add>` definuje poskytovatele "EventLogProvider", který protokoluje zadané události monitorování stavu pomocí třídy `EventLogWebEventProvider`. Třída `EventLogWebEventProvider` protokoluje událost do protokolu událostí systému Windows. Druhý `<add>` prvek definuje poskytovatele "SqlWebEventProvider", který protokoluje události do databáze Microsoft SQL Server prostřednictvím třídy `SqlWebEventProvider`. Konfigurace "SqlWebEventProvider" Určuje připojovací řetězec databáze (`connectionStringName`) mezi dalšími možnostmi konfigurace.

Element `<rules>` mapuje události zadané v elementu `<eventMappings>` na zdroje protokolu v elementu `<providers>`. Ve výchozím nastavení protokoluje webové aplikace ASP.NET všechny neošetřené výjimky a chyby auditu do protokolu událostí systému Windows.

## <a name="logging-events-to-a-database"></a>Protokolování událostí do databáze

Výchozí konfiguraci systému sledování stavu lze přizpůsobit na základě webové aplikace pomocí přidání oddílu `<healthMonitoring>` do souboru `Web.config` aplikace. Do sekcí `<eventMappings>`, `<providers>`a `<rules>` můžete zahrnout další prvky pomocí elementu `<add>`. Chcete-li odebrat nastavení z výchozí konfigurace, použijte element `<remove>`, nebo pomocí `<clear />` odeberte všechny výchozí hodnoty z jedné z těchto oddílů. Pojďme nakonfigurovat webovou aplikaci recenze knih na protokolování všech neošetřených výjimek do databáze Microsoft SQL Server pomocí `SqlWebEventProvider` třídy.

Třída `SqlWebEventProvider` je součástí systému sledování stavu a zapisuje událost monitorování stavu do zadané SQL Server databáze. Třída `SqlWebEventProvider` očekává, že zadaná databáze zahrnuje uloženou proceduru s názvem `aspnet_WebEvent_LogEvent`. Tato uložená procedura se dokončí na podrobnosti události a má na úkol ukládání podrobností události. Dobrá zpráva je, že nemusíte vytvářet tuto uloženou proceduru ani tabulku pro ukládání podrobností události. Tyto objekty můžete přidat do databáze pomocí nástroje `aspnet_regsql.exe`.

> [!NOTE]
> Nástroj `aspnet_regsql.exe` byl v rámci [ *Konfigurace webu, který používá aplikační služby kurz,* ](configuring-a-website-that-uses-application-services-cs.md) až po přidání podpory pro ASP. Aplikační služby netto. V důsledku toho již databáze webu recenzí knihy obsahuje `aspnet_WebEvent_LogEvent` uloženou proceduru, která ukládá informace o událostech do tabulky s názvem `aspnet_WebEvent_Events`.

Jakmile budete mít do své databáze k dispozici veškerou uloženou proceduru a tabulku, je vše, co je potřeba k tomu, aby se do databáze hlásily všechny neošetřené výjimky. To lze provést přidáním následujícího kódu do souboru `Web.config` vašeho webu:

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample2.xml)]

Výše uvedený kód pro konfiguraci sledování stavu používá `<clear />` prvky k vymazání informací o konfiguraci, které jsou předem definované, v sekcích `<eventMappings>`, `<providers>`a `<rules>`. Pak přidá jednu položku do každého z těchto oddílů.

- Element `<eventMappings>` definuje jednu událost monitorování stavu s oznámením s názvem "všechny chyby", která je vyvolána vždy, když dojde k neošetřené výjimce.
- Element `<providers>` definuje jeden zdroj protokolu s názvem "SqlWebEventProvider", který používá třídu `SqlWebEventProvider`. Atribut `connectionStringName` byl nastaven na hodnotu "ReviewsConnectionString", což je název našeho připojovacího řetězce definovaného v části `<connectionStrings>`.
- Nakonec&gt; prvek &lt;Rules označuje, že když událost všechny chyby ukáže, že by měla být protokolovaná pomocí poskytovatele "SqlWebEventProvider".

Tyto informace o konfiguraci instruují systém monitorování stavu, aby protokoloval všechny neošetřené výjimky do databáze recenze knih.

> [!NOTE]
> Událost `WebBaseErrorEvent` je aktivována pouze pro chyby serveru; nejsou vyvolány pro chyby protokolu HTTP, jako je například požadavek na prostředek ASP.NET, který nebyl nalezen. To se liší od chování události `Error` `HttpApplication` třídy, která je vyvolána pro chyby serveru i protokolu HTTP.

Pokud chcete zobrazit systém monitorování stavu v akci, navštivte web a vygenerujte chybu za běhu návštěvou `Genre.aspx?ID=foo`. Měla by se zobrazit příslušná chybová stránka-podrobnosti o výjimce žlutá obrazovka smrti (při místní návštěvě) nebo vlastní chybová stránka (při návštěvě lokality v produkčním prostředí). Na pozadí systém sledování stavu zaznamenal do databáze informace o chybě. V tabulce `aspnet_WebEvent_Events` by měl být jeden záznam (viz **Obrázek 1**); Tento záznam obsahuje informace o běhové chybě, ke které došlo pouze.

[![](logging-error-details-with-asp-net-health-monitoring-cs/_static/image2.png)](logging-error-details-with-asp-net-health-monitoring-cs/_static/image1.png)

**Obrázek 1**: podrobnosti o chybě se zaznamenaly do `aspnet_WebEvent_Events` tabulky.  
([Kliknutím zobrazíte obrázek v plné velikosti.](logging-error-details-with-asp-net-health-monitoring-cs/_static/image3.png))

### <a name="displaying-the-error-log-in-a-web-page"></a>Zobrazení protokolu chyb na webové stránce

V případě aktuální konfigurace webu protokoluje systém monitorování stavu všechny neošetřené výjimky do databáze. Monitorování stavu ale neposkytuje žádný mechanismus pro zobrazení protokolu chyb prostřednictvím webové stránky. Mohli byste však vytvořit stránku ASP.NET, která zobrazí tyto informace z databáze. (Jak budeme pokaždé, když uvidíme za chvíli, můžete se rozhodnout, že budete mít v e-mailové zprávě zasílané podrobnosti o chybě.)

Pokud takovou stránku vytvoříte, ujistěte se, že jste provedli kroky, abyste mohli zobrazit podrobnosti o chybě jenom autorizovaným uživatelům. Pokud vaše lokalita už využívá uživatelské účty, můžete použít autorizační pravidla URL k omezení přístupu k této stránce na určité uživatele nebo role. Další informace o tom, jak udělit nebo omezit přístup k webovým stránkám na základě přihlášeného uživatele, najdete v tématu naše [kurzy zabezpečení webu](../../older-versions-security/introduction/security-basics-and-asp-net-support-cs.md).

> [!NOTE]
> V dalším kurzu se prozkoumá alternativní protokolování chyb a systém oznámení s názvem knihovny ELMAH. KNIHOVNY ELMAH obsahuje integrovaný mechanizmus pro zobrazení protokolu chyb z webové stránky i kanálu RSS.

## <a name="logging-events-to-email"></a>Protokolování událostí do e-mailu

Systém monitorování stavu zahrnuje poskytovatele zdroje protokolu, který protokoluje událost do e-mailové zprávy. Zdroj protokolu obsahuje stejné informace, které se protokolují do databáze v těle e-mailové zprávy. Tento zdroj protokolu můžete použít k upozorňování vývojáře, když dojde k určité události monitorování stavu.

Pojďme aktualizovat konfiguraci webu recenzí recenze, aby obdržení e-mailu vždycky, když dojde k výjimce. K tomu musíme provést tři úkoly:

1. Konfigurace webové aplikace ASP.NET pro odesílání e-mailů To lze provést zadáním způsobu odesílání e-mailových zpráv prostřednictvím elementu konfigurace `<system.net>`. Další informace o posílání e-mailových zpráv v aplikaci ASP.NET najdete [v tématu posílání e-mailů v ASP.NET](http://aspnet.4guysfromrolla.com/articles/072606-1.aspx) a [Nejčastější dotazy k System .NET. mailu](http://systemnetmail.com/).
2. Zaregistrujte poskytovatele zdroje e-mailových protokolů v prvku `<providers>` a
3. Přidejte položku do prvku `<rules>`, který mapuje událost všechny chyby na zprostředkovatele zdroje protokolu přidaný v kroku (2).

Systém monitorování stavu zahrnuje dvě třídy poskytovatele zdrojového e-mailového protokolu: `SimpleMailWebEventProvider` a `TemplatedMailWebEventProvider`. [Třída`SimpleMailWebEventProvider`](https://msdn.microsoft.com/library/system.web.management.simplemailwebeventprovider.aspx) pošle e-mailovou zprávu s prostým textem, která obsahuje podrobnosti o události a poskytuje malé přizpůsobení těla e-mailu. Pomocí [třídy`TemplatedMailWebEventProvider`](https://msdn.microsoft.com/library/system.web.management.templatedmailwebeventprovider.aspx) zadáte stránku ASP.NET, jejíž vykreslený kód slouží jako tělo e-mailové zprávy. [Třída`TemplatedMailWebEventProvider`](https://msdn.microsoft.com/library/system.web.management.templatedmailwebeventprovider.aspx) poskytuje mnohem větší kontrolu nad obsahem a formátem e-mailové zprávy, ale vyžaduje trochu větší práci, protože je třeba vytvořit stránku ASP.NET, která generuje tělo e-mailové zprávy. Tento kurz se zaměřuje na použití `SimpleMailWebEventProvider` třídy.

Aktualizujte `<providers>` prvek systému monitorování stavu v souboru `Web.config` tak, aby zahrnoval zdroj protokolu pro třídu `SimpleMailWebEventProvider`:

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample3.xml)]

Výše uvedený kód používá třídu `SimpleMailWebEventProvider` jako poskytovatele zdroje protokolu a přiřadí mu popisný název "EmailWebEventProvider". Kromě toho atribut `<add>` obsahuje další možnosti konfigurace, jako jsou adresy a a z e-mailové zprávy.

Po definování zdroje protokolu e-mailu je to vše, co je potřeba k tomu, aby systém monitorování stavu používal tento zdroj k neošetřeným výjimkám protokolu. Toho je možné dosáhnout přidáním nového pravidla do části `<rules>`:

[!code-xml[Main](logging-error-details-with-asp-net-health-monitoring-cs/samples/sample4.xml)]

Oddíl `<rules>` nyní obsahuje dvě pravidla. První z nich s názvem "všechny chyby na E-mail" pošle všechny neošetřené výjimky do zdroje protokolu "EmailWebEventProvider". Toto pravidlo má vliv na odeslání podrobností o chybách na webu do zadané adresy. Pravidlo "všechny chyby na databázi" protokoluje podrobnosti o chybě do databáze lokality. V důsledku toho dojde při každém výskytu neošetřené výjimky na webu k tomu, že se v databázi protokolují obě podrobnosti a odešlou se na zadanou e-mailovou adresu.

**Obrázek 2** ukazuje e-mail generovaný při `SimpleMailWebEventProvider` třídy při návštěvě `Genre.aspx?ID=foo`.

[![](logging-error-details-with-asp-net-health-monitoring-cs/_static/image5.png)](logging-error-details-with-asp-net-health-monitoring-cs/_static/image4.png)

**Obrázek 2**: podrobnosti o chybě se odesílají v e-mailové zprávě.  
([Kliknutím zobrazíte obrázek v plné velikosti.](logging-error-details-with-asp-net-health-monitoring-cs/_static/image6.png))

## <a name="summary"></a>Přehled

Systém sledování stavu ASP.NET je navržený tak, aby správcům umožnil monitorovat stav nasazené webové aplikace. Události monitorování stavu jsou vyvolány, když jsou určité akce odložení, například při zastavení aplikace, když se uživatel úspěšně přihlásí k webu nebo když dojde k neošetřené výjimce. Tyto události mohou být protokolovány do libovolného počtu zdrojů protokolů. Tento kurz ukázal, jak protokolovat podrobnosti neošetřených výjimek do databáze a prostřednictvím e-mailové zprávy.

Tento kurz se zaměřuje na použití sledování stavu k protokolování neošetřených výjimek, ale mějte na paměti, že monitorování stavu je navržené tak, aby měřilo celkový stav nasazené aplikace v ASP.NET a zahrnuje širokou řadu událostí monitorování stavu a zdrojů protokolů, které nejsou Prozkoumejte tady. A co víc, můžete vytvořit vlastní události monitorování stavu a zdroje protokolů, které by měly nastat. Pokud vás zajímá Další informace o monitorování stavu, je dobrým prvním krokem Přečtěte si [Nejčastější dotazy k monitorování stavu](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx) [Erik Reitan](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx). Postup najdete v tématu [Postupy: použití monitorování stavu v ASP.NET 2,0](https://msdn.microsoft.com/library/ms998306.aspx).

Šťastné programování!

### <a name="further-reading"></a>Další čtení

Další informace o tématech popsaných v tomto kurzu najdete v následujících zdrojích informací:

- [Přehled monitorování stavu ASP.NET](https://msdn.microsoft.com/library/bb398933.aspx)
- [Konfigurace a přizpůsobení systému monitorování stavu ASP.NET](http://dotnetslackers.com/articles/aspnet/ConfiguringAndCustomizingTheHealthMonitoringSystemOfASPNET.aspx)
- [Nejčastější dotazy týkající se monitorování stavu v ASP.NET 2,0](https://blogs.msdn.com/erikreitan/archive/2006/05/22/603586.aspx)
- [Postupy: odesílání e-mailů pro oznámení monitorování stavu](https://msdn.microsoft.com/library/ms227553.aspx)
- [Postupy: použití monitorování stavu v ASP.NET](https://msdn.microsoft.com/library/ms998306.aspx)
- [Monitorování stavu v ASP.NET](http://aspnet.4guysfromrolla.com/articles/031407-1.aspx)

> [!div class="step-by-step"]
> [Předchozí](processing-unhandled-exceptions-cs.md)
> [Další](logging-error-details-with-elmah-cs.md)

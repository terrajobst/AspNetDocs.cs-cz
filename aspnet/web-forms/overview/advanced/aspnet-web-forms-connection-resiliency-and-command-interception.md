---
uid: web-forms/overview/advanced/aspnet-web-forms-connection-resiliency-and-command-interception
title: Odolnost připojení webových formulářů ASP.NET a zachycení příkazu | Microsoft Docs
author: Erikre
description: V tomto kurzu se dozvíte, jak upravit ukázkovou aplikaci pro podporu odolnosti připojení a zachycení příkazů.
ms.author: riande
ms.date: 03/31/2014
ms.assetid: 6d497001-fa80-4765-b4cc-181fe90b894e
msc.legacyurl: /web-forms/overview/advanced/aspnet-web-forms-connection-resiliency-and-command-interception
msc.type: authoredcontent
ms.openlocfilehash: 95f0b5635c12d5ef88622e5766c1278c6570dd4d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598425"
---
# <a name="aspnet-web-forms-connection-resiliency-and-command-interception"></a>Webové formuláře ASP.NET – odolnost připojení a zachycení příkazů

od [Erik Reitan](https://github.com/Erikre)

V tomto kurzu upravíte ukázkovou aplikaci Wingtip Toys tak, aby podporovala odolnost připojení a zachycení příkazů. Když zapnete odolnost připojení, ukázková aplikace Wingtip Toys automaticky zopakuje volání dat, když dojde k přechodným chybám, které jsou typické pro cloudové prostředí. Při implementaci zachycení příkazu bude také ukázková aplikace Wingtip Toys zachytit všechny dotazy SQL odeslané do databáze, aby je bylo možné protokolovat nebo změnit.

> [!NOTE] 
> 
> Tento kurz webových formulářů byl založen na tom, jak je Dykstra následující kurz MVC:  
> [Odolnost připojení a zachycení příkazů pomocí Entity Framework v aplikaci ASP.NET MVC](../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="what-youll-learn"></a>Naučíte se:

- Jak zajistit odolnost připojení.
- Způsob implementace zachycení příkazu.

## <a name="prerequisites"></a>Předpoklady

Než začnete, ujistěte se, že máte v počítači nainstalovaný následující software:

- [Microsoft Visual Studio 2013](https://www.microsoft.com/visualstudio/11/downloads#vs) nebo [Microsoft Visual Studio Express 2013 pro web](https://www.microsoft.com/visualstudio/11/downloads#express-web). .NET Framework se nainstaluje automaticky.
- Ukázkový projekt Wingtip Toys, abyste mohli implementovat funkce uvedené v tomto kurzu v rámci projektu Wingtip Toys. Následující odkaz poskytuje informace ke stažení:

    - [Začínáme s webovými formuláři ASP.NET 4.5.1 – Wingtip Toys](https://go.microsoft.com/fwlink/?LinkID=389434&amp;clcid=0x409) (C#)
- Před dokončením tohoto kurzu zvažte, jak si můžete projít související řadu kurzů [Začínáme webové formuláře a Visual Studio 2013 ASP.NET 4,5](../getting-started/getting-started-with-aspnet-45-web-forms/introduction-and-overview.md). Série kurzů vám pomůže seznámit se s **WingtipToys** projektem a kódem.

## <a name="connection-resiliency"></a>Odolnost připojení

Když zvažte nasazení aplikace do platformy Windows Azure, jedna z možností, kterou je třeba zvážit, je nasazení databáze do **windows** **Azure SQL Database**, cloudové databázové služby. Přechodné chyby připojení jsou obvykle častější při připojení ke cloudové databázové službě, než když je váš webový server a databázový server přímo propojen ve stejném datovém centru. I v případě, že je cloudový webový server a cloudová databázová služba hostovány ve stejném datovém centru, je mezi nimi více síťových připojení, která mohou mít problémy, jako jsou například nástroje pro vyrovnávání zatížení.

Cloudová služba se většinou sdílí i s ostatními uživateli, což znamená, že jejich odezva může být ovlivněná. A přístup k databázi může být omezen omezením. Omezování znamená, že databázová služba vyvolá výjimky, když se pokusíte o přístup častěji, než je povoleno ve vaší *smlouva SLA* (SLA).

Mnoho nebo více problémů s připojením, ke kterým dochází při přístupu ke cloudové službě, je přechodný, to znamená, že se v krátké době vyřeší samy. Takže když zkusíte databázovou operaci a obdržíte typ chyby, která je obvykle přechodný, zkuste operaci zopakovat po krátkém čekání a operace může být úspěšná. Pokud se pokusíte vyřešit přechodné chyby automatickým opakovaným pokusem, můžete uživatelům poskytnout mnohem lepší možnosti, aby je většina z nich neviditelná pro zákazníka. Funkce odolnosti připojení v Entity Framework 6 automatizuje proces opakování neúspěšných dotazů SQL.

Pro určitou databázovou službu musí být správně nakonfigurovaná funkce odolnosti připojení:

1. Je nutné zjistit, které výjimky budou pravděpodobně přechodné. Chcete opakovat chyby způsobené dočasnou ztrátou v připojení k síti, například chyby způsobené chybami programu.
2. Musí počkat odpovídající dobu mezi opakovanými pokusy operace, která selhala. Můžete počkat mezi opakovanými pokusy dávkového procesu, než můžete pro online webovou stránku, kde uživatel čeká na odpověď.
3. Před tím, než bude zacházet, je nutné opakovat příslušný počet. Je možné, že budete chtít v dávkovém procesu několikrát opakovat pokus o provedení v online aplikaci.

Tato nastavení můžete nakonfigurovat ručně pro jakékoli databázové prostředí podporované poskytovatelem Entity Framework.

K povolení odolnosti proti chybám je možné v sestavení vytvořit třídu, která je odvozená od třídy `DbConfiguration`, a v této třídě nastavte strategii spouštění SQL Database, která v Entity Framework je další termín pro zásady opakování.

### <a name="implementing-connection-resiliency"></a>Implementace odolnosti připojení

1. Stáhněte a otevřete ukázkovou aplikaci webových formulářů [WingtipToys](https://go.microsoft.com/fwlink/?LinkID=389434&amp;clcid=0x409) v aplikaci Visual Studio.
2. Do složky *Logic* aplikace **WingtipToys** přidejte soubor třídy s názvem *WingtipToysConfiguration.cs*.
3. Nahraďte existující kód následujícím kódem:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample1.cs)]

Entity Framework automaticky spustí kód, který najde ve třídě, která je odvozena z `DbConfiguration`. Třídu `DbConfiguration` lze použít k provádění úloh konfigurace v kódu, které byste jinak propadli v souboru *Web. config* . Další informace najdete v tématu [EntityFramework konfigurace na základě kódu](https://msdn.microsoft.com/data/jj680699).

1. Ve složce *Logic* otevřete soubor *AddProducts.cs* .
2. Přidejte příkaz `using` pro `System.Data.Entity.Infrastructure`, jak je vidět zvýrazněný žlutě:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample2.cs?highlight=6)]
3. Do metody `AddProduct` přidejte `catch` blok, aby se `RetryLimitExceededException` protokoloval jako zvýrazněný žlutě:   

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample3.cs?highlight=14-15,17-22)]

Přidáním výjimky `RetryLimitExceededException` můžete poskytnout lepší protokolování nebo zobrazit chybovou zprávu uživateli, kde se můžou rozhodnout zkusit tento proces znovu. Když zachytíte výjimku `RetryLimitExceededException`, všechny chyby, které budou pravděpodobně přechodné, budou již vyzkoušeny a v některých případech se nezdařily. Vlastní vrácená výjimka bude zabalena do výjimky `RetryLimitExceededException`. Kromě toho jste přidali také obecný blok catch. Další informace o výjimce `RetryLimitExceededException` najdete v tématu [Entity Framework odolnost proti chybám připojení a logice opakování](https://msdn.microsoft.com/data/dn456835).

## <a name="command-interception"></a>Zachycení příkazu

Teď, když jste zapnuli zásady opakování, jak otestujete a ověříte, že funguje podle očekávání? Nemusíte tak snadno vynutit přechod k přechodným chybám, zejména pokud pracujete místně, a bylo by obzvláště obtížné integrovat skutečné přechodné chyby do automatizovaného testu jednotek. Chcete-li otestovat funkci odolnost připojení, budete potřebovat způsob, jak zachytit dotazy, které Entity Framework odesílá SQL Server a nahradit odpověď SQL Server typem výjimky, která je obvykle přechodný.

K implementaci osvědčeného postupu pro cloudové aplikace můžete také použít zachycení dotazů: Zaprotokolujte latenci a úspěch nebo neúspěch všech volání externích služeb, jako jsou třeba databázové služby.

V této části kurzu použijete [*funkci zachycení*](https://msdn.microsoft.com/data/dn469464) Entity Framework pro protokolování i pro simulaci přechodných chyb.

### <a name="create-a-logging-interface-and-class"></a>Vytvoření protokolovacího rozhraní a třídy

Osvědčeným postupem pro protokolování je to udělat pomocí [`interface`](https://msdn.microsoft.com/library/ms173156.aspx) namísto volání pevně zakódování do `System.Diagnostics.Trace` nebo třídy protokolování. To usnadňuje změnu mechanismu protokolování později, pokud ho budete potřebovat. Takže v této části vytvoříte protokolovací rozhraní a třídu, která ji implementuje.

Na základě výše uvedeného postupu jste stáhli a otevřeli ukázkovou aplikaci **WingtipToys** v aplikaci Visual Studio.

1. Vytvořte složku v projektu **WingtipToys** a pojmenujte ji *Logging*.
2. Ve složce *protokolování* vytvořte soubor třídy s názvem *ILogger.cs* a nahraďte výchozí kód následujícím kódem:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample4.cs)]

   Rozhraní poskytuje tři úrovně trasování k označení relativní důležitosti protokolů a jednu určenou pro poskytování informací o latenci pro volání externích služeb, jako jsou databázové dotazy. Metody protokolování mají přetížení, které umožňují předat výjimku. To znamená, že informace o výjimce, včetně trasování zásobníku a vnitřních výjimek, jsou spolehlivě protokolovány třídou, která implementuje rozhraní, a nemusíte přitom spoléhat na to, že v každém volání metody protokolování v rámci aplikace.  
  
   Metody `TraceApi` umožňují sledovat latenci každého volání externí služby, jako je například SQL Database.
3. Ve složce *protokolování* vytvořte soubor třídy s názvem *Logger.cs* a nahraďte výchozí kód následujícím kódem:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample5.cs)]

Implementace používá `System.Diagnostics` k trasování. Toto je integrovaná funkce rozhraní .NET, která usnadňuje generování a používání trasovacích informací. Existuje mnoho &quot;naslouchací procesy&quot; můžete použít s trasováním `System.Diagnostics`, k zápisu protokolů do souborů, například nebo k jejich zápisu do úložiště objektů BLOB v systému Windows Azure. Podívejte se na některé z možností a odkazy na další materiály, kde najdete další informace v tématu [řešení potíží s weby Windows Azure v aplikaci Visual Studio](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio). V tomto kurzu se podíváte jenom na protokoly v okně **výstup** sady Visual Studio.

V produkční aplikaci můžete zvážit použití jiných rozhraní trasování než `System.Diagnostics`a rozhraní `ILogger` je poměrně snadné přepnout na jiný mechanismus trasování, pokud se o to rozhodnete.

### <a name="create-interceptor-classes"></a>Vytváření tříd zachytávací

V dalším kroku vytvoříte třídy, které Entity Framework bude volat při každém odeslání dotazu do databáze, jeden pro simulaci přechodných chyb a druhý pro protokolování. Tyto třídy zachytávací musí být odvozeny od třídy `DbCommandInterceptor`. V těchto případech zapíšete přepisy metod, které jsou automaticky volány při spuštění dotazu. V těchto metodách můžete prozkoumávat nebo zaprotokolovat dotaz, který se odesílá do databáze, a můžete změnit dotaz před odesláním do databáze nebo vrátit něco do Entity Framework, aniž byste museli dotaz předat do databáze.

1. Chcete-li vytvořit třídu zachytávací, která bude protokolovat každý dotaz SQL před odesláním do databáze, vytvořte soubor třídy s názvem *InterceptorLogging.cs* ve složce *Logic* a nahraďte výchozí kód následujícím kódem:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample6.cs)]

   Pro úspěšné dotazy nebo příkazy tento kód zapisuje protokol informací s informacemi o latenci. V případě výjimek vytvoří protokol chyb.
2. Chcete-li vytvořit třídu zachytávací, která bude při zadání &quot;throw&quot; do textového pole **název** na stránce s názvem *AdminPage. aspx*vytvořena, vytvořte ve složce *Logic* soubor s názvem *InterceptorTransientErrors.cs* a nahraďte výchozí kód následujícím kódem:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample7.cs)]

    Tento kód Přepisuje pouze metodu `ReaderExecuting`, která je volána pro dotazy, které mohou vracet více řádků dat. Pokud jste chtěli ověřit odolnost připojení pro jiné typy dotazů, můžete také přepsat `NonQueryExecuting` a `ScalarExecuting` metody, protože zachytávací protokolovací modul.  
  
   Později se přihlásíte jako správce a v horním navigačním panelu vyberte odkaz **správce** . Pak na stránce *AdminPage. aspx* přidáte produkt s názvem &quot;throw&quot;. Kód vytvoří fiktivní výjimku SQL Database pro chybu číslo 20, což je známý typ, který je obvykle přechodný. Další čísla chyb, která jsou aktuálně rozpoznaná jako přechodné, jsou 64, 233, 10053, 10054, 10060, 10928, 10929, 40197, 40501 a 40613, ale mohou se změnit v nových verzích SQL Database. Produkt se přejmenuje na "TransientErrorExample", který můžete sledovat v kódu souboru *InterceptorTransientErrors.cs* .  
  
   Kód vrátí výjimku Entity Framework místo spuštění dotazu a předání výsledků zpět. Přechodná výjimka se vrátí *čtyřikrát* a potom se kód vrátí do normálního postupu předávání dotazu do databáze.

    Vzhledem k tomu, že všechno je protokolováno, budete moci zjistit, že Entity Framework se pokusí spustit dotaz čtyřikrát před dokončením a jediným rozdílem v aplikaci je to, že bude trvat déle, než vykreslí stránku s výsledky dotazu.  
  
   Počet opakovaných pokusů, kolikrát se Entity Framework bude konfigurovat; kód určuje čtyřikrát, protože to je výchozí hodnota pro zásady spouštění SQL Database. Pokud změníte zásady spouštění, můžete také změnit kód, který určuje, kolikrát se mají vygenerovat přechodné chyby. Můžete také změnit kód pro generování více výjimek, aby Entity Framework vyvolala výjimku `RetryLimitExceededException`.
3. V *Global. asax*přidejte následující příkazy using:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample8.cs)]
4. Pak přidejte zvýrazněné řádky do metody `Application_Start`:  

    [!code-csharp[Main](aspnet-web-forms-connection-resiliency-and-command-interception/samples/sample9.cs?highlight=17-20)]

Tyto řádky kódu způsobí, že se váš kód pro zachycování spustí, když Entity Framework odesílá dotazy do databáze. Všimněte si, že vzhledem k tomu, že jste vytvořili samostatné třídy zachytávací pro simulaci přechodných chyb a protokolování, můžete je nezávisle povolit a zakázat.   
  
 Můžete přidat zachycení pomocí metody `DbInterception.Add` kdekoli v kódu; nemusí být v metodě `Application_Start`. Další možnost, pokud jste nepřidali zachycení do metody `Application_Start`, by měla aktualizovat nebo přidat třídu s názvem *WingtipToysConfiguration.cs* a umístit výše uvedený kód na konci konstruktoru `WingtipToysConfiguration` třídy.

Bez ohledu na to, jak tento kód vložíte, buďte opatrní, nespouštějte `DbInterception.Add` pro stejný zachytávací více než jednou, nebo získáte další instance zachytávací. Pokud například přidáte zachytávací modul protokolování dvakrát, zobrazí se pro každý dotaz SQL dva protokoly.

Zachycení jsou spouštěna v pořadí podle registrace (pořadí, ve kterém je volána metoda `DbInterception.Add`). Pořadí může být v závislosti na tom, co děláte v rámci zachytávací. Zachytávací modul může například změnit příkaz SQL, který získá ve vlastnosti `CommandText`. Pokud dojde ke změně příkazu SQL, další zachytávací příkaz získá změněný příkaz SQL, nikoli původní příkaz SQL.

Napsali jste kód simulace přechodných chyb způsobem, který umožňuje způsobit přechodné chyby zadáním jiné hodnoty v uživatelském rozhraní. Jako alternativu můžete napsat kód pro zachycování, aby vždy generoval sekvenci přechodných výjimek bez kontroly konkrétní hodnoty parametru. Zachytávací pak můžete přidat jenom v případě, že chcete generovat přechodné chyby. Pokud to uděláte, nepřidáte tento zachytávací až po dokončení inicializace databáze. Jinými slovy, před zahájením generování přechodných chyb udělejte alespoň jednu databázovou operaci, například dotaz na jednu ze sad entit. Entity Framework provede během inicializace databáze několik dotazů a neprovádí se v transakci, takže chyby během inicializace by mohly způsobit nekonzistentní stav kontextu.

## <a name="test-logging-and-connection-resiliency"></a>Protokolování testů a odolnost připojení

1. V aplikaci Visual Studio stiskněte klávesu **F5** a spusťte aplikaci v režimu ladění a potom se přihlaste jako "admin" pomocí "Pa $ $Word" jako hesla.
2. V horním navigačním panelu vyberte **správce** .
3. Zadejte nový produkt s názvem throw s příslušným popisem, ceníkem a souborem s obrázkem.
4. Stiskněte tlačítko **Přidat produkt** .  
   Všimněte si, že v prohlížeči se zdá, že při Entity Framework opakovaném pokusu o dotaz na několik sekund přestane reagovat. K prvnímu opakování dochází velmi rychle, čekání se ještě před každým dalším opakováním poroste. Tento proces čekání je delší, než se každé opakování nazývá *exponenciální omezení rychlosti* .
5. Počkejte, dokud se stránka nebude pokoušet o načtení.
6. Pokud chcete zobrazit výstup trasování, zastavte projekt a podívejte se do okna **výstup** sady Visual Studio. Okno **výstup** můžete najít tak, že vyberete **ladění** -&gt; **Windows** -&gt; **výstup**. Možná budete muset přejít do několika dalších protokolů zapsaných protokolovacím nástrojem.  
  
   Všimněte si, že můžete zobrazit skutečné dotazy SQL odeslané do databáze. Zobrazí se některé úvodní dotazy a příkazy, které Entity Framework provede, když se zkontroluje verze databáze a tabulka historie migrace.   
    ![Okno Výstup](aspnet-web-forms-connection-resiliency-and-command-interception/_static/image1.png)   
   Všimněte si, že tento test nemůžete opakovat, dokud aplikaci nezastavíte a nerestartujete. Pokud jste chtěli mít v jednom spuštění aplikace víckrát testovat odolnost připojení, mohli byste napsat kód pro resetování čítače chyb v `InterceptorTransientErrors`.
7. Chcete-li zobrazit rozdíl v strategii provádění (zásady opakování), odkomentujte `SetExecutionStrategy` řádek v souboru *WingtipToysConfiguration.cs* ve složce *Logic* , spusťte znovu stránku **správce** v režimu ladění a přidejte produkt s názvem &quot;znovu vyvolejte&quot;.  
  
   Tentokrát se ladicí program zastaví na první vygenerované výjimce okamžitě při pokusu o spuštění dotazu poprvé.  
    ![Ladění-Podrobnosti zobrazení](aspnet-web-forms-connection-resiliency-and-command-interception/_static/image2.png)
8. Odkomentujte `SetExecutionStrategy` řádek v souboru *WingtipToysConfiguration.cs* .

## <a name="summary"></a>Souhrn

V tomto kurzu jste viděli, jak upravit ukázkovou aplikaci webových formulářů pro podporu odolnosti připojení a zachycení příkazů.

## <a name="next-steps"></a>Další kroky

Po kontrole odolnosti připojení a zachycení příkazu ve webových formulářích ASP.NET si přečtěte téma webové formuláře ASP.NET [asynchronní metody v ASP.NET 4,5](../performance-and-caching/using-asynchronous-methods-in-aspnet-45.md). Téma vás seznámí se základy vytváření asynchronní aplikace webových formulářů ASP.NET pomocí sady Visual Studio.

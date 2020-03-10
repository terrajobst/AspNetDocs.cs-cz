---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application
title: 'Kurz: použití odolnosti připojení a zachycení příkazů s EF v aplikaci ASP.NET MVC'
author: tdykstra
description: V tomto kurzu se dozvíte, jak používat odolnost připojení a zachycení příkazů. Jsou to dvě důležité funkce Entity Framework 6.
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: c89d809f-6c65-4425-a3fa-c9f6e8ac89f2
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 276266f8ae9df38529d44742ebe6ac0dc8e79727
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583452"
---
# <a name="tutorial-use-connection-resiliency-and-command-interception-with-entity-framework-in-an-aspnet-mvc-app"></a>Kurz: použití odolnosti připojení a zachycení příkazů s Entity Framework v aplikaci ASP.NET MVC

Proto byla aplikace spuštěna místně v IIS Express ve vývojovém počítači. Chcete-li zajistit, aby byla skutečná aplikace k dispozici ostatním uživatelům pro použití přes Internet, je nutné ji nasadit na poskytovatele hostování webů a je nutné nasadit databázi na databázový server.

V tomto kurzu se dozvíte, jak používat odolnost připojení a zachycení příkazů. Jsou to dvě důležité funkce Entity Framework 6, které jsou obzvláště důležité při nasazení do cloudového prostředí: odolnost připojení (automatické opakování pro přechodné chyby) a zachycení příkazu (zachycení všech dotazů SQL odeslaných do databáze. aby bylo možné je zaznamenat nebo změnit).

V tomto kurzu je tato odolnost připojení a zachycení příkazu volitelná. Pokud tento kurz přeskočíte, bude nutné provést několik menších úprav v následujících kurzech.

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Povolit odolnost připojení
> * Povolit zachycení příkazu
> * Otestování nové konfigurace

## <a name="prerequisites"></a>Předpoklady

* [Řazení, filtrování a stránkování](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="enable-connection-resiliency"></a>Povolit odolnost připojení

Když nasadíte aplikaci do Windows Azure, nasadíte databázi do Windows Azure SQL Database, cloudové databázové služby. Přechodné chyby připojení jsou obvykle častější při připojení ke cloudové databázové službě, než když je váš webový server a databázový server přímo propojen ve stejném datovém centru. I v případě, že je cloudový webový server a cloudová databázová služba hostovány ve stejném datovém centru, je mezi nimi více síťových připojení, která mohou mít problémy, jako jsou například nástroje pro vyrovnávání zatížení.

Cloudová služba se většinou sdílí i s ostatními uživateli, což znamená, že jejich odezva může být ovlivněná. A přístup k databázi může být omezen omezením. Omezování znamená, že databázová služba vyvolá výjimky, když se pokusíte o přístup častěji, než je povoleno ve vaší smlouva SLA (SLA).

Velký počet problémů s připojením při přístupu ke cloudové službě je přechodný, to znamená, že se v krátké době vyřeší sami. Takže když zkusíte databázovou operaci a obdržíte typ chyby, která je obvykle přechodný, zkuste operaci zopakovat po krátkém čekání a operace může být úspěšná. Pokud se pokusíte vyřešit přechodné chyby automatickým opakovaným pokusem, můžete uživatelům poskytnout mnohem lepší možnosti, aby je většina z nich neviditelná pro zákazníka. Funkce odolnosti připojení v Entity Framework 6 automatizuje proces opakování neúspěšných dotazů SQL.

Pro určitou databázovou službu musí být správně nakonfigurovaná funkce odolnosti připojení:

- Je nutné zjistit, které výjimky budou pravděpodobně přechodné. Chcete opakovat chyby způsobené dočasnou ztrátou v připojení k síti, například chyby způsobené chybami programu.
- Musí počkat odpovídající dobu mezi opakovanými pokusy operace, která selhala. Můžete počkat mezi opakovanými pokusy dávkového procesu, než můžete pro online webovou stránku, kde uživatel čeká na odpověď.
- Před tím, než bude zacházet, je nutné opakovat příslušný počet. Je možné, že budete chtít v dávkovém procesu několikrát opakovat pokus o provedení v online aplikaci.

Tato nastavení můžete nakonfigurovat ručně pro jakékoli databázové prostředí podporované poskytovatelem Entity Framework, ale výchozí hodnoty, které obvykle fungují dobře pro online aplikaci, která používá Windows Azure SQL Database, už jsou pro vás nakonfigurované a Toto jsou nastavení, která implementujete pro aplikaci Contoso University.

Pro povolení odolnosti připojení je v sestavení vytvořená třída, která je odvozená od třídy [DbConfiguration](https://msdn.microsoft.com/data/jj680699.aspx) , a v této třídě nastavte *strategii spouštění*SQL Database, která je v EF pro *zásady opakování*další.

1. Ve složce DAL přidejte soubor třídy s názvem *SchoolConfiguration.cs*.
2. Nahraďte kód šablony následujícím kódem:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

    Entity Framework automaticky spustí kód, který najde ve třídě, která je odvozena z `DbConfiguration`. Třídu `DbConfiguration` lze použít k provádění úloh konfigurace v kódu, které byste jinak propadli v souboru *Web. config* . Další informace najdete v tématu [EntityFramework konfigurace na základě kódu](https://msdn.microsoft.com/data/jj680699).
3. Do *StudentController.cs*přidejte příkaz `using` pro `System.Data.Entity.Infrastructure`.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]
4. Změňte všechny bloky `catch`, které zachycují výjimky `DataException` tak, aby se místo toho zachytily `RetryLimitExceededException` výjimky. Příklad:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=1)]

    Používali jste `DataException` k pokusu o identifikaci chyb, které by mohly být přechodné, aby se vytvořila Popisná zpráva "zkusit znovu". Ale teď, když jste zapnuli zásady opakování, budou se už jenom chyby, které se pravděpodobně dočasná, vyzkoušely a nemusely být úspěšné a vlastní vrácená výjimka se zabalí do `RetryLimitExceededException` výjimky.

Další informace najdete v tématu [Entity Framework odolnost proti chybám připojení a logice opakování](https://msdn.microsoft.com/data/dn456835).

## <a name="enable-command-interception"></a>Povolit zachycení příkazu

Teď, když jste zapnuli zásady opakování, jak otestujete a ověříte, že funguje podle očekávání? Nemusíte tak snadno vynutit přechod k přechodným chybám, zejména pokud pracujete místně, a bylo by obzvláště obtížné integrovat skutečné přechodné chyby do automatizovaného testu jednotek. Chcete-li otestovat funkci odolnost připojení, budete potřebovat způsob, jak zachytit dotazy, které Entity Framework odesílá SQL Server a nahradit odpověď SQL Server typem výjimky, která je obvykle přechodný.

K implementaci osvědčeného postupu pro cloudové aplikace můžete také použít zachycení dotazů: [Zaprotokolujte latenci a úspěch nebo neúspěch všech volání externích služeb](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log) , jako jsou třeba databázové služby. EF6 poskytuje [vyhrazené rozhraní API pro protokolování](https://msdn.microsoft.com/data/dn469464) , které může zjednodušit protokolování, ale v této části kurzu se naučíte, jak používat [funkci zachycení](https://msdn.microsoft.com/data/dn469464) Entity Framework přímo, jak pro protokolování, tak pro simulaci přechodných chyb.

### <a name="create-a-logging-interface-and-class"></a>Vytvoření protokolovacího rozhraní a třídy

[Osvědčeným postupem pro protokolování](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/monitoring-and-telemetry.md#log) je to udělat pomocí rozhraní, nikoli prostřednictvím pevného kódování volání System. Diagnostics. Trace nebo třídy protokolování. To usnadňuje změnu mechanismu protokolování později, pokud ho budete potřebovat. Takže v této části vytvoříte protokolovací rozhraní a třídu, která ji implementuje./p >

1. Vytvořte v projektu složku a pojmenujte ji *Logging*.
2. Ve složce *protokolování* vytvořte soubor třídy s názvem *ILogger.cs*a nahraďte kód šablony následujícím kódem:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

    Rozhraní poskytuje tři úrovně trasování k označení relativní důležitosti protokolů a jednu určenou pro poskytování informací o latenci pro volání externích služeb, jako jsou databázové dotazy. Metody protokolování mají přetížení, které umožňují předat výjimku. To znamená, že informace o výjimce, včetně trasování zásobníku a vnitřních výjimek, jsou spolehlivě protokolovány třídou, která implementuje rozhraní, a nemusíte přitom spoléhat na to, že v každém volání metody protokolování v rámci aplikace.

    Metody TraceApi umožňují sledovat latenci každého volání externí služby, jako je například SQL Database.
3. Ve složce *protokolování* vytvořte soubor třídy s názvem *Logger.cs*a nahraďte kód šablony následujícím kódem:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

    Implementace používá pro trasování System. Diagnostics. Toto je integrovaná funkce rozhraní .NET, která usnadňuje generování a používání trasovacích informací. Existuje mnoho "posluchačů", které můžete použít s trasováním System. Diagnostics, k zápisu protokolů do souborů, například nebo k jejich zápisu do úložiště objektů BLOB v Azure. Podívejte se na některé z možností a odkazy na další materiály, kde najdete další informace v tématu [řešení potíží s weby Azure v aplikaci Visual Studio](https://docs.microsoft.com/azure/app-service-web/web-sites-dotnet-troubleshoot-visual-studio). V tomto kurzu se podíváte jenom na protokoly v okně **výstup** sady Visual Studio.

    V produkční aplikaci si možná budete chtít vzít v úvahu jiné trasovací balíčky než System. Diagnostics a rozhraní ILogger je poměrně snadné přepnout na jiný mechanismus trasování, pokud se o to rozhodnete.

### <a name="create-interceptor-classes"></a>Vytváření tříd zachytávací

V dalším kroku vytvoříte třídy, které Entity Framework zavolá na pokaždé, když pošle dotaz do databáze, jednu pro simulaci přechodných chyb a jeden pro protokolování. Tyto třídy zachytávací musí být odvozeny od třídy `DbCommandInterceptor`. V nich zapíšete přepsání metod, která jsou automaticky volána, když bude dotaz proveden. V těchto metodách můžete prozkoumávat nebo zaprotokolovat dotaz, který se odesílá do databáze, a můžete změnit dotaz před odesláním do databáze nebo vrátit něco do Entity Framework, aniž byste museli dotaz předat do databáze.

1. Chcete-li vytvořit třídu zachytávací, která bude protokolovat každý dotaz SQL, který je odeslán do databáze, vytvořte soubor třídy s názvem *SchoolInterceptorLogging.cs* ve složce *dal* a nahraďte kód šablony následujícím kódem:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

    Pro úspěšné dotazy nebo příkazy tento kód zapisuje protokol informací s informacemi o latenci. V případě výjimek vytvoří protokol chyb.
2. Chcete-li vytvořit třídu zachytávací, která bude při zadání příkazu throw do **vyhledávacího** pole generovat fiktivní přechodné chyby, vytvořte soubor třídy s názvem *SchoolInterceptorTransientErrors.cs* ve složce *dal* a nahraďte kód šablony následujícím kódem:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

    Tento kód Přepisuje pouze metodu `ReaderExecuting`, která je volána pro dotazy, které mohou vracet více řádků dat. Pokud jste chtěli ověřit odolnost připojení pro jiné typy dotazů, můžete také přepsat `NonQueryExecuting` a `ScalarExecuting` metody, protože zachytávací protokolovací modul.

    Když spustíte stránku student a jako hledaný řetězec zadáte throw, tento kód vytvoří fiktivní výjimku SQL Database pro chybu číslo 20, což je známý typ, který je obvykle přechodný. Další čísla chyb, která jsou aktuálně rozpoznaná jako přechodné, jsou 64, 233, 10053, 10054, 10060, 10928, 10929, 40197, 40501 a 40613, ale mohou se změnit v nových verzích SQL Database.

    Kód vrátí výjimku Entity Framework místo spuštění dotazu a předání výsledků dotazu zpět. Přechodná výjimka se vrátí čtyřikrát a potom se kód vrátí do normálního postupu předávání dotazu do databáze.

    Vzhledem k tomu, že všechno je protokolováno, budete moci zjistit, že Entity Framework se pokusí spustit dotaz čtyřikrát před dokončením a jediným rozdílem v aplikaci je to, že bude trvat déle, než vykreslí stránku s výsledky dotazu.

    Počet opakovaných pokusů, kolikrát se Entity Framework bude konfigurovat; kód určuje čtyřikrát, protože to je výchozí hodnota pro zásady spouštění SQL Database. Pokud změníte zásady spouštění, můžete také změnit kód, který určuje, kolikrát se mají vygenerovat přechodné chyby. Můžete také změnit kód pro generování více výjimek, aby Entity Framework vyvolala výjimku `RetryLimitExceededException`.

    Hodnota, kterou zadáte do vyhledávacího pole, bude `command.Parameters[0]` a `command.Parameters[1]` (jedna se použije pro křestní jméno a jeden pro příjmení). Při nalezení hodnoty "% throw%" je "throw" nahrazen v těchto parametrech "a", takže někteří studenti budou nalezeni a vráceni.

    Toto je pouze pohodlný způsob, jak otestovat odolnost připojení na základě změny nějakého vstupu v uživatelském rozhraní aplikace. Můžete také napsat kód, který generuje přechodné chyby pro všechny dotazy nebo aktualizace, jak je vysvětleno dále v komentářích k metodě *DbInterception. Add* .
3. V *Global. asax*přidejte následující příkazy `using`:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]
4. Přidejte zvýrazněné řádky do metody `Application_Start`:

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs?highlight=7-8)]

    Tyto řádky kódu způsobí, že se váš kód pro zachycování spustí, když Entity Framework odesílá dotazy do databáze. Všimněte si, že vzhledem k tomu, že jste vytvořili samostatné třídy zachytávací pro simulaci přechodných chyb a protokolování, můžete je nezávisle povolit a zakázat.

    Můžete přidat zachycení pomocí metody `DbInterception.Add` kdekoli v kódu; nemusí být v metodě `Application_Start`. Další možností je vložit tento kód do třídy DbConfiguration, kterou jste vytvořili dříve, a nakonfigurovat zásady spouštění.

    [!code-csharp[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs?highlight=6-7)]

    Bez ohledu na to, jak tento kód vložíte, buďte opatrní, nespouštějte `DbInterception.Add` pro stejný zachytávací více než jednou, nebo získáte další instance zachytávací. Pokud například přidáte zachytávací modul protokolování dvakrát, zobrazí se pro každý dotaz SQL dva protokoly.

    Zachycení jsou spouštěna v pořadí podle registrace (pořadí, ve kterém je volána metoda `DbInterception.Add`). Pořadí může být v závislosti na tom, co děláte v rámci zachytávací. Zachytávací modul může například změnit příkaz SQL, který získá ve vlastnosti `CommandText`. Pokud dojde ke změně příkazu SQL, další zachytávací příkaz získá změněný příkaz SQL, nikoli původní příkaz SQL.

    Napsali jste kód simulace přechodných chyb způsobem, který umožňuje způsobit přechodné chyby zadáním jiné hodnoty v uživatelském rozhraní. Jako alternativu můžete napsat kód pro zachycování, aby vždy generoval sekvenci přechodných výjimek bez kontroly konkrétní hodnoty parametru. Zachytávací pak můžete přidat jenom v případě, že chcete generovat přechodné chyby. Pokud to uděláte, nepřidáte tento zachytávací až po dokončení inicializace databáze. Jinými slovy, před zahájením generování přechodných chyb udělejte alespoň jednu databázovou operaci, například dotaz na jednu ze sad entit. Entity Framework provede během inicializace databáze několik dotazů a neprovádí se v transakci, takže chyby během inicializace by mohly způsobit nekonzistentní stav kontextu.

## <a name="test-the-new-configuration"></a>Otestování nové konfigurace

1. Stisknutím klávesy **F5** spusťte aplikaci v režimu ladění a potom klikněte na kartu **studenti** .
2. Podívejte se na výstup trasování v okně **výstup** sady Visual Studio. Možná se budete muset posunout o některé chyby JavaScriptu, abyste se dostali do protokolů zapsaných protokolovacím nástrojem.

    Všimněte si, že můžete zobrazit skutečné dotazy SQL odeslané do databáze. Zobrazí se některé úvodní dotazy a příkazy, které Entity Framework Začínáme, Kontrola verze databáze a tabulky historie migrace (v dalším kurzu se dozvíte o migraci). A zobrazí se dotaz na stránkování, kde zjistíte, kolik studentů existuje, a nakonec se zobrazí dotaz, který získá data studenta.

    ![Protokolování pro normální dotaz](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)
3. Na stránce **Students** zadejte jako hledaný řetězec "throw" a klikněte na **Hledat**.

    ![Vyvolat hledaný řetězec](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

    Všimněte si, že v prohlížeči se zdá, že při Entity Framework opakovaném pokusu o dotaz na několik sekund přestane reagovat. K prvnímu opakování dochází velmi rychle, čekání před tím, než se provede každé další opakování. Tento proces čekání je delší, než se každé opakování nazývá *exponenciální omezení rychlosti*.

    Po zobrazení stránky se zobrazí studenty, které mají ve svém jménu "a", podívejte se do okna výstup a uvidíte, že se stejný dotaz pokusy nastavil pětkrát, přičemž první čtyři časy vrací přechodné výjimky. Pro každou přechodnou chybu se zobrazí protokol, který píšete při generování přechodné chyby ve třídě `SchoolInterceptorTransientErrors` ("vracející přechodnou chybu pro příkaz..."), a když `SchoolInterceptorLogging` získá výjimku, zobrazí se protokol.

    ![Výstup protokolování ukazující opakované pokusy](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

    Vzhledem k tomu, že jste zadali hledaný řetězec, dotaz, který vrací údaje o studentech, je parametrizovaný:

    [!code-sql[Main](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.sql)]

    Nezaznamenáváte hodnotu parametrů, ale můžete to provést. Pokud chcete zobrazit hodnoty parametrů, můžete napsat kód protokolování pro získání hodnot parametrů z vlastnosti `Parameters` objektu `DbCommand`, který získáte v metodách pro zachycování.

    Všimněte si, že tento test nemůžete opakovat, dokud aplikaci nezastavíte a nerestartujete. Pokud jste chtěli mít v jednom spuštění aplikace víckrát testovat odolnost připojení, mohli byste napsat kód pro resetování čítače chyb v `SchoolInterceptorTransientErrors`.
4. Pokud chcete zobrazit rozdíl v rámci strategie provádění (zásady opakování), odkomentujte `SetExecutionStrategy` řádek v *SchoolConfiguration.cs*, znovu spusťte stránku students v režimu ladění a znovu vyhledejte "throw".

    Tentokrát se ladicí program zastaví na první vygenerované výjimce okamžitě při pokusu o spuštění dotazu poprvé.

    ![Fiktivní výjimka](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)
5. Odkomentujte *SetExecutionStrategy* čáru v *SchoolConfiguration.cs*.

## <a name="get-the-code"></a>Získání kódu

[Stáhnout dokončený projekt](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>Další zdroje

Odkazy na další prostředky Entity Framework najdete v [prostředcích, které jsou doporučeny pro přístup k datům ASP.NET](../../../../whitepapers/aspnet-data-access-content-map.md).

## <a name="next-steps"></a>Další kroky

V tomto kurzu se naučíte:

> [!div class="checklist"]
> * Povolená odolnost připojení
> * Povolení zachycení příkazu
> * Otestování nové konfigurace

V dalším článku se dozvíte, jak Code First migrace a nasazení Azure.
> [!div class="nextstepaction"]
> [Code First migrace a nasazení Azure](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)

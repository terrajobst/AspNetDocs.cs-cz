---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
title: 'Příloha: Ukázková aplikace pro opravu IT (vytváření skutečných cloudových aplikací s Azure) | Microsoft Docs'
author: MikeWasson
description: Vytváření reálných cloudových aplikací pomocí Azure je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které mohou...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 1bc333c5-f096-4ea7-b170-779accc21c1a
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/the-fix-it-sample-application
msc.type: authoredcontent
ms.openlocfilehash: e6fda47babd3c2505315f42667c45f09482218c2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74583749"
---
# <a name="appendix-the-fix-it-sample-application-building-real-world-cloud-apps-with-azure"></a>Příloha: Ukázková aplikace pro opravu IT (vytváření skutečných cloudových aplikací s Azure)

[Jan Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Dykstra](https://github.com/tdykstra)

[Stáhnout opravit projekt IT](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)

> **Vytváření reálných cloudových aplikací pomocí Azure** je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které vám pomůžou úspěšně vyvíjet webové aplikace pro Cloud. Informace o elektronické příručce najdete v [první kapitole](introduction.md).

Tento dodatek k vytváření reálných cloudových aplikací pomocí Azure obsahuje následující oddíly, které obsahují další informace o ukázkové aplikaci pro opravu IT, kterou si můžete stáhnout:

- [Známé problémy](#knownissues)
- [Osvědčené postupy](#bestpractices)
- [Jak spustit aplikaci ze sady Visual Studio na místním počítači](#run-in-vs)
- [Postup nasazení základní aplikace pro Azure App Service Web Apps pomocí skriptů prostředí Windows PowerShell](#deploybase)
- [Řešení potíží se skripty prostředí Windows PowerShell](#troubleshooting)
- [Nasazení aplikace se zpracováním fronty pro Azure App Service Web Apps a cloudovou službu Azure](#deployqueues)

<a id="knownissues"></a>
## <a name="known-issues"></a>Známé problémy

Oprava IT aplikace byla původně vyvinuta, aby se co nejvíce zobrazovalo jako některé ze vzorů uvedených v této elektronické knize. Vzhledem k tomu, že elektronická kniha se chystá sestavovat reálné aplikace, jsme zjistili, že tento kód opravujeme do procesu kontroly a testování podobně jako v případě vydaných softwaru. Zjistili jsme řadu problémů a stejně jako u jakékoli reálné aplikace jsme opravili některé z nich a některé z nich jsme odložili na pozdější verzi.

Následující seznam obsahuje problémy, které by se měly řešit v produkční aplikaci, ale z jednoho důvodu nebo jiného rozhodla neřešit v počáteční verzi ukázkové aplikace této opravy.

### <a name="security"></a>Zabezpečení –

- Ujistěte se, že nemůžete přiřadit úkol neexistujícímu vlastníkovi.
- Ujistěte se, že můžete zobrazovat a upravovat jenom úkoly, které jste vytvořili nebo vám byly přiřazeni.
- Pro přihlašovací stránky a soubory cookie pro ověřování použijte protokol HTTPS.
- Zadejte časový limit pro soubory cookie ověřování.

### <a name="input-validation"></a>Ověřování vstupu

Obecně platí, že produkční aplikace by prověřila více ověřování vstupu než aplikace opravit IT. Například velikost souboru obrázku nebo obrázku, která je povolena pro nahrávání, by měla být omezená.

### <a name="administrator-functionality"></a>Funkce Správce

Správce by měl být schopný měnit vlastnictví u stávajících úloh. Například tvůrce úlohy může opustit společnost, přičemž nikdo nebude mít oprávnění k údržbě úlohy, pokud není povolen přístup pro správu.

### <a name="queue-message-processing"></a>Zpracování zprávy ve frontě

Zpracování zprávy ve frontě v aplikaci Fix it bylo navrženo tak, aby bylo znázorněno jako jednoduché pro ilustraci vzoru práce orientovaného na fronty s minimálním množstvím kódu. Tento jednoduchý kód by neměl být vhodný pro skutečnou produkční aplikaci.

- Kód nezaručuje, že každá zpráva fronty bude zpracována pouze jednou. Když dostanete zprávu z fronty, dojde k vypršení časového limitu, během kterého je zpráva neviditelná pro ostatní naslouchací procesy front. Pokud časový limit vyprší před odstraněním zprávy, bude zpráva opět viditelná. Proto pokud instance role pracovního procesu stráví dlouhou dobu zpracováním zprávy, je teoreticky možné, že se stejnou zprávu zpracuje dvakrát a výsledkem je duplicitní úloha v databázi. Další informace o tomto problému najdete v tématu [použití Azure Storagech front](https://msdn.microsoft.com/library/ff803365.aspx#sec7).
- Logika cyklického dotazování fronty by mohla být cenově výhodnější díky dávkovému načítání zpráv. Pokaždé, když zavoláte [CloudQueue. GetMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessageasync.aspx), bude se jednat o transakční náklady. Místo toho můžete volat [CloudQueue. GetMessagesAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.getmessagesasync.aspx) (Všimněte si plural '), který získá více zpráv v jedné transakci. Náklady na transakce pro fronty Azure Storage jsou velmi nízké, takže dopad na náklady není ve většině případů podstatný.
- Těsná smyčka ve frontě kódu pro zpracování zpráv způsobuje spřažení PROCESORů, což efektivně nevyužívá virtuální počítače s více jádry. Lepší návrh by používal úlohu paralelismu k paralelnímu spuštění několika asynchronních úloh.
- Zpracování zprávy ve frontě má pouze zpracování výjimek základní. Kód například nezpracovává [poškozené zprávy](https://msdn.microsoft.com/library/ms789028.aspx). (Pokud zpracování zprávy způsobí výjimku, musíte chybu zaprotokolovat a zprávu odstranit, nebo se role pracovního procesu pokusí o její zpracování znovu a smyčka bude pokračovat po dobu neurčitou.)

### <a name="sql-queries-are-unbounded"></a>Dotazy SQL jsou bez vazby.

Aktuální kód opravy neomezuje počet řádků, které mohou vracet dotazy na stránky indexu. Pokud je do databáze vložen velký objem úloh, může dojít k problémům s výkonem v případě, že velikost výsledných seznamů byla přijata. Řešením je implementovat stránkování. Příklad najdete v tématu [řazení, filtrování a stránkování s Entity Framework v aplikaci ASP.NET MVC](../../../../mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application.md).

### <a name="view-models-recommended"></a>Doporučené modely zobrazení

Aplikace Fix it používá třídu entity FixItTask k předávání informací mezi kontrolkou a zobrazením. Osvědčeným postupem je použití modelů zobrazení. Doménový model (např. Třída entity FixItTask) je navržený kolem toho, co je potřeba pro trvalost dat, zatímco model zobrazení může být navržený pro prezentaci dat. Další informace najdete v článku o [osvědčených postupech pro ASP.NET MVC](https://codeclimber.net.nz/archive/2009/10/27/12-asp.net-mvc-best-practices.aspx).

### <a name="secure-image-blob-recommended"></a>Doporučuje se objekt BLOB zabezpečeného obrazu.

Oprava IT aplikace ukládá nahrané obrázky jako veřejné, což znamená, že přístup k obrázkům má kdokoli, kdo najde adresu URL. Image se můžou zabezpečit místo veřejného.

### <a name="no-powershell-automation-scripts-for-queues"></a>Žádné skripty automatizace PowerShellu pro fronty

Ukázkové skripty PowerShellu pro automatizaci byly zapsány pouze pro základní verzi, která ji spouští zcela v Azure App Service Web Apps. Neposkytli jsme skripty pro nastavení a nasazení webové aplikace a prostředí cloudové služby, které je potřeba pro zpracování fronty.

### <a name="special-handling-for-html-codes-in-user-input"></a>Speciální zpracování kódů HTML ve vstupu uživatele

ASP.NET automaticky zabraňuje mnoha způsobům, jak se mohou uživatelé zlými úmysly pokusit o útoky prostřednictvím skriptování mezi weby zadáním skriptu do textových polí vstupu uživatele. A Pomocník pro MVC `DisplayFor`, který slouží k zobrazení názvů úkolů a poznámek, automaticky kóduje kód HTML, který posílá do prohlížeče. V produkční aplikaci ale možná budete chtít provést další měření. Další informace najdete v tématu [žádosti o ověření v ASP.NET](https://msdn.microsoft.com/library/hh882339.aspx).

<a id="bestpractices"></a>
## <a name="best-practices"></a>Osvědčené postupy

Níže jsou uvedené některé problémy, které byly opraveny po zjištění v revizi kódu a testování původní verze aplikace pro opravu IT. Některé byly způsobeny tím, že původní programátor si nevědí o konkrétním osvědčeném postupu. stačí, když kód byl rychle napsán a nebyl určen pro vydaný software. Zde uvedené problémy uvádíme v případě, že se něco naučilo z této recenze a testování, které by mohlo být užitečné pro ostatní, kteří také vyvíjí webové aplikace.

### <a name="dispose-the-database-repository"></a>Uvolnit úložiště databáze

Třída `FixItTaskRepository` musí uvolnit instanci Entity Framework `DbContext`. Provedli jsme to implementací `IDisposable` ve třídě `FixItTaskRepository`:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample1.cs)]

Všimněte si, že AutoFac automaticky odstraní instanci `FixItTaskRepository`, takže ji nemusíme explicitně vyřadit.

Další možností je odebrat `DbContext` členskou proměnnou z `FixItTaskRepository`a místo toho vytvořit místní `DbContext` proměnnou v rámci každé metody úložiště uvnitř příkazu `using`. Příklad:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample2.cs)]

### <a name="register-singletons-as-such-with-di"></a>Zaregistrujte singleton jako například pomocí DI.

Vzhledem k tomu, že je potřeba jenom jedna instance třídy `PhotoService` a `Logger` třídy, měly by se tyto třídy [zaregistrovat jako samostatné instance pro vkládání závislostí](https://code.google.com/p/autofac/wiki/InstanceScope) v *DependenciesConfig.cs*:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample3.cs?highlight=1,3)]

### <a name="security-dont-show-error-details-to-users"></a>Zabezpečení: Nezobrazovat podrobnosti o chybách uživatelům

Původní aplikace Fix it neobsahovala obecnou chybovou stránku, takže všechny výjimky, jako například chyby připojení k databázi, by mohly vést k zobrazení úplného trasování zásobníku v prohlížeči. Podrobné informace o chybě mohou někdy usnadnit útoky uživatelů se zlými úmysly. Řešením je zaprotokolovat podrobnosti výjimky a zobrazit uživateli chybovou stránku, která neobsahuje podrobnosti o chybě. V souboru Web. config jsme doplnili `<customErrors mode=On>` opravit IT aplikaci a aby se zobrazila chybová stránka.

[!code-xml[Main](the-fix-it-sample-application/samples/sample4.xml?highlight=2)]

Ve výchozím nastavení to způsobí, že se *Views\Shared\Error.cshtml* zobrazí chyby. Můžete přizpůsobit *Error. cshtml* nebo vytvořit vlastní zobrazení chybové stránky a přidat atribut `defaultRedirect`. Můžete také zadat různé chybové stránky pro konkrétní chyby.

### <a name="security-only-allow-a-task-to-be-edited-by-its-creator"></a>Zabezpečení: umožňuje pouze upravovat úkol tvůrcem.

Stránka index řídicího panelu zobrazuje jenom úkoly vytvořené přihlášeným uživatelem, ale uživatel se zlými úmysly může vytvořit adresu URL s ID pro úlohu jiného uživatele. Do *DashboardController.cs* jsme přidali kód, který vrátí 404 v tomto případě:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample5.cs?highlight=9-14,24-29)]

### <a name="dont-swallow-exceptions"></a>Bez požití výjimek

Původní aplikace, která ji opravila, vrátila po protokolování výjimky, která byla výsledkem dotazu SQL, jenom null:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample6.cs?highlight=4)]

To by mělo vypadat uživateli, jako kdyby dotaz uspěl, ale nevrátil žádné řádky. Řešením je znovu vyvolat výjimku po zachycení a protokolování:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample7.cs)]

### <a name="catch-all-exceptions-in-worker-roles"></a>Zachytit všechny výjimky v rolích pracovního procesu

Jakékoli neošetřené výjimky v roli pracovního procesu způsobí, že se virtuální počítač recykluje, takže budete chtít zabalit všechno, co děláte do bloku try-catch, a zpracovat všechny výjimky.

### <a name="specify-length-for-string-properties-in-entity-classes"></a>Zadat délku pro vlastnosti řetězce v třídách entit

Aby bylo možné zobrazit jednoduchý kód, původní verze aplikace, ve které se tato oprava nezměnila, nespecifikuje délky polí FixItTask entity a v důsledku toho byly definovány jako varchar (max) v databázi. V důsledku toho uživatelské rozhraní přijme skoro jakékoli množství vstupu. Určení délek nastaví omezení, která platí pro vstup uživatele na webové stránce a v velikosti sloupce v databázi:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample8.cs?highlight=4,7,10,12,14)]

### <a name="mark-private-members-as-readonly-when-they-arent-expected-to-change"></a>Označit soukromé členy jako jen pro čtení, pokud se neočekává změna

Například ve třídě `DashboardController` je vytvořena instance `FixItTaskRepository`, která se neočekává, že se změní, takže jsme ji definovali jako [jen pro čtení](https://msdn.microsoft.com/library/acdd6hb7.aspx).

[!code-csharp[Main](the-fix-it-sample-application/samples/sample9.cs?highlight=3)]

### <a name="use-listany-instead-of-listcount-gt-0"></a>Použijte seznam. Any () místo seznamu. Count () &gt; 0

Pokud vás zajímá, že jedna nebo více položek v seznamu odpovídají zadaným kritériím, použijte metodu [Any](https://msdn.microsoft.com/library/bb534972.aspx) , protože se vrátí hned po nalezení položky, zatímco metoda `Count` vždy musí iterovat všemi položkami. V souboru *. cshtml s indexem* řídicího panelu byl původně tento kód:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample10.cshtml)]

Změnili jsme to na toto:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample11.cshtml?highlight=1)]

### <a name="generate-urls-in-mvc-views-using-mvc-helpers"></a>Generování adres URL v zobrazeních MVC pomocí pomocníků MVC

V případě tlačítka pro **Vytvoření opravy** na domovské stránce se v aplikaci oprava, která je pevně zakóduje, dopravuje element kotvy:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample12.cshtml)]

U odkazů na zobrazení a akce, jako je to, je vhodnější použít [adresu URL.](https://msdn.microsoft.com/library/system.web.mvc.urlhelper.action.aspx) pomocník HTML, například:

[!code-cshtml[Main](the-fix-it-sample-application/samples/sample13.cshtml)]

### <a name="use-taskdelay-instead-of-threadsleep-in-worker-role"></a>Použijte Task. Delay místo Thread. spánek v roli pracovního procesu.

Šablona New-Project vloží `Thread.Sleep` do vzorového kódu pro roli pracovního procesu, ale způsobí, že vlákno do režimu spánku může způsobit, že fond vláken vytvoří další zbytečná vlákna. K tomu se můžete vyhnout pomocí [Task. Delay](https://msdn.microsoft.com/library/hh139096.aspx) místo.

[!code-csharp[Main](the-fix-it-sample-application/samples/sample14.cs?highlight=11)]

### <a name="avoid-async-void"></a>Vyhnout se asynchronnímu anulování

Pokud asynchronní metoda nepotřebuje vracet hodnotu, vraťte `Task` typ místo `void`.

Tento příklad je z `FixItQueueManager` třídy:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample15.cs)]

`async void` byste měli použít pouze pro obslužné rutiny událostí nejvyšší úrovně. Pokud definujete metodu jako `async void`, volající nemůže **očekávat** metodu nebo zachytit jakékoli výjimky, které metoda vyvolá. Další informace najdete v tématu [osvědčené postupy při asynchronním programování](https://msdn.microsoft.com/magazine/jj991977.aspx).

### <a name="use-a-cancellation-token-to-break-from-worker-role-loop"></a>Přerušení od smyčky role pracovního procesu pomocí tokenu zrušení

Metoda **Run** v roli pracovního procesu obvykle obsahuje nekonečnou smyčku. Při zastavování role pracovního procesu je volána metoda [RoleEntryPoint. stop](https://msdn.microsoft.com/library/windowsazure/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx) . Tuto metodu byste měli použít, chcete-li zrušit práci prováděnou uvnitř metody **Run** a řádně skončit. V opačném případě se může proces ukončit uprostřed operace.

### <a name="opt-out-of-automatic-mime-sniffing-procedure"></a>Odsouhlasit automatický postup sledování MIME

V některých případech Internet Explorer hlásí typ MIME odlišný od typu určeného webovým serverem. Pokud například Internet Explorer najde obsah ve formátu HTML v souboru dodaném pomocí Content-Type hlavičky HTTP odpovědi: text/prostý, aplikace Internet Explorer určí, že by měl být obsah vykreslen jako HTML. Bohužel to může vést k problémům zabezpečení pro servery hostující nedůvěryhodný obsah. Internet Explorer 8 pro boj proti tomuto problému provedl řadu změn kódu pro určení typu MIME a umožňuje vývojářům aplikací [Odhlásit se pomocí sledování MIME](https://blogs.msdn.com/b/ie/archive/2008/07/02/ie8-security-part-v-comprehensive-protection.aspx). Do souboru *Web. config* byl přidán následující kód.

[!code-xml[Main](the-fix-it-sample-application/samples/sample16.xml?highlight=2-7)]

### <a name="enable-bundling-and-minification"></a>Povolení sdružování a minifikace

Když Visual Studio vytvoří nový webový projekt, sdružování a minifikace souborů JavaScriptu není ve výchozím nastavení povolené. Do BundleConfig.cs jsme přidali řádek kódu:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample17.cs?highlight=9)]

### <a name="set-an-expiration-time-out-for-authentication-cookies"></a>Nastavení časového limitu vypršení platnosti pro soubory cookie ověřování

Ve výchozím nastavení vyprší platnost souborů cookie ověřování za dva týdny. Kratší doba je bezpečnější. Toto nastavení můžete změnit v *StartupAuth.cs*:

[!code-csharp[Main](the-fix-it-sample-application/samples/sample18.cs?highlight=4-5)]

<a id="run-in-vs"></a>
## <a name="how-to-run-the-app-from-visual-studio-on-your-local-computer"></a>Jak spustit aplikaci ze sady Visual Studio na místním počítači

Existují dva způsoby, jak spustit aplikaci pro opravu IT:

- Spusťte základní aplikaci, která zapisuje nové úkoly přímo do databáze SQL.
- Spusťte aplikaci pomocí fronty a služby back-end pro vytváření úloh. Vzor fronty je popsaný v kapitole [vzor práce orientované na fronty](queue-centric-work-pattern.md).

<a id="runbase"></a>
### <a name="run-the-base-application"></a>Spuštění základní aplikace

1. Nainstalujte [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).
2. Nainstalujte [sadu Azure SDK pro .NET pro Visual Studio](https://azure.microsoft.com/downloads/).
3. Stáhněte soubor. zip z [Galerie kódu na webu MSDN](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4).
4. V Průzkumníku souborů klikněte pravým tlačítkem na soubor. zip a klikněte na vlastnosti a pak v okno Vlastnosti klikněte na odblokovat.
5. Rozbalte soubor.
6. Dvojím kliknutím na soubor. sln spustíte Visual Studio.
7. V nabídce **nástroje** klikněte na **Správce balíčků NuGet**a pak na **Konzola správce balíčků**.
8. V konzole správce balíčků (PMC) klikněte na obnovit.
9. Ukončete aplikaci Visual Studio.
10. Spusťte [emulátor úložiště Azure](/azure/storage/common/storage-use-emulator).
11. Restartujte Visual Studio a otevřete soubor řešení, který jste uzavřeli v předchozím kroku.
12. Zajistěte, aby byl projekt FixIt nastaven jako spouštěný projekt, a potom stisknutím kombinace kláves CTRL + F5 spusťte projekt.

<a id="queueslocal"></a>
### <a name="run-the-application-with-queue-processing"></a>Spuštění aplikace se zpracováním fronty

1. Postupujte podle pokynů pro [spuštění základní aplikace](#runbase)a pak zavřete prohlížeč a zavřete Visual Studio.
2. Spusťte aplikaci Visual Studio s oprávněními správce. (Budete používat emulátor služby Azure COMPUTE, který vyžaduje oprávnění správce.)
3. V souboru *Web. config* aplikace v projektu *MyFixIt* (webový projekt) změňte hodnotu `appSettings/UseQueues` na "true":

    [!code-console[Main](the-fix-it-sample-application/samples/sample19.cmd?highlight=3)]
4. Pokud [emulátor úložiště Azure](https://msdn.microsoft.com/library/windowsazure/hh403989.aspx) stále není spuštěný, spusťte ho znovu.
5. Spusťte webový projekt FixIt a projekt MyFixItCloudService současně.

    Pomocí sady Visual Studio:

   1. Stisknutím klávesy **F5** spusťte projekt fixit.
   2. V **Průzkumník řešení**klikněte pravým tlačítkem myši na projekt MyFixItCloudService a potom klikněte na položku **ladit** > **spustit novou instanci**.

    Použití Visual Studio 2013 Express pro web:

   3. V Průzkumník řešení klikněte pravým tlačítkem na řešení FixIt a vyberte **vlastnosti**.
   4. Vyberte **více projektů po spuštění**.
   5. V rozevíracím seznamu **Akce** pod položkou MyFixIt a MyFixItCloudService vyberte **Spustit**.
   6. Klikněte na tlačítko **OK**.
   7. Stiskněte klávesu **F5** pro spuštění obou projektů.

      Když spustíte projekt MyFixItCloudService, Visual Studio spustí emulátor služby COMPUTE pro Azure. V závislosti na konfiguraci brány firewall možná budete muset zapnout emulátor přes bránu firewall.

<a id="deploybase"></a>
## <a name="how-to-deploy-the-base-app-to-azure-app-service-web-apps-by-using-the-windows-powershell-scripts"></a>Postup nasazení základní aplikace pro Azure App Service Web Apps pomocí skriptů prostředí Windows PowerShell

K ilustraci modelu [Automatizace všeho](automate-everything.md) se poskytuje oprava IT aplikace pomocí skriptů, které nastaví prostředí v Azure a nasadí projekt do nového prostředí. Následující pokyny vysvětlují, jak používat skripty.

Pokud chcete provozovat v Azure bez použití front a jste udělali změny, které se mají spouštět místně s frontami, před pokračováním v následujících pokynech nastavte hodnotu UseQueues appSetting zpět na false.

Tyto pokyny předpokládají, že jste už stáhli a spustili řešení opravit IT místně a že máte účet Azure, nebo máte předplatné Azure, které máte autorizované na správu.

1. Nainstalujte konzolu **Azure PowerShell** . Pokyny najdete v tématu [instalace a konfigurace Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1).

    Tato přizpůsobená konzola je nakonfigurovaná tak, aby fungovala s předplatným Azure. Modul Azure se nainstaluje v adresáři *Program Files* a automaticky se naimportuje při každém použití konzoly Azure PowerShell.

    Pokud dáváte přednost práci v jiném hostitelském programu, například Integrované skriptovací prostředí (ISE) v prostředí Windows PowerShell, nezapomeňte pomocí rutiny [Import-Module](https://go.microsoft.com/fwlink/?LinkID=141553) naimportovat modul Azure nebo pomocí příkazu v modulu Azure aktivovat automatický import modulu.
2. Spusťte Azure PowerShell s možností **Spustit jako správce** .
3. Spuštěním rutiny [Set-ExecutionPolicy](https://go.microsoft.com/fwlink/p/?linkid=293941) nastavte zásady spouštění Azure PowerShell na `RemoteSigned`. Zadejte **Y** (pro Ano), aby se změna zásad dokončila.

    [!code-console[Main](the-fix-it-sample-application/samples/sample20.cmd)]

    Toto nastavení umožňuje spustit místní skripty, které nejsou digitálně podepsané. (Můžete také nastavit zásady spouštění na `Unrestricted`, což eliminuje nutnost zrušit krok odblokování později, ale z bezpečnostních důvodů to nedoporučujeme.)
4. Spuštěním rutiny `Add-AzureAccount` nastavte PowerShell s přihlašovacími údaji pro váš účet.

    [!code-console[Main](the-fix-it-sample-application/samples/sample21.cmd)]

    Platnost těchto přihlašovacích údajů vyprší po uplynutí určité doby a je nutné znovu spustit rutinu `Add-AzureAccount`. Jak je tato elektronická kniha zapisována, časový limit před vypršením platnosti přihlašovacích údajů je 12 hodin.
5. Pokud máte více předplatných, pomocí rutiny Select-AzureSubscription určete předplatné, ve kterém chcete vytvořit testovací prostředí.
6. Importujte certifikát pro správu pro stejné předplatné Azure pomocí rutin `Get-AzurePublishSettingsFile` a `Import-AzurePublishSettingsFile`. První z těchto rutin stáhne soubor certifikátu a v druhém případě určí umístění tohoto souboru, aby jej bylo možné importovat. > [!IMPORTANT]
   > Uložte stažený soubor v bezpečném umístění nebo ho odstraňte, až budete s ním hotový, protože obsahuje certifikát, který se dá použít ke správě služeb Azure.

    [!code-console[Main](the-fix-it-sample-application/samples/sample22.cmd)]

    Certifikát se používá pro volání REST API, které detekuje IP adresu vývojového počítače, aby bylo možné nastavit pravidlo brány firewall na serveru SQL Database.
7. Spuštěním rutiny [set-Location](https://go.microsoft.com/fwlink/p/?linkid=293912) (aliasy jsou `cd`, `chdir`a `sl`) přejděte do adresáře, který obsahuje skripty. (Nacházejí se ve složce *Automation* ve složce řešení pro opravu IT.) Pokud název adresáře obsahuje mezery, vložte cestu do uvozovek. Pokud například chcete přejít do adresáře `c:\Sample Apps\FixIt\Automation`, můžete zadat následující příkaz:

    [!code-console[Main](the-fix-it-sample-application/samples/sample23.cmd)]
8. Pokud chcete, aby Windows PowerShell mohl spouštět tyto skripty, použijte rutinu [odblokování souboru](https://go.microsoft.com/fwlink/p/?linkid=294021) . (Skripty jsou blokované, protože byly staženy z Internetu.)

    > [!WARNING]
    > Zabezpečení – před spuštěním `Unblock-File` na jakémkoli skriptu nebo spustitelném souboru otevřete soubor v programu Poznámkový blok, Projděte příkazy a ověřte, zda neobsahují škodlivý kód.

    Například následující příkaz spustí rutinu `Unblock-File` na všech skriptech v aktuálním adresáři.

    [!code-console[Main](the-fix-it-sample-application/samples/sample24.cmd)]
9. Chcete-li vytvořit webovou aplikaci pro základní (bez zpracování fronty), spusťte skript pro vytvoření prostředí.

    Požadovaný parametr `Name` Určuje název databáze a používá se také pro účet úložiště, který skript vytvoří. Název musí být globálně jedinečný v rámci domény azurewebsites.net. Pokud zadáte název, který není jedinečný, například fixit nebo test (nebo dokonce jako v příkladu fixitdemo), rutina `New-AzureWebsite` se nezdařila s vnitřní chybou, která hlásí konflikt. Skript převede název na všechna malá písmena, aby splňoval požadavky na název pro webové aplikace, účty úložiště a databáze.

    Požadovaný parametr `SqlDatabasePassword` Určuje heslo pro účet správce, který se vytvoří pro SQL Database. V hesle Nepoužívejte speciální znaky XML (&amp; &lt; &gt;;). Toto je omezení způsobu, jakým byly skripty zapsány, nikoli omezení Azure.

    Například pokud chcete vytvořit webovou aplikaci s názvem "fixitdemo" a použít SQL Server heslo správce "Passw0rd1", můžete zadat následující příkaz:

    [!code-console[Main](the-fix-it-sample-application/samples/sample25.cmd)]

    Název musí být v doméně azurewebsites.net jedinečný a heslo musí splňovat SQL Database požadavky na složitost hesla. (Vzorový Passw0rd1 splňuje požadavky.)

    Všimněte si, že příkaz začíná na.\". Aby se zabránilo škodlivému spouštění skriptů, Windows PowerShell vyžaduje, abyste při spuštění skriptu zadali úplnou cestu k souboru skriptu. Pomocí tečky můžete označit aktuální adresář (".\") nebo zadejte plně kvalifikovanou cestu, například:

    [!code-console[Main](the-fix-it-sample-application/samples/sample26.cmd)]

    Další informace o skriptu získáte pomocí rutiny `Get-Help`.

    [!code-console[Main](the-fix-it-sample-application/samples/sample27.cmd)]

    Pomocí parametrů `Detailed`, `Full`, `Parameters`a `Examples` rutiny Get-Help můžete vyfiltrovat vrácenou nápovědu.

    Pokud se skript nepovede nebo dojde k chybě, například "New-AzureWebsite: Call set-AzureSubscription a SELECT-AzureSubscription First", možná jste nedokončili konfiguraci Azure PowerShell.

    Po dokončení skriptu můžete pomocí Portál pro správu Azure zobrazit prostředky, které byly vytvořeny, jak je znázorněno v části [automatizovat vše](automate-everything.md) .
10. K nasazení projektu FixIt do nového prostředí Azure použijte skript *AzureWebsite. ps1* . Příklad:

    [!code-console[Main](the-fix-it-sample-application/samples/sample28.cmd)]

    Po dokončení nasazení se otevře prohlížeč s opravou, která běží v Azure.

<a id="troubleshooting"></a>
## <a name="troubleshooting-the-windows-powershell-scripts"></a>Řešení potíží se skripty prostředí Windows PowerShell

Nejběžnější chyby zjištěné při spuštění těchto skriptů souvisejí s oprávněními. Ujistěte se, že `Add-AzureAccount` a `Import-AzurePublishSettingsFile` byly úspěšné a že jste je použili pro stejné předplatné Azure. I v případě, že `Add-AzureAccount` bylo úspěšné, může být nutné ji znovu spustit. Oprávnění přidaná `Add-AzureAccount` vyprší za 12 hodin.

### <a name="object-reference-not-set-to-an-instance-of-an-object"></a>Odkaz na objekt není nastaven na instanci objektu.

Pokud skript vrátí chyby, například "odkaz na objekt není nastaven na instanci objektu", což znamená, že Windows PowerShell nemůže najít objekt, který se má zpracovat (Jedná se o výjimku s nulovým odkazem), spusťte rutinu `Add-AzureAccount` a zkuste skript znovu.

[!code-console[Main](the-fix-it-sample-application/samples/sample29.cmd)]

### <a name="internalerror-the-server-encountered-an-internal-error"></a>InternalError: na serveru došlo k vnitřní chybě.

Rutina `New-AzureWebsite` vrátí vnitřní chybu, pokud název není jedinečný v doméně azurewebsites.net. Chcete-li vyřešit tuto chybu, použijte jinou hodnotu pro název, který je v parametru název *New-AzureWebsiteEnv. ps1*.

[!code-console[Main](the-fix-it-sample-application/samples/sample30.cmd)]

### <a name="restarting-the-script"></a>Restartování skriptu

Pokud potřebujete skript *New-AzureWebsiteEnv. ps1* restartovat, protože se nezdařil před tím, než se vytiskla zpráva "skript je dokončen", možná budete chtít odstranit prostředky, které skript vytvořil před jeho zastavením. Pokud například skript již vytvořil webovou aplikaci ContosoFixItDemo a znovu spustíte skript se stejným názvem, skript se nezdaří, protože název se používá.

Chcete-li zjistit, které prostředky skript vytvořil před jeho zastavením, použijte následující rutiny:

- `Get-AzureWebsite`
- `Get-AzureSqlDatabaseServer`
- `Get-AzureSqlDatabase`: Chcete-li spustit tuto rutinu, přesměrujte název databázového serveru na `Get-AzureSqlDatabase`: `Get-AzureSqlDatabaseServer | Get-AzureSqlDatabase.`

K odstranění těchto prostředků použijte následující příkazy. Pamatujte na to, že při odstranění databázového serveru automaticky odstraníte databáze přidružené k tomuto serveru.

- `Get-AzureWebsite -Name <WebsiteName> | Remove-AzureWebsite`
- `Get-AzureSqlDatabase -Name <DatabaseName> -ServerName <DatabaseServerName> | Remove-SqlAzureDatabase`
- `Get-AzureSqlDatabaseServer | Remove-AzureSqlDatabaseServer`

<a id="deployqueues"></a>
## <a name="how-to-deploy-the-app-with-queue-processing-to-azure-app-service-web-apps-and-an-azure-cloud-service"></a>Nasazení aplikace se zpracováním fronty pro Azure App Service Web Apps a cloudovou službu Azure

Pokud chcete povolit fronty, proveďte v souboru MyFixIt\Web.config následující změny. V části `appSettings`změňte hodnotu `UseQueues` na "true":

[!code-xml[Main](the-fix-it-sample-application/samples/sample31.xml)]

Pak nasaďte aplikaci MVC do webové aplikace v Azure App Service, jak je popsáno [výše](#deploybase).

Pak vytvořte novou cloudovou službu Azure. Skripty, které jsou součástí aplikace Fix it, nevytvářejí ani nesazují cloudovou službu, takže je pro ně nutné použít Azure Portal. Na portálu klikněte na **nový** -- **COMPUTE** – **cloudová služba** -- **rychlé vytvoření**a pak zadejte adresu URL a umístění datového centra. Použijte stejné datové centrum, kde jste nasadili webovou aplikaci.

![](the-fix-it-sample-application/_static/image1.png)

Než budete moct nasadit cloudovou službu, musíte aktualizovat některé konfigurační soubory.

V MyFixIt. WorkerRole\app.config v části `connectionStrings`nahraďte hodnotu připojovacího řetězce `appdb` skutečným připojovacím řetězcem pro SQL Database. Připojovací řetězec můžete získat z portálu. Na portálu klikněte na **databáze SQL** - **appdb** - **zobrazení SQL Database připojovacích řetězců pro ADO .NET, ODBC, php a JDBC**. Zkopírujte připojovací řetězec ADO.NET a vložte hodnotu do souboru App. config. Nahraďte heslo "{Your\_Password\_sem}" heslem databáze. (Za předpokladu, že jste použili skripty pro nasazení aplikace MVC, zadali jste heslo databáze do parametru skriptu `SqlDatabasePassword`.)

Výsledek by měl vypadat takto:

[!code-xml[Main](the-fix-it-sample-application/samples/sample32.xml)]

Ve stejném souboru MyFixIt. WorkerRole\app.config v části `appSettings`nahraďte dvě zástupné hodnoty pro účet služby Azure Storage.

[!code-xml[Main](the-fix-it-sample-application/samples/sample33.xml?highlight=2-3)]

Přístupovou klávesu můžete získat z portálu. Viz [jak spravovat účty úložiště](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).

V MyFixItCloudService\ServiceConfiguration.Cloud.cscfg nahraďte stejné dvě hodnoty zástupných symbolů pro účet služby Azure Storage.

[!code-xml[Main](the-fix-it-sample-application/samples/sample34.xml?highlight=3)]

Teď jste připraveni nasadit cloudovou službu. V prozkoumávání řešení klikněte pravým tlačítkem myši na projekt MyFixItCloudService a vyberte **publikovat**. Další informace najdete v tématu[nasazení aplikace do Azure](https://www.windowsazure.com/develop/net/tutorials/multi-tier-web-site/2-download-and-run/#deployAz), které je v části 2 [tohoto kurzu](https://code.msdn.microsoft.com/Windows-Azure-Multi-Tier-eadceb36).

> [!div class="step-by-step"]
> [Předchozí](more-patterns-and-guidance.md)

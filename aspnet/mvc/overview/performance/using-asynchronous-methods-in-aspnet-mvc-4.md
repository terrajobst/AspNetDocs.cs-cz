---
uid: mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4
title: Použití asynchronních metod v ASP.NET MVC 4 | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se naučíte základy vytváření asynchronní webové aplikace ASP.NET MVC pomocí Visual Studio Express 2012 pro web, což je zdarma...
ms.author: riande
ms.date: 06/06/2012
ms.assetid: a56572ba-81c3-47af-826d-941e9c4775ec
msc.legacyurl: /mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 5df6a9c136b1934b3afd731eb0ceac1e0faa483e
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/15/2019
ms.locfileid: "74115077"
---
# <a name="using-asynchronous-methods-in-aspnet-mvc-4"></a>Použití asynchronních metod v ASP.NET MVC 4

Od [Rick Anderson]((https://twitter.com/RickAndMSFT))

> V tomto kurzu se naučíte základy vytváření asynchronní webové aplikace ASP.NET MVC pomocí [Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/11), což je bezplatná verze Microsoft Visual Studio. Můžete také použít [Visual Studio 2012](https://www.microsoft.com/visualstudio/11).
> 
> Pro tento kurz na GitHubu je k dispozici kompletní ukázka [https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET/)

Třída [kontroleru](https://msdn.microsoft.com/library/system.web.mvc.controller(VS.108).aspx) ASP.NET MVC 4 v kombinaci [.NET 4,5](https://msdn.microsoft.com/library/w0x726c2(VS.110).aspx) umožňuje psát asynchronní metody akcí, které vracejí objekt typu [Task&lt;ActionResult&gt;](https://msdn.microsoft.com/library/dd321424(VS.110).aspx). .NET Framework 4 představila asynchronní programovací koncept, který je označován jako [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) a ASP.NET MVC [4.](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) Úkoly jsou reprezentovány typem **úkolu** a souvisejícími typy v oboru názvů [System. Threading. Tasks](https://msdn.microsoft.com/library/system.threading.tasks.aspx) . .NET Framework 4,5 sestaví k této asynchronní podpoře s klíčovým slovem [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) a [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) , která umožňují pracovat s objekty [úlohy](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) mnohem méně složitější než předchozí asynchronní přístupy. Klíčové slovo [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) je syntaktická zkratka pro značící, že část kódu by měla asynchronně čekat na nějakou jinou část kódu. Klíčové slovo [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) představuje pomocný parametr, který můžete použít k označení metod jako asynchronních metod založených na úlohách. Kombinace **operátoru await**, **Async**a objektu **Task** usnadňuje psaní asynchronního kódu v rozhraní .NET 4,5. Nový model pro asynchronní metody se nazývá *asynchronní vzor založený na úlohách* (**klepněte**). V tomto kurzu se předpokládá, že máte zkušenosti s asynchronním programováním pomocí klíčových slov [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) a [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) a oboru názvů [úkolu](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) .

Další informace o klíčovém slově [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) a [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) a oboru názvů [úkolů](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) naleznete v následujících odkazech.

- [Dokument White Paper: asynchronii v .NET](https://go.microsoft.com/fwlink/?LinkId=204844)
- [Nejčastější dotazy k Async/await](https://blogs.msdn.com/b/pfxteam/archive/2012/04/12/10293335.aspx)
- [Asynchronní programování v aplikaci Visual Studio](https://msdn.microsoft.com/vstudio/gg316360)

## <a id="HowRequestsProcessedByTP"></a>Způsob zpracování požadavků fondem vláken

Na webovém serveru .NET Framework udržuje fond vláken, která se používají k obsluhování požadavků ASP.NET. Když požadavek dorazí, vlákno z fondu se odešle do zpracování tohoto požadavku. Pokud je požadavek zpracováván synchronně, vlákno, který zpracovává požadavek, je při zpracování žádosti zaneprázdněno a vlákno nemůže obsluhovat jiný požadavek.   
  
Nemusí se jednat o problém, protože fond vláken je možné dostatečně velký, aby se vešel do mnoha zaneprázdněných vláken. Počet vláken ve fondu vláken je ale omezený (výchozí maximum pro .NET 4,5 je 5 000). Ve velkých aplikacích s vysokou souběžnou délkou dlouhotrvajících požadavků můžou být všechna dostupná vlákna zaneprázdněná. Tato podmínka se označuje jako vyčerpání vlákna. Po dosažení tohoto stavu vyřadí webové servery požadavky. Pokud se fronta požadavků zaplní, webový server odmítne žádosti se stavem HTTP 503 (Server je příliš zaneprázdněný). Fond vláken CLR má omezení pro vkládání nových vláken. Pokud je souběžnost souběžnosti (to znamená, že váš web může náhle obdržet velký počet požadavků) a že všechna dostupná vlákna požadavků jsou zaneprázdněna z důvodu back-endu s vysokou latencí, může vaše aplikace velmi špatně reagovat. Každé nové vlákno přidané do fondu vláken má navíc režii (například 1 MB paměti zásobníku). Webová aplikace, která používá synchronní metody pro obsluhu vysoké latence, kdy se fond vláken zvětšuje na standard .NET 4,5, ve výchozím nastavení maximum je 5 000 vláken, což by využilo přibližně 5 GB paměti, než je aplikace schopná, aby služba používala stejné požadavky. asynchronní metody a jenom 50 vláken. Při asynchronní práci nepoužíváte vždy vlákno. Například při provádění asynchronní žádosti webové služby nebude ASP.NET používat žádná vlákna mezi voláním **asynchronní** metody a **await**. Použití fondu vláken ke zpracování žádostí s vysokou latencí může způsobit velké nároky na paměť a špatné využití hardwaru serveru.

## <a name="processing-asynchronous-requests"></a>Zpracování asynchronních požadavků

Ve webové aplikaci, která vidí velký počet souběžných požadavků při spuštění nebo má zátěžové zatížení (kde se souběžně roste souběžně), provádí volání webové služby asynchronní odezvu aplikace. Asynchronní požadavek trvá zpracování jako synchronní požadavek stejným časem. Pokud požadavek provede volání webové služby, které vyžaduje dokončení dvou sekund, požadavek trvá dvě sekundy, ať už se provádí synchronně nebo asynchronně. Během asynchronního volání ale vlákno neblokuje reakci na jiné požadavky, zatímco čeká na dokončení první žádosti. Asynchronní požadavky proto zabraňují zařazování požadavků a nárůstu fondu vláken, pokud existuje celá řada souběžných požadavků, které spouštějí dlouhotrvající operace.

## <a id="ChoosingSyncVasync"></a>Výběr metod synchronní nebo asynchronní akce

V této části jsou uvedeny pokyny pro použití synchronních nebo asynchronních metod akcí. Jsou to jenom pokyny. Prověřte každou aplikaci jednotlivě a určete, zda asynchronní metody pomůžou s výkonem.

Obecně platí, že použijte synchronní metody pro následující podmínky:

- Operace jsou jednoduché nebo krátkodobé.
- Jednoduchost je důležitější než efektivita.
- Operace jsou primárně operace CPU místo operací, které zahrnují velký výkon disku nebo síťové režie. Použití asynchronních metod akcí na operacích vázaných na procesor poskytuje žádné výhody a má za následek větší režii.

Obecně použijte asynchronní metody pro následující podmínky:

- Voláte služby, které mohou být spotřebovány prostřednictvím asynchronních metod, a používáte rozhraní .NET 4,5 nebo vyšší.
- Operace jsou vázané na síť nebo vstupně-výstupní operace, nikoli vázané na procesor.
- Paralelismus je důležitější než jednoduchost kódu.
- Chcete poskytnout mechanismus, který umožňuje uživatelům zrušit dlouho běžící požadavek.
- Pokud výhoda přepínání vláken převáží náklady na přepínač kontextu. Obecně byste měli provést asynchronní metodu, pokud synchronní metoda čeká na vlákno žádosti ASP.NET, zatímco neprovádí žádnou práci. Provedením asynchronního volání není vlákno žádosti ASP.NET zastaveno, protože čeká na dokončení žádosti webové služby.
- Testování ukazuje, že blokující operace jsou kritické pro výkon lokality a že služba IIS může obsluhovat více požadavků pomocí asynchronních metod pro tato blokující volání.

Ukázka ke stažení ukazuje, jak efektivně používat asynchronní metody akcí. Uvedená ukázka byla navržena tak, aby poskytovala jednoduchou ukázku asynchronního programování v ASP.NET MVC 4 pomocí .NET 4,5. Vzorek není určen jako referenční architektura pro asynchronní programování v ASP.NET MVC. Vzorový program volá metody [ASP.NET webového rozhraní API](../../../web-api/index.md) , které zavolají [Task. Delay](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) pro simulaci dlouhotrvajících volání webové služby. Většina produkčních aplikací nebude zobrazovat takové zjevné výhody použití asynchronních metod akcí.   
  
Několik aplikací vyžaduje, aby všechny metody akcí byly asynchronní. Často převod několika synchronních metod akcí na asynchronní metody poskytuje nejlepší zvýšení efektivity pro požadovanou práci.

## <a id="SampleApp"></a>Ukázková aplikace

Ukázkovou aplikaci si můžete stáhnout z [https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET) na webu [GitHub](https://github.com/) . Úložiště se skládá ze tří projektů:

- *Mvc4Async*: projekt ASP.NET MVC 4 obsahující kód použitý v tomto kurzu. Provádí volání rozhraní Web API ke službě **WebAPIpgw** .
- *WebAPIpgw*: projekt webového rozhraní API ASP.NET MVC 4, který implementuje řadiče `Products, Gizmos and Widgets`. Poskytuje data pro projekt *WebAppAsync* a projekt *Mvc4Async* .
- *WebAppAsync*: projekt webových formulářů ASP.NET použitý v jiném kurzu.

## <a id="GizmosSynch"></a>Metoda synchronní akce Gizma

 Následující kód ukazuje metodu `Gizmos` synchronní akci, která se používá k zobrazení seznamu gizma. (Pro tento článek je Gizmo fiktivní mechanické zařízení.) 

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample1.cs)]

Následující kód ukazuje metodu `GetGizmos` služby Gizmo.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample2.cs)]

Metoda `GizmoService GetGizmos` předává identifikátor URI službě HTTP webového rozhraní API ASP.NET, která vrací seznam dat gizma. Projekt *WebAPIpgw* obsahuje implementaci `gizmos, widget` webového rozhraní API a `product`ch řadičů.  
Na následujícím obrázku je znázorněno zobrazení gizma z ukázkového projektu.

![Gizma](using-asynchronous-methods-in-aspnet-mvc-4/_static/image1.png)

## <a id="CreatingAsynchGizmos"></a>Vytvoření asynchronní metody akce Gizma

Ukázka používá nová klíčová slova [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) a [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) (k dispozici v rozhraních .NET 4,5 a Visual Studio 2012), aby kompilátor mohl být zodpovědný za údržbu složitých transformací potřebných pro asynchronní programování. Kompilátor umožňuje psát kód pomocí C#konstrukce asynchronního toku řízení a kompilátor automaticky aplikuje transformace potřebné k použití zpětných volání, aby nedocházelo k blokování vláken.

Následující kód ukazuje `Gizmos` synchronní metodu a `GizmosAsync` asynchronní metodu. Pokud prohlížeč podporuje [prvek `<mark>` HTML 5](http://www.w3.org/wiki/HTML/Elements/mark), uvidíte změny v `GizmosAsync` žlutým zvýrazněním.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample3.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample4.cs?highlight=1,3,5)]

 Následující změny byly aplikovány, aby bylo možné `GizmosAsync` být asynchronní.

- Metoda je označena pomocí klíčového slova [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) , které dává kompilátoru pokyn ke generování zpětných volání pro části těla a k automatickému vytvoření `Task<ActionResult>`, který je vrácen.
- k názvu metody se připojila &quot;Async&quot;. Připojení "Async" není vyžadováno, ale je to konvence při psaní asynchronních metod.
- Návratový typ se změnil z `ActionResult` na `Task<ActionResult>`. Návratový typ `Task<ActionResult>` představuje průběžnou práci a poskytuje volajícím metody s popisovačem, přes který má počkat na dokončení asynchronní operace. V tomto případě je volající webové služby. `Task<ActionResult>` představuje probíhající práci s výsledkem `ActionResult.`
- Klíčové slovo [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) bylo použito pro volání webové služby.
- Bylo voláno rozhraní API asynchronní webové služby (`GetGizmosAsync`).

V těle metody `GetGizmosAsync` jiné asynchronní metody je volána `GetGizmosAsync`. `GetGizmosAsync` okamžitě vrátí `Task<List<Gizmo>>`, která se nakonec dokončí, když budou data k dispozici. Vzhledem k tomu, že nechcete nic dalšího dělat, dokud nebudete mít Gizmo data, kód očekává úlohu (pomocí klíčového slova **await** ). Klíčové slovo **await** lze použít pouze v metodách popsaných pomocí klíčového slova **Async** .

Klíčové slovo **await** neblokuje vlákno, dokud není úloha dokončena. Zaregistruje zbytek metody jako zpětné volání na úkolu a okamžitě se vrátí. Když se nakonec očekávaný úkol dokončí, vyvolá toto zpětné volání, takže bude pokračovat v provádění metody přímo tam, kde byla vypnuta. Další informace o použití klíčových slov [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) a [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) a oboru názvů [úkolů](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) naleznete v tématu [asynchronní odkazy](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/async).

Následující kód ukazuje metody `GetGizmos` a `GetGizmosAsync`.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample5.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample6.cs?highlight=1,4-8)]

 Asynchronní změny jsou podobné těm, které jste udělali výše v **GizmosAsync** . 

- Podpis metody byl opatřen poznámkami pomocí klíčového slova [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) , návratový typ byl změněn na `Task<List<Gizmo>>`a k názvu metody byl přidán *Async* .
- Namísto třídy [WebClient](https://msdn.microsoft.com/library/system.net.webclient.aspx) se používá asynchronní třída [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx) .
- Klíčové slovo [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) bylo použito pro asynchronní metody [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx) .

Na následujícím obrázku vidíte zobrazení asynchronního Gizmo.

![async](using-asynchronous-methods-in-aspnet-mvc-4/_static/image2.png)

Prezentace prohlížečů gizma dat je shodná se zobrazením vytvořeným synchronním voláním. Jediným rozdílem je, že asynchronní verze může být větší výkon při velkém zatížení.

## <a id="Parallel"></a>Paralelní provádění více operací

Metody asynchronní akce mají významnou výhodu oproti synchronním metodám, pokud akce musí provádět několik nezávislých operací. V zadané ukázce se synchronní metoda `PWG`(pro Products, widgets a Gizma) zobrazí výsledky tří volání webové služby, které získá seznam produktů, widgetů a gizma. Projekt [webového rozhraní API ASP.NET](../../../web-api/index.md) , který poskytuje tyto služby, používá [Task. Delay](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) k simulaci latence nebo pomalých síťových volání. Pokud je zpoždění nastavené na 500 milisekund, asynchronní metoda `PWGasync` trvá několik málo než 500 milisekund, zatímco synchronní `PWG`á verze přebírá více než 1 500 milisekund. Metoda synchronního `PWG` je uvedena v následujícím kódu.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample7.cs)]

Metoda asynchronního `PWGasync` je uvedena v následujícím kódu.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample8.cs?highlight=1,3,12)]

Následující obrázek znázorňuje zobrazení vrácené z metody **PWGasync** .

![pwgAsync](using-asynchronous-methods-in-aspnet-mvc-4/_static/image3.png)

## <a id="CancelToken"></a>Použití tokenu zrušení

Asynchronní metody akcí vracející `Task<ActionResult>`jsou zrušitelné, to znamená, že přebírají parametr [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx) , pokud je jeden k dispozici s atributem [hodnota vlastnosti AsyncTimeout](https://msdn.microsoft.com/library/system.web.mvc.asynctimeoutattribute(VS.108).aspx) . Následující kód ukazuje metodu `GizmosCancelAsync` s časovým limitem 150 milisekund.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample9.cs?highlight=1-3,5,10)]

Následující kód ukazuje přetížení GetGizmosAsync, které přijímá parametr [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx) .

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-mvc-4/samples/sample10.cs)]

V ukázkové aplikaci, která je k dispozici, vyberte odkaz *demo tokenu zrušení* , který volá metodu `GizmosCancelAsync` a demonstruje zrušení asynchronního volání.

## <a id="ServerConfig"></a>Konfigurace serveru pro volání webové služby vysoké souběžnosti nebo vysoké latence

Aby bylo možné využít výhody asynchronní webové aplikace, může být nutné provést některé změny výchozí konfigurace serveru. Při konfiguraci a zátěži testování asynchronní webové aplikace mějte na paměti následující skutečnosti.

- Windows 7, Windows Vista a všechny klientské operační systémy Windows mají maximálně 10 souběžných požadavků. Budete potřebovat serverový operační systém Windows, abyste viděli výhody asynchronních metod při vysokém zatížení.
- Registrace .NET 4,5 se službou IIS z příkazového řádku se zvýšenými oprávněními:  
  %windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet\_regiis – i  
  Viz [registrační nástroj služby IIS pro ASP.NET (Aspnet\_regiis. exe)](https://msdn.microsoft.com/library/k6h9cz8h.aspx) .
- Možná budete muset zvýšit limit fronty [http. sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) z výchozí hodnoty 1 000 na 5 000. Pokud je nastavení příliš nízké, může se stát, že žádosti o odmítnutí [http. sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) se zobrazí ve stavu HTTP 503. Změna limitu fronty HTTP. sys:

    - Otevřete Správce služby IIS a přejděte do podokna fondy aplikací.
    - Klikněte pravým tlačítkem na cílový fond aplikací a vyberte **Upřesnit nastavení**.  
        ![pokročilé](using-asynchronous-methods-in-aspnet-mvc-4/_static/image4.png)
    - V dialogovém okně **Upřesnit nastavení** změňte *délku fronty* z 1 000 na 5 000.  
        Délka fronty ![](using-asynchronous-methods-in-aspnet-mvc-4/_static/image5.png)  
  
  Všimněte si, že na obrázcích výše je rozhraní .NET Framework uvedeno jako v 4.0, i když fond aplikací používá rozhraní .NET 4,5. Pro pochopení této nesrovnalosti si přečtěte následující informace:

    - [Verze rozhraní .NET a cílení na více verzí – .NET 4,5 je místní upgrade na rozhraní .NET 4,0](http://www.hanselman.com/blog/NETVersioningAndMultiTargetingNET45IsAnInplaceUpgradeToNET40.aspx)
    - [Jak nastavit aplikaci IIS nebo službu AppPool na použití ASP.NET 3,5 místo 2,0](http://www.hanselman.com/blog/HowToSetAnIISApplicationOrAppPoolToUseASPNET35RatherThan20.aspx)
    - [.NET Framework verze a závislosti](https://msdn.microsoft.com/library/bb822049(VS.110).aspx)
- Pokud vaše aplikace používá webové služby nebo System.NET ke komunikaci s back-endu přes protokol HTTP, může být nutné zvýšit [connectionManagement/maxconnection](https://msdn.microsoft.com/library/fb6y0fyc(VS.110).aspx) element. U aplikací ASP.NET to je omezené funkcí Automatická konfigurace na 12 časů počtu procesorů. To znamená, že u čtyřjádrových procesů můžete mít maximálně 12 \* 4 = 48 souběžných připojení k koncovému bodu IP adres. Vzhledem k tomu, že se jedná o přizpůsobitelné [automatické konfigurace](https://msdn.microsoft.com/library/7w2sway1(VS.110).aspx), nejjednodušší způsob, jak zvýšit `maxconnection` v aplikaci ASP.NET, je nastavit [System .NET. Třída ServicePointManager. DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit(VS.110).aspx) programově v metodě `Application_Start` v souboru *Global. asax* . Příklad najdete v ukázkovém souboru ke stažení.
- V rozhraní .NET 4,5 by měla být výchozí hodnota 5000 pro [maxConcurrentRequestsPerCPU](https://blogs.msdn.com/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx) .

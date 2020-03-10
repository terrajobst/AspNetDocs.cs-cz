---
uid: web-forms/overview/performance-and-caching/using-asynchronous-methods-in-aspnet-45
title: Použití asynchronních metod v ASP.NET 4,5 | Microsoft Docs
author: Rick-Anderson
description: V tomto kurzu se seznámíte se základy vytváření asynchronní aplikace webového formuláře ASP.NET pomocí Visual Studio Express 2012 pro web, což je zdarma...
ms.author: riande
ms.date: 01/02/2019
ms.assetid: a585c9a2-7c8e-478b-9706-90f3739c50d1
msc.legacyurl: /web-forms/overview/performance-and-caching/using-asynchronous-methods-in-aspnet-45
msc.type: authoredcontent
ms.openlocfilehash: 7abc3d7acc60d7d868958f2a313bc408f96c95a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78625193"
---
# <a name="using-asynchronous-methods-in-aspnet-45"></a>Použití asynchronních metod v ASP.NET 4.5

od [Rick Anderson](https://twitter.com/RickAndMSFT)

> V tomto kurzu se seznámíte se základy vytváření asynchronní aplikace webového formuláře ASP.NET pomocí [Visual Studio Express 2012 pro web](https://www.microsoft.com/visualstudio/11), což je bezplatná verze Microsoft Visual Studio. Můžete také použít [Visual Studio 2012](https://www.microsoft.com/visualstudio/11). V tomto kurzu jsou uvedené následující oddíly.
> 
> - [Způsob zpracování požadavků fondem vláken](#HowRequestsProcessedByTP)
> - [Výběr synchronních nebo asynchronních metod](#ChoosingSyncVasync)
> - [Ukázková aplikace](#SampleApp)
> - [Synchronní stránka Gizma](#GizmosSynch)
> - [Vytvoření asynchronní stránky Gizma](#CreatingAsynchGizmos)
> - [Paralelní provádění více operací](#Parallel)
> - [Použití tokenu zrušení](#CancelToken)
> - [Konfigurace serveru pro volání webové služby vysoké souběžnosti nebo vysoké latence](#ServerConfig)
> 
> K dispozici je kompletní ukázka v tomto kurzu.  
> [https://github.com/RickAndMSFT/Async-ASP.NET/](https://github.com/RickAndMSFT/Async-ASP.NET/) na webu [GitHub](https://github.com/) .

Webové stránky ASP.NET 4,5 v kombinaci s [rozhraním .net 4,5](https://msdn.microsoft.com/library/w0x726c2(VS.110).aspx) umožňují registrovat asynchronní metody, které vracejí objekt typu [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx). .NET Framework 4 představila asynchronní programovací koncept, který je označován jako [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) a ASP.NET 4,5, který podporuje [úlohu](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx). Úkoly jsou reprezentovány typem **úkolu** a souvisejícími typy v oboru názvů [System. Threading. Tasks](https://msdn.microsoft.com/library/system.threading.tasks.aspx) . .NET Framework 4,5 sestaví k této asynchronní podpoře s klíčovým slovem [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) a [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) , která umožňují pracovat s objekty [úlohy](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) mnohem méně složitější než předchozí asynchronní přístupy. Klíčové slovo [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) je syntaktická zkratka pro značící, že část kódu by měla asynchronně čekat na nějakou jinou část kódu. Klíčové slovo [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) představuje pomocný parametr, který můžete použít k označení metod jako asynchronních metod založených na úlohách. Kombinace **operátoru await**, **Async**a objektu **Task** usnadňuje psaní asynchronního kódu v rozhraní .NET 4,5. Nový model pro asynchronní metody se nazývá *asynchronní vzor založený na úlohách* (**klepněte**). V tomto kurzu se předpokládá, že máte zkušenosti s asynchronním programováním pomocí klíčových slov [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) a [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) a oboru názvů [úkolu](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) .

Další informace o klíčovém slově [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) a [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) a oboru názvů [úkolů](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) naleznete v následujících odkazech.

- [Dokument White Paper: asynchronii v .NET](https://go.microsoft.com/fwlink/?LinkId=204844)
- [Nejčastější dotazy k Async/await](https://blogs.msdn.com/b/pfxteam/archive/2012/04/12/10293335.aspx)
- [Asynchronní programování v aplikaci Visual Studio](https://msdn.microsoft.com/vstudio/gg316360)

## <a id="HowRequestsProcessedByTP"></a>Způsob zpracování požadavků fondem vláken

Na webovém serveru .NET Framework udržuje fond vláken, která se používají k obsluhování požadavků ASP.NET. Když požadavek dorazí, vlákno z fondu se odešle do zpracování tohoto požadavku. Pokud je požadavek zpracováván synchronně, vlákno, který zpracovává požadavek, je při zpracování žádosti zaneprázdněno a vlákno nemůže obsluhovat jiný požadavek.   
  
Nemusí se jednat o problém, protože fond vláken je možné dostatečně velký, aby se vešel do mnoha zaneprázdněných vláken. Počet vláken ve fondu vláken je ale omezený (výchozí maximum pro .NET 4,5 je 5 000). Ve velkých aplikacích s vysokou souběžnou délkou dlouhotrvajících požadavků můžou být všechna dostupná vlákna zaneprázdněná. Tato podmínka se označuje jako vyčerpání vlákna. Po dosažení tohoto stavu vyřadí webové servery požadavky. Pokud se fronta požadavků zaplní, webový server odmítne žádosti se stavem HTTP 503 (Server je příliš zaneprázdněný). Fond vláken CLR má omezení pro vkládání nových vláken. Pokud je souběžnost souběžnosti (to znamená, že váš web může náhle obdržet velký počet požadavků) a že všechna dostupná vlákna požadavků jsou zaneprázdněna z důvodu back-endu s vysokou latencí, může vaše aplikace velmi špatně reagovat. Každé nové vlákno přidané do fondu vláken má navíc režii (například 1 MB paměti zásobníku). Webová aplikace, která používá synchronní metody pro obsluhu vysoké latence, kdy se fond vláken zvětšuje na standard .NET 4,5, ve výchozím nastavení maximum je 5 000 vláken, což by využilo přibližně 5 GB paměti, než je aplikace schopná, aby služba používala stejné požadavky. asynchronní metody a jenom 50 vláken. Při asynchronní práci nepoužíváte vždy vlákno. Například při provádění asynchronní žádosti webové služby nebude ASP.NET používat žádná vlákna mezi voláním **asynchronní** metody a **await**. Použití fondu vláken ke zpracování žádostí s vysokou latencí může způsobit velké nároky na paměť a špatné využití hardwaru serveru.

## <a name="processing-asynchronous-requests"></a>Zpracování asynchronních požadavků

Ve webových aplikacích, které zobrazují velký počet souběžných požadavků při spuštění nebo mají zátěžové zatížení (kde se souběžně roste souběžně), probíhá asynchronní volání webové služby, čímž se zvýší rychlost odezvy vaší aplikace. Asynchronní požadavek trvá zpracování jako synchronní požadavek stejným časem. Například pokud požadavek provede volání webové služby, které vyžaduje dokončení dvou sekund, požadavek trvá dvě sekundy, ať už se provádí synchronně nebo asynchronně. Během asynchronního volání však vlákno neblokuje odpověď na jiné požadavky, zatímco čeká na dokončení první žádosti. Asynchronní požadavky proto zabraňují zařazování požadavků a nárůstu fondu vláken, pokud existuje celá řada souběžných požadavků, které spouštějí dlouhotrvající operace.

## <a id="ChoosingSyncVasync"></a>Výběr synchronních nebo asynchronních metod

V této části jsou uvedeny pokyny pro použití synchronních nebo asynchronních metod. Jsou to jenom pokyny. Prověřte každou aplikaci jednotlivě a určete, zda asynchronní metody pomůžou s výkonem.

Obecně platí, že použijte synchronní metody pro následující podmínky:

- Operace jsou jednoduché nebo krátkodobé.
- Jednoduchost je důležitější než efektivita.
- Operace jsou primárně operace CPU místo operací, které zahrnují velký výkon disku nebo síťové režie. Použití asynchronních metod na operacích vázaných na procesor poskytuje žádné výhody a má za následek větší režii.

Obecně použijte asynchronní metody pro následující podmínky:

- Voláte služby, které mohou být spotřebovány prostřednictvím asynchronních metod, a používáte rozhraní .NET 4,5 nebo vyšší.
- Operace jsou vázané na síť nebo vstupně-výstupní operace, nikoli vázané na procesor.
- Paralelismus je důležitější než jednoduchost kódu.
- Chcete poskytnout mechanismus, který umožňuje uživatelům zrušit dlouho běžící požadavek.
- Pokud výhoda přepínání vláken převáží náklady na přepínač kontextu. Obecně byste měli provést asynchronní metodu, pokud synchronní metoda blokuje vlákno žádosti ASP.NET při nečinnosti. Voláním asynchronního volání není vlákno požadavku ASP.NET zablokováno, protože při čekání na dokončení požadavku webové služby nebude fungovat.
- Testování ukazuje, že blokující operace jsou kritické pro výkon lokality a že služba IIS může obsluhovat více požadavků pomocí asynchronních metod pro tato blokující volání.

  Ukázka ke stažení ukazuje, jak efektivně používat asynchronní metody. Uvedená ukázka byla navržena tak, aby poskytovala jednoduchou ukázku asynchronního programování v ASP.NET 4,5. Vzorek není určen jako referenční architektura pro asynchronní programování v ASP.NET. Vzorový program volá metody [ASP.NET webového rozhraní API](../../../web-api/index.md) , které zavolají [Task. Delay](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) pro simulaci dlouhotrvajících volání webové služby. Většina produkčních aplikací nebude zobrazovat takové zjevné výhody použití asynchronních metod.   
  
Několik aplikací vyžaduje, aby všechny metody byly asynchronní. Často převod několika synchronních metod na asynchronní metody poskytuje nejlepší zvýšení efektivity požadované práce.

## <a id="SampleApp"></a>Ukázková aplikace

Ukázkovou aplikaci si můžete stáhnout z [https://github.com/RickAndMSFT/Async-ASP.NET](https://github.com/RickAndMSFT/Async-ASP.NET) na webu [GitHub](https://github.com/) . Úložiště se skládá ze tří projektů:

- *WebAppAsync*: projekt webových formulářů ASP.NET, který využívá službu webového rozhraní API **WebAPIpwg** . Většina kódu pro tento kurz je z tohoto projektu.
- *WebAPIpgw*: projekt webového rozhraní API ASP.NET MVC 4, který implementuje řadiče `Products, Gizmos and Widgets`. Poskytuje data pro projekt *WebAppAsync* a projekt *Mvc4Async* .
- *Mvc4Async*: projekt ASP.NET MVC 4, který obsahuje kód používaný v jiném kurzu. Provádí volání rozhraní Web API ke službě **WebAPIpwg** .

## <a id="GizmosSynch"></a>Synchronní stránka Gizma

 Následující kód ukazuje `Page_Load` synchronní metodu, která slouží k zobrazení seznamu gizma. (Pro tento článek je Gizmo fiktivní mechanické zařízení.) 

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample1.cs)]

Následující kód ukazuje metodu `GetGizmos` služby Gizmo.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample2.cs)]

Metoda `GizmoService GetGizmos` předává identifikátor URI službě HTTP webového rozhraní API ASP.NET, která vrací seznam dat gizma. Projekt *WebAPIpgw* obsahuje implementaci `gizmos, widget` webového rozhraní API a `product`ch řadičů.  
Následující obrázek ukazuje stránku gizma z ukázkového projektu.

![Gizma](using-asynchronous-methods-in-aspnet-45/_static/image1.png)

## <a id="CreatingAsynchGizmos"></a>Vytvoření asynchronní stránky Gizma

Ukázka používá nová klíčová slova [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) a [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) (k dispozici v rozhraních .NET 4,5 a Visual Studio 2012), aby kompilátor mohl být zodpovědný za údržbu složitých transformací potřebných pro asynchronní programování. Kompilátor umožňuje psát kód pomocí C#konstrukce asynchronního toku řízení a kompilátor automaticky aplikuje transformace potřebné k použití zpětných volání, aby nedocházelo k blokování vláken.

Asynchronní stránky ASP.NET musí zahrnovat direktivu [stránky](https://msdn.microsoft.com/library/ydy4x04a.aspx) s atributem `Async` nastaveným na hodnotu "true". Následující kód ukazuje direktivu [stránky](https://msdn.microsoft.com/library/ydy4x04a.aspx) s atributem `Async` nastaveným na hodnotu "true" pro stránku *GizmosAsync. aspx* .

[!code-aspx[Main](using-asynchronous-methods-in-aspnet-45/samples/sample3.aspx?highlight=1)]

Následující kód ukazuje `Gizmos` metodu synchronního `Page_Load` a `GizmosAsync` asynchronní stránku. Pokud prohlížeč podporuje [&gt; elementu &lt;značkami HTML 5](http://www.w3.org/wiki/HTML/Elements/mark), uvidíte změny v `GizmosAsync` žlutým zvýrazněním.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample4.cs)]

Asynchronní verze:

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample5.cs?highlight=3,6-7,9,11)]

 Pro povolení asynchronní stránky `GizmosAsync` byly aplikovány následující změny.

- Direktiva [stránky](https://msdn.microsoft.com/library/ydy4x04a.aspx) musí mít atribut `Async` nastaven na hodnotu "true".
- Metoda `RegisterAsyncTask` slouží k registraci asynchronní úlohy obsahující kód, který běží asynchronně.
- Nová metoda `GetGizmosSvcAsync` je označena pomocí klíčového slova [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) , které kompilátor instruuje, aby vygeneroval zpětná volání pro části těla a automaticky vytvořila vrácenou `Task`.
- k názvu asynchronní metody byla připojena &quot;Async&quot;. Připojení "Async" není vyžadováno, ale je to konvence při psaní asynchronních metod.
- Návratový typ nové metody `GetGizmosSvcAsync` je `Task`. Návratový typ `Task` představuje průběžnou práci a poskytuje volajícím metody s popisovačem, přes který má počkat na dokončení asynchronní operace.
- Klíčové slovo [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) bylo použito pro volání webové služby.
- Bylo voláno rozhraní API asynchronní webové služby (`GetGizmosAsync`).

V těle metody `GetGizmosSvcAsync` jiné asynchronní metody je volána `GetGizmosAsync`. `GetGizmosAsync` okamžitě vrátí `Task<List<Gizmo>>`, která se nakonec dokončí, když budou data k dispozici. Vzhledem k tomu, že nechcete nic dalšího dělat, dokud nebudete mít Gizmo data, kód očekává úlohu (pomocí klíčového slova **await** ). Klíčové slovo **await** lze použít pouze v metodách popsaných pomocí klíčového slova **Async** .

Klíčové slovo **await** neblokuje vlákno, dokud není úloha dokončena. Zaregistruje zbytek metody jako zpětné volání na úkolu a okamžitě se vrátí. Když se nakonec očekávaný úkol dokončí, vyvolá toto zpětné volání, takže bude pokračovat v provádění metody přímo tam, kde byla vypnuta. Další informace o použití klíčových slov [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) a [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) a oboru názvů [úkolů](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) naleznete v tématu [asynchronní odkazy](https://docs.microsoft.com/dotnet/csharp/language-reference/keywords/async).

Následující kód ukazuje metody `GetGizmos` a `GetGizmosAsync`.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample6.cs)]

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample7.cs?highlight=1,4-8)]

 Asynchronní změny jsou podobné těm, které jste udělali výše v **GizmosAsync** . 

- Podpis metody byl opatřen poznámkami pomocí klíčového slova [Async](https://msdn.microsoft.com/library/hh156513(VS.110).aspx) , návratový typ byl změněn na `Task<List<Gizmo>>`a k názvu metody byl přidán *Async* .
- Namísto synchronní třídy [WebClient](https://msdn.microsoft.com/library/system.net.webclient.aspx) se používá asynchronní třída [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx) .
- Klíčové slovo [await](https://msdn.microsoft.com/library/hh156528(VS.110).aspx) bylo použito pro asynchronní metodu [HttpClient](https://msdn.microsoft.com/library/system.net.http.httpclient(VS.110).aspx)[GetAsync](https://msdn.microsoft.com/library/hh158944(VS.110).aspx) .

Na následujícím obrázku vidíte zobrazení asynchronního Gizmo.

![async](using-asynchronous-methods-in-aspnet-45/_static/image2.png)

Prezentace prohlížečů gizma dat je shodná se zobrazením vytvořeným synchronním voláním. Jediným rozdílem je, že asynchronní verze může být větší výkon při velkém zatížení.

## <a name="registerasynctask-notes"></a>RegisterAsyncTask poznámky

Metody zapojování s `RegisterAsyncTask` budou spouštěny ihned po provedení [fáze PreRender](https://msdn.microsoft.com/library/ms178472.aspx). Můžete také použít asynchronní události void stránky přímo, jak je znázorněno v následujícím kódu:

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample8.cs)]

Nevýhodou na asynchronní události void je, že vývojáři již mají při spuštění událostí plnou kontrolu. Například pokud. aspx a. Hlavní definice `Page_Load` události a jedna nebo obě jsou asynchronní, pořadí spouštění nelze zaručit. Platí stejné indeterminiate pořadí pro obslužné rutiny událostí bez události (například `async void Button_Click`). Pro většinu vývojářů to by mělo být přijatelné, ale ty, kteří vyžadují plnou kontrolu nad pořadím spuštění, by měli používat jenom rozhraní API, jako je `RegisterAsyncTask`, které využívají metody, které vracejí objekt Task.

## <a id="Parallel"></a>Paralelní provádění více operací

Asynchronní metody mají významnou výhodu oproti synchronním metodám, pokud akce musí provádět několik nezávislých operací. V zadané ukázce zobrazuje synchronní stránka *pwg. aspx*(pro produkty, widgety a gizma) výsledky tří volání webové služby a získá seznam produktů, widgetů a gizma. Projekt [webového rozhraní API ASP.NET](../../../web-api/index.md) , který poskytuje tyto služby, používá [Task. Delay](https://msdn.microsoft.com/library/hh139096(VS.110).aspx) k simulaci latence nebo pomalých síťových volání. Když je zpoždění nastavené na 500 milisekund, *PWGasync* stránka asynchronního přenosu po dobu delší než 500 ms trvá, zatímco synchronní `PWG`á verze přebírá více než 1 500 milisekund. Synchronní stránka *pwg. aspx* je zobrazena v následujícím kódu.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample9.cs)]

Asynchronní kód `PWGasync` na pozadí je uveden níže.

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample10.cs?highlight=5,11,21)]

Na následujícím obrázku vidíte zobrazení vrácené ze stránky asynchronní *PWGasync. aspx* .

![](using-asynchronous-methods-in-aspnet-45/_static/image3.png)

## <a id="CancelToken"></a>Použití tokenu zrušení

Asynchronní metody vracející `Task`jsou zrušitelné, to znamená, že převezmou parametr [CancellationToken](https://msdn.microsoft.com/library/system.threading.cancellationtoken(VS.110).aspx) , pokud je k dispozici atribut `AsyncTimeout` direktivy [stránky](https://msdn.microsoft.com/library/ydy4x04a.aspx) . Následující kód ukazuje stránku *GizmosCancelAsync. aspx* s časovým limitem sekund.

[!code-aspx[Main](using-asynchronous-methods-in-aspnet-45/samples/sample11.aspx?highlight=1)]

Následující kód ukazuje soubor *GizmosCancelAsync.aspx.cs* .

[!code-csharp[Main](using-asynchronous-methods-in-aspnet-45/samples/sample12.cs?highlight=6,9)]

V poskytnuté ukázkové aplikaci výběr odkazu *GizmosCancelAsync* volá stránku *GizmosCancelAsync. aspx* a demonstruje zrušení (časování) asynchronního volání. Vzhledem k tomu, že doba zpoždění spadá do náhodného rozsahu, může být nutné stránku několikrát aktualizovat, aby se zobrazila chybová zpráva.

## <a id="ServerConfig"></a>Konfigurace serveru pro volání webové služby vysoké souběžnosti nebo vysoké latence

Aby bylo možné využít výhody asynchronní webové aplikace, může být nutné provést některé změny výchozí konfigurace serveru. Při konfiguraci a zátěži testování asynchronní webové aplikace mějte na paměti následující skutečnosti.

- Windows 7, Windows Vista, Window 8 a všechny klientské operační systémy Windows mají maximálně 10 souběžných požadavků. Budete potřebovat serverový operační systém Windows, abyste viděli výhody asynchronních metod při vysokém zatížení.
- Pomocí následujícího příkazu zaregistrujte .NET 4,5 se službou IIS z příkazového řádku se zvýšenými oprávněními:  
  %windir%\Microsoft.NET\Framework64 \v4.0.30319\aspnet\_regiis – i  
  Viz [registrační nástroj služby IIS pro ASP.NET (Aspnet\_regiis. exe)](https://msdn.microsoft.com/library/k6h9cz8h.aspx) .
- Možná budete muset zvýšit limit fronty [http. sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) z výchozí hodnoty 1 000 na 5 000. Pokud je nastavení příliš nízké, může se stát, že žádosti o odmítnutí [http. sys](https://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture) se zobrazí ve stavu HTTP 503. Změna limitu fronty HTTP. sys:

    - Otevřete Správce služby IIS a přejděte do podokna fondy aplikací.
    - Klikněte pravým tlačítkem na cílový fond aplikací a vyberte **Upřesnit nastavení**.  
        ![pokročilé](using-asynchronous-methods-in-aspnet-45/_static/image4.png)
    - V dialogovém okně **Upřesnit nastavení** změňte *délku fronty* z 1 000 na 5 000.  
        Délka fronty ![](using-asynchronous-methods-in-aspnet-45/_static/image5.png)  
  
  Všimněte si, že na obrázcích výše je rozhraní .NET Framework uvedeno jako v 4.0, i když fond aplikací používá rozhraní .NET 4,5. Pro pochopení této nesrovnalosti si přečtěte následující informace:

- [Verze rozhraní .NET a cílení na více verzí – .NET 4,5 je místní upgrade na rozhraní .NET 4,0](http://www.hanselman.com/blog/NETVersioningAndMultiTargetingNET45IsAnInplaceUpgradeToNET40.aspx)
- [Jak nastavit aplikaci IIS nebo službu AppPool na použití ASP.NET 3,5 místo 2,0](http://www.hanselman.com/blog/HowToSetAnIISApplicationOrAppPoolToUseASPNET35RatherThan20.aspx)
- [.NET Framework verze a závislosti](https://msdn.microsoft.com/library/bb822049(VS.110).aspx)

- Pokud vaše aplikace používá webové služby nebo System.NET ke komunikaci s back-endu přes protokol HTTP, může být nutné zvýšit [connectionManagement/maxconnection](https://msdn.microsoft.com/library/fb6y0fyc(VS.110).aspx) element. U aplikací ASP.NET to je omezené funkcí Automatická konfigurace na 12 časů počtu procesorů. To znamená, že u čtyřjádrových procesů můžete mít maximálně 12 \* 4 = 48 souběžných připojení k koncovému bodu IP adres. Vzhledem k tomu, že se jedná o přizpůsobitelné [automatické konfigurace](https://msdn.microsoft.com/library/7w2sway1(VS.110).aspx), nejjednodušší způsob, jak zvýšit `maxconnection` v aplikaci ASP.NET, je nastavit [System .NET. Třída ServicePointManager. DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit(VS.110).aspx) programově v metodě `Application_Start` v souboru *Global. asax* . Příklad najdete v ukázkovém souboru ke stažení.
- V rozhraní .NET 4,5 by měla být výchozí hodnota 5000 pro [maxConcurrentRequestsPerCPU](https://blogs.msdn.com/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx) .

## <a name="contributors"></a>Přispěvatelé

- [Broderick dávky](http://stackoverflow.com/users/59641/levi)
- [Dykstra](http://www.bing.com/search?q=site%3Aasp.net+%22Tom+Dykstra%22+-forums.asp.net&amp;qs=n&amp;form=QBRE&amp;pq=site%3Aasp.net+%22tom+dykstra%22+-forums.asp.net&amp;sc=8-42&amp;sp=-1&amp;sk=)
- [Brad Wilson](http://bradwilson.typepad.com/)
- [HongMei GE](https://blogs.msdn.com/b/hongmeig/)

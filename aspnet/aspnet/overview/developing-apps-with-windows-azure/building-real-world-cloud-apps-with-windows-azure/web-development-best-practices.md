---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
title: Osvědčené postupy vývoje pro web (vytváření skutečných cloudových aplikací s Azure) | Microsoft Docs
author: MikeWasson
description: Vytváření reálných cloudových aplikací pomocí Azure je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které mohou...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: 52d6c941-2cd9-442f-9872-2c798d6d90cd
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices
msc.type: authoredcontent
ms.openlocfilehash: 0956aaaf1f6a1a0d2f5d93f98cb6959cec98dbaf
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74582703"
---
# <a name="web-development-best-practices-building-real-world-cloud-apps-with-azure"></a>Osvědčené postupy vývoje pro web (vytváření skutečných cloudových aplikací s Azure)

[Jan Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Dykstra](https://github.com/tdykstra)

[Stažení opravy projektu IT](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stažení elektronické knihy](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **Vytváření reálných cloudových aplikací pomocí Azure** je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které vám pomůžou úspěšně vyvíjet webové aplikace pro Cloud. Informace o elektronické příručce najdete v [první kapitole](introduction.md).

První tři vzory byly o nastavení procesu agilního vývoje; zbytek se týká architektury a kódu. Toto je kolekce osvědčených postupů vývoje pro web:

- [Bezstavové webové servery](#stateless) za inteligentním nástrojem pro vyrovnávání zatížení.
- [Vyhněte se stavu relace](#sessionstate) (nebo pokud se k tomu nemůžete vyhnout, používejte distribuovanou mezipaměť místo databáze).
- [Používejte síť CDN](#cdn) pro statické souborové prostředky (obrázky, skripty) na hraničních počítačích.
- K zamezení blokování volání [použijte asynchronní podporu rozhraní .NET 4.5](#async) .

Tyto postupy jsou platné pro veškerý vývoj na webu, ne jenom pro cloudové aplikace, ale jsou obzvláště důležité pro cloudové aplikace. Pracují společně, aby vám pomohly zajistit optimální využití vysoce flexibilního škálování, které nabízí cloudové prostředí. Pokud tyto postupy nedodržujete, při pokusu o škálování aplikace se podíváte na omezení.

<a id="stateless"></a>
## <a name="stateless-web-tier-behind-a-smart-load-balancer"></a>Bezstavová webová vrstva za inteligentním nástrojem pro vyrovnávání zatížení

*Bezstavová webová úroveň* znamená, že neuložíte žádná data aplikací do paměti webového serveru nebo systému souborů. Zachování stavu vaší webové vrstvy vám umožní poskytovat lepší prostředí pro zákazníky a ušetřit peníze:

- Pokud je webová vrstva Bezstavová a je umístěná za nástrojem pro vyrovnávání zatížení, můžete rychle reagovat na změny v provozu aplikace tím, že dynamicky přidáte nebo odeberete servery. V cloudovém prostředí, kde platíte jenom za prostředky serveru, pokud je skutečně používáte, což je schopnost reagovat na změny v poptávce se může překládat na obrovských úspor.
- Bezstavová webová úroveň je v podstatě jednodušší pro horizontální navýšení kapacity aplikace. To vám také umožňuje rychle reagovat na škálování potřeb rychleji a strávit méně peněz při vývoji a testování v rámci procesu.
- Cloudové servery, jako jsou třeba místní servery, je potřeba opravit a občas spustit; a pokud je webová vrstva Bezstavová, směrování provozu při dočasném výpadku serveru nezpůsobí chyby nebo neočekávané chování.

Většina reálných aplikací potřebuje uložit stav pro relaci webu. hlavní bod není uložený na webovém serveru. Stav můžete uložit jinými způsoby, například u klienta v souborech cookie nebo mimo procesový Server ve stavu relace ASP.NET pomocí poskytovatele mezipaměti. Soubory můžete ukládat do [úložiště objektů BLOB v Microsoft Azure](unstructured-blob-storage.md) místo do místního systému souborů.

Příkladem toho, jak snadné je škálování aplikace na webech Windows Azure, pokud je vaše webová úroveň Bezstavová, najdete na kartě **škálování** webu Windows Azure na portálu pro správu:

![Karta škálování](web-development-best-practices/_static/image1.png)

Pokud chcete přidat webové servery, můžete jednoduše přetáhnout posuvník počet instancí vpravo. Nastavte ji na 5 a klikněte na **Uložit**a během pár sekund máte 5 webových serverů v systému Windows Azure, které zpracovávají provoz vašeho webu.

![Pět instancí](web-development-best-practices/_static/image2.png)

Můžete tak jednoduše nastavit počet instancí dolů na 3 nebo přejít na 1. Při horizontálním navýšení kapacity začnete okamžitě ukládat peníze, protože se Microsoft Azure účtuje po minutách, ne po hodinách.

Můžete také sdělit službě Windows Azure automatické zvýšení nebo snížení počtu webových serverů na základě využití procesoru. Když v následujícím příkladu využití CPU překročí 60%, počet webových serverů se zmenší na minimálně 2 a pokud využití procesoru překročí 80%, počet webových serverů se zvýší až na 4.

![Škálování podle využití procesoru](web-development-best-practices/_static/image3.png)

Nebo co když víte, že váš web bude v pracovní době zaneprázdněný? Můžete říct službě Windows Azure, aby spouštěla více serverů během denní doby a snížila se na jeden server, a to i na noci a víkendy. Následující série snímků obrazovky ukazuje, jak nastavit web tak, aby na jednom serveru spouštěl jeden server za hodinu a 4 servery během pracovní doby od 8 do 5 odp.

![Škálování podle plánu](web-development-best-practices/_static/image4.png)

![Nastavení časů plánu](web-development-best-practices/_static/image5.png)

![Plán Daytime](web-development-best-practices/_static/image6.png)

![Plán weeknight](web-development-best-practices/_static/image7.png)

![Plán víkendu](web-development-best-practices/_static/image8.png)

To všechno samozřejmě můžete udělat ve skriptech i na portálu.

Schopnost vaší aplikace při horizontálním navýšení kapacity je ve Windows Azure skoro neomezená, pokud se vyhnete překážkám dynamického přidávání a odebírání virtuálních počítačů, a to tak, že zůstanete bez stavu na webové úrovni.

<a id="sessionstate"></a>
## <a name="avoid-session-state"></a>Vyhněte se stavu relace

V reálné cloudové aplikaci není často praktické, aby se zabránilo ukládání určitého stavu pro relaci uživatele, ale některé přístupy mají dopad na výkon a škálovatelnost více než jiných. Pokud je třeba uložit stav, nejlepším řešením je zachovat malý objem a uložit ho do souborů cookie. Pokud to není proveditelné, příští nejlepší řešení je použití stavu relace ASP.NET se zprostředkovatelem pro [distribuovanou mezipaměť v paměti](distributed-caching.md#sessionstate). Nejhorším řešením z hlediska výkonu a škálovatelnosti je použití zprostředkovatele stavu relace zálohovaného databáze.

<a id="cdn"></a>
## <a name="use-a-cdn-to-cache-static-file-assets"></a>Používání sítě CDN k ukládání statických souborových prostředků do mezipaměti

CDN je zkratka pro Content Delivery Network. Do poskytovatele CDN poskytujete statické souborové prostředky, jako jsou obrázky a soubory skriptu, a poskytovatel tyto soubory ukládá do mezipaměti v datových centrech po celém světě, aby se do vaší aplikace dostaly relativně rychlá odezva a nízká latence pro ukládání do mezipaměti. hmot. Tím se zrychlí celková doba načítání lokality a snižuje se zatížení webových serverů. Sítě CDN jsou obzvláště důležité, pokud se snažíte oslovit cílovou skupinu, která je geograficky distribuována.

Microsoft Azure má síť CDN a můžete použít jiné sítě CDN v aplikaci, která běží na Windows Azure nebo v jakémkoli webovém hostitelském prostředí.

<a id="async"></a>
## <a name="use-net-45s-async-support-to-avoid-blocking-calls"></a>Zabránit zablokování volání pomocí asynchronní podpory .NET 4.5

Rozhraní .NET 4,5 rozšířilo programovací jazyky C# a jazyka VB, aby bylo mnohem jednodušší zpracovávat úlohy asynchronně. Výhoda asynchronního programování není pouze pro situace paralelního zpracování, například když chcete aktivovat více volání webové služby současně. Umožňuje také, aby váš webový server při vysokém zatížení prováděl efektivnější a spolehlivější výkon. Pro webový server je k dispozici pouze omezený počet vláken a v případě vysokého zatížení při použití všech vláken musí příchozí požadavky počkat, dokud nebudou uvolněna vlákna. Pokud váš kód aplikace nezpracovává úlohy, jako jsou dotazy databáze a volání webové služby asynchronně, mnoho vláken je zbytečně nevázaně, zatímco server čeká na reakci v/v. Tím se omezí množství provozu, které server může zpracovat za podmínek vysokého zatížení. Při asynchronním programování se vlákna, která čekají na webovou službu nebo databázi, vrátí do služby nové žádosti, dokud nebudou přijata data. V případě zaneprázdněného webového serveru je pak možné zpracovávat stovky nebo tisíce požadavků, které by jinak čekaly na uvolnění vláken.

Jak jste viděli dříve, je stejně snadné snížit počet webových serverů, které zpracovávají váš web, protože je můžete zvýšit. Takže pokud server může dosáhnout větší propustnosti, nepotřebujete tolik z nich a můžete snížit náklady, protože potřebujete méně serverů pro daný objem přenosů, než by bylo možné jinak.

Podpora asynchronního programovacího modelu .NET 4,5 je součástí ASP.NET 4,5 pro webové formuláře, MVC a webové rozhraní API; v Entity Framework 6 a v [rozhraní Windows Azure Storage API](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/07/12/introducing-storage-client-library-2-1-rc-for-net-and-windows-phone-8.aspx).

### <a name="async-support-in-aspnet-45"></a>Asynchronní podpora v ASP.NET 4,5

V ASP.NET 4,5 se podpora pro asynchronní programování přidala nejen do jazyka, ale také do rozhraní MVC, webových formulářů a webových rozhraní API. Například metoda akce kontroleru ASP.NET MVC přijme data z webového požadavku a předá data do zobrazení, které pak vytvoří HTML, který se odešle do prohlížeče. Metoda Action často potřebuje získat data z databáze nebo webové služby, aby ji bylo možné zobrazit na webové stránce nebo uložit data zadaná na webové stránce. V těchto scénářích je snadné provést asynchronní metodu akce: namísto vrácení objektu *ActionResult* vracíte *&lt;&gt;* a označíte metodu pomocí klíčového slova *Async* . V případě, že se řádek kódu v rámci metody sestaví jako operace, která zahrnuje dobu čekání, označíte ji pomocí klíčového slova await.

Tady je jednoduchá metoda akce, která volá metodu úložiště pro databázový dotaz:

[!code-csharp[Main](web-development-best-practices/samples/sample1.cs)]

A zde je stejná metoda, která zpracovává asynchronní volání databáze:

[!code-csharp[Main](web-development-best-practices/samples/sample2.cs?highlight=1,4)]

V části pokrývá kompilátor vygeneruje příslušný asynchronní kód. Když aplikace provede volání `FindTaskByIdAsync`, ASP.NET provede požadavek `FindTask` a potom odvíjí pracovní podproces a zpřístupní ho pro zpracování další žádosti. Po dokončení žádosti o `FindTask` je vlákno restartováno, aby pokračovalo ve zpracování kódu, který se nachází po volání. Během předběžného mezi tím, kdy je zahájena žádost o `FindTask` a vrácení dat, máte k dispozici vlákno, pomocí kterého lze provádět užitečnou práci, která by jinak mohla být vázána na odpověď.

Pro asynchronní kód je k dispozici režie, ale v podmínkách nízkého zatížení je tato režie zanedbatelná, zatímco v podmínkách vysokého zatížení můžete zpracovávat požadavky, které by jinak probíhaly čekání na dostupná vlákna.

Tento druh asynchronního programování je možné provést od ASP.NET 1,1, ale je obtížné zapisovat, náchylnost k chybám a být obtížné ho ladit. Teď, když jsme zjednodušili kódování pro IT v ASP.NET 4,5, neexistuje žádný důvod, proč to dělat.

### <a name="async-support-in-entity-framework-6"></a>Asynchronní podpora v Entity Framework 6

Jako součást asynchronní podpory v 4,5 jsme dodali asynchronní podporu pro volání webové služby, sokety a vstupně-výstupní operace se systémem souborů, ale nejběžnějším vzorem pro webové aplikace je vystavení databáze a naše knihovny dat nepodporovaly asynchronní zpracování. Nyní Entity Framework 6 přidává asynchronní podporu pro přístup k databázi.

V Entity Framework 6 všechny metody, které způsobují odeslání dotazu nebo příkazu do databáze, mají asynchronní verze. Zde uvedený příklad ukazuje asynchronní verzi metody *find* .

[!code-csharp[Main](web-development-best-practices/samples/sample3.cs?highlight=8)]

A tato asynchronní podpora funguje nejen pro příkazy INSERT, DELETE, Updates a Simple, ale funguje i s dotazy LINQ:

[!code-csharp[Main](web-development-best-practices/samples/sample4.cs?highlight=7,10)]

K dispozici je `Async` verze metody `ToList`, protože v tomto kódu je metoda, která způsobí odeslání dotazu do databáze. Metody `Where` a `OrderByDescending` pouze konfigurují dotaz, zatímco metoda `ToListAsync` spouští dotaz a ukládá odpověď do `result` proměnné.

## <a name="summary"></a>Přehled

Osvědčené postupy vývoje pro web, které jsou zde popsané, můžete implementovat v jakémkoli webovém programovacím rozhraní a jakémkoli cloudovém prostředí, ale máme nástroje v ASP.NET a Windows Azure, abychom to usnadnili. Pokud budete postupovat podle těchto vzorů, můžete snadno škálovat svou webovou vrstvu a minimalizovat své náklady, protože každý server bude moci zvládnout více provozu.

V [Další části](single-sign-on.md) najdete informace o tom, jak Cloud umožňuje použití scénářů jednotného přihlašování.

## <a name="resources"></a>Prostředky

Další informace najdete v následujících zdrojích informací.

Bezstavové webové servery:

- [Vzory a postupy Microsoft – pokyny](https://msdn.microsoft.com/library/dn589774.aspx)k automatickému škálování
- [Zakazuje se spřažení instancí ARR na webech Windows Azure](https://azure.microsoft.com/blog/2013/11/18/disabling-arrs-instance-affinity-in-windows-azure-web-sites/). Příspěvek na blogu od Ereze Benari vysvětluje spřažení relací na webech Windows Azure.

ZDROJ

- [Failsafe: vytváření škálovatelných, odolných Cloud Services](https://channel9.msdn.com/Series/FailSafe). Devět datových řad podle Ulrich Homann, matolin Mercuri a Simms. Podívejte se na diskuzi CDN ve epizody 3 od 1.1:34:00.
- [Vzor pro hostování statických obsahu Microsoft Patterns and Practices](https://msdn.microsoft.com/library/dn589776.aspx)
- [Recenze CDN](http://www.cdnreviews.com/). Přehled mnoha sítě CDN

Asynchronní programování:

- [Použití asynchronních metod v ASP.NET MVC 4](../../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md). Kurz Rick Anderson.
- [Asynchronní programování pomocí modifikátoru Async aC# operátoru Await (a Visual Basic)](https://msdn.microsoft.com/library/vstudio/hh191443.aspx). Dokument White Paper MSDN, který vysvětluje použití pro asynchronní programování, jak funguje v ASP.NET 4,5, a jak napsat kód pro implementaci.
- [Entity Framework asynchronní dotaz a uložení](https://msdn.microsoft.com/data/jj819165)
- [Jak vytvářet ASP.NET webové aplikace pomocí Async](https://channel9.msdn.com/Events/TechEd/NorthAmerica/2013/DEV-B337#fbid=tgkT4SR_DK7). Prezentace videa podle Rowan Miller. Obsahuje grafickou ukázku způsobu, jakým asynchronní programování může výrazně zvýšit propustnost webového serveru v podmínkách vysokého zatížení.
- [Failsafe: vytváření škálovatelných, odolných Cloud Services](https://channel9.msdn.com/Series/FailSafe). Devět datových řad podle Ulrich Homann, matolin Mercuri a Simms. Diskuze o dopadu asynchronního programování na škálovatelnost najdete v části epizody 4 a epizody 8.
- Hodnota [Magic pro použití asynchronních metod v ASP.NET 4,5 plus důležité gotcha](http://www.hanselman.com/blog/TheMagicOfUsingAsynchronousMethodsInASPNET45PlusAnImportantGotcha.aspx). Blogový příspěvek od Scott Hanselman, primárně o použití Async v aplikacích ASP.NET Web Forms.

Další doporučené postupy pro vývoj na webu najdete v následujících zdrojích informací:

- [Opravte ukázkové Doporučené postupy pro aplikace](the-fix-it-sample-application.md#bestpractices). Příloha této elektronické knihy obsahuje řadu doporučených postupů, které byly implementovány v aplikaci Fix it.
- [Kontrolní seznam pro webový vývojář](http://webdevchecklist.com/asp.net)

> [!div class="step-by-step"]
> [Předchozí](continuous-integration-and-continuous-delivery.md)
> [Další](single-sign-on.md)

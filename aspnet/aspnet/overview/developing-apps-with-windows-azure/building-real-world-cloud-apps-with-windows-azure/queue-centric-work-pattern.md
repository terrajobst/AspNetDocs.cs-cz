---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern
title: Pracovní vzor orientovaný na fronty (vytváření skutečných cloudových aplikací s Azure) | Microsoft Docs
author: MikeWasson
description: Vytváření reálných cloudových aplikací pomocí Azure je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které mohou...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: cc1ad51b-40c3-4c68-8620-9aaa0fd1f6cf
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/queue-centric-work-pattern
msc.type: authoredcontent
ms.openlocfilehash: c73b070f11366e781bcea70ffc84fd49a47d469a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2019
ms.locfileid: "74582751"
---
# <a name="queue-centric-work-pattern-building-real-world-cloud-apps-with-azure"></a>Pracovní vzor orientovaný na fronty (vytváření skutečných cloudových aplikací s Azure)

[Jan Wasson](https://github.com/MikeWasson), [Rick Anderson]((https://twitter.com/RickAndMSFT)), [Dykstra](https://github.com/tdykstra)

[Stažení opravy projektu IT](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stažení elektronické knihy](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **Vytváření reálných cloudových aplikací pomocí Azure** je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které vám pomůžou úspěšně vyvíjet webové aplikace pro Cloud. Informace o elektronické příručce najdete v [první kapitole](introduction.md).

Dříve jsme zjistili, že používání více služeb může mít za následek "složenou" smlouvu SLA, kde efektivní smlouva SLA aplikace je *produktem* jednotlivého SLA. Například aplikace pro opravu IT používá webové servery, úložiště a SQL Database. Pokud některá z těchto služeb selže, aplikace vrátí uživateli chybu.

Ukládání do mezipaměti je dobrý způsob, jak zpracovat přechodná selhání pro obsah, který je jen pro čtení. Ale co když vaše aplikace potřebuje pracovat? Například když uživatel odešle novou úlohu opravy IT, aplikace nemůže tuto úlohu pouze vložit do mezipaměti. Aplikace musí zapsat úlohu opravit IT do trvalého úložiště dat, aby ji bylo možné zpracovat.

To je místo, ve kterém se model práce orientované na fronty nachází v. Tento model umožňuje volné spojení mezi webovou vrstvou a back-end službou.

Tady je postup, jak tento model funguje. Když aplikace získá požadavek, přesune pracovní položku do fronty a okamžitě vrátí odpověď. Pak samostatný back-end proces vyžádá pracovní položky z fronty a provede práci.

Pracovní vzor orientovaný na fronty je užitečný pro:

- Práce, která je časově náročná (vysoká latence).
- Práce, která vyžaduje externí službu, která nemusí být vždy k dispozici.
- Práce, která je náročná na prostředky (vysoký procesor).
- Práce, která by mohla těžit z vyrovnání sazeb (podléhající náhlému nárůstu zatížení).

## <a name="reduced-latency"></a>Omezená latence

Fronty jsou užitečné kdykoli, když provádíte časově náročnou práci. Pokud úloha trvá několik sekund nebo i déle, místo blokování koncového uživatele umístěte pracovní položku do fronty. Sdělte uživateli, že na něm pracujeme, a pak pomocí naslouchacího procesu fronty úlohu zpracujte na pozadí.

Například při nákupu nějakého programu v online prodejně potvrdí web okamžitě vaši objednávku. Ale to neznamená, že vaše věci jsou už součástí doručování. Umístí úkol do fronty a na pozadí, kde provádí kontrolu kreditu, přípravu položek k expedici a tak dále.

U scénářů s krátkou latencí může celková koncová doba delší dobu trvat, než se úloha provede synchronně. Ale dokonce i ostatní výhody mohou tuto nevýhodu převážit.

## <a name="increased-reliability"></a>Zvýšená spolehlivost

Ve verzi opravy, kterou jsme prohledali zatím, je webový front-end úzce spojený s SQL Database back-endu. Pokud není služba SQL Database k dispozici, uživatel dostane chybu. Pokud se opakované pokusy nefungují (to znamená, že selhání je více než přechodný), může se zobrazit chyba a požádat uživatele, aby se pokusil o akci později.

![Diagram znázorňující selhání webového front-endu v případě selhání SQL Database back-endu](queue-centric-work-pattern/_static/image1.png)

Když uživatel odešle úlohu opravy IT pomocí front, zapíše do fronty zprávu. Datová část zprávy je reprezentace úlohy ve formátu [JSON](http://json.org/) . Jakmile se zpráva do fronty zapíše, aplikace se vrátí a okamžitě zobrazí uživateli zprávu o úspěchu.

Pokud se kterákoli ze služeb back-end, jako je například databáze SQL nebo naslouchací proces front--přejít do režimu offline, mohou uživatelé i nadále odesílat nové úlohy pro opravu IT. Zprávy se zařadí do fronty, dokud nebudou služby back-end k dispozici. V tomto okamžiku se back-end služby zachytí na nevyřízené položky.

![Diagram znázorňující, že webový front-end bude dál fungovat, když dojde k chybě SQL Database](queue-centric-work-pattern/_static/image2.png)

Navíc teď můžete přidat další back-end logiku, aniž byste se museli starat o odolnost front-endu. Můžete například chtít poslat vlastníkovi e-mail nebo zprávu SMS při každém přiřazení nové opravy. Pokud nebude e-mail nebo služba SMS k dispozici, můžete zpracovat všechno ostatní a potom do samostatné fronty vložit zprávu pro odesílání zpráv e-mailu nebo zprávy SMS.

Dřív byla naše platná smlouva SLA Web Apps &times; úložiště &times; SQL Database = 99,7%. (Viz [Návrh a zachována selhání](design-to-survive-failures.md).)

Když aplikaci změníme tak, aby používala frontu, webový front-end závisí jenom na Web Apps a úložišti, a to u složené smlouvy SLA 99,8%. (Všimněte si, že fronty jsou součástí služby Azure Storage, takže jsou zahrnuté ve stejné smlouvě SLA jako úložiště objektů BLOB.)

Pokud potřebujete ještě lepší než 99,8%, můžete vytvořit dvě fronty ve dvou různých oblastech. Určete jako primární a druhý jako sekundární. Pokud není primární fronta k dispozici, v aplikaci převezme služby při selhání sekundární frontou. Pravděpodobnost, že obě nejsou k dispozici ve stejnou chvíli, je velmi malá.

## <a name="rate-leveling-and-independent-scaling"></a>Vyrovnávání kapacity a nezávislé škálování

Fronty jsou užitečné také pro něco nazývaného *vyrovnání sazeb* nebo *Vyrovnávání zatížení*.

Webové aplikace jsou často náchylné k náhlým nárůstům provozu. I když můžete pomocí automatického škálování automaticky přidávat webové servery ke zpracování zvýšeného webového provozu, automatické škálování nemusí být schopné rychle reagovat, aby se mohlo zvládnout prudké špičky. Pokud webové servery můžou přesměrovat část práce, kterou musí provést, zapsáním zprávy do fronty, můžou zpracovávat víc provozu. Back-end služba pak může číst zprávy z fronty a zpracovávat je. Velikost fronty se bude zvětšovat nebo zmenšovat, protože se liší příchozí zatížení.

Díky spoustě časově náročné práce na back-end službu může webová vrstva snadněji reagovat na náhlé špičky v provozu. A ušetříte peníze, protože určité množství přenosů může být zpracováno méně webovými servery.

Webovou vrstvu a back-end službu můžete škálovat nezávisle. Například můžete potřebovat tři webové servery, ale pouze jeden server zpracovávající zprávy ve frontě. Nebo pokud spouštíte úlohu náročné na výpočetní výkon na pozadí, možná budete potřebovat další servery back-end.

![](queue-centric-work-pattern/_static/image3.png)

Automatické škálování funguje s back-end službami a s webovou vrstvou. Počet virtuálních počítačů, které zpracovávají úlohy ve frontě, můžete škálovat nahoru nebo dolů na základě využití CPU back-end virtuálních počítačů. Nebo můžete automatické škálování podle toho, kolik položek je ve frontě. Můžete například určit automatické škálování, které se pokusí ve frontě zachovat více než 10 položek. Pokud má fronta více než 10 položek, bude automatické škálování přidávat virtuální počítače. Při zachycení se automatické škálování odeberou další virtuální počítače.

## <a name="adding-queues-to-the-fix-it-application"></a>Přidání front do aplikace pro opravu IT

Abychom mohli model fronty implementovat, musíme udělat dvě změny v aplikaci opravit IT.

- Když uživatel odešle novou úlohu opravit úkol, umístí ji do fronty místo jejího zápisu do databáze.
- Vytvořte back-end službu, která zpracovává zprávy ve frontě.

Pro tuto frontu používáme [službu Azure Queue Storage](https://www.windowsazure.com/develop/net/how-to-guides/queue-service/). Další možností je použít [Azure Service Bus](https://docs.microsoft.com/azure/service-bus/).

Pokud chcete rozhodnout, kterou službu Queue Service použít, zvažte, jak vaše aplikace potřebuje odesílat a přijímat zprávy ve frontě:

- Pokud máte spolupracující výrobce a konkurenční zákazníky, zvažte použití služby Azure Queue Storage. Spolupracující výrobci znamená, že více procesů přidává zprávy do fronty. Konkurenční spotřebitelé znamená, že více procesů zpracovává zprávy z fronty za účelem jejich zpracování, ale kterákoli z nich může zpracovat pouze jeden uživatel. Pokud potřebujete větší propustnost, než můžete získat s jedinou frontou, použijte další fronty a/nebo další účty úložiště.
- Pokud potřebujete [model publikování/odběrů](http://en.wikipedia.org/wiki/Publish/subscribe), zvažte použití Azure Service Bus fronty.

Oprava IT aplikace vyhovuje spolupracujím výrobcům a konkurenčním modelům zákazníků.

Dalším aspektem je dostupnost aplikace. Služba Queue Storage je součástí stejné služby, kterou používáme pro úložiště objektů blob, takže její použití nemá žádný vliv na naši smlouvu SLA. Azure Service Bus je samostatná služba s vlastní smlouvou SLA. Pokud jsme používali Service Busch front, museli bychom zvážit dodatečné procento smlouvy SLA a naše složená smlouva SLA by byla nižší. Když zvolíte službu front, ujistěte se, že rozumíte dopadu vaší volby na dostupnost aplikace. Další informace najdete v části [Resources](#resources) .

## <a name="creating-queue-messages"></a>Vytváření zpráv fronty

Chcete-li vložit úlohu opravy IT do fronty, webový front-end provede následující kroky:

1. Vytvořte instanci [CloudQueueClient](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueueclient.aspx) . Instance `CloudQueueClient` se používá ke spouštění požadavků na službu front.
2. Vytvořte frontu, pokud ještě neexistuje.
3. Serializovat úlohu opravy IT.
4. Chcete-li vložit zprávu do fronty, zavolejte [CloudQueue. AddMessageAsync](https://msdn.microsoft.com/library/microsoft.windowsazure.storage.queue.cloudqueue.addmessageasync.aspx) .

Tuto práci provedeme v konstruktoru a metodě `SendMessageAsync` nové třídy `FixItQueueManager`.

[!code-csharp[Main](queue-centric-work-pattern/samples/sample1.cs?highlight=11-12,16,18-25)]

Tady používáme knihovnu [JSON.NET](https://github.com/JamesNK/Newtonsoft.Json) k serializaci fixit ve formátu JSON. Můžete použít libovolný přístup k serializaci, který dáváte přednost. JSON je výhodou pro lidské čtení, zatímco je méně podrobný než XML.

Kód v produkčním prostředí by měl přidat logiku zpracování chyb, pozastavit, jestli se databáze nestala k dispozici, zpracovávat obnovení efektivněji, vytvořit frontu při spuštění aplikace a spravovat "[poškozené" zprávy](https://msdn.microsoft.com/library/ms789028(v=vs.110).aspx). (Nezpracovatelná zpráva je zpráva, kterou nelze z nějakého důvodu zpracovat. Nechcete, aby se v této frontě zařadily nefunkční zprávy, kde se role pracovního procesu neustále pokusí o jejich zpracování, selhání, opakování, selhání atd.)

V front-endové aplikaci MVC potřebujeme aktualizovat kód, který vytvoří nový úkol. Místo vložení úkolu do úložiště zavolejte výše uvedenou metodu `SendMessageAsync`.

[!code-csharp[Main](queue-centric-work-pattern/samples/sample2.cs?highlight=10)]

## <a name="processing-queue-messages"></a>Zpracování zpráv fronty

Pokud chcete zpracovat zprávy ve frontě, vytvoříme back-end službu. Back-end služba spustí nekonečnou smyčku, která provede následující kroky:

1. Získá další zprávu z fronty.
2. Deserializovat zprávu na úlohu opravy IT.
3. Zapište úlohu opravit IT do databáze.

Pro hostování back-end služby vytvoříme cloudovou službu Azure, která obsahuje *roli pracovního procesu*. Role pracovního procesu se skládá z jednoho nebo více virtuálních počítačů, které mohou provádět zpracování back-endu. Kód, který běží na těchto virtuálních počítačích, načte zprávy z fronty, jakmile budou k dispozici. U každé zprávy budeme deserializovat datovou část JSON a zapsat instanci entity úlohy opravit IT do databáze pomocí stejného úložiště, které jsme použili dříve ve webové vrstvě.

Následující postup ukazuje, jak přidat projekt role pracovního procesu do řešení, které má standardní webový projekt. Tyto kroky už byly provedeny v projektu opravit IT, který si můžete stáhnout.

Nejdřív přidejte projekt cloudové služby do řešení sady Visual Studio. Klikněte pravým tlačítkem na řešení a vyberte **Přidat**, **Nový projekt**. V levém podokně rozbalte **vizuál C#**  a vyberte **Cloud**.

[![](queue-centric-work-pattern/_static/image5.png)](queue-centric-work-pattern/_static/image4.png)

V dialogovém okně **Nová cloudová služba Azure** rozbalte uzel **vizuál C#**  v levém podokně. Vyberte **role pracovního procesu** a klikněte na ikonu se šipkou vpravo.

![](queue-centric-work-pattern/_static/image6.png)

(Všimněte si, že můžete také přidat *webovou roli*. Místo jejího spuštění na webu Azure můžeme opravit front-end ve stejné cloudové službě. To má několik výhod, jak snadno koordinovat spojení mezi front-end a back-end. Pokud ale chcete tuto ukázku uchovávat snadno, udržujeme front-end ve Azure App Service webové aplikaci a v cloudové službě běželi jenom back-end.)

Role pracovního procesu se přiřadí výchozímu názvu. Chcete-li změnit název, najeďte myší na roli pracovního procesu v pravém podokně a pak klikněte na ikonu tužky.

![](queue-centric-work-pattern/_static/image7.png)

Kliknutím na tlačítko **OK** dokončete dialog. Tím se do řešení sady Visual Studio přidá dva projekty.

- projekt Azure, který definuje cloudovou službu, včetně informací o konfiguraci.
- Projekt role pracovního procesu, který definuje roli pracovního procesu.

![](queue-centric-work-pattern/_static/image8.png)

Další informace najdete v tématu [Vytvoření projektu Azure pomocí sady Visual Studio.](https://msdn.microsoft.com/library/windowsazure/ee405487.aspx)

V roli pracovního procesu se dotazuje na zprávy voláním metody `ProcessMessageAsync` třídy `FixItQueueManager`, kterou jsme dříve viděli.

[!code-csharp[Main](queue-centric-work-pattern/samples/sample3.cs?highlight=25)]

Metoda `ProcessMessagesAsync` kontroluje, zda se čeká na zprávu. Pokud existuje, deserializace zprávu do `FixItTask` entity a uloží entitu v databázi. Tato smyčka se zacykluje, dokud není fronta prázdná.

[!code-csharp[Main](queue-centric-work-pattern/samples/sample4.cs)]

Cyklické dotazování na zprávy ve frontě vznikají za malý poplatek za transakce, takže když nebude žádná zpráva čekat na zpracování, `RunAsync` metoda role pracovního procesu před dalším dotazem počká, než se znovu dotazuje, a to voláním `Task.Delay(1000)`.

Ve webovém projektu může přidání asynchronního kódu automaticky zvýšit výkon, protože služba IIS spravuje omezený fond vláken. Nejedná se o případ v projektu role pracovního procesu. Pro zlepšení škálovatelnosti role pracovního procesu můžete napsat vícevláknový kód nebo použít asynchronní kód k implementaci [paralelního programování](https://msdn.microsoft.com/library/ff963553.aspx). Ukázka neimplementuje paralelní programování, ale ukazuje, jak vytvořit asynchronní kód, abyste mohli implementovat paralelní programování.

## <a name="summary"></a>Přehled

V této kapitole jste viděli, jak zlepšit odezvu aplikací, spolehlivost a škálovatelnost implementací modelu práce orientovaného na fronty.

Toto je poslední z 13 vzorů popsaných v této elektronické knize, ale samozřejmě existuje mnoho dalších vzorů a postupů, které vám pomůžou při sestavování úspěšných cloudových aplikací. [Poslední kapitola](more-patterns-and-guidance.md) obsahuje odkazy na zdroje informací o tématech, která se nezabývá těmito 13 vzorci.

<a id="resources"></a>
## <a name="resources"></a>Prostředky

Další informace o frontách najdete v následujících zdrojích informací.

Nápovědě

- [Microsoft Azure Storage fronty část 1: Začínáme](https://www.red-gate.com/simple-talk/cloud/platform-as-a-service/microsoft-azure-storage-queues-part-1-getting-started/). Článek podle latinkové Schacherl
- [Provádění úloh na pozadí](https://msdn.microsoft.com/library/ff803365.aspx), kapitola 5 z [přesunu aplikací do cloudu, třetí edice](https://msdn.microsoft.com/library/ff728592.aspx) od Microsoft Patterns and Practices. (Konkrétně část ["použití Azure Storage fronty"](https://msdn.microsoft.com/library/ff803365.aspx#sec7).)
- [Osvědčené postupy pro maximalizaci škálovatelnosti a nákladové efektivity řešení zasílání zpráv na základě fronty v Azure](https://msdn.microsoft.com/library/windowsazure/hh697709.aspx). Dokument white paper o Valery Mizonov.
- [Porovnání front Azure a front Service Bus](https://msdn.microsoft.com/magazine/jj159884.aspx). Článek na webu MSDN Magazine, kde najdete další informace, které vám pomůžou zvolit službu fronty, která se má použít. Článek uvádí, že Service Bus je závislý na službě ACS pro ověřování, což znamená, že vaše fronty SB nebudou k dispozici, pokud služba ACS není dostupná. Vzhledem k tomu, že byl článek vytvořen, SB byl změněn, aby bylo možné používat [tokeny SAS](https://msdn.microsoft.com/library/windowsazure/dn170477.aspx) jako alternativu ke službě ACS.
- [Vzory a postupy Microsoftu – doprovodné materiály pro Azure](https://msdn.microsoft.com/library/dn568099.aspx) Přečtěte si téma Úvod do asynchronního zasílání zpráv, model kanálů a filtrů, vzorec kompenzační transakce, model konkurenčních spotřebitelů, CQRS vzor.
- [CQRS cesta](https://msdn.microsoft.com/library/jj554200). Elektronická kniha o CQRS podle vzorů a postupů Microsoftu.

Obrazový

- [Failsafe: vytváření škálovatelných, odolných Cloud Services](https://channel9.msdn.com/Series/FailSafe). Devět datových řad podle Ulrich Homann, matolin Mercuri a Simms. Prezentuje základní koncepty a principy architektury v rámci velmi přístupného a zajímavého způsobu, který vychází ze zkušeností zákazníků Microsoftu pro poradenské zákazníky (CAT) se skutečnými zákazníky. Úvod ke službě Azure Storage a frontách najdete v části epizody 5 od 35:13.

> [!div class="step-by-step"]
> [Předchozí](distributed-caching.md)
> [Další](more-patterns-and-guidance.md)

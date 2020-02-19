---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
title: Sestavování skutečných cloudových aplikací s využitím Azure | Microsoft Docs
author: MikeWasson
description: Tato elektronická kniha vás provede vytvořením skutečných cloudových řešení na základě vzorů. Vzory se vztahují na proces vývoje i na...
ms.author: riande
ms.date: 06/12/2014
ms.assetid: accfa16a-ab15-4c26-9ad4-babdc2a77d2e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction
msc.type: authoredcontent
ms.openlocfilehash: b88573b3702b755b155e8da35f5f8a67931bafc6
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457112"
---
# <a name="building-real-world-cloud-apps-with-azure"></a>Sestavování skutečných cloudových aplikací s využitím Azure

[Jan Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Dykstra](https://github.com/tdykstra)

[Stažení opravy projektu IT](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stažení elektronické knihy](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> Tato elektronická kniha vás provede vytvořením skutečných cloudových řešení na základě vzorů. Vzory platí pro proces vývoje a také pro postupy architektury a kódování.
> 
> Obsah je založen na prezentaci vyvinuté Scottem Guthrie a jejím držitelem na konferenci norského vývojáře (NORWEGIAN Developers Conference) v červnu 2013 ([část 1](http://vimeo.com/68215538), [část 2](http://vimeo.com/68215602)) a v Microsoft Tech Ed Austrálie v září 2013 ([část 1](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR324), část [2](https://channel9.msdn.com/Events/TechEd/Australia/2013/AZR325)). [Mnoho dalších](more-patterns-and-guidance.md#acknowledgments) aktualizovaných a rozšířených obsahu při přechodu z videa do napsaného formuláře.

## <a name="intended-audience"></a>Zamýšlená cílová skupina

Vývojáři, kteří se zajímá o vývoji pro Cloud, berou v úvahách o přesunu do cloudu nebo jsou novinkou pro vývoj v cloudu, naleznou stručný přehled nejdůležitějších konceptů a postupů, které potřebují znát. Koncepty jsou znázorněny v konkrétních příkladech a každá z nich odkazuje na další zdroje, kde najdete podrobné informace. Příklady a odkazy na další zdroje jsou pro Microsoft Framework and Services, ale principy, které jsme ukázali, se vztahují i na jiné vývojové architektury pro web a cloudová prostředí.

Vývojáři, kteří už mají vývoj pro Cloud, můžou najít nápady, které vám pomůžou s tím, jak budou úspěšné. Každá kapitola v řadě se dá číst nezávisle, takže si můžete vybrat a vybrat témata, která vás zajímají.

Každý, kdo sledoval Scott Guthrie, *sestavuje reálné cloudové aplikace s* využitím Azure Presentation a potřebuje další podrobnosti a aktualizované informace najdete tady.

<a id="patterns"></a>
## <a name="cloud-development-patterns"></a>Vzory vývoje pro Cloud

Tato elektronická příručka vysvětluje třináctně Doporučené vzory pro vývoj pro Cloud. "Vzor" se tady používá v širokém smyslu, což znamená doporučený způsob provádění akcí: jak nejlépe se naučit vývoj, navrhování a kódování cloudových aplikací. Jedná se o klíčové vzory, které vám pomůžou přejít do části úspěchy, pokud je použijete.

- [Automatizujte vše](automate-everything.md).

    - Pomocí skriptů můžete maximalizovat efektivitu a minimalizovat chyby v opakujících se procesech.
    - Ukázka: skripty pro správu Azure.
- [Správa zdrojového kódu](source-control.md). 

    - Nastavte strukturu větvení ve správě zdrojového kódu, abyste usnadnili DevOps pracovní postup.
    - Ukázka: Přidání skriptů do správy zdrojového kódu.
    - Ukázka: uchování citlivých dat ze správy zdrojového kódu.
    - Ukázka: použijte Git v aplikaci Visual Studio.
- [Průběžná integrace a doručování](continuous-integration-and-continuous-delivery.md). 

    - Automatizujte sestavování a nasazování při každém vrácení se změnami správy zdrojového kódu.
- [Osvědčené postupy vývoje pro web](web-development-best-practices.md). 

    - Zůstane bez stavu webové vrstvy.
    - Ukázka: škálování a automatické škálování v Web Apps v Azure App Service.
    - Vyhněte se stavu relace.
    - Pokud CDN není k dispozici, využijte síť CDN s náhradní sadou.
    - Použijte asynchronní programovací model.
    - Ukázka: Async v ASP.NET MVC a Entity Framework.
- [Jednotné přihlašování](single-sign-on.md). 

    - Seznámení s Azure Active Directory.
    - Ukázka: Vytvoření aplikace ASP.NET, která používá Azure Active Directory.
- [Možnosti úložiště dat](data-storage-options.md). 

    - Typy úložišť dat.
    - Jak zvolit správné úložiště dat.
    - Ukázka: Azure SQL Database.
- [Strategie dělení dat](data-partitioning-strategies.md). 

    - Umožňuje rozdělit data svisle, vodorovně nebo obojí, aby se usnadnilo škálování relační databáze.
- [Nestrukturované úložiště objektů BLOB](unstructured-blob-storage.md). 

    - Ukládání souborů v cloudu pomocí služby BLOB Service.
    - Ukázka: používání služby Blob Storage v aplikaci opravit IT.
- [Návrh pro zakonání selhání](design-to-survive-failures.md). 

    - Typy selhání.
    - Rozsah selhání.
    - Principy SLA
- [Monitorování a telemetrie](monitoring-and-telemetry.md). 

    - Proč byste měli koupit aplikaci telemetrie a napsat vlastní kód pro instrumentaci vaší aplikace.
    - Ukázka: nové Relic pro Azure
    - Ukázka: protokolování kódu v aplikaci Fix it.
    - Ukázka: vkládání závislostí v aplikaci Fix it.
    - Ukázka: Integrovaná podpora protokolování v Azure.
- [Zpracování přechodných chyb](transient-fault-handling.md). 

    - Pomocí inteligentního opakování/zpětného vypínání můžete zmírnit dopad přechodných selhání.
    - Ukázka: u Entity Framework 6 zkuste operaci zopakovat nebo znovu zapnout.
- [Distribuované ukládání do mezipaměti](distributed-caching.md). 

    - Využití distribuované mezipaměti vám pomůže zlepšit škálovatelnost a snížit náklady na transakce databáze.
- [Pracovní vzor orientovaný na fronty](queue-centric-work-pattern.md). 

    - Umožněte vysokou dostupnost a zvyšte škálovatelnost díky volnému spojování webových a pracovních vrstev.
    - Ukázka: fronty Azure Storage v aplikaci opravit IT.
- [Další modely a doprovodné materiály ke cloudovým aplikacím](more-patterns-and-guidance.md).
- [Příloha: ukázková aplikace Fix It](the-fix-it-sample-application.md)

    - Známé problémy
    - Doporučené postupy
    - Jak stahovat, sestavovat, spouštět a nasazovat.

Tyto vzory se vztahují na všechna cloudová prostředí, ale budeme je považovat za použití příkladů založených na technologiích a službách společnosti Microsoft, jako je například Visual Studio, Team Foundation Service, ASP.NET a Azure.

Tato část této kapitoly zavádí ukázkovou aplikaci pro opravu IT a Web Apps v Azure App Service cloudovém prostředí, ve kterém se spouští oprava IT aplikace.

<a id="fixit"></a>
## <a name="the-fix-it-sample-application"></a>Ukázková aplikace pro opravu IT

Většina snímků obrazovky a příkladů kódu zobrazených v této elektronické knize je založená na opravě aplikace IT, kterou původně vyvinul [Scott Guthrie](https://weblogs.asp.net/scottgu/) , k předvedení doporučených vzorů a postupů vývoje cloudových aplikací.

![Opravit domovskou stránku aplikace](introduction/_static/image1.png)

Ukázková aplikace je jednoduchý systém lístků pracovních položek. Pokud potřebujete něco pevně, vytvoříte lístek a přiřadíte ho někomu a ostatním se může přihlásit a zobrazit lístky, které jsou jim přiřazeny, a označit lístky jako dokončené.

Jedná se o standardní webový projekt sady Visual Studio. Je postavená na ASP.NET MVC a používá databázi SQL Server. Může běžet místně v IIS Express a dá se nasadit na web Azure, který se bude spouštět v cloudu. Můžete se přihlásit pomocí ověřování pomocí formulářů a místní databáze nebo pomocí poskytovatele sociálních sítí, jako je Google. (Později také ukážeme, jak se přihlásit pomocí účtu organizace služby Active Directory.)

![Přihlašovací stránka](introduction/_static/image2.png)

Jakmile se přihlásíte, můžete vytvořit lístek, přiřadit ho někomu a nahrát na něj obrázek toho, co chcete vyřešit.

![Vytvořit úlohu opravy IT](introduction/_static/image3.png)

![Opravit úlohu, kterou vytvořil](introduction/_static/image4.png)

Průběh pracovních položek, které jste vytvořili, můžete sledovat v části lístky, které jsou vám přiřazeny, zobrazit podrobnosti lístku a označovat položky jako dokončené.

To je velmi jednoduchá aplikace z perspektivy funkcí, ale uvidíte, jak ji sestavit, aby se mohla škálovat na miliony uživatelů a byla odolná vůči tomu, jako je selhání databáze a ukončení připojení. Také se dozvíte, jak vytvořit automatizovaný a agilní vývojový pracovní postup, který vám umožní začít pracovat snadno a lépe a zdokonalovat tím, že cyklus vývoje efektivně a rychle využijeme.

<a id="waws"></a>
## <a name="web-apps-in-azure-app-service"></a>Web Apps v Azure App Service

Cloudové prostředí používané pro opravu IT aplikace je služba Azure, kterou zavoláme na webové servery. Tato služba představuje způsob, jakým můžete hostovat svou vlastní webovou aplikaci v Azure bez nutnosti vytvářet virtuální počítače a udržovat je aktualizované, instalovat a konfigurovat IIS atd. Váš web hostuje na našich virtuálních počítačích a automaticky zajišťuje zálohování a obnovení a další služby za vás. Služba Web Sites spolupracuje s ASP.NET, Node. js, PHP a Pythonem. Umožňuje velmi rychle nasadit pomocí sady Visual Studio, Nasazení webu, FTP, Git nebo TFS. Obvykle je to několik sekund mezi časem spuštění nasazení a čas, kdy je vaše aktualizace k dispozici prostřednictvím Internetu. Je to vše zdarma, abyste mohli začít a narůstá objem provozu.

Na pozadí Web Apps v Azure App Service poskytuje spoustu součástí architektury a funkcí, které byste měli vytvořit sami, pokud jste chtěli hostovat web pomocí služby IIS na svých vlastních virtuálních počítačích. Jedna součást je koncový bod nasazení, který automaticky nakonfiguruje službu IIS a nainstaluje aplikaci do tolika virtuálních počítačů, ve kterých chcete provozovat Web.

![Služba nasazení](introduction/_static/image5.png)

Když uživatel narazí na web, neuskuteční přímo virtuální počítače služby IIS, procházejí je prostřednictvím nástrojů pro vyrovnávání zatížení [(ARR) žádostí o aplikace](https://www.iis.net/downloads/microsoft/application-request-routing) . Můžete je použít s vlastními servery, ale výhodou je, že jsou nastavené automaticky. Využívají inteligentní heuristickou službu, která bere v úvahu faktory, jako je spřažení relací, hloubka fronty ve službě IIS a využití CPU na každém počítači, aby se mohly směrovat přenosy na virtuální počítače, které hostují váš web.

![Nástroj pro vyrovnávání zatížení ARR](introduction/_static/image6.png)

Pokud dojde k výpadku počítače, Azure ho automaticky načte z rotace, roztáhne novou instanci virtuálního počítače a zahájí směrování provozu do nové instance – to vše bez výpadku vaší aplikace.

![Automatické obnovení při selhání počítače](introduction/_static/image7.png)

To vše se provádí automaticky. Vše, co potřebujete udělat, je vytvoření webu a nasazení aplikace do něj, pomocí Windows PowerShellu, sady Visual Studio nebo portálu pro správu Azure.

Rychlý a jednoduchý podrobný kurz, který ukazuje, jak vytvořit webovou aplikaci v aplikaci Visual Studio a jak ji nasadit na web Azure, najdete v tématu [Začínáme s Azure a ASP.NET](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).

<a id="summary"></a>
## <a name="summary"></a>Souhrn

Tento Úvod obsahuje seznam témat, na které se kniha zabývá, snímky obrazovky ukázkové aplikace a stručný přehled Web Apps v cloudovém prostředí Azure App Service. Jednou z výhod vývoje aplikací v a pro Cloud je, že je snadné automatizovat opakované vývojářské úlohy, jako je vytvoření testovacího prostředí a nasazení kódu do něj. Jak to udělat, je předmět [Další kapitoly](automate-everything.md).

## <a name="resources"></a>Prostředky

Další informace o tématech popsaných v této kapitole najdete v následujících zdrojích.

Nápovědě

- [Web Apps v Azure App Service](https://azure.microsoft.com/services/app-service/web/). Stránka portálu pro dokumentaci k Azure o Web Apps.
- [Web Apps, Cloud Services a virtuální počítače: Kdy použít?](https://azure.microsoft.com/documentation/articles/choose-web-site-cloud-service-vm/) WAWS, jak je znázorněno v této kapitole, je jedním ze tří způsobů, jak můžete spouštět webové aplikace v Azure. Tento článek vysvětluje rozdíly mezi třemi způsoby a poskytuje pokyny k výběru toho, který z nich je pro váš scénář nejvhodnější. Podobně jako u webů je Cloud Services funkce PaaS v Azure. Virtuální počítače jsou funkcí IaaS. Vysvětlení PaaS versus IaaS naleznete v kapitole [Možnosti dat](data-storage-options.md#paasiaas) .

Videa:

- [Scott Guthrie začíná krokem 0 – co je Azure Cloud OS?](https://azure.microsoft.com/documentation/videos/what-is-the-cloud-os-scottgu/)
- [Architektura webů – s Stefan Schackow](https://azure.microsoft.com/documentation/videos/why-azure-web-sites-plus-architecture/).
- [Weby Azure jsou interní s Jmenuji Nir a Mashkowski](https://channel9.msdn.com/Shows/Web+Camps+TV/Windows-Azure-Web-Sites-Internals-with-Nir-Mashkowski).

> [!div class="step-by-step"]
> [Next](automate-everything.md)

---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
title: Nestrukturované Blob Storage (vytváření skutečných cloudových aplikací s Azure) | Microsoft Docs
author: MikeWasson
description: Vytváření reálných cloudových aplikací pomocí Azure je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které mohou...
ms.author: riande
ms.date: 03/30/2015
ms.assetid: 9f05ccb1-2004-4661-ad8b-c370e6c09c8e
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/unstructured-blob-storage
msc.type: authoredcontent
ms.openlocfilehash: f48b2be755b84dff9b2672bd348c73107602c6dd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78617311"
---
# <a name="unstructured-blob-storage-building-real-world-cloud-apps-with-azure"></a>Nestrukturované Blob Storage (vytváření skutečných cloudových aplikací s Azure)

[Jan Wasson](https://github.com/MikeWasson), [Rick Anderson](https://twitter.com/RickAndMSFT), [Dykstra](https://github.com/tdykstra)

[Stažení opravy projektu IT](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4) nebo [stažení elektronické knihy](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **Vytváření reálných cloudových aplikací pomocí Azure** je založené na prezentaci vyvinuté Scottem Guthrie. Vysvětluje 13 vzorů a postupů, které vám pomůžou úspěšně vyvíjet webové aplikace pro Cloud. Informace o elektronické příručce najdete v [první kapitole](introduction.md).

V předchozí kapitole jsme se podívali na oddíly schémat a vysvětlete, jak aplikace opravit IT ukládá obrázky do služby Azure Storage Blob a další data úloh v Azure SQL Database. V této kapitole se podrobněji seznámíme s Blob service a ukážeme, jak se implementuje v kódu projektu opravit IT.

## <a name="what-is-blob-storage"></a>Co je BLOB Storage?

Služba Azure Storage Blob poskytuje způsob, jak ukládat soubory v cloudu. Blob service má řadu výhod pro ukládání souborů do místního síťového systému souborů:

- Je vysoce škálovatelná. Jeden účet úložiště může ukládat [stovky terabajtů](https://msdn.microsoft.com/library/windowsazure/dn249410.aspx)a můžete mít víc účtů úložiště. Některé z největších zákazníků Azure ukládají stovky petabajty. Microsoft SkyDrive využívá úložiště objektů BLOB.
- Je trvalý. Každý soubor, který ukládáte do Blob service, se automaticky zálohuje.
- Poskytuje vysokou dostupnost. [Smlouva SLA pro úložiště](https://go.microsoft.com/fwlink/p/?linkid=159705&amp;clcid=0x409) příslibů 99,9% nebo 99,99% doba provozu v závislosti na tom, jakou možnost geografického redundance zvolíte.
- Azure je funkce typu platforma jako služba (PaaS), což znamená, že jenom ukládáte a načítáte soubory a platíte jenom za skutečně využité úložiště a Azure automaticky postará o nastavení a správu všech virtuálních počítačů a diskových jednotek vyžadovaných pro službám.
- K Blob service můžete přistupovat pomocí REST API nebo pomocí rozhraní API programovacího jazyka. Sady SDK jsou dostupné pro .NET, Java, Ruby a další.
- Když soubor uložíte v Blob service, můžete ho snadno zpřístupnit prostřednictvím Internetu.
- Soubory můžete zabezpečit v Blob service tak, aby k nim měli přístup jenom autorizovaní uživatelé, nebo můžete poskytnout dočasné přístupové tokeny, které je zpřístupní někomu jenom po omezenou dobu.

Kdykoli vytváříte aplikaci pro Azure a chcete ukládat spoustu dat, která by v místním prostředí vypadala v souborech, jako jsou obrázky, videa, soubory PDF, tabulky atd. – zvažte Blob service.

## <a name="creating-a-storage-account"></a>Vytváří se účet úložiště.

Pokud chcete začít s Blob service vytvoříte účet úložiště v Azure. Na portálu klikněte na **nový** -- **Data Services** -- **úložiště** -- **rychlé vytvoření**a pak zadejte adresu URL a umístění datového centra. Umístění datového centra by mělo být stejné jako u vaší webové aplikace.

![Vytvořit ACCT úložiště](unstructured-blob-storage/_static/image1.png)

Vyberete primární oblast, do které chcete obsah uložit, a pokud zvolíte možnost [geografické replikace](https://blogs.msdn.com/b/windowsazurestorage/archive/2013/12/11/introducing-read-access-geo-replicated-storage-ra-grs-for-windows-azure-storage.aspx#_Geo_Redundant_Storage) , Azure vytvoří repliky všech vašich dat v jiném datovém centru v jiné oblasti země. Pokud například zvolíte datové centrum Western US, uložíte soubor, který se nachází v datovém centru Western US, ale v Azure na pozadí se také zkopíruje do jednoho z dalších datových center USA. Pokud dojde k havárii v jedné oblasti země, vaše data budou pořád bezpečná.

Azure neprovede replikaci dat mezi geograficky politickými hranicemi: Pokud je vaše primární umístění v USA, replikují se soubory jenom do jiné oblasti v USA. Pokud je vaše primární umístění Austrálie, soubory se replikují jenom do jiného datového centra v Austrálii.

Účet úložiště samozřejmě můžete vytvořit také spuštěním příkazů ze skriptu, jak jsme viděli dříve. Účet úložiště vytvoříte pomocí příkazu Windows PowerShellu:

[!code-powershell[Main](unstructured-blob-storage/samples/sample1.ps1)]

Jakmile budete mít účet úložiště, můžete ihned začít ukládat soubory do Blob service.

## <a name="using-blob-storage-in-the-fix-it-app"></a>Použití úložiště objektů BLOB v aplikaci opravit IT

Aplikace opravit IT umožňuje nahrávat fotky.

![Vytvořit úlohu opravy IT](unstructured-blob-storage/_static/image2.png)

Když kliknete na **vytvořit fixit**, aplikace nahraje zadaný soubor obrázku a uloží ho do BLOB Service.

### <a name="set-up-the-blob-container"></a>Nastavení kontejneru objektů BLOB

Aby bylo možné uložit soubor do Blob service budete potřebovat *kontejner* , ve kterém ho uložíte. Kontejner Blob service odpovídá složce systému souborů. Skripty pro vytvoření prostředí, které jsme prozkoumali v [kapitole automatizace všeho](automate-everything.md) , vytvoří účet úložiště, ale nevytvoří kontejner. Proto je účel metody `CreateAndConfigure` třídy `PhotoService` vytvořit kontejner, pokud ještě neexistuje. Tato metoda je volána z metody `Application_Start` v *Global. asax*.

[!code-csharp[Main](unstructured-blob-storage/samples/sample2.cs)]

Název účtu úložiště a přístupový klíč jsou uložené v kolekci `appSettings` souboru *Web. config* a kód v metodě `StorageUtils.StorageAccount` tyto hodnoty používá k sestavení připojovacího řetězce a navázání připojení:

[!code-csharp[Main](unstructured-blob-storage/samples/sample3.cs)]

Metoda `CreateAndConfigureAsync` poté vytvoří objekt, který představuje Blob service a objekt, který představuje kontejner (složka) s názvem "image" v Blob service:

[!code-csharp[Main](unstructured-blob-storage/samples/sample4.cs)]

Pokud kontejner s názvem "images" ještě neexistuje – což bude pravda při prvním spuštění aplikace proti novému účtu úložiště – kód vytvoří kontejner a nastaví oprávnění k jeho veřejnému zpřístupnění. (Ve výchozím nastavení jsou nové kontejnery objektů BLOB privátní a jsou přístupné jenom uživatelům, kteří mají oprávnění pro přístup k vašemu účtu úložiště.)

[!code-csharp[Main](unstructured-blob-storage/samples/sample5.cs)]

### <a name="store-the-uploaded-photo-in-blob-storage"></a>Uložení nahrané fotky do úložiště objektů BLOB

Pro nahrání a uložení souboru obrázku aplikace používá rozhraní `IPhotoService` a implementaci rozhraní ve třídě `PhotoService`. Soubor *PhotoService.cs* obsahuje veškerý kód v aplikaci pro opravu IT, který komunikuje s BLOB Service.

Následující metoda kontroleru MVC se volá, když uživatel klikne na **vytvořit fixit**. V tomto kódu `photoService` odkazuje na instanci `PhotoService` třídy a `fixittask` odkazuje na instanci třídy `FixItTask` entity, která ukládá data pro nový úkol.

[!code-csharp[Main](unstructured-blob-storage/samples/sample6.cs?highlight=8)]

Metoda `UploadPhotoAsync` ve třídě `PhotoService` ukládá nahraný soubor do Blob service a vrátí adresu URL, která odkazuje na nový objekt BLOB.

[!code-csharp[Main](unstructured-blob-storage/samples/sample7.cs)]

Stejně jako v metodě `CreateAndConfigure` se kód připojí k účtu úložiště a vytvoří objekt, který představuje kontejner objektů blob "image", s výjimkou případů, kdy tento kontejner předpokládá, že kontejner již existuje.

Pak vytvoří jedinečný identifikátor obrázku, který se má nahrát, zřetězením nové hodnoty GUID s příponou souboru:

[!code-csharp[Main](unstructured-blob-storage/samples/sample8.cs)]

Kód pak pomocí objektu kontejneru objektů BLOB a nového jedinečného identifikátoru vytvoří objekt blob, nastaví u tohoto objektu atribut, který označuje, jaký typ souboru je, a pak pomocí objektu BLOB uloží soubor do úložiště objektů BLOB.

[!code-csharp[Main](unstructured-blob-storage/samples/sample9.cs)]

Nakonec získá adresu URL, která odkazuje na objekt BLOB. Tato adresa URL bude uložena v databázi a lze ji použít na webových stránkách opravit k zobrazení nahrané bitové kopie.

[!code-csharp[Main](unstructured-blob-storage/samples/sample10.cs)]

Tato adresa URL je uložená v databázi jako jeden ze sloupců tabulky FixItTask.

[!code-csharp[Main](unstructured-blob-storage/samples/sample11.cs?highlight=10)]

V případě, že je v databázi jenom adresa URL a obrázky v úložišti objektů blob, oprava IT aplikace udržuje databázi malou, škálovatelnou a nenákladnou, zatímco image jsou uložené tam, kde je úložiště levné a dokáže zpracovávat terabajty nebo petabajty. Jeden účet úložiště může ukládat stovky terabajtů opravných fotek a platíte jenom za to, co využijete. Takže můžete začít s malým placením za 9 centů za první gigabajt a přidat další obrázky pro Pennies za další gigabajt.

### <a name="display-the-uploaded-file"></a>Zobrazit nahraný soubor

Aplikace opravit IT zobrazuje nahraný soubor obrázku při zobrazení podrobností pro úlohu.

![Oprava podrobností úkolu IT pomocí fotky](unstructured-blob-storage/_static/image3.png)

Chcete-li zobrazit obrázek, je nutné, aby zobrazení všech zobrazení MVC zahrnovalo hodnotu `PhotoUrl` do HTML odesílané do prohlížeče. Webový server a databáze nepoužívají cykly k zobrazení obrázku, zachovává pouze několik bajtů s adresou URL obrázku. V následujícím kódu Razor `Model` odkazuje na instanci třídy `FixItTask` entity.

[!code-cshtml[Main](unstructured-blob-storage/samples/sample12.cshtml?highlight=11)]

Pokud se podíváte na HTML stránku, která se zobrazí, zobrazí se adresa URL ukazující přímo na obrázek v úložišti objektů blob, což je něco podobného:

[!code-cshtml[Main](unstructured-blob-storage/samples/sample13.cshtml?highlight=11)]

## <a name="summary"></a>Souhrn

Viděli jste, jak aplikace Fix it ukládá obrázky do Blob service a jenom image URL v databázi SQL. Použití Blob service udržuje databázi SQL mnohem menší, než v opačném případě, umožňuje horizontální navýšení kapacity až na téměř neomezený počet úkolů a dá se provést bez napsání velkého množství kódu.

V účtu úložiště můžete mít stovky terabajtů a náklady na úložiště jsou mnohem levnější než SQL Database úložiště, od 1 do 3 centů za gigabajt za měsíc a za malý poplatek za transakci. A pamatujte na to, že neplatíte za maximální kapacitu, ale jenom za skutečně uloženou částku, takže vaše aplikace je připravená na škálování, ale neplatíte za veškerou dodatečnou kapacitu.

V [Další části](design-to-survive-failures.md) se seznámíte s důležitostí, jak zajistit, aby cloudová aplikace mohla řádně zpracovat selhání.

## <a name="resources"></a>Zdroje

Další informace najdete v následujících zdrojích informací:

- [Úvod do úložiště objektů BLOB v Azure](https://www.simple-talk.com/cloud/cloud-data/an-introduction-to-windows-azure-blob-storage-/) Blog o Jan dřevo.
- [Jak používat službu Azure Blob Storage v rozhraní .NET](https://docs.microsoft.com/azure/storage/blobs/storage-dotnet-how-to-use-blobs). Oficiální dokumentace na webu MicrosoftAzure.com. Stručný úvod do služby Blob Storage následovaný příklady kódu, které ukazují, jak se připojit k úložišti objektů blob, vytvářet kontejnery, nahrávat a stahovat objekty blob atd.
- [Failsafe: vytváření škálovatelných, odolných Cloud Services](https://channel9.msdn.com/Series/FailSafe). Devět datových řad podle Ulrich Homann, matolin Mercuri a Simms. Prezentuje základní koncepty a principy architektury v rámci velmi přístupného a zajímavého způsobu, který vychází ze zkušeností zákazníků Microsoftu pro poradenské zákazníky (CAT) se skutečnými zákazníky. Diskuzi o službě Azure Storage a objektech blob najdete v části epizody 5 od 35:13.
- [Vzory a postupy Microsoftu – doprovodné materiály pro Azure](https://msdn.microsoft.com/library/dn568099.aspx) Viz osobního Key Pattern.

> [!div class="step-by-step"]
> [Předchozí](data-partitioning-strategies.md)
> [Další](design-to-survive-failures.md)

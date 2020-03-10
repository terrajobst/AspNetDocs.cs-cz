---
uid: mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
title: 'Iterace #4 – zajistěte, aby byla aplikaceC#volně spojená () | Microsoft Docs'
author: microsoft
description: V této čtvrté iteraci využijeme několik vzorů návrhu softwaru, které usnadňují údržbu a úpravy aplikace Správce kontaktů. Pro...
ms.author: riande
ms.date: 02/20/2009
ms.assetid: 829f589f-e201-4f6e-9ae6-08ae84322065
msc.legacyurl: /mvc/overview/older-versions-1/contact-manager/iteration-4-make-the-application-loosely-coupled-cs
msc.type: authoredcontent
ms.openlocfilehash: ce8e3c4ff8a59be9f2f572813db599604216119d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544455"
---
# <a name="iteration-4--make-the-application-loosely-coupled-c"></a>Iterace #4 – zajistěte, aby byla aplikaceC#volně spojená ()

od [Microsoftu](https://github.com/microsoft)

[Stáhnout kód](iteration-4-make-the-application-loosely-coupled-cs/_static/contactmanager_4_cs1.zip)

> V této čtvrté iteraci využijeme několik vzorů návrhu softwaru, které usnadňují údržbu a úpravy aplikace Správce kontaktů. Například refaktorujte naši aplikaci, aby používala vzor úložiště a vzor vkládání závislostí.

## <a name="building-a-contact-management-aspnet-mvc-application-c"></a>Sestavování aplikace pro správu kontaktů ASP.NETC#MVC ()

V této sérii kurzů sestavíme celou aplikaci pro správu kontaktů od začátku do konce. Aplikace Správce kontaktů umožňuje ukládat kontaktní údaje – jména, telefonní čísla a e-mailové adresy – seznam lidí.

Aplikaci sestavíme přes několik iterací. U každé iterace doporučujeme aplikaci postupně vylepšit. Cílem tohoto vícenásobného přístupu k iteraci je umožnit pochopení příčiny každé změny.

- Iterace #1 – Vytvoření aplikace V první iteraci vytvoříme nejjednodušším způsobem správce kontaktů. Přidáváme podporu základních databázových operací: vytváření, čtení, aktualizace a odstraňování (CRUD).

- Iterace #2 – nastaví vzhled aplikace jako příjemné. V této iteraci Vylepšete vzhled aplikace úpravou výchozí stránky předlohy zobrazení ASP.NET MVC a šablony kaskádových stylů.

- Iterace #3 – Přidání ověření formuláře. Třetí iterace přidá základní ověřování formuláře. Uživatelům bráníme v odesílání formuláře bez nutnosti vyplnit požadovaná pole formuláře. Ověřujeme taky e-mailové adresy a telefonní čísla.

- Iterace #4 – zajistěte, aby byla aplikace volně spojená. V této čtvrté iteraci využijeme několik vzorů návrhu softwaru, které usnadňují údržbu a úpravy aplikace Správce kontaktů. Například refaktorujte naši aplikaci, aby používala vzor úložiště a vzor vkládání závislostí.

- Iterace #5 – vytvoření testů jednotek. V páté iteraci aplikace usnadňuje údržbu a úpravy přidáním jednotkových testů. Pro naše řadiče a logiku ověřování jsme nastavili třídy datového modelu a testy jednotek.

- Iterace #6 – použití vývoje řízeného testem. V této šesté iteraci přidáme do naší aplikace nové funkce, a to tak, že nejprve zapíšeme testy jednotek a napíšeme kód na testy jednotek. V této iteraci přidáváme skupiny kontaktů.

- Iterace #7 – přidání funkce AJAX V sedmé iteraci vylepšit rychlost reakce a výkon naší aplikace přidáním podpory pro AJAX.

## <a name="this-iteration"></a>Tato iterace

V této čtvrté iteraci aplikace Správce kontaktů se aplikace refaktoruje tak, aby aplikace byla uvolněna rychleji. Pokud je aplikace volně spojena, můžete kód upravit v jedné části aplikace, aniž byste museli upravovat kód v jiných částech aplikace. Volně spárované aplikace jsou odolnější ke změně.

V současné době jsou všechna pravidla přístupu k datům a ověřování používaná aplikací Správce kontaktů obsažena v třídách kontroleru. Jedná se o špatný nápad. Kdykoli budete potřebovat upravit jednu část aplikace, riskujete, že zavedete chyby do jiné části aplikace. Pokud například upravíte logiku ověřování, riskujete, že zavedete nové chyby do logiky přístupu k datům nebo kontroleru.

> [!NOTE] 
> 
> (SRP), třída by nikdy neměla mít více než jeden důvod ke změně. Kombinace kontroleru, ověřování a databázové logiky je obrovským porušením principu jedné zodpovědnosti.

Existuje několik důvodů, proč může být nutné aplikaci upravit. Je možné, že budete muset do aplikace přidat novou funkci, možná budete muset opravit chybu v aplikaci nebo může být nutné změnit způsob, jakým je funkce aplikace implementována. Aplikace jsou zřídka statické. V průběhu času se mají v průběhu času rozrůstat a postupovat.

Představte si například, že se rozhodnete změnit způsob implementace vrstvy přístupu k datům. Aplikace Správce kontaktů teď pro přístup k databázi používá Microsoft Entity Framework. Můžete se ale rozhodnout migrovat na novou nebo alternativní technologii pro přístup k datům, jako je ADO.NET Data Services nebo NHibernate. Vzhledem k tomu, že kód pro přístup k datům není izolovaný od ověřovacího a řídicího kódu, neexistuje způsob, jak změnit kód pro přístup k datům v aplikaci, aniž byste museli upravovat jiný kód, který přímo nesouvisí s přístupem k datům.

Pokud je aplikace volně spojená, můžete provést změny v jedné části aplikace bez zásahu do jiných částí aplikace. Můžete například přepnout technologie pro přístup k datům bez úprav ověřování nebo logiky kontroleru.

V této iteraci využijeme několik vzorů návrhu softwaru, které nám umožňují Refaktorovat naši aplikaci Správce kontaktů ve více volně vázaných aplikacích. Až to bude hotové, správce kontaktů vyhrál t něco, co předtím neudělal. V budoucnu ale budeme moct aplikaci snadno změnit.

> [!NOTE] 
> 
> Refaktoring je proces přepsání aplikace takovým způsobem, že neztratí žádné existující funkce.

## <a name="using-the-repository-software-design-pattern"></a>Použití vzoru návrhu softwaru pro úložiště

Naší první změnou je využívejte vzor návrhu softwaru, který se nazývá vzor úložiště. K izolaci kódu přístupu k datům ze zbytku naší aplikace použijeme vzor úložiště.

Implementace vzoru úložiště vyžaduje, abychom dokončili následující dva kroky:

1. Vytvoření rozhraní
2. Vytvoří konkrétní třídu, která implementuje rozhraní.

Nejdřív musíme vytvořit rozhraní, které popisuje všechny metody přístupu k datům, které potřebujeme udělat. Rozhraní IContactManagerRepository je obsaženo v seznamu 1. Toto rozhraní popisuje pět metod: CreateContact (), DeleteContact (), EditContact (), GetContact a ListContacts ().

**Výpis 1 – Models\IContactManagerRepository.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample1.cs)]

Dále je potřeba vytvořit konkrétní třídu, která implementuje rozhraní IContactManagerRepository. Vzhledem k tomu, že používáme Microsoft Entity Framework pro přístup k databázi, vytvoříme novou třídu s názvem EntityContactManagerRepository. Tato třída je obsažena v seznamu 2.

**Výpis 2 – Models\EntityContactManagerRepository.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample2.cs)]

Všimněte si, že třída EntityContactManagerRepository implementuje rozhraní IContactManagerRepository. Třída implementuje všechny pět metod popsaných v tomto rozhraní.

Možná vás zajímá, proč musíme bother s rozhraním. Proč musíme vytvořit rozhraní i třídu, která ho implementuje?

V případě jedné výjimky bude zbytek naší aplikace pracovat s rozhraním a nikoli konkrétní třídou. Namísto volání metod vystavených třídou EntityContactManagerRepository budeme volat metody vystavené rozhraním IContactManagerRepository.

Tímto způsobem můžeme implementovat rozhraní s novou třídou, aniž byste museli upravovat zbytek naší aplikace. Například v nějakém budoucím datu můžeme implementovat třídu DataServicesContactManagerRepository, která implementuje rozhraní IContactManagerRepository. Třída DataServicesContactManagerRepository může použít Data Services ADO.NET pro přístup k databázi místo Microsoft Entity Framework.

Pokud je náš kód aplikace naprogramován na rozhraní IContactManagerRepository namísto konkrétní třídy EntityContactManagerRepository, můžeme přepínat konkrétní třídy, aniž byste museli měnit žádný zbytek našeho kódu. Například můžeme přepnout z třídy EntityContactManagerRepository na třídu DataServicesContactManagerRepository, aniž byste museli měnit přístup k datům nebo logiku ověřování.

Programování proti rozhraním (abstrakce) místo konkrétních tříd usnadňuje změnu v naší aplikaci.

> [!NOTE] 
> 
> Rozhraní můžete z konkrétní třídy v sadě Visual Studio rychle vytvořit tak, že vyberete refaktoru možnosti nabídky, rozbalíte rozhraní. Například můžete vytvořit nejprve třídu EntityContactManagerRepository a pak pomocí extrahovat rozhraní vygenerovat rozhraní IContactManagerRepository automaticky.

## <a name="using-the-dependency-injection-software-design-pattern"></a>Použití vzoru návrhu pro vkládání závislostí

Teď, když jsme migrovali kód pro přístup k datům do samostatné třídy úložiště, musíme upravit náš kontroler kontaktů, aby tuto třídu používal. Využijeme vzor návrhu softwaru s názvem vkládání závislostí pro použití třídy úložiště v našem řadiči.

Změněný kontroler kontaktů je obsažen v seznamu 3.

**Výpis 3 – Controllers\ContactController.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample3.cs)]

Všimněte si, že kontroler kontaktů v seznamu 3 má dva konstruktory. První konstruktor předá konkrétní instanci rozhraní IContactManagerRepository k druhému konstruktoru. Třída kontroleru kontaktů používá *vkládání závislostí konstruktoru*.

Ta, kterou používá třída EntityContactManagerRepository, je v prvním konstruktoru. Zbytek třídy používá rozhraní IContactManagerRepository místo konkrétní třídy EntityContactManagerRepository.

Díky tomu je v budoucnu snadné přepínat implementace třídy IContactManagerRepository. Pokud chcete použít třídu DataServicesContactRepository namísto třídy EntityContactManagerRepository, stačí upravit první konstruktor.

Vložení závislosti konstruktoru také způsobí, že se třída kontroleru kontaktů velmi testovatelné. V testování částí můžete vytvořit instanci kontroleru kontaktů předáním přípravou implementace třídy IContactManagerRepository. Při sestavování testů jednotek pro aplikaci Správce kontaktů bude tato funkce vkládání závislostí velmi důležitá pro nás v další iteraci.

> [!NOTE] 
> 
> Pokud chcete úplně oddělit třídu kontroleru kontaktů od určité implementace rozhraní IContactManagerRepository, můžete využít výhod rozhraní, které podporuje vkládání závislostí, jako je StructureMap nebo Microsoft. Entity Framework (MEF). Pokud využijete rozhraní injektáže závislosti, nikdy nemusíte odkazovat na konkrétní třídu v kódu.

## <a name="creating-a-service-layer"></a>Vytvoření vrstvy služby

Možná jste si všimli, že naše logika ověřování se pořád smíchá s naší logikou kontroleru v upravené třídě kontroleru v seznamu 3. Z toho důvodu, že je vhodné izolovat naši logiku přístupu k datům, je vhodné izolovat naši logiku ověřování.

K vyřešení tohoto problému můžeme vytvořit samostatnou [*vrstvu služby*](http://martinfowler.com/eaaCatalog/serviceLayer.html). Vrstva služby je samostatná vrstva, kterou můžeme vložit mezi naše řadiče a třídy úložiště. Vrstva služby obsahuje naši obchodní logiku včetně všech našich ověřovacích logik.

ContactManagerService je obsažený v seznamu 4. Obsahuje logiku ověřování z třídy kontroleru kontaktů.

**Výpis 4 – Models\ContactManagerService.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample4.cs)]

Všimněte si, že konstruktor pro ContactManagerService vyžaduje ValidationDictionary. Vrstva služby komunikuje s vrstvou kontroleru prostřednictvím tohoto ValidationDictionary. Když se podíváme na vzor dekoratér, probereme ValidationDictionary detailně v následující části.

Všimněte si také, že ContactManagerService implementuje rozhraní IContactManagerService. Vždy byste měli usilovat o program na rozhraní místo konkrétní třídy. Jiné třídy v aplikaci Správce kontaktů nepracují přímo s třídou ContactManagerService. Místo toho s jednou výjimkou je zbývající část aplikace Správce kontaktů naprogramována na rozhraní IContactManagerService.

Rozhraní IContactManagerService je obsaženo v seznamu 5.

**Výpis 5 – Models\IContactManagerService.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample5.cs)]

Upravená třída ovladače kontaktů je obsažena v seznamu 6. Všimněte si, že kontroler kontaktů už nekomunikuje s úložištěm ContactManager. Místo toho kontroler kontaktů spolupracuje se službou ContactManager. Každá vrstva je od jiných vrstev izolovaná co nejvíce.

**Výpis 6 – Controllers\ContactController.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample6.cs)]

Naše aplikace už neběží na afoulí jediného principu zodpovědnosti (SRP). Kontroler kontaktů v seznamu 6 byl odstraněn z každé jiné zodpovědnosti než řízení toku provádění aplikace. Veškerá logika ověřování byla odebrána z kontroleru kontaktů a vložena do vrstvy služeb. Veškerá databázová logika byla vložena do vrstvy úložiště.

## <a name="using-the-decorator-pattern"></a>Použití vzoru dekoratér

Chceme být schopni zcela oddělit naši vrstvu služby od naší vrstvy kontroleru. V podstatě by měla být schopná kompilovat naši vrstvu služby v samostatném sestavení z naší vrstvy kontroleru, aniž by bylo potřeba přidat odkaz na naši aplikaci MVC.

Nicméně naše vrstva služby potřebuje být schopná předat zprávy o chybách ověřování zpátky do vrstvy kontroleru. Jak můžeme povolit, aby vrstva služby komunikovala chybové zprávy ověřování bez propojení řadiče a vrstvy služby? Můžeme využít vzor návrhu softwaru s názvem [dekoratér vzor](http://en.wikipedia.org/wiki/Decorator_pattern).

Kontroler používá ModelStateDictionary s názvem ModelState k vyjádření chyb ověřování. Proto je možné zvážit předání ModelState z vrstvy řadiče do vrstvy služby. Použití ModelState ve vrstvě služeb ale by vedlo k tomu, že vaše vrstva služby bude závislá na funkci rozhraní ASP.NET MVC. To by bylo chybné, protože Someday, možná budete chtít použít vrstvu služby s aplikací WPF namísto aplikace ASP.NET MVC. V takovém případě byste nechtěli chtít odkazovat na rozhraní ASP.NET MVC, aby používalo třídu ModelStateDictionary.

Vzor dekoratér umožňuje zabalit existující třídu do nové třídy, aby bylo možné implementovat rozhraní. Náš projekt správce kontaktů obsahuje třídu ModelStateWrapper, která je obsažena v seznamu 7. Třída ModelStateWrapper implementuje rozhraní v seznamu 8.

**Výpis 7 – Models\Validation\ModelStateWrapper.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample7.cs)]

**Výpis 8 – Models\Validation\IValidationDictionary.cs**

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample8.cs)]

Pokud se podíváte na výpis 5, uvidíte, že vrstva služby ContactManager používá výhradně rozhraní IValidationDictionary. Služba ContactManager není závislá na třídě ModelStateDictionary. Když řadič kontaktu vytvoří službu ContactManager, kontroler zabalí své ModelStatey takto:

[!code-csharp[Main](iteration-4-make-the-application-loosely-coupled-cs/samples/sample9.cs)]

## <a name="summary"></a>Souhrn

V této iteraci jsme do aplikace Správce kontaktů nepřidali žádné nové funkce. Cílem této iterace je refaktorování aplikace Správce kontaktů, aby bylo snazší je zachovat a upravit.

Za prvé jsme implementovali vzor návrhu pro software úložiště. Všechny datové kódy pro přístup jsme migrovali do samostatné třídy úložiště ContactManager.

Také jsme zavedli naši logiku ověřování z naší logiky kontroleru. Vytvořili jsme samostatnou vrstvu služby, která obsahuje celý kód pro ověření. Vrstva kontroleru komunikuje s vrstvou služby a vrstva služby komunikuje s vrstvou úložiště.

Když jsme vytvořili vrstvu služby, využili jsme výhod dekoratér vzoru, který izoluje ModelState z naší vrstvy služeb. V naší vrstvě služeb jsme naprogramoval na rozhraní IValidationDictionary namísto ModelState.

Nakonec jsme využili výhod vzoru návrhu, který se nazývá vzor vkládání závislostí. Tento model umožňuje programům naprogramovat rozhraní (abstrakce) místo konkrétních tříd. Implementace vzorového vzoru pro vkládání závislostí také provede náš kód více testovatelné. V další iteraci přidáme testování částí do našeho projektu.

> [!div class="step-by-step"]
> [Předchozí](iteration-3-add-form-validation-cs.md)
> [Další](iteration-5-create-unit-tests-cs.md)

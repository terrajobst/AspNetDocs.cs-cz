---
uid: web-forms/what-is-web-forms
title: Co jsou webové formuláře | Microsoft Docs
author: rick-anderson
description: ''
ms.author: riande
ms.date: 02/21/2014
ms.assetid: 5fa1daf9-1161-4cfa-bd4c-658f48b2c229
msc.legacyurl: /web-forms/what-is-web-forms
msc.type: content
ms.openlocfilehash: 19be419c499759713971a6c77674c924867d1bbc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/06/2020
ms.locfileid: "78636575"
---
# <a name="what-is-web-forms"></a>Co jsou webové formuláře

Webové formuláře ASP.NET jsou součástí architektury webové aplikace ASP.NET a jsou součástí sady [Visual Studio](https://www.asp.net/downloads). Jedná se o jeden ze čtyř programovacích modelů, pomocí kterých můžete vytvářet webové aplikace v ASP.NET, ostatní jsou ASP.NET MVC, ASP.NET webové stránky a ASP.NET jednostránkové aplikace.

Webové formuláře jsou stránky, které vaši uživatelé požadují pomocí prohlížeče. Tyto stránky lze zapsat pomocí kombinace jazyka HTML, skriptu klienta, serverových ovládacích prvků a kódu serveru. Když si uživatel vyžádá stránku, zkompiluje a provede na serveru rozhraním a poté rozhraní generuje kód HTML, který může prohlížeč vykreslit. Stránka webových formulářů ASP.NET prezentuje informace uživateli v jakémkoli prohlížeči nebo klientském zařízení.

Pomocí sady Visual Studio můžete vytvářet webové formuláře ASP.NET. Integrované vývojové prostředí (IDE) sady Visual Studio umožňuje přetahovat ovládací prvky serveru pro rozložení stránky webových formulářů. Pak můžete snadno nastavit vlastnosti, metody a události ovládacích prvků na stránce nebo samotné stránky. Tyto vlastnosti, metody a události se používají k definování chování webové stránky, vzhledu a chování. Chcete-li napsat kód serveru pro zpracování logiky stránky, můžete použít jazyk rozhraní .NET, například Visual Basic nebo C#.

> [!NOTE] 
> 
> Dokumentace k ASP.NET a sadě Visual Studio zahrnuje několik verzí. Témata, která zvýrazňují funkce z předchozích verzí, můžou být užitečná pro vaše aktuální úlohy a scénáře s využitím nejnovějších verzí.

**Webové formuláře ASP.NET jsou:** 

- Na základě Microsoft ASP.NET technologie, kdy kód, který běží na serveru, dynamicky generuje výstup webové stránky do prohlížeče nebo klientského zařízení.
- Kompatibilní s jakýmkoli prohlížečem nebo mobilním zařízením. Webová stránka ASP.NET automaticky vykreslí správné soubory HTML kompatibilní s prohlížečem pro funkce, jako jsou styly, rozložení a tak dále.
- Kompatibilní s jakýmkoli jazykem podporovaným modulem CLR (Common Language Runtime) .NET, jako je například C#Microsoft Visual Basic a Microsoft Visual.
- Postavené na Microsoft .NET Framework. To poskytuje všechny výhody rozhraní, včetně spravovaného prostředí, zabezpečení typů a dědičnosti.
- Flexibilní, protože do nich můžete přidat ovládací prvky vytvořené uživatelem a třetí stranou.

**ASP.NET webové formuláře nabídky:** 

- Oddělení HTML a jiného kódu uživatelského rozhraní z aplikační logiky.
- Bohatá sada serverových ovládacích prvků pro běžné úlohy, včetně přístupu k datům.
- Výkonná datová vazba s skvělou podporou nástrojů.
- Podpora skriptování na straně klienta, které se spouští v prohlížeči.
- Podpora nejrůznějších funkcí, včetně směrování, zabezpečení, výkonu, mezinárodní správy, testování, ladění, manipulace s chybami a správy stavů.

## <a name="aspnet-web-forms-helps-you-overcome-challenges"></a>Webové formuláře ASP.NET vám pomůžou překonat problémy.

Programování webových aplikací představuje problémy, které obvykle nevzniknou při programování tradičních klientských aplikací. Mezi problémy patří:

- **Implementace formátovaného webového uživatelského rozhraní** – může být obtížné a zdlouhavé pro návrh a implementaci uživatelského rozhraní pomocí základních funkcí HTML, zejména pokud má stránka komplexní rozložení, velký objem dynamického obsahu a plnohodnotné interaktivní objekty uživatele.
- **Oddělení klienta a serveru** – v rámci webové aplikace jsou klienti (prohlížeč) a server různých programů často spuštěny na různých počítačích (a dokonce i v různých operačních systémech). V důsledku toho dvě poloviny aplikace sdílejí velmi málo informací; můžou komunikovat, ale obvykle vyměňují jenom malé bloky jednoduchých informací.
- **Bezstavové provádění** – když webový server obdrží požadavek na stránku, vyhledá stránku, zpracuje ji, pošle ji do prohlížeče a pak zahodí všechny informace o stránce. Pokud uživatel znovu vyžádá stejnou stránku, server zopakuje celou sekvenci a znovu zpracuje stránku od začátku. Další způsob je, že server nemá na paměti žádné stránky, které zpracoval – stránka je Bezstavová. Proto pokud aplikace potřebuje zachovat informace o stránce, může dojít k problému bez stavové povahy.
- **Neznámé možnosti klienta** – v mnoha případech jsou webové aplikace přístupné pro mnoho uživatelů pomocí různých prohlížečů. Prohlížeče mají různé možnosti, takže je obtížné vytvořit aplikaci, která bude fungovat stejně dobře i na všech těchto prohlížečích.
- **Komplikace při přístupu k datům** – čtení z a zápis do zdroje dat v tradičních webových aplikacích může být komplikované a náročné na prostředky.
- **Komplikace s škálovatelností** – v mnoha případech webové aplikace navržené s existujícími metodami nevyhovují cílům škálovatelnosti kvůli nedostatku kompatibility mezi různými součástmi aplikace. To je často běžný bod selhání pro aplikace v rámci velkého růstového cyklu.

Splnění těchto výzev pro webové aplikace může vyžadovat značnou dobu a úsilí. Webové formuláře ASP.NET a rozhraní ASP.NET řeší tyto výzvy následujícími způsoby:

- **Intuitivní a konzistentní objektový model** – architektura stránky ASP.NET prezentuje objektový model, který vám umožní považovat vaše formuláře za jednotku, ne jako samostatné části klienta a serveru. V tomto modelu můžete stránku programovat intuitivnějším způsobem než v tradičních webových aplikacích, včetně možnosti nastavovat vlastnosti pro prvky stránky a reagovat na události. Kromě toho jsou serverové ovládací prvky ASP.NET abstrakcí z fyzického obsahu stránky HTML a z přímé interakce mezi prohlížečem a serverem. Obecně můžete použít serverový ovládací prvek jako způsob práce s ovládacími prvky v klientské aplikaci a nemusíte se domnívat, jak vytvořit HTML pro prezentování a zpracování ovládacích prvků a jejich obsahu.
- **Model programování řízený událostmi** – webové formuláře ASP.NET přinášejí webovým aplikacím známý model pro psaní obslužných rutin událostí pro události, ke kterým dochází na klientovi nebo na serveru. Rozhraní stránky ASP.NET tento model vyabstrakce takovým způsobem, že základní mechanismus pro zachycení události v klientovi, jeho přenos na server a volání příslušné metody je vše, co je pro vás automatické a neviditelné. Výsledkem je jasná, snadno psaná struktura kódu, která podporuje vývoj řízený událostmi.
- **Intuitivní Správa stavu** – rozhraní stránky ASP.NET automaticky zpracovává úlohu údržby stavu vaší stránky a jejích ovládacích prvků a poskytuje explicitní způsoby, jak zachovat stav informací specifických pro aplikaci. To se provádí bez těžkého využívání prostředků serveru a dá se implementovat s nebo bez posílání souborů cookie do prohlížeče.
- **Aplikace nezávislé na prohlížeči** – rozhraní stránky ASP.NET umožňuje vytvořit na serveru veškerou aplikační logiku a eliminovat nutnost explicitního kódu pro rozdíly v prohlížečích. Pořád ale umožňuje využít výhod funkcí specifických pro prohlížeč, a to pomocí psaní kódu na straně klienta, který poskytuje Vylepšený výkon a bohatší klientské prostředí.
- **.NET Framework podporu modulu CLR** – rozhraní stránky ASP.NET je postavené na .NET Framework, takže je k dispozici celá rozhraní pro všechny aplikace ASP.NET. Vaše aplikace může být napsána v jakémkoli jazyce, který je kompatibilní s modulem runtime. Přístup k datům je navíc zjednodušený pomocí infrastruktury přístupu k datům poskytované .NET Framework, včetně ADO.NET.
- **.NET Framework škálovatelný výkon serveru** – rozhraní stránky ASP.NET umožňuje škálovat webové aplikace z jednoho počítače na webový server s více počítači a čistě i bez komplikovaných změn v logice aplikace.

## <a name="features-of-aspnet-web-forms"></a>Funkce webových formulářů ASP.NET

- **Serverový ovládací**prvek – ovládací prvky webového serveru ASP.NET jsou objekty na webových stránkách ASP.NET, které se spouštějí při vyžádání stránky a vykreslení značek do prohlížeče. Mnoho ovládacích prvků webového serveru je podobné známým prvkům HTML, jako jsou tlačítka a textová pole. Další ovládací prvky zahrnují složité chování, například ovládací prvky kalendáře a ovládací prvky, které můžete použít pro připojení ke zdrojům dat a zobrazení dat.
- **Stránky předlohy**– hlavní stránky ASP.NET umožňují vytvořit konzistentní rozložení stránek ve vaší aplikaci. Jedna hlavní stránka definuje vzhled a chování a standardní chování, které chcete mít u všech stránek (nebo skupiny stránek) ve vaší aplikaci. Pak můžete vytvořit jednotlivé stránky obsahu, které obsahují obsah, který chcete zobrazit. Když uživatelé požadují stránky obsahu, sloučí se se stránkou předlohy, aby vytvářely výstup, který kombinuje rozložení stránky předlohy s obsahem ze stránky obsahu.
- **Práce s daty**– ASP.NET poskytuje mnoho možností pro ukládání, načítání a zobrazování dat. V aplikaci webových formulářů ASP.NET můžete použít ovládací prvky vázané na data pro automatizaci prezentace nebo zadání dat v prvcích uživatelského rozhraní webových stránek, jako jsou tabulky a textová pole a rozevírací seznamy.
- **Členství**– ASP.NET identity ukládá přihlašovací údaje vašich uživatelů v databázi vytvořené aplikací. Když se uživatelé přihlásí, aplikace ověří své přihlašovací údaje čtením databáze. Složka *účtu* vašeho projektu obsahuje soubory, které implementují různé části členství: registrace, přihlášení, změna hesla a autorizace přístupu. Webové formuláře ASP.NET navíc podporují OAuth a OpenID. Tato vylepšení ověřování umožňují uživatelům přihlašovat se k webu pomocí stávajících přihlašovacích údajů, z těchto účtů jako Facebook, Twitter, Windows Live a Google. Ve výchozím nastavení šablona vytvoří databázi členství pomocí výchozího názvu databáze na instanci SQL Server Express LocalDB, server pro vývoj databáze, který je součástí Visual Studio Express 2013 pro web.
- **Klientské skripty a klientské architektury**– serverové funkce ASP.NET můžete vylepšit zahrnutím funkcí klientského skriptu na stránky webových formulářů ASP.NET. Klientský skript můžete použít k zajištění bohatšího a lépe reagujícího uživatelského rozhraní uživatelům. Pomocí klientského skriptu můžete také provádět asynchronní volání na webový server, zatímco stránka běží v prohlížeči.
- **Směrování – směrování**adres URL umožňuje nakonfigurovat aplikaci tak, aby přijímala adresy URL požadavků, které nemapují fyzické soubory. Adresa URL požadavku je jednoduše adresa URL, kterou uživatel zadá do prohlížeče, aby našli stránku na vašem webu. Směrování můžete použít k definování adres URL, které jsou sémanticky smysluplné pro uživatele a které můžou pomáhat s optimalizací vyhledávání na modulech (SEO).
- **Správa stavu**– webové formuláře ASP.NET obsahují několik možností, které vám pomůžou zachovat data na jednotlivých stránkách i v rámci celé aplikace.
- **Zabezpečení**– důležitou součástí vývoje bezpečnější aplikace je seznámit se s hrozbami. Společnost Microsoft vyvinula způsob, jak zařadit hrozby do kategorií: falšování identity, manipulace, odmítnutí, zpřístupnění informací, odepření služby, zvýšení oprávnění (Rozteč). Ve webových formulářích ASP.NET můžete přidat body rozšiřitelnosti a možnosti konfigurace, které vám umožní přizpůsobit různá bezpečnostní chování ve webových formulářích ASP.NET.
- **Výkon**– výkon může být klíčovým faktorem v úspěšném webu nebo projektu. Webové formuláře ASP.NET umožňují upravovat výkon související se zpracováním stránky a řízení serveru, správou stavu, přístupem k datům, konfigurací aplikace a načítáním a efektivními postupy kódování.
- **Mezinárodní**verze – webové formuláře ASP.NET umožňují vytvářet webové stránky, které mohou získat obsah a další data na základě nastavení preferovaného jazyka pro prohlížeč nebo na základě explicitního výběru jazyka uživatele. Obsah a další data se označují jako prostředky a tato data je možné ukládat do souborů prostředků nebo jiných zdrojů. Na stránce webových formulářů ASP.NET nakonfigurujete ovládací prvky, aby získaly hodnoty vlastností z prostředků. V době běhu jsou výrazy prostředků nahrazeny prostředky z příslušného lokalizovaného souboru prostředků.
- **Ladění a zpracování chyb**– ASP.NET obsahuje funkce, které vám pomohou diagnostikovat problémy, které mohou nastat v aplikaci webového formuláře. Ladění a zpracování chyb jsou ve webových formulářích ASP.NET dobře podporované, takže vaše aplikace se budou kompilovat a efektivně spouštět.
- **Nasazení a hostování**– Visual Studio, ASP.NET, Azure a IIS poskytují nástroje, které vám pomůžou s procesem nasazení a hostování aplikace webových formulářů.

## <a name="deciding-when-to-create-a-web-forms-application"></a>Rozhodnutí o tom, kdy vytvořit aplikaci webových formulářů

Je třeba pečlivě zvážit, zda implementovat webovou aplikaci pomocí modelu webového formuláře ASP.NET nebo jiného modelu, jako je například rozhraní ASP.NET MVC. Architektura MVC nenahrazuje model webových formulářů – pro webové aplikace lze využít oba tyto přístupy. Než se rozhodnete použít model webových formulářů nebo rozhraní MVC pro určitý web, zvažte výhody každého přístupu.

### <a name="advantages-of-a-web-forms-based-web-application"></a>Výhody webové aplikace využívající webové formuláře

Architektura využívající webové formuláře nabízí následující výhody:

- Podporuje model událostí, který zachovává stav prostřednictvím protokolu HTTP, což je výhodné pro vývoj obchodních webových aplikací. Aplikace využívající webové formuláře poskytuje desítky událostí, které jsou podporovány stovkami ovládacích prvků serveru.
- Využívá vzor Page Controller, který přidává funkce jednotlivým stránkám. Další informace najdete v tématu [kontroler stránky](https://go.microsoft.com/fwlink/?LinkId=106359 "Kontroler stránky") na webu MSDN.
- Používá zobrazení stavů nebo serverových formulářů, které usnadňují správu informací o stavu.
- Dobře se hodí pro menší týmy webových vývojářů a návrhářů, které chtějí využít nabídky velkého množství komponent vhodných k rychlému vývoji aplikací.
- Obecně platí, že pro vývoj aplikací je méně složitá, protože komponenty (třída **stránky** , ovládací prvky atd.) jsou pevně integrované a obvykle vyžadují méně kódu než model MVC.

### <a name="advantages-of-an-mvc-based-web-application"></a>Výhody webové aplikace využívající architekturu MVC

Architektura ASP.NET MVC nabízí následující výhody:

- Rozdělením na model, zobrazení a kontroler usnadňuje správu složitých aplikací.
- Nevyužívá stav zobrazení ani formuláře umístěné na serveru. Z tohoto důvodu je architektura MVC ideální pro vývojáře, kteří chtějí mít plnou kontrolu nad chováním aplikace.
- Využívá vzor Front Controller, který zpracovává požadavky webové aplikace prostřednictvím jediného kontroleru. To umožňuje návrh aplikací podporujících infrastrukturu s rozsáhlým směrováním. Další informace najdete v části [front Controller](https://go.microsoft.com/fwlink/?LinkId=106357 "Front-Controller") na webu MSDN.
- Poskytuje lepší podporu pro vývoj řízený testováním (TDD).
- Funguje dobře pro webové aplikace, které jsou podporovány velkými týmy vývojářů a webovými návrháři, kteří potřebují vysoký stupeň kontroly nad chováním aplikace.
